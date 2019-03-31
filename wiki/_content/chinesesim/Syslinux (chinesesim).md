相关文章

*   [Arch Boot Process (简体中文)](/index.php/Arch_Boot_Process_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Boot Process (简体中文)")

**翻译状态：** 本文是英文页面 [Syslinux](/index.php/Syslinux "Syslinux") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-04-21，点击[这里](https://wiki.archlinux.org/index.php?title=Syslinux&diff=0&oldid=471645)可以查看翻译后英文页面的改动。

[Syslinux](https://en.wikipedia.org/wiki/SYSLINUX "wikipedia:SYSLINUX")是一个优秀的启动加载器集合，可以从硬盘、光盘或通过 [PXE](/index.php/PXE "PXE") 的网络引导启动系统。支持的 [文件系统](/index.php/File_systems "File systems") 包括 [FAT](https://en.wikipedia.org/wiki/File_Allocation_Table "wikipedia:File Allocation Table"), [ext2](https://en.wikipedia.org/wiki/ext2 "wikipedia:ext2"), [ext3](/index.php/Ext3 "Ext3"), [ext4](/index.php/Ext4 "Ext4")和非压缩的单设备 [Btrfs](/index.php/Btrfs "Btrfs").

**Warning:** Syslinux 6.03 中，有些文件系统的功能不被支持。详情请参考 [[1]](https://wiki.syslinux.org/wiki/index.php/Filesystem)。

**Note:** Syslinux 本身只能访问其所在分区上的数据，通过 [#Chainloading](#Chainloading) 可以绕过这个限制。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 BIOS 系统](#BIOS_系统)
    *   [1.1 启动流程](#启动流程)
    *   [1.2 在 BIOS 上安装](#在_BIOS_上安装)
        *   [1.2.1 自动完成安装](#自动完成安装)
        *   [1.2.2 手工完成安装](#手工完成安装)
            *   [1.2.2.1 MBR分区表](#MBR分区表)
        *   [1.2.3 GUID Partition Table aka GPT](#GUID_Partition_Table_aka_GPT)
        *   [1.2.4 重启](#重启)
*   [2 UEFI 系统](#UEFI_系统)
    *   [2.1 UEFI Syslinux 的局限性](#UEFI_Syslinux_的局限性)
    *   [2.2 安装](#安装)
*   [3 配置](#配置)
    *   [3.1 示例](#示例)
        *   [3.1.1 比较简单的 Syslinux 配置](#比较简单的_Syslinux_配置)
        *   [3.1.2 文本的启动菜单](#文本的启动菜单)
        *   [3.1.3 图形化的启动菜单](#图形化的启动菜单)
    *   [3.2 Chainloading](#Chainloading)
    *   [3.3 使用内存测试 memtest](#使用内存测试_memtest)
    *   [3.4 使用硬件探测工具HDT](#使用硬件探测工具HDT)
    *   [3.5 重启和关闭电源](#重启和关闭电源)
*   [4 常见问题](#常见问题)
    *   [4.1 I have a Syslinux Prompt - Yikes!](#I_have_a_Syslinux_Prompt_-_Yikes!)
    *   [4.2 某些电脑中，会出现没找到默认配置或者界面](#某些电脑中，会出现没找到默认配置或者界面)
    *   [4.3 MISSING OPERATING SYSTEM](#MISSING_OPERATING_SYSTEM)
    *   [4.4 Windows boots up! No Syslinux!](#Windows_boots_up!_No_Syslinux!)
    *   [4.5 进入子菜单，但干不了任何事](#进入子菜单，但干不了任何事)
    *   [4.6 无法删除ldlinux.sys](#无法删除ldlinux.sys)
*   [5 更多信息可见](#更多信息可见)

## BIOS 系统

### 启动流程

1.  电脑启动时，BIOS 会先加载磁盘开始的 440 字节 [MBR](/index.php/MBR "MBR") 启动代码(`/usr/lib/syslinux/bios/mbr.bin` 或 `/usr/lib/syslinux/bios/gptmbr.bin`)
2.  MBR 寻找活动分区（设置了 boot 标记的 MBR 分区），假设是 `/boot` 分区。
3.  找到这个分区后， MBR 启动代码会执行卷启动记录程序（VBR=volume boot record）。对于 Syslinux 来说，VBR 就是 `/boot/syslinux/ldlinux.sys` 开始扇区的代码， 由 `extlinux --install` 命令创建。
4.  VBR 会加载剩余的 `ldlinux.sys`。`ldlinux.sys`开始扇区是被写死进卷启动记录程序里的。对于 btrfs 来说，因为文件不断移动导致`ldlinux.sys`扇区的位置不断变化，而让上面方法失效。从而使得整个syslinux需要被存储在文件系统之外。程序将被存储在卷启动记录程序之后。
5.  `ldlinux.sys` 会接着加载 `/boot/syslinux/ldlinux.c32` 核心模块，这个模块包含因为文件大小限制，无法放入 `ldlinux.sys` 的代码。
6.  当 syslinux 完全加载完毕，它将自动查找配置文件，配置文件名是 `/boot/syslinux/syslinux.cfg` 或 `/boot/syslinux/extlinux.conf`
7.  找到之后，将加载整个配置文件，否则，将进入命令行窗口，显示 `boot:` 提示。

### 在 BIOS 上安装

[安装](/index.php/Pacman "Pacman") 软件包 [syslinux](https://www.archlinux.org/packages/?name=syslinux)。如果启动分区是 FAT，需要同时安装 [mtools](https://www.archlinux.org/packages/?name=mtools).

**Note:**

*   安装 [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) 之后才能支持 [GPT](/index.php/GPT "GPT")，参考[#Automatic install](#Automatic_install)部分。
*   如果你的启动分区是 [FAT](/index.php/FAT "FAT")，还需要安装 [mtools](https://www.archlinux.org/packages/?name=mtools).

相关的软件包安装完成之后，还需要将启动加载器代码写入磁盘的对应扇区位置。有自动脚本和手动安装两种方式。

#### 自动完成安装

**Note:** 脚本 `syslinux-install_update` 是Arch特有的, Syslinux上游不提供/支持。Please direct any bug reports specific to the script to the [Arch Bug Tracker](https://bugs.archlinux.org/) and not upstream.

syslinux-install_update脚本将自动安装启动代码（一般是VBR）, 复制COM32模块到`/boot/syslinux`, 设置启动标识，安装到MBR.可自动根据softraid处理[MBR](/index.php/MBR "MBR")和 [GPT](/index.php/GPT "GPT")磁盘。

2\. 确认`/boot`是否已经加载
3\. 运行脚本`syslinux-install_update` ，参数使用 -i (安装) -a (设可启动标识) -m (安装到mbr)

```
/usr/sbin/syslinux-install_update -i -a -m

```

4\. 修改配置文件 `/boot/syslinux/syslinux.cfg`

**Note:** For this to work with [GPT](/index.php/GUID_Partition_Table "GUID Partition Table"), the [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) package is needed as the backend for setting the boot flag.

#### 手工完成安装

**Note:** 如果您尝试使用Live CD拯救已安装的系统，在执行这些命令之前请确保已经[chroot](/index.php/Chroot "Chroot")到系统. 如果没有先做chroot，您必须在所有文件（除了`/dev/`）路径之前添加挂载点。

您计划安装Syslinux的启动分区必须包含FAT，ext2，ext3，ext4或Btrfs文件系统。您不必把它安装在文件系统的根目录上，比如把磁盘 `/dev/sda1` 挂在到 `/boot`。 举个例子, 可以在`syslinux`子目录里安装 Syslinux:

```
 # mkdir /boot/syslinux

```

如果您希望使用除基本引导提示之外的任何菜单或配置，请把`/usr/lib/syslinux/bios/`里的所有`.c32` 文件复制到 `/boot/syslinux/` . Do not symlink them.

```
 # cp /usr/lib/syslinux/bios/*.c32 /boot/syslinux/     

```

安装bootloader. 对 挂载后的，格式是FAT, ext2/3/4, 或者 btrfs 的启动分区使用 *extlinux*:

```
# extlinux --install /boot/syslinux

```

或者, 对于一个**卸载**的，格式是FAT的启动分区使用*syslinux*:

```
 # syslinux --directory syslinux --install /dev/sda1

```

在此之后，继续安装适用于分区表的Syslinux引导代码：:

*   `mbr.bin` will be installed for an [#MBR partition table](#MBR_partition_table), or
*   `gptmbr.bin` will be installed for a [#GUID partition table](#GUID_partition_table)

as described in the next sections. See [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") for further general information.

**Tip:** If you are unsure of which partition table you are using (MBR or GPT), you can check using `blkid -s PTTYPE -o value /dev/sda`.

**Note:** For a partitionless install, there is no need to install the Syslinux boot code to the MBR. You could skip below and jump to [#Configuration](#Configuration). See [[2]](https://unix.stackexchange.com/questions/103501/boot-partiotionless-disk-with-syslinux).

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
 # dd bs=440 count=1 conv=notrunc if=/usr/lib/syslinux/bios/mbr.bin of=/dev/sda

```

#### GUID Partition Table aka GPT

Main article [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table")

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

*   如果此时重启，会有提示，以确认是自动启动还是给出一个启动菜单，此时需要创建一个配置文件。
*   如果你在另外一个跟文件夹（比如：在安装磁盘）通过chroot来安装SYSLINUX:

```
 # syslinux-install_update -i -a -m -c /mnt

```

## UEFI 系统

**注意:**

*   在下面的命令中，`$esp`是ESP (EFI 系统分区) 的挂载点。

*   `efi64` denotes x86_64 UEFI systems, for IA32 (32-bit) EFI replace `efi64` with `efi32` in the below commands.

*   syslinux, 内核 和 initramfs 文件需要在 ESP, as syslinux does not (currently) have the ability to access files outside its own partition (i.e. outside ESP in this case). 因此建议 ESP 挂载到 `/boot`.

*   自动安装脚本 `/usr/bin/syslinux-install_update` 不支持 UEFI 安装.

*   `syslinux.cfg`文件 为UEFI 的配置语法和 BIOS 一样.

### UEFI Syslinux 的局限性

*   UEFI Syslinux application `syslinux.efi` cannot be signed by `sbsign` (from sbsigntool) for UEFI Secure Boot. Bug report - [https://bugzilla.syslinux.org/show_bug.cgi?id=8](https://bugzilla.syslinux.org/show_bug.cgi?id=8)

*   Using TAB to edit kernel parameters in UEFI Syslinux menu lead to garbaged display (text on top of one-another). Bug report - [https://bugzilla.syslinux.org/show_bug.cgi?id=9](https://bugzilla.syslinux.org/show_bug.cgi?id=9)

*   UEFI Syslinux does not support chainloading other EFI applications like `UEFI Shell` or `Windows Boot Manager`. Bug report - [https://bugzilla.syslinux.org/show_bug.cgi?id=17](https://bugzilla.syslinux.org/show_bug.cgi?id=17)

*   UEFI Syslinux may not boot in some Virtual Machines like QEMU/OVMF or VirtualBox or some VMware products/versions and in some UEFI emulation environments like DUET. A Syslinux contributor has confirmed no such issues present on VMware Workstation 10.0.2 and Syslinux-6.02\. Bug reports - [https://bugzilla.syslinux.org/show_bug.cgi?id=21](https://bugzilla.syslinux.org/show_bug.cgi?id=21) and [https://bugzilla.syslinux.org/show_bug.cgi?id=23](https://bugzilla.syslinux.org/show_bug.cgi?id=23)

*   Memdisk is not available for UEFI. Bug report - [https://bugzilla.syslinux.org/show_bug.cgi?id=30](https://bugzilla.syslinux.org/show_bug.cgi?id=30)

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

*   按照[#配置](#配置)创建或编辑`$esp/EFI/syslinux/syslinux.cfg` [#Configuration](#Configuration).

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

If you want to chainload other operating systems (such as Windows) or boot loaders, copy (or symlink) the *chain.c32* module to the syslinux folder (for details, see the instructions in the previous section). Then, create a section in the configuration file:

```
LABEL windows
        MENU LABEL Windows
        COM32 chain.c32
        APPEND hd0 3

```

*hd0 3* is the third partition on the first BIOS drive - drives are counted from zero, but partitions are counted from one. For more details about chainloading, see [[3]](http://syslinux.zytor.com/wiki/index.php/Comboot/chain.c32).

If you have [grub2](/index.php/Grub2 "Grub2") installed in your boot partition, you can chainload it by using:

```
LABEL grub2
       MENU LABEL Grub2
       COM32 chain.c32
       append file=../grub/boot.img

```

This maybe required for booting from iso images.

### 使用内存测试 memtest

使用下面的 LABEL章节部分，可加载(需要安装软件包：*memtest86+*，否则不起作用):

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