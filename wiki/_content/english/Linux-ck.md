Related articles

*   [Unofficial user repositories/Repo-ck](/index.php/Unofficial_user_repositories/Repo-ck "Unofficial user repositories/Repo-ck")
*   [Modprobed-db](/index.php/Modprobed-db "Modprobed-db")

## Contents

*   [1 General package details](#General_package_details)
    *   [1.1 Release cycle](#Release_cycle)
    *   [1.2 Long-Term Support (LTS) CK releases](#Long-Term_Support_(LTS)_CK_releases)
*   [2 Installation options](#Installation_options)
    *   [2.1 Compile the package from source](#Compile_the_package_from_source)
    *   [2.2 Use pre-compiled packages](#Use_pre-compiled_packages)
*   [3 How to enable the BFQ I/O Scheduler](#How_to_enable_the_BFQ_I/O_Scheduler)
*   [4 More about MuQSS](#More_about_MuQSS)
    *   [4.1 Check if MuQSS is enabled](#Check_if_MuQSS_is_enabled)
    *   [4.2 MuQSS patched kernels and systemd](#MuQSS_patched_kernels_and_systemd)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Silencing psi: task underflow message](#Silencing_psi:_task_underflow_message)
    *   [5.2 Running VirtualBox with Linux-ck](#Running_VirtualBox_with_Linux-ck)
        *   [5.2.1 Use the unofficial repo (recommended if Linux-ck is installed from Repo-ck)](#Use_the_unofficial_repo_(recommended_if_Linux-ck_is_installed_from_Repo-ck))
        *   [5.2.2 DKMS](#DKMS)
    *   [5.3 Downgrading](#Downgrading)
    *   [5.4 Forum support](#Forum_support)
*   [6 See also](#See_also)

## General package details

[Linux-ck](https://aur.archlinux.org/packages/Linux-ck/) is a package available both in [AUR](/index.php/AUR "AUR") and in the [unofficial repo-ck repository](#Use_pre-compiled_packages) that allows users to run a kernel and headers setup patched with Con Kolivas' ck patchset[[1]](http://ck.kolivas.org/patches/), including a CPU scheduler named MuQSS (*Multiple Queue Skiplist Scheduler*, pronounced *mux*) which replaces Brain Fuck Scheduler (BFS), his previous work. Many Arch Linux users choose this kernel for its excellent desktop interactivity and responsiveness under any load situation.

CK patchset is designed for desktop/laptop use but not for servers. It provides low latency environment and works well for 16 CPUs or fewer.

### Release cycle

Linux-ck roughly follows the release cycle of the official Arch kernel but not only. The following are requirements for a new package release:

*   CK patchset compatible with the current kernel version
*   corresponding Arch kernel must be in existence otherwise it will break other packages i.e. nvidia. See [git.archlinux.org](https://git.archlinux.org/svntogit/packages.git/log/trunk?h=packages/linux) for the official [linux](https://www.archlinux.org/packages/?name=linux) package

### Long-Term Support (LTS) CK releases

In addition to the [linux-ck](https://aur.archlinux.org/packages/linux-ck/) package, there are LTS kernel releases patched with the above patchsets as well and with the previously mentioned modifications:

*   [linux-lts-ck](https://aur.archlinux.org/packages/linux-lts-ck/) - The current Arch Linux LTS kernel patched with the CK patchset

**Note:** This package is maintained by vishwin, thus pre-compiled versions will not be present in the unofficial ck repo.

## Installation options

**Note:** As with *any* additional kernel, users need to manually update their [boot loader](/index.php/Boot_loader "Boot loader")'s configuration file in order to make it aware of the new kernel image.

Users have two options to get these kernel packages.

### Compile the package from source

The [AUR](/index.php/AUR "AUR") contains entries for both packages mentioned above.

Users can further customize the linux-ck package via tweaks contained in the PKGBUILD:

*   Optional **nconfig** for user specific tweaking.
*   Option to compile a minimal set of modules via a make **localmodconfig**.
*   Option to bypass the standard Arch config options and simply use the **current kernel configuration** file.
*   Optionally set the [BFQ I/O scheduler](http://algo.ing.unimo.it/people/paolo/disk_sched/) as default.

More details about these options are provided in the PKGBUILD itself. Be sure to read them carefully if compiling from AUR!

**Note:** There are the related PKGBUILDs in AUR for other common kernel modules. For example [nvidia-ck](https://aur.archlinux.org/packages/nvidia-ck/), [nvidia-340xx-ck](https://aur.archlinux.org/packages/nvidia-340xx-ck/), and [broadcom-wl-ck](https://aur.archlinux.org/packages/broadcom-wl-ck/) to name a few. Alternatively, use the corresponding [DKMS](/index.php/DKMS "DKMS") package, for instance install [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms) as described in [NVIDIA#Custom kernel](/index.php/NVIDIA#Custom_kernel "NVIDIA").

### Use pre-compiled packages

If user prefers to spend no time to compile on their own, the unofficial repo maintained by [graysky](/index.php/User:Graysky "User:Graysky") is available to the community. For details, see: [Unofficial user repositories/Repo-ck](/index.php/Unofficial_user_repositories/Repo-ck "Unofficial user repositories/Repo-ck").

## How to enable the BFQ I/O Scheduler

**Note:** Do not confuse MuQSS (Multiple Queue Skiplist Scheduler) with BFQ (Budget Fair Queueing). MuQSS is a CPU scheduler and is enabled by default whereas BFQ is an I/O scheduler and must explicitly be enabled in order to use it.

See the [Improving performance#Input/output schedulers](/index.php/Improving_performance#Input/output_schedulers "Improving performance") section for some background about the different IO schedulers and how to activate *BFQ*.

## More about MuQSS

See the [LKML announcement](https://lkml.org/lkml/2016/10/29/4) posted by CK.

### Check if MuQSS is enabled

This start-up message should appear in the kernel ring buffer when MuQSS in enabled:

```
$ dmesg | grep -i muqss
...
MuQSS CPU scheduler v0.120 by Con Kolivas.

```

### MuQSS patched kernels and systemd

It is a common mistake to think that MuQSS does not support *cgroups*. It does but not all the cgroup features (e.g. CPU limiting will not work).

## Troubleshooting

### Silencing psi: task underflow message

New in MuQSS v0.185 is support for [PSI](https://lwn.net/Articles/763629/) which [CK is characterizing](http://ck-hack.blogspot.com/2018/12/linux-420-ck1-muqss-version-0185-for.html?showComment=1546576441759#c2919535897335602087) as "completely untested and probably broken."

In response to this, some users may notice [psi: task underflow!](https://bbs.archlinux.org/viewtopic.php?pid=1824594#p1824594) in dmesg/journalctl output. With the release of 4.20.0-3-ck1, is compiled in but disabled by default. Users wanting PSI enabled should boot with the following [Kernel_parameter] on their respective bootloader config: **psi=1**

### Running VirtualBox with Linux-ck

VirtualBox works just fine with custom kernels such as Linux-ck *without* the need to keep any of the official Arch kernel headers package on the system.

Do not forget to add users to the *vboxusers* group:

```
# gpasswd -a USERNAME vboxusers

```

#### Use the unofficial repo (recommended if Linux-ck is installed from Repo-ck)

**Note:** As of 17-Oct-2012, Repo-ck users can enjoy these modules as pre-compiled packages in the repo itself. If you build Linux-ck from AUR you **can not use the repo** as all packages in the repo are matched groups.

See the [Unofficial user repositories/Repo-ck](/index.php/Unofficial_user_repositories/Repo-ck "Unofficial user repositories/Repo-ck") to set up it correctly.

#### DKMS

Install **virtualbox** with the **virtualbox-host-dkms** package. Then setup DKMS as follows:

```
# pacman -S virtualbox virtualbox-host-dkms

```

### Downgrading

Users wishing to downgrade to a previous version of Linux-ck, have several options:

*   Source archives are [available](http://repo-ck.com/bench.htm) dating back to linux-ck-3.3.7-1.
*   [AUR.git](http://pkgbuild.com/git/aur-mirror.git/log/linux-ck) holds AUR git commits for Linux-ck, dating back to linux-ck-2.6.39.3-1.

### Forum support

Always feel free to open a thread in the forums for support purpose. Be sure to give the thread a descriptive title to draw attention to the fact that the post relates to the Linux-ck package.

There is also an [official thread](https://bbs.archlinux.org/viewtopic.php?id=111715) for Linux-ck.

## See also

*   [Kernel patch repository of Con Kolivas](http://ck.kolivas.org/patches/)
*   [Con Kolivas' Blog](http://ck-hack.blogspot.it/)
*   [Con Kolivas' first BFS announcement on the Linux Kernel Mailing List](http://lkml.org/lkml/2009/9/6/136)
*   [Wikipedia's Con Kolivas page](https://en.wikipedia.org/wiki/Con_Kolivas "wikipedia:Con Kolivas")
*   [Wikipedia's BFS article](https://en.wikipedia.org/wiki/Brain_Fuck_Scheduler "wikipedia:Brain Fuck Scheduler")