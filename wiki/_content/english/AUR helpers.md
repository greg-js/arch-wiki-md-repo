**Warning:** AUR helpers are **not** [supported](https://bbs.archlinux.org/viewtopic.php?pid=828310#p828310) by Arch Linux. You should become familiar with the [manual build process](/index.php/Arch_User_Repository#Installing_packages "Arch User Repository") in order to be prepared to troubleshoot problems.

AUR helpers automate certain tasks for using the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). Most helpers automate the process of retrieving a package's [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") from the AUR and building the package. In most cases packages installed from the AUR are not checked for updates by [pacman](/index.php/Pacman "Pacman"); thus some helpers check the AUR for updates and automate the re-build process. However, keep in mind that a rebuild of an AUR package, or any other packages built and installed locally, may be required when shared libraries are updated, not just when the package is updated.

Since AUR helpers are unsupported, they are not present in the [official repositories](/index.php/Official_repositories "Official repositories").

## Contents

*   [1 Legend](#Legend)
*   [2 Search-only](#Search-only)
*   [3 Build and search](#Build_and_search)
*   [4 Pacman wrappers](#Pacman_wrappers)
*   [5 Graphical](#Graphical)
*   [6 Libraries](#Libraries)
*   [7 Maintenance](#Maintenance)
*   [8 Uploading](#Uploading)

## Legend

**Note:** Do not edit this section prior to discussion in [Talk:AUR helpers](/index.php/Talk:AUR_helpers "Talk:AUR helpers").

The columns have the following meaning:

*   *File review*: does not [source](/index.php/Source "Source") the PKGBUILD at all by default; or, alerts the user and offers the opportunity to inspect the PKGBUILD manually before it is sourced. Some helpers are known to source PKGBUILDs before the user can inspect them, **allowing malicious code to be executed**. *Optional* means that there is a command line flag or configuration option to prevent the automatic sourcing before viewing.
*   *Diff view*: ability to view package differences on inspection. Besides the PKGBUILD, this includes changes to files such as `.install` or `.patch` files.
*   *Git clone*: uses [git-clone(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-clone.1) by default to retrieve build files from the AUR.
*   *Reliable parser*: ability to handle complex packages by using the provided metadata (RPC/.SRCINFO) instead of PKGBUILD [parsing](https://en.wikipedia.org/wiki/Parsing#Parser "w:Parsing"), such as [aws-cli-git](https://aur.archlinux.org/packages/aws-cli-git/).
*   *Reliable solver*: ability to correctly solve and build complex dependency chains, such as [ros-lunar-desktop](https://aur.archlinux.org/packages/ros-lunar-desktop/).
*   *Split packages*: ability to correctly build and install:

	– Multiple packages from the same package base, without rebuilding or reinstalling multiple times, such as [clion](https://aur.archlinux.org/packages/clion/)

	– Split packages which depend on a package from the same package base, such as [libc++](https://aur.archlinux.org/packages/libc%2B%2B/) and [libc++abi](https://aur.archlinux.org/packages/libc%2B%2Babi/).

	– Split packages independently, such as [python-pyalsaaudio](https://aur.archlinux.org/packages/python-pyalsaaudio/) and [python2-pyalsaaudio](https://aur.archlinux.org/packages/python2-pyalsaaudio/).

*   *Clean build*: does not export new variables that can prevent a successful build process.
*   *Batch interaction*: ability to prompt before the build process, in particular:

1.  Inspection of package files or their differences;
2.  Summary of package upgrades;
3.  Resolution of package conflicts and installations.

	An asterisk denotes functionality specifically enabled by the user.

*   *Shell completion*: [tab completion](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion") is available for the listed [shells](/index.php/Shell "Shell").

**Note:**

*   Table rows are sorted by column values, where *Yes* or *N/A* take precedence over *Partial* or *Optional* and *No*, or alphabetically if values are equal.
*   *Optional* means that a feature is available, but only through a command-line argument or configuration option. *Partial* means that a feature is not fully implemented, or that it partially deviates from the given criteria.

## Search-only

| Name | Written in | File review | Git clone | Reliable parser | Reliable solver | Shell completion | Specificity |
| [pbget](https://aur.archlinux.org/packages/pbget/) | Python | Yes | Yes | Yes | – | – | – |
| [yaah](https://aur.archlinux.org/packages/yaah/) | Bash | Yes | Optional | Yes | – | bash | – |
| [auracle-git](https://aur.archlinux.org/packages/auracle-git/) | C++ | Yes | No | Yes | Yes | – | print build order |
| [cower](https://aur.archlinux.org/packages/cower/) | C | Yes | No | Yes | – | bash, zsh | regex support, sort by votes/popularity |
| [package-query](https://aur.archlinux.org/packages/package-query/) | C | Yes | – | [No](https://github.com/archlinuxfr/package-query/issues/135) | – | – | – |
| [repoctl](https://aur.archlinux.org/packages/repoctl/) | Go | Yes | No | [Yes](https://github.com/goulash/pacman/blob/master/aur/aur.go) | – | zsh | local repository support |
| [aurel](https://aur.archlinux.org/packages/aurel/)
<small>([discontinued](https://bbs.archlinux.org/viewtopic.php?pid=1522459#p1522459))</small> | Emacs Lisp | Yes | No | Yes | – | – | Emacs integration |

## Build and search

| Name | Written in | File review | Diff view | Git clone | Reliable parser | Reliable solver | Split packages | Clean build | Batch interaction | Shell completion | Specificity |
| [aurutils](https://aur.archlinux.org/packages/aurutils/) | Bash/C | Yes | Yes | Yes | Yes | Yes | Yes | Yes | 1 | zsh | [vifm](/index.php/Vifm "Vifm"), [local repository](/index.php/Local_repository "Local repository"), [package signing](/index.php/Package_signing "Package signing"), [clean chroot](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot") support, sort by votes/popularity |
| [bauerbill](https://aur.archlinux.org/packages/bauerbill/) | Python | Yes | No | Yes | Yes | Yes | Yes | Yes | 1 | bash, zsh | trust management, [ABS](/index.php/ABS "ABS") support, extends *powerpill*, `bb-wrapper` for *pacman* wrapping |
| [PKGBUILDer](https://aur.archlinux.org/packages/PKGBUILDer/) | Python | Optional | [No](https://github.com/Kwpolska/pkgbuilder/issues/36) | Yes | Yes | Yes | [Partial](https://github.com/Kwpolska/pkgbuilder/issues/39) | Yes | 1* | – | automatic builds by default, use `-F` to disable; multilingual, `pb-wrapper` for *pacman* wrapping |
| [naaman](https://aur.archlinux.org/packages/naaman/) | Python | Optional | No | Yes | Yes | [Partial](https://github.com/enckse/naaman/issues/19) | [Partial](https://github.com/enckse/naaman/issues/20) | Yes | 1* | bash | automatic builds by default, use `--fetch` to disable; use `-d` to enable the solver |
| [repofish](https://aur.archlinux.org/packages/repofish/) | Bash | Optional | Yes | Yes | No | No | No | Yes | 1* | – | automatic builds by default, use `check` or `update` to disable; [local repository](/index.php/Local_repository "Local repository") support |
| [aurget](https://aur.archlinux.org/packages/aurget/) | Bash | Optional | [No](https://github.com/pbrisbin/aurget/issues/41) | No | No | No | [No](https://github.com/pbrisbin/aurget/issues/40) | Yes | – | bash, zsh | sort by votes |
| [spinach](https://aur.archlinux.org/packages/spinach/)
<small>([discontinued](https://github.com/floft/spinach))</small> | Bash | [Yes](https://github.com/floft/spinach/commit/5455747) | No | No | No | No | No | Yes | – | – | – |
| [burgaur](https://aur.archlinux.org/packages/burgaur/)
<small>([discontinued](https://github.com/m45t3r/burgaur/issues/7#issuecomment-365599675))</small> | Python/C | Optional | No | No | No | No | No | Yes | – | – | wrapper for *cower* |

## Pacman wrappers

**Warning:** [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) wrappers abstract the work of the package manager. They may (optionally or by default) introduce [unsafe flags](/index.php/System_maintenance#Avoid_certain_pacman_commands "System maintenance"), or other unexpected behavior leading to a defective system.

| Name | Written in | File review | Diff view | Git clone | Reliable parser | Reliable solver | Split packages | Clean build | Unsafe flags | Batch interaction | Shell completion | Specificity |
| [yay](https://aur.archlinux.org/packages/yay/) | Go | Yes | [Yes](https://github.com/Jguer/yay/pull/447) | [Yes](https://github.com/Jguer/yay/pull/297) | Yes | Yes | Yes | Yes | [`-Sy`*](https://github.com/Jguer/yay/commit/3bdb534)
[`--ask`*](https://github.com/Jguer/yay/commit/ea5a94e) | 1, [2*](https://github.com/Jguer/yay/commit/3bdb534), [3*](https://github.com/Jguer/yay/commit/ea5a94e) | bash, fish, zsh | fetch PGP keys, sort by votes/popularity, [prompt architecture](https://github.com/Jguer/yay/commit/4bcd3a6) |
| [pakku](https://aur.archlinux.org/packages/pakku/) | Nim | Yes | [Yes](https://github.com/kitsunyan/pakku/commit/396e9f4) | Yes | Yes | Yes | Yes | [Yes](https://github.com/kitsunyan/pakku/commit/864cc03) | [`-Sy`](https://github.com/kitsunyan/pakku/wiki/Native-Pacman-Explanation) | 1 | bash, zsh | [ABS](/index.php/ABS "ABS") support, AUR comments, fetch PGP keys |
| [pikaur](https://aur.archlinux.org/packages/pikaur/) | Python | Yes | Yes | Yes | Yes | Yes | [Yes](https://github.com/actionless/pikaur/commit/d409b95) | Yes | [`-Sy`](https://github.com/actionless/pikaur#pikaur) | 1, 2, 3 | bash, fish, zsh | [dynamic users](http://0pointer.net/blog/dynamic-users-with-systemd.html), [multilingual](https://github.com/actionless/pikaur/tree/master/locale), sort by votes/popularity, print news, [ignore errors](https://github.com/actionless/pikaur/commit/3688d82) |
| [trizen](https://aur.archlinux.org/packages/trizen/) | Perl | Yes | Yes | [Yes](https://github.com/trizen/trizen/commit/6fb0cc9) | [Yes](https://github.com/trizen/trizen/commit/7ab7ee5f) | Yes | [Partial](https://github.com/trizen/trizen/issues/46) | Yes | [`-Ud`*](https://github.com/trizen/trizen/commit/9e7b40e) | 1* | bash, fish, zsh | automatic builds by default, use `-G` to disable; AUR comments |
| [aura](https://aur.archlinux.org/packages/aura/) | Haskell | Optional | [Partial](https://github.com/aurapm/aura/blob/89bf702/aura/src/Aura/Pkgbuild/Records.hs) | [No](https://github.com/aurapm/aura/pull/346) | [Yes](https://github.com/aurapm/aura/commit/7848e983) | No | [No](https://github.com/aurapm/aura/issues/353) | Yes | – | 1* | bash, zsh | automatic builds by default, use `--dryrun` to disable; [downgrade](/index.php/Downgrade "Downgrade") support, multilingual |
| [aurman](https://aur.archlinux.org/packages/aurman/)
<small>([no user support](https://github.com/polygamma/aurman#stopped-development-for-public-use))</small> | Python | Yes | Yes | Yes | Yes | [Yes](https://github.com/polygamma/aurman/wiki/Description-of-the-aurman-dependency-solving) | Yes | Yes | [`-Sy`*](https://github.com/polygamma/aurman/commit/6c02ba3)
[`--ask`*](https://github.com/polygamma/aurman#make-use-of-the-undocumented---ask-flag-of-pacman) | 1, [2*, 3*](https://github.com/polygamma/aurman#question-6) | bash, fish | fetch PGP keys, sort by votes/popularity, print news |
| [pacaur](https://aur.archlinux.org/packages/pacaur/)
<small>([discontinued](https://bbs.archlinux.org/viewtopic.php?pid=1755144#p1755144))</small> | Bash/C | Yes | Yes | Yes | Yes | Yes | Yes | Yes | [`-Ud`](https://github.com/rmarquis/pacaur/commit/d8f4918)
[`--ask`](https://github.com/rmarquis/pacaur/commit/12707cc) | 1, 3 | bash, zsh | multilingual, sort by votes/popularity |
| [wrapaur](https://aur.archlinux.org/packages/wrapaur/)
<small>(stalled)</small> | Bash | Yes | No | Yes | No | No | No | Yes | – | – | – | mirror updates, print news and AUR comments |
| [packer-aur](https://aur.archlinux.org/packages/packer-aur/)
<small>(stalled)</small> | Bash | No | No | No | No | No | No | Yes | – | – | – | – |
| [yaourt](https://aur.archlinux.org/packages/yaourt/)
<small>(low activity)</small> | Bash/C | [No](https://github.com/archlinuxfr/yaourt/blob/34b5c0b/src/lib/aur.sh#L54-L72) | Optional | Optional | No | [No](https://github.com/archlinuxfr/yaourt/issues/186) | [No](https://github.com/archlinuxfr/yaourt/issues/85) | [No](https://lists.archlinux.org/pipermail/aur-general/2015-August/031314.html) | [`-Sy`](https://github.com/archlinuxfr/yaourt/blob/d30823e/yaourt/yaourt#L1773) | 2 | bash, fish, zsh | ABS support, print AUR comments, multilingual |

## Graphical

**Warning:**

*   Graphical AUR helpers are typically aimed at [Arch-based distributions](/index.php/Arch-based_distributions "Arch-based distributions"). Their use in [Arch Linux](/index.php/Arch_Linux "Arch Linux") may lead to a defective system, for example through unattended [partial upgrades](/index.php/Partial_upgrades "Partial upgrades").
*   If a helper has *known* problematic behavior, it is colored with a red entry.

| Name | Written in | GUI toolkit | Backend helper | Notes |
| [aarchup](https://aur.archlinux.org/packages/aarchup/) | C | GTK+ 2 | auracle | – |
| [argon](https://aur.archlinux.org/packages/argon/) | Python | GTK+ 3 | auracle, pacaur | – |
| [cylon](https://aur.archlinux.org/packages/cylon/) | Bash | TUI | auracle, trizen | – |
| [kalu](https://aur.archlinux.org/packages/kalu/) | C | GTK+ 3 | – | – |
| [pactray](https://aur.archlinux.org/packages/pactray/) | Python | GTK+3 | auracle | – |
| [pamac-aur](https://aur.archlinux.org/packages/pamac-aur/) | Vala | GTK+ 3 | – | Uses [libalpm(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libalpm.3) instead of [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) |
| [pakku-gui](https://aur.archlinux.org/packages/pakku-gui/) | Python | GTK+ 3 | pakku | – |
| [pkgbrowser](https://aur.archlinux.org/packages/pkgbrowser/) | Python | Qt 5 | – | – |
| [updatehint](https://aur.archlinux.org/packages/updatehint/) | Bash | GTK+ 3 | auracle | – |
| [octopi](https://aur.archlinux.org/packages/octopi/) | C++ | Qt 5 | trizen, pacaur, yaourt | [enabled on install](https://github.com/aarnt/octopi/blob/271c7e1/octopi.install) notifier service regularly [performs partial upgrades](https://github.com/aarnt/octopi/issues/134#issuecomment-142099266) |

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
*   **aurpublish** — Helper script to manage and upload AUR packages using [git-subtree(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-subtree.1). Uses [githooks(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/githooks.5) to verify the PKGBUILD integrity, generate .SRCINFO automatically, and create a commit message template.

	[https://github.com/eli-schwartz/aurpublish](https://github.com/eli-schwartz/aurpublish) || [aurpublish](https://www.archlinux.org/packages/?name=aurpublish)