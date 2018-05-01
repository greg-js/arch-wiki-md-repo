Related articles

*   [Arch terminology](/index.php/Arch_terminology "Arch terminology")
*   [Arch User Repository#FAQ](/index.php/Arch_User_Repository#FAQ "Arch User Repository")
*   [General troubleshooting](/index.php/General_troubleshooting "General troubleshooting")

## Contents

*   [1 Általános](#.C3.81ltal.C3.A1nos)
    *   [1.1 Mi az az Arch Linux?](#Mi_az_az_Arch_Linux.3F)
    *   [1.2 Miért nem szeretném az Archot használni?](#Mi.C3.A9rt_nem_szeretn.C3.A9m_az_Archot_haszn.C3.A1lni.3F)
    *   [1.3 Milyen architektúrákat támogat az Arch?](#Milyen_architekt.C3.BAr.C3.A1kat_t.C3.A1mogat_az_Arch.3F)
    *   [1.4 Támogat az Arch ARM processzorokat?](#T.C3.A1mogat_az_Arch_ARM_processzorokat.3F)
    *   [1.5 Az Arch követi a Linux Alapítvány(Linux Foundation) Fájlrendszer Hierarchia Szabványát (FHS)?](#Az_Arch_k.C3.B6veti_a_Linux_Alap.C3.ADtv.C3.A1ny.28Linux_Foundation.29_F.C3.A1jlrendszer_Hierarchia_Szabv.C3.A1ny.C3.A1t_.28FHS.29.3F)
    *   [1.6 I am a complete GNU/Linux beginner. Should I use Arch?](#I_am_a_complete_GNU.2FLinux_beginner._Should_I_use_Arch.3F)
    *   [1.7 Is Arch designed to be used as a server? A desktop? A workstation?](#Is_Arch_designed_to_be_used_as_a_server.3F_A_desktop.3F_A_workstation.3F)
    *   [1.8 I really like Arch, except the development team needs to implement feature X](#I_really_like_Arch.2C_except_the_development_team_needs_to_implement_feature_X)
    *   [1.9 When will the new release be made available?](#When_will_the_new_release_be_made_available.3F)
    *   [1.10 Is Arch Linux a stable distribution? Will I get frequent breakage?](#Is_Arch_Linux_a_stable_distribution.3F_Will_I_get_frequent_breakage.3F)
    *   [1.11 Arch needs more press (i.e. advertisement)](#Arch_needs_more_press_.28i.e._advertisement.29)
    *   [1.12 Arch needs more developers](#Arch_needs_more_developers)
    *   [1.13 Why is my internet so slow compared to other operating systems?](#Why_is_my_internet_so_slow_compared_to_other_operating_systems.3F)
    *   [1.14 Why is Arch using all my RAM?](#Why_is_Arch_using_all_my_RAM.3F)
    *   [1.15 Where did all my free space go?](#Where_did_all_my_free_space_go.3F)
*   [2 Package management](#Package_management)
    *   [2.1 I have found an error with Package X. What should I do?](#I_have_found_an_error_with_Package_X._What_should_I_do.3F)
    *   [2.2 Arch packages need to use a unique naming convention. ".pkg.tar.gz" and ".pkg.tar.xz" are too long and/or confusing](#Arch_packages_need_to_use_a_unique_naming_convention._.22.pkg.tar.gz.22_and_.22.pkg.tar.xz.22_are_too_long_and.2For_confusing)
    *   [2.3 Pacman needs a library so other applications can easily access package information](#Pacman_needs_a_library_so_other_applications_can_easily_access_package_information)
    *   [2.4 Pacman needs feature X!](#Pacman_needs_feature_X.21)
    *   [2.5 I just installed Package X. How do I start it?](#I_just_installed_Package_X._How_do_I_start_it.3F)
    *   [2.6 Why is there only a single version of each shared library in the official repositories?](#Why_is_there_only_a_single_version_of_each_shared_library_in_the_official_repositories.3F)
    *   [2.7 What if I run a full system upgrade and there will be an update for a shared library, but not for the apps that depend on it?](#What_if_I_run_a_full_system_upgrade_and_there_will_be_an_update_for_a_shared_library.2C_but_not_for_the_apps_that_depend_on_it.3F)
    *   [2.8 Is it possible that there is a major kernel update in the repository, and that some of the driver packages have not been updated?](#Is_it_possible_that_there_is_a_major_kernel_update_in_the_repository.2C_and_that_some_of_the_driver_packages_have_not_been_updated.3F)
    *   [2.9 What to do before upgrading?](#What_to_do_before_upgrading.3F)
    *   [2.10 A package update was released, but pacman says the system is up to date](#A_package_update_was_released.2C_but_pacman_says_the_system_is_up_to_date)
    *   [2.11 Upstream project *X* has released a new version. How long will it take for the Arch package to update to that new version?](#Upstream_project_X_has_released_a_new_version._How_long_will_it_take_for_the_Arch_package_to_update_to_that_new_version.3F)
*   [3 Installation](#Installation)
    *   [3.1 Arch needs an installer. Maybe a GUI installer?](#Arch_needs_an_installer._Maybe_a_GUI_installer.3F)
    *   [3.2 I installed Arch, and now I am at a shell! What now?](#I_installed_Arch.2C_and_now_I_am_at_a_shell.21_What_now.3F)
    *   [3.3 Which desktop environment or window manager should I use?](#Which_desktop_environment_or_window_manager_should_I_use.3F)
    *   [3.4 What makes Arch unique amongst other "minimal" distributions?](#What_makes_Arch_unique_amongst_other_.22minimal.22_distributions.3F)
*   [4 64-bit](#64-bit)
    *   [4.1 How do I determine if my processor is x86_64 compatible?](#How_do_I_determine_if_my_processor_is_x86_64_compatible.3F)
    *   [4.2 Why 64-bit?](#Why_64-bit.3F)
    *   [4.3 Válthatok i686-ról x86_64-re újratelepítés nélkül?](#V.C3.A1lthatok_i686-r.C3.B3l_x86_64-re_.C3.BAjratelep.C3.ADt.C3.A9s_n.C3.A9lk.C3.BCl.3F)

## Általános

### Mi az az Arch Linux?

Lásd az [Arch Linux](/index.php/Arch_Linux "Arch Linux") cikket.

### Miért nem szeretném az Archot használni?

**Nem** szeretnéd az Archot használni, ha:

*   nincs meg a készséged/időd/vágyad egy 'csináld magad' GNU/Linux disztribúcióra.
*   szükséged van olyan architektúra támogatására a x86_64 helyett.
*   erősen alapozol egy olyan disztribúció használatán ami csak ingyenes szoftvert szolgáltat a GNU-ban foglaltak szerint.
*   azt hiszed, hogy az operációs rendszer önmagát beállítja, fusson már az első bekapcsoláskor, és tartalmazzon egy alapértelmezett szoftver készletet és asztali környezetet a telepítő eszközön.
*   nem akarsz egy folyton frissülő GNU/Linux disztribúciót.
*   boldog vagy a jelenlegi rendszereddel.

### Milyen architektúrákat támogat az Arch?

Az Arch csak az x86_64-es (néha amd64-nek nevezett) architektúrát. Az i686-os támogatás még 2017 novemberében megszűnt[[1]](https://www.archlinux.org/news/the-end-of-i686-support/)Ha a géped még mindig az i686-as verzióját futtatja az Archnak de van x86_64-es processzora, lásd a [#Válthatok i686-ról x86_64-re újratelepítés nélkül?](#V.C3.A1lthatok_i686-r.C3.B3l_x86_64-re_.C3.BAjratelep.C3.ADt.C3.A9s_n.C3.A9lk.C3.BCl.3F) pontot. Ha a géped nem képes rá, akkor válts a [Arch Linux 32](https://archlinux32.org/)-re.

### Támogat az Arch ARM processzorokat?

Nem, de a [Arch Linux ARM](http://archlinuxarm.org/) projekt kínál egy portot néhány ARM plaformra. Lásd: [[2]](http://ix.io/73w/irc).

### Az Arch követi a Linux Alapítvány(Linux Foundation) Fájlrendszer Hierarchia Szabványát (FHS)?

Az Arch Linux követi a *fájlrendszer hierarchiát* operációs rendszereknek a [systemd](/index.php/Systemd "Systemd") szolgáltatás kezelőt használva. Lásd a [file-hierarchy(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/file-hierarchy.7)-t magyarázatért minden egyes könyvtárnak a jelölésükkel. Különösen a `/bin`, `/sbin`, és a `/usr/sbin` szimbolikus linkek a `/usr/bin`-nek, és a `/lib` és a `/lib64` szimbolikus linkek a `/usr/lib`-hez.

### I am a complete GNU/Linux beginner. Should I use Arch?

If you are a beginner and want to use Arch, you must be willing to invest time into learning a new system, and accept that Arch is designed as a DIY (Do-It-Yourself) distribution; it is the user who assembles the system.

Before asking for help, do your own independent research by Googling, searching the forum and the superb documentation provided by the Arch Wiki. *There is a reason these resources were made available to you in the first place.* Many thousands of *volunteered* hours have been spent compiling this excellent information.

See also [Arch terminology#RTFM](/index.php/Arch_terminology#RTFM "Arch terminology") and the [Installation guide](/index.php/Installation_guide "Installation guide").

### Is Arch designed to be used as a server? A desktop? A workstation?

Arch is not designed for any particular type of use. Rather, it is designed for a particular type of *user*. Arch targets competent users who enjoy its do-it-yourself nature, and who further exploit it to shape the system to fit their unique needs. Therefore, in the hands of its target user base, Arch can be used for virtually any purpose. Many use Arch on both their desktops and workstations. And of course, archlinux.org runs on Arch.

### I really like Arch, except the development team needs to implement feature X

Get involved, contribute your code/solution to the community. If it is well regarded by the community and development team, perhaps it will be merged. The Arch community thrives on contribution and sharing of code and tools.

### When will the new release be made available?

Arch Linux releases are simply a live environment for installation or rescue, which include the [base](https://www.archlinux.org/groups/x86_64/base/) group and a few [other packages](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both). The releases are issued usually in the first half of every month.

### Is Arch Linux a stable distribution? Will I get frequent breakage?

It is *the user* who is ultimately responsible for the stability of his own rolling release system. The user decides when to upgrade, and merges necessary changes when required. If the user reaches out to the community for help, it is often provided in a timely manner. The difference between Arch and other distributions in this regard is that Arch is truly a 'do-it-yourself' distribution; complaints of breakage are misguided and unproductive, since upstream changes are not the responsibility of Arch devs.

See the [System maintenance](/index.php/System_maintenance "System maintenance") article for tips on how to make an Arch Linux system as stable as possible.

### Arch needs more press (i.e. advertisement)

Arch gets plenty of press as it is. The goal of Arch Linux is not to be large; rather, organic, sustainable growth occurs naturally amongst the target user base.

### Arch needs more developers

Possibly so. Feel free to volunteer your time! Visit the [forums](https://bbs.archlinux.org), [IRC channels](/index.php/IRC_channels "IRC channels"), and [mailing lists](https://mailman.archlinux.org/mailman/listinfo/), and see what needs to be done. Getting involved in the Community Contributions subforum is a good way to start.

### Why is my internet so slow compared to other operating systems?

Is your network configured correctly? Have a look at the [Network configuration](/index.php/Network_configuration "Network configuration") article.

Also note that Arch Linux does not come with [traffic shaping](https://en.wikipedia.org/wiki/Traffic_shaping "wikipedia:Traffic shaping") enabled. Thus, it is possible that if a program on it somehow utilizes your internet connection to the full – regardless if it is over P2P or classic client-server connections – other local ones will find it clogged, resulting in severe lags and timeouts. Relief can be provided by [firewalls](/index.php/Firewalls "Firewalls") such as Shorewall or Vuurmuur; there are also static scripts for [iproute2](https://www.archlinux.org/packages/?name=iproute2) (such as [this derivative](http://serendipity.ruwenzori.net/index.php/2008/06/01/modified-wondershaper-for-better-voip-qos) of Wondershaper), which allow shaping on the network layer.

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

See [this wonderful article](http://www.linuxjournal.com/article/2770) if your curiosity has been piqued! There is also a website dedicated to clearing this confusion: [http://www.linuxatemyram.com/](http://www.linuxatemyram.com/)

### Where did all my free space go?

The answer to this question depends on your system. There are some [fine utilities](/index.php/List_of_applications#Disk_usage_display "List of applications") that may help you find the answer.

## Package management

See the [pacman](/index.php/Pacman "Pacman"), [pacman/Tips and tricks](/index.php/Pacman/Tips_and_tricks "Pacman/Tips and tricks") and [Official repositories](/index.php/Official_repositories "Official repositories") pages for more answers.

### I have found an error with Package X. What should I do?

First, you need to figure out if this error is something the Arch team can fix. Sometimes it is not (e.g. Firefox crashes may be the fault of the Mozilla team); this is called an *upstream error*. If it is an Arch problem, there is a series of steps you can take:

1.  Search the forums for information. See if anyone else has noticed it.
2.  Post a [bug report](/index.php/Bug_report "Bug report") with detailed information at [https://bugs.archlinux.org](https://bugs.archlinux.org).
3.  If you would like, write a forum post detailing the problem and the fact that you have reported it already. This will help prevent a lot of people from reporting the same error.

### Arch packages need to use a unique naming convention. ".pkg.tar.gz" and ".pkg.tar.xz" are too long and/or confusing

This has been discussed on the Arch mailing list. Some proposed a *.pac* file extension, but there is no plan to change the package extension. As Tobias Kieslich, one of the Arch developers, put it, "A package **is** a gzipped *[xz]* tarball! And it can be opened, investigated and manipulated by any tar-capable application. Moreover, the mime-type is automatically detected correctly by most applications."

### Pacman needs a library so other applications can easily access package information

Pacman is a front-end to [libalpm](https://www.archlinux.org/pacman/libalpm.3.html)—the "Arch Linux Package Management" library—which allows alternative front-ends, like a GUI front-end, to be written.

### Pacman needs feature X!

If you think an idea has merit, you may choose to discuss it on [pacman-dev](https://lists.archlinux.org//listinfo/pacman-dev/). Also check [https://bugs.archlinux.org](https://bugs.archlinux.org) for existing feature requests.

However, the best way to get a feature added to pacman or Arch Linux is to implement it yourself. The patch or code may or may not be officially accepted, but perhaps others will appreciate, test and contribute to your effort.

### I just installed Package X. How do I start it?

If you are using a desktop environment like [KDE](/index.php/KDE "KDE") or [GNOME](/index.php/GNOME "GNOME"), the program should automatically show up in your menu. If you are trying to run the program from a terminal and do not know the binary name, use:

```
$ pacman -Qlq *package_name* | grep /usr/bin/

```

### Why is there only a single version of each shared library in the official repositories?

Several distributions, such as Debian, have different versions of shared libraries packaged as different packages: `libfoo1`, `libfoo2`, `libfoo3` and so on. In this way it is possible to have applications compiled against different versions of `libfoo` installed on the same system.

In case of a distribution like Arch, only the latest stable versions of packages are officially supported. By dropping support for outdated software, package maintainers are able to spend more time ensuring that the newest versions work as expected. As soon as a new version of a shared library becomes available from upstream, it is added to the repositories and affected packages are rebuilt to use the new version.

### What if I run a full system upgrade and there will be an update for a shared library, but not for the apps that depend on it?

This scenario should not happen at all. Assuming an application called `foobaz` is in one of the official repositories and builds successfully against a new version of a shared library called `libbaz`, it will be updated along with `libbaz`. If, however, it does not build successfully, `foobaz` package will have a versioned dependency (e.g. *libbaz 1.5*), and will be removed by pacman during `libbaz` upgrade, due to a conflict.

If `foobaz` is a package that you built yourself and installed from AUR, you should try rebuilding `foobaz` against the new version of `libbaz`. If the build fails, report the bug to the `foobaz` developers.

### Is it possible that there is a major kernel update in the repository, and that some of the driver packages have not been updated?

No, it is not possible. Major kernel updates (e.g. *linux 3.5.0-1* to *linux 3.6.0-1*) are always accompanied by rebuilds of all supported kernel driver packages. On the other hand, if you have an unsupported driver package installed on your system, such as [catalyst](https://aur.archlinux.org/packages/catalyst/), then a kernel update might break things for you if you do not rebuild it for the new kernel. Users are responsible for updating any unsupported driver packages that they have installed.

### What to do before upgrading?

Follow the [System maintenance#Upgrading the system](/index.php/System_maintenance#Upgrading_the_system "System maintenance") section.

### A package update was released, but pacman says the system is up to date

*pacman* mirrors are not synced immediately. It may take over 24 hours before an update is available to you. The only options are be patient or use another mirror. [MirrorStatus](https://www.archlinux.org/mirrors/status/) can help you identify an up-to-date mirror.

### Upstream project *X* has released a new version. How long will it take for the Arch package to update to that new version?

Package updates will be released when they are ready. The specific amount of time can be as short as a few hours after upstream releases a minor bugfix update to as long as several weeks after a large package group's major update. The amount of time from an upstream's new version to Arch releasing a new package depends on the specific packages and the availability of the package maintainers. Additionally, some packages spend some time in the [testing](/index.php/Testing "Testing") repository, so this can prolong the time before a package is updated. [Package maintainers](/index.php/Package_maintainer "Package maintainer") attempt to work quickly to bring stable updates to the repositories. If you find a package in the official repositories that is out of date, go to that package's page at the [package website](https://www.archlinux.org/packages/) and flag it.

## Installation

### Arch needs an installer. Maybe a GUI installer?

Since installation does not occur often (read the rest of this article to know more about what *rolling release* means), it is not a high priority for developers or users. The [Installation guide](/index.php/Installation_guide "Installation guide") has been fully updated to use the command-line method.

### I installed Arch, and now I am at a shell! What now?

See [General recommendations](/index.php/General_recommendations "General recommendations").

### Which desktop environment or window manager should I use?

Since many are available to you, use the one you like the most to fit your needs. Have a look at the [Desktop environment](/index.php/Desktop_environment "Desktop environment") and [Window manager](/index.php/Window_manager "Window manager") articles.

### What makes Arch unique amongst other "minimal" distributions?

See [Arch compared to other distributions](/index.php/Arch_compared_to_other_distributions "Arch compared to other distributions").

## 64-bit

### How do I determine if my processor is x86_64 compatible?

If your processor is [x86_64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64") compatible, you will have the `lm` flag in `/proc/cpuinfo`. For example,

```
$ grep -w lm /proc/cpuinfo

```

Under Windows, using the freeware [CPU-Z](http://www.cpuid.com/cpuz.php) helps determine whether your CPU is 64-bit compatible. CPUs with AMD's instruction set "AMD64" or Intel's solution "EM64T" should be compatible with the x86_64 releases and binary packages.

### Why 64-bit?

It is faster under most circumstances and as an added bonus also inherently more secure due to the nature of [Address space layout randomization (ASLR)](https://en.wikipedia.org/wiki/Address_space_layout_randomization "wikipedia:Address space layout randomization") in combination with [Position-independent code (PIC)](https://en.wikipedia.org/wiki/Position-independent_code "wikipedia:Position-independent code") and the [NX Bit](https://en.wikipedia.org/wiki/NX_Bit "wikipedia:NX Bit") which is not available in the stock i686 kernel due to disabled PAE. If your computer has more than 4GB of RAM, only a 64-bit OS will be able to fully utilize it.

Programmers also increasingly tend to care less about 32-bit ("legacy") as "new" x86 CPUs typically support the 64-bit extensions.

There are many more reasons we could list here to tell you to avoid 32-bit, but between the kernel, userspace and individual programs it is simply not viable to list every last thing that 64-bit does much better these days.

### Válthatok i686-ról x86_64-re újratelepítés nélkül?

No. All packages need to be reinstalled for the new architecture and configuration changes may be necessary. However, you do not need to repartition or reformat your hard drives during installation, so it is possible to migrate all of your old data. A forum thread has been created [here](https://bbs.archlinux.org/viewtopic.php?id=64485) which outlines steps taken to migrate an install from 32 to 64 bit without losing any configurations/settings/data using a large external hard drive.

However, you can also start the system with the 64-bit installation ISO, mount the disk, backup anything you may want to keep that is not a 32-bit binary (e.g: `/home` & `/etc`), and install.

You may also want to read about [migrating between architectures](/index.php/Migrating_between_architectures "Migrating between architectures").