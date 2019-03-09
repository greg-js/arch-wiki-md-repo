Related articles

*   [Conky/Tips_and_tricks](/index.php/Conky/Tips_and_tricks "Conky/Tips and tricks")
*   [Lm_sensors](/index.php/Lm_sensors "Lm sensors")
*   [Hddtemp](/index.php/Hddtemp "Hddtemp")

[Conky](https://en.wikipedia.org/wiki/Conky_(software) is a system monitor software for the X Window System. It is available for GNU/Linux and FreeBSD. It is free software released under the terms of the GPL license. Conky is able to monitor many system variables including CPU, memory, swap, disk space, temperature, top, upload, download, system messages, and much more. It is extremely configurable, however, the configuration can be a little hard to understand. *Conky* is a fork of torsmo.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Dual screen](#Dual_screen)
    *   [2.2 Config file syntax changed](#Config_file_syntax_changed)
*   [3 Fonts](#Fonts)
    *   [3.1 Symbolic Fonts](#Symbolic_Fonts)
*   [4 Autostart](#Autostart)
*   [5 Trouble Shooting](#Trouble_Shooting)
    *   [5.1 Conky starts and doesn't display anything on the screen](#Conky_starts_and_doesn't_display_anything_on_the_screen)
    *   [5.2 Transparency](#Transparency)
        *   [5.2.1 Pseudo-transparency](#Pseudo-transparency)
        *   [5.2.2 Enable real transparency](#Enable_real_transparency)
        *   [5.2.3 Semi-transparency](#Semi-transparency)
    *   [5.3 Do not minimize on Show Desktop](#Do_not_minimize_on_Show_Desktop)
    *   [5.4 Integrate with GNOME Shell](#Integrate_with_GNOME_Shell)
    *   [5.5 Prevent flickering](#Prevent_flickering)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [conky](https://www.archlinux.org/packages/?name=conky) package. There are also alternative packages you can install from [AUR](/index.php/AUR "AUR") with extra compile options enabled:

*   [conky-cli](https://aur.archlinux.org/packages/conky-cli/) - conky without X11 dependencies
*   [conky-lua](https://aur.archlinux.org/packages/conky-lua/) - with Lua support
*   [conky-lua-nv](https://aur.archlinux.org/packages/conky-lua-nv/) - with both Lua and Nvidia support
*   [conky-nvidia](https://aur.archlinux.org/packages/conky-nvidia/) - with Nvidia support

Some built in variables in conky require additional packages to be installed in order to be utilized, for example [Hddtemp](/index.php/Hddtemp "Hddtemp") for hard drive tempurature and [mpd](/index.php/Mpd "Mpd") for music.

Additional utility:

*   **Conky Manager** — Theme manager for Conky widgets. It provides options to start/stop, browse and edit Conky themes installed on the system.

	[http://www.teejeetech.in/p/conky-manager.html](http://www.teejeetech.in/p/conky-manager.html) || [conky-manager](https://www.archlinux.org/packages/?name=conky-manager)

## Configuration

By default conky uses a configuration file located at `~/.config/conky/conky.conf`. You can print out an example configuration with:

```
$ conky --print-config

```

If you prefer to have a configuration [dotfile](/index.php/Dotfile "Dotfile") in home, you can create a file elsewhere and tell conky to use it using arguments.

For example to tell conky to use a dotfile located in the user's home directory:

```
$ conky --config=~/.conky.conf

```

Additional example configuration files are available at [this page](https://github.com/brndnmtthws/conky/wiki/User-Configs).

When editing your config file while conky is running, conky will update with the new changes every time you write to the file.

### Dual screen

When using a dual screen configuration, you will need to play with a few options to place your *conky* window where you want it on the desktop.

By adjusting `gap_x`, let's say you are running a 1680x1050 pixels resolution and you want the window on middle top of your left monitor, you will use:

```
alignment = 'top_left',
gap_X = 840,

```

The `alignment` option is self-explanatory, the `gap_X` is the distance, in pixels, from the left border of your screen.

`xinerama_head` is an alternative useful option, the following will place the *conky* window at the top right of the second screen:

```
alignment = 'top_right',
xinerama_head = 2,

```

### Config file syntax changed

Since Conky 1.10, configuration files have been written with a new [Lua](/index.php/Lua "Lua") syntax, like so:

```
 conky.config = {
   -- Comments start with a double dash
   bool_value = true,
   string_value = 'foo',
   int_value = 42,
 }
 conky.text = [[
 $variable
 ${evaluated variable}
 ]]

```

Some examples below may still use the old syntax, which looks like this:

```
 bool_value yes
 string_value 'foo'
 int_value 42

```

A Lua script is available to convert from the old syntax to the new Lua syntax [here](https://github.com/brndnmtthws/conky/blob/master/extras/convert.lua).

## Fonts

For displaying Unicode pictures and emoji with conky you will need a [font](/index.php/Fonts#Emoji_and_symbols "Fonts") that supports this and then configure conky to use the font with the Unicode you want to display. For example:

```
 ${font Symbola:size=48}☺${font} 

```

### Symbolic Fonts

Symbolic fonts are also very commonly used in more decorated conky configurations, some of the more popular ones include;

*   [ttf-pizzadude-bullets](https://aur.archlinux.org/packages/ttf-pizzadude-bullets/) - PizzaDude Bullet's font
*   [otf-font-awesome-5-free](https://aur.archlinux.org/packages/otf-font-awesome-5-free/) - Font awesome icon from from [http://fontawesome.com/](http://fontawesome.com/)
*   [ttf-weather-icons](https://aur.archlinux.org/packages/ttf-weather-icons/) - Erik flowers weather icon font with 222 glyphs

## Autostart

Conky can be started automatically several different ways, as outlined in "[Autostarting](/index.php/Autostarting "Autostarting")". Choose the one that works best for your window manager/desktop environment.

Conky has a configuration setting which will tell it to fork to the background. This may be desirable for some autostarting setups.

In `conky.conf`:

```
conky.config = {
    background = true,
}

```

If you use a graphical desktop environment and wish to use a `conky.desktop` file for autostarting, use the following:

 `~/.config/autostart/conky.desktop` 
```
[Desktop Entry]
Type=Application
Name=conky
Exec=conky --daemonize --pause=5
StartupNotify=false
Terminal=false
```

The `pause=5` parameter delays *conky'*s drawing for 5 seconds at startup to make sure that the desktop had time to load and is up.

## Trouble Shooting

These are known issues people have with conky and their solutions.

### Conky starts and doesn't display anything on the screen

First check for syntax errors in your configuration file's text variable. Then double check that your user has permission to run every command inside your configuration file and that all needed packages are installed.

### Transparency

Conky supports two different types of transparency. Pseudo-transparency and real transparency that requires a [composite manager](/index.php/Composite_manager "Composite manager") to be installed and running. If you enable real transparency and don't have a composite manager running your conky will not be alpha transparent with transparency enabled for fonts and images as well as the background.

#### Pseudo-transparency

Pseudo-transparency is enabled by default in conky. Pseudo-transparency works by copying the background image from the root window and using the relevant section as the background for conky. Some window managers set the background wallpaper to a level above the root window which can cause conky to have a grey background. To fix this issue you need to set it manually. An example with [feh](/index.php/Feh "Feh") is:

In `~/.xinitrc`:

```
 sleep 1 && feh --bg-center ~/background.png &

```

#### Enable real transparency

To enable real transparency, you must have a [composite manager](/index.php/Composite_manager "Composite manager") running and the following lines added to `.conkyrc` inside the conky.config array:

```
 conky.config = {
    own_window = true,
    own_window_transparent = true,
    own_window_argb_visual = true,
    own_window_type = desktop,
 }

```

If window type "desktop" does not work try changing it to `normal`. If that does not work try the other options: `dock`, `panel`, or `override` instead.

**Note:** [Xfce](/index.php/Xfce "Xfce") requires enabled compositing, see [[1]](https://forum.xfce.org/viewtopic.php?pid=25939).

#### Semi-transparency

To achieve semi-transparency in real transparency mode, the following setup must be used in the conky configuration file:

```
 conky.config = {
    own_window = true,
    own_window_transparent = false,
    own_window_argb_visual = true,
    own_window_argb_value = 90,
    own_window_type = desktop,
 }

```

To reduce the transparency of the conky window, one can increase the value of `own_window_argb_value` towards 255.

### Do not minimize on Show Desktop

**Using Compiz:** If the 'Show Desktop' button or key-binding minimizes Conky along with all other windows, start the Compiz configuration settings manager, go to "General Options" and uncheck the "Hide Skip Taskbar Windows" option.

If you do not use Compiz, try editing `conky.conf` and adding/changing the following line:

```
own_window_type = 'override',

```

or

```
own_window_type = 'desktop',

```

Refer to [conky(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/conky.1) [man page](/index.php/Man_page "Man page") for the exact differences. But the latter option enables you to snap windows to *conky*s border using resize key-binds in e.g. Openbox, which the first one does not.

### Integrate with GNOME Shell

Some have experienced problems with *conky* showing up under [GNOME](/index.php/GNOME "GNOME").

Add these lines to `conky.conf`:

```
own_window = true,
own_window_type = 'desktop',

```

### Prevent flickering

*Conky* needs Double Buffer Extension *(DBE)* support from the X server to prevent flickering because it cannot update the window fast enough without it. It can be enabled with [Xorg](/index.php/Xorg "Xorg") in `/etc/X11/xorg.conf` with `Load "dbe"` line in `"Module"` section. The `xorg.conf` file has been replaced (1.8.x patch upwards) by `/etc/X11/xorg.conf.d` which contains the particular configuration files. *DBE* is loaded automatically as long as it is present within `/usr/lib/xorg/modules`. The list of loaded modules can be checked with `grep LoadModule /var/log/Xorg.0.log`.

To enable double buffering, add the `double_buffer` option to `conky.conf`:

```
 conky.config = {
     double_buffer = true,
 }

```

## See also

*   [Official website](https://github.com/brndnmtthws/conky)
*   [Official Conky variables for configuration](http://conky.sourceforge.net/config_settings.html)
*   [Official Conky objects](http://conky.sourceforge.net/variables.html)
*   [Conky Configs on arch forums](https://bbs.archlinux.org/viewtopic.php?id=39906)
*   [Conky](http://freecode.com/projects/conky/) on [Freecode](https://en.wikipedia.org/wiki/Freecode "wikipedia:Freecode")
*   [#conky](irc://chat.freenode.org/conky) IRC chat channel on [freenode](https://en.wikipedia.org/wiki/Freenode "wikipedia:Freenode")
*   [FAQ](https://github.com/brndnmtthws/conky/wiki/FAQ)