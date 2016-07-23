**翻译状态：** 本文是英文页面 [Router](/index.php/Router "Router") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-07-23，点击[这里](https://wiki.archlinux.org/index.php?title=Router&diff=0&oldid=442356)可以查看翻译后英文页面的改动。

This article is a tutorial for turning a computer into an internet gateway/router. It focuses on *security*, since the gateway is connected directly to the Internet. It should not run **any** services available to the outside world. Towards the LAN, it should only run gateway specific services. It should not run httpd, ftpd, samba, nfsd, etc. as those belong on a server in the LAN as they introduce security flaws.

This article does not attempt to show how to set up a shared connection between 2 PCs using cross-over cables. For a simple internet sharing solution, see [Internet sharing](/index.php/Internet_sharing "Internet sharing").

## Contents

*   [1 硬件需求](#.E7.A1.AC.E4.BB.B6.E9.9C.80.E6.B1.82)
*   [2 约定](#.E7.BA.A6.E5.AE.9A)
*   [3 网络接口配置](#.E7.BD.91.E7.BB.9C.E6.8E.A5.E5.8F.A3.E9.85.8D.E7.BD.AE)
    *   [3.1 持久化命名与接口重命名](#.E6.8C.81.E4.B9.85.E5.8C.96.E5.91.BD.E5.90.8D.E4.B8.8E.E6.8E.A5.E5.8F.A3.E9.87.8D.E5.91.BD.E5.90.8D)
    *   [3.2 IP 配置](#IP_.E9.85.8D.E7.BD.AE)
*   [4 ADSL 连接/PPPoE](#ADSL_.E8.BF.9E.E6.8E.A5.2FPPPoE)
    *   [4.1 PPPoE 配置](#PPPoE_.E9.85.8D.E7.BD.AE)
*   [5 DNS 和 DHCP](#DNS_.E5.92.8C_DHCP)
*   [6 连接共享](#.E8.BF.9E.E6.8E.A5.E5.85.B1.E4.BA.AB)
*   [7 IPv6 tips](#IPv6_tips)
    *   [7.1 Unique Local Addresses](#Unique_Local_Addresses)
    *   [7.2 Global Unicast Addresses](#Global_Unicast_Addresses)
        *   [7.2.1 Static IPv6 prefix](#Static_IPv6_prefix)
        *   [7.2.2 Acquiring IPv6 prefix via DHCPv6-PD](#Acquiring_IPv6_prefix_via_DHCPv6-PD)
    *   [7.3 路由通告与无状态自动配置(SLAAC)](#.E8.B7.AF.E7.94.B1.E9.80.9A.E5.91.8A.E4.B8.8E.E6.97.A0.E7.8A.B6.E6.80.81.E8.87.AA.E5.8A.A8.E9.85.8D.E7.BD.AE.28SLAAC.29)
*   [8 可选附加功能](#.E5.8F.AF.E9.80.89.E9.99.84.E5.8A.A0.E5.8A.9F.E8.83.BD)
    *   [8.1 UPnP](#UPnP)
    *   [8.2 远程管理](#.E8.BF.9C.E7.A8.8B.E7.AE.A1.E7.90.86)
    *   [8.3 缓存网页代理](#.E7.BC.93.E5.AD.98.E7.BD.91.E9.A1.B5.E4.BB.A3.E7.90.86)
    *   [8.4 时间服务器](#.E6.97.B6.E9.97.B4.E6.9C.8D.E5.8A.A1.E5.99.A8)
    *   [8.5 内容过滤](#.E5.86.85.E5.AE.B9.E8.BF.87.E6.BB.A4)
    *   [8.6 流量共享](#.E6.B5.81.E9.87.8F.E5.85.B1.E4.BA.AB)
        *   [8.6.1 用 shorewall 实现流量共享](#.E7.94.A8_shorewall_.E5.AE.9E.E7.8E.B0.E6.B5.81.E9.87.8F.E5.85.B1.E4.BA.AB)
*   [9 参阅](#.E5.8F.82.E9.98.85)

## 硬件需求

*   至少 1 GB 硬盘空间。基本安装约需 500MB 硬盘空间，如果使用 web 代理缓存还需额外预留空间。
*   至少两个实体网口：网关要将两个网络彼此联通。需要将两个网络连接到同一台实体机器，其中一个网口连接到外部网络，另一个连接内部网络。
*   一个集线器或交换机以及网线：将其他机器连接到网关。

## 约定

为描述清晰，下文使用示意性网口名称。

*   **intern0**（内网口）：连接到局域网的网口。真实名字可能是 enp2s0、enp1s1 等等。
*   **extern0**（外网口）：连接到外部网络或广域网的网口。真实名字可能是 enp2s0、enp1s1 等等。

## 网络接口配置

### 持久化命名与接口重命名

Systemd 将自动为网口选择一个唯一接口名称。这个命名将是持久化的，不因重启而改变。如果想改成更易理解的名称请参阅[网络配置#设备命名](/index.php/%E7%BD%91%E7%BB%9C%E9%85%8D%E7%BD%AE#.E8.AE.BE.E5.A4.87.E5.91.BD.E5.90.8D "网络配置")。

### IP 配置

首先配置网口。配置网口最好的方式是编辑 [netctl (简体中文)](/index.php/Netctl_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Netctl (简体中文)") 配置文件。需要创建两个配置文件。

**注意:** 如果仅通过 PPPoE 连接到互联网（只有一个广域网网口），则**不要**设置或启用外网口配置文件。详阅下文“配置 PPPoE”

*   `/etc/netctl/extern0-profile`

```
Description='Public Interface.'
Interface=extern0
Connection=ethernet
IP='dhcp'

```

*   `/etc/netctl/intern0-profile`

```
Description='Private Interface'
Interface=intern0
Connection=ethernet
IP='static'
Address=('10.0.0.1/24')

```

**注意:** 上例中假定路由面向整个子网。如果要面向少数几台机器，要修改 CIDR 后缀缩减范围。例如 /27 是限定 10.0.0.1 至 10.0.0.30 。有很多在线 CIDR 计算器可用。

下一步是用 netctl 启用网络接口配置。

```
# netctl enable extern0-profile
# netctl enable intern0-profile

```

## ADSL 连接/PPPoE

可以用 rp-pppoe 将防火墙的 `extern0` 接口连接到 ADSL modem 并且管理该连接。确认已将 modem 设置为*桥接*（或半桥接或 RFC1483）模式，否则 modem 工作于路由器模式。[安装](/index.php/Install "Install") [rp-pppoe](https://www.archlinux.org/packages/?name=rp-pppoe) 包。

需要注意的是：如果仅能通过 PPPoE 连接到互联网（除了能连接 modem 之外没有其它广域网接口），则不必启用 `extern0-profile` ，因为此时外网口使用名为 ppp0 的伪接口。

### PPPoE 配置

可以使用 netctl 设置 pppoe 连接。首先，

```
# cp /etc/netctl/examples/pppoe /etc/netctl/

```

然后编辑它。选择连接到 modem 的接口并配置它。如果你仅仅通过 PPPoE 连接到互联网，基本上就是 `extern0` 接口。其他字段填入 ISP 的信息。详情参阅 netctl.profile 手册页的 pppoe 章节。

## DNS 和 DHCP

可以用专为小型站点设计的 [dnsmasq](/index.php/Dnsmasq_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Dnsmasq (简体中文)") 向局域网提供 DNS 和 DHCP 服务。[安装](/index.php/Help:Reading_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Help:Reading (简体中文)") [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) 包即可。

Dnsmasq 要配置为 DHCP 服务器。编辑 `/etc/dnsmasq.conf`：

```
interface=intern0 # 使 dnsmasq 只侦听来自内网口（intern0，即局域网）的请求
expand-hosts      # 为 /etc/hosts 中的短主机名添加一个域名
domain=foo.bar    # allow fully qualified domain names for DHCP hosts （配合上条）
dhcp-range=10.0.0.2,10.0.0.255,255.255.255.0,1h # 定义局域网中 DHCP 地址范围：
                  # 从 10.0.0.2 至.255，子网掩码为 255.255.255.0
                  # DHCP 租期 1 小时 （可按需修改）

```

下面将看到，只能添加***静态*** DHCP 租约，例如，分配一个 IP 地址给局域网中某一台机器的 MAC 地址。这样，无论这台机器何时请求，它都将获得同一个 IP 地址。对于需要 DNS 记录的网络服务来说这非常有用。这也可以拒绝特定 MAC 的机器获取 IP 地址。

现在 [启动](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BD.BF.E7.94.A8.E5.8D.95.E5.85.83 "Systemd (简体中文)") `dnsmasq.service` 服务。

## 连接共享

现在可以连通两个网络接口了。详阅 [Shorewall](/index.php/Shorewall "Shorewall") 配置。

## IPv6 tips

Useful reading: [IPv6](/index.php/IPv6 "IPv6") and the [wikipedia:IPv6](https://en.wikipedia.org/wiki/IPv6 "wikipedia:IPv6").

### Unique Local Addresses

You can use your router in IPv6 mode even if you do not have an IPv6 address from your ISP. Unless you disable IPv6 all interfaces should have been assigned a unique `fe80::/10` address.

For internal networking the block `fc00::/7` has been reserved. These addresses are guaranteed to be unique and non-routable from the open internet. Addresses that belong to the `fc00::/7` block are called [Unique Local Addresses](https://en.wikipedia.org/wiki/Unique_local_address "wikipedia:Unique local address"). To get started [generate a ULA /64 block](http://www.simpledns.com/private-ipv6.aspx) to use in your network. For this example we will use `fd00:aaaa:bbbb:cccc::/64`. Firstly we must assign a static IPv6 on the internal interface. Modify the `intern0-profile` we created above to include the following line

```
 IPCustom=('-6 addr add fd00:aaaa:bbbb:cccc::1/64 dev intern0')

```

This will add the ULA to the internal interface. As far as the router goes, this is all you need to configure.

### Global Unicast Addresses

If your ISP or WAN network can access the IPv6 Internet you can additionally assign global link addresses to your router and propagate them through SLAAC to your internal network. The global unicast prefix is usually either *static* or provided through *prefix delegation*.

#### Static IPv6 prefix

If your ISP has provided you with a static prefix then edit `/etc/netctl/extern0-profile` and simply add the IPv6 and the IPv6 prefix (usually /64) you have been provided

```
IPCustom=('-6 addr add 2002:1:2:3:4:5:6:7/64 dev extern0')

```

You can use this in addition to the ULA address described above.

#### Acquiring IPv6 prefix via DHCPv6-PD

If your ISP handles IPv6 via prefix delegation then you can follow the instructions in the [main IPv6 article](/index.php/IPv6#Prefix_delegation_.28DHCPv6-PD.29 "IPv6") on how to properly configure your router. Following the conventions of this article the WAN interface is `extern0` (or `ppp0` if you are connecting through PPPoE) and the LAN interface is `intern0`.

### 路由通告与无状态自动配置(SLAAC)

To properly hand out IPv6s to the network clients we will need to use an advertising daemon. Follow the details of the [main IPv6 article](/index.php/IPv6#For_gateways "IPv6") on how to setup `radvd`. Following the convention of this guide the LAN facing interfaces is `intern0`. You can either advertise all prefixes or choose which prefixes will be assigned to the local network.

## 可选附加功能

### UPnP

上述 shorewall 的配置不包含 [UPnP](https://en.wikipedia.org/wiki/UPnP "wikipedia:UPnP") 支持。尽管 可能使路由器遭到来自局域网内部的攻击，然而某些应用要求必须使用 UPnP。

要在路由器上启用 UPnP ，需要安装一个 UPnP 互联网网关守护进程（IGD）。可从[官方仓库](/index.php/Official_repositories "Official repositories")安装 [miniupnpd](https://www.archlinux.org/packages/?name=miniupnpd) 。

更详细信息请查阅 [Shorewall guide on UPnP](http://www.shorewall.net/UPnP.html) 。

### 远程管理

[OpenSSH](/index.php/Secure_Shell_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Secure Shell (简体中文)") 可用于远程管理路由器，十分适合运行在“**无头**”模式（无显示器或输入设备）的机器。

### 缓存网页代理

参阅 [Squid](/index.php/Squid "Squid") 或 [Polipo](/index.php/Polipo "Polipo") 如何配置代理为网页浏览加速和/或添加额外的安全层。

### 时间服务器

将路由器用作一台时间服务器，参阅[网络时间协议守护进程](/index.php/%E7%BD%91%E7%BB%9C%E6%97%B6%E9%97%B4%E5%8D%8F%E8%AE%AE%E5%AE%88%E6%8A%A4%E8%BF%9B%E7%A8%8B "网络时间协议守护进程")。

然后配置 shorewall 或者 iptables 允许 NTP 流量流出。

### 内容过滤

如果需要内容过滤，可以安装配置 [DansGuardian](/index.php/DansGuardian "DansGuardian") 或者 [Privoxy](/index.php/Privoxy "Privoxy") 。

### 流量共享

流量共享很有用，尤其当局域网中不止一台机器时。基本思路是为不同类型的流量分配优先级。交互型流量（ssh、在线游戏等）可能需要高优先级，而 P2P 流量可分配低优先级。其他流量介于二者之间。

#### 用 shorewall 实现流量共享

参阅 [Shorewall#Traffic shaping](/index.php/Shorewall#Traffic_shaping "Shorewall")

## 参阅

*   [Simple stateful firewall (简体中文)](/index.php/Simple_stateful_firewall_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Simple stateful firewall (简体中文)")
*   [Internet sharing (简体中文)](/index.php?title=Internet_sharing_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&action=edit&redlink=1 "Internet sharing (简体中文) (page does not exist)")