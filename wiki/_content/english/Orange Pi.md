Orange Pi (One) is a minimalist computer built for the [ARMv7-A architecture](https://en.wikipedia.org/wiki/ARMv7-A "wikipedia:ARMv7-A"). [More information about this project](http://www.orangepi.org/).

**Note:** The device is not officially supported by the ALARM project, i.e. please refrain from submitting patches, feature requests or bug reports for it.

**Warning:** Do not upgrade to linux-armv7-4.12.0-1, Ethernet will no longer work

This article is strongly based on [Banana Pi](/index.php/Banana_Pi "Banana Pi"). Moreover this article is not meant to be an exhaustive setup guide and assumes that the reader has setup an Arch system before.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Using original ArchLinuxARM tarball](#Using_original_ArchLinuxARM_tarball)
        *   [1.1.1 Install basesystem to a SD card](#Install_basesystem_to_a_SD_card)
        *   [1.1.2 Compile and copy U-Boot bootloader](#Compile_and_copy_U-Boot_bootloader)
        *   [1.1.3 Login / SSH](#Login_.2F_SSH)
*   [2 Orange Pi PC2](#Orange_Pi_PC2)
    *   [2.1 UBoot](#UBoot)
    *   [2.2 Kernel](#Kernel)
*   [3 See also](#See_also)

## Installation

### Using original ArchLinuxARM tarball

This method will install unmodified ArchLinuxARM armv7 basesystem to your Orange Pi One, meaning you'll have the latest mainline kernel running. It will probably also work on other H3 Orange Pis with mainline support.

#### Install basesystem to a SD card

Zero the beginning of the SD card:

```
dd if=/dev/zero of=/dev/sdX bs=1M count=8

```

Use [fdisk](/index.php/Fdisk "Fdisk") to partition the SD card, and [format](/index.php/File_systems "File systems") it with `mkfs.ext4 -O ^metadata_csum,^64bit /dev/sdX1`.

Mount the ext4 filesystem, replacing `sda1` with the formatted partition:

```
# mkdir mnt
# mount /dev/*sda1* mnt

```

Download and extract the root filesystem:

```
# wget [http://archlinuxarm.org/os/ArchLinuxARM-armv7-latest.tar.gz](http://archlinuxarm.org/os/ArchLinuxARM-armv7-latest.tar.gz)
# bsdtar -xpf ArchLinuxARM-armv7-latest.tar.gz -C mnt/

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
# mkimage -A arm -O linux -T script -C none -a 0 -e 0 -n "Orange Pi One boot script" -d boot.cmd mnt/boot/boot.scr
# umount mnt

```

#### Compile and copy U-Boot bootloader

The next step is creating a u-boot image. Make sure you have [arm-none-eabi-gcc](https://www.archlinux.org/packages/?name=arm-none-eabi-gcc), [dtc](https://www.archlinux.org/packages/?name=dtc), [git](https://www.archlinux.org/packages/?name=git) and [uboot-tools](https://www.archlinux.org/packages/?name=uboot-tools) installed on your system. If you compile for a different H3 Orange Pi than the One, replace orangepi_one_config accordingly. Then clone the u-boot source code and compile a Orange Pi image:

```
$ git clone --depth 1 [git://git.denx.de/u-boot.git](git://git.denx.de/u-boot.git)
$ cd u-boot
$ make -j4 ARCH=arm CROSS_COMPILE=arm-none-eabi- orangepi_one_defconfig
$ make -j4 ARCH=arm CROSS_COMPILE=arm-none-eabi-

```

If everything went fine you should have an U-Boot image: u-boot-sunxi-with-spl.bin. Now dd the image to your sdcard, where /dev/sdX is your sdcard.

```
# dd if=u-boot-sunxi-with-spl.bin of=/dev/sdX bs=1024 seek=8

```

#### Login / SSH

SSH login for root is disabled by default. Login with the default user account and use [su](/index.php/Su "Su").

| Type | Username | Password |
| Root | `root` | `root` |
| User | `alarm` | `alarm` |

## Orange Pi PC2

Allwinner H5 @ 1.20Ghz 64bit system AArch64

[General information about the device](http://linux-sunxi.org/Xunlong_Orange_Pi_PC_2)

**Note:** The device is also not officially supported by the ALARM project

Follow general installation instruction above. Differences:

### UBoot

```
# git clone [https://github.com/ARM-software/arm-trusted-firmware.git](https://github.com/ARM-software/arm-trusted-firmware.git)
# git clone -b v2017.07 [git://git.denx.de/u-boot.git](git://git.denx.de/u-boot.git)
# cd arm-trusted-firmware
# make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j4 PLAT=sun50iw1p1 DEBUG=1 bl31
# cp build/sun50iw1p1/debug/bl31.bin ../u-boot/
# cd ../u-boot
# make ARCH=arm CROSS_COMPILE=aarch64-linux-gnu- -j4 orangepi_pc2_defconfig
# make ARCH=arm CROSS_COMPILE=aarch64-linux-gnu- -j4
# cat spl/sunxi-spl.bin u-boot.itb > u-boot-sunxi-with-spl.bin
# dd if=u-boot-sunxi-with-spl.bin of=/dev/sdX bs=8k seek=1

```

### Kernel

For AARCH64 you'll need another rootfs

```
# wget [http://archlinuxarm.org/os/ArchLinuxARM-aarch64-latest.tar.gz](http://archlinuxarm.org/os/ArchLinuxARM-aarch64-latest.tar.gz)
# bsdtar -xpf ArchLinuxARM-aarch64-latest.tar.gz -C mnt/

```

You need to compile your own kernel. Download latest mainline release from:

```
[https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/)

```

or fetch this kernel repository with new patches already included:

```
git clone [https://github.com/megous/linux.git](https://github.com/megous/linux.git)

```

```
# cd linux

```

Here is a basic config file to start with:

```
# wget [https://github.com/armbian/build/raw/master/config/kernel/linux-sunxi-next.config](https://github.com/armbian/build/raw/master/config/kernel/linux-sunxi-next.config) -O .config
# make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j4
# make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- INSTALL_MOD_PATH=/mnt  -j4 modules_install
# cp arch/arm64/boot/Image /mnt/boot
# cp arch/arm64/boot/dts/allwinner/sun50i-h5-orangepi-pc2.dtb /mnt/boot/dtbs/allwinner/sun50i-h5-orangepi-pc2.dtb

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

## See also

*   ["Just another Geek's" blog about installing Linux](https://blog.christophersmart.com/2016/10/23/building-and-booting-upstream-linux-and-u-boot-for-orange-pi-one-arm-board/)