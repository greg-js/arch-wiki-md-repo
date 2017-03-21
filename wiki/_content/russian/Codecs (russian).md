Цитата из [Википедии](https://en.wikipedia.org/wiki/ru:%D0%9A%D0%BE%D0%B4%D0%B5%D0%BA "wikipedia:ru:Кодек"):

	*Ко́дек (англ. codec, от coder/decoder — кодировщик/декодировщик или compressor/decompressor) — устройство или программа, способная выполнять преобразование данных или сигнала.*

Кодеки используются мультимедийными приложениями для кодирования и декодирования аудио и видео потоков. Для того, чтобы иметь возможность проигрывать закодированные потоки, пользователи должны обеспечить установку соответствующего кодека.

## Contents

*   [1 Требования](#.D0.A2.D1.80.D0.B5.D0.B1.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
*   [2 Список кодеков](#.D0.A1.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D0.BA.D0.BE.D0.B4.D0.B5.D0.BA.D0.BE.D0.B2)
*   [3 Бэкэнды](#.D0.91.D1.8D.D0.BA.D1.8D.D0.BD.D0.B4.D1.8B)
    *   [3.1 GStreamer](#GStreamer)
    *   [3.2 xine](#xine)
    *   [3.3 libavcodec](#libavcodec)
*   [4 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [4.1 Установка бинарных кодеков MPlayer](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B1.D0.B8.D0.BD.D0.B0.D1.80.D0.BD.D1.8B.D1.85_.D0.BA.D0.BE.D0.B4.D0.B5.D0.BA.D0.BE.D0.B2_MPlayer)
    *   [4.2 Не работают H264, mpg4 или Musepack (.mpc) в Totem Player](#.D0.9D.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.8E.D1.82_H264.2C_mpg4_.D0.B8.D0.BB.D0.B8_Musepack_.28.mpc.29_.D0.B2_Totem_Player)

## Требования

Любой проигрыватель мультимедиа требует наличия двух компонентов:

*   Собственно медиа плеер
*   Соответствующий кодек

Данная статья посвящена только операциям с кодеками; смотрите статью [Список приложений/Мультимедиа](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9/%D0%9C%D1%83%D0%BB%D1%8C%D1%82%D0%B8%D0%BC%D0%B5%D0%B4%D0%B8%D0%B0 "Список приложений/Мультимедиа") для выбора подходящего плеера ([MPlayer](/index.php/MPlayer_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MPlayer (Русский)") или [VLC](http://www.videolan.org/vlc/) для выбора наиболее популярного).

## Список кодеков

*   **[ALAC](https://en.wikipedia.org/wiki/ALAC "wikipedia:ALAC")** — Метод сжатия аудио без потери качества.

	[https://alac.macosforge.org/](https://alac.macosforge.org/) || [alac-svn](https://aur.archlinux.org/packages/alac-svn/)

*   **[CELT](https://en.wikipedia.org/wiki/CELT "wikipedia:CELT")** — Алгоритм сжатия аудио. Так же, как MP3, Vorbis или AAC, разработан для передачи музыки высокого качества, но, в отличие от них, имеет очень короткую задержку сигнала, даже короче, чем у типичных форматов, ориентиованных на речь: Sppex, GSM или G.729.

	[http://www.celt-codec.org/](http://www.celt-codec.org/) || [celt](https://www.archlinux.org/packages/?name=celt)

*   **[Daala](https://en.wikipedia.org/wiki/ru:Daala "wikipedia:ru:Daala")** — Новая технология сжатия видео, являющаяся плодом сотрудничества Mozilla Foundation, Xiph.Org Foundation и др. Цель проекта — предоставить свободный для использования и распространения формат медиа данных и его эталонную реализацию, превосходящую по эффективности h.265.

	[https://www.xiph.org/daala/](https://www.xiph.org/daala/) || [libdaala-git](https://aur.archlinux.org/packages/libdaala-git/)

*   **[FAAC](https://en.wikipedia.org/wiki/FAAC "wikipedia:FAAC")** — Проприетарный AAC аудио шифратор (кодер).

	[http://www.audiocoding.com/faac.html](http://www.audiocoding.com/faac.html) || [faac](https://www.archlinux.org/packages/?name=faac)

*   **[FAAD2](https://en.wikipedia.org/wiki/FAAD2 "wikipedia:FAAD2")** — ISO AAC аудио декодер.

	[http://www.audiocoding.com/faad2.html](http://www.audiocoding.com/faad2.html) || [faad2](https://www.archlinux.org/packages/?name=faad2)

*   **[FLAC](https://en.wikipedia.org/wiki/ru:FLAC "wikipedia:ru:FLAC")** — Свободный аудио кодек, сжимающий данные без потерь.

	[https://xiph.org/flac/](https://xiph.org/flac/) || [flac](https://www.archlinux.org/packages/?name=flac)

*   **[Fraunhofer FDK AAC](https://en.wikipedia.org/wiki/FAAD2 "wikipedia:FAAD2")** — Полноценный, высококачественный кодек для Linux (в том числе Android).

	[http://www.iis.fraunhofer.de/en/bf/amm/implementierungen/fdkaaccodec.html](http://www.iis.fraunhofer.de/en/bf/amm/implementierungen/fdkaaccodec.html) || [libfdk-aac-git](https://aur.archlinux.org/packages/libfdk-aac-git/)

*   **[JasPer](https://en.wikipedia.org/wiki/JasPer "wikipedia:JasPer")** — Программная реализация кодека, описанного в стандарте JPEG-2000 Part-1.

	[http://www.ece.uvic.ca/~frodo/jasper/](http://www.ece.uvic.ca/~frodo/jasper/) || [jasper](https://www.archlinux.org/packages/?name=jasper)

*   **[LAME](https://en.wikipedia.org/wiki/ru:LAME "wikipedia:ru:LAME")** — Высококачественный MPEG Audio Layer III (MP3) кодер.

	[http://lame.sourceforge.net/](http://lame.sourceforge.net/) || [lame](https://www.archlinux.org/packages/?name=lame)

*   **liba52** — Свободная библиотека для декодирования ATSC A/52 потоков.

	[http://liba52.sourceforge.net/](http://liba52.sourceforge.net/) || [a52dec](https://www.archlinux.org/packages/?name=a52dec)

*   **[libdca](https://en.wikipedia.org/wiki/libdca "wikipedia:libdca")** — Библиотека для декодирования DTS Coherent Acoustics потоков.

	[https://www.videolan.org/developers/libdca.html](https://www.videolan.org/developers/libdca.html) || [libdca](https://www.archlinux.org/packages/?name=libdca)

*   **libde265** — Открытая реализация видеокодека h.265.

	[https://github.com/strukturag/libde265](https://github.com/strukturag/libde265) || [libde265](https://aur.archlinux.org/packages/libde265/) [libde265-git](https://aur.archlinux.org/packages/libde265-git/)

*   **[libdv](https://en.wikipedia.org/wiki/ru:DV "wikipedia:ru:DV")** — Программный кодек для DV видео.

	[http://libdv.sourceforge.net/](http://libdv.sourceforge.net/) || [libdv](https://www.archlinux.org/packages/?name=libdv)

*   **[libmpeg2](https://en.wikipedia.org/wiki/libmpeg2 "wikipedia:libmpeg2")** — Библиотека для декодирования MPEG-1 и MPEG-2 видеопотоков.

	[http://libmpeg2.sourceforge.net/](http://libmpeg2.sourceforge.net/) || [libmpeg2](https://www.archlinux.org/packages/?name=libmpeg2)

*   **[MAD](https://en.wikipedia.org/wiki/libmad "wikipedia:libmad")** — Высококачественный декодер MPEG аудио.

	[http://www.underbit.com/products/mad/](http://www.underbit.com/products/mad/) || [libmad](https://www.archlinux.org/packages/?name=libmad)

*   **[Musepack](https://en.wikipedia.org/wiki/ru:Musepack "wikipedia:ru:Musepack")** — Формат сжатия данных с особым акцентом на качестве. Сжимает данные с потерями, но разработан так, что вы не услышите разницы между оригиналом и гораздо меньшим по объему MPC файлом. Основан на алгоритмах MPEG-1 Layer-2 / MP2, но с 1997-го года кодек был переработан и значительно улучшен и теперь состоит только из хорошо оптимизированного и свободного кода.

	[http://musepack.net/](http://musepack.net/) || [libmpcdec](https://www.archlinux.org/packages/?name=libmpcdec)

*   **[Nero AAC](https://en.wikipedia.org/wiki/ru:Advanced_Audio_Coding "wikipedia:ru:Advanced Audio Coding")** — AAC аудиокодек.

	[http://www.nero.com/eng/company/about-nero/nero-aac-codec.php](http://www.nero.com/eng/company/about-nero/nero-aac-codec.php) || [neroaac](https://aur.archlinux.org/packages/neroaac/)

*   **[opencore-amr](https://en.wikipedia.org/wiki/ru:AMR_(%D1%81%D0%B6%D0%B0%D1%82%D0%B8%D0%B5_%D0%B7%D0%B2%D1%83%D0%BA%D0%B0) "wikipedia:ru:AMR (сжатие звука)")** — Открытая реализация речевого кодека Adaptive Multi Rate (AMR).

	[http://sourceforge.net/projects/opencore-amr/](http://sourceforge.net/projects/opencore-amr/) || [opencore-amr](https://www.archlinux.org/packages/?name=opencore-amr)

*   **[Opus](https://en.wikipedia.org/wiki/ru:Opus_(%D0%BA%D0%BE%D0%B4%D0%B5%D0%BA) "wikipedia:ru:Opus (кодек)")** — Полностью открытый, бесплатный и очень гибкий аудиокодек. Opus не только бесподобен для передачи аудио в реальном времени через Интернет, но и подходит для хранения данных. Он стандартизирован Internet Engineering Task Force (IETF) как RFC 6716, включающий технологии SILK (Skype)и CELT (Xiph.Org) кодеков.

	[http://www.opus-codec.org/](http://www.opus-codec.org/) || [opus](https://www.archlinux.org/packages/?name=opus) [opus-git](https://aur.archlinux.org/packages/opus-git/)

*   **[Schrödinger](https://en.wikipedia.org/wiki/ru:Dirac "wikipedia:ru:Dirac")** — Бесплатный формат сжатия видео, подходящий для широкого круга применений: от передачи веб-контента низкого разрешения до трансляции HD и выше и студийного редактирования видео.

	[http://www.audiocoding.com/faac.html](http://www.audiocoding.com/faac.html) || [schroedinger](https://www.archlinux.org/packages/?name=schroedinger)

*   **[Speex](https://en.wikipedia.org/wiki/ru:Speex "wikipedia:ru:Speex")** — Формат сжатия данных, разработанный для речи.

	[http://www.speex.org/](http://www.speex.org/) || [speex](https://www.archlinux.org/packages/?name=speex)

*   **[Theora](https://en.wikipedia.org/wiki/ru:Theora "wikipedia:ru:Theora")** — Открытый видеокодек, разработанный Xiph.org.

	[http://www.theora.org/](http://www.theora.org/) || [libtheora](https://www.archlinux.org/packages/?name=libtheora)

*   **[Vorbis](https://en.wikipedia.org/wiki/ru:Vorbis "wikipedia:ru:Vorbis")** — Полностью открытая, профессиональная технология стриминга и сжатия аудио.

	[http://www.vorbis.com/](http://www.vorbis.com/) || [libvorbis](https://www.archlinux.org/packages/?name=libvorbis)

*   **[VP8](https://en.wikipedia.org/wiki/ru:VP8 "wikipedia:ru:VP8")** — Высококачественный, открытый видеоформат для веба, доступный всем.

	[http://www.webmproject.org](http://www.webmproject.org) || [libvpx](https://www.archlinux.org/packages/?name=libvpx) [libvpx-git](https://aur.archlinux.org/packages/libvpx-git/)

*   **[WavPack](https://en.wikipedia.org/wiki/ru:WavPack "wikipedia:ru:WavPack")** — Аудиокодер с тремя режимами: без потерь, с потерями и гибридный.

	[http://www.wavpack.com/](http://www.wavpack.com/) || [wavpack](https://www.archlinux.org/packages/?name=wavpack)

*   **[x264](https://en.wikipedia.org/wiki/ru:x264 "wikipedia:ru:x264")** — Свободная библиотека для кодирования H264/AVC видеопотоков.

	[https://www.videolan.org/developers/x264.html](https://www.videolan.org/developers/x264.html) || [x264](https://www.archlinux.org/packages/?name=x264) [x264-git](https://aur.archlinux.org/packages/x264-git/)

*   **[x265](https://en.wikipedia.org/wiki/ru:x265 "wikipedia:ru:x265")** — Свободная библиотека для кодирования в H.265/High Efficiency Video Coding (HEVC) формат.

	[http://x265.org/](http://x265.org/) || [x265](https://www.archlinux.org/packages/?name=x265) [x265-hg](https://aur.archlinux.org/packages/x265-hg/)

*   **[Xvid](https://en.wikipedia.org/wiki/ru:Xvid "wikipedia:ru:Xvid")** — Открытый MPEG-4 видеокодек.

	[http://www.xvid.org/](http://www.xvid.org/) || [xvidcore](https://www.archlinux.org/packages/?name=xvidcore)

## Бэкэнды

### GStreamer

GStreamer — это мультимедийный фреймворк, являющийся «ядром» многих мультимедийных приложений, таких как видеоредакторы, потоковые серверы и медиаплееры. См. [GStreamer](/index.php/GStreamer "GStreamer").

### xine

xine — свободный, эффективный и переносимый мультимедийный фреймворк. Сам по себе, xine является библиотекой с простым, но мощным API, использующейся во многих приложениях.

Как альтернатива GStreamer, многие медиаплееры могут быть настроены так, чтобы использовать xine, предоставляемый пакетом [xine-lib](https://www.archlinux.org/packages/?name=xine-lib).

Заметьте, что сам проект xine предоставляет видеоплеер — [xine-ui](https://www.archlinux.org/packages/?name=xine-ui).

### libavcodec

[libavcodec](/index.php/FFmpeg "FFmpeg") — часть проекта [FFmpeg](http://ffmpeg.org/). Библиотека включает в себя большое число видео- и аудиокодеков. Эти кодеки идут в составе таких медиаплееров, как [MPlayer](/index.php/MPlayer_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MPlayer (Русский)") или [VLC](/index.php/VLC "VLC"). Таким образом, вам не требуется устанавливать сам пакет [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg).

## Советы и рекомендации

### Установка бинарных кодеков MPlayer

Если больше ничего не остается, вы можете попробовать установить бинарные кодеки MPlayer.

Если не проигрываются некоторые файлы, зайдите на [http://www.mplayerhq.hu/design7/dload-ru.html](http://www.mplayerhq.hu/design7/dload-ru.html), прочитайте инструкции и установите кодеки, которые вам нужны.

Они могут быть найдены в AUR с именем [codecs](https://aur.archlinux.org/packages/codecs/) или [codecs64](https://aur.archlinux.org/packages/codecs64/).

### Не работают H264, mpg4 или Musepack (.mpc) в Totem Player

Если вы видите предупреждение "The H264 plugin is missing", используя Totem Player, просто установите библиотеку GStreamer libav [gst-libav](https://www.archlinux.org/packages/?name=gst-libav).