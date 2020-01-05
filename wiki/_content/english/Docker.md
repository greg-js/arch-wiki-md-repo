Related articles

*   [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")
*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")
*   [Vagrant](/index.php/Vagrant "Vagrant")

[Docker](https://en.wikipedia.org/wiki/Docker_(software) is a utility to pack, ship and run any application as a lightweight container.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Storage driver](#Storage_driver)
    *   [2.2 Remote API](#Remote_API)
        *   [2.2.1 Remote API with systemd](#Remote_API_with_systemd)
    *   [2.3 Daemon socket configuration](#Daemon_socket_configuration)
    *   [2.4 Proxies](#Proxies)
        *   [2.4.1 Proxy configuration](#Proxy_configuration)
        *   [2.4.2 Container configuration](#Container_configuration)
    *   [2.5 Configuring DNS](#Configuring_DNS)
    *   [2.6 Running Docker with a manually-defined network on systemd-networkd](#Running_Docker_with_a_manually-defined_network_on_systemd-networkd)
    *   [2.7 Images location](#Images_location)
    *   [2.8 Insecure registries](#Insecure_registries)
*   [3 Images](#Images)
    *   [3.1 Arch Linux](#Arch_Linux)
    *   [3.2 Debian](#Debian)
        *   [3.2.1 Manually](#Manually)
*   [4 Remove Docker and images](#Remove_Docker_and_images)
*   [5 Run GPU accelerated Docker containers with NVIDIA GPUs](#Run_GPU_accelerated_Docker_containers_with_NVIDIA_GPUs)
    *   [5.1 With NVIDIA Container Toolkit (recommended)](#With_NVIDIA_Container_Toolkit_(recommended))
    *   [5.2 With NVIDIA Container Runtime](#With_NVIDIA_Container_Runtime)
    *   [5.3 With nvidia-docker (deprecated)](#With_nvidia-docker_(deprecated))
*   [6 Useful tips](#Useful_tips)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 docker0 Bridge gets no IP / no internet access in containers](#docker0_Bridge_gets_no_IP_/_no_internet_access_in_containers)
    *   [7.2 Default number of allowed processes/threads too low](#Default_number_of_allowed_processes/threads_too_low)
    *   [7.3 Error initializing graphdriver: devmapper](#Error_initializing_graphdriver:_devmapper)
    *   [7.4 Failed to create some/path/to/file: No space left on device](#Failed_to_create_some/path/to/file:_No_space_left_on_device)
    *   [7.5 Invalid cross-device link in kernel 4.19.1](#Invalid_cross-device_link_in_kernel_4.19.1)
    *   [7.6 CPUACCT missing in docker with Linux-ck](#CPUACCT_missing_in_docker_with_Linux-ck)
    *   [7.7 Docker-machine fails to create virtual machines using the virtualbox driver](#Docker-machine_fails_to_create_virtual_machines_using_the_virtualbox_driver)
    *   [7.8 Starting Docker breaks KVM bridged networking](#Starting_Docker_breaks_KVM_bridged_networking)
*   [8 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [docker](https://www.archlinux.org/packages/?name=docker) package or, for the development version, the [docker-git](https://aur.archlinux.org/packages/docker-git/) package. Next [start](/index.php/Start "Start") and enable `docker.service` and verify operation:

```
# docker info

```

Note that starting the docker service may fail if you have an active VPN connection due to IP conflicts between the VPN and Docker's bridge and overlay networks. If this is the case, try disconnecting the VPN before starting the docker service. You may reconnect the VPN immediately afterwards. [You can also try to deconflict the networks.](https://stackoverflow.com/questions/45692255/how-make-openvpn-work-with-docker)

If you want to be able to run docker as a regular user, add your user to the `docker` [user group](/index.php/User_group "User group").

**Warning:** Anyone added to the `docker` group is root equivalent. More information [here](https://github.com/docker/docker/issues/9976) and [here](https://docs.docker.com/engine/security/security/).

## Configuration

### Storage driver

The docker storage driver (or graph driver) has a huge impact on performance. Its job is to store layers of container images efficiently, that is when several images share a layer, only one layer uses disk space. The compatible option, `devicemapper` offers suboptimal performance, which is outright terrible on rotating disks. Additionally, `devicemapper` is not recommended in production.

As Arch linux ships new kernels, there is no point using the compatibility option. A good, modern choice is `overlay2`.

To see the current storage driver, run `# docker info | grep -i storage`; modern docker installations should already use `overlay2` by default.

To set your own choice of storage driver, edit `/etc/docker/daemon.json` (create it if it does not exist):

 `/etc/docker/daemon.json` 
```
{
  "storage-driver": "overlay2"
}
```

Afterwards, [restart](/index.php/Restart "Restart") docker.

Further information on options is available on the [user guide](https://docs.docker.com/engine/userguide/storagedriver/selectadriver/). For more information about options in `daemon.json` see [dockerd documentation](https://docs.docker.com/engine/reference/commandline/dockerd/#daemon-configuration-file).

### Remote API

To open the Remote API to port `4243` manually, run:

```
# /usr/bin/dockerd -H tcp://0.0.0.0:4243 -H unix:///var/run/docker.sock

```

The `-H tcp://0.0.0.0:4243` part is for opening the Remote API.

The `-H unix:///var/run/docker.sock` part is for host machine access via terminal.

#### Remote API with systemd

To start the remote API with the docker daemon, create a [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") with the following content:

 `/etc/systemd/system/docker.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H tcp://0.0.0.0:4243 -H unix:///var/run/docker.sock
```

### Daemon socket configuration

The *docker* daemon listens to a [Unix socket](https://en.wikipedia.org/wiki/Unix_domain_socket "wikipedia:Unix domain socket") by default. To listen on a specified port instead, create a [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") with the following content:

 `/etc/systemd/system/docker.socket.d/socket.conf` 
```
[Socket]
ListenStream=0.0.0.0:2375
```

### Proxies

Proxy configuration is broken down into two. First is the host configuration of the Docker daemon, second is the configuration required for your container to see your proxy.

#### Proxy configuration

Create a [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") with the following content:

 `/etc/systemd/system/docker.service.d/proxy.conf` 
```
[Service]
Environment="HTTP_PROXY=192.168.1.1:8080"
Environment="HTTPS_PROXY=192.168.1.1:8080"
```

**Note:** This assumes `192.168.1.1` is your proxy server, do not use `127.0.0.1`.

Verify that the configuration has been loaded:

 `# systemctl show docker --property Environment`  `Environment=HTTP_PROXY=192.168.1.1:8080 HTTPS_PROXY=192.168.1.1:8080` 

#### Container configuration

The settings in the `docker.service` file will not translate into containers. To achieve this you must set `ENV` variables in your `Dockerfile` thus:

```
FROM archlinux/base
ENV http_proxy="http://192.168.1.1:3128"
ENV https_proxy="https://192.168.1.1:3128"

```

[Docker](https://docs.docker.com/engine/reference/builder/#env) provide detailed information on configuration via `ENV` within a Dockerfile.

### Configuring DNS

By default, docker will make `resolv.conf` in the container match `/etc/resolv.conf` on the host machine, filtering out local addresses (e.g. `127.0.0.1`). If this yields an empty file, then [Google DNS servers](https://developers.google.com/speed/public-dns/) are used. If you are using a service like [dnsmasq](/index.php/Dnsmasq "Dnsmasq") to provide name resolution, you may need to add an entry to the `/etc/resolv.conf` for docker's network interface so that it is not filtered out.

### Running Docker with a manually-defined network on systemd-networkd

If you manually configure your network using [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") version **220 or higher**, containers you start with Docker may be unable to access your network. Beginning with version 220, the forwarding setting for a given network (`net.ipv4.conf.<interface>.forwarding`) defaults to `off`. This setting prevents IP forwarding. It also conflicts with Docker which enables the `net.ipv4.conf.all.forwarding` setting within a container.

A workaround is to edit the `<interface>.network` file in `/etc/systemd/network/`, adding `IPForward=kernel` on the Docker host:

 `/etc/systemd/network/<interface>.network` 
```
[Network]
...
IPForward=kernel
...
```

This configuration allows IP forwarding from the container as expected.

### Images location

By default, docker images are located at `/var/lib/docker`. They can be moved to other partitions. First, [stop](/index.php/Stop "Stop") the `docker.service`.

If you have run the docker images, you need to make sure the images are unmounted totally. Once that is completed, you may move the images from `/var/lib/docker` to the target destination.

Then add a [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") for the `docker.service`, adding the `--data-root` parameter to the `ExecStart`:

 `/etc/systemd/system/docker.service.d/docker-storage.conf` 
```
[Service]
ExecStart= 
ExecStart=/usr/bin/dockerd --data-root=*/path/to/new/location/docker* -H fd://
```

### Insecure registries

If you decide to use a self signed certificate for your private registry, Docker will refuse to use it until you declare that you trust it. Add a [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") for the `docker.service`, adding the `--insecure-registry` parameter to the `dockerd`:

 `/etc/systemd/system/docker.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H fd:// --insecure-registry my.registry.name:5000
```

## Images

### Arch Linux

The following command pulls the [archlinux/base](https://hub.docker.com/r/archlinux/base/) x86_64 image. This is a stripped down version of Arch core without network, etc.

```
# docker pull archlinux/base

```

See also [README.md](https://github.com/archlinux/archlinux-docker/blob/master/README.md).

For a full Arch base, clone the repo from above and build your own image.

```
$ git clone [https://github.com/archlinux/archlinux-docker.git](https://github.com/archlinux/archlinux-docker.git)

```

Make sure that the [devtools](https://www.archlinux.org/packages/?name=devtools) package is installed.

Edit the `packages` file so it only contains 'base'. Then run:

```
# make docker-image

```

### Debian

The following command pulls the [debian](https://hub.docker.com/r/_/debian/) x86_64 image.

```
# docker pull debian

```

#### Manually

Build Debian image with [debootstrap](https://www.archlinux.org/packages/?name=debootstrap):

```
# mkdir jessie-chroot
# debootstrap jessie ./jessie-chroot [http://http.debian.net/debian/](http://http.debian.net/debian/)
# cd jessie-chroot
# tar cpf - . | docker import - debian
# docker run -t -i --rm debian /bin/bash

```

## Remove Docker and images

In case you want to remove Docker entirely you can do this by following the steps below:

**Note:** Do not just copy paste those commands without making sure you know what you are doing.

Check for running containers:

```
# docker ps

```

List all containers running on the host for deletion:

```
# docker ps -a

```

Stop a running container:

```
# docker stop <CONTAINER ID>

```

Killing still running containers:

```
# docker kill <CONTAINER ID>

```

Delete all containers listed by ID:

```
# docker rm <CONTAINER ID>

```

List all Docker images:

```
# docker images

```

Delete all images by ID:

```
# docker rmi <IMAGE ID>

```

Delete all images, containers, volumes, and networks that are not associated with a container (dangling):

```
# docker system prune

```

To additionally remove any stopped containers and all unused images (not just dangling ones), add the -a flag to the command:

```
# docker system prune -a

```

Delete all Docker data (purge directory):

```
# rm -R /var/lib/docker

```

## Run GPU accelerated Docker containers with NVIDIA GPUs

### With NVIDIA Container Toolkit (recommended)

Starting from Docker version 19.03, NVIDIA GPUs are natively supported as Docker devices. [NVIDIA Container Toolkit](https://github.com/NVIDIA/nvidia-docker) is the recommended way of running containers that leverage NVIDIA GPUs.

Install the [nvidia-container-toolkit](https://aur.archlinux.org/packages/nvidia-container-toolkit/) package. Next, [restart](/index.php/Restart "Restart") docker. You can now run containers that make use of NVIDIA GPUs using the `--gpus` option:

```
# docker run --gpus all nvidia/cuda:9.0-base nvidia-smi

```

Specify how many GPUs are enabled inside a container:

```
# docker run --gpus 2 nvidia/cuda:9.0-base nvidia-smi

```

Specify which GPUs to use:

```
# docker run --gpus '"device=1,2"' nvidia/cuda:9.0-base nvidia-smi

```

or

```
# docker run --gpus '"device=UUID-ABCDEF,1"' nvidia/cuda:9.0-base nvidia-smi

```

Specify a capability (graphics, compute, ...) for the container (though this is rarely if ever used this way):

```
# docker run --gpus all,capabilities=utility nvidia/cuda:9.0-base nvidia-smi

```

For more information see [README.md](https://github.com/NVIDIA/nvidia-docker/blob/master/README.md) and [Wiki](https://github.com/NVIDIA/nvidia-docker/wiki).

### With NVIDIA Container Runtime

Install the [nvidia-container-runtime](https://aur.archlinux.org/packages/nvidia-container-runtime/) package. Next, register the NVIDIA runtime by editing `/etc/docker/daemon.json`

 `/etc/docker/daemon.json` 
```
{
  "runtimes": {
    "nvidia": {
      "path": "/usr/bin/nvidia-container-runtime",
      "runtimeArgs": []
    }
  }
}
```

and then [restart](/index.php/Restart "Restart") docker.

The runtime can also be registered via a command line option to *dockerd*:

```
# /usr/bin/dockerd --add-runtime=nvidia=/usr/bin/nvidia-container-runtime

```

Afterwards GPU accelerated containers can be started with

```
# docker run --runtime=nvidia nvidia/cuda:9.0-base nvidia-smi

```

or (required Docker version 19.03 or higher)

```
# docker run --gpus all nvidia/cuda:9.0-base nvidia-smi

```

See also [README.md](https://github.com/NVIDIA/nvidia-container-runtime/blob/master/README.md).

### With nvidia-docker (deprecated)

[nvidia-docker](https://nvidia.github.io/nvidia-docker/) is a wrapper around NVIDIA Container Runtime which registers the NVIDIA runtime by default and provides the *nvidia-docker* command.

To use nvidia-docker, install the [nvidia-docker](https://aur.archlinux.org/packages/nvidia-docker/) package and then [restart](/index.php/Restart "Restart") docker. Containers with NVIDIA GPU support can then be run using any of the following methods:

```
# docker run --runtime=nvidia nvidia/cuda:9.0-base nvidia-smi

```

```
# nvidia-docker run nvidia/cuda:9.0-base nvidia-smi

```

or (required Docker version 19.03 or higher)

```
# docker run --gpus all nvidia/cuda:9.0-base nvidia-smi

```

**Note:** nvidia-docker is a legacy method for running NVIDIA GPU accelerated containers used prior to Docker 19.03 and has been deprecated. If you are using Docker version 19.03 or higher, it is recommended to use [NVIDIA Container Toolkit](#With_NVIDIA_Container_Toolkit_(recommended)) instead.

## Useful tips

To grab the IP address of a running container:

 `$ docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <container-name OR id> `  `172.17.0.37` 

For each running container, the name and corresponding IP address can be listed for use in `/etc/hosts`:

```
#!/usr/bin/env sh
for ID in $(docker ps -q | awk '{print $1}'); do
    IP=$(docker inspect --format="{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}" "$ID")
    NAME=$(docker ps | grep "$ID" | awk '{print $NF}')
    printf "%s %s
" "$IP" "$NAME"
done
```

## Troubleshooting

### docker0 Bridge gets no IP / no internet access in containers

Docker enables IP forwarding by itself, but by default [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") overrides the respective sysctl setting. Set `IPForward=yes` in the network profile. See [Internet sharing#Enable packet forwarding](/index.php/Internet_sharing#Enable_packet_forwarding "Internet sharing") for details.

**Note:**

*   You may need to [restart](/index.php/Restart "Restart") `docker.service` each time you [restart](/index.php/Restart "Restart") `systemd-networkd.service` or `iptables.service`.
*   Also be aware that [nftables](/index.php/Nftables "Nftables") may block docker connections by default. Use `nft list ruleset` to check for blocking rules. `nft flush chain inet filter forward` removes all forwarding rules temporarily. Edit `/etc/nftables.conf` to make changes permanent. Remember to [restart](/index.php/Restart "Restart") `nftables.service` to reload rules from the config file.

### Default number of allowed processes/threads too low

If you run into error messages like

```
# e.g. Java
java.lang.OutOfMemoryError: unable to create new native thread
# e.g. C, bash, ...
fork failed: Resource temporarily unavailable

```

then you might need to adjust the number of processes allowed by systemd. The default is 500 (see `system.conf`), which is pretty small for running several docker containers. [Edit](/index.php/Edit "Edit") the `docker.service` with the following snippet:

 `# systemctl edit docker.service` 
```
[Service]
TasksMax=infinity
```

### Error initializing graphdriver: devmapper

If *systemctl* fails to start docker and provides an error:

```
Error starting daemon: error initializing graphdriver: devmapper: Device docker-8:2-915035-pool is not a thin pool

```

Then, try the following steps to resolve the error. Stop the service, back up `/var/lib/docker/` (if desired), remove the contents of `/var/lib/docker/`, and try to start the service. See the open [GitHub issue](https://github.com/docker/docker/issues/21304) for details.

### Failed to create some/path/to/file: No space left on device

If you are getting an error message like this:

```
ERROR: Failed to create some/path/to/file: No space left on device

```

when building or running a Docker image, even though you do have enough disk space available, make sure:

*   [Tmpfs](/index.php/Tmpfs "Tmpfs") is disabled or has enough memory allocation. Docker might be trying to write files into `/tmp` but fails due to restrictions in memory usage and not disk space.
*   If you are using [XFS](/index.php/XFS "XFS"), you might want to remove the `noquota` mount option from the relevant entries in `/etc/fstab` (usually where `/tmp` and/or `/var/lib/docker` reside). Refer to [Disk quota](/index.php/Disk_quota "Disk quota") for more information, especially if you plan on using and resizing `overlay2` Docker storage driver.
*   XFS quota mount options (`uquota`, `gquota`, `prjquota`, etc.) fail during re-mount of the file system. To enable quota for root file system, the mount option must be passed to initramfs as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `rootflags=`. Subsequently, it should not be listed among mount options in `/etc/fstab` for the root (`/`) filesystem.

**Note:** There are some differences of XFS Quota compared to standard Linux [Disk quota](/index.php/Disk_quota "Disk quota"), [[1]](http://inai.de/linux/adm_quota) may be worth reading.

### Invalid cross-device link in kernel 4.19.1

If commands like *dpkg* fail to run in docker, e.g:

```
dpkg: error: error creating new backup file '/var/lib/dpkg/status-old': Invalid cross-device link

```

Either add a `overlay.metacopy=N` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") or downgrade to 4.18.x until [this issue](https://github.com/docker/for-linux/issues/480) is resolved. More info in the [Arch forum](https://bbs.archlinux.org/viewtopic.php?id=241866).

### CPUACCT missing in docker with Linux-ck

In newer versions of [Linux-ck](/index.php/Linux-ck "Linux-ck") ([some experienced](https://aur.archlinux.org/packages/linux-ck#comment-677316) with 4.19, 4.20 seems general), a change to the MuQSS was made that disables the `CONFIG_CGROUP_CPUACCT` option from the kernel, which makes *some* usage of docker (`run` or `build`) to produce the following error:

 `$ docker run --rm hello-world`  `docker: Error response from daemon: unable to find "cpuacct" in controller set: unknown.` 

This error does not seem to affect the docker daemon, just containers. Read more on [Linux-ck#CPUACCT missing in docker](/index.php/Linux-ck#CPUACCT_missing_in_docker "Linux-ck").

### Docker-machine fails to create virtual machines using the virtualbox driver

In case docker-machine fails to create the VM's using the virtualbox driver, with the following:

```
VBoxManage: error: VBoxNetAdpCtl: Error while adding new interface: failed to open /dev/vboxnetctl: No such file or directory

```

Simply reload the virtualbox via CLI with `vboxreload`.

### Starting Docker breaks KVM bridged networking

This is a [known issue](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=865975). You can use the following workaround:

 `/etc/docker/daemon.json` 
```
{
  "iptables": false
}
```

## See also

*   [Official website](https://www.docker.com)
*   [Arch Linux on docs.docker.com](https://docs.docker.com/engine/installation/linux/archlinux/)
*   [Are Docker containers really secure?](https://opensource.com/business/14/7/docker-security-selinux) — opensource.com
*   [Awesome Docker](https://awesome-docker.netlify.com/)