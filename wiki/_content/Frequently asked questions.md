# Frequently asked questions

Besides the questions covered below, you may find [The Arch Way](/index.php/The_Arch_Way "The Arch Way") and [Arch Linux](/index.php/Arch_Linux "Arch Linux") helpful. Both articles contain a good deal of information about Arch Linux.

## Contents

*   [1 General](#General)
    *   [1.1 What is Arch Linux?](#What_is_Arch_Linux.3F)
    *   [1.2 Why would I want to use Arch?](#Why_would_I_want_to_use_Arch.3F)
    *   [1.3 Why would I not want to use Arch?](#Why_would_I_not_want_to_use_Arch.3F)
    *   [1.4 What distribution is Arch based on?](#What_distribution_is_Arch_based_on.3F)
    *   [1.5 What architectures does Arch support?](#What_architectures_does_Arch_support.3F)
    *   [1.6 Does Arch support ARM CPUs?](#Does_Arch_support_ARM_CPUs.3F)
    *   [1.7 I am a complete GNU/Linux beginner. Should I use Arch?](#I_am_a_complete_GNU.2FLinux_beginner._Should_I_use_Arch.3F)
    *   [1.8 Arch requires too much time and effort to install and use. Also, the community keeps telling me to RTFM in so many words](#Arch_requires_too_much_time_and_effort_to_install_and_use._Also.2C_the_community_keeps_telling_me_to_RTFM_in_so_many_words)
    *   [1.9 Is Arch designed to be used as a server? A desktop? A workstation?](#Is_Arch_designed_to_be_used_as_a_server.3F_A_desktop.3F_A_workstation.3F)
    *   [1.10 I really like Arch, except the development team needs to implement feature X](#I_really_like_Arch.2C_except_the_development_team_needs_to_implement_feature_X)
    *   [1.11 When will the new release be made available?](#When_will_the_new_release_be_made_available.3F)
    *   [1.12 Is Arch Linux a stable distribution? Will I get frequent breakage?](#Is_Arch_Linux_a_stable_distribution.3F_Will_I_get_frequent_breakage.3F)
    *   [1.13 Arch needs more press (i.e. advertisement)](#Arch_needs_more_press_.28i.e._advertisement.29)
    *   [1.14 Arch needs more developers](#Arch_needs_more_developers)
    *   [1.15 Why is my internet so slow compared to other operating systems?](#Why_is_my_internet_so_slow_compared_to_other_operating_systems.3F)
    *   [1.16 Why is Arch using all my RAM?](#Why_is_Arch_using_all_my_RAM.3F)
    *   [1.17 Where did all my free space go?](#Where_did_all_my_free_space_go.3F)
*   [2 Package Management](#Package_Management)
    *   [2.1 In which package is X?](#In_which_package_is_X.3F)
    *   [2.2 I've found an error with Package X. What should I do?](#I.27ve_found_an_error_with_Package_X._What_should_I_do.3F)
    *   [2.3 Arch packages need to use a unique naming convention. ".pkg.tar.gz" and ".pkg.tar.xz" are too long and/or confusing](#Arch_packages_need_to_use_a_unique_naming_convention._.22.pkg.tar.gz.22_and_.22.pkg.tar.xz.22_are_too_long_and.2For_confusing)
    *   [2.4 Pacman needs a library so other applications can easily access package information](#Pacman_needs_a_library_so_other_applications_can_easily_access_package_information)
    *   [2.5 Why doesn't pacman have an official GUI front-end?](#Why_doesn.27t_pacman_have_an_official_GUI_front-end.3F)
    *   [2.6 Pacman needs feature X!](#Pacman_needs_feature_X.21)
    *   [2.7 What is the difference between all these repositories?](#What_is_the_difference_between_all_these_repositories.3F)
    *   [2.8 I just installed Package X. How do I start it?](#I_just_installed_Package_X._How_do_I_start_it.3F)
    *   [2.9 Why is there only a single version of each shared library in the official repositories?](#Why_is_there_only_a_single_version_of_each_shared_library_in_the_official_repositories.3F)
    *   [2.10 What if I run a full system upgrade and there will be an update for a shared library, but not for the apps that depend on it?](#What_if_I_run_a_full_system_upgrade_and_there_will_be_an_update_for_a_shared_library.2C_but_not_for_the_apps_that_depend_on_it.3F)
    *   [2.11 Is it possible that there's a major kernel update in the repository, and that some of the driver packages haven't been updated?](#Is_it_possible_that_there.27s_a_major_kernel_update_in_the_repository.2C_and_that_some_of_the_driver_packages_haven.27t_been_updated.3F)
    *   [2.12 Does Arch use package signing?](#Does_Arch_use_package_signing.3F)
    *   [2.13 What to do before upgrading?](#What_to_do_before_upgrading.3F)
    *   [2.14 A package update was released, but pacman says the system is up to date](#A_package_update_was_released.2C_but_pacman_says_the_system_is_up_to_date)
*   [3 Installation](#Installation)
    *   [3.1 Arch needs an installer. Maybe a GUI installer?](#Arch_needs_an_installer._Maybe_a_GUI_installer.3F)
    *   [3.2 I installed Arch, and now I am at a shell! What now?](#I_installed_Arch.2C_and_now_I_am_at_a_shell.21_What_now.3F)
    *   [3.3 Which desktop environment or window manager should I use?](#Which_desktop_environment_or_window_manager_should_I_use.3F)
    *   [3.4 What makes Arch unique amongst other "minimal" distributions?](#What_makes_Arch_unique_amongst_other_.22minimal.22_distributions.3F)

## General

### What is Arch Linux?

See the article entitled [Arch Linux](/index.php/Arch_Linux "Arch Linux").

### Why would I want to use Arch?

If, after reading about the [The Arch Way](/index.php/The_Arch_Way "The Arch Way") philosophy, you wish to embrace the 'do-it-yourself' approach and require or desire a simple, elegant, highly customizable, bleeding edge, general purpose GNU/Linux distribution, you may like Arch.

### Why would I not want to use Arch?

You may **not** want to use Arch, if:

*   after reading [The Arch Way](/index.php/The_Arch_Way "The Arch Way"), you disagree with the philosophy.
*   you do not have the ability/time/desire for a 'do-it-yourself' GNU/Linux distribution.
*   you require support for an architecture other than x86_64 or i686.
*   you take a strong stand on using a distribution which only provides free software as defined by GNU.
*   you believe an operating system should configure itself, run out of the box, and include a complete default set of software and desktop environment on the installation media.
*   you do not want a bleeding edge, rolling release GNU/Linux distribution.
*   you are happy with your current OS.
*   you want an OS that targets a different userbase.

### What distribution is Arch based on?

Arch is independently developed, was built from scratch and is not based on any other GNU/Linux distribution. Before creating Arch, Judd Vinet admired and used CRUX, a great, minimalist distribution created by Per Lidén. Originally inspired by ideas in common with CRUX, Arch was built from scratch, and pacman was then coded in C.

### What architectures does Arch support?

Arch supports the i686 and x86_64 (sometimes called amd64) architectures.

### Does Arch support ARM CPUs?

No, but the [Arch Linux ARM](http://archlinuxarm.org/) project provides a port of Arch Linux to several ARM platforms.

### I am a complete GNU/Linux beginner. Should I use Arch?

This question has had much debate. Arch is targeted more towards advanced GNU/Linux users, but some people feel that Arch is a good place to start for the motivated novice. If you are a beginner and want to use Arch, just be warned that you must be willing to invest significant time into learning a new system, as well as accept the fact that Arch is fundamentally designed as a DIY (Do-It-Yourself) distribution. It is the user who assembles the system and controls what it will become. Before asking for help, do your own independent research by Googling, searching the forum (and reading the rest of these FAQs) and searching the superb documentation provided by the Arch Wiki. _There is a reason these resources were made available to you in the first place._ Many thousands of _volunteered_ hours have been spent compiling this excellent information.

Recommended reading: The Arch Linux [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide").

### Arch requires too much time and effort to install and use. Also, the community keeps telling me to RTFM in so many words

Arch is designed for and used by a specifically targeted user base. Perhaps it is not right for you. See [above](#I_am_a_complete_GNU.2FLinux_beginner._Should_I_use_Arch.3F).

### Is Arch designed to be used as a server? A desktop? A workstation?

Arch is not designed for any particular type of use. Rather, it is designed for a particular type of _user_. Arch targets competent users who enjoy its do-it-yourself nature, and who further exploit it to shape the system to fit their unique needs. Therefore, in the hands of its target user base, Arch can be used for virtually any purpose. Many use Arch on both their desktops and workstations. And of course, archlinux.org runs on Arch.

### I really like Arch, except the development team needs to implement feature X

Before going further, did you read [The Arch Way](/index.php/The_Arch_Way "The Arch Way")? Have you provided the feature/solution? Does it conform to the Arch philosophy of _minimalism_ and _code-correctness over convenience_? Get involved, contribute your code/solution to the community. If it is well regarded by the community and development team, perhaps it will be merged. The Arch community thrives on contribution and sharing of code and tools.

### When will the new release be made available?

Arch Linux releases are simply a live environment for installation or rescue, which include the [base](https://www.archlinux.org/groups/x86_64/base/) group and a few [other packages](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both). The releases are issued usually in the first half of every month.

The rolling release model keeps every Arch Linux system current and on the bleeding edge by issuing one command. For this reason, releases are not terribly important in Arch, because they become out of date as soon as a package has been updated. If you are looking to obtain the latest Arch Linux release, you do not need to reinstall. Simply run the `pacman -Syu` command, and your system will be identical to what you would get with a brand-new install. For this same reason, new Arch Linux releases are not typically full of new and exciting features. New and exciting features are released as needed with the packages that are updated, and can be obtained immediately via `pacman -Syu`.

### Is Arch Linux a stable distribution? Will I get frequent breakage?

The short answer is: It is largely as stable as _you_ make it.

_You_ assemble your own Arch system, atop the simple base environment, and _you_ control system upgrades. Obviously, a larger, more complicated system incorporating multitudes of customized packages, and a plethora of toolkits and desktop environments would be more likely to experience configuration problems due to upstream changes than a slimmer, more simple system would. Arch is targeted at capable, proactive users. General UNIX competence and good system maintenance and upgrade practices also play a large role in system stability. Also recall that Arch packages are predominantly unpatched, so most application problems are inherently upstream.

Therefore, it is _the user_ who is ultimately responsible for the stability of his own rolling release system. The user decides when to upgrade, and merges necessary changes when required. If the user reaches out to the community for help, it is often provided in a timely manner. The difference between Arch and other distributions in this regard is that Arch is truly a 'do-it-yourself' distribution; complaints of breakage are misguided and unproductive, since upstream changes are not the responsibility of Arch devs.

See the [System maintenance](/index.php/System_maintenance "System maintenance") article for tips on how to make an Arch Linux system as stable as possible.

### Arch needs more press (i.e. advertisement)

Arch gets plenty of press as it is. The goal of Arch Linux is not to be large, but rather, to provide an elegant, minimalist and bleeding edge distribution focused on simplicity and code-correctness. Organic, sustainable growth occurs naturally amongst the target user base.

### Arch needs more developers

Possibly so. Feel free to volunteer your time! Visit the [forums](https://bbs.archlinux.org), [IRC channels](/index.php/IRC_channel "IRC channel"), and [mailing lists](https://mailman.archlinux.org/mailman/listinfo/), and see what needs to be done. Getting involved in the Community Contributions subforum is a good way to start.

### Why is my internet so slow compared to other operating systems?

Is your network configured correctly? Have a look at [Hostname](/index.php/Beginners%27_guide#Hostname "Beginners' guide") and [Configure the network](/index.php/Beginners%27_guide#Configure_the_network "Beginners' guide") from the Beginners' Guide.

Also note that Arch Linux does not come with [traffic shaping](https://en.wikipedia.org/wiki/Traffic_shaping "wikipedia:Traffic shaping") enabled. Thus, it is possible that if a program on it somehow utilizes your internet connection to the full – regardless if it's over P2P or classic client-server connections – other local ones will find it clogged, resulting in severe lags and timeouts. Relief can be provided by [firewalls](/index.php/Firewalls "Firewalls") such as Shorewall or Vuurmuur; there are also static scripts for [iproute2](https://www.archlinux.org/packages/?name=iproute2) (such as [this derivative](http://serendipity.ruwenzori.net/index.php/2008/06/01/modified-wondershaper-for-better-voip-qos) of Wondershaper), which allow shaping on the network layer.

### Why is Arch using all my RAM?

Essentially, unused RAM is wasted RAM.

Many new users notice how the Linux kernel handles memory differently than they are used to. Since accessing data from RAM is much faster than from a storage drive, the kernel caches recently accessed data in memory. The cached data is only cleared when the system begins to run out of available memory and new data needs to be loaded.

We could distinguish the difference from `free` command:

 `$ free -h` 

```
              total        used        free      shared  buff/cache   available
Mem:           2.8G        1.1G        283M        224M        1.4G        1.2G
Swap:          3.0G        881M        2.1G

```

It is important to note the difference between "free" and "available" memory. In the above example, a laptop with 2.8G of total RAM appears to be using most of it, with only 283M as free memory. However, 1.4G of it is "buff/cache". There is still 1.2G available for starting new applications, without swapping. See `man free(1)` for detail. The result of all this? Performance!

See [this wonderful article](http://www.linuxjournal.com/article/2770) if your curiosity has been piqued! There's also a website dedicated to clearing this confusion: [http://www.linuxatemyram.com/](http://www.linuxatemyram.com/)

### Where did all my free space go?

The answer to this question depends on your system. There are some [fine utilities](/index.php/List_of_applications#Disk_usage_display "List of applications") that may help you find the answer.

## Package Management

### In which package is X?

You can find out with [pkgfile](/index.php/Pkgfile "Pkgfile").

For example:

```
$ pkgfile _file_name_

```

### I've found an error with Package X. What should I do?

First, you need to figure out if this error is something the Arch team can fix. Sometimes it's not (e.g. Firefox crashes may be the fault of the Mozilla team); this is called an _upstream error_. If it is an Arch problem, there is a series of steps you can take:

1.  Search the forums for information. See if anyone else has noticed it.
2.  Post a [bug report](/index.php/Bug_report "Bug report") with detailed information at [https://bugs.archlinux.org](https://bugs.archlinux.org).
3.  If you'd like, write a forum post detailing the problem and the fact that you have reported it already. This will help prevent a lot of people from reporting the same error.

### Arch packages need to use a unique naming convention. ".pkg.tar.gz" and ".pkg.tar.xz" are too long and/or confusing

This has been discussed on the Arch mailing list. Some proposed a `.pac` file extension. As far as is currently known, there is no plan to change the package extension. As Tobias Kieslich, one of the Arch devs, put it, "_A package **is** a gzipped_ [xz] _tarball! And it can be opened, investigated and manipulated by any tar-capable application. Moreover, the mime-type is automatically detected correctly by most applications._"

### Pacman needs a library so other applications can easily access package information

Since version 3.0.0, pacman has been the front-end to libalpm, the "Arch Linux Package Management" library. This library allows alternative front-ends to be written (for instance, a GUI front-end).

### Why doesn't pacman have an official GUI front-end?

Please read [The Arch Way](/index.php/The_Arch_Way "The Arch Way") and [Arch Linux](/index.php/Arch_Linux "Arch Linux"). Basically, the answer is that the Arch dev team will not be providing one. Feel free to use one developed by other users. A selective list can be found in [Pacman GUI Frontends](/index.php/Pacman_GUI_Frontends "Pacman GUI Frontends").

### Pacman needs feature X!

Please read [The Arch Way](/index.php/The_Arch_Way "The Arch Way") and [Arch Linux](/index.php/Arch_Linux "Arch Linux"). The Arch philosophy is "Keep It Simple". If you think the idea has merit, and does not violate this simple litany, then you may choose to discuss it on the forum [here](https://bbs.archlinux.org/). You might also like to check [here](https://bugs.archlinux.org); it is a place for feature requests if you find it is important.

However, the best way to get a feature added to pacman or Arch Linux is to implement it yourself. The patch or code may or may not be officially accepted, but perhaps others will appreciate, test and contribute to your effort.

### What is the difference between all these repositories?

See [Official repositories](/index.php/Official_repositories "Official repositories").

### I just installed Package X. How do I start it?

If you're using a desktop environment like [KDE](/index.php/KDE "KDE") or [GNOME](/index.php/GNOME "GNOME"), the program should automatically show up in your menu. If you're trying to run the program from a terminal and do not know the binary name, use:

```
$ pacman -Qlq _package_name_ | grep /usr/bin/

```

### Why is there only a single version of each shared library in the official repositories?

Several distributions, such as Debian, have different versions of shared libraries packaged as different packages: `libfoo1`, `libfoo2`, `libfoo3` and so on. In this way it is possible to have apps compiled against different versions of `libfoo` installed on the same system.

Unlike Debian, Arch is a rolling-release cutting-edge distribution. The most visible trait of a cutting-edge distribution is availability of the latest versions of software in the repositories; in case of a distribution like Arch, it also means that only the latest versions of all packages are officially supported. By dropping support for outdated software, package maintainers are able to spend more time ensuring that the newest versions work as expected. As soon as a new version of a shared library becomes available from upstream, it is added to the repositories and affected packages are rebuilt to utilize the new version.

### What if I run a full system upgrade and there will be an update for a shared library, but not for the apps that depend on it?

This scenario should not happen at all. Assuming an application called `foobaz` is in one of the official repositories and builds successfully against a new version of a shared library called `libbaz`, it will be updated along with `libbaz`. If, however, it doesn't build successfully, `foobaz` package will have a versioned dependency (e.g. _libbaz 1.5_), and will be removed by pacman during `libbaz` upgrade, due to a conflict.

If `foobaz` is a package that you built yourself and installed from AUR, you should try rebuilding `foobaz` against the new version of `libbaz`. If the build fails, report the bug to the `foobaz` developers.

### Is it possible that there's a major kernel update in the repository, and that some of the driver packages haven't been updated?

No, it is not possible. Major kernel updates (e.g. _linux 3.5.0-1_ to _linux 3.6.0-1_) are always accompanied by rebuilds of all supported kernel driver packages. On the other hand, if you have an unsupported driver package installed on your system, such as [catalyst](https://aur.archlinux.org/packages/catalyst/)<sup><small>AUR</small></sup>, then a kernel update might break things for you if you do not rebuild it for the new kernel. Users are responsible for updating any unsupported driver packages that they have installed.

### Does Arch use package signing?

Yes. Package signing in [pacman](/index.php/Pacman "Pacman") has been implemented since version 4\. See [package signing](/index.php/Package_signing "Package signing") for more information.

### What to do before upgrading?

It is important in Arch Linux, before upgrading to "Check the front page [Arch news](https://www.archlinux.org/), [Announcement lists](https://mailman.archlinux.org/mailman/listinfo/arch-announce/), and optionally the [forum](https://bbs.archlinux.org/) and [Mailing Lists](https://mailman.archlinux.org/mailman/listinfo/), before hitting enter." Any special instructions will be posted there. See also [System maintenance#Upgrading the system](/index.php/System_maintenance#Upgrading_the_system "System maintenance").

### A package update was released, but pacman says the system is up to date

_pacman_ mirrors are not synced immediately. It may take over 24 hours before an update is available to you. The only options are be patient or use another mirror. [MirrorStatus](https://www.archlinux.org/mirrors/status/) can help you identify an up-to-date mirror.

## Installation

### Arch needs an installer. Maybe a GUI installer?

Since installation doesn't occur often (read the rest of this article to know more about what _rolling release_ means), it is not a high priority for developers or users. The [Installation guide](/index.php/Installation_guide "Installation guide") and [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") have been fully updated to use the command-line method. If you're still interested in using an installer, consider using [Archboot](/index.php/Archboot "Archboot").

### I installed Arch, and now I am at a shell! What now?

Have a look at the Arch Linux [Beginners' guide#Post-installation](/index.php/Beginners%27_guide#Post-installation "Beginners' guide").

### Which desktop environment or window manager should I use?

Since many are available to you, use the one you like the most to fit your needs. Have a look at the [Desktop environment](/index.php/Desktop_environment "Desktop environment") and [Window manager](/index.php/Window_manager "Window manager") articles.

### What makes Arch unique amongst other "minimal" distributions?

Some distributions may provide minimal installation methods, sharing some similarities to the Arch installation process. However, a few points must be noted:

1.  Arch has been _fundamentally designed_ as a lightweight, minimal base environment upon which to build.
2.  The _only_ way to install Arch is by building up from this minimal base.
3.  The base system and the entire distribution are inherently a K.I.S.S. design approach, which makes it uniquely suitable for its target base of users.
4.  Installing services and packages requires manual, interactive user configuration. Unlike other distributions which automatically configure services and startup behavior, the Arch philosophy puts emphasis on the power user's competence and prerogative to handle such responsibilities.
5.  Arch packaging is designed to be minimal, and _optional_ package dependencies are never automatically installed. Rather, the user is simply notified of their existence during package installation, resulting in a slimmer system.
6.  Arch provides excellent, thorough documentation, aiding in the process of system assembly.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Frequently_asked_questions&oldid=406312](https://wiki.archlinux.org/index.php?title=Frequently_asked_questions&oldid=406312)"