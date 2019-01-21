[Kubernetes](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/) is an open-source system for automating deployment, scaling, and management of containerized applications. Kubernetes is also referred to as k8s.

## Kubernetes for Arch Linux

There are several AUR packages for Kubernetes on Arch Linux:

*   [kubernetes](https://aur.archlinux.org/packages/kubernetes/): It builds the go-source code of Kubernetes from the GitHub.

*   [kubernetes-bin](https://aur.archlinux.org/packages/kubernetes-bin/): It installs the pre-built binaries and configurations of the kubernetes package without requiring to build them.

## Kubectl plugins for Arch Linux

[Kubectl](https://kubernetes.io/docs/reference/kubectl/overview/) plugins are independent binaries that can be used to extend the Kubectl's functionalities by providing additional subcommands.

There are AUR packages for Kubectl plugins on Arch Linux:

*   [kubectl-trace-git](https://aur.archlinux.org/packages/kubectl-trace-git/): Schedule bpftrace programs on your kubernetes cluster using the kubectl.

## Basic Configuration of Kubernetes for Arch Linux VMs

For a sample of configuration, please see [here](https://github.com/kubernetes/kubeadm/issues/465).