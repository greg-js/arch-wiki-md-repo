**翻译状态：** 本文是英文页面 [Installation_guide](/index.php/Installation_guide "Installation guide") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-08-22，点击[这里](https://wiki.archlinux.org/index.php?title=Installation_guide&diff=0&oldid=446203)可以查看翻译后英文页面的改动。

本文将引导您从用官方安装镜像启动的 Live 系统安装 [Arch Linux](/index.php/Arch_Linux "Arch Linux")。安装之前请先阅读 [FAQ (简体中文)](/index.php/FAQ_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "FAQ (简体中文)")。为了更清楚的阅读此文档，请参考 [Help:Reading](/index.php/Help:Reading "Help:Reading").

[Category:Getting and installing Arch (简体中文)](/index.php/Category:Getting_and_installing_Arch_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Getting and installing Arch (简体中文)") 包含了更多针对特殊情况的安装指南。

更详细的资源，可以阅读 [ArchWiki](/index.php/ArchWiki:About "ArchWiki:About") 文章(安装环境中可以使用 [ELinks](/index.php/ELinks "ELinks") 访问)。如需要交互帮助，还可以通过 [IRC channel](/index.php/IRC_channel "IRC channel") 频道和 [论坛](https://bbs.archlinux.org/) 。此外，在使用您不熟悉的命令之前，请务必首先阅读该命令对应的 `man` 文件。查看该文件的方法很简单，通常只需要 `man *要查看的命令*` 即可。

## Contents

*   [1 安装准备](#.E5.AE.89.E8.A3.85.E5.87.86.E5.A4.87)
    *   [1.1 验证启动模式](#.E9.AA.8C.E8.AF.81.E5.90.AF.E5.8A.A8.E6.A8.A1.E5.BC.8F)
    *   [1.2 键盘布局](#.E9.94.AE.E7.9B.98.E5.B8.83.E5.B1.80)
    *   [1.3 连接到因特网](#.E8.BF.9E.E6.8E.A5.E5.88.B0.E5.9B.A0.E7.89.B9.E7.BD.91)
    *   [1.4 更新系统时间](#.E6.9B.B4.E6.96.B0.E7.B3.BB.E7.BB.9F.E6.97.B6.E9.97.B4)
    *   [1.5 建立硬盘分区](#.E5.BB.BA.E7.AB.8B.E7.A1.AC.E7.9B.98.E5.88.86.E5.8C.BA)
    *   [1.6 格式化分区](#.E6.A0.BC.E5.BC.8F.E5.8C.96.E5.88.86.E5.8C.BA)
    *   [1.7 挂载分区](#.E6.8C.82.E8.BD.BD.E5.88.86.E5.8C.BA)
*   [2 安装](#.E5.AE.89.E8.A3.85)
    *   [2.1 选择镜像](#.E9.80.89.E6.8B.A9.E9.95.9C.E5.83.8F)
    *   [2.2 安装基本系统](#.E5.AE.89.E8.A3.85.E5.9F.BA.E6.9C.AC.E7.B3.BB.E7.BB.9F)
*   [3 配置系统](#.E9.85.8D.E7.BD.AE.E7.B3.BB.E7.BB.9F)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Time zone](#Time_zone)
    *   [3.4 Locale](#Locale)
    *   [3.5 主机名](#.E4.B8.BB.E6.9C.BA.E5.90.8D)
    *   [3.6 网络配置](#.E7.BD.91.E7.BB.9C.E9.85.8D.E7.BD.AE)
    *   [3.7 Initramfs](#Initramfs)
    *   [3.8 Root 密码](#Root_.E5.AF.86.E7.A0.81)
    *   [3.9 安装引导程序](#.E5.AE.89.E8.A3.85.E5.BC.95.E5.AF.BC.E7.A8.8B.E5.BA.8F)
    *   [3.10 重启](#.E9.87.8D.E5.90.AF)
*   [4 安装后的工作](#.E5.AE.89.E8.A3.85.E5.90.8E.E7.9A.84.E5.B7.A5.E4.BD.9C)

## 安装准备

理论上，Arch Linux能在任何内存空间不小于 256MB 的[i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) "wikipedia:P6 (microarchitecture)")兼容机上运行。最基本的[base](https://www.archlinux.org/groups/x86_64/base/)组中包含的包将占用约 800MB 存储空间。

[Category:Getting and installing Arch (简体中文)](/index.php/Category:Getting_and_installing_Arch_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Getting and installing Arch (简体中文)") 中包含了下载和启动安装介质的说明。建议始终使用最新的 ISO 镜像。启动完成后会自动以 root 登录并进入[zsh](/index.php/Zsh_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Zsh (简体中文)")命令提示， [grml config](http://grml.org/zsh/)提供了额外的配置。编辑配置文件时可以使用 [nano](/index.php/Nano#Usage "Nano") 或 [vim](/index.php/Vim#Usage "Vim") 。

### 验证启动模式

要确认是否已进入[UEFI](/index.php/UEFI "UEFI")模式，检查 [efivars](/index.php/Efivars "Efivars")：

```
# ls /sys/firmware/efi/efivars

```

### 键盘布局

[控制台键盘布局](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") 默认为`us`（美式键盘映射）。如果您正在使用非[美式](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg")键盘布局，通过以下的命令选择相应的键盘映射表：

 `# loadkeys *layout*` 

将 *layout* 转换为您的键盘布局，如`fr`，`uk`，`dvorak`或`be-latin1`。[这里](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements "wikipedia:ISO 3166-1 alpha-2")有国家的二位字母编码表。使用命令 `ls /usr/share/kbd/keymaps/**/*.map.gz` 列出所有可用的键盘布局。

[Console fonts](/index.php/Console_fonts "Console fonts") 位于 `/usr/share/kbd/consolefonts/`, 设置方式请参考 [setfont(8)](http://man7.org/linux/man-pages/man8/setfont.8.html).

### 连接到因特网

所有有线网络连接都启用了 `dhcpcd`,可以用 [ping(8)](http://man7.org/linux/man-pages/man8/ping.8.html) 等工具验证。

其它[网络配置方式](/index.php/Network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network configuration (简体中文)")可以使用 [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") 和 [netctl](/index.php/Netctl "Netctl")。参考[netctl.profile(5)](https://git.archlinux.org/netctl.git/tree/docs/netctl.profile.5.txt).

使用这两个方式时，需要 [停止](/index.php/Stop "Stop") `dhcpcd@*interface*.service`:

```
# systemctl stop dhcpcd@*interface*.service

```

### 更新系统时间

用 [systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd") 确保系统时间是正确的：

```
# timedatectl set-ntp true

```

用 `timedatectl status` 检查服务状态.详情阅读 [Time (简体中文)](/index.php/Time_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Time (简体中文)").

参阅 [systemd-timesyncd](/index.php/Systemd-timesyncd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd-timesyncd (简体中文)")。

### 建立硬盘分区

详情参见 [Partitioning (简体中文)](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Partitioning (简体中文)")；可能需要一些特别的分区，详情请参阅[在 Linux 上创建 EFI 系统分区](/index.php/UEFI#EFI_System_Partition "UEFI")以及[GRUB BIOS boot partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB")(英文)；

要修改 [分区表](/index.php/Partition_table "Partition table")，可以使用 [fdisk](/index.php/Fdisk "Fdisk") 或 [parted](/index.php/Parted "Parted")，这两个 Tool 都支持 [MBR](/index.php/MBR "MBR") 和 [GPT](/index.php/GPT "GPT"), [gdisk(8)](http://www.rodsbooks.com/gdisk/gdisk.html) 仅支持 GPT.

至少需要一个 `/` 目录，[UEFI](/index.php/UEFI "UEFI") 系统还需要 [EFI 系统分区](/index.php/EFI_System_Partition_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "EFI System Partition (简体中文)")。GRUB 还需要一个额外分区，参考 [GRUB BIOS boot partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB").

如果需要需要创建多级存储，请参考 [LVM](/index.php/LVM "LVM")、[LUKS](/index.php/Dm-crypt_with_LUKS "Dm-crypt with LUKS") 或 [RAID](/index.php/RAID "RAID")。

### 格式化分区

详情参见 [文件系统](/index.php/File_systems#Create_a_file_system "File systems") 和 [swap (简体中文)](/index.php/Swap_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Swap (简体中文)")。

如果您正在使用(U)EFI，您很可能需要另外一个分区来放置UEFI系统分区。请阅读[这篇文章](/index.php/Unified_Extensible_Firmware_Interface#Create_an_UEFI_System_Partition_in_Linux "Unified Extensible Firmware Interface")。

### 挂载分区

将分区[挂载(8)](http://man7.org/linux/man-pages/man8/%E6%8C%82%E8%BD%BD.8.html)到 `/mnt`，如果使用多个分区，还需要为其他分区创建目录并挂载它们（`/mnt/boot`、`/mnt/home`、……）。激活 [swapon(8)](http://man7.org/linux/man-pages/man8/swapon.8.html) 分区，这样 `genfstab` 才能自动检测到它们。

## 安装

### 选择镜像

编辑 `/etc/pacman.d/mirrorlist`，选择您的首选 [mirror](/index.php/Mirrors "Mirrors"). 这个 mirror 列表也将通过 `pacstrap` 被复制并保存在到系统中，所以请确保设置正确。

### 安装基本系统

执行 [pacstrap](https://git.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) 脚本，默认会安装 [base](https://www.archlinux.org/groups/x86_64/base/) 组：

```
# pacstrap /mnt

```

这个组并没有包含全部 live 环境中的程序，有些需要额外安装，例如[btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs)。[packages.both](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both) 页面包含了它们的差异。

如果您想通过 [AUR (简体中文)](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)") 或者 [ABS (简体中文)](/index.php/ABS_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ABS (简体中文)") 编译安装软件包,需要装上 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/)：

```
# pacstrap -i /mnt base base-devel

```

使用 `-i` 选项时会在实际安装前进行确认。此章节会给您安装好最基本的 Arch 系统，其它软件以后会用 [pacman (简体中文)](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 安装得到。第一个 [initramfs](/index.php/Initramfs "Initramfs") 会在新系统的启动路径生成和安装，请确保 `==> Image creation successful`.

## 配置系统

### Fstab

用以下命令生成 [fstab](/index.php/Fstab "Fstab") 文件 (用 `-U` 或 `-L` 选项设置UUID 或卷标)：

```
# genfstab -U -p /mnt >> /mnt/etc/fstab

```

**强烈建议** 在执行完以上命令后，后检查一下生成的 `/mnt/etc/fstab` 文件是否正确。

### Chroot

[Change root](/index.php/Change_root "Change root") 到新安装的系统：

```
# arch-chroot /mnt /bin/bash

```

### Time zone

设置 [时区](/index.php/Time_zone "Time zone"):

```
# ln -s /usr/share/zoneinfo/*zone*/*subzone* /etc/localtime

```

例如：

```
# ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

```

建议设置[时间标准](/index.php/Time_standard "Time standard") 为 UTC，并调整 [时间漂移](/index.php/Time_skew "Time skew"):

```
# hwclock --systohc --utc

```

### Locale

本地化的程序与库若要本地化文本，都依赖 [Locale](/index.php/Locale "Locale"), 后者明确规定地域、货币、时区日期的格式、字符排列方式和其他本地化标准等等。在下面两个文件设置：`locale.gen` 与 `locale.conf`.

`/etc/locale.gen`是一个仅包含注释文档的文本文件。指定您需要的本地化类型，只需移除对应行前面的注释符号（`＃`）即可，建议选择帶`UTF-8`的項：

 `# nano /etc/locale.gen` 
```
en_US.UTF-8 UTF-8
zh_CN.UTF-8 UTF-8
zh_TW.UTF-8 UTF-8

```

接着执行`locale-gen`以生成locale讯息：

```
# locale-gen

```

`/etc/locale.gen` 生成指定的本地化文件，每次 [glibc](https://www.archlinux.org/packages/?name=glibc) 更新之后也会运行 `locale-gen`。

创建 `locale.conf` 并提交您的本地化选项：

**Tip:** 将系统 locale 设置为`en_US.UTF-8`，系统的 Log 就会用英文显示，这样更容易问题的判断和处理。用户可以设置自己的 locale，详情参阅[Locale#Per user](/index.php/Locale#Per_user "Locale").

```
# echo LANG=en_US.UTF-8 > /etc/locale.conf

```

**警告:** 不推荐在此设置任何中文locale，或导致tty乱码。

### 主机名

要设置 [hostname](/index.php/Hostname "Hostname")，将其[添加](/index.php/Add "Add") 到 `/etc/hostname`, *myhostname* 是需要的主机名:

```
# echo ***myhostname*** > /etc/hostname

```

### 网络配置

对新安装的系统，需要再次设置网络。具体请参考 [Network configuration (简体中文)](/index.php/Network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network configuration (简体中文)") 和

对于 [无线网络配置](/index.php/Wireless_network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wireless network configuration (简体中文)")，[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [iw](https://www.archlinux.org/packages/?name=iw), [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant)，[dialog](https://www.archlinux.org/packages/?name=dialog) 以及需要的 [固件软件包](/index.php/Wireless#Installing_driver.2Ffirmware "Wireless").

### Initramfs

如果修改了 [mkinitcpio.conf](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mkinitcpio (简体中文)")，用以下命令创建一个初始 RAM disk：

```
# mkinitcpio -p linux

```

### Root 密码

设置 root [密码](/index.php/Password "Password"):

```
# passwd

```

### 安装引导程序

[启动加载器](/index.php/Boot_loaders_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Boot loaders (简体中文)")页面介绍了可用选项和配置方法。包括 [GRUB](/index.php/GRUB "GRUB") (BIOS/UEFI), [systemd-boot](/index.php/Systemd-boot "Systemd-boot") (UEFI) 和 [syslinux](/index.php/Syslinux "Syslinux") (BIOS)等.

Intel CPU 也需要安装 [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) 并根据 [Microcode](/index.php/Microcode "Microcode") 配置 boot loader.

### 重启

输入 `exit` 或按 `Ctrl+D` 退出 chroot。

可选，卸载挂载的分区，如果有问题可以通过 [fuser(1)](http://man7.org/linux/man-pages/man1/fuser.1.html) 检查。

```
# umount -R /mnt

```

现在重启系统，移除安装介质并执行`reboot`，新系统启动后用 root 登录。

## 安装后的工作

系统管理引导，图形用户界面的安装、声音管理、触摸板支持等后期工作参见 [General recommendations (简体中文)](/index.php/General_recommendations_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "General recommendations (简体中文)")。

感兴趣的各类程序，请参见[List of applications (简体中文)](/index.php/List_of_applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of applications (简体中文)")。