Related articles

*   [Optical disc drive#Playback](/index.php/Optical_disc_drive#Playback "Optical disc drive")
*   [GStreamer](/index.php/GStreamer "GStreamer")
*   [ffmpeg](/index.php/Ffmpeg "Ffmpeg")

From [Wikipedia](https://en.wikipedia.org/wiki/Codec "wikipedia:Codec"), "a codec is a device or computer program capable of encoding and/or decoding a digital data stream or signal."

In general, codecs are utilized by multimedia applications to encode or decode audio or video streams. In order to play encoded streams, users must ensure an appropriate codec is installed.

This article deals only with codecs and application backends; see [List of applications/Multimedia](/index.php/List_of_applications/Multimedia "List of applications/Multimedia") for a list of media players ([MPlayer](/index.php/MPlayer "MPlayer"), [mpv](/index.php/Mpv "Mpv") and [VLC](/index.php/VLC "VLC") are popular choices).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Requirements](#Requirements)
*   [2 List of codecs](#List_of_codecs)
    *   [2.1 Audio](#Audio)
        *   [2.1.1 Lossless audio codecs](#Lossless_audio_codecs)
        *   [2.1.2 Lossy audio codecs](#Lossy_audio_codecs)
            *   [2.1.2.1 AAC](#AAC)
    *   [2.2 Image codecs](#Image_codecs)
    *   [2.3 Video codecs](#Video_codecs)
*   [3 Container format tools](#Container_format_tools)
*   [4 Backends](#Backends)
    *   [4.1 GStreamer](#GStreamer)
    *   [4.2 xine](#xine)
    *   [4.3 libavcodec](#libavcodec)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Install MPlayer binary codecs](#Install_MPlayer_binary_codecs)
    *   [5.2 No H264, mpg4 or Musepack (.mpc) in Totem Player](#No_H264,_mpg4_or_Musepack_(.mpc)_in_Totem_Player)

## Requirements

Playing multimedia content requires two components:

*   A capable media player
*   The appropriate codec

It is not always necessary to explicitly install codecs if you have installed a media player. For example, [MPlayer](/index.php/MPlayer "MPlayer") pulls in a large number of codecs as dependencies, and also has codecs built in.

## List of codecs

### Audio

See also [Wikipedia:Comparison of audio coding formats](https://en.wikipedia.org/wiki/Comparison_of_audio_coding_formats "wikipedia:Comparison of audio coding formats").

#### Lossless audio codecs

*   **[Apple Lossless](https://en.wikipedia.org/wiki/Apple_Lossless "wikipedia:Apple Lossless") (ALAC)** — A lossless audio compression codec developed by Apple and deployed on all of its platforms and devices.

	[https://alac.macosforge.org/](https://alac.macosforge.org/) || [alac-git](https://aur.archlinux.org/packages/alac-git/)

*   **[FLAC](https://en.wikipedia.org/wiki/FLAC "wikipedia:FLAC")** — Free Lossless Audio Codec.

	[https://xiph.org/flac/](https://xiph.org/flac/) || [flac](https://www.archlinux.org/packages/?name=flac)

*   **[WavPack](https://en.wikipedia.org/wiki/WavPack "wikipedia:WavPack")** — Lossless audio compression format that also has a lossy [hybrid mode](https://en.wikipedia.org/wiki/WavPack#Hybrid_mode "wikipedia:WavPack").

	[http://www.wavpack.com/](http://www.wavpack.com/) || [wavpack](https://www.archlinux.org/packages/?name=wavpack)

#### Lossy audio codecs

| Codec | Encode | Decode |
| [AAC](https://en.wikipedia.org/wiki/Advanced_Audio_Coding "wikipedia:Advanced Audio Coding") | [#AAC](#AAC) |
| [ATSC A/52](https://en.wikipedia.org/wiki/ATSC_A/52 "wikipedia:ATSC A/52") | [aften](https://aur.archlinux.org/packages/aften/) | [a52dec](https://www.archlinux.org/packages/?name=a52dec) |
| [CELT](https://en.wikipedia.org/wiki/CELT "wikipedia:CELT") | [celt](https://www.archlinux.org/packages/?name=celt) |
| [MPEG-1](https://en.wikipedia.org/wiki/MPEG-1 "wikipedia:MPEG-1") | [libmad](https://www.archlinux.org/packages/?name=libmad) |
| [MP3](https://en.wikipedia.org/wiki/MP3 "wikipedia:MP3") | [lame](https://www.archlinux.org/packages/?name=lame) |
| [Musepack](https://en.wikipedia.org/wiki/Musepack "wikipedia:Musepack") (MPC) | –  | [libmpcdec](https://www.archlinux.org/packages/?name=libmpcdec) |
| [Opus](https://en.wikipedia.org/wiki/Opus_(audio_format) | [opus](https://www.archlinux.org/packages/?name=opus), [opus-git](https://aur.archlinux.org/packages/opus-git/) |
| [Vorbis](https://en.wikipedia.org/wiki/Vorbis "wikipedia:Vorbis") | [libvorbis](https://www.archlinux.org/packages/?name=libvorbis) |
| Speech codecs |
| [AMR](https://en.wikipedia.org/wiki/Adaptive_Multi-Rate_audio_codec "wikipedia:Adaptive Multi-Rate audio codec") | [opencore-amr](https://www.archlinux.org/packages/?name=opencore-amr) |
| [Speex](https://en.wikipedia.org/wiki/Speex "wikipedia:Speex") | [speex](https://www.archlinux.org/packages/?name=speex) |

1.  mppenc is not packaged.

*   **[CELT](https://en.wikipedia.org/wiki/CELT "wikipedia:CELT")** — Open, royalty-free lossy audio codec, optimized for low latency.

	[http://www.celt-codec.org/](http://www.celt-codec.org/) || [celt](https://www.archlinux.org/packages/?name=celt)

*   **[LAME](https://en.wikipedia.org/wiki/LAME "wikipedia:LAME")** — MP3 encoder and graphical frame analyzer.

	[http://lame.sourceforge.net/](http://lame.sourceforge.net/) || [lame](https://www.archlinux.org/packages/?name=lame)

*   **liba52** — Free library for decoding [ATSC A/52](https://en.wikipedia.org/wiki/ATSC_A/52 "wikipedia:ATSC A/52") (Dolby Digital) streams (lossy).

	[http://liba52.sourceforge.net/](http://liba52.sourceforge.net/) || [a52dec](https://www.archlinux.org/packages/?name=a52dec)

*   **[libdca](https://en.wikipedia.org/wiki/libdca "wikipedia:libdca")** — Free library for decoding DTS Coherent Acoustics streams.

	[https://www.videolan.org/developers/libdca.html](https://www.videolan.org/developers/libdca.html) || [libdca](https://www.archlinux.org/packages/?name=libdca)

*   **[MAD](https://en.wikipedia.org/wiki/libmad "wikipedia:libmad")** — High-quality MPEG audio decoder.

	[https://www.underbit.com/products/mad/](https://www.underbit.com/products/mad/) || [libmad](https://www.archlinux.org/packages/?name=libmad)

*   **[Musepack](https://en.wikipedia.org/wiki/Musepack "wikipedia:Musepack") (MPC)** — Open source lossy audio codec, designed for [transparency](https://en.wikipedia.org/wiki/Transparency_(data_compression) "wikipedia:Transparency (data compression)").

	[https://musepack.net/](https://musepack.net/) || [libmpcdec](https://www.archlinux.org/packages/?name=libmpcdec)

*   **[opencore-amr](https://en.wikipedia.org/wiki/Adaptive_Multi-Rate_audio_codec "wikipedia:Adaptive Multi-Rate audio codec")** — Open source implementation of the Adaptive Multi Rate (AMR) speech codec.

	[https://sourceforge.net/projects/opencore-amr/](https://sourceforge.net/projects/opencore-amr/) || [opencore-amr](https://www.archlinux.org/packages/?name=opencore-amr)

*   **[Opus](https://en.wikipedia.org/wiki/Opus_(audio_codec) "wikipedia:Opus (audio codec)")** — Open, royalty-free, lossy audio codec, designed for speech and general audio coding and low latency.

	[https://www.opus-codec.org/](https://www.opus-codec.org/) || [opus](https://www.archlinux.org/packages/?name=opus), [opus-git](https://aur.archlinux.org/packages/opus-git/)

*   **[Speex](https://en.wikipedia.org/wiki/Speex "wikipedia:Speex")** — Patent-free, lossy audio compression format designed for speech.

	[https://www.speex.org/](https://www.speex.org/) || [speex](https://www.archlinux.org/packages/?name=speex)

*   **[Vorbis](https://en.wikipedia.org/wiki/Vorbis "wikipedia:Vorbis")** — Open, patent-free, lossy audio codec.

	[https://xiph.org/vorbis/](https://xiph.org/vorbis/) || [libvorbis](https://www.archlinux.org/packages/?name=libvorbis)

##### AAC

From [Wikipedia](https://en.wikipedia.org/wiki/Advanced_Audio_Coding "wikipedia:Advanced Audio Coding"):

	**Advanced Audio Coding** (AAC) is a proprietary audio coding standard for lossy digital audio compression. Designed to be the successor of the MP3 format, AAC generally achieves better sound quality than MP3 at the same bit rate.

*   **[FAAC](https://en.wikipedia.org/wiki/FAAC "wikipedia:FAAC")** — Proprietary AAC audio encoder.

	[https://www.audiocoding.com/faac.html](https://www.audiocoding.com/faac.html) || [faac](https://www.archlinux.org/packages/?name=faac)

*   **[FAAD2](https://en.wikipedia.org/wiki/FAAD2 "wikipedia:FAAD2")** — ISO AAC audio decoder.

	[http://www.audiocoding.com/faad2.html](http://www.audiocoding.com/faad2.html) || [faad2](https://www.archlinux.org/packages/?name=faad2)

*   **[Fraunhofer FDK AAC](https://en.wikipedia.org/wiki/FAAD2 "wikipedia:FAAD2")** — Complete, high-quality audio solution to Android (and Linux) users.

	[http://www.iis.fraunhofer.de/en/bf/amm/implementierungen/fdkaaccodec.html](http://www.iis.fraunhofer.de/en/bf/amm/implementierungen/fdkaaccodec.html) || [libfdk-aac](https://www.archlinux.org/packages/?name=libfdk-aac)

*   **[Nero AAC](https://en.wikipedia.org/wiki/Nero_AAC_Codec "wikipedia:Nero AAC Codec")** — Nero AAC reference quality MPEG-4 and 3GPP audio codec. (deprecated)

	[https://www.nero.com/](https://www.nero.com/) || [neroaac-bin](https://aur.archlinux.org/pkgbase/neroaac-bin/)

### Image codecs

*   **[JasPer](https://en.wikipedia.org/wiki/JasPer "wikipedia:JasPer")** — Software-based implementation of the codec specified in the emerging JPEG-2000 Part-1 standard.

	[http://www.ece.uvic.ca/~frodo/jasper/](http://www.ece.uvic.ca/~frodo/jasper/) || [jasper](https://www.archlinux.org/packages/?name=jasper)

*   **[OpenJPEG](https://en.wikipedia.org/wiki/OpenJPEG "wikipedia:OpenJPEG")** — Open source JPEG 2000 codec.

	[http://www.openjpeg.org/](http://www.openjpeg.org/) || [openjpeg](https://www.archlinux.org/packages/?name=openjpeg)

### Video codecs

See also [Wikipedia:Comparison of video codecs](https://en.wikipedia.org/wiki/Comparison_of_video_codecs "wikipedia:Comparison of video codecs").

| Codec | Libraries |
| [AV1](https://en.wikipedia.org/wiki/AV1 "wikipedia:AV1") | [aom](https://www.archlinux.org/packages/?name=aom) |
| [Daala](https://en.wikipedia.org/wiki/Daala "wikipedia:Daala") | [daala-git](https://aur.archlinux.org/packages/daala-git/) |
| [Dirac](https://en.wikipedia.org/wiki/Dirac_(video_compression_format) | [schroedinger](https://www.archlinux.org/packages/?name=schroedinger) |
| [DV](https://en.wikipedia.org/wiki/DV "wikipedia:DV") | [libdv](https://www.archlinux.org/packages/?name=libdv) |
| [H.265](https://en.wikipedia.org/wiki/High_Efficiency_Video_Coding "wikipedia:High Efficiency Video Coding") | [x265](https://www.archlinux.org/packages/?name=x265), [x265-hg](https://aur.archlinux.org/packages/x265-hg/) |
| [libde265](https://www.archlinux.org/packages/?name=libde265), [libde265-git](https://aur.archlinux.org/packages/libde265-git/) |
| [H.264](https://en.wikipedia.org/wiki/H.264 "wikipedia:H.264") | [x264](https://www.archlinux.org/packages/?name=x264), [x264-git](https://aur.archlinux.org/packages/x264-git/) |
| [MPEG-1](https://en.wikipedia.org/wiki/MPEG-1 "wikipedia:MPEG-1") | [libmpeg2](https://www.archlinux.org/packages/?name=libmpeg2) (decode) |
| [MPEG-2](https://en.wikipedia.org/wiki/MPEG-2 "wikipedia:MPEG-2") |
| [MPEG-4](https://en.wikipedia.org/wiki/MPEG-4 "wikipedia:MPEG-4") | [Xvid](https://en.wikipedia.org/wiki/Xvid "wikipedia:Xvid") ([xvidcore](https://www.archlinux.org/packages/?name=xvidcore)) |
| [Theora](https://en.wikipedia.org/wiki/Theora "wikipedia:Theora") | [libtheora](https://www.archlinux.org/packages/?name=libtheora) |
| [VP8](https://en.wikipedia.org/wiki/VP8 "wikipedia:VP8") | [libvpx](https://www.archlinux.org/packages/?name=libvpx), [libvpx-git](https://aur.archlinux.org/packages/libvpx-git/) |

*   **[AV1](https://en.wikipedia.org/wiki/AV1 "wikipedia:AV1")** — AOMedia Video 1 (AV1) is successor codec to Google's VP9, Mozilla's Daala, Cisco's Thor.

	[https://aomediacodec.github.io/av1-spec/](https://aomediacodec.github.io/av1-spec/) || [aom](https://www.archlinux.org/packages/?name=aom)

*   **[Daala](https://en.wikipedia.org/wiki/Daala "wikipedia:Daala")** — New video compression technology. The effort is a collaboration between Mozilla Foundation, Xiph.Org Foundation and other contributors. The goal of the project is to provide a free to implement, use and distribute digital media format and reference implementation with technical performance superior to h.265.

	[https://www.xiph.org/daala/](https://www.xiph.org/daala/) || [daala-git](https://aur.archlinux.org/packages/daala-git/)

*   **libde265** — Open source implementation of the h.265 video codec.

	[https://github.com/strukturag/libde265](https://github.com/strukturag/libde265) || [libde265](https://www.archlinux.org/packages/?name=libde265), [libde265-git](https://aur.archlinux.org/packages/libde265-git/)

*   **[libdv](https://en.wikipedia.org/wiki/DV "wikipedia:DV")** — The Quasar DV codec (libdv) is a software codec for DV video.

	[http://libdv.sourceforge.net/](http://libdv.sourceforge.net/) || [libdv](https://www.archlinux.org/packages/?name=libdv)

*   **[libmpeg2](https://en.wikipedia.org/wiki/libmpeg2 "wikipedia:libmpeg2")** — Library for decoding MPEG-1 and MPEG-2 video streams.

	[http://libmpeg2.sourceforge.net/](http://libmpeg2.sourceforge.net/) || [libmpeg2](https://www.archlinux.org/packages/?name=libmpeg2)

*   **[Schrödinger](https://en.wikipedia.org/wiki/Dirac_(video_compression_format) "wikipedia:Dirac (video compression format)")** — Advanced royalty-free video compression format designed for a wide range of uses, from delivering low-resolution web content to broadcasting HD and beyond, to near-lossless studio editing.

	[http://diracvideo.org/](http://diracvideo.org/) || [schroedinger](https://www.archlinux.org/packages/?name=schroedinger)

*   **[Theora](https://en.wikipedia.org/wiki/Theora "wikipedia:Theora")** — Open video codec developed by the Xiph.org.

	[https://www.theora.org/](https://www.theora.org/) || [libtheora](https://www.archlinux.org/packages/?name=libtheora)

*   **[VP8](https://en.wikipedia.org/wiki/VP8 "wikipedia:VP8")** — High-quality, open video format for the web that's freely available to everyone.

	[https://www.webmproject.org](https://www.webmproject.org) || [libvpx](https://www.archlinux.org/packages/?name=libvpx), [libvpx-git](https://aur.archlinux.org/packages/libvpx-git/)

*   **[x264](https://en.wikipedia.org/wiki/x264 "wikipedia:x264")** — Free library for encoding H264/AVC video streams.

	[https://www.videolan.org/developers/x264.html](https://www.videolan.org/developers/x264.html) || [x264](https://www.archlinux.org/packages/?name=x264), [x264-git](https://aur.archlinux.org/packages/x264-git/)

*   **[x265](https://en.wikipedia.org/wiki/x265 "wikipedia:x265")** — Open-source project and free application library for encoding video streams into the H.265/High Efficiency Video Coding (HEVC) format.

	[http://x265.org/](http://x265.org/) || [x265](https://www.archlinux.org/packages/?name=x265) [x265-hg](https://aur.archlinux.org/packages/x265-hg/)

*   **[Xvid](https://en.wikipedia.org/wiki/Xvid "wikipedia:Xvid")** — Open source MPEG-4 video codec.

	[https://www.xvid.org/](https://www.xvid.org/) || [xvidcore](https://www.archlinux.org/packages/?name=xvidcore)

## Container format tools

See also [Wikipedia:Comparison of video container formats](https://en.wikipedia.org/wiki/Comparison_of_video_container_formats "wikipedia:Comparison of video container formats").

*   **[MKVToolNix](https://en.wikipedia.org/wiki/MKVToolNix "wikipedia:MKVToolNix")** — Set of tools to create, edit and inspect Matroska files.

	[https://mkvtoolnix.download/](https://mkvtoolnix.download/) || [mkvtoolnix-cli](https://www.archlinux.org/packages/?name=mkvtoolnix-cli), [mkvtoolnix-gui](https://www.archlinux.org/packages/?name=mkvtoolnix-gui)

*   **OGMtools** — Information, extraction or creation for OGG media streams.

	[http://www.bunkus.org/videotools/ogmtools](http://www.bunkus.org/videotools/ogmtools) || [ogmtools](https://www.archlinux.org/packages/?name=ogmtools)

## Backends

### GStreamer

From [http://www.gstreamer.net/](http://www.gstreamer.net/):

	GStreamer is a library for constructing graphs of media-handling components. The applications it supports range from simple Ogg/Vorbis playback, audio/video streaming to complex audio (mixing) and video (non-linear editing) processing.

Simply, GStreamer is a *backend* or *framework* utilized by many media applications. See [GStreamer](/index.php/GStreamer "GStreamer") article.

### xine

From [http://www.xine-project.org/about](http://www.xine-project.org/about):

	xine is a free (gpl-licensed) high-performance, portable and reusable multimedia playback engine. xine itself is a shared library with an easy to use, yet powerful API which is used by many applications for smooth video playback and video processing purposes.

As an alternative to GStreamer, many media players can be configured to utilize the xine backend provided by [xine-lib](https://www.archlinux.org/packages/?name=xine-lib).

Note that the xine project itself provides a capable video player, [xine-ui](https://www.archlinux.org/packages/?name=xine-ui).

### libavcodec

[libavcodec](https://ffmpeg.org/libavcodec.html) is part of the [FFmpeg](/index.php/FFmpeg "FFmpeg") project. It includes a large number of video and audio codecs. The libavcodec codecs are included with media players such as [MPlayer](/index.php/MPlayer "MPlayer") and [VLC](/index.php/VLC "VLC"), so you may not need to install the [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) package itself.

## Tips and tricks

### Install MPlayer binary codecs

As an ultimate solution, you can try to install MPlayer binary codecs.

If you are not able to play some files go to [http://www.mplayerhq.hu/design7/dload.html](http://www.mplayerhq.hu/design7/dload.html), read the instructions and install the codec you need to play your files.

They can also be found in the [codecs](https://aur.archlinux.org/packages/codecs/) and [codecs64](https://aur.archlinux.org/packages/codecs64/) packages.

### No H264, mpg4 or Musepack (.mpc) in Totem Player

If you see the "The H264 plugin is missing" warning with Totem media player, [install](/index.php/Install "Install") [gst-libav](https://www.archlinux.org/packages/?name=gst-libav).