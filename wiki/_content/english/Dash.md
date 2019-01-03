Related articles

*   [Command-line shell](/index.php/Command-line_shell "Command-line shell")
*   [Bash](/index.php/Bash "Bash")

[DASH (Debian Almquist shell)](https://en.wikipedia.org/wiki/Debian_Almquist_shell "wikipedia:Debian Almquist shell") is a modern POSIX-compliant implementation of [`/bin/sh` (sh, Bourne shell)](https://en.wikipedia.org/wiki/Bourne_shell "wikipedia:Bourne shell").

DASH is not [Bash](/index.php/Bash "Bash") compatible, but Bash tries to be mostly compatible with POSIX, and thus Dash.

DASH shines in:

*   Speed of execution. Roughly [4x times faster](https://unix.stackexchange.com/questions/148035/is-dash-or-some-other-shell-faster-than-bash) than Bash and others.
*   Very limited resources (disk space, RAM or CPU). As minimalistic as possible - much smaller (134.1 kB vs 6.5 MB installed, 13 kSLOC vs 176 kSLOC) than Bash and others.
*   Security. Dash is a long-established, tiny project with simple and long-established functionality; one that is still very much [alive](https://git.kernel.org/cgit/utils/dash/dash.git/log/), and with [many](https://git.kernel.org/cgit/utils/dash/dash.git/stats/?period=q&ofs=10) active developers. Thus, Dash has a much smaller attack surface, while still having many eyes on its code.
*   If classic `/bin/sh` needed only.

## Contents

*   [1 Installation](#Installation)
*   [2 Use DASH as /bin/sh](#Use_DASH_as_/bin/sh)
    *   [2.1 Identifying bashisms](#Identifying_bashisms)
        *   [2.1.1 Common places to check](#Common_places_to_check)
    *   [2.2 Relinking /bin/sh](#Relinking_/bin/sh)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [dash](https://www.archlinux.org/packages/?name=dash) from the [official repositories](/index.php/Official_repositories "Official repositories") or [dash-static-musl](https://aur.archlinux.org/packages/dash-static-musl/) from the [AUR](/index.php/AUR "AUR").

## Use DASH as `/bin/sh`

Most POSIX compliant scripts specify `/bin/sh` at the first line of the script, which means it will run `/bin/sh` as the shell, which by default in Arch is a symlink to `/bin/bash`.

You can re-symlink `/bin/sh` to `/bin/dash`, which can improve system performance, but first you must verify that none of the scripts that aren't explicitly `#!/bin/bash` scripts are safely POSIX compliant and do not require any of Bash's features.

### Identifying bashisms

Features of bash that aren't included in Dash ('bashisms') will not work without being explicitly pointed to `/bin/bash`. The following instructions will allow you to find any scripts that may need modification.

Install [checkbashisms](https://www.archlinux.org/packages/?name=checkbashisms).

#### Common places to check

*   Installed scripts with a `#!/bin/sh` shebang:

```
$ gawk '/^#!.*( |[/])sh/{printf "%s\0", FILENAME} {nextfile}' /usr/bin/* | xargs -0 checkbashisms

```

*   `pacman -Qlq` can be used to list all pacman-installed files.

### Relinking /bin/sh

Once you have verified that it won't break any functionality, it should be safe to relink `/bin/sh`. To do so use the following command:

```
# ln -sfT dash /usr/bin/sh

```

Updates of Bash will overwrite `/bin/sh` with the default symlink. To prevent this, use the following [pacman hook](/index.php/Pacman_hook "Pacman hook"), which will relink `/bin/sh` after every affected update:

```
[Trigger]
Type = Package
Operation = Install
Operation = Upgrade
Target = bash

[Action]
Description = Re-pointing /bin/sh symlink to dash...
When = PostTransaction
Exec = /usr/bin/ln -sfT dash /usr/bin/sh
Depends = dash

```

This is provided by [dashbinsh](https://aur.archlinux.org/packages/dashbinsh/).

## See also

*   [http://article.gmane.org/gmane.linux.arch.devel/11418](http://article.gmane.org/gmane.linux.arch.devel/11418):
*   [https://mailman.archlinux.org/pipermail/arch-dev-public/2007-November/003053.html](https://mailman.archlinux.org/pipermail/arch-dev-public/2007-November/003053.html)
*   [https://launchpad.net/ubuntu/+spec/dash-as-bin-sh](https://launchpad.net/ubuntu/+spec/dash-as-bin-sh)
*   [https://wiki.ubuntu.com/DashAsBinSh](https://wiki.ubuntu.com/DashAsBinSh)