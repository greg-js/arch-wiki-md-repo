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
*   [4 See also](#See_also)

## Installation

*sway* can be [installed](/index.php/Installed "Installed") with the [sway-git](https://aur.archlinux.org/packages/sway-git/) package. If you already use i3, then copy your i3 configuration to `~/.config/sway/config` and it will work out of the box. Otherwise, copy the sample configuration file to `~/.config/sway/config`. It is located at `/etc/sway/config`, unless the `DFALLBACK_CONFIG_DIR` flag has been set. See the sway(5) [man page](/index.php/Man_page "Man page") for information on the configuration.

## Starting sway

### From TTY

You can start sway by simply typing `sway` in the TTY.

### Using a display manager

The sway session is located at `/usr/share/wayland-sessions/sway.desktop`. It is automatically recognized by GDM.

### From X

If you want to start *sway* in an X session for testing purposes it is possible to start it as a regular program.

## Configuration

### Keymap

By default, sway starts with the US keymap. You can override this behaviour by starting sway with

```
$ XKB_DEFAULT_LAYOUT=de sway

```

to get a German keyboard layout, for example.

If you are using a display manager, you can not simply prepend the above line to the `sway.desktop` file. As root, create the following file:

 `/usr/bin/sway-de` 
```
#!/bin/sh
XKB_DEFAULT_LAYOUT=de sway
```

Then, create a `sway-de.desktop` file that starts the above script:

 `/usr/share/wayland-sessions/sway.desktop` 
```
[Desktop Entry]
Name=Sway (German keymap)
Comment=SirCmpwn's Wayland window manager with German keymap
Exec=sway-de
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

### Custom keybindings

Special keys on your keyboard can be used to execute commands, for example to control your volume or your monitor brightness:

 `~/.config/sway/config` 
```
 bindsym XF86AudioRaiseVolume exec pactl set-sink-volume 0 +15%
 bindsym XF86AudioLowerVolume exec pactl set-sink-volume 0 -15%
 bindsym XF86AudioToggle exec pactl set-sink-mute 0 toggle
 bindsym XF86MonBrightnessDown exec dsplight down 5
 bindsym XF86MonBrightnessUp exec dsplight up 5

```

## See also

*   [Github project](https://github.com/SirCmpwn/sway)
*   [Website](http://swaywm.org)