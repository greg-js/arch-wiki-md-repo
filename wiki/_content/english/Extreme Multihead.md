Related articles

*   [Xorg#Monitor settings](/index.php/Xorg#Monitor_settings "Xorg")
*   [Multihead](/index.php/Multihead "Multihead")
*   [xrandr](/index.php/Xrandr "Xrandr")

Several monitors can be attached to a single computer system. Many years ago this was only possible by installing two or more video cards in a computer. Then some high-end video cards began appearing with outputs for two monitors. Nowadays, most laptops come with a main display and a socket for an external monitor while the integrated video cards on desktop systems provide VGA + DVI + HDMI outputs as standard. If you plug in multiple monitors to whatever video sockets you have available, they will more often than not "just work" - offering two or more versions of the same display. In some cases this is exactly what is required; allowing the same desktop to be viewed from different directions.

It is also possible to have these multiple monitors work together as an extended single desktop. It is even possible to join the displays from several computers - each with single or multiple monitors - into one very large extended desktop.

This document describes how to configure such a system.

## Contents

*   [1 Experimenting with multiple monitors](#Experimenting_with_multiple_monitors)
    *   [1.1 Loading configuration at X start](#Loading_configuration_at_X_start)
*   [2 Make settings the default](#Make_settings_the_default)
    *   [2.1 05-device.conf](#05-device.conf)
    *   [2.2 10-monitor.conf](#10-monitor.conf)
*   [3 Extending a desktop beyond the local system](#Extending_a_desktop_beyond_the_local_system)
    *   [3.1 Synergy](#Synergy)
    *   [3.2 Xdmx](#Xdmx)
    *   [3.3 VNC](#VNC)

## Experimenting with multiple monitors

The easiest way to begin experimenting with multiple monitors is start with a system which has a working X set-up supporting a single monitor. If you already have the additional equipment installed

*   a video card with multiple video outputs or multiple video cards
*   monitors plugged into each of the video outputs

When everything is on you should see the same output on each monitor. The desktop is "cloned" on to the secondary monitors. If all the monitors are not exactly the same shape or support different resolutions you may only see portions of the main desktop display.

The best tool to experiment with configuring your monitors to display as you want is `xrandr`. This may already installed as part of your Xorg installation from either the xorg or xorg-apps packages.

Use *xrandr* to experiment with different configurations until you arrive at settings you want to make permanent. The [DualScreen](/index.php/DualScreen "DualScreen") and [xrandr](/index.php/Xrandr "Xrandr") pages, the man page and various locations on the web provide more information on using the tool.

For example, the following command configures my dual monitor set-up:

```
$ xrandr --output VGA-1 --rotate left --output VGA-1 --pos 0x0 --output DVI-0 --rotate left  --output DVI-0 --pos 1080x0

```

I have two monitor devices with the logical names `VGA-1` and `DVI-0`. These names can be determined using the command `xrandr -q` or even searching through the X.org log-file `/var/log/Xorg.0.log`. Both monitors are identical (with a resolution of 1920x1080) and can rotate or pivot from a landscape to a portrait orientation.

1.  VGA-1 is rotated 90 counter-clockwise from landscape to portrait `--output VGA-1 --rotate left`
2.  VGA-1 is the main display, the position of other monitors will be measured relative to its top, left corner `--output VGA-1 --pos 0x0`
3.  DVI-0 is also rotated `--output DVI-0 --rotate left`
4.  DVI-0 sits immediately to the right of VGA-1 `--output DVI-0 --pos 1080x0`

If you have not done so already, create a simple batch script containing your desired xrandr command. Save it somewhere useful; /usr/local/bin perhaps. Your system can then be configured to call this script as you login to your account as your window manager starts. There are different locations for saving initialisation commands and indeed some Settings tools can add these commands in place for you.

### Loading configuration at X start

Add the command to either to individual or system xinitrc scripts. Add a line after the window manager has been started but before any applications are called. Execution of the command is usually quite noticeable as the monitors change from the basic cloned, landscape display to the independent portrait mode.

**Note:** This will only work if X is started manually, not from a display manager such as kdm, gdm, slim or whatever.

*   system-wide initialisation file is `/etc/X11/xinit/xinitrc`
*   a user's personal initialisation file is `~/.xinitrc`

## Make settings the default

Now you have your regular desktop spanning multiple monitors, it would be better if

*   the irritating flicker as the monitors change did not happen as you login
*   the login manager was also set to span multiple monitors; this is especially irritating if your monitors are rotated, like mine, so you have to turn your head 90 as you login

All that has to be done is to create an Xorg configuration file that serves the same purpose as the xrandr command; easy now we know what the configuration should be.

We need to create two files:

*   `05-device.conf` to specify how the monitor configuration can be found for the video device
*   `10-monitor` to specify the actual configuration of the monitors

These configuration files, and others you may need to manage your keyboard, mouse and other devices have a multitude of options available described in [Multihead](/index.php/Multihead "Multihead") and Xorg documentation; the examples below are offered to illustrate a particular solution.

**Note:** Since Xorg moved away from a monolithic configuration file that required every option to be spelled out to the lighter multiple configuration files only over-riding a default configuration, you only need to be concerned with specifying the exact changes you want; do not simply copy from these examples

### 05-device.conf

This is used to reference the individual monitor configurations by naming the devices. This configuration files should be loaded before the monitor file and so has a lower number ""05""

```
Section "Device"
    Identifier "radeon"
    Driver "ati"
    Option "monitor-VGA-1" "VGA"
    Option "monitor-DVI-0" "DVI"
EndSection

```

The `Identifier` should match the actual video device; check `/var/log/Xorg.0.log` to confirm this. Similarly, `Driver` corresponds to the driver. Then we reference the two monitors by name pointing to relevant sections in the 10-monitor.conf file

*   `monitor-VGA-1` specifies the name that Xorg will detect the monitors as; the same names the `xrandr -q` reported to us; the name is prefixed with **"monitor-"**
*   `VGA` specifies the identifier we will use to refer to this monitor

Essentially we are specifying a relationship between the actual device and its configuration.

### 10-monitor.conf

This file then specifies how we want the monitors to be configured. The file name is not important other than ensuring to is loaded after the `device` file. The important elements are the Section name and its Identifier:

```
Section "Monitor"
    Identifier "VGA"
    Option "Rotate" "Left"
EndSection

Section "Monitor"
    Identifier "DVI"
    Option "Rotate" "Left"
    Option "RightOf " "VGA"
EndSection

```

*   `Option "Rotate" "Left"` rotates each monitor counter-clockwise 90
*   `Option "RightOf" VGA` places the monitor identified as DVI to the right of the monitor whose Identifier is VGA. Other possibilities include "LeftOf", "Above" and "Below"

With these configuration files in place and all references to xrandr removes, the display manager can be restarted and

1.  the display manager should start with all monitors correctly placed and oriented
2.  user login will no longer flash as xrandr executes

When you login, some window managers may attempt to reset this configuration with the result that your logged-in desktop has reverted to a pair of cloned displays and in some cases a panel stretching to a now, non-existent monitor. The 4.10 & 4.11 versions of XFCE4 will do this. This bad behaviour can usually be resolved by configuring your monitor set-up using the window manager tools and configuration files. For XFCE4, this is explained in [Xfce#Multiple monitors](/index.php/Xfce#Multiple_monitors "Xfce")

## Extending a desktop beyond the local system

The previous section outlined how to access other systems usually not close to your desktop. This section examines how to access systems which are very close to your desktop in such a way that it appears your desktop has been extended still further to incorporate these additional monitors. There are two possibilities

*   **synergy** this tool allows your keyboard and mouse to access remote systems by making your desktop seem to extend onto the remote desktop. Simply by moving your mouse off the edge of your desktop it will appear on a remote system where both mouse and keyboard can interact with the remote systems GUI (i.e. synergy can connect Macs and Windows systems too). Windows cannot be dragged across system boundaries and indeed applications launched through a remote systems GUI, run on the remote system. For an integrated Linux desktop, disk shares also need to be set-up
*   **Xdmx** a proxy server for X allows the X server on remote systems to contribute its monitor to the desktop of a master system. In this case the destop is genuinely extending onto remote systems; windows can be dragged across system boundaries and applications launched from a remote monitor run on the local, master system. In this environment, the remote systems need only provide sufficient resources to run an X session.

### Synergy

Using a tool called [Synergy](/index.php/Synergy "Synergy") it is possible for a single keyboard and mouse to access several systems as though all their monitors were a single desktop.

[quicksynergy](https://aur.archlinux.org/packages/quicksynergy/) provides a convenient wrapper for the application.

### Xdmx

Xdmx is a proxy server for X. Using it, the monitors from any number of systems can be consolidated into a single desktop or constructed as a *wall* of monitors.

To establish an Xdmx desktop involves the following steps automated so that the construction appears transparent:

1.  on each system configure and initiate a minimal X session; a minimal twm session is enough
2.  authorise the master system to access X resources on each remote system (use xhost +)
3.  install [xorg-server-xdmx](https://www.archlinux.org/packages/?name=xorg-server-xdmx) on the master system
4.  initiate a minimal X session on the master system
5.  configure the desired Xdmx session
6.  initiate the Xdmx session with an appropriate window manager as a working desktop

At present either Xdmx itself or the current state of window managers do not work well together for complex arrangements of multihead set-ups; the server tends to crash as soon as window drawing is required after the integrated desktop has been established.

### VNC

Using [X11vnc](/index.php/X11vnc "X11vnc"), [tigervnc](/index.php/Tigervnc "Tigervnc") and [Xrandr](/index.php/Xrandr "Xrandr") it is possible to create and share virtual monitors for display on the local network.

First, create at-least one virtual display in xorg

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
    Identifier "intelgpu0"
    Driver "intel"
    Option "VirtualHeads" "1"
EndSection

```

This virtual display can then be activated using.

```
$ xrandr --output <virtual display> --mode<resolution>   

```

At this point, this display may be further configured either through DE tools or xrandr itself.

To share the display using X11vnc, run:

```
$ x11vnc -display :0 -clip <resolution>+<offset> -multiptr -forever  

```

This vnc instance can then be displayed on the remote machine by running

```
$ vncviewer -shared -ViewOnly -Fullscreen <host ip>

```

While functional, this can suffer from poor performance over low-bandwidth connections.