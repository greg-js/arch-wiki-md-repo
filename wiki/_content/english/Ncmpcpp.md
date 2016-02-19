[Ncmpcpp](http://unkart.ovh.org/ncmpcpp/) or ncmpcpp is an [mpd](/index.php/Mpd "Mpd") client (compatible with *mopidy*) with a UI very similar to *ncmpc*, but it provides new useful features such as support for regular expressions for library searches, extended song format, items filtering, the ability to sort playlists, and a local filesystem browser.

To use it, a functional *mpd* must be present on the system since *ncmpcpp*/*mpd* work together in a client/server relationship.

## Contents

*   [1 Installation](#Installation)
*   [2 Basic configuration](#Basic_configuration)
*   [3 Enabling visualization](#Enabling_visualization)
*   [4 Basic usage](#Basic_usage)
    *   [4.1 Loading ncmpcpp](#Loading_ncmpcpp)
    *   [4.2 Different views](#Different_views)
    *   [4.3 Other UI keys](#Other_UI_keys)
    *   [4.4 Playback modes](#Playback_modes)
*   [5 Remapping keys](#Remapping_keys)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [ncmpcpp](https://www.archlinux.org/packages/?name=ncmpcpp) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Basic configuration

The shell "GUI" for *ncmpcpp* is highly customizable. Edit `~/.ncmpcpp/config` to your liking. If, after installation, `~/.ncmpcpp/config` has not been created, simply copy the sample config, [change owner](/index.php/Chmod#chown "Chmod") and edit at the very least the following three configuration options:

*   **mpd_host** - Should point to the host on which *mpd* resides, can be "localhost" or "127.0.0.1" if on the same machine
*   **mpd_port** - The default of *mpd* should be "6600"
*   **mpd_music_dir** - The same directory value as specified in "music_directory" in `mpd.conf`

For inspiration, see the following resources:

*   Sample configuration file in `/usr/share/doc/ncmpcpp/config`.
*   [Show your .ncmpcpp/config with screenshot forum thread](https://bbs.archlinux.org/viewtopic.php?id=66488)
*   [Project screenshots page](http://unkart.ovh.org/ncmpcpp/screenshots.php)

## Enabling visualization

For visualization, add a few lines to `/etc/mpd.conf` to enable the generation of the [fast Fourier transform](https://en.wikipedia.org/wiki/Fast_Fourier_transform "wikipedia:Fast Fourier transform") data for the visualization:

```
audio_output {
    type                    "fifo"
    name                    "my_fifo"
    path                    "/tmp/mpd.fifo"
    format                  "44100:16:2"
}

```

Additional lines need to be added to `~/.ncmpcpp/config`

```
visualizer_fifo_path = "/tmp/mpd.fifo"
visualizer_output_name = "my_fifo"
visualizer_sync_interval = "30" 
visualizer_in_stereo = "yes"
#visualizer_type = "wave" (spectrum/wave)
visualizer_type = "spectrum" (spectrum/wave)
visualizer_look = "+|"

```

*   **visualizer_sync_interval** - Set the interval for synchronizing the visualizer with the audio output from *mpd*. It should be set to greater than 10 to avoid trying to synchronize too frequently, which freezes the visualization. The recommended value is 30, but it can be reduced if the audio becomes desynced with the visualization.
*   **visualizer_type** - Set the visualization to either a spectrum analyzer or wave form.
*   **visualizer_look** - Set the visualizer's look (string has to be exactly 2 characters long: first one is for wave whereas second for frequency spectrum).

## Basic usage

### Loading ncmpcpp

Load ncmpcpp in a shell:

```
$ ncmpcpp

```

### Different views

Partial list of views within ncmpcpp:

*   `1` - Current playlist
*   `2` - Filesystem browser
*   `3` - DB search
*   `4` - Library
*   `5` - Playlist editor
*   `6` - Tag editor (very powerful!)
*   `7` - Output selector
*   `8` - Music visualizer
*   `=` - Clock
*   `F1` - Help

### Other UI keys

*   `q` - Quit
*   `f` - Seek forward
*   `b` - Seek backward
*   `\` - Switch between classic and alternative views
*   `#` - Display bitrate of file
*   `i` - Show song info
*   `I` - Show artist info (saved in `~/.ncmpcpp/artists/ARTIST.txt`)
*   `L` - Shuffle between available lyric databases
*   `l` - Retrieve song lyrics for current song Show/hide lyrics
*   `>` - Next track
*   `<` - Previous track

### Playback modes

Noticed the control panel in the upper right; shown in alternative mode:

```
1:40/4:16 1082 kbps                            ──┤ Criminal ├──                                       Vol: 98%
[playing]                             Disturbed - Indestructible (2008)                               **[-z-c--]**

```

And again in classic mode:

```
─────────────────────────────────────────────────────────────────────────────────────────────────────────**[zc]**─

```

This corresponds to the playback modes; ordered from left to right, they are:

*   `r` - repeat mode **[r-----]**
*   `z` - random mode **[-z----]**
*   `y` - single mode **[--s---]**
*   `R` - consume mode **[---c--]**
*   `x` - crossfade mode **[----x-]**

The final "-" is only active when the user forces an update to the datebase via `u`.

## Remapping keys

A listing of key bindings and their respective functions is available from within npmpcpp itself via hitting `F1`. Users may remap any of the default keys simply by copying `/usr/share/doc/ncmpcpp/bindings` to `~/.ncmpcpp/` and editing it.

## See also

[dotshare.it configurations](http://dotshare.it/category/mpd/ncmpcpp/)