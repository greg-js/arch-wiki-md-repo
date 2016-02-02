# Lenovo ThinkPad X220

## Contents

*   [1 Setup](#Setup)
    *   [1.1 Battery](#Battery)
    *   [1.2 Fingerprint reader](#Fingerprint_reader)
    *   [1.3 Graphics](#Graphics)
    *   [1.4 Trackpoint and Clickpad](#Trackpoint_and_Clickpad)
*   [2 Issues](#Issues)
    *   [2.1 Boot fails](#Boot_fails)
    *   [2.2 Reboot loop after resume from suspend](#Reboot_loop_after_resume_from_suspend)
    *   [2.3 Microphone](#Microphone)
    *   [2.4 Backlight](#Backlight)
*   [3 See also](#See_also)

## Setup

### Battery

Battery functions like charging thresholds can be controlled using the script [tpacpi-bat](https://aur.archlinux.org/packages/tpacpi-bat/)<sup><small>AUR</small></sup> together with the kernel module [acpi_call-git](https://aur.archlinux.org/packages/acpi_call-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/acpi_call-git)]</sup>. The [TLP](/index.php/TLP "TLP") power saving tool supports using acpi_call as backend for setting the thresholds as well.

### Fingerprint reader

The Upek fingerprint reader is supported by [Fingerprint-gui](/index.php/Fingerprint-gui "Fingerprint-gui").

### Graphics

The graphics driver is provided by the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package from the [Official repositories](/index.php/Official_repositories "Official repositories").

### Trackpoint and Clickpad

Though this model does have physical Trackpoint buttons, the middle-button-scroll does not work by default. In order to make it work, you need to install the [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) package from the [Official repositories](/index.php/Official_repositories "Official repositories").

As the Clickpad is buttonless, middle- and right-click support can be enabled by following the instructions [on the Synaptics page](/index.php/Synaptics#Buttonless_touchpads_.28aka_ClickPads.29 "Synaptics").

Trackpoint properties like speed and sensitivity can be configured using either the sysfs or [udev rules](/index.php/Udev_rules "Udev rules").

To set the speed and sensitivity temporarily, run as root:

```
# echo 120 > /sys/devices/platform/i8042/serio1/speed
# echo 200 > /sys/devices/platform/i8042/serio1/sensitivity

```

The following udev rule makes these changes permanent:

 `/etc/udev/rules.d/82-trackpoint.rules` 

```
# Set the trackpoint speed and sensitivity
SUBSYSTEM=="serio", DRIVERS=="psmouse", ATTR{sensitivity}="200", ATTR{speed}="120"
```

Alternatively an udev add-rule can be used, if the changes are not applied correctly. This can happen if the trackpoint device was not instantiated yet. This solution was posted here: [thinkpad-forum.de](http://thinkpad-forum.de/threads/160979-gel%C3%B6st-Trackpoint-Sensitivit%C3%A4t-Geschwindigkeit-ArchLinux?p=1621976&viewfull=1#post1621976)

 `/etc/udev/rules.d/82-trackpoint.rules` 

```
# Set the trackpoint speed and sensitivity
ACTION=="add",SUBSYSTEM=="input",ATTR{name}=="TPPS/2 IBM TrackPoint",ATTR{device/sensitivity}="240",ATTR{device/speed}="200"
```

## Issues

### Boot fails

The laptop can not boot from a GPT disk in legacy BIOS mode, it is necessary to either switch to UEFI booting or create a MBR Partition Table.

### Reboot loop after resume from suspend

This can be caused by the EFI storage getting too full. Run the following commands as root to free up some space.

```
 # First clear the pstore
 mkdir -p /dev/pstore
 mount -t pstore pstore /dev/pstore
 ls /dev/pstore # <- Nothing important should be here, but check first anyway
 rm /dev/pstore/*

```

```
 # Next some EFI variables. These are used/created by pstore, but I've had them even though 
 #I deleted the pstore data using the above commands. YMMV.
 rm /sys/firmware/efi/efivars/dump-type0-*

```

This information was taken from [the Lenovo forums](http://forums.lenovo.com/t5/X-Series-ThinkPad-Laptops/x220-does-not-resume-from-sleep/m-p/1083233/highlight/false#M48825)

### Microphone

The x220 internal microphone has been the source of many complaints across platforms. Specifically, it can generate a lot of static or hissing on top of any recorded audio. The workaround is to mute the right mic input channel (in audio control programs that allow independent channel setting) or to drag the balance slider in a GUI for the internal mic level fully to the left.

Note also that the audio jack is a combination headset/mic jack and will work with modern smartphone headsets with inline microphones, as an alternative.

### Backlight

Since `linux 3.16`, some backlight-related kernel parameter defaults have been changed, causing the hardware brightness up/down keys to no longer function automatically. This can be worked around by setting `acpi_osi`, e.g.

```
 acpi_osi="!Windows 2012"

```

in the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). More details can be found on [the Backlight page](/index.php/Backlight#Kernel_command-line_options "Backlight").

## See also

*   Arch user blogs about the X220
    *   [Thinkpad X220 model 4287CTO](http://natalian.org/archives/2011/11/10/Thinkpad_X220/) using a msata SSD for 64 bit Archlinux
    *   [X220 i5](http://blog.jamiek.it/2011/10/arch-linux-on-thinkpad-x220.html)
*   [Thinkwiki X220 reference](http://www.thinkwiki.org/wiki/Category:X220)
*   ["Arch By Hand" UEFI GPT SSD LUKS Install Script](https://bbs.archlinux.org/viewtopic.php?id=129885), built on an x220 tablet with an SSD.
*   [Power saving options for the X220 - Notebook Review Forum](http://forum.notebookreview.com/lenovo-ibm/575569-linux-x220-29.html#post8075286)
*   [thinkpad-scripts](https://aur.archlinux.org/packages/thinkpad-scripts/)<sup><small>AUR</small></sup> for ThinkPad X220 Tablet rotation, docking, etc scripts

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_X220&oldid=411999](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_X220&oldid=411999)"