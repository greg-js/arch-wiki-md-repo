相关文章

*   [Kernel modules (简体中文)](/index.php/Kernel_modules_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel modules (简体中文)")
*   [Compile kernel module](/index.php/Compile_kernel_module "Compile kernel module")
*   [Kernel Panics (简体中文)](/index.php/Kernel_Panics_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel Panics (简体中文)")
*   [Linux-ck (简体中文)](/index.php/Linux-ck_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Linux-ck (简体中文)")
*   [sysctl](/index.php/Sysctl "Sysctl")

**翻译状态：** 本文是英文页面 [Kernels](/index.php/Kernels "Kernels") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-11-02，点击[这里](https://wiki.archlinux.org/index.php?title=Kernels&diff=0&oldid=545349)可以查看翻译后英文页面的改动。

来自 [Wikipedia](https://en.wikipedia.org/wiki/Kernel_(computing) "wikipedia:Kernel (computing)"):

	*内核是计算机操作系统的核心组件，对系统有完全的控制。开机时最先启动，然后负责后续的启动工作。它负责处理其它软件的请求，讲这些请求转化为中央处理器的数据处理请求。内核还负责管理内存，管理系统和其它打印机、扬声器等外围设备的通讯，是操作系统最基础的部分。*

在Arch Linux中，除了官方内核之外，还有许多各种各样的内核可供选择。这篇文章列出了这些内核和它们的简短介绍。这里还列出了一些可用的内核补丁的介绍。在文章的最后介绍了自行编译内核的方法。

## Contents

*   [1 官方支持的内核](#官方支持的内核)
*   [2 编译](#编译)
    *   [2.1 使用 Arch 构建系统(ABS)(推荐)](#使用_Arch_构建系统(ABS)(推荐))
    *   [2.2 传统方式](#传统方式)
*   [3 Patches and patchsets](#Patches_and_patchsets)
    *   [3.1 Major patchsets](#Major_patchsets)
    *   [3.2 Other patchsets](#Other_patchsets)
*   [4 参见](#参见)

## 官方支持的内核

	[linux](https://www.archlinux.org/packages/?name=linux)

	位于 "core" 仓库中，包含了对应的 Linux 内核和内核模块。官方原版内核再加 [几个补丁](https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/linux).

	[linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened)

	更加注重安全的 Linux 内核，采用一系列 [加固补丁](https://github.com/thestinger/linux-hardened) 以减少内核和用户空间产生漏洞的风险。和 [linux](https://www.archlinux.org/packages/?name=linux) 相比，还启用了一些加固选项，比如用户命名空间(同时通过补丁禁用未授权用户的访问)、审计以及 [SELinux](/index.php/SELinux "SELinux")。

	[linux-lts](https://www.archlinux.org/packages/?name=linux-lts)

	长期支持版 (LTS) 位于[core]仓库中，包含了长期支持的 Linux 内核和内核模块。

	[linux-zen](https://www.archlinux.org/packages/?name=linux-zen)

	[ZEN Kernel](https://github.com/zen-kernel/zen-kernel) 是一些内核黑客合作的结果，提供了适合日常使用的优秀内核。

## 编译

Arch Linux 提供了多种内核构建方式。

### 使用 Arch 构建系统(ABS)(推荐)

推荐使用 [Arch 构建系统](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)")，这样可以充分利用已有的 [linux](https://www.archlinux.org/packages/?name=linux) [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 以及包管理系统。PKGBUILD 已经是结构化的，你可以在下载源代码之后配置内核。

参见 [编译内核/Arch 构建系统](/index.php/Kernels/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernels/Arch Build System (简体中文)").

### 传统方式

另外，也可以不使用 [Arch 构建系统](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)") 编译内核(传统方式)。这个方法需要手动下载内核源代码包，然后在自己的主目录里以普通用户的权限编译。一旦完成配置之后，有两种编译(安装)方式：传统的安装和适用makepkg/pacman 的安装。

使用传统方式的一个优点是在其他发行版中也可以使用。

参见 [传统方式](/index.php/Kernels/Compilation/Traditional "Kernels/Compilation/Traditional") **.**

## Patches and patchsets

There are lots of reasons to patch your kernel, the major ones are for performance or support for non-mainline features such as [reiser4](/index.php/Reiser4 "Reiser4") file system support. Other reasons might include fun and to see how it is done and what the improvements are.

However, it is important to note that the best way to increase the speed of your system is to first tailor your kernel to your system, especially the architecture and processor type. For this reason using pre-packaged versions of custom kernels with generic architecture settings is not recommended or really worth it. A further benefit is that you can reduce the size of your kernel (and therefore build time) by not including support for things you do not have or use. For example, you might start with the stock kernel config when a new kernel version is released and remove support for things like bluetooth, video4linux, 1000Mbit ethernet, etc.; functionality you know you will not require for your specific machine. Although this page is not about customizing your kernel config, it is recommended as a first step--before moving on to using a patchset once you have grasped the fundamentals involved.

The config files for the Arch kernel packages can be used as a starting point. They are in the Arch package source files, for example [[1]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/linux) linked from [linux](https://www.archlinux.org/packages/?name=linux). The config file of your currently running kernel may also be available in your file system at `/proc/config.gz` if the `CONFIG_IKCONFIG_PROC` kernel option is enabled.

If you have not actually patched or customized a kernel before it is not that hard and there are many PKGBUILDs on the forum for individual patchsets. However, you are advised to start from scratch with a bit of research on the benefits of each patchset, rather than just arbitrarily picking one. This way you will learn much more about what you are doing rather than just choosing a kernel at startup and then be left wondering what it actually does.

**Warning:** Patchsets are developed by a variety of people. Some of these people are actually involved in the production of the linux kernel and others are hobbyists, which may reflect its level of reliability and stability.

### Major patchsets

*   **[Linux-ck](/index.php/Linux-ck "Linux-ck")** — Contains patches by Con Kolivas designed to improve system responsiveness with specific emphasis on the desktop, but suitable to any workload.

	[http://ck.kolivas.org/patches/](http://ck.kolivas.org/patches/) || [linux-ck](https://aur.archlinux.org/packages/linux-ck/)

*   **[pf-kernel](https://gitlab.com/post-factum/pf-kernel/)** — Provides you with a handful of awesome features not merged into mainline. It is based on neither existing Linux fork nor patchset, although some unofficial ports may be used if required patches have not been released officially. The most prominent patches of linux-pf are PDS CPU scheduler and UKSM.

	[https://gitlab.com/post-factum/pf-kernel/wikis/README](https://gitlab.com/post-factum/pf-kernel/wikis/README) || Packages:

*   [Repository](/index.php/Unofficial_user_repositories#post-factum_kernels "Unofficial user repositories") by pf-kernel developer, [post-factum](https://aur.archlinux.org/account/post-factum)
*   [Repository](/index.php/Unofficial_user_repositories#home-thaodan "Unofficial user repositories"), [linux-pf](https://aur.archlinux.org/packages/linux-pf/), [linux-pf-preset-default](https://aur.archlinux.org/packages/linux-pf-preset-default/), [linux-pf-lts](https://aur.archlinux.org/packages/linux-pf-lts/) by pf-kernel fork developer, [Thaodan](https://aur.archlinux.org/account/Thaodan)

*   **[Realtime kernel](/index.php/Realtime_kernel "Realtime kernel")** — Maintained by a small group of core developers, led by Ingo Molnar. This patch allows nearly all of the kernel to be preempted, with the exception of a few very small regions of code ("raw_spinlock critical regions"). This is done by replacing most kernel spinlocks with mutexes that support priority inheritance, as well as moving all interrupt and software interrupts to kernel threads.

	[https://wiki.linuxfoundation.org/realtime/start](https://wiki.linuxfoundation.org/realtime/start) || [linux-rt](https://aur.archlinux.org/packages/linux-rt/), [linux-rt-lts](https://aur.archlinux.org/packages/linux-rt-lts/)

### Other patchsets

Some of the listed packages may also be available as binary packages via [Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories").

*   **AppArmor** — The [Mandatory Access Control](https://en.wikipedia.org/wiki/Mandatory_access_control "wikipedia:Mandatory access control") (MAC) system, implemented upon the [Linux Security Modules](https://en.wikipedia.org/wiki/Linux_Security_Modules "wikipedia:Linux Security Modules") (LSM). While [linux](https://www.archlinux.org/packages/?name=linux) supports apparmor this kernel has the required [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") enabled by default.

	[AppArmor](/index.php/AppArmor "AppArmor") || [linux-apparmor](https://aur.archlinux.org/packages/linux-apparmor/)

*   **Aufs** — The aufs-compatible linux kernel and modules, useful when using [docker](/index.php/Docker "Docker").

	[http://aufs.sourceforge.net/](http://aufs.sourceforge.net/) || [linux-aufs_friendly](https://aur.archlinux.org/packages/linux-aufs_friendly/)

*   **BLD** — Best described as a O(1) CPU picking technique. Which is done by reordering CPU runqueues based on runqueue loads. In other words, it keeps the scheduler aware of the load changes, which helps scheduler to keep runqueues in an order. This technique does not depend on scheduler ticks. The two most simple things in this technique are: load tracking and runqueue ordering; these are relatively simpler operations. Load tracking will be done whenever a load change happens on the system and based on this load change runqueue will be ordered. So, if we have an ordered runqueue from lowest to highest, then picking the less (or even busiest) runqueue is easy. Scheduler can pick the lowest runqueue without calculation and comparison at the time of placing a task in a runqueue. And while trying to distribute load at sched_exec and sched_fork our best choice is to pick the lowest busiest runqueue of the system. And in this way, system remains balanced without doing any load balancing. At the time of try_to_wake_up picking the idlest runqueue is topmost priority but it has been done as per domain basis to utilize CPU cache properly and it's an area where more concentration is requires.

	[https://github.com/rmullick/bld-patches](https://github.com/rmullick/bld-patches) || [linux-bld](https://aur.archlinux.org/packages/linux-bld/)

*   **Git** — Linux kernel and modules built using sources from Linus Torvalds' Git repository

	[https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git) || [linux-git](https://aur.archlinux.org/packages/linux-git/)

*   **Libre** — The Linux Kernels without "binary blobs".

	[https://www.fsfla.org/ikiwiki/selibre/linux-libre/](https://www.fsfla.org/ikiwiki/selibre/linux-libre/) || [linux-libre](https://aur.archlinux.org/packages/linux-libre/)

*   **Liquorix** — Kernel replacement built using Debian-targeted configuration and the ZEN kernel sources. Designed for desktop, multimedia, and gaming workloads, it is often used as a Debian Linux performance replacement kernel. Damentz, the maintainer of the Liquorix patchset, is a developer for the ZEN patchset as well.

	[https://liquorix.net](https://liquorix.net) || [linux-lqx](https://aur.archlinux.org/packages/linux-lqx/)

*   **Longterm 4.4** — Long-term support (LTS) Linux 4.4 kernel and modules.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts44](https://aur.archlinux.org/packages/linux-lts44/)

*   **Mainline** — The Mainline Linux Kernel and modules.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/)

*   **MultiPath TCP** — The Linux Kernel and modules with Multipath TCP support.

	[https://multipath-tcp.org/](https://multipath-tcp.org/) || [linux-mptcp](https://aur.archlinux.org/packages/linux-mptcp/)

*   **[Reiser4](/index.php/Reiser4 "Reiser4")** — Successor filesystem for ReiserFS, developed from scratch by Namesys and Hans Reiser.

	[https://sourceforge.net/projects/reiser4/files/](https://sourceforge.net/projects/reiser4/files/) ||

*   **VFIO** — The Linux kernel and a few patches written by Alex Williamson (acs override and i915) to enable the ability to do PCI Passthrough with KVM on some machines.

	[https://lwn.net/Articles/499240/](https://lwn.net/Articles/499240/) || [linux-vfio](https://aur.archlinux.org/packages/linux-vfio/), [linux-vfio-lts](https://aur.archlinux.org/packages/linux-vfio-lts/)

## 参见

*   [O'Reilly - Linux Kernel in a Nutshell](http://www.kroah.com/lkn/) （自由开源的电子书，包含内核配置、安装和其他的东西）