相关文章

*   [Network configuration](/index.php/Network_configuration "Network configuration")
*   [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")
*   [Netctl](/index.php/Netctl "Netctl")
*   [NetworkManager](/index.php/NetworkManager "NetworkManager")

[Wicd](http://www.wicd.net/)是一个既能管理有线网络又能管理无线网络的网络接入管理器，是 [NetworkManager](/index.php/NetworkManager "NetworkManager") 的一个功能相似的替代。Wicd是用[Python](/index.php/Python_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Python (简体中文)")和[GTK+](/index.php/GTK%2B_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GTK+ (简体中文)")写成的。另外，一个用[Qt](/index.php/Qt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Qt (简体中文)")写成的在[KDE](/index.php/KDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KDE (简体中文)")中工作的版本，可以从 [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")得到。Wicd 也可以从终端中用 curses 界面运行，不需要 X server 会话或者任务面板 (参见 [#运行 Wicd](#运行_Wicd))。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
    *   [1.1 基础软件包](#基础软件包)
    *   [1.2 GTK 客户端](#GTK_客户端)
    *   [1.3 KDE 客户端](#KDE_客户端)
    *   [1.4 通知程序](#通知程序)
    *   [1.5 其他软件包安装方法](#其他软件包安装方法)
*   [2 开始使用](#开始使用)
    *   [2.1 初始设置](#初始设置)
    *   [2.2 运行 Wicd](#运行_Wicd)
*   [3 常见问题解决方法](#常见问题解决方法)
    *   [3.1 GUI 图形界面](#GUI_图形界面)
    *   [3.2 Hidden Wireless Networks and Autoconnection HACK](#Hidden_Wireless_Networks_and_Autoconnection_HACK)
*   [4 相关链接](#相关链接)

## 安装

### 基础软件包

[安装](/index.php/Pacman "Pacman")位于[官方软件仓库](/index.php/Official_repositories "Official repositories")的 [wicd](https://www.archlinux.org/packages/?name=wicd)。这个基础软件包包含了运行 wicd 守护进程所需程序和 `wicd-cli` 和 `wicd-curses` 界面。

### GTK 客户端

使用 GTK 前端，请安装位于[官方软件仓库](/index.php/Official_repositories "Official repositories")的 [wicd-gtk](https://www.archlinux.org/packages/?name=wicd-gtk)。这个软件包提供了 GTK 图形前端和自动启动程序文件。

### KDE 客户端

KDE 前端，请安装[AUR](/index.php/AUR "AUR")中的[wicd-kde](https://aur.archlinux.org/packages/wicd-kde/)。

### 通知程序

要获得网络状态变化的通知，请安装 [notification-daemon](https://www.archlinux.org/packages/?name=notification-daemon).

如果你没有使用 [GNOME](/index.php/GNOME "GNOME")，可以安装 [xfce4-notifyd](https://www.archlinux.org/packages/?name=xfce4-notifyd)已避免安装许多不需要的 GNOME 依赖程序。

### 其他软件包安装方法

[wicd-git](https://aur.archlinux.org/packages/wicd-git/) 是最新的开发版本，如果你要完全定制安装或者制作自己的包，可使用 [ABS](/index.php/ABS "ABS") 编译。

## 开始使用

### 初始设置

Wicd 提供了一个需要启动的守护进程。

**警告:** 使用多种网络管理工具**容易**产生各种问题，因此，请只用一种网络管理工具来管理网络连接。所以，在使用wicd前，必须先**关闭其他网络管理工具**。

首先，使用以下命令手动关闭network、dhcpbd和networkmanager这些守护程序。

```
# systemctl stop netcfg
# systemctl stop dhcpcd@.service
# systemctl stop NetworkManager.service

```

然后，禁用各种网络管理守护进程，包括**network**, **dhcdbd**, 和 **networkmanager**：

```
# systemctl disable netcfg
# systemctl disable dhcpcd@.service
# systemctl disable NetworkManager.service

```

添加服务

```
# systemctl enable wicd.service

```

把你帐号加入到`users`组中，把`$USERNAME`替换成你自己帐号名称。

```
gpasswd -a $USERNAME users

```

**注意:** 可以访问**wicd**的用户组是能更改的，可能不是 *users*. 检查`/etc/dbus-1/system.d/wicd.conf`中指定的用户组,并将你的用户加入该组。

最后，启动**wicd** :

```
# systemctl start wicd

```

如果你添加了自己的用户到新组中，登出再登入。

### 运行 Wicd

命令行输入:

```
$ wicd-client

```

如果你不需要wicd出现在通知区，使用下面命令：

```
$ wicd-client -n

```

**注意:** 这只有在你安装了 wicd-gtk 之后才可以使用。如果你没有安装 wicd-gtk 那么可以使用 wicd-cli 或者 wicd-curses

你也可以把**wicd-client**添加到你所使用的DE/WM 自启动列表中，这样每次登录就能自动启动图形管理界面。

**注意:** 一些用户当使用这种方法会遇到运行两个 `wicd-client` 进程的问题。在 Arch forums 和 Arch bug reports 有关于此的讨论(参见 [#相关链接](#相关链接))。貌似是 wicd 包会在 `/etc/xdg/autostart/wicd-tray.desktop` 放置一个文件，这会在登入桌面环境/窗口管理器时自动启动 wicd-client。如果是这个问题，如果你在桌面环境/窗口管理器的启动文件中添加了一个 `wicd-client` 的话你会有两个 `wicd-client` 同时运行。如果发生这种情况，确认 `wicd-tray.desktop` 文件存在于 `/etc/xdg/autostart`; 如果是，只需要在守护进程列表中有 `wicd` 就可以了。

你也可以在终端中运行 wicd 作为一个 curses 程序：

```
$ wicd-curses

```

**注意:** Wicd 不会向你请求密码。要使用加密连接 (WPA/WEP)，展开你想访问的网络，点击**高级**然后输入必要的信息。

## 常见问题解决方法

### GUI 图形界面

如果在你点击了wicd的状态栏图标后，wicd的GUI没有出现，那么请你确保你是单击了图标而不是双击，因为单击一下图标是显示GUI，再单击一个图标就是关闭GUI，双击正好被程序误认为是开了又关了。

### Hidden Wireless Networks and Autoconnection HACK

I had problems with my hidden network and the autoconnection function of wicd. It seems that the essid of my hidden network is not "<hidden>", but an empty string. Connect manually to the network and run:

```
$ iwlist scan

```

Output of my hidden network:

```
...
wlan0     Scan completed :
          Cell 01 - Address: xx:xx:xx:xx:xx:xx
                    ESSID:""
                    Mode:Master
                    Channel:11
...

```

If you have the same problems and your iwlist output shows ESSID:"", change /usr/lib/wicd/networking.py:

```
cd /usr/lib/wicd
sed -i.orig -e 's/if CurrentNetwork\["essid"\] == "<hidden>":/if CurrentNetwork\["essid"\] \
== "<hidden>" or CurrentNetwork\["essid"\] == "":/' networking.py

```

This changes /usr/lib/wicd/networking.py and saves a backup of the original file to /usr/lib/wicd/networking.py.orig.

Based on wicd version 1.4.1-4

## 相关链接

*   [Note on the network daemon and interfaces](https://bbs.archlinux.org/viewtopic.php?id=40337)
*   [Note on interfaces at the official site](http://www.wicd.net/download.php)
*   [KDE Autostart Issue](http://www.wicd.net/phpbb/viewtopic.php?p=1420)
*   [Common Bugs](http://www.wicd.net/phpbb/viewtopic.php?f=5&t=263&sid=90b13d4cec6ce6109515532267d39ae0&p=2005)