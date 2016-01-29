# BusyBox

**Warning:** Do not expect full drop-in replacement and compatibility. Certain utilities may not exist and for those that do, there may be missing options. One purpose of this Wiki is to document missing features and the problems they cause (in order to device work-arounds). Make sure that the replacement(s) that you install fill your needs before proceeding.

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** Last proper update was from 2011, so especially the "missing" sections should be checked (Discuss in [Talk:BusyBox#](https://wiki.archlinux.org/index.php/Talk:BusyBox))

## Contents

*   [1 Installation](#Installation)
*   [2 init](#init)
*   [3 coreutils](#coreutils)
    *   [3.1 Missing functionality](#Missing_functionality)
    *   [3.2 Missing utilities mapped to corresponding Busybox functions or ash script files](#Missing_utilities_mapped_to_corresponding_Busybox_functions_or_ash_script_files)
    *   [3.3 Missing features that cause problems](#Missing_features_that_cause_problems)
*   [4 util-linux](#util-linux)
    *   [4.1 Missing utilities](#Missing_utilities)
*   [5 findutils](#findutils)
    *   [5.1 Missing utilities](#Missing_utilities_2)
*   [6 diffutils](#diffutils)
    *   [6.1 Missing utilities](#Missing_utilities_3)
*   [7 mdev](#mdev)

## Installation

[Install](/index.php/Install "Install") [busybox](https://www.archlinux.org/packages/?name=busybox) from the [official repositories](/index.php/Official_repositories "Official repositories").

Busybox commands are symbolic links to `/usr/bin/busybox` and thus take very little space. This is especially interesting for low-footprint systems. Several packages in the [AUR](/index.php/AUR "AUR") replace the GNU utilities with these symbolic links.

## init

[Minirc](https://github.com/hut/minirc) provides an init script compatible to busybox-init. See [init](/index.php/Init "Init") for details.

## coreutils

[busybox-coreutils](https://aur.archlinux.org/packages/busybox-coreutils/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/busybox-coreutils)]</sup> is the busybox equivalent to GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils). Some commands lack options present in the corresponding coreutils binaries.

Space gain: 13.1 MB installed (coreutils)

### Missing functionality

```
dircolors chcon csplit factor fmt join nl nproc paste pinky pr ptx runcon shuf stdbuf timeout truncate tsort users

```

### Missing utilities mapped to corresponding Busybox functions or ash script files

```
dir --> ls
shred --> rm
vdir --> ls

```

```
link --> ln
unlink --> rm
sha224sum --> script: perl-digest-sha
sha256sum --> script: perl-digest-sha
sha384sum --> script: perl-digest-sha
sha512sum --> script: perl-digest-sha

```

### Missing features that cause problems

```
readlink: missing option [-e, -m, -q or -s]

```

## util-linux

[busybox-util-linux](https://aur.archlinux.org/packages/busybox-util-linux/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/busybox-util-linux)]</sup> is the busybox equivalent to GNU [util-linux](https://www.archlinux.org/packages/?name=util-linux).

Space gain: 7.5 MB installed (util-linux)

### Missing utilities

```
arch findmnt lsblk agetty blkid cfdisk ctrlaltdel findfs fsck.cramfs fsfreeze fstrim mkfs mkfs.bfs mkfs.cramfs raw sfdisk swaplabel wipefs 

```

```
chkdupexe col colcrt colrm column cytune ddate fallocate i386 ionice ipcmk isosize line look lscpu mcookie namei pg rename scriptreplay setterm tailf taskset ul unshare uuidgen whereis write x86_64

```

```
addpart delpart ldattach partx tunelp uuidd

```

## findutils

[busybox-findutils](https://aur.archlinux.org/packages/busybox-findutils/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/busybox-findutils)]</sup> is the busybox equivalent to GNU [findutils](https://www.archlinux.org/packages/?name=findutils).

### Missing utilities

```
oldfind

```

## diffutils

[busybox-diffutils](https://aur.archlinux.org/packages/busybox-diffutils/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/busybox-diffutils)]</sup> from the AUR offers functionality corresponding to the binaries found in GNU [diffutils](https://www.archlinux.org/packages/?name=diffutils).

Space gain: 1.4 MB installed (diffutils)

### Missing utilities

```
diff3 sdiff

```

## mdev

See [Gentoo wiki](https://wiki.gentoo.org/wiki/Mdev).

Retrieved from "[https://wiki.archlinux.org/index.php?title=BusyBox&oldid=412048](https://wiki.archlinux.org/index.php?title=BusyBox&oldid=412048)"