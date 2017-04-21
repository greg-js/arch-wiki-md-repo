| **Device** | **Status** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Wireless](/index.php/Wireless "Wireless") | Yes |
| Mobile Broadband | Yes |
| [ALSA](/index.php/ALSA "ALSA") | Yes |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| Smartcard Reader | Yes |

This article covers the installation and configuration of Arch Linux on a Lenovo T470s laptop.

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

## Contents

*   [1 firmware (e.g. bios and peripherals)](#firmware_.28e.g._bios_and_peripherals.29)
*   [2 kernel and hardware support](#kernel_and_hardware_support)
*   [3 mobile broadband](#mobile_broadband)
*   [4 lspci and lsusb](#lspci_and_lsusb)
    *   [4.1 lspci](#lspci)
    *   [4.2 lsusb](#lsusb)
*   [5 Configuration](#Configuration)
    *   [5.1 Smartcard Reader](#Smartcard_Reader)
*   [6 See also](#See_also)

## firmware (e.g. bios and peripherals)

As of writing, the current bios version is 1.0.7\. By visiting the downloads section (for the type HG/HF T470s) an iso can be downloaded and burned to disk which will perform the update [[1]](http://pcsupport.lenovo.com/us/en/products/laptops-and-netbooks/thinkpad-t-series-laptops/thinkpad-t470s/downloads)

This laptop is unique in that it retains the thinkpad dock connection as well as provides docking ability over USB-C. We have tested with the [Thinkpad Ultra Dock](http://www.thinkwiki.org/wiki/ThinkPad_Ultra_Dock) and are able to utilize multiple HiDPI monitors via individual connections (e.g. no display port chaining). There are published [firmware updates](https://support.lenovo.com/us/en/solutions/pd014572) for the dock that require windows to install. DisplayPort chaining works via USB-C to DisplayPort adapter.

## kernel and hardware support

Installation with modern media puts you on Kernel 4.10.10-1, however [this note](/index.php/Dell_XPS_13_(9360)#NVME_Power_Saving_Patch "Dell XPS 13 (9360)") made [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/) seem essential.

As advised in [Intel graphics#Enable early KMS](/index.php/Intel_graphics#Enable_early_KMS "Intel graphics") and [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") you can add i915 to your modules.

[Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration") with Kaby Lake seems to work fine via va-api.

## mobile broadband

The mobile broadband card is a [Sierra EM7455](https://www.sierrawireless.com/products-and-solutions/embedded-solutions/networking-modules/), which can be seen below in the lsusb. We have confirmed working with with [Google's Project Fi](https://fi.google.com).

## lspci and lsusb

On kernel '4.11.0-rc6-mainline' via [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/) on a *20HG* T470s

### lspci

```
00:00.0 Host bridge: Intel Corporation Device 5904 (rev 02)
00:02.0 VGA compatible controller: Intel Corporation Device 5916 (rev 02)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:16.3 Serial controller: Intel Corporation Device 9d3d (rev 21)
00:1c.0 PCI bridge: Intel Corporation Device 9d10 (rev f1)
00:1c.2 PCI bridge: Intel Corporation Device 9d12 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Device 9d4e (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Device 9d71 (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (4) I219-LM (rev 21)
3a:00.0 Network controller: Intel Corporation Device 24fd (rev 78)
3c:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd Device a804

```

### lsusb

```
Bus 002 Device 003: ID 0bda:0316 Realtek Semiconductor Corp. 
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 006: ID 138a:0097 Validity Sensors, Inc. 
Bus 001 Device 005: ID 5986:111c Acer, Inc 
Bus 001 Device 008: ID 1199:9079 Sierra Wireless, Inc. 
Bus 001 Device 002: ID 058f:9540 Alcor Micro Corp. AU9540 Smartcard Reader
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Configuration

### Smartcard Reader

```
Bus 001 Device 002: ID 058f:9540 Alcor Micro Corp. AU9540 Smartcard Reader

```

## See also

*   [Lenovo Support Page](http://support.lenovo.com/us/en/products/Laptops-and-netbooks/ThinkPad-T-Series-laptops/ThinkPad-T470s?beta=false)