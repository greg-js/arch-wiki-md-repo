Articoli correlati

*   [DVD Playing](/index.php/DVD_Playing "DVD Playing")
*   [GStreamer](/index.php/GStreamer "GStreamer")
*   [Mplayer](/index.php/MPlayer_(Italiano) "MPlayer (Italiano)")
*   [VLC media player](/index.php/VLC_media_player "VLC media player")

Da [wikipedia](https://en.wikipedia.org/wiki/it:Codec "wikipedia:it:Codec"):

	*In elettronica, informatica e telecomunicazioni un codec è un programma o un dispositivo che si occupa di codificare e/o decodificare digitalmente un segnale analogico.*

In generale, i codec sono utilizzati dalle applicazioni multimediali per codificare e/o decodificare un flusso audio o video. Per poter decodificare un flusso, gli utenti devono avere installato il codec appropriato.

Questo articolo tratterà solamente di codec e di applicazioni che lavorano come backend; si veda l'articolo [Lista delle applicazioni](/index.php/List_of_applications_(Italiano)#Multimedia.23Multimedia "List of applications (Italiano)") per una lista completa di media player più utilizzati (come [MPlayer](/index.php/MPlayer_(Italiano) "MPlayer (Italiano)"), [mpv](/index.php/Mpv "Mpv") e [VLC](/index.php/VLC "VLC")).

## Contents

*   [1 Requisiti](#Requisiti)
*   [2 Lista dei codec](#Lista_dei_codec)
*   [3 Backends](#Backends)
    *   [3.1 GStreamer](#GStreamer)
    *   [3.2 xine](#xine)
    *   [3.3 libavcodec](#libavcodec)
*   [4 Trucchi e Soluzioni](#Trucchi_e_Soluzioni)
    *   [4.1 Installare codec binari per MPlayer](#Installare_codec_binari_per_MPlayer)
    *   [4.2 H264, mpg4 o Musepack (.mpc) mancante in Totem Player](#H264.2C_mpg4_o_Musepack_.28.mpc.29_mancante_in_Totem_Player)

## Requisiti

La riproduzione di file multimediali richiede due componenti:

*   Un lettore multimediale compatibile
*   Il codec appropriato

Non è sempre necesario installare un codec specifico se si installa un lettore multimediale. Ad esempio, [MPlayer](/index.php/MPlayer_(Italiano) "MPlayer (Italiano)") si tira dietro come dipendenze un largo numero di codec, e altri ne ha inglobati nella sua compilazione.

## Lista dei codec

*   **[ALAC](https://en.wikipedia.org/wiki/ALAC "wikipedia:ALAC")** — Metodo di compressione dei dati che riduce la dimensione dei file audio senza perdita di informazioni.

	[https://alac.macosforge.org/](https://alac.macosforge.org/) || [alac-svn](https://aur.archlinux.org/packages/alac-svn/)

*   **[CELT](https://en.wikipedia.org/wiki/CELT "wikipedia:CELT")** — Algoritmo di compressione per l'audio. Come MP3, Vorbis, AAC, ed è adatto per la trasmissione di musica con alta qualità. A differenza di questi formati CELT impone un ritardo sul segnale molto ridotto, è tipico per i formati di trasmissione vocale come Speex, GSM, o G.729\.

	[http://www.celt-codec.org/](http://www.celt-codec.org/) || [celt](https://www.archlinux.org/packages/?name=celt)

*   **[Daala](https://en.wikipedia.org/wiki/Daala "wikipedia:Daala")** — La nuova tecnologia di compressione video. Lo sforzo è una collaborazione tra Mozilla Foundation, Xiph.Org Fondazione e altri collaboratori. L'obiettivo del progetto è quello di fornire una implementazione libera, utilizzare e distribuire il formato digitale dei media e fornire un punto di riferimanto, con prestazioni tecniche superiori a h.265.

	[https://www.xiph.org/daala/](https://www.xiph.org/daala/) || [libdaala-git](https://aur.archlinux.org/packages/libdaala-git/)

*   **[FAAC](https://en.wikipedia.org/wiki/FAAC "wikipedia:FAAC")** — Codificatore audio proprietario AAC.

	[http://www.audiocoding.com/faac.html](http://www.audiocoding.com/faac.html) || [faac](https://www.archlinux.org/packages/?name=faac)

*   **[FAAD2](https://en.wikipedia.org/wiki/FAAD2 "wikipedia:FAAD2")** — ISO AAC audio decoder.

	[http://www.audiocoding.com/faad2.html](http://www.audiocoding.com/faad2.html) || [faad2](https://www.archlinux.org/packages/?name=faad2)

*   **[FLAC](https://en.wikipedia.org/wiki/FLAC "wikipedia:FLAC")** — Free Lossless Audio Codec.

	[https://xiph.org/flac/](https://xiph.org/flac/) || [flac](https://www.archlinux.org/packages/?name=flac)

*   **[Fraunhofer FDK AAC](https://en.wikipedia.org/wiki/FAAD2 "wikipedia:FAAD2")** —

	Soluzione audio completa di alta qualità per gli utenti Android ( e Linux ). || [http://www.iis.fraunhofer.de/en/bf/amm/implementierungen/fdkaaccodec.html](http://www.iis.fraunhofer.de/en/bf/amm/implementierungen/fdkaaccodec.html)

*   **[Musepack](https://en.wikipedia.org/wiki/Musepack "wikipedia:Musepack")** — Formato di compressione audio con una forte enfasi sulla qualità . Non è lossless ma è progettato per la trasparenza, in modo che non sarà in grado di sentire le differenze tra il file wave originale e il file MPC molto più piccolo. Si basa sugli algoritmi MPEG-1 Layer-2 / MP2, ma dal 1997 si è rapidamente sviluppato e notevolmente migliorato ed è ora in fase avanzata in cui contiene un codice pesantemente ottimizzato e performante.

	[http://musepack.net/](http://musepack.net/) || [libmpcdec](https://www.archlinux.org/packages/?name=libmpcdec)

*   **[JasPer](https://en.wikipedia.org/wiki/JasPer "wikipedia:JasPer")** — Implementazione software basata sul codec specificato nello standard emergente JPEG-2000 Part 1.

	[http://www.ece.uvic.ca/~frodo/jasper/](http://www.ece.uvic.ca/~frodo/jasper/) || [jasper](https://www.archlinux.org/packages/?name=jasper)

*   **[LAME](https://en.wikipedia.org/wiki/LAME "wikipedia:LAME")** — Encoder MP3 e analizzatore grafico.

	[http://lame.sourceforge.net/](http://lame.sourceforge.net/) || [lame](https://www.archlinux.org/packages/?name=lame)

*   **liba52** — Libreria gratuita per la decodifica di flussi ATSC A/52.

	[http://liba52.sourceforge.net/](http://liba52.sourceforge.net/) || [a52dec](https://www.archlinux.org/packages/?name=a52dec)

*   **[libdca](https://en.wikipedia.org/wiki/libdca "wikipedia:libdca")** — Libreria gratuita per la decodifica dei flussi DTS Coherent Acoustics.

	[https://www.videolan.org/developers/libdca.html](https://www.videolan.org/developers/libdca.html) || [libdca](https://www.archlinux.org/packages/?name=libdca)

*   **libde265** — Implementazione open source del codec video h.265\.

	[https://github.com/strukturag/libde265](https://github.com/strukturag/libde265) || [libde265](https://www.archlinux.org/packages/?name=libde265) [libde265-git](https://aur.archlinux.org/packages/libde265-git/)

*   **[libdv](https://en.wikipedia.org/wiki/DV "wikipedia:DV")** — Il codec Quasar DV ( libdv ) è un codec software per video DV.

	[http://libdv.sourceforge.net/](http://libdv.sourceforge.net/) || [libdv](https://www.archlinux.org/packages/?name=libdv)

*   **[libmpeg2](https://en.wikipedia.org/wiki/libmpeg2 "wikipedia:libmpeg2")** — Libreria per la decodifica MPEG-1 e MPEG-2 stream video.

	[http://libmpeg2.sourceforge.net/](http://libmpeg2.sourceforge.net/) || [libmpeg2](https://www.archlinux.org/packages/?name=libmpeg2)

*   **[MAD](https://en.wikipedia.org/wiki/libmad "wikipedia:libmad")** — Decodificatore audio MPEG di alta qualità.

	[http://www.underbit.com/products/mad/](http://www.underbit.com/products/mad/) || [libmad](https://www.archlinux.org/packages/?name=libmad)

*   **[Nero AAC](https://en.wikipedia.org/wiki/AAC "wikipedia:AAC")** — AAC audio codec tutto incluso (decode/encode/tag).

	[http://www.nero.com/eng/company/about-nero/nero-aac-codec.php](http://www.nero.com/eng/company/about-nero/nero-aac-codec.php) || [neroaac](https://aur.archlinux.org/packages/neroaac/)

*   **[opencore-amr](https://en.wikipedia.org/wiki/Adaptive_Multi-Rate_audio_codec "wikipedia:Adaptive Multi-Rate audio codec")** — Implementazione open source del codec vocale Adaptive Multi Rate (AMR).

	[http://sourceforge.net/projects/opencore-amr/](http://sourceforge.net/projects/opencore-amr/) || [opencore-amr](https://www.archlinux.org/packages/?name=opencore-amr)

*   **[Speex](https://en.wikipedia.org/wiki/Speex "wikipedia:Speex")** — Formato di compressione audio libero da brevetti progettato per la sintesi vocale.

	[http://www.speex.org/](http://www.speex.org/) || [speex](https://www.archlinux.org/packages/?name=speex)

*   **[Theora](https://en.wikipedia.org/wiki/Theora "wikipedia:Theora")** — Codec video libero sviluppato da Xiph.org.

	[http://www.theora.org/](http://www.theora.org/) || [libtheora](https://www.archlinux.org/packages/?name=libtheora)

*   **[Vorbis](https://en.wikipedia.org/wiki/Vorbis "wikipedia:Vorbis")** — Completamente libera, codifica audio professionale libero da brevetti e tecnologia di streaming.

	[http://www.vorbis.com/](http://www.vorbis.com/) || [libvorbis](https://www.archlinux.org/packages/?name=libvorbis)

*   **[libvpx](https://en.wikipedia.org/wiki/libvpx "wikipedia:libvpx")** — Di alta qualità, formato video libero per il web, liberamente disponibile a tutti.

	[http://www.webmproject.org](http://www.webmproject.org) || [libvpx](https://www.archlinux.org/packages/?name=libvpx) [libvpx-git](https://aur.archlinux.org/packages/libvpx-git/)

*   **[Opus](https://en.wikipedia.org/wiki/Opus_(audio_codec) "wikipedia:Opus (audio codec)")** — Completamente libero, codec audio estremamente versatile royalty-free. Opus è impareggiabile per il discorso interattivo e trasmissione di musica su Internet, ma è destinato anche per le applicazioni di archiviazione e streaming. É standardizzato dalla Internet Engineering Task Force (IETF), come RFC 6716 che ha incorporato la tecnologia di codec SILK di Skype e il codec CELT di Xiph.Org.

	[http://www.opus-codec.org/](http://www.opus-codec.org/) || [opus](https://www.archlinux.org/packages/?name=opus) [opus-git](https://aur.archlinux.org/packages/opus-git/)

*   **[Schrödinger](https://en.wikipedia.org/wiki/Dirac_(video_compression_format) "wikipedia:Dirac (video compression format)")** — Formato di compressione video avanzata royalty-free, progettato per una vasta gamma di utilizzi, dalla distribuzione di contenuti web a bassa risoluzione per trasmissioni HD e oltre, a near- lossless editing studio.

	[http://www.audiocoding.com/faac.html](http://www.audiocoding.com/faac.html) || [schroedinger](https://www.archlinux.org/packages/?name=schroedinger)

*   **[WavPack](https://en.wikipedia.org/wiki/WavPack "wikipedia:WavPack")** — Formato di compressione audio con lossless, lossy e modalità di compressione ibrida.

	[http://www.wavpack.com/](http://www.wavpack.com/) || [wavpack](https://www.archlinux.org/packages/?name=wavpack)

*   **[x264](https://en.wikipedia.org/wiki/x264 "wikipedia:x264")** — Libreria gratuita per la codifica di flussi video H264/AVC.

	[https://www.videolan.org/developers/x264.html](https://www.videolan.org/developers/x264.html) || [x264](https://www.archlinux.org/packages/?name=x264) [x264-git](https://aur.archlinux.org/packages/x264-git/)

*   **[x265](https://en.wikipedia.org/wiki/x265 "wikipedia:x265")** — Progetto open-source e libreria di applicazione gratuita per la codifica di flussi video in formato H.265/High Efficiency Video Coding (HEVC).

	[http://x265.org/](http://x265.org/) || [x265](https://www.archlinux.org/packages/?name=x265) [x265-hg](https://aur.archlinux.org/packages/x265-hg/)

*   **[XviD](https://en.wikipedia.org/wiki/XviD "wikipedia:XviD")** — Codec open source video MPEG-4.

	[http://www.xvid.org/](http://www.xvid.org/) || [xvidcore](https://www.archlinux.org/packages/?name=xvidcore)

## Backends

### GStreamer

Da [http://www.gstreamer.net/](http://www.gstreamer.net/):

	*[GStreamer](/index.php/GStreamer "GStreamer") è una piattaforma software altamente modulare utilizzata per creare applicazioni multimediali. Le applicazioni supportate vanno da semplici riproduttori Ogg/Vorbis, flussi audio/video a mixaggio audio complessi ed elaborazione di video-editing non lineare.*

Più semplicemente, GStreamer e un *backend* o *framework* utilizzato da molti lettori multimediali. Si veda la pagina [GStreamer](/index.php/GStreamer "GStreamer") per ulteriori informazioni.

### xine

Da [http://www.xine-project.org/about](http://www.xine-project.org/about):

	*xine è un libero (licenza GPL) motore di riproduzione multimediale ad alte prestazioni, portatile e riutilizzabile. xine è di per sé una libreria condivisa facile da usare, ed anche una potente API che viene utilizzata da molte applicazioni per la riproduzione video e nella finalità di elaborazione video.*

In alternativa a GStreamer, molti media player possono essere configurati per utilizzare il backend xine fornito dal pacchetto [xine-lib](https://www.archlinux.org/packages/?name=xine-lib).

Si noti che il progetto xine fornisce anche un lettore video, [xine-ui](https://www.archlinux.org/packages/?name=xine-ui).

### libavcodec

[libavcodec](/index.php/FFmpeg "FFmpeg") è parte del progetto [FFmpeg](http://ffmpeg.org/). Esso comprende un gran numero di codec video e audio. I codec libavcodec sono inclusi con i lettori multimediali come [MPlayer](/index.php/MPlayer_(Italiano) "MPlayer (Italiano)") e [VLC](/index.php/VLC "VLC"), quindi potrebbe non essere necessario installare il pacchetto ffmpeg.

## Trucchi e Soluzioni

### Installare codec binari per MPlayer

Una soluzione definitiva potrebbe essere quella di installare i codec binari per MPlayer.

Se non si riesce a riprodurre alcuni file, visitare la pagina [http://www.mplayerhq.hu/design7/dload.html](http://www.mplayerhq.hu/design7/dload.html), leggere le istruzioni e installare il codec necessario a riprodurre il file.

Inoltre possono essere installati tramite il pacchetto [codecs](https://aur.archlinux.org/packages/codecs/) e [codecs64](https://aur.archlinux.org/packages/codecs64/), disponibili su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").

### H264, mpg4 o Musepack (.mpc) mancante in Totem Player

Se viene visualizzato l'avviso "Il plugin H264 è mancante" con il lettore multimediale Totem, è sufficiente installare la libreria Gstreamer libav ([gst-libav](https://www.archlinux.org/packages/?name=gst-libav)), per risolvere il problema.