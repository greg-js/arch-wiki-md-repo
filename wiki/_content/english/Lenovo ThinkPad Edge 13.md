How to setup archlinux on Lenovo ThinkPad Edge 13\. This guide has been written aside the ThinkPad Edge AMD version with ATI-graphics.

This article was written to assist you with getting archlinux run on the Lenovo ThinkPad Edge 13.

## Contents

*   [1 Prerequisits](#Prerequisits)
    *   [1.1 BIOS-Update:](#BIOS-Update:)
    *   [1.2 Creating an installation medium](#Creating_an_installation_medium)
*   [2 Installation](#Installation)
    *   [2.1 WLAN deauthentication issues](#WLAN_deauthentication_issues)
    *   [2.2 Audio](#Audio)
    *   [2.3 Video](#Video)
    *   [2.4 Touchpad](#Touchpad)
    *   [2.5 Frequency scaling](#Frequency_scaling)
    *   [2.6 Fan control](#Fan_control)
    *   [2.7 Webcam](#Webcam)
    *   [2.8 Suspend](#Suspend)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 High power consumption](#High_power_consumption)

## Prerequisits

First and important to do is an BIOS-Update (As of 2010/08/20 to Version 1.19.)

This was done, by using grub4dos, one can get [here](http://grub4dos.sourceforge.net/wiki/). Because a simple dd didn't create a bootable USB-Stick for me.

### BIOS-Update:

Download [grub4dos](http://download.gna.org/grub4dos/).

Unpack it on another *nix-box and run:

```
 sudo ./bootlace.com /dev/sdX

```

with /dev/sdX being your USB-Stick (as the Thinkpad Edge 13 has no CDROM-Drive) in the directory, where you unpacked your files.

Afterwards copy grldr and menu.lst to the device:

```
 cp grldr /media/USBSTICK
 cp menu.lst /media/USBSTICK

```

Download the BIOS update from the BIOS section on [this support site](http://www-307.ibm.com/pc/support/site.wss/MIGR-74581.html). Pick the one that matches your current BIOS Id. Copy the iso-file to the / directory of the USB-Stick!

Finally you have to add the following code to the menu.lst on your pendrive to make the USB-Stick boot the PC DOS program made by lenovo:

```
 title Thinkpad-Edge-BIOS-UPDATE
 find --set-root /6yuj06uc.iso
 map /6yuj06uc.iso (0xff) || map --mem /6yuj06uc.iso (0xff)
 map --hook
 chainloader (0xff)
 boot

```

Inserting such a prepared USB-Stick into your Thinkpad Edge, and things should be self-explanatory after that.

### Creating an installation medium

To create a bootable USB-Stick with the archlinux*.iso you downloaded, simply:

```
 dd bs=8M if=archlinux*.iso of=/dev/sdX

```

which will/should behave like a regular bootable CD-Rom in addition to a capable BIOS and the <u>correct bootsequence</u>! In doubt or in case of problems see [Install from a USB flash drive](/index.php/Install_from_a_USB_flash_drive "Install from a USB flash drive") for more detailed instructions.

## Installation

### WLAN deauthentication issues

If you are using the rtl8192ce module, you may experience some intermittent deauthentication issues with newer kernels (tested on 3.4.4-2-ARCH). The reason is because the BIOS is turning off the wireless card when the BIOS deems it to be "inactive." This is the case if `dmesg` reports

```
[  285.140301] wlan0: deauthenticating from MAC by local choice (reason=3)

```

A simple solution to this problem is to enter the BIOS setup and disable PCI Express power management.

### Audio

To get jack sensing to work add:

```
 options snd-hda-intel model="olpc-xo-1_5"

```

to /etc/modprobe.d/modprobe.conf.

### Video

If you have the AMD-AMD model you can use the free ati drivers.

```
 pacman -S xorg-server xf86-video-ati

```

These drivers give enough horsepower for compiz and video playback.

### Touchpad

A synaptics touchpad with two-finger scrolling.

```
 pacman -S xf86-input-synaptics

```

### Frequency scaling

The Turion work well with powernow-k8\. Please refer to the wiki for more information on cpufrequtils. Dont forget to add powernow-k8 to your modules array.

### Fan control

Add the follwing line to your /etc/modprobe.d/modprobe.conf

```
 options thinkpad_acpi fan_control=1

```

Then you can manually set your fanspeed with:

```
 echo level 7 > /proc/acpi/ibm/fan
 cat /proc/acpi/ibm/fan # for more commands.
 # Other files will report their status and commands when read too.

```

### Webcam

Works out of the box. Test with

```
 mplayer tv:// -tv driver=v4l2

```

If you use skype and the video is way to dark, skype forgot to enable automatic exposure control. Install v4l2 control and set it yourself. You need to to do it everytime you use skype.

```
 pacman -S v4l2-utils
 v4l2-utils -c exposure_auto_priority 1

```

Your video should gradually begin to brighten up. More options:

```
 v4l2-utils -l

```

### Suspend

First, you might need to add the following to your kernel commandline if suspend does not work. Newer models do not require the following hacks, so make sure that neither suspend nor wifi works.

```
 kernel root= ... acpi_osi=linux noapic

```

Second, your wifi card will delay resume by roughly 2 minutes. That means that your laptop is not frozen but still resuming. Wifi wont want to work, too. This can be worked around by removing the wifi modules before suspend. You can do this automatically if you use pm-utils. Please refer for more information to the pm-utils wiki article. Below follows my /etc/pm/sleep.d/100wifiworkaround.sh script for automation

```
 #!/bin/bash
 #
 case $1 in
   hibernate)
     ifconfig wlan0 down
     rmmod rtl8192ce
     rmmod r8169
     ;;
   thaw)
     modprobe rtl8192ce # Pulls r8169 in
     ;;
   sleep)
     ifconfig wlan0 down
     rmmod rtl8192ce
     rmmod r8169
     ;;
   resume)
     modprobe rtl8192ce
     ;;
   *)
     echo "I dont do that. Read me first please."
     ;;
 esac

```

## Troubleshooting

### High power consumption

In some cases you may experience high power consumption despite of all BIOS powersaving functions turned on.

This is because the BIOS settings do not really disable the dedicated video card, they just force the notebook to use the integrated graphics.

The solution is simple: enable video card switching and use system means (vgaswitcheroo?) to disable dedicated graphics.