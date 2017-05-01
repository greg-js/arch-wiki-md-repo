**翻译状态：** 本文是英文页面 [Installation_guide](/index.php/Installation_guide "Installation guide") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-10-21，点击[这里](https://wiki.archlinux.org/index.php?title=Installation_guide&diff=0&oldid=463062)可以查看翻译后英文页面的改动。

本文将引导您从用官方安装镜像启动的 Live 系统安装 [Arch Linux](/index.php/Arch_Linux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Linux (简体中文)")。建议在安装前阅读 [FAQ](/index.php/FAQ_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "FAQ (简体中文)")。对于本文中使用的基本操作及术语，请参阅 [Help:Reading](/index.php/Help:Reading_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Help:Reading (简体中文)").

有关更详细的说明，请阅读本指南内相应的 [ArchWiki](/index.php/ArchWiki:About "ArchWiki:About") 文章或各类程序的[手册](/index.php/Man_page_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Man page (简体中文)")。有关配置的概述，请参阅 [archlinux(7)](https://projects.archlinux.org/svntogit/packages.git/tree/filesystem/trunk/archlinux.7.txt)。如需要交互帮助，可以使用 [IRC channel](/index.php/IRC_channel "IRC channel") 频道和 [论坛](https://bbs.archlinux.org/)。

## Contents

*   [1 安装准备](#.E5.AE.89.E8.A3.85.E5.87.86.E5.A4.87)
    *   [1.1 键盘布局](#.E9.94.AE.E7.9B.98.E5.B8.83.E5.B1.80)
    *   [1.2 验证启动模式](#.E9.AA.8C.E8.AF.81.E5.90.AF.E5.8A.A8.E6.A8.A1.E5.BC.8F)
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
    *   [3.3 时区](#.E6.97.B6.E5.8C.BA)
    *   [3.4 Locale](#Locale)
    *   [3.5 主机名](#.E4.B8.BB.E6.9C.BA.E5.90.8D)
    *   [3.6 网络配置](#.E7.BD.91.E7.BB.9C.E9.85.8D.E7.BD.AE)
    *   [3.7 Initramfs](#Initramfs)
    *   [3.8 Root 密码](#Root_.E5.AF.86.E7.A0.81)
    *   [3.9 安装引导程序](#.E5.AE.89.E8.A3.85.E5.BC.95.E5.AF.BC.E7.A8.8B.E5.BA.8F)
    *   [3.10 重启](#.E9.87.8D.E5.90.AF)
*   [4 安装后的工作](#.E5.AE.89.E8.A3.85.E5.90.8E.E7.9A.84.E5.B7.A5.E4.BD.9C)

## 安装准备

Arch Linux能在任何内存空间不小于 512MB 内存的[x86_64](https://en.wikipedia.org/wiki/X86-64 "w:X86-64")兼容机上运行。最基本的[base](https://www.archlinux.org/groups/x86_64/base/)组中包含的包将占用小于 800MB 的存储空间。由于安装过程中需要从远程存储库获取软件包，机器将需要一个有效的互联网连接。

根据 [Category:Getting and installing Arch (简体中文)](/index.php/Category:Getting_and_installing_Arch_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Getting and installing Arch (简体中文)") 中所述，下载并引导安装介质。启动完成后将会自动以 root 身份登录虚拟控制台并进入[zsh](/index.php/Zsh_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Zsh (简体中文)")命令提示符。类似 [systemctl(1)](http://man7.org/linux/man-pages/man1/systemctl.1.html) 的常规命令都可以用 `Tab` [自动补全](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion")。

如果你想切换至其它的虚拟终端来干点别的事, 例如使用 [ELinks](/index.php/ELinks "ELinks") 来查看本篇指南，使用 `Alt+*arrow*` [快捷键](/index.php/Keyboard_shortcuts_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Keyboard shortcuts (简体中文)")。可以使用 [nano](/index.php/Nano#Usage "Nano")，[vi](https://en.wikipedia.org/wiki/vi "w:vi") 或 [vim](/index.php/Vim#Usage "Vim") [编辑](/index.php/Textedit "Textedit")配置文件。

### 键盘布局

[控制台键盘布局](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") 默认为`us`（美式键盘映射）。如果您正在使用非[美式](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg")键盘布局，通过以下的命令选择相应的键盘映射表：

 `# loadkeys *layout*` 

将 *layout* 转换为您的键盘布局，如`fr`，`uk`，`dvorak`或`be-latin1`。[这里](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements "wikipedia:ISO 3166-1 alpha-2")有国家的二位字母编码表。使用命令 `ls /usr/share/kbd/keymaps/**/*.map.gz` 列出所有可用的键盘布局。

[Console fonts](/index.php/Console_fonts "Console fonts") 位于 `/usr/share/kbd/consolefonts/`, 设置方式请参考 [setfont(8)](http://man7.org/linux/man-pages/man8/setfont.8.html).

### 验证启动模式

如果以在 UEFI 主板上启用 [UEFI](/index.php/UEFI "UEFI") 模式, [Archiso](/index.php/Archiso "Archiso") 将会使用 [systemd-boot](/index.php/Systemd-boot_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd-boot (简体中文)") 来[启动](/index.php/Boot "Boot") Arch Linux。可以列出 [efivars](/index.php/UEFI#UEFI_Variables "UEFI") 目录以验证启动模式:

```
# ls /sys/firmware/efi/efivars

```

如果目录不存在，系统可能以 [BIOS](https://en.wikipedia.org/wiki/BIOS "w:BIOS") 或 CSM 模式启动，详见您的主板手册。

### 连接到因特网

守护进程 [dhcpcd](/index.php/Dhcpcd "Dhcpcd") 已被默认[启用](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules)来探测**有线**设备, 并会尝试连接。如需验证网络是否正常, 可以使用 [ping](/index.php/Ping "Ping"):

```
# ping -c 3 archlinux.org

```

若发现网络不通,利用 `systemctl stop dhcpcd@<TAB>` [停用](/index.php/Systemd#Using_units "Systemd") *dhcpcd* 进程，然后查看 [网络配置](/index.php/Network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network configuration (简体中文)").

对于**无线**连接,iw(8), wpa_supplicant(8) 和 [netctl](/index.php/Netctl#Wireless_.28WPA-PSK.29 "Netctl") 等工具已被提供. 详情查看[无线网络配置](/index.php/Wireless_network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wireless network configuration (简体中文)").

### 更新系统时间

用 [systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd") 确保系统时间是正确的：

```
# timedatectl set-ntp true

```

用 `timedatectl status` 检查服务状态.详情阅读 [Time (简体中文)](/index.php/Time_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Time (简体中文)").

参阅 [systemd-timesyncd](/index.php/Systemd-timesyncd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd-timesyncd (简体中文)")。

### 建立硬盘分区

磁盘若被系统识别到，就会被分配为一个*块设备*，如`/dev/sda`。识别这些设备，使用[lsblk](/index.php/Core_utilities#lsblk "Core utilities")或*fdisk*。输出中以`rom`, `loop` 或 `airoot` 结尾的可以被忽略。

```
# fdisk -l

```

对于一个选定的设备，以下的*分区*是必须要有的:

*   一个根分区（挂载在根目录） `/`.
*   如果 [UEFI](/index.php/UEFI "UEFI") 模式被启用,你还需要一个 [EFI 系统分区](/index.php/EFI_System_Partition "EFI System Partition").
*   [Swap](/index.php/Swap_space "Swap space") 可以在一个独立的分区上设置，也可以直接建立 [交换文件](/index.php/Swap#Swap_file "Swap").

如需修改*分区表*,使用 [fdisk](/index.php/Fdisk "Fdisk") 或 [parted](/index.php/Parted "Parted"). 查看[Partitioning (简体中文)](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Partitioning (简体中文)")以获得更多详情.

如果需要需要创建多级存储例如 [LVM](/index.php/LVM "LVM")、[LUKS](/index.php/Dm-crypt_with_LUKS "Dm-crypt with LUKS") 或 [RAID](/index.php/RAID "RAID")，请在此时完成。

### 格式化分区

当分区配置好了, 这些分区应立即被格式化并使用一个合适的[文件系统](/index.php/File_system "File system"). 例如，如果你想将`/dev/*sda1*`格式化成`*ext4*`, 使用这个命令:

```
# mkfs.*ext4* /dev/*sda1*

```

详情参见 [文件系统](/index.php/File_systems#Create_a_file_system "File systems") 和 [swap (简体中文)](/index.php/Swap_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Swap (简体中文)")。

### 挂载分区

首先将根分区[挂载](/index.php/File_systems#Mount_a_filesystem "File systems")到 `/mnt`，例如：

```
# mount /dev/*sda1* /mnt

```

如果使用多个分区，还需要为其他分区创建目录并挂载它们（`/mnt/boot`、`/mnt/home`、……）。

```
# mkdir /mnt/*boot*
# mount /dev/*sda2* /mnt/*boot*

```

如果你有[swap (简体中文)](/index.php/Swap_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Swap (简体中文)")分区，你还应该使用 [swapon(8)](http://man7.org/linux/man-pages/man8/swapon.8.html) 激活分区。当此步骤完成，`genfstab` 才能自动检测到它们。

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
# genfstab -U /mnt >> /mnt/etc/fstab

```

**强烈建议** 在执行完以上命令后，后检查一下生成的 `/mnt/etc/fstab` 文件是否正确。

### Chroot

[Change root](/index.php/Change_root "Change root") 到新安装的系统：

```
# arch-chroot /mnt /bin/bash

```

### 时区

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

另外，如果你需要修改[键盘布局](#Set_the_keyboard_layout), 并想让这个设置持续生效，编辑 [vconsole.conf(5)](http://man7.org/linux/man-pages/man5/vconsole.conf.5.html)，例如:

 `/etc/vconsole.conf`  `KEYMAP=*de-latin1*` 

### 主机名

要设置 [hostname](/index.php/Hostname "Hostname")，将其[添加](/index.php/Add "Add") 到 `/etc/hostname`, *myhostname* 是需要的主机名:

```
# echo ***myhostname*** > /etc/hostname

```

建议添加[对应的信息](/index.php/Network_configuration#Local_network_hostname_resolution "Network configuration")到[hosts(5)](http://man7.org/linux/man-pages/man5/hosts.5.html):

 `/etc/hosts` 
```
127.0.0.1	localhost.localdomain	localhost
::1		localhost.localdomain	localhost
**127.0.1.1	*myhostname*.localdomain	*myhostname***

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

[启动加载器](/index.php/Boot_loaders_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Boot loaders (简体中文)")页面介绍了可用选项和配置方法。包括 [GRUB (简体中文)](/index.php/GRUB_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GRUB (简体中文)") (BIOS/UEFI), [systemd-boot (简体中文)](/index.php/Systemd-boot_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd-boot (简体中文)") (UEFI) 和 [Syslinux (简体中文)](/index.php/Syslinux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Syslinux (简体中文)") (BIOS)等.

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