OpenTTD is a free re-implementation of the popular DOS game [Transport Tycoon Deluxe](https://en.wikipedia.org/wiki/Transport_Tycoon_Deluxe "wikipedia:Transport Tycoon Deluxe"). You are a transport company owner, and you must manage it over the years in order to make profit.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Original Transport Tycoon Deluxe data (optional)](#Original_Transport_Tycoon_Deluxe_data_(optional))
*   [2 Tutorial](#Tutorial)
*   [3 Configuration](#Configuration)
    *   [3.1 Game Options](#Game_Options)
    *   [3.2 Difficulty](#Difficulty)
    *   [3.3 Advanced Settings](#Advanced_Settings)
    *   [3.4 AI/Game Script Settings](#AI/Game_Script_Settings)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Heightmaps](#Heightmaps)
    *   [4.2 Cheats](#Cheats)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Music is not playing](#Music_is_not_playing)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [openttd](https://www.archlinux.org/packages/?name=openttd) package.

If you do not own the original game, [openttd-opengfx](https://www.archlinux.org/packages/?name=openttd-opengfx) and [openttd-opensfx](https://www.archlinux.org/packages/?name=openttd-opensfx) contains the free graphics & sounds.

The free music pack, [OpenMSX](https://wiki.openttd.org/OpenMSX), can be downloaded from [the online content downloader provided with the game](https://wiki.openttd.org/Online_content).

### Original Transport Tycoon Deluxe data (optional)

OpenTTD can use the non-free graphics and sound data of the original Windows/DOS version of Transport Tycoon Deluxe.

**Note:** While you can dump the files from either the DOS or the Windows version of the game, only the Windows version provides the original music.

You can get these files from the game CD-ROM, from an existing install or you get them from the freely available game installation archive available at [Abandonia](http://www.abandonia.com/en/games/240).

To use the original graphics & sound effects, copy the following files to `/usr/share/openttd/data/` or `~/.openttd/baseset` :

*   Windows : trg1r.grf, trgcr.grf, trghr.grf, trgir.grf, trgtr.grf
*   DOS : TRG1.GRF, TRGC.GRF, TRGH.GRF, TRGI.GRF, TRGT.GRF
*   sample.cat from either version

For the original soundtrack, copy the files from the gm folder of the original TTD game directory to `~/.openttd/gm`.

## Tutorial

The game can be quite confusing at first. A good tutorial is available on the wiki [here](http://wiki.openttd.org/Tutorial).

For an in-game tutorial, a game script has been implemented. Just download 'Beginner Tutorial' with the in-game download manager and load the 'Beginner Tutorial' scenario.

## Configuration

The OpenTTD main configuration file is located at `~/.openttd/openttd.cfg` and is automatically created upon first startup.

Various settings in the configuration file can be edited with buttons on the main menu. Each button is explained below.

### Game Options

This window allows you to set options which will be used by default at the start of a new game.

**Note:** Settings will not be updated for games which have already been started. The options can still be changed in-game.

You can also set the default graphics, sound, and music here.

### Difficulty

This window allows you to change the difficulty of the game, and specific options about them. You can either use the difficulty presets by selecting the difficulty buttons at the top of the window, or set custom options.

More information can be found [here](http://wiki.openttd.org/Difficulty).

### Advanced Settings

In this window, nearly all the other settings in the configuration file can be modified. All the options are grouped in expandable sections. You can also search for the setting to be changed using the search utility.

Details about these settings can be found [here](http://wiki.openttd.org/Advanced_Settings).

### AI/Game Script Settings

This window allows you to customize various options relating to artificial intelligence (bots or CPU players) and Game Scripts.

Game Scripts are a goal-based scripts which can perform many in-game actions to enhance or extend the game.

Detailed information about this window can be found [here](http://wiki.openttd.org/AI_settings).

## Tips and tricks

### Heightmaps

OpenTTD allows using a grayscale image as a [heightmap](https://wiki.openttd.org/Heightmap) for landscape generation. There's an excellent heightmap generator available at [terrain.party](http://terrain.party/), based on real Earth terrain. You may further use [gimp](https://www.archlinux.org/packages/?name=gimp) for fine-tuning the heightmap, especially useful are the Levels and Gaussian Blur tools.

### Cheats

A cheat menu can be shown in a local game by pressing Ctrl-Alt-C.

Detailed information about cheats are available [here](https://secure.openttd.org/wiki/Cheats).

## Troubleshooting

### Music is not playing

The soundtrack of the game is made of [MIDI](/index.php/MIDI "MIDI") files. Therefore, you need a [MIDI synthesizer](/index.php/MIDI#Software "MIDI") to play them.

The game will automatically try to use [TiMidity++](/index.php/Timidity "Timidity") with no additional arguments. If for some reason you need/want to use another synthesizer, OpenTTD provides the "extmidi" music driver, which allows you to configure a command to be ran to play music.

**Warning:** When using the extmidi driver, the in-game volume control sliders are disabled and cannot be used to change the volume.

**Warning:** If the command you want to run is not included in `$PATH`, you must specify the absolute path.

Edit your openttd.cfg to configure extmidi :

 `~/.openttd/openttd.cfg` 
```
[misc]
musicdriver = "extmidi:cmd=<command>"
```

**Note:** You can also configure extmidi when starting up the game : `openttd -m extmidi:cmd=<command>`

However, extmidi does not allow additionnal arguments in the command. The solution is to use a wrapper script (for example, `~/.openttd/playmidi`) :

```
#!/bin/bash

#here, we want to use the [FluidSynth](/index.php/FluidSynth "FluidSynth") synthesizer with the soundfont
#provided in [soundfont-fluid](https://www.archlinux.org/packages/?name=soundfont-fluid) and [PulseAudio](/index.php/PulseAudio "PulseAudio")

trap "pkill fluidsynth" EXIT
fluidsynth -a pulseaudio -i /usr/share/soundfonts/FluidR3_GM2-2.sf2 $*

```

Mark it as executable :

```
$ chmod 755 ~/.openttd/playmidi

```

Then you can specify the full path to the script as the command to be used with extmidi :

 `~/.openttd/openttd.cfg` 
```
[misc]
musicdriver = "extmidi:cmd=/home/<user>/openttd/playmidi"
```

## See also

*   [OpenTTD](http://www.openttd.org)
*   [OpenTTD Wiki](http://wiki.openttd.org/Main_Page)