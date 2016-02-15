Questo articolo riguarda l'installazione e la configurazione del driver Open Source [Nouveau](http://nouveau.freedesktop.org/wiki/) per schede video NVIDIA. Per informazioni sul driver proprietario ufficiale, vedere [NVIDIA](/index.php/NVIDIA_(Italiano) "NVIDIA (Italiano)").

## Contents

*   [1 Se avete i driver proprietari NVIDIA](#Se_avete_i_driver_proprietari_NVIDIA)
*   [2 Installazione](#Installazione)
*   [3 Caricamento](#Caricamento)
    *   [3.1 KMS](#KMS)
        *   [3.1.1 Avvio ritardato](#Avvio_ritardato)
        *   [3.1.2 Avvio anticipato](#Avvio_anticipato)
*   [4 Trucchi e Consigli](#Trucchi_e_Consigli)
    *   [4.1 Mantenere i driver NVIDIA installati](#Mantenere_i_driver_NVIDIA_installati)
    *   [4.2 Installazione dei pacchetti più recenti in sviluppo](#Installazione_dei_pacchetti_pi.C3.B9_recenti_in_sviluppo)
    *   [4.3 Problemi di tearing con il composite](#Problemi_di_tearing_con_il_composite)
    *   [4.4 Dual Head](#Dual_Head)
    *   [4.5 La risoluzione della console virtuale non corrisponde alla reale](#La_risoluzione_della_console_virtuale_non_corrisponde_alla_reale)
    *   [4.6 Gestione energetica](#Gestione_energetica)
    *   [4.7 Abilitare MSI (Message Signaled Interrupts)](#Abilitare_MSI_.28Message_Signaled_Interrupts.29)
    *   [4.8 Optimus](#Optimus)
*   [5 Risoluzione dei Problemi](#Risoluzione_dei_Problemi)
    *   [5.1 Problema delle uscite fantasma](#Problema_delle_uscite_fantasma)

## Se avete i driver proprietari NVIDIA

**Nota:** Questa sezione è solo per coloro che hanno i driver proprietari [NVIDIA](/index.php/NVIDIA_(Italiano) "NVIDIA (Italiano)") installato. Può essere saltata da tutti gli altri utenti.

**Suggerimento:** Se volete mantenere i driver NVIDIA installati, allora è richiesta una [ulteriore configurazione](#Mantenere_i_driver_NVIDIA_installati) per permettere il caricamento dei driver Nouveau al posto del driver NVIDIA.

```
 # pacman -Rdds nvidia nvidia-utils nvidia-libgl libvdpau libcl

```

Potrebbe essere necessario sostituire nvidia con nvidia-304xx se si sta utilizzando ramo legacy .

Assicurarsi di eliminare anche il file `/etc/X11/xorg.conf` che il driver Nvidia ha creato ( o annullare le modifiche ), altrimenti X non caricherà correttamente il driver Nouveau.

Si raccomanda inoltre di reinstallare [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) e [mesa](https://www.archlinux.org/packages/?name=mesa) poichè il driver proprietario potrebbe cambiare i file da essi forniti.

## Installazione

Prima di procedere bisogna contyrollare se la vostra scheda è [supportata](http://nouveau.freedesktop.org/wiki/CodeNames) (un elenco più dettagliato è disponibile su [Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_Nvidia_Graphics_Processing_Units "wikipedia:Comparison of Nvidia Graphics Processing Units")), inoltre si controlli anche la pagina [feature matrix](http://nouveau.freedesktop.org/wiki/FeatureMatrix/), per verificare quali funzioni sono supportate dal vostro disposito. Inoltre, assicurarsi di avere [Xorg](/index.php/Xorg_(Italiano) "Xorg (Italiano)") installato correttamente .

[Installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") il pacchetto [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau), che è disponibile nel [Depositi ufficiali](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)"). Il quale fornisce il driver DDX per l'accelerazione 2D e ha come dipendenza il pacchetto [mesa](https://www.archlinux.org/packages/?name=mesa) che fornisce il driver DRI per l'accelerazione 3D.

Per utilizzare applicazioni 32 bit con accelerazione 3D su Arch x86_64, installare [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) dal deposito [multilib](/index.php/Multilib "Multilib").

**Nota:** Fare riferimento alla [pagina Nouveau MesaDrivers](http://nouveau.freedesktop.org/wiki/MesaDrivers) prima di segnalare bug relativi all'accelerazione 3D.

## Caricamento

I modulo del kernel Nouveau dovrebbe caricarsi automaticamente senza problemi all'avvio del sistema.

Nel caso che questo non avvenga, allora:

*   Assicurarsi di non avere `nomodeset` o `vga=` tra i [parametri del kernel](/index.php/Kernel_parameters "Kernel parameters"), altrimenti il modulo Nouveau non sarà in grado di avviare con successo il kernel mode-setting (KMS). (si veda in seguito)
*   Controllare di non aver disabilitato il driver Nouveau utilizzando il metodo di blacklist tramite `/etc/modprobe.d/`.

### KMS

**Suggerimento:** Se avete problemi con la risoluzione , controllare [questa pagina](/index.php/Kernel_Mode_Setting#Forcing_modes_and_EDID "Kernel Mode Setting").

Il [Kernel Mode Setting](/index.php/Kernel_Mode_Setting "Kernel Mode Setting") (KMS) è richiesto dal driver Nouveau. All'avvio del sistema la risoluzione verrà cambiata quando il KMS inizializzerà il driver video. Semplicemente, installare il driver Nouveau dovrebbe essere sufficiente per ottenere al sistema di riconoscere e inizializzarlo nella modalità "avvio ritardato" (trattato in seguito). Si veda la pagina [Nouveau KerneModeSetting](http://nouveau.freedesktop.org/wiki/KernelModeSetting) per maggiori informazioni.

**Nota:** Molti utenti preferiscono abilitare il metodo di "avvio anticipato" in modo da non causare un cambio di risoluzione durante il processo di boot.

#### Avvio ritardato

Questo metodo consente di avviare il KMS dopo che gli altri moduli del kernel vengono caricati. Vedrete il testo "Caricamento moduli" (Loading modules) e la dimensione del testo può cambiare, possibilmente con un indesiderabile sfarfallio.

#### Avvio anticipato

Questo metodo avvierà KMS prima possibile nel processo di boot, quando [initramfs](/index.php/Initramfs "Initramfs") viene caricato. Qui c'è la descrizione di come farlo con i pacchetti originali:

A tale scopo, aggiungere `nouveau` alla riga `MODULES` in `/etc/mkinitcpio.conf`:

```
MODULES="... nouveau ..."

```

Se si utilizza un file EDID personalizzato, è necessario incorporarlo in initramfs così:

 `/etc/mkinitcpio.conf`  `FILES="/lib/firmware/edid/your_edid.bin"` 

Ri-generare l'immagine ramdisk iniziale:

```
# mkinitcpio -p <kernel prescelto, es. "linux">

```

Se si hanno problemi con i driver Nouveau, e si è costretti a ricostruire nouveau-drm diverse volte per scopi di test, non si aggiunga `nouveau` all' initramfs. È facile dimenticare di ricostruire l' initramfs e renderà qualsiasi test più difficile. Si usi perciò _avvio ritardato_. Ci potrebbero essere problemi addizionali con initramfs se si ha bisogno di un firmware (generalmente sconsigliato)

## Trucchi e Consigli

### Mantenere i driver NVIDIA installati

Se volete mantenere i driver NVIDIA proprietari, ma volete provare il driver nouveau, commentare la riga che mette il driver nouveau in blacklist in `/etc/modprobe.d/nouveau_blacklist.conf` modificandola come segue:

```
#blacklist nouveau

```

Istruire Xorg per caricare i driver nouveau al posto dei nvidia, creando il file `/etc/X11/xorg.conf.d/20-nouveau.conf` con il seguente contenuto:

```
Section "Device"
   Identifier "Nvidia card"
   Driver "nouveau"
EndSection

```

**Suggerimento:** É possibile utilizzare [questo script](/index.php/NVIDIA_(Italiano)#Passare_tra_i_driver_nvidia_e_nouveau "NVIDIA (Italiano)") se si ha l'intenzione di passare dai driver proprietari a quelli liberi molto spesso.

Se utilizzate il driver NVIDIA, e volete testare i Nouveau senza riavviare il sistema, allora assicurarsi che il modulo 'nvidia' non sia più caricato:

```
# rmmod nvidia

```

Caricare il modulo 'nouveau' :

```
# modprobe nouveau

```

Controllare che il caricamento sia andato a buon fine guardando l'output dei messaggi del kernel:

```
$ dmesg

```

### Installazione dei pacchetti più recenti in sviluppo

Potreste voler provare un driver in versione più recente (-git) tramite [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)"):

*   È possibile utilizzare [mesa-git](https://aur.archlinux.org/packages/mesa-git/) che vi permetterà l'installazione degli ultimi driver mesa (inclusi gli ultimi driver DRI).
*   È possibile utilizzare [xf86-video-nouveau-git](https://aur.archlinux.org/packages/xf86-video-nouveau-git/) che vi permetterà l'installazione degli ultimi driver DDX.
*   Potete inoltre provare ad installare una versione più recente del kernel, usando pacchetti come ad esempio [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/) nel quale il codice Nouveau DRM può avere delle prestazioni migliori.
*   Per avere le ultimissime modifiche di Nouveau, dovreste usare il pacchetto [linux-git](https://aur.archlinux.org/packages/linux-git/) da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)"), modificandone il PKGBUILD per puntare al repository proprio del progetto nouveau, che è attualmente questo: [git://anongit.freedesktop.org/git/nouveau/xf86-video-nouveau](git://anongit.freedesktop.org/git/nouveau/xf86-video-nouveau).

I sorgenti per le ultime versioni dei driver possono essere reperiti alla pagina [Nouveau Source](http://nouveau.freedesktop.org/wiki/Source).

### Problemi di tearing con il composite

Modificare il file `/etc/X11/xorg.conf.d/20-nouveau.conf`, e aggiungere quanto segue alla sezione `Device`:

```
Section "Device"
   Identifier "nvidia card"
   Driver "nouveau"
   Option "GLXVBlank" "true"
EndSection

```

### Dual Head

Nouveau supporta l'estensione xrandr per monitor multipli e per il modesetting. Si veda la pagina [RandR12](/index.php/RandR12 "RandR12") per i tutorial.

Qui c'è un modello completo dell'inizio di `/etc/X11/xorg.conf.d/20-nouveau.conf` per avviare 2 monitor nella modalità dual head. Si potrebbe preferire usare uno strumento grafico per configurare i monitor come proprietà-display-gnome (Sistema -> Preferenze -> Display).

 `/etc/X11/xorg.conf` 

```
# the right one
Section "Monitor"
          Identifier   "NEC"
          Option "PreferredMode" "1280x1024_60.00"
EndSection

# the left one
Section "Monitor"
          Identifier   "FUS"
          Option "PreferredMode" "1280x1024_60.00"
          Option "LeftOf" "NEC"
EndSection

Section "Device"
    Identifier "nvidia card"
    Driver "nouveau"
    Option  "Monitor-DVI-I-0" "NEC"
    Option  "Monitor-DVI-I-1" "FUS"
EndSection

Section "Screen"
    Identifier "screen1"
    Monitor "NEC"
    DefaultDepth 24
      SubSection "Display"
       Depth      24
       Virtual 2560 2048
      EndSubSection
    Device "nvidia card"
EndSection

Section "ServerLayout"
    Identifier "layout1"
    Screen "screen1"
EndSection

```

### La risoluzione della console virtuale non corrisponde alla reale

Tramite l'utility [fbset](https://www.archlinux.org/packages/?name=fbset) è possibile regolare la risoluzione della console.

Inoltre è possibile impostare la risoluzione passando al kernel l'opzione **video=**. Vedere la pagina relativa a [KMS](/index.php/KMS "KMS") per ulteriori informazioni.

### Gestione energetica

Lo scaling GPU per la gestione energetica è in varie fasi di sviluppo a seconda della GPU. Si veda la pagina [Nouveau PowerManagement](http://nouveau.freedesktop.org/wiki/PowerManagement) per ulteriori informazioni.

### Abilitare MSI (Message Signaled Interrupts)

Questa opzione può fornire un vantaggio in termini di prestazioni ed è supportato solo su schede NV50 e superiori, di default è disattivato.

**Attenzione:** Questa procedura può causare instabilità con qualche combinazione di scheda madre/GPU.

Inserire la seguente linea in `/etc/modprobe.d/nouveau.conf`:

```
options nouveau msi=1

```

Se si utilizza l'[avvio anticipato](#Avvio_anticipato) per il supporto al KMS, aggiungere la stringa `FILES="/etc/modprobe.d/nouveau.conf"` al file `/etc/mkinitcpio.conf` e rigenerare l'immagine del kernel:

```
# mkinitcpio -p <kernel prescelto, es. linux>

```

Riavviare il sistema affinché le modifiche abbiano effetto.

### Optimus

Ci sono due soluzioni per utilizzare [Optimus](/index.php/Optimus "Optimus") su un computer portatile (ovvero grafica ibrida, quando si dispone di due GPU sul proprio laptop) : [blumbebee](/index.php/Bumblebee_(Italiano) "Bumblebee (Italiano)") e [PRIME](/index.php/PRIME "PRIME").

## Risoluzione dei Problemi

Aggiungere `drm.debug=14` e `log_buf_len=16M` ai [parametri del kernel](/index.php/Kernel_parameters "Kernel parameters") per attivare il debug video

Creare un file di log dettagliato per Xorg:

```
$ startx -- -logverbose 9 -verbose 9

```

Visualizza i parametri e i valori caricati dal modulo video:

```
$ modinfo -p video

```

#### Problema delle uscite fantasma

È possibile che il driver nouveau per rilevi delle uscite "fantasma". Ad esempio, vengono visualizzate come collegati sia VGA-1 che LVDS-1, ma solo LVDS-1 è realmente presente.

Questo provoca problemi di visualizzazione e di uno schermo danneggiato.

Il problema può essere superato disabilitando l'uscita fantasma (VGA-1 nell'esempio riportato) sulla riga di comando del kernel del boot loader. Ciò può essere ottenuto aggiungendo la seguente opzione:

```
video=VGA-1:d

```

Dove **d** = disabilita.

L'uscita fantasma può anche essere disattivata in X aggiungendo quanto segue in `/etc/X11/xorg.conf.d/20-nouveau.conf` :

```
Section "Monitor"
Identifier "VGA-1"
Option "Ignore" "1"
EndSection

```

**Fonte:** [http://gentoo-en.vfose.ru/wiki/Nouveau#Phantom_and_unpopulated_output_connector_issues](http://gentoo-en.vfose.ru/wiki/Nouveau#Phantom_and_unpopulated_output_connector_issues)