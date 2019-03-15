Related articles

*   [Partitioning](/index.php/Partitioning "Partitioning")
*   [fdisk](/index.php/Fdisk "Fdisk")
*   [GNU Parted](/index.php/GNU_Parted "GNU Parted")
*   [dd](/index.php/Dd "Dd")

[GPT fdisk](https://www.rodsbooks.com/gdisk/) (consisting of the *gdisk*, *cgdisk*, *sgdisk*, and *fixparts* programs) is a set of text-mode partitioning tools made by Rod Smith. They work on Globally Unique Identifier (GUID) Partition Table (GPT) disks, rather than on the older (and once more common) Master Boot Record (MBR) partition tables.

*gdisk*, *cgdisk* and *sgdisk* all have the same functionality but provide different user interfaces. *gdisk* is text-mode interactive, *sgdisk* is command-line and *cgdisk* has terminal user interface. This article covers [gdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gdisk.8) and [sgdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sgdisk.8) utilities.

**Tip:**

*   For basic partitioning functionality with a text user interface, [cgdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cgdisk.8) can be used.
*   GPT fdisk website has detailed walkthroughs for [gdisk](https://www.rodsbooks.com/gdisk/walkthrough.html), [cgdisk](https://www.rodsbooks.com/gdisk/cgdisk-walkthrough.html), [sgdisk](https://www.rodsbooks.com/gdisk/sgdisk-walkthrough.html) and [FixParts](https://www.rodsbooks.com/fixparts/).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 List partitions](#List_partitions)
*   [3 Backup and restore partition table](#Backup_and_restore_partition_table)
*   [4 Create a partition table and partitions](#Create_a_partition_table_and_partitions)
    *   [4.1 Create new table](#Create_new_table)
    *   [4.2 Create partitions](#Create_partitions)
        *   [4.2.1 Partition number](#Partition_number)
        *   [4.2.2 First and last sector](#First_and_last_sector)
        *   [4.2.3 Partition type](#Partition_type)
    *   [4.3 Write changes to disk](#Write_changes_to_disk)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Convert between MBR and GPT](#Convert_between_MBR_and_GPT)
    *   [5.2 Sort partitions](#Sort_partitions)
    *   [5.3 Recover GPT header](#Recover_GPT_header)
    *   [5.4 Expand a GPT disk](#Expand_a_GPT_disk)
    *   [5.5 Prevent GPT partition automounting](#Prevent_GPT_partition_automounting)
    *   [5.6 gdisk EFI application](#gdisk_EFI_application)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) package.

## List partitions

To list partition tables and partitions on a [block device](/index.php/Block_device "Block device"), you can run the following, where device is a name like `/dev/sda`, `/dev/nvme0n1`, `/dev/mmcblk0`, etc.:

```
# gdisk -l /dev/sda

```

or alternatively the same action using *sgdisk*:

```
# sgdisk -p /dev/sda

```

## Backup and restore partition table

Before making changes to a disk, you may want to backup the partition table and partition scheme of the drive. You can also use a backup to copy the same partition layout to numerous drives.

Using *sgdisk* you can create a binary backup consisting of the protective MBR, the main GPT header, the backup GPT header, and one copy of the partition table. The example below will save the partition table of `/dev/sda` to a file `sgdisk-sda.bin`:

```
# sgdisk -b=sgdisk-sda.bin /dev/sda

```

You can later restore the backup by running:

```
# sgdisk -l=sgdisk-sda.bin /dev/sda

```

If you want to clone your current device's partition layout (`/dev/sda` in this case) to another drive (`/dev/sdc`) run:

```
# sgdisk -R=/dev/sdc /dev/sda

```

If both drives will be in the same computer, you need to randomize the disk and partition GUIDs:

```
# sgdisk -G /dev/sdc

```

## Create a partition table and partitions

The first step to [partitioning](/index.php/Partitioning "Partitioning") a disk is making a partition table. After that, the actual partitions are created according to the desired [partition scheme](/index.php/Partition_scheme "Partition scheme").

Before beginning, you may wish to [backup](#Backup_and_restore_partition_table) your current partition table and scheme.

The following shows how to use *gdisk* to perform both the creation of a partition table and the creation of the actual partitions. Alternatively, you may use the curses-based version called *cgdisk*; however, the following instructions do not apply to it. See [cgdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cgdisk.8) for its usage.

*gdisk* performs partition alignment automatically on a 2048 512-byte sector (1 MiB) block size base which should be compatible with all [Advanced Format](/index.php/Advanced_Format "Advanced Format") HDDs and the vast majority of [SSDs](/index.php/SSD "SSD") if not all.

To use *gdisk*, run the program with the name of the [block device](/index.php/Block_device "Block device") you want to change/edit. This example uses `/dev/sda`:

```
# gdisk /dev/sda

```

### Create new table

**Warning:** If you create a new partition table on a disk with data on it, it will erase all the data on the disk. Make sure this is what you want to do.

To create a new [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table") and clear all current partition data, type `o` at the prompt. Skip this step if the table you require has already been created.

### Create partitions

Create a new partition with the `n` command. You must enter the partition number, first sector, last sector and the partition type.

**Note:** See [Partitioning#Partition scheme](/index.php/Partitioning#Partition_scheme "Partitioning") for considerations concerning the size and location of partitions.

**Tip:**

*   It is advised to follow the [Discoverable Partitions Specification](https://www.freedesktop.org/wiki/Specifications/DiscoverablePartitionsSpec/) since [systemd-gpt-auto-generator(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-gpt-auto-generator.8) will automount them. See [#Prevent GPT partition automounting](#Prevent_GPT_partition_automounting) if you want to disable automounting for a partition.
*   Leave a 1 MiB free space somewhere in the first 2 TiB of the disk (e.g. by using `+1M` as the first sector of a partition) in case you ever need to create a [BIOS boot partition](/index.php/BIOS_boot_partition "BIOS boot partition").

#### Partition number

A partition number is the number assigned to a partition, e.g. a partition with number `1` on a disk `/dev/sda` would be `/dev/sda1`. Partition numbers may not always match the order of partitions on disk, in which case they can be [sorted](#Sort_partitions).

It is advised to choose the default number suggested by *gdisk*.

#### First and last sector

The first and last sectors of the partition can be specified in sector numbers or as positions measured in kibibytes (`K`), mebibytes (`M`), gibibytes (`G`), tebibytes (`T`), or pebibytes (`P`);

The position can be specified in:

*   absolute terms from the start of the disk. E.g. `40M` as a first sector specifies a position 40 MiB from the start of the disk.
*   relative terms by preceding the size with `**+***size*` or `**-***size*`. E.g. `+2G` to specify a point 2 GiB after the default start sector, or `-200M` to specify a point 200 MiB before the last available sector.

Pressing the `Enter` key with no input specifies the default value, which is the start of the largest available block for the first sector and the end of the same block for the last sector.

**Tip:** When partitioning it is always a good idea to specify partition sizes using relative terms with the `+*size{M,G,T,P}*` notation and not use sizes smaller than 1 MiB. Such partitions will always be aligned according to the device properties.

#### Partition type

Select the partition's type by entering gdisk's internal type code or specifying the [partition type GUID](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table") manually. The default, `Linux filesystem` (GUID `0FC63DAF-8483-4772-8E79-3D69D8477DE4`, gdisk's internal code `8300`), should be fine for most use cases.

<caption>Common partition types</caption>
| Partition type | Mountpoint | gdisk's
code | [Partition type GUID](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table") |
| Linux filesystem | Any | `8300` | `0FC63DAF-8483-4772-8E79-3D69D8477DE4` |
| [EFI system partition](/index.php/EFI_system_partition "EFI system partition") | Any | `ef00` | `C12A7328-F81F-11D2-BA4B-00A0C93EC93B` |
| [BIOS boot partition](/index.php/BIOS_boot_partition "BIOS boot partition") | None | `ef02` | `21686148-6449-6E6F-744E-656564454649` |
| [Linux x86-64 root (/)](/index.php/Partitioning#/ "Partitioning") | `/` | `8304` | `4F68BCE3-E8CD-4DB1-96E7-FBCAF984B709` |
| [Linux swap](/index.php/Partitioning#Swap "Partitioning") | `[SWAP]` | `8200` | `0657FD6D-A4AB-43C4-84E5-0933C84B4F4F` |
| [Linux /home](/index.php/Partitioning#/home "Partitioning") | `/home` | `8302` | `933AC7E1-2EB4-4F13-B844-0E14E2AEF915` |
| [Linux /srv](/index.php/Partitioning#Discrete_partitions "Partitioning") | `/srv` | `8306` | `3B8F8425-20E0-4F3B-907F-1A25A76F98E8` |
| [Linux LVM](/index.php/LVM#Create_partitions "LVM") | Any | `8e00` | `E6D6D379-F507-44C2-A23C-238F2A3DF928` |
| [Linux RAID](/index.php/RAID#GUID_Partition_Table "RAID") | Any | `fd00` | `A19D880F-05FC-4D3B-A006-743F0F84911E` |
| [Linux LUKS](/index.php/Dm-crypt/Drive_preparation#Physical_partitions "Dm-crypt/Drive preparation") | Any | `8309` | `CA7D7CCB-63ED-4C53-861C-1742536059CC` |
| [Linux dm-crypt](/index.php/Dm-crypt/Drive_preparation#Physical_partitions "Dm-crypt/Drive preparation") | Any | `8308` | `7FFEC5C9-2D00-49B7-8941-3EA10A5586B7` |

**Tip:** Press `L` to show gdisk's internal code list.

Repeat this procedure until you have the partitions you desire.

### Write changes to disk

**Tip:** Use the command `c` to change a partition's name ([PARTLABEL](/index.php/PARTLABEL "PARTLABEL")) for easy distinguishing.

Write the table to disk and exit via the `w` command.

## Tips and tricks

### Convert between MBR and GPT

**Tip:** Read Rod Smith's [Converting to or from GPT](https://www.rodsbooks.com/gdisk/mbr2gpt.html) for more detailed information and walktrough.

*gdisk*, *sgdisk* and *cgdisk* have the ability to convert MBR and [BSD disklabels](https://en.wikipedia.org/wiki/BSD_disklabel "wikipedia:BSD disklabel") to GPT without data loss. Upon conversion, all the MBR primary partitions and the logical partitions become GPT partitions with the correct partition type GUIDs and Unique partition GUIDs created for each partition.

After conversion, the [boot loader](/index.php/Boot_loader "Boot loader") will need to be reinstalled to configure it to boot from GPT.

**Warning:**

*   GPT stores a secondary table at the end of disk. This data structure consumes 33 512-byte sectors (16.5 KiB) by default. MBR does not have a similar data structure at its end, which means that the last partition on an MBR disk sometimes extends to the very end of the disk and prevents complete conversion. If this happens to you, you must abandon the conversion and resize the final partition.

*   There are known corruption issues with the backup GPT on laptops that are Intel chipset based, and run in RAID mode. The solution is to use AHCI instead of RAID, if possible.

To convert an MBR partition table to GPT using *sgdisk*, use the `-g`/`--mbrtogpt` option:

```
# sgdisk -g /dev/sda

```

To convert GPT to MBR use the `-m`/`--gpttombr` option. Note that it is not possible to convert more than four partitions from GPT to MBR.

```
# sgdisk -m /dev/sda

```

### Sort partitions

This applies for when a new partition is created in the space between two partitions or a partition is deleted. `/dev/sda` is used in this example.

```
# sgdisk -s /dev/sda

```

After sorting the partitions if you are not using [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming"), it might be required to adjust the `/etc/fstab` and/or the `/etc/crypttab` configuration files.

**Note:** The kernel must read the new partition table for the partitions (e.g. `/dev/sda1`) to be usable. Reboot the system or tell the kernel to [reread the partition table](https://serverfault.com/questions/36038/reread-partition-table-without-rebooting).

### Recover GPT header

In case main GPT header or backup GPT header gets damaged, you can recover one from the other with *gdisk*. `/dev/sda` is used in this example.

```
# gdisk /dev/sda

```

choose `r` for recovery and transformation options (experts only). From there choose either

*   `b`: use backup GPT header (rebuilding main)
*   `d`: use main GPT header (rebuilding backup)

When done write the table to disk and exit via the `w` command.

### Expand a GPT disk

After enlarging a disk (e.g. in hardware [RAID](/index.php/RAID "RAID") or a [virtual machine](/index.php/Virtual_machine "Virtual machine") disk) the newly added free space will not be immediately usable since GPT keeps data at the end of the disk. You must relocate the backup GPT header to the new end of the disk.

Run *sgdisk* with the option `-e`/`--move-second-header`, e.g.:

```
# sgdisk -e /dev/sda

```

Afterwards [print the partition table](#List_partitions); the total free space should now be increased.

### Prevent GPT partition automounting

[systemd-gpt-auto-generator(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-gpt-auto-generator.8) will automount partitions following the [Discoverable Partitions Specification](https://www.freedesktop.org/wiki/Specifications/DiscoverablePartitionsSpec/). Sometimes that may not be desirable.

The automounting can be disabled by setting the [partition attribute](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_entries_.28LBA_2-33.29 "wikipedia:GUID Partition Table") `63` "do not automount" on the partition.

Start *gdisk*, e.g.:

```
# gdisk /dev/sda

```

Press `p` to print the partition table and take note of the partition number(s) of the for which you want to disable automounting.

Press `x` *extra functionality (experts only)*.

Press `a` *set attributes*. Input the partition number and set the attribute `63`. Under `Set fields are:` it should now show `63 (do not automount)`. Press `Enter` to end attribute changing. Repeat this for all partitions you want to prevent from automounting.

When done write the table to disk and exit via the `w` command.

Alternatively using *sgdisk*, the attribute can be set using the `-A`/`--attributes=` option; see [sgdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sgdisk.8) for usage. For example, to set partition attribute `63` "do not automount" on `/dev/sda2` run:

```
# sgdisk -A 2:set:63 /dev/sda

```

### gdisk EFI application

There is no package for the EFI version of gdisk, but Rod Smith provides a prebuilt gdisk EFI binary on [SourceForge](https://sourceforge.net/projects/gptfdisk/files/gptfdisk/). Download `gdisk-efi-*.zip` and extract the archive. To use it, copy `gdisk_x64.efi` to the [EFI system partition](/index.php/EFI_system_partition "EFI system partition") and launch it from your [boot loader](/index.php/Boot_loader "Boot loader") or [UEFI Shell](/index.php/Unified_Extensible_Firmware_Interface#UEFI_Shell "Unified Extensible Firmware Interface").

*gdisk_x64.efi* allows you to edit the partition table before the operating system is even booted. It is used the same way as the *gdisk* binary on Linux.

**Note:** *gdisk_x64.efi* cannot access the file system, thus it cannot backup the partition table or restore it from backup.

See [README-efi.txt](https://sourceforge.net/p/gptfdisk/code/ci/master/tree/README-efi.txt) for more information.

## See also

*   [GPT fdisk Tutorial](https://www.rodsbooks.com/gdisk/index.html) - offical webpage of GPT fdisk with detailed walkthroughs.
*   [GPT fdisk's SourceForge page](https://sourceforge.net/projects/gptfdisk/)