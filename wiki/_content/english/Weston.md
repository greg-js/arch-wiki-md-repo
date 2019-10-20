Weston is the reference implementation of a [Wayland](/index.php/Wayland "Wayland") compositor.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
    *   [3.1 XWayland](#XWayland)
    *   [3.2 High DPI displays](#High_DPI_displays)
    *   [3.3 Shell font](#Shell_font)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Screencast recording](#Screencast_recording)
    *   [4.2 Window switching](#Window_switching)

## Installation

[Install](/index.php/Install "Install") the [weston](https://www.archlinux.org/packages/?name=weston) package.

## Usage

**Tip:** Super (windows key) can be changed, see [weston.ini](#Configuration)

<caption>**Keyboard Shortcuts**</caption>
| Cmd | Action |
| `Ctrl+Alt+Backspace` | Quit Weston |
| `Super+Scroll` (or `PageUp`/`PageDown`) | Zoom in/out of desktop |
| `Super+Tab` | Switch windows |
| `Super+LMB` | Move Window |
| `Super+MMB` | Rotate Window |
| `Super+RMB` | Resize Window |
| `Super+Alt+Scroll` | Change window opacity |
| `Super+k` | Force Kill Active Window |
| `Super+Up/Down` | Switch Prev/Next Workspace |
| `Super+Shift+Up/Down` | Grab Current Window and Switch Workspace |
| `Super+F*n*` | Switch to Workspace *n* (e.g. F2) |
| `Super+s` | Take a screenshot |
| `Super+r` | Record a screencast |

To launch Weston natively (from a TTY) or to run Weston inside a running X session:

```
$ weston

```

Then within Weston, you can run the demos. To launch a terminal emulator:

```
$ weston-terminal

```

To move flowers around the screen:

```
$ weston-flower 

```

To display images:

```
$ weston-image image1.jpg image2.jpg...

```

## Configuration

Weston's outputs differ slightly from those of `xorg.conf` Monitors:

```
$ ls /sys/class/drm
card0
card0-VGA-1
card1
card1-DVI-I-1
card1-HDMI-A-1
card1-VGA-2

```

`card0` is the unused built-in video adapter. The add-on adapter `card1` is cabled to one HDMI and one DVI monitor, so the output names are `HDMI-A-1` and `DVI-I-1`.

Following is an example configuration file. See [weston.ini(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/weston.ini.5) for more.

 `~/.config/weston.ini` 
```
[core]
# xwayland support
xwayland=true

[libinput]
enable-tap=true

[shell]
#background-image=/usr/share/backgrounds/gnome/Aqua.jpg
background-type=scale-crop
background-color=0xff000000
#background-color=0xff002244
#panel-color=0x90ff0000
panel-color=0x00ffffff
panel-position=bottom
#clock-format=none
#animation=zoom
#startup-animation=none
close-animation=none
focus-animation=dim-layer
#binding-modifier=ctrl
num-workspaces=6
locking=false
cursor-theme=Adwaita
cursor-size=24

# tablet options
#lockscreen-icon=/usr/share/icons/gnome/256x256/actions/lock.png
#lockscreen=/usr/share/backgrounds/gnome/Garden.jpg
#homescreen=/usr/share/backgrounds/gnome/Blinds.jpg
#animation=fade

# for Laptop displays
[output]
name=LVDS1
mode=preferred
#mode=1680x1050
#transform=90

#[output]
#name=VGA1
# The following sets the mode with a modeline, you can get modelines for your preffered resolutions using the cvt utility
#mode=173.00 1920 2048 2248 2576 1080 1083 1088 1120 -hsync +vsync
#transform=flipped

#[output]
#name=X1
#mode=1024x768
#transform=flipped-270

# on screen keyboard input method
#[input-method]
#path=/usr/lib/weston/weston-keyboard

[keyboard]
keymap_rules=evdev
#keymap_layout=us,de
#keymap_variant=colemak,
#keymap_options=grp:shifts_toggle
#keymap_options=caps:ctrl_modifier,shift:both_capslock_cancel
repeat-rate=30
repeat-delay=300

# keymap_options from /usr/share/X11/xkb/rules/base.lst
#numlock-on=true

[terminal]
font=monospace
font-size=18

[launcher]
icon=/usr/share/weston/icon_flower.png
path=/usr/bin/weston-flower

[launcher]
icon=/usr/share/icons/gnome/32x32/apps/utilities-terminal.png
path=/usr/bin/weston-terminal --shell=/usr/bin/bash

#[launcher]
#icon=/usr/share/icons/gnome/32x32/apps/utilities-terminal.png
#path=/usr/bin/gnome-terminal

[launcher]
icon=/usr/share/icons/hicolor/32x32/apps/firefox.png
path=MOZ_GTK_TITLEBAR_DECORATION=client /usr/bin/firefox

#[launcher]
#icon=/usr/share/icons/Adwaita/32x32/apps/multimedia-volume-control.png
#path=/usr/bin/st alsamixer -c0

```

Minimal `weston.ini`:

 `~/.config/weston.ini` 
```
[core]
xwayland=true

[keyboard]
keymap_layout=gb

[output]
name=LVDS1
mode=1680x1050
transform=90

[launcher]
icon=/usr/share/icons/gnome/24x24/apps/utilities-terminal.png
path=/usr/bin/weston-terminal

[launcher]
icon=/usr/share/icons/hicolor/24x24/apps/firefox.png
path=/usr/bin/firefox

```

#### XWayland

[Install](/index.php/Install "Install") the [xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland) package.

When you want to run an X application from within Weston, it spins up Xwayland to service the request. The following configuration is shown above:

 `~/.config/weston.ini` 
```
[core]
xwayland=true

```

**Note:** if X is not already configured you may need to configure a keymap: [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg")

### High DPI displays

For [Retina](https://en.wikipedia.org/wiki/Retina_Display "wikipedia:Retina Display") or [HiDPI](/index.php/HiDPI "HiDPI") displays, use:

 `~/.config/weston.ini` 
```
[output]
name=...
scale=2

```

### Shell font

Weston uses the default sans-serif font for window title bars, clocks, etc. See [Font configuration#Replace or set default fonts](/index.php/Font_configuration#Replace_or_set_default_fonts "Font configuration") for instructions on how to change this font.

## Tips and tricks

### Screencast recording

Weston has built-in screencast recording which can be started and stopped by pressing the `Super`+`r` key combination. Screencasts are saved to the file `capture.wcap` in the current working directory of Weston. The WCAP format is a lossless video format specific to Weston, which only records the difference in frames. To be able to play the recorded screencast, the WCAP file will need to be converted to a format which a media player can understand. First, convert the capture to the YUV pixel format:

```
$ wcap-decode --yuv4mpeg2 capture.wcap > capture.y4m

```

The YUV file can then be transcoded to other formats using [FFmpeg](/index.php/FFmpeg "FFmpeg") or [x264](https://www.archlinux.org/packages/?name=x264) (see `x264 -h` for more).

### Window switching

To switch windows with `Super+Space` instead of `Super+Tab` change `KEY_TAB` to `KEY_SPACE` in `desktop-shell/shell.c` and recompile [weston](https://www.archlinux.org/packages/?name=weston).