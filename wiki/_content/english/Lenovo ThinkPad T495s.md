| **Device** | **Status** |
| [AMD graphics](/index.php/AMDGPU "AMDGPU") | Yes |
| [Wireless](/index.php/Wireless "Wireless") | Yes |
| [ALSA](/index.php/ALSA "ALSA") | Yes |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [Webcam](/index.php/Webcam "Webcam") | Yes |
| [Fingerprint Sensor](/index.php/Fprint "Fprint") | ? |
| [Mobile Broadband](/index.php/ThinkPad_mobile_internet "ThinkPad mobile internet") | ? |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes |
| Smartcard Reader | ? |

This article covers the installation and configuration of Arch Linux on a Lenovo T495s laptop. Almost everything seems to work pretty much out the box. Yet untested: wwan, smartcardreader

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware](#Hardware)
*   [2 AMD Graphics](#AMD_Graphics)
*   [3 Fingerprint reader](#Fingerprint_reader)
*   [4 Backlight](#Backlight)

## Hardware

Using kernel 5.2.5-arch1-1-ARCH.

```
Release Date: 2019
Product Name: Thinkpad T495s
SKU Number: 20QKS01E00

```

`lspci` returns something like:

```
00:00.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Root Complex 
00:00.2 IOMMU: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 IOMMU 
00:01.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 00h-1fh) PCIe Dummy Host Bridge 
00:01.2 PCI bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 PCIe GPP Bridge [6:0] 
00:01.3 PCI bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 PCIe GPP Bridge [6:0] 
00:01.4 PCI bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 PCIe GPP Bridge [6:0] 
00:01.7 PCI bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 PCIe GPP Bridge [6:0] 
00:08.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 00h-1fh) PCIe Dummy Host Bridge 
00:08.1 PCI bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Internal PCIe GPP Bridge 0 to Bus A 
00:14.0 SMBus: Advanced Micro Devices, Inc. [AMD] FCH SMBus Controller (rev 61) 
00:14.3 ISA bridge: Advanced Micro Devices, Inc. [AMD] FCH LPC Bridge (rev 51) 
00:18.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Device 24: Function 0 
00:18.1 Host bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Device 24: Function 1 
00:18.2 Host bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Device 24: Function 2 
00:18.3 Host bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Device 24: Function 3 
00:18.4 Host bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Device 24: Function 4 
00:18.5 Host bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Device 24: Function 5 
00:18.6 Host bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Device 24: Function 6 
00:18.7 Host bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Device 24: Function 7 
01:00.0 Network controller: Intel Corporation Wireless-AC 9260 (rev 29) 
02:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller SM981/PM981 
03:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 0e) 
03:00.1 Serial controller: Realtek Semiconductor Co., Ltd. Device 816a (rev 0e) 
03:00.2 Serial controller: Realtek Semiconductor Co., Ltd. Device 816b (rev 0e) 
03:00.3 IPMI Interface: Realtek Semiconductor Co., Ltd. Device 816c (rev 0e) 
03:00.4 USB controller: Realtek Semiconductor Co., Ltd. Device 816d (rev 0e) 
04:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS522A PCI Express Card Reader (rev 01) 
05:00.0 VGA compatible controller: Advanced Micro Devices, Inc. [AMD/ATI] Picasso (rev d1) 
05:00.1 Audio device: Advanced Micro Devices, Inc. [AMD/ATI] Raven/Raven2/Fenghuang HDMI/DP Audio Controller 
05:00.2 Encryption controller: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 10h-1fh) Platform Security Processor 
05:00.3 USB controller: Advanced Micro Devices, Inc. [AMD] Raven USB 3.1 
05:00.4 USB controller: Advanced Micro Devices, Inc. [AMD] Raven USB 3.1 
05:00.5 Multimedia controller: Advanced Micro Devices, Inc. [AMD] Raven/Raven2/FireFlight/Renoir Audio Processor 
05:00.6 Audio device: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 10h-1fh) HD Audio Controller 

```

`lsusb` returns something like:

```
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 013: ID 0bda:0316 Realtek Semiconductor Corp. 
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 5986:2113 Acer, Inc 
Bus 001 Device 003: ID 8087:0a2b Intel Corp. 
Bus 001 Device 005: ID 046d:c246 Logitech, Inc. Gaming Mouse G300
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## AMD Graphics

The opensource [AMDGPU](/index.php/AMDGPU "AMDGPU") drivers work correctly with no special modification.

## Fingerprint reader

Fingerprint sensor 06cb:00bd is not supported by libfprint right now. There is some talk of an upcoming [driver](https://gitlab.freedesktop.org/vincenth/libfprint/tree/synaptics-driver-20190617) though.

## Backlight

Backlight works correctly by manipulating the values, between 0-255, inside `/sys/class/backlight/amdgpu_bl0/brightness` or using a backlight managing utility.

`systemd-backlight@backlight:acpi_video0.service` requires [masking](/index.php/Systemd#Using_units "Systemd") as it seems to be triggered and fails on boot.