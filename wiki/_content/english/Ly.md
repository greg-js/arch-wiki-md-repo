[Ly](https://github.com/cylgom/ly) is an experimental display manager using ncurses.

## Installation

[Install](/index.php/Install "Install") the [ly-git](https://aur.archlinux.org/packages/ly-git/) package.

Now ensure no other display managers get started by disabling their systemd services with `systemctl disable`.

For example, if you were using the Gnome Display Manager, you would stop it from starting at boot by running

```
# systemctl disable gdm.service

```

Enable the systemd service

```
# systemctl enable ly.service

```

Disable getty on the tty used by *Ly* (tty2 by default), to prevent *login* from spawning on top of it

```
# systemctl disable getty@tty2.service

```

## Configuration

*Ly* is configured through its `config.h` file, consider maintaining your own [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") with your `config.h`.