Si veda [PulseAudio](/index.php/PulseAudio_(Italiano) "PulseAudio (Italiano)") per l'articolo principale.

## Contents

*   [1 Niente suono dopo l'installazione](#Niente_suono_dopo_l.27installazione)
    *   [1.1 Dispositivo audio muto](#Dispositivo_audio_muto)
    *   [1.2 Modalità Auto-Mute](#Modalit.C3.A0_Auto-Mute)
    *   [1.3 Files di configurazione non corretti](#Files_di_configurazione_non_corretti)
    *   [1.4 Contenuti Flash](#Contenuti_Flash)
    *   [1.5 Nessuna scheda audio rilevata](#Nessuna_scheda_audio_rilevata)
    *   [1.6 Viene visualizzato solo il dispositivo "dummy output", oppure le schede audio appena connesse non vengono rilevate](#Viene_visualizzato_solo_il_dispositivo_.22dummy_output.22.2C_oppure_le_schede_audio_appena_connesse_non_vengono_rilevate)
    *   [1.7 Impossibilie scegliere output 5.1/7.1](#Impossibilie_scegliere_output_5.1.2F7.1)
    *   [1.8 KDE4](#KDE4)
    *   [1.9 Errore "Failed to create sink input: sink is suspended"](#Errore_.22Failed_to_create_sink_input:_sink_is_suspended.22)
*   [2 Avviare una applicazione interrompe il suono di un'altra](#Avviare_una_applicazione_interrompe_il_suono_di_un.27altra)
*   [3 Nessun output audio HDMI se si spegne il monitor per un certo periodo di tempo](#Nessun_output_audio_HDMI_se_si_spegne_il_monitor_per_un_certo_periodo_di_tempo)
*   [4 Abilitare la soppressione dei rumori/dell'eco](#Abilitare_la_soppressione_dei_rumori.2Fdell.27eco)
*   [5 Non è possibile aggiornare la configurazione della scheda audio da pavucontrol](#Non_.C3.A8_possibile_aggiornare_la_configurazione_della_scheda_audio_da_pavucontrol)
*   [6 Output simultaneo verso più schede audio / dispositivi](#Output_simultaneo_verso_pi.C3.B9_schede_audio_.2F_dispositivi)
*   [7 L'output simultaneo verso più schede audio / dispositivi non funziona](#L.27output_simultaneo_verso_pi.C3.B9_schede_audio_.2F_dispositivi_non_funziona)
*   [8 Disabilitare il supporto ai dispositivi Bluetooth](#Disabilitare_il_supporto_ai_dispositivi_Bluetooth)
*   [9 Problemi di riproduzione con cuffie Bluetooth](#Problemi_di_riproduzione_con_cuffie_Bluetooth)
*   [10 Switch automatico agli headset Bluetooth o USB](#Switch_automatico_agli_headset_Bluetooth_o_USB)
*   [11 Pulse sovrascrive le impostazioni di Alsa](#Pulse_sovrascrive_le_impostazioni_di_Alsa)
*   [12 Impedire il riavvio di PulseAudio una volta ucciso](#Impedire_il_riavvio_di_PulseAudio_una_volta_ucciso)
*   [13 Avvio del demone fallito](#Avvio_del_demone_fallito)
    *   [13.1 Possibili output delle utility per il controllo degli errori di PulseAudio](#Possibili_output_delle_utility_per_il_controllo_degli_errori_di_PulseAudio)
*   [14 Artefatti sonori, audio intermittente o gracchiante](#Artefatti_sonori.2C_audio_intermittente_o_gracchiante)
*   [15 Impostare il numero di frammenti e la dimensione del buffer in PulseAudio](#Impostare_il_numero_di_frammenti_e_la_dimensione_del_buffer_in_PulseAudio)
    *   [15.1 Identificare i parametri della scheda audio in uso (1/4)](#Identificare_i_parametri_della_scheda_audio_in_uso_.281.2F4.29)
    *   [15.2 Si calcolino la dimensione ed il numero di frammenti in millisecondi (2/4)](#Si_calcolino_la_dimensione_ed_il_numero_di_frammenti_in_millisecondi_.282.2F4.29)
    *   [15.3 Modificare il file di configurazione di PulseAudio (3/4)](#Modificare_il_file_di_configurazione_di_PulseAudio_.283.2F4.29)
    *   [15.4 Riavviare il demone PulseAudio (4/4)](#Riavviare_il_demone_PulseAudio_.284.2F4.29)
*   [16 Il suono arriva in ritardo](#Il_suono_arriva_in_ritardo)
*   [17 Suono intermittente e distorto](#Suono_intermittente_e_distorto)
*   [18 I controlli del volume non funzionano correttamente](#I_controlli_del_volume_non_funzionano_correttamente)
*   [19 Il volume delle singole applicazioni varia quando si modifica il livello del volume generale](#Il_volume_delle_singole_applicazioni_varia_quando_si_modifica_il_livello_del_volume_generale)
*   [20 Il livello del volume si alza ogni volta che una nuova applicazione viene avviata](#Il_livello_del_volume_si_alza_ogni_volta_che_una_nuova_applicazione_viene_avviata)
*   [21 Microfono non funzionante su ThinkPad T400/T500/T420](#Microfono_non_funzionante_su_ThinkPad_T400.2FT500.2FT420)
*   [22 Microfono non funzionante su Acer Aspire One](#Microfono_non_funzionante_su_Acer_Aspire_One)
*   [23 Output monocanale su M-Audio Audiophile 2496](#Output_monocanale_su_M-Audio_Audiophile_2496)
*   [24 Rumore statico durante la registrazione da microfono](#Rumore_statico_durante_la_registrazione_da_microfono)
    *   [24.1 Determinare le schede audio installate nel sistema (1/5)](#Determinare_le_schede_audio_installate_nel_sistema_.281.2F5.29)
    *   [24.2 Determinare la frequenza di campionamento della scheda audio (2/5)](#Determinare_la_frequenza_di_campionamento_della_scheda_audio_.282.2F5.29)
    *   [24.3 Impostare la frequenza di campionamento nella configurazione di Pulseaudio (3/5)](#Impostare_la_frequenza_di_campionamento_nella_configurazione_di_Pulseaudio_.283.2F5.29)
    *   [24.4 Riavviare Pulseaudio per applicare i cambiamenti(4/5)](#Riavviare_Pulseaudio_per_applicare_i_cambiamenti.284.2F5.29)
    *   [24.5 Effettuare una prova registrando e poi ascoltando la registrazione (5/5)](#Effettuare_una_prova_registrando_e_poi_ascoltando_la_registrazione_.285.2F5.29)
*   [25 Il mio dispositivo bluetooth viene rilevato ma non riproduce alcun suono](#Il_mio_dispositivo_bluetooth_viene_rilevato_ma_non_riproduce_alcun_suono)
*   [26 Il subwoofer smette di funzionare alla fine della riproduzione di una canzone](#Il_subwoofer_smette_di_funzionare_alla_fine_della_riproduzione_di_una_canzone)
*   [27 Pulseaudio utilizza il microfono sbagliato](#Pulseaudio_utilizza_il_microfono_sbagliato)
*   [28 Suono intermittente quando si usa il profilo Analog Surround Sound](#Suono_intermittente_quando_si_usa_il_profilo_Analog_Surround_Sound)
*   [29 Impossibilità di scegliere configurazioni surround diverse da "Surround 4.0"](#Impossibilit.C3.A0_di_scegliere_configurazioni_surround_diverse_da_.22Surround_4.0.22)
*   [30 Assenza di suono sotto un certo livello di volume](#Assenza_di_suono_sotto_un_certo_livello_di_volume)
*   [31 Basso livello volume del microfono integrato](#Basso_livello_volume_del_microfono_integrato)
*   [32 I client alterano il controllo volume generale (ovvero volume al massimo dopo aver lanciato un'applicazione)](#I_client_alterano_il_controllo_volume_generale_.28ovvero_volume_al_massimo_dopo_aver_lanciato_un.27applicazione.29)
*   [33 Scheduling realtime](#Scheduling_realtime)
*   [34 Nessun suono dopo il resume dalla sospensione](#Nessun_suono_dopo_il_resume_dalla_sospensione)
*   [35 Canali ALSA muti a causa di un collegamento/scollegamento improprio delle cuffie](#Canali_ALSA_muti_a_causa_di_un_collegamento.2Fscollegamento_improprio_delle_cuffie)
*   [36 Errore "invalid option" di pactl quando si specificano argomenti in formato percentuale negativo](#Errore_.22invalid_option.22_di_pactl_quando_si_specificano_argomenti_in_formato_percentuale_negativo)
*   [37 Messaggio "Daemon already running"](#Messaggio_.22Daemon_already_running.22)
*   [38 Il dispositivo di fallback non viene rispettato](#Il_dispositivo_di_fallback_non_viene_rispettato)
*   [39 Il microfono non funziona su Steam o Skype quando enable-remixing ha valore no](#Il_microfono_non_funziona_su_Steam_o_Skype_quando_enable-remixing_ha_valore_no)

### Niente suono dopo l'installazione

#### Dispositivo audio muto

Se non si sente nessun suono anche usando [ALSA](/index.php/ALSA_(Italiano) "ALSA (Italiano)") come dispositivo di default, potrebbe essere necessario togliere il mute dalla scheda audio. Per farlo, si dovrà lanciare `alsamixer` ed assicurarsi che ogni colonna abbia uno `00` verde sotto di essa (si prema `m` per abilitare/disabilitare il mute, dopo aver selezionato la colonna desiderata).

```
$ alsamixer -c 0

```

**Nota:** `alsamixer` non specifica quale dispositivo di output è quello di default. Una delle possibili cause della mancanza di suono dopo l'ìnstallazione di PulseAudio potrebbe proprio risiedere nell'erronea identificazione dell'output di default. Si provi ad installare [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) e a controllare se è presente dell'output quando si riproduce un file `.wav`.

#### Modalità Auto-Mute

La modalità Auto-Mute potrebbe essere abilitata, ed è possibile disabilitarla usando `alsamixer`.

Si veda [questa](http://superuser.com/questions/431079/how-to-disable-auto-mute-mode) discussione per ulteriori informazioni.

Per salvare le modifiche, si esegua `alsactl store` da root.

#### Files di configurazione non corretti

Se, dopo aver avviato Pulseaudio, il sistema non riproduce alcun suono, potrebbe essere necessario eliminare il contenuto delle directory `~/.pulse` e `~/.config/pulse`. Pulseaudio ricreerà quindi dei nuovi files di configurazione la prossima volta che verrà avviato.

#### Contenuti Flash

Dal momento che Flash non supporta PulseAudio direttamente, è consigliabile [configurare ALSA per utilizzare la scheda audio virtuale fornita da PulseAudio](#ALSA).

In alternativa, è possibile installare [libflashsupport-pulse](https://aur.archlinux.org/packages/libflashsupport-pulse/) da AUR.

**Nota:** L'installazione del pacchetto potrebbe mandare in crash il plugin flash.

Se l'audio tramite flash arriva in ritardo potrebbe essere necessario utilizzare ALSA direttamente: per risolvere si [configuri PulseAudio per l'utilizzo con dmix](#ALSA_.2F_dmix_senza_che_PulseAudio_prenda_possesso_della_scheda_audio).

#### Nessuna scheda audio rilevata

Se Pulseaudio si avvia, si esegua `pacmd list`. Se non viene elencata nessuna scheda audio, assicurarsi che i propri dispositivi ALSA non siano in uso:

```
$ fuser -v /dev/snd/*
$ fuser -v /dev/dsp

```

Assicurarsi che utte le applicazioni che usano i dispositivi sopra riportati siano chiuse. prima di riavviare Pulseaudio.

#### Viene visualizzato solo il dispositivo "dummy output", oppure le schede audio appena connesse non vengono rilevate

Questo comportamento potrebbe essere causato dalla presenza di un file `~/.asoundrc` che ha la precedenza rispetto alle impostazioni globali di sistema situate in`/etc/asound.conf`.

È possibile inibire gli effetti del file `~/.asoundrc` commentando l'ultima linea, in questo modo:

 `~/.asoundrc` 
```
# </home/*nomeutente*/.asoundrc.asoundconf>	

```

È anche possibile che qualche programma abbia accesso esclusivo al dispositivo audio. Si provi il seguente comando:

```
# fuser -v /dev/snd/*

```

Se l'output è simile a questo,

 `# fuser -v /dev/snd/*` 
```
                     USER      PID  ACCESS COMMAND
/dev/snd/controlC0:  root        931 F....  timidity
                     bob        1195 F....  panel-6-mixer
/dev/snd/controlC1:  bob        1195 F....  panel-6-mixer
                     bob        1215 F....  pulseaudio
/dev/snd/pcmC0D0p:   root        931 F...m  timidity
/dev/snd/seq:        root        931 F....  timidity
/dev/snd/timer:      root        931 f....  timidity

```

timidity potrebbe star impedendo a PulseAudio di accedere al dispositivo audio. Solitamente, uccidere il processo di timidity risolve il problema

Se il comando di cui sopra non produce output o quanto sopra non ha funzionato, si rimuova il pacchetto [timidity++](https://www.archlinux.org/packages/?name=timidity%2B%2B) e si riavvii il sistema per eliminare il dispositivo "dummy output".

Questo problema potrebbe anche essere causato da un conflitto tra [FluidSynth](/index.php/FluidSynth "FluidSynth") e PulseAudio, come riportato in [questo thread](https://bbs.archlinux.org/viewtopic.php?id=154002). Una soluzione potrebbe essere quella di rimuovere [fluidsynth](https://www.archlinux.org/packages/?name=fluidsynth)

In alternativa è possibile provare a modificare il file di configurazione (`/etc/conf.d/fluidsynth`), cambiando il driver in PulseAudio.

Una volta completata la modifica si riavviino fluidsynth e PulseAudio:

 `/etc/conf.d/fluidsynth`  `SYNTHOPTS="-is -a pulseaudio -m alsa_seq -r 48000"` 

#### Impossibilie scegliere output 5.1/7.1

Se non si riesce ad impostare l'output 5.1/7.1 da un dispositivo HDMI funzionante, è possibile provare a disabilitare la "lettura dei dispositivi di streaming" tramite il file `/etc/pulse/default.pa`:

Si veda a tal proposito [#Il dispositivo di fallback non viene rispettato](#Il_dispositivo_di_fallback_non_viene_rispettato)

#### KDE4

È possibile che un altro dispositivo sia impostato come preferito da phonon. Assicurarsi che ogni impostazione ad esso relativa abbia il dispositivo di output preferito in cima alla lista, e si controlli la tab "playback streams" in `kmix` per verificare che le applicazioni lo stiano utilizzando.

Per visualizzare il dispositivo audio predefinito, si esegua:

$ pactl stat

Per l'elenco dei dispositivi audio disponibili, eseguire:

$ pactl list

Per impostare un dispositivo audio come predefinito si utilizzi il comando `pacmd` o si modifichi `/etc/pulse/default.pa`:

```
set-default-sink alsa_output.analog-stereo

```

#### Errore "Failed to create sink input: sink is suspended"

Se non viene riprodotto alcun suono e `journalctl -b` riceve molti errori relativi ad un sink sospeso, si effettui il backup e poi si rimuovano le cartelle di PulseAudio relative al proprio utente:

```
$ rm -r ~/.pulse ~/.pulse-cookie ~/.config/pulse

```

### Avviare una applicazione interrompe il suono di un'altra

Se alcune applicazioni (ad esempio Teamspeak o Mumble) interrompono la riproduzione di altre già avviate (ad esempio DeadBeef), è possibile rimediare commentando la linea `load-module module-role-cork` in `/etc/pulse/default.pa`, come mostrato sotto:

 `/etc/pulse/default.pa` 
```
### Cork music/video streams when a phone stream is active
# load-module module-role-cork

```

Si riavvii PulseAudio come utente normale:

```
$ pulseaudio -k
$ pulseaudio --start

```

### Nessun output audio HDMI se si spegne il monitor per un certo periodo di tempo

Il monitor è collegato tramite HDMI/DisplayPort, e il jack audio è collegato all'uscita cuffie sul monitor, ma PulseAudio lo considera scollegato.

 `pactl list sinks` 
```
...
hdmi-output-0: HDMI / DisplayPort (priority: 5900, not available)
...

```

Il che non consente la riproduzione del suono dall'uscita HDMI. È possibile ovviare al problema cambiando momentaneamente VT. Se quanto sopra non funziona si provi a spegnere il monitor, cambiare VT, riaccendere il monitor e tornare a quella utilizzata in precedenza. Il problema affligge gli utenti con schede video ATI/Nvidia/Intel.

### Abilitare la soppressione dei rumori/dell'eco

Arch non carica automaticamente il modulo relativo: sarà quindi necessario aggiungerlo in `/etc/pulse/default.pa`. Verificare innanzitutto se il modulo esiste con `pacmd`, inserendo il comando {{|iclist-modules}}. Se non viene visualizzata una linea simile a {ic|name: <module-echo-cancel>}}, sarà necessario aggiungere:

 `/etc/pulse/default.pa` 
```
load-module module-echo-cancel

```

quindi riavviare PulseAudio

```
$ pulseaudio -k
$ pulseaudio --start

```

Controllare nuovamente l'avvenuto caricamento del modulo tramite `pavucontrol`. Nel tab `Recording`, il dispositivo di input dovrebbe mostrare `Echo-Cancel Source Stream from"`

### Non è possibile aggiornare la configurazione della scheda audio da pavucontrol

[pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) è un utile tool grafico per configurare PulseAudio. Nella scheda "Configuration" è possibile scegliere un profilo diverso per ogni dispositivo di riproduzione, come Stereo analogico, output digitale (IEC958), HDMI 5.1 Surround eccetera.

Può tuttavia verificarsi un crash del demone Pulse con conseguente autoriavvio se si tenta di scegliere un profilo diverso per una scheda audio, senza che le modifiche vengano salvate. Nel caso, si utilizzi il tool grafico [paprefs](https://www.archlinux.org/packages/?name=paprefs) e controllare se sotto la scheda "Simultaneous Output" sia presente un dispositivo simultaneo virtuale: se lo stesso è abilitato, non si sarà in grado di cambiare le impostazioni da `pavucontrol`. Si disabiliti momentaneamente il dispositivo deselezionando la relativa casella, si effettuino le modifiche in `pavucontrol` e si riabiliti il dispositivo.

### Output simultaneo verso più schede audio / dispositivi

L'output simultaneo verso dispositivi differenti è una funzionalità molto utile: ad esempio è possibile inviare l'audio al proprio ricevitore A/V tramite l'uscita HDMI della propria scheda video e allo stesso tempo inviarlo all'uscita analogica posta sulla propria scheda madre.

La procedura è molto meno problematica rispetto al passato (nell'esempio che segue, verrà utilizzato il DE GNOME).

Utilizzando [paprefs](https://www.archlinux.org/packages/?name=paprefs), si selezioni "Add virtual output device for simultaneous output on all local sound cards", posto sotto la scheda "Simultaneous Output" quindi, dalle impostazioni audio di GNOME, si selezioni l'uscita virtuale appena creata.

Se quanto sopra non funziona, aggiungere le seguenti righe al proprio `~/.asoundrc`:

```
pcm.dsp {
 type plug
 slave.pcm "dmix"
}

```

### L'output simultaneo verso più schede audio / dispositivi non funziona

Quanto segue è utile ad utenti che hanno differenti sorgenti sonore e vogliono riprodurle su sinks/output differenti. Un caso d'uso potrebbe essere il riprodurre simultaneamente musica e la voce di una chat, redirigendo la musica agli altoparlanti (in questo caso l'uscita Digital S/PDIF) e la voce alle cuffie (Analog).

PulseAudio non riesce sempre a rilevare la configurazione descritta sopra. Se si è certi che la propria scheda audio supporti questa funzionalità e non viene visualizzata la relativa opzione nei profili di [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) o [veromix](https://www.archlinux.org/packages/?name=veromix), potrebbe essere necessario creare un file di configurazione per la propria scheda.

Nello specifico, si dovrà creare un profilo per la propria scheda. Il procedimento può essere diviso in due parti:

*   Creazione della regola di udev per costringere PulseAudio a scegliere il file di configurazione personalizzato per la scheda audio in uso
*   Creazione del file di configurazione

Si crei una regola udev per PulseAudio:

**Nota:** Quanto segue è un esempio valido per una Asus Xonar Essence STX. Si legga la pagina del wiki relativa ad [udev](/index.php/Udev_(Italiano) "Udev (Italiano)") per trovare i valori corretti.

**Nota:** La regola deve avere un numero più basso rispetto a quella originale per avere effetto.
 `/usr/lib/udev/rules.d/90-pulseaudio-Xonar-STX.rules` 
```
ACTION=="change", SUBSYSTEM=="sound", KERNEL=="card*", \
ATTRS{subsystem_vendor}=="0x1043", ATTRS{subsystem_device}=="0x835c", ENV{PULSE_PROFILE_SET}="asus-xonar-essence-stx.conf" 

```

Si crei quindi un nuovo profilo. È possibile partire da zero ed arricchirlo man mano, oppure utilizzare il profilo originale rinominandolo e facendo le dovute modifiche.

Per abilitare sink multipli su una Asus Xonar Essence STX, si scriva quanto segue:

**Nota:** `asus-xonar-essence-stx.conf` comprende tutto il codice/mappature di `default.conf`.
 `/usr/share/pulseaudio/alsa-mixer/profile-sets/asus-xonar-essence-stx.conf` 
```
[Profile analog-stereo+iec958-stereo]
description = Analog Stereo Duplex + Digital Stereo Output
input-mappings = analog-stereo
output-mappings = analog-stereo iec958-stereo
skip-probe = yes

```

Quanto sopra configurerà la vostra Asus Xonar Essence STX con i profili di default e consente l'aggiunta di un profilo personalizzato per l'utilizzo con più sink simultanei.

Sarà necessario creare un ulteriore profilo nel file di configurazione se si vorrà usufruire della stessa funzionalità con output AC3 Digital 5.1.

Si legga [questo](https://www.freedesktop.org/wiki/Software/PulseAudio/Backends/ALSA/Profiles/) articolo sui profili di PulseAudio.

### Disabilitare il supporto ai dispositivi Bluetooth

Se non si utilizzano dispositivi Bluetooth, il journal di sistema potrebbe contenere il seguente errore:

```
bluez5-util.c: GetManagedObjects() failed: org.freedesktop.DBus.Error.ServiceUnknown: The name org.bluez was not provided by any .service files

```

Per disabilitare il supporto Bluetooth in PulseAudio, assicurarsi che le seguenti linee dei file di configurazione `~/.config/pulse/default.pa` o `/etc/pulse/default.pa` siano commentate:

 `~/.config/pulse/default.pa` 
```
### Automatically load driver modules for Bluetooth hardware
#.ifexists module-bluetooth-policy.so
#load-module module-bluetooth-policy
#.endif

#.ifexists module-bluetooth-discover.so
#load-module module-bluetooth-discover
#.endif

```

### Problemi di riproduzione con cuffie Bluetooth

Alcuni utenti [riferiscono](https://bbs.archlinux.org/viewtopic.php?id=117420) di enormi ritardi nella riproduzione del suono, o addirittura assenza di suono quando la connessione bluetooth rimane inattiva. Ciò è causato da `idle-suspend-module`, che mette a risposo automaticamente le sinks/sources relative. Visto che questo modulo causa problemi con i dispositivi bluetooth, può essere disattivato.

Per disabilitare il modulo in questione, assicurarsi che le seguenti linee dei file di configurazione `~/.config/pulse/default.pa` o `/etc/pulse/default.pa` siano commentate:

 `~/.config/pulse/default.pa` 
```
### Automatically suspend sinks/sources that become idle for too long
#load-module module-suspend-on-idle

```

Si riavvii PulseAudio per applicare i cambiamenti.

### Switch automatico agli headset Bluetooth o USB

Si aggiunga la seguente riga al file `/etc/pulse/default.pa`:

 `/etc/pulse/default.pa` 
```
 # automatically switch to newly-connected devices
 load-module module-switch-on-connect

```

### Pulse sovrascrive le impostazioni di Alsa

Pulseaudio è solito sovrascrivere le impostazioni di Alsa; ad esempio quando si ripristinano i livelli del volume all'avvio, anche se il demone alsa è attivo. Dal momento che non sembrano esserci altri modi per limitare questo comportamento, è necessario ricorrere ad un workaround che ripristini nuovamente le impostazioni di Alsa dopo che Pulseaudio si è avviato.

Si aggiunga il seguente comando a `.xinitrc`, `.bash_profile` o a qualsiasi altro file si utilizzi per l'[autostart](/index.php/Autostarting "Autostarting") delle applicazioni:

```
restore_alsa() {
 while [ -z "$(pidof pulseaudio)" ]; do
  sleep 0.5
 done
 alsactl -f /var/lib/alsa/asound.state restore 
}
restore_alsa &

```

### Impedire il riavvio di PulseAudio una volta ucciso

Potrebbe capitare di voler temporaneamente disabilitare il riavvio automatico di PulseAudio; per farlo si aggiunga la seguente riga al file `~/.pulse/client.conf`:

```
autospawn=no

```

### Avvio del demone fallito

Si provi a ripristinare la configurazione di Pulseaudio, in questo modo:

```
$ rm -rf /tmp/pulse* ~/.pulse* ~/.config/pulse
$ pulseaudio -k
$ pulseaudio --start

```

*   Si controlli che le opzioni per i vari sinks siano corrette

*   Se si è modificato il file `default.pa` per utilizzare i moduli OSS, controllare tramite [lsof](https://www.archlinux.org/packages/?name=lsof) che `/dev/dsp` non sia utilizzato da altre applicazioni.

*   LXDE potrebbe avere problemi a chiudere tutte le applicazioni dopo che si è effettuato il logout. Per risolvere leggere: [Incorrect logout handling](/index.php/LXDM#Incorrect_logout_handling "LXDM").

*   Si imposti un metodo di ricampionamento preferito. Utilizzare `pulseaudio --dump-resample-methods` per visualizzare quelli disponibili.

*   Per visualizzare informazioni su eventuali errori o per conoscere lo stato del demone, utilizzare comandi come `pax11publish -d` e `pulseaudio -v`, dove l'opzione `v` può essere specificata più volte per impostare la verbosità dell'output, similmente all'opzione `--log-level=[LEVEL]` dove *LEVEL* va da 0 a 4\. Si veda la sezione [#Possibili output delle utility per il controllo degli errori di PulseAudio](#Possibili_output_delle_utility_per_il_controllo_degli_errori_di_PulseAudio) per ulteriori informazioni.

Si consultino inoltre le pagine di manuale per [pax11publish(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pax11publish.1) e [pulseaudio(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pulseaudio.1).

#### Possibili output delle utility per il controllo degli errori di PulseAudio

Se `pax11publish -d` visualizza un messaggio simile a questo:

```
 N: [pulseaudio] main.c: User-configured server at "user", refusing to start/autospawn.

```

Si esegua `pax11publish -r`, quindi effettuare nuovamente il login. Tale operazione è sempre necessaria se si utilizza LXDM, in quanto quest'ultimo non riavvia il server X al logout. Si veda [LXDM#PulseAudio](/index.php/LXDM#PulseAudio "LXDM").

Se il comando `pulseaudio -vvvv` mostra un messaggio simile a:

```
E: [pulseaudio] module-udev-detect.c: You apparently ran out of inotify watches, probably because Tracker/Beagle took them all away. I wished people would do their homework first and fix inotify before using it for watching whole directory trees which is something the current inotify is certainly not useful for. Please make sure to drop the Tracker/Beagle guys a line complaining about their broken use of inotify.

```

È possibile risolvere temporaneamente con:

```
$ echo 100000 > /proc/sys/fs/inotify/max_user_watches

```
Per rendere la modifica permanente, si modifichi `/etc/sysctl.d/99-sysctl.conf` 
```
 # Increase inotify max watches per user
 fs.inotify.max_user_watches = 100000

```

**Attenzione:** Quanto sopra potrebbe aumentare il consumo di memoria da parte del kernel.

**Vedere anche**

*   [proc_sys_fs_inotify](http://www.linuxinsight.com/proc_sys_fs_inotify.html) e [dnotify, inotify](http://lwn.net/Articles/604686/) - ulteriori dettagli su *inotify/max_user_watches*
*   [valori ragionevoli per inotify watches su Linux](http://stackoverflow.com/questions/535768/what-is-a-reasonable-amount-of-inotify-watches-with-linux?answertab=votes#tab-top)
*   [inotify(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/inotify.7) - pagina di manuale

### Artefatti sonori, audio intermittente o gracchiante

La nuova implementazione del server Pulseaudio usa uno scheduling audio basato su timer, invece di usare l'approccio traduzionale basato sugli interrupt. Lo scheduling basato su timer potrebbe causare problemi con alcuni driver ALSA, anche altri potrebbero dare problemi se lo si disattiva, perciò si agisca in base a come si comporta il proprio sistema.

Per disattivarlo, si aggiunga `tsched=0` come parametro al modulo udev-detect in `/etc/pulse/default.pa`:

 `/etc/pulse/default.pa` 
```
 load-module module-udev-detect tsched=0

```

Poi si riavvii Pulseaudio:

```
$ pulseaudio -k
$ pulseaudio --start

```

Si compiano gli stessi passaggi a ritroso per abilitare lo scheduling basato su timer, se non è stato abilitato di default.

L'utilizzo della funzionalità [IOMMU](https://en.wikipedia.org/wiki/IOMMU "wikipedia:IOMMU") di Intel potrebbe causare questo problema. Si provi quindi a passare al kernel il parametro`intel_iommu=igfx_off`.

Se possibile, segnalare le schede audio con le quali si verifica il problema in [questa](http://www.freedesktop.org/wiki/Software/PulseAudio/Backends/ALSA/BrokenDrivers/) pagina.

### Impostare il numero di frammenti e la dimensione del buffer in PulseAudio

[Ulteriori informazioni](http://forums.linuxmint.com/viewtopic.php?f=42&t=44862)

#### Identificare i parametri della scheda audio in uso (1/4)

Si eseguano i seguenti comandi bash per individuare le impostazioni di buffering della propria scheda audio:

```
$ echo autospawn = no >> ~/.config/pulse/client.conf
$ pulseaudio -k
$ LANG=C timeout --foreground -k 10 -s kill 10 pulseaudio -vvvv 2>&1 | grep device.buffering -B 10
$ sed -i '$d' ~/.config/pulse/client.conf

```

Per ogni scheda audio identificata da PulseAudio si avrà un output simile al seguente:

```
I: [pulseaudio] source.c:     alsa.long_card_name = "HDA Intel at 0xfa200000 irq 46"
I: [pulseaudio] source.c:     alsa.driver_name = "snd_hda_intel"
I: [pulseaudio] source.c:     device.bus_path = "pci-0000:00:1b.0"
I: [pulseaudio] source.c:     sysfs.path = "/devices/pci0000:00/0000:00:1b.0/sound/card0"
I: [pulseaudio] source.c:     device.bus = "pci"
I: [pulseaudio] source.c:     device.vendor.id = "8086"
I: [pulseaudio] source.c:     device.vendor.name = "Intel Corporation"
I: [pulseaudio] source.c:     device.product.name = "82801I (ICH9 Family) HD Audio Controller"
I: [pulseaudio] source.c:     device.form_factor = "internal"
I: [pulseaudio] source.c:     device.string = "front:0"
I: [pulseaudio] source.c:     device.buffering.buffer_size = "768000"
I: [pulseaudio] source.c:     device.buffering.fragment_size = "384000"

```

Si prenda nota dei valori `buffer_size` e `fragment_size` per la scheda audio in uso.

#### Si calcolino la dimensione ed il numero di frammenti in millisecondi (2/4)

La frequenza di campionamento di default in PulseAudio e i bit utilizzati corrispondono rispettivamente a `44100 Hz` e `16 bit`.

Utilizzando questi valori, il bitrate da impostare corrisponde a `44100 * 16 = 705600` bit al secondo, oppure `1411200 b/s` in caso si utilizzino due canali (stereo).

Utilizziamo i valori ottenuti nel passaggio precedente:

```
device.buffering.buffer_size = "768000" => 768000/1411200 = 0.544217687075s = 544 ms
device.buffering.fragment_size = "384000" => 384000/1411200 = 0.272108843537s = 272 ms

```

#### Modificare il file di configurazione di PulseAudio (3/4)

 `/etc/pulse/daemon.conf` 
```
; default-fragments = X
; default-fragment-size-msec = Y

```

Nel passagio precedente si è calcolata la dimensione del frammento. Il numero di frammenti è dato da `buffer_size / fragment_size` che nel nostro caso (`544/272`) è `2`.

Si modifichino quindi le righe di cui sopra utilizzando i risultati ottenuti:

 `/etc/pulse/daemon.conf` 
```
; default-fragments = '''2'''
; default-fragment-size-msec = '''272'''

```

#### Riavviare il demone PulseAudio (4/4)

```
$ pulseaudio -k
$ pulseaudio --start

```

### Il suono arriva in ritardo

Questo problema è causato da una dimensione non corretta dei buffer. Si verifichi che le variabili `default-fragments`e `default-fragment-size-msec` non abbiano valori differenti da quelli di default contenuti nel file `/etc/pulse/daemon.conf`.

Se il problema si verifica nuovamente si provi ad assegnare questi valori:

 `/etc/pulse/daemon.conf` 
```
default-fragments = 5
default-fragment-size-msec = 2
```

### Suono intermittente e distorto

La scelta di una frequenza di campionamento errata può causare un suono intermittente. Si effettui la seguente modifica:

 `/etc/pulse/daemon.conf` 
```
default-sample-rate = 48000

```

E si riavvii il server Pulseaudio.

Se il suono è intermittente in applicazioni che usano [OpenAL](https://en.wikipedia.org/wiki/OpenAL "wikipedia:OpenAL"), si dovrebbe cambiare la frequenza di campionamento anche in `/etc/openal/alsoft.conf`:

 `/etc/openal/alsoft.conf`  `frequency = 48000` 

Impostare il volume del canale PCM sopra 0dB può causare il [clipping](https://en.wikipedia.org/wiki/Clipping_(audio) del segnale audio. Eseguire `alsamixer -c0` permetterà di capire se questo è il problema. Si noti che ALSA [correctly potrebbe](http://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/PulseAudioStoleMyVolumes) non passare correttamente il valore della frequenza di campionamento a PulseAudio.

Si provi come segue:

 `/etc/pulse/defaults.pa` 
```
load-module module-udev-detect ignore_dB=1

```

E si riavvii PulseAudio. Si veda anche [#Assenza di suono sotto un certo livello di volume](#Assenza_di_suono_sotto_un_certo_livello_di_volume)

### I controlli del volume non funzionano correttamente

Si potrebbe voler controllare:

```
/usr/share/pulseaudio/alsa-mixer/paths/analog-output.conf.common

```

Poiché pulseaudio ha una maggior raggio di incremento (0-65535, per essere precisi), è possibile che il volume non venga regolato correttamente usando `alsamixer` o `amixer`. Si provino ad usare valori più grandi quando si cambia il volume (es: `amixer set Master 655+`).

### Il volume delle singole applicazioni varia quando si modifica il livello del volume generale

Questo comportamento si verifica a causa dell'utilizzo dei "flat-volumes" da parte di PulseAudio al posto dei volumi relativi, relativi ad un volume master assoluto. Se questa funzionalità dovesse apparirvi scomoda, stupida o comunque indesiderabile, è possibile abilitare i volumi relativi disabilitando i "flat-volumes":

 `/etc/pulse/daemon.conf o ~/.config/pulse/daemon.conf` 
```
flat-volumes = no

```

Riavviare poi Pulseaudio con:

```
$ pulseaudio -k
$ pulseaudio --start

```

### Il livello del volume si alza ogni volta che una nuova applicazione viene avviata

Pare che, come comportamento di default, la modifica del volume di una applicazione vari di conseguenza il livello volume generale invece di riguardare la singola applicazione. Anche le applicazioni che impostano il proprio volume all'avvio causano questo problema.

È possibile risolvere disabilitando i flat volumes, come spiegato nella sezione precedente. Quando Pulseaudio si sarà riavviato, le applicazioni non altereranno più il volume di sistema e faranno riferimento ai propri livelli di volume.

**Nota:** Una precedente installazione e successiva rimozione di un equalizzatore per PulseAudio potrebbe lasciare tracce in `~/.config/pulse/default.pa`, che potrebbero causare problemi di volume impostato al massimo. Si commentino le parti relative secondo le proprie necessità.

### Microfono non funzionante su ThinkPad T400/T500/T420

Si esegua:

```
alsamixer -c 0

```

e si porti al massimo/si tolga il mute dal controllo "Internal Mic".

Anche se il device associato viene visualizzato tramite il comando

```
arecord -l

```

potrebbe essere ancora necessario sistemare le impostazioni, dal momento che il microfono e il jack audio sono "duplexed". Si imposti il valore dell'audio interno in pavucontrol ad "Analog Stereo Duplex".

### Microfono non funzionante su Acer Aspire One

Si installi [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol), si scolleghino i canali del microfono e si imposti a 0 quello di sinistra. Ora si dovrebbe essere in grado di utilizzare il microfono. Riferimenti: [http://getsatisfaction.com/jolicloud/topics/deaf_internal_mic_on_acer_aspire_one#reply_2108048](http://getsatisfaction.com/jolicloud/topics/deaf_internal_mic_on_acer_aspire_one#reply_2108048)

### Output monocanale su M-Audio Audiophile 2496

Si aggiunganno le seguenti righe a `/etc/pulse/default.pa`:

 `/etc/pulse/default.pa` 
```
load-module module-alsa-sink sink_name=delta_out device=hw:M2496 format=s24le channels=10 channel_map=left,right,aux0,aux1,aux2,aux3,aux4,aux5,aux6,aux7
load-module module-alsa-source source_name=delta_in device=hw:M2496 format=s24le channels=12 channel_map=left,right,aux0,aux1,aux2,aux3,aux4,aux5,aux6,aux7,aux8,aux9
set-default-sink delta_out
set-default-source delta_in

```

### Rumore statico durante la registrazione da microfono

Se si ottiene del rumore di fondo nelle registrazioni con skype, gnome-sound-recorder, arecord eccetera, allora la frequenza di campionamento della scheda audio non è corretta. Per risolvere il problema, dobbiamo impostare la frequenza di campionamento in `/etc/pulse/daemon.conf`.

#### Determinare le schede audio installate nel sistema (1/5)

È necessario che [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) e i relativi pacchetti siano installati:

 `$ arecord --list-devices` 
```
   **** List of CAPTURE Hardware Devices ****
   card 0: Intel [HDA Intel], device 0: ALC888 Analog [ALC888 Analog]
     Subdevices: 1/1
     Subdevice #0: subdevice #0
   card 0: Intel [HDA Intel], device 2: ALC888 Analog [ALC888 Analog]
     Subdevices: 1/1
     Subdevice #0: subdevice #0

```

La scheda audio è `hw:0,0`.

#### Determinare la frequenza di campionamento della scheda audio (2/5)

 ` arecord -f dat -r 60000 -D hw:0,0 -d 5 test.wav` 
```
  "Recording WAVE 'test.wav' : Signed 16 bit Little Endian, Rate 60000 Hz, Stereo
  Warning: rate is not accurate (requested = 60000Hz, got = 96000Hz)
  please, try the plug plugin

```

Si noti il `got = 96000Hz`, che indica la frequenza di campionamento massima supportata dalla scheda audio.

#### Impostare la frequenza di campionamento nella configurazione di Pulseaudio (3/5)

La frequenza di campionamento predefinita in Pulseaudio è ottenibile con:

 `$ grep "default-sample-rate" /etc/pulse/daemon.conf` 
```
; default-sample-rate = 44100

```

È pari a `44100 Hz` ed è disabilitata. Si imposti ora la frequenza di campionamento desiderata con il comando seguente:

```
# sed 's/; default-sample-rate = 44100/default-sample-rate = 96000/g' -i /etc/pulse/daemon.conf

```

#### Riavviare Pulseaudio per applicare i cambiamenti(4/5)

```
$ pulseaudio -k
$ pulseaudio --start

```

#### Effettuare una prova registrando e poi ascoltando la registrazione (5/5)

```
$ arecord -f cd -d 10 test-mic.wav

```

Dopo 10 secondi, riprodurre la registrazione:

```
$ aplay test-mic.wav

```

Il problema dovrebbe essere stato risolto.

### Il mio dispositivo bluetooth viene rilevato ma non riproduce alcun suono

[Si faccia riferimento a questo articolo nella sezione Bluetooth](/index.php/Bluetooth#My_device_is_paired_but_no_sound_is_played_from_it "Bluetooth")

A partire da PulseAudio 2.99 e bluez 4.101 è consigliabile evitare l'utilizzo dell'interfaccia Socket. **Non aggiungere quanto segue al proprio** `/etc/bluetooth/audio.conf`:

 `/etc/bluetooth/audio.conf` 
```
 [General]
 Enable=Socket

```

Se si hanno problemi con A2DP e Pulseaudio 2.99 assicurarsi di aver installato la libreria [sbc](https://www.archlinux.org/packages/?name=sbc):

### Il subwoofer smette di funzionare alla fine della riproduzione di una canzone

Problema noto: [https://bugs.launchpad.net/ubuntu/+source/pulseaudio/+bug/494099](https://bugs.launchpad.net/ubuntu/+source/pulseaudio/+bug/494099)

Per risolvere, modificare `/etc/pulse/daemon.conf` e abilitare l'opzione `enable-lfe-remixing`:

 `/etc/pulse/daemon.conf` 
```
enable-lfe-remixing = yes

```

### Pulseaudio utilizza il microfono sbagliato

Se Pulseaudio utilizza il microfono sbagliato e si è già provato a modificare il dispositivo di input tramite `pavucontrol`, è consigliabile controllare le impostazioni di `alsamixer`. Talvolta può accadere che `pavucontrol` non imposti correttamente i dispositivi di input.

Si esegua:

```
$ alsamixer

```

Si prema `F6` e si selezioni la propria scheda audio (es. `HDA Intel`. Ora si prema `F5` per mostrare tutte le voci. Si cerchi la voce `Input Source` e la si modifichi con l'ausilio dei tasti freccia.

Si verifichi quindi l'utilizzo del microfono corretto.

### Suono intermittente quando si usa il profilo Analog Surround Sound

Il canale LFE (low-frequency effects) non viene remixato di default. Per abilitare questa funzionalità si modifichi `/etc/pulse/daemon.conf`:

 `/etc/pulse/daemon.conf` 
```
enable-lfe-remixing = yes

```

### Impossibilità di scegliere configurazioni surround diverse da "Surround 4.0"

Se non si è in grado di selezionare l'output surround 5.1 da *pavucontrol*, si apra il mixer di ALSA e si imposti un output a 6 canali. Si riavvii quindi PulseAudio; *pavucontrol* mostrerà ora più opzioni.

### Assenza di suono sotto un certo livello di volume

Problema conosciuto (non sarà sistemato): [https://bugs.launchpad.net/ubuntu/+source/pulseaudio/+bug/223133](https://bugs.launchpad.net/ubuntu/+source/pulseaudio/+bug/223133)

Se non viene riprodotto alcun suono sotto un certo livello di volume, si passi `ignore_dB=1` come parametro al modulo udev-detect nel file `/etc/pulse/default.pa`:

 `/etc/pulse/default.pa` 
```
load-module module-udev-detect ignore_dB=1

```

### Basso livello volume del microfono integrato

Se il volume del microfono integrato del vostro notebook è troppo basso, si inserisca alla fine del file:

 `/etc/pulse/default.pa` 
```
set-source-volume 1 300000

```

### I client alterano il controllo volume generale (ovvero volume al massimo dopo aver lanciato un'applicazione)

Potrebbe capitare che, a causa della modalità *flat volumes* di PulseAudio, la modifica del volume in applicazioni specifiche abbia effetto anche sul volume generale di sistema. Al posto di disabilitare tale modalità, gli utenti KDE dovrebbero provare ad abbassare il volume delle notifiche di sistema in *Impostazioni di sistema -> Notifiche delle applicazioni e di sistema -> Gestisci le notifiche*, tab *Impostazioni di riproduzione*. La modifica del livello volume *Event Sounds* in KMix o altri mixer non sortirà l'effetto desiderato.

Nel caso la modalità flat-volumes non funzioni, è probabile che qualche altra applicazione stia richiedendo il livello volume al 100% durante la riproduzione. Se non ri riesce a risolvere il problema, è possibile disabilitare la modalità *flat volumes*:

 `/etc/pulse/daemon.conf` 
```
flat-volumes = no

```

Si riavvii quindi il demone PulseAudio:

```
# pulseaudio -k
# pulseaudio --start

```

### Scheduling realtime

Se rtkit non funziona è possibile avviare PulseAudio con lo scheduling in realtime manualmente. Per farlo si aggiungano le seguenti righe ad `/etc/security/limits.conf`:

```
@pulse-rt - rtprio 9
@pulse-rt - nice -11

```

Sarà quindi necessario aggiungere il proprio utente al gruppo `pulse-rt`:

```
# gpasswd -a <utente> pulse-rt

```

### Nessun suono dopo il resume dalla sospensione

Se l'audio smette di funzionare dopo un resume, si provi a ricaricare PulseAudio eseguendo:

```
$ /usr/bin/pasuspender /bin/true

```

Il comando di cui sopra è preferibile all'uccisione e riavvio del server (`pulseaudio -k` seguito da `pulseaudio --start`), poichè non crea problemi alle applicazioni già in esecuzione.

Se le operazioni di cui sopra risolvono il problema, si potrebbe volerle automatizzare creando un file .service per systemd:

1\. Si crei il template:

 `/etc/systemd/system/resume-fix-pulseaudio@.service` 
```
[Unit]
Description=Fix PulseAudio after resume from suspend
After=suspend.target

[Service]
User=%I
Type=oneshot
Environment="XDG_RUNTIME_DIR=/run/user/%U"
ExecStart=/usr/bin/pasuspender /bin/true

[Install]
WantedBy=suspend.target

```

2\. Abilitarlo per il proprio account:

```
# systemctl enable resume-fix-pulseaudio@NOME_UTENTE.service

```

3\. Riavviare systemd:

```
# systemctl --system daemon-reload

```

### Canali ALSA muti a causa di un collegamento/scollegamento improprio delle cuffie

Se quando si collegano/scollegano le cuffie vengono impostati come muti i canali sbagliati in `alsamixer` è possibile provare a commentare la seguente riga in `/etc/pulse/default.pa`:

```
load-module module-switch-on-port-available

```

### Errore "invalid option" di pactl quando si specificano argomenti in formato percentuale negativo

I comandi di `pactl` che accettano percentuali negative come argomenti mostreranno l'errore in oggetto. Si utilizzi `--` prima dell'argomento con valore negativo per disabilitarne il parsing. Esempio: `pactl set-sink-volume 1 -- -5%`.

### Messaggio "Daemon already running"

Su alcuni sistemi, PulseAudio potrebbe venir avviato più volte. In questi casi `journalctl` mostrerà il seguente messaggio:

```
[pulseaudio] pid.c: Daemon already running.

```

Assicurarsi di utilizzare solo uno dei metodi per l'avvio automatico delle applicazioni. [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) include al suo interno i seguenti files:

*   `/etc/X11/xinit/xinitrc.d/pulseaudio`
*   `/etc/xdg/autostart/pulseaudio.desktop`
*   `/etc/xdg/autostart/pulseaudio-kde.desktop`

Si controllino anche i files e le directory dell'utente, come [xinitrc](/index.php/Xinitrc_(Italiano) "Xinitrc (Italiano)"), `~/.config/autostart` eccetera.

### Il dispositivo di fallback non viene rispettato

PulseAudio non ha un vero e proprio dispositivo di output di default, bensì utilizza un [fallback](http://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/DefaultDevice), applicato solamente ai nuovi stream, il che significa che eventuali applicazioni già in esecuzione non verranno influenzate dal dispositivo di fallback appena creato.

I pacchetti [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center), [mate-media-pulseaudio](https://www.archlinux.org/packages/?name=mate-media-pulseaudio) e [paswitch](https://aur.archlinux.org/packages/paswitch/) gestiscono questa funzionalità in modo elegante. In alternativa si proceda come segue:

1\. Si spostino manualmente tramite [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) gli stream già in esecuzione al nuovo dispositivo.

2\. Si termini PulseAudio e si cancelli *stream-volumes* in `~/.config/pulse`, quindi si riavvii PulseAudio. Questa operazione azzera i livelli volume personalizzati delle applicazioni.

3\. Si disabiliti la lettura dei dispositivi di streaming. Tale operazione potrebbe non essere desiderata se si utilizzano diverse schede audio con diverse applicazioni:

 `/etc/pulse/default.pa` 
```
load-module module-stream-restore restore_device=false

```

### Il microfono non funziona su Steam o Skype quando enable-remixing ha valore no

Se si imposta la variabile `enable-remixing = no` in `/etc/pulse/daemon.conf` è possibile che il microfono smetta di funzionare con applicazioni come Skype o Steam. Il problema è causato dal fatto che queste applicazioni catturano il microfono come mono e, dal momento che il remixing è disabilitato, PulseAudio non è in grado di mixare nuovamente il microfono stereo in mono.

Sarà necessario qundi abilitare il remixing:

1\. Identificare il nome della sorgente:

```
# pacmd list-sources

```

Output di esempio troncato per brevità: la parte d'interesse è evidenziata in grassetto:

```
   index: 2
       name: <**alsa_input.pci-0000_00_14.2.analog-stereo**>
       driver: <module-alsa-card.c>
       flags: HARDWARE HW_MUTE_CTRL HW_VOLUME_CTRL DECIBEL_VOLUME LATENCY DYNAMIC_LATENCY

```

2\. Si aggiunga una regola di rimappatura in `/etc/pulse/default.pa` usando il valore ottenuto con il comando precedente, in questo caso **alsa_input.pci-0000_00_14.2.analog-stereo**:

 `/etc/pulse/default.pa` 
```
### Remap microphone to mono
load-module module-remap-source master=alsa_input.pci-0000_00_14.2.analog-stereo master_channel_map=front-left,front-right channels=2 channel_map=mono,mono

```

3\. Riavviare PulseAudio:

```
# pulseaudio -k

```

**Nota:** PulseAudio potrebbe non avviarsi correttamente se non si chiudono le applicazioni che stavano usando il microfono (ad esempio se si sono effettuate delle prove su Steam prima di modificare il file), nel qual caso sarà necessario avviare manualmente PulseAudio:
```
# pulseaudio --start

```