**翻译状态：** 本文是英文页面 [Disk_cloning](/index.php/Disk_cloning "Disk cloning") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-08-04，点击[这里](https://wiki.archlinux.org/index.php?title=Disk_cloning&diff=0&oldid=328428)可以查看翻译后英文页面的改动。

磁盘克隆是制作整个硬盘镜像的过程, 其对于复制整个磁盘到别的电脑和备份/恢复都十分有用. 你可以访问[File recovery (简体中文)](/index.php/File_recovery_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "File recovery (简体中文)"), 这是一个专注于文件恢复的页面.

## Contents

*   [1 使用dd](#.E4.BD.BF.E7.94.A8dd)
    *   [1.1 克隆分区](#.E5.85.8B.E9.9A.86.E5.88.86.E5.8C.BA)
    *   [1.2 克隆整个硬盘](#.E5.85.8B.E9.9A.86.E6.95.B4.E4.B8.AA.E7.A1.AC.E7.9B.98)
    *   [1.3 Backing up the MBR](#Backing_up_the_MBR)
    *   [1.4 Create disk image](#Create_disk_image)
    *   [1.5 Restore system](#Restore_system)
    *   [1.6 Examples with compression](#Examples_with_compression)
        *   [1.6.1 7zip](#7zip)
        *   [1.6.2 Zip](#Zip)
        *   [1.6.3 Rar](#Rar)
        *   [1.6.4 Bzip2](#Bzip2)
*   [2 Using cp](#Using_cp)
*   [3 Disk cloning software](#Disk_cloning_software)
    *   [3.1 Disk cloning in Arch](#Disk_cloning_in_Arch)
    *   [3.2 Disk cloning outside of Arch](#Disk_cloning_outside_of_Arch)
*   [4 外部链接](#.E5.A4.96.E9.83.A8.E9.93.BE.E6.8E.A5)

## 使用dd

dd命令是一个简单而多功能且强大的工具. 它可以用于在无视文件系统或操作系统的情况下一块一块的将数据从原始地址复制到目的地. 在live环境比如livecd下使用dd是个方便的做法.

**Warning:** 在使用这个工具时请对任何操作保持警惕, 因为它可以破坏你的数据. 请牢记输入文件 (if=) 和输出文件 (of=) 的次序并千万不要颠倒他们! 请确保目的地(也就是分区 (of=) 不能小于源地址 (if=).

### 克隆分区

从物理盘 /dev/sda 的1分区 到物理盘 /dev/sdb 的1分区.

```
dd if=/dev/sda1 of=/dev/sdb1 bs=4096 conv=notrunc,noerror,sync

```

如果输出文件 _**of**_ (在这个例子中是sdb1) 不存在, dd 会从这个磁盘的开头开始并且创建他.

### 克隆整个硬盘

从物理盘 /dev/sda 到物理盘 /dev/sdb

```
dd if=/dev/sda of=/dev/sdb bs=4096 conv=notrunc,noerror,sync

```

这条命令会克隆整个盘, 包括MBR(所以也包括bootloader), 所有的分区、UIUD 以及数据.

*   _notrunc_ (也就是'不许删') 通过要求 dd 不对数据进行任何删节来保证数据的统一完整.
*   _noerror_ 要求 dd 无视任何读错并继续工作. dd的初始设定是一旦遇到错误就停下.
*   _sync_ 对读错误进行清零, 这样数据的开端就可以保持在 sync.
*   _bs=4096_ 将block size设置为4k. 这样硬盘读写效率不知道高到哪里去了, 显然这个对克隆速度就是最好的.

**Note:** 如果想要重新获得独特的UUID, 请对每个分区都使用 "tune2fs /deb/sdbX -U random".

{{Note|dd带来的分区表的改变并不会注册到内核. 如果想要不重启即传达这一变化, 请使用类似于 partprobe(GNU parted 的一部分)的工具来达到目的.

### Backing up the MBR

The MBR is stored in the the first 512 bytes of the disk. It consist of 3 parts:

1.  The first 446 bytes contain the boot loader.
2.  The next 64 bytes contain the partition table (4 entries of 16 bytes each, one entry for each primary partition).
3.  The last 2 bytes contain an identifier

To save the MBR into the file "mbr.img":

```
  # dd if=/dev/hda of=/mnt/sda1/mbr.img bs=512 count=1

```

To restore (be careful : this could destroy your existing partition table and with it access to all data on the disk):

```
  # dd if=/mnt/sda1/mbr.img of=/dev/hda

```

If you only want to restore the boot loader, but not the primary partition table entries, just restore the first 446 bytes of the MBR:

```
  # dd if=/mnt/sda1/mbr.img of=/dev/hda bs=446 count=1

```

To restore only the partition table, one must use

```
  # dd if=/mnt/sda1/mbr.img of=/dev/hda bs=1 skip=446 count=64

```

You can also get the MBR from a full dd disk image.

```
  #dd if=/path/to/disk.img of=/mnt/sda1/mbr.img bs=512 count=1

```

### Create disk image

1\. Boot from a liveCD or liveUSB.

2\. Make sure no partitions are mounted from the source hard drive.

3\. Mount the external HD

4\. Backup the drive.

```
 # dd if=/dev/hda conv=sync,noerror bs=64K | gzip -c  > /mnt/sda1/hda.img.gz

```

5\. Save extra information about the drive geometry necessary in order to interpret the partition table stored within the image. The most important of which is the cylinder size.

```
 # fdisk -l /dev/hda > /mnt/sda1/hda_fdisk.info

```

**NOTE:** You may wish to use a block size (bs=) that is equal to the amount of cache on the HD you are backing up. For example, bs=8192K works for an 8MB cache. The 64K mentioned in this article is better than the default bs=512 bytes, but it will run faster with a larger bs=.

### Restore system

To restore your system:

```
 # gunzip -c /mnt/sda1/hda.img.gz | dd of=/dev/hda

```

### Examples with compression

When you need to create the hard drive or a single partition compressed backup image file you must use compression tools which can do backup from a _stdout_ and the _dd_ command. Those compressed files cannot be mounted by the _mount_ command but are useful to know how to create and restore them.

#### 7zip

Install the [p7zip](https://www.archlinux.org/packages/?name=p7zip) package from the [official repositories](/index.php/Official_repositories "Official repositories"). This backup example will split the _dd_ command output in the files by up to the 100 megabyte each:

```
dd if=/dev/sdXY | 7z a -v100m -t7z -si image-file.7z

```

Restore with 7zip:

```
7z x -so  image-file.7z | dd of=/dev/sdXY

```

**Note:** 7zip can split only the _7z_ compression type files

#### Zip

Install the [zip](https://www.archlinux.org/packages/?name=zip) package from the [official repositories](/index.php/Official_repositories "Official repositories"), which contains _zipsplit_ among other utilities for the management of zip archives. It will create a file with "-" name inside the image-file.zip file which will contain data from the _dd_ command output. To make a raw output of the file you can use the `-cp` option with _unzip_ in stdout for the _dd_ command. Backup:

```
dd if=/dev/sdXY | zip --compression-method bzip2  image-file.zip - 

```

Restore:

```
unzip -cp image-file.zip | dd of=/dev/sdXY

```

The _zip_ tool cannot split files on the fly but you can use the `zipsplit` utility on an already created file.

See also `man zip` for more information.

#### Rar

Install the [rar](https://aur.archlinux.org/packages/rar/) package from the [AUR](/index.php/AUR "AUR").

**Warning:** The _rar_ examples were made based on the manuals, please confirm!

This should do a backup and split the creating file on the fly in by up to 150 megabyte files each.

```
dd if=/dev/sdXY | rar a -v150m -siimage-file.rar

```

This should restore

```
unrar x -p image-file.rar | dd of=/dev/sdXY

```

or you can use the _rar_ instead of the [unrar](https://www.archlinux.org/packages/?name=unrar) utility. The unrar utility is available in the official repositories and can be installed with `pacman -S unrar`.

#### Bzip2

Creation by using the _dd_ is more safe and use to be error free:

 `dd if=/dev/sdXY | bzip2 -f5 > compressedfile.bzip2` 

```
937016+0 records in
937016+0 records out
479752192 bytes (480 MB) copied, 94.7002 s, 5.1 MB/s

```

And a safe way of restoring with combination of the _dd_:

```
$ bunzip2 -dc compressedfile.bzip2 | dd of=/dev/sdXY

```

or

```
$ bzcat compressedfile.bzip2 | dd of=/dev/sdXY

```

**Warning:** Never ever use the `bzip2 -kdc imgage.bzip2 > /dev/sdXY` and `bzip2 -kc /dev/sdXY > imgage.bzip2` methods for serious backup of partitions and disks. The errors might be due the end of the device or partition and the restore process gives also errors due the truncated end.

## Using cp

The cp program can be used to clone a disk, one partition at a time. An advantage to using cp is that the filesystem type of the destination partition(s) may be the same or different than the source. For safety, perform the process from a live environment.

**Note:** This method should not be considered in the same category as disk cloning on the level at which dd operates. Also, it has been reported that even with the **-a** flag, some extended attributes may not be copied. For better results, rsync or tar should be used.

The basic procedure from a live environment will be:

*   Create the new destination partition(s) using fdisk, cfdisk or other tools available in the live environment.
*   Create a filesystem on each of the newly created partitions. Example:

```
mkfs -t ext3 /dev/sdb1

```

*   Mount the source and destination partitions. Example:

```
mount -t ext3 /dev/sda1 /mnt/source
mount -t ext3 /dev/sdb1 /mnt/destination

```

*   Copy the files from the source partition to the destination

```
cp -a /mnt/source/* /mnt/destination

```

**-a**: preserve all attributes , never follow symbolic links and copy recursively

*   Change the mount points of the newly cloned partitions in /etc/fstab accordingly
*   Finally, install the GRUB bootloader if necessary. (See [GRUB](/index.php/GRUB "GRUB"))

## Disk cloning software

### Disk cloning in Arch

*   [Partclone](/index.php/Partclone "Partclone") provides utilities to save and restore used blocks on a partition and supports ext2, ext3, ext4, hfs+, reiserfs, reiser4, btrfs, vmfs3, vmfs5, xfs, jfs, ufs, ntfs, fat(12/16/32) and exfat. Optionally, a ncurses interface can be used. Partclone is available in the community repository.
*   [Partimage](http://www.partimage.org/), an ncurses program, is available in the community repos. Partimage does not currently support ext4 or btrfs filesystems. NTFS is experimental.

### Disk cloning outside of Arch

If you wish to backup or propagate your Arch install root, you are probably better off booting into something else and clone the partition from there. Some suggestions:

*   [PartedMagic](http://partedmagic.com/doku.php?id=start) has a very nice live cd/usb with PartImage and other recovery tools.
*   [Mindi](http://www.mondorescue.org/) is a linux distribution specifically for disk clone backup. It comes with its own cloning program, Mondo Rescue.
*   [Acronis True Image](https://en.wikipedia.org/wiki/Acronis_True_Image "wikipedia:Acronis True Image") is a commercial disk cloner for Windows. It allows you to create a live (from within Windows), so you do not need a working Windows install on the actual machine to use it. After regitratinon of the Acronis software on their website, you will be able to download a Linux based Live cd and/or plugins for BartPE for creation of the Windows based live cd.
*   [FSArchiver](http://www.fsarchiver.org/Main_Page) allows you to save the contents of a file system to a compressed archive file. Can be found on the [System Rescue CD](http://www.sysresccd.org/Main_Page).
*   [Clonezilla](http://clonezilla.org/) is an enhanced partition imager which can also restore entire disks as well as partitions.
*   [Redo Backup and Recovery](http://redobackup.org/) is a Live CD featuring a graphical front-end to partclone.

## 外部链接

*   [Wikipedia:List of disk cloning software](https://en.wikipedia.org/wiki/List_of_disk_cloning_software "wikipedia:List of disk cloning software")
*   [Arch Linux forum thread](https://bbs.archlinux.org/viewtopic.php?id=4329)