| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Working | ath10k |
| Bluetooth | Working | btusb |
| Audio | Working | snd_hda_intel |
| Touchpad | Working |  ? |
| Webcam | Working | uvcvideo |
| USB-C / Thunderbolt 3 | Working |  ? |
| Wireless switch | Working | intel_hid |
| Function/Multimedia Keys | Working |  ? |

The Dell XPS 13 Late 2016 (9360) is the fourth-generation model of the XPS 13 line. The laptop is available since October in both a standard edition with Windows installed as well as a Developer Edition with Ubuntu installed. There is no hardware difference between them. Just like the older versions ([Dell XPS 13 (9333)](/index.php/Dell_XPS_13_(9333) "Dell XPS 13 (9333)"), [Dell XPS 13 (9343)](/index.php/Dell_XPS_13_(9343) "Dell XPS 13 (9343)")), [Dell XPS 13 (9350)](/index.php/Dell_XPS_13_(9350) "Dell XPS 13 (9350)")) it is available in different hardware configurations. This fourth gen model includes Intel's Kaby Lake CPU and configurable with up to 16GB LPDDR 1866 MHz RAM and a 1TB PCI SSD. It will now also be available in Rose Gold. Prior to previous information it won't be available with LPDDR 2133 MHz RAM.

The installation process for Arch on the XPS 13 does not differ from any other PC. For installation help, please see the [Installation guide](/index.php/Installation_guide "Installation guide") and [UEFI](/index.php/UEFI "UEFI"). This page covers the current status of hardware support on Arch, as well as post-installation recommendations.

As of kernel 4.5, the Intel Kaby Lake architecture is supported.

## Contents

