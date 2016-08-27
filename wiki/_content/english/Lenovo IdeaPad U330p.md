## Contents

*   [1 Overview](#Overview)
*   [2 Hardware](#Hardware)
*   [3 Installation](#Installation)
    *   [3.1 BIOS setup](#BIOS_setup)
*   [4 Configuration](#Configuration)
    *   [4.1 Sound card](#Sound_card)
    *   [4.2 Video driver](#Video_driver)
    *   [4.3 Touchpad](#Touchpad)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Use of headphones](#Use_of_headphones)
    *   [5.2 Network connectivity/latency](#Network_connectivity.2Flatency)
    *   [5.3 Wired networking](#Wired_networking)
    *   [5.4 VGA output](#VGA_output)

## Overview

This subnotebook exists in two configurations (see below)

There are no major issues with the first one. Everything works. There is a wifi issue with the second one, but it's reparable.

This page contains just some comments that may be useful during installation or troubleshooting.

## Hardware

The unit used for testing contained the following hardware:

*   Intel Core i5-4200U Processor

*   Intel HD Graphics 4400

*   Atheros AR9462 Wireless Network Adapter or Intel 7260

*   A thin Seagate 500GB hybrid drive (i.e. 500GB HDD + 8GB SSD) or 256GB SSD

## Installation

The best way to ensure that Arch Linux is correctly installed is to follow the [Installation guide](/index.php/Installation_guide "Installation guide") step by step.

In the second configuration your wifi won't work out of the box (connection will drop repeatedly). There is a work-around: unload iwlmvm and iwlwifi kernel modules (iwlwifi needs iwlmvm)

```
# modprobe -r iwlmvm iwlwifi

```

and load iwlwifi without 11n support. For the parameter list see

```
# modinfo -p iwlwifi

```

to load use

```
# modprobe iwlwifi 11n_disable=1

```

iwlmvm will then load automatically, if you load iwlmvm before iwlwife, it will load iwlwifi automatically with default parameters.

Check with

```
# systool -v -m iwlwifi

```

that 11n_disable is set to 1. Now you have a stable wifi. To set 11n_disable=1 permanently after the installation see [Kernel modules](/index.php/Kernel_modules "Kernel modules")

### BIOS setup

Before booting with the USB stick, enter the BIOS in order to prepare the machine for the new OS. For that purpose, press the small button on the side panel next to the HDMI port. A boot menu will appear. Select "BIOS Setup", and then:

*   In the "Security" menu, disable "Secure Boot" (although Arch Linux can be configured to work with secure boot, this will probably spare you a few issues during installation).
*   In the "Boot" menu, leave "Boot Mode" set to "UEFI", and "USB Boot" enabled.
*   In the "Exit" menu, set "OS Optimized Defaults" to "Other OS". Exit by saving changes.

## Configuration

### Sound card

Set the default sound card by creating an `alsa-base.conf` file in `/etc/modprobe.d/`:

 `/etc/modprobe.d/alsa-base.conf`  `options snd_hda_intel index=1` 

and then reboot.

Install [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) and run `alsamixer` to unmute the channels, as described [here](/index.php/Advanced_Linux_Sound_Architecture#Unmuting_the_channels "Advanced Linux Sound Architecture").

### Video driver

Use [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel). This is the correct driver for the hardware and it is being developed [with the support of Intel](https://01.org/linuxgraphics/community/xf86-video-intel).

At the time of this writing (Dec. 2013), Intel has just released [extensive information](https://01.org/linuxgraphics/documentation/2013-intel-core-processor-family) about this graphics hardware.

### Touchpad

[Install](/index.php/Install "Install") [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics).

This will make sure that the touchpad works correctly and will also provide two-finger scrolling.

## Troubleshooting

### Use of headphones

If you use headphones often and you shutdown the machine with the headphones plugged in, it may happen that in the next reboots the sound is directed to the headphones by default, even when the headphones are not plugged in.

To fix this issue:

*   Plug the headphones in and out. The sound should now be directed to the speakers.

*   Install and run [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) once (you don't have to do anything, just open it, browse through the different tabs, and close it).

*   Reboot the machine (ensuring that the headphones are not plugged in). The sound should now be directed back to the speakers by default.

### Network connectivity/latency

When using [NetworkManager](/index.php/NetworkManager "NetworkManager"), it appears that wireless networking is not as responsive as it could or should be. For example, there is a noticeable lag when trying to acess some websites that should open immediately (e.g. Google, YouTube, etc.)

On the Web, there are several reports of connectivity/latency problems with this particular hardware (Atheros AR9462). However, some testing with [Wicd](/index.php/Wicd "Wicd") seems to indicate that the network adapter is working fine.

There are some things that can be tried to alleviate this problem:

*   Disable IPv6 in NetworkManager. Go to Wi-Fi settings and turn off IPv6 for each wireless network that you connect to.

*   Create an `ath9k.conf` file to specify the option `nohwcrypt=1`:

 `/etc/modprobe.d/ath9k.conf`  `options ath9k nohwcrypt=1` 

and then reboot.

### Wired networking

This model does not have an Ethernet port, but it is possible to use a USB-to-Ethernet adapter. One such adapter is [ASUS USB Ethernet Cable](http://www.asus.com/Tablet_Mobile_Accessories/USB_Ethernet_Cable/), which works right out of the box.

### VGA output

If you need to connect to an external monitor or projector through VGA, you can use an HDMI-to-VGA adapter such as [this one](http://www.lindy-international.com/HDMI-to-VGA-Adapter.htm?websale8=ld0101.ld020102&pi=38191), which works quite well.