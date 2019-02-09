*sway* is a compositor for [Wayland](/index.php/Wayland "Wayland") designed to be fully compatible with [i3](/index.php/I3 "I3"). According to [the official website](https://swaywm.org):

	Sway is a drop-in replacement for the i3 window manager, but for Wayland instead of X11\. It works with your existing i3 configuration and supports most of i3's features, and a few extras.

## Contents

*   [1 Status](#Status)
*   [2 Installation](#Installation)
*   [3 Starting](#Starting)
    *   [3.1 From a TTY](#From_a_TTY)
    *   [3.2 From a display manager](#From_a_display_manager)
*   [4 Configuration](#Configuration)
    *   [4.1 Keymap](#Keymap)
    *   [4.2 Statusbar](#Statusbar)
    *   [4.3 Wallpaper](#Wallpaper)
    *   [4.4 Input devices](#Input_devices)
    *   [4.5 HiDPI](#HiDPI)
    *   [4.6 Custom keybindings](#Custom_keybindings)
    *   [4.7 Xresources](#Xresources)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Autostart on login](#Autostart_on_login)
    *   [5.2 Backlight toggle](#Backlight_toggle)
*   [6 Known issues](#Known_issues)
    *   [6.1 Application launchers](#Application_launchers)
    *   [6.2 VirtualBox](#VirtualBox)
    *   [6.3 Sway Socket Not Detected](#Sway_Socket_Not_Detected)
    *   [6.4 Incorrect Monitor Resolution](#Incorrect_Monitor_Resolution)
*   [7 See also](#See_also)

## Status

Sway is a work-in-progress so caution is advised. However, the project's creator, [Drew DeVault](https://drewdevault.com/) (aka SirCmpwn) has deemed it ready for regular use.

A detailed accounting of what features have been implemented and what features are still outstanding can be found at the following links:

*   [i3 feature support](https://github.com/SirCmpwn/sway/issues/2#issue-99897933)
*   [IPC feature support](https://github.com/SirCmpwn/sway/issues/98)
*   [i3bar compatibility](https://github.com/SirCmpwn/sway/issues/343)
*   [Airblader fork features](https://github.com/SirCmpwn/sway/issues/307)

## Installation

*sway* can be [installed](/index.php/Install "Install") with the [sway](https://www.archlinux.org/packages/?name=sway) package. This will install the stable (but abandoned) *0.15* version which is based on the (also abandoned) [wlc](https://github.com/Cloudef/wlc) library.

At the time of writing, *sway 1.0-beta* (based on the new [wlroots](https://github.com/swaywm/wlroots) library) is under active development and quite stable. Install the following two [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") packages instead: [wlroots-git](https://aur.archlinux.org/packages/wlroots-git/) and [sway-git](https://aur.archlinux.org/packages/sway-git/).

It's advisable to always update *wlroots* when you update *sway*, due to tight dependencies.

## Starting

**Tip:** See [Wayland#GUI libraries](/index.php/Wayland#GUI_libraries "Wayland") for appropriate environment variables to set for window decoration libraries.

### From a TTY

To start Sway, simply type *sway* from a TTY.

### From a display manager

**Note:** Sway does not support display managers officially.

The sway session is located at `/usr/share/wayland-sessions/sway.desktop`. It is automatically recognized by modern display managers like [GDM](/index.php/GDM "GDM") and [SDDM](/index.php/SDDM "SDDM").

## Configuration

If you already use i3, then copy your i3 configuration to `~/.config/sway/config` and it should work out of the box. Otherwise, copy the sample configuration file to `~/.config/sway/config`. It is located at `/etc/sway/config`, unless the `DFALLBACK_CONFIG_DIR` flag has been set. See [sway(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sway.5) for information on the configuration.

### Keymap

By default, sway starts with the US QWERTY keymap. You can override this behaviour by starting sway with:

```
$ export XKB_DEFAULT_LAYOUT=gb; export XKB_DEFAULT_VARIANT=colemak; export XKB_DEFAULT_MODEL=pc101; sway

```

This will launch sway with the keyboard set to the Colemak variant of the British keymap with the 101-key keyboard model.

See [alias](/index.php/Alias "Alias") to simplify starting from a tty and [Desktop entries#Modify environment variables](/index.php/Desktop_entries#Modify_environment_variables "Desktop entries") to start [#From a display manager](#From_a_display_manager).

If none of the above worked, you could add:

```
export XKB_DEFAULT_LAYOUT=gb; export XKB_DEFAULT_VARIANT=colemak; export XKB_DEFAULT_MODEL=pc101

```

to either your `.bash_profile` or `.zprofile` (or similar).

If you want multiple keyboard layouts at startup edit `.bash_profile` and add, for example US English and German layouts, switchable by `Mod+Space`:

 `~/.bash_profile` 
```
if [[ -z $DISPLAY ]] && [[ $(tty) = /dev/tty1 ]]; then
  export XKB_DEFAULT_LAYOUT=us,de
  export XKB_DEFAULT_OPTIONS=grp:win_space_toggle
  exec sway
fi

```

Another option for switching keyboard layout is `Alt`+`Shift`: `grp:alt_shift_toggle`.

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

More documentation and options like acceleration profiles can be found in [sway-input(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sway-input.5).

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
 bindsym XF86MonBrightnessDown exec brightnessctl set 5%-
 bindsym XF86MonBrightnessUp exec brightnessctl set +5%

```

To control brightness you can use [brightnessctl](https://aur.archlinux.org/packages/brightnessctl/). For a list of utilities to control brightness and color correction see [Backlight](/index.php/Backlight "Backlight").

### Xresources

Copy `~/.Xresources` to `~/.Xdefaults` to use them in Sway.

## Tips and tricks

### Autostart on login

To start sway from tty1 on login with default US keyboard, edit:

 `~/.bash_profile` 
```
if [[ -z $DISPLAY ]] && [[ $(tty) = /dev/tty1 ]]; then
  XKB_DEFAULT_LAYOUT=us exec sway
fi

```

### Backlight toggle

To turn off (and on) your displays with a key (e.g. `Pause`) bind the following in your Sway `config`:

```
#!/usr/bin/dash
read lcd < /tmp/lcd
    if [ "$lcd" -eq "0" ]; then
        swaymsg "output * dpms on"
        echo 1 > /tmp/lcd
    else
        swaymsg "output * dpms off"
        echo 0 > /tmp/lcd
    fi

```

## Known issues

### Application launchers

i3-dmenu-desktop, [j4-dmenu-desktop](https://aur.archlinux.org/packages/j4-dmenu-desktop/), [dmenu](https://www.archlinux.org/packages/?name=dmenu), and [rofi](https://www.archlinux.org/packages/?name=rofi) all function relatively well in Sway, but all run under XWayland and suffer from the same issue where they can become unresponsive if the cursor is moved to a native Wayland window. Moving the cursor to an XWayland window and pressing Escape should fix the issue, and sometimes running `pkill` does too.

One alternative is [bemenu-git](https://aur.archlinux.org/packages/bemenu-git/), which is a native Wayland dmenu replacement.

The reason for this issue is that Wayland clients/windows do not have access to input devices unless they have focus of the screen. The XWayland server is itself a client to the Wayland compositor, so one of its XWayland clients must have focus for it to access user input. However, once one of its clients has focus, it can gather input and make it available to all XWayland clients through the X11 protocol.

### VirtualBox

Sway doesn't work well (or at all) under [VirtualBox](/index.php/VirtualBox "VirtualBox").

### Sway Socket Not Detected

Using a `swaymsg` argument, such as `swaymsg -t get_outputs`, will sometimes return the message:

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

## See also

*   [GitHub project](https://github.com/SirCmpwn/sway)
*   [sr.ht git page](https://git.sr.ht/~sircmpwn/sway)
*   [Website](https://swaywm.org)