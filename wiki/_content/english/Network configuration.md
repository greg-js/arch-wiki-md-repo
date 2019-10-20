Related articles

*   [Network Debugging](/index.php/Network_Debugging "Network Debugging")
*   [Firewalls](/index.php/Firewalls "Firewalls")
*   [Jumbo frames](/index.php/Jumbo_frames "Jumbo frames")
*   [Internet sharing](/index.php/Internet_sharing "Internet sharing")
*   [Router](/index.php/Router "Router")

This article describes how to configure network connections on [OSI layer 3](https://en.wikipedia.org/wiki/OSI_layer_3 "wikipedia:OSI layer 3") and above. Medium-specifics are handled in the [/Ethernet](/index.php/Network_configuration/Ethernet "Network configuration/Ethernet") and [/Wireless](/index.php/Network_configuration/Wireless "Network configuration/Wireless") subpages.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Check the connection](#Check_the_connection)
    *   [1.1 Ping](#Ping)
*   [2 Network management](#Network_management)
    *   [2.1 net-tools](#net-tools)
    *   [2.2 iproute2](#iproute2)
    *   [2.3 Network interfaces](#Network_interfaces)
        *   [2.3.1 Listing network interfaces](#Listing_network_interfaces)
        *   [2.3.2 Enabling and disabling network interfaces](#Enabling_and_disabling_network_interfaces)
    *   [2.4 Static IP address](#Static_IP_address)
    *   [2.5 IP addresses](#IP_addresses)
    *   [2.6 Routing table](#Routing_table)
    *   [2.7 DHCP](#DHCP)
    *   [2.8 Network managers](#Network_managers)
*   [3 Set the hostname](#Set_the_hostname)
    *   [3.1 Local hostname resolution](#Local_hostname_resolution)
    *   [3.2 Local network hostname resolution](#Local_network_hostname_resolution)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Change interface name](#Change_interface_name)
    *   [4.2 Revert to traditional interface names](#Revert_to_traditional_interface_names)
    *   [4.3 Set device MTU and queue length](#Set_device_MTU_and_queue_length)
    *   [4.4 Bonding or LAG](#Bonding_or_LAG)
    *   [4.5 IP address aliasing](#IP_address_aliasing)
        *   [4.5.1 Example](#Example)
    *   [4.6 Promiscuous mode](#Promiscuous_mode)
    *   [4.7 Investigate sockets](#Investigate_sockets)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 The TCP window scaling problem](#The_TCP_window_scaling_problem)
        *   [5.1.1 How to diagnose the problem](#How_to_diagnose_the_problem)
        *   [5.1.2 Ways of fixing it](#Ways_of_fixing_it)
            *   [5.1.2.1 Bad](#Bad)
            *   [5.1.2.2 Good](#Good)
            *   [5.1.2.3 Best](#Best)
        *   [5.1.3 More about it](#More_about_it)
*   [6 See also](#See_also)

## Check the connection

To troubleshoot a network connection, go through the following conditions and ensure that you meet them:

1.  Your [network interface](#Network_interfaces) is listed and enabled. Otherwise, check the device driver – see [/Ethernet#Device driver](/index.php/Network_configuration/Ethernet#Device_driver "Network configuration/Ethernet") or [/Wireless#Device driver](/index.php/Network_configuration/Wireless#Device_driver "Network configuration/Wireless").
2.  You are connected to the network. The cable is plugged in or you are [connected to the wireless LAN](/index.php/Network_configuration/Wireless "Network configuration/Wireless").
3.  Your network interface has an [IP address](#IP_addresses).
4.  Your [routing table](#Routing_table) is correctly set up.
5.  You can [ping](#Ping) a local IP address (e.g. your default gateway).
6.  You can [ping](#Ping) a public IP address (e.g. `8.8.8.8`, which is a Google DNS server and is a convenient address to test with).
7.  [Check if you can resolve domain names](/index.php/Check_if_you_can_resolve_domain_names "Check if you can resolve domain names") (e.g. `archlinux.org`).

### Ping

[ping](https://en.wikipedia.org/wiki/Ping_(networking_utility) is used to test if you can reach a host.

 `$ ping www.example.com` 
```
PING www.example.com (93.184.216.34): 56(84) data bytes
64 bytes from 93.184.216.34: icmp_seq=0 ttl=56 time=11.632 ms
64 bytes from 93.184.216.34: icmp_seq=1 ttl=56 time=11.726 ms
64 bytes from 93.184.216.34: icmp_seq=2 ttl=56 time=10.683 ms
...
```

For every reply you receive, the ping utility will print a line like the above. For more information see the [ping(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ping.8) manual. Note that computers can be configured not to respond to ICMP echo requests. [[1]](https://unix.stackexchange.com/questions/412446/how-to-disable-ping-response-icmp-echo-in-linux-all-the-time)

If you receive no reply, this may be related to your default gateway or your Internet Service Provider (ISP). You can run a [traceroute](/index.php/Traceroute "Traceroute") to further diagnose the route to the host.

**Note:** If you receive an error like `ping: icmp open socket: Operation not permitted` when executing *ping*, try to re-install the [iputils](https://www.archlinux.org/packages/?name=iputils) package.

## Network management

To set up a network connection, go through the following steps:

1.  Ensure your [network interface](#Network_interfaces) is listed and enabled.
2.  Connect to the network. Plug in the Ethernet cable or [connect to the wireless LAN](/index.php/Network_configuration/Wireless "Network configuration/Wireless").
3.  Configure your network connection:
    *   [static IP address](#Static_IP_address)
    *   dynamic IP address: use [DHCP](#DHCP)

**Note:** The installation image enables [dhcpcd](/index.php/Dhcpcd "Dhcpcd") (`dhcpcd@*interface*.service`) for [wired network devices](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) on boot.

### net-tools

Arch Linux has deprecated [net-tools](https://www.archlinux.org/packages/?name=net-tools) in favor of [iproute2](https://www.archlinux.org/packages/?name=iproute2).[[2]](https://www.archlinux.org/news/deprecation-of-net-tools/)

| Deprecated command | Replacement commands |
| arp | ip neighbor |
| [ifconfig](https://en.wikipedia.org/wiki/ifconfig "wikipedia:ifconfig") | ip address, ip link |
| netstat | [ss](#Investigate_sockets) |
| route | ip route |

For a more complete rundown, see [this blog post](https://dougvitale.wordpress.com/2011/12/21/deprecated-linux-networking-commands-and-their-replacements/).

### iproute2

[iproute2](https://en.wikipedia.org/wiki/iproute2 "wikipedia:iproute2") is a dependency of the [base](https://www.archlinux.org/packages/?name=base) [meta package](/index.php/Meta_package "Meta package") and provides the [ip(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip.8) command-line interface, used to manage [network interfaces](#Network_interfaces), [IP addresses](#IP_addresses) and the [routing table](#Routing_table). Be aware that configuration made using `ip` will be lost after a reboot. For persistent configuration, you can use a [network manager](/index.php/Network_manager "Network manager") or automate *ip* commands using scripts and [systemd units](/index.php/Systemd#Writing_unit_files "Systemd"). Also note that `ip` commands can generally be abbreviated, for clarity they are however spelled out in this article.

### Network interfaces

By default [udev](/index.php/Udev "Udev") assigns names to your network interfaces using [Predictable Network Interface Names](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames), which prefixes interfaces names with `en` (wired/[Ethernet](https://en.wikipedia.org/wiki/Ethernet "wikipedia:Ethernet")), `wl` (wireless/WLAN), or `ww` ([WWAN](https://en.wikipedia.org/wiki/Wireless_WAN "wikipedia:Wireless WAN")).

**Tip:** To change interface names, see [#Change interface name](#Change_interface_name) and [#Revert to traditional interface names](#Revert_to_traditional_interface_names).

#### Listing network interfaces

Both wired and wireless interface names can be found via `ls /sys/class/net` or `ip link`. Note that `lo` is the [loop device](https://en.wikipedia.org/wiki/loop_device "wikipedia:loop device") and not used in making network connections.

Wireless device names can also be retrieved using `iw dev`. See also [/Wireless#Get the name of the interface](/index.php/Network_configuration/Wireless#Get_the_name_of_the_interface "Network configuration/Wireless").

If your network interface is not listed, make sure your [device driver](#Device_driver) was loaded successfully.

#### Enabling and disabling network interfaces

Network interfaces can be enabled / disabled using `ip link set *interface* up|down`, see [ip-link(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-link.8).

To check the status of the interface `eth0`:

 `$ ip link show dev eth0` 
```
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master br0 state DOWN mode DEFAULT qlen 1000
...

```

The `UP` in `<BROADCAST,MULTICAST,UP,LOWER_UP>` is what indicates the interface is up, not the later `state DOWN`.

**Note:** If your default route is through interface `eth0`, taking it down will also remove the route, and bringing it back up will not automatically re-establish the default route. See [#Routing table](#Routing_table) for re-establishing it.

### Static IP address

A static IP address can be configured with most standard [network managers](#Network_managers) and also [dhcpcd](/index.php/Dhcpcd "Dhcpcd").

To manually configure a static IP address, add an IP address as described in [#IP addresses](#IP_addresses), set up your [routing table](#Routing_table) and [configure your DNS servers](/index.php/Domain_name_resolution "Domain name resolution").

### IP addresses

[IP addresses](https://en.wikipedia.org/wiki/IP_address "wikipedia:IP address") are managed using [ip-address(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-address.8).

List IP addresses:

```
$ ip address show

```

Add an IP address to an interface:

```
# ip address add *address/prefix_len* broadcast + dev *interface*

```

	Note that:

*   the address is given in [CIDR notation](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation "wikipedia:Classless Inter-Domain Routing") to also supply a [subnet mask](https://en.wikipedia.org/wiki/Subnetwork "wikipedia:Subnetwork")
*   `+` is a special symbol that makes `ip` derive the [broadcast address](https://en.wikipedia.org/wiki/Broadcast_address "wikipedia:Broadcast address") from the IP address and the subnet mask

**Note:** Make sure manually assigned IP addresses do not conflict with DHCP assigned ones.

Delete an IP address from an interface:

```
$ ip address del *address/prefix_len* dev *interface*

```

Delete all addresses matching a criteria, e.g. of a specific interface:

```
$ ip address flush dev *interface*

```

**Tip:** IP addresses can be calculated with [ipcalc](http://jodies.de/ipcalc) ([ipcalc](https://www.archlinux.org/packages/?name=ipcalc)).

### Routing table

The [routing table](https://en.wikipedia.org/wiki/Routing_table "wikipedia:Routing table") is used to determine if you can reach an IP address directly or what gateway (router) you should use. If no other route matches the IP address, the [default gateway](https://en.wikipedia.org/wiki/Default_gateway "wikipedia:Default gateway") is used.

The routing table is managed using [ip-route(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-route.8).

*PREFIX* is either a CIDR notation or `default` for the default gateway.

List IPv4 routes:

```
$ ip route show

```

List IPv6 routes:

```
$ ip -6 route

```

Add a route:

```
# ip route add *PREFIX* via *address* dev *interface*

```

Delete a route:

```
# ip route del *PREFIX* via *address* dev *interface*

```

### DHCP

A [Dynamic Host Configuration Protocol](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol "wikipedia:Dynamic Host Configuration Protocol") (DHCP) server provides clients with a dynamic IP address, the subnet mask, the default gateway IP address and optionally also with DNS name servers.

**Note:** You should not run two DHCP clients simultaneously.

To use DHCP you need a DHCP server in your network and a DHCP client:

| Client | Package | [Archiso](/index.php/Archiso "Archiso") | Note | Systemd units |
| [dhcpcd](/index.php/Dhcpcd "Dhcpcd") | [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) | Yes | DHCP, DHCPv6, ZeroConf, static IP | `dhcpcd.service`, `dhcpcd@*interface*.service` |
| [ISC dhclient](https://www.isc.org/downloads/dhcp/) | [dhclient](https://www.archlinux.org/packages/?name=dhclient) | Yes | DHCP, DHCPv6, BOOTP, static IP | `dhclient@*interface*.service` |

Note that instead of directly using a DHCP client you can also use a [network manager](#Network_managers).

**Tip:** You can check if a DHCP server is running with [dhcping](https://www.archlinux.org/packages/?name=dhcping).

### Network managers

A network manager lets you manage network connection settings in so called network profiles to facilitate switching networks.

**Note:** There are many solutions to choose from, but remember that all of them are mutually exclusive; you should not run two daemons simultaneously.

| Network manager | GUI | [Archiso](/index.php/Archiso "Archiso") [[3]](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) | CLI tools | [PPP](https://en.wikipedia.org/wiki/Point-to-Point_Protocol "wikipedia:Point-to-Point Protocol") support
(e.g. 3G modem) | [DHCP client](#DHCP) | Systemd units |
| [ConnMan](/index.php/ConnMan "ConnMan") | 8 unofficial | No | [connmanctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/connmanctl.1) | Yes (with [ofono](https://aur.archlinux.org/packages/ofono/)) | internal | `connman.service` |
| [netctl](/index.php/Netctl "Netctl") | 2 unofficial | Yes | [netctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/netctl.1), wifi-menu | Yes | [dhcpcd](/index.php/Dhcpcd "Dhcpcd") or [dhclient](https://www.archlinux.org/packages/?name=dhclient) | `netctl-ifplugd@*interface*.service`, `netctl-auto@*interface*.service` |
| [NetworkManager](/index.php/NetworkManager "NetworkManager") | Yes | No | [nmcli(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nmcli.1), [nmtui(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nmtui.1) | Yes | internal, [dhcpcd](/index.php/Dhcpcd "Dhcpcd") or [dhclient](https://www.archlinux.org/packages/?name=dhclient) | `NetworkManager.service` |
| [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") | No | Yes ([base](https://www.archlinux.org/packages/?name=base)) | [networkctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/networkctl.1) | [No](https://github.com/systemd/systemd/issues/481) | internal | `systemd-networkd.service`, `systemd-resolved.service` |
| [Wicd](/index.php/Wicd "Wicd") | Yes | No | [wicd-cli(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wicd-cli.8), [wicd-curses(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wicd-curses.8) | No | [dhcpcd](/index.php/Dhcpcd "Dhcpcd") | `wicd.service` |

There also is [Wifi Radar](/index.php/Wifi_Radar "Wifi Radar"), a GUI application to manage WiFi networks with [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools), it however does not handle wired connections.

See also [List of applications#Network managers](/index.php/List_of_applications#Network_managers "List of applications").

## Set the hostname

A [hostname](https://en.wikipedia.org/wiki/Hostname "wikipedia:Hostname") is a unique name created to identify a machine on a network, configured in `/etc/hostname`—see [hostname(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.5) and [hostname(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.7) for details. The file can contain the system's domain name, if any. To set the hostname, [edit](/index.php/Textedit "Textedit") `/etc/hostname` to include a single line with `*myhostname*`:

 `/etc/hostname` 
```
*myhostname*

```

**Tip:** For advice on choosing a hostname, see [RFC 1178](https://tools.ietf.org/html/rfc1178).

Alternatively, using [hostnamectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostnamectl.1):

```
# hostnamectl set-hostname *myhostname*

```

To temporarily set the hostname (until reboot), use [hostname(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.1) from [inetutils](https://www.archlinux.org/packages/?name=inetutils):

```
# hostname *myhostname*

```

To set the "pretty" hostname and other machine metadata, see [machine-info(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/machine-info.5#https%26%2358%3B%2F%2Fwww.freedesktop.org%2Fsoftware%2Fsystemd%2Fman%2Fmachine-info.html).

### Local hostname resolution

The `myhostname` [Name Service Switch](/index.php/Name_Service_Switch "Name Service Switch") (NSS) module of [systemd](/index.php/Systemd "Systemd") provides local hostname resolution without having to edit `/etc/hosts` ([hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5)). It is enabled by default.

Some clients may however still rely on `/etc/hosts`, see [[4]](https://lists.debian.org/debian-devel/2013/07/msg00809.html) [[5]](https://bugzilla.mozilla.org/show_bug.cgi?id=87717#c55) for examples.

To configure the hosts file, add the following lines to `/etc/hosts`:

```
127.0.0.1        localhost
::1              localhost
127.0.1.1        *myhostname*.localdomain        *myhostname*

```

**Note:** The order of hostnames/aliases that follow the IP address in `/etc/hosts` is significant. The first string is considered the canonical hostname and may be appended with parent domains, where domain components are separated by a dot (ie. `.localdomain` above). All following strings on the same line are considered aliases. See [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5) for more info.

As a result the system resolves to both entries:

 `$ getent hosts` 
```
127.0.0.1       localhost
127.0.0.1       localhost
127.0.1.1       *myhostname*.localdomain *myhostname*

```

For a system with a permanent IP address, that permanent IP address should be used instead of `127.0.1.1`.

### Local network hostname resolution

To make your machine accessible in your LAN via its hostname you can:

*   edit the `/etc/hosts` file for every device in your LAN, see [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5)
*   set up a [DNS server](/index.php/DNS_server "DNS server") to resolve your hostname and make the LAN devices use it (e.g. via [#DHCP](#DHCP))
*   or the easy way: use a [Zero-configuration networking](https://en.wikipedia.org/wiki/Zero-configuration_networking "wikipedia:Zero-configuration networking") service:
    *   Hostname resolution via Microsoft's [NetBIOS](https://en.wikipedia.org/wiki/NetBIOS#Name_service "wikipedia:NetBIOS"). Provided by [Samba](/index.php/Samba "Samba") on Linux. It only requires the `nmb.service`. Computers running Windows, macOS, or Linux with `nmb` running, will be able to find your machine.
    *   Hostname resolution via [mDNS](https://en.wikipedia.org/wiki/Multicast_DNS "wikipedia:Multicast DNS"). Provided by either `nss_mdns` with [Avahi](/index.php/Avahi "Avahi") (see [Avahi#Hostname resolution](/index.php/Avahi#Hostname_resolution "Avahi") for setup details) or [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved"). Computers running macOS, or Linux with Avahi or systemd-resolved running, will be able to find your machine. Windows does not have a built-in mDNS client or daemon.

## Tips and tricks

### Change interface name

**Note:** When changing the naming scheme, do not forget to update all network-related configuration files and custom systemd unit files to reflect the change.

You can change the device name by defining the name manually with an udev-rule. For example:

 `/etc/udev/rules.d/10-network.rules` 
```
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="aa:bb:cc:dd:ee:ff", NAME="net1"
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="ff:ee:dd:cc:bb:aa", NAME="net0"
```

These rules will be applied automatically at boot.

A couple of things to note:

*   To get the MAC address of each card, use this command: `cat /sys/class/net/*device_name*/address`
*   Make sure to use the lower-case hex values in your udev rules. It does not like upper-case.

If the network card has a dynamic MAC, you can use `DEVPATH`, for example:

 `/etc/udev/rules.d/10-network.rules` 
```
SUBSYSTEM=="net", DEVPATH=="/devices/platform/wemac.*", NAME="int"
SUBSYSTEM=="net", DEVPATH=="/devices/pci*/*1c.0/*/net/*", NAME="en"
```

To get the `DEVPATH` of all currently-connected devices, see where the symlinks in `/sys/class/net/` lead. For example:

 `file /sys/class/net/*` 
```
/sys/class/net/enp0s20f0u4u1: symbolic link to ../../devices/pci0000:00/0000:00:14.0/usb2/2-4/2-4.1/2-4.1:1.0/net/enp0s20f0u4u1
/sys/class/net/enp0s31f6:     symbolic link to ../../devices/pci0000:00/0000:00:1f.6/net/enp0s31f6
/sys/class/net/lo:            symbolic link to ../../devices/virtual/net/lo
/sys/class/net/wlp4s0:        symbolic link to ../../devices/pci0000:00/0000:00:1c.6/0000:04:00.0/net/wlp4s0

```

The device path should match both the new and old device name, since the rule may be executed more than once on bootup. For example, in the second rule, `"/devices/pci*/*1c.0/*/net/enp*"` would be wrong since it will stop matching once the name is changed to `en`. Only the system-default rule will fire the second time around, causing the name to be changed back to e.g. `enp1s0`.

If you are using a USB network device (e.g. Android phone tethering) that has a dynamic MAC address and you want to be able to use different USB ports, you could use a rule that matched depending on vendor and product ID instead:

 `/etc/udev/rules.d/10-network.rules`  `SUBSYSTEM=="net", ACTION=="add", ATTRS{idVendor}=="12ab", ATTRS{idProduct}=="3cd4", NAME="net2"` 

To [test](/index.php/Udev#Testing_rules_before_loading "Udev") your rules, they can be triggered directly from userspace, e.g. with `udevadm --debug test /sys/class/net/*`. Remember to first take down the interface you are trying to rename (e.g. `ip link set enp1s0 down`).

**Note:** When choosing the static names **it should be avoided to use names in the format of "eth*X*" and "wlan*X*"**, because this may lead to race conditions between the kernel and udev during boot. Instead, it is better to use interface names that are not used by the kernel as default, e.g.: `net0`, `net1`, `wifi0`, `wifi1`. For further details please see the [systemd](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames) documentation.

### Revert to traditional interface names

If you would prefer to retain traditional interface names such as eth0, [Predictable Network Interface Names](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames) can be disabled by masking the udev rule:

```
# ln -s /dev/null /etc/udev/rules.d/80-net-setup-link.rules

```

Alternatively, add `net.ifnames=0` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

### Set device MTU and queue length

You can change the device [MTU](https://en.wikipedia.org/wiki/Maximum_transmission_unit "wikipedia:Maximum transmission unit") and queue length by defining manually with an udev-rule. For example:

 `/etc/udev/rules.d/10-network.rules`  `ACTION=="add", SUBSYSTEM=="net", KERNEL=="wl*", ATTR{mtu}="1500", ATTR{tx_queue_len}="2000"` 
**Note:**

*   `mtu`: For PPPoE, the MTU should be no larger than 1492\. You can also set MTU via [systemd.netdev(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.netdev.5).
*   `tx_queue_len`: Small value for slower devices with a high latency like modem links and ISDN. High value is recommend for server connected over the high-speed Internet connections that perform large data transfers.

### Bonding or LAG

See [netctl#Bonding](/index.php/Netctl#Bonding "Netctl") or [Wireless bonding](/index.php/Wireless_bonding "Wireless bonding").

### IP address aliasing

IP aliasing is the process of adding more than one IP address to a network interface. With this, one node on a network can have multiple connections to a network, each serving a different purpose. Typical uses are virtual hosting of Web and FTP servers, or reorganizing servers without having to update any other machines (this is especially useful for nameservers).

#### Example

To manually set an alias, for some NIC, use [iproute2](https://www.archlinux.org/packages/?name=iproute2) to execute

```
# ip addr add 192.168.2.101/24 dev eth0 label eth0:1

```

To remove a given alias execute

```
# ip addr del 192.168.2.101/24 dev eth0:1

```

Packets destined for a subnet will use the primary alias by default. If the destination IP is within a subnet of a secondary alias, then the source IP is set respectively. Consider the case where there is more than one NIC, the default routes can be listed with `ip route`.

### Promiscuous mode

Toggling [promiscuous mode](https://en.wikipedia.org/wiki/Promiscuous_mode "wikipedia:Promiscuous mode") will make a (wireless) NIC forward all traffic it receives to the OS for further processing. This is opposite to "normal mode" where a NIC will drop frames it is not intended to receive. It is most often used for advanced network troubleshooting and [packet sniffing](https://en.wikipedia.org/wiki/Packet_sniffing "wikipedia:Packet sniffing").

 `/etc/systemd/system/promiscuous@.service` 
```
[Unit]
Description=Set %i interface in promiscuous mode
After=network.target

[Service]
Type=oneshot
ExecStart=/usr/bin/ip link set dev %i promisc on
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target

```

If you want to enable promiscuous mode on interface `eth0` run [enable](/index.php/Enable "Enable") `promiscuous@eth0.service`.

### Investigate sockets

*ss* is a utility to investigate network ports and is part of the [iproute2](https://www.archlinux.org/packages/?name=iproute2) package. It has a similar functionality to the [deprecated](https://www.archlinux.org/news/deprecation-of-net-tools/) netstat utility.

Common usage includes:

Display all TCP Sockets with service names:

```
$ ss -at

```

Display all TCP Sockets with port numbers:

```
$ ss -atn

```

Display all UDP Sockets:

```
$ ss -au

```

For more information see [ss(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ss.8).

## Troubleshooting

### The TCP window scaling problem

TCP packets contain a "window" value in their headers indicating how much data the other host may send in return. This value is represented with only 16 bits, hence the window size is at most 64Kb. TCP packets are cached for a while (they have to be reordered), and as memory is (or used to be) limited, one host could easily run out of it.

Back in 1992, as more and more memory became available, [RFC 1323](http://www.faqs.org/rfcs/rfc1323.html) was written to improve the situation: Window Scaling. The "window" value, provided in all packets, will be modified by a Scale Factor defined once, at the very beginning of the connection. That 8-bit Scale Factor allows the Window to be up to 32 times higher than the initial 64Kb.

It appears that some broken routers and firewalls on the Internet are rewriting the Scale Factor to 0 which causes misunderstandings between hosts. The Linux kernel 2.6.17 introduced a new calculation scheme generating higher Scale Factors, virtually making the aftermaths of the broken routers and firewalls more visible.

The resulting connection is at best very slow or broken.

#### How to diagnose the problem

First of all, let us make it clear: this problem is odd. In some cases, you will not be able to use TCP connections (HTTP, FTP, ...) at all and in others, you will be able to communicate with some hosts (very few).

When you have this problem, the `dmesg`'s output is OK, logs are clean and `ip addr` will report normal status... and actually everything appears normal.

If you cannot browse any website, but you can ping some random hosts, chances are great that you are experiencing this problem: ping uses ICMP and is not affected by TCP problems.

You can try to use [Wireshark](/index.php/Wireshark "Wireshark"). You might see successful UDP and ICMP communications but unsuccessful TCP communications (only to foreign hosts).

#### Ways of fixing it

##### Bad

To fix it the bad way, you can change the `tcp_rmem` value, on which Scale Factor calculation is based. Although it should work for most hosts, it is not guaranteed, especially for very distant ones.

```
# echo "4096 87380 174760" > /proc/sys/net/ipv4/tcp_rmem

```

##### Good

Simply disable Window Scaling. Since Window Scaling is a nice TCP feature, it may be uncomfortable to disable it, especially if you cannot fix the broken router. There are several ways to disable Window Scaling, and it seems that the most bulletproof way (which will work with most kernels) is to add the following line to `/etc/sysctl.d/99-disable_window_scaling.conf` (see also [sysctl](/index.php/Sysctl "Sysctl")):

```
net.ipv4.tcp_window_scaling = 0

```

##### Best

This problem is caused by broken routers/firewalls, so let us change them. Some users have reported that the broken router was their very own DSL router.

#### More about it

This section is based on the LWN article [TCP window scaling and broken routers](http://lwn.net/Articles/92727/) and an archived Kernel Trap article: [Window Scaling on the Internet](https://web.archive.org/web/20120426135627/http://kerneltrap.org:80/node/6723).

There are also several relevant threads on the LKML.

## See also

*   [Linux Network Administrators Guide](https://www.tldp.org/LDP/nag2/index.html)
*   [Debian Reference: Network setup](https://www.debian.org/doc/manuals/debian-reference/ch05.en.html)
*   [RHEL7: Networking Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Networking_Guide/)
*   [Linux Home Networking](http://www.linuxhomenetworking.com/wiki/)
*   [Monitoring and tuning the Linux Networking Stack: Receiving data](https://blog.packagecloud.io/eng/2016/06/22/monitoring-tuning-linux-networking-stack-receiving-data/)
*   [Monitoring and tuning the Linux Networking Stack: Sending data](https://blog.packagecloud.io/eng/2017/02/06/monitoring-tuning-linux-networking-stack-sending-data/)
*   [Tracing a packet journey using tracepoints, perf and eBPF](http://blog.yadutaf.fr/2017/07/28/tracing-a-packet-journey-using-linux-tracepoints-perf-ebpf/)