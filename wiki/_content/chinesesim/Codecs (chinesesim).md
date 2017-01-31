来自 [wikipedia](https://en.wikipedia.org/wiki/Codec "wikipedia:Codec"):

	*编解码器（codec）指的是一个能够对一个信号或者一个数据流进行变换的设备或者程序。*

通常来说，编解码器被多媒体应用程序用来编码或解码音频视频流。为了播放编码过的流媒体，用户必须确保安装了合适的编解码器。

本文仅仅关心解码器和应用程序后端。参见 [Common Applications](/index.php/Common_Applications#Multimedia "Common Applications") 查看媒体播放器列表 ([MPlayer](/index.php/MPlayer_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "MPlayer (简体中文)") 和 [VLC](/index.php/VLC_media_player "VLC media player") 是常用的选择。)

## Contents

*   [1 需求条件](#.E9.9C.80.E6.B1.82.E6.9D.A1.E4.BB.B6)
*   [2 常用编解码器](#.E5.B8.B8.E7.94.A8.E7.BC.96.E8.A7.A3.E7.A0.81.E5.99.A8)
*   [3 后端](#.E5.90.8E.E7.AB.AF)
    *   [3.1 GStreamer](#GStreamer)
    *   [3.2 xine](#xine)
    *   [3.3 libavcodec](#libavcodec)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Install MPlayer binary codecs](#Install_MPlayer_binary_codecs)

## 需求条件

播放多媒体内容需要两个组件：

*   一个合适的媒体播放器
*   合适的解码器

如果你安装了一个媒体播放器，通常不需要特意的安装解码器。如 [MPlayer](/index.php/MPlayer "MPlayer") 包含了大量的解码器作为依赖，同时也内嵌了一些解码器。

## 常用编解码器

*   [a52dec](https://www.archlinux.org/packages/?name=a52dec): liba52 is a free library for decoding ATSC A/52 streams
*   [faac](https://www.archlinux.org/packages/?name=faac): FAAC is an AAC audio encoder
*   [faad2](https://www.archlinux.org/packages/?name=faad2): ISO AAC audio decoder
*   [flac](https://www.archlinux.org/packages/?name=flac): Free Lossless Audio Codec
*   [jasper](https://www.archlinux.org/packages/?name=jasper): A software-based implementation of the codec specified in the emerging JPEG-2000 Part-1 standard
*   [lame](https://www.archlinux.org/packages/?name=lame): An MP3 encoder and graphical frame analyzer
*   [libdca](https://www.archlinux.org/packages/?name=libdca): Free library for decoding DTS Coherent Acoustics streams
*   [libdv](https://www.archlinux.org/packages/?name=libdv): The Quasar DV codec (libdv) is a software codec for DV video
*   [libmad](https://www.archlinux.org/packages/?name=libmad): A high-quality MPEG audio decoder
*   [libmpeg2](https://www.archlinux.org/packages/?name=libmpeg2): libmpeg2 is a library for decoding MPEG-1 and MPEG-2 video streams
*   [libtheora](https://www.archlinux.org/packages/?name=libtheora): An open video codec developed by the Xiph.org
*   [libvorbis](https://www.archlinux.org/packages/?name=libvorbis): Vorbis codec library
*   [libxv](https://www.archlinux.org/packages/?name=libxv): X11 Video extension library
*   [wavpack](https://www.archlinux.org/packages/?name=wavpack): Audio compression format with lossless, lossy, and hybrid compression modes
*   [x264](https://www.archlinux.org/packages/?name=x264): Free library for encoding H264/AVC video streams
*   [xvidcore](https://www.archlinux.org/packages/?name=xvidcore): XviD is an open source MPEG-4 video codec

## 后端

### GStreamer

From [http://www.gstreamer.net/](http://www.gstreamer.net/):

	*[GStreamer](/index.php/GStreamer "GStreamer") is a library for constructing graphs of media-handling components. The applications it supports range from simple Ogg/Vorbis playback, audio/video streaming to complex audio (mixing) and video (non-linear editing) processing.*

Simply, GStreamer is a *backend* or *framework* utilized by many media players.

GStreamer uses a plugin architecture which makes the most of GStreamer's functionality implemented as shared libraries. Since version 0.10 the plugins come grouped into three sets (named after the film The Good, the Bad and the Ugly).[wikipedia:GStreamer](https://en.wikipedia.org/wiki/GStreamer "wikipedia:GStreamer")

*   [gstreamer0.10-base-plugins](https://aur.archlinux.org/packages/gstreamer0.10-base-plugins/)
*   [gstreamer0.10-good-plugins](https://aur.archlinux.org/packages/gstreamer0.10-good-plugins/)
*   [gstreamer0.10-bad-plugins](https://aur.archlinux.org/packages/gstreamer0.10-bad-plugins/)
*   [gstreamer0.10-ugly-plugins](https://aur.archlinux.org/packages/gstreamer0.10-ugly-plugins/)
*   [gstreamer0.10-ffmpeg](https://aur.archlinux.org/packages/gstreamer0.10-ffmpeg/)

For the most complete solution:

```
# pacman -S gstreamer0.10-plugins

```

### xine

From [http://www.xine-project.org/about](http://www.xine-project.org/about):

	*xine is a free (gpl-licensed) high-performance, portable and reusable multimedia playback engine. xine itself is a shared library with an easy to use, yet powerful API which is used by many applications for smooth video playback and video processing purposes.*

As an alternative to GStreamer, many media players can be configured to utilize the xine backend:

```
# pacman -S xine-lib

```

Note that the xine project itself provides a capable video player, [xine-ui](https://www.archlinux.org/packages/?name=xine-ui).

### libavcodec

libavcodec is part of the [FFmpeg](http://ffmpeg.org/) project. It includes a large number of video and audio codecs. The libavcodec codecs are included with media players such as [MPlayer](/index.php/MPlayer "MPlayer") and [VLC](/index.php/VLC "VLC"), so you may not need to install the [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) package itself.

## Tips and tricks

### Install MPlayer binary codecs

As an ultimate solution, you can try to install MPlayer binary codecs.

If you are not able to play some files go to [http://www.mplayerhq.hu/design7/dload.html](http://www.mplayerhq.hu/design7/dload.html), read the instructions and install the codec you need to play your files.

They can also be found in AUR with the name [codecs](https://aur.archlinux.org/packages/codecs/).