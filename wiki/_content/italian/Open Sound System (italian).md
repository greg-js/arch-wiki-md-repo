Questo articolo spiega come installare e configurare l' **O**pen **S**ound **S**ystem (OSS) sul tuo computer.

L' [Open Sound System](https://it.wikipedia.org/wiki/Open_Sound_System) è un'architettura audio per i sistemi derivati da UNIX e POSIX-compatibili. La versione 3 di OSS é stata la versione originale usata per il sistema audio di Linux ed è inserita nel kernel ma nel 2002 fu rimpiazzata da ALSA quando la versione 4 di OSS divenne software proprietario. OSSv4 è ritornata software libero nel 2007 quando [4Front Technologies](http://www.opensound.com/) ha rilasciato il suo codice sorgente con licenza GPL.

## Contents

*   [1 Confronto con ALSA](#Confronto_con_ALSA)
    *   [1.1 Vantaggi di OSS (utenti)](#Vantaggi_di_OSS_.28utenti.29)
    *   [1.2 Vantaggi di OSS (sviluppatori)](#Vantaggi_di_OSS_.28sviluppatori.29)
    *   [1.3 Vantaggi di ALSA](#Vantaggi_di_ALSA)
*   [2 Installazione](#Installazione)
*   [3 Testing](#Testing)
*   [4 Regolazione del Volume](#Regolazione_del_Volume)
    *   [4.1 Definizione dei Colori](#Definizione_dei_Colori)
    *   [4.2 Salvare i Livelli del Mixer](#Salvare_i_Livelli_del_Mixer)
    *   [4.3 Altri Mixer](#Altri_Mixer)
*   [5 Configurare le Applicazioni per OSS](#Configurare_le_Applicazioni_per_OSS)
    *   [5.1 Skype](#Skype)
    *   [5.2 Wine](#Wine)
    *   [5.3 Gajim](#Gajim)
    *   [5.4 MOC](#MOC)
    *   [5.5 Applicazioni che usano Gstreamer](#Applicazioni_che_usano_Gstreamer)
    *   [5.6 Firefox >=3.5](#Firefox_.3E.3D3.5)
    *   [5.7 Mplayer](#Mplayer)
    *   [5.8 Music Player Daemon](#Music_Player_Daemon)
    *   [5.9 Altre applicazioni](#Altre_applicazioni)
*   [6 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [6.1 Risoluzione dei problemi con periferiche HDAudio](#Risoluzione_dei_problemi_con_periferiche_HDAudio)
        *   [6.1.1 Capire la causa del problema](#Capire_la_causa_del_problema)
        *   [6.1.2 Come risolvere](#Come_risolvere)
    *   [6.2 Suono disturbato con gli MMS in totem](#Suono_disturbato_con_gli_MMS_in_totem)
    *   [6.3 Il microfono viene riprodotto dagli altoparlanti](#Il_microfono_viene_riprodotto_dagli_altoparlanti)
    *   [6.4 Risoluzioni di altri problemi](#Risoluzioni_di_altri_problemi)
*   [7 Consigli e trucchi](#Consigli_e_trucchi)
    *   [7.1 Usare i tasti multimediali con OSS](#Usare_i_tasti_multimediali_con_OSS)
    *   [7.2 Risoluzione dei problemi di ossvol](#Risoluzione_dei_problemi_di_ossvol)
    *   [7.3 Modificare la frequenza di campionamento](#Modificare_la_frequenza_di_campionamento)
    *   [7.4 Cambiare l'uscita audio di Default](#Cambiare_l.27uscita_audio_di_Default)
    *   [7.5 Creative Sound Blaster X-Fi Surround 5.1 SB1090 USB](#Creative_Sound_Blaster_X-Fi_Surround_5.1_SB1090_USB)
    *   [7.6 Una semplice applet per il systray](#Una_semplice_applet_per_il_systray)
    *   [7.7 Avviare ossmix nella systray all'avvio](#Avviare_ossmix_nella_systray_all.27avvio)
    *   [7.8 Registrare l'uscita audio di un programma](#Registrare_l.27uscita_audio_di_un_programma)
    *   [7.9 Sospensione e Ibernazione](#Sospensione_e_Ibernazione)
    *   [7.10 Emulazione ALSA](#Emulazione_ALSA)
        *   [7.10.1 Istruzioni](#Istruzioni)
    *   [7.11 Impostazioni per driver specifici](#Impostazioni_per_driver_specifici)
*   [8 Pacchetti sperimentali](#Pacchetti_sperimentali)
    *   [8.1 La versione del repo Mercurial](#La_versione_del_repo_Mercurial)

## Confronto con ALSA

Alcuni vantaggi e svantaggi confrontati con l'uso dell' Advanced Linux Sound Architecture.

### Vantaggi di OSS (utenti)

*   Controllo del volume audio per ogni applicazione.
*   Alcune schede audio di tipo legacy sono meglio supportate (e.g. Creative X-Fi).
*   Il tempo di risposta iniziale in applicazioni audio è generalmente migliore.
*   Miglior supporto per le applicazioni che utilizzano l' API OSS. Molte applicazioni continuano ad usare questa API, che non richiedono un livello di emulazione come quello utilizzato da ALSA.

### Vantaggi di OSS (sviluppatori)

*   API migliore, più pulita e facila da usare [documentazione](http://manuals.opensound.com/developer).
*   Supporto per i driver nello spazio utente.
*   Accessibilità. OSS funziona su sistemi BSD e Solaris.
*   Portabilità. OSS è [più facile](http://revolf.free.fr/Alchimie-7/Alchimie7_OSS_Haiku.en.pdf) da portare su altri sistemi operativi.

### Vantaggi di ALSA

*   Supporto migliore per le periferiche audio USB. Con OSS l'output è sperimentale, l'input non è implementato.
*   Supporto per le periferiche audio Bluetooth.
*   Supporto per i modem software AC'97 e HDAudio come il Si3055.
*   Supporto migliore per le periferiche MIDI. Con OSS è necessario utilizzare un sintetizzatore software come Timidity o Fluidsynth.
*   Supporto per la sospensione. OSS e i programmi associati devono prima essere chiusi.
*   Supporto migliore per la rilevazione dei jack. Su alcune schede madri HD gli utenti devono abbassare il volume degli altoparlanti per l'inserimento delle cuffie.

## Installazione

Installa OSS eseguendo:

```
# pacman -S oss

```

Questo installa i file di OSS e esegue lo script di installazione che disabilita temporaneamente i moduli ALSA e installa i moduli kernel di OSS. Dal momento che ALSA è abilitato di default negli script di boot, è necessario disabilitarlo per evitare conflitti con OSS durante il boot. E' possibile fare questo modificando `rc.conf` e aggiungendo:

```
MODULES=(!soundcore ...

```

Aggiungere poi OSS all'array dei demoni:

```
DAEMONS=(crond hal @oss...

```

Se l' utente non appartiene al gruppo audio, aggiungerlo con:

```
# gpasswd -a username audio

```

Poi avviare OSS con:

```
# /etc/rc.d/oss start

```

Nel caso OSS non sia in grado di riconoscere automaticamente la tua scheda audio alla partenza, esegui:

```
# ossdetect -v

```

Poi `soundoff && soundon` per riattivarlo.

## Testing

Considerare che il volume di default è molto alto, evitare di usare le cuffie e abbassare fisicamente il livello degli speaker (se possibile) prima di eseguire il test.

**Test OSS eseguendo:**

```
$ osstest

```

Dovrebbe essere possibile ascoltare una musica durante il processo di test. Se non c'è audio provare a regolare il volume o consultare la sezione dei problemi.

Per sentire suoni da più di un'applicazione simultaneamente è necessario vmix, il mixer software OSS.

**Controllare che vmix sia abilitato eseguendo:**

```
$ ossmix -a | grep -i vmix

```

Dovrebbe essere possibile vedere una linea del tipo 'vmix0-enable ON|OFF (currently ON)'. Se non è possibile vedere nessuna linea che inizi con 'vmix', probabilmente significa che vmix non è collegato alla periferica audio. Per collegare vmix, eseguire il comando:

```
$ vmixctl attach device

```

dove *device* è la scheda audio, eg., /dev/oss/oss_envy240/pcm0 .

Per evitare di rieseguire questo comando manualmente in futuro, è possibile aggiungere a /usr/lib/oss/soundon.user, come suggerito in [questo articolo](http://www.opensound.com/wiki/index.php/Tips_And_Tricks#Changing_the_default_sound_output).

Se si riceve l'errore "Periferica o risorsa occupata", è necessario aggiungere "vmix_no_autoattach=1" in /usr/lib/oss/conf/osscore.conf, e successivamente riavviare.

**Vedere quali periferiche sono riconosciute eseguendo:**

```
$ ossinfo

```

Dovrebbe essere possibile vedere una lista delle proprie periferiche sotto Device object o Audio Devices. Se la periferica che si vuole utilizzare non è in cima alle sezioni Audio device o Device objects, è necessario modificare /usr/lib/oss/etc/installed_drivers. Il driver per la periferica che si vuole utilizzare dovrebbe essere in cima. E probabilmente necessario un `soundoff && soundon`. Se questo non risolve, commentare tutti i driver presenti che non sono della periferica preferita.

## Regolazione del Volume

Per regolare il volume delle varie periferiche devono essere impostati i livelli dei mixer. Il mixer da linea di comando si chiama `ossmix`. E' molto simile al mixer audio di BSD (mixerctl). Il mixer grafico si chiama `ossxmix` e per essere installato necessita di [gtk2](https://www.archlinux.org/packages/?name=gtk2).

I controllo di base del comando <tt>ossxmix</tt>:

```
 / High Definition Audio ALC262 \    --------------------------------> 1
/________________________________\________________________________
|                                                                 \
| [x] vmix0-enable [vmix0-rate: 48.000kHz]      vmix0-channels    |--> 2
|                                               [ Stereo [v] ]    |
|                                                                 |
|  __codec1______________________________________________________ |
| |  _jack______________________________________________________ ||--> 3
| | |  _int-speaker_________________   _green_________________  |||
| | | |                             | |                       | |||
| | | |  _mode_____ | |             | |  _mode_____   | |     | |||
| | | | [ mix [v] ] o o [x] [ ]mute | | [ mix  [v] ]  o o [x] | |||
| | | |             | |             | |               | |     | |||
| | | |_____________________________| |_______________________| |||
| | |___________________________________________________________|||
| |______________________________________________________________||
| ___vmix0______________________________________________________  |
| |  __mocp___  O O   _firefox_  O O  __pcm7___  O O            | |--> 4
| | |         | O O  |         | x x |         | O O            | |
| | | | |     | x O  | | |     | x x | | |     | O O            | |
| | | o o [x] | x x  | o o [x] | x x | o o [x] | O O            | |
| | | | |     | x x  | | |     | x x | | |     | O O            | |
| | |_________| x x  |_________| x x |_________| O O            | |
| |_____________________________________________________________| |
|_________________________________________________________________|

```

1.  Una scheda per ogni periferica audio
2.  Le configurazione speciali del vmix (mixer virtuale) sono presenti in alto. Queste includono il sampling e la priorità del mixer.
3.  Queste sono le configurazioni dei jack della scheda audio (ingresso e uscita). Ogni regolazione mixer qui presente è fornita dalla scheda audio.
4.  Controlli e livelli audio del mixer vmix dell'applicazione . Se l'applicazione non sta attualmente riproducendo un suono sarà etichettata pcm08, pcm09..., quando l'applicazione è in riproduzione sarò mostrato il nome dell'applicazione.

### Definizione dei Colori

Per l'audio ad alta definizione (HD), `ossxmix` mostra le configurazioni dei jack colorate secondo i colori predefiniti:

| Color | Type | Connector |
| verde | canali frontali (uscita stereo) | 3.5mm TRS |
| nero | canali posteriori (uscita stereo) | 3.5mm TRS |
| grigio | canali laterali (uscita stereo) | 3.5mm TRS |
| oro | centrale e subwoofer (doppia uscita) | 3.5mm TRS |
| blu | livello di linea (ingresso stereo) | 3.5mm TRS |
| rosa | microfono (ingresso mono) | 3.5mm TS |

### Salvare i Livelli del Mixer

I livelli del mixer sono salvati quando il computer viene spento. Per salvare immediatamente i livelli del mixer, come root:

```
# savemixer

```

`savemixer` può essere utilizzato per salvare i livelli del mixer in un file con lo switch `-f` e ricaricarli con lo switch `-L`.

### Altri Mixer

Altri mixer supportano OSS:

*   GNOME - Gnome volume control
*   KDE - Kmix - Il supporto OSS è in fase di sviluppo.

## Configurare le Applicazioni per OSS

### Skype

Il pacchetto <tt>skype</tt> include soltanto il supporto per ALSA. Per ottenere una versione di Skype compatibile con OSS installare il pacchetto <tt>skype-oss</tt>:

```
# pacman -S skype-oss

```

Sulle versioni x86_64 è possibile ottenere il pacchetto [bin32-skype-oss](https://aur.archlinux.org/packages/bin32-skype-oss/) da AUR.

### Wine

*   Eseguire <tt>winecfg</tt>.

```
$ winecfg

```

*   Andare sulla scheda <tt>Audio</tt>.

*   Selezionare <tt>OSS Driver</tt>.

### Gajim

Come default Gajim usa `aplay -q` per riprodurre un suono. Per cambiare questo comportamento andare in Opzioni Avanzate e cercare la variabile `soundplayer`. Il programma ossplay incluso nel package oss è una buona alternativa: `ossplay -qq`

### MOC

Per usare MOC con OSS v 4.1 è necessario cambiare la sezione OSSMixerDevice in `/dev/ossmix` nel file di configurazione (posizionato in `"$HOME"/.moc`). Così MOC dovrebbe funzionare con la versione 4.1 di OSS. In alternativa è possibile compilare il pacchetto moc-svn disponibile su AUR (esso ha il supporto per il nuovo vmix). Per i problemi con l'interfaccia si provi a cambiare OSSMixerChannel; dopo aver avviato mocp premere 'w' (passa a mixer software).

### Applicazioni che usano Gstreamer

Rimuovere le librerie e i programmi di pulseaudio e gstremaer*-pulse.

Per cambiare le impostazioni di gstreamer in modo da inviare il suono a OSS invece che ad ALSA come da default, eseguire:

```
gstreamer-properties

```

Cambiare il plugin **Default Output** in custom e cambiare la pipeline in:

```
oss4sink

```

Per l'ingresso:

```
oss4src

```

**Note:** Non è sicuro che l'input suonerà meglio usando oss4src piuttosto che osssrc, quindi cambiarlo solo se migliora la qualità del suono in input. <da confermare>

**Note:** Per alcune applicazioni (e.g. Rhythmbox, Totem) il comando gstreamer-propertiers non ha effetto, dal momento che esse fanno riferimento a "musicaudiosink" invece di "audiosink" (modificata da gstreamer-properties). Soluzione: Impostare audiosink con gstreamer-properties e usare il comando gconf-editor per copiare il valore di "/system/gstreamer/0.10/default/audiosink" to "musicaudiosink" (nello stesso percorso)

Se viene usato phonon con il backend gstreamer è necessario impostare la relativa variabile ambiente. Per aggiungerla all'utente corrente:

```
export PHONON_GST_AUDIOSINK=oss4sink

```

Aggiungere questo comando al proprio `~/.bashrc` per caricarla al login.

### Firefox >=3.5

Firefox 3.5 introduce il supporto ai tag <video> e <audio> ed è in grado di riprodurre file multimediali ogg nativamente. Comunque, attualmente non può essere compilato con il supporto ad ALSA e ad OSS contemporaneamente. E' così necessario installare il pacchetto xulrunner-oss package da [community].

```
1\. Chiudere firefox.
2\. Installare il pacchetto xulrunner-oss da [community].
3\. Avviare firefox.

```

### Mplayer

Se viene usata un'interfaccia grafica è necessario trovare le impostazioni di uscita di oss nelle impostazioni audio. Con l'uso della versione a riga di comando è necessario specificare la modalità di uscita audio: `mplayer -ao oss /some/file/to/play.mkv` . Se non si vuole perdere tempo a scriverlo tutte le volte aggiungere "ao=oss" al proprio file di configurazione.(`"$HOME"/.mplayer/config`)

### Music Player Daemon

MPD è configurato tramite /etc/mpd.conf o ~/.mpdconf. Controllare entrambi i file, alla ricerca di qualcosa del tipo:

```
 audio_output {
       type           "alsa"
       name           "Some Device Name"
 }

```

Se viene trovata un'impostazione ALSA non commentata (le linee che non iniziano con #) come la precedente, commentarla tutta opppure cancellarla e aggiungere la seguente:

```
 audio_output {
       type           "oss"
       name           "My OSS Device"
 }

```

**Note:** Si deve mettere questa impostazione nel file ~/.mpdconf per farla funzionare correttamente ma dovrebbe funzionare anche in /etc/mpd.conf

Ulteriori impostazioni non dovrebbero essere necessarie per tutti gli utenti. Comunque, se vengono riscontrati dei problemi (MPD non funziona correttamente dopo essere stato riavviato), o se è preferibile avere file di configurazione specifici (più configurati dall'utente, meno configurati automaticamente), l'uscita audio per OSS può essere impostata specificatamente come segue: inizialmente eseguire:

```
 ossinfo | grep /dev/dsp

```

Cercare la linea che dice qualcosa di simile a `/dev/dsp -> /dev/oss/<SOME_CARD_IDENTIFIER>/pcm0`. Prendere nota del proprio <SOME_CARD_IDENTIFIER> e aggiungere le linee evidenziate nella sezione dell' uscita audio OSS del proprio file di configurazione di mpd:

```
 audio_output {
       type            "oss"
       name            "My OSS Device"
       **device          "/dev/oss/<SOME_CARD_IDENTIFIER>/pcm0"**
       **mixer_device    "/dev/oss/<SOME_CARD_IDENTIFIER>/mix0"**
 }

```

### Altre applicazioni

*   Se non è possibile ottenere l'audio da un'applicazione non indicata qui, provare a controllare sulla pagina [Configuring Applications for OSSv4](http://www.4front-tech.com/wiki/index.php/Configuring_Applications_for_OSSv4)
*   Cercare pacchetti specifici per OSS usando `pacman -Ss -- '-oss'` e [in AUR](https://aur.archlinux.org/packages.php?K=-oss%7C).

## Risoluzione dei problemi

### Risoluzione dei problemi con periferiche HDAudio

#### Capire la causa del problema

Se si possiede una periferica audio HDAudio, è molto probabile che sia necessario aggiustare alcune regolazioni del mixer prima che l'audio funzioni correttamente.

Le periferiche HDAudio sono molto potenti in questo senso e possono contenere molti piccolo circuiti (chiamati *widgets*) che possono sempre essere regolati via software. Questi controlli sono disponbili nel mixer, e possono essere usati, per esempio, per rimappare un jack per le cuffie in un jack di ingresso piuttosto che in uno di uscita.

Comunque, c'è un effetto collaterale, principalmente perchè lo standard HDAudio è più flessibile di quello che dovrebbe essere, e perchè i rivenditori spesso si preoccupano del corretto funzionamento soltanto dei loro *driver ufficiali*

Quindi quando si usano periferiche HDAudio, spesso si troveranno controlli mixer disorganizzati che non funzionano per niente nella configurazione di default e si rende necessario provare ogni combinazione dei controlli del mixer fino a raggiungere una configurazione funzionante.

#### Come risolvere

Aprire <tt>ossxmix</tt> e provare a cambiare ogni configurazione del mixer nell' *area centrale*, che contiene i controlli specifici della scheda audio, come spiegato nella precedente sezione "[Regolazione del Volume](#Regolazione_del_Volume)".

Probabilmente si vorrà impostare un programma per registrare/riprodurre continuamente in background (e.g. `ossrecord -` per registrare oppure `osstest -lV` per riprodurre), mentre si stanno cambiando le impostazioni del mixer.

*   Aumentare ogni slider di controllo dei volumi.
*   Per ogni opzione, provare a cambiare l'opzione selezionata, provando tutte le possibili combinazione.
*   Se si ottiene del rumore, provare ad abbassare e/o a silenziare alcuni controlli volume fino ad individuare la sorgente del rumore.

Nota bene che **non** è necessario cambiare nessuna impostazione nell' *area superiore o nell'* area inferiore*, dal momento che esse sono impostazioni relativa al mixer virtuale <tt>vmix</tt>.*

*   Modificare `/usr/lib/oss/conf/oss_hdaudio.conf` s commentando e modificando *hdaudio_noskip=0* con un valore da 0 a 7 che può rendere disponibili più opzioni relativa ai jack in ossmix.

E' stato necessario modificarlo a *hdaudio_noskip=7* per attivare gli altoparlanti posteriori e il subwoofer sul computer portatile e riavviare oss per applicare i cambiamenti `/etc/rc.d/oss restart`

### Suono disturbato con gli MMS in totem

Se gli stream hanno un suono disturbato o producono strani rumori in totem è possibile provare a riprodurli con un altro backend come ffmpeg (mplayer). Questo non risolverà il problema che ha gstreamer durante la riproduzione di stream MMS ma darà l'opzione di riprodurli con una buona qualità del suono. Riprodurli con mplayer è semplice:

```
# mplayer mmsh://yourstreamurl

```

### Il microfono viene riprodotto dagli altoparlanti

Di default OSS riproduce il microfono attraverso gli speaker. Per disabilitare questa funzione trovare in ossmix la sezione misc. Disattivare ogni "input-mix-mute" per disabilitarla.

### Risoluzioni di altri problemi

*   Se si ottiene un suono distorto, provare ad abbassare alcuni slider del volume.

*   Se è necessario cambiare la scheda audio di default controllare [qui](http://www.opensound.com/wiki/index.php/Tips_And_Tricks#Changing_the_default_sound_output).

*   Se è presente un' altro problema, provare a cercare o a chiedere aiuto sul [forum 4front](http://www.4front-tech.com/forum).

## Consigli e trucchi

### Usare i tasti multimediali con OSS

Un modo facile per attivare/disattivare l'audio e aumentare/ridurre il volume è usare lo [`ossvol` script](http://www.opensound.com/wiki/index.php/Tips_And_Tricks#ossvol) disponibile in [AUR](/index.php/AUR "AUR").

Una volta installato provare ad attivare/disattivare l'audio con:

```
$ ossvol -t

```

Usare `ossvol -h` per gli altri comandi disponibili.

Se non si conosce come assegnare i comandi ai propri tasti multimediali, controllare [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys").

### Risoluzione dei problemi di `ossvol`

Se si riceve un errore del tipo:

```
Bad mixer control name(987) 'vol'

```

è necessario modificare lo script (`/usr/bin/ossvol`) e cambiare il valore della variabile `CHANNEL` posizionata all'inizio dello script. Ad esempio `CHANNEL="vmix0-outvol"`.

*   **Nota** se si sta usando xbindkeys per i propri tasti multimediali aggiungere:

```
"ossmix vmix0-outvol -- +1"

```

incrementa il volume

```
"ossmix vmix0-outvol -- -1"

```

decrementa il volume

alla sezione relativa alla regolazione del volume nel file .xbindkeysrc è una soluzione semplice per la regolazione del volume.

### Modificare la frequenza di campionamento

Cambiare la frequenza di campionamento di uscita non è così ovvio. Le frequenze di campionamento possono essere cambiate soltanto da root e vmix non deve essere utilizzato da nessun altro programma. Prima di seguire questi passi, assicurarsi di utilizzare un sintoamplificatore e di utilizzare altoparlanti di qualità e non comuni altoparlanti da PC. Se si stanno usando comuni altoparlanti da PC, non preoccuparsi di cambiare niente dal momento che non sarà udibile nessuna differenza.

Di default la frequenza di campionamento è 48000hz. Ci sono diverse situazioni in cui si può voler cambiare. Dipende tutto dall'utilizzo che se ne fa. E' consigliato impostare la frequenza di campionamento corrispondente alla sorgente utilizzata più frequentemente. Se il computer deve cambiare la frequenza di campionamento di una sorgente per farla corrispondere a quella dell'hardware è probabile, anche se non certo, che ci sarà una perdita nella qualità dell'audio. Questo è particolarmente riscontrabile nel downsampling (ie. 96000hz → 48000hz). C'è un articolo su questo problema su ["Stereophile"](http://www.stereophile.com/news/121707lucky/) che è stato [discusso](http://lists.apple.com/archives/coreaudio-api/2008/Jan/msg00272.html) sulla mailing list della Apple "CoreAudio API", se si vuole approfondire questa problematica.

Alcuni esempi di frequenze di campionamento:

*   44100hz - Frequenza di campionamento dello standard [Red Book](https://en.wikipedia.org/wiki/Red_Book_(audio_CD_standard) per i CD audio.
*   88000hz - Frequenza di campionamento dei [SACD](https://en.wikipedia.org/wiki/Super_Audio_CD "wikipedia:Super Audio CD") ad alta definizione. E' raro che la scheda madre supporti questo tipo di frequenza.
*   96000hz - Frequenza di campionamento della maggior parte dei download audio ad alta definizione. Se la scheda madre è una scheda madre [AC'97](https://en.wikipedia.org/wiki/AC%2797 "wikipedia:AC'97"), probabilmente questa sarà la frequenza più alta.
*   192000hz - Frequenza di campionamento dei BluRay e di alcuni (molto pochi) download ad alta definizione. Il supporto per ricevitori audio esterni è limitato alle periferiche high-end. Non tutte le schede madri lo supportano. Un esempio di chipset di una scheda madre che potrebbe supportarlo include l'[Intel HDA audio](https://en.wikipedia.org/wiki/Intel_High_Definition_Audio "wikipedia:Intel High Definition Audio").

Per verificare qual' è la frequenza di campionamento attualmente impostata:

1.  Eseguire `"ossmix | grep rate"`.

Probabilmente sarà visibile `"vmix0-rate <decimal value> (currently 48000) (Read-only)"`.

In questo caso, OSS userà la frequenza richiesta dal programma che sta attualmente utilizzando la periferica, ignorando questa sezione. Eccezione: Le schede envy24(ht) hanno un' impostazione envy24.rate che ha una funzione similare (vedere la pagina di manuale di "oss_envy24"). E' possibile seguire i seguenti passi, ma al secondo passo, sotituire con ossmix il valore di "envy24.rate".

Passi per effettuare il cambiamento:

1.  Primo, essere sicuri che la scheda audio supporti la nuova frequenza. Eseguire "ossinfo -v2" e controllare se la frequenza voluta è presente nei "Native sample rates".
2.  Come root, eseguire `"/usr/lib/oss/scripts/killprocs.sh"`. Attenzione, questo comando terminerà tutti i programmi che hanno attualmente un canale audio aperto (ad esempio riproduttori multimediali, Firefox superiore alla versione 3.5 se xulrunner-oss è abilitato e il controllo del volume di gnome)
3.  Dopo che tutti i programmi che stavano utilizzando vmix sono terminati, eseguire come root: `"vmixctl rate /dev/dsp 96000"` sostituendo la frequenza con la frequenza desiderata.
4.  Eseguire `"ossmix | grep rate"` e controllare che `"vmix0-rate <decimal value> (currently 96000) (Read-only)"` rispecchi la frequenza desiderata sia stata impostata correttamente.
5.  **Salvare i cambiamenti permanentemente** tramite il file soundon.user per impostare la frequenza ad ogni soundon

```
scrivere `"vmixctl rate /dev/dsp 96000" nel file /usr/lib/oss/soundon.user` e renderlo eseguibile.

```

### Cambiare l'uscita audio di Default

Durante l'esecuzione di osstest, il primo test viene superato per il primo canale ma non per il canale di destra o per i canali stereo, il suono è distorto e sibilante. Se avviene questo è selezionata l'uscita audio sbagliata.

```
      *** Scanning sound adapter #-1 ***
      /dev/oss/oss_hdaudio0/pcm0 (audio engine 0): HD Audio play front
      - Performing audio playback test... 
      <left> OK <right> OK <stereo> OK <measured srate 47991.00 Hz (-0.02%)> 

```

Il canale sinistro suona bene, il destro e lo stereo sono distorti.

Continuare il test fino ad ottenere un output funzionante:

```
      /dev/oss/oss_hdaudio0/spdout0 (audio engine 5): HD Audio play spdif-out 
      - Performing audio playback test... 
      <left> OK <right> OK <stereo> OK <measured srate 47991.00 Hz (-0.02%)> 

```

Se così viene superato il test su tutti i canali sinistro, destro e stereo procedere al prossimo passo.

Da qui: [Changing_the_default_sound_output](http://www.opensound.com/wiki/index.php/Tips_And_Tricks#Changing_the_default_sound_output) recuperare il comando per cambiare l'uscita audio di default; cambiare in base alla configurazione funzionante

```
      sudo ln -sf /dev/oss/oss_hdaudio0/spdout0 /dev/dsp_multich

```

Con il surround 5.1 scegliere dsp_multichannel; con 2 canali dsp dovrebbe fuzionare.

### Creative Sound Blaster X-Fi Surround 5.1 SB1090 USB

Queste informazioni provengono completamente da [4front-tech.com](http://www.4front-tech.com/forum/viewtopic.php?f=3&t=3423); per cortesia di kristian e Maxa. Grazie!!

E' sorprendente come la scheda audio esterna non funzioni soltanto a causa di un mancato valore di ritorno di true nella funzione write_control_value(...) in ossusb_audio.c.

Attualmente per risolvere è necessario ricompilare oss.

1\. Ottenere l'ultima verione di oss dai Repo di Arch

```
[https://repos.archlinux.org/wsvn/community/oss/repos/community-x86_64/](https://repos.archlinux.org/wsvn/community/oss/repos/community-x86_64/)

```

2\. Estrarre

3\. fare cd nella cartella ottenuta, è possibile rinominarla in oss

4\. eseguire makepkg --nobuild

5\. fare cd in src/kernel/drv/oss_usb/ ; **modificare il file ossusb_audio.c**; **aggiungere Return 1**; a questo punto dovrebbe apparire così e **SALVARE**

```
  static int
 write_control_value (ossusb_devc * devc, udi_endpoint_handle_t * endpoint,
            int ctl, int l, unsigned int v)
 {
   return 1;

```

6\. fare cd in /src/kernel/setup e modificare srcconf_linux.inx, cercare -Werror e rimuoverlo, altrimenti OSS non verrà compilato.

7\. eseguire makepkg --noextract

Adesso è possibile installare il pacchetto con pacman -U ; rimuovere prima oss se è già installato(pacman -Rd oss)

### Una semplice applet per il systray

Si vuole un'applet per controllare il volume come in GNOME? Da [qui](https://bbs.archlinux.org/viewtopic.php?id=77440) è possibile ottenerne [una](http://pastebin.furver.se/0xflchkfz/) funzionante.

Scaricare [questo](http://pastebin.furver.se/0xflchkfz/0xflchkfz.txt) script e rinominarlo con un nome a piacere, e.g.: ossvolctl. Eseguire il seguente comando:

```
$chmod +x ossvolctl
#cp ossvolctl /usr/bin/ossvolctl

```

oppure

```
#install -Dm755 ossvolctl /usr/bin/ossvolctl

```

### Avviare ossmix nella systray all'avvio

**KDE 4**

Creare un launcher di applicazione chiamato `ossxmix.desktop` nella propria directory locale dei launcher (`~/.local/share/applications/` e poi inserire:

```
[Desktop Entry]
Name=Open Sound System Mixer
GenericName=Audio Mixer
Exec=ossxmix -b
Icon=audio-card
Categories=Application;GTK;AudioVideo;Player;
Terminal=false
Type=Application
Encoding=UTF-8
```

Per aggiungerlo all'avvio automatico al caricamento dell' ambiente desktop:

System Settings > Advanced tab > Autostart. Poi cliccare aggiungi programma e scegliere dalla lista 'Multimedia'.

**Gnome**

*   Come Root creare il file /usr/local/bin/ossxmix_bg con il seguente contenuto:

```
#!/bin/sh
exec /usr/bin/ossxmix -b

```

Andare in System > Preferences > Start Up Applications

*   Cliccare Aggiungi, scrivere OSSMIX nel campo Nome e `/usr/local/bin/ossxmix_bg` nel campo Comando e successivamente premere il tasto Aggiungi.

*   Rieffettuare il login per vedere i cambiamenti.

### Registrare l'uscita audio di un programma

*   [Recording sound output of a program](http://www.opensound.com/wiki/index.php/Tips_And_Tricks#Recording_sound_output_of_a_program).

### Sospensione e Ibernazione

OSS non suppporta automaticamente la sospensione così è necessario fermare manualmente OSS prima della sospensione o della ibernazione

OSS fornisce <tt>soundon</tt> e <tt>soundoff</tt> per abilitare e disabilitare OSS, nonostante tutti i processi che usano il suono debbano prima essere terminati.

Il seguente script è un semplice metodo per fermare automaticamente OSS prima della sospensione e riavviarlo alla fine.

```
#!/bin/sh
. "${PM_FUNCTIONS}"

suspend_osssound()
{
 /usr/lib/oss/scripts/killprocs.sh
 /usr/sbin/soundoff
}

resume_osssound()
{
 /usr/sbin/soundon
}

case "$1" in
 hibernate|suspend)
 suspend_osssound
	;;
 thaw|resume)
	resume_osssound
	;;
 *) exit $NA
	;;
esac

```

Salvare il contenuto dello script (come root) in `/etc/pm/sleep.d/50ossound` e renderlo eseguibile. `chmod a+x /etc/pm/sleep.d/50ossound`

**Nota:** Questo script è piuttosto semplice e terminerà qualsiasi applicazione che stia usando direttamente OSS, salvare il proprio lavoro prima di sospendere/ibernare.

OSS non supporta la sospensione ma non è indispensabile dal momento che [s2ram](/index.php/Suspend_to_RAM "Suspend to RAM") funziona correttamente senza fermare OSS. Creare semplicemente uno script di sospensione in /sbin/suspend e renderlo eseguibile.

```
 #!/bin/sh
 ## Checking if you are a root or not
 if ! [ -w / ]; then
   echo >&2 "This script must be run as root"
   exit 1
 fi

 s2ram -f

 sleep 2

 /etc/rc.d/oss restart 2>/tmp/oss.txt ||
 echo "OSS restart failed, check /tmp/oss.txt for advice"

```

Con questo tutte le applicazioni funzioneranno correttamente con la sospensione. \o/

**Nota:** Se si sta usando Opera è necessario terminare operapluginwrapper prima della sospensione. Per farlo aggiungere **pid=$(pidof operapluginwrapper) && kill $pid** prima di s2ram -f.

### Emulazione ALSA

E' possibile configurare <tt>alsa-lib</tt> per utilizzare OSS come suo sistema audio di uscita. Questo funziona come una sorta di emulazione di ALSA.

E' da notare, comunque, che questo metodo può introdurre latenza aggiuntiva nel suono di uscita, e che l'emulazione non è completa e non funziona con tutte le applicazioni. Non funziona, ad esempio, con programmi che provano a riconoscere periferiche usando ALSA.

Per questo, dal momento che la maggior parte delle applicazioni supporta OSS direttamente, usare questo metodo soltanto come ultima risorsa.

In futuro, metodi più completi per emulare ALSA saranno disponibili, come <tt>libsalsa</tt> and <tt>cuckoo</tt>.

#### Istruzioni

*   Installare il pacchetto <tt>alsa-plugins</tt>.

```
# pacman -S alsa-plugins

```

*   Modificare `/etc/asound.conf` nel seguente modo.

```
pcm.oss {
   type oss
    device /dev/dsp
}

pcm.!default {
    type oss
    device /dev/dsp
}

ctl.oss {
    type oss
    device /dev/mixer
}

ctl.!default {
    type oss
    device /dev/mixer
}

```

**Nota:** Se non si vuole più usare OSS, non dimenticarsi di annullare i cambiamenti fatti in `/etc/asound.conf`.

### Impostazioni per driver specifici

Se qualcosa non funziona, c'è la possibilità, che ci siano delle impostazioni specifiche per driver specifici (in questo modo è possibile attivare l'auto-sense dei jack sui portatili)

*   Trovare il driver usato

```
# lspci -vnn|grep -i -A 15 audio

```

```
00:1e.2 Multimedia audio controller [0401]: Intel Corporation 82801FB/FBM/FR/FW/FRW (ICH6 Family) AC'97 Audio Controller [8086:266e] (rev 03)
	Subsystem: Hewlett-Packard Company NX6110/NC6120 [103c:099c]
	Flags: bus master, medium devsel, latency 0, IRQ 21
	I/O ports at 2100 [size=256]
	I/O ports at 2200 [size=64]
	Memory at d0581000 (32-bit, non-prefetchable) [size=512]
	Memory at d0582000 (32-bit, non-prefetchable) [size=256]
	Capabilities: <access denied>
	Kernel driver in use: *oss_ich*
	Kernel modules: snd-intel8x0
```

*   Individuare il file di configurazione per la periferica in:

```
# cd /usr/lib/oss/conf/

```

*   Provare a cambiare le impostazioni di default. Ci sono soltanto poche impostazioni e si spiegano da sole.

Impostazione:

```
ich_jacksense = 1 

```

in oss-ich.conf abilita l'auto-sense dei jack su alcuni laptop (l'inserimento delle cuffie viene rilevato e gli altoparlanti vengono disattivati.)

*   Riavviare oss per applicare i cambiamenti.

```
# sudo /etc/rc.d/oss restart

```

*   oss_hdaudio.conf ha anche hdaudio_jacksens. Anche questo potrebbe funzionare. Sfortunatamente non per tutti.

## Pacchetti sperimentali

### La versione del repo Mercurial

C'è un pacchetto [oss-mercurial](https://aur.archlinux.org/packages/oss-mercurial/) in [AUR](/index.php/AUR "AUR"). Questo pacchetto compila e installa l'ultima versione di sviluppo di OSS direttamente dal repo Mercurial.

E' possible provare questo pacchetto se si vuole contribuire al codice di OSS oppure se soltanto una modifica molto recente nel codice di OSS ha introdotto il supporto alla vostra periferica audio.

Se si vuole che oss riproduca i suoni delle animazioni flash (e anche dei suoni delle applicazioni Adobe-Air) è necessario installare libflashsupport:

```
# pacman -S libflashsupport

```