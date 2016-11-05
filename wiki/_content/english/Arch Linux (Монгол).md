Arch Linux is an independently developed, i686/x86-64 general-purpose GNU/Linux distribution that strives to provide the latest stable versions of most software by following a rolling-release model. The default installation is a minimal base system, configured by the user to only add what is purposely required.

## Contents

*   [1 Үндсэн асуудал](#.D2.AE.D0.BD.D0.B4.D1.81.D1.8D.D0.BD_.D0.B0.D1.81.D1.83.D1.83.D0.B4.D0.B0.D0.BB)
    *   [1.1 Энгийн](#.D0.AD.D0.BD.D0.B3.D0.B8.D0.B9.D0.BD)
    *   [1.2 Орчин үеийн](#.D0.9E.D1.80.D1.87.D0.B8.D0.BD_.D2.AF.D0.B5.D0.B8.D0.B9.D0.BD)
    *   [1.3 Прагматизм](#.D0.9F.D1.80.D0.B0.D0.B3.D0.BC.D0.B0.D1.82.D0.B8.D0.B7.D0.BC)
    *   [1.4 Хэрэглэгч төвт](#.D0.A5.D1.8D.D1.80.D1.8D.D0.B3.D0.BB.D1.8D.D0.B3.D1.87_.D1.82.D3.A9.D0.B2.D1.82)
    *   [1.5 Олон талт байдал](#.D0.9E.D0.BB.D0.BE.D0.BD_.D1.82.D0.B0.D0.BB.D1.82_.D0.B1.D0.B0.D0.B9.D0.B4.D0.B0.D0.BB)
*   [2 Түүх](#.D0.A2.D2.AF.D2.AF.D1.85)
    *   [2.1 Эхний жилүүд](#.D0.AD.D1.85.D0.BD.D0.B8.D0.B9_.D0.B6.D0.B8.D0.BB.D2.AF.D2.AF.D0.B4)
    *   [2.2 Дунд үе](#.D0.94.D1.83.D0.BD.D0.B4_.D2.AF.D0.B5)
    *   [2.3 A. Griffin-ний үеийн эхлэл](#A._Griffin-.D0.BD.D0.B8.D0.B9_.D2.AF.D0.B5.D0.B8.D0.B9.D0.BD_.D1.8D.D1.85.D0.BB.D1.8D.D0.BB)

## Үндсэн асуудал

### Энгийн

Arch Linux defines simplicity as *without unnecessary additions or modifications*. It ships software as released by the original developers ([upstream](https://en.wikipedia.org/wiki/Upstream_(software_development) "wikipedia:Upstream (software development)")) with minimal distribution-specific (downstream) changes: patches not accepted by upstream are avoided, and Arch's downstream patches consist almost entirely of backported bug fixes that are obsoleted by the project's next release.

In a similar fashion, Arch ships the configuration files provided by upstream with changes limited to distribution-specific issues like adjusting the system file paths. It does not add automation features such as enabling a service simply because the package was installed. Packages are only split when compelling advantages exist, such as to save disk space in particularly bad cases of waste. GUI configuration utilities are not officially provided, encouraging users to perform most system configuration from the shell and a text editor.

### Орчин үеийн

Arch Linux strives to maintain the latest stable release versions of its software as long as systemic package breakage can be reasonably avoided. It is based on a [rolling-release](https://en.wikipedia.org/wiki/Rolling_release "wikipedia:Rolling release") system, which allows a one-time installation with continuous upgrades.

Arch incorporates many of the newer features available to GNU/Linux users, including the [systemd](/index.php/Systemd "Systemd") init system, modern [file systems](/index.php/File_systems "File systems"), LVM2, software RAID, udev support and initcpio (with [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")), as well as the latest available kernels.

### Прагматизм

Arch is a pragmatic distribution rather than an ideological one. The principles here are only useful guidelines. Ultimately, design decisions are made on a case-by-case basis through developer consensus. Evidence-based technical analysis and debate are what matter, not politics or popular opinion.

The large number of packages and build scripts in the various Arch Linux repositories offer free and open source software for those who prefer it, as well as proprietary software packages for those who embrace *functionality over ideology*.

### Хэрэглэгч төвт

Whereas many GNU/Linux distributions attempt to be more *user-friendly*, Arch Linux has always been, and shall always remain *user-centric*. The distribution is intended to fill the needs of those contributing to it, rather than trying to appeal to as many users as possible. It is targeted at the proficient GNU/Linux user, or anyone with a do-it-yourself attitude who is willing to read the documentation, and solve their own problems.

All users are encouraged to [participate](/index.php/Getting_involved "Getting involved") and contribute to the distribution. Reporting and helping fix [bugs](https://bugs.archlinux.org/) is highly valued and patches improving packages or the core [projects](https://projects.archlinux.org/) are very appreciated: Arch's developers are volunteers and active contributors will often find themselves becoming part of that team. *Archers* can freely contribute packages to the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"), improve the [ArchWiki documentation](/index.php/Main_page "Main page"), provide technical assistance to others or just exchange opinions in the [forums](https://bbs.archlinux.org/), [mailing lists](https://mailman.archlinux.org/mailman/listinfo/), or [IRC channels](/index.php/IRC_channels "IRC channels"). Arch Linux is the operating system of choice for many people around the globe, and there exist several [international communities](/index.php/International_communities "International communities") that offer help and provide documentation in many different languages.

### Олон талт байдал

Arch Linux is a general-purpose distribution. Upon installation, only a command-line environment is provided: rather than tearing out unneeded and unwanted packages, the user is offered the ability to build a custom system by choosing among thousands of high-quality packages provided in the [official repositories](/index.php/Official_repositories "Official repositories"), supporting the [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) and [x86-64](https://en.wikipedia.org/wiki/x86-64 "wikipedia:x86-64") architectures.

Arch is backed by [pacman](/index.php/Pacman "Pacman"), a lightweight, simple and fast package manager that allows to upgrade the entire system with one command. Arch also provides the [Arch Build System](/index.php/Arch_Build_System "Arch Build System"), a ports-like system to make it easy to build and install packages from source, which can also be synchronized with one command. In addition, the *Arch User Repository* contains many thousands more of community-contributed [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") scripts for compiling installable packages from source using the [makepkg](/index.php/Makepkg "Makepkg") application. It is also possible for users to build and maintain their own custom repositories with ease.

## Түүх

### Эхний жилүүд

Judd Vinet, a Canadian programmer and occasional guitarist, began developing Arch Linux in early 2001\. Its first formal release, Arch Linux 0.1, was on March 11, 2002\. Inspired by the elegant simplicity of [Slackware](http://www.slackware.com/), [BSD](https://en.wikipedia.org/wiki/Berkeley_Software_Distribution "wikipedia:Berkeley Software Distribution"), [PLD Linux](http://www.pld-linux.org/), and [CRUX](http://crux.nu/), and yet disappointed with their lack of package management at the time; Vinet built his own distribution on similar principles as those distros. But, he also wrote a package management program called [pacman](/index.php/Pacman "Pacman"), to automatically handle package installation, removal, and upgrades.

### Дунд үе

The early Arch community grew steadily, as evidenced by [this chart of forum posts, users, and bug reports](https://dev.archlinux.org/~dan/archstats.svg). Moreover, it was from its early days known as [an open, friendly, and helpful community](http://www.osnews.com/story/4827).

### A. Griffin-ний үеийн эхлэл

In late 2007, Judd Vinet retired from active participation as an Arch developer, and [smoothly transferred the reins over to American programmer Aaron Griffin](https://bbs.archlinux.org/viewtopic.php?id=38024), aka Phrakture, who remains the lead Arch developer to this day.

Over the years, the Arch community continued to grow and mature, and has recently received an unusual amount of [attention and review](/index.php/Arch_Linux_Press_Review "Arch Linux Press Review") for a Linux distro of its modest size.

Arch developers remain unpaid, part-time volunteers, and there are no prospects for monetizing Arch Linux, so it will remain free in all senses of the word. Those curious to peruse more detail about Arch's development history can browse the [Arch entry in the Internet Archive Wayback Machine](http://web.archive.org/web/*/archlinux.org) and the [Arch Linux News Archives](https://www.archlinux.org/news/).