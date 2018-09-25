相关文章

*   [DVD Playing](/index.php/DVD_Playing "DVD Playing")
*   [GStreamer](/index.php/GStreamer "GStreamer")
*   [MPlayer](/index.php/MPlayer_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "MPlayer (简体中文)")
*   [VLC media player](/index.php/VLC_media_player "VLC media player")

**翻译状态：** 本文是英文页面 [Codecs](/index.php/Codecs "Codecs") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-12-04，点击[这里](https://wiki.archlinux.org/index.php?title=Codecs&diff=0&oldid=495092)可以查看翻译后英文页面的改动。

来自 [wikipedia](https://en.wikipedia.org/wiki/Codec "wikipedia:Codec"):

	*编解码器（codec）指的是一个能够对一个信号或者一个数据流进行变换的设备或者程序。*

通常来说，编解码器被多媒体应用程序用来编码或解码音频视频流。为了播放编码过的流媒体，用户必须确保安装了合适的编解码器。

本文仅仅关心解码器和应用程序后端。[这里](/index.php/Common_Applications#Multimedia "Common Applications")包含媒体播放器的列表。[MPlayer](/index.php/MPlayer_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "MPlayer (简体中文)") 和 [VLC](/index.php/VLC_media_player "VLC media player") 是常用的选择。

## Contents

*   [1 需求条件](#.E9.9C.80.E6.B1.82.E6.9D.A1.E4.BB.B6)
*   [2 常用编解码器](#.E5.B8.B8.E7.94.A8.E7.BC.96.E8.A7.A3.E7.A0.81.E5.99.A8)
*   [3 后端](#.E5.90.8E.E7.AB.AF)
    *   [3.1 GStreamer](#GStreamer)
    *   [3.2 xine](#xine)
    *   [3.3 libavcodec](#libavcodec)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Install MPlayer binary codecs](#Install_MPlayer_binary_codecs)
    *   [4.2 No H264, mpg4 or Musepack (.mpc) in Totem Player](#No_H264.2C_mpg4_or_Musepack_.28.mpc.29_in_Totem_Player)

## 需求条件

播放多媒体内容需要两个组件：

*   一个合适的媒体播放器
*   合适的解码器

如果你安装了一个媒体播放器，通常不需要特意的安装解码器。如 [MPlayer](/index.php/MPlayer "MPlayer") 包含了大量的解码器作为依赖，同时也内嵌了一些解码器。

## 常用编解码器

*   **[ALAC](https://en.wikipedia.org/wiki/ALAC "wikipedia:ALAC")** — Data compression method which reduces the size of audio files with no loss of information.

	[https://alac.macosforge.org/](https://alac.macosforge.org/) || [alac-git](https://aur.archlinux.org/packages/alac-git/)

*   **[CELT](https://en.wikipedia.org/wiki/CELT "wikipedia:CELT")** — Compression algorithm for audio. Like MP3, Vorbis, and AAC it is suitable for transmitting music with high quality. Unlike these formats CELT imposes very little delay on the signal, even less than is typical for speech centric formats like Speex, GSM, or G.729.

	[http://www.celt-codec.org/](http://www.celt-codec.org/) || [celt](https://www.archlinux.org/packages/?name=celt)

*   **[Daala](https://en.wikipedia.org/wiki/Daala "wikipedia:Daala")** — New video compression technology. The effort is a collaboration between Mozilla Foundation, Xiph.Org Foundation and other contributors. The goal of the project is to provide a free to implement, use and distribute digital media format and reference implementation with technical performance superior to h.265.

	[https://www.xiph.org/daala/](https://www.xiph.org/daala/) || [daala-git](https://aur.archlinux.org/packages/daala-git/)

*   **[FAAC](https://en.wikipedia.org/wiki/FAAC "wikipedia:FAAC")** — Proprietary AAC audio encoder.

	[http://www.audiocoding.com/faac.html](http://www.audiocoding.com/faac.html) || [faac](https://www.archlinux.org/packages/?name=faac)

*   **[FAAD2](https://en.wikipedia.org/wiki/FAAD2 "wikipedia:FAAD2")** — ISO AAC audio decoder.

	[http://www.audiocoding.com/faad2.html](http://www.audiocoding.com/faad2.html) || [faad2](https://www.archlinux.org/packages/?name=faad2)

*   **[FLAC](https://en.wikipedia.org/wiki/FLAC "wikipedia:FLAC")** — Free Lossless Audio Codec.

	[https://xiph.org/flac/](https://xiph.org/flac/) || [flac](https://www.archlinux.org/packages/?name=flac)

*   **[Fraunhofer FDK AAC](https://en.wikipedia.org/wiki/FAAD2 "wikipedia:FAAD2")** — Complete, high-quality audio solution to Android (and Linux) users.

	[http://www.iis.fraunhofer.de/en/bf/amm/implementierungen/fdkaaccodec.html](http://www.iis.fraunhofer.de/en/bf/amm/implementierungen/fdkaaccodec.html) || [libfdk-aac](https://www.archlinux.org/packages/?name=libfdk-aac)

*   **[JasPer](https://en.wikipedia.org/wiki/JasPer "wikipedia:JasPer")** — Software-based implementation of the codec specified in the emerging JPEG-2000 Part-1 standard.

	[http://www.ece.uvic.ca/~frodo/jasper/](http://www.ece.uvic.ca/~frodo/jasper/) || [jasper](https://www.archlinux.org/packages/?name=jasper)

*   **[LAME](https://en.wikipedia.org/wiki/LAME "wikipedia:LAME")** — MP3 encoder and graphical frame analyzer.

	[http://lame.sourceforge.net/](http://lame.sourceforge.net/) || [lame](https://www.archlinux.org/packages/?name=lame)

*   **liba52** — Free library for decoding ATSC A/52 streams.

	[http://liba52.sourceforge.net/](http://liba52.sourceforge.net/) || [a52dec](https://www.archlinux.org/packages/?name=a52dec)

*   **[libdca](https://en.wikipedia.org/wiki/libdca "wikipedia:libdca")** — Free library for decoding DTS Coherent Acoustics streams.

	[https://www.videolan.org/developers/libdca.html](https://www.videolan.org/developers/libdca.html) || [libdca](https://www.archlinux.org/packages/?name=libdca)

*   **libde265** — Open source implementation of the h.265 video codec.

	[https://github.com/strukturag/libde265](https://github.com/strukturag/libde265) || [libde265](https://www.archlinux.org/packages/?name=libde265) [libde265-git](https://aur.archlinux.org/packages/libde265-git/)

*   **[libdv](https://en.wikipedia.org/wiki/DV "wikipedia:DV")** — The Quasar DV codec (libdv) is a software codec for DV video.

	[http://libdv.sourceforge.net/](http://libdv.sourceforge.net/) || [libdv](https://www.archlinux.org/packages/?name=libdv)

*   **[libmpeg2](https://en.wikipedia.org/wiki/libmpeg2 "wikipedia:libmpeg2")** — Library for decoding MPEG-1 and MPEG-2 video streams.

	[http://libmpeg2.sourceforge.net/](http://libmpeg2.sourceforge.net/) || [libmpeg2](https://www.archlinux.org/packages/?name=libmpeg2)

*   **[MAD](https://en.wikipedia.org/wiki/libmad "wikipedia:libmad")** — High-quality MPEG audio decoder.

	[http://www.underbit.com/products/mad/](http://www.underbit.com/products/mad/) || [libmad](https://www.archlinux.org/packages/?name=libmad)

*   **[Musepack](https://en.wikipedia.org/wiki/Musepack "wikipedia:Musepack")** — Audio compression format with a strong emphasis on high quality. It's not lossless, but it is designed for transparency, so that you won't be able to hear differences between the original wave file and the much smaller MPC file. It is based on the MPEG-1 Layer-2 / MP2 algorithms, but since 1997 it has rapidly developed and vastly improved and is now at an advanced stage in which it contains heavily optimized and patentless code.

	[http://musepack.net/](http://musepack.net/) || [libmpcdec](https://www.archlinux.org/packages/?name=libmpcdec)

*   **[Nero AAC](https://en.wikipedia.org/wiki/Advanced_Audio_Coding "wikipedia:Advanced Audio Coding")** — AAC audio codec (decode/encode/tag) all-in-one.

	[http://www.nero.com/eng/company/about-nero/nero-aac-codec.php](http://www.nero.com/eng/company/about-nero/nero-aac-codec.php) || [neroaac](https://aur.archlinux.org/packages/neroaac/)

*   **[opencore-amr](https://en.wikipedia.org/wiki/Adaptive_Multi-Rate_audio_codec "wikipedia:Adaptive Multi-Rate audio codec")** — Open source implementation of the Adaptive Multi Rate (AMR) speech codec.

	[http://sourceforge.net/projects/opencore-amr/](http://sourceforge.net/projects/opencore-amr/) || [opencore-amr](https://www.archlinux.org/packages/?name=opencore-amr)

*   **[Opus](https://en.wikipedia.org/wiki/Opus_(audio_codec) "wikipedia:Opus (audio codec)")** — Totally open, royalty-free, highly versatile audio codec. Opus is unmatched for interactive speech and music transmission over the Internet, but is also intended for storage and streaming applications. It is standardized by the Internet Engineering Task Force (IETF) as RFC 6716 which incorporated technology from Skype's SILK codec and Xiph.Org's CELT codec.

	[http://www.opus-codec.org/](http://www.opus-codec.org/) || [opus](https://www.archlinux.org/packages/?name=opus) [opus-git](https://aur.archlinux.org/packages/opus-git/)

*   **[Schrödinger](https://en.wikipedia.org/wiki/Dirac_(video_compression_format) "wikipedia:Dirac (video compression format)")** — Advanced royalty-free video compression format designed for a wide range of uses, from delivering low-resolution web content to broadcasting HD and beyond, to near-lossless studio editing.

	[http://diracvideo.org/](http://diracvideo.org/) || [schroedinger](https://www.archlinux.org/packages/?name=schroedinger)

*   **[Speex](https://en.wikipedia.org/wiki/Speex "wikipedia:Speex")** — Patent-free audio compression format designed for speech.

	[http://www.speex.org/](http://www.speex.org/) || [speex](https://www.archlinux.org/packages/?name=speex)

*   **[Theora](https://en.wikipedia.org/wiki/Theora "wikipedia:Theora")** — Open video codec developed by the Xiph.org.

	[http://www.theora.org/](http://www.theora.org/) || [libtheora](https://www.archlinux.org/packages/?name=libtheora)

*   **[Vorbis](https://en.wikipedia.org/wiki/Vorbis "wikipedia:Vorbis")** — Completely open, patent-free, professional audio encoding and streaming technology.

	[http://www.vorbis.com/](http://www.vorbis.com/) || [libvorbis](https://www.archlinux.org/packages/?name=libvorbis)

*   **[VP8](https://en.wikipedia.org/wiki/VP8 "wikipedia:VP8")** — High-quality, open video format for the web that's freely available to everyone.

	[http://www.webmproject.org](http://www.webmproject.org) || [libvpx](https://www.archlinux.org/packages/?name=libvpx) [libvpx-git](https://aur.archlinux.org/packages/libvpx-git/)

*   **[WavPack](https://en.wikipedia.org/wiki/WavPack "wikipedia:WavPack")** — Audio compression format with lossless, lossy, and hybrid compression modes.

	[http://www.wavpack.com/](http://www.wavpack.com/) || [wavpack](https://www.archlinux.org/packages/?name=wavpack)

*   **[x264](https://en.wikipedia.org/wiki/x264 "wikipedia:x264")** — Free library for encoding H264/AVC video streams.

	[https://www.videolan.org/developers/x264.html](https://www.videolan.org/developers/x264.html) || [x264](https://www.archlinux.org/packages/?name=x264) [x264-git](https://aur.archlinux.org/packages/x264-git/)

*   **[x265](https://en.wikipedia.org/wiki/x265 "wikipedia:x265")** — Open-source project and free application library for encoding video streams into the H.265/High Efficiency Video Coding (HEVC) format.

	[http://x265.org/](http://x265.org/) || [x265](https://www.archlinux.org/packages/?name=x265) [x265-hg](https://aur.archlinux.org/packages/x265-hg/)

*   **[Xvid](https://en.wikipedia.org/wiki/Xvid "wikipedia:Xvid")** — Open source MPEG-4 video codec.

	[http://www.xvid.org/](http://www.xvid.org/) || [xvidcore](https://www.archlinux.org/packages/?name=xvidcore)

## 后端

### GStreamer

From [http://www.gstreamer.net/](http://www.gstreamer.net/):

	GStreamer is a library for constructing graphs of media-handling components. The applications supports range from simple Ogg/Vorbis playback, audio/video streaming to complex audio (mixing) and video (non-linear editing) processing.

Simply, GStreamer is a *backend* or *framework* utilized by many media applications. See [GStreamer](/index.php/GStreamer "GStreamer") article.

### xine

From [http://www.xine-project.org/about](http://www.xine-project.org/about):

	xine is a free (gpl-licensed) high-performance, portable and reusable multimedia playback engine. xine itself is a shared library with an easy to use, yet powerful API which is used by many applications for smooth video playback and video processing purposes.

As an alternative to GStreamer, many media players can be configured to utilize the xine backend provided by [xine-lib](https://www.archlinux.org/packages/?name=xine-lib).

Note that the xine project itself provides a capable video player, [xine-ui](https://www.archlinux.org/packages/?name=xine-ui).

### libavcodec

[libavcodec](/index.php/FFmpeg "FFmpeg") is part of the [FFmpeg](http://ffmpeg.org/) project. It includes a large number of video and audio codecs. The libavcodec codecs are included with media players such as [MPlayer](/index.php/MPlayer "MPlayer") and [VLC](/index.php/VLC "VLC"), so you may not need to install the [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) package itself.

## Tips and tricks

### Install MPlayer binary codecs

As an ultimate solution, you can try to install MPlayer binary codecs.

If you are not able to play some files go to [http://www.mplayerhq.hu/design7/dload.html](http://www.mplayerhq.hu/design7/dload.html), read the instructions and install the codec you need to play your files.

They can also be found in the [codecs](https://aur.archlinux.org/packages/codecs/) and [codecs64](https://aur.archlinux.org/packages/codecs64/) packages.

### No H264, mpg4 or Musepack (.mpc) in Totem Player

If you see the "The H264 plugin is missing" warning with Totem media player, just install the Gstreamer libav library to fix it install [gst-libav](https://www.archlinux.org/packages/?name=gst-libav).