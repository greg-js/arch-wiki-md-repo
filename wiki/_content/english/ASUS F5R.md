## Contents

*   [1 Hardware](#Hardware)
*   [2 Configuration](#Configuration)
    *   [2.1 CPU](#CPU)
    *   [2.2 Video](#Video)
    *   [2.3 Audio](#Audio)
    *   [2.4 Wi-Fi](#Wi-Fi)
    *   [2.5 Webcam](#Webcam)
    *   [2.6 Bluetooth](#Bluetooth)
    *   [2.7 Pointer](#Pointer)
    *   [2.8 Leds & ACPI upgrade](#Leds_.26_ACPI_upgrade)
    *   [2.9 OLED Display](#OLED_Display)
        *   [2.9.1 Function Keys](#Function_Keys)
    *   [2.10 Utilities](#Utilities)
        *   [2.10.1 The Lapsus daemon & KDE applet](#The_Lapsus_daemon_.26_KDE_applet)

## Hardware

*   _CPU:_
    *   _Intel(R) Celeron(R), M 520 (1.6GHz), 533MHz FSB, 1MB L2 Cache_
    *   _Intel(R) Core Duo(R), T 2130 (1.86GHz), 533MHz FSB, 1MB L2 Cache_
*   _Chipset:_ ATI Radeon Xpress 1100
*   _RAM:_ 1024MB (1 x 1024MB) SO-DIMM DDR2 533MHz, max 2048 MB
*   _Hard Disk:_ SATA 120GB 5400 rpm
*   _DVD Burner:_ DVD-RW Super Multi DualLayer
*   _Display:_ TFT 15.4" WXGA (1280x800) _ColorShine TFT-LCD, Asus Splendid Video Intelligent Technology_
*   _Video:_ ATI® Xpress™ Radeon™ X1100 128MB HyperMemory
*   _Audio:_ Intel High Definition Audio
*   _Wi-Fi:_ 802.11g
*   _Bluetooth:_ 2.0+EDR
*   _Webcam:_ 1.3 Mpixel
*   _Modem:_ 56 Kbps V.90
*   _LAN:_10/100 Mbps Ethernet
*   _Connectors:_
    *   _1 x Microphone-in jack_
    *   _1 x Headphone-out jack (S/PDIF)_
    *   _1 x TypeII PCMCIA slot'_
    *   _1 x VGA port_
    *   _4 x USB 2.0 ports_
    *   _1 x RJ11 Modem jack for phone line_
    *   _1 x RJ45 LAN Jack for LAN insert_
*   _Card Reader:_ MMC, SD, MS, MS-Pro
*   _Dimension and Weight:_
    *   _362mm * 262mm * 27mm(W x D x H)_
    *   _2,6 Kg (6-cell)_
*   _Pointer:_ Touch pad

## Configuration

### CPU

Works out of the box.

Follow this [SpeedStep](/index.php/SpeedStep "SpeedStep") guide to enable speed-stepping.

### Video

Works with the ATI Catalyst proprietary driver.

Follow this guide: [ATI#ATI Catalyst proprietary driver](/index.php/ATI#ATI_Catalyst_proprietary_driver "ATI")

Console framebuffer is working in 1024x768 with the vga=0x317 kernel boot option. With the vesafb-tng patch the native display resolution should work, too.

### Audio

Works out of the box.

Follow the official documentation: [ALSA](/index.php/ALSA "ALSA")

### Wi-Fi

To enable wireless follow the official guide: [Wireless network configuration#ndiswrapper](/index.php/Wireless_network_configuration#ndiswrapper "Wireless network configuration")

Please note that the Asus F5R needs the bcmwl5.inf driver.

Other way is to use b43 driver: [Wireless network configuration#b43](/index.php/Wireless_network_configuration#b43 "Wireless network configuration")

NetworkManager is also a cool option.

### Webcam

Since there is no official support for the Asus Webcam, you need to install separate drivers from [the AUR](https://aur.archlinux.org/packages.php?ID=12669).

### Bluetooth

Works out of the box.

### Pointer

To enable the pointer follow this guide: [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")

A really cool utility is gsynaptics (available in the [community] repo).

### Leds & ACPI upgrade

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

#### Function Keys

WiP

### Utilities

Here are some useful utilities:

#### The Lapsus daemon & KDE applet

Lapsus is a set of programs created to help manage additional laptop features such as:

```
   * All the LEDs (on/off)
   * LCD Backlight
   * Wireless radio switch
   * Bluetooth adapter switch
   * Alsa mixer (volume control, mute/unmute)
   * Synaptics touchpad (on/off)
   * Volume/Mute hotkeys
   * Touchpad hotkey
   * Backlight hotkey
   * LightSensor switch and sensitivity level (svn version only)

```

~~Prerequisites: acpi4asus from CVS (at least a version > 0.41).~~ In your rc.conf, blacklist the 'acpi_asus' module and add the 'asus_laptop' one in the MODULES array.

Install the latest lapsus package from [aur](https://aur.archlinux.org/packages.php?do_Details=1&ID=11207). Now start the lapsusd daemon: **/etc/rc.d/lapsusd start**. You can add it into DAEMONS array in **/etc/rc.conf**.

Finally add the lapsus applet to KDE kicker.