Related articles

*   [Kernel modules](/index.php/Kernel_modules "Kernel modules")
*   [Compile kernel module](/index.php/Compile_kernel_module "Compile kernel module")
*   [Kernel Panics](/index.php/Kernel_Panics "Kernel Panics")
*   [Linux-ck](/index.php/Linux-ck "Linux-ck")
*   [sysctl](/index.php/Sysctl "Sysctl")

According to [Wikipedia](https://en.wikipedia.org/wiki/Kernel_(computing) "wikipedia:Kernel (computing)"):

	The kernel is a computer program that constitutes the central core of a computer's operating system. It has complete control over everything that occurs in the system. As such, it is the first program loaded on startup, and then manages the remainder of the startup, as well as input/output requests from software, translating them into data processing instructions for the central processing unit. It is also responsible for managing memory, and for managing and communicating with computing peripherals, like printers, speakers, etc. The kernel is a fundamental part of a modern computer's operating system.

There are various alternative kernels available for Arch Linux in addition to the mainline Linux kernel. This article lists some of the options available in the repositories with a brief description of each. There is also a description of patches that can be applied to the system's kernel. The article ends with an overview of custom kernel compilation with links to various methods.

## Contents

*   [1 Precompiled kernels](#Precompiled_kernels)
    *   [1.1 Official packages](#Official_packages)
    *   [1.2 AUR packages](#AUR_packages)
*   [2 Patches and Patchsets](#Patches_and_Patchsets)
    *   [2.1 How to install](#How_to_install)
    *   [2.2 Major patchsets](#Major_patchsets)
        *   [2.2.1 -ck](#-ck)
        *   [2.2.2 -rt](#-rt)
        *   [2.2.3 -bld](#-bld)
        *   [2.2.4 Tiny-Patches](#Tiny-Patches)
        *   [2.2.5 -pf](#-pf)
    *   [2.3 Individual patches](#Individual_patches)
        *   [2.3.1 Reiser4](#Reiser4)
        *   [2.3.2 fbsplash](#fbsplash)
*   [3 Compilation](#Compilation)
    *   [3.1 Using the Arch Build System](#Using_the_Arch_Build_System)
    *   [3.2 Traditional](#Traditional)
*   [4 See also](#See_also)

## Precompiled kernels

### Official packages

	[linux](https://www.archlinux.org/packages/?name=linux)

	The Linux kernel and modules from the *core* repository. Vanilla kernel with [a few patches applied](https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/linux).

	[linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened)

	A security-focused Linux kernel applying a set of [hardening patches](https://github.com/thestinger/linux-hardened) to mitigate kernel and userspace exploits. It also enables more upstream kernel hardening features than [linux](https://www.archlinux.org/packages/?name=linux) along with user namespaces (with unprivileged usage disabled by default via a patch), audit and [SELinux](/index.php/SELinux "SELinux").

	[linux-lts](https://www.archlinux.org/packages/?name=linux-lts)

	Long term support (LTS) Linux kernel and modules from the *core* repository.

	[linux-zen](https://www.archlinux.org/packages/?name=linux-zen)

	The [ZEN Kernel](https://github.com/zen-kernel/zen-kernel) is the result of a collaborative effort of kernel hackers to provide the best Linux kernel possible for everyday systems.

### AUR packages

Note for [AUR](/index.php/AUR "AUR") packages, "pre-compiled" means the packages are (usually) maintained, tested and verified to be working. Some of the listed packages may also be available as binary packages via [Unofficial repositories](/index.php/Unofficial_repositories "Unofficial repositories").

	[linux-aufs_friendly](https://aur.archlinux.org/packages/linux-aufs_friendly/)

	The aufs-compatible linux kernel and modules, useful when using [docker](/index.php/Docker "Docker").

	[linux-ck](https://aur.archlinux.org/packages/linux-ck/)

	Linux Kernel built with Con Kolivas' ck1 patchset—see the [#-ck](#-ck) section or the [linux-ck](/index.php/Linux-ck "Linux-ck") page. Additional options which can be toggled on/off in the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") include: BFQ scheduler, nconfig, localmodconfig and use running kernel's config.

	[linux-fbcondecor](https://aur.archlinux.org/packages/linux-fbcondecor/)

	The Linux Kernel and modules with [fbcondecor support](/index.php/Fbsplash "Fbsplash").

	[linux-git](https://aur.archlinux.org/packages/linux-git/)

	Linux kernel and modules built using sources from [Linus Torvalds' Git repository](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git).

	[linux-ice](https://aur.archlinux.org/packages/linux-ice/)

	The Linux Kernel and modules with gentoo-sources patchset and [TuxOnIce](/index.php/TuxOnIce "TuxOnIce") support.

	[linux-libre](https://aur.archlinux.org/packages/linux-libre/), [linux-libre-lts](https://aur.archlinux.org/packages/linux-libre-lts/), [linux-libre-rt](https://aur.archlinux.org/packages/linux-libre-rt/), [linux-libre-xen](https://aur.archlinux.org/packages/linux-libre-xen/)

	The Linux Kernels without "binary blobs".

	[linux-lqx](https://aur.archlinux.org/packages/linux-lqx/)

	[Liquorix](http://liquorix.net) is a distro kernel replacement built using a Debian-targeted configuration and the ZEN kernel sources. Designed for desktop, multimedia, and gaming workloads, it is often used as a Debian Linux performance replacement kernel. Damentz, the maintainer of the Liquorix patchset, is a developer for the ZEN patchset as well.

	[linux-lts310](https://aur.archlinux.org/packages/linux-lts310/)

	The Linux 3.10 Long-Term Support Kernel and modules.

	[linux-mainline](https://aur.archlinux.org/packages/linux-mainline/)

	The Mainline Linux Kernel and modules.

	[linux-mptcp](https://aur.archlinux.org/packages/linux-mptcp/)

	The Linux Kernel and modules with [Multipath TCP](http://multipath-tcp.org/) support.

	[linux-pf](https://aur.archlinux.org/packages/linux-pf/)

	Linux kernel and modules with the pf-kernel patch [-ck patchset (BFS included), TuxOnIce, BFQ] and aufs3.

	[linux-rt](https://aur.archlinux.org/packages/linux-rt/)

	Linux kernel with the realtime patch set. Improves latency and introduces hard realtime support. [https://rt.wiki.kernel.org/](https://rt.wiki.kernel.org/)

	[linux-tresor](https://aur.archlinux.org/packages/linux-tresor/)/[linux-lts-tresor](https://aur.archlinux.org/packages/linux-lts-tresor/)

	The current/LTS Linux Kernel and modules with integrated [TRESOR](https://www1.informatik.uni-erlangen.de/tresor)

	[linux-vfio](https://aur.archlinux.org/packages/linux-vfio/)/[linux-vfio-lts](https://aur.archlinux.org/packages/linux-vfio-lts/)

	The Linux kernel and a few patches written by Alex Williamson (acs override and i915) to enable the ability to do PCI Passthrough with KVM on some machines.

	[linux-kpatch](https://aur.archlinux.org/packages/linux-kpatch/)

	The Linux kernel with [live patching](/index.php/Kernel_live_patching "Kernel live patching") support.

## Patches and Patchsets

There are lots of reasons to patch your kernel, the major ones are for performance or support for non-mainline features such as reiser4 file system support. Other reasons might include fun and to see how it is done and what the improvements are.

However, it is important to note that the best way to increase the speed of your system is to first tailor your kernel to your system, especially the architecture and processor type. For this reason using pre-packaged versions of custom kernels with generic architecture settings is not recommended or really worth it. A further benefit is that you can reduce the size of your kernel (and therefore build time) by not including support for things you do not have or use. For example, you might start with the stock kernel config when a new kernel version is released and remove support for things like bluetooth, video4linux, 1000Mbit ethernet, etc.; functionality you know you will not require for your specific machine. Although this page is not about customizing your kernel config, it is recommended as a first step--before moving on to using a patchset once you have grasped the fundamentals involved.

The config files for the Arch kernel packages can be used as a starting point. They are in the Arch package source files, for example [[1]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/linux) linked from [linux](https://www.archlinux.org/packages/?name=linux). The config file of your currently running kernel may also be available in your file system at `/proc/config.gz` if the `CONFIG_IKCONFIG_PROC` kernel option is enabled.

### How to install

The installation process of custom kernel packages relies on the Arch Build System (ABS). If you have not built any custom packages yet you may consult the following articles: [Arch Build System](/index.php/Arch_Build_System "Arch Build System") and [Creating packages](/index.php/Creating_packages "Creating packages").

If you have not actually patched or customized a kernel before it is not that hard and there are many PKGBUILDs on the forum for individual patchsets. However, you are advised to start from scratch with a bit of research on the benefits of each patchset, rather than just arbitrarily picking one. This way you will learn much more about what you are doing rather than just choosing a kernel at startup and then be left wondering what it actually does.

See [#Compilation](#Compilation).

**Note:** Do not forget to change the boot options in your bootloader, e.g. [GRUB](/index.php/GRUB "GRUB"), to use the new kernel.

### Major patchsets

First of all it is important to note that patchsets are developed by a variety of people. Some of these people are actually involved in the production of the linux kernel and others are hobbyists, which may reflect its level of reliability and stability.

It is also worth noting that some patchsets are built on the back of other patchsets (which may or may not be reflected in the title of the patch). Patchsets (and kernel updates) can be released **very** frequently and often it is not worth keeping up with ALL of them; so, do not go crazy, unless you make it your hobby!

You can search Google for more sets, but remember to use quotes (`"-nitro"`, for example); otherwise, Google will deliberately **NOT** show the results you want!

**Note:** This section is for **information only** - clearly no guarantees of stability or reliability are implied by inclusion on this page.

#### -ck

[Linux-ck](/index.php/Linux-ck "Linux-ck") contains patches designed to improve system responsiveness with specific emphasis on the desktop, but suitable to any workload. The patches are created and maintained by Con Kolivas, his site is at [http://users.tpg.com.au/ckolivas/kernel/](http://users.tpg.com.au/ckolivas/kernel/). Con maintains a full set but also provides the patches broken down so you can add only those you prefer.

The -ck patches can be found at [http://ck.kolivas.org/patches/](http://ck.kolivas.org/patches/)

#### -rt

This patchset is maintained by a small group of core developers, led by Ingo Molnar. This patch allows nearly all of the kernel to be preempted, with the exception of a few very small regions of code ("raw_spinlock critical regions"). This is done by replacing most kernel spinlocks with mutexes that support priority inheritance, as well as moving all interrupt and software interrupts to kernel threads.

It further incorporates high resolution timers - a patch set, which is independently maintained.

[as said from the [Real-Time Linux Wiki](https://rt.wiki.kernel.org/index.php/CONFIG_PREEMPT_RT_Patch)]

patch at [https://www.kernel.org/pub/linux/kernel/projects/rt/](https://www.kernel.org/pub/linux/kernel/projects/rt/)

#### -bld

**Warning:** This patch is in development.

BLD is best described as a O(1) CPU picking technique. Which is done by reordering CPU runqueues based on runqueue loads. In other words, it keeps the scheduler aware of the load changes, which helps scheduler to keep runqueues in an order. This technique does not depend on scheduler ticks. The two most simple things in this technique are: load tracking and runqueue ordering; these are relatively simpler operations. Load tracking will be done whenever a load change happens on the system and based on this load change runqueue will be ordered. So, if we have an ordered runqueue from lowest to highest, then picking the less (or even busiest) runqueue is easy. Scheduler can pick the lowest runqueue without calculation and comparison at the time of placing a task in a runqueue. And while trying to distribute load at sched_exec and sched_fork our best choice is to pick the lowest busiest runqueue of the system. And in this way, system remains balanced without doing any load balancing. At the time of try_to_wake_up picking the idlest runqueue is topmost priority but it has been done as per domain basis to utilize CPU cache properly and it's an area where more concentration is requires.

Google Code web page: [https://code.google.com/p/bld/](https://code.google.com/p/bld/) *(old)*

Github web page: [https://github.com/rmullick/bld-patches](https://github.com/rmullick/bld-patches)

#### Tiny-Patches

The goal of [Linux Tiny](http://elinux.org/Linux_Tiny) is to reduce its memory and disk footprint, as well as to add features to aid working on small systems. Target users are developers of embedded system and users of small or legacy machines such as 386s.

Patch releases against the mainstream Linux kernel have been discontinued. The developers chose to focus on a few patches and spend their time trying to get them merged into the mainline kernel.

#### -pf

[linux-pf](https://aur.archlinux.org/packages/linux-pf/) is yet another Linux kernel fork which provides you with a handful of awesome features not merged into mainline. It is based on neither existing Linux fork nor patchset, although some unofficial ports may be used if required patches have not been released officially. The most prominent patches of linux-pf are TuxOnIce, the CK patchset (most notably BFS), AUFS3, LinuxIMQ, l7 filter and BFQ.

See [linux-pf](/index.php/Linux-pf "Linux-pf") for more information.

### Individual patches

These are patches which can be simply included in any build of a vanilla kernel or incorporated (probably with some major tweaking) into another patchset.

#### Reiser4

[Reiser4](/index.php/Reiser4 "Reiser4")

#### fbsplash

[fbsplash](/index.php/Fbsplash "Fbsplash")

## Compilation

Arch Linux provides for several methods of kernel compilation.

### Using the Arch Build System

Using the [Arch Build System](/index.php/Arch_Build_System "Arch Build System") takes advantage of the high quality of the existing [linux](https://www.archlinux.org/packages/?name=linux) [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") and the benefits of [package management](https://en.wikipedia.org/wiki/Package_management_system "wikipedia:Package management system"). The PKGBUILD is structured so that you can stop the build after the source is downloaded and configure the kernel.

See [Kernels/Arch Build System](/index.php/Kernels/Arch_Build_System "Kernels/Arch Build System").

### Traditional

This involves manually downloading a source tarball, and compiling in your home directory as a normal user. Once configured, two installation methods are available; the traditional manual method, or with [Makepkg](/index.php/Makepkg "Makepkg") + [Pacman](/index.php/Pacman "Pacman").

See [Kernels/Traditional compilation](/index.php/Kernels/Traditional_compilation "Kernels/Traditional compilation").

## See also

*   [O'Reilly - Linux Kernel in a Nutshell](http://www.kroah.com/lkn/) (free ebook)