[مستودع البرنامج](https://en.wikipedia.org/wiki/software_repository "wikipedia:software repository") هو موقع لتخزين حزم البرامج التي قد يتم طلبها و تثبينها في جهاز الكمبيوتر . مشرفو حزم ارش لينكس (المطورين والمستخدمين الموثوق بهم) يقومون برعاية عدد من المستودعات الرسمية المحتوية على حزم البرمجيات الأساسية والشعبية، يمكن الوصول الى الحزم بسهولة عبر [pacman](/index.php/Pacman "Pacman"). هذه المقالة تتطرق للمستودعات المدعومة رسميا.

## Contents

*   [1 الخلفية التاريخية](#.D8.A7.D9.84.D8.AE.D9.84.D9.81.D9.8A.D8.A9_.D8.A7.D9.84.D8.AA.D8.A7.D8.B1.D9.8A.D8.AE.D9.8A.D8.A9)
*   [2 [core]](#.5Bcore.5D)
*   [3 [extra]](#.5Bextra.5D)
*   [4 [community]](#.5Bcommunity.5D)
*   [5 [multilib]](#.5Bmultilib.5D)
*   [6 [testing]](#.5Btesting.5D)
*   [7 [community-testing]](#.5Bcommunity-testing.5D)
*   [8 [multilib-testing]](#.5Bmultilib-testing.5D)

## الخلفية التاريخية

Most of the repository splits are for historical reasons. Originally, when Arch Linux was used by very few users, there was only one repository known as [official] (now [core]). At the time, [official] basically contained Judd Vinet's preferred applications. It was designed to contain one of each "type" of program -- one DE, one major browser, etc. There were users back then that did not like Judd's selection, so since the Arch Build System is so easy to use, they created packages of their own. These packages went into a repository called [unofficial], and were maintained by developers other than Judd. Eventually, the two repositories were both considered equally supported by the developers, so the names [official] and [unofficial] no longer reflected their true purpose. They were subsequently renamed to [current] and [extra] sometime near the release version 0.5. Shortly after the 2007.8.1 release, [current] was renamed [core] in order to prevent confusion over what exactly it contains. The repositories are now more or less equal in the eyes of the developers and the community, but [core] does have some differences. The main distinction is that packages used for Installation CDs and release snapshots are taken only from [core]. This repository still gives a complete Linux system, though it may not be the Linux system you want. Now, sometime around 0.5 or 0.6, they found there were a lot of packages that the developers did not want to maintain. One of the developers (Xentac) set up the "Trusted User Repositories", which were unofficial repositories in which trusted users could place packages they had created. There was a [staging] repository where packages could be promoted into the official repositories by one of the Arch Linux developers, but other than this, the developers and trusted users were more or less distinct. This worked for a while, but not when trusted users got bored with their repositories, and not when untrusted users wanted to share their own packages. This led to the development of the AUR. The TUs were conglomerated into a more closely knit group, and they now collectively maintain the [community] repository. The Trusted Users are still a separate group from the Arch Linux developers, and there is not a lot of communication between them. However, popular packages are still promoted from [community] to [extra] on occasion. The AUR also allows untrusted users to submit PKGBUILDs. After a kernel in [core] broke many user systems, the "core signoff policy" was introduced. Since then, all package updates for [core] need to go through a [testing] repository first, and only after multiple signoffs from other developers are they allowed to move. Over time, it was noticed that various [core] packages had low usage, and user signoffs or even lack of bug reports became informally accepted as criteria to accept such packages. In late 2009/the beginning of 2010, with the advent of some new filesystems and the desire to support them during installation, along with the realization that [core] was never clearly defined (just "important packages, handpicked by developers"), the repository received a more accurate description (see below).

## [core]

This repository can be found in `.../core/os/` on your favorite mirror.

It has fairly strict quality requirements:

*   Developers and/or users need to signoff on updates before package updates are accepted.

*   For packages with low usage, a reasonable exposure (i.e. inform people about update, request signoffs, keep in testing up to a week depending on the severity of the change, lack of outstanding bug reports, along with the implicit signoff of the package maintainer) is enough.

It contains packages which:

*   are needed to boot any kind of supported Arch system.
*   may be needed to connect to the Internet.
*   are essential for package building.
*   can manage and check/repair supported filesystems.
*   virtually anyone will want or need early in the system setup process (e.g. [openssh](https://www.archlinux.org/packages/?name=openssh)).
*   are dependencies (but not necessarily makedepends) of the above.

**ملاحظة:** This repository used to be included in the core installation media, so you could build a fully working base system without Internet access. This is no longer the case. Internet access is now required in order to install a new system. See [here](/index.php/Pacman_tips#Installing_packages_from_a_CD.2FDVD_or_USB_stick "Pacman tips") if you would like to create a local repository with packages from [core] or from any of the other repositories.

## [extra]

This repository can be found in `.../extra/os/` on your favorite mirror.

It contains all packages that do not fit in [core]. Example: Xorg, window managers, web browsers, media players, tools for working with languages such as Python and Ruby, and a lot more.

## [community]

This repository can be found in `.../community/os/` on your favorite mirror.

It contains packages from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") which gained enough votes to be adopted by a [Trusted User](/index.php/Trusted_Users "Trusted Users").

## [multilib]

This repository can be found in `.../multilib/os/` on your favorite mirror.

It contains 32 bit software and libraries that can be used to run and build 32 bit applications on 64 bit installs (e.g. [wine](https://www.archlinux.org/packages/?name=wine), [skype](https://www.archlinux.org/packages/?name=skype), etc).

For more information, see [Multilib](/index.php/Multilib "Multilib").

## [testing]

**تحذير:** Be careful when enabling the [testing] repository. Your system may break after performing an update. Only experienced users who know how to deal with potential system breakage should use it.

This repository can be found in `.../testing/os/` on your favorite mirror.

It's special because it contains packages that are candidates for the [core] or [extra] repositories.

New packages go into [testing] if:

*   They are expected to break something on update and need to be tested first.

*   They require other packages to be rebuilt. In this case, all packages that need to be rebuilt are put into [testing] first and when all rebuilds are done, they are moved back to the other repositories.

This is the only repository that can have name collisions with any of the other official repositories. If enabled, it has to be the first repository listed in your `/etc/pacman.conf` file.

Note that it's not for the "newest of the new" package versions. Part of its purpose is to hold package updates that have the potential to **cause system breakage**, either by being part of the [core] set of packages, or by being critical in other ways. As such, users of the [testing] repository are **strongly encouraged** to subscribe to the [arch-dev-public](https://mailman.archlinux.org/mailman/listinfo/arch-dev-public) mailing list, watch the [[testing] Repository Forum](https://bbs.archlinux.org/viewforum.php?id=49), and to [report](https://bugs.archlinux.org/) all bugs.

If you enable [testing], you must also enable [community-testing].

## [community-testing]

This repository is like the [testing] repository, but for packages that are candidates for the [community] repository.

If you enable it, you must also enable [testing].

## [multilib-testing]

This repository is like the [testing] repository, but for packages that are candidates for the [multilib] repository.

If you enable it, you must also enable [testing].