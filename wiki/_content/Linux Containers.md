# Linux Containers

**LinuX Containers** (**LXC**) is an operating system-level virtualization method for running multiple isolated Linux systems (containers) on a single control host (LXC host). It does not provide a virtual machine, but rather provides a virtual environment that has its own CPU, memory, block I/O, network, etc. space. This is provided by [cgroups](/index.php/Cgroups "Cgroups") features in Linux kernel on LXC host. It is similar to a chroot, but offers much more isolation.

## Contents

*   [1 Setup](#Setup)
    *   [1.1 Required software](#Required_software)
    *   [1.2 Host Network Configuration](#Host_Network_Configuration)
        *   [1.2.1 Example for a wired network](#Example_for_a_wired_network)
        *   [1.2.2 Example for a wireless network](#Example_for_a_wireless_network)
    *   [1.3 Container creation](#Container_creation)
    *   [1.4 Container configuration](#Container_configuration)
        *   [1.4.1 Basic config with networking](#Basic_config_with_networking)
        *   [1.4.2 Systemd considerations (required)](#Systemd_considerations_.28required.29)
            *   [1.4.2.1 Systemd conflicts in the /dev tree](#Systemd_conflicts_in_the_.2Fdev_tree)
            *   [1.4.2.2 Maintain devpts consistency](#Maintain_devpts_consistency)
            *   [1.4.2.3 Prevent excess journald activity](#Prevent_excess_journald_activity)
        *   [1.4.3 Xorg program considerations (optional)](#Xorg_program_considerations_.28optional.29)
        *   [1.4.4 OpenVPN considerations](#OpenVPN_considerations)
*   [2 Managing Containers](#Managing_Containers)
*   [3 Running Xorg programs](#Running_Xorg_programs)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 root login fails](#root_login_fails)
    *   [4.2 no network-connection with veth in container config](#no_network-connection_with_veth_in_container_config)
*   [5 See also](#See_also)

## Setup

### Required software

Install [lxc](https://www.archlinux.org/packages/?name=lxc) and [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) from the [official repositories](/index.php/Official_repositories "Official repositories").

Verify that the running kernel is properly configured to run a container:

```
$ lxc-checkconfig

```

Due to security concerns, the default Arch kernel does NOT ship with the ability to run containers as an unprivileged user; therefore, it is normal to see a **missing** status for "User namespaces" when running the check. See [FS#36969](https://bugs.archlinux.org/task/36969) for this feature request.

### Host Network Configuration

LXCs support different virtual network types. A bridge device on the host is required for most types of virtual networking. The examples of creating a bridge provided below are not meant to be limiting, but illustrative. Users may use other programs to achieve the same results. A wired and wireless example is provided below, but other setups are possible. Users are referred to the [Network bridge](/index.php/Network_bridge "Network bridge") article for additional options.

#### Example for a wired network

[netctl](https://www.archlinux.org/packages/?name=netctl) is available from the [official repositories](/index.php/Official_repositories "Official repositories"). A bridge template can be found in `/etc/netctl/examples` which needs to be edited to match the host network hardware specs and IP ranges of the host network. Below are two example bridge configs, one using a dhcp setup and the other using a static IP setup.

 `/etc/netctl/lxcbridge` 

```
Description="LXC bridge"
Interface=br0
Connection=bridge
BindsToInterfaces=('eno1')
IP=dhcp
SkipForwardingDelay=yes
```

 `/etc/netctl/lxcbridge` 

```
Description="LXC bridge"
Interface=br0
Connection=bridge
BindsToInterfaces=('eno1')
IP=static
Address=192.168.0.2/24
Gateway='192.168.0.1'
DNS=('192.168.0.1')
```

Before attempting to start the bridge, [disable](/index.php/Disable "Disable") the running network interface on the host as the bridge will replace it; this depends on how the host network is configured, common networking examples are shown in [Beginners' guide#Configure the network](/index.php/Beginners%27_guide#Configure_the_network "Beginners' guide").

For users already using netctl to manage an adapter, simply switch-to it:

```
# netctl switch-to lxcbridge
# netctl enable lxcbridge

```

Verify network connectivity on the host before continuing. This can be accomplished with a simple ping:

```
$ ping -c 1 www.google.com

```

#### Example for a wireless network

Wireless networks cannot be bridged directly; a different method must be used in this case. First, a bridge must be created similar to the previous examples, but it should not have any interface defined to it (other than the virtual interface of the container itself, which is done automatically). Assign a static IP address to the bridge, but do not assign a gateway.

The host must be configured to perform NAT using [iptables](/index.php/Iptables "Iptables"):

```
# iptables -t nat -A POSTROUTING -o _wlp3s0_ -j MASQUERADE

```

where `_wlp3s0_` is the name of the wireless interface. [Enable packet forwarding](/index.php/Internet_sharing#Enable_packet_forwarding "Internet sharing"), which is disabled by default.

The remaining steps are similar, except for one thing: for the container, the gateway must be configured to be the IP address of the host (in this example, it was 192.168.0.2). This is specified in `/var/lib/lxc/_container_name_/config` (see the following sections).

### Container creation

Select a template from `/usr/share/lxc/templates` that matches the target distro to containerize. Users wishing to containerize non-Arch distros will need additional packages on the host depending on the target distro:

*   Debian-based: [debootstrap](https://aur.archlinux.org/packages/debootstrap/) from [AUR](/index.php/AUR "AUR").
*   Fedora-based: [yum](https://aur.archlinux.org/packages/yum/) from [AUR](/index.php/AUR "AUR").

Run `lxc-create` to create the container, which installs the root filesystem of the LXC to `/var/lib/lxc/CONTAINER_NAME/rootfs` by default. Example creating an Arch Linux LXC named "playtime":

```
# lxc-create -n playtime -t /usr/share/lxc/templates/lxc-archlinux

```

**Tip:** Users may optionally install [haveged](https://www.archlinux.org/packages/?name=haveged) and [start](/index.php/Start "Start") `haveged.service` to avoid a perceived hang during the setup process while waiting for system entropy to be seeded. Without it, the generation of private/GPG keys can add a lengthy wait to the process.

**Tip:** Users of [Btrfs](/index.php/Btrfs "Btrfs") can append `-B btrfs` to create a Btrfs subvolume for storing containerized rootfs. This comes in handy if cloning containers with the help of `lxc-clone` command. [ZFS](/index.php/ZFS "ZFS") users may use `-B zfs`, correspondingly.

**Tip:** As of July 2015, creating an empty container using `-t none` does not work, see the [bug report](https://bugs.launchpad.net/bugs/1466458). As a workaround one can use `-t /bin/true`.

### Container configuration

#### Basic config with networking

System resources to be virtualized/isolated when a process is using the container are defined in `/var/lib/lxc/CONTAINER_NAME/config`. By default, the creation process will make a minimum setup without networking support. Below is an example config with networking:

 `/var/lib/lxc/playtime/config` 

```
# Template used to create this container: /usr/share/lxc/templates/lxc-archlinux
# Parameters passed to the template:
# For additional config options, please look at lxc.container.conf(5)

## default values
lxc.rootfs = /var/lib/lxc/playtime/rootfs
lxc.utsname = playtime
lxc.arch = x86_64
lxc.include = /usr/share/lxc/config/archlinux.common.conf

## network
lxc.network.type = veth
lxc.network.link = br0
lxc.network.flags = up
lxc.network.ipv4 = 192.168.0.3/24
lxc.network.ipv4.gateway = 192.168.0.1
lxc.network.name = eth0

## mounts
## specify shared filesystem paths in the format below
## make sure that the mount point exists on the lxc
#lxc.mount.entry = /mnt/data/share mnt/data none bind 0 0
#
# if running the same Arch linux on the same architecture it may be
# adventitious to share the package cache directory
#lxc.mount.entry = /var/cache/pacman/pkg var/cache/pacman/pkg none bind 0 0

```

#### Systemd considerations (required)

The following sections explain some quirks that should be addressed. A small bash script is required for this to work, which users should create:

 `/var/lib/lxc/playtime/autodev` 

```
#!/bin/bash
cd ${LXC_ROOTFS_MOUNT}/dev
mkdir net
mknod net/tun c 10 200
chmod 0666 net/tun

```

Make it executable:

```
# chmod +x /var/lib/lxc/playtime/autodev

```

Next, modify `/var/lib/lxc/playtime/config` to contain this new section:

```
## systemd within the lxc
lxc.autodev = 1
lxc.pts = 1024
lxc.kmsg = 0
lxc.hook.autodev=/var/lib/lxc/playtime/autodev

```

##### Systemd conflicts in the /dev tree

To avoid conflicts of systemd and lxc in the `/dev` tree. It is **highly recommended** to enable the _autodev_ mode. This will cause LXC to create its own device tree. This also means that the traditional way of manually creating device nodes in the container rootfs `/dev` tree will not work because `/dev` is overmounted by LXC.

**Warning:** Any device nodes required that are not created by LXC by default must be created by the _autodev hook_ script!

It is also important to disable services that are not supported inside a container. Either attach to the running LXC, or [chroot](/index.php/Chroot "Chroot") into the container rootfs, and mask those services:

```
ln -s /dev/null /etc/systemd/system/systemd-udevd.service
ln -s /dev/null /etc/systemd/system/systemd-udevd-control.socket
ln -s /dev/null /etc/systemd/system/systemd-udevd-kernel.socket
ln -s /dev/null /etc/systemd/system/proc-sys-fs-binfmt_misc.automount

```

This disables udev and mounting of `/proc/sys/fs/binfmt_misc`.

##### Maintain devpts consistency

Additionally ensure a pty declaration in the LXC container because the presence of this causes LXC to mount devpts as a new instance. Without this, the container gets the host's devpts, negative results will occur.

```
lxc.pts = 1024

```

**Note:** There is no need to explicitly mount system devices (either via the container config or via its own /etc/fstab), and this should not be done because systemd (or LXC in the case of /dev...) takes care of it.

##### Prevent excess journald activity

By default, lxc symlinks `/dev/kmsg` to `/dev/console`, this leads to journald running at 100% CPU usage all the time. To prevent the symlink, use:

```
lxc.kmsg = 0

```

#### Xorg program considerations (optional)

In order to run programs on the host's display, some bind mounts need to be defined so that the containerized programs can access the host's resources. Add the following section to `/var/lib/lxc/playtime/config`:

```
## for xorg
## fix overmounting see: [https://github.com/lxc/lxc/issues/434](https://github.com/lxc/lxc/issues/434)
lxc.mount.entry = tmpfs tmp tmpfs defaults
lxc.mount.entry = /dev/dri dev/dri none bind,optional,create=dir
lxc.mount.entry = /dev/snd dev/snd none bind,optional,create=dir
lxc.mount.entry = /tmp/.X11-unix tmp/.X11-unix none bind,optional,create=dir
lxc.mount.entry = /dev/video0 dev/video0 none bind,optional,create=file

```

#### OpenVPN considerations

Users wishing to run [OpenVPN](/index.php/OpenVPN "OpenVPN") within the container should read the [OpenVPN in Linux containers](/index.php/OpenVPN_in_Linux_containers "OpenVPN in Linux containers") article.

## Managing Containers

To list all installed LXC containers:

```
# lxc-ls -f

```

Systemd can be used to [start](/index.php/Start "Start") and to [stop](/index.php/Stop "Stop") LXCs via `lxc@CONTAINER_NAME.service`. [Enable](/index.php/Enable "Enable") `lxc@CONTAINER_NAME.service` to have it start when the host system boots.

Users can also start/stop LXCs without systemd. Start a container:

```
# lxc-start -n CONTAINER_NAME

```

Stop a container:

```
# lxc-stop -n CONTAINER_NAME

```

To login into a container:

```
# lxc-console -n CONTAINER_NAME

```

Once logged, treat the container like any other linux system, set the root password, create users, install packages, etc.

To attach to a container:

```
# lxc-attach -n CONTAINER_NAME

```

It works nearly the same as lxc-console, but you are automatically accessing root prompt inside the container, bypassing login.

## Running Xorg programs

Either attach to or [SSH](/index.php/SSH "SSH") into the target container and prefix the call to the program with the DISPLAY ID of the host's X session. For most simple setups, the display is always 0.

An example of running Firefox from the container in the host's display:

```
$ DISPLAY=:0 firefox

```

Alternatively, to avoid directly attaching to or connecting to the container, the following can be used on the host to automate the process:

```
# lxc-attach -n playtime --clear-env -- sudo -u YOURUSER env DISPLAY=0.0 firefox

```

## Troubleshooting

### root login fails

If you get the following error when you try to login using lxc-console:

```
login: root
Login incorrect

```

And the container's `journalctl` shows:

```
pam_securetty(login:auth): access denied: tty 'pts/0' is not secure !

```

Add `pts/0` to the list of terminal names in `/etc/securetty` on the **container** filesystem, see [[1]](http://unix.stackexchange.com/questions/41840/effect-of-entries-in-etc-securetty/41939#41939). You can also opt to delete `/etc/securetty` on the **container** to allow always root to login, see [[2]](https://github.com/systemd/systemd/issues/852).

Alternatively, create a new user in lxc-attach and use it for logging in to the system, then switch to root.

```
# lxc-attach -n playtime
[root@playtime]# useradd -m -Gwheel newuser
[root@playtime]# passwd newuser
[root@playtime]# passwd root
[root@playtime]# exit
# lxc-console -n playtime
[newuser@playtime]$ su

```

### no network-connection with veth in container config

If you can't access your LAN or WAN with a networking interface configured as **veth** and setup through `/etc/lxc/_containername_/config`. If the virtual interface gets the ip assigned and should be connected to the network correctly.

```
ip addr show veth0 
inet 192.168.1.111/24

```

You may disable all the relevant static ip formulas and try setting the ip through the booted container-os like you would normaly do.

Example `_container_/config`

```
...
lxc.network.type = veth
lxc.network.name = veth0
lxc.network.flags = up
lxc.network.link = `bridge`
...

```

And then assign your IP through your preferred method **inside** the container, see also [Network configuration#Configure the IP address](/index.php/Network_configuration#Configure_the_IP_address "Network configuration").

## See also

*   [LXC 1.0 Blog Post Series](https://www.stgraber.org/2013/12/20/lxc-1-0-blog-post-series/)
*   [LXC@developerWorks](http://www.ibm.com/developerworks/linux/library/l-lxc-containers/)
*   [Docker Installation on ArchLinux](http://docs.docker.io/en/latest/installation/archlinux/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Linux_Containers&oldid=413406](https://wiki.archlinux.org/index.php?title=Linux_Containers&oldid=413406)"