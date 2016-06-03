Tratto da Bumblebee's [FAQ](https://github.com/Bumblebee-Project/Bumblebee/wiki/FAQ):

"*Bumblebee è una soluzione per rendere la tecnologia di Nvidia Optimus, presente sui computer portatili predisposti, disponibile nei sistemi GNU/Linux. Tale caratteristica coinvolge due schede grafiche con due differenti profili di consumo di alimentazione, che collegati in modo stratificato condividono un singolo framebuffer.*"

## Contents

*   [1 Bumblebee: Tecnologia Optimus per Linux](#Bumblebee:_Tecnologia_Optimus_per_Linux)
*   [2 Installazione](#Installazione)
    *   [2.1 Installare Bumblebee con Intel/Nvidia](#Installare_Bumblebee_con_Intel.2FNvidia)
    *   [2.2 Installare Bumblebee con Intel/Nouveau](#Installare_Bumblebee_con_Intel.2FNouveau)
*   [3 Avviare Bumblebee](#Avviare_Bumblebee)
*   [4 Utilizzo](#Utilizzo)
*   [5 Configurazione](#Configurazione)
    *   [5.1 Ottimizzare la velocità quando si utilizza VirtualGL come bridge](#Ottimizzare_la_velocit.C3.A0_quando_si_utilizza_VirtualGL_come_bridge)
    *   [5.2 Gestione energetica](#Gestione_energetica)
        *   [5.2.1 Risparmio energetico predefinito della scheda NVIDIA con bbswitch](#Risparmio_energetico_predefinito_della_scheda_NVIDIA_con_bbswitch)
        *   [5.2.2 Abilitare la scheda NVIDIA durante lo spegnimento](#Abilitare_la_scheda_NVIDIA_durante_lo_spegnimento)
    *   [5.3 Monitor multipli](#Monitor_multipli)
        *   [5.3.1 Uscite collegate al chip Intel](#Uscite_collegate_al_chip_Intel)
        *   [5.3.2 Uscite collegate al chip NVIDIA](#Uscite_collegate_al_chip_NVIDIA)
            *   [5.3.2.1 xf86-video-intel-virtual-crtc e hybrid-screenclone](#xf86-video-intel-virtual-crtc_e_hybrid-screenclone)
*   [6 Effettuare lo switch da una scheda integrata all'altra come in Windows](#Effettuare_lo_switch_da_una_scheda_integrata_all.27altra_come_in_Windows)
*   [7 CUDA senza Bumblebee](#CUDA_senza_Bumblebee)
*   [8 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [8.1 [VGL] ERROR: Could not open display :8](#.5BVGL.5D_ERROR:_Could_not_open_display_:8)
    *   [8.2 [ERROR]Cannot access secondary GPU](#.5BERROR.5DCannot_access_secondary_GPU)
        *   [8.2.1 Nessun dispositivo rilevato](#Nessun_dispositivo_rilevato)
        *   [8.2.2 NVIDIA(0): Failed to assign any connected display devices to X screen 0](#NVIDIA.280.29:_Failed_to_assign_any_connected_display_devices_to_X_screen_0)
        *   [8.2.3 Impossibile caricare il driver GPU](#Impossibile_caricare_il_driver_GPU)
        *   [8.2.4 Impossibile inizializzare la scheda NVIDIA su PCI:1:0:0 (GPU non rilevata al BUS)](#Impossibile_inizializzare_la_scheda_NVIDIA_su_PCI:1:0:0_.28GPU_non_rilevata_al_BUS.29)
    *   [8.3 ERROR: ld.so: object 'libdlfaker.so' from LD_PRELOAD cannot be preloaded: ignored](#ERROR:_ld.so:_object_.27libdlfaker.so.27_from_LD_PRELOAD_cannot_be_preloaded:_ignored)
    *   [8.4 Fatal IO error 11 (Risorsa temporaneamente non disponibile) sul server X](#Fatal_IO_error_11_.28Risorsa_temporaneamente_non_disponibile.29_sul_server_X)
    *   [8.5 Video tearing](#Video_tearing)
    *   [8.6 Bumblebee non può collegarsi al Socket](#Bumblebee_non_pu.C3.B2_collegarsi_al_Socket)
*   [9 Ulteriori risorse](#Ulteriori_risorse)

## Bumblebee: Tecnologia Optimus per Linux

La [Tecnologia Optimus](http://www.nvidia.com/object/optimus_technology.html) è un'implementazione *[grafica ibrida](http://hybrid-graphics-linux.tuxfamily.org/index.php?title=Hybrid_graphics)* senza hardware multiplexer. La GPU integrata gestisce il display, mentre la GPU dedicata gestisce il rendering più impegnativo ed invia il risultato alla GPU integrata per la visualizzazione. Quando il portatile è alimentato a batteria, la GPU dedicata si spegne per risparmiare energia e aumentare l'autonomia. É stato anche testato con successo con macchine desktop con grafica Intel integrata e una scheda grafica nVidia dedicata .

Bumblebee è un'implementazione software composta di due parti:

*   Il rendering di programmi off-screen sulla scheda video dedicata e visualizzati sullo schermo utilizzando la scheda video integrata. Questo bridge è fornito da VirtualGL o primus (leggere di seguito) e si connette a un server X avviato per la scheda video dedicata.
*   Disattivare la scheda video dedicata quando non è in uso (si veda il paragrafo [Gestione energetica](#Gestione_energetica)).

Si cerca di imitare il comportamento della tecnologia Optimus, utilizzando la GPU dedicata per il rendering quando necessario e spegnerlo quando non in uso. Le versioni attuali supportano solo il rendering su richiesta, l'avvio automatico di un programma con la scheda video dedicata in base al carico di lavoro non è implementata.

## Installazione

Prima di procedere all'installazione di Bunblebee controllare il vostro BIOS e attivare l'opzione Optimus (nei vecchi computer portatili è chiamato "switchable"), se disponibile (non tutti i BIOS forniscono questa possibilità), e assicurarsi di installare il [driver Intel](/index.php/Intel_(Italiano) "Intel (Italiano)") per la scheda video secondaria.

Sono disponibili diversi pacchetti per un setup completo :

*   [bumblebee](https://www.archlinux.org/packages/?name=bumblebee) - Il pacchetto principale che fornisce il demone e programmi client.
*   (opzionale) [bbswitch](https://www.archlinux.org/packages/?name=bbswitch) (o [bbswitch-dkms](https://www.archlinux.org/packages/?name=bbswitch-dkms)) -Consigliato per il risparmio energetico disabilitando la scheda Nvidia
*   (opzionale ) Se si desidera più di un semplice risparmio energetico, per un rendering di programmi sulla scheda Nvidia dedicata, è inoltre necessario:
    *   Un driver per la scheda Nvidia. Il driver open-source [Nouveau](/index.php/Nouveau_(Italiano) "Nouveau (Italiano)") o il driver proprietario [Nvidia](/index.php/NVIDIA_(Italiano) "NVIDIA (Italiano)"). Vedere la sottosezione.
    *   Un bridge per il rendering e la visualizzazione. Attualmente sono disponibili due pacchetti che sono in grado di farlo, [primus](https://www.archlinux.org/packages/?name=primus) e [virtualgl](https://www.archlinux.org/packages/?name=virtualgl). Solo uno di loro è necessario, ma possono essere installati ugualmente entrambi.

**Note:** Se si desidera eseguire una applicazione a 32 bit su un sistema a 64 bit è necessario installare le opportune librerie lib32-* per il programma. inoltre è necessario anche installare [lib32-virtualgl](https://www.archlinux.org/packages/?name=lib32-virtualgl) o [lib32-primus](https://www.archlinux.org/packages/?name=lib32-primus), in base a cosa avete scelto per effettuare il bridge del rendering. Basta fare in modo di eseguire `primusrun` invece di `optirun` se si decide di utilizzare bridge Primus per il rendering.

### Installare Bumblebee con Intel/Nvidia

*   Installare [mesa](https://www.archlinux.org/packages/?name=mesa), [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel), [bumblebee](https://www.archlinux.org/packages/?name=bumblebee) e [nvidia](https://www.archlinux.org/packages/?name=nvidia).

Se si desidera eseguire applicazioni a 32-bit (come i giochi su wine) su sistemi a 64-bit, è necessario il pacchetto addizionale [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) (e [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) se si intende utilizzare `primusrun`).

**Nota:** Non installare lib32-nvidia-libgl! Bumblebee troverà le giuste librerie lib32 nvidia senza di esso.

### Installare Bumblebee con Intel/Nouveau

Installare:

*   [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) driver sperimentale con accelerazione 3D
*   [mesa](https://www.archlinux.org/packages/?name=mesa) Mesa classic DRI + driver Gallium3D e librerie grafiche Mesa 3-D

## Avviare Bumblebee

Per poter utilizzare Bumblebee è necessario innanzitutto aggiungere il proprio utente (anche altri eventuali utenti) al gruppo Bumblebee:

```
# gpasswd -a $USER bumblebee

```

dove `$USER` è il nome di login dell'utente da aggiungere. Ri-effettuare il login per rendere effettive le modifiche.

**Suggerimento:** Se volete che Bumblebee sia disponibile all'avvio, allora abilitate il servizio di [Systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)") **bumblebeed**.

Ora riavviare il sistema e utilizzare il programma `[optirun](#Utilizzo)` da un terminale per usufruire della tecnologia Optimus NVIDIA per il rendering.

Se si desidera semplicemente disabilitare la scheda nvidia, questo dovrebbe essere tutto ciò che è necessario, oltre ad avere `bbswitch` installato. Il demone bumblebeed, per impostazione predefinita, istruisce bbswitch per spegnere la scheda quando viene avviato. Vedi anche la sezione [Gestione energetica](#Gestione_energetica).

## Utilizzo

La riga di comando programma `optirun` fornito con Bumblebee è il vostro migliore amico per l'esecuzione di applicazioni sulla scheda NVIDIA Optimus.

È possibile testare Bumblebee con questo comando:

```
$ optirun glxgears -info

```

Se il programma viene eseguito con successo e il terminale fornisce informazioni sulla scheda NVIDIA, allora significa che Optimus con Bumblebee è funzionante.

Per avviare un'applicazione utilizzando la scheda grafica dedicata:

```
$ optirun [opzione] *application* [parametri-applicazione]

```

Alcuni esempi:

Avviare applicazioni Windows con Optiumus

```
$ optirun wine *windows application*.exe

```

Utilizzare NVIDIA Settings con Optimus

```
$ optirun -b none nvidia-settings -c :8 

```

Per un elenco di opzioni per `optirun` vedere la sua pagina man.

Un nuovo programma in futuro diventerà la scelta predefinita, poichè apporta migliori prestazioni, vale a dire primus. Attualmente è necessario eseguire il programma a parte (che non accetta le opzioni a differenza di `optirun` ), ma in futuro sarà avviato automaticamente da optirun.

Utilizo:

```
$ primusrun glxgears

```

## Configurazione

È possibile configurare il comportamento di Bumblebee per soddisfare le vostre esigenze. Alcune ottimizzazioni come l'ottimizzazione della velocità, la gestione dell'alimentazione e altre cose possono essere configurate in `/etc/bumblebee/bumblebee.conf`.

### Ottimizzare la velocità quando si utilizza VirtualGL come bridge

Bumblebee gestisce il rendering dei fotogrammi per la scheda NVIDIA Optimus in un server X invisibile con VirtualGL e li trasporta di nuovo al vostro Server X visibile.

I Frames saranno compressi prima di essere trasportati - ciò consente di risparmiare larghezza di banda e può essere utilizzato per l'ottimizzazione della velocità di Bumblebee.

Per usare un metodo di compressione per una singola applicazione:

```
$ optirun -c *metodo-di-comppressione* applicazione

```

I metodi di compressione influiscono sulle prestazioni di utilizzo della CPU/GPU. I metodi compressi (come `jpeg`) caricheranno al massimo la CPU e al minimo possibile la GPU; i metodi non compressi caricheranno più la GPU mentre la CPU avrà il minor carico possibile.

Metodi compressi sono: `jpeg`, `rgb`, `yuv`

Metodi non compressi sono: `proxy`, `xv`

Per impostare un metodo di compressione per tutte le applicazioni impostare il valore `VGLTransport` con il `*metodo-di-compressione*` preferito in `/etc/bumblebee/bumblebee.conf`:

 `/etc/bumblebee/bumblebee.conf` 
```
[...]
[optirun]
VGLTransport=proxy
[...]
```

Si può anche fare in modo che VirtualGL legga i pixel dalla vostra scheda grafica. Impostare la variabile di ambiente `VGL_READBACK` in `pbo` dovrebbe aumentare le prestazioni. In confronto:

```
# PBO dovrebbe essere più veloce
VGL_READBACK=pbo optirun glxspheres
#Il valore predefinito è sync
VGL_READBACK=sync optirun glxspheres

```

**Note:** CPU frequency scaling influisce direttamente sulle prestazioni rendering

### Gestione energetica

L'obiettivo di gestione dell'alimentazione è quello di spegnere la scheda NVIDIA quando non viene utilizzata da nessuna applicazione, e riaccenderla quando è necessario. Se bbswitch è installato, verrà rilevato automaticamente quando si avvia il demone Bumblebee. Nessuna configurazione aggiuntiva è necessaria.

#### Risparmio energetico predefinito della scheda NVIDIA con bbswitch

Il comportamento predefinito di bbswitch è di lasciare lo stato di alimentazione della scheda invariata. `bumblebeed` non fa altro che disabilitare la scheda quando viene avviato, in tal modo, quanto segue è necessario solo se si utilizza bbswitch senza bumblebeed .

Impostare le opzioni dei moduli `load_state` e `unload_state` in base alle vostre esigenze (si veda la [documentazione di bbswitch](https://github.com/Bumblebee-Project/bbswitch)).

 `/etc/modprobe.d/bbswitch.conf`  `options bbswitch load_state=0 unload_state=1` 

#### Abilitare la scheda NVIDIA durante lo spegnimento

La scheda NVIDIA non viene inizializzata correttamente durante la fase di boot se la scheda è stata spenta quando il sistema è stato arrestato l'ultima volta. Una soluzione è impostare l'opzione `TurnCardOffAtExit=false` in `/etc/bumblebee/bumblebee.conf`, tuttavia questo consentirà alla scheda di fermare ogni volta il demone Bumblebee, anche se fatto manualmente. Per assicurare che la scheda NVIDIA rimanga sempre accesa durante l'arresto, aggiungere il seguente servizio di [Systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)") (se state utilizzando [bbswitch](https://www.archlinux.org/packages/?name=bbswitch)):

 `/etc/systemd/system/nvidia-enable.service` 
```
[Unit]
Description=Enable NVIDIA card
DefaultDependencies=no

[Service]
Type=oneshot
ExecStart=/bin/sh -c 'echo ON > /proc/acpi/bbswitch'

[Install]
WantedBy=shutdown.target
```

Per attivare il servizio eseguire `systemctl enable nvidia-enable.service` come root.

### Monitor multipli

#### Uscite collegate al chip Intel

Se la porta (DisplayPort/HDMI/VGA) è collegato al chip Intel, è possibile impostare più monitor con xorg.conf. Si possono impostarli per utilizzare la scheda Intel, ma con Bumblebee è ancora possibile utilizzare la scheda NVIDIA. Un esempio di configurazione, qui di seguito, mostra l'uso di due schermi identici con risoluzione 1080p e con connessione HDMI.

 `/etc/X11/xorg.conf` 
```
Section "Screen"
    Identifier     "Screen0"
    Device         "intelgpu0"
    Monitor        "Monitor0"
    DefaultDepth    24
    Option         "TwinView" "0"
    SubSection "Display"
        Depth          24
        Modes          "1980x1080_60.00"
    EndSubSection
EndSection

Section "Screen"
    Identifier     "Screen1"
    Device         "intelgpu1"
    Monitor        "Monitor1"
    DefaultDepth   24
    Option         "TwinView" "0"
    SubSection "Display"
        Depth          24
        Modes          "1980x1080_60.00"
    EndSubSection
EndSection

Section "Monitor"
    Identifier     "Monitor0"
    Option         "Enable" "true"
EndSection

Section "Monitor"
    Identifier     "Monitor1"
    Option         "Enable" "true"
EndSection

Section "Device"
    Identifier     "intelgpu0"
    Driver         "intel"
    Option         "XvMC" "true"
    Option         "UseEvents" "true"
    Option         "AccelMethod" "UXA"
    BusID          "PCI:0:2:0"
EndSection

Section "Device"
    Identifier     "intelgpu1"
    Driver         "intel"
    Option         "XvMC" "true"
    Option         "UseEvents" "true"
    Option         "AccelMethod" "UXA"
    BusID          "PCI:0:2:0"
EndSection

Section "Device"
    Identifier "nvidiagpu1"
    Driver "nvidia"
    BusID "PCI:0:1:0"
EndSection
```

Probabilmente sarà necessario cambiare il BusID in base alle vostre esigenze sia per la Intel e la scheda Nvidia.

 `$ lspci | grep VGA` 
```
00:02.0 VGA compatible controller: Intel Corporation 2nd Generation Core Processor Family Integrated Graphics Controller (rev 09)

```

In questo esempio il BusID è 0:2:0

#### Uscite collegate al chip NVIDIA

Su alcuni notebook, l'uscita video digitale ( HDMI o DisplayPort ) è cablato al chip NVIDIA. Se si desidera utilizzare tutti i display su un tale sistema simultaneamente, è necessario eseguire due server X. La prima prevede di utilizzare il driver Intel per il pannello notebook e un display collegato a VGA. Il secondo sarà avviato attraverso optirun sulla scheda NVIDIA, e al driver per il display digitale.

Attualmente ci sono diverse istruzioni sul web come una tale impostazione può essere fatta funzionare. Uno può essere trovato sul [wiki](https://github.com/Bumblebee-Project/Bumblebee/wiki/Multi-monitor-setup) di Bumblebee. Un altro approccio è descritto in seguito.

##### xf86-video-intel-virtual-crtc e hybrid-screenclone

Questo metodo utilizza un driver patchato Intel, che viene esteso per avere un display virtuale, e il programma hybrid-screenclone che viene utilizzato per copiare il display sopra un display virtuale un secondo server X, che è in esecuzione sulla scheda NVIDIA utilizzando Optirun. Merito va ai [Triple-head monitors on a Thinkpad T520](http://judsonsnotes.com/notes/index.php?option=com_content&view=article&id=673:triple-head-monitors-on-thinkpad-t520&catid=37:tech-notes&Itemid=59) che ha una spiegazione dettagliata di come questo viene fatto su un sistema Ubuntu.

Per semplicità, DP viene utilizzato per riferirsi al Digital Output (DisplayPort) . Le istruzioni devono essere uguali se invece il notebook dispone di una porta HDMI.

*   Impostare il sistema in modo da utilizzare esclusivamente la scheda NVIDIA, test combinato DP/Monitor e generare un file `xorg.nvidia.conf`. Questo passaggio non è obbligatorio, ma consigliato se il vostro BIOS di sistema ha la possibilità di cambiare la grafica in modalità NVIDIA-only. Per fare questo, prima disinstallare il pacchetto di Bumblebee e installare solo il driver NVIDIA. Successivamente riavviare, entrare nel BIOS e cambiare la modalità grafica in NVIDIA-only. Quando si ritorna in Arch, collegare il monitor sulla porta DP e utilizza startx per verificare se si sta lavorando correttamente. Usare `Xorg -configure` per generare un file xorg.conf per la scheda NVIDIA. Questo sarà utile più avanti.

*   Reinstallare bumlbebee e bbswitch, riavviare ed impostare la modalità grafica nel BIOS in Hybrid.
*   Installare [xf86-video-intel-virtual-crtc](https://aur.archlinux.org/packages/xf86-video-intel-virtual-crtc/), e sostituirlo al proprio pacchetto xf86-video-intel.
*   Scaricare [hybrid-screenclone](https://github.com/liskin/hybrid-screenclone) e compilarlo utilizzando "make".
*   Modificare queste impostazioni inbumblebee.conf:

 `/etc/bumblebee/bumblebee.conf` 
```
KeepUnusedXServer=true
Driver=nvidia
```

**Nota:** Lasciare il parametro PMMethod impostato su "bumblebee". Questo è in contrasto con le istruzioni legate nell'articolo sopra, ma su Arch Linux deve essere lasciato è necessaria in modo che il modulo bbswitch venga caricato automaticamente con queste opzioni.

*   Copiare il file `xorg.conf` generato in precedenza nello step1 in `/etc/X11` (es. `/etc/X11/xorg.nvidia.conf`). Nella sezione [driver-nvidia] di `bumblebee.conf`, cambiare il parametro `XorgConfFile` in modo che punti ad esso.
*   Testare che la configurazione `/etc/X11/xorg.nvidia.conf` sia funzionante con `startx -- -config /etc/X11/xorg.nvidia.conf`
*   Affinché il vostro DP Monitor si presentarsi con la risoluzione corretta nel display virtuale, potrebbe essere necessario modificare la sezione `Monitor` nel file `/etc/xorg.nvidia.conf`. Dal momento che questo è un lavoro extra, si potrebbe provare a continuare con il file generato automaticamente. Tornare a questo passo delle istruzioni se si scopre che la risoluzione del display virtuale, come mostrato da xrandr, non è corretto .
    *   Prima di tutto dovete generare una `Modeline`. Potete usare il tool [amlc](http://amlc.berlios.de/),che genearte una Modeline se si introduce alcuni parametri di base.

	Esempio: 24" 1920x1080 Monitor

	Avviare il tool con `amlc -c`

```
Monitor Identifier: Samsung 2494
Aspect Ratio: 2
physical size[cm]: 60
Ideal refresh rate, in Hz: 60
min HSync, kHz: 40
max HSync, kHz: 90
min VSync, Hz: 50
max VSync, Hz: 70
max pixel Clock, MHz: 400
```

Questa è la sezione Monitor che `amlc` generato per questo ingresso:

```
Section "Monitor"
    Identifier     "Samsung 2494"
    ModelName      "Generated by Another Modeline Calculator"
    HorizSync      40-90
    VertRefresh    50-70
    DisplaySize    532 299  # Aspect ratio 1.778:1
    # Custom modes
    Modeline "1920x1080" 174.83 1920 2056 2248 2536 1080 1081 1084 1149             # 174.83 MHz,  68.94 kHz,  60.00 Hz
EndSection  # Samsung 2494
```

Cambiare `xorg.nvidia.conf` per includere questa sezione Monitor. È anche possibile tagliare il vostro file in modo che contenga solo ServerLayout, Monitor Device e sezioni Screen. Per riferimento eccovi un esempio:

 `/etc/X11/xorg.nvidia.conf` 
```
Section "ServerLayout"
        Identifier     "X.org Nvidia DP"
        Screen      0  "Screen0" 0 0
        InputDevice    "Mouse0" "CorePointer"
        InputDevice    "Keyboard0" "CoreKeyboard"
EndSection

Section "Monitor"
    Identifier     "Samsung 2494"
    ModelName      "Generated by Another Modeline Calculator"
    HorizSync      40-90
    VertRefresh    50-70
    DisplaySize    532 299  # Aspect ratio 1.778:1
    # Custom modes
    Modeline "1920x1080" 174.83 1920 2056 2248 2536 1080 1081 1084 1149             # 174.83 MHz,  68.94 kHz,  60.00 Hz
EndSection  # Samsung 2494

Section "Device"
        Identifier  "DiscreteNvidia"
        Driver      "nvidia"
        BusID       "PCI:1:0:0"
EndSection

Section "Screen"
        Identifier "Screen0"
        Device     "DiscreteNvidia"
        Monitor    "Samsung 2494"
        SubSection "Display"
                Viewport   0 0
                Depth     24
        EndSubSection
EndSection

```

*   Collegare entrambi i monitor esterni e avviare con startx. Controllare il proprio `/var/log/Xorg.0.log`. Verificare che il monitor VGA venga rilevato con le modalità corrette. Si dovrebbe anche vedere un uscita VIRTUAL mostrata con una propria modalità.
*   Avviare `xrandr` e i tre display dovrebbe essere incluso lì, insieme con le modalità supportate.
*   Se i Modelines elencati per il vostro display virtuale non presenta la risoluzione nativa del proprio monitor, prendere nota del nome esatto dell'uscita. Ad esempio `VIRTUAL1`. Successivamente ricontrollate il file `Xorg.0.log`. Si dovrebbe vedere un messaggio del tipo: *Output VIRTUAL1 has no monitor section*. Cambieremo questo mettendo un file con la sezione Monitor necessaria in `/etc/X11/xorg.conf.d`. Poi usciremo e riavvieremo X.

 `/etc/X11/xorg.conf.d/20-monitor_samsung.conf` 
```
Section "Monitor"
    Identifier     "VIRTUAL1"
    ModelName      "Generated by Another Modeline Calculator"
    HorizSync      40-90
    VertRefresh    50-70
    DisplaySize    532 299  # Aspect ratio 1.778:1
    # Custom modes
    Modeline "1920x1080" 174.83 1920 2056 2248 2536 1080 1081 1084 1149             # 174.83 MHz,  68.94 kHz,  60.00 Hz
EndSection  # Samsung 2494

```

*   Accendere la scheda NVIDIA eseguendo: `sudo tee /proc/acpi/bbswitch <<< ON`
*   Avviare un altro server X per il monitor collegato alla DisplayPort: `sudo optirun true`
*   Conrollare il file di log per il secondo server X in `/var/log/Xorg.8.log`
*   Eseguire xrandr per impostare il display VIRTUAL con la giusta dimensione ed il corretto posizionamento, ad esempio: `xrandr --output VGA1 --auto --rotate normal --pos 0x0 --output VIRTUAL1 --mode 1920x1080 --right-of VGA1 --output LVDS1 --auto --rotate normal --right-of VIRTUAL1`
*   Prendere nota della posizione del display VIRTUAL nella lista delle uscite mostrata da xrandr. Il conteggio parte da zer , vale a dire che se il terzo display è mostrato, è necessario specificare `-x 2` come parametro per `screenclone`
*   Clonare il contenuto del display VIRTUAL dentro il server X creato da Bumblebee, che è collegato al monitor tramite DisplayPort ed il chip NVIDIA : `screenclone -d :8 -x 2`

Ecco fatto, tutti e tre gli schermi dovrebbero ora essere funzionanti.

## Effettuare lo switch da una scheda integrata all'altra come in Windows

Su Windows, Nvidia Optimus funziona in maniera tale che è possibile avere una whitelist di applicazioni che richiedono l'utilizzo di Optimus, ed è anche possibile aggiungere le applicazioni in questa whitelist se necessario. Quando si avvia l'applicazione, viene deciso automaticamente quale scheda video usare.

Per imitare questo comportamento in Linux , è possibile utilizzare [libgl-switcheroo-git](https://aur.archlinux.org/packages/libgl-switcheroo-git/). Dopo l'installazione, è possibile aggiungere quanto segue in basso nel vostro `.Xprofile`:

 `~/.xprofile` 
```
mkdir -p /tmp/libgl-switcheroo-$USER/fs
gtkglswitch &
libgl-switcheroo /tmp/libgl-switcheroo-$USER/fs &
```

A tal fine, è necessario aggiungere quanto segue alla shell da cui si intende avviare le applicazioni (ho semplicemente aggiungerlo al file .xprofile)

```
export LD_LIBRARY_PATH=/tmp/libgl-switcheroo-$USER/fs/\$LIB${LD_LIBRARY_PATH+:}$LD_LIBRARY_PATH

```

Una volta che questo è stato fatto tutto , ogni applicazione che si avvia da questo shell aprirà una finestra GTK chiedendo con quale scheda si desidera eseguire (potete anche aggiungere un programma alla whitelist nella configurazione). La configurazione si trova in `$ XDG_CONFIG_HOME/libgl-switcheroo.conf`, di solito `~/.config/libgl-switcheroo.conf`.

## CUDA senza Bumblebee

Non vi è una chiara documentazione in proposito, ma non è necessario che Bumblebee utilizzi CUDA e può funzionare anche su macchine in cui non riesce optirun. Per una guida su come farlo funzionare con il Lenovo IdeaPad Y580 (che utilizza il GeForce 660M), si veda: [Lenovo IdeaPad Y580#NVIDIA_Card](/index.php/Lenovo_IdeaPad_Y580#NVIDIA_Card "Lenovo IdeaPad Y580") . Queste istruzioni molto probabilmente funzioneranno anche con altre macchine (ad eccezione della parte acpi-manico-hack , che non può essere tralasciata).

## Risoluzione dei problemi

**Note:** Si prega di riportare i bugs al [Bumblebee-Project](https://github.com/Bumblebee-Project/Bumblebee) il GitHub tracker come descritto nel [Wiki](https://github.com/Bumblebee-Project/Bumblebee/wiki/Reporting-Issues).

### [VGL] ERROR: Could not open display :8

Esiste un problema noto con alcune applicazioni che vengono lanciate con wine che si biforcano e uccidono il processo padre senza tenere traccia del problema (per esempio la sessione libera di gioco on-line di "Runes of Magic").

Questo è un problema noto con VirtualGL . Come con bumblebee 3.1, fintanto che lo avete installato, è possibile utilizzare Primus come ponte di rendering :

```
$ optirun -b primus wine *windows program*.exe

```

Se questo non funziona, una soluzione alternativa a questo problema è quanto segue:

```
$ optirun bash
$ optirun wine *windows program*.exe

```

Se state utilizzando il driver NVIDA, una soluzione a questo problema è quello di modificare `/etc/bumblebee/xorg.conf.nvidia` e cambiare l'opzione `ConnectedMonitor` su `CRT-0`.

### [ERROR]Cannot access secondary GPU

#### Nessun dispositivo rilevato

In alcuni casi, l'esecuzione di optirun ritorna il seguente errore:

```
[ERROR]Cannot access secondary GPU - error: [XORG] (EE) No devices detected.
[ERROR]Aborting because fallback start is disabled.

```

In questo caso sarà necessario spostare il file `/etc/X11/xorg.conf.d/20-intel.conf` da qualche altra parte, o rimuoverlo se non utilizzato. Riavviare il demone bumblebeed e l'errore non dovrebbe più ripresentarsi. Se si ha bisogno di modificare alcune caratteristiche su modulo Intel , una soluzione è spostare il vostro `/etc/X11/xorg.conf.d/20-intel.conf` in `/etc/X11/xorg.conf`.

Potrebbe anche essere necessario commentare la linea riguardante il driver nel file `/etc/X11/xorg.conf.d/10-monitor.conf`.

Se si sta utilizzando il driver nouveau si potrebbe provare a passare al driver nVidia.

Potrebbe essere necessario definire la scheda nvidia da qualche parte, (ad esempio un file in `/etc/X11/xorg.conf.d`), e ricordarsi di cambiare il BusID usando lspci.

```
Section "Device"
    Identifier "nvidiagpu1"
    Driver "nvidia"
    BusID "PCI:0:1:0"
EndSection

```

#### NVIDIA(0): Failed to assign any connected display devices to X screen 0

Se ottenete un errore simile nella console:

```
[ERROR]Cannot access secondary GPU - error: [XORG] (EE) NVIDIA(0): Failed to assign any connected display devices to X screen 0
[ERROR]Aborting because fallback start is disabled.

```

Potete cambiare questa linea in `/etc/bumblebee/xorg.conf.nvidia` da:

```
Option "ConnectedMonitor" "DFP"

```

a

```
Option "ConnectedMonitor" "CRT"

```

#### Impossibile caricare il driver GPU

Se l'output della console è :

```
[ERROR]Cannot access secondary GPU - error: Could not load GPU driver

```

e tentando di caricare il modulo nvidia si ottiene :

```
modprobe nvidia
modprobe: ERROR: could not insert 'nvidia': Exec format error

```

Si dovrebbe provare a compilare manualmente i pacchetti nvidia per il vostro kernel.

```
yaourt -Sb nvidia

```

Questo dovrebbe correggere l'errore

#### Impossibile inizializzare la scheda NVIDIA su PCI:1:0:0 (GPU non rilevata al BUS)

Si può provare ad aggiungere `rcutree.rcu_idle_gp_delay=1` nel parametro `GRUB_CMDLINE_LINUX_DEFAULT` presente in `/etc/default/grub` (ricordarsi rigenerare il file di grub con `# grub-mkconfig -o /boot/grub/grub.cfg`). Questo problema è stato discusso [qui](https://bbs.archlinux.org/viewtopic.php?id=169742).

### ERROR: ld.so: object 'libdlfaker.so' from LD_PRELOAD cannot be preloaded: ignored

Probabilmente si desidera avviare una applicazione a 32 bit con bumblebee su un sistema a 64 bit. Si veda la "nota" nella sezione [Installazione](#Installazione)

### Fatal IO error 11 (Risorsa temporaneamente non disponibile) sul server X

Cambiare `KeepUnusedXServer` in `/etc/bumblebee/bumblebee.conf` da `false` a `true`. Bumblebee non era in grado di riconoscere i vostri programmi forzati in background.

### Video tearing

Problemi di tearing video sono piuttosto comuni utilizzando Bumblebee. Per risolvere il problema, è necessario attivare `vsync`. Dovrebbe essere abilitato per impostazione predefinita sulla scheda Intel, ma verificarlo dai log di Xorg. Per verificare se sia o non sia abilitato per nvidia, eseguire:

```
$ optirun nvidia-settings -c :8

```

Le voci `X Server XVideo Setings -> Sync to VBlank` e `OpenGL Settings -> Sync to VBlank` dovrebbero essere entrambi attivati. La scheda Intel ha in generale meno problemi di tearing, in questo modo potrebbe essere utilizzata per la riproduzione video. In particolare utilizzando VA-API per la decodifica video (ad esempio `mplayer-vaapi` e con il parametro `-vsync`). Fare riferimento all'articolo [Intel](/index.php/Intel_(Italiano)#Video_tearing "Intel (Italiano)") su come risolvere i problemi di tearing sulla scheda Intel. Se non è ancora risolto, provate a disabilitare il compositing dal proprio ambiente desktop. Una ulteriore soluzione , potrebbe essere quella di disabilitare il triple buffering.

### Bumblebee non può collegarsi al Socket

Si potrebbe ottenere qualcosa di simile:

 `$ optirun glxspheres` 
```
[ 1648.179533] [ERROR]You've no permission to communicate with the Bumblebee daemon. Try adding yourself to the 'bumblebee' group
[ 1648.179628] [ERROR]Could not connect to bumblebee daemon - is it running?

```

Se siete già nel gruppo `bumblebee` (`$ groups | grep bumblebee`), si può provare a [rimuovere il socket](https://bbs.archlinux.org/viewtopic.php?pid=1178729#p1178729) `/var/run/bumblebeed.socket`.

## Ulteriori risorse

*   [Bumblebee Project repository](http://www.bumblebee-project.org)
*   [Bumblebee Project Wiki](http://wiki.bumblebee-project.org/)
*   [Bumblebee Project bbswitch repository](https://github.com/Bumblebee-Project/bbswitch)

Potete unirvi al canale #bumblebee su freenode.net