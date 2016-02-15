This article describes how to play .rmvb video files.

## Installation

The most simple way is to install [VLC](/index.php/VLC "VLC"), which plays .rmvb now, as well as many other video format.

```
# pacman -S vlc

```

Or you can install [realplayer](https://aur.archlinux.org/packages/realplayer/) from the [AUR](/index.php/AUR "AUR").

Next, start it with:

```
$ realplay &

```

On the first run, a configuration wizard will set up the necessary options.

## .ram files

To play .ram files, this script is intended to replace the use of realplayer by using vlc instead : [http://www.sputnick-area.net/scripts/realplay.bash](http://www.sputnick-area.net/scripts/realplay.bash)

See comments inside.

## Conversion of RealMedia Files

As RealMedia files are not widely (nor well) supported, it may be useful to convert them to another format. [FFmpeg](http://ffmpeg.org/) can be used for this.

```
# pacman -S ffmpeg

```

For example, to convert the video **foo.rm** to an mp4 file:

```
ffmpeg -i foo.rm -vcodec mpeg4 -sameq -acodec libfaac -ab 94208 foo.mp4

```