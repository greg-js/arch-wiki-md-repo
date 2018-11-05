**Warning:** AUR helpers are **not supported** by Arch Linux. You should become familiar with the [manual build process](/index.php/Arch_User_Repository#Installing_packages "Arch User Repository") in order to be prepared to troubleshoot problems.

**Note:** Please use the discussion page to suggest edits to this article: [Talk:AUR helpers](/index.php/Talk:AUR_helpers "Talk:AUR helpers").

AUR helpers automate certain usage of the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). Most AUR helpers can search for packages in the AUR and retrieve their [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") – others additionally assist with the build and install process.

[Pacman](/index.php/Pacman "Pacman") only handles updates for pre-built packages in its repositories. AUR packages are redistributed in form of [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") and need an AUR helper to automate the re-build process. However, keep in mind that a rebuild of package may be required when its shared library dependencies are updated, not only when the package itself is updated.

Since AUR helpers are unsupported, they are not present in the [official repositories](/index.php/Official_repositories "Official repositories").

## Contents

*   [1 Legend](#Legend)
*   [2 Search and download](#Search_and_download)
*   [3 Download and build](#Download_and_build)
*   [4 Pacman wrappers](#Pacman_wrappers)
*   [5 Graphical](#Graphical)
*   [6 Libraries](#Libraries)
*   [7 Maintenance](#Maintenance)
*   [8 Uploading](#Uploading)

## Legend

The columns have the following meaning:

	File review

	Does not [source](/index.php/Source "Source") the PKGBUILD at all by default; or, alerts the user and offers the opportunity to inspect the PKGBUILD manually before it is sourced. Some helpers are known to source PKGBUILDs before the user can inspect them, **allowing malicious code to be executed**. *Optional* means that there is a command line flag or configuration option to prevent the automatic sourcing before viewing.

	Diff view

	Ability to view package differences on inspection. Besides the PKGBUILD, this includes changes to files such as `.install` or `.patch` files.

	Git clone

	Uses [git-clone(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-clone.1) by default to retrieve build files from the AUR.

	Reliable parser

	Ability to handle complex packages by using the provided metadata ([RPC](/index.php/Aurweb_RPC_interface "Aurweb RPC interface")/.SRCINFO) instead of PKGBUILD [parsing](https://en.wikipedia.org/wiki/Parsing#Parser "w:Parsing"), such as [aws-cli-git](https://aur.archlinux.org/packages/aws-cli-git/).

	Reliable solver

	Ability to correctly solve and build complex dependency chains, such as [ros-lunar-desktop](https://aur.archlinux.org/packages/ros-lunar-desktop/).

	Split packages

	Ability to correctly build and install:

*   Multiple packages from the same package base, without rebuilding or reinstalling multiple times, such as [clion](https://aur.archlinux.org/packages/clion/)
*   Split packages which depend on a package from the same package base, such as [libc++](https://aur.archlinux.org/packages/libc%2B%2B/) and [libc++abi](https://aur.archlinux.org/packages/libc%2B%2Babi/).
*   Split packages independently, such as [python-pyalsaaudio](https://aur.archlinux.org/packages/python-pyalsaaudio/) and [python2-pyalsaaudio](https://aur.archlinux.org/packages/python2-pyalsaaudio/).

	Clean build

	Does not export new variables that can prevent a successful build process.

	Batch interaction

	Ability to prompt before the build process, in particular:

1.  Inspection of package files or their differences;
2.  Summary of package upgrades;
3.  Resolution of package conflicts and installations.

	An asterisk denotes functionality specifically enabled by the user.

	Shell completion

	[Tab completion](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion") is available for the listed [shells](/index.php/Shell "Shell").

**Note:**

*   Table rows are sorted by column values, where *Yes* or *N/A* take precedence over *Partial* or *Optional* and *No*, or alphabetically if values are equal.
*   *Optional* means that a feature is available, but only through a command-line argument or configuration option. *Partial* means that a feature is not fully implemented, or that it partially deviates from the given criteria.

## Search and download

| Name | Written in | File review | Git clone | Reliable parser | Reliable solver | Shell completion | Specificity |
| [auracle-git](https://aur.archlinux.org/packages/auracle-git/) | C++ | Yes | [Yes](https://github.com/falconindy/auracle/commit/c73bbee) | Yes | Yes | bash | print build order |
| [pbget](https://aur.archlinux.org/packages/pbget/) | Python | Yes | Yes | Yes | – | – | – |
| [yaah](https://aur.archlinux.org/packages/yaah/) | Bash | Yes | Optional | Yes | – | bash | – |
| [package-query](https://aur.archlinux.org/packages/package-query/) | C | Yes | – | [No](https://github.com/archlinuxfr/package-query/issues/135) | – | – | search only |
| [repoctl](https://aur.archlinux.org/packages/repoctl/) | Go | Yes | No | [Yes](https://github.com/goulash/pacman/blob/master/aur/aur.go) | – | zsh | local repository support |
| [aurel](https://aur.archlinux.org/packages/aurel/)
<small>([discontinued](https://bbs.archlinux.org/viewtopic.php?pid=1522459#p1522459))</small> | Emacs Lisp | Yes | No | Yes | – | – | Emacs integration |
| [cower](https://aur.archlinux.org/packages/cower/)
<small>([discontinued](https://github.com/falconindy/cower#description))</small> | C | Yes | No | Yes | – | bash, zsh | regex support, sort by votes/popularity |

## Download and build

| Name | Written in | File review | Diff view | Git clone | Reliable parser | Reliable solver | Split packages | Clean build | Batch interaction | Shell completion | Specificity |
| [aurutils](https://aur.archlinux.org/packages/aurutils/) | Bash/C | Yes | Yes | Yes | Yes | Yes | Yes | Yes | 1 | zsh | [vifm](/index.php/Vifm "Vifm"), [local repository](/index.php/Local_repository "Local repository"), [package signing](/index.php/Package_signing "Package signing"), [clean chroot](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot") support, sort by votes/popularity |
| [bauerbill](https://aur.archlinux.org/packages/bauerbill/) | Python | Yes | No | Yes | Yes | Yes | Yes | Yes | 1 | bash, zsh | trust management, [ABS](/index.php/ABS "ABS") support, extends *powerpill*, `bb-wrapper` for *pacman* wrapping |
| [rua](https://aur.archlinux.org/packages/rua/) | Rust | Yes | [No](https://github.com/vn971/rua/issues/1) | Yes | [Yes](https://github.com/vn971/rua/commit/fc8c2f3) | Yes | Yes | Yes | 1 | bash, zsh, fish | tar artifact inspections (SUID, install file etc), isolated build, offline build |
| [PKGBUILDer](https://aur.archlinux.org/packages/PKGBUILDer/) | Python | Optional | [No](https://github.com/Kwpolska/pkgbuilder/issues/36) | Yes | Yes | Yes | [Partial](https://github.com/Kwpolska/pkgbuilder/issues/39) | Yes | 1* | – | automatic builds by default, use `-F` to disable; multilingual, `pb-wrapper` for *pacman* wrapping |
| [repofish](https://aur.archlinux.org/packages/repofish/) | Bash | Optional | Yes | Yes | No | No | No | Yes | 1* | – | automatic builds by default, use `check` or `update` to disable; [local repository](/index.php/Local_repository "Local repository") support |
| [naaman](https://aur.archlinux.org/packages/naaman/)
<small>([discontinued](https://github.com/enckse/naaman/issues/20#issuecomment-433781874))</small> | Python | Optional | No | Yes | Yes | [Partial](https://github.com/enckse/naaman/issues/19) | [Partial](https://github.com/enckse/naaman/issues/20) | Yes | 1* | bash | automatic builds by default, use `--fetch` to disable; use `-d` to enable the solver |
| [spinach](https://aur.archlinux.org/packages/spinach/)
<small>([discontinued](https://github.com/floft/spinach))</small> | Bash | [Yes](https://github.com/floft/spinach/commit/5455747) | No | No | No | No | No | Yes | – | – | – |
| [aurget](https://aur.archlinux.org/packages/aurget/)
<small>(stalled)</small> | Bash | Optional | [No](https://github.com/pbrisbin/aurget/issues/41) | No | No | No | [No](https://github.com/pbrisbin/aurget/issues/40) | Yes | – | bash, zsh | sort by votes |
| [burgaur](https://aur.archlinux.org/packages/burgaur/)
<small>([discontinued](https://github.com/m45t3r/burgaur/issues/7#issuecomment-365599675))</small> | Python/C | Optional | No | No | No | No | No | Yes | – | – | wrapper for *cower* |

## Pacman wrappers

**Warning:** [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) wrappers abstract the work of the package manager. They may (optionally or by default) introduce [unsafe flags](/index.php/System_maintenance#Avoid_certain_pacman_commands "System maintenance"), or other unexpected behavior leading to a defective system.

| Name | Written in | File review | Diff view | Git clone | Reliable parser | Reliable solver | Split packages | Clean build | Unsafe flags | Batch interaction | Shell completion | Specificity |
| [pakku](https://aur.archlinux.org/packages/pakku/) | Nim | Yes | [Yes](https://github.com/kitsunyan/pakku/commit/396e9f4) | Yes | Yes | Yes | Yes | [Yes](https://github.com/kitsunyan/pakku/commit/864cc03) | [-Sy](https://github.com/kitsunyan/pakku/wiki/Native-Pacman-Explanation) | 1 | bash, zsh | [ABS](/index.php/ABS "ABS") support, AUR comments, fetch PGP keys |
| [pikaur](https://aur.archlinux.org/packages/pikaur/) | Python | Yes | Yes | Yes | Yes | Yes | [Yes](https://github.com/actionless/pikaur/commit/d409b95) | Yes | [-Sy](https://github.com/actionless/pikaur#pikaur) | 1, 2, 3 | bash, fish, zsh | [dynamic users](http://0pointer.net/blog/dynamic-users-with-systemd.html), [multilingual](https://github.com/actionless/pikaur/tree/master/locale), sort by votes/popularity, print news, [ignore errors](https://github.com/actionless/pikaur/commit/3688d82) |
| [yay](https://aur.archlinux.org/packages/yay/) | Go | Yes | [Yes](https://github.com/Jguer/yay/pull/447) | [Yes](https://github.com/Jguer/yay/pull/297) | Yes | Yes | Yes | Yes | [-Sy*](https://github.com/Jguer/yay/commit/3bdb534)
[--ask*](https://github.com/Jguer/yay/commit/ea5a94e) | 1, [2*](https://github.com/Jguer/yay/commit/3bdb534), [3*](https://github.com/Jguer/yay/commit/ea5a94e) | bash, fish, zsh | fetch PGP keys, sort by votes/popularity, [prompt architecture](https://github.com/Jguer/yay/commit/4bcd3a6) |
| [trizen](https://aur.archlinux.org/packages/trizen/) | Perl | Yes | Yes | [Yes](https://github.com/trizen/trizen/commit/6fb0cc9) | [Yes](https://github.com/trizen/trizen/commit/7ab7ee5f) | Yes | [Partial](https://github.com/trizen/trizen/issues/46) | Yes | [-Ud*](https://github.com/trizen/trizen/commit/9e7b40e) | 1* | bash, fish, zsh | automatic builds by default, use `-G` to disable; AUR comments |
| [aura](https://aur.archlinux.org/packages/aura/) | Haskell | Optional | [Partial](https://github.com/aurapm/aura/blob/89bf702/aura/src/Aura/Pkgbuild/Records.hs) | [No](https://github.com/aurapm/aura/pull/346) | [Yes](https://github.com/aurapm/aura/commit/7848e983) | No | [No](https://github.com/aurapm/aura/issues/353) | Yes | – | 1* | bash, zsh | automatic builds by default, use `--dryrun` to disable; [downgrade](/index.php/Downgrade "Downgrade") support, multilingual |
| [aurman](https://aur.archlinux.org/packages/aurman/)
<small>([no user support](https://github.com/polygamma/aurman#stopped-development-for-public-use))</small> | Python | Yes | Yes | Yes | Yes | [Yes](https://github.com/polygamma/aurman/wiki/Description-of-the-aurman-dependency-solving) | Yes | Yes | [-Sy*](https://github.com/polygamma/aurman/commit/6c02ba3)
[--ask*](https://github.com/polygamma/aurman#make-use-of-the-undocumented---ask-flag-of-pacman) | 1, [2*, 3*](https://github.com/polygamma/aurman#question-6) | bash, fish | fetch PGP keys, sort by votes/popularity, print news |
| [pacaur](https://aur.archlinux.org/packages/pacaur/)
<small>([discontinued](https://bbs.archlinux.org/viewtopic.php?pid=1755144#p1755144))</small> | Bash/C | Yes | Yes | Yes | Yes | Yes | Yes | Yes | [-Ud](https://github.com/rmarquis/pacaur/commit/d8f4918)
[--ask](https://github.com/rmarquis/pacaur/commit/12707cc) | 1, 3 | bash, zsh | multilingual, sort by votes/popularity |
| [wrapaur](https://aur.archlinux.org/packages/wrapaur/)
<small>(stalled)</small> | Bash | Yes | No | Yes | No | No | No | Yes | – | – | – | mirror updates, print news and AUR comments |
| [packer-aur](https://aur.archlinux.org/packages/packer-aur/)
<small>(stalled)</small> | Bash | No | No | No | No | No | No | Yes | – | – | – | – |
| [yaourt](https://aur.archlinux.org/packages/yaourt/)
<small>(stalled)</small> | Bash/C | [No](https://github.com/archlinuxfr/yaourt/blob/34b5c0b/src/lib/aur.sh#L54-L72) | Optional | Optional | No | [No](https://github.com/archlinuxfr/yaourt/issues/186) | [No](https://github.com/archlinuxfr/yaourt/issues/85) | [No](https://lists.archlinux.org/pipermail/aur-general/2015-August/031314.html) | [-Sy](https://github.com/archlinuxfr/yaourt/blob/d30823e/yaourt/yaourt#L1773) | 2 | bash, fish, zsh | ABS support, print AUR comments, multilingual |

## Graphical

**Warning:** Usage of graphical AUR helpers may lead to a defective system, for example through unattended [partial upgrades](/index.php/Partial_upgrades "Partial upgrades").

*   **Argon** — GTK+ 3 pacman wrapper written in Python.

	[https://github.com/14mRh4X0r/arch-argon](https://github.com/14mRh4X0r/arch-argon) || [argon](https://aur.archlinux.org/packages/argon/)

*   **Cylon** — TUI pacman wrapper written in Bash.

	[https://github.com/gavinlyonsrepo/cylon](https://github.com/gavinlyonsrepo/cylon) || [cylon](https://aur.archlinux.org/packages/cylon/)

*   **Pamac** — Standalone GTK+ 3 package manager using [libalpm(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libalpm.3) written in Vala.

	[https://gitlab.manjaro.org/applications/pamac](https://gitlab.manjaro.org/applications/pamac) || [pamac-aur](https://aur.archlinux.org/packages/pamac-aur/)

*   **Pakku GUI** — GTK+ 3 frontend for pakku written in Python.

	[https://gitlab.com/mrvik/pakku-gui](https://gitlab.com/mrvik/pakku-gui) || [pakku-gui](https://aur.archlinux.org/packages/pakku-gui/)

*   **PkgBrowser** — Qt 5 read-only browser for repository packages and AUR written in Python.

	[https://bitbucket.org/kachelaqa/pkgbrowser](https://bitbucket.org/kachelaqa/pkgbrowser) || [pkgbrowser](https://aur.archlinux.org/packages/pkgbrowser/)

*   **Octopi** — Qt 5 pacman wrapper written in C++. May lead to defective system as [enabled on install](https://github.com/aarnt/octopi/blob/271c7e1/octopi.install) notifier service [regularly performs](https://github.com/aarnt/octopi/issues/134#issuecomment-142099266) [partial upgrades](/index.php/Partial_upgrades "Partial upgrades").

	[https://octopiproject.wordpress.com/](https://octopiproject.wordpress.com/) || [octopi](https://aur.archlinux.org/packages/octopi/)

## Libraries

*   [aur.rs](https://github.com/zeyla/aur.rs) — Rust library for accessing [Aurweb RPC interface](/index.php/Aurweb_RPC_interface "Aurweb RPC interface").

*   **haskell-archlinux** — Library to access the AUR and package metadata from the Haskell programming language.

	[https://hackage.haskell.org/package/archlinux](https://hackage.haskell.org/package/archlinux) || [haskell-archlinux](https://aur.archlinux.org/packages/haskell-archlinux/)

*   **python3-aur** — Python 3 modules for accessing AUR package information and automating AUR interactions.

	[https://xyne.archlinux.ca/projects/python3-aur](https://xyne.archlinux.ca/projects/python3-aur) || [python3-aur](https://aur.archlinux.org/packages/python3-aur/)

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