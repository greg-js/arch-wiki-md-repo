相关文章

*   [Jumbo frames](/index.php/Jumbo_frames "Jumbo frames")
*   [Firewalls (简体中文)](/index.php/Firewalls_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Firewalls (简体中文)")
*   [Router (简体中文)](/index.php/Router_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Router (简体中文)")
*   [Internet sharing (简体中文)](/index.php/Internet_sharing_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Internet sharing (简体中文)")
*   [Network Debugging](/index.php/Network_Debugging "Network Debugging")

**翻译状态：** 本文是英文页面 [Network_configuration](/index.php/Network_configuration "Network configuration") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-08-28，点击[这里](https://wiki.archlinux.org/index.php?title=Network_configuration&diff=0&oldid=445647)可以查看翻译后英文页面的改动。

本页解释了如何在 [OSI 第三层](https://en.wikipedia.org/wiki/OSI_layer_3 两个页面中。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 检查连接](#检查连接)
    *   [1.1 Ping](#Ping)
*   [2 网络管理](#网络管理)
    *   [2.1 网络工具](#网络工具)
    *   [2.2 iproute2](#iproute2)
    *   [2.3 网络接口](#网络接口)
        *   [2.3.1 列出网络接口](#列出网络接口)
        *   [2.3.2 启用和禁用网络接口](#启用和禁用网络接口)
    *   [2.4 静态 IP 地址](#静态_IP_地址)
    *   [2.5 IP 地址](#IP_地址)
    *   [2.6 路由表](#路由表)
    *   [2.7 DHCP](#DHCP)
        *   [2.7.1 服务器](#服务器)
    *   [2.8 网络管理器](#网络管理器)
*   [3 设置计算机名](#设置计算机名)
*   [4 设备驱动程序](#设备驱动程序)
    *   [4.1 检测驱动状态](#检测驱动状态)
    *   [4.2 加载设备模块](#加载设备模块)
*   [5 网络接口](#网络接口_2)
    *   [5.1 设备命名](#设备命名)
    *   [5.2 获取当前网络名](#获取当前网络名)
        *   [5.2.1 更改设备名称](#更改设备名称)
        *   [5.2.2 使用传统网络命名规则](#使用传统网络命名规则)
    *   [5.3 设定设备的 MTU 和队列长度](#设定设备的_MTU_和队列长度)
    *   [5.4 启用和禁用网络接口](#启用和禁用网络接口_2)
*   [6 配置 IP 地址](#配置_IP_地址)
    *   [6.1 动态 IP 地址](#动态_IP_地址)
        *   [6.1.1 systemd-networkd](#systemd-networkd)
        *   [6.1.2 dhcpcd](#dhcpcd)
        *   [6.1.3 netctl](#netctl)
    *   [6.2 静态 IP 地址](#静态_IP_地址_2)
        *   [6.2.1 netctl](#netctl_2)
        *   [6.2.2 systemd-networkd](#systemd-networkd_2)
        *   [6.2.3 dhcpcd](#dhcpcd_2)
        *   [6.2.4 手动指定](#手动指定)
        *   [6.2.5 计算地址](#计算地址)
    *   [6.3 IP 地址](#IP_地址_2)
    *   [6.4 路由表](#路由表_2)
*   [7 更多设置](#更多设置)
    *   [7.1 笔记本电脑使用 Ifplugd](#笔记本电脑使用_Ifplugd)
    *   [7.2 绑定和链路聚合](#绑定和链路聚合)
    *   [7.3 IP 别名](#IP_别名)
    *   [7.4 更改 MAC/硬件地址](#更改_MAC/硬件地址)
    *   [7.5 共享网络连接](#共享网络连接)
    *   [7.6 路由配置](#路由配置)
    *   [7.7 局域网主机的名称解析](#局域网主机的名称解析)
    *   [7.8 全接收模式](#全接收模式)
*   [8 疑难排解](#疑难排解)
    *   [8.1 更换了连接cable modem的计算机](#更换了连接cable_modem的计算机)
    *   [8.2 TCP窗口扩缩（window scaling）故障](#TCP窗口扩缩（window_scaling）故障)
        *   [8.2.1 如何诊断故障](#如何诊断故障)
        *   [8.2.2 如何修复（糟糕的方法）](#如何修复（糟糕的方法）)
        *   [8.2.3 如何修复（好点的方法）](#如何修复（好点的方法）)
        *   [8.2.4 如何修复（最佳的方法）](#如何修复（最佳的方法）)
        *   [8.2.5 更多](#更多)
    *   [8.3 Realtek 没有连接/网络唤醒故障](#Realtek_没有连接/网络唤醒故障)
        *   [8.3.1 在 Linux 中启用网卡](#在_Linux_中启用网卡)
        *   [8.3.2 方法一 还原/变更Win驱动](#方法一_还原/变更Win驱动)
        *   [8.3.3 方法二 启动Windows驱动里的网络唤醒功能](#方法二_启动Windows驱动里的网络唤醒功能)
        *   [8.3.4 方法三 更新Realtek Linux驱动](#方法三_更新Realtek_Linux驱动)
        *   [8.3.5 方法四 在 BIOS/CMOS 中启用 *LAN Boot ROM*](#方法四_在_BIOS/CMOS_中启用_LAN_Boot_ROM)
    *   [8.4 检查 DHCP 问题先释放 IP 地址](#检查_DHCP_问题先释放_IP_地址)
    *   [8.5 Atheros 芯片组找不到网卡](#Atheros_芯片组找不到网卡)
    *   [8.6 Broadcom BCM57780](#Broadcom_BCM57780)
    *   [8.7 Realtek RTL8111/8168B](#Realtek_RTL8111/8168B)
    *   [8.8 Gigabyte Motherboard with Realtek 8111/8168/8411](#Gigabyte_Motherboard_with_Realtek_8111/8168/8411)

## 检查连接

若要排查网络连接问题，请先确保你满足了以下要求。

1.  你的[网络接口](#网络接口)可见并已启用。否则请检查设备驱动－请查阅 [Network configuration/Ethernet#Device driver](/index.php/Network_configuration/Ethernet#Device_driver "Network configuration/Ethernet") 或 [Wireless network configuration (简体中文)#设备驱动](/index.php/Wireless_network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#设备驱动 "Wireless network configuration (简体中文)") 页面。
2.  你已连接到网络。网线已接好或者已经[连接到无线局域网](/index.php/Wireless_network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wireless network configuration (简体中文)")。
3.  你的网络接口拥有一个[IP 地址](#IP_地址)。
4.  你的[路由表](#路由表)设置正确。
5.  你可以 [ping](#Ping) 通一个本地 IP 地址（例如你的默认网关）。
6.  你可以 [ping](#Ping) 通一个公网 IP 地址（例如 `8.8.8.8` ，即谷歌的 DNS 服务器）。
7.  [检查是否能解析域名](/index.php/Check_if_you_can_resolve_domain_names "Check if you can resolve domain names")（例如 `archlinux.org`）。

### Ping

[ping](https://en.wikipedia.org/wiki/Ping_(networking_utility) 用于测试你是否可连接到某个主机。

 `$ ping www.example.com` 
```
PING www.example.com (93.184.216.34): 56(84) data bytes
64 bytes from 93.184.216.34: icmp_seq=0 ttl=56 time=11.632 ms
64 bytes from 93.184.216.34: icmp_seq=1 ttl=56 time=11.726 ms
64 bytes from 93.184.216.34: icmp_seq=2 ttl=56 time=10.683 ms
...
```

如上所示，Ping 命令对每个收到的回应都会显示一行信息。详细的解释请阅读 [ping(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ping.8) 手册。注意，计算机可以配置为不响应 ICMP 回应请求。[[1]](https://unix.stackexchange.com/questions/412446/how-to-disable-ping-response-icmp-echo-in-linux-all-the-time)

如果没有收到回应，原因可能与你的默认网关配置或者你的网络接入服务商（ISP）有关。你可以运行 [traceroute](/index.php/Traceroute "Traceroute") 以进一步诊断到对端主机的路由。

**注意:** 如果你运行 ping 命令时收到一条类似 `ping: icmp open socket: Operation not permitted` 的报错信息，请尝试重新安装 [iputils](https://www.archlinux.org/packages/?name=iputils) 软件包。

## 网络管理

通过以下步骤来设置网络链接：

1.  确保网络接口已连接并已开启。
2.  连接到网络。网线已接好或者已经[连接到无线局域网](/index.php/Wireless_network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wireless network configuration (简体中文)")。
3.  配置网络连接：
    *   [静态 IP 地址](#静态_IP_地址)
    *   动态 IP 地址：使用 [DHCP](#DHCP)

**注意:** 安装镜像会在开机时为 [有线网络设备](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) 启用 [dhcpcd](/index.php/Dhcpcd "Dhcpcd") (`dhcpcd@*interface*.service`)

### 网络工具

Arch Linux 已经弃用了 [net-tools](https://www.archlinux.org/packages/?name=net-tools) 转而使用 [iproute2](https://www.archlinux.org/packages/?name=iproute2)。 [[2]](https://www.archlinux.org/news/deprecation-of-net-tools/)

| 已弃用的命令 | 替换命令 |
| arp | ip neighbor |
| [ifconfig](https://zh.wikipedia.org/wiki/Ifconfig) | ip address, ip link |
| netstat | [ss](#Investigate_sockets) |
| route | ip route |

想要更多更完整的总结，请参阅[这篇文章](https://dougvitale.wordpress.com/2011/12/21/deprecated-linux-networking-commands-and-their-replacements/)。

### iproute2

[iproute2](https://en.wikipedia.org/wiki/iproute2 使 ip 命令自动化。同时需要注意的是 ip 命令通常能够缩写，为了清楚起见，本文对其进行了详细说明。

### 网络接口

默认情况下， [udev](/index.php/Udev_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Udev (简体中文)") 使用 [可预测的网络接口名称](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames) 分配给你的网络接口，该名称以 `en` (有线/[以太网](https://zh.wikipedia.org/wiki/以太网)) ，`wl` (无线/WLAN) 或 `ww` ([WWAN](https://en.wikipedia.org/wiki/Wireless_WAN "wikipedia:Wireless WAN")) 。

**Tip:** 要改变接口名称，请参阅 [#Change interface name](#Change_interface_name) 和 [#Revert to traditional interface names](#Revert_to_traditional_interface_names) 。

#### 列出网络接口

有线和无线接口名称都可以通过 `ls /sys/class/net` 或 `ip link` 找到。要注意的是 `lo` 是 [Loop 设备](https://zh.wikipedia.org/wiki/Loop设备) ，不被用于建立网络连接。

同样，也可以用 `iw dev` 来检索无线设备的名称。可以参阅 [Wireless network configuration (简体中文)#获取有用信息](/index.php/Wireless_network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#获取有用信息 "Wireless network configuration (简体中文)")

如果未列出您的网络接口，请确保已成功加载设备驱动。参阅 [Network configuration/Ethernet#Device driver](/index.php/Network_configuration/Ethernet#Device_driver "Network configuration/Ethernet") 或 [Wireless network configuration (简体中文)#设备驱动](/index.php/Wireless_network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#设备驱动 "Wireless network configuration (简体中文)") 。

#### 启用和禁用网络接口

可以使用 `ip link set *interface* up|down` 来启用 / 禁用网络接口，参阅 [ip-link(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-link.8) 。

要想检查接口 `eth0` 的状态：

 `$ ip link show dev eth0` 
```
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master br0 state DOWN mode DEFAULT qlen 1000
...

```

`<BROADCAST,MULTICAST,UP,LOWER_UP>` 中的 `UP` 表示接口已经启动，而非表示稍后的 `state DOWN` 。

**注意:** 如果您的默认路由是通过接口 `eth0` 进行的，则将其删除也会删除该路由，而恢复备份将不会自动重新建立默认路由。参阅 [#路由表](#路由表) 以重新建立它。

### 静态 IP 地址

可以通过绝大多数的 [网络管理器](#网络管理器) 或 [dhcpcd (简体中文)](/index.php/Dhcpcd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Dhcpcd (简体中文)") 来配置静态 IP 地址。

要手动配置静态 IP 地址，请按照 [IP 地址](#IP_地址) 中的说明添加 IP 地址，设置 [路由表](#路由表) 并[配置 DNS 服务器](/index.php/Domain_name_resolution_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Domain name resolution (简体中文)")。

### IP 地址

通过 [ip-address(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-address.8) 来管理 [IP 地址](https://zh.wikipedia.org/wiki/IP地址)。

列出 IP 地址：

```
$ ip address show

```

将 IP 地址添加到接口：

```
# ip address add *address/prefix_len* broadcast + dev *interface*

```

	注意：

*   这个地址将以 [CIDR 表示法](https://zh.wikipedia.org/wiki/无类别域间路由) 给出，还会提供 [子网掩码](https://zh.wikipedia.org/wiki/子网) 。
*   `+` 是使 `ip` 从 IP 地址和子网掩码派生 [broadcast address](https://en.wikipedia.org/wiki/Broadcast_address "wikipedia:Broadcast address") 的特殊符号

**注意:** 要确保手动分配的 IP 地址与 DHCP 分配的 IP 地址不冲突。

将 IP 地址从接口中删除：

```
$ ip address del *address/prefix_len* dev *interface*

```

删除所有符合条件的地址，例如某个特定接口的地址：

```
$ ip address flush dev *interface*

```

**Tip:** 可通过 [ipcalc](http://jodies.de/ipcalc) ([ipcalc](https://www.archlinux.org/packages/?name=ipcalc)) 计算 IP 地址。

### 路由表

[路由表](https://zh.wikipedia.org/wiki/路由表) 被用于确定是否可以直接访问某个 IP 地址或该使用哪个网关（路由器）。如果别的路由与这个 IP 地址匹配，将使用[默认网关](https://en.wikipedia.org/wiki/Default_gateway "wikipedia:Default gateway") 。

通过 [ip-route(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-route.8) 来管理路由表。

**PREFIX** 是 CIDR 表示法或默认网关的 `默认值` 。

列出 IPv4 路由：

```
$ ip route show

```

列出 IPv6 路由：

```
$ ip -6 route

```

添加路由：

```
# ip route add *PREFIX* via *address* dev *interface*

```

删除路由：

```
# ip route del *PREFIX* via *address* dev *interface*

```

### DHCP

[动态主机配置协议（DHCP）](https://zh.wikipedia.org/wiki/动态主机配置协议) 服务器为客户端提供动态 IP 地址，子网掩码，默认网关 IP 地址，有时还可以提供域名服务器。

要使用 DHCP ，需要网络中有的 DHCP 服务器和 DHCP 客户端：

| 客户端 | 软件包 | [Archiso](/index.php/Archiso_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Archiso (简体中文)") | 注意 | Systemd units |
| [dhcpcd](/index.php/Dhcpcd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Dhcpcd (简体中文)") | [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) | Yes | DHCP, DHCPv6, ZeroConf, static IP | `dhcpcd.service`, `dhcpcd@*interface*.service` |
| [ISC dhclient](https://www.isc.org/downloads/dhcp/) | [dhclient](https://www.archlinux.org/packages/?name=dhclient) | Yes | DHCP, DHCPv6, BOOTP, static IP | `dhclient@*interface*.service` |

**注意:**

*   不能同时运行两个 DHCP 客户端
*   使用 DHCP 客户端的同时还需要同时使用 [网络管理器](#网络管理器)

**Tip:** 你可以通过 [dhcping](https://www.archlinux.org/packages/?name=dhcping) 检查一个 DHCP 服务器是否在运行。

#### 服务器

| 服务器 | 软件包 | IPv4 | IPv6 | GUI | 接口 | 后端存储 | 注意 |
| [dhcpd](/index.php/Dhcpd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Dhcpd (简体中文)") | [dhcp](https://www.archlinux.org/packages/?name=dhcp) | Yes | Yes | [Glass-ISC-DHCP](https://github.com/Akkadius/glass-isc-dhcp) | ? | File |
| [dnsmasq](/index.php/Dnsmasq_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Dnsmasq (简体中文)") | [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) | Yes | Yes | No | ? | File | Also DNS, PXE and TFTP |
| [Kea](/index.php/Kea "Kea") | [kea](https://www.archlinux.org/packages/?name=kea) | Yes | Yes | [Kea-Anterius (Experimental)](https://github.com/isc-projects/kea-anterius) | REST, RADIUS and NETCONF | File, MySQL, PostgreSQL and Cassandra | Also DNS |

### 网络管理器

网络管理器可以在网络配置文件中管理网络连接设置，以便切换网络。

**注意:** 有许多可选的方案，但他们都相互排斥，因此不要同时运行两个守护程序

| 网络管理器 | GUI | [Archiso (简体中文)](/index.php/Archiso_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Archiso (简体中文)") [[3]](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) | CLI 工具 | [点对点协议](https://zh.wikipedia.org/wiki/点对点协议) 支持
(e.g. 3G modem) | [DHCP 客户端](#DHCP) | Systemd units |
| [ConnMan](/index.php/ConnMan "ConnMan") | 8 unofficial | No | [connmanctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/connmanctl.1) | Yes (with [ofono](https://aur.archlinux.org/packages/ofono/)) | 内置 | `connman.service` |
| [netctl](/index.php/Netctl_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Netctl (简体中文)") | 2 unofficial | Yes | [netctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/netctl.1), wifi-menu | Yes | [dhcpcd](/index.php/Dhcpcd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Dhcpcd (简体中文)") 或 [dhclient](https://www.archlinux.org/packages/?name=dhclient) | `netctl-ifplugd@*interface*.service`, `netctl-auto@*interface*.service` |
| [NetworkManager](/index.php/NetworkManager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NetworkManager (简体中文)") | Yes | No | [nmcli(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nmcli.1), [nmtui(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nmtui.1) | Yes | internal, [dhcpcd](/index.php/Dhcpcd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Dhcpcd (简体中文)") 或 [dhclient](https://www.archlinux.org/packages/?name=dhclient) | `NetworkManager.service` |
| [systemd-networkd](/index.php/Systemd-networkd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd-networkd (简体中文)") | No | Yes ([base](https://www.archlinux.org/packages/?name=base)) | [networkctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/networkctl.1) | [No](https://github.com/systemd/systemd/issues/481) | 内置 | `systemd-networkd.service`, `systemd-resolved.service` |
| [Wicd](/index.php/Wicd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wicd (简体中文)") | Yes | No | [wicd-cli(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wicd-cli.8), [wicd-curses(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wicd-curses.8) | No | [dhcpcd](/index.php/Dhcpcd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Dhcpcd (简体中文)") | `wicd.service` |

还有 使用[wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools) 管理 WiFi 网络的 GUI 应用 [Wifi Radar](/index.php/Wifi_Radar_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wifi Radar (简体中文)") ，但它不处理有线连接。

参阅 [List of applications (简体中文)#网络管理](/index.php/List_of_applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#网络管理 "List of applications (简体中文)") 。

## 设置计算机名

[主机名](https://en.wikipedia.org/wiki/Hostname "wikipedia:Hostname") 是一个网络中唯一标识一台机器的名称。主机名通过文件 `/etc/hostname` 进行配置。这样设置主机名：

```
# hostnamectl set-hostname **myhostname**

```

这将会把 **myhostname** 写入 `/etc/hostname`。详情参见 [hostname(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.5) 和 [hostnamectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostnamectl.1)。

**注意:** 在 Arch Linux chroot 安装环境中，*hostnamectl*不起作用，要设置安装环境的主机名，请手动[编辑](/index.php/Textedit "Textedit") `/etc/hostname`，加入一行`*myhostname*`.

建议同时在 `/etc/hosts` 中设置 hostname：

 `/etc/hosts` 
```
#
# /etc/hosts: static lookup table for host names
#

#<ip-address>	<hostname.domain.org>	<hostname>
127.0.0.1	localhost.localdomain	localhost	 *myhostname*
::1		localhost.localdomain	localhost	 *myhostname*
```

**注意:** [systemd](https://www.archlinux.org/packages/?name=systemd) 通过 `myhostname` nss 模块(在 `/etc/nsswitch.conf` 中默认启用)进行主机名解析，所以大部分情况下都不需要在 `/etc/hosts` 中设置主机名。但是有些用户反馈如果不设置，某些依赖网络的程序会碰到延迟问题。参考 [#Local network hostname resolution](#Local_network_hostname_resolution)。

要临时设置主机名（直到下次重启为止），使用 [inetutils](https://www.archlinux.org/packages/?name=inetutils) 中的 `hostname` 命令：

```
# hostname *myhostname*

```

要设置清晰的主机名和其它机器数据，请参考 `machine-info` 手册页.

## 设备驱动程序

### 检测驱动状态

[Udev](/index.php/Udev "Udev") 会探测网卡（[NIC](https://en.wikipedia.org/wiki/Network_interface_controller "wikipedia:Network interface controller")）并在启动时自动载入必要的模块。 检查 `lspci -v` 输出中 "Ethernet controller" （或者类似的）条目，它会告诉你哪个内核模块包含了网络设备的驱动程序。例如：

 `$ lspci -v` 
```
02:00.0 Ethernet controller: Attansic Technology Corp. L1 Gigabit Ethernet Adapter (rev b0)
 	...
 	Kernel driver in use: atl1
 	Kernel modules: atl1

```

接下来， 用 `dmesg | grep *module_name*` 来检查是否已经加载了驱动。例如：

```
$ dmesg |grep atl1
  ...
  atl1 0000:02:00.0: eth0 link is up 100 Mbps full duplex

```

如果驱动加载成功，就跳过下一节，否则，你需要知道您特定型号的网络设备需要哪一个模块。

### 加载设备模块

用 Google 查找芯片组需要的模块/驱动。常见的驱动模块有用于 Realtek 芯片组网卡的 `8139too`，或者用于 Sis 芯片组网卡的 `sis900`。知道要使用什么模块之后，尝试 [手动加载它](/index.php/Kernel_modules#Manual_module_handling "Kernel modules")。如果你碰到了未找到模块的错误，可能驱动没有包括在 Arch 的内核中。你可以在 [AUR](/index.php/AUR "AUR") 中搜索模块名称。

如果 udev 在引导时不能自动侦测和加载适当的模块，参见 [Kernel modules#Loading](/index.php/Kernel_modules#Loading "Kernel modules")。

## 网络接口

### 设备命名

对于有多块网卡的电脑，固定的设备名称很重要。许多配置问题都是由于网络接口名称变化引起的。

[udev](/index.php/Udev "Udev") 负责给设备命名。Systemd v197 引入了[可预测的网络接口名称](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames)自动给网络设备分配静态名称，网络接口现在是以前缀 `en`（以太网）、`wl`（WLAN）、或者 `ww`（WWAN）附上一个自动生成的标识符，产生了一个类似于 `enp0s25` 的条目。在 [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") 中添加 `net.ifnames=0` 可以禁用此功能.

**注意:** 当你改变接口命名规则时，不要忘记更新所有与网络相关的配置文件和自定义的 systemd unit 文件以反映变化。特别是当你启用了 [netctl 静态配置](/index.php/Netctl#Basic_method "Netctl") 时，要运行 `netctl reenable *profile*` 来更新生成的服务文件。

### 获取当前网络名

可以通过 sysfs 或 `ip link` 找到。

 `$ ls /sys/class/net` 
```

lo eth0 eth1 firewire0

```
 `$ ip link` 
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 08:00:27:23:6f:3a brd ff:ff:ff:ff:ff:ff

```

无线设备名称也可以通过 `iw dev` 查看，请参考 [Wireless network configuration#Getting some useful information](/index.php/Wireless_network_configuration#Getting_some_useful_information "Wireless network configuration").

#### 更改设备名称

你可以用 udev-rule 手动定义名称来更改设备名称。例如：

 `/etc/udev/rules.d/10-network.rules` 
```
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="aa:bb:cc:dd:ee:ff", NAME="net1"
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="ff:ee:dd:cc:bb:aa", NAME="net0"

```

值得注意的两点：

*   使用这条命令来获得每张网卡的 MAC 地址：`cat /sys/class/net/**设备名**/address`
*   确保你的 udev 规则中使用小写的十六进制值，而不是大写。

**注意:** 选择静态名称时，**应该避免使用形如 "eth*X*" 或 "wlan*X*" 的名称**，因为这可能在引导时导致内核与 udev 之间的竞争状态。相反，最好用内核默认不会使用的接口名称，例如：`net0`、`net1`、`wifi0`、`wifi1`。更多细节请查看 [systemd](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames) 文档。

#### 使用传统网络命名规则

如果希望使用传统的命名方法 eth0,可以通过下面方法禁用 [Predictable Network Interface Names](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames):

1.  ln -s /dev/null /etc/udev/rules.d/80-net-setup-link.rules

### 设定设备的 MTU 和队列长度

你可以手动定义一条 udev 规则来改变队列的 MTU（最大传输单元）和队列长度You can change the device MTU and queue length by defining manually with an udev-rule。举例来说：

 `/etc/udev/rules.d/10-network.rules` 
```
ACTION=="add", SUBSYSTEM=="net", KERNEL=="wl*", ATTR{mtu}="1480", ATTR{tx_queue_len}="2000"

```

### 启用和禁用网络接口

可以通过如下命令启用或禁用接口：

```
# ip link set eth0 up
# ip link set eth0 down

```

查看结果：

 `$ ip link show dev eth0` 
```
2: eth0: <BROADCAST,MULTICAST,PROMISC,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master br0 state UP mode DEFAULT qlen 1000
...

```

**Note:** 如果默认路由是通过 `eth0` 建立，禁用接口同时也会删除路由，再次启用也不会自动重新建立路由，要重新建立，请参考 [#手动分配](#手动分配).

## 配置 IP 地址

有两种配置方式：通过 [DHCP](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol "wikipedia:Dynamic Host Configuration Protocol")，或者不变的*静态*地址。请选择一种方式，同时使用多个设置方式可能会引起冲突。

### 动态 IP 地址

#### systemd-networkd

一种DHCP的简单配置方法是利用systemd提供的[systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd")服务。参见[systemd-networkd#Basic DHCP network](/index.php/Systemd-networkd#Basic_DHCP_network "Systemd-networkd")。

#### dhcpcd

[dhcpcd](/index.php/Dhcpcd "Dhcpcd") 是 Arch Linux 安装 ISO 上默认的 DHCP 客户端，功能强大，有多种客户端配置选项。启用方式请参考 [dhcpcd#Running](/index.php/Dhcpcd#Running "Dhcpcd")。

#### netctl

[netctl](/index.php/Netctl "Netctl")是利用用户创建的profiles进行网络配置的CTI-based工具，如何创建profile参见[netctl#Example profiles](/index.php/Netctl#Example_profiles "Netctl")，激活参见[netctl#Basic method](/index.php/Netctl#Basic_method "Netctl")。

### 静态 IP 地址

不管用什么方法设置静态 IP，都需要确定：

*   静态IP地址，
*   [子网掩码](https://en.wikipedia.org/wiki/Subnetwork "wikipedia:Subnetwork")，使用 [CIDR 表示法](https://en.wikipedia.org/wiki/CIDR_notation "wikipedia:CIDR notation")
*   [CIDR 表示法](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation "wikipedia:Classless Inter-Domain Routing") 的子网掩码，例如 `255.255.255.0` 按 CIDR 表示为 `/24`
*   [广播地址](https://en.wikipedia.org/wiki/Broadcast_address "wikipedia:Broadcast address")，
*   [网关](https://en.wikipedia.org/wiki/Default_gateway "wikipedia:Default gateway")的IP地址
*   Name server (DNS) IP addresses. See also [resolv.conf](/index.php/Resolv.conf "Resolv.conf").

如果你想配置一个内部网络，可以将你的 IP 设置成 192.168.*.* ，子网掩码设置成 255.255.255.0 ，广播地址设置成 192.168.*.255 。网关通常是 192.168.*.1 或者 192.168.*.254。

**Warning:**

*   请确保手动设置的 IP 地址不会和 DHCP 自动分配的地址冲突，参考 [这个论坛帖子](http://www.raspberrypi.org/forums/viewtopic.php?f=28&t=16797)
*   在不使用路由器的情况下和一台安装 Windows 的电脑分享你的网络连接，请确保两台电脑都使用静态 IP ，否则你的局域网将会有问题。

#### netctl

要创建 [netctl](/index.php/Netctl "Netctl") 静态 IP 配置，设置 `IP=static` 选项以及 `Address`, `Gateway` 和 `DNS`. 参考 [netctl#Wired](/index.php/Netctl#Wired "Netctl").

#### systemd-networkd

[systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") 服务可以使用简单的配置文件配置静态 IP 地址，参考 [systemd-networkd#Wired adapter using a static IP](/index.php/Systemd-networkd#Wired_adapter_using_a_static_IP "Systemd-networkd").

#### dhcpcd

参考 [dhcpcd#Static profile](/index.php/Dhcpcd#Static_profile "Dhcpcd").

#### 手动指定

可以利用[iproute2](https://www.archlinux.org/packages/?name=iproute2)来手动指定静态 IP。这种方法设置的IP在重启后不会保留，因此这是一个测试连接的好方法。首先开启[network interface](#Network_interfaces)：

```
 # ip link set *interface* up

```

在终端中指定一个静态 IP：

```
# ip addr add *IP_address*/*subnet_mask* broadcast *broadcast_address* dev *interface*

```

如此添加你的网关（用你的网关 IP 替换）：

```
# ip route add default via <默认网关的 IP 地址>

```

例如：

```
# ip link set eth0 up
# ip addr add 192.168.1.2/24 dev eth0
# ip route add default via 192.168.1.1

```

**Tip:** 如果遇到 `RTNETLINK answers: Network is unreachable`错误，请将路由创建步骤拆成两步：
```
# ip route add 192.168.1.1 dev eth0
# ip route add default via 192.168.1.1 dev eth0

```

要撤销设置 (例如将要切换成动态 IP 前)，先删除所有关联的 IP 地址:

```
# ip addr flush dev *interface*

```

然后删除指定的网关：

```
# ip route flush dev *interface*

```

最后禁用接口：

1.  ip link set *interface* down

更多选项参见：[ip(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip.7)，这些命令可以用 systemd 服务自动启动，请参考[systemd units](/index.php/Systemd#Writing_unit_files "Systemd").

#### 计算地址

可以用 [ipcalc](https://www.archlinux.org/packages/?name=ipcalc) 软件包提供的 `ipcalc` 工具自动计算 IP 广播、子网掩码、主机范围等。例如通过火线连接视窗系统主机到 Arch。为了安全和网络组织，将它们分到独立的网络中，然后配置子网掩码和广播地址，网络中只有2台主机。要找出掩码和广播地址，我使用了 ipcalc，提供了它 arch firewire nic 的 IP 地址10.66.66.1，并告诉 ipcalc 要建立一个只有2台主机的网络。

 `$ ipcalc -nb 10.66.66.1 -s 1` 
```
Address:   10.66.66.1

Netmask:   255.255.255.252 = 30
Network:   10.66.66.0/30
HostMin:   10.66.66.1
HostMax:   10.66.66.2
Broadcast: 10.66.66.3
Hosts/Net: 2                     Class A, Private Internet

```

### IP 地址

[IP addresses](https://en.wikipedia.org/wiki/IP_address "wikipedia:IP address")使用[ip-address(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-address.8)管理。

显示 IP 地址：

```
$ ip address show

```

向某接口添加一个 IP：

```
# ip address add *地址/前缀长度* broadcast + dev *interface*

```

	请注意:

*   地址格式是[CIDR 标记](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation "wikipedia:Classless Inter-Domain Routing")格式，这种格式也可以提供[子网掩码](https://en.wikipedia.org/wiki/Subnetwork "wikipedia:Subnetwork")。
*   `+`是一种特殊符号，使`ip`程序从 IP 地址和子网掩码获得[广播地址](https://en.wikipedia.org/wiki/Broadcast_address "wikipedia:Broadcast address")。

**Note:** 确保手动分配的 IP 和 DHCP 分配的不冲突。

从某接口删除一个 IP 地址：

```
$ ip address del *地址/前缀长度* dev *interface*

```

删除所有符合某种条件的地址，例如删除特定接口下的地址：

```
$ ip address flush dev *interface*

```

**Tip:** 可以使用 [ipcalc](http://jodies.de/ipcalc) ([ipcalc](https://www.archlinux.org/packages/?name=ipcalc)) 计算 IP 地址。

### 路由表

[routing table](https://en.wikipedia.org/wiki/Routing_table "wikipedia:Routing table")用于决定是否能直连某个 IP 地址，或者应该使用哪个网关（路由器）进行通信。如果 IP 地址不匹配任何路由，就会走[默认网关](https://en.wikipedia.org/wiki/Default_gateway "wikipedia:Default gateway")。

路由表由[ip-route(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-route.8)管理。

*PREFIX*要么是 CIDR 标记，要么是`default`（默认网关）。

显示路由表：

```
$ ip route show

```

添加路由：

```
# ip route add *PREFIX* via *address* dev *interface*

```

删除路由：

```
# ip route del *PREFIX* via *address* dev *interface*

```

## 更多设置

### 笔记本电脑使用 Ifplugd

**Tip:** [dhcpcd](/index.php/Dhcpcd "Dhcpcd") 也提供了同样的功能。

[官方仓库](/index.php/%E5%AE%98%E6%96%B9%E4%BB%93%E5%BA%93 "官方仓库") 中的 [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) 是一个守护进程，当网络适配器插入的时候自动配置网络，当网络断开的时候自动取消配置（比如某些3G的usb网络适配器）。这对于笔记本电脑这样的使用移动式的网络适配器的情况很有用，因为他只会在网络实际接入的时候才会配置网络接口。另外一个可能会用得着它的情况是，你需要重启你的网络，可是你既不想重启电脑也不想在 shell 中配置。

在默认情况下，它会检查 `eth0` 设备。要更改这个设置（以及更改其他设置，比如等待时间），可以编辑 `/etc/ifplugd/ifplugd.conf`。

启用 `net-auto-wired.service` 就会在开机时启动 ifplugd，否则，你可以使用 `ifplugd@eth0.service`。

**注意:** [Netctl](/index.php/Netctl "Netctl") 软件包包含了 `netctl-ifplugd@.service`，否则你可以使用 [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) 软件包中的 `ifplugd@.service`。例如 `systemctl enable ifplugd@eth0.service`。

### 绑定和链路聚合

参见 [绑定](/index.php/Netctl_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#绑定 "Netctl (简体中文)") 或 [无线网络绑定](/index.php/%E6%97%A0%E7%BA%BF%E7%BD%91%E7%BB%9C%E7%BB%91%E5%AE%9A "无线网络绑定")。

### IP 别名

IP 别名是指给同一个网络接口分配多个 IP 地址。这样一个网络节点可以有多个网络连接，每个实现不同的作用。典型的用处是 Web 服务器和 FTP 服务器的虚拟主机，或者是重组服务器时不需要更新其他任何机器上的 IP （对于名称服务器来说很有用）。

要手动设置别名，可以使用 [iproute2](https://www.archlinux.org/packages/?name=iproute2) 执行：

```
# ip addr add 192.168.2.101/24 dev eth0 label eth0:1

```

要删除别名：

```
# ip addr del 192.168.2.101/24 dev eth0:1

```

发送到一个子网的软件不会使用主别名，如果目标 IP 属于子别名，原始 IP 也会被相应设置。如果有多个网卡，可以通过 `ip route` 查看默认路由。

### 更改 MAC/硬件地址

参见 [伪造 MAC 地址](/index.php/MAC_address_spoofing "MAC address spoofing")。

### 共享网络连接

参见 [共享网络连接](/index.php/Internet_sharing "Internet sharing")。

### 路由配置

参见 [路由](/index.php/Router "Router")。

### 局域网主机的名称解析

首先需要设置好主机名。

 `$ ping *myhostname*` 
```
PING myhostname (192.168.1.2) 56(84) bytes of data.
64 bytes from myhostname (192.168.1.2): icmp_seq=1 ttl=64 time=0.043 ms
```

如果希望其他机器通过主机名访问到这台机器，可以手动修改 `/etc/hosts` 文件或通过一个服务解析此主机名。使用 systemd 时，主机名解析可以通过 `myhostname` nss 模块提供。但是并不是所有的网络服务都被支持 (例如: [[4]](https://bbs.archlinux.org/viewtopic.php?id=176761), [[5]](https://bbs.archlinux.org/viewtopic.php?id=186967))，或者其它客户端使用不同的操作系统解析主机名，这个也无法被 systemd 支持。

第一个解决方法是修改 `/etc/hosts`:

```
127.0.1.1	*myhostname*.localdomain	*myhostname*	

```

这样系统可以同时解析两个主机名:

```
$ getent hosts 
127.0.0.1       localhost
127.0.1.1       myhostname.localdomain myhostname

```

如果使用固定 IP 地址，请用 IP 地址替换 `127.0.1.1`.

还有一个方法是架设 DNS 服务器例如 [BIND](/index.php/BIND "BIND") or [Unbound](/index.php/Unbound "Unbound"), 但是这些方法有点小提大作。小的网络可以使用 [zero-configuration networking](https://en.wikipedia.org/wiki/Zero-configuration_networking "wikipedia:Zero-configuration networking") 服务。有两个选择：

*   [Samba](/index.php/Samba "Samba") 通过 Microsoft's **NetBIOS** 提供主机名称解析。这只需要安装 [samba](https://www.archlinux.org/packages/?name=samba) 并启用 `nmbd.service` 服务。运行 Windows、 OS X、或者运行着 `nmbd` 的 Linux，将能找到你的机器。

*   [Avahi](/index.php/Avahi "Avahi") 通过 **zeroconf**，提供主机名称解析, 它也被称称作 Avahi 或者 Bonjour。这需要比 Samba 再稍微复杂一点的配置：详细信息参见 [Avahi#Hostname resolution](/index.php/Avahi#Hostname_resolution "Avahi")。运行 OS X 的电脑，或者运行着 Avahi 守护进程的 Linux，将能找到你的机器。Windows 没有内置的 Avahi 客户端或者守护进程。

### 全接收模式

切换网卡到 [全接收模式](https://en.wikipedia.org/wiki/Promiscuous_mode "wikipedia:Promiscuous mode") 可以让网卡接收所有数据然后转交给操作系统处理。而正常模式下，网卡会丢掉不是不发给自己的数据。通常用来检查网络问题或进行 [数据包嗅探](https://en.wikipedia.org/wiki/Packet_sniffing "wikipedia:Packet sniffing").

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

如果要在 `eth0` 上启用全接收模式，只需要 [启用](/index.php/Enable "Enable") `promiscuous@eth0.service`.

## 疑难排解

### 更换了连接cable modem的计算机

许多家庭有线电视的运营商（例如加拿大最大的有线电视公司Videotron,还有中国大陆的有线电视宽带公司）都使用记录网卡MAC地址的方法将cable modem配置为只能一台计算机使用。一旦cable modem获得第一台连接它的PC的MAC地址，就不会响应任何其它MAC地址。这样如果你换了台PC（或者路由器），由于新PC（或者路由器）的MAC地址和旧的不同，就没法连接cable modem了。这时候必须复位cable modem以使它重新辨认新的PC。 你得关闭cable modem电源，然后重新打开。一旦cable modem重启并再次登录在线完毕（指示灯熄灭），重启新连接的PC以使它发起一个DHCP请求，或者手动发起DHCP请求。

如果这个方法不能奏效，你需要克隆原来机器上的MAC地址。参见 [Change MAC/hardware address](/index.php/Configuring_Network#Change_MAC/hardware_address "Configuring Network")。

### TCP窗口扩缩（window scaling）故障

TCP包头有个窗口（window）值表明其它主机可以发送多少数据回来。这个值只有16个bit，也就是说窗口打消最多只有64Kb。TCP包会被缓存一段时间（得被记录），如果内存限制（过去经常是）的话，主机很容易会用完内存。

回到1992年，内存逐渐增加，[RFC 1323](http://www.faqs.org/rfcs/rfc1323.html)被发布以改善情况:窗口扩缩(Window Scaling)。所有包里的窗口值，可以被初始连接时定义的一个缩放因子（Scale Factor）所改变。

8-bit的缩放因子使得窗口可以是初始64Kb的32倍。

但是Internet上有些有故障的路由器和防火墙会将缩放因子重写为0,这导致主机之间产生误解。

Linux内核2.6.17引入了新的计算方式生成更高的缩放因子，间接的使得这些有故障的路由器和防火墙引发的后果更明显。

这导致连接缓慢甚至中断。

#### 如何诊断故障

首先，我们要明白：这个问题很怪异。在某些案例中，你根本无法使用(HTTP, FTP, ...)，而有时候，你可以连接某些主机（很少）。

当你碰到这个故障时，`dmesg`的输出正确，日志也没问题，`ip a`报告状态正常— 实际上一切都正常。

如果你无法浏览任何网站，不过你能ping通少部分主机，很可能你是遇到了这个问题。：ping使用ICMP协议所以不受TCP问题的影响。

你可以尝试使用WireShark。你也许会看到UDP和ICMP通讯成功，但是TCP通讯不成功（仅对外国主机）。

#### 如何修复（糟糕的方法）

用比较糟糕的方法修复的话，你可以修改缩放因子计算所基于的tcp_rmem值。虽然它对大部分主机有效，但并不担保一定都有效，特别是某些很远的主机。

```
# echo "4096 87380 174760" > /proc/sys/net/ipv4/tcp_rmem

```

#### 如何修复（好点的方法）

只需要禁止窗口缩放。虽然窗口缩放是个不错的TCP特性，但它也可能令人不安，特别是当你没法修改除了问题的路由器的时候。有几种方法可以禁止窗口缩放，而看来最可靠的（适用于大部分内核）将下面一行加入到你的`/etc/sysctl.d/99-disable_window_scaling.conf` 中 （见 [sysctl](/index.php/Sysctl "Sysctl")）

```
net.ipv4.tcp_window_scaling = 0

```

#### 如何修复（最佳的方法）

这个故障是由有毛病的路由器/防火墙引致的，所以最好换了它。有些用户报告说那些有故障的路由是他们自己的DSL路由。

#### 更多

本段内容是基于LWN文章[TCP window scaling and broken routers](http://lwn.net/Articles/92727/)和一个Kernel Trap 文章：[Window Scaling on the Internet](http://kerneltrap.org/node/6723)。

在LKML上也有几篇相关的帖子。

### Realtek 没有连接/网络唤醒故障

使用基于Realtek 8168 8169 8101 8111芯片网卡（独立网卡和板载）的用户也许会发现这个故障，启动时网卡不可用，网卡上的连接指示灯不亮。这通常会发生在安装了Windows的双启动系统上。在windows下使用realtek官方驱动（2007年5月后的版本）会引发故障。新驱动通过在Windows关机时禁止网卡来关闭网络唤醒功能，直到下一次Windows启动前网卡都会一直不可用。通过观察连接指示灯在Windows启动前一直熄灭，而Windows关机时也会熄灭，你可以发现它。正常操作应该是只要系统一直开着，即使在POST加电过程中，连接指示灯也应该一直亮着的。这个故障也会影响其它没有安装新驱动的操作系统（例如Live CD等）。这里给出几种解决方案：

#### 在 Linux 中启用网卡

参考上面的启用和禁用网络接口段落。

#### 方法一 还原/变更Win驱动

你可以将你的Windows网卡驱动还原回Microsoft自带的驱动（如果有的话），或者安装2007年5月份以前的Realtek官方驱动（也许在网卡附带的CD上）。

#### 方法二 启动Windows驱动里的网络唤醒功能

也许最好最快的修复方法就是改变Windows驱动里的这个设置。这个方法可以解决很多其它操作系统而不仅仅是Arch的麻烦。在Windows的设备管理器里，找到你的Realtek网卡，双击它。在“高级”标签页中，开启"wake-on-lan after shutdown"选项。

```
 例如在Windows XP里
 右键点击我的电脑-->管理-->设备管理器-->网络适配器-->双击 Realtek ... --> 高级标签页--> Wake-On-Lan After Shutdown --> 启用。

```

**注意:** 新的 Realtek Windows 驱动程序中（已测试了 2009/01/22 GIGABYTE 上的 *Realtek 8111/8169 LAN Driver v5.708.1030.2008*）可能与这里的选项稍微有点不同，像 *Shutdown Wake-On-LAN --> Enable*。似乎把它切换成 `Disable` 没有效果（你仍然可以在Windows关闭时看到连接指示灯熄灭）。一个比较不好的解决方法是引导 Windows，然后立即重启系统（执行非正常重启/关机），不给予 Windows 驱动程序关闭 LAN 的机会。连接指示灯将会保持亮着，网卡也会在 POST 之后保持可用 - 直到你再次进入 Windows 并正常关机。

#### 方法三 更新Realtek Linux驱动

可以在realtek的官方网页上找到新的Linux驱动。(没有测试过，不过相信也能解决问题）。

#### 方法四 在 BIOS/CMOS 中启用 *LAN Boot ROM*

尽管 Windows 驱动程序在系统关闭时禁用了它，但在 BIOS/CMOS 中设置 *Integrated Peripherals --> Onboard LAN Boot ROM --> Enabled*，系统启动时会重新激活 Realtek LAN 芯片。

**注意:** 这个方法多次在 GIGABYTE GA-G31M-ES2L 主板，2009/02/05 发布的 BIOS 版本 F8 上测试成功。YMMV。

### 检查 DHCP 问题先释放 IP 地址

当 DHCP 获得了错误的 IP 分配就可能产生这个问题。举例来说，当两个路由器通过VPN相连，通过VPN与我相连的路由器可能分配IP地址。要修复这个问题，在终端中以 root 权限释放 IP 地址：

```
# dhcpcd -k

```

然后请求一个新的地址：

```
# dhcpcd

```

可能你必须运行这两个命令好几次。

### Atheros 芯片组找不到网卡

有些用户的 Atheros 芯片无法正常工作 (至少在 2014.2 月的安装中). 可以通过安装 [backports-patched](https://aur.archlinux.org/packages/backports-patched/) 解决。

### Broadcom BCM57780

这个 Broadcom 芯片只有你指定模块的加载顺序后才能正常工作。这些模块是 `broadcom` 和 `tg3`，前者需要首先加载。

如果你的电脑有这个芯片，这些步骤应该有用：

```
$ lspci | grep Ethernet
02:00.0 Ethernet controller: Broadcom Corporation NetLink BCM57780 Gigabit Ethernet PCIe (rev 01)

```

如果你的有线网络不能工作，尝试断开网线，然后以 root 权限实施以下步骤：

```
# modprobe -r tg3
# modprobe broadcom
# modprobe tg3

```

现在接入网线。如果现在你的故障解决了，你可以把 `broadcom` 和 `tg3` （以此顺序）加入到 `/etc/mkinitcpio.conf` 的 `MODULES` 一行，使得变更持久化：

```
MODULES=".. broadcom tg3 .."

```

然后重新编译 initramfs:

```
# mkinitcpio -p linux

```

*   还有一种方法是创建 `/etc/modprobe.d/broadcom.conf`:

```
 softdep tg3 pre: broadcom

```

**注意:** 这些方法可能也适用于其它芯片，例如 BCM57760。

### Realtek RTL8111/8168B

 `# lspci | grep Ethernet` 
```
03:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168B PCI Express Gigabit Ethernet controller (rev 02)

```

The adapter should be recognized by the `r8169` module. However, with some chip revisions the connection may go off and on all the time. The alternative [r8168](https://www.archlinux.org/packages/?name=r8168) can be found in the [official repositories](/index.php/Official_repositories "Official repositories") and should be used for a reliable connection in this case. [Blacklist](/index.php/Kernel_modules#Blacklisting "Kernel modules") `r8169`, if [r8168](https://www.archlinux.org/packages/?name=r8168) is not automatically loaded by [udev](/index.php/Udev "Udev")，see [Kernel modules#Automatic module handling](/index.php/Kernel_modules#Automatic_module_handling "Kernel modules")。

Another fault in the drivers for some revisions of this adapter is poor IPv6 support. [IPv6#Disable functionality](/index.php/IPv6#Disable_functionality "IPv6") can be helpful if you encounter issues such as hanging webpages and slow speeds.

### Gigabyte Motherboard with Realtek 8111/8168/8411

With motherboards such as the Gigabyte GA-990FXA-UD3, booting with IOMMU off (which can be the default) will cause the network interface to be unreliable, often failing to connect or connecting but allowing no throughput. This will apply not only to the onboard NIC, but any other pci-NIC you put in the box because the IOMMU setting affects the entire network interface on the board. Enabling IOMMU and booting with the install media will throw AMD I-10/xhci page faults for a second, but then boot normally, resulting in a fully functional onboard NIC (even with the r8169 module).

When configuring the boot process for your installation, add `iommu=soft` as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") to eliminate the error messages on boot and restore USB3.0 functionality.