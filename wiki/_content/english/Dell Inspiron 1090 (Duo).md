The Dell Inspiron 1090 (also Dell Inspiron Duo or Dell Duo) is a notebook/tablet convertible with a touchscreen with two-finger multitouch support. The touchscreen (with multitouch), wireless/bluetooth controller, sound system, webcam and CrystalHD chip work without problem. The only component which currently does not work is the [#Accelerometer](#Accelerometer).

## Contents

*   [1 Hardware specifications](#Hardware_specifications)
    *   [1.1 Official specifications](#Official_specifications)
    *   [1.2 Specifications according to uname, lspci and lsusb](#Specifications_according_to_uname.2C_lspci_and_lsusb)
        *   [1.2.1 Microarchitecture, processor and platform](#Microarchitecture.2C_processor_and_platform)
        *   [1.2.2 PCI buses and devices](#PCI_buses_and_devices)
        *   [1.2.3 USB devices](#USB_devices)
*   [2 Hardware configuration](#Hardware_configuration)
    *   [2.1 Accelerometer](#Accelerometer)
    *   [2.2 Wireless](#Wireless)
    *   [2.3 Webcam](#Webcam)
    *   [2.4 Graphics controller](#Graphics_controller)
    *   [2.5 Touchpad](#Touchpad)
    *   [2.6 Bluetooth](#Bluetooth)
    *   [2.7 Speakers](#Speakers)
    *   [2.8 HD video playback](#HD_video_playback)
    *   [2.9 Touchscreen](#Touchscreen)
    *   [2.10 Docking Station](#Docking_Station)
*   [3 Tablet Mode](#Tablet_Mode)
    *   [3.1 (Un)folding detection](#.28Un.29folding_detection)
    *   [3.2 Transparent cursor](#Transparent_cursor)
        *   [3.2.1 Hide mouse pointer in Gnome 3.x](#Hide_mouse_pointer_in_Gnome_3.x)
        *   [3.2.2 Hide mouse pointer in GDM](#Hide_mouse_pointer_in_GDM)
    *   [3.3 On-screen keyboard](#On-screen_keyboard)
        *   [3.3.1 Generic](#Generic)
        *   [3.3.2 Gnome 3.2.x](#Gnome_3.2.x)
    *   [3.4 Gesture recognition](#Gesture_recognition)
    *   [3.5 Screen rotation](#Screen_rotation)
*   [4 Examples of use](#Examples_of_use)
    *   [4.1 Script for rotating the screen](#Script_for_rotating_the_screen)
    *   [4.2 Script for toggling tablet mode ON and OFF (Gnome 3.x)](#Script_for_toggling_tablet_mode_ON_and_OFF_.28Gnome_3.x.29)
*   [5 See also](#See_also)

## Hardware specifications

### Official specifications

*   **Processor:** Intel® Atom® Dual Core Processor N570 (1.6GHz, 512K L2 Cache).
*   **Memory:** 2GB DDR3 SDRAM.
*   **Chipset:** Intel® NM10 Express Chipset.
*   **Video card:** Intel NM10 Express Video.
*   **Display:** 10.1" Widescreen (1366x768) Capacitive Multi Touch.
*   **Audio and speakers:** 2 X 1W speakers for total of 2W standard.
*   **Hard drive:** Up to 320GB5 SATA hard drive (7200RPM).
*   **Battery:** 29Whr 4 cell battery, captive, factory replaceable.
    *   **Battery life:** Up to 3 hours and 57 minutes of battery life.
*   **Camera:** Built-in 1.3 megapixel Webcam.
*   **Wireless:** Wireless 802.11b/g/n.
*   **Bluetooth:** Wireless 802.11b/g/n / Bluetooth 3.0 combo Card (Optional).
*   **Ports:**
    *   (1) Microphone.
    *   (1) Headphone JACK.
    *   (2) USB 2.0.
    *   (1) AC adapter connector.
*   **Dimensions and weight:**
    *   Width: 11.22" (285.0mm).
    *   Height: 1.03" (26.2mm) front – 1.13" (28.7mm) back.
    *   Depth: 7.66" (194.5mm).
    *   Starting weight: 3.39 lbs (1.54Kg).

### Specifications according to `uname`, `lspci` and `lsusb`

#### Microarchitecture, processor and platform

 `uname -mpi`  `i686 Intel(R) Atom(TM) CPU N550 @ 1.50GHz GenuineIntel` 

#### PCI buses and devices

 `lspci` 
```
00:00.0 Host bridge: Intel Corporation N10 Family DMI Bridge (rev 02)
00:02.0 VGA compatible controller: Intel Corporation N10 Family Integrated Graphics Controller (rev 02)
00:02.1 Display controller: Intel Corporation N10 Family Integrated Graphics Controller (rev 02)
00:1b.0 Audio device: Intel Corporation N10/ICH 7 Family High Definition Audio Controller (rev 02)
00:1c.0 PCI bridge: Intel Corporation N10/ICH 7 Family PCI Express Port 1 (rev 02)
00:1c.1 PCI bridge: Intel Corporation N10/ICH 7 Family PCI Express Port 2 (rev 02)
00:1c.2 PCI bridge: Intel Corporation N10/ICH 7 Family PCI Express Port 3 (rev 02)
00:1c.3 PCI bridge: Intel Corporation N10/ICH 7 Family PCI Express Port 4 (rev 02)
00:1d.0 USB controller: Intel Corporation N10/ICH 7 Family USB UHCI Controller #1 (rev 02)
00:1d.1 USB controller: Intel Corporation N10/ICH 7 Family USB UHCI Controller #2 (rev 02)
00:1d.2 USB controller: Intel Corporation N10/ICH 7 Family USB UHCI Controller #3 (rev 02)
00:1d.3 USB controller: Intel Corporation N10/ICH 7 Family USB UHCI Controller #4 (rev 02)
00:1d.7 USB controller: Intel Corporation N10/ICH 7 Family USB2 EHCI Controller (rev 02)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev e2)
00:1f.0 ISA bridge: Intel Corporation NM10 Family LPC Controller (rev 02)
00:1f.2 SATA controller: Intel Corporation N10/ICH7 Family SATA AHCI Controller (rev 02)
00:1f.3 SMBus: Intel Corporation N10/ICH 7 Family SMBus Controller (rev 02)
01:00.0 Multimedia controller: Broadcom Corporation BCM70015 Video Decoder [Crystal HD]
02:00.0 Network controller: Atheros Communications Inc. AR9285 Wireless Network Adapter (PCI-Express) (rev 01)
```

#### USB devices

 `lsusb` 
```
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 005 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 001 Device 002: ID 0bda:58f4 Realtek Semiconductor Corp. 
Bus 004 Device 002: ID 0eef:725e D-WAV Scientific Co., Ltd 
Bus 004 Device 003: ID 0cf3:3005 Atheros Communications, Inc. AR3011 Bluetooth
```

## Hardware configuration

### Accelerometer

According to [this source](http://lukeross.name/dell/), model name is `LSM303DLH`. Only partial configuration has been achieved so far, athough the cited source claims to have full support of the accelerometer. See [STMicroelectronics LSM303DLH Accelerometer/Magenetometer](/index.php/STMicroelectronics_LSM303DLH_Accelerometer/Magenetometer "STMicroelectronics LSM303DLH Accelerometer/Magenetometer").

### Wireless

Works out of the box.

### Webcam

Detected by `udev` as

```
Bus 001 Device 002: ID 0bda:58f4 Realtek Semiconductor Corp. 

```

Works out of the box. Uses the `uvcvideo` module, see [Kernel modules](/index.php/Kernel_modules "Kernel modules") and [Webcam setup](/index.php/Webcam_setup "Webcam setup").

### Graphics controller

[Install](/index.php/Install "Install") the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package. See [Intel](/index.php/Intel "Intel").

### Touchpad

[Install](/index.php/Install "Install") the [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) package.

### Bluetooth

Uses `bluetooth` daemon, see [Daemon](/index.php/Daemon "Daemon").

### Speakers

Uses `snd-hda-intel` module, see [Kernel modules](/index.php/Kernel_modules "Kernel modules").

### HD video playback

Install [crystalhd-git](https://aur.archlinux.org/packages/crystalhd-git/), available in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). The new module is located in

```
/lib/modules/$(uname -r)/kernel/drivers/video/broadcom/crystalhd.ko

```

Unload the staging module `crystalhd` and load the new one, see [Kernel modules](/index.php/Kernel_modules "Kernel modules").

### Touchscreen

Detected by `udev` as:

```
Bus 004 Device 002: ID 0eef:725e D-WAV Scientific Co., Ltd

```

For configuration, see [Multitouch displays](/index.php/Multitouch_displays "Multitouch displays").

### Docking Station

A docking station is sold optionally with this computer.

The docking station is an apparant PCI bus, connected from the bottom of the computer, that adds two USB, one audio, and one 10/100 hardwire 10/100 ethernet port.

## Tablet Mode

The instructions above make the 1090 a fully-working netbook. To take advantage of this hardware, some tablet-related features need to be configured.

### (Un)folding detection

When this computer is folded (or unfolded) into a tablet, it sends a keystroke. You can assign the keys `XF86LAUNCH1` and `XF86LAUNCH2` to these keystrokes with the following commands, respectively:

```
setkeycodes e073 148
setkeycodes e074 149

```

**Tip:** Add those commands to `/etc/rc.local` to execute them when booting.

### Transparent cursor

Install [xcursor-transparent-theme](https://aur.archlinux.org/packages/xcursor-transparent-theme/), available in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

#### Hide mouse pointer in Gnome 3.x

Run the following commands as a normal user:

```
gsettings set org.gnome.desktop.interface cursor-theme "xcursor-transparent" &
gconftool-2 --type string  --set /desktop/gnome/peripherals/mouse/cursor_theme xcursor-transparent &
```

#### Hide mouse pointer in GDM

**Warning:** This will also hide the pointer in *all* Qt applications (you can only see the arrow pointer, secondary pointers as hand, beam or move will be invisible).

Create/edit the file `/usr/share/icons/default/index.theme` with the following contents:

```
[Icon Theme]
Inherits=xcursor-transparent
```

### On-screen keyboard

#### Generic

Install [florence](https://aur.archlinux.org/packages/florence/), available in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

#### Gnome 3.2.x

[Install](/index.php/Install "Install") the [caribou](https://www.archlinux.org/packages/?name=caribou) package.

### Gesture recognition

Install [easystroke-mt](https://aur.archlinux.org/packages/easystroke-mt/), available in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). It has multitouch support.

**Note:** [easystroke](https://www.archlinux.org/packages/?name=easystroke) (also available in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") does not work properly with multitouch. When the screen is touched with two fingers it is interpreted at a gesture given by the line defined between the two points of contact.

### Screen rotation

The screen can be rotated with `xrandr`, but the coordinates of the touchscreen are not rotated accordingly. You can fix this with `xinput` by running the following commands:

**Warning:** This commmands depend on the output of `xinput --list`, which may change on driver updates for the touchscreen.
 `xrandr -o left` 
```
xinput set-prop "eGalax Inc. USB TouchController" 'Coordinate Transformation Matrix' 0 1 0 1 0 0 0 0 1
xinput set-prop "eGalax Inc. USB TouchController" 'Evdev Axis Inversion' 0 1
xinput set-prop "eGalaxTouch Virtual Device for Multi" 'Coordinate Transformation Matrix' 0 1 0 1 0 0 0 0 1
xinput set-prop "eGalaxTouch Virtual Device for Multi" 'Evdev Axis Inversion' 0 1
xinput set-prop "eGalaxTouch Virtual Device for Single" 'Coordinate Transformation Matrix' 0 1 0 1 0 0 0 0 1
xinput set-prop "eGalaxTouch Virtual Device for Single" 'Evdev Axis Inversion' 0 1

```
 `xrandr -o right` 
```
xinput set-prop "eGalax Inc. USB TouchController" 'Coordinate Transformation Matrix' 0 1 0 1 0 0 0 0 1
xinput set-prop "eGalax Inc. USB TouchController" 'Evdev Axis Inversion' 1 0
xinput set-prop "eGalaxTouch Virtual Device for Multi" 'Coordinate Transformation Matrix' 0 1 0 1 0 0 0 0 1
xinput set-prop "eGalaxTouch Virtual Device for Multi" 'Evdev Axis Inversion' 1 0
xinput set-prop "eGalaxTouch Virtual Device for Single" 'Coordinate Transformation Matrix' 0 1 0 1 0 0 0 0 1
xinput set-prop "eGalaxTouch Virtual Device for Single" 'Evdev Axis Inversion' 1 0

```
 `xrandr -o inverted` 
```
xinput set-prop "eGalax Inc. USB TouchController" 'Coordinate Transformation Matrix' 1 0 0 0 1 0 0 0 1
xinput set-prop "eGalax Inc. USB TouchController" 'Evdev Axis Inversion' 1 1
xinput set-prop "eGalaxTouch Virtual Device for Multi" 'Coordinate Transformation Matrix' 1 0 0 0 1 0 0 0 1
xinput set-prop "eGalaxTouch Virtual Device for Multi" 'Evdev Axis Inversion' 0 0
xinput set-prop "eGalaxTouch Virtual Device for Single" 'Coordinate Transformation Matrix' 1 0 0 0 1 0 0 0 1
xinput set-prop "eGalaxTouch Virtual Device for Single" 'Evdev Axis Inversion' 0 0

```
 `xrandr -o normal` 
```
xinput set-prop "eGalax Inc. USB TouchController" 'Coordinate Transformation Matrix' 1 0 0 0 1 0 0 0 1
xinput set-prop "eGalax Inc. USB TouchController" 'Evdev Axis Inversion' 0 0
xinput set-prop "eGalaxTouch Virtual Device for Multi" 'Coordinate Transformation Matrix' 1 0 0 0 1 0 0 0 1
xinput set-prop "eGalaxTouch Virtual Device for Multi" 'Evdev Axis Inversion' 0 0
xinput set-prop "eGalaxTouch Virtual Device for Single" 'Coordinate Transformation Matrix' 1 0 0 0 1 0 0 0 1
xinput set-prop "eGalaxTouch Virtual Device for Single" 'Evdev Axis Inversion' 0 0

```

Observe that the transformation matrix is the same for normal and inverted orientations, and for left and right orientations. Therefor the corresponding commands need to be applied only when changing between orientations with *different* transformation matrix.

## Examples of use

### Script for rotating the screen

The commands above can be used to make a simple shell script for toggling the screen orientation between landscape and portrait as follows, see also [#Screen rotation](#Screen_rotation):

 `~/toggle_orientation.sh` 
```
#!/bin/bash

rotation="$(xrandr -q --verbose | grep 'connected' | egrep -o  '\) (normal|left|inverted|right) \(' | egrep -o '(normal|left|inverted|right)')"

if [ $rotation = "normal" ] ;
then
    xrandr -o left
    xinput set-prop "eGalax Inc. USB TouchController" 'Coordinate Transformation Matrix' 0 1 0 1 0 0 0 0 1
    xinput set-prop "eGalax Inc. USB TouchController" 'Evdev Axis Inversion' 0 1
    xinput set-prop "eGalaxTouch Virtual Device for Multi" 'Coordinate Transformation Matrix' 0 1 0 1 0 0 0 0 1
    xinput set-prop "eGalaxTouch Virtual Device for Multi" 'Evdev Axis Inversion' 0 1
    xinput set-prop "eGalaxTouch Virtual Device for Single" 'Coordinate Transformation Matrix' 0 1 0 1 0 0 0 0 1
    xinput set-prop "eGalaxTouch Virtual Device for Single" 'Evdev Axis Inversion' 0 1
else
    xrandr -o normal
    xinput set-prop "eGalax Inc. USB TouchController" 'Coordinate Transformation Matrix' 1 0 0 0 1 0 0 0 1
    xinput set-prop "eGalax Inc. USB TouchController" 'Evdev Axis Inversion' 0 0
    xinput set-prop "eGalaxTouch Virtual Device for Multi" 'Coordinate Transformation Matrix' 1 0 0 0 1 0 0 0 1
    xinput set-prop "eGalaxTouch Virtual Device for Multi" 'Evdev Axis Inversion' 0 0
    xinput set-prop "eGalaxTouch Virtual Device for Single" 'Coordinate Transformation Matrix' 1 0 0 0 1 0 0 0 1
    xinput set-prop "eGalaxTouch Virtual Device for Single" 'Evdev Axis Inversion' 0 0
fi
exit 0
```

**Tip:** For an improved user experience you can:

*   Associate this script to a gesture using [easystroke-mt](https://aur.archlinux.org/packages/easystroke-mt/), see [#Gesture recognition](#Gesture_recognition).
*   Create a desktop launcher/system tray icon to run this script.

### Script for toggling tablet mode ON and OFF (Gnome 3.x)

The following shell script hides the mouse pointer and activates Gnome 3.x's on-screen keyboard, [caribou](https://www.archlinux.org/packages/?name=caribou), when the netbook is fold into a tablet. It detects the current mode based on the current cursor theme (if the cursor is hidden, then the computer is in tablet mode). When you unfold the computer, it returns the screen to the default orientation.

**Note:** It assumes [xcursor-transparent-theme](https://aur.archlinux.org/packages/xcursor-transparent-theme/) and [caribou](https://www.archlinux.org/packages/?name=caribou) are installed, see [#Transparent cursor](#Transparent_cursor) and [#On-screen keyboard](#On-screen_keyboard); and that `Adwaita`, Gnome 3.x's default cursor theme is in use. See also [#Screen rotation](#Screen_rotation).
 `~/toggle_tabletmode.sh` 
```
#!/bin/bash

if [ $(echo $(gsettings get org.gnome.desktop.interface cursor-theme) | cut -c2- | sed 's/\(.*\)./\1/') = "xcursor-transparent" ] ;
then
    gsettings set org.gnome.desktop.interface cursor-theme "Adwaita" &
    gconftool-2 --type string  --set /desktop/gnome/peripherals/mouse/cursor_theme Adwaita &
    dconf write /org/gnome/desktop/a11y/applications/screen-keyboard-enabled false &
    xrandr -o normal
    xinput set-prop "eGalax Inc. USB TouchController" 'Coordinate Transformation Matrix' 1 0 0 0 1 0 0 0 1
    xinput set-prop "eGalax Inc. USB TouchController" 'Evdev Axis Inversion' 0 0
    xinput set-prop "eGalaxTouch Virtual Device for Multi" 'Coordinate Transformation Matrix' 1 0 0 0 1 0 0 0 1
    xinput set-prop "eGalaxTouch Virtual Device for Multi" 'Evdev Axis Inversion' 0 0
    xinput set-prop "eGalaxTouch Virtual Device for Single" 'Coordinate Transformation Matrix' 1 0 0 0 1 0 0 0 1
    xinput set-prop "eGalaxTouch Virtual Device for Single" 'Evdev Axis Inversion' 0 0
else
    gsettings set org.gnome.desktop.interface cursor-theme "xcursor-transparent" &
    gconftool-2 --type string  --set /desktop/gnome/peripherals/mouse/cursor_theme xcursor-transparent &
    dconf write /org/gnome/desktop/a11y/applications/screen-keyboard-enabled true &
fi
exit 0
```

**Tip:** You can run this script when (un)folding the netbook associating it to the keys `XF86LAUNCH1` and `XF86LAUNCH2`, see [#(Un)folding detection](#.28Un.29folding_detection).

## See also

*   Thread in the [Ubuntu Forums](http://ubuntuforums.org/showthread.php?t=1658635).
*   [Luke Ross' website](http://lukeross.name/dell/).