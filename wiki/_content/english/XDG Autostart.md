The [XDG Autostart specification](https://specifications.freedesktop.org/autostart-spec/autostart-spec-latest.html) defines a method for [autostarting](/index.php/Autostarting "Autostarting") ordinary [desktop entries](/index.php/Desktop_entries "Desktop entries") on [desktop environment](/index.php/Desktop_environment "Desktop environment") startup and removable medium mounting, by placing them in specific [#Directories](#Directories).

## Prerequisites

You need to use either a [desktop environment](/index.php/Desktop_environment "Desktop environment") that supports it, or a dedicated implementation, like [dex](https://www.archlinux.org/packages/?name=dex), [dapper](https://aur.archlinux.org/packages/dapper/), or [fbautostart](https://aur.archlinux.org/packages/fbautostart/).

## Directories

The Autostart directories in order of preference are:

*   user-specific: `$XDG_CONFIG_HOME/autostart` (`~/.config/autostart` by default)
*   system-wide: `$XDG_CONFIG_DIRS/autostart` (`/etc/xdg/autostart` by default)[[1]](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html#referencing)

System-wide [desktop entries](/index.php/Desktop_entries "Desktop entries") can be overridden by user-specific entries with the same filename.

To disable a system-wide entry, create an overriding entry containing `Hidden=true`.

For more details, read [the specification](https://specifications.freedesktop.org/autostart-spec/autostart-spec-latest.html).