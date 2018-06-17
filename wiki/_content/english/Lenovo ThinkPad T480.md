| **Device** | **Status** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Wireless](/index.php/Wireless "Wireless") | Yes |
| [ALSA](/index.php/ALSA "ALSA") | Yes |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [Webcam](/index.php/Webcam "Webcam") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes |
| Fingerprint Sensor |

This article covers the installation and configuration of Arch Linux on a Lenovo T480 laptop. Everything seems to work pretty much out the box.

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

## Contents

*   [1 Hardware](#Hardware)
*   [2 Suspend / Hibernation](#Suspend_.2F_Hibernation)
*   [3 TrackPoint and Touchpad](#TrackPoint_and_Touchpad)
*   [4 Power management/Throttling issues](#Power_management.2FThrottling_issues)

## Hardware

Using kernel 4.16.8-1-ARCH

```
Product Name: 20L5CTO1WW
Version: ThinkPad T480
SKU Number: LENOVO_MT_20L5_BU_Think_FM_ThinkPad T480
Product Name: 20L5CTO1WW

```

`lspci` returns something like:

```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v6/7th Gen Core Processor Host Bridge/DRAM Registers (rev 08)
00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 620 (rev 07)
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 08)
00:08.0 System peripheral: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th Gen Core Processor Gaussian Mixture Model
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:15.0 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #0 (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #1 (rev f1)
00:1c.6 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #7 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1)
00:1d.2 PCI bridge: Intel Corporation Device 9d1a (rev f1)
00:1f.0 ISA bridge: Intel Corporation Device 9d4e (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (4) I219-V (rev 21)
03:00.0 Network controller: Intel Corporation Wireless 8265 / 8275 (rev 78)
3d:00.0 Non-Volatile memory controller: Lenovo Device 0003

```

`lsusb` returns something like:

```
Bus 002 Device 005: ID 0bda:0316 Realtek Semiconductor Corp. 
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 06cb:009a Synaptics, Inc. 
Bus 001 Device 003: ID 04f2:b604 Chicony Electronics Co., Ltd 
Bus 001 Device 002: ID 8087:0a2b Intel Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Suspend / Hibernation

Suspend and Hibernation work out of the box. The T480 does not have the same issues as the [X1 Carbon Gen 6](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_6)#Suspend_issues "Lenovo ThinkPad X1 Carbon (Gen 6)")

## TrackPoint and Touchpad

TrackPoint and Touchpad work out of the box and do not seem to have the same issues as the [X1 Carbon Gen 6](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_6)#TrackPoint_and_Touchpad_issues "Lenovo ThinkPad X1 Carbon (Gen 6)")

## Power management/Throttling issues

See

*   X1 Carbon Gen 6 [Power management/Throttling issues](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_6)#Power_management.2FThrottling_issues "Lenovo ThinkPad X1 Carbon (Gen 6)")
*   ThinkPad T480s [Thermal Throttling Fix](/index.php/Lenovo_ThinkPad_T480s#Thermal_Throttling_Fix "Lenovo ThinkPad T480s")
*   [https://github.com/erpalma/lenovo-throttling-fix](https://github.com/erpalma/lenovo-throttling-fix)