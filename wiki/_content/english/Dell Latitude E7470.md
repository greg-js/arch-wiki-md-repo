The Dell Latitude E7470 is a 14" business notebook released in the first quarter of 2016.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware Overview](#Hardware_Overview)
*   [2 What works](#What_works)
*   [3 What doesn't work](#What_doesn't_work)
*   [4 What was not tested](#What_was_not_tested)

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

## What works

Almost everything works:

*   Video: Intel HD 520
*   Audio: Intel HD Audio with ALSA
*   Ethernet
*   Wireless: Intel 8260
*   Bluetooth
*   Suspend to RAM
*   Keyboard, touchpad and pointing stick
*   Keyboard backlight control
*   Screen backlight control
*   Fn-lock
*   HDMI output
*   Webcam (only 480p)
*   UEFI BIOS update with [fwupd](https://www.archlinux.org/packages/?name=fwupd)

## What doesn't work

*   Fingerprint reader (tracked at [https://gitlab.freedesktop.org/libfprint/libfprint/issues/88](https://gitlab.freedesktop.org/libfprint/libfprint/issues/88))

## What was not tested

*   Suspend to disk
*   Mini DisplayPort
*   SmartCard reader
*   NFC