相关文章

*   [Arch boot process](/index.php/Arch_boot_process "Arch boot process")
*   [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table")
*   [Partitioning](/index.php/Partitioning "Partitioning")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")

**翻译状态：** 本文是英文页面 [Master_Boot_Record](/index.php/Master_Boot_Record "Master Boot Record") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-08-25，点击[这里](https://wiki.archlinux.org/index.php?title=Master_Boot_Record&diff=0&oldid=445496)可以查看翻译后英文页面的改动。

主引导记录 [Master Boot Record](https://en.wikipedia.org/wiki/Master_Boot_Record "w:Master Boot Record")(MBR) 是指一个存储设备的开头 512 字节。它包含操作系统的引导器和存储设备的分区表。在 [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") 系统的 [启动过程](/index.php/Boot_process "Boot process") 中扮演重要角色。

**注意:** 作为新的分区方案， [GPT](/index.php/GPT "GPT") ( [UEFI](/index.php/UEFI "UEFI") 标准的一部分) 也能通过[保护分区](https://en.wikipedia.org/wiki/GUID_Partition_Table#Legacy_MBR_.28LBA_0.29 "wikipedia:GUID Partition Table")在 BIOS 系统上使用。GPT 解决了一些 MBR 的遗留问题但又造成了许多兼容问题。更多见 [GUID Partition Table#Master Boot Record](/index.php/GUID_Partition_Table#Master_Boot_Record "GUID Partition Table")。

## Contents

*   [1 关于主引导记录(MBR)](#.E5.85.B3.E4.BA.8E.E4.B8.BB.E5.BC.95.E5.AF.BC.E8.AE.B0.E5.BD.95.28MBR.29)
    *   [1.1 MBR 导致的问题](#MBR_.E5.AF.BC.E8.87.B4.E7.9A.84.E9.97.AE.E9.A2.98)
*   [2 启动过程](#.E5.90.AF.E5.8A.A8.E8.BF.87.E7.A8.8B)
*   [3 备份与还原](#.E5.A4.87.E4.BB.BD.E4.B8.8E.E8.BF.98.E5.8E.9F)
*   [4 恢复 Windows 引导记录](#.E6.81.A2.E5.A4.8D_Windows_.E5.BC.95.E5.AF.BC.E8.AE.B0.E5.BD.95)
*   [5 TestDisk MBRCode](#TestDisk_MBRCode)
*   [6 另见](#.E5.8F.A6.E8.A7.81)

## 关于主引导记录(MBR)

MBR 分区表像下面这样把分区信息存储在第一个扇区:

| HDD 上的位置 | 代码的用意 |
| `001-440 bytes` | 由 BIOS 启动的 MBR 启动代码 |
| `441-446 bytes` | MBR 硬盘签名 |
| `447-510 bytes` | 分区表 (主分区和扩展分区，而非逻辑分区) |
| `511-512 bytes` | MBR 启动签名 0xAA55. |

所有主分区的信息都被限制在分配给的64B空间里。为了扩展，我们采用了扩展分区。一个扩展分区就像是 MBR 上的一个主分区，它是其他被称为逻辑分区的分区的容器。所以一块硬盘被限制为四个主分区或者三个主分区加一个内有许多逻辑分区的扩展分区。

### MBR 导致的问题

1.  只能有四个主分区或者三个主分区加一个扩展分区 (以及在扩展分区中的任意数量的逻辑分区). 如果你有三个主分区加一个扩展分区以及除此之外的空闲空间，在空闲空间之上你无法创立分区。
2.  在扩展分区里，逻辑分区的元数据被存储在一个链表结构中。如果一个环节丢失，该元数据之后的逻辑分区全部丢失。
3.  MBR 只支持1个字节的分区类型编码，导致许多冲突。
4.  MBR 使用32位的 LBA 值来存储分区扇区信息。LBA 的大小以及512B的扇区大小共同限制了硬盘可寻址大小最大为2[TB](https://en.wikipedia.org/wiki/TiB "wikipedia:TiB"). 如果使用 MBR, 2TB以外的空间无法使用。

[GPT](/index.php/GUID_Partition_Table_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GUID Partition Table (简体中文)")是新一代分区表格式，用以解决 [MBR](/index.php/MBR "MBR") 分区表的缺点

## 启动过程

启动是一个多阶段的过程。今天，大多数 PC 通过一个叫做 [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") (Basic Input/Output System) 的固件初始化系统，它存储在主板的专有芯片中。系统初始化之后，BIOS 会搜寻在第一个识别出的存储设备(机械硬盘，固态硬盘，CD/DVD, USB等等) MBR 的第一个分区的引导器，然后运行它。引导器读取分区表，然后它就能加载操作系统了。常见的 GNU/Linux 引导器包括 [GRUB](/index.php/GRUB "GRUB") 和 [Syslinux](/index.php/Syslinux "Syslinux").

## 备份与还原

因为 MBR 位于硬盘上所以它能被备份以及还原。

备份 MBR:

```
# dd if=/dev/sda of=/path/mbr-backup bs=512 count=1

```

还原 MBR:

```
# dd if=/path/mbr-backup of=/dev/sda bs=512 count=1

```

**警告:** 把 MBR 还原到不相符的分区表会导致数据不可读并且很可能无法恢复。如果你只是想重新安装引导器，见其专属页面[DOS 兼容区](http://www.pixelbeat.org/docs/disk/): [GRUB](/index.php/GRUB "GRUB") 或 [Syslinux](/index.php/Syslinux "Syslinux").

擦除 MBR (可能当你全新安装另一个操作系统时有用) 只需以0填充头446B因为剩余部分是分区表:

```
# dd if=/dev/zero of=/dev/sda bs=446 count=1

```

请参考 [fdisk#Backup and restore](/index.php/Fdisk#Backup_and_restore "Fdisk").

## 恢复 Windows 引导记录

按照习俗 (以及安装方便)，Windows 通常安装在第一个分区上并安装了分区表和到把该分区的第一个扇区引用到引导器。如果你意外安装了像 GRUB 的引导器到 Windows 分区或者以某种方式破坏了引导记录，你会需要一个工具来修复它的。Microsoft 在他们的修复盘，或者安装盘里提供了引导扇区修复工具 `FIXBOOT` 和名为 `FIXMBR` 的 MBR 修复工具。以这种方式，你可以分别修复第一个分区到引导器的引导和第一个分区的 MBR. 做完之后 你需要如原来一样[重新安装 GRUB](/index.php/GRUB#Bootloader_installation "GRUB") 到 MBR (也就是说 GRUB 引导器可以用来链接到 Windows 引导器)。

如果你想恢复使用 Windows, 你可以用 `FIXBOOT` 命令，它能让第一个分区的启动扇区的 MBR 恢复正常，自动加载 Windows 系统。

值得注意的是，有一个名为 `ms-sys` (AUR 里的包 [ms-sys](https://aur.archlinux.org/packages/ms-sys/)) 的 Linux 工具能够安装 MBR. 然而这个工具只能写入新的 MBR (支持所有系统和文件系统) 和引导扇区 (又名引导记录; 这种方法和对 FAT 文件系统用 `FIXBOOT`) 等同。大部分 LiveCD 默认不包含这个工具，所以首先我们要安装它或者你可以找一个含有它的急救 CD，例如 [Parted Magic](http://partedmagic.com/).

首先，再次写入分区信息(分区表):

```
# ms-sys --partition /dev/sda1

```

下一步，写入 Windows 2000/XP/2003 MBR:

```
# ms-sys --mbr /dev/sda  # Read options for different versions

```

然后，写入新的引导扇区 (引导记录):

```
# ms-sys -(1-6)          # Read options to discover the correct FAT record type

```

`ms-sys` 也能写入 Windows 98, ME, Vista, 和 7 的 MBR，见 `ms-sys -h`.

## TestDisk MBRCode

[官方源](/index.php/%E5%AE%98%E6%96%B9%E6%BA%90 "官方源")的 [testdisk](https://www.archlinux.org/packages/?name=testdisk) 能把它自己的 [代码](http://www.cgsecurity.org/wiki/Menu_MBRCode)写入 MBR (它应该能够启动 Windows). 该软件包也包含在安装介质中。

## 另见

*   [What is a Master Boot Record (MBR)?](http://kb.iu.edu/data/aijw.html)