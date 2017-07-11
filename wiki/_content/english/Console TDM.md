[Console TDM](https://github.com/dopsi/console-tdm) is an extension for xorg-xinit written in pure bash. It is inspired by CDM, which aimed to be a replacement of display managers such as GDM.

## Installation

[Install](/index.php/Install "Install") the [console-tdm](https://aur.archlinux.org/packages/console-tdm/) package ([console-tdm-git](https://aur.archlinux.org/packages/console-tdm-git/) package for the development version).

Now ensure no other display managers get started by [disabling](/index.php/Disabling "Disabling") their systemd services.

After installing Console TDM, you should modify your `~/.bash_profile`, and add a line:

```
source /usr/bin/tdm

```

If you use [zsh](/index.php/Zsh "Zsh"), add to your `~/.zprofile` the following line:

```
bash /usr/bin/tdm

```

or

```
tdm

```

Regardless of which shell is used you should edit `~/.xinitrc` by replace your existing `exec` line with:

```
exec tdm --xstart

```

## Configuration

You should copy the links to your WM/DE starter to `~/.tdm/sessions`, and links to non-X programs to `~/.tdm/extra`. For convenience, you can just run `tdmctl init`.

The use of the program `tdmctl` is much like `systemctl`, and it's a powerful tool to configure Console TDM.

You can customize Console TDM by editing `~/.tdm/tdminit`.

## See also

*   [Homepage](http://dopsi.github.io/console-tdm/)