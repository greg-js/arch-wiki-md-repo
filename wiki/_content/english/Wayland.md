Related articles

*   [KMS](/index.php/KMS "KMS")
*   [Xorg](/index.php/Xorg "Xorg")

[Wayland](https://wayland.freedesktop.org/) is a protocol for a [compositing window manager](https://en.wikipedia.org/wiki/Compositing_window_manager "wikipedia:Compositing window manager") to talk to its clients, as well as a library implementing the protocol. It is supported on some desktop environments like [GNOME](/index.php/GNOME "GNOME") and [KDE](/index.php/KDE "KDE"). There is also a compositor reference implementation called [Weston](/index.php/Weston "Weston"). XWayland provides a compatibility layer to seamlessly run legacy [X11](/index.php/X11 "X11") applications in Wayland.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Requirements](#Requirements)
*   [2 Compositors](#Compositors)
*   [3 Display managers](#Display_managers)
*   [4 GUI libraries](#GUI_libraries)
    *   [4.1 GTK 3](#GTK_3)
    *   [4.2 Qt 5](#Qt_5)
    *   [4.3 Clutter](#Clutter)
    *   [4.4 SDL2](#SDL2)
    *   [4.5 GLFW](#GLFW)
    *   [4.6 GLEW](#GLEW)
    *   [4.7 EFL](#EFL)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 GDM and NVIDIA proprietary drivers](#GDM_and_NVIDIA_proprietary_drivers)
    *   [5.2 Gamma](#Gamma)
    *   [5.3 LLVM assertion failure](#LLVM_assertion_failure)
    *   [5.4 Slow motion, graphical glitches, and crashes](#Slow_motion,_graphical_glitches,_and_crashes)
    *   [5.5 Cannot open display: :0 with Electron-based applications](#Cannot_open_display:_:0_with_Electron-based_applications)
    *   [5.6 Screen recording](#Screen_recording)
    *   [5.7 Remote display](#Remote_display)
    *   [5.8 Input grabbing in games, remote desktop and VM windows](#Input_grabbing_in_games,_remote_desktop_and_VM_windows)
        *   [5.8.1 wlroots input inhibitor protocol](#wlroots_input_inhibitor_protocol)
*   [6 See also](#See_also)

## Requirements

Most Wayland compositors only work on systems using [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting"). Wayland by itself does not provide a graphical environment; for this you also need a compositor such as [Weston](/index.php/Weston "Weston") or [Sway](/index.php/Sway "Sway"), or a desktop environment that includes a compositor like [GNOME](/index.php/GNOME "GNOME") or [KDE](/index.php/KDE "KDE").

For the GPU driver and Wayland compositor to be compatible they must support the same buffer API. There are two main APIs: [GBM](https://en.wikipedia.org/wiki/Generic_Buffer_Management "wikipedia:Generic Buffer Management") and [EGLStreams](https://www.phoronix.com/scan.php?page=news_item&px=XDC2016-Device-Memory-API).

| Buffer API | GPU driver support | Wayland compositor support |
| GBM | All except [NVIDIA](/index.php/NVIDIA "NVIDIA") | All |
| EGLStreams | [NVIDIA](/index.php/NVIDIA "NVIDIA") | [GNOME](/index.php/GNOME "GNOME"), [KDE](/index.php/KDE "KDE") |

## Compositors

| Name | Type | Description |
| GNOME | Stacking | See [GNOME#Starting](/index.php/GNOME#Starting "GNOME"). |
| sway | Tiling | [Sway](/index.php/Sway "Sway") is an i3-compatible window manager for Wayland. [GitHub](https://github.com/SirCmpwn/sway) |
| Enlightenment | Stacking and tiling | [More Info](https://www.enlightenment.org/about-wayland) |
| KDE Plasma | Stacking | See [KDE#Starting Plasma](/index.php/KDE#Starting_Plasma "KDE") |
| Orbment | Tiling | [orbment](https://github.com/Cloudef/orbment) (previously loliwm) is an abandoned tiling WM for Wayland. |
| Velox | Tiling | [Velox](/index.php/Velox "Velox") is a simple window manager based on swc. It is inspired by [dwm](/index.php/Dwm "Dwm") and [xmonad](/index.php/Xmonad "Xmonad"). |
| Orbital | Stacking | [Orbital](https://github.com/giucam/orbital) is a Wayland compositor and shell (more akin to a WM than a DE) using Qt5 and Weston. The goal of the project is to build a simple but flexible and good looking Wayland desktop. |
| Liri Shell | Stacking | [Liri Shell](https://github.com/lirios/shell) is the desktop shell for [Liri](/index.php/Liri "Liri"), built using QtQuick and QtCompositor as a compositor for Wayland. |
| Maynard | *(Unclear)* | [Maynard](https://github.com/raspberrypi/maynard) is a desktop shell client for Weston based on GTK. It was based on weston-gtk-shell, a project by Tiago Vignatti. Not under development. [[1]](https://github.com/raspberrypi/maynard/issues/54#issuecomment-303422302)[[2]](https://github.com/raspberrypi/maynard/issues/55#issuecomment-373808518) |
| Motorcar | *(Unclear)* | [Motorcar](https://github.com/evil0sheep/motorcar) is a Wayland compositor to explore 3D windowing using virtual reality. |
| Way Cooler | Tiling | [Way Cooler](https://github.com/way-cooler/way-cooler) is a customizable (Lua config files) Wayland compositor written in Rust. Inspired by i3 and awesome. |
| Maze Compositor | Floating 3D | [Maze Compositor](https://github.com/imbavirus/mazecompositor) is a 3D Qt based Wayland compositor |
| Cage | Kiosk | [Cage](https://www.hjdskes.nl/projects/cage/) is a Wayland compositor that displays a single fullscreen application |
| Greenfield | Stacking | [Greenfield](https://github.com/udevbe/greenfield) is a Wayland compositor that runs in a web browser and can display remote applications |
| Grefsen | Floating | [Grefsen](https://github.com/ec1oud/grefsen) is a Qt/Wayland compositor providing a minimal desktop environment. |
| Waymonad | Tiling | [Waymonad](https://github.com/waymonad/waymonad) is a Wayland compositor based on ideas from and inspired by xmonad |
| wayfire | Stacking | [Wayfire](https://github.com/WayfireWM/wayfire) is a general purpose compositor. |
| Weston | Floating | [Weston](/index.php/Weston "Weston") is a Wayland compositor reference implementation. |

Some of the above may support [display managers](/index.php/Display_manager "Display manager"). Check `/usr/share/wayland-sessions/*compositor*.desktop` to see how they are started.

## Display managers

Below listed display managers which supports running Wayland compositors. The Type column indicates whether the display manager supports running on Wayland or not.

| Name | Type | Description |
| GDM | Runs on Wayland | [GNOME](/index.php/GNOME "GNOME") display manager. |
| LightDM | Runs on X11 | Cross-desktop display manager. |
| Ly | Runs in console | TUI display manager written in C |
| SDDM | Runs on X11 | QML-based display manager. |

## GUI libraries

See details on the [official website](https://wayland.freedesktop.org/toolkits.html).

### GTK 3

The [gtk3](https://www.archlinux.org/packages/?name=gtk3) package has the Wayland backend enabled. GTK will default to the Wayland backend, but it is possible to override it to Xwayland by modifying an environment variable: `GDK_BACKEND=x11`.

### Qt 5

To enable Wayland support in Qt 5, install the [qt5-wayland](https://www.archlinux.org/packages/?name=qt5-wayland) package.

To run a Qt 5 app with the Wayland plugin [[3]](https://wiki.qt.io/QtWayland#How_do_I_use_QtWayland.3F), use `-platform wayland` or `QT_QPA_PLATFORM=wayland-egl` [environment variable](/index.php/Environment_variable "Environment variable"). To force the usage of [X11](/index.php/X11 "X11") on a Wayland session, use `QT_QPA_PLATFORM=xcb`.

### Clutter

The Clutter toolkit has a Wayland backend that allows it to run as a Wayland client. The backend is enabled in the [clutter](https://www.archlinux.org/packages/?name=clutter) package.

To run a Clutter app on Wayland, set `CLUTTER_BACKEND=wayland`.

### SDL2

To run a SDL2 application on Wayland, set `SDL_VIDEODRIVER=wayland`.

**Note:** Many proprietary games come bundled with old versions of SDL, which don't support Wayland and might break entirely if you set `SDL_VIDEODRIVER=wayland`. To force the application to run with XWayland, set `SDL_VIDEODRIVER=x11`.

### GLFW

To use GLFW with the Wayland backend, install the [glfw-wayland](https://www.archlinux.org/packages/?name=glfw-wayland) package (instead of [glfw-x11](https://www.archlinux.org/packages/?name=glfw-x11)).

### GLEW

To use GLEW with the Wayland backend, install the [glew-wayland](https://www.archlinux.org/packages/?name=glew-wayland) package (instead of [glew](https://www.archlinux.org/packages/?name=glew)).

### EFL

EFL has complete Wayland support. To run a EFL application on Wayland, see Wayland [project page](https://wayland.freedesktop.org/efl.html).

## Troubleshooting

### GDM and NVIDIA proprietary drivers

If you are using the proprietary [NVIDIA](/index.php/NVIDIA "NVIDIA") driver, [GDM](/index.php/GDM "GDM") explicitly [disables](https://bbs.archlinux.org/viewtopic.php?pid=1837424#p1837424) Wayland support. The [rationale](https://gitlab.gnome.org/GNOME/gdm/commit/5cd78602d3d4c8355869151875fc317e8bcd5f08) for this decision is that GLX applications currently do not work well when the proprietary NVIDIA driver is used with a Wayland session.

To force-enable Wayland, disable the [udev](/index.php/Udev "Udev") rule responsible for disabling Wayland in GDM:

```
# ln -s /dev/null /etc/udev/rules.d/61-gdm.rules

```

### Gamma

While [Redshift](/index.php/Redshift "Redshift") doesn't support Wayland (without a patch) it is possible to apply the desired temperature in [tty](/index.php/Tty "Tty") before starting a compositor. For example:

```
redshift -m drm -PO 3000

```

Otherwise some compositors feature this option during runtime:

*   [GNOME](/index.php/GNOME "GNOME") provides features like [Redshift](/index.php/Redshift "Redshift") out-of-the-box and has Wayland support. Enable [Night Light](/index.php/GNOME#Night_Light "GNOME") in Display settings.
*   Likewise, [KDE Plasma](/index.php/KDE_Plasma "KDE Plasma") also provides *Night Color*.
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

### Cannot open display: :0 with Electron-based applications

Make sure you haven't set GDK_BACKEND=wayland. Setting it globally will break Electron apps.

### Screen recording

[green-recorder](https://aur.archlinux.org/packages/green-recorder/), [obs-gnome-screencast](https://aur.archlinux.org/packages/obs-gnome-screencast/) and [obs-xdg-portal-git](https://aur.archlinux.org/packages/obs-xdg-portal-git/) support screen recording on Wayland using GNOME screencast feature.

[wf-recorder-git](https://aur.archlinux.org/packages/wf-recorder-git/) is a video recorder for wlroots-based compositors.

[wlrobs-hg](https://aur.archlinux.org/packages/wlrobs-hg/) is a [obs-studio](https://www.archlinux.org/packages/?name=obs-studio) plugin that allows you to screen capture on wlroots-based compositors.

### Remote display

*   (20190503) [wlroots](https://www.archlinux.org/packages/?name=wlroots) (used by [sway](/index.php/Sway "Sway")) offers an RDP backend since version 0.6 [[4]](https://github.com/swaywm/wlroots/blob/master/docs/env_vars.md).
*   (20180401) [mutter](https://www.archlinux.org/packages/?name=mutter) has now remote desktop enabled at compile time, see [[5]](https://wiki.gnome.org/Projects/Mutter/RemoteDesktop) and [gnome-remote-desktop](https://www.archlinux.org/packages/?name=gnome-remote-desktop) for details.
*   There was a merge of FreeRDP into Weston in 2013, enabled via a compile flag. The [weston](https://www.archlinux.org/packages/?name=weston) package has it enabled since version 6.0.0.
*   [waypipe-git](https://aur.archlinux.org/packages/waypipe-git/) is a transparent proxy for Wayland applications, with a wrapper command to run over [SSH](/index.php/SSH "SSH")

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
Sway and wlroots do not support the `Compositor shortcuts inhibit` and `XWayland keyboard grabbing` protocols, and it seems they are against adding support for the latter [[6]](https://github.com/swaywm/wlroots/pull/635#issuecomment-366385856) [[7]](https://github.com/swaywm/wlroots/issues/624#issuecomment-367276476).
No widget toolkit or application is known to support this protocol.

## See also

*   [Article about Wayland debugging on Fedora Wiki](https://fedoraproject.org/wiki/How_to_debug_Wayland_problems)
*   [Cursor themes](/index.php/Cursor_themes "Cursor themes")
*   [Arch Linux forum discussion](https://bbs.archlinux.org/viewtopic.php?id=107499)
*   [Wayland documentation online](https://wayland.freedesktop.org/docs/html/)