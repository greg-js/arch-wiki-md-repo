相关文章

*   [Partitioning (简体中文)](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Partitioning (简体中文)")
*   [fdisk (简体中文)](/index.php/Fdisk_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fdisk (简体中文)")
*   [GNU Parted (简体中文)](/index.php/GNU_Parted_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNU Parted (简体中文)")

[GPT fdisk](https://www.rodsbooks.com/gdisk/) 是编辑 GPT（Globally Unique Identifier Partition Table）硬盘的文本模式工具集。由 gdisk, sgdisk 和 cgdisk 组成. 用于 GPT 而不是老的 MBR(Master Boot Record) 分区表。

本文介绍 [gdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gdisk.8) 和 [sgdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sgdisk.8) 工具。

**Tip:**

*   [cgdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cgdisk.8) 提供了基本的功能和命令行用户界面。
*   GPT fdisk 网站包含了一个 [gdisk](https://www.rodsbooks.com/gdisk/walkthrough.html), [cgdisk](https://www.rodsbooks.com/gdisk/cgdisk-walkthrough.html), [sgdisk](https://www.rodsbooks.com/gdisk/sgdisk-walkthrough.html) 和[FixParts](https://www.rodsbooks.com/fixparts/) 的详细使用步骤。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 显示分区](#.E6.98.BE.E7.A4.BA.E5.88.86.E5.8C.BA)
*   [3 备份和恢复分区表](#.E5.A4.87.E4.BB.BD.E5.92.8C.E6.81.A2.E5.A4.8D.E5.88.86.E5.8C.BA.E8.A1.A8)
*   [4 创建分区表和分区](#.E5.88.9B.E5.BB.BA.E5.88.86.E5.8C.BA.E8.A1.A8.E5.92.8C.E5.88.86.E5.8C.BA)
    *   [4.1 创建新分区表](#.E5.88.9B.E5.BB.BA.E6.96.B0.E5.88.86.E5.8C.BA.E8.A1.A8)
    *   [4.2 创建分区](#.E5.88.9B.E5.BB.BA.E5.88.86.E5.8C.BA)
        *   [4.2.1 分区编号](#.E5.88.86.E5.8C.BA.E7.BC.96.E5.8F.B7)
        *   [4.2.2 First and last sector](#First_and_last_sector)
        *   [4.2.3 Partition type](#Partition_type)
    *   [4.3 Write changes to disk](#Write_changes_to_disk)
*   [5 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [5.1 在 MBR 和 GPT 之间转换](#.E5.9C.A8_MBR_.E5.92.8C_GPT_.E4.B9.8B.E9.97.B4.E8.BD.AC.E6.8D.A2)
    *   [5.2 Sort partitions](#Sort_partitions)
    *   [5.3 Recover GPT header](#Recover_GPT_header)
    *   [5.4 Expand a GPT disk](#Expand_a_GPT_disk)
    *   [5.5 Prevent GPT partition automounting](#Prevent_GPT_partition_automounting)
*   [6 参阅](#.E5.8F.82.E9.98.85)

## 安装

[安装](/index.php/Install "Install") 软件包 [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk)。

## 显示分区

要显示分区表和分区信息，以 `/dev/sda` 磁盘为例:

```
# gdisk -l /dev/sda

```

或者使用 *sgdisk* 命令:

```
# sgdisk -p /dev/sda

```

## 备份和恢复分区表

习惯磁盘前，请先备份磁盘的分区表，也可以将磁盘信息备份到相同的设备上。

*sgdisk* 可以创建一个二进制备份，包含 MBR, GPT 主表头，GPT 备份表头和分区表。下面示例将 `/dev/sda` 的分区表信息备份到 `sgdisk-sda.bin`:

```
# sgdisk -b=sgdisk-sda.bin /dev/sda

```

通过下面命令恢复备份:

```
# sgdisk -l=sgdisk-sda.bin /dev/sda

```

如果要复制分区到其它磁盘，例如从 `/dev/sda` 复制到 `/dev/sdc`:

```
# sgdisk -R=/dev/sdc /dev/sda

```

如果两个磁盘位于同一个计算机，使用下面命令设置随机的分区 GUIDs:

```
# sgdisk -G /dev/sdc

```

## 创建分区表和分区

The first step to [partitioning](/index.php/Partitioning "Partitioning") a disk is making a partition table. After that, the actual partitions are created according to the desired [partition scheme](/index.php/Partition_scheme "Partition scheme").

Before beginning, you may wish to [backup](#Backup_and_restore_partition_table) your current partition table and scheme.

The following shows how to use *gdisk* to perform both the creation of a partition table and the creation of the actual partitions. Alternatively, you may use the curses-based version called *cgdisk*; however, the following instructions do not apply to it. See [cgdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cgdisk.8) for its usage.

performs partition alignment automatically on a 2048 512-byte sector (1 MiB) block size base which should be compatible with all [Advanced Format](/index.php/Advanced_Format "Advanced Format") HDDs and the vast majority of [SSDs](/index.php/SSD "SSD") if not all.

*gdisk* 自动将分区按 2048 512-byte 扇区（1 MiB）对齐，这个设置兼容所有 [Advanced Format](/index.php/Advanced_Format "Advanced Format") HDD 和大部分的 [SSD](/index.php/SSD "SSD")。

要使用 *gdisk*, 将要编辑的分区作为命令参数, 例如要编辑 `/dev/sda`:

```
# gdisk /dev/sda

```

### 创建新分区表

**Warning:** If you create a new partition table on a disk with data on it, it will erase all the data on the disk. Make sure this is what you want to do.

如果是全新的磁盘，或要清空所有当前分区表数据，使用 `o` 命令建立一个新的空 GUID 分区表，如果分区已经创建分区，请跳过此步骤。

### 创建分区

使用 `n` 命令创建一个新的分区. You must enter the partition number, first sector, last sector and the partition type.

**Note:** See [Partitioning#Partition scheme](/index.php/Partitioning#Partition_scheme "Partitioning") for considerations concerning the size and location of partitions.

**Tip:**

*   It is advised to follow the [Discoverable Partitions Specification](https://www.freedesktop.org/wiki/Specifications/DiscoverablePartitionsSpec/) since [systemd-gpt-auto-generator(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-gpt-auto-generator.8) will automount them. See [#Prevent GPT partition automounting](#Prevent_GPT_partition_automounting) if you want to disable automounting for a partition.
*   Leave a 1 MiB free space somewhere in the first 2 TiB of the disk (e.g. by using `+1M` as the first sector of a partition) in case you ever need to create a [BIOS boot partition](/index.php/BIOS_boot_partition "BIOS boot partition").

*   如果可能需要建立一个 [BIOS boot partition](/index.php/BIOS_boot_partition "BIOS boot partition")，在磁盘前 2TiB 内预留一个 1MiB 的空间，例如用 `+1M` 在磁盘最前面空出一段。

#### 分区编号

A partition number is the number assigned to a partition, e.g. a partition with number `1` on a disk `/dev/sda` would be `/dev/sda1`. Partition numbers may not always match the order of partitions on disk, in which case they can be [sorted](#Sort_partitions).

It is advised to choose the default number suggested by *gdisk*.

#### First and last sector

The first and last sectors of the partition can be specified in sector numbers or as positions measured in kibibytes (`K`), mebibytes (`M`), gibibytes (`G`), tebibytes (`T`), or pebibytes (`P`);

The position can be specified in:

*   absolute terms from the star of the disk. E.g. `40M` as a first sector specifies a position 40 MiB from the start of the disk.
*   relative terms by preceding the size with `**+***size*` or `**-***size*`. E.g. `+2G` to specify a point 2 GiB after the default start sector, or `-200M` to specify a point 200 MiB before the last available sector.

Pressing the `Enter` key with no input specifies the default value, which is the start of the largest available block for the first sector and the end of the same block for the last sector.

**Tip:** When partitioning it is always a good idea to specify partition sizes using relative terms with the `+*size{M,G,T,P}*` notation and not use sizes smaller than 1 MiB. Such partitions will always be aligned according to the device properties.

#### Partition type

Select the partition's type by entering gdisk's internal type code or specifying the manually. The default, `Linux filesystem` (GUID `0FC63DAF-8483-4772-8E79-3D69D8477DE4`, gdisk's internal code `8300`), should be fine for most use cases.

选择 gdisk 类型编码或手动输入[分区类型 GUID](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table")，默认的 `Linux filesystem` 的 gdisk 代码是 `8300`，GUID 是 `0FC63DAF-8483-4772-8E79-3D69D8477DE4`，在大多数情况下都可以使用此类型。

<caption>Common partition types</caption>
| Partition type | Mountpoint | gdisk's

code

 | [Partition type GUID](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table") |
| Linux filesystem | Any | `8300` | `0FC63DAF-8483-4772-8E79-3D69D8477DE4` |
| [EFI system partition](/index.php/EFI_system_partition "EFI system partition") | Any | `ef00` | `C12A7328-F81F-11D2-BA4B-00A0C93EC93B` |
| [BIOS boot partition](/index.php/BIOS_boot_partition "BIOS boot partition") | None | `ef02` | `21686148-6449-6E6F-744E-656564454649` |
| [Linux x86-64 root (/)](/index.php/Partitioning#.2F "Partitioning") | `/` | `8304` | `4F68BCE3-E8CD-4DB1-96E7-FBCAF984B709` |
| [Linux swap](/index.php/Partitioning#Swap "Partitioning") | `[SWAP]` | `8200` | `0657FD6D-A4AB-43C4-84E5-0933C84B4F4F` |
| [Linux /home](/index.php/Partitioning#.2Fhome "Partitioning") | `/home` | `8302` | `933AC7E1-2EB4-4F13-B844-0E14E2AEF915` |
| [Linux /srv](/index.php/Partitioning#Discrete_partitions "Partitioning") | `/srv` | `8306` | `3B8F8425-20E0-4F3B-907F-1A25A76F98E8` |
| [Linux LVM](/index.php/LVM#Create_partitions "LVM") | Any | `8e00` | `E6D6D379-F507-44C2-A23C-238F2A3DF928` |
| [Linux RAID](/index.php/RAID#GUID_Partition_Table "RAID") | Any | `fd00` | `A19D880F-05FC-4D3B-A006-743F0F84911E` |
| [Linux LUKS](/index.php/Dm-crypt/Drive_preparation#Physical_partitions "Dm-crypt/Drive preparation") | Any | `8309` | `CA7D7CCB-63ED-4C53-861C-1742536059CC` |
| [Linux dm-crypt](/index.php/Dm-crypt/Drive_preparation#Physical_partitions "Dm-crypt/Drive preparation") | Any | `8308` | `7FFEC5C9-2D00-49B7-8941-3EA10A5586B7` |

**Tip:** 按下 `L` 可以显示 gdisk 的内部编码列表。

Repeat this procedure until you have the partitions you desire.

### Write changes to disk

**Tip:** Use the command `c` to change a partition's name ([PARTLABEL](/index.php/Persistent_block_device_naming#by-partlabel "Persistent block device naming")) for easy identification.

使用 `w` 命令将分区表写入磁盘并退出。

## 提示和技巧

### 在 MBR 和 GPT 之间转换

**Tip:** 更多信息请阅读 Rod Smith 的 [MBR 到 GPT 转换说明](https://www.rodsbooks.com/gdisk/mbr2gpt.html)。

转换之后，需要重新安装 [boot loaders](/index.php/Boot_loader "Boot loader") 并配置为从 GPT 启动。

gdisk、sgdisk 和 cgdisk 能将 MBR 和 [BSD 盘符](https://en.wikipedia.org/wiki/BSD_disklabel "wikipedia:BSD disklabel") 无损转换为 GPT。转换时，所有 MBR 主分区和逻辑分区都会变成 GPT 分区并生成有正确的分区类型 GUID 和唯一分区 GUID.

**Warning:**

*   GPT 在硬盘末尾存储了第二分区表。这个数据结构默认有 33512B 空间。MBR 不具有类似数据结构，这意味着 MBR 硬盘的最后一个分区的最后一部分可能被占用进而妨碍到完全的转换。如果这发生在你身上，你必须放弃转换，改变最后一个分区的大小。
*   在 RAID 模式下的基于 Intel的笔记本有一些关于备份 GPT 表损坏的问题，解决方法是尽可能使用 AHCI 替代 RAID.

只需打开 MBR, 用 gdisk 的"w"选项来把改变写入到硬盘(和 fdisk 类似)以转换到 GPT. **警惕所有错误并在写入硬盘之前修复它们**，因为你会有损失数据的风险。

要用 *sgdisk* 将 MBR 分区表转换为 GPT，使用 `-g`/`--mbrtogpt` 选项:

```
# sgdisk -g /dev/sda

```

要将 GPT 转换为 MBR，使用 `-m`/`--gpttombr` 选项，注意最多只能转换四个分区。

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

## 参阅

*   [GPT fdisk Tutorial](https://www.rodsbooks.com/gdisk/index.html) - offical webpage of GPT fdisk with detailed walkthroughs.
*   [GPT fdisk's SourceForge page](https://sourceforge.net/projects/gptfdisk/)