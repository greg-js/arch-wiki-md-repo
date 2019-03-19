[D-Bus](https://en.wikipedia.org/wiki/D-Bus "wikipedia:D-Bus") is a message bus system that provides an easy way for inter-process communication. It consists of a daemon, which can be run both system-wide and for each user session, and a set of libraries to allow applications to use D-Bus.

[dbus](https://www.archlinux.org/packages/?name=dbus) is pulled and installed as a dependency of [systemd](https://www.archlinux.org/packages/?name=systemd) and user session bus is [started automatically](https://www.archlinux.org/news/d-bus-now-launches-user-buses/) for each user.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Alternative Implementations](#Alternative_Implementations)
    *   [1.1 dbus-broker](#dbus-broker)
*   [2 Debugging](#Debugging)
*   [3 See also](#See_also)

## Alternative Implementations

### dbus-broker

[dbus-broker](https://www.archlinux.org/packages/?name=dbus-broker) is a drop-in replacement for the libdbus reference implementation, which aims "to provide high performance and reliability, while keeping compatibility to the D-Bus reference implementation". [[1]](https://github.com/bus1/dbus-broker)

To enable dbus-broker as the system bus:

```
# systemctl enable dbus-broker.service

```

To enable as a user bus, run as the desired user:

```
$ systemctl --user enable dbus-broker.service

```

Or, to enable for all users, run as root:

```
# systemctl --global enable dbus-broker.service

```

Reboot for these settings to take effect.

## Debugging

*   **D-Feet** — Easy to use D-Bus debugger GUI tool. D-Feet can be used to inspect D-Bus interfaces of running programs and invoke methods on those interfaces.

	[https://wiki.gnome.org/Apps/DFeet](https://wiki.gnome.org/Apps/DFeet) || [d-feet](https://www.archlinux.org/packages/?name=d-feet)

*   **QDbusViewer** — GUI D-Bus debugger. Can be used to inspect D-Bus services and invoke methods on them.

	[https://doc.qt.io/qt-5/qdbusviewer.html](https://doc.qt.io/qt-5/qdbusviewer.html) || [qt5-tools](https://www.archlinux.org/packages/?name=qt5-tools)

## See also

*   [D-Bus homepage](https://www.freedesktop.org/wiki/Software/dbus/) – freedesktop.org
*   [Introduction to D-Bus](https://www.freedesktop.org/wiki/IntroductionToDBus/) – freedesktop.org