相关文章

*   [File systems](/index.php/File_systems "File systems")
*   [Btrfs - Tips and tricks](/index.php/Btrfs_-_Tips_and_tricks "Btrfs - Tips and tricks")
*   [Mkinitcpio-btrfs](/index.php/Mkinitcpio-btrfs "Mkinitcpio-btrfs")
*   [Snapper](/index.php/Snapper "Snapper")
*   [Installing on Btrfs root](/index.php/Installing_on_Btrfs_root "Installing on Btrfs root")

**翻译状态：** 本文是英文页面 [Btrfs](/index.php/Btrfs "Btrfs") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-11-16，点击[这里](https://wiki.archlinux.org/index.php?title=Btrfs&diff=0&oldid=544462)可以查看翻译后英文页面的改动。

来自 [Btrfs Wiki](https://btrfs.wiki.kernel.org/index.php/Main_Page):

	Btrfs 是一种新型的写时复制 (COW) Linux 文件系统已经并入内核主线。Btrfs 设计实现高级功能的同时，着重于容错、修复以及易于管理。它由 Oracle, Red Hat, Fujitsu, Intel, SUSE, STRATO 等企业和开发者共同开发, Btrfs 以 GNU GPL 协议授权,同时欢迎任何人的贡献.

**Warning:**

*   Btrfs 有一些功能被认为是实验性的特性，可参见内核百科的 [Btrfs 稳定性状态报告](https://btrfs.wiki.kernel.org/index.php/Main_Page#Stability_status)，[Btrfs 足够稳定了吗？](https://btrfs.wiki.kernel.org/index.php/FAQ#Is_btrfs_stable.3F)和[开始使用 Btrfs](https://btrfs.wiki.kernel.org/index.php/Getting_started)。
*   了解当前的[局限性](#局限性).

## Contents

*   [1 准备工作](#准备工作)
*   [2 创建文件系统](#创建文件系统)
    *   [2.1 单一设备上的文件系统](#单一设备上的文件系统)
    *   [2.2 多设备文件系统](#多设备文件系统)
*   [3 配置文件系统](#配置文件系统)
    *   [3.1 写时复制 (CoW)](#写时复制_(CoW))
        *   [3.1.1 停用 CoW](#停用_CoW)
        *   [3.1.2 创建轻量副本](#创建轻量副本)
    *   [3.2 压缩](#压缩)
    *   [3.3 子卷](#子卷)
        *   [3.3.1 创建子卷](#创建子卷)
        *   [3.3.2 列出子卷列表](#列出子卷列表)
        *   [3.3.3 删除子卷](#删除子卷)
        *   [3.3.4 挂载子卷](#挂载子卷)
        *   [3.3.5 改变默认子卷](#改变默认子卷)
    *   [3.4 配额](#配额)
    *   [3.5 提交间隔](#提交间隔)
    *   [3.6 SSD TRIM](#SSD_TRIM)
*   [4 使用](#使用)
    *   [4.1 显示已使用的/空闲空间](#显示已使用的/空闲空间)
    *   [4.2 碎片整理](#碎片整理)
    *   [4.3 RAID](#RAID)
    *   [4.4 Scrub](#Scrub)
        *   [4.4.1 手动启动](#手动启动)
        *   [4.4.2 通过服务或者定时器启动](#通过服务或者定时器启动)
    *   [4.5 Balance](#Balance)
    *   [4.6 快照](#快照)
    *   [4.7 发送和接收](#发送和接收)
    *   [4.8 去重](#去重)
*   [5 已知问题](#已知问题)
    *   [5.1 加密](#加密)
    *   [5.2 交换文件](#交换文件)
    *   [5.3 TLP](#TLP)
*   [6 提示和技巧](#提示和技巧)
    *   [6.1 无分区 Btrfs 磁盘](#无分区_Btrfs_磁盘)
    *   [6.2 从 Ext3/4 转换](#从_Ext3/4_转换)
    *   [6.3 Checksum 硬件加速](#Checksum_硬件加速)
    *   [6.4 损坏恢复](#损坏恢复)
    *   [6.5 引导进入快照](#引导进入快照)
    *   [6.6 Use Btrfs subvolumes with systemd-nspawn](#Use_Btrfs_subvolumes_with_systemd-nspawn)
*   [7 故障排除](#故障排除)
    *   [7.1 GRUB](#GRUB)
        *   [7.1.1 分区偏移](#分区偏移)
        *   [7.1.2 Missing root](#Missing_root)
    *   [7.2 BTRFS: open_ctree failed](#BTRFS:_open_ctree_failed)
    *   [7.3 检查 btrfs 文件系统](#检查_btrfs_文件系统)
*   [8 另见](#另见)

## 准备工作

Btrfs 支持已经包含在[linux](https://www.archlinux.org/packages/?name=linux)和[linux-lts](https://www.archlinux.org/packages/?name=linux-lts)的内核中.

要使用一些用户空间工具的话，需要[安装](/index.php/Install "Install") 不在 [base](https://www.archlinux.org/groups/x86_64/base/) 包组中的而且基础操作必须的 [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) 软件包。

如果你需要从 Btrfs 文件系统引导（比如说你的内核和内存盘在一个 Btrfs 的分区上），请检查你的 [启动引导器](https://wiki.archlinux.org/index.php/Arch_boot_process_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)) 是否支持 Btrfs。

## 创建文件系统

下文展示了如何创建一个新的 Btrfs [文件系统](/index.php/File_systems_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "File systems (简体中文)")。要将一个 ext3/4 分区转换为 Btrfs，请参考 [#从_Ext3/4_转换](#从_Ext3/4_转换)。要使用无分区的配置，请参考 [#无分区_Btrfs_磁盘](#无分区_Btrfs_磁盘)。

查阅 [mkfs.btrfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.btrfs.8) 以获取更多信息。

### 单一设备上的文件系统

在分区 `/dev/*partition*` 上创建一个 Btrfs 文件系统：

```
# mkfs.btrfs -L *mylabel* /dev/*partition*

```

Btrfs 的默认块大小为 16KB。 要使用更大的 blocksize 数据/元数据的话，可以通过指定 `-n` 来修改 `nodesize`，正如本例所示的设置为 16KB:

```
# mkfs.btrfs -L *mylabel* -n 16k /dev/*partition*

```

### 多设备文件系统

**Warning:** Btrfs 的 RAID 5 和 RAID 6 模式存在致命缺陷, 不应当用于任何场景，除非用来做丢失数据的测试。 查阅 [the Btrfs page on RAID5 and RAID6](https://btrfs.wiki.kernel.org/index.php/RAID56) 以获取最新动态。

多个设备可以用来创建一组 RAID。支持的RAID级别有 RAID 0,RAID 1,RAID 10,RAID 5 和 RAID 6。数据和元数据的 RAID 等级可以独立地用 `-d` 和 `-m` 参数指定。默认情况下元数据使用镜像 (RAID1)，而数据则会被条带化 (RAID0)。参阅 [Btrfs Wiki:在多个设备上使用 btrfs](https://btrfs.wiki.kernel.org/index.php/Using_Btrfs_with_Multiple_Devices) 或查阅 `mkfs.btrfs` 的手册页获得更多信息.

```
# mkfs.btrfs -d raid0 -m raid1 /dev/*part1* /dev/*part2* ...

```

要将多个 Btrfs 设备作为一个池使用的话，你需要将 `udev` 钩子或者 `btrfs` 钩子加入到 `/etc/mkinitcpio.conf` 中。查阅 [Mkinitcpio_(简体中文)#常用钩子](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#常用钩子 "Mkinitcpio (简体中文)")以获取更多信息。

**Note:**

*   磁盘阵列中的各个磁盘大小不一样可能会导致不能使用所有磁盘的完整空间。为了充分利用所有磁盘的容量，使用 `-d single` 而不是 `-d raid0 -m raid1` （元数据镜像，数据非镜像且非条带化）
*   挂载一个这样的文件系统可能会导致除了对应的 *.device* 的所有任务卡死且 Systemd 可能因为无法正确处理多设备 btrfs 文件系统上的每一个设备而不能正常启动，详见这个 [BUG 报告](https://github.com/systemd/systemd/issues/1921)。
*   有些[启动加载器](/index.php?title=%E5%90%AF%E5%8A%A8%E5%8A%A0%E8%BD%BD%E5%99%A8&action=edit&redlink=1 "启动加载器 (page does not exist)")不支持多设备文件系统，比如 [Syslinux](/index.php/Syslinux "Syslinux")。

[RAID](#RAID) 中有关于维护多设备上的 btrfs 文件系统的一些建议.

## 配置文件系统

### 写时复制 (CoW)

默认情况下 btrfs 对所有文件使用 [写时复制 (CoW)](https://en.wikipedia.org/wiki/copy-on-write "wikipedia:copy-on-write")。参阅[the Btrfs Sysadmin Guide section](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Copy_on_Write_.28CoW.29) 以获取实现细节以及它的优点和缺点。

#### 停用 CoW

要对某个子卷上的新文件停用写时复制，使用 `nodatacow` 挂载选项。这只会影响新创建的文件，写时复制仍然会在已存在的文件上生效。`nodatacow` 参数同样会禁用压缩。参阅 [btrfs(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/btrfs.5) 以了解细节。

**Note:** 来自 Btrfs Wiki [Mount options](https://btrfs.wiki.kernel.org/index.php/Mount_options): within a single file system, it is not possible to mount some subvolumes with `nodatacow` and others with `datacow`. The mount option of the first mounted subvolume applies to any other subvolumes.

**Note:** 根据 Btrfs Wiki [Mount options](https://btrfs.wiki.kernel.org/index.php/Mount_options): 在单个文件系统中，无法使用 `nodatacow` 参数挂载某些子卷，而其他的使用 `datacow` 参数。第一个被挂载子卷的挂载参数将会应用于其他所有子卷。

要单文件或目录禁用写时复制特性，请使用下面的命令：

```
$ chattr +C *[文件/目录的地址(path)]*

```

这会为这个文件的单个引用停用写时复制,如果这个文件不只有一个引用(例如通过 `cp --reflink=always` 生成或者在文件系统快照中),写时复制依然生效.

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

#### 创建轻量副本

默认情况下，使用 `cp` 复制 Btrfs 文件系统上的文件时，会创建实际副本。要创建引用原始数据的轻量级副本，请使用 *reflink* 选项：

```
$ cp --reflink *source* *dest* 

```

参阅 `cp` 的手册页获得关于 `--reflink` 标志的更多信息。

### 压缩

Btrfs支持透明压缩，这意味着分区里的每个文件都被自动压缩。这不单减小了文件的大小，在某些特定的场景下（比如单线程、重文件 I/O）还[提高了性能](http://www.phoronix.com/scan.php?page=article&item=btrfs_compress_2635&num=1)，尽管在其他的场景下（比如多线程和/或具有大文件 I/O 的 CPU 密集型任务）显著得影响了性能。使用更快的压缩算法比如 *zstd* 和 *lzo* 通常可以获得更好的性能，这个[性能测试](https://www.phoronix.com/scan.php?page=article&item=btrfs-zstd-compress) 提供了详细的对比。

压缩可以通过使用挂载参数 `compress` 来启用，它的可选值包括 `zlib`，`lzo`，`zstd` 或者是 `no` （不启用压缩）。只有在加入挂载选项后创建或修改的文件才会被压缩。

不过也可以在安装以后通过 `btrfs filesystem defragment -c*alg*` (也可以使用其它压缩算法,例如 `zlib` / `lzo`) 压缩一个分区 (例如从 ext3/4 转换以后的文件系统).

要将整个文件系统通过 [zstd](https://www.archlinux.org/packages/?name=zstd) 重新压缩,运行下面的命令:

```
# btrfs filesystem defragment -r -v -czstd /

```

在一个新的 btrfs 分区上安装 Arch Linux 时,要充分利用压缩特性，最好安装时就启用压缩功能。在[File systems](/index.php/File_systems "File systems") 时使用 `compress` 参数: `mount -o compress=lzo /dev/sd*xY* /mnt/`.在 时把 `compress=lzo` 添加到 [fstab](/index.php/Fstab "Fstab") 中的根目录中的选项上。

**Tip:** 通过 `chattr +c` ,也可以在不使用 `compress` 选项的情况下为单个文件启用压缩属性.对目录启用会使这个目录下新文件自动压缩.

**Warning:**

*   如果你使用 `zstd` 这个参数的话，使用没有 `zstd` 支持的旧版本内核或者 [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) 可能不能读取或者修复你的文件系统。
*   [GRUB](/index.php/GRUB "GRUB") 和 [rEFInd](/index.php/REFInd "REFInd") 目前缺少对 *zstd* 的支持，请使用没有启用 *zstd* 选项的独立 boot 分区或者使用其他已被支持的算法重新压缩引导文件，比如： `$ btrfs filesystem defragment -v -clzo /boot/*` 

### 子卷

"btrfs 子卷不是 (也不能看作) 块设备,一个子卷可以看作 POSIX 文件名字空间.这个名字空间可以通过子卷上层访问,也可以独立挂载."[[1]](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Subvolumes)

每个 btrfs 文件系统都有一个 ID 为 5 的顶层子卷。它可以挂载为 `/`（默认情况下），或者可以挂载为另一个子卷。子卷可以在文件系统中移动，它们通过其 ID 而不是路径来标识。

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

可以使用 `subvol=*/path/to/subvolume*` 或 `subvolid=*objectid'*` *挂载标志来安装子卷，就像文件系统分区一样。例如，您可以拥有一个名为 `subvol_root` 的子卷，并将其挂载为 `/`。通过在文件系统的顶层创建各种子卷，然后将它们安装在适当的挂载点，可以模仿传统的文件系统分区。 因此，可以使用[#Snapshots](#Snapshots)轻松地将文件系统（或其一部分）恢复到先前的状态。*

**Tip:** 为了方便地修改子卷的结构，请考虑创建新的子卷，然后挂载为 `/` 而不是使用顶层子卷 (ID=5) 挂载为根目录（这是默认行为）。

**Note:** “大多数挂载选项适用于**整个文件系统**，并且只有要挂载的第一个子卷的选项才会生效。 这是因为没有实现，未来可能会发生变化。” [[2]](https://btrfs.wiki.kernel.org/index.php/Mount_options) 查阅[Btrfs Wiki FAQ](https://btrfs.wiki.kernel.org/index.php/FAQ#Can_I_mount_subvolumes_with_different_mount_options.3F) 以了解哪些挂载参数能够被用于独立的子卷

参阅 [Snapper#Suggested filesystem layout](/index.php/Snapper#Suggested_filesystem_layout "Snapper"), [Btrfs SysadminGuide#Managing Snapshots](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Managing_Snapshots) 和 [Btrfs SysadminGuide#Layout](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Layout) 获得子卷应用的示例.

有关特定于btrfs的挂载选项的完整列表，请参阅 [btrfs(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/btrfs.5)。

#### 改变默认子卷

如果挂载时不指定 `subvol=` 选项便会挂载默认子卷.要改变默认子卷:

```
# btrfs subvolume set-default *subvolume-id* /

```

*subvolume-id* 可以通过[#列出子卷列表](#列出子卷列表)获得.

**Note:** 在安装了 [GRUB](/index.php/GRUB "GRUB") 的系统上,在改变默认子卷以后不要忘记运行 `grub-install` . 参见 [this forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1615373).

通过 `btrfs subvolume set-default` 修改默认子卷将会导致文件系统的最顶层无法访问，除非使用 `subvol=/` 或者 `subvolid=5` 挂载参数。[[3]](https://btrfs.wiki.kernel.org/index.php/SysadminGuide)

### 配额

**Warning:** Qgroup 尚且不稳定且在有（过多）快照的子卷上应用配额可能会导致性能问题，比如在删除快照的时候。 此外，这里还有更多 [已知问题](https://btrfs.wiki.kernel.org/index.php/Quota_support#Known_issues).

Btrfs中的配额支持是通过使用配额组或 qgroup 在子卷级别实现的：默认情况下，每个子卷都以 *0/<subvolume id>* 的形式分配配额组。 但是，如果需要的话，可以使用任意数字创建配额组。

要使用 qgroup，你需要首先启用它：

```
# btrfs quota enable <path>

```

从此时开始，新创建的子卷将由这些配额组控制。 为了能够为已创建的子卷启用配额，首先正常启用配额，然后使用它们的 *<subvolume id>* 为每个子卷创建一个配额组，再重新扫描它们：

```
# btrfs subvolume list <path> | cut -d' ' -f2 | xargs -I{} -n1 btrfs qgroup create 0/{} <path>
# btrfs quota rescan <path>

```

Btrfs 中的配额组形成树层次结构，其中 qgroup 附加到子卷。大小限制由每个 qgroup 独立配置且在并在包含给定子卷的树中达到任何限制时应用。

配额组的限制可以应用于总数据使用，非共享数据使用，压缩数据使用或全部。文件复制和文件删除可能都会影响限制，因为如果删除原始卷的文件并且只剩下一个副本，则另一个 qgroup 的非共享限制可能会更改。例如，新快照几乎与原始子卷共享所有块，对子卷的新写入将向专用限制提升，一个卷中的公共数据的删除将升高到另一个卷中的专用限制。

要对 qgroup 应用限制，请使用命令 `btrfs qgroup limit`。根据你的使用情况，使用总限制，非共享限制（ `-e`）或压缩限制（ `-c`）。

显示文件系统使用中给定路径的使用情况和限制：

```
# btrfs qgroup show -reF <path>

```

### 提交间隔

将数据写入文件系统的频率由 Btrfs 本身和系统的设置决定。Btrfs 默认设置为 30 秒检查点间隔，新数据将在 30 秒内被提交到文件系统。 这可以通过在 `/etc/fstab` 增加 `commit` 挂载参数来修改：

```
LABEL=arch64 / btrfs defaults,noatime,compress=lzo,commit=120 0 0

```

系统范围的设置也会影响提交间隔。它们包括 `/proc/sys/vm/*` 下的文件，这超出了本维基文章的范围，因此不再赘述。 它们的内核文档位于 `Documentation/sysctl/vm.txt`。

### SSD TRIM

Btrfs 文件系统能够从支持 TRIM 命令的 SSD 驱动器中释放未使用的块。

有关启用和使用 TRIM 的更多信息，请参阅 [Solid State Drives#TRIM](/index.php/Solid_State_Drives#TRIM "Solid State Drives")。

## 使用

### 显示已使用的/空闲空间

像 `df` 这样的用户空间工具可能不会准确的计算剩余空间 (因为并没有分别计算文件和元数据的使用情况) 。推荐使用 `btrfs filesystem usage` 来查看使用情况。比如说：

```
# btrfs filesystem usage /

```

**Note:** The `btrfs filesystem usage` 在 `RAID5/RAID6` 设备上可能无法正常工作。

查看 [[4]](https://btrfs.wiki.kernel.org/index.php/FAQ#How_much_free_space_do_I_have.3F) 以获取更多信息。

### 碎片整理

Btrfs 支持通过配置 [挂载参数](https://btrfs.wiki.kernel.org/index.php/Manpage/btrfs(5)#MOUNT_OPTIONS) `autodefrag` 来实现在线的碎片整理。要手动整理你的根目录的话，可以使用：

```
# btrfs filesystem defragment -r /

```

使用不带 `-r` 开关的上述命令将导致仅整理该目录的子卷所拥有的元数据。这允许通过简单地指定路径进行单个文件碎片整理。

对具有 CoW 副本（快照副本或使用`cp --reflink`或 bcp 创建的文件）进行碎片整理以及使用带压缩算法的 `-c` 开关进行碎片整理可能会导致生成两个不相关的文件从而增加磁盘使用量。

### RAID

Btrfs 提供对 RAID 一类的 [#多设备文件系统](#多设备文件系统)的原生支持.参阅 [the Btrfs wiki page](https://btrfs.wiki.kernel.org/index.php/Using_Btrfs_with_Multiple_Devices) 获得更多信息. [Btrfs 管理员手册](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#RAID_and_data_replication) 提供了技术背景信息.

**Warning:** 奇偶校验 RAID（RAID 5/6）代码中存在多个严重的数据丢失错误。 检查 Btrfs 的 Wiki [RAID5/6 page](https://btrfs.wiki.kernel.org/index.php/RAID56) 和 BUG 汇报 [linux-btrfs mailing list](https://www.mail-archive.com/linux-btrfs@vger.kernel.org/msg55161.html) 以获取更多信息。

### Scrub

[Btrfs Wiki 术语表](https://btrfs.wiki.kernel.org/index.php/Glossary)中写到 scrub 是一种 "在线文件系统检查工具".它读取文件系统中的文件和元数据,并使用校验值和 RAID 存储上的镜像区分并修复损坏的数据.

**Warning:** 运行 scrub 会阻止系统待机, 详见 [这个讨论](http://comments.gmane.org/gmane.comp.file-systems.btrfs/33106).

#### 手动启动

启动一个（后台运行的）包含 `/` 目录的文件系统在线检查任务：

```
# btrfs scrub start /

```

检查该任务的运行状态：

```
# btrfs scrub status /

```

#### 通过服务或者定时器启动

[btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) 软件包带有 `btrfs-scrub@.timer` 系统单元,用来每月运行 scrub 命令.通过添加挂载点的参数来[启用](/index.php/Enable "Enable")它,例如`btrfs-scrub@-.timer` (`/`) 或者 `btrfs-scrub@home.timer` (`/home`).

也可以通过[启动](/index.php/Starting "Starting") `btrfs-scrub@.service` 来手动运行 scrub (使用同样的挂载点参数) ,相对于 `# btrfs scrub` 这么做的优点是会记录在 [Systemd 日志](/index.php/Systemd_journal "Systemd journal")中。

### Balance

“Balance 将会通过分配器再次传递文件系统中的所有数据。它主要用于在添加或删除设备时跨设备重新平衡文件系统中的数据。如果设备出现故障，余额将为冗余 RAID 级别重新生成缺失的副本。”[[5]](https://btrfs.wiki.kernel.org/index.php/Glossary)。参阅 [上游的 FAQ](https://btrfs.wiki.kernel.org/index.php/FAQ#What_does_.22balance.22_do.3F).

在单设备文件系统上，余额对于（临时）减少分配但未使用（元）数据块的数量也是有用的。有时候这对于解决 ["filesystem full" 故障](https://btrfs.wiki.kernel.org/index.php/FAQ#Help.21_Btrfs_claims_I.27m_out_of_space.2C_but_it_looks_like_I_should_have_lots_left.21) 来说也是必须的。

```
# btrfs balance start /
# btrfs balance status /

```

### 快照

"快照是和特定子卷共享文件和元数据的特殊子卷, 利用了 btrfs 的写时复制特性." 详见 [Btrfs Wiki SysadminGuide#Snapshots](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Snapshots).

要创建一个快照:

```
# btrfs subvolume snapshot *source* [*dest*/]*name*

```

`*source*`为要创建快照的对象，`[*dest*/]*name*`为快照安放路径。

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
 # btrfs send -p /root_backup /root_backup_new | btrfs receive /backup

```

现在你 `/backup` 的快照会是 `root_backup_new`.

参阅 [Btrfs Wiki's Incremental Backup page](https://btrfs.wiki.kernel.org/index.php/Incremental_Backup) 获得更多信息 (例如使用工具自动化这一过程)。

### 去重

使用写时复制，Btrfs能够复制文件或整个子卷而无需实际复制数据。但是，无论何时更改文件，都会创建一个新的 “真正的” 副本。重复数据删除更进一步，通过主动识别共享公共序列的数据块并将它们组合到具有相同写时复制语义的范围内。

专用于 Btrfs 分区去重的工具包括 [duperemove](https://aur.archlinux.org/packages/duperemove/)，[bedup](https://aur.archlinux.org/packages/bedup/) 和 *btrfs-dedup*。人们可能还希望仅使用基于文件的级别对数据进行重复数据删除，比如 [rmlint](https://www.archlinux.org/packages/?name=rmlint) 或者 [jdupes](https://aur.archlinux.org/packages/jdupes/)。有关这些程序的可用功能的概述和其他信息，请查看[上游 Wiki 条目](https://btrfs.wiki.kernel.org/index.php/Deduplication#Batch)。

此外，Btrfs开发人员正致力于带内（也称为同步或内联）重复数据删除，这意味着在将新数据写入文件系统时完成重复数据删除。目前，它仍然是一个在 out-of-tree 开发的实验。愿意测试新功能的用户可以阅读[相关的内核 Wiki 页](https://btrfs.wiki.kernel.org/index.php/User_notes_on_dedupe)。

## 已知问题

一些在尝试之前应该知道的限制。

### 加密

Btrfs 目前还没有内建的加密支持，但未来[可能](https://lwn.net/Articles/700487/)加入此功能。可以在运行`mkfs.btrfs`前加密分区，参阅[Dm-crypt with LUKS](/index.php/Dm-crypt_with_LUKS "Dm-crypt with LUKS").

(如果已经创建了文件系统，可以使用[EncFS](/index.php/EncFS "EncFS")或[TrueCrypt](/index.php/TrueCrypt "TrueCrypt"),但是这样会无法使用 btrfs 的一些功能。)

### 交换文件

Btrfs 不支持交换文件，因为 Btrfs 有潜在的文件系统损坏风险，没有加入交换文件需要的功能，参阅[这里](https://btrfs.wiki.kernel.org/index.php/FAQ#Does_btrfs_support_swap_files.3F)。交换文件可以挂载到 loop 设备中，但是性能比较差。[systemd-loop-swapfile](https://aur.archlinux.org/packages/systemd-loop-swapfile/)提供了需要的服务文件。

### TLP

使用 TLP 需要特殊的预防措施，以避免文件系统损坏。有关更多信息，请参阅[TLP＃Btrfs](/index.php?title=TLP%EF%BC%83Btrfs&action=edit&redlink=1 "TLP＃Btrfs (page does not exist)")。

## 提示和技巧

### 无分区 Btrfs 磁盘

**Warning:** 大多数用户不希望这种类型的设置，应该在常规分区上安装 Btrfs。 此外，GRUB 强烈建议不要安装到无分区磁盘。

Btrfs 能在整个设备上使用,替代 [MBR](/index.php/MBR "MBR") 或 [GPT](/index.php/GPT "GPT") 分区表,但是并不要求一定这么做,最简单的方法是 [在一个已存在的分区上创建 btrfs 文件系统](#Creating_a_new_file_system). 如果你选择用 btrfs 替代分区表, 可以用 [子卷](#Subvolumes)模拟不同的分区。下列是在单个无分区设备上使用 Btrfs 文件系统的限制:

*   不能在不同的 [挂载点](/index.php/Fstab "Fstab") 上使用不同的[文件系统](/index.php/File_systems "File systems").
*   不能使用 [交换空间](/index.php/Swap_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Swap (简体中文)") (因为 btrfs 不支持 [交换文件](/index.php/Swap_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BA.A4.E6.8D.A2.E6.96.87.E4.BB.B6 "Swap (简体中文)") 而且硬盘上没有空间用来创建 [交换分区](/index.php/Swap_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BA.A4.E6.8D.A2.E5.88.86.E5.8C.BA "Swap (简体中文)").) 这同时也限制了睡眠和休眠 (因为需要交换空间) .
*   不能使用 [UEFI](/index.php/UEFI "UEFI") 启动.

运行下面的命令把整个设备的分区表替换成 btrfs:

```
# mkfs.btrfs /dev/sd*X*

```

如果设备上存在分区表，则需要使用：

```
# mkfs.btrfs -f /dev/sd*X*

```

例如 `/dev/sda` 而不是 `/dev/sda1`. 后一种形式会格式化现有的分区而不是替换掉原有的分区表.

像使用普通的 MBR 分区表存储设备一样安装 [启动管理器](/index.php/Boot_loader "Boot loader"), 参考 [Syslinux#Manual install](/index.php/Syslinux#Manual_install "Syslinux") 或 [GRUB/Tips and tricks#Install to partition or partitionless disk](/index.php/GRUB/Tips_and_tricks#Install_to_partition_or_partitionless_disk "GRUB/Tips and tricks")。

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

请记住，之前安装的某些应用程序必须适配 Btrfs。值得注意的是 [TLP＃Btrfs](/index.php?title=TLP%EF%BC%83Btrfs&action=edit&redlink=1 "TLP＃Btrfs (page does not exist)") 需要特别小心以避免文件系统损坏，但其他应用程序也可能从某些功能中获益。

### Checksum 硬件加速

要验证Btrfs校验和是否是硬件加速：

 `$ dmesg | grep crc32c`  `Btrfs loaded, crc32c=crc32c-intel` 

如果你看到 `crc32c=crc32c-generic`，这很有可能是因为你的根分区是 Btrfs，你将会需要编译 `crc32c-intel` 进入内核并启用它。将 `crc32c-intel` 放入 [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") 是 *不会* 生效的。

### 损坏恢复

*btrfs-check* 不能在一个已挂载的文件系统上工作。为了能够在不从 Live USB 启动的情况下使用 *btrfs-check*，需要将其添加到初始内存盘：

 `/etc/mkinitcpio.conf`  `BINARIES=("/usr/bin/btrfs")` 

[Regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs")。

之后如果启动时出现问题，则可以使用该实用程序进行修复。

**Note:** 如果 fsck 进程必须使空间缓存（和/或其他缓存？）无效，那么后续引导挂起一段时间是正常的（它可能会给出关于 btrfs-transaction 挂起的控制台消息）。系统应该在一段时间后从中恢复。

查阅 [Btrfs Wiki 页](https://btrfs.wiki.kernel.org/index.php/Btrfsck) 以获取更多信息。

### 引导进入快照

为了能够引导进入快照，你必须通过 [内核参数](/index.php/Kernel_parameters#Configuration "Kernel parameters") `rootflags=subvol=*/path/to/subvolume*` 来指定子卷，同时需要修改 `/etc/fstab` 使用 `subvol=` 来指定相同的子卷。或者，子卷可以用其 id 来指定 - 例如可以用例如可检索的。 `btrfs subvolume list */root/path*` - 和`rootflags=subvolid=*objectid*` 分别作为内核参数`subvolid= *objectid*` 作为 `/etc/fstab` 中的挂载选项。

如果使用 GRUB，则可以在 [grub-btrfs](https://aur.archlinux.org/packages/grub-btrfs/) 或 [grub-btrfs-git](https://aur.archlinux.org/packages/grub-btrfs-git/) 的帮助下重新生成配置文件时使用 Btrfs 快照自动填充启动菜单。

### Use Btrfs subvolumes with systemd-nspawn

查阅 [Systemd-nspawn#Use Btrfs subvolume as container root](/index.php/Systemd-nspawn#Use_Btrfs_subvolume_as_container_root "Systemd-nspawn") 和 [Systemd-nspawn#Use temporary Btrfs snapshot of container](/index.php/Systemd-nspawn#Use_temporary_Btrfs_snapshot_of_container "Systemd-nspawn") 等文章。

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