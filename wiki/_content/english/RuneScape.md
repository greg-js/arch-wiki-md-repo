From [Wikipedia](https://en.wikipedia.org/wiki/RuneScape "wikipedia:RuneScape"):

	*RuneScape is a fantasy massively multiplayer online role-playing game (MMORPG) released in January 2001 by Andrew and Paul Gower, and developed and published by Jagex Games Studio. It is a graphical browser game implemented on the client-side in Java or HTML5, and incorporates 3D rendering. The game has had over 200 million accounts created and is recognised by the Guinness World Records as the world's largest free MMORPG and the most-updated game.*

## Contents

*   [1 Methods to play](#Methods_to_play)
    *   [1.1 RuneScape NXT](#RuneScape_NXT)
    *   [1.2 Rsu-client](#Rsu-client)
    *   [1.3 OSBuddy (Old School RuneScape only)](#OSBuddy_.28Old_School_RuneScape_only.29)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Runescape UI flicker](#Runescape_UI_flicker)

## Methods to play

### RuneScape NXT

Install the official RuneScape NXT client with the [runescape-launcher](https://aur.archlinux.org/packages/runescape-launcher/) package.

### Rsu-client

**Note:** If you are unable to install the client from the AUR because of a problem with [perl-wx](https://aur.archlinux.org/packages/perl-wx/), remove it from the [depends array](/index.php/PKGBUILD#depends "PKGBUILD"). [perl-wx](https://aur.archlinux.org/packages/perl-wx/) is needed for the [GUI](https://en.wikipedia.org/wiki/Graphical_user_interface "wikipedia:Graphical user interface"). The client will work fine without it, but you will not have a [GUI](https://en.wikipedia.org/wiki/Graphical_user_interface "wikipedia:Graphical user interface").

Rsu-client is an unofficial RuneScape Unix/Linux Client and it's currently the recommended way to play RuneScape/Old School RuneScape. It's available to install from the AUR [unix-runescape-client](https://aur.archlinux.org/packages/unix-runescape-client/), or you can manually grab the source at [https://github.com/HikariKnight/rsu-client](https://github.com/HikariKnight/rsu-client). After installation, to start playing, open either “RuneScape” or “RuneScape OldSchool”, depending on what version you are interested in.

### OSBuddy (Old School RuneScape only)

[OSBuddy](https://rsbuddy.com/osbuddy/) is a third-party toolkit for Old School RuneScape which in addition to a client offers useful features, such as highscores, notes, price checker etc. It's available for installation from the AUR, [osbuddy](https://aur.archlinux.org/packages/osbuddy/).

## Troubleshooting

### Runescape UI flicker

Issue has been solved by the [2017-06-11 patch](http://services.runescape.com/m=forum/l=0/sl=0/forums.ws?15,16,160,65917986).