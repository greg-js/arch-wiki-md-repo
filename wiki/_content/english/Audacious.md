**Audacious** is a free and advanced audio player based on GTK+. It's focused on audio quality and supports a wide variety of audio codecs, and is easily extensible through third-party plugins.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Interfaces](#Interfaces)
        *   [2.1.1 Adding Winamp skins](#Adding_Winamp_skins)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Audtool](#Audtool)
    *   [3.2 MP3 problems](#MP3_problems)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Audacious sets itself as the default file manager](#Audacious_sets_itself_as_the_default_file_manager)
*   [5 See also](#See_also)

## Installation

[audacious](https://www.archlinux.org/packages/?name=audacious) is available from [official repositories](/index.php/Official_repositories "Official repositories"). Install it with [pacman](/index.php/Pacman "Pacman"). If you want audio CD support, install [libcdio](https://www.archlinux.org/packages/?name=libcdio).

## Configuration

### Interfaces

**Note:** GTK+ is now the default interface in Audacious 2.4 and above.

Audacious currently provides two interfaces:

*   Winamp classic interface
*   GTK+ interface.

One may switch between two interfaces in Audacious.

#### Adding Winamp skins

Adding Winamp skins to Audacious is very simple. Just copy your skin file (.zip, .wsz, .tgz, .tar.gz, or .tar.bz2 file) to either `~/.local/share/audacious/Skins` (affect your user only) or `/usr/share/audacious/Skins` (affects every user), and then you can browse and select it from *Skinned Interface* tab in *Preferences*. Another way is dragging the skin file directly into the list view of available skins.

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