## Contents

*   [1 Overview](#Overview)
*   [2 Hardware](#Hardware)
*   [3 Firmware](#Firmware)
*   [4 Installation](#Installation)
    *   [4.1 UEFI](#UEFI)
*   [5 WiFi](#WiFi)
*   [6 Touchpad](#Touchpad)
*   [7 Sound](#Sound)
*   [8 Graphics](#Graphics)

## Overview

The Lenovo IdeaPad S205 has some issues with the Bootloader and WiFi.

## Hardware

The unit used for testing contained the following hardware:

*   Processor: AMD E-450 APU (integrated Mobility Radeon HD6320)

*   WiFi: Ralink RT3090

## Firmware

The IdeaPad uses a system firmware based on the SecureCore Tiano Platform. It supports UEFI and Legacy booting, but you can't manually switch between them; which one is used depends whether the disk is partitioned as GPT or MBR. It doesn't have secure boot.

The firmware has many bugs. If anything related to it doesn't work, try loading setup defaults.

## Installation

Follow the [Installation guide](/index.php/Installation_guide "Installation guide") until bootloader installation.

You can not use the GUID Partition Table and still boot using legacy BIOS. If your desired partition layout doesn't work for MBR you must use UEFI.

### UEFI

While installing the bootloader, you might get the error

```
Failed to create EFI Boot variable entry: No space left on device

```

The firmware wants the `.efi`-file to be the UEFI default loader, specifically `<ESP>/EFI/boot/bootx64.efi` The firmware does not seem to be able to boot any other file, thus giving you the above error message. The trick is to just copy your bootloader, (`grubx64.efi` `systemd-bootx64.efi`, etc) to `<ESP>/EFI/boot/bootx64.efi` and reboot into your system.

## WiFi

Drivers work out of the box.

If you're using UEFI, your device might show up as hard blocked. This is due to a bug in the firmware. You can fix it by doing the following things:

1.  Go into system firmware settings and reload factory defaults
2.  If WiFi still doesn't work, change the boot order so that it boots from PXE (PCI LAN) before booting from Hard Drive.

## Touchpad

Works by installing the [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) package.

## Sound

Detected by ALSA automatically.

## Graphics

The open source [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) driver works fine and is recommended.

You can also install the proprietary [Catalyst](/index.php/Catalyst "Catalyst") driver, but it causes glitches when waking up from hibernation. Also you may run into errors when using the HDMI output on some Monitors.