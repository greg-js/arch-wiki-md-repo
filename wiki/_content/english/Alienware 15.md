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

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware overview](#Hardware_overview)
    *   [1.1 Alienware 15(early 2015)](#Alienware_15(early_2015))
    *   [1.2 Alienware 15 R2](#Alienware_15_R2)
    *   [1.3 Alienware 15 R3](#Alienware_15_R3)
    *   [1.4 Alienware 15 R4](#Alienware_15_R4)
*   [2 Networking](#Networking)
    *   [2.1 Qualcomm Atheros QCA6174 802.11ac Wireless Network Adapter](#Qualcomm_Atheros_QCA6174_802.11ac_Wireless_Network_Adapter)
*   [3 Input](#Input)
*   [4 Video](#Video)
    *   [4.1 NVIDIA Corporation GM204M [GeForce GTX 965M]](#NVIDIA_Corporation_GM204M_[GeForce_GTX_965M])
*   [5 Control of the light colors](#Control_of_the_light_colors)
*   [6 Issues](#Issues)
    *   [6.1 Alienware 15 R3](#Alienware_15_R3_2)

## Hardware overview

### Alienware 15(early 2015)

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

### Alienware 15 R2

lspci:

```
00:00.0 Host bridge: Intel Corporation Skylake Host Bridge/DRAM Registers (rev 07)
00:01.0 PCI bridge: Intel Corporation Skylake PCIe Controller (x16) (rev 07)
00:02.0 VGA compatible controller: Intel Corporation Skylake Integrated Graphics (rev 06)
00:04.0 Signal processing controller: Intel Corporation Skylake Processor Thermal Subsystem (rev 07)
00:14.0 USB controller: Intel Corporation Sunrise Point-H USB 3.0 xHCI Controller (rev 31)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-H Thermal subsystem (rev 31)
00:16.0 Communication controller: Intel Corporation Sunrise Point-H CSME HECI #1 (rev 31)
00:17.0 RAID bus controller: Intel Corporation 82801 Mobile SATA Controller [RAID mode] (rev 31)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #1 (rev f1)
00:1c.4 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #5 (rev f1)
00:1c.5 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #6 (rev f1)
00:1c.6 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #7 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-H LPC Controller (rev 31)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-H PMC (rev 31)
00:1f.3 Audio device: Intel Corporation Sunrise Point-H HD Audio (rev 31)
00:1f.4 SMBus: Intel Corporation Sunrise Point-H SMBus (rev 31)
01:00.0 3D controller: NVIDIA Corporation GM204M [GeForce GTX 965M] (rev a1)
3b:00.0 Ethernet controller: Qualcomm Atheros Killer E2400 Gigabit Ethernet Controller (rev 10)
3c:00.0 Network controller: Qualcomm Atheros QCA6174 802.11ac Wireless Network Adapter (rev 32)
3d:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS5227 PCI Express Card Reader (rev 01)

```

lsusb:

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 1bcf:2b8c Sunplus Innovation Technology Inc. 
Bus 001 Device 003: ID 0cf3:e300 Atheros Communications, Inc. 
Bus 001 Device 002: ID 187c:0528 Alienware Corporation 
Bus 001 Device 005: ID 04d9:a070 Holtek Semiconductor, Inc. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

### Alienware 15 R3

lspci:

```
00:00.0 Host bridge: Intel Corporation Skylake Host Bridge/DRAM Registers (rev 07)
00:01.0 PCI bridge: Intel Corporation Skylake PCIe Controller (x16) (rev 07)
00:01.2 PCI bridge: Intel Corporation Skylake PCIe Controller (x4) (rev 07)
00:02.0 VGA compatible controller: Intel Corporation HD Graphics 530 (rev 06)
00:04.0 Signal processing controller: Intel Corporation Skylake Processor Thermal Subsystem (rev 07)
00:14.0 USB controller: Intel Corporation Sunrise Point-H USB 3.0 xHCI Controller (rev 31)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-H Thermal subsystem (rev 31)
00:16.0 Communication controller: Intel Corporation Sunrise Point-H CSME HECI #1 (rev 31)
00:17.0 SATA controller: Intel Corporation Sunrise Point-H SATA controller [AHCI mode] (rev 31)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #1 (rev f1)
00:1c.4 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #5 (rev f1)
00:1c.5 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #6 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #9 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-H LPC Controller (rev 31)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-H PMC (rev 31)
00:1f.3 Audio device: Intel Corporation Sunrise Point-H HD Audio (rev 31)
00:1f.4 SMBus: Intel Corporation Sunrise Point-H SMBus (rev 31)
01:00.0 VGA compatible controller: NVIDIA Corporation GP104M [GeForce GTX 1070 Mobile] (rev ff)
3c:00.0 Ethernet controller: Qualcomm Atheros Killer E2400 Gigabit Ethernet Controller (rev 10)
3d:00.0 Network controller: Intel Corporation Wireless 8260 (rev 3a)
3e:00.0 Non-Volatile memory controller: Toshiba America Info Systems Device 0115 (rev 01)

```

lsusb:

```
Bus 002 Device 003: ID 2109:0812 VIA Labs, Inc. VL812 Hub
Bus 002 Device 002: ID 2109:0812 VIA Labs, Inc. VL812 Hub
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 007: ID 0bda:58c2 Realtek Semiconductor Corp. 
Bus 001 Device 005: ID 8087:0a2b Intel Corp. 
Bus 001 Device 003: ID 187c:0530 Alienware Corporation 
Bus 001 Device 009: ID 1a40:0101 Terminus Technology Inc. Hub
Bus 001 Device 008: ID 062a:4102 MosArt Semiconductor Corp. 
Bus 001 Device 006: ID 2109:2812 VIA Labs, Inc. VL812 Hub
Bus 001 Device 004: ID 258a:1006  
Bus 001 Device 002: ID 2109:2812 VIA Labs, Inc. VL812 Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

### Alienware 15 R4

lspci:

```
00:00.0 Host bridge: Intel Corporation 8th Gen Core Processor Host Bridge/DRAM Registers (rev 07)
00:01.0 PCI bridge: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor PCIe Controller (x16) (rev 07)
00:01.1 PCI bridge: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor PCIe Controller (x8) (rev 07)
00:01.2 PCI bridge: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor PCIe Controller (x4) (rev 07)
00:02.0 Display controller: Intel Corporation UHD Graphics 630 (Mobile)
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 07)
00:12.0 Signal processing controller: Intel Corporation Cannon Lake PCH Thermal Controller (rev 10)
00:14.0 USB controller: Intel Corporation Cannon Lake PCH USB 3.1 xHCI Host Controller (rev 10)
00:14.2 RAM memory: Intel Corporation Cannon Lake PCH Shared SRAM (rev 10)
00:15.0 Serial bus controller [0c80]: Intel Corporation Device a368 (rev 10)
00:16.0 Communication controller: Intel Corporation Cannon Lake PCH HECI Controller (rev 10)
00:17.0 SATA controller: Intel Corporation Device a353 (rev 10)
00:1d.0 PCI bridge: Intel Corporation Cannon Lake PCH PCI Express Root Port #9 (rev f0)
00:1d.6 PCI bridge: Intel Corporation Cannon Lake PCH PCI Express Root Port #15 (rev f0)
00:1d.7 PCI bridge: Intel Corporation Cannon Lake PCH PCI Express Root Port #16 (rev f0)
00:1f.0 ISA bridge: Intel Corporation Device a30e (rev 10)
00:1f.3 Audio device: Intel Corporation Cannon Lake PCH cAVS (rev 10)
00:1f.4 SMBus: Intel Corporation Cannon Lake PCH SMBus Controller (rev 10)
00:1f.5 Serial bus controller [0c80]: Intel Corporation Cannon Lake PCH SPI Controller (rev 10)
01:00.0 VGA compatible controller: NVIDIA Corporation GP104BM [GeForce GTX 1070 Mobile] (rev a1)
43:00.0 Non-Volatile memory controller: Toshiba America Info Systems Device 0116
44:00.0 Ethernet controller: Qualcomm Atheros Killer E2500 Gigabit Ethernet Controller (rev 10)
45:00.0 Network controller: Qualcomm Atheros QCA6174 802.11ac Wireless Network Adapter (rev 32)

```

lsusb:

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 1bcf:2b97 Sunplus Innovation Technology Inc. 
Bus 001 Device 002: ID 187c:0550 Alienware Corporation 
Bus 001 Device 004: ID 0cf3:e300 Qualcomm Atheros Communications 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

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

### Qualcomm Atheros QCA6174 802.11ac Wireless Network Adapter

As of the main website you can install the supported driver for [QCA6174 802.11ac Wireless Network Adapter](http://www.killernetworking.com/support/knowledge-base/17-linux/20-killer-wireless-ac-in-linux-ubuntu-debian).

First download the **board.bin** file via wget and put it into your firmware library:

```
wget [http://www.killernetworking.com/support/board.bin](http://www.killernetworking.com/support/board.bin)
sudo mkdir -p /lib/firmware/ath10k/QCA6174/hw3.0/
sudo mv board.bin /lib/firmware/ath10k/QCA6174/hw3.0/

```

and then download the specific firmware binary and move it into your firmware library:

```
wget [https://github.com/kvalo/ath10k-firmware/blob/master/QCA6174/hw3.0/firmware-4.bin_WLAN.RM.2.0-00180-QCARMSWPZ-1](https://github.com/kvalo/ath10k-firmware/blob/master/QCA6174/hw3.0/firmware-4.bin_WLAN.RM.2.0-00180-QCARMSWPZ-1)
sudo mv firmware-4.bin_WLAN.RM.2.0-00180-QCARMSWPZ-1 /lib/firmware/ath10k/QCA6174/hw3.0/firmware-4.bin

```

then reboot and you are good to go.

## Input

Suported out-of-the-box

See more at: [Synaptics](/index.php/Synaptics "Synaptics")

Keyboard: For Macro keys - see : [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys")

NOTE: Keyboard doesn't have Menu key.

## Video

Nvidia & Intel video card configuration: [Bumblebee](/index.php/Bumblebee "Bumblebee")

### NVIDIA Corporation GM204M [GeForce GTX 965M]

Currently not supported by [Bumblebee](/index.php/Bumblebee "Bumblebee") (Tested on Alienware 15 R2) Please install only [Intel](/index.php/Intel "Intel") driver via [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)

## Control of the light colors

*   Currently unsupported by pyAlienFx and alienfx[[1]](https://github.com/erlkonig/alienfx) have some diff from previous version.
*   Probably supported by [alienware-kbl](https://github.com/rsm-gh/alienware-kbl), a software to manage the light colors with a graphical interface, python or bash commands.

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

### Alienware 15 R3

Xorg freezes when starting with discrete graphics card OFF

For fix: Add

```
 acpi_osi=! acpi_osi="Windows 2009"

```

to Kernel options.