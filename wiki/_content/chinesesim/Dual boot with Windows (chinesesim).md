**翻译状态：** 本文是英文页面 [Dual_boot_with_Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-08-20，点击[这里](https://wiki.archlinux.org/index.php?title=Dual_boot_with_Windows&diff=0&oldid=445881)可以查看翻译后英文页面的改动。

Related articles

*   [Dual boot with Windows/SafeBoot](/index.php/Dual_boot_with_Windows/SafeBoot "Dual boot with Windows/SafeBoot")

这篇条目提供了 Arch Linux 和 Windows 双重启动的一些相关信息。

## Contents

*   [1 重要信息](#重要信息)
    *   [1.1 Windows UEFI 和 BIOS 启动限制](#Windows_UEFI_和_BIOS_启动限制)
    *   [1.2 安装介质限制](#安装介质限制)
    *   [1.3 UEFI / BIOS 启动管理器限制](#UEFI_/_BIOS_启动管理器限制)
    *   [1.4 UEFI 安全启动](#UEFI_安全启动)
    *   [1.5 快速启动](#快速启动)
    *   [1.6 Windows 中的文件名限制](#Windows_中的文件名限制)
*   [2 安装](#安装)
    *   [2.1 BIOS 系统](#BIOS_系统)
        *   [2.1.1 使用 Linux 启动管理器](#使用_Linux_启动管理器)
        *   [2.1.2 使用 Windows 启动管理器](#使用_Windows_启动管理器)
            *   [2.1.2.1 Windows Vista/7/8/8.1/10 的启动管理器](#Windows_Vista/7/8/8.1/10_的启动管理器)
    *   [2.2 UEFI 系统](#UEFI_系统)
    *   [2.3 疑难解答](#疑难解答)
        *   [2.3.1 Couldn't create a new partition or locate an existing one (无法创建或者定位分区)](#Couldn't_create_a_new_partition_or_locate_an_existing_one_(无法创建或者定位分区))
        *   [2.3.2 安装 Windows 后无法再引导 Linux](#安装_Windows_后无法再引导_Linux)
*   [3 时间标准](#时间标准)
*   [4 另见](#另见)

## 重要信息

### Windows UEFI 和 BIOS 启动限制

Microsoft 对不同版本的启动方式限制不同:

| Windows 版本 | BIOS-MBR | UEFI-GPT |
| x86 (IA32) | x86_64 |
| Windows XP | x86 | 支持

（大多数）

 | 不支持 | 不支持 |
| x64 |
| Windows Vista | x86 |
| x64 | 带有 SP1 的版本支持 |
| Windows 7 | x86 | 不支持 |
| x64 | 支持 |
| Windows 8/8.1 | x86 | 部分支持 | 不支持 |
| x64 | 不支持 | 支持 |
| Windows 10 | x86 | 部分支持 | 不支持 |
| x64 | 不支持 | 支持 |

所有版本的 Windows 都不支持 BIOS 引导 GPT 分区上的 Windows 或 UEFI 引导 MBR 分区上的 Windows。

某些 Intel Atom 芯片的平板电脑只支持 IA32-UEFI ，因此只能启动 GPT 分区上的 32 位 ( x86 ) 操作系统。

对于预装在电脑上的 Windows 的大多数情况:

*   预装 Windows XP ( 所有版本 ),Windows Vista 或 Windows 7 (32 位版本),默认通过 BIOS-MBR 启动.
*   大多数预装 Windows 7 64位版本的电脑默认通过 BIOS-MBR 启动,有部分近期预装Windows 7 64位版本的电脑通过 UEFI-GPT 启动.
*   预装 Windows 8/8.1/10 的电脑都是通过 UEFI 启动,32 位系统通过 IA32 UEFI 模式启动,64 位系统通过 x86_64 UEFI 模式启动.

可以从 Windows 系统信息中了解具体的启动类型 (这个方法来自[这里](http://www.eightforums.com/tutorials/29504-bios-mode-see-if-windows-boot-uefi-legacy-mode.html)):

*   启动进 Windows
*   按下 Windows 徽标键和 R 键打开 "运行" 对话框
*   键入 "msinfo32" 并回车确认
*   在系统信息窗口中,选择"系统摘要",查看右侧的"BIOS 模式".
*   对于 UEFI-GPT 模式,这里的值为 "UEFI",对于 BIOS-MBR 模式,这里的值为 "Legacy".

一般的, Windows 强制通过固件类型确定硬盘分区表.这是由 Windows 安装程序限定的(例如以 UEFI 模式启动的安装程序只能安装在 GPT 硬盘上,以 Legacy BIOS 模式启动的安装程序只能安装在 MBR (也叫做 msdos) 分区表的硬盘上).目前官方 (Microsoft) 没有在 UEFI-MBR 或 BIOS-GPT 上运行 Windows 的方法.因此 Windows 只支持 UEFI-GPT 或 BIOS-MBR 启动.

尽管 Linux 内核并不强制要求这些,但是考虑到 Windows 的限制和启动管理器的需要,如果需要在一个硬盘上启动 Windows 和 Linux 的话,建议用户选择 Windows 可用的分区组合,例如 UEFI-GPT 或 BIOS-MBR,参阅 [http://support.microsoft.com/kb/2581408](http://support.microsoft.com/kb/2581408) 获得更多信息.

### 安装介质限制

某些 Intel Atom SoC 平板 (Clover trail / Bay Trail) 因为 Microsoft 对 Connected Standby 的要求只提供 IA32 UEFI 固件支持而不包含 Legacy BIOS 支持 (和大多数 x86_64 UEFI 系统不同).Arch Linux 官方安装介质和 Archboot (2014/02 以前) 并不提供 IA32-UEFI 启动支持,因此在这种设备上无法通过 ArchISO 启动安装.

### UEFI / BIOS 启动管理器限制

大部分 Linux 的启动管理器不支持运行或链式加载另一种固件的启动管理器. 因此安装在 UEFI 模式下的 Arch Linux 的启动管理器无法加载位于另一个 BIOS-MBR 硬盘上的 Windows .安装在 BIOS 模式下的 Arch Linux 的启动管理器也无法加载位于另一个 UEFI-GPT 硬盘上的 Windows.

例外是安装在 Apple Mac 上的 UEFI 模式的 GRUB (通过 **apploloader** 实现引导 BIOS 系统,不能用于非 Apple 设备上),和 rEFInd (技术上支持 UEFI 引导 BIOS 系统,但是作者 Rod Smith 称[不能用于非 Apple UEFI 上](http://rodsbooks.com/refind/using.html#legacy).)

另外安装在 BIOS-GPT 上的 Arch 可以引导另一块 BIOS-MBR 硬盘上的 Windows (如果所选用的启动管理器支持链式加载另一块硬盘上的启动扇区).

**Note:** 对于同一个硬盘上安装的 Arch Linux 和 Windows ,Arch 要使用和 Windows 一致的启动模式和分区组合.

### UEFI 安全启动

所有预装 Windows 8/8.1/10 并以 UEFI 模式启动的电脑默认开启安全启动. Arch Linux 的安装媒体可以在安全启动打开的状态下启动,参见[Secure Boot#Booting archiso](/index.php/Secure_Boot#Booting_archiso "Secure Boot").

建议在启动 Arch Linux 之前手动从 UEFI 固件设置中关闭安全启动,Windows 应该仍能启动.唯一的要求是能访问 UEFI 固件设置并且能够从固件设置中禁用安全启动 (因为 Microsoft 禁止在预装 Windows 8/8.1/10 的电脑中远程关闭或者在系统中关闭安全启动).

### 快速启动

快速启动是 Windows 8 (及更新的版本) 中的一项功能,通过休眠来提高启动速度.但是如果你休眠 Windows 然后进入另一个系统修改文件,可能会造成数据丢失.即使你不打算在双系统中共享文件,这也容易损坏 EFI 系统分区.因此你应该在安装 Linux 前禁用快速启动:

*   [Windows 8](http://www.eightforums.com/tutorials/6320-fast-startup-turn-off-windows-8-a.html)
*   [Windows 10](http://www.tenforums.com/tutorials/4189-fast-startup-turn-off-windows-10-a.html),

[ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) 通过 [safe-guard](http://sourceforge.net/p/ntfs-3g/ntfs-3g/ci/559270a8f67c77a7ce51246c23d2b2837bcff0c9/) 阻止以读写方式挂载休眠中的硬盘,但 Linux 内核中的驱动并不能保证这一点.

### Windows 中的文件名限制

Windows 中的文件名长度最长为 [260 字符](http://blogs.msdn.com/b/bclteam/archive/2007/02/13/long-paths-in-net-part-1-of-3-kim-hamilton.aspx).

另外 Windows [对文件名中包含的字符也有限制](http://msdn.microsoft.com/en-us/library/aa365247(VS.85).aspx#naming_conventions), Windows 中文件名中不能包含:

*   < (小于号)
*   > (大于号)
*   : (冒号)
*   " (双引号)
*   / (斜线)
*   \ (反斜线)
*   | (管道符号)
*   ? (问号)
*   * (星号)

这是 Windows 而非 NTFS 的限制,因此其它系统依然可以在 NTFS 文件系统中创建文件名中带有这些符号的文件,但 Windows 无法识别这些文件. 运行 `chkdsk` 时也可能删除它们,这是一个引发数据丢失的风险.

**NTFS-3G** 可以通过 [windows_filenames](http://www.tuxera.com/community/ntfs-3g-manual/#4) 挂载选项遵循这些限制 (参阅 [fstab](/index.php/Fstab "Fstab")).

## 安装

推荐先安装 Windows 再安装 Linux , 安装 Windows 时只使用硬盘的部分空间建立需要的分区.在 Windows 安装完毕后,进入 Linux 安装环境中后你可以对硬盘未分配的空间进行分区而不改动 Windows 分区. 对于 UEFI 系统,可以使用 Windows 安装时建立的 EFI 系统分区.

### BIOS 系统

#### 使用 Linux 启动管理器

你可以使用 [GRUB](/index.php/GRUB#Dual-booting "GRUB") 或 [Syslinux](/index.php/Syslinux#Chainloading "Syslinux").

#### 使用 Windows 启动管理器

需要设置 Windows 启动管理器使它加载另一个启动管理器 (例如 GRUB ),然后启动 Arch Linux.

##### Windows Vista/7/8/8.1/10 的启动管理器

下面的内容摘录自 [http://www.iceflatline.com/2009/09/how-to-dual-boot-windows-7-and-linux-using-bcdedit/](http://www.iceflatline.com/2009/09/how-to-dual-boot-windows-7-and-linux-using-bcdedit/).

In order to have the Windows boot loader see the Linux partition, one of the Linux partitions created needs to be FAT32 (in this case, `/dev/sda3`). The remainder of the setup is similar to a typical installation. Some documents state that the partition being loaded by the Windows boot loader must be a primary partition but I have used this without problem on an extended partition.

*   When installing the GRUB boot loader, install it on your `/boot` partition rather than the MBR.
    **Note:** For instance, my `/boot` partition is `/dev/sda5`. So I installed GRUB at `/dev/sda5` instead of `/dev/sda`. For help on doing this, see [GRUB#Install to partition or partitionless disk](/index.php/GRUB#Install_to_partition_or_partitionless_disk "GRUB")

*   Under Linux make a copy of the boot info by typing the following at the command shell:

```
my_windows_part=/dev/sda3
my_boot_part=/dev/sda5
mkdir /media/win
mount $my_windows_part /media/win
dd if=$my_boot_part of=/media/win/linux.bin bs=512 count=1

```

*   Boot to Windows and open up and you should be able to see the FAT32 partition. Copy the linux.bin file to `C:\`. Now run **cmd** with administrator privileges (navigate to *Start > All Programs > Accessories*, right-click on *Command Prompt* and select *Run as administrator*):

```
bcdedit /create /d “Linux” /application BOOTSECTOR

```

*   BCDEdit will return an alphanumeric identifier for this entry that I will refer to as {ID} in the remaining steps. You will need to replace {ID} by the actual returned identifier. An example of {ID} is {d7294d4e-9837-11de-99ac-f3f3a79e3e93}.

```
bcdedit /set {ID} device partition=c:
bcdedit /set {ID}  path \linux.bin
bcdedit /displayorder {ID} /addlast
bcdedit /timeout 30

```

Reboot and enjoy. In my case I'm using the Windows boot loader so that I can map my Dell Precision M4500's second power button to boot Linux instead of Windows.

### UEFI 系统

在你安装好 Windows 以后,你的硬盘上应该会有这些分区 :

*   格式化成 `FAT32` 的 EFI 系统分区,分区类型为 `ef00 EFI System`,
*   一个分区类型为 `0c01 Microsoft reserved` 的 Microsoft 保留分区, 一般大小为 `128 MiB`,
*   一个 `NTFS` 文件系统 ,分区类型为 `0700 Microsoft basic data` (Microsoft 基本数据) 的分区 ,这是 Windows 中的 `C:\`,
*   可能还会有与 C:\ 相同类型的分区,一般为恢复分区 .

用 Windows 中的磁盘分区工具(例如"磁盘管理"),检查这些分区的位置和卷标.这会帮你理解哪些分区对 Windows 而言是重要的. 简而言之:前三个分区(EFI 系统分区,Microsoft 保留分区,和 Windows 所在的分区)很重要,不要删除它们.

你可以根据需要 [进行分区](/index.php/Partitioning "Partitioning"), 记住如果有就没必要创建新的 EFI 系统分区.如果需要,[挂载](/index.php/Mount "Mount") 现有的 EFI 系统分区到`/boot`, 安装 [bootloader](/index.php/Bootloader "Bootloader") ,并把它的信息写入到 `/etc/[fstab](/index.php/Fstab "Fstab")`.

选择一个合适的启动管理器, [systemd-boot](/index.php/Systemd-boot "Systemd-boot") 和 [rEFInd](/index.php/REFInd "REFInd") 可以自动检测 *Windows Boot Manager* (`\EFI\Microsoft\Boot\bootmgfw.efi`) 并为它添加启动项.

[GRUB](/index.php/GRUB "GRUB") 用户请参阅 [GRUB#Windows installed in UEFI/GPT mode](/index.php/GRUB#Windows_installed_in_UEFI/GPT_mode "GRUB"). Syslinux (version 6.02 和 6.03-pre9) 和 ELILO 不支持链式加载 EFI 可执行文件,所以不能引导 `\EFI\Microsoft\Boot\bootmgfw.efi`.

对于打开 [安全启动](/index.php/Secure_Boot "Secure Boot") 的电脑,你可能需要更多的步骤(关闭安全启动或是使安装介质支持安全启动,参见前面的链接).

### 疑难解答

#### Couldn't create a new partition or locate an existing one (无法创建或者定位分区)

Windows 的安装介质应该格式化为与硬盘分区表相同的模式,见上文 [#Windows UEFI 和 BIOS 启动限制](#Windows_UEFI_和_BIOS_启动限制).

#### 安装 Windows 后无法再引导 Linux

参阅 [UEFI#Windows changes boot order](/index.php/UEFI#Windows_changes_boot_order "UEFI").

## 时间标准

*   推荐: 参照 [System time#UTC in Windows](/index.php/System_time#UTC_in_Windows "System time") 将 Windows 和 Arch 的硬件时钟设置为 UTC,并停用 Windows 的自动更新时间服务 (因为 Windows 会重新成默认的 *localtime*).

*   不推荐: 设置 Arch Linux 的硬件时钟为 *localtime* 并停用所有时间同步关联的服务,例如 [NTPd](/index.php/NTPd "NTPd") . 这会让 Windows 接管硬件时钟设置,因此你应该至少每年启动两次 Windows (例如当你所在的地区应用夏令时,在每年的春季和秋季启动一次). 同时,如果你这么做,就别在论坛里问为什么时钟慢了一个小时之类的问题了(特别是你有些时候没启动 Windows 的情况下).

## 另见

*   [Booting Windows from a desktop shortcut](https://bbs.archlinux.org/viewtopic.php?id=140049)