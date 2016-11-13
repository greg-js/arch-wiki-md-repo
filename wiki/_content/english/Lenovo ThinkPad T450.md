This article covers details pertaining to installing and configuring your Arch on Lenovo Thinkpad T450 laptop.

## Contents

*   [1 Installation](#Installation)
*   [2 Hardware](#Hardware)
    *   [2.1 Sound](#Sound)
    *   [2.2 Rebinding Forward and Back Keys](#Rebinding_Forward_and_Back_Keys)

## Installation

This laptop supports [UEFI](/index.php/UEFI "UEFI") as well as the traditional BIOS.

There are no issues with installing Arch Linux with the latest [Archiso](https://www.archlinux.org/download/).

The rest of the installation process can be followed with the [Installation guide](/index.php/Installation_guide "Installation guide").

## Hardware

All hardware works out of the box, except the following:

### Sound

The audio has a conflict between two modules. The modules inquestion are `snd_hda_intel` and `snd_hda_codec`. Disabling the intel sound module module fixes the sound issue. You can disable it by creating a blacklisting snd_hda_intel (possible snd_hda_codec instead?) file.

 `/etc/modprobe.d/alsa-base.conf`  `options snd_hda_intel index=1` 

### Rebinding Forward and Back Keys

See [T420](https://wiki.archlinux.org/index.php/Lenovo_ThinkPad_T420#Rebind_Forward_and_Back_keys)