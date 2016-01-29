# Armstone A9

The ArmStone A9 is an ARM developement platform board in PicoITX form factor with Freescale i.MX6 CPU.

## Contents

*   [1 Prerequisites](#Prerequisites)
    *   [1.1 Bootloader version](#Bootloader_version)
    *   [1.2 Base system](#Base_system)
    *   [1.3 Serial console access](#Serial_console_access)
*   [2 Setup](#Setup)
    *   [2.1 Install kernel](#Install_kernel)
    *   [2.2 Booting from USB](#Booting_from_USB)
*   [3 See also](#See_also)

## Prerequisites

### Bootloader version

Sources, kernel and firmware images can be downloaded from the companies [support page](https://www.fs-net.de/de/support/mein-f-und-s/). Registration is required and after that you have to activate access to specific device documentation and resources by providing the board serial number. Its recommended to use the newest uboot and nboot firmware images provided by the company, since essential functionalities like booting from usb/sdcard were added in later versions. In some cases, partial version upgrades are necessary to get from a very old bootloader version to the newest one. Consult the manufacturer [linux documentation](https://www.fs-net.de/assets/download/docu/common/en/FSiMX6_FirstSteps_eng.pdf) on how to access and update the bootloader.

### Base system

Unfortunately, this board is only supported by the companys own [linux kernel 3.0.35](http://forum.fs-net.de/index.php/Thread/3972-fsimx6-V2-1-released/), which is too old to run the newest stock ArchLinuxARM image ([systemd requires at least kernel 3.15/3.16](http://archlinuxarm.org/forum/viewtopic.php?f=47&t=9225#p48367)). The company is looking forward to provide a newer kernel in the [first quarter of 2016](http://forum.fs-net.de/index.php/Thread/3842-armStoneA9-Linux-development-state-and-releases/?postID=13176#post13176). So usually we could use [ArchLinuxARM-armv7-latest](http://os.archlinuxarm.org/os/ArchLinuxARM-armv7-latest.tar.gz) base system but following packages has to be downgraded and recompiled:

```
libsystemd ~221-1
systemd ~216-3
libgcrypt
dbus
dbus-glib
libdbus
libutil-linux
util-linux

```

**Warning:** The following section referes to ArchLinuxARM images which are from an untrusted and unknown source. Use it at your own risk!

Following ArchLinuxARM base system package already contains older systemd binaries and is compatible with the older stock kernel: [https://groups.google.com/forum/#!topic/wandboard/Spo2LR0wmZo](https://groups.google.com/forum/#!topic/wandboard/Spo2LR0wmZo) The content of the package can be copied to a sdcard or usb-stick partition, preferably ext3/ext4 formatted.

### Serial console access

The pins 55 (RX0), 57 (TX0) and 61 (GND) can be used for RS232 serial connection according to the [hardware documentation](https://www.fs-net.de/assets/download/docu/armstone/en/armStoneA9_Hardware_eng.pdf). Serial console access is necessary to update and configure the bootloader.

## Setup

First access the bootloader console via. serial connection, see manufacturer [linux documentation](https://www.fs-net.de/assets/download/docu/common/en/FSiMX6_FirstSteps_eng.pdf).

### Install kernel

In this example, we'll initialize the usb system and load the kernel image from a ext3/ext4 partition on the usb stick. After that the NAND kernel partition gets erased and recieves a the new kernel image:

```
armStoneA9 # usb start
armStoneA9 # ex4load usb 0:1 $(loadaddr) /boot/uImage-fsimx6
armStoneA9 # nand erase.part Kernel
armStoneA9 # nand write $loadaddr Kernel $filesize

```

### Booting from USB

Considering we already have the kernel loaded into NAND, we just need a base system on the usb stick to start from. Before that, we have to define the rootfs environement variable in the U-Boot bootloader. This variable will tell the kernel which device is to be used to start from. In this case, it's the usb partition called `/dev/sda1`:

```
armStoneA9 # setenv rootfs root=/dev/sda1 rootdelay=5 
armStoneA9 # run bootcmd

```

The command `run bootcmd` initiates the boot process by starting the kernel.

## See also

*   [Main product page from the manufacturer](https://www.fs-net.de/en/products/armstone/armstonea9/)
*   [Hardware documentation (pdf)](https://www.fs-net.de/assets/download/docu/armstone/en/armStoneA9_Hardware_eng.pdf)
*   [Linux documentation (pdf)](https://www.fs-net.de/assets/download/docu/common/en/FSiMX6_FirstSteps_eng.pdf)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Armstone_A9&oldid=413510](https://wiki.archlinux.org/index.php?title=Armstone_A9&oldid=413510)"