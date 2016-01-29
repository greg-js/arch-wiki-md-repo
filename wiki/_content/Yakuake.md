# Yakuake

Related articles

*   [KDE](/index.php/KDE "KDE")

[Yakuake](http://yakuake.kde.org/) is a top-down terminal for [KDE](/index.php/KDE "KDE") (in the style of [Guake](/index.php/Guake "Guake") for [GNOME](/index.php/GNOME "GNOME"), [Tilda](/index.php/Tilda "Tilda") or the terminal used in Quake).

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Yakuake scripting](#Yakuake_scripting)
    *   [3.1 dbus-send instead of qdbus](#dbus-send_instead_of_qdbus)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [yakuake](https://www.archlinux.org/packages/?name=yakuake), available in the [official repositories](/index.php/Official_repositories "Official repositories").

## Usage

Once installed, you can start Yakuake from the terminal with:

```
$ yakuake

```

After yakuake has started you can click on configure yakuake by clicking on the "Open Menu" button (middle button on the bottom right hand side of the interface) and select "Configure Shortcuts" to change the hotkey to drop/retract the terminal automatically, by default it is set to F12.

## Yakuake scripting

Like [Guake](/index.php/Guake "Guake"), Yakuake allows to control itself at runtime by sending the [D-Bus](/index.php/D-Bus "D-Bus") messages. Thus it can be used to start Yakuake in a user defined session. You can create tabs, assign names for them and also ask to run any specific command in any opened tab or just to show/hide Yakuake window, manually in a terminal or by creating a custom script for it.

Example of such a script is given below.

```
#!/bin/bash
# Starting yakuake based on user preferences. Information based on [http://forums.gentoo.org/viewtopic-t-873915-start-0.html](http://forums.gentoo.org/viewtopic-t-873915-start-0.html)
# Adding sessions from previous website is broken, use this: [http://pawelkoston.pl/blog/sublime-text-3-cheatsheet-modules-web-develpment/](http://pawelkoston.pl/blog/sublime-text-3-cheatsheet-modules-web-develpment/)
# This line is needed in case yakuake does not accept fcitx inputs.
/usr/bin/yakuake --im /usr/bin/fcitx --inputstyle onthespot

# Start iotop in its own tab.
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 0 "iotop" 
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 0 "iotop"

# Start htop in its own tab.
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 1 "htop"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 1 "htop"

# Start atop in its own tab.
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 2 "atop"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 2 "atop"

# Start (watching) iptables in its own tab.
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 3 "iptables -nvL"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 3 "~/.iptables.sh"

# Start journalctl --follow --full in its own tab.
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 4 "journalctl"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 4 "journalctl --follow --full"

# Start irssi in its own tab.
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 5 "irssi"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 5 "irssi"

# Start root shell 1 in its own tab.
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 6 "rootshell0"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 6 "sudo -i"

# Start root shell 2 in its own tab.
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 7 "rootshell1"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 7 "sudo -i"

# Start shell 1 in its own tab.
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 8 "shell0"

# Start shell 2 in its own tab.
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 9 "shell1"

# Kill default (and now redundant) new shell tab. Already there are two shells each opened for both root and user.
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.removeSession 10

```

### dbus-send instead of qdbus

You can replace _qdbus_ bundled with [Qt](/index.php/Qt "Qt") with more common _dbus-send_. For example, to show/hide Yakuake:

```
$ dbus-send  --type=method_call --dest=org.kde.yakuake /yakuake/window org.kde.yakuake.toggleWindowState

```

## See also

*   [Yakuake scripting on coderwall.com](https://coderwall.com/p/kq9ghg/yakuake-scripting)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Yakuake&oldid=412226](https://wiki.archlinux.org/index.php?title=Yakuake&oldid=412226)"