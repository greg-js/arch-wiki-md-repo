**Warning:** Guix is **not** the [official package manager of Arch](/index.php/Pacman "Pacman"). It is also still under heavy development. Some packages may currently fail to build on Arch.

[GNU Guix](https://www.gnu.org/software/guix/) is a package manager that offers transactional, reproducible, per-user package management. While Guix can be used stand-alone and provide a full GNU distribution and a kernel by itself, you can install the Guix package manager on top of Arch to make Guix available to users while using a more traditional and mature Unix-like system as a base.

See the [Guix manual](https://www.gnu.org/software/guix/manual) for information on what per-user packaging commands Guix makes available to users.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Manual Installation](#Manual_Installation)
    *   [1.2 AUR Package Installation](#AUR_Package_Installation)
*   [2 Building packages outside of /tmp](#Building_packages_outside_of_/tmp)
*   [3 Uninstalling Guix](#Uninstalling_Guix)

## Installation

On Arch Linux you can install Guix either using the AUR or manually as described in the Guix Manual. Installing using the AUR has the advantage that pacman is aware of the package and the extra files in the `/usr` file tree. But contrarily to other AUR packages, uninstalling the package does not unwind the entire Guix installation. Since Guix is a package manager by itself and it can also update itself, you still have to manually uninstall the files installed via Guix (no matter whether you installed the AUR package or the manual installation). Therefore, after updating Guix once, the AUR advantage really turns into a disadvantage, as there will be many unnecessary files in the `/usr` file tree that are part of the Guix AUR package but that are never used by Guix anymore. Therefore, consider using the manual installation.

### Manual Installation

For the manual installation, see [chapter Installation](https://guix.gnu.org/manual/html_node/Installation.html#Installation) of the Guix manual. The easiest way is to use the shell installer script linked in there.

As of July 2019 this script installs files into the following locations:

*   `/gnu/store`, `/var/guix` (the Guix store)
*   `/usr/local/share/info`, `/usr/local/bin`, (only symlinks)
*   `/root/.config/guix` (a symlink to the current profile)

Furthermore it installs and enables a systemd service called `guix-daemon.service`, and creates users `guixbuilder01` ... `guixbuilder10` and a group `guixbuild`.

After running the script, create a new file called `/etc/profile.d/guix.sh`:

```
# Arrange so that ~/.config/guix/current paths end up first in 
# the particular path list.
for profile in "$HOME/.guix-profile" "$HOME/.config/guix/current"
do
  if [ -f "$profile/etc/profile" ]
  then
    # Load the user profile's settings.
    GUIX_PROFILE="$profile" ; \
    . "$profile/etc/profile"
  else
    # At least define this one so that basic things just work
    # when the user installs their first package.
    export PATH="$profile/bin${PATH:+:$PATH}"
    export INFOPATH="$profile/share/info${INFOPATH:+:$INFOPATH}"
  fi
done

unset profile

export GUIX_LOCPATH=$HOME/.guix-profile/lib/locale

```

Now start a new login shell (alternatively reboot your machine) and you can start using Guix:

```
# guix install glibc-locales

```

### AUR Package Installation

**Note:** The build check currently fails if `/bin/sh` is not a link to bash, which is not a problem on a default Arch installation.

**Note:** As of 13.05.2018 *guix-environment-container* test fails during makepkg build if [BUILDDIR environment variable](/index.php/Makepkg#Building_from_files_in_memory "Makepkg") points to tmpfs mount.

GNU Guix is available in the AUR as [guix](https://aur.archlinux.org/packages/guix/). As described in the `PKGBUILD`, the PGP key by the Guix distributor will need to be added first.

Guix makes builds more reproducible by running the build process using an unprivileged build user account. Therefore if you want to be able to build `*n*` packages simultaneously (e.g. for serving multiple users at the same time) you should create `*n*` build user accounts. as Guix should be able to build simultaneously. The following command does this the way described in [Guix manual](https://www.gnu.org/software/guix/manual/html_node/Build-Environment-Setup.html#Build-Environment-Setup):

```
# groupadd --system guixbuild
# uncomment and type e.g.  10  for   *n* below  -->  have ten users  
# for i in `seq -w 1 *n*`;
  do
    useradd -g guixbuild -G guixbuild           \
            -d /var/empty -s `which nologin`    \
            -c "Guix build user $i" --system    \
            guixbuilder$i;
  done

```

[Start and enable](/index.php/Systemd#Using_units "Systemd") `guix-daemon.service`.

You may want to authorize Guix to download and use binary packages (‘substitutes’) from the [Guix Official Substitute Server](http://ci.guix.gnu.org):

```
# guix archive --authorize < /usr/share/guix/ci.guix.gnu.org.pub

```

## Building packages outside of /tmp

The unit file may need to be extended to use a different `TMPDIR` for building if `/tmp` does not provide enough space (see the [Guix manual](https://www.gnu.org/software/guix/manual/html_node/Build-Environment-Setup.html#Build-Environment-Setup) for details). To use `*/tmpdir*` for building instead of `/tmp`, run

```
# systemctl edit guix-daemon.service

```

to add the following lines:

```
[Service]
Environment=TMPDIR=*/tmpdir*
```

## Uninstalling Guix

Stop and disable `guix-daemon.service`. If you installed Guix as an AUR package, then remove Guix using [pacman](/index.php/Pacman "Pacman").

Remove `/etc/systemd/system/guix-daemon.service`, `/etc/systemd/system/guix-daemon.service.d`, and `/etc/profile.d/guix.sh` if existent.

Now remove all the Guix build users and their group:

```
# for i in `seq -w 1 *n*`; do userdel guixbuilder$i; done
# groupdel guixbuild

```

Then remove the Guix store `/gnu` as well as `/var/guix` and `/var/log/guix`. Remove stall symlinks in `/usr/local/share/info` and `/usr/local/bin` if existent.