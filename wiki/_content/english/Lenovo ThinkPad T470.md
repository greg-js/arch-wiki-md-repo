| **Device** | **Status** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Wireless](/index.php/Wireless "Wireless") | Yes |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| Fingerprint Reader | No |

This article covers the installation and configuration of Arch Linux on a Lenovo T470 laptop.

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

## Contents

*   [1 Firmware (e.g. bios and peripherals)](#Firmware_.28e.g._bios_and_peripherals.29)
*   [2 Kernel and hardware support](#Kernel_and_hardware_support)
    *   [2.1 Screen backlight](#Screen_backlight)
    *   [2.2 Thunderbolt 3](#Thunderbolt_3)
    *   [2.3 UEFI boot](#UEFI_boot)
*   [3 PCI and USB devices](#PCI_and_USB_devices)
    *   [3.1 T470 model 20HD](#T470_model_20HD)
        *   [3.1.1 lspci](#lspci)
        *   [3.1.2 lsusb](#lsusb)
    *   [3.2 T470 model 20JN](#T470_model_20JN)
        *   [3.2.1 lspci](#lspci_2)
        *   [3.2.2 lsusb](#lsusb_2)
*   [4 See also](#See_also)

## Firmware (e.g. bios and peripherals)

As of writing, the current BIOS version is 1.39\. By visiting the downloads section (T470) an ISO can be downloaded and burned to disk which will perform the update [from Lenovo](http://pcsupport.lenovo.com/gb/en/products/laptops-and-netbooks/thinkpad-t-series-laptops/thinkpad-t470/downloads). Or [extracted and copied on a USB Stick](http://www.thinkwiki.org/wiki/BIOS_Upgrade#Booting_from_a_USB_Flash_drive).

## Kernel and hardware support

[Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration") with Kaby Lake seems to work fine via va-api.

As noted in [Intel graphics](/index.php/Intel_graphics "Intel graphics"), the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver seems to cause more issue than the builtin *modesetting* Xorg driver. Works fine without the intel driver (on a Skylake configuration).

suspend-resume results in the fan holding at 100% without ever spinning down. This is being tracked on the [kernel bugtracker](https://bugzilla.kernel.org/show_bug.cgi?id=191181), and on [reddit](https://www.reddit.com/r/thinkpad/comments/5ze76f/t470_nonstop_fan_after_resuming_from_sleep/).

138a:0097 will hopefully be supported as part of [Validity90](https://github.com/nmikhailov/Validity90).

### Screen backlight

Without the *intel* driver ([xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel), neither *xbacklight* or *xrandr* brightness control are working. It is possible that, with the good *acpi_** kernel parameters, the backlight related keys do their job.

Other workaround exists, such as described [on this post](https://bbs.archlinux.org/viewtopic.php?pid=1449243#p1449243) or in the wiki [acpid#Enabling backlight control](/index.php/Acpid#Enabling_backlight_control "Acpid"). Using the [acpilight](https://aur.archlinux.org/packages/acpilight/) package as a *xbacklight* replacement works well. You can also check [this repository](https://lab.knightsofnii.com/kristaba/tpacpi-backlight)] as a base to add the ACPI rules to call *xbacklight* when backlight keys are pressed.

**Note:** The [acpilight](https://aur.archlinux.org/packages/acpilight/) package is known to allow controlling the ThinkPad keyboard backlight. Similar ACPI rules should allow to toggle it when the keyboard backlight key is pressed.

### Thunderbolt 3

With the latest kernel (4.12.12 as of writing), the *Alpine Ridge* thunderbolt 3 controller is recognized without any additional configuration. Using a generic thunderbolt 3 to HDMI + USB3 hub works out of the box (the HDMI output is recognized by xrandr as DP-1 output).

### UEFI boot

After configuring the BIOS setup to allow UEFI boot (either *UEFI only* or *both*), it works flawlessly.

**Note:** I was unable to boot with a GPT + BIOS configuration, and therefore switch to GPT + EFI. However, until another confirmation, it is quite probable that was caused by some bad configuration from my side.

## PCI and USB devices

### T470 model 20HD

Kernel '4.10.13-1-ARCH'

#### lspci

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

#### lsusb

```
Bus 002 Device 007: ID 0bda:0316 Realtek Semiconductor Corp. 
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 008: ID 138a:0097 Validity Sensors, Inc. 
Bus 001 Device 005: ID 5986:111c Acer, Inc 
Bus 001 Device 003: ID 8087:0a2b Intel Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

### T470 model 20JN

Quite specific model, comes with a 6th generation Intel processor (Skylake) instead of a Kaby Lake like most T470 models. Output of lspci and lsusb with kernel 4.12.12-1.

#### lspci

```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Host Bridge/DRAM Registers (rev 08)
00:02.0 VGA compatible controller: Intel Corporation HD Graphics 520 (rev 07)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #1 (rev f1)
00:1c.6 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #7 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1)
00:1d.2 PCI bridge: Intel Corporation Device 9d1a (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-LP LPC Controller (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection I219-LM (rev 21)
04:00.0 Network controller: Intel Corporation Wireless 8260 (rev 3a)
05:00.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
06:00.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
06:01.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
06:02.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
3d:00.0 USB controller: Intel Corporation Device 15c1 (rev 01)

```

#### lsusb

```
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 002: ID 0bda:0316 Realtek Semiconductor Corp. 
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 8087:0a2b Intel Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## See also

*   [Lenovo Support Page](http://support.lenovo.com/us/en/products/Laptops-and-netbooks/ThinkPad-T-Series-laptops/ThinkPad-T470?beta=false)