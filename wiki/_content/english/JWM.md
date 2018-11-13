**JWM** (Joe's Window Manager) is a lightweight [window manager](/index.php/Window_manager "Window manager") for [Xorg](/index.php/Xorg "Xorg") written in [C](https://en.wikipedia.org/wiki/C_(programming_language) "wikipedia:C (programming language)"). It is under active development and maintained by [Joe Wingbermuehle](http://joewing.net/about.html). It is the default window manager base for distributions like [Puppy Linux](http://www.puppylinux.org/) and [Damn Small Linux](http://damnsmalllinux.org/).

## Contents

*   [1 Installation](#Installation)
*   [2 Starting](#Starting)
*   [3 Configuration](#Configuration)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Improve <Tasklist> contrast](#Improve_<Tasklist>_contrast)
    *   [4.2 Logout and refresh](#Logout_and_refresh)
        *   [4.2.1 Reboot and shutdown](#Reboot_and_shutdown)
        *   [4.2.2 Conky](#Conky)
    *   [4.3 Minimal font suggestions](#Minimal_font_suggestions)
    *   [4.4 Manual tiling support](#Manual_tiling_support)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Additional troubleshooting](#Additional_troubleshooting)
    *   [5.2 All windows are transparent using compton](#All_windows_are_transparent_using_compton)
    *   [5.3 Terminal windows do not fully maximize](#Terminal_windows_do_not_fully_maximize)
    *   [5.4 Verify configuration changes](#Verify_configuration_changes)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [jwm](https://www.archlinux.org/packages/?name=jwm) package.

**Warning:** Recent SVN snapshots (e.g. 500) have migrated to Mod key masks (e.g. `H` to `4`).

## Starting

Run `jwm` with [xinit](/index.php/Xinit "Xinit").

## Configuration

Configuration is done via a single [XML](https://en.wikipedia.org/wiki/XML "wikipedia:XML") file. There is native support for customizable panels and buttons, and a [system tray](https://en.wikipedia.org/wiki/Taskbar "wikipedia:Taskbar") dock. A sample configuration file is located at `/etc/system.jwmrc` which can be copied to the user configuration `~/.jwmrc`:

```
$ cp -i /etc/system.jwmrc ~/.jwmrc

```

Edit this file to establish the environment. See [JWM Configuration](http://joewing.net/projects/jwm/config-2.3.html) for a complete list of available tags, attributes and values.

**Note:** The rolling content of JWM Configuration is based on the latest SVN snapshot and may not reflect the options available in the the current release.

## Tips and tricks

### Improve <Tasklist> contrast

Change the default `<Tasklist>` settings to match the improved contrast style of the default `<MenuStyle>` and active `<WindowStyle>`:

```
<TaskListStyle>
    ~~<ActiveForeground>black</ActiveForeground>~~
    ~~<ActiveBackground>gray90:gray70</ActiveBackground>~~
</TaskListStyle>

<TaskListStyle>
    <ActiveForeground>white</ActiveForeground>
    <ActiveBackground>#70849d:#2e3a67</ActiveBackground>
</TaskListStyle>
```

### Logout and refresh

`<Exit/>` (Logout) is the menu command to cleanly log out of the current X server.

`<Restart/>` (Refresh) is the menu command tag which reinitializes the configuration file and updates menus and keybindings accordingly.

`<Restart/>` and `<Exit/>` can be bound to the `Ctrl+Alt` modified keys following the example syntax below:

```
<Key mask="CA" key="r">exec:jwm -restart</Key>
<Key mask="CA" key="e">exec:jwm -exit</Key>

```

#### Reboot and shutdown

A system with [systemd](/index.php/Systemd "Systemd") can be rebooted with the `Restart` and `Poweroff` menu options.

```
<Program label="Restart">systemctl reboot</Program>
<Program label="Poweroff">systemctl poweroff</Program>

```

Alternatively, use `<Key>` to bind the commands to a chosen key.

See [Allow users to shutdown](/index.php/Allow_users_to_shutdown "Allow users to shutdown") for additional information.

#### Conky

[Conky](/index.php/Conky "Conky") can be run within the `<StartupCommand>` to provide the display of various data streams (e.g. battery life and AC adapter status for notebooks). [xfdesktop](https://www.archlinux.org/packages/?name=xfdesktop) may conflict with Conky; workarounds include:

1.  Review the [Conky FAQ](http://conky.sourceforge.net/faq.html) for workarounds in `~/.conkyrc`
2.  `<Group>` Conky and specify the following `<Option>` tags in `~/.jwmrc`:

```
<Group>
    <Class>Conky</Class>
    <Option>nolist</Option>
    <Option>noborder</Option>
    <Option>notitle</Option>
    <Option>sticky</Option>
</Group>
```

### Minimal font suggestions

```
<WindowStyle>
<font>-*-fixed-*-r-*-*-10-*-*-*-*-*-*-*</font>

<TaskListStyle>
<font>-*-fixed-*-r-*-*-13-*-*-*-*-*-*-*</font>

<TrayStyle>
<font>-*-fixed-*-r-*-*-13-*-*-*-*-*-*-*</font>
```

*   Man `xfontsel` and review the [X Logical Font Description](https://en.wikipedia.org/wiki/X_logical_font_description "wikipedia:X logical font description") article for additional details and pattern descriptions.

### Manual tiling support

Tiling support can be added to JWM with the [Poor Man's Tiling Window Manager](https://github.com/TheWanderer/stiler/tree/master). Assuming `manage.py` is part of the local `PATH`, various tiling actions can be assigned to keys, for example:

```
<Key mask="H" key="Up">exec:manage.py swap</Key>
<Key mask="H" key="Down">exec:manage.py cycle</Key>
<Key mask="H" key="Left">exec:manage.py left</Key>
<Key mask="H" key="Right">exec:manage.py right</Key>

```

**Note:** Run the `env` command to list the modified environments of the current user.

## Troubleshooting

### Additional troubleshooting

If X is not already running on `tty1`, `Ctrl+Alt+F1` will allow you to review standard output errors and messages. See [script(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/script.1) command for details on how to create a typescript of what is printed to the terminal.

### All windows are transparent using compton

Adjust the window transparency in `~/.jwmrc`:

```
<Inactive>
  <Opacity>1,0</Opacity>
</Inactive>

```

### Terminal windows do not fully maximize

Add a group with the `iignore` option to `~/.jwmrc`, for example:

```
<Group>
 <Class>URxvt</Class>
 <Option>iignore</Option>
</Group>

```

### Verify configuration changes

To check the JWM configuration and return syntax errors (including associated line numbers), if any, run:

```
$ jwm -p

```

**Note:** Configuration changes are applied after restarting JWM via the `<Restart/>` command, available on the initial root menu. There is no need to restart the X server for changes to apply. Users are recommended to use `jwm -p` between configuration changes to ensure valid markup and a stable environment.

## See also

*   [Joe's Window Manager](http://joewing.net/projects/jwm/index.shtml)
*   [PuppyLinux JoesWindowManager](http://puppylinux.org/wikka/JoesWindowManager)
*   [Puppy Linux JWM themes exchange](http://www.murga-linux.com/puppy/viewtopic.php?t=23260)