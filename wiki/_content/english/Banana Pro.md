The Banana Pro (also often referred to as Banana Pi Pro) is a SBC from the manufacturer [LeMaker](http://www.lemaker.org/). You can see the specifications [here](http://www.lemaker.org/product-bananapro-specification.html). By now, this article only covers the installation using the [tarball](http://archlinuxarm.org/os/ArchLinuxARM-armv7-latest.tar.gz), which is very similar to the installation of the [Banana Pi](/index.php/Banana_Pi "Banana Pi").

## Contents

*   [1 Information prior to installing](#Information_prior_to_installing)
*   [2 Installation](#Installation)
    *   [2.1 Install base system to a SD card](#Install_base_system_to_a_SD_card)
    *   [2.2 Install base system to a SD card and SATA/USB device](#Install_base_system_to_a_SD_card_and_SATA.2FUSB_device)
    *   [2.3 Login](#Login)
*   [3 See also](#See_also)

## Information prior to installing

This article is very similar to [Banana Pi](/index.php/Banana_Pi "Banana Pi"), though the description there doesn't apply fully to the Banana Pro. Also, users have to be familiar with installing an Arch system ([Partitioning](/index.php/Partitioning "Partitioning"), [formatting](/index.php/File_systems "File systems"), etc.), as this will only cover the installation of the base system. Further configuration won't be covered here.

## Installation

### Install base system to a SD card

Zero the beginning of the SD card (**sdX**):

```
dd if=/dev/zero of=/dev/sdX bs=1M count=8

```

Download the root filesystem and the required boot files (will be saved in your current working directory):

```
# wget [http://archlinuxarm.org/os/ArchLinuxARM-armv7-latest.tar.gz](http://archlinuxarm.org/os/ArchLinuxARM-armv7-latest.tar.gz)                     # base system
# wget [http://pkgbuild.com/~tredaelli/alarm/bananapro/boot/u-boot-sunxi-with-spl.bin](http://pkgbuild.com/~tredaelli/alarm/bananapro/boot/u-boot-sunxi-with-spl.bin)   # Bootloader for Banana Pro
# wget [http://pkgbuild.com/~tredaelli/alarm/bananapro/boot/boot.scr](http://pkgbuild.com/~tredaelli/alarm/bananapro/boot/boot.scr)                    # Also a required boot file for the Banana Pro

```

Use `fdisk` to partition the SD card and format it with `mkfs.ext4`.

```
# fdisk /dev/sdX
# mkfs.ext4 /dev/sdXn

```

Create a mountpoint if needed and mount the root partition, replacing `sdXn` with the root partition on your SD card, on which you want to have Arch Linux installed. (e.g. `sdc1`)

```
# mkdir [mountpoint]
# mount /dev/sdXn [mountpoint]

```

Extract the root file system to the root partition of your SD card:

```
# bsdtar -xpf ArchLinuxARM-armv7-latest.tar.gz -C [mountpoint]                         # extract to SD card

```

Copy the bootloader (`u-boot-sunxi-with-spl.bin`) and boot file:

```
# dd if=/path/to/u-boot-sunxi-with-spl.bin of=/dev/sdX bs=1024 seek=8                  # install the bootloader
# cp /path/to/boot.scr [mountpoint]/boot
# umount [mountpoint]

```

**Note:** It is very important to `dd` the .bin file in the first place (before copying the .scr file)! Doing otherwise may lead to denial of boot.

After inserting the SD card into the slot on the bottom, your Banana Pro should boot properly and prompt you with a console.

### Install base system to a SD card and SATA/USB device

**Note:** Do not partition your SD card in this procedure.

This part covers the procedure of installing your system on a SATA/USB device. The only required part of the system, that has to be on the SD card, is the bootloader. The other parts may reside on an external device. In the following, **sdX** represents your **SD card** and *sdY* represents the *SATA/USB device*.

Zero the beginning of the SD card:

```
dd if=/dev/zero of=/dev/**sdX** bs=1M count=8

```

Download the required files if you haven't done it already:

```
# wget [http://archlinuxarm.org/os/ArchLinuxARM-armv7-latest.tar.gz](http://archlinuxarm.org/os/ArchLinuxARM-armv7-latest.tar.gz)                     # base system
# wget [http://pkgbuild.com/~tredaelli/alarm/bananapro/boot/u-boot-sunxi-with-spl.bin](http://pkgbuild.com/~tredaelli/alarm/bananapro/boot/u-boot-sunxi-with-spl.bin)   # Bootloader for Banana Pro
# wget [http://pkgbuild.com/~tredaelli/alarm/bananapro/boot/boot.scr](http://pkgbuild.com/~tredaelli/alarm/bananapro/boot/boot.scr)                    # Also a required boot file

```

Install the bootloader to the (whole) SD card:

```
# dd if=/path/to/u-boot-sunxi-with-spl.bin of=/dev/**sdX** bs=1024 seek=8                       # Installs only the bootloader to your SD card. You can eject the SD card now if you want to.

```

Use `fdisk` to partition the *SATA/USB device* and format it with `mkfs.ext4`.

```
# fdisk /dev/*sdY*
# mkfs.ext4 /dev/*sdYn*

```

Create a mountpoint if needed and mount the root partition. Again, `*sdYn*` is the partition, on which you want to have Arch Linux installed later on.

```
# mount /dev/*sdYn* [mountpoint]                                                         # Mount the root partition
# bsdtar -xpf ArchLinuxARM-armv7-latest.tar.gz -C [mountpoint]                         # Extract the root filesystem to your root partition
# cp /path/to/boot.scr [mountpoint]/boot
# umount [mountpoint]

```

This whole guide is inspired by the installation procedure for the [OlinuXino Lime2](https://archlinuxarm.org/platforms/armv7/allwinner/a20-olinuxino-lime2) with a few adaptations.

### Login

These are the default logins for a new installation.

| Type | Username | Password |
| Root | `root` | `root` |
| User | `alarm` | `alarm` |

## See also

[Banana Pro FAQ](http://wiki.lemaker.org/BananaPro/Pi:FAQs)