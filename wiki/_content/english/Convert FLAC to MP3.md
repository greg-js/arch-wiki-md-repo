Related articles

*   [Convert any Movie to DVD Video](/index.php/Convert_any_Movie_to_DVD_Video "Convert any Movie to DVD Video")

This article presents ways of doing audio transcoding between FLAC and MP3 audio files using command line/scripted tools, and suggest a few graphical utilities to do the same and more.

## Contents

*   [1 Scripts](#Scripts)
    *   [1.1 With FFmpeg](#With_FFmpeg)
        *   [1.1.1 Parallel version](#Parallel_version)
        *   [1.1.2 Makefile for incremental recursive transcoding](#Makefile_for_incremental_recursive_transcoding)
    *   [1.2 Without FFmpeg](#Without_FFmpeg)
    *   [1.3 Recursively](#Recursively)
    *   [1.4 Usage](#Usage)
    *   [1.5 Packages](#Packages)
*   [2 Graphical applications](#Graphical_applications)
*   [3 See also](#See_also)

## Scripts

In these two examples, FLAC files in current directory are encoded by the LAME MP3 encoder. Both scripts pass the ID3 tags from the FLAC files to the resulting MP3 files, and encode to MP3 V0\. V0 results in a variable bitrate usually between 220-260 kbps. The audio of a V0 file is transparent, meaning one cannot tell the difference between the lossy file and the original source (compact disc/lossless), but yet the file size is significantly reduced. For more information on LAME switches/settings such as V0, visit the [Hydrogenaudio LAME Wiki](http://wiki.hydrogenaudio.org/index.php?title=LAME).

The original `.flac` files are not modified and the resulting `.mp3`s will be in the same directory. All files with extensions not matching `*.flac` in the working directory (`.nfo`, images, `.sfv`, etc.) are ignored.

### With FFmpeg

Chances are, your system already has [FFmpeg](/index.php/FFmpeg "FFmpeg") installed, which brings in the [flac](https://www.archlinux.org/packages/?name=flac) and [lame](https://www.archlinux.org/packages/?name=lame) packages. FFmpeg has all the encoding and decoding facilities built in to do the job.

```
#!/bin/bash

for a in ./*.flac; do
  ffmpeg -i "$a" -qscale:a 0 "${a[@]/%flac/mp3}"
done

```

#### Parallel version

Since LAME is a single-threaded encoder, conversion can be accelerated by encoding multiple files concurrently on multiple cores. To do this, [install](/index.php/Install "Install") the [parallel](https://www.archlinux.org/packages/?name=parallel) package, and run:

```
parallel ffmpeg -i {} -qscale:a 0 {.}.mp3 ::: ./*.flac

```

#### Makefile for incremental recursive transcoding

**Warning:** Makefiles do not handle spaces correctly, see [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1506405#p1506405) for details.

Besides transcoding in parallel with `make -j$(nproc)`, this has the added benefit of not regenerating transcoded files that already exist on subsequent executions:

```
SOURCE_DIR := flacdir
XCODE_MP3_DIR := mp3dir
# NOTE: see lame -v option for quality meaning
XCODE_MP3_QUALITY := 0

# Find .flac sources and determine corresponding targets
flac_srcs := $(shell find $(SOURCE_DIR) -type f -name '*.flac')
flac_2_mp3_tgts := $(patsubst $(SOURCE_DIR)/%.flac, $(XCODE_MP3_DIR)/%.mp3, \
    $(flac_srcs))

.PHONY: all mp3 flac_2_mp3

all: mp3 

mp3: flac_2_mp3

flac_2_mp3: $(flac_2_mp3_tgts)

$(XCODE_MP3_DIR)/%.mp3: $(SOURCE_DIR)/%.flac
        @echo "converting -> $@"
        @mkdir -p "$(@D)"
        @ffmpeg -v error -i "$<" -codec:a libmp3lame \
            -q:a $(XCODE_MP3_QUALITY) "$(@)"

```

### Without FFmpeg

If for some reason FFmpeg is not installed and you do not want to install it, you still need to have [flac](https://www.archlinux.org/packages/?name=flac) and [lame](https://www.archlinux.org/packages/?name=lame) installed. Here, the tagging process is more explicit using the metadata utility that comes with [flac](https://www.archlinux.org/packages/?name=flac) and passing the information to [lame](https://www.archlinux.org/packages/?name=lame). The process duration will slightly increase since FLACs must first be decoded to WAVE and then fed into the MP3 encoder.

```
#!/bin/bash

for a in ./*.flac; do
  # give output correct extension
  OUTF="${a[@]/%flac/mp3}"

  # get the tags
  ARTIST=$(metaflac "$a" --show-tag=ARTIST | sed s/.*=//g)
  TITLE=$(metaflac "$a" --show-tag=TITLE | sed s/.*=//g)
  ALBUM=$(metaflac "$a" --show-tag=ALBUM | sed s/.*=//g)
  GENRE=$(metaflac "$a" --show-tag=GENRE | sed s/.*=//g)
  TRACKNUMBER=$(metaflac "$a" --show-tag=TRACKNUMBER | sed s/.*=//g)
  DATE=$(metaflac "$a" --show-tag=DATE | sed s/.*=//g)

  # stream flac into the lame encoder
  flac -c -d "$a" | lame -V0 --add-id3v2 --pad-id3v2 --ignore-tag-errors \
    --ta "$ARTIST" --tt "$TITLE" --tl "$ALBUM"  --tg "${GENRE:-12}" \
    --tn "${TRACKNUMBER:-0}" --ty "$DATE" - "$OUTF"
done

```

### Recursively

A useful extension of the above scripts is to let them recurse into all subdirectories of the working directory. To do so, replace the first line (`for .... do`) with:

```
find -type f -name "*.flac" -print0 | while read -d $'\0' a; do

```

### Usage

For ease of use, add the script to your `PATH`. Open up a terminal, `cd` to the directory of FLAC files that you wish to convert, and invoke `flac2mp3` (or whatever you named the script). You will see the verbose decoding/encoding process in the terminal which may take a few moments. Done! At this point, it is trivial to `mv *.mp3` all your new MP3s wherever you wish.

### Packages

*   [whatmp3](https://aur.archlinux.org/packages/whatmp3/) - A small Python script that accepts a list of directories containing FLAC files as arguments and converts them to MP3 with the specified options.
*   [flac2all](https://aur.archlinux.org/packages/flac2all/) - Audio converter of FLAC to either Ogg Vorbis or MP3 retaining all tags and metadata.
*   [flac2mp3-bash](https://aur.archlinux.org/packages/flac2mp3-bash/) - Bash script to convert Flac to Mp3 easily.

## Graphical applications

*   **SoundConverter** — A dedicated audio transcoding utility built for the [GNOME](/index.php/GNOME "GNOME") desktop and relying on GStreamer. It can make use of [GNOME Audio Profiles](http://library.gnome.org/users/gnome-audio-profiles/stable/gnome-audio-profiles-usage.html.en) and features multithreaded conversions. It can also extract the audio from videos.

	[http://soundconverter.org/](http://soundconverter.org/) || [soundconverter](https://www.archlinux.org/packages/?name=soundconverter)

*   **soundKonverter** — A Qt graphical frontend to various audio manipulation programs. Features conversion, ripping and other audio manipulation functionalities.

	[https://github.com/HessiJames/soundkonverter/wiki](https://github.com/HessiJames/soundkonverter/wiki) || [soundkonverter](https://www.archlinux.org/packages/?name=soundkonverter)

*   **[WinFF](https://en.wikipedia.org/wiki/FFmpeg#Projects_using_FFmpeg "wikipedia:FFmpeg")** — A GUI for the powerful multimedia converter FFmpeg. Features dedicated profiles for audio transcoding.

	[http://code.google.com/p/winff/](http://code.google.com/p/winff/) || [winff](https://www.archlinux.org/packages/?name=winff)

## See also

*   [https://www.xiph.org/flac/](https://www.xiph.org/flac/)
*   [wikipedia:FLAC](https://en.wikipedia.org/wiki/FLAC "wikipedia:FLAC")
*   [http://lame.sourceforge.net/](http://lame.sourceforge.net/)
*   [http://wiki.hydrogenaudio.org/index.php?title=Flac](http://wiki.hydrogenaudio.org/index.php?title=Flac) - More information on FLAC.