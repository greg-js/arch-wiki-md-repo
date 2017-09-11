**MPlayer** è un famosissimo lettore multimediale per Linux. MPlayer supporta praticamente tutti i formati audio e video, risultando quindi un lettore molto versatile, anche se la maggior parte delle persone lo usa solo come lettore video.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Consigli di installazione addizionali](#Consigli_di_installazione_addizionali)
    *   [2.1 Interfacce grafiche/GUI](#Interfacce_grafiche.2FGUI)
    *   [2.2 Integrazione con i Browser](#Integrazione_con_i_Browser)
        *   [2.2.1 Firefox](#Firefox)
        *   [2.2.2 Konqueror](#Konqueror)
        *   [2.2.3 Chromium](#Chromium)
*   [3 Uso di MPlayer](#Uso_di_MPlayer)
    *   [3.1 Configurazione](#Configurazione)
    *   [3.2 Scorciatoie da tastiera](#Scorciatoie_da_tastiera)
*   [4 Trucchi e consigli](#Trucchi_e_consigli)
    *   [4.1 Riprendi da dove si è interrotta la visualizzazione](#Riprendi_da_dove_si_.C3.A8_interrotta_la_visualizzazione)
    *   [4.2 Abilitare VDPAU (solo per schede grafiche nVidia moderne)](#Abilitare_VDPAU_.28solo_per_schede_grafiche_nVidia_moderne.29)
        *   [4.2.1 Usare il file di configurazione](#Usare_il_file_di_configurazione)
        *   [4.2.2 Usare uno script](#Usare_uno_script)
    *   [4.3 Video traslucente con Radeon e Composite abilitato](#Video_traslucente_con_Radeon_e_Composite_abilitato)
    *   [4.4 Problemi video Smplayer](#Problemi_video_Smplayer)
    *   [4.5 (S)mplayer fallisce la ripresa dopo una pausa](#.28S.29mplayer_fallisce_la_ripresa_dopo_una_pausa)
    *   [4.6 Trasparenza di SMPlayer in GNOME con Composite abilitato](#Trasparenza_di_SMPlayer_in_GNOME_con_Composite_abilitato)
    *   [4.7 SMPlayer: i font di OSD sono troppo grossi/i sottotitoli sono troppo piccoli](#SMPlayer:_i_font_di_OSD_sono_troppo_grossi.2Fi_sottotitoli_sono_troppo_piccoli)
    *   [4.8 Vedere video in streaming](#Vedere_video_in_streaming)
    *   [4.9 Abilitare il supporto a dvdnav](#Abilitare_il_supporto_a_dvdnav)
    *   [4.10 Andare avanti e indietro in un file in scaricamento](#Andare_avanti_e_indietro_in_un_file_in_scaricamento)
    *   [4.11 Incrementare il volume totale](#Incrementare_il_volume_totale)
    *   [4.12 Stream audio jack](#Stream_audio_jack)
    *   [4.13 Mplayer fallisce nell'apertura di file con spazi o caratteri strani nel nome](#Mplayer_fallisce_nell.27apertura_di_file_con_spazi_o_caratteri_strani_nel_nome)
*   [5 Links Esterni](#Links_Esterni)

## Installazione

MPlayer è disponibile nel [repository [extra]](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

*   [mplayer](https://www.archlinux.org/packages/?name=mplayer): il pacchetto "standard".
*   [mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/): una versione di MPlayer con il supporto a VAAPI.
*   [mplayer2](https://aur.archlinux.org/packages/mplayer2/): un [fork di MPlayer](http://www.mplayer2.org/) con numerose caratteristiche in più.

In alternativa, è possibile installare le ultime versioni in sviluppo da [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)"):

*   [mplayer-svn](https://aur.archlinux.org/packages/mplayer-svn/): versione in sviluppo di MPlayer.
*   [mplayer2-git](https://aur.archlinux.org/packages/mplayer2-git/): versione in sviluppo di MPlayer2.

Per le differenze fra MPlayer e MPlayer2 consultare questo articolo: [MPlayer2 vs MPlayer](http://www.mplayer2.org/differences/).

## Consigli di installazione addizionali

### Interfacce grafiche/GUI

Ci sono diverse interfacce grafiche per MPlayer.

*   **[SMPlayer](https://en.wikipedia.org/wiki/SMPlayer "wikipedia:SMPlayer")** — Un front-end in Qt per mplayer con alcune patches.

	[http://smplayer.sourceforge.net/](http://smplayer.sourceforge.net/) || [smplayer](https://www.archlinux.org/packages/?name=smplayer)

*   **UMPlayer** — Un fork di SMPlayer con più features (Temi CSS, integrazione con YouTube, supporto a ShoutCast, etc.)

	[http://www.umplayer.com/](http://www.umplayer.com/) || [umplayer](https://aur.archlinux.org/packages/umplayer/)

*   **GNOME-MPlayer** — Un semplice frontend in GTK per MPlayer.

	[http://kdekorte.googlepages.com/gnomemplayer](http://kdekorte.googlepages.com/gnomemplayer) || [gnome-mplayer](https://www.archlinux.org/packages/?name=gnome-mplayer)

*   **Pymp** — Front-end in PyGTK per MPlayer

	[http://jdolan.dyndns.org/trac/wiki/Pymp](http://jdolan.dyndns.org/trac/wiki/Pymp) || [pymp](https://aur.archlinux.org/packages/pymp/)

*   **KMPlayer** — Un player video, plugin for Konqueror, frontend per MPlayer/Xine/ffmpeg/ffserver/VDR per KDE.

	[http://kmplayer.kde.org/](http://kmplayer.kde.org/) || [kmplayer](https://www.archlinux.org/packages/?name=kmplayer)

*   **Xt7-Player** — Una GUI per mplayer scritta in Gambas, con una lunga lista di features.

	[http://xt7-player.sourceforge.net/xt7forum/](http://xt7-player.sourceforge.net/xt7forum/) || [xt7-player](https://aur.archlinux.org/packages/xt7-player/)

### Integrazione con i Browser

Se desiderate che Mplayer si occupi di riprodurre i video sul web nel vostro browser preferito, provate le seguenti:

#### Firefox

Il plugin per [Firefox](/index.php/Firefox_(Italiano) "Firefox (Italiano)") si chiama [gecko-mediaplayer](https://www.archlinux.org/packages/?name=gecko-mediaplayer) e si trova nei [repositories ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

**Note:** Dipende da [gnome-mplayer](https://www.archlinux.org/packages/?name=gnome-mplayer) il quale provvede anche a una completa GUI per MPlayer

#### Konqueror

Il pacchetto [kmplayer](https://www.archlinux.org/packages/?name=kmplayer) è disponibile il [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").

**Note:** il pacchetto fornisce anche un'ulteriore interfaccia a MPlayer.

#### Chromium

Il plugin per Firefox [gecko-mediaplayer](https://www.archlinux.org/packages/?name=gecko-mediaplayer) funziona egregiamente anche su [Chromium](/index.php/Chromium "Chromium").

## Uso di MPlayer

### Configurazione

Il file di configurazione generale (valido per tutti gli utenti) si trova in `/usr/local/etc/mplayer/mplayer.conf`, mentre le configurazioni personalizzate per gli utenti sono memorizzate nel file `~/.mplayer/config`.

Un esempio di configuratione:

 `/etc/mplayer/example.conf` 
```
# *[default]* viene applicata a ogni file
[default]
# usa il server grafico X come video output
vo=xv
# usa alsa per l'audio output
ao=alsa
# ao=oss # Use OSS4
# decodifica multithreaded H264/MPEG-1/2 (valido: 1-8)
lavdopts=threads=2
# impostare il canale audio preferito (in questo esempio il numero sei)
channels = 6
# scala i sottotitoli al 3% della dimensione dello schermo
subfont-text-scale = 3
# non usa fontconfig
nofontconfig = 1
# aggiunge bordi neri ai filmati che non hanno lo stesso aspetto di forma dello schermo
# per wide screen monitors
vf-add=expand=::::1:16/9:16
# per non wide screen traditional monitors
#vf-add=expand=::::1:4/3:16

#profilo di *up-mixing* da due canali audio a sei canali
# use -profile 2chto6ch to activate
[2chto6ch]
af-add=pan=6:1:0:.4:0:.6:2:0:1:0:.4:.6:2

#profilo di *down-mixing* da sei canali audio a due canali
# use -profile 6chto2ch to activate
[6chto2ch]
af-add=pan=2:0.7:0:0:0.7:0.5:0:0:0.5:0.6:0.6:0:0

# Disabilita screensaver
heartbeat-cmd="xscreensaver-command -deactivate &" # stop xscreensaver
stop-xscreensaver="yes" # stop gnome-screensaver
```

### Scorciatoie da tastiera

Le scorciatoie da tastiera di MPlayer sono configurate in `/etc/mplayer/input.conf`. Per personalizzare la scorciatoie da tastiera editare il file `~/.mplayer/input.conf` Ecco una lista dei più basilari tasti di default per controllare MPlayer. Per la lista completa si cerchi nelle pagine *man*: [mplayer(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mplayer.1).

| Tasto | Descrizione |
| `p` | Mette in pausa/esegue. |
| `Barra Spaziatrice` | Toglie la pausa/esegue. |
| `←` | Manda indietro 10 secondi. |
| `→` | Manda avanti 10 secondi. |
| `↓` | Manda indietro 1 minuto. |
| `↑` | Manda avanti 1 minuto. |
| `<` | Va indietro nella playlist. |
| `>` | Va avanti nella playlist. |
| `m` | Mette in muto. |
| `0` | Aumenta il volume. |
| `9` | Abbassa il volume. |
| `f` | Mette\Toglie la modalità a schermo intero. |
| `o` | Cambia lo stato dell OSD. |
| `v` | Mette\toglie la visibilità dei sottotitoli. |
| `I` | Mostra il nome del file. |
| `1`, `2` | Regola il contrasto. |
| `3`, `4` | Regola la luminosità. |

## Trucchi e consigli

### Riprendi da dove si è interrotta la visualizzazione

Su [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)") si trova un elegante script in perl che permette questa utile funzionalità: [mplayer-resumer](https://aur.archlinux.org/packages/mplayer-resumer/).

L'utilizzo è semplice: è sufficiente lanciare il video usando *mplayer-resumer* al posto di *mplayer'. Esempio:*

```
$ mplayer-resumer [options] [path/]filename

```

Se lo script è riavviato con meno di 5 secondi di ritardo dalla chiusura di MPlayer, tale script potrebbe non funzionare e la visione ripartirà dall'inizio.

Se si sta guardando un video da una directory che per qualunque motivo non possa essere scritta (sia per motivi di permessi magari settati su read-only o spazio insufficiente) è probabile che non la ripresa da una pausa fallisca. Ciò è dato dal fatto che mplayer usa di default lo stesso percorso per scrivere un file parallelo di *conteggio* del tempo.

### Abilitare VDPAU (solo per schede grafiche nVidia moderne)

Per una lista completa dell'hardware compatibile con la tecnologia VDPAU controllare [questa tabella](https://en.wikipedia.org/wiki/PureVideo#Table_of_PureVideo_.28HD.29_GPUs e seguire uno dei due seguenti metodi per abilitare VDPAU di default ad ogni avvio di mplayer.

#### Usare il file di configurazione

Aggiungere queste righe al file di configurazione globale `/etc/mplayer/mplayer.conf` o specifico dell'utente `~/.mplayer/config`:

```
vo=vdpau,
vc=ffh264vdpau,ffmpeg12vdpau,ffodivxvdpau,ffwmv3vdpau,ffvc1vdpau,

```

**Nota:** Le virgole sono importanti! Trasmettono a mplayer quali codec usare.

**Attenzione:** ffodivxvdpau funziona solo con hardware molto recente. Valutare caso per caso se abilitarlo o no.Vedere [la relativa pagina NVIDIA](/index.php/NVIDIA_(Italiano)#Abilitare_Video_HD_.28VDPAU.2FVAAPI.29 "NVIDIA (Italiano)") per maggiori informazioni.

#### Usare uno script

Su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") esiste un semplice script in bash ([mplayer-vdpau-auto](https://aur.archlinux.org/packages/mplayer-vdpau-auto/)) che rileva automaticamente come settare *vc* quando *vo=vdpau*.

Un altro semplice wrapper è [mplayer-vdpau-shell-git](https://aur.archlinux.org/packages/mplayer-vdpau-shell-git/) in grado di evitare l'errore "VDPAU FATAL". Tale wrapper usa l'opzione *-include* per includere il supporto a VDPAU, quindi sarebbe meglio evitare di inserire la configurazione di VDPAU in `~/.mplayer/config`.

### Video traslucente con Radeon e Composite abilitato

Per avere un video traslucente lanciare mplayer con:

```
$ mplayer -vo xv:adaptor=1 <File>

```

O aggiungere questa riga a `~/.mplayer/config`:

```
vo=xv:adaptor=1

```

Si può usare *xvinfo* per vedere quali modalità video sono supportate dalla propria scheda video.

### Problemi video Smplayer

Smplayer può essere che abbia problemi ad aprire i file .mp4 (e forse anche .flv). Se aprendo un file con tali estensioni si nota che c'è solo l'audio, aprire `~/.mplayer/config` e aggiungere:

```
 [extension.mp4]
 demuxer=mov

```

Se il problema persiste eliminare il file di configurazione di smplayer:

```
 $ rm -rf ~/.config/smplayer/file_settings

```

### (S)mplayer fallisce la ripresa dopo una pausa

Questo succede se l' *audio output* è settato male nel file di configurazione di mplayer. Se si usa [PulseAudio](/index.php/PulseAudio_(Italiano) "PulseAudio (Italiano)") lanciare mplayer con l'opzione "-ao pulse" o editare `~/.mplayer/config` e aggiungere:

```
ao=pulse

```

Per Smplayer invece cambiare "Driver in uscita" in "Opzioni"-"Preferenze"-"Generale"-"Audio".

### Trasparenza di SMPlayer in GNOME con Composite abilitato

È ridicolo che usando smplayer con Compiz attivo non si riesca nè a vedere nè a sentire nulla. Per fixare questo problema editare il file:

 `/usr/bin/smplayer.helper` 
```
export XLIB_SKIP_ARGB_VISUALS=1
exec smplayer.real "$@"

```

e successivamente dare questi comandi in un terminale:

```
# chmod 755 /usr/bin/smplayer.helper
# mv /usr/bin/smplayer{,.real}
# ln -sf smplayer.helper /usr/bin/smplayer

```

### SMPlayer: i font di OSD sono troppo grossi/i sottotitoli sono troppo piccoli

Dalle release smplayer 0.8.2.1 / mplayer2 20121128-1, il rapporto fra le dimensione delle notifiche OSD e i sottotitoli è davvero strano, tanto che il testo di OSD occupi metà schermo e i sottotitoli siano troppo piccoli per essere letti. Questo problema è aggirabile aggiungendo:

```
-subfont-osd-scale 2

```

alle opzioni extra passate a MPlayer (in SMPlayer opzioni avanzate).

In alternativa aggiungere al file `~/.mplayer/config`:

```
subfont-osd-scale=2

```

### Vedere video in streaming

Per vedere un video in streaming (ad esempio un link *.asx) laciare così mplayer:

```
$ mplayer -playlist link-to-stream.asx

```

Per avviare lo stream, l'opzione '-playlist' è fondamentale.

### Abilitare il supporto a dvdnav

Per abilitare la funzionalità dei menu dei dvd riprodotti è necessario abilitare dvdnav. Lanciare mplayer così:

```
$ mplayer -nocache dvdnav://

```

### Andare avanti e indietro in un file in scaricamento

Per essere in grado di scorrere indietro (o avanti) un video in streaming aggiungere al file di configurazione:

```
idx=yes

```

### Incrementare il volume totale

Se il volume generale non è abbastanza elevato, è possibile incrementare il volume di mplayer così: attivare *softvol* e settare *softvol-max* in un range tra 10 a 10000.

```
softvol=1
softvol-max=600

```

### Stream audio jack

Per impostare l'uscita output di defaul su [JACK](/index.php/JACK "JACK"), editare `~/.mplayer/config` e aggiungere:

```
ao=jack

```

Se non si ha sempre inserito un JACK e si vuole che MPlayer usi tale uscita audio solo se presente, è possibile lanciare MPlayer in questo modo:

```
$ mplayer -ao jack [path]/nomefile

```

### Mplayer fallisce nell'apertura di file con spazi o caratteri strani nel nome

Se provate ad aprire un file con degli spazi nel nome (es "Il Film.avi") e mplayer fallisce, lamentandosi di non poter aprire il file (file:///Il%20Film.avi), dunque indicando tutti gli spazi convertiti in %20, allora aprite il file

```
/usr/share/applications/mplayer.desktop

```

con permessi di root e cambiate la riga

```
Exec=mplayer %U

```

in

```
Exec=mplayer '%F'

```

Se si ha una GUI modificare così:

```
Exec=nome_della_gui '%F'.

```

## Links Esterni

*   [Sito ufficiale di MPlayer](http://www.mplayerhq.hu/)
*   [FAQ di MPlayer](http://wiki.multimedia.cx/index.php?title=MPlayer_FAQ)
*   [Note su MPlayer](https://www.youtube.com/watch?v=n4Ul_A0VBVI)
*   [Tip per MPlayer](https://help.ubuntu.com/community/MPlayerTips)
*   [Come configurare MPlayer](http://how-to.wikia.com/wiki/How_to_configure_MPlayer)