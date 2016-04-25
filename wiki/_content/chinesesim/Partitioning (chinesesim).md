**翻译状态：** 本文是英文页面 [Partitioning](/index.php/Partitioning "Partitioning") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-09-17，点击[这里](https://wiki.archlinux.org/index.php?title=Partitioning&diff=0&oldid=335810)可以查看翻译后英文页面的改动。

*分区* 硬盘的可用空间可以划分为多个逻辑区块，区块之间的访问是相互独立的。

可以为一个硬盘划分一个或者多个分区。一些场景需要使用多个分区：例如双重或多重启动，或使用 [swap](/index.php/Swap "Swap") 分区。此外，分区也可以从逻辑上隔离数据，例如为音频和视频数据创建单独的分区。下面将会讨论通用的分区方案。

每个分区在使用前需要格式化为 [文件系统](/index.php/File_systems_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "File systems (简体中文)") 。

## Contents

*   [1 分区表](#.E5.88.86.E5.8C.BA.E8.A1.A8)
    *   [1.1 Master Boot Record](#Master_Boot_Record)
    *   [1.2 GUID 分区表](#GUID_.E5.88.86.E5.8C.BA.E8.A1.A8)
    *   [1.3 Btrfs 分区](#Btrfs_.E5.88.86.E5.8C.BA)
    *   [1.4 选择GPT 还是 MBR](#.E9.80.89.E6.8B.A9GPT_.E8.BF.98.E6.98.AF_MBR)
*   [2 分区方案](#.E5.88.86.E5.8C.BA.E6.96.B9.E6.A1.88)
    *   [2.1 单root分区](#.E5.8D.95root.E5.88.86.E5.8C.BA)
    *   [2.2 多分区](#.E5.A4.9A.E5.88.86.E5.8C.BA)
    *   [2.3 挂载点](#.E6.8C.82.E8.BD.BD.E7.82.B9)
        *   [2.3.1 根分区](#.E6.A0.B9.E5.88.86.E5.8C.BA)
        *   [2.3.2 /boot](#.2Fboot)
        *   [2.3.3 /home](#.2Fhome)
        *   [2.3.4 /var](#.2Fvar)
        *   [2.3.5 /tmp](#.2Ftmp)
        *   [2.3.6 Swap](#Swap)
        *   [2.3.7 分区应该设置多大？](#.E5.88.86.E5.8C.BA.E5.BA.94.E8.AF.A5.E8.AE.BE.E7.BD.AE.E5.A4.9A.E5.A4.A7.EF.BC.9F)
*   [3 分区工具](#.E5.88.86.E5.8C.BA.E5.B7.A5.E5.85.B7)
*   [4 分区对齐](#.E5.88.86.E5.8C.BA.E5.AF.B9.E9.BD.90)
    *   [4.1 机械硬盘](#.E6.9C.BA.E6.A2.B0.E7.A1.AC.E7.9B.98)
    *   [4.2 固态硬盘](#.E5.9B.BA.E6.80.81.E7.A1.AC.E7.9B.98)
    *   [4.3 分区工具](#.E5.88.86.E5.8C.BA.E5.B7.A5.E5.85.B7_2)
*   [5 参考资料](#.E5.8F.82.E8.80.83.E8.B5.84.E6.96.99)

## 分区表

分区信息被存放在分区表中。目前有两种主流的模式：传统的 [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record")，和新的 [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table")。后者功能更强大，解决了许多MBR的限制。

### Master Boot Record

MBR原本只支持最多4个分区。后来加入了扩展分区和逻辑分区以绕过这个限制。

目前有三中分区类型：

*   主分区（Primary）
*   扩展分区（Extended）
    *   逻辑分区（Logical）

**主分区**每个磁盘或者RAID卷上只能有4个，可设置为可启动状态。如果分区方案要求使用4个以上的分区，就需要使用一个包含**逻辑分区**的**扩展分区**。扩展分区可以被看作是容纳逻辑分区的容器。硬盘上最多只能有1个扩展分区。如果磁盘上有1个扩展分区，它也被看作是1个主分区。因此只能另外再建立3个主分区（例如3个主分区加1个扩展分区）。扩展分区内所包含的逻辑分区数量没有限制。如果在双重启动中有Windows，Windows需要占据一个主分区。

通常习惯是创建主分区*sda1*到*sda3*，然后建立一个扩展分区*sda4*。*sda4*中包含*sda5*，*sda6*等逻辑分区。

请参考 [Wikipedia](https://en.wikipedia.org/wiki/zh:Main_Page "wikipedia:zh:Main Page") 以获取更多关于本主题的信息: **[主引导记录](https://en.wikipedia.org/wiki/zh:%E4%B8%BB%E5%BC%95%E5%AF%BC%E8%AE%B0%E5%BD%95 "wikipedia:zh:主引导记录")**

### GUID 分区表

GPT方案中只有一种分区类型，**主分区**。磁盘和RAID卷中包含的分区数量没有限制。

请参考 [Wikipedia](https://en.wikipedia.org/wiki/zh:Main_Page "wikipedia:zh:Main Page") 以获取更多关于本主题的信息: **[GUID磁碟分割表](https://en.wikipedia.org/wiki/zh:GUID%E7%A3%81%E7%A2%9F%E5%88%86%E5%89%B2%E8%A1%A8 "wikipedia:zh:GUID磁碟分割表")**

### Btrfs 分区

Btrfs可以独占整个存储设备并替代 [MBR](/index.php/MBR "MBR") 和 [GPT](/index.php/GPT "GPT") 分区方案。请参考[Btrfs Partitioning](/index.php/Btrfs#Partitioning "Btrfs")以获取更多信息。

请参考 [Wikipedia](https://en.wikipedia.org/wiki/zh:Main_Page "wikipedia:zh:Main Page") 以获取更多关于本主题的信息: **[Btrfs](https://en.wikipedia.org/wiki/zh:Btrfs "wikipedia:zh:Btrfs")**

### 选择GPT 还是 MBR

[GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table") （GPT）是一种更灵活的分区方式。它正在逐步取代[Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") （MBR）系统。GPT相对于诞生于MS-DOS时代的MBR而言，有许多优点。新版的*fdisk*（MBR）和*gdisk*（GPT）使得使用GPT或者MBR在可靠性和性能最大化上都非常容易。

在做出选择前，需要考虑如下内容：

*   如果使用GRUB legacy作为bootloader，必须使用MBR。
*   如果使用传统的BIOS，并且双启动中包含 Windows （无论是32位版还是64位版），必须使用MBR。
*   如果使用 [UEFI](/index.php/UEFI "UEFI") 而不是BIOS，并且双启动中包含 Windows 64位版，必须使用GPT。
*   如果不属于上述任何一种情况，可以随意选择使用 GPT 还是 MBR。由于 GPT 更先进，建议选择 GPT。
*   建议在使用 [UEFI](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface") 的情况下选择 GPT，因为有些 UEFI firmware 不支持从 MBR 启动。

**注意:** 为了使 GRUB 从一台有 GPT 分区的基于 BIOS 的系统上启动，需要创建一个 [BIOS 启动分区](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB")

## 分区方案

虽然有一些关于分区方案的通用建议，但没有严格的准则。有许多影响分区方案的因素，例如对灵活性的期望，访问速度，安全性以及可用磁盘空间的硬性限制。实际上就是个人取舍的问题。如果你想双启动 Arch Linux 和 Windows，请参考 [Windows and Arch Dual Boot](/index.php/Windows_and_Arch_Dual_Boot "Windows and Arch Dual Boot")。

**警告:** 请别忘记为boot-loader预留空间。这对于 MBR 和 GRUB-Legacy 来说不是问题，但是许多新方案可能要求占用一个特殊的小分区。

### 单root分区

这种是最简单，同时也能满足大部分应用场景的方案。如果需要的话，可以建立一个 [swapfile](/index.php/Swapfile "Swapfile")。通常刚开始的时候建议一个单独的 `/` 分区，然后根据应用场景的需要，例如 RAID，加密，独立的多媒体分区等建立其他的分区。注意，在一个 BIOS 系统上使用 GPT 进行分区后，安装 GRUB 时会需要一个额外的 BIOS 启动分区。

### 多分区

将某个路径挂载为独立分区可以使其拥有不同的文件系统和挂载参数。某些情况下（例如多媒体文件分区），可以被多个操作系统共享。

### 挂载点

下面这些路径可以作为独立分区的挂载点，你也可以根据实际需要做出其他决定。

#### 根分区

根目录是目录树的顶层，这里是主文件系统挂载和其他文件系统挂靠的地方。所有文件和目录都在根目录 `/` 显示，即使它们实际上存储在其他的物理设备上。根文件系统中的内容应该足以启动、恢复、修复系统。因此 `/` 目录下的特定目录是不能作为独立分区的。

`/` 分区或叫根分区是最重要而且必需的。其他其他分区可以被它取代。

**警告:** 与系统启动相关的特定目录（除了 `/boot`） **必须** 与 `/` 在同一个分区，或在系统刚进入用户态的时候通过 [initramfs](/index.php/Initramfs "Initramfs") 挂载。这些特定的目录包括：`/etc` 和 `/usr` [[1]](http://freedesktop.org/wiki/Software/systemd/separate-usr-is-broken) 。

#### /boot

`/boot` 分区包含内核、ramdisk 镜像以及 bootloader 配置文件和 bootloader stage。它也可以存放内核在执行用户态程序之前所使用的其他数据。`/boot` 在日常系统运行中并不需要，只在启动和内核升级（包括重建initial ramdisk）的时候用到。

如果使用软RAID0（条带化）系统的话，必须有一个独立的 `/boot` 分区。

#### /home

`/home`目录包含用户定义的配置文件、缓存、应用程序数据和媒体文件。

将`/home`目录独立使得`/`分区可以单独重新划分，但是请注意你可以在 `/home` 没有独立分区的情况下你仍然可以在不修改 `/home` 目录内容的情况下重装 Arch —— 删除其他顶级目录，然后执行pacstrap。

不能与使用其他发行版的用户共享同一个home目录，因为不同的发行版可能使用不兼容的软件版本和补丁。可以共享媒体目录，或至少使用 `/home` 分区下的不同home目录。

#### /var

`/var` 目录存储变量数据例如 spool 目录和文件，管理和登录数据，[pacman](/index.php/Pacman "Pacman") 的缓存，[ABS](/index.php/ABS "ABS") 树等等。它通常被用作缓存或者日志记录，因此读写频繁。将它独立出来可以避免由于大量日志写入造成的磁盘空间耗尽等问题。

可以将 `/usr` 设置为只读挂载。所有在操作系统运行过程中（例如安装或软件维护）写入 `/usr` 的东西放到 `/var` 下。

**注意:** `/var`包含许多小文件。如果将其作为独立分区，在文件系统的选择上需要考虑这一点。

#### /tmp

默认情况下这个目录已经是一个独立分区，systemd 将其挂载问*tmpfs*。

#### Swap

[swap](/index.php/Swap "Swap") 分区提供能够被作为虚拟内存的内存空间。[swap file](/index.php/Swap#Swap_file "Swap") 也可以实现同样的功能，并且它们之间没有明显的性能区别，但是后者更易于根据需要调整大小。如果没有使用休眠特性的话，swap 分区*可以*被多个系统共享。

#### 分区应该设置多大？

**注意:**

*   以下只是简单的建议，分区大小没有严格的准则
*   如果可能的话，为每个文件系统保留 25% 的额外空间以应对今后的变化，还可以避免文件系统碎片

分区的大小主要取决于个人的选择，以下内容可能会有一定帮助：

	/boot - 200 MB 

	实际需求大约 100 MB，如果有多个内核/启动镜像同时存在，建议分配 200 或者 300 MB。

	/ - 15-20 GB 

	传统上包括 `/usr` 目录，根据安装的软件数量，会产生非常明显的增长。15-20 GB 对于大多数用户来说是一个比较合适的取值。如果你打算在这里放一个交换文件（swap file）的话，需要适当调大取值。

	/var - 8-12 GB 

	除了其他数据以外，还包括[ABS](/index.php/ABS "ABS") 树和 [pacman](/index.php/Pacman "Pacman") 缓存。保留缓存的包提供了包降级的能力，因此非常有用。也正因为这样，`/var` 的大小会随着时间推移而增长。尤其是 pacman 缓存将会随着新软件的安装、系统的升级而增长。在磁盘空间不足的时候，可以安全的清理这个目录。`/var` 分配 8-12 GB 对于桌面系统来说是比较合适的取值，具体取值取决于安装的软件数量。

	/home - [不定] 

	通常用于存放用户数据，下载的文件和媒体文件。在桌面系统中，`/home` 通常是最大的文件系统。

	swap - [不定] 

	历史上 swap 分区的大小通常是物理内存的2倍。由于当前的电脑内存容量快速增长，这条规则已经不那么适用。在拥有不足 512 MB 内存的机器上，通常为 swap 分区分配2倍内存大小的空间。如果有更大的内存（大于 1024 MB），可以分配较少的空间甚至不需要swap 分区。在拥有 2 GB 以上物理内存的情况下，不使用 swap 分区可以获得更好的性能。

**注意:** 如果你要使用休眠到磁盘功能，你需要参考[Suspend and hibernate#About swap partition/file size](/index.php/Suspend_and_hibernate#About_swap_partition.2Ffile_size "Suspend and hibernate")。

	/data - [不定] 

	可以为需要多用户共享的文件建立一个“data”分区。也可以使用 `/home` 分区用于这一目的。

## 分区工具

*   **fdisk** — Linux 自带的命令行分区工具。

	[https://www.kernel.org/](https://www.kernel.org/) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

*   **cfdisk** — 使用 ncurses 库编写的具有伪图形界面的命令行分区工具。

	[https://www.kernel.org/](https://www.kernel.org/) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

**警告:** *cfdisk* 创建的第一个分区起始位置是63扇区而不是通常的2048扇区。这将会在 SSD 和使用高级格式化（4k 扇区）的设备上造成性能问题。[GRUB2](/index.php/GRUB2#msdos-style_error_message "GRUB2") 也会受影响。GRUB legacy 和 Syslinux不受影响。

*   **gdisk** — [GPT](/index.php/GPT "GPT") 版的 fdisk。

	[http://www.rodsbooks.com/gdisk/](http://www.rodsbooks.com/gdisk/) || [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk)

*   **cgdisk** — GPT 版的 cfdisk。

	[http://www.rodsbooks.com/gdisk/](http://www.rodsbooks.com/gdisk/) || [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk)

*   **sgdisk** — Scriptable version of gdisk.

	[http://www.rodsbooks.com/gdisk/sgdisk-walkthrough.html](http://www.rodsbooks.com/gdisk/sgdisk-walkthrough.html) || [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk)

*   **GNU Parted** — 命令行分区工具。

	[http://www.gnu.org/software/parted/parted.html](http://www.gnu.org/software/parted/parted.html) || [parted](https://www.archlinux.org/packages/?name=parted)

*   **[GParted](/index.php/GParted "GParted")** — GTK 图形界面的分区工具。

	[http://gparted.sourceforge.net/](http://gparted.sourceforge.net/) || [gparted](https://www.archlinux.org/packages/?name=gparted)

*   **Partitionmanager** — QT 图形界面的分区工具。

	[http://sourceforge.net/projects/partitionman/](http://sourceforge.net/projects/partitionman/) || [partitionmanager](https://www.archlinux.org/packages/?name=partitionmanager)

*   **QtParted** — 与 Partitionmanager 类似，在 [AUR](/index.php/AUR "AUR") 中可获取。

	[http://qtparted.sourceforge.net/](http://qtparted.sourceforge.net/) || [qtparted](https://aur.archlinux.org/packages/qtparted/)

## 分区对齐

恰当的分区对齐有助于提升性能和使用寿命。这是由硬件层面和文件系统层面的每次[块](https://en.wikipedia.org/wiki/Block_(data_storage) I/O 操作特性决定的。对齐的关健是分区大小（至少）是*块大小*的倍数，*块大小*取决于选用的硬件设备。如果分区没有以*块大小*的整数倍对齐，对齐文件系统就失去意义了，因为从分区的起始偏移开始就是有偏差的。

### 机械硬盘

传统上，机械硬盘是按照*柱面*、*磁头*和*扇区*来寻址需要读写的数据位置（也被称作 [CHS addressing](https://en.wikipedia.org/wiki/Cylinder-head-sector "wikipedia:Cylinder-head-sector")）。这代表了相关数据的径向的位置、驱动器磁头（包括盘片和盘面）和轴向的位置。对于 [LBA (逻辑块寻址)](https://en.wikipedia.org/wiki/Logical_block_addressing "wikipedia:Logical block addressing")，这就不再是这样了。而是整个磁盘被按照连续的数据流寻址，以[扇区](https://en.wikipedia.org/wiki/Disk_sector "wikipedia:Disk sector")作为最小寻址单位。

标准的*扇区大小*是512B，但是现代的高容量机械硬盘使用更大的值，通常是 4KiB。使用高于512B的值被称作[高级格式化](/index.php/Advanced_Format "Advanced Format")

### 固态硬盘

固态硬盘基于[闪存芯片](https://en.wikipedia.org/wiki/Flash_memory "wikipedia:Flash memory")，与机械硬盘有显著的不同。只读访问能够以随机方式进行，而擦除（覆写或随机写入）只能以[整块](https://en.wikipedia.org/wiki/Flash_memory#Block_erasure "wikipedia:Flash memory")进行。此外，*擦除块大小*（Erase Block Size，EBS）比*块大小*明显大很多，例如 128KiB vs 4KiB，所以需要以 EBS 的整数倍进行对齐。

### 分区工具

以前，在分区的时候需要手工计算和介入以确保正确对齐。现在有许多常用的分区工具已经可以自动处理分区对齐问题：

*   fdisk
*   gdisk
*   gparted
*   parted

要验证一个分区是否对齐，像下面这样使用 `/usr/bin/blockdev` 工具进行检查，如果返回值为0，则分区已经对齐：

```
# blockdev --getalignoff /dev/<partition>
0

```

## 参考资料

*   [Creating ext4 partitions from scratch](/index.php/Ext4#Creating_ext4_partitions_from_scratch "Ext4")
*   [Wikipedia:Disk partitioning](https://en.wikipedia.org/wiki/Disk_partitioning "wikipedia:Disk partitioning")