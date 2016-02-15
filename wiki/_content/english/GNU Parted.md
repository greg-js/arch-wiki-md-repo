GNU Parted is a program for creating and manipulating partition tables. [GParted](/index.php/GParted "GParted") is a GUI frontend.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Command line mode](#Command_line_mode)
    *   [2.2 Interactive mode](#Interactive_mode)
*   [3 Rounding](#Rounding)
*   [4 Partitioning](#Partitioning)
    *   [4.1 Create new partition table](#Create_new_partition_table)
    *   [4.2 Partition schemes](#Partition_schemes)
        *   [4.2.1 UEFI/GPT examples](#UEFI.2FGPT_examples)
        *   [4.2.2 BIOS/MBR examples](#BIOS.2FMBR_examples)
    *   [4.3 Resizing Partitions](#Resizing_Partitions)
        *   [4.3.1 Growing partitions](#Growing_partitions)
        *   [4.3.2 Shrinking partitions](#Shrinking_partitions)
*   [5 Warnings](#Warnings)
    *   [5.1 Alignment](#Alignment)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [parted](https://www.archlinux.org/packages/?name=parted) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Usage

Parted has two modes: command line and interactive. Parted should always be started with:

```
# parted device

```

where `_device_` is the hard disk device to edit (for example `/dev/sda`). If you omit the `_device_` argument, _parted_ will attempt to guess which device you want.

### Command line mode

In command line mode, this is followed by one or more commands. For example:

```
# parted /dev/sda mklabel gpt mkpart P1 ext3 1MiB 8MiB 

```

**Note:** Options (like `--help`) can only be specified on the command line.

### Interactive mode

Interactive mode simplifies the partitioning process and reduces unnecessary repetition by automatically applying all partitioning commands to the specified device.

In order to start operating on a device, execute:

```
# parted /dev/sd_x_

```

You will notice that the command-line prompt changes from a hash (`#`) to `(parted)`: this also means that the new prompt is not a command to be manually entered when running the commands in the examples.

To see a list of the available commands, enter:

```
(parted) help

```

When finished, or if wishing to implement a partition table or scheme for another device, exit from parted with:

```
(parted) quit

```

After exiting, the command-line prompt will change back to `#`.

If you do not give a parameter to a command, Parted will prompt you for it. For example:

```
(parted) mklabel
New disk label type? gpt

```

## Rounding

Since many partitioning systems have complicated constraints, Parted will usually do something slightly different to what you asked. (For example, create a partition starting at 10.352Mb, not 10.4Mb) If the calculated values differ too much, Parted will ask you for confirmation. If you know exactly what you want, or to see exactly what Parted is doing, it helps to specify partition endpoints in sectors (with the "s" suffix) and give the "unit s" command so that the partition endpoints are displayed in sectors.

As of parted-2.4, when you specify start and/or end values using IEC binary units like “MiB”, “GiB”, “TiB”, etc., parted treats those values as exact, and equivalent to the same number specified in bytes (i.e., with the “B” suffix), in that it provides no “helpful” range of sloppiness. Contrast that with a partition start request of “4GB”, which may actually resolve to some sector up to 500MB before or after that point. Thus, when creating a partition, you should prefer to specify units of bytes (“B”), sectors (“s”), or IEC binary units like “MiB”, but not “MB”, “GB”, etc.

## Partitioning

### Create new partition table

You need to (re)create the partition table of a device when it has never been partitioned before, or when you want to change the type of its partition table. Recreating the partition table of a device is also useful when the partition scheme needs to be restructured from scratch.

Open each device whose partition table must be (re)created with:

```
# parted /dev/sd_x_

```

To then create a new MBR/msdos partition table for BIOS systems, use the following command:

```
(parted) mklabel msdos

```

To create a new GPT partition table for UEFI systems instead, use:

```
(parted) mklabel gpt

```

### Partition schemes

You can decide the number and size of the partitions the devices should be split into, and which directories will be used to mount the partitions in the installed system (also known as _mount points_). The mapping from partitions to directories is the [partition scheme](/index.php/Partitioning#Partition_scheme "Partitioning"), which must comply with the following requirements:

*   At least a partition for the `/` (_root_) directory **must** be created.
*   When using a UEFI motherboard, one [EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") **must** be created

In the examples below it is assumed that a new and contiguous partitioning scheme is applied to a single device. Some optional partitions will also be created for the `/boot` and `/home` directories: see also [Arch filesystem hierarchy](/index.php/Arch_filesystem_hierarchy "Arch filesystem hierarchy") for an explanation of the purpose of the various directories; if separate partitions for directories like `/boot` or `/home` are not created, these will simply be contained in the `/` partition. Also the creation of an optional partiton for [swap space](/index.php/Swap_space "Swap space") will be illustrated.

If not already open in a _parted_ interactive session, open each device to be partitioned with:

```
# parted /dev/sd_x_

```

The following command will be used to create partitions:

```
(parted) mkpart _part-type_ _fs-type_ _start_ _end_

```

*   `_part-type_` is one of `primary`, `extended` or `logical`, and is meaningful only for MBR partition tables.
*   `_fs-type_` is an identifier chosen among those listed by entering `help mkpart` as the closest match to the file system that you will use in [#Create filesystems](#Create_filesystems). The _mkpart_ command does not actually create the file system: the `_fs-type_` parameter will simply be used by _parted_ to set a 1-byte code that is used by boot loaders to "preview" what kind of data is found in the partition, and act accordingly if necessary. See also [Wikipedia:Disk partitioning#PC partition types](https://en.wikipedia.org/wiki/Disk_partitioning#PC_partition_types "wikipedia:Disk partitioning").

**Tip:** Most [Linux native file systems](https://en.wikipedia.org/wiki/File_system#Linux "wikipedia:File system") map to the same partition code ([0x83](https://en.wikipedia.org/wiki/Partition_type#PID_83h "wikipedia:Partition type")), so it is perfectly safe to e.g. use `ext2` for an _ext4_-formatted partition.

*   `_start_` is the beginning of the partition from the start of the device. It consists of a number followed by a [unit](http://www.gnu.org/software/parted/manual/parted.html#unit), for example `1M` means start at 1MiB.
*   `_end_` is the end of the partition from the start of the device (_not_ from the `_start_` value). It has the same syntax as `_start_`, for example `100%` means end at the end of the device (use all the remaining space).

**Warning:** It is important that the partitions do not overlap each other: if you do not want to leave unused space in the device, make sure that each partition starts where the previous one ends.

**Note:** _parted_ may issue a warning like:

```
Warning: The resulting partition is not properly aligned for best performance.
Ignore/Cancel?

```

In this case, read [Partitioning#Partition alignment](/index.php/Partitioning#Partition_alignment "Partitioning") and follow [#Alignment](#Alignment) to fix it.

The following command will be used to flag the partition that contains the `/boot` directory as bootable:

```
(parted) set _partition_ boot on

```

*   `_partition_` is the number of the partition to be flagged (see the output of the `print` command).

#### UEFI/GPT examples

In every instance, a special bootable [EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") is required.

If creating a new EFI System Partition, use the following commands (the recommended size is 512MiB):

```
(parted) mkpart ESP fat32 1MiB 513MiB
(parted) set 1 boot on

```

The remaining partition scheme is entirely up to you. For one other partition using 100% of remaining space:

```
(parted) mkpart primary ext3 513MiB 100%

```

For separate `/` (20GiB) and `/home` (all remaining space) partitions:

```
(parted) mkpart primary ext3 513MiB 20.5GiB
(parted) mkpart primary ext3 20.5GiB 100%

```

And for separate `/` (20GiB), swap (4GiB), and `/home` (all remaining space) partitions:

```
(parted) mkpart primary ext3 513MiB 20.5GiB
(parted) mkpart primary linux-swap 20.5GiB 24.5GiB
(parted) mkpart primary ext3 24.5GiB 100%

```

#### BIOS/MBR examples

For a minimum single primary partition using all available disk space, the following command would be used:

```
(parted) mkpart primary ext3 1MiB 100%
(parted) set 1 boot on

```

In the following instance, a 20GiB `/` partition will be created, followed by a `/home` partition using all the remaining space:

```
(parted) mkpart primary ext3 1MiB 20GiB
(parted) set 1 boot on
(parted) mkpart primary ext3 20GiB 100%

```

In the final example below, separate `/boot` (100MiB), `/` (20GiB), swap (4GiB), and `/home` (all remaining space) partitions will be created:

```
(parted) mkpart primary ext3 1MiB 100MiB
(parted) set 1 boot on
(parted) mkpart primary ext3 100MiB 20GiB
(parted) mkpart primary linux-swap 20GiB 24GiB
(parted) mkpart primary ext3 24GiB 100%

```

### Resizing Partitions

**Warning:** Partitions that are being resized must be unmounted and not in use. If it cannot be done (e.g. the partition that mounts to `/`), use a live media/rescue system.

**Note:**

*   You can only move the end of the partition with `parted`.
*   As of parted v4.2 _resizepart_ may need the use of [#Interactive mode](#Interactive_mode).[[1]](https://bugs.launchpad.net/ubuntu/+source/parted/+bug/1270203)
*   These instructions apply to partitions that have ext2, ext3 or ext4 filesystems.

If you are growing a partition, you have to first resize the partition and then resize the filesystem on it, while for shrinking the filesystem must be resized before the partition to avoid data loss.

#### Growing partitions

To grow a partition (in parted interactive mode):

```
(parted) resizepart _number_ _end_

```

Where `_number_` is the number of the partition you are growing, and `_end_` is the new end of the partition (which needs to be larger than the old end).

Then, to grow the filesystem on the partition:

```
# resize2fs /dev/_sdaX_ _size_

```

Where `_sdaX_` stands for the partition you are growing, and `_size_` is the new size of the partition.

#### Shrinking partitions

To shrink the filesystem on the partition:

```
# resize2fs /dev/_sdaX_ _size_

```

Where `_sdaX_` stands for the partition you are growing, and `_size_` is the new size of the partition.

Then shrink the partition (in parted interactive mode):

```
(parted) resizepart _number_ _end_

```

Where `_number_` is the number of the partition you are shrinking, and `_end_` is the new end of the partition (which needs to be smaller than the old end).

When done, use the _resizepart_ command from [util-linux](https://www.archlinux.org/packages/?name=util-linux) to tell the kernel about the new size:

```
# resizepart _device_ _number_ _size_

```

Where `_device_` is the device that holds the partition, `_number_` is the number of the partition and `_size_` is the new size of the partition.

## Warnings

Parted will always warn you before doing something that is potentially dangerous, unless the command is one of those that is inherently dangerous (viz., rm, mklabel and mkpart).

### Alignment

When creating a partition, _parted_ might warn about improper partition alignment but does not hint about proper alignment. For example:

```
(parted) mkpart primary fat16 0 32M
Warning: The resulting partition is not properly aligned for best performance.
Ignore/Cancel?                                                     

```

The warning means the partition start is not aligned. Enter "Ignore" to go ahead anyway, print the partition table in sectors to see where it starts, and remove/recreate the partition with the start sector rounded up to increasing powers of 2 until the warning stops. As one example, on a flash drive with 512B sectors, Parted wanted partitions to start on sectors that were a multiple of 2048, which is 1 MiB alignment.

## See also

*   [GNU parted - Parted User's Manual](https://www.gnu.org/software/parted/manual/)
*   [How to align partitions for best performance using parted](http://rainbow.chard.org/2013/01/30/how-to-align-partitions-for-best-performance-using-parted/)
*   [Resize an ext3/ext4 partition](http://positon.org/resize-an-ext3-ext4-partition)