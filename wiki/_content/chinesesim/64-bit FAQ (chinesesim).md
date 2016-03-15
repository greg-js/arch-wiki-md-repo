下面是关于Arch64的问答列表。

## Contents

*   [1 我如何确定我的处理器是否支持 x86_64?](#.E6.88.91.E5.A6.82.E4.BD.95.E7.A1.AE.E5.AE.9A.E6.88.91.E7.9A.84.E5.A4.84.E7.90.86.E5.99.A8.E6.98.AF.E5.90.A6.E6.94.AF.E6.8C.81_x86_64.3F)
    *   [1.1 Linux 用户](#Linux_.E7.94.A8.E6.88.B7)
    *   [1.2 Windows 用户](#Windows_.E7.94.A8.E6.88.B7)
*   [2 我应该使用32位还是64位版本的 Arch?](#.E6.88.91.E5.BA.94.E8.AF.A5.E4.BD.BF.E7.94.A832.E4.BD.8D.E8.BF.98.E6.98.AF64.E4.BD.8D.E7.89.88.E6.9C.AC.E7.9A.84_Arch.3F)
*   [3 如何安装Arch64？](#.E5.A6.82.E4.BD.95.E5.AE.89.E8.A3.85Arch64.EF.BC.9F)
*   [4 是否拥有所有32位 Arch 环境下的软件包？](#.E6.98.AF.E5.90.A6.E6.8B.A5.E6.9C.89.E6.89.80.E6.9C.8932.E4.BD.8D_Arch_.E7.8E.AF.E5.A2.83.E4.B8.8B.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85.EF.BC.9F)
*   [5 为什么使用64位?](#.E4.B8.BA.E4.BB.80.E4.B9.88.E4.BD.BF.E7.94.A864.E4.BD.8D.3F)
*   [6 我该设置哪个仓库给pacman使用？](#.E6.88.91.E8.AF.A5.E8.AE.BE.E7.BD.AE.E5.93.AA.E4.B8.AA.E4.BB.93.E5.BA.93.E7.BB.99pacman.E4.BD.BF.E7.94.A8.EF.BC.9F)
*   [7 Arch64缺少什么？](#Arch64.E7.BC.BA.E5.B0.91.E4.BB.80.E4.B9.88.EF.BC.9F)
*   [8 我能否在Arch64里运行32-bit应用程序？](#.E6.88.91.E8.83.BD.E5.90.A6.E5.9C.A8Arch64.E9.87.8C.E8.BF.90.E8.A1.8C32-bit.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F.EF.BC.9F)
*   [9 我可以在Arch64下编译给i686用的32-bit软件包吗？](#.E6.88.91.E5.8F.AF.E4.BB.A5.E5.9C.A8Arch64.E4.B8.8B.E7.BC.96.E8.AF.91.E7.BB.99i686.E7.94.A8.E7.9A.8432-bit.E8.BD.AF.E4.BB.B6.E5.8C.85.E5.90.97.EF.BC.9F)
    *   [9.1 Multilib 仓库 - Multilib_Project](#Multilib_.E4.BB.93.E5.BA.93_-_Multilib_Project)
    *   [9.2 Chroot](#Chroot)
*   [10 我可以无需重新安装将我的系统从i686升级/切换到x86_64吗？](#.E6.88.91.E5.8F.AF.E4.BB.A5.E6.97.A0.E9.9C.80.E9.87.8D.E6.96.B0.E5.AE.89.E8.A3.85.E5.B0.86.E6.88.91.E7.9A.84.E7.B3.BB.E7.BB.9F.E4.BB.8Ei686.E5.8D.87.E7.BA.A7.2F.E5.88.87.E6.8D.A2.E5.88.B0x86_64.E5.90.97.EF.BC.9F)

## 我如何确定我的处理器是否支持 x86_64?

### Linux 用户

运行下面的命令：

```
$ less /proc/cpuinfo

```

查找 `flags` 条目。如果你看见 `lm` 标志，那么你的处理器是支持 x86_64 的。

或者你可以运行以下命令：

```
$ grep "^flags.*\blm\b" /proc/cpuinfo

```

### Windows 用户

使用免费软件 [CPU-Z](http://www.cpuid.com/cpuz.php)，可以确定CPU是否支持64位。

带有 AMD 的 "AMD64" 指令集或者英特尔的 "EM64T" 指令集的 CPU 兼容 x86_64 发行版和二进制包。

## 我应该使用32位还是64位版本的 Arch?

如果你的处理器支持 [x86_64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64")，你应该使用 Arch64。

## 如何安装Arch64？

使用[官方安装iso光盘](https://www.archlinux.org/download/).

## 是否拥有所有32位 Arch 环境下的软件包？

仓库已经被移植，并且可喜的是完全可以正常工作。

有很少部分 [AUR](/index.php/AUR "AUR") 中的包只列出了 `'i686'`，但是大部分包都可以在64位环境工作，只需要添加 `'x86_64'`。

## 为什么使用64位?

64位系统(大多数情况下)更快，而且更安全。更安全是由于拥有 [Address space layout randomization (ASLR)](https://en.wikipedia.org/wiki/Address_space_layout_randomization "wikipedia:Address space layout randomization") 、 [Position-independent code (PIC)](https://en.wikipedia.org/wiki/Position-independent_code "wikipedia:Position-independent code") 特性，以及 [NX Bit](https://en.wikipedia.org/wiki/NX_Bit "wikipedia:NX Bit") (它在i686内核中由于禁用了PAE而无法使用)。如果你的计算机在运行4GB或者更多的内容，应该使用64位系统，因为多余的内存无法被32位系统分配。

编程人员也更加倾向于不关心32位系统，因为新的x86 CPU通常都支持64位扩展。

还有许多其他的理由让我们不使用32位系统，但是在内核、用户空间和单独的程序中我们没有办法列出所有的64位比32位做得好的地方。

## 我该设置哪个仓库给pacman使用？

所有仓库都支持移植。

## Arch64缺少什么？

实际上，没有。现在基本上所有的程序都支持64位，或者正在过渡到兼容64位。

最大的问题是一些包或者是**闭源**的，或者包含一些x86的汇编代码，很难移植到64位中(尤其是模拟器)。

下列应用程序原本是有问题的，现在可以在[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)") 中得到，并且工作很好：

*   Acrobat Reader 现在没有 64 位版本，但是你也可以在兼容模式中运行32位版本。有一些开源替代可以用来阅读 PDF 文件。

其他的一切都运行的很好。如果你发现某个Arch32软件包可以在x86_64下编译而又没有移植，（也许你在其他的64位发行版中发现了原生包），请联系开发人员或在论坛请求新软件包。

## 我能否在Arch64里运行32-bit应用程序？

可以！

*   你可使用 multilib 软件仓库中的 `lib32-*` 库。添加下面几行到 `/etc/pacman.conf` 启用该软件仓库：

```
[multilib]
Include = /etc/pacman.d/mirrorlist

```

现在(2011年12月)，它包含 wine 和 skype。另外，还包含一个 multilib 编译器。

*   或者你可以创建另一个使用32位系统的 chroot (参考 [Arch64 Install bundled 32bit system](/index.php/Arch64_Install_bundled_32bit_system "Arch64 Install bundled 32bit system")):

启动到Arch64，startx，打开一个终端：

```
$ xhost +local:
$ su
# mount /dev/sda1 /mnt/arch32
# mount --bind /proc /mnt/arch32/proc
# chroot /mnt/arch32
# su your32bitusername
$ /usr/bin/command-you want # or eg: /opt/mozilla/bin/firefox

```

某些32-bit应用程序（例如OpenOffice）可能需要其它绑定。下面几行可以放到rc.local里以确保满足所有32-bit应用程序的需要（假设fstab里已经挂载/mnt/arch32于）：

```
mount --bind /dev /mnt/arch32/dev
mount --bind /dev/pts /mnt/arch32/dev/pts
mount --bind /dev/shm /mnt/arch32/dev/shm
mount --bind /proc /mnt/arch32/proc
mount --bind /proc/bus/usb /mnt/arch32/proc/bus/usb
mount --bind /sys /mnt/arch32/sys
mount --bind /tmp /mnt/arch32/tmp
#如果你不使用同一个home文件夹的话，可以注释掉下面这行
mount --bind /home /mnt/arch32/home

```

然后在终端里输入：

```
$ xhost +localhost
$ sudo chroot /mnt/arch32 su your32bitusername /opt/openoffice/program/soffice

```

## 我可以在Arch64下编译给i686用的32-bit软件包吗？

可以。你可以使用：

*   从multilibC仓库中使用相关包的 multilib 版本，或者
*   一个 i686 chroot。

### Multilib 仓库 - [Multilib_Project](/index.php/Multilib_Project "Multilib Project")

想要使用 multilib 仓库，编辑 `/etc/pacman.conf` 添加下面内容：

```
[multilib]
Include = /etc/pacman.d/mirrorlist

```

升级系统：

```
# pacman -Syu

```

然后安装 [gcc-multilib](https://www.archlinux.org/packages/?name=gcc-multilib) 及其依赖。

```
pacman -S gcc-multilib gcc-libs-multilib binutils-multilib libtool-multilib lib32-glibc

```

**注意:** 如果系统安装了 `base-devel` ，用户必须按照下面的说明用 [multilib] 版本替换 [extra] 版本。

**注意:** [gcc-multilib](https://www.archlinux.org/packages/?name=gcc-multilib) 能够编译32位和64位代码。你可以在 x86_64 系统中安全的安装 `multilib-devel` 然后移除 `base-devel`。参见 [https://bbs.archlinux.org/viewtopic.php?id=102828](https://bbs.archlinux.org/viewtopic.php?id=102828) 获取更多信息。

```
# pacman -S gcc-multilib gcc-libs-multilib binutils-multilib libtool-multilib lib32-glibc
resolving dependencies...
warning: dependency cycle detected:
warning: lib32-gcc-libs will be installed before its gcc-libs-multilib dependency
looking for inter-conflicts...
:: gcc-libs-multilib and gcc-libs are in conflict. Remove gcc-libs? [y/N] y
:: binutils-multilib and binutils are in conflict. Remove binutils? [y/N] y
:: gcc-multilib and gcc are in conflict. Remove gcc? [y/N] y
:: libtool-multilib and libtool are in conflict. Remove libtool? [y/N] y

Remove (4): gcc-libs-4.6.1-1  binutils-2.21.1-1  gcc-4.6.1-1  libtool-2.4-4

Total Removed Size:   87.65 MB

Targets (7): lib32-glibc-2.14-4  lib32-gcc-libs-4.6.1-1  gcc-libs-multilib-4.6.1-1  binutils-multilib-2.21.1-1
             gcc-multilib-4.6.1-1  lib32-libtool-2.4-2  libtool-multilib-2.4-2

Total Download Size:    25.04 MB
Total Installed Size:   108.27 MB

Proceed with installation? [Y/n]

```

在 x86_64 系统上编译 i686 程序，只需要简单的添加下面的几行到 `~/.makepkg.conf`

```
CARCH="i686"
CHOST="i686-pc-linux-gnu"
CFLAGS="-m32 -march=i686 -mtune=generic -O2 -pipe -fstack-protector --param=ssp-buffer-size=4 -D_FORTIFY_SOURCE=2"
CXXFLAGS="${CFLAGS}"

```

然后通过下面的命令调用 makepkg

```
$ linux32 makepkg -src

```

记得编译完成 i686 包之后移除或更改 `~/.makepkg.conf`。

### Chroot

想要使用 i686 chroot (推荐在Arch64里使用i686 iso的"quickinstall"来安装，或者参考 [Arch64 Install bundled 32bit system](/index.php/Arch64_Install_bundled_32bit_system "Arch64 Install bundled 32bit system"))。从current仓库安装"linux32" 封装包，使得chroot象一个真正的i686系统。然后用这个脚本以root身份登录到chroot环境：

```
#!/bin/bash
mount --bind /dev /path-to-your-chroot/dev
mount --bind /dev/pts /path-to-your-chroot/dev/pts
mount --bind /dev/shm /path-to-your-chroot/dev/shm
mount -t proc none /path-to-your-chroot/proc
mount -t sysfs none /path-to-your-chroot/sys
linux32 chroot /path-to-your-chroot

```

如果你在x86_64宿主系统里保留了源码，你可以在脚本里再加入

```
"mount --bind /path-to-your-stored-sources /path-to-your-chroot/path-to-your-stored-sources" 

```

使得宿主可以共享源码给chroot系统，使得可以在 `/etc/makepkg.conf` 中用来创建软件包。

## 我可以无需重新安装将我的系统从i686升级/切换到x86_64吗？

不可以。但是有一个[帖子](https://bbs.archlinux.org/viewtopic.php?id=64485)说明了如果成功的从32位迁移到64位而不损失任何配置/设置/数据。注意：需要用一个大的外置硬盘来完成迁移

然而，你也可以用Arch64安装光盘启动系统，挂载磁盘，备份所有你希望保留的非32-bit二进制文件（例如/home和/etc，然后开始安装。

你也许需要阅读 [Migrating Between Architectures Without Reinstalling](/index.php/Migrating_Between_Architectures_Without_Reinstalling "Migrating Between Architectures Without Reinstalling")。