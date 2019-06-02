Related articles

*   [Daemons (简体中文)](/index.php/Daemons_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Daemons (简体中文)")

**翻译状态：** 本文是英文页面 [Autostarting](/index.php/Autostarting "Autostarting") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-06-01，点击[这里](https://wiki.archlinux.org/index.php?title=Autostarting&diff=0&oldid=574197)可以查看翻译后英文页面的改动。

本文介绍在某个特定事件发生时（如启动、关机）如何自动执行脚本或应用的方法。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 开关机](#开关机)
*   [2 登录登出](#登录登出)
*   [3 插入拔出设备](#插入拔出设备)
*   [4 计时事件](#计时事件)
*   [5 文件系统事件](#文件系统事件)
*   [6 shell登录登出](#shell登录登出)
*   [7 Xorg](#Xorg)
*   [8 桌面环境](#桌面环境)
*   [9 窗口管理启动](#窗口管理启动)

## 开关机

用 [systemd (简体中文)](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)") 服务。

## 登录登出

用 [systemd/User (简体中文)](/index.php/Systemd/User_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd/User (简体中文)") 服务。

## 插入拔出设备

用 [udev (简体中文)](/index.php/Udev_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Udev (简体中文)")

## 计时事件

在特定时间、日期、场合执行脚本或应用：

*   [systemd/Timers (简体中文)](/index.php/Systemd/Timers_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd/Timers (简体中文)")
*   [Cron (简体中文)](/index.php/Cron_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Cron (简体中文)")

只执行一次:

*   [systemd/Timers (简体中文)](/index.php/Systemd/Timers_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd/Timers (简体中文)")
*   [at](https://www.archlinux.org/packages/?name=at)

## 文件系统事件

用 [inotify](https://en.wikipedia.org/wiki/inotify "wikipedia:inotify") 事件监视器:

*   [inotify-tools](https://www.archlinux.org/packages/?name=inotify-tools), see [inotifywait(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/inotifywait.1)
*   [Incron](/index.php/Incron "Incron")
*   [fswatch](https://aur.archlinux.org/packages/fswatch/)

## shell登录登出

参考 [Command-line shell#Configuration files (简体中文)](/index.php/Command-line_shell#Configuration_files_(简体中文) "Command-line shell")。

## Xorg

*   [xinitrc (简体中文)](/index.php/Xinitrc_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xinitrc (简体中文)") if you are starting [Xorg (简体中文)](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)") manually with [xinit (简体中文)](/index.php/Xinit_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xinit (简体中文)").
*   [xprofile (简体中文)](/index.php/Xprofile_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xprofile (简体中文)") if you are using a [display manager (简体中文)](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)").

## 桌面环境

大多数 [desktop environment (简体中文)](/index.php/Desktop_environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop environment (简体中文)") 依赖 [XDG Autostart](/index.php/XDG_Autostart "XDG Autostart").

查看与自动启动相关的信息。

*   [GNOME#Autostart (简体中文)](/index.php/GNOME#Autostart_(简体中文) "GNOME")
*   [KDE#Autostart (简体中文)](/index.php/KDE#Autostart_(简体中文) "KDE")
*   [Xfce#Autostart (简体中文)](/index.php/Xfce#Autostart_(简体中文) "Xfce")
*   [LXDE#Autostart (简体中文)](/index.php/LXDE#Autostart_(简体中文) "LXDE")
*   [LXQt#Autostart (简体中文)](/index.php/LXQt#Autostart_(简体中文) "LXQt")

## 窗口管理启动

许多[window manager (简体中文)](/index.php/Window_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Window manager (简体中文)") 依赖 [XDG Autostart](/index.php/XDG_Autostart "XDG Autostart").

查看与窗口管理有关的信息。

*   [Fluxbox#Autostart (简体中文)](/index.php/Fluxbox#Autostart_(简体中文) "Fluxbox")
*   [Openbox#Autostart (简体中文)](/index.php/Openbox#Autostart_(简体中文) "Openbox")
*   [Awesome#Autostart (简体中文)](/index.php/Awesome#Autostart_(简体中文) "Awesome")
*   [i3#Autostart (简体中文)](/index.php/I3#Autostart_(简体中文) "I3")