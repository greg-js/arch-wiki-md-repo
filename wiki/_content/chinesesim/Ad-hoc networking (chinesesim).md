相关文章

*   [网络配置](/index.php/Network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network configuration (简体中文)")
*   [无线设置](/index.php/Wireless_Setup_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wireless Setup (简体中文)")
*   [软AP](/index.php/%E8%BD%AFAP "软AP")
*   [Internet sharing](/index.php/Internet_sharing "Internet sharing")

**翻译状态：** 本文是英文页面 [Ad-hoc_networking](/index.php/Ad-hoc_networking "Ad-hoc networking") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-08-22，点击[这里](https://wiki.archlinux.org/index.php?title=Ad-hoc_networking&diff=0&oldid=463497)可以查看翻译后英文页面的改动。

Independent Basic Service Set(独立基本服务集)，缩写是 IBSS，也被称为自组网络，是一种不使用中心控制节点，就能让一组设备相互通讯的方法。是点对点网络的一种，网络中的设备直接通讯，不需要中转。自组网络可以用来进行 [网络共享](/index.php/Internet_sharing "Internet sharing")。

## Contents

*   [1 要求](#.E8.A6.81.E6.B1.82)
*   [2 Wifi 链路层](#Wifi_.E9.93.BE.E8.B7.AF.E5.B1.82)
    *   [2.1 手动设置](#.E6.89.8B.E5.8A.A8.E8.AE.BE.E7.BD.AE)
    *   [2.2 WPA supplicant](#WPA_supplicant)
*   [3 网络配置](#.E7.BD.91.E7.BB.9C.E9.85.8D.E7.BD.AE)
*   [4 技巧](#.E6.8A.80.E5.B7.A7)
    *   [4.1 使用 NetworkManager](#.E4.BD.BF.E7.94.A8_NetworkManager)
    *   [4.2 自定义 systemd 服务(使用 wpa_supplicant 和静态 IP)](#.E8.87.AA.E5.AE.9A.E4.B9.89_systemd_.E6.9C.8D.E5.8A.A1.28.E4.BD.BF.E7.94.A8_wpa_supplicant_.E5.92.8C.E9.9D.99.E6.80.81_IP.29)
*   [5 See also](#See_also)

## 要求

所有要连接到网络的设备都具有兼容 [[1]](https://wireless.wiki.kernel.org/en/users/drivers%7Cnl80211) 的无线网卡。

## Wifi 链路层

因为 IBSS 网络是点对点网络，所有设备都应该使用相同的 wifi 连接设置。

**Tip:** 可以设置更复杂的网络拓扑，[Linux 无线文档](http://wireless.kernel.org/en/users/Documentation/iw/vif) 包含更高级的示例。

### 手动设置

**警告:** 此方法创建的是 **非加密** 自组网络，要创建加密网络，请参考 [#WPA supplicant](#WPA_supplicant).

详细信息请参考 [Wireless network configuration#Manual setup](/index.php/Wireless_network_configuration#Manual_setup "Wireless network configuration")。请先[安装](/index.php/Pacman "Pacman") 软件包 [iw](https://www.archlinux.org/packages/?name=iw)。

设置操作模式为 ibss:

```
# iw *interface* set type ibss

```

启动接口(可能需要额外的 `rfkill unblock wifi`):

```
# ip link set *interface* up

```

现在可以创建自组网络了，将 *your_ssid* 替换为实际的网络，*frequency* 替换为以 MHz 为单位的频率。频道和频率的对应关系，请参考, [这里](https://en.wikipedia.org/wiki/List_of_WLAN_channels#Interference_Concerns "wikipedia:List of WLAN channels") 。

```
# iw *interface* ibss join *your_ssid* *frequency*

```

### WPA supplicant

确保已经 [安装](/index.php/Pacman "Pacman") 了 [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant)，并进行了配置(参考 [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant")).

 `/etc/wpa_supplicant-adhoc.conf` 
```
ctrl_interface=DIR=/run/wpa_supplicant GROUP=wheel

# use 'ap_scan=2' on all devices connected to the network
# this is unnecessary if you only want the network to be created when no other networks are available
ap_scan=2

network={
    ssid="MySSID"
    mode=1
    frequency=2432
    proto=RSN
    key_mgmt=WPA-PSK
    pairwise=CCMP
    group=CCMP
    psk="secret passphrase"
}

```

所有连接到网络的设备运行下面 *wpa_supplicant* 命令:

```
# wpa_supplicant -B -i *interface* -c /etc/wpa_supplicant-adhoc.conf -D nl80211,wext

```

## 网络配置

最后一步是给网络中的所有设备分配 IP 地址，有多种方法：

*   分配静态 IP 地址，参考：[Network configuration#Static IP address](/index.php/Network_configuration#Static_IP_address "Network configuration").
*   在一个设备上运行 DHCP，参考 [dhcpd](/index.php/Dhcpd "Dhcpd") 或 [dnsmasq](/index.php/Dnsmasq "Dnsmasq").
*   运行 *avahi-autoipd*. 参考 [Avahi#Obtaining IPv4LL IP address](/index.php/Avahi#Obtaining_IPv4LL_IP_address "Avahi").

要向自组网络共享外网连接，请参考 [Internet sharing](/index.php/Internet_sharing "Internet sharing").

## 技巧

### 使用 NetworkManager

如果使用 [NetworkManager](/index.php/NetworkManager "NetworkManager")，可以使用 *nm-applet* 进行自组网络配置，不用使用手动方法。详情参考 [NetworkManager#Ad-hoc](/index.php/NetworkManager#Ad-hoc "NetworkManager")。

**Note:** NetworkManager 在自组网络模式中不支持 WPA 加密。

### 自定义 systemd 服务(使用 wpa_supplicant 和静态 IP)

可以使用下面模板启用无线自组网络：

 `/etc/conf.d/network-wireless-adhoc@<interface>` 
```
addr=192.168.0.2
mask=24

```
 `/etc/systemd/system/network-wireless-adhoc@.service` 
```
[Unit]
Description=Ad-hoc wireless network connectivity (%i)
Wants=network.target
Before=network.target
BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

[Service]
Type=oneshot
RemainAfterExit=yes
EnvironmentFile=/etc/conf.d/network-wireless-adhoc@%i

# perhaps rfkill is not needed for you
ExecStart=/usr/bin/rfkill unblock wifi
ExecStart=/usr/bin/ip link set %i up
ExecStart=/usr/bin/wpa_supplicant -B -i %i -D nl80211,wext -c /etc/wpa_supplicant-adhoc.conf
ExecStart=/usr/bin/ip addr add ${addr}/${mask} dev %i

ExecStop=/usr/bin/ip addr flush dev %i
ExecStop=/usr/bin/ip link set %i down

[Install]
WantedBy=multi-user.target

```

## See also

*   [Ubuntu community wiki WifiDocs/Adhoc](https://help.ubuntu.com/community/WifiDocs/Adhoc)
*   [Manual about creating an Ad-Hoc network on UbuntuGeek](http://www.ubuntugeek.com/creating-an-adhoc-host-with-ubuntu.html)
*   [Share your 3G Internet connection over wifi](http://go2linux.garron.me/linux/2011/03/share-your-3g-internet-connection-over-wifi-linux-ipod-touch-925)