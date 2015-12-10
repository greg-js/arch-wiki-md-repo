# ASUS G1

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:ASUS G1#](https://wiki.archlinux.org/index.php/Talk:ASUS_G1))

## Contents

*   [1 Hardware](#Hardware)
*   [2 Configuration](#Configuration)
    *   [2.1 CPU](#CPU)
    *   [2.2 Video](#Video)
        *   [2.2.1 Xorg](#Xorg)
    *   [2.3 Audio](#Audio)
    *   [2.4 Wi-Fi](#Wi-Fi)
    *   [2.5 Webcam](#Webcam)
    *   [2.6 Bluetooth](#Bluetooth)
    *   [2.7 Pointer](#Pointer)
    *   [2.8 Leds & ACPI upgrade](#Leds_.26_ACPI_upgrade)
    *   [2.9 OLED Display](#OLED_Display)
        *   [2.9.1 Function Keys](#Function_Keys)

## Hardware

*   _CPU:_ Intel Core 2 Duo T7200 (2.00GHz, 4MB cache L2, FSB 667MHz)
*   _Chipset:_ Mobile Intel® 945 PM Express Chipset + ICH7M
*   _RAM:_ 2048MB (2 x 1024MB) DDR2 SDRAM 667 Mhz
*   _Hard Disk:_ SATA 160GB 5400 rpm - SATA 120GB 5400 rpm
*   _DVD Burner:_ SUPER MULTI DOUBLE LAYER
*   _Display:_
    *   _TFT 15.4" WXGA (1280x800)_ ColorShine TFT-LCD, Asus Splendid Video Intelligent Technology
    *   _TFT 15.4" WSXGA+ (1680x1050)_ ColorShine TFT-LCD, Asus Splendid Video Intelligent Technology
*   _Video:_ NVIDIA GeForce Go 7700 512MB
*   _Audio:_ Scheda Intel High Definition Audio
*   _Wi-Fi:_ 802.11a/b/g
*   _Bluetooth:_ 2.0+EDR
*   _Webcam:_ 1.3 Mpixel
*   _Modem:_ 56 Kbps V.90
*   _LAN Gigabit Ethernet:_ 10/100/1000
*   _Connectors:_
    *   _1 x Microphone-in jack_
    *   _1 x Headphone-out jack (S/PDIF)_
    *   _1 x TypeII PCMCIA slot_
    *   _1 x Line-in jack_
    *   _1 x VGA port_
    *   _1 x DVI-D port_
    *   _4 x USB 2.0 ports_
    *   _1 x IEEE 1394 port_
    *   _1 x RJ11 Modem jack for phone line_
    *   _1 x RJ45 LAN Jack for LAN insert_
    *   _1 x TV-out(S-Video)_
*   _Card Reader:_ MMC, SD, MS, MS-Pro
*   _Dimension and Weight:_
    *   _324mm * 284mm * 37.4 mm(W x D x H)_
    *   _3.1 Kg (8-cell)_
*   _Pointer:_ Touch pad

## Configuration

### CPU

Works out of the box. See [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") for some tweaks.

### Video

Works with the proprietary Nvidia driver in full display resolution.

TV-Out/DVI currently untested, but the graphics driver finds the interfaces, so they should be switchable with the nvidia-tools.

VGA-Out is working with nvidia-settings.

Console framebuffer is working in 1024x768 with the vga=0x317 kernel boot option. With the vesafb-tng patch the native display resolution should work, too.

#### Xorg

Follow this guide: [NVIDIA](/index.php/NVIDIA "NVIDIA")

No problems detected.

### Audio

Works out of the box.

Follow the official documentation: [ALSA](/index.php/ALSA "ALSA")

### Wi-Fi

To enable wireless follow the official guide: [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")

Please note that the Asus G1 needs the ipw3945 driver.

NetworkManager is also a cool option.

### Webcam

See [Webcam setup](/index.php/Webcam_setup "Webcam setup").

### Bluetooth

See the main article: [Bluetooth](/index.php/Bluetooth "Bluetooth")

### Pointer

To enable the pointer follow this guide: [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")

### Leds & ACPI upgrade

_**Note:**_ With recent kernels, compiling acpi4asus is no longer necessary. Skip to editing rc.conf below.

To enable every led (the ones on the LCD too) the first thing needed is upgrading the acpi module with the one provided by [acpi4asus](http://acpi4asus.sourceforge.net/).

It's really easy, follow these steps:

```
mkdir sources
cvs -d:pserver:anonymous@acpi4asus.cvs.sourceforge.net:/cvsroot/acpi4asus login
cvs -z3 -d:pserver:anonymous@acpi4asus.cvs.sourceforge.net:/cvsroot/acpi4asus co -P acpi4asus
cd acpi4asus/driver
make
make install

```

Now the new driver is installed. To use it and prevent udev from using the old one, edit your /etc/rc.conf and:

1.  Add to "MOD_BLACKLIST": asus_acpi
2.  Add to "MODULES": asus_laptop

Right now you can reboot or execute:

```
modprobe -r asus_acpi
modprobe asus_laptop

```

Everything done!

You'll find the leds in "/sys/class/leds/".

To enable a led write "1" in the "brightness" file in the right directory. To disable a led write "0" in the "brightness" file in the right directory.

Try this:

```
echo 1 > /sys/class/leds/asus:gaming/brightness 

```

Enjoy your leds!

### OLED Display

There is a package in AUR named asusoled.

kernel < 2.6.23: It needs turning off usbhid (rmmod usbhid) or patching the kernel: [asus-lcm.diff](http://kharg.LKSnet.org/asus-lcm.diff)

kernel >= 2.6.23: works out of a box

There is also a separate kernel driver based on asusoled: [Asus_OLED](http://lapsus.berlios.de/asus_oled.html). It works without patching usbhid or removing asus_laptop. Just load it before the usbhid module gets loaded and it will work (< 2.6.23, in new kernels works out of a box). It contains a small Qt utility, which can be used as a drop-in replacement for asusoled, and has some additional features.

You may simply want to display a digital clock with the date in the asusoled area. To do this :

1.  install [asus_oled-clock-svn](https://aur.archlinux.org/packages/asus_oled-clock-svn/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/asus_oled-clock-svn)]</sup> from the [AUR](/index.php/AUR "AUR").
2.  add 'asusoled-clock' in the daemons array of your rc.conf

There are also some interesting utilities available to control and utilize the OLED display over here: [https://bitbucket.org/SysGhost/asus-oled-command-line-utility.git](https://bitbucket.org/SysGhost/asus-oled-command-line-utility.git)

#### Function Keys

WiP -- Use Lapsus

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_G1&oldid=391882](https://wiki.archlinux.org/index.php?title=ASUS_G1&oldid=391882)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [ASUS](/index.php/Category:ASUS "Category:ASUS")