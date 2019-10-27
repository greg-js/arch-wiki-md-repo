Related articles

*   [Unofficial user repositories/Repo-ck](/index.php/Unofficial_user_repositories/Repo-ck "Unofficial user repositories/Repo-ck")
*   [Modprobed-db](/index.php/Modprobed-db "Modprobed-db")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 General package details](#General_package_details)
    *   [1.1 Release cycle](#Release_cycle)
    *   [1.2 Long-Term Support (LTS) CK releases](#Long-Term_Support_(LTS)_CK_releases)
*   [2 More about MuQSS](#More_about_MuQSS)
    *   [2.1 Check if MuQSS is enabled](#Check_if_MuQSS_is_enabled)
    *   [2.2 MuQSS patched kernels and systemd](#MuQSS_patched_kernels_and_systemd)
*   [3 Using out-of-tree modules with linux-ck](#Using_out-of-tree_modules_with_linux-ck)
*   [4 See also](#See_also)

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

## Using out-of-tree modules with linux-ck

Many out-of-tree modules (broadcom-wl, nvidia, virtualbox, etc.) can be easily compiled and managed by using [dkms](/index.php/Dkms "Dkms"). A requisite for this is the corresponding headers package and base-devel package. See the dkms article for more.

## See also

*   [Kernel patch repository of Con Kolivas](http://ck.kolivas.org/patches/)
*   [Con Kolivas' Blog](http://ck-hack.blogspot.it/)
*   [Con Kolivas' first BFS announcement on the Linux Kernel Mailing List](http://lkml.org/lkml/2009/9/6/136)
*   [Wikipedia's Con Kolivas page](https://en.wikipedia.org/wiki/Con_Kolivas "wikipedia:Con Kolivas")
*   [Wikipedia's BFS article](https://en.wikipedia.org/wiki/Brain_Fuck_Scheduler "wikipedia:Brain Fuck Scheduler")
*   [Arch ck Linux forum support thread](https://bbs.archlinux.org/viewtopic.php?pid=1869636)