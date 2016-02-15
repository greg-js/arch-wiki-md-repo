The Master Boot Record (MBR) is the first 512 bytes of a storage device. It contains an operating system bootloader and the storage device's partition table.

**Note:** As a newer partitioning scheme, the [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table") (part of the [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface") specification) can be used also on BIOS systems via a [protective MBR](https://en.wikipedia.org/wiki/GUID_Partition_Table#Legacy_MBR_.28LBA_0.29 "wikipedia:GUID Partition Table"). GPT solves some legacy problems with MBR but also may have compatibility problems. Read more on [GUID Partition Table#About the Master Boot Record](/index.php/GUID_Partition_Table#About_the_Master_Boot_Record "GUID Partition Table").

## Contents

*   [1 Boot process](#Boot_process)
*   [2 History](#History)
*   [3 Backup and restoration](#Backup_and_restoration)
*   [4 Restoring a Windows boot record](#Restoring_a_Windows_boot_record)
*   [5 TestDisk MBRCode](#TestDisk_MBRCode)
*   [6 See also](#See_also)

## Boot process

Booting is a multi-stage process. Most PCs today initialize system devices with firmware called the [BIOS](http://en.wikipedia.org/wiki/BIOS) (Basic Input/Output System), which is typically stored in a dedicated ROM chip on the system board. After system devices have been initialized, the BIOS looks for the bootloader on the MBR of the first recognized storage device (hard disk drive, solid state drive, CD/DVD drive, USB drive...) or the first partition of the device. It then executes that program. The bootloader reads the partition table, and is then capable of loading the operating system(s). Common GNU/Linux bootloaders include [GRUB](/index.php/GRUB "GRUB") and [Syslinux](/index.php/Syslinux "Syslinux").

## History

The MBR consists of a short piece of assembly code (the initial bootloader – 446 bytes), a partition table for the 4 primary partitions (16 bytes each) and a _sentinel_ (0xAA55).

The "Conventional" Windows/DOS MBR bootloader code will check the partition table for one and only one _active_ partition, read X sectors from this partition and then transfer control to the operating system. The Windows/DOS bootloader can _not_ boot an Arch Linux partition because it is not designed to load the Linux kernel, and it can only cater for an _active_, _primary_ partition (which GRUB safely ignores).

The [GRand Unified Bootloader (GRUB)](/index.php/GRUB "GRUB") is the de facto standard bootloader for GNU/Linux, and users are recommended to install it on the MBR to allow booting from _any_ partition, whether it be primary or logical.

## Backup and restoration

Because the MBR is located on the disk it can be backed up and later recovered.

To backup the MBR:

```
# dd if=/dev/sda of=/path/mbr-backup bs=512 count=1

```

Restore the MBR:

```
# dd if=/path/mbr-backup of=/dev/sda bs=512 count=1

```

**Warning:** Restoring the MBR with a mismatching partition table will make your data unreadable and nearly impossible to recover. If you simply need to reinstall the bootloader see their respective pages as they also employ the [DOS compatibility region](http://www.pixelbeat.org/docs/disk/): [GRUB](/index.php/GRUB "GRUB") or [Syslinux](/index.php/Syslinux "Syslinux").

To erase the MBR (may be useful if you have to do a full reinstall of another operating system) only the first 446 bytes are zeroed because the rest of the data contains the partition table:

```
# dd if=/dev/zero of=/dev/sda bs=446 count=1

```

## Restoring a Windows boot record

By convention (and for ease of installation), Windows is usually installed on the first partition and installs its partition table and reference to its bootloader to the first sector of that partition. If you accidentally install a bootloader like GRUB to the Windows partition or damage the boot record in some other way, you will need to use a utility to repair it. Microsoft includes a boot sector fix utility `FIXBOOT` and an MBR fix utility called `FIXMBR` on their recovery discs, or sometimes on their install discs. Using this method, you can fix the reference on the boot sector of the first partition to the bootloader file and fix the reference on the MBR to the first partition, respectively. After doing this you will have to [reinstall GRUB](/index.php/GRUB#Bootloader_installation "GRUB") to the MBR as was originally intended (that is, the GRUB bootloader can be assigned to chainload the Windows bootloader).

If you wish to revert back to using Windows, you can use the `FIXBOOT` command which chains from the MBR to the boot sector of the first partition to restore normal, automatic loading of the Windows operating system.

Of note, there is a Linux utility called `ms-sys` (package [ms-sys](https://aur.archlinux.org/packages/ms-sys/) in AUR) that can install MBR's. However, this utility is only currently capable of writing new MBRs (all OS's and file systems supported) and boot sectors (a.k.a. boot record; equivalent to using `FIXBOOT`) for FAT file systems. Most LiveCDs do not have this utility by default, so it will need to be installed first, or you can look at a rescue CD that does have it, such as [Parted Magic](http://partedmagic.com/).

First, write the partition info (table) again by:

```
# ms-sys --partition /dev/sda1

```

Next, write a Windows 2000/XP/2003 MBR:

```
# ms-sys --mbr /dev/sda  # Read options for different versions

```

Then, write the new boot sector (boot record):

```
# ms-sys -(1-6)          # Read options to discover the correct FAT record type

```

`ms-sys` can also write Windows 98, ME, Vista, and 7 MBRs as well, see `ms-sys -h`.

## TestDisk MBRCode

[testdisk](https://www.archlinux.org/packages/?name=testdisk) from the [official repositories](/index.php/Official_repositories "Official repositories") can write the MBR with its own [code](http://www.cgsecurity.org/wiki/Menu_MBRCode) (which should be able to boot Windows). The package is also included in the installation media.

## See also

*   Wikipedia article: [Master boot record](https://en.wikipedia.org/wiki/Master_boot_record "wikipedia:Master boot record")
*   [What is a Master Boot Record (MBR)?](http://kb.iu.edu/data/aijw.html)