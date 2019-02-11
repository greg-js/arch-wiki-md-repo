DisplayLink devices on Linux still only have experimental support. While some people have had success in using them, it is generally not an easy process and not guaranteed to work. The steps on this page describe the generally most successful methods of using external monitors with DisplayLink.

Also be warned that even over USB 3.0, a DisplayLink monitor may exhibit noticeably more lag than e.g. a DisplayPort monitor, especially when large portions of the screen are being redrawn.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 USB 2.0 DL-1x5, DL-1x0 Devices](#USB_2.0_DL-1x5,_DL-1x0_Devices)
    *   [1.2 USB 3.0 DL-6xxx, DL-5xxx, DL-41xx, DL-3xxx Devices](#USB_3.0_DL-6xxx,_DL-5xxx,_DL-41xx,_DL-3xxx_Devices)
    *   [1.3 Setting up X Displays](#Setting_up_X_Displays)
*   [2 Configuration](#Configuration)
    *   [2.1 Load the framebuffer device](#Load_the_framebuffer_device)
    *   [2.2 Configuring X Server](#Configuring_X_Server)
        *   [2.2.1 xrandr](#xrandr)
        *   [2.2.2 Enabling DVI output on startup](#Enabling_DVI_output_on_startup)
        *   [2.2.3 Switching between displaylink and nvidia/nouveau driver](#Switching_between_displaylink_and_nvidia/nouveau_driver)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Not working configuration](#Not_working_configuration)
    *   [3.2 Screen redraw is broken](#Screen_redraw_is_broken)
    *   [3.3 DisplayLink refresh rate is extremely slow with gnome 3](#DisplayLink_refresh_rate_is_extremely_slow_with_gnome_3)
    *   [3.4 Slow redraw/Unresponsiveness in Google Chrome and Webkit2-based Applications](#Slow_redraw/Unresponsiveness_in_Google_Chrome_and_Webkit2-based_Applications)
    *   [3.5 Impossible to activate displaylink's screen](#Impossible_to_activate_displaylink's_screen)
    *   [3.6 Suspend problem](#Suspend_problem)
    *   [3.7 DisplayLink is not working when usb hot plugged](#DisplayLink_is_not_working_when_usb_hot_plugged)
    *   [3.8 DisplayLink driver does not work with Intel GPUs after recent X upgrades](#DisplayLink_driver_does_not_work_with_Intel_GPUs_after_recent_X_upgrades)
        *   [3.8.1 Workaround 1: Use older intel driver as a fallback](#Workaround_1:_Use_older_intel_driver_as_a_fallback)
        *   [3.8.2 Workaround 2: Temporarily disable PageFlip for modesetting](#Workaround_2:_Temporarily_disable_PageFlip_for_modesetting)
    *   [3.9 Displays disconnect at random intervals when using the Dell D6000 docking station](#Displays_disconnect_at_random_intervals_when_using_the_Dell_D6000_docking_station)
*   [4 See Also](#See_Also)

## Installation

### USB 2.0 DL-1x5, DL-1x0 Devices

The kernel [DRM](https://en.wikipedia.org/wiki/Direct_Rendering_Manager "wikipedia:Direct Rendering Manager") driver for DisplayLink is `udl`, a rewrite of the original [udlfb](https://www.kernel.org/doc/Documentation/fb/udlfb.txt) driver. It allows configuring DisplayLink monitors using [Xrandr](/index.php/Xrandr "Xrandr").

This should work without any configuration changes on [linux](https://www.archlinux.org/packages/?name=linux) 4.14.9-1 and later. If you're using an earlier version of that package or have `CONFIG_FB_UDL=m` set in your kernel config, you need to [blacklist](/index.php/Blacklist "Blacklist") the old kernel module, `udlfb`, which may attempt to load itself first.

### USB 3.0 DL-6xxx, DL-5xxx, DL-41xx, DL-3xxx Devices

1.  Install the [displaylink](https://aur.archlinux.org/packages/displaylink/) driver. It allows configuring DisplayLink monitors using [Xrandr](/index.php/Xrandr "Xrandr") in the same manner as the `udl` driver.
2.  Enable `displaylink.service`.
3.  Use the "modesetting" driver with AccelMethod "none" and MatchDriver "evdi".

Create a file with the following content:

 `/usr/share/X11/xorg.conf.d/20-evdidevice.conf` 
```
Section "OutputClass"
	Identifier "DisplayLink"
	MatchDriver "evdi"
	Driver "modesetting"
	Option  "AccelMethod" "none"
EndSection

```

A reboot is required for the setting to be effective. You may need the [evdi-git](https://aur.archlinux.org/packages/evdi-git/) package.

### Setting up X Displays

After that, run:

 `$ xrandr --listproviders` 
```
Providers: number : 2
Provider 0: id: 0x49 cap: 0xb, Source Output, Sink Output, Sink Offload crtcs: 2 outputs: 8 associated providers: 0 name:Intel
Provider 1: id: 0x13c cap: 0x2, Sink Output crtcs: 1 outputs: 1 associated providers: 0 name:modesetting

```

In the above output, we can see that provider 0 is the system's regular graphics provider (Intel), and provider 1 (modesetting) is the DisplayLink provider. To use the DisplayLink device, connect provider 1 to provider 0:

```
$ xrandr --setprovideroutputsource 1 0

```

and xrandr will add a DVI output you can [use as normal with xrandr](/index.php/Xrandr#Configuration "Xrandr"). This is still experimental but supports hotplugging and when works, it is by far the simplest setup. If it works then everything below is unnecessary.

## Configuration

These instructions assume that you already have an up and running X server and are simply adding a monitor to your existing setup.

### Load the framebuffer device

Before your system will recognize your DisplayLink device, the `udl` kernel module must be loaded. To do this, run

```
# modprobe udl

```

If your DisplayLink device is connected, it should show some visual indication of this. Although a green screen is the standard indicator of this, other variations have been spotted and are perfectly normal. Most importantly, the output of `dmesg` should show something like the following, indicating a new DisplayLink device was found:

```
usb 2-1.1: new high-speed USB device number 7 using ehci-pci
usb 2-1.1: New USB device found, idVendor=17e9, idProduct=03e0
usb 2-1.1: New USB device strings: Mfr=1, Product=2, SerialNumber=3
usb 2-1.1: Product: Lenovo LT1421 wide
usb 2-1.1: Manufacturer: DisplayLink
usb 2-1.1: SerialNumber: 6V9BBRM1
[drm] vendor descriptor length:17 data:17 5f 01 00 15 05 00 01 03 00 04
udl 2-1.1:1.0: fb1: udldrmfb frame buffer device
[drm] Initialized udl 0.0.1 20120220 on minor 1

```

Furthermore, `/dev` should contain a new `fb` device, likely `/dev/fb1` if you already had a framebuffer for your primary display.

To automatically load `udl` at boot, create the file `udl.conf` in `/etc/modules-load.d/` with the following contents:

 `/etc/modules-load.d/udl.conf`  `udl` 

For more information on loading kernel modules, see [Kernel modules#Automatic module loading with systemd](/index.php/Kernel_modules#Automatic_module_loading_with_systemd "Kernel modules").

### Configuring X Server

Use `xrandr` or your Desktop Environment's display setup UI to configure your USB monitors running either the `udl` or `displaylink` driver.

#### xrandr

Once the driver is loaded, the DisplayLink monitor is listed as an output provider:

 `$ xrandr --listproviders` 
```
Providers: number : 2
Provider 0: id: 0x43 cap: 0xb, Source Output, Sink Output, Sink Offload crtcs: 2 outputs: 2 associated providers: 1 name:Intel
Provider 1: id: 0xcb cap: 0x2, Sink Output crtcs: 1 outputs: 1 associated providers: 1 name:modesetting

```

In the above example, provider 1 is the DisplayLink device, and provider 0 is the default display. Running `xrandr --current` gives a list of available screens:

 `$ xrandr --current` 
```
Screen 0: minimum 320 x 200, current 1600 x 900, maximum 8192 x 8192
LVDS1 connected 1600x900+0+0 (normal left inverted right x axis y axis) 309mm x 174mm
   1600x900       60.0*+   40.0  
   1440x900       59.9  
   1360x768       59.8     60.0  
   1152x864       60.0  
   1024x768       60.0  
   800x600        60.3     56.2  
   640x480        59.9  
VGA1 disconnected (normal left inverted right x axis y axis)
DVI-1-0 connected (normal left inverted right x axis y axis)
   1366x768       60.0 +
   1368x768_59.90   59.9  
  1368x768_59.90 (0xd0)   85.7MHz
        h: width  1368 start 1440 end 1584 total 1800 skew    0 clock   47.6KHz
        v: height  768 start  769 end  772 total  795           clock   59.9Hz

```

If the above does not list the DisplayLink screen, then you will need to offload DisplayLink to the main GPU:

 `xrandr --setprovideroutputsource 1 0` 

Once the screen is available, refer to [Xrandr](/index.php/Xrandr "Xrandr") for info on setting it up. For automating the configuration process, see [displaylink.sh](https://github.com/nathantypanski/displaylink.sh).

#### Enabling DVI output on startup

The DisplayLink provider will not be automatically connected to the main provider in most cases, therefore the DVI output device will not be available. It can be helpful to automatically do this when X starts to facilitate automatic display configuration by the window manager.

Edit your desktop manager's startup configuration and add commands similar to:

```
$(xrandr --listproviders | grep -q "modesetting") && xrandr --setprovideroutputsource 1 0

```

For example, the appropriate startup configuration file for [SDDM](/index.php/SDDM "SDDM") is `/usr/share/sddm/scripts/Xsetup`.

Avoid placing these commands in `~/.xprofile` as this breaks the display configuration of some window managers. Instead these commands should be run prior to any display output or setup.

**Note:** If you have additional providers, specify the name of the provider instead of using indexes. The name of the DisplayLink device will be `modesetting`

#### Switching between displaylink and nvidia/nouveau driver

Currently (displaylink version 1.3.54-1) it is not possible to use displaylink device and nvidia/nouveau driver simultaniously on optimus based laptops. Currently to be able to use displaylink device on intel GPU, you should create config file (see troubleshooting section below). However, with that config file it is not possible to use primusrun. Bumblebee service is running, but it cannot work. Also, laptop's fans are becoming very noisy and laptop's temperature becomes very high. When you want to switch back to activate nvidia driver, comment everything in that file and reboot.

To simplify process of switching, you can [install](/index.php/Install "Install") [dl-switch](https://aur.archlinux.org/packages/dl-switch/) and add an additional menu entry to your bootloader using the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `systemd.unit=displaylink.target`, thus activating displaylink workaround.

To check which driver is used for your discrete video card, run `lspci -nnk -s xx:xx.x` (replace xx:xx.x with your nvidia gpu pci id).

## Troubleshooting

### Not working configuration

These are tested on [Xfce](/index.php/Xfce "Xfce") using Display settings (included in XFCE4 package) and external tool - [arandr](https://www.archlinux.org/packages/?name=arandr). XFCE4 Display settings are likely to crash, so ARandR might help.

When you connect display link device via USB to your computer, the computer should show monitors in Display settings. There are few troubleshooting steps that you should try:

*   Check [#Setting up X Displays](#Setting_up_X_Displays). If you can find any external monitors recognized, you should try to make them visible by the following commands:

```
xrandr --setprovideroutputsource 1 0
xrandr --setprovideroutputsource 2 0
xrandr --setprovideroutputsource 3 0
...

```

This will make them visible and recognized in Display settings.

*   Restart `displaylink.service`.
*   Re-connecte USB cable.
*   Check if `udl` driver is loaded and monitors are connected.

### Screen redraw is broken

If you are using `udl` as your kernel driver and the monitor appears to work, but is only updating where you move the mouse or when windows change in certain places, then you probably have the wrong modeline for your screen. Getting a proper modeline for your screen with a command like

```
gtf 1366 768 59.9

```

where `1366` and `768` are the horizontal and vertical resolutions for your monitor, and `59.9` is the refresh rate from its specs. To use this, create a new mode with `xrandr` like follows:

```
xrandr --newmode "1368x768_59.90"  85.72  1368 1440 1584 1800  768 769 772 795  -HSync +Vsync

```

and add it to [Xrandr](/index.php/Xrandr "Xrandr"):

```
xrandr --addmode DVI-0 1368x768_59.90

```

Then tell the monitor to use that mode for the DisplayLink monitor, and this should fix the redraw issues. Check the [Xrandr](/index.php/Xrandr "Xrandr") page for information on using a different mode.

If this does not solve the problem (or if the correct modeline was already in place because of correct DDC data), it can help to run a compositor. E.g. when using plain i3, running [xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr) or [compton](https://www.archlinux.org/packages/?name=compton) can mitigate the problem.

### DisplayLink refresh rate is extremely slow with gnome 3

If once you set up your DisplayLink your entire desktop becomes slow, try setting a "simpler" background image, such as complete black.

### Slow redraw/Unresponsiveness in Google Chrome and Webkit2-based Applications

This is to be associated with bugs in hardware acceleration, which can be tested by running glxgears in the displaylink screen resulting in 1fps. There is currently no complete fix available, but turning off Hardware-Acceleration in affected applications can work as a temporary fix.

This can be done in applications without a hardware-acceleration option by prepending the `LIBGL_ALWAYS_SOFTWARE=1` environment variable.

### Impossible to activate displaylink's screen

In case you are able to see attached monitor via DisplayLink device in your screen settings, but after you turn it on and apply settings, it becomes deactivated, then try blacklist nouveau module and reboot:

 `/etc/modprobe.d/nouveau.conf` 
```
blacklist nouveau
options nouveau modeset=0

```

### Suspend problem

Displaylink is not working after suspend. Unplug and then plug again displaylink's usb cable to your computer. Monitor that is connected via DisplayLink will remain black. If you have lock screen, login to the system and then picture will appear at that monitor and you will be able to use displaylink as normal.

### DisplayLink is not working when usb hot plugged

To be able to use DisplayLink monitors, its usb cable should be attached to laptop during boot time. Otherwise it can behave like they are available and mouse can be moved there, but its picture is frozen, even with correct configuration (see workaround 1). If it was not attached at boot time, attach it and reboot.

### DisplayLink driver does not work with Intel GPUs after recent X upgrades

As [this support](http://support.displaylink.com/knowledgebase/articles/1181623) page says, upgrading the X Window Server to a version newer than 1.18.3 will make the system not compatible with DisplayLink by default. This applies to systems using an integrated Intel GPU, or a combination of integrated Intel GPU and a discrete GPU. Until fixes in X Windows System will be released, there are two workarounds:

#### Workaround 1: Use older intel driver as a fallback

Use the "intel" driver for the integrated GPU instead of "modesetting", which is now the default.

Create a file with the following content:

 `/usr/share/X11/xorg.conf.d/20-displaylink.conf` 
```
Section "Device" 
  Identifier "Intel Graphics"
  Driver "intel"
EndSection

```

A reboot is required for the setting to be effective.

You may need the [evdi-git](https://aur.archlinux.org/packages/evdi-git/) package.

#### Workaround 2: Temporarily disable PageFlip for modesetting

For users that prefer to keep using "modesetting" driver, disabling page flipping should also help. Create a file with the following content:

 `/usr/share/X11/xorg.conf.d/20-displaylink.conf` 
```
Section "Device"
  Identifier "DisplayLink"
  Driver "modesetting"
  Option "PageFlip" "false"
EndSection 

```

### Displays disconnect at random intervals when using the Dell D6000 docking station

User's have [reported](https://www.displaylink.org/forum/showthread.php?t=65476) that when using the Dell D6000 docking station, their display(s) may disconnect at random intervals during usage. This will require physically reconnecting the dock in order to reinitialise the displays.

This issue appears to be caused by [PulseAudio](/index.php/PulseAudio "PulseAudio")'s `module-suspend-on-idle` module, which automatically suspends sinks/sources on idle.

To disable loading of the `module-suspend-on-idle` module, comment out the following line in the configuration file in use (`~/.config/pulse/default.pa` or `/etc/pulse/default.pa`):

 `/etc/pulse/default.pa` 
```
### Automatically suspend sinks/sources that become idle for too long
# load-module module-suspend-on-idle

```

## See Also

*   [DisplayLink Open Source](http://displaylink.org/forum/forumdisplay.php?f=29): Official DisplayLink open source support forum
*   [Plugable](http://plugable.com/platforms/linux): Vendor blog chronicling Linux support for DisplayLink.
*   [Ubuntu Driver Download](http://www.displaylink.com/downloads/ubuntu.php): DisplayLink Ubuntu Driver Download and Information
*   [Release Notes](http://downloads.displaylink.com/releasenotes/DisplayLink_Ubuntu_1.0.68_release-note.txt): Latest release notes for DisplayLink Ubuntu Software