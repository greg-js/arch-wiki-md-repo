# Lenovo Ideapad s10-3t

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Contents

*   [1 System Specification](#System_Specification)
*   [2 Network](#Network)
    *   [2.1 Wired Ethernet](#Wired_Ethernet)
    *   [2.2 Wireless](#Wireless)
*   [3 Graphics](#Graphics)
*   [4 TouchScreen](#TouchScreen)
*   [5 SD Card Reader](#SD_Card_Reader)
*   [6 Accelerometer](#Accelerometer)

# System Specification

*   CPU: Intel Atom N450 (1.66 GHz) or N470?
*   Memory: 1GB DDR2 - can be upgraded to max of 2GB
*   Ethernet: Broadcom NetLink BCM57780 Gigabit
*   WiFi: Broadcom BCM4313 or Intel Corporation WiMAX/WiFi Link 6050 Series
*   Hard-Drive: 160GB standard with larger sizes available
*   Optical Drive: None
*   Integrated Graphics: Intel Pineview Integrated graphics
*   Touchscreen: ??? (2081:0A01) or Cando TouchScreen (2087:0A01)
*   Sound: Conexant pebble high definition smartaudip (14F1:5066) or Intel Corporation 82801G (ICH7 Family) High Definition Audio Controller (8086:27d8)
*   Screen: 10" LCD (1024x600)
*   SD Card Reader
*   Webcam: Lenovo Easycam?
*   Bluetooth: USI Co., Ltd (10ab:0816)?

# Network

## Wired Ethernet

See [Network configuration#Broadcom BCM57780](/index.php/Network_configuration#Broadcom_BCM57780 "Network configuration").

## Wireless

The Broadcom BCM4313 card requires the [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/)<sup><small>AUR</small></sup> module which is available in the AUR.

Intel Corporation WiMAX/WiFi Link 6050 Series works out of the box (2.6.34).

For WiMAX requires the kernel 2.6.35, [i2400m-firmware](https://aur.archlinux.org/packages.php?ID=39403)<sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2014-12-26]</sup>, [libeap](https://aur.archlinux.org/packages/libeap/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/libeap)]</sup>, [wimax-tools](https://aur.archlinux.org/packages/wimax-tools/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/wimax-tools)]</sup> and [wimax-network-service](https://aur.archlinux.org/packages/wimax-network-service/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/wimax-network-service)]</sup> which is available in the AUR.

# Graphics

*   This came from [Lenovo ideapad s10](https://wiki.archlinux.org/index.php/Lenovo_ideapad_s10) ...
*   So far I have not been able to get keyboard/touchpad to work with or without xorg.conf
*   use **vga=866** for the kernel line in `menu.lst`

See [Xorg](/index.php/Xorg "Xorg"), [Intel graphics](/index.php/Intel_graphics "Intel graphics") and [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

# TouchScreen

Cando TouchScreen works out of the box from kernel 2.6.35\. OneTouch.

# SD Card Reader

Works right out of the box (in fact you can even install arch directly on it with grub.)

# Accelerometer

The [IAPS](http://gitorious.org/iaps) driver works.

```
cd /usr/src
git clone [git://gitorious.org/iaps/iaps.git](git://gitorious.org/iaps/iaps.git)
cd iaps
make
sudo make install
depmod -a
modprobe iaps
dmesg
(you see something like input: iaps as /devices/virtual/input/input13)

```

lsinput (if you have input-utils installed) will give you something like this

```
/dev/input/event12
  bustype : BUS_ISA
  vendor  : 0x0
  product : 0x0
  version : 0
  name    : "iaps"
  phys    : "isa702/input0"
  bits ev : EV_SYN EV_ABS

```

and you can read events like this

```
$ input-events 12
waiting for events
15:13:53.622930: EV_ABS ABS_X 555
15:13:53.622958: EV_SYN code=0 value=0
15:13:53.973886: EV_ABS ABS_X 541
15:13:53.973916: EV_SYN code=0 value=0
15:13:54.024218: EV_ABS ABS_X 556
15:13:54.024240: EV_ABS ABS_Y 532
15:13:54.024243: EV_SYN code=0 value=0
15:13:54.073551: EV_ABS ABS_X 555
...

```

Here are some [ideas](http://www.thinkwiki.org/wiki/HDAPS#Applications) what to do with it.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_Ideapad_s10-3t&oldid=392336](https://wiki.archlinux.org/index.php?title=Lenovo_Ideapad_s10-3t&oldid=392336)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")