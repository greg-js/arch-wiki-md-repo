| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Working | ath10k |
| Bluetooth | Working | btusb |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | hid_multitouch |
| Webcam | Working (with 1.0 firmware) ¹ | uvcvideo |
| USB-C / Thunderbolt 3 | Working |  ? |
| Wireless switch | Working | intel_hid |
| Function/Multimedia Keys | Working |  ? |
| Fingerprint sensor | Not working |  ? |

The Dell XPS 13 Early 2018 (9370) is the fifth-generation model of the XPS 13 line. The laptop was released in January 2018 in both a standard edition with Windows installed as well as a Developer Edition with Ubuntu 16.04 installed, featuring kernel 4.4 as of now. There are only minor hardware differences between them, mostly in regards to the mainboard microchip manufacturers. Just like the older versions ([9333](/index.php/Dell_XPS_13_(9333) "Dell XPS 13 (9333)"), [9343](/index.php/Dell_XPS_13_(9343) "Dell XPS 13 (9343)"), [9350](/index.php/Dell_XPS_13_(9350) "Dell XPS 13 (9350)"), and [9360](/index.php/Dell_XPS_13_(9360) "Dell XPS 13 (9360)")) it is available in different hardware configurations as well. These fifth gen models includes Intel's eighth generation Kaby Lake processors, and can be configured with up to 16GB LPDDR3 2133 MHz RAM and a 1TB PCI SSD. Unlike previous iterations, the Wi-Fi/BT module is soldered and cannot be replaced, only the Killer 1435 (QCA6174A) is available for consumers, enterprise versions with the Intel 8265 modem also exist.

The installation process for Arch on the XPS 13 does not differ from any other PC. For installation help, please see the [Installation guide](/index.php/Installation_guide "Installation guide") and [UEFI](/index.php/UEFI "UEFI"). This page covers the current status of hardware support on Arch, as well as post-installation recommendations.

¹ Some users have experienced webcam firmware issues with recent models and there are [many reports of non-functional webcams on new laptops](https://www.dell.com/community/Linux-General/Dell-xps-13-9370-Webcam-support/td-p/6032049). User reports indicate Dell support is responsive to replacing screens to install a webcam that uses linux-compatible UVC 1.0 rather than 1.5 firmware drivers.

## Contents

*   [1 Booting](#Booting)
*   [2 Content Adaptive Brightness Control](#Content_Adaptive_Brightness_Control)
*   [3 Video](#Video)
*   [4 Wifi](#Wifi)
*   [5 Bluetooth](#Bluetooth)
*   [6 Keyboard](#Keyboard)
*   [7 Power Management](#Power_Management)
*   [8 Firmware Updates](#Firmware_Updates)

## Booting

To boot from a USB device attached via the USB-C to USB-A adapter included in the box, you'll need to enable Thunderbolt boot in the BIOS (press F2 while the Dell logo is displayed). Once enabled, F12 on boot will enter the boot menu. It is also possible to use the right USB-C port directly without any BIOS adjustment.

## Content Adaptive Brightness Control

In the XPS 13 the display panels (both FHD and QHD+) come with Content Adaptive Brightness Control (usually referred to as CABC or DBC) enabled by default. While disabling required flashing the display firmware in previous generations, DBC can now be disabled in recent BIOS versions. To test if DBS is enabled, go to this [test page](http://tylerwatt12.com/dc/).

## Video

The video should work with the `i915` driver of the current [linux](https://www.archlinux.org/packages/?name=linux) kernel. Consult [Intel graphics](/index.php/Intel_graphics "Intel graphics") for a detailed installation and configuration guide as well as for [Intel graphics#Troubleshooting](/index.php/Intel_graphics#Troubleshooting "Intel graphics").

If you have the 4K (3840x2160) model, also check out [HiDPI](/index.php/HiDPI "HiDPI") for UI scaling configurations.

Note that the 'enable_psr=1' option appears not to work properly, at least on the touchscreen model.

[Some user support requests indicate that currently-shipping 9370 models may bundle webcams that use UVC 1.5 firmware rather than 1.0](https://www.dell.com/community/Linux-General/Dell-xps-13-9370-Webcam-support/td-p/6032049), which is not supported.

## Wifi

Wifi should work out of the box with the `ath10k_pci` driver in recent [linux](https://www.archlinux.org/packages/?name=linux) kernels. (In my case) the Wifi firmware sometimes crashes when waking up from suspend. (firmware version `WLAN.RM.4.4.1-00051-QCARMSWP-1`; [dmesg](https://gist.github.com/dsprenkels/eb1c7095385fe16ee9b128ab0834be21)) (In my case) the crash has not again occurred after booting `linux-4.15.7` or newer.

## Bluetooth

The Bluetooth adapter sometimes becomes unavailable after waking up from suspend and can even stay deactivated and invisible after a warm reboot.

## Keyboard

With older firmware, some keys were skipped when typing fast. The issue is fixed in system firmware 0.1.3.3.

## Power Management

If the laptop seems to have an high drain when in sleep mode, it is almost certainly because is not entering proper in deep sleep. Add `quiet mem_sleep_default=deep` to the [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

## Firmware Updates

Dell provides firmware updates via Linux Vendor Firmware Service (LVFS). Refer to [Flashing BIOS from Linux#fwupd](/index.php/Flashing_BIOS_from_Linux#fwupd "Flashing BIOS from Linux") for additional information. A package is readily available at [fwupd](https://www.archlinux.org/packages/?name=fwupd).