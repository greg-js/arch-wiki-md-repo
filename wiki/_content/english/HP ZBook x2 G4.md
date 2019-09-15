<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Overview](#Overview)
*   [2 Configuration](#Configuration)
    *   [2.1 TouchScreen and Stylus](#TouchScreen_and_Stylus)
    *   [2.2 Video](#Video)
    *   [2.3 Bluetooth](#Bluetooth)
*   [3 Hardware information](#Hardware_information)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Backlight not working](#Backlight_not_working)

## Overview

Basic functionality works out of the box. Suspending the machine doesn't work out of the box.

| **Device** | **Status** | **Modules** |
| Graphics | **Working** | nvidia |
| Wireless | **Working** | iwlwifi |
| Audio | **Onboard Working; Audio via HDMI/DisplayPort Broken** | snd_hda_intel |
| Touchscreen | **Working** | wacom |
| Stylus | **Working** | wacom,usbhid |
| Buttons around screen | **Broken** |
| Accelerometer | **Working** | hid_sensor_accel_3d |
| Touchpad | **Working** | hid_multitouch |
| Camera | **Working** | uvcvideo |
| Card Reader | **???** |
| Bluetooth | **Working** | btintel |
| Fingerprint Reader | **???** |
| Smartcard reader | **???** |

## Configuration

### TouchScreen and Stylus

Touchscreen works with the Wacom driver (package: [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom)).

### Video

Nvidia graphics works well

The HDMI port works (except no audio).

### Bluetooth

The Bluetooth adapter works out of the box. It was tested with bluetooth speakers

## Hardware information

The output of *lspci* is

```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v6/7th Gen Core Processor Host Bridge/DRAM Registers (rev 02)
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 02)
00:13.0 Non-VGA unclassified device: Intel Corporation Sunrise Point-LP Integrated Sensor Hub (rev 21)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:15.0 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #0 (rev 21)
00:15.1 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #1 (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:16.3 Serial controller: Intel Corporation Device 9d3d (rev 21)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #1 (rev f1)
00:1c.2 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #3 (rev f1)
00:1c.3 PCI bridge: Intel Corporation Device 9d13 (rev f1)
00:1c.4 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #5 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Intel(R) 100 Series Chipset Family LPC Controller/eSPI Controller - 9D4E (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
01:00.0 VGA compatible controller: NVIDIA Corporation GM107GLM [Quadro M620 Mobile] (rev a2)
02:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS522A PCI Express Card Reader (rev 01)
03:00.0 Network controller: Intel Corporation Wireless 8265 / 8275 (rev 78)
6f:00.0 Non-Volatile memory controller: Toshiba America Info Systems Device 0116

```

The output of *lsusb* is

```
Bus 002 Device 002: ID 0bda:5666 Realtek Semiconductor Corp. 
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 005: ID 05c8:0808 Cheng Uei Precision Industry Co., Ltd (Foxlink) 
Bus 001 Device 004: ID 8087:0a2b Intel Corp. 
Bus 001 Device 003: ID 1fc9:0088 NXP Semiconductors 
Bus 001 Device 002: ID 03f0:0a56 Hewlett-Packard 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Troubleshooting

### Backlight not working

The screen backlight is only exposed through the Nvidia driver.