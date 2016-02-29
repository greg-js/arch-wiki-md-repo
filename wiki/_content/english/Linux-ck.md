## Contents

*   [1 General package details](#General_package_details)
    *   [1.1 Release cycle](#Release_cycle)
    *   [1.2 Package defaults](#Package_defaults)
    *   [1.3 Long-Term Support (LTS) CK releases](#Long-Term_Support_.28LTS.29_CK_releases)
*   [2 Installation options](#Installation_options)
    *   [2.1 1\. Compile the package from source](#1._Compile_the_package_from_source)
    *   [2.2 2 . Use pre-compiled packages](#2_._Use_pre-compiled_packages)
*   [3 How to enable the BFQ I/O Scheduler](#How_to_enable_the_BFQ_I.2FO_Scheduler)
    *   [3.1 Enable BFQ for all devices](#Enable_BFQ_for_all_devices)
    *   [3.2 Enable BFQ for only specified devices](#Enable_BFQ_for_only_specified_devices)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Boot loader and Linux-ck](#Boot_loader_and_Linux-ck)
    *   [4.2 Running VirtualBox with Linux-ck](#Running_VirtualBox_with_Linux-ck)
        *   [4.2.1 Use the unofficial repo (recommended if linux-ck is installed from Repo-ck)](#Use_the_unofficial_repo_.28recommended_if_linux-ck_is_installed_from_Repo-ck.29)
        *   [4.2.2 The virtualbox-ck-host-modules package (recommended if linux-ck is built by you from the AUR)](#The_virtualbox-ck-host-modules_package_.28recommended_if_linux-ck_is_built_by_you_from_the_AUR.29)
        *   [4.2.3 Use DKMS (more complicated, recommended with LTS releases)](#Use_DKMS_.28more_complicated.2C_recommended_with_LTS_releases.29)
    *   [4.3 Downgrading](#Downgrading)
    *   [4.4 Forum support](#Forum_support)
*   [5 A little about the BFS](#A_little_about_the_BFS)
    *   [5.1 BFS design goals](#BFS_design_goals)
    *   [5.2 An example video about queuing theory](#An_example_video_about_queuing_theory)
    *   [5.3 Some performance-based metrics: BFS vs. CFS](#Some_performance-based_metrics:_BFS_vs._CFS)
    *   [5.4 Check if enabled](#Check_if_enabled)
*   [6 BFS myths](#BFS_myths)
    *   [6.1 BFS patched kernels CAN in fact use systemd](#BFS_patched_kernels_CAN_in_fact_use_systemd)
*   [7 Further Reading on BFS and CK Patchset](#Further_Reading_on_BFS_and_CK_Patchset)

## General package details

[Linux-ck](https://aur.archlinux.org/packages/Linux-ck/) is a package available in the [AUR](/index.php/AUR "AUR") and in the [unofficial linux-ck repo](#2_._Use_pre-compiled_packages) that allows users to run a kernel/headers setup patched with Con Kolivas' ck1 patchset, including the Brain Fuck Scheduler (BFS). Many Archers elect to use this package for the BFS' excellent desktop interactivity and responsiveness under any load situation. Additionally, the bfs imparts performance gains beyond interactivity. For example, see: [CPU_Schedulers_Compared.pdf](http://repo-ck.com/bench/cpu_schedulers_compared.pdf).

### Release cycle

Linux-ck roughly follows the release cycle of the official ARCH kernel. The following are requirements for its release:

*   Upstream code
*   CK's Patchset
*   BFQ Patchset
*   ARCH config/config.x86_64 sets for major version jumps only

### Package defaults

There are **three** modifications to the config files:

1.  The options that the ck patchset enable/disable.
2.  The options that the BFQ patchset need to compile without user interaction.
3.  Apply [GCC patch](https://github.com/graysky2/kernel_gcc_patch) that enables additional CPU optimizations at compile time (these options are not part of the standard linux-ck package and are only available when the user compiles custom options).

**All other options are set to the ARCH defaults outlined in the main kernel's config files.** Users are of course free to modify them! The linux-ck package contains an option to switch on the **nconfig** config editor (see section below). For some suggestions, see CK's [BFS configuration FAQ](http://ck.kolivas.org/patches/bfs/bfs-configuration-faq.txt).

### Long-Term Support (LTS) CK releases

In addition to the linux-ck package, there are the following LTS kernel releases patched with the above patchsets, with the previously mentioned modifications to the config files:

*   [linux-lts-ck](https://aur.archlinux.org/packages/linux-lts-ck/) - The current ArchLinux LTS kernel patched with the CK patchset
*   [linux-lts310-ck](https://aur.archlinux.org/packages/linux-lts310-ck/) - The 3.10 LTS kernel patched with the CK patchset
*   [linux-lts312-ck](https://aur.archlinux.org/packages/linux-lts312-ck/) - The 3.12 LTS kernel patched with the CK patchset

**These three packages are maintained by clfarron4\. Pre-packaged versions will not be found in the unofficial ck repo.**

## Installation options

**Note:** As with *any* additional kernel, users will need to manually update their boot loader's config file to make it aware of the new kernel images. For example, users of [GRUB](/index.php/GRUB "GRUB") should execute "grub-mkconfig -o /boot/grub/grub.cfg". Syslinux, GRUB-legacy, etc. will need to be modified as well.

Users have two options to get these kernel packages.

### 1\. Compile the package from source

The [AUR](/index.php/AUR "AUR") contains entries for both packages mentioned above.

Users can customize the linux-ck package via tweaks in the PKGBUILD:

*   Optional nconfig for user specific tweaking.
*   Option to compile a minimal set of modules via a make localmodconfig.
*   Option to bypass the standard ARCH config options and simply use the current kernel's .config file.
*   Optionally set the [BFQ I/O scheduler](http://algo.ing.unimo.it/people/paolo/disk_sched/) as default.

More details about these options are provided in the PKGBUILD itself via line comments. Be sure to read them if compiling from the AUR!

**Note:** There are related PKGBUILDs in the AUR for other common modules unique to linux-ck. For example [nvidia-ck](https://aur.archlinux.org/packages/nvidia-ck/), [nvidia-304xx-ck](https://aur.archlinux.org/packages/nvidia-304xx-ck/),[nvidia-340xx-ck](https://aur.archlinux.org/packages/nvidia-340xx-ck/), and [broadcom-wl-ck](https://aur.archlinux.org/packages/broadcom-wl-ck/) to name a few.

### 2 . Use pre-compiled packages

If users would rather not spend the time to compile on their own, an unofficial repo maintained by [graysky](/index.php/User:Graysky "User:Graysky") is available to the community.

For details, see: [Repo-ck](/index.php/Repo-ck "Repo-ck").

There are also unofficial repositories for the aforementioned LTS branches, available at [linux-lts-ck](/index.php/Unofficial_user_repositories#linux-lts-ck "Unofficial user repositories") and [linux-lts31x-ck](/index.php/Unofficial_user_repositories#linux-lts31x-ck "Unofficial user repositories"), maintained by [clfarron4](/index.php/User:Clfarron4 "User:Clfarron4").

## How to enable the BFQ I/O Scheduler

**Note:** Do not confuse BFS (Brain Fuck Scheduler) with BFQ (Budget Fair Queueing). The BFS is a CPU scheduler and is enabled by default whereas BFQ is an I/O scheduler and must explicitly be enabled in order to use it.

Budget Fair Queueing is a disk scheduler which allows each process/thread to be assigned a portion of the disk throughput. Its creator has released some [benchmarks](http://www.youtube.com/watch?v=KhZl9LjCKuU) which shows some pretty amazing latency performance.

Since linux-ck-3.0.4-2, the BFQ patchset is applied to the package by default, but the scheduler must be enabled manually. Users have several options to do so.

### Enable BFQ for all devices

If compiling from the AUR, simply set the BFQ flag to "y" in the PKGBUILD prior to building

```
_BFQ_enable_="y"

```

Users of [repo-ck](/index.php/Repo-ck "Repo-ck") or those who have not modified the PKGBUILD prior to building may appened `elevator=bfq` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

### Enable BFQ for only specified devices

An alternative method is to direct the kernel to use BFQ on a device-by-device basis. For example, to enable it for `/dev/sda` simply:

```
# echo bfq > /sys/block/sda/queue/scheduler

```

To confirm:

```
# cat /sys/block/sda/queue/scheduler
noop deadline cfq [bfq] 

```

Note that doing it this way will not survive a reboot. To make the change automatically at the next system boot, create the following tmpfile where sdX is the desired device:

 `/etc/tmpfiles.d/set_IO_scheduler.conf`  `w /sys/block/sdX/queue/scheduler - - - - bfq` 

## Troubleshooting

### Boot loader and Linux-ck

The [boot loader](/index.php/Boot_loader "Boot loader") configuration needs to find the (new) kernel images. For GRUB, see [GRUB#Generate the main configuration file](/index.php/GRUB#Generate_the_main_configuration_file "GRUB"). For other boot loaders it may be necessary to add a custom entry.

This is an example if adding a custom entry if using [REFInd](/index.php/REFInd#Custom_Menu_Entries "REFInd"):

 `refind.conf` 
```
menuentry Linux {
        icon EFI/refind/icons/os_linux.png
        ostype Linux
        volume boot
        loader /vmlinuz-linux-ck
        initrd /initramfs-linux-ck.img
        options "root=/dev/mapper/root elevator=bfq"
}

```

### Running VirtualBox with Linux-ck

VirtualBox works just fine with custom kernels such as Linux-ck *without* the need to keep any of the official ARCH kernel-headers packages on the system!

Do not forget to add users to the *vboxusers* group:

```
# gpasswd -a USERNAME vboxusers

```

#### Use the unofficial repo (recommended if linux-ck is installed from Repo-ck)

**Note:** As of 17-Oct-2012, Repo-ck users can enjoy these modules as pre-compiled packages in the repo itself. If you built your linux-ck from the AUR you **cannot use the repo** as all packages in the repo are matched groups.

See the [Repo-ck](/index.php/Repo-ck "Repo-ck") article to set up [http://repo-ck.com](http://repo-ck.com) for pacman to use directly.

#### The virtualbox-ck-host-modules package (recommended if linux-ck is built by you from the AUR)

Install the [virtualbox-ck-host-modules](https://aur.archlinux.org/packages/virtualbox-ck-host-modules/) package and then install **virtualbox** package.

#### Use DKMS (more complicated, recommended with LTS releases)

Install **virtualbox** with the **virtualbox-host-dkms** package. Then setup dkms as follows:

```
# pacman -S virtualbox virtualbox-host-dkms
# dkms install vboxhost/4.3.12

```

**Note:** Make sure to substitute the correct version number of virtualbox in the second command. At the time of writing, 4.3.12 is current.

### Downgrading

Users wishing to downgrade to a previous version of linux-ck, have several options:

*   Source archives are [available](http://repo-ck.com/bench.htm) dating back to linux-ck-3.3.7-1\.
*   [AUR.git](http://pkgbuild.com/git/aur-mirror.git/log/linux-ck) holds AUR git commits for linux-ck dating back to linux-ck-2.6.39.3-1.

### Forum support

Always feel free to open a thread in the forums for support. Be sure to give the thread a descriptive title to draw attention to the fact that the post relates to the Linux- ck package.

## A little about the BFS

The Brain Fuck Scheduler is a desktop orientated cpu process scheduler with extremely low latencies for excellent interactivity within normal load levels.

### BFS design goals

The BFS has two major design goals:

1.  Achieve excellent desktop interactivity and responsiveness without heuristics and tuning knobs that are difficult to understand, impossible to model and predict the effect of, and when tuned to one workload cause massive detriment to another.
2.  Completely do away with the complex designs of the past for the cpu process scheduler and instead implement one that is very simple in basic design.

For additional information, see the [#Further Reading on BFS and CK Patchset](#Further_Reading_on_BFS_and_CK_Patchset) section of this article.

### An example video about queuing theory

See [this video](http://www.youtube.com/watch?v=F5Ri_HhziI0) about queuing theory for an interesting parallel with supermarket checkouts. Quote from CK, "the relevance of that video is that BFS uses a single queue, whereas the mainline Linux kernel uses a multiple queue design. The people are tasks, and the checkouts are CPUs. Of course there is a lot more to a CPU scheduler than just the queue design, but I thought this video was very relevant."

### Some performance-based metrics: BFS vs. CFS

A major benefit of using the BFS is increased responsiveness. The benefits however, are not limited to desktop feel. [Graysky](/index.php/User:Graysky "User:Graysky") put together some non-responsiveness based benchmarks to compare it to the CFS contained in the "stock" linux kernel. Seven different machines were used to see if differences exist and, to what degree they scale using performance based metrics. Again, these end-points were never factors in the primary design goals of the bfs. Results were encouraging.

For those not wanting to see the full report, here is the conclusion: Kernels patched with the ck1 patch set including the bfs outperformed the vanilla kernel using the cfs at nearly all the performance-based benchmarks tested. Further study with a larger test set could be conducted, but based on the small test set of 7 PCs evaluated, these increases in process queuing, efficiency/speed are, on the whole, independent of CPU type (mono, dual, quad, hyperthreaded, etc.), CPU architecture (32-bit and 64-bit) and of CPU multiplicity (mono or dual socket).

Moreover, several "modern" CPUs (Intel C2D and Ci7) that represent common workstations and laptops, consistently outperformed the cfs in the vanilla kernel at all benchmarks. Efficiency and speed gains were small to moderate.

[CPU_Schedulers_Compared.pdf](http://repo-ck.com/bench/cpu_schedulers_compared.pdf) is available for download.

### Check if enabled

This start-up message should appear in the kernel ring buffer when BFS in enabled:

```
# dmesg | grep scheduler
...
[    0.380500] BFS CPU scheduler v0.420 by Con Kolivas.

```

## BFS myths

### BFS patched kernels CAN in fact use systemd

It is a common mistake to think that BFS does not support cgroups. It does support cgroups, just not all the cgroup features (e. g. CPU limiting will not work).

## Further Reading on BFS and CK Patchset

*   [Con Kolivas' White Paper on the BFS](http://ck.kolivas.org/patches/bfs/bfs-faq.txt)
*   [Wikipedia's BFS Article](https://en.wikipedia.org/wiki/Brain_Fuck_Scheduler "wikipedia:Brain Fuck Scheduler")
*   [Con Kolivas' Blog](http://ck-hack.blogspot.com/)