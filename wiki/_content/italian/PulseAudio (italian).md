Articoli correlati

*   [PulseAudio/Examples (Italiano)](/index.php/PulseAudio/Examples_(Italiano) "PulseAudio/Examples (Italiano)")
*   [PulseAudio/Troubleshooting (Italiano)](/index.php/PulseAudio/Troubleshooting_(Italiano) "PulseAudio/Troubleshooting (Italiano)")

[PulseAudio](https://en.wikipedia.org/wiki/PulseAudio e [KDE](/index.php/KDE_(Italiano) "KDE (Italiano)") e funge da proxy per le applicazioni che richiedano l'utilizzo dell'audio utilizzando componenti come [ALSA](/index.php/ALSA_(Italiano) "ALSA (Italiano)") od [OSS](/index.php/OSS_(Italiano) "OSS (Italiano)"). Dal momento che Alsa viene incluso in Arch Linux di default, i casi di utilizzo più comuni proposti di seguito coprono l'utilizzo di PulseAudio con Alsa.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
*   [3 Esecuzione](#Esecuzione)
    *   [3.1 Avvio automatico in ambienti desktop non supportati](#Avvio_automatico_in_ambienti_desktop_non_supportati)
*   [4 Configurazione del backend](#Configurazione_del_backend)
    *   [4.1 ALSA](#ALSA)
    *   [4.2 ALSA / dmix senza che PulseAudio prenda possesso della scheda audio](#ALSA_/_dmix_senza_che_PulseAudio_prenda_possesso_della_scheda_audio)
    *   [4.3 OSS](#OSS)
        *   [4.3.1 ossp](#ossp)
        *   [4.3.2 padsp wrapper](#padsp_wrapper)
    *   [4.4 Gstreamer](#Gstreamer)
    *   [4.5 OpenAL](#OpenAL)
    *   [4.6 libao](#libao)
*   [5 Equalizzatore](#Equalizzatore)
    *   [5.1 Installazione componenti necessari](#Installazione_componenti_necessari)
    *   [5.2 Caricamento dei moduli equalizer-sink e dbus-protocol](#Caricamento_dei_moduli_equalizer-sink_e_dbus-protocol)
    *   [5.3 Installazione ed esecuzione del frontend grafico](#Installazione_ed_esecuzione_del_frontend_grafico)
    *   [5.4 Caricamento automatico dei moduli equalizer-sink e dbus-protocol al boot](#Caricamento_automatico_dei_moduli_equalizer-sink_e_dbus-protocol_al_boot)
*   [6 Applicazioni](#Applicazioni)
    *   [6.1 QEMU](#QEMU)
    *   [6.2 AlsaMixer.app](#AlsaMixer.app)
    *   [6.3 XMMS2](#XMMS2)
    *   [6.4 KDE Plasma Workspaces e Qt4](#KDE_Plasma_Workspaces_e_Qt4)
    *   [6.5 Audacious](#Audacious)
    *   [6.6 Java/OpenJDK 6](#Java/OpenJDK_6)
    *   [6.7 Music Player Daemon (MPD)](#Music_Player_Daemon_(MPD))
    *   [6.8 MPlayer](#MPlayer)
    *   [6.9 guvcview](#guvcview)
*   [7 Risoluzione dei problemi](#Risoluzione_dei_problemi)
*   [8 Link esterni](#Link_esterni)

## Installazione

*   Pacchetto richiesto: [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio)
*   GUI GTK opzionali: [paprefs](https://www.archlinux.org/packages/?name=paprefs) e [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol)
*   Controllo volume opzionale via tastiera: [pulseaudio-ctl](https://aur.archlinux.org/packages/pulseaudio-ctl/)
*   Mixer da console (CLI) opzionali: [ponymix-git](https://aur.archlinux.org/packages/ponymix-git/) e [pamixer-git](https://aur.archlinux.org/packages/pamixer-git/)
*   Controllo volume via web opzionale:
*   Icona nella tray di sistema opzionale: [PaWebControl](https://github.com/Siot/PaWebControl)[pasystray-git](https://aur.archlinux.org/packages/pasystray-git/)
*   Applet di Plasma per KDE: [kmix](https://www.archlinux.org/packages/?name=kmix) e [kdeplasma-applets-veromix](https://aur.archlinux.org/packages/kdeplasma-applets-veromix/) (Se KMix/Veromix non riescono a connettersi a PulseAudio all'avvio, potrebbe essere necessario modificare `/etc/pulse/client.conf` e modificare `autospawn = yes` in `autospawn = no`.)

## Configurazione

Si sarà notato che PulseAudio supporta vari moduli per estendere le proprie funzionalità. È possibile reperirne un elenco completo [qui](http://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/Modules/). Per abilitarli sarà sufficiente aggiungere `load-module <module-name-from-list>` a `/etc/pulse/default.pa`.

## Esecuzione

**Attenzione:** Se si dispone di copie locali dei files di configurazione (`client.conf`, `daemon.conf` o `default.pa` in `~/.config/pulse`, sarà necessario allinearle ai cambiamenti dei files situati in `/etc/pulse`, altrimenti PulseAudio potrebbe non avviarsi a causa di errori di configurazione.

**Nota:**

La maggior parte degli ambienti grafici avviano PulseAudio automaticamente.

Nel caso in cui PulseAudio non venisse automaticamente avviato all'avvio di X, può essere avviato con:

```
$ pulseaudio --start

```

PulseAudio può essere interrotto con:

```
$ pulseaudio --kill

```

### Avvio automatico in ambienti desktop non supportati

**Nota:** Come già detto in precedenza, PulseAudio viene molto probabilmente già lanciato automaticamente tramite `/etc/X11/xinit/xinitrc.d/pulseaudio` o i file in `/etc/xdg/autostart`, se si è installato un DE.

Si controlli se PulseAudio è in esecuzione:

 `$ pgrep -af pulseaudio` 
```
369 /usr/bin/pulseaudio

```

Se PulseAudio non è avviato e si sta utilizzando X, il comando che segue ne consentirà l'avvio manuale, assieme a tutti i plugin richiesti:

```
$ start-pulseaudio-x11

```

Se non si sta utilizzando GNOME, KDE o Xfce e il proprio [~/.xinitrc](/index.php/Xinitrc "Xinitrc") non effettua il source degli script in `/etc/X11/xinit/xinitrc.d`, è possibile avviare PulseAudio al boot con:

 `~/.xinitrc` 
```
/usr/bin/start-pulseaudio-x11

```

## Configurazione del backend

### ALSA

Si installi [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa) dai [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)"). Il pacchetto contiene il file `/etc/asound.conf` per impostare ALSA per l'utilizzo con PulseAudio.

Si installino inoltre [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) e [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins) se si è su un sistema a 64 bit e si utilizzano applicazioni [multilib](/index.php/Multilib "Multilib") a 32 bit come Wine, Skype e Steam.

Per impedire alle applicazioni di usare l'emulazione OSS di ALSA bypassando così Pulseaudio (non consentendo così ad altri programmi di riprodurre suoni), assicurarsi che il modulo `snd_pcm_oss` non venga caricato al boot. Se è caricato (controllare con `lsmod | grep oss`), è possibile rimuoverlo con:

```
# rmmod snd_pcm_oss

```

### ALSA / dmix senza che PulseAudio prenda possesso della scheda audio

**Nota:** Questa sezione descrive una configurazione alternativa, generalmente **NON** consigliabile.

Si potrebbe voler utilizzare ALSA direttamente nella maggior parte delle applicazioni e al tempo stesso utilizzarne delle altre che richiedono PulseAudio. I passi seguenti consentiranno a PulseAudio di utilizzare dmix senza che lo stesso debba prendere il controllo della scheda audio.

*   Si rimuova il pacchetto [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa), che fornisce un layer di compatibilità tra le applicazioni ALSA e PulseAudio. Una volta fatto, tali applicazioni utilizzeranno ALSA direttamente senza passare per PulseAudio.

*   Si modifichi `/etc/pulse/default.pa`.

	Si identifichino e decommentino le linee che effettuano il caricamento dei drivers per i backend e si aggiunga loro il parametro **device** come mostrato sotto. Si commentino poi le linee che caricano i moduli per l'autorilevamento.

```
load-module module-alsa-sink **device=dmix**
load-module module-alsa-source **device=dsnoop**
# load-module module-udev-detect
# load-module module-detect

```

*   *Opzionale:* Se si utilizza [kmix](https://www.archlinux.org/packages/?name=kmix), si potrebbe voler controllare il volume di ALSA invece che quello di PulseAudio:

```
$ echo export KMIX_PULSEAUDIO_DISABLE=1 > ~/.kde4/env/kmix_disable_pulse.sh
$ chmod +x ~/.kde4/env/kmix_disable_pulse.sh

```

*   Si riavvii il pc e si provi quindi ad eseguire applicazioni che utilizzano ALSA e PulseAudio contemporaneamente: il suono dovrebbe venir riprodotto simultaneamente da entrambe.

	Si utilizzi quindi [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) per regolare il volume di PulseAudio secondo le proprie necessità.

### OSS

Ci sono diversi modi per fare in modo che programmi compatibili solo con OSS passino l'output a PulseAudio:

#### [ossp](https://www.archlinux.org/packages/?name=ossp)

Si installi il pacchetto [ossp](https://www.archlinux.org/packages/?name=ossp) e si avvii il servizio `osspd.service`.

#### padsp wrapper

I programmi che utilizzano OSS, possono funzionare con Pulseaudio se avviati con padsp (incluso in PulseAudio):

```
$ padsp OSSprogram

```

Un paio di esempi:

```
$ padsp aumix
$ padsp sox foo.wav -t ossdsp /dev/dsp

```

E' anche possibile creare un wrapper, in questo modo:

 `/usr/local/bin/nome_programma` 
```
#!/bin/sh
exec padsp /usr/bin/OSSprogram "$@"

```

Assicurarsi che `/usr/local/bin` abbia la precedenza su `/usr/bin` nel vostro `PATH`.

### Gstreamer

Si installi il pacchetto [gst-plugins-good](https://www.archlinux.org/packages/?name=gst-plugins-good) oppure [gstreamer0.10-good-plugins](https://aur.archlinux.org/packages/gstreamer0.10-good-plugins/) se il programma in questione utilizza un'implementazione vecchia di [GStreamer](/index.php/GStreamer "GStreamer").

### OpenAL

OpenAL Soft dovrebbe utilizzare PulseAudio di default, ma in caso di necessità può essere manualmente configurato tramite

 `/etc/openal/alsoft.conf`  `drivers=pulse,alsa` 

### libao

Modificare il file di configurazione di libao:

 `/etc/libao.conf`  `default_driver=pulse` 

Assicurarsi di rimuovere l'opzione `dev=default` del driver alsa o specificare il nome di un sink di PulseAudio o il relativo numero.

**Nota:** È possibile mantenere i valori di default di libao e lasciargli usare il driver `alsa` per l'output se si installa il pacchetto [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa), poichè in quel caso il dispositivo ALSA di default sarebbe PulseAudio.

## Equalizzatore

Le nuove versioni di PulseAudio dispongono di un equalizzatore a 10 bande integrato. Per utilizzarlo, si proceda come segue:

#### Installazione componenti necessari

```
# pacman -S pulseaudio-equalizer

```

#### Caricamento dei moduli equalizer-sink e dbus-protocol

```
$ pactl load-module module-equalizer-sink
$ pactl load-module module-dbus-protocol

```

#### Installazione ed esecuzione del frontend grafico

Si installi il pacchetto [python2-pyqt4](https://aur.archlinux.org/packages/python2-pyqt4/) e si esegua:

```
$ qpaeq

```

**Nota:** Se `qpaeq` non ha effetto, si installi [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) e si modifichi l'opzione "ALSA Playback on" in "FFT based equalizer on" mentre il player è in riproduzione.

#### Caricamento automatico dei moduli equalizer-sink e dbus-protocol al boot

Si modifichi il file `/etc/pulse/default.pa`, aggiungendo le righe seguenti:

```
### Load the intergrated pulseaudio equalizer module
load-module module-equalizer-sink
load-module module-dbus-protocol

```

## Applicazioni

### QEMU

Per verificare se QEMU supporta PulseAudio, si esegua:

```
$ qemu-system-x86_64 -audio-help | grep 'Name: pa'

```

QEMU può utilizzare le variabili d'ambiente per la configurazione dell'audio:

```
export QEMU_AUDIO_DRV=pa
export QEMU_PA_SINK=alsa_output.pci-0000_04_01.0.analog-stereo.monitor
export QEMU_PA_SOURCE=input
```

Per altre opzioni di configurazione di PulseAudio, si esegua:

```
$ qemu-system-x86_64 -audio-help | grep '_PA_'

```

Per una lista dei driver emulati supportati si esegua:

```
$ qemu-system-x86_64 -soundhw help

```

Ad esempio, per utilizzare il driver `ac97` per il sistema guest, si passi il parametro `-soundhw ac97` a QEMU.

**Nota:**

*   Nel comando `qemu-system-*XXX*`, *XXX* specifica l'architettura del sistema guest. Per visualizzare un elenco di quelle disponibili, eseguire: `ls /usr/bin/qemu-system-* -1`
*   I driver video emulati potrebbero causare problemi di qualità audio nella macchinav irtuale. Si provi ogni driver per identificare quello più adatto. È possibile visualizzare un elenco dei driver disponibili con: `qemu-system-x86_64 -h | grep vga`.

### AlsaMixer.app

Per fare in modo che la dockapp [AlsaMixer.app](https://aur.archlinux.org/packages/AlsaMixer.app/) per [windowmaker](https://aur.archlinux.org/packages/windowmaker/) utilizzi PulseAudio, utilizzare:

```
$ AlsaMixer.app --device pulse

```

Di seguito due esempi, il primo per ALSA e il secondo per PulseAudio. È possibile eseguire istanze multiple dell'applicazione. Si utilizzi l'opzione `-w` per scegliere quale dei due pulsanti di controllo assegnare alla rotella del mouse:

```
# AlsaMixer.app -3 Mic -1 Master -2 PCM --card 0 -w 1
# AlsaMixer.app --device pulse -1 Capture -2 Master -w 2

```

**Nota:** L'applicazione può utilizzare solamente gli output sinks impostati come default.

### XMMS2

Per utilizzare PulseAudio come output:

```
$ nyxmms2 server config output.plugin pulse

```

Per utilizzare ALSA:

```
$ nyxmms2 server config output.plugin alsa

```

Per utilizzare un sink di output differente:

```
$ nyxmms2 server config pulse.sink alsa_output.pci-0000_04_01.0.analog-stereo.monitor

```

Consultare inoltre la guida ufficiale: [[1]](https://xmms2.org/wiki/Using_the_application).

### KDE Plasma Workspaces e Qt4

PulseAudio viene utilizzato automaticamente dalle applicazioni KDE/Qt4 e supportato di default nel mixer di KDE. Per ulteriori informazioni si veda la [pagina](http://www.pulseaudio.org/wiki/KDE) relativa a KDE sul wiki di PulseAudio. Un consiglio utile dal link di cui sopra è quello di aggiungere `load-module module-device-manager` a `/etc/pulse/default.pa`.

Se si sta utilizzando il backend phonon-gstreamer per Phonon, sarà necessario configurare anche GStreamer come descritto in [#Gstreamer](#Gstreamer).

### Audacious

[Audacious](/index.php/Audacious "Audacious") supporta Pulseaudio nativamente. Per usarlo, è necessario avviare Audacious e recarsi in: Audacious Preferences -> Audio -> Current Output plugin, quindi scegliere 'Pulseaudio Output Plugin'

### Java/OpenJDK 6

Si crei un wrapper per l'eseguibile java usando `padsp` come si è visto alla pagina [Audio Java con Pulseaudio](/index.php/Java_(Italiano)#Audio_Java_con_Pulseaudio "Java (Italiano)").

### Music Player Daemon (MPD)

È necessario [configurare](http://mpd.wikia.com/wiki/PulseAudio) mpd affinché usi Pulseaudio. Si veda anche [MPD/Tips and Tricks#MPD and PulseAudio](/index.php/MPD/Tips_and_Tricks#MPD_and_PulseAudio "MPD/Tips and Tricks").

Si noti comunque che quanto sopra potrebbe causare un bug che impedisce a PulseAudio di togliere il muto agli altoparlanti quando vengono rimosse cuffie o altri dispositivi audio.

### MPlayer

MPlayer supporta l'output attraverso Pulseaudio specificando l'opzione `"-ao pulse"`. È inoltre possibile configurarlo affinché venga usato in modo predefinito modificando `~/.mplayer/config` per l'utente corrente o `/etc/mplayer/mplayer.conf` per applicare le modifiche a tutto il sistema.

```
/etc/mplayer/mplayer.conf

```
 `ao=pulse` 

### guvcview

È possibile che l'input audio venga sospeso quando si utilizza l'input PulseAudio da una [Webcam](/index.php/Webcam "Webcam"), causando cosi la mancata registrazione dell'audio.

Si verifichi eseguendo:

```
$ pactl list sources

```

Se la sorgente audio è sospesa, si modifichi `/etc/pulse/default.pa` cambiando:

```
load-module module-suspend-on-idle

```

in:

```
#load-module module-suspend-on-idle

```

Così facendo, il riavvio di PulseAudio o del sistema metterà in idle la sorgente di input invece di sospenderla. [guvcview](https://www.archlinux.org/packages/?name=guvcview) potrà quindi registrare l'audio dal dispositivo in maniera corretta.

## Risoluzione dei problemi

Si veda [PulseAudio/Troubleshooting (Italiano)](/index.php/PulseAudio/Troubleshooting_(Italiano) "PulseAudio/Troubleshooting (Italiano)").

## Link esterni

*   [http://www.alsa-project.org/main/index.php/Asoundrc](http://www.alsa-project.org/main/index.php/Asoundrc) - Pagina del wiki di ALSA relativa ad .asoundrc
*   [http://www.pulseaudio.org/](http://www.pulseaudio.org/) - Sito ufficiale di Pulseaudio
*   [http://www.pulseaudio.org/wiki/FAQ](http://www.pulseaudio.org/wiki/FAQ) - Faq per Pulseaudio.