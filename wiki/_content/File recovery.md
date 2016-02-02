# File recovery

This article lists data recovery and undeletion options for Arch Linux.

## Contents

*   [1 Special notes](#Special_notes)
    *   [1.1 Before you start](#Before_you_start)
    *   [1.2 Failing drives](#Failing_drives)
    *   [1.3 Backup flash media/small partitions](#Backup_flash_media.2Fsmall_partitions)
    *   [1.4 Working with digital cameras](#Working_with_digital_cameras)
*   [2 Foremost](#Foremost)
*   [3 Extundelete](#Extundelete)
    *   [3.1 Installation](#Installation)
    *   [3.2 Usage](#Usage)
*   [4 Testdisk and PhotoRec](#Testdisk_and_PhotoRec)
    *   [4.1 Installation](#Installation_2)
    *   [4.2 Files recovered by photorec](#Files_recovered_by_photorec)
    *   [4.3 See also](#See_also)
*   [5 e2fsck](#e2fsck)
    *   [5.1 Installation](#Installation_3)
    *   [5.2 See also](#See_also_2)
*   [6 Working with raw disk images](#Working_with_raw_disk_images)
    *   [6.1 Mount the entire disk](#Mount_the_entire_disk)
    *   [6.2 Mounting partitions](#Mounting_partitions)
        *   [6.2.1 Getting disk geometry](#Getting_disk_geometry)
    *   [6.3 Using QEMU to Repair NTFS](#Using_QEMU_to_Repair_NTFS)
*   [7 Text file recovery](#Text_file_recovery)
*   [8 See also](#See_also_3)

## Special notes

### Before you start

This page is mostly intended to be used for educational purposes. If you have accidentally deleted or otherwise damaged your **valuable and irreplaceable** data and have no previous experience with data recovery, turn off your computer immediately (Just press and hold the off button or pull the plug; do not use the system shutdown function) and seek professional help. It is quite possible and even probable that, if you follow any of the steps described below without fully understanding them, you will worsen your situation.

### Failing drives

In the area of data recovery, it is best to work on images of disks rather than physical disks themselves. Generally, a failing drive's condition worsens over time. The goal ought to be to first rescue as much data as possible as early as possible in the failure of the disk and to then abandon the disk. The [ddrescue](https://www.archlinux.org/packages/?name=ddrescue) and [dd_rescue](https://www.archlinux.org/packages/?name=dd_rescue) utilities, unlike `dd`, will repeatedly try to recover from errors and will read the drive front to back, then back to front, attempting to salvage data. They keep log files so that recovery can be paused and resumed without losing progress.

See [Disk cloning](/index.php/Disk_cloning "Disk cloning").

The image files created from a utility like ddrescue can then be mounted like a physical device and can be worked on safely. Always make a copy of the original image so that you can revert if things go sour!

A tried and true method of improving failing drive reads is to keep the drive cold. A bit of time in the freezer is appropriate, but be careful to avoid bringing the drive from cold to warm too quickly, as condensation will form. Keeping the drive in the freezer with cables connected to the recovering PC works great.

Do not attempt a filesystem check on a failing drive, as this will likely make the problem **worse**. Mount it read-only.

### Backup flash media/small partitions

As an alternative to working with a 'live' partition (mounted or not), it is often preferable to work with an image, provided that the filesystem in question is not too large and that you have sufficient free HDD space to accommodate the image file. For example, flash memory devices like thumb drives, digital cameras, portable music players, cellular phones, etc. are likely to be small enough to image in many cases.

Be sure to read the man pages for the utilities listed below to verify that they are capable of working with image files.

To make an image, one can use `dd` as follows:

```
# dd if=/dev/target_partition of=/home/user/partition.image

```

### Working with digital cameras

In order for some of the utilities listed in the next section to work with flash media, the device in question needs to be mounted as a block device (i.e., listed under /dev). Digital cameras operating in PTP (Picture Transfer Protocol) mode will not work in this regard. PTP cameras are transparently handled by libgphoto and/or libptp. In this case, "transparently" means that PTP devices do not get block devices. The alternative to PTP mode, USB Mass Storage (UMS) mode, is not supported by all cameras. Some cameras have a menu item that allows switching between the two modes; refer to your camera's user manual. If your camera does not support UMS mode and therefore cannot be accessed as a block device, your only alternative is to use a flash media reader and physically remove the storage media from your camera.

## Foremost

[Foremost](http://foremost.sourceforge.net) is a console program to recover files based on their headers, footers, and internal data structures. This process is commonly referred to as data carving. Foremost can work on disk image files (such as those generated by dd, Safeback, Encase, etc.) or directly on a drive. The headers and footers can be specified by a configuration file or command line switches can be used to specify built-in file types. These built-in types look at the data structures of a given file format, allowing for more reliable and faster recovery.

See [Foremost](/index.php/Foremost "Foremost") article.

## Extundelete

**[Extundelete](http://extundelete.sourceforge.net/)** is a terminal-based utility designed to recover deleted files from ext3 and ext4 partitions. It can recover all the recently deleted files from a partition and/or a specific file(s) given by relative path or inode information. Note that it works only when the partition is unmounted. The recovered files are saved in the current directory under the folder named `RECOVERED_FILES/`.

### Installation

[extundelete](https://www.archlinux.org/packages/?name=extundelete) is available in the [official repositories](/index.php/Official_repositories "Official repositories").

### Usage

_Derived from the post on [Linux Poison](http://linuxpoison.blogspot.com/2010/09/utility-to-recover-deleted-files-from.html)._

To recover data from a specific partition, the device name for the partition, which will be in the format `/dev/sd_XN_` (_X_ is a letter and _N_ is a number.), must be known. The example used here is `/dev/sda4`, but your system might use something different (For example, MMC card readers use `/dev/mmcblkNpN` as their naming scheme.) depending on your filesystem and device configuration. If you are unsure, run `df`, which prints currently mounted partitions.

Once which partition data is to be recovered from has been determined, simply run:

```
# extundelete /dev/sda4 --restore-file _directory_/_file_

```

Any subdirectories must be specified, and the command runs from the highest level of the partition, so, to recover a file in `/home/_SomeUserName_/`, assuming `/home` is on its own partition, run:

```
# extundelete /dev/sda4 --restore-file _SomeUserName_/_SomeFile_

```

To speed up multi-file recovery, extundelete has a `--restore-files` option as well.

To recover an entire directory, run:

```
# extundelete /dev/sda4 --restore-directory _SomeUserName_/_SomeDirectory_

```

For advanced users, to manually recover blocks or inodes with extundelete, debugfs can be used to find the inode to be recovered; then, run:

```
# extundelete --restore-inode _inode_

```

_inode_ stands for any valid inode. Additional inodes to recover can be listed in an unspaced, comma-separated fashion.

Finally, to recover all deleted files from an entire partition, run:

```
# extundelete /dev/sda4 --restore-all

```

## Testdisk and PhotoRec

TestDisk and Photorec are both open-source data recovery utilities licensed under the terms of the [GNU Public License](http://www.gnu.org/licenses/gpl.html) (GPL).

**TestDisk** is primarily designed to help recover lost partitions and/or make non-booting disks bootable again when these symptoms are caused by faulty software, certain types of viruses, or human error, such as the accidental deletion of partition tables.

**PhotoRec** is file recovery software designed to recover lost files including photographs (Hint: **Photo**graph**Rec**overy), videos, documents, archives from hard disks and CD-ROMs. PhotoRec ignores the filesystem and goes after the underlying data, so it will still work even with a re-formatted or severely damaged filesystems and/or partition tables.

### Installation

[testdisk](https://www.archlinux.org/packages/?name=testdisk) from the [official repositories](/index.php/Official_repositories "Official repositories") provides both TestDisk and PhotoRec.

### Files recovered by photorec

The photorec utility stores recovered files with a random names(for most of the files) under a numbered directories, e.g. `./recup_dir.1/f872690288.jpg`, `./recup_dir.1/f864563104_wmclockmon-0.1.0.tar.gz`.

### See also

*   How to get the original filenames: [PhotoRec FAQ](http://www.cgsecurity.org/wiki/PhotoRec_FAQ#How_to_get_the_original_filenames_.3F)
*   Wiki (TestDisk): [http://www.cgsecurity.org/wiki/TestDisk](http://www.cgsecurity.org/wiki/TestDisk)
*   Wiki (Photorec): [http://www.cgsecurity.org/wiki/PhotoRec](http://www.cgsecurity.org/wiki/PhotoRec)
*   Homepage: [http://www.cgsecurity.org/](http://www.cgsecurity.org/)

## e2fsck

**e2fsck** is the ext2/ext3 filesystem checker included in the base install of Arch. e2fsck relies on a valid superblock. A superblock is a description of the entire filesystem's parameters. Because this data is so important, several copies of the superblock are distributed throughout the partition. With the `-b` option, e2fsck can take an alternate superblock argument; this is useful if the main, first superblock is damaged.

To determine where the superblocks are, run `dumpe2fs -h` on the target, unmounted partition. Superblocks are spaced differently depending on the filesystem's blocksize, which is set when the filesystem is created.

An alternate method to determine the locations of superblocks is to use the -n option with mke2fs. Be **sure** to use the `-n` flag, which, according to the `mke2fs` manpage, "_Causes mke2fs to not actually create a filesystem, but display what it would do if it were to create a filesystem. This can be used to determine the location of the backup superblocks for a particular filesystem, so long as the mke2fs parameters that were passed when the filesystem was originally created are used again. (With the -n option added, of course!)_".

### Installation

Both `e2fsck` and `dumpe2fs` are included in the base Arch install as part of [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs).

### See also

*   e2fsck man page: [http://phpunixman.sourceforge.net/index.php/man/e2fsck/8](http://phpunixman.sourceforge.net/index.php/man/e2fsck/8)
*   dumpe2fs man page: [http://phpunixman.sourceforge.net/index.php?parameter=dumpe2fs&mode=man](http://phpunixman.sourceforge.net/index.php?parameter=dumpe2fs&mode=man)

## Working with raw disk images

If you have backed up a drive using ddrescue or dd and you need to mount this image as a physical drive, see this section.

### Mount the entire disk

To mount a complete disk image to the next free loop device, use the `losetup` command:

```
# losetup -f -P /path/to/image

```

**Tip:**

*   The `-f` flag mounts the image to the next available loop device.
*   The `-P` flag creates additional devices for every partition.

See also [more information about loop devices](/index.php/QEMU#With_loop_module_autodetecting_partitions "QEMU").

### Mounting partitions

In order to be able to mount a partiton of a whole disk image, follow [the steps above](#Mount_the_entire_disk).

Once the whole disk image is mounted, a normal `mount` command can be used on the loop device:

```
# mount /dev/loop0p1 /mnt/example

```

This command mounts the first partition of the image in loop0 to the folder to the mountpoint `/mnt/example`. Remember that the mountpoint directory must exist!

#### Getting disk geometry

Once the entire disk image has been mounted as a loopback device, its drive layout can be inspected.

### Using QEMU to Repair NTFS

With a disk image that contains one or more NTFS partitions that need to be `chkdsk`ed by Windows since no good NTFS filesystem checker for Linux exists, QEMU can use a raw disk image as a real hard disk inside a virtual machine:

```
# qemu -hda _/path/to/primary_.img -hdb _/path/to/DamagedDisk_.img

```

Then, assuming Windows is installed on `_primary_.img`, it can be used to check partitions on `_/path/to/DamagedDisk_.img`.

**Warning:** Do not use lower version of Windows to check NTFS partitions create by higher version of it, e.g. Windows XP can do damage to NTFS partitions created by Windows 8 by "fixing" [metadata](https://en.wikipedia.org/wiki/NTFS#Metafiles "wikipedia:NTFS") configuration that has support for, not supported entries will be removed or miss-configured.

## Text file recovery

It is possible to find deleted plain text files on a hard drive by directly searching on the block device. A preferably unique string from the file you are trying to recover is needed.

Use `grep` to search for fixed strings (`-F`) directly on the partition:

```
$ grep -a -C 200 -F 'Unique string in text file' /dev/sd_XN_ > _OutputFile_

```

Hopefully, the content of the deleted file is now in _OutputFile_, which can be extracted from the surrounding context manually.

**Note:** The `-C 200` option tells grep to print 200 lines of context from before and after each match of the string. You may need to adjust this if the file you are looking for is very long.

## See also

*   [Data Recovery](https://help.ubuntu.com/community/DataRecovery) on the Ubuntu wiki

Retrieved from "[https://wiki.archlinux.org/index.php?title=File_recovery&oldid=415431](https://wiki.archlinux.org/index.php?title=File_recovery&oldid=415431)"