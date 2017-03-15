## Contents

*   [1 General package details](#General_package_details)
    *   [1.1 Release cycle](#Release_cycle)
    *   [1.2 Package defaults](#Package_defaults)
    *   [1.3 Long-Term Support (LTS) CK releases](#Long-Term_Support_.28LTS.29_CK_releases)
*   [2 Installation options](#Installation_options)
    *   [2.1 Compile the package from source](#Compile_the_package_from_source)
    *   [2.2 Use pre-compiled packages](#Use_pre-compiled_packages)
*   [3 How to enable the BFQ I/O Scheduler](#How_to_enable_the_BFQ_I.2FO_Scheduler)
    *   [3.1 Enable BFQ for all devices](#Enable_BFQ_for_all_devices)
    *   [3.2 Enable BFQ only for specific devices](#Enable_BFQ_only_for_specific_devices)
*   [4 More about MuQSS](#More_about_MuQSS)
    *   [4.1 Check if MuQSS is enabled](#Check_if_MuQSS_is_enabled)
    *   [4.2 MuQSS patched kernels and systemd](#MuQSS_patched_kernels_and_systemd)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Running VirtualBox with Linux-ck](#Running_VirtualBox_with_Linux-ck)
        *   [5.1.1 Use the unofficial repo (recommended if Linux-ck is installed from Repo-ck)](#Use_the_unofficial_repo_.28recommended_if_Linux-ck_is_installed_from_Repo-ck.29)
        *   [5.1.2 The virtualbox-ck-host-modules package (recommended if Linux-ck is built from AUR)](#The_virtualbox-ck-host-modules_package_.28recommended_if_Linux-ck_is_built_from_AUR.29)
        *   [5.1.3 Use DKMS (more complicated, recommended for LTS versions)](#Use_DKMS_.28more_complicated.2C_recommended_for_LTS_versions.29)
    *   [5.2 Downgrading](#Downgrading)
    *   [5.3 Forum support](#Forum_support)
*   [6 See also](#See_also)

## General package details

[Linux-ck](https://aur.archlinux.org/packages/Linux-ck/) is a package available both in [AUR](/index.php/AUR "AUR") and in the [unofficial repo-ck repository](#Use_pre-compiled_packages) that allows users to run a kernel and headers setup patched with Con Kolivas' ck patchset[[1]](http://users.tpg.com.au/ckolivas/kernel/), including MuQSS (Multiple Queue Skiplist Scheduler, pronounced *mux*) which replaces Brain Fuck Scheduler (BFS), his previous work. Many Arch Linux users choose this kernel for its excellent desktop interactivity and responsiveness under any load situation.

Ck patchset is designed for desktop/laptop use but not for servers. It provides low latency environment and works well for 16 CPUs or fewer.

### Release cycle

Linux-ck roughly follows the release cycle of the official ARCH kernel but not only. The following are requirements for a new package release:

*   CK patchset compatible with the current kernel version
*   corresponding ARCH kernel must be in existence otherwise it will break other packages i.e. nvidia. See [git.archlinux.org](https://git.archlinux.org/svntogit/packages.git/log/trunk?h=packages/linux) for the official [linux](https://www.archlinux.org/packages/?name=linux) package

### Package defaults

There are **three** modifications to the config files:

1.  The options that the CK patchset enable/disable.
2.  The tickrate is set to 100 Hz (CK's recommendation).
3.  The extra CPU types optionally available to compilation thanks to the [GCC patch](https://github.com/graysky2/kernel_gcc_patch).

**All other options are set to the ARCH defaults outlined in the main kernel's config files.** Of course users are free to edit them.

The [linux-ck](https://aur.archlinux.org/packages/linux-ck/) package contains an option to switch on the **nconfig** config editor (see the section [below](/index.php/Linux-ck#Compile_the_package_from_source "Linux-ck")).

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
*   Option to bypass the standard ARCH config options and simply use the **current kernel configuration** file.
*   Optionally set the [BFQ I/O scheduler](http://algo.ing.unimo.it/people/paolo/disk_sched/) as default.

More details about these options are provided in the PKGBUILD itself. Be sure to read them carefully if compiling from AUR!

**Note:** There are the related PKGBUILDs in AUR for other common kernel modules. For example [nvidia-ck](https://aur.archlinux.org/packages/nvidia-ck/), [nvidia-304xx-ck](https://aur.archlinux.org/packages/nvidia-304xx-ck/), [nvidia-340xx-ck](https://aur.archlinux.org/packages/nvidia-340xx-ck/), and [broadcom-wl-ck](https://aur.archlinux.org/packages/broadcom-wl-ck/) to name a few. Alternatively, use the corresponding [DKMS](/index.php/DKMS "DKMS") package, for instance install [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms) as described in [NVIDIA#Custom_kernel](/index.php/NVIDIA#Custom_kernel "NVIDIA").

### Use pre-compiled packages

If user prefers to spend no time to compile on their own, the unofficial repo maintained by [graysky](/index.php/User:Graysky "User:Graysky") is available to the community. For details, see: [Repo-ck](/index.php/Repo-ck "Repo-ck").

## How to enable the BFQ I/O Scheduler

**Note:** Do not confuse MuQSS (Multiple Queue Skiplist Scheduler) with BFQ (Budget Fair Queueing). MuQSS is a CPU scheduler and is enabled by default whereas BFQ is an I/O scheduler and must explicitly be enabled in order to use it.

Budget Fair Queueing is a disk scheduler which allows each process/thread to be assigned a portion of the disk throughput. Its creator shares the results of many benchmarks ([results](http://algo.ing.unimo.it/people/paolo/disk_sched/results.php) and [video](http://www.youtube.com/watch?v=KhZl9LjCKuU)) which show the latency performance improvement.

Due to CK's patchset defaults, BFQ is built into [linux-ck](/index.php/AUR "AUR") but the above-mentioned scheduler must be enabled manually. User has several options to do that.

### Enable BFQ for all devices

If compiling from the AUR, simply set the BFQ flag to "y" in the PKGBUILD prior to building

```
_BFQ_enable_="y"

```

Users of [repo-ck](/index.php/Repo-ck "Repo-ck") or those who have not modified the PKGBUILD prior to compile the package can append `elevator=bfq` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

### Enable BFQ only for specific devices

An alternative method is to instruct the kernel at runtime to use BFQ on a device-by-device basis. For configuration examples see the [Improving performance#Tuning IO schedulers](/index.php/Improving_performance#Tuning_IO_schedulers "Improving performance") section.

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

### Running VirtualBox with Linux-ck

VirtualBox works just fine with custom kernels such as Linux-ck *without* the need to keep any of the official ARCH kernel headers package on the system.

Do not forget to add users to the *vboxusers* group:

```
# gpasswd -a USERNAME vboxusers

```

#### Use the unofficial repo (recommended if Linux-ck is installed from Repo-ck)

**Note:** As of 17-Oct-2012, Repo-ck users can enjoy these modules as pre-compiled packages in the repo itself. If you build Linux-ck from AUR you **can not use the repo** as all packages in the repo are matched groups.

See the [Repo-ck](/index.php/Repo-ck "Repo-ck") section to set up it correctly.

#### The virtualbox-ck-host-modules package (recommended if Linux-ck is built from AUR)

Install the [virtualbox-ck-host-modules](https://aur.archlinux.org/packages/virtualbox-ck-host-modules/) package and then install the **virtualbox** package.

#### Use DKMS (more complicated, recommended for LTS versions)

Install **virtualbox** with the **virtualbox-host-dkms** package. Then setup DKMS as follows:

```
# pacman -S virtualbox virtualbox-host-dkms
# dkms install vboxhost/4.3.12

```

**Note:** Make sure to substitute the correct version number of virtualbox in the second command. At the time of writing, 4.3.12 is current.

### Downgrading

Users wishing to downgrade to a previous version of Linux-ck, have several options:

*   Source archives are [available](http://repo-ck.com/bench.htm) dating back to linux-ck-3.3.7-1\.
*   [AUR.git](http://pkgbuild.com/git/aur-mirror.git/log/linux-ck) holds AUR git commits for Linux-ck, dating back to linux-ck-2.6.39.3-1.

### Forum support

Always feel free to open a thread in the forums for support purpose. Be sure to give the thread a descriptive title to draw attention to the fact that the post relates to the Linux-ck package.

## See also

*   [Kernel patch homepage of Con Kolivas](http://users.tpg.com.au/ckolivas/kernel/)
*   [Con Kolivas' Blog](http://ck-hack.blogspot.it/)
*   [Con Kolivas' desktop-centric kernel patchset](http://lkml.org/lkml/2009/9/6/136)
*   [Wikipedia's Con Kovalis page](https://en.wikipedia.org/wiki/Con_Kolivas)
*   [Wikipedia's BFS article](https://en.wikipedia.org/wiki/Brain_Fuck_Scheduler)