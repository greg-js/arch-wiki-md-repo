*systemd-networkd* is a system daemon that manages network configurations. It detects and configures network devices as they appear; it can also create virtual network devices. This service can be especially useful to set up complex network configurations for a container managed by [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") or for virtual machines. It also works fine on simple connections.

## Contents

*   [1 Basic usage](#Basic_usage)
    *   [1.1 Required services and setup](#Required_services_and_setup)
    *   [1.2 Configuration examples](#Configuration_examples)
        *   [1.2.1 Wired adapter using DHCP](#Wired_adapter_using_DHCP)
        *   [1.2.2 Wired adapter using a static IP](#Wired_adapter_using_a_static_IP)
        *   [1.2.3 Wireless adapter](#Wireless_adapter)
        *   [1.2.4 Wired and wireless adapters on the same machine](#Wired_and_wireless_adapters_on_the_same_machine)
*   [2 Configuration files](#Configuration_files)
    *   [2.1 network files](#network_files)
        *   [2.1.1 [Match] section](#.5BMatch.5D_section)
        *   [2.1.2 [Link] section](#.5BLink.5D_section)
        *   [2.1.3 [Network] section](#.5BNetwork.5D_section)
        *   [2.1.4 [Address] section](#.5BAddress.5D_section)
        *   [2.1.5 [Route] section](#.5BRoute.5D_section)
    *   [2.2 netdev files](#netdev_files)
        *   [2.2.1 [Match] section](#.5BMatch.5D_section_2)
        *   [2.2.2 [NetDev] section](#.5BNetDev.5D_section)
    *   [2.3 link files](#link_files)
        *   [2.3.1 [Match] section](#.5BMatch.5D_section_3)
        *   [2.3.2 [Link] section](#.5BLink.5D_section_2)
        *   [2.3.3 Renaming an interface](#Renaming_an_interface)
*   [3 Usage with containers](#Usage_with_containers)
    *   [3.1 Basic DHCP network](#Basic_DHCP_network)
    *   [3.2 DHCP with two distinct IP](#DHCP_with_two_distinct_IP)
        *   [3.2.1 Bridge interface](#Bridge_interface)
        *   [3.2.2 Bind ethernet to bridge](#Bind_ethernet_to_bridge)
        *   [3.2.3 Bridge network](#Bridge_network)
        *   [3.2.4 Add option to boot the container](#Add_option_to_boot_the_container)
        *   [3.2.5 Result](#Result)
        *   [3.2.6 Notice](#Notice)
    *   [3.3 Static IP network](#Static_IP_network)
*   [4 Management and desktop integration](#Management_and_desktop_integration)
*   [5 See also](#See_also)

## Basic usage

The [systemd](https://www.archlinux.org/packages/?name=systemd) package is part of the default Arch installation and contains all needed files to operate a wired network. Wireless adapters can be setup by other services, such as [wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant"), which are covered later in this article.

### Required services and setup

To use *systemd-networkd*, [start](/index.php/Start "Start") the following two services and [enable](/index.php/Enable "Enable") them to run on system boot:

*   `systemd-networkd.service`
*   `systemd-resolved.service`

**Note:** *systemd-resolved* is actually required only if you are specifying DNS entries in *.network* files or if you want to obtain DNS addresses from networkd's DHCP client.

For compatibility with [resolv.conf](/index.php/Resolv.conf "Resolv.conf"), delete or rename the existing file and create the following symbolic link:

```
# ln -s /usr/lib/systemd/resolv.conf /etc/resolv.conf

```

Optionally, if you wish to use the local DNS stub resolver of *systemd-resolved* (and thus use LLMNR and DNS merging per interface), replace `dns` with `resolve` in `/etc/nsswitch.conf`:

```
hosts: files **resolve** myhostname

```

See `man systemd-resolved` and `man resolved.conf` and [Systemd README](https://github.com/systemd/systemd/blob/master/README#L205).

**Note:** Systemd's `resolve` may not search the local domain when given just the hostname, even when `UseDomains=yes` or `Domains=[domain-list]` is present in the appropriate `.network` file, and that file produces the expected `search [domain-list]` in `resolv.conf`. If you run into this problem:

*   Switch to using fully-qualified domain names
*   Use `/etc/hosts` to resolve hostnames
*   Fall back to using glibc's `dns` instead of using systemd's `resolve`

### Configuration examples

All configurations in this section are stored as `foo.network` in `/etc/systemd/network`. For a full listing of options and processing order, see [#Configuration files](#Configuration_files) and the `systemd.network` man page.

Systemd/udev automatically assigns predictable, stable network interface names for all local Ethernet, WLAN, and WWAN interfaces. Use `networkctl list` to list the devices on the system.

After making changes to a configuration file, [restart](/index.php/Restart "Restart") `systemd-networkd.service`.

**Note:** In the examples below, `enp1s0` is the wired adapter and `wlp2s0` is the wireless adapter. These names can be different on different systems.

#### Wired adapter using DHCP

 `/etc/systemd/network/*wired*.network` 
```
[Match]
Name=enp1s0

[Network]
DHCP=ipv4

```

#### Wired adapter using a static IP

 `/etc/systemd/network/*wired*.network` 
```
[Match]
Name=enp1s0

[Network]
Address=10.1.10.9/24
Gateway=10.1.10.1

```

You may specify multiple IP addresses. Add an IPv6 address with another Address= line. See the `systemd.network(5)` man page for more network options such as specifying DNS servers and a broadcast address.

#### Wireless adapter

In order to connect to a wireless network with *systemd-networkd*, a wireless adapter configured with another service such as [wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant") is required. In this example, the corresponding systemd service file that needs to be enabled is `wpa_supplicant@wlp2s0.service`. This service will run *wpa_supplicant* with the configuration file `/etc/wpa_supplicant/wpa_supplicant-wlp2s0.conf`. If this file does not exist, the service will not start.

 `/etc/systemd/network/*wireless*.network` 
```
[Match]
Name=wlp2s0

[Network]
DHCP=ipv4

```

If the wireless adapter has a static IP address, the configuration is the same (except for the interface name) as in a [wired adapter](#Wired_adapter_using_a_static_IP).

#### Wired and wireless adapters on the same machine

This setup will enable a DHCP IP for both a wired and wireless connection making use of the metric directive to allow the kernel the decide on-the-fly which one to use. This way, no connection downtime is observed when the wired connection is unplugged.

The kernel's route metric (same as configured with *ip*) decides which route to use for outgoing packets, in cases when several match. This will be the case when both wireless and wired devices on the system have active connections. To break the tie, the kernel uses the metric. If one of the connections is terminated, the other automatically wins without there being a gap with nothing configured (ongoing transfers may still not deal with this nicely but that is at a different OSI layer).

**Note:** The **Metric** option is for static routes while the **RouteMetric** option is for setups not using static routes.
 `/etc/systemd/network/*wired*.network` 
```
[Match]
Name=enp1s0

[Network]
DHCP=ipv4

[DHCP]
RouteMetric=10

```
 `/etc/systemd/network/*wireless*.network` 
```
[Match]
Name=wlp2s0

[Network]
DHCP=ipv4

[DHCP]
RouteMetric=20

```

## Configuration files

Configuration files are located in `/usr/lib/systemd/network`, the volatile runtime network directory `/run/systemd/network` and, the local administration network directory `/etc/systemd/network`. Files in `/etc/systemd/network` have the highest priority.

There are three types of configuration files.

*   **.network** files. They will apply a network configuration for a *matching* device
*   **.netdev** files. They will create a *virtual network device* for a *matching* environment
*   **.link** files. When a network device appears, [udev](/index.php/Udev "Udev") will look for the first *matching* **.link** file

They all follow the same rules:

*   If **all** conditions in the `[Match]` section are matched, the profile will be activated
*   an empty `[Match]` section means the profile will apply in any case (can be compared to the `*` joker)
*   each entry is a key with the `NAME=VALUE` syntax
*   all configuration files are collectively sorted and processed in lexical order, regardless of the directory in which they live
*   files with identical name replace each other

**Tip:**

*   to override a system-supplied file in `/usr/lib/systemd/network` in a permanent manner (i.e even after upgrade), place a file with same name in `/etc/systemd/network` and symlink it to `/dev/null`
*   the `*` joker can be used in `VALUE` (e.g `en*` will match any Ethernet device)
*   following this [Arch-general thread](https://mailman.archlinux.org/pipermail/arch-general/2014-March/035381.html), the best practice is to setup specific container network settings *inside the container* with **networkd** configuration files.

### network files

These files are aimed at setting network configuration variables, especially for servers and containers.

Below is a basic structure of a `*MyProfile*.network` file:

 `/etc/systemd/network/*MyProfile*.network` 
```
[Match]
*a vertical list of keys*

[Network]
*a vertical list of keys*

[Address]
*a vertical list of keys*

[Route]
*a vertical list of keys*

```

#### [Match] section

Most common keys are:

*   `Name=` the device name (e.g Br0, enp4s0, en*)
*   `Host=` the machine hostname
*   `Virtualization=` check whether the system is executed in a virtualized environment or not. A `Virtualization=no` key will only apply on your host machine, while `Virtualization=yes` apply to any container or VM.

#### [Link] section

Most common keys are:

*   `MACAddress=` useful for [MAC address spoofing](/index.php/MAC_address_spoofing#Method_1:_systemd-networkd "MAC address spoofing")
*   `MTUBytes=` the maximum transmission unit in bytes (suffixes K, M, G, are supported and are understood to the base of 1024). Using a larger MTU value ([Jumbo frames](/index.php/Jumbo_frames "Jumbo frames")) can significantly speed up your network transfers.

#### [Network] section

Most common keys are:

*   `DHCP=` enables [DHCPv4](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol "wikipedia:Dynamic Host Configuration Protocol") and/or DHCPv6 support. Accepts `yes`, `no`, `ipv4` or `ipv6`
*   `DNS=` is a [DNS](https://en.wikipedia.org/wiki/Domain_Name_System "wikipedia:Domain Name System") server address. You can specify this option more than once
*   `Bridge=` is the name of the bridge to add the link to
*   `IPForward=` defaults to `no`. It enables IP forwarding, performing the forwarding according to the routing table and is required for setting up [Internet sharing](/index.php/Internet_sharing "Internet sharing"). Note that turning `IPForward=` on applies to *all* network interfaces.
*   `Domains=` a list of the domains used for DNS host name resolution.

Please see `systemd.network(5)` for details.

#### [Address] section

Most common key in the `[Address]` section is:

*   `Address=` is a static **IPv4** or **IPv6** address and its prefix length, separated by a `/` character (e.g `192.168.1.90/24`). This option is **mandatory** unless DHCP is used.

#### [Route] section

Most common key in the `[Route]` section is:

*   `Gateway=` is the address of your machine gateway. This option is **mandatory** unless DHCP is used.

For an exhaustive key list, please refer to `systemd.network(5)`

**Tip:** you can put the `Address=` and `Gateway=` keys in the `[Network]` section as a short-hand if `Address=` contains only an Address key and `Gateway=` section contains only a Gateway key

### netdev files

These files will create virtual network devices.

Below is a basic structure of a *Mydevice*.netdev file:

 `/etc/systemd/network/*MyDevice*.netdev` 
```
[Match]
*a vertical list of keys*

[NetDev]
*a vertical list of keys*

```

#### [Match] section

Most common keys are `Host=` and `Virtualization=`

#### [NetDev] section

Most common keys are:

*   `Name=` is the interface name used when creating the netdev. This option is **compulsory**
*   `Kind=` is the netdev kind. For example, *bridge*, *bond*, *vlan*, *veth*, *sit*, etc. are supported. This option is **compulsory**

For an exhaustive key list, please refer to `systemd.netdev(5)`

### link files

These files are an alternative to custom udev rules and will be applied by [udev](/index.php/Udev "Udev") as the device appears.

Below is a basic structure of a *Mydevice*.link file:

 `/etc/systemd/network/*MyDevice*.link` 
```
[Match]
*a vertical list of keys*

[Link]
*a vertical list of keys*

```

The `[Match]` section will determine if a given link file may be applied to a given device, when the `[Link]` section specifies the device configuration.

**Tip:** Use `udevadm test-builtin net_setup_link /sys/path/to/network/device` to diagnose problems with `.link` files.

#### [Match] section

Most common keys are `MACAddress=`, `Host=` and `Virtualization=`.

`Type=` is the device type (e.g. vlan)

#### [Link] section

Most common keys are:

`MACAddressPolicy=` is either *persistent* when the hardware has a persistent MAC address (as most hardware should) or *random* , which allows to give a random MAC address when the device appears.

`MACAddress=` shall be used when no `MACAddressPolicy=` is specified.

**Note:** the system `/usr/lib/systemd/network/99-default.link` is generally sufficient for most of the basic cases.

#### Renaming an interface

Instead of [editing udev rules](/index.php/Network_configuration#Change_device_name "Network configuration"), a .link file can be used to rename an interface. A useful example is to set a predictable interface name for a USB-to-Ethernet adapter based on its MAC address, as those adapters are usually given different names depending on which USB port they are plugged into.

 `/etc/systemd/network/10-ethusb0.link` 
```
[Match]
MACAddress=12:34:56:78:90:ab

[Link]
Description=USB to Ethernet Adapter
Name=ethusb0
```

**Note:** The default link file `/usr/lib/systemd/network/99-default.link` is shipped by the system. Any user-supplied .link **should** have a lexically earlier file name to be considered at all. For example, name the file `10-ethusb0.link` and not `ethusb0.link`.

## Usage with containers

The service is available with [systemd](https://www.archlinux.org/packages/?name=systemd). You will want to [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `systemd-networkd.service` unit on the host and container.

For debugging purposes, it is strongly advised to [install](/index.php/Install "Install") the [bridge-utils](https://www.archlinux.org/packages/?name=bridge-utils), [net-tools](https://www.archlinux.org/packages/?name=net-tools), and [iproute2](https://www.archlinux.org/packages/?name=iproute2) packages.

If you are using *systemd-nspawn*, you may need to modify the `systemd-nspawn@.service` and append boot options to the `ExecStart` line. Please refer to `man 1 systemd-nspawn` for an exhaustive list of options.

Note that if you want to take advantage of automatic DNS configuration from DHCP, you need to enable `systemd-resolved` and symlink `/run/systemd/resolve/resolv.conf` to `/etc/resolv.conf`. See `systemd-resolved.service(8)` for more details.

**Tip:** Before you start to configure your container network, it is useful to:

*   disable all your [netctl](/index.php/Netctl "Netctl") services. This will avoid any potential conflicts with `systemd-networkd` and make all your configurations easier to test. Furthermore, odds are high you will end with few or even no [netctl](/index.php/Netctl "Netctl") activated profiles. The `netctl list` command will output a list of all your profiles, with the activated one being starred.
*   disable the `systemd-nspawn@.service` and use the `systemd-nspawn -bnD /path_to/your_container/` command as root to boot the container. To log off and shutdown inside the container `systemctl poweroff` is used as root. Once the network setting meets your requirements, [enable and start](/index.php/Systemd#Basic_systemctl_usage "Systemd") `systemd-nspawn@.service`
*   disable the `dhcpcd.service` if enabled on your system, since it activates *dhcpcd* on **all** interfaces
*   make sure you have no [netctl](/index.php/Netctl "Netctl") profiles activated in the container, and ensure that `systemd-networkd.service` is neither enabled nor started
*   make sure you do not have any [iptables](/index.php/Iptables "Iptables") rules which can block traffic
*   make sure *packet forwarding* is [enabled](/index.php/Internet_sharing#Enable_packet_forwarding "Internet sharing") if you want to let containers access the internet. Make sure that your `.network` file does not accidentally turn off forwarding because if you do not have a `IPForward=1` setting in it, `systemd-networkd` will turn off forwarding on this interface, even if you have it enabled globally.
*   when the daemon is started the systemd `networkctl` command displays the status of network interfaces.

**Note:** For the set-up described below,

*   we will limit the output of the `ip a` command to the concerned interfaces
*   we assume the *host* is your main OS you are booting to and the *container* is your guest virtual machine
*   all interface names and IP addresses are only examples

### Basic DHCP network

This setup will enable a DHCP IP for host and container. In this case, both systems will share the same IP as they share the same interfaces.

 `/etc/systemd/network/*MyDhcp*.network` 
```
[Match]
Name=en*

[Network]
DHCP=ipv4

```

Then, [enable](/index.php/Enable "Enable") and start `systemd-networkd.service` on your container.

You can of course replace `en*` by the full name of your ethernet device given by the output of the `ip link` command.

*   on host and container:

 `$ ip a` 
```
2: enp7s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 14:da:e9:b5:7a:88 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.72/24 brd 192.168.1.255 scope global enp7s0
       valid_lft forever preferred_lft forever
    inet6 fe80::16da:e9ff:feb5:7a88/64 scope link 
       valid_lft forever preferred_lft forever

```

By default, hostname received from the DHCP server will be used as the transient hostname.

To change it add `UseHostname=false` in section `[DHCPv4]`

 `/etc/systemd/network/*MyDhcp*.network` 
```
[DHCPv4]
UseHostname=false

```

If you did not want to configure a DNS in `/etc/resolv.conf` and want to rely on DHCP for setting it up, you need to [enable](/index.php/Enable "Enable") `systemd-resolved.service` and symlink `/run/systemd/resolve/resolv.conf` to `/etc/resolv.conf`

```
# ln -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf

```

See `systemd-resolved.service(8)` for more details.

### DHCP with two distinct IP

#### Bridge interface

Create a virtual bridge interface

 `/etc/systemd/network/*MyBridge*.netdev` 
```
[NetDev]
Name=br0
Kind=bridge

```

[Restart](/index.php/Restart "Restart") `systemd-networkd.service` to have systemd create the bridge.

On host and container:

 `$ ip a` 
```
3: br0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default 
    link/ether ae:bd:35:ea:0c:c9 brd ff:ff:ff:ff:ff:ff

```

Note that the interface br0 is listed but is DOWN.

#### Bind ethernet to bridge

Modify the `/etc/systemd/network/*MyDhcp*.network` to remove the DHCP, as the bridge requires an interface to bind to with no IP, and add a key to bind this device to br0\. Let us change its name to a more relevant one.

 `/etc/systemd/network/*MyEth*.network` 
```
[Match]
Name=en*

[Network]
Bridge=br0

```

#### Bridge network

Create a network profile for the Bridge

 `/etc/systemd/network/*MyBridge*.network` 
```
[Match]
Name=br0

[Network]
DHCP=ipv4

```

#### Add option to boot the container

As we want to give a separate IP for host and container, we need to *Disconnect* networking of the container from the host. To do this, add this option `--network-bridge=br0` to your container boot command.

```
# systemd-nspawn --network-bridge=br0 -bD /path_to/my_container

```

#### Result

*   on host

 `$ ip a` 
```
3: br0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 14:da:e9:b5:7a:88 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.87/24 brd 192.168.1.255 scope global br0
       valid_lft forever preferred_lft forever
    inet6 fe80::16da:e9ff:feb5:7a88/64 scope link 
       valid_lft forever preferred_lft forever
6: vb-*MyContainer*: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master br0 state UP group default qlen 1000
    link/ether d2:7c:97:97:37:25 brd ff:ff:ff:ff:ff:ff
    inet6 fe80::d07c:97ff:fe97:3725/64 scope link 
       valid_lft forever preferred_lft forever

```

*   on container

 `$ ip a` 
```
2: host0: <BROADCAST,MULTICAST,ALLMULTI,AUTOMEDIA,NOTRAILERS,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 5e:96:85:83:a8:5d brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.73/24 brd 192.168.1.255 scope global host0
       valid_lft forever preferred_lft forever
    inet6 fe80::5c96:85ff:fe83:a85d/64 scope link 
       valid_lft forever preferred_lft forever

```

#### Notice

*   we have now one IP address for Br0 on the host, and one for host0 in the container
*   two new interfaces have appeared: `vb-*MyContainer*` in the host and `host0` in the container. This comes as a result of the `--network-bridge=br0` option. This option *implies* another option, `--network-veth`. This means a *virtual Ethernet link* has been created between host and container.
*   the DHCP address on `host0` comes from the system `/usr/lib/systemd/network/80-container-host0.network` file.
*   on host

 `$ brctl show` 
```
bridge name	bridge id		STP enabled	interfaces
br0		8000.14dae9b57a88	no		enp7s0
							vb-*MyContainer*

```

the above command output confirms we have a bridge with two interfaces binded to.

*   on host

 `$ ip route` 
```
default via 192.168.1.254 dev br0 
192.168.1.0/24 dev br0  proto kernel  scope link  src 192.168.1.87

```

*   on container

 `$ ip route` 
```
default via 192.168.1.254 dev host0 
192.168.1.0/24 dev host0  proto kernel  scope link  src 192.168.1.73

```

the above command outputs confirm we have activated `br0` and `host0` interfaces with an IP address and Gateway 192.168.1.254\. The gateway address has been automatically grabbed by *systemd-networkd*

 `$ cat /run/systemd/resolve/resolv.conf` 
```
nameserver 192.168.1.254

```

### Static IP network

Setting a static IP for each device can be helpful in case of deployed web services (e.g FTP, http, SSH). Each device will keep the same MAC address across reboots if your system `/usr/lib/systemd/network/99-default.link` file has the `MACAddressPolicy=persistent` option (it has by default). Thus, you will easily route any service on your Gateway to the desired device. First, we shall get rid of the system `/usr/lib/systemd/network/80-container-host0.network` file. To do it in a permanent way (e.g even after upgrades), do the following on container. This will mask the file `/usr/lib/systemd/network/80-container-host0.network` since files of the same name in `/etc/systemd/network` take priority over `/usr/lib/systemd/network`.

```
# ln -sf /dev/null /etc/systemd/network/80-container-host0.network

```

Then, [enable and start](/index.php/Systemd#Basic_systemctl_usage "Systemd") `systemd-networkd` on your container.

The needed configuration files:

*   on host

```
/etc/systemd/network/*MyBridge*.netdev
/etc/systemd/network/*MyEth*.network

```

A modified *MyBridge*.network

 `/etc/systemd/network/*MyBridge*.network` 
```
[Match]
Name=br0

[Network]
DNS=192.168.1.254
Address=192.168.1.87/24
Gateway=192.168.1.254

```

*   on container

 `/etc/systemd/network/*MyVeth*.network` 
```
[Match]
Name=host0

[Network]
DNS=192.168.1.254
Address=192.168.1.94/24
Gateway=192.168.1.254

```

## Management and desktop integration

*systemd-networkd* doesn't have a proper interactive management interface via either command-line or GUI. *networkctl* (via CLI) just offers a simple dump of the network interface states.

When *networkd* is configured with [wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant"), both *wpa_cli* and *wpa_gui* offer the ability to associate and reconfigure WLAN interfaces dynamically.

[networkd-notify](https://github.com/wavexx/networkd-notify) can generate simple notifications in response to network interface state changes (such as connection/disconnection and re-association).

## See also

*   [systemd.networkd man page](http://www.freedesktop.org/software/systemd/man/systemd-networkd.service.html)
*   [Tom Gundersen, main systemd-networkd developer, G+ home page](https://plus.google.com/u/0/+TomGundersen/posts)
*   [Tom Gundersen posts on Core OS blog](https://coreos.com/blog/intro-to-systemd-networkd/)
*   [How to set up systemd-networkd with wpa_supplicant](https://bbs.archlinux.org/viewtopic.php?pid=1393759#p1393759) (WonderWoofy's walkthrough on Arch forums)