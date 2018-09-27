This is an install and configuration guide for the Dell Inspiron 13 5368 laptop (2 in 1 Touch), testing with the 2016.10.01 version.

| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Working | iwlmvm |
| Bluetooth | Working | btusb |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | i2c_hid |
| Touchscreen | Working | usbhid |
| Webcam | Working | uvcvideo |
| Wireless switch | Working | intel_hid |
| Keyboard backlight switch | Working | ? |
| Harddisk/Battery light switch | Working | ? |
| Function/Multimedia Keys | Working | ? |

See the [Laptop/Dell](/index.php/Laptop/Dell "Laptop/Dell") chart for information on other Dell laptops.

## Contents

*   [1 Hardware Details](#Hardware_Details)
*   [2 Installation](#Installation)
*   [3 Hardware](#Hardware)
    *   [3.1 Audio](#Audio)
    *   [3.2 Video](#Video)
    *   [3.3 Keyboard](#Keyboard)
    *   [3.4 Touchpad](#Touchpad)
    *   [3.5 Touchscreen](#Touchscreen)
    *   [3.6 Wireless](#Wireless)
    *   [3.7 HDMI/Monitor](#HDMI.2FMonitor)
    *   [3.8 USB, SD card slot, HDMI, webcam](#USB.2C_SD_card_slot.2C_HDMI.2C_webcam)

## Hardware Details

lspci:

```
00:00.0 Host bridge: Intel Corporation Skylake Host Bridge/DRAM Registers (rev 08)
00:02.0 VGA compatible controller: Intel Corporation HD Graphics 520 (rev 07)
00:04.0 Signal processing controller: Intel Corporation Skylake Processor Thermal Subsystem (rev 08)
00:13.0 Non-VGA unclassified device: Intel Corporation Device 9d35 (rev 21)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:15.0 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #0 (rev 21)
00:15.1 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #1 (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:17.0 SATA controller: Intel Corporation Sunrise Point-LP SATA Controller [AHCI mode] (rev 21)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #5 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-LP LPC Controller (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
01:00.0 Network controller: Intel Corporation Wireless 3165 (rev 79)
```

lsusb:

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 2386:3111  
Bus 001 Device 002: ID 0bda:568a Realtek Semiconductor Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

## Installation

See [Installation guide](/index.php/Installation_guide "Installation guide").

## Hardware

### Audio

There are two options to get audio working: [ALSA](/index.php/ALSA "ALSA") and [PulseAudio](/index.php/PulseAudio "PulseAudio"). With ALSA the sound works well, both headphone jacks work and volume can be set independently. With Pulse Audio you will generally get better quality and louder sound.

### Video

The notebook comes with the [Intel HD Graphics 520](https://en.wikipedia.org/wiki/Intel_HD_and_Iris_Graphics "wikipedia:Intel HD and Iris Graphics") GPU, which uses the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver. See: [Intel](/index.php/Intel "Intel") for details.

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

See [xrandr](/index.php/Xrandr "Xrandr").

xrandr:

```
Screen 0: minimum 8 x 8, current 1920 x 1080, maximum 32767 x 32767
eDP1 connected primary 1920x1080+0+0 (normal left inverted right x axis y axis) 290mm x 170mm
   1920x1080     60.05*+  48.12  
   1400x1050     59.98  
   1600x900      60.00  
   1280x1024     60.02  
   1280x960      60.00  
   1368x768      60.00  
   1280x720      60.00  
   1024x768      60.00  
   1024x576      60.00  
   960x540       60.00  
   800x600       60.32    56.25  
   864x486       60.00  
   640x480       59.94  
   720x405       60.00  
   640x360       60.00  
DP1 disconnected (normal left inverted right x axis y axis)
HDMI1 disconnected (normal left inverted right x axis y axis)
HDMI2 disconnected (normal left inverted right x axis y axis)
VIRTUAL1 disconnected (normal left inverted right x axis y axis)
```

### USB, SD card slot, HDMI, webcam

All work out of the box.