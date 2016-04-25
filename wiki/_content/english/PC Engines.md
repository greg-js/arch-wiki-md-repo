[PC Engines](http://pcengines.ch/) is a swiss hardware manufacturer for embedded x86 devices.

## Contents

*   [1 apu2c4](#apu2c4)
    *   [1.1 Hardware](#Hardware)
    *   [1.2 Setup preperations](#Setup_preperations)
    *   [1.3 Boot the system](#Boot_the_system)
    *   [1.4 Install the system](#Install_the_system)

## apu2c4

This document describes how to install Arch Linux to the SSD via a SD card.

### Hardware

CPU: AMD Embedded G series GX-412TC, 1 GHz quad Jaguar core with 64 bit

RAM: 4GB DRAM with ECC

**Note:** Remove the screws from the serial port first!

Assemble the device with care and read the [guide for the cooling system](http://pcengines.ch/apucool.htm)!

### Setup preperations

*   You need a serial (RS-232) connection to the apu to controll it.
*   Add your user to uucp
*   Install picocom or something similar, see [Working with the serial console#Making Connections](/index.php/Working_with_the_serial_console#Making_Connections "Working with the serial console")
*   Download and verify the [arch-dualboot.iso](https://www.archlinux.org/download/)

### Boot the system

To see the BIOS use this command

```
LANG=C picocom --baud 115200 --omap crcrlf /dev/ttyUSB0

```

If your device does not boot from the SD, press F10 during the boot and select the sdcard with a press to 1. Then close picocom with "Ctl+A" "Ctl+Q"

Reconnect to the ArchIso Grub:

```
LANG=C picocom --baud 38400 /dev/ttyUSB0

```

Enter cli mode by pressing "Tab", prompt should look like this:

```
kernel ....

```

add the following **with a leading space**

```
 console=ttyS0,38400

```

and press "Enter"

Now wait for about 30 seconds and you will get a colorful boot prompt

### Install the system

The most comftable way to install Arch now is to start the sshd and use [Install guide](/index.php/Install_guide "Install guide")

You may need to get a new IP with dhclient and start sshd

```
systemctl start sshd.service

```

One possible layout of the SSD maybe looking like this:

```
 /dev/sda1           2048   264191   262144  128M 83 Linux
 /dev/sda2         264192 25430015 25165824   12G 83 Linux
 /dev/sda3       25430016 31277231  5847216  2.8G 82 Linux swap / Solaris

```

It is a good idea to use a MBR layout with [GRUB](/index.php/GRUB "GRUB"):

```
grub-install --target=i386-pc /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg

```

Also you should read [Working with the serial console#Configure console access on the target machine](/index.php/Working_with_the_serial_console#Configure_console_access_on_the_target_machine "Working with the serial console")

Remember to remove the SD after you finished your setup.