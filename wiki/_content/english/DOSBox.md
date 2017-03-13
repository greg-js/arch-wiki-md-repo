[DOSBox](http://www.dosbox.com/) is an x86 PC DOS-emulator for running old DOS games or programs.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
*   [4 Tips](#Tips)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [dosbox](https://www.archlinux.org/packages/?name=dosbox) package.

## Configuration

No initial configuration is needed, however the official DOSBox manual refers to a configuration file named `dosbox.conf`. By default that file exists in your `~/.dosbox` folder.

You can also make a new configuration file on a per-application basis by copying `dosbox.conf` from `~/.dosbox` to the directory where your DOS app resides and modifying the settings accordingly. You can also create a a config file automatically: simply run `dosbox` without any parameters inside your desired application's folder:

```
$ dosbox

```

Then at the DOS prompt, type:

```
Z:\> config -wc dosbox.conf

```

The configuration file `dosbox.conf` will then be saved in the current directory. Go in a change whatever settings you need.

The configuration options are described in the official DosBox wiki: [http://www.dosbox.com/wiki/Dosbox.conf](http://www.dosbox.com/wiki/Dosbox.conf).

## Usage

A simple way to run DOSBox is to place your DOS game (or its setup files) into a directory and then run dosbox with the directory path appended. For example:

```
$ dosbox ./game-folder/

```

You should now have a DOS prompt whose working directory is the one specified above. From there, you can execute the desired programs:

```
C:\> SETUP.EXE

```

## Tips

If DOSBox traps your focus, use `Ctrl+F10` to free it.

To play music, some DOS games require a [MIDI](/index.php/MIDI "MIDI") synthesizer which DOSBox does not emulate. However DOSBox can use one if one is available. A software synthesizer such as [FluidSynth](/index.php/FluidSynth "FluidSynth") or [Timidity](/index.php/Timidity "Timidity") can be used if your computer does not have a hardware synthesizer.

## See also

*   [http://www.dosbox.com/](http://www.dosbox.com/) - The official DOSBox site.
*   [http://www.abandonia.com/](http://www.abandonia.com/) - Abandonia: large repository of old and abandoned DOS games.
*   [http://www.dosgames.com/](http://www.dosgames.com/) - DosGames.com: large repository of DOS games.