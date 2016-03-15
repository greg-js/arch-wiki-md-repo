**翻译状态：** 本文是英文页面 [GParted](/index.php/GParted "GParted") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-03-01，点击[这里](https://wiki.archlinux.org/index.php?title=GParted&diff=0&oldid=363208)可以查看翻译后英文页面的改动。

[GParted](http://gparted.sourceforge.net/index.php) 是 GNU Parted 的 GTK+ 前端，也是 GNOME 官方指定的分区编辑程序。它可以建立/删除/更改/检查几乎[所有文件格式](http://gparted.sourceforge.net/features.php)的分分区，还可以管理驱动器盘符、参数和复制/粘贴整个分区。GParted 收录于 [extra] 库，还有 [Live CD](http://gparted.sourceforge.net/download.php) 版本。若要调整平常无法卸载的根文件系统所在分区，需要下载 Live CD.

**警告:** GParted 可以读写您的硬盘分区，因此若使用不慎会导致数据丢失。建议您在使用 GParted 之前先备份会受到影响的分区。

## Contents

*   [1 安装到 Arch](#.E5.AE.89.E8.A3.85.E5.88.B0_Arch)
    *   [1.1 可选依赖](#.E5.8F.AF.E9.80.89.E4.BE.9D.E8.B5.96)
        *   [1.1.1 文件系统](#.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
        *   [1.1.2 额外功能](#.E9.A2.9D.E5.A4.96.E5.8A.9F.E8.83.BD)
*   [2 GParted 支持](#GParted_.E6.94.AF.E6.8C.81)
*   [3 小技巧](#.E5.B0.8F.E6.8A.80.E5.B7.A7)
    *   [3.1 把 GParted-live 添加至您的 GRUB 菜单](#.E6.8A.8A_GParted-live_.E6.B7.BB.E5.8A.A0.E8.87.B3.E6.82.A8.E7.9A.84_GRUB_.E8.8F.9C.E5.8D.95)
    *   [3.2 双启动 Windows XP](#.E5.8F.8C.E5.90.AF.E5.8A.A8_Windows_XP)
    *   [3.3 修复混乱的分区顺序](#.E4.BF.AE.E5.A4.8D.E6.B7.B7.E4.B9.B1.E7.9A.84.E5.88.86.E5.8C.BA.E9.A1.BA.E5.BA.8F)
    *   [3.4 从菜单启动 GParted](#.E4.BB.8E.E8.8F.9C.E5.8D.95.E5.90.AF.E5.8A.A8_GParted)
    *   [3.5 启用 GParted 在线调整大小和设备对应器磁盘阵列(dmraid)功能](#.E5.90.AF.E7.94.A8_GParted_.E5.9C.A8.E7.BA.BF.E8.B0.83.E6.95.B4.E5.A4.A7.E5.B0.8F.E5.92.8C.E8.AE.BE.E5.A4.87.E5.AF.B9.E5.BA.94.E5.99.A8.E7.A3.81.E7.9B.98.E9.98.B5.E5.88.97.28dmraid.29.E5.8A.9F.E8.83.BD)

## 安装到 Arch

从[官方源](/index.php/%E5%AE%98%E6%96%B9%E6%BA%90 "官方源")[安装](/index.php/Pacman "Pacman") [gparted](https://www.archlinux.org/packages/?name=gparted) .

### 可选依赖

#### 文件系统

单独的 GParted 软件包本身并不支持所有文件系统。以下列举了为支持不同文件系统所需的软件包:

| **软件包** | **文件系统** |
| [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) | [Btrfs](/index.php/Btrfs "Btrfs") |
| [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) | fat16/32 |
| [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) | ext2/[ext3](/index.php/Ext3 "Ext3")/[ext4](/index.php/Ext4 "Ext4") (v1.41+) |
| [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils) | exfat |
| [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools) | [F2FS](/index.php/F2fs "F2fs") |
| [jfsutils](https://www.archlinux.org/packages/?name=jfsutils) | [JFS](/index.php/JFS "JFS") |
| [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) | [NTFS](/index.php/NTFS "NTFS") |
| [reiser4progs](https://aur.archlinux.org/packages/reiser4progs/) | [Reiser4](/index.php/Reiser4 "Reiser4") |
| [reiserfsprogs](https://www.archlinux.org/packages/?name=reiserfsprogs) | Reiser3 |
| [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs) | [XFS](/index.php/XFS "XFS") |

#### 额外功能

| **软件包** | **功能** |
| [mtools](https://www.archlinux.org/packages/?name=mtools) | 适用于 MSDOS 硬盘。如果您要更改 FAT 分区的盘符，就需要这个。 |

**注意:** 若您通过 pacman 安装 GParted, pacman 也会为您列举这些可选软件包。

## GParted 支持

若您不确定某个指令的作用为何，可以参考[官方 GParted 论坛](http://gparted-forum.surf4.info/)。

## 小技巧

### 把 GParted-live 添加至您的 GRUB 菜单

将 GParted-live 添加至您的 GRUB 菜单的步骤，请参阅 [Gparted-Live](/index.php/Gparted-Live "Gparted-Live") wiki 文章。好处是您可以直接从 GRUB 启动进 GParted-live CD 的 live 环境，不需要另外准备一张 CD！

### 双启动 Windows XP

如果您打算将一个同属于启动分区的 Windows XP 分区移动到另一块硬盘，只要将以下的注册表删除，之后就可以用 GParted 轻易地操作，Windows 不会出现任何问题:

```
HKEY_LOCAL_MACHINE\SYSTEM\MountedDevices

```

相关资料参见[这里](http://gparted-forum.surf4.info/viewtopic.php?pid=8347#p8347)。

### 修复混乱的分区顺序

如果您的硬盘上有逻辑分区，刪除其中一个可能会导致分区顺序混乱。例如以下的范例:

```
/dev/sda1 (主分区)
/dev/sda2 (主分区)
/dev/sda3 (主分区)
/dev/sda4 (**扩展**分区)
/dev/sda5 (逻辑分区)
/dev/sda6 (逻辑分区)
/dev/sda7 (逻辑分区)

```

1-3 是主分区。5-6 是隶属于扩展分区 (4) 的逻辑分区。假设您砍掉 `/dev/sda5`，并将 `/dev/sda2` 复制一份到释出的空间上，那么现在您的硬盘看起来像下面这样:

```
/dev/sda1 (主分区)
/dev/sda2 (主分区)
/dev/sda3 (主分区)
/dev/sda4 (**扩展**分区)
/dev/sda7 (逻辑分区)
/dev/sda5 (逻辑分区)
/dev/sda6 (逻辑分区)

```

注意到在删除、复制/粘贴分区之后，分区顺序混乱了。这可能会导致各种问题：无法顺利挂载分区、出现 GRUB Error 17 "no bootable system"等等。解決这个小问题的方法很简单：

1.  用您的 Arch Live CD、GParted Live CD (或任何其他 live Linux CD) 启动系统
2.  运行 fdisk, 选择硬盘，进入高级模式，修复分区顺序，并将变更写入硬盘

例如使用 `/dev/sda`:

```
# fdisk /dev/sda

```

1.  进入 fdisk 之后，选择 `x` 选项 (额外功能 (仅限进阶用户)) 并按 enter
2.  接着选择 `f` 选项 (修复分区顺序) 并按 enter
3.  接着选择 `w` 选项 (写入分区表之后退出) 并按 enter

**注意:** 您必须以 root 身分执行 **partprobe**，或是重启系统，这样内核才能读取新的分区表！

### 从菜单启动 GParted

如果您从菜单 (例如 xfce 的应用程序菜单) 载入 GParted 时发生任何问题，安装 [polkit](https://www.archlinux.org/packages/?name=polkit) 软件包，并设定为和当前会话同时启动。

### 启用 GParted 在线调整大小和设备对应器磁盘阵列(dmraid)功能

你需要以以下参数重新编译软件包:

./configure --enable-online-resize --enable-libparted-dmraid