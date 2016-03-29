**翻译状态：** 本文是英文页面 [GRUB_Legacy](/index.php/GRUB_Legacy "GRUB Legacy") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-02-28，点击[这里](https://wiki.archlinux.org/index.php?title=GRUB_Legacy&diff=0&oldid=348680)可以查看翻译后英文页面的改动。

[GRUB Legacy](http://www.gnu.org/software/grub/grub-legacy.html) 是一个原本由 [GNU Project](/index.php/GNU_Project "GNU Project") 维护的 [多启动](http://www.gnu.org/software/grub/manual/multiboot/) 引导器，其前身为 GRUB (GRand Unified Bootloader), 最初由 Erich Stefan Boleyn 设计和实现。

简单的说，**启动引导程序**是计算机启动时运行的第一个程序。它可用于选择操作系统分区上的不同内核，也可用于向这些内核传递启动参数。然后内核逐个初始化操作系统的其余部分。

**警告:** 上游已停止维护 GRUB Legacy 并且 Arch 官方也停止支持 (见[这条](https://www.archlinux.org/news/grub-legacy-no-longer-supported/)新闻). 我们推荐用户使用 [GRUB](/index.php/GRUB "GRUB")(2) 或 [Syslinux](/index.php/Syslinux "Syslinux") 来替代。见 [Upgrading to GRUB2](#Upgrading_to_GRUB2).

**注意:** 如果你在你的系统里把 grub-legacy 安装为包 grub-0.97, 那么在软件包升级时会升级为包 [grub](https://www.archlinux.org/packages/?name=grub)-2.xx (GRUB2). 如果你想继续使用 grub-legacy, 从 AUR 安装包 [grub-legacy](https://aur.archlinux.org/packages/grub-legacy/) 以避免冲突。升级过程中只改变了 `/usr/lib/grub/` 里的文件，grub-legacy 安装到 `/boot/grub` 的文件和 `MBR` 并未被移除。 只需重命名 `/boot/grub/menu.lst.pacsave` 为 `/boot/grub/menu.lst` 即可启动进入 grub-legacy.

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 升级到 GRUB2](#.E5.8D.87.E7.BA.A7.E5.88.B0_GRUB2)
    *   [2.1 必须升级吗?](#.E5.BF.85.E9.A1.BB.E5.8D.87.E7.BA.A7.E5.90.97.3F)
    *   [2.2 如何升级](#.E5.A6.82.E4.BD.95.E5.8D.87.E7.BA.A7)
    *   [2.3 区别](#.E5.8C.BA.E5.88.AB)
        *   [2.3.1 备份重要数据](#.E5.A4.87.E4.BB.BD.E9.87.8D.E8.A6.81.E6.95.B0.E6.8D.AE)
    *   [2.4 把 GRUB Legacy 的配置文件转换为新格式](#.E6.8A.8A_GRUB_Legacy_.E7.9A.84.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6.E8.BD.AC.E6.8D.A2.E4.B8.BA.E6.96.B0.E6.A0.BC.E5.BC.8F)
    *   [2.5 恢复 GRUB Legacy](#.E6.81.A2.E5.A4.8D_GRUB_Legacy)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 寻找 GRUB 的根分区](#.E5.AF.BB.E6.89.BE_GRUB_.E7.9A.84.E6.A0.B9.E5.88.86.E5.8C.BA)
    *   [3.2 双启动到 Windows](#.E5.8F.8C.E5.90.AF.E5.8A.A8.E5.88.B0_Windows)
    *   [3.3 双启动到 GNU/Linux](#.E5.8F.8C.E5.90.AF.E5.8A.A8.E5.88.B0_GNU.2FLinux)
    *   [3.4 chainloader 和 configfile](#chainloader_.E5.92.8C_configfile)
    *   [3.5 双启动 GNU/Linux (GRUB2)](#.E5.8F.8C.E5.90.AF.E5.8A.A8_GNU.2FLinux_.28GRUB2.29)
*   [4 安装启动器](#.E5.AE.89.E8.A3.85.E5.90.AF.E5.8A.A8.E5.99.A8)
    *   [4.1 手动恢复 GRUB 库](#.E6.89.8B.E5.8A.A8.E6.81.A2.E5.A4.8D_GRUB_.E5.BA.93)
    *   [4.2 安装 GRUB 的常识](#.E5.AE.89.E8.A3.85_GRUB_.E7.9A.84.E5.B8.B8.E8.AF.86)
    *   [4.3 安装到 MBR](#.E5.AE.89.E8.A3.85.E5.88.B0_MBR)
    *   [4.4 安装到分区](#.E5.AE.89.E8.A3.85.E5.88.B0.E5.88.86.E5.8C.BA)
    *   [4.5 备选方案 (grub-install)](#.E5.A4.87.E9.80.89.E6.96.B9.E6.A1.88_.28grub-install.29)
*   [5 小技巧](#.E5.B0.8F.E6.8A.80.E5.B7.A7)
    *   [5.1 图形化启动](#.E5.9B.BE.E5.BD.A2.E5.8C.96.E5.90.AF.E5.8A.A8)
    *   [5.2 Framebuffer 分辨率](#Framebuffer_.E5.88.86.E8.BE.A8.E7.8E.87)
        *   [5.2.1 GRUB 可识别的值](#GRUB_.E5.8F.AF.E8.AF.86.E5.88.AB.E7.9A.84.E5.80.BC)
        *   [5.2.2 hwinfo](#hwinfo)
        *   [5.2.3 vbetest](#vbetest)
    *   [5.3 给分区命名](#.E7.BB.99.E5.88.86.E5.8C.BA.E5.91.BD.E5.90.8D)
        *   [5.3.1 按盘符](#.E6.8C.89.E7.9B.98.E7.AC.A6)
        *   [5.3.2 按 UUID](#.E6.8C.89_UUID)
    *   [5.4 以 root 身份启动 (单用户模式)](#.E4.BB.A5_root_.E8.BA.AB.E4.BB.BD.E5.90.AF.E5.8A.A8_.28.E5.8D.95.E7.94.A8.E6.88.B7.E6.A8.A1.E5.BC.8F.29)
    *   [5.5 密码保护](#.E5.AF.86.E7.A0.81.E4.BF.9D.E6.8A.A4)
    *   [5.6 启动命名过的引导选项](#.E5.90.AF.E5.8A.A8.E5.91.BD.E5.90.8D.E8.BF.87.E7.9A.84.E5.BC.95.E5.AF.BC.E9.80.89.E9.A1.B9)
    *   [5.7 LILO 和 GRUB 相互配合](#LILO_.E5.92.8C_GRUB_.E7.9B.B8.E4.BA.92.E9.85.8D.E5.90.88)
    *   [5.8 GRUB 启动盘](#GRUB_.E5.90.AF.E5.8A.A8.E7.9B.98)
    *   [5.9 隐藏 GRUB 菜单](#.E9.9A.90.E8.97.8F_GRUB_.E8.8F.9C.E5.8D.95)
*   [6 进一步排除 bug](#.E8.BF.9B.E4.B8.80.E6.AD.A5.E6.8E.92.E9.99.A4_bug)
*   [7 疑难问题](#.E7.96.91.E9.9A.BE.E9.97.AE.E9.A2.98)
    *   [7.1 GRUB Error 17](#GRUB_Error_17)
    *   [7.2 /boot/grub/stage1 not read correctly](#.2Fboot.2Fgrub.2Fstage1_not_read_correctly)
    *   [7.3 意外安装到了 Windows 分区](#.E6.84.8F.E5.A4.96.E5.AE.89.E8.A3.85.E5.88.B0.E4.BA.86_Windows_.E5.88.86.E5.8C.BA)
    *   [7.4 在引导菜单中编辑 GRUB 条目](#.E5.9C.A8.E5.BC.95.E5.AF.BC.E8.8F.9C.E5.8D.95.E4.B8.AD.E7.BC.96.E8.BE.91_GRUB_.E6.9D.A1.E7.9B.AE)
    *   [7.5 device.map error](#device.map_error)
    *   [7.6 KDE 重启后下拉菜单失效](#KDE_.E9.87.8D.E5.90.AF.E5.90.8E.E4.B8.8B.E6.8B.89.E8.8F.9C.E5.8D.95.E5.A4.B1.E6.95.88)
    *   [7.7 GRUB 无法找到或安装到 virtio */dev/vd** 或其他非 BIOS 设备](#GRUB_.E6.97.A0.E6.B3.95.E6.89.BE.E5.88.B0.E6.88.96.E5.AE.89.E8.A3.85.E5.88.B0_virtio_.2Fdev.2Fvd.2A_.E6.88.96.E5.85.B6.E4.BB.96.E9.9D.9E_BIOS_.E8.AE.BE.E5.A4.87)
*   [8 另见](#.E5.8F.A6.E8.A7.81)

## 安装

GRUB Legacy 已从[官方源](/index.php/%E5%AE%98%E6%96%B9%E6%BA%90 "官方源")移除以支持 [GRUB version 2.x](/index.php/GRUB "GRUB"). [AUR](/index.php/AUR "AUR") 的 [grub-legacy](https://aur.archlinux.org/packages/grub-legacy/) 依然可用。

另外，若想 GRUB 以引导器工作它必须被安装到设备或分区的引导扇区。这在 [Bootloader installation](#Bootloader_installation) 部分有所提及。

## 升级到 GRUB2

### 必须升级吗?

不是必须的。老 GRUB 不会从系统删除，照旧工作。

然而，和其它不被支持的软件包一样，后续的 bug 将无人修复。所以建议所有的用户抽时间升级到 [GRUB version 2.x](/index.php/GRUB "GRUB"), 或其它支持的 [Boot Loader](/index.php/Boot_Loader "Boot Loader").

GRUB legacy 不支持 [GPT](/index.php/GPT "GPT") 硬盘，[Btrfs](/index.php/Btrfs "Btrfs") 文件系统和 [UEFI](/index.php/UEFI "UEFI") 固件。

### 如何升级

升级 GRUB Legacy 到 [GRUB version 2.x](/index.php/GRUB "GRUB") 和在已有 Arch Linux 上安装 GRUB 一样。详细教程见[这里](/index.php/GRUB#Installation "GRUB")。

### 区别

*   GRUB Legacy 和 GRUB 的命令之间有许多区别。执行命令之前请学习 [GRUB commands](https://www.gnu.org/software/grub/manual/grub.html#Commands) (例如 "find" 被替换为 "search").
*   GRUB 现在是*模块化*的并再也不需要 "stage 1.5". 因此，引导器本身受到限制 -- 若想扩展功能必须加载模块 (例如为了添加 [LVM](/index.php/LVM "LVM") 或 RAID 支持).
*   GRUB Legacy 和 GRUB 显示的设备名不同。分区从 1 而不是 0 开始计数，但驱动器依然从 0 开始，并添加了分区表前缀。例如，`/dev/sda1` 会显示为 `(hd0,msdos1)` (对于 MBR) 或 `(hd0,gpt1)` (对于 GPT).
*   GRUB 显著比 GRUB legacy 大 (占用 `/boot` ~13 MB ). 如果你从单独的 `/boot` 分区启动并且它小于 32 MB, 你就会碰到硬盘空间问题，pacman 不会安装新的内核。

#### 备份重要数据

尽管 GRUB 会平滑地完成安装，我们依然强烈建议在升级到 GRUB v2 之前备份 GRUB Legacy 的文件。

```
# mv /boot/grub /boot/grub-legacy

```

备份含有引导代码和分区表的 MBR (把 `/dev/sd*X*` 替换为你的真实路径):

```
# dd if=/dev/sd*X* of=/path/to/backup/mbr_backup bs=512 count=1

```

MBR 只有 446B 包含引导代码，接下来的 64B 包含分区表。如果你不想在恢复时覆盖分区表，我们强烈建议只备份 MBR 引导代码:

```
# dd if=/dev/sd*X* of=/path/to/backup/bootcode_backup bs=446 count=1

```

如果无法正常安装 GRUB2 , 见[恢复 GRUB Legacy](#.E6.81.A2.E5.A4.8D_GRUB_Legacy).

### 把 GRUB Legacy 的配置文件转换为新格式

如果 `grub-mkconfig` 失败，如下转换你的 `/boot/grub/menu.lst` 为 `/boot/grub/grub.cfg`:

```
# grub-menulst2cfg /boot/grub/menu.lst /boot/grub/grub.cfg

```

**注意:** 该选项仅在 BIOS 系统有效，UEFI 系统则不。

例如:

 `/boot/grub/menu.lst` 
```
default=0
timeout=5

title  Arch Linux Stock Kernel
root   (hd0,0)
kernel /vmlinuz-linux root=/dev/sda2 ro
initrd /initramfs-linux.img

title  Arch Linux Stock Kernel Fallback
root   (hd0,0)
kernel /vmlinuz-linux root=/dev/sda2 ro
initrd /initramfs-linux-fallback.img

```
 `/boot/grub/grub.cfg` 
```
set default='0'; if [ x"$default" = xsaved ]; then load_env; set default="$saved_entry"; fi
set timeout=5

menuentry 'Arch Linux Stock Kernel' {
  set root='(hd0,1)'; set legacy_hdbias='0'
  legacy_kernel   '/vmlinuz-linux' '/vmlinuz-linux' 'root=/dev/sda2' 'ro'
  legacy_initrd '/initramfs-linux.img' '/initramfs-linux.img'
}

menuentry 'Arch Linux Stock Kernel Fallback' {
  set root='(hd0,1)'; set legacy_hdbias='0'
  legacy_kernel   '/vmlinuz-linux' '/vmlinuz-linux' 'root=/dev/sda2' 'ro'
  legacy_initrd '/initramfs-linux-fallback.img' '/initramfs-linux-fallback.img'
}

```

如果你忘了创建 GRUB `/boot/grub/grub.cfg` 配置文件然后启动进了 GRUB Command Shell, 输入:

```
sh:grub> insmod legacycfg
sh:grub> legacy_configfile ${prefix}/menu.lst

```

启动进 Arch 重新创建 GRUB `/boot/grub/grub.cfg` 配置文件。

### 恢复 GRUB Legacy

*   移除 GRUB v2 的文件:

```
# mv /boot/grub /boot/grub.nonfunctional

```

*   复制 GRUB Legacy 到 `/boot`:

```
# cp -af /boot/grub-legacy /boot/grub

```

*   从备份恢复 sda 的 MBR 以及接下来的 62 扇区

**警告:** 该命令也恢复了分区表，所以以旧版覆盖修改过的分区表时请小心，它**将会**导致系统混乱。

```
# dd if=/path/to/backup/first-sectors of=/dev/sdX bs=512 count=1

```

以下是一个更安全的，只恢复 MBR 引导代码的方法:

```
# dd if=/path/to/backup/mbr-boot-code of=/dev/sdX bs=446 count=1

```

## 配置

配置文件位于 `/boot/grub/menu.lst`。按照你的要求编辑这个文件。

*   `timeout #` -- 默认操作系统被自动加载前的等待时间(单位是秒)。
*   `default #` -- 超时时默认的启动项。

一个范例配置文件(`/boot` 位于独立分区中):

```
/boot/grub/menu.lst

```

```
# Config file for GRUB - The GNU GRand Unified Bootloader
# /boot/grub/menu.lst

# DEVICE NAME CONVERSIONS
#
#  Linux           GRUB
# -------------------------
#  /dev/fd0        (fd0)
#  /dev/sda        (hd0)
#  /dev/sdb2       (hd1,1)
#  /dev/sda3       (hd0,2)
#

#  FRAMEBUFFER RESOLUTION SETTINGS
#     +-------------------------------------------------+
#          | 640x480    800x600    1024x768   1280x1024
#      ----+--------------------------------------------
#      256 | 0x301=769  0x303=771  0x305=773   0x307=775
#      32K | 0x310=784  0x313=787  0x316=790   0x319=793
#      64K | 0x311=785  0x314=788  0x317=791   0x31A=794
#      16M | 0x312=786  0x315=789  0x318=792   0x31B=795
#     +-------------------------------------------------+
#  for more details and different resolutions see
#  https://wiki.archlinux.org/index.php/GRUB#Framebuffer_Resolution

# general configuration:
timeout   5
default   0
color light-blue/black light-cyan/blue

# boot sections follow
# each is implicitly numbered from 0 in the order of appearance below
#
# TIP: If you want a 1024x768 framebuffer, add "vga=773" to your kernel line.
#
#-*

# (0) Arch Linux
title  Arch Linux
root   (hd0,0)
kernel /vmlinuz-linux root=/dev/sda3 ro
initrd /initramfs-linux.img

# (1) Windows
#title Windows
#rootnoverify (hd0,0)
#makeactive
#chainloader +1

```

### 寻找 GRUB 的根分区

GRUB 必须被告知它的文件位于文件系统的位置。因为可能有多个系统存在 (也就是在多启动环境中)。 GRUB 文件总是位于`/boot`，它有可能在一个独立的分区中。

**注意:** GRUB 定义的存储设备的方式与传统的内核命名方式不同。

*   硬盘定义为 **(hdX)**；这也可以用来指定任何 USB 存储设备。
*   设备和分区的编号从0开始。例如，BIOS 识别出的第一个硬盘被定为 **(hd0)**。第二个设备被叫做 **(hd1)**。这也应用到分区。因此第一个硬盘上的第二个分区叫做 **(hd0,1)**.

如果你不知道 `/boot` 的位置，使用 GRUB shell `find` 命令来定位 GRUB 文件。以 root 身份进入 GRUB shell:

```
# grub

```

下面的例子适用于*没有*独立 `/boot` 分区的系统。此时 `/boot` 只是 `/` 下的一个目录:

```
grub> find /boot/grub/stage1

```

下面的例子适用于*有*独立的 `/boot` 分区的系统:

```
grub> find /grub/stage1

```

GRUB 会找到这个文件，然后输出 `stage1` 文件的位置。例如:

 `grub> find /grub/stage1`  ` (hd0,0)` 

这个返回值需要输入到配置文件的 `root` 行。输入 `quit` 退出这个 shell.

### 双启动到 Windows

添加以下内容到你的 `/boot/grub/menu.lst` 末尾 (假设你的 Windows 分区是第一个设备的第一个分区):

 `/boot/grub/menu.lst` 
```
 title Windows
 rootnoverify (hd0,0)
 makeactive
 chainloader +1

```

**注意:**

*   如果你尝试双启动到 Windows 7，你需要注释掉 `makeactive` 行。
*   Windows 2000 和之后的版本**不需要**在第一个分区就可以启动(与通常认为的不同)。如果 Windows 分区改变了 (也就是说，如果你在 Windows 分区的前面添加了一个分区)，你需要编辑 Windows 的 `boot.ini` 文件来应对改变。(参见[本文](http://vlaurie.com/computers2/Articles/bootini.htm)获取更多细节。

如果 Windows 位于另一块硬盘，需要使用 map 命令。这会欺骗你的 Windows 安装程序，让它以为自己在主硬盘上。假设你的 Windows 分区是在第二块硬盘上的第一个分区:

 `/boot/grub/menu.lst` 
```
 title Windows
 map (hd0) (hd1)
 map (hd1) (hd0)
 rootnoverify (hd1,0)
 makeactive
 chainloader +1

```

**注意:** 如果你尝试双启动到 Windows 7，你需要注释掉 `makeactive` 行。

### 双启动到 GNU/Linux

和Arch linux的加载方式一样。例如:

 `/boot/grub/menu.lst` 
```
 title Other Linux
 root (hd0,2)
 kernel /path/to/kernel root=/dev/sda3 ro
 initrd /path/to/initrd

```

**注意:** 也许需要额外的选项，同时也可能不需要使用初始化内存盘。检查一下另一个发行版的 `/boot/grub/menu.lst` 来得到启动选项，或者参考 [#chainloader 和 configfile](#chainloader_.E5.92.8C_configfile) (推荐)。

### chainloader 和 configfile

为了方便系统维护，应该使用 `chainloader` 和 `configfile` 命令以启动提供了”自动化“引导机制的其他 Linux 操作系统(例如： Debian, Ubuntu, openSUSE),这样就允许每个发行版自行维护各自的 `menu.lst` 启动选项。

*   `chainloader`命令能装载其他的启动引导器（而不是内核镜像)； 当其他的启动引导器安装在一个分区的启动扇区(例如：GRUB)时就有用了. 这样就可以实现在 [MBR](/index.php/MBR "MBR") 安装一个“主”GRUB 和在每个分区的引导记录区 (PBR) 安装一些分散的 GRUB.

*   {ic|configfile}}命令能指导 GRUB 装载确切的配置文件. 这样就可以引导其他的操作系统的 `menu.lst` 而不需要在引导的操作系统上安装 GRUB. 这种方法一大缺陷就是其他操作系统的 `menu.lst` 可能和安装的 GRUB 版本不兼容; 许多版本的操作系统高度依赖于 GRUB 的版本。

例如, GRUB 即将安装在 [MBR](/index.php/MBR "MBR") (主引导记录区)上，但是其他的启动引导器(可能是 GRUB 或者 LILO)已经安装到了 `(hd0,2)` 启动扇区。

```
---------------------------------------------
|   |           |           |   %           |
| M |           |           | B %           |
| B |  (hd0,0)  |  (hd0,1)  | L %  (hd0,2)  |
| R |           |           |   %           |
|   |           |           |   %           |
---------------------------------------------
  |                           ^
  |       chainloading        |
  -----------------------------

```

你可以在 `menu.lst` 下添加:

```
title Other Linux
root (hd0,2)
chainloader +1

```

或者，当 `(hd0,2)` 上的启动引导器是 GRUB 时:

```
title Other Linux
root (hd0,2)
configfile /boot/grub/menu.lst

```

`chainloader` 命令也可以用来装载第二个驱动器的 MBR:

```
title Other drive
rootnoverify (hd1)
chainloader +1

```

### 双启动 GNU/Linux (GRUB2)

如果其他 Linux 发行版用 GRUB2 (如：Ubuntu 9.10或者更高版本)，而且你在它的/分区安装了启动装载程序, 你可以添加如下条目到你的 `/boot/grub/menu.lst`:

 `/boot/grub/menu.lst` 
```
 # other Linux using GRUB2
 title Ubuntu
 root (hd0,2)
 kernel /boot/grub/core.img

```

在启动时选择这个条目就可以引导其他发行版的 GRUB2 菜单 (假设安装在 `/dev/sda3`)。

## 安装启动器

### 手动恢复 GRUB 库

`*stage*` 文件在 `/boot/grub` 目录下, 但是在如下情况下没有：启动装载程序在系统安装时没有安装或者/分区的文件系统损坏，意外删除等。

使用如下的命令手动复制 GRUB 的库文件:

```
# cp -a /usr/lib/grub/i386-pc/* /boot/grub

```

{{注意|如果单独分区的话，不要忘记挂载系统的 {{ic|/boot} 分区!(上文假设 `/boot} 分区既可以挂载在根分区也可以挂载在根分区的/boot目录下!)`

### 安装 GRUB 的常识

GRUB 有可以一个单独的介质安装(例如:一张 LiveCD),或者直接从运行着的 Arch 中安装。GRUB 启动引导器*很少*需要重新安装，当遇到如下情况时*不*需要安装:

*   更新了配置文件。
*   升级了软件包 [grub-legacy](https://aur.archlinux.org/packages/grub-legacy/).

遇到如下请况时*需要*安装:

*   引导器还没有安装。
*   其他的操作系统覆盖了 Linux 的引导器。
*   引导器因为一些未知的原因未能成功引导系统。

在重装或安装之前，请注意以下几点:

*   在进行操作之前确保你的GRUB配置文件是正确的 (`/boot/grub/menu.lst`)。请参考[#寻找 GRUB 的根分区](#.E5.AF.BB.E6.89.BE_GRUB_.E7.9A.84.E6.A0.B9.E5.88.86.E5.8C.BA)以确认你的设备被正确的定义。
*   GRUB 必须安装在 [MBR](/index.php/MBR "MBR") (硬盘的第一扇区)，或者在能被大多数 BIOS 识别的第一个存储设备的第一个分区。为了满足个人的多系统引导需求，GRUB 的多重设置就起作用了，请参考[#chainloader 和 configfile](#chainloader_.E5.92.8C_configfile).
*   在安装 GRUB 启动引导器时可能需要在 `chroot` 过的环境下完成 (例如：通过安装光盘 chroot 安装的系统)，比如你编辑RAID的配置文件或者你忘记安装或者破坏了你的 GRUB, 你都需要通过一张 LiveCD 或者其他的 Linux 操作系统 [Change root](/index.php/Change_root "Change root") (即更改root目录).

首先，进入 GRUB shell:

```
# grub

```

使用 `root` 命令配合 `find` 的输出 (见 [#寻找 GRUB 的根分区](#.E5.AF.BB.E6.89.BE_GRUB_.E7.9A.84.E6.A0.B9.E5.88.86.E5.8C.BA))，以告诉 GRUB 哪个分区包含了 stage1 (同理还有 `/boot`):

```
grub> root (hd1,0)

```

**提示:** GRUB Shell 支持 Tab 补全，如果你键入'root (hd'然后连续敲击 `Tab` 两次你就可以看见可用的存储分区设备，在分区下也适用，Tab 补全在 GRUB 引导菜单上也适用，如果你的配置文件有错误你可以在引导菜单里编辑并使用 Tab 补全来协助寻找驱动器和分区。请参考[#Edit GRUB entries in the boot menu](#Edit_GRUB_entries_in_the_boot_menu).

### 安装到 MBR

下面的例子中把 GRUB 安装到第一个驱动器的 [MBR](/index.php/MBR "MBR"):

```
grub> setup (hd0)

```

### 安装到分区

下面的例子中把 GRUB 安装到第一个驱动器的第一个分区:

```
grub> setup (hd0,0)

```

在运行 `setup` 完成之后, 键入 `quit` 退出 shell. 如果你chroot 过，[退出 chroot 并卸载分区](/index.php/Change_root "Change root")。现在重启测试一下。

### 备选方案 (grub-install)

**注意:** 这个方法不怎么可靠，推荐使用 GRUB shell.

使用 `grub-install` +你安装启动装载程序的分区。例如将 GRUB 安装到第一个驱动器的 MBR:

```
# grub-install /dev/sda

```

GRUB 会提示它是否安装成功. 如果没有安装成功，你得用 GRUB Shell.

## 小技巧

额外的配置笔记。

### 图形化启动

对于那些渴望看见图形界面的人, 参阅 [grub-gfx](/index.php/Grub-gfx "Grub-gfx"). [GRUB2](/index.php/GRUB2 "GRUB2") 也提供增强的图形化功能，例如背景图片和点阵字体。

### Framebuffer 分辨率

我们可以用 `menu.lst` 里给出的分辨率，但也许你想使用 LCD 宽屏的最大原生分辨率。如下操作:

在 [Wikipedia](https://en.wikipedia.org/wiki/VESA_BIOS_Extensions#Linux_video_mode_numbers "wikipedia:VESA BIOS Extensions")上，列出了 framebuffer 分辨率 (即排除了 VBE 标准中的). 但是，比如我想用 1440x900 (`vga=867`) 却用不了。这是因为显卡制造商可以随便设置并非 VBE 3 标准的数字，这就导致了卡与卡之间编码不同 (就算是同一个制造商)。

所以除了使用表格以外，你可以使用如下方法得到正确的编码:

#### GRUB 可识别的值

只使用 GRUB 的话有一个简单的方法来获得正确的编码。

在 kernel 行，让内核询问该使用什么模式。

```
kernel /vmlinuz-linux root=/dev/sda1 ro **vga=ask**

```

重启。GRUB 现在会展示一系列可用的编码以及一个扫描更多的选项。

你可以选择你想要的编码 (别把它忘了，下一步还要用) 并在启动时使用。

在 kernel 行把 `ask` 替换为你选择的正确编码。

例如，`[369] 1680x1050x32` 的 kernel 行看起来如下:

```
kernel /vmlinuz-linux root=/dev/sda1 ro **vga=0x369**

```

#### hwinfo

1.  从官方源安装 [hwinfo](https://www.archlinux.org/packages/?name=hwinfo).
2.  以 root 身份运行 `hwinfo --framebuffer`.
3.  选择代表了你想要的分辨率的编码。
4.  在该6位数字编码前加上 0x 前缀，并把它加入到 `menu.lst` kernel 行的 `vga=` 选项后。或是转换为十进制以避免使用 0x 前缀。

**hwinfo** 输出样例:

```
Mode 0x0364: 1440x900 (+1440), 8 bits
Mode 0x0365: 1440x900 (+5760), 24 bits

```

以及 kernel 行:

```
kernel /vmlinuz-linux root=/dev/sda1 ro **vga=0x0365**

```

**注意:** *vbetest* 所给出的 VESA 模式我们要加上512才能在 kernel 选项里使用。*hwinfo* 直接给出了选项需要的值。

#### vbetest

1.  从 [AUR](/index.php/AUR "AUR") 安装软件包 [lrmi](https://aur.archlinux.org/packages/lrmi/), 它包含 **vbetest** 工具 (x86_64 用户需要使用 [hwinfo](#hwinfo)).
2.  以 root 身份运行 `vbetest`.
3.  代表分辨率的数字是以 [ ] 注释起来的。
4.  按 `q` 以退出 **vbetest** 互动提示符。
    1.  作为一个选项，在 root 身份的终端中，你可以运行 `vbetest -m <yourcode>` 来测试你选中的模式，然后会看见像[这样](http://www.phoronix.net/image.php?id=803&image=x_vbespy_5)的图案。
5.  给你找到的值加上 **512** ，并在 `menu.lst` 里设置给内核参数 `vga=`.
6.  重启并欣赏。

**vbetest** 输出样例:

```
[356] 1440x900 (256 color palette)
[357] 1440x900 (8:8:8)

```

你要的数字就是 357\. 然后，357 + 512 = 869, 所以你要设置 **vga=869**. 如下把它添加到 `menu.lst` 的 kernel 行:

```
kernel /vmlinuz-linux root=/dev/sda1 ro **vga=869**

```

**注意:**

*   (8:8:8) 是24位彩色 (24bit 就是 32bit)
*   (5:6:5) 是16位彩色
*   (5:5:5) 是15位彩色

### 给分区命名

#### 按盘符

如果你偶尔会调整 (或准备去调整) 分区大小你可以考虑按盘符给你的分区/驱动器命名。如下命名 ext2, ext3, ext4 分区:

```
e2label */dev/drive|partition* label

```

名字可以长达16个字符但不能有空格。在你的 `menu.lst` 里设置:

```
kernel /boot/vmlinuz-linux root=/dev/disk/by-label/Arch_Linux ro

```

#### 按 UUID

可使用 `blkid` 或 `ls -l /dev/disk/by-uuid` 来获取分区的 [UUID](/index.php/UUID "UUID") (Universally Unique IDentifier, 通用唯一标识符). 在 `menu.lst` 里如下设置:

```
kernel /boot/vmlinuz-linux root=/dev/disk/by-uuid/*uuid_number*

```

或:

```
kernel /boot/vmlinuz-linux root=UUID=*uuid_number*

```

都可。

### 以 root 身份启动 (单用户模式)

在引导器界面，选择一个条目并编辑 (按 `e`). 加上如下内核参数:

```
[...] single init=/bin/bash

```

然后会以单用户模式 (init 1) 启动，即没有输入密码前会停止在 root 提示。 这对设置 root 密码等恢复操作有用。 然而，如果你没有为 GRUB 设置[#密码保护](#.E5.AF.86.E7.A0.81.E4.BF.9D.E6.8A.A4)的话这是一个巨大的安全漏洞。

### 密码保护

你可以在 GRUB 配置文件里为你想要保护的操作系统设置密码保护。如果 BIOS 没有此类功能而你又需要额外安保措施的话你可能需要引导器密码保护。

首先选择一个你记得住的密码并加密:

 `# grub-md5-crypt` 
```
 Password:
 Retype password:
 $1$ZOGor$GABXUQ/hnzns/d5JYqqjw

```

然后把它加到 GRUB 配置文件 `/boot/grub/menu.lst` 的开头 (必须加到开头以便 GRUB 识别):

```
# general configuration
timeout   5
default   0
color light-blue/black light-cyan/blue

password --md5 $1$ZOGor$GABXUQ/hnzns/d5JYqqjw

```

**注意:** GRUB 使用 QWERTY 键盘布局输入。

然后为每个你要保护的操作系统加上 `lock` 命令:

```
# (0) Arch Linux
title  Arch Linux
lock
root   (hd0,1)
kernel /boot/vmlinuz-linux root=/dev/disk/by-label/Arch_Linux ro
initrd /boot/initramfs-linux.img

```

**警告:** 如果你在 BIOS 禁用了从其他设备启动 (比如 CD 驱动器) 那么密码保护会保护你所有的操作系统，并且如果密码忘掉的话很难重新进入系统了。

在主板设置跳线来重置 BIOS 永远都是可能的 (参见你主板的手册，每个型号都有所不同). 所以别人能够操作硬件的情况下基本上没法阻止他们突破启动密码。

### 启动命名过的引导选项

如果你意识到你经常需要切换到其他一些非默认的操作系统 (如 Windows) 中并需要重新启动，等待GRUB菜单出现是乏味的。 GRUB 提供了一种方法在重新启动时不用等待菜单，而是使用时指定一个临时的新的的默认选项，该选项用于记录您的操作系统选择。

假设 `menu.lst` 配置如下:

```
/boot/grub/menu.lst

```

```
# general configuration:
timeout 10
default 0
color light-blue/black light-cyan/blue

# (0) Arch
title  Arch Linux
root (hd0,1)
kernel /boot/vmlinuz-linux root=/dev/disk/by-label/ARCH ro
initrd /boot/initramfs-linux.img

# (1) Windows
title Windows XP
rootnoverify (hd0,0)
makeactive
chainloader +1

```

Arch 是 default (0). 现在我们要重启进入 Windows. 改变 `default 0` 为 `default saved` -- 不管 **savedefault** 命令有没有使用，这将把当前的默认选项记录到 GRUB目录下的 `default` 文件。把 `savedefault 0` 添加到 Windows 条目的底部。每当 Windows 启动时，将会重置默认为 Arch, 如此来临时指定默认为 Windows.

现在我们需要的是一种能轻松改变默认的方式。可通过命令 `grub-set-default` 完成。因此为启动进入 Windows, 输入如下命令:

```
# grub-set-default 1 && sudo shutdown -r now

```

易用起见，你可能希望实现 "[Allow users to shutdown](/index.php/Allow_users_to_shutdown "Allow users to shutdown") 补丁" (包括`/sbin/grub-set-default` 中不需要密码来执行的命令).

### LILO 和 GRUB 相互配合

如果 [LILO](/index.php/LILO "LILO") 软件包已经安装，删除它:

```
# pacman -R lilo

```

由于有些任务 (例如使用 `make all` 编译内核) 会调用 LILO, 并且 LILO 会覆盖安装 GRUB. LILO 可能已包含于你的基本系统中，这取决于你的安装介质版本以及你在软件安装阶段是否选择了它。

**注意:** 如果被安装到 MBR 的话，`pacman -R lilo` 不会把 LILO 从 MBR 移除而仅仅删除 [lilo](https://aur.archlinux.org/packages/lilo/) 软件包。安装到 MBR 的 LILO 引导器会当 GRUB (或其他引导器) 安装在 MBR 上时被覆盖。

### GRUB 启动盘

首先，你需要格式化一张软盘:

```
# fdformat /dev/fd0
# mke2fs /dev/fd0

```

然后挂载它:

```
# mount -t ext2 /dev/fd0 /mnt/fl

```

在上面安装 GRUB:

```
# grub-install --root-directory=/mnt/fl '(fd0)'

```

复制你的 `menu.lst` 文件到磁盘上:

```
# cp /boot/grub/menu.lst /mnt/fl/boot/grub/menu.lst

```

现在卸载你的软盘:

```
# umount /mnt/fl

```

这样就完成了！现在你可以用这张磁盘重启你的计算机，它应该会用GRUB启动。当然还需先确认在你的BIOS里启动顺序中已经将软盘设为比硬盘更高优先级。

另见: [Super GRUB Disk](http://www.supergrubdisk.org/).

### 隐藏 GRUB 菜单

`hiddenmenu` 选项能默认隐藏菜单. 这样在启动时没有菜单显示但默认的选项会在启动延时后自动选择.你仍然可以按 `Esc` 让菜单显示出来. 要用这个选项， 只要在 `/boot/grub/menu.lst`文件中添加:

```
hiddenmenu

```

## 进一步排除 bug

见 [article](/index.php/Boot_debugging "Boot debugging").

## 疑难问题

### GRUB Error 17

**注意:** 以下解决方案对 GRUB Error 15 也有效。

**第一步是拔下所有外部设备，看起来显而易见但是经常被忽略 ;)**

如果你的分区表混乱了，下一次开机时就只会看到"GRUB error 17". 有许多导致分区表混乱的原因。通常是使用 [GParted](/index.php/GParted "GParted") 操作硬盘 -- 特别是对逻辑分区 -- 造成分区顺序改变。例如，你删除了 `/dev/sda6` 并调整 `/dev/sda7` 的大小，最后在原 `/dev/sda6` 处创建分区，它会显示到列表底部，比如 `/dev/sda9`. 尽管物理上它们的顺序没有改变，它们被识别的顺序改变了。

修复分区表很简单。从你的 Arch CD/DVD/USB, 启动，以 root 身份登录，运行:

```
# fdisk /dev/sda

```

进入硬盘， e[x]tra/expert 模式，[f]ix 分区顺序，然后 [w]rite 分区表并退出。

你可通过 `fdisk -l` 来检查确实已经修复好了。现在只需修复 GRUB. 见[引导器的安装](#Bootloader_installation)部分。

基本上只要告诉 GRUB 正确的 `/boot` 然后重新写入 GRUB 到硬盘上的 [MBR](/index.php/MBR "MBR").

例如:

```
# grub

```

```
grub> root (hd0,6)
grub> setup (hd0)
grub> quit

```

更深入的总结见[这个页面](http://stringofthoughts.wordpress.com/2009/05/24/grub-error-17-debianubuntu)。

### /boot/grub/stage1 not read correctly

如果在设置 GRUB 时碰到这个问题并且分区表不是很干净时，值得一查。

```
# fdisk -l /dev/sda

```

将会显示 `/dev/sda` 的分区表。在此检验你的分区的"Id"值是否正确。 "System"栏目会给出"Id"值的解释。

比如你的启动分区被标记为"HPFS/NTFS", 你得把它改成"Linux". 为此，转到 fdisk,

```
# fdisk /dev/sda

```

用 `t` 改变分区的系统 id, 选择新的分区类型和 id (Linux = 83). 也可用 `L` 列出所有的系统 id.

如果你改变了分区系统 id, 你需要 [v]erify 分区表然后 [w]rite.

现在尝试重新设置 GRUB.

[这里](https://bbs.archlinux.org/viewtopic.php?pid=799930)是报告该问题的论坛帖子。

### 意外安装到了 Windows 分区

如果你意外地把 GRUB 安装到了 Windows 分区，GRUB 会覆盖该分区的引导扇区并擦除到 Windows 引导器的引用。 (NTLDR 及更早的确证有此类问题，更新的版本不确定).

你要使用 Windows Recovery Console 来修复此问题。由于许多制造商在他们的产品里不包含这个 (更多的是使用恢复分区), Microsoft 开放了下载。如果你使用 XP, 参见 [这个页面](http://tips.vlaurie.com/2006/05/recovery-console-for-those-without-an-xp-disk/)来把软盘做成 Recovery CD. 启动 Recovery CD (或启用 Windows 恢复模式) 并运行 `fixboot` 来修复引导扇区。之后你需要重新安装 GRUB --- 这次安装到 MBR, 不是 Windows 分区---来引导 Linux.

更深入的讨论见[这里](/index.php/MBR#Restoring_a_Windows_boot_record "MBR")。

### 在引导菜单中编辑 GRUB 条目

你选中了引导菜单中的条目后就可以按 `e` 来编辑。如果要找设备的话使用 Tab 补全，然后 `Esc` 退出。之后按 `b` 来引导。

**注意:** 这些设置**不会被保存**。

### device.map error

如果安装或引导时错误信息提及 `/boot/grub/device.map`, 运行:

```
# grub-install --recheck /dev/sda

```

以强制 GRUB 再次检查设备映射，即使之前有过一次。这在调整分区和添加/移除驱动器之后是必需的。

### KDE 重启后下拉菜单失效

如果你已经打开了一个含有 GRUB 配置的所有操作系统的列表子菜单，在其中选择一个，并且在重新启动时，你仍然启动了默认的操作系统，那么你可能要检查你在 `/boot/grub/menu.lst` 里是否有下面这行:

```
default saved

```

### GRUB 无法找到或安装到 virtio */dev/vd** 或其他非 BIOS 设备

我曾经在把 virtio 设备作为硬件设备的 KVM 虚拟机里的 Arch Linux 上安装 GRUB 时碰到了麻烦。为了安装 GRUB, 尝试了以下方案: 按 `Ctrl+Alt+F2` 或其他按键进入虚拟终端。 假设你的根文件系统挂载到 `/mnt`，boot 挂载或存储到 `/mnt/boot`.

**1.** 通过如下命令确认 GRUB 文件存在于 boot 目录里 (假设挂载到 `/mnt/boot`):

```
# ls /mnt/boot/grub

```

**2.** 如果 `/mnt/boot/grub` 已包含所有需要的文件，跳至第 3 步。否则，运行如下命令 (把 `/mnt`, `your_kernel` 和 `your_initrd` 替换为真实路径和名称). 你的 `menu.lst` 也应在这里:

```
# mkdir -p /mnt/boot/grub                # if the folder is not yet present
# cp -r /boot/grub/stage1 /boot/grub/stage2 /mnt/boot/grub
# cp -r your_kernel your_initrd /mnt/boot

```

**3.** 通过如下命令启动 GRUB shell:

```
# grub --device-map=/dev/null

```

**4.** 键入以下命令。把 `/dev/vda` 和 `(hd0,0)` 替换为你的设备和分区:

```
device (hd0) /dev/vda
root (hd0,0)
setup (hd0)
quit

```

**5.** 如果 GRUB 没有错误提示，那么就差不多完成了。你还要往 ramdisk 加入合适的模块。更多信息参见 [QEMU#Preparing an (Arch) Linux guest](/index.php/QEMU#Preparing_an_.28Arch.29_Linux_guest "QEMU").

## 另见

*   [GNU GRUB](http://www.gnu.org/software/grub/)
*   [GRUB Grotto](http://www.troubleshooters.com/linux/grub/index.htm)
*   [Boot debugging](/index.php/Boot_debugging "Boot debugging") - Debugging with GRUB, set module values