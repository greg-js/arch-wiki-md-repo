Related articles

*   [parted](/index.php/Parted "Parted")
*   [GParted](/index.php/GParted "GParted")
*   [Partitioning (简体中文)](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Partitioning (简体中文)")

**翻译状态：** 本文是英文页面 [Fdisk](/index.php/Fdisk "Fdisk") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-08-31，点击[这里](https://wiki.archlinux.org/index.php?title=Fdisk&diff=0&oldid=538937)可以查看翻译后英文页面的改动。

[util-linux fdisk](https://git.kernel.org/cgit/utils/util-linux/util-linux.git/) 是基于命令行界面的分区表创建和编辑工具。一个硬盘需要分为一个或多个分区，这个信息在分区表里面记录。

本文介绍 [fdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fdisk.8) 和 [sfdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sfdisk.8) 工具的使用。

**Tip:** [cfdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cfdisk.8) 工具提供了基本的功能和文本界面。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 显示分区](#.E6.98.BE.E7.A4.BA.E5.88.86.E5.8C.BA)
*   [3 备份和恢复分区](#.E5.A4.87.E4.BB.BD.E5.92.8C.E6.81.A2.E5.A4.8D.E5.88.86.E5.8C.BA)
    *   [3.1 Using dd](#Using_dd)
    *   [3.2 Using sfdisk](#Using_sfdisk)
*   [4 创建分区表和分区](#.E5.88.9B.E5.BB.BA.E5.88.86.E5.8C.BA.E8.A1.A8.E5.92.8C.E5.88.86.E5.8C.BA)
    *   [4.1 Create new table](#Create_new_table)
    *   [4.2 Create partitions](#Create_partitions)
    *   [4.3 Write changes to disk](#Write_changes_to_disk)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Sort partitions](#Sort_partitions)
*   [6 See also](#See_also)

## 安装

要使用 *fdisk* 及相关工具，请使用 [util-linux](https://www.archlinux.org/packages/?name=util-linux) 软件包，这个软件包已经位于 [base](https://www.archlinux.org/groups/x86_64/base/) 软件包组。

## 显示分区

To list partition tables and partitions on a device, you can run the following, where device is a name like `/dev/sda`:

```
# fdisk -l /dev/sda

```

**Note:** If the device is not specified, *fdisk* will list all partitions in `/proc/partitions`.

## 备份和恢复分区

Before making changes to a hard disk, you may want to backup the partition table and partition scheme of the drive. You can also use a backup to copy the same partition layout to numerous drives.

### Using dd

See [Dd#Backup and restore MBR partition table](/index.php/Dd#Backup_and_restore_MBR_partition_table "Dd").

### Using sfdisk

For both GPT and MBR you can use *sfdisk* to save the partition layout of your device to a file with the `-d`/`--dump` option. Run the following command for device `/dev/sda`:

```
# sfdisk -d /dev/sda > sda.dump

```

The file should look something like this for a single ext4 partition that is 1 GiB in size:

 `sda.dump` 
```
label: gpt
label-id: AAAAAAAA-BBBB-CCCC-DDDD-EEEEEEEEEEEE
device: /dev/sda
unit: sectors
first-lba: 34
last-lba: 1048576

/dev/sda1 : start=2048, size=1048576, type=0FC63DAF-8483-4772-8E79-3D69D8477DE4, uuid=BBF1CD36-9262-463E-A4FB-81E32C12BDE7
```

To later restore this layout you can run:

```
# sfdisk /dev/sda < sda.dump

```

## 创建分区表和分区

The first step to [partitioning](/index.php/Partitioning "Partitioning") a disk is making a partition table. After that, the actual partitions are created according to the desired [partition scheme](/index.php/Partition_scheme "Partition scheme"). See the [partition table](/index.php/Partition_table "Partition table") article to help decide whether to use [MBR](/index.php/MBR "MBR") or [GPT](/index.php/GPT "GPT").

Before beginning, you may wish to [backup](#Backup_and_restore_partition_table) your current partition table and scheme.

Recent versions of *fdisk* have abandoned the deprecated system of using cylinders as the default display unit, as well as MS-DOS compatibility by default. *fdisk* automatically aligns all partitions to 2048 sectors, or 1 MiB, which should work for all EBS sizes that are known to be used by SSD manufacturers. This means that the default settings will give you proper alignment.

Start *fdisk* against your drive as root. In this example we are using `/dev/sda`:

```
# fdisk /dev/sda

```

This opens the *fdisk* dialogue where you can type in commands.

### Create new table

**Warning:** If you create a new partition table on a disk with data on it, it will erase all the data on the disk. Make sure this is what you want to do.

To create a new partition table and clear all current partition data type `o` at the prompt for a MBR partition table or `g` for a GUID Partition Table (GPT). Skip this step if the table you require has already been created.

### Create partitions

Create a new partition with the `n` command. You enter a partition type, partition number, starting sector, and an ending sector.

When prompted, specify the partition type, type `p` to create a primary partition or `e` to create an extended one. There may be up to four primary partitions.

The first sector must be specified in absolute terms using sector numbers. The last sector can be specified using the absolute position in sectors or using the `+` symbol to specify a position relative to the start sector measured in sectors, kibibytes (`K`), mebibytes (`M`), gibibytes (`G`), tebibytes (`T`), or pebibytes (`P`); for instance, setting `+2G` as the last sector will specify a point 2GiB after the start sector. Pressing the `Enter` key with no input specifies the default value, which is the start of the largest available block for the start sector and the end of the same block for the end sector.

Select the partition's type id. The default, `Linux filesystem`, should be fine for most use. Press `l` to show the codes list. You can make the partition bootable by typing `a`.

**Tip:**

*   When partitioning it is always a good idea to follow the default values for first and last partition sectors. Additionally, specify partition sizes with the *+<size>{M,G,...}* notation. Such partitions are always aligned according to the device properties.
*   On a MBR partitioned disk leave at least 16.5 KiB free space at the end of the disk to simplify [converting between MBR and GPT](/index.php/Gdisk#Convert_between_MBR_and_GPT "Gdisk") if the need ever arises.
*   [EFI system partition](/index.php/EFI_system_partition "EFI system partition") requires type `EFI System`.
*   [GRUB](/index.php/GRUB "GRUB") requires a [BIOS boot partition](/index.php/BIOS_boot_partition "BIOS boot partition") with type `BIOS boot` when installing GRUB to a disk.
*   It is recommended to use `Linux swap` for any [swap](/index.php/Swap "Swap") partitions, since systemd will automount it.

See the respective articles for considerations concerning the size and location of these partitions.

Repeat this procedure until you have the partitions you desire.

### Write changes to disk

Write the table to disk and exit via the `w` command.

## Tips and tricks

### Sort partitions

This applies for when a new partition is created in the space between two partitions or a partition is deleted. `/dev/sda` is used in this example.

```
# sfdisk -r /dev/sda

```

After sorting the partitions if you are not using [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming"), it might be required to adjust the `/etc/fstab` and/or the `/etc/crypttab` configuration files.

**Note:** The kernel must read the new partition table for the partitions (e.g. `/dev/sda1`) to be usable. Reboot the system or tell the kernel to [reread the partition table](https://serverfault.com/questions/36038/reread-partition-table-without-rebooting).

## See also

*   [Manually Partitioning Your Hard Drive with fdisk](http://www.novell.com/coolsolutions/feature/19350.html)