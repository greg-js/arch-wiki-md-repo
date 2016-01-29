# Internet sharing

Related articles

*   [Android tethering](/index.php/Android_tethering "Android tethering")
*   [Software access point](/index.php/Software_access_point "Software access point")
*   [Bridge with netctl](/index.php/Bridge_with_netctl "Bridge with netctl")
*   [Ad-hoc networking](/index.php/Ad-hoc_networking "Ad-hoc networking")
*   [Sharing PPP Connection](/index.php/Sharing_PPP_Connection "Sharing PPP Connection")
*   [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall")
*   [Router](/index.php/Router "Router")
*   [USB 3G Modem](/index.php/USB_3G_Modem "USB 3G Modem")

This article explains how to share the internet connection from one machine to other(s).

## Contents

*   [1 Requirements](#Requirements)
*   [2 Configuration](#Configuration)
    *   [2.1 Static IP address](#Static_IP_address)
    *   [2.2 Enable packet forwarding](#Enable_packet_forwarding)
    *   [2.3 Enable NAT](#Enable_NAT)
    *   [2.4 Assigning ip addresses to the client pc(s)](#Assigning_ip_addresses_to_the_client_pc.28s.29)
        *   [2.4.1 Manually adding an ip](#Manually_adding_an_ip)
*   [3 Troubleshooting](#Troubleshooting)
*   [4 See also](#See_also)

## Requirements

*   The machine acting as server should have an additional network device.
*   That network device should be connected to the machines that are going to receive internet access. They can be one or more machines. To be able to share internet to several machines a [switch](https://en.wikipedia.org/wiki/Network_switch "wikipedia:Network switch") is required. If you are sharing to only one machine, a [crossover cable](https://en.wikipedia.org/wiki/Ethernet_crossover_cable "wikipedia:Ethernet crossover cable") is sufficient.

**Note:** If one of the two computers has a gigabit ethernet card, a crossover cable is not necessary and a regular ethernet cable should be enough

## Configuration

This section assumes, that the network device connected to the client computer(s) is named _**net0**_ and the network device connected to the internet as _**internet0**_.

**Tip:** You can rename your devices to this scheme using [Udev#Setting static device names](/index.php/Udev#Setting_static_device_names "Udev").

All configuration is done on the server computer, except for the final step of [#Assigning ip addresses to the client pc(s)](#Assigning_ip_addresses_to_the_client_pc.28s.29).

### Static IP address

On the server computer, assign a static IPv4 address to the interface connected to the other machines. The first 3 bytes of this address cannot be exactly the same as those of another interface.

```
# ip link set up dev net0
# ip addr add 192.168.123.100/24 dev net0 # arbitrary address

```

To have your static ip assigned at boot, you can use [netctl](/index.php/Netctl "Netctl").

### Enable packet forwarding

Check the current packet forwarding settings:

```
# sysctl -a | grep forward

```

You will note that options exist for controlling forwarding per default, per interface, as well as separate options for IPv4/IPv6 per interface.

Enter this command to temporarily enable packet forwarding at runtime:

```
# sysctl net.ipv4.ip_forward=1

```

**Tip:** To enable packet forwarding selectively for a specific interface, use `sysctl net.ipv4.conf._interface_name_.forwarding=1` instead.

Edit `/etc/sysctl.d/30-ipforward.conf` to make the previous change persistent after a reboot for all interfaces:

 `/etc/sysctl.d/30-ipforward.conf` 

```
net.ipv4.ip_forward=1
net.ipv6.conf.default.forwarding=1
net.ipv6.conf.all.forwarding=1

```

Afterwards it is advisable to double-check forwarding is enabled as required after a reboot.

**Note:** [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") introduced new forwarding semantics in version 220/221.[[1]](https://github.com/systemd/systemd/blob/a2088fd025deb90839c909829e27eece40f7fce4/NEWS) If you use systemd-networkd to control the network interfaces, it **overrides** `net.*.ip_forward` settings, turning forwarding off by default. To have it respect above settings it is required to set `IPForward=kernel` in systemd-networkd's interface configuration file (see `man 5 systemd.network` for more information).

### Enable NAT

[Install](/index.php/Install "Install") the package [iptables](https://www.archlinux.org/packages/?name=iptables) from the [official repositories](/index.php/Official_repositories "Official repositories"). Use iptables to enable NAT:

```
# iptables -t nat -A POSTROUTING -o internet0 -j MASQUERADE
# iptables -A FORWARD -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
# iptables -A FORWARD -i net0 -o internet0 -j ACCEPT

```

**Note:** Of course, this also works with a mobile broadband connection (usually called ppp0 on routing PC).

Read the [iptables](/index.php/Iptables "Iptables") article for more information (especially saving the rule and applying it automatically on boot). There is also an excellent guide on iptables [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall").

### Assigning ip addresses to the client pc(s)

If you are planning to regularly have several machines using the internet shared by this machine, then is a good idea to install a [dhcp server](https://en.wikipedia.org/wiki/dhcp "wikipedia:dhcp").

You can read the [dhcpd](/index.php/Dhcpd "Dhcpd") wiki article, to add a dhcp server. Then, install the [dhcpcd](/index.php/Dhcpcd "Dhcpcd") client on every client pc.

If you are not planing to use this setup regularly, you can manually add an ip to each client instead.

#### Manually adding an ip

Instead of using dhcp, on each client pc, add an ip address and the default route:

```
# ip addr add 192.168.123.201/24 dev eth0  # arbitrary address, first three blocks must match the address from above
# ip link set up dev eth0
# ip route add default via 192.168.123.100 dev eth0   # same address as in the beginning

```

Configure a DNS server for each client, see [resolv.conf](/index.php/Resolv.conf "Resolv.conf") for details.

That's it. The client PC should now have Internet.

## Troubleshooting

If you are able to connect the two PCs but cannot send data (for example, if the client PC makes a DHCP request to the server PC, the server PC receives the request and offers an IP to the client, but the client does not accept it, timing out instead), check that you do not have other [Iptables](/index.php/Iptables "Iptables") rules [interfering](https://bbs.archlinux.org/viewtopic.php?pid=1093208).

## See also

*   [Xyne's guide and scripts for launching a subnet with DHCP and DNS](http://xyne.archlinux.ca/notes/network/dhcp_with_dns.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Internet_sharing&oldid=412105](https://wiki.archlinux.org/index.php?title=Internet_sharing&oldid=412105)"