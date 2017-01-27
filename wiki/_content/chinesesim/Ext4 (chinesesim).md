Ext4是Linux上Ext3文件系统的进化。在很多方面，Ext4对于Ext3有着比Ext3对于Ext2更多更深的改变。Ext3主要是针对Ext2添加了日志系统，而Ext4修改了重要的文件系统的数据结构，比如用来存储文件数据的那部分。当然结果就是文件系统有更好的设计，更好的性能，稳定性还有更多的功能。

来源: [Ext4 - Linux Kernel Newbies](http://kernelnewbies.org/Ext4)

## Contents

*   [1 直接创建Ext4分区](#.E7.9B.B4.E6.8E.A5.E5.88.9B.E5.BB.BAExt4.E5.88.86.E5.8C.BA)
*   [2 从Ext2/3迁移到Ext4](#.E4.BB.8EExt2.2F3.E8.BF.81.E7.A7.BB.E5.88.B0Ext4)
    *   [2.1 不转换直接把ext3分区挂载成ext4分区格式](#.E4.B8.8D.E8.BD.AC.E6.8D.A2.E7.9B.B4.E6.8E.A5.E6.8A.8Aext3.E5.88.86.E5.8C.BA.E6.8C.82.E8.BD.BD.E6.88.90ext4.E5.88.86.E5.8C.BA.E6.A0.BC.E5.BC.8F)
    *   [2.2 基本原理](#.E5.9F.BA.E6.9C.AC.E5.8E.9F.E7.90.86)
        *   [2.2.1 步骤](#.E6.AD.A5.E9.AA.A4)
    *   [2.3 转换ext2/3分区到ext4格式](#.E8.BD.AC.E6.8D.A2ext2.2F3.E5.88.86.E5.8C.BA.E5.88.B0ext4.E6.A0.BC.E5.BC.8F)
        *   [2.3.1 基本原理](#.E5.9F.BA.E6.9C.AC.E5.8E.9F.E7.90.86_2)
        *   [2.3.2 步骤](#.E6.AD.A5.E9.AA.A4_2)
*   [3 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [3.1 删除保留块](#.E5.88.A0.E9.99.A4.E4.BF.9D.E7.95.99.E5.9D.97)
*   [4 问题解决](#.E9.97.AE.E9.A2.98.E8.A7.A3.E5.86.B3)
    *   [4.1 数据损坏](#.E6.95.B0.E6.8D.AE.E6.8D.9F.E5.9D.8F)
    *   [4.2 屏障与性能](#.E5.B1.8F.E9.9A.9C.E4.B8.8E.E6.80.A7.E8.83.BD)
        *   [4.2.1 E4rat](#E4rat)
*   [5 参见](#.E5.8F.82.E8.A7.81)

## 直接创建Ext4分区

1.  升级你的系统: `pacman -Syu`
2.  格式化分区: `mkfs.ext4 /dev/sdxY` (查看mkfs.ext4 man帮助获得更多选项)
3.  挂载这个分区
4.  添加相关条目到fstab `/etc/fstab`, 并且修改文件系统类型'type'为 ext4

**提示：** mkfs.ext4 的 man 页面提供了更多选项；编辑 `/etc/mke2fs.conf` 可以修改默认配置。

## 从Ext2/3迁移到Ext4

有两种方法迁移分区从Ext3到Ext4：

*   不转换直接把ext3分区挂载成ext4分区格式 (兼容)
*   转换ext3分区到ext4格式 (性能)

这两种方法下面详细介绍。

### 不转换直接把ext3分区挂载成ext4分区格式

### 基本原理

转换到ext4和继续使用ext3格式的折衷的办法就是把ext3分区当作ext4分区来挂载。

**优点:**

*   兼容性 (分区的文件系统依旧可以用ext3挂载) – 这允许用户继续使用那些不支持ext4文件格式的发行版/操作系统来读取该分区。（例如：带ext3驱动的Windows系统）
*   提高性能（然而性能依然没有完全转换成ext4分区时好） – 具体信息参看[Ext4 - Linux Kernel Newbies](http://kernelnewbies.org/Ext4)。

**缺点:**

*   仅有少部分ext4特性能够使用。（只有那些不改变分区格式的功能能被使用，例如multiblock allocation 和 delayed allocation。）

**注意:** 除了由ext4格式带来的相对新的不一样的特性（可以看作一种潜在风险）之外，**这种技术没有明显缺点**

#### 步骤

1.  修改 `/etc/fstab`，把你想要挂载成ext4的现有ext3分区的'type'栏的内容从 ext3改为ext4。
2.  重新挂载使修改成效。
3.  完成！

### 转换ext2/3分区到ext4格式

#### 基本原理

为了能够使用ext4的全部特性，必须完成一个不可逆转的转换过程。

**优点：**

*   提升性能以及使用新功能 – 细节参见 [Ext4 - Linux Kernel Newbies](http://kernelnewbies.org/Ext4)

**缺点**

*   无法用 ext3 驱动读写 (注意 Windows 中没有已知的 ext4 驱动)
*   不可逆 (ext4 分区无法被 '降级' 到 ext3)

#### 步骤

这些说明是从http://ext4.wiki.kernel.org/index.php/Ext4_Howto 还有 [https://bbs.archlinux.org/viewtopic.php?id=61602](https://bbs.archlinux.org/viewtopic.php?id=61602) 截取下来的。已经在2009年1月16日被作者测试过和确认过了。

*   **升级!** 进行一次整个系统的升级，来保证系统软件符合要求： `pacman -Syu`
*   **[备份!](/index.php/Backup_programs "Backup programs")** 备份准备转换到ext4的ext3分区上所有的数据。尽管ext4被认为日常使用非常稳定，但是仍然是一个年轻的没有经过充分测试的文件系统。何况，这个转换过程只是经过相对简单的测试，因为不可能测试所有各种各样用户可能用到的环境配置。
*   修改 `/etc/fstab` 的'type'栏，把需要转换的所有分区的ext3改为ext4。

**警告:** 如果不启用新的功能（不完全转换）的话，ext4是向下兼容ext3的。也就是不进行下面的步骤，如果用户有个分区需要和其他系统共享数据，但是其他系统并不支持ext4，那么还是可以在不支持ext4的系统中以ext3的方式挂载此分区，而在Arch中以ext4方式挂载。 但是，这样没有完全转换的ext4只拥有和ext3非常少的新特性。

*   使用`e2fsprogs`的转换过程必须在分区没有被挂载前提下进行。如果转换主分区，最简单的方法就是启动到其他live环境（其他支持ext4的环境）。就如同'前提条件'里面所描述的那样。
    *   有必要的话，启动到Live环境.
    *   对于每个需要转换的分区:
        *   确保分区**没有**被挂载
        *   如果要转换的是 ext2，先要增加日志功能，以 root 权限执行：`tune2fs -j /dev/sdxX`。分区变为 ext3 格式。
        *   运行`tune2fs -O extents,uninit_bg,dir_index /dev/分区` (`/dev/分区`替换成需要转换分区的路径，例如`/dev/sda1`)
        *   运行`fsck -fp /dev/分区`

**注意:** 用户**必须**检测(fsck)这个文件系统, 否则这个分区将不可读! 检测磁盘能够让文件系统回到一般状态。**这个过程将在group descriptors找到checksum错误** -- 这个是被预料到的。 '-f'参数要求磁盘检测一定要检查，哪怕文件系统标记是正常的。'-p'参数要求检测的时候能够自动修复(否则，用户将被要求没遇到一个错误确认一次).

*   重新启动 Arch Linux!

**警告:** 如果用户转换了主(/)分区，启动过程可能遇到kernel panic。如果真的出现了，简单的使用fallback模式启动，然后重新创建默认模式：`mkinitcpio -p linux`

## 提示和技巧

### 删除保留块

默认会预留 5% 的文件空间给 root 用户。对现在的大容量硬盘来说是很大的浪费。在下面情况下可以缩小它以节省空间

*   非常大 (例如 >50 G)
*   不被系统文件使用

tune2fs 工具可以完成这个工作，下面的命令将保留比例设置为 1.0%:

```
tune2fs -m 1.0 /dev/sdXY

```

## 问题解决

#### 数据损坏

在强行重启系统之后有可能会遇到数据损坏的情况。请参阅 [Ext4 data loss; explanations and workarounds](http://www.h-online.com/open/Ext4-data-loss-explanations-and-workarounds--/news/112892) 来获取更多信息。

有人发现在 GRUB `menu.lst` 文件的 `kernel` 行后添加 `rootflags=data=ordered` 可以解决这一问题。

kernel 2.6.30 之后，ext4 更安全了，一些补丁提高了 ext4 的稳定性 - 性能上做了牺牲。参数 `auto_da_alloc` 可以禁用此行为。更多信息请访问 [Linux 2 6 30 - 文件系统性能提升](http://kernelnewbies.org/Linux_2_6_30#head-329ba44b44a7f58c98ae22b8f2730418cdd6630d).

2.6.30 之前的内核版本可以在 GRUB 的 `menu.lst` 中的 `kernel` 行加入 `rootflags=data=ordered` 预防问题的发生。

#### 屏障与性能

从内核 2.6.30 开始，ext4 的性能开始下降，原因是由于提供保护数据完整性的功能发生了变化 [[1]](http://www.phoronix.com/scan.php?page=article&item=ext4_then_now&num=1).

*大多数文件系统 (XFS, ext3, ext4, reiserfs) 在fsync之后或者传输提交的时候，发送写屏障信号给磁盘。写屏障信号可以确保正确的写入顺序，是易失性的写入缓存可以安全的使用(损失一些性能)。如果你的磁盘有一种或多种备用电源，禁用屏障可以安全的提升性能。*

*发送写入屏障可以通过使用 barrier=0 挂载选项(对于 ext3, ext4, 和 reiserfs) ，或者使用 nobarrier 挂载选项(对于 XFS)来禁用。* [[2]](http://doc.opensuse.org/products/draft/SLES/SLES-tuning_sd_draft/cha.tuning.io.html).

**警告:** 如果磁盘无法保证在电源掉电时缓存正确写入，禁用写入屏障可以导致严重的文件系统损坏和数据丢失。

要关闭屏障选项，添加 `barrier=0` 选项到 `/etc/fstab` 中想要的文件系统中。例如：

```
# /dev/sda5    /    ext4    noatime,barrier=0    0    1

```

##### E4rat

[E4rat](/index.php/E4rat "E4rat") 是为 ext4 文件系统专门设计的应用程序。它可以监视自开机以来被打开的文件，通过优化它们在分区上所处的位置，并在开机过程之初就预加载它们来提升访问效率。

## 参见

*   [Fstab](/index.php/Fstab_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fstab (简体中文)")