相关文章

*   [安装指南](/index.php/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Installation guide (简体中文)")
*   [一般建议](/index.php/General_recommendations_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "General recommendations (简体中文)")
*   [General troubleshooting](/index.php/General_troubleshooting "General troubleshooting")

**翻译状态：** 本文是英文页面 [Installing_Arch_Linux_on_a_USB_key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-9-9，点击[这里](https://wiki.archlinux.org/index.php?title=Installing_Arch_Linux_on_a_USB_key&diff=0&oldid=398959)可以查看翻译后英文页面的改动。

本页讨论如何在U盘(闪存盘)上安装一个常规的 Arch，这里的系统是指一个可以升级和使用的系统，而不是一个用来引导系统启动的[USB 安装媒介](/index.php/USB_Installation_Media_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "USB Installation Media (简体中文)")。

## Contents

*   [1 准备](#准备)
*   [2 安装](#安装)
*   [3 配置](#配置)
    *   [3.1 GRUB legacy](#GRUB_legacy)
    *   [3.2 GRUB](#GRUB)
    *   [3.3 Syslinux](#Syslinux)
*   [4 小技巧](#小技巧)
    *   [4.1 在多个机器上使用优盘](#在多个机器上使用优盘)
        *   [4.1.1 架构](#架构)
        *   [4.1.2 输入设备](#输入设备)
        *   [4.1.3 显卡驱动](#显卡驱动)
    *   [4.2 兼容性](#兼容性)
        *   [4.2.1 持久块设备命名](#持久块设备命名)
        *   [4.2.2 内核参数](#内核参数)
        *   [4.2.3 从USB3.0 介质中启动](#从USB3.0_介质中启动)
    *   [4.3 最小化磁盘访问](#最小化磁盘访问)
*   [5 参阅](#参阅)

## 准备

如果打算安装 KDE 之类大容量的应用程序，建议至少准备一个 3GiB 的U盘。GNOME 和 Xfce4 的话，如果只安装常用桌面包，(GIMP, Pidgin, OpenOffice, Firefox, flashplugin)，可以安装到 2GiB U盘中，给用户数据留一些空间。

将 Arch 安装到 USB 有多种方式，最简单的方法是从 Arch 中安装：

*   启动到 Arch 系统中，[安装](/index.php/Pacman "Pacman") 软件包 [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts)，然后按照 [安装指南](/index.php/Installation_guide "Installation guide") 进行安装。只不过安装的目标不再是 `/dev/sda`. 通过 `$ lsblk` 确定优盘对应的 `/dev/sd*` 设备号。

**警告:** 如果错误的格式化了`/dev/sda`，整个硬盘数据都会丢失。

*   启动到 Arch 安装光盘/优盘，安装目标是另外一个优盘。
*   如果你有别的 linux 电脑（不一定是 Arch),你也可以参考这篇文章 [从现有的 Linux 系统进行安装](/index.php/Install_from_existing_Linux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Install from existing Linux (简体中文)")，并跳过配置部分。
*   如果你运行Windows或OS X，可以通过VirtualBox引导Arch的Live ISO，然后将U盘连接到虚拟机上进行安装。

## 安装

按照[安装指南](/index.php/Installation_guide "Installation guide")进行安装，仅需注意以下几点：

*   如果 cfdisk 由于 "Partition ends in the final partial cylinder" 这个错误失败，唯一的解决方法就是干掉U盘上的所有分区。打开另一个终端(Alt+F2)，输入 fdisk /dev/sdX (sdX 对应你的 U盘)，显示分区表(p)，查看，删除掉已存在的分区(d)然后保存修改(w)。最后，再进 cfdisk。
*   强烈建议，关于如何选择文件系统的问题，请先阅读一下 [SSD](/index.php/SSD "SSD") 这篇文章 [关于优化 SSD 固态硬盘读写的技巧](/index.php/SSD#Tips_for_minimizing_disk_reads/writes "SSD")，总地来说，不带日志(journal)功能的 ext4 是比较通用的优选方案。可以用这样的命令来创建：`# mkfs.ext4 -O "^has_journal" /dev/sdXX`。因为带日志功能的文件系统日志更新会在一定程度上消耗闪存有限的写入寿命。由于同样的原因，最好放弃 swap 分区。注意这个建议并不适用于安装在 USB(机械)硬盘的情况。
*   用 `# mkinitcpio -p linux`创建 RAM Disk 前，在修改 `/etc/mkinitcpio.conf`，将 `block` 添加到紧挨 udev 的后面. 只有这样早期用户空间才能正确的装入模块。
*   如果想在其它操作系统上继续使用优盘，可以使用 NTFS 或 exFAT 创建数据分区. 数据分区需要是设备的第一个分区，因为 Windows 会假定移动设备仅有一个分区。需要安装 [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) 和 [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g).网上有一些工具可以翻转U盘的可移动媒体位使得操作系统把它当作额外的硬盘，这样你就可以使用你选择的任意磁盘划分方式。

**警告:** 因为不是所有的U盘都可以翻转可移动媒体位而且使用不成熟的软件进行操作可能会损坏你的设备，所以不推荐使用翻转可移动媒体位的方法

*   安装[NetworkManager](/index.php/NetworkManager "NetworkManager")来管理网络，它可以改变不同硬件的接口名称

## 配置

请确认在 /etc/fstab 中的 / 目录分区信息和 U盘中的所有分区信息都要正确。如果这个U盘会用来启动多台电脑，建议使用[UUID](/index.php/UUID "UUID")方式生成[fstab](/index.php/Fstab "Fstab") 和启动管理器配置，详情参阅 [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming")。

使用**blkid**可以获取各个分区的 UUID 属性,当前的 GRUB已经默认使用 UUID。

**注意:**

*   如果U盘上安装了 GRUB，U盘总是 `hd0,0`。
*   当前版本的GRUB默认使用UUID，下面的指南是针对GRUB legacy的。

### GRUB legacy

GRUB legacy的配置文件`menu.lst` 应该大致如下进行编辑:

使用固定的`/dev/sda*X*`:

```
root (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/sda1 ro
initrd /boot/initramfs-linux.img

```

使用标签时，你的配置文件应该像这样:

```
root (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/disk/by-label/**Arch** ro
initrd /boot/initramfs-linux.img

```

使用UUID时应该像这样:

```
root (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/disk/by-uuid/3a9f8929-627b-4667-9db4-388c4eaaf9fa ro
initrd /boot/initramfs-linux.img

```

### GRUB

对于MBR系统，假设你的U盘的设备名称为/dev/sdy1：

```
# mkdir -p /mnt/usb ; mount /dev/sdy1 /mnt/usb
# grub-install --target=i386-pc --recheck --debug --boot-directory=/mnt/usb/boot /dev/sdy
# grub-mkconfig -o /mnt/usb/boot/grub/grub.cfg

```

```
# optional, backup config files of grub.cfg
# mkdir -p /mnt/usb/etc/default
# cp /etc/default/grub /mnt/usb/etc/default
# cp -a /etc/grub.d /mnt/usb/etc

```

```
# sync; umount /mnt/usb

```

如果希望在运行UEFI的计算机上运行，确定你遵循了[GRUB#UEFI systems](/index.php/GRUB#UEFI_systems "GRUB")的说明，并加上--removable 选项（否则可能会损坏已有的GRUB安装），例如：

```
# grub-install --target=x86_64-efi --efi-directory=$esp --bootloader-id=grub **--removable** --recheck

```

### Syslinux

使用固定的`/dev/sda*X*`:

```
LABEL Arch
        MENU LABEL Arch Linux
        LINUX ../vmlinuz-linux
        APPEND root=/dev/sdax ro
        INITRD ../initramfs-linux.img

```

使用UUID:

```
LABEL Arch
        MENU LABEL Arch Linux
        LINUX ../vmlinuz-linux
        APPEND root=UUID=3a9f8929-627b-4667-9db4-388c4eaaf9fa ro
        INITRD ../initramfs-linux.img

```

## 小技巧

### 在多个机器上使用优盘

#### 架构

i686 架构可以在 32位和 64位系统上使用，而且 32位二进制软件包会减少空间占用。

**注意:** 如果要 Chroot 到 64 位系统（例如进行安装或系统修复），必须使用 x86_64 Arch.

#### 输入设备

要支持笔记本，请安装 [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics)，详情参阅 [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

#### 显卡驱动

不要使用非开源驱动，建议安装的驱动： [xf86-video-vesa](https://www.archlinux.org/packages/?name=xf86-video-vesa) [mesa](https://www.archlinux.org/packages/?name=mesa) [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) [xf86-video-nv](https://aur.archlinux.org/packages/xf86-video-nv/).

同时安装32位软件库：[lib32-ati-dri](https://www.archlinux.org/packages/?name=lib32-ati-dri) [lib32-intel-dri](https://www.archlinux.org/packages/?name=lib32-intel-dri) [lib32-nouveau-dri](https://www.archlinux.org/packages/?name=lib32-nouveau-dri).

### 兼容性

使用 fallback 内核可以获得最大的兼容性。

#### 持久块设备命名

推荐在[fstab](/index.php/Fstab_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fstab (简体中文)")和启动管理器的配置文件中都使用持久块设备命名法,参阅[Persistent block device naming (简体中文)](/index.php/Persistent_block_device_naming_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Persistent block device naming (简体中文)")获得更多细节.

或者,你可以自行创建udev规则为你的U盘创建符号链接并将其用于fstab和启动管理器的配置文件中,参阅[udev#Setting static device names](/index.php/Udev#Setting_static_device_names "Udev")获得更多信息.

#### 内核参数

你也许因为遇到过空白屏幕,"no signal"错误或是其他原因希望禁用KMS(特别是在某些Intel视频卡上).要禁用KMS,加入`nomodeset`内核参数.你也许希望了解[内核参数](/index.php/Kernel_parameters "Kernel parameters")的详细信息.

**Warning:** KMS禁用时某些[Xorg](/index.php/Xorg "Xorg")驱动无法正常工作.请在对应的wiki页面上查找详细信息.特别对于Nouveau(它依靠KMS来决定正确的分辨率),如果你在有Nvidia显示卡的电脑上禁用了KMSd,你可能必须手动调整分辨率.参阅[Xrandr](/index.php/Xrandr "Xrandr")获得更多信息.

#### 从USB3.0 介质中启动

参阅 [[1]](http://www.wyae.de/docs/boot-usb3/).

### 最小化磁盘访问

*   你也许希望[journald](/index.php/Systemd#Journal "Systemd")将日志储存到内存中,例如新建这样的配置文件来实现 :

 `/etc/systemd/journald.conf.d/usbstick.conf` 
```
[Journal]
Storage=volatile
RuntimeMaxUse=30M
```

*   要在web浏览器或者其他应用没有写入关键数据时停用`fsync`和相关的系统调用,可以使用来自[libeatmydata](https://aur.archlinux.org/packages/libeatmydata/)的*eatmydata*来避免过多的系统调用:

```
$ eatmydata firefox

```

## 参阅

*   [Installing Arch Linux from VirtualBox](/index.php/Installing_Arch_Linux_from_VirtualBox "Installing Arch Linux from VirtualBox")
*   [固态硬盘](/index.php/%E5%9B%BA%E6%80%81%E7%A1%AC%E7%9B%98 "固态硬盘")