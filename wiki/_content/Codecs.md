# Codecs

Related articles

*   [Optical disc drive#DVD playing](/index.php/Optical_disc_drive#DVD_playing "Optical disc drive")
*   [GStreamer](/index.php/GStreamer "GStreamer")
*   [MPlayer](/index.php/MPlayer "MPlayer")
*   [VLC media player](/index.php/VLC_media_player "VLC media player")

From [Wikipedia](https://en.wikipedia.org/wiki/Codec "wikipedia:Codec"):

NaN

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

NaN

*   **[CELT](https://en.wikipedia.org/wiki/CELT "wikipedia:CELT")** — Compression algorithm for audio. Like MP3, Vorbis, and AAC it is suitable for transmitting music with high quality. Unlike these formats CELT imposes very little delay on the signal, even less than is typical for speech centric formats like Speex, GSM, or G.729\.

NaN

*   **[Daala](https://en.wikipedia.org/wiki/Daala "wikipedia:Daala")** — New video compression technology. The effort is a collaboration between Mozilla Foundation, Xiph.Org Foundation and other contributors. The goal of the project is to provide a free to implement, use and distribute digital media format and reference implementation with technical performance superior to h.265.

NaN

*   **[FAAC](https://en.wikipedia.org/wiki/FAAC "wikipedia:FAAC")** — Proprietary AAC audio encoder.

NaN

*   **[FAAD2](https://en.wikipedia.org/wiki/FAAD2 "wikipedia:FAAD2")** — ISO AAC audio decoder.

NaN

*   **[FLAC](https://en.wikipedia.org/wiki/FLAC "wikipedia:FLAC")** — Free Lossless Audio Codec.

NaN

*   **[Fraunhofer FDK AAC](https://en.wikipedia.org/wiki/FAAD2 "wikipedia:FAAD2")** — Complete, high-quality audio solution to Android (and Linux) users.

NaN

*   **[JasPer](https://en.wikipedia.org/wiki/JasPer "wikipedia:JasPer")** — Software-based implementation of the codec specified in the emerging JPEG-2000 Part-1 standard.

NaN

*   **[LAME](https://en.wikipedia.org/wiki/LAME "wikipedia:LAME")** — MP3 encoder and graphical frame analyzer.

NaN

*   **liba52** — Free library for decoding ATSC A/52 streams.

NaN

*   **[libdca](https://en.wikipedia.org/wiki/libdca "wikipedia:libdca")** — Free library for decoding DTS Coherent Acoustics streams.

NaN

*   **libde265** — Open source implementation of the h.265 video codec.

NaN

*   **[libdv](https://en.wikipedia.org/wiki/DV "wikipedia:DV")** — The Quasar DV codec (libdv) is a software codec for DV video.

NaN

*   **[libmpeg2](https://en.wikipedia.org/wiki/libmpeg2 "wikipedia:libmpeg2")** — Library for decoding MPEG-1 and MPEG-2 video streams.

NaN

*   **[MAD](https://en.wikipedia.org/wiki/libmad "wikipedia:libmad")** — High-quality MPEG audio decoder.

NaN

*   **[Musepack](https://en.wikipedia.org/wiki/Musepack "wikipedia:Musepack")** — Audio compression format with a strong emphasis on high quality. It's not lossless, but it is designed for transparency, so that you won't be able to hear differences between the original wave file and the much smaller MPC file. It is based on the MPEG-1 Layer-2 / MP2 algorithms, but since 1997 it has rapidly developed and vastly improved and is now at an advanced stage in which it contains heavily optimized and patentless code.

NaN

*   **[Nero AAC](https://en.wikipedia.org/wiki/Advanced_Audio_Coding "wikipedia:Advanced Audio Coding")** — AAC audio codec (decode/encode/tag) all-in-one.

NaN

*   **[opencore-amr](https://en.wikipedia.org/wiki/Adaptive_Multi-Rate_audio_codec "wikipedia:Adaptive Multi-Rate audio codec")** — Open source implementation of the Adaptive Multi Rate (AMR) speech codec.

NaN

*   **[Opus](https://en.wikipedia.org/wiki/Opus_(audio_codec) "wikipedia:Opus (audio codec)")** — Totally open, royalty-free, highly versatile audio codec. Opus is unmatched for interactive speech and music transmission over the Internet, but is also intended for storage and streaming applications. It is standardized by the Internet Engineering Task Force (IETF) as [RFC 6716](//tools.ietf.org/html/rfc6716) which incorporated technology from Skype's SILK codec and Xiph.Org's CELT codec.

NaN

*   **[Schrödinger](https://en.wikipedia.org/wiki/Dirac_(video_compression_format) "wikipedia:Dirac (video compression format)")** — Advanced royalty-free video compression format designed for a wide range of uses, from delivering low-resolution web content to broadcasting HD and beyond, to near-lossless studio editing.

NaN

*   **[Speex](https://en.wikipedia.org/wiki/Speex "wikipedia:Speex")** — Patent-free audio compression format designed for speech.

NaN

*   **[Theora](https://en.wikipedia.org/wiki/Theora "wikipedia:Theora")** — Open video codec developed by the Xiph.org.

NaN

*   **[Vorbis](https://en.wikipedia.org/wiki/Vorbis "wikipedia:Vorbis")** — Completely open, patent-free, professional audio encoding and streaming technology.

NaN

*   **[VP8](https://en.wikipedia.org/wiki/VP8 "wikipedia:VP8")** — High-quality, open video format for the web that's freely available to everyone.

NaN

*   **[WavPack](https://en.wikipedia.org/wiki/WavPack "wikipedia:WavPack")** — Audio compression format with lossless, lossy, and hybrid compression modes.

NaN

*   **[x264](https://en.wikipedia.org/wiki/x264 "wikipedia:x264")** — Free library for encoding H264/AVC video streams.

NaN

*   **[x265](https://en.wikipedia.org/wiki/x265 "wikipedia:x265")** — Open-source project and free application library for encoding video streams into the H.265/High Efficiency Video Coding (HEVC) format.

NaN

*   **[Xvid](https://en.wikipedia.org/wiki/Xvid "wikipedia:Xvid")** — Open source MPEG-4 video codec.

NaN

## Backends

### GStreamer

From [http://www.gstreamer.net/](http://www.gstreamer.net/):

NaN

Simply, GStreamer is a _backend_ or _framework_ utilized by many media applications. See [GStreamer](/index.php/GStreamer "GStreamer") article.

### xine

From [http://www.xine-project.org/about](http://www.xine-project.org/about):

NaN

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