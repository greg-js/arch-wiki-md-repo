## Contents

*   [1 System Specification](#System_Specification)
*   [2 Wireless](#Wireless)
    *   [2.1 Free kernel driver for the Broadcom BCM4113 chipset](#Free_kernel_driver_for_the_Broadcom_BCM4113_chipset)
    *   [2.2 Non-free alternative driver for the Broadcom BCM4113 chipset](#Non-free_alternative_driver_for_the_Broadcom_BCM4113_chipset)
    *   [2.3 Free kernel driver for the Atheros AR9285 802.11b/g chipset](#Free_kernel_driver_for_the_Atheros_AR9285_802.11b.2Fg_chipset)
*   [3 Graphics](#Graphics)
*   [4 Input](#Input)
    *   [4.1 Function keys](#Function_keys)

## System Specification

*   CPU: Intel Atom N450 (1.66 GHz, 512 MB L2 cache)
*   Memory: 1 GB DDR2 SDRAM - can be expanded to a maximum of 2GB (one RAM slot)
*   WiFi: Broadcom BCM4113
*   Hard-Drive: 250 GB 2,5" SATA, 5400 RPM
*   Optical Drive: None
*   Integrated Graphics: Intel GMA 3150
*   Sound: Intel HDA: Realtek ALC272
*   Screen: 10.1" LCD 1024x600 (WSVGA)
*   5 in 1 Card Reader
*   Webcam: Lenovo Easycam

**Note:** Some newer models have an Intel Atom N455 (same spec as 450) and 1GB of DDR3 memory.

## Wireless

This laptop uses a Broadcom BCM4113 chipset for wireless networking. Some revisions have an Atheros AR9285 802.11b/g chipset.

### Free kernel driver for the Broadcom BCM4113 chipset

As of kernel version 2.6.37, there is now a Free driver in the kernel: [brcmsmac](http://linuxwireless.org/en/users/Drivers/brcm80211). This driver should be loaded out of the box. It does however suffer from a resume issue in kernel 2.6.37 when the laptop resumes from suspend. The Wi-Fi does not come back up unless it is [reloaded](/index.php/Broadcom_wireless#Wifi_card_does_not_work_when_resuming_from_suspend_.28brcm80211.29 "Broadcom wireless").

### Non-free alternative driver for the Broadcom BCM4113 chipset

An alternative may be the [802.11 Linux STA driver](http://www.broadcom.com/support/802.11/linux_sta.php), which can be installed from the [AUR](/index.php/AUR "AUR"): [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/)

### Free kernel driver for the Atheros AR9285 802.11b/g chipset

The [ath9k](http://wireless.kernel.org/en/users/Drivers/ath9k) module is detected by [udev](/index.php/Udev "Udev") and loaded out of the box.

Some users report issues with the `ath9k` driver and this particular chipset. In this case, use the [ndiswrapper](/index.php/Wireless_Setup#ndiswrapper "Wireless Setup") method. Also, add `!ath9k` and `ndiswrapper` to the `MODULES` array in `/etc/rc.conf`.

## Graphics

The Intel GMA 3150 requires the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) module. No xorg.conf file is required.

## Input

The keyboard and touchpad work more or less without problems using the [xf86-input-keyboard](https://www.archlinux.org/packages/?name=xf86-input-keyboard) and [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) modules, respectively. Right- and left-clicking works, as well as vertical edge scrolling and right-click tapping. I have not managed to get two- and three-finger taps to work, nor two-finger scroll.

### Function keys

The function keys only work for some extent, e.g. the keys for turning off the LCD backlight works but not those for turning on and off Wi-Fi, touchpad, etc. To make the volume keys work, map "XF86AudioRaiseVolume" to "amixer set Master 5%+" and "XF86AudioLowerVolume" to "amixer set Master 5%-"

The brightness keys do not work and do not appear to be recognized by the system. To adjust brightness, see [[1]](http://www.winmoor.nl/Samsung-R519-Display-Brightness.html) and map `Super`+`Up` and `Super`+`Down` to the up and down scripts, respectively.

Create a file called something like "brighness_up" in a directory of your choice, e.g. `/home/your_user_name/scripts/brightness_up`

Paste the text below, and save the file.

```
#!/bin/bash

# these are the possible values:
# 42 56 70 92 AF CC E5 FF
# 30 40 50 60 70 80 90 100 %

Current=`sudo setpci -s 00:02.0 F4.B`
case $Current in
  42)
    sudo setpci -s 00:02.0 F4.B=56
  ;;
  56)
    sudo setpci -s 00:02.0 F4.B=70
  ;;
  70)
    sudo setpci -s 00:02.0 F4.B=92
  ;;
  92)
    sudo setpci -s 00:02.0 F4.B=af
  ;;
  af)
    sudo setpci -s 00:02.0 F4.B=cc
  ;;
  cc)
    sudo setpci -s 00:02.0 F4.B=e5
  ;;
  e5)
    sudo setpci -s 00:02.0 F4.B=ff
  ;;
esac
Current=`sudo setpci -s 00:02.0 F4.B`
case $Current in
  42)
    notify-send "Brightness is at 30%"
  ;;
  56)
    notify-send "Brightness is at 40%"
  ;;
  70)
    notify-send "Brightness is at 50%"
  ;;
  92)
    notify-send "Brightness is at 60%"
  ;;
  af)
    notify-send "Brightness is at 70%"
  ;;
  cc)
    notify-send "Brightness is at 80%"
  ;;
  e5)
    notify-send "Brightness is at 90%"
  ;;
  ff)
    notify-send "Brightness is at 100%"
  ;;
esac

```

And make the file executable, e.g

```
chmod u+x ~/scripts/brightness_up

```

For lowering the screen brightness, make a script containing this:

```
#!/bin/bash

# these are the possible values:
# 42 56 70 92 AF CC E5 FF
# 30 40 50 60 70 80 90 100 %

Current=`sudo setpci -s 00:02.0 F4.B`
case $Current in
  ff)
    sudo setpci -s 00:02.0 F4.B=e5
  ;;
  e5)
    sudo setpci -s 00:02.0 F4.B=cc
  ;;
  cc)
    sudo setpci -s 00:02.0 F4.B=af
  ;;
  af)
    sudo setpci -s 00:02.0 F4.B=92
  ;;
  92)
    sudo setpci -s 00:02.0 F4.B=70
  ;;
  70)
    sudo setpci -s 00:02.0 F4.B=56
  ;;
  56)
    sudo setpci -s 00:02.0 F4.B=42
  ;;
esac
Current=`sudo setpci -s 00:02.0 F4.B`
case $Current in
  42)
    notify-send "Brightness is at 30%"
  ;;
  56)
    notify-send "Brightness is at 40%"
  ;;
  70)
    notify-send "Brightness is at 50%"
  ;;
  92)
    notify-send "Brightness is at 60%"
  ;;
  af)
    notify-send "Brightness is at 70%"
  ;;
  cc)
    notify-send "Brightness is at 80%"
  ;;
  e5)
    notify-send "Brightness is at 90%"
  ;;
  ff)
    notify-send "Brightness is at 100%"
  ;;
esac

```

**Note:** With Kernel 3.10.10-1 the function keys, including Wifi, touchpad, volume, and brightness, work out of the box