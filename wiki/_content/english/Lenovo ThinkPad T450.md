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

See [ALSA#Set the default sound card](/index.php/ALSA#Set_the_default_sound_card "ALSA") to set the default sound card to Intel PCH (speakers and headphones).

 ` /etc/modprobe.d/thinkpad-t450s.conf `  `options snd_hda_intel index=1,0` 

### Rebinding Forward and Back Keys

See [T420](https://wiki.archlinux.org/index.php/Lenovo_ThinkPad_T420#Rebind_Forward_and_Back_keys)