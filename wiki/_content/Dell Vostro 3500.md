# Dell Vostro 3500

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:Dell Vostro 3500#](https://wiki.archlinux.org/index.php/Talk:Dell_Vostro_3500))

This page deals with setting up Arch Linux on the Dell Vostro 3500 laptop.

## Contents

*   [1 Installation notes](#Installation_notes)
*   [2 CPU](#CPU)
    *   [2.1 Fan Control](#Fan_Control)
*   [3 Network](#Network)
    *   [3.1 Ethernet](#Ethernet)
    *   [3.2 Wireless](#Wireless)
*   [4 Video](#Video)
    *   [4.1 Intel card](#Intel_card)
    *   [4.2 Nvidia card](#Nvidia_card)

## Installation notes

Since kernel version 3.0 the 'bcmsmac' module fully supports this laptop's wireless card. However you will need to blacklist 'bcma' module at boot up in order to make it work at installation time. Add this to the grub line at install media boot:

```
modprobe.blacklist=bcma

```

Then install following the normal procedure

## CPU

This laptop has several CPU configurations and that will depend on the purchase. The one we are documenting has a Core i5-460M CPU.

```
$ uname -p
Intel(R) Core(TM) i5 CPU M 460 @ 2.53GHz

```

This CPU is capable of [frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling").

### Fan Control

**Warning:** This laptop's BIOS manages the fans with 3 different speeds, the i8k module only manages the first two, use it only on well cooled environments or when the laptop is properly docked. Be careful about fan control. Incorrect setting of fan speeds can lead to irreparable CPU break

This laptop can use the i8k kernel module to control fan, but will need some adjustments and tweaks.

First of all, this laptop only has one fan and by default it is controlled by the BIOS. This setting is not bad but the only thing BIOS does is to turn on the fan at maximum speed, that can be unnecessary and annoying in loudness.

Install the [i8kutils](https://aur.archlinux.org/packages/i8kutils/)<sup><small>AUR</small></sup> package from the [official repositories](/index.php/Official_repositories "Official repositories") and [i8kmonitor](https://aur.archlinux.org/packages/i8kmonitor/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/i8kmonitor)]</sup> from the [AUR](/index.php/AUR "AUR").

You need to load the i8k module

```
# modprobe i8k

```

To make this permanent. Add it to the `MODULES` array in [rc.conf](/index.php/Rc.conf "Rc.conf").

This will enable the utilities to control the fan through 'i8kfan' program. You can check the current state of the fan by running:

```
$ i8kfan
-1 1

```

The first number is the first fan (unused because this laptop only has one fan). The second show the fan speed in two preset speeds: '1' and '2'. Also the i8kutils package provides a daemon to control the fans automatically based on CPU temperature.

**Warning:** Again, fan control can be dangerous if done wrong.

First, monitor the temperature along the way. If something goes wrong and core temperature starts rising run:

```
$ i8kfan 2 2

```

That will turn the fan to the maximum, then wait for the laptop to cool off. To monitor the temperature install [lm_sensors](/index.php/Lm_sensors "Lm sensors") then open a terminal and run

```
$ watch sensors

```

This will report the temperature every 2 seconds.

**Tip:** you can have a better reading by using the _coretemp_ kernel module

Check the **i8kmon** and **i8kctl** manpages on how to configure the fan configuration. here are some sane values for `/etc/i8kutils/i8kmon.conf`

```
# Temperature thresholds: {fan_speeds low_ac high_ac low_batt high_batt}
set config(0)	{{- 0}  -1  40  -1  45}
set config(1)	{{- 1}  30  55  35  60}
set config(2)	{{- 2}  45  80  50  80}
set config(3)	{{- 2}  70 128  70 128}

```

## Network

### Ethernet

Works out of the box. Just set up `dhcpd` daemon, plug and go.

### Wireless

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Dell Vostro 3500#](https://wiki.archlinux.org/index.php/Talk:Dell_Vostro_3500))

```
$ lspci -d 14e4:4727
12:00.0 Network controller: Broadcom Corporation BCM4313 802.11b/g/n Wireless LAN Controller (rev 01)

```

You will need the [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/)<sup><small>AUR</small></sup> proprietary driver for it to work properly. Current new kernels support basic functionality but freezes the system when hot-plugging the device and causes hibernation/suspend issues.

A dirty way to make the wireless work is described in what follows.

First, compile the the [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/)<sup><small>AUR</small></sup> driver from AUR, using the instructions in [AUR#Installing packages](/index.php/AUR#Installing_packages "AUR"), in order to obtain the wl module.

Second, add `blacklist bcma` to `/etc/modprobe.d/modprobe.conf` and restart the computer. Finally, do

```
# rmmod wl
# rmmod brcmsmac
# rmmod brcmutil
# modprobe wl

```

Now the wifi LED is supposed to turn on, and it should to work, as one can check using

```
$ iwlist eth1 scan

```

from the [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools) package.

## Video

**Note:** Configuration may vary depending on the purchase, your laptop may not have a dedicated graphics card at all

This laptop comes with Optimus switchable graphics configuration. This is a muxless hybrid-graphics configuration without any BIOS setting to turn it off. That said, the main Xorg server will be running on the integrated card. To be able to use it, you will need [bumblebee](/index.php/Bumblebee "Bumblebee") or [ironhide](/index.php?title=Ironhide&action=edit&redlink=1 "Ironhide (page does not exist)") workarounds.

### Intel card

### Nvidia card

Works well under [bumblebee](/index.php/Bumblebee "Bumblebee") with 3D acceleration on both [NVIDIA](/index.php/NVIDIA "NVIDIA") and [nouveau](/index.php/Nouveau "Nouveau") drivers.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dell_Vostro_3500&oldid=400579](https://wiki.archlinux.org/index.php?title=Dell_Vostro_3500&oldid=400579)"