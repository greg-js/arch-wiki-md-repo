This is an install and configuration guide for the Dell Inspiron 1525 laptop, testing with the 2010.05 installer snapshot.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Audio](#Audio)
    *   [2.2 Microphone](#Microphone)
    *   [2.3 Video](#Video)
    *   [2.4 Keyboard](#Keyboard)
    *   [2.5 Touchpad](#Touchpad)
    *   [2.6 Wireless](#Wireless)
    *   [2.7 Modem](#Modem)
    *   [2.8 USB, SD card slot, ethernet, firewire, VGA, S-video, HDMI, webcam and mediakeys](#USB,_SD_card_slot,_ethernet,_firewire,_VGA,_S-video,_HDMI,_webcam_and_mediakeys)
    *   [2.9 PCMCIA](#PCMCIA)

## Installation

When the installation media has boot, hit TAB in the first entry and add *i915.modeset=0* to the options. Then hit ENTER to install.

## Configuration

There are different many [variants](https://en.wikipedia.org/wiki/http://en.wikipedia.org/wiki/Dell_inspiron_1525#System_specifications "wikipedia:http://en.wikipedia.org/wiki/Dell inspiron 1525") of this notebook. You will notice differences in CPU and Wireless. Some models also have a webcam.

### Audio

There are two options to get audio working: [ALSA](/index.php/ALSA "ALSA") and [OSS](/index.php/OSS "OSS"). With ALSA the sound works well, both headphone jacks work and volume can be set independently. With OSS you will generally get better quality and louder sound.

### Microphone

If the built-in microphone is static, [setting the sample rate in PulseAudio](/index.php/PulseAudio/Troubleshooting#Static_noise_in_microphone_recording "PulseAudio/Troubleshooting") may solve the problem.

### Video

The notebook comes with the [Intel GMA X3100](https://en.wikipedia.org/wiki/Intel_GMA#GMA_X3100 "wikipedia:Intel GMA") GPU, which uses the *xf86-video-intel* driver. See [Intel](/index.php/Intel "Intel") for details.

Since xf86-video-intel 2.10, using KMS is [mandatory](https://www.archlinux.org/news/484/), so do not use [GRUB Frame Buffer.](/index.php/GRUB#Frame_Buffer "GRUB") Touchpad

### Keyboard

Keyboard worked out of the box.

### Touchpad

Touchpad worked out of the box. To enable scroll and more, install [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics). With the default configuration file it will work well, but if you want to fine tune the behavior, read [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

### Wireless

See [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

### Modem

You need [hsfmodem](https://aur.archlinux.org/packages/hsfmodem/) package from AUR in order to get modem working. After you install that package you need to:

1.  Run `hsfconfig` as root to build the module and initialize the modem. A reboot is required before the modem can be initialized. Run `hsfconfig` again after reboot.
2.  The modules are automatically loaded and a `/dev/modem` symlink is setup for use with the modem. Now use wvdial or other dialer programs to connect to the internet.

Dialing has not been tested, however the modem device will show in /dev.

### USB, SD card slot, ethernet, firewire, VGA, S-video, HDMI, webcam and mediakeys

All work out of the box.

### PCMCIA

Not tested.