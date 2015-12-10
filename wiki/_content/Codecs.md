# Codecs

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Optical disc drive#DVD playing](/index.php/Optical_disc_drive#DVD_playing "Optical disc drive")
*   [GStreamer](/index.php/GStreamer "GStreamer")
*   [MPlayer](/index.php/MPlayer "MPlayer")
*   [VLC media player](/index.php/VLC_media_player "VLC media player")

From [Wikipedia](https://en.wikipedia.org/wiki/Codec "wikipedia:Codec"):

_A codec is a device or computer program capable of encoding and/or decoding a digital data stream or signal._

In general, codecs are utilized by multimedia applications to encode or decode audio or video streams. In order to play encoded streams, users must ensure an appropriate codec is installed.

This article deals only with codecs and application backends; see [List of Applications](/index.php/List_of_applications#Multimedia "List of applications") for a list of media players ([MPlayer](/index.php/MPlayer "MPlayer"), [mpv](/index.php/Mpv "Mpv") and [VLC](/index.php/VLC "VLC") are popular choices).

## Contents

*   [1 Requirements](#Requirements)
*   [2 List of codecs](#List_of_codecs)
*   [3 Backends](#Backends)
    *   [3.1 GStreamer](#GStreamer)
    *   [3.2 xine](#xine)
    *   [3.3 libavcodec](#libavcodec)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Install MPlayer binary codecs](#Install_MPlayer_binary_codecs)
    *   [4.2 No H264, mpg4 or Musepack (.mpc) in Totem Player](#No_H264.2C_mpg4_or_Musepack_.28.mpc.29_in_Totem_Player)

## Requirements

Playing multimedia content requires two components:

*   A capable media player
*   The appropriate codec

It is not always necessary to explicitly install codecs if you have installed a media player. For example, [MPlayer](/index.php/MPlayer "MPlayer") pulls in a large number of codecs as dependencies, and also has codecs built in.

## List of codecs

*   **[ALAC](https://en.wikipedia.org/wiki/ALAC "wikipedia:ALAC")** — Data compression method which reduces the size of audio files with no loss of information.

[https://alac.macosforge.org/](https://alac.macosforge.org/) || [alac-svn](https://aur.archlinux.org/packages/alac-svn/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/alac-svn)]</sup>

*   **[CELT](https://en.wikipedia.org/wiki/CELT "wikipedia:CELT")** — Compression algorithm for audio. Like MP3, Vorbis, and AAC it is suitable for transmitting music with high quality. Unlike these formats CELT imposes very little delay on the signal, even less than is typical for speech centric formats like Speex, GSM, or G.729\.

[http://www.celt-codec.org/](http://www.celt-codec.org/) || [celt](https://www.archlinux.org/packages/?name=celt)

*   **[Daala](https://en.wikipedia.org/wiki/Daala "wikipedia:Daala")** — New video compression technology. The effort is a collaboration between Mozilla Foundation, Xiph.Org Foundation and other contributors. The goal of the project is to provide a free to implement, use and distribute digital media format and reference implementation with technical performance superior to h.265.

[https://www.xiph.org/daala/](https://www.xiph.org/daala/) || [libdaala-git](https://aur.archlinux.org/packages/libdaala-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/libdaala-git)]</sup>

*   **[FAAC](https://en.wikipedia.org/wiki/FAAC "wikipedia:FAAC")** — Proprietary AAC audio encoder.

[http://www.audiocoding.com/faac.html](http://www.audiocoding.com/faac.html) || [faac](https://www.archlinux.org/packages/?name=faac)

*   **[FAAD2](https://en.wikipedia.org/wiki/FAAD2 "wikipedia:FAAD2")** — ISO AAC audio decoder.

[http://www.audiocoding.com/faad2.html](http://www.audiocoding.com/faad2.html) || [faad2](https://www.archlinux.org/packages/?name=faad2)

*   **[FLAC](https://en.wikipedia.org/wiki/FLAC "wikipedia:FLAC")** — Free Lossless Audio Codec.

[https://xiph.org/flac/](https://xiph.org/flac/) || [flac](https://www.archlinux.org/packages/?name=flac)

*   **[Fraunhofer FDK AAC](https://en.wikipedia.org/wiki/FAAD2 "wikipedia:FAAD2")** — Complete, high-quality audio solution to Android (and Linux) users.

[http://www.iis.fraunhofer.de/en/bf/amm/implementierungen/fdkaaccodec.html](http://www.iis.fraunhofer.de/en/bf/amm/implementierungen/fdkaaccodec.html) || [libfdk-aac-git](https://aur.archlinux.org/packages/libfdk-aac-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/libfdk-aac-git)]</sup>

*   **[JasPer](https://en.wikipedia.org/wiki/JasPer "wikipedia:JasPer")** — Software-based implementation of the codec specified in the emerging JPEG-2000 Part-1 standard.

[http://www.ece.uvic.ca/~frodo/jasper/](http://www.ece.uvic.ca/~frodo/jasper/) || [jasper](https://www.archlinux.org/packages/?name=jasper)

*   **[LAME](https://en.wikipedia.org/wiki/LAME "wikipedia:LAME")** — MP3 encoder and graphical frame analyzer.

[http://lame.sourceforge.net/](http://lame.sourceforge.net/) || [lame](https://www.archlinux.org/packages/?name=lame)

*   **liba52** — Free library for decoding ATSC A/52 streams.

[http://liba52.sourceforge.net/](http://liba52.sourceforge.net/) || [a52dec](https://www.archlinux.org/packages/?name=a52dec)

*   **[libdca](https://en.wikipedia.org/wiki/libdca "wikipedia:libdca")** — Free library for decoding DTS Coherent Acoustics streams.

[https://www.videolan.org/developers/libdca.html](https://www.videolan.org/developers/libdca.html) || [libdca](https://www.archlinux.org/packages/?name=libdca)

*   **libde265** — Open source implementation of the h.265 video codec.

[https://github.com/strukturag/libde265](https://github.com/strukturag/libde265) || [libde265](https://aur.archlinux.org/packages/libde265/)<sup><small>AUR</small></sup> [libde265-git](https://aur.archlinux.org/packages/libde265-git/)<sup><small>AUR</small></sup>

*   **[libdv](https://en.wikipedia.org/wiki/DV "wikipedia:DV")** — The Quasar DV codec (libdv) is a software codec for DV video.

[http://libdv.sourceforge.net/](http://libdv.sourceforge.net/) || [libdv](https://www.archlinux.org/packages/?name=libdv)

*   **[libmpeg2](https://en.wikipedia.org/wiki/libmpeg2 "wikipedia:libmpeg2")** — Library for decoding MPEG-1 and MPEG-2 video streams.

[http://libmpeg2.sourceforge.net/](http://libmpeg2.sourceforge.net/) || [libmpeg2](https://www.archlinux.org/packages/?name=libmpeg2)

*   **[MAD](https://en.wikipedia.org/wiki/libmad "wikipedia:libmad")** — High-quality MPEG audio decoder.

[http://www.underbit.com/products/mad/](http://www.underbit.com/products/mad/) || [libmad](https://www.archlinux.org/packages/?name=libmad)

*   **[Musepack](https://en.wikipedia.org/wiki/Musepack "wikipedia:Musepack")** — Audio compression format with a strong emphasis on high quality. It's not lossless, but it is designed for transparency, so that you won't be able to hear differences between the original wave file and the much smaller MPC file. It is based on the MPEG-1 Layer-2 / MP2 algorithms, but since 1997 it has rapidly developed and vastly improved and is now at an advanced stage in which it contains heavily optimized and patentless code.

[http://musepack.net/](http://musepack.net/) || [libmpcdec](https://www.archlinux.org/packages/?name=libmpcdec)

*   **[Nero AAC](https://en.wikipedia.org/wiki/Advanced_Audio_Coding "wikipedia:Advanced Audio Coding")** — AAC audio codec (decode/encode/tag) all-in-one.

[http://www.nero.com/eng/company/about-nero/nero-aac-codec.php](http://www.nero.com/eng/company/about-nero/nero-aac-codec.php) || [neroaac](https://aur.archlinux.org/packages/neroaac/)<sup><small>AUR</small></sup>

*   **[opencore-amr](https://en.wikipedia.org/wiki/Adaptive_Multi-Rate_audio_codec "wikipedia:Adaptive Multi-Rate audio codec")** — Open source implementation of the Adaptive Multi Rate (AMR) speech codec.

[http://sourceforge.net/projects/opencore-amr/](http://sourceforge.net/projects/opencore-amr/) || [opencore-amr](https://www.archlinux.org/packages/?name=opencore-amr)

*   **[Opus](https://en.wikipedia.org/wiki/Opus_(audio_codec) "wikipedia:Opus (audio codec)")** — Totally open, royalty-free, highly versatile audio codec. Opus is unmatched for interactive speech and music transmission over the Internet, but is also intended for storage and streaming applications. It is standardized by the Internet Engineering Task Force (IETF) as [RFC 6716](//tools.ietf.org/html/rfc6716) which incorporated technology from Skype's SILK codec and Xiph.Org's CELT codec.

[http://www.opus-codec.org/](http://www.opus-codec.org/) || [opus](https://www.archlinux.org/packages/?name=opus) [opus-git](https://aur.archlinux.org/packages/opus-git/)<sup><small>AUR</small></sup>

*   **[Schrödinger](https://en.wikipedia.org/wiki/Dirac_(video_compression_format) "wikipedia:Dirac (video compression format)")** — Advanced royalty-free video compression format designed for a wide range of uses, from delivering low-resolution web content to broadcasting HD and beyond, to near-lossless studio editing.

[http://diracvideo.org/](http://diracvideo.org/) || [schroedinger](https://www.archlinux.org/packages/?name=schroedinger)

*   **[Speex](https://en.wikipedia.org/wiki/Speex "wikipedia:Speex")** — Patent-free audio compression format designed for speech.

[http://www.speex.org/](http://www.speex.org/) || [speex](https://www.archlinux.org/packages/?name=speex)

*   **[Theora](https://en.wikipedia.org/wiki/Theora "wikipedia:Theora")** — Open video codec developed by the Xiph.org.

[http://www.theora.org/](http://www.theora.org/) || [libtheora](https://www.archlinux.org/packages/?name=libtheora)

*   **[Vorbis](https://en.wikipedia.org/wiki/Vorbis "wikipedia:Vorbis")** — Completely open, patent-free, professional audio encoding and streaming technology.

[http://www.vorbis.com/](http://www.vorbis.com/) || [libvorbis](https://www.archlinux.org/packages/?name=libvorbis)

*   **[VP8](https://en.wikipedia.org/wiki/VP8 "wikipedia:VP8")** — High-quality, open video format for the web that's freely available to everyone.

[http://www.webmproject.org](http://www.webmproject.org) || [libvpx](https://www.archlinux.org/packages/?name=libvpx) [libvpx-git](https://aur.archlinux.org/packages/libvpx-git/)<sup><small>AUR</small></sup>

*   **[WavPack](https://en.wikipedia.org/wiki/WavPack "wikipedia:WavPack")** — Audio compression format with lossless, lossy, and hybrid compression modes.

[http://www.wavpack.com/](http://www.wavpack.com/) || [wavpack](https://www.archlinux.org/packages/?name=wavpack)

*   **[x264](https://en.wikipedia.org/wiki/x264 "wikipedia:x264")** — Free library for encoding H264/AVC video streams.

[https://www.videolan.org/developers/x264.html](https://www.videolan.org/developers/x264.html) || [x264](https://www.archlinux.org/packages/?name=x264) [x264-git](https://aur.archlinux.org/packages/x264-git/)<sup><small>AUR</small></sup>

*   **[x265](https://en.wikipedia.org/wiki/x265 "wikipedia:x265")** — Open-source project and free application library for encoding video streams into the H.265/High Efficiency Video Coding (HEVC) format.

[http://x265.org/](http://x265.org/) || [x265](https://www.archlinux.org/packages/?name=x265) [x265-hg](https://aur.archlinux.org/packages/x265-hg/)<sup><small>AUR</small></sup>

*   **[Xvid](https://en.wikipedia.org/wiki/Xvid "wikipedia:Xvid")** — Open source MPEG-4 video codec.

[http://www.xvid.org/](http://www.xvid.org/) || [xvidcore](https://www.archlinux.org/packages/?name=xvidcore)

## Backends

### GStreamer

From [http://www.gstreamer.net/](http://www.gstreamer.net/):

_GStreamer is a library for constructing graphs of media-handling components. The applications supports range from simple Ogg/Vorbis playback, audio/video streaming to complex audio (mixing) and video (non-linear editing) processing._

Simply, GStreamer is a _backend_ or _framework_ utilized by many media applications. See [GStreamer](/index.php/GStreamer "GStreamer") article.

### xine

From [http://www.xine-project.org/about](http://www.xine-project.org/about):

_xine is a free (gpl-licensed) high-performance, portable and reusable multimedia playback engine. xine itself is a shared library with an easy to use, yet powerful API which is used by many applications for smooth video playback and video processing purposes._

As an alternative to GStreamer, many media players can be configured to utilize the xine backend provided by [xine-lib](https://www.archlinux.org/packages/?name=xine-lib).

Note that the xine project itself provides a capable video player, [xine-ui](https://www.archlinux.org/packages/?name=xine-ui).

### libavcodec

[libavcodec](/index.php/FFmpeg "FFmpeg") is part of the [FFmpeg](http://ffmpeg.org/) project. It includes a large number of video and audio codecs. The libavcodec codecs are included with media players such as [MPlayer](/index.php/MPlayer "MPlayer") and [VLC](/index.php/VLC "VLC"), so you may not need to install the [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) package itself.

## Tips and tricks

### Install MPlayer binary codecs

As an ultimate solution, you can try to install MPlayer binary codecs.

If you are not able to play some files go to [http://www.mplayerhq.hu/design7/dload.html](http://www.mplayerhq.hu/design7/dload.html), read the instructions and install the codec you need to play your files.

They can also be found in AUR with the name [codecs](https://aur.archlinux.org/packages/codecs/)<sup><small>AUR</small></sup> and [codecs64](https://aur.archlinux.org/packages/codecs64/)<sup><small>AUR</small></sup>.

### No H264, mpg4 or Musepack (.mpc) in Totem Player

If you see the "The H264 plugin is missing" warning with Totem media player, just install the Gstreamer libav library to fix it install [gst-libav](https://www.archlinux.org/packages/?name=gst-libav).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Codecs&oldid=392015](https://wiki.archlinux.org/index.php?title=Codecs&oldid=392015)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Multimedia](/index.php/Category:Multimedia "Category:Multimedia")