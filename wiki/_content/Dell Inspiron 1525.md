# Dell Inspiron 1525

This is an install and configuration guide for the Dell Inspiron 1525 laptop, testing with the 2010.05 installer snapshot.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Audio](#Audio)
    *   [2.2 Microphone](#Microphone)
    *   [2.3 Video](#Video)
    *   [2.4 Keyboard](#Keyboard)
    *   [2.5 Touchpad](#Touchpad)
    *   [2.6 Wireless](#Wireless)
    *   [2.7 Modem](#Modem)
    *   [2.8 USB, SD card slot, ethernet, firewire, VGA, S-video, HDMI, webcam and mediakeys](#USB.2C_SD_card_slot.2C_ethernet.2C_firewire.2C_VGA.2C_S-video.2C_HDMI.2C_webcam_and_mediakeys)
    *   [2.9 PCMCIA](#PCMCIA)

## Installation

When the installation media has boot, hit TAB in the first entry and add _i915.modeset=0_ to the options. Then hit ENTER to install.

## Configuration

There are different many [variants](https://en.wikipedia.org/wiki/http://en.wikipedia.org/wiki/Dell_inspiron_1525#System_specifications "wikipedia:http://en.wikipedia.org/wiki/Dell inspiron 1525") of this notebook. You will notice differences in CPU and Wireless. Some models also have a webcam.

### Audio

There are two options to get audio working: [ALSA](/index.php/ALSA "ALSA") and [OSS](/index.php/OSS "OSS"). With ALSA the sound works well, both headphone jacks work and volume can be set independently. With OSS you will generally get better quality and louder sound.

### Microphone

If the built-in microphone is static, [setting the sample rate in PulseAudio](/index.php/PulseAudio/Troubleshooting#Static_noise_in_microphone_recording "PulseAudio/Troubleshooting") may solve the problem.

### Video

The notebook comes with the [Intel GMA X3100](https://en.wikipedia.org/wiki/Intel_GMA#GMA_X3100 "wikipedia:Intel GMA") GPU, which uses the _xf86-video-intel_ driver. See [Intel](/index.php/Intel "Intel") for details.

Since xf86-video-intel 2.10, using KMS is [mandatory](https://www.archlinux.org/news/484/), so do not use [GRUB Frame Buffer.](/index.php/GRUB#Frame_Buffer "GRUB") Touchpad

### Keyboard

Keyboard worked out of the box.

### Touchpad

Touchpad worked out of the box. To enable scroll and more, install [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics). With the default configuration file it will work well, but if you want to fine tune the behavior, read [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

### Wireless

See [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

### Modem

You need [hsfmodem](https://aur.archlinux.org/packages/hsfmodem/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/hsfmodem)]</sup> package from AUR in order to get modem working. After you install that package you need to:

1.  Run `hsfconfig` as root to build the module and initialize the modem. A reboot is required before the modem can be initialized. Run `hsfconfig` again after reboot.
2.  The modules are automatically loaded and a `/dev/modem` symlink is setup for use with the modem. Now use wvdial or other dialer programs to connect to the internet.

Dialing has not been tested, however the modem device will show in /dev.

### USB, SD card slot, ethernet, firewire, VGA, S-video, HDMI, webcam and mediakeys

All work out of the box.

### PCMCIA

Not tested.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dell_Inspiron_1525&oldid=392051](https://wiki.archlinux.org/index.php?title=Dell_Inspiron_1525&oldid=392051)"