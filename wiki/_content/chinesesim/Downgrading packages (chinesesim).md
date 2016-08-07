**翻译状态：** 本文是英文页面 [Downgrading_Packages](/index.php/Downgrading_Packages "Downgrading Packages") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-08-05，点击[这里](https://wiki.archlinux.org/index.php?title=Downgrading_Packages&diff=0&oldid=438900)可以查看翻译后英文页面的改动。

在决定降级之前，请小心考虑。如果是因为现有包有Bug，请在[Bug追踪系统](https://bugs.archlinux.org/)搜索现有的Bug报告。如果没有，请花上几分钟帮忙把它报告给Arch的Bug追踪系统或软件包的项目地址，或者在论坛中警告其他可能遇到类似问题的用户。

**警告:**

*   降级某个软件包可能需要降级相应的依赖包.如果依赖包数量巨大,参见[Arch Linux Archive (简体中文)#如何恢复所有包到指定日期](/index.php/Arch_Linux_Archive_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.A6.82.E4.BD.95.E6.81.A2.E5.A4.8D.E6.89.80.E6.9C.89.E5.8C.85.E5.88.B0.E6.8C.87.E5.AE.9A.E6.97.A5.E6.9C.9F "Arch Linux Archive (简体中文)").
*   在修改配置文件和脚本时请小心.只要我们不绕过pacman的安全措施,它将为我们处理这些问题.

## Contents

*   [1 如何降级软件包](#.E5.A6.82.E4.BD.95.E9.99.8D.E7.BA.A7.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [1.1 使用pacman的临时文件](#.E4.BD.BF.E7.94.A8pacman.E7.9A.84.E4.B8.B4.E6.97.B6.E6.96.87.E4.BB.B6)
    *   [1.2 降级内核](#.E9.99.8D.E7.BA.A7.E5.86.85.E6.A0.B8)
    *   [1.3 Arch Linux Archive](#Arch_Linux_Archive)
    *   [1.4 手动编译](#.E6.89.8B.E5.8A.A8.E7.BC.96.E8.AF.91)
        *   [1.4.1 vABS - Versioned Arch Build System](#vABS_-_Versioned_Arch_Build_System)
    *   [1.5 自动化](#.E8.87.AA.E5.8A.A8.E5.8C.96)
*   [2 从[testing]中返回](#.E4.BB.8E.5Btesting.5D.E4.B8.AD.E8.BF.94.E5.9B.9E)

## 如何降级软件包

### 使用pacman的临时文件

如果一个新包刚刚被安装并且没有删除[pacman cache](/index.php/Pacman#Cleaning_the_package_cache "Pacman"),你可以在`/var/cache/pacman/pkg/`中找到较早版本. 安装替换现有的版本.[pacman](/index.php/Pacman "Pacman")会处理依赖包但不会处理依赖库的版本冲突。如果一个其依赖库因该包降级需要降级，你需要手动降级这些包。

```
# cd /var/cache/pacman/pkg/
# pacman -U <file_name_of_the_package>

```

当成功降级该包以后，请暂时将其加入`pacman.conf`的[IgnorePkg section](/index.php/Pacman#Skip_package_from_being_upgraded "Pacman")，直到您的问题被解决。

### 降级内核

如果您在升级内核后无法启动，您可以通过使用live CD来降级内核。方法类似Arch Linux的安装进程。启动后在`/mnt`挂载你的根目录文件系统，别忘了挂载其他分区如`/boot`或`/var`等等。(例子 `mount /dev/sdc3 /mnt/boot`)。然后[chroot](/index.php/Chroot "Chroot")进入系统。

```
# arch-chroot /mnt /bin/bash

```

现在你可以在`/var/cache/pacman/pkg` 寻找旧的安装包。必须降级的有[linux](https://www.archlinux.org/packages/?name=linux)， [linux-headers](https://www.archlinux.org/packages/?name=linux-headers)和任何内核模块。举例来说：

```
# pacman -U linux-3.5.6-1-x86_64.pkg.tar.xz linux-headers-3.5.6-1-x86_64.pkg.tar.xz virtualbox-host-modules-4.2.0-5-x86_64.pkg.tar.xz

```

退出并重启。

### Arch Linux Archive

[Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive")是[official repositories](/index.php/Official_repositories "Official repositories")的日更快照。

*ALA*能被用来降级包或者还原整个系统到过去版本。

### 手动编译

如果上述方法都失效，那你就需要自己动手编译旧版本的软件包了。从abs中先取出该软件包的PKGBUILD文件，然后修改相应的内容（通常是版本号）。或者访问 [https://www.archlinux.org/packages/](https://www.archlinux.org/packages/) 搜索你需要的降级的软件包，然后点 "查看修改" 链接，选择“查看日志“。找到你需要的版本然后点击路径。然后下载相应的文件再用makepkg编译即可。

对于AUR包来说，只能在http://pkgbuild.com/git/aur-mirror.git/ 处找到旧包的PKGBUILD，或者你可以到[Unofficial User Repositories]]处找到旧的二进制包。

#### vABS - Versioned Arch Build System

[vABS](https://vabs.archlinux-br.org) 是一个ABS的拓展物，主要用来保存不同版本的官方PKGBUILD。你能够在其中找到两年内的旧版本。选择你期望的版本并编译安装，详细参见[这里](https://www.archlinux-br.org/vabs_en).

### 自动化

[downgrader](https://aur.archlinux.org/packages/downgrader/) 是一个基于libalpm的小工具, 支持 pacman log，使用 [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive")，本地缓存和[ARM](http://repo-arm.archlinuxcn.org)进行降级.

[downgrade](https://aur.archlinux.org/packages/downgrade/) 基于Bash使用本地缓存和[Arch Rollback Machine](/index.php/Arch_Rollback_Machine "Arch Rollback Machine")。详见`man downgrade`。

[agetpkg-git](https://aur.archlinux.org/packages/agetpkg-git/)功能与上述类似。

## 从[testing]中返回

参见 [Official repositories#Disabling testing repositories](/index.php/Official_repositories#Disabling_testing_repositories "Official repositories")。