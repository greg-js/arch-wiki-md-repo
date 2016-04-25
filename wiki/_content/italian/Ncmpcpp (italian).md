## Contents

*   [1 Introduzione](#Introduzione)
*   [2 Installazione](#Installazione)
*   [3 Configurazione (molto) basilare](#Configurazione_.28molto.29_basilare)
*   [4 Abilitare la visualizzazione](#Abilitare_la_visualizzazione)
*   [5 Utilizzo di base](#Utilizzo_di_base)
    *   [5.1 Caricare ncmpc++](#Caricare_ncmpc.2B.2B)
    *   [5.2 Impostare le scorciatoie da tastiera](#Impostare_le_scorciatoie_da_tastiera)
    *   [5.3 Altre visuali](#Altre_visuali)
    *   [5.4 Altre scorciatoie da tastiera](#Altre_scorciatoie_da_tastiera)
    *   [5.5 Modalità di riproduzione](#Modalit.C3.A0_di_riproduzione)

## Introduzione

[Ncmpcpp](http://unkart.ovh.org/ncmpcpp/) o ncmpc++ è un client [Mpd](/index.php/Music_Player_Daemon_(Italiano) "Music Player Daemon (Italiano)") che ha un'intefaccia utente molto simile a quella di ncmpc, ma che mette a disposizione delle utilità aggiuntive come il supporto ad espressioni regolari nel motore di ricerca, formato esteso per le canzoni, filtro degli oggetti, supporto a last.fm, possibilità di ordinare le playlist, un browser per le cartelle locali, oltre a funzioni minori aggiuntive. Per usarlo, [mpd](/index.php/Music_Player_Daemon_(Italiano) "Music Player Daemon (Italiano)") deve essere installato e funzionante sul sistema, poiché ncmpcpp e mpd lavorano insieme in rapporto client/server.

L'interfaccia grafica (GUI) da shell per ncmpcpp è altamente configurabile. È sufficiente modificare `~/.ncmpcpp/config` secondo le proprie prederenze. Per qualche esempio, consultare i seguenti link:

*   [Show your .ncmpcpp/config with Screenshot forum thread](https://bbs.archlinux.org/viewtopic.php?id=66488)
*   [Project screenshots page](http://unkart.ovh.org/ncmpcpp/screenshots.php)

## Installazione

[ncmpcpp](https://www.archlinux.org/packages/?name=ncmpcpp) si [installa](/index.php/Pacman_(Italiano) "Pacman (Italiano)") dai [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

## Configurazione (molto) basilare

Dopo l'installazione è possibile trovare un semplice file di configurazione in /usr/share/doc/ncmpcpp/config

Nel caso in cui, dopo l'installazione, ~/.ncmpcpp/config non sia stato creato, è possibile copiare e modificare la configurazione d'esempio in particolare le tre opzioni seguenti:

*   mpd_host (deve indicare l'host su cui si trova mpd: può essere "localhost" o "127.0.0.1" se è sullo stesso sistema)
*   mpd_port (a meno che non sia stato cambiato quello di default in mpd, dovrebbe essere "6600")
*   mpd_music_dir (la stessa cartella "music_directory" indicata in mpd.conf)

## Abilitare la visualizzazione

Per abilitare la visualizzazione, è necessario il pacchetto [ncmpcpp-git](https://aur.archlinux.org/packages/ncmpcpp-git/) da [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)"). Una volta compilato, è necessario aggiungere delle righe a `/etc/mpd.conf` (o `$HOME/.mpd/mpd.conf`, nel caso in cui [si avvii mpd come utente](/index.php/Music_Player_Daemon_(Italiano)#Configurazione_alternativa "Music Player Daemon (Italiano)")) per abilitare la generazione dei dati [fast Fourier transform](https://it.wikipedia.org/wiki/Trasformata_di_Fourier_veloce) per la visualizzazione:

```
audio_output {
      type            "fifo"
      name            "My FIFO"
      path            "/tmp/mpd.fifo"
      format          "44100:16:2"
}

```

Delle altre righe devono essere poi aggiunte a `~/.ncmpcpp/config`

```
visualizer_fifo_path = "/tmp/mpd.fifo"
visualizer_output_name = "My FIFO"
visualizer_sync_interval = "1"
#visualizer_type = "wave" (spectrum/wave)
visualizer_type = "spectrum" (spectrum/wave)

```

È possibile scegliere tra un analizzatore dello spettro (spectrum) o una forma d'onda (wave).

## Utilizzo di base

### Caricare ncmpc++

Caricare ncmpc++ in una shell

```
$ ncmpcpp

```

### Impostare le scorciatoie da tastiera

Una lista di tasti e delle loro rispettive funzioni è disponibile all'interno dello stesso ncmpcpp semplicemente premendo `1`. L'utente può modificare le impostazioni predefinite per un tasto qualunque copiando `/usr/share/doc/ncmpcpp/keys` in ~/.ncmpcpp ed editandolo.

### Altre visuali

Ecco una lista parziale delle visuali alternative in ncmpc++

*   `0` - Orologio
*   `1` - Aiuto
*   `2` - Playlist attuale
*   `3` - Filesystem browser
*   `4` - Ricerca nel database
*   `5` - Libreria
*   `6` - Editor della playlist
*   `7` - Editor dei tag (molto performante!)
*   `9` - Modalità visuale

### Altre scorciatoie da tastiera

*   `\` - Passa da visualizzazione classica ad alternativa
*   `#` - Mostra il bitrate del file
*   `i` - Mostra informazioni della canzone
*   `I` - Mostra informazioni sull'artista (salvate in `~/.ncmpcpp/artists/ARTIST.txt`)
*   `L` - Scorre i database dei testi disponibili
*   `l` - Recupera i testi per la canzone corrente; Mostra/nasconde i testi

**Note:** Come già menzionato, la visualizzazione non è abilitata nel pacchetto ncmpcpp dei repo. È necessaria la versione git da AUR.

### Modalità di riproduzione

Facciamo attenzione al pannello di controllo in alto a destra: mostrato in modalità altenative:

```
1:40/7:38 1082 kbps                            ──┤ Hatred ├──                                       Vol: 98%
[playing]                             Manowar - Into glory ride (1983)                              **[-z-c--]**

```

e poi ancora nella modalità classica:

```
─────────────────────────────────────────────────────────────────────────────────────────────────────────**[zc]**─

```

Questo corrisponde alle modalità di riproduzione; ordinandole da sinistra a destra, sono:

*   `r` - ripetizione **[r-----]**
*   `z` - riproduzione casuale **[-z----]**
*   `y` - riproduzione singola **[--s---]**
*   `R` - riproduzione ad esaurimento **[---c--]**
*   `x` - riproduzione incrociata (crossfade) **[----x-]**

L'ultimo "-" è attivo solo quando l'utente forza l'update del database premendo `u`.