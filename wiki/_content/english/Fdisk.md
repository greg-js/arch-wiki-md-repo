[util-linux fdisk](https://git.kernel.org/cgit/utils/util-linux/util-linux.git/) is a dialogue-driven command-line utility that creates and manipulates partition tables and partitions on a hard disk. Hard disks are divided into partitions and this division is described in the partition table.

[GPT fdisk](http://www.rodsbooks.com/gdisk/), as implemented in the *gdisk* program and its associated utilities, works "on Globally Unique Identifier (GUID) Partition Table ([GPT](/index.php/GPT "GPT")) disks, rather than on the more common (through at least early 2013) Master Boot Record ([MBR](/index.php/MBR "MBR")) partition tables."

This article covers [fdisk(8)](http://man7.org/linux/man-pages/man8/fdisk.8.html) and its related [sfdisk(8)](http://man7.org/linux/man-pages/man8/sfdisk.8.html) utility, as well as the analogous [gdisk(8)](http://www.rodsbooks.com/gdisk/gdisk.html) and [sgdisk(8)](http://www.rodsbooks.com/gdisk/sgdisk.html) utilities.

**Tip:** For basic partitioning functionality with a graphical interface, [cfdisk(8)](http://man7.org/linux/man-pages/man8/cfdisk.8.html) and [cgdisk(8)](http://www.rodsbooks.com/gdisk/cgdisk.html) can be used.

## Contents

*   [1 Installation](#Installation)
*   [2 List partitions](#List_partitions)
*   [3 Backup and restore partition table](#Backup_and_restore_partition_table)
    *   [3.1 Using dd](#Using_dd)
    *   [3.2 Using sfdisk](#Using_sfdisk)
    *   [3.3 Using sgdisk](#Using_sgdisk)
*   [4 Create a partition table and partitions](#Create_a_partition_table_and_partitions)
    *   [4.1 Start the partition manipulator](#Start_the_partition_manipulator)
        *   [4.1.1 fdisk](#fdisk)
        *   [4.1.2 gdisk](#gdisk)
    *   [4.2 Create new table](#Create_new_table)
    *   [4.3 Create partitions](#Create_partitions)
    *   [4.4 Write changes to disk](#Write_changes_to_disk)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Convert between MBR and GPT](#Convert_between_MBR_and_GPT)
    *   [5.2 Sort partitions](#Sort_partitions)
    *   [5.3 Recover GPT header](#Recover_GPT_header)
*   [6 See also](#See_also)

## Installation

To use *fdisk* and its associated utilities, the [util-linux](https://www.archlinux.org/packages/?name=util-linux) package, which is part of the [base](https://www.archlinux.org/groups/x86_64/base/) group is required.

To use *gdisk* and its associated utilities, [install](/index.php/Install "Install") the [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) package.

## List partitions

To list partition tables and partitions on a device, you can run the following, where device is a name like `/dev/sda`:

```
# fdisk -l /dev/sda

```

**Note:** If the device is not specified, *fdisk* will list all partitions in `/proc/partitions`.

Or for the *gdisk*:

```
# gdisk -l /dev/sda

```

## Backup and restore partition table

Before making changes to a hard disk, you may want to backup the partition table and partition scheme of the drive. You can also use a backup to copy the same partition layout to numerous drives.

### Using dd

The MBR is stored in the the first 512 bytes of the disk. It consist of 3 parts:

1.  The first 446 bytes contain the boot loader.
2.  The next 64 bytes contain the partition table (4 entries of 16 bytes each, one entry for each primary partition).
3.  The last 2 bytes contain an identifier

To save the MBR as `mbr_file.img`:

```
# dd if=/dev/sdX of=/path/to/mbr_file.img bs=512 count=1

```

You can also extract the MBR from a full dd disk image:

```
# dd if=/path/to/disk.img of=/path/to/mbr_file.img bs=512 count=1

```

To restore (be careful, this destroys the existing partition table and with it access to all data on the disk):

```
# dd if=/path/to/mbr_file.img of=/dev/sdX bs=512 count=1

```

**Warning:** Restoring the MBR with a mismatching partition table will make your data unreadable and nearly impossible to recover. If you simply need to reinstall the bootloader see their respective pages as they also employ the [DOS compatibility region](http://www.pixelbeat.org/docs/disk/): [GRUB](/index.php/GRUB "GRUB") or [Syslinux](/index.php/Syslinux "Syslinux").

If you only want to restore the boot loader, but not the primary partition table entries, just restore the first 446 bytes of the MBR:

```
# dd if=/path/to/mbr_file.img of=/dev/sdX bs=446 count=1

```

To restore only the partition table, one must use:

```
# dd if=/path/to/mbr_file.img of=/dev/sdX bs=1 skip=446 count=64

```

To erase the MBR (may be useful if you have to do a full reinstall of another operating system) only the first 446 bytes are zeroed because the rest of the data contains the partition table:

```
# dd if=/dev/zero of=/dev/sda bs=446 count=1

```

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

The first step to [partitioning](/index.php/Partitioning "Partitioning") a disk is making a partition table. After that, the actual partitions are created according to the desired [partition scheme](/index.php/Partition_scheme "Partition scheme"). See the [partition table](/index.php/Partition_table "Partition table") article to help decide whether to use [MBR](/index.php/MBR "MBR") or [GPT](/index.php/GPT "GPT").

Before beginning, you may wish to [backup](#Backup_and_restore_partition_table) your current partition table and scheme.

The following shows how to use both *gdisk* and *fdisk* to perform both the creation of a partition table and the creation of the actual partitions. Differences are noted when necessary.

### Start the partition manipulator

Start either *fdisk* or *gdisk* as instructed in the following sections. Then continue with [#Create new table](#Create_new_table).

#### fdisk

Using [MBR](/index.php/MBR "MBR"), the utility for editing the partition table is called *fdisk*. Recent versions of *fdisk* have abandoned the deprecated system of using cylinders as the default display unit, as well as MS-DOS compatibility by default. The latest *fdisk* automatically aligns all partitions to 2048 sectors, or 1024 KiB, which should work for all EBS sizes that are known to be used by SSD manufacturers. This means that the default settings will give you proper alignment.

Start *fdisk* against your drive as root. In this example we are using `/dev/sda`:

```
# fdisk /dev/sda

```

This opens the *fdisk* dialogue where you can type in commands.

#### gdisk

Using [GPT](/index.php/GPT "GPT"), the utility for editing the partition table is called *gdisk*. Alternatively, you may use the curses-based version called *cgdisk*; however, the following instructions do not apply to it. See [cgdisk(8)](http://www.rodsbooks.com/gdisk/cgdisk.html) for its usage.

*gdisk* performs partition alignment automatically on a 2048 sector (or 1024KiB) block size base which should be compatible with the vast majority of SSDs if not all. [GNU Parted](/index.php/GNU_Parted "GNU Parted") also supports GPT, but is [less user-friendly](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=601813) for aligning partitions.

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

Select the partition's type id. The default, `Linux filesystem`, should be fine for most use. Press `l` to show the codes list.

**Tip:**

*   When partitioning it is always a good idea to follow the default values for first and last partition sectors. Additionally, specify partition sizes with the *+<size>{M,G,...}* notation. Such partitions are always aligned according to the device properties.
*   [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition") requires code `ef00` with *gdisk* and `EFI System` with *fdisk*.
*   [GRUB](/index.php/GRUB "GRUB") requires a BIOS boot partition with code `ef02` with *gdisk* and `BIOS boot` with *fdisk* when installing GRUB to a disk.
*   It is recommended to use `8200` with *gdisk* and `Linux swap` with *fdisk* for any [swap](/index.php/Swap "Swap") partitions, since systemd will automount it.

See the respective articles for considerations concerning the size and location of these partitions.

Repeat this procedure until you have the partitions you desire.

### Write changes to disk

Write the table to disk and exit via the `w` command.

## Tips and tricks

### Convert between MBR and GPT

*gdisk*, *sgdisk* and *cgdisk* have the ability to convert MBR and [BSD disklabels](https://en.wikipedia.org/wiki/BSD_disklabel "wikipedia:BSD disklabel") to GPT without data loss. Upon conversion, all the MBR primary partitions and the logical partitions become GPT partitions with the correct partition type GUIDs and Unique partition GUIDs created for each partition. See Rod Smith's [Converting to or from GPT](http://www.rodsbooks.com/gdisk/mbr2gpt.html) for more info.

After conversion, the bootloaders will need to be reinstalled to configure them to boot from GPT.

**Note:**

*   GPT stores a secondary table at the end of disk. This data structure consumes 33 512-byte sectors by default. MBR doesn't have a similar data structure at its end, which means that the last partition on an MBR disk sometimes extends to the very end of the disk and prevents complete conversion. If this happens to you, you must abandon the conversion and resize the final partition.
*   If your boot loader is GRUB, it needs a [BIOS Boot Partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB").
*   There are known corruption issues with the backup GPT table on laptops that are Intel chipset based, and run in RAID mode. The solution is to use AHCI instead of RAID, if possible.

To convert an MBR partition table to GPT, use *sgdisk*.

```
# sgdisk -g /dev/sda

```

To convert GPT to MBR use the `m` option. Note that it is not possible to convert more than four partitions from GPT to MBR.

```
# sgdisk -m /dev/sda

```

If the device will be bootable you will need to set the bootable flag with *fdisk*.

### Sort partitions

This applies for when a new partition is created in the space between two partitions or a partition is deleted.

MBR

```
# sfdisk -r */dev/sda*

```

GPT

```
# sgdisk -s */dev/sda*

```

After sorting the partitions if you are not using [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming"), it might be required to adjust the `/etc/fstab` and/or the `/etc/crypttab` configuration files.

### Recover GPT header

In case main GPT header or backup GPT header gets damaged, you can recover one from the other with *gdisk*.

```
# gdisk */dev/sda*

```

choose `r` for recovery and transformation options (experts only). From there choose either

*   `b`: use backup GPT header (rebuilding main)
*   `d`: use main GPT header (rebuilding backup)

When done write the table to disk and exit via the `w` command.

## See also

*   [GPT fdisk Tutorial](http://www.rodsbooks.com/gdisk/index.html) - offical webpage of gdisk with detailed walkthroughs.
*   [Manually Partitioning Your Hard Drive with fdisk](http://www.novell.com/coolsolutions/feature/19350.html)