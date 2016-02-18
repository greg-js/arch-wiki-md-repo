| **Device** | **Status** | **Modules** |
| Intel | Working | xf86-video-intel |
| Nvidia | Working | nouveau *or* nvidia |
| Touchpad | Working | xf86-input-synaptics |
| Camera | Working | linux-uvc |
| Wi-Fi | Working | iwlwifi |
| Bluetooth | Working | btusb |
| Ethernet | Working | alx |
| Card reader | Working | rtsx_usb |

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop")

## Contents

*   [1 Hardware overview](#Hardware_overview)
*   [2 Networking](#Networking)
*   [3 Input](#Input)
*   [4 Video](#Video)
*   [5 Alien FX](#Alien_FX)
*   [6 Issues](#Issues)

## Hardware overview

Tested configuration:

lspci:

```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor DRAM Controller (rev 06) 
00:01.0 PCI bridge: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor PCI Express x16 Controller (rev 06) 
00:02.0 VGA compatible controller: Intel Corporation 4th Gen Core Processor Integrated Graphics Controller (rev 06) 
00:03.0 Audio device: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor HD Audio Controller (rev 06) 
00:04.0 Signal processing controller: Intel Corporation Device 0c03 (rev 06) 
00:14.0 USB controller: Intel Corporation 8 Series/C220 Series Chipset Family USB xHCI (rev 05) 
00:16.0 Communication controller: Intel Corporation 8 Series/C220 Series Chipset Family MEI Controller #1 (rev 04) 
00:1a.0 USB controller: Intel Corporation 8 Series/C220 Series Chipset Family USB EHCI #2 (rev 05) 
00:1b.0 Audio device: Intel Corporation 8 Series/C220 Series Chipset High Definition Audio Controller (rev 05) 
00:1c.0 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #3 (rev d5) 
00:1c.3 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #4 (rev d5) 
00:1c.4 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #5 (rev d5) 
00:1d.0 USB controller: Intel Corporation 8 Series/C220 Series Chipset Family USB EHCI #1 (rev 05) 
00:1f.0 ISA bridge: Intel Corporation HM87 Express LPC Controller (rev 05) 
00:1f.2 RAID bus controller: Intel Corporation 82801 Mobile SATA Controller [RAID mode] (rev 05) 
00:1f.3 SMBus: Intel Corporation 8 Series/C220 Series Chipset Family SMBus Controller (rev 05) 
01:00.0 3D controller: NVIDIA Corporation GM204M [GeForce GTX 970M] (rev ff) 
02:00.0 Ethernet controller: Qualcomm Atheros Killer E220x Gigabit Ethernet Controller (rev 10) 
03:00.0 Network controller: Intel Corporation Wireless 7265 (rev 59) 
04:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS5227 PCI Express Card Reader (rev 01)

```

lsusb:

```
Bus 002 Device 002: ID 8087:8000 Intel Corp.  
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub 
Bus 001 Device 002: ID 8087:8008 Intel Corp.  
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub 
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub 
Bus 003 Device 003: ID 8087:0a2a Intel Corp.  
Bus 003 Device 002: ID 187c:0528 Alienware Corporation  
Bus 003 Device 004: ID 1bcf:28b6 Sunplus Innovation Technology Inc.  
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Networking

Wi-Fi & Bluetooth:

```
Intel Corporation Wireless 7265

```

Wi-Fi - Supported out-of-the-box Bluetooth - TODO Wired ethernet:

```
Qualcomm Atheros Killer E220x Gigabit Ethernet Controller

```

## Input

Suported out-of-the-box

See more at: [Synaptics](/index.php/Synaptics "Synaptics")

Keyboard: For Macro keys - see : [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys")

NOTE: Keyboard doesn't have Menu key.

## Video

Nvidia & Intel video card configuration: [Bumblebee](/index.php/Bumblebee "Bumblebee")

## Alien FX

Currently unsupported by pyAlienFx and alienfx[[1]](https://github.com/erlkonig/alienfx) have some diff from previous version.

## Issues

Sound don't switch to headphone, after plug jack

For fix: Add

```
'options snd-hda-intel position_fix=1' 

```

to

```
/etc/modprobe.d/alsa-base.conf

```