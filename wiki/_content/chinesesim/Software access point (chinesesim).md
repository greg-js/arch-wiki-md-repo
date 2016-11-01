**翻译状态：** 本文是英文页面 [Software_access_point](/index.php/Software_access_point "Software access point") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-03-13，点击[这里](https://wiki.archlinux.org/index.php?title=Software_access_point&diff=0&oldid=420459)可以查看翻译后英文页面的改动。

软件接入点是在你要让你的电脑当作一个本地网络的Wi-Fi接入点时使用的。它免除了你去弄一个独立无线路由器的麻烦。

## Contents

*   [1 要求](#.E8.A6.81.E6.B1.82)
    *   [1.1 无线网卡必须支持AP模式](#.E6.97.A0.E7.BA.BF.E7.BD.91.E5.8D.A1.E5.BF.85.E9.A1.BB.E6.94.AF.E6.8C.81AP.E6.A8.A1.E5.BC.8F)
    *   [1.2 单个Wi-Fi设备同时作为无线客户端和AP](#.E5.8D.95.E4.B8.AAWi-Fi.E8.AE.BE.E5.A4.87.E5.90.8C.E6.97.B6.E4.BD.9C.E4.B8.BA.E6.97.A0.E7.BA.BF.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.92.8CAP)
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
    *   [6.2 NetworkManager的干扰](#NetworkManager.E7.9A.84.E5.B9.B2.E6.89.B0)
*   [7 相关文章](#.E7.9B.B8.E5.85.B3.E6.96.87.E7.AB.A0)

## 要求

### 无线网卡必须支持AP模式

你需要一个兼容 [nl80211](http://wireless.kernel.org/en/developers/Documentation/nl80211) 的无线设备,并且该设备支持AP[operating mode](http://wireless.kernel.org/en/users/Documentation/modes)模式。这可以通过运行`iw list`命令来验证, 在`Supported interface modes`区块下面应该列出 `AP` 模式:

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

### 单个Wi-Fi设备同时作为无线客户端和AP

创建一个软件无线AP不依赖于你自己的网络连接方式(以太网,无线网,......)。许多无线设备甚至可以支持*并存*操作,同时既作为AP又作为无线*客户端*。 使用这种能力,你可以为现有网络创建一个软件AP作为一个*无线中继器*。 设备是否支持这种能力,被列在如下栏目中 `iw list` 命令的输出中:

 `$ iw list` 
```
Wiphy phy1
...
        valid interface combinations:
                 * #{ managed } <= 2048, #{ AP, mesh point } <= 8, #{ P2P-client, P2P-GO } <= 1,
                   total <= 2048, #channels <= 1, STA/AP BI must match
...
```

约束`#channels <= 1`说明你的软件AP必须和你的Wi-fi客户端连接处于同一信道来运作。 参见`channel`里的`hostapd.conf`设置。

如果你需要这种能力/特性,可能是因为以太网络连接不可用,你为了使用它需要创建两个分立的*虚拟网络接口*。 物理设备 `wlan0_sta` 的虚拟网络接口可能通过如下方式来创建:

首先,*虚拟网络接口*是为网络连接 `wlan0_sta` 自身和软件AP/hostapd"无线中继器"创建的。

```
iw dev wlan0 interface add wlan0_sta type station  
iw dev wlan0 interface add wlan0_ap  type __ap     

```

其次,这个接口被分配不同的MAC地址(使用用户唯一地址)

```
ip link set dev wlan0_sta address 12:34:56:78:ab:cd
ip link set dev wlan0_ap  address 12:34:56:78:ab:ce

```

## 概述

设置一个接入点包含两个主要部分:

*   设置 **Wi-Fi链路层**,这样无线客户端可以加入你电脑的"软件接入点"并在你的电脑间来回收发IP包; 这是hostapd包将为你做的.
*   在你的电脑上建立**网络配置**, 这样你的电脑可以在Internet连接和无线客户端之间有效地转发IP包.

## 无线链路层

其实Wi-Fi链路是通过[hostapd](https://www.archlinux.org/packages/?name=hostapd)包来建立的,且支持WPA2.

如果有必要,调整*hostpad*配置里的选项. 尤其是修改`ssid`和`wpa_passphrase`. 参见 [hostapd Linux documentation page](http://wireless.kernel.org/en/users/Documentation/hostapd) 来获取更多内容.

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

**Tip:** 你可以用UTF-8字符来创建SSID, 所以国际化的字符都可以正常显示了. 启用这个选项用`utf8_ssid=1`. 一些客户端在识别正确的编码时可能会有问题(如:[wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant")或windows 7).

当启动hospapd时,请确认无线网络接口已经在之前正确启动了.

```
# ip link set dev wlan0_ap up

```

否则,会启动失败,提示节点脚本错误:"不能配置驱动模式".

为了自动启动hostapd, [Enable](/index.php/Daemon "Daemon") `hostapd.service`.

**Warning:** 根据地域的不同允许作为接入点的无线信道是不同的。 根据无线设备的固件, 你应当设置正确的地区来使用合法的信道。 **不要**选择非本地区域, 这样你可能非法扰乱网络通讯, 在信号覆盖范围内影响你和他人设备的无线功能! 区域信道参见[Wireless network configuration#Respecting the regulatory domain](/index.php/Wireless_network_configuration#Respecting_the_regulatory_domain "Wireless network configuration").

**Note:** 如果你有一个基于RTL8192CU芯片组的网卡, 请从[AUR](/index.php/AUR "AUR")中安装[hostapd-8192cu](https://aur.archlinux.org/packages/hostapd-8192cu/)并在`hostapd.conf` 文件中将`driver=nl80211` 换成 `driver=rtl871xdrv`。

## 网络配置

有两种基本的方法来实现：

1.  **网桥**: 在你的电脑上搭一个网桥 （无线客户端就可以像使用你的电脑一样访问同一个网络接口和同一个子网）
2.  **NAT**: 通过IP转发/伪装 和 DHCP服务 （无线客户端会专门使用一个子网, 数据进出这个子网是被网络地址转换的(NAT-ted) —— 就像是连接在你数字用户回路(DSL)或铜轴线(Cabel)调制解调器上的一个普通的无线路由器一样)

使用网桥方式会更加简单, 但它要求无线客户端所需要的任何服务 (比方说，DHCP) 在你电脑的外部接口上是可用的。也就是说如果你使用拨号连接(如,通过PPPoE或3G调制解调器)或你在使用铜轴线调制解调器,它会通过DHCP提供一个确定的IP地址, 这些状态下桥接将不能正常工作。

使用NAT方式会更加灵活, NAT把Wi-Fi客户端和你的电脑清晰地分离开来并且对外界完全透明。 对于任何种类的网络连接它都适用，而且（如果必要的话）你可以使用iptables的方式来控制进出策略。

当然，将*两者结合物*也是可能的. 那么, 你需要分别参考相关的文章。 比方说：有一个拥有一个静态IP的网桥既包含以太网设备又有无线设备,提供DHCP服务,和建立配置好的NAT去转发数据到另外一个网络设备（可能是ppp或者 eth）。

### 网桥设置

你应该创建一个 *网桥* 并把你的网络接口（比方说 `eth0`）加入其中 。 你 **不应该**添加无线网络设备 （比方说`wlan0`） 到网桥上；因为hostapd会自行添加。

参阅 [Network bridge](/index.php/Network_bridge "Network bridge")。

**Tip:** 你可能希望重用一个现有的网桥，如果你已经创建了一个.(比如, 虚拟机使用的网桥)。

### NAT设置

详细内容请参考[Internet sharing](/index.php/Internet_sharing "Internet sharing")。

在那篇文章里，连接LAN的设备是 `net0`。 这里我们通常指的是的你的无线设备，比如说 `wlan0`。

## 工具

### create_ap

可以用[create_ap](https://bbs.archlinux.org/viewtopic.php?pid=1269258) 脚本[AUR](/index.php/AUR "AUR") [create_ap](https://www.archlinux.org/packages/?name=create_ap)融合了 [hostapd](https://www.archlinux.org/packages/?name=hostapd), [dnsmasq](/index.php/Dnsmasq "Dnsmasq") 和 [iptables](/index.php/Iptables "Iptables") 来创建桥接或NAT方式的接入点(在[AUR](/index.php/AUR "AUR") [create_ap](https://www.archlinux.org/packages/?name=create_ap)可用)。

### RADIUS

可以参阅 [[1]](https://me.m01.eu/blog/2012/05/wpa-2-enterprise-from-scratch-on-a-raspberry-pi/) 的说明来运行[WPA2企业级加密](/index.php/WPA2_Enterprise "WPA2 Enterprise")的 [FreeRADIUS](http://freeradius.org/) 服务器.

## 常见问题与解答

### 无线局域网很慢

可能由低熵值造成。 考虑安装 [haveged](/index.php/Haveged "Haveged") 试试.

### NetworkManager的干扰

如果网络设备被NetworkManager管理的话，hostapd可能不起作用. 你可以屏蔽(对)这个设备(的管理):

 `/etc/NetworkManager/NetworkManager.conf` 
```
[keyfile]
unmanaged-devices=mac:<hwaddr>

```

## 相关文章

*   [Router](/index.php/Router "Router")
*   [Hostapd : The Linux Way to create Virtual Wi-Fi Access Point](http://nims11.wordpress.com/2012/04/27/hostapd-the-linux-way-to-create-virtual-wifi-access-point/)
*   [tutorial and script for configuring a subnet with DHCP and DNS](http://xyne.archlinux.ca/notes/network/dhcp_with_dns.html)