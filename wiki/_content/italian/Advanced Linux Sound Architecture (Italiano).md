L' [Architettura Avanzata per il Suono su Linux](https://en.wikipedia.org/wiki/Advanced_Linux_Sound_Architecture "wikipedia:Advanced Linux Sound Architecture") (conosciuta con l'acronimo di **ALSA**) è un componente del kernel che rimpiazza l'originale Open Sound System (OSSv3) utilizzato per fornire driver di periferica per le schede audio. Oltre ai driver audio, **ALSA** mette a disposizione anche una libreria in spazio-utente per sviluppatori di applicazioni che vogliano utilizzare le funzioni dei driver tramite un'API piuttosto che con un'interazione diretta con i driver del kernel.

**Nota:** Per una eventuale alternativa consultare la pagina [OSS](/index.php/OSS "OSS").

## Contents

*   [1 Installazione](#Installazione)
    *   [1.1 Utility](#Utility)
*   [2 Togliere il muto ai canali](#Togliere_il_muto_ai_canali)
*   [3 Configurazione](#Configurazione)
    *   [3.1 Nessun suono in VirtualBox](#Nessun_suono_in_VirtualBox)
    *   [3.2 Impostare la scheda audio predefinita](#Impostare_la_scheda_audio_predefinita)
        *   [3.2.1 Selezionare il PCM di default tramite variabili d'ambiente](#Selezionare_il_PCM_di_default_tramite_variabili_d.27ambiente)
        *   [3.2.2 Metodo alternativo](#Metodo_alternativo)
    *   [3.3 Assicurarsi che i moduli audio siano caricati](#Assicurarsi_che_i_moduli_audio_siano_caricati)
    *   [3.4 Ottenere un output SPDIF](#Ottenere_un_output_SPDIF)
    *   [3.5 Equalizzatore System-Wide](#Equalizzatore_System-Wide)
        *   [3.5.1 Utilizzando AlsaEqual (fornisce l’interfaccia grafica)](#Utilizzando_AlsaEqual_.28fornisce_l.E2.80.99interfaccia_grafica.29)
            *   [3.5.1.1 Gestire gli stati di AlsaEqual](#Gestire_gli_stati_di_AlsaEqual)
        *   [3.5.2 Utilizzando mbeq](#Utilizzando_mbeq)
*   [4 Ricampionamento in alta qualità](#Ricampionamento_in_alta_qualit.C3.A0)
*   [5 Upmixing/Downmixing](#Upmixing.2FDownmixing)
    *   [5.1 Upmixing](#Upmixing)
    *   [5.2 Downmixing](#Downmixing)
*   [6 Mixaggio](#Mixaggio)
    *   [6.1 Mixaggio software (dmix)](#Mixaggio_software_.28dmix.29)
    *   [6.2 Mixaggio Hardware](#Mixaggio_Hardware)
        *   [6.2.1 Supporto](#Supporto)
        *   [6.2.2 Fix](#Fix)
*   [7 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [7.1 Suono che salta utilizzando Dynamic Frequency Scaling](#Suono_che_salta_utilizzando_Dynamic_Frequency_Scaling)
    *   [7.2 Problemi con la disponibilità del mixaggio software per più di un utente per volta](#Problemi_con_la_disponibilit.C3.A0_del_mixaggio_software_per_pi.C3.B9_di_un_utente_per_volta)
    *   [7.3 Problemi di riproduzione simultanea](#Problemi_di_riproduzione_simultanea)
    *   [7.4 Mancanza di suono casuale](#Mancanza_di_suono_casuale)
        *   [7.4.1 Timidity](#Timidity)
    *   [7.5 Problemi specifici di alcuni programmi](#Problemi_specifici_di_alcuni_programmi)
    *   [7.6 Impostazione modelli](#Impostazione_modelli)
    *   [7.7 Audio in conflitto con altoparlante interno del PC](#Audio_in_conflitto_con_altoparlante_interno_del_PC)
    *   [7.8 Nessun Input dal Microfono](#Nessun_Input_dal_Microfono)
    *   [7.9 Impostazione predefinita Microfono/Dispositivo di acquisizione](#Impostazione_predefinita_Microfono.2FDispositivo_di_acquisizione)
    *   [7.10 Il microfono interno non funziona](#Il_microfono_interno_non_funziona)
    *   [7.11 Nessun suono con scheda integrata Intel](#Nessun_suono_con_scheda_integrata_Intel)
    *   [7.12 Nessun suono dalle cuffie con scheda audio integrata Intel](#Nessun_suono_dalle_cuffie_con_scheda_audio_integrata_Intel)
    *   [7.13 Nessun suono quando è installata la scheda video con S/PDIF](#Nessun_suono_quando_.C3.A8_installata_la_scheda_video_con_S.2FPDIF)
    *   [7.14 La qualità dell'audio è bassa](#La_qualit.C3.A0_dell.27audio_.C3.A8_bassa)
    *   [7.15 Rumori/Suoni all’avvio ed allo stop della riproduzione](#Rumori.2FSuoni_all.E2.80.99avvio_ed_allo_stop_della_riproduzione)
    *   [7.16 L'uscita S/PDIF non funziona](#L.27uscita_S.2FPDIF_non_funziona)
    *   [7.17 L'uscita HDMI non funziona](#L.27uscita_HDMI_non_funziona)
    *   [7.18 HP TX2500](#HP_TX2500)
    *   [7.19 Salto di suono durante la riproduzione MP3](#Salto_di_suono_durante_la_riproduzione_MP3)
    *   [7.20 Cuffia USB e schede audio esterne USB](#Cuffia_USB_e_schede_audio_esterne_USB)
        *   [7.20.1 Suono gracchiante su dispositivi USB](#Suono_gracchiante_su_dispositivi_USB)
        *   [7.20.2 Inserimento a caldo di una scheda audio USB](#Inserimento_a_caldo_di_una_scheda_audio_USB)
    *   [7.21 Errore 'Unknown hardware' dopo aggiornamento Kernel](#Errore_.27Unknown_hardware.27_dopo_aggiornamento_Kernel)
    *   [7.22 HDA Analyzer](#HDA_Analyzer)
    *   [7.23 ALSA con SDL](#ALSA_con_SDL)
    *   [7.24 Workaround in caso di volume basso](#Workaround_in_caso_di_volume_basso)
    *   [7.25 "Schiocco" al resume dopo una sospensione](#.22Schiocco.22_al_resume_dopo_una_sospensione)
*   [8 Configurazioni d'esempio](#Configurazioni_d.27esempio)
*   [9 Link esterni](#Link_esterni)

## Installazione

ALSA è incluso nel kernel di default di Arch come insieme di moduli, perciò non è necessario installarlo esplicitamente.

[Udev](/index.php/Udev_(Italiano) "Udev (Italiano)") interrogherà automaticamente l'hardware al boot, caricando il modulo del kernel corretto per l'hardware rilevato. Perciò, la scheda audio dovrebbe essere subito funzionante, ma di default la configurazione prevederà che tutti i canali siano impostati su muto.

Gli utenti con un login locale (su terminale virtuale o tramite display manager) hanno la facoltà di riprodurre l'audio e modificare i canali del mixer. Per consentire queste operazioni a chi ha un login remoto, l'utente deve essere [inserito](/index.php/Utenti_e_Gruppi#Gestione_dei_gruppi "Utenti e Gruppi") nel gruppo `audio`. L'aggiunta dell'utente al gruppo `audio` consente anche l'accesso diretto ai dispositivi, e ciò potrebbe portare alcune applicazioni ad impadronirsi in maniera esclusive di alcune uscite (rendendo impossibile il mixaggio software), impedire il passaggio rapido ad un altro utente, ed il sistema multiseat. Per questi motivi l'aggiunto di un utente al gruppo `audio` **non** è raccomandata, a meno di necessità specifiche. [[1]](https://wiki.ubuntu.com/Audio/TheAudioGroup).

### Utility

Installare dai [repository ufficiali](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)") il pacchetto [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils), contenente lo strumento `alsamixer`, che consente la configurazione delle periferiche audio tramite console o terminale. Installare anche il pacchetto [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins) se si necessità del [ricampionamento in alta qualità](#Ricampionamento_in_alta_qualit.C3.A0), dell'[upmixing/downmixing](#Upmixing.2FDownmixing) e di altre funzionalità avanzate. Se si vuole che le applicazioni basate su [OSS](/index.php/Open_Sound_System_(Italiano) "Open Sound System (Italiano)") funzionino tramite dmix (mixaggio software) installare anche il pacchetto [alsa-oss](https://www.archlinux.org/packages/?name=alsa-oss). Caricare i [moduli del kernel](/index.php/Kernel_modules_(Italiano) "Kernel modules (Italiano)") `snd_seq_oss`, `snd_pcm_oss` e `snd_mixer_oss` per abilitare i componenti di emulazione di OSS.

## Togliere il muto ai canali

La versione attuale di ALSA, viene installata con tutti i canali impostati su **muto di default**. Sarà necessario togliere il "muto" manualmente. Il metodo più semplice per fare ciò è utilizzare l'interfaccia utente in ncurses `alsamixer`.

`$ alsamixer`

Alternativamente, è possibile utilizzare `amixer` da riga di comando:

`$ amixer sset Master unmute`

In `alsamixer`, l'etichetta `MM` sotto un canale indica che quest'ultimo è impostato su muto, mentre `00` indica che è attivo.

Togliere il muto dai canali `Master` e `PCM` posizionandovi sopra di essi tramite i tasti `←` e `→` e premendo il tasto `M`. Usare il tasto `↑` per incrementare il volume ed ottenere un `db gain` pari a 0\. Il valore di gain si trova in alto a sinistra dopo il campo `Item:`. Valori di gain superiori produrranno suoni distorti.

Per ottenere un vero suono surround 5.1 o 7.1, è necessario togliere il muto anche ad altri canali come Front, Surround, Center, LFE (subwoofer) e Side (questi sono i nomi dei canali per il modulo intel HDA, possono variare in base all'hardware). Si tenga presente che ciò non abilita direttamente l'upmixing delle sorgenti stereo (come la maggior parte della musica). Per ottenere quell'effetto è necessario consultare il paragrafo [upmixing/downmixing](#Upmixing.2FDownmixing).

Per abilitare il microfono, portarsi sulla tab Capture tramite `F4` ed abilitare il canale premendo `Spazio`

Uscire da alsamixer premendo `Esc`.

**Nota:** Alcune schede necessitano del canale digitale disattivato per produrre suono sull'uscita analogica. Per la SoundBlaster Audigy LS è necessario impostare su muto il canale IEC958. Alcuni sistemi (come il Thinkpad T61), richiedono che anche il canale Speaker sia attivato e regolato.

Alcuni sistemi, (come il Dell E6400) potrebbero anche richiedere che ai canali `Front` ed `Headphone` venga tolto il muto e che vengano regolati.

Si può ora verificare che il suono funzioni:

`$ speaker-test -c 2`

Modificare il valore di `-c` in base al proprio sistema, ad esempio utilizzare `-c 8` per un 7.1.

`$ speaker-test -c 8`

Se non dovesse funzionare, passare al paragrafo [#Configurazione](#Configurazione) e quindi a [#Risoluzione dei problemi](#Risoluzione_dei_problemi).

Il pacchetto [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) include `alsa-restore.service` e `alsa-store.service` che sono preconfigurati per essere eseguiti rispettivamente all'avvio ed allo spegnimento.

## Configurazione

### Nessun suono in VirtualBox

Se si riscontrassero problemi audio in VirtualBox, il seguente comando potrebbe essere d'aiuto.

 `$ alsactl init` 
```

Found hardware: "ICH" "SigmaTel STAC9700,83,84" "AC97a:83847600" "0x8086" "0x0000"
Hardware is initialized using a generic method

```

Potrebbe essere necessario attivare l'uscita ALSA anche nel proprio software audio.

### Impostare la scheda audio predefinita

Se l'ordine delle schede audio del sistema cambia ad ogni avvio, è possibile renderlo immutabile specificandolo all'interno di un file col suffisso `.conf` all'interno di `/etc/modprobe.d` (`/etc/modprobe.d/alsa-base.conf` è quello solitamente usato).

Ad esempio, se si desidera che la scheda audio mia sia la #0

 `/etc/modprobe.d/alsa-base.conf` 
```
options snd slots=snd_mia,snd_hda_intel
options snd_mia index=0
options snd_hda_intel index=1

```

Utilizzare `$ lsmod | grep snd` per ottenere la lista dei dispositivi. Questa configurazione presuppone che sul sistema siano presenti una scheda audio mia che utilizza `snd_mia` ed un'altra (ad esempio integrata sulla scheda madre) che utilizza `snd_hda_intel`.

Si può anche istruire ALSA ad utilizzare un indice di `-2` per non far utilizzare mai una determinata scheda come primaria. Distribuzioni come Ubuntu e Mint utilizzano questo sistema per evitare che schede audio USB ed altri dispositivi "particolari" ottengano l'indice `0`

 `/etc/modprobe.d/alsa-base.conf` 
```
options bt87x index=-2
options cx88_alsa index=-2
options saa7134-alsa index=-2
options snd-atiixp-modem index=-2
options snd-intel8x0m index=-2
options snd-via82xx-modem index=-2
options snd-usb-audio index=-2
options snd-usb-caiaq index=-2
options snd-usb-ua101 index=-2
options snd-usb-us122l index=-2
options snd-usb-usx2y index=-2
options snd-pcsp index=-2
options snd-usb-audio index=-2
```

Questa modifica richiede il riavvio del sistema.

#### Selezionare il PCM di default tramite variabili d'ambiente

Nel proprio file di configurazione, preferibilmente quello globale, aggiungere

```
 pcm.!default {
   type plug
   slave.pcm {
     @func getenv
     vars [ ALSAPCM ]
     default "hw:Audigy2"
   }
 }

```

È necessario sostituire la riga default col nome della propria scheda (nell'esempio è `Audigy2`). Si può ottenere il nome necessario tramite `aplay -l` oppure si possono utilizzare PCM come **surround51**. Se però è necessario utilizzare il microfono, è una buona idea selezionare full-duplex PCM come default. Ora sarà possibile avviare programmi selezionando la scheda audio desiderata semplicemente cambiando il valore della variabile `ALSAPCM`. Si rivela utile per tutti quei programmi che non consentono di selezionare la scheda audio da utilizzare, per gli altri assicurarsi di aver mantenuto la scheda di default. Ad esempio, consideriamo il caso in cui si sia creato un downmix PCM dal nome **mix51to20**, sarà possibile utilizzarlo con `mplayer` attraverso questo comando

`ALSAPCM=mix51to20 mplayer example_6_channel.wav`

#### Metodo alternativo

Bisogna innanzitutto rilevare gli id della scheda e del dispositivo che si vogliono impostare come predefiniti eseguendo `aplay -l`.

 `$ aplay -l` 
```
**** List of PLAYBACK Hardware Devices ****
card 0: Intel [HDA Intel], device 0: CONEXANT Analog [CONEXANT Analog]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 0: Intel [HDA Intel], device 1: Conexant Digital [Conexant Digital]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 1: JamLab [JamLab], device 0: USB Audio [USB Audio]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 2: Audio [Altec Lansing XT1 - USB Audio], device 0: USB Audio [USB Audio]
  Subdevices: 1/1
  Subdevice #0: subdevice #0

```

Ad esempio, l'ultima voce in questa lista si riferisce alla scheda con id 2, ed al dispositivo con id 0\. Per impostarli come predefinit1, si può sia utilizzare il file di sistema `/etc/asound.conf`, sia quello con influenza limitata sul singolo utente `~/.asoundrc`. Potrebbe essere necessario creare il file se quest0ultimo non dovesse esistere.. Dopodichè inserirvi le seguenti opzioni con i corrispondenti id relativi alla scheda ed al dispositivo:

```
defaults.pcm.card 2
defaults.pcm.device 0
defaults.ctl.card 2

```

L'opzione `pcm` specifica quale scheda e dispositivo verranno utilizzati per la riproduzione dell'audio, mentre l'opzione `ctl` indica quali saranno controllati da utility come alsamixer. Le opzioni dovrebbere essere effettive nel momento in cui un'applicazione relativa ad esse (mplayer, alsamixer, etc...) viene riavviata.

### Assicurarsi che i moduli audio siano caricati

Verificare che udev abbia rilevato automaticamente l'audio,con il comando:

 `$ lsmod|grep '^snd'| column -t ` 
```
snd_hda_codec_hdmi     22378   4
snd_hda_codec_realtek  294191  1
snd_hda_intel          21738   1
snd_hda_codec          73739   3  snd_hda_codec_hdmi,snd_hda_codec_realtek,snd_hda_intel
snd_hwdep              6134    1  snd_hda_codec
snd_pcm                71032   3  snd_hda_codec_hdmi,snd_hda_intel,snd_hda_codec
snd_timer              18992   1  snd_pcm
snd                    55132   9  snd_hda_codec_hdmi,snd_hda_codec_realtek,snd_hda_intel,snd_hda_codec,snd_hwdep,snd_pcm,snd_timer
snd_page_alloc         7017    2  snd_hda_intel,snd_pcm

```

Se l'output è simile, i driver audio sono stati autorilevati con successo. Si può anche controllare la directory `/dev/snd` per visualizzare i giusti file del dispositivo:

**Nota:** A partire da udev>=171, i moduli per l'emulazione OSS (`snd_seq_oss, snd_pcm_oss, snd_mixer_oss`) non sono più caricati automaticamente di default: [Impostarne il caricamento](/index.php/Kernel_modules_(Italiano)#Caricamento "Kernel modules (Italiano)") se si desidera che vengano caricati automaticamente ad ogni avvio.

Si potrebbe anche controllare la directory `/dev/snd/` per conoscere i nomi di dispositivo corretti:

 `$ ls -l /dev/snd/` 
```
total 0
crw-rw----  1 root audio 116,  0 Apr  8 14:17 controlC0
crw-rw----  1 root audio 116, 32 Apr  8 14:17 controlC1
crw-rw----  1 root audio 116, 24 Apr  8 14:17 pcmC0D0c
crw-rw----  1 root audio 116, 16 Apr  8 14:17 pcmC0D0p
crw-rw----  1 root audio 116, 25 Apr  8 14:17 pcmC0D1c
crw-rw----  1 root audio 116, 56 Apr  8 14:17 pcmC1D0c
crw-rw----  1 root audio 116, 48 Apr  8 14:17 pcmC1D0p
crw-rw----  1 root audio 116,  1 Apr  8 14:17 seq
crw-rw----  1 root audio 116, 33 Apr  8 14:17 timer

```

**In caso di richiesta di aiuto su IRC o sui forum, per favore postare l'output dei comandi precedenti.**

Se sono presenti i dispositivi `controlC0` e `pcmC0D0p` o simili, allora i moduli audio sono stati rilevati e caricati correttamente.

Altrimenti, i moduli audio non sono stati rilevati correttamente. Per risolvere, provare a caricare i moduli manualmente:

*   Individuare il modulo della scheda audio: [ALSA Soundcard Matrix](http://www.alsa-project.org/main/index.php/Matrix:Main). Il modulo sarà preceduto dal suffisso 'snd-' (ad esempio: 'snd-via82xx').
*   [Caricare i moduli](/index.php/Kernel_modules_(Italiano)#Caricamento "Kernel modules (Italiano)"):
*   Controllare i file del dispositivo in `/dev/snd` (vedi sopra) e/o provare se `alsamixer` o `amixer` hanno un corretto output.
*   Configurare `snd-NOME-DEL-MODULO` e `snd-pcm-oss` in modo che [vengano caricati all'avvio](/index.php/Kernel_modules_(Italiano)#Caricamento "Kernel modules (Italiano)").

### Ottenere un output SPDIF

(da gralves dai forum di Gentoo)

*   Nel Controllo Volume di GNOME, sotto il tab delle opzioni, cambiare IEC958 in PCM. Questa opzione può essere abilitata nelle preferenze.
*   Se non è installato il Controllo Volume di GNOME,
    *   Editare `/var/lib/alsa/asound.state`. In questo file alsasound salva le regolazioni del mixer.
    *   Trovare la riga che riporta: `IEC958 Playback Switch`. Vicino ad essa c'è una riga nella quale è indicato `value:false`. Cambiarla in `value:true`.
    *   Adesso trovare questa riga: `IEC958 Playback AC97-SPSA`. Cambiare il suo valore in `0`.
    *   Riavviare alsa.

Un metodo alternativo per abilitare un output SPDIF automaticamente al login (testato su una SoundBlaster Audigy) è il seguente:

*   aggiungere le seguenti righe in `/etc/rc.local`:

 `/etc/rc.local` 
```
# Use COAX-digital output
amixer set 'IEC958 Optical' 100 unmute
amixer set 'Audigy Analog/Digital Output Jack' on

```

Si può visualizzare il nome dell'uscita digitale della scheda con:

 `$ amixer scontrols` 

### Equalizzatore System-Wide

#### Utilizzando AlsaEqual (fornisce l’interfaccia grafica)

Installare [alsaequal](https://aur.archlinux.org/packages/alsaequal/) da [AUR](/index.php/AUR "AUR").

**Note:** Se si utilizza un sistema x86_64 e 32bit-flashplugin, il suono in flash non funzionerà. Si dovrà quindi o disabilitare alsaequal o compilarlo per 32bit.

Dopo aver installato il pacchetto, inserire nel file di configurazione ALSA (`~/.asoundrc` o `/etc/asound.conf`) quanto segue:

 `~/.asoundrc` 
```
ctl.equal {
 type equal;
}

pcm.plugequal {
  type equal;
  # Modify the line below if you don't
  # want to use sound card 0.
  #slave.pcm "plughw:0,0";
  #by default we want to play from more sources at time:
  slave.pcm "plug:dmix";
}

#pcm.equal {
  # Or if you want the equalizer to be your
  # default soundcard uncomment the following
  # line and comment the above line.
pcm.!default {
  type plug;
  slave.pcm plugequal;
}

```

Ora si è pronti per modificare l’equalizzatore tramite il comando:

 `$ alsamixer -D equal` 

Si noti che il file di configurazione, diverso per ogni utente (se non diversamente specificato), viene salvato in `$HOME/.alsaequal.bin`. Perciò se si vuole utilizzare AlsaEqual con [mpd](/index.php/Mpd "Mpd") o con un altro software, con un utente diverso, è possibile configurarlo con il comando:

 `# su mpd -c 'alsamixer -D equal` 

Oppure, è possibile creare un link simbolico a `.alsaequal.bin` nella home di quell’utente.

##### Gestire gli stati di AlsaEqual

Installare [alsaequal-mgr](http://xyne.archlinux.ca/projects/alsaequal-mgr/) da [Xyne's repos](http://xyne.archlinux.ca/repos/) o da [AUR](https://aur.archlinux.org/packages.php?ID=62420).

Configurare l'equalizzatore come al solito tramite

`$ alsamixer -D equal`

Quando si è soddisfatti del risultato, si può dare un nome alla configurazione ("foo" in questo esempio) e salvarlo:

`alsaequal-mgr save foo`

Lo stato "foo" può essere richiamato in seguito tramite

`$ alsaequal-mgr load foo`

È quindi possibile creare stati differenziati per giochi, film, generi musicali, applicazioni VoIP, etc. e caricarli quando necessario.

Consultare [project page](http://xyne.archlinux.ca/projects/alsaequal-mgr/) ed i messaggi di aiuto per ulteriori informazioni.

#### Utilizzando mbeq

**Nota:** Questo metodo richiede l'utilizzo del plugin ladspa che può comportare un consumo un po' più alto della CPU quando si esegue un suono. Inoltre, questo metodo è pensato per l'utilizzo di un suono stereofonico (ad esempio, ottimizzato per un ascolto tramite cuffie)

Installare [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins), [ladspa](https://www.archlinux.org/packages/?name=ladspa) e [swh-plugins](https://www.archlinux.org/packages/?name=swh-plugins)

*   sarà necessario avere uno dei file tra `~/.asoundrc` e `/etc/asound.conf`, dunque, se non è ancora stato fatto, creare uno dei due

 `touch ~/.asoundrc` 

ed inserirvi le seguenti righe:

 `/etc/asound.conf` 
```
pcm.eq {
  type ladspa

  # The output from the EQ can either go direct to a hardware device
  # (if you have a hardware mixer, e.g. SBLive/Audigy) or it can go
  # to the software mixer shown here.
  #slave.pcm "plughw:0,0"
  slave.pcm "plug:dmix"

  # Sometimes you may need to specify the path to the plugins,
  # especially if you have just installed them.  Once you have logged
  # out/restarted this should not be necessary, but if you get errors
  # about being unable to find plugins, try uncommenting this.
  #path "/usr/lib/ladspa"

  plugins [
    {
      label mbeq
      id 1197
      input {
        #this setting is here by example, edit to your own taste
        #bands: 50hz, 100hz, 156hz, 220hz, 311hz, 440hz, 622hz, 880hz, 1250hz, 1750hz, 25000hz,
        #50000hz, 10000hz, 20000hz
        controls [ -5 -5 -5 -5 -5 -10 -20 -15 -10 -10 -10 -10 -10 -3 -2 ]
      }
    }
  ]
 }

 # Redirect the default device to go via the EQ - you may want to do
 # this last, once you're sure everything is working.  Otherwise all
 # your audio programs will break/crash if something has gone wrong.

 pcm.!default {
  type plug
  slave.pcm "eq"
 }

 # Redirect the OSS emulation through the EQ too (when programs are running through "aoss")

 pcm.dsp0 {
  type plug
  slave.pcm "eq"
 }

```

*   ora tutto dovrebbe essere sistemato

## Ricampionamento in alta qualità

Quando viene abilitato il mixaggio software, ALSA è costretto a ricampionare tutto alla stessa frequenza (di default a 48000, se supportata). Dmix utilizza un algoritmo di ricampionamento poco efficace, che produce una notevole perdita di qualità.

Installare [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins) e [libsamplerate](https://www.archlinux.org/packages/?name=libsamplerate)

Modificare il tasso di conversione di default a libsamplerate

 `/etc/asoundrc`  `defaults.pcm.rate_converter "samplerate_best"` 

**samplerate_best** offre la miglior qualità audio, ma necessità di cpu almeno decenti, in quanto il ricampionamento in tempo reale richiede un numero notevole di cicli di cpu. Sono disponibili anche altri algoritmi (**samplerate**, etc.) ma non forniscono tangibili miglioramenti rispetto al ricampionatore di default.

## Upmixing/Downmixing

### Upmixing

Per fare in modo che una sorgente audio stereo saturi tutte le uscite di un sistema che ne ha più di 2, come 5.1 o 7.1, è necessario effettuare un upmixing. In passato questa procedura risultava complessa e suscettibile di errori, ma al giorno d'oggi esistono dei plugin che se ne occupano. In questo esempio si utilizzerà il plugin `upmix`, incluso in [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins).

Dopodichè aggiungere il seguente codice al file di configurazione di ALSA a propria scelta (`/etc/asound.conf` oppure `~/.asoundrc`):

 `~/.asoundrc` 
```
pcm.upmix71 {
     type upmix
     slave.pcm "surround71"
     delay 15
     channels 8
 }

```

È intuitivo come adeguare questo esempio da 7.1 ad altro sistema.

Questo metodo aggiunge un nuovo pcm che è possibile utilizzare per l'upmixing. Se si vuole che tutte le sorgenti audio vengano redirette verso questo pcm, aggiungerlo come default successivamente al codice appena scritto, in questo modo

 `~/.asoundrc` 
```
....
pcm.!default "plug:upmix71"
....

```

Il plugin consente automaticamente alle sorgenti di essere riprodotte attraverso di esso, quindi impostarlo come predefinito è una scelta sicura. Se ciò non dovesse funzionare, si può provare a impostare dmix affinchè effettui l'upmixing del canale PCM in questo modo

 `~/.asoundrc` 
```
pcm.dmix6 {
    type asym
    playback.pcm {
        type dmix
        ipc_key 567829
        slave {
            pcm "hw:0,0"
            channels 6
        }
    }
}

```

ed usare "dmix6" al posto di "surround71". Se si dovessero riscontrare problemi di suono che salta o risulta distorto, provare ad incrementare la dimensione del buffer (ad esempio a 32768) oppure utilizzare un [ricampionatore di alta qualità](#Ricampionamento_in_alta_qualit.C3.A0).

### Downmixing

Se si vuole effettuare il downmixing, ad esempio per ascoltare su un'uscita stereo il sonoro di un video in 5.1, è necessario utilizzare il plugin `vdownmix` contenuto in [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins).

Nel file di configurazione aggiungere quanto segue

 `~/.asoundrc` 
```
pcm.!surround51 {
     type vdownmix
     slave.pcm "default"
 }
 pcm.!surround40 {
     type vdownmix
     slave.pcm "default"
 }

```

## Mixaggio

### Mixaggio software (dmix)

Sistema di mixaggio software di ALSA

**Nota:** : Per versioni di ALSA uguali o superiori alla 1.0.9rc2 non vi è necessità di configurare dmix per le uscite audio analogiche. Dmix è abilitato di default se viene rilevata una scheda audio che non supporta il mixaggio via hardware.

Se comunque non dovesse funzionare automaticamente è sufficiente creare il (o modificare l'esistente) file `~/.asoundrc` con questo contenuto:

 `~/.asoundrc` 
```
pcm.dsp {
    type plug
    slave.pcm "dmix"
}

```

Questo dovrebbe abilitare il mixaggio software ed abilitare più applicazioni all'accesso alla periferica contemporaneamente. Per le uscite audio digitali come S/PDIF, il pacchetto ALSA tuttora non abilita dmix di default. Perciò la configurazione appena mostrata si rivela in questo caso necessaria per l'utilizzo del mixaggio software su uscite S/PDIF. Consultare [#Risoluzione dei problemi](#Risoluzione_dei_problemi) per soluzioni a problemi comuni.

### Mixaggio Hardware

#### Supporto

Se sul sistema è presente un chipset audio che supporta il mixaggio hardware, non è richiesta alcuna configurazione. Quasi tutti i chip integrati nelle schede madri non supportano il mixaggio hardware, e obbligano ad effettuare un mixaggio via software (vedere paragrafo precedente). Molte schede audio supportano il mixaggio hardware, e quelle meglio supportate su Linux sono le seguenti:

*   Creative SoundBlaster Live! (5.1 model)
*   Creative SoundBlaster Audigy (some models)
*   Creative SoundBlaster Audidy 2 (ZS models)
*   Creative SoundBlaster Audigy 4 (Pro models)

**Nota:**

*   Le versioni economiche delle suddette schede, (Audigy SE, Audigy 2 NX, SoundBlaster Live! 24bit and SoundBlaster Live! 7.1) **non** supportano il mixaggio hardware, in quanto utilizzano chip differenti.
*   Il chip integrato VIA8237 che supporta il mixaggio hardware di 4 flussi. In realtà ridotti a 3 su alcune schede madri (il quarto non emette suono). Anche se funzionante, la qualità del suono non è comparabile a quella delle altre soluzioni.

#### Fix

Si si utilizza Arch64 e la scheda Intel Corporation 82801I (ICH9 Family) HD Audio Controller (rev 02), bisogna impostare alcuni parametri per ottenere suono da Enemy Territory:

```
$ echo "et.x86 0 0 direct" > /proc/asound/card0/pcm0p/oss
$ echo "et.x86 0 0 disable" > /proc/asound/card0/pcm0c/oss
```

## Risoluzione dei problemi

### Suono che salta utilizzando Dynamic Frequency Scaling

Alcune combinazioni di determinati driver ALSA e chipset, possono causare dei "salti" nel suono da tutte le sorgenti se utilizzati in combinazione con un governor dinamico della frequenza della cpu come `ondemand` o `conservative`. Attualmente, l'unica soluzione è di passare al governor `performance`. Fare riferimento alla pagina [CPU Frequency Scaling (Italiano)](/index.php/CPU_Frequency_Scaling_(Italiano) "CPU Frequency Scaling (Italiano)") per ulteriori informazioni.

### Problemi con la disponibilità del mixaggio software per più di un utente per volta

Può capitare di rilevare che solo un utente per volta può utilizzare dmix. Questa situazione può andar bene per la maggior parte degli utenti, ma coloro i quali utilizzano [mpd](/index.php/Mpd "Mpd") come utente differente, ciò diviene un problema. Quando mpd è in esecuzione un utente non può eseguire suoni tramite dmix. Nonostante sia sufficiente eseguire mpd tramite l'account utente di login, è stata trovata anche un'altra soluzione. L'aggiunta della riga `ipc_key_add_uid 0` al blocco `pcm.dmixer` disabilita questa limitazione. Quello seguente è un estratto del codice di `/etc/asound.conf`, il resto è identico a quello mostrato in precedenza.

 `/etc/asound.conf` 
```
...
pcm.dmixer {
 type dmix
 ipc_key 1024
 ipc_key_add_uid 0 
 ipc_perm 0660
slave {
...

```

### Problemi di riproduzione simultanea

Se si hanno problemmi a riprodurre più tracce contemporaneamente, e se è installto [PulseAudio](/index.php/PulseAudio "PulseAudio") (ad esempio utilizzando [GNOME](/index.php/GNOME "GNOME")), la sua configurazione di default verrà utilizzata automaticamente. Alcuni utenti potrebbero non voler utilizzare [PulseAudio](/index.php/PulseAudio "PulseAudio") trovandosi bene con le proprie configurazioni di ALSA. Un metodo per risolvere il problema, è modificare il file `/etc/asound.conf` e commentare le righe seguenti:

```
# Use PulseAudio by default
#pcm.!default {
#  type pulse
#  fallback "sysdefault"
#  hint {
#    show on
#    description "Default ALSA Output (currently PulseAudio Sound Server)"
#  }
#}

```

Commentare anche queste potrebbe rivelarsi necessario:

```
#ctl.!default {
#  type pulse
#  fallback "sysdefault"
#}

```

Questa può rivelarsi una soluzione più semplice rispetto alla totale disinstallazione di [PulseAudio](/index.php/PulseAudio "PulseAudio"). Qui di seguito viene mostrato un esempio di un `/etc/asound.conf` correttamente funzionante.

```
cm.dmixer {
        type dmix
        ipc_key 1024
        ipc_key_add_uid 0
        ipc_perm 0660
}
pcm.dsp {
        type plug
        slave.pcm "dmix"
}

```

**Nota:** Questo `/etc/asound.conf` è stato creato ed utilizzato con successo per una configurazione globale di [MPD](/index.php/Music_Player_Daemon_(Italiano) "Music Player Daemon (Italiano)"). Consultare [questa sezione](#Problemi_con_la_disponibilit.C3.A0_del_mixaggio_software_per_pi.C3.B9_di_un_utente_per_volta)

### Mancanza di suono casuale

Si può testare velocemente il comparto audio eseguendo `speaker-test`. Se non viene emesso alcun suono, il messaggio d'errore dovrebbe essere qualcosa di simile a:

```
ALSA lib pcm_dmix.c:1022:(snd_pcm_dmix_open) unable to open slave
Playback open error: -16
Device or resource busy
```

Se non si ottiene alcun suono all'avvio del sistema, può darsi che sul proprio sistema siano presenti più schede audio, e che il loro ordine cambi ad ogni avvio. Se fosse questo il caso, seguire [#Impostare la scheda audio predefinita questo paragrafo](#Impostare_la_scheda_audio_predefinita_questo_paragrafo)

Se si utilizza mpd ed il consiglio precedente non dovesse funzionare provare [[questa soluzione](http://mpd.wikia.com/wiki/Configuration#ALSA_MPD_software_volume_control)

#### Timidity

[Timidity](/index.php/Timidity "Timidity") potrebbe essere la causa della mancanza di suono. Provare ad eseguire:

`systemctl status timidity`

Se l'avvio del demone dovesse risultare fallito, provare ad eseguire `# killall -9 timidity`. Se questo dovesse risolvere il problema, sarà necessario disabilitare l'avvio automatico del demone.

### Problemi specifici di alcuni programmi

Per alcuni programmi che continuano ad utilizzare i loro propri settaggi audio, come XMMS ed Mplayer, potrebbe rendersi necessaria l'impostazione dei loro specifici parametri. Per Mplayer, aprire`~/.mplayer/config` (o `/etc/mplayer/mplayer.conf` per un'impostazione globale) ed aggiungere la seguente linea `ao=alsa`

Per XMMS/Beep Media Player, portarsi nella scheda delle preferenze ed assicurarsi che sia selezionato come sistema audio ALSA e non OSS. Per fare ciò in XMMS

*   Aprire XMMS
    *   Opzioni -> Preferenze.
    *   Scegliere il plugin di uscita ALSA.

Per applicazioni che non forniscono compatibilità con ALSA è possibile utilizzare il pacchetto alsa-oss. Per utilizzare aoss, eseguire il programma anteponendogli `aoss`, ad esempio: `aoss realplay`

`pcm.!default{ ... }` sembra non funzionare più, al suo posto si può utilizzare `pcm.default pcm.dmixer`

### Impostazione modelli

Anche se Alsa rileva la scheda audio attraverso il BIOS a volte può non essere in grado di riconoscerne [il modello](http://www.kernel.org/doc/Documentation/sound/alsa/HD-Audio-Models.txt). Il chip della scheda audio può essere trovato in `alsamixer` (ad esempio ALC662) e il modello può essere impostato in `/etc/modprobe.d/modprobe.conf` o `/etc/modprobe.d/sound.conf`. Ad esempio:

```
options snd-hda-intel model=MODEL

```

Ci sono anche altri modelli da impostare. Nella maggior parte dei casi Alsa lo farà in automatico. Se si vogliono vedere nel dettaglio le impostazioni della propria scheda audio si veda [Alsa Soundcard List](http://bugtrack.alsa-project.org/main/index.php/Matrix:Main), si individui il proprio modello, si clicchi su “*Details*” e si osservi la sezione "*Setting up modprobe...*". Inserire i valori trovati in `/etc/modprobe.d/modprobe.conf`. Ad esempio, per una scheda AC97 Intel:

```
# ALSA portion
alias char-major-116 snd
alias snd-card-0 snd-intel8x0
# module options should go here

# OSS/Free portion
alias char-major-14 soundcore
alias sound-slot-0 snd-card-0

# card #1
alias sound-service-0-0 snd-mixer-oss
alias sound-service-0-1 snd-seq-oss
alias sound-service-0-3 snd-pcm-oss
alias sound-service-0-8 snd-seq-oss
alias sound-service-0-12 snd-pcm-oss
```

### Audio in conflitto con altoparlante interno del PC

Se si è sicuri che tutto è attivo, che i propri driver sono installati correttamente, e che il volume è giusto, ma non si sente ancora nessun suono, allora si proceda all’aggiunta delle seguenti linee di codice in `/etc/modprobe.d/modprobe.conf`:

```
options snd-NAME-OF-MODULE ac97_quirk=0

```

Funziona con `via82xx`

```
options snd-NAME-OF-MODULE ac97_quirk=1

```

Funziona con `snd_intel8x0`

### Nessun Input dal Microfono

Assicurarsi, in alsamixer, che tutti i livelli del volume, nella sezione Registrazione, siano attivi e che la modalità CAPTURE del microfono sia abilitata (in alsamixer, selezionarla e premere spazio). Potrebbe anche essere necessario attivare e aumentare il volume di Line-in (Linea in ingresso) nella sezione Playblack (Riproduzione).

Per testare il microfono, eseguire questi comandi:

```
 arecord -d 5 test-mic.wav
 aplay test-mic.wav

```

Si consiglia di leggere la pagina *man* di *arecord*. Comunque, nel caso in cui non si sentisse alcun suono, il microfono potrebbe essere guasto oppure collegato nell’ingresso sbagliato.

Alcuni portatili Dell richiedono che il suffisso "-dmic" sia aggiunto al nome del modello all'interno di `/etc/modprobe.d/modprobe.conf`: `options snd-hda-intel model=dell-m6-dmic`

Alcuni programmi tentano di utilizzare OSS come software di input principale. Se sono stati abilitati in precedenza i [moduli del kernel](/index.php/Kernel_modules_(Italiano) "Kernel modules (Italiano)") `snd_pcm_oss`, `snd_mixer_oss` o `snd_seq_oss` (di default non sono caricati automaticamente), provare a scaricarli.

### Impostazione predefinita Microfono/Dispositivo di acquisizione

Alcune applicazioni (Pidgin, Adobe Flash) non forniscono una opzione per modificare il dispositivo di acquisizione. Ciò può costituire un problema se il microfono è su un dispositivo diverso (ad esempio una webcam USB o proprio un microfono) dalla scheda audio. Per cambiare solo il dispositivo di acquisizione, lasciando quello di riproduzione di default, si può modificare il file `~/.asoundrc` inserendo quanto segue:

```
pcm.usb
{
    type hw
    card U0x46d0x81d
}

pcm.!default
{
    type asym
    playback.pcm
    {
        type plug
        slave.pcm "dmix"
    }
    capture.pcm 
    {
        type plug
        slave.pcm "usb"
    }
}

```

Sostituire "U0x46d0x81d" con il nome della scheda del dispositivo di acquisizione in ALSA. È possibile utilizzare il comando `arecord -L` oppure `cat /proc/asound/cards` per visualizzare l’elenco di tutti i dispositivi di acquisizione rilevati da ALSA.

### Il microfono interno non funziona

Assicurarsi, in alsamixer, che tutti i livelli del volume, nella sezione Registrazione, siano attivi. Per ottenere una nuova impostazione volume, chiamata Capture, che registrerà il microfono interno, occorre aggiungere un’opzione al file `/etc/sound.conf` e ricaricare il modulo snd-*. Ad esempio, per snd-hda-intel, aggiungere:

```
 options snd-hda-intel enable_msi=1

```

Quindi, con i comandi riportati di seguito, ricaricare il modulo, attivare la nuova impostazione volume (Capture) e riprovare.

```
 rmmod snd-hda-intel
 modprobe snd-hda-intel

```

### Nessun suono con scheda integrata Intel

Ci potrebbe essere un conflitto tra due moduli caricati, chiamati `snd_intel8x0` e `snd_intel8x0m`. In questo caso, mettere in blacklist `snd_intel8x0m`:

 `/etc/modprobe.d/modprobe.conf`  `blacklist snd_intel8x0m` 

*Disabilitare* i canali "External Amplifier" in `alsamixer` o in `amixer` potrebbe essere d'aiuto. Consultare anche [il wiki ALSA](http://alsa.opensrc.org/index.php/Intel8x0#Dell_Inspiron_8600_.28and_probably_others.29).

Anche togliere il muto al canale Mix del mixer potrebbe risolvere il problema.

### Nessun suono dalle cuffie con scheda audio integrata Intel

Su di un portatile con **Intel Corporation 82801 I (ICH9 Family) HD Audio Controller** potrebbe essere necessario aggiungere questa riga a `modprobe` o al `sound.conf`:

```
options snd-hda-intel model=$model

```

Dove $model è uno dei modelli che seguono (non in ordine di merito ma di probabilità di funzionamento):

*   dell-vostro
*   olpc-xo-1_5
*   dell-m6

**Nota:** Potrebbe essere necessario inserire queste "opzioni" dopo eventuali "alias"

Si possono visualizzare tutti i modelli disponibili nella documentazione del kernel. Ad esempio [qui](http://git.kernel.org/cgit/linux/kernel/git/stable/linux-stable.git/tree/Documentation/sound/alsa/HD-Audio-Models.txt), ma accertarsi che si tratti della documentazione della versione del kernel in uso.

Un elenco di tutti i modelli è anche disponibile a [questo indirizzo](http://www.mjmwired.net/kernel/Documentation/sound/alsa/HD-Audio-Models.txt). Per conoscere il nome del proprio chip eseguire il seguente comando `$ grep Codec /proc/asound/card*/codec*`

**Nota:** Alcuni chip potrebbero essere stati rinominati, e non avere quindi un riscontro diretto con i nomi all'interno del file

Se seguendo questo metodo si dovessero riscontrare malfunzionamenti o anomalie, si prega di segnalare ad ALSA eventuali bug.

Inoltre, in caso di problemi con segnali acustici (pcspkr):

```
options snd-hda-intel model=$model enable=1 index=0

```

### Nessun suono quando è installata la scheda video con S/PDIF

Individuare i moduli disponibili ed il loro ordine:

 `$ cat /proc/asound/modules` 
```
0 snd_hda_intel
1 snd_ca0106

```

Disattivare il codec audio della scheda video in `/etc/modprobe.d/modprobe.conf`:

```
# /etc/modprobe.d/modprobe.conf
#
install snd_hda_intel /bin/false

```

Se entrambi i dispositivi utilizzano lo stesso modulo, dovrebbe essere possibile disattivare uno dei due tramite il BIOS.

### La qualità dell'audio è bassa

Se si riscontra una bassa qualità dell'audio, provare ad impostare il volume di PCM (in alsamixer) ad un livello di gain 0.

Se è stato caricato il driver snd-usb-audio, potresti provare ad abilitare `softvol` all'interno del file `/etc/asound.conf`. Configurazione d'esempio per il primo dispositivo audio:

```
pcm.!default {
   type plug
   slave.pcm "softvol"
 }
 pcm.dmixer {
      type dmix
      ipc_key 1024
      slave {
          pcm "hw:0"
          period_time 0
          period_size 4096
          buffer_size 131072
          rate 50000
      }
      bindings {
          0 0
          1 1
      }
 }
 pcm.dsnooper {
      type dsnoop
      ipc_key 1024
      slave {
          pcm "hw:0"
          channels 2
          period_time 0
          period_size 4096
          buffer_size 131072
          rate 50000
      }
      bindings {
          0 0
          1 1
      }
 }
 pcm.softvol {
      type softvol
      slave { pcm "dmixer" }
      control {
          name "Master"
          card 0
      }
 }
 ctl.!default {
   type hw
   card 0
 }
 ctl.softvol {
   type hw
   card 0
 }
 ctl.dmixer {
   type hw
   card 0
 }

```

### Rumori/Suoni all’avvio ed allo stop della riproduzione

Alcuni moduli (ad es. snd-ac97-codec e snd-hda-intel) posso spegnere la scheda audio quando questa non è utilizzata. Lo spegnimento può generare un suono. A volte ciò può avvenire anche quando si agisce sulla barra del volume, o quando si aprono o chiudono finestre (KDE4). Per evitare che ciò avvenga si può eseguire `modinfo snd-MY-MODULE`, e cercare un’opzione che regoli o disattivi questa funzione.

Ad esempio: per disabilitare il risparmio energetico utilizzando snd_hda_intel aggiungere in `/etc/modprobe.d/modprobe.conf` `options snd-hda-intel power_save=0` o `options snd-hda-intel power_save=0 power_save_controller=N` 

È anche possibile provare prima al volo le configurazioni dando, ad esempio, `modprobe snd_hda_intel power_save=0`

Potrebbe anche rivelarsi necessario togliere il muto dal canale alsa 'Line'. Qualsiasi valore, purchè non 0 o troppo alto, andrà bene.

Ad esempio: su una scheda integrata VIA VT1708S (che utilizza il modulo snd-hda-intel) questi disturbi erano presenti anche dopo aver impostato il parametro 'power_save' a 0\. Im postandolo ad 1 e togliendo il muto al canale 'Line', il problema è stato risolto.

Fonte: [http://www.kernel.org/doc/Documentation/sound/alsa/powersave.txt](http://www.kernel.org/doc/Documentation/sound/alsa/powersave.txt)

Se si utilizza un portatile, pm-utils riporterà il valore di `power_save` a 1 quando si passa all'alimentazione da batteria, anche se è stato disabilitato il risparmio energetico in `/etc/modprobe.d`. Evitare questo comportamento di pm-utils disabilitando lo script che lo determina (consultare [Disabling a hook](https://wiki.archlinux.org/index.php/Pm-utils#Disabling_a_hook) per ulteriori informazioni):

`# touch /etc/pm/power.d/intel-audio-powersave`

### L'uscita S/PDIF non funziona

Se l'uscita digitale ottica/coassiale della scheda madre/scheda audio non funziona o ha smesso di funzionare, e in alsamixer i relativi canali sono già attivi, provare ad eseguire:

```
iecset audio on

```

da utente root.

È inoltre possibile inserire questo comando in `rc.local` in quanto a volte può smettere di funzionare dopo un riavvio.

### L'uscita HDMI non funziona

La procedura esposta di seguito consente di testare il funzionamento dell'uscita audio HDMI. Prima di procede, accertarsi di aver abilitato e levato il muto all'output corrispondente tramite `alsamixer`.

**Note:** Se si utilizza una scheda video ATI ed un kernel linux >=3.0, un modulo del kernel necessario risulterà disabilitato. Consultare [ATI#HDMI_Audio](/index.php/ATI#HDMI_Audio "ATI").

Collegare il pc al monitor tramite cavo HDMI ed abilitare il display con un tool come `xrandr` o `arandr`. Ad esempio

```
$ xrandr # list outputs
$ xrandr --output DVI-D_1 --mode 1024x768 --right-of PANEL # enable output
```

Interrogare i dispositivi di riproduzione:

 `$ aplay -l` 
```
**** List of PLAYBACK Hardware Devices ****
card 0: NVidia [HDA NVidia], device 0: ALC1200 Analog [ALC1200 Analog]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 0: NVidia [HDA NVidia], device 1: ALC1200 Digital [ALC1200 Digital]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 0: NVidia [HDA NVidia], device 3: NVIDIA HDMI [NVIDIA HDMI]
  Subdevices: 0/1
  Subdevice #0: subdevice #0

```

Ora che abbiamo le informazioni per la periferica HDMI, si può fare una prova. Nell'esempio che segue, 0 è il numero della scheda e 3 è il numero del dispositivo.

 `$ aplay -D plughw:0,3 /usr/share/sounds/alsa/Front_Center.wav` 

Se aplay non restituisce alcun errore, ma ancora non si sente alcun suono, "riavviare" il ricevitore, il monitor o la tv. Poichè l'interfaccia HDMI esegue un rigido controllo sulla connessione, potrebbe aver recepito che prima non c'era alcun flusso audio, ed ha quindi disabilitato la decodifica audio.

Se la verifica ha esito positivo, modificare/creare `~/.asoundrc` per impostare HDMI come dispositivo audio predefinito e riavviare; ora l'audio dovrebbe funzionare.

 `~/.asoundrc` 
```
pcm.!default {
  type hw
  card 0
  device 3
}

```

Se la configurazione precedente non dovesse funzionare, provare con:

 `~/.asoundrc` 
```
defaults.pcm.card 0
defaults.pcm.device 3
defaults.ctl.card 0

```

### HP TX2500

Aggiungere queste due righe in `/etc/modprobe.d/modprobe.conf`:

```
options snd-cmipci mpu_port=0x330 fm_port=0x388
options snd-hda-intel index=0 model=toshiba position_fix=1

```

```
options snd-hda-intel model=hp (works for tx2000cto)

```

### Salto di suono durante la riproduzione MP3

Se si hanno salti di suono durante la riproduzione di file MP3 e se al computer sono collegati di più di 2 altoparlanti (o più di due), eseguire `alsamixer` e disabilitare i canali degli altoparlanti che **NON** si posseggono (ad esempio, disabilitare il canale dell’altoparlante centrale se non si dispone di un altoparlante centrale).

### Cuffia USB e schede audio esterne USB

Se si utilizza una cuffia USB con ALSA, si può provare ad usare [asoundconf](https://aur.archlinux.org/packages/asoundconf/) (attualmente disponibile solo da [AUR](/index.php/AUR "AUR")) per impostare l'auricolare come uscita audio principale. Prima di proseguire, assicurarsi di avere abilitato il modulo usb audio (`modprobe snd-usb-audio`).

```
#modprobe snd-usb-audio

```

Se si vuole, si può aggiungere quanto segue al file `/etc/rc.conf`

```
# asoundconf is-active
# asoundconf list
# asoundconf set-default-card <chosen soundcard>

```

#### Suono gracchiante su dispositivi USB

Se si riscontra audio gracchiante su dispositivi USB, si può provare ad impostare il modulo snd-usb-audio per minime latenze. Aggiungere questo codice a `/etc/modprobe.d/modprobe.conf` :

```
options snd-usb-audio nrpacks=1

```

Fonte: [http://alsa.opensrc.org/Usb-audio#Tuning_USB_devices_for_minimal_latencies](http://alsa.opensrc.org/Usb-audio#Tuning_USB_devices_for_minimal_latencies)

#### Inserimento a caldo di una scheda audio USB

Per fare in modo che una scheda audio USB diventi al suo inserimento automaticamente la scheda principale, si può utilizzare la seguente regola di udev (ad esempio aggiungendo queste righe al file `/etc/udev/rules.d/00-local.rules`):

```
KERNEL=="pcmC[D0-9cp]*", ACTION=="add", PROGRAM="/bin/sh -c 'K=%k; K=$${K#pcmC}; K=$${K%%D*}; echo defaults.ctl.card $$K > /etc/asound.conf; echo defaults.pcm.card $$K >>/etc/asound.conf'"
KERNEL=="pcmC[D0-9cp]*", ACTION=="remove", PROGRAM="/bin/sh -c 'echo defaults.ctl.card 0 > /etc/asound.conf; echo defaults.pcm.card 0 >>/etc/asound.conf'"
```

### Errore 'Unknown hardware' dopo aggiornamento Kernel

I seguenti messaggi possono essere visualizzati durante l'avvio di ALSA, dopo l'aggiornamento del kernel:

```
Unknown hardware "foo" "bar" ...
Hardware is initialized using a guess method
/usr/bin/alsactl: set_control:nnnn:failed to obtain info for control #mm (No such file or directory)

```

oppure

```
Found hardware: "HDA-Intel" "VIA VT1705" "HDA:11064397,18490397,00100000" "0x1849" "0x0397"
Hardware is initialized using a generic method
/usr/bin/alsactl: set_control:1328: failed to obtain info for control #1 (No such file or directory)
/usr/bin/alsactl: set_control:1328: failed to obtain info for control #2 (No such file or directory)
/usr/bin/alsactl: set_control:1328: failed to obtain info for control #25 (No such file or directory)
/usr/bin/alsactl: set_control:1328: failed to obtain info for control #26 (No such file or directory)

```

E’ sufficiente memorizzare nuovamente le impostazioni del mixer di ALSA (da root):

```
# alsactl -f /var/lib/alsa/asound.state store

```

Potrebbe essere necessario configurare nuovamente ALSA tramite `alsamixer`

### HDA Analyzer

Se la mappatura dei pin (spinotti) audio non corrisponde ma ALSA funzione regolarmente, si può provare HDA Analyzer – un’interfaccia grafica (GUI) in pyGTK2 per il controllo dell’audio HD, disponibile nel [wiki di ALSA](http://www.alsa-project.org/main/index.php/HDA_Analyzer). Provare anche ad utilizzare la sezione Widget Control per gestire i PIN, impostando IN per il microfono e OUT per le cuffie. Potrebbe essere una buona idea fare riferimento ai valori di default (Config Defaults).

**Note:**

NOTA: Lo script è incompatibile con python3 (che è attualmente fornito con ArchLinux) ma si può comunque provare ad utilizzarlo. La soluzione è: aprire “run.py”, trovare tutte le ricorrenze "python" (2 ricorrenze - una nella prima riga, e la seconda nell'ultima riga) e sostituirle con "python2".

NOTA 2: Lo script richiede i privilegi di root, ma non funziona attraverso su/sudo. Eseguirlo quindi tramite `kdesu` o `gksu`.

### ALSA con SDL

Se non si riesce ad ottenere alcun suono tramite SDL, ma ALSA non può essere selezionato nella configurazione dell'applicazione, provare ad impostare la variabile d'ambiente SDL_AUDIODRIVER su "alsa"

 `export SDL_AUDIODRIVER=alsa` 

### Workaround in caso di volume basso

Se ci si dovesse ritrovare con un audio molto basso nonostante la massimizzazione del volume delle casse/cuffie, si può fare un tentativo col plugin softvol. Aggiungere il seguente codice al file `/etc/asound.conf`.

```
pcm.!default {
      type plug
      slave.pcm "softvol"
  }

pcm.softvol {
    type softvol
    slave {
        pcm "dmix"
    }
    control {
        name "Pre-Amp"
        card 0
    }
    min_dB -5.0
    max_dB 20.0
    resolution 6
}

```

**Note:** Potrebbe essere necessario riavviare l'intero sistema, in quanto il semplice riavvio del demone alsa potrebbe non caricare la nuova configurazione. Se ciò non dovesse avvenire anche dopo un riavvio del sistema, provare a modificare `plug` in `hw` nel codice precedente.

Una volta che le modifiche saranno state caricate, si noterà una nuova sezione `Pre-Amp` in alsamixer. È possibile regolare i volumi da lì.

**Note:** L'impostazione di valori eccessivamente alti in `Pre-Amp` potrebbe causare una distorsione del suono, accertarsi quindi di regolarli con cura.

### "Schiocco" al resume dopo una sospensione

Potrebbe capitare di udire un suono simile ad uno schiocco quando si effettua il resume di un sistema dalla sospensione. Questò può essere evitato modificando il file `/etc/pm/sleep.d/90alsa` e rimuovendo la riga `aplay -d 1 /dev/zero`

## Configurazioni d'esempio

Consultare [Advanced Linux Sound Architecture/Example Configurations (Italiano)](/index.php/Advanced_Linux_Sound_Architecture/Example_Configurations_(Italiano) "Advanced Linux Sound Architecture/Example Configurations (Italiano)")

## Link esterni

Altre informazioni possono essere trovate ai seguenti link:

*   [Advanced ALSA module configuration](http://www.mjmwired.net/kernel/Documentation/sound/alsa/ALSA-Configuration.txt)
*   [Unofficial ALSA Wiki](http://alsa.opensrc.org/Main_Page)
*   [HOWTO: Compile driver from svn](https://bbs.archlinux.org/viewtopic.php?id=36815)