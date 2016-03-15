来自 [Wikipedia](https://en.wikipedia.org/wiki/Kernel_(computing) "wikipedia:Kernel (computing)"):

	*内核是大多数计算机操作系统的主要组件。它是沟通应用程序和硬件层实际数据处理的桥梁。内核的任务包括管理系统的资源(软硬件之间的通信)。*

在Arch Linux中，除了官方内核之外，还有许多各种各样的内核可供选择。这篇文章列出了这些内核和它们的简短介绍。这里还列出了一些可用的内核补丁的介绍。在文章的最后讲述了自己编译内核的方法的总览。

## Contents

*   [1 预编译的内核](#.E9.A2.84.E7.BC.96.E8.AF.91.E7.9A.84.E5.86.85.E6.A0.B8)
    *   [1.1 官方软件包](#.E5.AE.98.E6.96.B9.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [1.2 AUR 软件包](#AUR_.E8.BD.AF.E4.BB.B6.E5.8C.85)
*   [2 补丁与补丁集](#.E8.A1.A5.E4.B8.81.E4.B8.8E.E8.A1.A5.E4.B8.81.E9.9B.86)
    *   [2.1 如何安装](#.E5.A6.82.E4.BD.95.E5.AE.89.E8.A3.85)
    *   [2.2 主要补丁集](#.E4.B8.BB.E8.A6.81.E8.A1.A5.E4.B8.81.E9.9B.86)
        *   [2.2.1 -ck](#-ck)
        *   [2.2.2 -rt](#-rt)
        *   [2.2.3 -bld](#-bld)
        *   [2.2.4 -grsecurity](#-grsecurity)
        *   [2.2.5 Tiny-Patches](#Tiny-Patches)
        *   [2.2.6 -pf](#-pf)
    *   [2.3 独立补丁](#.E7.8B.AC.E7.AB.8B.E8.A1.A5.E4.B8.81)
        *   [2.3.1 Reiser4](#Reiser4)
        *   [2.3.2 Gensplash/fbsplash](#Gensplash.2Ffbsplash)
*   [3 编译](#.E7.BC.96.E8.AF.91)
    *   [3.1 使用 Arch 构建系统(ABS)(推荐)](#.E4.BD.BF.E7.94.A8_Arch_.E6.9E.84.E5.BB.BA.E7.B3.BB.E7.BB.9F.28ABS.29.28.E6.8E.A8.E8.8D.90.29)
    *   [3.2 传统方式](#.E4.BC.A0.E7.BB.9F.E6.96.B9.E5.BC.8F)
    *   [3.3 NVIDIA 闭源驱动](#NVIDIA_.E9.97.AD.E6.BA.90.E9.A9.B1.E5.8A.A8)
*   [4 参见](#.E5.8F.82.E8.A7.81)

## 预编译的内核

### 官方软件包

	[linux](https://www.archlinux.org/packages/?name=linux)

	位于[core]仓库中，包含了对应的Linux内核和内核模块。官方原版内核再加 [两个补丁](https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/linux) (到3.12.1为止).

	[linux-lts](https://www.archlinux.org/packages/?name=linux-lts)

	长期支持版 (LTS) 位于[core]仓库中，包含了对应的Linux内核和内核模块。

### AUR 软件包

	[linux-aufs_friendly](https://aur.archlinux.org/packages/linux-aufs_friendly/)

	The aufs-compatible linux kernel and modules, useful when using [docker](/index.php/Docker "Docker").

	[linux-bfs](https://aur.archlinux.org/packages/linux-bfs/)

	Linux kernel and modules with the [Brain Fuck Scheduler](https://en.wikipedia.org/wiki/Brain_Fuck_Scheduler "wikipedia:Brain Fuck Scheduler") (BFS) - created by Con Kolivas for desktop computers with fewer than 4096 cores, with BFQ I/O scheduler as optional.

	[linux-ck](https://aur.archlinux.org/packages/linux-ck/)

	Linux Kernel built with Con Kolivas' ck1 patchset.

	Additional options which can be toggled on/off in the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") include: BFQ scheduler, nconfig, localmodconfig and use running kernel's config.

	These are patches designed to improve system responsiveness with specific emphasis on the desktop, but suitable to any workload. The ck patches include BFS.

	For further information and installation instructions, please read the [linux-ck](/index.php/Linux-ck "Linux-ck") main article.

	[linux-eee-ck](https://aur.archlinux.org/packages/linux-eee-ck/)

	The Linux Kernel and modules for the Asus Eee PC 701, built with Con Kolivas' ck1 patchset.

	[linux-fbcondecor](https://aur.archlinux.org/packages/linux-fbcondecor/)

	The Linux Kernel and modules with [fbcondecor support](/index.php/Fbsplash "Fbsplash").

	[linux-mainline](https://aur.archlinux.org/packages/linux-mainline/)

	The Mainline Linux Kernel and modules.

	[linux-pax](https://aur.archlinux.org/packages/linux-pax/)

	The Linux Kernel and modules with PaX patches for increased security.

	[linux-ice](https://aur.archlinux.org/packages/linux-ice/)

	The Linux Kernel and modules with gentoo-sources patchset and [TuxOnIce](/index.php/TuxOnIce "TuxOnIce") support.

	[linux-lqx](https://aur.archlinux.org/packages/linux-lqx/)

	[Liquorix](http://liquorix.net) is a distro kernel replacement built using a Debian-targeted configuration and the ZEN kernel sources. Designed for desktop, multimedia, and gaming workloads, it is often used as a Debian Linux performance replacement kernel. Damentz, the maintainer of the Liquorix patchset, is a developer for the ZEN patchset as well.

	[linux-lts34](https://aur.archlinux.org/packages/linux-lts34/)

	The Linux 3.4 Long-Term Support Kernel and modules.

	[linux-lts310](https://aur.archlinux.org/packages/linux-lts310/)

	The Linux 3.10 Long-Term Support Kernel and modules.

	[linux-lts312](https://aur.archlinux.org/packages/linux-lts312/)

	The Linux 3.12 Long-Term Support Kernel and modules.

	[linux-pf](https://aur.archlinux.org/packages/linux-pf/)

	Linux kernel and modules with the pf-kernel patch [-ck patchset (BFS included), TuxOnIce, BFQ] and aufs3.

	[linux-zen](https://www.archlinux.org/packages/?name=linux-zen)

	The [ZEN Kernel](http://zen-kernel.org) is the result of a collaborative effort of kernel hackers to provide the best Linux kernel possible for every day systems. Builds of a ZEN kernel are available [in this repository](https://bbs.archlinux.org/viewtopic.php?id=117157).

	[linux-libre](https://aur.archlinux.org/packages/linux-libre/)

	The Linux Kernel without "binary blobs".

	[kernel-netbook](https://aur.archlinux.org/packages/kernel-netbook/)

	Static kernel for netbooks with Intel Atom N270/N280/N450/N550 such as the Eee PC with the add-on of external firmware ([broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/)) and patchset (BFS + TuxOnIce + BFQ optional) - Only Intel GPU

	[linux-tresor](https://aur.archlinux.org/packages/linux-tresor/)/[linux-lts-tresor](https://aur.archlinux.org/packages/linux-lts-tresor/)

	The current/LTS Linux Kernel and modules with integrated [TRESOR](https://www1.informatik.uni-erlangen.de/tresor)

	[linux-git](https://aur.archlinux.org/packages/linux-git/)

	Linux kernel and modules built using sources from [Linus Torvalds' Git repository](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git).

	[linux-chromebook](https://aur.archlinux.org/packages/linux-chromebook/)

	The Linux kernel with patches added to support chromebook hardware.

## 补丁与补丁集

There are lots of reasons to patch your kernel, the major ones are for performance or support for non-mainline features such as reiser4 file system support. Other reasons might include fun and to see how it is done and what the improvements are.

However, it is important to note that the best way to increase the speed of your system is to first tailor your kernel to your system, especially the architecture and processor type. For this reason using pre-packaged versions of custom kernels with generic architecture settings is not recommended or really worth it. A further benefit is that you can reduce the size of your kernel (and therefore build time) by not including support for things you do not have or use. For example, I always start with the stock kernel config when a new kernel version is released and I remove support for things like bluetooth, video4linux, 1000Mbit ethernet, etc. Stuff **I** know I won't use **before** I build my next kernel! However, this page is not about customizing your kernel config but I would recommend that as a first step to be combined with a patchset later.

### 如何安装

The installation process of custom kernel packages relies on the Arch Build System (AUR). If you haven't built any custom packages yet you may consult the following articles: [Arch Build System](/index.php/Arch_Build_System "Arch Build System") and [Creating packages](/index.php/Creating_packages "Creating packages").

If you haven't actually patched or customized a kernel before it is not that hard and there are many PKGBUILDS on the forum for individual patchsets. However, I would advise you to start from scratch with a bit of research on the benefits of each patchset rather than jumping on the nearest bandwagon! This way you'll learn much more about what you are doing rather than just choosing a kernel at startup and wondering what it actually does.

See [#编译](#.E7.BC.96.E8.AF.91).

**Note:** Don't forget to change the boot options in your bootloader, e.g. grub, to use the new kernel.

### 主要补丁集

First of all it is important to note that patchsets are developed by a variety of people. Some of these people are actually involved in the production of the linux kernel and others are hobbyists, which may reflect its level of reliability and stability.

It is also worth noting that some patchsets are built on the back of other patchsets (which may or may not be reflected in the title of the patch). Patchsets (and kernel updates) can be released **very** frequently and often it is not worth keeping up with ALL of them so do not go crazy, unless you make it your hobby!

You can search google for more sets - remember to use quotes `"-nitro"` for example otherwise google will deliberately **NOT** show the results you want!

**Note:** This section is for **information only** - clearly no guarantees of stability or reliability are implied by inclusion on this page.

#### -ck

These are patches designed to improve system responsiveness with specific emphasis on the desktop, but suitable to any workload. The patches are created and maintained by Con Kolivas, his site is at [http://users.on.net/~ckolivas/kernel/](http://users.on.net/~ckolivas/kernel/). Con maintains a full set but also provides the patches broken down so you can add only those you prefer.

The -ck patches can be found at [http://www.kernel.org/pub/linux/kernel/people/ck/patches/2.6/](http://www.kernel.org/pub/linux/kernel/people/ck/patches/2.6/)

#### -rt

This patchset is maintained by a small group of core developers, led by Ingo Molnar. This patch allows nearly all of the kernel to be preempted, with the exception of a few very small regions of code ("raw_spinlock critical regions"). This is done by replacing most kernel spinlocks with mutexes that support priority inheritance, as well as moving all interrupt and software interrupts to kernel threads.

It further incorporates high resolution timers - a patch set, which is independently maintained.

[as said from the [Real-Time Linux Wiki](http://rt.wiki.kernel.org/index.php/CONFIG_PREEMPT_RT_Patch)]

patch at [http://www.kernel.org/pub/linux/kernel/projects/rt/](http://www.kernel.org/pub/linux/kernel/projects/rt/)

#### -bld

**Warning:** This scheduler is in development.

BLD is best described as a O(1) CPU picking technique. Which is done by reordering CPU runqueues based on runqueue loads. In other words, it keeps the scheduler aware of the load changes, which helps scheduler to keep runqueues in an order. This technique doesn't depend on scheduler ticks. The two most simple things in this technique are: load tracking and runqueue ordering; these are relatively simpler operations. Load tracking will be done whenever a load change happens on the system and based on this load change runqueue will be ordered. So, if we have an ordered runqueue from lowest to highest, then picking the less (or even busiest) runqueue is easy. Scheduler can pick the lowest runqueue without calculation and comparison at the time of placing a task in a runqueue. And while trying to distribute load at sched_exec and sched_fork our best choice is to pick the lowest busiest runqueue of the system. And in this way, system remains balanced without doing any load balancing. At the time of try_to_wake_up picking the idlest runqueue is topmost priority but it has been done as per domain basis to utilize CPU cache properly and it's an area where more concentration is requires.

Google code Webpage: [http://code.google.com/p/bld/](http://code.google.com/p/bld/)

#### -grsecurity

Grsecurity is a security focused patchset. It adds numerous security related features such as Role-Based Access Control and utilizes features of the PaX project. It can be used on a desktop but a public server would receive the greatest benefit. Some applications are incompatible with the additional security measures implemented by this patchset. If this occurs, consider using a lower security level.

The -grsecurity patches can be found at [http://grsecurity.net](http://grsecurity.net)

#### Tiny-Patches

The goal of [Linux Tiny](http://elinux.org/Linux_Tiny) is to reduce its memory and disk footprint, as well as to add features to aid working on small systems. Target users are developers of embedded system and users of small or legacy machines such as 386s.

Patch releases against the mainstream Linux kernel have been discontinued. The developers chose to focus on a few patches and spend their time trying to get them merged into the mainline kernel.

#### -pf

[linux-pf](https://aur.archlinux.org/packages/linux-pf/) is yet another Linux kernel fork which provides you with a handful of awesome features not merged into mainline. It is based on neither existing Linux fork nor patchset, although some unofficial ports may be used if required patches haven't been released officially. The most prominent patches of linux-pf are TuxOnIce, the CK patchset (most notably BFS), AUFS3, LinuxIMQ, l7 filter and BFQ.

### 独立补丁

这里有一些补丁可以直接应用在任何一个主流内核中，或加入到其它补丁集中（可能需要一些调整）。I have included some common ones for starters.

#### Reiser4

[Reiser4](/index.php/Reiser4 "Reiser4")

#### Gensplash/fbsplash

[Gensplash](/index.php/Gensplash "Gensplash") - [http://dev.gentoo.org/~spock/projects/](http://dev.gentoo.org/~spock/projects/)

## 编译

Arch Linux 提供了多种内核构建方式。

### 使用 Arch 构建系统(ABS)(推荐)

推荐使用 [Arch 构建系统](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)")，这样可以充分利用已有的 [linux](https://www.archlinux.org/packages/?name=linux) [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 以及包管理系统。PKGBUILD 已经是结构化的，你可以在下载源代码之后配置内核。

参见 [编译内核/Arch 构建系统](/index.php/Kernels/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernels/Arch Build System (简体中文)").

### 传统方式

另外，也可以不使用 [Arch 构建系统](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)") 编译内核(传统方式)。这个方法需要手动下载内核源代码包，然后在自己的主目录里以普通用户的权限编译。一旦完成配置之后，有两种编译(安装)方式：传统的安装和适用makepkg/pacman 的安装。

使用传统方式的一个优点是在其他发行版中也可以使用。

参见 [传统方式](/index.php/Kernels/Compilation/Traditional "Kernels/Compilation/Traditional") **.**

### NVIDIA 闭源驱动

参见 [定制内核](/index.php/NVIDIA#Alternate_install:_custom_kernel "NVIDIA") 查看详细关于在自定义内核中使用 Nvidia 闭源驱动的方法。

## 参见

*   [O'Reilly - Linux Kernel in a Nutshell](http://www.kroah.com/lkn/) （自由开源的电子书，包含内核配置、安装和其他的东西）