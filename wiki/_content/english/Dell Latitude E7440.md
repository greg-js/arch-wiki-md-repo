The Dell Latitude E7440 is a business Ultrabook™. Generally speaking, it has nice support of (Arch) Linux.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware Overview](#Hardware_Overview)
*   [2 Further Information about other Configurations](#Further_Information_about_other_Configurations)
*   [3 Installation](#Installation)
*   [4 Drivers](#Drivers)
*   [5 What does not work](#What_does_not_work)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 "Invalid partition table!" when booting](#"Invalid_partition_table!"_when_booting)
    *   [6.2 Keyboard inputs the same character multiple times on one keypress](#Keyboard_inputs_the_same_character_multiple_times_on_one_keypress)
    *   [6.3 SSD in the mSATA slot is only recognized after waking from susped](#SSD_in_the_mSATA_slot_is_only_recognized_after_waking_from_susped)
    *   [6.4 Freeze before going to suspend when lid is closed](#Freeze_before_going_to_suspend_when_lid_is_closed)
    *   [6.5 Wifi-problems with bluetooth enabled](#Wifi-problems_with_bluetooth_enabled)
    *   [6.6 Wifi problems when coming back from supend state](#Wifi_problems_when_coming_back_from_supend_state)
    *   [6.7 Hang with 4.2.0 kernel when docking with E-Port Plus and external monitors](#Hang_with_4.2.0_kernel_when_docking_with_E-Port_Plus_and_external_monitors)
*   [7 See also](#See_also)

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

## Further Information about other Configurations

On the configuration Intel i7-4600U with 256 GB SSD harddrive, 8 GB RAM, Arch Linux could be installed in UEFI partitioning without any problem (wireless also working). A22 version is stable and tested with Arch Linux 2018.01 base release (Januar 2018).

## Installation

The instructions below focus on GPT partitioning scheme, and relies on UEFI features of the laptop.

**Before any installation please make sure that latest system BIOS firmware is installed first**.

*   A USB flash drive can be prepared on another computer. Firmware update process does not need an operating system and it can be done with BIOS utilities of the laptop.
*   The latest BIOS firmware, which is an EXE file, can be downloaded from the ["Dell website"](https://www.dell.com/support/home/us/en/19/product-support/product/latitude-e7440-ultrabook/drivers).
*   On Windows, the firmware can be burned with [Rufus](https://rufus.akeo.ie/) into a bootable USB flash drive. USB Flash drive can be made UEFI/GPT bootable.
*   After the USB flash is prepared, plug the USB flash stick, boot the laptop by pressing F12 and follow the instructions to boot the USB flash.
*   After the firmware update, during reboot press F2 and check whether the shown BIOS version is the one which is burned.

You can follow the [Installation guide](/index.php/Installation_guide "Installation guide") to get yourself up and running.

Further remarks for this laptop:

*   After setting up ESP and having installed a boot manager (rEFind), make sure that BIOS was able to detect ESP and boot manager and could show its entries in UEFI setings.
*   Wireless connection can be set up during the installation without any problem.
*   UEFI with GPT harddisk partitioning works properly.
*   It is advisable to partition the disks in 1 GB aligment for maximum performance (see below)

Following partitioning scheme was tested on a 256GB SSD drive:

*   /dev/sda1/ ESP with label ESP, to be mounted to /boot/efi, file system FAT32\. As mentioned in ["Managing EFI Boot Loaders for Linux: Basic Principles"](http://www.rodsbooks.com/efi-bootloaders/principles.html), the ESP should have 550 MB at least. For max. performance on SSD, 1 GB was allocated.
*   /dev/sda2/ file system ext4 - 1 GB boundary (2nd 1 GB area of the SSD). It can be reserved for multi-boot installations in the future.
*   /dev/sda3/ swap with label SWAP, 8 GB for the laptop with 8 GB. The end sector is last sector of the 1st 10 GB of SSD.
*   /dev/sda4/ to be mounted as/data, file system ext4 and can be shared between many Linux installations. This is a 40 GB area which end is aligned to 1st 64 GB of SSD. End of 1st 10 GB and 24 GB beginning was not allocated. This was reserved if 8 GB RAM is upgraded to 16 GB RAM for which at least 16 GB swap could be needed. Since 1st 2x 1GB was reserved for ESP and sda2, this area starts at 24GB boundary, thus giving 40 GB to the end of 1st 64 GB.
*   /dev/sda5 file system ext4, to be mounted to /, 2nd 64 GB.
*   With the scheme above, an 256GB SSD has been partitioned for the 1st 2x 64 GB. The last two 64GB regions can be partitioned for other Linux operating systems. In [Partitioning](/index.php/Partitioning "Partitioning") it is advised to reserve 15-20 GB for a distro. For maximum flexibility 64 GB is taken in the scheme above.

## Drivers

*   [Intel graphics](/index.php/Intel_graphics "Intel graphics") for HD4400 graphics card.
*   [Wireless#iwlwifi](/index.php/Wireless#iwlwifi "Wireless") for Intel 7260 wifi card.
*   [Synaptics](/index.php/Synaptics "Synaptics") for Touchpad
*   [Fan speed control#Dell laptops](/index.php/Fan_speed_control#Dell_laptops "Fan speed control") to control fan speed. There is only one fan on this laptop, detected on the right. Don't forget to disable BIOS fan speed control to be able to use custom fan speed config.

## What does not work

*   The touchpad is not usable (the pointer jumps & clicks randomly), the keyboard inputs are randomly repeated. This problem is described in the [bug #1258837 on ubuntu launchpad](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1258837).
    *   I have never experienced the issue with touchpad, however, it can be a bit too sensitive. BIOS version A14 should fix the keyboard issue
        *   BIOS A14 does appear to fix the repeated key press issue on my E7440
*   Webcam does not work with Virtualbox (as of community/virtualbox 4.3.6-1), but it works with native programs such as skype.
*   There is no driver for the fingerprint sensor.
*   Occassionally crashes/freezes/hangs when docked and then changing display modes
    *   Tested with Dell E-Port Plus II, using two external monitors together with the laptop display (three displays total)

## Troubleshooting

### "Invalid partition table!" when booting

If you use BIOS+[MBR](/index.php/MBR "MBR") boot method and msdos partition table, the BIOS may show this error message before entering [Syslinux](/index.php/Syslinux "Syslinux") or other [boot loaders](/index.php/Boot_loader "Boot loader"). To bypass it, press Enter. To prevent it, put the "boot" flag on a primary partition (instead of a logical partition). You may refer to the wiki page of your boot loader to see how this works. It may be a "kindly reminder" to Windows users, since Windows can only boot on primary partitions.

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

### Wifi problems when coming back from supend state

When your wifi is gone after resume try going to BIOS and deactivate the functionality to turn wifi and wwan down when ethernet cable is connected.

### Hang with 4.2.0 kernel when docking with E-Port Plus and external monitors

After updating to the 4.2.0 kernel (in testing as of 9/9/15) my latitude hangs when docked in an Dell E-Port Plus with an external monitor connected. I reverted back to 4.1.6 for now.

## See also

[Dell Latitude E7440 | Post-installation et optimisation (French)](http://williamhollacsek.com/blog/2013/09/12/dell-latitude-e7440-optimisation)