Articoli correlati

*   [Nouveau](/index.php/Nouveau_(Italiano) "Nouveau (Italiano)")
*   [Bumblebee](/index.php/Bumblebee_(Italiano) "Bumblebee (Italiano)")
*   [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus")
*   [Xorg](/index.php/Xorg_(Italiano) "Xorg (Italiano)")

Questo articolo tratta dell'installazione e configurazione dei driver proprietari per schede grafiche [NVIDIA](http://www.nvidia.com). Si veda [Nouveau](/index.php/Nouveau "Nouveau") per le informazioni sui driver open-source. Si consulti invece l'articolo [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus") se disponete di un portatile che sfrutta questa tecnologia.

## Contents

*   [1 Installazione](#Installazione)
    *   [1.1 Installazione alternativa: kernel personalizzato](#Installazione_alternativa:_kernel_personalizzato)
    *   [1.2 Ri-compilazione automatica del modulo NVIDIA ad ogni aggiornamento su qualsiasi kernel](#Ri-compilazione_automatica_del_modulo_NVIDIA_ad_ogni_aggiornamento_su_qualsiasi_kernel)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Configurazione minimale](#Configurazione_minimale)
    *   [2.2 Configurazione automatica](#Configurazione_automatica)
    *   [2.3 Monitor multipli](#Monitor_multipli)
        *   [2.3.1 TwinView](#TwinView)
            *   [2.3.1.1 Configurazione manuale in CLI tramite xrandr](#Configurazione_manuale_in_CLI_tramite_xrandr)
        *   [2.3.2 Utilizzare NVIDIA Settings](#Utilizzare_NVIDIA_Settings)
        *   [2.3.3 ConnectedMonitor](#ConnectedMonitor)
        *   [2.3.4 Modalità Mosaico](#Modalit.C3.A0_Mosaico)
            *   [2.3.4.1 Base Mosaic](#Base_Mosaic)
            *   [2.3.4.2 SLI Mosaic](#SLI_Mosaic)
*   [3 Tweaking](#Tweaking)
    *   [3.1 GUI: nvidia-settings](#GUI:_nvidia-settings)
    *   [3.2 Avanzato: 20-nvidia.conf](#Avanzato:_20-nvidia.conf)
        *   [3.2.1 Abilitare la desktop composition](#Abilitare_la_desktop_composition)
        *   [3.2.2 Disabiliare visione logo all'avvio](#Disabiliare_visione_logo_all.27avvio)
        *   [3.2.3 Abilitare accelerazione hardware](#Abilitare_accelerazione_hardware)
        *   [3.2.4 Annullare la ricerca del monitor](#Annullare_la_ricerca_del_monitor)
        *   [3.2.5 Abilitare il triple buffering](#Abilitare_il_triple_buffering)
        *   [3.2.6 Usare gli eventi di sistema](#Usare_gli_eventi_di_sistema)
        *   [3.2.7 Abilitare il risparmio energetico](#Abilitare_il_risparmio_energetico)
        *   [3.2.8 Abilitare il controllo della luminosità](#Abilitare_il_controllo_della_luminosit.C3.A0)
        *   [3.2.9 Abilitare la modalità SLI](#Abilitare_la_modalit.C3.A0_SLI)
        *   [3.2.10 Forzare il livello di performance Powermizer (per portatili)](#Forzare_il_livello_di_performance_Powermizer_.28per_portatili.29)
            *   [3.2.10.1 Lasciare che la GPU imposti automaticamente il livello di performance (basato sulla temperatura)](#Lasciare_che_la_GPU_imposti_automaticamente_il_livello_di_performance_.28basato_sulla_temperatura.29)
        *   [3.2.11 Disabilitare i *vblank interrupts* (per portatili)](#Disabilitare_i_vblank_interrupts_.28per_portatili.29)
        *   [3.2.12 Abilitare l'overclocking](#Abilitare_l.27overclocking)
            *   [3.2.12.1 Impostare un clock statico 2D/3D](#Impostare_un_clock_statico_2D.2F3D)
*   [4 Trucchi e consigli](#Trucchi_e_consigli)
    *   [4.1 Aggiustare la Risoluzione del terminale di avvio](#Aggiustare_la_Risoluzione_del_terminale_di_avvio)
    *   [4.2 Abilitare Video HD (VDPAU/VAAPI)](#Abilitare_Video_HD_.28VDPAU.2FVAAPI.29)
    *   [4.3 Evitare screen tearing in KDE (KWin)](#Evitare_screen_tearing_in_KDE_.28KWin.29)
    *   [4.4 Accelerazione hardware con il codec video XvMC](#Accelerazione_hardware_con_il_codec_video_XvMC)
    *   [4.5 Usare l'uscita TV](#Usare_l.27uscita_TV)
    *   [4.6 X con la TV (DFP) come unico display](#X_con_la_TV_.28DFP.29_come_unico_display)
    *   [4.7 Controllare l'alimentazione](#Controllare_l.27alimentazione)
    *   [4.8 Visualizzare la temperatura GPU nella shell](#Visualizzare_la_temperatura_GPU_nella_shell)
        *   [4.8.1 Metodo 1 - nvidia-settings](#Metodo_1_-_nvidia-settings)
        *   [4.8.2 Metodo 2 - nvidia-smi](#Metodo_2_-_nvidia-smi)
        *   [4.8.3 Metodo 3 - nvclock](#Metodo_3_-_nvclock)
    *   [4.9 Impostare la velocità della ventola al Login](#Impostare_la_velocit.C3.A0_della_ventola_al_Login)
    *   [4.10 Ordine di installazione/disinstallazione al cambiamento dei driver](#Ordine_di_installazione.2Fdisinstallazione_al_cambiamento_dei_driver)
    *   [4.11 Passare tra i driver nvidia e nouveau](#Passare_tra_i_driver_nvidia_e_nouveau)
*   [5 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [5.1 Performance scadenti, es. ridisegno lento quando si passa tra le schede in Chrome](#Performance_scadenti.2C_es._ridisegno_lento_quando_si_passa_tra_le_schede_in_Chrome)
    *   [5.2 Giocare usando Twinview](#Giocare_usando_Twinview)
    *   [5.3 Vertical sync using TwinView](#Vertical_sync_using_TwinView)
    *   [5.4 Vecchie impostazioni Xorg](#Vecchie_impostazioni_Xorg)
    *   [5.5 Schermata corrotta: il problema dei "Sei schermi"](#Schermata_corrotta:_il_problema_dei_.22Sei_schermi.22)
    *   [5.6 Errore '/dev/nvidia0' Input/Output](#Errore_.27.2Fdev.2Fnvidia0.27_Input.2FOutput)
    *   [5.7 Errori '/dev/nvidiactl'](#Errori_.27.2Fdev.2Fnvidiactl.27)
    *   [5.8 Le applicazioni 32 bit non si avviano](#Le_applicazioni_32_bit_non_si_avviano)
    *   [5.9 Errori dopo l'aggiornamento del kernel](#Errori_dopo_l.27aggiornamento_del_kernel)
    *   [5.10 Crash generali](#Crash_generali)
    *   [5.11 Brutte performance dopo aver installato una nuova versione dei driver](#Brutte_performance_dopo_aver_installato_una_nuova_versione_dei_driver)
    *   [5.12 Picchi alti di CPU con schede della serie 400](#Picchi_alti_di_CPU_con_schede_della_serie_400)
    *   [5.13 Per i laptop: X si blocca durante il login/out, ovviato con Ctrl+Alt+Backspace](#Per_i_laptop:_X_si_blocca_durante_il_login.2Fout.2C_ovviato_con_Ctrl.2BAlt.2BBackspace)
    *   [5.14 La frequenza di refresh non viene rilevata correttamente dalle utility dipendenti da XRandR](#La_frequenza_di_refresh_non_viene_rilevata_correttamente_dalle_utility_dipendenti_da_XRandR)
    *   [5.15 Nessun schermo trovato su un computer portatile e Nvidia Optimus](#Nessun_schermo_trovato_su_un_computer_portatile_e_Nvidia_Optimus)
        *   [5.15.1 Possibile Soluzione](#Possibile_Soluzione)
    *   [5.16 Schermo(i) trovati, ma nessuna configurazione utilizzabile](#Schermo.28i.29_trovati.2C_ma_nessuna_configurazione_utilizzabile)
    *   [5.17 Nessun controllo della luminosità sui portatili](#Nessun_controllo_della_luminosit.C3.A0_sui_portatili)
    *   [5.18 Barre nere durante la riproduzione a schermo intero di video flash con la configurazione Twinview](#Barre_nere_durante_la_riproduzione_a_schermo_intero_di_video_flash_con_la_configurazione_Twinview)
    *   [5.19 La retroilluminazione non si spegne in alcune circostanze](#La_retroilluminazione_non_si_spegne_in_alcune_circostanze)
    *   [5.20 Colori blu su video che utilizzano Flash](#Colori_blu_su_video_che_utilizzano_Flash)
    *   [5.21 Bleeding Overlay con Flash](#Bleeding_Overlay_con_Flash)
    *   [5.22 Il sistema si blocca completamente utilizzando Flash](#Il_sistema_si_blocca_completamente_utilizzando_Flash)
    *   [5.23 Xorg fallisce il caricamento o appare una schermata rossa](#Xorg_fallisce_il_caricamento_o_appare_una_schermata_rossa)
    *   [5.24 Schermo nero su sistemi con GPU integrate Intel](#Schermo_nero_su_sistemi_con_GPU_integrate_Intel)
    *   [5.25 Schermo nero su sistemi con GPU integrata VIA](#Schermo_nero_su_sistemi_con_GPU_integrata_VIA)
    *   [5.26 X fallisce con "no screens found" una Intel iGPU](#X_fallisce_con_.22no_screens_found.22_una_Intel_iGPU)
    *   [5.27 Xorg non fallisce durante l'avvio , ma il sistema si avvia comunque](#Xorg_non_fallisce_durante_l.27avvio_.2C_ma_il_sistema_si_avvia_comunque)
*   [6 Link esterni](#Link_esterni)

## Installazione

Queste istruzioni sono per gli utenti che usano il pacchetto stock [linux](https://www.archlinux.org/packages/?name=linux). Per kernel personalizzati si veda [il prossimo passaggio](#Installazione_alternativa:_kernel_personalizzato).

**Suggerimento:** E' consigliato l'utilizzo di [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)") per l'installazione dei driver NVIDIA rispetto al pacchetto fornito dal sito NVIDIA, questo permette che i driver vengano aggiornati assieme al resto del sistema

1\. Se non conoscete la scheda grafica che state utilizzando, potete scoprirlo mediante il comando:

	 ` # lspci -k | grep -A 2 -i "VGA"` 

2\. Determinare il driver necessario per la vostra scheda video visitando il sito NVIDIA nella pagina dei [download dei driver](http://www.nvidia.com/Download/index.aspx?lang=it) guardando il nome del driver NVIDIA. Potete anche controllare [questa lista](http://www.nvidia.com/object/IO_32667.html) per le vecchie schede o cercare il codice del nome nella [pagina dei nomi dei codici sul wiki di nouveau](http://nouveau.freedesktop.org/wiki/CodeNames).}}

3\. Installare il driver appropriato per la propria scheda:

*   Per schede serie GeForce 8 e superiori [NV50 e nuovi], installare il pacchetto [nvidia](https://www.archlinux.org/packages/?name=nvidia) disponibile nei [repositori ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").
*   Per schede serie GeForce 6/7 e superiori [[NV40-NV50], installare il pacchetto [nvidia-304xx](https://www.archlinux.org/packages/?name=nvidia-304xx) disponibile nei [repositori ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").
*   Per schede serie GeForce 5 FX [NV30-NV38], installare il pacchetto [nvidia-173xx](https://aur.archlinux.org/packages/nvidia-173xx/), disponibile su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").
*   Per schede serie GeForce2/3/4 MX/Ti [NV11 and NV17-NV28], installare il pacchetto [nvidia-96xx](https://aur.archlinux.org/packages/nvidia-96xx/), disponibile su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").

	Per i modelli GPU più recenti, può essere necessario installare [nvidia-beta](https://aur.archlinux.org/packages/nvidia-beta/) da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") , dal momento che i driver stabili potrebbero non supportare le nuove funzionalità introdotte . Provare prima quelli stabili.

	Se siete in ambiente a 64-bit e necessitate del supporto OpenGL a 32-bit, sarà necessario installare il pacchetto *lib32* equivalente dal deposito [multilib](/index.php/Multilib "Multilib") (per esempio [lib32-nvidia-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-libgl) o *lib32-nvidia-{304xx,173xx,96xx}-utils*).}}

**Suggerimento:** I driver legacy nvidia-96xx e nvidia-173xx possono essere anche installati dal deposito non ufficiale [[city]](http://pkgbuild.com/~bgyorgy/city.html).

4\. Riavviare. Il pacchetto [nvidia](https://www.archlinux.org/packages/?name=nvidia) contiene un file che mette in blacklist il modulo `nouveau`. Un riavvio del sistema risulta necessario perché questo procedimento abbia effetto.

Una volta terminata l'installazione, si prosegua con la [configurazione](#Configurazione).

### Installazione alternativa: kernel personalizzato

Per prima cosa potrebbe essere utile sapere come funziona il sistema [ABS](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)"), leggendo alcuni articoli al riguardo:

*   Articolo principale di [ABS](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)")
*   Articolo su [makepkg](/index.php/Makepkg_(Italiano) "Makepkg (Italiano)")
*   Articolo su [Creazione pacchetti](/index.php/Creating_packages_(Italiano) "Creating packages (Italiano)")

**Nota:** É presente anche il pacchetto [nvidia-all](https://aur.archlinux.org/packages/nvidia-all/) reperibile su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") che risulta più semplice da utilizzare con kernel personalizzati e/o multipli.

Quello che segue è un piccolo tutorial per la creazione di un pacchetto di driver NVIDIA personalizzato utilizzando ABS:

[Installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") il pacchetto [abs](https://www.archlinux.org/packages/?name=abs) e generare l'albero con:

```
# abs

```

Utilizzando un utente non privilegiato, si crei una cartella temporanea per la creazione del nuovo pacchetto:

```
$ mkdir -p ~/devel/abs

```

Si copi la cartella del pacchetto `nvidia` :

```
$ cp -r /var/abs/extra/nvidia/ ~/devel/abs/

```

Ci si sposti nella cartella di compilazione `nvidia` temporanea:

```
$ cd ~/devel/abs/nvidia

```

E' ora necessario modificare i file `nvidia.install` e `PKGBUILD` in modo che le variabili riportino la giusta versione del kernel.

Utilizzando un kernel personalizzato, si ottengano la giusta versione kernel e locale:

```
$ uname -r

```

1.  Nel file `nvidia.install` si sostituisca la variabile `EXTRAMODULES='extramodules-3.4-ARCH'` con la versione del kernel personalizzato, come `EXTRAMODULES='extramodules-3.4.4'` oppure `EXTRAMODULES='extramodules-3.4.4-custom'` a seconda della versione del kernel e il testo/numero di quella locale. Si ripeta poi l'operazione per tutte le occorrenze in questo file.

1.  Nel file `PKGBUILD` si cambi la variabile `_extramodules=extramodules-3.4-ARCH` in modo che corrisponda alla corretta versione, allo stesso modo del passaggio precedente.

3\. Se ci sono più di un kernel installati in parallelo sullo stesso sistema, (come un kernel personalizzato a fianco al kernel -ARCH di default) si cambi la variabile `"pkgname=nvidia"` nel file `PKGBUILD` con un nuovo unico identificativo, come `"pkgname=nvidia-344"` o `"pkgname=nvidia-custom"`. Questo permetterà ad entrambi i kernel di utilizzare il modulo nvidia dal momento che il pacchetto del modulo personalizzato avrà un nome differente e non sovrascriverà l'originale. Si avrà bisogno anche di commentare la riga in `package()` che mette in blacklist il modulo nouveau in `/usr/lib/modprobe.d/nvidia.conf` (non c'è bisogno di ripeterlo).

Si esegua poi:

```
$ makepkg -c -i

```

L'operando `-c` dice a makepkg di eliminare i file residui del processo di pacchettizzazione dopo la creazione del pacchetto, mentre `-i` farà in modo che makepkg esegua automaticamente pacman per installarlo.

### Ri-compilazione automatica del modulo NVIDIA ad ogni aggiornamento su qualsiasi kernel

Questo è possibile grazie al pacchetto [nvidia-hook](https://aur.archlinux.org/packages/nvidia-hook/) da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)"). Sarà necessario installare i sorgenti del modulo: o [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms) per i driver stabili. In **nvidia-hook**, la funzionalità per la 'ri-compilazione automatica' è garantita da un **nvidia hook** su [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") dopo aver forzato l'aggiornamento del pacchetto **linux-headers**. Avrete bisogno di aggiungere `nvidia` tra gli HOOK in `/etc/mkinitcpio.conf`.

L'Hook chiamerà il comando **dkms** per aggiornare il modulo NVIDIA per la versione del nuovo kernel .

**Nota:**

*   Se si utilizza questa funzionalità è **importante** controllare l'output del processo di installazione del pacchetto Linux ( o qualsiasi altro kernel ). L'hook nvidia segnalerà se qualcosa andasse storto.

*   Se si desidera eseguire questa operazione manualmente si prega di vedere questa sezione [nella pagina wiki di dkms.](/index.php/Dynamic_Kernel_Module_Support#Usage "Dynamic Kernel Module Support")}}

## Configurazione

E' possibile che dopo l'installazione dei driver non sia necessario creare un file di configurazione per il server Xorg, si può verificare il corretto funzionamento del server Xorg senza un file di configurazione. Tuttavia può essere necessario creare un file di configurazione ( è preferibilre creare il file `/etc/X11/xorg.conf.d/20-nvidia.conf` al posto di `/etc/X11/xorg.conf`) in modo da poter modificare varie impostazioni. Questa configurazione può essere generata dal tool di configurazione Xorg NVIDIA, o può essere creato manualmente. Se creato manualmente possiamo creare una configurazione minimale (nel senso che verranno passate solo le opzioni base al server [Xorg](/index.php/Xorg "Xorg")), o può includere una serie di impostazioni che possono bypassare le opzioni preconfigurate o di autoricerca di Xorg.

**Nota:** Sin dalla versione 1.8.x, Xorg utilizza file separati di configurazione allocati in `/etc/X11/xorg.conf.d/`, si veda la sezione [configurazione avanzata](/index.php/NVIDIA#Avanzato:_20-nvidia.conf "NVIDIA") per maggiori informazioni.

### Configurazione minimale

Un blocco di configurazione di base in `20-nvidia.conf` (o nel deprecato `xorg.conf`) può essere simile a questo:

 `/etc/X11/xorg.conf.d/20-nvidia.conf` 
```
Section "Device"
        Identifier "Nvidia Card"
        Driver "nvidia"
        VendorName "NVIDIA Corporation"
        Option "NoLogo" "true"
        #Option "UseEDID" "false"
        #Option "ConnectedMonitor" "DFP"
        # ...
EndSection

```

**Suggerimento:** Se state aggiornando dopo aver utilizzato i driver nouveau, assicurarsi di rimuovere `nouveau` dal file `/etc/mkinitcpio.conf`. Si veda [passare tra i driver nvidia e nouveau](#Passare_tra_i_driver_nvidia_e_nouveau), se si desidera passare tra i driver Open e quelli proprietari.

### Configurazione automatica

Il pacchetto NVIDIA include un tool di configurazione automatica per creare un file di configurazione(`xorg.conf`) per il server Xorg e può essere eseguito con:

```
# nvidia-xconfig

```

Questo comando ricercherà automaticamente e creerà (o modificherà se già presente) la configurazione di `/etc/X11/xorg.conf`, a seconda dell'hardware installato.

Se risulta presente l'istanza di DRI, assicurarsi che sia commentata:

```
#    Load        "dri"

```

Controllare che il file `/etc/X11/xorg.conf` appena creato contenga come valori predefiniti di depth, horizontal sync, vertical refresh, e risoluzione monitor accettabili per il vostro hardware.

**Attenzione:** Questa procedura potrebbe non funzionare correttamente con Xorg-server 1.8

### Monitor multipli

	*Si veda l'articolo [Multimonitor](/index.php/Multihead "Multihead") per maggiori informazioni generali*

**Attenzione:** A partire da agosto 2013, Xinerama non funziona quando si utilizza il driver NVIDIA proprietario dalla versione 319 in su. Gli utenti che desiderano utilizzare Xinerama con il driver NVIDIA devono utilizzare il driver NVIDIA 313 , che funziona solo con kernel Linux precedenti alla versione 3.10\. vedere [this thread](https://bbs.archlinux.org/viewtopic.php?id=163319) per maggiori informazioni.

Per attivare il supporto al doppio schermo, è sufficiente modificare il file `/etc/X11/xorg.conf.d/10-monitor.conf` che si è precedentemente creato.

Per ogni monitor fisico, aggiungere una sezione Monitor, Device, and Screen, e poi una sezione ServerLayout per gestirli. Sappiate che quando Xinerama è abilitato, il driver NVIDIA proprietario disattiva automaticamente il compositing. Se desiderate sfruttare il compositing, si dovrebbero commentare la linea `Xinerama` in `ServerLayout` e utilizzare, invece, TwinView (si veda sotto).

 `/etc/X11/xorg.conf.d/10-monitor.conf` 
```
Section "ServerLayout"
    Identifier     "DualSreen"
    Screen       0 "Screen0"
    Screen       1 "Screen1" RightOf "Screen0" #Screen1 at the right of Screen0
    Option         "Xinerama" "1" #To move windows between screens
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
    Identifier     "Device0"
    Driver         "nvidia"
    Screen         0
EndSection

Section "Device"
    Identifier     "Device1"
    Driver         "nvidia"
    Screen         1
EndSection

Section "Screen"
    Identifier     "Screen0"
    Device         "Device0"
    Monitor        "Monitor0"
    DefaultDepth    24
    Option         "TwinView" "0"
    SubSection "Display"
        Depth          24
        Modes          "1280x800_75.00"
    EndSubSection
EndSection

Section "Screen"
    Identifier     "Screen1"
    Device         "Device1"
    Monitor        "Monitor1"
    DefaultDepth   24
    Option         "TwinView" "0"
    SubSection "Display"
        Depth          24
    EndSubSection
EndSection

```

#### TwinView

Si vuole solo un grande schermo invece di due. Impostare l'opzione `TwinView` a `1`. Questa opzione dovrebbe essere usato al posto di Xinerama (vedi sopra), se si desidera il compositing.

```
Option "TwinView" "1"

```

TwinView funziona solo sulla scheda di base: Se si dispone di più schede, dovrete usare xinerama o la modalità zaphod (schermi multipli in X). È possibile combinare TwinView con la modalità zaphod, ad esempio, con due schermi X che coprono due monitor ciascuno. La maggior parte dei window manager falliscono miseramente in modalità Zaphod. Una brillante eccezione è Awesome, in alcuni casi funziona anche con KDE.

Esempio di configurazione:

 `/etc/X11/xorg.conf.d/10-monitor.conf` 
```
Section "ServerLayout"
    Identifier    "TwinLayout"
    Screen        0 "metaScreen" 0 0
EndSection

Section "Monitor"
    Identifier    "Monitor0"
    Option        "Enable" "true"
EndSection

Section "Monitor"
    Identifier    "Monitor1"
    Option        "Enable" "true"
EndSection

Section "Device"
    Identifier    "Card0"
    Driver        "nvidia"
    VendorName    "NVIDIA Corporation"
    #refer to the link below for more information on each of the following options.
    Option        "HorizSync"          "DFP-0: 28-33; DFP-1 28-33"
    Option        "VertRefresh"        "DFP-0: 43-73; DFP-1 43-73"
    Option        "MetaModes"          "1920x1080, 1920x1080"
    Option        "ConnectedMonitor"  "DFP-0, DFP-1"
    Option        "MetaModeOrientation" "DFP-1 LeftOf DFP-0"
EndSection

Section "Screen"
    Identifier    "metaScreen"
    Device        "Card0"
    Monitor        "Monitor0"
    DefaultDepth    24
    Option        "TwinView" "True"
    SubSection "Display"
        Modes          "1920x1080"
    EndSubSection
EndSection

```

[Informazioni sulle opzioni da usare in Device](http://us.download.nvidia.com/XFree86/Linux-x86/304.51/README/configtwinview.html)

Se si dispone di più in modalità SLI, è possibile eseguire più di un monitor collegato a schede separate ( per esempio : due schede in SLI con un monitor collegato a ciascuno). L'opzione " MetaModes " in collaborazione con la modalità SLI Mosaic permette questo. Qui di seguito è una configurazione che funziona per l'esempio di cui sopra e corre [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)") senza problemi .

 `/etc/X11/xorg.conf.d/10-monitor.conf` 
```
Section "Device"
        Identifier      "Card A"
        Driver          "nvidia"
        BusID           "PCI:1:00:0"
EndSection

Section "Device"
        Identifier      "Card B"
        Driver          "nvidia"
        BusID           "PCI:2:00:0"
EndSection

Section "Monitor"
        Identifier      "Right Monitor"
EndSection

Section "Monitor"
        Identifier      "Left Monitor"
EndSection

Section "Screen"
        Identifier      "Right Screen"
        Device          "Card A"
        Monitor         "Right Monitor"
        DefaultDepth    24
        Option          "SLI" "Mosaic"
        Option          "Stereo" "0"
        Option          "BaseMosaic" "True"
        Option          "MetaModes" "GPU-0.DFP-0: 1920x1200+4480+0, GPU-1.DFP-0:1920x1200+0+0"
        SubSection      "Display"
                        Depth           24
        EndSubSection
EndSection

Section "Screen"
        Identifier      "Left Screen"
        Device          "Card B"
        Monitor         "Left Monitor"
        DefaultDepth    24
        Option          "SLI" "Mosaic"
        Option          "Stereo" "0"
        Option          "BaseMosaic" "True"
        Option          "MetaModes" "GPU-0.DFP-0: 1920x1200+4480+0, GPU-1.DFP-0:1920x1200+0+0"
        SubSection      "Display"
                        Depth           24
        EndSubSection
EndSection

Section "ServerLayout"
        Identifier      "Default"
        Screen 0        "Right Screen" 0 0
        Option          "Xinerama" "0"
EndSection
```

##### Configurazione manuale in CLI tramite xrandr

Se l'ultima soluzione non dovesse funzionare, è possibile utilizzare il trucco dell'*autostart* tramite il vostro gestore di finestre per eseguire un comando `xrandr` come questo:

```
xrandr --output DVI-I-0 --auto --primary --left-of DVI-I-1

```

oppure :

```
xrandr --output DVI-I-1 --pos 1440x0 --mode 1440x900 --rate 75.0

```

Dove:

*   `--output` serve per indicare a quale monitor impostare le opzioni.
*   `DVI-I-1` è il nome del secondo monitor..
*   `--pos` è la posizione del secondo monitor rispetto al primo.
*   `--mode` è la risoluzione del secondo monitor.
*   `--rate` imposta la frequenza in Hz.

É necessario adattare questa stringa con opzioni di `xrandr` con l'aiuto dell'output generato dal solo comando `xrandr` eseguito in un terminale.

#### Utilizzare NVIDIA Settings

È inoltre possibile utilizzare lo strumento `nvidia-settings` fornito da [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils). Con questo metodo, si utilizzerà il software proprietario di NVIDIA messo a disposizione dai loro driver. Basta eseguire `nvidia-settings` da root, quindi configurare come si desidera, e salvare la configurazione `/etc/X11/xorg.conf.d/10-monitor.conf`.

#### ConnectedMonitor

Se il driver non rileva un secondo monitor, si può costringerlo a farlo con ConnectedMonitor.

 `/etc/X11/xorg.conf` 
```

Section "Monitor"
    Identifier     "Monitor1"
    VendorName     "Panasonic"
    ModelName      "Panasonic MICRON 2100Ex"
    HorizSync       30.0 - 121.0 # this monitor has incorrect EDID, hence Option "UseEDIDFreqs" "false"
    VertRefresh     50.0 - 160.0
    Option         "DPMS"
EndSection

Section "Monitor"
    Identifier     "Monitor2"
    VendorName     "Gateway"
    ModelName      "GatewayVX1120"
    HorizSync       30.0 - 121.0
    VertRefresh     50.0 - 160.0
    Option         "DPMS"
EndSection

Section "Device"
    Identifier     "Device1"
    Driver         "nvidia"
    Option         "NoLogo"
    Option         "UseEDIDFreqs" "false"
    Option         "ConnectedMonitor" "CRT,CRT"
    VendorName     "NVIDIA Corporation"
    BoardName      "GeForce 6200 LE"
    BusID          "PCI:3:0:0"
    Screen          0
EndSection

Section "Device"
    Identifier     "Device2"
    Driver         "nvidia"
    Option         "NoLogo"
    Option         "UseEDIDFreqs" "false"
    Option         "ConnectedMonitor" "CRT,CRT"
    VendorName     "NVIDIA Corporation"
    BoardName      "GeForce 6200 LE"
    BusID          "PCI:3:0:0"
    Screen          1
EndSection

```

La sezione duplicata di "Device" con `Screen` serve ad impostare X ad usare due monitor su una singola scheda senza utilizzare `TwinView`. Si noti che `nvidia-settings` eliminerà tutte le opzioni `ConnectedMonitor` che sono state aggiunte.

#### Modalità Mosaico

La modalità mosaico è l' unico modo per utilizzare più di 2 monitor su più schede grafiche con il compositing. Il window manager può o non può riconoscere la distinzione tra ogni monitor.

##### Base Mosaic

La modalità mosaico di Base funziona su qualsiasi GPU dalla serie GeForce 8000 o superiore. Non può essere attivata tramite l'interfaccia grafica di nvidia-setting. È necessario utilizzare il programma a riga di comando nvidia-xconfig o modificare xorg.conf a mano, nel quale deve essere specificato il MetaModes. Segue un esempio di quattro connessioni DFP in configurazione 2x2, ciascuno in esecuzione a risoluzione 1920x1024, con due monitor DFP collegati a due schede:

```
$ nvidia-xconfig --base-mosaic --metamodes="GPU-0.DFP-0: 1920x1024+0+0, GPU-0.DFP-1: 1920x1024+1920+0, GPU-1.DFP-0: 1920x1024+0+1024, GPU-1.DFP-1: 1920x1024+1920+1024"

```

##### SLI Mosaic

Se si dispone di una configurazione SLI e ogni GPU è una Quadro FX 5800, Quadro Fermi o successivo, allora è possibile utilizzare la modalità SLI=Mosaic. Può essere abilitato direttamente dalla GUI di nvidia-settings GUI o dal riga di comando con:

```
$ nvidia-xconfig --sli=Mosaic --metamodes="GPU-0.DFP-0: 1920x1024+0+0, GPU-0.DFP-1: 1920x1024+1920+0, GPU-1.DFP-0: 1920x1024+0+1024, GPU-1.DFP-1: 1920x1024+1920+1024"

```

## Tweaking

### GUI: nvidia-settings

Il pacchetto NVIDIA include il programma `nvidia-settings` che permette l'adattamento di diverse impostazioni aggiuntive.

Per caricare le impostazioni al login eseguire questo comando dal terminale:

```
$ nvidia-settings --load-config-only

```

Il metodo di auto-avvio del desktop environment 'può' non funzionare per caricare nvidia-settings correttamente (KDE). Per essere sicuri che le impostazioni siano realmente caricate mettere il comando nel file `~/.xinitrc` (crearlo se non presente).

Per un aumento considerevole di prestazioni grafiche 2D in applicazioni che sfruttano in modo intensivo il pixmap, es. Firefox, impostare il parametro `InitialPixmapPlacement` a 2:

```
$ nvidia-settings -a InitialPixmapPlacement=2

```

Questo è documentato nel [codice sorgente di nvidia-settings](http://cgit.freedesktop.org/~aplattner/nvidia-settings/tree/src/libXNVCtrl/NVCtrl.h?id=b27db3d10d58b821e87fbe3f46166e02dc589855#n2797). Per renderlo permanente, questo comando necesita di essere lanciato ad ogni avvio di sistema. È possibile aggiungerlo al file `~/.Xinitrc` per un auto-avvio con X.

**Suggerimento:** In rare occasioni il `~/.nvidia-settings-rc` può risultare corrotto. Se questo accade il server Xorg può crashare e il file dovrà essere cancellato per risolvere il problema.

### Avanzato: 20-nvidia.conf

Modificare `/etc/X11/xorg.conf.d/20-nvidia.conf` e aggiungere le opzioni alla sezione corretta. Il server Xorg dovrà essere riavviato prima che le modifiche abbiano effetto.

Vedere [NVIDIA Accelerated Linux Graphics Driver README and Installation Guide](http://http.download.nvidia.com/XFree86/Linux-x86/304.51/README/) per maggiori dettagli e opzioni di configurazione.

#### Abilitare la desktop composition

Dalla versione 180.44 dei driver NVIDIA il supporto per GLX con Damage e l'estensione Composite X sono abilitate di default. Si faccia riferimento alla pagina di [Xorg](/index.php/Xorg#Composite "Xorg") per delle istruzioni dettagliate.

#### Disabiliare visione logo all'avvio

Aggiungere l'opzione `"NoLogo"` nella sezione `Device`:

```
Option "NoLogo" "True"

```

#### Abilitare accelerazione hardware

Aggiungere l'opzione `"RenderAccel"` nella sezione `Device`:

```
Option "RenderAccel" "True"

```

**Nota:** `RenderAccel` è abilitato di default dalla versione 97.46.xx dei driver.

#### Annullare la ricerca del monitor

L'opzione `"ConnectedMonitor"` nella sezione `Device` permette di annullare la ricerca del monitor all'avvio del server X, il che può far risparmiare diverso tempo. Le opzioni disponibili sono: `"CRT"` per connessioni analogiche, `"DFP"` per monitor digitali e `"TV"` per le televisioni.

La seguente dichiarazione forza i driver NVIDIA a bypassare i controlli d'avvio e a riconoscere il monitor come DFP:

```
Option "ConnectedMonitor" "DFP"

```

**Nota:** Si utilizzi "CRT" per tutte le connessioni analogiche 15 pin VGA, anche se il display è uno schermo piatto. "DFP" è da utilizzarsi solamente per le connessioni digitali DVI.

#### Abilitare il triple buffering

Per abilitare il triple buffering si aggiunga l'opzione `"TripleBuffer"` nella sezione `Device`:

```
Option "TripleBuffer" "True"

```

Si usi questa opzione se la scheda video abbonda di RAM (uguale o superiore a 128MB). L'impostazione ha effetto solamente quando `syncing to vblank`, una delle opzioni disponibili in `nvidia-settings`, è abilitata.

**Nota:** Questa opzione può causare problemi di visualizzazione a schermo intero. Come sulle schede R300, dove vblank è abilitato di default

#### Usare gli eventi di sistema

Dal file [LEGGIMI](http://http.download.nvidia.com/XFree86/Linux-x86/304.51/README/xconfigoptions.html) dei driver NVIDIA: *"Usa gli eventi di sistema per dare notifica ad X quando un client ha compiuto il direct rendering su una finestra che necessita di essere composta."* Qualsiasi cosa identifichi, aiuta ad aumentare le prestazioni. Questa opzione è al momento incompatibile con le tecnologie SLI e Multi-GPU.

Nella sezione `Device` aggiungete:

```
Option "DamageEvents" "1"

```

**Nota:** Questa opzione è abilitata di default nei driver più recenti.

#### Abilitare il risparmio energetico

Nella sezione `Monitor` aggiungete:

```
Option "DPMS" "1"

```

#### Abilitare il controllo della luminosità

Aggiungere nella sezione `Device`:

```
Option "RegistryDwords" "EnableBrightnessControl=1"

```

**Nota:** Se avete questa opzione già abilitata e il controllo della luminosità non funziona, provate a commentarla.

#### Abilitare la modalità SLI

**Attenzione:** L'abilitazione della modalità SLI, potrebbe causare scarse prestazioni video se si utilizza Gnome3 come ambiente desktop

Tratto dall'appendice del [[README](http://http.download.nvidia.com/XFree86/Linux-x86/304.51/README/xconfigoptions.html) dei driver nVidia: *Questa opzione controlla la configurazione SLI di rendering in configurazioni supportate.* Una *configurazione supportata* è un computer dotato di una scheda madre SLI-Certified Motherboard e 2 o 3 schede video SLI-Certified GeForce GPUs. Si veda NVIDIA's [SLI Zone](http://www.slizone.com/page/home.html) per ulteriori dettagli.

Per prima cosa individuare il PCI Bus ID delle GPU utilizzando `lspci`:

 ` $ lspci | grep VGA` 
```
 03:00.0 VGA compatible controller: nVidia Corporation G92 [GeForce 8800 GTS 512] (rev a2)
 05:00.0 VGA compatible controller: nVidia Corporation G92 [GeForce 8800 GTS 512] (rev a2)

```

Aggiungere il BusID (Nel nostro esempio è il 3) nella sezione `Device`:

```
BusID "PCI:3:0:0"

```

**Nota:** Il formato è molto importante. Il valore del BusID deve essere specificato come `"PCI:<BusID>:0:0"`

Aggiungere il valore desiderato per la modalità di rendering SLI da utilizzare nella sezione `Screen`:

```
Option "SLI" "AA"

```

La seguente tabella mostra le varie modalità di rendering disponibili.

| Valore | Comportamento |
| 0, no, off, false, Single | Usare solo una singola GPU per il rendering. |
| 1, yes, on, true, Auto | Abilita lo SLI e consente al driver di selezionare automaticamente la modalità di rendering appropriata. |
| AFR | Abilita lo SLI e utilizza una modalità di rendering a frame alternato. |
| SFR | Abilita lo SLI e utilizza una modalità di rendering a frame "diviso". |
| AA | Abilita lo SLI e usa anche lo SLI antialiasing. Utilizzare questa modalità combinata con l'antialiasing a schermo intero per migliorare la qualità visiva . |

In alternativa si può usare l'utilità `nvidia-xconfig` per inserire i cambiamenti voluti direttamente nel file `xorg.conf` con un singolo comando:

```
# nvidia-xconfig --busid=PCI:3:0:0 --sli=AA

```

Per verificare se la modalità SLI è abilitata, scrivere in un terminale:

 `nvidia-settings -q all | grep SLIMode` 
```
  Attribute 'SLIMode' (arch:0.0): AA 
    'SLIMode' is a string attribute.
    'SLIMode' is a read-only attribute.
    'SLIMode' can use the following target types: X Screen.

```

**Attenzione:** Dopo l'attivazione SLI il sistema potrebbe diventare congelato o non risponde all'avvio di xorg . Si consiglia di disattivare il vostro display manager prima di riavviare.

#### Forzare il livello di performance Powermizer (per portatili)

Nel vostro file xorg.conf, aggiungete le seguenti linee nella sezione `Device`:

 `/etc/X11/xorg.conf` 
```
.......
# Force Powermizer to a certain level at all times
# level 0x0=adaptiv (Driver Default)
# level 0x1=highest
# level 0x2=med
# level 0x3=lowest

# Battery settings:
Option	"RegistryDwords" "PowerMizerLevel=0x3"

# (Optional) AC Power adaptiv Mode and Battery Power forced to lowest Mode:
 Option "RegistryDwords" "PowerMizerLevelAC=0x0; PowerMizerLevel=0x3"

```

##### Lasciare che la GPU imposti automaticamente il livello di performance (basato sulla temperatura)

Nel vostro file xorg.conf, aggiungete la seguente linea nella sezione `Device`

```
Option "RegistryDwords" "PerfLevelSrc=0x3333"

```

#### Disabilitare i *vblank interrupts* (per portatili)

Quando l'utility di riconoscimento degli interrupt [powertop](/index.php/Powertop "Powertop") è attiva, è noto che i driver NVIDIA generano un interrupt per ogni vblank. Per evitare questo inconveniente, aggiungere la seguente riga nella sezione `Device`:

```
Option         "OnDemandVBlankInterrupts" "1"

```

Questa modifica ridurrà sensibilmente gli interrupt al secondo.

#### Abilitare l'overclocking

**Attenzione:** L'overclocking può danneggiare il vostro hardware e alcuna responsabilità può pendere sugli autori di questa pagina in seguito a possibili danni riportati dalla strumentazione hardware modificata in modo da operare diversamente dalle specifiche tecniche di fabbrica.

Per abilitare l'overclocking, aggiungere la riga seguente nella sezione `device`:

```
Option         "Coolbits" "1"

```

Questa modifica abiliterà la gestione dell'overclocking attraverso nvidia-settings all'interno di X.

```
$ nvidia-settings

```

**Nota:** La schede nvidia della serie GeForce 400/500/600/700 che utilizzano il core "Fermi/Kepler" non supportano attualmente il metodo 'Coolbits' per l'overclocking . Una alternativa è quella di flashare e modificare il BIOS della GPU sotto DOS (preferibile), o da un sistema WIN32 tramite l'ausilio di [nvflash](http://www.mvktech.net/component/option,com_remository/Itemid,26/func,select/id,127/orderby,2/page,1/) e [NiBiTor 6.0](http://www.mvktech.net/component/option,com_remository/Itemid,26/func,select/id,135/orderby,2/page,1/). Il vantaggio di effettuare un flash del BIOS è che non solo può essere aumentato il limite di tensione, ma la stabilità è generalmente migliorata rispetto ai metodi di overclocking software come Coolbits.

##### Impostare un clock statico 2D/3D

Aggiungere la seguente stringa alla *Section Device* per impostare il sistema PowerMizer al livello di *maximum performance*.

```
Option "RegistryDwords" "PerfLevelSrc=0x2222"

```

Aggiungere le seguenti due stringhe in *Section Device* per abilitare il controllo manuale della velocità delle ventole tramite `nvidia-settings`.

```
Option "Coolbits" "4"
Option "Coolbits" "5"

```

## Trucchi e consigli

### Aggiustare la Risoluzione del terminale di avvio

La transizione da nouveau può causare all'avvio una visualizzazione del terminale ad una risoluzione inferiore. Una possibile soluzione (se si utilizza GRUB) è quella di modificare la linea `GRUB_GFXMODE` in `/etc/default/grub` con la risoluzione dello schermo desiderata. É possibile specificare più risoluzioni, compreso il il parametro predefinito `auto`, per cui si consiglia di modificare la riga come questo esempio: {{ic|GRUB_GFXMODE=<risoluzione desiderper ulteriori informazioni.

### Abilitare Video HD (VDPAU/VAAPI)

**Requisiti Hardware:**

Avere una scheda video che supporti almeno la seconda generazione di PureVideo HD [wikipedia:Nvidia_PureVideo#Table_of_PureVideo_.28HD.29_GPUs](https://en.wikipedia.org/wiki/Nvidia_PureVideo#Table_of_PureVideo_.28HD.29_GPUs "wikipedia:Nvidia PureVideo")

**Software richiesto:**

le schede video Nvidia con i driver proprietari installati forniscono la capacità di decodifica video con l'interfaccia VDPAU a livelli diversi a seconda della generazione PureVideo.

Si può aggiungere il supporto all'interfaccia VA-API installando[libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver).

Controllare il supporto VA-API con:

```
$ vainfo

```

Per sfruttare appieno la capacità hardware di decodifica della scheda video si necessita dell'utilizzo di un lettore multimediale che supporta VDPAU o VA-API.

*   Abilitare l'accelerazione hardware in [MPlayer](/index.php/MPlayer "MPlayer") modificando `~/.mplayer/config` in questo modo:

```
vo=vdpau
vc=ffmpeg12vdpau,ffwmv3vdpau,ffvc1vdpau,ffh264vdpau,ffodivxvdpau,

```

**Attenzione:** Il codec `ffodivxvdpau` è supportato solo dalla più recente serie di hardware NVIDIA . Considerare di ometterlo, sulla base di hardware specifico.

*   Per abilitare l'accelerazione hardware in [VLC](/index.php/VLC "VLC") andate su:

`**Strumenti**>**Preferenze**>**Ingresso e Codificatori**` e spuntare `**Use GPU acceleration**`

*   Per abilitare l'accelerazione hardware in **smplayer** andate su:

`**Opzioni**>**Preferenze**>**Generali**>**Scheda Video**` e selezionare `**vdpau**` come uscita del driver

*   Per abilitare l'accelerazione hardware in **gnome-mplayer** andate su:

`**Modifica**>**Preferenze**` e impostare l'`**uscita video**` su `**vdpau**`

**Guardare i video HD in presenza di schede con poca memoria:**

Se la vostra scheda grafica non ha una buon quantitativo di memoria (>521MB?), può capitare che i video riprodotti alla risoluzione 1080p o 720p , presentito scarse prestazioni, come per esempio che il video vada a scatti. Un possibile metodo per evitare che ciò accada è utilizzare un windows manager molto leggero come TWM o MWM.

In aggiunta aumentare la cache di MPlayer's editando `~/.mplayer/config` può aiutare, quando guardando un video in HD si decade la velocità dell'hard disk.

### Evitare screen tearing in KDE (KWin)

 `/etc/profile.d/kwin.sh` 
```
export __GL_YIELD="USLEEP"

```

Anche se quanto sopra non aiuta , allora si provi questo :

 `/etc/profile.d/kwin.sh` 
```
export KWIN_TRIPLE_BUFFER=1

```

Non utilizzate entrambi i metodi allo stesso tempo. Inoltre se si attiva il Triple buffer, assicurarsi di attivarlo anche per il driver stesso. Fonte: [https://bugs.kde.org/show_bug.cgi?id=322060](https://bugs.kde.org/show_bug.cgi?id=322060)

### Accelerazione hardware con il codec video XvMC

La decodifica accelerata per video MPEG-1 e MPEG-2 tramite [XvMC](/index.php/XvMC "XvMC") è supportata sulle schede della serie GeForce4, GeForce 5 FX, GeForce 6 e GeForce 7\. Si veda come configurare i [programmi supportati](/index.php/XvMC#Supported_software "XvMC"). Per usufruirne creare un nuovo file `/etc/X11/XvMCConfig` con il seguente contenuto :

```
libXvMCNVIDIA_dynamic.so.1

```

### Usare l'uscita TV

Un buon articolo a riguardo può essere trovato [qui](http://en.wikibooks.org/wiki/NVidia/TV-OUT)

### X con la TV (DFP) come unico display

Il server X ritorna a CRT-0 se nessun monitor viene riconosciuto automaticamente. Ciò può rappresentare un problema nel caso in cui si usi una TV connessa tramite DVI come display principale, e il server X venga avviato mentre la TV è spenta o disconnessa.

Per forzare i driver nvidia ad usare DFP, si conservi una copia dell' EDID da qualche parte nel filesystem in modo tale che X possa analizzare il file invece di leggere l' EDID dalla TV/DFP.

Per acquisire l' EDID, si avvii nvidia-settings. Verranno mostrate alcune informazioni in una struttura ad albero, si ignorino per il momento il resto delle impostazioni e si selezioni GPU (l'entrata corrispondente dovrebbe intitolarsi "GPU-0" o qualcosa di simile), quindi la sezione `DFP` (di nuovo, `DFP-0` o qualcosa di simile), si clicchi su `Acquire Edid` e lo si salvi da qualche parte, ad esempio, `/etc/X11/dfp0.edid`.

Si modifichi `xorg.conf` aggiungendo alla sezione `Device`:

```
Option "ConnectedMonitor" "DFP"
Option "CustomEDID" "DFP-0:/etc/X11/dfp0.edid"

```

L'opzione `ConnectedMonitor` forza il driver a riconoscere la DFP come se fosse connessa. L'opzione `CustomEDID` fornisce l'informazione EDID per il device, ciò significa che sarà avviato esattamente come se la TV/DFP fosse stata connessa durante il processo X.

In questa maniera, si può avviare automaticamente un display manager al boot e quindi avere una schermata di X funzionante e propriamente configurata entro l'accensione della TV.

### Controllare l'alimentazione

Il driver NVIDIA X.org può anche essere utilizzato per controllare l'alimentazione della GPU. Per vedere lo stato di alimentazione corrente, controllare il parametro di sola lettura 'GPUPowerSource' (0 = AC, 1 = batteria) :

 `$ nvidia-settings -q GPUPowerSource -t`  `1` 

Se viene visualizzato un messaggio di errore simile a quello qui sotto, allora dovreste aver bisogno di installare [acpid](/index.php/Acpid_(Italiano) "Acpid (Italiano)") o avviare il servizio systemd tramite `systemctl start acpid.service`

```
ACPI: failed to connect to the ACPI event daemon; the daemon
may not be running or the "AcpidSocketPath" X
configuration option may not be set correctly.  When the
ACPI event daemon is available, the NVIDIA X driver will
try to use it to receive ACPI event notifications.  For
details, please see the "ConnectToAcpid" and
"AcpidSocketPath" X configuration options in Appendix B: X
Config Options in the README.

```

(Se non viene cisualizzato questo errore, non è necessario installare e/o eseguire solo acpid per questo scopo. Lo stato di alimentazione può essere correttamente segnalato anche se non si è installato acpid.)

### Visualizzare la temperatura GPU nella shell

#### Metodo 1 - nvidia-settings

**Nota:** Questo metodo richiede l'uso di X. Si segua altrimenti il metodo 2 od il metodo 3\. Si noti inoltre che il metodo 3 non funzionerà con nuove schede nvidia come la G210/220 o le Zotac IONITX's 8800GS

Per visualizzare la temperatura GPU nella shell, si usi `nvidia-settings` come segue:

```
$ nvidia-settings -q gpucoretemp

```

Ciò darà come output qualcosa di simile a:

```
Attribute 'GPUCoreTemp' (hostname:0.0): 41.
'GPUCoreTemp' is an integer attribute.
'GPUCoreTemp' is a read-only attribute.
'GPUCoreTemp' can use the following target types: X Screen, GPU.

```

La temperatura GPU di questa scheda è di 41 C.

Per ottenere solamente la temperatura per usarla in programmi come `rrdtool` o `conky`, tra gli altri:

 ` $ nvidia-settings -q gpucoretemp -t`  ` 41` 

#### Metodo 2 - nvidia-smi

Usare nvidia-smi, che può leggere la temperatura direttamente dalla GPU senza utilizzare X. Questo metodo è perfetto per coloro i quali non hanno necessità di utilizzare X, ad esempio se il computer in questione è un server, e non utilizza applicazioni con interfaccia grafica. Per mostrare la temperatura della GPU nella shell, usare nvidia-smi come mostrato:

```
$ nvidia-smi

```

Il comando dovrebbe generare un output simile al qui riportato:

 `$ nvidia-smi` 
```
Fri Jan  6 18:53:54 2012      
+------------------------------------------------------+                      
| NVIDIA-SMI 2.290.10  Driver Version: 290.10          |                      
|-------------------------------+----------------------+----------------------+
| Nb.  Name                     | Bus Id        Disp.  | Volatile ECC SB / DB |
| Fan  Temp  Power Usage /Cap   | Memory Usage         | GPU Util. Compute M. |
|===============================+======================+======================|
| 0\.  GeForce 8500 GT           | 0000:01:00.0  N/A    |      N/A        N/A  |
|  30%  62 C  N/A  N/A /  N/A   |  17%  42MB /  255MB  |  N/A      Default    |
|-------------------------------+----------------------+----------------------|
| Compute processes:                                              GPU Memory  |
|  GPU  PID    Process name                                      Usage        |
|=============================================================================|
|  0\.          ERROR: Not Supported                                           |
+-----------------------------------------------------------------------------+

```

Per mostrare dati solo sulla temperatura:

 `$ nvidia-smi -q -d TEMPERATURE` 
```
==============NVSMI LOG==============
Timestamp                      : Fri Jan  6 18:50:57 2012
Driver Version                 : 290.10
Attached GPUs                  : 1
GPU 0000:01:00.0
    Temperature
        Gpu                    : 62 C

```

Per catturare solo il valore della temperatura, per utilizzarla in strumenti come rrdtool o conky, eseguire il comando:

 `$ nvidia-smi -q -d TEMPERATURE | grep Gpu | cut -c35-36`  ` 62` 

Riferimenti: [http://www.question-defense.com/2010/03/22/gpu-linux-shell-temp-get-nvidia-gpu-temperatures-via-linux-cli](http://www.question-defense.com/2010/03/22/gpu-linux-shell-temp-get-nvidia-gpu-temperatures-via-linux-cli)

#### Metodo 3 - nvclock

Si usi [nvclock](https://aur.archlinux.org/packages/nvclock/) che è disponibile su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)")

**Nota:** Si noti che `nvclock` non può accedere ai sensori termali di nuove schede NVIDIA come la G210/220.

Ci possono essere differenze significative tra le temperature riportato da nvclock e nvidia-settings/nv-control. Secondo [questo post](http://sourceforge.net/projects/nvclock/forums/forum/67426/topic/1906899) da parte dell'autore (Thunderbird) di nvclock, i valori nvclock dovrebbero essere più accurati.

### Impostare la velocità della ventola al Login

È possibile regolare la velocità della ventola della scheda grafica con l'ausilio del programma `nvidia-settings`. Prima assicurarsi che nella configurazione di Xorg sia impostata l'opzione Coolbits a `4` o nella sezione `Device` per abilitare il controllo delle ventole.

```
Option "Coolbits" "4"

```

**Nota:** Le schede della serie GTX 4xx/5xx attualmente non possono impostare la velocità della ventola tramite questo metodo all'avvio del sistema. Questo metodo consente solo la regolazione di velocità della ventola all'interno della sessione corrente di X tramite l'uso di nvidia-settings.

Aggiunger ele seguenti stringe nel vostro file [`~/.xinitrc`](/index.php/Xinitrc "Xinitrc") per impostare la velocità desiderata della ventola all'avvio di Xorg. Sostituire `*n*` con un valore percentuale in base alle vostre esigenze.

```
nvidia-settings -a "[gpu:0]/GPUFanControlState=1" -a "[fan:0]/GPUCurrentFanSpeed=*n*"

```

È inoltre possibile configurare una seconda GPU per incrementare il numero di GPU e della ventola.

```
nvidia-settings -a "[gpu:0]/GPUFanControlState=1" \ 
-a "[gpu:1]/GPUFanControlState=1" \
-a "[fan:0]/GPUCurrentFanSpeed=*n*" \
-a  [fan:1]/GPUCurrentFanSpeed=*n*" &

```

Se si sta utilizzando un gestore di accesso come GDM o KDM, si può creare un file .desktop che contiene al suo interno le impostazioni da avviare. Create il file `~/.config/autostart/nvidia-fan-speed.desktop` ed aggiungete al suo interno quanto segue. Anche in questo caso sostituite ad `*n*` un valore percentuale in base alle vostre esigenze.

```
[Desktop Entry]
Type=Application
Exec=nvidia-settings -a "[gpu:0]/GPUFanControlState=1" -a "[fan:0]/GPUCurrentFanSpeed=*n*"
X-GNOME-Autostart-enabled=true
Name=nvidia-fan-speed

```

### Ordine di installazione/disinstallazione al cambiamento dei driver

Nei casi in cui il vecchio driver è nvidiaO e il nuovo driver è nvidiaN.

```
Rimuovere nvidiaO
Installare nvidia-libglN
installare nvidiaN
installare lib32-nvidia-libgl-N (se richiesto)

```

### Passare tra i driver nvidia e nouveau

Se si desidera passare spesso tra i driver nvidia e i nouveau, è possibile utilizzare questi due semplici script per rendere il lavoro più semplice [necessitano di essere lanciati come root):

```
 #!/bin/bash
 # nouveau -> nvidia

 set -e

 # check if root
 if [[ $EUID -ne 0 ]]; then
    echo "You must be root to run this script. Aborting...";
    exit 1;
 fi

 sed -i 's/MODULES="nouveau"/#MODULES="nouveau"/' /etc/mkinitcpio.conf

 pacman -Rdds --noconfirm nouveau-dri xf86-video-nouveau mesa-libgl #lib32-nouveau-dri lib32-mesa-libgl
 pacman -S --noconfirm nvidia #lib32-nvidia-libgl

 mkinitcpio -p linux

```

```
 #!/bin/bash
 # nvidia -> nouveau

 set -e

 # check if root
 if [[ $EUID -ne 0 ]]; then
    echo "You must be root to run this script. Aborting...";
    exit 1;
 fi

 sed -i 's/#*MODULES="nouveau"/MODULES="nouveau"/' /etc/mkinitcpio.conf

 pacman -Rdds --noconfirm nvidia #lib32-nvidia-libgl
 pacman -S --noconfirm nouveau-dri xf86-video-nouveau #lib32-nouveau-dri

 mkinitcpio -p linux

```

Un riavvio è necessario per completare il passaggio.

Modificare questi script in base alle proprie esigenze, nel caso si utilizzino dei driver diversi dai NVIDIA (Es. nvidia-173xx).

De-commentare le stringhe ai pacchetti lib32 se si sta eseguendo un sistema a 64bit e sono richieste librerie a 32bit ((es. giochi 32-bit/Steam).

Si necessita di aver creato nella stessa directory dello script, sia il file `10-monitor.conf` che il file [20-nouveau.conf](/index.php/Nouveau_(Italiano)#Configurazione "Nouveau (Italiano)").

## Risoluzione dei problemi

### Performance scadenti, es. ridisegno lento quando si passa tra le schede in Chrome

Su alcune macchine, i recenti driver nvidia introducono un bug(?) Che provoca il ridisegnamento pixmaps molto lento in X11\. Il passaggio tra le schede di commutazione in Chrome/Chromium (pur avendo più di 2 schede aperte) dura 1-2 secondi, invece di pochi millisecondi.

Sembrerebbe che impostare la variabile **InitialPixmapPlacement** a **0** risolva il problema, anche se (come descritto nei paragrafi sopra) **InitialPixmapPlacement=2** dovrebbe in realtà essere il metodo più veloce.

La variabile può essere impostata (temporaneamente) con il comando:

```
$ nvidia-settings -a InitialPixmapPlacement=0

```

Per rendere questo parametro permanente, immettere il comando in uno script di avvio.

### Giocare usando Twinview

Nel caso in cui si desideri giocare a schermo intero con l'opzione Twinview, si avrà notato come i giochi riconoscono i due schermi come fossero uno solo. Sebbene ciò è tecnicamente corretto (lo schermo virtuale X è esattamente della dimensione della combinazione dei tuoi schermi), probabilmente non si vorrà giocare su entrambi gli schermi contemporaneamente.

Per correggere questo comportamento per SDL, si provi con:

```
export SDL_VIDEO_FULLSCREEN_HEAD=1

```

Per OpenGL, si aggiungano gli appropriati Metamodes al xorg.conf nella sezione `Device` e si riavvi X:

```
Option "Metamodes" "1680x1050,1680x1050; 1280x1024,1280x1024; 1680x1050,NULL;  1280x1024,NULL;"

```

Un altro metodo che può funzionare da solo o congiuntamente a quelli sopra descritti consiste nel [starting games in a seperate X server](/index.php/Gaming#Starting_games_in_a_separate_X_server "Gaming").

### Vertical sync using TwinView

Se si utilizza Vertical sync in combinazione con TwinView (l'opzione "Sync to Vblank" in **nvidia-settings**), noterete che solo uno schermo viene correttamente sincronizzato, a meno che non abbiate due monitor identici. Anche se **nvidia-settings** offre un'opzione per abilitare la sincronizzazione al cambio dello schermo (l'opzione "Sync to this display device"), questo non sempre funziona. Una soluzione è quella di aggiungere le seguenti variabili d'ambiente in fase di avvio, ad esempio in `/etc/profile`:

```
export __GL_SYNC_TO_VBLANK=1
export __GL_SYNC_DISPLAY_DEVICE=DFP-0
export __VDPAU_NVIDIA_SYNC_DISPLAY_DEVICE=DFP-0

```

Potete cambiare il valore `DFP-0` in base alle vostre esigenze (`DFP-0` indica la porta DVI, mentre `CRT-0` è la porta VGA). Potete trovare l'identificativo per il vostro display su **nvidia -settings** nella sezione " XVideoSettings X server".

### Vecchie impostazioni Xorg

Se si effettua l'upgrade da una vecchia installazione, si rimuovino i vecchi percorsi a `/usr/X11R6/` dal momento che possono creare problemi durante l'installazione.

### Schermata corrotta: il problema dei "Sei schermi"

Per alcuni utilizzatori delle schede video Geforce GT 100M, la schermata si rivela corrotta dopo aver avviato X; divisa in 6 sezioni con la risoluzione limitata a 640x480.

Lo stesso problema è stato recentemente segnalato con Quadro 2000 e ad alta risoluzione display.

Per risolvere questo problema, si abiliti il Validation Mode `NoTotalSizeCheck` nella sezione `Device`:

```
Option "ModeValidation" "NoTotalSizeCheck"

```

### Errore '/dev/nvidia0' Input/Output

Questo errore può verificarsi per diversi motivi, e la soluzione più comune è quella di verificare i permessi per il gruppo/file, anche se in molti casi si *non è* la soluzione del problema. Nella documentazione di NVIDIA non si accenna nel dettaglio di cosa si dovrebbe fare per correggere questo problema, ma ci sono alcuni metodi che hanno funzionato per diversi utenti. il problema può essere un conflitto con l'IRQ di un'altra periferica oppure un'errata assegnazione da parte del kernel o del tuo BIOS.

La prima cosa da tentare è quella di rimuovere eventuali altri dispositivi video, come schede di acquisizione, e vedere se il problema scompare. Avere troppi processori video sullo stesso sistema può portare nel kernel all'incapacità di avviarli, a causa di problemi di allocazione di memoria con il controller video. In particolare, su sistemi con bassa memoria video, questo problema si può presentare anche in presenza di un solo processore video. In tal caso si dovrebbe capire la quantità di memoria video del sistema (ad esempio con il comando `lspci -v`) e passare i parametri di assegnazione al kernel, ad esempio:

```
vmalloc=64M
or
vmalloc=256M

```

Se si utilizza un kernel a 64bit, un difetto del driver può causare che il modulo nvidia a fallisca l'inizializzazione IOMMU quando è attivato. Alcuni utenti hanno confermato che disattivarlo può risolvere il problema .

Un'altra cosa da provare è cambiare il controllo dell'assegnazione degli IRQ nel BIOS da `Operating system controlled` in `BIOS controlled` oppure provare le altre opzioni. Il primo può essere passato come parametro del kernel:

```
PCI=biosirq

```

Il parametro `noacpi` del kernel è stato anche suggerito come una possibile soluzione, ma dal momento che disattiva completamente il controllo ACPI dovrebbe essere usato con cautela. Alcuni componenti hardware possono essere facilmente danneggiati da surriscaldamento

**Nota:** I parametri del kernel possono essere passati tramite linea di comando del kernel o nel file di configurazione del bootloader. Vedere la pagina Wiki relativa al proprio bootloader in uso per maggiori informazioni.

### Errori '/dev/nvidiactl'

Provando ad iniziare un'applicazione opengl si riscontrano errori del tipo:

```
Error: Could not open /dev/nvidiactl because the permissions are too
restrictive. Please see the `FREQUENTLY ASKED QUESTIONS` 
section of `/usr/share/doc/NVIDIA_GLX-1.0/README` 
for steps to correct.

```

Si risolve aggiungendo l'user appropriato al gruppo`video` e effettuando nuovamente il login:

```
# gpasswd -a username video

```

### Le applicazioni 32 bit non si avviano

Nei sistemi a 64 bit, installare [lib32-nvidia-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-libgl) ,che corrisponde alla stessa versione installata per i driver a 64 bit, risolve il problema.

### Errori dopo l'aggiornamento del kernel

Se si sta utilizzando un modulo NVIDIA compilato al posto del pacchetto reperibile in [extra], è necessario effettuare una ricompilazione del modulo ad ogni aggiornamento del kernel. Un riavvio del sistema e generalmente raccomandato dopo un aggiornamento del kernel e dei driver grafici.

### Crash generali

*   Prova disabilitando `RenderAccel` in `xorg.conf`.
*   Se Xorg restituisce un errore riguardo "conflicting memory type",aggiungi `nopat` alla fine della linea `kernel` in `/boot/grub/menu.lst`.
*   Se il compilatore NVIDIA si lamenta di differenti versioni di GCC tra quella corrente e quella usata per compilare il kernel, aggiungi in `/etc/profile`:

```
export IGNORE_CC_MISMATCH=1

```

*   Se Xorg dovesse andare in crash con un "Signal 11" durante l'ulizzo dei drivers nvidia-96xx, si provi a disabilitare PAT. Si aggiunga l'opzione `nopat` ai [parametri del kernel](/index.php/Kernel_parameters "Kernel parameters").

Maggiori informazioni sulla risoluzione dei problemi dei driver possono essere trovate in [NVIDIA forums.](http://www.nvnews.net/vbulletin/forumdisplay.php?s=&forumid=14)

### Brutte performance dopo aver installato una nuova versione dei driver

Se gli FPS sono calati rispetto quelli con i vecchi driver, innanzitutto si controlli di aver abilitato il direct rendering (glxinfo è incluso nel pacchetto [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos)):

```
glxinfo | grep direct

```

Se il comando da come risposta:

 `glxinfo | grep direct`  ` direct rendering: No ` 

allora questo può essere indice dell'improvviso calo di FPS.

Una soluzione possibile consiste nel tornare alla versione di driver precedente e quindi riavviare.

### Picchi alti di CPU con schede della serie 400

Se si riscontrano picchi di CPU intermittente con una scheda della serie 400, ciò può essere causato da PowerMizer che cambia costantemente la frequenza di clock della GPU. Cambiare l'impostazione di PowerMizer da 'Adaptive' a 'Performance', aggiungendo la seguente opzione nella sezione `Device` della propria configurazione di Xorg:

```
 Option "RegistryDwords" "PowerMizerEnable=0x1; PerfLevelSrc=0x3322; PowerMizerDefaultAC=0x1"

```

### Per i laptop: X si blocca durante il login/out, ovviato con Ctrl+Alt+Backspace

Se durante l'utilizzo dei drivers nvidia ufficiali Xorg si dovesse bloccare durante il login e logout (in particolare con una schermata insolita divisa in due pezzi neri e bianco/grigi), ma è ancora possibile effettuare il login con `Ctrl+Alt+Backspace` (o qualsiasi sia la nuova scorciatoia "kill X"), si provi ad aggiungere questo in `/etc/modprobe.d/modprobe.conf`:

```
options nvidia NVreg_Mobile=1

```

Invece un utente ha avuto fortuna in questa maniera, ma per altri questa soluzione va a ledere sulle performance:

```
options nvidia NVreg_DeviceFileUID=0 NVreg_DeviceFileGID=33 NVreg_DeviceFileMode=0660 NVreg_SoftEDIDs=0 NVreg_Mobile=1

```

Si noti che `NVreg_Mobile` necessita di essere modificato in linea con il laptop:

*   1 per i laptops Dell.
*   2 per i laptops non Compal Toshiba.
*   3 per gli altri laptops.
*   4 per i laptops Compal Toshiba.
*   5 per i laptops Gateway.

Si veda [NVIDIA Driver's Readme:Appendix K](http://http.download.nvidia.com/XFree86/Linux-x86/1.0-7182/README/readme.txt) per maggiori informazioni.

### La frequenza di refresh non viene rilevata correttamente dalle utility dipendenti da XRandR

L'estensione XRandR X al momento non è in grado di gestire device con display multipli in un'unica schermata di X; si vede solamente il box fisso di `MetaMode`, che può contenere uno o più actual modes. Ciò significa che se diversi MetaMode hanno lo stesso box fisso, XRandR non sarà in grado di distinguerli.

In modo da supportare la `DynamicTwinView`, i driver NVIDIA devono far apparire a XRandR ogni MetaMode come unico. Al momento, i driver Nvidia realizzano questo usando la frequenza di refresh come unico identificatore.

Si usi `nvidia-settings -q RefreshRate` per richiedere l'attuale frequenza di refresh su ogni display.

L'estensione XRandR al momento sta per essere ridisegnata dalla comunità di X.Org, così la soluzione della frequenza di refresh potrà essere rimossa tra un pò di tempo.

Questa soluzione può essere anche disabilitata impostando l'opzione di configurazione di X `DynamicTwinView` a `false`, che disabiliterà il supporto a NV-CONTROL per manipolare i MetaMode, ma causerà, per essere accurata, visibili frequenze di refresh a XRandR e a XF86VidMode.

### Nessun schermo trovato su un computer portatile e Nvidia Optimus

Su un computer portatile, se il driver nvidia non riesce a trovare lo schermo (no screen found), è probabile che siate in presenza di una configurazione che utilizza Nvidia Optimus: un chipset Intel collegato allo schermo e le uscite video, e una scheda Nvidia che fa tutto il lavoro duro e scrive per il chipset della memoria video.

Controllare se `$ lspci | grep VGA` restituisce un output simile a questo:

```
00:02.0 VGA compatible controller: Intel Corporation Core Processor Integrated Graphics Controller (rev 02)
01:00.0 VGA compatible controller: nVidia Corporation Device 0df4 (rev a1)

```

Dalla versione 319,12 Beta, i driver NVIDIA offrono il supporto ad Optimus [[2]](http://www.nvidia.com/object/linux-display-amd64-319.12-driver.html) con versioni del kernel 2.9 e superiori.

Un'altra soluzione è installare il driver [Intel](/index.php/Intel_(Italiano) "Intel (Italiano)") per gestire gli schermi, inoltre se si vuole che funzioni anche il software 3D si potrebbe utilizzare [Bumblebee](/index.php/Bumblebee_(Italiano) "Bumblebee (Italiano)") per fare in modo che essi utilizzino la scheda Nvidia.

#### Possibile Soluzione

Entrare nel BIOS e cambiare l'impostazione grafica di default da 'Optimus' a 'Discrete', ed il driver Nvidia installato (295,20-1 al momento della scrittura) riconosce gli schermi.

Passaggi:

1.  Entrare nel BIOS
2.  Trovare Graphics Settings (in alcuni casi è nella scheda *Config > Display*)
3.  Cambiare 'Graphics Device' in 'Discrete Graphics' (questo disabilita la scheda grafica Intel).
4.  Cambiare OS Detection di Nvidia Optimus in *Disabled*.
5.  Salvare ed uscire.

Testato su un Lenovo W520 con una Quadro 1000M e Nvidia Optimus.

### Schermo(i) trovati, ma nessuna configurazione utilizzabile

Su un computer portatile, a volte il driver NVIDIA non riesce a trovare lo schermo attivo. Esso può essere causato perché si possiede una scheda grafica con uscita VGA/TV. Si dovrebbe esaminare Xorg.0.log per vedere dov'è l'errore.

Un'altra cosa da provare è l'aggiunta di opzione che invalida `"ConnectedMonitor" Option` alla sezione `Section "Device"` per forzare Xorg a generare un errore e mostrare come correggerlo. [Qui](http://http.download.nvidia.com/XFree86/Linux-x86/304.51/README/xconfigoptions.html) potete trovate più informazioni sulle impostazioni di ConnectedMonitor.

Dopo il riavvio di X, controllare Xorg.0.log per ottenere i corretti valori di CRT-x,-x DFP, TV-x.

il comando `nvidia-xconfig --query-gpu-info` potrebbe esservi utile.

### Nessun controllo della luminosità sui portatili

aggiungete la seguente stringa in **20-nvidia.conf**

```
Option "RegistryDwords" "EnableBrightnessControl=1"

```

Se questa soluzione non dovesse funzionare, si può provare ad installare il pacchetto [nvidia-bl](https://aur.archlinux.org/packages/nvidia-bl/) o [nvidiabl](https://aur.archlinux.org/packages/nvidiabl/).

### Barre nere durante la riproduzione a schermo intero di video flash con la configurazione Twinview

Seguire le istruzioni riportate in questo articolo: [link](http://al.robotfuzz.com/content/workaround-fullscreen-flash-linux-multiheaded-desktops)

### La retroilluminazione non si spegne in alcune circostanze

Per impostazione predefinita, DPMS dovrebbe spegnere la retroilluminazione con il impostando un dato valore di tempo o eseguendo xset. Tuttavia, probabilmente a causa di un bug nei driver proprietari Nvidia, il risultato è una schermata vuota, senza nessun risparmio energetico. Una soluzione alternativa, fino a quando il bug non verrà corretto, è possibile utilizzare il `vbetool` come utente root.

Installare il pacchetto [vbetool](https://www.archlinux.org/packages/?name=vbetool).

Per spegnere lo schermo quando si desidera per poi riaccendere la retroilluminazione premendo un tasto a caso:

```
vbetool dpms off && read -n1; vbetool dpms on

```

In alternativa, xrandr è in grado di disattivare e riattivare le uscite monitor senza i permessi di root.

```
xrandr --output DP-1 --off; read -n1; xrandr --output DP-1 --auto

```

### Colori blu su video che utilizzano Flash

Un problema con le versioni 11.2.202.228-1 e 11.2.202.233-1 di [flashplugin](https://www.archlinux.org/packages/?name=flashplugin) causano l'invio dei pannelli U/V pannelli in un ordine incorretto, con una conseguente tinta blu per determinati video. Ci sono alcune correzioni potenziali per questo bug:

1.  Installare il pacchetto [libvdpau](https://www.archlinux.org/packages/?name=libvdpau).
2.  Patchare `vdpau_trace.so` con [questo makepkg](https://bbs.archlinux.org/viewtopic.php?pid=1078368#p1078368).
3.  Tasto destro del mouse su un video, selezionare "Impostazioni..." e spuntare "Abilita l'accelerazione hardware". Ricaricare la pagina per fare in modo che le modifiche abbiano effetto. Si noti che viene disabilitata l'accelerazione GPU.
4.  Effettuare un [downgrade](/index.php/Downgrading_packages_(Italiano) "Downgrading packages (Italiano)") di [flashplugin](https://www.archlinux.org/packages/?name=flashplugin) alla versione 11.1.102.63-1 o precedente.
5.  Utilizzare [google-chrome](https://aur.archlinux.org/packages/google-chrome/) con la nuova [pepper-flash](https://www.archlinux.org/packages/?name=pepper-flash)
6.  Provare una delle poche alternative Flash.

I meriti di ciascuno sono discussi in [questo thread](https://bbs.archlinux.org/viewtopic.php?id=137877).

### Bleeding Overlay con Flash

Questo bug è dovuto alla non corretta chiave di colore usata dalla versione 11.2.202.228-1 di [flashplugin](https://www.archlinux.org/packages/?name=flashplugin), e fa sì che i contenuti flash causino delle "perdite" in altre pagine o sfondi neri solidi. Per evitare questo problema è sufficiente installare il pacchetto [libvdpau](https://www.archlinux.org/packages/?name=libvdpau) oppure

```
esportare `VDPAU_NVIDIA_NO_OVERLAY=1` all'interno del profilo della vostra shell (ad esempio `~/.bash_profile` o `~/.zprofile`) o in `~/.xinitrc`

```

### Il sistema si blocca completamente utilizzando Flash

Se occasionalmente capita che il sistema si blocca completamente (soltanto il mouse si muove) durante l'utilizzo di flashplugin, e nel log riscontrate:

 `/var/log/errors.log` 
```
  NVRM: Xid (0000:01:00): 31, Ch 00000007, engmask 00000120, intr 10000000

```

Una possibile soluzione è quella di disabilitare l'accelerazione hardware di flash, impostando

 `/etc/adobe/mms.cfg` 
```
 EnableLinuxHWVideoDecode=0

```

Oppure, se si vuole mantenere l'accelerazione hardware abilitata , si può provare ad :

```
export VDPAU_NVIDIA_NO_OVERLAY=1

```

... prima di avviare il browser. Si noti che questo può introdurre tearing.

### Xorg fallisce il caricamento o appare una schermata rossa

Se si ottiene una schermata rossa e utilizzate grub2, disabilitare il framebuffer di grub2 modificando `/etc/defaults/grub`, de-commentando la stringa GRUB_TERMINAL_OUTPUT. Per maggiori informazioni vedere [Disabilitare il framebuffer](/index.php/GRUB2_(Italiano)#Disabilitare_il_framebuffer "GRUB2 (Italiano)").

### Schermo nero su sistemi con GPU integrate Intel

Se si dispone di una CPU Intel con GPU integrata (ad esempio Intel HD 4000) e ottiene una schermata nera al boot dopo l'installazione del pacchetto [nvidia](https://www.archlinux.org/packages/?name=nvidia), questo può essere causato da un conflitto tra i moduli grafici. Questo è risolto mettendo in blacklist i moduli per la GPU Intel. Creare il file `/etc/modprobe.d/blacklist.conf` e prevenire che i moduli *i915* e *intel_agp' vengano caricati all'avvio:*

 `/etc/modprobe.d/blacklist.conf` 
```
install i915 /bin/false
install intel_agp /bin/false

```

### Schermo nero su sistemi con GPU integrata VIA

Come sopra, mettere in blacklist il modulo *viafb* potrebbe risolvere i conflitti con i driver NVIDIA :

 `/etc/modprobe.d/blacklist.conf` 
```
install viafb /usr/bin/false

```

### X fallisce con "no screens found" una Intel iGPU

Se avete un processore Intel che integra anche una GPU e X fallisce all'avvio con :

```
[ 76.633] (EE) No devices detected.
[ 76.633] Fatal server error:
[ 76.633] no screens found

```

Allora è necessario aggiungere il BusID della scheda nvidia alla propria configurazione di X. Potete trovarlo con questo comando:

 `# lspci | grep VGA` 
```
 00:02.0 VGA compatible controller: Intel Corporation Xeon E3-1200 v2/3rd Gen Core processor Graphics Controller (rev 09)
 01:00.0 VGA compatible controller: NVIDIA Corporation GK107 [GeForce GTX 650] (rev a1)

```

Per risolvere il problema si aggiunga la propria scheda nella sezione `Device` nel file di configurazione di X, ad esempio:

 `/etc/X11/xorg.conf.d/10-nvidia.conf` 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BusID          "PCI:1:0:0"
EndSection

```

Si noti come `01:00.0` viene scritto come `1:0:0`.

### Xorg non fallisce durante l'avvio , ma il sistema si avvia comunque

Sui sistemi boot molto veloci , systemd può tentare di avviare il display manager prima che il driver NVIDIA sia completamente inizializzato. Verrà visualizzato un messaggio simile al seguente nei log solo quando Xorg viene eseguito durante l'avvio .

 `/var/log/Xorg.0.log` 
```
[     1.807] (EE) NVIDIA(0): Failed to initialize the NVIDIA kernel module. Please see the
[     1.807] (EE) NVIDIA(0):     system's kernel log for additional error messages and
[     1.808] (EE) NVIDIA(0):     consult the NVIDIA README for details.
[     1.808] (EE) NVIDIA(0):  *** Aborting ***
```

In questo caso sarà necessario stabilire una dipendenza ordinare dal display manager al dispositivo DRI . Prima di creare unità di periferica per dispositivi DRI creando un nuovo file di regole udev.

 `/etc/udev/rules.d/99-systemd-dri-devices.rules`  `ACTION=="add", KERNEL=="card*", SUBSYSTEM=="drm", TAG+="systemd"` 

Quindi creare la dipendenza dal display manager al dispositivo(i).

 `/etc/systemd/system/display-manager.service.d/10-wait-for-dri-devices.conf` 
```
[Unit]
Wants=dev-dri-card0.device
After=dev-dri-card0.device
```

Se si dispone di schede supplementari necessarie per il desktop, allora aggiungerle alle stringhe Wants e After separati da uno spazio.

## Link esterni

*   [NVIDIA forums](http://www.nvnews.net/vbulletin/forumdisplay.php?s=&forumid=14)
*   [Official readme for NVIDIA drivers](http://http.download.nvidia.com/XFree86/Linux-x86/1.0-7182/README/readme.txt)