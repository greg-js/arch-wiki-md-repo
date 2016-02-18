This article describes how to split audio files using CUE metadata.

## Contents

*   [1 Installation](#Installation)
*   [2 Splitting](#Splitting)
*   [3 Tagging](#Tagging)
*   [4 Alternatives](#Alternatives)
*   [5 References](#References)

## Installation

To split audio files you need [shntool](https://www.archlinux.org/packages/?name=shntool). To split CD images in ISO or raw format you need [bchunk](https://www.archlinux.org/packages/?name=bchunk).

The WAV format is supported natively for both input and output. To decode or encode files in other format you need an appropriate decoder. For example: [flac](https://www.archlinux.org/packages/?name=flac), [mac](https://www.archlinux.org/packages/?name=mac), or [wavpack](https://www.archlinux.org/packages/?name=wavpack).

To tag audio files you need extra tools, such as [cuetools](https://www.archlinux.org/packages/?name=cuetools), [mp3info](https://www.archlinux.org/packages/?name=mp3info), or [vorbis-tools](https://www.archlinux.org/packages/?name=vorbis-tools).

## Splitting

To split an audio file accompanied by a CUE sheet into tracks in *.wav* format, use the *shnsplit* command:

```
$ shnsplit -f file.cue file.ape

```

To split *.bin* file with CUE sheet into tracks in *.wav* format:

```
$ bchunk -v -w file.bin file.cue out

```

Format for output file names can be specified with the `-t` option (`%n` for track number, `%t` for title):

```
$ shnsplit -f file.cue -t "%n %t" file.ape

```

*shnsplit* supports on-the-fly encoding to many lossless formats (see `shntool(1)` for the full list). For example to encode split tracks in the FLAC format:

```
$ shnsplit -f file.cue -o flac file.ape

```

Encoding options, including the encoder itself, can be specified with the `-o` parameter (see `shntool(1)` for details):

```
$ shnsplit -f file.cue -o "flac flac -s -8 -o %f -" file.ape

```

The formats supported by *shntool* and default encoder options can be view with the `shntool -a` command. If the desired format is not supported by *shntool*, it can be specified manually. For example, to encode split tracks directly into the Ogg Vorbis format:

```
$ shnsplit -f file.cue -o "cust ext=ogg oggenc -b 192 -o %f -" file.ape

```

## Tagging

You will need [cuetools](https://www.archlinux.org/packages/?name=cuetools) to use *cuetag.sh*.

To copy the metadata from a CUE sheet to the split files you can use:

```
$ cuetag.sh file.cue *.mp3

```

or if you need to select only certain files:

```
$ cuetag.sh file.cue track01.mp3 track02.mp3 track03.mp3 track04.mp3

```

*cuetag.sh* supports id3 tags for *.mp3* files and vorbis tags for *.ogg* and *.flac* files.

## Alternatives

*   This is a script that splits and converts files to tagged FLAC: [https://bbs.archlinux.org/viewtopic.php?id=75774](https://bbs.archlinux.org/viewtopic.php?id=75774).
*   You can also try the [split2flac](https://aur.archlinux.org/packages/split2flac/) or [split2flac-git](https://aur.archlinux.org/packages/split2flac-git/) script from the [AUR](/index.php/AUR "AUR").
*   You may also use [flacon](https://aur.archlinux.org/packages/flacon/) or [flacon-git](https://aur.archlinux.org/packages/flacon-git/), a graphical Qt program that splits, converts and tags album audio files into song audio files. It also features automatic character set detection for CUE files.
*   To avoid quality loss from transcoding mp3 files, [mp3splt-gtk](https://www.archlinux.org/packages/?name=mp3splt-gtk) or [mp3splt](https://www.archlinux.org/packages/?name=mp3splt) may be used to directly split mp3 files either manually or automatically with a provided cuesheet. Batch mode processing is also available.

## References

*   [What is APE?](https://en.wikipedia.org/wiki/Monkey%27s_Audio "wikipedia:Monkey's Audio")
*   [What is CUE?](https://en.wikipedia.org/wiki/Cue_file "wikipedia:Cue file")
*   [Rip Audio CDs](/index.php/Rip_Audio_CDs "Rip Audio CDs")