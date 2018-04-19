**Warning:**

*   AUR helpers are **not** [supported](https://bbs.archlinux.org/viewtopic.php?pid=828254#p828254) by Arch Linux. It is recommended to become familiar with the [manual build process](/index.php/Arch_User_Repository#Installing_packages "Arch User Repository") in order to be prepared to troubleshoot problems on one's own.
*   AUR helpers can replicate [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) usage for the [official repositories](/index.php/Official_repositories "Official repositories"), such as `pacman -Syu`. This usage may deviate from *pacman* in various ways; it is thus **not** supported or recommended.

AUR helpers are written to automate certain tasks for the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

## Contents

*   [1 Build and search](#Build_and_search)
    *   [1.1 Active](#Active)
    *   [1.2 Inactive](#Inactive)
    *   [1.3 Workarounds](#Workarounds)
*   [2 Libraries](#Libraries)
*   [3 Maintenance](#Maintenance)
*   [4 Uploading](#Uploading)

## Build and search

The columns have the following meaning:

*   *Secure*: does not [source](/index.php/Source "Source") the PKGBUILD at all by default; or, alerts the user and offers the opportunity to inspect the PKGBUILD manually before it is sourced. Some helpers are known to source PKGBUILDs before the user can inspect them, **allowing malicious code to be executed**. *Optional* means that there is a command line flag or configuration option to prevent the automatic sourcing before viewing.
*   *Clean build*: does not export new variables that can prevent a successful build process.
*   *Reliable parser*: ability to handle complex packages by using the provided metadata (RPC/.SRCINFO) instead of PKGBUILD [parsing](https://en.wikipedia.org/wiki/Parsing#Parser "w:Parsing"), such as [aws-cli-git](https://aur.archlinux.org/packages/aws-cli-git/).
*   *Reliable solver*: ability to correctly solve and build complex dependency chains, such as [ros-lunar-desktop](https://aur.archlinux.org/packages/ros-lunar-desktop/).
*   *Split packages*: ability to correctly build and install:

	– Multiple packages from the same package base, without rebuilding or reinstalling multiple times, such as [clion](https://aur.archlinux.org/packages/clion/)

	– Split packages which depend on a package from the same package base, such as [libc++](https://aur.archlinux.org/packages/libc%2B%2B/) and [libc++abi](https://aur.archlinux.org/packages/libc%2B%2Babi/).

	– Split packages independently, such as [python-pyalsaaudio](https://aur.archlinux.org/packages/python-pyalsaaudio/) and [python2-pyalsaaudio](https://aur.archlinux.org/packages/python2-pyalsaaudio/).

*   *Git clone*: uses [git-clone(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-clone.1) by default to retrieve build files from the AUR.
*   *Native pacman*: when used as replacement for [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) commands such as `pacman -Syu`, the following are obeyed *by default*:

	– do not separate commands, for example `pacman -Syu` is not split to `pacman -Sy` and `pacman -S *packages*`;

	– use *pacman* directly instead of manual database manipulation or usage of [libalpm(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libalpm.3).

	In addition, unsupported commands such as `pacman -Ud`, `pacman -Rdd` or `pacman --force` are **not** used.

*   *Shell completion*: [tab completion](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion") is available for the listed [shells](/index.php/Shell "Shell").

**Note:**

*   Table rows are sorted by column values, where *Yes* or *N/A* take precedence over *Partial* or *Optional* and *No*, or alphabetically if values are equal.
*   *Optional* means that a feature is available, but only through a command-line argument or configuration option. *Partial* means that a feature is not fully implemented, or that it deviates from the given criteria in a minor way.

### Active

| Name | Written In | Secure | Clean build | Reliable parser | Reliable solver | Split packages | Git clone | Native pacman | Shell completion | Specificity |
| [aurman](https://aur.archlinux.org/packages/aurman/) | Python | Yes | Yes | Yes | Yes | Yes | Yes | Yes | bash, fish | batch interaction, fetch pgp keys, sort by popularity, [deep search](https://github.com/polygamma/aurman/wiki/Description-of-the-aurman-dependency-solving) |
| [aurutils](https://aur.archlinux.org/packages/aurutils/) | Bash/C | Yes | Yes | Yes | Yes | Yes | Yes | N/A | zsh | [vifm](/index.php/Vifm "Vifm"), [PCRE](https://en.wikipedia.org/wiki/PCRE "w:PCRE"), [local repository](/index.php/Local_repository "Local repository"), [package signing](/index.php/Package_signing "Package signing"), [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") support, sort by votes/popularity |
| [bauerbill](https://aur.archlinux.org/packages/bauerbill/) | Python | Yes | Yes | Yes | Yes | Yes | Yes | Yes | bash, zsh | Trust management, ABS support, extends Powerpill |
| [pakku](https://aur.archlinux.org/packages/pakku/) | Nim | Yes | Yes [[1]](https://github.com/kitsunyan/pakku/commit/864cc0373fd6095295f68cc44d1657bd17269732) | Yes | Yes | Yes | Yes | Partial [[2]](https://github.com/kitsunyan/pakku/wiki/Pacman-Wrap-Explanation) | bash | AUR comments, batch interaction, fetch PGP keys |
| [pikaur](https://aur.archlinux.org/packages/pikaur/) | Python | Yes | Yes | Yes | Yes | Yes [[3]](https://github.com/actionless/pikaur/commit/d409b958b4ff403d4fda06681231061854d32b3c) | Yes | Partial [[4]](https://github.com/actionless/pikaur/issues/81) | bash, fish, zsh | [dynamic users](http://0pointer.net/blog/dynamic-users-with-systemd.html), multilingual, sort by votes/popularity, batch interaction |
| [PKGBUILDer](https://aur.archlinux.org/packages/PKGBUILDer/) | Python | Optional | Yes | Yes | Yes | Partial [[5]](https://github.com/Kwpolska/pkgbuilder/issues/39) | Yes | Yes [[6]](https://github.com/Kwpolska/pkgbuilder/blob/master/docs/wrapper.rst) | None | Automatic builds by default, use `-F` to disable; multilingual |
| [auracle-git](https://aur.archlinux.org/packages/auracle-git/) | C++ | Yes | N/A | Yes | Yes | N/A | No | N/A | N/A | No automatic builds |
| [package-query](https://aur.archlinux.org/packages/package-query/) | C | Yes | N/A | No [[7]](https://github.com/archlinuxfr/package-query/issues/135) | N/A | N/A | N/A | N/A | None | No automatic builds |
| [repoctl](https://aur.archlinux.org/packages/repoctl/) | Go | Yes | N/A | Yes [[8]](https://github.com/goulash/pacman/blob/master/aur/aur.go) | N/A | N/A | No | N/A | zsh | No automatic builds, local repository support |
| [trizen](https://aur.archlinux.org/packages/trizen/) | Perl | Yes | Yes | Yes [[9]](https://github.com/trizen/trizen/commit/7ab7ee5f9f1f5d971b731d092fc8e1dd963add4b) | Yes | Yes [[10]](https://github.com/trizen/trizen/commit/3c94434c66ede793758f2bf7de84d68e3174e2ac) | Yes [[11]](https://github.com/trizen/trizen/commit/6fb0cc9e0ab66b8cca9493b0618ba4bab5fd2252) | No [[12]](https://github.com/trizen/trizen/commit/ba687bc3c3e306e6f3942e95f825ed6a55d3ad69) | bash, zsh, fish | AUR comments |
| [yay](https://aur.archlinux.org/packages/yay/) | Go | Yes | Yes | Yes | Yes | Yes | No [[13]](https://github.com/Jguer/yay/pull/297) | Partial [[14]](https://github.com/Jguer/yay/commit/98ea801004fc63b5a294f46392910e85286ffd98) | bash, zsh, fish | sort by votes, batch interaction, fetch PGP keys, [prompt architecture](https://github.com/Jguer/yay/pull/260) |
| [naaman](https://aur.archlinux.org/packages/naaman/) | Python | Optional | Yes | Yes | No | No | Yes | N/A | bash | Automatic builds by default, use `--fetch` to disable |
| [aura](https://aur.archlinux.org/packages/aura/) | Haskell | Yes | Yes | Yes [[15]](https://github.com/aurapm/aura/commit/7848e9830cd880215f1d12a1c0294992428ea778) | No | No [[16]](https://github.com/aurapm/aura/issues/353) | No [[17]](https://github.com/aurapm/aura/pull/346) | Yes [[18]](https://github.com/aurapm/aura/blob/master/aura/src/Aura/Pacman.hs) | bash, zsh | Downgrade, [ABS](/index.php/ABS "ABS"), [powerpill](/index.php/Powerpill "Powerpill") support, multilingual, requires [ArchHaskell](/index.php/ArchHaskell "ArchHaskell") |

### Inactive

A project is considered *inactive* if it fullfills **any** of the following criteria:

*   it has been discontinued by the author in favor of a different project or otherwise;
*   it has seen no general activity in the last 6 months;
*   existing issues on security and clean build have been ignored in the last 6 months.

| Name | Written In | Secure | Clean build | Reliable parser | Reliable solver | Split packages | Git clone | Native pacman | Shell completion | Specificity |
| [pbget](https://aur.archlinux.org/packages/pbget/) | Python | Yes | N/A | Yes | N/A | N/A | Yes | N/A | None | No automatic builds |
| [yaah](https://aur.archlinux.org/packages/yaah/) | Bash | Yes | N/A | Yes | N/A | N/A | Optional | N/A | bash | No automatic builds |
| [aurel-git](https://aur.archlinux.org/packages/aurel-git/) [[19]](https://bbs.archlinux.org/viewtopic.php?pid=1522459#p1522459) | Emacs Lisp | Yes | N/A | Yes | N/A | N/A | No | N/A | N/A | Emacs integration, no automatic builds |
| [cower](https://aur.archlinux.org/packages/cower/) [[20]](https://github.com/falconindy/auracle#what-is-auracle) | C | Yes | N/A | Yes | N/A | N/A | No | N/A | bash/zsh | No automatic builds, regex support, sort by votes/popularity |
| [pacaur](https://aur.archlinux.org/packages/pacaur/) [[21]](https://bbs.archlinux.org/viewtopic.php?pid=1755144#p1755144) | Bash/C | Yes | Yes | Yes | Yes | Yes | Yes | No [[22]](https://github.com/rmarquis/pacaur/commit/d8f49188452785fb28afc017baadd01d9e24ba21) | bash, zsh | multilingual, sort by votes/popularity, batch interaction |
| [wrapaur](https://aur.archlinux.org/packages/wrapaur/) | Bash | Yes | Yes | No | No | No | Yes | Yes | None | Mirror updates, print news and AUR comments |
| [spinach](https://aur.archlinux.org/packages/spinach/) | Bash | Yes [[23]](https://github.com/floft/spinach/commit/545574700812eb369b9537370f085ec9e5c3f01a) | Yes | No | No | No | No | N/A | None | - |
| [aurget](https://aur.archlinux.org/packages/aurget/) | Bash | Optional | Yes | No | No | No [[24]](https://github.com/pbrisbin/aurget/issues/40) | No | N/A | bash, zsh | sort by votes |
| [burgaur](https://aur.archlinux.org/packages/burgaur/) [[25]](https://github.com/m45t3r/burgaur/issues/7#issuecomment-365599675) | Python/C | Optional | Yes | No | No | No | No | N/A | None | Wrapper for *cower* |
| [packer](https://aur.archlinux.org/packages/packer/) | Bash | No | Yes | No | No | No | No | Yes | None | - |
| [yaourt](https://aur.archlinux.org/packages/yaourt/) | Bash/C | No [[26]](https://github.com/archlinuxfr/yaourt/blob/f373121d23d87031a24135fee593115832d803ec/src/lib/aur.sh#L47) [[27]](https://github.com/archlinuxfr/yaourt/blob/d9790e29cd7194535c793f51d185b7130a396916/src/lib/pkgbuild.sh.in#L415-L438) | No [[28]](https://lists.archlinux.org/pipermail/aur-general/2015-August/031314.html) | No | No [[29]](https://github.com/archlinuxfr/yaourt/issues/186) | No [[30]](https://github.com/archlinuxfr/yaourt/issues/85) | Optional | No | bash, zsh, fish | Backup, ABS support, AUR comments, multilingual |

### Workarounds

*   [Pacman](/index.php/Pacman "Pacman") 4.2\. introduced architecture specific fields. [[32]](http://allanmcrae.com/2014/12/pacman-4-2-released/) [AurJson](/index.php/AurJson "AurJson") merges these fields to their generic counterparts, such as `depends` and `makedepends`: [FS#48796](https://bugs.archlinux.org/task/48796). The following workarounds may be used:

	– Retrieve specific fields from [.SRCINFO](/index.php/.SRCINFO ".SRCINFO"): [bauerbill](https://aur.archlinux.org/packages/bauerbill/) [[33]](https://bbs.archlinux.org/viewtopic.php?pid=1617235#p1617235), [pkgbuilder](https://aur.archlinux.org/packages/pkgbuilder/) [[34]](https://github.com/Kwpolska/pkgbuilder/blob/65d9d74ef05f8996b81afb1cd005e3c337afa8b2/pkgbuilder/build.py#L198)

	– Strip the `lib32-` prefix on `i686` systems: [aurutils](https://aur.archlinux.org/packages/aurutils/) [[35]](https://github.com/AladW/aurutils/issues/80), [pacaur](https://aur.archlinux.org/packages/pacaur/) [[36]](https://github.com/rmarquis/pacaur/issues/465), [trizen](https://aur.archlinux.org/packages/trizen/) [[37]](https://github.com/trizen/trizen/commit/6a8ff9dc8cc83af783b8475dfbe89988dbc8a553)

*   The RPC does not support querying versioned packages: [FS#54906](https://bugs.archlinux.org/task/54906). [pacaur](https://aur.archlinux.org/packages/pacaur/) and [aurman](https://aur.archlinux.org/packages/aurman/) implement this manually.

## Libraries

*   **haskell-archlinux** — Library to access the AUR and package metadata from the Haskell programming language

	[http://hackage.haskell.org/package/archlinux](http://hackage.haskell.org/package/archlinux) || [haskell-archlinux](https://aur.archlinux.org/packages/haskell-archlinux/)

*   **python3-aur** — Python 3 modules for accessing AUR package information and automating AUR interactions.

	[http://xyne.archlinux.ca/projects/python3-aur](http://xyne.archlinux.ca/projects/python3-aur) || [python3-aur](https://aur.archlinux.org/packages/python3-aur/)

## Maintenance

*   **aur-out-of-date** — Uses hoster APIs to check AUR packages for upstream changes

	[https://github.com/simon04/aur-out-of-date](https://github.com/simon04/aur-out-of-date) || [aur-out-of-date](https://aur.archlinux.org/packages/aur-out-of-date/)

*   **pkgbuild-watch** — Looks for changes on the upstream web pages

	[http://kmkeen.com/pkgbuild-watch](http://kmkeen.com/pkgbuild-watch) || [pkgbuild-watch](https://aur.archlinux.org/packages/pkgbuild-watch/)

*   **pkgbuildup** — Helps AUR package maintainers automatically update PKGBUILD files. Supports a template variable syntax.

	[https://github.com/fasheng/pkgbuildup](https://github.com/fasheng/pkgbuildup) || [pkgbuildup-git](https://aur.archlinux.org/packages/pkgbuildup-git/)

*   **pkgcheck** — Uses rules in PKGBUILDs to parse upstream version information or looks for changes by checksumming the web page

	[https://bbs.archlinux.org/viewtopic.php?id=162816](https://bbs.archlinux.org/viewtopic.php?id=162816) || Repository: [GitHub](https://github.com/onny/pkgcheck)

*   **pkgoutofdate** — Parses the source URL from PKGBUILDs and tries to find new versions of packages by incrementing the version number and sending requests to the web server

	[https://github.com/anatol/pkgoutofdate](https://github.com/anatol/pkgoutofdate) || [pkgoutofdate-git](https://aur.archlinux.org/packages/pkgoutofdate-git/)

## Uploading

*   [aur4_import.sh](https://github.com/JonnyJD/PKGBUILDs/blob/master/_bin/aur4_import.sh) — Splits a package from a git repository with multiple packages, adding/updating `.SRCINFO` for every commit.
*   [aur4_make_submodule.sh](https://github.com/JonnyJD/PKGBUILDs/blob/master/_bin/aur4_make_submodule.sh) — Replaces a package in a bigger git repository with an AUR 4 submodule, including `.SRCINFO`.
*   [aurpublish](https://github.com/Edenhofer/abs/blob/master/aurpublish) — Manage AUR packages as [git subtrees](https://raw.githubusercontent.com/git/git/master/contrib/subtree/git-subtree.txt). The [generation of `.SRCINFO` files, `PKGBUILD` checking](https://github.com/Edenhofer/abs/blob/master/pre-commit.hook) and the [creation of a per package commit message template](https://github.com/Edenhofer/abs/blob/master/prepare-commit-msg.hook) is left to the git hooks in the same [repo](https://github.com/Edenhofer/abs/blob/master/README.md).