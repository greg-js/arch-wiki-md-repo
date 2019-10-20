<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Impostare l'output analogico come default](#Impostare_l'output_analogico_come_default)
*   [2 Usare l'uscita HDMI e analogica contemporaneamente](#Usare_l'uscita_HDMI_e_analogica_contemporaneamente)
*   [3 Configurazione dell'uscita HDMI](#Configurazione_dell'uscita_HDMI)
    *   [3.1 Trovare l'output HDMI](#Trovare_l'output_HDMI)
    *   [3.2 Identificare la scheda corretta](#Identificare_la_scheda_corretta)
    *   [3.3 Configurare Pulseaudio per rilevare l'uscita HDMI Nvidia](#Configurare_Pulseaudio_per_rilevare_l'uscita_HDMI_Nvidia)
*   [4 Sistemi surround](#Sistemi_surround)
    *   [4.1 Dividere le uscite frontali/posteriori](#Dividere_le_uscite_frontali/posteriori)
    *   [4.2 Remixing LFE](#Remixing_LFE)
*   [5 Streaming audio via rete attraverso Pulseaudio](#Streaming_audio_via_rete_attraverso_Pulseaudio)
    *   [5.1 Supporto TCP (streaming audio via rete)](#Supporto_TCP_(streaming_audio_via_rete))
    *   [5.2 Supporto TCP con client anonimi](#Supporto_TCP_con_client_anonimi)
    *   [5.3 Publishing attraverso Zeroconf (avahi)](#Publishing_attraverso_Zeroconf_(avahi))
    *   [5.4 Cambiare il server Pulseaudio usato dai clients X locali](#Cambiare_il_server_Pulseaudio_usato_dai_clients_X_locali)
    *   [5.5 Quando ogni altro tentativo risulta vano](#Quando_ogni_altro_tentativo_risulta_vano)
*   [6 ALSA Monitor source](#ALSA_Monitor_source)
*   [7 Pulseaudio attraverso JACK](#Pulseaudio_attraverso_JACK)
    *   [7.1 Il metodo ancora più nuovo](#Il_metodo_ancora_più_nuovo)
    *   [7.2 Nuovo metodo](#Nuovo_metodo)
    *   [7.3 Vecchio metodo](#Vecchio_metodo)
        *   [7.3.1 QjackCtl con script di avvio/shutdown](#QjackCtl_con_script_di_avvio/shutdown)
*   [8 Pulseaudio attraverso OSS](#Pulseaudio_attraverso_OSS)
*   [9 Pulseaudio da chroot](#Pulseaudio_da_chroot)
*   [10 Disabilitare l'auto spawning del server PulseAudio](#Disabilitare_l'auto_spawning_del_server_PulseAudio)
*   [11 Mappare il canale stereo su mono](#Mappare_il_canale_stereo_su_mono)

## Impostare l'output analogico come default

**Nota:** Per ottenere l'elenco dei dispositivi, viene utilizzato `aplay`. Questo programma è parte del pacchetto [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) e NON è richiesto per effettuare l'output su sorgenti multiple: è solamente necessario per elencare i dispositivi di riproduzione, e può essere rimosso alla fine della procedura.

Per selezionare una sorgente output diversa da quella di default, è innanzitutto necessario elencarle tutte:

 `$ aplay -l` 
```
**** List of PLAYBACK Hardware Devices ****
card 0: Intel [HDA Intel], device 0: ALC889A Analog [ALC889A Analog]
  Subdevices: 0/1
  Subdevice #0: subdevice #0
card 0: Intel [HDA Intel], device 1: ALC889A Digital [ALC889A Digital]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 0: Intel [HDA Intel], device 3: HDMI 0 [HDMI 0]
  Subdevices: 0/1
  Subdevice #0: subdevice #0

```

Su questa macchina, la sorgente analogica è identificata da `card 0` `device 0`. Si modifichi `/etc/pulse/default.pa` inserendo la seguente linea:

```
load-module module-alsa-sink device=hw:0,0

```

Si determini l'indice corretto della nuova sorgente:

```
$ pacmd list-sinks | less

```

Si annoti il numero d'indice che corrisponde al sink `alsa_output.hw_0_0`

Infine, si aggiunga una seconda linea ad `/etc/pulse/default.pa` per impostare l'output di default:

```
set-default-sink 2

```

Si effettui nuovamente il login o si riavvii PulseAudio per applicare i cambiamenti.

## Usare l'uscita HDMI e analogica contemporaneamente

Pulseaudio permette l'output simulteaneo su più dispositivi. Nell'esempio presentato di seguito, alcune applicazioni sono configurate per usare l'uscita HDMI, mentre altre utilizzeranno quella analogica. E' possibile inviare l'audio a più applicazioni contemporaneamente.

 `$ aplay -l` 
```
**** List of PLAYBACK Hardware Devices ****
card 0: Intel [HDA Intel], device 0: ALC889A Analog [ALC889A Analog]
  Subdevices: 0/1
  Subdevice #0: subdevice #0
card 0: Intel [HDA Intel], device 1: ALC889A Digital [ALC889A Digital]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 0: Intel [HDA Intel], device 3: HDMI 0 [HDMI 0]
  Subdevices: 0/1
  Subdevice #0: subdevice #0

```

Il segreto per realizzare con succcesso una configurazione come questa è capire che il dispositivo selezionato in pavucontrol (sotto Configuration->Internal Audio), verrà trattato come quello di default. Si avvii pavucontrol, ci si rechi nella sezione *Configurazion* e si selezioni il profilo HDMI.

Si aggiungano poi le seguenti linee ad `/etc/pulse/default.pa`, per impostare l'uscita analogica come sorgente secondaria:

```
### Load analog device
load-module module-alsa-sink device=hw:0,0
load-module module-combine-sink sink_name=combined
set-default-sink combined

```

Si riavvi PulseAudio e si esegua `pavucontrol`, quindi selezionare il tab "Output Devices". Dovrebbero ora apparire tre voci:

1.  Internal Audio Digital Stereo (HDMI)
2.  Internal Audio
3.  Simultaneous ouput to Internal Audio Digital Stereo (HDMI), Internal Audio

Avviare quindi un programma che utilizzi Pulseaudio come mplayer,vlc,mpd eccetera, quindi si clicchi sulla tab "Playback". Dovrebbe comparire un menù a tendina per ciascuno dei programmi avviati, che permette di scegliere una sorgente fra le tre elencate sopra.

Si veda inoltre [questo thread](https://bbs.archlinux.org/viewtopic.php?id=118026) per una variazione sul tema e le [FAQ di PulseAudio](http://www.freedesktop.org/wiki/Software/PulseAudio/FAQ#Can_I_use_PulseAudio_to_playback_music_on_two_sound_cards_simultaneously.3F).

## Configurazione dell'uscita HDMI

Come sottolineato in [ftp://download.nvidia.com/XFree86/gpu-hdmi-audio-document/gpu-hdmi-audio.html#_issues_in_pulseaudio](ftp://download.nvidia.com/XFree86/gpu-hdmi-audio-document/gpu-hdmi-audio.html#_issues_in_pulseaudio), a causa di un bug di Pulseaudio, usando una scheda video con supporto HDMI, non verrà riprodotto alcun suono a meno che la porta HDMI sia impostata come primo dispositivo di output. La soluzione proposta sotto, consiste nello scoprire quale output HTMI funziona usando l'utility `aplay`, contenuta nel pacchetto [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils).

Il titolo originale di questa sezione assumeva che il problema fosse relativo alle sole schede nvidia, ma come si è visto in [questo thread](https://bbs.archlinux.org/viewtopic.php?id=133222), anche altre schede video potrebbero esserne affette. Il resto dell'articolo, userà una scheda nvidia come esempio, ma la soluzione dovrebbe applicarsi anche agli utilizzatori di schede diverse.

### Trovare l'output HDMI

```
# aplay -l

```

```
sample output:
 **** List of PLAYBACK Hardware Devices ****
 card 0: NVidia [HDA NVidia], device 0: ALC1200 Analog [ALC1200 Analog]
   Subdevices: 1/1
   Subdevice #0: subdevice #0
 card 0: NVidia [HDA NVidia], device 3: ALC1200 Digital [ALC1200 Digital]
   Subdevices: 1/1
   Subdevice #0: subdevice #0
 card 1: NVidia_1 [HDA NVidia], device 3: HDMI 0 [HDMI 0]
   Subdevices: 1/1
   Subdevice #0: subdevice #0
 card 1: NVidia_1 [HDA NVidia], device 7: HDMI 0 [HDMI 0]
   Subdevices: 0/1
   Subdevice #0: subdevice #0
 card 1: NVidia_1 [HDA NVidia], device 8: HDMI 0 [HDMI 0]
   Subdevices: 1/1
   Subdevice #0: subdevice #0
 card 1: NVidia_1 [HDA NVidia], device 9: HDMI 0 [HDMI 0]
   Subdevices: 1/1
   Subdevice #0: subdevice #0

```

### Identificare la scheda corretta

Ora che si dispone di un elenco di tutte le schede rilevate, è necessario scoprire quale di esse invia l'output al tv/monitor:

```
# aplay -D plughw:1,3 /usr/share/sounds/alsa/Front_Right.wav

```

Dove 1 rappresenta la scheda e 3 è il device (i valori sono quelli elencati nella sezione precedente). Se non viene riprodotto alcun suono, si provi ad usare un device differente (nel mio caso ho dovuto usare la scheda 1 e il subdevice 7).

### Configurare Pulseaudio per rilevare l'uscita HDMI Nvidia

Una volta ricavato il dispositivo funzionante, è necessario forzare Pulseaudio ad usarlo. Si modifichi `/etc/pulse/default.pa`, aggiungendo la seguente linea:

```
# load-module module-alsa-sink device=hw:1,7

```

Dove 1 e 7 rappresentano i valori trovati nella sezione precedente.

Si riavvii quindi Pulseaudio:

```
# killall pulseaudio

```

Si apra il pannello impostazioni del suono, e ci si assicuri che, sotto la scheda "Hardware", l'audio HDMI della scheda video sia impostato su "Digital Stereo (HDMI) Output" (L'audio della mia scheda video era identificato con "GF100 High Definition Audio Controller").

Si apra quindi la scheda "Output", dove dovrebbero ora apparire due output HDMI per la scheda video. Si verifichi quale dei due funziona selezionandolo e poi aprendo un programma per la riproduzione audio (ad esempio, si usi VLC per riprodurre un filmato: se non si ottiene nessun suono, selezionare l'altra uscita).

## Sistemi surround

Molte persone hanno una scheda che supporta il surround, ma diffusori che usano solamente due canali, cosa che impedisce a Pulseaudio di configurarsi per il supporto al surround in modo automatico. Per abilitare tutti i canali, modificare `/etc/pulse/daemon.conf`: si decommenti la linea "default-sample-channels" (ossia si rimuova il ';' dall'inizio della linea), modificando il valore a **6** se si ha un impianto 5.1, oppure a **8** se si dispone di un sistema 7.1.

```
# Default
default-sample-channels=2
# Sistemi 5.1
default-sample-channels=6
# Sistemi 7.1
default-sample-channels=8

```

Dopo aver effettuato le modifiche, sarà necessario riavviare Pulseaudio.

### Dividere le uscite frontali/posteriori

Si potrebbe voler connettere gli altoparlanti all'output analogico frontale e le cuffie a quello posteriore. Sarebbe utile dividere le uscite in sink separati. Si aggiunga al file `/etc/pulse/default.pa`:

```
load-module module-remap-sink sink_name=speakers remix=no master=alsa_output.pci-0000_05_00.0.analog-surround-40 channels=2 master_channel_map=front-left,front-right channel_map=front-left,front-right

```

```
load-module module-remap-sink sink_name=headphones remix=no master=alsa_output.pci-0000_05_00.0.analog-surround-40 channels=2 master_channel_map=rear-left,rear-right  channel_map=front-left,front-right

```

(Si sostituisca `alsa_output.pci-0000_05_00.0.analog-surround-40` con il nome della propria scheda audio, ottenuto con `pacmd list-sinks`).

E' ora possibile scegliere se usare le cuffie o gli altoparlanti direttamente dal player audio.

### Remixing LFE

Di default, Pulseaudio effettua il remix del numero di canali basandosi sul valore di `default-sample-channels`, escludendo però il canale LFE. Per abilitare il remixing LFE, si decommenti la linea:

```
; enable-lfe-remixing = no

```

sostituendo "no" con "yes":

```
enable-lfe-remixing = yes

```

Si riavvii quindi Pulseaudio.

## Streaming audio via rete attraverso Pulseaudio

Una delle caratteristiche più interessanti di Pulseaudio è la possibilità di effettuare lo streaming audio dai clients, attraverso i protocollo TCP, al server che ha in esecuzione il demone Pulseaudio, permettendo all'audio di essere trasmesso in streaming attraverso la propria LAN.

Affinché questo funzioni, è necessario abilitare il relativo modulo in Pulseaudio e copiare il pulse-cookie sui clients.

### Supporto TCP (streaming audio via rete)

Per abilitare il modulo TCP, aggiungere questa riga (o decommentarla, se già presente) al file `/etc/pulse/default.pa` (sia sul client che sul server):

```
load-module module-native-protocol-tcp

```

Affinchè il tutto funzioni, è necessario che sia il client che il server condividano lo stesso cookie, situato in `~/.config/pulse/cookie`. Non fa differenza utilizzare il cookie del server o quello del client: l'importante è che entrambe le macchine utilizzino lo stesso.

Nota: Se si riscontrano problemi di connessione, si usi (sul server):

```
pacmd list-modules

```

### Supporto TCP con client anonimi

Se non si desidera copiare il file del cookie dai vari client, è possibile consentire a client anonimi di connettersi, passando questi parametri al modulo `module-native-protocol-tcp` sul server (sempre modificando `/etc/pulse/default.pa`):

```
 load-module module-native-protocol-tcp auth-ip-acl=127.0.0.1;192.168.0.0/24 auth-anonymous=1

```

Si cambi la sottorete della LAN in modo che combaci con quella in cui si trovano i client che desiderano connettersi al server.

### Publishing attraverso Zeroconf (avahi)

Affinché il server Pulseaudio remoto appaia nel Device Chooser di Pulseaudio (`pasystray`) sarà necessario caricare i moduli di zeroconf necessari ed abilitare il demone [Avahi](/index.php/Avahi "Avahi").

Su entrambe le macchine si esegua:

```
# systemctl start avahi-daemon.service
# systemctl enable avahi-daemon.service

```

Sul server si aggiunga `load-module module-zeroconf-publish` al file `/etc/pulse/default.pa`, mentre sul client aggiungere allo stesso file `load-module module-zeroconf-discover`. Redirigere infine qualsiasi stream o output audio al server pulseaudio remoto selezionando il sink apposito.

Se si riscontrano problemi con i sink remoti dalle macchine client, si provi a riavviare il demone avahi in modo da effettuare nuovamente il broadcast delle interfacce disponibili.

### Cambiare il server Pulseaudio usato dai clients X locali

Per scegliere tra diversi server sul client da dentro X, è possibile utilizzare il comando `pax11publish`. Per esempio, per usare, al posto di quello di default, il server avviato sulla macchina con hostname foo:

```
$ pax11publish -e -S foo

```

Oppure, per tornare al server di default:

```
$ pax11publish -e -r

```

Si noti che, affinché il cambio abbia effetto, è necessario riavviare i programmi che usano Pulseaudio.

### Quando ogni altro tentativo risulta vano

Si noti che quanto presentato di seguito, è un fix temporaneo e **non** rappresenta una soluzione permanente.

Sul server:

```
$ paprefs

```

Accesso alla rete -> Abilitare l'accesso per i dispositivi audio locali (Selezionare sia 'Permetti discover' che 'Non richedere autenticazione').

Sul client:

```
$ export PULSE_SERVER=server.ip && mplayer test.mp3

```

## ALSA Monitor source

Per registrare da una monitor source (ossia "What-U-Hear", "Stereo Mix"), si utilizzi `pactl list` per individuare il nome della sorgente in Pulseaudio (es: `alsa_output.pci-0000_00_1b.0.analog-stereo.monitor`). Si aggiungano quindi le linee simili a quella di cui sopra al file `/etc/asound.conf`, oppure `~/.asoundrc`:

```
pcm.pulse_monitor {
  type pulse
  device alsa_output.pci-0000_00_1b.0.analog-stereo.monitor
}
ctl.pulse_monitor {
  type pulse
  device alsa_output.pci-0000_00_1b.0.analog-stereo.monitor
}

```

È ora possibile selezionare `pulse_monitor` come sorgente di registrazione.

È altresì possibile usare pavucontrol per svolgere questo compito: ci si assicuri di aver impostato il display su "All input Devices" e si selezioni "Monitor of [nome scheda audio]" come sorgente di registrazione.

## Pulseaudio attraverso JACK

### Il metodo ancora più nuovo

Questo metodo funzionerà solo con jackdbus (JACK compilato con il supporto a D-Bus). Si aggiunga la seguente linea ad `/etc/pulse/default.pa`:

```
load-module module-jackdbus-detect

```

Come descritto sulla pagina relativa alla [pacchettizzazione di Jack-DBUS](http://trac.jackaudio.org/wiki/JackDbusPackaging):

*L'autoavvio del server è implementato come una chiamata a D-Bus che attiva automaticamente il servizio D-Bus relativo a Jack, nel caso in cui non sia già stato avviato automaticamente, ed inizializza il server Jack. L'interazione corretta con PulseAudio avviene attraverso un sistema di "acquisizione/rilascio" della scheda audio basato su D-Bus. Quando il server Jack si avvia, richiede al servizio D-Bus di prendere possesso della scheda audio e PulseAudio la rilascia immediatamente. Al contrario, quando il server viene fermato, è quest'ultimo a rilasciare la scheda audio che potrà così essere di nuovo gestita da PulseAudio.*

`module-jackdbus-detect.so` carica e rimuove dinamicamente i moduli `module-jack-sink` e `module-jack-source` quando jackdbus viene avviato o fermato.

### Nuovo metodo

Uccidere Pulseaudio non è una buona idea, poichè potrebbe far crashare le applicazioni che lo stanno utilizzando ed interrompere la riproduzione dell'audio.

Si procederà come segue:

1.  PulseAudio rilascia la scheda audio
2.  Jack ne prende possesso e si avvia
3.  Lo script redirige PulseAudio a JACK
4.  inviare manualmente l'output delle applicazioni PulseAudio a JACK (pavucontrol potrebbe essere d'aiuto in questo caso)
5.  usare programmi JACK
6.  attraverso lo script, smettere di redirigere l'output di PulseAudio a JACK
7.  uccidere JACK e rilasciare la scheda audio
8.  PulseAudio riprende possesso della scheda e redirige l'audio di conseguenza

Con QJackCTL, implementare questi script:

Script da eseguire all'avvio: `pulse-jack-pre-start.sh`

```
#!/bin/bash
pacmd suspend true

```

Script da eseguire dopo l'avvio: `pulse-jack-post-start.sh`

```
#!/bin/bash
pactl load-module module-jack-sink channels=2
pactl load-module module-jack-source channels=2
pacmd set-default-sink jack_out
pacmd set-default-source jack_in

```

Script da eseguire allo spegnimento: `pulse-jack-pre-stop.sh`

```
#!/bin/bash
SINKID=$(pactl list | grep -B 1 "Name: module-jack-sink" | grep Module | sed 's/[^0-9]//g')
SOURCEID=$(pactl list | grep -B 1 "Name: module-jack-source" | grep Module | sed 's/[^0-9]//g')
pactl unload-module $SINKID
pactl unload-module $SOURCEID
sleep 5

```

Script da eseguire dopo lo spegnimento: `pulse-jack-post-stop.sh`

```
#!/bin/bash
pacmd suspend false

```

### Vecchio metodo

Il JACK-Audio-Connection-Kit è popolare tra chi lavora in ambito audio, ed è ampiamente supportato dalle relative applicazioni Linux. Si inserisce in una nicchia d'uso simile a quella occupata da Pulseaudio, ma è più adatto ad essere usato da chi lavora in ambito multimediale. In particolare, applicazioni audio come Ardour e Audacity (recentemente), funzionano bene con Jack.

Pulseaudio fornisce i moduli jack-source e jack-sink, che gli permettono di essere avviato come sound server sopra al demone JACK. Ciò consente di impostare valori di volume personalizzati per ogni applicazione che lo necessiti, applicazioni play-back per filmati ed audio, consentendo al tempo stesso di stabilire una interconnettività a bassa latenza per applicazioni di sound processing che si connettono a JACK.

Tuttavia, ciò impedirà a Pulseaudio di scrivere direttamente nei buffers della scheda audio, cosa che aumenterà l'uso complessivo della CPU.

Per provare ad utilizzare Pulseaudio su JACK, è necessario caricare i relativi moduli all'avvio:

```
pulseaudio -L module-jack-sink -L module-jack-source

```

Per usare Pulsaudio con JACK, questo deve essere caricato prima di Pulseaudio, usando un metodo di vostra scelta. Pulseaudio deve quindi essere avviato avendo cura di caricare due moduli rilevanti. Si modifichi `/etc/pulse/default.pa`, cambiando la seguente parte:

```
### Load audio drivers statically (it is probably better to not load
### these drivers manually, but instead use module-hal-detect --
### see below -- for doing this automatically)
#load-module module-alsa-sink
#load-module module-alsa-source device=hw:1,0
#load-module module-oss device="/dev/dsp" sink_name=output source_name=input
#load-module module-oss-mmap device="/dev/dsp" sink_name=output source_name=input
#load-module module-null-sink 
#load-module module-pipe-sink
### Automatically load driver modules depending on the hardware available
.ifexists module-udev-detect.so
load-module module-udev-detect
.else
### Alternatively use the static hardware detection module (for  systems that
### lack udev support)
load-module module-detect
.endif

```

In questo modo:

```
### Load audio drivers statically (it is probably better to not load
### these drivers manually, but instead use module-hal-detect --
### see below -- for doing this automatically)
#load-module module-alsa-sink
#load-module module-alsa-source device=hw:1,0
#load-module module-oss device="/dev/dsp" sink_name=output source_name=input
#load-module module-oss-mmap device="/dev/dsp" sink_name=output source_name=input
#load-module module-null-sink
#load-module module-pipe-sink
load-module module-jack-source
load-module module-jack-sink
### Automatically load driver modules depending on the hardware available
#.ifexists module-udev-detect.so
#load-module module-udev-detect
#.else
### Alternatively use the static hardware detection module (for  systems that
### lack udev support)
#load-module module-detect
#.endif

```

Sostanzialmente, viene qui impedito il caricamento del modulo udev-detect, il quale cercherà di prendere il controllo della vostra scheda audio. (JACK ha già effettutato questa operazione, perciò si otterrà un errore se il modulo viene caricato). Inoltre, i moduli jack-source e jack-sink, devono essere caricati esplicitamente.

#### QjackCtl con script di avvio/shutdown

Usando le impostazioni descritte sopra, è possibile usare [qjackctl](https://www.archlinux.org/packages/?name=qjackctl) per eseguire uno script all'avvio e allo spegnimento per avviare/terminare Pulseaudio. Una delle ragioni percui si possa voler fare una cosa simile è che i cambiamenti riportati sopra disabilitano i moduli di Pulseaudio che si occupano dell'autorilevazione dell'hardware.

Le impostazioni che seguono, sono adatte per utilizzare Pulseaudio con JACK, benché gli script possano essere modificati per essere usati con un setup diverso da questo. Terminare e riavviare Pulseaudio mentre dei programmi lo stanno utilizzando potrebbe rivelarsi problematico.

**Nota:** Per quanto riguarda l'esempio seguente, `padevchooser` è da considerarsi deprecato e sostituito da `pasystray`.

L'esempio seguente può essere usato e modificato secondo le proprie necessità in uno script d'avvio che avvia Pulseaudio in modalità demone e carica il programma [padevchooser](https://aur.archlinux.org/packages/padevchooser/) (opzionale, va compilato dopo averlo scaricato da AUR) chiamato `jack_startup`:

```
#!/bin/bash
#Load PulseAudio and PulseAudio Device Chooser
pulseaudio -D
padevchooser&

```

Segue uno script di shutdown che termina Pulseaudio, chiamato `jack_shutdown`, da posizionare anch'esso nella propria home directory:

```
#!/bin/bash
#Kill PulseAudio and PulseAudio Device Chooser
pulseaudio --kill
killall padevchooser

```

Entrambi gli script devono essere resi eseguibili:

```
chmod +x jack_startup jack_shutdown

```

Poi, una volta avviato QjackCtl, fare click sul pulsante *setup*, selezionare il tab *Opzioni* e spuntare "Execute Script after Startup" e "Execute Script on Shutdown", quindi specificare il percorso relativo ai due script appena visti, avendo cura di salvare le modifiche apportate.

## Pulseaudio attraverso OSS

Si aggiunga la seguente riga ad `/etc/pulse/default.pa`

```
load-module module-oss

```

Poi si avvii Pulseaudio come al solito. Dovrebbero essere disponibili sinks e sorgenti per i propri dispositivi OSS.

## Pulseaudio da chroot

Poiché un ambiente di chroot definisce una root alternativa per l'ingabbiamento e l'utilizzo delle applicazioni, Pulseaudio deve essere installato all'interno dello stesso (`pacman -S pulseaudio` dato da dentro l'ambiente di chroot).

Se Pulseaudio non è configurato per connettersi ad un server specifico (si può ovviare modificando `/etc/pulse/client.conf`, usando la variabile d'ambiente PULSE_SERVER, oppure tramite l'annuncio alle proprietà locali di X11 usando il modulo x11-publish), tenterà di connettersi al server Pulseaudio locale, fallendo ed avviando una nuova istanza dello stesso. Ogni server Pulseaudio è identificato da un ID univoco basato sul valore *machine-id* contenuto in `/var/lib/dbus`. Affinché le applicazioni eseguite all'interno del chroot possano accedere al server, le seguenti directory devono essere montate nel chroot:

```
/var/run
/var/lib/dbus
/tmp
~/.pulse

```

Si consiglia di montare anche `/dev/shm` per ottenere le massime performance ed efficienza. Si noti che montando la `/home`, è possibile condividere la cartella `~/.pulse`.

PulseAudio sceglie il percorso al socket in base al valore di `XDG_RUNTIME_DIR`, percui assicurarsi di importarla durante il chroot via [sudo](/index.php/Sudo_(Italiano) "Sudo (Italiano)") da utente normale (si veda [Sudo (Italiano)#Variabili d'ambiente](/index.php/Sudo_(Italiano)#Variabili_d'ambiente "Sudo (Italiano)")).

Per istruzioni specifiche su come effettuare i vari mount, si faccia riferimento al wiki relativo all'installazione di un ambiente chroot a 32 bit, specialmente si legga la [sezione aggiuntiva](https://wiki.archlinux.org/index.php?title=Arch64_Install_bundled_32bit_system#Additional_mount_option_to_allow_32-bit_apps_to_access_the_64-bit_Pulseaudio_server) relativa a Pulseaudio.

## Disabilitare l'auto spawning del server PulseAudio

Alcuni utenti potrebbero voler avviare il server pulseaudio manualmente prima di eseguire certi programmi e chiuderlo quando questi ultimi hanno portato a termine le proprie operazioni.

È possibile ottenere questo comportamento modificando `/etc/pulse/client.conf`, cambiando `autospawn = yes` in `autospawn = no`, ed impostando la variabile `daemon-binary` a `/bin/true`. Ci si assicuri inoltre che le due linee di cui sopra siano decommentate:

 `/etc/pulse/client.conf` 
```
autospawn = no
daemon-binary = /bin/true 

```

È ora possibile avviare manualmente pulseaudio con:

```
$ pulseaudio --start

```

e terminarlo con:

```
$ pulseaudio --kill

```

Potrebbe inoltre essere necessario rimuovere o rinominare il file `.desktop` in `/etc/xdg/autostart`, se presente.

## Mappare il canale stereo su mono

È possibile rimappare un sink di input stereo in un sink mono utilizzando un sink virtuale. Si aggiunga ad `/etc/pulse/default.pa`:

```
load-module module-remap-sink master=alsa_output.pci-0000_00_1f.5.analog-stereo sink_name=mono channels=2 channel_map=mono,mono

```

1.  Opzionale: Impostare il sink appena creato come predefinito.

```
set-default-sink mono

```

**Nota:** Sostituire ad `alsa_output.pci-0000_00_1f.5.analog-stereo` il nome della propria scheda audio, come visualizzato da `pacmd list-sinks`.