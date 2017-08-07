This is an install and configuration guide for the Dell Inspiron 13 5378 laptop (2 in 1 Touch), testing with the 2017.08.01 version.

| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Working | iwlmvm |
| Bluetooth | Working | btusb |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | i2c_hid |
| Touchscreen | Working | usbhid |
| Webcam | Working | uvcvideo |
| Wireless switch | Working | intel_hid |
| Keyboard backlight switch | Working |  ? |
| Harddisk/Battery light switch | Working |  ? |
| Function/Multimedia Keys | Working |  ? |

See the [Laptop/Dell](/index.php/Laptop/Dell "Laptop/Dell") chart for information on other Dell laptops.

## Contents

*   [1 Installation](#Installation)
*   [2 Hardware](#Hardware)
    *   [2.1 Audio](#Audio)
    *   [2.2 Video](#Video)
    *   [2.3 Keyboard](#Keyboard)
    *   [2.4 Touchpad](#Touchpad)
    *   [2.5 Touchscreen](#Touchscreen)
    *   [2.6 Wireless](#Wireless)
    *   [2.7 HDMI/Monitor](#HDMI.2FMonitor)
    *   [2.8 USB, SD card slot, HDMI, webcam](#USB.2C_SD_card_slot.2C_HDMI.2C_webcam)

## Installation

See [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch")

## Hardware

### Audio

There are two options to get audio working: [ALSA](/index.php/ALSA "ALSA") and [PulseAudio](/index.php/PulseAudio "PulseAudio"). With ALSA the sound works well, both headphone jacks work and volume can be set independently. With Pulse Audio you will generally get better quality and louder sound.

### Video

The notebook comes with the [Intel HD Graphics 620](https://en.wikipedia.org/wiki/Intel_HD_and_Iris_Graphics "wikipedia:Intel HD and Iris Graphics") GPU, which uses the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver. See: [Intel](/index.php/Intel "Intel") for details.

### Keyboard

Keyboard worked out of the box.

### Touchpad

Touchpad worked out of the box. To enable scroll and more, install [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput). With the default configuration file it will work well, but if you want to fine tune the behavior.

See: [Libinput](/index.php/Libinput "Libinput").

### Touchscreen

Touchscreen worked out of the box. More can be done after installing [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev). Works well with the default configuration file.

### Wireless

This laptop comes Intel Corporation Wireless 3165 wireless card, which worked out of the box.

See: [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

### HDMI/Monitor

### USB, SD card slot, HDMI, webcam

All work out of the box.