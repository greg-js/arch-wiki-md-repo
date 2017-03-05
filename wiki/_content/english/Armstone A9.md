The ArmStone A9 is an ARM developement platform board in PicoITX form factor with Freescale i.MX6 CPU.

**Note:** The device is not officially supported by the ALARM project, i.e. please refrain from submitting patches, feature requests or bug reports for it.

## Contents

*   [1 Prerequisites](#Prerequisites)
    *   [1.1 Bootloader version](#Bootloader_version)
    *   [1.2 Base system](#Base_system)
    *   [1.3 Serial console access](#Serial_console_access)
*   [2 Setup](#Setup)
    *   [2.1 Install kernel](#Install_kernel)
    *   [2.2 Install device tree file](#Install_device_tree_file)
    *   [2.3 Booting from USB](#Booting_from_USB)
*   [3 See also](#See_also)

## Prerequisites

### Bootloader version

Sources, kernel and firmware images can be downloaded from the companies [support page](https://www.fs-net.de/de/support/mein-f-und-s/). Registration is required and after that you have to activate access to specific device documentation and resources by providing the board serial number. Its recommended to use the newest uboot and nboot firmware images provided by the company, since essential functionalities like booting from usb/sdcard were added in later versions. In some cases, partial version upgrades are necessary to get from a very old bootloader version to the newest one. Consult the manufacturer [linux documentation](https://www.fs-net.de/assets/download/docu/common/en/FSiMX6_FirstSteps_eng.pdf) on how to access and update the bootloader.

### Base system

The content of the package [ArchLinuxARM-armv7-latest](http://os.archlinuxarm.org/os/ArchLinuxARM-armv7-latest.tar.gz) can be copied to a sdcard or usb-stick partition, preferably ext2/ext3 formatted. Further put the factory kernel (4.1) into the /boot directory of your flash drive, so it can be used later.

### Serial console access

The pins 55 (RX0), 57 (TX0) and 61 (GND) can be used for RS232 serial connection according to the [hardware documentation](https://www.fs-net.de/assets/download/docu/armstone/en/armStoneA9_Hardware_eng.pdf). Serial console access is necessary to update and configure the bootloader.

## Setup

First access the bootloader console via. serial connection, see manufacturer [linux documentation](https://www.fs-net.de/assets/download/docu/common/en/FSiMX6_FirstSteps_eng.pdf).

### Install kernel

In this example, we'll initialize the usb system and load the kernel image from a ext2/ext3 partition on the usb stick. After that the NAND kernel partition gets erased and recieves a the new kernel image:

```
armStoneA9 # usb start
armStoneA9 # ext2load usb 0:1 $(loadaddr) /boot/uImage-fsimx6
armStoneA9 # nand erase.part Kernel
armStoneA9 # nand write $loadaddr Kernel $filesize

```

### Install device tree file

```
tftp armstonea9q.dtb
nand erase.part FDT
nand write $loadaddr FDT $filesize

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