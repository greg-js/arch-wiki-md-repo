**Warning:** None of these tools are [officially](https://bbs.archlinux.org/viewtopic.php?pid=828254#p828254) supported by Arch Linux, therefore it is recommended to become familiar with the [manual build process](/index.php/Arch_User_Repository#Installing_packages "Arch User Repository") in order to be prepared to troubleshoot problems on one's own.

AUR Helpers are written to make using the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") more comfortable.

## Contents

*   [1 Uploading](#Uploading)
*   [2 Build and search](#Build_and_search)
*   [3 Maintenance](#Maintenance)
*   [4 Libraries](#Libraries)
*   [5 Graphical](#Graphical)
*   [6 Comparison table](#Comparison_table)
*   [7 See also](#See_also)

## Uploading

| Script | Description |
| [bbidulock's script](https://gist.github.com/bbidulock/82ab6f5347f021136054) | Migrate from a .backup directory with all packages. |
| [aur4_import.sh](https://github.com/JonnyJD/PKGBUILDs/blob/master/_bin/aur4_import.sh) | Splits a package from a git repository with multiple packages, adding/updating `.SRCINFO` for every commit. |
| 

[aur4_make_submodule.sh](https://github.com/JonnyJD/PKGBUILDs/blob/master/_bin/aur4_make_submodule.sh)
[subaur4](https://github.com/alexandre-mbm/arch-pkgs/blob/master/subaur4)

 | Replaces a package in a bigger git repository with an AUR 4 submodule, including `.SRCINFO`. |
| [import-to-aur4](https://github.com/ido/packages-archlinux/blob/master/bin/import-to-aur4.sh) | Splits an existing git repository into multiple AUR 4 packages, all at once, including `.SRCINFO` for every commit. |

## Build and search

This is a list of helper utilities that search and/or build packages.

*   **apacman** — A fork of packer with additional features and bugfixes.

	[https://github.com/oshazard/apacman](https://github.com/oshazard/apacman) || [apacman](https://aur.archlinux.org/packages/apacman/)

*   **[aura](/index.php/Aura "Aura")** — A package manager for Arch Linux written in Haskell.

	[https://github.com/fosskers/aura](https://github.com/fosskers/aura) || [aura](https://aur.archlinux.org/packages/aura/) or [aura-bin](https://aur.archlinux.org/packages/aura-bin/) (binary)

*   **aurel** — Search, vote and download AUR packages from Emacs. ([Forum page](https://bbs.archlinux.org/viewtopic.php?id=177142))

	[https://github.com/alezost/aurel](https://github.com/alezost/aurel) || [aurel](https://aur.archlinux.org/packages/aurel/)

*   **aurget** — Aims to be a pacman-like interface to the AUR, without wrapping pacman commands.

	[http://github.com/pbrisbin/aurget/](http://github.com/pbrisbin/aurget/) || [aurget](https://aur.archlinux.org/packages/aurget/)

*   **aurquery** — Caching wrapper around the AUR's RPC interface using the python3-aur library.

	[http://xyne.archlinux.ca/projects/python3-aur](http://xyne.archlinux.ca/projects/python3-aur) || [python3-aur](https://aur.archlinux.org/packages/python3-aur/)

*   **bauerbill** — Powerpill/pacman extension with support for building packages from ABS and AUR, with full dependency resolution.

	[http://xyne.archlinux.ca/projects/bauerbill](http://xyne.archlinux.ca/projects/bauerbill) || [bauerbill](https://aur.archlinux.org/packages/bauerbill/)

*   **burgaur** — A front-end for cower written in Python.

	[https://github.com/m45t3r/burgaur](https://github.com/m45t3r/burgaur) || [burgaur](https://aur.archlinux.org/packages/burgaur/)

*   **cower** — AUR search and download agent written in C, which also checks for updates and package dependencies. ([Forum page](https://bbs.archlinux.org/viewtopic.php?id=97137))

	[https://github.com/falconindy/cower](https://github.com/falconindy/cower) || [cower](https://aur.archlinux.org/packages/cower/)

*   **pacaur** — An AUR helper that minimizes user interaction. ([Forum page](https://bbs.archlinux.org/viewtopic.php?pid=937423))

	[https://github.com/Spyhawk/pacaur](https://github.com/Spyhawk/pacaur) || [pacaur](https://aur.archlinux.org/packages/pacaur/)

*   **packer** — Wrapper for pacman and the AUR. ([Forum page](https://bbs.archlinux.org/viewtopic.php?id=88115))

	[https://github.com/keenerd/packer](https://github.com/keenerd/packer) || [packer](https://aur.archlinux.org/packages/packer/)

*   **pbget** — Retrieve source files from the official SVN and CVS web interface, the AUR, and the ABS rsync server.

	[http://xyne.archlinux.ca/projects/pbget](http://xyne.archlinux.ca/projects/pbget) || [pbget](https://aur.archlinux.org/packages/pbget/)

*   **PKGBUILDer** — An AUR helper with dependency support written in Python 3.

	[https://github.com/Kwpolska/pkgbuilder](https://github.com/Kwpolska/pkgbuilder) || [pkgbuilder](https://aur.archlinux.org/packages/pkgbuilder/)

*   **prm** — An AUR and ABS helper.

	[https://git.fleshless.org/prm/](https://git.fleshless.org/prm/) || [PKGBUILD](https://pkg.fleshless.org/prm/plain/PKGBUILD)

*   **trizen** — A wrapper for the AUR written in Perl.

	[https://github.com/trizen/trizen](https://github.com/trizen/trizen) || [trizen](https://aur.archlinux.org/packages/trizen/)

*   **wrapaur** — A pacman and AUR wrapper written in bash.

	[https://aur.archlinux.org/packages/wrapaur/](https://aur.archlinux.org/packages/wrapaur/) || [wrapaur](https://aur.archlinux.org/packages/wrapaur/)

*   **yaah** — Yet another AUR helper

	[https://bitbucket.org/the_metalgamer/yaah](https://bitbucket.org/the_metalgamer/yaah) || [yaah](https://aur.archlinux.org/packages/yaah/)

*   **yaourt** — A wrapper for the AUR and regular packages.

	[http://archlinux.fr/yaourt-en](http://archlinux.fr/yaourt-en) || [yaourt](https://aur.archlinux.org/packages/yaourt/)

## Maintenance

*   **pkgbuild-watch** — Looks for changes on the upstream web pages

	[http://kmkeen.com/pkgbuild-watch](http://kmkeen.com/pkgbuild-watch) || [pkgbuild-watch](https://aur.archlinux.org/packages/pkgbuild-watch/)

*   **pkgbuildup** — Helps AUR package maintainers automatically update PKGBUILD files. Supports a template variable syntax.

	Repository: [GitHub](https://github.com/fasheng/pkgbuildup) || [pkgbuildup-git](https://aur.archlinux.org/packages/pkgbuildup-git/)

*   **pkgcheck** — Uses rules in PKGBUILDs to parse upstream version information or looks for changes by checksumming the web page

	[https://bbs.archlinux.org/viewtopic.php?id=162816](https://bbs.archlinux.org/viewtopic.php?id=162816) || Repository: [GitHub](https://github.com/onny/pkgcheck)

*   **pkgoutofdate** — Parses the source URL from PKGBUILDs and tries to find new versions of packages by incrementing the version number and sending requests to the web server

	Repository: [GitHub](https://github.com/anatol/pkgoutofdate) || [pkgoutofdate-git](https://aur.archlinux.org/packages/pkgoutofdate-git/)

## Libraries

*   **haskell-archlinux** — Library to access the AUR and package metadata from the Haskell programming language

	[http://hackage.haskell.org/package/archlinux](http://hackage.haskell.org/package/archlinux) || [haskell-archlinux](https://aur.archlinux.org/packages/haskell-archlinux/)

*   **python3-aur** — Python 3 modules for accessing AUR package information and automating AUR interactions.

	[http://xyne.archlinux.ca/projects/python3-aur](http://xyne.archlinux.ca/projects/python3-aur) || [python3-aur](https://aur.archlinux.org/packages/python3-aur/)

## Graphical

*   **Aarchup** — Fork of archup. Has the same options as archup plus a few other features. For differences between both please check [changelog](https://bbs.archlinux.org/viewtopic.php?id=119129).

	[https://github.com/aericson/aarchup/](https://github.com/aericson/aarchup/) || [aarchup](https://aur.archlinux.org/packages/aarchup/)

*   **PkgBrowser** — Application for searching and browsing Arch packages, showing details on selected packages.

	[https://bitbucket.org/kachelaqa/pkgbrowser/wiki/Home](https://bitbucket.org/kachelaqa/pkgbrowser/wiki/Home) || [pkgbrowser](https://aur.archlinux.org/packages/pkgbrowser/)

*   **kalu** — Small C application that adds an icon in the systray and can show notifications for Arch Linux News, Upgrades, AUR upgrades, and watched (AUR) upgrades (upgrades for packages not installed). Also includes a GUI system upgrader.

	[https://github.com/jjk-jacky/kalu](https://github.com/jjk-jacky/kalu) || [kalu](https://aur.archlinux.org/packages/kalu/) (or [kalu-kde](https://aur.archlinux.org/packages/kalu-kde/) for auto-hide in KDE's panel)

*   **Yapan** — Written in C++ and Qt. It shows an icon in the system tray and popup notifications for new packages and supports AUR helpers.

	[https://github.com/fluxer/arch-yapan](https://github.com/fluxer/arch-yapan) || [yapan](https://aur.archlinux.org/packages/yapan/)

## Comparison table

**Note:**

*   *Secure* means that the application, by default, does not source the PKGBUILD at all, or, before doing so, reminds the user and offers him the opportunity to inspect it manually. Some helpers are known to source PKGBUILDs before the user can inspect them, allowing malicious code to be executed. *Optional* means that there is a command line flag or configuration option to prevent the automatic sourcing before viewing.
*   *Clean build* means that no new variables are exported to the build process.
*   *Git clone* means that the helper uses git clones instead of tarballs in line with AUR 4.

| Name | Written In | Git clone | Clean build | Pacman-like Syntax | Shell Tab Completion | Secure (<small>see note above</small>) | Multilingual | Specificity |
| apacman | Bash | No | Yes | Yes | No | Optional | No | Fork of packer |
| [aura](/index.php/Aura "Aura") | Haskell | No | Yes | Yes | Yes (bash/zsh/fish) | Yes | Yes | Handles backups, downgrades, ABS support |
| aurel | Emacs Lisp | No | N/A | No | No | Yes | No | Emacs integration |
| aurget | Bash | No | Yes | Yes | Yes (bash/zsh) | Optional | No | - |
| bauerbill | Python | No | Yes | Yes | Yes (bash/zsh) | Yes | No | Trust management, split package support, ABS support |
| burgaur | Python 3 | No | Yes | No | No | Optional, with [mc](/index.php/Mc "Mc") | No | Wrapper around cower |
| cower | C | No [[3]](https://github.com/falconindy/cower/commit/5b6009e7c3d006263eee5827dd247ffeefa2dbb5) | N/A | No | Yes (bash/zsh) | Yes | No | No automatic build support |
| pacaur | Bash/C | Yes | Yes | Yes | Yes (bash/zsh) | Yes | Yes | Minimizes user interaction, split package support |
| packer | Bash | No | Yes | Yes | No | Optional | No | - |
| pbget | Python 3 | No | N/A | No | No | Yes | No | No automatic build support |
| PKGBUILDer | Python 3 | Yes | Yes | Yes | No | Optional | Yes | Automatic builds by default, use -F to disable |
| prm | Bash | Yes | N/A | No | No | Yes | No | ABS support (svn) |
| trizen | Perl | No | Yes | Yes | No | Yes | No | - |
| wrapaur | Bash | Yes | Yes | No | No | Yes | No | Mirror updates, print news and AUR comments |
| yaah | Bash | Optional | N/A | No | Yes (bash) | Yes | No | No automatic build support |
| yaourt | Bash/C | Optional | No [[4]](https://lists.archlinux.org/pipermail/aur-general/2015-August/031314.html) | Yes | Yes (bash/zsh/fish) | Yes | Yes | Handles backups, ABS support |

## See also

*   [AUR helpers comparison](http://www.slant.co/topics/1447/~what-is-the-best-aur-helper-for-arch-based-linux-distributions)