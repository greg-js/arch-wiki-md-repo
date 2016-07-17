**翻译状态：** 本文是英文页面 [Installation_guide](/index.php/Installation_guide "Installation guide") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-11-20，点击[这里](https://wiki.archlinux.org/index.php?title=Installation_guide&diff=0&oldid=408953)可以查看翻译后英文页面的改动。

本文将引导您从用官方安装镜像启动的 Live 系统安装 [Arch Linux](/index.php/Arch_Linux "Arch Linux")。安装之前请先阅读 [FAQ (简体中文)](/index.php/FAQ_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "FAQ (简体中文)")。如需更丰富更详细的安装指导，请参考 [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide")。 [Category:Getting and installing Arch (简体中文)](/index.php/Category:Getting_and_installing_Arch_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Getting and installing Arch (简体中文)") 包含了更多针对特殊情况的安装指南。

[Arch wiki](/index.php/Main_page_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Main page (简体中文)") 是由社区维护的优秀资源，当您遇到各种问题，这是您的首选参考资料。如需要交互帮助，还可以通过 [IRC channel](/index.php/IRC_channel "IRC channel") 频道和 [论坛](https://bbs.archlinux.org/) 。此外，在使用您不熟悉的命令之前，请务必首先阅读该命令对应的 `man` 文件。查看该文件的方法很简单，通常只需要 `man *要查看的命令*` 即可。

## Contents

*   [1 安装准备](#.E5.AE.89.E8.A3.85.E5.87.86.E5.A4.87)
    *   [1.1 键盘布局](#.E9.94.AE.E7.9B.98.E5.B8.83.E5.B1.80)
    *   [1.2 连接到因特网](#.E8.BF.9E.E6.8E.A5.E5.88.B0.E5.9B.A0.E7.89.B9.E7.BD.91)
    *   [1.3 更新系统时间](#.E6.9B.B4.E6.96.B0.E7.B3.BB.E7.BB.9F.E6.97.B6.E9.97.B4)
    *   [1.4 建立硬盘分区](#.E5.BB.BA.E7.AB.8B.E7.A1.AC.E7.9B.98.E5.88.86.E5.8C.BA)
    *   [1.5 格式化分区](#.E6.A0.BC.E5.BC.8F.E5.8C.96.E5.88.86.E5.8C.BA)
    *   [1.6 挂载分区](#.E6.8C.82.E8.BD.BD.E5.88.86.E5.8C.BA)
*   [2 安装](#.E5.AE.89.E8.A3.85)
    *   [2.1 选择镜像](#.E9.80.89.E6.8B.A9.E9.95.9C.E5.83.8F)
    *   [2.2 安装基本系统](#.E5.AE.89.E8.A3.85.E5.9F.BA.E6.9C.AC.E7.B3.BB.E7.BB.9F)
    *   [2.3 配置系统](#.E9.85.8D.E7.BD.AE.E7.B3.BB.E7.BB.9F)
    *   [2.4 安装引导程序](#.E5.AE.89.E8.A3.85.E5.BC.95.E5.AF.BC.E7.A8.8B.E5.BA.8F)
    *   [2.5 重启](#.E9.87.8D.E5.90.AF)
*   [3 安装后的工作](#.E5.AE.89.E8.A3.85.E5.90.8E.E7.9A.84.E5.B7.A5.E4.BD.9C)

## 安装准备

[Category:Getting and installing Arch (简体中文)](/index.php/Category:Getting_and_installing_Arch_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Getting and installing Arch (简体中文)") 中包含了下载和启动安装介质的说明, 参考本指引后续内容处理剩余的安装过程。镜像中不包含软件包，安装的软件是通过服务器上的源下载，所以安装的时候必须要有网络连接。

### 键盘布局

默认键盘布局是 US 键盘, 可以通过 `loadkeys "keymap_name"` 的命令切换键盘布局，键盘映射表请查看 `/usr/share/kbd/keymaps/`。

### 连接到因特网

所有有线网络连接都启用了 `dhcpcd`。如果您希望使用静态 IP，或使用 [Netctl](/index.php/Netctl "Netctl") 等管理工具，请先运行`systemctl stop dhcpcd.service`停止该服务。获取更多信息请访问[Network configuration (简体中文)](/index.php/Network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network configuration (简体中文)")。

运行 `wifi-menu` 设置无线网络。详情参见 [Wireless network configuration (简体中文)](/index.php/Wireless_network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wireless network configuration (简体中文)") 和 [Netctl (简体中文)](/index.php/Netctl_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Netctl (简体中文)")。

### 更新系统时间

参阅 [systemd-timesyncd](/index.php/Systemd-timesyncd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd-timesyncd (简体中文)")。

### 建立硬盘分区

详情参见 [Partitioning (简体中文)](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Partitioning (简体中文)")；可能需要一些特别的分区，详情请参阅[在 Linux 上创建 EFI 系统分区](/index.php/UEFI#EFI_System_Partition "UEFI")以及[GRUB BIOS boot partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB")(英文)；如果需要需要创建多级存储，请参考 [LVM](/index.php/LVM "LVM")、[LUKS](/index.php/Dm-crypt_with_LUKS "Dm-crypt with LUKS") 或 [RAID](/index.php/RAID "RAID")。

### 格式化分区

详情参见 [文件系统](/index.php/Format_a_device#Step_2:_create_the_new_file_system "Format a device") 和 [swap (简体中文)](/index.php/Swap_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Swap (简体中文)")。

如果您正在使用(U)EFI，您很可能需要另外一个分区来放置UEFI系统分区。请阅读[这篇文章](/index.php/Unified_Extensible_Firmware_Interface#Create_an_UEFI_System_Partition_in_Linux "Unified Extensible Firmware Interface")。

### 挂载分区

将分区挂载到`/mnt`，如果使用多个分区，还需要为其他分区创建目录并挂载它们（`/mnt/boot`、`/mnt/home`、……）。激活 *swap* 分区，这样 `genfstab` 才能自动检测到它们。

## 安装

### 选择镜像

编辑 `/etc/pacman.d/mirrorlist`，选择您的首选 [mirror](/index.php/Mirrors "Mirrors"). 这个 mirror 列表也将通过 `pacstrap` 被复制并保存在到系统中，所以请确保设置正确。

### 安装基本系统

使用 [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) 安装[base](https://www.archlinux.org/groups/x86_64/base/) 软件组。

```
# pacstrap /mnt base

```

其它软件包可以通过将其包名添加到上述命令安装（用空格隔开）。

### 配置系统

用以下命令生成 [fstab](/index.php/Fstab "Fstab") 文件 (用 `-U` 或 `-L` 选项设置UUID 或卷标)：

```
# genfstab -U -p /mnt >> /mnt/etc/fstab

```

[Change root](/index.php/Change_root "Change root") 到新安装的系统：

```
# arch-chroot /mnt /bin/bash

```

设置 [主机名](/index.php/Hostname "Hostname"):

```
# echo *computer_name* > /etc/hostname

```

设置 [时区](/index.php/Time_zone "Time zone"):

```
# ln -s /usr/share/zoneinfo/*zone*/*subzone* /etc/localtime

```

例如：

```
# ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

```

编辑 `/etc/locale.gen`，反注释需要的 locale，并用 `locale-gen` 生成正确的 locale 信息。

在 `/etc/locale.conf` 里设置系统[locale](/index.php/Locale#Setting_the_system_locale "Locale")偏好；单个用户请设置`$HOME/.config/locale.conf`:

```
# echo LANG=*your_locale* > /etc/locale.conf

```

在 `/etc/vconsole.conf` 中加入[控制台键盘映射](/index.php/KEYMAP "KEYMAP")和[字体](/index.php/Fonts_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E7.BB.88.E7.AB.AF.E5.AD.97.E4.BD.93 "Fonts (简体中文)")偏好。

对新安装的系统，需要再次设置网络。具体请参考 [Network configuration (简体中文)](/index.php/Network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network configuration (简体中文)") 和 [Wireless network configuration (简体中文)](/index.php/Wireless_network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wireless network configuration (简体中文)")。

必要时配置 `/etc/mkinitcpio.conf` （参见 [mkinitcpio (简体中文)](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mkinitcpio (简体中文)")），然后用以下命令创建一个初始 RAM disk：

```
# mkinitcpio -p linux

```

设置 root 密码:

```
# passwd

```

### 安装引导程序

可用的引导程序及其配置请参考[Boot loaders (简体中文)](/index.php/Boot_loaders_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Boot loaders (简体中文)")。

### 重启

输入 `exit` 或按 `Ctrl+D` 退出 chroot。

可选，卸载挂载的分区，如果有问题可以通过[fuser](https://en.wikipedia.org/wiki/fuser_(Unix) "wikipedia:fuser (Unix)")检查。

```
# umount -R /mnt

```

现在重启系统，移除安装介质并执行`reboot`，新系统启动后用 root 登录。

## 安装后的工作

系统管理引导，图形用户界面的安装、声音管理、触摸板支持等后期工作参见 [General recommendations (简体中文)](/index.php/General_recommendations_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "General recommendations (简体中文)")。

感兴趣的各类程序，请参见[List of applications (简体中文)](/index.php/List_of_applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of applications (简体中文)")。