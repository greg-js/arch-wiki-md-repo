**翻译状态：** 本文是英文页面 [NetworkManager](/index.php/NetworkManager "NetworkManager") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-02-17，点击[这里](https://wiki.archlinux.org/index.php?title=NetworkManager&diff=0&oldid=361369)可以查看翻译后英文页面的改动。

[网络管理器](http://projects.gnome.org/NetworkManager/)(NetworManager)是检测网络、自动连接网络的程序。无论是无线还是有线连接，它都可以令您轻松管理。对于无线网络,网络管理器优先连接已知的网络并可以自动切换到最可靠的无线网络。利用网络管理器的程序可以自由切换在线和离线模式。网络管理器会相对无线网络优先选择有线网络，支持 VPN。网络管理器最初由 Redhat 公司开发，现在由 [GNOME](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)") 管理。

**警告:** 请注意, Wi-Fi 的密码默认情况下是明文保存的。参见 [#加密的Wi-Fi密码](#.E5.8A.A0.E5.AF.86.E7.9A.84Wi-Fi.E5.AF.86.E7.A0.81)

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 VPN 支持](#VPN_.E6.94.AF.E6.8C.81)
    *   [1.2 PPPoE / DSL 支持](#PPPoE_.2F_DSL_.E6.94.AF.E6.8C.81)
*   [2 前端](#.E5.89.8D.E7.AB.AF)
    *   [2.1 Gnome环境](#Gnome.E7.8E.AF.E5.A2.83)
    *   [2.2 KDE Plasma](#KDE_Plasma)
    *   [2.3 KDE 4](#KDE_4)
    *   [2.4 XFCE](#XFCE)
    *   [2.5 Openbox](#Openbox)
    *   [2.6 其它桌面和窗口管理器](#.E5.85.B6.E5.AE.83.E6.A1.8C.E9.9D.A2.E5.92.8C.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [2.7 命令行](#.E5.91.BD.E4.BB.A4.E8.A1.8C)
        *   [2.7.1 nmcli](#nmcli)
        *   [2.7.2 nmtui](#nmtui)
        *   [2.7.3 nmcli-dmenu](#nmcli-dmenu)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 启用 NetworkManager](#.E5.90.AF.E7.94.A8_NetworkManager)
    *   [3.2 设置 PolicyKit 权限](#.E8.AE.BE.E7.BD.AE_PolicyKit_.E6.9D.83.E9.99.90)
    *   [3.3 使用 NetworkManager 调度网络服务](#.E4.BD.BF.E7.94.A8_NetworkManager_.E8.B0.83.E5.BA.A6.E7.BD.91.E7.BB.9C.E6.9C.8D.E5.8A.A1)
        *   [3.3.1 避免超时](#.E9.81.BF.E5.85.8D.E8.B6.85.E6.97.B6)
        *   [3.3.2 启动 OpenNTPD](#.E5.90.AF.E5.8A.A8_OpenNTPD)
        *   [3.3.3 使用sshfs挂载远程文件夹](#.E4.BD.BF.E7.94.A8sshfs.E6.8C.82.E8.BD.BD.E8.BF.9C.E7.A8.8B.E6.96.87.E4.BB.B6.E5.A4.B9)
        *   [3.3.4 使用 dispatcher 在网络连接建立后连接 vpn](#.E4.BD.BF.E7.94.A8_dispatcher_.E5.9C.A8.E7.BD.91.E7.BB.9C.E8.BF.9E.E6.8E.A5.E5.BB.BA.E7.AB.8B.E5.90.8E.E8.BF.9E.E6.8E.A5_vpn)
    *   [3.4 代理设置](#.E4.BB.A3.E7.90.86.E8.AE.BE.E7.BD.AE)
    *   [3.5 禁用 NetworkManager](#.E7.A6.81.E7.94.A8_NetworkManager)
*   [4 测试](#.E6.B5.8B.E8.AF.95)
*   [5 常见问题](#.E5.B8.B8.E8.A7.81.E9.97.AE.E9.A2.98)
    *   [5.1 安全Wi-Fi网络不提示输入密码](#.E5.AE.89.E5.85.A8Wi-Fi.E7.BD.91.E7.BB.9C.E4.B8.8D.E6.8F.90.E7.A4.BA.E8.BE.93.E5.85.A5.E5.AF.86.E7.A0.81)
    *   [5.2 PPTP 通道中无流量](#PPTP_.E9.80.9A.E9.81.93.E4.B8.AD.E6.97.A0.E6.B5.81.E9.87.8F)
    *   [5.3 网络管理功能失效](#.E7.BD.91.E7.BB.9C.E7.AE.A1.E7.90.86.E5.8A.9F.E8.83.BD.E5.A4.B1.E6.95.88)
    *   [5.4 定制resolv.conf](#.E5.AE.9A.E5.88.B6resolv.conf)
    *   [5.5 使用 resolv.conf.head 和 resolv.conf.tail](#.E4.BD.BF.E7.94.A8_resolv.conf.head_.E5.92.8C_resolv.conf.tail)
    *   [5.6 在resolv.conf中保留改动](#.E5.9C.A8resolv.conf.E4.B8.AD.E4.BF.9D.E7.95.99.E6.94.B9.E5.8A.A8)
    *   [5.7 使用dhclient时的DHCP问题](#.E4.BD.BF.E7.94.A8dhclient.E6.97.B6.E7.9A.84DHCP.E9.97.AE.E9.A2.98)
    *   [5.8 主机名问题](#.E4.B8.BB.E6.9C.BA.E5.90.8D.E9.97.AE.E9.A2.98)
    *   [5.9 配置dhclient把主机名推送到DHCP服务器](#.E9.85.8D.E7.BD.AEdhclient.E6.8A.8A.E4.B8.BB.E6.9C.BA.E5.90.8D.E6.8E.A8.E9.80.81.E5.88.B0DHCP.E6.9C.8D.E5.8A.A1.E5.99.A8)
    *   [5.10 配置NetworkManager使用一个特性的DHCP客户端](#.E9.85.8D.E7.BD.AENetworkManager.E4.BD.BF.E7.94.A8.E4.B8.80.E4.B8.AA.E7.89.B9.E6.80.A7.E7.9A.84DHCP.E5.AE.A2.E6.88.B7.E7.AB.AF)
    *   [5.11 缺少默认路由 route](#.E7.BC.BA.E5.B0.91.E9.BB.98.E8.AE.A4.E8.B7.AF.E7.94.B1_route)
    *   [5.12 没有探测到 3G 模块](#.E6.B2.A1.E6.9C.89.E6.8E.A2.E6.B5.8B.E5.88.B0_3G_.E6.A8.A1.E5.9D.97)
    *   [5.13 在笔记本上关闭WLAN](#.E5.9C.A8.E7.AC.94.E8.AE.B0.E6.9C.AC.E4.B8.8A.E5.85.B3.E9.97.ADWLAN)
    *   [5.14 静态 IP 设置 变成 DHCP](#.E9.9D.99.E6.80.81_IP_.E8.AE.BE.E7.BD.AE_.E5.8F.98.E6.88.90_DHCP)
    *   [5.15 普通用户无法编辑链接](#.E6.99.AE.E9.80.9A.E7.94.A8.E6.88.B7.E6.97.A0.E6.B3.95.E7.BC.96.E8.BE.91.E9.93.BE.E6.8E.A5)
    *   [5.16 删除隐蔽无线网络链接](#.E5.88.A0.E9.99.A4.E9.9A.90.E8.94.BD.E6.97.A0.E7.BA.BF.E7.BD.91.E7.BB.9C.E9.93.BE.E6.8E.A5)
    *   [5.17 GNOME VPN失效问题](#GNOME_VPN.E5.A4.B1.E6.95.88.E9.97.AE.E9.A2.98)
    *   [5.18 Unable to connect to visible European wireless networks](#Unable_to_connect_to_visible_European_wireless_networks)
    *   [5.19 引导时自动连接到VPN不工作](#.E5.BC.95.E5.AF.BC.E6.97.B6.E8.87.AA.E5.8A.A8.E8.BF.9E.E6.8E.A5.E5.88.B0VPN.E4.B8.8D.E5.B7.A5.E4.BD.9C)
    *   [5.20 dhcpd不断地拒绝租约](#dhcpd.E4.B8.8D.E6.96.AD.E5.9C.B0.E6.8B.92.E7.BB.9D.E7.A7.9F.E7.BA.A6)
    *   [5.21 Systemd瓶颈](#Systemd.E7.93.B6.E9.A2.88)
    *   [5.22 网络(WiFi)经常有规律地断开](#.E7.BD.91.E7.BB.9C.28WiFi.29.E7.BB.8F.E5.B8.B8.E6.9C.89.E8.A7.84.E5.BE.8B.E5.9C.B0.E6.96.AD.E5.BC.80)
*   [6 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [6.1 加密的Wi-Fi密码](#.E5.8A.A0.E5.AF.86.E7.9A.84Wi-Fi.E5.AF.86.E7.A0.81)
    *   [6.2 通过Wi-Fi共享网络连接](#.E9.80.9A.E8.BF.87Wi-Fi.E5.85.B1.E4.BA.AB.E7.BD.91.E7.BB.9C.E8.BF.9E.E6.8E.A5)
        *   [6.2.1 Ad-hoc](#Ad-hoc)
        *   [6.2.2 Real AP](#Real_AP)
    *   [6.3 通过Ethernet共享连接](#.E9.80.9A.E8.BF.87Ethernet.E5.85.B1.E4.BA.AB.E8.BF.9E.E6.8E.A5)
    *   [6.4 在cron任务（jobs）或脚本中检查网络是否连接](#.E5.9C.A8cron.E4.BB.BB.E5.8A.A1.EF.BC.88jobs.EF.BC.89.E6.88.96.E8.84.9A.E6.9C.AC.E4.B8.AD.E6.A3.80.E6.9F.A5.E7.BD.91.E7.BB.9C.E6.98.AF.E5.90.A6.E8.BF.9E.E6.8E.A5)
    *   [6.5 登陆后自动解锁秘钥环](#.E7.99.BB.E9.99.86.E5.90.8E.E8.87.AA.E5.8A.A8.E8.A7.A3.E9.94.81.E7.A7.98.E9.92.A5.E7.8E.AF)
        *   [6.5.1 GNOME](#GNOME)
        *   [6.5.2 SLiM 登录管理器](#SLiM_.E7.99.BB.E5.BD.95.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [6.6 有密码认证的KDE and OpenConnect VPN](#.E6.9C.89.E5.AF.86.E7.A0.81.E8.AE.A4.E8.AF.81.E7.9A.84KDE_and_OpenConnect_VPN)
    *   [6.7 忽略特定设备](#.E5.BF.BD.E7.95.A5.E7.89.B9.E5.AE.9A.E8.AE.BE.E5.A4.87)
    *   [6.8 启用DNS缓存](#.E5.90.AF.E7.94.A8DNS.E7.BC.93.E5.AD.98)
    *   [6.9 启用IPv6隐私扩展](#.E5.90.AF.E7.94.A8IPv6.E9.9A.90.E7.A7.81.E6.89.A9.E5.B1.95)
*   [7 其它资源](#.E5.85.B6.E5.AE.83.E8.B5.84.E6.BA.90)

## 安装

网络管理其可以通过[networkmanager](https://www.archlinux.org/packages/?name=networkmanager)包[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")。这个包不包括托盘插件*nm-applet*,此插件是[network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet)包的一部分。从1.0版本开始，网络管理内部获得了对基本DHCP功能的支持。对于全功能的DHCP或者如果你需要IPV6支持，[dhclient](https://www.archlinux.org/packages/?name=dhclient) 集成了这些功能。

```
# pacman -Syu networkmanager

```

**Note:** 你必须确保没有其他想要配置网络相关的服务正在运行; 事实上, 多个网络配置服务之间会相互冲突。如果想知道当前有哪些服务正在运行, 可以运行 `systemctl --type=service` 然后 [停止](/index.php/Systemd#Using_units "Systemd") 多余的网络配置服务。参见 [#配置](#.E9.85.8D.E7.BD.AE) 来激活 NetworkManager 服务。

### VPN 支持

NetworkManager 的 VPN 支持基于一个插件系统。如果需要通过 NetworkManager 来使用 VPN, 请安装以下任一软件包:

*   [networkmanager-openconnect](https://www.archlinux.org/packages/?name=networkmanager-openconnect)
*   [networkmanager-openvpn](https://www.archlinux.org/packages/?name=networkmanager-openvpn)
*   [networkmanager-pptp](https://www.archlinux.org/packages/?name=networkmanager-pptp)
*   [networkmanager-vpnc](https://www.archlinux.org/packages/?name=networkmanager-vpnc)

通过 [AUR](/index.php/AUR "AUR"):

*   [networkmanager-l2tp](https://aur.archlinux.org/packages/networkmanager-l2tp/)
*   [networkmanager-strongswan](https://www.archlinux.org/packages/?name=networkmanager-strongswan)

**警告:** VPN支持[不稳定](https://bugzilla.gnome.org/buglist.cgi?quicksearch=networkmanager%20vpn)，检查守护进程正确处理了通过GUI设置的选项，并对每一个发行包二次检查。[[1]](https://bugzilla.gnome.org/show_bug.cgi?id=755350)

### PPPoE / DSL 支持

安装 [rp-pppoe](https://www.archlinux.org/packages/?name=rp-pppoe) 来获得 PPPoE / DSL 连接支持。

## 前端

为了配置和轻松使用网络管理器，大多数用户会希望安装一个托盘组件。图形前端往往显示在系统托盘（或通知区域），从而允许用户选择网络或者配置 NetworkManager。不同类型的桌面环境下有多种托盘插件。

### Gnome环境

Gnome的[network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet)几乎可以运行在所有的桌面环境下。

如果你想储存验证信息(Wireless/DSL), 安装和配置[GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring")

注意，对一个连接激活了`Make available to other users`勾选框后，NetworkManager用明文存储密码，但是相应的文件只能被root（或者其他用户通过`nm-applet`)）访问。参见[#Encrypted Wi-Fi passwords](#Encrypted_Wi-Fi_passwords)。

### KDE Plasma

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") the [plasma-nm](https://www.archlinux.org/packages/?name=plasma-nm) applet.

### KDE 4

Plasma-nm 前端可以通过官方软件仓库中的 [kdeplasma-applets-plasma-nm](https://www.archlinux.org/packages/?name=kdeplasma-applets-plasma-nm) 安装。老的 KNetworkManager 前端已经移到了[AUR](/index.php/AUR "AUR") 软件包 [kdeplasma-applets-networkmanagement](https://aur.archlinux.org/packages/kdeplasma-applets-networkmanagement/) 。

如果同时安装了 KNetworkManager 和 nm-applet，在使用 KDE 时不想使用 nm-applet，将下行加入 `/etc/xdg/autostart/nm-applet.desktop`

```
NotShowIn=KDE

```

详情参阅 [Userbase 页面](http://userbase.kde.org/NetworkManagement)。

### XFCE

虽然[network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet)在[Xfce](/index.php/Xfce "Xfce")下正常工作，但是为了可以看到通知信息，包括错误信息， `nm-applet`需要一个 Freedesktop 桌面通知说明（参见 [Galapago Project](http://www.galago-project.org/specs/notification/0.9/index.html)）来显示他们。要激活通知，请安装[xfce4-notifyd](https://www.archlinux.org/packages/?name=xfce4-notifyd), 此包提供了上述说明的一个实现。

如果没有这个通知守护进程，`nm-applet`就会输出下面的错误到 stdout/stderr：

```
(nm-applet:24209): libnotify-WARNING **: Failed to connect to proxy
** (nm-applet:24209): WARNING **: get_all_cb: couldn't retrieve
system settings properties: (25) Launch helper exited with unknown
return code 1.
** (nm-applet:24209): WARNING **: fetch_connections_done: error
fetching connections: (25) Launch helper exited with unknown return
code 1.
** (nm-applet:24209): WARNING **: Failed to register as an agent:
(25) Launch helper exited with unknown return code 1

```

`nm-applet` 还会工作得不错, 不过，没有通知消息。

如果 `nm-applet` 在连接到 WiFi 时没有提示输入密码, 仅仅立即断开连接, 你可能需要安装 [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring)。

如果托盘插件没有显示，安装[xfce4-indicator-plugin](https://aur.archlinux.org/packages/xfce4-indicator-plugin/)包。[[2]](http://askubuntu.com/questions/449658/networkmanager-tray-nm-applet-is-gone-after-upgrade-to-14-04-trusty)

### Openbox

为了能在[Openbox](/index.php/Openbox "Openbox")中优雅地工作，Gnome小程序，因为和XFCE同样的原因，需要[xfce4-notifyd](https://www.archlinux.org/packages/?name=xfce4-notifyd)通知进程和[gnome-icon-theme](https://www.archlinux.org/packages/?name=gnome-icon-theme)来在系统托盘中显示小程序。 GNOME applet 和 xfce4-notifyd 结合可以很好的工作:

如果你想储存身份验证信息(Wireless/DSL)，请安装和配置[gnome-keyring](/index.php/Gnome-keyring "Gnome-keyring")：

`nm-applet`在`/etc/xdg/autostart/nm-applet.desktop`中安装自动启动文件. 如果你遇到问题（比如，`nm-applet`启动了两次或者根本没有启动), 参考[Openbox#autostart](/index.php/Openbox#autostart "Openbox") 或者[[3]](https://bbs.archlinux.org/viewtopic.php?pid=993738)来解决.

### 其它桌面和窗口管理器

所有其他场景下，推荐使用 GNOME 组件。你也需要确保需要[gnome-icon-theme](https://www.archlinux.org/packages/?name=gnome-icon-theme)被正确安装并可以显示小程序。安装 GNOME hicolor 主题：

要存储连接密码，请安装和配置[GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring")。

想要不使用系统托盘来运行`nm-applet`，可以使用 [trayer](https://www.archlinux.org/packages/?name=trayer) 或 [stalonetray](https://www.archlinux.org/packages/?name=stalonetray)。例如，你的PATH中加入像这样的一个脚本：

 `nmgui` 
```
#!/bin/sh
nm-applet    2>&1 > /dev/null &
stalonetray  2>&1 > /dev/null
killall nm-applet

```

当你关闭 *stalonetray* 窗口时，也将会同时关闭 `nm-applet`，所以完成网络设置后不会使用额外的内存。

### 命令行

下列应用程序可能对于没有X时配置和管理网络有帮助。

#### nmcli

命令行前端*nmcli*包括在[networkmanager](https://www.archlinux.org/packages/?name=networkmanager)中。

对于使用信息，参考`man nmcli`。 例子:

*   连接 WiFi 网络: `nmcli dev wifi connect <name> password <password>` 
*   通过`wlan1`接口连接 WiFi 网络: `nmcli dev wifi connect <name> password <password> iface wlan1 [profile name]` 
*   断开一个接口: `nmcli dev disconnect iface eth0` 
*   重新连接一个标记为已断开的接口: `nmcli con up uuid <uuid>` 
*   获得 UUID 列表: `nmcli con show` 
*   查看网络设备及其状态列表: `nmcli dev` 
*   关闭 WiFi: `nmcli r wifi off` 

#### nmtui

"nmtui" 是一个基于curses的图形化前端，包括在[networkmanager](https://www.archlinux.org/packages/?name=networkmanager)中。

使用信息参见`man nmtui`。

#### nmcli-dmenu

[networkmanager-dmenu-git](https://aur.archlinux.org/packages/networkmanager-dmenu-git/) 是一个通过 *dmenu* 而不是 `nm-applet` 来管理 NetworkManager 连接的脚本。它提供了所有必要的特性, 例如连接到已有的 WiFi 或有线网络, 连接到新的 WiFi 网络, 在需要的时候询问密码, 连接到已有的 VPN, 启用/停用网络连接, 运行 *nm-connection-editor* 的图形界面。

## 配置

NetworkManager 需要做这么几步保证正常运行。确保你`/etc/hosts`按照[Network configuration#Set the hostname](/index.php/Network_configuration#Set_the_hostname "Network configuration")一节的描述配置了`/etc/hosts`。

### 启用 NetworkManager

NetworkManager通过`NetworkManager.service`[控制](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BD.BF.E7.94.A8.E5.8D.95.E5.85.83 "Systemd (简体中文)")。 NetworkManager 守护进程启动后，会自动连接到任何可用的已经配置的**系统连接**。**用户连接**或未配置的连接需要通过`nmcli`或桌面工具进行配置和连接。

开机启用 NetworkManager：

```
# systemctl enable NetworkManager

```

立即启动 NetworkManager：

```
# systemctl start NetworkManager

```

NetworkManager在`/etc/NetworkManager/NetworkManager.conf`有一个全局的配置文件。通常全局的默认配置不需要改动。

**Note:** 当[NetworkManager-dispatcher.service](#Network_services_with_NetworkManager_dispatcher)和[ModemManager.service](https://www.archlinux.org/packages/?name=modemmanager)没有被激活时，NetworkManager会向你的系统日至打印无意义的警告([FS#34971](https://bugs.archlinux.org/task/34971))，你可能需要将两者激活来抑制这些消息。

### 设置 PolicyKit 权限

参照[General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting")建立一个工作会话. 在工作会话中,你有三种方式授予NetworkManager工作所必须的权限.

*方式 1.* 登录后运行[PolicyKit](/index.php/PolicyKit "PolicyKit")认证代理,比如 `/usr/lib/polkit-gnome/polkit-gnome-authentication-agent-1` ([polkit-gnome](https://www.archlinux.org/packages/?name=polkit-gnome) 的一部分). 当你添加和删除一个网络链接时会提示输入密码.

*方式 2.* 将你的账户加入`wheel`账户组. 管理网络时你将不需要输入密码,但注意你的账户同时被赋予了此账户组的其他权限,比如运行[sudo](/index.php/Sudo "Sudo")命令是无需密码.

*方式 3.* 将你的账户加入`network`账户组,同时创建以下文件:

 `/etc/polkit-1/rules.d/50-org.freedesktop.NetworkManager.rules` 
```
polkit.addRule(function(action, subject) {
  if (action.id.indexOf("org.freedesktop.NetworkManager.") == 0 && subject.isInGroup("network")) {
    return polkit.Result.YES;
  }
});

```

所有在`network`账户群中的用户都能免密码管理网络. 但是如果你没有在 [systemd-logind](/index.php/Systemd#Using_systemd-logind "Systemd") 中拥有一个活跃会话的话, 在systemd下此方式将失效.

### 使用 NetworkManager 调度网络服务

有些服务只有联网时才有意义，例如 [OpenNTPD](/index.php/OpenNTPD "OpenNTPD") 和 网络文件系统挂载(**netfs**)。dispatcher 可以在连接网络后启动这些服务，并在网络关闭时停止它们。要使用这一功能, 需要启动 `NetworkManager-dispatcher.service`。 并且将脚本加到 `/etc/NetworkManager/dispatcher.d` 目录。这些脚本必须属于 root, 否则不会被执行。为了安全起见, 用户组也设置为 root:

```
# chown root:root *scriptname*

```

而且脚本必须只能是拥有者可写, 否则不会被执行:

```
# chmod 755 *scriptname*

```

脚本将在连接网络时按字母表顺序运行，并在网络停止时反向停止。要保证启动顺序，可以在前面加数字，例如 `10_portmap` 或 `30_netfs` 这样就能保证 portmapper 在 NFS 挂载之前启动。

**警告:** 如果没有连接到外部网络，请注意启动的服务和需要它们的程序。如果连接公共网络时启动了错误的服务，可能导致安全问题。

#### 避免超时

如果一切运行良好, 那么这一节就可以跳过了。 However, there is a general problem related to running dispatcher scripts which take longer to be executed. Initially an internal timeout of three seconds only was used. If the called script did not complete in time, it was killed. Later the timeout was extended to about 20 seconds (see the [Bugtracker](https://bugzilla.redhat.com/show_bug.cgi?id=982734) for more information). If the timeout still creates the problem, a work around may be to modify the dispatcher service file `/usr/lib/systemd/system/NetworkManager-dispatcher.service` to remain active after exit:

 `/etc/systemd/system/NetworkManager-dispatcher.service` 
```
.include /usr/lib/systemd/system/NetworkManager-dispatcher.service
[Service]
RemainAfterExit=yes
```

运行修改后的 `NetworkManager-dispatcher` 服务并将其设置为开机启动。

**警告:** 加入了 `RemainAfterExit` 那一行后会让 dispatcher 一直运行。不幸的是, dispatcher **必须**在再次运行脚本前被关闭。这意味着脚本只能被运行一次。因此, 除非超时确实引起了问题, 否则不要修改服务文件。

#### 启动 OpenNTPD

安装 [networkmanager-dispatcher-openntpd](https://www.archlinux.org/packages/?name=networkmanager-dispatcher-openntpd) 软件包

#### 使用sshfs挂载远程文件夹

由于该脚本在一个非常受限制的环境中运行, 为了连接上SSH agent, 你必须 export `SSH_AUTH_SOCK`。 这里有几种不同方式, 参照 [here](https://bbs.archlinux.org/viewtopic.php?pid=1042030#p1042030) 获取更多详细信息. 以下示例需要 gnome-keyring , 如果 gnome-keyring 没解锁,将需要你输入密码. 如果 NetworkManager 设置为登录后自动连接, 很有可能因为 *gnome-keyring* 还没启动导致失败(转入睡眠). 对应的 UUID 可以通过命令 `nmcli con status` 或 `nmcli con list` 查得。

```
#!/bin/sh
USER='username'
REMOTE='user@host:/remote/path'
LOCAL='/local/path'

interface=$1 status=$2
if [ "$CONNECTION_UUID" = "*uuid*" ]; then
  case $status in
    up)
      export SSH_AUTH_SOCK=$(find /tmp -maxdepth 1 -type s -user "$USER" -name 'ssh')
      su "$USER" -c "sshfs $REMOTE $LOCAL"
      ;;
    down)
      fusermount -u "$LOCAL"
      ;;
  esac
fi

```

#### 使用 dispatcher 在网络连接建立后连接 vpn

此部分示例演示如果自动连接到NetworkManager已定义的vpn-connection.首先创建调度脚本定义vpn连接之后的事务

	1\. 创建调度脚本

 `/etc/NetworkManager/dispatcher.d/vpn-up` 
```
#!/bin/sh
VPN_NAME="name of VPN connection defined in NetworkManager"
ESSID="Wi-Fi network ESSID (not connection name)"

interface=$1 status=$2
case $status in
  up|vpn-down)
    if iwgetid | grep -qs ":\"$ESSID\""; then
      nmcli con up id "$VPN_NAME"
    fi
    ;;
  down)
    if iwgetid | grep -qs ":\"$ESSID\""; then
      if nmcli con status id "$VPN_NAME" | grep -qs activated; then
        nmcli con down id "$VPN_NAME"
      fi
    fi
    ;;
esac

```

如果想在任意 Wi-Fi 网络都可以自动连接 VPN, 你可以用这样给 ESSID 赋值: `ESSID=$(iwgetid -r)`。记住要给脚本设置相应的权限, 参见 [上文](#.E7.BD.91.E7.BB.9C.E5.88.86.E9.85.8D.E5.99.A8)。

如果想任意用户都能使用 VPN, 即使已经在 `nm-applet` 中勾选了 *Make the VPN connection available to all users* 选项, 由于 [VPN secrets 保管方式的原因](http://developer.gnome.org/NetworkManager/0.9/secrets-flags.html), 连接依然可能会失败并且 NetworkManager 会报错 'no valid VPN secrets'。这样就需要执行步骤2:

	2\. 可以选择编辑 VPN 连接的配置文件让 NetworkManager 自己储存 secrets 而不是把 secrets 保存在 [不能被root访问的](https://bugzilla.redhat.com/show_bug.cgi?id=710552) keyring 中: 打开 `/etc/NetworkManager/system-connections/*name of your VPN connection*`, 把 `password-flags` 以及 `secret-flags` 从 `1` 改为 `0`。

或者直接在 VPN 配置文件中加入 `vpn-secrets` 并写入密码:

```
 [vpn]
 ....
 password-flags=0

 [vpn-secrets]
 password=*your_password*

```

**注意:** 现在可能有必要重新打开 NetworkManager connection editor 并再次保存 VPN passwords/secrets。

### 代理设置

NetworkManager不直接处理代理设置，但是如果你使用[GNOME](/index.php/GNOME "GNOME")，你可以使用 [proxydriver](http://marin.jb.free.fr/proxydriver/)配合NetworkManager。 [proxydriver](https://aur.archlinux.org/packages/proxydriver/)软件包位于 [AUR](/index.php/AUR "AUR").

为使proxydriver设置代理，你需要在设置GNOME自动启动进程( System->Preferences->Startup Applications):

```
xhost +si:localuser:your_username

```

参照: [Proxy settings](/index.php/Proxy_settings "Proxy settings")

### 禁用 NetworkManager

由于服务是通过 *dbus* 自动启动的, 所以要完全禁用可以用 *systemctl* 来屏蔽:

```
systemctl mask NetworkManager
systemctl mask NetworkManager-dispatcher

```

## 测试

NetworkManager 托盘组件被设计成开机自动启动，所以对大部分用户来说，并不需要过多配置。 但是如果你手动停用旧有的网络设置断网，你需要测试一下 NetworkManager 是否正常工作。 首先启动服务：

```
systemctl start NetworkManager

```

有些托盘组件会提供给你一个 .desktop 文件以便通过系统菜单运行。 如果没有，那你就需要通过命令或者注销重登录系统来让托盘组件运行。 一旦托盘组件运行了，它会自动请求网络连接并通过 DHCP 服务器来进行网络配置。

在一些 non-xdg-compliant 窗口系统，比如 Awesome 中启动 GNOME applet：

```
nm-applet --sm-disable &

```

如果需要静态 IP，你需要配置 NetworkManager。一般来说，在托盘图标上面点击右键， 选择「编辑连接」即可。

## 常见问题

常见问题的一些解决办法。

### 安全Wi-Fi网络不提示输入密码

当连接到一个安全的WI-Fi网络时，没有输入密码的提示，而且没有连接建立。当没有秘钥环(keyring)包安装时，会发生这种情况。一个简单的解决办法是安装[gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring)。如果你希望密码以加密的形式存储，按照[GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring")来设置*gnome-keyring-daemon*。

### PPTP 通道中无流量

PPTP连接成功登录，可以看到一个有正确VPN IP的ppp0接口，但是甚至不能ping通远端IP。这是由于Arch提供的pppd缺少MPPE (Microsoft Point-to-Point Encryption) 支持。 推荐首先尝试Arch提供的[ppp](https://www.archlinux.org/packages/?name=ppp)，因为它可能会按照希望的样子工作。

要解决这个问题，安装[ppp-mppe](https://aur.archlinux.org/packages/ppp-mppe/)包应该足够了。

参见[WPA2 Enterprise#MS-CHAPv2](/index.php/WPA2_Enterprise#MS-CHAPv2 "WPA2 Enterprise")。

### 网络管理功能失效

有时NetworkManager关闭了，但对应的pid文件却没有移除，同时你得到提示 'Network management disabled'. 你可以手工处理:

```
# rm /var/lib/NetworkManager/NetworkManager.state

```

### 定制resolv.conf

参见主页面[resolv.conf](/index.php/Resolv.conf "Resolv.conf")。如果你使用[dhclient](https://www.archlinux.org/packages/?name=dhclient)，你可以尝试[networkmanager-dispatch-resolv](https://aur.archlinux.org/packages/networkmanager-dispatch-resolv/)包。

### 使用 resolv.conf.head 和 resolv.conf.tail

请阅读 [resolv.conf](/index.php/Resolv.conf "Resolv.conf") 并确保 NetworkManager 使用的是 [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) 而不是 [dhclient](https://www.archlinux.org/packages/?name=dhclient)。如果要使用 [dhclient](https://www.archlinux.org/packages/?name=dhclient)，可以试试[AUR](/index.php/AUR "AUR")里面的 [networkmanager-dispatch-resolv](https://aur.archlinux.org/packages/networkmanager-dispatch-resolv/)。

### 在resolv.conf中保留改动

NetworkManager试图将DHCP中获取的DNS信息写入`/etc/resolv.conf`,导致原文件被覆盖,你可以在文件属性中设置i参数避免文件被修改

```
# chattr +i /etc/resolv.conf

```

如果你要修改此文件,移除i参数:

```
# chattr -i /etc/resolv.conf

```

### 使用dhclient时的DHCP问题

如果你无法通过DHCP获取IP,尝试在`/etc/dhclient.conf`添加如下配置:

```
 interface "eth0" {
   send dhcp-client-identifier 01:aa:bb:cc:dd:ee:ff;
 }

```

其中`aa:bb:cc:dd:ee:ff` 是你网卡的MAC地址. MAC地址可以使用[iproute2](https://www.archlinux.org/packages/?name=iproute2) 包中的 `ip link show eth0` 命令获得。

### 主机名问题

主机名是否被转发到所链接的路由器取决与你所使用的NetworkManager插件。通用的“密钥文件”插件默认不转发主机名。为了使之转发主机名，添加下面的内容到`/etc/NetworkManager/NetworkManager.conf`：

```
[keyfile]
hostname=*your_hostname*

```

`[keyfile]`下的选项会应用到默认`/etc/NetworkManager/system-connections`路径的网络连接。

另一种选择是配置NetworkManager自动启动的DHCP客户端来转发主机名。NetworkManager默认使用[dhclient](https://www.archlinux.org/packages/?name=dhclient)，并且当前者没有安装时使用[dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd)。使*dhclient* 转发主机名需要设置一个非默认选项, *dhcpcd*默认转发主机名.

首先，检查使用的是哪一个DHCP客户端(以*dhclient*为例):

 `# journalctl -b | egrep "dhc"` 
```
...
Nov 17 21:03:20 zenbook dhclient[2949]: Nov 17 21:03:20 zenbook dhclient[2949]: Bound to *:546
Nov 17 21:03:20 zenbook dhclient[2949]: Listening on Socket/wlan0
Nov 17 21:03:20 zenbook dhclient[2949]: Sending on   Socket/wlan0
Nov 17 21:03:20 zenbook dhclient[2949]: XMT: Info-Request on wlan0, interval 1020ms.
Nov 17 21:03:20 zenbook dhclient[2949]: RCV: Reply message on wlan0 from fe80::126f:3fff:fe0c:2dc.

```

### 配置dhclient把主机名推送到DHCP服务器

复制示例配置文件：

```
# cp /usr/share/dhclient/dhclient.conf.example /etc/dhclient.conf

```

看一下这个文件 - 其实我们想保存的只有一行而且*dhclient*会使用其他选项的默认值 (就像你没有这个文件时它使用的那样)。下面是那重要的一行：

 `/etc/dhclient.conf`  `send host-name = pick-first-value(gethostname(), "ISC-dhclient");` 

用你最喜欢的方法强制进行IP地址刷新，然后你应该可以在你的DHCP服务器上看到你的主机名了。

IPv6推送主机名：

```
# cp /usr/share/dhclient/dhclient.conf.example /etc/dhclient6.conf

```
 `/etc/dhclient6.conf`  `send fqdn.fqdn = pick-first-value(gethostname(), "ISC-dhclient");` 

### 配置NetworkManager使用一个特性的DHCP客户端

如果你想显示地设置Networkmanager使用的DHCP客户端，可以在全局配置文件中设置：

 `/etc/NetworkManager/NetworkManager.conf`  `dhcp=internal` 

如果这个选项更没有设置，按照默认使用的是替代的`dhcp=dhclient`。

然后[restart](/index.php/Restart "Restart") `NetworkManager.service`。

**Note:** [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd)的支持已经在[networkmanager](https://www.archlinux.org/packages/?name=networkmanager)-1.0.0-2 (2015-02-14)中 [禁用](https://projects.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/networkmanager&id=a1df79cbcebaec0c043789eb31965e57d17b6cdb) 。

### 缺少默认路由 route

在至少一个KDE4系统中,当使用NetworkManager [Wireless Setup (简体中文)](/index.php/Wireless_Setup_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wireless Setup (简体中文)")链接时不会建立缺省路由。 改变无线链接的路由配置来移除*Use only for resources on this connection"的默认选择能解决这个问题。*

### 没有探测到 3G 模块

如果NetworkManager(从v0.7.999)没有探测到你的3G模块,但是你仍然可以使用[wvdial](/index.php/Wvdial "Wvdial")连接, 可以尝试安装[modemmanager](https://www.archlinux.org/packages/?name=modemmanager),并使用`rc.d restart networkmanager`重启服务,你可能需要重插或重启你的3G模块, 这可以让NetworkManager支持默认数据库中缺失的硬件模块

参考[USB 3G Modem#Network Manager](/index.php/USB_3G_Modem#Network_Manager "USB 3G Modem").

### 在笔记本上关闭WLAN

有时候在你使用笔记本上的开关禁用WI-Fi然后重新启用后，NetworkManager无法工作。这常常是`rfkill`的问题。请安装[rfkill](https://www.archlinux.org/packages/?name=rfkill)并使用 $ watch -n1 rfkill list all 检查驱动`rfkill`是否通知到无线适配器的状态. 如果你开启适配器后,其标识符仍然显示blocked,你可以尝试如下命令手动unblock(X是前一条命令的identifier编号)

```
# rfkill event unblock X

```

### 静态 IP 设置 变成 DHCP

因为一个尚未结局的bug，当改变默认连接为静态IP时，`nm-applet` 可能不能恰当地保存你的IP配置改变，而自动转变为DHCP模式。

要解决这个问题，你不得不在`nm-applet`中改变默认连接名（比如将"Auto eth0"变成“my eth0”）,去掉“Available to all users”的勾号，输入你的配置IP地址，然后点击“Apply”。这样就能按照所给的名字保存新的配置

接下来，你可能不希望默认链接自动连接网络。运行 `nm-connection-editor` (*不要*以root身份)。在链接编辑窗口，编辑默认配置(eg "Auto eth0") 去掉"Connect automatically".， 点击 **Apply**，关掉窗口。

### 普通用户无法编辑链接

参见 [#Set_up_PolicyKit_permissions](#Set_up_PolicyKit_permissions).

### 删除隐蔽无线网络链接

因为隐蔽无线网络不出现在无线列表中，所以不能在GUI中删除，你可以试用以下命令：

```
# rm /etc/NetworkManager/system-connections/[SSID]

```

此命令对任何其他连接有效。

### GNOME VPN失效问题

在[GNOME](/index.php/GNOME "GNOME")系统中用NetworkManager 设立[OpenConnect](/index.php/OpenConnect "OpenConnect")或VPN链接，有时会无法跳出对话框，在/var/log/errors.log中会出现如下错误提示：

```
localhost NetworkManager[399]: <error> [1361719690.10506] [nm-vpn-connection.c:1405] get_secrets_cb(): Failed to request VPN secrets #3: (6) No agents were available for this request.

```

这是由于Gnome NM Applet在/usr/lib/gnome-shell中读取脚本， 而NetworkManager安装包将脚本安装/usr/lib/networkmanager中（这个bug已经存在一段时间了）. 临时解决方法可以文件夹中创建软连接

*   对于OpenConnect: `ln -s /usr/lib/networkmanager/nm-openconnect-auth-dialog /usr/lib/gnome-shell/`
*   对于VPNC (也即 Cisco VPN): `ln -s /usr/lib/networkmanager/nm-vpnc-auth-dialog /usr/lib/gnome-shell/`

对其他类型的NM VPN插件可能也需要做类似的事情，不过上述两种VPN是最常见的。

### Unable to connect to visible European wireless networks

WLAN chips are shipped with a default [regulatory domain](/index.php/Wireless_network_configuration#Respecting_the_regulatory_domain "Wireless network configuration"). If your access point does not operate within these limitations, you will not be able to connect to the network. Fixing this is easy:

1.  [Install](/index.php/Install "Install") [crda](https://www.archlinux.org/packages/?name=crda)
2.  Uncomment the correct Country Code in `/etc/conf.d/wireless-regdom`
3.  Reboot the system, because the setting is only read on boot

### 引导时自动连接到VPN不工作

问题原因在于，当系统(也即以root用户运行的NetworkManager)尝试建立一个VPN连接时无法获取密码，因为密码存储在一个特性用户的Gnome kerying中。

解决的一个办法是用明文存储VPN密码，如[#Use dispatcher to connect to a VPN after a network connection is established](#Use_dispatcher_to_connect_to_a_VPN_after_a_network_connection_is_established)步骤(2.)中所描述。

如果你使用`nm-applet`GUI中的新的"auto-connect VPN"选项，你不再需要使用步骤(1.)所描述的分配器来自动连接。

### dhcpd不断地拒绝租约

有人报告dhcpd不断地拒绝租约，同时大量产生如下日志消息：

```
 dhcpcd[25188]: wlan0: NAK: from 10.1.0.1
 dhcpcd[25188]: wlan0: soliciting a DHCP lease
 dhcpcd[25188]: wlan0: offered 10.2.0.159 from 10.2.0.1
 dhcpcd[25188]: wlan0: ignoring offer of 10.1.0.197 from 10.1.0.1
 dhcpcd[25188]: wlan0: NAK: from 10.1.0.1
 dhcpcd[25188]: wlan0: soliciting a DHCP lease
 dhcpcd[25188]: wlan0: offered 10.2.0.159 from 10.2.0.1
 dhcpcd[25188]: wlan0: ignoring offer of 10.1.0.197 from 10.1.0.1

```

解决这个问题似乎可以通过切换到 [dhclient](https://www.archlinux.org/packages/?name=dhclient)而不是[dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd)(对于 NetworkManager, 在`/etc/NetworkManager/NetworkManager.conf`中设置`dhcp`选项为 `dhclient`).

### Systemd瓶颈

经过一段时间，日志文件(`/var/log/journal`)可能会变得非常庞大。当使用NetworkManager时，这可能对引导新更能产生大的影响，参考：[Systemd#Boot time increasing over time](/index.php/Systemd#Boot_time_increasing_over_time "Systemd")。

### 网络(WiFi)经常有规律地断开

有些WIFI驱动如果在连接/关联的同时扫描基站会有问题。症状包括VPN断开/重连和丢包，页面无法加载但之后刷新没有问题。

运行`journalctl -f`可以表明这种情况是否正在发生，和下面相似的信息会在日志文件中以有规律的间隔出现：

```
NetworkManager[410]: <info>  (wlp3s0): roamed from BSSID 00:14:48:11:20:CF (my-wifi-name) to (none) ((none))

```

有一个补丁版的NetworkManager应该可以阻止这种扫描：[networkmanager-noscan](https://aur.archlinux.org/packages/networkmanager-noscan/)。

## 提示与技巧

### 加密的Wi-Fi密码

NetworkManager默认在连接文件`/etc/NetworkManager/system-connections/`中以明文存储密码。要打印存储的密码，使用下列命令：

```
# grep -H '^psk=' /etc/NetworkManager/system-connections/*

```

密码可以被文件系统上的root用户以及可以通过GUI（例如`nm-applet`）访问设置的普通用户访问。

以加密形式而不是明文存储密码更好，可以通过在秘钥环中存储它们来实现，NetworkManager之后会向秘钥环询问密码。建议使用的秘钥环守护进程是[GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring")或者(仅适用于KDE)[KDE Wallet](/index.php/KDE_Wallet "KDE Wallet")。 要想让之后的东西工作，秘钥环守护进程需要启动，并且秘钥环需要解锁。

更进一步，NetworkManager需要配置为不为所有的用户存储密码。使用GNOME`nm-applet`，运行`nm-connection-editor`来获取一个终端，选择网络连接，点击`Edit`，选择 `Wifi-Security`选项卡单后点击密码右侧的图标，勾选`Store the password for this user`。使用KDE的[kdeplasma-applets-plasma-nm](https://www.archlinux.org/packages/?name=kdeplasma-applets-plasma-nm)，点击小程序，点击右上方`Settings`图标，双击一个网络连接，在 `General settings`选项卡中，去掉`all users may connect to this network`。如果这个选项被勾选了，及时秘钥环守护进程在运行，密码也将会以明文存储。

如果这个选项之前被选择了，然后你去掉了它，你可能需要先使用`reset`选项来使密码从文件中消失。或者，先删掉连接，然后重新建立。

秘钥环的缺点是连接要为每一个用户设置。

### 通过Wi-Fi共享网络连接

使用nm，你只要点击几下就可以共享你的internet连接（例如，3G或者有线）。你需要一个支持的Wi-Fi卡（基于Atheros AR9xx或者至少AR5xx的网卡可能是最好的选择）。

#### Ad-hoc

*   [安装](/index.php/%E5%AE%89%E8%A3%85 "安装")[dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq)包来能够实际共享连接。
*   配置`dnsmasq.conf`可能会干扰NetworkManager (对此不确定，不过我觉得是这样)。
*   点击小程序，选择"Create new wireless network"。
*   按照指南 (如果使用WEP, 确保使用5到13字符长度的密码,其他的长度可能会失败)。
*   下次你需要的时候，设置依然在存储着。

#### Real AP

2012年底，NetworkManager添加了对infrastructure mode（安卓手机需要这个模式，因为他们故意不支持ad-hoc模式）的支持。

参见 [Fedora's wiki](https://fedoraproject.org/wiki/Features/RealHotspot).

### 通过Ethernet共享连接

场景: 你的设备有通过wi-fi的internet连接，你想通过ethernet和其他设备共享internet连接。

要求:

*   [安装](/index.php/%E5%AE%89%E8%A3%85 "安装")[dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq)以能够真正地共享连接。
*   你的连有internet的设备和其他的设备通过合适的ethernet线缆连接（通常这意味着一个交叉线(cross over cable)或者之间有一个交换机（switch））

步骤:

*   从终端运行`nm-connection-editor`
*   添加一个新的ethernet连接
*   给它起一个合适的名字。比如"共享连接"
*   转到"IPv4 设置"（IPv4 settings）
*   对于"方法:"（method） 选择 "与其他电脑共享"（Shared to other computers）
*   保存

现在，你在NetworkManager的有线连接下应该有了一个新"共享连接"的选项。

### 在cron任务（jobs）或脚本中检查网络是否连接

有些*cron*任务需要可用的网络连接才能成功。你可能希望在网络不可用时避免运行这些任务。为此，添加一个网络的**if** 测试，该测试询问NetworkManager的*nm-tool* 并检查网状态。下面展示的测试当任何接口可用时成功，当所有借口都不可用时失败。对于可能连接有线，无线或者关闭网络的笔记本来说这很方便。

```
if [ $(nm-tool|grep State|cut -f2 -d' ') == "connected" ]; then
    #Whatever you want to do if the network is online
else
    #Whatever you want to do if the network is offline - note, this and the else above are optional
fi

```

例如，这对于一个运行*fpupdate*来更新F-Prot病毒扫描签名的`cron.hourly`脚本很有帮助。另外，经过小的修改，使用*nm-tool*输出的不同部分可以区分不同的网络；例如，因为活跃的无线网络连接有一个星号（asterisk'*'）表示，你可以grep网络名，然后grep星号。

### 登陆后自动解锁秘钥环

#### GNOME

1.  右击面板中的`nm-applet`图标，并选择编辑连接（Edit Connections），打开无线(wireless)选项卡
2.  选择你想要使用的连接并单击编辑
3.  勾选"自动连接"（“Connect Automatically”）框和"对所有用户可用"（“Available to all users”）框

登出并重新登录，完成。

**Note:** 下述方法已经年代久远，并且已知在至少一个机器上不能工作

*   在`/etc/pam.d/gdm` (或者 `/etc/pam.d`里你相应的守护进程中),如果"auth"和"session"块不存在，在后面添加如下内容：

```
 auth            optional        pam_gnome_keyring.so
 session         optional        pam_gnome_keyring.so  auto_start

```

*   在`/etc/pam.d/passwd`中, 使用这一行替代'password'块:

```
 password    optional    pam_gnome_keyring.so

```

	下次登录时，你会被询问你是否希望密码在登录时自动解锁。

#### SLiM 登录管理器

参见 [SLiM#SLiM and Gnome Keyring](/index.php/SLiM#SLiM_and_Gnome_Keyring "SLiM").

### 有密码认证的KDE and OpenConnect VPN

[kdeplasma-applets-plasma-nm](https://www.archlinux.org/packages/?name=kdeplasma-applets-plasma-nm)现在支持配置OpenConnect VPN连接的用户名和密码。打开你的VPN连接，接受证书，连接域会出现。如果没有，看下面的指令，现在输入正确的用户名和密码。

==== 问题解决 ====‘

虽然你可能在连接时输入两个值，[kdeplasma-applets-plasma-nm](https://www.archlinux.org/packages/?name=kdeplasma-applets-plasma-nm) 0.9.3.2-1及以上版本能够直接从KWallet中获取OpenConnect用户名和密码。

打开"KDE Wallet Manager"在"Network Management|Maps"下面查找你的OpenConnect VPN连接。点击"Show values"并在这个表的键值"VpnSecrets"下输入你的凭据（相应替代'username'和'password'）:

```
form:main:username%SEP%*username*%SEP%form:main:password%SEP%*password*

```

下次你连接时，用户名和密码会出现在"VPN secrets"对话框中。

### 忽略特定设备

有时，可能希望Networkmanager忽略特定的设备，并且不为他们配置地址和路由。通过在`/etc/NetworkManager/NetworkManager.conf`中使用下述配置，你可以快速轻松地按照MAC或者接口名忽略设备。

```
[keyfile]
unmanaged-devices=mac:00:22:68:1c:59:b1;mac:00:1E:65:30:D1:C4;interface-name:eth0

```

填入上述内容后，[重启](/index.php/Daemons_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Daemons (简体中文)")NetworkManager，然后你应该能够在NetworkManager不改变你已经完成的设置的情况下配置接口。

### 启用DNS缓存

使用[dnsmasq](/index.php/Dnsmasq "Dnsmasq")来启用允许DNS缓存的插件参见 [dnsmasq#NetworkManager](/index.php/Dnsmasq#NetworkManager "Dnsmasq")

### 启用IPv6隐私扩展

参见 [IPv6#NetworkManager](/index.php/IPv6#NetworkManager "IPv6")

## 其它资源

*   [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") -- 无线配置(wiki)
*   [NetworkManager](http://www.gnome.org/projects/NetworkManager/) - 网络管理器的官方主页
*   [NetworkManager for Administrators Part 1](http://blogs.gnome.org/dcbw/2015/02/16/networkmanager-for-administrators-part-1/)