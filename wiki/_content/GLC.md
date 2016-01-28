# GLC

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

GLC is an ALSA & OpenGL capture tool for Linux. It consists of a generic video capture, playback and processing library and a set of tools built around that library. GLC should be able to capture any application that uses ALSA for sound and OpenGL for drawing. It is similar to Fraps on Windows.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Playback](#Playback)
*   [4 Encoding](#Encoding)
*   [5 Mixing audio streams](#Mixing_audio_streams)
*   [6 Interfaces](#Interfaces)
*   [7 See also](#See_also)

## Installation

To install GLC, simply install the [glc](https://aur.archlinux.org/packages/glc/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/glc)]</sup> package from AUR.

If you want to record 32 bit programs such as Wine on a 64 bit system, you will also need to install [lib32-glc](https://aur.archlinux.org/packages/lib32-glc/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/lib32-glc)]</sup>.

NOTE: GLC will only work with ALSA. If you use Pulseaudio, install the [glc-pulseaudio*](https://aur.archlinux.org/packages.php?O=0&K=glc-pulseaudio&do_Search=Pesquisar) packages instead. If you use OSS, you will probably need to record the audio separately.

## Usage

The basic usage is simple. By default, GLC will save a (large) .glc file in the current directory. You can then play or encode it. Just run this:

```
glc-capture [application]

```

Press **Shift + F8** to start and stop recording. Otherwise you can use:

```
glc-capture -s [application]

```

To start recording immediately. For complete list of available options see:

```
glc-capture --help

```

If you want to record from two different audio devices, usually the application and the microphone, you need to use the **-a** option. For example:

```
glc-capture -a 'hw:0,48000,1;hw:1,48000,1' [application]

```

The **-a** format is _device,rate,channels;device2..._; you probably want to mix the two audio streams togheter after, so to make it easier keep both sample rate at the same value.

## Playback

To play a captured stream directly, execute

```
glc-play [stream file]

```

**ESC** stops playback, **f** toggles fullscreen and Right seeks forward.

## Encoding

In order to use the videos outside of glc-play, you will need to encode it. Here are a few example that work well for encoding. Of course, you can be creative and use any of the formats supported by ffmpeg to get your desired result (mencoder works too, I'm just not familiar with it).

For either script, run with the following context (assuming it's saved as glc-encode.sh):

```
glc-encode.sh filename.glc

```

**H.264 Ultrafast + FLAC Audio**: (fairly quick encoding, high quality, good filesize) This script requires the following packages: ffmpeg

```
#!/bin/bash
glc-play $1 -a 1 -o glc.wav
glc-play $1 -o - -y 1 | ffmpeg -i - -preset ultrafast -i glc.wav -acodec flac -vcodec libx264 output.mkv
rm glc.wav

```

It will output as output.mkv

**Lossless** (usually quickest, no quality loss, _huge_ files, need plenty of HD space): This script requires the following packages: ffmpeg

```
#!/bin/bash
glc-play $1 -a 1 -o glc.wav
glc-play $1 -y 1 -o glc.yuv
ffmpeg -i glc.wav -i glc.yuv -acodec copy -vcodec copy output.mkv
rm glc.yuv
rm glc.wav

```

It will output as output.mkv

**WebM**: This script requires the following packages: vorbis-tools, ffmpeg, and mkvtoolnix

```
#!/bin/bash
glc-play $1 -a 1 -o - | oggenc - -b 128k -o glc.ogg
glc-play $1 -o - -y 1 | ffmpeg -i - -vcodec libvpx glc.webm
mkvmerge -o output.webm glc.webm glc.ogg
rm glc.ogg
rm glc.webm

```

It will output as output.webm

Note: Sometimes when recording WINE, the audio stream you want won't be #1, so you'll have to find out which one it is and experiment, and edit the encoding script accordingly. You can get some info on the streams using **glc-play -i 1 filename.glc**

## Mixing audio streams

Using **glc-play -i 1 filename.glc** you get the list of audio tracks, extract them with the command from the previous section and you get **.wav** files with the audio tracks.

Depending on how the application started the Alsa driver, it is possible there are silent tracks, so listen them and delete the unneeded ones. Once done you can mix using **sox** (from the package of the same name) using this command:

```
sox -m -v 0.3 gamesound.wav -v 0.7 voice.wav finalaudio.wav

```

The **-m** option asks the mix, instead **-v** options change the volume of the audio file, try to keep the sum of both to 1.

Once you get a single **.wav** file with audio as you want, encode and mux normally.

## Interfaces

Two graphical interfaces are available for glc to try and simplify it's usage, with both of them being avalible from the [AUR](/index.php/AUR "AUR").

*   [soulcapture](https://aur.archlinux.org/packages/soulcapture/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/soulcapture)]</sup> is a graphical front-end made in [Gambas](/index.php/Gambas "Gambas") that utilizes [FFmpeg](/index.php/FFmpeg "FFmpeg") for encoding.
*   [gamecaster](https://aur.archlinux.org/packages/gamecaster/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gamecaster)]</sup> is a graphical front-end made in [Python](/index.php/Python "Python") that utilizes [FFmpeg](/index.php/FFmpeg "FFmpeg") for encoding; optimized for Ubuntu.

## See also

*   [https://github.com/nullkey/glc](https://github.com/nullkey/glc) - Homepage, and they have a good wiki there as well
*   [https://github.com/darkimmortal/glc](https://github.com/darkimmortal/glc) - An alternative version with support for 32-bit float audio (many Windows games via [wine](/index.php/Wine "Wine") use this)

Retrieved from "[https://wiki.archlinux.org/index.php?title=GLC&oldid=392151](https://wiki.archlinux.org/index.php?title=GLC&oldid=392151)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Multimedia](/index.php/Category:Multimedia "Category:Multimedia")

Hidden category:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")