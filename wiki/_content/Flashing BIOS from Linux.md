# Flashing BIOS from Linux

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This article aims on providing information on flashing your system BIOS under Linux. Most manufacturers provide a Windows executable or a BIOS executable that can only be run under Windows. However, there are a few utilities, that allow you to upgrade your system BIOS under Linux.

**Warning:** Flashing motherboard BIOS is a dangerous activity that can render your motherboard inoperable! While the author of this article has successfully run this procedure many times, your mileage may vary. Be careful! You may want to consider updating [microcode](/index.php/Microcode "Microcode") instead if it is supported by your system.

## Contents

*   [1 Introduction](#Introduction)
*   [2 BiosDisk](#BiosDisk)
    *   [2.1 Installation](#Installation)
    *   [2.2 Usage](#Usage)
*   [3 Flashrom](#Flashrom)
    *   [3.1 Installation](#Installation_2)
    *   [3.2 Usage](#Usage_2)
*   [4 FreeDOS](#FreeDOS)
    *   [4.1 Unetbootin](#Unetbootin)
    *   [4.2 Gentoo](#Gentoo)
    *   [4.3 Prebuilt images](#Prebuilt_images)
    *   [4.4 Images that are too large for a floppy](#Images_that_are_too_large_for_a_floppy)
    *   [4.5 Usage](#Usage_3)
*   [5 Geteltorito.pl](#Geteltorito.pl)
    *   [5.1 Installation](#Installation_3)
    *   [5.2 Usage](#Usage_4)

## Introduction

There are a few ways that you can use to flash the system BIOS under Linux.

## BiosDisk

[BiosDisk](http://linux.dell.com/git/biosdisk.git) BiosDisk simplifies the process of flashing your system BIOS under Linux

### Installation

[Install](/index.php/Install "Install") the [biosdisk-git](https://aur.archlinux.org/packages/biosdisk-git/)<sup><small>AUR</small></sup>.

### Usage

To use the biosdisk utility to create a BIOS flash image, first download the latest raw BIOS image for your system from your manufacturer's website. Make sure however, that you always get the BIOS executable and NOT the Windows executable. You then have one of several options: create a floppy, create a dd floppy image, create a user-installable distribution-specific package (e.g. RPM), or actually install the image for your bootloader.

*   The mkfloppy action will create the biosdisk image and write it directly to a floppy disk. Usage is the following:

```
    biosdisk mkfloppy [-o option] [-d device] [-k baseimage] /path/to/.exe 

```

*   The mkimage action will create a floppy image on the user's hard drive. Usage is the following:

```
    biosdisk mkimage [-o option] [-i destination] [-k baseimage] /path/to/.exe 

```

*   The mkpkg action will create the floppy image, and use it to create a user-installable package specific to the distribution (example: RPM). When the package is installed, it will use the distribution's built-in tools to update the system's bootloader so that the user can boot to the image from the hard drive to flash the BIOS, without needing a floppy drive. Currently only Red Hat/Fedora RPM packages are supported. Usage is as follows:

```
    biosdisk mkpkg [-o option] [--install] [--distro=] [--name=] [--version=] [--release=] /path/to/{.exe | .img}

```

*   The install action will create the biosdisk image, copy the image file to /boot, and then update the bootloader with an entry for the image. Then all the user has to do is boot the system and select the image to flash the BIOS; this will load the biosdisk image directly from the hard drive and flash the BIOS.

```
    biosdisk install [-o option] [--name=] /path/to/{.exe | .img}

```

## Flashrom

[Flashrom](http://www.flashrom.org/Flashrom)is a utility for identifying, reading, writing, verifying and erasing flash chips. It is designed to flash BIOS/EFI/coreboot/firmware/optionROM images on mainboards, network/graphics/storage controller cards, and various programmer devices.

### Installation

[Install](/index.php/Pacman "Pacman") the [flashrom](https://www.archlinux.org/packages/?name=flashrom) or [flashrom-svn](https://aur.archlinux.org/packages/flashrom-svn/)<sup><small>AUR</small></sup>.

### Usage

Find out if your motherboard and chipset (internal) is supported by flashrom at this website. [Supported Hardware](http://www.flashrom.org/Supported_hardware) You can also find out if your hardware is supported by issuing the following command

```
# flashrom --programmer internal

```

The above command will tell you your motherboard and chipset. You can then find out if yours is supported by issuing this command:

```
# flashrom --programmer internal -L | grep CHIPNAMEfrompreviouscommand

```

On modern mainboards you probably get more than one rom chip listed. You have to select the chipname you get from the upper command. Them you use the `-c` option to select which rom is affected by the command

```
# flashrom --programmer internal -c "CHIPNAME" -r backup_CHIPNAME.bin

```

Write and verify the new BIOS image (proprietary or Coreboot) on the ROM chip:

```
# flashrom --programmer internal internal -c "CHIPNAME" -w newbios.bin

```

If you want to flash other flash chips on your mainboard, you will find all options with

```
# flashrom

```

## FreeDOS

[FreeDOS](http://www.freedos.org/) a free DOS-compatible operating system, is up to the challenge, no need for proprietary DOS versions. So, all you need is a bootable floppy disk image with FreeDOS kernel on it.

### Unetbootin

By far the easiest way to make a bootable FreeDOS USB Stick is using [unetbootin](https://www.archlinux.org/packages/?name=unetbootin), available in the [Official repositories](/index.php/Official_repositories "Official repositories").

You should format a pendrive with FAT16 and flag it as "boot" (you may do this through a GUI with [gparted](https://www.archlinux.org/packages/?name=gparted), [qtparted](https://aur.archlinux.org/packages/qtparted/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/qtparted)]</sup> or [partitionmanager](https://www.archlinux.org/packages/?name=partitionmanager)). Then, after mounting the flash drive, select under distribution **FreeDOS** and your mounted stick. The app will automatically download the image for you and copy it to the drive. Finally, you may copy everything you want to flash there (BIOS, firmwares, etc).

**Warning:** Unetbootin may not function properly on some Lenovo systems. It may be necessary to create the bootable stick on a different device. See [here](http://reboot.pro/topic/9849-blinking-cursor-at-boot/).

### Gentoo

Check out [FreeDOS Flash Drive](https://wiki.gentoo.org/wiki/BIOS_Update#FreeDOS_environment) on the Gentoo Wiki if you want to create a bootable FreeDOS Flash drive.

### Prebuilt images

Yet another simple solution: [FreeDOS prebuilt bootable USB flash drive image by Christian Taube](http://chtaube.eu/computers/freedos/bootable-usb/)

### Images that are too large for a floppy

If your flash image is too large for a floppy, go to the [FreeDos bootdisk website](http://www.fdos.org/bootdisks/), and download the 10Mb hard-disk image. This image is a full disk image, including partitions, so adding your flash utility will be a little trickier:

First find the first partition (at time of writing, the first partition starts at block 63; this means that the partitions starts at offset <tt>512 * 63 = 32256</tt>). You can either use:

```
# file -sk _<image-file>_ | sed -r 's/.*startsector ([0-9]+).*/\1/'
**63**

```

Or:

```
# fdisk -l _<image-file>_
…
Units = sectors of 1 * **512** = 512 bytes
…
      Device  Boot  Start    End  Blocks  Id  System
              *        **63**  19151   9544+   1  FAT12

```

Now you can mount the image:

```
# mount -oloop,offset=$((63 * 512)) _<image-file>_ /mnt

```

Then you can copy your flash utility onto the filesystem as normal. Once you're done:

```
# umount /mnt

```

The image can now be copied to a USB stick for booting, or booted as a memdisk as per normal instructions.

### Usage

The OEM Bootdisk version is recommended, as it only includes `kernel` and `command.com` thus leaving more space for the flash utility and new BIOS image. Download and decompress the FreeDOS image:

```
$ wget [http://www.fdos.org/bootdisks/autogen/FDOEM.144.gz](http://www.fdos.org/bootdisks/autogen/FDOEM.144.gz)
$ gunzip FDOEM.144.gz

```

Copy your BIOS flash utility and new BIOS image to the mounted floppy disk image. Load the necessary modules:

```
# modprobe vfat
# modprobe loop

```

`/proc/fileystems` shows if the needed file systems are supported. "loop mount" the floppy disk image to a temporary path:

```
$ mkdir /tmp/floppy
$ mount -t vfat -o loop FDOEM.144 /tmp/floppy

```

If the mount went without errors, copy the BIOS flash utility and new BIOS image to the mounted floppy disk image. You will probably have to unzip the archive you downloaded from your motherboard vendor site, to get to those two files. For example:

```
# unzip 775Dual-VSTA\(2.60\).zip
Archive: 775Dual-VSTA(2.60).zip
 inflating: 75DVSTA2.60
 inflating: ASRflash.exe
# cp 75DVSTA2.60 ASRflash.exe /tmp/floppy

```

Check that the two files were not too big for the floppy:

```
Filesystem           1K-blocks      Used Available Use% Mounted on
/tmp/FDOEM.144
                         1424       990       434  70% /tmp/floppy

```

Unmount the floppy disk image:

```
umount /tmp/floppy

```

The next step is to burn the floppy image to a CD/DVD-RW media, but in a way that it can be booted afterwards. First create a bootable CD image, and then burn it.

```
genisoimage -o bootcd.iso -b FDOEM.144 FDOEM.144
wodim -v bootcd.iso

```

You may alternatively add your image to the [GRUB](/index.php/GRUB "GRUB") menu. Install [syslinux](/index.php/Syslinux "Syslinux") and copy `memdisk` and your image to `/boot`:

```
 cp /usr/lib/syslinux/memdisk /boot
 cp FDOEM.144 /boot/flashbios.img

```

Now add an entry to `/boot/grub/menu.lst`:

```
 title Flash BIOS
 kernel /memdisk
 initrd /flashbios.img

```

Or for GRUB2 in `/boot/grub/grub.cfg`:

```
 menuentry "Flash BIOS" {
 linux16 /boot/memdisk
 initrd16 /boot/flashbios.img
 }

```

Or for syslinux in `/boot/syslinux/syslinux.cfg`:

```
LABEL flashbios
	MENU LABEL Flash BIOS
	LINUX ../memdisk
	INITRD ../fdboot.img

```

Finally reboot your machine, making sure the CD drive is first in the boot sequence, and run the BIOS upgrade procedure when the CD boots. If using the GRUB method, choose the new entry on the list, and it should boot into FreeDOS.

## Geteltorito.pl

This perl script will extract the El Torito boot image. It has worked on Lenovo laptops like X220 X230, and W540\. It may work for other vendors as well.

### Installation

Install the [geteltorito](https://aur.archlinux.org/packages/geteltorito/)<sup><small>AUR</small></sup>.

### Usage

Get the bios update iso from the vendor support site. Run the _geteltorito_ image extraction:

```
# geteltorito.pl -o <image>.img <image>.iso

```

Copy the image to the usb thumbdrive:

```
# dd if=<image>.img of=<destination> bs=512K

```

Reboot and boot from the USB drive, follow vendor directions.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Flashing_BIOS_from_Linux&oldid=411671](https://wiki.archlinux.org/index.php?title=Flashing_BIOS_from_Linux&oldid=411671)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Mainboards and BIOS](/index.php/Category:Mainboards_and_BIOS "Category:Mainboards and BIOS")