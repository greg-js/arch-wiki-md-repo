From the [manufacturer](http://www.lemaker.org/):

	Banana Pi is an open-source single-board computer. It can run Android 4.4, Ubuntu, Debian, Rasberry Pi Image, as well as the Cubieboard Image. It uses the AllWinner A20 SoC, and has 1GB DDR3 SDRAM

BananaPi is a minimalist computer built for the [ARMv7-A architecture](https://en.wikipedia.org/wiki/ARMv7-A "wikipedia:ARMv7-A"). [More information about this project](http://www.bananapi.org/) and [technical specification](http://www.bananapi.org/p/product.html).

With its Allwinner SoC, a Banana board usually runs the well documented Sunxi Linux kernel. So for any hardware or kernel related tasks, you should [take a look at the Sunxi Wiki](https://linux-sunxi.org/Main_Page) as well.

**Note:** The device is not officially supported by the ALARM project, i.e. please refrain from submitting patches, feature requests or bug reports for it.

## Contents

*   [1 Article preface](#Article_preface)
*   [2 Installation](#Installation)
    *   [2.1 Install basesystem to a SD card](#Install_basesystem_to_a_SD_card)
    *   [2.2 Compile and copy U-Boot bootloader](#Compile_and_copy_U-Boot_bootloader)
    *   [2.3 Login / SSH](#Login_.2F_SSH)
*   [3 X.org driver](#X.org_driver)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Ethernet not working](#Ethernet_not_working)
    *   [4.2 Display turns off after idle and does not turn on again](#Display_turns_off_after_idle_and_does_not_turn_on_again)
*   [5 See also](#See_also)

## Article preface

This article is strongly based on [Raspberry Pi](/index.php/Raspberry_Pi "Raspberry Pi"). Moreover this article is not meant to be an exhaustive setup guide and assumes that the reader has setup an Arch system before.

## Installation

This method will install unmodified ArchLinuxARM armv7 basesystem to your Banana Pi, meaning you'll have the latest mainline kernel running.

### Install basesystem to a SD card

Zero the beginning of the SD card:

```
# dd if=/dev/zero of=/dev/sdX bs=1M count=8

```

Use [fdisk](/index.php/Fdisk "Fdisk") to partition the SD card, and [format](/index.php/File_systems "File systems") it with `mkfs.ext4 -O ^metadata_csum,^64bit /dev/sdX1`.

Mount the ext4 filesystem, replacing `sda1` with the formatted partition:

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
# mkimage -A arm -O linux -T script -C none -a 0 -e 0 -n "BananPI boot script" -d boot.cmd /mnt/boot/boot.scr
# umount /mnt

```

### Compile and copy U-Boot bootloader

The next step is creating a u-boot image. Make sure you have [arm-none-eabi-gcc](https://www.archlinux.org/packages/?name=arm-none-eabi-gcc), [dtc](https://www.archlinux.org/packages/?name=dtc), [git](https://www.archlinux.org/packages/?name=git) and [uboot-tools](https://www.archlinux.org/packages/?name=uboot-tools) installed on your system. Then clone the u-boot source code and compile a Banana Pi image:

```
$ git clone [git://git.denx.de/u-boot.git](git://git.denx.de/u-boot.git)
$ cd u-boot
$ make -j4 ARCH=arm CROSS_COMPILE=arm-none-eabi- Bananapi_defconfig 
$ make -j4 ARCH=arm CROSS_COMPILE=arm-none-eabi-

```

If everything went fine you should have an U-Boot image: u-boot-sunxi-with-spl.bin. Now dd the image to your sdcard, where /dev/sdX is your sdcard.

```
# dd if=u-boot-sunxi-with-spl.bin of=/dev/sdX bs=1024 seek=8

```

### Login / SSH

SSH login for root is disabled by default. Login with the default user account and use [su](/index.php/Su "Su").

| Type | Username | Password |
| Root | `root` | `root` |
| User | `alarm` | `alarm` |

## X.org driver

The X.org driver for Banana Pi can be installed with the [xf86-video-fbdev](https://www.archlinux.org/packages/?name=xf86-video-fbdev) package.

## Troubleshooting

### Ethernet not working

In some cases, the Gbit ethernet connection is unstable or not working properly. It might help to limit the link speed to 100 Mbps using [ethtool](https://www.archlinux.org/packages/?name=ethtool):

```
ethtool -s eth0 speed 100 duplex half autoneg off

```

### Display turns off after idle and does not turn on again

If you also have an issue with the display turning off after some idle time and not turning on again, you might want to disable [DPMS](/index.php/DPMS "DPMS"). Therefore add these X11 arguments to the proper configuration of your display manager.

```
-s 0 -dpms

```

For example, if you use [SLiM](/index.php/SLiM "SLiM"), you would modify in your `/etc/slim.conf`:

```
xserver_arguments -nolisten tcp vt07 -s 0 -dpms 

```

If for some reason the display still keeps turning off, e.g. when restarting your receiving device, you can turn it on again, by temporary change the resolution:

```
# echo "D:1280x720p-60" > /sys/class/graphics/fb0/mode
# echo "D:1920x1080p-60" > /sys/class/graphics/fb0/mode

```

## See also

*   [Manufacturer device FAQ](http://wiki.lemaker.org/BananaPro/Pi:FAQs)
*   [Jelly's blog on installing ALARM](http://vdwaa.nl/archlinux/arm/bananapi/banana-pi-archlinux-arm/)