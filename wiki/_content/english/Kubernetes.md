[Kubernetes](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/) is an open-source system for automating deployment, scaling, and management of containerized applications. Kubernetes is also referred to as k8s.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Kubernetes for Arch Linux](#Kubernetes_for_Arch_Linux)
*   [2 Kubectl plugins for Arch Linux](#Kubectl_plugins_for_Arch_Linux)
*   [3 Basic configuration](#Basic_configuration)
    *   [3.1 Using kubeadm](#Using_kubeadm)
        *   [3.1.1 Master](#Master)
        *   [3.1.2 Node](#Node)
*   [4 Trouble shooting](#Trouble_shooting)
    *   [4.1 settings behind proxy](#settings_behind_proxy)
    *   [4.2 fatal error: runtime: out of memory](#fatal_error:_runtime:_out_of_memory)
    *   [4.3 error when creating "xxx.yaml": No API token found for service account "default"](#error_when_creating_"xxx.yaml":_No_API_token_found_for_service_account_"default")
    *   [4.4 Error: unable to load server certificate](#Error:_unable_to_load_server_certificate)

## Kubernetes for Arch Linux

There are several AUR packages for Kubernetes on Arch Linux:

*   [kubernetes](https://aur.archlinux.org/packages/kubernetes/): It builds the go-source code of Kubernetes from the GitHub.

*   [kubernetes-bin](https://aur.archlinux.org/packages/kubernetes-bin/): It installs the pre-built binaries and configurations of the kubernetes package without requiring to build them.

## Kubectl plugins for Arch Linux

[Kubectl](https://kubernetes.io/docs/reference/kubectl/overview/) plugins are independent binaries that can be used to extend the Kubectl's functionalities by providing additional subcommands.

There are AUR packages for Kubectl plugins on Arch Linux:

*   [kubectl-trace-git](https://aur.archlinux.org/packages/kubectl-trace-git/): Schedule bpftrace programs on your kubernetes cluster using the kubectl.
*   [kubelogin](https://aur.archlinux.org/packages/kubelogin/): Kubectl plugin for Kubernetes OpenID Connect authentication (oidc-login).

## Basic configuration

You may either choose the `kubeadm` helper or manually configuring a kubernetes cluster.

### Using kubeadm

The following guide is for a one-master-one-slave build, where both nodes are in `192.168.122.0/24` network and the master hosts the kubernetes cluster at `192.168.122.1`. Note that pods have their own CIDR, assuming `192.168.123.0/24` here.

#### Master

First, setup the configuration file for kubelet service,

 `/etc/kubernetes/kubelet` 
```
KUBELET_ARGS="--bootstrap-kubeconfig=/etc/kubernetes/bootstrap-kubelet.conf \
              --kubeconfig=/etc/kubernetes/kubelet.conf \
              --config=/var/lib/kubelet/config.yaml \
              --network-plugin=cni \
              --pod-infra-container-image=k8s.gcr.io/pause:3.1"

```

Don't worry for the not yet existing files in the arguments. They will be created during the `kubeadm` initialization process. Note that if you are in a proxy environment or have special DNS settings, you should specify the `resolv.conf` to be used in containers by adding one more argument

 `--resolv-conf=/the/path/to/the/resolv.conf` 

Then, run

 `# kubeadm init --apiserver-advertise-address=192.168.122.1 --pod-network-cidr=192.168.123.0/24` 

It will show the progress of initialization and stuck later, complaining about something like

```
[kubelet-check] It seems like the kubelet isn't running or healthy.
[kubelet-check] The HTTP call equal to 'curl -sSL [http://localhost:10248/healthz'](http://localhost:10248/healthz') failed with error: Get [http://localhost:10248/healthz](http://localhost:10248/healthz): dial tcp 127.0.0.1:10248: connect: connection refused.

```

At this moment, [start](/index.php/Start "Start") `kubelet.service`. It is anticipated that kubelet will launch some kubernetes components, which will be confirmed by `kubeadm`. If done successfully, there should be a message like:

```
Your Kubernetes master has initialized successfully!

```

Then you can configure your account as the administrator of this newly-created kubernetes cluster,

```
$ mkdir -p $HOME/.kube
$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
$ sudo chown $(id -u):$(id -g) $HOME/.kube/config

```

Then you can deploy a pod network. Many choices can be found [here](https://kubernetes.io/docs/concepts/cluster-administration/addons/). Note that all the options have their own default pod network CIDR. Thus, you should modify those settings according to what was given in `--pod-network-cidr`.

Finally, check the health of this master,

```
$ kubectl get componentstatus

```

#### Node

Join the cluster by simply type in the final line of master's successful message,

```
kubeadm join --token <token> 192.168.122.1:6443 --discovery-token-ca-cert-hash sha256:<hash>

```

## Trouble shooting

### settings behind proxy

`kubeadm` reads the `https_proxy`, `http_proxy`, and `no_proxy` environment variables. Kubernetes internal networking should be included in the latest one, for example

```
export no_proxy="192.168.122.0/24,10.96.0.0/12,192.168.123.0/24"

```

where the second one is the default service network CIDR.

You may also need extra CNI plugins

```
$ go get -d github.com/containernetworking/plugins
$ cd ~/go/src/github.com/containernetworking/plugins
$ bash ./build_linux.sh 
# cp bin/* /opt/cni/bin/

```

### fatal error: runtime: out of memory

This might happen when building kubernetes from source. A known trick is to setup a `zram` region:

```
# ￼￼modprobe zram
# echo lz4 > /sys/block/zram0/comp_algorithm
# echo 16G > /sys/block/zram0/disksize
# mkswap --label zram0 /dev/zram0
# swapon --priority 100 /dev/zram0

```

### error when creating "xxx.yaml": No API token found for service account "default"

Please check the details on [stackoverflow](https://stackoverflow.com/questions/31891734/not-able-to-create-pod-in-kubernetes).

### Error: unable to load server certificate

This might happen when start a service. Check if any of the `*.key` files' permission setting is not appropriate.