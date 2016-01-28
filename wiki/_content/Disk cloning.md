# Disk cloning

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Disk cloning is the process of making an image of a partition or of an entire hard drive. This can be useful for copying the drive to other computers and for [backup](/index.php/Backup "Backup") and [recovery](/index.php/File_recovery "File recovery") purposes.

## Contents

*   [1 Using dd](#Using_dd)
    *   [1.1 Cloning a partition](#Cloning_a_partition)
    *   [1.2 Cloning an entire hard disk](#Cloning_an_entire_hard_disk)
    *   [1.3 Backing up the MBR](#Backing_up_the_MBR)
    *   [1.4 Create disk image](#Create_disk_image)
    *   [1.5 Restore system](#Restore_system)
*   [2 Disk cloning software](#Disk_cloning_software)
    *   [2.1 Disk cloning in Arch](#Disk_cloning_in_Arch)
    *   [2.2 Disk cloning outside of Arch](#Disk_cloning_outside_of_Arch)
*   [3 External Links](#External_Links)

## Using dd

The _dd_ command is a simple, yet versatile and powerful tool. It can be used to copy from source to destination, block-by-block, regardless of their filesystem types or operating systems. A convenient method is to use _dd_ from a live environment, as in a Live CD.

**Warning:** As with any command of this type, you should be very cautious when using it; it can destroy data. Remember the order of input file (`if=`) and output file (`of=`) and do not reverse them! Always ensure that the destination drive or partition (`of=`) is of equal or greater size than the source (`if=`).

### Cloning a partition

From physical disk `/dev/sda`, partition 1, to physical disk `/dev/sdb`, partition 1.

```
# dd if=/dev/sda1 of=/dev/sdb1 bs=512 conv=noerror,sync

```

**Warning:** If output file `of=` (`sdb1` in the example) does not exist, _dd_ will create a file with this name and will start filling up your root file system!

### Cloning an entire hard disk

From physical disk `/dev/sd_X_` to physical disk `/dev/sd_Y_`

```
# dd if=/dev/sd_X_ of=/dev/sd_Y_ bs=512 conv=noerror,sync

```

This will clone the entire drive, including the MBR (and therefore bootloader), all partitions, UUIDs, and data.

*   `noerror` instructs _dd_ to continue operation, ignoring all read errors. Default behavior for _dd_ is to halt at any error.
*   `sync` fills input blocks with zeroes if there were any read errors, so data offsets stay in sync.
*   `bs=512` sets the block size to 512 bytes, the "classic" block size for hard drives. If and only if your hard drives have a 4 Kib block size, you may use "4096" instead of "512". Also, please read the warning below, because there is more to this than just "block sizes" -it also influences how read errors propagate.

**Warning:** The block size you specify influences how read errors are handled. Read below.

The _dd_ utility technically has an "input block size" (IBS) and an "output block size" (OBS). When you set `bs`, you effectively set both IBS and OBS. Normally, if your block size is, say, 1 Mib, _dd_ will read 1024*1024 bytes and write as many bytes. But if a read error occurs, things will go wrong. Many people seem to think that _dd_ will "fill up read errors with zeroes" if you use the `noerror,sync` options, but this is not what happens. _dd_ will, according to documentation, fill up the OBS to IBS size _after completing its read_, which means adding zeroes at the _end_ of the block. This means, for a disk, that effectively the whole 1 Mib would become messed up because of a single 512 byte read error in the beginning of the read: 12ERROR89 would become 128900000 instead of 120000089.

If you are positive that your disk does not contain any errors, you could proceed using a larger block size, which will increase the speed of your copying several fold. For example, changing bs from 512 to 64 Ki changed copying speed from 35 MB/s to 120 MB/s on a simple Celeron 2.7 GHz system. But keep in mind that read errors on the source disk will end up as _block errors_ on the destination disk, i.e. a single 512-byte read error will mess up the whole 64 Kib output block.

**Tip:** If you would like to view _dd_ progressing, use the `status=progress` option. See [dd](/index.php/Dd "Dd") for details.

**Note:**

*   To regain unique UUIDs of an _ext2/3/4_ filesystem, use `tune2fs /dev/sd_XY_ -U random` on every partition.
*   Partition table changes from _dd_ are not registered by the kernel. To notify of changes without rebooting, use a utility like _partprobe_ (part of [GNU Parted](/index.php/GNU_Parted "GNU Parted")).

### Backing up the MBR

The MBR is stored in the the first 512 bytes of the disk. It consist of 3 parts:

1.  The first 446 bytes contain the boot loader.
2.  The next 64 bytes contain the partition table (4 entries of 16 bytes each, one entry for each primary partition).
3.  The last 2 bytes contain an identifier

To save the MBR as `mbr.img`:

```
# dd if=/dev/sdX of=/path/to/mbr_file.img bs=512 count=1

```

To restore (be careful: this could destroy your existing partition table and with it access to all data on the disk):

```
# dd if=/path/to/mbr_file.img of=/dev/sdX

```

If you only want to restore the boot loader, but not the primary partition table entries, just restore the first 446 bytes of the MBR:

```
# dd if=/path/to/mbr_file.img of=/dev/sdX bs=446 count=1

```

To restore only the partition table, one must use:

```
# dd if=/path/to/mbr_file.img of=/dev/sdX bs=1 skip=446 count=64

```

You can also get the MBR from a full dd disk image:

```
# dd if=/path/to/disk.img of=/path/to/mbr_file.img bs=512 count=1

```

### Create disk image

1\. Boot from a live media.

2\. Make sure no partitions are mounted from the source hard drive.

3\. Mount the external HD

4\. Backup the drive.

```
# dd if=/dev/sd_X_ conv=sync,noerror bs=64K | gzip -c  > _/path/to/backup.img.gz_

```

If necessary (e.g. when the format of the external HD is FAT32) split the disk image in volumes (see also the _split_ man pages).

```
# dd if=/dev/sd_X_ conv=sync,noerror bs=64K | gzip -c | split -a3 -b2G - _/path/to/backup.img.gz_

```

If there is not enough disk space locally, you may send the image through ssh:

```
# dd if=/dev/sd_X_ conv=sync,noerror bs=64K | gzip -c | ssh user@local dd of=backup.img.gz

```

5\. Save extra information about the drive geometry necessary in order to interpret the partition table stored within the image. The most important of which is the cylinder size.

```
# fdisk -l /dev/sd_X_ > _/path/to/list_fdisk.info_

```

**Note:** You may wish to use a block size (`bs=`) that is equal to the amount of cache on the HD you are backing up. For example, `bs=8192K` works for an 8 MiB cache. The 64 Kib mentioned in this article is better than the default `bs=512` bytes, but it will run faster with a larger `bs=`.

### Restore system

To restore your system:

```
# gunzip -c _/path/to/backup.img.gz_ | dd of=/dev/sd_X_

```

When the image has been split, use the following instead:

```
# cat _/path/to/backup.img.gz*_ | gunzip -c | dd of=/dev/sd_X_

```

## Disk cloning software

See also [Backup programs#Non-incremental backups](/index.php/Backup_programs#Non-incremental_backups "Backup programs").

### Disk cloning in Arch

*   [Partclone](/index.php/Partclone "Partclone") provides utilities to save and restore used blocks on a partition and supports _ext2_, _ext3_, _ext4_, _hfs+_, _reiserfs_, _reiser4_, _btrfs_, _vmfs3_, _vmfs5_, _xfs_, _jfs_, _ufs_, _ntfs_, _fat(12/16/32)_, _exfat_. Optionally, an _ncurses_ interface can be used. Partclone is available in the community repository.
*   [Partimage](http://www.partimage.org/), an _ncurses_ program, is available in the community repos. Partimage does not currently support _ext4_ or _btrfs_ filesystems. NTFS is experimental.

### Disk cloning outside of Arch

If you wish to backup or propagate your Arch install root, you are probably better off booting into something else and clone the partition from there. Some suggestions:

*   [PartedMagic](http://partedmagic.com/doku.php?id=start) has a very nice live cd/usb with PartImage and other recovery tools.
*   [Mindi](http://www.mondorescue.org/) is a linux distribution specifically for disk clone backup. It comes with its own cloning program, Mondo Rescue.
*   [Acronis True Image](https://en.wikipedia.org/wiki/Acronis_True_Image "wikipedia:Acronis True Image") is a commercial disk cloner for Windows. It allows you to create a live (from within Windows), so you do not need a working Windows install on the actual machine to use it. After registration of the Acronis software on their website, you will be able to download a Linux-based Live CD and/or plugins for BartPE for creation of the Windows-based live CD. It can also create a WinPE Live CD based on Windows. The created ISO Live CD image by Acronis doesn't have the [hybrid boot](http://www.syslinux.org/wiki/index.php/Isohybrid) ability and cannot be written to USB storage as a raw file.
*   [FSArchiver](http://www.fsarchiver.org/Main_Page) allows you to save the contents of a file system to a compressed archive file. Can be found on the [System Rescue CD](http://www.sysresccd.org/Main_Page).
*   [Clonezilla](http://clonezilla.org/) is an enhanced partition imager which can also restore entire disks as well as partitions. Clonezilla is included on the Arch Linux installation media.
*   [Redo Backup and Recovery](http://redobackup.org/) is a Live CD featuring a graphical front-end to _partclone_.

## External Links

*   [Wikipedia:List of disk cloning software](https://en.wikipedia.org/wiki/List_of_disk_cloning_software "wikipedia:List of disk cloning software")
*   [Arch Linux forum thread](https://bbs.archlinux.org/viewtopic.php?id=4329)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Disk_cloning&oldid=417537](https://wiki.archlinux.org/index.php?title=Disk_cloning&oldid=417537)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Data compression and archiving](/index.php/Category:Data_compression_and_archiving "Category:Data compression and archiving")
*   [System recovery](/index.php/Category:System_recovery "Category:System recovery")