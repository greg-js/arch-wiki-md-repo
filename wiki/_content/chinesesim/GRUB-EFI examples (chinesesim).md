**翻译状态：** 本文是英文页面 [GRUB/EFI_examples](/index.php/GRUB/EFI_examples "GRUB/EFI examples") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-02-28，点击[这里](https://wiki.archlinux.org/index.php?title=GRUB%2FEFI_examples&diff=0&oldid=362948)可以查看翻译后英文页面的改动。

我们都知道不同的主板制造商有不同的 UEFI 实现。本文介绍了一些针对不同硬件来以 EFI 模式安装/恢复 GRUB 的可行方法。

## Contents

*   [1 Apple Mac EFI 系统](#Apple_Mac_EFI_.E7.B3.BB.E7.BB.9F)
    *   [1.1 通用 Mac 电脑](#.E9.80.9A.E7.94.A8_Mac_.E7.94.B5.E8.84.91)
*   [2 华硕](#.E5.8D.8E.E7.A1.95)
    *   [2.1 Z68 系列和 U47 系列](#Z68_.E7.B3.BB.E5.88.97.E5.92.8C_U47_.E7.B3.BB.E5.88.97)
    *   [2.2 ux32vd](#ux32vd)
    *   [2.3 P8Z77 系列](#P8Z77_.E7.B3.BB.E5.88.97)
    *   [2.4 M5A97](#M5A97)
*   [3 HP](#HP)
    *   [3.1 EliteBook 840 G1](#EliteBook_840_G1)
*   [4 Intel](#Intel)
    *   [4.1 S5400 系列](#S5400_.E7.B3.BB.E5.88.97)
*   [5 联想](#.E8.81.94.E6.83.B3)
    *   [5.1 K450 IdeaCentre](#K450_IdeaCentre)
    *   [5.2 M92p ThinkCentre](#M92p_ThinkCentre)

## Apple Mac EFI 系统

### 通用 Mac 电脑

使用 Mac OS X 自带的 bless 命令把 `grubx64.efi` 设置为默认启动选项。如果你只安装了 Linux, 也可以启动进入 Mac OS X 安装盘并打开终端。创建一个目录并挂载 EFI 系统分区:

```
# cd /Volumes
# mkdir efi
# mount -t msdos /dev/disk0s1 /Volumes/efi

```

然后让 bless 作用于 `grub.efi` 和 EFI 分区以设置为默认启动选项。

```
# bless --folder=/Volumes/efi --file=/Volumes/efi/efi/arch_grub/grubx64.efi --setBoot
# bless --mount=/Volumes/efi --file=/Volumes/efi/efi/arch_grub/grubx64.efi --setBoot

```

更多信息见 [https://help.ubuntu.com/community/UEFIBooting#Apple_Mac_EFI_systems_.28both_EFI_architecture.29](https://help.ubuntu.com/community/UEFIBooting#Apple_Mac_EFI_systems_.28both_EFI_architecture.29).

**注意:** TODO: GRUB 上游源 Bazaar 的 mactel 分支 [http://bzr.savannah.gnu.org/lh/grub/branches/mactel/changes](http://bzr.savannah.gnu.org/lh/grub/branches/mactel/changes). GRUB 开发者将停止提交变更。

**注意:** TODO: Fedora 开发者开发的实验性的 Linux 版 bless 工具 - [mactel-boot](https://aur.archlinux.org/packages/mactel-boot/). 需要更多测试。

## 华硕

### Z68 系列和 U47 系列

```
# cp /boot/efi/EFI/arch_grub/grubx64.efi /boot/efi/shellx64.efi

```

从 UEFI 设置/菜单启动 UEFI Shell 之后 (在华硕 UEFI BIOS 中切换到高级模式，按下位于右上角的 Exit 并选择"Launch EFI shell from filesystem device"). GRUB2 菜单会出现然后可以进入系统。之后，可以使用 efibootmgr 来设置菜单条目，例如 UEFI 分区是 /dev/sda1: (参见 [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface"))

```
efibootmgr -c -g -d /dev/sda -p 1 -w -L "Arch Linux (GRUB)" -l /EFI/arch_grub/grubx64.efi

```

如果你的主板没有这个选项 (就算它有), 你也可以使用 UEFI shell ([Unified Extensible Firmware Interface#UEFI Shell](/index.php/Unified_Extensible_Firmware_Interface#UEFI_Shell "Unified Extensible Firmware Interface")) 来临时为 Arch 分区创建 UEFI 启动选项。

进入 EFI shell 之后，添加 UEFI 启动菜单条目:

```
Shell> bcfg boot add 0 fs1:\EFI\arch_grub\grubx64.efi "Arch Linux (GRUB2)"

```

此处 `fs1` 映射到 UEFI 系统分区，`\EFI\arch_grub\grubx64.efi` 来源于上面 `grub-install` 命令含有的 `--bootloader-id`.

这会临时添加 UEFI 启动选项以在下一次重启时进入 Arch. 进入之后，输入命令 `modprobe efivars` 并确证 `efibootmgr` 没有错误 (没有错误意味着你成功地进入了 UEFI 模式). 然后 [GRUB#UEFI systems](/index.php/GRUB#UEFI_systems "GRUB") 会再次运行并能成功地往 UEFI 菜单永久性地添加启动条目。

### ux32vd

**注意:** 如果没有正确设置 EFI 启动条目的话，BIOS 会无法从 GPT 硬盘启动。这种情况下 BIOS 甚至认不出硬盘。

存在一个大问题，即如果机器从 MBR 启动，之后运行 grub-install (或 efibootmgr) 会失败，并伴随着以下错误提示:

```
EFI variables are not supported on this system

```

首先应以 EFI 启动并创建启动条目。对于 Z68 系列可由如下方法完成: 复制 `/boot/efi/EFI/arch_grub/grubx64.efi` 为 `/boot/efi/shellx64.efi` 并选择"Launch EFI shell from filesystem device". 成功启动之后就能以 grub-install 或 efibootmgr 创建启动条目了。

### P8Z77 系列

*   启动进 live 系统并 chroot 进目标系统。
*   确证 100 MB fat32 的分区被标记为 "EFI System" (gdisk 使用16进制编码 ef00).

**注意:** 如果你得到信息"WARNING: Not enough clusters for a 32 bit FAT!"，就要用 `mkfs.vfat -s2 -F32 ...` 来减小簇大小否则 UEFI 会无法读取分区。

**在 CHROOT 内**

```
# mount -t vfat /dev/sdXY /boot/efi
# grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=arch --recheck
# grub-mkconfig -o /boot/grub/grub.cfg
# wget [https://edk2.svn.sourceforge.net/svnroot/edk2/trunk/edk2/ShellBinPkg/UefiShell/X64/Shell.efi](https://edk2.svn.sourceforge.net/svnroot/edk2/trunk/edk2/ShellBinPkg/UefiShell/X64/Shell.efi)
# umount /boot/efi

```

EFI 分区应该只包含两个文件:

```
/Shell.efi
/EFI/arch/grubx64.efi

```

*   重启进入 BIOS (`Delete` 键可以做到).
*   使用方向键移动到 'exit' 菜单进入到 EFI Shell.
*   往菜单里为 Arch 添加新条目。下面的是一个范例，更多见文章 [UEFI#Launching UEFI Shell](/index.php/UEFI#Launching_UEFI_Shell "UEFI").

**在 EFI SHELL 内**

```
Shell> bcfg boot dump -v
Shell> bcfg boot add 1 fs0:\EFI\arch\grubx64.efi "Arch Linux (grub manually added)"
Shell> exit

```

*   重启进入 BIOS.
*   进入 'Boot' 部分并调整启动选项次序，使得 "Arch Linux (grub 手动添加)" 在 SSD 上。
*   进入该条目，享受成功的喜悦。

### M5A97

完成标准 Arch 安装流程，确保已安装 [grub](https://www.archlinux.org/packages/?name=grub) 并且硬盘是 GPT 格式。

来自 [GRUB#UEFI systems](/index.php/GRUB#UEFI_systems "GRUB"):

UEFI 系统分区需要挂载到 `/boot/efi/` 以便 GRUB 安装脚本探测到:

```
# mkdir -p /boot/efi
# mount -t vfat /dev/sdXY /boot/efi

```

此处 X 是你的启动硬盘 Y 是你之前创建的 EFI 分区。

使用如下命令添加 GRUB UEFI 应用程序到 `/boot/efi/EFI/arch_grub` 以及添加模块到 `/boot/grub/x86_64-efi`:

```
# modprobe dm-mod
# grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=arch_grub --recheck --debug
# mkdir -p /boot/grub/locale
# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

```

为 GRUB 生成配置文件:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

然后复制 [修改版 UEFI Shell v2 二进制文件](http://dl.dropbox.com/u/17629062/Shell2.zip) UefiShellX64.efi 到你的 EFI 系统分区根目录。

```
# cp ~/Shell2/UefiShellX64.efi /mnt/boot/efi/shellx64.efi

```

我们使用这个 Shell 应用程序因为 efibootmgr 命令在 grub-install 期间没有错误提示。

之后从 UEFI 设置/菜单启动 UEFI Shell 之后 (在华硕 UEFI BIOS 中切换到高级模式，按下位于右上角的 Exit 并选择"Launch EFI shell from filesystem device"). UEFI Shell 会出现。在此添加 GRUB UEFI app 到引导器。

```
Shell> bcfg boot add 3 fs0:\EFI\Arch_Grub\grubx64.efi "Arch_Grub"

```

此处 `fs0` 映射到 UEFI 系统分区，`3` 是0启动项目录。

**注意:** UEFI Shell 命令通常支持 `-b` 选项，它用来在每页输出完后暂停。`map` 列出识别的文件系统 (`fs0`, ...) 和数据存储设备 (`blk0`, ...). 运行 `help -b` 以列出可用命令。 [Unified Extensible Firmware Interface#Important UEFI Shell Commands](/index.php/Unified_Extensible_Firmware_Interface#Important_UEFI_Shell_Commands "Unified Extensible Firmware Interface")

列出目前启动条目，运行:

```
Shell> bcfg boot dump -v

```

## HP

### EliteBook 840 G1

详见 [HP EliteBook 840 G1#UEFI Setup](/index.php/HP_EliteBook_840_G1#UEFI_Setup "HP EliteBook 840 G1").

**注意:** 上面的流程对一些 HP 其他型号也有用。

## Intel

### S5400 系列

这个主板可以在 BIOS 和 EFI 模式下运行。BIOS 模式需要 MBR 分区方案的硬盘，EFI 需要 GPT 的。注意这个主板执行 Intel EFI v1.10 标准，并且仅限 i386\. 除开以下变更之外，遵循正常 UEFI 安装流程。

*   不使用 `grub-efi-x86_64` 包，而是 `grub-efi-i386`.
*   在 UEFI (v2.0) 前的固件 `bcfg` 命令不可用。`startup.nsh` 可在 EFI 分区的根目录使用，其中要包含引导器的路径。例如:

`fs0:\EFI\arch_grub\boot.efi` 必须位于在 EFI 分区根目录上的 `startup.nsh` 文件里。

*   `grub.cfg` 必须与 grub EFI 文件放到一起，否则 grub 会找不到并进入交互 shell.

## 联想

### K450 IdeaCentre

"EFI System"分区要求文件 `EFI\Boot\bootx64.efi` 存在来进行引导，否则会收到"Error 1962: No operating system found. Boot sequence will automatically repeat." 假设"EFI System"挂载在 `/boot/efi`:

```
 # grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=grub --recheck --debug
 # mkdir /boot/efi/EFI/Boot
 # touch /boot/efi/EFI/Boot/bootx64.efi

```

这是 UEFI 实现的疑似 bug 的解决方案。

### M92p ThinkCentre

系统有 EFI 白名单标签。只能从标有"Red Hat Enterprise Linux"的启动。所以给引导器指定一个合适的 id:

```
 # grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id="Red Hat Enterprise Linux" --recheck --debug

```