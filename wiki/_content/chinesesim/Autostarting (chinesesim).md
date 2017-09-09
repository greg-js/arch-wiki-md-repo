**翻译状态：** 本文是英文页面 [Autostarting](/index.php/Autostarting "Autostarting") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-09-09，点击[这里](https://wiki.archlinux.org/index.php?title=Autostarting&diff=0&oldid=484303)可以查看翻译后英文页面的改动。

文本介绍如何在某个事件发生时，自动运行应用程序，例如在启动、关机、shell 登录或退出时，自动执行程序。

## Contents

*   [1 守护进程](#.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B)
    *   [1.1 Systemd](#Systemd)
*   [2 Cron](#Cron)
*   [3 文件系统变更](#.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E5.8F.98.E6.9B.B4)
*   [4 Shells](#Shells)
    *   [4.1 /etc/profile](#.2Fetc.2Fprofile)
*   [5 图形程序](#.E5.9B.BE.E5.BD.A2.E7.A8.8B.E5.BA.8F)
    *   [5.1 X 会话启动](#X_.E4.BC.9A.E8.AF.9D.E5.90.AF.E5.8A.A8)
    *   [5.2 Desktop entries](#Desktop_entries)
    *   [5.3 GNOME](#GNOME)
    *   [5.4 KDE Plasma](#KDE_Plasma)
    *   [5.5 Xfce](#Xfce)
    *   [5.6 LXDE](#LXDE)
    *   [5.7 LXQt](#LXQt)
    *   [5.8 Fluxbox](#Fluxbox)
    *   [5.9 Openbox](#Openbox)
    *   [5.10 Awesome](#Awesome)

## 守护进程

可以将程序或脚本以 [守护进程](/index.php/Daemon "Daemon") 方式启动。

### Systemd

*systemd* 现在是默认的 init 框架，*systemd* 启动的服务位于 `/etc/systemd/system/` 下的子目录. 可以用 `systemctl` 自动启用服务。更多信息请参考 [systemd](/index.php/Systemd "Systemd"). 要针对某个用户启动脚本，请参考 [systemd/User](/index.php/Systemd/User "Systemd/User").

## Cron

可以用 [Cron](/index.php/Cron "Cron") 自动启动非图形程序。

## 文件系统变更

[inotify-tools](https://www.archlinux.org/packages/?name=inotify-tools) 可以在收到文件系统变更的 [inotify](https://en.wikipedia.org/wiki/inotify "wikipedia:inotify") 事件时执行命令和脚本，示例请参考 [这里](https://techarena51.com/index.php/inotify-tools-example/).

类似的工具还包括 [incron](https://www.archlinux.org/packages/?name=incron) 和 [fswatch](https://aur.archlinux.org/packages/fswatch/).

## Shells

使用 shell 启动文件目录可以在登录时自动执行脚本，请阅读所用 shell 的文档和对应的 ArchWiki 页面，例如 [Bash#Configuration files](/index.php/Bash#Configuration_files "Bash") 或 [Zsh#Startup/Shutdown files](/index.php/Zsh#Startup.2FShutdown_files "Zsh").

参阅： [Wikipedia:Unix shell#Configuration files for shells](https://en.wikipedia.org/wiki/Unix_shell#Configuration_files_for_shells "wikipedia:Unix shell").

### /etc/profile

在登录时，所有 Bourne 兼容的 shell 都会加载 `/etc/profile`, 此文件会加载 `/etc/profile.d/` 目录下的所有可读 `*.sh` 文件，这些文件不需要设置解析器，也不需要可执行权限，通常用来设置环境变量和应用程序相关的设置。

## 图形程序

可以在登录 [窗口管理器](/index.php/Window_manager "Window manager") 或 [桌面环境](/index.php/Desktop_environment "Desktop environment") 时自动执行程序。

### X 会话启动

请参阅 [xinitrc](/index.php/Xinitrc "Xinitrc") 和 [xprofile](/index.php/Xprofile "Xprofile").

### Desktop entries

请参阅 [Desktop entries#Autostart](/index.php/Desktop_entries#Autostart "Desktop entries").

### GNOME

请参阅 [GNOME#Startup applications](/index.php/GNOME#Startup_applications "GNOME").

### KDE Plasma

请参阅 [KDE#Autostarting applications](/index.php/KDE#Autostarting_applications "KDE").

### Xfce

请参阅 [Xfce#Startup applications](/index.php/Xfce#Startup_applications "Xfce").

### LXDE

请参阅 [LXDE#Autostart](/index.php/LXDE#Autostart "LXDE").

### LXQt

请参阅 [LXQt#Autostarting applications](/index.php/LXQt#Autostarting_applications "LXQt").

### Fluxbox

请参阅 [Fluxbox#Autostart programs](/index.php/Fluxbox#Autostart_programs "Fluxbox").

### Openbox

请参阅 [Openbox#autostart](/index.php/Openbox#autostart "Openbox").

### Awesome

请参阅 [Awesome#Autorun programs](/index.php/Awesome#Autorun_programs "Awesome").