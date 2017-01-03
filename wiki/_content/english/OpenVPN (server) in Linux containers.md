This article describes how to setup a [Linux Container](/index.php/Linux_Container "Linux Container") to run [OpenVPN](/index.php/OpenVPN "OpenVPN") in server mode for secure/private internet use. Doing so offers a distinct advantage over using full-blown virtualization like [VirtualBox](/index.php/VirtualBox "VirtualBox") or [QEMU](/index.php/QEMU "QEMU") in that the resource overhead is minimal by comparison and able to run on low powered devices.

## Contents

*   [1 Host setup](#Host_setup)
*   [2 Container setup](#Container_setup)
    *   [2.1 LXC config](#LXC_config)
    *   [2.2 Needed packages within the container](#Needed_packages_within_the_container)
    *   [2.3 Package setup](#Package_setup)
        *   [2.3.1 OpenVPN](#OpenVPN)
        *   [2.3.2 ufw](#ufw)

## Host setup

1.  The host OS needs a bridge ethernet setup to allow the container to run. Refer to [Linux_Containers#Host_network_configuration](/index.php/Linux_Containers#Host_network_configuration "Linux Containers") for this.
2.  One needs to enable packet forwarding. Refer to [Internet_sharing#Enable_packet_forwarding](/index.php/Internet_sharing#Enable_packet_forwarding "Internet sharing") for this.
3.  Although not strictly required, a firewall is highly recommended.

**Warning:** On the ODROID series of hardware, users need to configure the default forward policy due to some quirkiness. This does not apply to other Arch ARM devices such as Raspberry Pis nor does it apply to x86_64 or i686 machines. For a work-around, see [ODROID#DHCP_assignments_to_LXCs_do_not_work_as_expected](/index.php/ODROID#DHCP_assignments_to_LXCs_do_not_work_as_expected "ODROID") for a work-around.

## Container setup

Basic setup and understanding of [Linux Containers](/index.php/Linux_Containers "Linux Containers") is required. This article assumes that readers have a base LXC setup and operational. New comers to these are directed to the aforementioned article.

### LXC config

The container's config should be modified to include several key sections in order run OpenVPN.

For the example, the lxc is named "playtime" and a full config is shown:

 `/var/lib/lxc/playtime/config` 
```
# Template used to create this container: /usr/share/lxc/templates/lxc-archlinux
# Parameters passed to the template:
# For additional config options, please look at lxc.container.conf(5)

lxc.rootfs = /var/lib/lxc/playtime/rootfs
lxc.utsname = playtime
lxc.arch = x86_64
lxc.include = /usr/share/lxc/config/archlinux.common.conf

## network
lxc.network.type = veth
lxc.network.link = br0
lxc.network.flags = up
lxc.network.name = eth0

## systemd within the lxc
lxc.autodev = 1
lxc.hook.autodev = /var/lib/lxc/playtime/autodev
lxc.pts = 1024
lxc.kmsg = 0

## mounts
lxc.mount.entry = /var/cache/pacman/pkg var/cache/pacman/pkg none bind 0 0

## for openvpn
lxc.cgroup.devices.allow = c 10:200 rwm

```

**Note:** This example requires the use of the **autodev** hook which calls the corresponding `/var/lib/lxc/playtime/autodev` script which users need to create and make executable. For the sake of completeness, this script is provided below. Refer to [Linux Containers](/index.php/Linux_Containers "Linux Containers") for additional discussion if needed.
 `/var/lib/lxc/playtime/autodev` 
```
#!/bin/bash
cd ${LXC_ROOTFS_MOUNT}/dev
mkdir net
mknod net/tun c 10 200
chmod 0666 net/tun

```

### Needed packages within the container

In addition to the base system, [openvpn](https://www.archlinux.org/packages/?name=openvpn) is required and available from the [official repositories](/index.php/Official_repositories "Official repositories"). A properly configured [firewall](/index.php/Firewall "Firewall") to run within the container is *highly* recommended. This guide uses [ufw](https://www.archlinux.org/packages/?name=ufw) which is very easy to configure, but other examples can certainly be used.

### Package setup

#### OpenVPN

Refer to the [OpenVPN](/index.php/OpenVPN "OpenVPN") article to properly setup the home server. Verify openvpn functionality within the container; [start](/index.php/Start "Start") openvpn via `openvpn@myprofile.service` and once satisfied [enable](/index.php/Enable "Enable") it to run at boot.

#### ufw

Refer to [OpenVPN#Firewall configuration](/index.php/OpenVPN#Firewall_configuration "OpenVPN") to setup the routes and firewall within the container. Failure to do so or to implement with an alternative will prevent openvpn from functioning properly in the container.

Start ufw and [enable](/index.php/Enable "Enable") `ufw.service` to start at boot.

```
# ufw enable

```