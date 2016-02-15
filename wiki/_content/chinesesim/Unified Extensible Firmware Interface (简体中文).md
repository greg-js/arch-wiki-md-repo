**翻译状态：** 本文是英文页面 [Unified_Extensible_Firmware_Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-02-27，点击[这里](https://wiki.archlinux.org/index.php?title=Unified_Extensible_Firmware_Interface&diff=0&oldid=362674)可以查看翻译后英文页面的改动。

**统一可扩展固件界面（Unified Extensible Firmware Interface）** (或简称为UEFI) 是一种新型固件，它引入了一种新的启动系统的方式，该方式有别于传统[BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS")系统所使用的“[MBR](/index.php/MBR "MBR")启动代码”(其二者区别见 [Arch boot process#Firmware_types](/index.php/Arch_boot_process#Firmware_types "Arch boot process") )。本文介绍了 **什么是UEFI** 以及 **UEFI在Linux内核中的支持** 。若要配置 UEFI 引导器，详见 [Boot loaders](/index.php/Boot_loaders "Boot loaders").

## Contents

*   [1 UEFI 发展历史](#UEFI_.E5.8F.91.E5.B1.95.E5.8E.86.E5.8F.B2)
*   [2 UEFI 引导过程](#UEFI_.E5.BC.95.E5.AF.BC.E8.BF.87.E7.A8.8B)
    *   [2.1 UEFI 的多重引导](#UEFI_.E7.9A.84.E5.A4.9A.E9.87.8D.E5.BC.95.E5.AF.BC)
        *   [2.1.1 启动 Microsoft Windows](#.E5.90.AF.E5.8A.A8_Microsoft_Windows)
    *   [2.2 检测 UEFI 固件架构](#.E6.A3.80.E6.B5.8B_UEFI_.E5.9B.BA.E4.BB.B6.E6.9E.B6.E6.9E.84)
        *   [2.2.1 非 Mac 机](#.E9.9D.9E_Mac_.E6.9C.BA)
        *   [2.2.2 Apple Mac](#Apple_Mac)
    *   [2.3 Secure Boot](#Secure_Boot)
*   [3 Linux 内核中有关 UEFI 的配置选项](#Linux_.E5.86.85.E6.A0.B8.E4.B8.AD.E6.9C.89.E5.85.B3_UEFI_.E7.9A.84.E9.85.8D.E7.BD.AE.E9.80.89.E9.A1.B9)
*   [4 UEFI 变量](#UEFI_.E5.8F.98.E9.87.8F)
    *   [4.1 Linux 内核中的 UEFI 变量支持](#Linux_.E5.86.85.E6.A0.B8.E4.B8.AD.E7.9A.84_UEFI_.E5.8F.98.E9.87.8F.E6.94.AF.E6.8C.81)
        *   [4.1.1 efivarfs 和 sysfs-efivars 的不一致](#efivarfs_.E5.92.8C_sysfs-efivars_.E7.9A.84.E4.B8.8D.E4.B8.80.E8.87.B4)
    *   [4.2 UEFI 变量正常工作的需求](#UEFI_.E5.8F.98.E9.87.8F.E6.AD.A3.E5.B8.B8.E5.B7.A5.E4.BD.9C.E7.9A.84.E9.9C.80.E6.B1.82)
        *   [4.2.1 挂载 efivarfs](#.E6.8C.82.E8.BD.BD_efivarfs)
    *   [4.3 用户空间工具](#.E7.94.A8.E6.88.B7.E7.A9.BA.E9.97.B4.E5.B7.A5.E5.85.B7)
        *   [4.3.1 efibootmgr](#efibootmgr)
*   [5 EFI 系统分区](#EFI_.E7.B3.BB.E7.BB.9F.E5.88.86.E5.8C.BA)
    *   [5.1 GPT 磁盘分区](#GPT_.E7.A3.81.E7.9B.98.E5.88.86.E5.8C.BA)
    *   [5.2 MBR 磁盘分区](#MBR_.E7.A3.81.E7.9B.98.E5.88.86.E5.8C.BA)
    *   [5.3 RAID 上的 ESP](#RAID_.E4.B8.8A.E7.9A.84_ESP)
*   [6 UEFI Shell](#UEFI_Shell)
    *   [6.1 获取 UEFI Shell](#.E8.8E.B7.E5.8F.96_UEFI_Shell)
    *   [6.2 启动 UEFI Shell](#.E5.90.AF.E5.8A.A8_UEFI_Shell)
    *   [6.3 重要 UEFI Shell 命令](#.E9.87.8D.E8.A6.81_UEFI_Shell_.E5.91.BD.E4.BB.A4)
        *   [6.3.1 bcfg](#bcfg)
        *   [6.3.2 edit](#edit)
*   [7 UEFI Linux 硬件兼容性](#UEFI_Linux_.E7.A1.AC.E4.BB.B6.E5.85.BC.E5.AE.B9.E6.80.A7)
*   [8 UEFI 可启动介质](#UEFI_.E5.8F.AF.E5.90.AF.E5.8A.A8.E4.BB.8B.E8.B4.A8)
    *   [8.1 从 ISO 创建 UEFI 可启动 USB](#.E4.BB.8E_ISO_.E5.88.9B.E5.BB.BA_UEFI_.E5.8F.AF.E5.90.AF.E5.8A.A8_USB)
    *   [8.2 从光学介质里移除 UEFI 启动支持](#.E4.BB.8E.E5.85.89.E5.AD.A6.E4.BB.8B.E8.B4.A8.E9.87.8C.E7.A7.BB.E9.99.A4_UEFI_.E5.90.AF.E5.8A.A8.E6.94.AF.E6.8C.81)
*   [9 原生无支持情况下测试 UEFI](#.E5.8E.9F.E7.94.9F.E6.97.A0.E6.94.AF.E6.8C.81.E6.83.85.E5.86.B5.E4.B8.8B.E6.B5.8B.E8.AF.95_UEFI)
    *   [9.1 虚拟机使用 OVMF](#.E8.99.9A.E6.8B.9F.E6.9C.BA.E4.BD.BF.E7.94.A8_OVMF)
    *   [9.2 仅 BIOS 的系统使用 DUET](#.E4.BB.85_BIOS_.E7.9A.84.E7.B3.BB.E7.BB.9F.E4.BD.BF.E7.94.A8_DUET)
*   [10 疑难问题](#.E7.96.91.E9.9A.BE.E9.97.AE.E9.A2.98)
    *   [10.1 Windows 7 无法以 UEFI 模式启动](#Windows_7_.E6.97.A0.E6.B3.95.E4.BB.A5_UEFI_.E6.A8.A1.E5.BC.8F.E5.90.AF.E5.8A.A8)
    *   [10.2 Windows 改变了启动次序](#Windows_.E6.94.B9.E5.8F.98.E4.BA.86.E5.90.AF.E5.8A.A8.E6.AC.A1.E5.BA.8F)
    *   [10.3 USB 介质卡在黑屏界面](#USB_.E4.BB.8B.E8.B4.A8.E5.8D.A1.E5.9C.A8.E9.BB.91.E5.B1.8F.E7.95.8C.E9.9D.A2)
        *   [10.3.1 使用 GRUB](#.E4.BD.BF.E7.94.A8_GRUB)
*   [11 另见](#.E5.8F.A6.E8.A7.81)

## UEFI 发展历史

*   UEFI起始于Intel的EFI 1.x版。
*   从2.0版本起，一个名为UEFI论坛的公司组织接管了其开发工作，并更名为Unified EFI(统一EFI).
*   除非特别指明是EFI 1.x, EFI和UEFI均指代UEFI 2.x固件。
*   自2013年七月24日起，UEFI标准2.4 (发布于013年7月11日)是最新的版本。
*   苹果公司的EFI实现不是EFI 1.x也不是UEFI 2.x而是这两者的混合体。这类固件不被归入到任何(U)EFI规格中，因而并没有一个标准的UEFI固件。除非特别指明，以下说明可通用但部分可能会在[Apple Macs](/index.php/MacBook "MacBook")上有所不同或是会不起效。

## UEFI 引导过程

1.  系统开机 - 上电自检（Power On Self Test 或 POST）。
2.  UEFI 固件被加载，并由它初始化启动要用的硬件。
3.  固件读取其引导管理器以确定从何处（比如，从哪个硬盘及分区）加载哪个 UEFI 应用。
4.  固件按照引导管理器中的启动项目，加载UEFI 应用。
5.  已启动的 UEFI 应用还可以启动其他应用（对应于 UEFI shell 或 rEFInd 之类的引导管理器的情况）或者启动内核及initramfs（对应于GRUB之类引导器的情况），这取决于 UEFI 应用的配置。

**Note:** 在有些 UEFI 系统中，唯一可行的启动时（如果应用没有在 UEFI 启动菜单定制条目的话）加载 UEFI 应用的方法是把它放在此固定位置：`<EFI SYSTEM PARTITION>/EFI/boot/bootx64.efi` （对于 64 位的 x86 系统）

### UEFI 的多重引导

因为每个操作系统或者提供者都可以维护自己的 EFI 系统分区中的文件，同时不影响其他系统，所以 UEFI 的多重启动只是简单的运行不同的UEFI 程序，对应于特定操作系统的引导程序。这避免了依赖 chainloading 机制（通过一个[引导程序](/index.php/Boot_loaders "Boot loaders")加载另一个引导程序，来切换操作系统）。

#### 启动 Microsoft Windows

64位版本的 Windows Vista (SP1+)、Windows 7 和 Windows 8 源生支持通过 UEFI 固件引导，但是这需要将硬盘格式化为 GPT 格式。64位版本的 Windows 系统支持 UEFI-GPT 模式引导或 BIOS-MBR 模式引导，而32位版本的 Windows 系统仅支持 BIOS-MBR 模式引导。具体做法请参考论坛参考文献章节中提供的链接。查看 [[这里](http://support.microsoft.com/default.aspx?scid=kb;EN-US;2581408)] 来获得更多信息。

### 检测 UEFI 固件架构

#### 非 Mac 机

检查目录 `/sys/firmware/efi` 是否存在，如果存在表明内核已经以 UEFI 模式启动，这种情况下 UEFI 架构等同于内核架构。(例如： 32位 或者 64位)

**注意:** Intel 的 Atom 片上系统 附带32位的 UEFI (自2013年11月2日). 更多信息见 [这个页面](/index.php?title=HCL/Firmwares/UEFI&action=edit&redlink=1 "HCL/Firmwares/UEFI (page does not exist)") 。

#### Apple Mac

2008年以前的 Mac 大都使用 i386-efi 固件， 2008年以后大都使用 x86_64-efi 。有能力运行 Mac OS X Snow Leopard 64位内核的 Mac 都是 x86_64 EFI 1.x 版的固件。 在 Mac OS 下输入以下命令可以找出该 Mac 的 efi 固件：

```
ioreg -l -p IODeviceTree | grep firmware-abi

```

如果命令返回 EFI32 则对应的是 i386 EFI 1.x 版本的固件，返回 EFI64 对应的则是 x86_64 EFI 1.x 版的固件. Mac 没有 UEFI 2.x 固件，Apple的 EFI 实现也不完全跟 UEFI 标准兼容。

### Secure Boot

关于在 Linux 中 Secure Boot 的概述请参考文章 [Rodsbooks' Secure Boot](http://www.rodsbooks.com/efi-bootloaders/secureboot.html). 本节的重点在于如何在 Arch Linux 中设置安全启动。本节暂时仅介绍在开启 Secure Boot 模式的情况下启动 archiso 的步骤。因为 EFI 程序 `PreLoader.efi` 和 `HashTool.efi` 已经添加到 archiso 中，所以在开启 Secure Boot 模式的情况下启动 archiso 是可以的，将会显示一条 "Failed to Start loader...I will now execute HashTool". 的消息。要使用 HashTool 来注册 `loader.efi` 和 `vmlinuz.efi` 的 hash 值，执行如下步骤：

*   选择 `OK`
*   在 HashTool 主菜单先选择 `Enroll Hash`，再选择 `\loader.efi`，然后点击 `Yes` 确认。再选择 `Enroll Hash` 和 `archiso`，进入 archiso 目录，然后选择 `vmlinuz-efi` 并且点击 `Yes` 确认，最后点击 `Exit` 返回启动设备选择菜单。
*   在启动设备选择菜单选择 `Arch Linux archiso x86_64 UEFI CD`。

archiso 启动后会自动以 root 登陆，并且出现 shell 提示符。使用以下命令检查 archiso 是否以 Secure Boot 模式启动：

```
$ od -An -t u1 /sys/firmware/efi/efivars/SecureBoot-XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX

```

如果以 Secure Boot 模式启动，命令会返回以 **1** 结尾的五个整数，例如：

```
6  0  0  0  1

```

XXXX 部分因不同机器而各不相同。可以使用 tab 补全来获取帮助或者列出 EFI 变量。

此外，另一种方法是执行：

```
$ bootctl status

```

## Linux 内核中有关 UEFI 的配置选项

UEFI 系统所要求的 Linux 内核配置选项设置如下:

```
CONFIG_RELOCATABLE=y
CONFIG_EFI=y
CONFIG_EFI_STUB=y
CONFIG_FB_EFI=y
CONFIG_FRAMEBUFFER_CONSOLE=y

```

UEFI运行时变量支持 (**efivarfs** 文件系统 - `/sys/firmware/efi/efivars`). 该选项十分重要，因为它是使用如 `/usr/bin/efibootmgr` 的工具来操作UEFI运行时变量所必须的。下面的选项已添加进了版本3.10及以上的内核中。

```
CONFIG_EFIVAR_FS=y

```

UEFI运行时变量支持 (老式 **efivars sysfs** 接口 - `/sys/firmware/efi/vars`). 应当禁用该选项来防止同时启用 efivarfs 和 sysfs-efivars 所导致的潜在问题。

```
CONFIG_EFI_VARS=n

```

GUID 分区表 [GPT](/index.php/GPT "GPT") 配置选项 - UEFI 支持的强制需求

```
CONFIG_EFI_PARTITION=y

```

**注意:** 以上所有选项是通过 UEFI 启动 Linux 所必须的，并已在官方源的 Archlinux 内核中启用。

来自于 [https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/plain/Documentation/x86/x86_64/uefi.txt](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/plain/Documentation/x86/x86_64/uefi.txt) .

## UEFI 变量

UEFI 定义了变量，通过它们操作系统可以与固件进行交互。 UEFI 引导变量只在早期系统启动时由引导加载程序和操作系统使用。UEFI运行时变量允许操作系统来管理固件的某些设置(如UEFI引导管理器)或 UEFI Secure Boot 协议的密钥。你可通过下面的命令来获得变量列表:

```
$ efivar -l

```

### Linux 内核中的 UEFI 变量支持

Linux 内核通过两个接口来把 EFI 变量数据传递给用户空间:

*   **老式 sysfs-efivars** 接口 (CONFIG_EFI_VARS) - 由位于 `/sys/firmware/efi/vars` 的内核模块 `efivars` 生成 - 每个变量数据最大大小为1024B, 不支持 UEFI Secure Boot 变量(由于大小限制)，并再也不被上游推荐使用。现仍被上游支持但**在 Arch 官方内核中已完全禁用**。

*   **新式 efivarfs** (**EFI** **VAR**iable **F**ile**S**ystem) 接口 (CONFIG_EFIVAR_FS) - 由位于 `/sys/firmware/efi/efivars` 的 `efivarfs` 内核模块挂载使用 - 老式 sysfs-efivars 接口的替代品，不限制变量数据大小，支持 UEFI Secure Boot 变量并被上游推荐使用。在3.8版的内核中引入，新的 `efivarfs` 模块在3.10版内核中从旧的 `efivars` 内核模块中分离。

#### efivarfs 和 sysfs-efivars 的不一致

同时启用老式的 sysfs-efivars 和新式的 efivarfs 会导致数据不一致的问题(更多信息见 [https://lkml.org/lkml/2013/4/16/473](https://lkml.org/lkml/2013/4/16/473) )。由于(自从 **core/[linux](https://www.archlinux.org/packages/?name=linux)-3.11** 和 **core/[linux-lts](https://www.archlinux.org/packages/?name=linux-lts)-3.10**)老式的 sysfs-efivars 在 Arch 官方内核中已完全禁用，新式的 efivarfs 将会被继续地启用/支持下去。自2013年10月1日起，在[官方源](/index.php/%E5%AE%98%E6%96%B9%E6%BA%90 "官方源")中所有与 UEFI 变量相关的工具都支持 efivarfs.

**注意:** 作为禁用老式 sysfs-efivars 的副作用，`efi_pstore` 在 Arch 官方内核中也被禁用，因为 EFI pstore 功能依赖老式 sysfs-efivars 支持。

如果在使用任何用户空间工具访问 EFI VAR 数据前你同时开启了这两者，请禁用其中之一并重新开启另一个接口 (为了刷新数据和防止不一致) :

禁用 sysfs-efivars 并刷新 efivarfs:

```
# modprobe -r efivars

# umount /sys/firmware/efi/efivars
# modprobe -r efivarfs

# modprobe efivarfs
# mount -t efivarfs efivarfs /sys/firmware/efi/efivars

```

禁用 efivarfs 并刷新 sysfs-efivars:

```
# umount /sys/firmware/efi/efivars
# modprobe -r efivarfs

# modprobe -r efivars
# modprobe efivars

```

### UEFI 变量正常工作的需求

1.  EFI 运行时服务支持应出现在内核中 (`CONFIG_EFI=y`, 运行 `zgrep CONFIG_EFI /proc/config.gz` 来核对是否共存 ).
2.  内核处理器的位数/架构应该与EFI处理器的位数/架构相符。
3.  内核应以 EFI 模式(通过 [EFISTUB](/index.php/EFISTUB "EFISTUB") 或 [EFI 引导器](/index.php/Boot_loaders "Boot loaders")，而不是 BIOS/CSM 或者同为 BIOS/CSM 的"bootcamp")启动。
4.  EFI 运行时服务在内核命令行中**不应被禁用**，即**不应使用**内核参数 `noefi`.
5.  `efivarfs` 文件系统应被挂载在 `/sys/firmware/efi/efivars`, 否则参考下文 [#挂载 efivarfs](#.E6.8C.82.E8.BD.BD_efivarfs) 部分。
6.  `efivar` 应无错列出 (选项 `-l`) EFI 变量。参见输出内容 [#Sample_List_of_UEFI_Variables](#Sample_List_of_UEFI_Variables).

如果 EFI 变量支持在满足以上条件后仍有问题，尝试以下解决方案:

1.  如果所有的用户空间工具都不能修改 EFI 变量数据，检查 `/sys/firmware/efi/efivars/dump-*` 文件是否存在。如果是，删掉，重启，再试一次。
2.  如果上面的步骤没有解决问题，尝试以内核参数 `efi_no_storage_paranoia` 启动以禁用内核 EFI 变量存储空间来防止对 EFI 变量的写入/修改。

**注意:** `efi_no_storage_paranoia` 仅当需要时使用且不应留下作为正常启动参数。该内核参数的效果是关闭正在实施的安全保护，来避免 NVRAM 过满时机器故障。

#### 挂载 efivarfs

如果 `efivarfs` 启动时并没有被 [systemd](/index.php/Systemd "Systemd") 自动挂载在 `/sys/firmware/efi/efivars`, 你需要手动挂载来把 EFI 变量支持传递给像 `efibootmgr` 等的用户空间工具:

```
# mount -t efivarfs efivarfs /sys/firmware/efi/efivars

```

**注意:** 这个命令即使要运行的话也要在 **chroot** 之外(之前)和之内都运行一次。

如下通过 `/etc/fstab` 来自动挂载 `efivarfs` 也是极好的:

 `/etc/fstab` 

```
efivarfs    /sys/firmware/efi/efivars    efivarfs    defaults    0    0

```

### 用户空间工具

只有少量工具能够访问/修改 UEFI 变量，即

1.  **efivar** - 操作 UEFI 变量的库和工具 (被 efibootmgr 用到) - [https://github.com/vathpela/efivar](https://github.com/vathpela/efivar) - [efivar](https://www.archlinux.org/packages/?name=efivar) 或 [efivar-git](https://aur.archlinux.org/packages/efivar-git/)
2.  **efibootmgr** - 操作 UEFI 固件启动管理器设置的工具- [https://github.com/vathpela/efibootmgr](https://github.com/vathpela/efibootmgr) - [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) 或 [efibootmgr-git](https://aur.archlinux.org/packages/efibootmgr-git/)
3.  **uefivars** - 转储 UEFI 变量和 PCI 相关信息 (内部使用 efibootmgr 源码) - [https://github.com/fpmurphy/Various/tree/master/uefivars-2.0](https://github.com/fpmurphy/Various/tree/master/uefivars-2.0) 仅支持 efivarfs ，以及 [https://github.com/fpmurphy/Various/tree/master/uefivars-1.0](https://github.com/fpmurphy/Various/tree/master/uefivars-1.0) 仅支持 sysfs-efivars . AUR 软件包 [uefivars-git](https://aur.archlinux.org/packages/uefivars-git/)
4.  **efitools** - 创建与设置自己的 UEFI Secure Boot 证书，密钥和签名过的程序的工具 (需要 efivarfs) - [efitools-git](https://aur.archlinux.org/packages/efitools-git/)
5.  **Ubuntu的固件测试套件** - [https://wiki.ubuntu.com/FirmwareTestSuite/](https://wiki.ubuntu.com/FirmwareTestSuite/) - [fwts](https://aur.archlinux.org/packages/fwts/) (以及 [fwts-efi-runtime-dkms](https://aur.archlinux.org/packages/fwts-efi-runtime-dkms/)) 或 [fwts-git](https://aur.archlinux.org/packages/fwts-git/)

#### efibootmgr

**注意:**

*   如果 `efibootmgr` 完全无效，你可以重启进入 UEFI Shell v2 使用 `bcfg` 命令来给引导器创建一个启动条目。
*   如果你不能使用 `efibootmgr`, 某些 UEFI 固件允许用户用内建的启动时界面管理启动条目。例如，某些华硕机有 "Add New Boot Option" 选项，能让你选择本地 EFI 系统分区并手动进入 EFI 存根位置 (例如 `\EFI\refind\refind_x64.efi`).
*   下面的命令用 [refind-efi](https://www.archlinux.org/packages/?name=refind-efi) 引导器作为例子。

假设要启动的引导器文件是 `/boot/efi/EFI/refind/refind_x64.efi`, `/boot/efi/EFI/refind/refind_x64.efi` 可被分拆为 `/boot/efi` 和 `/EFI/refind/refind_x64.efi`, 其中 `/boot/efi` 是 EFI 系统分区的挂载点，假设是 `/dev/sdXY` (在这里 `X` 和 `Y` 只是真实值的占位符 - 例如:- 位于 `/dev/sda1` , `X==a` `Y==1`).

为确定 EFI 系统分区的设备路径 (此例假设挂载点是 `/boot/efi`) (应为 `/dev/sdXY` 形式), 尝试:

```
# findmnt /boot/efi
TARGET SOURCE  FSTYPE OPTIONS
/boot/efi  /dev/sdXY  vfat         rw,flush,tz=UTC

```

检查内核中的 UEFI 变量支持是否正常运行:

```
# efivar -l

```

如果 efivar 无错列出变量，那么你可以开始了。如果不是，检查 [#Requirements for UEFI Variables support to work properly](#Requirements_for_UEFI_Variables_support_to_work_properly) 中的要求是否全部满足。

然后用 efibootmgr 如下创建启动条目:

```
# efibootmgr -c -d /dev/sdX -p Y -l /EFI/refind/refind_x64.efi -L "rEFInd"

```

**注意:** UEFI 使用反斜杠 `\` 作为路径分隔符 (类似于 Windows 路径)，但是官方 [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) 包使用 `-l` 选项时也支持 Unix 风格的路径分隔符斜杠 `/` . Efibootmgr 解析路径之前内部会把 `/` 转换为 `\` . 有关纳入此功能的 git 评论是 [http://linux.dell.com/cgi-bin/cgit.cgi/efibootmgr.git/commit/?id=f38f4aaad1dfa677918e417c9faa6e3286411378](http://linux.dell.com/cgi-bin/cgit.cgi/efibootmgr.git/commit/?id=f38f4aaad1dfa677918e417c9faa6e3286411378) .

在上面的命令中 `/boot/efi/EFI/refind/refind_x64.efi` 转译为 `/boot/efi` 和 `/EFI/refind/refind_x64.efi` , 进一步译为 `/dev/sdX` -> 分区 `Y` -> 文件 `/EFI/refind/refind_x64.efi`.

'label' 是出现在 UEFI 启动菜单的菜单条目名。用户可随便起名，这并不影响系统启动。更多内容见 [efibootmgr GIT README](http://linux.dell.com/cgi-bin/cgit.cgi/efibootmgr.git/plain/README) .

FAT32 文件系统大小写不敏感因为它默认不使用 UTF-8 编码格式。这种情况下固件使用大写字母 'EFI' 而不是小写的 'efi', 因此 `\EFI\refind\refindx64.efi` 或 `\efi\refind\refind_x64.efi` 都没问题 (当文件系统采用 UTF-8 编码时就不同了).

## EFI 系统分区

EFI 系统分区(也称为 ESP 或者 EFISYS)是一个 FAT32 格式的物理分区 (在硬盘主分区表上，而不是 LVM 或软件 RAID 等等) ，从这里 UEFI 固件启动 UEFI 引导器和应用程序。

它与操作系统无关而是作为 EFI 固件要启动的引导器和应用程序的存储空间，是 UEFI 启动所必须。它的分区类型应该是 EFI 系统分区 (见 [#GPT_partitioned_disks](#GPT_partitioned_disks)). 推荐 ESP 大小为 512 MiB 尽管大一点小一点都没问题 (见下面的注意)。更多信息见 [Wikipedia:EFI System partition](https://en.wikipedia.org/wiki/EFI_System_partition "wikipedia:EFI System partition").

**注意:**

*   推荐使用 GPT 和 UEFI 搭配因为有的 UEFI 固件不支持 UEFI-MBR 启动。
*   在 [GNU Parted](/index.php/GNU_Parted "GNU Parted") 中， `boot` 参数 (不要与 `legacy_boot` 参数搞混了) 在 MBR 和 GPT 盘上作用不同。在 MBR 硬盘上，它标识分区为活动分区。在 GPT 硬盘上，它把分区编码改为 `EFI System Partition` 类型。 [Parted](/index.php/Parted "Parted") 没有在 MBR 上标识 ESP 的参数 (尽管可以通过 fdisk 完成)。
*   Microsoft 文献注解了 ESP 大小: 对高级格式化 (Advanced Format) 4K 本地驱动器 (每扇区4KB) 来说，由于 FAT32 文件格式的限制，最小为 260 MB。 FAT32 的最小分区大小可由扇区大小 (4KB) x 65527 = 算出 256 MB。高级格式化 512e 驱动器不受此限制影响，因为其虚拟扇区是 512B. 512 bytes x 65527 = 32 MB, 这比 100 MB 最小限制还要小。[[1]](http://technet.microsoft.com/en-us/library/hh824839.aspx#DiskPartitionRules)
*   为防止 [EFISTUB](/index.php/EFISTUB "EFISTUB"), 内核以及 initramfs 文件应储存在 EFI 系统分区。精简起见，当以 EFISTUB 启动时你可以把 ESP 当做 `/boot` 分区而不是单独分一个 `/boot` 分区。

### GPT 磁盘分区

*   **fdisk**/**gdisk**: 创建类型为 EFI System (`EFI System` (在 _fdisk_ 中) 或 `ef00` (在 _gdisk_ 中)的分区。然后运行 `mkfs.fat -F32 /dev/<THAT_PARTITION>` 格式化为 FAT32 格式。

(或)

*   [GNU Parted](/index.php/GNU_Parted "GNU Parted"): 创建一个 FAT32 分区然后在 Parted 中为那个分区设置/激活 `boot` 参数 (不是 `legacy_boot` 参数).

**注意:** 如果你收到消息 `WARNING: Not enough clusters for a 32 bit FAT!`, 运行 `mkfs.fat -s2 -F32 ...` 或 `-s1` 以减小簇大小，否则 UEFI 无法读取分区。

### MBR 磁盘分区

*   **fdisk**: 使用 fdisk 创建类型为 _EFI System_ 的分区，然后运行 `mkfs.fat -F32 /dev/<THAT_PARTITION>` 格式化为 FAT32.

### RAID 上的 ESP

将 ESP 包含进 RAID1 组是可行的，但是会有数据污染的危险，创建 ESP 时请三思。 细节见 [https://bbs.archlinux.org/viewtopic.php?pid=1398710#p1398710](https://bbs.archlinux.org/viewtopic.php?pid=1398710#p1398710) 和 [https://bbs.archlinux.org/viewtopic.php?pid=1390741#p1390741](https://bbs.archlinux.org/viewtopic.php?pid=1390741#p1390741) .

## UEFI Shell

UEFI Shell 是固件的终端，可用于启动包括引导器的 UEFI 程序。除此之外， Shell也可用于采集固件和系统的各种信息，例如内存映射 (memmap), 修改启动管理器变量 (bcfg), 运行分区程序 (diskpart), 加载 UEFI 驱动，编辑文本文件 (edit), 十六进制编辑等等。

### 获取 UEFI Shell

你可从 Intel 的 Tianocore UDK/EDK2 Sourceforge.net 工程下载以 BSD 许可证发布的 UEFI Shell.

*   [AUR](/index.php/AUR "AUR") **[uefi-shell-svn](https://aur.archlinux.org/packages/uefi-shell-svn/)** 包 (推荐) - 为 x86_64 系统提供 x86_64 Shell 以及为 i686 系统提供 IA32 Shell - 直接从 Tianocore EDK2 SVN 最新的源码编译
*   [Precompiled x86_64 UEFI Shell v2 binary](https://svn.code.sf.net/p/edk2/code/trunk/edk2/ShellBinPkg/UefiShell/X64/Shell.efi) (可能不是最新)
*   [Precompiled x86_64 UEFI Shell v1 binary](https://svn.code.sf.net/p/edk2/code/trunk/edk2/EdkShellBinPkg/FullShell/X64/Shell_Full.efi) (上游再也不更新了)
*   [Precompiled IA32 UEFI Shell v2 binary](https://svn.code.sf.net/p/edk2/code/trunk/edk2/ShellBinPkg/UefiShell/Ia32/Shell.efi) (可能不是最新)
*   [Precompiled IA32 UEFI Shell v1 binary](https://svn.code.sf.net/p/edk2/code/trunk/edk2/EdkShellBinPkg/FullShell/Ia32/Shell_Full.efi) (上游再也不更新了)

Shell v2 在 UEFI 2.3+ 系统上表现最好，并比 Shell v1 优先推荐。Shell v1 应该在所有 UEFI 系统上有效并且与它们遵循的 UEFI 标准版本无关。更多信息见 [ShellPkg](http://sourceforge.net/apps/mediawiki/tianocore/index.php?title=ShellPkg) 和 [这封邮件](http://sourceforge.net/mailarchive/message.php?msg_id=28690732)

### 启动 UEFI Shell

部分基于华硕和 AMI Aptio x86_64 UEFI 固件的主板 (从 Sandy Bridge 起) 提供了一个叫做 `"Launch EFI Shell from filesystem device"` 的选项。对于这些主板，下载 x86_64 UEFI Shell ，复制进 EFI 系统分区，命名为 `<EFI_SYSTEM_PARTITION>/shellx64.efi` (大部分是 `/boot/efi/shellx64.efi`) .

Phoenix SecureCore Tiano UEFI 固件已内嵌 UEFI Shell, 可按 `F6`, `F11` 或 `F12` 键来启动。

**注意:** 如果你用以上方法不能启动 UEFI Shell, 创建一个 FAT32 格式的 USB 并把 `Shell.efi` 复制到 `(USB)/efi/boot/bootx64.efi`. 这个 USB 会出现在固件的启动菜单里。启动它就会启动到 UEFI Shell.

### 重要 UEFI Shell 命令

UEFI Shell 命令通常支持 `-b` 选项，它在输出的每页末尾暂停。 `map` 能列出识别出的文件系统 (`fs0`, ...) 和存储设备 (`blk0`, ...). 运行 `help -b` 来列出所有可用命令。

更多信息见 [http://software.intel.com/en-us/articles/efi-shells-and-scripting/](http://software.intel.com/en-us/articles/efi-shells-and-scripting/)

#### bcfg

BCFG 命令用于修改 UEFI NVRAM 条目，它能让用户改变启动条目或驱动器选项。在"UEFI Shell Specification 2.0" PDF 文档的83页 (Section 5.3) 有详细描述。

**注意:**

*   仅当 `efibootmgr` 无法创建启动条目时才推荐尝试 `bcfg`.
*   UEFI Shell v1 官方二进制文件不支持 `bcfg` 命令。你可以下载一个 [modified UEFI Shell v2 二进制文件](http://dl.dropbox.com/u/17629062/Shell2.zip)，它在 UEFI 2.3前的固件有效。

转储当前启动条目:

```
Shell> bcfg boot dump -v

```

为 rEFInd (作为例子) 添加一个启动菜单条目，在启动菜单里是第4个 (从0开始计数) 选项:

```
Shell> bcfg boot add 3 fs0:\EFI\refind\refind_x64.efi "rEFInd"

```

`fs0:` 映射到 EFI 系统分区，`fs0:\EFI\refind\refind_x64.efi` i是要启动的文件。

删除第4个启动选项:

```
Shell> bcfg boot rm 3

```

把第3个启动选项移动到第0 (也就是说第1个是 UEFI 启动菜单的默认启动选项):

```
Shell> bcfg boot mv 3 0

```

bcfg 帮助文档:

```
Shell> help bcfg -v -b

```

或:

```
Shell> bcfg -? -v -b

```

#### edit

EDIT 命令提供了类似于 nano 界面的基本编辑器，但是功能略少一点。它以 UTF-8 编码并且行尾结束符兼容 LF 和 CRLF.

本例中，编辑在固件 EFI 系统分区 (`fs0:` 中 rEFInd 的 `refind.conf`

```
Shell> fs0:
FS0:\> cd \EFI\arch\refind
FS0:\EFI\arch\refind\> edit refind.conf

```

输入 `Ctrl-E` 以获得帮助。

## UEFI Linux 硬件兼容性

主要文章见 [HCL/Firmwares/UEFI](/index.php?title=HCL/Firmwares/UEFI&action=edit&redlink=1 "HCL/Firmwares/UEFI (page does not exist)").

## UEFI 可启动介质

### 从 ISO 创建 UEFI 可启动 USB

教程见 [USB flash installation media#BIOS and UEFI Bootable USB](/index.php/USB_flash_installation_media#BIOS_and_UEFI_Bootable_USB "USB flash installation media").

### 从光学介质里移除 UEFI 启动支持

**注意:** 本部分提及的是给 **CD/DVD only** (光学介质)而不是 USB 闪存移除 UEFI 启动支持。

大部分32位 EFI Mac 机和部分64位 EFI Mac 机无法从 UEFI(X64)+BIOS 可启动 CD/DVD 启动。如果希望使用光学介质完成安装，可能首先需要移除 UEFI 启动支持。

*   挂载官方安装介质并如前所述获取 `archisolabel` .

```
# mount -o loop _input.iso_ /mnt/iso

```

*   然后重建 ISO, 使用 [libisoburn](https://www.archlinux.org/packages/?name=libisoburn) 的 `xorriso` 移除 UEFI 光学介质启动支持。确认已设置正确的 archisolabel, 例如 "ARCH_201411"或类似的:

```
$ xorriso -as mkisofs -iso-level 3 \
    -full-iso9660-filenames\
    -volid "_archisolabel_" \
    -appid "Arch Linux CD" \
    -publisher "Arch Linux <[https://www.archlinux.org](https://www.archlinux.org)>" \
    -preparer "prepared by $USER" \
    -eltorito-boot isolinux/isolinux.bin \
    -eltorito-catalog isolinux/boot.cat \
    -no-emul-boot -boot-load-size 4 -boot-info-table \
    -isohybrid-mbr "/mnt/iso/isolinux/isohdpfx.bin" \
    -output _output.iso_ /mnt/iso/
```

*   把 `_output.iso_` 烧制进光学介质并照常完成安装。

## 原生无支持情况下测试 UEFI

### 虚拟机使用 OVMF

[OVMF](https://tianocore.github.io/ovmf/) 是一个 tianocore 工程用以对虚拟机支持 UEFI. OVMF 为 QEMU 包含了一个样本 UEFI 固件。

你可从 AUR [ovmf-svn](https://aur.archlinux.org/packages/ovmf-svn/) 建立 OVMF (有 Secure Boot 支持), 运行如下命令:

```
$ qemu-system-x86_64 -enable-kvm -net none -m 1024 -pflash /usr/share/ovmf/x86_64/bios.bin

```

### 仅 BIOS 的系统使用 DUET

DUET 是一个 tianocore 工程用以从 BIOS 启动到完整 UEFI 环境，这与 BIOS 启动操作系统相似。在 [http://www.insanelymac.com/forum/topic/186440-linux-and-windows-uefi-boot-using-tianocore-duet-firmware/](http://www.insanelymac.com/forum/topic/186440-linux-and-windows-uefi-boot-using-tianocore-duet-firmware/) 里有广泛讨论。预建立的 DUET 镜像可从其中一个源 [https://gitorious.org/tianocore_uefi_duet_builds](https://gitorious.org/tianocore_uefi_duet_builds) 下载。教程见 [https://gitorious.org/tianocore_uefi_duet_builds/tianocore_uefi_duet_installer/blobs/raw/master/Migle_BootDuet_INSTALL.txt](https://gitorious.org/tianocore_uefi_duet_builds/tianocore_uefi_duet_installer/blobs/raw/master/Migle_BootDuet_INSTALL.txt).

也可考虑 [http://sourceforge.net/projects/cloverefiboot/](http://sourceforge.net/projects/cloverefiboot/) , 它提供的 DUET 镜像可能包含了一些系统的专用补丁，并且比 gitorious 源更新得更频繁。

## 疑难问题

### Windows 7 无法以 UEFI 模式启动

如果你把 Windows 安装进了另一个 GPT 格式的硬盘并且你电脑里还有一个 MBR 格式的硬盘，那么可能 UEFI 固件启动了 CSM 支持(为从 MBR 分区启动的支持) 因而 Windows 无法启动。为解决问题，把 MBR 硬盘的内容合并到 GPT 硬盘中并禁用 MBR 硬盘使用的 SATA 接口或者直接把硬盘拔下来。

有此类问题的主板:

Gigabyte Z77X-UD3H rev. 1.1 (UEFI 版本 F19e)

- 固件启动选项 "UEFI Only" 并不妨碍以 CSM 启动。

### Windows 改变了启动次序

某些主板上 (ASRock Z77 Extreme4 确认有此问题) Windows 8 每次启动时改变了 NVRAM 中的启动次序。解决方式是让 Windows Boot Manager 加载另一引导器而不是启动 Windows. Windows 下以管理员模式执行如下命令:

```
bcdedit /set {bootmgr} path \EFI\boot_app_dir\boot_app.efi

```

### USB 介质卡在黑屏界面

*   也可能是 [KMS](/index.php/KMS "KMS") 的问题。从 USB 启动时尝试 [Disabling KMS](/index.php/Kernel_mode_setting#Disabling_modesetting "Kernel mode setting").

*   如果不是 KMS 的问题，那么可能是 [EFISTUB](/index.php/EFISTUB "EFISTUB") 启动的 bug (更多信息见 [[2]](https://bugs.archlinux.org/task/33745) and [[3]](https://bbs.archlinux.org/viewtopic.php?id=156670) ). 官方 ISO ([Archiso](/index.php/Archiso "Archiso")) 和 [Archboot](/index.php/Archboot "Archboot") iso 都用 EFISTUB (通过 [Gummiboot](/index.php/Gummiboot "Gummiboot") 启动管理器) 来让内核以 UEFI 模式启动。这种情况下参考下文来使用 [GRUB](/index.php/GRUB "GRUB") 作为 USB 的引导器。

#### 使用 GRUB

*   如 [link](/index.php/USB_flash_installation_media#BIOS_and_UEFI_Bootable_USB "USB flash installation media") 所述创建 USB 闪存安装介质。之后按照以下步骤来使用 GRUB 替代 Gummiboot.

*   把 `<USB>/EFI/boot/loader.efi` 备份为 `<USB>/EFI/boot/gummiboot.efi`

*   [创建一个独立的 GRUB 镜像](/index.php/GRUB#GRUB_Standalone "GRUB")并把它复制为 `<USB>/EFI/boot/loader.efi`

*   按如下内容创建 `<USB>/EFI/boot/grub.cfg` (替换 `ARCH_YYYYMM` 为 USB 盘，例如 `ARCH_201404`):

 `grub.cfg for Official ISO` 

```
insmod part_gpt
insmod part_msdos
insmod fat

insmod efi_gop
insmod efi_uga
insmod video_bochs
insmod video_cirrus

insmod font

if loadfont "${prefix}/fonts/unicode.pf2" ; then
    insmod gfxterm
    set gfxmode="1024x768x32;auto"
    terminal_input console
    terminal_output gfxterm
fi

menuentry "Arch Linux archiso x86_64" {
    set gfxpayload=keep
    search --no-floppy --set=root --label ARCH_YYYYMM
    linux /arch/boot/x86_64/vmlinuz archisobasedir=arch archisolabel=ARCH_YYYYMM add_efi_memmap
    initrd /arch/boot/x86_64/archiso.img
}

menuentry "UEFI Shell x86_64 v2" {
    search --no-floppy --set=root --label ARCH_YYYYMM
    chainloader /EFI/shellx64_v2.efi
}

menuentry "UEFI Shell x86_64 v1" {
    search --no-floppy --set=root --label ARCH_YYYYMM
    chainloader /EFI/shellx64_v1.efi
}

```

 `grub.cfg for Archboot ISO` 

```
insmod part_gpt
insmod part_msdos
insmod fat

insmod efi_gop
insmod efi_uga
insmod video_bochs
insmod video_cirrus

insmod font

if loadfont "${prefix}/fonts/unicode.pf2" ; then
    insmod gfxterm
    set gfxmode="1024x768x32;auto"
    terminal_input console
    terminal_output gfxterm
fi

menuentry "Arch Linux x86_64 Archboot" {
    set gfxpayload=keep
    search --no-floppy --set=root --file /boot/vmlinuz_x86_64
    linux /boot/vmlinuz_x86_64 cgroup_disable=memory loglevel=7 add_efi_memmap
    initrd /boot/initramfs_x86_64.img
}

menuentry "UEFI Shell x86_64 v2" {
    search --no-floppy --set=root --file /boot/vmlinuz_x86_64
    chainloader /EFI/tools/shellx64_v2.efi
}

menuentry "UEFI Shell x86_64 v1" {
    search --no-floppy --set=root --file /boot/vmlinuz_x86_64
    chainloader /EFI/tools/shellx64_v1.efi
}

```

## 另见

*   [Wikipedia:UEFI](https://en.wikipedia.org/wiki/UEFI "wikipedia:UEFI")
*   [UEFI Forum](http://www.uefi.org/home/) - contains the official [UEFI Specifications](http://www.uefi.org/specs/) - GUID Partition Table is part of UEFI Specification
*   [UEFI boot: how does that actually work, then? - A blog post by AdamW](https://www.happyassassin.net/2014/01/25/uefi-boot-how-does-that-actually-work-then/)
*   [Wikipedia:EFI System partition](https://en.wikipedia.org/wiki/EFI_System_partition "wikipedia:EFI System partition")
*   [The EFI System Partition and the Default Boot Behavior](http://blog.uncooperative.org/blog/2014/02/06/the-efi-system-partition/)
*   [Linux Kernel x86_64 UEFI Documentation](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/plain/Documentation/x86/x86_64/uefi.txt)
*   [Intel's page on EFI](http://www.intel.com/technology/efi/)
*   [Intel UEFI Community Resource Center](http://uefidk.intel.com/)
*   [Matt Fleming - The Linux EFI Boot Stub](http://uefidk.intel.com/blog/linux-efi-boot-stub)
*   [Matt Fleming - Accessing UEFI Variables from Linux](http://uefidk.intel.com/blog/accessing-uefi-variables-linux)
*   [Rod Smith - Linux on UEFI: A Quick Installation Guide](http://www.rodsbooks.com/linux-uefi/)
*   [UEFI Boot problems on some newer machines (LKML)](https://lkml.org/lkml/2011/6/8/322)
*   [LPC 2012 Plumbing UEFI into Linux](http://linuxplumbers.ubicast.tv/videos/plumbing-uefi-into-linux/)
*   [LPC 2012 UEFI Tutorial : part 1](http://linuxplumbers.ubicast.tv/videos/uefi-tutorial-part-1/)
*   [LPC 2012 UEFI Tutorial : part 2](http://linuxplumbers.ubicast.tv/videos/uefi-tutorial-part-2/)
*   [Intel's Tianocore Project](http://sourceforge.net/apps/mediawiki/tianocore/index.php?title=Welcome_to_TianoCore) for Open-Source UEFI firmware which includes DuetPkg for direct BIOS based booting and OvmfPkg used in QEMU and Oracle VirtualBox
*   [FGA: The EFI boot process](http://homepage.ntlworld.com/jonathan.deboynepollard/FGA/efi-boot-process.html)
*   [Microsoft's Windows and GPT FAQ](http://www.microsoft.com/whdc/device/storage/GPT_FAQ.mspx)
*   [Convert Windows x64 from BIOS-MBR mode to UEFI-GPT mode without Reinstall](https://gitorious.org/tianocore_uefi_duet_builds/pages/Windows_x64_BIOS_to_UEFI)
*   [Create a Linux BIOS+UEFI and Windows x64 BIOS+UEFI bootable USB drive](https://gitorious.org/tianocore_uefi_duet_builds/pages/Linux_Windows_BIOS_UEFI_boot_USB)
*   [Rod Smith - A BIOS to UEFI Transformation](http://rodsbooks.com/bios2uefi/)
*   [EFI Shells and Scripting - Intel Documentation](http://software.intel.com/en-us/articles/efi-shells-and-scripting/)
*   [UEFI Shell - Intel Documentation](http://software.intel.com/en-us/articles/uefi-shell/)
*   [UEFI Shell - bcfg command info](http://www.hpuxtips.es/?q=node/293)
*   [UEFI Shell v2 binary with bcfg modified to work with UEFI pre-2.3 firmware - from Clover efiboot](http://dl.dropbox.com/u/17629062/Shell2.zip)