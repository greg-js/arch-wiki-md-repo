**Note:** This page is based on the L5H60EA#ABD version of HP Pro x2 612 G2, it should also work with the other versions.

| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Working | iwlwifi |
| LTE/HSPA+ 4G Mobile Broadband | Not tested |  ? |
| Bluetooth | Working | bluetooth |
| Audio | Working | snd_hda_intel |
| Touchscreen | Working |  ? |
| Webcam | Not working |  ? |
| microSD Card Reader | Working | rtsx_pci |
| Wireless switch | Working | intel_hid |
| Function/Multimedia Keys | Buggy |  ? |
| Power Management | Working | ... |
| Finger Print Scanner | Not tested |  ? |
| Smart Card Reader | Not tested |  ? |
| Ambient light sensor | Not tested |  ? |
| Acceleration sensor, Magnetometer, Gyro | Not tested |  ? |

This page covers the current status of hardware support on Arch, pre-installation system configuration tweaks, as well as post-installation recommendations to improve the usability of the system.

The installation process for Arch on the HP Pro x2 612 G2 does not differ from any other PC. For installation help please see the [Installation guide](/index.php/Installation_guide "Installation guide") and [UEFI](/index.php/UEFI "UEFI"). To set up a dual boot configuration with Windows, refer to [Dual boot with Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows").

As of kernel 4.3, the Intel Skylake architecture is supported.

## Contents

*   [1 Pre-Installation System Settings](#Pre-Installation_System_Settings)
*   [2 Graphics Configuration](#Graphics_Configuration)
    *   [2.1 Hardware video decoding](#Hardware_video_decoding)
        *   [2.1.1 mpv](#mpv)
*   [3 Power Management](#Power_Management)
    *   [3.1 Suspend](#Suspend)
    *   [3.2 Battery](#Battery)

## Pre-Installation System Settings

Prior to installation, access the system UEFI firmware by pressing F2 during boot.

*   Secure Boot: disable

Installation of Arch can proceed normally. Refer to the [Installation guide](/index.php/Installation_guide "Installation guide") for more info.

## Graphics Configuration

The HP Pro x2 612 G2 has Intel HD Graphics 615 integrated graphics, just install the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver.

### Hardware video decoding

Simple install [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) and use one media player which support libva.

[Source](/index.php/Intel_graphics#H.264_decoding_on_GMA_4500 "Intel graphics")

#### mpv

 `~/.config/mpv/mpv.conf`  `hwdec=vaapi` 

[Source](/index.php/Mpv#Hardware_Decoding "Mpv")

## Power Management

### Suspend

Suspend works without issues.

### Battery

Battery life can be improved by installing [powertop](https://www.archlinux.org/packages/?name=powertop) and calibrating it. See [Powertop](/index.php/Powertop "Powertop") for more info.

It's also possible to deactivate some devices and ports over the BIOS.

BIOS -> Advanced -> Build-In Device options (Example: WWAN) BIOS -> Advanced -> Port Options (Example: Smart Card)