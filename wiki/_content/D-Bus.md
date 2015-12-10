# D-Bus

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Mention disabling of dbus services through use of `systemctl mask` and overrides in `/etc/dbus-1/services` (Discuss in [Talk:D-Bus#](https://wiki.archlinux.org/index.php/Talk:D-Bus))

Related articles

*   [kdbus](/index.php/Kdbus "Kdbus")

[D-Bus](https://en.wikipedia.org/wiki/D-Bus "wikipedia:D-Bus") is a message bus system that provides an easy way for inter-process communication. It consists of a daemon, which can be run both system-wide and for each user session, and a set of libraries to allow applications to use D-Bus.

## Contents

*   [1 Installation](#Installation)
*   [2 Starting the user session](#Starting_the_user_session)
*   [3 Debugging](#Debugging)
*   [4 See also](#See_also)

## Installation

D-Bus is enabled automatically when using [systemd](/index.php/Systemd "Systemd") because [dbus](https://www.archlinux.org/packages/?name=dbus) is a dependency of systemd.

## Starting the user session

As of [systemd](https://www.archlinux.org/packages/?name=systemd) `226-1` and [dbus](https://www.archlinux.org/packages/?name=dbus) `1.10.0-3`, the D-Bus session is started automatically. [[1]](https://www.archlinux.org/news/d-bus-now-launches-user-buses/)

## Debugging

[d-feet](https://www.archlinux.org/packages/?name=d-feet) is an easy to use D-Bus debugger GUI tool. D-Feet can be used to inspect D-Bus interfaces of running programs and invoke methods on those interfaces. See [its homepage](https://wiki.gnome.org/DFeet) for more info.

## See also

*   [D-Bus page at freedesktop.org](http://www.freedesktop.org/wiki/Software/dbus)
*   [Introduction to D-Bus](http://www.freedesktop.org/wiki/IntroductionToDBus) on freedesktop.org

Retrieved from "[https://wiki.archlinux.org/index.php?title=D-Bus&oldid=401198](https://wiki.archlinux.org/index.php?title=D-Bus&oldid=401198)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Daemons and system services](/index.php/Category:Daemons_and_system_services "Category:Daemons and system services")