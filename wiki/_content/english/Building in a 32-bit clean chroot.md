Related articles

*   [DeveloperWiki:Building in a clean chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot")

*Native* 32-bit packages can be built in [a clean chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot").

## Setting up a chroot

First, create a directory in which the chroot will reside. For example, `$HOME/chroot32`.

```
$ mkdir ~/chroot32

```

Copy `/etc/pacman.conf` and `/etc/makepkg.conf` into this directory and specify 32-bit options in them:

In `~/chroot32/pacman.conf`, set:

```
Architecture = i686

```

**Note:** Comment out any `[multilib]` repositories!

In `~/chroot32/makepkg.conf`, set:

```
CARCH="i686"
CHOST="i686-unknown-linux-gnu"
CFLAGS="-march=i686 -mtune=generic -O2 -pipe"
CXXFLAGS="-march=i686 -mtune=generic -O2 -pipe"

```

Then create the chroot:

```
$ mkarchroot -C ~/chroot32/pacman.conf -M ~/chroot32/makepkg.conf ~/chroot32/root base-devel

```

See [DeveloperWiki:Building in a clean chroot#Setting up a chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot#Setting_up_a_chroot "DeveloperWiki:Building in a clean chroot") for more details.

## Building in the chroot

Specify this chroot to makechrootpkg to build i686 packages:

```
$ makechrootpkg -c -r ~/chroot32/

```

See [DeveloperWiki:Building in a clean chroot#Building in the chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot#Building_in_the_chroot "DeveloperWiki:Building in a clean chroot") for more details.