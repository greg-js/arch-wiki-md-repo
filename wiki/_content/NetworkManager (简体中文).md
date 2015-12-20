# NetworkManager (简体中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Network configuration](/index.php/Network_configuration "Network configuration")
*   [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")
*   [Category:Network managers](/index.php/Category:Network_managers "Category:Network managers")

**翻译状态：** 本文是英文页面 [NetworkManager](/index.php/NetworkManager "NetworkManager") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-02-17，点击[这里](https://wiki.archlinux.org/index.php?title=NetworkManager&diff=0&oldid=361369)可以查看翻译后英文页面的改动。

[网络管理器](http://projects.gnome.org/NetworkManager/)(NetworManager)是检测网络、自动连接网络的程序。无论是无线还是有线连接，它都可以令您轻松管理。对于无线网络,网络管理器可以自动切换到最可靠的无线网络。利用网络管理器的程序可以自由切换在线和离线模式。网络管理器可以优先选择有线网络，支持 VPN。网络管理器最初由 Redhat 公司开发，现在由 [GNOME](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)") 管理。

**警告:** 请注意, Wi-Fi 的密码默认情况下是明文保存的。参见 [#Encrypted Wi-Fi passwords](#Encrypted_Wi-Fi_passwords)

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 VPN 支持](#VPN_.E6.94.AF.E6.8C.81)
    *   [1.2 PPPoE / DSL 支持](#PPPoE_.2F_DSL_.E6.94.AF.E6.8C.81)
*   [2 图形前端](#.E5.9B.BE.E5.BD.A2.E5.89.8D.E7.AB.AF)
    *   [2.1 Gnome环境](#Gnome.E7.8E.AF.E5.A2.83)
    *   [2.2 KDE4](#KDE4)
    *   [2.3 XFCE](#XFCE)
    *   [2.4 Openbox](#Openbox)
    *   [2.5 其它桌面和窗口管理器](#.E5.85.B6.E5.AE.83.E6.A1.8C.E9.9D.A2.E5.92.8C.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [2.6 命令行](#.E5.91.BD.E4.BB.A4.E8.A1.8C)
        *   [2.6.1 nmcli](#nmcli)
        *   [2.6.2 nmtui](#nmtui)
        *   [2.6.3 nmcli-dmenu](#nmcli-dmenu)
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
    *   [5.1 PPTP 通道中无流量](#PPTP_.E9.80.9A.E9.81.93.E4.B8.AD.E6.97.A0.E6.B5.81.E9.87.8F)
    *   [5.2 网络管理功能失效](#.E7.BD.91.E7.BB.9C.E7.AE.A1.E7.90.86.E5.8A.9F.E8.83.BD.E5.A4.B1.E6.95.88)
    *   [5.3 使用 resolv.conf.head 和 resolv.conf.tail](#.E4.BD.BF.E7.94.A8_resolv.conf.head_.E5.92.8C_resolv.conf.tail)
    *   [5.4 在resolv.conf中保留改动](#.E5.9C.A8resolv.conf.E4.B8.AD.E4.BF.9D.E7.95.99.E6.94.B9.E5.8A.A8)
    *   [5.5 DHCP 问题](#DHCP_.E9.97.AE.E9.A2.98)
    *   [5.6 主机问题](#.E4.B8.BB.E6.9C.BA.E9.97.AE.E9.A2.98)
    *   [5.7 缺少默认路由 route](#.E7.BC.BA.E5.B0.91.E9.BB.98.E8.AE.A4.E8.B7.AF.E7.94.B1_route)
    *   [5.8 没有探测到 3G 模块](#.E6.B2.A1.E6.9C.89.E6.8E.A2.E6.B5.8B.E5.88.B0_3G_.E6.A8.A1.E5.9D.97)
    *   [5.9 在笔记本上切换网络](#.E5.9C.A8.E7.AC.94.E8.AE.B0.E6.9C.AC.E4.B8.8A.E5.88.87.E6.8D.A2.E7.BD.91.E7.BB.9C)
    *   [5.10 静态 IP 设置 变成 DHCP](#.E9.9D.99.E6.80.81_IP_.E8.AE.BE.E7.BD.AE_.E5.8F.98.E6.88.90_DHCP)
    *   [5.11 普通用户无法编辑链接](#.E6.99.AE.E9.80.9A.E7.94.A8.E6.88.B7.E6.97.A0.E6.B3.95.E7.BC.96.E8.BE.91.E9.93.BE.E6.8E.A5)
    *   [5.12 删除隐蔽无线网络链接](#.E5.88.A0.E9.99.A4.E9.9A.90.E8.94.BD.E6.97.A0.E7.BA.BF.E7.BD.91.E7.BB.9C.E9.93.BE.E6.8E.A5)
    *   [5.13 GNOME VPN失效问题](#GNOME_VPN.E5.A4.B1.E6.95.88.E9.97.AE.E9.A2.98)
    *   [5.14 Unable to connect to visible European wireless networks](#Unable_to_connect_to_visible_European_wireless_networks)
    *   [5.15 Automatic connect to VPN on boot is not working](#Automatic_connect_to_VPN_on_boot_is_not_working)
    *   [5.16 dhcpcd repetitively refusing leases](#dhcpcd_repetitively_refusing_leases)
    *   [5.17 Systemd Bottleneck](#Systemd_Bottleneck)
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 Encrypted Wi-Fi passwords](#Encrypted_Wi-Fi_passwords)
    *   [6.2 将internet连接设置成WIFI网络共享](#.E5.B0.86internet.E8.BF.9E.E6.8E.A5.E8.AE.BE.E7.BD.AE.E6.88.90WIFI.E7.BD.91.E7.BB.9C.E5.85.B1.E4.BA.AB)
        *   [6.2.1 Ad-hoc](#Ad-hoc)
        *   [6.2.2 Real AP](#Real_AP)
    *   [6.3 在cron脚本中检查网络是否OK](#.E5.9C.A8cron.E8.84.9A.E6.9C.AC.E4.B8.AD.E6.A3.80.E6.9F.A5.E7.BD.91.E7.BB.9C.E6.98.AF.E5.90.A6OK)
    *   [6.4 Automatically unlock keyring after login](#Automatically_unlock_keyring_after_login)
        *   [6.4.1 GNOME](#GNOME)
        *   [6.4.2 KDE](#KDE)
        *   [6.4.3 SLiM](#SLiM)
    *   [6.5 Ignore specific devices](#Ignore_specific_devices)
    *   [6.6 Connect faster](#Connect_faster)
        *   [6.6.1 Disabling IPv6](#Disabling_IPv6)
        *   [6.6.2 Speed up DHCP by disabling ARP probing in DHCPCD](#Speed_up_DHCP_by_disabling_ARP_probing_in_DHCPCD)
        *   [6.6.3 开启 OpenDNS 服务](#.E5.BC.80.E5.90.AF_OpenDNS_.E6.9C.8D.E5.8A.A1)
*   [7 其它资源](#.E5.85.B6.E5.AE.83.E8.B5.84.E6.BA.90)

## 安装

[networkmanager](https://www.archlinux.org/packages/?name=networkmanager) 可以直接在 `[extra]` 源中进行安装

```
# pacman -S networkmanager

```

**Note:** 请确保没有其他与配置网络相关的服务正在运行; 事实上, 多个网络配置服务之间会相互冲突。如果想知道当前有哪些服务正在运行, 可以运行 `systemctl --type=service` 然后 [停止](/index.php/Systemd#Using_units "Systemd") 多余的网络配置服务。参见 [#配置](#.E9.85.8D.E7.BD.AE) 来启动 NetworkManager 服务。

### VPN 支持

NetworkManager 的 VPN 支持基于一个插件系统。如果需要通过 NetworkManager 来使用 VPN, 请从 [官方软件仓库](/index.php/Official_repositories "Official repositories") 下载安装以下任一软件包:

*   [networkmanager-openconnect](https://www.archlinux.org/packages/?name=networkmanager-openconnect)
*   [networkmanager-openvpn](https://www.archlinux.org/packages/?name=networkmanager-openvpn)
*   [networkmanager-pptp](https://www.archlinux.org/packages/?name=networkmanager-pptp)
*   [networkmanager-vpnc](https://www.archlinux.org/packages/?name=networkmanager-vpnc)

通过 [AUR](/index.php/AUR "AUR"):

*   [networkmanager-l2tp](https://aur.archlinux.org/packages/networkmanager-l2tp/)<sup><small>AUR</small></sup>

### PPPoE / DSL 支持

安装 [rp-pppoe](https://www.archlinux.org/packages/?name=rp-pppoe) 来获得 PPPoE / DSL 连接支持。

## 图形前端

为了方便使用网络管理器进行管理和配置，通常需要安装托盘组件。图形前端往往显示在系统托盘（或通知区域），从而允许用户选择网络或者配置 NetworkManager。各种桌面环境的安装方法如下:

### Gnome环境

Gnome的[network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet)是一个轻量级的全能组件，几乎可以运行在所有的桌面环境下。

如果你想储存验证信息(Wireless/DSL)，并提供给所有用户使用，那么您还需要安装和配置[GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring")

### KDE4

Plasma-nm 前端可以通过官方软件仓库中的 [kdeplasma-applets-plasma-nm](https://www.archlinux.org/packages/?name=kdeplasma-applets-plasma-nm)<sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kdeplasma-applets-plasma-nm)]</sup> 安装。老的 KNetworkManager 前端已经移到了[AUR](/index.php/AUR "AUR") 软件包 [kdeplasma-applets-networkmanagement](https://aur.archlinux.org/packages/kdeplasma-applets-networkmanagement/)<sup><small>AUR</small></sup> 。

如果同时安装了 KNetworkManager 和 nm-applet，在使用 KDE 时不想使用 nm-applet，将下行加入 `/etc/xdg/autostart/nm-applet.desktop`

```
NotShowIn=KDE

```

详情参阅 [Userbase 页面](http://userbase.kde.org/NetworkManagement)。

### XFCE

nm-applet 可以在 XFCE 下正常工作，但是为了可以显示通知信息，_包括错误信息_， nm-applet 需要一个 Freedesktop 桌面通知扩展（查阅 [[1]](http://www.galago-project.org/specs/notification/0.9/index.html)）。xfce4-notifyd 就是这么一个扩展。

```
# pacman -S network-manager-applet xfce4-notifyd

```

如果这个扩展没有运行守护进程，nm-applet 就会输出下面的错误到 stdout/stderr：

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

尽管没有通知系统，nm-applet 仍然会正常工作。

如果 `nm-applet` 在连接到 WiFi 时没有提示输入密码, 且会立即断开连接, 你可能需要安装 [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring)。

### Openbox

GNOME applet 和 xfce4-notifyd 结合可以很好的工作:

```
# pacman -S network-manager-applet xfce4-notifyd hicolor-icon-theme gnome-icon-theme

```

如果你想储存验证信息(Wireless/DSL)，请安装：

```
# pacman -S gnome-keyring

```

要让 Openbox `autostart` 启动 nm-applet，需要删除文件`/etc/xdg/autostart/nm-applet.desktop`。每次更新 network-manager-applet 都需要删除这个文件。 在 `autostart` 中加入：

```
# (sleep 3 && /usr/bin/nm-applet --sm-disable) &

```

### 其它桌面和窗口管理器

推荐使用 GNOME 组件，需要安装 GNOME hicolor 主题：

```
# pacman -S hicolor-icon-theme gnome-icon-theme

```

不使用系统托盘，可以使用 [trayer](https://www.archlinux.org/packages/?name=trayer) 或 [stalonetray](https://www.archlinux.org/packages/?name=stalonetray)。例如，在路径中加入 "nmgui" 脚本：

 `nmgui` 

```
#!/bin/sh
nm-applet    2>&1 /dev/null &
stalonetray  2>&1 /dev/null
killall nm-applet

```

关闭 stalonetray 窗口时，将会同时关闭 `nm-applet`，所以完成网络设置后不会使用额外的内存。

### 命令行

#### nmcli

[networkmanager](https://www.archlinux.org/packages/?name=networkmanager) 0.8.1 版之后包含 [nmcli](http://manpages.ubuntu.com/manpages/maverick/man1/nmcli.1.html)

例子:

*   连接到 WiFi 网络: `nmcli dev wifi connect <name> password <password>` 
*   通过接口 wlan1 连接到 WiFi 网络: `nmcli dev wifi connect <name> password <password> iface wlan1 [profile name]` 
*   断开 WiFi 连接: `nmcli dev disconnect iface eth0` 
*   通过一个已断开连接的接口重新连接: `nmcli con up uuid <uuid>` 
*   获得一份 UUID 列表: `nmcli con show` 
*   查看网络设备及其状态: `nmcli dev` 
*   关闭 WiFi: `nmcli r wifi off` 

#### nmtui

"nmtui" 是 networkmanager 的一个图形化前端。在没有 X Window 的情况下可以用它来方便地配置及管理网络。[networkmanager](https://www.archlinux.org/packages/?name=networkmanager) 0.9.10 版之后就包含了 "nmtui"。

#### nmcli-dmenu

[networkmanager-dmenu-git](https://aur.archlinux.org/packages/networkmanager-dmenu-git/)<sup><small>AUR</small></sup> 是一个通过 _dmenu_ 而不是 `nm-applet` 来管理 NetworkManager 连接的脚本。它提供了所有必要的特性, 例如连接到已有的 WiFi 或有线网络, 连接到新的 WiFi 网络, 在需要的时候询问密码, 连接到已有的 VPN, 启用或停用网络连接, 运行 _nm-connection-editor_ 的图形界面。

## 配置

NetworkManager 需要做这么几步保证正常运行。

先验证 `/etc/hosts` 配置正确，如果配置不正确，网络管理器可能修改它。示例：

 `/etc/hosts` 

```
127.0.0.1 localhost
::1       localhost

```

**注意:** 请使用 `systemctl --type=service` 命令察看是否有其它网络配置相关的服务。多个网络配置服务之间会相互冲突。

### 启用 NetworkManager

NetworkManager 守护进程启动后，会自动连接到已经配置的**系统连接**。**用户连接**或未配置的连接需要通过`nmcli`或桌面工具进行配置和连接。

开机启用 NetworkManager：

```
# systemctl enable NetworkManager

```

立即启动 NetworkManager：

```
# systemctl start NetworkManager

```

**注意:** 个别服务在网络建立前启动会出错，需要使用`NetworkManager-wait-online.service`。

### 设置 PolicyKit 权限

参照[General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting")建立一个工作会话. 在工作会话中,你有三种方式授予NetworkManager工作所必须的权限.

_方式 1._ 登录后运行[PolicyKit](/index.php/PolicyKit "PolicyKit")认证代理,比如 `/usr/lib/polkit-gnome/polkit-gnome-authentication-agent-1` ([polkit-gnome](https://www.archlinux.org/packages/?name=polkit-gnome) 的一部分). 当你添加和删除一个网络链接时会提示输入密码.

_方式 2._ 将你的账户加入`wheel`账户组. 管理网络时你将不需要输入密码,但注意你的账户同时被赋予了此账户组的其他权限,比如运行[sudo](/index.php/Sudo "Sudo")命令是无需密码.

_方式 3._ 将你的账户加入`network`账户组,同时创建以下文件:

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
# chown root:root _scriptname_

```

而且脚本必须只能是拥有者可写, 否则不会被执行:

```
# chmod 755 _scriptname_

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

由于该脚本在一个非常受限制的环境中运行, 为了连接上SSH agent, 你必须 export `SSH_AUTH_SOCK`。 这里有几种不同方式, 参照 [here](https://bbs.archlinux.org/viewtopic.php?pid=1042030#p1042030) 获取更多详细信息. 以下示例需要 gnome-keyring , 如果 gnome-keyring 没解锁,将需要你输入密码. 如果 NetworkManager 设置为登录后自动连接, 很有可能因为 _gnome-keyring_ 还没启动导致失败(转入睡眠). 对应的 UUID 可以通过命令 `nmcli con status` 或 `nmcli con list` 查得。

```
#!/bin/sh
USER='username'
REMOTE='user@host:/remote/path'
LOCAL='/local/path'

interface=$1 status=$2
if [ "$CONNECTION_UUID" = "_uuid_" ]; then
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

如果想任意用户都能使用 VPN, 即使已经在 `nm-applet` 中勾选了 _Make the VPN connection available to all users_ 选项, 由于 [VPN secrets 保管方式的原因](http://developer.gnome.org/NetworkManager/0.9/secrets-flags.html), 连接依然可能会失败并且 NetworkManager 会报错 'no valid VPN secrets'。这样就需要执行步骤2:

2\. 可以选择编辑 VPN 连接的配置文件让 NetworkManager 自己储存 secrets 而不是把 secrets 保存在 [不能被root访问的](https://bugzilla.redhat.com/show_bug.cgi?id=710552) keyring 中: 打开 `/etc/NetworkManager/system-connections/_name of your VPN connection_`, 把 `password-flags` 以及 `secret-flags` 从 `1` 改为 `0`。

或者直接在 VPN 配置文件中加入 `vpn-secrets` 并写入密码:

```
 [vpn]
 ....
 password-flags=0

 [vpn-secrets]
 password=_your_password_

```

**注意:** 现在可能有必要重新打开 NetworkManager connection editor 并再次保存 VPN passwords/secrets。

### 代理设置

NetworkManager不直接处理代理设置，但是如果你使用[GNOME](/index.php/GNOME "GNOME")，你可以使用 [proxydriver](http://marin.jb.free.fr/proxydriver/)配合NetworkManager。 [proxydriver](https://aur.archlinux.org/packages/proxydriver/)<sup><small>AUR</small></sup>软件包位于 [AUR](/index.php/AUR "AUR").

为使proxydriver设置代理，你需要在设置GNOME自动启动进程( System->Preferences->Startup Applications):

```
xhost +si:localuser:your_username

```

参照: [Proxy settings](/index.php/Proxy_settings "Proxy settings")

### 禁用 NetworkManager

由于服务是通过 _dbus_ 自动启动的, 所以要完全禁用可以用 _systemctl_ 来屏蔽:

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

为一些常见问题提供解决办法。

### PPTP 通道中无流量

PPTP连接正常，可以正常看到VPN IP，但是不能ping通远端IP，这是由于Arch pppd缺少MPPE (Microsoft Point-to-Point Encryption) 支持. 推荐首先使用[ppp](https://www.archlinux.org/packages/?name=ppp)。

同时安装 [ppp-mppe](https://aur.archlinux.org/packages/ppp-mppe/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ppp-mppe)]</sup>

### 网络管理功能失效

有时NetworkManager关闭了，但对应的pid文件却没有移除，同时你得到提示 'Network management disabled'. 你可以手工处理:

```
# rm /var/lib/NetworkManager/NetworkManager.state

```

### 使用 resolv.conf.head 和 resolv.conf.tail

请阅读 [resolv.conf](/index.php/Resolv.conf "Resolv.conf") 并确保 NetworkManager 使用的是 [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) 而不是 [dhclient](https://www.archlinux.org/packages/?name=dhclient)。如果要使用 [dhclient](https://www.archlinux.org/packages/?name=dhclient)，可以试试[AUR](/index.php/AUR "AUR")里面的 [networkmanager-dispatch-resolv](https://aur.archlinux.org/packages/networkmanager-dispatch-resolv/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/networkmanager-dispatch-resolv)]</sup>。

### 在resolv.conf中保留改动

NetworkManager试图将DHCP中获取的DNS信息写入`/etc/resolv.conf`,导致原文件被覆盖,你可以在文件属性中设置i参数避免文件被修改

```
# chattr +i /etc/resolv.conf

```

如果你要修改此文件,移除i参数:

```
# chattr -i /etc/resolv.conf

```

### DHCP 问题

如果你无法通过DHCP获取IP,尝试在`/etc/dhclient.conf`添加如下配置:

```
 interface "eth0" {
   send dhcp-client-identifier 01:aa:bb:cc:dd:ee:ff;
 }

```

`aa:bb:cc:dd:ee:ff` 是你网卡的MAC地址. MAC地址可以使用[iproute2](https://www.archlinux.org/packages/?name=iproute2) 中的 `ip link show eth0` 命令

对某些不兼容的路由器,你必须在`/etc/dhcpcd.conf` (注意此文件有别于`dhcpd.conf`)文件中注释

```
require dhcp_server_identifier

```

这样应该可以工作了,但是如果你的网络中不幸存在多个DHCP服务器的话,你还需要参照 [this page](http://technet.microsoft.com/en-us/library/cc977442.aspx) 获取更多信息.

### 主机问题

这取决与你所使用的NetworkManager插件，该主机名是否被转发到一个已经链接上的路由器上。通用的“密钥文件”插件不违反默认配置主机名转发。为了能够转发主机名，添加下面的内容到`/etc/NetworkManager/NetworkManager.conf`：

```
[keyfile]
hostname=_your_hostname_

```

默认路径`/etc/NetworkManager/system-connections`的网络链接将应用`[密钥文件]`的选择。

另一种选择是配置NetworkManager自动启动配置DHCP客户端去转发主机名。 NetworkManager utilizes [dhclient](https://www.archlinux.org/packages/?name=dhclient) in default and falls back to [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd), if the former is not installed. To make _dhclient_ forward the hostname requires to set a non-default option, _dhcpcd_ forwards the hostname by default.

首先，核对使用哪一个DHCP客户端(_dhclient_ in this example):

 `# journalctl -b | egrep "dhclient|dhcpcd"` 

```
...
Nov 17 21:03:20 zenbook dhclient[2949]: Nov 17 21:03:20 zenbook dhclient[2949]: Bound to *:546
Nov 17 21:03:20 zenbook dhclient[2949]: Listening on Socket/wlan0
Nov 17 21:03:20 zenbook dhclient[2949]: Sending on   Socket/wlan0
Nov 17 21:03:20 zenbook dhclient[2949]: XMT: Info-Request on wlan0, interval 1020ms.
Nov 17 21:03:20 zenbook dhclient[2949]: RCV: Reply message on wlan0 from fe80::126f:3fff:fe0c:2dc.

```

source [https://bbs.archlinux.org/viewtopic.php?id=152376](https://bbs.archlinux.org/viewtopic.php?id=152376)

### 缺少默认路由 route

至少在KDE4系统中,当使用NetworkManager [Wireless_Setup_(简体中文)](/index.php/Wireless_Setup_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wireless Setup (简体中文)")链接时不会建立缺省路由. 可以通过在无线链接路由配置中移除"Use only for resources on this connection"部分解决问题

### 没有探测到 3G 模块

如果NetworkManager(从v0.7.999)没有探测到你的3G模块,但是你仍然可以使用[wvdial](/index.php/Wvdial "Wvdial")连接, 可以尝试安装[modemmanager](https://www.archlinux.org/packages/?name=modemmanager),并使用`rc.d restart networkmanager`重启服务,你可能需要重插或重启你的3G模块, 这可以让NetworkManager支持默认数据库中缺失的硬件模块

### 在笔记本上切换网络

有时候, NetworkManager在你关闭和开启WIFI适配器后会无法工作,这常常是`rfkill`的问题,请从[official repositories](/index.php/Official_repositories "Official repositories")安装[rfkill](https://www.archlinux.org/packages/?name=rfkill)并使用 $ watch -n1 rfkill list all 检测驱动`rfkill`是否上报无线适配器的状态. 如果你开启适配器后,其标识符仍然显示blocked,你可以尝试如下命令,手动unblock(X是前一条命令的identifier编号)

```
# rfkill event unblock X

```

### 静态 IP 设置 变成 DHCP

这里有个BUG，当你将缺省链接设置成静态IP时，`nm-applet` 可能不能保存你的IP配置，而自动转变为DHCP模式。

对于这个问题，你不得不在首先在`nm-applet`改变连接的名称（比如将"Auto eth0"变成“my eth0”）,去掉“Available to all users”的勾号。输入你的配置IP地址，然后点击“Apply”，这样就能保存你的配置

如果你不希望默认链接自动连接网络，运行 `nm-connection-editor` (_not_ as root). 在链接配置窗口，选中默认配置(eg "Auto eth0") 去掉"Connect automatically". 点击 **Apply**.

### 普通用户无法编辑链接

See [#Set_up_PolicyKit_permissions](#Set_up_PolicyKit_permissions).

### 删除隐蔽无线网络链接

因为隐蔽无线网络不出现在无线列表中，所以不能在GUI中删除，你可以试用以下命令：

```
# rm /etc/NetworkManager/system-connections/[SSID]

```

此命令对所用所有连接有效 This works for any other connection.

### GNOME VPN失效问题

在[Gnome](/index.php/Gnome "Gnome")系统中用NetworkManager 设立[OpenConnect](/index.php/OpenConnect "OpenConnect")或VPN链接，有时会无法跳出对话框，在/var/log/errors.log中会出现如下错误提示：

```
localhost NetworkManager[399]: <error> [1361719690.10506] [nm-vpn-connection.c:1405] get_secrets_cb(): Failed to request VPN secrets #3: (6) No agents were available for this request.

```

这是由于Gnome NM Applet在/usr/lib/gnome-shell中读取脚本， 而NetworkManager安装包将脚本安装/usr/lib/networkmanager中. 临时解决方法可以文件夹中创建软连接

```
# For OpenConnect
ln -s /usr/lib/networkmanager/nm-openconnect-auth-dialog /usr/lib/gnome-shell/ 

```

```
# For VPNC (i.e. Cisco VPN)
ln -s /usr/lib/networkmanager/nm-vpnc-auth-dialog /usr/lib/gnome-shell/

```

这种方法对其他类型的NM VPN插件也适用，不过上述两种VPN是最平常的。

### Unable to connect to visible European wireless networks

WLAN chips are shipped with a default [regulatory domain](/index.php/Wireless_network_configuration#Respecting_the_regulatory_domain "Wireless network configuration"). If your access point does not operate within these limitations, you will not be able to connect to the network. Fixing this is easy:

1.  [Install](/index.php/Install "Install") [crda](https://www.archlinux.org/packages/?name=crda)
2.  Uncomment the correct Country Code in `/etc/conf.d/wireless-regdom`
3.  Reboot the system, because the setting is only read on boot

### Automatic connect to VPN on boot is not working

The problem occurs when the system (i.e. NetworkManager running as the root user) tries to establish a VPN connection, but the password is not accessible because it is stored in the Gnome keyring of a particular user.

A solution is to keep the password to your VPN in plaintext, as described in step (2.) of [#Use dispatcher to connect to a VPN after a network connection is established](#Use_dispatcher_to_connect_to_a_VPN_after_a_network_connection_is_established).

You do not need to use the dispatcher described in step (1.) to auto-connect anymore, if you use the new "auto-connect VPN" option from the `nm-applet` GUI.

### dhcpcd repetitively refusing leases

An occurrence of dhcpcd repetitively refusing leases has been reported, while spouting a large quantity of the following log messages :

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

This problem seems to be solved by switching to [dhclient](https://www.archlinux.org/packages/?name=dhclient) instead of [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) (with NetworkManager, set the `dhcp` option to `dhclient` in `/etc/NetworkManager/NetworkManager.conf`).

### Systemd Bottleneck

Over time the log files (`/var/log/journal`) can become very large. This can have a big impact on boot performance when using NetworkManager, see: [Systemd#Boot time increasing over time](/index.php/Systemd#Boot_time_increasing_over_time "Systemd").

## Tips and tricks

### Encrypted Wi-Fi passwords

By default, NetworkManager stores passwords in clear text in the connection files at `/etc/NetworkManager/system-connections/`. To print the stored passwords, use the following command:

```
# grep -H '^psk=' /etc/NetworkManager/system-connections/*

```

The passwords are accessible to the root user in the filesystem and to users with access to settings via the GUI (e.g. `nm-applet`).

If it is preferable to save the passwords in encrypted form instead of clear text, this can be achieved by storing them in a keyring which NetworkManager then queries for the passwords. A suggested keyring daemon is [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring") or (for KDE specifically) [KDE Wallet](/index.php/KDE_Wallet "KDE Wallet"). The keyring daemon has to be started and the keyring needs to be unlocked for the following to work.

Furthermore, NetworkManager needs to be configured not to store the password for all users. Using GNOME `nm-applet`, run `nm-connection-editor` from a terminal, select a network connection, click `Edit`, select the `Wifi-Security` tab and click on the right icon of password and check `Store the password for this user`. Using KDE's [kdeplasma-applets-plasma-nm](https://www.archlinux.org/packages/?name=kdeplasma-applets-plasma-nm)<sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kdeplasma-applets-plasma-nm)]</sup>, click the applet, click on the top right `Settings` icon, double click on a network connection, in the `General settings` tab, untick `all users may connect to this network`. If the option is ticked, the passwords will still be stored in clear text, even if a keyring daemon is running.

If the option was selected previously and you un-tick it, you may have to use the `reset` option first to make the password disappear from the file. Alternatively, delete the connection first and set it up again.

The downside of using the keyring is that the connections have to be set up for each user.

### 将internet连接设置成WIFI网络共享

你可以适用nm分享你的internet连接（3G或有线），硬件上你需要有WIFI无线网卡(最好基于Atheros AR9xx or at least AR5xx)

#### Ad-hoc

*   pacman -S dnsmasq
*   custom dnsmasq.conf may interfere with nm (not sure about this, but i think so)
*   Click on nm-applet -> Create new wireless network
*   Follow wizard (if using WEP be sure to use 5 or 13 charactes long password, different lengths will fail)
*   Settings will remain stored for next time you'll need it

#### Real AP

Support of infrastructure mode (which is needed by Andoid phones as they don't intentionally support ad-hoc) is not currently supported by NetworkManager, but is in active development...

See: [http://fedoraproject.org/wiki/Features/RealHotspot](http://fedoraproject.org/wiki/Features/RealHotspot)

### 在cron脚本中检查网络是否OK

某些cron jobs需要在网络OK的状态下工作，你可能希望在网络无法连接时不启动这些cron. 你可以在脚本中使用

```
NetworkManager's `nm-tool` 查询网络状态。 笔记本经常在有线、无线中切换，以下脚本演示了如何处理这种状态 
if [ `nm-tool|grep State|cut -f2 -d' '` == "connected" ]; then
       #Whatever you want to do if the network is online
else
       #Whatever you want to do if the network is offline - note, this and the else above are optional
fi

```

This useful for a `cron.hourly` script that runs `fpupdate` for the F-Prot virus scanner signature update, as an example. Another way it might be useful, with a little modification, is to differentiate between networks using various parts of the output from `nm-tool`; for example, since the active wireless network is denoted with an asterisk, you could grep for the network name and then grep for a literal asterisk.

### Automatically unlock keyring after login

#### GNOME

1.  Right click on the `nm-applet` icon in your panel and select Edit Connections and open the Wireless tab
2.  Select the connection you want to work with and click the Edit button
3.  Check the boxes “Connect Automatically” and “Available to all users”

Log out and log back in to complete.

**Note:** The following method is dated and known not to work on at least one machine!

*   In `/etc/pam.d/gdm` (or your corresponding daemon in `/etc/pam.d`), add these lines at the end of the "auth" and "session" blocks if they do not exist already:

```
 auth            optional        pam_gnome_keyring.so
 session         optional        pam_gnome_keyring.so  auto_start

```

*   In `/etc/pam.d/passwd`, use this line for the 'password' block:

```
 password    optional    pam_gnome_keyring.so

```

Next time you log in, you should be asked if you want the password to be unlocked automatically on login.

#### KDE

**Note:** See [http://live.gnome.org/GnomeKeyring/Pam](http://live.gnome.org/GnomeKeyring/Pam) for reference, and if you are using KDE with KDM, you can use [pam-keyring-tool](https://aur.archlinux.org/packages/pam-keyring-tool/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/pam-keyring-tool)]</sup> from the [AUR](/index.php/AUR "AUR").

Put a script like the following in `~/.kde4/Autostart`:

```
 #!/bin/sh
 echo PASSWORD | /usr/bin/pam-keyring-tool --unlock --keyring=default -s

```

Similar should work with Openbox, LXDE, etc.

#### SLiM

参阅[Slim#SLiM and Gnome Keyring](/index.php/Slim#SLiM_and_Gnome_Keyring "Slim").

### Ignore specific devices

Sometimes it may be desired that NetworkManager ignores specific devices and does not try to configure addresses and routes for them.

1\. You can quickly and easily ignore devices by MAC by using the following in `/etc/NetworkManager/NetworkManager.conf` :

```
[keyfile]
unmanaged-devices=mac:00:22:68:1c:59:b1;mac:00:1E:65:30:D1:C4

```

After you have put this in, [restart](/index.php/Daemon "Daemon") NetworkManager, and you should be able to configure interfaces without NetworkManager altering what you have set.

2\. If that is not appropriate, you could ignore by HAL.

*   First you have to find out the Hal UDI (e.g. with `lshal`):

```
 ...
 info.product = 'Networking Interface'  (string)
 info.subsystem = 'net'  (string)
 info.udi = '/org/freedesktop/Hal/devices/net_00_1f_11_01_06_55'  (string)
 linux.hotplug_type = 2  (0x2)  (int)
 linux.subsystem = 'net'  (string)
 ...

```

*   Add the udi to `/etc/NetworkManager/nm-system-settings.conf`:

```
 [keyfile]
   unmanaged-devices=/org/freedesktop/Hal/devices/net_00_1f_11_01_06_55

```

Multiple devices can be specified, delimited by semicolons:

```
 [keyfile]
   unmanaged-devices=/org/freedesktop/Hal/devices/net_00_1f_11_01_06_55;/org/freedesktop/Hal/devices/net_00_2c_6d_e2_08_af

```

You do not need to restart NetworkManager for the changes to take effect.

3\. Devices could also be ignored at boot time by using following script (change `NetworkManager.conf` with `nm-system-settings.conf` if using a version of NetworkManager smaller than 0.8.1):

```
  #!/bin/sh
  # author: tim noise <darknoise@drkns.net>
  COUNT=0
  TARGET_FILE="/etc/NetworkManager/NetworkManager.conf"
  for i in `lshal | grep -A6 'Networking Interface' | awk -F "'" '/info.udi = / {print $2}'`; do
      if [ $COUNT = 0 ]; then
          COUNT=$COUNT+1;
          echo "unmanaged-devices=$i" >> $TARGET_FILE
      else
          echo -n ";$i" >> $TARGET_FILE
      fi
  done
  printf "\n" >> $TARGET_FILE

```

It can be changed to ignore WiFi devices, etc. being used on a non-persistant filesystem.

### Connect faster

#### Disabling IPv6

Slow connection or reconnection to the network may be due to superfluous IPv6 queries in NetworkManager. If there is no IPv6 support on the local network, connecting to a network may take longer than normal while NetworkManager tries to establish an IPv6 connection that eventually times out. The solution is to disable IPv6 within NetworkManager which will make network connection faster. This has to be done once for every network you connect to.

*   Right-click on the network status icon.
*   Click on "Edit Connections".
*   Go to the "Wired" or "Wireless" tab, as appropriate.
*   Select the name of the network.
*   Click on "Edit".
*   Go to the "IPv6 Settings" tab.
*   In the "Method" dropdown, choose "Ignore/Disabled".
*   Click on "Save".

#### Speed up DHCP by disabling ARP probing in DHCPCD

`dhcpcd` contains an implementation of a recommendation of the DHCP standard ([RFC2131](http://www.ietf.org/rfc/rfc2131.txt) section 2.2) to check via ARP if the assigned IP address is really not taken. This seems mostly useless in home networks, so you can save about 5 seconds on every connect by adding the following line to `/etc/dhcpcd.conf`:

```
noarp

```

This is equivalent to passing `--noarp` to `dhcpcd`, and disables the described ARP probing, speeding up connections to networks with DHCP.

#### 开启 OpenDNS 服务

Create `/etc/resolv.conf.opendns` with the nameservers:

```
nameserver 208.67.222.222
nameserver 208.67.220.220

```

And have the dispatcher replace the discovered DHCP servers with the OpenDNS ones:

 `/etc/NetworkManager/dispatcher.d/dns-servers-opendns` 

```
#!/bin/bash
# Use OpenDNS servers over DHCP discovered servers

cp -f /etc/resolv.conf.opendns /etc/resolv.conf
```

Make the script executable:

```
# chmod +x /etc/NetworkManager/dispatcher.d/dns-servers-opendns

```

## 其它资源

*   [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") -- 无线配置(wiki)
*   [NetworkManager](http://www.gnome.org/projects/NetworkManager/) - 网络管理器的官方主页

Retrieved from "[https://wiki.archlinux.org/index.php?title=NetworkManager_(简体中文)&oldid=412827](https://wiki.archlinux.org/index.php?title=NetworkManager_(简体中文)&oldid=412827)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Networking (简体中文)](/index.php/Category:Networking_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Networking (简体中文)")
*   [简体中文](/index.php/Category:%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87 "Category:简体中文")