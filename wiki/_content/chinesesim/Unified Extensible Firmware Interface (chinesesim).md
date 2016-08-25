**翻译状态：** 本文是英文页面 [Unified_Extensible_Firmware_Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-08-25，点击[这里](https://wiki.archlinux.org/index.php?title=Unified_Extensible_Firmware_Interface&diff=0&oldid=447214)可以查看翻译后英文页面的改动。

[统一可扩展固件界面](http://www.uefi.org/)(Unified Extensible Firmware Interface)，简称 UEFI, 是操作系统与固件交互的新模式，提供了启动操作系统或程序的标准环境。该方式有别于传统[BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS")系统所使用的“[MBR](/index.php/MBR "MBR")”，二者启动的区别见 [Arch boot process#Firmware types](/index.php/Arch_boot_process#Firmware_types "Arch boot process")。若要配置 UEFI 引导器，详见 [Boot loaders (简体中文)](/index.php/Boot_loaders_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Boot loaders (简体中文)").

## Contents

*   [1 UEFI 发展历史](#UEFI_.E5.8F.91.E5.B1.95.E5.8E.86.E5.8F.B2)
    *   [1.1 检测 UEFI 固件架构](#.E6.A3.80.E6.B5.8B_UEFI_.E5.9B.BA.E4.BB.B6.E6.9E.B6.E6.9E.84)
    *   [1.2 Apple Mac](#Apple_Mac)
*   [2 Linux 内核中有关 UEFI 的配置选项](#Linux_.E5.86.85.E6.A0.B8.E4.B8.AD.E6.9C.89.E5.85.B3_UEFI_.E7.9A.84.E9.85.8D.E7.BD.AE.E9.80.89.E9.A1.B9)
*   [3 UEFI 变量](#UEFI_.E5.8F.98.E9.87.8F)
    *   [3.1 Linux 内核中的 UEFI 变量支持](#Linux_.E5.86.85.E6.A0.B8.E4.B8.AD.E7.9A.84_UEFI_.E5.8F.98.E9.87.8F.E6.94.AF.E6.8C.81)
        *   [3.1.1 efivarfs 和 sysfs-efivars 的不一致](#efivarfs_.E5.92.8C_sysfs-efivars_.E7.9A.84.E4.B8.8D.E4.B8.80.E8.87.B4)
    *   [3.2 UEFI 变量正常工作的需求](#UEFI_.E5.8F.98.E9.87.8F.E6.AD.A3.E5.B8.B8.E5.B7.A5.E4.BD.9C.E7.9A.84.E9.9C.80.E6.B1.82)
        *   [3.2.1 挂载 efivarfs](#.E6.8C.82.E8.BD.BD_efivarfs)
    *   [3.3 用户空间工具](#.E7.94.A8.E6.88.B7.E7.A9.BA.E9.97.B4.E5.B7.A5.E5.85.B7)
        *   [3.3.1 efibootmgr](#efibootmgr)
*   [4 UEFI Shell](#UEFI_Shell)
    *   [4.1 获取 UEFI Shell](#.E8.8E.B7.E5.8F.96_UEFI_Shell)
    *   [4.2 启动 UEFI Shell](#.E5.90.AF.E5.8A.A8_UEFI_Shell)
    *   [4.3 重要 UEFI Shell 命令](#.E9.87.8D.E8.A6.81_UEFI_Shell_.E5.91.BD.E4.BB.A4)
        *   [4.3.1 bcfg](#bcfg)
        *   [4.3.2 map](#map)
        *   [4.3.3 edit](#edit)
*   [5 UEFI Linux 硬件兼容性](#UEFI_Linux_.E7.A1.AC.E4.BB.B6.E5.85.BC.E5.AE.B9.E6.80.A7)
*   [6 UEFI 可启动介质](#UEFI_.E5.8F.AF.E5.90.AF.E5.8A.A8.E4.BB.8B.E8.B4.A8)
    *   [6.1 从 ISO 创建 UEFI 可启动 USB](#.E4.BB.8E_ISO_.E5.88.9B.E5.BB.BA_UEFI_.E5.8F.AF.E5.90.AF.E5.8A.A8_USB)
    *   [6.2 从光学介质里移除 UEFI 启动支持](#.E4.BB.8E.E5.85.89.E5.AD.A6.E4.BB.8B.E8.B4.A8.E9.87.8C.E7.A7.BB.E9.99.A4_UEFI_.E5.90.AF.E5.8A.A8.E6.94.AF.E6.8C.81)
*   [7 原生无支持情况下测试 UEFI](#.E5.8E.9F.E7.94.9F.E6.97.A0.E6.94.AF.E6.8C.81.E6.83.85.E5.86.B5.E4.B8.8B.E6.B5.8B.E8.AF.95_UEFI)
    *   [7.1 虚拟机使用 OVMF](#.E8.99.9A.E6.8B.9F.E6.9C.BA.E4.BD.BF.E7.94.A8_OVMF)
    *   [7.2 仅 BIOS 的系统使用 DUET](#.E4.BB.85_BIOS_.E7.9A.84.E7.B3.BB.E7.BB.9F.E4.BD.BF.E7.94.A8_DUET)
*   [8 疑难问题](#.E7.96.91.E9.9A.BE.E9.97.AE.E9.A2.98)
    *   [8.1 Windows 7 无法以 UEFI 模式启动](#Windows_7_.E6.97.A0.E6.B3.95.E4.BB.A5_UEFI_.E6.A8.A1.E5.BC.8F.E5.90.AF.E5.8A.A8)
    *   [8.2 Windows 改变了启动次序](#Windows_.E6.94.B9.E5.8F.98.E4.BA.86.E5.90.AF.E5.8A.A8.E6.AC.A1.E5.BA.8F)
    *   [8.3 USB 介质卡在黑屏界面](#USB_.E4.BB.8B.E8.B4.A8.E5.8D.A1.E5.9C.A8.E9.BB.91.E5.B1.8F.E7.95.8C.E9.9D.A2)
    *   [8.4 Booting 64-bit kernel on 32-bit UEFI](#Booting_64-bit_kernel_on_32-bit_UEFI)
        *   [8.4.1 使用 GRUB](#.E4.BD.BF.E7.94.A8_GRUB)
*   [9 参阅](#.E5.8F.82.E9.98.85)

## UEFI 发展历史

*   UEFI起始于Intel的EFI 1.x版。
*   从2.0版本起，一个名为UEFI论坛的公司组织接管了其开发工作，并更名为Unified EFI(统一EFI).
*   除非特别指明是EFI 1.x, EFI和UEFI均指代UEFI 2.x固件。
*   自2015年4月，UEFI 标准 2.5 是最新的版本。
*   苹果公司的EFI实现不是EFI 1.x也不是UEFI 2.x而是这两者的混合体。这类固件不被归入到任何(U)EFI规格中，因而并没有一个标准的UEFI固件。除非特别指明，以下说明可通用但部分可能会在[Apple Macs](/index.php/MacBook "MacBook")上有所不同或是会不起效。

### 检测 UEFI 固件架构

UEFI 下每一个程序，无论它是某个 OS 引导器还是某个内存测试或数据恢复的工具，都要兼容于 EFI 固件位数或体系结构。

目前主流的 UEFI 固件，包括近期的 Apple Macs，都采用了 x86_64 EFI 固件。目前还在用 IA32 即 32 位的 EFI 的已知设备只有于 2008 年前生产的 Apple Macs，一些 Intel Cloverfield 超级本和采用 EFI 1.10 固件的 Intel 服务器主板。

x86_64 EFI 不能兼容 32 位 EFI 程序。所以 UEFI 应用程序必须依固件处理器位数／体系结构编译而成。

### Apple Mac

2008年以前的 Mac 大都使用 i386-efi 固件， 2008年以后大都使用 x86_64-efi 。有能力运行 Mac OS X Snow Leopard 64位内核的 Mac 都是 x86_64 EFI 1.x 版的固件。 在 Mac OS 下输入以下命令可以找出该 Mac 的 efi 固件：

```
ioreg -l -p IODeviceTree | grep firmware-abi

```

如果命令返回 EFI32 则对应的是 i386 EFI 1.x 版本的固件，返回 EFI64 对应的则是 x86_64 EFI 1.x 版的固件. Mac 没有 UEFI 2.x 固件，Apple的 EFI 实现也不完全跟 UEFI 标准兼容。

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

1.  内核处理器的位数/架构应该与EFI处理器的位数/架构相符。
2.  内核应以 EFI 模式(通过 [EFISTUB](/index.php/EFISTUB "EFISTUB") 或 [EFI 引导器](/index.php/Boot_loaders "Boot loaders")，而不是 BIOS/CSM 或者同为 BIOS/CSM 的"bootcamp")启动。
3.  EFI 运行时服务支持应出现在内核中 (`CONFIG_EFI=y`, 运行 `zgrep CONFIG_EFI /proc/config.gz` 来核对是否共存 ).
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
5.  **Ubuntu的固件测试套件** - [https://wiki.ubuntu.com/FirmwareTestSuite/](https://wiki.ubuntu.com/FirmwareTestSuite/) - [fwts-git](https://aur.archlinux.org/packages/fwts-git/)

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
 # efibootmgr --create --disk /dev/sdX --part Y --loader /EFI/refind/refind_x64.efi --label "rEFInd Boot Manager"

```

**注意:** UEFI 使用反斜杠 `\` 作为路径分隔符 (类似于 Windows 路径)，但是官方 [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) 包使用 `-l`/`--loader` 选项时也支持 Unix 风格的路径分隔符斜杠 `/` . Efibootmgr 解析路径之前内部会把 `/` 转换为 `\`.

在上面的命令中 `/boot/efi/EFI/refind/refind_x64.efi` 转译为 `/boot/efi` 和 `/EFI/refind/refind_x64.efi` , 进一步译为 `/dev/sdX` -> 分区 `Y` -> 文件 `/EFI/refind/refind_x64.efi`.

'label' 是出现在 UEFI 启动菜单的菜单条目名。用户可随便起名，这并不影响系统启动。更多内容见 [efibootmgr GIT README](http://linux.dell.com/cgi-bin/cgit.cgi/efibootmgr.git/plain/README) .

FAT32 文件系统大小写不敏感因为它默认不使用 UTF-8 编码格式。这种情况下固件使用大写字母 'EFI' 而不是小写的 'efi', 因此 `\EFI\refind\refindx64.efi` 或 `\efi\refind\refind_x64.efi` 都没问题 (当文件系统采用 UTF-8 编码时就不同了).

## UEFI Shell

UEFI Shell 是固件的终端，可用于启动包括引导器的 UEFI 程序。除此之外， Shell也可用于采集固件和系统的各种信息，例如内存映射 (memmap), 修改启动管理器变量 (bcfg), 运行分区程序 (diskpart), 加载 UEFI 驱动，编辑文本文件 (edit), 十六进制编辑等等。

### 获取 UEFI Shell

你可从 Intel 的 Tianocore UDK/EDK2 Sourceforge.net 工程下载以 BSD 许可证发布的 UEFI Shell.

*   [uefi-shell-git](https://aur.archlinux.org/packages/uefi-shell-git/) 包 (推荐) - 为 x86_64 系统提供 x86_64 Shell 以及为 i686 系统提供 IA32 Shell - 直接从 Tianocore EDK2 最新的源码编译
*   [Precompiled UEFI Shell v2 binaries](https://github.com/tianocore/edk2/tree/master/ShellBinPkg) (may not be up-to-date)
*   [Precompiled UEFI Shell v1 binaries](https://github.com/tianocore/edk2/tree/master/EdkShellBinPkg) (not updated anymore upstream)
*   [UEFI Shell v2 binary with bcfg modified to work with UEFI pre-2.3 firmware](http://dl.dropbox.com/u/17629062/Shell2.zip) - from Clover EFI bootloader

Shell v2 在 UEFI 2.3+ 系统上表现最好，并比 Shell v1 优先推荐。Shell v1 应该在所有 UEFI 系统上有效并且与它们遵循的 UEFI 标准版本无关。更多信息见 [ShellPkg](http://sourceforge.net/apps/mediawiki/tianocore/index.php?title=ShellPkg) 和 [这封邮件](http://sourceforge.net/mailarchive/message.php?msg_id=28690732)

### 启动 UEFI Shell

部分基于华硕和 AMI Aptio x86_64 UEFI 固件的主板 (从 Sandy Bridge 起) 提供了一个叫做 `"Launch EFI Shell from filesystem device"` 的选项。对于这些主板，下载 x86_64 UEFI Shell ，复制进 EFI 系统分区，命名为 `<EFI_SYSTEM_PARTITION>/shellx64.efi` (大部分是 `/boot/efi/shellx64.efi`) .

Phoenix SecureCore Tiano UEFI 固件已内嵌 UEFI Shell, 可按 `F6`, `F11` 或 `F12` 键来启动。

**注意:** 如果你用以上方法不能启动 UEFI Shell, 创建一个 FAT32 格式的 USB 并把 `Shell.efi` 复制到 `(USB)/efi/boot/bootx64.efi`. 这个 USB 会出现在固件的启动菜单里。启动它就会启动到 UEFI Shell.

### 重要 UEFI Shell 命令

UEFI Shell 命令通常支持 `-b` 选项，它在输出的每页末尾暂停. 运行 `help -b` 来列出所有可用命令。

更多信息见 [http://software.intel.com/en-us/articles/efi-shells-and-scripting/](http://software.intel.com/en-us/articles/efi-shells-and-scripting/)

#### bcfg

`bcfg` 命令用于修改 UEFI NVRAM 条目，它能让用户改变启动条目或驱动器选项。在"UEFI Shell Specification 2.0" PDF 文档的83页 (Section 5.3) 有详细描述。

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

To add an entry to boot directly into your system without a bootloader, configure a boot option using your kernel as an [EFISTUB](/index.php/EFISTUB#UEFI_Shell "EFISTUB"):

```
Shell> bcfg boot add **N** fs**V**:\vmlinuz-linux "Arch Linux"	
Shell> bcfg boot -opt **N** "root=**/dev/sdX#** initrd=\initramfs-linux.img"

```

where `N` is the priority, `V` is the volume number of your EFI partition, and `/dev/sdX#` is your root partition.

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

#### map

`map` displays a list of device mappings i.e. the names of available file systems (`fs0`) and storage devices (`blk0`).

Before running file system commands such as `cd` or `ls`, you need to change the shell to the appropriate file system by typing its name:

```
 Shell> fs0:
 fs0:\> cd EFI/

```

#### edit

EDIT 命令提供了类似于 nano 界面的基本编辑器，但是功能略少一点。它以 UTF-8 编码并且行尾结束符兼容 LF 和 CRLF.

本例中，编辑在固件 EFI 系统分区 (`fs0:` 中 rEFInd 的 `refind.conf`

```
 Shell> edit FS0:\EFI\refind\refind.conf

```

输入 `Ctrl-E` 以获得帮助。

## UEFI Linux 硬件兼容性

主要文章见 [Unified Extensible Firmware Interface/Hardware](/index.php/Unified_Extensible_Firmware_Interface/Hardware "Unified Extensible Firmware Interface/Hardware").

## UEFI 可启动介质

### 从 ISO 创建 UEFI 可启动 USB

教程见 [USB flash installation media#BIOS and UEFI Bootable USB](/index.php/USB_flash_installation_media#BIOS_and_UEFI_Bootable_USB "USB flash installation media").

### 从光学介质里移除 UEFI 启动支持

**注意:** 本部分提及的是给 **CD/DVD only** (光学介质)而不是 USB 闪存移除 UEFI 启动支持。

大部分32位 EFI Mac 机和部分64位 EFI Mac 机无法从 UEFI(X64)+BIOS 可启动 CD/DVD 启动。如果希望使用光学介质完成安装，可能首先需要移除 UEFI 启动支持。

*   挂载官方安装介质并如前所述获取 `archisolabel` .

```
# mount -o loop *input.iso* /mnt/iso

```

*   然后重建 ISO, 使用 [libisoburn](https://www.archlinux.org/packages/?name=libisoburn) 的 `xorriso` 移除 UEFI 光学介质启动支持。确认已设置正确的 archisolabel, 例如 "ARCH_201411"或类似的:

```
$ xorriso -as mkisofs -iso-level 3 \
    -full-iso9660-filenames\
    -volid "*archisolabel*" \
    -appid "Arch Linux CD" \
    -publisher "Arch Linux <[https://www.archlinux.org](https://www.archlinux.org)>" \
    -preparer "prepared by $USER" \
    -eltorito-boot isolinux/isolinux.bin \
    -eltorito-catalog isolinux/boot.cat \
    -no-emul-boot -boot-load-size 4 -boot-info-table \
    -isohybrid-mbr "/mnt/iso/isolinux/isohdpfx.bin" \
    -output *output.iso* /mnt/iso/
```

*   把 `*output.iso*` 烧制进光学介质并照常完成安装。

## 原生无支持情况下测试 UEFI

### 虚拟机使用 OVMF

[OVMF](https://tianocore.github.io/ovmf/) 是一个 tianocore 工程用以对虚拟机支持 UEFI. OVMF 为 QEMU 包含了一个样本 UEFI 固件。

安装 [ovmf](https://www.archlinux.org/packages/?name=ovmf)，建立 OVMF (有 Secure Boot 支持), 运行如下命令:

```
$ qemu-system-x86_64 -enable-kvm -net none -m 1024 -drive file=/usr/share/ovmf/ovmf_x64.bin,format=raw,if=pflash,readonly

```

As shorter alternative, [ovmf](https://www.archlinux.org/packages/?name=ovmf) can be loaded using `-bios` parameter

```
$ qemu-system-x86_64 -enable-kvm -m 1G -bios /usr/share/ovmf/ovmf_x64.bin

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

例如你升级 Windows 后直接启动了Windows而不是选择启动菜单:

*   确定UEFI固件设置中的"安全启动"(Secure Boot) 和 [Windows 中的"快速启动"](/index.php/Dual_boot_with_Windows#Fast_Start-Up "Dual boot with Windows") 选项没有启用.
*   确定UEFI固件设置的启动顺序中Linux Boot Manager 先于 Windows Boot Manager.

**Note:** Windows 8.x+,和 Windows 10,可能会覆盖你在UEFI固件设置中设置的启动顺序并把自己设置成第一启动选项. 所以你应该知道如何修改"一次性启动选项".

你可以通过组策略和一个批处理文件(".bat")来阻止Windows更改启动设置,在Windows上这样做:

1.  以管理员身份打开命令提示符,运行 `bcdedit /enum firmware`
2.  寻找描述中带有"linux"的启动选项,例如 "Linux Boot Manager"
3.  复制带大括号的描述符, 例如 `{31d0d5f4-22ad-11e5-b30b-806e6f6e6963}`
4.  创建一个批处理文件 (例如 `bootorder.bat`) ,包含下列的内容: `bcdedit /set {fwbootmgr} DEFAULT {*这里是你在第三步中获得的描述符*}` (例如 `bcdedit /set {fwbootmgr} DEFAULT {31d0d5f4-22ad-11e5-b30b-806e6f6e6963}`).
5.  运行 *gpedit (组策略对象编辑器)* 在 *本地计算机策略 > 计算机设置 > Windows 设置 > 脚本(启动/关机)*中,选择"启动,会打开一个名为"启动选项:的对话框.
6.  添加第四步中创建的批处理文件到"脚本"列表中.

或者让Windows 启动管理器加载systemd-boot的EFI应用程序,要这样做的话在Windows上以管理员身份运行:

```
bcdedit /set {bootmgr} path \EFI\systemd\systemd-bootx64.efi

```

### USB 介质卡在黑屏界面

可能是 [KMS](/index.php/KMS "KMS") 的问题。从 USB 启动时尝试 [Disabling KMS](/index.php/Kernel_mode_setting#Disabling_modesetting "Kernel mode setting").

### Booting 64-bit kernel on 32-bit UEFI

官方 ISO ([Archiso](/index.php/Archiso "Archiso")) 和 [Archboot](/index.php/Archboot "Archboot") iso 都用 EFISTUB (通过 [systemd-boot](/index.php/Systemd-boot "Systemd-boot") 启动管理器) 来让内核以 UEFI 模式启动。这种情况下参考下文来使用 [GRUB](/index.php/GRUB "GRUB") 作为 USB 的引导器。

#### 使用 GRUB

*   如 [link](/index.php/USB_flash_installation_media#BIOS_and_UEFI_Bootable_USB "USB flash installation media") 所述创建 USB 闪存安装介质。之后按照以下步骤来使用 GRUB 替代 Gummiboot.

*   把 `<USB>/EFI/boot/loader.efi` 备份为 `<USB>/EFI/boot/gummiboot.efi`

*   [创建一个独立的 GRUB 镜像](/index.php/GRUB#GRUB_standalone "GRUB")并把它复制为 `<USB>/EFI/boot/loader.efi` 或 `EFI/boot/bootia32.efi`

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

## 参阅

*   [Wikipedia:UEFI](https://en.wikipedia.org/wiki/UEFI "wikipedia:UEFI")
*   [UEFI Forum](http://www.uefi.org/home/) - contains the official [UEFI Specifications](http://www.uefi.org/specs/) - GUID Partition Table is part of UEFI Specification
*   [UEFI boot: how does that actually work, then? - A blog post by AdamW](https://www.happyassassin.net/2014/01/25/uefi-boot-how-does-that-actually-work-then/)
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
*   [FGA: The EFI boot process](https://jdebp.eu/FGA/efi-boot-process.html)
*   [Microsoft's Windows and GPT FAQ](http://www.microsoft.com/whdc/device/storage/GPT_FAQ.mspx)
*   [Convert Windows x64 from BIOS-MBR mode to UEFI-GPT mode without Reinstall](https://gitorious.org/tianocore_uefi_duet_builds/pages/Windows_x64_BIOS_to_UEFI)
*   [Create a Linux BIOS+UEFI and Windows x64 BIOS+UEFI bootable USB drive](https://gitorious.org/tianocore_uefi_duet_builds/pages/Linux_Windows_BIOS_UEFI_boot_USB)
*   [Rod Smith - A BIOS to UEFI Transformation](http://rodsbooks.com/bios2uefi/)
*   [EFI Shells and Scripting - Intel Documentation](http://software.intel.com/en-us/articles/efi-shells-and-scripting/)
*   [UEFI Shell - Intel Documentation](http://software.intel.com/en-us/articles/uefi-shell/)
*   [UEFI Shell - bcfg command info](http://www.hpuxtips.es/?q=node/293)