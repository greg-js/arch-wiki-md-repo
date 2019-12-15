相关文章

*   [File systems (简体中文)](/index.php/File_systems_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "File systems (简体中文)")

**翻译状态：** 本文是英文页面 [XFS](/index.php/XFS "XFS") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-09-01，点击[这里](https://wiki.archlinux.org/index.php?title=XFS&diff=0&oldid=523873)可以查看翻译后英文页面的改动。

XFS 是由硅谷图形公司 (Silicon Graphics, Inc.) 开发的高性能日志式文件系统。XFS 因其基于分配组 (allocation group) 的设计而特别擅长并行 IO。当该文件系统跨越多个存储设备时，这种设计使得 IO 线程数、文件系统带宽、文件和文件系统大小都具有极大的可伸缩性。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 数据损坏](#数据损坏)
    *   [2.1 修复 XFS 文件系统](#修复_XFS_文件系统)
    *   [2.2 在线元数据检查 (scrub)](#在线元数据检查_(scrub))
*   [3 数据完整性](#数据完整性)
*   [4 性能](#性能)
    *   [4.1 带区大小和宽度](#带区大小和宽度)
    *   [4.2 关闭写入屏障 (Barrier)](#关闭写入屏障_(Barrier))
    *   [4.3 访问时间记录](#访问时间记录)
    *   [4.4 磁盘碎片整理](#磁盘碎片整理)
        *   [4.4.1 检查碎片程度](#检查碎片程度)
        *   [4.4.2 进行碎片整理](#进行碎片整理)
    *   [4.5 B+树（用于索引未用 inode）](#B+树（用于索引未用_inode）)
*   [5 故障排除](#故障排除)
    *   [5.1 根文件系统配额](#根文件系统配额)
*   [6 参考资料](#参考资料)

## 安装

用于管理 XFS 分区的工具位于 [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs) 软件包中，该包默认已经安装在基本系统中。

## 数据损坏

如果遇到了任何原因的引起的数据损坏，就需要手动修复文件系统。

### 修复 XFS 文件系统

先卸载 XFS 文件系统：

```
# umount /dev/sda3

```

卸载后，运行 [xfs_repair(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xfs_repair.8) 工具来修复：

```
# xfs_repair -v /dev/sda3

```

### 在线元数据检查 (scrub)

**警告:** 该程序目前是**实验性**的，这意味着它的行为和接口可能随时发生变化。参见 [xfs_scrub(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xfs_scrub.8)。

`xfs_scrub` 请求内核检查 [文件系统](/index.php/File_systems_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "File systems (简体中文)") 中的所有元数据对象。内核会扫描元数据记录以查找明显错误的值，然后与其他元数据进行交叉引用。其目的是通过检查单个元数据记录与文件系统中其他元数据的一致性，建立对整个文件系统一致性的合理置信度。如果存在完整的冗余数据结构，则可以根据其他元数据重建损坏的元数据。

[Enable](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#使用单元 "Systemd (简体中文)") `xfs_scrub_all.timer` 以定期在线检查所有文件系统元数据。有时可能需要[编辑](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#修改现存单元文件 "Systemd (简体中文)") `xfs_scrub_all.timer`，因为它仅在每周日上午 3:10 运行。

## 数据完整性

xfsprogs 3.2.0 引入了一种新型磁盘格式 (v5)，其包含了称为 [自描述元数据 (Self-Describing Metadata)](https://www.kernel.org/doc/Documentation/filesystems/xfs-self-describing-metadata.txt) 的元数据校验方案。 基于 CRC32，它提供的额外保护措施可以在意外断电时防止元数据损坏。当使用 xfsprogs 3.2.3 或更高版本时，这种校验默认是打开的。如果需要在旧版内核中挂载 XFS 为可读写，可以在调用 [mkfs.xfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.xfs.8) 时加上 `-m crc=0` 来关闭校验特性。

```
# mkfs.xfs -m crc=0 /dev/*target_partition*

```

自 Linux Kernel 3.15 起，XFS v5 磁盘格式被视作稳定特性，可用于生产环境。

**注意:** 与 [Btrfs](/index.php/Btrfs_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Btrfs (简体中文)") 和 [ZFS](/index.php/ZFS_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ZFS (简体中文)") 不同，XFS 中的 CRC32 校验仅用于元数据而非实际数据。

## 性能

要获得最佳速度，只要这样创建 XFS 文件系统：

```
# mkfs.xfs /dev/*target_partition*

```

对，就是这么简单 - 因为所有 [新特性默认都是开启的](http://xfs.org/index.php/XFS_FAQ#Q:_I_want_to_tune_my_XFS_filesystems_for_.3Csomething.3E)。

**警告:** 关闭写入屏障 (barrier)、关闭访问时间记录 (atime) 以及其他性能增强功能会导致数据损坏和丢失的可能性更大。

根据 [XFS wiki](http://xfs.org/index.php/XFS_FAQ#Q:_I_want_to_tune_my_XFS_filesystems_for_.3Csomething.3E)，可以考虑更改默认的 CFQ [I/O 调度器](/index.php/Improving_performance#Input/output_schedulers "Improving performance")（比如改成 [Deadline](https://en.wikipedia.org/wiki/Deadline_scheduler 上。

### 带区大小和宽度

如果这个文件系统位于条带化的 RAID 上，可以在 [mkfs.xfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.xfs.8) 命令中指定带区大小来获得显著的性能提升。

参考 [How to calculate the correct sunit,swidth values for optimal performance](http://xfs.org/index.php/XFS_FAQ#Q:_How_to_calculate_the_correct_sunit.2Cswidth_values_for_optimal_performance)

### 关闭写入屏障 (Barrier)

可以通过关闭文件系统的写入屏障来提高性能，方法是向 [fstab](/index.php/Fstab_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fstab (简体中文)") 中添加 `nobarrier` 挂载选项。

### 访问时间记录

某些文件系统可以通过在 `/etc/fstab` 文件中添加 `noatime` 挂载选项来增强性能。对于 XFS 文件系统来说，默认的访问时间记录行为是 `relatime`，与 noatime 相比这几乎没有额外开销，且仍然可以记录正确的访问时间。所有 Linux 文件系统现在都以这个选项为默认值（从大约 2.6.30 版本开始），但是 XFS 从 2006 年开始就采用了类似 relatime 的特性，因此不需要出于性能考虑而在 XFS 上使用 noatime。

另外，`noatime` 包含了 `nodiratime`，所以指定了 **noatime** 时就不需要指定 **nodiratime**。

### 磁盘碎片整理

尽管 XFS 本质上基于区段 (Extent) 并且延迟分配策略很大程度上增强了它对磁盘碎片的抗性，XFS 仍然提供了磁盘碎片整理程序（*xfs_fsr*，XFS filesystem reorganizer 的缩写），它可以在已挂载且活动的 XFS 文件系统上整理碎片。定期查看 XFS 碎片也很有用。

[xfs_fsr(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xfs_fsr.8) 改进了已挂载文件系统的文件组织。该重组织算法一次操作一份文件，对文件进行压缩或改进文件区段布局（改成连续数据块）。

#### 检查碎片程度

查看当前文件系统中有多少磁盘碎片：

```
# xfs_db -c frag -r /dev/sda3

```

#### 进行碎片整理

要启动碎片整理，使用 [xfs_fsr(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xfs_fsr.8) 命令：

```
# xfs_fsr /dev/sda3

```

### B+树（用于索引未用 inode）

自 Linux 3.16 起，XFS 增加了 B+树用于索引未被使用的 inode。它等同于索引已使用 inode 的 B+树，不同之处在于索引未用 inode 的 B+树至少包含一个未用 inode。这一设计的目的是改进分配 inode 时寻找未用 inode 簇的性能。它可以提高长期使用后的文件系统性能，比如你在数月或数年之间已经向文件系统写入或删除了数百万的文件。使用这个功能不会影响整个文件系统的可靠性程度或恢复能力。

这个功能依赖于新的 v5 磁盘格式，自 Linux Kernel 3.15 起它被视作可用于生产环境的稳定特性。它没有改变磁盘上原本的数据结构，但会添加一个新的结构来使它与 B+树（用于分配 inode）保持兼容；因此，旧版本的内核只能将带有 B+树功能的文件系统挂载为只读模式。

当使用 xfsprogs 3.2.3 或更高版本时这个功能默认是开启的。如果你需要一个旧版本内核可写入的文件系统，这个功能可以在格式化 XFS 分区时用 `finobt=0` 开关来关闭。你还需要把它和 `crc=0` 一起用。

```
# mkfs.xfs -m crc=0,finobt=0 /dev/*target_partition*

```

也可以简写（`crc` 包含了 `finobt`）

```
# mkfs.xfs -m crc=0 /dev/*target_partition*

```

## 故障排除

### 根文件系统配额

XFS 配额挂载选项（`uquota`、`gquota`、`prjquota` 等）会在重新挂载文件系统时失效。要对根文件系统启用配额功能，这个挂载选项需要作为 [内核参数](/index.php/Kernel_parameters_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel parameters (简体中文)") `rootflags=` 传递给初始化内存盘 (initramfs)。在随后的启动过程中，这个选项不需要在 `/etc/fstab` 中挂载根 (`/`) 文件系统的选项里再次列出。

**注意:** XFS 配额相较于标准 Linux [磁盘配额](/index.php/Disk_quota "Disk quota") 有一些区别，这篇文章 [http://inai.de/linux/adm_quota](http://inai.de/linux/adm_quota) 或许值得一读。

## 参考资料

*   [XFS FAQ](http://xfs.org/index.php/XFS_FAQ)
*   [Improving Metadata Performance By Reducing Journal Overhead](http://xfs.org/index.php/Improving_Metadata_Performance_By_Reducing_Journal_Overhead)
*   [XFS Wikipedia Entry](https://en.wikipedia.org/wiki/XFS "wikipedia:XFS")