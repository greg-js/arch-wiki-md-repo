# Xorg

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Start X at login](/index.php/Start_X_at_login "Start X at login")
*   [Autostarting](/index.php/Autostarting "Autostarting")
*   [Display manager](/index.php/Display_manager "Display manager")
*   [Window manager](/index.php/Window_manager "Window manager")
*   [Font configuration](/index.php/Font_configuration "Font configuration")
*   [Cursor themes](/index.php/Cursor_themes "Cursor themes")
*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Wayland](/index.php/Wayland "Wayland")
*   [Mir](/index.php/Mir "Mir")
*   [Xinitrc](/index.php/Xinitrc "Xinitrc")

From [http://www.x.org/wiki/](http://www.x.org/wiki/):

_The X.Org project provides an open source implementation of the X Window System. The development work is being done in conjunction with the freedesktop.org community. The X.Org Foundation is the educational non-profit corporation whose Board serves this effort, and whose Members lead this work._

**Xorg** is the open-source reference implementation of the X window system version 11\. Since Xorg is the most popular choice among Linux users, its ubiquity has led to making it an ever-present requisite for GUI applications, resulting in massive adoption from most distributions. See the [Xorg](https://en.wikipedia.org/wiki/X.Org_Server "wikipedia:X.Org Server") Wikipedia article or visit the [Xorg website](http://www.x.org/wiki/) for more details.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Driver installation](#Driver_installation)
*   [2 Running](#Running)
    *   [2.1 Display manager](#Display_manager)
    *   [2.2 Manually](#Manually)
*   [3 Configuration](#Configuration)
    *   [3.1 Using .conf files](#Using_.conf_files)
    *   [3.2 Using xorg.conf](#Using_xorg.conf)
*   [4 Input devices](#Input_devices)
    *   [4.1 Mouse acceleration](#Mouse_acceleration)
    *   [4.2 Extra mouse buttons](#Extra_mouse_buttons)
    *   [4.3 Touchpad](#Touchpad)
    *   [4.4 Touchscreen](#Touchscreen)
    *   [4.5 Keyboard settings](#Keyboard_settings)
*   [5 Monitor settings](#Monitor_settings)
    *   [5.1 Getting started](#Getting_started)
    *   [5.2 Multiple monitors](#Multiple_monitors)
        *   [5.2.1 More than one graphics card](#More_than_one_graphics_card)
    *   [5.3 Display size and DPI](#Display_size_and_DPI)
        *   [5.3.1 Setting DPI manually](#Setting_DPI_manually)
            *   [5.3.1.1 Proprietary NVIDIA driver](#Proprietary_NVIDIA_driver)
    *   [5.4 DPMS](#DPMS)
*   [6 Composite](#Composite)
    *   [6.1 List of composite managers](#List_of_composite_managers)
*   [7 Tips and tricks](#Tips_and_tricks)
    *   [7.1 X startup tweaking (startx)](#X_startup_tweaking_.28startx.29)
    *   [7.2 Nested X session](#Nested_X_session)
    *   [7.3 Starting GUI programs remotely](#Starting_GUI_programs_remotely)
    *   [7.4 On-demand disabling and enabling of input sources](#On-demand_disabling_and_enabling_of_input_sources)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 General](#General)
    *   [8.2 Black screen, No protocol specified.., Resource temporarily unavailable for all or some users](#Black_screen.2C_No_protocol_specified...2C_Resource_temporarily_unavailable_for_all_or_some_users)
    *   [8.3 CTRL right key does not work with oss keymap](#CTRL_right_key_does_not_work_with_oss_keymap)
    *   [8.4 DRI with Matrox cards stops working](#DRI_with_Matrox_cards_stops_working)
    *   [8.5 Frame-buffer mode problems](#Frame-buffer_mode_problems)
    *   [8.6 Launching multiple X sessions with proprietary NVIDIA on Xorg 1.16](#Launching_multiple_X_sessions_with_proprietary_NVIDIA_on_Xorg_1.16)
    *   [8.7 Program requests "font '(null)'"](#Program_requests_.22font_.27.28null.29.27.22)
    *   [8.8 Recovery: disabling Xorg before GUI login](#Recovery:_disabling_Xorg_before_GUI_login)
    *   [8.9 X clients started with "su" fail](#X_clients_started_with_.22su.22_fail)
    *   [8.10 X failed to start: Keyboard initialization failed](#X_failed_to_start:_Keyboard_initialization_failed)
    *   [8.11 Rootless Xorg (v1.16)](#Rootless_Xorg_.28v1.16.29)
        *   [8.11.1 Broken redirection](#Broken_redirection)
    *   [8.12 Why do I get a green screen whenever I try to watch a video?](#Why_do_I_get_a_green_screen_whenever_I_try_to_watch_a_video.3F)

## Installation

Xorg can be [installed](/index.php/Install "Install") with the [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) package.

Additionally, some packages from the [xorg-server-utils](https://www.archlinux.org/packages/?name=xorg-server-utils) meta-package are necessary for certain configuration tasks, they are pointed out in the relevant sections. Other useful packages are in the [xorg-apps](https://www.archlinux.org/groups/x86_64/xorg-apps/) group.

**Tip:** You will typically seek to install a [window manager](/index.php/Window_manager "Window manager") or a [desktop environment](/index.php/Desktop_environment "Desktop environment") to supplement X.

### Driver installation

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Too cryptic for an introduction (Discuss in [Talk:Xorg#](https://wiki.archlinux.org/index.php/Talk:Xorg))

The Linux kernel includes open-source video drivers and support for hardware accelerated framebuffers. However, userland support is required for OpenGL and 2D acceleration in X11.

First, identify your card:

```
$ lspci | grep -e VGA -e 3D

```

Then install an appropriate driver. You can search the package database for a complete list of open-source video drivers:

```
$ pacman -Ss xf86-video

```

The default graphics driver is [xf86-video-vesa](https://www.archlinux.org/packages/?name=xf86-video-vesa), which handles a large number of chipsets but does not include any 2D or 3D acceleration. If a better driver cannot be found or fails to load, Xorg will fall back to _vesa_.

In order for video acceleration to work, and often to expose all the modes that the GPU can set, a proper video driver is required:

**Note:** If you have a NVIDIA Optimus enabled laptop which uses an integrated video card combined with a dedicated GPU, see [Bumblebee](/index.php/Bumblebee "Bumblebee").

<table class="wikitable" style="text-align:center">

<tbody>

<tr>

<th>Brand</th>

<th>Type</th>

<th>Driver</th>

<th>[Multilib](/index.php/Multilib "Multilib")</th>

<th>Documentation</th>

</tr>

<tr>

<td rowspan="3" style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">**AMD/ATI**</td>

<td rowspan="2">Open source</td>

<td>[xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu)</td>

<td rowspan="2">[lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl)</td>

<td rowspan="2">[ATI](/index.php/ATI "ATI")</td>

</tr>

<tr>

<td>[xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati)</td>

</tr>

<tr>

<td>Proprietary</td>

<td>[catalyst](https://aur.archlinux.org/packages/catalyst/)<sup><small>AUR</small></sup></td>

<td>[lib32-catalyst-libgl](https://aur.archlinux.org/packages/lib32-catalyst-libgl/)<sup><small>AUR</small></sup></td>

<td>[AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst")</td>

</tr>

<tr>

<td style="background: #aff; color: inherit; vertical-align: middle; text-align: center;">**Intel**</td>

<td>Open source</td>

<td>[xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)</td>

<td>[lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl)</td>

<td>[Intel graphics](/index.php/Intel_graphics "Intel graphics")</td>

</tr>

<tr>

<td rowspan="4" style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">**Nvidia**</td>

<td>Open source</td>

<td>[xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau)</td>

<td>[lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl)</td>

<td>[Nouveau](/index.php/Nouveau "Nouveau")</td>

</tr>

<tr>

<td rowspan="3">Proprietary</td>

<td>[nvidia](https://www.archlinux.org/packages/?name=nvidia)</td>

<td>[lib32-nvidia-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-libgl)</td>

<td rowspan="3">[NVIDIA](/index.php/NVIDIA "NVIDIA")</td>

</tr>

<tr>

<td>[nvidia-340xx](https://www.archlinux.org/packages/?name=nvidia-340xx)</td>

<td>[lib32-nvidia-340xx-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-340xx-libgl)</td>

</tr>

<tr>

<td>[nvidia-304xx](https://www.archlinux.org/packages/?name=nvidia-304xx)</td>

<td>[lib32-nvidia-304xx-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-304xx-libgl)</td>

</tr>

</tbody>

</table>

Other video drivers can be found in the [xorg-drivers](https://www.archlinux.org/groups/x86_64/xorg-drivers/) group.

Xorg should run smoothly without closed source drivers, which are typically needed only for advanced features such as fast 3D-accelerated rendering for games.

## Running

### Display manager

A convenient way to start X, but one that requires an additional application and dependencies, is by using a [display manager](/index.php/Display_manager "Display manager").

### Manually

To start the X server without a display manager, see [Xinitrc](/index.php/Xinitrc "Xinitrc").

## Configuration

**Note:** Arch supplies default configuration files in `/usr/share/X11/xorg.conf.d`, and no extra configuration is necessary for most setups.

Xorg uses a configuration file called `xorg.conf` and files ending in the suffix `.conf` for its initial setup: the complete list of the folders where these files are searched can be found at [[1]](http://www.x.org/releases/current/doc/man/man5/xorg.conf.5.xhtml) or by running `man xorg.conf`, together with a detailed explanation of all the available options.

### Using .conf files

The `/etc/X11/xorg.conf.d/` directory stores host-specific configuration. You are free to add configuration files there, but they must have a `.conf` suffix: the files are read in ASCII order, and by convention their names start with `_XX_-` (two digits and a hyphen, so that for example 10 is read before 20). These files are parsed by the X server upon startup and are treated like part of the traditional `xorg.conf` configuration file. The X server essentially treats the collection of configuration files as one big file with entries from `xorg.conf` at the end.

### Using xorg.conf

Xorg can also be configured via `/etc/X11/xorg.conf` or `/etc/xorg.conf`. You can also generate a skeleton for `xorg.conf` with:

```
# Xorg :0 -configure

```

This should create a `xorg.conf.new` file in `/root/` that you can copy over to `/etc/X11/xorg.conf`.

**Tip:** If you are already running an X server, use a different display, for example `Xorg :2 -configure`.

Alternatively, your proprietary video card drivers may come with a tool to automatically configure Xorg: see the article of your video driver, [NVIDIA](/index.php/NVIDIA "NVIDIA") or [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst"), for more details.

**Note:** Configuration file keywords are case insensitive, and "_" characters are ignored. Most strings (including Option names) are also case insensitive, and insensitive to white space and "_" characters.

## Input devices

[Udev](/index.php/Udev "Udev") will detect your hardware and [evdev](https://en.wikipedia.org/wiki/evdev "wikipedia:evdev") will act as the hotplugging input driver for almost all devices. Udev is provided by [systemd](https://www.archlinux.org/packages/?name=systemd) and [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev) is required by [xorg-server](https://www.archlinux.org/packages/?name=xorg-server), so there is no need to explicitly install those packages.

You should have `10-evdev.conf` in the `/usr/share/X11/xorg.conf.d/` directory, which manages keyboards, mice, touchpads and touchscreens.

If evdev does not support your device, install the needed driver from the [xorg-drivers](https://www.archlinux.org/groups/x86_64/xorg-drivers/) group. Alike evdev, [libinput](/index.php/Libinput "Libinput") ([xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput)) is a driver which supports a wide array of hardware from all device categories.

See the following pages for specific instructions, or the [Fedora wiki](https://fedoraproject.org/wiki/Input_device_configuration) entry for more examples.

### Mouse acceleration

See [Mouse acceleration](/index.php/Mouse_acceleration "Mouse acceleration").

### Extra mouse buttons

See [All Mouse Buttons Working](/index.php/All_Mouse_Buttons_Working "All Mouse Buttons Working").

### Touchpad

See [Synaptics](/index.php/Synaptics "Synaptics") or [libinput](/index.php/Libinput "Libinput").

### Touchscreen

See [Touchscreen](/index.php/Touchscreen "Touchscreen").

### Keyboard settings

See [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg").

## Monitor settings

### Getting started

**Note:** Newer versions of Xorg are auto-configuring, you should not need to use this.

First, create a new config file, such as `/etc/X11/xorg.conf.d/10-monitor.conf`.

 `/etc/X11/xorg.conf.d/10-monitor.conf` 

```
Section "Monitor"
    Identifier             "Monitor0"
EndSection

Section "Device"
    Identifier             "Device0"
    Driver                 "vesa" #Choose the driver used for this monitor
EndSection

Section "Screen"
    Identifier             "Screen0"  #Collapse Monitor and Device section to Screen section
    Device                 "Device0"
    Monitor                "Monitor0"
    DefaultDepth           16 #Choose the depth (16||24)
    SubSection             "Display"
        Depth              16
        Modes              "1024x768_75.00" #Choose the resolution
    EndSubSection
EndSection

```

**Note:** By default, Xorg needs to be able to detect a monitor and will not start otherwise. A workaround is to create a configuration file such as the example above and thus avoid auto-configuring. A common case where this is necessary is a headless system, which boots without a monitor and starts Xorg automatically, either from a [virtual console](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console") at [login](/index.php/Start_X_at_login "Start X at login"), or from a [display manager](/index.php/Display_manager "Display manager").

### Multiple monitors

See main article [Multihead](/index.php/Multihead "Multihead") for general information.

See also GPU-specific instructions:

*   [NVIDIA#Multiple monitors](/index.php/NVIDIA#Multiple_monitors "NVIDIA")
*   [Nouveau#Dual Head](/index.php/Nouveau#Dual_Head "Nouveau")
*   [AMD Catalyst#Double Screen (Dual Head / Dual Screen / Xinerama)](/index.php/AMD_Catalyst#Double_Screen_.28Dual_Head_.2F_Dual_Screen_.2F_Xinerama.29 "AMD Catalyst")
*   [ATI#Dual Head setup](/index.php/ATI#Dual_Head_setup "ATI")

#### More than one graphics card

You must define the correct driver to use and put the bus ID of your graphic cards.

```
Section "Device"
    Identifier             "Screen0"
    Driver                 "nouveau"
    BusID                  "PCI:0:12:0"
EndSection

Section "Device"
    Identifier             "Screen1"
    Driver                 "radeon"
    BusID                  "PCI:1:0:0"
EndSection

```

To get your bus ID:

 `$ lspci | grep VGA` 

```
01:00.0 VGA compatible controller: nVidia Corporation G96 [GeForce 9600M GT] (rev a1)

```

The bus ID here is 1:0:0.

### Display size and DPI

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** Xorg always sets dpi to 96\. See [this](https://bugs.freedesktop.org/show_bug.cgi?id=23705), [this](https://bugs.freedesktop.org/show_bug.cgi?id=41115) and finally [this](http://pastebin.com/vtzyBK6e). (Discuss in [Talk:Xorg#](https://wiki.archlinux.org/index.php/Talk:Xorg))

The DPI of the X server is determined in the following manner:

1.  The -dpi command line option has highest priority.
2.  If this is not used, the DisplaySize setting in the X config file is used to derive the DPI, given the screen resolution.
3.  If no DisplaySize is given, the monitor size values from DDC are used to derive the DPI, given the screen resolution.
4.  If DDC does not specify a size, 75 DPI is used by default.

In order to get correct dots per inch (DPI) set, the display size must be recognized or set. Having the correct DPI is especially necessary where fine detail is required (like font rendering). Previously, manufacturers tried to create a standard for 96 DPI (a 10.3" diagonal monitor would be 800x600, a 13.2" monitor 1024x768). These days, screen DPIs vary and may not be equal horizontally and vertically. For example, a 19" widescreen LCD at 1440x900 may have a DPI of 89x87\. To be able to set the DPI, the Xorg server attempts to auto-detect your monitor's physical screen size through the graphic card with [DDC](https://en.wikipedia.org/wiki/Display_Data_Channel "wikipedia:Display Data Channel"). <s>When the Xorg server knows the physical screen size, it will be able to set the correct DPI depending on resolution size.</s>

To see if your display size and DPI are detected/calculated correctly:

```
$ xdpyinfo | grep -B2 resolution

```

Check that the dimensions match your display size. If the Xorg server is not able to correctly calculate the screen size, it will default to 75x75 DPI and you will have to calculate it yourself.

If you have specifications on the physical size of the screen, they can be entered in the Xorg configuration file so that the proper DPI is calculated:

```
Section "Monitor"
    Identifier             "Monitor0"
    DisplaySize             286 179    # In millimeters
EndSection

```

If you only want to enter the specification of your monitor **without** creating a full xorg.conf create a new config file. For example (`/etc/X11/xorg.conf.d/90-monitor.conf`):

```
Section "Monitor"
    Identifier             "<default monitor>"
    DisplaySize            286 179    # In millimeters
EndSection

```

If you do not have specifications for physical screen width and height (most specifications these days only list by diagonal size), you can use the monitor's native resolution (or aspect ratio) and diagonal length to calculate the horizontal and vertical physical dimensions. Using the Pythagorean theorem on a 13.3" diagonal length screen with a 1280x800 native resolution (or 16:10 aspect ratio):

```
$ echo 'scale=5;sqrt(1280^2+800^2)' | bc  # 1509.43698

```

This will give the pixel diagonal length and with this value you can discover the physical horizontal and vertical lengths (and convert them to millimeters):

```
$ echo 'scale=5;(13.3/1509)*1280*25.4' | bc  # 286.43072
$ echo 'scale=5;(13.3/1509)*800*25.4'  | bc  # 179.01920

```

**Note:** This calculation works for monitors with square pixels; however, there is the seldom monitor that may compress aspect ratio (e.g 16:10 aspect resolution to a 16:9 monitor). If this is the case, you should measure your screen size manually.

#### Setting DPI manually

**Note:** While you can set any dpi you like and applications using Qt and GTK will scale accordingly, it's recommended to set it to 96, 120 (25% higher), 144 (50% higher), 168 (75% higher), 192 (100% higher) etc., to reduce scaling artifacts to GUI that use bitmaps. Reducing it below 96 dpi may not reduce size of graphical elements of GUI as typically the lowest dpi the icons are made for is 96.

For RandR compliant drivers (for example the open source ATI driver), you can set it by:

```
$ xrandr --dpi 144

```

**Note:** Applications that comply with the setting will not change immediately. You have to start them anew.

See [Execute commands after X start](/index.php/Execute_commands_after_X_start "Execute commands after X start") to make it permanent.

##### Proprietary NVIDIA driver

DPI can be set manually if you only plan to use one resolution ([DPI calculator](http://pxcalc.com/)):

```
Section "Monitor"
    Identifier             "Monitor0"
    Option                 "DPI" "96 x 96"
EndSection

```

You can manually set the DPI adding the options below on `/etc/X11/xorg.conf.d/20-nvidia.conf` (inside **Device** section):

```
Option              "UseEdidDpi" "False"
Option              "DPI" "96 x 96"

```

### DPMS

DPMS (Display Power Management Signaling) is a technology that allows power saving behaviour of monitors when the computer is not in use. This will allow you to have your monitors automatically go into standby after a predefined period of time. See: [DPMS](/index.php/DPMS "DPMS")

## Composite

The Composite extension for X causes an entire sub-tree of the window hierarchy to be rendered to an off-screen buffer. Applications can then take the contents of that buffer and do whatever they like. The off-screen buffer can be automatically merged into the parent window or merged by external programs, called compositing managers. See the following article for more information: [compositing window manager](https://en.wikipedia.org/wiki/Compositing_window_manager "wikipedia:Compositing window manager")

### List of composite managers

*   **[Cairo Composite Manager](/index.php/Cairo_Compmgr "Cairo Compmgr")** — Cairo based composite manager

[http://cairo-compmgr.tuxfamily.org/](http://cairo-compmgr.tuxfamily.org/) || [cairo-compmgr-git](https://aur.archlinux.org/packages/cairo-compmgr-git/)<sup><small>AUR</small></sup>

*   **[Compiz](/index.php/Compiz "Compiz")** — Composite manager for Aiglx and Xgl, with plugins and CCSM

[http://www.compiz.org/](http://www.compiz.org/) || [compiz](https://aur.archlinux.org/packages/compiz/)<sup><small>AUR</small></sup>

*   **[Compton](/index.php/Compton "Compton")** — Compositor (a fork of xcompmgr-dana)

[https://github.com/chjj/compton](https://github.com/chjj/compton) || [compton](https://aur.archlinux.org/packages/compton/)<sup><small>AUR</small></sup>

*   **[Xcompmgr](/index.php/Xcompmgr "Xcompmgr")** — Composite window-effects manager

[http://cgit.freedesktop.org/xorg/app/xcompmgr/](http://cgit.freedesktop.org/xorg/app/xcompmgr/) || [xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr)

*   **Unagi** — Modular compositing manager which aims written in C and based on XCB

[http://projects.mini-dweeb.org/projects/unagi](http://projects.mini-dweeb.org/projects/unagi) || [unagi](https://aur.archlinux.org/packages/unagi/)<sup><small>AUR</small></sup>

## Tips and tricks

### X startup tweaking (startx)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** `/usr/bin/startx` should not be modified, _startx_ recognises the options as command line arguments (Discuss in [Talk:Xorg#](https://wiki.archlinux.org/index.php/Talk:Xorg))

For X's option reference see:

```
$ man Xserver

```

The following options have to be appended to the variable `"defaultserverargs"` in the `/usr/bin/startx` file:

*   Enable deferred glyph loading for 16 bit fonts:

```
-deferglyphs 16

```

**Note:** If you start X with kdm, the startx script does not seem to be executed. X options must be appended to the variable `ServerArgsLocal` in the `/usr/share/config/kdm/kdmrc` file.

### Nested X session

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** mention [xephyr](/index.php/Awesome#Using_Xephyr "Awesome") (Discuss in [Talk:Xorg#](https://wiki.archlinux.org/index.php/Talk:Xorg))

To run a nested session of another desktop environment:

```
$ /usr/bin/Xnest :1 -geometry 1024x768+0+0 -ac -name Windowmaker & wmaker -display :1

```

This will launch a Window Maker session in a 1024 by 768 window within your current X session.

This needs the package [xorg-server-xnest](https://www.archlinux.org/packages/?name=xorg-server-xnest) to be installed.

### Starting GUI programs remotely

See main article: [SSH#X11 forwarding](/index.php/SSH#X11_forwarding "SSH").

### On-demand disabling and enabling of input sources

With the help of _xinput_ you can temporarily disable or enable input sources. This might be useful, for example, on systems that have more than one mouse, such as the ThinkPads and you would rather use just one to avoid unwanted mouse clicks.

[Install](/index.php/Install "Install") the [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput) package from the [official repositories](/index.php/Official_repositories "Official repositories").

Find the ID of the device you want to disable:

```
$ xinput

```

For example in a Lenovo ThinkPad T500, the output looks like this:

 `$ xinput` 

```
⎡ Virtual core pointer                          id=2    [master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer                id=4    [slave  pointer  (2)]
⎜   ↳ TPPS/2 IBM TrackPoint                     id=11   [slave  pointer  (2)]
⎜   ↳ SynPS/2 Synaptics TouchPad                id=10   [slave  pointer  (2)]
⎣ Virtual core keyboard                         id=3    [master keyboard (2)]
    ↳ Virtual core XTEST keyboard               id=5    [slave  keyboard (3)]
    ↳ Power Button                              id=6    [slave  keyboard (3)]
    ↳ Video Bus                                 id=7    [slave  keyboard (3)]
    ↳ Sleep Button                              id=8    [slave  keyboard (3)]
    ↳ AT Translated Set 2 keyboard              id=9    [slave  keyboard (3)]
    ↳ ThinkPad Extra Buttons                    id=12   [slave  keyboard (3)]

```

Disable the device with `xinput --disable _device_id_`, where _device_id_ is the device ID you want to disable. In this example we will disable the Synaptics Touchpad, with the ID 10:

```
$ xinput --disable 10

```

To re-enable the device, just issue the opposite command:

```
$ xinput --enable 10

```

## Troubleshooting

### General

If a problem occurs, view the log stored in either `/var/log/` or, for the rootless X default since v1.16, in `~/.local/share/xorg/`. [GDM](/index.php/GDM "GDM") users should check the [systemd](/index.php/Systemd "Systemd") journal. [[2]](https://bbs.archlinux.org/viewtopic.php?id=184639)

The logfiles are of the form `Xorg.n.log` with `n` being the display number. For a single user machine with default configuration the applicable log is frequently `Xorg.0.log`, but otherwise it may vary. To make sure to pick the right file it may help to look at the timestamp of the X server session start and from which console it was started. For example:

 `$ grep -e Log -e tty Xorg.0.log` 

```
[    40.623] (==) Log file: "/home/archuser/.local/share/xorg/Xorg.0.log", Time: Thu Aug 28 12:36:44 2014
[    40.704] (--) controlling tty is VT number 1, auto-enabling KeepTty
```

*   In the logfile then be on the lookout for any lines beginning with `(EE)`, which represent errors, and also `(WW)`, which are warnings that could indicate other issues.

*   If there is an _empty_ `.xinitrc` file in your `$HOME`, either delete or edit it in order for X to start properly. If you do not do this X will show a blank screen with what appears to be no errors in your `Xorg.0.log`. Simply deleting it will get it running with a default X environment.
*   If the screen goes black, you may still attempt to switch to a different virtual console (e.g. `Ctrl+Alt+F2`), and blindly log in as root. You can do this by typing `root` (press `Enter` after typing it) and entering the root password (again, press `Enter` after typing it).

You may also attempt to kill the X server with:

 `# pkill X` 

If this does not work, reboot blindly with:

 `# reboot` 

*   Check specific pages in [Category:Input devices](/index.php/Category:Input_devices "Category:Input devices") if you have issues with keyboard, mouse, touchpad etc.
*   Search for common problems in [ATI](/index.php/ATI "ATI"), [Intel](/index.php/Intel "Intel") and [NVIDIA](/index.php/NVIDIA "NVIDIA") articles.

### Black screen, No protocol specified.., Resource temporarily unavailable for all or some users

X creates configuration and temporary files in current user's home directory. Make sure there is free disk space available on the partition your home directory resides in. Unfortunately, X server does not provide any more obvious information about lack of disk space in this case.

### CTRL right key does not work with oss keymap

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** The file will be overwritten on [xkeyboard-config](https://www.archlinux.org/packages/?name=xkeyboard-config) update; for such simple task should be used [Xmodmap](/index.php/Xmodmap "Xmodmap"). (Discuss in [Talk:Xorg#](https://wiki.archlinux.org/index.php/Talk:Xorg))

Edit as root `/usr/share/X11/xkb/symbols/fr`, and change the line:

```
include "level5(rctrl_switch)"

```

to

```
// include "level5(rctrl_switch)"

```

Then restart X, reboot or run

```
setxkbmap fr oss

```

### DRI with Matrox cards stops working

If you use a Matrox card and DRI stops working after upgrading to Xorg, try adding the line:

```
Option "OldDmaInit" "On"

```

to the Device section that references the video card in `xorg.conf`.

### Frame-buffer mode problems

If X fails to start with the following log messages,

```
(WW) Falling back to old probe method for fbdev
(II) Loading sub module "fbdevhw"
(II) LoadModule: "fbdevhw"
(II) Loading /usr/lib/xorg/modules/linux//libfbdevhw.so
(II) Module fbdevhw: vendor="X.Org Foundation"
       compiled for 1.6.1, module version=0.0.2
       ABI class: X.Org Video Driver, version 5.0
(II) FBDEV(1): using default device

Fatal server error:
Cannot run in framebuffer mode. Please specify busIDs for all framebuffer devices

```

uninstall fbdev:

```
# pacman -R xf86-video-fbdev

```

### Launching multiple X sessions with proprietary NVIDIA on Xorg 1.16

When attempting to launch X sessions in multiple ttys on Xorg 1.16, you may be rejected with a log indicating that no drivers were found. I found that a workaround for this was to specifically tell X that we'd like to use the 'nvidia' driver.

`/etc/X11/xorg.conf.d/20-nvidia.conf`

```
Section "Device"
    Identifier "Device0"
    Driver     "nvidia"
    VendorName "NVIDIA Corporation"
    Option     "NoLogo" "True"
EndSection

```

### Program requests "font '(null)'"

*   Error message: "_unable to load font `(null)'._"

Some programs only work with bitmap fonts. Two major packages with bitmap fonts are available, [xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi) and [xorg-fonts-100dpi](https://www.archlinux.org/packages/?name=xorg-fonts-100dpi). You do not need both; one should be enough. To find out which one would be better in your case, try this:

```
$ xdpyinfo | grep resolution

```

and use what is closer to the shown value.

### Recovery: disabling Xorg before GUI login

If Xorg is set to boot up automatically and for some reason you need to prevent it from starting up before the login/display manager appears (if the system is wrongly configured and Xorg does not recognize your mouse or keyboard input, for instance), you can accomplish this task with two methods.

*   Change default target to rescue.target. See [systemd#Change default target to boot into](/index.php/Systemd#Change_default_target_to_boot_into "Systemd").
*   If you have not only a faulty system that makes Xorg unusable, but you have also set the GRUB menu wait time to zero, or cannot otherwise use GRUB to prevent Xorg from booting, you can use the Arch Linux live CD. Follow the [installation guide](/index.php/Installation_guide#Mount_the_partitions "Installation guide") about how to mount and chroot into the installed Arch Linux. Alternatively try to switch into another [tty](/index.php/Getty "Getty") with `Ctrl+Alt` + function key (usually from `F1` to `F7` depending on which is not used by X), login as root and follow steps below.

Depending on setup, you will need to do one or more of these steps:

*   [Disable](/index.php/Disable "Disable") the [display manager](/index.php/Display_manager "Display manager").
*   Disable the [automatic start of the X](/index.php/Start_X_at_login "Start X at login").
*   Rename the `~/.xinitrc` or comment out the `exec` line in it.

### X clients started with "su" fail

If you are getting "Client is not authorized to connect to server", try adding the line:

```
session        optional        pam_xauth.so

```

to `/etc/pam.d/su`. `pam_xauth` will then properly set environment variables and handle `xauth` keys.

### X failed to start: Keyboard initialization failed

If your hard disk is full, startx will fail. `/var/log/Xorg.0.log` will end with:

```
(EE) Error compiling keymap (server-0)
(EE) XKB: Could not compile keymap
(EE) XKB: Failed to load keymap. Loading default keymap instead.
(EE) Error compiling keymap (server-0)
(EE) XKB: Could not compile keymap
XKB: Failed to compile keymap
Keyboard initialization failed. This could be a missing or incorrect setup of xkeyboard-config.
Fatal server error:
Failed to activate core devices.
Please consult the The X.Org Foundation support at http://wiki.x.org
for help.
Please also check the log file at "/var/log/Xorg.0.log" for additional information.
(II) AIGLX: Suspending AIGLX clients for VT switch

```

Make some free space on your root partition and X will start.

### Rootless Xorg (v1.16)

As of version 1.16 [[3]](https://www.archlinux.org/news/xorg-server-116-is-now-available/), Xorg may run with standard user privileges with the help of `logind`. The requirements for this are:

*   [systemd](/index.php/Systemd "Systemd"); version >=216 for multiple instances
*   Starting X via [xinit](/index.php/Xinit "Xinit"); display managers are not supported
*   [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting"); implementations in proprietary display drivers fail [auto-detection](http://cgit.freedesktop.org/xorg/xserver/tree/hw/xfree86/xorg-wrapper.c#n222) and require manually setting `needs_root_rights = no` in `/etc/X11/Xwrapper.config`.

If you do not fit these requirements, re-enable root rights in `/etc/X11/Xwrapper.config`:

```
needs_root_rights = _yes_

```

See also [Xorg.wrap(1)](http://manned.org/Xorg.wrap.1) and [Systemd/User#Xorg as a systemd user service](/index.php/Systemd/User#Xorg_as_a_systemd_user_service "Systemd/User").

#### Broken redirection

While user Xorg logs are stored in `~/.local/share/xorg/Xorg.log`, they do not include the output from the X session. To re-enable redirection, start X with the `-keeptty` flag:

```
exec startx -- -keeptty -nolisten tcp > ~/.xorg.log 2>&1

```

Or copy `/etc/X11/xinit/xserverrc` to `~/.xserverrc`, and append `-keeptty`. See [[4]](https://bbs.archlinux.org/viewtopic.php?pid=1446402#p1446402).

### Why do I get a green screen whenever I try to watch a video?

Your color depth is set wrong. It may need to be 24 instead of 16, for example.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Xorg&oldid=412223](https://wiki.archlinux.org/index.php?title=Xorg&oldid=412223)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [X server](/index.php/Category:X_server "Category:X server")
*   [Graphics](/index.php/Category:Graphics "Category:Graphics")