The Dell Latitude e7470 is a 14" business notebook.

## Contents

*   [1 Hardware Overview](#Hardware_Overview)
*   [2 Touchpad](#Touchpad)
*   [3 Installation](#Installation)
*   [4 What does not work](#What_does_not_work)

## Hardware Overview

Output of `lspci -nn`:

```
00:00.0 Host bridge [0600]: Intel Corporation Skylake Host Bridge/DRAM Registers [8086:1904] (rev 08)
00:02.0 VGA compatible controller [0300]: Intel Corporation HD Graphics 520 [8086:1916] (rev 07)
00:04.0 Signal processing controller [1180]: Intel Corporation Skylake Processor Thermal Subsystem [8086:1903] (rev 08)
00:14.0 USB controller [0c03]: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller [8086:9d2f] (rev 21)
00:14.2 Signal processing controller [1180]: Intel Corporation Sunrise Point-LP Thermal subsystem [8086:9d31] (rev 21)
00:16.0 Communication controller [0780]: Intel Corporation Sunrise Point-LP CSME HECI #1 [8086:9d3a] (rev 21)
00:16.3 Serial controller [0700]: Intel Corporation Device [8086:9d3d] (rev 21)
00:17.0 RAID bus controller [0104]: Intel Corporation 82801 Mobile SATA Controller [RAID mode] [8086:282a] (rev 21)
00:1c.0 PCI bridge [0604]: Intel Corporation Sunrise Point-LP PCI Express Root Port #5 [8086:9d14] (rev f1)
00:1d.0 PCI bridge [0604]: Intel Corporation Device [8086:9d1a] (rev f1)
00:1f.0 ISA bridge [0601]: Intel Corporation Sunrise Point-LP LPC Controller [8086:9d48] (rev 21)
00:1f.2 Memory controller [0580]: Intel Corporation Sunrise Point-LP PMC [8086:9d21] (rev 21)
00:1f.3 Audio device [0403]: Intel Corporation Sunrise Point-LP HD Audio [8086:9d70] (rev 21)
00:1f.4 SMBus [0c05]: Intel Corporation Sunrise Point-LP SMBus [8086:9d23] (rev 21)
00:1f.6 Ethernet controller [0200]: Intel Corporation Ethernet Connection I219-LM [8086:156f] (rev 21)
01:00.0 Network controller [0280]: Intel Corporation Wireless 8260 [8086:24f3] (rev 3a)
02:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS525A PCI Express Card Reader [10ec:525a] (rev 01)

```

Output of `lsusb`:

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 8087:0a2b Intel Corp. 
Bus 001 Device 003: ID 0a5c:5834 Broadcom Corp. 
Bus 001 Device 002: ID 1bcf:28b8 Sunplus Innovation Technology Inc. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Touchpad

Support for the ALPS touchpad included in Dell E7270 & E7470 was only added in Linux kernel 4.9, with some issues accidentally introduced in 4.13 and then refixed in 4.15\. The fixes were backported to Linux LTS kernels 4.9 & 4.14\. Earlier kernels didn't recognize the touchpad and used it in its emulated PS/2 mode, so changing options (like scroll direction, multi-touch gestures, etc.) was not possible.

## Installation

I followed the [Installation guide](/index.php/Installation_guide "Installation guide") to get up and running. All the basic stuff seems to work fine.

## What does not work

*   Fingerprint reader. The fingerprint reader does not seem to be supported by `fprintd` or `fingerprint-gui` yet. I did not put too much effort into searching. The usb id of the fingerprint reader is `0a5c:5834`