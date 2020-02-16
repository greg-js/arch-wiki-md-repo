Related articles

*   [Kernel modules](/index.php/Kernel_modules "Kernel modules")
*   [Compile kernel module](/index.php/Compile_kernel_module "Compile kernel module")
*   [Kernel Panics](/index.php/Kernel_Panics "Kernel Panics")
*   [sysctl](/index.php/Sysctl "Sysctl")

According to Wikipedia:

	The [Linux kernel](https://en.wikipedia.org/wiki/Linux_kernel "wikipedia:Linux kernel") is an open-source monolithic Unix-like computer [operating system kernel](https://en.wikipedia.org/wiki/Kernel_(operating_system) "wikipedia:Kernel (operating system)").

[Arch Linux](/index.php/Arch_Linux "Arch Linux") is based on the Linux kernel. There are various alternative Linux kernels available for Arch Linux in addition to the latest stable kernel. This article lists some of the options available in the repositories with a brief description of each. There is also a description of patches that can be applied to the system's kernel. The article ends with an overview of custom kernel compilation with links to various methods.

Kernel packages are [installed](/index.php/Install "Install") onto the file system under `/boot/`. To be able to boot into kernels, the [boot loader](/index.php/Boot_loader "Boot loader") has to be configured appropriately.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Officially supported kernels](#Officially_supported_kernels)
*   [2 Compilation](#Compilation)
*   [3 kernel.org kernels](#kernel.org_kernels)
*   [4 Patches and patchsets](#Patches_and_patchsets)
    *   [4.1 Major patchsets](#Major_patchsets)
    *   [4.2 Other patchsets](#Other_patchsets)
*   [5 See also](#See_also)

## Officially supported kernels

*   **Stable** — Vanilla Linux kernel and modules, with a few patches applied.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux](https://www.archlinux.org/packages/?name=linux)

*   **Hardened** — A security-focused Linux kernel applying a set of hardening patches to mitigate kernel and userspace exploits. It also enables more upstream kernel hardening features than [linux](https://www.archlinux.org/packages/?name=linux).

	[https://github.com/anthraxx/linux-hardened](https://github.com/anthraxx/linux-hardened) || [linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened)

*   **Longterm** — Long-term support (LTS) Linux kernel and modules.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts](https://www.archlinux.org/packages/?name=linux-lts)

*   **Zen Kernel** — Result of a collaborative effort of kernel hackers to provide the best Linux kernel possible for everyday systems. Some more details can be found on [https://liquorix.net](https://liquorix.net) (which provides kernel binaries based on Zen for Debian).

	[https://github.com/zen-kernel/zen-kernel](https://github.com/zen-kernel/zen-kernel) || [linux-zen](https://www.archlinux.org/packages/?name=linux-zen)

## Compilation

Arch Linux provides two methods to compile your own kernel.

	[/Arch Build System](/index.php/Kernel/Arch_Build_System "Kernel/Arch Build System")

	Takes advantage of the high quality of existing [linux](https://www.archlinux.org/packages/?name=linux) [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") and the benefits of [package management](https://en.wikipedia.org/wiki/Package_management_system "wikipedia:Package management system").

	[/Traditional compilation](/index.php/Kernel/Traditional_compilation "Kernel/Traditional compilation")

	Involves manually downloading a source tarball, and compiling in your home directory as a normal user.

## kernel.org kernels

*   **Git** — Linux kernel and modules built using sources from Linus Torvalds' Git repository

	[https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git) || [linux-git](https://aur.archlinux.org/packages/linux-git/)

*   **Mainline** — Kernels where all new features are introduced, released every 2-3 months.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/)

*   **Next** — Bleeding edge kernels with features pending to be merged into next mainline release.

	[https://www.kernel.org/doc/man-pages/linux-next.html](https://www.kernel.org/doc/man-pages/linux-next.html) || [linux-next-git](https://aur.archlinux.org/packages/linux-next-git/)

*   **Longterm 3.16** — Long-term support (LTS) Linux 3.16 kernel and modules.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts316](https://aur.archlinux.org/packages/linux-lts316/)

*   **Longterm 4.4** — Long-term support (LTS) Linux 4.4 kernel and modules.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts44](https://aur.archlinux.org/packages/linux-lts44/)

*   **Longterm 4.9** — Long-term support (LTS) Linux 4.9 kernel and modules.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts49](https://aur.archlinux.org/packages/linux-lts49/)

*   **Longterm 4.14** — Long-term support (LTS) Linux 4.14 kernel and modules.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts414](https://aur.archlinux.org/packages/linux-lts414/)

*   **Longterm 4.19** — Long-term support (LTS) Linux 4.19 kernel and modules.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts419](https://aur.archlinux.org/packages/linux-lts419/)

## Patches and patchsets

There are lots of reasons to patch your kernel, the major ones are for performance or support for non-mainline features. Other reasons might include fun and to see how it is done and what the improvements are.

However, it is important to note that the best way to increase the speed of your system is to first tailor your kernel to your system, especially the architecture and processor type. For this reason using pre-packaged versions of custom kernels with generic architecture settings is not recommended or really worth it. A further benefit is that you can reduce the size of your kernel (and therefore build time) by not including support for things you do not have or use. For example, you might start with the stock kernel config when a new kernel version is released and remove support for things like bluetooth, video4linux, 1000Mbit ethernet, etc.; functionality you know you will not require for your specific machine. Although this page is not about customizing your kernel config, it is recommended as a first step--before moving on to using a patchset once you have grasped the fundamentals involved.

The config files for the Arch kernel packages can be used as a starting point. They are in the Arch package source files, for example [[1]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/linux) linked from [linux](https://www.archlinux.org/packages/?name=linux). The config file of your currently running kernel may also be available in your file system at `/proc/config.gz` if the `CONFIG_IKCONFIG_PROC` kernel option is enabled.

If you have not actually patched or customized a kernel before it is not that hard and there are many PKGBUILDs on the forum for individual patchsets. However, you are advised to start from scratch with a bit of research on the benefits of each patchset, rather than just arbitrarily picking one. This way you will learn much more about what you are doing rather than just choosing a kernel at startup and then be left wondering what it actually does.

**Warning:** Patchsets are developed by a variety of people. Some of these people are actually involved in the production of the linux kernel and others are hobbyists, which may reflect its level of reliability and stability.

### Major patchsets

*   **[Linux-ck](/index.php/Linux-ck "Linux-ck")** — Contains patches by Con Kolivas designed to improve system responsiveness with specific emphasis on the desktop, but suitable to any workload.

	[http://ck.kolivas.org/](http://ck.kolivas.org/) || [linux-ck](https://aur.archlinux.org/packages/linux-ck/)

*   **pf-kernel** — Provides you with a handful of awesome features not merged into mainline. It is based on neither existing Linux fork nor patchset, although some unofficial ports may be used if required patches have not been released officially. The most prominent patches of linux-pf are PDS CPU scheduler and UKSM.

	[https://gitlab.com/post-factum/pf-kernel/wikis/README](https://gitlab.com/post-factum/pf-kernel/wikis/README) || Packages:

*   [Repository](/index.php/Unofficial_user_repositories#post-factum_kernels "Unofficial user repositories") by pf-kernel developer, [post-factum](https://aur.archlinux.org/account/post-factum)
*   [Repository](/index.php/Unofficial_user_repositories#home-thaodan "Unofficial user repositories"), [linux-pf](https://aur.archlinux.org/packages/linux-pf/), [linux-pf-preset-default](https://aur.archlinux.org/packages/linux-pf-preset-default/), [linux-pf-lts](https://aur.archlinux.org/packages/linux-pf-lts/) by pf-kernel fork developer, [Thaodan](https://aur.archlinux.org/account/Thaodan)

*   **[Realtime kernel](/index.php/Realtime_kernel "Realtime kernel")** — Maintained by a small group of core developers, led by Ingo Molnar. This patch allows nearly all of the kernel to be preempted, with the exception of a few very small regions of code ("raw_spinlock critical regions"). This is done by replacing most kernel spinlocks with mutexes that support priority inheritance, as well as moving all interrupt and software interrupts to kernel threads.

	[https://wiki.linuxfoundation.org/realtime/start](https://wiki.linuxfoundation.org/realtime/start) || [linux-rt](https://aur.archlinux.org/packages/linux-rt/), [linux-rt-lts](https://aur.archlinux.org/packages/linux-rt-lts/)

### Other patchsets

Some of the listed packages may also be available as binary packages via [Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories").

*   **Aufs** — The aufs-compatible linux kernel and modules, useful when using [docker](/index.php/Docker "Docker").

	[http://aufs.sourceforge.net/](http://aufs.sourceforge.net/) || [linux-aufs](https://aur.archlinux.org/packages/linux-aufs/)

*   **Clear** — Patches from Intel's Clear Linux project. Provides performance and security optimizations; [WireGuard](/index.php/WireGuard "WireGuard") module.

	[https://github.com/clearlinux-pkgs/linux](https://github.com/clearlinux-pkgs/linux) || [linux-clear](https://aur.archlinux.org/packages/linux-clear/)

*   **GalliumOS** — The Linux kernel and modules with GalliumOS patches for chromebooks.

	[https://github.com/GalliumOS/linux](https://github.com/GalliumOS/linux) || [linux-galliumos](https://aur.archlinux.org/packages/linux-galliumos/)

*   **Libre** — The Linux Kernels without "binary blobs".

	[https://www.fsfla.org/ikiwiki/selibre/linux-libre/](https://www.fsfla.org/ikiwiki/selibre/linux-libre/) || [linux-libre](https://aur.archlinux.org/packages/linux-libre/)

*   **Liquorix** — Kernel replacement built using Debian-targeted configuration and the Zen kernel sources. Designed for desktop, multimedia, and gaming workloads, it is often used as a Debian Linux performance replacement kernel. Damentz, the maintainer of the Liquorix patchset, is a developer for the Zen patchset as well.

	[https://liquorix.net](https://liquorix.net) || [linux-lqx](https://aur.archlinux.org/packages/linux-lqx/)

*   **MultiPath TCP** — The Linux Kernel and modules with Multipath TCP support.

	[https://multipath-tcp.org/](https://multipath-tcp.org/) || [linux-mptcp](https://aur.archlinux.org/packages/linux-mptcp/)

*   **VFIO** — The Linux kernel and a few patches written by Alex Williamson (acs override and i915) to enable the ability to do PCI Passthrough with KVM on some machines.

	[https://lwn.net/Articles/499240/](https://lwn.net/Articles/499240/) || [linux-vfio](https://aur.archlinux.org/packages/linux-vfio/), [linux-vfio-lts](https://aur.archlinux.org/packages/linux-vfio-lts/)

*   **XanMod** — Aiming to take full advantage in high-performance workstations, gaming desktops, media centers and others and built to provide a more rock-solid, responsive and smooth desktop experience. This kernel uses the BFS scheduler, BFQ I/O scheduler, UKSM realtime memory data deduplication, YeAH TCP congestion control, x86_64 advanced instruction set support, and other default changes.

	[https://xanmod.org/](https://xanmod.org/) || [linux-xanmod](https://aur.archlinux.org/packages/linux-xanmod/)

## See also

*   [O'Reilly - Linux Kernel in a Nutshell](http://www.kroah.com/lkn/) (free ebook)
*   [What stable kernel should I use?](http://kroah.com/log/blog/2018/08/24/what-stable-kernel-should-i-use/) by Greg Kroah-Hartman