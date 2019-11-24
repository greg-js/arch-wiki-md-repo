Related articles

*   [Lenovo ThinkPad T490](/index.php/Lenovo_ThinkPad_T490 "Lenovo ThinkPad T490")
*   [Lenovo ThinkPad T490s](/index.php?title=Lenovo_ThinkPad_T490s&action=edit&redlink=1 "Lenovo ThinkPad T490s (page does not exist)")
*   [Lenovo ThinkPad T480](/index.php/Lenovo_ThinkPad_T480 "Lenovo ThinkPad T480")
*   [Lenovo ThinkPad T480s](/index.php/Lenovo_ThinkPad_T480s "Lenovo ThinkPad T480s")
*   [Lenovo ThinkPad T470](/index.php/Lenovo_ThinkPad_T470 "Lenovo ThinkPad T470")

| **Device** | **Status** |
| [AMDGPU](/index.php/AMDGPU "AMDGPU") | Yes |
| [Wireless](/index.php/Wireless "Wireless") | Yes |
| [ALSA](/index.php/ALSA "ALSA") | Yes |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [Webcam](/index.php/Webcam "Webcam") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes |
| [Mobile internet](/index.php/ThinkPad_mobile_Internet "ThinkPad mobile Internet") | not tested |
| Fingerprint Sensor | No¹ |
| MicroSD Reader | Yes |
| 

1.  Support for Synaptics 06cb:00bd is under development. See [here](https://gitlab.freedesktop.org/libfprint/libfprint/issues/181) and [here](https://gitlab.freedesktop.org/libfprint/libfprint/merge_requests/63).

 |

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware](#Hardware)
*   [2 Backlight](#Backlight)
*   [3 Power management](#Power_management)
    *   [3.1 Suspend and resume](#Suspend_and_resume)
    *   [3.2 TLP](#TLP)

## Hardware

Using kernel 5.3.11-arch1-1-ARCH

```
Version: ThinkPad T490
Product Name: 20NJCTO1WW

```

additional hardware information from `lsusb` and `lspci` can be found bellow:

`lsusb`

```
Bus 005 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 004 Device 005: ID 06cb:00bd Synaptics, Inc. 
Bus 004 Device 004: ID 04f2:b681 Chicony Electronics Co., Ltd 
Bus 004 Device 003: ID 05e3:0610 Genesys Logic, Inc. 4-port hub
Bus 004 Device 002: ID 8087:0025 Intel Corp. 
Bus 004 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

`lspci`

```
00:00.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Root Complex
00:00.2 IOMMU: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 IOMMU
00:01.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 00h-1fh) PCIe Dummy Host Bridge
00:01.2 PCI bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 PCIe GPP Bridge [6:0]
00:01.3 PCI bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 PCIe GPP Bridge [6:0]
00:01.4 PCI bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 PCIe GPP Bridge [6:0]
00:01.6 PCI bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 PCIe GPP Bridge [6:0]
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
02:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller SM981/PM981/PM983
03:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 0e)
03:00.1 Serial controller: Realtek Semiconductor Co., Ltd. Device 816a (rev 0e)
03:00.2 Serial controller: Realtek Semiconductor Co., Ltd. Device 816b (rev 0e)
03:00.3 IPMI Interface: Realtek Semiconductor Co., Ltd. Device 816c (rev 0e)
03:00.4 USB controller: Realtek Semiconductor Co., Ltd. Device 816d (rev 0e)
04:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 10)
05:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS522A PCI Express Card Reader (rev 01)
06:00.0 VGA compatible controller: Advanced Micro Devices, Inc. [AMD/ATI] Picasso (rev d2)
06:00.1 Audio device: Advanced Micro Devices, Inc. [AMD/ATI] Raven/Raven2/Fenghuang HDMI/DP Audio Controller
06:00.2 Encryption controller: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 10h-1fh) Platform Security Processor
06:00.3 USB controller: Advanced Micro Devices, Inc. [AMD] Raven USB 3.1
06:00.4 USB controller: Advanced Micro Devices, Inc. [AMD] Raven USB 3.1
06:00.5 Multimedia controller: Advanced Micro Devices, Inc. [AMD] Raven/Raven2/FireFlight/Renoir Audio Processor
06:00.6 Audio device: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 10h-1fh) HD Audio Controller

```

## Backlight

You need to add `acpi_backlight=native` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

## Power management

### Suspend and resume

Users have reported that the laptop is waking up immediately after entering suspending (see [[1]](https://www.reddit.com/r/thinkpad/comments/ckkbej/t495_linux_avoid/) and [[2]](https://www.reddit.com/r/thinkpad/comments/cveeyl/linux_on_t495t495sx395_suspendresume_fix/)). However, this seems to be fixed in the latest kernel. Suspend and resume works fine out-of-the-box.

### TLP

If you have installed [TLP](/index.php/TLP "TLP") to enable advance power management, you might notice that USB ports will not work under battery mode. Disable [Runtime Power Management](https://linrunner.de/en/tlp/docs/tlp-configuration.html#runtimepm) for USB controllers to fix this. To get PCIe device addresses of USB controllers:

```
$ lspci | grep -i usb

```

The first column of the output is the address:

```
03:00.4 USB controller: Realtek Semiconductor Co., Ltd. Device 816d (rev 0e)
07:00.3 USB controller: Advanced Micro Devices, Inc. [AMD] Raven USB 3.1
07:00.4 USB controller: Advanced Micro Devices, Inc. [AMD] Raven USB 3.1

```

To disable runtime power management for these devices, edit `/etc/default/tlp`:

 `/etc/default/tlp`  `RUNTIME_PM_BLACKLIST="03:00.4 07:00.3 07:00.4"`