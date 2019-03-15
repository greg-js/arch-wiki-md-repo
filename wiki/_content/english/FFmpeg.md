From the project [home page](http://www.ffmpeg.org/):

	FFmpeg is a complete, cross-platform solution to record, convert and stream audio and video. It includes libavcodec - the leading audio/video codec library.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Encoding examples](#Encoding_examples)
    *   [2.1 Screen capture](#Screen_capture)
    *   [2.2 Recording webcam](#Recording_webcam)
    *   [2.3 VOB to any container](#VOB_to_any_container)
    *   [2.4 x264 lossless](#x264_lossless)
    *   [2.5 x265](#x265)
    *   [2.6 Single-pass MPEG-2 (near lossless)](#Single-pass_MPEG-2_(near_lossless))
    *   [2.7 x264: constant rate factor](#x264:_constant_rate_factor)
    *   [2.8 Two-pass x264 (very high-quality)](#Two-pass_x264_(very_high-quality))
    *   [2.9 x264 video stabilization](#x264_video_stabilization)
        *   [2.9.1 First pass](#First_pass)
        *   [2.9.2 Second pass](#Second_pass)
    *   [2.10 Subtitles](#Subtitles)
        *   [2.10.1 Extracting](#Extracting)
        *   [2.10.2 Hardsubbing](#Hardsubbing)
    *   [2.11 Volume gain](#Volume_gain)
    *   [2.12 Extracting audio](#Extracting_audio)
    *   [2.13 Stripping audio](#Stripping_audio)
    *   [2.14 Splitting files](#Splitting_files)
    *   [2.15 Hardware video acceleration](#Hardware_video_acceleration)
        *   [2.15.1 VA-API](#VA-API)
        *   [2.15.2 NVIDIA NVENC/NVDEC](#NVIDIA_NVENC/NVDEC)
        *   [2.15.3 Intel QuickSync (QSV)](#Intel_QuickSync_(QSV))
*   [3 Preset files](#Preset_files)
    *   [3.1 Using preset files](#Using_preset_files)
        *   [3.1.1 libavcodec-vhq.ffpreset](#libavcodec-vhq.ffpreset)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Output the duration of a video](#Output_the_duration_of_a_video)
    *   [4.2 Output stream information as JSON](#Output_stream_information_as_JSON)
    *   [4.3 Create a screen of the video every X frames](#Create_a_screen_of_the_video_every_X_frames)
*   [5 See also](#See_also)

## Installation

**Note:** You may encounter FFmpeg forks like *libav* and *avconv*, see [The FFmpeg/Libav situation](http://blog.pkh.me/p/13-the-ffmpeg-libav-situation.html) for a blog article about the differences between the project and the current status of FFmpeg.

[Install](/index.php/Install "Install") the [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) package.

For the development version, install the [ffmpeg-git](https://aur.archlinux.org/packages/ffmpeg-git/) package. There is also [ffmpeg-full](https://aur.archlinux.org/packages/ffmpeg-full/), which is built with as many optional features enabled as possible.

## Encoding examples

**Note:**

*   It is important parameters are specified in the correct order (e.g. input, video, filters, audio, output), failing to do so may cause parameters being skipped or will prevent FFmpeg from executing.
*   FFmpeg should automatically choose the number of CPU threads available. However you may want to force the number of threads available by the parameter `-threads <number>`.

### Screen capture

FFmpeg includes the [x11grab](http://www.ffmpeg.org/ffmpeg-devices.html#x11grab) and [ALSA](http://www.ffmpeg.org/ffmpeg-devices.html#alsa-1) virtual devices that enable capturing the entire user display and audio input.

To take a screenshot `screen.png`:

```
$ ffmpeg -f x11grab -video_size 1920x1080 -i $DISPLAY -vframes 1 screen.png

```

where `-video_size` specifies the size of the area to capture.

To take a screencast `screen.mkv` with lossless encoding and without audio:

```
$ ffmpeg -f x11grab -video_size 1920x1080 -framerate 25 -i $DISPLAY -c:v ffvhuff screen.mkv

```

Here, the Huffyuv codec is used, which is fast, but produces huge file sizes.

To take a screencast `screen.mp4` with lossy encoding and with audio:

```
$ ffmpeg -f x11grab -video_size 1920x1080 -framerate 25 -i $DISPLAY -f alsa -i default -c:v libx264 -preset ultrafast -c:a aac screen.mp4

```

Here, the x264 codec with the fastest possible encoding speed is used. Other codecs can be used; if writing each frame is too slow (either due to inadequate disk performance or slow encoding), then frames will be dropped and video output will be choppy.

See also the [official documentation](https://trac.ffmpeg.org/wiki/Capture/Desktop#Linux).

### Recording webcam

FFmpeg includes the [video4linux2](http://www.ffmpeg.org/ffmpeg-devices.html#video4linux2_002c-v4l2) and [ALSA](http://www.ffmpeg.org/ffmpeg-devices.html#alsa-1) input devices that enable capturing webcam and audio input.

The following command will record a video `webcam.mp4` from the webcam without audio, assuming that the webcam is correctly recognized under `/dev/video0`:

```
$ ffmpeg -f v4l2 -video_size 640x480 -i /dev/video0 -c:v libx264 -preset ultrafast webcam.mp4

```

where `-video_size` specifies the largest allowed image size from the webcam.

The above produces a silent video. To record a video `webcam.mp4` from the webcam with audio:

```
$ ffmpeg -f v4l2 -video_size 640x480 -i /dev/video0 -f alsa -i default -c:v libx264 -preset ultrafast -c:a aac webcam.mp4

```

Here, the x264 codec with the fastest possible encoding speed is used. Other codecs can be used; if writing each frame is too slow (either due to inadequate disk performance or slow encoding), then frames will be dropped and video output will be choppy.

See also the [official documentation](https://trac.ffmpeg.org/wiki/Capture/Webcam#Linux).

### VOB to any container

Concatenate the desired [VOB](https://en.wikipedia.org/wiki/VOB "wikipedia:VOB") files into a single stream and mux them to MPEG-2:

```
$ cat f0.VOB f1.VOB f2.VOB | ffmpeg -i - out.mp2

```

### x264 lossless

The *ultrafast* preset will provide the fastest encoding and is useful for quick capturing (such as screencasting):

```
$ ffmpeg -i input -c:v libx264 -preset ultrafast -qp 0 -c:a copy output

```

On the opposite end of the preset spectrum is *veryslow* and will encode slower than *ultrafast* but provide a smaller output file size:

```
$ ffmpeg -i input -c:v libx264 -preset veryslow -qp 0 -c:a copy output

```

Both examples will provide the same quality output.

**Tip:** If your computer is able to handle `-preset superfast` in realtime, you should use that instead of `-preset ultrafast`. Ultrafast is *far* less efficient compression than superfast.

### x265

In encoding x265 files, you may need to specify the aspect ratio of the file via `-aspect <width:height>`. Example :

 ` ffmpeg -i input -c:v libx265 -aspect 1920:1080 -preset veryslow -x265-params crf=20 output` 

### Single-pass MPEG-2 (near lossless)

Allow FFmpeg to automatically set DVD standardized parameters. Encode to DVD [MPEG-2](https://en.wikipedia.org/wiki/MPEG-2 "wikipedia:MPEG-2") at ~30 FPS:

```
$ ffmpeg -i *video*.VOB -target ntsc-dvd *output*.mpg

```

Encode to DVD MPEG-2 at ~24 FPS:

```
$ ffmpeg -i *video*.VOB -target film-dvd *output*.mpg

```

### x264: constant rate factor

Used when you want a specific quality output. General usage is to use the highest `-crf` value that still provides an acceptable quality. Lower values are higher quality; 0 is lossless, 18 is visually lossless, and 23 is the default value. A sane range is between 18 and 28\. Use the slowest `-preset` you have patience for. See the [x264 Encoding Guide](https://ffmpeg.org/trac/ffmpeg/wiki/x264EncodingGuide) for more information.

```
$ ffmpeg -i *video* -c:v libx264 -tune film -preset slow -crf 22 -x264opts fast_pskip=0 -c:a libmp3lame -aq 4 *output*.mkv

```

`-tune` option can be used to [match the type and content of the of media being encoded](http://forum.doom9.org/showthread.php?t=149394).

### Two-pass x264 (very high-quality)

Audio deactivated as only video statistics are recorded during the first of multiple pass runs:

```
$ ffmpeg -i *video*.VOB -an -vcodec libx264 -pass 1 -preset veryslow \
-threads 0 -b:v 3000k -x264opts frameref=15:fast_pskip=0 -f rawvideo -y /dev/null

```

Container format is automatically detected and muxed into from the output file extenstion (`.mkv`):

```
$ ffmpeg -i *video*.VOB -acodec aac -b:a 256k -ar 96000 -vcodec libx264 \
-pass 2 -preset veryslow -threads 0 -b:v 3000k -x264opts frameref=15:fast_pskip=0 *video*.mkv

```

### x264 video stabilization

Video stablization using the vbid.stab plugin entails two passes.

#### First pass

The first pass records stabilization parameters to a file and/or a test video for visual analysis.

*   Records stabilization parameters to a file only

```
$ ffmpeg -i input -vf vidstabdetect=stepsize=4:mincontrast=0:result=transforms.trf -f null -

```

*   Records stabilization parameters to a file and create test video "output-stab" for visual analysis

```
$ ffmpeg -i input -vf vidstabdetect=stepsize=4:mincontrast=0:result=transforms.trf -f output-stab

```

#### Second pass

The second pass parses the stabilization parameters generated from the first pass and applies them to produce "output-stab_final". You will want to apply any additional filters at this point so as to aboid subsequent transcoding to preserve as much video quality as possible. The following example performs the following in addition to video stabilization:

*   `unsharp` is recommended by the author of vid.stab. Here we are simply using the defaults of 5:5:1.0:5:5:1.0
*   **Tip:** fade=t=in:st=0:d=4
    fade in from black starting from the beginning of the file for four seconds
*   **Tip:** fade=t=out:st=60:d=4
    fade out to black starting from sixty seconds into the video for four seconds
*   `-c:a pcm_s16le` XAVC-S codec records in pcm_s16be which is losslessly transcoded to pcm_s16le

```
$  ffmpeg -i input -vf vidstabtransform=smoothing=30:interpol=bicubic:input=transforms.trf,unsharp,fade=t=in:st=0:d=4,fade=t=out:st=60:d=4 -c:v libx264 -tune film -preset veryslow -crf 8 -x264opts fast_pskip=0 -c:a pcm_s16le output-stab_final

```

### Subtitles

#### Extracting

Subtitles embedded in container files, such as MPEG-2 and Matroska, can be extracted and converted into SRT, SSA, among other subtitle formats.

*   Inspect a file to determine if it contains a subtitle stream:

 `$ ffprobe foo.mkv` 
```
...
Stream #0:0(und): Video: h264 (High), yuv420p, 1920x800 [SAR 1:1 DAR 12:5], 23.98 fps, 23.98 tbr, 1k tbn, 47.95 tbc (default)
  Metadata:
  CREATION_TIME   : 2012-06-05 05:04:15
  LANGUAGE        : und
Stream #0:1(und): Audio: aac, 44100 Hz, stereo, fltp (default)
 Metadata:
 CREATION_TIME   : 2012-06-05 05:10:34
 LANGUAGE        : und
 HANDLER_NAME    : GPAC ISO Audio Handler
**Stream #0:2: Subtitle: ssa (default)**

```

*   `foo.mkv` has an embedded SSA subtitle which can be extracted into an independent file:

```
$ ffmpeg -i foo.mkv foo.ssa

```

When dealing with multiple subtitles, you may need to specify the stream that needs to be extracted using the `-map <key>:<stream>` parameter:

```
$ ffmpeg -i foo.mkv -map 0:2 foo.ssa

```

#### Hardsubbing

(instructions based on [HowToBurnSubtitlesIntoVideo](http://trac.ffmpeg.org/wiki/HowToBurnSubtitlesIntoVideo) at the FFmpeg wiki)

[Hardsubbing](https://en.wikipedia.org/wiki/Hardsub "wikipedia:Hardsub") entails merging subtitles with the video. Hardsubs can't be disabled, nor language switched.

*   Overlay `foo.mpg` with the subtitles in `foo.ssa`:

```
$ ffmpeg -i foo.mpg -vf subtitles=foo.ssa out.mpg

```

### Volume gain

Change the audio volume in multiples of 256 where **256 = 100%** (normal) volume. Additional values such as 400 are also valid options.

```
-vol 256  = 100%
-vol 512  = 200%
-vol 768  = 300%
-vol 1024 = 400%
-vol 2048 = 800%

```

To double the volume **(512 = 200%)** of an [MP3](https://en.wikipedia.org/wiki/Mp3 "wikipedia:Mp3") file:

```
$ ffmpeg -i *file*.mp3 -vol 512 *louder_file*.mp3

```

To quadruple the volume **(1024 = 400%)** of an [Ogg](https://en.wikipedia.org/wiki/Ogg "wikipedia:Ogg") file:

```
$ ffmpeg -i *file*.ogg -vol 1024 *louder_file*.ogg

```

Note that gain metadata is only written to the output file. Unlike mp3gain or ogggain, the source sound file is untouched.

### Extracting audio

 `$ ffmpeg -i *video*.mpg` 
```
...
Input #0, avi, from '*video*.mpg':
  Duration: 01:58:28.96, start: 0.000000, bitrate: 3000 kb/s
    Stream #0.0: Video: mpeg4, yuv420p, 720x480 [PAR 1:1 DAR 16:9], 29.97 tbr, 29.97 tbn, 29.97 tbc
    Stream #0.1: Audio: ac3, 48000 Hz, stereo, s16, 384 kb/s
    Stream #0.2: Audio: ac3, 48000 Hz, 5.1, s16, 448 kb/s
    Stream #0.3: Audio: dts, 48000 Hz, 5.1 768 kb/s
...

```

Extract the first (`-map 0:1`) [AC-3](https://en.wikipedia.org/wiki/Dolby_Digital "wikipedia:Dolby Digital") encoded audio stream exactly as it was multiplexed into the file:

```
$ ffmpeg -i *video*.mpg -map 0:1 -acodec copy -vn *video*.ac3

```

Convert the third (`-map 0:3`) [DTS](https://en.wikipedia.org/wiki/DTS_(sound_system) audio stream to an [AAC](https://en.wikipedia.org/wiki/Advanced_Audio_Coding "wikipedia:Advanced Audio Coding") file with a bitrate of 192 kb/s and a [sampling rate](https://en.wikipedia.org/wiki/Sampling_rate "wikipedia:Sampling rate") of 96000 Hz:

```
$ ffmpeg -i *video*.mpg -map 0:3 -acodec aac -b:a 192k -ar 96000 -vn *output*.aac

```

`-vn` disables the processing of the video stream.

Extract audio stream with certain time interval:

```
$ ffmpeg -ss 00:01:25 -t 00:00:05 -i *video*.mpg -map 0:1 -acodec copy -vn *output*.ac3

```

`-ss` specifies the start point, and `-t` specifies the duration.

### Stripping audio

1.  Copy the first video stream (`-map 0:0`) along with the second AC-3 audio stream (`-map 0:2`).
2.  Convert the AC-3 audio stream to two-channel MP3 with a bitrate of 128 kb/s and a sampling rate of 48000 Hz.

```
$ ffmpeg -i *video*.mpg -map 0:0 -map 0:2 -vcodec copy -acodec libmp3lame \
-b:a 128k -ar 48000 -ac 2 *video*.mkv

```
 `$ ffmpeg -i *video*.mkv` 
```
...
Input #0, avi, from '*video*.mpg':
  Duration: 01:58:28.96, start: 0.000000, bitrate: 3000 kb/s
    Stream #0.0: Video: mpeg4, yuv420p, 720x480 [PAR 1:1 DAR 16:9], 29.97 tbr, 29.97 tbn, 29.97 tbc
    Stream #0.1: Audio: mp3, 48000 Hz, stereo, s16, 128 kb/s

```

**Note:** Removing undesired audio streams allows for additional bits to be allocated towards improving video quality.

### Splitting files

You can use the `copy` codec to perform operations on a file without changing the encoding. For example, this allows you to easily split any kind of media file into two:

```
$ ffmpeg -i file.ext -t 00:05:30 -c copy part1.ext -ss 00:05:30 -c copy part2.ext

```

### Hardware video acceleration

**Warning:** Encoding may fail when using hardware acceleration, use software encoding as a fallback.

Encoding performance may be improved by using [hardware acceleration API's](https://trac.ffmpeg.org/wiki/HWAccelIntro), however only a specific kind of codec(s) are allowed and/or may not always produce the same result when using software encoding.

#### VA-API

[VA-API](/index.php/VA-API "VA-API") can be used for encoding and decoding on Intel CPUs (requires [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver)) and on certain AMD GPUs when using the open-source [AMDGPU](/index.php/AMDGPU "AMDGPU") driver (requires [libva-mesa-driver](https://www.archlinux.org/packages/?name=libva-mesa-driver)). See the following [GitHub gist](https://gist.github.com/Brainiarc7/95c9338a737aa36d9bb2931bed379219) and [Libav documentation](https://wiki.libav.org/Hardware/vaapi) for information about available parameters and supported platforms.

An example of encoding using the supported H.264 codec:

```
$ ffmpeg -threads 1 -i file.ext -vaapi_device /dev/dri/renderD128 -vcodec h264_vaapi -vf format='nv12|vaapi,hwupload' output.mp4

```

#### NVIDIA NVENC/NVDEC

[NVENC](https://en.wikipedia.org/wiki/Nvidia_NVENC "w:Nvidia NVENC") and [NVDEC](https://en.wikipedia.org/wiki/Nvidia_NVDEC "w:Nvidia NVDEC") can be used for encoding/decoding when using the proprietary [NVIDIA](/index.php/NVIDIA "NVIDIA") driver with the [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) package installed. Minimum supported GPUs are from 600 series, see [Hardware video acceleration#NVIDIA](/index.php/Hardware_video_acceleration#NVIDIA "Hardware video acceleration") for details.

The [following gist](https://gist.github.com/Brainiarc7/8b471ff91319483cdb725f615908286e) provides some techniques. NVENC is somewhat similar to [CUDA](/index.php/CUDA "CUDA"), thus it works even from terminal session. Depending on hardware NVENC is several times faster than Intel's VA-API encoders.

To print available options execute (`hevc_nvenc` may also be available):

```
$ ffmpeg -help encoder=h264_nvenc

```

Example usage:

```
$ ffmpeg -i source.ext -c:v h264_nvenc -rc constqp -qp 28 output.mkv

```

#### Intel QuickSync (QSV)

[Quick Sync Video](https://www.intel.com/content/www/us/en/architecture-and-technology/quick-sync-video/quick-sync-video-general.html%7CIntel®) uses media processing capabilities of an [Intel](/index.php/Intel "Intel") GPU to decode and encode fast, enabling the processor to complete other tasks and improving system responsiveness.

This requires [intel-media-sdk](https://aur.archlinux.org/packages/intel-media-sdk/) to be installed and FFmpeg needs to be build with `--enable-libmfx`. Packages are available in [AUR](/index.php/AUR "AUR"): [ffmpeg-qsv](https://aur.archlinux.org/packages/ffmpeg-qsv/) or [ffmpeg-qsv-git](https://aur.archlinux.org/packages/ffmpeg-qsv-git/). The package [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) doesn't have this flag enabled.

The usage of QuickSync is describe in the [FFmpeg Wiki](https://trac.ffmpeg.org/wiki/Hardware/QuickSync). It is recommended to use [VA-API](/index.php/VA-API "VA-API") [[1]](https://trac.ffmpeg.org/wiki/Hardware/VAAPI) with either the *iHD* or *i965* driver instead of using *libmfx* directly, see the FFmpeg Wiki section *Hybrid transcode* for encoding examples and [Hardware video acceleration#Configuring VA-API](/index.php/Hardware_video_acceleration#Configuring_VA-API "Hardware video acceleration") for driver instructions.

## Preset files

Populate `~/.ffmpeg` with the default [preset files](http://ffmpeg.org/ffmpeg.html#Preset-files):

```
$ cp -iR /usr/share/ffmpeg ~/.ffmpeg

```

Create new and/or modify the default preset files:

 `~/.ffmpeg/libavcodec-vhq.ffpreset` 
```
vtag=DX50
mbd=2
trellis=2
flags=+cbp+mv0
pre_dia_size=4
dia_size=4
precmp=4
cmp=4
subcmp=4
preme=2
qns=2
```

### Using preset files

Enable the `-vpre` option after declaring the desired `-vcodec`

#### libavcodec-vhq.ffpreset

*   `libavcodec` **=** Name of the vcodec/acodec
*   `vhq` **=** Name of specific preset to be called out
*   `ffpreset` **=** FFmpeg preset filetype suffix

## Tips and tricks

### Output the duration of a video

```
$ ffprobe -select_streams v:0 -show_entries stream=duration -of default=noprint_wrappers=1:nokey=1 file.ext

```

### Output stream information as JSON

```
$ ffprobe -v quiet -print_format json -show_format -show_streams file.ext

```

### Create a screen of the video every X frames

```
$ ffmpeg -i file.ext -an -s 319x180 -vf fps=1/**100** -qscale:v 75 %03d.jpg

```

## See also

*   [FFmpeg documentation](http://ffmpeg.org/ffmpeg.html) - official documentation
*   [Encoding](https://trac.ffmpeg.org/wiki#Encoding) - FFmpeg wiki
*   [Encoding with the x264 codec](http://www.mplayerhq.hu/DOCS/HTML/en/menc-feat-x264.html) - MEncoder documentation
*   [H.264 encoding guide](http://avidemux.org/admWiki/doku.php?id=tutorial:h.264) - Avidemux wiki
*   [Using FFmpeg](http://howto-pages.org/ffmpeg/) - Linux how to pages
*   [List](http://ffmpeg.org/general.html#Supported-File-Formats-and-Codecs) of supported audio and video streams