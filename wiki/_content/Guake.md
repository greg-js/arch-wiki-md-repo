# Guake

[Guake](http://guake.org) is a top-down terminal for [GNOME](/index.php/GNOME "GNOME") (in the style of [Yakuake](/index.php/Yakuake "Yakuake") for [KDE](/index.php/KDE "KDE"), [Tilda](/index.php/Tilda "Tilda") or the terminal used in Quake).

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Autostartup](#Autostartup)
*   [4 Guake scripting](#Guake_scripting)
*   [5 Using Guake on multiple monitors](#Using_Guake_on_multiple_monitors)
*   [6 Throubleshooting](#Throubleshooting)
    *   [6.1 'Ctrl' keybind problem](#.27Ctrl.27_keybind_problem)
    *   [6.2 In Floating WM](#In_Floating_WM)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [guake](https://www.archlinux.org/packages/?name=guake), available in the [official repositories](/index.php/Official_repositories "Official repositories").

## Usage

Once installed, you can start Guake from the terminal with:

```
$ guake

```

After guake has started you can right click on the interface and select _Preferences_ to change the hotkey to drop the terminal automatically, by default it is set to `F12`.

Also, you can adjust many of the Guake preferences with _gconf-editor_ tool under _apps > guake_. If it's not enough for you, you are always free to copy the _guake_ executable (`/usr/bin/guake`) to `/usr/local/bin/guake` and edit it in text editor, since it's just a [Python](/index.php/Python "Python") script. Remember to make the file executable.

## Autostartup

You may want Guake to load on starting up Desktop Environment. To do this, you need to

```
# cp /usr/share/applications/guake.desktop /etc/xdg/autostart/

```

See [Autostarting](/index.php/Autostarting "Autostarting") for more info.

## Guake scripting

Like [Yakuake](/index.php/Yakuake "Yakuake"), Guake allows to control itself at runtime by sending the [D-Bus](/index.php/D-Bus "D-Bus") messages. Thus it can be used to start Guake in a user defined session. You can create tabs, assign names for them and also ask to run any specific command in any opened tab or just to show/hide Guake window, manually in a terminal or by creating a custom script for it.

Example of such a script is given below this section.

You can use _guake_ executable itself to send D-Bus messages. Here is the list of available options you may be interested in:

*   `-t`, `--toggle-visibility` — toggle the visibility of the terminal window. Actually, you can just type `guake`, and it will toggle the visibility of already running instance.
*   `-f`, `--fullscreen` — put Guake to fullscreen mode.
*   `--show` — show Guake main window.
*   `--hide` — hide Guake main window.
*   `-n _CUR_DIR_`, `--new-tab=_CUR_DIR_` — create new tab and select it. Value of `CUR_DIR` used to set a current directory for the tab, if specified.
*   `-s _INDEX_`, `--select-tab=_INDEX_` — select tab with index `INDEX`. Tab indexes are started with 0.
*   `-g`, `--selected-tab` — print index of currently selected tab.
*   `-e _CMD_`, `--execute-command=_CMD_` — execute an arbitrary command `CMD` in the selected tab.
*   `-i _INDEX_`, `--tab-index=_INDEX_` — used with `--rename-tab` to specify index `INDEX` of a tab to rename. Default value is 0.
*   `--rename-tab=_TITLE_` — set the tab name to `TITLE`. You can reset tab title to default value by passing a single dash (`"-"`). Use `-i` option to specify which tab to rename.
*   `--bgcolor=_RGB_` — set the hexadecimal (`#rrggbb`) background color `RGB` of the selected tab.
*   `--fgcolor=_RGB_` — set the hexadecimal (`#rrggbb`) foreground color `RGB` of the selected tab.
*   `-r _TITLE_`, `--rename-current-tab=_TITLE_` — same as `--rename-tab`, but renames the currently selected tab.
*   `-q`, `--quit` — shutdown running Guake instance.

Multiple options may be combined in a single call. If there's no guake instance running, all of the options specified will be applied to the newly created instance.

To display list of all available options, type `guake --help`.

Example:

```
#!/bin/bash

/usr/bin/guake &
sleep 5 # let main guake process start and initialize D-Bus session

# adjust tab which was opened by default
guake --rename-tab="iotop" --execute="/usr/bin/iotop"

# create new tab, start bash session in it
guake --new-tab --execute="/usr/bin/bash"
# and then execute htop, renaming the tab to "htop"
guake --execute="/usr/bin/htop" --rename-tab="htop"

# ...
guake --new-tab --execute="/usr/bin/bash"
guake --execute="/usr/bin/atop" --rename-tab="atop"

guake --new-tab --execute="/usr/bin/bash"
guake --execute="~/.iptables.sh" --rename-tab="iptables -nvL"

guake --new-tab --execute="/usr/bin/bash"
guake --execute="/usr/bin/journalctl --follow --full" --rename-tab="journalctl"

guake --new-tab --execute="/usr/bin/bash"
guake --execute="/usr/bin/irssi" --rename-tab="irssi"

guake --new-tab --execute="/usr/bin/bash"
guake --execute="/usr/bin/sudo -i" --rename-tab="rootshell0"

guake --new-tab --execute="/usr/bin/bash"
guake --execute="/usr/bin/sudo -i" --rename-tab="rootshell1"

guake --new-tab --execute="/usr/bin/bash"
guake --rename-tab="shell0"

guake --new-tab --execute="/usr/bin/bash"
guake --rename-tab="shell1"

```

Notice than we should wait some time calling _sleep_ to avoid race conditions between running instances.

## Using Guake on multiple monitors

There are two GConf options allowing you to change the screen on which Guake window will appear:

*   `/apps/guake/general/display_n` — display to appear on if the `mouse_display` option is not set. If this is set to an invalid value (as in the case of removing a screen from a system), the invalid value is automatically updated to the current primary screen.

*   `/apps/guake/general/mouse_display` — appear on the mouse display. This overrides any setting in `display_n`.

Use some tool like _gconf-editor_ to edit GConf options.

## Throubleshooting

### 'Ctrl' keybind problem

As of [guake](https://www.archlinux.org/packages/?name=guake) 0.4.2-7 there has been a noted bug affecting multiple users concerning the use of the `Ctrl` key to toggle Guake window visibility (i.e. users that setup `Ctrl+Shift+z` to open the guake console are able to open it by just pressing `Shift+z`, independent on whether `Ctrl` key has been pressed).

To solve the problem you should manually fix the value of the GConf key `/apps/guake/keybindings/global/show_hide`. Open a _gconf-editor_, navigate to _apps > guake > keybindings > global > show_hide_ and replace `<Primary>` with `<Control>`.

### In Floating WM

If you are using Tilda and a floating WM, you may find out that you can use class string "Tilda" to set the window keep floating. But that Guake's WM_CLASS(STRING)'s out put is "Main.py", so you should use "Main.py" to do this. For example, in i3wm, add this to your .i3/config:

```
for_window [class="Main.py"] floating enable

```

## See also

*   [man guake(1)](http://linux.die.net/man/1/guake) on die.net

Retrieved from "[https://wiki.archlinux.org/index.php?title=Guake&oldid=412246](https://wiki.archlinux.org/index.php?title=Guake&oldid=412246)"