*   [1 Content adaptive brightness control](#Content_adaptive_brightness_control)
*   [2 NVM Express SSD](#NVM_Express_SSD)
    *   [2.1 NVME Power Saving Patch](#NVME_Power_Saving_Patch)
*   [3 Coil Whine](#Coil_Whine)
*   [4 Video](#Video)
    *   [4.1 Blank screen issue after booting](#Blank_screen_issue_after_booting)
*   [5 Wireless](#Wireless)
*   [6 Bluetooth](#Bluetooth)
*   [7 Thunderbolt 3 / USB 3.1](#Thunderbolt_3_.2F_USB_3.1)
    *   [7.1 Ethernet repeatedly disconnects/reconnects with Dell USB-C adapter (DA200)](#Ethernet_repeatedly_disconnects.2Freconnects_with_Dell_USB-C_adapter_.28DA200.29)
*   [8 SATA controller](#SATA_controller)
*   [9 Touchpad](#Touchpad)
    *   [9.1 Remove psmouse errors from dmesg](#Remove_psmouse_errors_from_dmesg)
*   [10 Touchscreen](#Touchscreen)
    *   [10.1 Gestures](#Gestures)
*   [11 Firmware Updates](#Firmware_Updates)

## Content adaptive brightness control

In the XPS 13 the display panels (both FHD and QHD+) come with adaptive brightness embedded in the panel firmware, this "content adaptive brightness control" (usually referred to as CABC or DBC) will adjust the screen brightness depending on the content displayed on the screen and will generally be found undesirable, especially for Linux users who are likely to be switching between dark and light screen content. Dell has issued a fix for this however it is only available to run in Windows and for the QHD+ model of the laptop so this precaution should be taken before installing Linux, the FHD model of the XPS 13 (9360) cannot be fixed. This is not a problem with the panel but rather a problem with the way the panels are configured for the XPS 13, as the same panel exists in the Dell's Latitude 13 7000 series (e7370) FHD model but with CABC disabled. The fix is available directly from [Dell](http://www.dell.com/support/home/de/de/debsdt1/Drivers/DriversDetails?driverId=20JWV&fileId=3574543510&osCode=WT64A&productCode=xps-13-9360-laptop&languageCode=ge&categoryId=AP).

## NVM Express SSD

### NVME Power Saving Patch

Andy Lutomirski has released version 4 of his patchset which fixes powersaving for NVME devices in linux. Currently, this patch is not merged into mainline yet. Until it lands in mainline kernel use the AUR package below. **Linux-nvme** — Mainline linux kernel patched with Andy's patch for NVME powersaving APST.

	[https://github.com/damige/linux-nvme](https://github.com/damige/linux-nvme) || [linux-nvme](https://aur.archlinux.org/packages/linux-nvme/)

## Coil Whine

Unfortunately Dell still did not fix this issue and the sound for my model was very loud. The issue seems to be connected to the graphic card. At least for me it was possible to reduce it a lot by activating frame buffer compression "enable_fbc=1" [Intel graphics#Module-based Powersaving Options](/index.php/Intel_graphics#Module-based_Powersaving_Options "Intel graphics"). The coil whine will then start again under havy graphic load, which means all the time with a 4k montior.

## Video

The video should work with the `i915` driver of the current [linux](https://www.archlinux.org/packages/?name=linux) kernel. Consult [Intel graphics](/index.php/Intel_graphics "Intel graphics") for a detailed installation and configuration guide as well as for [Troubleshooting](/index.php/Intel_graphics#Troubleshooting "Intel graphics").

### Blank screen issue after booting

If using "late start" [KMS](/index.php/KMS "KMS") (the default) and the screen goes blank when loading modules, it may help to add `i915` and `intel_agp` to the initramfs or using a special [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"). Consult [Intel graphics#Blank screen during boot, when "Loading modules"](/index.php/Intel_graphics#Blank_screen_during_boot.2C_when_.22Loading_modules.22 "Intel graphics") for more information about the kernel paramter way and have a look at [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting") for a guide on how to setup the modules for the initramfs.

## Wireless

The Killer 1535 Wirless Adapter is functional and the ath10k firmware is included in recent linux kernel versions. The connection speed reported by iw is limited to 1-6Mbits/s. However this is just the output being wrong. The real connection speed is not limited to this value.

## Bluetooth

After following the instructions given at [Bluetooth](/index.php/Bluetooth "Bluetooth") tethering of internet connections via phone works immediately.

## Thunderbolt 3 / USB 3.1

The USB-C port supports Thunderbolt 3, Displayport-over-USB-C and USB power delivery as well as USB 3.1.

### Ethernet repeatedly disconnects/reconnects with Dell USB-C adapter (DA200)

Use of a power management package (such as [TLP](/index.php/TLP "TLP")) may cause the ethernet adapter to repeatedly disconnect and reconnect. If this happens, disable/blacklist USB autosuspend for the ethernet adapter. (On my laptop, this is the device <tt>Bus 004 Device 007: ID 0bda:8153 Realtek Semiconductor Corp</tt> in the output of <tt>lsusb</tt>.)

## SATA controller

When the SATA-controller is set to `RAID On` in Bios, the hard disk (at least the SSD) is not recognized. Set to `Off` or `AHCI` (`AHCI` is recommended) before attempting to install Arch.

## Touchpad

The touchpad has no explicit buttons. The buttons are built into the pads surface. There is a small line printed on the pad separating left from right click button. The pad has a **middle button** built in! (works with libinput without any configuration): To issue a middle click, simply press on the middle area right between the virtual left and click buttons - so on the small printed separator line.

### Remove psmouse errors from dmesg

If `dmesg | grep -i psmouse` returns an error, but your touchpad still works, then it might be a good idea to disable `psmouse`. First create a config file:

```
   # nano /etc/modprobe.d/modprobe.conf

   blacklist psmouse

```

Then add this file to `/etc/mkinitcpio.conf`:

```
   ...
   FILES="/etc/modprobe.d/modprobe.conf"
   ...

```

Rebuild your initial ramdisk image (see [Mkinitcpio#Image creation and activation](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio")).

## Touchscreen

The touchscreen works without additional configuration. The bug resulting in a disabled touchscreen after resume was fixed with kernel 4.8.5.

### Gestures

Refer to [libinput#Gestures](/index.php/Libinput#Gestures "Libinput") for information about the current development state and available methods.

## Firmware Updates

Dell provides firmware updates via [fwupd](https://aur.archlinux.org/packages/fwupd/). See [Flashing_BIOS_from_Linux#fwupd](/index.php/Flashing_BIOS_from_Linux#fwupd "Flashing BIOS from Linux").