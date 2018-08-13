## Contents

*   [1 Hardware info](#Hardware_info)
    *   [1.1 Specifications](#Specifications)
    *   [1.2 lspci](#lspci)
    *   [1.3 lsusb](#lsusb)
*   [2 Installation](#Installation)
*   [3 Tweaks](#Tweaks)
    *   [3.1 Scaling](#Scaling)

## Hardware info

### Specifications

This model was released in late 2017.

*   [Intel® Core™ i7-8550U Processor (4 cores, 8 threads, 1.8 GHz, 4.00 GHz turbo, 8M Cache)](https://ark.intel.com/products/122589/Intel-Core-i7-8550U-Processor-8M-Cache-up-to-4_00-GHz)
*   NVIDIA® GeForce® MX150 (2 GB GDDR5)
*   15.6" 4K (3840x2160) Ultra HD IPS eDP WLED multitouch display
*   16 GB Samsung DDR4-2400 / SK Hynix DDR4-2400 / Micron DDR4-2667
*   512 GB NVMe Samsung PM961 SSD
*   1 Thunderbolt™ USB Type C port, 1 USB 3.1 Type C™ Gen 1, 3 USB 3.1 Gen 1 (all USB has HP Sleep and Charge), 1 HDMI 2.0 port, 1 SD card reader, 1 headphone/microphone jack
*   Intel® 802.11b/g/n/ac (2x2) Wi-Fi® and Bluetooth® 4.2
*   Bang & Olufsen speakers
*   6-cell, 79,2 Wh Li-ion battery (50% in 30 min)
*   HP TrueVision FHD-IR-Camera, Dual-Array-Digital-Microphone
*   Backlit keyboard
*   35,6 x 25,1 x 1,79 cm
*   2.01 kg

### lspci

```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v6/7th Gen Core Processor Host Bridge/DRAM Registers (rev 08)
00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 620 (rev 07)
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 08)
00:13.0 Non-VGA unclassified device: Intel Corporation Sunrise Point-LP Integrated Sensor Hub (rev 21)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:15.0 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #0 (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #1 (rev f1)
00:1c.4 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #5 (rev f1)
00:1c.6 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #7 (rev f1)
00:1c.7 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #8 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Intel(R) 100 Series Chipset Family LPC Controller/eSPI Controller - 9D4E (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
01:00.0 3D controller: NVIDIA Corporation GP108M [GeForce MX150] (rev ff)
3b:00.0 Network controller: Intel Corporation Wireless 8265 / 8275 (rev 78)
3c:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS525A PCI Express Card Reader (rev 01)
3d:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller SM961/PM961

```

### lsusb

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 8087:0a2b Intel Corp. 
Bus 001 Device 002: ID 064e:3401 Suyin Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Installation

Disable secure boot (F10 for BIOS options; F9 for boot options). Dual boot work with Windows 10 ( Windows tends to store time in local, which can be changed to UTC with a registry edit).

## Tweaks

### Scaling

200% on Gnome, plus Large font on in Universal Access.