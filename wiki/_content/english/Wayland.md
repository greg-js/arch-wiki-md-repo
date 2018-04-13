Related articles

*   [KMS](/index.php/KMS "KMS")
*   [Xorg](/index.php/Xorg "Xorg")

[Wayland](http://wayland.freedesktop.org/) is a protocol for a [compositor](https://en.wikipedia.org/wiki/Compositing_window_manager "wikipedia:Compositing window manager") to talk to its clients, as well as a library implementing this protocol. Many major Linux desktop environments, like [GNOME](/index.php/GNOME "GNOME") and [KDE](/index.php/KDE "KDE"), support Wayland. There is also a compositor reference implementation called "Weston". [XWayland](https://wayland.freedesktop.org/xserver.html) implements a compatibility layer to seamlessly run legacy X11 applications on Wayland.

## Contents

*   [1 Requirements](#Requirements)
    *   [1.1 Buffer API support](#Buffer_API_support)
*   [2 Weston](#Weston)
    *   [2.1 Installation](#Installation)
    *   [2.2 Usage](#Usage)
    *   [2.3 Configuration](#Configuration)
        *   [2.3.1 XWayland](#XWayland)
        *   [2.3.2 Screencast recording](#Screencast_recording)
        *   [2.3.3 High DPI displays](#High_DPI_displays)
        *   [2.3.4 Shell font](#Shell_font)
*   [3 GUI libraries](#GUI_libraries)
    *   [3.1 GTK+ 3](#GTK.2B_3)
    *   [3.2 Qt 5](#Qt_5)
    *   [3.3 Clutter](#Clutter)
    *   [3.4 SDL2](#SDL2)
    *   [3.5 GLFW](#GLFW)
    *   [3.6 GLEW](#GLEW)
    *   [3.7 EFL](#EFL)
*   [4 Compositors](#Compositors)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Running graphical applications as root](#Running_graphical_applications_as_root)
    *   [5.2 LLVM assertion failure](#LLVM_assertion_failure)
    *   [5.3 Slow motion, graphical glitches, and crashes](#Slow_motion.2C_graphical_glitches.2C_and_crashes)
    *   [5.4 nemo](#nemo)
    *   [5.5 X11 on tty1, wayland on tty2](#X11_on_tty1.2C_wayland_on_tty2)
    *   [5.6 gnome wayland on tty1, weston on tty2](#gnome_wayland_on_tty1.2C_weston_on_tty2)
    *   [5.7 weston-terminal](#weston-terminal)
    *   [5.8 liteide](#liteide)
    *   [5.9 screen recording](#screen_recording)
    *   [5.10 remote display](#remote_display)
    *   [5.11 Input grabbing in games, remote desktop and VM windows](#Input_grabbing_in_games.2C_remote_desktop_and_VM_windows)
*   [6 See also](#See_also)

## Requirements

Most Wayland compositors only work on systems using [KMS](/index.php/KMS "KMS").

Wayland by itself does not provide a graphical environment; for this you also need a compositor such as [#Weston](#Weston) or [Sway](/index.php/Sway "Sway"), or a desktop environment that includes a compositor such as [GNOME](/index.php/GNOME "GNOME") or [KDE](/index.php/KDE "KDE").

### Buffer API support

For the GPU driver and Wayland compositor to be compatible they must support the same buffer API. There are two main APIs: [GBM](https://en.wikipedia.org/wiki/Generic_Buffer_Management "wikipedia:Generic Buffer Management") and [EGLStreams](http://www.phoronix.com/scan.php?page=news_item&px=XDC2016-Device-Memory-API).

| Buffer API | GPU driver support | Wayland compositor support |
| GBM | All except [NVIDIA](/index.php/NVIDIA "NVIDIA") | All |
| EGLStreams | [NVIDIA](/index.php/NVIDIA "NVIDIA") | [GNOME](/index.php/GNOME "GNOME"), [Grefsen](/index.php?title=Grefsen&action=edit&redlink=1 "Grefsen (page does not exist)"), [Sway](/index.php/Sway "Sway") ([will be removed](https://sircmpwn.github.io/2017/10/26/Fuck-you-nvidia.html)) |

## Weston

Weston is the reference implementation of a Wayland compositor.

### Installation

Install the [weston](https://www.archlinux.org/packages/?name=weston) package.

### Usage

<caption>***Keyboard Shortcuts** (super = windows key - can be changed, see weston.ini)* `Ctrl-b`</caption>
| Cmd | Action |
| `Ctrl+Alt+Backspace` | Quit Weston |
| `Super+Scroll` (or `PageUp`/`PageDown`) | Zoom in/out of desktop |
| `Super+Tab` | Switch windows |
| `Super+LMB` | Move Window |
| `Super+MMB` | Rotate Window ! |
| `Super+RMB` | Resize Window |
| `Super+Alt+Scroll` | Change window opacity |
| `Super+K` | Force Kill Active Window |
| `Super+KeyUp/KeyDown` | Switch Prev/Next Workspace |
| `Super+Shift+KeyUp/KeyDown` | Grab Current Window and Switch Workspace |
| `Super+F***n***` | Switch to Workspace ***n*** |
| `Super+S` | Take a screenshot |
| `Super+R` | Record a screencast. |

Now that Wayland and its requirements are installed you should be ready to test it out.

It is possible to run Weston inside a running X session:

```
$ weston

```

Alternatively, to try to launch Weston natively, switch to a terminal and run:

```
$ weston-launch

```

Then at a TTY within Weston, you can run the demos. To launch a terminal emulator:

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

Example configuration file for keyboard layout, module selection and UI modifications. See [weston.ini(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/weston.ini.5) for full details. The Weston outputs differ slightly from `xorg.conf`'s Monitors:

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

 `~/.config/weston.ini` 
```
[core]
# xwayland support
xwayland=true

[libinput]
enable_tap=true

[shell]
background-image=/usr/share/backgrounds/gnome/Aqua.jpg
background-color=0xff002244
panel-color=0x90ff0000
locking=true
animation=zoom
close-animation=fade
focus-animation=dim-layer
#binding-modifier=ctrl
#num-workspaces=6
### for cursor themes install xcursor-themes pkg from Extra. ###
#cursor-theme=whiteglass
#cursor-size=24

### tablet options ###
#lockscreen-icon=/usr/share/icons/gnome/256x256/actions/lock.png
#lockscreen=/usr/share/backgrounds/gnome/Garden.jpg
#homescreen=/usr/share/backgrounds/gnome/Blinds.jpg
#animation=fade

###  for Laptop displays  ###
#[output]
#name=LVDS1
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

[input-method]
#path=/usr/lib/weston/weston-keyboard

[keyboard]
keymap_rules=evdev
#keymap_layout=gb,de
#keymap_options=caps:ctrl_modifier,shift:both_capslock_cancel
### keymap_options from /usr/share/X11/xkb/rules/base.lst ###
numlock-on=true

[terminal]
#font=DroidSansMono
#font-size=14

[launcher]
icon=/usr/share/icons/gnome/24x24/apps/utilities-terminal.png
path=/usr/bin/weston-terminal

[launcher]
icon=/usr/share/icons/gnome/24x24/apps/utilities-terminal.png
path=/usr/bin/gnome-terminal

[launcher]
icon=/usr/share/icons/hicolor/24x24/apps/firefox.png
path=/usr/bin/firefox

[launcher]
icon=/usr/share/weston/icon_flower.png
path=/usr/bin/weston-flower

[screensaver]
# Uncomment path to disable screensaver
path=/usr/libexec/weston-screensaver
duration=600

```

Minimal `weston.ini` :

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
modules=xwayland.so

```

**Note:** if X is not already configured you may need to configure a keymap: [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg")

#### Screencast recording

Weston has build-in screencast recording which can be started and stopped by pressing the `Super+r` key combination. Screencasts are saved to the file `capture.wcap` in the current working directory of Weston.

The WCAP format is a lossless video format specific to Weston, which only records the difference in frames. To be able to play the recorded screencast, the WCAP file will need to be converted to a format which a media player can understand. First, convert the capture to the YUV pixel format:

```
$ wcap-decode capture.wcap --yuv4mpeg2 > capture.y4m

```

The YUV file can then be transcoded to other formats using [FFmpeg](/index.php/FFmpeg "FFmpeg").

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
| GNOME | Stacking | See [GNOME#Starting GNOME](/index.php/GNOME#Starting_GNOME "GNOME"). |
| sway | Tiling | [Sway](/index.php/Sway "Sway") is an i3-compatible window manager for Wayland. [GitHub](https://github.com/SirCmpwn/sway) |
| Enlightenment | Stacking | [More Info](https://www.enlightenment.org/about-wayland) |
| KDE Plasma | Stacking | See [KDE#Starting Plasma](/index.php/KDE#Starting_Plasma "KDE") |
| Orbment | Tiling | [orbment](https://github.com/Cloudef/orbment) (previously loliwm) is an abandonned tiling WM for Wayland. |
| Velox | Tiling | [Velox](/index.php/Velox "Velox") is a simple window manager based on swc. It is inspired by [dwm](/index.php/Dwm "Dwm") and [xmonad](/index.php/Xmonad "Xmonad"). |
| Orbital | Stacking | [Orbital](https://github.com/giucam/orbital) is a Wayland compositor and shell, using Qt5 and Weston. The goal of the project is to build a simple yet flexible and good looking Wayland desktop. It is not a full fledged DE but rather the analogue of a WM in the X11 world, such as [Awesome](/index.php/Awesome "Awesome") or [Fluxbox](/index.php/Fluxbox "Fluxbox"). |
| Liri Shell | Stacking | [Liri Shell](https://github.com/lirios/shell) is the desktop shell for [Liri](/index.php/Liri "Liri"), built using QtQuick and QtCompositor as a compositor for Wayland. |
| Maynard | *(Unclear)* | [Maynard](https://github.com/raspberrypi/maynard) is a desktop shell client for Weston based on GTK. It was based on weston-gtk-shell, a project by Tiago Vignatti. |
| Motorcar | *(Unclear)* | [Motorcar](https://github.com/evil0sheep/motorcar) is a Wayland compositor to explore 3D windowing using virtual reality. |
| Way Cooler | Tiling | [way-cooler](https://aur.archlinux.org/packages/way-cooler/) is a customizable (Lua config files) Wayland compositor written in Rust. Inspired by i3 and awesome. |
| Maze Compositor | Floating 3D | [Maze Compositor](https://github.com/capisce/mazecompositor) is a 3D Qt based Wayland compositor |
| Grefsen | Floating | [Grefsen](https://github.com/ec1oud/grefsen) is a Qt/Wayland compositor providing a minimal desktop environment. |

Some of installed wayland desktop clients might store information in `/usr/share/wayland-sessions/*.desktop` files about how to start them in wayland.

## Troubleshooting

### Running graphical applications as root

Trying to run a graphical application as root via [su](/index.php/Su "Su"), [sudo](/index.php/Sudo "Sudo") or [pkexec](/index.php/Polkit "Polkit") in a Wayland session (*e.g.* [GParted](/index.php/GParted "GParted") or [Gedit](/index.php/Gedit "Gedit")), be it in a terminal emulator or from a graphical component, will fail with an error similar to this:

```
$ sudo gedit
No protocol specified
Unable to init server: Could not connect: Connection refused

(gedit:2349): Gtk-WARNING **: cannot open display: :0

```

Before Wayland, running GUI applications with elevated privileges could be properly implemented by creating a [Polkit](/index.php/Polkit "Polkit") policy, or more dangerously done by running the command in a terminal by prepending the command with `sudo`; but under (X)Wayland this does not work anymore as the default has been made to only allow the user who started the X server to connect clients to it (see the [bug report](https://bugzilla.redhat.com/show_bug.cgi?id=1266771) and [the](https://cgit.freedesktop.org/xorg/xserver/commit/?id=c4534a3) [upstream](https://cgit.freedesktop.org/xorg/xserver/commit/?id=4b4b908) [commits](https://cgit.freedesktop.org/xorg/xserver/commit/?id=76636ac) it refers to).

The most straightforward workaround is to use [xhost](/index.php/Xhost "Xhost") to temporarily allow the root user to access the local user's X session. To do so, execute the following command as the current (unprivileged) user[[1]](https://bugzilla.redhat.com/show_bug.cgi?id=1274451#c64):

```
 xhost si:localuser:root

```

To remove this access after the application has been closed:

```
 xhost -si:localuser:root

```

**Note:** This [GNOME bug report](https://bugzilla.gnome.org//show_bug.cgi?id=772875) suggests two other workarounds, with one specific to editing text files.

### LLVM assertion failure

If you get an LLVM assertion failure, you need to rebuild [mesa](https://www.archlinux.org/packages/?name=mesa) without Gallium LLVM until this problem is fixed.

This may imply disabling some drivers which require LLVM. You may also try exporting the following, if having problems with hardware drivers:

```
$ export EGL_DRIVER=/usr/lib/egl/egl_gallium.so

```

### Slow motion, graphical glitches, and crashes

Gnome-shell users may experience display issues when they switch to Wayland from X. One of the root cause might be the `CLUTTER_PAINT=disable-clipped-redraws:disable-culling` set by yourself for Xorg-based gnome-shell. Just try to remove it from `/etc/environment` or other rc files to see if everything goes back to normal.

### nemo

(20161229) prevent that the desktop is created <ref>[nemo issue 1343](https://github.com/linuxmint/nemo/issues/1343)</ref>

```
gsettings set org.nemo.desktop show-desktop-icons false

```

### X11 on tty1, wayland on tty2

(20161209) windows of gnome applications end up on tty2 no matter where started ([gnome issue 774775)](https://bugzilla.gnome.org/show_bug.cgi?id=774775)

### gnome wayland on tty1, weston on tty2

(20170106) apps started on gnome with WAYLAND_DISPLAY set to westen make it not respond any more ([wayland issue 99489](https://bugs.freedesktop.org/show_bug.cgi?id=99489))

### weston-terminal

(20161229) core dump when started on gnome

### liteide

(20161229) [core dump](https://github.com/visualfc/liteide/issues/734)] on gnome and weston.

### screen recording

Currently only [green-recorder](https://aur.archlinux.org/packages/green-recorder/) supports screen recording on Wayland (requires a GNOME session).

### remote display

(20180401) mutter has now remote desktop enabled at compile time, see [https://wiki.gnome.org/Projects/Mutter/RemoteDesktop](https://wiki.gnome.org/Projects/Mutter/RemoteDesktop) and [https://aur.archlinux.org/packages/gnome-remote-desktop/](https://aur.archlinux.org/packages/gnome-remote-desktop/) for details. (20161229) there was a merge of FreeRDP into weston in 2013, enabled via compile time switch. The arch linux weston package currently has it not enabled.

### Input grabbing in games, remote desktop and VM windows

In contrast to Xorg, Wayland does not allow exclusive input device grabbing, also known as active or explicit grab (e.g. [keyboard](https://tronche.com/gui/x/xlib/input/XGrabKeyboard.html), [mouse](https://tronche.com/gui/x/xlib/input/XGrabPointer.html)), instead, it depends on the Wayland compositor to pass keyboard shortcuts and confine the pointer device to the application window.

This change in input grabbing breaks current applications' behavior, meaning:

*   Hotkey combinations and modifiers will be caught by the compositor and won't be sent to remote desktop and virtual machine windows.
*   The mouse pointer will not be restricted to the application's window which might cause a parallax effect where the location of the mouse pointer inside the window of the virtual machine or remote desktop is displaced from the host's mouse pointer.

Wayland solves this by adding protocol extensions for Wayland and XWayland. Support for these extensions is needed to be added to the Wayland compositors. In the case of native Wayland clients, the used widget toolkits (e.g GTK, QT) needs to support these extensions or the applications themselves if no widget toolkit is being used. In the case of Xorg applications, no changes in the applications or widget toolkits are needed as the XWayland support is enough.

These extensions are already included in the latest stable release of [wayland-protocols](https://www.archlinux.org/packages/?name=wayland-protocols), and supported by the latest release candidate of [xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland) 1.20.

The related extensions are:

*   [XWayland keyboard grabbing protocol](https://cgit.freedesktop.org/wayland/wayland-protocols/tree/unstable/xwayland-keyboard-grab/xwayland-keyboard-grab-unstable-v1.xml)
*   [Compositor shortcuts inhibit protocol](https://cgit.freedesktop.org/wayland/wayland-protocols/tree/unstable/keyboard-shortcuts-inhibit/keyboard-shortcuts-inhibit-unstable-v1.xml)
*   [Relative pointer protocol](https://cgit.freedesktop.org/wayland/wayland-protocols/tree/unstable/relative-pointer/relative-pointer-unstable-v1.xml)
*   [Pointer constraints protocol](https://cgit.freedesktop.org/wayland/wayland-protocols/tree/unstable/pointer-constraints/pointer-constraints-unstable-v1.xml)

Supporting Wayland compositors:

*   Mutter, [GNOME's](/index.php/GNOME "GNOME") compositor [since release 3.28](https://bugzilla.gnome.org/show_bug.cgi?id=783342).

Supporting widget toolkits:

*   GTK since release 3.22.18.

## See also

*   [Article about Wayland debugging on Fedora Wiki](https://fedoraproject.org/wiki/How_to_debug_Wayland_problems)
*   [Cursor themes](/index.php/Cursor_themes "Cursor themes")
*   [Arch Linux forum discussion](https://bbs.archlinux.org/viewtopic.php?id=107499)
*   [Wayland documentation online](http://wayland.freedesktop.org/docs/html/)