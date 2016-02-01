# AUR helpers

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

NaN

*   **[aura](/index.php/Aura "Aura")** — A package manager for Arch Linux written in Haskell.

NaN

*   **aurel** — Search, vote and download AUR packages from Emacs. ([Forum page](https://bbs.archlinux.org/viewtopic.php?id=177142))

NaN

*   **aurget** — Aims to be a pacman-like interface to the AUR, without wrapping pacman commands.

NaN

*   **aurquery** — Caching wrapper around the AUR's RPC interface using the python3-aur library.

NaN

*   **bauerbill** — Powerpill/pacman extension with support for building packages from ABS and AUR, with full dependency resolution.

NaN

*   **burgaur** — A front-end for cower written in Python.

NaN

*   **cower** — AUR search and download agent written in C, which also checks for updates and package dependencies. ([Forum page](https://bbs.archlinux.org/viewtopic.php?id=97137))

NaN

*   **pacaur** — An AUR helper that minimizes user interaction. ([Forum page](https://bbs.archlinux.org/viewtopic.php?pid=937423))

NaN

*   **packer** — Wrapper for pacman and the AUR. ([Forum page](https://bbs.archlinux.org/viewtopic.php?id=88115))

NaN

*   **pbget** — Retrieve source files from the official SVN and CVS web interface, the AUR, and the ABS rsync server.

NaN

*   **PKGBUILDer** — An AUR helper with dependency support written in Python 3.

NaN

*   **prm** — An AUR and ABS helper.

NaN

*   **trizen** — A wrapper for the AUR written in Perl.

NaN

*   **wrapaur** — A pacman and AUR wrapper written in bash.

NaN

*   **yaah** — Yet another AUR helper

NaN

*   **yaourt** — A wrapper for the AUR and regular packages.

NaN

## Maintenance

*   **pkgbuild-watch** — Looks for changes on the upstream web pages

NaN

*   **pkgbuildup** — Helps AUR package maintainers automatically update PKGBUILD files. Supports a template variable syntax.

NaN

*   **pkgcheck** — Uses rules in PKGBUILDs to parse upstream version information or looks for changes by checksumming the web page

NaN

*   **pkgoutofdate** — Parses the source URL from PKGBUILDs and tries to find new versions of packages by incrementing the version number and sending requests to the web server

NaN

## Libraries

*   **haskell-archlinux** — Library to access the AUR and package metadata from the Haskell programming language

NaN

*   **python3-aur** — Python 3 modules for accessing AUR package information and automating AUR interactions.

NaN

## Graphical

*   **Aarchup** — Fork of archup. Has the same options as archup plus a few other features. For differences between both please check [changelog](https://bbs.archlinux.org/viewtopic.php?id=119129).

NaN

*   **PkgBrowser** — Application for searching and browsing Arch packages, showing details on selected packages.

NaN

*   **kalu** — Small C application that adds an icon in the systray and can show notifications for Arch Linux News, Upgrades, AUR upgrades, and watched (AUR) upgrades (upgrades for packages not installed). Also includes a GUI system upgrader.

NaN

*   **Yapan** — Written in C++ and Qt. It shows an icon in the system tray and popup notifications for new packages and supports AUR helpers.

NaN

## Comparison table

**Note:**

*   _Secure_ means that the application, by default, does not source the PKGBUILD at all, or, before doing so, reminds the user and offers him the opportunity to inspect it manually. Some helpers are known to source PKGBUILDs before the user can inspect them, allowing malicious code to be executed. _Optional_ means that there is a command line flag or configuration option to prevent the automatic sourcing before viewing.
*   _Clean build_ means that no new variables are exported to the build process.
*   _Git clone_ means that the helper uses git clones instead of tarballs in line with AUR 4.

| Name | Written In | Git clone | Clean build | Pacman-like Syntax | Shell Tab Completion | Secure (<small>see note above</small>) | Multilingual | Specificity |
| apacman | Bash | No | Yes | Yes | No | Optional | No | Fork of packer. |
| [aura](/index.php/Aura "Aura") | Haskell | No | Yes | Yes | Yes (bash/zsh/fish) | Yes | Yes | Handles backups, downgrades, ABS Support |
| aurel | Emacs Lisp | No | N/A | No | No | Yes | No | Emacs integration. |
| aurget | Bash | No | Yes | Yes | Yes (bash/zsh) | Optional | No | - |
| bauerbill | Python | No | Yes | Yes | Yes (bash/zsh) | Yes | No | ABS Support, full AUR searches and package lists |
| burgaur | Python 3 | No | Yes | No | No | Optional, with [mc](/index.php/Mc "Mc") | No | Wrapper around cower. |
| cower | C | No [[1]](https://github.com/falconindy/cower/commit/5b6009e7c3d006263eee5827dd247ffeefa2dbb5) | N/A | No | Yes (bash/zsh) | Yes | No | No automatic build support. |
| pacaur | Bash/C | Yes | Yes | Yes | Yes (bash/zsh) | Yes | Yes | Minimizes user interaction. |
| packer | Bash | No | Yes | Yes | No | Optional | No | - |
| pbget | Python 3 | No | N/A | No | No | Yes | No | No automatic build support. |
| PKGBUILDer | Python 3 | Yes | Yes | Yes | No | Optional | Yes | Automatic builds by default, use -F to disable |
| prm | Bash | Yes | N/A | No | No | Yes | No | ABS support (svn) |
| trizen | Perl | No | Yes | Yes | No | Yes | No | - |
| wrapaur | Bash | Yes | Yes | No | No | Yes | No | Mirror updates, print news and AUR comments |
| yaah | Bash | Optional | N/A | No | Yes (bash) | Yes | No | No automatic build support |
| yaourt | Bash/C | Optional | No [[2]](https://lists.archlinux.org/pipermail/aur-general/2015-August/031314.html) | Yes | Yes (bash/zsh/fish) | Yes | Yes | Handles backups, ABS support |

## See also

*   [AUR helpers comparison](http://www.slant.co/topics/1447/~what-is-the-best-aur-helper-for-arch-based-linux-distributions)

Retrieved from "[https://wiki.archlinux.org/index.php?title=AUR_helpers&oldid=418451](https://wiki.archlinux.org/index.php?title=AUR_helpers&oldid=418451)"