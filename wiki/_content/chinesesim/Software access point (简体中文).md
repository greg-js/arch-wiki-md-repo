**翻译状态：** 本文是英文页面 [Software_access_point](/index.php/Software_access_point "Software access point") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-08-23，点击[这里](https://wiki.archlinux.org/index.php?title=Software_access_point&diff=0&oldid=393095)可以查看翻译后英文页面的改动。

当你想让你的电脑变成一个Wifi接入点时，你需要一个无线AP。它能帮你免去你购买配置一个无线路由器的麻烦。

## Contents

*   [1 要求](#.E8.A6.81.E6.B1.82)
    *   [1.1 无线网卡必须支持AP模式](#.E6.97.A0.E7.BA.BF.E7.BD.91.E5.8D.A1.E5.BF.85.E9.A1.BB.E6.94.AF.E6.8C.81AP.E6.A8.A1.E5.BC.8F)
    *   [1.2 一张网卡同时作为AP和连接其他无线网络的客户端](#.E4.B8.80.E5.BC.A0.E7.BD.91.E5.8D.A1.E5.90.8C.E6.97.B6.E4.BD.9C.E4.B8.BAAP.E5.92.8C.E8.BF.9E.E6.8E.A5.E5.85.B6.E4.BB.96.E6.97.A0.E7.BA.BF.E7.BD.91.E7.BB.9C.E7.9A.84.E5.AE.A2.E6.88.B7.E7.AB.AF)
*   [2 概述](#.E6.A6.82.E8.BF.B0)
*   [3 无线链路层](#.E6.97.A0.E7.BA.BF.E9.93.BE.E8.B7.AF.E5.B1.82)
*   [4 网络配置](#.E7.BD.91.E7.BB.9C.E9.85.8D.E7.BD.AE)
    *   [4.1 网桥设置](#.E7.BD.91.E6.A1.A5.E8.AE.BE.E7.BD.AE)
    *   [4.2 NAT设置](#NAT.E8.AE.BE.E7.BD.AE)
*   [5 工具](#.E5.B7.A5.E5.85.B7)
    *   [5.1 create_ap](#create_ap)
    *   [5.2 RADIUS](#RADIUS)
*   [6 常见问题与解答](#.E5.B8.B8.E8.A7.81.E9.97.AE.E9.A2.98.E4.B8.8E.E8.A7.A3.E7.AD.94)
    *   [6.1 无线局域网很慢](#.E6.97.A0.E7.BA.BF.E5.B1.80.E5.9F.9F.E7.BD.91.E5.BE.88.E6.85.A2)
    *   [6.2 NetworkManager影响网卡](#NetworkManager.E5.BD.B1.E5.93.8D.E7.BD.91.E5.8D.A1)
*   [7 相关文章](#.E7.9B.B8.E5.85.B3.E6.96.87.E7.AB.A0)

## 要求

### 无线网卡必须支持AP模式

你需要一个兼容 [nl80211](http://wireless.kernel.org/en/developers/Documentation/nl80211) 的网卡（nl80211网卡支持AP模式[网卡模式](http://wireless.kernel.org/en/users/Documentation/modes)）。你可以输入 `iw list` 命令, 查看 `Supported interface modes`以下的几行，看是否支持 `AP` 模式:

 `$ iw list` 

```
Wiphy phy1
...
	Supported interface modes:
		 * IBSS
		 * managed
		 * **AP**
		 * AP/VLAN
		 * WDS
		 * monitor
		 * mesh point
...

```

### 一张网卡同时作为AP和连接其他无线网络的客户端

创建一个无线AP是独立于该网卡其他的网络连接。许多网卡甚至可以支持同时作为AP和客户端。 这样一张网卡你就可以做一个无线中继。 你可以输入 `iw list` 命令, 查看 `valid interface combinations:`　以下的几行，看是否支持无线中继:

 `$ iw list` 

```
Wiphy phy1
...
        valid interface combinations:
                 * #{ managed } <= 2048, #{ AP, mesh point } <= 8, #{ P2P-client, P2P-GO } <= 1,
                   total <= 2048, #channels <= 1, STA/AP BI must match
...
```

参数`#channels <= 1`说明你的无线AP必须和你接入的Wifi热点处于同一信道。 你会在`hostapd.conf`中的 `channel` 设置中看到。

你需要开启两个虚拟网络接口来使用这种特性。一个是用来连接其他热点， `wlan0_sta`。另一个作为无线AP，`wlan0_ap`。

```
iw dev wlan0 interface add wlan0_sta type station  
iw dev wlan0 interface add wlan0_ap  type __ap     

```

接来下，你可以随意给两个借口设置不同的MAC地址

```
ip link set dev wlan0_sta address 12:34:56:78:ab:cd
ip link set dev wlan0_ap  address 12:34:56:78:ab:ce

```

## 概述

设置一个AP需要两个部分

*   设置 **无线链路层**：其他客户端就可以连接这个AP并接受发送IP包， 这就是hostpad包帮你做的.
*   网络配置： 你的电脑将从因特网连接正确的转发IP数据包到无线客户端。

## 无线链路层

修改hostpad配置是很有必要的. 尤其是修改`ssid`和`wpa_passphrase`. 查看 [hostapd Linux documentation page](http://wireless.kernel.org/en/users/Documentation/hostapd) 来参考更多内容.

 `/etc/hostapd/hostapd.conf` 

```
ssid=YourWiFiName
wpa_passphrase=Somepassphrase
interface=wlan0_ap
bridge=br0
auth_algs=3
channel=7
driver=nl80211
hw_mode=g
logger_stdout=-1
logger_stdout_level=2
max_num_sta=5
rsn_pairwise=CCMP
wpa=2
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP CCMP

```

[启用](/index.php/Daemon "Daemon")`hostapd.service`来开启hostapd。

**Warning:** AP可选用的信道根据地域而不同。 根据无线网卡的固件，你必须设置正确的地区来确定信道。 **不要** 选择另外的地区，因为你可能因此扰乱其他的网络交通， 在信号覆盖内影响你的网卡和其它网卡的运作！ 设置信道请看[Wireless network configuration#Respecting the regulatory domain](/index.php/Wireless_network_configuration#Respecting_the_regulatory_domain "Wireless network configuration").

**Note:** 如果你的网卡是基于RTL8192CU芯片组,请从[AUR](/index.php/AUR "AUR")中安装[hostapd-8192cu](https://aur.archlinux.org/packages/hostapd-8192cu/)并在`hostapd.conf` 文件中将`driver=nl80211` 换成 `driver=rtl871xdrv`。

## 网络配置

有两种方法实现：

1.  **网桥**: 在你的电脑上搭一个网桥 （无线客户端就像是和你本人电脑访问的网络接口和子网一样）
2.  **NAT**: 通过IP转发／掩藏 和 DHCP服务 （无线客户端会专门使用一个子网 —— 就像是连接在调制调节器上的一个普通的无线路由器一样)

使用网桥会更加简单,但它要求任何无线客户端需要的服务 （比方说，DHCP）能被你的无线网卡所满足。也就是说拨号服务是不能使用网桥的 （比方说， 通过PPPoE或者3G调制调解器）或者你使用有线调制调解器且通过DHCP只分配了一个IP。

使用NAT会更加灵活。 NAT把Wifi客户端和你的电脑分离开来并且对外界完全不可见。 对于任何种类的网络连接它都适用，而且 （如果必要的话）你可以使用iptables来控制流量。

当然，将两者_联合起来_也是可能的. 那么你需要分别参考相关的文章。 比方说：使用网桥将以太网设备和无线网用静态IP连起来，同时使用DHCP并设置NAT去转发流量到另外一个网络设备（ppp或者 eth）。

### 网桥设置

你应该创建一个 _网桥_ 并连上网络设备 （比方说 `eth0`） 。 你 **不应该** 自行加上一个无线网络设备 （比方说`wlan0`） 在那个桥上， 因为hostapd会自行帮你加上去的。

参阅 [Network bridge](/index.php/Network_bridge "Network bridge")。

**Tip:** 你可以重用一个网桥，如果你的虚拟机已经有了一个网桥的话。

### NAT设置

详细内容请参考[Internet sharing](/index.php/Internet_sharing "Internet sharing")。

那篇文章里，连接LAN的设备是 `net0`。 这里我们通常指的是的你的无线网卡，比如说 `wlan0`。

## 工具

### create_ap

可以用[create_ap](https://bbs.archlinux.org/viewtopic.php?pid=1269258) 脚本[AUR](/index.php/AUR "AUR") [create_ap](https://aur.archlinux.org/packages/create_ap/)融合了 [hostapd](https://www.archlinux.org/packages/?name=hostapd), [dnsmasq](/index.php/Dnsmasq "Dnsmasq") 和 [iptables](/index.php/Iptables "Iptables") 创建NAT/桥接 AP。

### RADIUS

可以参阅 [[1]](https://me.m01.eu/blog/2012/05/wpa-2-enterprise-from-scratch-on-a-raspberry-pi/) 来运行 [FreeRADIUS](http://freeradius.org/) 服务器 [WPA2 Enterprise](/index.php/WPA2_Enterprise "WPA2 Enterprise").

## 常见问题与解答

### 无线局域网很慢

可能由熵值过低造成。 可以安装 [haveged](/index.php/Haveged "Haveged") 试试.

### NetworkManager影响网卡

如果网卡被NetworkManager管理的话，hostapd可能不起作用. 你可以掩盖这个设备:

 `/etc/NetworkManager/NetworkManager.conf` 

```
[keyfile]
unmanaged-devices=mac:<hwaddr>

```

## 相关文章

*   [Router](/index.php/Router "Router")
*   [Hostapd : The Linux Way to create Virtual Wi-Fi Access Point](http://nims11.wordpress.com/2012/04/27/hostapd-the-linux-way-to-create-virtual-wifi-access-point/)
*   [tutorial and script for configuring a subnet with DHCP and DNS](http://xyne.archlinux.ca/notes/network/dhcp_with_dns.html)