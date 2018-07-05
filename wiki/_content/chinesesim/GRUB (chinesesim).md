**翻译状态：** 本文是英文页面 [GRUB](/index.php/GRUB "GRUB") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-10-16，点击[这里](https://wiki.archlinux.org/index.php?title=GRUB&diff=0&oldid=492896)可以查看翻译后英文页面的改动。

相关文章

*   [Arch boot process](/index.php/Arch_boot_process "Arch boot process")
*   [Boot loaders](/index.php/Boot_loaders "Boot loaders")
*   [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record")
*   [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")
*   [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy")
*   [GRUB/EFI examples](/index.php/GRUB/EFI_examples "GRUB/EFI examples")
*   [GRUB/Tips and tricks](/index.php/GRUB/Tips_and_tricks "GRUB/Tips and tricks")
*   [Multiboot USB drive](/index.php/Multiboot_USB_drive "Multiboot USB drive")

[GRUB](https://www.gnu.org/software/grub/) , 是下一代 GRand Unified Bootloader, 请不要和 [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy")  混淆了。它来自下一代 GRUB 研究项目 [PUPA](http://www.nongnu.org/pupa/)，代码全部重写，实现了模块化和增强了移植性。[[1]](http://www.gnu.org/software/grub/grub-faq.en.html#q1).

## Contents

*   [1 前言](#.E5.89.8D.E8.A8.80)
*   [2 BIOS 系统](#BIOS_.E7.B3.BB.E7.BB.9F)
    *   [2.1 GUID分区表(GPT)特殊操作](#GUID.E5.88.86.E5.8C.BA.E8.A1.A8.28GPT.29.E7.89.B9.E6.AE.8A.E6.93.8D.E4.BD.9C)
    *   [2.2 主引导记录(MBR)特殊操作](#.E4.B8.BB.E5.BC.95.E5.AF.BC.E8.AE.B0.E5.BD.95.28MBR.29.E7.89.B9.E6.AE.8A.E6.93.8D.E4.BD.9C)
    *   [2.3 安装](#.E5.AE.89.E8.A3.85)
*   [3 UEFI 系统](#UEFI_.E7.B3.BB.E7.BB.9F)
    *   [3.1 检查你是否使用GPT且有ESP分区](#.E6.A3.80.E6.9F.A5.E4.BD.A0.E6.98.AF.E5.90.A6.E4.BD.BF.E7.94.A8GPT.E4.B8.94.E6.9C.89ESP.E5.88.86.E5.8C.BA)
    *   [3.2 安装](#.E5.AE.89.E8.A3.85_2)
*   [4 生成主配置文件](#.E7.94.9F.E6.88.90.E4.B8.BB.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
*   [5 配置](#.E9.85.8D.E7.BD.AE)
    *   [5.1 额外的参数](#.E9.A2.9D.E5.A4.96.E7.9A.84.E5.8F.82.E6.95.B0)
    *   [5.2 多系统启动](#.E5.A4.9A.E7.B3.BB.E7.BB.9F.E5.90.AF.E5.8A.A8)
        *   [5.2.1 使用 /etc/grub.d/40_custom 和 grub-mkconfig 自动生成](#.E4.BD.BF.E7.94.A8_.2Fetc.2Fgrub.d.2F40_custom_.E5.92.8C_grub-mkconfig_.E8.87.AA.E5.8A.A8.E7.94.9F.E6.88.90)
            *   [5.2.1.1 GNU/Linux 启动项](#GNU.2FLinux_.E5.90.AF.E5.8A.A8.E9.A1.B9)
            *   [5.2.1.2 FreeBSD 启动项](#FreeBSD_.E5.90.AF.E5.8A.A8.E9.A1.B9)
                *   [5.2.1.2.1 直接加载内核](#.E7.9B.B4.E6.8E.A5.E5.8A.A0.E8.BD.BD.E5.86.85.E6.A0.B8)
                *   [5.2.1.2.2 Chainloading 嵌入的启动项](#Chainloading_.E5.B5.8C.E5.85.A5.E7.9A.84.E5.90.AF.E5.8A.A8.E9.A1.B9)
                *   [5.2.1.2.3 运行传统的 BSD 第二阶段 loader](#.E8.BF.90.E8.A1.8C.E4.BC.A0.E7.BB.9F.E7.9A.84_BSD_.E7.AC.AC.E4.BA.8C.E9.98.B6.E6.AE.B5_loader)
            *   [5.2.1.3 UEFI-GPT 模式下安装的Windows的启动项](#UEFI-GPT_.E6.A8.A1.E5.BC.8F.E4.B8.8B.E5.AE.89.E8.A3.85.E7.9A.84Windows.E7.9A.84.E5.90.AF.E5.8A.A8.E9.A1.B9)
            *   [5.2.1.4 "Shutdown" 启动项](#.22Shutdown.22_.E5.90.AF.E5.8A.A8.E9.A1.B9)
            *   [5.2.1.5 "Restart" 启动项](#.22Restart.22_.E5.90.AF.E5.8A.A8.E9.A1.B9)
            *   [5.2.1.6 在BIOS-MBR模式下安装的Microsoft Windows](#.E5.9C.A8BIOS-MBR.E6.A8.A1.E5.BC.8F.E4.B8.8B.E5.AE.89.E8.A3.85.E7.9A.84Microsoft_Windows)
        *   [5.2.2 通过EasyBCD NeoGRUB 和Windows共存](#.E9.80.9A.E8.BF.87EasyBCD_NeoGRUB_.E5.92.8CWindows.E5.85.B1.E5.AD.98)
    *   [5.3 其他选项](#.E5.85.B6.E4.BB.96.E9.80.89.E9.A1.B9)
        *   [5.3.1 LVM](#LVM)
        *   [5.3.2 阵列](#.E9.98.B5.E5.88.97)
        *   [5.3.3 root加密](#root.E5.8A.A0.E5.AF.86)
    *   [5.4 在GRUB中直接从ISO启动](#.E5.9C.A8GRUB.E4.B8.AD.E7.9B.B4.E6.8E.A5.E4.BB.8EISO.E5.90.AF.E5.8A.A8)
        *   [5.4.1 Arch ISO](#Arch_ISO)
            *   [5.4.1.1 x86_64](#x86_64)
            *   [5.4.1.2 i686](#i686)
        *   [5.4.2 Ubuntu ISO](#Ubuntu_ISO)
        *   [5.4.3 Other ISOs](#Other_ISOs)
*   [6 使用GRUB命令行](#.E4.BD.BF.E7.94.A8GRUB.E5.91.BD.E4.BB.A4.E8.A1.8C)
    *   [6.1 分页支持](#.E5.88.86.E9.A1.B5.E6.94.AF.E6.8C.81)
    *   [6.2 使用命令行引导操作系统](#.E4.BD.BF.E7.94.A8.E5.91.BD.E4.BB.A4.E8.A1.8C.E5.BC.95.E5.AF.BC.E6.93.8D.E4.BD.9C.E7.B3.BB.E7.BB.9F)
        *   [6.2.1 链式加载一个分区](#.E9.93.BE.E5.BC.8F.E5.8A.A0.E8.BD.BD.E4.B8.80.E4.B8.AA.E5.88.86.E5.8C.BA)
        *   [6.2.2 链式加载磁盘](#.E9.93.BE.E5.BC.8F.E5.8A.A0.E8.BD.BD.E7.A3.81.E7.9B.98)
        *   [6.2.3 正常载入](#.E6.AD.A3.E5.B8.B8.E8.BD.BD.E5.85.A5)
*   [7 parttool](#parttool)
*   [8 使用应急命令行](#.E4.BD.BF.E7.94.A8.E5.BA.94.E6.80.A5.E5.91.BD.E4.BB.A4.E8.A1.8C)
*   [9 异常处理](#.E5.BC.82.E5.B8.B8.E5.A4.84.E7.90.86)
    *   [9.1 Intel BIOS不能引导GPT](#Intel_BIOS.E4.B8.8D.E8.83.BD.E5.BC.95.E5.AF.BCGPT)
    *   [9.2 启用调试信息](#.E5.90.AF.E7.94.A8.E8.B0.83.E8.AF.95.E4.BF.A1.E6.81.AF)
    *   [9.3 "No suitable mode found" error](#.22No_suitable_mode_found.22_error)
    *   [9.4 出现"msdos-style"错误消息](#.E5.87.BA.E7.8E.B0.22msdos-style.22.E9.94.99.E8.AF.AF.E6.B6.88.E6.81.AF)
    *   [9.5 GRUB UEFI 启动到了rescue shell下](#GRUB_UEFI_.E5.90.AF.E5.8A.A8.E5.88.B0.E4.BA.86rescue_shell.E4.B8.8B)
    *   [9.6 GRUB UEFI 无法被载入](#GRUB_UEFI_.E6.97.A0.E6.B3.95.E8.A2.AB.E8.BD.BD.E5.85.A5)
    *   [9.7 "Invalid signature"错误](#.22Invalid_signature.22.E9.94.99.E8.AF.AF)
    *   [9.8 引导过程卡死](#.E5.BC.95.E5.AF.BC.E8.BF.87.E7.A8.8B.E5.8D.A1.E6.AD.BB)
    *   [9.9 回滚到 GRUB Legacy](#.E5.9B.9E.E6.BB.9A.E5.88.B0_GRUB_Legacy)
    *   [9.10 其他系统不能自动发现Arch Linux](#.E5.85.B6.E4.BB.96.E7.B3.BB.E7.BB.9F.E4.B8.8D.E8.83.BD.E8.87.AA.E5.8A.A8.E5.8F.91.E7.8E.B0Arch_Linux)
    *   [9.11 未找到 Windows 8/10](#.E6.9C.AA.E6.89.BE.E5.88.B0_Windows_8.2F10)
*   [10 参阅](#.E5.8F.82.E9.98.85)

## 前言

简单的说,**Boot Loader**是电脑启动时运行的第一个程序,它负责装载内核并将控制权转交。内核再初始化操作系统的其它部分。官方所称的 GRUB 是软件的第二版,即 GRUB2,请参考[[2]](https://www.gnu.org/software/grub/).

GRUB 不支持[F2FS](/index.php/F2FS "F2FS")格式的根目录,所以你需要为`/boot`分区单独设置一个支持的文件系统.

## BIOS 系统

### GUID分区表(GPT)特殊操作

BIOS/[GPT](/index.php/GPT "GPT")配置中，必须使用 [BIOS 启动分区](https://www.gnu.org/software/grub/manual/grub/html_node/BIOS-installation.html#BIOS-installation)。GRUB将`core.img`嵌入到这个分区。

**Note:**

*   在尝试分区之前请记住不是所有的系统都支持这种分区方案, 请参阅 [GUID 分区表](/index.php/Partitioning#GUID_Partition_Table "Partitioning").
*   此额外分区只在GRUB, BIOS/GPT分区方式中使用. 对于 GRUB, BIOS/MBR 分区方式, GRUB会把`core.img`放到 MBR 后面的间隙中去. 而 GPT 下不使用这个间隙是因为 GPT 分区需要满足 1M/2048 扇区的磁盘边界规范.
*   [UEFI](/index.php/UEFI "UEFI") 系统也不需要这额外分区, 因为它不需要嵌入启动扇区.UEFI 系统需要有 [ESP](/index.php/ESP "ESP") 分区。

安装 GRUB 前，在一个没有文件系统的磁盘上，用 `fdisk` 或 `gdisk` 创建一个 `+1M` 分区，设置为 `BIOS boot` 类型，在 `fdisk` 中的类型号是 `4`, 在 `gdisk` 中的类型是 `ef02`，在 `parted` 中是 `bios_grub`。此分区可以在磁盘前 2TB 的任何位置。分区建立好后，按下面的命令安装启动管理器。

GPT 后面的空间也可以用作 BIOS 启动分区，但是这会违反 GPT 对齐规范。因为这个分区不会经常访问，所以性能的影响很小。只不过有些分区工具会发出警告。在 `fdisk` 或 `gdisk` 中创建一个新分区，从 34 扇区开始，一直到 2047，然后设置类型。为了让其它分区对齐，可以最后再创建此分区。

### 主引导记录(MBR)特殊操作

一般来说,如果使用兼容 DOS 的分区对齐模式, [MBR](/index.php/MBR "MBR") 512 byte 结束位置和第一个分区之间都有 31KB 的空闲空间。不过,为了提供足够的空间嵌入GRUB的`core.img`文件,建议将这个空间设置为 1 到 2 Mib([FS#24103](https://bugs.archlinux.org/task/24103)). 建议使用支持 1 MiB分区对齐的分区软件来分区, 因为这样也能满足非512B扇区磁盘分区的需求.

### 安装

[安装](/index.php/Pacman "Pacman") 软件包 [grub](https://www.archlinux.org/packages/?name=grub). 如果之前安装过 [grub-legacy](https://aur.archlinux.org/packages/grub-legacy/)，安装完成后它会代替[grub-legacy](https://aur.archlinux.org/packages/grub-legacy/).

```
# grub-install --target=i386-pc /dev/sd*x*

```

**Note:**

*   `--target=i386-pc`指示`grub-install`是为使用BIOS的系统安装. 推荐一直标明这点以防混淆.
*   `/dev/sd*x*` 是已经完成[分区](/index.php/Partition "Partition")的磁盘，grub 将安装到它上面。

命令会

*   将`grub`安装到 MBR 的启动代码区域
*   填充`/boot/grub`文件夹
*   生成`/boot/grub/i386-pc/core.img`
*   如果是 MBR 分区的磁盘，将其嵌入 MBR 后面的 31KB 空间
*   如果是 GPT 分区的磁盘，将其嵌入 BIOS 启动分区中

然后必须生成主配置文件。

**Tip:** [GRUB/Tips and tricks#Alternative installation methods](/index.php/GRUB/Tips_and_tricks#Alternative_installation_methods "GRUB/Tips and tricks") 包含了其它 GRUB 安装方式，比如安装到优盘。

详情请参考 [grub-install(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/grub-install.8) 和 [[3]](https://www.gnu.org/software/grub/manual/grub/html_node/BIOS-installation.html#BIOS-installation)。

如果 `/boot` 使用 [LVM](/index.php/LVM "LVM"),可以将 GRUB 安装在多个物理磁盘上.

## UEFI 系统

**注意:**

*   建议阅读并理解[UEFI](/index.php/UEFI "UEFI"), [GPT](/index.php/GPT "GPT") and [UEFI Bootloaders](/index.php/UEFI_Bootloaders "UEFI Bootloaders")
*   使用UEFI安装时，重要的是从开始安装时您的机器就在 UEFI 模式。Arch Linux的安装介质必须是UEFI启动。

### 检查你是否使用GPT且有ESP分区

要使用 EFI 在某个磁盘上进行启动,就需要使用[EFI系统分区](/index.php/EFI_system_partition "EFI system partition")(ESP). GPT 倒不是必须的,不过我们还是高度建议使用 GPT,并且这也是本文当前唯一支持的方法.如果你在一个支持 EFI,并且已经有操作系统(Win8/Win10)的电脑上安装 Arch,系统上已经有了ESP.可以通过`parted`来列出启动磁盘上的分区表以检查其是否支持GPT和ESP(假设这个启动磁盘是/dev/sda)

```
# parted /dev/sda print

```

如果使用 GPT,那么会出现"分区表:GPT".如果使用 EFI,那么会有一个文件系统为vfat的小分区(一般小于512MiB)并且被标志为启动分区.在这个小分区上,应该有一个名为EFI的文件夹.如果这些条件都满足,那么这就是ESP了.注意分区序号,因为之后安装 GRUB 时你需要先挂载这个分区。请将下文中的 `*esp*` 替换为对应的分区号。

如果还没有ESP,请参考 [EFI system partition](/index.php/EFI_system_partition "EFI system partition") 进行创建。

### 安装

**注意:** 众所周知,不同硬件厂商的 UEFI 实现方式也不一样.我们鼓励用户将其配置过程中遇到的问题及其细节分享出来.为了保证[GRUB](/index.php/GRUB "GRUB")页面的简洁,请参考[GRUB/EFI examples (简体中文)](/index.php/GRUB/EFI_examples_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GRUB/EFI examples (简体中文)")。

本节假设您正在 x86_64 上安装 GRUB 系统(x86_64-EFI）。对于 i686 系统，将 `x86_64-efi` 替换为 `i386-efi`。

请确保您在 [bash](/index.php/Bash_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Bash (简体中文)") shell 中。

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [grub](https://www.archlinux.org/packages/?name=grub) 和 [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr)。"GRUB"是引导程序， *efibootmgr* 创建 GRUB 安装脚本使用的 `.efi` 启动项。

接下来的步骤安装 GRUB UEFI 程序到 `**esp**/EFI/grub`中, 安装其模块到`/boot/grub/x86_64-efi`, 然后将可以启动的 `grubx64.efi` 到 `**esp**/EFI/grub`.

首先，告诉 GRUB 使用 UEFI，设置启动目录，并设置引导程序ID。挂载 ESP 分区，例如挂载到 `/boot` 或 `/boot/efi`。将下面命令中的 `*esp_mount*` 修改为挂载点(通常为 `/boot`)

```
# grub-install --target=x86_64-efi --efi-directory=*esp_mount* --bootloader-id=**grub**

```

`--bootloader-id` 是启动项中用来识别 GRUB EFI 的标记，请用容易判断的信息。安装程序会在 `*esp*/EFI/` 的相同目录创建相同名称的目录用来存放 EFI 二进制启动加载器。

上述安装完成后 GRUB 的主目录将位于 `/boot/grub/`。

请记得阅读 [#生成主配置文件](#.E7.94.9F.E6.88.90.E4.B8.BB.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6) 和 [#配置](#.E9.85.8D.E7.BD.AE).

**注意:**

*   一些发行版要求必须有 `/boot/efi`或`/boot/EFI`目录，但 Arch 没有这样的要求。
*   `--efi-directory` 和 `--bootloader-id`是 GRUB UEFI 特有的. `--efi-directory` 指定了 ESP 分区的挂载点，替代了已经废弃的 `--root-directory`
*   您可能注意到在 `grub-install` 命令中没有一个<device_path>选项(例如: `/dev/sda`)。事实上即使提供了 <device_path>,也会被 GRUB 安装脚本忽略，因为 UEFI 启动加载器不使用 MBR 或启动扇区。

## 生成主配置文件

安装后,需要生成置文件 `grub.cfg`。配置文件的生成过程受到 `/etc/default/grub` 和 `/etc/grub.d/` 下脚本的影响。

如果没有额外配置，自动生成程序会侦测 root 目录。所以请确保系统已经启动或 chroot 进入。

**Note:** `/etc/default/grub` 或 `/etc/grub.d/` 中的配置文件变更后，需要重新生成 `grub.cfg`。

使用下面命令生成 `grub.cfg`:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

默认生成脚本自动为 Arch Linux 创建菜单项，其它系统的配置参考配置段落。

[安装](/index.php/Install "Install") 软件包 [os-prober](https://www.archlinux.org/packages/?name=os-prober) 并 [挂载](/index.php/File_systems#Mount_a_file_system "File systems") 包含其它系统的磁盘，*grub-mkconfig* 会自动搜索已经安装的其它系统并添加到启动菜单。

默认文件路径是`/boot/grub/grub.cfg`, 而不是`/boot/grub/i386-pc/grub.cfg`.[grub](https://www.archlinux.org/packages/?name=grub) 软件包提供了示例 `/boot/grub/grub.cfg` 文件，请确保需要的修改都保存在此文件中。

如果是在 chroot 或 *systemd-nspawn* 容器中执行 *grub-mkconfig*，可能会报 *grub-probe* 无法获取 "canonical path of /dev/sdaX" 错误，请尝试使用 *arch-chroot*。参考 [BBS post](https://bbs.archlinux.org/viewtopic.php?pid=1225067#p1225067).

## 配置

本部分介绍了 `/etc/default/grub` 文件的配置，更多信息请参考 [GRUB/Tips and tricks](/index.php/GRUB/Tips_and_tricks "GRUB/Tips and tricks").

每次修改 `/etc/default/grub` 后，都需要重新[#生成主配置文件](#.E7.94.9F.E6.88.90.E4.B8.BB.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6).

### 额外的参数

在 `/etc/default/grub` 中设置 `GRUB_CMDLINE_LINUX` 和 `GRUB_CMDLINE_LINUX_DEFAULT` 变量可以向 Linux 镜像传递额外的参数. 生成普通启动项时,这两个参数的值会合并在一起加入, 对于*recovery*启动项, 则添加 `GRUB_CMDLINE_LINUX` 参数的值.

没有必要两者都使用，如果要系统支持休眠后恢复,可以使用`GRUB_CMDLINE_LINUX_DEFAULT="resume=/dev/sdaX quiet"` (`sda**X**`是交换分区).生成 recovery 启动项时,不会加入 resume 和 quiet 参数; 而其他的普通启动项会包含它们.

*grub-mkconfig* 默认使用根文件系统的 [UUID](/index.php/UUID "UUID") 要禁用此设置，取消 `GRUB_DISABLE_LINUX_UUID=true` 前的注释.

你也可以使用`GRUB_CMDLINE_LINUX="resume=UUID=uuid-of-swap-partition"`

要生成 GRUB recovery启动项,需要在 `/etc/default/grub` 中将 `#GRUB_DISABLE_RECOVERY=true` 注释掉.

更多信息请参考[Kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

### 多系统启动

#### 使用 /etc/grub.d/40_custom 和 grub-mkconfig 自动生成

添加其他启动项的最好方法是编辑 `/etc/grub.d/40_custom` 或 `/boot/grub/custom.cfg`. 运行`grub-mkconfig`后,这些文件中的启动项会被自动添加到 `/boot/grub/custom.cfg` 中.

更新了这些文件后,运行下面命令更新`grub.cfg`:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

在UEFI-GPT模式下,运行:

```
# grub-mkconfig -o /boot/efi/EFI/GRUB/grub.cfg

```

一个典型 `/etc/grub.d/40_custom` 示例文件类似于下面。每个 `menuentry` 的结构都应该和下面的类似.请注意 UEFI 分区`/dev/sda2` 被命名为`hd0,gpt2` 和 `ahci0,gpt2`(请参考[here](/index.php/GRUB#Windows_installed_in_UEFI.2FGPT_Mode_menu_entry "GRUB")获取更多信息)

 `/etc/grub.d/40_custom` 
```
#!/bin/sh
exec tail -n +3 $0
# This file provides an easy way to add custom menu entries.  Simply type the
# menu entries you want to add after this comment.  Be careful not to change
# the 'exec tail' line above.

menuentry "Microsoft Windows 8.1" {
	echo "Loading Microsoft Windows 8.1..."
	insmod part_gpt
	insmod fat
	insmod search_fs_uuid
	insmod chain
	search --fs-uuid --no-floppy --set=root --hint-bios=hd0,gpt2 --hint-efi=hd0,gpt2 --hint-baremetal=ahci0,gpt2 763A-9CB6
	chainloader /EFI/Microsoft/Boot/bootmgfw.efi
}

menuentry "Microsoft Control Center" {
	echo "Loading Microsoft Control Center..."
	insmod part_gpt
	insmod fat
	insmod search_fs_uuid
	insmod chain
	search --fs-uuid --no-floppy --set=root --hint-bios=hd0,gpt2 --hint-efi=hd0,gpt2 --hint-baremetal=ahci0,gpt2 763A-9CB6
	chainloader /EFI/HP/boot/bootmgfw.efi
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

或者让 grub 根据 *UUID* 或 *label* 查找启动项:

```
menuentry "Other Linux" {
        # assuming that UUID is 763A-9CB6
	search --set=root --fs-uuid 763A-9CB6

        # search by label OTHER_LINUX (make sure that partition label is unambiguous)
        #search --set=root --label OTHER_LINUX

	linux /boot/vmlinuz (add other options here as required, for example: root=UUID=763A-9CB6)
	initrd /boot/initrd.img (if the other kernel uses/needs one)
}
```

##### FreeBSD 启动项

要求 FreeBSD 安装在单独的 UFS(v2) 分区上,假设在分区表里面 FreeBSD 分区是 `sda4`:

###### 直接加载内核

```
menuentry 'FreeBSD' {
	insmod ufs2
	set root='hd0,gpt4,bsd1'
	## or 'hd0,msdos4,bsd1', if using an IBM-PC (MS-DOS) style partition table
	kfreebsd /boot/kernel/kernel
	kfreebsd_loadenv /boot/device.hints
	set kFreeBSD.vfs.root.mountfrom=ufs:/dev/ada0s4a
	set kFreeBSD.vfs.root.mountfrom.options=rw
}
```

###### Chainloading 嵌入的启动项

```
menuentry 'FreeBSD' {
	insmod ufs2
	set root='hd0,gpt4,bsd1'
	chainloader +1
}
```

###### 运行传统的 BSD 第二阶段 loader

```
menuentry 'FreeBSD' {
  insmod ufs2
  set root='(hd0,4)'
  kfreebsd /boot/loader
}
```

##### UEFI-GPT 模式下安装的Windows的启动项

**Note:** 这个启动项仅在 UEFI 模式下才起作用，而且 Windows 和 UEFI 的位数必须相同。如果 Grub 是 BIOS 模式，这个方法**无效**。想去参考 [Dual boot with Windows#Windows UEFI vs BIOS limitations](/index.php/Dual_boot_with_Windows#Windows_UEFI_vs_BIOS_limitations "Dual boot with Windows") 和 [Dual boot with Windows#Bootloader UEFI vs BIOS limitations](/index.php/Dual_boot_with_Windows#Bootloader_UEFI_vs_BIOS_limitations "Dual boot with Windows").

```
if [ "${grub_platform}" == "efi" ]; then
	menuentry "Microsoft Windows Vista/7/8/8.1 UEFI-GPT" {
		insmod part_gpt
		insmod fat
		insmod search_fs_uuid
		insmod chain
		search --fs-uuid --set=root $hints_string $fs_uuid
		chainloader /EFI/Microsoft/Boot/bootmgfw.efi
	}
fi
```

`$hints_string` 和 `$uuid`可以通过以下命令获取。`$uuid`:

```
# grub-probe --target=fs_uuid $esp/EFI/Microsoft/Boot/bootmgfw.efi
1ce5-7f28
```

`$hints_string`:

 `# grub-probe --target=hints_string $esp/EFI/Microsoft/Boot/bootmgfw.efi`  `--hint-bios=hd0,gpt1 --hint-efi=hd0,gpt1 --hint-baremetal=ahci0,gpt1` 

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
    ntldr /ntldr
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

## 异常处理

### Intel BIOS不能引导GPT

一些Intel的BIOS要求至少要一个可启动的分区(MBR方案下的),导致GPT方案下的分区GRUB无法启动.

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

有人发现有些发行版不能使用`os-prober`自动发现Arch Linux.据称先使用`/etc/lsb-release`可能会解决这个问题.相关文件和工具可以在 [官方仓库](/index.php/Official_repositories "Official repositories")的[lsb-release](https://www.archlinux.org/packages/?name=lsb-release)包中找到.

### 未找到 Windows 8/10

Windows 8/10 如果启用了 "Hiberboot", "Hybrid Boot" 或 "Fast Boot"，可能会导致 Windows 分区无法被挂载。所以 `grub-mkconfig` 无法找到安装的 Windows。可以先禁用混合启动，将其添加到 GRUB 菜单。

## 参阅

*   官方GRUB说明 - [https://www.gnu.org/software/grub/manual/grub.html](https://www.gnu.org/software/grub/manual/grub.html)
*   Ubuntu GRUB Wiki - [https://help.ubuntu.com/community/Grub2](https://help.ubuntu.com/community/Grub2)
*   在UEFI系统上编译GRUB步骤描述- [https://help.ubuntu.com/community/UEFIBooting](https://help.ubuntu.com/community/UEFIBooting)
*   维基百科[BIOS启动分区](https://en.wikipedia.org/wiki/BIOS_Boot_partition "wikipedia:BIOS Boot partition")
*   配置GRUB的完整说明 - [http://members.iinet.net/~herman546/p20/GRUB2%20Configuration%20File%20Commands.html](http://members.iinet.net/~herman546/p20/GRUB2%20Configuration%20File%20Commands.html)