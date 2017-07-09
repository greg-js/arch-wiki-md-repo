*sway* is a compositor for [Wayland](/index.php/Wayland "Wayland") designed to be fully compatible with [i3](/index.php/I3 "I3"). According to [the official website](http://swaywm.org):

	Sway is a drop-in replacement for the i3 window manager, but for Wayland instead of X11\. It works with your existing i3 configuration and supports most of i3's features, and a few extras.

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
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Automatically start on login](#Automatically_start_on_login)
*   [6 Known issues](#Known_issues)
    *   [6.1 Using i3-dmenu-desktop](#Using_i3-dmenu-desktop)
    *   [6.2 Using VirtualBox](#Using_VirtualBox)
    *   [6.3 Sway Socket Not Detected](#Sway_Socket_Not_Detected)
    *   [6.4 Incorrect Monitor Resolution](#Incorrect_Monitor_Resolution)
    *   [6.5 Extraneous cursor after logging in with gdm](#Extraneous_cursor_after_logging_in_with_gdm)
*   [7 See also](#See_also)

## Status

Sway is a work-in-progress so caution is advised. However, the project's creator, [Drew DeVault](https://drewdevault.com/) (aka SirCmpwn) has deemed it ready for regular use.

A detailed accounting of what features have been implemented and what features are still outstanding can be found at the following links:

*   [i3 feature support](https://github.com/SirCmpwn/sway/issues/2#issue-99897933)
*   [IPC feature support](https://github.com/SirCmpwn/sway/issues/98)
*   [i3bar compatibility](https://github.com/SirCmpwn/sway/issues/343)
*   [Airblader fork features](https://github.com/SirCmpwn/sway/issues/307)

## Installation

*sway* can be [installed](/index.php/Installed "Installed") with the [sway](https://www.archlinux.org/packages/?name=sway) package. Alternatively install the [sway-git](https://aur.archlinux.org/packages/sway-git/) package for the latest development version.

## Starting sway

**Tip:** See [Wayland#GUI libraries](/index.php/Wayland#GUI_libraries "Wayland") for appropriate environment variables to set for window decoration libraries.

### From a terminal

You can start sway by simply typing `sway` in a terminal.

### Using a display manager

The sway session is located at `/usr/share/wayland-sessions/sway.desktop`. It is automatically recognized by modern display managers like [GDM](/index.php/GDM "GDM") and [SDDM](/index.php/SDDM "SDDM").

### From X

If you want to start *sway* in an X session for testing purposes it is possible to start it as a regular program.

## Configuration

If you already use i3, then copy your i3 configuration to `~/.config/sway/config` and it should work out of the box. Otherwise, copy the sample configuration file to `~/.config/sway/config`. It is located at `/etc/sway/config`, unless the `DFALLBACK_CONFIG_DIR` flag has been set. See sway(5) for information on the configuration.

### Keymap

By default, sway starts with the US QWERTY keymap. You can override this behaviour by starting sway with

```
$ export XKB_DEFAULT_LAYOUT=gb; export XKB_DEFAULT_VARIANT=colemak; export XKB_DEFAULT_MODEL=pc101; sway

```

This will launch sway with the keyboard set to the Colemak variant of the British keymap with the 101-key keyboard model.

If you are using a display manager, you can not simply prepend the above line to the `sway.desktop` file. As root, create the following file:

 `/usr/bin/sway-gb-ck` 
```
#!/bin/sh
XKB_DEFAULT_LAYOUT=gb XKB_DEFAULT_VARIANT=colemak XKB_DEFAULT_MODEL=pc101 sway
```

Then, create a `sway-gb-ck.desktop` file that starts the above script:

 `/usr/share/wayland-sessions/sway-gb-ck.desktop` 
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

More documentation and options like acceleration profiles can be found in sway-input(5).

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
 bindsym XF86AudioMute exec pactl set-sink-mute $(pacmd list-sinks |awk '/* index:/{print $3}') toggle
 bindsym XF86MonBrightnessDown exec dsplight down 5
 bindsym XF86MonBrightnessUp exec dsplight up 5

```

To control brightness you can use [brightnessctl](https://aur.archlinux.org/packages/brightnessctl/). For a list of utilities to control brightness and color correction see [Backlight](/index.php/Backlight "Backlight").

## Tips and tricks

### Automatically start on login

To start on login to tty1, add the following to your `.bash_profile`:

```
if [[ -z $DISPLAY ]] && [[ $(tty) = /dev/tty1 ]]; then
  exec sway
fi

```

## Known issues

### Using i3-dmenu-desktop

i3-dmenu-desktop is not usable directly from sway, but a patch is available here : [https://github.com/i3/i3/pull/2265/files](https://github.com/i3/i3/pull/2265/files) Unfortunately, the patch cannot be merged because it breaks when used from i3 in some corner cases.

See here for more information: [https://github.com/SirCmpwn/sway/issues/521](https://github.com/SirCmpwn/sway/issues/521)

You can still apply the patch manually through installing [sway-dmenu-desktop](https://aur.archlinux.org/packages/sway-dmenu-desktop/). This creates a new binary called `sway-dmenu-desktop` to be using within sway.

An alternative is to use [j4-dmenu-desktop](https://aur.archlinux.org/packages/j4-dmenu-desktop/), which is advertised as faster than i3-dmenu-desktop.

### Using VirtualBox

Sway doesn't work well (or at all) under VirtualBox.

### Sway Socket Not Detected

Using a `swaymsg` argument, such as `swaymsg -t get_outputs`, will sometimes return the message

```
sway socket not detected.
ERROR: Unable to connect to

```

when run inside a terminal multiplexer (such as gnu screen or tmux). This means `swaymsg` could not connect to the socket provided in your `SWAYSOCK`.

To view what the current value of `SWAYSOCK` is, type:

```
$ env | fgrep SWAYSOCK
SWAYSOCK=/run/user/1000/sway-ipc.1000.4981.sock

```

To work around this problem, you may try attaching to the first available sway socket, and retrying your command:

```
$ export SWAYSOCK=$(ls /run/user/*/sway-ipc.*.sock | head -n 1)

```

To avoid this error, run the command outside of a multiplexer.

### Incorrect Monitor Resolution

Config options such as `output "HDMI-A-1" res 1280x1024` may not successfully change the resolution. The compositor [wlc](https://www.archlinux.org/packages/?name=wlc) is responsible for setting the resolution, and attempts to figure out monitor resolution from the TTY.

You may be able to alter your TTY resolution (thus also altering the WLC and Sway resolution) by passing a kernel parameter such as `video=HDMI-A-1:1280x1024:e` or with with custom edid binaries ([see Kernel Mode Setting](/index.php/Kernel_mode_setting "Kernel mode setting")).

### Extraneous cursor after logging in with gdm

If you use gdm as your login manager, an extraneous cursor will be left after logging in (see [issue #759](https://github.com/SirCmpwn/sway/issues/759)).

The current workaround is to switch to another TTY, and switch back to sway.

## See also

*   [GitHub project](https://github.com/SirCmpwn/sway)
*   [Website](http://swaywm.org)