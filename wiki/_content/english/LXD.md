**[LXD](https://linuxcontainers.org/lxd/)** is a container "hypervisor" and a new user experience for [Linux Containers](/index.php/Linux_Containers "Linux Containers").

## Contents

*   [1 Setup](#Setup)
    *   [1.1 Required software](#Required_software)
    *   [1.2 Sub{u,g}id configuration](#Sub.7Bu.2Cg.7Did_configuration)
    *   [1.3 Accessing LXD as a unprivileged user](#Accessing_LXD_as_a_unprivileged_user)
    *   [1.4 LXD Networking](#LXD_Networking)
*   [2 Basic usage](#Basic_usage)
    *   [2.1 First steps](#First_steps)
*   [3 See also](#See_also)

## Setup

### Required software

Install [LXC](/index.php/LXC "LXC") and the [lxd](https://aur.archlinux.org/packages/lxd/) package, then [start](/index.php/Start "Start") `lxd.service`.

Verify that the running kernel is properly configured to run a container:

```
$ lxc-checkconfig

```

Due to security concerns, the default Arch kernel does **not** ship with the ability to run containers as an unprivileged user. LXD however needs this ability to run. You can either build a kernel yourself that has `CONFIG_USER_NS` enabled, or use [linux-user-ns-enabled](https://aur.archlinux.org/packages/linux-user-ns-enabled/) from the [AUR](/index.php/AUR "AUR").

### Sub{u,g}id configuration

You will need sub{u,g}ids for root, so that LXD can create the unprivileged containers:

```
$ echo "root:1000000:65536" | sudo tee -a /etc/subuid /etc/subgid

```

### Accessing LXD as a unprivileged user

By default the LXD daemon allows users in the `lxd` group access, so add your user to the group:

```
$ usermod -a -G lxd <user>

```

### LXD Networking

LXD uses LXC's networking capabilities. By default it connects containers to the `lxcbr0` network device. Refer to the LXC documentation on [network configuration](/index.php/Linux_Containers#Host_Network_Configuration "Linux Containers") to set up a bridge for your containers.

If you want to use a different interface than `lxcbr0` edit the default using the lxc command line tool:

```
$ lxc profile edit default

```

An editor will open with a config file that by default contains:

```
name: default
config: {}
devices:
  eth0:
    name: eth0
    nictype: bridged
    parent: lxcbr0
    type: nic

```

You can set the `parent` parameter to whichever bridge you want LXD to attach the containers to by default.

## Basic usage

### First steps

LXD has two parts, the daemon (the lxd binary), and the client (the lxc binary). Now that the daemon is all configured and running, you can import an image:

```
$ lxd-images import ubuntu --alias ubuntu

```

With that image imported into LXD, you can now start containers:

```
$ lxc launch ubuntu

```

Alternatively, you can also use a remote LXD host as a source of images. Those will be automatically cached for you for up at container startup time:

```
$ remote add images images.linuxcontainers.org
$ launch images:centos/7/amd64 centos

```

## See also

*   [The official LXD homepage](https://linuxcontainers.org/lxd/)
*   [The LXD GitHub page](https://github.com/lxc/lxd)