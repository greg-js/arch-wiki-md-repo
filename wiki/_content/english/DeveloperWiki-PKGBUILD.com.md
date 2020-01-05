<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Warning](#Warning)
*   [2 Directories that must be used](#Directories_that_must_be_used)
*   [3 Creating chroots and building packages](#Creating_chroots_and_building_packages)
*   [4 x86_64](#x86_64)
*   [5 Packager && Makeflags](#Packager_&&_Makeflags)
*   [6 Connecting to sigurd or gerolde from brynhild](#Connecting_to_sigurd_or_gerolde_from_brynhild)
*   [7 Generating rebuilding list when soname is bumped](#Generating_rebuilding_list_when_soname_is_bumped)

## Warning

This article now describes the build server at **dragon.archlinux.org** instead.

## Directories that must be used

All users should use **only** `~/packages` for storing packages builds and `~/svn-packages`. These directories are excluded from backups and all other directories are automatically backed up.

## Creating chroots and building packages

Devtools 0.9.10 has build helpers that can be used.

```
/usr/bin/extra-x86_64-build
/usr/bin/multilib-build
/usr/bin/staging-x86_64-build
/usr/bin/testing-x86_64-build

```

This can be used to _create_ and build packages. Chroots are created by default in /var/tmp/archbuild. To build packages that depend on each other you should use makechrootpkg directly.

```
$ sudo extra-x86_64-build
$ sudo testing-x86_64-build

```

## x86_64

```
$ sudo makechrootpkg -cr /var/lib/archbuild/extra-x86_64 -- -i

```

next package

```
$ sudo makechrootpkg -r /var/lib/archbuild/extra-x86_64

```

## Packager && Makeflags

```
Add ~/.makepkg.conf with PACKAGER information

```

```
PACKAGER="Name <email>"
MAKEFLAGS="-j5"

```

## Connecting to sigurd or gerolde from brynhild

On your local system add this:

```
$ cat .ssh/config
  Host pkgbuild.com
    Hostname pkgbuild.com
    User youruser
    ForwardAgent yes

```

## Generating rebuilding list when soname is bumped

Available in repo-tools.git ([https://projects.archlinux.de/repo-tools.git/](https://projects.archlinux.de/repo-tools.git/)) and available on brynhild:

```
$ sogrep <repo> <soname>
$ sogrep extra x264.so.107

```