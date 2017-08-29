[Ly](https://github.com/cylgom/ly) is an experimental [display manager](/index.php/Display_manager "Display manager") using ncurses.

## Installation

[Install](/index.php/Install "Install") the [ly-git](https://aur.archlinux.org/packages/ly-git/) package.

## Configuration

*Ly* is configured through its `config.h` file, consider maintaining your own [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") with your `config.h`.

## Usage

1.  [Disable](/index.php/Disable "Disable") other display managers.
2.  [Enable](/index.php/Enable "Enable") `ly.service`.
3.  [Disable](/index.php/Disable "Disable") `getty@tty2.service`: getty on the tty used by *Ly* (tty2 by default), to prevent *login* from spawning on top of it.