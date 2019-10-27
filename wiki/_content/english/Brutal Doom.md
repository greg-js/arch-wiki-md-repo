[Brutal Doom](http://www.moddb.com/mods/brutal-doom) is a gore-themed gameplay mod that was created in 2010 by Marcos Abenante (Sergeant_Mark_IV). It is compatible with Doom, The Ultimate Doom, Doom II: Hell on Earth, Final Doom, and other custom WADs. Brutal Doom won the first ever Cacoward in 2011 for Best Gameplay Mod and a MOTY award for creativity by Mod DB in 2012.

The mod adds features many new graphical effects like additional blood (blood gets splattered on walls and ceilings if enemies or the player get hit), the ability to blow off body parts with strong weapons like the shotgun, new death animations, fake flares and 3D blood effects for OpenGL, and the addition of special illuminating effects on projectiles and pick ups. It is compatible with the source ports ZDoom, GZDoom, Skulltag, and Zandronum.

While primarily a gore mod, it goes further and alters the gameplay by changing the weapons, monster AI, sounds, graphics, and combat. One such change is the increased difficulty, making enemy behavior much faster, unpredictable and dangerous (many attacks do double the normal damage to the player) and altering their attacks. It makes the animations smoother and gives the player new abilities. [[1]](http://doom.wikia.com/wiki/Brutal_Doom) [[2]](https://doomwiki.org/wiki/Brutal_Doom)

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Brutal Doom Mod](#Brutal_Doom_Mod)
    *   [1.2 Configuration](#Configuration)
*   [2 See Also](#See_Also)

## Installation

[Install](/index.php/Install "Install") the [brutal-doom](https://aur.archlinux.org/packages/brutal-doom/) package, which requires having two `gzdoom.ini` files. Alternatively [gzdoom-git](https://aur.archlinux.org/packages/gzdoom-git/) can be modified directly as shown below. However, if you want to be able to run both *gzdoom* and *brutal-doom* separately in order to play both versions, then you would need the *brutal-doom* package.

### Brutal Doom Mod

Acquire a registered IWAD (Internal WAD) file for [DOOM](https://zdoom.org/wiki/IWAD): `doom.wad`, `doom2.wad`, `doomu.wad`, `tnt.wad`, or `plutonia.wad`. `freedoom.WAD` from [freedoom2](https://aur.archlinux.org/packages/freedoom2/) is also compatible.

Download the *.zip* file containing the *.pk3* for the latest [Brutal Doom](http://www.moddb.com/mods/brutal-doom/downloads). As of January 2018 that is "Brutal Doom v21 Public Beta Jan 02 2018". You may need to install [unzip](https://www.archlinux.org/packages/?name=unzip).

Optionally you can acquire some [metal music](http://www.libregeek.org/Linux/game-files/brutal-doom/DoomMetalVol4.wad) for the gameplay.

Place all the *.wad* and *.pk3* files in a created folder such as `/usr/share/games/brutal-doom`.

### Configuration

Change `~/.config/gzdoom/gzdoom.ini` as follows (the `Search.Directories` mentioned are the only directories needed):

```
[IWADSearch.Directories]
Path=/usr/share/games/brutal-doom
...

[FileSearch.Directories]
Path=/usr/share/games/brutal-doom
Path=/usr/share/gzdoom
...

[Global.Autoload]
Path=/usr/share/games/brutal-doom/*modfile*.pk3
Path=/usr/share/games/brutal-doom/DoomMetalVol4.wad
...

vid_defheight=*<height in pixels>*
vid_defwidth=*<width in pixels>*
```

*modfile* is the downloaded *.pk3* file. *<height in pixels>* and *<width in pixels>* should be roughly the size of your screen resolution or preferred size.

The folder permissions for the created folder and files (all the files inside the `brutal-doom` directory):

```
drwxr-xr-x root root brutal-doom

```

```
-rw-r--r-- root root *<files in directory>*

```

To start the program:

```
$ gzdoom

```

## See Also

*   [Brutal Doom on Wikia](http://doom.wikia.com/wiki/Brutal_Doom)

*   [Brutal Doom on Doom Wiki](https://doomwiki.org/wiki/Brutal_Doom)

*   [IWAD files on ZDoom Wiki](https://zdoom.org/wiki/IWAD)