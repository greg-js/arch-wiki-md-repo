Related articles

*   [File systems](/index.php/File_systems "File systems")

[F2FS](https://en.wikipedia.org/wiki/F2FS "wikipedia:F2FS") (Flash-Friendly File System) is a file system intended for NAND-based flash memory equipped with Flash Transition Layer. Unlike JFFS or UBIFS it relies on FTL to handle write distribution. It is supported from kernel 3.8 onwards.

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

First use a [partition tool](/index.php/Partitioning#Partitioning_tools "Partitioning") to resize the partition. This can be done, for example, by deleting the old partition and creating a new one with with the same type, the same start sector, and a new end position.

Then expand the filesystem to fill the new partition using:

```
# resize.f2fs /dev/sdxY

```

where `*/dev/sdxY*` is the target F2FS volume to grow. See [resize.f2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resize.f2fs.8) for supported options.

**Note:** If you're using GPT, the partition's GUID (seen in `/dev/disk/by-partuuid/`) might change, but the filesystem UUID (seen in `/dev/disk/by-uuid/`) should stay the same.

## Checking and repair

Checking and repairs to f2fs file systems are accomplished with `fsck.f2fs` provided by [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools). See [fsck.f2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fsck.f2fs.8) for available switches.

## Troubleshooting

### GRUB with root on F2FS

When using [GRUB](/index.php/GRUB "GRUB") your freshly installed system might not boot after reboot. As GRUB does not support F2FS it is not able to extract the [UUID](/index.php/UUID "UUID") of your drive so it uses classic non-persistent `/dev/*sdXx*` names instead. In this case you might have to manually edit `/boot/grub/grub.cfg` and replace `root=/dev/*sdXx*` with `root=UUID=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX*`. You can use the `blkid` command to get the UUID of your device, see [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming").