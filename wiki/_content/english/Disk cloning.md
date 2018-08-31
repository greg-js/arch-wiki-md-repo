Related articles

*   [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs")
*   [System maintenance#Backup](/index.php/System_maintenance#Backup "System maintenance")
*   [System backup](/index.php/System_backup "System backup")

Disk cloning is the process of making an image of a partition or of an entire hard drive. This can be useful for copying the drive to other computers and for [backup](/index.php/Backup "Backup") and [recovery](/index.php/File_recovery "File recovery") purposes.

## Contents

*   [1 Using dd](#Using_dd)
    *   [1.1 Cloning a partition](#Cloning_a_partition)
    *   [1.2 Cloning an entire hard disk](#Cloning_an_entire_hard_disk)
    *   [1.3 Backing up the partition table](#Backing_up_the_partition_table)
    *   [1.4 Create disk image](#Create_disk_image)
    *   [1.5 Restore system](#Restore_system)
*   [2 Using ddrescue](#Using_ddrescue)
*   [3 Using e2image](#Using_e2image)
*   [4 Disk cloning software](#Disk_cloning_software)
    *   [4.1 dd spin-offs](#dd_spin-offs)
*   [5 See also](#See_also)

## Using dd

The *dd* command is a simple, yet versatile and powerful tool. It can be used to copy from source to destination, block-by-block, regardless of their filesystem types or operating systems. A convenient method is to use *dd* from a live environment, as in a Live CD.

**Warning:** As with any command of this type, you should be very cautious when using it; it can destroy data. Remember the order of input file (`if=`) and output file (`of=`) and do not reverse them! Always ensure that the destination drive or partition (`of=`) is of equal or greater size than the source (`if=`).

### Cloning a partition

From physical disk `/dev/sda`, partition 1, to physical disk `/dev/sdb`, partition 1.

```
# dd if=/dev/sda1 of=/dev/sdb1 bs=64K conv=noerror,sync status=progress

```

**Warning:** If output file `of=` (`sdb1` in the example) does not exist, *dd* will create a file with this name and will start filling up your root file system!

### Cloning an entire hard disk

From physical disk `/dev/sd*X*` to physical disk `/dev/sd*Y*`

```
# dd if=/dev/sd*X* of=/dev/sd*Y* bs=64K conv=noerror,sync status=progress

```

This will clone the entire drive, including the MBR (and therefore bootloader), all partitions, UUIDs, and data.

*   `bs=` sets the block size. Defaults to 512 bytes, which is the "classic" block size for hard drives since the early 1980s, but is not the most convenient. Use a bigger value, 64K or 128K. Also, please read the warning below, because there is more to this than just "block sizes" -it also influences how read errors propagate. See [[1]](http://www.mail-archive.com/eug-lug@efn.org/msg12073.html) and [[2]](http://blog.tdg5.com/tuning-dd-block-size/) for details and to figure out the best bs value for your use case.
*   `noerror` instructs *dd* to continue operation, ignoring all read errors. Default behavior for *dd* is to halt at any error.
*   `sync` fills input blocks with zeroes if there were any read errors, so data offsets stay in sync.
*   `status=progress` shows periodic transfer statistics which can be used to estimate when the operation may be complete.

**Warning:** The block size you specify influences how read errors are handled. Read below. For data recovery, use [ddrescue](#Using_ddrescue).

The *dd* utility technically has an "input block size" (IBS) and an "output block size" (OBS). When you set `bs`, you effectively set both IBS and OBS. Normally, if your block size is, say, 1 MiB, *dd* will read 1024*1024 bytes and write as many bytes. But if a read error occurs, things will go wrong. Many people seem to think that *dd* will "fill up read errors with zeroes" if you use the `noerror,sync` options, but this is not what happens. *dd* will, according to documentation, fill up the OBS to IBS size *after completing its read*, which means adding zeroes at the *end* of the block. This means, for a disk, that effectively the whole 1 MiB would become messed up because of a single 512 byte read error in the beginning of the read: 12ERROR89 would become 128900000 instead of 120000089.

If you are positive that your disk does not contain any errors, you could proceed using a larger block size, which will increase the speed of your copying several fold. For example, changing bs from 512 to 64K changed copying speed from 35 MB/s to 120 MB/s on a simple Celeron 2.7 GHz system. But keep in mind that read errors on the source disk will end up as *block errors* on the destination disk, i.e. a single 512-byte read error will mess up the whole 64 KiB output block.

**Tip:** If you would like to view *dd* progressing, use the `status=progress` option. See [dd](/index.php/Dd "Dd") for details.

**Note:**

*   To regain unique UUIDs of an *ext2/3/4* filesystem, use `tune2fs /dev/sd*XY* -U random` on every partition. For swap partitions, use `mkswap /dev/sd*XY*` instead.
*   Partition table changes from *dd* are not registered by the kernel. To notify of changes without rebooting, use a utility like *partprobe* (part of [GNU Parted](/index.php/GNU_Parted "GNU Parted")).

### Backing up the partition table

See [fdisk#Backup and restore partition table](/index.php/Fdisk#Backup_and_restore_partition_table "Fdisk") or [gdisk#Backup and restore partition table](/index.php/Gdisk#Backup_and_restore_partition_table "Gdisk").

### Create disk image

Boot from a live media and make sure no partitions are mounted from the source hard drive.

Then mount the external hard drive and backup the drive:

```
# dd if=/dev/sd*X* conv=sync,noerror bs=64K | gzip -c  > */path/to/backup.img.gz*

```

If necessary (e.g. when the format of the external HD is FAT32) split the disk image in volumes (see also the *split* man pages).

```
# dd if=/dev/sd*X* conv=sync,noerror bs=64K | gzip -c | split -a3 -b2G - */path/to/backup.img.gz*

```

If there is not enough disk space locally, you may send the image through ssh:

```
# dd if=/dev/sd*X* conv=sync,noerror bs=64K | gzip -c | ssh user@local dd of=backup.img.gz

```

Finally, save extra information about the drive geometry necessary in order to interpret the partition table stored within the image. The most important of which is the cylinder size.

```
# fdisk -l /dev/sd*X* > */path/to/list_fdisk.info*

```

**Note:** You may wish to use a block size (`bs=`) that is equal to the amount of cache on the HD you are backing up. For example, `bs=8192K` works for an 8 MiB cache. The 64 KiB mentioned in this article is better than the default `bs=512` bytes, but it will run faster with a larger `bs=`.

### Restore system

To restore your system:

```
# gunzip -c */path/to/backup.img.gz* | dd of=/dev/sd*X*

```

When the image has been split, use the following instead:

```
# cat */path/to/backup.img.gz** | gunzip -c | dd of=/dev/sd*X*

```

## Using ddrescue

*ddrescue* is a tool designed for cloning and recovering data. It copies data from one file or block device (hard disc, cdrom, etc) to another, trying to rescue the good parts first in case of read errors, to maximize the recovered data.

To clone a faulty or dying drive, run ddrescue twice. First round, copy every block without read error and log the errors to rescue.log.

```
# ddrescue -f -n /dev/sdX /dev/sdY rescue.log

```

Second round, copy only the bad blocks and try 3 times to read from the source before giving up.

```
# ddrescue -d -f -r3 /dev/sdX /dev/sdY rescue.log

```

Now you can check the file system for corruption and mount the new drive.

```
# fsck -f /dev/sdY

```

## Using e2image

*e2image* is a tool included in [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) for debugging purposes. It can be used to copy ext2, ext3, and ext4 partitions efficiently by only copying the used blocks. Note that this only works for ext2, ext3, and ext4 filesystems, and the unused blocks are not copied so this may not be a useful tool if one is hoping to recover deleted files.

To clone a partition from physical disk `/dev/sda`, partition 1, to physical disk `/dev/sdb`, partition 1 with e2image, run

```
# e2image -ra -p /dev/sda1 /dev/sdb1

```

**Note:** gparted uses e2image to efficiently copy ext2/3/4 partitions.

## Disk cloning software

These applications allow easy backup of entire filesystems and recovery in case of failure, usually in the form of a Live CD or USB drive. They contain complete system images from one or more specific points in time and are frequently used to record known good configurations. See [Wikipedia:Comparison of disk cloning software](https://en.wikipedia.org/wiki/Comparison_of_disk_cloning_software "wikipedia:Comparison of disk cloning software") for their comparison.

See also [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs") for other applications that can take full system snapshots, among other functionality.

*   **Arch Backup** — A trivial backup script with simple configuration.
    *   Configurable compression method.
    *   Multiple backup targets.

	[https://github.com/p5n/archlinux-stuff/tree/master/arch-backup/](https://github.com/p5n/archlinux-stuff/tree/master/arch-backup/) || [arch-backup](https://aur.archlinux.org/packages/arch-backup/)

*   **[Clonezilla](https://en.wikipedia.org/wiki/Clonezilla "wikipedia:Clonezilla")** — A disaster recovery, disk cloning, disk imaging and deployment solution.
    *   Boots from live CD, USB flash drive or PXE server.
    *   Supports ext2, ext3, ext4, reiserfs, reiser4, xfs, jfs, btrfs, FAT32, NTFS, HFS+ and others.
    *   Uses Partclone (default), Partimage (optional), ntfsclone (optional), or dd to image or clone a partition.
    *   Multicasting server to restore to many machines at once.
    *   Included on the Arch Linux installation media.

	[http://clonezilla.org/](http://clonezilla.org/) || [clonezilla](https://www.archlinux.org/packages/?name=clonezilla)

*   **Deepin Clone** — Tool by Deepin to backup and restore. It supports to clone, backup and restore disk or partition.

	[https://www.deepin.org/en/original/deepin-clone/](https://www.deepin.org/en/original/deepin-clone/) || [deepin-clone](https://www.archlinux.org/packages/?name=deepin-clone)

*   **FSArchiver** — A safe and flexible file-system backup and deployment tool
    *   Support for basic file attributes (permissions, owner, ...).
    *   Support for multiple file-systems per archive.
    *   Support for extended attributes (they are used by SELinux).
    *   Support the basic file-system attributes (label, uuid, block-size) for all linux file-systems.
    *   Support for [ntfs filesystems](http://www.fsarchiver.org/Cloning-ntfs) (ability to create flexible clones of a Windows partitions).
    *   Checksumming of everything which is written in the archive (headers, data blocks, whole files).
    *   Ability to restore an archive which is corrupt (it will just skip the current file).
    *   Multi-threaded lzo, gzip, bzip2, lzma compression.
    *   Support for splitting large archives into several files with a fixed maximum size.
    *   Encryption of the archive using a password. Based on blowfish from libcrypto from [OpenSSL](/index.php/OpenSSL "OpenSSL").
    *   Support backup of a mounted root filesystem (-A option).
    *   Can be found on the [System Rescue CD](http://www.sysresccd.org/Main_Page).

	[http://www.fsarchiver.org/](http://www.fsarchiver.org/) || [fsarchiver](https://www.archlinux.org/packages/?name=fsarchiver)

*   **[Mondo Rescue](https://en.wikipedia.org/wiki/Mondo_Rescue "wikipedia:Mondo Rescue")** — A disaster recovery solution to create backup media that can be used to redeploy the damaged system.
    *   Image-based backups, supporting Linux/Windows.
    *   Compression rate is adjustable.
    *   Can backup live systems (without having to halt it).
    *   Can split image over many files.
    *   Supports booting to a Live CD to perform a full restore.
    *   Can backup/restore over NFS, from CDs, tape drives and and other media.
    *   Can verify backups.

	[http://www.mondorescue.org/](http://www.mondorescue.org/) || [mondo](https://aur.archlinux.org/packages/mondo/)

*   **[Partclone](/index.php/Partclone "Partclone")** — A tool that can be used to back up and restore a partition while considering only used blocks.
    *   Supports *ext2*, *ext3*, *ext4*, *hfs+*, *reiserfs*, *reiser4*, *btrfs*, *vmfs3*, *vmfs5*, *xfs*, *jfs*, *ufs*, *ntfs*, *fat(12/16/32)*, *exfat*.
    *   Supports compression.
    *   Optionally, an *ncurses* interface can be used.

	[http://partclone.org/](http://partclone.org/) || [partclone](https://www.archlinux.org/packages/?name=partclone)

*   **[Partimage](https://en.wikipedia.org/wiki/Partimage "wikipedia:Partimage")** — An *ncurses* disk cloning utility for Linux/UNIX environments.
    *   Has a Live CD.
    *   Supports the most popular filesystems on Linux, Windows and Mac OS.
    *   Compression.
    *   Saving to multiple CDs or DVDs or across a network using Samba/NFS.
    *   Development stopped in favor of FSArchiver.

	[http://www.partimage.org](http://www.partimage.org) || [partimage](https://www.archlinux.org/packages/?name=partimage)

*   **J7Z** — GUI for Linux in java which attempts to simplify data compression and backup. It can create 7z, BZip2, Zip, GZip, Tar archives.
    *   Updates existing archives quickly.
    *   Backup multiple folders to a storage location.
    *   Create or extract protected archives.
    *   Lessen effort by using archiving profiles and lists.

	[http://j7z.xavion.name/](http://j7z.xavion.name/) || [j7z](https://aur.archlinux.org/packages/j7z/)

*   **[Redo Backup and Recovery](https://en.wikipedia.org/wiki/Redo_Backup_and_Recovery "wikipedia:Redo Backup and Recovery")** — A backup and disaster recovery application that runs from a bootable Linux CD image.
    *   Is capable of bare-metal backup and recovery of disk partitions.
    *   Uses [xPUD](http://www.xpud.org/) and [Partclone](/index.php/Partclone "Partclone") for the backend.

	[http://www.redobackup.org/](http://www.redobackup.org/) ||

*   **System Tar & Restore** — Backup and Restore your system using tar or Transfer it with rsync
    *   GUI and CLI interfaces
    *   Creates *.tar.gz*, *.tar.bz2*, *.tar.xz* or *.tar* archives
    *   Supports openssl / gpg encryption
    *   Uses rsync to transfer a running system
    *   Supports Grub2, Syslinux, EFISTUB/efibootmgr and Systemd/bootctl

	[https://github.com/tritonas00/system-tar-and-restore](https://github.com/tritonas00/system-tar-and-restore) || [system-tar-and-restore](https://aur.archlinux.org/packages/system-tar-and-restore/)

### dd spin-offs

	dcfldd 

	[dcfldd](https://www.archlinux.org/packages/?name=dcfldd) is a dd replacement with on-the-fly hashing capability helping to ensure integrity. It accepts most of dd's parameters and includes status output. A stable version of *dcfldd* was [last released in 2006](http://dcfldd.sourceforge.net/).

	ddrescue 

	GNU [ddrescue](https://www.archlinux.org/packages/?name=ddrescue) is a data recovery tool capable of ignoring read errors. *ddrescue* is not related to dd in any way except that both can be used for copying data from one device to another. The key difference is that *ddrescue* uses a sophisticated algorithm to copy data from failing drives causing them as little additional damage as possible. See the [ddrescue manual](http://www.gnu.org/software/ddrescue/manual/ddrescue_manual.html) for details.

## See also

*   [Wikipedia:List of disk cloning software](https://en.wikipedia.org/wiki/List_of_disk_cloning_software "wikipedia:List of disk cloning software")
*   [Arch Linux forum thread](https://bbs.archlinux.org/viewtopic.php?id=4329)