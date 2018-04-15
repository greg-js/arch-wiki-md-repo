The [XDG Autostart specification](https://specifications.freedesktop.org/autostart-spec/autostart-spec-latest.html) defines a standard for [autostarting](/index.php/Autostarting "Autostarting") ordinary [desktop entries](/index.php/Desktop_entries "Desktop entries") on [desktop environment](/index.php/Desktop_environment "Desktop environment") startup and removable medium mounting, by placing them in specific [#Directories](#Directories).

## Prerequisites

You need to use either a [desktop environment](/index.php/Desktop_environment "Desktop environment") that supports it, or a dedicated implementation, like [dex](https://www.archlinux.org/packages/?name=dex), [dapper](https://aur.archlinux.org/packages/dapper/), or [fbautostart](https://aur.archlinux.org/packages/fbautostart/).

## Directories

An XDG-compliant desktop environment will automatically start [desktop entries](/index.php/Desktop_entries "Desktop entries") found in the following directories:

*   System-wide: `$XDG_CONFIG_DIRS/autostart/` (`/etc/xdg/autostart/` by default)

*   [GNOME](/index.php/GNOME "GNOME") also starts files found in `/usr/share/gnome/autostart/`

*   User-specific: `$XDG_CONFIG_HOME/autostart/` (`~/.config/autostart/` by default)

Users can override system-wide [desktop entries](/index.php/Desktop_entries "Desktop entries") by copying them into the user-specific directory.

For a more details, consult [the specification](http://standards.freedesktop.org/autostart-spec/autostart-spec-latest.html).