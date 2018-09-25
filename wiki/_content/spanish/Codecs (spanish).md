**Estado de la traducción:** este artículo es una versión traducida de [Codecs](/index.php/Codecs "Codecs"). Fecha de la última traducción/revisión: **2018-09-07**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Codecs&diff=0&oldid=527964).

Artículos relacionados

*   [Reproducir DVD](/index.php/Optical_disc_drive_(Espa%C3%B1ol)#Reproducir_DVD "Optical disc drive (Español)")
*   [GStreamer](/index.php/GStreamer_(Espa%C3%B1ol) "GStreamer (Español)")
*   [MPlayer](/index.php/MPlayer_(Espa%C3%B1ol) "MPlayer (Español)")
*   [VLC media player](/index.php/VLC_media_player "VLC media player")

Desde [wikipedia](https://en.wikipedia.org/wiki/es:C%C3%B3dec "wikipedia:es:Códec"): «un códec es un dispositivo o programa informático capaz de codificar y/o decodificar un flujo de datos o señal digitales.»

En general, los codecs son utilizados por aplicaciones multimedia para codificar o decodificar transmisiones de audio o vídeo. Para reproducir transmisiones codificadas, los usuarios deben asegurarse de que esté instalado un códec apropiado.

Este artículo trata solo con codecs y backends de aplicaciones; véase la [lista de aplicaciones multimedia](/index.php/List_of_applications#Multimedia "List of applications") para obtener una lista de reproductores multimedia ([MPlayer](/index.php/MPlayer "MPlayer"), [mpv](/index.php/Mpv "Mpv") y [VLC](/index.php/VLC "VLC") son ​​opciones populares).

## Contents

*   [1 Requisitos](#Requisitos)
*   [2 Listado de codecs](#Listado_de_codecs)
    *   [2.1 Codecs de audio](#Codecs_de_audio)
        *   [2.1.1 AAC](#AAC)
        *   [2.1.2 Compresión sin pérdida](#Compresi.C3.B3n_sin_p.C3.A9rdida)
    *   [2.2 Codecs de imagen](#Codecs_de_imagen)
    *   [2.3 Codecs de vídeo](#Codecs_de_v.C3.ADdeo)
*   [3 Backends](#Backends)
    *   [3.1 GStreamer](#GStreamer)
    *   [3.2 xine](#xine)
    *   [3.3 libavcodec](#libavcodec)
*   [4 Consejos y trucos](#Consejos_y_trucos)
    *   [4.1 Instalar codecs binarios de MPlayer](#Instalar_codecs_binarios_de_MPlayer)
    *   [4.2 Sin H264, mpg4 o Musepack (.mpc) en Totem Player](#Sin_H264.2C_mpg4_o_Musepack_.28.mpc.29_en_Totem_Player)

## Requisitos

Para reproducir un contenido multimedia se requieren dos elementos:

*   Un reproductor multimedia
*   El códec adecuado

No siempre es necesario instalar codecs explícitamente si tiene instalado un reproductor multimedia. Por ejemplo, [MPlayer](/index.php/MPlayer "MPlayer") extrae una gran cantidad de codecs como dependencias y también tiene codecs integrados.

## Listado de codecs

### Codecs de audio

*   **[CELT](https://en.wikipedia.org/wiki/CELT "wikipedia:CELT")** — Códec de audio de compresión con pérdida, libre de regalías, optimizado para baja latencia.

	[http://www.celt-codec.org/](http://www.celt-codec.org/) || [celt](https://www.archlinux.org/packages/?name=celt)

*   **[LAME](https://en.wikipedia.org/wiki/LAME "wikipedia:LAME")** — Codificador MP3 y analizador gráfico de tramas.

	[http://lame.sourceforge.net/](http://lame.sourceforge.net/) || [lame](https://www.archlinux.org/packages/?name=lame)

*   **liba52** — Biblioteca libre para la decodificación de secuencias [ATSC A/52](https://en.wikipedia.org/wiki/ATSC_A/52 "wikipedia:ATSC A/52") (Dolby Digital).

	[http://liba52.sourceforge.net/](http://liba52.sourceforge.net/) || [a52dec](https://www.archlinux.org/packages/?name=a52dec)

*   **[libdca](https://en.wikipedia.org/wiki/libdca "wikipedia:libdca")** — Biblioteca libre para decodificar secuencias DTS Coherent Acoustics.

	[https://www.videolan.org/developers/libdca.html](https://www.videolan.org/developers/libdca.html) || [libdca](https://www.archlinux.org/packages/?name=libdca)

*   **[MAD](https://en.wikipedia.org/wiki/libmad "wikipedia:libmad")** — Decodificador de audio MPEG de alta calidad.

	[http://www.underbit.com/products/mad/](http://www.underbit.com/products/mad/) || [libmad](https://www.archlinux.org/packages/?name=libmad)

*   **[Musepack](https://en.wikipedia.org/wiki/Musepack "wikipedia:Musepack")** — Códec de audio de compresión con pérdida de código abierto, diseñado para [transparencia](https://en.wikipedia.org/wiki/es:Transparencia_(compresi%C3%B3n_de_datos) "wikipedia:es:Transparencia (compresión de datos)").

	[http://musepack.net/](http://musepack.net/) || [libmpcdec](https://www.archlinux.org/packages/?name=libmpcdec)

*   **[opencore-amr](https://en.wikipedia.org/wiki/Adaptive_Multi-Rate_audio_codec "wikipedia:Adaptive Multi-Rate audio codec")** — Implementación de código abierto del códec de voz Adaptive Multi Rate (AMR).

	[http://sourceforge.net/projects/opencore-amr/](http://sourceforge.net/projects/opencore-amr/) || [opencore-amr](https://www.archlinux.org/packages/?name=opencore-amr)

*   **[Opus](https://en.wikipedia.org/wiki/Opus_(audio_codec) "wikipedia:Opus (audio codec)")** — Códec de audio abierto, libre de regalías y de compresión con pérdida, diseñado para la codificación de voz y audio en general y baja latencia.

	[http://www.opus-codec.org/](http://www.opus-codec.org/) || [opus](https://www.archlinux.org/packages/?name=opus) [opus-git](https://aur.archlinux.org/packages/opus-git/)

*   **[Speex](https://en.wikipedia.org/wiki/Speex "wikipedia:Speex")** — Formato de compresión de audio de compresión con pérdida y sin patentes diseñado para voz.

	[http://www.speex.org/](http://www.speex.org/) || [speex](https://www.archlinux.org/packages/?name=speex)

*   **[Vorbis](https://en.wikipedia.org/wiki/Vorbis "wikipedia:Vorbis")** — Códec de audio abierto, libre de patentes y de compresión con pérdida.

	[http://www.vorbis.com/](http://www.vorbis.com/) || [libvorbis](https://www.archlinux.org/packages/?name=libvorbis)

#### AAC

De [Wikipedia](https://en.wikipedia.org/wiki/Advanced_Audio_Coding "wikipedia:Advanced Audio Coding"):

	**Advanced Audio Coding** (AAC) es un estándar de codificación de audio patentado para la compresión de audio digital con pérdida. Diseñado para ser el sucesor del formato MP3, AAC generalmente logra una mejor calidad de sonido que MP3 a la misma velocidad de bits.

*   **[FAAC](https://en.wikipedia.org/wiki/FAAC "wikipedia:FAAC")** — Codificador de audio AAC propietario.

	[http://www.audiocoding.com/faac.html](http://www.audiocoding.com/faac.html) || [faac](https://www.archlinux.org/packages/?name=faac)

*   **[FAAD2](https://en.wikipedia.org/wiki/FAAD2 "wikipedia:FAAD2")** — Decodificador de audio ISO AAC.

	[http://www.audiocoding.com/faad2.html](http://www.audiocoding.com/faad2.html) || [faad2](https://www.archlinux.org/packages/?name=faad2)

*   **[Fraunhofer FDK AAC](https://en.wikipedia.org/wiki/FAAD2 "wikipedia:FAAD2")** — Solución de audio completa y de alta calidad para usuarios de Android (y Linux).

	[http://www.iis.fraunhofer.de/en/bf/amm/implementierungen/fdkaaccodec.html](http://www.iis.fraunhofer.de/en/bf/amm/implementierungen/fdkaaccodec.html) || [libfdk-aac](https://www.archlinux.org/packages/?name=libfdk-aac)

*   **[Nero AAC](https://en.wikipedia.org/wiki/AAC "wikipedia:AAC")** — Códec de audio AAC (decodificar/codificar/etiquetar) todo en uno.

	[http://www.nero.com/eng/company/about-nero/nero-aac-codec.php](http://www.nero.com/eng/company/about-nero/nero-aac-codec.php) || [neroaac](https://aur.archlinux.org/packages/neroaac/)

#### Compresión sin pérdida

*   **[Apple Lossless](https://en.wikipedia.org/wiki/es:Apple_Lossless "wikipedia:es:Apple Lossless") (ALAC)** — Un códec de compresión de audio sin pérdida desarrollado por Apple e implementado en todas sus plataformas y dispositivos.

	[https://alac.macosforge.org/](https://alac.macosforge.org/) || [alac-git](https://aur.archlinux.org/packages/alac-git/)

*   **[FLAC](https://en.wikipedia.org/wiki/FLAC "wikipedia:FLAC")** — Códec de audio libre de compresión sin pérdida.

	[https://xiph.org/flac/](https://xiph.org/flac/) || [flac](https://www.archlinux.org/packages/?name=flac)

*   **[WavPack](https://en.wikipedia.org/wiki/WavPack "wikipedia:WavPack")** — Formato de compresión de audio con modos de comprensión sin pérdida, con pérdida e híbrido.

	[http://www.wavpack.com/](http://www.wavpack.com/) || [wavpack](https://www.archlinux.org/packages/?name=wavpack)

### Codecs de imagen

*   **[JasPer](https://en.wikipedia.org/wiki/JasPer "wikipedia:JasPer")** — Implementación basada en software del códec especificado en el estándar emergente JPEG-2000 Part-1.

	[http://www.ece.uvic.ca/~frodo/jasper/](http://www.ece.uvic.ca/~frodo/jasper/) || [jasper](https://www.archlinux.org/packages/?name=jasper)

*   **[OpenJPEG](https://en.wikipedia.org/wiki/OpenJPEG "wikipedia:OpenJPEG")** — Open source JPEG 2000 codec.

	[http://www.openjpeg.org/](http://www.openjpeg.org/) || [openjpeg](https://www.archlinux.org/packages/?name=openjpeg)

### Codecs de vídeo

*   **[AV1](https://en.wikipedia.org/wiki/AV1 "wikipedia:AV1")** — AOMedia Video 1 (AV1) es el códec sucesor de VP9 de Google, Daala de Mozilla, Thor de Cisco.

	[https://aomediacodec.github.io/av1-spec/](https://aomediacodec.github.io/av1-spec/) || [aom](https://www.archlinux.org/packages/?name=aom)

*   **[Daala](https://en.wikipedia.org/wiki/Daala "wikipedia:Daala")** — Nueva tecnología de compresión de vídeo. Es el esfuerzo de una colaboración entre la Fundación Mozilla, la Fundación Xiph.Org y otros colaboradores. El objetivo del proyecto es proporcionar un formato de medios digitales de referencia de implementación, uso y distribución libre con un rendimiento técnico superior a h.265.

	[https://www.xiph.org/daala/](https://www.xiph.org/daala/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **libde265** — Implementación de código abierto del códec de vídeo h.265.

	[https://github.com/strukturag/libde265](https://github.com/strukturag/libde265) || [libde265](https://www.archlinux.org/packages/?name=libde265) [libde265-git](https://aur.archlinux.org/packages/libde265-git/)

*   **[libdv](https://en.wikipedia.org/wiki/DV "wikipedia:DV")** — El códec Quasar DV (libdv) es un códec por software para vídeo DV.

	[http://libdv.sourceforge.net/](http://libdv.sourceforge.net/) || [libdv](https://www.archlinux.org/packages/?name=libdv)

*   **[libmpeg2](https://en.wikipedia.org/wiki/libmpeg2 "wikipedia:libmpeg2")** — Biblioteca para decodificar secuencias de vídeo MPEG-1 y MPEG-2.

	[http://libmpeg2.sourceforge.net/](http://libmpeg2.sourceforge.net/) || [libmpeg2](https://www.archlinux.org/packages/?name=libmpeg2)

*   **[Schrödinger](https://en.wikipedia.org/wiki/Dirac_(video_compression_format) "wikipedia:Dirac (video compression format)")** — Formato avanzado de compresión de vídeo sin regalías diseñado para una amplia gama de usos, desde la entrega de contenido web de baja resolución hasta la transmisión de HD y más allá, la edición de estudio casi sin pérdidas.

	[http://www.audiocoding.com/faac.html](http://www.audiocoding.com/faac.html) || [schroedinger](https://www.archlinux.org/packages/?name=schroedinger)

*   **[Theora](https://en.wikipedia.org/wiki/Theora "wikipedia:Theora")** — Códec de vídeo libre desarrollado por Xiph.org.

	[http://www.theora.org/](http://www.theora.org/) || [libtheora](https://www.archlinux.org/packages/?name=libtheora)

*   **[VP8](https://en.wikipedia.org/wiki/VP8 "wikipedia:VP8")** — Formato de vídeo abierto y de alta calidad para la web que está disponible libremente para todos.

	[http://www.webmproject.org](http://www.webmproject.org) || [libvpx](https://www.archlinux.org/packages/?name=libvpx) [libvpx-git](https://aur.archlinux.org/packages/libvpx-git/)

*   **[x264](https://en.wikipedia.org/wiki/x264 "wikipedia:x264")** — Biblioteca libre para la codificación de secuencias de vídeo H264/AVC.

	[https://www.videolan.org/developers/x264.html](https://www.videolan.org/developers/x264.html) || [x264](https://www.archlinux.org/packages/?name=x264) [x264-git](https://aur.archlinux.org/packages/x264-git/)

*   **[x265](https://en.wikipedia.org/wiki/x265 "wikipedia:x265")** — Proyecto de código abierto y biblioteca de aplicaciones libres para la codificación de secuencias de vídeo en el formato H.265/Codificación de video de alta eficiencia (HEVC).

	[http://x265.org/](http://x265.org/) || [x265](https://www.archlinux.org/packages/?name=x265) [x265-hg](https://aur.archlinux.org/packages/x265-hg/)

*   **[XviD](https://en.wikipedia.org/wiki/XviD "wikipedia:XviD")** — Códec de vídeo de código abierto MPEG-4.

	[http://www.xvid.org/](http://www.xvid.org/) || [xvidcore](https://www.archlinux.org/packages/?name=xvidcore)

## Backends

### GStreamer

De [http://www.gstreamer.net/](http://www.gstreamer.net/):

	GStreamer es una biblioteca para construir grafos de componentes de manejo de medios. Las aplicaciones son compatibles con la reproducción simple de Ogg/Vorbis, la transmisión de audio/vídeo al procesamiento complejo de audio (mezcla) y vídeo (edición no lineal).

Simplemente, GStreamer es un *back-end* o *framework* utilizado por muchas aplicaciones de medios. Véase el artículo [GStreamer](/index.php/GStreamer "GStreamer").

### xine

De [http://www.xine-project.org/about](http://www.xine-project.org/about):

	xine es un motor de reproducción multimedia portátil, reutilizable y de alto rendimiento (con licencia gpl). xine en sí es una biblioteca compartida con una API potente y fácil de usar que es utilizada por muchas aplicaciones para la reproducción fluida de vídeos y el procesamiento de vídeo.

Como alternativa a GStreamer, muchos reproductores de medios pueden configurarse para utilizar el back-end xine proporcionado por [xine-lib](https://www.archlinux.org/packages/?name=xine-lib).

Tenga en cuenta que el proyecto xine en sí mismo proporciona un reproductor de vídeo propio, [xine-ui](https://www.archlinux.org/packages/?name=xine-ui).

### libavcodec

[libavcodec](/index.php/FFmpeg "FFmpeg") es parte del proyecto [FFmpeg](http://ffmpeg.org/). Incluye una gran cantidad de codecs de vídeo y audio. Los codecs de libavcodec se incluyen con reproductores multimedia como [MPlayer](/index.php/MPlayer "MPlayer") y [VLC](/index.php/VLC "VLC"), por lo que es posible que no necesite instalar el paquete [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg).

## Consejos y trucos

### Instalar codecs binarios de MPlayer

Como solución definitiva, puede intentar instalar los codecs binarios de MPlayer.

Si no puede reproducir algunos archivos, vaya a [http://www.mplayerhq.hu/design7/dload.html](http://www.mplayerhq.hu/design7/dload.html), lea las instrucciones e instale el códec que necesite para reproducir sus archivos.

También se pueden encontrar en los paquetes [codecs](https://aur.archlinux.org/packages/codecs/) y [codecs64](https://aur.archlinux.org/packages/codecs64/).

### Sin H264, mpg4 o Musepack (.mpc) en Totem Player

Si observa la advertencia «The H264 plugin is missing» *(No se encuentra el complemento H264)* con el reproductor multimedia Totem, simplemente instale la biblioteca libav de Gstreamer para arreglarlo instalando [gst-libav](https://www.archlinux.org/packages/?name=gst-libav).