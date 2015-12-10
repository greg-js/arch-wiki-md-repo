# Toshiba P205D-S8804

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

I'm currently working on getting Arch set up on my new Toshiba Satellite P205D-S8804\. This page isn't complete yet, but I'll work on it as I get things up!

## Contents

*   [1 Networking](#Networking)
    *   [1.1 Wifi](#Wifi)
    *   [1.2 Modem](#Modem)
*   [2 Audio](#Audio)
*   [3 Video](#Video)
    *   [3.1 Free Drivers](#Free_Drivers)
    *   [3.2 ATI Catalyst Driver](#ATI_Catalyst_Driver)
*   [4 Touchpad](#Touchpad)
*   [5 Hotkeys](#Hotkeys)
*   [6 CD/DVD/Labelflash](#CD.2FDVD.2FLabelflash)
*   [7 USB](#USB)
*   [8 Firewire](#Firewire)
*   [9 PCMCIA](#PCMCIA)
*   [10 5-in-1 card reader](#5-in-1_card_reader)
*   [11 Power Management](#Power_Management)
    *   [11.1 Cpufreq](#Cpufreq)
    *   [11.2 Suspend and hibernate](#Suspend_and_hibernate)
*   [12 Webcam](#Webcam)

## Networking

The on-board ethernet adaptor worked out of the box for me.

### Wifi

This laptop has an Atheros chipset, which is now supported by the latest madwifi release. With that installed, no additional configuration should be necessary.

### Modem

Looks like this is a winmodem, but I haven't tried it yet, and do not ever plan to.

## Audio

Audio worked out of the box for me as well. See [ALSA](/index.php/ALSA "ALSA") for details.

## Video

This laptop ships with ATI Radeon X1200 integrated video. This card combined with the 17" screen should yield a max resolution of up to 1440x900.

### Free Drivers

Initially, I used the free drivers because the prior version of ATI's official driver had serious issues with resolution. I've used xf86-video-vesa, xf86-video-ati, and xf86-radeonhd without problems. All are available in pacman. Note that the vesa driver will not yield high resolutions, and that none of the three provide decent 3D acceleration, although the RadeonHD driver provides some limited accelerated functionality.

### ATI Catalyst Driver

Visit the [ATI wiki page](/index.php/ATI "ATI") for instructions on how to get the intial set up completed.

You'll want to edit your _/etc/X11/xorg.conf_, because otherwise using accelerated 3D causes rather annoying hard (un-recoverable) kernel locks.

```
cp /etc/X11/xorg.conf /etc/X11/xorg.conf.sav

```

to backup the original file, then

```
nano /etc/X11/xorg.conf

```

and make changes to the sections below **Note: I intentionally left out some sections, like "Fonts" because that may vary from system to system.**

```
Section "ServerLayout"
Identifier     "X.org Configured"
Screen      0  "Screen0" 0 0
InputDevice    "Touchpad[1]" "CorePointer"
InputDevice    "Keyboard0" "CoreKeyboard"
Option	"aiglx"	"true"
EndSection

```

```
Section "Module"
#Load  "GLcore"
Load  "dri"
Load  "dbe"
Load  "record"
Load  "glx"
Load  "xtrap"
Load  "extmod"
Load  "freetype"
Load  "synaptics"
#Load  "vbe"
EndSection

```

```
Section "ServerFlags"
Option	"IgnoreABI"	"on"
EndSection

```

```
Section "Device"
Option      "XAANoOffscreenPixmaps"
Option	    "RenderAccel"	"true"
Option 	    "VideoOverlay"	"on"
Option	    "OpenGLOverlay" 	"off"
Option      "AllowGLXWithComposite" "true"
Identifier  "Card0"
Driver      "fglrx"
VendorName  "ATI Technologies Inc"
BoardName   "Radeon X1200 Series"
BusID       "PCI:1:5:0"
EndSection

```

```
Section "Extensions"
Option "DAMAGE"	   "true"
Option "RENDER"    "true"
Option "Composite" "true"
EndSection

```

```
Section "DRI"
Mode	0666
EndSection

```

I added AIGLX to this configuration file, but I do not know that it is necessary -- I added it personally for Compiz.

I haven't tested dual displays or the S-Video out yet.

## Touchpad

Works fine with the [synaptics](/index.php/Synaptics "Synaptics") driver.

## Hotkeys

Not all "hotkeys" are funtional on this machine -- Some of them are not even generating events in the kernel, although I think we can eventually work around that. Here are the keys that I have gotten to work so far:

```
Mute
Suspend to Ram
Brightness up
Brightness down
Volume Wheel
"Web" key
Play/Pause
Stop
Previous Track
Next Track

```

What I still have left to fix:

```
Lock
Search
Suspend to disk
Display toggle
Wifi switch (Not sure what this key does -- it is on F8, though)
Touchpad switch

```

In order to get any kind of functionality out of these keys, we need to map them to keysyms under X11\. Some window managers (eg GNOME) may do this automatically, but if it doesn't, then here's what we need to do:

1.  Find out the scan code of the keys we want to map to a specific function. Here's the list that I compiled:

```
Mute = 160
Suspend to Ram = 223
Brightness Down = 101
Brightness Up = 212
Internet = 178
Play = 162
Stop = 164
Previous Track 144
Next Track = 153
Volume Wheel Down = 174
Volume Wheel Up = 176

```

1.  Create an Xmodmap file in your home directory with the functions you want to give those keys.

```
nano /home/**username**/.Xmodmap

```

and create a file with the following format:

```
keycode ### = _function name_

```

where ### = the numerical keycode from the list above, and _function name_ is one of the functions listed in /usr/share/X11/XKeysymDB

For reference, here's what I used for my .Xmodmap:

```
keycode 160 = XF86AudioMute
keycode 223 = XF86Sleep
keycode 101 = F28
keycode 212 = F29
keycode 178 = XF86WWW
keycode 162 = XF86AudioPlay
keycode 164 = XF86AudioStop
keycode 144 = XF86AudioPrev
keycode 153 = XF86AudioNext
keycode 174 = XF86AudioLowerVolume
keycode 176 = XF86AudioRaiseVolume

```

I mapped Brightness up/down to F28 and F29 since I needed two seperate keys for the scripts that I am trying to write to control the LCD brightness -- this laptop is not really playing nicely with ACPI.

From here you'll have to configure your individual system to react to these X11 events -- this will vary depending on what window manager you use, or Desktop Environment.

## CD/DVD/Labelflash

The drive reads and writes both CD's and DVD's out of the box. This drive also has labelflash capabilities, but I 'm not sure if that is supported under linux or not.

## USB

Functional out of the box

## Firewire

Have not tested.

## PCMCIA

Have not tested.

## 5-in-1 card reader

Funtional out of the box, although we need to manually add a module to enable SD card support

```
modprobe tifm_sd
modprobe tifm_7xx1
modprobe tifm_ms
modprobe tifm_core

```

and add tifm_sd, tifm_7xx1, tifm_ms and tifm_core to the modules section of your _/etc/rc.conf_

I'm not actually sure if things like CompactFlash or MemoryStick are working, SD card is the only thing I have at the moment.

## Power Management

### Cpufreq

Cpu frequency scaling is supported and works well. Visit the [Cpufrequtils](/index.php/Cpufrequtils "Cpufrequtils") wiki page for instructions. The frequency range in question is 800MHz to a max of 2GHz.

### Suspend and hibernate

Appears to work flawlessly, although not really speedily. See [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate") for configuration details.

## Webcam

_lsusb_ returns this webcam as a "Chicony USB 2.0" webcam, which is supported via the _uvcvideo_ and snd_usb_audio modules. See [Webcam setup](/index.php/Webcam_setup "Webcam setup") for details.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Toshiba_P205D-S8804&oldid=400466](https://wiki.archlinux.org/index.php?title=Toshiba_P205D-S8804&oldid=400466)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Toshiba](/index.php/Category:Toshiba "Category:Toshiba")