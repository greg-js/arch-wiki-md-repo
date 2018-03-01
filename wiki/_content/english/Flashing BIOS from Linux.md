This article aims on providing information on flashing your system BIOS under Linux. Most manufacturers provide a Windows executable or a BIOS executable that can only be run under Windows. However, there are a few utilities, that allow you to upgrade your system BIOS under Linux.

**Warning:** Flashing motherboard BIOS is a dangerous activity that can render your motherboard inoperable! While the author of this article has successfully run this procedure many times, your mileage may vary. Be careful! You may want to consider updating [microcode](/index.php/Microcode "Microcode") instead if it is supported by your system.

**Note:**

*   HP users may download Windows BIOS updater from HP website, extract *.exe file and locate ISO image for burning to a CD. Using CD, upgrade is possible from BIOS menu using 'Firmware Upgrade' without using below tools. See [this](https://h30434.www3.hp.com/t5/Notebook-Operating-System-and-Recovery/How-to-update-BIOS-on-Linux/td-p/4869835) thread for details.
*   For users with Dell computers, Dell recommends Linux users flash their BIOS following information located [here](https://www.dell.com/support/article/us/en/19/sln171755/updating-the-dell-bios-in-linux-and-ubuntu-environments).

## Contents

*   [1 fwupd](#fwupd)
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
    *   [4.4 Using a FreeDOS-provided Disk Image + USB stick](#Using_a_FreeDOS-provided_Disk_Image_.2B_USB_stick)
    *   [4.5 Images that are too large for a floppy](#Images_that_are_too_large_for_a_floppy)
    *   [4.6 Usage](#Usage_3)
*   [5 Bootable optical disk emulation](#Bootable_optical_disk_emulation)
    *   [5.1 Installation](#Installation_3)
    *   [5.2 Usage](#Usage_4)

## fwupd

fwupd is a simple daemon to allow session software to update device firmware on your local machine.

Large vendors including Dell and Logitech use this way to distribute firmware updates to Linux.

fwupd only supports flashing BIOS updates in UEFI mode.

See [fwupd](/index.php/Fwupd "Fwupd") for further information about installation and usage.

## BiosDisk

[BiosDisk](https://github.com/dell/biosdisk) simplifies the process of flashing your system BIOS under Linux.

**Note:** This is only supported on systems when booted in "Legacy mode". In UEFI mode you will need to use a different method.

### Installation

[Install](/index.php/Install "Install") the [biosdisk-git](https://aur.archlinux.org/packages/biosdisk-git/) package.

### Usage

To use the biosdisk utility to create a BIOS flash image, first download the latest raw BIOS image for your system from your manufacturer's website. Make sure however, that you always get the BIOS executable and NOT the Windows executable. You then have one of two options: create a ISO or install the image for your bootloader.

*   The mkimage action will create a ISO image on the user's hard drive. Usage is the following:

```
# biosdisk mkimage [-o option] [-i destination] /path/to/.exe 

```

*   The install action will create the biosdisk image, copy the image file to /boot, and then update the bootloader with an entry for the image. Then all the user has to do is boot the system and select the image to flash the BIOS; this will load the biosdisk image directly from the hard drive and flash the BIOS.

```
# biosdisk install [-o option] [--name=] /path/to/.exe

```

## Flashrom

[Flashrom](http://www.flashrom.org/Flashrom) is a utility for identifying, reading, writing, verifying and erasing flash chips. It is designed to flash BIOS/EFI/coreboot/firmware/optionROM images on mainboards, network/graphics/storage controller cards, and various programmer devices.

**Warning:** If you have a laptop/notebook/netbook, please do NOT try flashrom because interactions with the EC on these machines might crash your machine during flashing. flashrom tries to detect if a machine is a laptop, but not all laptops follow the standard, so this is not 100% reliable.[[1]](https://www.flashrom.org/Board_Testing_HOWTO)

### Installation

[Install](/index.php/Install "Install") the [flashrom](https://www.archlinux.org/packages/?name=flashrom) or [flashrom-git](https://aur.archlinux.org/packages/flashrom-git/) package.

### Usage

Find out if your motherboard and chipset (internal) is supported by flashrom at this website. [Supported Hardware](http://www.flashrom.org/Supported_hardware) You can also find out if your hardware is supported by issuing the following command

```
# flashrom --programmer internal

```

The above command will tell you your motherboard and chipset. You can then find out if yours is supported by issuing this command:

```
# flashrom --programmer internal -L | grep CHIPNAMEfrompreviouscommand

```

On modern mainboards you probably get more than one rom chip listed. You have to select the chipname you get from the upper command. Then you use the `-c` option to select which rom is affected by the command

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

**Note:** With Linux kernel versions greater than 4.4, `CONFIG_IO_STRICT_DEVMEM` a new kernel security measure can make flashrom stop working, in that case you can try adding `iomem=relaxed` to your kernel parameters. [FAQ](https://www.flashrom.org/FAQ).

## FreeDOS

[FreeDOS](http://www.freedos.org/) a free DOS-compatible operating system, is up to the challenge, no need for proprietary DOS versions. So, all you need is a bootable floppy disk image with FreeDOS kernel on it.

### Unetbootin

By far the easiest way to make a bootable FreeDOS USB Stick is using [unetbootin](https://aur.archlinux.org/packages/unetbootin/).

You should format a pendrive with FAT16 and flag it as "boot" (you may do this through a GUI with [gparted](https://www.archlinux.org/packages/?name=gparted) or [partitionmanager](https://www.archlinux.org/packages/?name=partitionmanager)). Then, after mounting the flash drive, select under distribution **FreeDOS** and your mounted stick. The app will automatically download the image for you and copy it to the drive. Finally, you may copy everything you want to flash there (BIOS, firmwares, etc).

**Warning:** Unetbootin may not function properly on some Lenovo systems. It may be necessary to create the bootable stick on a different device. See [here](http://reboot.pro/topic/9849-blinking-cursor-at-boot/).

### Gentoo

Check out [FreeDOS Flash Drive](https://wiki.gentoo.org/wiki/BIOS_Update#FreeDOS_environment "gentoo:BIOS Update") on the Gentoo Wiki if you want to create a bootable FreeDOS Flash drive.

### Prebuilt images

Yet another simple solution: [FreeDOS prebuilt bootable USB flash drive image by Christian Taube](http://chtaube.eu/computers/freedos/bootable-usb/)

### Using a FreeDOS-provided Disk Image + USB stick

As of writing (2017-07-11), [unetbootin](https://aur.archlinux.org/packages/unetbootin/) doesn't support versions of FreeDOS more recent than 1.0 (current version is 1.2). The following procedure worked to upgrade an Inspiron 17-3737 to the A09 BIOS. (Dell offers this as a possibility [on their site](http://www.dell.com/support/article/ca/en/cabsdt1/SLN171755/updating-the-dell-bios-in-linux-and-ubuntu-environments?lang=EN#Creating%20a%20USB%20Bootable%20Storage%20Device))

Some notes before starting:

*   You can check your current BIOS version with [dmidecode](https://www.archlinux.org/packages/?name=dmidecode). You might already be at the latest version.
*   Ensure that your hardware vendor has verified this method works (use of FreeDOS to run BIOS update `.exe`)
*   Laptop users should not attempt this without AC power
*   This is dangerous, and you assume all risk for following this procedure.

Procedure:

1.  Grab the latest USB installer from the [FreeDOS Download Page](http://www.freedos.org/download/)
    *   author note: used the "Full" version on suspicion that it might include more drivers, etc (pure speculation)
2.  Extract the archive, you get a *.img* file
3.  Determine which of `/dev/sdX` is your USB stick (use `fdisk -l`)
4.  Write the image directly to the block device:
    *   `dd if=FD12FULL.img of=/dev/sdX status=progress` (where `X` is the letter representing your USB stick as a block device, don't write the image to a partition)
5.  Double-check that the image copying worked:
    *   `fdisk -l` (you should see a single partition on a DOS disk with the bootable ("boot") flag set)
6.  Mount the partition, and copy over the *.exe* used to update your firmware
    *   Stay on the safe side and limit the filename to 8 characters (without extension), upper case
    *   Ensure that you verified any checksums provided by your hardware vendor
7.  Unmount and reboot. Do whatever is needed to boot from the USB drive

Now you will find yourself in the FreeDOS live installation environment.

1.  Select your language
2.  You will be prompted to install FreeDOS
    *   Select "No - Return to DOS"
3.  You should see a prompt (`C:\>`)
4.  Run `dir /w` and verify that your firmware upgrade tool is present
5.  Run the executable
    *   author note: in the case of the Dell tool, the machine displayed a spash screen and then rebooted. Upon reboot, it started the firmware upgrade automatically, and ran for about 2 minutes with the fan at full speed)
6.  Once the process specific to your vendor completes, optionally verify through the BIOS setup screen, as well as by running [dmidecode](https://www.archlinux.org/packages/?name=dmidecode) when you're back in linux

### Images that are too large for a floppy

If your flash image is too large for a floppy, go to the [FreeDos bootdisk website](http://www.fdos.org/bootdisks/), and download the 10Mb hard-disk image. This image is a full disk image, including partitions, so adding your flash utility will be a little trickier:

First find the first partition (at time of writing, the first partition starts at block 63; this means that the partitions starts at offset `512 * 63 = 32256`). You can either use:

 `# file -sk *<image-file>* | sed -r 's/.*startsector ([0-9]+).*/\1/'` 
```
**63**

```

Or:

 `# fdisk -l *<image-file>*` 
```
…
Units = sectors of 1 * **512** = 512 bytes
…
      Device  Boot  Start    End  Blocks  Id  System
              *        **63**  19151   9544+   1  FAT12
```

Now you can mount the image:

```
# mount -oloop,offset=$((63 * 512)) *<image-file>* /mnt

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

 `# unzip 775Dual-VSTA\(2.60\).zip` 
```
Archive: 775Dual-VSTA(2.60).zip
 inflating: 75DVSTA2.60
 inflating: ASRflash.exe

```

```
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
# umount /tmp/floppy

```

The next step is to burn the floppy image to a CD/DVD-RW media, but in a way that it can be booted afterwards. First create a bootable CD image, and then burn it.

```
# genisoimage -o bootcd.iso -b FDOEM.144 FDOEM.144
# wodim -v bootcd.iso

```

You may alternatively add your image to the [GRUB](/index.php/GRUB "GRUB") menu. Install [syslinux](/index.php/Syslinux "Syslinux") and copy `memdisk` and your image to `/boot`:

```
# cp /usr/lib/syslinux/memdisk /boot
# cp FDOEM.144 /boot/flashbios.img

```

Now add an entry to `/boot/grub/menu.lst`:

 `/boot/grub/menu.lst` 
```
title Flash BIOS
kernel /memdisk
initrd /flashbios.img

```

Or for GRUB2 in `/boot/grub/grub.cfg`:

 `/boot/grub/grub.cfg` 
```
menuentry "Flash BIOS" {
 linux16 /boot/memdisk
 initrd16 /boot/flashbios.img
}

```

Or for syslinux in `/boot/syslinux/syslinux.cfg`:

 `/boot/syslinux/syslinux.cfg` 
```
LABEL flashbios
	MENU LABEL Flash BIOS
	LINUX ../memdisk
	INITRD ../fdboot.img

```

Finally reboot your machine, making sure the CD drive is first in the boot sequence, and run the BIOS upgrade procedure when the CD boots. If using the GRUB method, choose the new entry on the list, and it should boot into FreeDOS.

## Bootable optical disk emulation

The script Geteltorito.pl will extract the [El Torito](https://en.wikipedia.org/wiki/El_Torito_(CD-ROM_standard) boot image. It has worked on Lenovo laptops like X220, X230, X260, W540, T450 and T450s. It may work for other vendors as well.

### Installation

Install the [geteltorito](https://aur.archlinux.org/packages/geteltorito/) package.

### Usage

Get the bios update iso from the vendor support site. Run the *geteltorito* image extraction:

```
$ geteltorito.pl -o <image>.img <image>.iso

```

Copy the image to the usb thumbdrive:

```
# dd if=<image>.img of=<destination> bs=512K

```

Reboot and boot from the USB drive, follow vendor directions.

**Note:** If you get the message "Secure Flash Authentication failed!", it means that some security check did not allow the flash to happen. It can help to go to the BIOS options page "Security" > "UEFI BIOS Update Option" and disable "Secure RollBack Prevention" and enable "Flash BIOS Updating by End-Users". You can set them to what you want after flashing.