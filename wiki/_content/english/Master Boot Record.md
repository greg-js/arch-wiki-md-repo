The [Master Boot Record](https://en.wikipedia.org/wiki/Master_Boot_Record "w:Master Boot Record") (MBR) is the first 512 bytes of a storage device. It contains an operating system bootloader and the storage device's partition table. It plays an important role in the [boot process](/index.php/Boot_process "Boot process") under [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") systems.

## Contents

*   [1 Introduction](#Introduction)
    *   [1.1 Problems with MBR](#Problems_with_MBR)
*   [2 Backup and restoration](#Backup_and_restoration)
*   [3 Restoring a Windows boot record](#Restoring_a_Windows_boot_record)
*   [4 TestDisk MBRCode](#TestDisk_MBRCode)
*   [5 See also](#See_also)

## Introduction

The MBR partition table stores the partitions info in the first sector of a hard disk as follows:

| Location in the HDD | Purpose of the Code |
| `001-440 bytes` | MBR boot code that is launched by the BIOS. |
| `441-446 bytes` | MBR disk signature. |
| `447-510 bytes` | Partition table (of primary and extended partitions, not logical). |
| `511-512 bytes` | MBR boot signature 0xAA55. |

The entire information about the primary partitions is limited to the 64 bytes allotted. To extend this, extended partitions were used. An extended partition is simply a primary partition in the MBR which acts like a container for other partitions called logical partitions. So one is limited to either 4 primary partitions, or 3 primary and 1 extended partitions with many logical partitions inside it.

### Problems with MBR

1.  Only 4 primary partitions or 3 primary + 1 extended partitions (with arbitrary number of logical partitions within the extended partition) can be defined. If you have 3 primary + 1 extended partitions, and you have some free space outside the extended partition area, you cannot create a new partition over that free space.
2.  Within the extended partition, the logical partitions' meta-data is stored in a linked-list structure. If one link is lost, all the logical partitions following that metadata are lost.
3.  MBR supports only 1 byte partition type codes which leads to many collisions.
4.  MBR stores partition sector information using 32-bit LBA values. This LBA length along with 512 byte sector size (more commonly used) limits the maximum addressable size of the disk to be 2 [TiB](https://en.wikipedia.org/wiki/TiB "wikipedia:TiB"). Any space beyond 2 TiB cannot be defined as a partition if MBR partitioning is used.

[GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table") is the next generation partitioning scheme designed to succeed the Master Boot Record partitioning scheme method to fix above problems.

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

See also [fdisk#Backup and restore](/index.php/Fdisk#Backup_and_restore "Fdisk").

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

*   [What is a Master Boot Record (MBR)?](http://kb.iu.edu/data/aijw.html)