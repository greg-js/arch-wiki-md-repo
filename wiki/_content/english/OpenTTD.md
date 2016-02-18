OpenTTD is a tile-based transportation management game based on [Transport Tycoon Deluxe](https://en.wikipedia.org/wiki/Transport_Tycoon_Deluxe "wikipedia:Transport Tycoon Deluxe"). The game is in the community repository.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Original Transport Tycoon Deluxe data (optional)](#Original_Transport_Tycoon_Deluxe_data_.28optional.29)
        *   [1.1.1 Where to get the data](#Where_to_get_the_data)
        *   [1.1.2 Graphics and sound effects](#Graphics_and_sound_effects)
        *   [1.1.3 Music](#Music)
*   [2 Tutorial](#Tutorial)
*   [3 Configuration](#Configuration)
    *   [3.1 Game Options](#Game_Options)
    *   [3.2 Difficulty](#Difficulty)
    *   [3.3 Advanced Settings](#Advanced_Settings)
    *   [3.4 AI/Game Script Settings](#AI.2FGame_Script_Settings)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Heightmaps](#Heightmaps)
    *   [4.2 Cheats](#Cheats)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [openttd](https://www.archlinux.org/packages/?name=openttd) package.

The [openttd-opengfx](https://www.archlinux.org/packages/?name=openttd-opengfx) package provides a free replacement of the base graphics.

The [openttd-opensfx](https://www.archlinux.org/packages/?name=openttd-opensfx) package provides a free replacement of the base sound.

### Original Transport Tycoon Deluxe data (optional)

OpenTTD can utilize the non-free graphics and sound data of the original Windows/DOS version of Transport Tycoon Deluxe.

#### Where to get the data

If you wish to play OpenTTD with the non-free TTD base graphics and sounds, you will need several files from either the Windows/DOS version of Transport Tycoon Deluxe.

You can get these files from the game CD-ROM, from an existing install or you get them from the freely available game installation archive available at [Abandonia](http://www.abandonia.com/en/games/240).

#### Graphics and sound effects

Copy the following files to /usr/share/openttd/data/

*   trg1r.grf or TRG1.GRF
*   trgcr.grf or TRGC.GRF
*   trghr.grf or TRGH.GRF
*   trgir.grf or TRGI.GRF
*   trgtr.grf or TRGT.GRF
*   sample.cat

#### Music

The free music set [OpenMSX](http://dev.openttdcoop.org/projects/openmsx) can be installed directly from the in-game download manager.

If you wish to listen to the original music (Windows version only), Copy the files from the gm folder of the original TTD game directory to: `~/.openttd/gm`

If your sound driver does not support MIDI natively, you will need to install [timidity](/index.php/Timidity "Timidity") (configuring a sound sample is enough). timidity might not work in some environments, e.g. with [PulseAudio](/index.php/PulseAudio "PulseAudio"); the alternative is to use [FluidSynth](/index.php/FluidSynth "FluidSynth") as follows.

Install the [fluidsynth](https://www.archlinux.org/packages/?name=fluidsynth) and [soundfont-fluid](https://www.archlinux.org/packages/?name=soundfont-fluid) packages.

Create a fluidsynth wrapper script in e.g. `~/.openttd/playmidi`:

```
#!/bin/bash

trap "pkill fluidsynth" EXIT
fluidsynth -a pulseaudio -i /usr/share/soundfonts/FluidR3_GM2-2.sf2 $*

```

Do not forget to allow the script to execute:

```
$ chmod 755 ~/.openttd/playmidi

```

Run *openttd*, passing the wrapper script filename as an argument to the *extmidi* driver:

```
 $ PATH=$HOME/.openttd:$PATH openttd -m extmidi:cmd=playmidi

```

## Tutorial

The game can be quite confusing at first. A good tutorial is available on the wiki [here](http://wiki.openttd.org/Tutorial).

For an in-game tutorial, a game script has been implemented. Just download 'Beginner Tutorial' with the in-game download manager and load the 'Beginner Tutorial' scenario.

## Configuration

The OpenTTD main configuration file is located at ~/.openttd/openttd.cfg and is automatically created upon first startup.

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

## See also

*   [OpenTTD](http://www.openttd.org)
*   [OpenTTD Wiki](http://wiki.openttd.org/Main_Page)