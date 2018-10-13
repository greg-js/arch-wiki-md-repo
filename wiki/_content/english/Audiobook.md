Related articles

*   [iPod](/index.php/IPod "IPod")
*   [Rip Audio CDs](/index.php/Rip_Audio_CDs "Rip Audio CDs")

Audiobook media can be Audio CDs or downloaded files, several formats exist. For certain hardware media players a specific format will be necessary. This article documents how to create or convert an audiobook of various format types.

## Contents

*   [1 iPod-compatible format](#iPod-compatible_format)
    *   [1.1 Tools](#Tools)
    *   [1.2 Extracting or decoding](#Extracting_or_decoding)
    *   [1.3 Concatenation or splitting](#Concatenation_or_splitting)
    *   [1.4 Encoding](#Encoding)
    *   [1.5 Chapter index merging](#Chapter_index_merging)
        *   [1.5.1 Recurring intervals](#Recurring_intervals)
        *   [1.5.2 Particular intervals](#Particular_intervals)
    *   [1.6 Tagging](#Tagging)
    *   [1.7 Example of batching](#Example_of_batching)
*   [2 Audible format](#Audible_format)
*   [3 See also](#See_also)

## iPod-compatible format

The purpose of this section is to detail a process to create an iPod-friendly audiobook from digital media using Linux native tools.

An audiobook designed for iPods is largely the same as a MPEG-4 audio file — it contains both an audio stream and information about that stream (metadata). The two differences are: one, it is wrapped in a specifically-named MPEG-4 container (`.m4b`); and two, it has a chapter index added to the metadata. The chapter index uses the Quicktime standard.

The basic process is this: the audio source is decoded/uncompressed (it is usually preferably to have a decoded audio-only file as this will simplify the concatenation/splitting of files later and prevent mixing of metadata tags); after this, the audio files are encoded to the [AAC](https://en.wikipedia.org/wiki/Advanced_Audio_Coding "wikipedia:Advanced Audio Coding") format — with a MPEG-4 container; last, the chapter index and audio information tags are added.

Multiple tools are available to help create audiobook files.

### Tools

*   [m4baker-git](https://aur.archlinux.org/packages/m4baker-git/) — GUI program to combine numerous AAC-encoded audio files into a single m4b file with a chapter index

	m4baker usage is straightforward and detailed on the [project wiki](http://code.google.com/p/m4baker/w/list) — its usage will not be covered here.

*   [faac](https://www.archlinux.org/packages/?name=faac) — open source AAC encoder
*   [neroaacenc](https://aur.archlinux.org/packages/neroaacenc/) — proprietary AAC encoder
*   [gpac](https://www.archlinux.org/packages/?name=gpac) — multimedia framework for manipulating MPEG-4 media
*   [lame](https://www.archlinux.org/packages/?name=lame) — MP3 encoder and decoder

### Extracting or decoding

The audio source file(s) will either need to be extracted, if a disc media, or to be decoded, if an encoded file.

If the audiobook is a *disc media*, various [digital audio extraction utilities](/index.php/Optical_disc_drive#Ripping "Optical disc drive") are available. A common way to extract audio from a CD to WAV-formatted files is:

```
cdparanoia -B

```

If the audiobook is a *audio file*, various programs can decode it. For example, for MP3s:

```
lame --decode part-01.mp3

```

(If no splitting of concatenation will be required, files can be directly encoded to AAC with a MPEG-4 container.)

### Concatenation or splitting

Audiobooks parts are typically saved in about one hour, ten minute segments (usually the time extent of a audio CD). They can be concatenated or split as desired.

Join *WAV* files:

```
sndfile-concat track-01.wav track-02.wav… disc-1.wav  # or more easily
sndfile-concat track*.wav disc-1.wav

```

Join *MPEG-4 compatible audio* files (AAC, AVI, MP3…):

```
MP4Box -cat track-01.aac -cat track-02.aac… disc-1.aac

```

Split a wav file ([wavsplit](https://aur.archlinux.org/packages/wavsplit/) can do this (untested)).

Split a *MP3* files into 10 minute intervals:

```
mp3splt -f -t 10.0 part-01.mp3 -o @n

```

Split a *MP3* by chapters/tracks (this method scans for silence and assumes them to be chapter/track marks, splitting them on those marks — these settings are generalized and will likely required further adjusting to work):

```
mp3splt -f -s -p -min=3 part-01.mp3

```

Split *MPEG 4 compatible audio* files (metadata repair will likely be necessary) into 10 minute intervals.

```
MP4Box -split 600 target.mp4

```

### Encoding

Multiple programs exist that can encode to AAC.

To encode with the open source encoder FAAC:

```
faac -q 80 -o part-01.aac part-01.wav
faac -q 80 -o part-01.m4b part-01.wav -w  # with a MPEG-4 container(wrapper)

```

To encode with the proprietary encoder Nero:

```
neroAacEnc -q 0.7 -of part-01.aac -if part-01.wav

```

**Note:** The FAAC quantizer quality setting of 55 (~64kbps) is recommended when encoding from an audiobook CD. This setting is for an audio source that is already an encoded file. The FAAC setting of 80 should reasonably accommodate sound quality while preserving file size close to the original file. *Whenever converting from one lossy format to another, there will always be some amount of information lost.*

**Warning:** Though `ffmpeg` can convert MP3 to an AAC encoding in one step (`ffmpeg -i track1.mp3 -acodec aac -strict -2 track1.aac`), support for AAC is experimental.

### Chapter index merging

To merge a chapter index into a audio file it must be decided what type of index to use: one, *recurring intervals* with periodic chapter times; or two, *particular intervals* with definitive chapter times and names.

Add a MPEG-4 container to the audio file:

```
MP4Box -add disc-1.aac disc-1.m4b

```

#### Recurring intervals

To merge a chapter index with chapters at every 10 minutes:

```
mp4chaps --every 600 disc-1.m4b

```

#### Particular intervals

The method requires writing a chapter index as a text file and merging it into the audio file.

**Note:** `mp4chaps` will complain about *not* seeing a video stream when attempting to merge the chapter index with the `--import` option (a bug should probably be filed). An alternate method is to use `MP4Box`. Though MP4Box is typically seen used for video files it has the ability to add chapters while not introducing a video stream. Because of this the resulting media will be able to play on iPods and iTunes as expected.

The chapter index will need to be written as a text file before being merged into audio file. There are two standards for chapter indexes: one, the Quicktime standard; and two, the Nero standard. Either can be initially merged.

The Quicktime standard looks like this (thousandths of a second can also be added `.000`):

```
00:00:00 Track 01
00:08:40 Track 02
...

```

The Nero standard looks like this:

```
CHAPTER1=00:00:00
CHAPTER1NAME=Track 01
CHAPTER2=00:08:40
CHAPTER2NAME=Track 02
...

```

To merge the chapter index file:

```
MP4Box -chap disc-1.chapters.txt disc-1.m4b

```

To merge the chapter index file in one step along with the audio file and a container:

```
MP4Box -chap disc-1.chapters.txt -add disc-1.aac disc-1.m4b

```

The chapter index will need to be converted to the Quicktime standard (though MP4Box will recognize both chapter index standards when importing, it imports using the Nero standard). Convert to the Quicktime standard with:

```
mp4chaps --convert --chapter-qt disc-1.m4b

```

The chapter index can now be tested, for example, with VLC.

### Tagging

A number of [tagging programs](/index.php/List_of_applications/Multimedia#Audio_tag_editors "List of applications/Multimedia") can be used. The basic command line programs (likely already installed — `mp4tag`, `mp4art`, `mp4file`, `mp4info`…) have numerous abilities:

```
 mp4tags -album "An Good Audiobook" -artist "John Doe" -disk 2 -disks 10 -genre Nonfiction -albumartist "Ms. Foo Bar" -song "Disc 2" -year 2004 disc1.m4b

```

Add coverart:

```
mp4art --add a-good-audiobook.jpg disc-1.m4b

```

Optimize the container:

```
mp4file --optimize *.m4b

```

### Example of batching

A number of audio files can be processed using a loop:

```
for m in *.mp3; do
  lame --decode "$m"
  faac -q 80 -o "${m%.*}".aac "$m"
done

```

To write tags for sequential disc numbering:

```
for b in *.m4b; do
  [ "$n" ] && n=$((10#$n + 1))
  [ -z "$n" ] && n=1
  mp4tags -album "An Good Audiobook"… -disk $(printf "%02u" $n)… "$b"
done

```

## Audible format

It can be a laborious process to convert and Audible book format — [article](http://linuxtidbits.wordpress.com/2011/09/21/audible-com-and-linux-arghh/).

A much easier way is to use this script to retrieve your activation bytes from a downloaded Audible audiobook — [link](https://github.com/inAudible-NG/tables).

You can then use [mpv](https://www.archlinux.org/packages/?name=mpv) to listen to the file:

```
$ mpv --demuxer-lavf-o=activation_bytes=<your activation bytes> <filename>.aax

```

Or you can write the file to unencrypted .mp4 with [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) [(documentation)](http://ffmpeg.org/ffmpeg-all.html#Audible-AAX/):

```
$ ffmpeg -activation_bytes <your activation bytes> -i <filename>.aax -vn -c:a copy <output>.mp4

```

The resulting file will have chapter headers intact.

## See also

*   [Wikipedia:.m4b](https://en.wikipedia.org/wiki/.m4b "wikipedia:.m4b")
*   [RipIT](https://aur.archlinux.org/packages/RipIT/) — thorough DAE with the ability to create chapter indexes with the `--book` option.