**Warning:** Guix is **not** the [official package manager of Arch](/index.php/Pacman "Pacman"). It is also still under heavy development. Some packages may currently fail to build on Arch.

[GNU Guix](https://www.gnu.org/software/guix/) is a package manager that offers transactional, reproducible, per-user package management. While Guix can be used stand-alone and provide a full GNU distribution and a kernel by itself, you can install the Guix package manager on top of Arch to make Guix available to users while using a more traditional and mature Unix-like system as a base.

See the [Guix manual](https://www.gnu.org/software/guix/manual) for information on what per-user packaging commands Guix makes available to users.

## Contents

*   [1 Installation](#Installation)
*   [2 Running](#Running)
    *   [2.1 Building packages outside of /tmp](#Building_packages_outside_of_.2Ftmp)
*   [3 Uninstalling Guix](#Uninstalling_Guix)

## Installation

**Note:** The build check currently fails if `/bin/sh` is not a link to bash, which is not a problem on a default Arch installation.

**Note:** As of 13.05.2018 *guix-environment-container* test fails during makepkg build if [BUILDDIR environment variable](/index.php/Makepkg#Building_from_files_in_memory "Makepkg") points to tmpfs mount.

GNU Guix is available in the AUR as [guix](https://aur.archlinux.org/packages/guix/). As described in the `PKGBUILD`, the PGP key by the Guix distributor will need to be added first.

## Running

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

You may want to authorize Guix to download and use binary packages (‘substitutes’) from [Hydra](http://hydra.gnu.org):

```
# guix archive --authorize < /usr/share/guix/hydra.gnu.org.pub

```

### Building packages outside of /tmp

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

Disable `guix-daemon.service` and then remove Guix using [pacman](/index.php/Pacman "Pacman"). Now remove all the Guix build users and their group:

```
# for i in `seq -w 1 *n*`; do userdel guixbuilder$i; done
# groupdel guixbuild

```

Then remove the Guix store `/gnu` as well as `/var/guix` and `/var/log/guix`. If you edited `guix-daemon.service`, you may want to remove `/etc/systemd/system/guix-daemon.service.d` as well.