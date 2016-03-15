**翻译状态：** 本文是英文页面 [USB_Flash_Installation_Media](/index.php/USB_Flash_Installation_Media "USB Flash Installation Media") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-09-21，点击[这里](https://wiki.archlinux.org/index.php?title=USB_Flash_Installation_Media&diff=0&oldid=336204)可以查看翻译后英文页面的改动。

本文探讨如何制作能在 UEFI 和 BIOS 系统上启动的 Arch Linux 安装 USB 驱动器（也被称为*“闪存驱动器”，“USB记忆棒"，“U盘”等）。制作好的U盘被称为 LiveUSB 系统（类似 LiveCD 系统），因为[SquashFS](https://en.wikipedia.org/wiki/SquashFS "wikipedia:SquashFS")的性质，关机后所有的更改都会丢失。这样的系统可用于安装 Arch Linux、系统维护或者系统恢复。*

如果想在U盘上运行完整的 Arch Linux（即能保留设置），参见[在U盘中安装Arch Linux](/index.php/Installing_Arch_Linux_on_a_USB_key_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Installing Arch Linux on a USB key (简体中文)")。如果想将 Arch Linux LiveUSB 当作救援 USB 来用，参见[Change Root](/index.php/Change_Root_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Change Root (简体中文)")

## Contents

*   [1 BIOS 和 UEFI 可启动 USB](#BIOS_.E5.92.8C_UEFI_.E5.8F.AF.E5.90.AF.E5.8A.A8_USB)
    *   [1.1 dd](#dd)
        *   [1.1.1 GNU/Linux](#GNU.2FLinux)
        *   [1.1.2 Windows](#Windows)
            *   [1.1.2.1 Rufus](#Rufus)
            *   [1.1.2.2 USBwriter](#USBwriter)
            *   [1.1.2.3 Cygwin](#Cygwin)
            *   [1.1.2.4 dd for Windows](#dd_for_Windows)
        *   [1.1.3 Mac OS X](#Mac_OS_X)
        *   [1.1.4 如何恢复U盘](#.E5.A6.82.E4.BD.95.E6.81.A2.E5.A4.8DU.E7.9B.98)
    *   [1.2 手动方法](#.E6.89.8B.E5.8A.A8.E6.96.B9.E6.B3.95)
        *   [1.2.1 GNU/Linux](#GNU.2FLinux_2)
        *   [1.2.2 Windows](#Windows_2)
*   [2 BIOS 系统的其他方法](#BIOS_.E7.B3.BB.E7.BB.9F.E7.9A.84.E5.85.B6.E4.BB.96.E6.96.B9.E6.B3.95)
    *   [2.1 GNU/Linux](#GNU.2FLinux_3)
        *   [2.1.1 UNetbootin](#UNetbootin)
    *   [2.2 Windows](#Windows_3)
        *   [2.2.1 Win32 Disk Imager](#Win32_Disk_Imager)
        *   [2.2.2 USBWriter for Windows](#USBWriter_for_Windows)
        *   [2.2.3 Flashnul](#Flashnul)
        *   [2.2.4 在内存加载安装介质](#.E5.9C.A8.E5.86.85.E5.AD.98.E5.8A.A0.E8.BD.BD.E5.AE.89.E8.A3.85.E4.BB.8B.E8.B4.A8)
            *   [2.2.4.1 准备 U 盘](#.E5.87.86.E5.A4.87_U_.E7.9B.98)
            *   [2.2.4.2 复制需要的文件到 U 盘](#.E5.A4.8D.E5.88.B6.E9.9C.80.E8.A6.81.E7.9A.84.E6.96.87.E4.BB.B6.E5.88.B0_U_.E7.9B.98)
            *   [2.2.4.3 创建配置文件](#.E5.88.9B.E5.BB.BA.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
            *   [2.2.4.4 最后的步骤](#.E6.9C.80.E5.90.8E.E7.9A.84.E6.AD.A5.E9.AA.A4)
*   [3 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
*   [4 参见](#.E5.8F.82.E8.A7.81)

## BIOS 和 UEFI 可启动 USB

### dd

**注意:** 推荐该方法是因为它简单。如果没有效果，请使用下面介绍的方法 [#手动方法](#.E6.89.8B.E5.8A.A8.E6.96.B9.E6.B3.95) 。

**警告:** 这种方法会删除 `/dev/sd**x**` 上的所有数据且不可逆

#### GNU/Linux

**小贴士:** 用 `lsblk` 找到U盘并确保**没有**挂载

用U盘替换 `/dev/**sdx**`，如 `/dev/sdb`。（**不要**加上数字，也就是说，**不要**键入 `/dev/sdb**1**` 之类的东西)

```
# dd bs=4M if=/path/to/archlinux.iso of=/dev/**sdx** && sync

```

#### Windows

##### Rufus

[Rufus](https://rufus.akeo.ie/?locale=zh_CN/) is a multi-purpose USB iso writer. Simply select the Arch Linux ISO, the USB drive you want to create the bootable Arch Linux onto and click start.

Since Rufus does not care if the drive is properly formatted or not and provides a GUI it may be the easiest and most robust tool to use.

##### USBwriter

这种方法和 `dd` 一样简单，只要下载 Arch Linux 安装镜像并用 [USBwriter](http://sourceforge.net/p/usbwriter/wiki/Documentation/) 写入U盘即可。

##### Cygwin

请确认您安装了[Cygwin](http://www.cygwin.com/)的 `dd` 包。

**小贴士:** 如果您不想安装 Cygwin，您可以直接从 [这里](http://www.chrysocome.net/dd)下载 `dd` for Windows。查看下一节以获得更多信息。

将您的镜像文件放在您的home目录中：

```
C:\cygwin\home\John\

```

以管理员身份运行cygwin（cygwin必须访问硬件）。用下列命令写入到您的USB设备：

```
dd if=image.iso of=\\.\[x]: bs=4M

```

其中 image.iso 要输入 `cygwin` 目录内的 iso 镜像文件名，而 `\\.\[**x**]`: 里面的 **x** 是 Windows为您的USB设备指定的盘符，例如 `\\.\d:`。

Cygwin 6.0 版本中可以这样找到正确的分区：

```
cat /proc/partitions

```

然后根据输出信息写入ISO映像，例如：

**警告:** 这个操作会不可恢复的删除您 USB 设备上的所有文件，所以执行这个操作前请先确定您的 USB 设备中没有任何重要的数据。

```
dd if=image.iso of=/dev/sdb bs=4M

```

##### dd for Windows

**注意:** 某些用户在使用这种方法时碰到了"isolinux.bin missing or corrupt"的问题。

[http://www.chrysocome.net/dd](http://www.chrysocome.net/dd) 上有基于 GPL 协议的 dd for Windows。相比于 Cygwin，它的优势在于下载量小。使用方法已经在上面的 Cygwin 部分中说明了。

首先下载最新版本的 dd for Windows，并把内容解压到 Downloads 目录或者别的什么地方。 保 现在以管理员身份运行 `命令提示符`。然后切换目录（`cd`）到 Downloads 目录。

如果你的 Arch Linux ISO 在别的地方，你可能需要列出完整路径。方便起见，你可能会把它放在 dd 程序的同一目录中。命令的基本格式像这样：

```
dd if=archlinux-2014-XX-xx-dual.iso of=\\.\x: bs=4m

```

**警告:** 这条命令会把驱动器的格式和内容按照 ISO 中的来填充。误操作后很可能无法恢复其原先的内容，在执行命令以前要确保你dd 中使用的是正确的驱动器！

用正常的日期和盘符来替换上面的空缺（以 "x" 来表示）

下面是一个实例：

```
dd if=ISOs\archlinux-2014.09.03-dual.iso of=\\.\d: bs=4M

```

#### Mac OS X

做一些特定操作后才能在 Mac 下使用 `dd` 写入 USB 设备。先插入 USB 设备，OS X 会自动挂载它，然后在终端程序中运行:

```
$ diskutil list

```

用 `mount` 或者 `sudo dmesg | tail`（例如 `/dev/disk1`）来找出 USB 设备的名称，卸载设备上的分区（即，/dev/disk1s1）同时保留设备本身（即，/dev/disk1）：

```
$ diskutil unmountDisk /dev/disk1

```

接着我们可以依照上面介绍的方法继续操作（如果用的是 OS X `dd`，用 `/dev/rdisk` 替代 `/dev/disk`，且 `bs=1m`。`rdisk`指的是“raw disk”，在 OS X 上比较快，而 `bs=1m`表示 1 MB 块大小）。

 `# dd if=image.iso of=/dev/rdisk1 bs=1m` 
```
20480+0 records in
20480+0 records out
167772160 bytes transferred in 220.016918 secs (762542 bytes/sec)

```

此时，在物理拔出U盘前，弹出您的USB驱动器可能是个好主意。

```
$ diskutil eject /dev/disk1

```

#### 如何恢复U盘

ISO 镜像是多功能镜像，既可以烧到光盘也能直接写入 USB，所以它不包含一个标准的分区表。

安装 Arch Linux 后，就不需要 USB 安装盘了。你需要往U盘的前 512 字节写零*（表示主引导记录中的引导代码和非标准的分区表）*来恢复它完整的容量。

```
# dd count=1 bs=512 if=/dev/zero of=/dev/sd**x** && sync

```

然后用 [gparted](https://www.archlinux.org/packages/?name=gparted) 创建一个新的分区表（如"msdos"）和文件系统（如 EXT4，FAT32），或者在终端中：

*   对于 EXT2/3/4 （相应地调整），命令是：

1.  cfdisk /dev/sd**x**
2.  mkfs.ext4 /dev/sd**x1**
3.  e2label /dev/sd**x1** USB_STICK

*   对于 FAT32，安装 [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) 软件包并运行：

1.  cfdisk /dev/sd**x**
2.  mkfs.vfat -F32 /dev/sd**x1**
3.  dosfslabel /dev/sd**x1** USB_STICK

### 手动方法

#### GNU/Linux

这种方法比 `dd` 复杂，但能够保持U盘可用（ISO 被装在[[Partitioning|]分了区的设备]的某个分区里而无需改变其他分区）。

**注意:** 接下来会用 `/dev/sd**Xn**` 指代目标分区，请根据自身的情况调整 **X** 和 **n**。

*   确保已经安装了最新版的 *syslinux*（6.02或更新）。

*   如果还未准备好，在继续前创建好分区表和分区。`/dev/sd**Xn**` 必须格式化为 FAT32。

*   挂载 ISO 镜像。挂载U盘上的 FAT32 分区，把 ISO 镜像内的文件都复制进去。卸载 ISO 镜像，但不要卸载 FAT32 分区。接着执行：

```
# mkdir -p /mnt/{iso,usb}
# mount -o loop archlinux-2014.09.03-dual.iso /mnt/iso
# mount /dev/sd**Xn** /mnt/usb
# cp -a /mnt/iso/* /mnt/usb
# sync
# umount /mnt/iso

```

*   **注意:** 如果用的是 [Archboot](/index.php/Archboot "Archboot")，以下步骤可省略；如果是[Archiso](/index.php/Archiso "Archiso") 则不可。
    卷标，或者 UUID 是成功引导必不可少的。默认识别的卷标是 `ARCH_2014**XX**`（XX 和镜像发布月份有关）。因此，FAT32 分区的卷标须设成一样的（可以用*gparted*）。 要修改识别的卷标，可以编辑 */mnt/usb/arch/boot/syslinux/archiso_sys32.cfg*、*archiso_sys64.cfg*和*/mnt/usb/loader/entries/archiso-x86_64.conf*中的 `archisolabel=ARCH_2014**XX**`（最后一个文件仅对 EFI 系统生效）。32位的 ISO 需要类似修改。要让安装镜像识别 UUID 而不是卷标，将这些地方改为 `archiso*device*=/dev/disk/by-uuid/**YOUR-UUID**`。UUID 可通过 `blkid -o value -s UUID /dev/sd**Xn**` 查看。

**警告:** 错误的卷标或 UUID 会导致启动失败。

*   */mnt/usb/arch/boot/syslinux* 里已经安装 syslinux。请按照 [Syslinux#Manual_install](/index.php/Syslinux#Manual_install "Syslinux")进行重装。
    *   用新 syslinux 的模块（`*.c32` 文件）覆盖原有 syslinux 的模块，以免因版本差异导致启动失败。
    *   运行：

```
# extlinux --install /mnt/usb/arch/boot/syslinux

```

*   *   卸载分区（`umount /mnt/usb`）并将 MBR 或 GPT 分区表安装到U盘。

*   将该分区标记为活跃（或“启动”）。

#### Windows

**注意:**

*   不要使用**可启动 USB 创建工具**制作UEFI 启动 USB。不要用*dd for Windows*将 ISO 镜像写入U盘。

*   以下命令假设U盘盘符为 **X:**。

*   Windows 使用反斜杠作为路径分隔符，以下命令也是。

*   所有命令都应该在**以管理员身份运行**的命令提示符内执行。

*   `>` 表示 Windows 命令提示符。

*   分区和格式化工具用 [Rufus USB partitioner](http://rufus.akeo.ie/)。partition scheme 选 **MBR for BIOS and UEFI**，文件系统选**FAT32**，反选“Create a bootable disk using ISO image”和“Create extended label and icon files”

*   如果用的是官方 ISO 镜像（[Archiso](/index.php/Archiso "Archiso")），修改U盘 `X:` **卷标**，与 `<ISO>\loader\entries\archiso-x86_64.conf` 中的 `archisolabel=` 保持一致。如果是 [Archboot](/index.php/Archboot "Archboot") 则不需要修改。卷标可在上一步使用 Rufus 进行分区和格式化时修改。

*   解压 ISO 文件至U盘（像解压 ZIP 文件一样，软件可用[7-Zip](http://7-zip.org/)）。

*   从 [https://www.kernel.org/pub/linux/utils/boot/syslinux/](https://www.kernel.org/pub/linux/utils/boot/syslinux/) 下载官方 syslinux 6.xx （ZIP文件）并解压。Syslinux 的版本应与 ISO 镜像所使用的版本一致。

*   运行以下命令（在命令提示符内，以管理员身份运行）：

**注意:** Archboot iso 用 `X:\boot\syslinux\`。

```
> cd bios\
> for /r %Y in (*.c32) do copy "%Y" "X:\arch\boot\syslinux\" /y
> copy mbr\*.bin X:\arch\boot\syslinux\ /y

```

*   通过以下命令将 Syslinux 安装到U盘（64位系统则用 `win64\syslinux64.exe`）：

**注意:** Archboot iso 用 `-d /boot/syslinux`。

```
> cd bios\
> win32\syslinux.exe -d /arch/boot/syslinux -i -a -m X:

```

**注意:**

*   上述步骤将安装 Syslinux `ldlinux.sys` 至U盘分区 VBR，在 MBR 分区表中将该分区设置为活跃/启动，并将 MBR 引导代码写入U盘前 440字节引导代码区中。

*   `-d`开关需要斜杠作为路径分隔符。

## BIOS 系统的其他方法

### GNU/Linux

#### UNetbootin

可以在任何 Linux 发行版或者 Windows 中用 UNetbootin 把你的 ISO 复制到 USB 设备中，但是 Unetbootin 会覆盖 syslinux.cfg，创建的 USB 设备不能正常引导。由于这个原因，**不推荐使用 Unetbootin** -- 请使用 `dd` 或者这里列出的其它方法。

**警告:** UNetbootin 覆盖了默认的 `syslinux.cfg`；在USB设备正常引导前需要还原它。

编辑 `syslinux.cfg`：

 `sysconfig.cfg` 
```
default menu.c32
prompt 0
menu title Archlinux Installer
timeout 100

label unetbootindefault
menu label Archlinux_x86_64
kernel /arch/boot/x86_64/vmlinuz
append initrd=/arch/boot/x86_64/archiso.img archisodevice=/dev/sd**x1** ../../

label ubnentry0
menu label Archlinux_i686
kernel /arch/boot/i686/vmlinuz
append initrd=/arch/boot/i686/archiso.img archisodevice=/dev/sd**x1** ../../
```

你必须用你安装 Arch Linux 的位置，即首个系统未使用的字母来替换 `/dev/sd**x1**` 中的 **x**（例如，如果你有两个硬盘，使用 `c`。）。你也可以在启动的第一阶段显示菜单的时候按 `Tab` 键改变它。

### Windows

#### Win32 Disk Imager

**警告:** 这些操作会销毁 U 盘中的所有信息！

首先从[这里](http://sourceforge.net/projects/win32diskimager/)下载程序。然后解压并运行可执行程序。在 `Image FIle` 部分中选择 Arch Linux ISO，在 `Device` 部分中选择 U 盘的盘符。准备就绪后点击 `Write`。

**注意:** 安装后你可能需要以[这里](/index.php/USB_Installation_Media#How_to_restore_the_USB_drive "USB Installation Media")列出的流程恢复 U 盘。

#### USBWriter for Windows

从 [http://sourceforge.net/projects/usbwriter/](http://sourceforge.net/projects/usbwriter/) 下载程序并运行。选择 arch 镜像文件和目标U盘，然后点击 `write` 按钮。现在你应该能够从 U 盘启动安装 Arch Linux。

#### Flashnul

[flashnul](http://shounen.ru/soft/flashnul/) 是一个用来检测和维护闪存（USB-Flash，IDE-Flash，SecureDigital，MMC，MemoryStick，SmartMedia，XD，CompactFlash 等）的工具。

从命令提示符下，使用 `–p` 参数调用 flashnul 命令来确定 USB 设备的盘符，例如：

 `C:\>flashnul -p` 
```
 Avaible physical drives:
 Avaible logical disks:
 C:\
 D:\
 E:\

```

在本例中，USB 设备的盘符是 E:

当您确定正确的设备后，您可以将镜像写入到您的设备中，通过调用flashnul命令，后面输入您的设备序号，再输入 `-L` 及镜像的完整路径，例如：

```
C:\>flashnul **E:** -L *path\to\arch.iso*

```

在您真的确定要写入这些数据时，输入yes，然后等它写入完成。如果您见到拒绝访问的错误提示，关闭所有打开的资源管理器的窗口。

如果是在 Vista 或者 Win7 下，您需要以管理员的身份打开控制台，否则flashnul不能以块设备的方式访问 U 盘，而只能通过 Windows 提供的驱动句柄写入数据。

**注意:** 请确认您使用的是盘符而不是数字。flashnul 1rc1, Windows 7 x64.

#### 在内存加载安装介质

这个方法使用 [Syslinux (简体中文)](/index.php/Syslinux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Syslinux (简体中文)") 和一个 [Ramdisk](/index.php/Ramdisk "Ramdisk") ([MEMDISK](http://www.syslinux.org/wiki/index.php/MEMDISK)) 来把整个 Arch Linux ISO 镜像加载到内存中。因为它将完全运行于系统内存中，您要确保使用这种方法安装的系统有足够的内存。至少 500MB 到 1G 内存就足以在 MEMDISK 上安装 Arch Linux。 Arch Linux 和 MEMDISK 系统要求参见[新手指南](/index.php/Beginners%27_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Beginners' guide (简体中文)")和[这里](http://www.etherboot.org/wiki/bootingmemdisk#preliminaries)。[论坛参考贴](https://bbs.archlinux.org/viewtopic.php?id=135266)。

**小贴士:** 一旦安装程序加载完毕，您就可以移除 U 盘，甚至再在另一台机器上用它开始执行整个安装步骤。使用 MEMDISK 还允许你在同一个 U 盘中引导并安装 Arch Linux 到它上面。

##### 准备 U 盘

首先格式化 U 盘分区为 ‘’‘FAT32 **文件系统。然后在格式化后的磁盘中创建以下目录：**

*   `Boot`
    *   `Boot/ISOs`
    *   `Boot/Settings`

##### 复制需要的文件到 U 盘

然后，把要引导的 ISO 复制到 `Boot/ISOs` 目录。接着，从[这里](http://www.kernel.org/pub/linux/utils/boot/syslinux/) 最新版的 [syslinux](https://www.archlinux.org/packages/?name=syslinux) 中提取以下文件并复制到下列目录：

*   `./win32/syslinux.exe` 到桌面或者系统中的 Downloads 目录。
*   `./memdisk/memdisk` 到 U 盘中的 {{ic|Settings} 目录。

##### 创建配置文件

复制完所需文件后，在 U 盘的 /Boot/Settings 目录中创建文件 `syslinux.cfg`：

**警告:** `INITRD` 一行中，一定要用复制到 `ISOs` 目录中的 ISO 文件名！
 `/Boot/Settings/syslinux.cfg` 
```
DEFAULT arch_iso

 LABEL arch_iso
         MENU LABEL Arch Setup
         LINUX memdisk
         INITRD /Boot/ISOs/archlinux-2013.08.01-dual.iso
         APPEND iso
```

更多关于 Syslinux 的信息，参见 [Arch Wiki 文章](/index.php/Syslinux "Syslinux")。

##### 最后的步骤

最后，在 `syslinux.exe` 所在目录创建一个 `*.bat` 文件并运行（如果是在 Vista 或者 Windows 7 下，需要“以管理员身份运行”）：

 `C:\Documents and Settings\username\Desktop\install.bat` 
```
 @echo off
 syslinux.exe -m -a -d /Boot/Settings X:
```

## 故障排除

*   对于 [MEMDISK 方法](#.E5.9C.A8.E5.86.85.E5.AD.98.E4.B8.AD.E5.8A.A0.E8.BD.BD.E5.AE.89.E8.A3.85.E4.BB.8B.E8.B4.A8)，如果你尝试引导 i686 版本的系统时碰到了著名的 *30 seconds error*，那么在 `Boot Arch Linux (i686)` 条目上按 `Tab` 键，然后在末尾添加 `vmalloc=448M`。参考： *如果你的映像大于 128MiB 且你使用的是32位操作系统，你必须增加最大内存使用参数vmalloc*。[(*)](http://www.syslinux.org/wiki/index.php/MEMDISK#-_memdiskfind_in_combination_with_phram_and_mtdblock)

*   如果你碰到因 `/dev/disk/by-label/ARCH_XXXXXX` 未挂载而导致的 *30 seconds error*，可尝试重命名你的 USB 媒介为 `ARCH_XXXXXX`（例如 `ARCH_201409`）。

## 参见

*   [Gentoo wiki - LiveUSB/HOWTO](https://wiki.gentoo.org/wiki/LiveUSB/HOWTO)
*   [Fedora wiki - How to create and use Live USB](https://fedoraproject.org/wiki/How_to_create_and_use_Live_USB)
*   [openSUSE wiki - SDB:Live USB stick](http://en.opensuse.org/SDB:Live_USB_stick)