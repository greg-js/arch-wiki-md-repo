| Working | Broken |
| 

*   SD card
*   Graphics ([i915](/index.php/I915 "I915"))
*   [Touchscreen](/index.php/Touchscreen "Touchscreen")
*   Battery/Charging
*   Audio ([ALSA](/index.php/ALSA "ALSA"))
*   [WiFi](/index.php/WiFi "WiFi")
*   [Bluetooth](/index.php/Bluetooth "Bluetooth")
*   USB-OTG, USB gadget mode
*   Sensors
*   [Backlight](/index.php/Backlight "Backlight")
*   [Suspend](/index.php/Suspend "Suspend")
*   [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration")

 | 

*   Camera
*   GPS

 |

The [ASUS MeMO Pad 7 (ME176C)](https://www.asus.com/Tablets/ASUS_MeMO_Pad_7_ME176C/) is an x86_64-based Android tablet. With Android 5.0 (Lollipop) it was updated with [UEFI](/index.php/UEFI "UEFI") boot, which makes it possible to boot any Linux distribution on it. In general, Arch Linux works as-is, but there are additional (custom) packages available for full functionality.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Overview](#Overview)
*   [2 Installation](#Installation)
    *   [2.1 Requirements](#Requirements)
    *   [2.2 Boot loader](#Boot_loader)
    *   [2.3 Boot the live environment](#Boot_the_live_environment)
    *   [2.4 Partitioning](#Partitioning)
    *   [2.5 Additional packages](#Additional_packages)
    *   [2.6 Boot loader configuration](#Boot_loader_configuration)
*   [3 Packages](#Packages)
    *   [3.1 me176c-factory](#me176c-factory)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Swap](#Swap)
    *   [4.2 Audio](#Audio)
    *   [4.3 WiFi/Bluetooth](#WiFi/Bluetooth)
    *   [4.4 Screen rotation](#Screen_rotation)
    *   [4.5 Hall sensor](#Hall_sensor)
    *   [4.6 See also](#See_also)
*   [5 See also](#See_also_2)

## Overview

[archlinux-me176c](https://github.com/me176c-dev/archlinux-me176c) contains a few additional packages that simplify installation and provide additional functionality.

## Installation

**Warning:** This article relies on third-party scripts and modifications, and may irreparably damage your hardware or data. Proceed at your own risk.

### Requirements

*   USB-OTG hub with external power supply (or USB-OTG adapter and USB hub with external power supply?)
*   USB keyboard
*   USB flash drive
*   Consider testing Arch Linux installation using UEFI and [systemd-boot](/index.php/Systemd-boot "Systemd-boot") on a desktop PC or VM first.

### Boot loader

The tablet can boot using [UEFI](/index.php/UEFI "UEFI") from the internal storage and USB(-OTG). It does not seem to be able to boot directly from an external SD card. However, it is possible to keep only the boot partition on the internal storage and have the root partition on an external SD card for dual/multi boot.

1.  To boot from internal storage you need an UEFI boot loader. [me176c-boot](https://github.com/me176c-dev/me176c-boot#readme) is a fork of [systemd-boot](/index.php/Systemd-boot "Systemd-boot") with extra features for this tablet. See [me176c-boot - Installation](https://github.com/me176c-dev/me176c-boot#installation).
2.  There is not enough space on the [EFI system partition](/index.php/EFI_system_partition "EFI system partition") to use it as a boot partition. Follow [me176c-boot - Setting up an additional ESP partition](https://github.com/me176c-dev/me176c-boot#setting-up-an-additional-esp-partition) to set up a supplemental ESP on the APD (ASUS Product Demo) partition.

### Boot the live environment

The default Arch Linux ISO does not contain the packages from [archlinux-me176c](https://github.com/me176c-dev/archlinux-me176c). Therefore, WiFi is not working out of the box. For convenience there are custom ISO provided in the [archlinux-me176c releases](https://github.com/me176c-dev/archlinux-me176c/releases). They do not differ from the default except that they run with *linux-me176c* and have all me176c packages installed. Look for the latest "archiso" release and download it, then follow [USB flash installation media](/index.php/USB_flash_installation_media "USB flash installation media") to flash it to your USB flash drive.

Connect the USB keyboard and the USB flash drive to the USB hub, enable the external power supply and connect it to the tablet while it is powered off. Keep pressing `F2` to enter the UEFI setup. There is no need to change anything. Navigate to the `Save & Exit` tab and use `Boot Override` to boot from the USB flash drive.

Installation instructions are provided in the [Installation guide](/index.php/Installation_guide "Installation guide"). A few device-specific recommendations and instructions are listed here.

### Partitioning

**Warning:** **Do not wipe or re-partition the internal storage!** It may prevent the tablet from booting and makes it difficult to return to Android later.

The internal storage is usually available as `/dev/mmcblk2`, the external SD card as `/dev/mmcblk0`. Check carefully. The internal storage has 16 partitions.

[me176c-boot - Example: Dual/multi boot](https://github.com/me176c-dev/me176c-boot/tree/master/examples/multi-boot) provides an overview about possible partitioning for dual/multi boot setups.

At the very least, you need a single root partition, and `/boot` on the ASUS Product Demo (APD) partition. If you have not changed the APD file system to [FAT32](/index.php/FAT32 "FAT32") yet, do it first:

```
# mkfs.fat -F32 /dev/disk/by-partlabel/APD
# mount ... /mnt
# mkdir /mnt/boot
# mount /dev/disk/by-partlabel/APD /mnt/boot

```

### Additional packages

**Note:** The [package signing key](/index.php/Package_signing#Adding_unofficial_keys "Package signing") for the ME176C [unofficial user repository](/index.php/Unofficial_user_repository "Unofficial user repository") is automatically trusted for installations from the custom ISO.

After installation, but before rebooting, configure the [ME176C unofficial user repository](/index.php/Unofficial_user_repository#me176c "Unofficial user repository") and install the additional packages in the chroot:

```
# pacman -S me176c

```

Consider [removing](/index.php/Removing "Removing") [linux](https://www.archlinux.org/packages/?name=linux) as it is not needed when using *linux-me176c* and will only take up space.

[Install](/index.php/Install "Install") [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) (and eventually [dialog](https://www.archlinux.org/packages/?name=dialog) for `wifi-menu`) if you would like to connect to the Internet after installation.

[Enable](/index.php/Enable "Enable") `upi_ug31xx.service` (from [me176c-battery](https://aur.archlinux.org/packages/me176c-battery/)) if you have chosen to install it.

### Boot loader configuration

There is no need to install any boot loader when using [me176c-boot](https://github.com/me176c-dev/me176c-boot#readme). However, you need to [create a loader configuration](/index.php/Systemd-boot#Adding_loaders "Systemd-boot") for your Arch Linux installation. The configuration needs to reside on the main [EFI system partition](/index.php/EFI_system_partition "EFI system partition"). While in the chroot, mount the [ESP](/index.php/ESP "ESP") at `/mnt`:

```
# mount /dev/disk/by-partlabel/ESP /mnt

```

Then create a new loader configuration in `/mnt/loader/entries`. Make sure to reference the APD partition, correct kernel and additional initrds:

```
title    Arch Linux
volume   80868086-8086-8086-8086-000000000007
linux    /vmlinuz-linux-me176c
initrd   /acpi-me176c.img
initrd   /initramfs-linux-me176c.img
options  root=PARTUUID=... rw

```

## Packages

**Tip:** All me176c packages are available in the `me176c` package group, so you can install all of them with: `pacman -S me176c`

*   *linux-me176c* is a fork of [linux](https://www.archlinux.org/packages/?name=linux) with additional patches and battery/charging drivers ported from the stock kernel.
*   [me176c-acpi](https://aur.archlinux.org/packages/me176c-acpi/) contains a patched [ACPI DSDT](/index.php/DSDT "DSDT") that is necessary for Touchscreen, Bluetooth, Battery/Charging and other functionality. Installs additional initrd `/acpi-me176c.img`.
*   [me176c-firmware](https://aur.archlinux.org/packages/me176c-firmware/) contains additional WiFi/Bluetooth firmware from the stock ROM.
*   [me176c-factory](https://aur.archlinux.org/packages/me176c-factory/) loads the WiFi/Bluetooth MAC address from the `factory` partition and provides [udev](/index.php/Udev "Udev") rules/[systemd](/index.php/Systemd "Systemd") units to automatically apply them while booting.
*   [me176c-battery](https://aur.archlinux.org/packages/me176c-battery/) provides [systemd](/index.php/Systemd "Systemd") units for the battery daemon `upi_ug31xx` used on the stock ROM. It may be needed for the battery driver to work correctly. [Start/enable](/index.php/Start/enable "Start/enable") `upi_ug31xx.service`.
*   [thermald-me176c](https://aur.archlinux.org/packages/thermald-me176c/) provides a custom configuration for [thermald](/index.php/CPU_frequency_scaling#thermald "CPU frequency scaling") based on values from the stock ROM. [Start/enable](/index.php/Start/enable "Start/enable") `thermald-me176c.service` instead of `thermald.service`.

These packages are maintained on [GitHub](https://github.com/me176c-dev/archlinux-me176c) and are available through the [AUR](/index.php/AUR "AUR") or through the [ME176C unofficial user repository](/index.php/Unofficial_user_repository#me176c "Unofficial user repository"). Older versions are available on [GitHub Releases](https://github.com/me176c-dev/archlinux-me176c/releases).

[Microcode](/index.php/Microcode "Microcode") updates for this tablet are not included in [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode), consider installing [intel-ucode-byt-t-c0](https://aur.archlinux.org/packages/intel-ucode-byt-t-c0/) instead and [enable early microcode updates](/index.php/Microcode#Enabling_early_microcode_updates "Microcode") for `/intel-ucode-byt-t-c0.img`.

### me176c-factory

With [me176c-factory](https://aur.archlinux.org/packages/me176c-factory/) installed, the WiFi/Bluetooth MAC address is loaded from the `factory` partition during the boot process and applied to the controllers. This is necessary for Bluetooth to work, because it does not have a unique MAC address otherwise. If you would like to use [MAC address spoofing](/index.php/MAC_address_spoofing "MAC address spoofing") you may need to disable this feature by [masking](/index.php/Mask "Mask") `me176c-factory-wifiaddr@wlan0.service` and/or `me176c-factory-bdaddr@hci0.service`. The MAC addresses are loaded using `me176c-factory.service` and are available in `/run/me176c`. See [me176c-factory](https://github.com/me176c-dev/linux-me176c/tree/master/factory).

## Tips and tricks

### Swap

The tablet has only very little RAM, so you almost certainly want to set up some kind of [swap](/index.php/Swap "Swap") space. However, keep in mind SD cards are slow and flash storage in general has only a limited amount of write cycles. Using it as swap space may kill it quickly. An alternative is [ZRAM](/index.php/ZRAM "ZRAM"), which compresses parts of the RAM to provide additional space at the cost of higher CPU usage.

### Audio

**Warning:** The speaker volume can be set higher than supported by the hardware. Setting it to very high values may damage the speakers or cause distortions.

Unless you are using [PulseAudio](/index.php/PulseAudio "PulseAudio"), you need to configure a few [ALSA](/index.php/ALSA "ALSA") mixers to make audio working. This is done using `alsaucm`:

```
# alsaucm -i -c bytcr-rt5640
alsaucm>> reset
alsaucm>> set _verb HiFi
alsaucm>> set _enadev Speaker

```

Using [ALSA](/index.php/ALSA "ALSA") some audio files (especially MP3/AAC) are not played correctly when converted to `float` format instead of `s16`. This does not happen when using [PulseAudio](/index.php/PulseAudio "PulseAudio").

### WiFi/Bluetooth

WiFi and Bluetooth share the same antenna, so the chip switches between WiFi and Bluetooth when they are both active at the same time. This appears to be broken in newer firmware versions included in [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware). WiFi may stop working entirely while Bluetooth is active. In this case, the only known workaround is to manually downgrade the WiFi firmware. Download the [old version](https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/plain/brcm/brcmfmac43362-sdio.bin?id=af2a88b901afbe38220ca6a9fb120beb05237997) and place it in `/lib/firmware/brcm/brcmfmac43362-sdio.bin`.

**Note:** The next time [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) is upgraded, the old version is replaced again with the newer version. (TODO: Suggest solution)

### Screen rotation

See [Automatic Rotation](/index.php/Tablet_PC#Automatic_rotation "Tablet PC"). To rotate the [Linux console](/index.php/Linux_console "Linux console"), add the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `fbcon=rotate:<direction>`, e.g. `fbcon=rotate:1` to rotate 90° (see [fbcon.txt](https://www.kernel.org/doc/Documentation/fb/fbcon.txt)).

### Hall sensor

If you have a case that closes magnetically and automatically wakes/puts the device to sleep, it may trigger too early/often and suspend your device unexpectedly. To disable this, edit `/etc/systemd/logind.conf` with `HandleLidSwitch=ignore`.

### See also

*   [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")
*   [Tablet PC](/index.php/Tablet_PC "Tablet PC")
*   [Power management](/index.php/Power_management "Power management")

## See also

*   [XDA-Developers Forum Thread](https://forum.xda-developers.com/memo-pad-7/orig-development/linux-arch-linux-asus-memo-pad-7-me176x-t3917593)
*   [Project Overview for ASUS MeMO Pad 7 (ME176C(X))](https://github.com/me176c-dev/me176c#readme)
*   [archlinux-me176c](https://github.com/me176c-dev/archlinux-me176c) (source code for packages)
*   [me176c-boot](https://github.com/me176c-dev/me176c-boot) (documentation, examples and source code)
*   [linux-me176c](https://github.com/me176c-dev/linux-me176c) (shared code and Linux kernel source code)