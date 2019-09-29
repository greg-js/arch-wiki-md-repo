**MPD** (music player daemon) è un player audio con struttura client-server. MPD lavora in background come demone, gestisce le playlist e il database della musica e utilizza pochissime risorse. Per interfacciarsi con il demone è necessario un client. Maggiori informazioni possono essere reperite [sul sito di MPD](http://www.musicpd.org/).

*Attenzione* leggere anche la pagina ufficiale per l'installazione e la risoluzione dei problemi, lo sviluppatore principale ha indicato la nostra pagina wiki al suo stato attuale come piena di problemi (*"full of symptom killers"*), per cui la pagina ufficiale dovrebbe contenere informazioni più complete.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installare il demone](#Installare_il_demone)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Comportamento di MPD in una configurazione tipica](#Comportamento_di_MPD_in_una_configurazione_tipica)
    *   [2.2 File di configurazione minimo](#File_di_configurazione_minimo)
    *   [2.3 Configurare correttamente il suono](#Configurare_correttamente_il_suono)
    *   [2.4 Mixing software](#Mixing_software)
    *   [2.5 Modifica di mpd.conf](#Modifica_di_mpd.conf)
*   [3 Configurazione alternativa](#Configurazione_alternativa)
    *   [3.1 Configurazione veloce](#Configurazione_veloce)
    *   [3.2 Configurazione multi-demone](#Configurazione_multi-demone)
*   [4 Installazione del client](#Installazione_del_client)
*   [5 Funzionalità Extra](#Funzionalità_Extra)
    *   [5.1 Scrobbling su Last.fm](#Scrobbling_su_Last.fm)
        *   [5.1.1 mpdscribble](#mpdscribble)
        *   [5.1.2 Sonata & Ario](#Sonata_&_Ario)
        *   [5.1.3 lastfmsubmitd](#lastfmsubmitd)
    *   [5.2 Riproduzione da Last.fm con lastfmproxy](#Riproduzione_da_Last.fm_con_lastfmproxy)
    *   [5.3 Non riprodurre all'avvio](#Non_riprodurre_all'avvio)
        *   [5.3.1 Metodo 1](#Metodo_1)
        *   [5.3.2 Metodo 2](#Metodo_2)
        *   [5.3.3 Metodo 3](#Metodo_3)
    *   [5.4 MPD & ALSA](#MPD_&_ALSA)
        *   [5.4.1 Elevato utilizzo della CPU con ALSA](#Elevato_utilizzo_della_CPU_con_ALSA)
    *   [5.5 Controllare MPD con lirc](#Controllare_MPD_con_lirc)
    *   [5.6 Controllare MPD tramite cellulare bluetooth](#Controllare_MPD_tramite_cellulare_bluetooth)
    *   [5.7 MPD & PulseAudio](#MPD_&_PulseAudio)
*   [6 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [6.1 Autorilevamento fallito](#Autorilevamento_fallito)
    *   [6.2 Permessi di esecuzione](#Permessi_di_esecuzione)
        *   [6.2.1 Soluzione alternativa](#Soluzione_alternativa)
        *   [6.2.2 Altra soluzione alternativa](#Altra_soluzione_alternativa)
    *   [6.3 Evitare i timeout](#Evitare_i_timeout)
    *   [6.4 Impostare le codifiche](#Impostare_le_codifiche)
    *   [6.5 Controllare MPD in rete](#Controllare_MPD_in_rete)
    *   [6.6 Streaming](#Streaming)
    *   [6.7 mpd --create-db si blocca](#mpd_--create-db_si_blocca)
        *   [6.7.1 Easy Tag](#Easy_Tag)
        *   [6.7.2 KID3](#KID3)
    *   [6.8 Cannot connect to mpd: host "localhost" not found: Temporary failure in name resolution](#Cannot_connect_to_mpd:_host_"localhost"_not_found:_Temporary_failure_in_name_resolution)
    *   [6.9 Port 6600 already in use](#Port_6600_already_in_use)
    *   [6.10 Crepitii con alcuni file audio](#Crepitii_con_alcuni_file_audio)
    *   [6.11 daemon: cannot setgid for user "mpd": Operation not permitted](#daemon:_cannot_setgid_for_user_"mpd":_Operation_not_permitted)
*   [7 Riferimenti esterni](#Riferimenti_esterni)

## Installare il demone

Il demone è disponibile nel repository "extra", è quindi possibile installarlo con [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)"):

```
# pacman -S mpd

```

## Configurazione

Per maggiori informazioni sulla configurazione di MPD visitare [http://mpd.wikia.com/wiki/Configuration](http://mpd.wikia.com/wiki/Configuration).

### Comportamento di MPD in una configurazione tipica

1.  MPD viene avviato al boot da `/etc/rc.conf`, includendolo nell'array `DAEMONS`. (In alternativa può essere avviato manualmente lanciando `/etc/rc.d/mpd start` con privilegi di root).
2.  Essendo stato lanciato come root, MPD per prima cosa legge il file `/etc/mpd.conf`.
3.  MPD individua l'utente di esecuzione dal file `/etc/mpd.conf`, e cambia la proprietà del processo da root a questo utente.
4.  Una volta cambiata la proprietà, MPD analizza i contenuti di `/etc/mpd.conf` si configura di conseguenza.

Si noti che MPD cambia l'utente attivo da root a quello menzionato in `/etc/mpd.conf`. In questo modo, l'uso di `~` nel file di configurazione punta correttamente alla directory home dell'utente, e non a quella di root. Potrebbe valer la pena di sostituire tutte le occorrenze di `~` con `/home/username` per evitare ogni confusione con questo particolare comportamento di MPD.

### File di configurazione minimo

*   Come root, verificare se il file `/etc/mpd.conf` esiste e, nel caso, eliminarlo. Questo è sicuro e consigliato.

MPD crea un file di configurazione di esempio, situato in `/usr/share/doc/mpd/mpd.conf.example`. Questo file contiene moltissime informazioni sulla configurazione di MPD, oltre ad alcuni valori del mixer di default che possono semplicemente essere commentati.

*   Come root, copiare questo file di esempio in `/etc/mpd.conf`.

```
# cp /usr/share/mpd/mpd.conf.example /etc/mpd.conf

```

(`/usr/share/doc/mpd/mpd.conf.example` è un ottimo punto di partenza per una orientata al singolo utente)

Mai mettere questo file nella home dell'utente come suggerito in altri tutorial. Questo complicherrebe le cose e molte volte è anche inutile (notare come si stia leggendo una guida per l'installazione veloce). Se è stato precedentemente creato un file `.mpdconf` nella propria home, cancellarlo adesso. Questo è importante per evitare conflitti di configurazione. Copiandolo in `/etc`, come fatto in questa guida, MPD sarà in grado di operare come demone all'avvio. Altrimenti sarebbe necessario uno script per lanciare MPD *dopo* il login dell'utente (ad esempio in kdm o `~/.fluxbox/startup`) oppure un avviamento manuale. Per una singola collezione musicale, il metodo qui descritto è semplicemente migliore, anche se la collezione è condivisa con più utenti. Inoltre, non bisogna preoccuparsi dei privilegi di root: anche quando MPD opera come demone, non opererà mai completamente come root in quanto automaticamente scarica i suoi privilegi di root dopo l'esecuzione.

### Configurare correttamente il suono

Per far funzionare l'audio assicurarsi di aver correttamente configurato la scheda audio e il mixer. Visitare [ALSA (Italiano)](/index.php/ALSA_(Italiano) "ALSA (Italiano)"). Non dimenticarsi di rimuovere il muto dai canali necessari in alsamixer, alzare il volume e salvare i cambiamenti con alsactl store. Visitare `~/.mpd/error` se ancora l'audio non funziona.

Assicurarsi che la propria scheda audio possa effettuare il mixing hardware (molte di esse possono, incluse quelle integrate). In caso contrario questo potrebbe causare problemi con le riproduzioni multiple. Per esempio, impedirebbe ad Mplayer di riprodurre il suono mentre il demone MPD è attivo, restituendo un messaggio di errore audio comunicante che il dispositivo è occupato.

### Mixing software

Per cambiare il volume dell'audio di MPD indipendentemente da altri programmi, decommentare o aggiungere in mpd.conf:

 `/etc/mpd.conf` 
```
mixer_type			"software"

```

### Modifica di `mpd.conf`

**Si mantiene la configurazione in /var e si utilizza "mpd" come utente predefinito invece di ingombrare ~/. Il pacchetto Arch è configurato in questo modo.**

Modificare `/etc/mpd.conf` nel seguente modo.

 `/etc/mpd.conf` 
```
music_directory       "/home/user/music"         # La directory della collezione musicale.
playlist_directory    "/var/lib/mpd/playlists"
db_file               "/var/lib/mpd/mpd.db"
log_file              "/var/log/mpd/mpd.log"
pid_file              "/var/run/mpd/mpd.pid"
state_file            "/var/lib/mpd/mpdstate"
user                  "mpd"
# bind_to_address e port causavano problemi in MPD-0.14.2
# meglio lasciare commentato
# bind_to_address       "127.0.0.1"
# port                  "6600"

```

Leggere i passaggi seguenti con attenzione, i permessi devono essere impostati correttamente.

*   Come utente creare i file specificati in `/etc/mpd.conf`, se le directory non esistono, crearle. Ciò non è richiesto se si usa la configurazione predefinita del pacchetto Arch.
*   Se la collezione musicale è contenuta in diverse directory, è possibile creare dei link simbolici in `/var/lib/mpd` e impostare 'music_dir' in `mpd.conf` alla directory contenente i link. Ricordare di impostare i permessi in accordo sulle directory linkate.
*   La creazione del database musicale si ottiene con la funzione "update" del client, ad esempio se si utilizza ncmpcpp è sufficiente premere 'u'.
    *   La funzione di creazione del database MPD da root (# mpd --create-db), è deprecata.

## Configurazione alternativa

MPD non ha bisogno di avviarsi con i permessi di root. L'unica ragione per cui MPD ha bisogno di essere avviato da root (venendo chiamato da `/etc/rc.conf`) è perché i file e le cartelle contenute nella configurazione di default puntano a directory di proprietà dell'utente root (la directory `/var`).Un approccio meno comune, ma forse più raffinato, è far lavorare MPD con file e directory di proprietà dell'utente normale. Avviare MPD come utente normale ha diversi vantaggi:

1.  Si può facilmente avere una singola directory `~/.mpd` (o una qualsiasi altra directory sotto `/home/username`) per tutti i file di configurazione di MPD
2.  Nessun errore causato da permessi di lettura/scrittura
3.  Chiamate ad MPD più flessibili usando `~/.xinitrc` invece di includere 'mpd' nell'array DAEMONS di `/etc/rc.conf`.

I seguenti passaggi illustrano come avviare MPD come utente normale. **Attenzione**: questo metodo non funzionerà se si desidera che più utenti possano accedere ad MPD.

*   Copiare i contenuti della configurazione di default di MPD da `/etc/mpd.conf.example` alla propria home. Una buona posizione potrebbe essere `"/home/user/.mpd/mpd.conf"`.
*   Seguire le istruzioni di configurazione più sopra, ignorando la prima parte riguardante la copia della configurazione in `/etc/mpd.conf`.
*   Creare tutti i file necessari in `"/home/user/.mpd/"`:

```
"~/.mpd/playlists"
"~/.mpd/db"
"~/.mpd/mpd.log"
"~/.mpd/mpd.error"
"~/.mpd/mpd.pid"
"~/.mpd/mpdstate"

```

*   Avviare MPD al boot chiamandolo dal proprio `~/.xinitrc` come segue:

```
# questo avvia MPD come utente normale
mpd /home/username/.mpd/mpd.conf

```

**Nota:** non c'è la necessita di inserire un "&" alla fine della riga precedente, in quanto MPD automaticamente si avvia come demone.

Infine, cancellare la voce 'mpd' dall'array DAEMONS in `/etc/rc.conf`, visto che non viene più avviato come root.

### Configurazione veloce

Il metodo più rapido per creare la struttura necessaria è eseguire il seguente comando:

```
$ mkdir -p ~/.mpd/playlists && touch ~/.mpd/database && cp /usr/share/doc/mpd/mpdconf.example ~/.mpd/mpd.conf

```

E successivamente modificare `mpd.conf` con i propri collegamenti. Attenzione che è necessario decommentare la voce db_file se è stato modificato `mpd.conf`.

Infine, avviare MPD:

```
$ mpd ~/.mpd/mpd.conf

```

### Configurazione multi-demone

**Utile se si desidera avviare, ad esempio, un server icecast.** Se si vuole un secondo demone MPD (ad esempio, con un output icecast per condividere la musica nella rete) che utilizzi la stessa musica e la stessa playlist di quello configurato come sopra, semplicemente copiare il file di configurazione qui sopra creato in un nuovo file (ad esempio, `/home/username/.mpd/config-icecast`), e modificare solo le voci log_file, error_file, pid_file, e state_file (ad esempio, `mpd-icecast.log`, `mpd-icecast.error`, e via di seguito); usare le stesse directory per la musica e le playlist assicura che questo secondo demone MPD utilizzerà la stessa collezione musicale del primo demone (quindi, creare e modificare una playlist dal primo demone influenzerà anche il secondo demone, così non sarà necessario creare la stessa playlist anche per il secondo demone). A questo punto, chiamare il secondo demone allo stesso modo del primo dal proprio `~/.xinitrc`. (Solo assicurarsi di utilizzare una porta differente, in modo da non causare conflitti con il primo demone).

## Installazione del client

Installare un programma client per MPD. Alcuni client comuni sono:

*   **mpc** – Client da linea di comando (la sua installazione è consigliata in ogni caso)

```
# pacman -S mpc

```

*   **ncmpc** – Client NCurses Client (estremamente utile da console) [Sito ufficiale di ncmpc](http://hem.bredband.net/kaw/ncmpc/)

```
# pacman -S ncmpc

```

*   **ncmpcpp** – Clone di ncmpc con funzioni aggiuntive scritto in C++ [Sito ufficiale di ncmpcpp](http://unkart.ovh.org/ncmpcpp/)

```
# pacman -S ncmpcpp

```

*   **pms** – Client NCurses altamente configurabile e di facile utilizzo [Sito ufficiale di pms](http://pms.sourceforge.net/)

```
Installare [pmus](https://aur.archlinux.org/packages/pmus/) da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").

```

*   **ario** – Client GTK+ con browser della libreria simile a Rhythmbox [Sito ufficiale di Ario](http://ario-player.sourceforge.net)

```
# pacman -S ario

```

*   **sonata** – Client GTK+ scritto in Python [Sito ufficiale di Sonata](http://sonata.berlios.de/)

```
# pacman -S sonata

```

*   **gmpc** – Client GNOME [Sito ufficiale di gmpc](http://gmpcwiki.sarine.nl/index.php?title=GMPC)

```
# pacman -S gmpc

```

*   **QMPDClient** – Client scritto in Qt 4.x. [Sito ufficiale di QMPDClient](http://bitcheese.net/wiki/QMPDClient)

```
# pacman -S qmpdclient

```

## Funzionalità Extra

### Scrobbling su Last.fm

Per eseguire lo scrobbling delle tracce su [Last.fm](http://www.last.fm) utilizzando MPD ci sono svariate alternative.

#### mpdscribble

mpdscribble è un'altro demone, ma è solo disponibile in [AUR](https://aur.archlinux.org/packages.php?ID=22274). Questa è probabilmente la migliore delle alternative, in quanto è lo scrobbler semi-ufficiale di MPD e utilizza la nuova funzione "idle" di MPD per uno scrobbling più accurato. Inoltre, non c'è bisogno dell'accesso root per configurarlo, perché non richiede nessuna modifica a `/etc`. Visitare [il sito ufficiale](http://mpd.wikia.com/wiki/Client:Mpdscribble) per maggiori informazioni.

Per ottenere mpdscribble, è sufficente installarlo dall'AUR ed eseguire i seguenti passaggi (non come root):

*   `$ mkdir ~/.mpdscribble`
*   Creare il file `~/.mpdscribble/mpdscribble.conf` e configurarlo come segue:

```
 [mpdscribble] 
 host = <host di mpd>
 port = <porta di mpd>
 log = ~/.mpdscribble/mpdscribble.log
 journal = ~/.mpdscribble/mpdscribble.cache
 verbose = 2
 sleep = 1
 musicdir = <directory della collezione>
 proxy = <il proxy> # opzionale, ad esempio http://uo.proxy:8080, di default vuoto

 [last.fm]
 # sezione last.fm, commentare se non si usa last.fm
 url = http://post.audioscrobbler.com # opzionale
 username = <username last>
 password = <password last.fm> # md5sum in alternativa: echo -n PASSWORD | md5sum | cut -f 1 -d " "

 [libre.fm]
 # sezione libre.fm, commentare se non si usa libre.fm
 url = http://turtle.libre.fm/
 username = <username libre.fm>
 password = <password libre.fm>

```

*   Aggiungere `mpdscribble` al proprio `~/.xinitrc`:

```
pidof mpdscribble >& /dev/null
if [ $? -ne 0 ]; then
  mpdscribble &
fi

```

Per chi non esegue il login direttamente da X, è possibile aggiungere mpdscribble all'array DAEMONS di `/etc/rc.conf`. Tuttavia in alcuni casi ciò non è sufficiente a garantire che mpdscribble venga eseguito all'avvio di sistema. Si può ovviare a questo inconveniente aggiungendo

```
mpdscribble &

```

a `/etc/rc.local`.

#### Sonata & Ario

La via più facile, se non è importante avere una finestra aperta tutto il tempo, è usare Sonata o Ario che sono frontend grafici a MPD. Hanno un supporto integrato per lo scrobbling su Last.fm nelle loro preferenze. Una nota negativa è che Sonata non salva una cache delle tracce se per qualche ragione non è disponibile una connessione internet durante la riproduzione.

#### lastfmsubmitd

lastfmsubmitd è un demone disponibile nel repository "community". Dopo averlo installato, per prima cosa modificare `/etc/lastfmsubmitd.conf` e aggiungere sia `lastfmsubmitd` che `lastmp` all'array `DAEMONS` in `/etc/rc.conf`.

### Riproduzione da Last.fm con lastfmproxy

lastfmproxy è uno script python che riproduce uno stream last.fm su un altro media player. Per configurarlo, installare [lastfmproxy](https://aur.archlinux.org/packages/lastfmproxy/) dall'[AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") e modificare `/usr/share/lastfmproxy/config.py`. Se si vuole riprodurre sono da MPD sullo stesso host, è sufficiente modificare le informazioni di login.

**Nota:** Visto che viene installato in una directory di sola lettura ma richiede permessi di lettura/scrittura per funzioni quali la memorizzazione delle stazioni precedentemente ascoltate, sarebbe saggio copiare `/usr/share/lastfmproxy` nella propria home.

Avviare lastfmproxy con `lastfmproxy` e visitare [http://localhost:1881/](http://localhost:1881/) nel proprio browser. Per aggiungere una stazione last.fm station navigare in [http://localhost:1881/](http://localhost:1881/) seguito da lastfm:// url. Esempio: [http://localhost:1881/lastfm://globaltags/punk](http://localhost:1881/lastfm://globaltags/punk) . Tornare in [http://localhost:1881/](http://localhost:1881/) e scaricare il file m3u selezionando il link *Start Listening*. Semplicemente aggiungere questo file alle playlist.

### Non riprodurre all'avvio

#### Metodo 1

Se non si desidera che MPD riproduca la playlist all'avvio del demone, ma si desidera preservare le altre informazioni di stato, aggiungere le righe seguenti al file `/etc/rc.d/mpd`:

```
 *...*
 *stat_busy "Avvio di Music Player Daemon"*

```

```
   # avviare sempre in pausa
   awk '/^state_file[ \t]+"[^"]+"$/ {
       match($0, "\".+\"")
       sfile = substr($0, RSTART + 1, RLENGTH - 2)
   } /^user[ \t]+"[^"]+"$/ {
       match($0, "\".+\"")
       user = substr($0, RSTART + 1, RLENGTH - 2)
   } END {
       if (sfile == "")
               exit;
       if (user != "")
               sub(/^~/, "/home/" user, sfile)
       system("sed -i \x27s|^\\(state:[ \\t]\\{1,\\}\\)play$|\\1pause|\x27 \x27" sfile "\x27")
   }' /etc/mpd.conf

```

```
 */usr/bin/mpd /etc/mpd.conf &> /dev/null*
 *...*

```

Questo imposterà il lettore in "pausa", se è stato fermato durante la riproduzione. Successivamente, se si vuole che questo file sia preservato, in modo che gli aggiornamenti di MPD non eliminino questa modifica, aggiungere o modificare la seguente linea in `/etc/pacman.conf`:

```
NoUpgrade = etc/rc.d/mpd

```

#### Metodo 2

Un metodo più semplice consiste nell'aggiungere mpd all'array DAEMONS di `[rc.conf](/index.php/Rc.conf "Rc.conf")` e aggiungere `mpc stop` oppure `mpc pause` a `/etc/rc.local.shutdown` e a `/etc/rc.local`. (Ricordarsi che è necessario avere mpc installato per sfruttare questo metodo).

Aggiungere il comando al solo `/etc/rc.local` non assicura che mpd non riproduca assolutamente nulla, in quanto potrebbe esserci un ritardo prima che il comando di stop sia eseguito. D'altro canto, se si aggiunge il comando unicamente a `/etc/rc.local.shutdown`, ci si assicura che mpd non riproduca nulla, fintantoché si spenga il sistema in modo corretto. Anche se sono ridondanti, aggiungerli a `/etc/rc.local` potrebbe servire per quelle, presumibilmente, rare occasioni in cui il sistema non si spenga in modo appropriato.

#### Metodo 3

L'idea di base di questo metodo è chiedere ad mpd di mettere in pausa la musica quando l'utente esegue il logout, così al prossimo avvio mpd si bloccherà nello stato di pausa. È possibile inviare questo comando usando [mpc](https://www.archlinux.org/packages/?name=mpc), l'interfaccia a linea di comando di mpd:

```
pacman -S mpc

```

Gli utenti di GDM possono aggiungere la riga seguente a `/etc/gdm/PostSession/Default` (assicurarsi di aggiungerla prima di "exit 0"):

```
/usr/bin/mpc pause

```

Gli altri utenti possono similmente utilizzare il loro login manager per lanciare il comando al logout.

### MPD & ALSA

A volte, quando si usano altri output audio, ad esempio alcune pagine web contenenti applet Flash, MPD non può riprodurre nulla fino al riavvio. L'errore, se si guarda `/var/log/mpd/mpd.error`, assomiglierà a:

```
Error opening alsa device "hw:0,0": Device or resource busy

```

E qui c'è la soluzione (dmix salva nuovamente la vita). Applicare le righe seguenti al proprio `/etc/mpd.conf`:

```
audio_output {
        type                    "alsa"
        name                    "Sound Card"
        options                 "dev=dmixer"
        device                  "plug:dmix"
}
```

E riavviare con `/etc/rc.d/mpd restart`.

Nel wiki di Gentoo si trovano alcune spiegazioni di tale inconveniente:

*   La scheda audio non supporta il mixing hardware (utilizza il plugin **dmix**)
*   Un'applicazione non è compatibile con ALSA nelle sue configurazioni di default

Per una descrizione dettagliata, si raccomanda di dare un'occhiata a [questo](http://mpd.wikia.com/wiki/Alsa) link. Qui è possibile trovare un esempio di `asound.conf` su cui basarsi per una corretta configurazione di ALSA.

#### Elevato utilizzo della CPU con ALSA

Quando si utilizza MPD con ALSA, è possibile che MPD impieghi molta CPU (circa il 20-30%). Questo è causato dal fatto che molte schede audio supportano i 48kHz mentre la maggior parte della musica è a 44kHz, costringendo quindi MPD a ricodificare la traccia. Questa operazione impiega molti cicli di CPU e un elevato utilizzo della stessa.

Per molti utenti il problema dovrebbe risolversi istruendo MPD a non ricodificare, aggiungendo `auto_resample "no"` alla sezione audio_output di `/etc/mpd.conf`. Tuttavia, ciò peggiorerà leggermente la qualità di alcune tracce.

Esempio da `mpd.conf`:

```
audio_output {
   type			"alsa"
   name			"My ALSA Device"
   auto_resample		"no"
}

```

Anche se non in modo drastico, abilitare mmap può accelerare le cose:

```
audio_output {
   type			"alsa"
   name			"My ALSA Device"
   use_mmap		"yes"
}

```

Alcuni utenti potrebbero anche voler comunicare a dmix di utilizzare i 44kHz. Maggiori informazioni su come migliorare le performance di MPD si possono trovare nel [wiki di MPD](http://mpd.wikia.com/wiki/Tuning)

### Controllare MPD con lirc

Esistono già alcuni client realizzati per interfacciare lircd e MPD, tuttavia, all'utilizzo pratico non sono molto utili in quanto le loro funzionalità sono estremamente limitate.

Si raccomanda di usare mpc con irexec. mpc è un player da linea di comando che invia un'istruzione a MPD ed esce immediatamente, il che è perfetto per irexec, il parser di comandi incluso in lirc. Ciò che irexec fa è lanciare uno specifico comando una volta ricevuto un controllo dal telecomando.

Prima di tutto, configurare il telecomando come indicato nell'articolo **[LIRC](/index.php/LIRC "LIRC")**.

Modificare il file di configurazione di lirc, usualmente situato in `~/.lircrc`, seguendo questa struttura base:

```
begin
     prog = irexec
     button = <button_name>
     config = <command_to_run>
     repeat = <0 or 1>
end

```

Un utile esempio:

```
## irexec
begin
     prog = irexec
     button = play_pause
     config = mpc toggle
     repeat = 0
end

begin
     prog = irexec
     button = stop
     config = mpc stop
     repeat = 0
end
begin
     prog = irexec
     button = previous
     config = mpc prev
     repeat = 0
end
begin
     prog = irexec
     button = next
     config = mpc next
     repeat = 0
end
begin
     prog = irexec
     button = volup
     config = mpc volume +2
     repeat = 1
end
begin
     prog = irexec
     button = voldown
     config = mpc volume -2
     repeat = 1
end
begin
     prog = irexec
     button = pbc
     config = mpc random
     repeat = 0
end
begin
     prog = irexec
     button = pdvd
     config = mpc update
     repeat = 0
end
begin
     prog = irexec
     button = right
     config = mpc seek +00:00:05
     repeat = 0
end
begin
     prog = irexec
     button = left
     config = mpc seek -00:00:05
     repeat = 0
end
begin
     prog = irexec
     button = up
     config = mpc seek +1%
     repeat = 0
end
begin
     prog = irexec
     button = down
     config = mpc seek -1%
     repeat = 0
end

```

mpc dispone di molte altre funzioni. [mpc(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mpc.1) per maggiori informazioni.

### Controllare MPD tramite cellulare bluetooth

È anche possibile controllare MPD (fino ad un certo punto) utilizzando un cellulare con bluetooth. È necessario eseguire le seguenti operazioni:

*   installare [remuco](http://remuco.sourceforge.net/index.php/Remuco) -- un controller wireless per molti media player Linux ([aur](https://aur.archlinux.org/packages.php?ID=25072))
*   trasferire il client remuco (file jar/jad) da `/usr/share/remuco/client/` al proprio telefono e installarlo
*   avviare `remuco-mpd` (come utente)
*   avviare remuco sul proprio cellulare, definire una nuova connessione bluetooth per remuco (connettere il cellulare se non è stato fatto prima) ed esplorare le sue capacità

Maggiori informazioni su remuco inclusa la risoluzione dei problemi si trovano nella sua [homepage](http://remuco.sourceforge.net/index.php/Remuco)

### MPD & PulseAudio

Modificare `/etc/mpd.conf`, e decommentare la sezione audio_output per la tipologia "pulse". Il server e le relative righe dovrebbero essere commentate a meno che non si sappia quello che si sta facendo.

Successivamente, aggiungere l'utente mpd (e il proprio se non è già stato fatto) ai gruppi pulse richiesti. Il gruppo pulse-access dovrebbe essere sufficiente, ma se si desidera aggiungere anche pulse-rt. Il gruppo "pulse" non sembra essere necessario.

```
# gpasswd -a mpd pulse-access
# gpasswd -a mpd pulse-rt

```

Infine, potrebbe essere necessario copiare `~/.pulse-cookie` dalla propria directory di lavoro di pulse alla propria directory di mpd. È probabile che sia `/var/lib/mpd` se si è seguita la prima parte di questo wiki. Questo probabilmente consentirà solo all'utente attuale di ascoltare MPD su pulse. Si dovrebbe considerare di lanciare pulse per tutti gli utenti se ciò non dovesse rivelarsi sufficiente.

## Risoluzione dei problemi

### Autorilevamento fallito

All'avvio, MPD cerca di rilevare il sistema e di configurare l'outout e il volume in accordo. Anche se nella maggior parte dei casi questo avviene senza problemi, in alcuni sistemi non succede. Potrebbe aiutare comunicare ad MPD cosa utilizzare come output e come mixer. Se è stato copiato `/etc/mpd.conf` da `/etc/mpd.conf.example` come precedentemente menzionato, basta semplicemente decommentare

per output su ALSA:

```
audio_output {
	type			"alsa"
	name			"My ALSA Device"
	device			"hw:0,0"	# optional
	format			"44100:16:2"	# optional
}

```

per mixer alsa:

```
mixer_type			"alsa"
mixer_device			"default"
mixer_control			"PCM"

```

**Nota:** in caso di problemi di permessi utilizzando ESD con MPD, lanciare questo come root:

```
# chsh -s /bin/true mpd

```

### Permessi di esecuzione

**Attenzione:** Questa azione non è sicura e potrebbe non essere necessaria.

MPD ha bisogno dei permessi di esecuzione su **TUTTE** le directory della collezione musicale (ad esempio se essa si trova al di fuori della home di mpd `/var/lib/mpd`). Di default `useradd` imposta i permessi della home come `1700 drwx------`. Potrebbe quindi esserci necessità di cambiare i permessi di `/home/user`. Ad esempio, se la collezione si trova in `/home/user/music`:

```
# chmod a+x /home/$USER
# chmod -R a+X /home/$USER/music

```

#### Soluzione alternativa

Una soluzione alternativa potrebbe essere quella di usare il gruppo dell'utente per condividere alcuni file, tra cui la collezione musicale. Per prima cosa rimuovere tutti i permessi per il gruppo e successivamente aggiungere al gruppo i permessi di lettura ed esecuzione di `home` e di `music`:

```
# chmod -R g-rwx /home/$USER
# chmod g+rx /home/$USER
# chmod -R g+rX /home/$USER/music

```

#### Altra soluzione alternativa

Un'altra alternativa è montare la collezione all'interno di una directory accessibile a MPD. È meno rischioso per la sicurezza minore di modificare i permessi della home di un utente:

```
# mkdir /var/lib/mpd/music
# echo "/home/$USER/music /var/lib/mpd/music none bind" >> /etc/fstab
# mount -a

```

Infine riavviate il demone. Vedere anche [questo thread](https://bbs.archlinux.org/viewtopic.php?id=86449) del forum inglese.

### Evitare i timeout

Per sbarazzarsi dei timeout (ad esempio, quando si mette in pausa per lungo tempo) in gpmc e altri client, decommentare ed incrementare l'opzione `connection_timeout` in `mpd.conf`.

### Impostare le codifiche

Se i file o i titoli sono mostrati con una codifica non corretta, decommentare e modificare le opzioni `filesystem_charset` e `id3v1_encoding`.

**Nota:** Non è possibile impostare la codifica per i tag ID3 v2\. Per risolvere questo inconveniente è possibile utilizzare [lettori di tag esterni](http://mpd.wikia.com/wiki/GenericDecoder#Generic_Tagreader).

### Controllare MPD in rete

Se si desidera controllare MPD tramite un altro computer in rete, l'opzione `bind_to_address` in `mpd.conf` dovrà essere impostata all'indirizzo IP desiderato, oppure ad `any` se l'IP cambia in continuamente. Ricordarsi di aggiungere mpd al file `/etc/hosts.allow` per permettere l'accesso esterno.

### Streaming

Dalla versione 0.15 di MPD è disponibile lo streaming http.

Per attivare questa funzionalità, è necessario aggiungere un nuovo output di tipo httpd in `mpd.conf`:

```
audio_output {
          type   "httpd"
          name   "What you want"
          encoder "lame"     # supportati vorbis o lame
          port    "8000"
          bitrate  "128"
          format   "44100:16:2"  # impostare a 2 per MONO
  }

```

Riavviare il demone MPD e, da un altro computer, semplicemente caricare lo stream come qualsiasi altro URL:

```
$ mplayer http://<IP DEL SERVER>:8000

```

**Nota:** Bisogna aprire la porta sul router/firewall perché ci si possa connettere allo stream da un altro computer.

Molti lettori, come vlc o xmms2, dovrebbero essere in grado di aprire lo stream da un opzione del menu come "add url...".

Questo è un metodo semplice e pulito per rimpiazzare un setup di icecast con qualcosa di nativamente supportato da MPD.

### mpd --create-db si blocca

Questo è un errore comune causato da tag mp3 corrotti. Di seguito un metodo sperimentale per risolvere questo problema. Necessari:

*   kid3
*   easytag

Questo metodo è estremamente tedioso, specialmente con un grande database. Giusto come riferimento, sono necessario 2 ore e mezza per sistemare un database da 16Gb.

#### Easy Tag

Lo funzione di easytag è individuare l'errore nel tag, ma come MPD si blocca e termina. Il trucco è che easytag indica il file che causa il problema nella barra di stato. Prima di avviare easytag ci si assicuri di avere un terminale a portata di mano per killare easytag in modo da evitare che si blocchi. Una volta pronti, nella vista ad albero selezionare le directory contenenti la libreria. Easytag comincerà a nelle sottodirectory i file mp3\. Appena si nota che easytag si ferma, prendere nota del file e killare il processo.

#### KID3

Con kid3 spostarsi al file in questione e riscrivere uno dei tag, poi salvare il file. Questo costringe kid3 a riscrivere tutto il tag risolvendo il problema del blocco con MPD e easytag.

Ripetere la procedura fino alla riparazione di tutti i file corrotti.

### Cannot connect to mpd: host "localhost" not found: Temporary failure in name resolution

Impossibile connettersi a MPD (con ncmpcpp), se non si è connessi alla rete. La soluzione è [disabilitare il modulo IPv6](/index.php/IPv6_-_Disabling_the_Module "IPv6 - Disabling the Module") oppure aggiungere la seguente linea a `/etc/hosts`:

```
::1 localhost.localdomain localhost

```

### Port 6600 already in use

MPD ha bisogno di collegarsi alla porta 6600 e non può avviarsi se questa è già in uso. La ragione più comune per questo errore è che l'utente ha già avviato MPD e successivamente ha lanciato `mpd --create-db`. Il nuovo comportamento di mpd è che l'opzione `--create-db` tenta anche di avviare il demone; se questo è già stato avviato, l'operazione fallisce. Se questo è il caso, provare:

```
$ mpd --kill
$ mpd --create-db

```

Un approccio più brutale:

```
$ killall mpd
$ mpd --create-db

```

**Nota:** Se tipicamente si lancia MPD come root, i comandi precedenti sono da eseguire come root..

Nella versione git di MPD, `mpd --create-db` è completamente deprecata. Il database verrà creato automagicamente al primo avvio e successivamente si aggiornerà tramite il client (ad esempio `mpc update`). Inoltre, il supporto a inotify fornisce un aggiornamento completamente automatico quando si aggiunge qualcosa alla propria collezione.

Se la porta 6600 è bloccata per qualche ragione, si può usare il seguente comando per identificare il processo bloccante:

```
# ss -tulpan | grep 6600

```

Questo mostrerà IP:Porta e nome del processo detenente la connessione (servono i privilegi di root per vedere tutti i processi).

### Crepitii con alcuni file audio

Questo è solitamente un problema di velocità di riproduzione e si può risolvere decommentando e modificando la riga audio_output_format in:

 `/etc/mpd.conf`  `audio_output_format "44100:16:2"` 

Solitamente questi sono valori adatti per la maggior parte dei file mp3.

### daemon: cannot setgid for user "mpd": Operation not permitted

Questo errore afferma che l'utente che avvia il processo non ha il permesso di diventare l'altro utente (mpd) che la configurazione ha indicato come proprietario del processo. Per risolvere, semplicemente avviare mpd come root.

## Riferimenti esterni

*   [Sito ufficale](http://www.musicpd.org/)
*   [Wiki ufficiale](http://mpd.wikia.com/wiki/Main_Page)
*   [Lista ordinata di client MPD](http://mpd.wikia.com/wiki/Clients)
*   [Forum MPD](http://www.musicpd.org/forum/)