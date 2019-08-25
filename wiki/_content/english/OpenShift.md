[OpenShift](https://www.openshift.com) is a [Kubernetes](/index.php/Kubernetes "Kubernetes") distribution from RedHat

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Server](#Server)
    *   [1.2 Client](#Client)
*   [2 Tips and tricks](#Tips_and_tricks)
    *   [2.1 Troubleshoot network traffic of a container](#Troubleshoot_network_traffic_of_a_container)

## Installation

### Server

[minishift](https://aur.archlinux.org/packages/minishift/) - Run a single-node OpenShift cluster inside a VM (use [VirtualBox](/index.php/VirtualBox "VirtualBox") or [KVM](/index.php/KVM "KVM").

### Client

[origin-client](https://aur.archlinux.org/packages/origin-client/) - Provides the `oc` command.

## Tips and tricks

### Troubleshoot network traffic of a container

In Kubernetes, each shares its network layer with other containers in the same pod. You can install a container with [tcpdump](/index.php?title=Tcpdump&action=edit&redlink=1 "Tcpdump (page does not exist)") in the same pod, and then use `oc rsh` to connect to the container and monitor the traffic.

See [Using sidecars to analyze and debug network traffic in OpenShift](https://developers.redhat.com/blog/2019/02/27/sidecars-analyze-debug-network-traffic-kubernetes-pod) for more details.