The [KornShell](https://en.wikipedia.org/wiki/KornShell "wikipedia:KornShell") (ksh) is a standard/restricted command and programming language developed by AT&T.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Making m/ksh your default login shell](#Making_m/ksh_your_default_login_shell)
*   [3 Uninstallation](#Uninstallation)
*   [4 See Also](#See_Also)

## Installation

First, [install](/index.php/Install "Install") an implementation from the [official repositories](/index.php/Official_repositories "Official repositories"):

*   **MirBSD™ Korn Shell** — Enhanced version of the public domain ksh.

	[https://www.mirbsd.org/mksh.htm](https://www.mirbsd.org/mksh.htm) || [mksh](https://www.archlinux.org/packages/?name=mksh)

More implementations are provided in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"):

*   **loksh** — A Linux port of OpenBSD's ksh

	[https://github.com/dimkr/loksh](https://github.com/dimkr/loksh) || [loksh-git](https://aur.archlinux.org/packages/loksh-git/)

*   **Public Domain Korn Shell** — Clone of the AT&T Korn shell. At the moment, it has most of the ksh88 features, not much of the ksh93 features, and a number of its own features.

	[http://www.cs.mun.ca/~michael/pdksh/](http://www.cs.mun.ca/~michael/pdksh/) || [pdksh](https://aur.archlinux.org/packages/pdksh/)

*   **[AT&T Korn shell](https://en.wikipedia.org/wiki/Korn_shell "wikipedia:Korn shell")** — Official AT&T version.

	[http://www.kornshell.com/](http://www.kornshell.com/) || [ksh](https://www.archlinux.org/packages/?name=ksh)

*   **OpenBSDs Korn Shell** — Porting of the OpenBSD version of ksh to GNU/Linux.

	[http://www.connochaetos.org/oksh/](http://www.connochaetos.org/oksh/) || [oksh](https://aur.archlinux.org/packages/oksh/)

## Making m/ksh your default login shell

Change the default shell for the current user:

```
$ chsh -s /bin/mksh

```

## Uninstallation

Change the default shell before removing the [mksh](https://www.archlinux.org/packages/?name=mksh) package.

**Warning:** Failure to follow the below procedure may result in users no longer having access to a working shell.

Run following command:

```
$ chsh -s /bin/bash *user*

```

Use it for every user with m/ksh set as their login shell (including root if needed). When completed, the [mksh](https://www.archlinux.org/packages/?name=mksh) package can be removed.

Alternatively, change the default shell back to Bash by editing `/etc/passwd` as root.

**Warning:** It is strongly recommended to use `vipw` when editing `/etc/passwd` as it helps prevent invalid entries and/or syntax errors.

For example, change the following:

```
*username*:x:1000:1000:*Full Name*,,,:/home/*username*:/bin/mksh

```

To this:

```
*username*:x:1000:1000:*Full Name*,,,:/home/*username*:/bin/bash

```

## See Also

*   [mksh - The MirBSD Korn Shell](https://www.mirbsd.org/mksh.htm)
*   [pdksh - the Public Domain Korn Shell](http://www.cs.mun.ca/~michael/pdksh/)