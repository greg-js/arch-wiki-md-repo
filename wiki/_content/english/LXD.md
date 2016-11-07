**[LXD](https://linuxcontainers.org/lxd/)** is a container "hypervisor" and a new user experience for [Linux Containers](/index.php/Linux_Containers "Linux Containers").

## Contents

*   [1 Setup](#Setup)
    *   [1.1 Required software](#Required_software)
    *   [1.2 Sub{u,g}id configuration](#Sub.7Bu.2Cg.7Did_configuration)
    *   [1.3 Accessing LXD as a unprivileged user](#Accessing_LXD_as_a_unprivileged_user)
    *   [1.4 LXD Networking](#LXD_Networking)
        *   [1.4.1 Example network configuration](#Example_network_configuration)
*   [2 Basic usage](#Basic_usage)
    *   [2.1 First steps](#First_steps)
*   [3 Advance usage](#Advance_usage)
    *   [3.1 Modify processes and files limit](#Modify_processes_and_files_limit)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Launching container without CONFIG_USER_NS](#Launching_container_without_CONFIG_USER_NS)
*   [5 See also](#See_also)

## Setup

### Required software

Install [LXC](/index.php/LXC "LXC") and the [lxd](https://aur.archlinux.org/packages/lxd/) package, then [start](/index.php/Start "Start") `lxd.service`.

Verify that the running kernel is properly configured to run a container:

```
$ lxc-checkconfig

```

Due to security concerns, the default Arch kernel does **not** ship with the ability to run containers as an unprivileged user. LXD however needs this ability to run. You can either build a kernel yourself that has `CONFIG_USER_NS` enabled, or use [linux-userns](https://aur.archlinux.org/packages/linux-userns/) or [linux-lts-userns](https://aur.archlinux.org/packages/linux-lts-userns/) from the [AUR](/index.php/AUR "AUR").

**Note:** You still be able to run containers without CONFIG_USER_NS kernel feature. See: [#Launching container without CONFIG_USER_NS](#Launching_container_without_CONFIG_USER_NS)

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

LXD uses LXC's networking capabilities. By default it connects containers to the `lxcbr0` network device. Refer to the LXC documentation on [network configuration](/index.php/Linux_Containers#Host_network_configuration "Linux Containers") to set up a bridge for your containers.

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

#### Example network configuration

Thanks to @jpic, the LXD package now provides some example networking configuration in `/usr/share/lxd/`. To use this configuration run the following commands:

```
$ ln -s /usr/share/lxd/dnsmasq-lxd.conf /etc/dnsmasq-lxd.conf
$ ln -s /usr/share/lxd/systemd/system/dnsmasq@lxd.service /etc/systemd/system/dnsmasq@lxd.service 
$ ln -s /usr/share/lxd/netctl/lxd  /etc/netctl/lxd
$ ln -s /usr/share/lxd/dbus-1/system.d/dnsmasq-lxd.conf /etc/dbus-1/system.d/dnsmasq-lxd.conf

```

If you use [NetworkManager](/index.php/NetworkManager "NetworkManager"), also symlink the following file:

```
$ ln -s /usr/share/lxd/NetworkManager/dnsmasq.d/lxd.conf /etc/NetworkManager/dnsmasq.d/lxd.conf

```

Change `parent: lxcbr0` to `parent: lxd`:

```
$ lxc profile edit default

```

Finally, [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `dnsmasq@lxd.service` and `netctl@lxd.service`.

If you encounter issue with the provided example configuration, or have suggestions to improve it, please leave a comment on the [lxd](https://aur.archlinux.org/packages/lxd/) page.

## Basic usage

### First steps

LXD has two parts, the daemon (the lxd binary), and the client (the lxc binary). Now that the daemon is all configured and running, you can create a container:

```
$ lxc launch ubuntu:14.04

```

Alternatively, you can also use a remote LXD host as a source of images. One comes pre-configured in LXD, called "images" (images.linuxcontainers.org)

```
$ lxc launch images:centos/7/amd64 centos

```

## Advance usage

### Modify processes and files limit

You may want to increase file descriptor limit or max user processes limit, since default file descriptor limit is 1024 on Archlinux

```
$ sudo systemctl edit lxd

```

And config as follow:

```
[Service]
LimitNOFILE=infinity
LimitNPROC=infinity
TasksMax=infinity

```

Then restart lxd

```
$ sudo systemctl restart lxd

```

## Troubleshooting

### Launching container without CONFIG_USER_NS

For launching images you must provide `security.privileged=true` during image creation:

```
$ lxc launch ubuntu:16.04 ubuntu -c security.privileged=true

```

Or for already existed image you may edit config:

```
$ lxc config edit ubuntu

```

```
name: ubuntu
profiles:
- default
config:
  ...
  security.privileged: "true"
  ...
devices:
  root:
    path: /
    type: disk
ephemeral: false

```

## See also

*   [The official LXD homepage](https://linuxcontainers.org/lxd/)
*   [The LXD GitHub page](https://github.com/lxc/lxd)