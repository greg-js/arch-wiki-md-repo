**Atenção:** Nenhuma dessas ferramentas possuem suporte [oficial](https://bbs.archlinux.org/viewtopic.php?pid=828254#p828254) pelo Arch Linux. É recomendado se tornar familiar com o [processo manual de compilação](/index.php/Arch_User_Repository_(Portugu%C3%AAs)#Instalando_pacotes "Arch User Repository (Português)") para estar preparado para diagnosticar e resolver problemas por conta própria.

Auxiliares do AUR são escritos para automatizar certas tarefas para o [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)").

## Contents

*   [1 Envio](#Envio)
*   [2 Compilar e pesquisa](#Compilar_e_pesquisa)
*   [3 Manutenção](#Manuten.C3.A7.C3.A3o)
*   [4 Bibliotecas](#Bibliotecas)
*   [5 Gráfico](#Gr.C3.A1fico)
*   [6 Tabela comparativa](#Tabela_comparativa)

## Envio

*   [bbidulock's script](https://gist.github.com/bbidulock/82ab6f5347f021136054) — Migra de um diretório .backup com todos os pacotes.
*   [aur4_import.sh](https://github.com/JonnyJD/PKGBUILDs/blob/master/_bin/aur4_import.sh) — Divide um pacote de um repositório git com múltiplos pacotes, adicionando/atualizando `.SRCINFO` para cada commit.
*   [aur4_make_submodule.sh](https://github.com/JonnyJD/PKGBUILDs/blob/master/_bin/aur4_make_submodule.sh) / [subaur4](https://github.com/alexandre-mbm/arch-pkgs/blob/master/subaur4) — Substitui um pacote em um repositório git maior com um submódulo do AUR 4, incluindo `.SRCINFO`.
*   [import-to-aur4](https://github.com/ido/packages-archlinux/blob/master/bin/import-to-aur4.sh) — Divide um repositório git existente em múltiplos do AUR 4, todos de uma vez, incluindo `.SRCINFO` para cada commit.
*   [aurpublish](https://github.com/Edenhofer/abs/blob/master/aurpublish) — Gerencia pacotes do AUR como [subárvores git](https://raw.githubusercontent.com/git/git/master/contrib/subtree/git-subtree.txt). A [geração de arquivos `.SRCINFO`, verificação de `PKGBUILD`](https://github.com/Edenhofer/abs/blob/master/pre-commit.hook) e a [criação de um modelo de mensagem de commit por pacote](https://github.com/Edenhofer/abs/blob/master/prepare-commit-msg.hook) é deixada para os *hooks* git no mesmo [repositório](https://github.com/Edenhofer/abs/blob/master/README.md).

## Compilar e pesquisa

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

*   **cylon** — pacman and pacaur wrapper, and is also a wrapper for cower and provides it a backend. Includes various other maintenance functions and extras.

	[https://github.com/gavinlyonsrepo/cylon](https://github.com/gavinlyonsrepo/cylon) || [cylon](https://aur.archlinux.org/packages/cylon/)

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

## Manutenção

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

## Bibliotecas

*   **haskell-archlinux** — Library to access the AUR and package metadata from the Haskell programming language

	[http://hackage.haskell.org/package/archlinux](http://hackage.haskell.org/package/archlinux) || [haskell-archlinux](https://aur.archlinux.org/packages/haskell-archlinux/)

*   **python3-aur** — Python 3 modules for accessing AUR package information and automating AUR interactions.

	[http://xyne.archlinux.ca/projects/python3-aur](http://xyne.archlinux.ca/projects/python3-aur) || [python3-aur](https://aur.archlinux.org/packages/python3-aur/)

## Gráfico

*   **Aarchup** — Fork of archup. Has the same options as archup plus a few other features. For differences between both please check [changelog](https://bbs.archlinux.org/viewtopic.php?id=119129).

	[https://github.com/aericson/aarchup/](https://github.com/aericson/aarchup/) || [aarchup](https://aur.archlinux.org/packages/aarchup/)

*   **Argon** — Graphical frontend to pacaur, featuring package installation, removal, and updating; and update notifications for both official repository and AUR packages.

	[https://github.com/14mRh4X0r/arch-argon](https://github.com/14mRh4X0r/arch-argon) || [argon](https://aur.archlinux.org/packages/argon/)

*   **PkgBrowser** — Application for searching and browsing Arch packages, showing details on selected packages.

	[https://bitbucket.org/kachelaqa/pkgbrowser/wiki/Home](https://bitbucket.org/kachelaqa/pkgbrowser/wiki/Home) || [pkgbrowser](https://aur.archlinux.org/packages/pkgbrowser/)

## Tabela comparativa

The columns have the following meaning:

*   *Secure*: does not [source](/index.php/Source "Source") the PKGBUILD at all by default; or, alerts the user and offers the opportunity to inspect the PKGBUILD manually before it is sourced. Some helpers are known to source PKGBUILDs before the user can inspect them, **allowing malicious code to be executed**. *Optional* means that there is a command line flag or configuration option to prevent the automatic sourcing before viewing.
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
| aurutils | Bash/C | Yes | Yes | Yes | Yes | Yes | Yes | zsh | S | [vifm](/index.php/Vifm "Vifm"), [PCRE](https://en.wikipedia.org/wiki/PCRE "w:PCRE"), [local repository](/index.php/Local_repository "Local repository"), [package signing](/index.php/Package_signing "Package signing"), [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") support |
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
| trizen | Perl | Yes | Yes | Yes [[10]](https://github.com/trizen/trizen/commit/7ab7ee5f9f1f5d971b731d092fc8e1dd963add4b) | Yes | Yes [[11]](https://github.com/trizen/trizen/commit/3c94434c66ede793758f2bf7de84d68e3174e2ac) | Yes [[12]](https://github.com/trizen/trizen/commit/6fb0cc9e0ab66b8cca9493b0618ba4bab5fd2252) | None | P | AUR comments |
| wrapaur | Bash | Yes | Yes | No | No | No | Yes | None | S | Mirror updates, print news and AUR comments |
| yaah | Bash | Yes | N/A | Yes | N/A | N/A | Optional | bash | S | No automatic builds |
| yaourt | Bash/C | No (*yaourt -Si*) [[13]](https://github.com/archlinuxfr/yaourt/blob/f373121d23d87031a24135fee593115832d803ec/src/lib/aur.sh#L47) [[14]](https://github.com/archlinuxfr/yaourt/blob/d9790e29cd7194535c793f51d185b7130a396916/src/lib/pkgbuild.sh.in#L415-L438) | No [[15]](https://lists.archlinux.org/pipermail/aur-general/2015-August/031314.html) | No | No [[16]](https://github.com/archlinuxfr/yaourt/issues/186) | No [[17]](https://github.com/archlinuxfr/yaourt/issues/85) | Optional | bash/zsh/fish | P | Backup, ABS support, AUR comments, multilingual |
| yay | Go | Yes | Yes | Yes | No | Partial | No | bash/zsh/fish | P | sort by votes |

**Note:** [Pacman](/index.php/Pacman "Pacman") 4.2\. introduced architecture specific fields. [[18]](http://allanmcrae.com/2014/12/pacman-4-2-released/) However, as of 06 April 2016, [AurJson](/index.php/AurJson "AurJson") combines all entries in a single field: [FS#48796](https://bugs.archlinux.org/task/48796). Helpers relying on the RPC may use the below workarounds to retrieve dependencies:

*   [bauerbill](https://aur.archlinux.org/packages/bauerbill/) [[19]](https://bbs.archlinux.org/viewtopic.php?pid=1617235#p1617235), [pkgbuilder](https://aur.archlinux.org/packages/pkgbuilder/) [[20]](https://github.com/Kwpolska/pkgbuilder/blob/65d9d74ef05f8996b81afb1cd005e3c337afa8b2/pkgbuilder/build.py#L198): Retrieve specific fields from [.SRCINFO](/index.php/.SRCINFO ".SRCINFO")
*   [aurutils](https://aur.archlinux.org/packages/aurutils/) [[21]](https://github.com/AladW/aurutils/issues/80), [pacaur](https://aur.archlinux.org/packages/pacaur/) [[22]](https://github.com/rmarquis/pacaur/issues/465), [trizen](https://aur.archlinux.org/packages/trizen/) [[23]](https://github.com/trizen/trizen/commit/6a8ff9dc8cc83af783b8475dfbe89988dbc8a553): Strip the `lib32-` prefix on `i686` systems