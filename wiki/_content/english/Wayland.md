**Wayland** is a new windowing protocol for Linux. Utilization of Wayland requires changes to and re-installation of parts of your system's software. For more information on Wayland see its [homepage](http://wayland.freedesktop.org/).

## Contents

*   [1 Requirements](#Requirements)
*   [2 Installation](#Installation)
*   [3 Usage](#Usage)
*   [4 Weston](#Weston)
    *   [4.1 Installation](#Installation_2)
    *   [4.2 Usage](#Usage_2)
    *   [4.3 Configuration](#Configuration)
        *   [4.3.1 XWayland](#XWayland)
        *   [4.3.2 Screencast recording](#Screencast_recording)
        *   [4.3.3 High DPI displays](#High_DPI_displays)
        *   [4.3.4 Shell font](#Shell_font)
*   [5 GUI libraries](#GUI_libraries)
    *   [5.1 GTK+ 3](#GTK.2B_3)
    *   [5.2 Qt 5](#Qt_5)
    *   [5.3 Clutter](#Clutter)
    *   [5.4 SDL](#SDL)
    *   [5.5 GLFW](#GLFW)
    *   [5.6 EFL](#EFL)
*   [6 Window managers and desktop shells](#Window_managers_and_desktop_shells)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 LLVM assertion failure](#LLVM_assertion_failure)
    *   [7.2 Weston fails to launch after update to 1.7](#Weston_fails_to_launch_after_update_to_1.7)
*   [8 See also](#See_also)

## Requirements

Currently Wayland will only work on systems utilizing [KMS](/index.php/KMS "KMS").

## Installation

**Note:** Wayland is most likely installed on your system already, since it is an indirect dependency of [gtk2](https://www.archlinux.org/packages/?name=gtk2) and [gtk3](https://www.archlinux.org/packages/?name=gtk3).

[Install](/index.php/Install "Install") the [wayland](https://www.archlinux.org/packages/?name=wayland) package.

## Usage

As Wayland is only a library, it is useless on its own. To replace X Server, you need a compositor (like [#Weston](#Weston)).

## Weston

### Installation

[Install](/index.php/Install "Install") the [weston](https://www.archlinux.org/packages/?name=weston) package.

### Usage

<caption>***Keyboard Shortcuts** (super = windows key - can be changed, see weston.ini)* `Ctrl-b`</caption>
| Cmd | Action |
| Ctrl + Alt + Backspace | Quit Weston |
| Super + Scroll (or PageUp/PageDown) | Zoom in/out of desktop |
| Super + Tab | Switch windows |
| Super + LMB | Move Window |
| Super + MMB | Rotate Window ! |
| Super + RMB | Resize Window |
| Super + Alt + Scroll | Change window opacity |
| Super + K | Force Kill Active Window |
| Super + KeyUp/KeyDown | Switch Prev/Next Workspace |
| Super + Shift + KeyUp/KeyDown | Grab Current Window and Switch Workspace |
| Super + F***n*** | Switch to Workspace ***n*** |
| Super + S | Take a screenshot |
| Super + R | Record a screencast. |

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

To test the frame protocol (runs `glxgears`):

```
$ weston-gears

```

To display images:

```
$ weston-image image1.jpg image2.jpg...

```

### Configuration

Example configuration file for keyboard layout, module selection and UI modifications. See `man weston.ini` for full details:

 `~/.config/weston.ini` 
```
[core]
# xwayland support
modules=xwayland.so

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
modules=xwayland.so

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

The [gtk3](https://www.archlinux.org/packages/?name=gtk3) package from the official repositories now has the Wayland backend enabled.

GTK+ 3 gained support for multiple backends at runtime and can switch between backends in the same way Qt can with lighthouse.

When both Wayland and X backends are enabled, GTK+ will default to the X11 backend, but this can be overridden by modifying an environment variable: `GDK_BACKEND=wayland`.

### Qt 5

The [qt5](https://www.archlinux.org/groups/x86_64/qt5/) package from the repositories has the Wayland support if [qt5-wayland](https://www.archlinux.org/packages/?name=qt5-wayland) is installed. To run a Qt 5 app with the Wayland plugin, set the `QT_QPA_PLATFORM=wayland-egl` [environment variable](/index.php/Environment_variable "Environment variable").

### Clutter

The Clutter toolkit has a Wayland backend that allows it to run as a Wayland client. The backend is enabled in the official package in extra.

To run a Clutter app on Wayland, set `CLUTTER_BACKEND=wayland`.

### SDL

Experimental wayland support is now in SDL 2.0.2 and enabled by default on Arch Linux.

To run a SDL application on Wayland, set `SDL_VIDEODRIVER=wayland`.

### GLFW

Experimental wayland support is now in GLFW 3.1 and can be enabled with the `-DGLFW_USE_WAYLAND=ON` CMake option at compile time. You can also install the package [glfw-wayland-git](https://aur.archlinux.org/packages/glfw-wayland-git/) from the AUR.

### EFL

EFL has complete Wayland support. To run a EFL application on Wayland, see Wayland [project page](http://wayland.freedesktop.org/efl.html).

## Window managers and desktop shells

| Name | Type | Description |
| GNOME | Compositing | See [GNOME#Starting GNOME](/index.php/GNOME#Starting_GNOME "GNOME"). |
| Hawaii | *(Unclear)* | See [Hawaii](/index.php/Hawaii "Hawaii"). |
| sway | Tiling | [Sway](/index.php/Sway "Sway") is an i3-compatible window manager for Wayland. [Github](https://github.com/SirCmpwn/sway) |
| Enlightenment | *(Unclear)* | Long running minimal Window Manager-turned Wayland compositor. E19 originally had Wayland support but this was removed and now only E20+ Wayland is considered stable enough for regular use. [More Info](https://www.enlightenment.org/about-wayland) |
| KDE Plasma | Compositing | See [KDE#Starting Plasma](/index.php/KDE#Starting_Plasma "KDE") |
| Orbment | Tiling | [orbment](https://github.com/Cloudef/orbment) (previously loliwm) is a tiling WM for Wayland. |
| Velox | Tiling | [Velox](/index.php/Velox "Velox") is a simple window manager based on swc. It is inspired by [dwm](/index.php/Dwm "Dwm") and [xmonad](/index.php/Xmonad "Xmonad"). |
| Orbital | Compositing | [Orbital](https://github.com/giucam/orbital) is a Wayland compositor and shell, using Qt5 and Weston. The goal of the project is to build a simple yet flexible and good looking Wayland desktop. It is not a full fledged DE but rather the analogue of a WM in the X11 world, such as [Awesome](/index.php/Awesome "Awesome") or [Fluxbox](/index.php/Fluxbox "Fluxbox"). |
| Papyros Shell | *(Unclear)* | [Papyros Shell](https://github.com/papyros/papyros-shell) is the desktop shell for [Papyros](/index.php/Papyros "Papyros"), built using QtQuick and QtCompositor as a compositor for Wayland. |
| Maynard | *(Unclear)* | [Maynard](https://github.com/raspberrypi/maynard) is a desktop shell client for Weston based on GTK. It was based on weston-gtk-shell, a project by Tiago Vignatti. |
| Motorcar | *(Unclear)* | [Motorcar](https://github.com/evil0sheep/motorcar) is a wayland compositor to explore 3D windowing. |
| Way Cooler | Tiling | Customizeable (lua config files) Wayland compositor written in Rust. Inspired by i3 and awesome. [AUR](https://aur.archlinux.org/packages/way-cooler/). |

Some of installed wayland desktop clients might store information in `/usr/share/wayland-sessions/*.desktop` files about how to start them in wayland.

## Troubleshooting

### LLVM assertion failure

If you get an LLVM assertion failure, you need to rebuild [mesa](https://www.archlinux.org/packages/?name=mesa) without Gallium LLVM until this problem is fixed.

This may imply disabling some drivers which require LLVM. You may also try exporting the following, if having problems with hardware drivers:

```
$ export EGL_DRIVER=/usr/lib/egl/egl_gallium.so

```

### Weston fails to launch after update to 1.7

This is possibly caused by the `desktop-shell.so` module being loaded by your `weston.ini`. This used to be required, but is not anymore.

Remove it from the `[core]` section:

 `~/.config/weston.ini` 
```
[core]
modules=xwayland.so,desktop-shell.so

```

So that you end up with:

 `~/.config/weston.ini` 
```
[core]
modules=xwayland.so

```

## See also

*   [Cursor themes](/index.php/Cursor_themes "Cursor themes")
*   [Arch Linux forum discussion](https://bbs.archlinux.org/viewtopic.php?id=107499)
*   [Wayland documentation online](http://wayland.freedesktop.org/docs/html/)