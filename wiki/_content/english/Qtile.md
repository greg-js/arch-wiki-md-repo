Related articles

*   [Comparison of tiling window managers](/index.php/Comparison_of_tiling_window_managers "Comparison of tiling window managers")
*   [Window manager](/index.php/Window_manager "Window manager")

From [Qtile web site](http://qtile.org/):

	Qtile is a full-featured, hackable tiling window manager written in Python. Qtile is simple, small, and extensible. It's easy to write your own layouts, widgets, and built-in commands.It is written and configured entirely in Python, which means you can leverage the full power and flexibility of the language to make it fit your needs.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installing](#Installing)
*   [2 Starting](#Starting)
*   [3 Configuration](#Configuration)
    *   [3.1 Groups](#Groups)
    *   [3.2 Keys](#Keys)
        *   [3.2.1 Sound](#Sound)
    *   [3.3 Screens](#Screens)
        *   [3.3.1 Bars and widgets](#Bars_and_widgets)
    *   [3.4 Startup](#Startup)
*   [4 Debugging](#Debugging)
*   [5 See also](#See_also)

## Installing

[Install](/index.php/Install "Install") one of the following packages:

*   [qtile](https://www.archlinux.org/packages/?name=qtile) for the latest official release, running on Python 3.
*   [qtile-python2](https://aur.archlinux.org/packages/qtile-python2/) for the latest official release, running on Python 2.
*   [qtile-python3-git](https://aur.archlinux.org/packages/qtile-python3-git/) for the latest git commit, running on Python 3.
*   [qtile-git](https://aur.archlinux.org/packages/qtile-git/) for the latest git commit, running on Python 2.

## Starting

Run `qtile` with [xinit](/index.php/Xinit "Xinit").

The [default configuration](http://docs.qtile.org/en/latest/manual/config/#default-configuration) includes the shortcut `Super+Enter` to open a new *xterm* terminal, and `Super+Ctrl+q` to quit Qtile.

## Configuration

**Note:** This chapter only explains the basics of the configuration of Qtile. For more complete information, look at the [official documentation](http://docs.qtile.org/en/latest/).

As described in [Configuration Lookup](http://docs.qtile.org/en/latest/manual/config/default.html#configuration-lookup), Qtile provides a default configuration file that will be used in absence of user-defined ones. In order to start customizing Qtile, copy it to `~/.config/qtile/config.py`:

```
$ mkdir -p ~/.config/qtile/
$ cp /usr/share/doc/*qtile_dir*/default_config.py ~/.config/qtile/config.py

```

Where `*qtile_dir*` is the name of the AUR package you [installed](#Installing).

Alternatively, the most recent default configuration file can be downloaded from the git repository at [libqtile/resources/default_config.py](https://github.com/qtile/qtile/blob/master/libqtile/resources/default_config.py).

Several more complete configuration file examples can be found in the [qtile-examples](https://github.com/qtile/qtile-examples) repository.

The configuration is fully done in Python: for a *very* quick introduction to the language you can read [this tutorial](https://developers.google.com/edu/python/introduction).

Before restarting Qtile you can test your configuration file for syntax errors using the command:

```
$ python2 -m py_compile ~/.config/qtile/config.py

```

If the command gives no output, your script is correct.

### Groups

In Qtile, the workspaces (or views) are called **Groups**. They can be defined as following:

```
from libqtile.config import Group, Match
...
groups = [
    Group("term"),
    Group("irc"),
    Group("web", match=Match(title=["Firefox"])),
   ]
...

```

### Keys

You can configure your shortcuts with the **Key** class. Here is an example of the shortcut `Alt+Shift+q` to quit the window manager.

```
from libqtile.config import Key
from libqtile.command import lazy
...
keys = [
    Key(
        ["mod1", "shift"], "q",
        lazy.shutdown())
   ]
...

```

You can find out which `modX` corresponds to which key with the command [Xmodmap](/index.php/Xmodmap "Xmodmap").

#### Sound

You can add shortcuts to easily control the sound volume and state by [adding a user](/index.php/Users_and_groups#Group_management "Users and groups") to the **audio** group and using the `alsamixer` command-line interface.

```
keys= [
    ...
    # Sound
    Key([], "XF86AudioMute", lazy.spawn("amixer -q set Master toggle")),
    Key([], "XF86AudioLowerVolume", lazy.spawn("amixer -c 0 sset Master 1- unmute")),
    Key([], "XF86AudioRaiseVolume", lazy.spawn("amixer -c 0 sset Master 1+ unmute"))
   ]

```

### Screens

Create one **Screen** class for every monitor you have. The bars of Qtile are configured in the **Screen** class as in the following example:

```
from libqtile.config import Screen
from libqtile import bar, widget
...
screens = [
    Screen(
        bottom=bar.Bar([          # add a bar to the bottom of the screen
            widget.GroupBox(),    # display the current Group
            widget.WindowName()   # display the name of the window that currently has focus
            ], 30))
   ]
...

```

#### Bars and widgets

You can find a list of all the built-in widgets in [the official documentation](http://docs.qtile.org/en/latest/manual/ref/widgets.html).

If you want to add a widget to your bar, just add it like in the example above (for the `WindowName` widget). For example, if we want to add a battery notification, we can use the `Battery` widget:

```
from libqtile.config import Screen
from libqtile import bar, widget
...
screens = [
    Screen(top=bar.Bar([
        widget.GroupBox(),    # display the current Group
        widget.Battery()      # display the battery state
       ], 30))
   ]
...

```

### Startup

You can start up applications using **hooks**, specifically the `startup` hook. For a list of available hooks see [the documentation](http://docs.qtile.org/en/latest/manual/ref/hooks.html).

Here is an example where an application starts only once:

```
import os
import subprocess

@hook.subscribe.startup_once
def autostart():
    home = os.path.expanduser('~')
    subprocess.call([home + '/.config/qtile/autostart.sh'])

```

## Debugging

If you want to locate the source of a problem, you can execute the following line in your terminal:

```
echo "exec qtile" > /tmp/.start_qtile ; xinit /tmp/.start_qtile -- :2

```

You can also consult the file in

/home/$USER/.local/share/qtile/qtile.log

## See also

*   [Qtile website](http://qtile.org/)
*   [The official documentation](http://docs.qtile.org/en/latest/)
*   [tilenol](https://github.com/tailhook/tilenol) - A window manager inspired by Qtile.