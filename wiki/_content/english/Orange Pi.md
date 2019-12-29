Orange Pi (One) is a minimalist computer built for the [ARMv7-A architecture](https://en.wikipedia.org/wiki/ARMv7-A "wikipedia:ARMv7-A"). [More information about this project](http://www.orangepi.org/).

**Note:** The device is not officially supported by the ALARM project, i.e. please refrain from submitting patches, feature requests or bug reports for it.

This article is strongly based on [Banana Pi](/index.php/Banana_Pi "Banana Pi"). Moreover this article is not meant to be an exhaustive setup guide and assumes that the reader has setup an Arch system before.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Prerequisites](#Prerequisites)
    *   [1.2 Using original ArchLinuxARM tarball](#Using_original_ArchLinuxARM_tarball)
        *   [1.2.1 Install basesystem to a SD card](#Install_basesystem_to_a_SD_card)
        *   [1.2.2 Compile and copy U-Boot bootloader](#Compile_and_copy_U-Boot_bootloader)
        *   [1.2.3 Using U-Boot precompiled binaries](#Using_U-Boot_precompiled_binaries)
        *   [1.2.4 Login / SSH](#Login_/_SSH)
    *   [1.3 Additional step, Wi-Fi Drivers](#Additional_step,_Wi-Fi_Drivers)
        *   [1.3.1 RTL8189ES/ETV](#RTL8189ES/ETV)
        *   [1.3.2 Xradio XR819](#Xradio_XR819)
*   [2 Orange Pi PC2](#Orange_Pi_PC2)
    *   [2.1 UBoot](#UBoot)
    *   [2.2 Install basesystem to a SD card](#Install_basesystem_to_a_SD_card_2)
*   [3 See also](#See_also)

## Installation

### Prerequisites

build-essentials and other common compiling packages (see [aur](/index.php/Aur "Aur")). For compiling boot script with mkimage [uboot-tools](https://www.archlinux.org/packages/?name=uboot-tools) and for bootloader compilation [arm-none-eabi-gcc](https://www.archlinux.org/packages/?name=arm-none-eabi-gcc)

### Using original ArchLinuxARM tarball

This method will install unmodified ArchLinuxARM armv7 basesystem to your Orange Pi One, meaning you'll have the latest mainline kernel running. It will probably also work on other H3 Orange Pis with mainline support.

#### Install basesystem to a SD card

Zero the beginning of the SD card:

```
dd if=/dev/zero of=/dev/sdX bs=1M count=8

```

Use [fdisk](/index.php/Fdisk "Fdisk") to partition the SD card, and [format](/index.php/File_systems "File systems") it with `mkfs.ext4 -O ^metadata_csum,^64bit /dev/sdX1`.

Mount the ext4 filesystem, replacing `sdX1` with the formatted partition:

```
# mkdir mnt
# mount /dev/*sdX1* /mnt

```

Download and extract the root filesystem:

```
# wget [http://archlinuxarm.org/os/ArchLinuxARM-armv7-latest.tar.gz](http://archlinuxarm.org/os/ArchLinuxARM-armv7-latest.tar.gz)
# bsdtar -xpf ArchLinuxARM-armv7-latest.tar.gz -C /mnt/

```

Create a file with the following boot script

 `boot.cmd` 
```
part uuid ${devtype} ${devnum}:${bootpart} uuid
setenv bootargs console=${console} root=PARTUUID=${uuid} rw rootwait

if load ${devtype} ${devnum}:${bootpart} ${kernel_addr_r} /boot/zImage; then
  if load ${devtype} ${devnum}:${bootpart} ${fdt_addr_r} /boot/dtbs/${fdtfile}; then
    if load ${devtype} ${devnum}:${bootpart} ${ramdisk_addr_r} /boot/initramfs-linux.img; then
      bootz ${kernel_addr_r} ${ramdisk_addr_r}:${filesize} ${fdt_addr_r};
    else
      bootz ${kernel_addr_r} - ${fdt_addr_r};
    fi;
  fi;
fi

if load ${devtype} ${devnum}:${bootpart} 0x48000000 /boot/uImage; then
  if load ${devtype} ${devnum}:${bootpart} 0x43000000 /boot/script.bin; then
    setenv bootm_boot_mode sec;
    bootm 0x48000000;
  fi;
fi
```

Compile it and write it to the SD-card using the package [uboot-tools](https://www.archlinux.org/packages/?name=uboot-tools)

```
# mkimage -A arm -O linux -T script -C none -a 0 -e 0 -n "Orange Pi One boot script" -d boot.cmd /mnt/boot/boot.scr
# umount /mnt

```

#### Compile and copy U-Boot bootloader

The next step is creating a u-boot image. Make sure you have [arm-none-eabi-gcc](https://www.archlinux.org/packages/?name=arm-none-eabi-gcc), [dtc](https://www.archlinux.org/packages/?name=dtc), [git](https://www.archlinux.org/packages/?name=git), [swig](https://www.archlinux.org/packages/?name=swig) and [uboot-tools](https://www.archlinux.org/packages/?name=uboot-tools) installed on your system. If you compile for a different H3 Orange Pi than the One, replace orangepi_one_config accordingly. Then clone the u-boot source code and compile a Orange Pi image:

```
$ git clone [git://git.denx.de/u-boot.git](git://git.denx.de/u-boot.git)
$ cd u-boot
$ git checkout tags/v2019.04
$ make -j4 ARCH=arm CROSS_COMPILE=arm-none-eabi- orangepi_one_defconfig
$ make -j4 ARCH=arm CROSS_COMPILE=arm-none-eabi-

```

If everything went fine you should have an U-Boot image: u-boot-sunxi-with-spl.bin. Now dd the image to your sdcard, where /dev/sdX is your sdcard.

```
# dd if=u-boot-sunxi-with-spl.bin of=/dev/sdX bs=1024 seek=8

```

#### Using U-Boot precompiled binaries

If you couldn't compile them on your AMD64 machine, just grab them at: [https://gitlab.com/vinibali/orangepi_uboot](https://gitlab.com/vinibali/orangepi_uboot)

Use the same command for placing it to the sdcard:

```
# dd if=u-boot-sunxi-with-spl.bin of=/dev/sdX bs=1024 seek=8

```

#### Login / SSH

SSH login for root is disabled by default. Login with the default user account and use [su](/index.php/Su "Su").

| Type | Username | Password |
| Root | `root` | `root` |
| User | `alarm` | `alarm` |

### Additional step, Wi-Fi Drivers

#### RTL8189ES/ETV

This driver will require to Orange Pi Plus / Plus 2.

First, Install the kernel headers.

```
# sudo pacman -S base-devel git linux-armv7-headers

```

Then, build out-of-tree driver.

**Note:** Replace KSRC to your own kernel version.

```
# git clone [https://github.com/jwrdegoede/rtl8189ES_linux.git](https://github.com/jwrdegoede/rtl8189ES_linux.git)
# cd rtl8189ES_linux
# make -j4 ARCH=arm KSRC=/usr/lib/modules/4.18.11-1-ARCH/build/ 

```

And install manually.

**Note:** Replace modules directory to your own kernel version.

```
# cp 8189es.ko /usr/lib/modules/4.18.11-1-ARCH/kernel/drivers/net/wireless/realtek/
# depmod -a
# modprobe 8189es

```

#### Xradio XR819

This hardware will require the out of tree [xradio-git](https://aur.archlinux.org/packages/xradio-git/) kernel driver for Orange Pi Zero.

```
# pacaur -S xradio-git

```

Version 5.3.1-1-ARCH is working fine, but if you couldn't find the wlan0 device on the interfaces list,

you'll need to burn the 201907 u-boot loader and copy the dtb file to /boot/dtbs as well from: [https://gitlab.com/vinibali/orangepi_uboot](https://gitlab.com/vinibali/orangepi_uboot).

```
# wget [https://gitlab.com/vinibali/orangepi_uboot/-/archive/master/orangepi_uboot-master.zip](https://gitlab.com/vinibali/orangepi_uboot/-/archive/master/orangepi_uboot-master.zip)
# unzip -q
# dd if=orangepi_uboot-master/201907/orangepi_zero/u-boot-sunxi-with-spl.bin of=/dev/mmcblk0 bs=1024 seek=8
# cp orangepi_uboot-master/201907/dtb/sun8i-h2-plus-orangepi-zero.dtb /boot/dtbs

```

## Orange Pi PC2

Allwinner H5 @ 1.20Ghz 64bit system AArch64

[General information about the device](http://linux-sunxi.org/Xunlong_Orange_Pi_PC_2)

**Note:** The device is also not officially supported by the ALARM project

Follow general installation instruction above. Differences:

### UBoot

```
# git clone [https://github.com/ARM-software/arm-trusted-firmware.git](https://github.com/ARM-software/arm-trusted-firmware.git)
# git clone [git://git.denx.de/u-boot.git](git://git.denx.de/u-boot.git)
# cd arm-trusted-firmware
# make CROSS_COMPILE=aarch64-linux-gnu- PLAT=sun50i_a64 DEBUG=1 -j4 bl31
# cp build/sun50i_a64/debug/bl31.bin ../u-boot/
# cd ../u-boot
# git checkout tags/v2019.04
# make ARCH=arm CROSS_COMPILE=aarch64-linux-gnu- -j4 orangepi_pc2_defconfig
# make ARCH=arm CROSS_COMPILE=aarch64-linux-gnu- -j4
# dd if=u-boot-sunxi-with-spl.bin of=/dev/sdX bs=8k seek=1

```

### Install basesystem to a SD card

For AARCH64 you'll need another rootfs

```
# wget [http://archlinuxarm.org/os/ArchLinuxARM-aarch64-latest.tar.gz](http://archlinuxarm.org/os/ArchLinuxARM-aarch64-latest.tar.gz)
# bsdtar -xpf ArchLinuxARM-aarch64-latest.tar.gz -C mnt/

```

change the /mnt/boot/boot.cmd to

 `boot.cmd` 
```
part uuid ${devtype} ${devnum}:${bootpart} uuid
setenv bootargs console=${console} root=PARTUUID=${uuid} rw rootwait
setenv fdtfile allwinner/sun50i-h5-orangepi-pc2.dtb

if load ${devtype} ${devnum}:${bootpart} ${kernel_addr_r} /boot/Image; then
  if load ${devtype} ${devnum}:${bootpart} ${fdt_addr_r} /boot/dtbs/${fdtfile}; then
    if load ${devtype} ${devnum}:${bootpart} ${ramdisk_addr_r} /boot/initramfs-linux.img; then
      booti ${kernel_addr_r} ${ramdisk_addr_r}:${filesize} ${fdt_addr_r};
    else
      booti ${kernel_addr_r} - ${fdt_addr_r};
    fi;
  fi;
fi
```

make image the /mnt/boot/boot.scr to

```
# mkimage -C none -A arm64 -T script -d /mnt/boot/boot.cmd /mnt/boot/boot.scr

```

## See also

*   ["Just another Geek's" blog about installing Linux](https://blog.christophersmart.com/2016/10/23/building-and-booting-upstream-linux-and-u-boot-for-orange-pi-one-arm-board/)