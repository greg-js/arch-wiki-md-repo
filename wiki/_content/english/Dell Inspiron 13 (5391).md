This is an install and configuration guide for the Dell Inspiron 13 5391 laptop.

| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Not working | iwlwifi |
| Bluetooth | ? | ? |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | i2c_hid |
| Webcam | ? | uvcvideo |
| Keyboard backlight switch | Working | ? |
| Function/Multimedia Keys | Working | ? |

See the [Laptop/Dell](/index.php/Laptop/Dell "Laptop/Dell") chart for information on other Dell laptops.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware Details](#Hardware_Details)
*   [2 Installation](#Installation)
*   [3 Hardware](#Hardware)
    *   [3.1 Audio](#Audio)
    *   [3.2 Video](#Video)
    *   [3.3 Keyboard](#Keyboard)
    *   [3.4 Touchpad](#Touchpad)
    *   [3.5 Wireless](#Wireless)
    *   [3.6 Backlight and Volume control with the function keys](#Backlight_and_Volume_control_with_the_function_keys)
    *   [3.7 HDMI/Monitor](#HDMI/Monitor)
    *   [3.8 USB, SD card slot, HDMI, webcam](#USB,_SD_card_slot,_HDMI,_webcam)

## Hardware Details

lspci:

```
00:00.0 Host bridge: Intel Corporation Device 9b61 (rev 0c)
00:02.0 VGA compatible controller: Intel Corporation Device 9b41 (rev 02)
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 0c)
00:08.0 System peripheral: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th/8th Gen Core Processor Gaussian Mixture Model
00:12.0 Signal processing controller: Intel Corporation Device 02f9
00:13.0 Serial controller: Intel Corporation Device 02fc
00:14.0 USB controller: Intel Corporation Device 02ed
00:14.2 RAM memory: Intel Corporation Device 02ef
00:14.3 Network controller: Intel Corporation Device 02f0
00:14.5 SD Host controller: Intel Corporation Device 02f5
00:15.0 Serial bus controller [0c80]: Intel Corporation Device 02e8
00:15.1 Serial bus controller [0c80]: Intel Corporation Device 02e9
00:16.0 Communication controller: Intel Corporation Device 02e0
00:1d.0 PCI bridge: Intel Corporation Device 02b4 (rev f0)
00:1f.0 ISA bridge: Intel Corporation Device 0284
00:1f.3 Multimedia audio controller: Intel Corporation Device 02c8
00:1f.4 SMBus: Intel Corporation Device 02a3
00:1f.5 Serial bus controller [0c80]: Intel Corporation Device 02a4
01:00.0 Non-Volatile memory controller: SK hynix Device 1339

```

lsusb:

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 0bda:565a Realtek Semiconductor Corp. Integrated_Webcam_HD
Bus 001 Device 003: ID 27c6:538d Goodix FingerPrint
Bus 001 Device 005: ID 8087:0aaa Intel Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Installation

See [Installation guide](/index.php/Installation_guide "Installation guide").

## Hardware

### Audio

Get it working with the help of: [https://forum.manjaro.org/t/hardware-acceleration-cannot-init/107199/2](https://forum.manjaro.org/t/hardware-acceleration-cannot-init/107199/2)

### Video

The notebook comes with the [Intel UHD Graphics](https://en.wikipedia.org/wiki/Intel_HD_and_Iris_Graphics "wikipedia:Intel HD and Iris Graphics") GPU, which uses the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver. See: [Intel](/index.php/Intel "Intel") for details.

### Keyboard

Keyboard worked out of the box.

### Touchpad

Touchpad worked out of the box. To enable scroll and more, install [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput). With the default configuration file it will work well, but if you want to fine tune the behavior.

See: [Libinput](/index.php/Libinput "Libinput").

### Wireless

This laptop has Intel Corporation Wireless-AC 9462 wireless card, which does not work out of the box due to a bug: [https://bugs.archlinux.org/task/64703](https://bugs.archlinux.org/task/64703).

To get wifi working again until the aforementioned bug is fixed, you can use the old kernel, firmware etc. by [downgrading to the software frozen on 02.12.2019](/index.php/Arch_Linux_Archive#How_to_restore_all_packages_to_a_specific_date "Arch Linux Archive").

Use the following line in your /etc/pacman.d/mirrorlist:

```
Server = [https://archive.archlinux.org/repos/2019/12/02/$repo/os/$arch](https://archive.archlinux.org/repos/2019/12/02/$repo/os/$arch)

```

See also: [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

### Backlight and Volume control with the function keys

See [Xbindkeys#Configuration](/index.php/Xbindkeys#Configuration "Xbindkeys")

### HDMI/Monitor

### USB, SD card slot, HDMI, webcam

Not tested yet.