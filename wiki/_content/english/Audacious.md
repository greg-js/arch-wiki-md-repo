[Audacious](http://audacious-media-player.org/) is a free and advanced audio player based on GTK+. It's focused on audio quality and supports a wide variety of audio codecs, and is easily extensible through third-party plugins.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Interfaces](#Interfaces)
        *   [2.1.1 GTK+](#GTK+)
        *   [2.1.2 Qt5](#Qt5)
        *   [2.1.3 Winamp](#Winamp)
    *   [2.2 Plugins](#Plugins)
        *   [2.2.1 AMIDI-Plug (MIDI Player)](#AMIDI-Plug_(MIDI_Player))
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Audtool](#Audtool)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Audacious starts instead of file manager](#Audacious_starts_instead_of_file_manager)
    *   [4.2 MP3 problems](#MP3_problems)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [audacious](https://www.archlinux.org/packages/?name=audacious) package. For audio CD support, install [libcdio](https://www.archlinux.org/packages/?name=libcdio).

**Note:** Some plugins may fail to load unless all optional dependencies of the [audacious-plugins](https://www.archlinux.org/packages/?name=audacious-plugins) package are satisfied.

## Configuration

### Interfaces

Audacious currently provides three interfaces:

#### GTK+

GTK+ 2 is the default interface in Audacious 2.4 and above.

#### Qt5

For the Qt5 interface install the [audacious-qt5](https://aur.archlinux.org/packages/audacious-qt5/) package and [audacious-plugins-qt5](https://aur.archlinux.org/packages/audacious-plugins-qt5/). To support both Qt5 and GTK+ and switch between interfaces, remove `--disable-gtk` from the [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") of both packages.

#### Winamp

To add classic Winamp skins to Audacious, just copy them to either `~/.local/share/audacious/Skins/` (user only) or `/usr/share/audacious/Skins/` (system wide), then select them from the *Skinned Interface* tab in *Preferences*. Alternatively drag the skin file directly into the list view of available skins.

### Plugins

#### AMIDI-Plug (MIDI Player)

To play MIDI and RMI files, it is required to install the [fluidsynth](https://www.archlinux.org/packages/?name=fluidsynth) package, and also install the sound font files, both [timidity-freepats](https://www.archlinux.org/packages/?name=timidity-freepats) and [soundfont-fluid](https://www.archlinux.org/packages/?name=soundfont-fluid). No further configuration is required on the fluidsynth package, but for additional functionality check the [FluidSynth](/index.php/FluidSynth "FluidSynth") instructions.

Afterwards, the plugin will be enabled, and in the plugin configuration panel (File, Settings ..., Plugins pane, Input tab, select AMIDI-Plug (MIDI Player)) add the installed sound font files one at a time (Extension `.sf2`) to the SoundFont dialog, they are located at `/usr/share/soundfonts/`.

## Tips and tricks

### Audtool

Audacious is shipped with a powerful management tool called Audtool which could be used to retrieve information or to control the player.

For example, to retrieve the current song's title or artist, issue the following commands:

```
$ audtool current-song
$ audtool current-song-tuple-data artist

```

There are also functions to control playback, manipulate the playlist, equalizer and main window. See `audtool --help` for the whole list of options.

## Troubleshooting

### Audacious starts instead of file manager

See [File manager functionality#Directories are not opened in the file manager](/index.php/File_manager_functionality#Directories_are_not_opened_in_the_file_manager "File manager functionality").

### MP3 problems

Install [mpg123](https://www.archlinux.org/packages/?name=mpg123).

## See also

*   [Audacious official site](http://audacious-media-player.org/)