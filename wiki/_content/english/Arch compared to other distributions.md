This page attempts to draw a comparison between Arch Linux and other popular GNU/Linux distributions and UNIX-like operating systems. The summaries that follow are brief descriptions that may help a person decide if Arch Linux will suit his or her needs. Although reviews and descriptions can be useful, first-hand experience is invariably the best way to compare distributions.

For a more complete comparison, see [w:Comparison of operating systems](https://en.wikipedia.org/wiki/Comparison_of_operating_systems "w:Comparison of operating systems") and [w:Comparison of Linux distributions](https://en.wikipedia.org/wiki/Comparison_of_Linux_distributions "w:Comparison of Linux distributions").

## Contents

*   [1 Source-based](#Source-based)
    *   [1.1 CRUX](#CRUX)
    *   [1.2 LFS](#LFS)
    *   [1.3 Gentoo/Funtoo Linux](#Gentoo.2FFuntoo_Linux)
*   [2 General](#General)
    *   [2.1 Debian GNU/Linux](#Debian_GNU.2FLinux)
    *   [2.2 Fedora](#Fedora)
    *   [2.3 Slackware](#Slackware)
*   [3 Beginner-friendly](#Beginner-friendly)
    *   [3.1 Ubuntu](#Ubuntu)
    *   [3.2 Linux Mint](#Linux_Mint)
    *   [3.3 openSUSE](#openSUSE)
    *   [3.4 Mandriva/Mageia](#Mandriva.2FMageia)
*   [4 The *BSDs](#The_.2ABSDs)
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
*   LFS provides no online repositories; sources are manually obtained, compiled and installed with *make*. (Several manual methods of package management exist, and are mentioned in LFS Hints).
*   Arch provides these very same packages, plus [systemd](/index.php/Systemd "Systemd"), a few extra tools and the powerful [pacman](/index.php/Pacman "Pacman") package manager as its base system, already compiled for i686/x86_64\. Along with the minimal Arch base system, the Arch community and developers provide and maintain many thousands of binary packages installable via pacman as well as [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") build scripts for use with the [Arch Build System](/index.php/Arch_Build_System "Arch Build System"). Arch also includes the [makepkg](/index.php/Makepkg "Makepkg") tool for expediently building or customizing *.pkg.tar.xz* packages, readily installable by pacman.
*   Judd Vinet built Arch from scratch, and then wrote pacman in C. Historically, Arch was sometimes humorously described simply as "Linux, with a nice package manager."

### Gentoo/Funtoo Linux

*   Both Arch Linux and Gentoo Linux are rolling release systems, making packages available to the distribution a short time after they are released upstream.
*   The Gentoo packages and base system are built directly from source code according to user-specified *USE flags*. Arch provides a ports-like system for building packages from source, though the Arch base system is designed to be installed as pre-built i686/x86_64 binary. This generally makes Arch quicker to build and update, and allows Gentoo to be more systemically customizable.
*   Arch supports i686 and x86_64 while Gentoo officially supports x86 (i486/i686), x86_64, PPC/PPC64, SPARC, Alpha, ARM, MIPS, HPPA, S/390 and Itanium architectures.
*   Gentoo's official package and system management tools tend to be rather more complex and "powerful" than those provided by Arch, and certain features which are at the very heart of Gentoo *([USE flags](https://wiki.gentoo.org/wiki/Handbook:X86/Working/USE), [SLOTs](https://wiki.gentoo.org/wiki/Handbook:X86/Working/Portage#Terminology), etc.)* do not have any direct Arch Linux equivalent. Some of that is due to the fact that Arch is primarily a binary distro, but differences in [design philosophy](/index.php/Arch_Linux#Principles "Arch Linux") also play a big role, with Arch taking a more principled stance in favor of architectural simplicity and avoiding over-engineering.
*   Because both the Gentoo and Arch installations only include a base system, both are considered to be highly customizable. If comfortable with [systemd](/index.php/Systemd "Systemd"), Gentoo users will also generally feel at ease with most other aspects of Arch.

## General

These distributions offer a broad range of advantages and strengths, and can be made to serve most operating system uses.

### Debian GNU/Linux

*   Debian is the largest upstream Linux distribution with a bigger community and features stable, testing, and unstable branches, offering over 43,000 packages. The available number of Arch binary packages is more modest. However, when including the AUR, the quantities are very comparable.

*   Debian has a more vehement stance on free software but still includes non-free software in its non-free repos. Arch is more lenient, and therefore inclusive, concerning *non-free packages* as defined by GNU.

*   Debian focuses on stringent testing of the Stable branch, which is "frozen" and supported up to [five years](https://wiki.debian.org/LTS). Arch packages are more current than Debian Stable and Testing, being more comparable to the Debian Unstable branch, and has no fixed release schedule.

*   Debian is available for many architectures, including alpha, arm, hppa, i386, x86_64, ia64, m68k, mips, mipsel, powerpc, s390, and sparc, whereas Arch is officially i686 and x86_64, with community ports for arm (for Raspberry Pi for example) only.

*   Arch provides more expedient support for building custom, installable packages from outside sources, with a ports-like package build system. Debian does not offer a ports system, relying instead on its large binary repositories.

*   The Arch installation system only offers a minimal base, transparently exposed during system configuration, whereas Debian's methods, such as the use of apt *tasks* to install pre-selected groups of packages, offer a more automatically configured approach as well as several alternative methods of installation.

*   Arch generally packages software libraries together with their header files, whereas in Debian header files have to be downloaded separately.

*   Arch keeps patching to a minimum, thus avoiding problems that upstream are unable to review, whereas Debian patches its packages more liberally for a wider audience.

### Fedora

*   Fedora is community developed, yet corporately backed by Red Hat; it is often presented as a testbed release system. Fedora packages and projects migrate to RHEL and some eventually become adopted by other distributions. Arch has no fixed releases, and does not serve as a testing branch for another distribution.

*   Fedora packages use the RPM format with the DNF package manager. Arch uses [pacman](/index.php/Pacman "Pacman") to manage tar.xz packages.

*   Fedora refuses to include MP3 media support and other non-free software in official repositories due to its dedication to free software, though third-party repositories are available for such packages. Arch is more lenient in its disposition toward MP3 and non-free software, leaving the discernment to the user.

*   Fedora offers many installation options including a graphical installer as well as a minimal option. Fedora "spins" also provide alternative assortments of desktop environments to choose from, each with a modest assortment of default packages. Arch, on the other hand, only provides a few scripts meant to ease the process of a minimal base system install.

*   Fedora has a scheduled release cycle, but officially supports discrete version upgrades with the FedUp tool. Arch is a rolling-release system.

*   Arch features a ports system, whereas Fedora does not.

*   Both Arch and Fedora are targeted at experienced users and developers. Both strongly encourage their users to contribute to project development.

*   Fedora has earned much community recognition for integration of SELinux, GCJ compiled packages (to remove the need for Oracle's JRE), and prolific upstream contribution; Red Hat and thus, Fedora developers by extension, contribute the highest percentage of Linux kernel code as compared to any other project.

*   Arch Linux provides what is widely regarded as the most thorough and comprehensive distribution wiki. The Fedora wiki is used in the original sense of the word "wiki", or a way to exchange information between developers, testers and users rapidly. It is not meant to be an end-user knowledge base like Arch's. Fedora's wiki resembles an issue tracker or a corporate wiki.

### Slackware

*   Slackware and Arch are quite similar in that both are simple distributions focused on elegance and minimalism.

*   Slackware is famous for its lack of branding and completely vanilla packages, from the kernel up. Arch typically applies patching only to avoid severe breakage or to ensure packages will compile cleanly.

*   Slackware uses BSD-style init scripts, Arch uses [systemd](/index.php/Systemd "Systemd").

*   Arch supplies a package management system in [pacman](/index.php/Pacman "Pacman") which, unlike Slackware's standard tools, offers automatic dependency resolution and allows for more automated system upgrades. Slackware users typically prefer their method of manual dependency resolution, citing the level of system control it grants them, as well as Slackware's excellent supply of pre-installed libraries and dependencies.

*   Arch is a rolling-release system. Slackware is seen as more conservative in its release cycle, preferring proven stable packages. Arch is more *bleeding-edge* in this respect.

*   Arch Linux provides many thousands of binary packages within its official repositories whereas Slackware official repositories are more modest.

*   Arch offers the [Arch Build System](/index.php/Arch_Build_System "Arch Build System"), an actual ports-like system and also the [AUR](/index.php/AUR "AUR"), a very large collection of PKGBUILDs contributed by users. Slackware offers a similar, though slimmer system at [slackbuilds.org](http://www.slackbuilds.org) which is a semi-official repository of Slackbuilds, which are analogous to Arch PKGBUILDs. Slackware users will generally be quite comfortable with most aspects of Arch.

## Beginner-friendly

Sometimes called "newbie distros", the beginner-friendly distributions share a lot of similarities, though Arch is quite different from them. Arch may be a better choice if you want to learn about GNU/Linux by building up from a small base, as an installation of Arch installs few packages in comparison. Specific differences between distributions are described below.

### Ubuntu

*   Ubuntu is a popular Debian-based distribution commercially sponsored by Canonical Ltd., while Arch is an independently developed system built from scratch.

*   The two projects have very different goals and are targeted at a different user base. Arch is designed for users who desire a do-it-yourself approach, whereas Ubuntu provides a preconfigured system. Arch presents a simpler design from the base installation onward, relying on the user to customize it to their own specific needs. Many Arch users have started on Ubuntu and eventually migrated to Arch.

*   Arch development is not biased towards any one particular user interface beyond what its community provide support for. Furthermore, Canonical's commercial nature has led them to some controversial decisions, such as the inclusion of advertisements in Unity's *Dash* menu and user data collection. Arch is an independent, community-driven project with no commercial agenda.

*   Ubuntu moves between discrete releases every 6 months, whereas Arch is a rolling-release system.

*   Arch offers a ports-like package build system and the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"), where users can share source packages for the [pacman](/index.php/Pacman "Pacman") package manager. Ubuntu uses the more complex [apt](https://en.wikipedia.org/wiki/Advanced_Packaging_Tool "wikipedia:Advanced Packaging Tool"), and allows redistribution of binary packages via [Personal Package Archives](https://launchpad.net/ubuntu/+ppas).

*   The two communities differ in some ways as well. The Arch community is much smaller and is strongly encouraged to contribute to the distribution. In contrast, the Ubuntu community is relatively large and can therefore tolerate a much larger percentage of users who do not actively contribute to development, packaging, or repository maintenance.

### Linux Mint

*   [Linux Mint](http://www.linuxmint.com/) was born as an [Ubuntu](#Ubuntu) derivative, and later added the LMDE (Linux Mint Debian Edition) that is instead based on [Debian](#Debian_GNU.2FLinux). On the other hand, Arch is an independent distribution that relies on its own [build system](/index.php/ABS "ABS") and [repositories](/index.php/Official_repositories "Official repositories").
*   Mint includes several graphical tools for easier maintenance, called *MintTools*. Arch only provides simple command-line tools like [pacman](/index.php/Pacman "Pacman") and leaves system management to be organized by the user.
*   Mint mainly ships with [Cinnamon](/index.php/Cinnamon "Cinnamon") or [MATE](/index.php/MATE "MATE") as its GUI, and alternatively [KDE](/index.php/KDE "KDE") or [Xfce4](/index.php/Xfce4 "Xfce4"), plus codecs, flash, DVD playback and MP3 support, some of which are proprietary software.
*   New versions of Mint are released every six months, about a month after Ubuntu. Each release is based on the most recent Ubuntu LTS and is supported for five years. Linux Mint Debian Edition (LMDE) is based on Debian Stable and only receives updates in Mint packages and security updates. Arch is instead a full rolling-release distribution.

### openSUSE

openSUSE is centered around the RPM package format and its well-regarded YaST2 GUI-driven configuration tool. Arch does not offer such a facility. openSUSE, may therefore be more appropriate for users who want a more GUI-driven environment, automatic configuration, or expected functionality out of the box while still allowing depth of customization.

### Mandriva/Mageia

Mandriva Linux (formerly Mandrake Linux) was created in 1998 with the goal of making GNU/Linux easy to use for everyone; it is RPM-based and uses the urpmi package manager. Mageia is a Mandriva fork created by former Mandriva employees which opposes its parent distribution's commercial position, being a non-profit and community-driven project. Again, Arch takes a simpler approach than Mandriva or Mageia, being text-based and relying on more manual configuration, and is aimed at intermediate to advanced users.

## The *BSDs

*   The *BSDs share a common origin and descend directly from the work done at UC Berkeley to produce a freely redistributable, free of cost, UNIX system. They are not GNU/Linux distributions, but rather, UNIX-like operating systems, and derived from the original AT&T UNIX code.

*   Arch and the *BSDs share the concept of a tightly-integrated base and ports system. However, unlike GNU/Linux distributions such as Arch, the *BSD kernel and userland programs (such as the shell and core utilities like *ls*, *cp*, *cat*, and *ps*) are developed together in a single source repository.

*   The BSD license is generally more protective of the *coder*, in contrast to the GPL, which favors protection of the *code* itself. Arch is released under the GPL.

*   To learn more about the *BSD variants, see [Wikipedia:Comparison of BSD operating systems](https://en.wikipedia.org/wiki/Comparison_of_BSD_operating_systems "wikipedia:Comparison of BSD operating systems").

## See also

*   [DistroWatch](http://distrowatch.com/)