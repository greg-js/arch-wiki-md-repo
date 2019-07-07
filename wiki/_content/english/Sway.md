*sway* is a compositor for [Wayland](/index.php/Wayland "Wayland") designed to be fully compatible with [i3](/index.php/I3 "I3"). According to [the official website](https://swaywm.org):

	Sway is a tiling Wayland compositor and a drop-in replacement for the i3 window manager for X11\. It works with your existing i3 configuration and supports most of i3's features, plus a few extras.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Starting](#Starting)
    *   [2.1 From a TTY](#From_a_TTY)
    *   [2.2 From a display manager](#From_a_display_manager)
*   [3 Configuration](#Configuration)
    *   [3.1 Keymap](#Keymap)
    *   [3.2 Statusbar](#Statusbar)
    *   [3.3 Wallpaper](#Wallpaper)
    *   [3.4 Input devices](#Input_devices)
    *   [3.5 HiDPI](#HiDPI)
    *   [3.6 Custom keybindings](#Custom_keybindings)
    *   [3.7 Xresources](#Xresources)
    *   [3.8 Run programs natively under Wayland (without Xwayland support)](#Run_programs_natively_under_Wayland_(without_Xwayland_support))
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Autostart on login](#Autostart_on_login)
    *   [4.2 Backlight toggle](#Backlight_toggle)
    *   [4.3 Screen capture](#Screen_capture)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Application launchers](#Application_launchers)
    *   [5.2 VirtualBox](#VirtualBox)
    *   [5.3 Sway socket not detected](#Sway_socket_not_detected)
    *   [5.4 Unable to retrieve socket path](#Unable_to_retrieve_socket_path)
    *   [5.5 Keybindings and keyboard layouts](#Keybindings_and_keyboard_layouts)
*   [6 See also](#See_also)

## Installation

*sway* can be [installed](/index.php/Install "Install") with the [sway](https://www.archlinux.org/packages/?name=sway) package. The development version can be installed using [wlroots-git](https://aur.archlinux.org/packages/wlroots-git/) and [sway-git](https://aur.archlinux.org/packages/sway-git/). It's advisable to always update *wlroots* when you update *sway*, due to tight dependencies.

You may also install [swaylock](https://www.archlinux.org/packages/?name=swaylock) and [swayidle](https://www.archlinux.org/packages/?name=swayidle) to lock your screen and set up an idle manager.

## Starting

**Tip:** See [Wayland#GUI libraries](/index.php/Wayland#GUI_libraries "Wayland") for appropriate environment variables to set for window decoration libraries.

### From a TTY

To start Sway, simply type *sway* from a TTY.

### From a display manager

**Note:** Sway does not support display managers officially.[[1]](https://github.com/swaywm/sway/pull/3634#issuecomment-462779163)

The sway session is located at `/usr/share/wayland-sessions/sway.desktop`. It is automatically recognized by modern display managers like [GDM](/index.php/GDM "GDM") and [SDDM](/index.php/SDDM "SDDM").

Also you can use text-based session manager, see [Display manager#Console](/index.php/Display_manager#Console "Display manager").

## Configuration

If you already use i3, then copy your i3 configuration to `~/.config/sway/config` and it should work out of the box. Otherwise, copy the sample configuration file to `~/.config/sway/config`. It is located at `/etc/sway/config`, unless the `DFALLBACK_CONFIG_DIR` flag has been set. See [sway(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sway.5) for information on the configuration.

### Keymap

By default, sway starts with the US QWERTY keymap. To configure per-input:

 `~/.config/sway/config` 
```
 input * xkb_layout "us,de,ru"
 input * xkb_variant "colemak,,typewriter"
 input * xkb_options "grp:win_space_toggle"
 input "MANUFACTURER1 Keyboard" xkb_model "pc101"
 input "MANUFACTURER2 Keyboard" xkb_model "jp106"

```

More details are available in [xkeyboard-config(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xkeyboard-config.7) and [sway-input(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sway-input.5).

The keymap can also be configured using environment variables (`XKB_DEFAULT_LAYOUT`, `XKB_DEFAULT_VARIANT`, etc.) when starting sway.

### Statusbar

Installing the program [i3status](https://www.archlinux.org/packages/?name=i3status) is an easy way to get a practical, default statusline. All one has to do is add following snippet at the end of your sway config:

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

**Tip:** [waybar](https://www.archlinux.org/packages/?name=waybar) is an alternative to the bar included with sway (swaybar).

### Wallpaper

Since release 1.1.1 the wallpaper part of the SwayWM project was moved to [swaybg](https://www.archlinux.org/packages/?name=swaybg), which is needed in order to run the output command.

This line, which can be appended at the end of your sway configuration, sets a background image on all displays (output matches all with name `"*"`):

 `~/.config/sway/config` 
```
 output "*" bg /home/onny/pictures/fredwang_norway.jpg fill

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
$ swaymsg -t get_inputs

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
$ swaymsg -t get_outputs

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

To control brightness you can use [brightnessctl](https://aur.archlinux.org/packages/brightnessctl/) or [light](https://www.archlinux.org/packages/?name=light). For a list of utilities to control brightness and color correction see [Backlight](/index.php/Backlight "Backlight").

### Xresources

Copy `~/.Xresources` to `~/.Xdefaults` to use them in Sway.

### Run programs natively under Wayland (without Xwayland support)

First, be sure the toolkit or library of every program that is and will be installed [support Wayland](/index.php/Wayland#GUI_libraries "Wayland"). Then append the following line to your sway configuration file to disable Xwayland support:

 `~/.config/sway/config` 
```
xwayland disable

```

**Note:** Some programs, like [Firefox](/index.php/Firefox#Wayland "Firefox"), [bemenu](#Application_launchers) or [Qt5](/index.php/Wayland#Qt_5 "Wayland") based programs, also need specific environment variables set for them to run natively under Wayland.

**Note:** In a fresh Sway install, you need to change the default menu and terminal applications because they depend on Xwayland.

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
$ grim screenshot.png

```

Take a screenshot of a part of the screen:

```
$ grim -g "$(slurp)" screenshot.png

```

Capture a video of the whole screen:

```
$ wf-recorder -o recording.mp4

```

Capture a video of a part of the screen:

```
$ wf-recorder -g "$(slurp)"

```

Example of usage with [grim](https://www.archlinux.org/packages/?name=grim), [slurp](https://www.archlinux.org/packages/?name=slurp) and [wl-clipboard](https://www.archlinux.org/packages/?name=wl-clipboard), screenshot directly with Print button to clipboard.

 `~/.config/sway/config` 
```
bindsym --release Print exec grim -g \"$(slurp)" - | wl-copy

```

## Troubleshooting

### Application launchers

i3-dmenu-desktop, [dmenu](https://www.archlinux.org/packages/?name=dmenu), and [rofi](https://www.archlinux.org/packages/?name=rofi) all function relatively well in Sway, but all run under XWayland and suffer from the same issue where they can become unresponsive if the cursor is moved to a native Wayland window. The reason for this issue is that Wayland clients/windows do not have access to input devices unless they have focus of the screen. The XWayland server is itself a client to the Wayland compositor, so one of its XWayland clients must have focus for it to access user input. However, once one of its clients has focus, it can gather input and make it available to all XWayland clients through the X11 protocol. Hence, moving the cursor to an XWayland window and pressing Escape should fix the issue, and sometimes running `pkill` does too.

[bemenu](https://www.archlinux.org/packages/?name=bemenu) is a native Wayland dmenu replacement which can optionally be combined with [j4-dmenu-desktop](https://aur.archlinux.org/packages/j4-dmenu-desktop/) to provide a Wayland-native combination for launching desktop files (as i3-dmenu-desktop does):

```
j4-dmenu-desktop --dmenu='bemenu -i --nb "#3f3f3f" --nf "#dcdccc" --fn "pango:DejaVu Sans Mono 12"' --term='termite'

```

You may need to set `BEMENU_BACKEND` environment variable to "wayland" if you choose not to disable XWayland.

You can also build your own with a floating terminal and fzf as discussed in a [GitHub issue](https://github.com/swaywm/sway/issues/1367).

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

### Unable to retrieve socket path

Requesting messages from `swaymsg -t` on a tty may return the following message:

```
Unable to retrieve socket path

```

`SWAYSOCK` environment variable is set after launching Sway, therefore a workaround to this error is to request `swaymsg -t [message]` in a terminal inside Sway.

### Keybindings and keyboard layouts

By default, if you are using more than one keyboard layout, e.g. `input * xkb_layout "us,ru"`, bindings may become broken when you switch on some secondary layout.

Thanks to [https://github.com/swaywm/sway/pull/3058](https://github.com/swaywm/sway/pull/3058), all you need is to add `--to-code` key to sensitive `bindsym` lines like this:

```
bindsym --to-code {
  $mod+$left focus left
  $mod+$down focus down
  $mod+$up focus up
  $mod+$right focus right
}

```

## See also

*   [GitHub project](https://github.com/swaywm/sway)
*   [Sway official wiki](https://github.com/swaywm/sway/wiki)
*   [sr.ht git page](https://git.sr.ht/~sircmpwn/sway)
*   [Website](https://swaywm.org)
*   [Announcing the release of sway 1.0](https://drewdevault.com/2019/03/11/Sway-1.0-released.html)