# HandBrakeCLI

[HandBrakeCLI](http://handbrake.fr/) is command-line driven interface to a collection of built-in libraries which enables the decoding, encoding and conversion of audio and video streams to [MP4](https://en.wikipedia.org/wiki/MPEG-4_Part_14 "wikipedia:MPEG-4 Part 14") (M4V) and [MKV](https://en.wikipedia.org/wiki/Matroska "wikipedia:Matroska") container formats with an emphasis on [H.264/MPEG-4 AVC](https://en.wikipedia.org/wiki/H.264/MPEG-4_AVC "wikipedia:H.264/MPEG-4 AVC") encoding through [x264](http://www.videolan.org/developers/x264.html).

## Contents

*   [1 Package installation](#Package_installation)
*   [2 Encoding examples](#Encoding_examples)
    *   [2.1 Single-pass x264 (very high-quality)](#Single-pass_x264_.28very_high-quality.29)
    *   [2.2 Two-pass x264 (very high-quality)](#Two-pass_x264_.28very_high-quality.29)
*   [3 Adding subtitles](#Adding_subtitles)
*   [4 See also](#See_also)

## Package installation

[Install](/index.php/Install "Install") [handbrake-cli](https://www.archlinux.org/packages/?name=handbrake-cli) from the [Official repositories](/index.php/Official_repositories "Official repositories").

## Encoding examples

### Single-pass x264 (very high-quality)

 `HandBrakeCLI -i X-Men.First.Class.2011.vob -o X-Men.First.Class.2011.mkv -E lame -B 160k -6 stereo -R 48000 -e x264 -x b_adapt=2:bframes=8:direct=auto:fast_pskip=0:deblock=-1,-1:psy-rd=1,0.15:me=umh:me_range=24:partitions=all:ref=16:subq=10:trellis=2:rc_lookahead=60:frameref=15:threads=auto -s1 -S 2250 -2 -v2` 

### Two-pass x264 (very high-quality)

 `HandBrakeCLI -i X-Men.First.Class.2011.vob -o X-Men.First.Class.2011.mkv -E lame -B 160k -6 stereo -R 48000 -e x264 -x b_adapt=2:bframes=8:direct=auto:fast_pskip=0:deblock=-1,-1:psy-rd=1,0.15:me=umh:me_range=24:partitions=all:ref=16:subq=10:trellis=2:rc_lookahead=60:frameref=15:threads=auto -s1 -S 2250 -2 -v2` 

ULTRAFAST TESTING

 `HandBrakeCLI -i Hostel.II.vob -o Hostel.II.mkv -E lame -B 128k -6 dpl2 -R 48000 -e x264 -x ref=1:bframes=0:cabac=0:8x8dct=0:weightp=0:me=dia:subq=0:rc-lookahead=0:mbtree=0:analyse=none:trellis=0:aq-mode=0:scenecut=0:no-deblock=1:threads=auto -s1 -S 750 -v` 

## Adding subtitles

## See also

*   [Official CLI Guide](https://trac.handbrake.fr/wiki/CLIGuide)

Retrieved from "[https://wiki.archlinux.org/index.php?title=HandBrakeCLI&oldid=412094](https://wiki.archlinux.org/index.php?title=HandBrakeCLI&oldid=412094)"