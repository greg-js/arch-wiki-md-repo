# Stalonetray

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Stalonetray is a stand-alone freedesktop.org and KDE system tray for the [X Window System](/index.php/X_Window_System "X Window System"). It has full XEMBED support, minimal dependencies and works with virtually any EWMH-compliant window manager. Window managers that are reported to work well with stalonetray are: [FVWM](/index.php/FVWM "FVWM"), [Openbox](/index.php/Openbox "Openbox"), [Enlightenment](/index.php/Enlightenment "Enlightenment"), [Ion3](/index.php/Ion3 "Ion3"), [Compiz](/index.php/Compiz "Compiz"), [Xmonad](/index.php/Xmonad "Xmonad"), [dwm](/index.php/Dwm "Dwm"), and [awesome](/index.php/Awesome "Awesome").

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Openbox](#Openbox)
    *   [2.2 Ion3](#Ion3)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Icons do not have the desired size](#Icons_do_not_have_the_desired_size)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Pacman "Pacman") [stalonetray](https://www.archlinux.org/packages/?name=stalonetray) from the [official repositories](/index.php/Official_repositories "Official repositories"). Once installed, copy the `stalonetrayrc` file to your home directory. Note that you should do this as a regular user.

```
$ cp /etc/stalonetrayrc ~/.stalonetrayrc

```

## Configuration

### Openbox

To run Stalonetray in Openbox, `dockapp-mode` must be set to `simple`. This can be accomplished with either the command-line argument `--dockapp-mode simple` or by modifying `~/.stalonetrayrc`.

Openbox now treats the tray as the dock, and you can adjust its position by using the Openbox Configuration Tool. To run Stalonetray on start up, add the following to `~/.config/openbox/autostart`:

```
stalonetray --dockapp-mode simple &

```

See also [Stalonetray WM hints for OpenBox](http://stalonetray.sourceforge.net/wmhints.html#openbox)

### Ion3

To run Stalonetray in Ion3:

```
$ stalonetray --kludges=force_icons_size,fix_window_pos

```

To include stalonetray in the statusbar, add the following to your configuration file in `~/.ion3/`:

```
-- Create a statusbar
mod_statusbar.create{
    screen=0,
    pos='bl',
    fullsize=true,
    systray=true,
    template="[ %date || %load || ... ] %systray%filler%systray_stalone",
}

defwinprop{class="stalonetray",instance="stalonetray",statusbar="systray_stalone"}
defwinprop{instance="stalonetray",statusbar="systray_stalone"}
defwinprop{class="stalonetray",statusbar="systray_stalone"}

```

See also [Stalonetray WM hints for ion3](http://stalonetray.sourceforge.net/wmhints.html#ion3)

## Troubleshooting

### Icons do not have the desired size

To force the size of the icons to be equal to icon_size, launch stalonetray with the following arguments:

```
stalonetray --icon-size=16 --kludges=force_icons_size

```

This will force the size of all icons to 16×16 pixels.

Alternatively, one could add the following to the configuration file:

```
icon_size 16
kludges force_icons_size

```

## See also

*   [http://stalonetray.sourceforge.net/manpage.html](http://stalonetray.sourceforge.net/manpage.html) - Stalonetray manual page

Retrieved from "[https://wiki.archlinux.org/index.php?title=Stalonetray&oldid=377117](https://wiki.archlinux.org/index.php?title=Stalonetray&oldid=377117)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Eye candy](/index.php/Category:Eye_candy "Category:Eye candy")