# AUR helpers

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

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

<table class="wikitable">

<tbody>

<tr>

<th>Script</th>

<th>Description</th>

</tr>

<tr>

<td>[bbidulock's script](https://gist.github.com/bbidulock/82ab6f5347f021136054)</td>

<td>Migrate from a .backup directory with all packages.</td>

</tr>

<tr>

<td>[aur4_import.sh](https://github.com/JonnyJD/PKGBUILDs/blob/master/_bin/aur4_import.sh)</td>

<td>Splits a package from a git repository with multiple packages, adding/updating `.SRCINFO` for every commit.</td>

</tr>

<tr>

<td>

[aur4_make_submodule.sh](https://github.com/JonnyJD/PKGBUILDs/blob/master/_bin/aur4_make_submodule.sh)  
[subaur4](https://github.com/alexandre-mbm/arch-pkgs/blob/master/subaur4)

</td>

<td>Replaces a package in a bigger git repository with an AUR 4 submodule, including `.SRCINFO`.</td>

</tr>

<tr>

<td>[import-to-aur4](https://github.com/ido/packages-archlinux/blob/master/bin/import-to-aur4.sh)</td>

<td>Splits an existing git repository into multiple AUR 4 packages, all at once, including `.SRCINFO` for every commit.</td>

</tr>

</tbody>

</table>

## Build and search

This is a list of helper utilities that search and/or build packages.

*   **apacman** — A fork of packer with additional features and bugfixes.

[https://github.com/oshazard/apacman](https://github.com/oshazard/apacman) || [apacman](https://aur.archlinux.org/packages/apacman/)<sup><small>AUR</small></sup>

*   **[aura](/index.php/Aura "Aura")** — A package manager for Arch Linux written in Haskell.

[https://github.com/fosskers/aura](https://github.com/fosskers/aura) || [aura](https://aur.archlinux.org/packages/aura/)<sup><small>AUR</small></sup> or [aura-bin](https://aur.archlinux.org/packages/aura-bin/)<sup><small>AUR</small></sup> (binary)

*   **aurel** — Search, vote and download AUR packages from Emacs. ([Forum page](https://bbs.archlinux.org/viewtopic.php?id=177142))

[https://github.com/alezost/aurel](https://github.com/alezost/aurel) || [aurel](https://aur.archlinux.org/packages/aurel/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/aurel)]</sup>

*   **aurget** — Aims to be a pacman-like interface to the AUR, without wrapping pacman commands.

[http://github.com/pbrisbin/aurget/](http://github.com/pbrisbin/aurget/) || [aurget](https://aur.archlinux.org/packages/aurget/)<sup><small>AUR</small></sup>

*   **aurquery** — Caching wrapper around the AUR's RPC interface using the python3-aur library.

[http://xyne.archlinux.ca/projects/python3-aur](http://xyne.archlinux.ca/projects/python3-aur) || [python3-aur](https://aur.archlinux.org/packages/python3-aur/)<sup><small>AUR</small></sup>

*   **bauerbill** — Powerpill/pacman extension with support for building packages from ABS and AUR, with full dependency resolution.

[http://xyne.archlinux.ca/projects/bauerbill](http://xyne.archlinux.ca/projects/bauerbill) || [bauerbill](https://aur.archlinux.org/packages/bauerbill/)<sup><small>AUR</small></sup>

*   **burgaur** — A front-end for cower written in Python.

[https://github.com/m45t3r/burgaur](https://github.com/m45t3r/burgaur) || [burgaur](https://aur.archlinux.org/packages/burgaur/)<sup><small>AUR</small></sup>

*   **cower** — AUR search and download agent written in C, which also checks for updates and package dependencies. ([Forum page](https://bbs.archlinux.org/viewtopic.php?id=97137))

[https://github.com/falconindy/cower](https://github.com/falconindy/cower) || [cower](https://aur.archlinux.org/packages/cower/)<sup><small>AUR</small></sup>

*   **pacaur** — An AUR helper that minimizes user interaction. ([Forum page](https://bbs.archlinux.org/viewtopic.php?pid=937423))

[https://github.com/Spyhawk/pacaur](https://github.com/Spyhawk/pacaur) || [pacaur](https://aur.archlinux.org/packages/pacaur/)<sup><small>AUR</small></sup>

*   **packer** — Wrapper for pacman and the AUR. ([Forum page](https://bbs.archlinux.org/viewtopic.php?id=88115))

[https://github.com/keenerd/packer](https://github.com/keenerd/packer) || [packer](https://aur.archlinux.org/packages/packer/)<sup><small>AUR</small></sup>

*   **pbget** — Retrieve source files from the official SVN and CVS web interface, the AUR, and the ABS rsync server.

[http://xyne.archlinux.ca/projects/pbget](http://xyne.archlinux.ca/projects/pbget) || [pbget](https://aur.archlinux.org/packages/pbget/)<sup><small>AUR</small></sup>

*   **PKGBUILDer** — An AUR helper with dependency support written in Python 3.

[https://github.com/Kwpolska/pkgbuilder](https://github.com/Kwpolska/pkgbuilder) || [pkgbuilder](https://aur.archlinux.org/packages/pkgbuilder/)<sup><small>AUR</small></sup>

*   **prm** — An AUR and ABS helper.

[https://git.fleshless.org/prm/](https://git.fleshless.org/prm/) || [PKGBUILD](https://pkg.fleshless.org/prm/plain/PKGBUILD)

*   **trizen** — A wrapper for the AUR written in Perl.

[https://github.com/trizen/trizen](https://github.com/trizen/trizen) || [trizen](https://aur.archlinux.org/packages/trizen/)<sup><small>AUR</small></sup>

*   **wrapaur** — A pacman and AUR wrapper written in bash.

[https://aur.archlinux.org/packages/wrapaur/](https://aur.archlinux.org/packages/wrapaur/) || [wrapaur](https://aur.archlinux.org/packages/wrapaur/)<sup><small>AUR</small></sup>

*   **yaah** — Yet another AUR helper

[https://bitbucket.org/the_metalgamer/yaah](https://bitbucket.org/the_metalgamer/yaah) || [yaah](https://aur.archlinux.org/packages/yaah/)<sup><small>AUR</small></sup>

*   **[yaourt](/index.php/Yaourt "Yaourt")** — A wrapper for the AUR and regular packages.

[http://archlinux.fr/yaourt-en](http://archlinux.fr/yaourt-en) || [yaourt](https://aur.archlinux.org/packages/yaourt/)<sup><small>AUR</small></sup>

## Maintenance

*   **pkgbuild-watch** — Looks for changes on the upstream web pages

[http://kmkeen.com/pkgbuild-watch](http://kmkeen.com/pkgbuild-watch) || [pkgbuild-watch](https://aur.archlinux.org/packages/pkgbuild-watch/)<sup><small>AUR</small></sup>

*   **pkgbuildup** — Help AUR package maintainers automatically update PKGBUILD files. Supports a simple template variable syntax

Repository: [GitHub](https://github.com/fasheng/pkgbuildup) || [pkgbuildup-git](https://aur.archlinux.org/packages/pkgbuildup-git/)<sup><small>AUR</small></sup>

*   **pkgcheck** — Uses rules in PKGBUILDs to parse upstream version information or looks for changes by checksumming the web page

[https://bbs.archlinux.org/viewtopic.php?id=162816](https://bbs.archlinux.org/viewtopic.php?id=162816) || Repository: [GitHub](https://github.com/onny/pkgcheck)

*   **pkgoutofdate** — Parses the source URL from PKGBUILDs and tries to find new versions of packages by incrementing the version number and sending requests to the web server

Repository: [GitHub](https://github.com/anatol/pkgoutofdate) || [pkgoutofdate-git](https://aur.archlinux.org/packages/pkgoutofdate-git/)<sup><small>AUR</small></sup>

## Libraries

*   **haskell-archlinux** — library to programmatically access the AUR and package metadata from the Haskell programming language

[http://hackage.haskell.org/package/archlinux](http://hackage.haskell.org/package/archlinux) || [haskell-archlinux](https://aur.archlinux.org/packages/haskell-archlinux/)<sup><small>AUR</small></sup>

*   **python3-aur** — Python 3 modules for accessing AUR package information and automating AUR interactions.

[http://xyne.archlinux.ca/projects/python3-aur](http://xyne.archlinux.ca/projects/python3-aur) || [python3-aur](https://aur.archlinux.org/packages/python3-aur/)<sup><small>AUR</small></sup>

## Graphical

*   **Aarchup** — Fork of archup. Has the same options as archup plus a few other features. For differences between both please check [changelog](https://bbs.archlinux.org/viewtopic.php?id=119129).

[https://github.com/aericson/aarchup/](https://github.com/aericson/aarchup/) || [aarchup](https://aur.archlinux.org/packages/aarchup/)<sup><small>AUR</small></sup>

*   **PkgBrowser** — Application for searching and browsing Arch packages, showing details on selected packages.

[https://bitbucket.org/kachelaqa/pkgbrowser/wiki/Home](https://bitbucket.org/kachelaqa/pkgbrowser/wiki/Home) || [pkgbrowser](https://aur.archlinux.org/packages/pkgbrowser/)<sup><small>AUR</small></sup>

*   **kalu** — Small C application that adds an icon in the systray and can show notifications for Arch Linux News, Upgrades, AUR upgrades, and watched (AUR) upgrades (upgrades for packages not installed). Also includes a GUI system upgrader.

[https://github.com/jjk-jacky/kalu](https://github.com/jjk-jacky/kalu) || [kalu](https://aur.archlinux.org/packages/kalu/)<sup><small>AUR</small></sup>

*   **Yapan** — Written in C++ and Qt. It shows an icon in the system tray and popup notifications for new packages and supports AUR helpers.

[https://github.com/fluxer/arch-yapan](https://github.com/fluxer/arch-yapan) || [yapan](https://aur.archlinux.org/packages/yapan/)<sup><small>AUR</small></sup>

## Comparison table

**Note:**

*   _Secure_ means that the application, by default, does not source the PKGBUILD at all, or, before doing it, reminds the user and offers him the opportunity to inspect it manually. Some helpers are known to source PKGBUILDs before the user can inspect them, allowing malicious code to be executed. Optional means that there is a command line flag or configuration option to prevent the automatic sourcing before viewing.
*   _Clean build_ means that no new variables are exported to the build process.
*   _Git clone_ means that the helper uses git clones instead of tarballs in line with AUR 4.

<table class="wikitable">

<tbody>

<tr>

<th>Name</th>

<th>Written In</th>

<th>Git clone</th>

<th>Clean build</th>

<th>Pacman-like Syntax</th>

<th>Shell Tab Completion</th>

<th>Secure (<small>see note above</small>)</th>

<th>Multilingual</th>

<th>Specificity</th>

</tr>

<tr>

<th>apacman</th>

<td>Bash</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #ffa; color: inherit; vertical-align: middle; text-align: center;">Optional</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>Fork of packer.</td>

</tr>

<tr>

<th>[aura](/index.php/Aura "Aura")</th>

<td>Haskell</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes (bash/zsh/fish)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td>Handles backups, downgrades, ABS Support</td>

</tr>

<tr>

<th>aurel</th>

<td>Emacs Lisp</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #aaf; color: inherit; vertical-align: middle; text-align: center;">N/A</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>Emacs integration.</td>

</tr>

<tr>

<th>aurget</th>

<td>Bash</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes (bash/zsh)</td>

<td style="background: #ffa; color: inherit; vertical-align: middle; text-align: center;">Optional</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>-</td>

</tr>

<tr>

<th>bauerbill</th>

<td>Python</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes (bash/zsh)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>ABS Support, full AUR searches and package lists</td>

</tr>

<tr>

<th>burgaur</th>

<td>Python 3</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #ffa; color: inherit; vertical-align: middle; text-align: center;">Optional, with [mc](/index.php/Mc "Mc")</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>Wrapper around cower.</td>

</tr>

<tr>

<th>cower</th>

<td>C</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No [[1]](https://github.com/falconindy/cower/commit/5b6009e7c3d006263eee5827dd247ffeefa2dbb5)</td>

<td style="background: #aaf; color: inherit; vertical-align: middle; text-align: center;">N/A</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes (bash/zsh)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>No automatic build support.</td>

</tr>

<tr>

<th>pacaur</th>

<td>Bash/C</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes (bash/zsh)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td>Minimizes user interaction.</td>

</tr>

<tr>

<th>packer</th>

<td>Bash</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #ffa; color: inherit; vertical-align: middle; text-align: center;">Optional</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>-</td>

</tr>

<tr>

<th>pbget</th>

<td>Python 3</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #aaf; color: inherit; vertical-align: middle; text-align: center;">N/A</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>No automatic build support.</td>

</tr>

<tr>

<th>PKGBUILDer</th>

<td>Python 3</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #ffa; color: inherit; vertical-align: middle; text-align: center;">Optional</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td>Automatic builds by default, use -F to disable</td>

</tr>

<tr>

<th>prm</th>

<td>Bash</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #aaf; color: inherit; vertical-align: middle; text-align: center;">N/A</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>ABS support (svn)</td>

</tr>

<tr>

<th>trizen</th>

<td>Perl</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>-</td>

</tr>

<tr>

<th>wrapaur</th>

<td>Bash</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>Mirror updates, print news and AUR comments</td>

</tr>

<tr>

<th>yaah</th>

<td>Bash</td>

<td style="background: #ffa; color: inherit; vertical-align: middle; text-align: center;">Optional</td>

<td style="background: #aaf; color: inherit; vertical-align: middle; text-align: center;">N/A</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes (bash)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>No automatic build support</td>

</tr>

<tr>

<th>[yaourt](/index.php/Yaourt "Yaourt")</th>

<td>Bash/C</td>

<td style="background: #ffa; color: inherit; vertical-align: middle; text-align: center;">Optional</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No [[2]](https://lists.archlinux.org/pipermail/aur-general/2015-August/031314.html)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes (bash/zsh/fish)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td>Handles backups, ABS support</td>

</tr>

</tbody>

</table>

## See also

*   [AUR helpers comparison](http://www.slant.co/topics/1447/~what-is-the-best-aur-helper-for-arch-based-linux-distributions)

Retrieved from "[https://wiki.archlinux.org/index.php?title=AUR_helpers&oldid=413185](https://wiki.archlinux.org/index.php?title=AUR_helpers&oldid=413185)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Arch User Repository](/index.php/Category:Arch_User_Repository "Category:Arch User Repository")