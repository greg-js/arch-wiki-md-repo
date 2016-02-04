# Sway

_sway_ (SirCmpwn's Wayland window manager) is an attempt to create a [Wayland](/index.php/Wayland "Wayland") version of [i3](/index.php/I3 "I3"), as an alternative to the official i3 Wayland port, i3way.

**Note:** This is still a work in progress so caution is advised. However, it is deemed ready for regular use by the creator.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration examples](#Configuration_examples)
    *   [2.1 Statusbar](#Statusbar)
    *   [2.2 Wallpaper](#Wallpaper)
    *   [2.3 Input devices](#Input_devices)
    *   [2.4 Custom keybindings](#Custom_keybindings)
*   [3 Usage](#Usage)
*   [4 See also](#See_also)

## Installation

_sway_ can be [installed](/index.php/Installed "Installed") with the [sway-git](https://aur.archlinux.org/packages/sway-git/) package. If you already use i3, then copy your i3 configuration to `~/.config/sway/config` and it will work out of the box. Otherwise, copy the sample configuration file to `~/.config/sway/config`. It is located at `/etc/sway/config`, unless the `DFALLBACK_CONFIG_DIR` flag has been set. See the sway(5) [man page](/index.php/Man_page "Man page") for information on the configuration.

## Configuration examples

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

Its possible to tweak specific input device configurations. For example enable tap-to-click for the laptops touchpad, append following line:

 `~/.config/sway/config` 

```
 input "2:14:ETPS/2_Elantech_Touchpad" tap enabled

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

## Usage

To actually use _sway_, you can type in a tty:

```
$ sway

```

However, if you want to start _sway_ in an X session for testing purposes it is possible to start it as a regular program or even from a [Display manager](/index.php/Display_manager "Display manager").

## See also

*   [Github project](https://github.com/SirCmpwn/sway)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Sway&oldid=416066](https://wiki.archlinux.org/index.php?title=Sway&oldid=416066)"