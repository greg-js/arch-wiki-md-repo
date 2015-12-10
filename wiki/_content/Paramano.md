# Paramano

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Paramano is a Gtk3 application released under the GPL that lets you select your cores' governor or frequency from a tray icon and displays information about your battery graphically. Paramano is designed to be desktop-environment-independent so it depends only on Gtk3, a system tray and sudo. It's a nice addition to Xfce, LXDE, dwm, and so on.

## Contents

*   [1 Short history](#Short_history)
*   [2 Features](#Features)
*   [3 Installation](#Installation)
*   [4 Troubleshooting and tips](#Troubleshooting_and_tips)
*   [5 See also](#See_also)

## Short history

The original version was abandoned at 0.2.x.dev1-3 (sometime during 2009) and eventually failed as `/proc/acpi/` became deprecated. The original project was forked and named trayfreq-archlinux with the aim of bringing trayfreq back into functionality.

It was later renamed to Paramano, initially a nonsense word which turned out to mean 'cuff' in Italian.

## Features

*   Displays an icon that shows you the current CPU frequency as a proportion of the maximum
*   When the CPU icon is right-clicked, it provides a menu of available frequencies and governors to choose.
*   (Optional) Displays a icon that shows you the status of your battery (charging, discharging, charged) and its current charge
*   Hovering over the battery icon gives the estimated time until fully charged/discharged
*   Automatic switching of CPU governor based on AC adapter presence
*   Configuration can be reloaded on-the-fly by sending the `USR1` signal
*   Lightweight and desktop-environment-independent

## Installation

Install [paramano](https://aur.archlinux.org/packages/paramano/)<sup><small>AUR</small></sup> from the AUR. Then optionally edit the configuration file. If you want to have per-user configuration, then create a configuration file in your home directory:

```
$ cp /etc/paramano.conf ~/.paramano.conf

```

Without this, what you change in the next step will be system-wide – it's your choice.

Open the appropriate config file (`/etc/paramano.conf` or `~/.paramano.conf`) with your favourite editor. Everything will be commented out; un-comment what you want to use. Note that, if a default frequency is set, it will override the governor.

## Troubleshooting and tips

A desktop file is installed into `/etc/xdg/autostart/`. It will automatically start once installed. If you do not want it to start automatically, open the start up manager that comes with your desktop environment and uncheck paramano.

If paramano doesn't seem to want to change the governor, it'll be because it's detected that it's not running as root and has tried to use sudo to elevate its privileges. However, it requires that it has passwordless access to run `/usr/bin/paramano-set`. If you have sudo configured such that you type your password to authenticate, you'll need to add this line to `/etc/sudoers`:

```
your_user_name ALL = NOPASSWD: /usr/bin/paramano-set

```

## See also

*   [Paramano main page](https://github.com/phillid/paramano)
*   [Paramano releases](https://github.com/phillid/paramano/releases)
*   [Original Trayfreq Website](http://trayfreq.sourceforge.net)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Paramano&oldid=363954](https://wiki.archlinux.org/index.php?title=Paramano&oldid=363954)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Power management](/index.php/Category:Power_management "Category:Power management")
*   [CPU](/index.php/Category:CPU "Category:CPU")