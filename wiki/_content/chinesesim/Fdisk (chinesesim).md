Related articles

*   [parted](/index.php/Parted "Parted")
*   [GParted](/index.php/GParted "GParted")
*   [Partitioning (简体中文)](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Partitioning (简体中文)")

**翻译状态：** 本文是英文页面 [Fdisk](/index.php/Fdisk "Fdisk") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-08-18，点击[这里](https://wiki.archlinux.org/index.php?title=Fdisk&diff=0&oldid=391664)可以查看翻译后英文页面的改动。

来自 util-linux 的 fdisk (用于 MBR 硬盘)等价。。

来自 util-linux (基于 util-linux 内建的 libfdisk) 的 fdisk 工具部分支持 GPT, 但仍在测试阶段 (自从2013年10月7日). 相关的 cfdisk 和 sfdisk 仍不支持 GPT, 并在 GPT 硬盘上使用的话有可能损坏 GPT 头和分区表。

## Contents

*   [1 使用 MBR - 传统方式](#.E4.BD.BF.E7.94.A8_MBR_-_.E4.BC.A0.E7.BB.9F.E6.96.B9.E5.BC.8F)
    *   [1.1 Fdisk 用法](#Fdisk_.E7.94.A8.E6.B3.95)
        *   [1.1.1 用 fdisk 建立 MBR 分区](#.E7.94.A8_fdisk_.E5.BB.BA.E7.AB.8B_MBR_.E5.88.86.E5.8C.BA)
*   [2 See also](#See_also)

## 使用 MBR - 传统方式

**警告:** 如果打算以 BIOS 模式双启动 Windows （这是32位版 Windows 和64位版 Windows XP 的唯一选择），**不要** 使用 GPT，因为 Windows **不支持**在使用 BIOS 的机器上从 GPT 分区的磁盘上启动。你需要像下面所说的那样，使用 MBR 分区，并且从 BIOS 模式启动。对于现代在 UEFI 模式下的64位 Windows 版本不存在这个限制。

使用 MBR 的话，可以使用*fdisk* 工具编辑分区表。新版本的 *fdisk* 已经废弃使用柱面作为默认显示单位的方式，同时默认也放弃了对MS-DOS的兼容性。最新版本的 *fdisk* 会自动将所有分区对齐到2048扇区，或1024 KiB，以兼容所有已知的 SSD 制造商的 EBS 大小。即使用默认设置即可获得合适的分区对齐。

注意，在以前 *fdisk* 使用柱面作为默认显示单位，并且保留了 MS-DOS 兼容性，这使其默认无法进行 SSD 对齐。因此人们需要从网上查找各种资料以保证分区对齐。使用最新版本的 *fdisk* 简单得多，正如本文档所述那样。

### Fdisk 用法

*   以 root 身份启动 *fdisk* （*disk-device* 形如 `/dev/sda`）:

```
# fdisk *disk-device*

```

*   如果是全新的磁盘或你想重新分区，使用 `o` 命令建立一个新的空 DOS 分区表。
*   使用`n` 命令创建一个新的分区（主分区/第一分区）。
*   使用 `+*x*G` 的格式指定分区大小为 *x* GB。例如，如果你需要创建一个 15 GiB 的分区，你需要输入 `+15G`。
*   使用`t` 命令将分区的 ID 从默认值修改为 Linux（`type 83`）。这是一个可选步骤。如果用户想创建其他类型的分区，如swap，NTFS，LVM 等也可以。注意，完整的可用分区类型列表可以通过 `l` 命令获取。
*   其他分区的处理方式类似。
*   使用 `w` 命令将分区表写入磁盘并退出。
*   将新分区格式化为[文件系统](/index.php/File_systems_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "File systems (简体中文)")。

##### 用 fdisk 建立 MBR 分区

**注意:** 安装媒介中亦有一个叫 `cfdisk` 的工具，它的 UI 与 `cgdisk` 相似；但目前仍不能正确地自动对齐好第一个分区。所以我们在这里改用经典的 fdisk 工具。

启动 *fdisk* :

```
# fdisk /dev/sda

```

创建分区表：

*   `Command (m for help):` 输入 `o` 并按下 `Enter`

然后建立第一个分区：

1.  `Command (m for help):` 输入 `n` 并按下 `Enter`
2.  Partition type: `Select (default p):` 按下 `Enter`
3.  `Partition number (1-4, default 1):` 按下 `Enter`
4.  `First sector (2048-209715199, default 2048):` 按下 `Enter`
5.  `Last sector, +sectors or +size{K,M,G} (2048-209715199....., default 209715199):` 输入 `+15G` 并按下 `Enter`

然后建立第二个分区：

1.  `Command (m for help):` 输入 `n` 并按下 `Enter`
2.  Partition type: `Select (default p):` 按下 `Enter`
3.  `Partition number (1-4, default 2):` 按下 `Enter`
4.  `First sector (31459328-209715199, default 31459328):` 按下 `Enter`
5.  `Last sector, +sectors or +size{K,M,G} (31459328-209715199....., default 209715199):` 按下 `Enter`

现在预览下新的分区表:

*   `Command (m for help):` 输入 `p` 并按下 `Enter`

```
Disk /dev/sda: 107.4 GB, 107374182400 bytes, 209715200 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x5698d902

   Device Boot     Start         End     Blocks   Id  System
/dev/sda1           2048    31459327   15728640   83   Linux
/dev/sda2       31459328   209715199   89127936   83   Linux

```

然后向磁盘写入这些改动：

*   `Command (m for help):` 输入 `w` 并按下 `Enter`

如果一切顺利无错误的话，fdisk 程序将显示如下信息：

```
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks. 

```

若因 *fdisk* 遇到错误导致以上操作无法完成，可以用 `q` 命令来退出。

## See also

*   [Manually Partitioning Your Hard Drive with fdisk](http://www.novell.com/coolsolutions/feature/19350.html)