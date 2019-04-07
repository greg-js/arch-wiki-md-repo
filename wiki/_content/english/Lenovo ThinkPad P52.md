The Lenovo P52 is a quad or hex core Intel 8th generation Laptop.

## Pre-Installation

Arch on a Lenovo P52 is an amazing combination.

**Before you begin:** There are some possible "BIOS BRICKING" settings. The settings are not directly related to installing Arch, but most Arch users will make configuration changes in the same areas where these settings can be modified. So I'm offering this warning here.

Make sure to update your BIOS to **V1.17 or later** current is v1.24 as of March 2019\. Earlier versions of the BIOS may become inoperable if you select certain settings:

1) Hybrid vs discrete graphics - [https://forums.lenovo.com/t5/ThinkPad-P-and-W-Series-Mobile/P52-won-t-start-after-change-to-only-discrete-graphic-card/m-p/4265065](https://forums.lenovo.com/t5/ThinkPad-P-and-W-Series-Mobile/P52-won-t-start-after-change-to-only-discrete-graphic-card/m-p/4265065)

2) Thunderbolt 3 Support - [https://forums.lenovo.com/t5/ThinkPad-P-and-W-Series-Mobile/Lenovo-P52-bricked-by-selecting-BIOS-thunderbolt-support-for/td-p/4207538/page/12](https://forums.lenovo.com/t5/ThinkPad-P-and-W-Series-Mobile/Lenovo-P52-bricked-by-selecting-BIOS-thunderbolt-support-for/td-p/4207538/page/12)

Note: You can update the BIOS using the bootable (CD) update option from Lenovo, or just update the BIOS using the pre-packaged Windows installation and software and then continue with Arch installation once the BIOS is updated.

## Installation

Follow the [Beginner's guide](/index.php/Beginner%27s_guide "Beginner's guide") to install Arch.

## lspci

`lspci` returns this on the P52:

```
00:00.0 Host bridge: Intel Corporation 8th Gen Core Processor Host Bridge/DRAM Registers (rev 07)
00:01.0 PCI bridge: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor PCIe Controller (x16) (rev 07)
00:02.0 VGA compatible controller: Intel Corporation Device 3e9b
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 07)
00:08.0 System peripheral: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th Gen Core Processor Gaussian Mixture Model
00:12.0 Signal processing controller: Intel Corporation Cannon Lake PCH Thermal Controller (rev 10)
00:14.0 USB controller: Intel Corporation Cannon Lake PCH USB 3.1 xHCI Host Controller (rev 10)
00:14.2 RAM memory: Intel Corporation Cannon Lake PCH Shared SRAM (rev 10)
00:14.3 Network controller: Intel Corporation Wireless-AC 9560 [Jefferson Peak] (rev 10)
00:15.0 Serial bus controller [0c80]: Intel Corporation Device a368 (rev 10)
00:16.0 Communication controller: Intel Corporation Cannon Lake PCH HECI Controller (rev 10)
00:16.3 Serial controller: Intel Corporation Device a363 (rev 10)
00:1b.0 PCI bridge: Intel Corporation Device a340 (rev f0)
00:1c.0 PCI bridge: Intel Corporation Device a338 (rev f0)
00:1c.7 PCI bridge: Intel Corporation Device a33f (rev f0)
00:1d.0 PCI bridge: Intel Corporation Cannon Lake PCH PCI Express Root Port 9 (rev f0)
00:1e.0 Communication controller: Intel Corporation Device a328 (rev 10)
00:1f.0 ISA bridge: Intel Corporation Device a30e (rev 10)
00:1f.3 Audio device: Intel Corporation Cannon Lake PCH cAVS (rev 10)
00:1f.4 SMBus: Intel Corporation Cannon Lake PCH SMBus Controller (rev 10)
00:1f.5 Serial bus controller [0c80]: Intel Corporation Cannon Lake PCH SPI Controller (rev 10)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (7) I219-LM (rev 10)
01:00.0 VGA compatible controller: NVIDIA Corporation GP104GLM [Quadro P3200 Mobile] (rev a1)
02:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller SM981/PM981
70:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS525A PCI Express Card Reader (rev 01)
71:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller SM981/PM981

```

`lsusb` returns something like this on the P52:

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 005: ID 06cb:009a Synaptics, Inc. 
Bus 001 Device 003: ID 5986:2113 Acer, Inc 
Bus 001 Device 002: ID 05e3:0608 Genesys Logic, Inc. Hub
Bus 001 Device 009: ID 8087:0aaa Intel Corp. 
Bus 001 Device 007: ID 058f:9540 Alcor Micro Corp. AU9540 Smartcard Reader
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```