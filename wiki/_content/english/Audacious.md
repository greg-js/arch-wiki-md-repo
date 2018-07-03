[Audacious](http://audacious-media-player.org/) is a free and advanced audio player based on GTK+. It's focused on audio quality and supports a wide variety of audio codecs, and is easily extensible through third-party plugins.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Interfaces](#Interfaces)
        *   [2.1.1 Adding Winamp skins](#Adding_Winamp_skins)
    *   [2.2 Plugin configuration](#Plugin_configuration)
        *   [2.2.1 AMIDI-Plug (MIDI Player)](#AMIDI-Plug_.28MIDI_Player.29)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Audtool](#Audtool)
    *   [3.2 MP3 problems](#MP3_problems)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Audacious sets itself as the default file manager](#Audacious_sets_itself_as_the_default_file_manager)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [audacious](https://www.archlinux.org/packages/?name=audacious) package. If you want audio CD support, install [libcdio](https://www.archlinux.org/packages/?name=libcdio).

**Note:** Some plugins may fail to load unless all optional dependencies of the [audacious-plugins](https://www.archlinux.org/packages/?name=audacious-plugins) package are satisfied.

## Configuration

### Interfaces

**Note:** GTK+ is now the default interface in Audacious 2.4 and above.

Audacious currently provides three interfaces:

*   Winamp classic interface
*   GTK+ interface
*   Qt5 interface.

For Qt5 interface, install [audacious-qt5](https://aur.archlinux.org/packages/audacious-qt5/) since package from official repository doesn't have Qt5 enabled by default. However, package from AUR doesn't support GTK+. If you want support for both Qt5 and GTK+, you should remove `--disable-gtk` option in [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") of both audacious-qt5 and [audacious-plugins-qt5](https://aur.archlinux.org/packages/audacious-plugins-qt5/). One may switch between interfaces in Audacious settings.

#### Adding Winamp skins

Adding Winamp skins to Audacious is very simple. Just copy your skin file (.zip, .wsz, .tgz, .tar.gz, or .tar.bz2 file) to either `~/.local/share/audacious/Skins` (affect your user only) or `/usr/share/audacious/Skins` (affects every user), and then you can browse and select it from *Skinned Interface* tab in *Preferences*. Another way is dragging the skin file directly into the list view of available skins.

### Plugin configuration

#### AMIDI-Plug (MIDI Player)

To play MIDI and RMI files, it is required to install the [fluidsynth](https://www.archlinux.org/packages/?name=fluidsynth) package, and also install the sound font files, both [timidity-freepats](https://www.archlinux.org/packages/?name=timidity-freepats) and [soundfont-fluid](https://www.archlinux.org/packages/?name=soundfont-fluid). No further configuration is required on the fluidsynth package, but for additional functionality check the [FluidSynth](/index.php/FluidSynth "FluidSynth") instructions.

Afterwards, the plugin will be enabled, and in the plugin configuration panel (File, Settings ..., Plugins pane, Input tab, select AMIDI-Plug (MIDI Player)) add the installed sound font files one at a time (Extension `.sf2`) to the SoundFont dialog, they are located at `/usr/share/soundfonts/`.

## Tips and tricks

### Audtool

Audacious is shipped with a powerful management tool called Audtool. Audtool could be used to retrieve information or to control the player.

For example, to retrieve current song title or artist, issue the following command:

```
$ audtool current-song
$ audtool current-song-tuple-data artist

```

There are also functions to control playback, manipulate the playlist, equalizer and main window. For the whole option list, see:

```
$ audtool --help

```

### MP3 problems

Install [mpg123](https://www.archlinux.org/packages/?name=mpg123).

## Troubleshooting

### Audacious sets itself as the default file manager

See [File manager functionality#Directories are not opened in the file manager](/index.php/File_manager_functionality#Directories_are_not_opened_in_the_file_manager "File manager functionality").

## See also

*   [Audacious official site](http://audacious-media-player.org/)