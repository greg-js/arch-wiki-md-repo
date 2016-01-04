# Wayland

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [KMS](/index.php/KMS "KMS")
*   [Xorg](/index.php/Xorg "Xorg")
*   [Mir](/index.php/Mir "Mir")

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

**Note:** Wayland is most likely installed on your system already, as it is an indirect dependency of [gtk2](https://www.archlinux.org/packages/?name=gtk2) and [gtk3](https://www.archlinux.org/packages/?name=gtk3).

[Install](/index.php/Install "Install") the [wayland](https://www.archlinux.org/packages/?name=wayland) package.

## Usage

As Wayland is only a library, it is useless on its own. To replace X Server, you need a compositor (like Weston).

## Weston

### Installation

[Install](/index.php/Install "Install") the [weston](https://www.archlinux.org/packages/?name=weston) package.

### Usage

<table class="wikitable" style="float: right; width: 200px;"><caption>_**Keyboard Shortcuts** (super = windows key - can be changed, see weston.ini)_ `Ctrl-b`</caption>

<tbody>

<tr>

<th>Cmd</th>

<th>Action</th>

</tr>

<tr>

<td>Ctrl + Alt + Backspace</td>

<td>Quit Weston</td>

</tr>

<tr>

<td>Super + Scroll (or PageUp/PageDown)</td>

<td>Zoom in/out of desktop</td>

</tr>

<tr>

<td>Super + Tab</td>

<td>Switch windows</td>

</tr>

<tr>

<td>Super + LMB</td>

<td>Move Window</td>

</tr>

<tr>

<td>Super + MMB</td>

<td>Resize Window</td>

</tr>

<tr>

<td>Super + RMB</td>

<td>Rotate Window !</td>

</tr>

<tr>

<td>Super + Alt + Scroll</td>

<td>Change window opacity</td>

</tr>

<tr>

<td>Super + K</td>

<td>Force Kill Active Window</td>

</tr>

<tr>

<td>Super + KeyUp/KeyDown</td>

<td>Switch Prev/Next Workspace</td>

</tr>

<tr>

<td>Super + Shift + KeyUp/KeyDown</td>

<td>Grab Current Window and Switch Workspace</td>

</tr>

<tr>

<td>Super + F_**n**_</td>

<td>Switch to Workspace _**n**_</td>

</tr>

<tr>

<td>Super + S</td>

<td>Take a screenshot</td>

</tr>

<tr>

<td>Super + R</td>

<td>Record a screencast.</td>

</tr>

</tbody>

</table>

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
### uncomment this line for xwayland support ###
#modules=xwayland.so

[shell]
background-image=/usr/share/backgrounds/gnome/Aqua.jpg
background-color=0xff002244
panel-color=0x90ff0000
locking=true
animation=zoom
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

[keyboard]
keymap_rules=evdev
#keymap_layout=gb
#keymap_options=caps:ctrl_modifier,shift:both_capslock_cancel
### keymap_options from /usr/share/X11/xkb/rules/base.lst ###

[terminal]
#font=DroidSansMono
#font-size=14

[launcher]
icon=/usr/share/icons/gnome/24x24/apps/utilities-terminal.png
path=/usr/bin/gnome-terminal

[launcher]
icon=/usr/share/icons/gnome/24x24/apps/utilities-terminal.png
path=/usr/bin/weston-terminal

[launcher]
icon=/usr/share/icons/hicolor/24x24/apps/firefox.png
path=/usr/bin/firefox

[launcher]
icon=/usr/share/icons/gnome/24x24/apps/arts.png
path=./clients/flower

[screensaver]
# Uncomment path to disable screensaver
path=/usr/libexec/weston-screensaver
duration=600

[input-method]
path=/usr/libexec/weston-keyboard

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

```

Minimal `weston.ini` :

 `~/.config/weston.ini` 

```
[core]
modules=xwayland.so

[keyboard]
keymap_layout=gb

[launcher]
icon=/usr/share/icons/gnome/24x24/apps/utilities-terminal.png
path=/usr/bin/weston-terminal

[launcher]
icon=/usr/share/icons/hicolor/24x24/apps/firefox.png
path=/usr/bin/firefox

[output]
name=LVDS1
mode=1680x1050
transform=90

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

Experimental wayland support is now in GLFW 3.1 and can be enabled with the `-DGLFW_USE_WAYLAND=ON` CMake option at compile time. You can also install the package [glfw-wayland-git](https://aur.archlinux.org/packages/glfw-wayland-git/)<sup><small>AUR</small></sup> from the AUR.

### EFL

EFL has complete Wayland support. To run a EFL application on Wayland, see Wayland [project page](http://wayland.freedesktop.org/efl.html).

## Window managers and desktop shells

<table class="wikitable">

<tbody>

<tr>

<th>Name</th>

<th>Type</th>

<th>Description</th>

</tr>

<tr>

<td>GNOME</td>

<td>Compositing</td>

<td>See [GNOME#Starting GNOME](/index.php/GNOME#Starting_GNOME "GNOME").</td>

</tr>

<tr>

<td>Hawaii</td>

<td>_(Unclear)_</td>

<td>See [Hawaii](/index.php/Hawaii "Hawaii").</td>

</tr>

<tr>

<td>sway</td>

<td>Tiling</td>

<td>[Sway](/index.php/Sway "Sway") is an i3-compatible window manager for Wayland. [Github](https://github.com/SirCmpwn/sway)</td>

</tr>

<tr>

<td>Enlightenment</td>

<td>_(Unclear)_</td>

<td>Long running minimal Window Manager-turned Wayland compositor. E19 originally had Wayland support but this was removed and now only E20+ Wayland is considered stable enough for regular use. [More Info](https://www.enlightenment.org/about-wayland)</td>

</tr>

<tr>

<td>KDE</td>

<td>Compositing</td>

<td>[KDE](/index.php/KDE "KDE") 4.11 added support for [KWin under Wayland system compositor](http://blog.martin-graesslin.com/blog/2013/06/starting-a-full-kde-plasma-session-in-wayland/). With [KDE Plasma 5.4](https://community.kde.org/KWin/Wayland#Start_a_Plasma_session_on_Wayland), the first technology preview of a Wayland session is released but it is currently targeted for the mobile platform and does not yet allow to use it as a full replacement for Xorg based desktop.</td>

</tr>

<tr>

<td>Orbment</td>

<td>Tiling</td>

<td>[orbment](https://github.com/Cloudef/orbment) (previously loliwm) is a tiling WM for Wayland.</td>

</tr>

<tr>

<td>Velox</td>

<td>Tiling</td>

<td>[velox](https://github.com/michaelforney/velox) is a simple window manager based on swc. It is inspired by [dwm](/index.php/Dwm "Dwm") and [xmonad](/index.php/Xmonad "Xmonad").</td>

</tr>

<tr>

<td>Orbital</td>

<td>Compositing</td>

<td>[Orbital](https://github.com/giucam/orbital) is a Wayland compositor and shell, using Qt5 and Weston. The goal of the project is to build a simple yet flexible and good looking Wayland desktop. It is not a full fledged DE but rather the analogue of a WM in the X11 world, such as [Awesome](/index.php/Awesome "Awesome") or [Fluxbox](/index.php/Fluxbox "Fluxbox").</td>

</tr>

<tr>

<td>Papyros Shell</td>

<td>_(Unclear)_</td>

<td>[Papyros Shell](https://github.com/papyros/papyros-shell) is the desktop shell for [Papyros](/index.php/Papyros "Papyros"), built using QtQuick and QtCompositor as a compositor for Wayland.</td>

</tr>

<tr>

<td>Maynard</td>

<td>_(Unclear)_</td>

<td>[Maynard](https://github.com/raspberrypi/maynard) is a desktop shell client for Weston based on GTK. It was based on weston-gtk-shell, a project by Tiago Vignatti.</td>

</tr>

<tr>

<td>Motorcar</td>

<td>_(Unclear)_</td>

<td>[Motorcar](https://github.com/evil0sheep/motorcar) is a wayland compositor to explore 3D windowing.</td>

</tr>

</tbody>

</table>

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

Retrieved from "[https://wiki.archlinux.org/index.php?title=Wayland&oldid=414293](https://wiki.archlinux.org/index.php?title=Wayland&oldid=414293)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [X server](/index.php/Category:X_server "Category:X server")