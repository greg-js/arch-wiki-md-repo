**翻译状态：** 本文是英文页面 [Archboot](/index.php/Archboot "Archboot") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-12-16，点击[这里](https://wiki.archlinux.org/index.php?title=Archboot&diff=0&oldid=229273)可以查看翻译后英文页面的改动。

## Contents

*   [1 Archboot是什么?](#Archboot.E6.98.AF.E4.BB.80.E4.B9.88.3F)
*   [2 安装](#.E5.AE.89.E8.A3.85)
*   [3 Archboot的发布](#Archboot.E7.9A.84.E5.8F.91.E5.B8.83)
    *   [3.1 Supported boot modes of Archboot media](#Supported_boot_modes_of_Archboot_media)
    *   [3.2 烧录发布](#.E7.83.A7.E5.BD.95.E5.8F.91.E5.B8.83)
    *   [3.3 PXE 启动 / 恢复系统](#PXE_.E5.90.AF.E5.8A.A8_.2F_.E6.81.A2.E5.A4.8D.E7.B3.BB.E7.BB.9F)
    *   [3.4 News](#News)
        *   [3.4.1 General](#General)
        *   [3.4.2 Environment changes](#Environment_changes)
        *   [3.4.3 setup changes](#setup_changes)
        *   [3.4.4 quickinst changes](#quickinst_changes)
    *   [3.5 历史](#.E5.8E.86.E5.8F.B2)
    *   [3.6 与正式发布的区别](#.E4.B8.8E.E6.AD.A3.E5.BC.8F.E5.8F.91.E5.B8.83.E7.9A.84.E5.8C.BA.E5.88.AB)
    *   [3.7 设置特性](#.E8.AE.BE.E7.BD.AE.E7.89.B9.E6.80.A7)
    *   [3.8 启动参数](#.E5.90.AF.E5.8A.A8.E5.8F.82.E6.95.B0)
        *   [3.8.1 通用启动参数](#.E9.80.9A.E7.94.A8.E5.90.AF.E5.8A.A8.E5.8F.82.E6.95.B0)
        *   [3.8.2 视频和framebuffer 选项](#.E8.A7.86.E9.A2.91.E5.92.8Cframebuffer_.E9.80.89.E9.A1.B9)
    *   [3.9 问题, Known Issues and limitations](#.E9.97.AE.E9.A2.98.2C_Known_Issues_and_limitations)
    *   [3.10 UEFI 参考](#UEFI_.E5.8F.82.E8.80.83)
    *   [3.11 Bugs](#Bugs)
*   [4 链接](#.E9.93.BE.E6.8E.A5)
*   [5 Usbstick 恢复](#Usbstick_.E6.81.A2.E5.A4.8D)
*   [6 建立镜像文件](#.E5.BB.BA.E7.AB.8B.E9.95.9C.E5.83.8F.E6.96.87.E4.BB.B6)
    *   [6.1 如何建立Archboot Allinone ISO](#.E5.A6.82.E4.BD.95.E5.BB.BA.E7.AB.8BArchboot_Allinone_ISO)
        *   [6.1.1 前提条件](#.E5.89.8D.E6.8F.90.E6.9D.A1.E4.BB.B6)
        *   [6.1.2 建立archboot chroots](#.E5.BB.BA.E7.AB.8Barchboot_chroots)
        *   [6.1.3 安装和更新archboot](#.E5.AE.89.E8.A3.85.E5.92.8C.E6.9B.B4.E6.96.B0archboot)
        *   [6.1.4 生成镜像](#.E7.94.9F.E6.88.90.E9.95.9C.E5.83.8F)

## Archboot是什么?

*   Archboot是一组启动CD/USB/PXE等启动介质的脚本。
*   它用来安装或者恢复系统。它带有TUI界面，适合新手使用
*   它不依赖于任何文件系统，只能运行在内存中，因此需要你有足够的内存。

## 安装

 `pacman -S archboot` 

## Archboot的发布

*   提供ISO镜像文件和BT种子，并且包含i686和x86_64的core库。
*   请阅读变更记录文件（Changelog）来确认对内存的需求。
*   使用前请检查md5sum。
*   [|下载最新版的archboot版livecd（中科大镜像源）](http://mirrors.ustc.edu.cn/archlinux/iso/archboot/latest/) / [[1]](ftp://ftp.archlinux.org/iso/archboot/Changelog-2012.10-1.txt%7C修改日志) / [[2]](https://bbs.archlinux.org/viewtopic.php?id=150833%7C论坛)

### Supported boot modes of Archboot media

*   It supports BIOS booting with syslinux.
*   It supports UEFI booting with gummiboot and EFISTUB,

	for booting LTS kernels with efilinux-efi .

	(only UEFI USB is supported, UEFI CD booting is not supported!)

*   It supports grub's iso loopback support.

	variables used (below for example):

	iso_loop_dev=UUID=XXXX

	iso_loop_path=/blah/archboot.iso

*   It supports booting using syslinux's memdisk (only in BIOS mode).

### 烧录发布

Hybrid镜像是一个CD和硬盘镜像。

*   可以用来刻录CD(RW)光盘.
*   可以使用'dd' 或者 similar 工具写入磁盘介质. 这种方法也可用用来制作USB盘。

 `'dd if=<imagefile> of=/dev/<yourdevice> bs=1M'` 

### PXE 启动 / 恢复系统

[Download 2012.10 „2k12-R4“](https://downloads.archlinux.de/iso/archboot/2012.10/boot)需要的文件:

*   vmlinuz_i686 + initramfs_i686.img (i686)
*   vmlinuz_x86_64 + initramfs_x86_64.img(x86_64)
*   vmlinuz_i686_lts + initramfs_i686.img (i686 LTS kernel)
*   vmlinuz_x86_64_lts + initramfs_x86_64.img (x86_64 LTS kernel)
*   For PXE booting add the kernel and initrd to your tftp setup and you will get a running installation/rescue system.
*   For Rescue booting add a entry to your bootloader pointing to the kernel and initrd.

### News

2012.10 „2k12-R4“

*   major update/cleanup on all components

#### General

*   kernel: 3.17.3-1
*   pacman: 4.1.2-6
*   systemd: 217-6
*   RAM recommendations: 640 MB

#### Environment changes

*   changed UEFI booting on USB media to use gummiboot with EFISTUB,

	for booting LTS kernels in UEFI use efilinux-efi

*   Removal of UEFI CD booting support (only UEFI USB is supported)
*   added grub's iso loopback support

	(below for example):

	iso_loop_dev=UUID=XXXX

	iso_loop_path=/blah/archboot.iso

*   added memdisk boot support (only in BIOS mode)
*   change to zsh as default shell
*   change to systemd live environment
*   replace binaries with corresponding symlinks, saves 40MB RAM
*   synced with latest mkinitcpio changes
*   replaced cpufreq with cpupower
*   generate enough entropy for pacman with haveged during boot
*   login with agetty autologin
*   added arch-install-scripts, arch-wiki-lite, gpg-agent, grub(2), xl2tpd,

	usb_modeswitch, wvdial, amd and intel ucode,

	refind-efi, efilinux-efi and gummiboot-efi to live environment

*   updated mirrorlist
*   added memdisk support
*   removed grub legacy
*   removed rtc hook

#### setup changes

*   HIGHLIGHT:

	new network setup with netcfg

	now supports wifi and lan setup

*   added checkspace before install packages
*   use new crypttab syntax
*   added 1MB gap on autoprepare between partitions,

	to avoid mdadm issues

*   added grub loopback and memdisk mount support
*   added refind-efi, gummiboot-efi and efilinux-efi support
*   fixed unmounting of partitions on deeper locations
*   fixed check on virtio media
*   update to new config file layout

	in order to respect the rc.conf cleanup

*   hide kernel messages during mounting
*   hide parted errors during checks
*   added PARTUUID and PARTLABEL support
*   added option to copy pacman entropy to installed system
*   added initscripts/systemd switch (default: systemd installation)
*   more systemd fixes
*   removed grub legacy
*   fix permission on /sys and /proc during installation

#### quickinst changes

*   remove bootloader information
*   added checkspace before install packages
*   added initscripts/systemd switch (default: systemd installation)
*   fix permission on /sys and /proc during installation

### 历史

发布历史可以从 [这里](ftp://ftp.archlinux.org/iso/archboot/history) 找到.

### 与正式发布的区别

*   It provides an additional interactive setup and quickinst script.
*   It contains [core] repository on media.
*   It provides the long time support kernel as boot and installation option.
*   It runs a modified Arch Linux system in initramfs.
*   It is restricted to RAM usage, everything which is not necessary like

	man or info pages etc. is not provided.

*   It doesn't mount anything during boot process.

### 设置特性

*   Media and Network installation mode
*   Changing keymap and consolefont
*   Changing time and date
*   Setup network with netcfg
*   Preparing storage disk, like auto-prepare, partitioning, GUID (gpt) support, 4k sector drive support etc.
*   Creation of software raid/raid partitions, lvm2 devices and luks encrypted devices
*   Supports standard linux,raid/raid_partitions,dmraid,lvm2 and encrypted devices
*   Filesystem support: ext2/3/4, btrfs, nilfs2, reiserfs,xfs,jfs,ntfs-3g,vfat
*   Name scheme support: PARTUUID, PARTLABEL, FSUUID, FSLABEL and KERNEL
*   Mount support of grub loopback and memdisk installation media
*   Package selection support
*   Signed package installation
*   hwdetect script is used for preconfiguration
*   Auto/Preconfiguration of framebuffer, uvesafb, kms mode, fstab, mkinitcpio.conf, rc.conf, systemd, crypttab and mdadm.conf
*   Configuration of basic system files
*   Setting root password
*   grub-bios, grub-efi-x86_64, grub-efi-i386, refind-efi-x86_64, gummiboot, efilinux-efi, lilo, extlinux/syslinux, bootloader support

### 启动参数

#### 通用启动参数

*   earlymodules

	load modules before hooks are executed

	Usage:

	earlymodules=<comma-separated-array>

	earlymodules=ahci,ehci-hcd

*   disablehooks

	disable a hook which is run during bootup

	Usage:

	disablehooks=<comma-separated-array>

	disablehooks=arch_floppy,arch_cdrom

*   root

	Using this option will boot you into your specified existing system.

	Usage:

	root=/dev/<your-root-of-installed-system>

	root=/dev/sda3

*   rootflags

	Using this option will pass special mount options for your root device

	Usage:

	rootflags=<comma-separated-array>

	rootflags=subvol=root,compress,ssd

*   lvmwait=

	Using parameter followed by a comma-separated list of device names can be given on the command line.

	It will cause the hook to wait until all given devices exist before trying to scan and activate any volume groups.

	Usage:

	lvmwait=/dev/mapper/device1,/dev/mapper/device2

*   advanced

	This will override advanced hooks running order for your system.

	Default order is arch_mdadm,arch_lvm2,arch_encrypt

	Advanced hooks are: arch_mdadm,arch_lvm2,arch_encrypt

	Usage:

	advanced=hook1,hook2,hook3

	advanced=arch_encrypt,arch_mdadm

*   ide-legacy

	This will turn on the old IDE subsystem. This is only needed, if your system does not support the new PATA subsystem.

	only valid parameter on LTS kernel images

*   arch-addons

	You want to load external addon packages or configs into the install environment.

	Place external addon packages in /packages directory of your external device.

	Place external configs in /config directory of your external device.

#### 视频和framebuffer 选项

*   uvesafb

	enables uvesafb mode during boot and activates setup routine to use it later on installed system.

	you need to specify your supported resolution eg.:

	uvesafb=<resolution>-<depth>

	uvesafb=1024x768-16

*   fbmodule

	Loads the fb module you specify durin boot process and activates setup routine to use it later on installed system.

	Use it like this fbmodule=<yourmodule>, e.g. fbmodule=cirrusfb

### 问题, Known Issues and limitations

*   Release specific known issues and workarounds are posted in changelog files.
*   Check also the forum threads for posted fixes and workarounds.
*   Why screen stays blank or other weird screen issues happen?

	Some hardware doesn't like the KMS activation, use radeon.modeset=0 or i915.modeset=0 on boot prompt.

*   Why are /etc/modprobe.d/sound_persistent.conf and /etc/udev/rules.d/network_persistent.rules created?

	These 2 files ensure persistent ordering of network and soundcards, else it might happen that the order changes during every boot.

*   dmraid might be broken on some boards, support is not perfect here.

	The reason is there are so many different hardware components out there. At the moment 1.0.0rc16 is included, with latest fedora patchset.

*   grub2 cannot detect correct bios boot order:

	It may happen that hd(x,x) entries are not correct, thus first reboot may not work.

	Reason: grub cannot detect bios boot order.

	Fix: Either change bios boot order or change menu.lst to correct entries after successful boot. This cannot be fixed it is a restriction in grub/grub2!

*   Why is parted used in setup routine, instead of cfdisk in msdos partitiontable mode?

	parted is the only linux partition program that can handle all type of things the setup routine offers.

	cfdisk cannot handle GPT/GUID nor it can allign partitions correct with 1MB spaces for 4k sector disks.

	cfdisk is a nice tool but is too limited to be the standard partitioner anymore.

	cfdisk is still included but has to be run in an other terminal.

### UEFI 参考

*   [Create UEFI bootable USB from ISO](/index.php/Unified_Extensible_Firmware_Interface#Archboot "Unified Extensible Firmware Interface")
*   [Remove UEFI boot support from ISO](/index.php/Unified_Extensible_Firmware_Interface#Archboot_2 "Unified Extensible Firmware Interface")

### Bugs

[Arch Linux Bugtracker](https://bugs.archlinux.org)

## 链接

*   [GIT repository](https://projects.archlinux.org/archboot.git/)

## Usbstick 恢复

Take care about which device actually is your USB stick. The next command will render all data on /dev/sdX inaccessible.

*   First, wipe the bootsector of the USB stick:

 `dd if=/dev/zero of=/dev/sdX bs=512 count=1` 

*   Then, create a new FAT32 partition on the stick and write a FAT32 filesystem on it (vfat or type b in fdisk terminology):

```
fdisk /dev/sdX <<EOF
n
p
1

t
b
w
EOF

mkdosfs -F32 /dev/sdX1

```

## 建立镜像文件

### 如何建立Archboot Allinone ISO

(Quick regeneration of installation media with latest available core packages)

#### 前提条件

*   x86_64环境
*   archboot的iso
*   3G以上的硬盘空间

#### 建立archboot chroots

```
# 安装 archboot
pacman -S archboot
# 以loop设备挂载archboot镜像文件
mount -o loop <imagefile> <imagepath>
# 建立 x86_64 chroot
mkdir <x86_64_chroot>
/usr/share/archboot/installer/quickinst media <x86_64_chroot> <imagepath>/core-x86_64/pkg
# 建立 i686 chroot
mkdir <i686_chroot>
linux32 /usr/share/archboot/installer/quickinst media <i686_chroot> <imagepath>/core-i686/pkg
# 卸载光盘镜像文件
umount <imagepath>

```

*   挂载并复制文件到chroot目录下:

```
mount -o bind /dev <chrootpath>/dev
mount -o bind /tmp <chrootpath>/tmp
mount -o bind /sys <chrootpath>/sys
mount -o bind /proc <chrootpath>/proc
cp -a /etc/mtab <chrootpath>/etc/mtab
cp /etc/resolv.conf  <chrootpath>/etc/resolv.conf

```

*   进入 archboot x86_64 chroot:

```
chroot <chrootpath>

```

*   进入 archboot i686 chroot:

```
linux32 chroot <chrootpath>

```

#### 安装和更新archboot

```
# 安装 in both chroots archboot:
pacman -S archboot
# 更新 in both chroots to latest available packages
pacman -Syu

```

#### 生成镜像

```
# 运行 in both chroots (needs quite some time ...)
archboot-allinone.sh -t
# put the generated tarballs in one directory and run (needs quite some time ...)
archboot-allinone.sh -g

```

*   Finished you get a burnable iso image, a rawwrite usb image and a hybrid image which is both in one.
*   在离开chroot时记得卸载它们:

```
umount <chrootpath>/dev
umount <chrootpath>/tmp
umount <chrootpath>/sys
umount <chrootpath>/proc

```

Have fun! tpowa (Archboot Developer)