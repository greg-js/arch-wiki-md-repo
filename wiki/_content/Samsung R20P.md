# Samsung R20P

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Contents

*   [1 Hardware specification](#Hardware_specification)
*   [2 Extra](#Extra)
*   [3 Installation](#Installation)
*   [4 Configuration](#Configuration)
    *   [4.1 Audio](#Audio)
        *   [4.1.1 Troubleshooting](#Troubleshooting)
    *   [4.2 Touchpad](#Touchpad)
    *   [4.3 Wireless](#Wireless)
*   [5 VGA Out](#VGA_Out)
*   [6 Troubleshooting](#Troubleshooting_2)
    *   [6.1 Yet untested](#Yet_untested)
*   [7 Resources](#Resources)
    *   [7.1 Output of _lscpi -nn_](#Output_of_lscpi_-nn)

### Hardware specification

**NP-R20Y**

*   LCD - 14.1" WXGA Glare TFT screen
*   CPU - Intel Core Duo T2330 @ 1.60Ghz
*   RAM - 2GB DDR2 (2 slots)
*   VGA - ATi Radeon Xpress 1250
*   HDD - 160GB SATA Samsung HM160HIS
*   CD/DVD - TS-L632H DL DVD+-RW SuperMulti
*   Audio - Realtek ALC262
*   Battery - 2600mAh LION / ~1.5-2h battery life

### Extra

*   Audio In / Mic In
*   3 USB 2.0 Ports
*   Sony Memory Stick Reader
*   1 VGA Out port
*   1 RJ-45
*   1 RJ-11
*   1 Express Card slot

# Installation

For installation I used both i686 and x86_64 2008.06 "Core" images. Installation of the system was very smooth, but to have a plesant experience with Arch Linux on this laptop I needed to tweak it a bit.

# Configuration

This laptop requires a bit tweaking to make it work without glitches on Arch Linux.

*   [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling")
*   [Pm-utils](/index.php/Pm-utils "Pm-utils") - Suspend / Hibernation
*   [ATI](/index.php/ATI "ATI")
*   [Laptop](/index.php/Laptop "Laptop")
*   [madwifi](/index.php/Wireless "Wireless")

## Audio

**Note:** Kernel 2.6.27 and Alsa 1.0.18 seems to be working without problems

### Troubleshooting

If you get **hda-intel: Invalid position buffer, using LPIB read method instead** message from _dmesg_ or _/var/log/everything.log_ edit your _/etc/modprobe.d/modprobe.conf_ as root and write :

```
options snd-hda-intel enable=1 index=0 position_fix=1

```

## Touchpad

See the [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") page for instructions. Currently there are some issues with the touchpad which causes enormus CPU usage, freezes and lock-ups. To fix that open, again as root, _/boot/grub/menu.lst_ and in the end of _kernel_ section write :

```
i8042.nomux=1 hpet=disable

```

## Wireless

**Note:** Kernel 2.6.27 contains an updated _ath5k_ driver, wireless works out of the box. (wlan0)

# VGA Out

Proper resolution of the secondary monitor is detected after an X server restart using open source (xf86-video-ati) driver.

# Troubleshooting

*   Suspend and Hibernation doesn't work with gnome-power-utils, but they work with [pm-utils](/index.php/Pm-utils "Pm-utils").

*   Fn keys currently do not work with _radeonhd_ driver, but they work with _fglrx_ , but not all of them.

## Yet untested

*   Modem
*   Express Card

# Resources

### Output of _lscpi -nn_

```
 00:00.0 Host bridge [0600]: ATI Technologies Inc Radeon Xpress 7930 Host Bridge [1002:7930]
 00:01.0 PCI bridge [0604]: ATI Technologies Inc RS7932 PCI Bridge [1002:7932]
 00:05.0 PCI bridge [0604]: ATI Technologies Inc Device [1002:7935]
 00:06.0 PCI bridge [0604]: ATI Technologies Inc RS7936 PCI Bridge [1002:7936]
 00:07.0 PCI bridge [0604]: ATI Technologies Inc Device [1002:7937]
 00:12.0 SATA controller [0106]: ATI Technologies Inc SB600 Non-Raid-5 SATA [1002:4380]
 00:13.0 USB Controller [0c03]: ATI Technologies Inc SB600 USB (OHCI0) [1002:4387]
 00:13.1 USB Controller [0c03]: ATI Technologies Inc SB600 USB (OHCI1) [1002:4388]
 00:13.2 USB Controller [0c03]: ATI Technologies Inc SB600 USB (OHCI2) [1002:4389]
 00:13.3 USB Controller [0c03]: ATI Technologies Inc SB600 USB (OHCI3) [1002:438a]
 00:13.4 USB Controller [0c03]: ATI Technologies Inc SB600 USB (OHCI4) [1002:438b]
 00:13.5 USB Controller [0c03]: ATI Technologies Inc SB600 USB Controller (EHCI) [1002:4386]
 00:14.0 SMBus [0c05]: ATI Technologies Inc SBx00 SMBus Controller [1002:4385] (rev 14)
 00:14.1 IDE interface [0101]: ATI Technologies Inc SB600 IDE [1002:438c]
 00:14.2 Audio device [0403]: ATI Technologies Inc SBx00 Azalia (Intel HDA) [1002:4383]
 00:14.3 ISA bridge [0601]: ATI Technologies Inc SB600 PCI to LPC Bridge [1002:438d]
 00:14.4 PCI bridge [0604]: ATI Technologies Inc SBx00 PCI to PCI Bridge [1002:4384]
 01:05.0 VGA compatible controller [0300]: ATI Technologies Inc Radeon Xpress 1250 [1002:7942]
 05:00.0 Ethernet controller [0200]: Atheros Communications Inc. AR242x 802.11abg Wireless PCI Express Adapter [168c:001c] (rev 01)
 0b:05.0 Ethernet controller [0200]: Realtek Semiconductor Co., Ltd. RTL-8139/8139C/8139C+ [10ec:8139] (rev 10)

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Samsung_R20P&oldid=309739](https://wiki.archlinux.org/index.php?title=Samsung_R20P&oldid=309739)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Samsung](/index.php/Category:Samsung "Category:Samsung")