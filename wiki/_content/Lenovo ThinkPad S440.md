# Lenovo ThinkPad S440

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This article was written to assist you with getting archlinux run on the Lenovo ThinkPad S440\. It is meant to be help you with some tricky points aside to the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide"): A guide through the whole process of installing and configuring Arch Linux; written for new or inexperienced users.

## Contents

*   [1 Prerequisites](#Prerequisites)
    *   [1.1 Creating an installation medium](#Creating_an_installation_medium)
    *   [1.2 Enable Legacy Boot](#Enable_Legacy_Boot)
*   [2 Installation](#Installation)
    *   [2.1 LAN](#LAN)
    *   [2.2 WLAN](#WLAN)
    *   [2.3 Audio](#Audio)
    *   [2.4 Video](#Video)
    *   [2.5 Touchpad](#Touchpad)
    *   [2.6 Frequency scaling](#Frequency_scaling)
    *   [2.7 Webcam](#Webcam)
    *   [2.8 Keyboard backlight](#Keyboard_backlight)
    *   [2.9 Fingerprint scanner](#Fingerprint_scanner)
    *   [2.10 Suspend](#Suspend)
    *   [2.11 Power consumption](#Power_consumption)

## Prerequisites

### Creating an installation medium

To create a bootable USB-Stick with the archlinux*.iso you downloaded, simply:

```
 dd bs=4M if=archlinux*.iso of=/dev/sdX && sync

```

which will/should behave like a regular bootable CD-Rom in addition to a capable BIOS and the <u>correct bootsequence</u>! In doubt or in case of problems see [Install from a USB flash drive](/index.php/Install_from_a_USB_flash_drive "Install from a USB flash drive") for more detailed instructions.

### Enable Legacy Boot

On boot press F12 to enter the BIOS menu and choose your USB-Stick to boot from. If you like, you can disable UEFI boot completely in the BIOS settings too.

## Installation

After that it is recommended to follow the usual installation procedure described in the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide").

### LAN

Works out of the box with module `r8169`.

If you use Lenovo's Thinkpad OneLink Dock you need [asix-ax88179-dkms](https://aur.archlinux.org/packages/asix-ax88179-dkms/)<sup><small>AUR</small></sup> for it's ThinkPad OneLink GigaLAN adapter. The module `ax88179_178a` delivered with the stock kernel doesn't work.

### WLAN

Works out of the box with module `iwlwifi`.

### Audio

Works out of the box with module `snd-hda-intel`.

### Video

The S440 comes with ati intel hybrid graphics. Currently the best implementation for `i915`/ `fglrx` hybrids is found in the [unofficial catalyst repository](/index.php/AMD_Catalyst#Installing_from_the_unofficial_repository "AMD Catalyst").

You can switch between the two drivers with on of the following commands:

```
 # intel
 aticonfig --px-igpu

```

```
 # ati
 aticonfig --px-dgpu

```

If you encounter tearing in video playback when using Intel graphics (some S440 variants come without dedicated ATI chip), [try enabling the Intel drivers' "TearFree" option](/index.php/Intel_graphics#Tear-free_video "Intel graphics").

### Touchpad

A synaptics touchpad with two-finger scrolling. Install [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) to get it running with multi-touch gestures.

### Frequency scaling

Work well with [cpupower](https://www.archlinux.org/packages/?name=cpupower) as described in [CPU Frequency Scaling](/index.php/CPU_frequency_scaling#cpupower "CPU frequency scaling"). Be aware, that the `ondemand` governer doesn't work with i7 4500M atm. I choose `powersave` as default.

### Webcam

Works out of the box with `uvcvideo`.

### Keyboard backlight

Currently the `thinkpad_acpi` module does not support to turn the keyboard backlight on. But you can turn it off with:

```
 echo 0 > /sys/devices/platform/thinkpad_acpi/leds/tpacpi::thinklight/brightness

```

### Fingerprint scanner

To get that working you need [fprintd](https://www.archlinux.org/packages/?name=fprintd) and [libfprint-vfs5011-git](https://aur.archlinux.org/packages/libfprint-vfs5011-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/libfprint-vfs5011-git)]</sup>. Follow the [Fprint](/index.php/Fprint "Fprint") guide for the rest.

### Suspend

Works flawlessly with with [pm-utils](https://www.archlinux.org/packages/?name=pm-utils) or any DE integration. If resuming from suspend works once but not a second time, try disabling Intel's Anti-Theft module in BIOS (see [this kernel bug report](https://bugzilla.kernel.org/show_bug.cgi?id=11963)).

### Power consumption

With [cpupower](https://www.archlinux.org/packages/?name=cpupower), [laptop-mode-tools](https://aur.archlinux.org/packages/laptop-mode-tools/)<sup><small>AUR</small></sup> and [acpid](https://www.archlinux.org/packages/?name=acpid) installed and graphics switched to intel gpu, I get over 9 hours battery life.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_S440&oldid=412556](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_S440&oldid=412556)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")

Hidden category:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")