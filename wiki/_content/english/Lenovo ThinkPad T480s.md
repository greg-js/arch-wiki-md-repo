| **Device** | **Status** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Wireless](/index.php/Wireless "Wireless") | Yes |
| [ALSA](/index.php/ALSA "ALSA") | no beep |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [Webcam](/index.php/Webcam "Webcam") | Yes |
| Fingerprint Sensor | No |
| [Mobile Broadband](/index.php/ThinkPad_mobile_internet "ThinkPad mobile internet") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") |
| Smartcard Reader | Yes |

This article covers the installation and configuration of Arch Linux on a Lenovo T480s laptop. Everything seems to work pretty much out the box.

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

## Contents

*   [1 Hardware](#Hardware)
    *   [1.1 Fingerprint reader](#Fingerprint_reader)
*   [2 Powersaving](#Powersaving)
*   [3 See also](#See_also)

## Hardware

Using kernel 4.15.7-1-ARCH.

```
Release Date: 01/22/2018
Product Name: 20L7CTO1WW
SKU Number: LENOVO_MT_20L7_BU_Think_FM_ThinkPad T480s
Product Name: 20L7CTO1WW

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
00:1c.4 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #5 (rev f1)
00:1c.6 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #7 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Device 9d4e (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (4) I219-V (rev 21)
04:00.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
05:00.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
05:01.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
05:02.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
06:00.0 System peripheral: Intel Corporation JHL6240 Thunderbolt 3 NHI (Low Power) [Alpine Ridge LP 2016] (rev 01)
3c:00.0 USB controller: Intel Corporation Device 15c1 (rev 01)
3d:00.0 Network controller: Intel Corporation Wireless 8265 / 8275 (rev 78)
3e:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd Device a808

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

### Fingerprint reader

Fingerprint sensor 06cb:009a is not supported by libfprint right now. There is a project to reverse enginer windows driver - [https://github.com/nmikhailov/Validity90](https://github.com/nmikhailov/Validity90) .

## Powersaving

Without special configuration and with default firmware settings, power usage is a bit high (around 7,5W in idle). There are a few knobs to improve battery life:

*   Set "Thunderbolt BIOS Assist Mode" to "Enabled" in the EFI firmware interface. This seems to reduce number of idle wakeups.
*   Disable unused peripherals under "Security" -> "I/O port access" in the firmware. This especially applies to the SD/MMC-cardreader, which seems to drain some power even when idle

As of Kernel 4.15, DisplayPort PSR (Panel self refresh) is disabled by default and broken when forcibly enabled (system hangs after a few seconds, display lag). 4.17-rc1 seems to improve a lot in this regard, but PSR still sometimes causes the screen to freeze for a few seconds.

## See also

*   [T480s install video playlist](https://www.youtube.com/watch?v=gRvYTLntgv4&list=PLiKgVPlhUNuz9k0xIp7PGUV5mmDdTS1vJ)