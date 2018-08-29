| **Device** | **Status** | **Modules** |
| Integrated Video | Working | i915 |
| Video | Working | amdgpu |
| Wireless | Working | iwlwifi |
| Bluetooth | Working | bluetooth |
| Audio | Mostly Working | snd_hda_intel |
| Touchpad | Working | serio |
| Touchscreen | Working | hid_multitouch |
| Card Reader | Working | rtsx_pci |
| Wireless switch | Working | intel-hid |
| Function/Multimedia Keys | Working | intel-vbtn |
| Tablet-Mode | Working | intel-vbtn |
| Accelerometer | Manual binding | intel-ish-ipc |

## Contents

*   [1 Hardware info](#Hardware_info)
    *   [1.1 Specifications](#Specifications)
    *   [1.2 lspci](#lspci)
    *   [1.3 lsusb](#lsusb)
*   [2 Installation](#Installation)
*   [3 Issues](#Issues)
    *   [3.1 Speaker](#Speaker)
    *   [3.2 Accelerometer](#Accelerometer)

## Hardware info

### Specifications

This model was released in February 2016.

*   Intel Core i7-8705G with Intel HD Graphics 630 (3.1 GHz, up to 4.1 GHz, 8 MB cache, 4 cores)
*   15.6" 4K (3840x2160) Ultra HD IPS WLED multitouch display
*   16 GB LPDDR3-1866 SDRAM
*   2 TB M.2 SDD
*   2 USB Type C Thunderbolt port, 1 USB 3.0 Type A ports, 1 HDMI port, 1 headphone/microphone jack
*   1 SD media card reader
*   802.11ac (2x2) and Bluetooth 4.0
*   Bang & Olufsen quad speakers
*   6-cell, 64.5 Wh Li-ion battery
*   Webcam
*   Backlit keyboard

### lspci

*   v00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v6/7th Gen Core Processor Host Bridge/DRAM Registers (rev 05)

00:01.0 PCI bridge: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor PCIe Controller (x16) (rev 05)

*   00:02.0 VGA compatible controller: Intel Corporation Device 591b (rev 04)
*   00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 05)
*   00:13.0 Non-VGA unclassified device: Intel Corporation Sunrise Point-H Integrated Sensor Hub (rev 31)
*   00:14.0 USB controller: Intel Corporation Sunrise Point-H USB 3.0 xHCI Controller (rev 31)
*   00:14.2 Signal processing controller: Intel Corporation Sunrise Point-H Thermal subsystem (rev 31)
*   00:15.0 Signal processing controller: Intel Corporation Sunrise Point-H Serial IO I2C Controller #0 (rev 31)
*   00:16.0 Communication controller: Intel Corporation Sunrise Point-H CSME HECI #1 (rev 31)
*   00:17.0 SATA controller: Intel Corporation Sunrise Point-H SATA Controller [AHCI mode] (rev 31)
*   00:1c.0 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #1 (rev f1)
*   00:1c.4 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #5 (rev f1)
*   00:1c.5 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #6 (rev f1)
*   00:1d.0 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #9 (rev f1)
*   00:1e.0 Signal processing controller: Intel Corporation Sunrise Point-H Serial IO UART #0 (rev 31)
*   00:1e.2 Signal processing controller: Intel Corporation Sunrise Point-H Serial IO SPI #0 (rev 31)
*   00:1f.0 ISA bridge: Intel Corporation Sunrise Point-H LPC Controller (rev 31)
*   00:1f.2 Memory controller: Intel Corporation Sunrise Point-H PMC (rev 31)
*   00:1f.3 Audio device: Intel Corporation CM238 HD Audio Controller (rev 31)
*   00:1f.4 SMBus: Intel Corporation Sunrise Point-H SMBus (rev 31)
*   01:00.0 Display controller: Advanced Micro Devices, Inc. [AMD/ATI] Polaris 22 [Radeon RX Vega M GL] (rev ff)
*   6d:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS525A PCI Express Card Reader (rev 01)
*   6e:00.0 Network controller: Intel Corporation Wireless 8265 / 8275 (rev 78)
*   6f:00.0 Non-Volatile memory controller: Toshiba America Info Systems Device 0116

### lsusb

*   Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
*   Bus 001 Device 003: ID 8087:0a2b Intel Corp.
*   Bus 001 Device 002: ID 05c8:0815 Cheng Uei Precision Industry Co., Ltd (Foxlink)
*   Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

## Installation

Installing Arch was mostly without hiccup; you do need to disable secure boot (F10 for BIOS options; F9 for boot options). Dual boot was not tested. The laptop does not have a CD drive, so you have to use a USB stick. The UEFI also would not startup from the USB stick, but you can browse the USB, and choose the loader.efi to startup from.

## Issues

### Speaker

Only the front speakers work out of the box right now.

### Accelerometer

The accelerometer is not found by any userspace programs, Running `G_MESSAGES_DEBUG=all /usr/sbin/iio-sensor-proxy ` from [iio-sensor-proxy](https://aur.archlinux.org/packages/iio-sensor-proxy/) gives ` ** (process:12472): DEBUG: 11:45:31.305: Could not find any supported sensors ` 

The accelerometer is connected to a new Intel Integrated Sensor Hub which is not supported by the kernel yet, but can be manually bound to the `intel-ish-ipc` driver.

 `$ lspci -nn` 
```
...
00:13.0 Non-VGA unclassified device [0000]: Intel Corporation Sunrise Point-H Integrated Sensor Hub [8086:a135] (rev 31)
...
```

```
# modprobe intel-ish-ipc
# echo "8086 a135" > /sys/bus/pci/drivers/intel_ish_ipc/new_id

```
 `$ monitor-sensor` 
```
    Waiting for iio-sensor-proxy to appear
+++ iio-sensor-proxy appeared
=== Has accelerometer (orientation: undefined)
=== No ambient light sensor
    Accelerometer orientation changed: normal

```