# Touhou

[Touhou Project](https://en.wikipedia.org/wiki/Touhou_Project) is the name of a series of [danmaku games](https://en.wikipedia.org/wiki/Danmaku#.22Bullet_hell.22_evolution_and_niche_appeal) (also know as "bullet-hell shooters")

Bullet-hell shooters is a genre of 2D shooters based on really complex patterns, which are beautiful and interesting to look at, and impiles great difficulty, memorizing patterns and fast player reaction.

Touhou Project games are one of the most popular of this genre because, among other things, the in-game world is a giant universe, the music (at least the WAVs in the full version) is spectacular, and, if you have been on the internet for a while, you might stumble upon its curious fanbase, which has produced videos, music, manga (japanese comics) and even unofficial games.

Despite the difficulty, they can be very addicting games.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Python Engine](#Python_Engine)
*   [2 Extra Info](#Extra_Info)
    *   [2.1 Installing the full version](#Installing_the_full_version)
    *   [2.2 MIDI Music](#MIDI_Music)
    *   [2.3 Audio in Windows-era games](#Audio_in_Windows-era_games)
*   [3 See also](#See_also)

## Installation

PC-98 games can be played using Linux-native X Neko Project II emulator ([xnp2](https://aur.archlinux.org/packages/xnp2/) in [AUR](/index.php/AUR "AUR")).

The following AUR packages only depend on [Wine](/index.php/Wine "Wine") to run (and timidity++ to play MIDI music). A python engine is under development to remove the wine dependency. They install the free trial versions. You can easily replace the trials with the full game if you have it.

These games have been packages in the AUR for your convenience:

*   Touhou 6: Embodiment of Scarlet Devil — [th06-demo-wine](https://aur.archlinux.org/packages/th06-demo-wine/) or [th06-demo-pytouhou](https://aur.archlinux.org/packages/th06-demo-pytouhou/)
*   Touhou 7: Perfect Cherry Blossom — [th07](https://aur.archlinux.org/packages/th07/)
*   Touhou 8: Imperishable Night — [th08](https://aur.archlinux.org/packages/th08/)

We need help [packaging](/index.php/Wine_PKGBUILD_Guidelines "Wine PKGBUILD Guidelines") more Touhou games for the AUR. This is a list of games that have free, downloadable trial editions to build off of:

*   Touhou 9: Phantasmagoria of Flower View
*   Touhou 10: Mountain of Faith
*   Touhou 11: Subterranean Animism
*   Touhou 12: Undefined Fantastic Object
*   Touhou 13: Ten Desires

### Python Engine

[Linkmauve](http://linkmauve.fr/doc/touhou/) has made an experimental python engine to make the games more portable. It is definitely not stable, and is more of an outline for an engine than an actual one, but it is interesting nonetheless. See packages [pytouhou-hg](https://aur.archlinux.org/packages/pytouhou-hg/) and [th06-demo-data](https://aur.archlinux.org/packages/th06-demo-data/) in AUR.

## Extra Info

### Installing the full version

If you have the full version of either Imperishable Night or Perfect Cherry Blossom, you can place them in your home folder, or you can place them in the overlay so that they will work in the liveCD and also get installed to disk.

NOTE: **.th08** is Imperishable Night's wineprefix folder, and **.th07** is Perfect Cherry Blossom's.

1.  Find the folder with the Touhou game files.
2.  Set your file manager to see hidden files/folders. (in Cherimoya's Dolphin file manager, just press **Alt+. (the period key)**)
3.  Go to your "Home" folder and find the folders ".th08" and/or ".th07".
4.  Paste your game files right over the shortcuts in either ".th08" or ".th07"
5.  Start your games normally. They will use the full version.

### MIDI Music

If you are using the trial edition, they only include MIDI files. To play them, you will also need to install Timidity++ ([timidity++](https://www.archlinux.org/packages/?name=timidity%2B%2B)) along with some soundfonts ([timidity-freepats](https://www.archlinux.org/packages/?name=timidity-freepats)).

Now add the following lines to Timidity++ configuration file:

 `/etc/timidity++/timidity.cfg` 

```
dir /usr/share/timidity/freepats
source /etc/timidity++/freepats/freepats.cfg

```

Remember to [start](/index.php/Daemons "Daemons") the **timidity++** daemon before play.

### Audio in Windows-era games

If you find that you have no audio in any of the Windows era or later games (Touhou 6 and later), make sure to install [lib32-alsa-utils](https://www.archlinux.org/packages/?name=lib32-alsa-utils) and [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins), and recheck your configuration in winecfg. In addition, set the audio in-game to "WAV" mode.

## See also

*   [Touhou Project on Wikipedia](https://en.wikipedia.org/wiki/Touhou_Project)
*   [Running Touhou Games in Linux](http://en.touhouwiki.net/wiki/Running_in_Linux_and_MacOS_X)
*   [Wine PKGBUILD Guidelines](/index.php/Wine_PKGBUILD_Guidelines "Wine PKGBUILD Guidelines")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Touhou&oldid=399132](https://wiki.archlinux.org/index.php?title=Touhou&oldid=399132)"