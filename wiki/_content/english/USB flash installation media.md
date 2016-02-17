This page discusses various multi-platform methods on how to create an Arch Linux Installer USB drive (also referred to as _"flash drive", "USB stick", "USB key"_, etc) for booting in BIOS and UEFI systems. The result will be a LiveUSB (LiveCD-like) system that can be used for installing Arch Linux, system maintenance or for recovery purposes, and that, because of the nature of [SquashFS](https://en.wikipedia.org/wiki/SquashFS "wikipedia:SquashFS"), will discard all changes once the computer shuts down.

If you would like to run a full install of Arch Linux from a USB drive (i.e. with persistent settings), see [Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key"). If you would like to use your bootable Arch Linux USB stick as a rescue USB, see [Change root](/index.php/Change_root "Change root").

## Contents

*   [1 BIOS and UEFI Bootable USB](#BIOS_and_UEFI_Bootable_USB)
    *   [1.1 Using dd](#Using_dd)
        *   [1.1.1 In GNU/Linux](#In_GNU.2FLinux)
        *   [1.1.2 In Windows](#In_Windows)
            *   [1.1.2.1 Using Rufus](#Using_Rufus)
            *   [1.1.2.2 Using USBwriter](#Using_USBwriter)
            *   [1.1.2.3 Using Cygwin](#Using_Cygwin)
            *   [1.1.2.4 dd for Windows](#dd_for_Windows)
        *   [1.1.3 In Mac OS X](#In_Mac_OS_X)
        *   [1.1.4 How to restore the USB drive](#How_to_restore_the_USB_drive)
    *   [1.2 Using manual formatting](#Using_manual_formatting)
        *   [1.2.1 In GNU/Linux](#In_GNU.2FLinux_2)
        *   [1.2.2 In Windows](#In_Windows_2)
*   [2 Other Methods for BIOS systems](#Other_Methods_for_BIOS_systems)
    *   [2.1 In GNU/Linux](#In_GNU.2FLinux_3)
        *   [2.1.1 Using a multiboot USB drive](#Using_a_multiboot_USB_drive)
        *   [2.1.2 Using UNetbootin](#Using_UNetbootin)
        *   [2.1.3 Using GNOME Disk Utility](#Using_GNOME_Disk_Utility)
        *   [2.1.4 Making an USB-ZIP drive](#Making_an_USB-ZIP_drive)
    *   [2.2 In Windows](#In_Windows_3)
        *   [2.2.1 Win32 Disk Imager](#Win32_Disk_Imager)
        *   [2.2.2 USBWriter for Windows](#USBWriter_for_Windows)
        *   [2.2.3 The Flashnul way](#The_Flashnul_way)
        *   [2.2.4 Loading the installation media from RAM](#Loading_the_installation_media_from_RAM)
            *   [2.2.4.1 Preparing the USB flash drive](#Preparing_the_USB_flash_drive)
            *   [2.2.4.2 Copy the needed files to the USB flash drive](#Copy_the_needed_files_to_the_USB_flash_drive)
            *   [2.2.4.3 Create the configuration file](#Create_the_configuration_file)
            *   [2.2.4.4 Final steps](#Final_steps)
*   [3 Troubleshooting](#Troubleshooting)
*   [4 See Also](#See_Also)

## BIOS and UEFI Bootable USB

### Using dd

**Note:** This method is recommended due to its simplicity. If it does not work, switch to the alternative method [#Using manual formatting](#Using_manual_formatting) below.

**Warning:** This will irrevocably destroy all data on `/dev/sd**x**`.

#### In GNU/Linux

**Tip:** Find out the name of your USB drive with `lsblk`. Make sure that it is **not** mounted.

Run the following command, replacing `/dev/**sdx**` with your drive, e.g. `/dev/sdb`. (do **not** append a partition number, so do **not** use something like `/dev/sdb**1**`):

```
# dd bs=4M if=/path/to/archlinux.iso of=/dev/**sdx** status=progress && sync

```

The option `status=progress` above reports transfer progress every so often. Do **not** miss _sync_ to complete before pulling the USB drive.

#### In Windows

##### Using Rufus

[Rufus](https://rufus.akeo.ie/) is a multi-purpose USB iso writer. Simply select the Arch Linux ISO, the USB drive you want to create the bootable Arch Linux onto and click start.

Since Rufus does not care if the drive is properly formatted or not and provides a GUI it may be the easiest and most robust tool to use.

##### Using USBwriter

This method does not require any workaround and is as straightforward as `dd` under Linux. Just download the Arch Linux ISO, and with local administrator rights use the [USBwriter](http://sourceforge.net/p/usbwriter/wiki/Documentation/) utility to write to your USB flash memory.

##### Using Cygwin

Make sure your [Cygwin](http://www.cygwin.com/) installation contains the `dd` package.

**Tip:** If you do not want to install Cygwin, you can download `dd` for Windows from [here](http://www.chrysocome.net/dd). See the next section for more information.

Place your image file in your home directory:

```
C:\cygwin\home\John\

```

Run cygwin as administrator (required for cygwin to access hardware). To write to your USB drive use the following command:

```
dd if=image.iso of=\\.\**x**: bs=4M

```

where image.iso is the path to the iso image file within the `cygwin` directory and `\\.\**x**:` is your USB flash drive where `**x**` is the windows designated letter, e.g. `\\.\d:`.

On Cygwin 6.0, find out the correct partition with:

```
cat /proc/partitions

```

and write the ISO image with the information from the output. Example:

**Warning:** This will irrevocably delete all files on your USB flash drive, so make sure you do not have any important files on the flash drive before doing this.

```
dd if=image.iso of=/dev/sdb bs=4M

```

##### dd for Windows

**Note:** Some users have an "isolinux.bin missing or corrupt" problem when booting the media with this method.

A GPL licensed dd version for Windows is available at [http://www.chrysocome.net/dd](http://www.chrysocome.net/dd). The advantage of this over Cygwin is a smaller download. Use it as shown in instructions for Cygwin above.

To begin, download the latest version of dd for Windows. Once downloaded, extract the archive's contents into Downloads or elsewhere.

Now, launch your `command prompt` as an administrator. Next, change directory (`cd`) into the Downloads directory.

If your Arch Linux ISO is elsewhere you may need to state the full path, for convenience you may wish to put the Arch Linux ISO into the same folder as the dd executable. The basic format of the command will look like this.

```
# dd if=_archlinux-2015-XX-YY-dual.iso_ od=\\.\_x_: bs=4M

```

**Note:** The Windows drive letters are linked to a partition. To allow selecting the entire disk, _dd for Windows_ provides the `od` parameter, which is used in the commands above. Note however that this parameter is specific to _dd for Windows_ and cannot be found in other implementations of _dd_.

**Warning:** Because the `od` is used, all partitions on the selected disk will be destroyed. Be absolutely sure that you are directing dd to the correct drive before executing.

Simply replace the various null spots (indicated by an "x") with the correct date and correct drive letter. Here is a complete example.

```
# dd if=ISOs\archlinux-2015.01.01-dual.iso od=\\.\d: bs=4M

```

**Note:** Alternatively, replace the drive letter with `\\.\PhysicalDrive_X_`, where `_X_` is the physical drive number (starts from 0). Example: `# dd if=ISOs\archlinux-2015.01.01-dual.iso of=\\.\PhysicalDrive1 bs=4M` 

You can find out the physical drive number by typing `wmic diskdrive list brief` at the command prompt or with `dd --list`

Any Explorer window must be closed or dd will report an error.

#### In Mac OS X

To be able to use `dd` on your USB device on a Mac you have to do some special maneuvers. First of all insert your usb device, OS X will automount it, and in `Terminal.app` run:

```
$ diskutil list

```

Figure out what your USB device is called with `mount` or `sudo dmesg | tail` (e.g. `/dev/disk2`) and unmount the partitions on the device (i.e., /dev/disk2s1) while keeping the device proper (i.e., /dev/disk2):

```
$ diskutil unmountDisk /dev/disk2

```

Now we can continue in accordance with the instructions above (but, if you are using the OS X `dd`, use `/dev/rdisk` instead of `/dev/disk`, and use `bs=1M`. `rdisk` means "raw disk" and is much faster on OS X, and `bs=1M` indicates a 1 MB block size).

 `# dd if=image.iso of=/dev/rdisk2 bs=1M` 

```
20480+0 records in
20480+0 records out
167772160 bytes transferred in 220.016918 secs (762542 bytes/sec)

```

It is probably a good idea to eject your drive before physical removal at this point:

```
$ diskutil eject /dev/disk2

```

#### How to restore the USB drive

Because the ISO image is a hybrid which can either be burned to a disc or directly written to a USB drive, it does not include a standard partition table.

After you install Arch Linux and you are done with the USB drive, you should zero out its first 512 bytes _(meaning the boot code from the MBR and the non-standard partition table)_ if you want to restore it to full capacity:

```
# dd count=1 bs=512 if=/dev/zero of=/dev/sd**x** && sync

```

Then create a new partition table (e.g. "msdos") and filesystem (e.g. EXT4, FAT32) using [gparted](https://www.archlinux.org/packages/?name=gparted), or from a terminal:

*   For EXT2/3/4 (adjust accordingly), it would be:

```
# cfdisk /dev/sd**x**
# mkfs.ext4 /dev/sd**x1**
# e2label /dev/sd**x1** USB_STICK

```

*   For FAT32, install the [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) package and run:

```
# cfdisk /dev/sd**x**
# mkfs.vfat -F32 /dev/sd**x1**
# dosfslabel /dev/sd**x1** USB_STICK

```

### Using manual formatting

#### In GNU/Linux

This method is more complicated than writing the image directly with `dd`, but it does keep the flash drive usable for data storage (that is, the ISO is installed in a specific partition within the already [partitioned device](/index.php/Partitioning "Partitioning") without altering other partitions).

**Note:** Here, we will denote the targeted partition as `/dev/sd**Xn**`. In any of the following commands, adjust **X** and **n** according to your system.

*   Make sure that the latest [syslinux](https://www.archlinux.org/packages/?name=syslinux) package (version 6.02 or newer) is installed on the system.

*   If not done yet, create the partition table and/or partition on the device before continuing. The partition `/dev/sd**Xn**` must be formatted to FAT32.

*   Mount the ISO image, the FAT32 filesystem located in the USB flash device, and copy the contents of the ISO image to it. Then unmount the ISO image, but keep the FAT32 partition mounted (this will be used in subsequent steps). Eg:

```
# mkdir -p /mnt/{iso,usb}
# mount -o loop archlinux-2015.01.01-dual.iso /mnt/iso
# mount /dev/sd**Xn** /mnt/usb
# cp -a /mnt/iso/* /mnt/usb
# sync
# umount /mnt/iso

```

*   **Note:** The following step is not required when using [Archboot](/index.php/Archboot "Archboot") instead of [Archiso](/index.php/Archiso "Archiso").

    To boot either a label or an [UUID](/index.php/UUID "UUID") to select the partition to boot from is required. By default the label `ARCH_2015**XX**` (with the appropriate release month) is used. Thus, the partition’s label has to be set accordingly, for example using _gparted_. Alternatively, you can change this behaviour by altering the lines ending by `archisolabel=ARCH_2015**XX**` in files _/mnt/usb/arch/boot/syslinux/archiso_sys32.cfg_ and _archiso_sys64.cfg_, as well as _/mnt/usb/loader/entries/archiso-x86_64.conf_ or similar for a 32-bit ISO (the last being useful only, if you want to boot the USB flash device from an EFI system). To use an UUID instead, replace those portions of lines with `archiso_device_=/dev/disk/by-uuid/**YOUR-UUID**`. The UUID can be retrieved with `blkid -o value -s UUID /dev/sd**Xn**`.

**Warning:** Mismatching labels or wrong UUID prevents booting from the created medium.

*   Syslinux is already preinstalled in _/mnt/usb/arch/boot/syslinux_. Install it completely to that folder by following [Syslinux#Manual install](/index.php/Syslinux#Manual_install "Syslinux"). Instructions are reproduced here for convenience.
    *   Overwrite the existing syslinux modules (`*.c32` files) present in the USB (from the ISO) with the ones from the syslinux package. This is necessary to avoid boot failure because of a possible version mismatch.
    *   Run:

```
# extlinux --install /mnt/usb/arch/boot/syslinux

```

*   *   Unmount the partition (`umount /mnt/usb`) and install the MBR or GPT partition table to the USB device as described in the page mentioned.

*   Mark the partition as active (or “bootable”).

#### In Windows

**Note:**

*   For manual formatting, do not use any **Bootable USB Creator utility** for creating the UEFI bootable USB. For manual formatting, do not use _dd for Windows_ to dd the ISO to the USB drive either.

*   In the below commands, **X:** is assumed to be the USB flash drive in Windows.

*   Windows uses backward slash `\` as path-separator, so the same is used in the below commands.

*   All commands should be run in Windows command prompt **as administrator**.

*   `>` denotes the Windows command prompt.

*   Partition and format the USB drive using [Rufus USB partitioner](http://rufus.akeo.ie/). Select partition scheme option as **MBR for BIOS and UEFI** and File system as **FAT32**. Uncheck "Create a bootable disk using ISO image" and "Create extended label and icon files" options.

*   Change the **Volume Label** of the USB flash drive `X:` to match the LABEL mentioned in the `archisolabel=` part in `<ISO>\loader\entries\archiso-x86_64.conf`. This step is required for Official ISO ([Archiso](/index.php/Archiso "Archiso")) but not required for [Archboot](/index.php/Archboot "Archboot"). This step can be also performed using Rufus, during the prior "partition and format" step.

*   Extract the ISO (similar to extracting ZIP archive) to the USB flash drive (using [7-Zip](http://7-zip.org/).

*   Download official syslinux 6.xx binaries (zip file) from [https://www.kernel.org/pub/linux/utils/boot/syslinux/](https://www.kernel.org/pub/linux/utils/boot/syslinux/) and extract it. The version of Syslinux should be the same version used in the ISO image.

*   Run the following command (in Windows cmd prompt, as admin):

**Note:** Use `X:\boot\syslinux\` for Archboot iso.

```
> cd bios\
> for /r %Y in (*.c32) do copy "%Y" "X:\arch\boot\syslinux\" /y
> copy mbr\*.bin X:\arch\boot\syslinux\ /y

```

*   Install Syslinux to the USB by running (use `win64\syslinux64.exe` for x64 Windows):

**Note:** Use `-d /boot/syslinux` for Archboot iso.

```
> cd bios\
> win32\syslinux.exe -d /arch/boot/syslinux -i -a -m X:

```

**Note:**

*   The above step installs Syslinux's `ldlinux.sys` to the VBR of the USB partition, sets the partition as "active/boot" in the MBR partition table and writes the MBR boot code to the 1st 440-byte boot code region of the USB.

*   The `-d` switch expects a path with forward slash path-separator like in *unix systems.

## Other Methods for BIOS systems

### In GNU/Linux

#### Using a multiboot USB drive

This allows booting multiple ISOs from a single USB device, including the archiso. Updating an existing USB drive to a more recent ISO is simpler than for most other methods. See [Multiboot USB drive](/index.php/Multiboot_USB_drive "Multiboot USB drive").

#### Using UNetbootin

UNetbootin can be used on any Linux distribution or Windows to copy your iso to a USB device. However, Unetbootin overwrites syslinux.cfg, so it creates a USB device that does not boot properly. For this reason, **Unetbootin is not recommended** -- please use `dd` or one of the other methods discussed in this topic.

**Warning:** UNetbootin writes over the default `syslinux.cfg`; this must be restored before the USB device will boot properly.

Edit `syslinux.cfg`:

 `sysconfig.cfg` 

```
default menu.c32
prompt 0
menu title Archlinux Installer
timeout 100

label unetbootindefault
menu label Archlinux_x86_64
kernel /arch/boot/x86_64/vmlinuz
append initrd=/arch/boot/x86_64/archiso.img archisodevice=/dev/sd**x1** ../../

label ubnentry0
menu label Archlinux_i686
kernel /arch/boot/i686/vmlinuz
append initrd=/arch/boot/i686/archiso.img archisodevice=/dev/sd**x1** ../../
```

In `/dev/sd**x1**` you must replace **x** with the first free letter after the last letter in use on the system where you are installing Arch Linux (e.g. if you have two hard drives, use `c`.). You can make this change during the first phase of boot by pressing `Tab` when the menu is shown.

#### Using GNOME Disk Utility

Linux distributions running GNOME can easily make a live CD through [nautilus](https://www.archlinux.org/packages/?name=nautilus) and [gnome-disk-utility](https://www.archlinux.org/packages/?name=gnome-disk-utility). Simply right-click on the .iso file, and select "Open With Disk Image Writer." When GNOME Disk Utility opens, specify the flash drive from the "Destination" drop-down menu and click "Start Restoring."

#### Making an USB-ZIP drive

For some old BIOS systems, only booting from USB-ZIP drives is supported. This method allows you to still boot from a USB-HDD drive.

**Warning:** This will destroy all information on your USB flash drive!

*   Download [syslinux](https://www.archlinux.org/packages/?name=syslinux) and [mtools](https://www.archlinux.org/packages/?name=mtools) from the official repositories.
*   Find your usb drive with `lsblk`.
*   Type `mkdiskimage -4 /dev/sd**x** 0 64 32` (replace x with the letter of your drive). This will take a while.

From here continue with the manual formatting method. The partition will be /dev/sd**x**4 due to the way ZIP drives work.

**Note:** Do not format the drive as FAT32 keep it as FAT16.

### In Windows

#### Win32 Disk Imager

**Warning:** This will destroy all information on your USB flash drive!

First, download the program from [here](http://sourceforge.net/projects/win32diskimager/). Next, extract the archive and run the executable. Now, select the Arch Linux ISO under the `Image File` section and the USB flash device letter (for example, [D:\]) under the `Device` section. Finally, click `Write` when ready.

**Note:** After installation, you may need to restore the USB flash drive following a process as outlined [here](#How_to_restore_the_USB_drive).

#### USBWriter for Windows

Download the program from [http://sourceforge.net/projects/usbwriter/](http://sourceforge.net/projects/usbwriter/) and run it. Select the arch image file, the target USB stick, and click on the `write` button. Now you should be able to boot from the usb stick and install Arch Linux from it.

#### The Flashnul way

[flashnul](https://translate.google.com/translate?hl=&sl=ru&tl=en&u=http%3A%2F%2Fshounen.ru%2Fsoft%2Fflashnul%2Freadme.rus.html&sandbox=1) is an utility to verify the functionality and maintenance of Flash-Memory (USB-Flash, IDE-Flash, SecureDigital, MMC, MemoryStick, SmartMedia, XD, CompactFlash etc).

From a command prompt, invoke flashnul with `-p`, and determine which device index is your USB drive, e.g.:

 `C:\>flashnul -p` 

```
Avaible physical drives:
Avaible logical disks:
C:\
D:\
E:\

```

When you have determined which device is the correct one, you can write the image to your drive, by invoking flashnul with the device index, `-L`, and the path to your image, e.g:

```
C:\>flashnul **E:** -L _path\to\arch.iso_

```

As long as you are really sure you want to write the data, type yes, then wait a bit for it to write. If you get an access denied error, close any Explorer windows you have open.

If under Vista or Win7, you should open the console as administrator, or else flashnul will fail to open the stick as a block device and will only be able to write via the drive handle windows provides

**Note:** Confirmed that you need to use drive letter as opposed to number. flashnul 1rc1, Windows 7 x64.

#### Loading the installation media from RAM

This method uses [Syslinux](/index.php/Syslinux "Syslinux") and a [Ramdisk](/index.php/Ramdisk "Ramdisk") ([MEMDISK](http://www.syslinux.org/wiki/index.php/MEMDISK)) to load the entire Arch Linux ISO image into RAM. Since this will be running entirely from system memory, you will need to make sure the system you will be installing this on has an adequate amount. A minimum amount of RAM between 500 MB and 1 GB should suffice for a MEMDISK based, Arch Linux install.

For more information on Arch Linux system requirements as well as those for MEMDISK see the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") and [here](http://www.etherboot.org/wiki/bootingmemdisk#preliminaries). For reference, here is the [preceding forum thread](https://bbs.archlinux.org/viewtopic.php?id=135266).

**Tip:** Once the installer has completed loading you can simply remove the USB stick and even use it on a different machine to start the process all over again. Utilizing MEMDISK also allows booting and installing Arch Linux to and from the same USB flash drive.

##### Preparing the USB flash drive

Begin by formatting the USB flash drive as **FAT32**. Then create the following folders on the newly formatted drive.

*   `Boot`
    *   `Boot/ISOs`
    *   `Boot/Settings`

##### Copy the needed files to the USB flash drive

Next copy the ISO that you would like to boot to the `Boot/ISOs` folder. After that, extract from the following files from the latest release of [syslinux](https://www.archlinux.org/packages/?name=syslinux) from [here](http://www.kernel.org/pub/linux/utils/boot/syslinux/) and copy them into the following folders.

*   `./win32/syslinux.exe` to the Desktop or Downloads folder on your system.
*   `./memdisk/memdisk` to the `Settings` folder on your USB flash drive.

##### Create the configuration file

After copying the needed files, navigate to the USB flash drive, /boot/Settings and create a `syslinux.cfg` file.

**Warning:** On the `INITRD` line, be sure to use the name of the ISO file that you copied to your `ISOs` folder!

 `/Boot/Settings/syslinux.cfg` 

```
DEFAULT arch_iso

LABEL arch_iso
        MENU LABEL Arch Setup
        LINUX memdisk
        INITRD /Boot/ISOs/archlinux-2015.01.01-dual.iso
        APPEND iso
```

For more information on Syslinux see the [Arch Wiki article](/index.php/Syslinux "Syslinux").

##### Final steps

Finally, create a `*.bat` file where `syslinux.exe` is located and run it ("Run as administrator" if you are on Vista or Windows 7):

 `C:\Documents and Settings\username\Desktop\install.bat` 

```
@echo off
syslinux.exe -m -a -d /Boot/Settings X:
```

## Troubleshooting

*   For the [MEMDISK Method](#Loading_the_installation_media_from_RAM), if you get the famous "30 seconds" error trying to boot the i686 version, press the `Tab` key over the `Boot Arch Linux (i686)` entry and add `vmalloc=448M` at the end. For reference: _If your image is bigger than 128MiB and you have a 32-bit OS, then you have to increase the maximum memory usage of vmalloc_. [[1]](http://www.syslinux.org/wiki/index.php/MEMDISK#-_memdiskfind_in_combination_with_phram_and_mtdblock)

*   If you get the "30 seconds" error due to the `/dev/disk/by-label/ARCH_XXXXYY` not mounting, try renaming your USB media to `ARCH_XXXXYY` (e.g. `ARCH_201501`).

## See Also

*   [Gentoo wiki - LiveUSB/HOWTO](https://wiki.gentoo.org/wiki/LiveUSB/HOWTO)
*   [Fedora wiki - How to create and use Live USB](https://fedoraproject.org/wiki/How_to_create_and_use_Live_USB)
*   [openSUSE wiki - SDB:Live USB stick](http://en.opensuse.org/SDB:Live_USB_stick)