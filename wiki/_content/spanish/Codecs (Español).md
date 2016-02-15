Desde [wikipedia](https://en.wikipedia.org/wiki/es:C%C3%B3dec "wikipedia:es:Códec"):

	_Un códec es un dispositivo o programa de ordenador capaz de codificar y/o decodificar un flujo de datos digitales o señal analógica._

En general, los codecs son utilizados por aplicaciones multimedia para codificar o decodificar flujos de audio o vídeo. Con el fin de reproducir secuencias codificadas, los usuarios deben tener instalado un códec apropiado.

En este artículo se tratará solamente de los codecs y de las aplicaciones que trabajan como backends; véase [Common Applications](/index.php/Common_Applications#Multimedia "Common Applications") para obtener una lista de reproductores multimedia (como [MPlayer](/index.php/MPlayer "MPlayer") y [VLC](/index.php/VLC_media_player "VLC media player")).

## Contents

*   [1 Requisitos](#Requisitos)
*   [2 Lista de códecs](#Lista_de_c.C3.B3decs)
*   [3 Backends](#Backends)
    *   [3.1 GStreamer](#GStreamer)
    *   [3.2 xine](#xine)
    *   [3.3 libavcodec](#libavcodec)
*   [4 Consejos y trucos](#Consejos_y_trucos)
    *   [4.1 Instalar codecs binarios de MPlayer](#Instalar_codecs_binarios_de_MPlayer)
    *   [4.2 Sin H264 o mpg4 en el reproductor Totem](#Sin_H264_o_mpg4_en_el_reproductor_Totem)

## Requisitos

Para reproducir un contenido multimedia se requieren dos elementos:

*   Un reproductor multimedia compatible
*   El códec adecuado

No siempre es necesario instalar explícitamente los codecs, si, previamente, se ha instalado un reproductor multimedia. Por ejemplo, [MPlayer](/index.php/MPlayer "MPlayer") conlleva un gran número de códecs como dependencias, y también tiene otros codecs integrados en su compilación.

## Lista de códecs

*   **[ALAC](https://en.wikipedia.org/wiki/ALAC "wikipedia:ALAC")** — Método de compresión de datos que reduce el tamaño de los archivos de audio sin pérdida de información.

	[https://alac.macosforge.org/](https://alac.macosforge.org/) || [alac-svn](https://aur.archlinux.org/packages/alac-svn/)

*   **[CELT](https://en.wikipedia.org/wiki/CELT "wikipedia:CELT")** — Algoritmo de compresión de audio. Al igual que MP3, Vorbis y AAC es adecuado para la transmisión de música con alta calidad. A diferencia de esos formatos, CELT impone muy poco de retraso en la señal, incluso menos que los típicos formatos centrados en la voz como Speex, GSM, o G.729\.

	[http://www.celt-codec.org/](http://www.celt-codec.org/) || [celt](https://www.archlinux.org/packages/?name=celt)

*   **[Daala](https://en.wikipedia.org/wiki/Daala "wikipedia:Daala")** — Nueva tecnología de compresión de vídeo. El esfuerzo es una colaboración entre Mozilla Foundation, Xiph.Org Foundation y otros colaboradores. El objetivo del proyecto es proporcionar una herramienta libre para implementar, usar y distribuir formato de medios digitales y servir de referencia para implementaciones con prestaciones técnicas superiores a h.265.

	[https://www.xiph.org/daala/](https://www.xiph.org/daala/) || [libdaala-git](https://aur.archlinux.org/packages/libdaala-git/)

*   **[FAAC](https://en.wikipedia.org/wiki/FAAC "wikipedia:FAAC")** — Codificador de audio AAC propietario.

	[http://www.audiocoding.com/faac.html](http://www.audiocoding.com/faac.html) || [faac](https://www.archlinux.org/packages/?name=faac)

*   **[FAAD2](https://en.wikipedia.org/wiki/FAAD2 "wikipedia:FAAD2")** — Decodificador de audio ISO AAC.

	[http://www.audiocoding.com/faad2.html](http://www.audiocoding.com/faad2.html) || [faad2](https://www.archlinux.org/packages/?name=faad2)

*   **[FLAC](https://en.wikipedia.org/wiki/FLAC "wikipedia:FLAC")** — Códec de audio libre de compresión sin pérdida.

	[https://xiph.org/flac/](https://xiph.org/flac/) || [flac](https://www.archlinux.org/packages/?name=flac)

*   **[Fraunhofer FDK AAC](https://en.wikipedia.org/wiki/FAAD2 "wikipedia:FAAD2")** — Solución de audio completa y de alta calidad para Android (y Linux).

	[http://www.iis.fraunhofer.de/en/bf/amm/implementierungen/fdkaaccodec.html](http://www.iis.fraunhofer.de/en/bf/amm/implementierungen/fdkaaccodec.html) || [libfdk-aac-git](https://aur.archlinux.org/packages/libfdk-aac-git/)

*   **[Musepack](https://en.wikipedia.org/wiki/Musepack "wikipedia:Musepack")** — Formato de compresión de audio con un fuerte énfasis en la alta calidad. No es un algoritmo de compresión sin pérdida, pero está diseñado para la transparencia, de modo que no seremos capaces de distinguir las diferencias entre el archivo de sonido original y el archivo MPC. Se basa en los algoritmos MPEG-1 Layer-2 / MP2, pero desde 1997 ha mejorado y se desarrollado rápidamente y ahora está en una etapa avanzada en la que mantiene el código optimizado.

	[http://musepack.net/](http://musepack.net/) || [libmpcdec](https://www.archlinux.org/packages/?name=libmpcdec)

*   **[JasPer](https://en.wikipedia.org/wiki/JasPer "wikipedia:JasPer")** — Implementación basada en software del códec especificado en el estándar emergente JPEG-2000 Part-1.

	[http://www.ece.uvic.ca/~frodo/jasper/](http://www.ece.uvic.ca/~frodo/jasper/) || [jasper](https://www.archlinux.org/packages/?name=jasper)

*   **[LAME](https://en.wikipedia.org/wiki/LAME "wikipedia:LAME")** — Codificador MP3 y analizador de marco gráfico.

	[http://lame.sourceforge.net/](http://lame.sourceforge.net/) || [lame](https://www.archlinux.org/packages/?name=lame)

*   **liba52** — Biblioteca libre para la decodificación de ATSC A/52.

	[http://liba52.sourceforge.net/](http://liba52.sourceforge.net/) || [a52dec](https://www.archlinux.org/packages/?name=a52dec)

*   **[libdca](https://en.wikipedia.org/wiki/libdca "wikipedia:libdca")** — Biblioteca libre para la decodificación de DTS Coherent Acoustics.

	[https://www.videolan.org/developers/libdca.html](https://www.videolan.org/developers/libdca.html) || [libdca](https://www.archlinux.org/packages/?name=libdca)

*   **libde265** — Implementación de código abierto del codec de vídeo h.265.

	[https://github.com/strukturag/libde265](https://github.com/strukturag/libde265) || [libde265](https://aur.archlinux.org/packages/libde265/) [libde265-git](https://aur.archlinux.org/packages/libde265-git/)

*   **[libdv](https://en.wikipedia.org/wiki/DV "wikipedia:DV")** — El códec Quasar DV (libd ) es un códec de software para vídeo DV.

	[http://libdv.sourceforge.net/](http://libdv.sourceforge.net/) || [libdv](https://www.archlinux.org/packages/?name=libdv)

*   **[libmpeg2](https://en.wikipedia.org/wiki/libmpeg2 "wikipedia:libmpeg2")** — Biblioteca para decodificar secuencias de vídeo MPEG-1 y MPEG-2.

	[http://libmpeg2.sourceforge.net/](http://libmpeg2.sourceforge.net/) || [libmpeg2](https://www.archlinux.org/packages/?name=libmpeg2)

*   **[MAD](https://en.wikipedia.org/wiki/libmad "wikipedia:libmad")** — Decodificador de audio MPEG de alta calidad .

	[http://www.underbit.com/products/mad/](http://www.underbit.com/products/mad/) || [libmad](https://www.archlinux.org/packages/?name=libmad)

*   **[Nero AAC](https://en.wikipedia.org/wiki/AAC "wikipedia:AAC")** — Códec de audio AAC (decodificar/codificar/etiquetar) todo en uno.

	[http://www.nero.com/eng/company/about-nero/nero-aac-codec.php](http://www.nero.com/eng/company/about-nero/nero-aac-codec.php) || [neroaac](https://aur.archlinux.org/packages/neroaac/)

*   **[opencore-amr](https://en.wikipedia.org/wiki/Adaptive_Multi-Rate_audio_codec "wikipedia:Adaptive Multi-Rate audio codec")** — Implementación de código abierto del códec de voz Adaptive Multi Rate (AMR).

	[http://sourceforge.net/projects/opencore-amr/](http://sourceforge.net/projects/opencore-amr/) || [opencore-amr](https://www.archlinux.org/packages/?name=opencore-amr)

*   **[Speex](https://en.wikipedia.org/wiki/Speex "wikipedia:Speex")** — Formato de compresión de audio libre de patentes diseñado para hablar.

	[http://www.speex.org/](http://www.speex.org/) || [speex](https://www.archlinux.org/packages/?name=speex)

*   **[Theora](https://en.wikipedia.org/wiki/Theora "wikipedia:Theora")** — Códec de vídeo libre desarrollado por Xiph.org.

	[http://www.theora.org/](http://www.theora.org/) || [libtheora](https://www.archlinux.org/packages/?name=libtheora)

*   **[Vorbis](https://en.wikipedia.org/wiki/Vorbis "wikipedia:Vorbis")** — Tecnología de streaming y codificación de audio profesional, completamente libre y libre de patentes.

	[http://www.vorbis.com/](http://www.vorbis.com/) || [libvorbis](https://www.archlinux.org/packages/?name=libvorbis)

*   **[libvpx](https://en.wikipedia.org/wiki/libvpx "wikipedia:libvpx")** — Formato de vídeo de código abierto para la web de alta calidad que está disponible gratuitamente para todo el mundo.

	[http://www.webmproject.org](http://www.webmproject.org) || [libvpx](https://www.archlinux.org/packages/?name=libvpx) [libvpx-git](https://aur.archlinux.org/packages/libvpx-git/)

*   **[Opus](https://en.wikipedia.org/wiki/Opus_(audio_codec) "wikipedia:Opus (audio codec)")** — Códec de audio altamente versátil, totalmente gratuito y libre de regalías. Opus no solo es incomparable para la voz interactiva y la transmisión de música a través de Internet, sino que también está diseñado para aplicaciones de almacenamiento y streaming. Está normalizado por la Internet Engineering Task Force (IETF) como [RFC 6716](//tools.ietf.org/html/rfc6716) que incorporó la tecnología del códec SILK para Skype y del códec CELT para Xiph.Org.

	[http://www.opus-codec.org/](http://www.opus-codec.org/) || [opus](https://www.archlinux.org/packages/?name=opus) [opus-git](https://aur.archlinux.org/packages/opus-git/)

*   **[Schrödinger](https://en.wikipedia.org/wiki/Dirac_(video_compression_format) "wikipedia:Dirac (video compression format)")** — Formato de compresión de vídeo, libre de regalías, de diseño avanzado, para una amplia gama de usos, desde la entrega de contenido web de baja resolución a la radiodifusión de alta definición y más, pasando por algoritmos de compresión sin pérdida para la edición de estudio.

	[http://www.audiocoding.com/faac.html](http://www.audiocoding.com/faac.html) || [schroedinger](https://www.archlinux.org/packages/?name=schroedinger)

*   **[WavPack](https://en.wikipedia.org/wiki/WavPack "wikipedia:WavPack")** — Formato de compresión de audio con modalidades de comprensión sin pérdidas, con pérdida y compresión híbrida.

	[http://www.wavpack.com/](http://www.wavpack.com/) || [wavpack](https://www.archlinux.org/packages/?name=wavpack)

*   **[x264](https://en.wikipedia.org/wiki/x264 "wikipedia:x264")** — Biblioteca libre para codificar secuencias de vídeo H264/AVC.

	[https://www.videolan.org/developers/x264.html](https://www.videolan.org/developers/x264.html) || [x264](https://www.archlinux.org/packages/?name=x264) [x264-git](https://aur.archlinux.org/packages/x264-git/)

*   **[x265](https://en.wikipedia.org/wiki/x265 "wikipedia:x265")** — Proyecto de código abierto y biblioteca de aplicaciones libres para la codificación de secuencias de vídeo en el formato H.265/High Efficiency Video Coding (HEVC).

	[http://x265.org/](http://x265.org/) || [x265](https://www.archlinux.org/packages/?name=x265) [x265-hg](https://aur.archlinux.org/packages/x265-hg/)

*   **[XviD](https://en.wikipedia.org/wiki/XviD "wikipedia:XviD")** — Códec de vídeo de código abierto MPEG-4.

	[http://www.xvid.org/](http://www.xvid.org/) || [xvidcore](https://www.archlinux.org/packages/?name=xvidcore)

## Backends

### GStreamer

Desde [http://www.gstreamer.net/](http://www.gstreamer.net/):

	_[GStreamer](/index.php/GStreamer "GStreamer") es una biblioteca utilizada para la construcción gráfica de los componentes multimedia manipulables. Las aplicaciones que soporta van desde la simple reproducción de Ogg/Vorbis, a la conversión de audio/video a audio complejo (mezclar) y la elaboración de vídeo (edición no lineal)._

Simplemente, GStreamer es un _backend_ o _framework_ utilizado por muchos reproductores multimedia.

### xine

Desde [http://www.xine-project.org/about](http://www.xine-project.org/about):

	_Xine es un recurso libre (licencia GPL) de alto rendimiento, un motor de reproducción multimedia, portátil y reutilizable. Xine es, en sí mismo, una biblioteca compartida de uso fácil, pero con un potente API, que es utilizado por muchas aplicaciones para la reproducción fluida de vídeo y para fines de elaboración de video_.

Como una alternativa a GStreamer, muchos reproductores multimedia pueden ser configurados para utilizar el backend de xine proporcionado por [xine-lib](https://www.archlinux.org/packages/?name=xine-lib).

Tenga en cuenta que el proyecto xine sí ofrece un reproductor de vídeo propio, [xine-ui](https://www.archlinux.org/packages/?name=xine-ui).

### libavcodec

libavcodec es parte del proyecto [FFmpeg](http://ffmpeg.org/). Incluye una gran cantidad de codecs de vídeo y audio. Los codecs libavcodec se incluyen en algunos reproductores multimedia como [MPlayer](/index.php/MPlayer "MPlayer") y [VLC](/index.php/VLC "VLC"), de modo que, instalados los mismos, no se necesita instalar el propio paquete [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg).

## Consejos y trucos

### Instalar codecs binarios de MPlayer

Como última solución, se puede tratar de instalar codecs binarios de MPlayer.

Si no es capaz de reproducir algunos archivos diríjase a [http://www.mplayerhq.hu/design7/dload.html](http://www.mplayerhq.hu/design7/dload.html), lea las instrucciones e instale el códec que necesite para reproducir los archivos correspondientes.

También se pueden encontrar en AUR con el nombre [codecs](https://aur.archlinux.org/packages/codecs/) y [codecs64](https://aur.archlinux.org/packages/codecs64/).

### Sin H264 o mpg4 en el reproductor Totem

Si observa el aviso «The H264 plugin is missing» con el reproductor multimedia Totem, solo tiene que instalar la biblioteca Gstreamer AV para arreglarlo instalando [gst-libav](https://www.archlinux.org/packages/?name=gst-libav).