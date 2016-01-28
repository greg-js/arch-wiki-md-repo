# Repo-ck

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Linux-ck](/index.php/Linux-ck "Linux-ck")
*   [Linux-ck/Changelog](/index.php/Linux-ck/Changelog "Linux-ck/Changelog")

_Repo-ck_ is an unofficial Arch Linux repository with generic and CPU-optimized kernels and support packages, featuring [BFS](http://ck-hack.blogspot.com) ([Brain Fuck Scheduler](https://en.wikipedia.org/wiki/Brain_Fuck_Scheduler "wikipedia:Brain Fuck Scheduler")) and rest of the `-ck` patchset by [Con Kolivas](https://en.wikipedia.org/wiki/Con_Kolivas "wikipedia:Con Kolivas").

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

The official kernel is available in two flavors (either i686 or x86_64) which are _generic_ packages, in that i686 will work with _any_ compatible x86 CPU and x86_64 will work with _any_ compatible x86_64 CPU. Users have a choice between the corresponding generic linux-ck package, or packages optimized for a specific CPU.

CPU-specific optimizations are invoked by selecting _Processor type and features > Processor family_ in `make menuconfig`, or by adjusting `.config` accordingly. These changes setup make specific GCC options, including `CFLAGS`.

Packages marked with `*` are available only for the 64-bit systems, see [this forum post](https://bbs.archlinux.org/viewtopic.php?pid=1423574#p1423574).

<table class="wikitable" align="center">

<tbody>

<tr>

<th>CPU Type</th>

<th>Group Alias</th>

<th>Details</th>

</tr>

<tr>

<td style="background: #aff; color: inherit; vertical-align: middle; text-align: center;">**Generic**</td>

<td>_ck-generic_</td>

<td>Generic kernel similar to the official Arch Linux kernel.</td>

</tr>

<tr>

<td rowspan="10" style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">**Intel**</td>

<td>_ck-atom_</td>

<td>Intel Atom specific optimizations.</td>

</tr>

<tr>

<td>_ck-silvermont *_</td>

<td>Intel Silvermont specific optimizations.</td>

</tr>

<tr>

<td>_ck-core2_</td>

<td>Intel Core 2-family including Dual and Quads.</td>

</tr>

<tr>

<td>_ck-nehalem *_</td>

<td>Intel 1st Generation Core i3/i5/i7-family</td>

</tr>

<tr>

<td>_ck-sandybridge *_</td>

<td>Intel 2nd Generation Core i3/i5/i7-family</td>

</tr>

<tr>

<td>_ck-ivybridge *_</td>

<td>Intel 3rd Generation Core i3/i5/i7-family</td>

</tr>

<tr>

<td>_ck-haswell *_</td>

<td>Intel 4th Generation Core i3/i5/i7-family</td>

</tr>

<tr>

<td>_ck-broadwell *_</td>

<td>Intel 5th Generation Core i3/i5/i7-family</td>

</tr>

<tr>

<td>_ck-p4_</td>

<td>Intel Pentium-4 (P4/P4-based Celeron/Pentium-4 M/Older Xeon).</td>

</tr>

<tr>

<td>_ck-pentm_</td>

<td>Intel Pentium-M (Pentium-M notebook chips/not Pentium-4 M).</td>

</tr>

<tr>

<td rowspan="5" style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">**AMD**</td>

<td>_ck-kx_</td>

<td>AMD K7/K8-family</td>

</tr>

<tr>

<td>_ck-k10 *_</td>

<td>AMD K10-family including 61xx Eight-Core Magny-Cours, Athlon X2 7x50, Phenom X3/X4/II, Athlon II X2/X3/X4, or Turion II-family processor.</td>

</tr>

<tr>

<td>_ck-bobcat *_</td>

<td>CPUs based on AMD Family 14h cores with x86-64 instruction set support.</td>

</tr>

<tr>

<td>_ck-bulldozer *_</td>

<td>CPUs based on AMD Family 15h cores with x86-64 instruction set support.</td>

</tr>

<tr>

<td>_ck-piledriver *_</td>

<td>CPUs based on AMD Family 15h cores with x86-64 instruction set support.</td>

</tr>

</tbody>

</table>

## Selecting the correct CPU optimized package

When unsure, install the **ck-generic** group, which works with any compatible CPU. Those wanting CPU-specific optimized packages can run the following command (assuming that [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) is installed):

```
$ gcc -c -Q -march=native --help=target | grep march

```

The resulting `-march` is what GCC would use natively. Refer to the table below for a mapping of this value to the correct group.

**Warning:** Intel CPU optimized packages support only full Core2 series and i3/i5/i7 series chips. Many Pentium/Celeron chips lack the full requisite instruction sets to make use of the optimized packages. Users of these chips should install the generic packages, even if GCC returns a value corresponding to full core i3/i5/i7 match such as haswell.

**Note:** This table has been updated to show the new simplified march options that ship with GCC v4.9+. For more information see the [release notes](https://gcc.gnu.org/gcc-4.9/changes.html).

<table class="wikitable" align="center">

<tbody>

<tr>

<th>Brand</th>

<th>Group</th>

<th>March</th>

</tr>

<tr>

<td rowspan="10" style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">**Intel**</td>

<td>_ck-atom_</td>

<td>bonnell</td>

</tr>

<tr>

<td>_ck-silvermont_</td>

<td>silvermont</td>

</tr>

<tr>

<td>_ck-core2_</td>

<td>core2</td>

</tr>

<tr>

<td>_ck-nehalem_</td>

<td>nehalem</td>

</tr>

<tr>

<td>_ck-sandybridge_</td>

<td>sandybridge</td>

</tr>

<tr>

<td>_ck-ivybridge_</td>

<td>ivybridge</td>

</tr>

<tr>

<td>_ck-haswell_</td>

<td>haswell</td>

</tr>

<tr>

<td>_ck-broadwell_</td>

<td>broadwell</td>

</tr>

<tr>

<td>_ck-p4_</td>

<td>pentium4, prescott, nocona</td>

</tr>

<tr>

<td>_ck-pentm_</td>

<td>pentm, pentium-m</td>

</tr>

<tr>

<td rowspan="5" style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">**AMD**</td>

<td>_ck-kx_</td>

<td>athlon, athlon-4, athlon-tbird, athlon-mp, athlon-xp, k8-sse3</td>

</tr>

<tr>

<td>_ck-k10_</td>

<td>amdfam10</td>

</tr>

<tr>

<td>_ck-bobcat_</td>

<td>btver1</td>

</tr>

<tr>

<td>_ck-bulldozer_</td>

<td>bdver1</td>

</tr>

<tr>

<td>_ck-piledriver_</td>

<td>bdver2</td>

</tr>

</tbody>

</table>

**Note:** Add additional entries to this table based on experience.

For further help, see:

*   [http://wiki.gentoo.org/wiki/Safe_CFLAGS#Intel](http://wiki.gentoo.org/wiki/Safe_CFLAGS#Intel)
*   [http://wiki.gentoo.org/wiki/Safe_CFLAGS#AMD](http://wiki.gentoo.org/wiki/Safe_CFLAGS#AMD)
*   [http://www.linuxforge.net/docs/linux/linux-gcc.php](http://www.linuxforge.net/docs/linux/linux-gcc.php)

### Speed benefits of CPU optimized packages

Extensive testing comparing the effect of GCC compile options show varying results, from no change to rather significant speed ups. [[1]](http://www.phoronix.com/scan.php?page=home) [[2]](https://bbs.archlinux.org/viewtopic.php?id=154333)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Add results to this section where appropriate. (Discuss in [Talk:Repo-ck#](https://wiki.archlinux.org/index.php/Talk:Repo-ck))

## Installation examples

**Note:** As with _any_ additional kernel, manually edit the boot loader configuration to make it aware of new kernel images. For example, see [GRUB#Generate the main configuration file](/index.php/GRUB#Generate_the_main_configuration_file "GRUB") for GRUB.

Use the **ck-X** group and select the desired packages for installation. There are 10 groups corresponding to the [package sets](#Kernels_and_related_packages). For example:

 `# pacman -S ck-generic` 

```
:: There are 8 members in group ck-generic:
:: Repository repo-ck
   1) broadcom-wl-ck  2) linux-ck  3) linux-ck-headers  4) nvidia-304xx-ck  5) nvidia-340xx-ck  6) nvidia-ck
   7) virtualbox-ck-guest-modules  8) virtualbox-ck-host-modules

Enter a selection (default=all):
```

Alternatively, direct pacman to install _linux-ck_ and _linux-ck-headers_.

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

Retrieved from "[https://wiki.archlinux.org/index.php?title=Repo-ck&oldid=414104](https://wiki.archlinux.org/index.php?title=Repo-ck&oldid=414104)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Kernel](/index.php/Category:Kernel "Category:Kernel")

Hidden category:

*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")