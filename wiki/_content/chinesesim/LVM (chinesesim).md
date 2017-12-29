**翻译状态：** 本文是英文页面 [LVM](/index.php/LVM "LVM") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-08-12，点击[这里](https://wiki.archlinux.org/index.php?title=LVM&diff=0&oldid=266713)可以查看翻译后英文页面的改动。

相关文章

*   [Software RAID and LVM](/index.php/Software_RAID_and_LVM "Software RAID and LVM")
*   [dm-crypt/Encrypting an entire system#LVM on LUKS](/index.php/Dm-crypt/Encrypting_an_entire_system#LVM_on_LUKS "Dm-crypt/Encrypting an entire system")
*   [dm-crypt/Encrypting an entire system#LUKS on LVM](/index.php/Dm-crypt/Encrypting_an_entire_system#LUKS_on_LVM "Dm-crypt/Encrypting an entire system")
*   [Resizing LVM-on-LUKS](/index.php/Resizing_LVM-on-LUKS "Resizing LVM-on-LUKS")

来自 [Wikipedia:Logical Volume Manager (Linux)](https://en.wikipedia.org/wiki/Logical_Volume_Manager_(Linux) 的解释：

	LVM 是一种可用在[Linux内核](https://en.wikipedia.org/wiki/Linux_kernel "wikipedia:Linux kernel")的[逻辑分卷管理器](https://en.wikipedia.org/wiki/logical_volume_management "wikipedia:logical volume management")；可用于管理磁盘驱动器或其他类似的大容量存储设备。

本文提供如何在 Arch Linux 中配置和使用 Logical Volume Manager (LVM) 的例子。

## Contents

*   [1 LVM基本组成](#LVM.E5.9F.BA.E6.9C.AC.E7.BB.84.E6.88.90)
*   [2 优点](#.E4.BC.98.E7.82.B9)
*   [3 缺点](#.E7.BC.BA.E7.82.B9)
*   [4 在LVM上安装Arch Linux](#.E5.9C.A8LVM.E4.B8.8A.E5.AE.89.E8.A3.85Arch_Linux)
    *   [4.1 创建分区](#.E5.88.9B.E5.BB.BA.E5.88.86.E5.8C.BA)
    *   [4.2 创建物理卷（PV）](#.E5.88.9B.E5.BB.BA.E7.89.A9.E7.90.86.E5.8D.B7.EF.BC.88PV.EF.BC.89)
    *   [4.3 创建卷组（VG）](#.E5.88.9B.E5.BB.BA.E5.8D.B7.E7.BB.84.EF.BC.88VG.EF.BC.89)
    *   [4.4 一步创建卷组](#.E4.B8.80.E6.AD.A5.E5.88.9B.E5.BB.BA.E5.8D.B7.E7.BB.84)
    *   [4.5 创建逻辑卷（LV）](#.E5.88.9B.E5.BB.BA.E9.80.BB.E8.BE.91.E5.8D.B7.EF.BC.88LV.EF.BC.89)
    *   [4.6 建立文件系统与挂载逻辑卷](#.E5.BB.BA.E7.AB.8B.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E4.B8.8E.E6.8C.82.E8.BD.BD.E9.80.BB.E8.BE.91.E5.8D.B7)
    *   [4.7 在mkinitcpio.conf中加入lvm的钩子扩展（hook）](#.E5.9C.A8mkinitcpio.conf.E4.B8.AD.E5.8A.A0.E5.85.A5lvm.E7.9A.84.E9.92.A9.E5.AD.90.E6.89.A9.E5.B1.95.EF.BC.88hook.EF.BC.89)
    *   [4.8 内核参数](#.E5.86.85.E6.A0.B8.E5.8F.82.E6.95.B0)
*   [5 配置](#.E9.85.8D.E7.BD.AE)
    *   [5.1 高级选项](#.E9.AB.98.E7.BA.A7.E9.80.89.E9.A1.B9)
        *   [5.1.1 物理卷](#.E7.89.A9.E7.90.86.E5.8D.B7)
            *   [5.1.1.1 扩增](#.E6.89.A9.E5.A2.9E)
            *   [5.1.1.2 缩小](#.E7.BC.A9.E5.B0.8F)
                *   [5.1.1.2.1 移动物理区域](#.E7.A7.BB.E5.8A.A8.E7.89.A9.E7.90.86.E5.8C.BA.E5.9F.9F)
                *   [5.1.1.2.2 调整物理卷大小](#.E8.B0.83.E6.95.B4.E7.89.A9.E7.90.86.E5.8D.B7.E5.A4.A7.E5.B0.8F)
                *   [5.1.1.2.3 调整分区大小](#.E8.B0.83.E6.95.B4.E5.88.86.E5.8C.BA.E5.A4.A7.E5.B0.8F)
        *   [5.1.2 逻辑卷](#.E9.80.BB.E8.BE.91.E5.8D.B7)
            *   [5.1.2.1 使用lvresize增加或缩小容量](#.E4.BD.BF.E7.94.A8lvresize.E5.A2.9E.E5.8A.A0.E6.88.96.E7.BC.A9.E5.B0.8F.E5.AE.B9.E9.87.8F)
            *   [5.1.2.2 单独设置文件系统大小](#.E5.8D.95.E7.8B.AC.E8.AE.BE.E7.BD.AE.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E5.A4.A7.E5.B0.8F)
    *   [5.2 移除逻辑卷](#.E7.A7.BB.E9.99.A4.E9.80.BB.E8.BE.91.E5.8D.B7)
    *   [5.3 添加物理卷（PV）到卷组（VG）中](#.E6.B7.BB.E5.8A.A0.E7.89.A9.E7.90.86.E5.8D.B7.EF.BC.88PV.EF.BC.89.E5.88.B0.E5.8D.B7.E7.BB.84.EF.BC.88VG.EF.BC.89.E4.B8.AD)
    *   [5.4 从卷组（VG）中移除分区](#.E4.BB.8E.E5.8D.B7.E7.BB.84.EF.BC.88VG.EF.BC.89.E4.B8.AD.E7.A7.BB.E9.99.A4.E5.88.86.E5.8C.BA)
    *   [5.5 快照功能](#.E5.BF.AB.E7.85.A7.E5.8A.9F.E8.83.BD)
        *   [5.5.1 介绍](#.E4.BB.8B.E7.BB.8D)
        *   [5.5.2 配置](#.E9.85.8D.E7.BD.AE_2)
*   [6 常见问题](#.E5.B8.B8.E8.A7.81.E9.97.AE.E9.A2.98)
    *   [6.1 Arch Linux默认设定所必须的设定值](#Arch_Linux.E9.BB.98.E8.AE.A4.E8.AE.BE.E5.AE.9A.E6.89.80.E5.BF.85.E9.A1.BB.E7.9A.84.E8.AE.BE.E5.AE.9A.E5.80.BC)
    *   [6.2 LVM 命令不起作用](#LVM_.E5.91.BD.E4.BB.A4.E4.B8.8D.E8.B5.B7.E4.BD.9C.E7.94.A8)
    *   [6.3 逻辑卷无法显示](#.E9.80.BB.E8.BE.91.E5.8D.B7.E6.97.A0.E6.B3.95.E6.98.BE.E7.A4.BA)
    *   [6.4 在可移除设备上的LVM问题](#.E5.9C.A8.E5.8F.AF.E7.A7.BB.E9.99.A4.E8.AE.BE.E5.A4.87.E4.B8.8A.E7.9A.84LVM.E9.97.AE.E9.A2.98)
    *   [6.5 Resizing a contiguous logical volume fails](#Resizing_a_contiguous_logical_volume_fails)
    *   [6.6 Command "grub-mkconfig" reports "unknown filesystem" errors](#Command_.22grub-mkconfig.22_reports_.22unknown_filesystem.22_errors)
*   [7 更多资源](#.E6.9B.B4.E5.A4.9A.E8.B5.84.E6.BA.90)

### LVM基本组成

LVM利用Linux内核的[device-mapper](http://sources.redhat.com/dm/)来实现存储系统的虚拟化（系统分区独立于底层硬件）。 通过LVM，你可以实现存储空间的抽象化并在上面建立虚拟分区（virtual partitions），可以更简便地扩大和缩小分区，可以增删分区时无需担心某个硬盘上没有足够的连续空间， without getting caught up in the problems of fdisking a disk that is in use (and wondering whether the kernel is using the old or new partition table) and without having to move other partition out of the way. LVM是用来方便管理的，不会提供额外的安全保证。 However, it sits nicely with the other two technologies we are using.

LVM的基本组成块（building blocks）如下：

*   **物理卷Physical volume (PV)**：可以在上面建立卷组的媒介，可以是硬盘分区，也可以是硬盘本身或者回环文件（loopback file）。物理卷包括一个特殊的header，其余部分被切割为一块块物理区域（physical extents）。 Think of physical volumes as big building blocks which can be used to build your hard drive.
*   **卷组Volume group (VG)**：将一组物理卷收集为一个管理单元。Group of physical volumes that are used as storage volume (as one disk). They contain logical volumes. Think of volume groups as hard drives.
*   **逻辑卷Logical volume (LV)**：虚拟分区，由物理区域（physical extents）组成。A "virtual/logical partition" that resides in a volume group and is composed of physical extents. Think of logical volumes as normal partitions.
*   **物理区域Physical extent (PE)**：硬盘可供指派给逻辑卷的最小单位（通常为4MB）。A small part of a disk (usually 4MB) that can be assigned to a logical Volume. Think of physical extents as parts of disks that can be allocated to any partition.

示例:

```
**两块物理硬盘**

  硬盘1 (/dev/sda):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 
    |分区1 50GB (物理卷)           |分区2 80GB (物理卷)            |
    |/dev/sda1                    |/dev/sda2                     |
    |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _ _ _ __|

  硬盘2 (/dev/sdb):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
    |分区1 120GB (物理卷)                         |
    |/dev/sdb1                                   |
    | _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|

```

```
**LVM方式**

  卷组VG1 (/dev/MyStorage/ = /dev/sda1 + /dev/sda2 + /dev/sdb1):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ __ 
    |逻辑卷1 15GB                  |逻辑卷2 35GB                        |逻辑卷3 200GB                         |
    |/dev/MyStorage/rootvol        |/dev/MyStorage/homevol             |/dev/MyStorage/mediavol              |
    |_ _ _ _ _ _ _ _ _ _ _ _ _ _ __|_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ __ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|

```

### 优点

比起正常的硬盘分区管理，LVM更富于弹性：

*   使用卷组(VG)，使众多硬盘空间看起来像一个大硬盘。
*   使用逻辑卷（LV），可以创建跨越众多硬盘空间的分区。
*   可以创建小的逻辑卷（LV），在空间不足时再动态调整它的大小。
*   在调整逻辑卷（LV）大小时可以不用考虑逻辑卷在硬盘上的位置，不用担心没有可用的连续空间。It does not depend on the position of the LV within VG, there is no need to ensure surrounding available space.
*   可以在线（online）对逻辑卷（LV）和卷组（VG）进行创建、删除、调整大小等操作。LVM上的文件系统也需要重新调整大小，某些文件系统也支持这样的在线操作。
*   无需重新启动服务，就可以将服务中用到的逻辑卷（LV）在线（online）/动态（live）迁移至别的硬盘上。
*   允许创建快照，可以保存文件系统的备份，同时使服务的下线时间（downtime）降低到最小。

这些优点使得LVM对服务器的管理非常有用，对于桌面系统管理的帮助则没有那么显著，你需要根据实际情况进行取舍。

### 缺点

*   在系统设置时需要更复杂的额外步骤。

## 在LVM上安装Arch Linux

你应该在安装过程的[分区](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Partitioning (简体中文)")和[创建文件系统](/index.php/File_systems_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.88.9B.E5.BB.BA.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F "File systems (简体中文)")这一步中创建LVM卷， 而且根（root）分区不再通过直接格式化硬盘来创建，而是创建在LVM逻辑卷（LV）上。

快速导览：

*   创建物理卷（PV）所在的分区，设置分区格式为'Linux LVM'，对应的十六进制码为8e（MBR）或8e00（GPT）。
*   创建物理卷（PV）。如果你只有一个硬盘，那么你最好只创建一个分区一个物理卷；如果你有多个硬盘，你可以创建多个分区，在每个分区上分别创建一个物理卷。
*   创建卷组（VG），并把所有物理卷加进卷组。
*   在卷组上创建逻辑卷（LV）。
*   继续[初学者指南](/index.php/Beginners%27_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Beginners' guide (简体中文)")中的格式化分区步骤。
*   当你做到初学者指南中的[创建初始 ramdisk 环境](/index.php/Beginners%27_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#Initramfs "Beginners' guide (简体中文)")时，把 `lvm`加入到 `mkinitcpio.conf`文件中（请参考下文）。

**警告:** 如果你的启动引导程序使用的是[GRUB Legacy](/index.php/GRUB_Legacy_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GRUB Legacy (简体中文)")，那么由于GRUB Legacy不支持LVM，因而你将无法在LVM上创建`/boot`分区。[GRUB](/index.php/GRUB_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GRUB (简体中文)")用户则不会有这个限制。如果你必须使用GRUB Legacy，那么请单独创建并在硬盘上直接格式化`/boot`分区。

### 创建分区

**注意:** 尽管多数情况下推荐首先对磁盘设备进行分区，但根据实际用户需要，该步骤是可选的。

参见[Partitioning](/index.php/Partitioning "Partitioning")对设备进行分区。

### 创建物理卷（PV）

可通过以下命令列出可被用作物理卷的设备：

```
# lvmdiskscan

```

**警告:** 请确认你对正确的设备进行操作，否则会导致文件丢失！

在列出的设备上创建物理卷：

```
 # pvcreate *DEVICE*

```

该命令在各个设备上创建LVM使用的头部。如[#LVM基本组成](#LVM.E5.9F.BA.E6.9C.AC.E7.BB.84.E6.88.90)所示, *DEVICE*可以是磁盘（如`/dev/sda`），分区（如`/dev/sda2`）或环回设备。例如：

```
# pvcreate /dev/sda2

```

你可以用以下命令查看已创建好的物理卷：

```
# pvdisplay

```

**注意:** 如果你用的是未格式化过且擦除块（erase block）大小小于1M的SSD，请采用以下命令`pvcreate --dataalignment 1m /dev/sda`来设置对齐（alignment），可以参考[链接（英文）](http://serverfault.com/questions/356534/ssd-erase-block-size-lvm-pv-on-raw-device-alignment)

### 创建卷组（VG）

创建完成物理卷（PV）之后，下一步就是在该物理卷创建卷组（VG）了。 首先必须先在其中一个物理卷（PV）创建一个卷组

```
# vgcreate <*volume_group*> <*physical_volume*>

```

例如：

```
# vgcreate VolGroup00 /dev/sda2

```

然后让该卷组扩大到其他所有的物理卷:

```
# vgextend <*volume_group*> <*physical_volume*>
# vgextend <*volume_group*> <*another_physical_volume*>
# ...

```

例如：

```
# vgextend VolGroup00 /dev/sdb1
# vgextend VolGroup00 /dev/sdc

```

其中，“VolGroup00”名字换成你自己起的名字即可。接下来可以用以下命令查看卷组：

```
# vgdisplay

```

**注意:** 你可以创建多个的卷组，但这将使你的硬盘空间分布在不同（逻辑）磁盘上。

### 一步创建卷组

LVM支持将卷组与物理卷的创建聚合在一个命令中。例如，为了在前文提到的三个设备中创建名为VolGroup00的卷组，可以执行如下命令：

```
# vgcreate VolGroup00 /dev/sda2 /dev/sdb1 /dev/sdc

```

该命令首先会在分区上创建物理卷（如果之前没有创建过），再创建一个包含三个物理卷的卷组。如果设备上已经存在文件系统，命令会提出警告。

### 创建逻辑卷（LV）

创建完卷组（VG）之后，就可以开始创建逻辑卷（LV）了。输入下面命令以指定新逻辑卷的名字、大小及其所在的卷组：

```
# lvcreate -L <*size*> <*volume_group*> -n <*logical_volume*>

```

例如：

```
# lvcreate -L 10G VolGroup00 -n lvolhome

```

该逻辑卷创建完后，你就可以通过`/dev/mapper/Volgroup00-lvolhome`或`/dev/VolGroup00/lvolhome`来访问它。与卷组命名类似，你可以按你的需要将逻辑卷命名。

你可以指定一个或多个物理卷来限制LVM分配数据空间的位置。比如你希望在较小的SSD硬盘上创建根文件系统，并在较慢的机械硬盘上创建家目录卷，仅需把物理卷设备加入到命令中，例如：

```
# lvcreate -L 10G VolGroup00 -n lvolhome /dev/sdc1

```

如果你想让要创建的逻辑卷拥有卷组（VG）的所有未使用空间，请使用以下命令：

```
# lvcreate -l +100%FREE  <*volume_group*> -n <*logical_volume*>

```

可以通过以下命令来查看逻辑卷：

```
# lvdisplay

```

**注意:** 为了使上述命令能正常运行，你可能需要加载*device-mapper*内核模块（请使用命令**modprobe dm-mod**）。

**提示：** 一开始可以创建小一点的逻辑卷，在卷组里留下一部分未使用空间，以后就可以根据需要再作扩展了。

### 建立文件系统与挂载逻辑卷

现在你的逻辑卷应该已经在`/dev/mapper/`和`/dev/*YourVolumeGroupName*`中了。如果你无法在以上位置找到它，请使用以下命令来加载模块、并扫描与激活卷组：

```
# modprobe dm-mod
# vgscan
# vgchange -ay

```

现在你可以在逻辑卷上创建文件系统并像普通分区一样挂载它了（如果你正在安装Arch linux，需要更详细的信息，请参考[挂载分区](/index.php/Beginners%27_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E6.8C.82.E8.BD.BD.E5.88.86.E5.8C.BA "Beginners' guide (简体中文)")）：

```
# mkfs.<*fstype*> /dev/mapper/<*volume_group*>-<*logical_volume*>
# mount /dev/mapper/<*volume_group*>-<*logical_volume*> /<*mountpoint*>

```

例如：

```
# mkfs.ext4 /dev/mapper/VolGroup00-lvolhome
# mount /dev/mapper/VolGroup00-lvolhome /home

```

**警告:** 挂载点请选择你所新建的逻辑卷（例如：`/dev/mapper/Volgroup00-lvolhome`），**不要**使用逻辑卷所在的实际分区设备（即不要使用：`/dev/sda2`）。

### 在mkinitcpio.conf中加入lvm的钩子扩展（hook）

如果你的根文件系统基于LVM，你需要保证`udev`和`lvm2`这两个[mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")的钩子扩展被启用。

`udev`默认已经预设好，不必手动启用了。你只需要编辑`/etc/mkinitcpio.conf`文件，在`block`与`filesystem`这两项中间插入`lvm2`：

 `/etc/mkinitcpio.conf`  `HOOKS="base udev ... block **lvm2** filesystems"` 

之后你就可以继续下一步的[创建和启用镜像](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.88.9B.E5.BB.BA.E5.92.8C.E5.90.AF.E7.94.A8.E9.95.9C.E5.83.8F "Mkinitcpio (简体中文)")操作了。

### 内核参数

如果你的根文件系统位于逻辑分卷，则`root=` [内核参数](/index.php/%E5%86%85%E6%A0%B8%E5%8F%82%E6%95%B0 "内核参数")必须指向一个映射设备，比如`/dev/mapper/*vg-name*-*lv-name*`。

你可能还需要`dolvm`的支持。

## 配置

### 高级选项

如果你需要监控功能（这对快照是必须的），那么你需要启用lvmetad。 这只需要在`/etc/lvm/lvm.conf`文件中设置`use_lvmetad = 1`选项即可。 目前这个选项已经成为预设选项，不需要手动设置。

可以通过修改`/etc/lvm/lvm.conf`文件中的`auto_activation_volume_list`参数限制自动激活的卷。如果存在问题，可以将此选项注释掉。

#### 物理卷

对于存在物理卷的设备，在扩增其容量之后或缩小其容量之前，必须使用`pvresize`命令对应地增加或减少物理卷的大小。

##### 扩增

增大[分区](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Partitioning (简体中文)")`/dev/sda1`的容量之后，需要执行以下命令扩展物理卷的大小

```
# pvresize /dev/sda1

```

命令将自动探测设备当前大小并将物理卷扩展到其最大容量。

**注意:** 该命令可在卷在线时运行。

##### 缩小

在减少某个物理卷所在设备大小之前，需要通过指定`--setphysicalvolumesize *size*`参数缩小物理卷大小，*例如*：

```
# pvresize --setphysicalvolumesize 40G /dev/sda1

```

该命令可能会提示以下错误：

```
 /dev/sda1: cannot resize to 25599 extents as later ones are allocated.
 0 physical volume(s) resized / 1 physical volume(s) not resized

```

即该物理卷已分配物理区域超过了命令指定的新大小边界，`pvresize`会拒绝将物理卷缩小。若磁盘空间足够，可通过[pvmove](#.E7.A7.BB.E5.8A.A8.E7.89.A9.E7.90.86.E5.8C.BA.E5.9F.9F)将物理区域重新分配至别的卷组来解决这个问题。

###### 移动物理区域

在移动空闲的物理区域到卷尾部之前，需要运行`# pvdisplay -v -m`命令查看物理分段。如下例所示，仅有一个物理卷`/dev/sdd1`, 一个卷组`vg1`和一个逻辑卷`backup`

 `# pvdisplay -v -m` 
```
    Finding all volume groups.
    Using physical volume(s) on command line.
  --- Physical volume ---
  PV Name               /dev/sdd1
  VG Name               vg1
  PV Size               1.52 TiB / not usable 1.97 MiB
  Allocatable           yes 
  PE Size               4.00 MiB
  Total PE              399669
  Free PE               153600
  Allocated PE          246069
  PV UUID               MR9J0X-zQB4-wi3k-EnaV-5ksf-hN1P-Jkm5mW

  --- Physical Segments ---
  Physical extent 0 to 153600:
    FREE
  Physical extent 153601 to 307199:
    Logical volume	/dev/vg1/backup
    Logical extents	1 to 153599
  Physical extent 307200 to 307200:
    FREE
  Physical extent 307201 to 399668:
    Logical volume	/dev/vg1/backup
    Logical extents	153601 to 246068
```

可用空间在卷中段。为了减小物理卷大小，首先必须把所有的已用分段移到前部。

此例中，第一个可用空间在第0至第153600分段共153601个可用区域。我们可以从最后的分段中移动相同数目的物理区域来填补这段空间

 `# pvmove --alloc anywhere /dev/sdd1:307201-399668 /dev/sdd1:0-92466` 
```
/dev/sdd1: Moved: 0.1 %
/dev/sdd1: Moved: 0.2 %
...
/dev/sdd1: Moved: 99.9 %
/dev/sdd1: Moved: 100,0%
```

**Note:**

*   命令将92467 (399668-307201)个物理区域**从**最后一个分段**移动到**第一个分段。由于第一个分段共有153600个空闲的物理区域，可以容纳92467个物理区域，命令可以成功执行。
*   参数`--alloc anywhere`可以用于在同一个分区中移动物理区域的。若要在不同分区中移动，命令形式应该是`# pvmove /dev/sdb1:1000-1999 /dev/sdc1:0-999`
*   当操作的数据较多时，移动操作将持续很久（一到两个小时）。最好在[Tmux](/index.php/Tmux "Tmux")或[GNU Screen](/index.php/GNU_Screen "GNU Screen")会话中执行此过程。任何形式的意外中断都可能会导致致命错误。
*   当操作完成后，可运行[Fsck](/index.php/Fsck "Fsck")保证文件系统完整性。

###### 调整物理卷大小

当所有空闲分段都移动到最后的物理区域时，运行`# vgdisplay`查看。

之后可以再次运行命令：

```
# pvresize --setphysicalvolumesize *size* *PhysicalVolume*

```

结果类似：

 `# pvs` 
```
  PV         VG   Fmt  Attr PSize    PFree 
  /dev/sdd1  vg1  lvm2 a--     1t     500g

```

###### 调整分区大小

最后，你可以用你喜欢的[分区工具](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.88.86.E5.8C.BA.E5.B7.A5.E5.85.B7 "Partitioning (简体中文)")来缩小该分区。

#### 逻辑卷

**注意:** 虽然`lvextend`和`lvreduce`可以实现*lvresize*特定选项实现的功能，且他们都有一个`-r, --resizefs`选项允许文件系统利用`fsadm(8)`（支持*ext2*, [ext3](/index.php/Ext3 "Ext3"), [ext4](/index.php/Ext4 "Ext4"), *ReiserFS*和[XFS](/index.php/XFS "XFS")）同步调节其大小。但除非你要对整个过程有更加精确的控制，直接使用`lvresize`辅以`--resizefs`选项来完成所有工作比较简便。

##### 使用lvresize增加或缩小容量

**警告:** 虽然即便是对根分区，增加文件系统大小一般都可以在线完成（*即*文件系统已经被挂载），缩小其大小往往要求首先卸载文件系统以避免数据丢失。请首先确定你的文件系统支持相关操作。

为了向逻辑组*vg1*中的逻辑卷*lv1*增加2GB空间但*并不*修改其文件系统，执行：

```
# lvresize -L +2G vg1/lv1

```

而从逻辑组`vg1/lv1`中减少500MB空间但*并不*修改其文件系统大小（需要确保[文件系统已经缩小过](/index.php/LVM#.E5.8D.95.E7.8B.AC.E8.AE.BE.E7.BD.AE.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E5.A4.A7.E5.B0.8F "LVM")），执行：

```
# lvresize -L -500M vg1/lv1

```

设置`vg1/lv1`为15GB*并同时*更改其文件系统大小：

```
# lvresize -L 15G -r vg1/lv1

```

**注意:** 仅支持*ext2*, [ext3](/index.php/Ext3 "Ext3"), [ext4](/index.php/Ext4 "Ext4"), *ReiserFS* and [XFS](/index.php/XFS "XFS") [file systems](/index.php/File_systems "File systems")。如果使用不同文件系统请使用[合适的组件](/index.php/File_systems#Arch_Linux_support "File systems")。

如果想将所有可用空间都加入一个卷组，可以执行：

```
# lvresize -l +100%FREE *vg*/*lv*

```

查阅[lvresize(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/lvresize.8)可见详细说明。

##### 单独设置文件系统大小

如果在执行`lv{resize,extend,reduce}`时没有使用`-r, --resizefs`选项， 或文件系统不支持`fsadm(8)`（如[Btrfs](/index.php/Btrfs "Btrfs"), [ZFS](/index.php/ZFS "ZFS")等），则需要在缩小逻辑卷之前或扩增逻辑卷后手动调整文件系统大小。

**警告:** 并非所有文件系统都支持无损或/且在线地调整大小。

例如对于ext2/ext3/ext4文件系统：

```
# resize2fs *vg*/*lv*

```

会将文件系统大小扩展到逻辑卷支持的最大容量，而

```
# resize2fs -M *vg*/*lv*

```

会将文件系统减小到其所需的最小容量。也可以指定具体的尺寸：

```
# resize2fs *vg*/*lv* *NewSize*

```

### 移除逻辑卷

**警告:** 在移除逻辑卷之前，请先备份好数据以免丢失！

首先，找到你所要移除的逻辑卷的名称。你可以使用以下命令来查看系统的所有逻辑卷：

```
# lvs

```

接下来，找到你所要移除的逻辑卷的挂载点

```
$ lsblk

```

并卸载它：

```
# umount /<*mountpoint*>

```

最后，使用以下命令来移除逻辑卷：

```
# lvremove <*volume_group*>/<*logical_volume*>

```

例如：

```
# lvremove VolGroup00/lvolhome

```

请输入`y`来确定你要执行移除逻辑卷操作。

此外，请不要忘了更新`/etc/fstab`。

你可以再次使用`lvs`命令来确认你的逻辑卷已被移除。

### 添加物理卷（PV）到卷组（VG）中

首先创建一个新的物理卷（PV），再把卷组（VG）扩充到该物理卷上：

```
# pvcreate /dev/sdb1
# vgextend VolGroup00 /dev/sdb1
```

这将增加你卷组中的物理区域总数，你可以按需要将它们分配到逻辑卷中。

**注意:** 将[分区表](/index.php/Partitioning "Partitioning")保存在LVM所在媒体设备是个值得借鉴的方式。对于MBR可以使用类型`8e`，或GPT类型`8e00`。

### 从卷组（VG）中移除分区

首先，分区中的所有数据需要被转移到别的分区，幸而LVM提供了以下的简便方式：

```
# pvmove /dev/sdb1

```

如果你想指定所要转移的目标分区，那么可以把该分区作为`pvmove`的第二个参数：

```
# pvmove /dev/sdb1 /dev/sdf1

```

接着，从卷组（VG）中移除物理卷（PV）：

```
# vgreduce myVg /dev/sdb1

```

或者把所有的空物理卷（PV）都移除掉：

```
# vgreduce --all vg0

```

最后，如果你仍然想要使用该分区，而且不想让LVM以为它是一个物理卷，那么你可以执行以下命令：

```
# pvremove /dev/sdb1

```

### 快照功能

#### 介绍

LVM可以给系统创建一个快照，由于使用了写入时复制(copy-on-write) 策略，相比传统的备份更有效率。 初始的快照只有关联到实际数据的inode的实体链接(hark-link)而已。只要实际的数据没有改变，快照就只会包含指向数据的inode的指针，而非数据本身。一旦你更改了快照对应的文件或目录，LVM就会自动拷贝相应的数据，包括快照所对应的旧数据的拷贝和你当前系统所对应的新数据的拷贝。这样的话，只要你修改的数据（包括原始的和快照的）不超过2G，你就可以只使用2G的空间对一个有35G数据的系统创建快照。

#### 配置

你可以像创建普通逻辑卷一样创建快照逻辑卷。

```
# lvcreate --size 100M --snapshot --name snap01 /dev/mapper/vg0-pv

```

你可以修改少于100M的数据直到该快照逻辑卷空间不足为止。

Reverting the modified 'pv' logical volume to the state when the 'snap01' snapshot was taken can be done with

`# lvconvert --merge /dev/vg0/snap01`

In case the origin logical volume is active, merging will occur on the next reboot.(Merging can be done even from a LiveCD)

The snapshot will no longer exist after merging.

Also multiple snapshots can be taken and each one can be merged with the origin logical volume at will.

The snapshot can be mounted and backed up with **dd** or **tar**. The size of the backup file done with **dd** will be the size of the files residing on the snapshot volume. To restore just create a snapshot, mount it, and write or extract the backup to it. And then merge it with the origin.

It is important to have the *dm_snapshot* module listed in the MODULES variable of `/etc/mkinitcpio.conf`, otherwise the system will not boot. If you do this on an already installed system, make sure to rebuild the image with

```
# mkinitcpio -g /boot/initramfs-linux.img

```

Todo: scripts to automate snapshots of root before updates, to rollback... updating menu.lst to boot snapshots (separate article?)

快照可以提供文件系统的冻结副本，主要被用来做备份；一份需要两小时才能完成的（快照）备份比直接备份分区更能保证文件系统映像的一致性。

See [Create root filesystem snapshots with LVM](/index.php/Create_root_filesystem_snapshots_with_LVM "Create root filesystem snapshots with LVM") for automating the creation of clean root file system snapshots during system startup for backup and rollback.

[Dm-crypt/Encrypting an entire system#LVM on LUKS](/index.php/Dm-crypt/Encrypting_an_entire_system#LVM_on_LUKS "Dm-crypt/Encrypting an entire system") and [Dm-crypt/Encrypting an entire system#LUKS on LVM](/index.php/Dm-crypt/Encrypting_an_entire_system#LUKS_on_LVM "Dm-crypt/Encrypting an entire system").

If you have LVM volumes not activated via the [initramfs](/index.php/Initramfs "Initramfs"), [enable](#Using_units) the **lvm-monitoring** service, which is provided by the [lvm2](https://www.archlinux.org/packages/?name=lvm2) package.

## 常见问题

### Arch Linux默认设定所必须的设定值

在`/etc/lvm/lvm.conf`文件中必须设定`use_lvmetad = 1`。现在这个选项已经成为预设值——你可以通过合并`lvm.conf.pacnew`文件来更新你过时的`/etc/lvm/lvm.conf`文件。

### LVM 命令不起作用

*   加载以下模块:

```
# modprobe dm_mod

```

正常情况下，`dm_mod`模块应当被自动加载。假如该模块无法被自动加载，你可以试着修改`/etc/mkinitcpio.conf`：

 `/etc/mkinitcpio.conf:`  `MODULES="dm_mod ..."` 

你需要[重建initramfs](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.88.9B.E5.BB.BA.E5.92.8C.E5.90.AF.E7.94.A8.E9.95.9C.E5.83.8F "Mkinitcpio (简体中文)")来提交你对`/etc/mkinitcpio.conf`的更改。

*   测试以*lvm*开头的命令是否可以被正确执行，例如：

```
# lvm pvdisplay

```

### 逻辑卷无法显示

如果你在挂载某个已创建好的逻辑卷时，发现它没有出现在`lvscan`命令的结果列表里，那么你可以用以下命令去激活它：

```
# vgscan
# vgchange -ay

```

### 在可移除设备上的LVM问题

症状：

```
# vgscan
 Reading all physical volumes.  This may take a while...
 /dev/backupdrive1/backup: read failed after 0 of 4096 at 319836585984: Input/output error
 /dev/backupdrive1/backup: read failed after 0 of 4096 at 319836643328: Input/output error
 /dev/backupdrive1/backup: read failed after 0 of 4096 at 0: Input/output error
 /dev/backupdrive1/backup: read failed after 0 of 4096 at 4096: Input/output error
 Found volume group "backupdrive1" using metadata type lvm2
 Found volume group "networkdrive" using metadata type lvm2

```

产生原因：

	在卷组（VG）失活（deactivate）之前就移除掉外部的LVM设备。在你断开连接之前，需要保证以下命令被执行：

```
# vgchange -an *volume group name*

```

解决方案：（假设你已经用`# vgchange -ay *vg*`命令来激活卷组，但仍有*Input/output error*的错误信息。）执行以下命令：

```
# vgchange -an *volume group name*

```

移除外部设备，稍候几分钟后再执行以下命令：

```
# vgscan
# vgchange -ay *volume group name*

```

### Resizing a contiguous logical volume fails

If trying to extend a logical volume errors with:

```
" Insufficient suitable contiguous allocatable extents for logical volume "

```

The reason is that the logical volume was created with an explicit contiguous allocation policy (options `-C y` or `--alloc contiguous`) and no further adjacent contiguous extents are available (see also [reference](http://www.hostatic.ro/2010/02/15/lvm-inherit-and-contiguous-policies/)).

To fix this, prior to extending the logical volume, change its allocation policy with `lvchange --alloc inherit <logical_volume>`. If you need to keep the contiguous allocation policy, an alternative approach is to move the volume to a disk area with sufficient free extents (see [[1]](http://superuser.com/questions/435075/how-to-align-logical-volumes-on-contiguous-physical-extents)).

### Command "grub-mkconfig" reports "unknown filesystem" errors

Make sure to remove snapshot volumes before generating grub.cfg

## 更多资源

*   [LVM2 Resource Page](http://sourceware.org/lvm2/) on SourceWare.org
*   [LVM HOWTO](http://tldp.org/HOWTO/LVM-HOWTO/) article at The Linux Documentation project
*   [LVM](http://wiki.gentoo.org/wiki/LVM) article at Gentoo wiki
*   [LVM2 Mirrors vs. MD Raid 1](http://www.joshbryan.com/blog/2008/01/02/lvm2-mirrors-vs-md-raid-1/) post by Josh Bryan
*   [Ubuntu LVM Guide Part 1](http://www.tutonics.com/2012/11/ubuntu-lvm-guide-part-1.html)[Part 2 detals snapshots](http://www.tutonics.com/2012/12/lvm-guide-part-2-snapshots.html)