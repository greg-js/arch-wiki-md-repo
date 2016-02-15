Syslinux是一个优秀的系统启动加载器，可引导自硬盘、光盘和通过PXE的网络启动。支持fat, ext2, ext3, ext4 and btrfs文件系统.

**注意:** 从Syslinux 4起, Extlinux和Syslinux是指同一个东西的

## Contents

*   [1 BIOS 系统](#BIOS_.E7.B3.BB.E7.BB.9F)
    *   [1.1 安装](#.E5.AE.89.E8.A3.85)
        *   [1.1.1 自动完成安装](#.E8.87.AA.E5.8A.A8.E5.AE.8C.E6.88.90.E5.AE.89.E8.A3.85)
        *   [1.1.2 手工完成安装](#.E6.89.8B.E5.B7.A5.E5.AE.8C.E6.88.90.E5.AE.89.E8.A3.85)
            *   [1.1.2.1 MBR分区表](#MBR.E5.88.86.E5.8C.BA.E8.A1.A8)
        *   [1.1.3 GUID Partition Table aka GPT](#GUID_Partition_Table_aka_GPT)
        *   [1.1.4 重启](#.E9.87.8D.E5.90.AF)
*   [2 UEFI 系统](#UEFI_.E7.B3.BB.E7.BB.9F)
    *   [2.1 UEFI Syslinux 的局限性](#UEFI_Syslinux_.E7.9A.84.E5.B1.80.E9.99.90.E6.80.A7)
    *   [2.2 安装](#.E5.AE.89.E8.A3.85_2)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 示例](#.E7.A4.BA.E4.BE.8B)
        *   [3.1.1 比较简单的 Syslinux 配置](#.E6.AF.94.E8.BE.83.E7.AE.80.E5.8D.95.E7.9A.84_Syslinux_.E9.85.8D.E7.BD.AE)
        *   [3.1.2 文本的启动菜单](#.E6.96.87.E6.9C.AC.E7.9A.84.E5.90.AF.E5.8A.A8.E8.8F.9C.E5.8D.95)
        *   [3.1.3 图形化的启动菜单](#.E5.9B.BE.E5.BD.A2.E5.8C.96.E7.9A.84.E5.90.AF.E5.8A.A8.E8.8F.9C.E5.8D.95)
    *   [3.2 Chainloading](#Chainloading)
    *   [3.3 使用内存测试 memtest](#.E4.BD.BF.E7.94.A8.E5.86.85.E5.AD.98.E6.B5.8B.E8.AF.95_memtest)
    *   [3.4 使用硬件探测工具HDT](#.E4.BD.BF.E7.94.A8.E7.A1.AC.E4.BB.B6.E6.8E.A2.E6.B5.8B.E5.B7.A5.E5.85.B7HDT)
    *   [3.5 重启和关闭电源](#.E9.87.8D.E5.90.AF.E5.92.8C.E5.85.B3.E9.97.AD.E7.94.B5.E6.BA.90)
*   [4 常见问题](#.E5.B8.B8.E8.A7.81.E9.97.AE.E9.A2.98)
    *   [4.1 I have a Syslinux Prompt - Yikes!](#I_have_a_Syslinux_Prompt_-_Yikes.21)
    *   [4.2 某些电脑中，会出现没找到默认配置或者界面](#.E6.9F.90.E4.BA.9B.E7.94.B5.E8.84.91.E4.B8.AD.EF.BC.8C.E4.BC.9A.E5.87.BA.E7.8E.B0.E6.B2.A1.E6.89.BE.E5.88.B0.E9.BB.98.E8.AE.A4.E9.85.8D.E7.BD.AE.E6.88.96.E8.80.85.E7.95.8C.E9.9D.A2)
    *   [4.3 MISSING OPERATING SYSTEM](#MISSING_OPERATING_SYSTEM)
    *   [4.4 Windows boots up! No Syslinux!](#Windows_boots_up.21_No_Syslinux.21)
    *   [4.5 进入子菜单，但干不了任何事](#.E8.BF.9B.E5.85.A5.E5.AD.90.E8.8F.9C.E5.8D.95.EF.BC.8C.E4.BD.86.E5.B9.B2.E4.B8.8D.E4.BA.86.E4.BB.BB.E4.BD.95.E4.BA.8B)
    *   [4.6 无法删除ldlinux.sys](#.E6.97.A0.E6.B3.95.E5.88.A0.E9.99.A4ldlinux.sys)
*   [5 更多信息可见](#.E6.9B.B4.E5.A4.9A.E4.BF.A1.E6.81.AF.E5.8F.AF.E8.A7.81)

## BIOS 系统

1.  电脑启动时，会先加载[MBR](/index.php/MBR "MBR") (`/usr/lib/syslinux/mbr.bin`)
2.  MBR查找那些活动的分区（标注了可启动的）
3.  找到这个分区后，卷启动记录程序（VBR=volume boot record）将被执行。如果是ext2/3/4和fat 12/16/32，`ldlinux.sys`开始的扇区是被写死进卷启动记录程序里的，卷启动记录程序将执行(`ldlinux.sys`)。当然，如果`ldlinux.sys` 的位置发生改变，syslinux将无法加载。如果是btrfs，因为文件不断移动导致`ldlinux.sys`扇区的位置不断变化，而让上面方法失效。从而使得整个syslinux需要被存储在文件系统之外。程序将被存储在卷启动记录程序之后。
4.  当syslinux完全加载完毕，它将自动寻找一个配置文件，名字叫 `extlinux.conf` 或者`syslinux.cfg`.
5.  找到之后，将加载整个配置文件，否则，将进入命令行窗口。

### 安装

从 [官方软件仓库](/index.php/Official_repositories "Official repositories") 中 [安装](/index.php/Pacman "Pacman") 软件包 [syslinux](https://www.archlinux.org/packages/?name=syslinux)。如果启动分区是 FAT，需要同时安装 [mtools](https://www.archlinux.org/packages/?name=mtools).

**Note:**

*   从 Syslinux 4 开始，Extlinux 和 Syslinux 已经统一，是同一个东西。
*   UEFI support was added in the 6.x branch. See [UEFI_Bootloaders#SYSLINUX](/index.php/UEFI_Bootloaders#SYSLINUX "UEFI Bootloaders") for more info.
*   [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) is required for [GPT](https://en.wikipedia.org/wiki/GUID_Partition_Table "wikipedia:GUID Partition Table") support using the automated script.

#### 自动完成安装

syslinux-install_update脚本将自动安装Syslinux, 复制COM32模块到`/boot/syslinux`, 设置启动标识，安装到MBR.可自动根据softraid处理MBR和 GPT磁盘。

2\. 确认`/boot`是否已经加载
3\. 运行脚本`syslinux-install_update` ，参数使用 -i (安装) -a (设可启动标识) -m (安装到mbr)

```
/usr/sbin/syslinux-install_update -i -a -m

```

4\. 修改配置文件 `/boot/syslinux/syslinux.cfg`

**Note:** For this to work with [GPT](/index.php/GUID_Partition_Table "GUID Partition Table"), the [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) package is needed as the backend for setting the boot flag.

#### 手工完成安装

**Note:** 若你不知你所使用的分区表是使用什么 (MBR or GPT), 默认一般使用的是MBR分区表。大部分情况下，GPT将使用整个磁盘创建一个特殊的MBR-类型的分区(type 0xEE) ，使用下面命令可显示：

```
# fdisk -l /dev/sda

```

或者可以这样：

```
# sgdisk -l /dev/sda

```

若其非GPT磁盘，将显示 " GPT: not present".

**Note:** If you are trying to rescue an installed system with a live CD, be sure to [chroot](/index.php/Change_root "Change root") into it before executing these commands. If you do not chroot first, you must prepend all file paths (not /dev/ paths) with the mount point.

Make sure you have the _syslinux_ package installed. Then install Syslinux onto your boot partition, which must contain a fat, ext2, ext3, ext4, or btrfs file system.

```
# mkdir /boot/syslinux
# extlinux --install /boot/syslinux #run on a mounted directory (not /dev/sdXY)
/boot/syslinux/ is device /dev/sda1

```

##### MBR分区表

需要标识启动分区为激活状态.可用这些工具实现：fdisk, cfdisk, sfdisk, (g)parted.最后结果看起来是这样：

```
# fdisk -l /dev/sda
[...]
  Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *        2048      104447       51200   83  Linux
/dev/sda2          104448   625142447   312519000   83  Linux

```

安装到主启动卷区:

```
# dd bs=440 conv=notrunc count=1 if=/usr/lib/syslinux/bios/mbr.bin of=/dev/sda

```

#### GUID Partition Table aka GPT

Main article [GUID_Partition_Table](/index.php/GUID_Partition_Table "GUID Partition Table")

Bit 2 of the attributes for the `/boot` partition need to be set.

```
# sgdisk /dev/sda --attributes=1:set:2

```

This would toggle the attribute legacy BIOS bootable on partition 1

Verify:

```
# sgdisk /dev/sda --attributes=1:show
1:2:1 (legacy BIOS bootable)

```

安装主启动卷区:

```
# dd bs=440 conv=notrunc count=1 if=/usr/lib/syslinux/bios/gptmbr.bin of=/dev/sda

```

#### 重启

如果此时重启，会有提示，以确认是自动启动还是给出一个启动菜单，此时需要创建一个配置文件。

## UEFI 系统

**注意:**

*   在下面的命令中，`$esp`是ESP (EFI 系统分区) 的挂载点。

*   `efi64` denotes x86_64 UEFI systems, for IA32 (32-bit) EFI replace `efi64` with `efi32` in the below commands.

*   syslinux, 内核 和 initramfs 文件需要在 ESP, as syslinux does not (currently) have the ability to access files outside its own partition (i.e. outside ESP in this case). 因此建议 ESP 挂载到 `/boot`.

*   自动安装脚本 `/usr/bin/syslinux-install_update` 不支持 UEFI 安装.

*   `syslinux.cfg`文件 为UEFI 的配置语法和 BIOS 一样.

### UEFI Syslinux 的局限性

*   UEFI Syslinux application `syslinux.efi` cannot be signed by `sbsign` (from sbsigntool) for UEFI Secure Boot. Bug report - [http://bugzilla.syslinux.org/show_bug.cgi?id=8](http://bugzilla.syslinux.org/show_bug.cgi?id=8)

*   Using TAB to edit kernel parameters in UEFI Syslinux menu lead to garbaged display (text on top of one-another). Bug report - [http://bugzilla.syslinux.org/show_bug.cgi?id=9](http://bugzilla.syslinux.org/show_bug.cgi?id=9)

*   UEFI Syslinux does not support chainloading other EFI applications like `UEFI Shell` or `Windows Boot Manager`. Bug report - [http://bugzilla.syslinux.org/show_bug.cgi?id=17](http://bugzilla.syslinux.org/show_bug.cgi?id=17)

*   UEFI Syslinux may not boot in some Virtual Machines like QEMU/OVMF or VirtualBox or some VMware products/versions and in some UEFI emulation environments like DUET. A Syslinux contributor has confirmed no such issues present on VMware Workstation 10.0.2 and Syslinux-6.02\. Bug reports - [http://bugzilla.syslinux.org/show_bug.cgi?id=21](http://bugzilla.syslinux.org/show_bug.cgi?id=21) and [http://bugzilla.syslinux.org/show_bug.cgi?id=23](http://bugzilla.syslinux.org/show_bug.cgi?id=23)

*   Memdisk is not available for UEFI. Bug report - [http://bugzilla.syslinux.org/show_bug.cgi?id=30](http://bugzilla.syslinux.org/show_bug.cgi?id=30)

### 安装

*   安装来自[official repositories](/index.php/Official_repositories "Official repositories")的 [syslinux](https://www.archlinux.org/packages/?name=syslinux) 和 [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr)。然后按如下步骤安装 syslinux 到 EFI System Partition (ESP) :

*   复制 syslinux 文件到 ESP (将 `$esp` 替换为ESP的挂载点, 通常是 `/boot`):

```
# mkdir -p $esp/EFI/syslinux
# cp -r /usr/lib/syslinux/efi64/* $esp/EFI/syslinux

```

*   Setup boot entry for Syslinux using [efibootmgr](/index.php/Unified_Extensible_Firmware_Interface#efibootmgr "Unified Extensible Firmware Interface"):

```
# efibootmgr -c -d /dev/sdX -p Y -l /EFI/syslinux/syslinux.efi -L "Syslinux"

```

```
`/dev/sdXY` 是包含引导程序的分区

```

*   按照[#配置](#.E9.85.8D.E7.BD.AE)创建或编辑`$esp/EFI/syslinux/syslinux.cfg` [#Configuration](#Configuration).

**注意:** UEFI 的配置文件是 `$esp/EFI/syslinux/syslinux.cfg`, 而不是 `/boot/syslinux/syslinux.cfg`. Files in `/boot/syslinux/` are BIOS specific and not related to UEFI syslinux.

## 配置

syslinux的配置文件 `syslinux.cfg` 必须和syslinux放在同一个目录下，在我们的例子中，是 '/boot/syslinux/'

启动器将自动寻找这两个配置文件：`syslinux.cfg` (优先) 或者 `extlinux.conf`

**补充**:

*   Instead of LINUX, the keyword KERNEL can also be used. KERNEL tries to detect the type of the file, while LINUX always expects a Linux kernel.
*   TIMEOUT 的值是1/10秒，也就是50代表5秒

### 示例

#### 比较简单的 Syslinux 配置

这是一个非常简单的配置，有启动提示，并且在5秒后自动启动第一个系统。

配置文件:

```
PROMPT 1
TIMEOUT 50
DEFAULT arch

LABEL arch
        LINUX ../vmlinuz-linux
        APPEND root=/dev/sda2 ro
        INITRD ../initramfs-linux.img

LABEL archfallback
        LINUX ../vmlinuz-linux
        APPEND root=/dev/sda2 ro
        INITRD ../initramfs-linux-fallback.img

```

若不想看到提示，设置PROMPT（显示时间）为0.

#### 文本的启动菜单

把模块menu COM32复制到syslinux目录中，即可使用文本菜单：

```
# cp /usr/lib/syslinux/menu.c32 /boot/syslinux/

```

若没有给/boot单独分区，且和/usr同一分区，那么，也可以仅使用一个软链接:

```
# ln -s /usr/lib/syslinux/menu.c32 /boot/syslinux/

```

配置:

```
UI menu.c32
PROMPT 0

MENU TITLE Boot Menu
TIMEOUT 50
DEFAULT arch

LABEL arch
        MENU LABEL Arch Linux
        LINUX ../vmlinuz-linux
        APPEND root=/dev/sda2 ro
        INITRD ../initramfs-linux.img

LABEL archfallback
        MENU LABEL Arch Linux Fallback
        LINUX /vmlinuz-linux
        APPEND root=/dev/sda2 ro
        INITRD /initramfs-linux-fallback.img

```

更多信息可见： [http://git.kernel.org/?p=boot/syslinux/syslinux.git;a=blob;f=doc/menu.txt](http://git.kernel.org/?p=boot/syslinux/syslinux.git;a=blob;f=doc/menu.txt).

#### 图形化的启动菜单

把vesamenu COM32移入到syslinux目录中，可使用图形启动界面:

```
# cp /usr/lib/syslinux/vesamenu.c32 /boot/syslinux/

```

若没有给/boot单独分区，且和/usr同一分区，那么，也可以仅使用一个软链接: :

```
# ln -s /usr/lib/syslinux/vesamenu.c32 /boot/syslinux/

```

This config uses the same menu design as the Arch Install CD: [syslinux.cfg](https://projects.archlinux.org/archiso.git/tree/configs/syslinux-iso/boot-files/syslinux/syslinux.cfg)

The background file can be found here: [splash.png](https://projects.archlinux.org/archiso.git/plain/configs/releng/syslinux/splash.png)

Config:

```
UI vesamenu.c32
DEFAULT arch
PROMPT 0
MENU TITLE Boot Menu
MENU BACKGROUND splash.png
TIMEOUT 50

MENU WIDTH 78
MENU MARGIN 4
MENU ROWS 5
MENU VSHIFT 10
MENU TIMEOUTROW 13
MENU TABMSGROW 11
MENU CMDLINEROW 11
MENU HELPMSGROW 16
MENU HELPMSGENDROW 29

# Refer to [http://syslinux.zytor.com/wiki/index.php/Doc/menu](http://syslinux.zytor.com/wiki/index.php/Doc/menu)

MENU COLOR border       30;44   #40ffffff #a0000000 std
MENU COLOR title        1;36;44 #9033ccff #a0000000 std
MENU COLOR sel          7;37;40 #e0ffffff #20ffffff all
MENU COLOR unsel        37;44   #50ffffff #a0000000 std
MENU COLOR help         37;40   #c0ffffff #a0000000 std
MENU COLOR timeout_msg  37;40   #80ffffff #00000000 std
MENU COLOR timeout      1;37;40 #c0ffffff #00000000 std
MENU COLOR msg07        37;40   #90ffffff #a0000000 std
MENU COLOR tabmsg       31;40   #30ffffff #00000000 std

LABEL arch
        MENU LABEL Arch Linux
        LINUX ../vmlinuz-linux
        APPEND root=/dev/sda2 ro
        INITRD ../initramfs-linux.img

LABEL archfallback
        MENU LABEL Arch Linux Fallback
        LINUX ../vmlinuz-linux
        APPEND root=/dev/sda2 ro
        INITRD ../initramfs-linux-fallback.img

```

Since Syslinux 3.84 vesamenu.c32 supports the "MENU RESOLUTION $WIDTH $HEIGHT" directive. To use it, insert "MENU RESOLUTION 1440 900" into your config for a 1440x900 resolution. The background picture has to have exactly the right resolution however as syslinux will otherwise refuse to load the menu.

### Chainloading

If you want to chainload other operating systems (such as Windows) or boot loaders, copy (or symlink) the _chain.c32_ module to the syslinux folder (for details, see the instructions in the previous section). Then, create a section in the configuration file:

```
LABEL windows
        MENU LABEL Windows
        COM32 chain.c32
        APPEND hd0 3

```

_hd0 3_ is the third partition on the first BIOS drive - drives are counted from zero, but partitions are counted from one. For more details about chainloading, see [[1]](http://syslinux.zytor.com/wiki/index.php/Comboot/chain.c32).

If you have [grub2](/index.php/Grub2 "Grub2") installed in your boot partition, you can chainload it by using:

```
LABEL grub2
       MENU LABEL Grub2
       COM32 chain.c32
       append file=../grub/boot.img

```

This maybe required for booting from iso images.

### 使用内存测试 memtest

使用下面的 LABEL章节部分，可加载(需要安装软件包：_memtest86+_，否则不起作用):

```
LABEL memtest
        MENU LABEL Memtest86+
        LINUX ../memtest86+/memtest.bin

```

### 使用硬件探测工具HDT

HDT (Hardware Detection Tool) displays hardware information. Like before, the .c32 file has to be copied or symlinked from /boot/syslinux/. For pci info either copy or symlink `/usr/share/hwdata/pci.ids` to `/boot/syslinux/pci.ids`

```
LABEL hdt
        MENU LABEL Hardware Info
        COM32 hdt.c32

```

### 重启和关闭电源

Use the following sections to reboot or power off your machine.

```
LABEL reboot
        MENU LABEL Reboot
        COM32 reboot.c32

LABEL poweroff
        MENU LABEL Power Off
        COMBOOT poweroff.com

```

## 常见问题

### I have a Syslinux Prompt - Yikes!

You can type in the LABEL name of the entry that you want to boot (as per your syslinux.cfg). If you used the example configs just type

```
boot: arch

```

If you get an error that the config file could not be loaded you can pass your needed boot parameters, e.g.:

```
boot: ../vmlinuz-linux root=/dev/sda2 ro initrd=../initramfs-linux.img

```

If you don't have access to 'boot:' in ramfs, and therefore temporarily unable to boot kernel again

1) create temp directory, in order to mount your root partition (if it doesn't exist already)

```
 mkdir -p /new_root

```

2) mount / under /new_root (in case /boot/ is on same partition, otherwise you'll need to mount them both)

```
 mount /dev/sd[a-z][1-9] /new_root

```

3) use 'vi' and edit syslinux.cfg again to suit your needs and save file;

4) reboot

### 某些电脑中，会出现没找到默认配置或者界面

Certain motherboard manufacturers have less compatibility for booting from USB devices than others. While an ext4 formatted usb drive may boot on a more recent computer, some computers may hang if the boot partition containing the kernel and initrd are not on a fat16 partition. to prevent an older machine from loading ldlinux and failing to read syslinux.cfg, use cfdisk to create a fat-16 partition (<=2GB) and format with

```
# pacman -S dosfstools
# mkfs.msdos -F 16 /dev/sda1

```

then install and configure syslinux.

### MISSING OPERATING SYSTEM

If you get this message, check if the partition that contains `/boot` has the boot flag enabled. If the flag is enabled, then perhaps this partition starts at sector 1 rather than sector 63 or 2048\. Check this with fdisk -l. If it starts at sector 1, you can move the partition(s) with gparted from a rescue disk. Or, if you have a separate boot partition, you can back up /boot with

```
cp -a /boot /boot.bak

```

and then boot up with the arch install disk. Next, use cfdisk to delete the /boot partition, and recreate it. This time it should begin at the proper sector, 63\. Now mount your partitions and chroot into your mounted system, as described in the beginners guide. Restore /boot with the command

```
cp -a /boot.bak/* /boot

```

Check if /etc/fstab is correct. Then run

```
/usr/sbin/syslinux-install_update -iam

```

and reboot.

### Windows boots up! No Syslinux!

**Solution:** Make sure the partition that contains /boot has the boot flag enabled. Also, make sure the boot flag is not enabled on the windows partition. See the installation section above.

The MBR that comes with syslinux looks for the first active partition that has the boot flag set. The windows partition was likely found first and had the boot flag set. If you wanted you could use the MBR that windows or msdos fdisk provides.

### 进入子菜单，但干不了任何事

You select a menu entry and it does nothing. It "refreshes" the menu
This usually means that you have an error in your configuration. Hit `TAB` to edit your boot parameters. Alternatively, press `ESC` and type in the LABEL of your boot entry (Example: arch)

### 无法删除ldlinux.sys

ldlinux.sys has the immutable attribute set which prevents the file from being deleted or overwritten. This is because the sector location of the file must not change or else syslinux has to be reinstalled. To remove:

```
chattr -i /boot/syslinux/ldlinux.sys
rm /boot/syslinux/ldlinux.sys

```

## 更多信息可见

*   [The Syslinux Project](http://syslinux.zytor.com/)'s website.