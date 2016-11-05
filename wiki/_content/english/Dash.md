[DASH (Debian Almquist shell)](https://en.wikipedia.org/wiki/Debian_Almquist_shell "wikipedia:Debian Almquist shell") is a modern POSIX-compliant implementation of [`/bin/sh` (sh, Bourne shell)](https://en.wikipedia.org/wiki/Bourne_shell "wikipedia:Bourne shell").

Not [Bash](/index.php/Bash "Bash") compatible, it is other way round.

DASH shines in:

*   Speed of execution. As simple, roughly [4x times faster](https://unix.stackexchange.com/questions/148035/is-dash-or-some-other-shell-faster-than-bash) than Bash and others.
*   Very limited resources (disc space, RAM or CPU). As minimalistic - much smaller (134.1 kB vs 6.5 MB installed, 13 kSLOC vs 176 kSLOC) then Bash and others.
*   Security. Long ago established tiny project, with simple and long ago established functionality. While it is well [alive](https://git.kernel.org/cgit/utils/dash/dash.git/log/) project with [many](https://git.kernel.org/cgit/utils/dash/dash.git/stats/?period=q&ofs=10) developers. Which mean small attack surface, while many eyes on code.
*   If classic `/bin/sh` needed only.

## Contents

*   [1 Installation](#Installation)
*   [2 Use DASH as /bin/sh](#Use_DASH_as_.2Fbin.2Fsh)
    *   [2.1 Identifying bashisms](#Identifying_bashisms)
        *   [2.1.1 Common places to check](#Common_places_to_check)
    *   [2.2 Relinking /bin/sh](#Relinking_.2Fbin.2Fsh)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [dash](https://www.archlinux.org/packages/?name=dash) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Use DASH as `/bin/sh`

Most POSIX compliant scripts specify `/bin/sh` at the first line of the script, which means it will run `/bin/sh` as the shell, which by default in Arch is a symlink to `/bin/bash`.

You can re-symlink `/bin/sh` to `/bin/dash`, which can improve system performance, but first you must verify that none of the scripts that aren't explicitly `#!/bin/bash` scripts are safely POSIX compliant and do not require any of Bash's features.

### Identifying bashisms

Features of bash that aren't included in Dash ('bashisms') will not work without being explicitly pointed to `/bin/bash`. The following instructions will allow you to find any scripts that may need modification.

Install [checkbashisms](https://aur.archlinux.org/packages/checkbashisms/) from the [AUR](/index.php/AUR "AUR").

#### Common places to check

*   Installed scripts with a `#!/bin/sh` shebang:

```
$ checkbashisms -f -p $(grep -IrlE '^#! ?(/usr)?/bin/(env )?sh' /usr/bin)

```

### Relinking /bin/sh

Once you have verified that it won't break any functionality, it should be safe to relink `/bin/sh`. To do so use the following command:

```
# ln -sfT dash /bin/sh

```

Updates of Bash could overwrite `/bin/sh`. To prevent this, add the following lines to the `[options]` section of `/etc/pacman.conf`:

```
NoUpgrade   = usr/bin/sh
NoExtract   = usr/bin/sh

```

## See also

*   [http://article.gmane.org/gmane.linux.arch.devel/11418](http://article.gmane.org/gmane.linux.arch.devel/11418):
*   [https://mailman.archlinux.org/pipermail/arch-dev-public/2007-November/003053.html](https://mailman.archlinux.org/pipermail/arch-dev-public/2007-November/003053.html)
*   [https://launchpad.net/ubuntu/+spec/dash-as-bin-sh](https://launchpad.net/ubuntu/+spec/dash-as-bin-sh)
*   [https://wiki.ubuntu.com/DashAsBinSh](https://wiki.ubuntu.com/DashAsBinSh)