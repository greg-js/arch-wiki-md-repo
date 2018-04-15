This article covers details pertaining to installing and configuring your Arch on Lenovo Thinkpad T450 laptop.

## Installation

Supports both UEFI and MBR style bios. There are no issues with installing Arch Linux with the latest that is known [Archiso](https://www.archlinux.org/download/). The installation process is the same [Installation guide](/index.php/Installation_guide "Installation guide") except, the sound.

### Sound

See [ALSA#Set the default sound card](/index.php/ALSA#Set_the_default_sound_card "ALSA") to set the default sound card to Intel PCH (speakers and headphones).

 ` /etc/modprobe.d/thinkpad-t450s.conf `  `options snd_hda_intel index=1,0` 

### Rebinding Forward and Back Keys

See [T420](/index.php/Lenovo_ThinkPad_T420#Rebind_Forward_and_Back_keys "Lenovo ThinkPad T420")