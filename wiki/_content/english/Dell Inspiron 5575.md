This is an install and configuration guide for the Dell Inspiron 15 000 Series (Model 5575) laptop, Ryzen 5 2500U with Vega Mobile graphics.

See the [Laptop/Dell](/index.php/Laptop/Dell "Laptop/Dell") chart for information on other Dell laptops.

## Contents

*   [1 Hardware Details](#Hardware_Details)
*   [2 Installation](#Installation)
*   [3 Configuration](#Configuration)
    *   [3.1 X](#X)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Boot](#Boot)
        *   [4.1.1 GRUB](#GRUB)
            *   [4.1.1.1 Booting in blind mode error](#Booting_in_blind_mode_error)
        *   [4.1.2 Screen freezes](#Screen_freezes)

## Hardware Details

lspci output:

```
00:00.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15d0
00:00.2 IOMMU: Advanced Micro Devices, Inc. [AMD] Device 15d1
00:01.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 00h-0fh) PCIe Dummy Host Bridge
00:01.6 PCI bridge: Advanced Micro Devices, Inc. [AMD] Device 15d3
00:01.7 PCI bridge: Advanced Micro Devices, Inc. [AMD] Device 15d3
00:08.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 00h-0fh) PCIe Dummy Host Bridge
00:08.1 PCI bridge: Advanced Micro Devices, Inc. [AMD] Device 15db
00:08.2 PCI bridge: Advanced Micro Devices, Inc. [AMD] Device 15dc
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
01:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8101/2/6E PCI Express Fast/Gigabit Ethernet controller (rev 07)
02:00.0 Network controller: Qualcomm Atheros QCA9377 802.11ac Wireless Network Adapter (rev 31)
03:00.0 VGA compatible controller: Advanced Micro Devices, Inc. [AMD/ATI] Raven Bridge [Radeon Vega Series / Radeon Vega Mobile Series] (rev c4)
03:00.1 Audio device: Advanced Micro Devices, Inc. [AMD/ATI] Device 15de
03:00.2 Encryption controller: Advanced Micro Devices, Inc. [AMD] Device 15df
03:00.3 USB controller: Advanced Micro Devices, Inc. [AMD] Device 15e0
03:00.4 USB controller: Advanced Micro Devices, Inc. [AMD] Device 15e1
03:00.6 Audio device: Advanced Micro Devices, Inc. [AMD] Device 15e3
04:00.0 SATA controller: Advanced Micro Devices, Inc. [AMD] FCH SATA Controller [AHCI mode] (rev 61)

```

lsusb output:

```
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 005: ID 0cf3:e009 Qualcomm Atheros Communications 
Bus 003 Device 004: ID 27c6:5301  
Bus 003 Device 003: ID 0bda:0129 Realtek Semiconductor Corp. RTS5129 Card Reader Controller
Bus 003 Device 002: ID 1a40:0101 Terminus Technology Inc. Hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 0c45:6a06 Microdia 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Installation

See [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch")

## Configuration

### X

Make sure you enable the TearFree option in the xorg file configuration (i.e, `/etc/X11/xorg.conf.d/10-amdgpu.conf`).

```
Section "Device"
	Identifier "AMD" 
	Driver "amdgpu"
	Option "TearFree" "true"
EndSection

```

## Troubleshooting

Along with this section, check [AMDGPU#Loading](/index.php/AMDGPU#Loading "AMDGPU") as well.

### Boot

#### GRUB

##### Booting in blind mode error

Add the line

```
insmod all_video

```

in your grub.cfg

#### Screen freezes

The boot process normally gets stuck at certain point of the boot process and the cursor blinking stops. You can check if the caps lock LED still works. If that's the case, it means that **only** the amdgpu driver is gone. The rest of the system will be functional, meaning:

*   You can ssh to that machine
*   You can perform login and some debugging commands in blind mode, dumping their output into some files in the hard disk for posterior checks.

One workaround is to boot the linux kernel with the nomodeset argument, just to get to the console login; however, so far it has not been possible to launch X through vesa.

The other workaround is to boot without the nomodeset argument in the kernel command line, so the amdgpu driver will be loaded into memory. Then, login to root either by ssh or blind mode metehods, and keep unloading/loading the amdgpu module until the screen is unfrozen:

```
# rmmod amdgpu
# modprobe amdgpu

```

Usually, in the second or third time that you enter the previous commands the screen will be back.

This error is somehow related to how the amdgpu driver gets information from the pci port. A bug is to be reported for this.