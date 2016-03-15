**翻译状态：** 本文是英文页面 [D-Bus](/index.php/D-Bus "D-Bus") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-12-05，点击[这里](https://wiki.archlinux.org/index.php?title=D-Bus&diff=0&oldid=285212)可以查看翻译后英文页面的改动。

[D-Bus](https://en.wikipedia.org/wiki/D-Bus "wikipedia:D-Bus") 是一个提供简便进程间通信的消息总线系统。包含一个能以全系统或者针对一个用户会话运行的守护进程，和一系列提供与 D-Bus 通信的库。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 启动用户会话](#.E5.90.AF.E5.8A.A8.E7.94.A8.E6.88.B7.E4.BC.9A.E8.AF.9D)
*   [3 调试](#.E8.B0.83.E8.AF.95)
*   [4 参阅](#.E5.8F.82.E9.98.85)

## 安装

因为[systemd](/index.php/Systemd "Systemd")依赖[dbus](https://www.archlinux.org/packages/?name=dbus),在使用 systemd 时，D-Bus 会被自动启动。如果需要[xinitrc](/index.php/Xinitrc "Xinitrc") dbus 文件，可以选择从[官方软件仓库](/index.php/Official_repositories "Official repositories")安装软件包 [dbus](https://www.archlinux.org/packages/?name=dbus)。

## 启动用户会话

[桌面环境](/index.php/Desktop_environment "Desktop environment") 和 xinitrc 会自动启动 D-Bus 会话。 [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit) 提供的框架文件 `~/.xinitrc` (`/etc/skel/.xinitrc`) 也会执行同样的操作。请确保自己的 `~/.[xinitrc](/index.php/Xinitrc "Xinitrc")` 是基于框架文件 `/etc/skel/.xinitrc`.

## 调试

[d-feet](https://www.archlinux.org/packages/?name=d-feet) 是方便易用的 D-Bus 图形调试工具。D-Feet 可以查看运行程序的 D-Bus 接口，并执行接口中对应的指令。详情参阅interfaces of running programs and invoke methods on those interfaces. See [主页](https://wiki.gnome.org/DFeet) 。

## 参阅

*   [freedesktop.org 上的 D-Bus](http://www.freedesktop.org/wiki/Software/dbus)