| **Device** | **Status** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Wireless](/index.php/Wireless "Wireless") | Yes |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| Fingerprint Reader | No |

This article covers the installation and configuration of Arch Linux on a Lenovo T470 laptop.

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

## Contents

*   [1 firmware (e.g. bios and peripherals)](#firmware_.28e.g._bios_and_peripherals.29)
*   [2 kernel and hardware support](#kernel_and_hardware_support)
*   [3 lspci and lsusb](#lspci_and_lsusb)
    *   [3.1 lspci](#lspci)
    *   [3.2 lsusb](#lsusb)
*   [4 See also](#See_also)

## firmware (e.g. bios and peripherals)

As of writing, the current BIOS version is 1.29\. By visiting the downloads section (T470) an ISO can be downloaded and burned to disk which will perform the update [from Lenovo](http://pcsupport.lenovo.com/gb/en/products/laptops-and-netbooks/thinkpad-t-series-laptops/thinkpad-t470/downloads).

## kernel and hardware support

[Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration") with Kaby Lake seems to work fine via va-api.

suspend-resume results in the fan holding at 100% without ever spinning down. This is being tracked on the [kernel bugtracker](https://bugzilla.kernel.org/show_bug.cgi?id=191181), and on [reddit](https://www.reddit.com/r/thinkpad/comments/5ze76f/t470_nonstop_fan_after_resuming_from_sleep/).

138a:0097 will hopefully be supported as part of [Validity90](https://github.com/nmikhailov/Validity90).

## lspci and lsusb

On kernel '4.10.13-1-ARCH' on a *20HD* T470

### lspci

```
00:00.0 Host bridge: Intel Corporation Device 5904 (rev 02)
00:02.0 VGA compatible controller: Intel Corporation Device 5916 (rev 02)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:1c.0 PCI bridge: Intel Corporation Device 9d10 (rev f1)
00:1c.6 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #7 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1)
00:1d.2 PCI bridge: Intel Corporation Device 9d1a (rev f1)
00:1f.0 ISA bridge: Intel Corporation Device 9d58 (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Device 9d71 (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (4) I219-V (rev 21)
04:00.0 Network controller: Intel Corporation Device 24fd (rev 78)
3e:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd Device a804

```

### lsusb

```
Bus 002 Device 007: ID 0bda:0316 Realtek Semiconductor Corp. 
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 008: ID 138a:0097 Validity Sensors, Inc. 
Bus 001 Device 005: ID 5986:111c Acer, Inc 
Bus 001 Device 003: ID 8087:0a2b Intel Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## See also

*   [Lenovo Support Page](http://support.lenovo.com/us/en/products/Laptops-and-netbooks/ThinkPad-T-Series-laptops/ThinkPad-T470?beta=false)