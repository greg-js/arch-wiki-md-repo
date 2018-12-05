相关文章

*   [GNU Parted](/index.php/GNU_Parted "GNU Parted")
*   [Gparted-Live](/index.php/Gparted-Live "Gparted-Live")
*   [Partitioning](/index.php/Partitioning "Partitioning")

**翻译状态：** 本文是英文页面 [Parted](/index.php/Parted "Parted") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-12-05，点击[这里](https://wiki.archlinux.org/index.php?title=Parted&diff=0&oldid=558274)可以查看翻译后英文页面的改动。

[GNU Parted](https://www.gnu.org/software/parted/parted.html) 是创建和处理分区表的程序。GParted 是 GUI 前端。

## Contents

*   [1 安装](#安装)
*   [2 使用](#使用)
    *   [2.1 命令行模式](#命令行模式)
    *   [2.2 交互模式](#交互模式)
*   [3 数值设定](#数值设定)
*   [4 Partitioning](#Partitioning)
    *   [4.1 创建新分区表](#创建新分区表)
    *   [4.2 分区方案](#分区方案)
        *   [4.2.1 UEFI/GPT 示例](#UEFI/GPT_示例)
        *   [4.2.2 BIOS/MBR 示例](#BIOS/MBR_示例)
    *   [4.3 Resizing partitions](#Resizing_partitions)
        *   [4.3.1 Growing partitions](#Growing_partitions)
        *   [4.3.2 Shrinking partitions](#Shrinking_partitions)
*   [5 Warnings](#Warnings)
    *   [5.1 Alignment](#Alignment)
*   [6 小技巧](#小技巧)
    *   [6.1 双启动 Windows XP](#双启动_Windows_XP)
    *   [6.2 Check alignment](#Check_alignment)

## 安装

从[官方源](/index.php/%E5%AE%98%E6%96%B9%E6%BA%90 "官方源")[安装](/index.php/Pacman "Pacman") 软件包 [parted](https://www.archlinux.org/packages/?name=parted), 要使用图像界面，安装 [gparted](https://www.archlinux.org/packages/?name=gparted)。

## 使用

Parted 有两种模式：命令行和交互，请用下面命令启动：

```
# parted device

```

`*device*` 是要编辑的硬盘设备(例如 `/dev/sda`)。如果忽略了 `*device*` 参数，*parted* 将尝试猜测要使用的设备。

### 命令行模式

在命令行模式下，可以同时执行一个或多个命令：

```
# parted /dev/sda mklabel gpt mkpart P1 ext3 1MiB 8MiB 

```

**注意:** `--help` 等参数只有在命令行中才能指定。

### 交互模式

交互模式简化了分区过程，可以自动对设备执行分区操作。打开需要新建分区表的设备：

```
# parted /dev/sd*x*

```

命令提示符会从 (`#`) 变成 `(parted)`: 要查看可用的命令：

```
(parted) help

```

完成操作后，用下面命令退出：

```
(parted) quit

```

退出后命令提示符变成 `#`.

如果命令没带参数，Parted 会进行询问：

```
(parted) mklabel
New disk label type? gpt

```

## 数值设定

很多分区系统有复杂的限制，Parted 可能会对输入的数值进行稍微的修改。例如设定了 10.4Mb，实际会使用 10.352Mb。如果修正后的数值差异太大，Parted 会进行提示确认。用扇区数值("s" 后缀)可以进行精确的数值设置。

parted 2.4 开始，当使用 “MiB”, “GiB”, “TiB” 等 IEC 单位时，parted 会使用精确数值，不进行修正。而使用 “4GB” 这样的设置时，可能会落在前后 500MB 的未知。所以在创建分区时，应该指定比特(“B”)、扇区(“s”)或 IEC 二进制单位 “MiB”，不要使用 “MB”, “GB”。

## Partitioning

### 创建新分区表

如果设备没有分区，或者要改变分区表类型，重建分区结构，需要新建分区表。

用下面命令打开分区：

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
*   BIOS/GPT + [GRUB](/index.php/GRUB "GRUB"): 需要按照 [BIOS 启动分区设置](/index.php/GRUB#GUID_Partition_Table_(GPT)_specific_instructions "GRUB") 的方式创建一个 1M 或 2M 的 `EF02` 类型分区.
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

表示分区没 [对齐](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#分区对齐 "Partitioning (简体中文)")，请按照 [分区对齐](#分区对齐) 进行修正。

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

### Resizing partitions

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

Where `*sdaX*` stands for the partition you are shrinking, and `*size*` is the new size of the partition.

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

## Warnings

Parted will always warn you before doing something that is potentially dangerous, unless the command is one of those that is inherently dangerous (viz., rm, mklabel and mkpart).

### Alignment

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

## 小技巧

### 双启动 Windows XP

如果您打算将一个同属于启动分区的 Windows XP 分区移动到另一块硬盘，只要将以下的注册表删除，之后就可以用 GParted 轻易地操作，Windows 不会出现任何问题:

```
HKEY_LOCAL_MACHINE\SYSTEM\MountedDevices

```

相关资料参见[这里](http://gparted-forum.surf4.info/viewtopic.php?pid=8347#p8347)。

### Check alignment

On an already partitioned disk, you can use *parted* to verify the alignment of a partition on a device. For instance, to verify alignment of partition 1 on `/dev/sda`:

```
# parted /dev/sda
(parted) align-check optimal 1
1 aligned

```