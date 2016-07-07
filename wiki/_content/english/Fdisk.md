[GNU fdisk](https://www.gnu.org/software/fdisk/) is a dialogue-driven command-line utility that creates and manipulates partition tables and partitions on a hard disk. Hard disks are divided into partitions and this division is described in the partition table. Arch Linux needs at least one partition in order to be installed.

This article covers **fdisk** and its related **sfdisk** and **cfdisk** utilities, as well as the analogous **gdisk**, **sgdisk** and **cgdisk** utilities.

## Contents

*   [1 Installation](#Installation)
*   [2 List partitions](#List_partitions)
*   [3 Backup and restore](#Backup_and_restore)
    *   [3.1 Using sfdisk](#Using_sfdisk)
    *   [3.2 Using sgdisk](#Using_sgdisk)
*   [4 Create a partition table and partitions](#Create_a_partition_table_and_partitions)
    *   [4.1 Start the partition manipulator](#Start_the_partition_manipulator)
        *   [4.1.1 fdisk](#fdisk)
        *   [4.1.2 gdisk](#gdisk)
    *   [4.2 Create new table](#Create_new_table)
    *   [4.3 Create partitions](#Create_partitions)
    *   [4.4 Write changes to disk](#Write_changes_to_disk)
*   [5 Convert between MBR and GPT](#Convert_between_MBR_and_GPT)

## Installation

To use *fdisk* and its associated utilities, the [util-linux](https://www.archlinux.org/packages/?name=util-linux) package, which is part of the [base](https://www.archlinux.org/groups/x86_64/base/) group is required. To use *gdisk* and its associated utilities, [install](/index.php/Install "Install") the [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) package.

## List partitions

To list partition tables and partitions on a device, you can run the following, where device is a name like `/dev/sda`:

```
# fdisk -l /dev/sda

```

Or for the *gdisk*:

```
# gdisk -l /dev/sda

```

## Backup and restore

Before making changes to a hard disk, you may want to backup the partition table and partition scheme of the drive. You can also use a backup to copy the same partition layout to numerous drives. See also [Master Boot Record#Backup and restoration](/index.php/Master_Boot_Record#Backup_and_restoration "Master Boot Record").

### Using sfdisk

For both GPT and MBR you can use *sfdisk* to save the partition layout of your device to a file with the `--dump` option. Run the following command for device `/dev/sda`:

```
# sfdisk -d /dev/sda > sda.dump

```

The file should look something like this for a single ext4 partition that is 1GB in size:

 `sda.dump` 
```
label: gpt
label-id: AAAAAAAA-BBBB-CCCC-DDDD-EEEEEEEEEEEE
device: /dev/sda
unit: sectors
first-lba: 34
last-lba: 1048576

/dev/sda1 : start=2048, size=1048576, type=0FC63DAF-8483-4772-8E79-3D69D8477DE4, uuid=BBF1CD36-9262-463E-A4FB-81E32C12BDE7

```

To later restore this layout you can run:

```
# sfdisk /dev/sda < sda.dump

```

### Using sgdisk

Using *sgdisk* you can create a binary backup consisting of the protective MBR, the main GPT header, the backup GPT header, and one copy of the partition table:

```
# sgdisk -b=sgdisk-sda.bak

```

You can later restore the backup by running:

```
# sgdisk -l=sgdisk-sda.bak

```

If you want to clone your current device's partition layout (/dev/sda in this case) to another drive (/dev/sdc) run:

```
# sgdisk -R=/dev/sdc /dev/sda

```

If both drives will be in the same computer, you need to randomize the GUID's:

```
# sgdisk -G /dev/sdc

```

## Create a partition table and partitions

The first step to [partitioning](/index.php/Partitioning "Partitioning") a disk is making a partition table. There are two different partition table types that Arch Linux can use, [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table") (GPT) and [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") (MBR). GPT is the more modern partition table type that supports larger disks and on disk partition table backups among others. MBR may be required if you [dual boot](/index.php/Dual_boot "Dual boot") with Microsoft Windows.

After that, the actual partitions are created according to the desired [partition scheme](/index.php/Partition_scheme "Partition scheme").

Before beginning, you may wish to [backup](#Backup_and_restore) your current partition table and scheme.

The following shows how to use both *gdisk* and *fdisk* to perform both steps. Differences are noted when necessary.

### Start the partition manipulator

Start either *fdisk* or *gdisk* as instructed in the following sections. Then continue with [#Create a new table](#Create_a_new_table).

#### fdisk

Using [MBR](/index.php/MBR "MBR"), the utility for editing the partition table is called *fdisk*. Recent versions of *fdisk* have abandoned the deprecated system of using cylinders as the default display unit, as well as MS-DOS compatibility by default. The latest *fdisk* automatically aligns all partitions to 2048 sectors, or 1024 KiB, which should work for all EBS sizes that are known to be used by SSD manufacturers. This means that the default settings will give you proper alignment.

Note that in the olden days, *fdisk* used cylinders as the default display unit, and retained an MS-DOS compatibility quirk that messed with SSD alignment. Therefore one will find many guides around the internet from around 2008-2009 making a big deal out of getting everything correct. With the latest *fdisk*, things are much simpler, as reflected in this guide.

Start *fdisk* against your drive as root, in this example we are using `/dev/sda`):

```
# fdisk /dev/sda

```

This opens the *fdisk* dialogue where you can type in commands.

#### gdisk

Using [GPT](/index.php/GPT "GPT"), the utility for editing the partition table is called *gdisk*. Alternatively, you may use the curses-based version called *cgdisk*; however, the following instructions do not apply to it. See `man cgdisk` for its usage.

*gdisk* can perform partition alignment automatically on a 2048 sector (or 1024KiB) block size base which should be compatible with the vast majority of SSDs if not all. [GNU parted](/index.php/GNU_parted "GNU parted") also supports GPT, but is [less user-friendly](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=601813) for aligning partitions.

To use *gdisk*, run the program with the name of the device you want to change/edit. This example uses `/dev/sda`:

```
# gdisk /dev/sda

```

### Create new table

To create a new MBR partition table and clear all current partition data, type `o` at the prompt. Skip this step if the table you require has already been created.

**Warning:** If you create a new partition table on a disk with data on it, it will erase all the data on the disk. Make sure this is what you want to do.

### Create partitions

Create a new partition with the `n` command. You enter a partition type (*fdisk* only), partition number, starting sector, and an ending sector.

For *fdisk*, when prompted, specify the partition type, type `p` to create a primary partition or `e` to create an extended one. There may be up to four primary partitions.

Both start and end sectors can be specified in absolute terms as sector numbers or as positions measured in kibibytes (`K`), mebibytes (`M`), gibibytes (`G`), tebibytes (`T`), or pebibytes (`P`); for instance, `40M` specifies a position 40MiB from the start of the disk. You can specify locations relative to the start or end of the specified default range by preceding the number by a `+` or `-` symbol, as in `+2G` to specify a point 2GiB after the default start sector, or `-200M` to specify a point 200MiB before the last available sector. Pressing the `Enter` key with no input specifies the default value, which is the start of the largest available block for the start sector and the end of the same block for the end sector.

Select the partition's type id. The default, `Linux filesystem`, should be fine for most use. Press `l` (*fdisk*) or `L` (*gdisk*) to show the codes list.

Repeat this procedure until you have the partitions you desire.

### Write changes to disk

Write the table to disk and exit via the `w` command.

## Convert between MBR and GPT

To convert an MBR partition table to GPT, you need the tool *sgdisk*.

```
# sgdisk -g /dev/sda

```

To convert GPT to MBR use the `m` option. Note that it is not possible to convert more than four partitions from GPT to MBR.

```
# sgdisk -m /dev/sda

```

If the device will be bootable you will need to set the bootable flag with *fdisk*.

See also [GUID Partition Table#Convert from MBR to GPT](/index.php/GUID_Partition_Table#Convert_from_MBR_to_GPT "GUID Partition Table").