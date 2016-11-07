**翻译状态：** 本文是英文页面 [Improve_Boot_Performance](/index.php/Improve_Boot_Performance "Improve Boot Performance") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2012-11-04，点击[这里](https://wiki.archlinux.org/index.php?title=Improve_Boot_Performance&diff=0&oldid=233480)可以查看翻译后英文页面的改动。

本文将为读者提供数种加速系统启动的方法。通过学习实践这些方法，读者不仅能改善系统性能，还能学习系统启动脚本的知识。

## Contents

*   [1 启动过程分析](#.E5.90.AF.E5.8A.A8.E8.BF.87.E7.A8.8B.E5.88.86.E6.9E.90)
    *   [1.1 使用 systemd-analyze](#.E4.BD.BF.E7.94.A8_systemd-analyze)
    *   [1.2 使用 systemd-bootchart](#.E4.BD.BF.E7.94.A8_systemd-bootchart)
    *   [1.3 使用 bootchart2](#.E4.BD.BF.E7.94.A8_bootchart2)
*   [2 自己编译内核](#.E8.87.AA.E5.B7.B1.E7.BC.96.E8.AF.91.E5.86.85.E6.A0.B8)
*   [3 Early start for services](#Early_start_for_services)
*   [4 Staggered spin-up](#Staggered_spin-up)
*   [5 避免重复挂载](#.E9.81.BF.E5.85.8D.E9.87.8D.E5.A4.8D.E6.8C.82.E8.BD.BD)
*   [6 精简输出信息](#.E7.B2.BE.E7.AE.80.E8.BE.93.E5.87.BA.E4.BF.A1.E6.81.AF)
*   [7 参阅](#.E5.8F.82.E9.98.85)

## 启动过程分析

### 使用 systemd-analyze

systemd 提供了一个分析启动过程的工具 —— `systemd-analyze`。可以用它看看哪些单元拖慢了开机过程，并据此进行优化。

查看开机过程在内核/用户空间消耗的时间：

```
$ systemd-analyze

```

**提示：** 如果使用 [UEFI](/index.php/UEFI "UEFI") 引导，且启动引导器实现了 systemd 的 [Boot Loader Interface](http://www.freedesktop.org/wiki/Software/systemd/BootLoaderInterface)（目前只有 [Gummiboot](/index.php/Gummiboot "Gummiboot") 实现了），**systemd-analyze** 还可以显示 EFI 固件和启动引导器自身花费的时间。

按照耗费时间顺序，输出启动每个单元耗费的时间：

```
$ systemd-analyze blame

```

在开机过程的一些时刻, 需要特定的单元成功启动了才能继续. 查看在启动链中哪些单元处于这种危急时刻, 可以:

```
$ systemd-analyze critical-chain

```

生成类似于 [bootchart](/index.php/Bootchart_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Bootchart (简体中文)") 的开机过程图表：

```
$ systemd-analyze plot > plot.svg

```

### 使用 systemd-bootchart

自2012年10月17日，bootchart 工具已经合并进 systemd 中，使用方法和原来的 bootchart 大同小异，添加下列内容到内核参数即可：

```
initcall_debug printk.time=y init=/usr/lib/systemd/systemd-bootchart

```

更多信息请查看 [manpage](http://www.freedesktop.org/software/systemd/man/systemd-bootchart.html)

### 使用 bootchart2

由于没有办法在内核参数设置两个 init，所以不能使用源里的 bootchart。不过，[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)") 软件包 [bootchart2-git](https://aur.archlinux.org/packages/bootchart2-git/) 提供了一个的 systemd 服务，这样就可以和 systemd 一起使用。安装后启用即可：

 `# systemctl enable bootchart.service` 

详情参阅 [bootchart 文档](https://github.com/mmeeks/bootchart)。

## 自己编译内核

自己编译内核、关闭不需要的功能，恐怕是加速系统启动的最有效方法了。 更多信息参见：[Kernel Compilation From Source](/index.php/Kernel_Compilation_From_Source "Kernel Compilation From Source")

## Early start for services

One central feature of systemd is [D-Bus](/index.php/D-Bus "D-Bus") and socket activation. This causes services to be started when they are first accessed and is generally a good thing. However, if you know that a service (like [UPower](/index.php/UPower "UPower")) will always be started during boot, then the overall boot time might be reduced by starting it as early as possible. This can be achieved (if the service file is set up for it, which in most cases it is) by issuing:

```
# systemctl enable upower

```

This will cause systemd to start UPower as soon as possible, without causing races with the socket or D-Bus activation.

## Staggered spin-up

有些硬件使用[staggered spin-up](https://en.wikipedia.org/wiki/Spin-up#Staggered_spin-up "wikipedia:Spin-up")，操作系统一个一个访问硬盘，以减少耗电。这会降低启动速度，大部分用户都不需要开启。检查是否开启：

```
$ dmesg | grep SSS

```

如果没有查到，表示未启动。如果有显示，可以将`libahci.ignore_sss=1` 加入 [kernel line](/index.php/Kernel_line "Kernel line") 进行禁用。

## 避免重复挂载

[mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")提供了 `fsck` 钩子，将启动加载配置中的 root 从 `ro` 修改为 `rw` 并删除 `/etc/fstab` 中的 root 挂载，可以避免重复挂载。挂载参数可以通过`rootflags=[mount options...]`设置。

删除 `/etc/fstab` 中的 API 文件系统，systemd 会自动挂载它们。下面命令可以获得这些 API 文件系统的列表：

```
$ pacman -Ql systemd | grep '\.mount$'

```

`/home`等其他文件系统可以通过自定义挂载单元进行挂载。

## 精简输出信息

修改启动加载器内核参数中的 `verbose` 为 `quiet` 即可。对于某些用户，特别是 SSD 用户，TTY 的龟速实际上成为了性能瓶颈，精简输出信息实际上有利于提高性能。

## 参阅

*   [e4rat](/index.php/E4rat "E4rat")
*   [udev](/index.php/Udev "Udev")
*   [Daemon](/index.php/Daemon "Daemon")
*   [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")
*   [Improving performance](/index.php/Improving_performance "Improving performance")
*   [Systemd](/index.php/Systemd "Systemd") - An alternative init process
*   [Bootchart](/index.php/Bootchart "Bootchart") - A tool to assist in profiling the boot process
*   [Kexec](/index.php/Kexec "Kexec") A tool to reboot very quickly without waiting for the whole BIOS boot process to finish.