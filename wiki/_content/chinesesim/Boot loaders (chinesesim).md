**翻译状态：** 本文是英文页面 [Boot Loaders](/index.php/Boot_Loaders "Boot Loaders") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-11-05，点击[这里](https://wiki.archlinux.org/index.php?title=Boot+Loaders&diff=0&oldid=397545)可以查看翻译后英文页面的改动。

启动加载器是 [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") 或 [UEFI](/index.php/UEFI "UEFI") 启动的第一个程序。负责使用正确的[内核](/index.php/Kernel_parameters "Kernel parameters")加载设备模块, 并[启动初始 RMA](/index.php/Mkinitcpio "Mkinitcpio")，开始 [启动过程](/index.php/Boot_process "Boot process")。Arch Linux 支持 [不同的 Bootloader](/index.php/Category:Boot_loaders "Category:Boot loaders")。

**Note:** 加载[Microcode](/index.php/Microcode "Microcode")更新需要调整启动加载器配置[[1]](https://www.archlinux.org/news/changes-to-intel-microcodeupdates/)

## Contents

*   [1 适用于 BIOS 和 UEFI 的启动加载器](#.E9.80.82.E7.94.A8.E4.BA.8E_BIOS_.E5.92.8C_UEFI_.E7.9A.84.E5.90.AF.E5.8A.A8.E5.8A.A0.E8.BD.BD.E5.99.A8)
    *   [1.1 GRUB](#GRUB)
    *   [1.2 Syslinux](#Syslinux)
*   [2 仅支持 UEFI 的启动加载器](#.E4.BB.85.E6.94.AF.E6.8C.81_UEFI_.E7.9A.84.E5.90.AF.E5.8A.A8.E5.8A.A0.E8.BD.BD.E5.99.A8)
    *   [2.1 Linux Kernel EFISTUB](#Linux_Kernel_EFISTUB)
        *   [2.1.1 systemd-boot](#systemd-boot)
        *   [2.1.2 rEFInd](#rEFInd)
        *   [2.1.3 Clover](#Clover)
    *   [2.2 ELILO](#ELILO)
*   [3 BIOS-only Boot Loaders](#BIOS-only_Boot_Loaders)
    *   [3.1 GRUB Legacy](#GRUB_Legacy)
    *   [3.2 LILO](#LILO)
    *   [3.3 NeoGRUB](#NeoGRUB)
*   [4 功能比较](#.E5.8A.9F.E8.83.BD.E6.AF.94.E8.BE.83)
*   [5 See also](#See_also)

## 适用于 BIOS 和 UEFI 的启动加载器

### GRUB

[GRUB](/index.php/GRUB "GRUB") 功能丰富，支持复杂场景。配置文件和 'sh' 脚本语言很类似，可以自动生成。也是Linux平台下最常用的启动加载器。

### Syslinux

[Syslinux](/index.php/Syslinux "Syslinux")目前仅能从安装分区加载文件，配置文件示例位于 [Syslinux#Examples](/index.php/Syslinux#Examples "Syslinux")。Syslinux主要用于Linux光盘的安装程序。

## 仅支持 UEFI 的启动加载器

### Linux Kernel EFISTUB

Linux 内核可以直接被 EFI 内嵌加载器加载，参阅 [EFISTUB](/index.php/EFISTUB "EFISTUB")。

#### systemd-boot

systemd 包含了一个 EFI 启动加载器，提供了一个可以启动 EFISTUB 内核的文本菜单。参阅 [systemd-boot](/index.php/Systemd-boot "Systemd-boot")。

#### rEFInd

rEFInd 是一个 UEFI 启动管理器，提供了一个可以启动 EFISTUB 内核的图形菜单。参阅 [rEFInd](/index.php/REFInd "REFInd")。

#### Clover

Clover 是一个 UEFI 启动管理器，提供了一个可以启动 EFISTUB 内核的原生分辨率的图形菜单。参阅 [Clover](/index.php/Clover "Clover")。

### ELILO

**警告:** ELILO 项目已经声明不再进行开发了，这意味者以后只修复问题而不添加新功能。参阅 [https://sourceforge.net/mailarchive/message.php?msg_id=31524008](https://sourceforge.net/mailarchive/message.php?msg_id=31524008) 。ELILO 也不被 Arch 开发人员正式支持
。

ELILO 是只支持 BIOS [LILO](/index.php/LILO "LILO") 的 UEFI 版本。它的配置文件 `elilo.conf` 与 [LILO](/index.php/LILO "LILO") 的配置文件相似。由上游编译好的二进制文件在此 [http://sourceforge.net/projects/elilo/，和](http://sourceforge.net/projects/elilo/，和) AUR 里的 [elilo-efi](https://aur.archlinux.org/packages/elilo-efi/)。

## BIOS-only Boot Loaders

**Note:** 这些启动加载器都未获得 ArchLinux 开发团队的官方支持，或者他们已经过时。

### GRUB Legacy

GRUB Legacy (也称之为 grub-0.97), is the legacy, BIOS-only branch of [GRUB](/index.php/GRUB "GRUB"). See [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy"). 旧的GRUB 0.x被称为GRUB Legacy或GRUB1，新的GRUB2则经过了重写和大革新。

### LILO

See [LILO](/index.php/LILO "LILO").

### NeoGRUB

NeoGRUB provides a means to boot Arch from the Windows boot loader without installing an additional boot loader. See [NeoGRUB](/index.php/NeoGRUB "NeoGRUB").

Booting Arch from NeoGRUB has not been tested yet from Windows 8 and/or UEFI systems.

## 功能比较

| Name | Firmware | Multi-boot | [File systems](/index.php/File_systems "File systems") | Notes |
| BIOS | [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Unified Extensible Firmware Interface (简体中文)") | [Btrfs](/index.php/Btrfs "Btrfs") | [ext4](/index.php/Ext4 "Ext4") | ReiserFS v3 | [VFAT](/index.php/VFAT "VFAT") | [XFS](/index.php/XFS "XFS") |
| [GRUB](/index.php/GRUB_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GRUB (简体中文)") | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | On BIOS/GPT configuration requires a [BIOS boot partition](/index.php/BIOS_boot_partition "BIOS boot partition"). |
| [systemd-boot](/index.php/Systemd-boot_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd-boot (简体中文)") | No | Yes | Yes | No | No | No | Yes | No | Cannot launch binaries from partitions other than [ESP](/index.php/ESP "ESP"). |
| [Syslinux](/index.php/Syslinux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Syslinux (简体中文)") | Yes | [Partial](/index.php/Syslinux#Limitations_of_UEFI_Syslinux "Syslinux") | [Partial](/index.php/Syslinux#Chainloading "Syslinux") | without: multi-device volumes, compression, encryption | without: `64bit` feature, encryption | No | Yes | v4 on [MBR](/index.php/MBR "MBR") only | No support for certain [file system](/index.php/File_system "File system") features [[2]](http://www.syslinux.org/wiki/index.php?title=Filesystem) |
| [EFISTUB](/index.php/EFISTUB "EFISTUB") | No | Yes | N/A | N/A | N/A | N/A | N/A | N/A |
| [rEFInd](/index.php/REFInd "REFInd") | No | Yes | Yes | without encryption | without encryption | without tail-packing feature | Yes | No |
| [Clover](/index.php/Clover "Clover") | emulates UEFI | Yes | Yes | No | Unknown | No | Yes | No | Main target audience is [Hackintosh](https://en.wikipedia.org/wiki/Hackintosh "wikipedia:Hackintosh") users. |
| [LILO](/index.php/LILO "LILO") | Yes | No | Unknown | Unknown | Unknown | Unknown | Unknown | MBR only [[3]](http://xfs.org/index.php/XFS_FAQ#Q:_Does_LILO_work_with_XFS.3F) | [Deprecated](https://lists.alioth.debian.org/pipermail/lilo-devel/2015-December/000083.html). Does not support [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table"). |
| [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") | Yes | No | Yes | No | No | Yes | Yes | v4 only | [Deprecated](https://www.gnu.org/software/grub/grub-legacy.html). Does not support [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table"). |
| [NeoGRUB](/index.php/NeoGRUB "NeoGRUB") | Yes | No | Yes | Unknown | Unknown | Unknown | Unknown | Unknown |

## See also

*   [Rod Smith - Managing EFI Boot Loaders for Linux](http://www.rodsbooks.com/efi-bootloaders/)
*   [Rod Smith - rEFInd, a fork or rEFIt](http://www.rodsbooks.com/refind/)
*   [Linux Kernel Documentation on EFISTUB](https://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=blob_plain;f=Documentation/x86/efi-stub.txt;hb=HEAD)
*   [Linux Kernel EFISTUB Git Commit](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=commitdiff;h=291f36325f9f252bd76ef5f603995f37e453fc60;hp=55839d515495e766605d7aaabd9c2758370a8d27)
*   [Rod Smith's page on EFISTUB](http://www.rodsbooks.com/efi-bootloaders/efistub.html)
*   [rEFInd Documentation for booting EFISTUB Kernels](http://www.rodsbooks.com/refind/linux.html)