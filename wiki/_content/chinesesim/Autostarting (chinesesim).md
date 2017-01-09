**翻译状态：** 本文是英文页面 [Autostarting](/index.php/Autostarting "Autostarting") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-01-09，点击[这里](https://wiki.archlinux.org/index.php?title=Autostarting&diff=0&oldid=462033)可以查看翻译后英文页面的改动。

This article links to various methods to launch scripts or applications automatically when some particular event is taking place, like system startup or shutdown, shell login or logout and so on.

## Contents

*   [1 Daemons](#Daemons)
    *   [1.1 Systemd](#Systemd)
*   [2 Cron](#Cron)
*   [3 Shells](#Shells)
    *   [3.1 /etc/profile](#.2Fetc.2Fprofile)
*   [4 Graphical](#Graphical)
    *   [4.1 X session startup](#X_session_startup)
    *   [4.2 Desktop entries](#Desktop_entries)
    *   [4.3 GNOME](#GNOME)
    *   [4.4 KDE Plasma](#KDE_Plasma)
    *   [4.5 Xfce](#Xfce)
    *   [4.6 LXDE](#LXDE)
    *   [4.7 LXQt](#LXQt)
    *   [4.8 Fluxbox](#Fluxbox)
    *   [4.9 Openbox](#Openbox)

## Daemons

You can start your scripts or applications as daemons, see [Daemon](/index.php/Daemon "Daemon").

### Systemd

*systemd* is the default init framework, replacing initscripts. The services which are started by *systemd* can be found in the subfolders of `/etc/systemd/system/`. Services can be enabled using the `systemctl` command. For more information about *systemd* and how to write autostart scripts for it, see at [systemd](/index.php/Systemd "Systemd"). To autostart scripts for specific users, see [systemd/User](/index.php/Systemd/User "Systemd/User").

## Cron

[Cron](/index.php/Cron "Cron") can be used to autostart non-GUI system setup tasks.

## Shells

To autostart programs in console or upon login, you can use shell startup files/directories. Read the documentation for your shell, or its ArchWiki article, e.g. [Bash#Configuration files](/index.php/Bash#Configuration_files "Bash") or [Zsh#Startup/Shutdown files](/index.php/Zsh#Startup.2FShutdown_files "Zsh").

See also [Wikipedia:Unix shell#Configuration files for shells](https://en.wikipedia.org/wiki/Unix_shell#Configuration_files_for_shells "wikipedia:Unix shell").

### /etc/profile

Upon login, all Bourne-compatible shells source `/etc/profile`, which in turn sources any readable `*.sh` files in `/etc/profile.d/`: these scripts do not require an interpreter directive, nor do they need to be executable. They are used to set up an environment and define application-specific settings.

## Graphical

You can autostart programs automatically when you login into your [Window manager](/index.php/Window_manager "Window manager") or [Desktop environment](/index.php/Desktop_environment "Desktop environment").

### X session startup

See [xinitrc](/index.php/Xinitrc "Xinitrc") and [xprofile](/index.php/Xprofile "Xprofile").

### Desktop entries

See [Desktop entries#Autostart](/index.php/Desktop_entries#Autostart "Desktop entries").

### GNOME

See [GNOME#Startup applications](/index.php/GNOME#Startup_applications "GNOME").

### KDE Plasma

See [KDE#Autostarting applications](/index.php/KDE#Autostarting_applications "KDE").

### Xfce

See [Xfce#Startup applications](/index.php/Xfce#Startup_applications "Xfce").

### LXDE

See [LXDE#Autostart](/index.php/LXDE#Autostart "LXDE").

### LXQt

See [LXQt#Autostarting applications](/index.php/LXQt#Autostarting_applications "LXQt").

### Fluxbox

See [Fluxbox#Autostart programs](/index.php/Fluxbox#Autostart_programs "Fluxbox").

### Openbox

See [Openbox#autostart](/index.php/Openbox#autostart "Openbox").