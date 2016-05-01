*sway* (SirCmpwn's Wayland window manager) is an attempt to create a [Wayland](/index.php/Wayland "Wayland") version of [i3](/index.php/I3 "I3").

**Note:** This is still a work in progress so caution is advised. However, it is deemed ready for regular use by the creator.

## Contents

*   [1 Installation](#Installation)
*   [2 Starting sway](#Starting_sway)
    *   [2.1 From TTY](#From_TTY)
    *   [2.2 Using a display manager](#Using_a_display_manager)
    *   [2.3 From X](#From_X)
*   [3 Configuration](#Configuration)
    *   [3.1 Keymap](#Keymap)
    *   [3.2 Statusbar](#Statusbar)
    *   [3.3 Wallpaper](#Wallpaper)
    *   [3.4 Input devices](#Input_devices)
    *   [3.5 Custom keybindings](#Custom_keybindings)
*   [4 Known issues](#Known_issues)
    *   [4.1 Using i3-dmenu-desktop](#Using_i3-dmenu-desktop)
*   [5 See also](#See_also)

## Installation

*sway* can be [installed](/index.php/Installed "Installed") with the [sway](https://www.archlinux.org/packages/?name=sway) package (or [sway-git](https://aur.archlinux.org/packages/sway-git/) for the latest git version). If you already use i3, then copy your i3 configuration to `~/.config/sway/config` and it will work out of the box. Otherwise, copy the sample configuration file to `~/.config/sway/config`. It is located at `/etc/sway/config`, unless the `DFALLBACK_CONFIG_DIR` flag has been set. See the sway(5) [man page](/index.php/Man_page "Man page") for information on the configuration.

## Starting sway

### From TTY

You can start sway by simply typing `sway` in the TTY.

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

Its possible to tweak specific input device configurations. For example to enable tap-to-click for a touchpad, add an input block:

 `~/.config/sway/config` 
```
 input "2:14:ETPS/2_Elantech_Touchpad" {
     tap enabled
 }

```

Where as the device identifier can be queried with:

```
swaymsg -t get_inputs

```

Output from the command, sometimes has "\" to escape some symbols like "/" (ie `"2:14:ETPS\/2_Elantech_Touchpad"`) and need to be removed

More documentation and options like acceleration profiles can be found with

```
man sway-input

```

### Custom keybindings

[Special keys](/index.php/Extra_keyboard_keys "Extra keyboard keys") on your keyboard can be used to execute commands, for example to control your volume or your monitor brightness:

 `~/.config/sway/config` 
```
 bindsym XF86AudioRaiseVolume exec pactl set-sink-volume 0 +15%
 bindsym XF86AudioLowerVolume exec pactl set-sink-volume 0 -15%
 bindsym XF86AudioToggle exec pactl set-sink-mute 0 toggle
 bindsym XF86MonBrightnessDown exec dsplight down 5
 bindsym XF86MonBrightnessUp exec dsplight up 5

```

## Known issues

### Using i3-dmenu-desktop

i3-dmenu-desktop is not usable directly from sway, but a patch is available here : [https://github.com/i3/i3/pull/2265/files](https://github.com/i3/i3/pull/2265/files) Unfortunately, the patch cannot be merged because it breaks when used from i3 in some corner cases.

See here for more information: [https://github.com/SirCmpwn/sway/issues/521](https://github.com/SirCmpwn/sway/issues/521)

You can still apply the patch manually though:

```
$ wget 'https://patch-diff.githubusercontent.com/raw/i3/i3/pull/2265.patch'
# patch -p0 /usr/bin/i3-dmenu-desktop < 2265.patch

```

## See also

*   [Github project](https://github.com/SirCmpwn/sway)
*   [Website](http://swaywm.org)