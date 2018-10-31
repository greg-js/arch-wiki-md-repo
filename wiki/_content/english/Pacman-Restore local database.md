Signs that pacman needs a local database restoration:

*   `pacman -Q` gives absolutely no output, and `pacman -Syu` erroneously reports that the system is up to date.
*   When trying to install a package using `pacman -S package`, and it outputs a list of already satisfied dependencies.

Most likely, pacman's database of installed software, `/var/lib/pacman/local`, has been corrupted or deleted. While this is a serious problem, it can be restored by following the instructions below.

Firstly, make sure pacman's log file is present:

```
$ ls /var/log/pacman.log

```

If it does not exist, it is *not* possible to continue with this method. You may be able to use [Xyne's package detection script](https://bbs.archlinux.org/viewtopic.php?pid=670876) to recreate the database. If not, then the likely solution is to re-install the entire system.

## Generating the package recovery list

**Warning:** If for some reason your [pacman](/index.php/Pacman "Pacman") cache or [makepkg](/index.php/Makepkg "Makepkg") package destination contain packages for other architectures, remove them before continuation.

[Install](/index.php/Install "Install") the [pacutils](https://www.archlinux.org/packages/?name=pacutils) package to get paclog.

Create the log filter script and make it executable:

 `pacrecover` 
```
#!/bin/bash -e

. /etc/makepkg.conf

PKGCACHE=$((grep -m 1 '^CacheDir' /etc/pacman.conf || echo 'CacheDir = /var/cache/pacman/pkg') | sed 's/CacheDir = //')

pkgdirs=("$@" "$PKGDEST" "$PKGCACHE")

while read -r -a parampart; do
  pkgname="${parampart[0]}-${parampart[1]}-*.pkg.tar.xz"
  for pkgdir in ${pkgdirs[@]}; do
    pkgpath="$pkgdir"/$pkgname
    [ -f $pkgpath ] && { echo $pkgpath; break; };
  done || echo ${parampart[0]} 1>&2
done

```

Run the script (optionally passing additional directories with packages as parameters):

```
$ paclog --pkglist /var/log/pacman.log | ./pacrecover >files.list 2>pkglist.orig

```

This way two files will be created: `files.list` with package files, still present on machine and `pkglist.orig`, packages from which should be downloaded. Later operation may result in mismatch between files of older versions of package, still present on machine, and files, found in new version. Such mismatches will have to be fixed manually.

Here is a way to automatically restrict second list to packages available in a repository:

```
$ { cat pkglist.orig; pacman -Slq; } | sort | uniq -d > pkglist

```

**Note:** If this fails with `failed to initialise alpm library`, then check if `/var/lib/pacman/local/ALPM_DB_VERSION` exists - if not, then run `pacman-db-upgrade` as root followed by `pacman -Sy` and then **retry the previous command**.

Check if some important *base* package are missing, and add them to the list:

```
$ comm -23 <(pacman -Sgq base | sort) pkglist.orig >> pkglist

```

Proceed once the contents of both lists are satisfactory, since they will be used to restore pacman's installed package database; `/var/lib/pacman/local/`.

## Performing the recovery

Define a bash function for recovery purposes:

```
 recovery-pacman() {
    sudo pacman "$@"  \
    --log /dev/null   \
    --noscriptlet     \
    --dbonly          \
    --force           \
    --nodeps          \
    --needed
}

```

`--log /dev/null` allows to avoid needless pollution of pacman log, `--needed` will save some time by skipping packages, already present in database, `--nodeps` will allow installation of cached packages, even if packages being installed depend on newer versions. Rest of options will allow **pacman** to operate without reading/writing filesystem.

Populate the sync database:

```
# pacman -Sy

```

Start database generation by installing locally available package files from `files.list`:

```
# recovery-pacman -U $(< files.list)

```

Install the rest from `pkglist`:

```
# recovery-pacman -S $(< pkglist)

```

Update the local database so that packages that are not required by any other package are marked as explicitly installed and the other as dependences. You will need be extra careful in the future when removing packages, but with the original database lost is the best we can do.

```
# pacman -D --asdeps $(pacman -Qq)
# pacman -D --asexplicit $(pacman -Qtq)

```

Optionally check all installed packages for corruption:

```
# pacman -Qk

```

Optionally [Pacman/Tips and tricks#Identify files not owned by any package](/index.php/Pacman/Tips_and_tricks#Identify_files_not_owned_by_any_package "Pacman/Tips and tricks").

Update all packages:

```
# pacman -Su

```