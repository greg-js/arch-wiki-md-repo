*Repo-ck* is an unofficial Arch Linux repository with generic and CPU-optimized kernels and support packages, featuring [BFS](http://ck-hack.blogspot.com) ([Brain Fuck Scheduler](https://en.wikipedia.org/wiki/Brain_Fuck_Scheduler "wikipedia:Brain Fuck Scheduler")) and rest of the `-ck` patchset by [Con Kolivas](https://en.wikipedia.org/wiki/Con_Kolivas "wikipedia:Con Kolivas").

## Contents

*   [1 Installation](#Installation)
*   [2 Kernels and related packages](#Kernels_and_related_packages)
*   [3 Selecting the correct CPU optimized package](#Selecting_the_correct_CPU_optimized_package)
    *   [3.1 Speed benefits of CPU optimized packages](#Speed_benefits_of_CPU_optimized_packages)
*   [4 Installation examples](#Installation_examples)
*   [5 BFQ I/O scheduler](#BFQ_I.2FO_scheduler)
*   [6 Repository statistics](#Repository_statistics)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Support](#Support)
    *   [7.2 Downloads interrupt regularly](#Downloads_interrupt_regularly)

## Installation

Add the [repo-ck](/index.php/Unofficial_user_repositories#repo-ck "Unofficial user repositories") repository to `pacman.conf` and [sign](/index.php/Pacman-key#Adding_unofficial_keys "Pacman-key") [Graysky](http://repo-ck.com/)'s key.

## Kernels and related packages

**Note:** LTS packages are not included.

The official kernel is available in two flavors (either i686 or x86_64) which are *generic* packages, in that i686 will work with *any* compatible x86 CPU and x86_64 will work with *any* compatible x86_64 CPU. Users have a choice between the corresponding generic linux-ck package, or packages optimized for a specific CPU.

CPU-specific optimizations are invoked by selecting *Processor type and features > Processor family* in `make menuconfig`, or by adjusting `.config` accordingly. These changes setup make specific GCC options, including `CFLAGS`.

Packages marked with `*` are available only for the 64-bit systems, see [this forum post](https://bbs.archlinux.org/viewtopic.php?pid=1423574#p1423574).

| CPU Type | Group Alias | Details |
| **Generic** | *ck-generic* | Generic kernel similar to the official Arch Linux kernel. |
| **Intel** | *ck-atom* | Intel Atom specific optimizations. |
| *ck-silvermont ** | Intel Silvermont specific optimizations. |
| *ck-core2* | Intel Core 2-family including Dual and Quads. |
| *ck-nehalem ** | Intel 1st Generation Core i3/i5/i7-family |
| *ck-sandybridge ** | Intel 2nd Generation Core i3/i5/i7-family |
| *ck-ivybridge ** | Intel 3rd Generation Core i3/i5/i7-family |
| *ck-haswell ** | Intel 4th Generation Core i3/i5/i7-family |
| *ck-broadwell ** | Intel 5th Generation Core i3/i5/i7-family |
| *ck-p4* | Intel Pentium-4 (P4/P4-based Celeron/Pentium-4 M/Older Xeon). |
| *ck-pentm* | Intel Pentium-M (Pentium-M notebook chips/not Pentium-4 M). |
| **AMD** | *ck-kx* | AMD K7/K8-family |
| *ck-k10 ** | AMD K10-family including 61xx Eight-Core Magny-Cours, Athlon X2 7x50, Phenom X3/X4/II, Athlon II X2/X3/X4, or Turion II-family processor. |
| *ck-bobcat ** | CPUs based on AMD Family 14h cores with x86-64 instruction set support. |
| *ck-bulldozer ** | CPUs based on AMD Family 15h cores with x86-64 instruction set support. |
| *ck-piledriver ** | CPUs based on AMD Family 15h cores with x86-64 instruction set support. |

## Selecting the correct CPU optimized package

When unsure, install the **ck-generic** group, which works with any compatible CPU. Those wanting CPU-specific optimized packages can run the following command (assuming that [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) is installed):

```
$ gcc -c -Q -march=native --help=target | grep march

```

The resulting `-march` is what GCC would use natively. Refer to the table below for a mapping of this value to the correct group.

**Warning:** Intel CPU optimized packages support only full Core2 series and i3/i5/i7 series chips. Many Pentium/Celeron chips lack the full requisite instruction sets to make use of the optimized packages. Users of these chips should install the generic packages, even if GCC returns a value corresponding to full core i3/i5/i7 match such as haswell.

**Note:** This table has been updated to show the new simplified march options that ship with GCC v4.9+. For more information see the [release notes](https://gcc.gnu.org/gcc-4.9/changes.html).

| Brand | Group | March |
| **Intel** | *ck-atom* | bonnell |
| *ck-silvermont* | silvermont |
| *ck-core2* | core2 |
| *ck-nehalem* | nehalem |
| *ck-sandybridge* | sandybridge |
| *ck-ivybridge* | ivybridge |
| *ck-haswell* | haswell |
| *ck-broadwell* | broadwell |
| *ck-p4* | pentium4, prescott, nocona |
| *ck-pentm* | pentm, pentium-m |
| **AMD** | *ck-kx* | athlon, athlon-4, athlon-tbird, athlon-mp, athlon-xp, k8-sse3 |
| *ck-k10* | amdfam10 |
| *ck-bobcat* | btver1 |
| *ck-bulldozer* | bdver1 |
| *ck-piledriver* | bdver2 |

**Note:** Add additional entries to this table based on experience.

For further help, see:

*   [http://wiki.gentoo.org/wiki/Safe_CFLAGS#Intel](http://wiki.gentoo.org/wiki/Safe_CFLAGS#Intel)
*   [http://wiki.gentoo.org/wiki/Safe_CFLAGS#AMD](http://wiki.gentoo.org/wiki/Safe_CFLAGS#AMD)
*   [http://www.linuxforge.net/docs/linux/linux-gcc.php](http://www.linuxforge.net/docs/linux/linux-gcc.php)

### Speed benefits of CPU optimized packages

Extensive testing comparing the effect of GCC compile options show varying results, from no change to rather significant speed ups. [[1]](http://www.phoronix.com/scan.php?page=home) [[2]](https://bbs.archlinux.org/viewtopic.php?id=154333)

## Installation examples

**Note:** As with *any* additional kernel, manually edit the boot loader configuration to make it aware of new kernel images. For example, see [GRUB#Generate the main configuration file](/index.php/GRUB#Generate_the_main_configuration_file "GRUB") for GRUB.

Use the **ck-X** group and select the desired packages for installation. There are 10 groups corresponding to the [package sets](#Kernels_and_related_packages). For example:

 `# pacman -S ck-generic` 
```
:: There are 8 members in group ck-generic:
:: Repository repo-ck
   1) broadcom-wl-ck  2) linux-ck  3) linux-ck-headers  4) nvidia-304xx-ck  5) nvidia-340xx-ck  6) nvidia-ck
   7) virtualbox-ck-guest-modules  8) virtualbox-ck-host-modules

Enter a selection (default=all):
```

Alternatively, direct pacman to install *linux-ck* and *linux-ck-headers*.

## BFQ I/O scheduler

See [Linux-ck#How to enable the BFQ I/O Scheduler](/index.php/Linux-ck#How_to_enable_the_BFQ_I.2FO_Scheduler "Linux-ck").

## Repository statistics

**Note:** The statistics are not updated daily but do give a snapshot of the data.

Repo [statistics](http://repo-ck.com/stats.pdf) are available (package and CPU popularity, number of downloads, and so forth).

## Troubleshooting

### Support

Please use [the BBS thread](https://bbs.archlinux.org/viewtopic.php?id=111715).

### Downloads interrupt regularly

[Graysky](https://aur.archlinux.org/account/graysky) is using [Go Daddy](https://en.wikipedia.org/wiki/Go_Daddy "wikipedia:Go Daddy") as his web host. Some of the transfers from their poorly implemented server end in an incomplete transfer. To combat this, list the repository address multiple times and pacman will automatically try the next available server. As repo-ck has only one address (no mirrors), use the same server line:

```
[repo-ck]
Server = http://repo-ck.com/$arch
Server = http://repo-ck.com/$arch
Server = http://repo-ck.com/$arch
Server = http://repo-ck.com/$arch
Server = http://repo-ck.com/$arch

```

Alternatively, change the [pacman](/index.php/Pacman "Pacman") downloader to [wget](/index.php/Improve_pacman_performance#Using_wget "Improve pacman performance"), which automatically resumes downloads.

See [this forum post](https://bbs.archlinux.org/viewtopic.php?pid=1422475#p1422475) for an explanation of these issues.