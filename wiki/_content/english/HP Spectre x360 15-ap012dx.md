| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Working | iwlwifi |
| Bluetooth | Working | bluetooth |
| Audio | Working | snd_hda_intel |
| Touchpad | Working |  ? |
| Touchscreen | Working | hid_multitouch |
| Webcam | working | uvcvideo |
| Card Reader | Working | rtsx_pci |
| Wireless switch | Working |  ? |
| Function/Multimedia Keys | Working |  ? |
| Suspend/Resume | Working |  ? |

This article is based on my personal experience with this laptop using Arch x86_64 (kernel 4.8.6-1-ARCH). While I found no noticeable issues remained after the initial installation, some issues have been found in a similar model (see [HP Spectre x360 4231](/index.php/HP_Spectre_x360_4231 "HP Spectre x360 4231")).

## Contents

*   [1 Hardware info](#Hardware_info)
    *   [1.1 Specifications](#Specifications)
    *   [1.2 lspci](#lspci)
    *   [1.3 lsusb](#lsusb)
*   [2 Installation](#Installation)
*   [3 Tweaks](#Tweaks)
    *   [3.1 KDE scaling](#KDE_scaling)
    *   [3.2 Screen Rotation](#Screen_Rotation)
    *   [3.3 TTY font](#TTY_font)

## Hardware info

### Specifications

This model was released in February 2016.

*   [Intel Core i7-6500U with Intel HD Graphics 520 (2.5 GHz, up to 3.1 GHz, 4 MB cache, 2 cores)](http://ark.intel.com/products/88194/Intel-Core-i7-6500U-Processor-4M-Cache-up-to-3_10-GHz)
*   15.6" 4K (3840x2160) Ultra HD IPS WLED multitouch display
*   16 GB LPDDR3-1866 SDRAM
*   256 GB M.2 SDD
*   1 USB Type C port, 3 USB 3.0 ports, 1 HDMI port, 1 Mini DisplayPort, 1 headphone/microphone jack
*   1 SD media card reader
*   802.11ac (2x2) and Bluetooth 4.0
*   Bang & Olufsen quad speakers
*   3-cell, 64.5 Wh Li-ion battery
*   Webcam
*   Backlit keyboard

### lspci

```
00:00.0 Host bridge: Intel Corporation Skylake Host Bridge/DRAM Registers (rev 08)
00:02.0 VGA compatible controller: Intel Corporation HD Graphics 520 (rev 07)
00:13.0 Non-VGA unclassified device: Intel Corporation Device 9d35 (rev 21)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:17.0 SATA controller: Intel Corporation Sunrise Point-LP SATA Controller [AHCI mode] (rev 21)
00:1c.0 PCI bridge: Intel Corporation Device 9d10 (rev f1)
00:1c.2 PCI bridge: Intel Corporation Device 9d12 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-LP LPC Controller (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
01:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS525A PCI Express Card Reader (rev 01)
02:00.0 Network controller: Intel Corporation Wireless 7265 (rev 61)

```

### lsusb

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 04f3:2274 Elan Microelectronics Corp.
Bus 001 Device 003: ID 8087:0a2a Intel Corp.
Bus 001 Device 002: ID 064e:c355 Suyin Corp.
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Installation

Installing Arch was mostly without hiccup; you do need to disable secure boot (F10 for BIOS options; F9 for boot options). Dual boot was not tested. The laptop does not have a CD drive, so you have to use a USB stick.

The following packages got all the hardware working for me:

```
xorg-server
xf86-video-intel
xf86-input-synaptics
libsynaptics
mesa
bluez
bluez-utils
bluez-hid2hci
pulseaudio-bluetooth

```

## Tweaks

### KDE scaling

The screen natively runs at 3840x2160\. KDE by default does not assume a scaling factor. You can go to System Settings > Display and Monitor > Displays > Scale Display to select a scaling factor. Often a factor of 2 is recommended (e.g. a factor of 2 is the default in Gnome). I use a factor of 1.5.

### Screen Rotation

The laptop can be flipped completely (hence the 360 in the name) and it is sometimes useful to rotate the display. It is unclear whether this can be done automatically by detecting the physical laptop orientation, but it should be easy enough to map a shortcut to the following script to toggle the screen display (Source: [Touchscreen Input Doesn't Rotate: Lenovo Yoga 13 / Yoga 2 Pro](http://askubuntu.com/questions/405628/))

```
#!/bin/bash
# This script rotates the screen and touchscreen input 180 degrees,
# disables the touchpad, and enables the virtual keyboard And rotates
# screen back if the touchpad was disabled

isEnabled=$(xinput --list-props 'SynPS/2 Synaptics TouchPad' | awk '/Device Enabled/{print $NF}')

if [ $isEnabled == 1 ]
then
    echo "Screen is turned upside down"
    xrandr -o inverted
    xinput set-prop 'ELAN Touchscreen' 'Coordinate Transformation Matrix' -1 0 1 0 -1 1 0 0 1
    xinput disable 'SynPS/2 Synaptics TouchPad'
    # Remove hashtag below if you want pop-up the virtual keyboard
    # onboard &
else
    echo "Screen is turned back to normal"
    xrandr -o normal
    xinput set-prop 'ELAN Touchscreen' 'Coordinate Transformation Matrix' 1 0 0 0 1 0 0 0 1
    xinput enable 'SynPS/2 Synaptics TouchPad'
    # killall onboard
fi

```

### TTY font

In case you find the tty font annoyingly small, I would recommend installing `terminus-font` and using one of the larger fonts available there (e.g. `setfont ter-m24b`).

To make this permanent,

*   Edit `/etc/vconsole.conf` to "FONT=ter-m24b"
*   Add `consolefont` to HOOKS="..."
*   Run `mkinitcpio -p linux`