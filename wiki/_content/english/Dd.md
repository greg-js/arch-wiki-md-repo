Related articles

*   [Disk cloning](/index.php/Disk_cloning "Disk cloning")
*   [USB flash installation media#Using dd](/index.php/USB_flash_installation_media#Using_dd "USB flash installation media")
*   [Benchmarking#dd](/index.php/Benchmarking#dd "Benchmarking")

[dd](https://en.wikipedia.org/wiki/dd_(Unix) is a [core utility](/index.php/Core_utility "Core utility") whose primary purpose is to convert and copy a file.

Similarly to *cp*, by default *dd* makes a bit-to-bit copy of the file, but with lower-level I/O flow control features.

For more information see [dd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dd.1) or the [full documentation](https://www.gnu.org/software/coreutils/dd).

**Tip:** By default, *dd* outputs nothing until the task has finished. To monitor the progress of the operation, add the `status=progress` option to the command.

**Warning:** One should be extremely cautious using *dd*, as with any command of this kind it can destroy data irreversibly.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Disk cloning and restore](#Disk_cloning_and_restore)
    *   [2.1 Cloning a partition](#Cloning_a_partition)
    *   [2.2 Cloning an entire hard disk](#Cloning_an_entire_hard_disk)
    *   [2.3 Backing up the partition table](#Backing_up_the_partition_table)
    *   [2.4 Create disk image](#Create_disk_image)
    *   [2.5 Restore system](#Restore_system)
*   [3 Binary file patching](#Binary_file_patching)
*   [4 Backup and restore MBR](#Backup_and_restore_MBR)

## Installation

dd is part of the GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils). For other utilities in the package, please refer to [Core utilities](/index.php/Core_utilities "Core utilities").

## Disk cloning and restore

The *dd* command is a simple, yet versatile and powerful tool. It can be used to copy from source to destination, block-by-block, regardless of their filesystem types or operating systems. A convenient method is to use *dd* from a live environment, as in a Live CD.

**Warning:** As with any command of this type, you should be very cautious when using it; it can destroy data. Remember the order of input file (`if=`) and output file (`of=`) and do not reverse them! Always ensure that the destination drive or partition (`of=`) is of equal or greater size than the source (`if=`).

### Cloning a partition

From physical disk `/dev/sda`, partition 1, to physical disk `/dev/sdb`, partition 1:

```
# dd if=/dev/sda1 of=/dev/sdb1 bs=64K conv=noerror,sync status=progress

```

**Note:** Be careful that if the output partition `of=` (`sdb1` in the example) does not exist, *dd* will create a file with this name and will start filling up your root file system.

### Cloning an entire hard disk

From physical disk `/dev/sda` to physical disk `/dev/sdb`:

```
# dd if=/dev/sda of=/dev/sdb bs=64K conv=noerror,sync status=progress

```

This will clone the entire drive, including the MBR (and therefore bootloader), all partitions, UUIDs, and data.

*   `bs=` sets the block size. Defaults to 512 bytes, which is the "classic" block size for hard drives since the early 1980s, but is not the most convenient. Use a bigger value, 64K or 128K. Also, please read the warning below, because there is more to this than just "block sizes" -it also influences how read errors propagate. See [[1]](http://www.mail-archive.com/eug-lug@efn.org/msg12073.html) and [[2]](http://blog.tdg5.com/tuning-dd-block-size/) for details and to figure out the best bs value for your use case.
*   `noerror` instructs *dd* to continue operation, ignoring all read errors. Default behavior for *dd* is to halt at any error.
*   `sync` fills input blocks with zeroes if there were any read errors, so data offsets stay in sync.
*   `status=progress` shows periodic transfer statistics which can be used to estimate when the operation may be complete.

**Note:** The block size you specify influences how read errors are handled. Read below. For data recovery, use [ddrescue](/index.php/Disk_cloning#Using_ddrescue "Disk cloning").

The *dd* utility technically has an "input block size" (IBS) and an "output block size" (OBS). When you set `bs`, you effectively set both IBS and OBS. Normally, if your block size is, say, 1 MiB, *dd* will read 1024×1024 bytes and write as many bytes. But if a read error occurs, things will go wrong. Many people seem to think that *dd* will "fill up read errors with zeroes" if you use the `noerror,sync` options, but this is not what happens. *dd* will, according to documentation, fill up the OBS to IBS size *after completing its read*, which means adding zeroes at the *end* of the block. This means, for a disk, that effectively the whole 1 MiB would become messed up because of a single 512 byte read error in the beginning of the read: 12ERROR89 would become 128900000 instead of 120000089.

If you are positive that your disk does not contain any errors, you could proceed using a larger block size, which will increase the speed of your copying several fold. For example, changing bs from 512 to 64K changed copying speed from 35 MB/s to 120 MB/s on a simple Celeron 2.7 GHz system. But keep in mind that read errors on the source disk will end up as *block errors* on the destination disk, i.e. a single 512-byte read error will mess up the whole 64 KiB output block.

**Tip:** If you would like to view *dd* progressing, use the `status=progress` option. See [dd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dd.1) for details.

**Note:**

*   To regain unique UUIDs of an *ext2/3/4* filesystem, use `tune2fs /dev/sd*XY* -U random` on every partition. For swap partitions, use `mkswap /dev/sd*XY*` instead.
*   Partition table changes from *dd* are not registered by the kernel. To notify of changes without rebooting, use a utility like *partprobe* (part of [GNU Parted](/index.php/GNU_Parted "GNU Parted")).

### Backing up the partition table

See [fdisk#Backup and restore partition table](/index.php/Fdisk#Backup_and_restore_partition_table "Fdisk") or [gdisk#Backup and restore partition table](/index.php/Gdisk#Backup_and_restore_partition_table "Gdisk").

### Create disk image

Boot from a live media and make sure no partitions are mounted from the source hard drive.

Then mount the external hard drive and backup the drive:

```
# dd if=/dev/sda conv=sync,noerror bs=64K | gzip -c  > */path/to/backup.img.gz*

```

If necessary (e.g. when the format of the external HD is FAT32) split the disk image in volumes (see also the *split* man pages):

```
# dd if=/dev/sda conv=sync,noerror bs=64K | gzip -c | split -a3 -b2G - */path/to/backup.img.gz*

```

If there is not enough disk space locally, you may send the image through ssh:

```
# dd if=/dev/sda conv=sync,noerror bs=64K | gzip -c | ssh user@local dd of=backup.img.gz

```

Finally, save extra information about the drive geometry necessary in order to interpret the partition table stored within the image. The most important of which is the cylinder size.

```
# fdisk -l /dev/sda > */path/to/list_fdisk.info*

```

**Note:** You may wish to use a block size (`bs=`) that is equal to the amount of cache on the HD you are backing up. For example, `bs=8192K` works for an 8 MiB cache. The 64 KiB mentioned in this article is better than the default `bs=512` bytes, but it will run faster with a larger `bs=`.

### Restore system

To restore your system:

```
# gunzip -c */path/to/backup.img.gz* | dd of=/dev/sda

```

When the image has been split, use the following instead:

```
# cat */path/to/backup.img.gz** | gunzip -c | dd of=/dev/sda

```

## Binary file patching

If one wants to replace offset `0x123AB` of a file with the `FF C0 14` hexadecimal sequence, this can be done with the command line: `# printf '\xff\xc0\x14' | dd seek=$((0x123AB)) conv=notrunc bs=1 of=*/path/to/file*` 

## Backup and restore MBR

Before making changes to a disk, you may want to backup the partition table and partition scheme of the drive. You can also use a backup to copy the same partition layout to numerous drives.

The MBR is stored in the the first 512 bytes of the disk. It consists of 4 parts:

1.  The first 440 bytes contain the bootstrap code (boot loader).
2.  The next 6 bytes contain the disk signature.
3.  The next 64 bytes contain the partition table (4 entries of 16 bytes each, one entry for each primary partition).
4.  The last 2 bytes contain a boot signature.

To save the MBR as `mbr_file.img`:

```
# dd if=/dev/sd*X* of=*/path/to/mbr_file.img* bs=512 count=1

```

You can also extract the MBR from a full dd disk image:

```
# dd if=*/path/to/disk.img* of=*/path/to/mbr_file.img* bs=512 count=1

```

To restore (be careful, this destroys the existing partition table and with it access to all data on the disk):

```
# dd if=/*path/to/mbr_file.img* of=/dev/sd*X* bs=512 count=1

```

**Warning:** Restoring the MBR with a mismatching partition table will make your data unreadable and nearly impossible to recover. If you simply need to reinstall the bootloader see their respective pages as they also employ the [DOS compatibility region](http://www.pixelbeat.org/docs/disk/): [GRUB](/index.php/GRUB "GRUB") or [Syslinux](/index.php/Syslinux "Syslinux").

If you only want to restore the boot loader, but not the primary partition table entries, just restore the first 440 bytes of the MBR:

```
# dd if=*/path/to/mbr_file.img* of=/dev/sd*X* bs=440 count=1

```

To restore only the partition table, one must use:

```
# dd if=*/path/to/mbr_file.img* of=/dev/sd*X* bs=1 skip=446 count=64

```

To erase the MBR bootstrap code (may be useful if you have to do a full reinstall of another operating system) only the first 440 bytes need to be zeroed:

```
# dd if=/dev/zero of=/dev/sd*X* bs=440 count=1

```