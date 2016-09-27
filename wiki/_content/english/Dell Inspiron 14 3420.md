This is an install and configuration guide for the Dell Inspiron 3420 laptop, testing with the 2016.09.03 version.

See the [Laptop/Dell](/index.php/Laptop/Dell "Laptop/Dell") chart for information on other Dell laptops.

## Contents

*   [1 Hardware Details](#Hardware_Details)
*   [2 Installation](#Installation)
*   [3 Hardware](#Hardware)
    *   [3.1 Audio](#Audio)
    *   [3.2 Video](#Video)
    *   [3.3 Keyboard](#Keyboard)
    *   [3.4 Touchpad](#Touchpad)
    *   [3.5 Wireless](#Wireless)
        *   [3.5.1 Toggle between HDMI/Monitor](#Toggle_between_HDMI.2FMonitor)
    *   [3.6 USB, SD card slot, ethernet, VGA, HDMI, webcam](#USB.2C_SD_card_slot.2C_ethernet.2C_VGA.2C_HDMI.2C_webcam)

## Hardware Details

lspci output:

```
00:00.0 Host bridge: Intel Corporation 3rd Gen Core processor DRAM Controller (rev 09)
00:02.0 VGA compatible controller: Intel Corporation 3rd Gen Core processor Graphics Controller (rev 09)
00:16.0 Communication controller: Intel Corporation 7 Series/C210 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #2 (rev 04)
00:1b.0 Audio device: Intel Corporation 7 Series/C210 Series Chipset Family High Definition Audio Controller (rev 04)
00:1c.0 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 1 (rev c4)
00:1c.3 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 4 (rev c4)
00:1c.5 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 6 (rev c4)
00:1d.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #1 (rev 04)
00:1f.0 ISA bridge: Intel Corporation HM75 Express Chipset LPC Controller (rev 04)
00:1f.2 SATA controller: Intel Corporation 7 Series Chipset Family 6-port SATA Controller [AHCI mode] (rev 04)
00:1f.3 SMBus: Intel Corporation 7 Series/C210 Series Chipset Family SMBus Controller (rev 04)
07:00.0 Network controller: Broadcom Corporation BCM43142 802.11b/g/n (rev 01)
09:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8101/2/6E PCI Express Fast/Gigabit Ethernet controller (rev 05)
```

lsusb:

```
Bus 002 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 004: ID 0c45:6473 Microdia 
Bus 001 Device 003: ID 0a5c:21d7 Broadcom Corp. BCM43142 Bluetooth 4.0
Bus 001 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

## Installation

See [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch")

## Hardware

### Audio

There are two options to get audio working: [ALSA](/index.php/ALSA "ALSA") and [PulseAudio](/index.php/PulseAudio "PulseAudio"). With ALSA the sound works well, both headphone jacks work and volume can be set independently. With Pulse Audio you will generally get better quality and louder sound.

### Video

The notebook comes with the [Intel HD 4000](https://en.wikipedia.org/wiki/Intel_HD_and_Iris_Graphics "wikipedia:Intel HD and Iris Graphics") GPU, which uses the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver. See: [Intel](/index.php/Intel "Intel") for details.

### Keyboard

Keyboard worked out of the box.

### Touchpad

Touchpad worked out of the box. To enable scroll and more, install [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics). With the default configuration file it will work well, but if you want to fine tune the behavior.

See: [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

### Wireless

This laptop comes Broadcom Corporation BCM43142 wireless card, which requires [broadcom-wl-dkms](https://aur.archlinux.org/packages/broadcom-wl-dkms/)

See: [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

#### Toggle between HDMI/Monitor

See [xrandr](/index.php/Xrandr "Xrandr").

### USB, SD card slot, ethernet, VGA, HDMI, webcam

All work out of the box.