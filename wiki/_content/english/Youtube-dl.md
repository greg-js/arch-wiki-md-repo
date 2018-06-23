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
    *   [4.1 Increasing download speeds](#Increasing_download_speeds)
    *   [4.2 Trim](#Trim)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [youtube-dl](https://www.archlinux.org/packages/?name=youtube-dl) package, or [youtube-dl-git](https://aur.archlinux.org/packages/youtube-dl-git/) for the development version.

## Usage

See the [youtube-dl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/youtube-dl.1) [man page](/index.php/Man_page "Man page").

```
$ youtube-dl [OPTIONS] *URL*

```

### Format selection

In cases where multiple formats of a video are available, youtube-dl will default to downloading the best possible version. If you'd like to choose a specific format to download, first get a list of the available formats:

```
$ youtube-dl -F *URL*

```

Note the format code for the version you want, and then run:

```
$ youtube-dl -f *format* *URL*

```

You can often download audio-only or video-only formats this way. If you have [FFmpeg](/index.php/FFmpeg "FFmpeg"), you can download both a video-only and audio-only format and mux them together into a single file:

```
$ youtube-dl -f *video_format*+*audio_format* *URL*

```

### Extract audio

Use `-x` for audio-only downloads (requires [FFmpeg](/index.php/FFmpeg "FFmpeg")).

```
$ youtube-dl -x -f bestaudio *URL*

```

## Configuration

The system-wide configuration file is `/etc/youtube-dl.conf` and the user-specific configuration file is `~/.config/youtube-dl/config`

The syntax is simply one command-line option per line. See the [youtube-dl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/youtube-dl.1) [man page](/index.php/Man_page "Man page") for supported options. Example configuration:

 `~/.config/youtube-dl/config` 
```
# Save in ~/Videos
-o ~/Videos/%(title)s.%(ext)s

# Prefer 1080p or lower resolutions
-f (bestvideo[height<=1080]/bestvideo)+bestaudio/best[height<=1080]/best
```

## Tips and tricks

### Increasing download speeds

Some websites throttle download speeds. You can often increase speeds by using [Aria2](/index.php/Aria2 "Aria2"), an external downloader which supports multi-connection downloads. Example:

```
$ youtube-dl --external-downloader aria2c --external-downloader-args '-c -x 5 -k 2M' *URL*

```

### Trim

Parts of [DASH](https://en.wikipedia.org/wiki/Dynamic_Adaptive_Streaming_over_HTTP "wikipedia:Dynamic Adaptive Streaming over HTTP") videos can be downloaded by using the output of `youtube-dl -g -f *format* *URL*` as *ffmpeg* input with the `-ss`, `-t` and `-c copy` [options](http://ffmpeg.org/ffmpeg.html#Main-options).

## See also

*   [GitHub repository](https://github.com/rg3/youtube-dl) for documentation.