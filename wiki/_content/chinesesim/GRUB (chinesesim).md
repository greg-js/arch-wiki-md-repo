**翻译状态：** 本文是英文页面 [GRUB](/index.php/GRUB "GRUB") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-11-15，点击[这里](https://wiki.archlinux.org/index.php?title=GRUB&diff=0&oldid=282734)可以查看翻译后英文页面的改动。

[GRUB2](http://www.gnu.org/software/grub/) 是下一代 GRand Unified Bootloader (GRUB,请不要和Grub Legacy混淆了)。 它来自下一代 GRUB 研究项目 [PUPA](http://www.nongnu.org/pupa/)，代码全部重写，实现了模块化和增强了移植性。[[1]](http://www.gnu.org/software/grub/grub-faq.en.html#q1).

简单的说,**Boot Loader**是电脑启动时运行的第一个程序,它负责装载内核并将控制权转交。内核再初始化操作系统的其它部分。

## Contents

*   [1 前言](#.E5.89.8D.E8.A8.80)
*   [2 BIOS 系统](#BIOS_.E7.B3.BB.E7.BB.9F)
    *   [2.1 GUID分区表(GPT)具体说明](#GUID.E5.88.86.E5.8C.BA.E8.A1.A8.28GPT.29.E5.85.B7.E4.BD.93.E8.AF.B4.E6.98.8E)
    *   [2.2 主引导记录(MBR)具体说明](#.E4.B8.BB.E5.BC.95.E5.AF.BC.E8.AE.B0.E5.BD.95.28MBR.29.E5.85.B7.E4.BD.93.E8.AF.B4.E6.98.8E)
    *   [2.3 安装](#.E5.AE.89.E8.A3.85)
        *   [2.3.1 安装Boot文件](#.E5.AE.89.E8.A3.85Boot.E6.96.87.E4.BB.B6)
            *   [2.3.1.1 安装到磁盘上](#.E5.AE.89.E8.A3.85.E5.88.B0.E7.A3.81.E7.9B.98.E4.B8.8A)
            *   [2.3.1.2 安装到U盘](#.E5.AE.89.E8.A3.85.E5.88.B0U.E7.9B.98)
            *   [2.3.1.3 安装到分区上或者无分区磁盘上](#.E5.AE.89.E8.A3.85.E5.88.B0.E5.88.86.E5.8C.BA.E4.B8.8A.E6.88.96.E8.80.85.E6.97.A0.E5.88.86.E5.8C.BA.E7.A3.81.E7.9B.98.E4.B8.8A)
            *   [2.3.1.4 只生成core.img](#.E5.8F.AA.E7.94.9F.E6.88.90core.img)
        *   [2.3.2 生成GRUB配置文件](#.E7.94.9F.E6.88.90GRUB.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
        *   [2.3.3 多系统启动](#.E5.A4.9A.E7.B3.BB.E7.BB.9F.E5.90.AF.E5.8A.A8)
            *   [2.3.3.1 在BIOS-MBR模式下安装的Microsoft Windows](#.E5.9C.A8BIOS-MBR.E6.A8.A1.E5.BC.8F.E4.B8.8B.E5.AE.89.E8.A3.85.E7.9A.84Microsoft_Windows)
*   [3 UEFI 系统](#UEFI_.E7.B3.BB.E7.BB.9F)
    *   [3.1 检查你是否使用GPT且有ESP分区](#.E6.A3.80.E6.9F.A5.E4.BD.A0.E6.98.AF.E5.90.A6.E4.BD.BF.E7.94.A8GPT.E4.B8.94.E6.9C.89ESP.E5.88.86.E5.8C.BA)
    *   [3.2 建立ESP](#.E5.BB.BA.E7.AB.8BESP)
    *   [3.3 安装](#.E5.AE.89.E8.A3.85_2)
        *   [3.3.1 延伸阅读](#.E5.BB.B6.E4.BC.B8.E9.98.85.E8.AF.BB)
            *   [3.3.1.1 其他方法](#.E5.85.B6.E4.BB.96.E6.96.B9.E6.B3.95)
        *   [3.3.2 在固件启动管理器中创建GRUB条目](#.E5.9C.A8.E5.9B.BA.E4.BB.B6.E5.90.AF.E5.8A.A8.E7.AE.A1.E7.90.86.E5.99.A8.E4.B8.AD.E5.88.9B.E5.BB.BAGRUB.E6.9D.A1.E7.9B.AE)
        *   [3.3.3 创建GRUB Standalone模式的UEFI应用程序](#.E5.88.9B.E5.BB.BAGRUB_Standalone.E6.A8.A1.E5.BC.8F.E7.9A.84UEFI.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
*   [4 配置](#.E9.85.8D.E7.BD.AE)
    *   [4.1 使用grub-mkconfig自动生成配置档](#.E4.BD.BF.E7.94.A8grub-mkconfig.E8.87.AA.E5.8A.A8.E7.94.9F.E6.88.90.E9.85.8D.E7.BD.AE.E6.A1.A3)
        *   [4.1.1 额外的参数](#.E9.A2.9D.E5.A4.96.E7.9A.84.E5.8F.82.E6.95.B0)
    *   [4.2 手动创建 grub.cfg](#.E6.89.8B.E5.8A.A8.E5.88.9B.E5.BB.BA_grub.cfg)
    *   [4.3 双启动](#.E5.8F.8C.E5.90.AF.E5.8A.A8)
        *   [4.3.1 使用/etc/grub.d/40_custom 和 grub-mkconfig自动生成](#.E4.BD.BF.E7.94.A8.2Fetc.2Fgrub.d.2F40_custom_.E5.92.8C_grub-mkconfig.E8.87.AA.E5.8A.A8.E7.94.9F.E6.88.90)
            *   [4.3.1.1 GNU/Linux 启动项](#GNU.2FLinux_.E5.90.AF.E5.8A.A8.E9.A1.B9)
            *   [4.3.1.2 FreeBSD 启动项](#FreeBSD_.E5.90.AF.E5.8A.A8.E9.A1.B9)
            *   [4.3.1.3 Windows XP 启动项](#Windows_XP_.E5.90.AF.E5.8A.A8.E9.A1.B9)
            *   [4.3.1.4 UEFI-GPT 模式下安装的Windows的启动项](#UEFI-GPT_.E6.A8.A1.E5.BC.8F.E4.B8.8B.E5.AE.89.E8.A3.85.E7.9A.84Windows.E7.9A.84.E5.90.AF.E5.8A.A8.E9.A1.B9)
            *   [4.3.1.5 "Shutdown" 启动项](#.22Shutdown.22_.E5.90.AF.E5.8A.A8.E9.A1.B9)
            *   [4.3.1.6 "Restart" 启动项](#.22Restart.22_.E5.90.AF.E5.8A.A8.E9.A1.B9)
        *   [4.3.2 通过EasyBCD NeoGRUB 和Windows共存](#.E9.80.9A.E8.BF.87EasyBCD_NeoGRUB_.E5.92.8CWindows.E5.85.B1.E5.AD.98)
    *   [4.4 可视化配置](#.E5.8F.AF.E8.A7.86.E5.8C.96.E9.85.8D.E7.BD.AE)
        *   [4.4.1 设定帧缓冲的分辨率](#.E8.AE.BE.E5.AE.9A.E5.B8.A7.E7.BC.93.E5.86.B2.E7.9A.84.E5.88.86.E8.BE.A8.E7.8E.87)
        *   [4.4.2 915resolution hack](#915resolution_hack)
        *   [4.4.3 背景图像和点阵字体](#.E8.83.8C.E6.99.AF.E5.9B.BE.E5.83.8F.E5.92.8C.E7.82.B9.E9.98.B5.E5.AD.97.E4.BD.93)
        *   [4.4.4 主题](#.E4.B8.BB.E9.A2.98)
        *   [4.4.5 目录颜色](#.E7.9B.AE.E5.BD.95.E9.A2.9C.E8.89.B2)
        *   [4.4.6 隐藏目录](#.E9.9A.90.E8.97.8F.E7.9B.AE.E5.BD.95)
        *   [4.4.7 禁用framebuffer](#.E7.A6.81.E7.94.A8framebuffer)
    *   [4.5 其他选项](#.E5.85.B6.E4.BB.96.E9.80.89.E9.A1.B9)
        *   [4.5.1 LVM](#LVM)
        *   [4.5.2 阵列](#.E9.98.B5.E5.88.97)
        *   [4.5.3 持久块设备命名法](#.E6.8C.81.E4.B9.85.E5.9D.97.E8.AE.BE.E5.A4.87.E5.91.BD.E5.90.8D.E6.B3.95)
        *   [4.5.4 使用卷标](#.E4.BD.BF.E7.94.A8.E5.8D.B7.E6.A0.87)
        *   [4.5.5 调用之前的启动项](#.E8.B0.83.E7.94.A8.E4.B9.8B.E5.89.8D.E7.9A.84.E5.90.AF.E5.8A.A8.E9.A1.B9)
        *   [4.5.6 改变默认启动项](#.E6.94.B9.E5.8F.98.E9.BB.98.E8.AE.A4.E5.90.AF.E5.8A.A8.E9.A1.B9)
        *   [4.5.7 安全](#.E5.AE.89.E5.85.A8)
        *   [4.5.8 root加密](#root.E5.8A.A0.E5.AF.86)
        *   [4.5.9 设定下次启动的启动项(一次性,非持久)](#.E8.AE.BE.E5.AE.9A.E4.B8.8B.E6.AC.A1.E5.90.AF.E5.8A.A8.E7.9A.84.E5.90.AF.E5.8A.A8.E9.A1.B9.28.E4.B8.80.E6.AC.A1.E6.80.A7.2C.E9.9D.9E.E6.8C.81.E4.B9.85.29)
        *   [4.5.10 启动时隐藏GRUB界面,除非按着SHIFT键](#.E5.90.AF.E5.8A.A8.E6.97.B6.E9.9A.90.E8.97.8FGRUB.E7.95.8C.E9.9D.A2.2C.E9.99.A4.E9.9D.9E.E6.8C.89.E7.9D.80SHIFT.E9.94.AE)
    *   [4.6 在GRUB中直接从ISO启动](#.E5.9C.A8GRUB.E4.B8.AD.E7.9B.B4.E6.8E.A5.E4.BB.8EISO.E5.90.AF.E5.8A.A8)
        *   [4.6.1 Arch ISO](#Arch_ISO)
            *   [4.6.1.1 x86_64](#x86_64)
            *   [4.6.1.2 i686](#i686)
        *   [4.6.2 Ubuntu ISO](#Ubuntu_ISO)
        *   [4.6.3 Other ISOs](#Other_ISOs)
*   [5 使用GRUB命令行](#.E4.BD.BF.E7.94.A8GRUB.E5.91.BD.E4.BB.A4.E8.A1.8C)
    *   [5.1 分页支持](#.E5.88.86.E9.A1.B5.E6.94.AF.E6.8C.81)
    *   [5.2 使用命令行引导操作系统](#.E4.BD.BF.E7.94.A8.E5.91.BD.E4.BB.A4.E8.A1.8C.E5.BC.95.E5.AF.BC.E6.93.8D.E4.BD.9C.E7.B3.BB.E7.BB.9F)
        *   [5.2.1 链式加载一个分区](#.E9.93.BE.E5.BC.8F.E5.8A.A0.E8.BD.BD.E4.B8.80.E4.B8.AA.E5.88.86.E5.8C.BA)
        *   [5.2.2 链式加载磁盘](#.E9.93.BE.E5.BC.8F.E5.8A.A0.E8.BD.BD.E7.A3.81.E7.9B.98)
        *   [5.2.3 正常载入](#.E6.AD.A3.E5.B8.B8.E8.BD.BD.E5.85.A5)
*   [6 图形化配置工具](#.E5.9B.BE.E5.BD.A2.E5.8C.96.E9.85.8D.E7.BD.AE.E5.B7.A5.E5.85.B7)
*   [7 parttool](#parttool)
*   [8 使用应急命令行](#.E4.BD.BF.E7.94.A8.E5.BA.94.E6.80.A5.E5.91.BD.E4.BB.A4.E8.A1.8C)
*   [9 使用UUID的基础脚本](#.E4.BD.BF.E7.94.A8UUID.E7.9A.84.E5.9F.BA.E7.A1.80.E8.84.9A.E6.9C.AC)
*   [10 异常处理](#.E5.BC.82.E5.B8.B8.E5.A4.84.E7.90.86)
    *   [10.1 Intel BIOS不能引导GPT](#Intel_BIOS.E4.B8.8D.E8.83.BD.E5.BC.95.E5.AF.BCGPT)
    *   [10.2 启用调试信息](#.E5.90.AF.E7.94.A8.E8.B0.83.E8.AF.95.E4.BF.A1.E6.81.AF)
    *   [10.3 "No suitable mode found" error](#.22No_suitable_mode_found.22_error)
    *   [10.4 出现"msdos-style"错误消息](#.E5.87.BA.E7.8E.B0.22msdos-style.22.E9.94.99.E8.AF.AF.E6.B6.88.E6.81.AF)
    *   [10.5 GRUB UEFI 启动到了rescue shell下](#GRUB_UEFI_.E5.90.AF.E5.8A.A8.E5.88.B0.E4.BA.86rescue_shell.E4.B8.8B)
    *   [10.6 GRUB UEFI 无法被载入](#GRUB_UEFI_.E6.97.A0.E6.B3.95.E8.A2.AB.E8.BD.BD.E5.85.A5)
    *   [10.7 "Invalid signature"错误](#.22Invalid_signature.22.E9.94.99.E8.AF.AF)
    *   [10.8 引导过程卡死](#.E5.BC.95.E5.AF.BC.E8.BF.87.E7.A8.8B.E5.8D.A1.E6.AD.BB)
    *   [10.9 回滚到 GRUB Legacy](#.E5.9B.9E.E6.BB.9A.E5.88.B0_GRUB_Legacy)
    *   [10.10 其他系统不能自动发现Arch Linux](#.E5.85.B6.E4.BB.96.E7.B3.BB.E7.BB.9F.E4.B8.8D.E8.83.BD.E8.87.AA.E5.8A.A8.E5.8F.91.E7.8E.B0Arch_Linux)
*   [11 参阅](#.E5.8F.82.E9.98.85)

## 前言

*   引导程序是计算机启动时第一个运行的程序。它负责加载并将控制权转移到Linux内核。内核作为回报，将初始化操作系统剩余部分
*   官方所称的GRUB代表的是本软件的第二版,即GRUB2,请参考[[2]](https://www.gnu.org/software/grub/).如果你是在找有关Grub Legacy的文章,请参考[GRUB Legacy](/index.php/GRUB_Legacy_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GRUB Legacy (简体中文)") .
*   GRUB2支持由zlib或者LZO压缩过的[Btrfs](/index.php/Btrfs "Btrfs")格式的根目录,如果使用Btrfs,不需要单独的`/boot`分区.
*   GRUB2 不支持[F2FS](/index.php/F2FS "F2FS")格式的根目录,所以你需要为`/boot`分区单独设置一个支持的文件系统.

## BIOS 系统

### GUID分区表(GPT)具体说明

BIOS/[GPT](/index.php/GPT "GPT")配置中，一个 [BIOS启动分区](http://www.gnu.org/software/grub/manual/html_node/BIOS-installation.html)是必需的。GRUB将`core.img`嵌入到这个分区。

**Note:**

*   在尝试分区之前请记住不是所有的系统都能够支持这种分区方案, 关于更多请阅读[GUID分区表](/index.php/GUID_Partition_Table#BIOS_systems "GUID Partition Table").
*   This additional partition is only needed on a GRUB, BIOS/GPT partitioning scheme. Previously, for a GRUB, BIOS/MBR partitioning scheme, GRUB used the Post-MBR gap for the embedding the `core.img`). GRUB for GPT, however, does not use the Post-GPT gap to conform to GPT specifications that require 1_megabyte/2048_sector disk boundaries.
*   For [UEFI](/index.php/UEFI "UEFI") systems this extra partition is not required as no embedding of boot sectors takes place in that case.

Create a mebibyte partition (`+1M` with `fdisk` or `gdisk`) on the disk with no file system and type BIOS boot (*BIOS boot* in fdisk, `ef02` in gdisk, `bios_grub` in `parted`). This partition can be in any position order but has to be on the first 2 TiB of the disk. This partition needs to be created before GRUB installation. When the partition is ready, install the bootloader as per the instructions below. The post-GPT gap can also be used as the BIOS boot partition though it will be out of GPT alignment specification. Since the partition will not be regularly accessed performance issues can be disregarded (though some disk utilities will display a warning about it). In `fdisk` or `gdisk` create a new partition starting at sector 34 and spanning to 2047 and set the type. To have the viewable partitions begin at the base consider adding this partition last.

### 主引导记录(MBR)具体说明

一般来说,如果使用兼容DOS的分区对齐模式,MBR后面空间(post-MBR gap)的大小都是31KiB(MBR和第一个分区之间的空间).不过,为了提供足够的空间嵌入GRUB的`core.img`文件([FS#24103](https://bugs.archlinux.org/task/24103)),建议将这个空间设置到1到2Mib.最好使用支持1MiB分区对齐的分区软件来分区,因为这样也能满足非512B扇区磁盘分区的需求.

### 安装

可以使用[pacman](/index.php/Pacman "Pacman")从[官方仓库](/index.php/Official_repositories "Official repositories")安装[grub](https://www.archlinux.org/packages/?name=grub)包.安装完成后它会代替[grub-legacy](https://aur.archlinux.org/packages/grub-legacy/).

**Note:** 简单的安装Grub包并不会更新`/boot/grub/i386-pc/core.img`和`/boot/grub/i386-pc`里的GRUB模组.需要使用下面介绍的`grub-install`来手动更新它们.

#### 安装Boot文件

有三种方式安装GRUB Boot文件:

*   [安装到磁盘上](#.E5.AE.89.E8.A3.85.E5.88.B0.E7.A3.81.E7.9B.98.E4.B8.8A) (推荐方式)
*   [安装到U盘](#.E5.AE.89.E8.A3.85.E5.88.B0U.E7.9B.98) (用于恢复)
*   [安装到分区或者无分区磁盘上](#.E5.AE.89.E8.A3.85.E5.88.B0.E5.88.86.E5.8C.BA.E4.B8.8A.E6.88.96.E8.80.85.E6.97.A0.E5.88.86.E5.8C.BA.E7.A3.81.E7.9B.98.E4.B8.8A) (不推荐)
*   [只生成core.img文件](#.E5.8F.AA.E7.94.9F.E6.88.90core.img) (最安全的方法, 但是需要另外的bootloader,比如[Syslinux](/index.php/Syslinux "Syslinux")来进行链式加载`/boot/grub/i386-pc/core.img`)

**Note:** 请参考 [http://www.gnu.org/software/grub/manual/html_node/BIOS-installation.html](http://www.gnu.org/software/grub/manual/html_node/BIOS-installation.html) 获取更详尽的资料

##### 安装到磁盘上

**Note:** 这种方法只限于将GRUB安装到可分区磁盘(MBR或GPT),GRUB 文件会被安装到`/boot/grub`,1st stage code会被安装到MBR的启动代码区域(以便和MBR分区表分开).对于无分区磁盘,请参考[#安装到分区上或者无分区磁盘上](#.E5.AE.89.E8.A3.85.E5.88.B0.E5.88.86.E5.8C.BA.E4.B8.8A.E6.88.96.E8.80.85.E6.97.A0.E5.88.86.E5.8C.BA.E7.A3.81.E7.9B.98.E4.B8.8A)

以下命令会将`grub`安装到MBR的启动代码区域,填充`/boot/grub`文件夹,生成`/boot/grub/i386-pc/core.img`,将其嵌入post-MBR gap或者放入BIOS boot partition中(分别对应MBR分区表和GPT分区表):

```
# grub-install --target=i386-pc --recheck --debug /dev/sda

```

**Note:**

*   `/dev/sda` 只是示例.
*   `--target=i386-pc`指示`grub-install`是为使用BIOS的系统安装. 推荐一直标明这点以防混淆.

如果你使用[LVM](/index.php/LVM "LVM")来进行启动,你可以将GRUB安装在多个物理磁盘上. 执行`grub-install`并不会生成GRUB配置文件,请移至[#生成GRUB配置文件](#.E7.94.9F.E6.88.90GRUB.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)一节

##### 安装到U盘

假设你的U盘第一个分区是FAT32，其分区是/dev/sdy1

```
# mkdir -p /mnt/usb ; mount /dev/sdy1 /mnt/usb
# grub-install --target=i386-pc --recheck --debug --boot-directory=/mnt/usb/boot /dev/sdy
# grub-mkconfig -o /mnt/usb/boot/grub/grub.cfg

```

```
# optional, backup config files of grub.cfg
# mkdir -p /mnt/usb/etc/default
# cp /etc/default/grub /mnt/usb/etc/default
# cp -a /etc/grub.d /mnt/usb/etc

```

```
#  sync ; umount /mnt/usb

```

##### 安装到分区上或者无分区磁盘上

**Note:** GRUB并不推荐将其安装到分区启动扇区或者无分区磁盘上(Grub Legacy和syslinux相反).这种安装方式不安全,当升级时可能会损坏.Arch开发人员也不支持这种方式

下面的命令将会将GRUB2安装到分区扇区或者无分区磁盘上(比如闪存上):

```
# chattr -i /boot/grub/i386-pc/core.img
# grub-install --target=i386-pc --recheck --debug --force /dev/sdaX
# chattr +i /boot/grub/i386-pc/core.img

```

**Note:**

*   `/dev/sda` 只是示例.
*   `--target=i386-pc`指示`grub-install`是为使用BIOS的系统安装. 推荐一直标明这点以防混淆.

必须使用`--force`选项来启用对blocklists(块列表)的支持,不应使用`--grub-setup=/bin/true`(这个选项的效果类似于只生成`core.img`). `grub-install`会生成以下警告,你可以通过这些警告判断发生了什么问题:

```
/sbin/grub-setup: warn: Attempting to install GRUB to a partitionless disk or to a partition. This is a BAD idea.
/sbin/grub-setup: warn: Embedding is not possible. GRUB can only be installed in this setup by using blocklists. 
                        However, blocklists are UNRELIABLE and their use is discouraged.

```

如果不指定`--force`选项,会出现以下错误,并且不会将启动代码安装到启动扇区上:

```
/sbin/grub-setup: error: will not proceed with blocklists

```

而指定了`--force`,会出现:

```
Installation finished. No error reported.

```

`grub-setup`不默认允许这种情况的原因是,在分区或者无分区磁盘上,`grub`依赖于嵌入分区引导扇区的块列表(blocklists)来定位`/boot/grub/i386-pc/core.img`和`/boot/grub`.而`core.img`在分区上的扇区位置很有可能随着分区文件系统的更改而变化(复制文件,删除文件等).详情请参考https://bugzilla.redhat.com/show_bug.cgi?id=728742 和 [https://bugzilla.redhat.com/show_bug.cgi?id=730915](https://bugzilla.redhat.com/show_bug.cgi?id=730915).

临时解决方案是给`/boot/grub/i386-pc/core.img`文件加"不可变"(immutable)标志.只有当将`grub`安装到分区启动扇区或者无分区磁盘上时才需要给core.img加"不可变"标志. 执行`grub-install`并不会生成GRUB配置文件,请移至[#生成GRUB配置文件](#.E7.94.9F.E6.88.90GRUB.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)一节

##### 只生成core.img

通过添加`--grub-setup=/bin/true`选项,`grub-install`命令会填充`/boot/grub`文件夹并生成`/boot/grub/i386-pc/core.img`,但是不会将grub启动引导代码嵌入到MBR,post-MBR gap和分区引导扇区中:

```
# grub-install --target=i386-pc --grub-setup=/bin/true --recheck --debug /dev/sda

```

**Note:**

*   `/dev/sda` 只是示例.
*   `--target=i386-pc`指示`grub-install`是为使用BIOS的系统安装. 推荐一直标明这点以防混淆.

生成后,Grub Legacy或者syslinux就可以通过链式加载GRUB2的`core.img`来间接加载Linux内核或者多启动内核了.

#### 生成GRUB配置文件

最后,生成GRUB2所需的配置文件(在配置章节会详述):

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

**Note:** 文件路径是`/boot/grub/grub.cfg`, 而不是`/boot/grub/i386-pc/grub.cfg`.

如果GRUB在启动时报错"no suitable mode found",请参考[#"No suitable mode found" error](#.22No_suitable_mode_found.22_error).

如果`grub-mkconfig`执行失败,可以通过如下方式将`/boot/grub/menu.lst`文件转化为`/boot/grub/grub.cfg`

**Note:** 这种方法只适合BIOS,不适合UEFI

```
# grub-menulst2cfg /boot/grub/menu.lst /boot/grub/grub.cfg

```

示例如下:

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

如果你忘记创建GRUB配置文件`/boot/grub/grub.cfg`,然后直接重启到了GRUB命令行界面,输入以下命令:

```
sh:grub> insmod legacycfg
sh:grub> legacy_configfile ${prefix}/menu.lst

```

选择启动到Arch下然后再重新创建合适的GRUB配置文件`/boot/grub/grub.cfg`

#### 多系统启动

为了实现多系统启动,需要安装[os-prober](https://www.archlinux.org/packages/?name=os-prober).安装后,再执行`grub-mkconfig -o /boot/grub/grub.cfg`.如果执行失败,可能就需要手动添加启动条目了.(后面有指导)

**Note:** 如果找不到Windows,可以将其boot partition挂载后再试

##### 在BIOS-MBR模式下安装的Microsoft Windows

**Note:** GRUB支持直接从`bootmgr`启动,现在不再需要链式加载分区启动扇区了

**Warning:** `bootmgr`位于**系统分区**(**system partition**),而不是Windows系统所在的分区(比如C盘).在uuid-卷名列表中,系统分区是那个名为`LABEL="SYSTEM RESERVED"` 或 `LABEL="SYSTEM"`的项,而且这个分区一般只有100到200MB大(和Arch的启动分区差不多).请参考[Wikipedia:System partition and boot partition](https://en.wikipedia.org/wiki/System_partition_and_boot_partition "wikipedia:System partition and boot partition")

本节假设你的Windows分区是`/dev/sda1`.首先,找到Windows系统分区的UUID(Windows's SYSTEM PARTITION,`bootmgr存放其上`).如果Windows `bootmgr`的位置是`/media/SYSTEM_RESERVED/bootmgr`,对于 Windows Vista/7/8,执行:

```
# grub-probe --target=fs_uuid /media/SYSTEM_RESERVED/bootmgr
69B235F6749E84CE

```

```
# grub-probe --target=hints_string /media/SYSTEM_RESERVED/bootmgr
--hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1

```

**Note:** 对于Windows XP, 请在上面的命令中用`NTLDR`替代`bootmgr`. 注意,可能`NTLDR`不是在名为"SYSTEM_RESERVED"的分区上,请在XP系统所在的分区上寻找 `NTLDR`

接着,将下面的代码添加到`/etc/grub.d/40_custom` 或者`/boot/grub/custom.cfg`中.然后,使用`grub-mkconfig`重新生成`grub.cfg`,这样就能在BIOS-MBR配置下使用GRUB2引导启动Windows系统了:

对于 Windows Vista/7/8

```
if [ "${grub_platform}" == "pc" ]; then
  menuentry "Microsoft Windows Vista/7/8 BIOS-MBR" {
    insmod part_msdos
    insmod ntfs
    insmod search_fs_uuid
    insmod ntldr     
    search --fs-uuid --set=root --hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1 69B235F6749E84CE
    ntldr /bootmgr
  }
fi

```

对于Windows XP

```
if [ "${grub_platform}" == "pc" ]; then
  menuentry "Microsoft Windows XP" {
    insmod part_msdos
    insmod ntfs
    insmod search_fs_uuid
    insmod ntldr     
    search --fs-uuid --set=root --hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1 69B235F6749E84CE
    ntldr /bootmgr
  }
fi

```

**Note:** 在某些情况下,可能在安装Windows 8之前就已经安装了GRUB.启动Windows时可能会`\boot\bcd`报错(错误代码为`0xc000000f`).可以通过Wondows Recovery Console来修复这个错误:
```
x:\> "bootrec.exe /fixboot" 
x:\> "bootrec.exe /RebuildBcd".

```

**不要**使用`bootrec.exe /Fixmbr`,因为那会将GRUB清除掉

`/etc/grub.d/40_custom`可以做为创建`/etc/grub.d/nn_custom`的模板.`nn`定义了脚本执行的优先级.脚本执行的顺序又决定了grub引导启动目录的内容.

**Note:** `nn` 应该比06大,这样才能确保必要的脚本被优先执行

## UEFI 系统

**注意:**

*   建议阅读并理解[UEFI](/index.php/UEFI "UEFI"), [GPT](/index.php/GPT "GPT") and [UEFI Bootloaders](/index.php/UEFI_Bootloaders "UEFI Bootloaders")
*   使用UEFI安装时，重要的是从开始安装时您的机器就在 UEFI 模式。Arch Linux的安装介质必须是UEFI启动。

### 检查你是否使用GPT且有ESP分区

如果想要使用EFI在某个磁盘上进行启动,那么就需要对这个磁盘进行EFI系统分区(EFI System Partition,即ESP),GPT倒不是必须的,不过我们还是高度建议使用GTP,并且这也是本篇文章当前支持的方法.如果你在一个支持EFI,并且已经有操作系统的电脑上安装Arch(比如Windows 8),那么你已经有了ESP了.可以通过`parted`来列出启动磁盘上的分区表以检查其是否支持GPT和ESP(假设这个启动磁盘是/dev/sda)

```
# parted /dev/sda print

```

如果使用GPT,那么会出现"分区表:GPT".如果使用EFI,那么会有一个文件系统为vfat的小分区(一般小于512MiB)并且被标志为启动分区.在这个小分区上,应该有一个名为EFI的文件夹.如果这些条件都满足,那么这就是ESP了.注意分区序号,因为之后安装GRUB2时你需要mount它.

### 建立ESP

如果你没有ESP,请参考[UEFI#EFI System Partition](/index.php/UEFI#EFI_System_Partition "UEFI")的引导来创建它

### 安装

**注意:** 众所周知,不同的主板厂商的UEFI实现方式也不一样.我们鼓励用户将其配置过程中遇到的问题及其细节分享出来.为了保证[GRUB](/index.php/GRUB "GRUB")页面的简洁,请参考[GRUB/EFI examples (简体中文)](/index.php/GRUB/EFI_examples_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GRUB/EFI examples (简体中文)")

本节假设您正在安装GRUB的x86_64系统下（x86_64-EFI）。对于 i686 系统，在适当情况下替换为 `x86_64-efi` 和 `i386-efi`。 请确保您在 [bash](/index.php/Bash_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Bash (简体中文)") shell 中。例如，当从Arch ISO引导时：

```
# arch-chroot /mnt /bin/bash

```

安装[grub](https://www.archlinux.org/packages/?name=grub) [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr)包。"GRUB"是引导程序， *efibootmgr* creates bootable `.efi` stub entries used by the GRUB installation script. 接下来的步骤将安装GRUB UEFI 程序到 `**$esp**/EFI/grub`中, 安装其模块到`/boot/grub/x86_64-efi`, and place the bootable `grubx64.efi` stub in `**$esp**/EFI/grub`.

首先，告诉GRUB使用UEFI，设置引导目录，并设置引导程序ID，将`$esp` 修改为你的 efi 分区 (通常为 `/boot`)

```
# grub-install --target=x86_64-efi --efi-directory=$esp --bootloader-id=grub --recheck

```

The `--bootloader-id` is what appears in the boot options to identity the GRUB EFI boot option; make sure this is something you will recognize later. The install will create a directory of the same name under `$esp/EFI/` where the EFI binary bootloader will be placed. 上述安装完成后 GRUB 的主目录将位于 `/boot/grub/`。

**注意:**

*   虽然一些发行版需要 `/boot/efi`或`/boot/EFI`目录，但 Arch没有。
*   `--efi-directory` 和 `--bootloader-id`是特定于GRUB UEFI的. `--efi-directory` 指定了 ESP分区的挂载点。`--root-directory`已经废弃了并被取代。
*   您可能注意到在 `grub-install`命令中没有一个<device_path>选项(例如: `/dev/sda`)。In fact any <device_path> provided will be ignored by the GRUB install script, as UEFI bootloaders do not use a MBR or partition boot sector at all.

现在GRUB已经安装好了.请移至[配置](#.E9.85.8D.E7.BD.AE)一节继续.

#### 延伸阅读

下面是关于通过UEFI安装Arch的相关信息

##### 其他方法

如果你想将所有的GRUB boot 文件放在ESP中,请给grub-install命令添加`--boot-directory=$esp/EFI`选项:

```
# grub-install --target=x86_64-efi --efi-directory=$esp --bootloader-id=grub --boot-directory=$esp/EFI --recheck --debug

```

下面的命令会将GRUB模组文件放在`$esp/EFI/grub`中.使用这个方法,grub.cfg也会被放在ESP中,所以请确保grub-mkconfig指向了正确的地方:

```
# grub-mkconfig -o $esp/EFI/grub/grub.cfg

```

配置档和BIOS-GRUB是一样的.

#### 在固件启动管理器中创建GRUB条目

`grub-install`会自动尝试在启动管理器中创建GRUB条目.如果没有成功,请参考[Beginners' guide#GRUB](/index.php/Beginners%27_guide#GRUB "Beginners' guide"),里面有关于使用`efibootmgr`创建启动目录条目的介绍.一般来说,这个问题都是因为你没有以UEFI模式启动CD/USB造成的.请参考[UEFI#Create UEFI bootable USB from ISO](/index.php/UEFI#Create_UEFI_bootable_USB_from_ISO "UEFI").

#### 创建GRUB Standalone模式的UEFI应用程序

可以建立一个`grubx64_standalone.efi`,这个应用将所有的模组嵌入自身的memdisk中,所以就不需要使用单独的目录来存放GRUB UEFI模组和其他相关文件了,使用[grub](https://www.archlinux.org/packages/?name=grub)包里的`grub-mkstandalone`可以实现这个功能.

最简单的的方法就是使用`grub-mkstandalone`,不过,我们还可以指定嵌入哪些模组:

```
# grub-mkstandalone --directory="/usr/lib/grub/x86_64-efi/" --format="x86_64-efi" --compression="xz" \
--output="$esp/EFI/grub/grubx64_standalone.efi" <你想嵌入的模组>

```

`grubx64_standalone.efi`文件要求将`grub.cfg`放置到`(memdisk)/boot/grub`中,而这个memdisk是嵌入到EFI应用当中的.`grub-mkstandlone`脚本允许传递将要嵌入memdisk的文件列表.(上面命令里的"<你想嵌入的模组>")

如果你的`grub.cfg`的路径是`/home/user/Desktop/grub.cfg`,那么需要创建一个临时的`/home/user/Desktop/boot/grub/`目录,然后将grub.cfg复制到其中并进入这个目录并运行:

```
# grub-mkstandalone --directory="/usr/lib/grub/x86_64-efi/" --format="x86_64-efi" --compression="xz" \
--output="$esp/EFI/grub/grubx64_standalone.efi" "boot/grub/grub.cfg"

```

进入`/home/user/Desktop/boot/grub/`但是传递`boot/grub/grub.cfg`参数(请注意是`boot/`而不是`/boot/`)的原因是`grub-mkstandalone`会自动将boot/grub/grub.cfg处理为`/(memdisk)/boot/grub/grub.cfg`

如果你传递`/home/user/Desktop/grub.cfg`,那么处理后的结果会是`(memdisk)/home/user/Desktop/grub.cfg`.如果传递`/home/user/Desktop/boot/grub/grub.cfg`,那么结果就是`(memdisk)/home/user/Desktop/boot/grub/grub.cfg`.所以需要进入`/home/user/Desktop/boot/grub/`并传递`boot/grub/grub.cfg`参数,因为这样才能生成`grub.efi`需要的`(memdisk)/boot/grub/grub.cfg`.

如果需要为`$esp/EFI/arch_grub/grubx64_standalone.efi`创建一个UEFI启动器条目,使用`efibootmgr`.[#Create GRUB entry in the Firmware Boot Manager](#Create_GRUB_entry_in_the_Firmware_Boot_Manager)里有介绍

## 配置

可以自动生成配置档,也可以手动编辑`grub.cfg`.

**Note:**

*   对于EFI系统,如果在安装GRUB时使用 `--boot-directory=$esp/EFI`了选项,`grub.cfg`文件必须和`grubx64.efi`放在同一文件夹.如果没有使用这个选项,那么`grub.cfg`应当在`/boot/grub/`下,和GRUB BIOS系统一样.
*   在[这里](http://members.iinet.net/~herman546/p20/GRUB2%20Configuration%20File%20Commands.html)可以找到关于如何配置GRUB的完整描述.

### 使用grub-mkconfig自动生成配置档

和GRUB Legacy配置文件`menu.lst`对应的GRUB配置文件是`/etc/default/grub` 和`/etc/grub.d/*`.`grub-mkconfig`使用这些文件来生成`grub.cfg`.grub-mkconfig默认输出至stdout.以下命令可以生成一个`grub.cfg`文件:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

`/etc/grub.d/10_linux`会自动为Arch Linux设置启动项.其他操作系统的话,可能需要手动在`/etc/grub.d/40_custom`或`/boot/grub/custom.cfg`中设置.

**Note:** 如果你在一个chroot环境中或者systemd-nspawn容器里执行这些操作,可能完全不会成功,因为grub-probe不能获取'/dev/sdaX'这样的典型路径.这种情况下,可以尝试使用[arch-chroot](https://bbs.archlinux.org/viewtopic.php?pid=1225067#p1225067).

#### 额外的参数

在`/etc/default/grub`中设置`GRUB_CMDLINE_LINUX`和`GRUB_CMDLINE_LINUX_DEFAULT`变量可以实现将向Linux镜像传递额外的参数.生成`grub.cfg`时,如果遇到普通启动项,这两个参数会一起使用,遇到*recovery*启动项,就只使用`GRUB_CMDLINE_LINUX`参数.

没有必要两者一起使用.这两个参数很有用.比如,如果要系统支持休眠后恢复,需要使用`GRUB_CMDLINE_LINUX_DEFAULT="resume=/dev/sdaX quiet"` (`sda**X**`是交换分区).这个选项会生成一个recovery启动项,这个启动项没有resume和quiet参数.其他的普通启动项也可能使用它们.(GRUB会为每个内核生成两个启动项,一个默认的一个recovery的,GRUB_CMDLINE_LINUX指定的参数会传递给这两个启动项.GRUB_CMDLINE_LINUX_DEFAULT指定的参数只会传递给默认启动项)

当生成GRUB recovery启动项时,你必须在`/etc/default/grub`中将`#GRUB_DISABLE_RECOVERY=true` 注释掉.

你也可以使用`GRUB_CMDLINE_LINUX="resume=/dev/disk/by-uuid/${swap_uuid}"`, `${swap_uuid}` 是交换分区的[UUID](/index.php/Persistent_block_device_naming "Persistent block device naming")

不同的启动项使用双引号引起来并用空格隔开.所以,对于即想使用resume又想使用systemd的用户来说,这个参数的设置可能是: `GRUB_CMDLINE_LINUX="resume=/dev/sdaX init=/usr/lib/systemd/systemd"` 更多信息请参考[Kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

### 手动创建 grub.cfg

**Warning:** *不推荐*编辑这个文件.这个文件由`grub-mkconfig`生成,最好编辑`/etc/default/grub`和`/etc/grub.d`文件夹下的脚本以实现修改.

基本的GRUB配置文件使用如下选项:

*   `(hd*X*,*Y*)` 是*X*磁盘的*Y*分区,分区从1开始计数,磁盘从0开始计数.
*   `set default=*N*`设定用户选择超时时间过后的默认启动项
*   `set timeout=*M*`设定用户选择超时时间(秒).
*   `menuentry "title" {entry options}`设置一个名为`title`的启动项
*   `set root=(hd*X*,*Y*)`设定启动分区(kernel和GRUB模组所在磁盘),/boot没被要求独占一个分区,有可能就是root分区下的一个文件夹

示例配置如下:

 `/boot/grub/grub.cfg` 
```
# Config file for GRUB - The GNU GRand Unified Bootloader
# /boot/grub/grub.cfg

# DEVICE NAME CONVERSIONS
#
#  Linux           Grub
# -------------------------
#  /dev/fd0        (fd0)
#  /dev/sda        (hd0)
#  /dev/sdb2       (hd1,2)
#  /dev/sda3       (hd0,3)
#

# Timeout for menu
set timeout=5

# Set default boot entry as Entry 0
set default=0

# (0) Arch Linux
menuentry "Arch Linux" {
  set root=(hd0,1)
  linux /vmlinuz-linux root=/dev/sda3 ro
  initrd /initramfs-linux.img
}

## (1) Windows
#menuentry "Windows" {
#  set root=(hd0,3)
#  chainloader +1
#}

```

### 双启动

**Note:** 如果你希望GRUB自动搜寻其他系统, 可以安装[os-prober](https://www.archlinux.org/packages/?name=os-prober).

#### 使用/etc/grub.d/40_custom 和 grub-mkconfig自动生成

添加其他启动项的最好方法是编辑`/etc/grub.d/40_custom`或`/boot/grub/custom.cfg`.运行`grub-mkconfig`后,这些文件中的启动项会被自动添加到grub.cfg中. 更新了这些文件后,运行:

 `# grub-mkconfig -o /boot/grub/grub.cfg` 

在UEFI-GPT模式下,运行:

 `# grub-mkconfig -o /boot/efi/EFI/GRUB/grub.cfg` 

这样会更新`grub.cfg`

一个典型`/etc/grub.d/40_custom`文件类似于下面这个为[HP Pavilion 15-e056sl Notebook PC|预装WIN8的HP Pavilion 15-e056sl Notebook PC](http://h10025.www1.hp.com/ewfrf/wc/product?cc=us&destPage=product&lc=en&product=5402703&tmp_docname=)而作的配置.每个启动项的结构都应该和下面的类似.请注意UEFI分区`/dev/sda2` 被命名为`hd0,gpt2` 和`ahci0,gpt2`(请参考[here](/index.php/GRUB#Windows_installed_in_UEFI-GPT_Mode_menu_entry "GRUB")获取更多信息)

**/etc/grub.d/40_custom**:

```
#!/bin/sh
exec tail -n +3 $0
# This file provides an easy way to add custom menu entries.  Simply type the
# menu entries you want to add after this comment.  Be careful not to change
# the 'exec tail' line above.

menuentry "HP / Microsoft Windows 8.1" {
	echo "Loading HP / Microsoft Windows 8.1..."
	insmod part_gpt
	insmod fat
	insmod search_fs_uuid
	insmod chain
	search --fs-uuid --set=root --hint-bios=hd0,gpt2 --hint-efi=hd0,gpt2 --hint-baremetal=ahci0,gpt2 763A-9CB6
	chainloader (${root})/EFI/Microsoft/Boot/bootmgfw.efi
}

menuentry "HP / Microsoft Control Center" {
	echo "Loading HP / Microsoft Control Center..."
	insmod part_gpt
	insmod fat
	insmod search_fs_uuid
	insmod chain
	search --fs-uuid --set=root --hint-bios=hd0,gpt2 --hint-efi=hd0,gpt2 --hint-baremetal=ahci0,gpt2 763A-9CB6
	chainloader (${root})/EFI/HP/boot/bootmgfw.efi
}

menuentry "System shutdown" {
	echo "System shutting down..."
	halt
}

menuentry "System restart" {
	echo "System rebooting..."
	reboot
}
```

##### GNU/Linux 启动项

假设另一个发行版位于`sda2`:

```
menuentry "Other Linux" {
	set root=(hd0,2)
	linux /boot/vmlinuz (add other options here as required)
	initrd /boot/initrd.img (if the other kernel uses/needs one)
}
```

##### FreeBSD 启动项

要求FreeBSD以UFS格式被安装在单独的分区上,假设安装在`sda4`上:

```
menuentry "FreeBSD" {
	set root=(hd0,4)
	chainloader +1
}
```

##### Windows XP 启动项

假设Windows分区是`sda3`.请记住需要将root设置到Windows安装时建立的启动分区上,然后链式加载它,而不是Windows系统所在分区.下面的例子就是假设启动分区就是`sda3`.

```
# (2) Windows XP
menuentry "Windows XP" {
	set root="(hd0,3)"
	chainloader +1
}
```

如果Windows的bootloader和GRUB不在一个硬盘上,那么需要让Windows认为它是在第一硬盘上.使用`drivemap`可以实现这点.假设GRUB在`hd0`而windows在`hd2`上,需要在设定root后执行:

 `drivemap -s hd0 hd2` 

##### UEFI-GPT 模式下安装的Windows的启动项

```
if [ "${grub_platform}" == "efi" ]; then
	menuentry "Microsoft Windows Vista/7/8 x86_64 UEFI-GPT" {
		insmod part_gpt
		insmod fat
		insmod search_fs_uuid
		insmod chain
		search --fs-uuid --set=root $hints_string $uuid
		chainloader /EFI/Microsoft/Boot/bootmgfw.efi
	}
fi
```

`$hints_string` 和 `$uuid`可以通过以下命令获取:

`$uuid`:

```
# grub-probe --target=fs_uuid $esp/EFI/Microsoft/Boot/bootmgfw.efi
1ce5-7f28
```

`$hints_string`:

```
# grub-probe --target=hints_string $esp/EFI/Microsoft/Boot/bootmgfw.efi
 --hint-bios=hd0,gpt1 --hint-efi=hd0,gpt1 --hint-baremetal=ahci0,gpt1
```

这两个命令都是假设ESP挂载在`$esp`上.当然,Windows的EFI文件路径可能有变,因为这就是Windows....

##### "Shutdown" 启动项

```
menuentry "System shutdown" {
	echo "System shutting down..."
	halt
}
```

##### "Restart" 启动项

```
menuentry "System restart" {
	echo "System rebooting..."
	reboot
}
```

#### 通过EasyBCD NeoGRUB 和Windows共存

现在EasyBCD的NeoGRUB还不能识别GRUB的目录格式,在 `C:\NST\menu.lst` 中添加如下行以链式加载到GRUB:

```
default 0
timeout 1

```

```
title       Chainload into GRUB v2
root        (hd0,7)
kernel      /boot/grub/i386-pc/core.img

```

最后,使用`grub-mkconfig`重建`grub.cfg`

### 可视化配置

GRUB默认就支持定制启动目录的外观.不过要确保使用合适的视频模式初始化GRUB的图形化终端gfxterm.在[#"No suitable mode found" error](#.22No_suitable_mode_found.22_error)一节中有介绍.GRUB通过'gfxpayload'来将视频模式传递给linux内核,所以任何可视化配置都需要这个模式的信息以正确工作.

#### 设定帧缓冲的分辨率

GRUB既可以为自己,也可以为内核设定帧缓冲.现在已经不使用老的`vga=`配置了.推荐方法是在`/etc/default/grub`进行如下编辑:

```
GRUB_GFXMODE=1024x768x32
GRUB_GFXPAYLOAD_LINUX=keep

```

运行以下命令使配置生效:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

`gfxpayload`属性会确保内核也保持这个分辨率

**Note:**

*   如果示例不起作用,请尝试用`vbemode="0x105"`代替`gfxmode="1024x768x32"`.请使用适合你屏幕的分辨率.
*   可以通过`# hwinfo --framebuffer`命令来显示所有可以使用的分辨率模式(hwinfo在[community](/index.php/Community "Community")里),在GRUB命令行下,可以使用`vbeinfo` 命令

这种方法不管用的话,可以试试老的`vga=`方法.将它添加到`"GRUB_CMDLINE_LINUX_DEFAULT="`里面就行了,比如 `"GRUB_CMDLINE_LINUX_DEFAULT="quiet splash vga=792"` 这会将系统的分辨率设定为1024*768

可以选择以下分辨率中的一种:`640×480`, `800×600`, `1024×768`, `1280×1024`, `1600×1200`, `1920×1200`

#### 915resolution hack

有些时候,Intel显卡无法通过`# hwinfo --framebuffer` 或`vbeinfo`显示你需要的分辨率.这种情况下,你可以使用`915resolution hack`.915resolution hack会临时性的修改显卡BIOS来添加所需的分辨率.详情请参考[915resolution's home page](http://915resolution.mango-lang.org/)

首先,找一个你想要替代的视频模式.例如在GRUB命令行模式下运行:

 `sh:grub> 915resolution -l` 
```
Intel 800/900 Series VBIOS Hack : version 0.5.3
[...]
**Mode 30** : 640x480, 8 bits/pixel
[...]

```

然后,使用`1440x900` 分辨率覆盖`Mode 30`

 `/etc/grub.d/00_header` 
```
[...]
**915resolution 30 1440 900  # Inserted line**
set gfxmode=${GRUB_GFXMODE}
[...]

```

最后,设置`GRUB_GFXMODE`,重新生成GRUB配置文件,重启并测试是否生效:

```
# grub-mkconfig -o /boot/grub/grub.cfg
# reboot

```

#### 背景图像和点阵字体

GRUB原生支持设置背景图像和点阵字体(以pf2格式).[grub](https://www.archlinux.org/packages/?name=grub)包含unifont字体,名为`unicode.pf2`.(也有可能只包含名为`ascii.pf2`的ASCII字符字体)

GRUB支持的图像格式有tga,png,jpeg.所支持的最大图像分辨率跟硬件有关.

Make sure you have set up the proper [framebuffer resolution](#Setting_the_framebuffer_resolution). 请确保你已经设定了合适的[帧缓冲分辨率](#.E8.AE.BE.E5.AE.9A.E5.B8.A7.E7.BC.93.E5.86.B2.E7.9A.84.E5.88.86.E8.BE.A8.E7.8E.87)

编辑`/etc/default/grub`:

```
GRUB_BACKGROUND="/boot/grub/myimage"
#GRUB_THEME="/path/to/gfxtheme"
GRUB_FONT="/path/to/font.pf2"

```

**Note:** 如果你将GRUB安装在单独的分区上, `/boot/grub/myimage` 应该改为 `/grub/myimage`.

重新生成配置文件:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

如果成功的添加了背景图片,那么用户会在命令行中看到`"Found background image..."`. 如果没有看到`"Found background image..."`,图像信息就可能没有嵌入`grub.cfg`中了.

如果图像没有正确显示,执行如下检查:

*   在`/etc/default/grub`里,图像的路径和名字是否正确
*   图像的大小和格式是否合适(tga,png,8-bit jpg)
*   图像是不是以RGB模式存储,是不是没有索引
*   `/etc/default/grub`里面是不是没有开启console模式
*   是否执行`grub-mkconfig`以重新生成配置文件

#### 主题

下面的例子将展示如何使用GRUB包重的starfield主题:

编辑 `/etc/default/grub`

```
GRUB_THEME="/usr/share/grub/themes/starfield/theme.txt"

```

重生成配置:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

配置成功的话,在重生成配置过程中,会出现`Found theme: /usr/share/grub/themes/starfield/theme.txt`.使用主题就不会使用之前的背景图像

#### 目录颜色

GRUB支持设置目录颜色.可使用的颜色能从[the GRUB Manual](https://www.gnu.org/software/grub/manual/html_node/Theme-file-format.html)里面找到.示例如下:

编辑`/etc/default/grub`:

```
GRUB_COLOR_NORMAL="light-blue/black"
GRUB_COLOR_HIGHLIGHT="light-cyan/blue"

```

重建配置档:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

#### 隐藏目录

GRUB特性之一就是支持隐藏/跳过目录,同时支持按`Esc`来打断隐藏/跳过.同时还支持设置是否显示timeout计时器 下面的例子设置5s钟内没有按Esc键就启动默认的启动项,并且在屏幕上显示倒计时:

编辑`/etc/default/grub`:

```
GRUB_HIDDEN_TIMEOUT=5
GRUB_HIDDEN_TIMEOUT_QUIET=false

```

重建配置档:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

#### 禁用framebuffer

Users who use NVIDIA proprietary driver might wish to disable GRUB's framebuffer as it can cause problems with the binary driver. 使用NVIDIA私有驱动的用户可能希望禁用GRUB的framebuffer,因为会导致驱动错误.

在`/etc/default/grub`中添加(如果已经有背注释掉的这行,就取消注释):

```
GRUB_TERMINAL_OUTPUT=console

```

重建配置档:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

如果你想保留GRUB的framebuffer,解决方法是在GRUB载入内核前进入文字模式.可以通过在`/etc/default/grub`设置如下:

```
GRUB_GFXPAYLOAD_LINUX=text

```

然后重建配置档.

### 其他选项

#### LVM

如果使用[LVM](/index.php/LVM "LVM")做为启动设备,那么在启动项里添加:

```
insmod lvm

```

然后在启动项里指定root:

```
set root=lvm/*lvm_group_name*-*lvm_logical_boot_partition_name*

```

示例如下:

```
# (0) Arch Linux
menuentry "Arch Linux" {
  insmod lvm
  set root=lvm/VolumeGroup-lv_boot
  # you can only set following two lines
  linux /vmlinuz-linux root=/dev/mapper/VolumeGroup-root ro
  initrd /initramfs-linux.img
}

```

#### 阵列

通过添加`insmod mdraid`,GRUB能够很方便的处理磁盘阵列.比如`/dev/md0`:

```
set root=(md0)

```

阵列上的分区(比如`/dev/md0p1`)则为:

```
set root=(md0,1)

```

如果启动分区在raid1上,想要安装grub,只需要在两个磁盘上分别运行grub-install即可:

```
grub-install --target=i386-pc --recheck --debug /dev/sda && grub-install --target=i386-pc --recheck --debug /dev/sdb

```

这时/dev/sda和/dev/sdb就都有了raid1的启动文件夹/boot了

#### 持久块设备命名法

[持久块设备命名法](/index.php/Persistent_block_device_naming "Persistent block device naming")(Persistent block device naming)的一个目的是使用全局的UUID来区分分区,而不是用老的`/dev/sd*`表示法.好处显而易见.

GRUB默认使用持久块设备命名法

**Note:** 每次文件系统调整过后,就需要用新的UUID来更新`/boot/grub.cfg`.通过Live-CD调整分区和文件系统后要特别注意这点

是否使用UUID由`/etc/default/grub`里的这个选项控制:

```
# GRUB_DISABLE_LINUX_UUID=true

```

无论如何,变更配置后请重建配置档:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

#### 使用卷标

GRUB支持以卷标识别文件系统(通过`search`命令的`--label参数`).

首先,给文件系统设置一个卷标:

```
# tune2fs -L *LABEL* *PARTITION*

```

然后在启动项中使用这个卷标:

```
menuentry "Arch Linux, session texte" {
  search --label --set=root archroot
  linux /boot/vmlinuz-linux root=/dev/disk/by-label/archroot ro
  initrd /boot/initramfs-linux.img
}

```

#### 调用之前的启动项

GRUB能够记住你当前使用的启动项并且在下次启动时将其作为默认项.当你使用多个内核或操作系统时,这个特性很有用. 编辑`/etc/default/grub`中的`GRUB_DEFAULT`选项:

```
GRUB_DEFAULT=saved

```

上面的命令会告诉GRUB使用记住的启动项为默认启动项. 将下面的行添加到`/etc/default/grub`会让GRUB记住当前的启动项:

```
GRUB_SAVEDEFAULT=true

```

**Note:** 手动添加启动项到`/etc/grub.d/40_custom`或`/boot/grub/custom.cfg`中,比如Windows启动项,需要添加`savedefault`

请记住重建配置档.

#### 改变默认启动项

可以通过修改`/etc/default/grub`中的`GRUB_DEFAULT`值来改变默认启动项

```
GRUB_DEFAULT=0

```

GRUB启动项序号从0开始计数.0代表第一个启动项.

除了使用启动项序号,也可以使用启动项名:

```
GRUB_DEFAULT='Arch Linux, with Linux core repo kernel'

```

**Note:** 请记住重建配置档

#### 安全

如果你想禁止其他人改变启动参数或者使用GRUB命令行,可以给GRUB配置添加用户名/密码. 运行 `grub-mkpasswd-pbkdf2`,输入密码:

 `grub-mkpasswd-pbkdf2` 
```
[...]
Your PBKDF2 is grub.pbkdf2.sha512.10000.C8ABD3E93C4DFC83138B0C7A3D719BC650E6234310DA069E6FDB0DD4156313DA3D0D9BFFC2846C21D5A2DDA515114CF6378F8A064C94198D0618E70D23717E82.509BFA8A4217EAD0B33C87432524C0B6B64B34FBAD22D3E6E6874D9B101996C5F98AB1746FE7C7199147ECF4ABD8661C222EEEDB7D14A843261FFF2C07B1269A

```

然后将下面的内容添加到`/etc/grub.d/00_header`:

 `/etc/grub.d/00_header` 
```
cat << EOF

set superusers="**username**"
password_pbkdf2 **username** **<password>**

EOF

```

**Note:** 不能直接将

set superusers="**username**" password_pbkdf2 **username** **<password>** 添加到/etc/grub.d/00_header中去,而必须使用上述方法.否则会报错 password_pbkdf2: not found

`<password>`是`grub-mkpasswd_pbkdf2`生成的那个加密过后密码.

然后重建配置档.其他用户没有密码就不能变更GRUB配置或者使用GRUB命令行了.

可以参考[the GRUB manual](https://www.gnu.org/software/grub/manual/grub.html#Security)中的"Security"部分来进行更多的客制化安全设定

#### root加密

将`cryptdevice=/dev/yourdevice:label`添加到`/etc/default/grub`中的`GRUB_CMDLINE_LINUX`配置项,可以让GRUB传递参数给内核,让内核对root加密:

**Tip:** 如果你使用从GRUB Legacy升级而来,检查`/boot/grub/menu.lst.pacsave`以获取正确的device/label. 在`kernel /vmlinuz-linux`后去找label.

将root映射到`/dev/mapper/root`:

```
GRUB_CMDLINE_LINUX="cryptdevice=/dev/sda2:root"

```

当然,需要在rootfs上禁用UUID:

```
GRUB_DISABLE_LINUX_UUID=true

```

Regenerate the configuration.

#### 设定下次启动的启动项(一次性,非持久)

命令`grub-reboot`可以设置下次启动时启动哪个启动项而不必修改配置文件或者在启动时手动选择.这个设置是一次性的,即不会改变GRUB的默认启动项.

**Note:** 需要在`/etc/default/grub`中设定 `GRUB_DEFAULT=saved`,然后重建配置档.在手动生成的 `grub.cfg`中, 使用 `set default="${saved_entry}"`.

#### 启动时隐藏GRUB界面,除非按着SHIFT键

为了获取更快的启动速度,而不用等GRUB倒计时,可以命令GRUB在启动时隐藏目录,除非SHIFT被按着. 将如下行添加到`/etc/default/grub`:

```
 GRUB_FORCE_HIDDEN_MENU="true"

```

然后创建如下文件:

 `/etc/grub.d/31_hold_shift` 
```
#! /bin/sh
set -e

# grub-mkconfig helper script.
# Copyright (C) 2006,2007,2008,2009  Free Software Foundation, Inc.
#
# GRUB is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# GRUB is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with GRUB.  If not, see <http://www.gnu.org/licenses/>.

prefix="/usr"
exec_prefix="${prefix}"
datarootdir="${prefix}/share"

export TEXTDOMAIN=grub
export TEXTDOMAINDIR="${datarootdir}/locale"
source "${datarootdir}/grub/grub-mkconfig_lib"

found_other_os=

make_timeout () {

  if [ "x${GRUB_FORCE_HIDDEN_MENU}" = "xtrue" ] ; then 
    if [ "x${1}" != "x" ] ; then
      if [ "x${GRUB_HIDDEN_TIMEOUT_QUIET}" = "xtrue" ] ; then
    verbose=
      else
    verbose=" --verbose"
      fi

      if [ "x${1}" = "x0" ] ; then
    cat <<EOF
if [ "x\${timeout}" != "x-1" ]; then
  if keystatus; then
    if keystatus --shift; then
      set timeout=-1
    else
      set timeout=0
    fi
  else
    if sleep$verbose --interruptible 3 ; then
      set timeout=0
    fi
  fi
fi
EOF
      else
    cat << EOF
if [ "x\${timeout}" != "x-1" ]; then
  if sleep$verbose --interruptible ${GRUB_HIDDEN_TIMEOUT} ; then
    set timeout=0
  fi
fi
EOF
      fi
    fi
  fi
}

adjust_timeout () {
  if [ "x$GRUB_BUTTON_CMOS_ADDRESS" != "x" ]; then
    cat <<EOF
if cmostest $GRUB_BUTTON_CMOS_ADDRESS ; then
EOF
    make_timeout "${GRUB_HIDDEN_TIMEOUT_BUTTON}" "${GRUB_TIMEOUT_BUTTON}"
    echo else
    make_timeout "${GRUB_HIDDEN_TIMEOUT}" "${GRUB_TIMEOUT}"
    echo fi
  else
    make_timeout "${GRUB_HIDDEN_TIMEOUT}" "${GRUB_TIMEOUT}"
  fi
}

  adjust_timeout

    cat <<EOF
if [ "x\${timeout}" != "x-1" ]; then
  if keystatus; then
    if keystatus --shift; then
      set timeout=-1
    else
      set timeout=0
    fi
  else
    if sleep$verbose --interruptible 3 ; then
      set timeout=0
    fi
  fi
fi
EOF

```

### 在GRUB中直接从ISO启动

编辑`/etc/grub.d/40_custom` 或 `/boot/grub/custom.cfg`,给目标ISO添加一个启动项.然后使用`grub-mkconfig -o /boot/grub/grub.cfg`更新配置档

#### Arch ISO

**Note:** 下面的例子都是假设ISO文件位于`hd0,6`分区上的`/archives`文件夹里

**Tip:** For thumbdrives, use something like `(hd1,$partition)` and either `/dev/sdb**Y**` for the `img_dev` parameter or [a persistent name](/index.php/Persistent_block_device_naming "Persistent block device naming"), e.g. `img_dev=/dev/disk/by-label/CORSAIR`.

**Tip:** 对于闪存,使用`(hd1,$partition)`或`/dev/sdb**Y**`作为`img_dev`参数的值,或者使用持久块设备命名法命名的设备,比如`img_dev=/dev/disk/by-label/CORSAIR`.

##### x86_64

```
menuentry "Archlinux-2013.05.01-dual.iso" --class iso {
  set isofile="/archives/archlinux-2013.05.01-dual.iso"
  set partition="6"
  loopback loop (hd0,$partition)/$isofile
  linux (loop)/arch/boot/x86_64/vmlinuz archisolabel=ARCH_201305 img_dev=/dev/sda$partition img_loop=$isofile earlymodules=loop
  initrd (loop)/arch/boot/x86_64/archiso.img
}

```

##### i686

```
menuentry "Archlinux-2013.05.01-dual.iso" --class iso {
  set isofile="/archives/archlinux-2013.05.01-dual.iso"
  set partition="6"
  loopback loop (hd0,$partition)/$isofile
  linux (loop)/arch/boot/i686/vmlinuz archisolabel=ARCH_201305 img_dev=/dev/sda$partition img_loop=$isofile earlymodules=loop
  initrd (loop)/arch/boot/i686/archiso.img
}

```

#### Ubuntu ISO

**Note:** 下面的例子都是假设ISO文件位于`hd0,6`分区上的`/archives`文件夹里. 用户需要根据自己系统的实际情况调整.

```
menuentry "ubuntu-13.04-desktop-amd64.iso" {
  set isofile="/archives/ubuntu-13.04-desktop-amd64.iso"
  loopback loop (hd0,6)/$isofile
  linux (loop)/casper/vmlinuz.efi boot=casper iso-scan/filename=$isofile quiet noeject noprompt splash --
  initrd (loop)/casper/initrd.lz
}

```

```
menuentry "ubuntu-12.04-desktop-amd64.iso" {
  set isofile="/archives/ubuntu-12.04-desktop-amd64.iso"
  loopback loop (hd0,6)/$isofile
  linux (loop)/casper/vmlinuz boot=casper iso-scan/filename=$isofile quiet noeject noprompt splash --
  initrd (loop)/casper/initrd.lz
}

```

#### Other ISOs

可从[这里](http://askubuntu.com/questions/141940/how-to-boot-live-iso-images)获取其他ISO的配置.

## 使用GRUB命令行

MBR太小,所以不足以存储所有的GRUB模组.MBR里面只有启动目录配置和一些很基本的命令.GRUB的主要功能通过`/boot/grub`里的模组实现,而且可以按需加载.出现错误时,GRUB可能不能引导启动(比如,磁盘分区发生了变化).这时候,一般会出现命令行界面.

GRUB不止提供一个shell.如果GRUB不能读取到启动目录配置,但是能找到磁盘,你很可能需要进入"normal" shell:

```
sh:grub>

```

如果有更严重的问题(比如,GRUB找不到必须的文件了),你就可能需要进入"rescue" shell:

```
grub rescue>

```

"rescue" shell是"normal" shell的一个子集,其支持的功能更少.如果不幸进入了"rescue" shell里,首先记载"normal"模组,然后启动"normal" shell:

```
grub rescue> set prefix=(hdX,Y)/boot/grub
grub rescue> insmod (hdX,Y)/boot/grub/i386-pc/normal.mod
rescue:grub> normal

```

### 分页支持

GRUB支持对长输出进行分页(比如运行`help`的输出).不过只有normal shell支持分页,而rescue shell不支持.开启分页支持的方法如下:

```
sh:grub> set pager=1

```

### 使用命令行引导操作系统

```
grub> 

```

可以使用GRUB命令行引导操作系统,一个典型的应用场景是通过**chainloading**来引导另一个Windows或Linux

*ChainLoading*的意思是用当前的bootloader去载入另一个bootloader,所以叫做**链式**加载.这个bootloader可能位于MBR,也可能在另一个分区的引导扇区上.

#### 链式加载一个分区

```
set root=(hdX,Y)
chainloader +1
boot

```

X=0,1,2... Y=1,2,3...

比如链式加载一个位于首磁盘,首分区上的Windows:

```
set root=(hd0,1)
chainloader +1
boot

```

也可以使用GRUB链式加载另一个分区引导扇区上的GRUB.

#### 链式加载磁盘

```
set root=hdX
chainloader +1
boot

```

#### 正常载入

请参考[#使用应急命令行](#.E4.BD.BF.E7.94.A8.E5.BA.94.E6.80.A5.E5.91.BD.E4.BB.A4.E8.A1.8C)

## 图形化配置工具

*   **grub-customizer** — 定制bootloader(GRUB or BURG)

	[https://launchpad.net/grub-customizer](https://launchpad.net/grub-customizer) || [grub-customizer](https://aur.archlinux.org/packages/grub-customizer/)

*   **grub2-editor** — KDE4上配置GRUB的控制模组

	[http://kde-apps.org/content/show.php?content=139643](http://kde-apps.org/content/show.php?content=139643) || [grub2-editor](https://aur.archlinux.org/packages/grub2-editor/)

*   **kcm-grub2** — 可以管理大部分常用GRUB配置的kcm模组

	[http://kde-apps.org/content/show.php?content=137886](http://kde-apps.org/content/show.php?content=137886) || [kcm-grub2](https://aur.archlinux.org/packages/kcm-grub2/)

*   **startupmanager** — GRUB Legacy, GRUB, Usplash and Splashy的图形化配置工具([abandonned](https://launchpad.net/startup-manager/+announcement/8300))

	[http://sourceforge.net/projects/startup-manager/](http://sourceforge.net/projects/startup-manager/) || [startupmanager](https://aur.archlinux.org/packages/startupmanager/)

## parttool

如果你安装了Windows 9x系列操作系统,而它们隐藏了磁盘(比如C盘),GRUB能够使用parttool来设置是否隐藏.比如,想从三个Windows 9x系统的第三个启动,可以这样:

```
parttool hd0,1 hidden+ boot-
parttool hd0,2 hidden+ boot-
parttool hd0,3 hidden- boot+
set root=hd0,3
chainloader +1
boot

```

## 使用应急命令行

请先阅读[#使用GRUB命令行](#.E4.BD.BF.E7.94.A8GRUB.E5.91.BD.E4.BB.A4.E8.A1.8C).如果无法进入命令行,请尝试使用Live CD或者其他rescue磁盘引导,然后修正错误.不过有些时候我们手上没有此类rescue磁盘,这时,应急命令行(rescue console)就可以派上用场了.

GRUB应急命令行里可用的命令有`insmod`, `ls`, `set`, `unset`.可以使用set/unset修改变量,使用insmod来载入模组.

首先,用户必须知道启动分区(`/boot`所在位置然后设置:

```
grub rescue> set prefix=(hdX,Y)/boot/grub

```

通过加载`linux`模组来扩展命令行的功能:

```
grub rescue> insmod (hdX,Y)/boot/grub/linux.mod

```

**Note:** 如果/boot是在单独的分区上,请从路径中移除/boot.(即. 输入 `set prefix=(hdX,Y)/grub` 然后`insmod (hdX,Y)/grub/linux.mod`)

这个模组会启动对我们熟悉的`linux` 和 `initrd` 命令的支持 (请参考[#配置](#.E9.85.8D.E7.BD.AE)).

比如:

```
set root=(hd0,5)
linux /boot/vmlinuz-linux root=/dev/sda5
initrd /boot/initramfs-linux.img
boot

```

如果/boot在单独分区上:

```
set root=(hd0,5)
linux /vmlinuz-linux root=/dev/sda6
initrd /initramfs-linux.img
boot

```

成功启动Arch后,用户可以修正配置的错误或者重新安装GRUB.

关于修正配置和重新安装GRUB,请参考[#配置](#.E9.85.8D.E7.BD.AE)和[#安装](#.E5.AE.89.E8.A3.85)章节.

## 使用UUID的基础脚本

如果你想要使用UUID来避免不可靠的BIOS设备命名或者正在研究GRUB语法,这里有个使用UUID的示例性的启动项配置脚本.如果你想要将其移植到自己的系统上,只需要修改UUID就行了.这个例子假设系统的boot和root文件系统是在不同的分区上.如果你还有其他分区,请做相应修改.

```
 menuentry "Arch Linux 64" {
         # Set the UUIDs for your boot and root partition respectively
         set the_boot_uuid=ece0448f-bb08-486d-9864-ac3271bd8d07
         set the_root_uuid=c55da16f-e2af-4603-9e0b-03f5f565ec4a

         # (Note: This may be the same as your boot partition)

         # Get the boot/root devices and set them in the root and grub_boot variables
         search --fs-uuid $the_root_uuid --set=root
         search --fs-uuid $the_boot_uuid --set=grub_boot

         # Check to see if boot and root are equal.
         # If they are, then append /boot to $grub_boot (Since $grub_boot is actually the root partition)
         if [ $the_boot_uuid == $the_root_uuid ] ; then
             set grub_boot=($grub_boot)/boot
         else
             set grub_boot=($grub_boot)
         fi

         # $grub_boot now points to the correct location, so the following will properly find the kernel and initrd
         linux $grub_boot/vmlinuz-linux root=/dev/disk/by-uuid/$the_root_uuid ro
         initrd $grub_boot/initramfs-linux.img
 }

```

## 异常处理

### Intel BIOS不能引导GPT

一些Intel的BIOS要求至少要一个可启动的分区(MBR方案下的),导致GTP方案下的分区GRUB无法启动.

可以通过fdisk来将一个GPT分区标志为'boot'((最好就设在你为GRUB创建的那个1007KiB分区上)),这样就可以绕过这个问题了:

```
1.对目标磁盘(比如/dev/sda)运行fdisk
2.按`a`键,然后选择想要设置'boot'标志的分区
3.最后按`w`键,将变更写入磁盘

```

**Note:** 必须使用fdisk或者类似于它的工具来设置'boot flag',不能用Gparted等,因为它们不会在MBR里面设置'boot flag'.

请参考 [http://www.rodsbooks.com/gdisk/bios.html](http://www.rodsbooks.com/gdisk/bios.html%7C)

### 启用调试信息

在`grub.cfg`里添加:

```
set pager=1
set debug=all

```

### "No suitable mode found" error

启动时可能出现如下提示信息:

```
error: no suitable mode found
Booting however

```

然后你需要以合适的视频模式(`gfxmode`)启动 GRUB 图形化终端(`gfxterm`).视频模式由GRUB通过'gfxpayload'变量传递给linux内核.在UEFI系统下,如果没有初始化视频模式的值,终端上就不会显示内核启动消息(至少直到KMS开始运行)

将`/usr/share/grub/unicode.pf2`复制到 ${GRUB_PREFIX_DIR}(`/boot/grub/` .如果GRUB UEFI安装时设定了`--boot-directory=$esp/EFI`,那么复制的目的文件夹是`$esp/EFI/grub/`:

```
# cp /usr/share/grub/unicode.pf2 ${GRUB_PREFIX_DIR}

```

如果`/usr/share/grub/unicode.pf2` 不存在, 安装[bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont), 创建 `unifont.pf2` 文件然后将其复制到 `${GRUB_PREFIX_DIR}`:

```
# grub-mkfont -o unicode.pf2 /usr/share/fonts/misc/unifont.bdf

```

然后,在`grub.cfg`文件中添加如下行: (会给linux内核传递合适的视频模式,否则你只会得到一个黑屏,虽然系统还是会启动成功) BIOS 系统:

```
insmod vbe

```

UEFI 系统:

```
insmod efi_gop
insmod efi_uga

```

在这些行后添加(BIOS&&UEFI):

```
insmod font

```

```
if loadfont ${prefix}/fonts/unicode.pf2
then
    insmod gfxterm
    set gfxmode=auto
    set gfxpayload=keep
    terminal_output gfxterm
fi

```

如果要gfxterm(图形化终端)工作正常,`${GRUB_PREFIX_DIR}`文件夹里面应该要有`unicode.pf2` .

### 出现"msdos-style"错误消息

以下错误可能出现在你将GRUB安装到VMware上时.请阅读[相关链接](https://bbs.archlinux.org/viewtopic.php?pid=581760#p581760).这种情况是因为首分区直接从MBR后开始(即第64个扇区),而不是和正常的那样有1到2M post-MBR gap.请参阅[#MBR专用指令](#MBR.E4.B8.93.E7.94.A8.E6.8C.87.E4.BB.A4)

```
grub-setup: warn: This msdos-style partition label has no post-MBR gap; embedding will not be possible!
grub-setup: warn: Embedding is not possible. GRUB can only be installed in this setup by using blocklists.
            However, blocklists are UNRELIABLE and its use is discouraged.
grub-setup: error: If you really want blocklists, use --force.

```

### GRUB UEFI 启动到了rescue shell下

如果GRUB直接就启动到了rescue shell下,而且没报错,这可能是因为`grub.cfg`丢失或者位置不对.如果GRUB UEFI 安装时设定了`--boot-directory`参数,而`grub.cfg`文件丢失,会出现这个问题.如果启动分区的分区号发生了变化(这个分区号会被直接编码到`grubx64.efi`文件中),也会出现这个问题.

### GRUB UEFI 无法被载入

下面是一个EFI启动项信息示例:

 `# efibootmgr -v` 
```
BootCurrent: 0000
Timeout: 3 seconds
BootOrder: 0000,0001,0002
Boot0000* Grub	HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\efi\grub\grub.efi)
Boot0001* Shell	HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\EfiShell.efi)
Boot0002* Festplatte	BIOS(2,0,00)P0: SAMSUNG HD204UI

```

如果启动后,屏幕直接变黑,几秒后就跳到了下一个启动项,根据[相关链接](https://bbs.archlinux.org/viewtopic.php?pid=981560#p981560)的说法是,将GRUB移动到root分区上可能会解决这个问题.必须先删除启动项,然后重建,变化如下:

```
Boot0000* Grub	HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\grub.efi)

```

### "Invalid signature"错误

如果在启动Windows时出现了"invalid signature"错误(比如在重新分区或者添加了新硬盘后),删除GRUB的磁盘mapping,然后重建:

```
# mv /boot/grub/device.map /boot/grub/device.map-old
# grub-mkconfig -o /boot/grub/grub.cfg

```

`grub-mkconfig`此时就应该生成了新的启动项了,包括Windows.确认能启动成功后,再将备份文件`/boot/grub/device.map-old`删除.

### 引导过程卡死

如果在GRUB载入内核并初始化ramdisk后引导过程卡死了,请尝试移除`add_efi_memmap`这个内核参数

### 回滚到 GRUB Legacy

*   将GRUB2相关文件改名以为备份:

```
# mv /boot/grub /boot/grub.nonfunctional

```

*   将GRUB Legacy 移回`/boot`:

```
# cp -af /boot/grub-legacy /boot/grub

```

*   恢复备份的MBR

**Warning:** 这个命令同时会恢复分区表,所以请要非常注意.

```
# dd if=/path/to/backup/first-sectors of=/dev/sdX bs=512 count=1

```

安全的方法是只恢复MBR中的启动代码:

```
# dd if=/path/to/backup/mbr-boot-code of=/dev/sdX bs=446 count=1

```

### 其他系统不能自动发现Arch Linux

有人发现有些发行版不能使用`os-prober`自动发现Arch Linux.据称先使用`/etc/lsb-release`可能会解决这个问题.相关文件和工具可以在 [官方仓库](/index.php/Official_repositories "Official repositories")的[lsb-release](https://www.archlinux.org/packages/?name=lsb-release)包中找到

## 参阅

*   官方GRUB说明 - [https://www.gnu.org/software/grub/manual/grub.html](https://www.gnu.org/software/grub/manual/grub.html)
*   Ubuntu GRUB Wiki - [https://help.ubuntu.com/community/Grub2](https://help.ubuntu.com/community/Grub2)
*   在UEFI系统上编译GRUB步骤描述- [https://help.ubuntu.com/community/UEFIBooting](https://help.ubuntu.com/community/UEFIBooting)
*   维基百科[BIOS启动分区](https://en.wikipedia.org/wiki/BIOS_Boot_partition "wikipedia:BIOS Boot partition")
*   配置GRUB的完整说明 - [http://members.iinet.net/~herman546/p20/GRUB2%20Configuration%20File%20Commands.html](http://members.iinet.net/~herman546/p20/GRUB2%20Configuration%20File%20Commands.html)