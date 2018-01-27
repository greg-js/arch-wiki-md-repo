From the project [home page](http://www.ffmpeg.org/):

	*FFmpeg is a complete, cross-platform solution to record, convert and stream audio and video. It includes libavcodec - the leading audio/video codec library.*

## Contents

*   [1 Package installation](#Package_installation)
    *   [1.1 Manual installation](#Manual_installation)
*   [2 Encoding examples](#Encoding_examples)
    *   [2.1 Screen cast](#Screen_cast)
    *   [2.2 Recording webcam](#Recording_webcam)
    *   [2.3 VOB to any container](#VOB_to_any_container)
    *   [2.4 x264 lossless](#x264_lossless)
    *   [2.5 x265](#x265)
    *   [2.6 Single-pass MPEG-2 (near lossless)](#Single-pass_MPEG-2_.28near_lossless.29)
    *   [2.7 x264: constant rate factor](#x264:_constant_rate_factor)
    *   [2.8 Two-pass x264 (very high-quality)](#Two-pass_x264_.28very_high-quality.29)
    *   [2.9 Two-pass MPEG-4 (very high-quality)](#Two-pass_MPEG-4_.28very_high-quality.29)
        *   [2.9.1 Determining bitrates with fixed output file sizes](#Determining_bitrates_with_fixed_output_file_sizes)
    *   [2.10 x264 video stabilization](#x264_video_stabilization)
        *   [2.10.1 First pass](#First_pass)
        *   [2.10.2 Second pass](#Second_pass)
    *   [2.11 Subtitles](#Subtitles)
        *   [2.11.1 Extracting](#Extracting)
        *   [2.11.2 Hardsubbing](#Hardsubbing)
    *   [2.12 Volume gain](#Volume_gain)
    *   [2.13 Extracting audio](#Extracting_audio)
    *   [2.14 Stripping audio](#Stripping_audio)
    *   [2.15 Splitting files](#Splitting_files)
    *   [2.16 Hardware acceleration](#Hardware_acceleration)
        *   [2.16.1 Intel GPU (VA-API)](#Intel_GPU_.28VA-API.29)
        *   [2.16.2 Nvidia GPU (NVENC)](#Nvidia_GPU_.28NVENC.29)
*   [3 Preset files](#Preset_files)
    *   [3.1 Using preset files](#Using_preset_files)
        *   [3.1.1 libavcodec-vhq.ffpreset](#libavcodec-vhq.ffpreset)
            *   [3.1.1.1 Two-pass MPEG-4 (very high quality)](#Two-pass_MPEG-4_.28very_high_quality.29)
*   [4 FFserver](#FFserver)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Output the duration of a video](#Output_the_duration_of_a_video)
    *   [5.2 Output stream information as JSON](#Output_stream_information_as_JSON)
    *   [5.3 Create a screen of the video every X frames](#Create_a_screen_of_the_video_every_X_frames)
*   [6 See also](#See_also)

## Package installation

**Note:** You may encounter FFmpeg forks like *libav* and *avconv*, see [The FFmpeg/Libav situation](http://blog.pkh.me/p/13-the-ffmpeg-libav-situation.html) for a blog article about the differences between the project and the current status of FFmpeg.

[Install](/index.php/Install "Install") the [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) package.

For the development version, install the [ffmpeg-git](https://aur.archlinux.org/packages/ffmpeg-git/) package. There is also [ffmpeg-full](https://aur.archlinux.org/packages/ffmpeg-full/), which is built with as many optional features enabled as possible.

### Manual installation

Some users may wish to skip the package or AUR and compile FFmpeg themselves from its git master directly, and add `/usr/local/lib` to `/etc/ld.so.conf`. This can cause the `/usr/bin/ffmpeg` tool provided by [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) to crash or work improperly due to the library version mismatch. (Frequently [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) is still installed as a dependency.) One fix for this is to add `/usr/lib` to the rpath of `/usr/bin/ffmpeg` with a tool such as [patchelf](https://www.archlinux.org/packages/?name=patchelf):

```
# patchelf --set-rpath /usr/lib /usr/bin/ffmpeg

```

This will be revoked whenever ffmpeg is reinstalled or upgraded, so adding a pacman hook might be prudent:

 `/etc/pacman.d/hooks/ffmpeg.hook` 
```
[Trigger]
Operation=Install
Operation=Upgrade
Type=Package
Target=ffmpeg

[Action]
Description=Adding /usr/lib to ffmpeg rpath...
Depends=patchelf
When=PostTransaction
Exec=/usr/bin/patchelf --set-rpath /usr/lib /usr/bin/ffmpeg
```

## Encoding examples

**Note:**

*   It is important parameters are specified in the correct order (e.g. input, video, filters, audio, output), failing to do so may cause parameters being skipped or will prevent FFmpeg from executing.
*   FFmpeg should automatically choose the number of CPU threads available. However you may want to force the number of threads available by the parameter `-threads <number>`.

### Screen cast

FFmpeg includes the [x11grab](http://www.ffmpeg.org/ffmpeg-devices.html#x11grab) and [ALSA](http://www.ffmpeg.org/ffmpeg-devices.html#alsa-1) virtual devices that enable capturing the entire user display and audio input.

To create `test.mkv` with lossless encoding:

```
$ ffmpeg -f x11grab -video_size 1920x1080 -framerate 60 -i $DISPLAY -f alsa -i default -c:v ffvhuff -c:a flac test.mkv

```

where `-video_size` specifies the size of the area to capture. Check the FFmpeg manual for examples of how to change the screen or position of the capture area.

To implicitly encode to a shareable size use :

```
$ ffmpeg -f x11grab -video_size 1920x1080 -framerate 60 -i $DISPLAY -f alsa -i default -r 30 -s 1280x720 -c:v libx264 -preset:v veryfast -b:v 2000k -c:a libopus -b:a 128k test.mkv

```

You may want to adjust the parameters (left-to-right): input **f**ormat, [input]**s**ize, frame**r**ate, **i**nput (in this case display, but could be a file too), input **f**ormat, **i**nput, **c**odec:**v**ideo, **b**itrate:**v**ideo, [output]**s**ize of output. Without context the meaning of the parameters may seem ambigious. See the manpage for the synopsis.

### Recording webcam

FFmpeg supports grabbing input from Video4Linux2 devices. The following command will record a video from the webcam, assuming that the webcam is correctly recognized under `/dev/video0`:

```
$ ffmpeg -f v4l2 -video_size 640x480 -i /dev/video0 output.mkv

```

The above produces a silent video. It is also possible to include audio sources from a microphone. The following command will include a stream from the default [ALSA](/index.php/ALSA "ALSA") recording device into the video:

```
$ ffmpeg -f v4l2 -video_size 640x480 -i /dev/video0 -f alsa -i default output.mkv

```

To use [PulseAudio](/index.php/PulseAudio "PulseAudio") with an ALSA backend:

```
$ ffmpeg -f v4l2 -video_size 640x480 -i /dev/video0 -f alsa -i pulse output.mkv

```

For a higher quality capture, try encoding the output using higher quality settings:

```
$ ffmpeg -f v4l2 -video_size 640x480 -i /dev/video0 -f alsa -i default -c:v libx264 -crf:v 18 -c:a flac output.mkv

```

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
$ ffmpeg -i *video*.VOB -an -vcodec libx264 -pass 1  -preset veryslow \
-threads 0 -b 3000k -x264opts frameref=15:fast_pskip=0 -f rawvideo -y /dev/null

```

Container format is automatically detected and muxed into from the output file extenstion (`.mkv`):

```
$ ffmpeg -i *video*.VOB -acodec libvo-aacenc -ab 256k -ar 96000 -vcodec libx264 \
-pass 2 -preset veryslow -threads 0 -b 3000k -x264opts frameref=15:fast_pskip=0 *video*.mkv

```

**Tip:** If you receive `Unknown encoder 'libvo-aacenc'` error (given the fact that your ffmpeg is compiled with libvo-aacenc enabled), you may want to try `-acodec libvo_aacenc`, an underscore instead of hyphen.

### Two-pass MPEG-4 (very high-quality)

Audio deactivated as only video statistics are logged during the first of multiple pass runs:

```
$ ffmpeg -i *video*.VOB -an -vcodec mpeg4 -pass 1 -mbd 2 -trellis 2 -flags +cbp+mv0 \
-pre_dia_size 4 -dia_size 4 -precmp 4 -cmp 4 -subcmp 4 -preme 2 -qns 2 -b 3000k \
-f rawvideo -y /dev/null

```

Container format is automatically detected and muxed into from the output file extenstion (`.avi`):

```
$ ffmpeg -i *video*.VOB -acodec copy -vcodec mpeg4 -vtag DX50 -pass 2 -mbd 2 -trellis 2 \
-flags +cbp+mv0 -pre_dia_size 4 -dia_size 4 -precmp 4 -cmp 4 -subcmp 4 -preme 2 -qns 2 \
-b 3000k *video*.avi

```

*   Introducing `threads`=`n`>`1` for `-vcodec mpeg4` may skew the effects of [motion estimation](https://en.wikipedia.org/wiki/Motion_estimation "wikipedia:Motion estimation") and lead to [reduced video quality](http://ffmpeg.org/faq.html#Why-do-I-see-a-slight-quality-degradation-with-multithreaded-MPEG_002a-encoding_003f) and compression efficiency.
*   The two-pass MPEG-4 example above also supports output to the [MP4](https://en.wikipedia.org/wiki/MPEG-4_Part_14 "wikipedia:MPEG-4 Part 14") container (replace `.avi` with `.mp4`).

#### Determining bitrates with fixed output file sizes

*   (Desired File Size in MB - Audio File Size in MB) **x** 8192 kb/MB **/** Length of Media in Seconds (s) **=** [Bitrate](https://en.wikipedia.org/wiki/Bitrate "wikipedia:Bitrate") in kb/s

*   (3900 MB - 275 MB) = 3625 MB **x** 8192 kb/MB **/** 8830 s = 3363 kb/s required to achieve an approximate total output file size of 3900 MB

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
  CREATION_TIME   : 2012-06-05 05:04:15
  LANGUAGE        : und
Stream #0:1(und): Audio: aac, 44100 Hz, stereo, fltp (default)
 Metadata:
 CREATION_TIME   : 2012-06-05 05:10:34
 LANGUAGE        : und
 HANDLER_NAME    : GPAC ISO Audio Handler
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

(instructions based on an [FFmpeg wiki article](http://trac.ffmpeg.org/wiki/How%20to%20burn%20subtitles%20into%20the%20video))

[Hardsubbing](https://en.wikipedia.org/wiki/Hardsub "wikipedia:Hardsub") entails merging subtitles with the video. Hardsubs can't be disabled, nor language switched.

*   Overlay `foo.mpg` with the subtitles in `foo.ssa`:

```
$ ffmpeg -i foo.mpg -c copy -vf subtitles=foo.ssa out.mpg

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
$ ffmpeg -i *video*.mpg -map 0:3 -acodec libvo-aacenc -ab 192k -ar 96000 -vn *output*.aac

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
-ab 128k -ar 48000 -ac 2 *video*.mkv

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

### Hardware acceleration

**Warning:** Encoding may fail when using hardware acceleration, use software encoding as a fallback.

Encoding performance may be improved by using [hardware acceleration API's](https://trac.ffmpeg.org/wiki/HWAccelIntro), however only a specific kind of codec(s) are allowed and/or may not always produce the same result when using software encoding.

#### Intel GPU (VA-API)

See the following [GitHub gist](https://gist.github.com/Brainiarc7/95c9338a737aa36d9bb2931bed379219) and [Libav documentation](https://wiki.libav.org/Hardware/vaapi) for information about available parameters and supported [Intel](/index.php/Intel "Intel") platforms when using [VA-API](/index.php/VA-API "VA-API").

An example of encoding using the supported H.264 codec:

```
$ ffmpeg -threads 1 -i file.ext -vaapi_device /dev/dri/renderD128 -vcodec h264_vaapi -vf format='nv12|vaapi,hwupload' output.mp4

```

#### Nvidia GPU (NVENC)

Since at least 3.4.1 the [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) package can use NVENC if [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) and proprietary kernel module (e.g. [nvidia](https://www.archlinux.org/packages/?name=nvidia)) are installed. See [this gist](https://gist.github.com/Brainiarc7/8b471ff91319483cdb725f615908286e) for some techniques. Minimum supported GPUs are from 600 series (see [w:Nvidia NVENC](https://en.wikipedia.org/wiki/Nvidia_NVENC "w:Nvidia NVENC")). NVENC is somewhat similar to [CUDA](/index.php/CUDA "CUDA"), thus it works even from terminal session. Depending on hardware NVENC is several times faster than Intel's VA-API encoders.

To print available options execute (`hevc_nvenc` may also be available):

```
$ ffmpeg -help encoder=h264_nvenc

```

Example usage:

```
$ ffmpeg -i source.ext -c:v h264_nvenc -rc constqp -qp 28 output.mkv

```

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

##### Two-pass MPEG-4 (very high quality)

First pass of a multipass (bitrate) ratecontrol transcode:

```
$ ffmpeg -i *video*.mpg -an -vcodec mpeg4 -pass 1 -vpre vhq -f rawvideo -y /dev/null

```

Ratecontrol based on the video statistics logged from the first pass:

```
$ ffmpeg -i *video*.mpg -acodec libvorbis -aq 8 -ar 48000 -vcodec mpeg4 \
-pass 2 -vpre vhq -b 3000k *output*.mp4

```

*   **libvorbis quality settings (VBR)**

*   `-aq 4` = 128 kb/s
*   `-aq 5` = 160 kb/s
*   `-aq 6` = 192 kb/s
*   `-aq 7` = 224 kb/s
*   `-aq 8` = 256 kb/s

*   [aoTuV](http://www.geocities.jp/aoyoume/aotuv/) is generally preferred over [libvorbis](http://vorbis.com/) provided by [Xiph.Org](http://www.xiph.org/) and is provided by [libvorbis-aotuv](https://aur.archlinux.org/packages/libvorbis-aotuv/).

## FFserver

The FFmpeg package includes FFserver, which can be used to stream media over a network. To use it, you first need to create the config file `/etc/ffserver.conf` to define your *feeds* and *streams*. Each feed specifies how the media will be sent to ffserver and each stream specifies how a particular feed will be transcoded for streaming over the network. You can start with the [sample configuration file](https://www.ffmpeg.org/sample.html) or check [ffserver(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ffserver.1) for feed and stream examples. Here is a simple configuration file for streaming flash video:

 `/etc/ffserver.conf` 
```
HTTPPort 8090
HTTPBindAddress 0.0.0.0
MaxHTTPConnections 2000
MaxClients 1000
MaxBandwidth 10000
CustomLog -

<Feed av_feed.ffm>
        File /tmp/av_feed.ffm
        FileMaxSize 1G
        ACL allow 127.0.0.1
</Feed>

<Stream av_stream.flv>
        Feed av_feed.ffm
        Format flv

        VideoCodec libx264
        VideoFrameRate 25
        VideoSize hd1080
        VideoBitRate 400
        AVOptionVideo qmin 10
        AVOptionVideo qmax 42
        AVOptionVideo flags +global_header

        AudioCodec libmp3lame
        AVOptionAudio flags +global_header

        Preroll 15
</Stream>

<Stream stat.html>
        Format status
        ACL allow localhost
        ACL allow 192.168.0.0 192.168.255.255
</Stream>

<Redirect index.html>
        URL http://www.ffmpeg.org/
</Redirect>
```

Once you have created your config file, you can start the server and send media to your feeds. For the previous config example, this would look like

```
$ ffserver &
$ ffmpeg -i myvideo.mkv http://localhost:8090/av_feed.ffm

```

You can then stream your media using the URL `http://yourserver.net:8090/av_stream.flv`.

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
$ ffmpeg -i file.ext -an -s 319x180 -vf fps=1/**100** -qscale:v 75 %03d.jpg

```

## See also

*   [x264 Settings](http://mewiki.project357.com/wiki/X264_Settings) - MeWiki documentation
*   [FFmpeg documentation](http://ffmpeg.org/ffmpeg-doc.html) - official documentation
*   [Encoding with the x264 codec](http://www.mplayerhq.hu/DOCS/HTML/en/menc-feat-x264.html) - MEncoder documentation
*   [H.264 encoding guide](http://avidemux.org/admWiki/doku.php?id=tutorial:h.264) - Avidemux wiki
*   [Using FFmpeg](http://howto-pages.org/ffmpeg/) - Linux how to pages
*   [List](http://ffmpeg.org/general.html#Supported-File-Formats-and-Codecs) of supported audio and video streams