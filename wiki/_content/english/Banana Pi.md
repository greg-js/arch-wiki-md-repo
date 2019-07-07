The Banana Pi was originally an open-source single-board computer capable of running multiple forms of Linux, Android and even prebuilt Raspberry Pi images. It is now the name of a small series of boards made available by the Banana Pi open source project. More info about their project and product line is available at [their website](http://www.banana-pi.org/).

The Banana Pi M1, M2 (most variants included), and M3 are all minimalist computers built for the [ARMv7-A architecture](https://en.wikipedia.org/wiki/ARMv7-A "wikipedia:ARMv7-A"). With their [Allwinner](https://en.wikipedia.org/wiki/Allwinner_Technology "wikipedia:Allwinner Technology") SoCs, these Banana Pi boards usually run the well documented Sunxi Linux kernel, so for any hardware or kernel related tasks you should [take a look at the Sunxi Wiki.](https://linux-sunxi.org/Main_Page)

**Note:** The device is not officially supported by the ALARM project, i.e. please refrain from submitting patches, feature requests or bug reports for it.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Article preface](#Article_preface)
*   [2 Installation](#Installation)
    *   [2.1 Install base system to a SD card](#Install_base_system_to_a_SD_card)
    *   [2.2 Compile and copy U-Boot boot loader](#Compile_and_copy_U-Boot_boot_loader)
    *   [2.3 Login / SSH](#Login_/_SSH)
*   [3 X.org driver](#X.org_driver)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Ethernet not working](#Ethernet_not_working)
    *   [4.2 Display turns off after idle and does not turn on again](#Display_turns_off_after_idle_and_does_not_turn_on_again)
*   [5 See also](#See_also)

## Article preface

This article is strongly based on the [Raspberry Pi](https://en.wikipedia.org/wiki/Raspberry_Pi "wikipedia:Raspberry Pi"). Moreover this article is not meant to be an exhaustive setup guide and assumes that the reader has setup an Arch system before.

## Installation

This method will install unmodified ArchLinuxARM armv7 base system to your Banana Pi, meaning you'll have the latest mainline kernel from the [ALARM Project](https://archlinuxarm.org/) even thought the Banana Pi series is not officially supported.

### Install base system to a SD card

Zero the beginning of the SD card replacing `*sdX*` with the drive's block device:

```
# dd if=/dev/zero of=/dev/*sdX* bs=1M count=8

```

Use [fdisk](/index.php/Fdisk "Fdisk") to partition the SD card with a [MBR](/index.php/MBR "MBR") partition table, and [format](/index.php/File_systems "File systems") the root partition, replacing `*sdX1*` with the root partition:

```
# mkfs.ext4 -O ^metadata_csum,^64bit /dev/*sdX1*

```

Mount the [Ext4](/index.php/Ext4 "Ext4") file system:

```
# mkdir mnt
# mount /dev/*sdX1* mnt

```

Download ArchLinuxARM with [wget](https://www.archlinux.org/packages/?name=wget):

```
# wget [http://archlinuxarm.org/os/ArchLinuxARM-armv7-latest.tar.gz](http://archlinuxarm.org/os/ArchLinuxARM-armv7-latest.tar.gz)

```

Extract the root file system:

```
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

Compile it and write it to the SD-card using the package [uboot-tools](https://www.archlinux.org/packages/?name=uboot-tools).

```
# mkimage -A arm -O linux -T script -C none -a 0 -e 0 -n "BananPI boot script" -d boot.cmd mnt/boot/boot.scr
# umount mnt

```

### Compile and copy U-Boot boot loader

The next step is creating a u-boot image. Make sure you have [arm-none-eabi-gcc](https://www.archlinux.org/packages/?name=arm-none-eabi-gcc), [dtc](https://www.archlinux.org/packages/?name=dtc), [git](https://www.archlinux.org/packages/?name=git), [swig](https://www.archlinux.org/packages/?name=swig) and [uboot-tools](https://www.archlinux.org/packages/?name=uboot-tools) installed on your system. Then clone the u-boot source code and compile an image, making sure to replace *defconfig* with the config of your specific board:

<caption>Config List</caption>
| Board | Defconfig |
| M1 | `Bananapi_defconfig` |
| M1+ | `bananapi_m1_plus_defconfig` |
| M2 | `Sinovoip_BPI_M2_defconfig` |
| M2 Berry | `bananapi_m2_berry_defconfig` |
| M2PLUS-H3 | `bananapi_m2_plus_h3_defconfig` |
| M2PLUS-H5 | `bananapi_m2_plus_h5_defconfig` |
| M2 Ultra | `Bananapi_M2_Ultra_defconfig` |
| M2 Magic | `Bananapi_m2m_defconfig` |
| M2 Zero | `bananapi_m2_zero_defconfig` |
| M3 | `Sinovoip_BPI_M3_defconfig` |

**Note:** The M2 Ultra and Magic boards have device tree files available. They, and other defconfigs, can be found at the [U-Boot GitLab](https://gitlab.denx.de/u-boot/u-boot/).

```
$ git clone [git://git.denx.de/u-boot.git](git://git.denx.de/u-boot.git)
$ cd u-boot
$ make -j4 ARCH=arm CROSS_COMPILE=arm-none-eabi- *defconfig*
$ make -j4 ARCH=arm CROSS_COMPILE=arm-none-eabi-

```

In case the following error shows up during the compilation:

```
 Traceback (most recent call last):
 File "./tools/binman/binman", line 31, in <module>
   import control
 File "/u00/thomas/Downloads/bananapi/u-boot/tools/binman/control.py", line 15, in <module>
   import fdt
 File "/u00/thomas/Downloads/bananapi/u-boot/tools/binman/../dtoc/fdt.py", line 13, in <module>
   import libfdt
 File "tools/libfdt.py", line 17, in <module>
   _libfdt = swig_import_helper()
 File "tools/libfdt.py", line 16, in swig_import_helper
   return importlib.import_module('_libfdt')
 File "/usr/lib/python2.7/importlib/__init__.py", line 37, in import_module
   __import__(name)
 ImportError: No module named _libfdt
 make: *** [Makefile:1149: u-boot-sunxi-with-spl.bin] Fehler 1

```

Make sure the python2 interpreter is used. To force that you could use for example:

```
$ virtualenv -p /usr/bin/python2.7 my_uboot
$ source my_uboot/bin/activate

```

Then compile again as above.

If everything went fine you should have an U-Boot image: u-boot-sunxi-with-spl.bin. Now dd the image to your SD Card, where ``/dev/sdX`` is your SD Card.

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

*   [Banana-Pi Forum](http://forum.banana-pi.org/)
*   [Banana-Pi Wiki](https://wiki.banana-pi.org/Main_Page)
*   [Banana-Pi GitBook](https://legacy.gitbook.com/@bananapi/)