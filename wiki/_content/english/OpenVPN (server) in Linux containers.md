Related articles

*   [Easy-RSA](/index.php/Easy-RSA "Easy-RSA")
*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")
*   [OpenVPN](/index.php/OpenVPN "OpenVPN")
*   [OpenVPN (client) in Linux containers](/index.php/OpenVPN_(client)_in_Linux_containers "OpenVPN (client) in Linux containers")
*   [ufw](/index.php/Ufw "Ufw")

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

1.  The host OS needs a bridge ethernet setup to allow the container to run. Refer to [Linux Containers#Host network configuration](/index.php/Linux_Containers#Host_network_configuration "Linux Containers") for this.
2.  One needs to enable packet forwarding. Refer to [Internet sharing#Enable packet forwarding](/index.php/Internet_sharing#Enable_packet_forwarding "Internet sharing") for this.
3.  Although not strictly required, a firewall is highly recommended.

## Container setup

Basic setup and understanding of [Linux Containers](/index.php/Linux_Containers "Linux Containers") is required. This article assumes that readers have a base LXC setup operational. Newcomers to these are directed to the aforementioned article.

### LXC config

The container's config should be modified to include several key lines in order run OpenVPN.

For the example, the lxc is named "playtime" and a full config is shown:

 `/var/lib/lxc/playtime/config` 
```
...

## for openvpn
lxc.mount.entry = /dev/net dev/net none bind,create=dir
lxc.cgroup.devices.allow = c 10:200 rwm

```

### Needed packages within the container

In addition to the base system, [openvpn](https://www.archlinux.org/packages/?name=openvpn) is required and available from the [official repositories](/index.php/Official_repositories "Official repositories"). A properly configured [firewall](/index.php/Firewall "Firewall") to run within the container is *highly* recommended. This guide uses [ufw](https://www.archlinux.org/packages/?name=ufw) which is very easy to configure, but other examples can certainly be used.

### Package setup

#### OpenVPN

Refer to the [OpenVPN](/index.php/OpenVPN "OpenVPN") article to properly setup the home server. Verify openvpn functionality within the container; [start](/index.php/Start "Start") openvpn via `openvpn@myprofile.service` and once satisfied [enable](/index.php/Enable "Enable") it to run at boot.

**Note:** Users running openvpn within an *unprivileged* container will need to create a custom systemd unit to start it within the container. Simply copy the package-provided `/usr/lib/systemd/system/openvpn-server@.service` to `/etc/systemd/system/openvpn-server@.service` and modify the new file commenting out the the line beginning with: `LimitNPROC...`

#### ufw

Refer to [OpenVPN#Firewall configuration](/index.php/OpenVPN#Firewall_configuration "OpenVPN") to setup the routes and firewall within the container. Failure to do so or to implement with an alternative will prevent openvpn from functioning properly in the container.

Start ufw and [enable](/index.php/Enable "Enable") `ufw.service` to start at boot.

```
# ufw enable

```