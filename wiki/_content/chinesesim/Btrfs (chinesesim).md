**翻译状态：** 本文是英文页面 [Btrfs](/index.php/Btrfs "Btrfs") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-10-14，点击[这里](https://wiki.archlinux.org/index.php?title=Btrfs&diff=0&oldid=401804)可以查看翻译后英文页面的改动。

来自 [Wikipedia:Btrfs](https://en.wikipedia.org/wiki/Btrfs "wikipedia:Btrfs")

**Btrfs**（B-tree 文件系统，通常念成 **Butter FS**，**Better FS**或**B-tree FS**），一种支持写入时复制（COW）的文件系统，运行在 Linux 操作系统上，采用 [GPL](https://en.wikipedia.org/wiki/GPL "wikipedia:GPL") 授权。[Oracle](/index.php/Oracle "Oracle") 于 2007 年对外宣布这项计划，并发布源代码，2014 年 8 月发布稳定版。目标是取代 [Linux](/index.php/Linux "Linux") 当时主流的 [ext3](/index.php/Ext3 "Ext3") 文件系统，摆脱 ext3 的一些限制，特別是单文件大小，文件系统总大小和文件校验，并加入 ext3 不支持的一些功能，比如可写快照（writable snapshots）、快照的快照（snapshots of snapshots）、内建磁盘阵列（RAID），以及子卷（subvolumes）。Btrfs 也宣称专注于「容错、修复及易于管理」。

Btrfs 是一个比较新的 Linux 文件系统，已经并入内核主线。Btrfs 设计实现高级功能的同时，着重于容错、修复以及易于管理。

**警告:**

*   Btrfs 有一些功能被认为是实验性的特性，可参见内核百科的 [Btrfs 稳定性状态报告](https://btrfs.wiki.kernel.org/index.php/Main_Page#Stability_status)，[Btrfs 足够稳定了吗？](https://btrfs.wiki.kernel.org/index.php/FAQ#Is_btrfs_stable.3F)和[开始使用 Btrfs](https://btrfs.wiki.kernel.org/index.php/Getting_started)。
*   当前[局限性](#.E5.B1.80.E9.99.90.E6.80.A7).

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 附加软件包](#.E9.99.84.E5.8A.A0.E8.BD.AF.E4.BB.B6.E5.8C.85)
*   [2 Btrfs 一般管理工作](#Btrfs_.E4.B8.80.E8.88.AC.E7.AE.A1.E7.90.86.E5.B7.A5.E4.BD.9C)
    *   [2.1 文件系统创建](#.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E5.88.9B.E5.BB.BA)
    *   [2.2 从 Ext3/4转换](#.E4.BB.8E_Ext3.2F4.E8.BD.AC.E6.8D.A2)
    *   [2.3 挂载选项](#.E6.8C.82.E8.BD.BD.E9.80.89.E9.A1.B9)
        *   [2.3.1 例如](#.E4.BE.8B.E5.A6.82)
    *   [2.4 显示使用/可用空间](#.E6.98.BE.E7.A4.BA.E4.BD.BF.E7.94.A8.2F.E5.8F.AF.E7.94.A8.E7.A9.BA.E9.97.B4)
*   [3 局限性](#.E5.B1.80.E9.99.90.E6.80.A7)
    *   [3.1 加密](#.E5.8A.A0.E5.AF.86)
    *   [3.2 交换文件](#.E4.BA.A4.E6.8D.A2.E6.96.87.E4.BB.B6)
    *   [3.3 GRUB2 和 core.img](#GRUB2_.E5.92.8C_core.img)
    *   [3.4 Linux-rt 内核](#Linux-rt_.E5.86.85.E6.A0.B8)
*   [4 Btrfs 特性](#Btrfs_.E7.89.B9.E6.80.A7)
    *   [4.1 写时复制 （Copy-On-Write (CoW)）](#.E5.86.99.E6.97.B6.E5.A4.8D.E5.88.B6_.EF.BC.88Copy-On-Write_.28CoW.29.EF.BC.89)
    *   [4.2 多设备文件系统和RAID特性](#.E5.A4.9A.E8.AE.BE.E5.A4.87.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E5.92.8CRAID.E7.89.B9.E6.80.A7)
        *   [4.2.1 多设备文件系统](#.E5.A4.9A.E8.AE.BE.E5.A4.87.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
        *   [4.2.2 RAID特性](#RAID.E7.89.B9.E6.80.A7)
    *   [4.3 子卷](#.E5.AD.90.E5.8D.B7)
        *   [4.3.1 创建子卷](#.E5.88.9B.E5.BB.BA.E5.AD.90.E5.8D.B7)
        *   [4.3.2 子卷列表](#.E5.AD.90.E5.8D.B7.E5.88.97.E8.A1.A8)
        *   [4.3.3 设置默认子卷](#.E8.AE.BE.E7.BD.AE.E9.BB.98.E8.AE.A4.E5.AD.90.E5.8D.B7)
        *   [4.3.4 快照](#.E5.BF.AB.E7.85.A7)
    *   [4.4 碎片整理](#.E7.A2.8E.E7.89.87.E6.95.B4.E7.90.86)
    *   [4.5 压缩](#.E5.8E.8B.E7.BC.A9)
    *   [4.6 Checkpoint interval](#Checkpoint_interval)
    *   [4.7 分区](#.E5.88.86.E5.8C.BA)
    *   [4.8 Scrub](#Scrub)
    *   [4.9 Balance](#Balance)
    *   [4.10 SSD TRIM](#SSD_TRIM)
*   [5 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [5.1 GRUB](#GRUB)
        *   [5.1.1 分区偏移](#.E5.88.86.E5.8C.BA.E5.81.8F.E7.A7.BB)
        *   [5.1.2 Missing root](#Missing_root)
    *   [5.2 BTRFS: open_ctree failed](#BTRFS:_open_ctree_failed)
    *   [5.3 btrfs check](#btrfs_check)
        *   [5.3.1 btrfs check example](#btrfs_check_example)
*   [6 参阅](#.E5.8F.82.E9.98.85)

## 安装

Btrfs 已经包含在[linux](https://www.archlinux.org/packages/?name=linux)和[linux-lts](https://www.archlinux.org/packages/?name=linux-lts)的内核中，安装系统时会默认安装[btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs)工具。

[GRUB 2](/index.php/GRUB "GRUB"),[mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")和 [Syslinux](/index.php/Syslinux "Syslinux") 已经支持 Btrfs，不需要额外配置。

### 附加软件包

*   [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) 包括 *btrfsck* 工具，可以修复 Btrfs 文件系统的错误。
*   [btrfs-progs-git](https://aur.archlinux.org/packages/btrfs-progs-git/) 每日构建

**Tip:** 见 [Btrfs Wiki Getting Started](https://btrfs.wiki.kernel.org/index.php/Getting_started) for suggestions regarding running Btrfs effectively.

## Btrfs 一般管理工作

### 文件系统创建

可以新建或者从已有文件系统转化为 Btrfs.

格式化分区：

```
# mkfs.btrfs /dev/<partition>

```

**Note:** As of [this](https://git.kernel.org/cgit/linux/kernel/git/mason/btrfs-progs.git/commit/?id=c652e4efb8e2dd76ef1627d8cd649c6af5905902) commit (November 2013), Btrfs default blocksize is 16KB.

使用更大的blocksize数据/元数据,为`nodesize`通过指定一个值`-n`开关使用16kb块如本例所示:

```
# mkfs.btrfs -L *mylabel* -n 16k /dev/*partition*

```

用户可选择多个设备来创建RAID。支持的RAID级别有 RAID 0、RAID 1和RAID 10。默认情况下，元数据使用镜像，而数据被 strip. See [Using Btrfs with Multiple Devices](https://btrfs.wiki.kernel.org/index.php/Using_Btrfs_with_Multiple_Devices) for more information about how to create a Btrfs RAID volume.

```
# mkfs.btrfs [*options*] /dev/*part1* /dev/*part2* ...

```

### 从 Ext3/4转换

从安装 CD 启动，然后转化分区:

```
# btrfs-convert /dev/*partition*

```

挂载转换后的分区并修改`/etc/fstab`文件，指定分区类型(**type** 为 btrfs，**fs_passno** [最后一列] 修改为0，Btrfs在启动时并不进行磁盘检查). 还要注意的是分区的UUID将有改变，所以使用UUID时，更新fstab中相应的。 `chroot` 到系统并重建 GRUB 条目（如果对此过程不熟悉，参考[Install from existing Linux](/index.php/Install_from_existing_Linux "Install from existing Linux")和[GRUB](/index.php/GRUB "GRUB")）。 If converting a root filesystem, while still chrooted run `mkinitcpio -p linux` to regenerate the initramfs or the system will not successfully boot. If you get stuck in grub with 'unknown filesystem' try reinstalling grub with `grub-install /dev/*partition*` and regenerate the config as well `grub-mkconfig -o /boot/grub/grub.cfg`.

确认没有问题后,完成转换通过删除备份`ext2_saved`子卷，请注意，如果没了它(备份子卷)，你将没办法还原回 ext3/4 文件系统。

```
# btrfs subvolume delete /ext2_saved

```

最后[balance](#Balance) 回收空间的文件系统上。

### 挂载选项

**Warning:** 为 btrfs 指定挂载选项有可能会关闭一些保险的特性，并且会增加导致文件系统完整性被损坏的风险。

参阅 [Btrfs Wiki Mount options](https://btrfs.wiki.kernel.org/index.php/Mount_options) and [Btrfs Wiki Gotchas](https://btrfs.wiki.kernel.org/index.php/Gotchas) for more information.

除了配置,可以在创建或在文件系统的过程中,各种挂载选项对Btrfs可以大大改变其性能特征。

因为这是一个文件系统仍然在开发中,应该预期变化和回归。见链接[#参阅](#.E5.8F.82.E9.98.85)部分基准。

#### 例如

*   **Linux 3.15**
    *   Btrfs在SSD系统安装和强调最大化性能 (参阅 [#SSD TRIM](#SSD_TRIM))

    	 `noatime,discard,ssd,compress=lzo,space_cache` 

    *   Btrfs 用于存档目的硬盘(HDD)上以最大化空间为重点。

    	 `noatime,autodefrag,compress-force=lzo,space_cache` 

### 显示使用/可用空间

General linux userspace tools such as `/usr/bin/df` will inaccurately report free space on a Btrfs partition since it does not take into account space allocated for and used by the metadata. It is recommended to use `/usr/bin/btrfs` to query a Btrfs partition. Below is an illustration of this effect, first querying using `df -h`, and then using `btrfs filesystem df`:

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

Notice that `df -h` reports 3.0GB used but `btrfs filesystem df` reports 2.73GB for the data. This is due to the way Btrfs allocates space into the pool. The true disk usage is the sum of all three 'used' values which is inferior to 3.0GB as reported by `df -h`.

**Note:** If you see an entry of type `unknown` in the output of `btrfs filesystem df` at kernel >= 3.15, this is a display bug. As of [this patch](http://thread.gmane.org/gmane.comp.file-systems.btrfs/34419), the entry means GlobalReserve, which is kind of a buffer for changes not yet flushed. This entry is displayed as `unknown, single` in RAID setups and is not possible to re-balance.

Another useful command to show a less verbose readout of used space is `btrfs filesystem show`:

 `# btrfs filesystem show /dev/sda3` 
```
failed to open /dev/sr0: No medium found
Label: 'arch64'  uuid: 02ad2ea2-be12-2233-8765-9e0a48e9303a
	Total devices 1 FS bytes used 2.91GB
	devid    1 size 118.95GB used 4.02GB path /dev/sda2

Btrfs v0.20-rc1-358-g194aa4a-dirty

```

## 局限性

使用前请了解如下局限。

### 加密

Btrfs 目前还没有内建的加密支持，但可以在运行`mkfs.btrfs`前加密分区，参阅[Dm-crypt with LUKS](/index.php/Dm-crypt_with_LUKS "Dm-crypt with LUKS").

(如果已经创建了文件系统，可以使用[EncFS](/index.php/EncFS "EncFS")或[TrueCrypt](/index.php/TrueCrypt "TrueCrypt"),但是这样会无法使用 btrfs 的一些功能。)

### 交换文件

Btrfs 不支持交换文件，因为 Btrfs 因为潜在的文件系统损坏风险，没有加入交换文件需要的功能，参阅[这里](https://btrfs.wiki.kernel.org/index.php/FAQ#Does_btrfs_support_swap_files.3F). 交换文件可以挂载到 loop 设备中，但是性能比较差。[systemd-loop-swapfile](https://aur.archlinux.org/packages/systemd-loop-swapfile/)提供了需要的服务文件。

### GRUB2 和 core.img

[Grub 2](/index.php/GRUB "GRUB")可以启动Btrfs分区，但是因为模块比较大， grub-install 安装的 core.img 文件超过了 MBR 与第一个分区见的空间大小。可以通过使用GPT或在第一个分区前空出1-2M的空间避免此问题。

### Linux-rt 内核

在版本 3.14.12_rt9中, [linux-rt](/index.php/Kernel#-rt "Kernel") 内核不能引导Btrfs文件系统，这是因为 *rt* 补丁集的开发相对缓慢导致的。

## Btrfs 特性

各种特征可用，并可以调整。

### 写时复制 （Copy-On-Write (CoW)）

CoW(写时复制)具有许多优点，但是对大文件的随机小写入有一定的负面性能影响。可以使用 recomended 为数据库文件和虚拟磁盘文件禁用CoW。 你可以在挂载时使用”nodatacow“选项来禁用整个块的CoW特性。这将禁用整个文件系统的CoW特性。 为单文件或目录禁用CoW特性，请使用下面的命令：

```
# chattr +C [文件/目录的地址(path)]

```

注意，chattr的man手册写着:在btrfs上，'C' 标志应该被设置在新建的或者是空白的文件/目录，如果被设置在已有数据的文件,当块分配给该文件时，文件将不确定是否完全稳定。如果'C' 标志被设置给一个目录，将不会影响目前的目录，但在该目录创建的新文件将具有No_COW属性。

### 多设备文件系统和RAID特性

参阅 [Using Btrfs with Multiple Devices](https://btrfs.wiki.kernel.org/index.php/Using_Btrfs_with_Multiple_Devices) for suggestions.

#### 多设备文件系统

当创建*btrfs*文件系统时，你可以将任意个分区或磁盘设备传给*mkfs.btrfs*。创建的文件系统将跨这些设备。你可以按这种办法**"**合并**"**多个分区或设备来得到一个大*btrfs*文件系统。

也可从现存的btrfs文件系统中增加或移除设备（务必小心）。

多设备*btrfs*文件系统（也称为一个btrfs卷）需要运行

```
 # btrfs device scan

```

才能被识别。这就是 *btrfs* mkinitcpio hook 或 /etc/rc.conf 的 *USEBTRFS* 变量的用途。

#### RAID特性

创建跨多设备文件系统时，你也可指定加入文件系统的设备使用RAID0、RAID1或RAID10。

**Note:** 在内核 3.19 版本中，恢复(recovery)和重建(rebuild)的代码已经被集成了。这个地步的实现对于大多数用途而言应该是有用的。由于这是新的代码，你应当期望它在接下去的几个内核发布版本中能够稳定。

When creating a multi-device filesystem, one can also specify to use RAID0, RAID1, RAID10, RAID5 or RAID6 across the devices comprising the filesystem. RAID levels can be applied independently to data and metadata. By default, metadata is duplicated on single volumes or RAID1 on multi-disk sets.

Btrfs works in block-pairs for raid0, raid1, and raid10\. This means:

raid0 - block-pair striped across 2 devices

raid1 - block-pair written to 2 devices

The raid level can be changed while the disks are online using the `btrfs balance` command:

```
# btrfs balance start -mconvert=RAIDLEVEL -dconvert=RAIDLEVEL /path/to/mount

```

For 2 disk sets, this matches raid levels as defined in md-raid (mdadm). For 3+ disk-sets, the result is entirely different than md-raid.

For example:

*   Three 1TB disks in an md based raid1 yields a `/dev/md0` with 1TB free space and the ability to safely lose 2 disks without losing data.
*   Three 1TB disks in a Btrfs volume with data=raid1 will allow the storage of approximately 1.5TB of data before reporting full. Only 1 disk can safely be lost without losing data.

Btrfs uses a round-robin scheme to decide how block-pairs are spread among disks. As of Linux 3.0, a quasi-round-robin scheme is used which prefers larger disks when distributing block pairs. This allows raid0 and raid1 to take advantage of most (and sometimes all) space in a disk set made of multiple disks. For example, a set consisting of a 1TB disk and 2 500GB disks with data=raid1 will place a copy of every block on the 1TB disk and alternate (round-robin) placing blocks on each of the 500GB disks. Full space utilization will be made. A set made from a 1TB disk, a 750GB disk, and a 500GB disk will work the same, but the filesystem will report full with 250GB unusable on the 750GB disk. To always take advantage of the full space (even in the last example), use data=single. (data=single is akin to JBOD defined by some raid controllers) See [the Btrfs FAQ](https://btrfs.wiki.kernel.org/index.php/FAQ#How_much_space_do_I_get_with_unequal_devices_in_RAID-1_mode.3F) for more info.

### 子卷

子卷是btrfs的特性之一。子卷实质上是一个保存文件和目录的命名的B树。它们的inode保存在树根之树中，可以为非根用户和组所有。子卷可选设定块配额。子卷内的所有块和文件区段都有引用计数以便做快照。和虚拟机存储的动态扩展相似，其只按需使用设备空间，消除了许多半满的分区。用户也可用不同的挂载选项挂载子卷，得到更灵活的安全性。

See the following links for more details:

*   [Btrfs Wiki SysadminGuide#Subvolumes](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Subvolumes)
*   [Btrfs Wiki Getting started#Basic Filesystem Commands](https://btrfs.wiki.kernel.org/index.php/Getting_started#Basic_Filesystem_Commands)
*   [Btrfs Wiki Trees](https://btrfs.wiki.kernel.org/index.php/Trees)

#### 创建子卷

创建子卷：

```
# btrfs subvolume create [<dest>/]

```

为提高灵活性，把系统安装到专用的子卷，在内核启动参数中使用：

 `rootflags=subvol=<whatever you called the subvol>` 

它使得系统可以回滚。

如果用在根分区，建议在`/etc/mkinitcpio.conf`的modules数组里加上**crc32c**，在 HOOKS 里加上 `btrfs`。

#### 子卷列表

查看当前的子卷的列表：:

```
# btrfs subvolume list -p .

```

#### 设置默认子卷

**Warning:** Changing the default subvolume with `btrfs subvolume set-default` will make the top level of the filesystem inaccessible, except by use of the `subvolid=0` mount option. Reference: [Btrfs Wiki Sysadmin Guide](https://btrfs.wiki.kernel.org/index.php/SysadminGuide).

The default sub-volume is mounted if no `subvol=` mount option is provided.

```
# btrfs subvolume set-default *subvolume-id* /.

```

**例如:**

 `# btrfs subvolume list .` 
```
ID 258 gen 9512 top level 5 path root_subvolume
ID 259 gen 9512 top level 258 path home
ID 260 gen 9512 top level 258 path var
ID 261 gen 9512 top level 258 path usr

```

```
# btrfs subvolume set-default 258 .

```

**重置:**

```
# btrfs subvolume set-default 0 .

```

#### 快照

参阅 [Btrfs Wiki SysadminGuide#Snapshots](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Snapshots) for details.

创建快照：

```
# btrfs subvolume snapshot <source> [<dest>/]<name>

```

快照不是递归包含的，这意味着子卷内的子卷在快照里是空目录。

### 碎片整理

Btrfs支持在线碎片整理。要整理根目录的元数据，只需运行：

```
# btrfs filesystem defragment /

```

这*不会*整理整个文件系统。查看更多信息，参考btrfs wiki上的[this page](https://btrfs.wiki.kernel.org/index.php/Problem_FAQ#Defragmenting_a_directory_doesn.27t_work)。

### 压缩

Btrfs支持透明压缩，这意味着分区里的每个文件都被自动压缩。这不单减小了文件的大小，还[提高了性能](http://www.phoronix.com/scan.php?page=article&item=btrfs_compress_2635&num=1)，特别是在使用[lzo算法](http://www.phoronix.com/scan.php?page=article&item=btrfs_lzo_2638&num=1)时。用`compress=gzip`或`compress=lzo`挂载选项打开压缩功能。只有在加入挂载选项后创建或修改的文件会被压缩，所以要充分利用压缩特性，最好安装时就启用压缩功能。在[准备硬盘](/index.php/Beginners%27_guide#Prepare_hard_drive "Beginners' guide")时，切换到另一个终端(`Ctrl+Alt+数字`)，运行如下命令：

```
# mount -o remount,compress=lzo /dev/sdXY /mnt/target

```

安装完成后，将`compress=lzo`加入到`/etc/fstab`的根文件系统挂载选项中。

### Checkpoint interval

Starting with Linux 3.12, users are able to change the checkpoint interval from the default 30 s to any value by appending the `commit` mount option in `/etc/fstab` for the btrfs partition.

```
LABEL=arch64 / btrfs defaults,noatime,ssd,compress=lzo,commit=120 0 0

```

### 分区

Btrfs can occupy an entire data storage device, replacing the [MBR](/index.php/MBR "MBR") or [GPT](/index.php/GPT "GPT") partitioning schemes. One can use [subvolumes](#Sub-volumes) to simulate partitions.

这种方法有一些限制在单一磁盘设置:

*   Cannot use different [file systems](/index.php/File_systems "File systems") for different [mount points](/index.php/Fstab "Fstab").
*   Cannot use [swap area](/index.php/Swap "Swap") as Btrfs does not support [swap files](/index.php/Swap#Swap_file "Swap") and there is no place to create [swap partition](/index.php/Swap#Swap_partition "Swap"). This also limits the use of hibernation/resume, which needs a swap area to store the hibernation image.
*   Cannot use [UEFI](/index.php/UEFI "UEFI") to boot.

Btrfs覆盖现有的分区表,运行以下命令:

```
# mkfs.btrfs /dev/sd*X*

```

Do not specify `/dev/sda*X*` or it will format an existing partition instead of replacing the entire partitioning scheme.

Install the [boot loader](/index.php/Boot_loader "Boot loader") in a like fashion to installing it for a data storage device with a [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record"). For example:

```
# grub-install --recheck /dev/sd*X*

```

for [GRUB](/index.php/GRUB#Install_to_440-byte_MBR_boot_code_region "GRUB").

**Warning:** Using the `btrfs subvolume set-default` command to change the default sub-volume from anything other than the top level (ID 0) may break Grub. See [#Setting a default sub-volume](#Setting_a_default_sub-volume) to reset.

### Scrub

See [Btrfs Wiki Glossary](https://btrfs.wiki.kernel.org/index.php/Glossary).

```
# btrfs scrub start /
# btrfs scrub status /

```

**Warning:** The running scrub process will prevent the system from suspending, see [this thread](http://comments.gmane.org/gmane.comp.file-systems.btrfs/33106) for details.

If running the scrub as a systemd service, use `Type=forking`. Alternatively, you can pass the `-B` flag to `btrfs scrub start` to run it in the foreground and use the default `Type` value.

### Balance

See [Upstream FAQ page](https://btrfs.wiki.kernel.org/index.php/FAQ#What_does_.22balance.22_do.3F).

Since [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs)-3.12 *balancing* is a background process - see `man 8 btrfs-balance` for full description.

```
# btrfs balance start /
# btrfs balance status /

```

### SSD TRIM

If mounted with the `discard` option, a Btrfs filesystem will automatically free unused blocks from an SSD drive supporting the TRIM command.

Note that before SATA 3.1, TRIM commands are synchronous and will block all I/O while running. This may cause short freezes while this happens, for example during a filesystem sync. You may not want to use `discard` in that case but enable regular trims instead:

```
# systemctl enable fstrim.timer

```

One way to check your SATA version is with:

```
# smartctl --info /dev/sd*X*

```

## 故障排除

See the [Btrfs Problem FAQ](https://btrfs.wiki.kernel.org/index.php/Problem_FAQ) for general troubleshooting.

### GRUB

#### 分区偏移

**Note:** The offset problem may happen when you try to embed `core.img` into a partitioned disk. It means that [it is OK](https://wiki.archlinux.org/index.php?title=Talk:Btrfs&diff=319474&oldid=292530) to embed grub's `corg.img` into a Btrfs pool on a partitionless disk (e.g. `/dev/sd*X*`) directly.

[GRUB](/index.php/GRUB "GRUB") can boot Btrfs partitions however the module may be larger than other [file systems](/index.php/File_systems "File systems"). And the `core.img` file made by `grub-install` may not fit in the first 63 sectors (31.5KiB) of the drive between the MBR and the first partition. Up-to-date partitioning tools such as `fdisk` and `gdisk` avoid this issue by offsetting the first partition by roughly 1MiB or 2MiB.

#### Missing root

Users experiencing the following: `error no such device: root` when booting from a RAID style setup then edit /usr/share/grub/grub-mkconfig_lib and remove both quotes from the line `echo " search --no-floppy --fs-uuid --set=root ${hints} ${fs_uuid}"`. Regenerate the config for grub and the system should boot without an error.

### BTRFS: open_ctree failed

As of November 2014 there seems to be a bug in [systemd](/index.php/Systemd "Systemd") or [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") causing the following error on systems with multi-device Btrfs filesystem using the `btrfs` hook in `mkinitcpio.conf`:

```
BTRFS: open_ctree failed
mount: wrong fs type, bad option, bad superblock on /dev/sdb2, missing codepage or helper program, or other error

In some cases useful info is found in syslog - try dmesg|tail or so.

You are now being dropped into an emergency shell.

```

A workaround is to remove `btrfs` from the `HOOKS` array in `/etc/mkinitcpio.conf` and instead adding `btrfs` to the `MODULES` array. Then regenerate the initramfs with `mkinitcpio -p linux` (adjust the preset if needed) and reboot.

See the [original forums thread](https://bbs.archlinux.org/viewtopic.php?id=189845) and [FS#42884](https://bugs.archlinux.org/task/42884) for further information and discussion.

You will get same error if you trying mount raid array without one device. A workaround is to use mount options `degraded`. Important use this options in `/etc/fstab` and `/etc/grub.d/10_linux` if you want to be sure that system will boot from btrfs raid array. add `rootflags=degraded` in `GRUB_CMDLINE_LINUX`

### btrfs check

The *[btrfs check](https://btrfs.wiki.kernel.org/index.php/Manpage/btrfs-check)* command can be used to check or repair an unmounted Btrfs filesystem. However, this repair tool is still immature and not able to repair certain filesystem errors even those that do not render the filesystem unmountable.

#### btrfs check example

**Warning:** Since Btrfs is under heavy development, especially the `btrfs check` command, it is highly recommended to consult the following Btfrs documentation before executing `btrfs check` with the `--repair` switch: [Btrfsck](https://btrfs.wiki.kernel.org/index.php/Btrfsck).

**Note:** The following scenario assumes that, after an unexpected shutdown, the filesystem cannot be mounted and the partition is encrypted.

	Methodology

**Note:** Make a backup first first. This can be done by using dd: `# dd if=/path/of/tryingToResuePatrition of=/path/to/backUp.iso`

*   Firstly, boot from an Arch Live USB
*   Then decrypt the backUp.iso (skip this step if this is not the case)

```
$ cryptsetup /path/buckUp .iso name
$ btrfs check /dev/mapping/name

```

*   If the previous steps were successful, execute the following:

```
$ btrfs check --repair /dev/mapping/name

```

Finally, try to mount the filesystem to see if the problem is fixed. If the mount was successful, the process can be repeated on a real partition.

## 参阅

*   **官方网站**
    *   [Btrfs Wiki](https://btrfs.wiki.kernel.org/)
    *   [Btrfs Wiki Glossary](https://btrfs.wiki.kernel.org/index.php/Glossary)
*   **官方FAQs**
    *   [Btrfs Wiki FAQ](https://btrfs.wiki.kernel.org/index.php/FAQ)
    *   [Btrfs Wiki Problem FAQ](https://btrfs.wiki.kernel.org/index.php/Problem_FAQ)
*   **Btrfs pull requests**
    *   [3.14](http://lkml.indiana.edu/hypermail/linux/kernel/1401.3/03045.html)
    *   [3.13](http://lkml.indiana.edu/hypermail/linux/kernel/1311.1/03526.html)
    *   [3.12](http://lkml.indiana.edu/hypermail/linux/kernel/1309.1/02981.html)
    *   [3.11](http://lkml.indiana.edu/hypermail/linux/kernel/1305.1/01064.html)
*   **性能相关**
    *   [Btrfs on raw disks?](http://superuser.com/questions/432188/should-i-put-my-multi-device-btrfs-filesystem-on-disk-partitions-or-raw-devices)
    *   [Varying leafsize and nodesize in Btrfs](http://comments.gmane.org/gmane.comp.file-systems.btrfs/19440)
    *   [Btrfs support for efficient SSD operation (data blocks alignment)](http://comments.gmane.org/gmane.comp.file-systems.btrfs/15646)
    *   [Is Btrfs optimized for SSDs?](https://btrfs.wiki.kernel.org/index.php/FAQ#Is_Btrfs_optimized_for_SSD.3F)
    *   **Phoronix mount option benchmarking**
        *   [Linux 3.14](http://www.phoronix.com/scan.php?page=article&item=linux_314_btrfs)
        *   [Linux 3.11](http://www.phoronix.com/scan.php?page=article&item=linux_btrfs_311&num=1)
        *   [Linux 3.9](http://www.phoronix.com/scan.php?page=news_item&px=MTM0OTU)
        *   [Linux 3.7](http://www.phoronix.com/scan.php?page=article&item=btrfs_linux37_mounts&num=1)
        *   [Linux 3.2](http://www.phoronix.com/scan.php?page=article&item=linux_btrfs_options&num=1)
    *   [Lzo vs. zLib](http://blog.erdemagaoglu.com/post/4605524309/lzo-vs-snappy-vs-lzf-vs-zlib-a-comparison-of)
*   **Miscellaneous**
    *   [Funtoo Wiki Btrfs Fun](http://www.funtoo.org/wiki/BTRFS_Fun)
    *   [Avi Miller presenting Btrfs](http://www.phoronix.com/scan.php?page=news_item&px=MTA0ODU) at SCALE 10x, January 2012.
    *   [Summary of Chris Mason's talk](http://www.phoronix.com/scan.php?page=news_item&px=MTA4Mzc) from LFCS 2012
    *   [Btrfs: stop providing a bmap operation to avoid swapfile corruptions](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=commit;h=35054394c4b3cecd52577c2662c84da1f3e73525) 2009-01-21
    *   [Doing Fast Incremental Backups With Btrfs Send and Receive](http://marc.merlins.org/perso/btrfs/post_2014-03-22_Btrfs-Tips_-Doing-Fast-Incremental-Backups-With-Btrfs-Send-and-Receive.html)