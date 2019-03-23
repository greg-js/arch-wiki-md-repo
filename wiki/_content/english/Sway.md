*sway* is a compositor for [Wayland](/index.php/Wayland "Wayland") designed to be fully compatible with [i3](/index.php/I3 "I3"). According to [the official website](https://swaywm.org):

	Sway is a tiling Wayland compositor and a drop-in replacement for the i3 window manager for X11\. It works with your existing i3 configuration and supports most of i3's features, plus a few extras.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

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
    *   [5.3 Screen capture](#Screen_capture)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Application launchers](#Application_launchers)
    *   [6.2 VirtualBox](#VirtualBox)
    *   [6.3 Sway socket not detected](#Sway_socket_not_detected)
    *   [6.4 Incorrect monitor resolution](#Incorrect_monitor_resolution)
*   [7 See also](#See_also)

## Status

Sway is 100% compatible with i3, aside from several features that only make sense with X11\. A detailed accounting of completed features can be found at the following links:

*   [i3 feature support](https://github.com/SirCmpwn/sway/issues/2#issue-99897933)
*   [IPC feature support](https://github.com/SirCmpwn/sway/issues/98)
*   [i3bar compatibility](https://github.com/SirCmpwn/sway/issues/343)
*   [Airblader fork features](https://github.com/SirCmpwn/sway/issues/307)

## Installation

*sway* can be [installed](/index.php/Install "Install") with the [sway](https://www.archlinux.org/packages/?name=sway) package. The development version can be installed using [wlroots-git](https://aur.archlinux.org/packages/wlroots-git/) and [sway-git](https://aur.archlinux.org/packages/sway-git/). It's advisable to always update *wlroots* when you update *sway*, due to tight dependencies.

You may also install [swaylock](https://www.archlinux.org/packages/?name=swaylock) and [swayidle](https://www.archlinux.org/packages/?name=swayidle) to lock your screen and set up an idle manager.

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

By default, sway starts with the US QWERTY keymap. To configure per-input:

 `~/.config/sway/config` 
```
 input * xkb_layout us,de,ru"
 input * xkb_variant "colemak,,typewriter"
 input * xkb_options "grp:win_space_toggle"
 input "MANUFACTURER1 Keyboard" xkb_model "pc101"
 input "MANUFACTURER2 Keyboard" xkb_model "jp106"

```

More details are available in [xkeyboard-config(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xkeyboard-config.7) and [sway-input(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sway-input.5).

The keymap can also be configured using environment variables (`XKB_DEFAULT_LAYOUT`, `XKB_DEFAULT_VARIANT`, etc.) when starting sway.

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

Set your displays scale factor with the `output` command in your config file. The scale factor can be fractional, but it is usually 2 for HiDPI screens.

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
 bindsym XF86AudioRaiseVolume exec pactl set-sink-volume @DEFAULT_SINK@ +5%
 bindsym XF86AudioLowerVolume exec pactl set-sink-volume @DEFAULT_SINK@ -5%
 bindsym XF86AudioMute exec pactl set-sink-mute @DEFAULT_SINK@ toggle
 bindsym XF86AudioMicMute exec pactl set-source-mute @DEFAULT_SOURCE@ toggle
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

### Screen capture

Capturing the screen can be done using [grim](https://www.archlinux.org/packages/?name=grim) or [swayshot](https://aur.archlinux.org/packages/swayshot/) for screenshots and [wf-recorder-git](https://aur.archlinux.org/packages/wf-recorder-git/) for video. Optionally, [slurp](https://www.archlinux.org/packages/?name=slurp) can be used to select the part of the screen to capture.

Take a screenshot of the whole screen:

```
grim screenshot.png

```

Take a screenshot of a part of the screen:

```
grim -g "$(slurp)" screenshot.png

```

Capture a video of the whole screen:

```
wf-recorder -o recording.mp4

```

Capture a video of a part of the screen:

```
wf-recorder -g "$(slurp)"

```

Example of usage with [grim](https://www.archlinux.org/packages/?name=grim), [slurp](https://www.archlinux.org/packages/?name=slurp) and [wl-clipboard](https://www.archlinux.org/packages/?name=wl-clipboard), screenshot directly with Print button to clipboard.

```
bindsym --release Print exec grim -g \"$(slurp)" - | wl-copy

```

## Troubleshooting

### Application launchers

i3-dmenu-desktop, [j4-dmenu-desktop](https://aur.archlinux.org/packages/j4-dmenu-desktop/), [dmenu](https://www.archlinux.org/packages/?name=dmenu), and [rofi](https://www.archlinux.org/packages/?name=rofi) all function relatively well in Sway, but all run under XWayland and suffer from the same issue where they can become unresponsive if the cursor is moved to a native Wayland window. Moving the cursor to an XWayland window and pressing Escape should fix the issue, and sometimes running `pkill` does too.

One alternative is [bemenu](https://www.archlinux.org/packages/?name=bemenu), which is a native Wayland dmenu replacement.

Or you can build your own with a floating terminal and fzf (Discussed in an [GitHub Issue](https://github.com/swaywm/sway/issues/1367)).

The reason for this issue is that Wayland clients/windows do not have access to input devices unless they have focus of the screen. The XWayland server is itself a client to the Wayland compositor, so one of its XWayland clients must have focus for it to access user input. However, once one of its clients has focus, it can gather input and make it available to all XWayland clients through the X11 protocol.

### VirtualBox

Sway doesn't work well (or at all) under [VirtualBox](/index.php/VirtualBox "VirtualBox").

### Sway socket not detected

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

To work around this problem, you may try attaching to a socket based on the running sway process:

```
$ export SWAYSOCK=/run/user/$(id -u)/sway-ipc.$(id -u).$(pgrep -x sway).sock

```

To avoid this error, run the command outside of a multiplexer.

### Incorrect monitor resolution

Config options such as `output "HDMI-A-1" res 1280x1024` may not successfully change the resolution. The compositor [wlc](https://www.archlinux.org/packages/?name=wlc) is responsible for setting the resolution, and attempts to figure out monitor resolution from the TTY.

You may be able to alter your TTY resolution (thus also altering the WLC and Sway resolution) by passing a kernel parameter such as `video=HDMI-A-1:1280x1024:e` or with with custom edid binaries (see [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting")).

## See also

*   [GitHub project](https://github.com/SirCmpwn/sway)
*   [sr.ht git page](https://git.sr.ht/~sircmpwn/sway)
*   [Website](https://swaywm.org)
*   [Announcing the release of sway 1.0](https://drewdevault.com/2019/03/11/Sway-1.0-released.html)