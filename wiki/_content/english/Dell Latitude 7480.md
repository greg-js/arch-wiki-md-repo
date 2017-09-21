Dell Latitude 7480 is a 14" business Ultrabook released in first quarter of 2017.

## Contents

*   [1 Installation](#Installation)
*   [2 Hardware Overview](#Hardware_Overview)
*   [3 What works](#What_works)
*   [4 What does not work](#What_does_not_work)

## Installation

Before installing, disable secure boot in UEFI settings. Installing linux on this laptop is quite straight forward. Follow any up to date installation guide, e.g. this one: [Installation guide](/index.php/Installation_guide "Installation guide")

## Hardware Overview

Test configuration: Core i5-7300u, 1080p display without an IR camera Output of `lspci -nn` is as below

```
00:00.0 Host bridge [0600]: Intel Corporation Xeon E3-1200 v6/7th Gen Core Processor Host Bridge/DRAM Registers [8086:5904] (rev 02)
00:02.0 VGA compatible controller [0300]: Intel Corporation HD Graphics 620 [8086:5916] (rev 02)
00:04.0 Signal processing controller [1180]: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem [8086:1903] (rev 02)
00:14.0 USB controller [0c03]: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller [8086:9d2f] (rev 21)
00:14.2 Signal processing controller [1180]: Intel Corporation Sunrise Point-LP Thermal subsystem [8086:9d31] (rev 21)
00:15.0 Signal processing controller [1180]: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #0 [8086:9d60] (rev 21)
00:15.1 Signal processing controller [1180]: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #1 [8086:9d61] (rev 21)
00:15.2 Signal processing controller [1180]: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #2 [8086:9d62] (rev 21)
00:16.0 Communication controller [0780]: Intel Corporation Sunrise Point-LP CSME HECI #1 [8086:9d3a] (rev 21)
00:17.0 SATA controller [0106]: Intel Corporation Sunrise Point-LP SATA Controller [AHCI mode] [8086:9d03] (rev 21)
00:1c.0 PCI bridge [0604]: Intel Corporation Sunrise Point-LP PCI Express Root Port #1 [8086:9d10] (rev f1)
00:1c.2 PCI bridge [0604]: Intel Corporation Sunrise Point-LP PCI Express Root Port #3 [8086:9d12] (rev f1)
00:1f.0 ISA bridge [0601]: Intel Corporation Device [8086:9d4e] (rev 21)
00:1f.2 Memory controller [0580]: Intel Corporation Sunrise Point-LP PMC [8086:9d21] (rev 21)
00:1f.3 Audio device [0403]: Intel Corporation Device [8086:9d71] (rev 21)
00:1f.4 SMBus [0c05]: Intel Corporation Sunrise Point-LP SMBus [8086:9d23] (rev 21)
00:1f.6 Ethernet controller [0200]: Intel Corporation Ethernet Connection (4) I219-LM [8086:15d7] (rev 21)
01:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS525A PCI Express Card Reader [10ec:525a] (rev 01)
02:00.0 Network controller [0280]: Intel Corporation Wireless 8265 / 8275 [8086:24fd] (rev 78)

```

The output of `lsusb`

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 8087:0a2b Intel Corp. 
Bus 001 Device 002: ID 1bcf:2b96 Sunplus Innovation Technology Inc. 
Bus 001 Device 004: ID 0a5c:5834 Broadcom Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## What works

Almost all the hardware works after configuring drivers, including

*   WiFi
*   Bluetooth
*   Touchpad
*   Webcam

## What does not work

The fingerprint reader (`0a5c:5834`) is not supported because no linux driver exists so far (Sep 2017).