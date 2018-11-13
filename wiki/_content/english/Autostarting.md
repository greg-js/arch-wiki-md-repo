Related articles

*   [Daemons](/index.php/Daemons "Daemons")

This article links to various methods to launch scripts or applications automatically when some particular event is taking place.

## Contents

*   [1 On bootup / shutdown](#On_bootup_/_shutdown)
*   [2 On user login / logout](#On_user_login_/_logout)
*   [3 On device plug in / unplug](#On_device_plug_in_/_unplug)
*   [4 On time events](#On_time_events)
*   [5 On filesystem events](#On_filesystem_events)
*   [6 On shell login / logout](#On_shell_login_/_logout)
*   [7 On Xorg startup](#On_Xorg_startup)
*   [8 On desktop environment startup](#On_desktop_environment_startup)
*   [9 On window manager startup](#On_window_manager_startup)

## On bootup / shutdown

Use [systemd](/index.php/Systemd "Systemd") services.

## On user login / logout

Use [systemd/User](/index.php/Systemd/User "Systemd/User") services.

## On device plug in / unplug

Use [udev](/index.php/Udev "Udev") rules.

## On time events

Periodically at certain times, dates or intervals:

*   [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers")
*   [Cron](/index.php/Cron "Cron")

Once at a date and time:

*   [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers")
*   [at](https://www.archlinux.org/packages/?name=at)

## On filesystem events

Use an [inotify](https://en.wikipedia.org/wiki/inotify "wikipedia:inotify") event watcher:

*   [inotify-tools](https://www.archlinux.org/packages/?name=inotify-tools), see [inotifywait(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/inotifywait.1)
*   [Incron](/index.php/Incron "Incron")
*   [fswatch](https://aur.archlinux.org/packages/fswatch/)

## On shell login / logout

See [Command-line shell#Configuration files](/index.php/Command-line_shell#Configuration_files "Command-line shell").

## On Xorg startup

*   [xinitrc](/index.php/Xinitrc "Xinitrc") if you are starting [Xorg](/index.php/Xorg "Xorg") manually with [xinit](/index.php/Xinit "Xinit").
*   [xprofile](/index.php/Xprofile "Xprofile") if you are using a [display manager](/index.php/Display_manager "Display manager").

## On desktop environment startup

Most [desktop environment](/index.php/Desktop_environment "Desktop environment") implement [XDG Autostart](/index.php/XDG_Autostart "XDG Autostart").

If the desktop environments has an article, see its *Autostart* section.

*   [GNOME#Autostart](/index.php/GNOME#Autostart "GNOME")
*   [KDE#Autostart](/index.php/KDE#Autostart "KDE")
*   [Xfce#Autostart](/index.php/Xfce#Autostart "Xfce")
*   [LXDE#Autostart](/index.php/LXDE#Autostart "LXDE")
*   [LXQt#Autostart](/index.php/LXQt#Autostart "LXQt")

## On window manager startup

If the [window manager](/index.php/Window_manager "Window manager") has an article, see its *Autostart* section.

*   [Fluxbox#Autostart](/index.php/Fluxbox#Autostart "Fluxbox")
*   [Openbox#Autostart](/index.php/Openbox#Autostart "Openbox")
*   [Awesome#Autostart](/index.php/Awesome#Autostart "Awesome")