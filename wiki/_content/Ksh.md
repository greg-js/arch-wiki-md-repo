# Ksh

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Korn Shell (ksh) is a standard/restricted command and programming language developed by AT&T.

## Contents

*   [1 Installation](#Installation)
*   [2 Making m/ksh your default login shell](#Making_m.2Fksh_your_default_login_shell)
*   [3 Uninstallation](#Uninstallation)
*   [4 See Also](#See_Also)

## Installation

First, [install](/index.php/Install "Install") an implementation from the [official repositories](/index.php/Official_repositories "Official repositories"):

*   **MirBSD™ Korn Shell** — Enhanced version of the public domain ksh.

[https://www.mirbsd.org/mksh.htm](https://www.mirbsd.org/mksh.htm) || [mksh](https://www.archlinux.org/packages/?name=mksh)

More implementations are provided in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"):

*   **loksh** — A Linux port of OpenBSD's ksh

[https://github.com/dimkr/loksh](https://github.com/dimkr/loksh) || [loksh](https://aur.archlinux.org/packages/loksh/)<sup><small>AUR</small></sup>

*   **Public Domain Korn Shell** — Clone of the AT&T Korn shell. At the moment, it has most of the ksh88 features, not much of the ksh93 features, and a number of its own features.

[http://www.cs.mun.ca/~michael/pdksh/](http://www.cs.mun.ca/~michael/pdksh/) || [pdksh](https://aur.archlinux.org/packages/pdksh/)<sup><small>AUR</small></sup>

*   **[AT&T Korn shell](https://en.wikipedia.org/wiki/Korn_shell "wikipedia:Korn shell")** — Official AT&T version.

[http://www.kornshell.com/](http://www.kornshell.com/) || [ksh](https://aur.archlinux.org/packages/ksh/)<sup><small>AUR</small></sup>

*   **OpenBSDs Korn Shell** — Porting of the OpenBSD version of ksh to GNU/Linux.

[http://www.connochaetos.org/oksh/](http://www.connochaetos.org/oksh/) || [oksh](https://aur.archlinux.org/packages/oksh/)<sup><small>AUR</small></sup>

*   **obase** — OpenBSD userland ported to Linux, statically linked.

[https://github.com/chneukirchen/obase](https://github.com/chneukirchen/obase) || [obase-git](https://aur.archlinux.org/packages/obase-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/obase-git)]</sup>

*   **obase musl** — OpenBSD userland ported to Linux, statically linked to musl libc.

[https://github.com/chneukirchen/obase](https://github.com/chneukirchen/obase) || [obase-musl-git](https://aur.archlinux.org/packages/obase-musl-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/obase-musl-git)]</sup>

## Making m/ksh your default login shell

Change the default shell for the current user:

```
$ chsh -s /usr/bin/mksh

```

## Uninstallation

Change the default shell before removing the [mksh](https://www.archlinux.org/packages/?name=mksh) package.

**Warning:** Failure to follow the below procedure may result in users no longer having access to a working shell.

Run following command:

```
$ chsh -s /bin/bash _user_

```

Use it for every user with m/ksh set as their login shell (including root if needed). When completed, the [mksh](https://www.archlinux.org/packages/?name=mksh) package can be removed.

Alternatively, change the default shell back to Bash by editing `/etc/passwd` as root.

**Warning:** It is strongly recommended to use `vipw` when editing `/etc/passwd` as it helps prevent invalid entries and/or syntax errors.

For example, change the following:

```
_username_:x:1000:1000:_Full Name_,,,:/home/_username_:/bin/mksh

```

To this:

```
_username_:x:1000:1000:_Full Name_,,,:/home/_username_:/bin/bash

```

## See Also

*   [mksh - The MirBSD Korn Shell](https://www.mirbsd.org/mksh.htm)
*   [pdksh - the Public Domain Korn Shell](http://www.cs.mun.ca/~michael/pdksh/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Ksh&oldid=412117](https://wiki.archlinux.org/index.php?title=Ksh&oldid=412117)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Command shells](/index.php/Category:Command_shells "Category:Command shells")

Hidden category:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")