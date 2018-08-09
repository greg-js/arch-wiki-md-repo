Related articles

*   [Linux-ck](/index.php/Linux-ck "Linux-ck")

[Repo-ck](http://repo-ck.com/) is an unofficial Arch Linux repository hosting generic and CPU-optimized kernels and support packages, featuring [MuQSS](http://ck-hack.blogspot.com) (pronounced mux) and rest of the ck patchset by [Con Kolivas](https://en.wikipedia.org/wiki/Con_Kolivas "wikipedia:Con Kolivas"). It has been in operation since 2011 and is maintained by [graysky](/index.php/User:Graysky "User:Graysky").

## Contents

*   [1 Setup](#Setup)
*   [2 Kernels and related packages](#Kernels_and_related_packages)
*   [3 Selecting the correct CPU optimized package](#Selecting_the_correct_CPU_optimized_package)
    *   [3.1 Speed benefits of CPU optimized packages](#Speed_benefits_of_CPU_optimized_packages)
*   [4 BFQ I/O scheduler](#BFQ_I.2FO_scheduler)
*   [5 Repository statistics](#Repository_statistics)
*   [6 Mirrors](#Mirrors)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Support](#Support)
    *   [7.2 Downloads interrupt regularly](#Downloads_interrupt_regularly)
    *   [7.3 Error: signature from graysky is unknown trust](#Error:_signature_from_graysky_is_unknown_trust)

## Setup

Add the repo to `/etc/pacman.conf` under the Arch [official repositories](/index.php/Official_repositories "Official repositories"):

 `/etc/pacman.conf` 
```
[repo-ck]
Server = http://repo-ck.com/$arch

```

[Sign](/index.php/Pacman-key#Adding_unofficial_keys "Pacman-key") graysky's key:

```
# pacman-key -r 5EE46C4C && pacman-key --lsign-key 5EE46C4C

```

Update your sync database:

```
# pacman -Syy

```

## Kernels and related packages

The official Arch Linux kernel provides a *generic* package which is built for the x86_64 architecture that will run on *any* compatible x86_64 CPU. Repo-ck also hosts a generic version of [linux-ck](/index.php/Linux-ck "Linux-ck") but also provides optimized packages for specific CPUs.

| CPU Type | Group Alias | Details |
| Generic | *ck-generic* | Generic kernel similar to the official Arch Linux kernel. |
| Intel | *ck-atom* | Intel Atom specific optimizations. |
| *ck-silvermont* | Intel Silvermont specific optimizations. |
| *ck-core2* | Intel Core 2-family including Dual and Quads. |
| *ck-nehalem* | Intel 1st Generation Core i3/i5/i7-family |
| *ck-sandybridge* | Intel 2nd Generation Core i3/i5/i7-family |
| *ck-ivybridge* | Intel 3rd Generation Core i3/i5/i7-family |
| *ck-haswell* | Intel 4th Generation Core i3/i5/i7-family |
| *ck-broadwell* | Intel 5th Generation Core i3/i5/i7-family |
| *ck-skylake* | Intel 6th Generation Core i3/i5/i7-family |
| *ck-p4* | Intel Pentium-4 (P4/P4-based Celeron/Pentium-4 M/Older Xeon). |
| *ck-pentm* | Intel Pentium-M (Pentium-M notebook chips/not Pentium-4 M). |
| AMD | *ck-kx* | AMD K7/K8-family |
| *ck-k10* | AMD K10-family including 61xx Eight-Core Magny-Cours, Athlon X2 7x50, Phenom X3/X4/II, Athlon II X2/X3/X4, or Turion II-family processor. |
| *ck-bobcat* | CPUs based on AMD Family 14h cores with x86-64 instruction set support. |
| *ck-bulldozer* | CPUs based on AMD Family 15h cores with x86-64 instruction set support. |
| *ck-piledriver* | CPUs based on AMD Family 15h cores with x86-64 instruction set support. |
| *ck-zen* | CPUs based on AMD Family 17h cores with x86-64 instruction set support. |

## Selecting the correct CPU optimized package

When unsure, install the **ck-generic** group, which works with any compatible CPU. Those wanting CPU-specific optimized packages can run the following command (assuming that [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) is installed):

```
$ gcc -c -Q -march=native --help=target | grep march

```

The resulting `-march` is what GCC would use natively. Refer to the table below for a mapping of this value to the correct group.

**Warning:** Intel CPU optimized packages support only full Core2 series and i3/i5/i7 series chips. Many Pentium/Celeron chips lack the full requisite instruction sets to make use of the optimized packages. Users of these chips should install the generic packages, even if GCC returns a value corresponding to full core i3/i5/i7 match such as haswell.

**Note:** This table has been updated to show the new simplified march options that ship with GCC v4.9+. For more information see the [release notes](https://gcc.gnu.org/gcc-4.9/changes.html).

| Brand | Group | March |
| Intel | *ck-atom* | bonnell |
| *ck-silvermont* | silvermont |
| *ck-core2* | core2 |
| *ck-nehalem* | nehalem |
| *ck-sandybridge* | sandybridge |
| *ck-ivybridge* | ivybridge |
| *ck-haswell* | haswell |
| *ck-broadwell* | broadwell |
| *ck-skylake* | skylake |
| *ck-p4* | pentium4, prescott, nocona |
| *ck-pentm* | pentm, pentium-m |
| AMD | *ck-kx* | athlon, athlon-4, athlon-tbird, athlon-mp, athlon-xp, k8-sse3 |
| *ck-k10* | amdfam10 |
| *ck-bobcat* | btver1 |
| *ck-bulldozer* | bdver1 |
| *ck-piledriver* | bdver2 |
| *ck-zen* | znver1 |

**Note:** Add additional entries to this table based on experience.

For further help, see:

*   [http://wiki.gentoo.org/wiki/Safe_CFLAGS#Intel](http://wiki.gentoo.org/wiki/Safe_CFLAGS#Intel)
*   [http://wiki.gentoo.org/wiki/Safe_CFLAGS#AMD](http://wiki.gentoo.org/wiki/Safe_CFLAGS#AMD)
*   [http://www.linuxforge.net/docs/linux/linux-gcc.php](http://www.linuxforge.net/docs/linux/linux-gcc.php)

### Speed benefits of CPU optimized packages

Extensive testing comparing the effect of GCC compile options show varying results, from no change to rather significant speed ups. [[1]](https://bbs.archlinux.org/viewtopic.php?id=154333) [[2]](https://www.phoronix.com/scan.php?page=news_item&px=GCC-Optimizations-E3V5-Levels) [[3]](https://www.phoronix.com/scan.php?page=article&item=intel_core_avx2&num=2)

## BFQ I/O scheduler

See [Improving performance#Input/output schedulers](/index.php/Improving_performance#Input.2Foutput_schedulers "Improving performance").

## Repository statistics

**Note:** The statistics are not updated daily but do give a snapshot of the data based on one mirror only.

Repo [statistics](http://repo-ck.com/stats.pdf) are available (package and CPU popularity, number of downloads, and so forth).

## Mirrors

There are two mirrors available now:

*   [https://mirror.archlinux.no/repo-ck](https://mirror.archlinux.no/repo-ck) (Very low uptime)
*   [https://archd.hkno.it](https://archd.hkno.it) (Unavailable)

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

Alternatively, change the [pacman](/index.php/Pacman "Pacman") downloader to [wget](/index.php/Pacman/Tips_and_tricks#wget "Pacman/Tips and tricks"), which automatically resumes downloads.

See [this forum post](https://bbs.archlinux.org/viewtopic.php?pid=1422475#p1422475) for an explanation of these issues.

### Error: signature from graysky is unknown trust

Users must import and sign graysky's gpg key. Instructions along with his key ID are located at [repo-ck.com](http://repo-ck.com/). See also [Pacman/Package signing#Adding unofficial keys](/index.php/Pacman/Package_signing#Adding_unofficial_keys "Pacman/Package signing").