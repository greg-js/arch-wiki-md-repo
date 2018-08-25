Related articles

*   [File systems](/index.php/File_systems "File systems")
*   [gdisk](/index.php/Gdisk "Gdisk")
*   [GNU Parted](/index.php/GNU_Parted "GNU Parted")
*   [Partitioning](/index.php/Partitioning "Partitioning")

[util-linux fdisk](https://git.kernel.org/cgit/utils/util-linux/util-linux.git/) is a dialogue-driven command-line utility that creates and manipulates partition tables and partitions on a hard disk. Hard disks are divided into partitions and this division is described in the partition table.

This article covers [fdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fdisk.8) and its related [sfdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sfdisk.8) utility.

**Tip:** For basic partitioning functionality with a text user interface, [cfdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cfdisk.8) can be used.

## Contents

*   [1 Installation](#Installation)
*   [2 List partitions](#List_partitions)
*   [3 Backup and restore partition table](#Backup_and_restore_partition_table)
    *   [3.1 Using dd](#Using_dd)
    *   [3.2 Using sfdisk](#Using_sfdisk)
*   [4 Create a partition table and partitions](#Create_a_partition_table_and_partitions)
    *   [4.1 Create new table](#Create_new_table)
    *   [4.2 Create partitions](#Create_partitions)
    *   [4.3 Write changes to disk](#Write_changes_to_disk)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Sort partitions](#Sort_partitions)
*   [6 See also](#See_also)

## Installation

To use *fdisk* and its associated utilities, the [util-linux](https://www.archlinux.org/packages/?name=util-linux) package, which is part of the [base](https://www.archlinux.org/groups/x86_64/base/) group is required.

## List partitions

To list partition tables and partitions on a device, you can run the following, where device is a name like `/dev/sda`:

```
# fdisk -l /dev/sda

```

**Note:** If the device is not specified, *fdisk* will list all partitions in `/proc/partitions`.

## Backup and restore partition table

Before making changes to a hard disk, you may want to backup the partition table and partition scheme of the drive. You can also use a backup to copy the same partition layout to numerous drives.

### Using dd

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

## Create a partition table and partitions

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