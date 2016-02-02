# Kernels

From [Wikipedia](https://en.wikipedia.org/wiki/Kernel_(computing) "wikipedia:Kernel (computing)"):

	_the kernel is the main component of most computer operating systems; it is a bridge between applications and the actual data processing done at the hardware level. The kernel's responsibilities include managing the system's resources (the communication between hardware and software components)._

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
        *   [2.2.4 -grsecurity](#-grsecurity)
        *   [2.2.5 Tiny-Patches](#Tiny-Patches)
        *   [2.2.6 -pf](#-pf)
    *   [2.3 Individual patches](#Individual_patches)
        *   [2.3.1 Reiser4](#Reiser4)
        *   [2.3.2 fbsplash](#fbsplash)
*   [3 Compilation](#Compilation)
    *   [3.1 Using the Arch Build System](#Using_the_Arch_Build_System)
    *   [3.2 Traditional](#Traditional)
    *   [3.3 Proprietary NVIDIA driver](#Proprietary_NVIDIA_driver)
*   [4 See also](#See_also)

## Precompiled kernels

### Official packages

	[linux](https://www.archlinux.org/packages/?name=linux)

	The Linux kernel and modules from the [core] repository. Vanilla kernel with [a few patches applied](https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/linux).

	[linux-lts](https://www.archlinux.org/packages/?name=linux-lts)

	Long term support (LTS) Linux kernel and modules from the [core] repository.

	[linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec)

	The Linux Kernel and modules with [Grsecurity Patchset](/index.php/Grsecurity_Patchset "Grsecurity Patchset") and PaX patches for increased security.

	[linux-zen](https://www.archlinux.org/packages/?name=linux-zen)

	The [ZEN Kernel](https://github.com/zen-kernel/zen-kernel) is the result of a collaborative effort of kernel hackers to provide the best Linux kernel possible for every day systems.

### AUR packages

	[linux-aufs_friendly](https://aur.archlinux.org/packages/linux-aufs_friendly/)<sup><small>AUR</small></sup>

	The aufs-compatible linux kernel and modules, useful when using [docker](/index.php/Docker "Docker").

	[linux-apparmor](https://aur.archlinux.org/packages/linux-apparmor/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/linux-apparmor)]</sup>

	Linux kernel with [AppArmor](/index.php/AppArmor "AppArmor") capabilities enabled.

	[linux-bfs](https://aur.archlinux.org/packages/linux-bfs/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/linux-bfs)]</sup>

	Linux kernel and modules with the [Brain Fuck Scheduler](https://en.wikipedia.org/wiki/Brain_Fuck_Scheduler "wikipedia:Brain Fuck Scheduler") (BFS) - created by Con Kolivas for desktop computers with fewer than 4096 cores, with BFQ I/O scheduler as optional.

	[linux-chromebook](https://aur.archlinux.org/packages/linux-chromebook/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/linux-chromebook)]</sup>

	The Linux kernel with patches added to support chromebook hardware.

	[linux-ck](https://aur.archlinux.org/packages/linux-ck/)<sup><small>AUR</small></sup>

	Linux Kernel built with Con Kolivas' ck1 patchset.

	Additional options which can be toggled on/off in the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") include: BFQ scheduler, nconfig, localmodconfig and use running kernel's config.

	These are patches designed to improve system responsiveness with specific emphasis on the desktop, but suitable to any workload. The ck patches include BFS.

	For further information and installation instructions, please read the [linux-ck](/index.php/Linux-ck "Linux-ck") main article.

	[linux-eee-ck](https://aur.archlinux.org/packages/linux-eee-ck/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/linux-eee-ck)]</sup>

	The Linux Kernel and modules for the Asus Eee PC 701, built with Con Kolivas' ck1 patchset.

	[linux-fbcondecor](https://aur.archlinux.org/packages/linux-fbcondecor/)<sup><small>AUR</small></sup>

	The Linux Kernel and modules with [fbcondecor support](/index.php/Fbsplash "Fbsplash").

	[linux-git](https://aur.archlinux.org/packages/linux-git/)<sup><small>AUR</small></sup>

	Linux kernel and modules built using sources from [Linus Torvalds' Git repository](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git).

	[linux-ice](https://aur.archlinux.org/packages/linux-ice/)<sup><small>AUR</small></sup>

	The Linux Kernel and modules with gentoo-sources patchset and [TuxOnIce](/index.php/TuxOnIce "TuxOnIce") support.

	[linux-libre](https://aur.archlinux.org/packages/linux-libre/)<sup><small>AUR</small></sup>, [linux-libre-lts](https://aur.archlinux.org/packages/linux-libre-lts/)<sup><small>AUR</small></sup>, [linux-libre-grsec](https://aur.archlinux.org/packages/linux-libre-grsec/)<sup><small>AUR</small></sup>, [linux-libre-rt](https://aur.archlinux.org/packages/linux-libre-rt/)<sup><small>AUR</small></sup>, [linux-libre-xen](https://aur.archlinux.org/packages/linux-libre-xen/)<sup><small>AUR</small></sup>

	The Linux Kernels without "binary blobs".

	[linux-lqx](https://aur.archlinux.org/packages/linux-lqx/)<sup><small>AUR</small></sup>

	[Liquorix](http://liquorix.net) is a distro kernel replacement built using a Debian-targeted configuration and the ZEN kernel sources. Designed for desktop, multimedia, and gaming workloads, it is often used as a Debian Linux performance replacement kernel. Damentz, the maintainer of the Liquorix patchset, is a developer for the ZEN patchset as well.

	[linux-lts34](https://aur.archlinux.org/packages/linux-lts34/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/linux-lts34)]</sup>

	The Linux 3.4 Long-Term Support Kernel and modules.

	[linux-lts310](https://aur.archlinux.org/packages/linux-lts310/)<sup><small>AUR</small></sup>

	The Linux 3.10 Long-Term Support Kernel and modules.

	[linux-lts312](https://aur.archlinux.org/packages/linux-lts312/)<sup><small>AUR</small></sup>

	The Linux 3.12 Long-Term Support Kernel and modules.

	[linux-mainline](https://aur.archlinux.org/packages/linux-mainline/)<sup><small>AUR</small></sup>

	The Mainline Linux Kernel and modules.

	[linux-mptcp](https://aur.archlinux.org/packages/linux-mptcp/)<sup><small>AUR</small></sup>

	The Linux Kernel and modules with [Multipath TCP](http://multipath-tcp.org/) support.

	[kernel-netbook](https://aur.archlinux.org/packages/kernel-netbook/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kernel-netbook)]</sup>

	Static kernel for netbooks with Intel Atom N270/N280/N450/N550 such as the Eee PC with the add-on of external firmware ([broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/)<sup><small>AUR</small></sup>) and patchset (BFS + TuxOnIce + BFQ optional) - Only Intel GPU

	[linux-pax](https://aur.archlinux.org/packages/linux-pax/)<sup><small>AUR</small></sup>

	The Linux Kernel and modules with [PaX](/index.php/PaX "PaX") patches for increased security.

	[linux-pf](https://aur.archlinux.org/packages/linux-pf/)<sup><small>AUR</small></sup>

	Linux kernel and modules with the pf-kernel patch [-ck patchset (BFS included), TuxOnIce, BFQ] and aufs3.

	[linux-tresor](https://aur.archlinux.org/packages/linux-tresor/)<sup><small>AUR</small></sup>/[linux-lts-tresor](https://aur.archlinux.org/packages/linux-lts-tresor/)<sup><small>AUR</small></sup>

	The current/LTS Linux Kernel and modules with integrated [TRESOR](https://www1.informatik.uni-erlangen.de/tresor)

	[linux-vfio](https://aur.archlinux.org/packages/linux-vfio/)<sup><small>AUR</small></sup>/[linux-vfio-lts](https://aur.archlinux.org/packages/linux-vfio-lts/)<sup><small>AUR</small></sup>

	The Linux kernel and a few patches written by Alex Williamson (acs override and i915) to enable the ability to do PCI Passthrough with KVM on some machines.

## Patches and Patchsets

There are lots of reasons to patch your kernel, the major ones are for performance or support for non-mainline features such as reiser4 file system support. Other reasons might include fun and to see how it is done and what the improvements are.

However, it is important to note that the best way to increase the speed of your system is to first tailor your kernel to your system, especially the architecture and processor type. For this reason using pre-packaged versions of custom kernels with generic architecture settings is not recommended or really worth it. A further benefit is that you can reduce the size of your kernel (and therefore build time) by not including support for things you do not have or use. For example, you might start with the stock kernel config when a new kernel version is released and remove support for things like bluetooth, video4linux, 1000Mbit ethernet, etc.; functionality you know you will not require for your specific machine. Although this page is not about customizing your kernel config, it is recommended as a first step--before moving on to using a patchset once you have grasped the fundamentals involved.

The config files for the Arch kernel packages can be used as a starting point. They are in the Arch package source files, for example [[1]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/linux) linked from [linux](https://www.archlinux.org/packages/?name=linux). The config file of your currently running kernel is also always available in your file system at `/proc/config.gz`.

### How to install

The installation process of custom kernel packages relies on the Arch Build System (ABS). If you have not built any custom packages yet you may consult the following articles: [Arch Build System](/index.php/Arch_Build_System "Arch Build System") and [Creating packages](/index.php/Creating_packages "Creating packages").

If you have not actually patched or customized a kernel before it is not that hard and there are many PKGBUILDs on the forum for individual patchsets. However, you are advised to start from scratch with a bit of research on the benefits of each patchset, rather than just arbitrarily picking one. This way you will learn much more about what you are doing rather than just choosing a kernel at startup and then be left wondering what it actually does.

See [#Compilation](#Compilation).

**Note:** Do not forget to change the boot options in your bootloader, e.g. [GRUB](/index.php/GRUB "GRUB"), to use the new kernel.

### Major patchsets

First of all it is important to note that patchsets are developed by a variety of people. Some of these people are actually involved in the production of the linux kernel and others are hobbyists, which may reflect its level of reliability and stability.

It is also worth noting that some patchsets are built on the back of other patchsets (which may or may not be reflected in the title of the patch). Patchsets (and kernel updates) can be released **very** frequently and often it is not worth keeping up with ALL of them so do not go crazy, unless you make it your hobby!

You can search google for more sets - remember to use quotes `"-nitro"` for example otherwise google will deliberately **NOT** show the results you want!

**Note:** This section is for **information only** - clearly no guarantees of stability or reliability are implied by inclusion on this page.

#### -ck

[Linux-ck](/index.php/Linux-ck "Linux-ck") contains patches designed to improve system responsiveness with specific emphasis on the desktop, but suitable to any workload. The patches are created and maintained by Con Kolivas, his site is at [http://users.on.net/~ckolivas/kernel/](http://users.on.net/~ckolivas/kernel/). Con maintains a full set but also provides the patches broken down so you can add only those you prefer.

The -ck patches can be found at [http://ck.kolivas.org/patches/4.0/](http://ck.kolivas.org/patches/4.0/)

#### -rt

This patchset is maintained by a small group of core developers, led by Ingo Molnar. This patch allows nearly all of the kernel to be preempted, with the exception of a few very small regions of code ("raw_spinlock critical regions"). This is done by replacing most kernel spinlocks with mutexes that support priority inheritance, as well as moving all interrupt and software interrupts to kernel threads.

It further incorporates high resolution timers - a patch set, which is independently maintained.

[as said from the [Real-Time Linux Wiki](https://rt.wiki.kernel.org/index.php/CONFIG_PREEMPT_RT_Patch)]

patch at [https://www.kernel.org/pub/linux/kernel/projects/rt/](https://www.kernel.org/pub/linux/kernel/projects/rt/)

#### -bld

**Warning:** This patch is in development.

BLD is best described as a O(1) CPU picking technique. Which is done by reordering CPU runqueues based on runqueue loads. In other words, it keeps the scheduler aware of the load changes, which helps scheduler to keep runqueues in an order. This technique does not depend on scheduler ticks. The two most simple things in this technique are: load tracking and runqueue ordering; these are relatively simpler operations. Load tracking will be done whenever a load change happens on the system and based on this load change runqueue will be ordered. So, if we have an ordered runqueue from lowest to highest, then picking the less (or even busiest) runqueue is easy. Scheduler can pick the lowest runqueue without calculation and comparison at the time of placing a task in a runqueue. And while trying to distribute load at sched_exec and sched_fork our best choice is to pick the lowest busiest runqueue of the system. And in this way, system remains balanced without doing any load balancing. At the time of try_to_wake_up picking the idlest runqueue is topmost priority but it has been done as per domain basis to utilize CPU cache properly and it's an area where more concentration is requires.

Google Code web page: [https://code.google.com/p/bld/](https://code.google.com/p/bld/)

#### -grsecurity

[Grsecurity](/index.php/Grsecurity "Grsecurity") is a security focused patchset. It adds numerous security related features such as Role-Based Access Control and utilizes features of the PaX project. It can be used on a desktop but a public server would receive the greatest benefit. Some applications are incompatible with the additional security measures implemented by this patchset. If this occurs, consider using a lower security level.

The -grsecurity patches can be found at [https://grsecurity.net](https://grsecurity.net)

#### Tiny-Patches

The goal of [Linux Tiny](http://elinux.org/Linux_Tiny) is to reduce its memory and disk footprint, as well as to add features to aid working on small systems. Target users are developers of embedded system and users of small or legacy machines such as 386s.

Patch releases against the mainstream Linux kernel have been discontinued. The developers chose to focus on a few patches and spend their time trying to get them merged into the mainline kernel.

#### -pf

[linux-pf](https://aur.archlinux.org/packages/linux-pf/)<sup><small>AUR</small></sup> is yet another Linux kernel fork which provides you with a handful of awesome features not merged into mainline. It is based on neither existing Linux fork nor patchset, although some unofficial ports may be used if required patches have not been released officially. The most prominent patches of linux-pf are TuxOnIce, the CK patchset (most notably BFS), AUFS3, LinuxIMQ, l7 filter and BFQ.

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

See [Kernels/Compilation/Traditional](/index.php/Kernels/Compilation/Traditional "Kernels/Compilation/Traditional").

### Proprietary NVIDIA driver

See [NVIDIA#Alternate install: custom kernel](/index.php/NVIDIA#Alternate_install:_custom_kernel "NVIDIA") for instructions on using the proprietary NVIDIA driver with a custom kernel.

## See also

*   [O'Reilly - Linux Kernel in a Nutshell](http://www.kroah.com/lkn/) (free ebook)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Kernels&oldid=410507](https://wiki.archlinux.org/index.php?title=Kernels&oldid=410507)"