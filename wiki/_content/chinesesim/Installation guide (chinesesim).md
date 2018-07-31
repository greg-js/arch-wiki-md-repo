**翻译状态：** 本文是英文页面 [Installation_guide](/index.php/Installation_guide "Installation guide") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-07-29，点击[这里](https://wiki.archlinux.org/index.php?title=Installation_guide&diff=0&oldid=529413)可以查看翻译后英文页面的改动。

本文将指导如何用官方安装镜像启动的 Live 系统安装 [Arch Linux](/index.php/Arch_Linux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Linux (简体中文)")。建议在安装前阅读 [FAQ](/index.php/FAQ_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "FAQ (简体中文)")。对于本文中使用的惯用术语，请参阅 [Help:Reading](/index.php/Help:Reading_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Help:Reading (简体中文)").请注意, 代码段可能会有占位符(格式是 `*italics*`),你可能需要手动去掉它们.

有关更详细的说明，请阅读本指南内相应的 [ArchWiki](/index.php/ArchWiki:About_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki:About (简体中文)") 文章或各类程序的[手册](/index.php/Man_page_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Man page (简体中文)")。有关配置的概述，请参阅 [archlinux(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/archlinux.7)。若需要交互帮助，可以使用 [IRC 频道](/index.php/IRC_channel "IRC channel")和[论坛](https://bbs.archlinux.org/)。

Arch Linux 能在任何内存空间不小于 512MB 的 [x86_64](https://en.wikipedia.org/wiki/zh:X86-64 "w:zh:X86-64") 兼容机上运行。用 [base](https://www.archlinux.org/groups/x86_64/base/) 组内的软件包进行的基本安装将占用小于 800MB 的存储空间。由于安装过程中需要从远程存储库获取软件包，机器将需要一个有效的互联网连接。

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
    *   [3.4 本地化](#.E6.9C.AC.E5.9C.B0.E5.8C.96)
    *   [3.5 主机名](#.E4.B8.BB.E6.9C.BA.E5.90.8D)
    *   [3.6 网络配置](#.E7.BD.91.E7.BB.9C.E9.85.8D.E7.BD.AE)
    *   [3.7 Initramfs](#Initramfs)
    *   [3.8 Root 密码](#Root_.E5.AF.86.E7.A0.81)
    *   [3.9 安装引导程序](#.E5.AE.89.E8.A3.85.E5.BC.95.E5.AF.BC.E7.A8.8B.E5.BA.8F)
*   [4 重启](#.E9.87.8D.E5.90.AF)
*   [5 安装后的工作](#.E5.AE.89.E8.A3.85.E5.90.8E.E7.9A.84.E5.B7.A5.E4.BD.9C)

## 安装准备

根据 [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Getting and installing Arch (简体中文)") 中所述，下载并引导安装介质。启动完成后将会自动以 root 身份登录虚拟控制台并进入 [Zsh](/index.php/Zsh_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Zsh (简体中文)") 命令提示符。

如果你想切换至其它的虚拟终端来干点别的事, 例如使用 [ELinks](/index.php/ELinks "ELinks") 来查看本篇指南，使用 `Alt+*方向鍵*` [快捷键](/index.php/Keyboard_shortcuts_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Keyboard shortcuts (简体中文)")。可以使用 [nano](/index.php/Nano#Usage "Nano")，[vi](https://en.wikipedia.org/wiki/vi "w:vi") 或 [vim](/index.php/Vim#Usage "Vim") [编辑](/index.php/Textedit "Textedit")配置文件。

### 键盘布局

[控制台键盘布局](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") 默认为`us`（美式键盘映射）。列出所有可用的键盘布局, 可以使用:

```
# ls /usr/share/kbd/keymaps/**/*.map.gz

```

如果您想要更改键盘布局,可以将一致的文件名添加进[loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1), 但请省略路径和扩展名. 比如, 要添加[German](https://en.wikipedia.org/wiki/File:KB_Germany.svg "wikipedia:File:KB Germany.svg")键盘布局:

```
# loadkeys de-latin1

```

[Console fonts](/index.php/Console_fonts "Console fonts") 位于 `/usr/share/kbd/consolefonts/`, 设置方式请参考 [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8).

### 验证启动模式

如果以在 UEFI 主板上启用 [UEFI](/index.php/UEFI "UEFI") 模式, [Archiso](/index.php/Archiso "Archiso") 将会使用 [systemd-boot](/index.php/Systemd-boot_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd-boot (简体中文)") 来[启动](/index.php/Boot "Boot") Arch Linux。可以列出 [efivars](/index.php/UEFI#UEFI_variables "UEFI") 目录以验证启动模式:

```
# ls /sys/firmware/efi/efivars

```

如果目录不存在，系统可能以 [BIOS](https://en.wikipedia.org/wiki/BIOS "w:BIOS") 或 CSM 模式启动，详见您的主板手册。

### 连接到因特网

守护进程 [dhcpcd](/index.php/Dhcpcd "Dhcpcd") 已被默认启用来探测[有线网络设备](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules), 并会尝试连接。 可以使用 [ping](/index.php/Ping "Ping") 验证连接是否正常:

```
# ping archlinux.org

```

如果没有可用网络连接,利用 `systemctl stop dhcpcd@*网络接口*`,`TAB` [停用](/index.php/Systemd#Using_units "Systemd") *dhcpcd* 进程，`*网络接口*` 名可以通过 [Tab补全](https://en.wikipedia.org/wiki/Command-line_completion "wikipedia:Command-line completion").。要配置网络，详见[网络配置](/index.php/Network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network configuration (简体中文)").

### 更新系统时间

使用 [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) 确保系统时间是准确的：

```
# timedatectl set-ntp true

```

可以使用 `timedatectl status` 检查服务状态。

### 建立硬盘分区

磁盘若被系统识别到，就会被分配为一个[块设备](https://en.wikipedia.org/wiki/zh:%E8%AE%BE%E5%A4%87%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F#.E5.91.BD.E5.90.8D.E7.BA.A6.E5.AE.9A "wikipedia:zh:设备文件系统")，如`/dev/sda`或者`/dev/nvme0n1`。可以使用 [lsblk](/index.php/Lsblk "Lsblk") 或者 *fdisk* 查看:

```
# fdisk -l

```

结果中以`rom`, `loop` 或者 `airoot`结束的可以被忽略。

对于一个选定的设备，以下的*分区*是必须要有的:

*   一个根分区（挂载在根目录） `/`.
*   如果 [UEFI](/index.php/UEFI "UEFI") 模式被启用,你还需要一个 [EFI 系统分区](/index.php/EFI_system_partition "EFI system partition").

**注意:** [Swap](/index.php/Swap_space "Swap space") 可以在一个独立的分区上设置，也可以直接建立 [交换文件](/index.php/Swap#Swap_file "Swap").

如需修改*分区表*,使用 [fdisk](/index.php/Fdisk "Fdisk") 或 [parted](/index.php/Parted "Parted").

```
# fdisk /dev/*sda*

```

查看[硬盘分区](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Partitioning (简体中文)")以获得更多详情.

**注意:** 如果需要需要创建多级存储例如 [LVM](/index.php/LVM "LVM")、[disk encryption](/index.php/Disk_encryption "Disk encryption") 或 [RAID](/index.php/RAID "RAID")，请在此时完成。

### 格式化分区

当分区建立好了, 这些分区都需要使用适当的[文件系统](/index.php/File_systems_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "File systems (简体中文)")进行格式化。举个例子，如果想将`/dev/*sda1*`格式化成`*ext4*`, 可以运行:

```
# mkfs.*ext4* /dev/*sda1*

```

如果您创建了交换分区（例如`/dev/*sda3*`），使用 mkswap 将其初始化：

```
# mkswap /dev/*sda3*
# swapon /dev/*sda3*

```

详情参见[文件系统](/index.php/File_systems_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.88.9B.E5.BB.BA.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F "File systems (简体中文)")。

### 挂载分区

首先将根分区[挂载](/index.php/Mount "Mount")到 `/mnt`，例如：

```
# mount /dev/*sda1* /mnt

```

如果使用多个分区，还需要为其他分区创建目录并挂载它们（`/mnt/boot`、`/mnt/home`、……）。

```
# mkdir /mnt/*boot*
# mount /dev/*sda2* /mnt/*boot*

```

接下来 [genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in) 将会自动检测挂载的文件系统和 swap 分区。

## 安装

### 选择镜像

文件`/etc/pacman.d/mirrorlist`定义了软件包会从哪个[镜像源](/index.php/Mirrors "Mirrors")下载.在LiveCD启动的系统上,所有的镜像都被启用,并且在镜像被制作时,我们已经通过他们的同步情况和速度排序.

在列表中越前的镜像在下载软件包时有越高的优先权. 你可以相应的修改文件`/etc/pacman.d/mirrorlist`, 并将地理位置最近的镜像源挪到文件的头部, 同时你也应该考虑一些其他标准。

这个文件接下来还会被*pacstrap*拷贝到新系统里, 所以请确保设置正确。

### 安装基本系统

使用[pacstrap](https://git.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) 脚本，安装 [base](https://www.archlinux.org/groups/x86_64/base/) 组：

```
# pacstrap /mnt base

```

这个组并没有包含全部 live 环境中的程序，有些需要额外安装，例如[btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs)。[packages.x86_64](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) 页面包含了它们的差异。

如果你还想安装其他软件包组比如[base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), 请将他们的名字添加到*pacstrap*后,并用空格隔开.你也可以在[#Chroot](#Chroot)之后使用[pacman](/index.php/Pacman "Pacman")手动安装软件包或组.

```
# pacstrap -i /mnt base base-devel

```

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
# arch-chroot /mnt

```

### 时区

设置 [时区](/index.php/Time_zone "Time zone"):

```
# ln -sf /usr/share/zoneinfo/*Region*/*City* /etc/localtime

```

例如：

```
# ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

```

运行[hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8)以生成`/etc/adjtime`:

```
# hwclock --systohc

```

这个命令假定硬件时间已经被设置为[UTC时间](https://en.wikipedia.org/wiki/UTC "wikipedia:UTC"). 详细信息请查看[Time#Time standard](/index.php/Time#Time_standard "Time").

### 本地化

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

`/etc/locale.gen` 会生成指定的本地化文件.

创建 `locale.conf` 并编辑：`LANG` [变量](/index.php/Variable "Variable"),比如:

**Tip:** 将系统 locale 设置为`en_US.UTF-8`，系统的 Log 就会用英文显示，这样更容易问题的判断和处理。用户可以设置自己的 locale，详情参阅[Locale](/index.php/Locale#Overriding_system_locale_per_user_session "Locale")或[Locale_(简体中文)#设置 locale](/index.php/Locale_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E8.AE.BE.E7.BD.AE_locale "Locale (简体中文)")
 `/etc/locale.conf`  `LANG=*en_US.UTF-8*` 
**警告:** 不推荐在此设置任何中文locale，或导致tty乱码。

另外，如果你需要修改[键盘布局](#Set_the_keyboard_layout), 并想让这个设置持续生效，编辑 [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5)，例如:

 `/etc/vconsole.conf`  `KEYMAP=*de-latin1*` 

### 主机名

要设置 [hostname](/index.php/Hostname "Hostname")，将其[添加](/index.php/Add "Add") 到 `/etc/hostname`, *myhostname* 是需要的主机名:

 `/etc/hostname` 
```
*myhostname*

```

并且添加[对应的信息](/index.php/Network_configuration#Local_network_hostname_resolution "Network configuration")到[hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5):

 `/etc/hosts` 
```
127.0.0.1	localhost
::1		localhost
127.0.1.1	*myhostname*.localdomain	*myhostname*

```

如果机器有一个永久的ip地址,请使用这个ip而不是`127.0.1.1`.

### 网络配置

对新安装的系统，需要再次设置网络。具体请参考 [Network configuration (简体中文)](/index.php/Network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network configuration (简体中文)")

对于 [无线网络配置](/index.php/Wireless_network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wireless network configuration (简体中文)")，[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [iw](https://www.archlinux.org/packages/?name=iw), [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant)，[dialog](https://www.archlinux.org/packages/?name=dialog) 以及需要的 [固件软件包](/index.php/Wireless#Installing_driver.2Ffirmware "Wireless").

### Initramfs

你通常不需要创建*initramfs*,因为在你执行*pacstrap*时已经安装[linux](https://www.archlinux.org/packages/?name=linux), 这时[mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")会被自动运行.

如果修改了 [mkinitcpio.conf](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mkinitcpio (简体中文)")，用以下命令创建一个Initramfs：

```
# mkinitcpio -p linux

```

### Root 密码

设置 root [密码](/index.php/Password "Password"):

```
# passwd

```

### 安装引导程序

你需要安装Linux引导程序以在安装后启动系统,你可以使用的的引导程序在["启动加载器"](/index.php/Boot_loaders_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Boot loaders (简体中文)")中,请选择一个并且安装并配置它,比如[GRUB](/index.php/GRUB "GRUB").

如果你使用Intel CPU，那么需要安装[intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode)并[启用英特尔微码更新](/index.php/Microcode#Enabling_Intel_microcode_updates "Microcode")

## 重启

输入 `exit` 或按 `Ctrl+D` 退出 chroot 环境。

可选用 `umount -R /mnt` 手动卸载被挂载的分区：这有助于发现任何“繁忙”的分区，并通过 [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1) 查找原因。

最后，通过执行 `reboot` 重启系统：*systemd* 将自动卸载仍然挂载的任何分区。不要忘记移除安装介质，然后使用root帐户登录到新系统。

## 安装后的工作

系统管理引导，图形用户界面的安装、声音管理、触摸板支持等后期工作参见 [General recommendations (简体中文)](/index.php/General_recommendations_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "General recommendations (简体中文)")。

感兴趣的各类程序，请参见[List of applications (简体中文)](/index.php/List_of_applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of applications (简体中文)")。