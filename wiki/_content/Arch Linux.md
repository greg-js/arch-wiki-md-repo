# Arch Linux

Arch Linux is an independently developed, [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) "wikipedia:P6 (microarchitecture)")/[x86-64](https://en.wikipedia.org/wiki/x86-64 "wikipedia:x86-64") general purpose GNU/Linux distribution versatile enough to suit any role. Development focuses on simplicity, minimalism, and code elegance. Arch is installed as a minimal base system, configured by the user upon which their own ideal environment is assembled by installing only what is required or desired for their unique purposes. GUI configuration utilities are not officially provided, and most system configuration is performed from the shell and a text editor. Based on a rolling-release model, Arch strives to stay bleeding edge, and typically offers the latest stable versions of most software.

## Contents

*   [1 Principles](#Principles)
    *   [1.1 Simplicity](#Simplicity)
    *   [1.2 Modernity](#Modernity)
    *   [1.3 Pragmatism](#Pragmatism)
    *   [1.4 User centrality](#User_centrality)
    *   [1.5 Versatility](#Versatility)
*   [2 Software packaging](#Software_packaging)
*   [3 Community](#Community)
*   [4 History](#History)
    *   [4.1 The early years](#The_early_years)
    *   [4.2 The middle years](#The_middle_years)
    *   [4.3 The dawning of the age of A. Griffin](#The_dawning_of_the_age_of_A._Griffin)

## Principles

The following core principles comprise what is commonly referred to as _the Arch Way_, or the Arch Philosophy, perhaps best summarized by the acronym KISS for Keep It Simple, Stupid.

### Simplicity

_Simplicity is the ultimate sophistication._ — Leonardo da Vinci

Arch Linux defines simplicity as _without unnecessary additions, modifications, or complications_. It ships software as released by the original developers ([upstream](https://en.wikipedia.org/wiki/Upstream_(software_development) "wikipedia:Upstream (software development)")) with minimal distribution-specific (downstream) changes.

Patches not accepted by upstream are avoided. Arch's downstream patches consist almost entirely of backported bug fixes that are obsoleted by the project's next release. In a similar fashion, Arch ships the configuration files provided by upstream with changes limited to distribution-specific issues like adjusting the system file paths. It does not add automation features such as enabling a service simply because the package was installed.

Arch Linux packages usually correspond directly to upstream projects. Packages are only split when compelling advantages exist rather than it being the norm. Splitting is only done to save disk space in particularly bad cases of waste.

### Modernity

Arch Linux strives to maintain the latest stable release versions of its software as long as systemic package breakage can be reasonably avoided. It is based on a [rolling-release](https://en.wikipedia.org/wiki/Rolling_release "wikipedia:Rolling release") system, which allows a one-time installation with continuous upgrades, without ever having to reinstall and without having to perform the elaborate procedures involved in system upgrades from one release version to the next. By issuing one command, an Arch system is kept up-to-date.

Arch incorporates many of the newer features available to GNU/Linux users, including the [systemd](/index.php/Systemd "Systemd") init system, modern filesystems (Ext2/3/4, Reiser, XFS, JFS, BTRFS), LVM2, software RAID, udev support and initcpio (with [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")), as well as the latest available kernels.

### Pragmatism

_Correctness is clearly the prime quality. If a system does not do what it is supposed to do, then everything else about it matters little._ — Bertrand Meyer

Arch is a pragmatic distribution rather than an ideological one. The principles here are only useful guidelines. Ultimately, design decisions are made on a case-by-case basis through developer consensus. Evidence-based technical analysis and debate are what matter, not politics or popular opinion.

The large number of packages and build scripts in the various Arch Linux repositories support freedom of choice, offering free and open source software for those who prefer it as well as proprietary software packages for those who embrace _functionality over ideology_.

### User centrality

Whereas many GNU/Linux distributions attempt to be more _user-friendly_, Arch Linux has always been, and shall always remain _user-centric_. The distribution is intended to fill the needs of those contributing to it rather than trying to appeal to as many users as possible. It is suited to anyone with a do-it-yourself attitude that's willing to spend some time reading the documentation and solving their own problems.

Every user is encouraged to contribute by reporting bugs, improving the community documentation on the wiki and providing technical assistance to others. Patches improving packages or the core projects are highly valued and the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") offers a repository of user-contributed packages. Arch's developers are volunteers and active contributors will often find themselves becoming part of that team.

As Judd Vinet, the founder of the Arch Linux project said: "[Arch Linux] is what _you_ make it."

### Versatility

Arch Linux is a general purpose distribution. Upon installation, a command-line environment is provided: rather than tearing out unneeded and unwanted packages, the user is offered the ability to build on a basic but carefully chosen set of software suitable for nearly any use case. Arch's design philosophy and implementation make it easy to extend and mold into whatever kind of system is required, from a basic console machine to feature-rich desktop environments: it is the user who decides what his system will be.

## Software packaging

Arch is backed by [pacman](/index.php/Pacman "Pacman"), an easy-to-use binary [package manager](https://en.wikipedia.org/wiki/Package_manager "wikipedia:Package manager") that allows you to upgrade your entire system with one command. Pacman is coded in _C_ and designed from the ground up to be lightweight, simple and very fast. Arch also provides the [Arch Build System](/index.php/Arch_Build_System "Arch Build System"), a ports-like system to make it easy to build and install packages from source, which can also be synchronized with one command. You can even rebuild your entire system with one command.

Supporting i686 and x86-64 architectures, Arch's [Official repositories](/index.php/Official_repositories "Official repositories") provide several thousands of high-quality packages to meet your software demands. In addition, Arch encourages community growth and contribution by offering the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"), which contains many thousands of user-maintained PKGBUILD scripts for compiling installable packages from source using the _makepkg_ application. It is also possible for users to easily build and maintain their own custom repositories.

## Community

The Arch community is very dependable, lively and welcoming: all _Archers_ are encouraged to participate and contribute to the distribution, be it helping with the development of the core software, maintaining packages, reporting or fixing [bugs](https://bugs.archlinux.org/), improving the [ArchWiki documentation](/index.php/Main_page "Main page"), helping other users solving problems or just exchanging opinions in the [forums](https://bbs.archlinux.org/), [mailing lists](https://mailman.archlinux.org/mailman/listinfo/), [IRC channels](/index.php/IRC_channels "IRC channels"), or sharing one's knowledge or even self-developed applications. Arch Linux is the operating system of choice for many people around the globe, and there exist several [international communities](/index.php/International_communities "International communities") that offer help and provide documentation in many different languages.

See [Getting involved](/index.php/Getting_involved "Getting involved") if you feel you want to become an active member of the community.

## History

### The early years

Judd Vinet, a Canadian programmer and occasional guitarist, began developing Arch Linux in early 2001\. Its first formal release, Arch Linux 0.1, was on March 11, 2002\. Inspired by the elegant simplicity of [Slackware](http://www.slackware.com/), [BSD](http://en.wikipedia.org/wiki/Berkeley_Software_Distribution), [PLD Linux](http://www.pld-linux.org/), and [CRUX](http://crux.nu/), and yet disappointed with their lack of package management at the time; Vinet built his own distribution on similar principles as those distros. But, he also wrote a package management program called [pacman](/index.php/Pacman "Pacman"), to automatically handle package installation, removal, and upgrades.

### The middle years

The early Arch community grew steadily, as evidenced by [this chart of forum posts, users, and bug reports](https://dev.archlinux.org/~dan/archstats.svg). Moreover, it was from its early days known as [an open, friendly, and helpful community](http://www.osnews.com/story/4827).

### The dawning of the age of A. Griffin

In late 2007, Judd Vinet retired from active participation as an Arch developer, and [smoothly transferred the reins over to American programmer Aaron Griffin](https://bbs.archlinux.org/viewtopic.php?id=38024), aka Phrakture, who remains the lead Arch developer to this day.

Over the years, the Arch community continued to grow and mature, and has recently received an unusual amount of [attention and review](/index.php/Arch_Linux_Press_Review "Arch Linux Press Review") for a Linux distro of its modest size.

Arch developers remain unpaid, part-time volunteers, and there are no prospects for monetizing Arch Linux, so it will remain free in all senses of the word. Those curious to peruse more detail about Arch's development history can browse the [Arch entry in the Internet Archive Wayback Machine](http://web.archive.org/web/*/archlinux.org) and the [Arch Linux News Archives](https://www.archlinux.org/news/).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Arch_Linux&oldid=390802](https://wiki.archlinux.org/index.php?title=Arch_Linux&oldid=390802)"