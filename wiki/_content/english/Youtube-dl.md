Related articles

*   [mpv](/index.php/Mpv "Mpv")
*   [FFmpeg](/index.php/FFmpeg "FFmpeg")

[youtube-dl](https://youtube-dl.org/) is a command-line program that lets you easily download videos and audio from more than a thousand websites. See the [list of supported sites](https://github.com/rg3/youtube-dl/blob/master/docs/supportedsites.md).

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Format selection](#Format_selection)
    *   [2.2 Extract audio](#Extract_audio)
*   [3 Configuration](#Configuration)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Faster downloads](#Faster_downloads)
    *   [4.2 Trim (partial download)](#Trim_.28partial_download.29)
    *   [4.3 URL from clipboard](#URL_from_clipboard)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [youtube-dl](https://www.archlinux.org/packages/?name=youtube-dl) package, or [youtube-dl-git](https://aur.archlinux.org/packages/youtube-dl-git/) for the development version. It is recommended to also install [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) as it is used for muxing for some sites.

## Usage

See [youtube-dl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/youtube-dl.1).

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

Use `-x` for audio-only downloads (requires [FFmpeg](/index.php/FFmpeg "FFmpeg")).

```
$ youtube-dl -x -f bestaudio *URL*

```

## Configuration

The system-wide configuration file is `/etc/youtube-dl.conf` and the user-specific configuration file is `~/.config/youtube-dl/config`. The syntax is simply one command-line option per line. Example configuration:

 `~/.config/youtube-dl/config` 
```
# Save in ~/Videos
-o ~/Videos/%(title)s.%(ext)s

# Prefer 1080p or lower resolutions
-f (bestvideo[height<=1080]/bestvideo)+bestaudio/best[height<=1080]/best
```

See [[1]](https://github.com/rg3/youtube-dl/blob/master/README.md#configuration) for more information.

## Tips and tricks

### Faster downloads

Some websites throttle transfer speeds. You can often get around this by using [Aria2](/index.php/Aria2 "Aria2"), an external downloader which supports multi-connection downloads. For example:

```
$ youtube-dl --external-downloader aria2c --external-downloader-args '-c -j 3 -x 3 -s 3 -k 1M' *URL*

```

### Trim (partial download)

Parts of videos can be downloaded by using the output of `youtube-dl -g -f *format* *URL*` as *ffmpeg* input with the `-ss`, `-t` and `-c copy` [options](http://ffmpeg.org/ffmpeg.html#Main-options).

### URL from clipboard

A shell alias or a keyboard shortcut can be set to download a video (or audio) of a selected (or copied) URL by outputting it from the [X selection](https://en.wikipedia.org/wiki/X_Window_selection "wikipedia:X Window selection"). See [Clipboard#Tools](/index.php/Clipboard#Tools "Clipboard").

## See also

*   [GitHub repository](https://github.com/rg3/youtube-dl) for documentation.