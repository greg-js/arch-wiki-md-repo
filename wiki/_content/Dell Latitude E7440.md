# Dell Latitude E7440

The Dell Latitude E7440 is a business Ultrabook™. Generally speaking, it has nice support of (Arch) Linux.

## Contents

*   [1 Hardware Overview](#Hardware_Overview)
*   [2 Installation](#Installation)
*   [3 Drivers](#Drivers)
*   [4 What does not work](#What_does_not_work)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 "Invalid partition table!" when booting](#.22Invalid_partition_table.21.22_when_booting)
    *   [5.2 Keyboard inputs the same character multiple times on one keypress](#Keyboard_inputs_the_same_character_multiple_times_on_one_keypress)
    *   [5.3 SSD in the mSATA slot is only recognized after waking from susped](#SSD_in_the_mSATA_slot_is_only_recognized_after_waking_from_susped)
    *   [5.4 Freeze before going to suspend when lid is closed](#Freeze_before_going_to_suspend_when_lid_is_closed)
    *   [5.5 Wifi-problems with bluetooth enabled](#Wifi-problems_with_bluetooth_enabled)
    *   [5.6 Hang with 4.2.0 kernel when docking with E-Port Plus and external monitors](#Hang_with_4.2.0_kernel_when_docking_with_E-Port_Plus_and_external_monitors)
*   [6 See also](#See_also)

## Hardware Overview

December 2013 model, configured with Intel Core i5-4300U, integrated Intel HD4400 graphics adapter, Intel Ethernet and wireless network adapter and a 1080p screen. Your configuration may differ from mine.

Output from `lspci -nn`: (2014-04-11)

```
00:00.0 Host bridge [0600]: Intel Corporation Haswell-ULT DRAM Controller [8086:0a04] (rev 0b)
00:02.0 VGA compatible controller [0300]: Intel Corporation Haswell-ULT Integrated Graphics Controller [8086:0a16] (rev 0b)
00:03.0 Audio device [0403]: Intel Corporation Device [8086:0a0c] (rev 0b)
00:14.0 USB controller [0c03]: Intel Corporation Lynx Point-LP USB xHCI HC [8086:9c31] (rev 04)
00:16.0 Communication controller [0780]: Intel Corporation Lynx Point-LP HECI #0 [8086:9c3a] (rev 04)
00:19.0 Ethernet controller [0200]: Intel Corporation Ethernet Connection I218-LM [8086:155a] (rev 04)
00:1b.0 Audio device [0403]: Intel Corporation Lynx Point-LP HD Audio Controller [8086:9c20] (rev 04)
00:1c.0 PCI bridge [0604]: Intel Corporation Lynx Point-LP PCI Express Root Port 1 [8086:9c10] (rev e4)
00:1c.3 PCI bridge [0604]: Intel Corporation Lynx Point-LP PCI Express Root Port 4 [8086:9c16] (rev e4)
00:1c.4 PCI bridge [0604]: Intel Corporation Lynx Point-LP PCI Express Root Port 5 [8086:9c18] (rev e4)
00:1d.0 USB controller [0c03]: Intel Corporation Lynx Point-LP USB EHCI #1 [8086:9c26] (rev 04)
00:1f.0 ISA bridge [0601]: Intel Corporation Lynx Point-LP LPC Controller [8086:9c43] (rev 04)
00:1f.2 SATA controller [0106]: Intel Corporation Lynx Point-LP SATA Controller 1 [AHCI mode] [8086:9c03] (rev 04)
00:1f.3 SMBus [0c05]: Intel Corporation Lynx Point-LP SMBus Controller [8086:9c22] (rev 04)
02:00.0 Network controller [0280]: Intel Corporation Wireless 7260 [8086:08b1] (rev 73)
03:00.0 SD Host controller [0805]: O2 Micro, Inc. Device [1217:8520] (rev 01)

```

Output from `lsusb`: (2014-04-11)

```
Bus 001 Device 002: ID 8087:8000 Intel Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 002 Device 003: ID 1bcf:2985 Sunplus Innovation Technology Inc. 
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Installation

You can follow the [Installation guide](/index.php/Installation_guide "Installation guide") to get yourself up and running. I simply transfered a 7mm SSD drive on my previous laptop to this one and the Arch Linux on it boots without errors.

## Drivers

*   [Intel graphics](/index.php/Intel_graphics "Intel graphics") for HD4400 graphics card. ===> MAJOR PERFORMANCE IMPACT:

After a very long research and several tens of reboots I came up with the conclusion that if you power on the laptop without having AC connected the overall GPU performance will be WAY worse than if you did with the AC connected. It does not matter whatsoever if you connect AC afterwards - GPU/OpenGL/drawing _IS_ going to be slow once you've started it without AC.

As a benchmark I've used the redraw time of pidgin GTK windows and the mouse moving speed of maps.google.com. Google maps should be very responsive and not laggy at all.

Tested on: i3-git, mesa-full-i965 and xf86-video-intel-git 2.99.911-1 but this was reproducing on the stable versions of mesa and i915 driver.

Laptop bios version A05\. ~~Meanwhile I've upgraded to bios version A08 and this issue seems to have been fixed.~~ Nope, it's still not fixed. If you want the video card to perform at full speed it is my impression you need to boot with the AC connected.

This is actually a "feature" called Intel SpeedStep, that reduces performance in order to extend battery life. It can be disabled in BIOS. The linux kernel seems to support it so it should be possible to configure this on OS level.

*   [Wireless#iwlwifi](/index.php/Wireless#iwlwifi "Wireless") for Intel 7260 wifi card.
*   [Synaptics](/index.php/Synaptics "Synaptics") for Touchpad

## What does not work

*   The touchpad is not usable (the pointer jumps & clicks randomly), the keyboard inputs are randomly repeated. This problem is described in the [bug #1258837 on ubuntu launchpad](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1258837).
    *   I have never experienced the issue with touchpad, however, it can be a bit too sensitive. BIOS version A14 should fix the keyboard issue --[Tachy](/index.php/User:Tachy "User:Tachy") ([talk](/index.php?title=User_talk:Tachy&action=edit&redlink=1 "User talk:Tachy (page does not exist)")) 09:02, 9 February 2015 (UTC)
        *   BIOS A14 does appear to fix the repeated key press issue on my E7440

*   The O2 Micro SD-card reader may only work with linux>=3.14.

*   ~~It seems that bluetooth on Intel 7260 is not working out of the box, but I don't know how to test it further. _Tested and seems to be working. Bluetooth is usable with "gnome-control-center bluetooth"._~~

*   Webcam does not work with Virtualbox (as of community/virtualbox 4.3.6-1), but it works with native programs such as skype.

*   There is no driver for the fingerprint sensor.

*   Occassionally crashes/freezes/hangs when docked and then changing display modes
    *   Tested with Dell E-Port Plus II, using two external monitors together with the laptop display (three displays total)
    *   Some of my Windows-using colleagues have also experienced this issue, so maybe it's a hardware/firmware bug --[Tachy](/index.php/User:Tachy "User:Tachy") ([talk](/index.php?title=User_talk:Tachy&action=edit&redlink=1 "User talk:Tachy (page does not exist)")) 14:15, 9 March 2015 (UTC)

## Troubleshooting

### "Invalid partition table!" when booting

If you use BIOS+[MBR](/index.php/MBR "MBR") boot method and msdos partition table, the BIOS may show this error message before entering [Syslinux](/index.php/Syslinux "Syslinux") or other [boot loaders](/index.php/Boot_loaders "Boot loaders"). To bypass it, press Enter. To prevent it, put the "boot" flag on a primary partition (instead of a logical partition). You may refer to the wiki page of your boot loader to see how this works. It may be a "kindly reminder" to Windows users, since Windows can only boot on primary partitions.

### Keyboard inputs the same character multiple times on one keypress

Happens with A10 bios. ~~Downgrading to A08 is the only fix for now~~. Also applies for Dell Latitude E7240.

**UPDATE:** A new BIOS version has been released, [A14](http://www.dell.com/support/home/us/en/04/Drivers/DriversDetails?driverId=0P7G1&fileId=3430208686), which addresses this problem with the internal keyboard.

### SSD in the mSATA slot is only recognized after waking from susped

Happened in BIOS < A10\. Upgrading to A10 appeared to be the only solution.

### Freeze before going to suspend when lid is closed

This seems to be related to [https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1301601](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1301601). Workaround 2 helps decrease frequency of freezes. For systemd, create a file in /usr/lib/systemd/system-sleep/ (e.g. 99switch_to_vt2) containing:

```
#!/bin/sh
# Possible workaround for bug:
# [https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1301601](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1301601)
#
# Switch to a VT before suspending and back after resume 
case "$1" in
    post)
        /bin/chvt 1
    ;;
    pre)
        /bin/chvt 2
    ;;
esac

```

### Wifi-problems with bluetooth enabled

Severe wifi problems (decresing traffic, connection drops) with bluetooth enabled. Workaround is to switch it off when not needed. This bug seems to be router-specific (happend with a Fritzbox).

### Hang with 4.2.0 kernel when docking with E-Port Plus and external monitors

After updating to the 4.2.0 kernel (in testing as of 9/9/15) my latitude hangs when docked in an Dell E-Port Plus with an external monitor connected. I reverted back to 4.1.6 for now.

## See also

[Dell Latitude E7440 | Post-installation et optimisation (French)](http://williamhollacsek.com/blog/2013/09/12/dell-latitude-e7440-optimisation)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dell_Latitude_E7440&oldid=402169](https://wiki.archlinux.org/index.php?title=Dell_Latitude_E7440&oldid=402169)"