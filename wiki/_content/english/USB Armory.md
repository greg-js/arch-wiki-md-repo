The [USB armory](http://inversepath.com/usbarmory) from Inverse Path is an open source hardware design, implementing a flash drive sized computer.

The compact USB powered device provides a platform for developing and running a variety of applications.

The security features of the USB armory System on a Chip (SoC), combined with the openness of the board design, empower developers and users with a fully customizable USB trusted device for open and innovative personal security applications.

The hardware design features the Freescale i.MX53 processor, supporting advanced security features such as secure boot and ARM® TrustZone®.

*   Freescale i.MX53 ARM® Cortex™-A8 800Mhz, 512MB DDR3 RAM
*   USB host powered (<500 mA) device with compact form factor (65 x 19 x 6 mm)
*   ARM® TrustZone®, secure boot + storage + RAM
*   microSD card slot
*   5-pin breakout header with GPIOs and UART
*   customizable LED, including secure mode detection
*   USB device emulation (CDC Ethernet, mass storage, HID, etc.)
*   Open Hardware & Software

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 LED Brightness](#LED_Brightness)
*   [3 See also](#See_also)

## Installation

Follow the [official Arch Linux ARM instructions](http://archlinuxarm.org/platforms/armv7/freescale/usb-armory).

## Usage

### LED Brightness

By default, LED is way too bright after boot. Disable default modules:

 `/etc/modprobe.d/led.conf` 
```
blacklist leds_gpio
blacklist led_class
blacklist ledtrig_heartbeat

```

Use [Systemd#Temporary files](/index.php/Systemd#Temporary_files "Systemd") to set the brightness config:

 `/etc/tmpfiles.d/led.conf` 
```
w /sys/class/gpio/export - - - - 123
w /sys/class/gpio/gpio123/direction - - - - in

```

## See also

*   [https://github.com/yuvadm/usbarmory-arch](https://github.com/yuvadm/usbarmory-arch) for relevant packages mentioned in this article
*   [http://archlinuxarm.org/platforms/armv7/freescale/usb-armory](http://archlinuxarm.org/platforms/armv7/freescale/usb-armory) Article on USB Armory on archlinuxarm.org
*   [https://wiki.archassault.org/USB_Armory](https://wiki.archassault.org/USB_Armory) Article on the USB Armory on the archassault.org wiki
*   [https://github.com/ckuethe/usbarmory/wiki/USB-Gadgets](https://github.com/ckuethe/usbarmory/wiki/USB-Gadgets) How to present USB Armory as a mass storage, hid device and ethernet adapter at the same time