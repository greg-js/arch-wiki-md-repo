The Banana Pro (also often referred to as Banana Pi Pro) is a SBC from the manufacturer [LeMaker](http://www.lemaker.org/). You can see the specifications [here](http://www.lemaker.org/product-bananapro-specification.html). By now, this article only covers the installation using the [tarball](http://archlinuxarm.org/os/ArchLinuxARM-armv7-latest.tar.gz), which is very similar to the installation of the [Banana Pi](/index.php/Banana_Pi "Banana Pi").

This article is very similar to the [Banana Pi](/index.php/Banana_Pi "Banana Pi"), though the description there doesn't apply fully to the Banana Pro. Also, users have to be familiar with installing an Arch system ([Partitioning](/index.php/Partitioning "Partitioning"), [formatting](/index.php/File_systems "File systems"), etc.), as this will only cover the installation of the base system. Further configuration won't be covered here.

**Note:**

*   The device is not officially supported by the ALARM project, i.e. please refrain from submitting patches, feature requests or bug reports for it.
*   Ensure to install the **root file system on the first partition**, otherwise it will not boot. (e.g. `sda**1**, sdb**1**, ...`).

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Install base system to a SD card](#Install_base_system_to_a_SD_card)
    *   [1.2 Install base system to a SD card and SATA/USB device](#Install_base_system_to_a_SD_card_and_SATA.2FUSB_device)
*   [2 Network](#Network)
    *   [2.1 LAN](#LAN)
    *   [2.2 WLAN](#WLAN)
*   [3 Login](#Login)
*   [4 See also](#See_also)

## Installation

### Install base system to a SD card

Zero the beginning of the SD card (**sdX**):

```
dd if=/dev/zero of=/dev/sdX bs=1M count=8

```

Download the root filesystem, bootloader and the required .scr file (will be saved in your current working directory):

```
# wget [http://archlinuxarm.org/os/ArchLinuxARM-armv7-latest.tar.gz](http://archlinuxarm.org/os/ArchLinuxARM-armv7-latest.tar.gz)
# wget [http://pkgbuild.com/~tredaelli/alarm/bananapro/boot/u-boot-sunxi-with-spl.bin](http://pkgbuild.com/~tredaelli/alarm/bananapro/boot/u-boot-sunxi-with-spl.bin)
# wget [http://pkgbuild.com/~tredaelli/alarm/bananapro/boot/boot.scr](http://pkgbuild.com/~tredaelli/alarm/bananapro/boot/boot.scr)

```

Use *fdisk* to partition the SD card:

```
# fdisk /dev/sdX

```

and format it:

```
# mkfs.ext4 -O ^metadata_csum,^64bit /dev/sdX1

```

Create a mountpoint if needed and mount the root partition, on which Arch Linux will be installed later on. Replace `sdX` with the device name of your SD card. (e.g. `sdc`)

```
# mkdir <mountpoint>
# mount /dev/sdX1 <mountpoint>

```

Extract the root file system to the root partition of your SD card:

```
# bsdtar -xpf ArchLinuxARM-armv7-latest.tar.gz -C <mountpoint>

```

Copy the bootloader (`u-boot-sunxi-with-spl.bin`) and boot file:

```
# dd if=/path/to/u-boot-sunxi-with-spl.bin of=/dev/sdX bs=1024 seek=8
# cp /path/to/boot.scr <mountpoint>/boot
# umount <mountpoint>

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

Download the required files if you have not done it already:

```
# wget [http://archlinuxarm.org/os/ArchLinuxARM-armv7-latest.tar.gz](http://archlinuxarm.org/os/ArchLinuxARM-armv7-latest.tar.gz)
# wget [http://pkgbuild.com/~tredaelli/alarm/bananapro/boot/u-boot-sunxi-with-spl.bin](http://pkgbuild.com/~tredaelli/alarm/bananapro/boot/u-boot-sunxi-with-spl.bin)
# wget [http://pkgbuild.com/~tredaelli/alarm/bananapro/boot/boot.scr](http://pkgbuild.com/~tredaelli/alarm/bananapro/boot/boot.scr)

```

Install the bootloader to the (whole) SD card:

```
# dd if=/path/to/u-boot-sunxi-with-spl.bin of=/dev/**sdX** bs=1024 seek=8                       

```

You can eject the SD card now, if you want.

Use *fdisk* to partition the *SATA/USB device*:

```
# fdisk /dev/*sdY*

```

and format it:

```
# mkfs.ext4 -O ^metadata_csum,^64bit /dev/*sdY1*

```

Create a mountpoint if needed and mount the root partition. Again, `*sdY1*` is the root partition of the *SATA/USB device* (`*sdY*`), on which Arch Linux will be installed.

```
# mount /dev/*sdY1* <mountpoint>
# bsdtar -xpf ArchLinuxARM-armv7-latest.tar.gz -C <mountpoint>
# cp /path/to/boot.scr <mountpoint>/boot
# umount <mountpoint>

```

This whole guide is inspired by the installation procedure for the [OlinuXino Lime2](https://archlinuxarm.org/platforms/armv7/allwinner/a20-olinuxino-lime2) with a few adaptations.

## Network

The network is by default configured by [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd").

### LAN

Ethernet will work out of the box when connected to a DHCP server.

### WLAN

To become wlan working you have to install the needed firmware and [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") which uses the kernel module `brcmfmac`.

```
# pacman -S firmware-ap6210 wpa_supplicant

```

## Login

These are the default logins for a new installation.

| Type | Username | Password |
| Root | `root` | `root` |
| User | `alarm` | `alarm` |

The root account is locked by default for SSH login. Login as normal user and use `su -` to become root.

## See also

*   [Banana Pro FAQ](http://wiki.lemaker.org/BananaPro/Pi:FAQs)