[Dash](https://en.wikipedia.org/wiki/Debian_Almquist_shell "wikipedia:Debian Almquist shell") is a minimalist POSIX-compliant shell. It can be much faster than Bash, and takes up less memory when in use. Most POSIX compliant scripts specify `/bin/sh` at the first line of the script, which means it will run `/bin/sh` as the shell, which by default in Arch is a symlink to `/bin/bash`.

## Contents

*   [1 Installation](#Installation)
*   [2 Use DASH as default shell](#Use_DASH_as_default_shell)
    *   [2.1 Identifying bashisms](#Identifying_bashisms)
        *   [2.1.1 Common places to check](#Common_places_to_check)
    *   [2.2 Relinking /bin/sh](#Relinking_.2Fbin.2Fsh)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [dash](https://www.archlinux.org/packages/?name=dash) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Use DASH as default shell

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

[http://article.gmane.org/gmane.linux.arch.devel/11418](http://article.gmane.org/gmane.linux.arch.devel/11418):

*   [https://mailman.archlinux.org/pipermail/arch-dev-public/2007-November/003053.html](https://mailman.archlinux.org/pipermail/arch-dev-public/2007-November/003053.html)
*   [https://launchpad.net/ubuntu/+spec/dash-as-bin-sh](https://launchpad.net/ubuntu/+spec/dash-as-bin-sh)
*   [https://wiki.ubuntu.com/DashAsBinSh](https://wiki.ubuntu.com/DashAsBinSh)