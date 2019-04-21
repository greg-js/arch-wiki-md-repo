The Lenovo Flex 6 is a flexible dual-mode laptop computer.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 14ARR (AMD Raven Ridge)](#14ARR_(AMD_Raven_Ridge))
    *   [1.1 PCI Devices (AMD)](#PCI_Devices_(AMD))
    *   [1.2 USB Devices](#USB_Devices)
    *   [1.3 Hardware Support](#Hardware_Support)
        *   [1.3.1 UEFI](#UEFI)
        *   [1.3.2 Video](#Video)
        *   [1.3.3 Touchpad](#Touchpad)
        *   [1.3.4 Touchscreen](#Touchscreen)
    *   [1.4 Issues](#Issues)
        *   [1.4.1 Wireless](#Wireless)
        *   [1.4.2 Firmware bug IOAPIC[x] not in IVRS table](#Firmware_bug_IOAPIC[x]_not_in_IVRS_table)

# 14ARR (AMD Raven Ridge)

## PCI Devices (AMD)

```
$ lspci
00:00.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15d0
00:00.2 IOMMU: Advanced Micro Devices, Inc. [AMD] Device 15d1
00:01.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 00h-0fh) PCIe Dummy Host Bridge
00:01.2 PCI bridge: Advanced Micro Devices, Inc. [AMD] Device 15d3
00:01.7 PCI bridge: Advanced Micro Devices, Inc. [AMD] Device 15d3
00:08.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 00h-0fh) PCIe Dummy Host Bridge
00:08.1 PCI bridge: Advanced Micro Devices, Inc. [AMD] Device 15db
00:14.0 SMBus: Advanced Micro Devices, Inc. [AMD] FCH SMBus Controller (rev 61)
00:14.3 ISA bridge: Advanced Micro Devices, Inc. [AMD] FCH LPC Bridge (rev 51)
00:18.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15e8
00:18.1 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15e9
00:18.2 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15ea
00:18.3 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15eb
00:18.4 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15ec
00:18.5 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15ed
00:18.6 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15ee
00:18.7 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15ef
01:00.0 Network controller: Realtek Semiconductor Co., Ltd. RTL8822BE 802.11a/b/g/n/ac WiFi adapter 
02:00.0 Non-Volatile memory controller: SK hynix Device 1327
03:00.0 VGA compatible controller: Advanced Micro Devices, Inc. [AMD/ATI] Raven Ridge [Radeon Vega Series / Radeon Vega Mobile Series] (rev c4)
03:00.1 Audio device: Advanced Micro Devices, Inc. [AMD/ATI] Device 15de
03:00.2 Encryption controller: Advanced Micro Devices, Inc. [AMD] Device 15df
03:00.3 USB controller: Advanced Micro Devices, Inc. [AMD] Device 15e0
03:00.4 USB controller: Advanced Micro Devices, Inc. [AMD] Device 15e1
03:00.6 Audio device: Advanced Micro Devices, Inc. [AMD] Device 15e3
03:00.7 Non-VGA unclassified device: Advanced Micro Devices, Inc. [AMD] Device 15e6

```

## USB Devices

```
$ lsusb
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 004: ID 06cb:0081 Synaptics, Inc. 
Bus 003 Device 003: ID 174f:2426 Syntek 
Bus 003 Device 002: ID 05e3:0608 Genesys Logic, Inc. Hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 0bda:b023 Realtek Semiconductor Corp. 
Bus 001 Device 002: ID 258a:0012  
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Hardware Support

### UEFI

Before installing any other OS (other than the default Windows 8/8.1) it is required to disable the secure boot option in the boot setup menu.

### Video

Works natively with [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu). However, you need to use kernel 4.17 or later.

### Touchpad

Recognized with [this kernel module](https://github.com/Syniurge/i2c-amd-mp2)

### Touchscreen

Recognized with [this kernel module](https://github.com/Syniurge/i2c-amd-mp2)

## Issues

### Wireless

The wireless card is supported, but you may run into an issue where the wireless card is hard blocked. Check if this is the case with:

```
$ rfkill

```

A solution is to block the lenovo ideapad drivers

edit the file

```
/etc/modprobe.d/blacklist.conf

```

and add this:

```
blacklist ideapad_laptop

```

### Firmware bug IOAPIC[x] not in IVRS table

More info on this issue [here](https://superuser.com/questions/1052023/ioapic0-not-in-ivrs-table).

Example of my paramters:

`ivrs_ioapic[4]=00:14.0 ivrs_ioapic[5]=00:00.1`

Before adding the above to your configuration, make sure you know how to edit your [kernel paramaters](/index.php/Kernel_parameters "Kernel parameters").