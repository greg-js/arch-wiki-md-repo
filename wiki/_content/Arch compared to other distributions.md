# Arch compared to other distributions

Related articles

*   [Arch Linux](/index.php/Arch_Linux "Arch Linux")
*   [The Arch Way](/index.php/The_Arch_Way "The Arch Way")
*   [Arch based distributions (active)](/index.php/Arch_based_distributions_(active) "Arch based distributions (active)")

This page attempts to draw a comparison between Arch Linux and other popular GNU/Linux distributions and UNIX-like operating systems. The summaries that follow are brief descriptions that may help a person decide if Arch Linux will suit his or her needs. Although reviews and descriptions can be useful, first-hand experience is invariably the best way to compare distributions.

## Contents

*   [1 Source-based](#Source-based)
    *   [1.1 CRUX](#CRUX)
    *   [1.2 LFS](#LFS)
    *   [1.3 Gentoo/Funtoo Linux](#Gentoo.2FFuntoo_Linux)
    *   [1.4 Sorcerer/Lunar-Linux/Source Mage](#Sorcerer.2FLunar-Linux.2FSource_Mage)
*   [2 General](#General)
    *   [2.1 Debian GNU/Linux](#Debian_GNU.2FLinux)
    *   [2.2 Fedora](#Fedora)
    *   [2.3 Slackware](#Slackware)
    *   [2.4 Frugalware](#Frugalware)
*   [3 Beginner-friendly](#Beginner-friendly)
    *   [3.1 Ubuntu](#Ubuntu)
    *   [3.2 Linux Mint](#Linux_Mint)
    *   [3.3 openSUSE](#openSUSE)
    *   [3.4 Mandriva/Mageia](#Mandriva.2FMageia)
    *   [3.5 PCLinuxOS](#PCLinuxOS)
*   [4 The *BSDs](#The_.2ABSDs)
    *   [4.1 FreeBSD](#FreeBSD)
    *   [4.2 NetBSD](#NetBSD)
    *   [4.3 OpenBSD](#OpenBSD)
    *   [4.4 OS X](#OS_X)
*   [5 See also](#See_also)

## Source-based

Source-based distributions are highly portable, giving the advantage of controlling and compiling the entire OS and applications for a particular machine architecture and usage scheme, with the disadvantage of the time-consuming nature of source compilation. The Arch base and all packages are compiled for i686 and x86_64 architectures, offering a potential performance boost over i486/i586 binary distributions, with the added advantage of expedient installation.

### CRUX

*   Before creating Arch, Judd Vinet admired and used CRUX; a minimalist distribution created by Per Lidén. Originally inspired by ideas in common with CRUX and BSD, Arch was built from scratch, and [pacman](/index.php/Pacman "Pacman") was then coded in C.
*   Arch and CRUX share some guiding principles: for instance, both are architecture-optimized, minimalist and K.I.S.S.-oriented.
*   Both ship with ports-like systems, and, like *BSD, both provide a minimal base environment to build upon.
*   Arch features pacman, which handles binary system package management and works seamlessly with the [Arch Build System](/index.php/Arch_Build_System "Arch Build System"). CRUX uses a community contributed system called prt-get, which, in combination with its own ports system, handles dependency resolution, but builds all packages from source (though the CRUX base installation is binary).
*   Arch officially supports x86_64 and i686 only, whereas CRUX officially offers only x86_64.
*   Arch uses a rolling-release system and features a large array of binary package repositories as well as the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). CRUX provides a more slimmed-down officially supported ports system in addition to a comparatively modest community repository.

### LFS

*   LFS, (or Linux From Scratch) exists simply as documentation. The book instructs the user on obtaining the source code for a minimal base package set for a functional GNU/Linux system, and how to manually compile, patch and configure it from scratch. LFS is as minimal as it gets, and offers an excellent and educational process of building and customizing a base system.
*   LFS provides no online repositories; sources are manually obtained, compiled and installed with _make_. (Several manual methods of package management exist, and are mentioned in LFS Hints).
*   Arch provides these very same packages, plus [systemd](/index.php/Systemd "Systemd"), a few extra tools and the powerful [pacman](/index.php/Pacman "Pacman") package manager as its base system, already compiled for i686/x86_64\. Along with the minimal Arch base system, the Arch community and developers provide and maintain many thousands of binary packages installable via pacman as well as [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") build scripts for use with the [Arch Build System](/index.php/Arch_Build_System "Arch Build System"). Arch also includes the [makepkg](/index.php/Makepkg "Makepkg") tool for expediently building or customizing _.pkg.tar.xz_ packages, readily installable by pacman.
*   Judd Vinet built Arch from scratch, and then wrote pacman in C. Historically, Arch was sometimes humorously described simply as "Linux, with a nice package manager."

### Gentoo/Funtoo Linux

*   Both Arch Linux and Gentoo Linux are rolling release systems, making packages available to the distribution a short time after they are released upstream.
*   The Gentoo packages and base system are built directly from source code according to user-specified _USE flags_. Arch provides a ports-like system for building packages from source, though the Arch base system is designed to be installed as pre-built i686/x86_64 binary. This generally makes Arch quicker to build and update, and allows Gentoo to be more systemically customizable.
*   Arch supports i686 and x86_64 while Gentoo officially supports x86 (i486/i686), x86_64, PPC/PPC64, SPARC, Alpha, ARM, MIPS, HPPA, S/390 and Itanium architectures.
*   Gentoo's official package and system management tools tend to be rather more complex and "powerful" than those provided by Arch, and certain features which are at the very heart of Gentoo _([USE flags](http://www.gentoo.org/doc/en/handbook/handbook-x86.xml?part=2&chap=2), [SLOTs](http://www.gentoo.org/doc/en/handbook/handbook-x86.xml?part=2&chap=1#doc_chap5), etc.)_ do not have any direct Arch Linux equivalent. Some of that is due to the fact that Arch is primarily a binary distro, but differences in [design philosophy](/index.php/The_Arch_Way "The Arch Way") also play a big role, with Arch taking a more principled stance in favor of architectural simplicity and avoiding over-engineering.
*   Because both the Gentoo and Arch installations only include a base system, both are considered to be highly customizable. Gentoo users will generally feel quite comfortable with most aspects of Arch.

### Sorcerer/Lunar-Linux/Source Mage

*   Sorcerer/Lunar-Linux/Source Mage (SLS) are all source-based distributions originally related to one another.
*   SLS distributions use a rather simple set of script files to create package descriptions, and use a global configuration file to configure the compilation process, much like the [Arch Build System](/index.php/Arch_Build_System "Arch Build System"). The SLS tools do full dependency checking, including handling optional features, package tracking, removal and upgrading. There are no binary packages for any of the SLS family, although they all provide the ability to roll back to earlier installed packages easily.
*   The installation process involves configuring a simple base system from the shell and ncurses menus, then optionally recompiling the base system afterward.
*   Like Arch, there is no default WM/DE/DM, and Xorg is not included in the base installation. Several X server alternatives are available (X.Org 6.8 or 7, XFree86).

## General

These distributions offer a broad range of advantages and strengths, and can be made to serve most operating system uses.

### Debian GNU/Linux

*   Debian is the largest upstream Linux distribution with a bigger community and features stable, testing, and unstable branches, offering over 30,000 high quality binary packages. The available number of Arch binary packages is more modest. However, when including the AUR, the quantities are very comparable.

*   Debian has a more vehement stance on free software but still includes non-free software in its non-free repos. Arch is more lenient, and therefore inclusive, concerning _non-free packages_ as defined by GNU, thereby leaving the choice to the users.

*   Debian's design approach focuses more on stability and stringent testing and focus based mostly on its famous "Debian social contract". Arch is focused more on the philosophy of simplicity, minimalism, and offering bleeding edge software. Arch packages are more current than Debian Stable and Testing, being more comparable to the Debian Unstable branch.

*   Both Debian and Arch offer well-regarded package management systems.

*   Arch is a rolling release, whereas Debian Stable is released with "frozen" packages. Debian unstable is rolling.

*   Debian is available for many architectures, including alpha, arm, hppa, i386, x86_64, ia64, m68k, mips, mipsel, powerpc, s390, and sparc, whereas Arch is officially i686 and x86_64, with community ports for arm (for Raspberry Pi for example) only.

*   Arch provides more expedient support for building custom, installable packages from outside sources, with a ports-like package build system. Debian does not offer a ports system, relying instead on its huge binary repositories.

*   The Arch installation system only offers a minimal base, transparently exposed during system configuration, whereas Debian's methods, such as the use of apt _tasks_ to install pre-selected groups of packages, offer a more automatically configured approach as well as several alternative methods of installation.

*   Arch generally packages software libraries together with their header files, whereas in Debian header files have to be downloaded separately.

*   Arch keeps patching to a minimum, thus avoiding problems that upstream are unable to review, whereas Debian patches its packages more liberally for a wider audience.

### Fedora

*   Fedora is community developed, yet corporately backed by Red Hat; it is often presented as a bleeding edge testbed release system; Fedora packages and projects migrate to RHEL and some eventually become adopted by other distributions. Arch too is generally considered bleeding edge, although it is a rolling-release and does not serve as a testing branch for another distribution.

*   Fedora packages are RPM format, using the DNF package manager, and official graphical package tools are also available. Arch uses [pacman](/index.php/Pacman "Pacman") to manage tar.xz packages and does not officially support a graphical frontend.

*   Fedora refuses to include MP3 media support and other non-free software in official repositories due to its dedication to free software, though third-party repositories are available for such packages. Arch is more lenient in its disposition toward MP3 and non-free software, leaving the discernment to the user.

*   Fedora offers many installation options including a graphical installer as well as a minimal option. Fedora "spins" also provide alternative assortments of desktop environments to choose from, each with a modest assortment of default packages. Arch, on the other hand, only provides a few scripts meant to ease the process of a minimal base system install.

*   Fedora has a scheduled release cycle, but officially supports discrete version upgrades with the FedUp tool. Arch is a rolling-release system.

*   **The Arch Way** focuses on simplicity, lightweight elegance and empowering the user, whereas **Fedora Core Values** focus on free software, community development and bleeding edge systemic innovation.

*   Arch features a ports system, whereas Fedora does not.

*   **Both Arch and Fedora are targeted at experienced users and developers.** Both strongly encourage their users to contribute to project development.

*   Fedora has earned much community recognition for integration of SELinux, GCJ compiled packages (to remove the need for Oracle's JRE), and prolific upstream contribution; Red Hat and thus, Fedora developers by extension, contribute the highest percentage of Linux kernel code as compared to any other project.

*   Arch Linux provides what is widely regarded as the most thorough and comprehensive distribution wiki. The Fedora wiki is used in the original sense of the word "wiki", or a way to exchange information between developers, testers and users rapidly. It is not meant to be an end-user knowledge base like Arch's. Fedora's wiki resembles an issue tracker or a corporate wiki.

### Slackware

*   Slackware and Arch are quite similar in that both are simple distributions focused on elegance and minimalism.

*   Slackware is famous for its lack of branding and completely vanilla packages, from the kernel up. Arch typically applies patching only to avoid severe breakage or to ensure packages will compile cleanly.

*   Slackware uses BSD-style init scripts, Arch uses [systemd](/index.php/Systemd "Systemd").

*   Arch supplies a package management system in [pacman](/index.php/Pacman "Pacman") which, unlike Slackware's standard tools, offers automatic dependency resolution and allows for more automated system upgrades. Slackware users typically prefer their method of manual dependency resolution, citing the level of system control it grants them, as well as Slackware's excellent supply of pre-installed libraries and dependencies.

*   Arch is a rolling-release system. Slackware is seen as more conservative in its release cycle, preferring proven stable packages. Arch is more _bleeding-edge_ in this respect.

*   Arch Linux provides many thousands of binary packages within its official repositories whereas Slackware official repositories are more modest.

*   Arch offers the [Arch Build System](/index.php/Arch_Build_System "Arch Build System"), an actual ports-like system and also the [AUR](/index.php/AUR "AUR"), a very large collection of PKGBUILDs contributed by users. Slackware offers a similar, though slimmer system at [slackbuilds.org](http://www.slackbuilds.org) which is a semi-official repository of Slackbuilds, which are analogous to Arch PKGBUILDs. Slackware users will generally be quite comfortable with most aspects of Arch.

### Frugalware

*   Arch is command-line oriented.

*   Frugalware does not support the JFS filesystem by default.

*   Both Arch and Frugalware are promoted as i686 optimized.

*   Both Arch and Frugalware could be installed as a minimal environment first and later expanded with pacman according to the user's choices and needs.

*   Frugalware also could be installed from a DVD, with default software choices and desktop environment chosen for the user already.

*   Frugalware has a scheduled release cycle. Again, Arch is more focused on simplicity, minimalism, code-correctness and bleeding edge packages within a rolling-release model.

## Beginner-friendly

Sometimes called "newbie distros", the beginner-friendly distributions share a lot of similarities, though Arch is quite different from them. Arch may be a better choice if you want to learn about GNU/Linux by building up from a very minimal base, as an installation of Arch installs very few packages in comparison. Specific differences between distributions are described below.

### Ubuntu

*   Ubuntu is a popular Debian-based distribution commercially sponsored by Canonical Ltd., while Arch is an independently developed system built from scratch.

*   The two projects have very different goals and are targeted at a different user base. Arch is designed for users who desire a do-it-yourself approach, whereas Ubuntu provides a preconfigured system. Arch presents a more minimalist design from the base installation onward, relying heavily on the user to customize it to their own specific needs. Many Arch users have started on Ubuntu and eventually migrated to Arch.

*   Arch development is not biased towards any one particular user interface beyond what its community provide support for. Furthermore, Canonical's commercial nature has led them to some controversial decisions, such as the inclusion of advertisements in Unity's _Dash_ menu and user data collection. Arch is an independent, community-driven project with no commercial agenda and features no bloatware in its distribution.

*   Ubuntu moves between discrete releases every 6 months, whereas Arch is a rolling-release system with a new snapshot issued every month.

*   Arch offers a ports-like package build system, while Ubuntu does not.

*   The two communities differ in some ways as well. The Arch community is much smaller and is strongly encouraged to contribute to the distribution. In contrast, the Ubuntu community is relatively large and can therefore tolerate a much larger percentage of users who do not actively contribute to development, packaging, or repository maintenance.

### Linux Mint

*   [Linux Mint](http://www.linuxmint.com/) was born as an [Ubuntu](#Ubuntu) derivative, and later added the LMDE (Linux Mint Debian Edition) that is instead based on [Debian](#Debian_GNU.2FLinux). On the other hand, Arch is an independent distribution that relies on its own [build system](/index.php/ABS "ABS") and [repositories](/index.php/Official_repositories "Official repositories").
*   Similarly to Ubuntu, Mint aims to be "a modern, elegant and comfortable operating system which is both powerful and easy to use" and its targeted user base, approach concerning the default distribution's packages and targets are clearly opposite to Arch's [minimalism](/index.php/The_Arch_Way "The Arch Way").
*   Mint includes several graphical tools for easier maintenance, called _MintTools_. Arch only provides simple command-line tools like [pacman](/index.php/Pacman "Pacman") and leaves system management to be organized by the user.
*   Mint mainly ships with [Cinnamon](/index.php/Cinnamon "Cinnamon") or [MATE](/index.php/MATE "MATE") as its GUI, and alternatively [KDE](/index.php/KDE "KDE") or [Xfce4](/index.php/Xfce4 "Xfce4"), plus codecs, flash, DVD playback and MP3 support, some of which are proprietary software; it also includes a variety of popular software, such as [Firefox](/index.php/Firefox "Firefox"), [GIMP](/index.php/GIMP "GIMP"), [LibreOffice](/index.php/LibreOffice "LibreOffice"), [pidgin](/index.php/Pidgin "Pidgin") and others. Arch's base installation does not even include [Xorg](/index.php/Xorg "Xorg"), let alone any window managers or desktop environments, which, if needed, can only be installed as a later step. Also, no proprietary software is included in Arch's default distribution.
*   New versions of Mint are released every six months, about a month after Ubuntu. Each release is based on the most recent Ubuntu LTS and is supported for five years. Linux Mint Debian Edition (LMDE) is based on Debian Stable and only receives updates in Mint packages and security updates. Arch is instead a full rolling-release distribution.
*   Mint uses APT as its package manager; Arch uses [pacman](/index.php/Pacman "Pacman").

### openSUSE

openSUSE is centered around the RPM package format and its well-regarded YaST2 GUI-driven configuration tool, which is a one-stop shop for most users' system configuration needs, including package management. Arch does not offer such a facility as it goes against [The Arch Way](/index.php/The_Arch_Way "The Arch Way"). openSUSE, therefore, is somewhat more appropriate for less-experienced users, or those who want a more GUI-driven environment, auto-configuration and expected functionality out of the box while still allowing depth of customization.

### Mandriva/Mageia

Mandriva Linux (formerly Mandrake Linux) was created in 1998 with the goal of making GNU/Linux easy to use for everyone; it is RPM-based and uses the urpmi package manager. Mageia is a Mandriva fork created by former Mandriva employees which opposes its parent distribution's commercial position, being a non-profit and community-driven project. Again, Arch takes a simpler approach than Mandriva or Mageia, being text-based and relying on more manual configuration, and is aimed at intermediate to advanced users.

### PCLinuxOS

*   PCLinuxOS is a popular distribution originally based on Mandriva providing a complete DE, designed for user-friendliness and is described as "simple", though its definition of simple is quite different than the Arch definition. Arch is designed as a simple base system to be customized from the ground up and is aimed more toward advanced users.

*   PCLOS uses the apt package manager as a wrapper for RPM packages. Arch uses its own independently-developed [pacman](/index.php/Pacman "Pacman") package manager with _.pkg.tar.xz_ packages.

*   PCLOS is very GUI-driven, provides GUI hardware configuration tools and the Synaptic package management front-end, and claims to have little or no reliance on the shell. Arch is command-line oriented and designed for more simple approaches to system configuration, management and maintenance.

## The *BSDs

*BSDs share a common origin and descend directly from the work done at UC Berkeley to produce a freely redistributable, free of cost, UNIX system. They are not GNU/Linux distributions, but rather, UNIX-like operating systems. Therefore, although Arch and the *BSDs share the concept of a tightly-integrated base and ports system, they are absolutely not related from a code standpoint, except for perhaps _vi_, as Arch's _vi_ is the original BSD _vi_ (most *BSDs do not use the original BSD _vi_ anymore). *BSDs were derived from the original AT&T UNIX code and have a true UNIX heritage. To learn more about the *BSD variants, visit the vendor's site.

### FreeBSD

*   Both Arch and [FreeBSD](http://www.freebsd.org/about.html) offer software which can be obtained using binaries or compiled using _ports_ systems.

*   Like other *BSDs, the FreeBSD base is developed fundamentally as a system designed as a whole, with each application _ported_ over to FreeBSD and made sure to work in the process. In contrast, GNU/Linux distributions such as Arch exist as amalgams combined from many separate sources.

*   The FreeBSD license is generally more protective of the _coder_, in contrast to the GPL, which favors protection of the _code_ itself. Arch is released under the GPL.

*   In FreeBSD, like Arch, decisions are delegated to you, the power user. This may be the most interesting comparison to Arch since it goes head-to-head in package modernity and has a somewhat sizable, smart, active, no-nonsense community.

*   Both systems share many similarities and FreeBSD users will generally feel quite comfortable with most aspects of Arch.

### NetBSD

*   NetBSD is a free, secure, and highly portable UNIX-like open-source operating system available for over 50 platforms, from 64-bit Opteron machines and desktop systems to hand-held and embedded devices. Its clean design and advanced features make it excellent in both production and research environments, and it is user-supported with complete source. Many applications are easily available through pkgsrc, the NetBSD Packages Collection.

*   Arch may not operate on the vast number of devices NetBSD operates on, but for an i686 system it may offer more applications.

*   NetBSD's pkgsrc provides a source based method of installation similar to Arch's ABS; however binary packages are also available using _pkg_tools_.

*   Arch does share similarities with NetBSD: both require manual configuration, they are minimalist and lightweight, both offer ports systems as well as binaries and both have active, no-nonsense developers and communities.

### OpenBSD

The OpenBSD project produces a free, multi-platform 4.4BSD-based UNIX-like operating system.

*   OpenBSD focuses on portability, standardization, code correctness, proactive security, and integrated cryptography. In contrast, Arch focuses more on simplicity, elegance, minimalism and bleeding edge software. OpenBSD is self-described as "perhaps the #1 security OS".

*   Both Arch and OpenBSD offer a small, elegant base install.

*   Both offer a ports and packaging system to allow for easy installation and management of programs which are not part of the base operating system.

*   In contrast to a GNU/Linux system like Arch, but in common with most other BSD-based operating systems, the OpenBSD kernel and userland programs, such as the shell and common tools (like _ls_, _cp_, _cat_ and _ps_), are developed together in a single source repository.

### OS X

Apple's OS X is UNIX-based, and its similarities with Arch end there.

*   Arch is a distribution of Linux, but OS X is based from Unix TSS (Which derives all code from the original BSD) and FreeBSD.

*   OS X is "Baby-proofed", and assumes that all users are not technically competent. All folders in the root directory, except for /Applications (For "Applications", which are bundles of binaries and related files), /Library (For Shared OS X Libraries), /System (For System Library Files), and /Users (Equivalent to Arch's /home), are hidden by default, and /usr is write-only, even as the root user. It also stores all binaries and files related to programs that it expects users to run in /Applications, removing the need for novice users to access /bin.

*   OS X does not come with a command-line package manager. Apple expects users to install packages from the "Mac App Store", and by default, doesn't let any third-party programs from other sources run. For extra command-line utilities, it is recommended to install another package manager, such as [Homebrew](http://brew.sh/).

*   "Aqua", a desktop environment and theme build for Mac OS X, is pre-installed with OS X, and not removable.

*   Arch is freely distributable. OS X has a license which restricts the user in many ways (Explaination [here](http://robb.weblaws.org/2015/10/17/os-x-el-capitan-license-in-plain-english/)).

## See also

*   [DistroWatch](http://distrowatch.com/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Arch_compared_to_other_distributions&oldid=417741](https://wiki.archlinux.org/index.php?title=Arch_compared_to_other_distributions&oldid=417741)"