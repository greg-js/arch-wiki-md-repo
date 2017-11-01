| **Device** | **Status** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [NVIDIA graphics](/index.php/NVIDIA "NVIDIA") | Yes |
| [Wireless](/index.php/Wireless "Wireless") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes |
| Mobile Broadband | Yes |
| [Webcam](/index.php/Webcam "Webcam") | Yes |
| Microsoft Hello | No |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [Touchscreen](/index.php/Touchscreen "Touchscreen") | Yes |
| Fingerprint Reader | No |

This article covers the installation and configuration of Arch Linux on a Lenovo T25 Anniversary Edition laptop. It is based on the Lenovo T470 laptop so most of the hardware is identical and therefore should work like the T470.

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

## Contents

*   [1 Firmware (e.g. bios and peripherals)](#Firmware_.28e.g._bios_and_peripherals.29)
*   [2 Kernel and hardware support](#Kernel_and_hardware_support)
    *   [2.1 Screen backlight](#Screen_backlight)
    *   [2.2 Thunderbolt 3](#Thunderbolt_3)
    *   [2.3 UEFI boot](#UEFI_boot)
*   [3 PCI and USB devices](#PCI_and_USB_devices)
    *   [3.1 T25 model 20K7](#T25_model_20K7)
        *   [3.1.1 lspci](#lspci)
        *   [3.1.2 lsusb](#lsusb)
*   [4 See also](#See_also)

## Firmware (e.g. bios and peripherals)

As of writing, the current BIOS version is 1.42\. By visiting the downloads section (T25) an ISO can be downloaded and burned to disk which will perform the update [from Lenovo](https://pcsupport.lenovo.com/de/en/products/laptops-and-netbooks/thinkpad-t-series-laptops/thinkpad-t25-type-20k7/downloads). Or [extracted and copied on a USB Stick](http://www.thinkwiki.org/wiki/BIOS_Upgrade#Booting_from_a_USB_Flash_drive).

## Kernel and hardware support

[Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration") with Kaby Lake seems to work fine via va-api.

As noted in [Intel graphics](/index.php/Intel_graphics "Intel graphics"), the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver seems to cause more issue than the builtin `modesetting` Xorg driver. Works fine without the intel driver (on a Skylake configuration).

138a:0097 will hopefully be supported as part of [Validity90](https://github.com/nmikhailov/Validity90).

### Screen backlight

With the `intel` driver ([xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) the `xbacklight` brightness control isn't working. It is possible that, with the good `acpi_*` kernel parameters, the backlight related keys do their job.

Other workaround exists, such as described [on this post](https://bbs.archlinux.org/viewtopic.php?pid=1449243#p1449243) or in the wiki [acpid#Enabling_backlight_control](/index.php/Acpid#Enabling_backlight_control "Acpid"). Using the [acpilight](https://aur.archlinux.org/packages/acpilight/) package as a `xbacklight` replacement works well. You can also check [this repository](https://lab.knightsofnii.com/kristaba/tpacpi-backlight)] as a base to add the ACPI rules to call `xbacklight` when backlight keys are pressed.

**Note:** The [acpilight](https://aur.archlinux.org/packages/acpilight/) package is known to allow controlling the ThinkPad keyboard backlight. Similar ACPI rules should allow to toggle it when the keyboard backlight key is pressed.

### Thunderbolt 3

With the latest kernel (4.13.9 as of writing), the *Alpine Ridge* thunderbolt 3 controller is recognized without any additional configuration. Using a generic thunderbolt 3 to HDMI + USB3 hub works out of the box (the HDMI output is recognized by xrandr as DP-1 output).

### UEFI boot

After configuring the BIOS setup to allow UEFI boot (either *UEFI only* or *both*), it works flawlessly.

## PCI and USB devices

### T25 model 20K7

Kernel '4.13.9-1-ARCH'

#### lspci

```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v6/7th Gen Core Processor Host Bridge/DRAM Registers (rev 02)
00:02.0 VGA compatible controller: Intel Corporation HD Graphics 620 (rev 02)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:15.0 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #0 (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #1 (rev f1)
00:1c.6 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #7 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1)
00:1d.2 PCI bridge: Intel Corporation Device 9d1a (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-LP LPC Controller (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (4) I219-V (rev 21)
02:00.0 3D controller: NVIDIA Corporation GM108M [GeForce 940MX] (rev ff)
04:00.0 Network controller: Intel Corporation Wireless 8265 / 8275 (rev 78)
3e:00.0 Non-Volatile memory controller: Lenovo Device 0004

```

#### lsusb

```
Bus 002 Device 006: ID 0bda:0316 Realtek Semiconductor Corp. 
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 006: ID 138a:0097 Validity Sensors, Inc. 
Bus 001 Device 005: ID 04f2:b5ab Chicony Electronics Co., Ltd 
Bus 001 Device 004: ID 8087:0a2b Intel Corp. 
Bus 001 Device 019: ID 1199:9079 Sierra Wireless, Inc. 
Bus 001 Device 002: ID 04f2:b5ac Chicony Electronics Co., Ltd 
Bus 001 Device 007: ID 2386:310e  
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## See also

*   [Lenovo Support Page](https://pcsupport.lenovo.com/de/en/products/laptops-and-netbooks/thinkpad-t-series-laptops/thinkpad-t25-type-20k7?beta=false)