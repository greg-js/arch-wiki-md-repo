**翻译状态：** 本文是英文页面 [IPv6](/index.php/IPv6 "IPv6") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-10-24，点击[这里](https://wiki.archlinux.org/index.php?title=IPv6&diff=0&oldid=405419)可以查看翻译后英文页面的改动。

在Arch Linux中，IPv6是默认开启的。如果你需要找IPv6隧道的资料，请看[IPv6 tunnel broker setup](/index.php/IPv6_tunnel_broker_setup "IPv6 tunnel broker setup")。

## Contents

*   [1 邻居发现](#.E9.82.BB.E5.B1.85.E5.8F.91.E7.8E.B0)
*   [2 无状态地址自动配置 (SLAAC)](#.E6.97.A0.E7.8A.B6.E6.80.81.E5.9C.B0.E5.9D.80.E8.87.AA.E5.8A.A8.E9.85.8D.E7.BD.AE_.28SLAAC.29)
    *   [2.1 客户端](#.E5.AE.A2.E6.88.B7.E7.AB.AF)
    *   [2.2 网关](#.E7.BD.91.E5.85.B3)
*   [3 IPv6隐私扩展](#IPv6.E9.9A.90.E7.A7.81.E6.89.A9.E5.B1.95)
    *   [3.1 dhcpcd](#dhcpcd)
    *   [3.2 NetworkManager](#NetworkManager)
    *   [3.3 systemd-networkd](#systemd-networkd)
*   [4 静态地址](#.E9.9D.99.E6.80.81.E5.9C.B0.E5.9D.80)
*   [5 IPv6与PPPoE](#IPv6.E4.B8.8EPPPoE)
*   [6 地址委派 (DHCPv6-PD)](#.E5.9C.B0.E5.9D.80.E5.A7.94.E6.B4.BE_.28DHCPv6-PD.29)
    *   [6.1 使用dibbler](#.E4.BD.BF.E7.94.A8dibbler)
    *   [6.2 使用dhcpcd](#.E4.BD.BF.E7.94.A8dhcpcd)
    *   [6.3 使用WIDE-DHCPv6](#.E4.BD.BF.E7.94.A8WIDE-DHCPv6)
*   [7 IPv6 on Comcast](#IPv6_on_Comcast)
*   [8 禁用IPv6](#.E7.A6.81.E7.94.A8IPv6)
    *   [8.1 关闭IPv6支持](#.E5.85.B3.E9.97.ADIPv6.E6.94.AF.E6.8C.81)
    *   [8.2 应用程序](#.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
        *   [8.2.1 dhcpcd](#dhcpcd_2)
        *   [8.2.2 NetworkManager](#NetworkManager_2)
        *   [8.2.3 ntpd](#ntpd)
*   [9 参见](#.E5.8F.82.E8.A7.81)

## 邻居发现

向多播地址`ff02::1`发送PING可以获得局域网内所有主机的回应。使用时需要注明网卡：

```
$ ping6 ff02::1%eth0

```

向多播地址`ff02::2`发送PING，只有路由器会回应。

在PING时加入选项`-I *你的ipv6公网地址*`，局域网内的主机会以各自的公网地址回应。这时不必注明网卡：

```
$ ping6 -I 2001:4f8:fff6::21 ff02::1

```

## 无状态地址自动配置 (SLAAC)

在网络准备好的情况下，获取IPv6地址最简单的方法是通过“无状态地址自动配置”（SLAAC）。地址会自动由路由器给出的前缀推算出，不需要其他配置，也不需要DHCP客户端。

### 客户端

如果你使用[netctl](/index.php/Netctl "Netctl")管理网络，那么只需要在网络配置中加入下面这一行：

```
 IP6=stateless

```

如果使用[NetworkManager](/index.php/NetworkManager "NetworkManager")，它会自动检测网络情况并配置好IPv6.

请注意：只有IPv6 icmp数据包可以经过网络传输时，SLAAC才可以正常工作。所以在要配置IPv6的计算机上，必须修改防火墙，允许`ipv6-icmp`数据包进入。如果你使用[Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall")或[iptables](/index.php/Iptables "Iptables")，你只需要加入：

```
 -A INPUT -p ipv6-icmp -j ACCEPT

```

如果你使用了其他防火墙（ufw，shorewall等等），请查阅其文档，允许`ipv6-icmp`数据包。

### 网关

网关需要运行一个守护进程，以确保能够将IPv6地址分发给客户端。一般使用[radvd](https://www.archlinux.org/packages/?name=radvd)（[official repositories](/index.php/Official_repositories "Official repositories")）。配置radvd很简单。修改`/etc/radvd.conf`，加入如下配置：

```
# replace LAN with your LAN facing interface
interface LAN {
  AdvSendAdvert on;
  MinRtrAdvInterval 3;
  MaxRtrAdvInterval 10;
  prefix ::/64 {
    AdvOnLink on;
    AdvAutonomous on;
    AdvRouterAddr on;
  };
};

```

这些配置可以要求客户端由64位的网络前缀自动推算并配置地址。请注意这些配置允许使用分配到局域网的**所有可用的前缀**。如果你不打算使用`::/64`，需要限制允许使用的前缀，可以注明前缀，例如`2001:DB8::/64`。`prefix`选项可以重复使用多次，分别记录不同的前缀。

网关必须在所有的方向上允许`ipv6-icmp`数据包。如果你使用[Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall")或[iptables](/index.php/Iptables "Iptables")，需要加入如下规则：

```
 -A INPUT -p ipv6-icmp -j ACCEPT
 -A OUTPUT -p ipv6-icmp -j ACCEPT
 -A FORWARD -p ipv6-icmp -j ACCEPT

```

使用其他防火墙也需要类似的规则。配置完成后可以开启`radvd.service`。

## IPv6隐私扩展

当一个客户端使用SLAAC配置其IPv6时，它会使用网络前缀和网卡的MAC地址构造地址。这会引起安全问题：计算机的MAC地址可以轻松通过其IPv6地址推算出。为了解决这个问题，提出了“IPv6隐私扩展”标准([RFC 4941](https://tools.ietf.org/html/rfc4941))。使用这个隐私扩展，内核会从原本的IPv6地址计算生成一个“临时地址”。在连接远程服务器时，系统会优先选择这个地址以隐藏原来的地址。要启用隐私拓展，可以按照如下步骤：

向`/etc/sysctl.d/40-ipv6.conf`加入如下内容：

```
# Enable IPv6 Privacy Extensions
net.ipv6.conf.all.use_tempaddr = 2
net.ipv6.conf.default.use_tempaddr = 2
net.ipv6.conf.*nic0*.use_tempaddr = 2
...
net.ipv6.conf.*nicN*.use_tempaddr = 2

```

其中，`nic0`到`nicN`是你的网卡。`all.use_tempaddr`或`default.use_tempaddr`参数不会对已经配置好的网卡起作用。

重启之后，隐私扩展将会启用。

### dhcpcd

[dhcpcd](/index.php/Dhcpcd "Dhcpcd")从6.4.0版本起就在其默认配置文件中添加了选项`slaac private`，实现对隐私扩展的支持，可以实现"Stable Private IPv6 Addresses instead of hardware based ones"，符合[RFC 7217](https://tools.ietf.org/html/rfc7217) 。([commit](http://roy.marples.name/projects/dhcpcd/info/8aa9dab00dc72c453aeccbde885ecce27a3d81ff))。因此，没有必要修改任何配置，除非你想经常更换地址，而不是在每次连接上新网络时。

### NetworkManager

NetworkManager不遵守`/etc/sysctl.d/40-ipv6.conf`中的配置。可以在重启后运行`$ ip -6 addr show *interface*`验证：正常的地址之外，没有状态为`scope global **temporary**`的地址。

请查阅[NetworkManager#Enable IPv6 Privacy Extensions](/index.php/NetworkManager#Enable_IPv6_Privacy_Extensions "NetworkManager")。

**注意:** 即使看起来开启隐私扩展产生的状态为`scope global temporary`的IPv6地址从不更新（它在过期后不进入`deprecated`状态），但已有验证在长时间之后它**会**改变。

### systemd-networkd

Systemd-networkd也不遵守`/etc/sysctl.d/40-ipv6.conf`的配置，需要在配置中设置`IPv6PrivacyExtensions`选项。

请查阅[systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd")和[systemd.network(5) man page](http://www.freedesktop.org/software/systemd/man/systemd.network.html)。

## 静态地址

有些情况下使用静态地址可以增强安全性。使用SLAAC分配动态地址时，你的计算机的地址会由其网卡MAC推算出，这不利于安全，因为即使地址的网络号改变，你的电脑依然可以被追踪到。

要想用[netctl](/index.php/Netctl "Netctl")分配一个静态地址，可以参照`/etc/netctl/examples/ethernet-static`。如下的部分尤其重要：

```
...
# For IPv6 static address configuration
IP6=static
Address6=('1234:5678:9abc:def::1/64' '1234:3456::123/96')
Routes6=('abcd::1234')
Gateway6='1234:0:123::abcd'

```

**注意:** 如果你只有IPv6连接，那么你要给出IPv6的DNS服务器，例如：
```
DNS=('6666:6666::1' '6666:6666::2')

```
如果你的ISP没有告诉你IPv6的DNS服务器地址，并且你也没有自己的服务器，你可以从[resolv.conf](/index.php/Resolv.conf "Resolv.conf")这篇文章中选一个。

## IPv6与PPPoE

PPPoE的软件包`pppd`提供了对PPPoE之上的IPv6的支持（前提是你的ISP和调制解调器支持）。只需要将如下内容加入`/etc/ppp/pppoe.conf`：

```
 +ipv6

```

如果你使用[netctl](/index.php/Netctl "Netctl")，那么就向你的netctl配置文件加入如下内容：

```
 PPPoEIP6=yes

```

## 地址委派 (DHCPv6-PD)

**注意:** 这个部分是针对自行使用配置网关的内容，不是客户端。如果你使用从市场购得的路由器，请查阅其附带的文档以开启地址委派。

地址委派是一种常见的IPv6部署方式，被许多ISP所采用。具体的做法是将一个地址前缀分配给用户（局域网），即路由器配置为将不同的前缀分配给不同的子网；ISP通过DHCPv6将地址前缀（通常是`/56`或`/64`）分发出去，DHCP客户端再将前缀分配给局域网。对于一个拥有两个网卡的简单网关来说，它的工作就是将从WAN口（或虚拟接口，比如ppp）获取的前缀分配给局域网。

### 使用dibbler

[Dibbler](http://klub.com.pl/dhcpv6/)是一个支持地址委派的DHCPv6客户端及服务器。它在[AUR](/index.php/AUR "AUR")中：[dibbler](https://aur.archlinux.org/packages/dibbler/)。

如果你使用`dibbler`，修改`/etc/dibbler/client.conf`：

```
log-mode short
log-level 7
# use the interface connected to your WAN
iface "WAN" {
  ia
  pd
}

```

**小贴士:** 查阅手册页**`dibbler-client(8)`**以获取更多的信息。

### 使用dhcpcd

[Dhcpcd](/index.php/Dhcpcd "Dhcpcd")在IPv4之外也提供了一个完整的支持DHCPv6-PD的客户端。如果你使用`dhcpcd`，需要修改`/etc/dhcpcd.conf`。你可能已经在用dhcpcd来配置IPv4,所以只需要对现有的配置进行小幅修改：

```
duid
noipv6rs
waitip 6
# Uncomment this line if you are running dhcpcd for IPv6 only.
#ipv6only

# use the interface connected to WAN
interface WAN
ipv6rs
iaid 1
# use the interface connected to your LAN
ia_pd 1 LAN
#ia_pd 1/::/64 LAN/0/64

```

这种配置下，客户端会从`WAN`接口获取一个前缀，分配给`LAN`接口。 如果ISP分配的是`/64`的地址，你需要用第二个`ia_pd`选项。 这也会禁用除`WAN`接口之外的所有路由器请求。

**小贴士:** 查阅手册页**`dhcpcd(8)`**与**`dhcpcd.conf(5)`**获得更多信息。

### 使用WIDE-DHCPv6

[WIDE-DHCPv6](http://wide-dhcpv6.sourceforge.net/)是原本由KAME计划开发的DHCPv6开源实现。它在[AUR](/index.php/AUR "AUR")中：[wide-dhcpv6](https://aur.archlinux.org/packages/wide-dhcpv6/)。

如果你使用`wide-dhcpv6`，修改`/etc/wide-dhcpv6/dhcp6c.conf`：

```
# use the interface connected to your WAN
interface WAN {
  send ia-pd 0;
};

id-assoc pd 0 {
  # use the interface connected to your LAN
  prefix-interface LAN {
    sla-id 1;
    sla-len 8;
  };
};

```

**注意:** `sla-len`应设置为满足`(WAN-prefix) + (sla-len) = 64`的值。这里示范的情况是针对一个长度`/56`的前缀，56+8=64。对于前缀长度`/64`的网络，`sla-len`应为`0`。

要启用或运行wide-dhcpv6，使用如下命令。把`WAN`改为连接到ISP的网卡:

```
# systemctl enable/start dhcp6c@WAN.service

```

**小贴士:** 查阅手册页**`dhcp6c(8)`**与**`dhcp6c.conf(5)`**获取更多信息。

## IPv6 on Comcast

`dhcpcd -4` or `dhcpcd -6` worked using a Motorola SURFBoard 6141 and a Realtek RTL8168d/8111d. Either would work, but would not run dual stack: both protocols and addresses on one interface. (The `-6` command would not work if `-4` ran first, even after resetting the interface. And when it did, it gave the NIC a /128 address.) Try these commands:

```
# dhclient -4 enp3s0
# dhclient -P -v enp3s0

```

The `-P` argument grabs a lease of the IPv6 prefix only. `-v` writes to `stdout` what is also written to `/var/lib/dhclient/dhclient6.leases`:

```
Bound to *:546
Listening on Socket/enp3s0
Sending on   Socket/enp3s0
PRC: Confirming active lease (INIT-REBOOT).
XMT: Forming Rebind, 0 ms elapsed.
XMT:  X-- IA_PD a1:b2:cd:e2
XMT:  | X-- Requested renew  +3600
XMT:  | X-- Requested rebind +5400
XMT:  | | X-- **IAPREFIX 1234:5:6700:890::/64**

```

`IAPREFIX` is the necessary value. Substitute `::1` before the CIDR slash to make the prefix a real address:

```
# ip -6 addr add 1234:5:6700:890::1/64 dev enp3s0

```

## 禁用IPv6

**注意:** Arch直接将IPv6支持编译进内核，因此不能禁用对应的内核模块。

### 关闭IPv6支持

**警告:** 禁用IPv6功能可能导致一些需要其启用的程序无法正常运行。[FS#46297](https://bugs.archlinux.org/task/46297)

向内核参数加入`ipv6.disable=1`可以完全关闭IPv6功能，这应该就是你遇到问题时要做的事。查阅[Kernel parameters](/index.php/Kernel_parameters "Kernel parameters")以获取更多信息。

此外，只加入`ipv6.disable_ipv6=1`内核参数可以保留IPv6功能，但不会向网卡分配IPv6地址。

也可以通过向`/etc/sysctl.d/40-ipv6.conf`加入如下配置来避免系统给网卡分配IPv6地址：

```
# Disable IPv6
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.*nic0*.disable_ipv6 = 1
...
net.ipv6.conf.*nicN*.disable_ipv6 = 1

```

注意你必须在这里清楚地列出所有不需要分配IPv6地址的网卡，仅仅设置`all.disable_ipv6`并不会立刻对已经连接的网卡起作用。

另外，如果使用sysctl关闭IPv6,你应该在`/etc/hosts`中删除所有的IPv6主机：

```
#<ip-address> <hostname.domain.org> <hostname>
127.0.0.1 localhost.localdomain localhost
#::1 localhost.localdomain localhost

```

如果忽略这一步，可能会出现连接错误，因为这些主机会解析到IPv6地址，无法连接。

### 应用程序

在内核中关闭IPv6功能不会阻止应用程序尝试使用IPv6。多数情况下，这样不会有问题，但如果你发现程序无法正常运行，你应该查阅该应用程序的手册页，以找到关闭IPv6的合适方法。

#### dhcpcd

*dhcpcd*会尝试发送IPv6路由器请求。要禁用这种行为，可以依照其手册页`dhcpcd.conf (5)`，向`/etc/dhcpcd.conf`加入如下内容：

```
noipv6rs
noipv6

```

#### NetworkManager

在图形界面下，关闭NetworkManager的IPv6支持可以以右键单击网络状态图表，依次选择*Edit Connections > Wired >* Network name *> Edit > IPv6 Settings > Method > Ignore/Disabled*，然后点击 "Save"。

在命令行终端下，关闭IPv6支持可以使用`nmcli`:

```
# nmcli connection edit *connection0*

```

其中，`connection0`是要修改的网络名称。`nmcli`运行后进入其命令行，输入如下命令：

```
nmcli> set ipv6.method ignore 

```

连接到该网络时，NetworkManager不会再配置该网络的IPv6地址。

#### ntpd

依照[Systemd#Drop-in snippets](/index.php/Systemd#Drop-in_snippets "Systemd")，修改`ntpd.service`的启动方式：

```
# systemctl edit ntpd.service

```

这样会产生一个drop-in snippet，替代原有的`ntpd.service`来加载ntpd。参数`-4`关闭了ntpd的IPv6支持。向drop-in snippet中加入如下内容：

```
[Service]
ExecStart=
ExecStart=/usr/bin/ntpd -4 -g -u ntp:ntp

```

第一行清除了之前的`ExecStart`配置，接下来的一行将该配置设置为带有`-4`参数的ntpd。

## 参见

*   [IPv6](https://www.kernel.org/doc/Documentation/networking/ipv6.txt) - kernel.org documentation
*   [IPv6 temporary addresses](http://www.ipsidixit.net/2012/08/09/ipv6-temporary-addresses-and-privacy-extensions/) - a summary about temporary addresses and privacy extensions
*   [IPv6 prefixes](http://tldp.org/HOWTO/Linux+IPv6-HOWTO/x513.html) - a summary of prefix types
*   [net.ipv6 options](http://tldp.org/HOWTO/Linux+IPv6-HOWTO/proc-sys-net-ipv6..html) - documentation of kernel parameters