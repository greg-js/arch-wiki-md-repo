[PC Engines](http://pcengines.ch/) is a swiss hardware manufacturer for embedded x86 devices.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 apu2c4](#apu2c4)
    *   [1.1 Hardware](#Hardware)
    *   [1.2 Setup preperations](#Setup_preperations)
    *   [1.3 Boot the system](#Boot_the_system)
    *   [1.4 Install the system](#Install_the_system)
    *   [1.5 LED Control](#LED_Control)
        *   [1.5.1 Load Modules](#Load_Modules)
        *   [1.5.2 Example Configuration](#Example_Configuration)
        *   [1.5.3 Persist Configuration](#Persist_Configuration)

## apu2c4

This document describes how to install Arch Linux to the SSD via an SD card or USB flash drive.

### Hardware

CPU: AMD Embedded G series GX-412TC, 1 GHz quad Jaguar core with 64 bit

RAM: 4GB DRAM with ECC

**Note:** Remove the screws from the serial port first!

Assemble the device with care and read the [guide for the cooling system](http://pcengines.ch/apucool.htm)!

### Setup preperations

*   You need a serial (RS-232) connection to the apu to control it.
*   Add your user to uucp
*   Install picocom or something similar, see [Working with the serial console#Making Connections](/index.php/Working_with_the_serial_console#Making_Connections "Working with the serial console")
*   Download and verify the [arch-dualboot.iso](https://www.archlinux.org/download/)

### Boot the system

To see the BIOS use this command

```
LANG=C picocom --baud 115200 --omap crcrlf /dev/ttyUSB0

```

If your device does not boot from the SD card or USB flash drive, press F10 during boot to bring up a boot menu. Then close picocom with "Ctl+A" "Ctl+Q"

Reconnect to the ArchIso Grub:

```
LANG=C picocom --baud 38400 /dev/ttyUSB0

```

Enter cli mode by pressing "Tab", prompt should look like this:

```
linux boot/x86_64/vmlinuz archisobasedir=arch archisolabel=ARCH_201710 initrd=boot/intel_ucode.img,boot/x86_64/archiso.img

```

add the following **with a leading space**

```
 console=ttyS0,115200

```

and press "Enter"

Now exit picocom and reconnect with the first command again to switch to the higher baud rate of 115200. Finally wait for about 30 seconds and you will get a colorful boot prompt.

### Install the system

The most comfortable way to install Arch now is to start the sshd and use [Install guide](/index.php/Install_guide "Install guide")

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

If using [Syslinux](/index.php/Syslinux "Syslinux"), make sure to provide a `console` option in the boot menu:

 `/boot/syslinux/syslinux.cfg` 
```
LABEL arch
    MENU LABEL Arch Linux
    LINUX ../vmlinuz-linux
    APPEND root=UUID=1ef5a2eb-1908-4929-9b91-f6c4183695ac rw console=ttyS0,115200
    INITRD ../initramfs-linux.img
```

Also you should read [Working with the serial console#Configure console access on the target machine](/index.php/Working_with_the_serial_console#Configure_console_access_on_the_target_machine "Working with the serial console")

Remember to remove the SD card or USB flash drive after you finished your setup.

### LED Control

Newer (as of 2019) kernels include both the `leds_apu` ([4.15+](https://github.com/torvalds/linux/commit/3faee9423ce07186fc9dcec2981d4eb8af8872bb)) and the `ledtrig_netdev` ([4.16+](https://github.com/torvalds/linux/commit/50081e437872e68300750068754f21d0faac5d86)) [kernel modules](/index.php/Kernel_module "Kernel module"). This enables control of the APU's 3 front LEDs through the following sysfs entries:

```
/sys/class/leds/apu2:green:1
/sys/class/leds/apu2:green:2
/sys/class/leds/apu2:green:3

```

#### Load Modules

The `leds_apu` driver should automatically load on boot, but you may need to [manually load](/index.php/Kernel_module#Manual_module_handling "Kernel module") `ledtrig_netdev`.

#### Example Configuration

A common use case is to use the APU as a wireless [router](/index.php/Router "Router"). In this scenario, one wired NIC (wan0) is connected upstream to an ISP and the remaining wired & wireless NICs are [bridged](/index.php/Network_bridge "Network bridge") (br0) together as the LAN. A typical LED configuration using the *netdev* trigger might be:

```
LED1: power on / power off indicator
LED2: upstream network (wan0) traffic indicator
LED3: local network (br0) traffic indicator

```

To enable this setup:

```
echo "netdev" > /sys/class/leds/apu2:green:2/trigger
echo "wan0" > /sys/class/leds/apu2:green:2/device_name
echo "1" > /sys/class/leds/apu2:green:2/tx
echo "1" > /sys/class/leds/apu2:green:2/rx
echo "netdev" > /sys/class/leds/apu2:green:3/trigger
echo "br0" > /sys/class/leds/apu2:green:3/device_name
echo "1" > /sys/class/leds/apu2:green:3/tx
echo "1" > /sys/class/leds/apu2:green:3/rx

```

**Note:** Writing to the `trigger` sysfs entry must be done first as this is what enables the `device_name`, `tx` `rx` entries.

`/sys/class/leds/apu2:green:1` is likely enabled on boot automatically but if not it can be set as follows:

```
echo "1" > /sys/class/leds/apu2:green:1/brightness

```

**Tip:** View triggers supported by the currently loaded modules: `cat /sys/class/leds/apu2:green:1/trigger`.

**Tip:** Additional trigger modules are available here: `/lib/modules/$(uname -r)/kernel/drivers/leds/trigger`.

#### Persist Configuration

Systemd [automatic module loading](/index.php/Kernel_module#Automatic_module_loading_with_systemd "Kernel module") and [tmpfiles.d](/index.php/Systemd#Temporary_files "Systemd") can be used to persist this configuration across restarts.

 `/etc/modules-load.d/ledtrig-netdev.conf`  `ledtrig_netdev`  `/etc/tmpfiles.d/leds.conf` 
```
w /sys/class/leds/apu2:green:2/trigger - - - - netdev
w /sys/class/leds/apu2:green:2/device_name - - - - wan0
w /sys/class/leds/apu2:green:2/tx - - - - 1
w /sys/class/leds/apu2:green:2/rx - - - - 1
w /sys/class/leds/apu2:green:3/trigger - - - - netdev
w /sys/class/leds/apu2:green:3/device_name - - - - br0
w /sys/class/leds/apu2:green:3/tx - - - - 1
w /sys/class/leds/apu2:green:3/rx - - - - 1
```