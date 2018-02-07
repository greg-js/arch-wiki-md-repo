Related articles

*   [CD Burning](/index.php/CD_Burning "CD Burning")
*   [Archiso](/index.php/Archiso "Archiso")
*   [Multiboot USB drive](/index.php/Multiboot_USB_drive "Multiboot USB drive")

This page discusses various multi-platform methods on how to create an Arch Linux Installer USB drive (also referred to as *"flash drive", "USB stick", "USB key"*, etc) for booting in BIOS and UEFI systems. The result will be a LiveUSB (LiveCD-like) system that can be used for installing Arch Linux, system maintenance or for recovery purposes, and that, because of the nature of [SquashFS](https://en.wikipedia.org/wiki/SquashFS "wikipedia:SquashFS"), will discard all changes once the computer shuts down.

If you would like to run a full install of Arch Linux from a USB drive (i.e. with persistent settings), see [Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key"). If you would like to use your bootable Arch Linux USB stick as a rescue USB, see [Change root](/index.php/Change_root "Change root").

## Contents

*   [1 BIOS and UEFI bootable USB](#BIOS_and_UEFI_bootable_USB)
    *   [1.1 Using dd](#Using_dd)
        *   [1.1.1 In GNU/Linux](#In_GNU.2FLinux)
        *   [1.1.2 In Windows](#In_Windows)
            *   [1.1.2.1 Using Rufus](#Using_Rufus)
            *   [1.1.2.2 Using USBwriter](#Using_USBwriter)
            *   [1.1.2.3 Using win32diskimager](#Using_win32diskimager)
            *   [1.1.2.4 Using Cygwin](#Using_Cygwin)
            *   [1.1.2.5 dd for Windows](#dd_for_Windows)
        *   [1.1.3 In macOS](#In_macOS)
    *   [1.2 Using manual formatting](#Using_manual_formatting)
        *   [1.2.1 In GNU/Linux](#In_GNU.2FLinux_2)
        *   [1.2.2 In Windows](#In_Windows_2)
*   [2 Other methods for BIOS systems](#Other_methods_for_BIOS_systems)
    *   [2.1 In GNU/Linux](#In_GNU.2FLinux_3)
        *   [2.1.1 Using a multiboot USB drive](#Using_a_multiboot_USB_drive)
        *   [2.1.2 Using GNOME Disk Utility](#Using_GNOME_Disk_Utility)
        *   [2.1.3 Making a USB-ZIP drive](#Making_a_USB-ZIP_drive)
        *   [2.1.4 Using UNetbootin](#Using_UNetbootin)
    *   [2.2 In Windows](#In_Windows_3)
        *   [2.2.1 The Flashnul way](#The_Flashnul_way)
        *   [2.2.2 Loading the installation media from RAM](#Loading_the_installation_media_from_RAM)
            *   [2.2.2.1 Preparing the USB flash drive](#Preparing_the_USB_flash_drive)
            *   [2.2.2.2 Copy the needed files to the USB flash drive](#Copy_the_needed_files_to_the_USB_flash_drive)
            *   [2.2.2.3 Create the configuration file](#Create_the_configuration_file)
            *   [2.2.2.4 Final steps](#Final_steps)
*   [3 Troubleshooting](#Troubleshooting)
*   [4 See also](#See_also)

## BIOS and UEFI bootable USB

### Using dd

**Note:** This method is recommended due to its simplicity. If it does not work, switch to the alternative method [#Using manual formatting](#Using_manual_formatting) below.

**Warning:** This will irrevocably destroy all data on `/dev/**sdx**`. To restore the USB drive as an empty, usable storage device after using the Arch ISO image, the iso9660 filesystem signature needs to be removed by running `wipefs --all /dev/**sdx**` as root, before [repartitioning](/index.php/Repartition "Repartition") and [reformating](/index.php/Reformat "Reformat") the USB drive.

#### In GNU/Linux

**Tip:** Find out the name of your USB drive with `lsblk`. Make sure that it is **not** mounted.

Run the following command, replacing `/dev/**sdx**` with your drive, e.g. `/dev/sdb`. (Do **not** append a partition number, so do **not** use something like `/dev/sdb**1**`)

```
# dd bs=4M if=/path/to/archlinux.iso of=/dev/**sdx** status=progress oflag=sync

```

See [Core utilities#dd](/index.php/Core_utilities#dd "Core utilities") for more information about `dd`. See [dd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dd.1#DESCRIPTION) for more information about `oflag=sync`.

#### In Windows

##### Using Rufus

[Rufus](https://rufus.akeo.ie/) is a multi-purpose USB iso writer. Simply select the Arch Linux ISO, the USB drive you want to create the bootable Arch Linux onto and click start.

Since Rufus does not care if the drive is properly formatted or not and provides a GUI it may be the easiest and most robust tool to use.

**Note:** Be sure to select **DD image** mode from the dropdown menu or the image will be transferred incorrectly.

##### Using USBwriter

This method does not require any workaround and is as straightforward as `dd` under Linux. Just download the Arch Linux ISO, and with local administrator rights use the [USBwriter](http://sourceforge.net/p/usbwriter/wiki/Documentation/) utility to write to your USB flash memory.

##### Using win32diskimager

[win32diskimager](https://sourceforge.net/projects/win32diskimager/) is another graphical USB iso writing tool for Windows. Simply select your iso image and the target USB drive letter (you may have to format it first to assign it a drive letter), and click Write.

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

A GPL licensed dd version for Windows is available at [http://www.chrysocome.net/dd](http://www.chrysocome.net/dd). The advantage of this over Cygwin is a smaller download. Use it as shown in instructions for Cygwin above.

To begin, download the latest version of dd for Windows. Once downloaded, extract the archive's contents into Downloads or elsewhere.

Now, launch your `command prompt` as an administrator. Next, change directory (`cd`) into the Downloads directory.

If your Arch Linux ISO is elsewhere you may need to state the full path, for convenience you may wish to put the Arch Linux ISO into the same folder as the dd executable. The basic format of the command will look like this.

```
# dd if=*archlinux-2017-XX-YY-x86_64.iso* od=\\.\*x*: bs=4M

```

**Note:** The Windows drive letters are linked to a partition. To allow selecting the entire disk, *dd for Windows* provides the `od` parameter, which is used in the commands above. Note however that this parameter is specific to *dd for Windows* and cannot be found in other implementations of *dd*.

**Warning:** Because the `od` is used, all partitions on the selected disk will be destroyed. Be absolutely sure that you are directing dd to the correct drive before executing.

Simply replace the various null spots (indicated by an "x") with the correct date and correct drive letter. Here is a complete example.

```
# dd if=ISOs\archlinux-2017.04.01-x86_64.iso od=\\.\d: bs=4M

```

**Note:** Alternatively, replace the drive letter with `\\.\PhysicalDrive*X*`, where `*X*` is the physical drive number (starts from 0). Example: `# dd if=ISOs\archlinux-2017.04.01-x86_64.iso of=\\.\PhysicalDrive1 bs=4M` 

You can find out the physical drive number by typing `wmic diskdrive list brief` at the command prompt or with `dd --list`

Any Explorer window must be closed or dd will report an error.

#### In macOS

First, you need to identify the USB device. Open `/Applications/Utilities/Terminal` and list all storage devices with the command:

```
$ diskutil list

```

Your USB device will appear as something like `/dev/disk2 (external, physical)`. Verify that this is the device you want to erase by checking its name and size and then use its identifier for the commands below instead of /dev/diskX.

A USB device is normally auto-mounted in macOS, and you have to unmount (not eject) it before block-writing to it with `dd`. In Terminal, do:

```
$ diskutil unmountDisk /dev/diskX

```

Now copy the ISO image file to the device. The `dd` command is similar to its Linux counterpart, but notice the 'r' before 'disk' for raw mode which makes the transfer much faster:

```
# dd if=path/to/arch.iso of=/dev/**r**diskX bs=1m

```

After completion, macOS may complain that "The disk you inserted was not readable by this computer". Select 'Ignore'. The USB device will be bootable.

### Using manual formatting

#### In GNU/Linux

This method is more complicated than writing the image directly with `dd`, but it does keep the flash drive usable for data storage (that is, the ISO is installed in a specific partition within the already [partitioned device](/index.php/Partitioning "Partitioning") without altering other partitions).

**Note:** Here, we will denote the targeted partition as `/dev/sd**Xn**`. In any of the following commands, adjust **X** and **n** according to your system.

*   Make sure that the [syslinux](https://www.archlinux.org/packages/?name=syslinux) package is installed on the system.

*   If not done yet, create the partition table and/or partition on the device before continuing. The partition `/dev/sd**Xn**` must be formatted to [FAT32](/index.php/FAT32 "FAT32").

*   Mount the ISO image, mount the FAT32 filesystem located in the USB flash device, and copy the contents of the ISO image to it. Then unmount the ISO image, but keep the FAT32 partition mounted (this will be used in subsequent steps). Eg:

```
# mkdir -p /mnt/{iso,usb}
# mount -o loop archlinux-2017.04.01-x86_64.iso /mnt/iso
# mount /dev/sd**Xn** /mnt/usb
# cp -a /mnt/iso/* /mnt/usb
# sync
# umount /mnt/iso

```

*   **Note:** The following step is not required when using [Archboot](/index.php/Archboot "Archboot") instead of [Archiso](/index.php/Archiso "Archiso").
    To boot either a label or an [UUID](/index.php/UUID "UUID") to select the partition to boot from is required. By default the label `ARCH_2017**XX**` (with the appropriate release month) is used. Thus, the partition’s label has to be set accordingly, for example using *gparted*. Alternatively, you can change this behaviour by altering the lines ending by `archisolabel=ARCH_2017**XX**` in the file `/mnt/usb/arch/boot/syslinux/archiso_sys.cfg` (for BIOS boot), and in `/mnt/usb/loader/entries/archiso-x86_64.conf` (for UEFI boot). To use an UUID instead, replace those portions of lines with `archiso*device*=/dev/disk/by-uuid/**YOUR-UUID**`. The UUID can be retrieved with `blkid -o value -s UUID /dev/sd**Xn**`.

**Warning:** Mismatching labels or wrong UUID prevents booting from the created medium.

*   Syslinux is already preinstalled in */mnt/usb/arch/boot/syslinux*. Install it completely to that folder by following [Syslinux#Manual install](/index.php/Syslinux#Manual_install "Syslinux"). Instructions are reproduced here for convenience.
    *   Overwrite the existing Syslinux modules (`*.c32` files) present in the USB (from the ISO) with the ones from the syslinux package (found in */usr/lib/syslinux/bios*). This is necessary to avoid boot failure because of a possible version mismatch.

```
# cp /usr/lib/syslinux/bios/*.c32 /mnt/usb/arch/boot/syslinux

```

*   *   Run:

```
# extlinux --install /mnt/usb/arch/boot/syslinux

```

*   *   Unmount the partition (`umount /mnt/usb`).

*   Mark the partition as active (or “bootable”).

#### In Windows

**Note:**

*   For manual formatting, do not use any **Bootable USB Creator utility** for creating the UEFI bootable USB. For manual formatting, do not use *dd for Windows* to dd the ISO to the USB drive either.

*   In the below commands, **X:** is assumed to be the USB flash drive in Windows.

*   Windows uses backward slash `\` as path-separator, so the same is used in the below commands.

*   All commands should be run in Windows command prompt **as administrator**.

*   `>` denotes the Windows command prompt.

*   Partition and format the USB drive using [Rufus USB partitioner](http://rufus.akeo.ie/). Select partition scheme option as **MBR for BIOS and UEFI** and File system as **FAT32**. Uncheck "Create a bootable disk using ISO image" and "Create extended label and icon files" options.

*   Change the **Volume Label** of the USB flash drive `X:` to match the LABEL mentioned in the `archisolabel=` part in `<ISO>\loader\entries\archiso-x86_64.conf`. This step is required for Official ISO ([Archiso](/index.php/Archiso "Archiso")) but not required for [Archboot](/index.php/Archboot "Archboot"). This step can be also performed using Rufus, during the prior "partition and format" step.

*   Extract the ISO (similar to extracting ZIP archive) to the USB flash drive (using [7-Zip](http://7-zip.org/).

*   Download official Syslinux 6.xx binaries (zip file) from [https://www.kernel.org/pub/linux/utils/boot/syslinux/](https://www.kernel.org/pub/linux/utils/boot/syslinux/) and extract it. The version of Syslinux should be the same version used in the ISO image.

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

## Other methods for BIOS systems

### In GNU/Linux

#### Using a multiboot USB drive

This allows booting multiple ISOs from a single USB device, including the archiso. Updating an existing USB drive to a more recent ISO is simpler than for most other methods. See [Multiboot USB drive](/index.php/Multiboot_USB_drive "Multiboot USB drive").

#### Using GNOME Disk Utility

Linux distributions running GNOME can easily make a live CD through [nautilus](https://www.archlinux.org/packages/?name=nautilus) and [gnome-disk-utility](https://www.archlinux.org/packages/?name=gnome-disk-utility). Simply right-click on the .iso file, and select "Open With Disk Image Writer." When GNOME Disk Utility opens, specify the flash drive from the "Destination" drop-down menu and click "Start Restoring."

#### Making a USB-ZIP drive

For some old BIOS systems, only booting from USB-ZIP drives is supported. This method allows you to still boot from a USB-HDD drive.

**Warning:** This will destroy all information on your USB flash drive!

*   Download [syslinux](https://www.archlinux.org/packages/?name=syslinux) and [mtools](https://www.archlinux.org/packages/?name=mtools) from the official repositories.
*   Find your usb drive with `lsblk`.
*   Type `mkdiskimage -4 /dev/sd**x** 0 64 32` (replace x with the letter of your drive). This will take a while.

From here continue with the manual formatting method. The partition will be `/dev/sd**x**4` due to the way ZIP drives work.

**Note:** Do not format the drive as FAT32; keep it as FAT16.

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
```

In `/dev/sd**x1**` you must replace **x** with the first free letter after the last letter in use on the system where you are installing Arch Linux (e.g. if you have two hard drives, use `c`.). You can make this change during the first phase of boot by pressing `Tab` when the menu is shown.

### In Windows

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
C:\>flashnul **E:** -L *path\to\arch.iso*

```

As long as you are really sure you want to write the data, type yes, then wait a bit for it to write. If you get an access denied error, close any Explorer windows you have open.

If under Vista or Win7, you should open the console as administrator, or else flashnul will fail to open the stick as a block device and will only be able to write via the drive handle windows provides

**Note:** Confirmed that you need to use drive letter as opposed to number. flashnul 1rc1, Windows 7 x64.

#### Loading the installation media from RAM

This method uses [Syslinux](/index.php/Syslinux "Syslinux") and a [Ramdisk](/index.php/Ramdisk "Ramdisk") ([MEMDISK](http://www.syslinux.org/wiki/index.php/MEMDISK)) to load the entire Arch Linux ISO image into RAM. Since this will be running entirely from system memory, you will need to make sure the system you will be installing this on has an adequate amount. A minimum amount of RAM between 500 MB and 1 GB should suffice for a MEMDISK based, Arch Linux install.

For more information on Arch Linux system requirements as well as those for MEMDISK see the [Installation guide](/index.php/Installation_guide "Installation guide") and [here](http://www.etherboot.org/wiki/bootingmemdisk#preliminaries). For reference, here is the [preceding forum thread](https://bbs.archlinux.org/viewtopic.php?id=135266).

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
        INITRD /Boot/ISOs/archlinux-2017.04.01-x86_64.iso
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

*   If you get the "device did not show up after 30 seconds" error due to the `/dev/disk/by-label/ARCH_XXXXYY` not mounting, try renaming your USB media to `ARCH_XXXXYY` (e.g. `ARCH_201501`).

## See also

*   [Gentoo wiki - LiveUSB/HOWTO](https://wiki.gentoo.org/wiki/LiveUSB/HOWTO)
*   [Fedora wiki - How to create and use Live USB](https://fedoraproject.org/wiki/How_to_create_and_use_Live_USB)
*   [openSUSE wiki - SDB:Live USB stick](http://en.opensuse.org/SDB:Live_USB_stick)