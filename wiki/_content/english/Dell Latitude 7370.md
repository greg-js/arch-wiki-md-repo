These laptops are a part of the Latitude 13 7000 Series featuring Intel Skylake [[1]](http://www.dell.com/us/business/p/latitude-13-7370-laptop/pd). This series does have _some_ relation to the [Dell XPS 13 (2016)](/index.php/Dell_XPS_13_(2016) "Dell XPS 13 (2016)") for general reference.

## Contents

*   [1 kernel](#kernel)
*   [2 dock](#dock)
*   [3 card reader](#card_reader)
*   [4 displays](#displays)
*   [5 lspci and lsusb](#lspci_and_lsusb)
    *   [5.1 lspci](#lspci)
    *   [5.2 lsusb](#lsusb)
*   [6 known issues](#known_issues)
    *   [6.1 suspend](#suspend)

## kernel

It is highly suggest to run a 4.6 (or greater) kernel (currently outside of [core](/index.php/Official_repositories#core "Official repositories")) via something like [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/)

## dock

The TB15 thunderbolt dock is still a work-in-progress for support [[2]](http://en.community.dell.com/techcenter/os-applications/f/4613/t/19678284?pi22229=4). It seems to, currently, work best when plugged in before booting and avoiding any form of hot-plugging [[3]](https://github.com/01org/thunderbolt-software/issues/2)

## card reader

The Broadcom reader is currently not supported via [ccid](https://www.archlinux.org/packages/?name=ccid) and [pcsclite](https://www.archlinux.org/packages/?name=pcsclite)

## displays

The display is a hidpi display. If experiencing screen flashes during boot it could be advised to add the "i915" driver to the MODULES in mkinitcpio.conf and regenerate

```
 sudo mkinitcpio -p linux

```

## lspci and lsusb

On kernel '4.7.0-rc1-mainline' via [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/)

### lspci

```
 00:00.0 Host bridge: Intel Corporation Skylake Host Bridge/DRAM Registers (rev 08)
 00:02.0 VGA compatible controller: Intel Corporation Skylake Integrated Graphics (rev 07)
 00:04.0 Signal processing controller: Intel Corporation Skylake Processor Thermal Subsystem (rev 08)
 00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
 00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
 00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
 00:1c.0 PCI bridge: Intel Corporation Device 9d10 (rev f1)
 00:1c.4 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #5 (rev f1)
 00:1c.7 PCI bridge: Intel Corporation Device 9d17 (rev f1)
 00:1d.0 PCI bridge: Intel Corporation Device 9d18 (rev f1)
 00:1f.0 ISA bridge: Intel Corporation Device 9d46 (rev 21)
 00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
 00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
 00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
 6c:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller (rev 01)
 6d:00.0 Network controller: Intel Corporation Wireless 8260 (rev 3a)
 6e:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS525A PCI Express Card Reader (rev 01)

```

### lsusb

```
 Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
 Bus 001 Device 003: ID 0a5c:5805 Broadcom Corp. 
 Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## known issues

### suspend

It appears the system can get into a state in which suspend will stop working (system will suspend but upon attempt to resume will cold boot)[[4]](https://bbs.archlinux.org/viewtopic.php?id=207543). Current resolution appears to be to perform a shutdown within the system and suspend should start working again.