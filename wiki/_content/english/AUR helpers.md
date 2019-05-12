**Warning:** AUR helpers are **not supported** by Arch Linux. You should become familiar with the [manual build process](/index.php/Arch_User_Repository#Installing_packages "Arch User Repository") in order to be prepared to troubleshoot problems.

**Note:** Please use the discussion page to suggest edits to this article: [Talk:AUR helpers](/index.php/Talk:AUR_helpers "Talk:AUR helpers").

AUR helpers automate certain usage of the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). Most AUR helpers can search for packages in the AUR and retrieve their [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") – others additionally assist with the build and install process.

[Pacman](/index.php/Pacman "Pacman") only handles updates for pre-built packages in its repositories. AUR packages are redistributed in form of [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") and need an AUR helper to automate the re-build process. However, keep in mind that a rebuild of package may be required when its shared library dependencies are updated, not only when the package itself is updated.

Since AUR helpers are unsupported, they are not present in the [official repositories](/index.php/Official_repositories "Official repositories").

## Legend

The [#Comparison table](#Comparison_table) columns have the following meaning:

	File review

	Does not [source](/index.php/Source "Source") the PKGBUILD at all *by default*; or, alerts the user and offers the opportunity to inspect the PKGBUILD manually before it is sourced. Some helpers are known to source PKGBUILDs before the user can inspect them, **allowing malicious code to be executed**.

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

	Batch interaction

	Ability to prompt before the build process and package transactions, in particular:

1.  Combined summary of repository and AUR package upgrades;
2.  Resolution of package conflicts and choice of providers.

	Shell completion

	[Tab completion](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion") is available for the listed [shells](/index.php/Shell "Shell").

**Note:** *Optional* means that a feature is available, but only through a command-line argument or configuration option. *Partial* means that a feature is not fully implemented, or that it partially deviates from the given criteria.

## Comparison table

### Search and download

| Name | Written in | Git clone | Reliable parser | Reliable solver | Shell completion | Specificity |
| [auracle-git](https://aur.archlinux.org/packages/auracle-git/) | C++ | [Yes](https://github.com/falconindy/auracle/commit/c73bbee) | Yes | Yes | bash | print build order |
| [pbget](https://aur.archlinux.org/packages/pbget/) | Python | Yes | Yes | – | – | – |
| [repoctl](https://aur.archlinux.org/packages/repoctl/) | Go | No | [Yes](https://github.com/goulash/pacman/blob/master/aur/aur.go) | – | zsh | [local repository](/index.php/Local_repository "Local repository") |
| [yaah](https://aur.archlinux.org/packages/yaah/) | Bash | Optional | Yes | – | bash | – |
| [aurel](https://aur.archlinux.org/packages/aurel/)
<small>([discontinued](https://bbs.archlinux.org/viewtopic.php?pid=1522459#p1522459))</small> | Emacs Lisp | No | Yes | – | – | [emacs](/index.php/Emacs "Emacs") integration |

### Search and build

| Name | Written in | File review | Diff view | Git clone | Reliable parser | Reliable solver | Split packages | Shell completion | Specificity |
| [aurget](https://aur.archlinux.org/packages/aurget/) | Bash | No | [No](https://github.com/pbrisbin/aurget/issues/41) | No | No | No | [No](https://github.com/pbrisbin/aurget/issues/40) | bash, zsh | – |
| [aurutils](https://aur.archlinux.org/packages/aurutils/) | Bash/C | Yes | Yes | Yes | Yes | Yes | Yes | bash, zsh | [modular](https://en.wikipedia.org/wiki/Modular_programming "w:Modular programming"), [local repository](/index.php/Local_repository "Local repository"), [package signing](/index.php/Package_signing "Package signing"), [clean chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot") |
| [bauerbill](https://aur.archlinux.org/packages/bauerbill/) | Python | Yes | No | Yes | Yes | Yes | Yes | bash, zsh | `bb-wrapper` for *pacman* wrapping, trust management |
| [PKGBUILDer](https://aur.archlinux.org/packages/PKGBUILDer/) | Python | No | [No](https://github.com/Kwpolska/pkgbuilder/issues/36) | Yes | Yes | Yes | [Partial](https://github.com/Kwpolska/pkgbuilder/issues/39) | – | `pb` for *pacman* wrapping |
| [repofish](https://aur.archlinux.org/packages/repofish/) | Bash | No | Yes | Yes | No | No | No | – | [local repository](/index.php/Local_repository "Local repository") |
| [rua](https://aur.archlinux.org/packages/rua/) | Rust | Yes | [No](https://github.com/vn971/rua/issues/1) | Yes | [Yes](https://github.com/vn971/rua/commit/fc8c2f3) | Yes | [No](https://github.com/vn971/rua/issues/21) | bash, zsh, fish | [bubblewrap](/index.php/Bubblewrap "Bubblewrap"), `.pkg.tar` inspection, [build-only](https://github.com/vn971/rua/issues/13) |
| [spinach](https://aur.archlinux.org/packages/spinach/)
<small>([discontinued](https://github.com/floft/spinach))</small> | Bash | [Yes](https://github.com/floft/spinach/commit/5455747) | No | No | No | No | No | – | – |

### Pacman wrappers

**Warning:** [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) wrappers abstract the work of the package manager. They may (optionally or by default) introduce [unsafe flags](/index.php/System_maintenance#Avoid_certain_pacman_commands "System maintenance"), or other unexpected behavior leading to a defective system.

| Name | Written in | File review | Diff view | Git clone | Reliable parser | Reliable solver | Split packages | Unsafe flags | Shell completion | Specificity |
| [aura](https://aur.archlinux.org/packages/aura/) | Haskell | No | [Partial](https://github.com/aurapm/aura/blob/89bf702/aura/src/Aura/Pkgbuild/Records.hs) | [No](https://github.com/aurapm/aura/pull/346) | [Yes](https://github.com/aurapm/aura/commit/7848e983) | No | [No](https://github.com/aurapm/aura/issues/353) | – | bash, zsh | – |
| [pacaur](https://aur.archlinux.org/packages/pacaur/) | Bash/C | Yes | Yes | Yes | Yes | Yes | Yes | [--ask](https://github.com/rmarquis/pacaur/commit/12707cc) | bash, zsh | batch interaction 2 |
| [pakku](https://aur.archlinux.org/packages/pakku/) | Nim | Yes | [Yes](https://github.com/kitsunyan/pakku/commit/396e9f4) | Yes | Yes | Yes | Yes | [-Sy](https://github.com/kitsunyan/pakku/wiki/Native-Pacman-Explanation) | bash, zsh | fetch PGP keys |
| [pikaur](https://aur.archlinux.org/packages/pikaur/) | Python | Yes | Yes | Yes | Yes | Yes | Yes | [-Sy](https://github.com/actionless/pikaur#pikaur) | bash, fish, zsh | batch interaction 1/2, [dynamic users](http://0pointer.net/blog/dynamic-users-with-systemd.html) |
| [trizen](https://aur.archlinux.org/packages/trizen/) | Perl | Yes | Yes | [Yes](https://github.com/trizen/trizen/commit/6fb0cc9) | [Yes](https://github.com/trizen/trizen/commit/7ab7ee5f) | Yes | [Partial](https://github.com/trizen/trizen/issues/46) | [-Ud*](https://github.com/trizen/trizen/commit/9e7b40e) | bash, fish, zsh | – |
| [yay](https://aur.archlinux.org/packages/yay/) | Go | Yes | [Yes](https://github.com/Jguer/yay/pull/447) | [Yes](https://github.com/Jguer/yay/pull/297) | Yes | [Yes](https://github.com/Jguer/yay/pull/866) | Yes | [-Sy*](https://github.com/Jguer/yay/commit/3bdb534)
[--ask*](https://github.com/Jguer/yay/commit/ea5a94e) | bash, fish, zsh | batch interaction 1/2, fetch PGP keys |
| [aurman](https://aur.archlinux.org/packages/aurman/)
<small>([discontinued](https://github.com/polygamma/aurman#stopped-development-for-public-use))</small> | Python | Yes | Yes | Yes | Yes | [No](https://github.com/polygamma/aurman/issues/259) | Yes | [-Sy*](https://github.com/polygamma/aurman/commit/6c02ba3)
[--ask*](https://github.com/polygamma/aurman#make-use-of-the-undocumented---ask-flag-of-pacman) | bash, fish | batch interaction 1/2, fetch PGP keys |
| [packer-aur-git](https://aur.archlinux.org/packages/packer-aur-git/)
<small>(discontinued)</small> | Bash | No | No | No | No | No | No | – | – | – |

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

## Maintenance

*   **aur-out-of-date** — Uses hoster APIs to check AUR packages for upstream changes.

	[https://github.com/simon04/aur-out-of-date](https://github.com/simon04/aur-out-of-date) || [aur-out-of-date](https://aur.archlinux.org/packages/aur-out-of-date/)

*   **aurpublish** — Helper script to manage and upload AUR packages using [git-subtree(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-subtree.1). Uses [githooks(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/githooks.5) to verify the PKGBUILD integrity, generate .SRCINFO automatically, and create a commit message template.

	[https://github.com/eli-schwartz/aurpublish](https://github.com/eli-schwartz/aurpublish) || [aurpublish](https://www.archlinux.org/packages/?name=aurpublish)

*   **[devtools](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot")** — Build packages in a clean environment ([systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") container) to ensure their correctness. Wrapped by [aurutils](https://aur.archlinux.org/packages/aurutils/) and [clean-chroot-manager](https://aur.archlinux.org/packages/clean-chroot-manager/).

	[https://git.archlinux.org/devtools.git/](https://git.archlinux.org/devtools.git/) || [devtools](https://www.archlinux.org/packages/?name=devtools)

*   **pkgbuild-watch** — Looks for changes on the upstream web pages.

	[http://kmkeen.com/pkgbuild-watch](http://kmkeen.com/pkgbuild-watch) || [pkgbuild-watch](https://aur.archlinux.org/packages/pkgbuild-watch/)

*   **pkgbuildup** — Helps AUR package maintainers automatically update PKGBUILD files. Supports a template variable syntax.

	[https://github.com/fasheng/pkgbuildup](https://github.com/fasheng/pkgbuildup) || [pkgbuildup-git](https://aur.archlinux.org/packages/pkgbuildup-git/)

*   **pkgoutofdate** — Parses the source URL from PKGBUILDs and tries to find new versions of packages by incrementing the version number and sending requests to the web server.

	[https://github.com/anatol/pkgoutofdate](https://github.com/anatol/pkgoutofdate) || [pkgoutofdate-git](https://aur.archlinux.org/packages/pkgoutofdate-git/)

## Other

*   **aur.rs** — Rust library for accessing [Aurweb RPC interface](/index.php/Aurweb_RPC_interface "Aurweb RPC interface").

	[https://github.com/zeyla/aur.rs](https://github.com/zeyla/aur.rs) ||

*   **aur-talk** — Fetch and display AUR comments.

	[https://github.com/GermainZ/aur-talk](https://github.com/GermainZ/aur-talk) || [aur-talk-git](https://aur.archlinux.org/packages/aur-talk-git/)

*   **aurvote-utils** — A set of utilities for managing AUR votes.

	[https://github.com/jadenPete/aurvote-utils](https://github.com/jadenPete/aurvote-utils) || [aurvote-utils](https://aur.archlinux.org/packages/aurvote-utils/)

*   **haskell-aur** — Haskell library for accessing Aurweb RPC interface.

	[https://hackage.haskell.org/package/aur](https://hackage.haskell.org/package/aur) || [haskell-aur](https://aur.archlinux.org/packages/haskell-aur/)

*   **package-query** — Tool for querying [libalpm(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libalpm.3) and the AUR.

	[https://github.com/archlinuxfr/package-query](https://github.com/archlinuxfr/package-query) || [package-query](https://aur.archlinux.org/packages/package-query/)

*   **python3-aur** — Python 3 modules and helper utilities for accessing AUR package information and automating AUR interactions.

	[https://xyne.archlinux.ca/projects/python3-aur](https://xyne.archlinux.ca/projects/python3-aur) || [python3-aur](https://aur.archlinux.org/packages/python3-aur/)