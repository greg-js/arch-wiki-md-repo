*sway* is a compositor for [Wayland](/index.php/Wayland "Wayland") designed to be fully compatible with [i3](/index.php/I3 "I3").

> <font color="grey">*Sway is a drop-in replacement for the i3 window manager, but for Wayland instead of X11\. It works with your existing i3 configuration and supports most of i3's features, and a few extras.*</font>
> — swaywm.org

## Contents

*   [1 Status](#Status)
*   [2 Installation](#Installation)
*   [3 Starting sway](#Starting_sway)
    *   [3.1 From a terminal](#From_a_terminal)
    *   [3.2 Using a display manager](#Using_a_display_manager)
    *   [3.3 From X](#From_X)
*   [4 Configuration](#Configuration)
    *   [4.1 Keymap](#Keymap)
    *   [4.2 Statusbar](#Statusbar)
    *   [4.3 Wallpaper](#Wallpaper)
    *   [4.4 Input devices](#Input_devices)
    *   [4.5 HiDPI](#HiDPI)
    *   [4.6 Custom keybindings](#Custom_keybindings)
*   [5 Known issues](#Known_issues)
    *   [5.1 Using i3-dmenu-desktop](#Using_i3-dmenu-desktop)
*   [6 See also](#See_also)

## Status

Sway is a work-in-progress so caution is advised. However, the project's creator, [Drew DeVault](https://drewdevault.com/) (aka SirCmpwn) has deemed ready for regular use.

A detailed accounting of what features have been implemented and what features are still outstanding can be found at the following links:

*   [i3 feature support](https://github.com/SirCmpwn/sway/issues/2#issue-99897933)
*   [IPC feature support](https://github.com/SirCmpwn/sway/issues/98)
*   [i3bar compatibility](https://github.com/SirCmpwn/sway/issues/343)
*   [Airblader fork features](https://github.com/SirCmpwn/sway/issues/307)

## Installation

*sway* can be [installed](/index.php/Installed "Installed") with the [sway](https://www.archlinux.org/packages/?name=sway) package (or [sway-git](https://aur.archlinux.org/packages/sway-git/) for the latest git version). If you already use i3, then copy your i3 configuration to `~/.config/sway/config` and it will work out of the box. Otherwise, copy the sample configuration file to `~/.config/sway/config`. It is located at `/etc/sway/config`, unless the `DFALLBACK_CONFIG_DIR` flag has been set. See the sway(5) [man page](/index.php/Man_page "Man page") for information on the configuration.

## Starting sway

### From a terminal

You can start sway by simply typing `sway` in a terminal.

### Using a display manager

The sway session is located at `/usr/share/wayland-sessions/sway.desktop`. It is automatically recognized by GDM.

### From X

If you want to start *sway* in an X session for testing purposes it is possible to start it as a regular program.

## Configuration

### Keymap

By default, sway starts with the US QWERTY keymap. You can override this behaviour by starting sway with

```
$ XKB_DEFAULT_LAYOUT=gb XKB_DEFAULT_VARIANT=colemak XKB_DEFAULT_MODEL=pc101 sway

```

This will launch sway with the keyboard set to the Colemak variant of the British keymap with the 101-key keyboard model.

If you are using a display manager, you can not simply prepend the above line to the `sway.desktop` file. As root, create the following file:

 `/usr/bin/sway-gb-ck` 
```
#!/bin/sh
XKB_DEFAULT_LAYOUT=gb XKB_DEFAULT_VARIANT=colemak XKB_DEFAULT_MODEL=pc101 sway
```

Then, create a `sway-gb-ck.desktop` file that starts the above script:

 `/usr/share/wayland-sessions/sway.desktop` 
```
[Desktop Entry]
Name=Sway British(Colemak)
Comment=SirCmpwn's Wayland window manager with the British Colemak keyboard layout
Exec=sway-gb-ck
Type=Application
```

### Statusbar

Installing the program [i3status](https://www.archlinux.org/packages/?name=i3status) is an easy way to get a practical, default statusbar. All one has to do is add following snippet at the end of your sway config:

 `~/.config/sway/config` 
```
 bar {
  status_command i3status
 }

```

If you want to achieve colored output of i3status, you can adjust following part in the i3status configuration:

 `~/.config/i3status/config` 
```
general {
        colors = true
        interval = 5
}

```

In both examples, the system-wide installed configuration files has been copied over to the user directory and then modified.

### Wallpaper

This line, which can be appended at the end of your sway configuration, sets a background image on all displays (output matches all with name `"*"`):

 `~/.config/sway/config` 
```
 output "*" background /home/onny/pictures/fredwang_norway.jpg fill

```

Of course you have to replace the file name and path according to your wallpaper.

### Input devices

Its possible to tweak specific input device configurations. For example to enable tap-to-click and natural scolling for a touchpad, add an input block:

 `~/.config/sway/config` 
```
input "2:14:ETPS/2_Elantech_Touchpad" {
    tap enabled
    natural_scroll enabled
}

```

Where as the device identifier can be queried with:

```
swaymsg -t get_inputs

```

The output from the command, sometimes has a "\" to escape symbols like "/" (ie `"2:14:ETPS\/2_Elantech_Touchpad"`) and it needs to be removed.

More documentation and options like acceleration profiles can be found with:

```
man sway-input

```

### HiDPI

Set your displays scale factor with the `output` command in your config file. The scale factor must be an integer, and is usually 2 for HiDPI screens.

```
output <name> scale <factor>

```

You can find your display name with the following command:

```
swaymsg -t get_outputs

```

### Custom keybindings

[Special keys](/index.php/Extra_keyboard_keys "Extra keyboard keys") on your keyboard can be used to execute commands, for example to control your volume or your monitor brightness:

 `~/.config/sway/config` 
```
 bindsym XF86AudioRaiseVolume exec pactl set-sink-volume $(pacmd list-sinks |awk '/* index:/{print $3}') +5%
 bindsym XF86AudioLowerVolume exec pactl set-sink-volume $(pacmd list-sinks |awk '/* index:/{print $3}') -5%
 bindsym XF86AudioToggle exec pactl set-sink-mute $(pacmd list-sinks |awk '/* index:/{print $3}') toggle
 bindsym XF86MonBrightnessDown exec dsplight down 5
 bindsym XF86MonBrightnessUp exec dsplight up 5

```

You many need to change the sound card index to 1 or 2 depending on your system configuration. See [Backlight](/index.php/Backlight "Backlight") for a list of utilities to control brightness and color correction.

## Known issues

### Using i3-dmenu-desktop

i3-dmenu-desktop is not usable directly from sway, but a patch is available here : [https://github.com/i3/i3/pull/2265/files](https://github.com/i3/i3/pull/2265/files) Unfortunately, the patch cannot be merged because it breaks when used from i3 in some corner cases.

See here for more information: [https://github.com/SirCmpwn/sway/issues/521](https://github.com/SirCmpwn/sway/issues/521)

You can still apply the patch manually though:

```
$ wget '[https://patch-diff.githubusercontent.com/raw/i3/i3/pull/2265.patch'](https://patch-diff.githubusercontent.com/raw/i3/i3/pull/2265.patch')
# patch -p0 /usr/bin/i3-dmenu-desktop < 2265.patch

```

## See also

*   [Github project](https://github.com/SirCmpwn/sway)
*   [Website](http://swaywm.org)