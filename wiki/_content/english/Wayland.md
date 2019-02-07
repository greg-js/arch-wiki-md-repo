Related articles

*   [KMS](/index.php/KMS "KMS")
*   [Xorg](/index.php/Xorg "Xorg")

[Wayland](http://wayland.freedesktop.org/) is a protocol for a [compositing window manager](https://en.wikipedia.org/wiki/Compositing_window_manager "wikipedia:Compositing window manager") to talk to its clients, as well as a library implementing the protocol. It is supported on some desktop environments like [GNOME](/index.php/GNOME "GNOME") and [KDE](/index.php/KDE "KDE"). There is also a compositor reference implementation called Weston. XWayland provides a compatibility layer to seamlessly run legacy [X11](/index.php/X11 "X11") applications in Wayland.

## Contents

*   [1 Requirements](#Requirements)
*   [2 Weston](#Weston)
    *   [2.1 Installation](#Installation)
    *   [2.2 Usage](#Usage)
    *   [2.3 Configuration](#Configuration)
        *   [2.3.1 XWayland](#XWayland)
        *   [2.3.2 High DPI displays](#High_DPI_displays)
        *   [2.3.3 Shell font](#Shell_font)
    *   [2.4 Tips and tricks](#Tips_and_tricks)
        *   [2.4.1 Screencast recording](#Screencast_recording)
        *   [2.4.2 Window switching](#Window_switching)
*   [3 GUI libraries](#GUI_libraries)
    *   [3.1 GTK+ 3](#GTK+_3)
    *   [3.2 Qt 5](#Qt_5)
    *   [3.3 Clutter](#Clutter)
    *   [3.4 SDL2](#SDL2)
    *   [3.5 GLFW](#GLFW)
    *   [3.6 GLEW](#GLEW)
    *   [3.7 EFL](#EFL)
*   [4 Compositors](#Compositors)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Gamma](#Gamma)
    *   [5.2 LLVM assertion failure](#LLVM_assertion_failure)
    *   [5.3 Slow motion, graphical glitches, and crashes](#Slow_motion,_graphical_glitches,_and_crashes)
    *   [5.4 GNOME Wayland on tty1, Weston on tty2](#GNOME_Wayland_on_tty1,_Weston_on_tty2)
    *   [5.5 Electron based applications / VS Code](#Electron_based_applications_/_VS_Code)
    *   [5.6 Screen recording](#Screen_recording)
    *   [5.7 Remote display](#Remote_display)
    *   [5.8 Input grabbing in games, remote desktop and VM windows](#Input_grabbing_in_games,_remote_desktop_and_VM_windows)
        *   [5.8.1 wlroots input inhibitor protocol](#wlroots_input_inhibitor_protocol)
*   [6 See also](#See_also)

## Requirements

Most Wayland compositors only work on systems using [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting"). Wayland by itself does not provide a graphical environment; for this you also need a compositor such as [#Weston](#Weston) or [Sway](/index.php/Sway "Sway"), or a desktop environment that includes a compositor like [GNOME](/index.php/GNOME "GNOME") or [KDE](/index.php/KDE "KDE").

For the GPU driver and Wayland compositor to be compatible they must support the same buffer API. There are two main APIs: [GBM](https://en.wikipedia.org/wiki/Generic_Buffer_Management "wikipedia:Generic Buffer Management") and [EGLStreams](http://www.phoronix.com/scan.php?page=news_item&px=XDC2016-Device-Memory-API).

| Buffer API | GPU driver support | Wayland compositor support |
| GBM | All except [NVIDIA](/index.php/NVIDIA "NVIDIA") | All |
| EGLStreams | [NVIDIA](/index.php/NVIDIA "NVIDIA") | [GNOME](/index.php/GNOME "GNOME"), Grefsen, [Sway](/index.php/Sway "Sway") ([will be removed](https://drewdevault.com/2017/10/26/Fuck-you-nvidia.html)) |

## Weston

Weston is the reference implementation of a Wayland compositor.

### Installation

[Install](/index.php/Install "Install") the [weston](https://www.archlinux.org/packages/?name=weston) package.

### Usage

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

### Configuration

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
enable_tap=true

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

#### High DPI displays

For [Retina](https://en.wikipedia.org/wiki/Retina_Display "wikipedia:Retina Display") or [HiDPI](/index.php/HiDPI "HiDPI") displays, use:

 `~/.config/weston.ini` 
```
[output]
name=...
scale=2

```

#### Shell font

Weston uses the default sans-serif font for window title bars, clocks, etc. See [Font configuration#Replace or set default fonts](/index.php/Font_configuration#Replace_or_set_default_fonts "Font configuration") for instructions on how to change this font.

### Tips and tricks

#### Screencast recording

Weston has built-in screencast recording which can be started and stopped by pressing the `Super`+`r` key combination. Screencasts are saved to the file `capture.wcap` in the current working directory of Weston. The WCAP format is a lossless video format specific to Weston, which only records the difference in frames. To be able to play the recorded screencast, the WCAP file will need to be converted to a format which a media player can understand. First, convert the capture to the YUV pixel format:

```
$ wcap-decode --yuv4mpeg2 capture.wcap > capture.y4m

```

The YUV file can then be transcoded to other formats using [FFmpeg](/index.php/FFmpeg "FFmpeg") or [x264](https://www.archlinux.org/packages/?name=x264) (see `x264 -h` for more).

#### Window switching

To switch windows with `Super`+`Space` instead of `Super`+`Tab` use the following patch:

```
diff --git a/shell.c b/shell.c
index 9a44715..348a576 100644
--- a/shell.c
+++ b/shell.c
@@ -4510,7 +4510,7 @@ switcher_key(struct weston_keyboard_grab *grab,
 	struct switcher *switcher = container_of(grab, struct switcher, grab);
 	enum wl_keyboard_key_state state = state_w;

-	if (key == KEY_TAB && state == WL_KEYBOARD_KEY_STATE_PRESSED)
+	if (key == KEY_SPACE && state == WL_KEYBOARD_KEY_STATE_PRESSED)
 		switcher_next(switcher);
 }

@@ -5003,7 +5003,7 @@ shell_add_bindings(struct weston_compositor *ec, struct desktop_shell *shell)
 		weston_compositor_add_button_binding(ec, BTN_MIDDLE, mod,
 						     rotate_binding, NULL);

-	weston_compositor_add_key_binding(ec, KEY_TAB, mod, switcher_binding,
+	weston_compositor_add_key_binding(ec, KEY_SPACE, mod, switcher_binding,
 					  shell);
 	weston_compositor_add_key_binding(ec, KEY_F9, mod, backlight_binding,
 					  ec);

```

## GUI libraries

See details on the [official website](http://wayland.freedesktop.org/toolkits.html).

### GTK+ 3

The [gtk3](https://www.archlinux.org/packages/?name=gtk3) package has the Wayland backend enabled. GTK+ will default to the Wayland backend, but it is possible to override it to Xwayland by modifying an environment variable: `GDK_BACKEND=x11`.

### Qt 5

To enable Wayland support in Qt 5, install the [qt5-wayland](https://www.archlinux.org/packages/?name=qt5-wayland) package.

To run a Qt 5 app with the Wayland plugin, use `-platform wayland` or set the `QT_QPA_PLATFORM=wayland-egl` [environment variable](/index.php/Environment_variable "Environment variable").

### Clutter

The Clutter toolkit has a Wayland backend that allows it to run as a Wayland client. The backend is enabled in the [clutter](https://www.archlinux.org/packages/?name=clutter) package.

To run a Clutter app on Wayland, set `CLUTTER_BACKEND=wayland`.

### SDL2

To run a SDL2 application on Wayland, set `SDL_VIDEODRIVER=wayland`.

### GLFW

To use GLFW with the Wayland backend, install the [glfw-wayland](https://www.archlinux.org/packages/?name=glfw-wayland) package (instead of [glfw-x11](https://www.archlinux.org/packages/?name=glfw-x11)).

### GLEW

To use GLEW with the Wayland backend, install the [glew-wayland](https://www.archlinux.org/packages/?name=glew-wayland) package (instead of [glew](https://www.archlinux.org/packages/?name=glew)).

### EFL

EFL has complete Wayland support. To run a EFL application on Wayland, see Wayland [project page](http://wayland.freedesktop.org/efl.html).

## Compositors

| Name | Type | Description |
| GNOME | Stacking | See [GNOME#Starting](/index.php/GNOME#Starting "GNOME"). |
| sway | Tiling | [Sway](/index.php/Sway "Sway") is an i3-compatible window manager for Wayland. [GitHub](https://github.com/SirCmpwn/sway) |
| Enlightenment | Stacking | [More Info](https://www.enlightenment.org/about-wayland) |
| KDE Plasma | Stacking | See [KDE#Starting Plasma](/index.php/KDE#Starting_Plasma "KDE") |
| Orbment | Tiling | [orbment](https://github.com/Cloudef/orbment) (previously loliwm) is an abandonned tiling WM for Wayland. |
| Velox | Tiling | [Velox](/index.php/Velox "Velox") is a simple window manager based on swc. It is inspired by [dwm](/index.php/Dwm "Dwm") and [xmonad](/index.php/Xmonad "Xmonad"). |
| Orbital | Stacking | [Orbital](https://github.com/giucam/orbital) is a Wayland compositor and shell (more akin to a WM than a DE) using Qt5 and Weston. The goal of the project is to build a simple but flexible and good looking Wayland desktop. |
| Liri Shell | Stacking | [Liri Shell](https://github.com/lirios/shell) is the desktop shell for [Liri](/index.php/Liri "Liri"), built using QtQuick and QtCompositor as a compositor for Wayland. |
| Maynard | *(Unclear)* | [Maynard](https://github.com/raspberrypi/maynard) is a desktop shell client for Weston based on GTK. It was based on weston-gtk-shell, a project by Tiago Vignatti. Not under development. [[1]](https://github.com/raspberrypi/maynard/issues/54#issuecomment-303422302)[[2]](https://github.com/raspberrypi/maynard/issues/55#issuecomment-373808518) |
| Motorcar | *(Unclear)* | [Motorcar](https://github.com/evil0sheep/motorcar) is a Wayland compositor to explore 3D windowing using virtual reality. |
| Way Cooler | Tiling | [Way Cooler](https://github.com/way-cooler/way-cooler) is a customizable (Lua config files) Wayland compositor written in Rust. Inspired by i3 and awesome. |
| Maze Compositor | Floating 3D | [Maze Compositor](https://github.com/imbavirus/mazecompositor) is a 3D Qt based Wayland compositor |
| Grefsen | Floating | [Grefsen](https://github.com/ec1oud/grefsen) is a Qt/Wayland compositor providing a minimal desktop environment. |
| Waymonad | Tiling | [Waymonad](https://github.com/waymonad/waymonad) is a Wayland compositor based on ideas from and inspired by xmonad |
| wayfire | Stacking | [Wayfire](https://github.com/WayfireWM/wayfire) is a general purpose compositor. |

Some of the above may support [display managers](/index.php/Display_manager "Display manager"). Check `/usr/share/wayland-sessions/*compositor*.desktop` to see how they are started.

## Troubleshooting

### Gamma

While [Redshift](/index.php/Redshift "Redshift") doesn't support Wayland (without a patch) it is possible to apply the desired temperature in [tty](/index.php/Tty "Tty") before starting a compositor. For example:

```
redshift -m drm -PO 3000

```

Otherwise some compositors feature this option during runtime:

*   [GNOME](/index.php/GNOME "GNOME") provides features like [Redshift](/index.php/Redshift "Redshift") out-of-the-box and has Wayland support. Enable [Night Light](/index.php/GNOME#Night_Light "GNOME") in Display settings.
*   Likewise, [KDE Plasma](/index.php/KDE_Plasma "KDE Plasma") provides *Night Color* which is Wayland-only.
*   On Sway 1.0 and other wlroots-based compositors, [redshift-wlr-gamma-control-git](https://aur.archlinux.org/packages/redshift-wlr-gamma-control-git/) can be used.
*   On Orbital, [redshift-wayland-git](https://aur.archlinux.org/packages/redshift-wayland-git/) can be used.

### LLVM assertion failure

If you get an LLVM assertion failure, you need to rebuild [mesa](https://www.archlinux.org/packages/?name=mesa) without Gallium LLVM until this problem is fixed.

This may imply disabling some drivers which require LLVM. You may also try exporting the following, if having problems with hardware drivers:

```
$ export EGL_DRIVER=/usr/lib/egl/egl_gallium.so

```

### Slow motion, graphical glitches, and crashes

Gnome-shell users may experience display issues when they switch to Wayland from X. One of the root cause might be the `CLUTTER_PAINT=disable-clipped-redraws:disable-culling` set by yourself for Xorg-based gnome-shell. Just try to remove it from `/etc/environment` or other rc files to see if everything goes back to normal.

### GNOME Wayland on tty1, Weston on tty2

(20170106) apps started on GNOME with WAYLAND_DISPLAY set to weston make it not respond any more ([Wayland issue 99489](https://bugs.freedesktop.org/show_bug.cgi?id=99489))

### Electron based applications / VS Code

Try running with GDK_BACKEND=x11\. Example alias:

```
$ alias code='GDK_BACKEND=x11 /usr/bin/code 2>/dev/null'

```

### Screen recording

Currently only [green-recorder](https://aur.archlinux.org/packages/green-recorder/) supports screen recording on Wayland (requires a GNOME session).

### Remote display

*   (20180401) mutter has now remote desktop enabled at compile time, see [https://wiki.gnome.org/Projects/Mutter/RemoteDesktop](https://wiki.gnome.org/Projects/Mutter/RemoteDesktop) and [gnome-remote-desktop](https://www.archlinux.org/packages/?name=gnome-remote-desktop) for details.
*   (20161229) there was a merge of FreeRDP into Weston in 2013, enabled via a compile flag. The [weston](https://www.archlinux.org/packages/?name=weston) package does not have it enabled.

### Input grabbing in games, remote desktop and VM windows

In contrast to Xorg, Wayland does not allow exclusive input device grabbing, also known as active or explicit grab (e.g. [keyboard](https://tronche.com/gui/x/xlib/input/XGrabKeyboard.html), [mouse](https://tronche.com/gui/x/xlib/input/XGrabPointer.html)), instead, it depends on the Wayland compositor to pass keyboard shortcuts and confine the pointer device to the application window.

This change in input grabbing breaks current applications' behavior, meaning:

*   Hotkey combinations and modifiers will be caught by the compositor and won't be sent to remote desktop and virtual machine windows.
*   The mouse pointer will not be restricted to the application's window which might cause a parallax effect where the location of the mouse pointer inside the window of the virtual machine or remote desktop is displaced from the host's mouse pointer.

Wayland solves this by adding protocol extensions for Wayland and XWayland. Support for these extensions is needed to be added to the Wayland compositors. In the case of native Wayland clients, the used widget toolkits (e.g GTK, QT) needs to support these extensions or the applications themselves if no widget toolkit is being used. In the case of Xorg applications, no changes in the applications or widget toolkits are needed as the XWayland support is enough.

These extensions are already included in [wayland-protocols](https://www.archlinux.org/packages/?name=wayland-protocols), and supported by [xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland) 1.20.

The related extensions are:

*   [XWayland keyboard grabbing protocol](https://cgit.freedesktop.org/wayland/wayland-protocols/tree/unstable/xwayland-keyboard-grab/xwayland-keyboard-grab-unstable-v1.xml)
*   [Compositor shortcuts inhibit protocol](https://cgit.freedesktop.org/wayland/wayland-protocols/tree/unstable/keyboard-shortcuts-inhibit/keyboard-shortcuts-inhibit-unstable-v1.xml)
*   [Relative pointer protocol](https://cgit.freedesktop.org/wayland/wayland-protocols/tree/unstable/relative-pointer/relative-pointer-unstable-v1.xml)
*   [Pointer constraints protocol](https://cgit.freedesktop.org/wayland/wayland-protocols/tree/unstable/pointer-constraints/pointer-constraints-unstable-v1.xml)

Supporting Wayland compositors:

*   Mutter, [GNOME](/index.php/GNOME "GNOME")'s compositor [since release 3.28](https://bugzilla.gnome.org/show_bug.cgi?id=783342).

Supporting widget toolkits:

*   GTK since release 3.22.18.

#### wlroots input inhibitor protocol

[Input inhibitor](https://github.com/swaywm/wlr-protocols/blob/master/unstable/wlr-input-inhibitor-unstable-v1.xml) is a Wayland protocol which was defined the by developers of Sway and wlroots and is overlapping Wayland's `Compositor shortcuts inhibit` protocol.
Sway and wlroots do not support the `Compositor shortcuts inhibit` and `XWayland keyboard grabbing` protocols, and it seems they are against adding support for the latter [[3]](https://github.com/swaywm/wlroots/pull/635#issuecomment-366385856) [[4]](https://github.com/swaywm/wlroots/issues/624#issuecomment-367276476).
No widget toolkit or application is known to support this protocol.

## See also

*   [Article about Wayland debugging on Fedora Wiki](https://fedoraproject.org/wiki/How_to_debug_Wayland_problems)
*   [Cursor themes](/index.php/Cursor_themes "Cursor themes")
*   [Arch Linux forum discussion](https://bbs.archlinux.org/viewtopic.php?id=107499)
*   [Wayland documentation online](http://wayland.freedesktop.org/docs/html/)