**Warning:** AUR helpers are **not** [supported](https://bbs.archlinux.org/viewtopic.php?pid=828310#p828310) by Arch Linux. You should become familiar with the [manual build process](/index.php/Arch_User_Repository#Installing_packages "Arch User Repository") in order to be prepared to troubleshoot problems.

AUR helpers automate certain tasks for using the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). Most helpers automate the process of retrieving a package's [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") from the AUR and building the package. In most cases packages installed from the AUR are not checked for updates by [pacman](/index.php/Pacman "Pacman"); thus some helpers check the AUR for updates and automate the re-build process. However, keep in mind that a rebuild of an AUR package, or any other packages built and installed locally, may be required when shared libraries are updated, not just when the package is updated.

Since AUR helpers are unsupported, they are not present in the [official repositories](/index.php/Official_repositories "Official repositories").

## Contents

*   [1 Build and search](#Build_and_search)
    *   [1.1 Active](#Active)
    *   [1.2 Search-only](#Search-only)
    *   [1.3 Discontinued or problematic](#Discontinued_or_problematic)
*   [2 Libraries](#Libraries)
*   [3 Maintenance](#Maintenance)
*   [4 Uploading](#Uploading)

## Build and search

**Note:** Do not edit this section prior to discussion in [Talk:AUR helpers](/index.php/Talk:AUR_helpers "Talk:AUR helpers").

The columns have the following meaning:

*   *Secure*: does not [source](/index.php/Source "Source") the PKGBUILD at all by default; or, alerts the user and offers the opportunity to inspect the PKGBUILD manually before it is sourced. Some helpers are known to source PKGBUILDs before the user can inspect them, **allowing malicious code to be executed**. *Optional* means that there is a command line flag or configuration option to prevent the automatic sourcing before viewing.
*   *Clean build*: does not export new variables that can prevent a successful build process.
*   *Native pacman*: when used as replacement for [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) commands such as `pacman -Syu`, the following are obeyed *by default*: [[1]](https://wiki.archlinux.org/index.php?title=Talk:AUR_helpers&oldid=515160#Add_.22pacman_wrap.22_column)

	– do not separate commands, for example `pacman -Syu` is not split to `pacman -Sy` and `pacman -S *packages*`;

	– use *pacman* directly instead of manual database manipulation or usage of [libalpm(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libalpm.3).

	In addition, potentially [harmful commands](/index.php/System_maintenance#Avoid_certain_pacman_commands "System maintenance") such as `pacman -Ud`, `pacman -Rdd`, `pacman --ask` or `pacman --force` are **not** used.

**Warning:** Notwithstanding these criteria, AUR helpers may deviate from [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) in various ways, in particular for installation of packages in the [official repositories](/index.php/Official_repositories "Official repositories"). Such usage is therefore **not** supported or recommended.

*   *Reliable parser*: ability to handle complex packages by using the provided metadata (RPC/.SRCINFO) instead of PKGBUILD [parsing](https://en.wikipedia.org/wiki/Parsing#Parser "w:Parsing"), such as [aws-cli-git](https://aur.archlinux.org/packages/aws-cli-git/).
*   *Reliable solver*: ability to correctly solve and build complex dependency chains, such as [ros-lunar-desktop](https://aur.archlinux.org/packages/ros-lunar-desktop/).
*   *Split packages*: ability to correctly build and install:

	– Multiple packages from the same package base, without rebuilding or reinstalling multiple times, such as [clion](https://aur.archlinux.org/packages/clion/)

	– Split packages which depend on a package from the same package base, such as [libc++](https://aur.archlinux.org/packages/libc%2B%2B/) and [libc++abi](https://aur.archlinux.org/packages/libc%2B%2Babi/).

	– Split packages independently, such as [python-pyalsaaudio](https://aur.archlinux.org/packages/python-pyalsaaudio/) and [python2-pyalsaaudio](https://aur.archlinux.org/packages/python2-pyalsaaudio/).

*   *Git clone*: uses [git-clone(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-clone.1) by default to retrieve build files from the AUR.
*   *Diff view*: ability to view package differences on inspection. Besides the PKGBUILD, this includes changes to files such as `.install` or `.patch` files.
*   *Batch interaction*: ability to prompt in direct succession, in particular for:

1.  Inspection of PKGBUILDs;
2.  Summarizing package upgrades;
3.  Resolution of package conflicts and installations.

	An asterisk denotes functionality specifically enabled by the user.

*   *Shell completion*: [tab completion](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion") is available for the listed [shells](/index.php/Shell "Shell").

**Note:**

*   Table rows are sorted by column values, where *Yes* or *N/A* take precedence over *Partial* or *Optional* and *No*, or alphabetically if values are equal.
*   *Optional* means that a feature is available, but only through a command-line argument or configuration option. *Partial* means that a feature is not fully implemented, or that it partially deviates from the given criteria.

### Active

| Name | Written In | Secure | Clean build | Native pacman | Reliable parser | Reliable solver | Split packages | Git clone | Diff view | Batch interaction | Shell completion | Specificity |
| [aurman](https://aur.archlinux.org/packages/aurman/) | Python | Yes | Yes | Yes | Yes | [Yes](https://github.com/polygamma/aurman/wiki/Description-of-the-aurman-dependency-solving) | Yes | Yes | Yes | 1, [2*, 3*](https://github.com/polygamma/aurman#question-5) | bash, fish | fetch PGP keys, sort by votes/popularity, print news |
| [aurutils](https://aur.archlinux.org/packages/aurutils/) | Bash/C | Yes | Yes | N/A | Yes | Yes | Yes | Yes | Yes | 1 | zsh | [vifm](/index.php/Vifm "Vifm"), [local repository](/index.php/Local_repository "Local repository"), [package signing](/index.php/Package_signing "Package signing"), [clean chroot](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot") support, sort by votes/popularity |
| [yay](https://aur.archlinux.org/packages/yay/) | Go | Yes | Yes | Yes [[2]](https://github.com/Jguer/yay/commit/3bdb5343218d99d40f8a449b887348611f6bdbfc)[[3]](https://github.com/Jguer/yay/commit/ea5a94e0f8bb5f76879099e6d319c0c0102231c2) | Yes | Yes | Yes | [Yes](https://github.com/Jguer/yay/pull/297) | [Yes](https://github.com/Jguer/yay/pull/447) | 1, [2*](https://github.com/Jguer/yay/commit/3bdb5343218d99d40f8a449b887348611f6bdbfc), [3*](https://github.com/Jguer/yay/commit/ea5a94e0f8bb5f76879099e6d319c0c0102231c2) | bash, fish, zsh | sort by votes, fetch PGP keys, [prompt architecture](https://github.com/Jguer/yay/commit/4bcd3a6297052714e91e3f886602ce5c12d15786) |
| [pakku](https://aur.archlinux.org/packages/pakku/) | Nim | Yes | [Yes](https://github.com/kitsunyan/pakku/commit/864cc0373fd6095295f68cc44d1657bd17269732) | [Partial](https://github.com/kitsunyan/pakku/wiki/Native-Pacman-Explanation) | Yes | Yes | Yes | Yes | [Yes](https://github.com/kitsunyan/pakku/commit/396e9f44c4f5a79c7b9238835599387f6ff418fe) | 1 | bash, zsh | [ABS](/index.php/ABS "ABS") support, AUR comments, fetch PGP keys |
| [pikaur](https://aur.archlinux.org/packages/pikaur/) | Python | Yes | Yes | [Partial](https://github.com/actionless/pikaur#pikaur) | Yes | Yes | [Yes](https://github.com/actionless/pikaur/commit/d409b958b4ff403d4fda06681231061854d32b3c) | Yes | Yes | 1, 2, 3 | bash, fish, zsh | [dynamic users](http://0pointer.net/blog/dynamic-users-with-systemd.html), [multilingual](https://github.com/actionless/pikaur/tree/master/locale), sort by votes/popularity, [print news](https://github.com/actionless/pikaur/pull/191) |
| [trizen](https://aur.archlinux.org/packages/trizen/) | Perl | Yes | Yes | [Yes](https://github.com/trizen/trizen/commit/9e7b40e110175ea5bc7a0fa002ffadbf1106704b) | [Yes](https://github.com/trizen/trizen/commit/7ab7ee5f9f1f5d971b731d092fc8e1dd963add4b) | Yes | [Partial](https://github.com/trizen/trizen/issues/46) | [Yes](https://github.com/trizen/trizen/commit/6fb0cc9e0ab66b8cca9493b0618ba4bab5fd2252) | Yes | 1* | bash, zsh, fish | Automatic builds by default, use `-G` to disable, AUR comments |
| [bauerbill](https://aur.archlinux.org/packages/bauerbill/) | Python | Yes | Yes | Yes | Yes | Yes | Yes | Yes | No | 1 | bash, zsh | Trust management, [ABS](/index.php/ABS "ABS") support, extends Powerpill |
| [PKGBUILDer](https://aur.archlinux.org/packages/PKGBUILDer/) | Python | Optional | Yes | [Yes](https://github.com/Kwpolska/pkgbuilder/blob/master/docs/wrapper.rst) | Yes | Yes | [Partial](https://github.com/Kwpolska/pkgbuilder/issues/39) | Yes | [No](https://github.com/Kwpolska/pkgbuilder/issues/36) | 1* | - | Automatic builds by default, use `-F` to disable; multilingual |
| [naaman](https://aur.archlinux.org/packages/naaman/) | Python | Optional | Yes | N/A | Yes | [Partial](https://github.com/enckse/naaman/issues/19) | [Partial](https://github.com/enckse/naaman/issues/20) | Yes | No | 1* | bash | Automatic builds by default, use `--fetch` to disable, use `-d` to enable the solver |
| [aura](https://aur.archlinux.org/packages/aura/) | Haskell | Optional | Yes | [Yes](https://github.com/aurapm/aura/blob/master/aura/src/Aura/Pacman.hs) | [Yes](https://github.com/aurapm/aura/commit/7848e9830cd880215f1d12a1c0294992428ea778) | No | [No](https://github.com/aurapm/aura/issues/353) | [No](https://github.com/aurapm/aura/pull/346) | [Partial](https://github.com/aurapm/aura/blob/89bf702bd0539fa757265c4c54ea2192155f85ed/aura/src/Aura/Pkgbuild/Records.hs) | 1* | bash, zsh | Automatic builds by default, use `--dryrun` to disable, [downgrade](/index.php/Downgrade "Downgrade") support, multilingual |
| [repofish](https://aur.archlinux.org/packages/repofish/) | Bash | Optional | Yes | N/A | No | No | No | Yes | Yes | 1* | - | Automatic builds by default, use `check` or `update` to disable, [local repository](/index.php/Local_repository "Local repository") support |
| [wrapaur](https://aur.archlinux.org/packages/wrapaur/) | Bash | Yes | Yes | Yes | No | No | No | Yes | No | - | - | Mirror updates, print news and AUR comments |
| [aurget](https://aur.archlinux.org/packages/aurget/) | Bash | Optional | Yes | N/A | No | No | [No](https://github.com/pbrisbin/aurget/issues/40) | No | [No](https://github.com/pbrisbin/aurget/issues/41) | - | bash, zsh | sort by votes |

### Search-only

| Name | Written In | Secure | Reliable parser | Reliable solver | Git clone | Shell completion | Specificity |
| [pbget](https://aur.archlinux.org/packages/pbget/) | Python | Yes | Yes | N/A | Yes | - | - |
| [yaah](https://aur.archlinux.org/packages/yaah/) | Bash | Yes | Yes | N/A | Optional | bash | - |
| [auracle-git](https://aur.archlinux.org/packages/auracle-git/) | C++ | Yes | Yes | Yes | No | - | print build order |
| [cower](https://aur.archlinux.org/packages/cower/) | C | Yes | Yes | N/A | No | bash/zsh | regex support, sort by votes/popularity |
| [package-query](https://aur.archlinux.org/packages/package-query/) | C | Yes | No [[4]](https://github.com/archlinuxfr/package-query/issues/135) | N/A | N/A | - | - |
| [repoctl](https://aur.archlinux.org/packages/repoctl/) | Go | Yes | Yes [[5]](https://github.com/goulash/pacman/blob/master/aur/aur.go) | N/A | No | zsh | local repository support |

### Discontinued or problematic

This table describes projects which either are discontinued by their authors, or have issues on *Security*, *Clean build* or *Native pacman* (see [#Build_and_search](#Build_and_search)) unaddressed in the last 6 months.

| Name | Written In | Secure | Clean build | Native pacman | Reliable parser | Reliable solver | Split packages | Git clone | Diff view | Batch interaction | Shell completion | Specificity |
| [aurel](https://aur.archlinux.org/packages/aurel/) [[6]](https://bbs.archlinux.org/viewtopic.php?pid=1522459#p1522459) | Emacs Lisp | Yes | N/A | N/A | N/A | N/A | N/A | No | N/A | N/A | N/A | Emacs integration, no automatic builds |
| [pacaur](https://aur.archlinux.org/packages/pacaur/) [[7]](https://bbs.archlinux.org/viewtopic.php?pid=1755144#p1755144) | Bash/C | Yes | Yes | [No](https://github.com/rmarquis/pacaur/commit/d8f49188452785fb28afc017baadd01d9e24ba21) | Yes | Yes | Yes | Yes | Yes | 1, 3 | bash, zsh | multilingual, sort by votes/popularity |
| [spinach](https://aur.archlinux.org/packages/spinach/) [[8]](https://github.com/floft/spinach) | Bash | [Yes](https://github.com/floft/spinach/commit/545574700812eb369b9537370f085ec9e5c3f01a) | Yes | N/A | No | No | No | No | No | - | - | - |
| [burgaur](https://aur.archlinux.org/packages/burgaur/) [[9]](https://github.com/m45t3r/burgaur/issues/7#issuecomment-365599675) | Python/C | Optional | Yes | N/A | No | No | No | No | No | - | - | Wrapper for *cower* |
| [packer](https://aur.archlinux.org/packages/packer/) | Bash | No | Yes | Yes | No | No | No | No | No | - | - | - |
| [yaourt](https://aur.archlinux.org/packages/yaourt/) | Bash/C | No [[10]](https://github.com/archlinuxfr/yaourt/blob/f373121d23d87031a24135fee593115832d803ec/src/lib/aur.sh#L47) [[11]](https://github.com/archlinuxfr/yaourt/blob/d9790e29cd7194535c793f51d185b7130a396916/src/lib/pkgbuild.sh.in#L415-L438) | [No](https://lists.archlinux.org/pipermail/aur-general/2015-August/031314.html) | No | No | [No](https://github.com/archlinuxfr/yaourt/issues/186) | [No](https://github.com/archlinuxfr/yaourt/issues/85) | Optional | Optional | 2 | bash, zsh, fish | Backup, ABS support, print AUR comments, multilingual |

## Libraries

*   **haskell-archlinux** — Library to access the AUR and package metadata from the Haskell programming language.

	[http://hackage.haskell.org/package/archlinux](http://hackage.haskell.org/package/archlinux) || [haskell-archlinux](https://aur.archlinux.org/packages/haskell-archlinux/)

*   **python3-aur** — Python 3 modules for accessing AUR package information and automating AUR interactions.

	[http://xyne.archlinux.ca/projects/python3-aur](http://xyne.archlinux.ca/projects/python3-aur) || [python3-aur](https://aur.archlinux.org/packages/python3-aur/)

## Maintenance

*   **aur-out-of-date** — Uses hoster APIs to check AUR packages for upstream changes.

	[https://github.com/simon04/aur-out-of-date](https://github.com/simon04/aur-out-of-date) || [aur-out-of-date](https://aur.archlinux.org/packages/aur-out-of-date/)

*   **pkgbuild-watch** — Looks for changes on the upstream web pages.

	[http://kmkeen.com/pkgbuild-watch](http://kmkeen.com/pkgbuild-watch) || [pkgbuild-watch](https://aur.archlinux.org/packages/pkgbuild-watch/)

*   **pkgbuildup** — Helps AUR package maintainers automatically update PKGBUILD files. Supports a template variable syntax.

	[https://github.com/fasheng/pkgbuildup](https://github.com/fasheng/pkgbuildup) || [pkgbuildup-git](https://aur.archlinux.org/packages/pkgbuildup-git/)

*   **pkgoutofdate** — Parses the source URL from PKGBUILDs and tries to find new versions of packages by incrementing the version number and sending requests to the web server.

	[https://github.com/anatol/pkgoutofdate](https://github.com/anatol/pkgoutofdate) || [pkgoutofdate-git](https://aur.archlinux.org/packages/pkgoutofdate-git/)

## Uploading

*   [aur4_import.sh](https://github.com/JonnyJD/PKGBUILDs/blob/master/_bin/aur4_import.sh) — Splits a package from a git repository with multiple packages, adding/updating `.SRCINFO` for every commit
*   [aur4_make_submodule.sh](https://github.com/JonnyJD/PKGBUILDs/blob/master/_bin/aur4_make_submodule.sh) — Replaces a package in a bigger git repository with an AUR 4 submodule, including `.SRCINFO`
*   [aurpublish](https://github.com/eli-schwartz/aurpublish) — PKGBUILD management framework for AUR