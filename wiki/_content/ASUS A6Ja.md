# ASUS A6Ja

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
    *   [2.10 Utilities](#Utilities)
        *   [2.10.1 The Lapsus daemon](#The_Lapsus_daemon)

## Hardware

*   _CPU:_ Intel Core Duo T2400 (1.83GHz, 2MB cache L2, FSB 667MHz)
*   _Chipset:_ Mobile Intel® 945 PM Express Chipset
*   _RAM:_ 1024MB (1 x 1024MB) DDR2 SDRAM 667 Mhz
*   _Hard Disk:_ SATA 100GB 4200 rpm
*   _DVD Burner:_ TSS-CORP TS-632d
*   _Display:_
    *   _TFT 15.4" WXGA (1280x800)_ ColorShine TFT-LCD, Asus Splendid Video Intelligent Technology
*   _Video:_ ATI Mobility Radeon X1600 256MB
*   _Audio:_ Scheda Intel High Definition Audio
*   _Wi-Fi:_ Intel PRO/Wireless 3945ABG 802.11a/b/g
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
    *   _354mm * 284mm * 35 mm(W x D x H)_
    *   _2.7 Kg (8-cell)_
*   _Pointer:_ Touch pad

## Configuration

### CPU

Works out of the box.

Follow this [SpeedStep](/index.php/SpeedStep "SpeedStep") guide to enable speed-stepping.

### Video

Works with the proprietary ATI driver in full display resolution.

TV-Out/DVI currently untested

VGA-Out is working with catalyst-control-center

#### Xorg

Follow this guide: [ATI](/index.php/ATI "ATI")

No problems detected.

### Audio

Works out of the box.

Follow the official documentation: [ALSA](/index.php/ALSA "ALSA")

### Wi-Fi

To enable wireless follow the official guide: [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")

NetworkManager is also a cool option.

### Webcam

Currently untested

### Bluetooth

To enable bluetooth support, go here: [Bluetooth](/index.php/Bluetooth "Bluetooth")

### Pointer

To enable the pointer follow this guide: [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")

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

Follow one of the guides in [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys")

### Utilities

Here are some useful utilities:

#### The Lapsus daemon

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

~~Prerequisites: acpi4asus from CVS (at least a version > 0.41).~~ In your /etc/modprobe.d/ directory, blacklist the 'acpi_asus' module and add the 'asus_laptop' in the /etc/modules-load.d directory.

Install [lapsus](https://github.com/aur-archive/lapsus) or [lapsus-svn](https://github.com/aur-archive/lapsus-svn) from the AUR archive. There will be certain complications. First, the berlios.de site on which the lapsus project was formerly hosted has closed down. Fortunately, the code is [archived on Google Code](https://code.google.com/p/lapsus/). You will need to modify the PKGBUILD accordingly. If you succeed in building the code you will need to create a lapsus.service file, since the PKGBUILDS antedate the adoption of systemd.

Now start the lapsusd daemon: **systemctl start lapsusd**. If if works well, then enable it **systemctl enable lapsusd**.

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_A6Ja&oldid=408077](https://wiki.archlinux.org/index.php?title=ASUS_A6Ja&oldid=408077)"