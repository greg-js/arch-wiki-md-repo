**翻译状态：** 本文是英文页面 [Btrfs](/index.php/Btrfs "Btrfs") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-05-13，点击[这里](https://wiki.archlinux.org/index.php?title=Btrfs&diff=0&oldid=432990)可以查看翻译后英文页面的改动。

来自 [Wikipedia:Btrfs](https://en.wikipedia.org/wiki/Btrfs "wikipedia:Btrfs")

**Btrfs**（B-tree 文件系统，通常念成 **Butter FS**，**Better FS**或**B-tree FS**），一种支持写入时复制（COW）的文件系统，运行在 Linux 操作系统上，采用 [GPL](https://en.wikipedia.org/wiki/GPL "wikipedia:GPL") 授权。[Oracle](/index.php/Oracle "Oracle") 于 2007 年对外宣布这项计划，并发布源代码，2014 年 8 月发布稳定版。目标是取代 [Linux](/index.php/Linux "Linux") 当时主流的 [ext3](/index.php/Ext3 "Ext3") 文件系统，摆脱 ext3 的一些限制，特別是单文件大小，文件系统总大小和文件校验，并加入 ext3 不支持的一些功能，比如可写快照（writable snapshots）、快照的快照（snapshots of snapshots）、内建磁盘阵列（RAID），以及子卷（subvolumes）。Btrfs 也宣称专注于「容错、修复及易于管理」。

来自 [Btrfs Wiki](https://btrfs.wiki.kernel.org/index.php/Main_Page):

	Btrfs 是一种新型的写时复制 (COW) Linux 文件系统已经并入内核主线。Btrfs 设计实现高级功能的同时，着重于容错、修复以及易于管理。它由 Oracle, Red Hat, Fujitsu, Intel, SUSE, STRATO 等企业和开发者共同开发, Btrfs 以 GNU GPL 协议授权,同时欢迎任何人的贡献.

**Warning:**

*   Btrfs 有一些功能被认为是实验性的特性，可参见内核百科的 [Btrfs 稳定性状态报告](https://btrfs.wiki.kernel.org/index.php/Main_Page#Stability_status)，[Btrfs 足够稳定了吗？](https://btrfs.wiki.kernel.org/index.php/FAQ#Is_btrfs_stable.3F)和[开始使用 Btrfs](https://btrfs.wiki.kernel.org/index.php/Getting_started)。
*   了解当前的[局限性](#.E5.B1.80.E9.99.90.E6.80.A7).

## Contents

*   [1 准备工作](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C)
*   [2 分区](#.E5.88.86.E5.8C.BA)
*   [3 创建文件系统](#.E5.88.9B.E5.BB.BA.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
    *   [3.1 新建文件系统](#.E6.96.B0.E5.BB.BA.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
        *   [3.1.1 单一设备上的文件系统](#.E5.8D.95.E4.B8.80.E8.AE.BE.E5.A4.87.E4.B8.8A.E7.9A.84.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
        *   [3.1.2 多设备文件系统](#.E5.A4.9A.E8.AE.BE.E5.A4.87.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
    *   [3.2 从 Ext3/4 转换](#.E4.BB.8E_Ext3.2F4_.E8.BD.AC.E6.8D.A2)
*   [4 设置文件系统](#.E8.AE.BE.E7.BD.AE.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
    *   [4.1 写时复制 (CoW)](#.E5.86.99.E6.97.B6.E5.A4.8D.E5.88.B6_.28CoW.29)
        *   [4.1.1 停用 CoW](#.E5.81.9C.E7.94.A8_CoW)
        *   [4.1.2 强制启用写时复制](#.E5.BC.BA.E5.88.B6.E5.90.AF.E7.94.A8.E5.86.99.E6.97.B6.E5.A4.8D.E5.88.B6)
    *   [4.2 压缩](#.E5.8E.8B.E7.BC.A9)
    *   [4.3 子卷](#.E5.AD.90.E5.8D.B7)
        *   [4.3.1 创建子卷](#.E5.88.9B.E5.BB.BA.E5.AD.90.E5.8D.B7)
        *   [4.3.2 列出子卷列表](#.E5.88.97.E5.87.BA.E5.AD.90.E5.8D.B7.E5.88.97.E8.A1.A8)
        *   [4.3.3 删除子卷](#.E5.88.A0.E9.99.A4.E5.AD.90.E5.8D.B7)
        *   [4.3.4 挂载子卷](#.E6.8C.82.E8.BD.BD.E5.AD.90.E5.8D.B7)
            *   [4.3.4.1 更改子卷的挂载选项](#.E6.9B.B4.E6.94.B9.E5.AD.90.E5.8D.B7.E7.9A.84.E6.8C.82.E8.BD.BD.E9.80.89.E9.A1.B9)
        *   [4.3.5 改变默认子卷](#.E6.94.B9.E5.8F.98.E9.BB.98.E8.AE.A4.E5.AD.90.E5.8D.B7)
    *   [4.4 Commit intervals setting](#Commit_intervals_setting)
    *   [4.5 Checkpoint 间隔](#Checkpoint_.E9.97.B4.E9.9A.94)
    *   [4.6 SSD TRIM](#SSD_TRIM)
*   [5 使用](#.E4.BD.BF.E7.94.A8)
    *   [5.1 显示已使用的/空闲空间](#.E6.98.BE.E7.A4.BA.E5.B7.B2.E4.BD.BF.E7.94.A8.E7.9A.84.2F.E7.A9.BA.E9.97.B2.E7.A9.BA.E9.97.B4)
    *   [5.2 碎片整理](#.E7.A2.8E.E7.89.87.E6.95.B4.E7.90.86)
    *   [5.3 Scrub](#Scrub)
    *   [5.4 Balance](#Balance)
    *   [5.5 RAID](#RAID)
    *   [5.6 快照](#.E5.BF.AB.E7.85.A7)
    *   [5.7 发送和接收](#.E5.8F.91.E9.80.81.E5.92.8C.E6.8E.A5.E6.94.B6)
*   [6 局限性](#.E5.B1.80.E9.99.90.E6.80.A7)
    *   [6.1 加密](#.E5.8A.A0.E5.AF.86)
    *   [6.2 交换文件](#.E4.BA.A4.E6.8D.A2.E6.96.87.E4.BB.B6)
    *   [6.3 Linux-rt 内核](#Linux-rt_.E5.86.85.E6.A0.B8)
*   [7 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
*   [8 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [8.1 GRUB](#GRUB)
        *   [8.1.1 分区偏移](#.E5.88.86.E5.8C.BA.E5.81.8F.E7.A7.BB)
        *   [8.1.2 Missing root](#Missing_root)
    *   [8.2 BTRFS: open_ctree failed](#BTRFS:_open_ctree_failed)
    *   [8.3 检查 btrfs 文件系统](#.E6.A3.80.E6.9F.A5_btrfs_.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
*   [9 另见](#.E5.8F.A6.E8.A7.81)

## 准备工作

Btrfs 支持已经包含在[linux](https://www.archlinux.org/packages/?name=linux)和[linux-lts](https://www.archlinux.org/packages/?name=linux-lts)的内核中.[GRUB 2](/index.php/GRUB "GRUB"),[mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")和 [Syslinux](/index.php/Syslinux "Syslinux") 也已经支持 Btrfs，不需要额外配置。

要使用一些用户空间工具,[安装](/index.php/Installing "Installing") [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) 软件包.

## 分区

Btrfs 能在整个设备上使用,替代 [MBR](/index.php/MBR "MBR") 或 [GPT](/index.php/GPT "GPT") 分区表,但是并不要求一定这么做,最简单的方法是 [在一个已存在的分区上创建 btrfs 文件系统](#Creating_a_new_file_system). 如果你选择用 btrfs 替代分区表, 可以用 [子卷](#Subvolumes)模拟不同的分区.

这是在单个设备上使用 btrfs 文件系统的限制:

*   不能在不同的 [挂载点](/index.php/Fstab "Fstab") 上使用不同的[文件系统](/index.php/File_systems "File systems").
*   不能使用 [交换空间](/index.php/Swap "Swap") (因为 btrfs 不支持 [交换文件](/index.php/Swap#Swap_file "Swap") 而且硬盘上没有空间用来创建 [交换分区](/index.php/Swap#Swap_partition "Swap").) 这同时也限制了睡眠和休眠 (因为需要交换空间) .
*   不能使用 [UEFI](/index.php/UEFI "UEFI") 启动.

运行下面的命令把整个设备的分区表替换成 btrfs:

```
# mkfs.btrfs /dev/sd*X*

```

例如 `/dev/sda` 而不是 `/dev/sda1`. 后一种形式会格式化现有的分区而不是替换掉原有的分区表.

像使用普通的 MBR 分区表存储设备一样安装 [启动管理器](/index.php/Boot_loader "Boot loader"), 例如[GRUB](/index.php/GRUB#Install_to_440-byte_MBR_boot_code_region "GRUB"):

```
# grub-install --recheck /dev/sd*X*

```

## 创建文件系统

可以新建或者从已有文件系统转化为 Btrfs.

### 新建文件系统

#### 单一设备上的文件系统

要格式化一个分区:

```
# mkfs.btrfs -L *mylabel* /dev/*partition*

```

Btrfs 的默认块大小为 16KB. 使用更大的blocksize数据/元数据,为`nodesize`通过指定一个值`-n`开关使用,如本例所示16kb块:

```
# mkfs.btrfs -L *mylabel* -n 16k /dev/*partition*

```

#### 多设备文件系统

用户可选择多个设备来创建RAID。支持的RAID级别有 RAID 0,RAID 1,RAID 10,RAID 5 和 RAID 6.数据和元数据的 RAID 等级可以用 `-d` 和 `-m` 参数指定. 默认情况下元数据使用镜像 (RAID1)，而数据被 strip (RAID0). 参阅 [Btrfs Wiki:在多个设备上使用 btrfs](https://btrfs.wiki.kernel.org/index.php/Using_Btrfs_with_Multiple_Devices) 或查阅 `mkfs.btrfs` 的手册页获得更多信息.

```
# mkfs.btrfs -d raid0 -m raid1 /dev/*part1* /dev/*part2* ...

```

**Note:** Systemd 可能无法因为正确处理多设备 btrfs 文件系统上的每一个设备而不能正常启动,详见 [这个bug报告](https://github.com/systemd/systemd/issues/1921) .

[RAID](#RAID) 文章有关于维护多设备上的 btrfs 文件系统的一些建议.

### 从 Ext3/4 转换

**Warning:** 到2015年中后期, btrfs 邮件列表中报告了多起失败的转换.尽管近期的更新有所修复,但还是建议小心使用.在开始之前确定你有*可用的*备份并且愿意承担丢失数据的风险. 详见 [Btrfs Wiki:从 Ext3 文件系统转换](https://btrfs.wiki.kernel.org/index.php/Conversion_from_Ext3) .

从安装 CD 启动，然后转化分区:

```
# btrfs-convert /dev/*partition*

```

挂载转换后的分区并修改`/etc/fstab`文件，指定分区类型(**type** 为 btrfs，**fs_passno** [最后一列] 修改为0，Btrfs在启动时并不进行磁盘检查). 还要注意的是分区的UUID将有改变，所以使用UUID时，更新fstab中相应的条目。 `chroot` 到系统并重建 GRUB 条目（如果对此过程不熟悉，参考[Install from existing Linux](/index.php/Install_from_existing_Linux "Install from existing Linux")和[GRUB](/index.php/GRUB "GRUB")). 如果正在转换根目录,还需要在 chroot 环境中重建初始化内存盘 (`mkinitcpio -p linux`). 如果 GRUB 不能启动 (例如 'unknown filesystem' 错误),则需要重新安装 (`grub-install /dev/*partition*`) 并生成配置文件 (`grub-mkconfig -o /boot/grub/grub.cfg`).

确认没有问题后,完成转换通过删除备份`ext2_saved`子卷，请注意，如果没了它(备份子卷)，你将没办法还原回 ext3/4 文件系统。

```
# btrfs subvolume delete /ext2_saved

```

最后通过 [balance](#Balance) 回收空间.

## 设置文件系统

### 写时复制 (CoW)

默认情况下 btrfs 对所有文件使用 [写时复制 (CoW)](https://en.wikipedia.org/wiki/copy-on-write "wikipedia:copy-on-write").参阅[the Btrfs Sysadmin Guide section](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Copy_on_Write_.28CoW.29) 获得技术细节.写时复制具有许多优点和缺点.

#### 停用 CoW

要对某个子卷上的新文件停用写时复制,使用 `nodatacow`选项,注意这只会影响新文件,并不改变已有文件的写时复制属性.

为单文件或目录禁用CoW特性，请使用下面的命令：

```
# chattr +C [文件/目录的地址(path)]

```

这会为这个文件的单个引用停用写时复制,如果这个文件不只有一个引用(例如通过 `cp --reflink=always` 生成或者在文件系统快照中),写时复制依然生效.

This will disable copy-on-write for those operation in which there is only one reference to the file. If there is more than one reference (e.g. through `cp --reflink=always` or because of a filesystem snapshot), copy-on-write still occurs.

**Note:** 来自 chattr 的手册页:在btrfs上，'C' 标志应该被设置在新建的或者是空白的文件/目录，如果被设置在已有数据的文件,当块分配给该文件时，文件将不确定是否完全稳定。如果'C' 标志被设置给一个目录，将不会影响目前的目录，但在该目录创建的新文件将具有No_COW属性。

**Tip:** 可以用下面的方法为已存在的文件或目录停用写时复制:
```
$ mv */path/to/dir* */path/to/dir*_old
$ mkdir */path/to/dir*
$ chattr +C */path/to/dir*
$ cp -a */path/to/dir*_old/* */path/to/dir*
$ rm -rf */path/to/dir*_old

```

需要保证这个过程中目标文件不会被使用,同时注意下面描述的 `mv` 或 `cp --reflink` 并不起作用.

#### 强制启用写时复制

如果复制的文件停用了写时复制,可以这样强制开启:

```
$ cp --reflink *source* *dest* 

```

参阅 `cp` 的手册页获得关于 `--reflink` 标志的更多信息.

### 压缩

Btrfs支持透明压缩，这意味着分区里的每个文件都被自动压缩。这不单减小了文件的大小，还[提高了性能](http://www.phoronix.com/scan.php?page=article&item=btrfs_compress_2635&num=1)，特别是在使用[lzo算法](http://www.phoronix.com/scan.php?page=article&item=btrfs_lzo_2638&num=1)时。用`compress=gzip`或`compress=lzo`挂载选项打开压缩功能。只有在加入挂载选项后创建或修改的文件会被压缩，所以要充分利用压缩特性，最好安装时就启用压缩功能。

不过也可以在安装以后通过 `btrfs filesystem defragment -c*alg*` (也可以使用其它压缩算法,例如 `zlib` / `lzo`) 压缩一个分区 (例如从 ext3/4 转换以后的文件系统).

要将整个文件系统通过 lzo 重新压缩,运行下面的命令:

```
# btrfs filesystem defragment -r -v -clzo /

```

**Tip:** 通过 `chattr +c` ,也可以在不使用 `compress` 选项的情况下为单个文件启用压缩属性.对目录启用会使这个目录下新文件自动压缩.

在一个新的 btrfs 分区上安装 Arch Linux 时,要充分利用压缩特性，最好安装时就启用压缩功能。在[File systems](/index.php/File_systems "File systems") 时使用 `compress` 参数: `mount -o compress=lzo /dev/sd*xY* /mnt/`.在 时把 `compress=lzo` 添加到 [fstab](/index.php/Fstab "Fstab") 中的根目录中的选项上.

### 子卷

"btrfs 子卷不是 (也不能看作) 块设备,一个子卷可以看作 POSIX 文件名字空间.这个名字空间可以通过子卷上层访问,也可以独立挂载."[[1]](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Subvolumes)

每个 btrfs 文件系统都有一个 ID 为5的子卷.默认情况下它可以作为 `/` 挂载.

参阅下面的链接获得更多信息:

*   [Btrfs Wiki SysadminGuide#Subvolumes](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Subvolumes)
*   [Btrfs Wiki Getting started#Basic Filesystem Commands](https://btrfs.wiki.kernel.org/index.php/Getting_started#Basic_Filesystem_Commands)
*   [Btrfs Wiki Trees](https://btrfs.wiki.kernel.org/index.php/Trees)

#### 创建子卷

要创建一个子卷:

```
# btrfs subvolume create */path/to/subvolume*

```

#### 列出子卷列表

要列出当前路径 (`*path*`) 下的子卷:

```
# btrfs subvolume list -p *path*

```

#### 删除子卷

要删除一个子卷:

```
# btrfs subvolume delete */path/to/subvolume*

```

只是移除子卷的目录 `*/path/to/subvolume*` 而不使用这个命令并不会删除一个子卷.

#### 挂载子卷

通过 `subvol=*/path/to/subvolume*` 或者 `subvolid=*objectid*` 挂载选项,子卷可以像文件系统一样挂载.例如创建一个名为 `subvol_root` 的子卷并挂载到 `/` 上.通过创建不同的子卷也可以用来模拟传统的文件系统,然后挂载到合适的位置.

**Tip:** 为了方便修改子卷，请考虑创建新的子卷,然后挂载它 (例如`/`) 而不是使用顶层子卷 (ID=5) 挂载为根目录.

参阅 [Snapper#Suggested filesystem layout](/index.php/Snapper#Suggested_filesystem_layout "Snapper"), [Btrfs SysadminGuide#Managing Snapshots](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Managing_Snapshots) 和 [Btrfs SysadminGuide#Layout](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Layout) 获得子卷应用的示例.

##### 更改子卷的挂载选项

当以 `subvol=` 参数挂载子卷时,可以使用某些参数 (例如影响压缩和写时复制的参数).

参阅 [Btrfs Wiki Mount options](https://btrfs.wiki.kernel.org/index.php/Mount_options) 和 [Btrfs Wiki Gotchas](https://btrfs.wiki.kernel.org/index.php/Gotchas) 获得更多信息. 作为正开发中的文件系统,不同的挂载选项可能会影响文件系统的性能.[[#另见|]] 一节中有一些评测文章可供参考.

**Warning:** 某些挂载选项可能会停用安全功能并增加损坏文件系统的风险.

#### 改变默认子卷

如果挂载时不指定 `subvol=` 选项便会挂载默认子卷.要改变默认子卷:

```
# btrfs subvolume set-default *subvolume-id* /

```

*subvolume-id* 可以通过[列出子卷列表](#Listing_subvolumes)获得.

**Note:** 在安装了 [GRUB](/index.php/GRUB "GRUB") 的系统上,在改变默认子卷以后不要忘记运行 `grub-install` . 参见 [this forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1615373).

**Warning:** 如果对正挂载默认子卷的文件系统上使用 `btrfs subvolume set-default` 可能会导致其无法访问,参阅 [Btrfs Wiki Sysadmin Guide](https://btrfs.wiki.kernel.org/index.php/SysadminGuide).

### Commit intervals setting

The resolution at which data are written to the filesystem is dictated by Btrfs itself and by system-wide settings. Btrfs defaults to a 30 seconds checkpoint interval in which new data are committed to the filesystem. This is tuneable using mount options (see below)

System-wide settings also affect commit intervals. They include the files under `/proc/sys/vm/*` and are out-of-scope of this wiki article. The kernel documentation for them resides in `Documentation/sysctl/vm.txt`.

### Checkpoint 间隔

从 Linux 内核 3.12 开始,用户可以通过在 `/etc/fstab` 改变 `commit` 的值来改变 Checkpoint 周期 (默认是30秒).

```
LABEL=arch64 / btrfs defaults,noatime,ssd,compress=lzo,commit=120 0 0

```

### SSD TRIM

在支持 TRIM 的固态硬盘上 btrfs 文件系统可以自动释放不使用的块.

[Solid State Drives#TRIM](/index.php/Solid_State_Drives#TRIM "Solid State Drives") 有关于使用 TRIM 的更多信息.

## 使用

### 显示已使用的/空闲空间

像 `/usr/bin/df` 这样的用户空间工具可能不会准确的计算剩余空间 (因为并没有分别计算文件和元数据的使用情况) .推荐使用 `/usr/bin/btrfs` 来查看使用情况. 下面的例子会同时使用 `df -h` 和 `btrfs filesystem df`.

 `$ df -h /` 
```
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda3       119G  3.0G  116G   3% /

```
 `$ btrfs filesystem df /` 
```
Data: total=3.01GB, used=2.73GB
System: total=4.00MB, used=16.00KB
Metadata: total=1.01GB, used=181.83MB
```

注意到 `df -h` 报告使用了 3.0GB 但 `btrfs filesystem df` 报告数据使使用了 2.73GB . 这是因为 btrfs 将文件分配到池中,真正的已使用空间是三个 "Used" 的总和. (约等于 `df -h` 的结果) .

**Note:** 如果在 Linux 内核 版本3.15 以后的输出中看到了 `unknown` at kernel >= 3.15,这是个显示问题. (参阅 [这个 patch](http://thread.gmane.org/gmane.comp.file-systems.btrfs/34419),这是 GlobalReserve, 表示没有刷新的缓冲区 (在 RAID 分区上可能会看到 `unknown, single`) 而且无法重新 balance .

`btrfs filesystem show` 命令也可以使用,输出的信息更少:

```
# btrfs filesystem show /dev/sda3

```

`btrfs filesystem usage` 是新增加的命令:

```
# btrfs filesystem usage

```

**Note:** The `btrfs filesystem usage` 在 `RAID5/RAID6` 设备上可能无法正常工作.

### 碎片整理

btrfs 支持在线碎片整理,要整理根文件夹:

```
# btrfs filesystem defragment /

```

这*并不会'整理整个文件系统参阅 [Btrfs Wiki上的这个页面](https://btrfs.wiki.kernel.org/index.php/Problem_FAQ#Defragmenting_a_directory_doesn.27t_work) 获得更多信息.*

要整理整个文件系统并观看冗长的输出:

```
# btrfs filesystem defragment -r -v /

```

### Scrub

[Btrfs Wiki 术语表](https://btrfs.wiki.kernel.org/index.php/Glossary)中写到 scrub 是一种 "在线文件系统检查工具".它读取文件系统中的文件和元数据,并使用效验值和 RAID 存储上的镜像区分并修复损坏的数据.

```
# btrfs scrub start /
# btrfs scrub status /

```

**Warning:** 运行 scrub 会阻止系统待机, 详见 [这个讨论](http://comments.gmane.org/gmane.comp.file-systems.btrfs/33106).

[btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) 软件包带有 `btrfs-scrub@.timer` 系统单元,用来每月运行 scrub 命令.通过添加挂载点的参数来[启用](/index.php/Enable "Enable")它,例如`btrfs-scrub@-.timer` (`/`) 或者 `btrfs-scrub@home.timer` (`/home`).

也可以通过[启动](/index.php/Starting "Starting") `btrfs-scrub@.service` 来手动运行 scrub (使用同样的挂载点参数) ,相对于 `# btrfs scrub` 这么做的优点是会记录在 [Systemd 日志](/index.php/Systemd_journal "Systemd journal")中.

### Balance

"balance passes all data in the filesystem through the allocator again. It is primarily intended to rebalance the data in the filesystem across the devices when a device is added or removed. A balance will regenerate missing copies for the redundant RAID levels, if a device has failed." [[2]](https://btrfs.wiki.kernel.org/index.php/Glossary) .

参阅 [上游的 FAQ](https://btrfs.wiki.kernel.org/index.php/FAQ#What_does_.22balance.22_do.3F).

```
# btrfs balance start /
# btrfs balance status /

```

### RAID

Btrfs 提供对 RAID 一类的 [多设备文件系统](#Multi-device_file_system)的原生支持.参阅 [the Btrfs wiki page](https://btrfs.wiki.kernel.org/index.php/Using_Btrfs_with_Multiple_Devices) 获得更多信息. [Btrfs 管理员手册](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#RAID_and_data_replication) 提供了技术背景信息.

### 快照

"快照是和特定子卷共享文件和元数据的特殊子卷, 利用了 btrfs 的写时复制特性." 详见 [Btrfs Wiki SysadminGuide#Snapshots](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Snapshots).

要创建一个快照:

```
# btrfs subvolume snapshot *source* [*dest*/]*name*

```

加入 `-r` 参数可以创建一个只读快照. 为只读快照创建一个快照可以获得一个只读快照的可写入版本.

**Note:** 快照不是递归包含的，这意味着子卷内的子卷在快照里是空目录。

### 发送和接收

可以通过 `send` 命令发送一个快照,通常会与 btrfs 中的 `receive` 组成管道.例如将快照 `/root_backup` (也许是`/`的备份) 发送到 `/backup`:

```
 # btrfs send /root_backup | btrfs receive /backup

```

*只能*发送只读快照,上面的命令在将子卷复制到外部设备 (例如备份驱动器) 时会很有用.

也可以只发送两个快照间发生变化的部分,例如如果你已经发送了快照 `root_backup` ,然后又建立了一个新的只读快照 `root_backup_new` ,可以这样完成增量发送:

```
 # btrfs send -p /root_backup /root_backup_new | btrfs send /backup

```

现在你 `/backup` 的快照会是 `root_backup_new`.

参阅 [Btrfs Wiki's Incremental Backup page](https://btrfs.wiki.kernel.org/index.php/Incremental_Backup) 获得更多信息 (例如使用工具自动化这一过程)

## 局限性

使用前请了解如下局限。

### 加密

Btrfs 目前还没有内建的加密支持，但可以在运行`mkfs.btrfs`前加密分区，参阅[Dm-crypt with LUKS](/index.php/Dm-crypt_with_LUKS "Dm-crypt with LUKS").

(如果已经创建了文件系统，可以使用[EncFS](/index.php/EncFS "EncFS")或[TrueCrypt](/index.php/TrueCrypt "TrueCrypt"),但是这样会无法使用 btrfs 的一些功能。)

### 交换文件

Btrfs 不支持交换文件，因为 Btrfs 因为潜在的文件系统损坏风险，没有加入交换文件需要的功能，参阅[这里](https://btrfs.wiki.kernel.org/index.php/FAQ#Does_btrfs_support_swap_files.3F). 交换文件可以挂载到 loop 设备中，但是性能比较差。[systemd-loop-swapfile](https://aur.archlinux.org/packages/systemd-loop-swapfile/)提供了需要的服务文件。

### Linux-rt 内核

在版本 3.14.12_rt9中, [linux-rt](/index.php/Kernel#-rt "Kernel") 内核不能引导Btrfs文件系统，这是因为 *rt* 补丁集的开发相对缓慢导致的。

## 提示和技巧

参阅 [Btrfs - Tips and tricks](/index.php/Btrfs_-_Tips_and_tricks "Btrfs - Tips and tricks").

## 故障排除

参阅 [Btrfs Problem FAQ](https://btrfs.wiki.kernel.org/index.php/Problem_FAQ) 获得排除一般问题的信息.

### GRUB

#### 分区偏移

**Note:** 在试图将 `core.img` 嵌入到已经分区的磁盘上时可能会发生偏移问题. [这意味着](https://wiki.archlinux.org/index.php?title=Talk:Btrfs&diff=319474&oldid=292530)可以把 `corg.img` 嵌入到 btrfs 池或是无分区磁盘 (例如`/dev/sd*X*`) 上.

Grub 2可以启动 Btrfs 分区，但是因为模块比较大， grub-install 安装的 core.img 文件超过了 MBR 与第一个分区之间的空间大小 (63 扇区/31.5KiB) .更新后的 `fdisk` 和 `gdisk` 的磁盘工具会通过第一个分区前空出 1-2M 的空间避免此问题.

#### Missing root

如果启动 RAID 卷设备后编辑了 /usr/share/grub/grub-mkconfig_lib 移除了 `echo " search --no-floppy --fs-uuid --set=root ${hints} ${fs_uuid}"` 中的引号,可能会遇到 `error no such device: root` 问题,重新生成 GRUB 设置文件应该能避免这个问题.

### BTRFS: open_ctree failed

2014 年 11 月的 [systemd](/index.php/Systemd "Systemd") 和 [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") 中的 bug 可能导致使用 `mkinitcpio.conf` 中 `btrfs` hook 的用户启动多设备文件系统的 btrfs 卷时出现错误\:

```
BTRFS: open_ctree failed
mount: wrong fs type, bad option, bad superblock on /dev/sdb2, missing codepage or helper program, or other error

In some cases useful info is found in syslog - try dmesg|tail or so.

You are now being dropped into an emergency shell.

```

一个临时解决方案是从 `HOOKS` 中移除 `btrfs` 并把它放入 `MODULES` 中,通过 `mkinitcpio -p linux` 重新生成 initramfs 并重新启动.

参阅 [原来的论坛讨论](https://bbs.archlinux.org/viewtopic.php?id=189845) 和[FS#42884](https://bugs.archlinux.org/task/42884) 获得更多的信息和讨论.

另外如果在挂载 RAID 卷组时缺少某个卷时也有可能会发生这个错误.这种情况下你需要把 `degraded` 加入到 `/etc/fstab` 中,如果根目录在卷组上,同时需要加入 `rootflags=degraded` [内核参数](/index.php/Kernel_parameters "Kernel parameters")

### 检查 btrfs 文件系统

**Warning:** btrfs (特别是`btrfs check` 命令)仍在开发阶段, 强烈建议在加上 `--repair` 参数运行 `btrfs check` 时做一个*备份*.

*[btrfs check](https://btrfs.wiki.kernel.org/index.php/Manpage/btrfs-check)* 可以检查并修复一个未挂载的 btrfs 文件系统.但是由于它并未开发完成,它并不能修复某些错误 (即使这些错误没导致无法挂载).

参阅 [Btrfsck](https://btrfs.wiki.kernel.org/index.php/Btrfsck) 获得更多信息.

## 另见

*   **官方网站**
    *   [Btrfs Wiki](https://btrfs.wiki.kernel.org/)
    *   [Btrfs Wiki Glossary](https://btrfs.wiki.kernel.org/index.php/Glossary)
*   **官方 FAQs**
    *   [Btrfs Wiki FAQ](https://btrfs.wiki.kernel.org/index.php/FAQ)
    *   [Btrfs Wiki Problem FAQ](https://btrfs.wiki.kernel.org/index.php/Problem_FAQ)
*   **Btrfs pull request**
    *   [3.14](http://lkml.indiana.edu/hypermail/linux/kernel/1401.3/03045.html)
    *   [3.13](http://lkml.indiana.edu/hypermail/linux/kernel/1311.1/03526.html)
    *   [3.12](http://lkml.indiana.edu/hypermail/linux/kernel/1309.1/02981.html)
    *   [3.11](http://lkml.indiana.edu/hypermail/linux/kernel/1305.1/01064.html)
*   **性能相关**
    *   [Btrfs on raw disks?](http://superuser.com/questions/432188/should-i-put-my-multi-device-btrfs-filesystem-on-disk-partitions-or-raw-devices)
    *   [Varying leafsize and nodesize in Btrfs](http://comments.gmane.org/gmane.comp.file-systems.btrfs/19440)
    *   [Btrfs support for efficient SSD operation (data blocks alignment)](http://comments.gmane.org/gmane.comp.file-systems.btrfs/15646)
    *   [Is Btrfs optimized for SSDs?](https://btrfs.wiki.kernel.org/index.php/FAQ#Is_Btrfs_optimized_for_SSD.3F)
    *   **Phoronix 的挂载选项测试**
        *   [Linux 3.14](http://www.phoronix.com/scan.php?page=article&item=linux_314_btrfs)
        *   [Linux 3.11](http://www.phoronix.com/scan.php?page=article&item=linux_btrfs_311&num=1)
        *   [Linux 3.9](http://www.phoronix.com/scan.php?page=news_item&px=MTM0OTU)
        *   [Linux 3.7](http://www.phoronix.com/scan.php?page=article&item=btrfs_linux37_mounts&num=1)
        *   [Linux 3.2](http://www.phoronix.com/scan.php?page=article&item=linux_btrfs_options&num=1)
    *   [Lzo vs. zLib](http://blog.erdemagaoglu.com/post/4605524309/lzo-vs-snappy-vs-lzf-vs-zlib-a-comparison-of)
*   **杂项**
    *   [Funtoo Wiki Btrfs Fun](http://www.funtoo.org/wiki/BTRFS_Fun)
    *   [Avi Miller presenting Btrfs](http://www.phoronix.com/scan.php?page=news_item&px=MTA0ODU) at SCALE 10x, January 2012.
    *   [Summary of Chris Mason's talk](http://www.phoronix.com/scan.php?page=news_item&px=MTA4Mzc) from LFCS 2012
    *   [Btrfs: stop providing a bmap operation to avoid swapfile corruptions](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=commit;h=35054394c4b3cecd52577c2662c84da1f3e73525) 2009-01-21
    *   [Doing Fast Incremental Backups With Btrfs Send and Receive](http://marc.merlins.org/perso/btrfs/post_2014-03-22_Btrfs-Tips_-Doing-Fast-Incremental-Backups-With-Btrfs-Send-and-Receive.html)