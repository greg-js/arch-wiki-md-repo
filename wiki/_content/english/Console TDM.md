Related articles

*   [Display manager](/index.php/Display_manager "Display manager")
*   [CDM](/index.php/CDM "CDM")

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

**Tip:** Since version 1.3.0, `tdm` may be forced to start if X is already running by adding the `--disable-xrunning-check` flag to the first call of `tdm`.

Regardless of which shell is used you should edit `~/.xinitrc` by replace your existing `exec` line with:

```
exec tdm --xstart

```

## Configuration

**Note:** Since version 1.3.0, `tdm` follows the XDG base directory specification. By default, `$XDG_CONFIG_HOME` is set to `$HOME/.config`.

**Warning:** Since support for `~/.tdm` will eventually be dropped, consider moving your configuration to `$XDG_CONFIG_HOME/tdm`. You can use `tdmctl migrate` to automatically migrate your configuration.

You should copy the links to your WM/DE starter to `$XDG_CONFIG_HOME/tdm/sessions`, and links to non-X programs to `$XDG_CONFIG_HOME/tdm/extra`. For convenience, you can just run `tdmctl init`.

The use of the program `tdmctl` is much like `systemctl`, and it's a powerful tool to configure Console TDM.

You can customize Console TDM by editing `$XDG_CONFIG_HOME/tdm/tdminit` (sourced before the user is prompted for a session) and `$XDG_CONFIG_HOME/tdm/tdmexit` (sourced before the session is actually started).

## See also

*   [Homepage](http://dopsi.github.io/console-tdm/)