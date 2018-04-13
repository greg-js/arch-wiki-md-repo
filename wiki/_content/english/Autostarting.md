To automatically run programs:

*   on bootup / shutdown, use [systemd](/index.php/Systemd "Systemd")
*   on user login / logout, use [systemd/User](/index.php/Systemd/User "Systemd/User") services
*   periodically at certain times, dates or intervals, use [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers") or [Cron](/index.php/Cron "Cron")
*   once at a date and time, use [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers") or [at](https://www.archlinux.org/packages/?name=at)
*   on filesystem events use an [inotify](https://en.wikipedia.org/wiki/inotify "wikipedia:inotify") event watcher, like [inotify-tools](https://www.archlinux.org/packages/?name=inotify-tools), [incron](https://www.archlinux.org/packages/?name=incron) or [fswatch](https://aur.archlinux.org/packages/fswatch/)
*   on shell login / logout, see the article / documentation of your [shell](/index.php/Shell "Shell")
*   on [Xorg](/index.php/Xorg "Xorg") startup, you can use:
    *   [xinitrc](/index.php/Xinitrc "Xinitrc") if you are starting [Xorg](/index.php/Xorg "Xorg") manually with [xinit](/index.php/Xinit "Xinit")
    *   [xprofile](/index.php/Xprofile "Xprofile") if you are using a [display manager](/index.php/Display_manager "Display manager")
    *   [XDG Autostart](/index.php/XDG_Autostart "XDG Autostart") i.e. place [Desktop entries](/index.php/Desktop_entries "Desktop entries") in specific directories

## Contents

*   [1 Daemons](#Daemons)
    *   [1.1 Systemd](#Systemd)
*   [2 Cron](#Cron)
*   [3 File-system changes](#File-system_changes)
*   [4 Shells](#Shells)
    *   [4.1 /etc/profile](#.2Fetc.2Fprofile)
*   [5 Graphical](#Graphical)
    *   [5.1 X session startup](#X_session_startup)
    *   [5.2 Desktop entries](#Desktop_entries)
    *   [5.3 GNOME](#GNOME)
    *   [5.4 KDE Plasma](#KDE_Plasma)
    *   [5.5 Xfce](#Xfce)
    *   [5.6 LXDE](#LXDE)
    *   [5.7 LXQt](#LXQt)
    *   [5.8 Fluxbox](#Fluxbox)
    *   [5.9 Openbox](#Openbox)
    *   [5.10 Awesome](#Awesome)

## Daemons

You can start your scripts or applications as daemons, see [Daemon](/index.php/Daemon "Daemon").

### Systemd

*systemd* is the default init framework, replacing initscripts. The services which are started by *systemd* can be found in the subfolders of `/etc/systemd/system/`. Services can be enabled using the `systemctl` command. For more information about *systemd* and how to write autostart scripts for it, see at [systemd](/index.php/Systemd "Systemd"). To autostart scripts for specific users, see [systemd/User](/index.php/Systemd/User "Systemd/User").

## Cron

[Cron](/index.php/Cron "Cron") can be used to autostart non-GUI system setup tasks.

## File-system changes

[inotify-tools](https://www.archlinux.org/packages/?name=inotify-tools) can be used to execute commands or scripts on [inotify](https://en.wikipedia.org/wiki/inotify "wikipedia:inotify") events, triggered by file-system changes. See [some examples](https://techarena51.com/index.php/inotify-tools-example/).

Other tools that use the same underlying functionality are [incron](https://www.archlinux.org/packages/?name=incron) and [fswatch](https://aur.archlinux.org/packages/fswatch/).

## Shells

To autostart programs in console or upon login, you can use shell startup files/directories. Read the documentation for your shell, or its ArchWiki article, e.g. [Bash#Configuration files](/index.php/Bash#Configuration_files "Bash") or [Zsh#Startup/Shutdown files](/index.php/Zsh#Startup.2FShutdown_files "Zsh").

See also [Wikipedia:Unix shell#Configuration files](https://en.wikipedia.org/wiki/Unix_shell#Configuration_files "wikipedia:Unix shell").

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

### Awesome

See [Awesome#Autorun programs](/index.php/Awesome#Autorun_programs "Awesome").