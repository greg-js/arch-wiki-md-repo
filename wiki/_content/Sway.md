# Sway

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

_sway_ (SirCmpwn's Wayland window manager) is an attempt to create a [Wayland](/index.php/Wayland "Wayland") version of [i3](/index.php/I3 "I3"), as an alternative to the official i3 Wayland port, i3way.

**Note:** This is still a work in progress so caution is advised. However, it is deemed ready for regular use by the creator.

## Installation

_sway_ can be [installed](/index.php/Installed "Installed") with the [sway-git](https://aur.archlinux.org/packages/sway-git/)<sup><small>AUR</small></sup> package. If you already use i3, then copy your i3 configuration to `~/.config/sway/config` and it will work out of the box. Otherwise, copy the sample configuration file to `~/.config/sway/config`. It is located at `/etc/sway/config`, unless the `DFALLBACK_CONFIG_DIR` flag has been set. See the sway(5) [man page](/index.php/Man_page "Man page") for information on the configuration.

## Usage

To actually use _sway_, you can type in a tty:

```
$ sway

```

However, if you want to start _sway_ in an X session for testing purposes it is possible to start it as a regular program or even from a [Display manager](/index.php/Display_manager "Display manager").

## See also

*   [Github project](https://github.com/SirCmpwn/sway)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Sway&oldid=412012](https://wiki.archlinux.org/index.php?title=Sway&oldid=412012)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Tiling WMs](/index.php/Category:Tiling_WMs "Category:Tiling WMs")
*   [Dynamic WMs](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs")