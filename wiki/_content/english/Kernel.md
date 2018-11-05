Related articles

*   [Kernel modules](/index.php/Kernel_modules "Kernel modules")
*   [Compile kernel module](/index.php/Compile_kernel_module "Compile kernel module")
*   [Kernel Panics](/index.php/Kernel_Panics "Kernel Panics")
*   [Linux-ck](/index.php/Linux-ck "Linux-ck")
*   [sysctl](/index.php/Sysctl "Sysctl")

According to [Wikipedia](https://en.wikipedia.org/wiki/Linux_kernel "wikipedia:Linux kernel"):

	The **Linux kernel** is an open-source monolithic Unix-like computer [operating system kernel](https://en.wikipedia.org/wiki/Kernel_(operating_system) "wikipedia:Kernel (operating system)").

[Arch Linux](/index.php/Arch_Linux "Arch Linux") is based on the Linux kernel. There are various alternative Linux kernels available for Arch Linux in addition to the stable [Linux kernel](https://en.wikipedia.org/wiki/Linux_kernel "wikipedia:Linux kernel"). This article lists some of the options available in the repositories with a brief description of each. There is also a description of patches that can be applied to the system's kernel. The article ends with an overview of custom kernel compilation with links to various methods.

## Contents

*   [1 Officially supported kernels](#Officially_supported_kernels)
*   [2 Compilation](#Compilation)
*   [3 Patches and patchsets](#Patches_and_patchsets)
    *   [3.1 Major patchsets](#Major_patchsets)
    *   [3.2 Other patchsets](#Other_patchsets)
*   [4 See also](#See_also)

## Officially supported kernels

*   **[Stable](https://www.kernel.org/category/releases.html)** — Vanilla Linux kernel and modules, with a few patches applied.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux](https://www.archlinux.org/packages/?name=linux)

*   **[Hardened](https://kernsec.org/wiki/index.php/Kernel_Self_Protection_Project)** — A security-focused Linux kernel applying a set of hardening patches to mitigate kernel and userspace exploits. It also enables more upstream kernel hardening features than [linux](https://www.archlinux.org/packages/?name=linux) along [AppArmor](/index.php/AppArmor "AppArmor") and [SELinux](/index.php/SELinux "SELinux").

	[https://github.com/anthraxx/linux-hardened](https://github.com/anthraxx/linux-hardened) || [linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened)

*   **[Longterm](https://www.kernel.org/category/releases.html)** — Long-term support (LTS) Linux kernel and modules.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts](https://www.archlinux.org/packages/?name=linux-lts)

*   **[ZEN Kernel](https://github.com/zen-kernel/zen-kernel)** — Result of a collaborative effort of kernel hackers to provide the best Linux kernel possible for everyday systems. Some more details can be found on [https://liquorix.net](https://liquorix.net) (which provides kernel binaries based on ZEN for Debian).

	[https://github.com/zen-kernel/zen-kernel](https://github.com/zen-kernel/zen-kernel) || [linux-zen](https://www.archlinux.org/packages/?name=linux-zen)

## Compilation

Arch Linux provides two methods of kernel compilation.

	[/Arch Build System](/index.php/Kernel/Arch_Build_System "Kernel/Arch Build System")

	Takes advantage of the high quality of existing [linux](https://www.archlinux.org/packages/?name=linux) [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") and the benefits of [package management](https://en.wikipedia.org/wiki/Package_management_system "wikipedia:Package management system").

	[/Traditional compilation](/index.php/Kernel/Traditional_compilation "Kernel/Traditional compilation")

	Involves manually downloading a source tarball, and compiling in your home directory as a normal user.

## Patches and patchsets

There are lots of reasons to patch your kernel, the major ones are for performance or support for non-mainline features such as [reiser4](/index.php/Reiser4 "Reiser4") file system support. Other reasons might include fun and to see how it is done and what the improvements are.

However, it is important to note that the best way to increase the speed of your system is to first tailor your kernel to your system, especially the architecture and processor type. For this reason using pre-packaged versions of custom kernels with generic architecture settings is not recommended or really worth it. A further benefit is that you can reduce the size of your kernel (and therefore build time) by not including support for things you do not have or use. For example, you might start with the stock kernel config when a new kernel version is released and remove support for things like bluetooth, video4linux, 1000Mbit ethernet, etc.; functionality you know you will not require for your specific machine. Although this page is not about customizing your kernel config, it is recommended as a first step--before moving on to using a patchset once you have grasped the fundamentals involved.

The config files for the Arch kernel packages can be used as a starting point. They are in the Arch package source files, for example [[1]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/linux) linked from [linux](https://www.archlinux.org/packages/?name=linux). The config file of your currently running kernel may also be available in your file system at `/proc/config.gz` if the `CONFIG_IKCONFIG_PROC` kernel option is enabled.

If you have not actually patched or customized a kernel before it is not that hard and there are many PKGBUILDs on the forum for individual patchsets. However, you are advised to start from scratch with a bit of research on the benefits of each patchset, rather than just arbitrarily picking one. This way you will learn much more about what you are doing rather than just choosing a kernel at startup and then be left wondering what it actually does.

**Warning:** Patchsets are developed by a variety of people. Some of these people are actually involved in the production of the linux kernel and others are hobbyists, which may reflect its level of reliability and stability.

### Major patchsets

*   **[Linux-ck](/index.php/Linux-ck "Linux-ck")** — Contains patches by Con Kolivas designed to improve system responsiveness with specific emphasis on the desktop, but suitable to any workload.

	[http://ck.kolivas.org/patches/](http://ck.kolivas.org/patches/) || [linux-ck](https://aur.archlinux.org/packages/linux-ck/)

*   **[Intel Clearlinux patches](https://github.com/clearlinux-pkgs/linux/)** — Maintained by Intel. The patches optimize kernel for performance and security, from the Cloud to the Edge, designed for customization, and manageability. It also provides [WireGuard](/index.php/WireGuard "WireGuard") as its module.

	[https://github.com/clearlinux-pkgs/linux](https://github.com/clearlinux-pkgs/linux) || [linux-clear](https://aur.archlinux.org/packages/linux-clear/)

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

## See also

*   [O'Reilly - Linux Kernel in a Nutshell](http://www.kroah.com/lkn/) (free ebook)
*   [What stable kernel should I use?](http://kroah.com/log/blog/2018/08/24/what-stable-kernel-should-i-use/) by Greg Kroah-Hartman