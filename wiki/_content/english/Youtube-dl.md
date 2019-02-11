Related articles

*   [mpv](/index.php/Mpv "Mpv")
*   [FFmpeg](/index.php/FFmpeg "FFmpeg")

[youtube-dl](https://youtube-dl.org/) is a command-line program that lets you easily download videos and audio from more than a thousand websites. See the [list of supported sites](https://github.com/rg3/youtube-dl/blob/master/docs/supportedsites.md).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Format selection](#Format_selection)
    *   [3.2 Extract audio](#Extract_audio)
    *   [3.3 Subtitles](#Subtitles)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Faster downloads](#Faster_downloads)
    *   [4.2 Trim (partial download)](#Trim_(partial_download))
    *   [4.3 URL from clipboard](#URL_from_clipboard)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [youtube-dl](https://www.archlinux.org/packages/?name=youtube-dl) package, or [youtube-dl-git](https://aur.archlinux.org/packages/youtube-dl-git/) for the development version. It is recommended to also install [FFmpeg](/index.php/FFmpeg "FFmpeg") as it is used for muxing for some sites. See the optional dependencies.

## Configuration

The system-wide configuration file is `/etc/youtube-dl.conf` and the user-specific configuration file is `~/.config/youtube-dl/config`. The syntax is simply one command-line option per line. Example configuration:

```
--ignore-errors
# --no-playlist

# Save in ~/Videos
-o ~/Videos/%(title)s.%(ext)s

# Prefer 1080p or lower resolutions
-f bestvideo[ext=mp4][height<1200]+bestaudio[ext=m4a]/bestvideo[ext=webm][height<1200]+bestaudio[ext=webm]/bestvideo[height<1200]+bestaudio/best[height<1200]/best

```

See [[1]](https://github.com/rg3/youtube-dl/blob/master/README.md#configuration) for more information.

## Usage

See [youtube-dl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/youtube-dl.1) for the manual.

```
$ youtube-dl [OPTIONS] *URL*

```

**Tip:** In some cases (like YouTube) *URL* can be substituted with the video ID.

### Format selection

In cases where multiple formats of a video are available, *youtube-dl* will download the best ones by default.

To select a specific one to download, first get a list of the available formats:

```
$ youtube-dl -F *URL*

```

Note the code of the format you want, then run:

```
$ youtube-dl -f *format* *URL*

```

### Extract audio

Use `-x` for audio-only downloads (requires [FFmpeg](/index.php/FFmpeg "FFmpeg")):

```
$ youtube-dl -x -f bestaudio *URL*

```

Depending on the available source streams, this will often correct the audio-only container. If an audio-only stream is not available, exclude `-f bestaudio` from the example above. This will download the video and copy its audio as post process. By default this will remove the downloaded video, include `-k` to keep it.

To also include album art (requires [atomicparsley](https://www.archlinux.org/packages/?name=atomicparsley)):

```
$ youtube-dl -x -f bestaudio[ext=m4a] --embed-thumbnail *URL*

```

### Subtitles

To see which languages are available:

```
$ youtube-dl --list-subs *URL*

```

To download a video with selected subtitles (comma separated):

```
$ youtube-dl --write-sub --sub-lang *LANG* *URL*

```

## Tips and tricks

### Faster downloads

Some websites throttle transfer speeds. You can often get around this by using [aria2](/index.php/Aria2 "Aria2"), an external downloader which supports multi-connection downloads. For example:

```
$ youtube-dl --external-downloader aria2c --external-downloader-args '-c -j 3 -x 3 -s 3 -k 1M' *URL*

```

### Trim (partial download)

Parts of videos can be downloaded by using the output of `youtube-dl -g -f *format* *URL*` as *ffmpeg* input with the `-ss`, `-t` and `-c copy` [options](http://ffmpeg.org/ffmpeg.html#Main-options).

### URL from clipboard

A shell [alias](/index.php/Alias "Alias"), a [desktop launcher](/index.php/Desktop_launcher "Desktop launcher") or a keyboard shortcut can be set to download a video (or audio) of a selected (or copied) URL by outputting it from the [X selection](https://en.wikipedia.org/wiki/X_Window_selection "wikipedia:X Window selection"). See [Clipboard#Tools](/index.php/Clipboard#Tools "Clipboard").

## See also

*   [GitHub repository](https://github.com/rg3/youtube-dl) for documentation.