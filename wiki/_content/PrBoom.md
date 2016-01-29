# PrBoom

[PrBoom](http://prboom.sourceforge.net/) is a cross-platform version of the classic 3D first person shooter [Doom](https://en.wikipedia.org/wiki/Doom_(video_game) "wikipedia:Doom (video game)") from id Software. Originally written for Microsoft Windows, PrBoom has since been ported to Linux and many other platforms. It offers a number of enhancements over the original game, including OpenGL rendering and high video resolutions, while attempting to remain true to the original Doom in terms of play. You will need the original Doom data, unless you install the FreeDoom package (see below).

## Contents

*   [1 Installation](#Installation)
*   [2 Use](#Use)
*   [3 Net](#Net)
*   [4 Music](#Music)
*   [5 Data](#Data)

## Installation

[prboom](https://aur.archlinux.org/packages/prboom/)<sup><small>AUR</small></sup> is available from the AUR.

## Use

To use prboom with an IWad file with default settings (unless you already have ~/.prboom/prboom.cfg edited):

```
# prboom -iwad /path/to/file

```

To change window resolution (you must disable fullscreen in options ingame):

```
# prboom -width 800 -height 600 -iwad /path/to/file 

```

A full list of settings can be found in the [man pages](http://pwet.fr/man/linux/jeux/prboom).

## Net

To start a server:

```
# prboom-game-server

```

By default it listens on port 5030, so to join the game:

```
# prboom -net localhost:5030 -iwad /path/to/file

```

## Music

If music is not working, then follow these steps.

```
# pacman -S timidity++ timidity-freepats

```

Edit /etc/timidity++/timidity.cfg , and add:

```
dir /usr/share/timidity/freepats
source /etc/timidity++/freepats/freepats.cfg

```

Please note that freepats is an incomplete soundfont ; therefore it will not play every instrument used by Doom and Doom 2\. You should consider installing an alternative [soundfont](/index.php/Timidity#SoundFonts "Timidity").

## Data

If you do not have the original Doom data available to play PrBoom, you can install the [freedoom1](https://aur.archlinux.org/packages/freedoom1/)<sup><small>AUR</small></sup> or [freedoom2](https://aur.archlinux.org/packages/freedoom2/)<sup><small>AUR</small></sup> package from the [AUR](/index.php/AUR "AUR").

This will place the data in the correct directory, so you can just start PrBoom and frag away!

Retrieved from "[https://wiki.archlinux.org/index.php?title=PrBoom&oldid=353070](https://wiki.archlinux.org/index.php?title=PrBoom&oldid=353070)"