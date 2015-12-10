# Toshiba Satellite A100-386

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Contents

*   [1 ACPI and Power Saving](#ACPI_and_Power_Saving)
*   [2 Networking](#Networking)
*   [3 Wireless](#Wireless)
*   [4 Audio](#Audio)
*   [5 Graphics](#Graphics)
*   [6 Framebuffer](#Framebuffer)
*   [7 Modem](#Modem)
*   [8 Touchpad](#Touchpad)
*   [9 SD card reader](#SD_card_reader)
*   [10 FireWire](#FireWire)
*   [11 DVD burner](#DVD_burner)

## ACPI and Power Saving

Unlike older Toshiba laptops, this one has a PhoenixBIOS and will NOT work with the toshiba_acpi module nor utilities which make use of toshiba_acpi. The Omnibook project doesn't support this laptop just yet, as no documentation has been released by Toshiba. Anyway, there's a PKGBUILD for omnibook-svn in AUR. As a result, the FN hotkeys are unusable at the moment. But you can use the ACPI video module to control the brightness of the LCD screen:

```
$ modprobe video
$ cat /proc/acpi/video/GFX0/LCD/brightness #get the available brightness levels
$ echo 10 > /proc/acpi/video/GFX0/LCD/brightness # set the LCD brightness

```

The EasyGuard hard disk protection also has no Linux driver at the moment.

You can use one of powersave, powernowd, cpudyn, cpufreqd or similar utilities to control CPU frequency scaling with the speedstep_centrino module.

## Networking

Intel Corp. Ethernet Controller. Use the e100 module.

## Wireless

Intel Corporation|PRO/Wireless 3945ABG. See [Wireless network configuration#iwlegacy](/index.php/Wireless_network_configuration#iwlegacy "Wireless network configuration") for details.

## Audio

The latest alsa patch included in the ARCH kernel adds the definitions for Toshiba integrated sound cards. But I get really low volume with this one so I prefer to force the model to 3stack instead:

Add this line to /etc/modprobe.d/modprobe.conf:

```
options snd-hda-intel model=3stack

```

## Graphics

NVIDIA GeForce Go 7300\. See [NVIDIA](/index.php/NVIDIA "NVIDIA") or [nouveau](/index.php/Nouveau "Nouveau") for details.

## Framebuffer

The Video BIOS doesn't have the 1280x800 resolution although X11 can use it without problems. So, no 1280x800 framebuffer for you. Sorry !

## Modem

Working with the slmodem driver and ALSA.

## Touchpad

See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

## SD card reader

Texas Instruments Card Reader. Use the tifm_sd module. Untested.

## FireWire

Untested but should work.

## DVD burner

Works fine out-of-the-box.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Toshiba_Satellite_A100-386&oldid=400455](https://wiki.archlinux.org/index.php?title=Toshiba_Satellite_A100-386&oldid=400455)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Toshiba](/index.php/Category:Toshiba "Category:Toshiba")