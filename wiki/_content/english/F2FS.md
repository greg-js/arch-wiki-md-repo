Related articles

*   [File systems](/index.php/File_systems "File systems")

[F2FS](https://en.wikipedia.org/wiki/F2FS "wikipedia:F2FS") (Flash-Friendly File System) is a file system intended for NAND-based flash memory equipped with Flash Translation Layer. Unlike JFFS or UBIFS it relies on FTL to handle write distribution. It is supported from kernel 3.8 onwards.

An FTL is found in all flash memory with a SCSI/SATA/PCIe/NVMe interface [[1]](http://accelazh.github.io/ssd/A-Summary-On-SSD-And-FTL), opposed to bare NAND Flash and SmartMediaCards [[2]](http://www.linux-mtd.infradead.org/archive/tech/nand.html).

## Contents

*   [1 Creating a F2FS file system](#Creating_a_F2FS_file_system)
*   [2 Mounting a F2FS file system](#Mounting_a_F2FS_file_system)
*   [3 Grow an F2FS file system](#Grow_an_F2FS_file_system)
*   [4 Checking and repair](#Checking_and_repair)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 GRUB with root on F2FS](#GRUB_with_root_on_F2FS)

## Creating a F2FS file system

In order to create a F2FS file system, [install](/index.php/Install "Install") [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools).

Create the file system:

```
# mkfs.f2fs -l mylabel */dev/sdxY*

```

where `*/dev/sdxY*` is the target volume to format in F2FS. See [mkfs.f2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.f2fs.8) for all available options.

## Mounting a F2FS file system

The file system can then be mounted manually or via other mechanisms:

```
# mount /dev/sdxY /mnt/foo

```

## Grow an F2FS file system

When the filesystem is unmounted, it can be grown if the partition is expanded. [Shrinking is not currently supported](https://www.mail-archive.com/linux-f2fs-devel@lists.sourceforge.net/msg04247.html).

First use a [partition tool](/index.php/Partitioning#Partitioning_tools "Partitioning") to resize the partition: for example, suppose the output of the `print` command in the `parted` console for your disk is the following:

```
   Number  Start   End     Size        File system     Name                  Flag
    1      1049kB  106MB   105MB       fat32           EFI system partition  boot, esp
    2      106MB   11,0GB  10,9GB      ext4
    3      11,0GB  12,3GB  1322MB      f2fs
    4      31,0GB  31,3GB  261MB       ext4

```

To resize the `f2fs` partition to occupy all the space up to the fourth one, just give `resizepart 3 31GB` and `exit`. You can now expand the filesystem to fill the new partition using:

```
# resize.f2fs /dev/sdxY

```

where `*/dev/sdxY*` is the target F2FS volume to grow. See [resize.f2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resize.f2fs.8) for supported options.

**Note:** If you're using GPT, the partition's GUID (seen in `/dev/disk/by-partuuid/`) might change, but the filesystem UUID (seen in `/dev/disk/by-uuid/`) should stay the same.

## Checking and repair

Checking and repairs to f2fs file systems are accomplished with `fsck.f2fs` provided by [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools). See [fsck.f2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fsck.f2fs.8) for available switches.

## Troubleshooting

### GRUB with root on F2FS

Support for the F2FS filesystem has been added in the not yet released [GRUB](/index.php/GRUB "GRUB") version 2.03\. For now you need to install the boot loader to a separate `/boot` partition, formatted with a compatible file system. See [GRUB#F2FS and other unsupported file systems](/index.php/GRUB#F2FS_and_other_unsupported_file_systems "GRUB").