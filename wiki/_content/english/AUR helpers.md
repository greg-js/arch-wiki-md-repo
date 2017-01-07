**Warning:** None of these tools are [officially](https://bbs.archlinux.org/viewtopic.php?pid=828254#p828254) supported by Arch Linux. It is recommended to become familiar with the [manual build process](/index.php/Arch_User_Repository#Installing_packages "Arch User Repository") in order to be prepared to troubleshoot problems on one's own.

AUR helpers are written to automate certain tasks for the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

## Contents

*   [1 Uploading](#Uploading)
*   [2 Build and search](#Build_and_search)
*   [3 Maintenance](#Maintenance)
*   [4 Libraries](#Libraries)
*   [5 Graphical](#Graphical)
*   [6 Comparison table](#Comparison_table)

## Uploading

*   [bbidulock's script](https://gist.github.com/bbidulock/82ab6f5347f021136054) — Migrate from a .backup directory with all packages.
*   [aur4_import.sh](https://github.com/JonnyJD/PKGBUILDs/blob/master/_bin/aur4_import.sh) — Splits a package from a git repository with multiple packages, adding/updating `.SRCINFO` for every commit.
*   [aur4_make_submodule.sh](https://github.com/JonnyJD/PKGBUILDs/blob/master/_bin/aur4_make_submodule.sh) / [subaur4](https://github.com/alexandre-mbm/arch-pkgs/blob/master/subaur4) — Replaces a package in a bigger git repository with an AUR 4 submodule, including `.SRCINFO`.
*   [import-to-aur4](https://github.com/ido/packages-archlinux/blob/master/bin/import-to-aur4.sh) — Splits an existing git repository into multiple AUR 4 packages, all at once, including `.SRCINFO` for every commit.
*   [aurpublish](https://github.com/Edenhofer/abs/blob/master/aurpublish) — Manage AUR packages as [git subtrees](https://raw.githubusercontent.com/git/git/master/contrib/subtree/git-subtree.txt). The [generation of `.SRCINFO` files, `PKGBUILD` checking](https://github.com/Edenhofer/abs/blob/master/pre-commit.hook) and the [creation of a per package commit message template](https://github.com/Edenhofer/abs/blob/master/prepare-commit-msg.hook) is left to the git hooks in the same [repo](https://github.com/Edenhofer/abs/blob/master/README.md).

## Build and search

This is a list of helper utilities that search, download and/or build packages.

*   **apacman** — A fork of packer.

	[https://github.com/oshazard/apacman](https://github.com/oshazard/apacman) || [apacman](https://aur.archlinux.org/packages/apacman/)

*   **aura** — A package manager for Arch Linux written in Haskell.

	[https://github.com/aurapm/aura](https://github.com/aurapm/aura) || [aura](https://aur.archlinux.org/packages/aura/) or [aura-bin](https://aur.archlinux.org/packages/aura-bin/) (binary)

*   **aurel** — Search, vote and download AUR packages from Emacs. ([Forum page](https://bbs.archlinux.org/viewtopic.php?id=177142))

	[https://github.com/alezost/aurel](https://github.com/alezost/aurel) || [aurel-git](https://aur.archlinux.org/packages/aurel-git/)

*   **aurget** — pacman-like interface to the AUR, without wrapping pacman commands.

	[https://github.com/pbrisbin/aurget/](https://github.com/pbrisbin/aurget/) || [aurget](https://aur.archlinux.org/packages/aurget/)

*   **aurquery** — Caching wrapper around the AUR's RPC interface using the python3-aur library.

	[http://xyne.archlinux.ca/projects/python3-aur](http://xyne.archlinux.ca/projects/python3-aur) || [python3-aur](https://aur.archlinux.org/packages/python3-aur/)

*   **aurutils** — Helper tools for the AUR. ([Forum page](https://bbs.archlinux.org/viewtopic.php?pid=1615428))

	[https://github.com/AladW/aurutils](https://github.com/AladW/aurutils) || [aurutils](https://aur.archlinux.org/packages/aurutils/)

*   **bauerbill** — Powerpill/pacman extension with support for building packages from ABS and AUR. ([Forum page](https://bbs.archlinux.org/viewtopic.php?id=205834))

	[http://xyne.archlinux.ca/projects/bauerbill](http://xyne.archlinux.ca/projects/bauerbill) || [bauerbill](https://aur.archlinux.org/packages/bauerbill/)

*   **burgaur** — A front-end for cower written in Python.

	[https://github.com/m45t3r/burgaur](https://github.com/m45t3r/burgaur) || [burgaur](https://aur.archlinux.org/packages/burgaur/)

*   **cower** — AUR search and download agent written in C, which also checks for updates and package dependencies. ([Forum page](https://bbs.archlinux.org/viewtopic.php?id=97137))

	[https://github.com/falconindy/cower](https://github.com/falconindy/cower) || [cower](https://aur.archlinux.org/packages/cower/)

*   **owlman** — pacman and cower wrapper ([Forum page](https://bbs.archlinux.org/viewtopic.php?id=129609))

	[https://github.com/baskerville/owlman](https://github.com/baskerville/owlman) || [owlman](https://aur.archlinux.org/packages/owlman/)

*   **pacaur** — An AUR helper that minimizes user interaction. ([Forum page](https://bbs.archlinux.org/viewtopic.php?pid=937423))

	[https://github.com/rmarquis/pacaur](https://github.com/rmarquis/pacaur) || [pacaur](https://aur.archlinux.org/packages/pacaur/)

*   **packer** — Wrapper for pacman and the AUR. ([Forum page](https://bbs.archlinux.org/viewtopic.php?id=88115))

	[https://github.com/keenerd/packer](https://github.com/keenerd/packer) || [packer](https://aur.archlinux.org/packages/packer/)

*   **pbget** — Retrieve source files from the Arch SVN and CVS web interface, the AUR, and the ABS rsync server.

	[http://xyne.archlinux.ca/projects/pbget](http://xyne.archlinux.ca/projects/pbget) || [pbget](https://aur.archlinux.org/packages/pbget/)

*   **PKGBUILDer** — An AUR helper with dependency support written in Python 3.

	[https://github.com/Kwpolska/pkgbuilder](https://github.com/Kwpolska/pkgbuilder) || [pkgbuilder](https://aur.archlinux.org/packages/pkgbuilder/)

*   **prm** — An AUR and ABS helper.

	[https://git.fleshless.org/prm/](https://git.fleshless.org/prm/) || [PKGBUILD](https://pkg.fleshless.org/prm/plain/PKGBUILD)

*   **repoctl** — Tool to help manage local repositories (AUR support).

	[https://github.com/cassava/repoctl](https://github.com/cassava/repoctl) || [repoctl](https://aur.archlinux.org/packages/repoctl/)

*   **spinach** — An AUR helper written in Bash

	[http://www.floft.net/code/spinach/](http://www.floft.net/code/spinach/) || [spinach](https://aur.archlinux.org/packages/spinach/)

*   **trizen** — A wrapper for the AUR written in Perl.

	[https://github.com/trizen/trizen](https://github.com/trizen/trizen) || [trizen](https://aur.archlinux.org/packages/trizen/)

*   **wrapaur** — A pacman and AUR wrapper written in bash.

	|| [wrapaur](https://aur.archlinux.org/packages/wrapaur/)

*   **yaah** — Yet another AUR helper

	[https://bitbucket.org/the_metalgamer/yaah](https://bitbucket.org/the_metalgamer/yaah) || [yaah](https://aur.archlinux.org/packages/yaah/)

*   **yaourt** — A wrapper for the AUR and regular packages.

	[https://archlinux.fr/yaourt-en](https://archlinux.fr/yaourt-en) || [yaourt](https://aur.archlinux.org/packages/yaourt/)

*   **yay** — AUR helper written in Go.

	[https://github.com/Jguer/yay](https://github.com/Jguer/yay) || [yay](https://aur.archlinux.org/packages/yay/) or [yay-bin](https://aur.archlinux.org/packages/yay-bin/) (binary)

## Maintenance

*   **pkgbuild-watch** — Looks for changes on the upstream web pages

	[http://kmkeen.com/pkgbuild-watch](http://kmkeen.com/pkgbuild-watch) || [pkgbuild-watch](https://aur.archlinux.org/packages/pkgbuild-watch/)

*   **pkgbuildup** — Helps AUR package maintainers automatically update PKGBUILD files. Supports a template variable syntax.

	[https://github.com/fasheng/pkgbuildup](https://github.com/fasheng/pkgbuildup) || [pkgbuildup-git](https://aur.archlinux.org/packages/pkgbuildup-git/)

*   **pkgcheck** — Uses rules in PKGBUILDs to parse upstream version information or looks for changes by checksumming the web page

	[https://bbs.archlinux.org/viewtopic.php?id=162816](https://bbs.archlinux.org/viewtopic.php?id=162816) || Repository: [GitHub](https://github.com/onny/pkgcheck)

*   **pkgoutofdate** — Parses the source URL from PKGBUILDs and tries to find new versions of packages by incrementing the version number and sending requests to the web server

	[https://github.com/anatol/pkgoutofdate](https://github.com/anatol/pkgoutofdate) || [pkgoutofdate-git](https://aur.archlinux.org/packages/pkgoutofdate-git/)

*   **aur-check** — Uses the AUR API to find newer versions of your foreign packages

	[https://gist.github.com/felipec/94752ddd08e1adfb80ac57947982443c](https://gist.github.com/felipec/94752ddd08e1adfb80ac57947982443c) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **updpkgver** — Detects upstream releases and updates the PKGBUILD automatically

	[https://github.com/renatosilva/pactoys/tree/master/source/updpkgver](https://github.com/renatosilva/pactoys/tree/master/source/updpkgver) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

## Libraries

*   **haskell-archlinux** — Library to access the AUR and package metadata from the Haskell programming language

	[http://hackage.haskell.org/package/archlinux](http://hackage.haskell.org/package/archlinux) || [haskell-archlinux](https://aur.archlinux.org/packages/haskell-archlinux/)

*   **python3-aur** — Python 3 modules for accessing AUR package information and automating AUR interactions.

	[http://xyne.archlinux.ca/projects/python3-aur](http://xyne.archlinux.ca/projects/python3-aur) || [python3-aur](https://aur.archlinux.org/packages/python3-aur/)

## Graphical

*   **Aarchup** — Fork of archup. Has the same options as archup plus a few other features. For differences between both please check [changelog](https://bbs.archlinux.org/viewtopic.php?id=119129).

	[https://github.com/aericson/aarchup/](https://github.com/aericson/aarchup/) || [aarchup](https://aur.archlinux.org/packages/aarchup/)

*   **Argon** — Graphical frontend to pacaur, featuring package installation, removal, and updating; and update notifications for both official repository and AUR packages.

	[https://github.com/14mRh4X0r/arch-argon](https://github.com/14mRh4X0r/arch-argon) || [argon](https://aur.archlinux.org/packages/argon/)

*   **PkgBrowser** — Application for searching and browsing Arch packages, showing details on selected packages.

	[https://bitbucket.org/kachelaqa/pkgbrowser/wiki/Home](https://bitbucket.org/kachelaqa/pkgbrowser/wiki/Home) || [pkgbrowser](https://aur.archlinux.org/packages/pkgbrowser/)

## Comparison table

The columns have the following meaning:

*   *Secure*: does not [source](/index.php/Source "Source"), by default, the PKGBUILD at all, or, before doing so, reminds the user and offers him the opportunity to inspect it manually. Some helpers are known to source PKGBUILDs before the user can inspect them, **allowing malicious code to be executed**. *Optional* means that there is a command line flag or configuration option to prevent the automatic sourcing before viewing.
*   *Clean build*: does not export new variables that can prevent a successful build process.
*   *Reliable parser*: ability to handle complex packages by using the provided metadata (RPC/.SRCINFO) instead of PKGBUILD [parsing](https://en.wikipedia.org/wiki/Parsing#Parser "w:Parsing"), such as [aws-cli-git](https://aur.archlinux.org/packages/aws-cli-git/).
*   *Reliable solver*: ability to correctly solve and build complex dependency chains, such as [plasma-git-meta](https://aur.archlinux.org/packages/plasma-git-meta/).
*   *Split packages*: ability to correctly build and install split packages independently, such as [python-nikola](https://aur.archlinux.org/packages/python-nikola/).
*   *Git clone*: uses git clones instead of downloading tarballs (deprecated since AUR 4).
*   *Syntax*: P stands for [Pacman](/index.php/Pacman "Pacman")-like, S for specific.

| Name | Written In | Secure | Clean build | Reliable parser | Reliable solver | Split packages | Git clone | Shell completion | Syntax | Specificity |
| apacman | Bash | No [[1]](https://github.com/oshazard/apacman/issues/8) | No [[2]](https://github.com/oshazard/apacman/search?utf8=%E2%9C%93&q=export) | No | No | No | No | None | P | Fork of *packer* |
| aura | Haskell | Yes | Yes | No [[3]](https://github.com/aurapm/aura/issues/14) | No | No [[4]](https://github.com/aurapm/aura/issues/353) | No | bash/zsh | P | Downgrade, [ABS](/index.php/ABS "ABS"), [powerpill](/index.php/Powerpill "Powerpill") support, multilingual, requires [ArchHaskell](/index.php/ArchHaskell "ArchHaskell") |
| aurel | Emacs Lisp | Yes | N/A | Yes | N/A | N/A | No | N/A | S | Emacs integration, no automatic builds |
| aurget | Bash | Optional | Yes | No | No | No [[5]](https://github.com/pbrisbin/aurget/issues/40) | No | bash/zsh | P | sort by votes |
| aurutils | Bash/C | Yes | Yes | Yes | Yes | Yes | Yes | zsh | S | [tsort](https://en.wikipedia.org/wiki/Topological_sorting "w:Topological sorting"), [PCRE](https://en.wikipedia.org/wiki/PCRE "w:PCRE"), [local repository](/index.php/Local_repository "Local repository"), [package signing](/index.php/Package_signing "Package signing"), [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") support |
| bauerbill | Python3 | Yes | Yes | Yes | Yes | Yes | Yes | bash/zsh | P/S | Trust management, ABS support, extends Powerpill |
| burgaur | Python3/C | Optional, with [mc](/index.php/Mc "Mc") | Yes | No | No | No | No | None | P | Wrapper for *cower* |
| cower | C | Yes | N/A | Yes | N/A | N/A | No | bash/zsh | S | No automatic builds, regex support, sort by votes/popularity |
| owlman | Bash/C | Yes | Yes | Yes | No | Partial | No | None | S | Wrapper for *cower* |
| pacaur | Bash/C | Yes | Yes | Yes | Yes | Yes | Yes | bash/zsh | P/S | Minimizes user interaction, multilingual, sort by votes/popularity |
| packer | Bash | No | Yes | No | No | No | No | None | P | - |
| pbget | Python3 | Yes | N/A | Yes | N/A | N/A | Yes | None | S | No automatic builds |
| PKGBUILDer | Python3 | Optional | Yes | Yes | Yes | Partial [[6]](https://github.com/Kwpolska/pkgbuilder/issues/39) | Yes | None | P | Automatic builds by default, use `-F` to disable; multilingual |
| prm | Bash | Yes [[7]](https://git.fleshless.org/prm/commit/?id=e7252333b07975ea40f526269ce995e375e627bf) | N/A | Yes | N/A | N/A | Yes | None | S | No automatic builds, ABS support |
| repoctl | Go | Yes | N/A | Yes [[8]](https://github.com/goulash/pacman/blob/master/aur/aur.go) | N/A | N/A | No | zsh | S | No automatic builds, local repository support |
| spinach | Bash | No [[9]](https://github.com/floft/spinach/blob/master/spinach#L287) | Yes | No | No | No | No | None | S | - |
| trizen | Perl | Yes | Yes | Yes [[10]](https://github.com/trizen/trizen/commit/7ab7ee5f9f1f5d971b731d092fc8e1dd963add4b) | No | No | No | None | P | AUR comments |
| wrapaur | Bash | Yes | Yes | No | No | No | Yes | None | S | Mirror updates, print news and AUR comments |
| yaah | Bash | Yes | N/A | Yes | N/A | N/A | Optional | bash | S | No automatic builds |
| yaourt | Bash/C | No (*yaourt -Si*) [[11]](https://github.com/archlinuxfr/yaourt/blob/f373121d23d87031a24135fee593115832d803ec/src/lib/aur.sh#L47) | No [[12]](https://lists.archlinux.org/pipermail/aur-general/2015-August/031314.html) | No | No [[13]](https://github.com/archlinuxfr/yaourt/issues/186) | No [[14]](https://github.com/archlinuxfr/yaourt/issues/85) | Optional | bash/zsh/fish | P | Backup, ABS support, AUR comments, multilingual |
| yay | Go | Yes | Yes | Yes | No | Partial | No | bash/zsh/fish | P | sort by votes |

**Note:** [Pacman](/index.php/Pacman "Pacman") 4.2\. introduced architecture specific fields. [[15]](http://allanmcrae.com/2014/12/pacman-4-2-released/) However, as of 06 April 2016, [AurJson](/index.php/AurJson "AurJson") combines all entries in a single field: [FS#48796](https://bugs.archlinux.org/task/48796). Helpers relying on the RPC may use the below workarounds to retrieve dependencies:

*   [bauerbill](https://aur.archlinux.org/packages/bauerbill/) [[16]](https://bbs.archlinux.org/viewtopic.php?pid=1617235#p1617235), [pkgbuilder](https://aur.archlinux.org/packages/pkgbuilder/) [[17]](https://github.com/Kwpolska/pkgbuilder/blob/65d9d74ef05f8996b81afb1cd005e3c337afa8b2/pkgbuilder/build.py#L198): Retrieve specific fields from [.SRCINFO](/index.php/.SRCINFO ".SRCINFO")
*   [aurutils](https://aur.archlinux.org/packages/aurutils/) [[18]](https://github.com/AladW/aurutils/issues/80), [pacaur](https://aur.archlinux.org/packages/pacaur/) [[19]](https://github.com/rmarquis/pacaur/issues/465), [trizen](https://aur.archlinux.org/packages/trizen/) [[20]](https://github.com/trizen/trizen/commit/6a8ff9dc8cc83af783b8475dfbe89988dbc8a553): Strip the `lib32-` prefix on `i686` systems