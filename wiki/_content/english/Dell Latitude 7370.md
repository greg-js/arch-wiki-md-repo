These laptops are a part of the Latitude 13 7000 Series featuring Intel Skylake [[1]](http://www.dell.com/us/business/p/latitude-13-7370-laptop/pd). This series does have _some_ relation to the [Dell XPS 13 (2016)](/index.php/Dell_XPS_13_(2016) "Dell XPS 13 (2016)") for general reference.

## Contents

*   [1 dock](#dock)
*   [2 bios](#bios)
    *   [2.1 updating](#updating)
*   [3 card reader](#card_reader)
*   [4 touchpad](#touchpad)
*   [5 displays](#displays)
*   [6 DisplayLink](#DisplayLink)
*   [7 lspci and lsusb](#lspci_and_lsusb)
    *   [7.1 lspci](#lspci)
    *   [7.2 lsusb](#lsusb)
*   [8 known issues](#known_issues)
    *   [8.1 suspend](#suspend)
    *   [8.2 no keyboard](#no_keyboard)

## dock

The TB15 Thunderbolt dock is no longer supported by dell, and is no longer being sold [[2]](http://www.itcentralpoint.com/dell-recalls-tb15-docking-station). The TB15 thunderbolt dock is still a work-in-progress for support, but the use of it is anectodtal [[3]](http://en.community.dell.com/techcenter/os-applications/f/4613/t/19678284). It seems to currently work best when plugged in before booting and avoiding any form of hot-plugging [[4]](https://github.com/01org/thunderbolt-software/issues/2).

The TB15 has been replaced by the TB16 [[5]](http://www.dell.com/en-us/shop/dell-thunderbolt-dock-tb16-240w/apd/452-bcnu/pc-accessories).

Alternative, the WD15 seems to work as an alternative docking station [[6]](http://www.dell.com/en-us/shop/dell-dock-wd15-with-180w-adapter/apd/450-aeuo/pc-accessories).

## bios

As of this writing, the latest version of the BIOS for the 7370 is version 1.9.3

### updating

Download the BIOS update from the dell site and place it either at the root of a FAT-formatted USB disk, or within /boot on the hard drive (If using EFI). Reboot and hit F12 during startup, selecting "BIOS Flash Update". The simple file browser should see the executable, select it and allow the update to occur.

## card reader

The Broadcom reader "should work" via [ccid](https://www.archlinux.org/packages/?name=ccid) and [pcsclite](https://www.archlinux.org/packages/?name=pcsclite), but requires an firmware/BIOS update that must be run in Windows [[7]](http://www.dell.com/support/home/us/en/19/Drivers/DriversDetails?driverId=JP80V&fileId=3559873652&osCode=W764&productCode=latitude-e5570-laptop&languageCode=en&categoryId=SY)

Supporting documentation regarding the card reader: [[8]](https://ludovicrousseau.blogspot.fr/2016/08/broadcom-ccid-readers.html) [[9]](https://bugs.launchpad.net/ubuntu/+source/pcsc-lite/+bug/1596662)

## touchpad

There is a known issue where the touchpad is detected as "ImPS/2 BYD TouchPad", a patch is in the works [[10]](https://patchwork.kernel.org/patch/9204273/).

## displays

Due to being HiDPI it is also common to notice latency when using desktop environments like Gnome-Shell. Installing "vulkan-intel" appears to alleviate some of these issues.

## DisplayLink

In order to connect to external projectors using an external dongle, you will need to configure [DisplayLink](/index.php/DisplayLink "DisplayLink").

## lspci and lsusb

On kernel '4.11.0-rc1-mainline' via [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/) with WD15 docking station connected

### lspci

```
00:00.0 Host bridge: Intel Corporation Skylake Host Bridge/DRAM Registers (rev 08)
00:02.0 VGA compatible controller: Intel Corporation HD Graphics 515 (rev 07)
00:04.0 Signal processing controller: Intel Corporation Skylake Processor Thermal Subsystem (rev 08)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:1c.0 PCI bridge: Intel Corporation Device 9d10 (rev f1)
00:1c.4 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #5 (rev f1)
00:1c.7 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #8 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Device 9d46 (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
01:00.0 PCI bridge: Intel Corporation DSL6540 Thunderbolt 3 Bridge [Alpine Ridge 4C 2015]
02:00.0 PCI bridge: Intel Corporation DSL6540 Thunderbolt 3 Bridge [Alpine Ridge 4C 2015]
02:01.0 PCI bridge: Intel Corporation DSL6540 Thunderbolt 3 Bridge [Alpine Ridge 4C 2015]
02:02.0 PCI bridge: Intel Corporation DSL6540 Thunderbolt 3 Bridge [Alpine Ridge 4C 2015]
02:04.0 PCI bridge: Intel Corporation DSL6540 Thunderbolt 3 Bridge [Alpine Ridge 4C 2015]
37:00.0 USB controller: Intel Corporation DSL6540 USB 3.1 Controller [Alpine Ridge]
6c:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller (rev 01)
6d:00.0 Network controller: Intel Corporation Wireless 8260 (rev 3a)
6e:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS525A PCI Express Card Reader (rev 01)

```

### lsusb

```
Bus 004 Device 005: ID 0451:8140 Texas Instruments, Inc. TUSB8041 4-Port Hub
Bus 004 Device 004: ID 0451:8140 Texas Instruments, Inc. TUSB8041 4-Port Hub
Bus 004 Device 003: ID 0bda:8153 Realtek Semiconductor Corp. RTL8153 Gigabit Ethernet Adapter
Bus 004 Device 002: ID 0424:5537 Standard Microsystems Corp. 
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 007: ID 413c:9016 Dell Computer Corp. 
Bus 003 Device 006: ID 0461:4d51 Primax Electronics, Ltd 0Y357C PMX-MMOCZUL (B) [Dell Laser Mouse]
Bus 003 Device 004: ID 0bda:4014 Realtek Semiconductor Corp. 
Bus 003 Device 005: ID 0451:8142 Texas Instruments, Inc. TUSB8041 4-Port Hub
Bus 003 Device 003: ID 0451:8142 Texas Instruments, Inc. TUSB8041 4-Port Hub
Bus 003 Device 002: ID 0424:2137 Standard Microsystems Corp. 
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 005: ID 0bda:5768 Realtek Semiconductor Corp. 
Bus 001 Device 004: ID 0a5c:5834 Broadcom Corp. 
Bus 001 Device 003: ID 04f3:2335 Elan Microelectronics Corp. 
Bus 001 Device 006: ID 8087:0a2b Intel Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## known issues

### suspend

It appears the system can get into a state in which suspend will stop working (system will suspend but upon attempt to resume will cold boot)[[11]](https://bbs.archlinux.org/viewtopic.php?id=207543). Current resolution appears to be to perform a shutdown within the system and suspend should start working again. Newer bios versions also have improved this issue, though it can still occur.

### no keyboard

It appears that on [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/) the system will boot without a keyboard. This can be resolved by adding `i8042` to the MODULES line in `/etc/mkinitcpio.conf`