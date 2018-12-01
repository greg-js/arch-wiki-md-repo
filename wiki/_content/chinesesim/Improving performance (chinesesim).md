本文将介绍关于系统性能诊断的基本知识，以及优化系统性能的具体步骤。

## Contents

*   [1 基础工作](#基础工作)
    *   [1.1 寻找瓶颈](#寻找瓶颈)
    *   [1.2 首选方案](#首选方案)
    *   [1.3 妥协的考量](#妥协的考量)
    *   [1.4 跑分](#跑分)
*   [2 存储设备](#存储设备)
    *   [2.1 分散存储](#分散存储)
    *   [2.2 交换分区/文件](#交换分区/文件)
    *   [2.3 组RAID (简体中文)](#组RAID_(简体中文))
    *   [2.4 硬盘的连接方式](#硬盘的连接方式)
    *   [2.5 分区方案](#分区方案)
    *   [2.6 文件系统](#文件系统)
        *   [2.6.1 挂载选项](#挂载选项)
        *   [2.6.2 Ext3](#Ext3)
        *   [2.6.3 Ext4](#Ext4)
        *   [2.6.4 JFS](#JFS)
        *   [2.6.5 XFS](#XFS)
        *   [2.6.6 Reiserfs](#Reiserfs)
        *   [2.6.7 Btrfs](#Btrfs)
    *   [2.7 调整内核参数](#调整内核参数)
    *   [2.8 优化SSD](#优化SSD)
    *   [2.9 使用RAM disks](#使用RAM_disks)
    *   [2.10 USB存储设备](#USB存储设备)
*   [3 CPU](#CPU)
    *   [3.1 使用Verynice服务](#使用Verynice服务)
*   [4 显卡](#显卡)
    *   [4.1 Xorg.conf配置](#Xorg.conf配置)
    *   [4.2 Driconf](#Driconf)
    *   [4.3 GPU超频](#GPU超频)
*   [5 内存及虚拟内存](#内存及虚拟内存)
    *   [5.1 将临时文件转移到tmpfs](#将临时文件转移到tmpfs)
    *   [5.2 Swappiness](#Swappiness)
    *   [5.3 Compcache/Zram](#Compcache/Zram)
    *   [5.4 使用显存](#使用显存)
    *   [5.5 预读](#预读)
        *   [5.5.1 Go-preload](#Go-preload)
        *   [5.5.2 Preload](#Preload)
*   [6 系统启动](#系统启动)
    *   [6.1 待机](#待机)
    *   [6.2 自己编译内核](#自己编译内核)
*   [7 针对特定程序的优化技巧](#针对特定程序的优化技巧)
    *   [7.1 Firefox](#Firefox)
    *   [7.2 Gcc/Makepkg](#Gcc/Makepkg)
    *   [7.3 LibreOffice](#LibreOffice)
    *   [7.4 Pacman](#Pacman)
    *   [7.5 SSH](#SSH)

## 基础工作

### 寻找瓶颈

性能优化的最佳方法是找到瓶颈，因为这个子系统是导致系统速度低下的主要原因。查看系统配置表可以发现瓶颈，也可以通过以下方式寻找线索：

*   运行多个大型程序（如OpenOffice.org、Firefox等）时变卡，提示瓶颈可能是内存。为进一步明确内存使用情况，可敲入以下命令，并检查“-/+ buffers/cache”那一栏信息：

```
$ free -m

```

*   如果开机时间非常长，并且第一次加载应用程序也很长（但是启动以后运行却很流畅），这就提示硬盘可能太慢。你可以借助`hdparm`命令测量硬盘速度，请在硬盘空闲时执行：

```
$ hdparm -t /dev/sdx

```

虽然这个命令只测定读取速度，但只要这个速度超过40MB/s就足以应付一般的系统需要。hdparm可在[Official repositories](/index.php/Official_repositories "Official repositories")中找到。

*   如果内存充裕，但是CPU使用率持续高企，那么CPU可能是系统的瓶颈。有多种方法可以监测CPU负荷，比如`top`命令：

```
$ top

```

*   如果仅仅是游戏或视频播放时出现卡顿，那就像是显卡的问题。首先，请使用`glxinfo`检查显卡是否开启了直接渲染功能：

```
$ glxinfo | grep direct

```

`glxinfo`在[mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos)包中。

### 首选方案

最简单有效的改善系统性能的方法是：改用轻量级桌面和应用程序。

*   不安装完整的[桌面环境](/index.php/Desktop_environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop environment (简体中文)")，仅仅使用[窗口管理器](/index.php/Window_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Window manager (简体中文)")。可选的方案包括[Awesome](/index.php/Awesome "Awesome")、[dwm](/index.php/Dwm "Dwm")、[Fluxbox](/index.php/Fluxbox "Fluxbox")、[i3](/index.php/I3 "I3")、[JWM](/index.php/JWM "JWM")、[Openbox](/index.php/Openbox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Openbox (简体中文)")、[wmii](/index.php/Wmii "Wmii")和[xmonad](/index.php/Xmonad "Xmonad")。
*   不用重量级的[GNOME](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)")或[KDE](/index.php/KDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KDE (简体中文)")，改用轻量的桌面环境，如[LXDE](/index.php/LXDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LXDE (简体中文)")或者[Xfce](/index.php/Xfce_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xfce (简体中文)")。
*   改用轻量级应用程序，你可以在[应用程序列表](/index.php/List_of_applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of applications (简体中文)")中搜索命令行界面的程序，或者参考论坛票选出的“年度轻便程序”：[2007](https://bbs.archlinux.org/viewtopic.php?id=41168)、 [2008](https://bbs.archlinux.org/viewtopic.php?id=67951)、 [2009](https://bbs.archlinux.org/viewtopic.php?id=78490)、 [2010](https://bbs.archlinux.org/viewtopic.php?id=88515)、 [2011](https://bbs.archlinux.org/viewtopic.php?id=111878)以及[2012](https://bbs.archlinux.org/viewtopic.php?id=138281)。
*   禁用多余的[系统服务](/index.php/Daemons_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Daemons (简体中文)")。

### 妥协的考量

绝大多数优化都会带来副作用。比如，轻量级软件做到了“轻”，但往往牺牲了“用”（功能）。又比如，系统优化需要花费时间调试、维护，甚至可能造成系统不稳定。用户应该根据自身的需要谨慎选择。

### 跑分

为定量评估优化成果，可使用[benchmarking (简体中文)](/index.php/Benchmarking_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Benchmarking (简体中文)")。

## 存储设备

### 分散存储

如果你有多个存储设备，那么把操作系统的工作负荷均匀分摊到这些设备上，将极大提升系统性能。将`/`、`/usr`、`/home`和`/var`分散到不同的硬盘，显著快于将它们集中放置在同一块硬盘。

### 交换分区/文件

把交换分区/文件放在系统盘以外，对提升速度也有所帮助，尤其是系统频繁使用交换分区/文件时。

### 组[RAID (简体中文)](/index.php/RAID_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "RAID (简体中文)")

如果你有多个硬盘，组一个软RAID或许有不小惊喜。RAID 0可使存储系统的速度翻翻，而且加入的硬盘越多，速度越快，不过，RAID 0没有数据冗余，一旦某个硬盘故障，数据将有损失。RAID 5则是兼顾速度和数据安全的明智选择，但它至少需要3块硬盘。

### 硬盘的连接方式

由于接口速度有差异，所以硬盘连接到主板的方式也将影响系统性能。例如，将固态硬盘接到USB接口，远不如将其接到SATA接口。如果你有很多个硬盘，而主板上的接口有限，那你要充分利用可用的接口，并注意合理安排：

*   PCI/PCIe/SATA
*   将硬盘改装为网络存储设备，通过网卡连接
*   USB/Firewire

使用USB接口时还要注意USB接口是否为“衍生”。如果某两个USB接口正好出自同一个USB根Hub，那么它俩同时使用时将彼此竞争速度。以下命令将帮助你了解个接口的衍生情况：

 `USB设备树`  `$ lsusb -tv`  `PCI设备树`  `$ lspci -tv` 

### 分区方案

对于机械硬盘，分区有可能影响系统性能，因为开头的分区靠近硬盘中心，转速较快。类似的，小的分区可以减少磁盘头的移动，可以提升磁盘性能。因此，建议将系统分区放在开始的部分，并且容量不必太大（10GB左右，取决于具体的需要）。

### 文件系统

#### 挂载选项

`noatime、nodiratime`可以提升大部分文件系统的磁盘性能。在默认情况下，Linux会记录文件的最近一次访问时间戳，这需要频繁执行写入操作，而且，访问时间戳对桌面用户意义不大。因此，桌面用户可以通过`noatime`参数可以禁止这种行为（“a”=access），从而提升性能。`nodiratime`参数禁止记录目录的访问时间戳，如果开启了`noatime`，则自动开启了`nodiratime`。 修改了`/etc/fstab`之后，使用下列命令可使新配置生效：

```
# mount -o remount /target

```

少数程序，如`mutt`在`noatime`下无法工作，折衷的方案是使用`relatime`。这个参数允许Linux在修改文件时顺便更新访问时间戳，从而避免了访问时间戳落后于修改时间戳的怪现象。事实上，2.6.30版本（2009年6月发布）及以后的内核，都**默认开启了`relatime`**。

#### Ext3

参见[Ext3](/index.php/Ext3 "Ext3")。

#### Ext4

参见[Ext4 (简体中文)](/index.php/Ext4_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Ext4 (简体中文)")。

#### JFS

参见[JFS Filesystem](/index.php/JFS_Filesystem#Optimizations "JFS Filesystem")。

#### XFS

参见[XFS](/index.php/XFS "XFS")、["boost knobs" are already "on" by default](http://xfs.org/index.php/XFS_FAQ#Q:_I_want_to_tune_my_XFS_filesystems_for_.3Csomething.3E)。

#### Reiserfs

参见[Reiser4](/index.php?title=Merge&action=edit&redlink=1 "Merge (page does not exist)")和[Using ReiserFS and Linux](http://www.funtoo.org/Funtoo_Filesystem_Guide,_Part_2)。 挂载选项`data=writeback`可以提高速度，但是，死机或突然断电时将丢失数据。挂载选项`notail`可以增加大约5%的磁盘空间，并提升速度。你还可以将日志文件和数据文件分散在不同的磁盘，从而减少硬盘负荷。不过，要达到这个目的需要重新格式化：

```
# mkreiserfs –j /dev/sd**a1** /dev/sd**b1**

```

其中，`/dev/sd**a1**`将保存日志，而`/dev/sd**b1**`将保存数据文件。

#### Btrfs

参见[defragmentation](/index.php/Btrfs#Defragmentation "Btrfs")和[compression](/index.php/Btrfs#Compression "Btrfs")。

### 调整内核参数

参见[Low write performance on SLES 11 servers with large RAM](http://www.novell.com/support/kb/doc.php?id=7010287)和[Better Linux Disk Caching & Performance with vm.dirty_ratio & vm.dirty_background_ratio](http://lonesysadmin.net/2013/12/22/better-linux-disk-caching-performance-vm-dirty_ratio/)。 对于大内存来说，需要考虑调整磁盘写缓存。在`[/etc/sysctl.conf](/index.php/Sysctl "Sysctl")`中加入

```
#磁盘写缓存上限（占总内存的百分比）
vm.dirty_ratio = 3
#内核flusher线程开始清理磁盘写缓存的上限
vm.dirty_background_ratio = 2

```

*   vm.dirty_ratio默认是10。按目前的标准配置，内存通常都有4GB，这就意味着磁盘的写缓存有400MB（4GB*10%）。对于磁盘的读取操作而言，大缓存并没有问题，但是对于写操作而言，过大的写缓存将造成两个重要风险，一是意外停机时丢失数据，二是累积太多的数据在内存，一旦开始集中写入操作很容易造成长时间卡机。所以，系统内存较大时，应该将这个参数降下来。
*   调整vm.dirty_background_ratio的原理同上。这个参数一般设置为vm.dirty_ratio的1/4～1/2。

### 优化SSD

参见[SSD#Tips for maximizing SSD performance](/index.php/SSD#Tips_for_maximizing_SSD_performance "SSD")。

### 使用RAM disks

参见[USB stick RAID](http://cs.joensuu.fi/~mmeri/usbraid/)和[Combine RAM disk with disk in RAID](https://bbs.archlinux.org/viewtopic.php?pid=493773#p493773)。

### USB存储设备

If you experienced slow copy speed to pendrive (mainly in KDE), then append these three lines in a [systemd](/index.php/Systemd "Systemd") tmpfile:

 `/etc/tmpfiles.d/local.conf` 
```
w /sys/kernel/mm/transparent_hugepage/enabled - - - - madvise
w /sys/kernel/mm/transparent_hugepage/defrag - - - - madvise
w /sys/kernel/mm/transparent_hugepage/khugepaged/defrag - - - - 0

```

See also [#Tuning kernel parameters](#Tuning_kernel_parameters).

## CPU

改善CPU速度的方法只有一个，那就是超频。超频可是一项复杂而又有风险的操作，不建议盲目使用。超频的最佳手段是通过BIOS。 acpi_cpufreq等工具常用工具无法读取I5或I7处理器超频后的频率。用户需要改用[AUR](/index.php/AUR "AUR")中的[i7z](https://www.archlinux.org/packages/?name=i7z)工具。 另外，请参考[Linux-ck](/index.php/Linux-ck "Linux-ck")以及[这篇文章](http://lkml.org/lkml/2009/9/6/136)修改内核调度器，它们针对桌面应用做了资源配置优化，使之更适应桌面系统的需要。[AUR]]中提供了打补丁内核的PKGBUILD，可以很方便的编译安装。比较著名的有：打了CK补丁包和BFS补丁的[kernel26-ck](https://aur.archlinux.org/packages/kernel26-ck/) ，打了BFS补丁的[kernel26-bfs](https://aur.archlinux.org/packages/kernel26-bfs/)，打了pf补丁集的[kernel26-pf](https://aur.archlinux.org/packages/kernel26-pf/)。

**Note:** BFS/CK适用于桌面机、笔记本，不适用于服务器。少于16个CPU时，这些补丁能起到比较好的效果。此外，Con Kolivas建议把HZ（时钟中断周期）设置为1000。参见：[BFS FAQ](http://ck.kolivas.org/patches/bfs/bfs-faq.txt)、[ck patches](http://www.kernel.org/pub/linux/kernel/people/ck/patches/2.6/2.6.37/2.6.37-ck1/patches/)。

### 使用Verynice服务

[AUR](/index.php/AUR "AUR")中的[verynice](https://aur.archlinux.org/packages/verynice/)是一种可以动态调整程序nice等级的服务。对响应时间敏感的应用程序，如X系统、多媒体程序等，可以在`/etc/verynice.conf`文件中将其标记为*goodexe*，而把那些可以在后台运行的高CPU占用的程序，如make，标记为*badexe*。这样，当系统负荷很重时仍能及时响应用户的指令。

## 显卡

### Xorg.conf配置

显卡性能严重依赖于`/etc/X11/xorg.conf`，请参阅[NVIDIA](/index.php/NVIDIA "NVIDIA")、[ATI](/index.php/ATI "ATI")以及[Intel](/index.php/Intel "Intel")显卡的相关教程修改配置。注意，不当的配置可能导致Xorg停止工作，所以，请审慎操作。

### Driconf

[driconf](https://www.archlinux.org/packages/?name=driconf)是[官方库](/index.php/Official_repositories "Official repositories")中收录的小工具，它可以修改开源驱动的直接渲染设置。启用HyperZ功能将显著改善性能。

### GPU超频

GPU超频要比CPU超频简单得多，通过软件可以实时调整GPU时钟频率。

*   ATI显卡可使用[rovclock](https://aur.archlinux.org/packages/rovclock/)或者[amdoverdrivectrl](https://aur.archlinux.org/packages/amdoverdrivectrl/)
*   NVIDIA显卡可使用[nvclock](https://aur.archlinux.org/packages/nvclock/)。
*   Intel显卡可使用[GMABooster.com](http://www.gmabooster.com/)出品的[gmabooster](https://aur.archlinux.org/packages/gmabooster/)。

超频设置可以保存到`~/.xinitrc`，每次X启动之后就能自动超频。当然，更安全的做法应该是按需设置。

## 内存及虚拟内存

### 将临时文件转移到tmpfs

如果内存充足，可将`/tmp`、`/dev/shm`或者浏览器缓存文件等转移至[tmpfs](https://en.wikipedia.org/wiki/tmpfs "wikipedia:tmpfs")，这些文件将保存在内存中，从而加快软件的响应速度。借助脚本的帮助，可以轻松实现：

*   同步浏览器缓存：[Profile-sync-daemon](/index.php/Profile-sync-daemon "Profile-sync-daemon")。
*   同步任意目录：[Anything-sync-daemon](/index.php/Anything-sync-daemon "Anything-sync-daemon")。

### Swappiness

参阅[Swap#Swappiness](/index.php/Swap#Swappiness "Swap")。

### Compcache/Zram

目前，[Compcache](https://code.google.com/p/compcache/)已被内核模块**zram**取代，它们在内存中开辟一个区域存储压缩过的交换文件。如果系统频繁陷入交换状态，此法可以改善系统响应。不过，Zram目前仍在开发状态，尚未完全稳定，使用需谨慎。 AUR中收录的[zramswap](https://aur.archlinux.org/packages/zramswap/)包含了一个脚本进行自动设置，每个CPU核心对应一个zram设备，总容量等于可用的内存。通过[systemctl](/index.php/Systemd#Basic_systemctl_usage "Systemd")启动`zramswap.service`，可使得每次开机时自动应用这些配置。

**Tip:** 该方法有利于减少由于交换空间造成的固态硬盘读写，延长固态硬盘寿命。

### 使用显存

如果你的系统内存很小，而显存又过剩（这种奇葩系统还真少见），请参阅[Swap on video RAM](/index.php/Swap_on_video_RAM "Swap on video RAM")的方法，将交换文件设置在显存上。

### 预读

通过预读程序、库到内存中，能有效加快程序加载速度。预读通常用于常用的程序，如浏览器。

#### Go-preload

[gopreload-git](https://aur.archlinux.org/packages/gopreload-git/)是来自gentoo的一个预读服务。安装后，通过下列命令采集预读信息：

```
# gopreload-prepare program

```

运行需要预读的程序，收集结束后按回车键。

然后会生成一个预读列表：`/usr/share/gopreload/enabled`。在`/etc/rc.conf`设置开机启动gopreload，Go-preload就会在每次开机时预读列表中的程序。要禁止预读某个程序，只需从`/usr/share/gopreload/enabled`删除项目，或者移入`/usr/share/gopreload/disabled`。

#### Preload

比起Go-preload，[Preload](/index.php/Preload "Preload")更自动化（尽管有违KISS）：只需要在`/etc/rc.conf`添加服务就完事了。

## 系统启动

参见：[加速系统启动](/index.php/Improve_boot_performance_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Improve boot performance (简体中文)")。

### 待机

想要加快系统启动，最好的方法就是不要关电脑，而选择[待机](/index.php/Suspend_to_RAM "Suspend to RAM")。当然，为了可持续发展（至少是电费），不用电脑时还是关了吧。

### 自己编译内核

自己编译内核，删除不需要的模块，可以减少引导时间和内存占用。但通常这是个耗时、枯燥甚至令人厌烦的事情，你可能面临各种错误——甚至最终节约的开机时间还不如你浪费的时间多。但通过自己编译内核，可以学习到不少知识。参见：[here](/index.php/Kernel_Compilation "Kernel Compilation")。

## 针对特定程序的优化技巧

### Firefox

[Firefox (简体中文)](/index.php/Firefox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Firefox (简体中文)")一文提供了不少技巧。常用的有：[禁用 pango](/index.php/Firefox_Tips_and_Tweaks#Improve_rendering_by_disabling_pango "Firefox Tips and Tweaks")，[清理sqlite数据库](/index.php/Firefox_Tips_and_Tweaks#Defragment_the_profile's_SQLite_databases "Firefox Tips and Tweaks")，使用[firefox-pgo](/index.php/Firefox#Firefox_customized_for_speed "Firefox")。另见：[Speed-up Firefox using tmpfs](/index.php/Speed-up_Firefox_using_tmpfs "Speed-up Firefox using tmpfs")、[关闭反钓鱼功能](/index.php/Firefox_Tips_and_Tweaks#Turn_off_anti-phishing "Firefox Tips and Tweaks")。

### Gcc/Makepkg

参见：[Ccache](/index.php/Ccache "Ccache")。

### LibreOffice

参见：[LibreOffice#Speed up LibreOffice](/index.php/LibreOffice#Speed_up_LibreOffice "LibreOffice")。

### Pacman

参见：[Improve pacman performance](/index.php/Improve_pacman_performance "Improve pacman performance")。

### SSH

参见：[Speed up SSH](/index.php/SSH#Speeding_up_SSH "SSH")。