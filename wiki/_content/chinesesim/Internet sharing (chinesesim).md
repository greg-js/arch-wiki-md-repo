Related articles

*   [Android tethering](/index.php/Android_tethering "Android tethering")
*   [Software access point](/index.php/Software_access_point "Software access point")
*   [Bridge with netctl](/index.php/Bridge_with_netctl "Bridge with netctl")
*   [Ad-hoc networking](/index.php/Ad-hoc_networking "Ad-hoc networking")
*   [Sharing PPP Connection](/index.php/Sharing_PPP_Connection "Sharing PPP Connection")
*   [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall")
*   [Router](/index.php/Router "Router")
*   [USB 3G Modem](/index.php/USB_3G_Modem "USB 3G Modem")

**翻译状态：** 本文是英文页面 [Internet sharing](/index.php/Internet_sharing "Internet sharing") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-06-28，点击[这里](https://wiki.archlinux.org/index.php?title=Internet+sharing&diff=0&oldid=480589)可以查看翻译后英文页面的改动。

这篇文章解释了如何从一台机器向其他机器分享网络连接。

## Contents

*   [1 依赖](#.E4.BE.9D.E8.B5.96)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 静态IP地址](#.E9.9D.99.E6.80.81IP.E5.9C.B0.E5.9D.80)
    *   [2.2 启用包转发](#.E5.90.AF.E7.94.A8.E5.8C.85.E8.BD.AC.E5.8F.91)
    *   [2.3 Enable NAT](#Enable_NAT)
        *   [2.3.1 With iptables](#With_iptables)
        *   [2.3.2 With nftables](#With_nftables)
    *   [2.4 给客户机分配IP地址](#.E7.BB.99.E5.AE.A2.E6.88.B7.E6.9C.BA.E5.88.86.E9.85.8DIP.E5.9C.B0.E5.9D.80)
        *   [2.4.1 Manually adding an IP](#Manually_adding_an_IP)
*   [3 Troubleshooting](#Troubleshooting)
*   [4 See also](#See_also)

## 依赖

作为服务器的机器应该有一个额外的网络设备。这个网络设备需要一个[数据链路层](https://en.wikipedia.org/wiki/data_link_layer "w:data link layer")来连接到将要获得网络访问的机器:

*   如果想给若干台机器分享网络连接，[switch](https://en.wikipedia.org/wiki/Network_switch "wikipedia:Network switch")可以提供数据连接。
*   一个无线设备同样可以给若干台机器分享网络访问，参见[Software access point](/index.php/Software_access_point "Software access point") first for this case.
*   If you are sharing to only one machine, a [crossover cable](https://en.wikipedia.org/wiki/Ethernet_crossover_cable "wikipedia:Ethernet crossover cable") is sufficient. In case one of the two computers' ethernet cards has [MDI-X](https://en.wikipedia.org/wiki/Medium_Dependent_Interface#Auto_MDI-X "w:Medium Dependent Interface") capability, a crossover cable is not necessary and a regular ethernet cable can be used. Executing `ethtool *interface* | grep MDI` as root helps to figure it.

## 配置

这个章节假定，连接到客户机的网络设备被命名为 ***net0***而连接到互联网的网络设备被命名为***internet0***。

**提示：** 为了此事，你可以使用[Udev#Setting static device names](/index.php/Udev#Setting_static_device_names "Udev")所述的方法重命名你的设备。

所有的配置都是在服务器计算机上完成的，除了最后一步[#给客户机分配IP地址](#.E7.BB.99.E5.AE.A2.E6.88.B7.E6.9C.BA.E5.88.86.E9.85.8DIP.E5.9C.B0.E5.9D.80).

### 静态IP地址

在服务器计算机上，给要连接到其他机器的网卡分配一个静态的IP地址。IP地址的前3个字节不能和其他网卡的一模一样，除非两个网卡都有一个严格大于/24的子网掩码。

```
# ip link set up dev net0
# ip addr add 192.168.123.100/24 dev net0 # arbitrary address

```

为了使你的静态IP在启动时被分配，你可以使用[network manager](/index.php/Network_manager "Network manager")。

### 启用包转发

检查当前的包转发设置：

```
# sysctl -a | grep forward

```

你将会注意到控制每个默认值，每个网卡的包转发的选项都是存在的，同时每个网卡的IPv4和IPv6选项都是分开的。

输入这条命令以在运行时临时启用包转发：

```
# sysctl net.ipv4.ip_forward=1

```

**提示：** 要想选择性地为某一个具体的网卡提供包转发，使用`sysctl net.ipv4.conf.*interface_name*.forwarding=1`来代替。

**警告:** 如果系统使用了[systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd")来控制网卡，就不可能为单个网卡配置IPv4的设置，换言之，systemd的操作规则会将所有配置过的转发发送到一个全局（针对所有网卡）的IPv4的设置。建议的变通方法是使用防火墙在选中的网卡上禁止转发。参考[systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5)手册页以获取更多信息。在之前的systemd发行版本220/221中引入的执行内核设置的`IPForward=kernel`已不再适用。[[1]](https://github.com/poettering/systemd/commit/765afd5c4dbc71940d6dd6007ecc3eaa5a0b2aa1) [[2]](https://github.com/systemd/systemd/blob/a2088fd025deb90839c909829e27eece40f7fce4/NEWS)

编辑`/etc/sysctl.d/30-ipforward.conf`来使得之前的改变可以永久地应用于所有接口上：

 `/etc/sysctl.d/30-ipforward.conf` 
```
net.ipv4.ip_forward=1
net.ipv6.conf.default.forwarding=1
net.ipv6.conf.all.forwarding=1

```

这之后，仍然建议在重启之后再次检查，以确认转发已经按需求启用。

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

You may want to add some more firewall restrictions on the forwarding (assuming the filter table already exists, like configured in [Nftables#Simple IPv4/IPv6 firewall](/index.php/Nftables#Simple_IPv4.2FIPv6_firewall "Nftables")):

```
# nft add chain inet filter forward { type filter hook forward priority 0 \; policy drop}
# nft add rule filter forward ct state related,established accept
# nft add rule filter forward iifname net0 oifname internet0 accept

```

You can find more information on NAT in nftables in the [nftables Wiki](https://wiki.nftables.org/wiki-nftables/index.php/Performing_Network_Address_Translation_(NAT)). If you want to make these changes permanent, follow the instructions on [nftables](/index.php/Nftables "Nftables")

### 给客户机分配IP地址

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