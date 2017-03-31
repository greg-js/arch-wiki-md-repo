**翻译状态：** 本文是英文页面 [GNU_Parted](/index.php/GNU_Parted "GNU Parted") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-10-07，点击[这里](https://wiki.archlinux.org/index.php?title=GNU_Parted&diff=0&oldid=440534)可以查看翻译后英文页面的改动。

GNU Parted 是创建和处理分区表的工具，[GParted](/index.php/GParted "GParted") 是图形前端.

## Contents

*   [1 Installation](#Installation)
*   [2 使用](#.E4.BD.BF.E7.94.A8)
    *   [2.1 Command line mode](#Command_line_mode)
    *   [2.2 Interactive mode](#Interactive_mode)
*   [3 Rounding](#Rounding)
*   [4 Partitioning](#Partitioning)
    *   [4.1 创建新分区表](#.E5.88.9B.E5.BB.BA.E6.96.B0.E5.88.86.E5.8C.BA.E8.A1.A8)
    *   [4.2 分区方案](#.E5.88.86.E5.8C.BA.E6.96.B9.E6.A1.88)
        *   [4.2.1 UEFI/GPT 示例](#UEFI.2FGPT_.E7.A4.BA.E4.BE.8B)
        *   [4.2.2 BIOS/MBR 示例](#BIOS.2FMBR_.E7.A4.BA.E4.BE.8B)
    *   [4.3 Resizing Partitions](#Resizing_Partitions)
        *   [4.3.1 Growing partitions](#Growing_partitions)
        *   [4.3.2 Shrinking partitions](#Shrinking_partitions)
*   [5 警告](#.E8.AD.A6.E5.91.8A)
    *   [5.1 分区对齐](#.E5.88.86.E5.8C.BA.E5.AF.B9.E9.BD.90)
*   [6 See also](#See_also)

## Installation

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [parted](https://www.archlinux.org/packages/?name=parted)。

## 使用

Parted has two modes: command line and interactive. Parted should always be started with:

```
# parted device

```

where `*device*` is the hard disk device to edit (for example `/dev/sda`). If you omit the `*device*` argument, *parted* will attempt to guess which device you want.

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
# parted /dev/sd*x*

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

### 创建新分区表

如果设备没有分区，或者要改变分区表类型，重建分区结构，需要新建分区表。

打开需要新建分区表的设备：

```
# parted /dev/sd*x*

```

为 BIOS 系统创建 MBR/msdos 分区表：

```
(parted) mklabel msdos

```

为 UEFI 系统创建 GPT 分区表：

```
(parted) mklabel gpt

```

### 分区方案

您可以决定磁盘应该分为多少个区，每个分区又挂载在系统的哪个目录。将分区如何映射至目录（一般称此为挂载点），取决于您的[分区方案](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.88.86.E5.8C.BA.E6.96.B9.E6.A1.88 "Partitioning (简体中文)")。需要满足：

*   至少需要创建一个 `/` (*root*) 目录，有些分区类型和 [启动加载器](/index.php/Boot_loaders_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Boot loaders (简体中文)")组合有额外的分区要求：
*   BIOS/GPT + [GRUB](/index.php/GRUB "GRUB"): 需要按照 [BIOS 启动分区设置](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB") 的方式创建一个 1M 或 2M 的 `EF02` 类型分区.
*   UEFI 的主板，需要一个 [EFI 系统分区](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface").
*   如果您需要[加密磁盘](/index.php/Disk_encryption "Disk encryption")，则必须加以调整分区方案。系统安装后，也可以再配置加密文件夹，容器或 home 目录。

系统需要需要 `/boot`、`/home` 等目录， [Arch 文件系统架构](/index.php/Arch_filesystem_hierarchy "Arch filesystem hierarchy") 有各目录的详细介绍。如果没有创建单独的`/boot` 或 `/home` 分区，这些目录直接放到了根分区下面。后面会介绍如何创建 [交换分区](/index.php/Swap_space "Swap space")。

In the examples below it is assumed that a new and contiguous partitioning scheme is applied to a single device. Some optional partitions will also be created for the `/boot` and `/home` directories: see also [Arch filesystem hierarchy](/index.php/Arch_filesystem_hierarchy "Arch filesystem hierarchy") for an explanation of the purpose of the various directories; if separate partitions for directories like `/boot` or `/home` are not created, these will simply be contained in the `/` partition. Also the creation of an optional partiton for [swap space](/index.php/Swap_space "Swap space") will be illustrated.

用下面命令打开 parted 交互模式：

```
# parted /dev/sd*x*

```

用下面命令创建分区：

```
(parted) mkpart *part-type* *fs-type* *start* *end*

```

*   `*part-type*` 是分区类型，可以选择 `primary`, `extended` 或 `logical`，仅用于 MBR 分区表.
*   `*fs-type*` 是文件系统类型，支持的类型列表可以通过 `help mkpart` 查看。 mkpart 并不会实际创建文件系统， `*fs-type*` 参数仅是让 *parted* 设置一个 1-byte 编码，让启动管理器可以提前知道分区中有什么格式的数据。参阅 [Wikipedia:Disk partitioning#PC partition types](https://en.wikipedia.org/wiki/Disk_partitioning#PC_partition_types "wikipedia:Disk partitioning").

**Tip:** Most [Linux native file systems](https://en.wikipedia.org/wiki/File_system#Linux "wikipedia:File system") map to the same partition code ([0x83](https://en.wikipedia.org/wiki/Partition_type#PID_83h "wikipedia:Partition type")), so it is perfectly safe to e.g. use `ext2` for an *ext4*-formatted partition.

*   `*start*` 是分区的起始位置，可以带[单位](http://www.gnu.org/software/parted/manual/parted.html#unit), 例如 `1M` 指 1MiB.
*   `*end*` 是设备的结束位置(**不是** 与 `*start*` 值的差)，同样可以带单位，也可以用百分比，例如 `100%` 表示到设备的末尾。
*   为了不留空隙，分区的开始和结束应该首尾相连。

**Warning:** It is important that the partitions do not overlap each other: if you do not want to leave unused space in the device, make sure that each partition starts where the previous one ends.

如果看到下面警告：

```
Warning: The resulting partition is not properly aligned for best performance.
Ignore/Cancel?

```

表示分区没 [对齐](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.88.86.E5.8C.BA.E5.AF.B9.E9.BD.90 "Partitioning (简体中文)")，请按照 [分区对齐](#.E5.88.86.E5.8C.BA.E5.AF.B9.E9.BD.90) 进行修正。

下面命令设置 `/boot` 为启动目录：

```
(parted) set *partition* boot on

```

*   `*partition*` 是分区的编号，从 `print` 命令获取。

#### UEFI/GPT 示例

首先需要一个 [EFI 系统分区](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface").如果是和 Windows 双系统启动，此分区已经存在，不要重新创建。

用下面命令创建分区 (建议大小是 512MiB)。

```
(parted) mkpart ESP fat32 1M 513M
(parted) set 1 boot on

```

剩下的空间可以按需要创建，root 占用全部 100% 剩余空间：

```
(parted) mkpart primary ext4 513M 100%

```

`/` (20GiB)，剩下的给 `/home`：

```
(parted) mkpart primary ext4 513M 20.5G
(parted) mkpart primary ext4 20.5G 100%

```

创建 `/` (20GiB), swap (4Gib), 剩下给 `/home`：

```
(parted) mkpart primary ext4 513M 20.5G
(parted) mkpart primary linux-swap 20.5G 24.5G
(parted) mkpart primary ext4 24.5G 100%

```

#### BIOS/MBR 示例

单根目录分区：

```
(parted) mkpart primary ext4 1M 100%
(parted) set 1 boot on

```

20Gib `/` 分区，剩下的给 `/home`：

```
(parted) mkpart primary ext4 1M 20G
(parted) set 1 boot on
(parted) mkpart primary ext4 20G 100%

```

`/boot` (100MiB), `/` (20Gib), swap (4GiB) 剩下的给 `/home`:

```
(parted) mkpart primary ext4 1M 100M
(parted) set 1 boot on
(parted) mkpart primary ext4 100M 20G
(parted) mkpart primary linux-swap 20G 24G
(parted) mkpart primary ext4 24G 100%

```

### Resizing Partitions

**Warning:** Partitions that are being resized must be unmounted and not in use. If it cannot be done (e.g. the partition that mounts to `/`), use a live media/rescue system.

**Note:**

*   You can only move the end of the partition with `parted`.
*   As of parted v4.2 *resizepart* may need the use of [#Interactive mode](#Interactive_mode).[[1]](https://bugs.launchpad.net/ubuntu/+source/parted/+bug/1270203)
*   These instructions apply to partitions that have ext2, ext3 or ext4 filesystems.

If you are growing a partition, you have to first resize the partition and then resize the filesystem on it, while for shrinking the filesystem must be resized before the partition to avoid data loss.

#### Growing partitions

To grow a partition (in parted interactive mode):

```
(parted) resizepart *number* *end*

```

Where `*number*` is the number of the partition you are growing, and `*end*` is the new end of the partition (which needs to be larger than the old end).

Then, to grow the filesystem on the partition:

```
# resize2fs /dev/*sdaX* *size*

```

Where `*sdaX*` stands for the partition you are growing, and `*size*` is the new size of the partition.

#### Shrinking partitions

To shrink the filesystem on the partition:

```
# resize2fs /dev/*sdaX* *size*

```

Where `*sdaX*` stands for the partition you are growing, and `*size*` is the new size of the partition.

Then shrink the partition (in parted interactive mode):

```
(parted) resizepart *number* *end*

```

Where `*number*` is the number of the partition you are shrinking, and `*end*` is the new end of the partition (which needs to be smaller than the old end).

When done, use the *resizepart* command from [util-linux](https://www.archlinux.org/packages/?name=util-linux) to tell the kernel about the new size:

```
# resizepart *device* *number* *size*

```

Where `*device*` is the device that holds the partition, `*number*` is the number of the partition and `*size*` is the new size of the partition.

## 警告

Parted will always warn you before doing something that is potentially dangerous, unless the command is one of those that is inherently dangerous (viz., rm, mklabel and mkpart).

### 分区对齐

When creating a partition, *parted* might warn about improper partition alignment but does not hint about proper alignment. For example:

```
(parted) mkpart primary fat16 0 32M
Warning: The resulting partition is not properly aligned for best performance.
Ignore/Cancel?                                                     

```

The warning means the partition start is not aligned. Enter "Ignore" to go ahead anyway, print the partition table in sectors to see where it starts, and remove/recreate the partition with the start sector rounded up to increasing powers of 2 until the warning stops. As one example, on a flash drive with 512B sectors, Parted wanted partitions to start on sectors that were a multiple of 2048, which is 1 MiB alignment.

If you want *parted* to attempt to calculate the correct alignment for you, specify the start position as 0% instead of some concrete value. To make one large ext4 partition, your command would look like this:

```
(parted) mkpart primary ext4 0% 100%

```

## See also

*   [GNU parted - Parted User's Manual](https://www.gnu.org/software/parted/manual/)
*   [How to align partitions for best performance using parted](http://rainbow.chard.org/2013/01/30/how-to-align-partitions-for-best-performance-using-parted/)
*   [Resize an ext3/ext4 partition](http://positon.org/resize-an-ext3-ext4-partition)