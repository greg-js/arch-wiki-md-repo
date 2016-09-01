The [Master Boot Record](https://en.wikipedia.org/wiki/Master_Boot_Record "w:Master Boot Record") (MBR) is the first 512 bytes of a storage device. It contains an operating system bootloader and the storage device's partition table. It plays an important role in the [boot process](/index.php/Boot_process "Boot process") under [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") systems.

## Contents

*   [1 Introduction](#Introduction)
    *   [1.1 Problems with MBR](#Problems_with_MBR)
*   [2 Backup and restoration](#Backup_and_restoration)
*   [3 See also](#See_also)

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

See [fdisk#Backup and restore](/index.php/Fdisk#Backup_and_restore "Fdisk") and [File recovery#Testdisk and PhotoRec](/index.php/File_recovery#Testdisk_and_PhotoRec "File recovery").

## See also

*   [What is a Master Boot Record (MBR)?](http://kb.iu.edu/data/aijw.html)
*   [Understanding Disk Drive Terminology](http://thestarman.pcministry.com/asm/mbr/DiskTerms.htm)