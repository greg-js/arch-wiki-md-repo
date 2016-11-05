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

Example of such a script is given below. This includes opening tabs, renaming tabs, splitting shells, and running commands.

```
#!/bin/bash
# Starting yakuake based on user preferences. Information based on [http://forums.gentoo.org/viewtopic-t-873915-start-0.html](http://forums.gentoo.org/viewtopic-t-873915-start-0.html)
# Adding sessions from previous website is broken, use this: [http://pawelkoston.pl/blog/sublime-text-3-cheatsheet-modules-web-develpment/](http://pawelkoston.pl/blog/sublime-text-3-cheatsheet-modules-web-develpment/)

# This line is needed in case yakuake does not accept fcitx inputs.
/usr/bin/yakuake --im /usr/bin/fcitx --inputstyle onthespot &

# gives Yakuake a couple seconds before sending dbus commands
sleep 2      

# Start htop in tab and split to user terminal and run iotop                                                        
TERMINAL_ID_0=$(qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.terminalIdsForSessionId 0)
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 0 "user"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 0 "htop"
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.splitTerminalLeftRight ${TERMINAL_ID_0}
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 1 "iotop

# Start split root sessions (password prompt) top and bottom                                                                                
SESSION_ID_1=$(qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession)
TERMINAL_ID_1=$(qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.terminalIdsForSessionId ${SESSION_ID_1})
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 1 "root"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 2 "su"
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.splitTerminalTopBottom ${TERMINAL_ID_1}
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 3 "su" 

# Start irssi in its own tab.                                                                                          
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 2 "irssi"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 4 "ssh home -t 'tmux attach -t irssi; bash -l'" 

# Start split ssh shells in own tab.                                                                                   
SESSION_ID_2=$(qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession)
TERMINAL_ID_2=$(qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.terminalIdsForSessionId ${SESSION_ID_2})
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 3 "work server"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 5 "ssh work"
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.splitTerminalLeftRight ${TERMINAL_ID_2}
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 6 "ssh work" 

```

### dbus-send instead of qdbus

You can replace *qdbus* bundled with [Qt](/index.php/Qt "Qt") with more common *dbus-send*. For example, to show/hide Yakuake:

```
$ dbus-send  --type=method_call --dest=org.kde.yakuake /yakuake/window org.kde.yakuake.toggleWindowState

```

## See also

*   [Yakuake scripting on coderwall.com](https://coderwall.com/p/kq9ghg/yakuake-scripting)