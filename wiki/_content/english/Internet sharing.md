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

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Requirements](#Requirements)
*   [2 Configuration](#Configuration)
    *   [2.1 Static IP address](#Static_IP_address)
    *   [2.2 Enable packet forwarding](#Enable_packet_forwarding)
    *   [2.3 Enable NAT](#Enable_NAT)
        *   [2.3.1 With iptables](#With_iptables)
        *   [2.3.2 With nftables](#With_nftables)
    *   [2.4 Assigning IP addresses to the client PC(s)](#Assigning_IP_addresses_to_the_client_PC(s))
        *   [2.4.1 Manually adding an IP](#Manually_adding_an_IP)
*   [3 Troubleshooting](#Troubleshooting)
*   [4 See also](#See_also)

## Requirements

The machine acting as server should have an additional network device. That network device requires a functional [w:data link layer](https://en.wikipedia.org/wiki/data_link_layer "w:data link layer") to the machine(s) that are going to receive internet access:

*   To be able to share internet to several machines a [switch](https://en.wikipedia.org/wiki/Network_switch "wikipedia:Network switch") can provide the data link.
*   A wireless device can share access to several machines as well, see [Software access point](/index.php/Software_access_point "Software access point") first for this case.
*   If you are sharing to only one machine, a [crossover cable](https://en.wikipedia.org/wiki/Ethernet_crossover_cable "wikipedia:Ethernet crossover cable") is sufficient. In case one of the two computers' ethernet cards has [MDI-X](https://en.wikipedia.org/wiki/Medium_Dependent_Interface#Auto_MDI-X "w:Medium Dependent Interface") capability, a crossover cable is not necessary and a regular ethernet cable can be used. Executing `ethtool *interface* | grep MDI` as root helps to figure it.

## Configuration

This section assumes, that the network device connected to the client computer(s) is named ***net0*** and the network device connected to the internet as ***internet0***.

**Tip:** You can rename your devices to this scheme using [Udev#Setting static device names](/index.php/Udev#Setting_static_device_names "Udev").

All configuration is done on the server computer, except for the final step of [#Assigning IP addresses to the client PC(s)](#Assigning_IP_addresses_to_the_client_PC(s)).

### Static IP address

On the server computer, assign a static IPv4 address to the interface connected to the other machines. The first 3 bytes of this address cannot be exactly the same as those of another interface, unless both interfaces have netmasks strictly greater than /24.

```
# ip link set up dev net0
# ip addr add 192.168.123.100/24 dev net0 # arbitrary address

```

To have your static ip assigned at boot, you can use a [network manager](/index.php/Network_manager "Network manager").

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

**Tip:** To enable packet forwarding selectively for a specific interface, use `sysctl net.ipv4.conf.*interface_name*.forwarding=1` instead.

**Warning:** If the system uses [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") to control the network interfaces, a per-interface setting for IPv4 is not possible, i.e. systemd logic propagates any configured forwarding into a global (for all interfaces) setting for IPv4\. The advised work-around is to use a firewall to forbid forwarding again on selective interfaces. See the [systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5) manual page for more information. The `IPForward=kernel` semantics introduced in a previous systemd release 220/221 to honor kernel settings does not apply anymore.[[1]](https://github.com/poettering/systemd/commit/765afd5c4dbc71940d6dd6007ecc3eaa5a0b2aa1) [[2]](https://github.com/systemd/systemd/blob/a2088fd025deb90839c909829e27eece40f7fce4/NEWS)

Edit `/etc/sysctl.d/30-ipforward.conf` to make the previous change persistent after a reboot for all interfaces:

 `/etc/sysctl.d/30-ipforward.conf` 
```
net.ipv4.ip_forward=1
net.ipv6.conf.default.forwarding=1
net.ipv6.conf.all.forwarding=1

```

Afterwards it is advisable to double-check forwarding is enabled as required after a reboot.

### Enable NAT

#### With iptables

[Install](/index.php/Install "Install") the [iptables](https://www.archlinux.org/packages/?name=iptables) package. Use iptables to enable NAT:

```
# iptables -t nat -A POSTROUTING -o internet0 -j MASQUERADE
# iptables -A FORWARD -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
# iptables -A FORWARD -i net0 -o internet0 -j ACCEPT

```

**Note:** Of course, this also works with a mobile broadband connection (usually called ppp0 on routing PC).

Read the [iptables](/index.php/Iptables "Iptables") article for more information (especially saving the rule and applying it automatically on boot). There is also an excellent guide on iptables [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall").

#### With nftables

[Install](/index.php/Install "Install") the [nftables](https://www.archlinux.org/packages/?name=nftables) package. To enable NAT with [nftables](/index.php/Nftables "Nftables"), you will have to create the prerouting and postrouting chains in a new/exisiting table (you need both chains even if they're empty):

```
# nft add table ip nat
# nft add chain ip nat prerouting { type nat hook prerouting priority 0 \; }
# nft add chain ip nat postrouting { type nat hook postrouting priority 100 \; }

```

**Note:** If you want to use IPv6, you have to replace all occurences of `ip` with `ip6`.

After that, you have to masquerade the `net0` adresses for `internet0`:

```
# nft add rule nat postrouting oifname internet0 masquerade

```

You may want to add some more firewall restrictions on the forwarding (assuming the filter table already exists, like configured in [Nftables#Server](/index.php/Nftables#Server "Nftables"):

```
# nft add chain inet filter forward { type filter hook forward priority 0\; policy drop\; }
# nft add rule filter forward ct state related,established accept
# nft add rule filter forward iifname net0 oifname internet0 accept

```

You can find more information on NAT in nftables in the [nftables Wiki](https://wiki.nftables.org/wiki-nftables/index.php/Performing_Network_Address_Translation_(NAT)). If you want to make these changes permanent, follow the instructions on [nftables](/index.php/Nftables "Nftables")

### Assigning IP addresses to the client PC(s)

If you are planning to regularly have several machines using the internet shared by this machine, then is a good idea to install a [DHCP](https://en.wikipedia.org/wiki/DHCP "wikipedia:DHCP") server, such as [dhcpd](/index.php/Dhcpd "Dhcpd") or [dnsmasq](/index.php/Dnsmasq "Dnsmasq"). Then configure a DHCP client (e.g. [dhcpcd](/index.php/Dhcpcd "Dhcpcd")) on every client PC.

Incoming connections to UDP port 67 has to be allowed for DHCP server. It also necessary to allow incoming connections to UDP/TCP port 53 for DNS requests.

```
# iptables -I INPUT -p udp --dport 67 -i net0 -j ACCEPT
# iptables -I INPUT -p udp --dport 53 -s 192.168.123.0/24 -j ACCEPT
# iptables -I INPUT -p tcp --dport 53 -s 192.168.123.0/24 -j ACCEPT

```

If you are not planing to use this setup regularly, you can manually add an IP to each client instead.

#### Manually adding an IP

Instead of using DHCP, on each client PC, add an IP address and the default route:

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
*   [NetworkManager](/index.php/NetworkManager "NetworkManager") can be configured for internet sharing if used.