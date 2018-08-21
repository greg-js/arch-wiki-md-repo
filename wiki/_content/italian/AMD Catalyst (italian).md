Articoli correlati

*   [ATI (Italiano)](/index.php/ATI_(Italiano) "ATI (Italiano)")
*   [Intel (Italiano)](/index.php/Intel_(Italiano) "Intel (Italiano)")
*   [NVIDIA (Italiano)](/index.php/NVIDIA_(Italiano) "NVIDIA (Italiano)")
*   [Xorg (Italiano)](/index.php/Xorg_(Italiano) "Xorg (Italiano)")

I possessori di schede video **ATI/AMD** possono scegliere tra i driver proprietari ATI ([Catalyst](https://aur.archlinux.org/packages/Catalyst/)) e i [driver opensource](/index.php/ATI_(Italiano) "ATI (Italiano)") ([xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati)). Questo articolo tratta i driver proprietari.

Conosciuti precedentemente come *fglrx*(**F**ire**GL** and **R**adeon **X**), ATI ha ribattezzato i suoi driver proprietari Linux, che sono ora noti come *Catalyst*. Attualmente solo il nome dei pacchetti è cambiato, mentre il modulo del kernel mantiene il nome originale *fglrx.ko*, perciò ogni riferimento a fglrx da qui in poi sarà specificatamente riferito al modulo del kernel, **non al pacchetto**.

Un tempo, catalyst era un pacchetto precompilato scaricabile dal repostory [extra] di Arch Linux, ma da Marzo 2009, il [supporto ufficiale è stato abbandonato](https://www.archlinux.org/news/ati-catalyst-support-dropped/) a causa della poco soddisfacente qualità e velocità in termini di sviluppo di questo driver proprietario. Da ottobre 2012, tali driver sono rientrati nei [repositories ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)"), più precisamente in [community]. Ad aprile 2013, i *catalyst* sono di nuovo usciti dai repositories ufficiale e, probabilmente, non ci rientreranno più.

Comparando i Catalyst con i driver open source, si nota che i driver open source hanno performance 2D migliori. Le parti si invertono se si passa a considerare l'accelerazione 3D, dove i Catalyst hanno la meglio.Nella versione [Radeon](https://en.wikipedia.org/wiki/Radeon "wikipedia:Radeon"), ATI ha rielaborato lo schema identificativo per collegare ogni prodotto ad un determinato segmento di mercato. Dalla versione **9.4**, i drivers proprietari ATI **supportano solo schede R600 o più recenti** (il che significa, **HD2xxx** o **più nuove**). Per schede video più datate è disponibile solo il driver open source[xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati). In questa guida, i lettori avranno modo di vedere sia i nomi del *product* (es. HD 4850, X1900) sia i nomi *code* o *core* (es. RV770, R580). Per ulteriori informazioni sui prodotti ATI consultare [Wikipedia:Comparison of AMD graphics processing units](https://en.wikipedia.org/wiki/Comparison_of_AMD_graphics_processing_units "wikipedia:Comparison of AMD graphics processing units"). Vedere anche la [wiki di Xorg](http://www.x.org/wiki/RadeonFeature#Decoder_ring_for_engineering_vs_marketing_names).

## Contents

*   [1 Installazione](#Installazione)
    *   [1.1 Installare i driver](#Installare_i_driver)
        *   [1.1.1 Installazione dal repository non ufficiale](#Installazione_dal_repository_non_ufficiale)
        *   [1.1.2 Installazione da AUR](#Installazione_da_AUR)
    *   [1.2 Configurazione dei driver](#Configurazione_dei_driver)
        *   [1.2.1 Configurare X](#Configurare_X)
        *   [1.2.2 Caricare moduli al boot](#Caricare_moduli_al_boot)
        *   [1.2.3 Disabilitare mode setting](#Disabilitare_mode_setting)
        *   [1.2.4 Controlli](#Controlli)
    *   [1.3 Kernel personalizzati](#Kernel_personalizzati)
    *   [1.4 Supporto a PowerXpress](#Supporto_a_PowerXpress)
        *   [1.4.1 Running two X servers (one using the Intel driver, another one using fglrx) simultaneously (inglese)](#Running_two_X_servers_.28one_using_the_Intel_driver.2C_another_one_using_fglrx.29_simultaneously_.28inglese.29)
        *   [1.4.2 Issues with PowerXpress laptops running in AMD mode (pxp_switch_catalyst amd) with external / secondary monitor (inglese)](#Issues_with_PowerXpress_laptops_running_in_AMD_mode_.28pxp_switch_catalyst_amd.29_with_external_.2F_secondary_monitor_.28inglese.29)
*   [2 Repository xorg-server](#Repository_xorg-server)
    *   [2.1 [xorg114]](#.5Bxorg114.5D)
    *   [2.2 [xorg113]](#.5Bxorg113.5D)
    *   [2.3 [xorg112]](#.5Bxorg112.5D)
*   [3 Strumenti](#Strumenti)
    *   [3.1 Catalyst-hook](#Catalyst-hook)
    *   [3.2 Catalyst-generator](#Catalyst-generator)
*   [4 Caratteristiche](#Caratteristiche)
    *   [4.1 Desktop senza Tearing](#Desktop_senza_Tearing)
    *   [4.2 Accelerazione video](#Accelerazione_video)
    *   [4.3 Strumenti per la frequenza GPU/Mem, Temperatura, Velocità ventole, Overclock utilities](#Strumenti_per_la_frequenza_GPU.2FMem.2C_Temperatura.2C_Velocit.C3.A0_ventole.2C_Overclock_utilities)
    *   [4.4 Double Screen (Dual Head / Dual Screen / Xinerama)](#Double_Screen_.28Dual_Head_.2F_Dual_Screen_.2F_Xinerama.29)
        *   [4.4.1 Introduzione](#Introduzione)
        *   [4.4.2 ATI Catalyst Control Center](#ATI_Catalyst_Control_Center)
        *   [4.4.3 Installazione](#Installazione_2)
        *   [4.4.4 Configurazione](#Configurazione)
*   [5 Risoluzione problemi](#Risoluzione_problemi)
    *   [5.1 Freeze delle applicazioni 3D Wine](#Freeze_delle_applicazioni_3D_Wine)
    *   [5.2 Problemi con i colori video](#Problemi_con_i_colori_video)
    *   [5.3 KWin e composite](#KWin_e_composite)
    *   [5.4 Schermo nero con completo blocco dopo riavvio o startx](#Schermo_nero_con_completo_blocco_dopo_riavvio_o_startx)
        *   [5.4.1 Chiamate hardware ACPI difettose](#Chiamate_hardware_ACPI_difettose)
    *   [5.5 KDM scompare dopo il logout](#KDM_scompare_dopo_il_logout)
    *   [5.6 Il Direct Rendering non funziona](#Il_Direct_Rendering_non_funziona)
    *   [5.7 Problemi con l'ibernazione/sospensione](#Problemi_con_l.27ibernazione.2Fsospensione)
        *   [5.7.1 La parte video fallisce nel tentativo di di riprendersi dal suspend2ram](#La_parte_video_fallisce_nel_tentativo_di_di_riprendersi_dal_suspend2ram)
    *   [5.8 Blocco del sistema/Hard lock](#Blocco_del_sistema.2FHard_lock)
    *   [5.9 Conflitti hardware](#Conflitti_hardware)
    *   [5.10 Blocchi temporanei durante l'esecuzione di video](#Blocchi_temporanei_durante_l.27esecuzione_di_video)
    *   [5.11 "aticonfig: No supported adaptaters detected"](#.22aticonfig:_No_supported_adaptaters_detected.22)
    *   [5.12 Supporto a WebGL in Chromium](#Supporto_a_WebGL_in_Chromium)
    *   [5.13 Freeze guardando video flash con flashplugin](#Freeze_guardando_video_flash_con_flashplugin)
    *   [5.14 Artefatti e movimenti lenti delle finestre con GNOME 3](#Artefatti_e_movimenti_lenti_delle_finestre_con_GNOME_3)
    *   [5.15 Impossibile usare la modalità fullscreen con risoluzione 1920x1080](#Impossibile_usare_la_modalit.C3.A0_fullscreen_con_risoluzione_1920x1080)
*   [6 Altre risorse](#Altre_risorse)

## Installazione

Ci sono 2 modi per installare Catalyst sul proprio sistema. Il primo metodo è usare il repository non ufficiale di Vi0L0 (il maintainer di Catalyst su AUR) che contiene tutti i pacchetti possibili per Arch Linux. Il secondo metodo prevede la compilazione dei pacchetti da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").

Prima di scegliere la modalità di installazione è necessario capire di quale driver si ha bisogno. Dalla release 12.4 di Catalyst, AMD ha deciso di prosdeguire in modo distinto lo sviluppo per le schede Radeon HD superiori alla serie 5xxx e per le schede Radeon HD 4xxx, 3xxx e 2xxx. Per queste ultime esiste il driver **legacy**, mentre per le Radeon HD 5xxx (e successive) usare il "normale" pacchetti *Catalyst*.

**Nota:** In seguito alle istruzioni per ogni tipo di installazione possibile, si troverà una sezione che tratta la configurazione che dovrà essere seguita a prescindere dal metodo scelto per l'installazione.

### Installare i driver

#### Installazione dal repository non ufficiale

Se non si è molto convinti di voler compilare tutto, la via più semplice è l'utilizzo del repository non ufficiale mantenuto dall'utente ViOlO. I pacchetti qui presenti sono firmati quindi il loro utilizzo è considerabile sicuro. Vi0L0 è responsabile di molti pacchetti che possono aiutare parecchio durante la configurazione di Catalyst su Arch Linux.

I repositories sono tre:

*   [catalyst](/index.php/Unofficial_user_repositories#catalyst "Unofficial user repositories") per schede Radeon HD >= 5xxx (contiene solo l'ultima release di Catalyst (stabile o beta));
*   *catalyst-stable*; contiene l'ultima release stabile dei Catalyst per schede HD 5xxx.
*   [catalyst-hd234k](/index.php/Unofficial_user_repositories#catalyst-hd234k "Unofficial user repositories"); per schede Radeon HD <= 4xxx.

Per abilitare uno di questi, seguire le istruzioni di [Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories"). Ricordarsi che ogni repository non ufficiale, va aggiunto DOPO i [repositories ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)") nel file `/etc/pacman.conf`.

**Nota:** I repositories *catalyst* e *catalyst-stable* condividono lo stesso link, quindi, per abilitare *catalyst-stable*, seguire le istruzioni per abilitare *catalyst* e rimpiazzare `catalyst` con `[catalyst-stable]` in `pacman.conf`. Se si ha la necessità di usare un driver più vecchio, si può usare un repository con il numero di versione del driver necessario, con lo stesso URL, ad esempio: *catalyst-stable-13.4*.

**Attenzione:**

*   Il driver Legacy non supporta Xorg 1.13\. Se si deve usare questo driver sarà necessario installare una versione vecchia di Xorg. Vedere la sezione [#Repository xorg-server](#Repository_xorg-server) per maggiori informazioni su come effettuare rollback a Xorg 1.12
*   Catalyst non supporta Xorg 1.15, vedere la sezione [#Repository xorg-server](#Repository_xorg-server) e scegliere il repository più appropriato per il proprio sistema.

**Tip:** Siccome catalyst.wirephire.com spesso va offline in caso di traffico dati elevato (in passato succedeva molto spesso) o potrebbe essere molto lento, esistono dei mirrors creati da yanom: [[1]](http://70.239.162.206/catalyst-mirror) (USA) e rtsinformatique: [[2]](http://mirror.rts-informatique.fr/archlinux-catalyst/) (Francia). Di tali mirror tuttavia non si hanno garanzie di funzionamento e aggiornamento. Decommentare il mirror più vicino alla proprio posizione geografica. Potrebbe essere una buona idea usare o uno o l'altro in caso di malfunzionamento di uno dei due.

Una volta aggiunti i repositories Catalyst necessari, aggiornare il database di pacman, quindi [installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") i seguenti pacchetti: (vedere [#Strumenti](#Strumenti) per maggiori informazioni):

*   *catalyst-hook*
*   *catalyst-utils*
*   *lib32-catalyst-utils* - opzionale, necessario per il supporto OpenGL 32-bit OpenGL su sistemi a 64-bit.

Se si usa un notebook con una grafica ibrida Intel/AMD installare questi pacchetti

*   *catalyst-hook*
*   *catalyst-utils-pxp*
*   *lib32-catalyst-utils-pxp* - opzionale, necessario per il supporto OpenGL 32-bit OpenGL su sistemi a 64-bit.

**Nota:** Se pacman dovesse chiedere di rimuovere il pacchetto **libgl** rispondere affermativamente.

**Attenzione:** Il pacchetto **catalyst** è stato rimosso dal repository di Vi0L0, al suo posto ora c'è **catalyst-hook**.

#### Installazione da AUR

Il secondo metodo per ottenere Catalyst, come detto è la compilazione tramite [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)"). Nel caso si voglia compilare i pacchetti in modo specifico per il proprio sistema questa è la via da seguire. Va ricordato che ad ogni aggiornamento i driver vanno ricompilati, quindi è il metodo che richiede più sforzi da parte dell'utente finale.

**Attenzione:** Se si sceglie di installare Catalyst tramite AUR sarà necessario ricompilare il pacchetto ad ogni aggiornamento del kernel. In caso contrario X potrebbe fallire l'avvio.

Tutte le informazioni scritte nel paragrafo precedente riguardante il repository non ufficiale di Vi0L0 sono valide anche per i pacchetti AUR:

*   [Catalyst](https://aur.archlinux.org/packages/Catalyst/)
*   [Catalyst-generator](https://aur.archlinux.org/packages/Catalyst-generator/)
*   [Catalyst-hook](https://aur.archlinux.org/packages/Catalyst-hook/)
*   [Catalyst-utils](https://aur.archlinux.org/packages/Catalyst-utils/)
*   [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/)

AUR inoltre contiene pacchetti che **non** si trovano su alcun repositories. Questi pacchetti sono:

*   [Catalyst-total-hd234k](https://aur.archlinux.org/packages/Catalyst-total-hd234k/)
*   [Catalyst-total](https://aur.archlinux.org/packages/Catalyst-total/)
*   [Catalyst-test](https://aur.archlinux.org/packages/Catalyst-test/)
*   [Catalyst-total-pxp](https://aur.archlinux.org/packages/Catalyst-total-pxp/)

Il pacchetto [catalyst-total](https://aur.archlinux.org/packages/catalyst-total/) serve a semplificare il più possibile la vita all'utente in quanto un solo pacchetto fornisce: driver, kernel utilities, utilities 32 bit. Tale pacchetto, compila anche [catalyst-hook](https://aur.archlinux.org/packages/catalyst-hook/), come descritto in [#Strumenti](#Strumenti).

[Catalyst-total-pxp](https://aur.archlinux.org/packages/Catalyst-total-pxp/) serve per compilare Catalyst con il supporto sperimentale a powerXpress.

Per maggiori informazioni circa l'utilizzo di AUR, consultare la relativa pagina wiki: [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").

### Configurazione dei driver

Dopo aver correttamente installato i pacchetti necessari con il proprio metodo preferito, sarà necessario configurare X in modo che lavori con i Catalyst, si dovrà essere certi che i moduli necessari vengano caricati al boot e si rendererà fondamentale disabilitare il [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting").

#### Configurare X

Per la configurazione di X si dovrà creare il file `xorg.conf`. Catalyst porta con se uno strumento molto potente: `aticonfig` che è in grado di generare, modificare e amministrare tale file. Ogni aspetto della propria scheda video inoltre è configurabile tramite `/etc/ati/amdpcsdb`. Per la lista completa delle opzioni del comando `aticonfig` eseguire:

```
# aticonfig --help | less

```

**Attenzione:** Si utilizzi l'opzione `--output` in modo da generare un file di prova e se ne verifichi il contenuto prima di copiarlo all'interno di `/etc/X11/xorg.conf`, in quanto la presenza di quest'ultimo renderà inutilizzate le impostazioni presenti nei file all'interno della directory `/etc/X11/xorg.conf.d`.

Ora, per iniziare la configurazione, se si ha un solo monitor, eseguire:

```
# aticonfig --initial

```

**Nota:** se si hanno problemi con PowerXpress assicurarsi di aver installato [catalyst-total-pxp](https://aur.archlinux.org/packages/catalyst-total-pxp/).

Se si hanno due monitor invece si può eseguire il comando qui sotto. Si noti però che lanciare tale comando farà si che i due monitor saranno configurati come "dual head", con il secondo schermo sopra il primo:

```
# aticonfig --initial=dual-head --screen-layout=above

```

**Nota:** Vedere [#Double Screen (Dual Head / Dual Screen / Xinerama)](#Double_Screen_.28Dual_Head_.2F_Dual_Screen_.2F_Xinerama.29) per maggiori informazioni sulla configurazione per i due monitor.

Ora è possibile comparare il file `xorg.conf` con un [file d'esempio](/index.php/Xorg_(Italiano)#Xorg.conf_di_esempio "Xorg (Italiano)").

La nuova versione di Xorg, rileva automaticamente molte delle opzioni specificate al suo avvio. Sarà quindi necessario esplicitarne solo poche in caso di cambiamenti di versione.

Qui è presente un file con delle note **per un confronto** veloce. Le voci dopo `#` potrebbero essere necessarie, quelle dopo `##` sono fondamentali:

 `/etc/X11/xorg.conf` 
```
Section "ServerLayout"
        Identifier     "Arch"
        Screen      0  "Screen0" 0 0          # lo 0 è necessario
EndSection
Section "Module"
        Load ...
        ...
EndSection
Section "Monitor"
        Identifier   "Monitor0"
        ...
EndSection
Section "Device"
        Identifier  "Card0"
        Driver      "fglrx"                         #
        BusID       "PCI:1:0:0"                     # Raccomandato se "autodetect" dovesse fallire
        Option      "OpenGLOverlay" "0"             ##
        Option      "XAANoOffscreenPixmaps" "false" ##
        Option      "UseInternalAGPGart"    "no"    ## Deprecato
        Option      "KernelModuleParm"  "agplock=0" ## se il supporto AGP GART è rimosso
EndSection
Section "Screen"
        Identifier "Screen0"
        Device     "Card0"
        Monitor    "Monitor0"
        DefaultDepth    24
        SubSection "Display"
                Viewport   0 0
                Depth     24                        # non modificare '24'
                Modes "1280x1024" "2048x1536"       ## 1° valore=risoluzione di default, 2°=massima.
                Virtual 1664 1200                   ## (x+64, y) to workaround potential OGL rect. artifacts/
        EndSubSection                               ## fixed in Catalyst 9.8
EndSection
Section "DRI"
        Mode 0666                                   # potrebbe tornare utile per abilitare il rendering diretto.
EndSection
```

**Nota:** Dopo **ogni** aggiornamento di Catalyst sarà necessario rimuovere `amdpcsdb` in questo modo: killare X, rimuovere `/etc/ati/amdpcsdb`, avviare X e lanciare `amdpcsdb`.

*Se si desiderano maggiori informazioni visitare questo [link](https://bbs.archlinux.org/viewtopic.php?id=57084).*

#### Caricare moduli al boot

Si dovrà blacklistare il modulo `radeon` in `/etc/modprobe.d/modprobe.conf`. Per maggiori informazioni consultare la pagina [Modprobe](/index.php/Modprobe "Modprobe") e [kernel modules#Blacklisting](/index.php/Kernel_modules#Blacklisting "Kernel modules").

Assicurarsi che il modulo `radeon` non sia presente in alcun file nella directory `/etc/modules-load.d/`, quindi aggiungere `fglrx` in una nuova riga di un file esistente in `/etc/modules-load.d/` e crearne uno apposito.

#### Disabilitare mode setting

**Nota:** Non farlo se si usa `catalyst-utils-pxp` o `catalyst-total-pxp` perchè i driver intel necessitano del KMS.

Per disabilitare il [KMS](/index.php/KMS "KMS") aggiungere `nomodeset` alla riga del kernel. Questa operazione è molto importante in quanto con KMS attivo si rischiano freeze del sistema durante operazioni come spegnimento, riavvio, sospensione...

Per disabilitare il Kernel Mode Setting, aggiungere `nomodeset` ai [parametri del kernel](/index.php/Kernel_parameters "Kernel parameters").

#### Controlli

Supponendo che il login sia andato bene, il comando per vedere se fglrx è stato caricato e sia correttamente attivo è:

```
$ lsmod | grep fglrx
$ fglrxinfo   

```

Infine, eseguire Xorg con `startx` o utilizzando GDM/KDM, e verificare che il direct rendering sia attivato eseguendo il seguente comando in un terminale:

```
$ glxinfo | grep direct

```

Se si riceve "direct rendering: yes" allora tutto è funzionante! Se il comando `glxinfo` non è trovato, si potrebbe aver bisogno di installare il pacchetto [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos).

**Nota:** Come alternativa è possibile usare:
```
$ fg_glxears

```
per testare glxears

**Attenzione:** In alcune versioni recenti di Xorg, i percorsi delle librerie sono cambiati. Quindi, a volte `libGL.so` non può essere caricato correttamente anche se installato. Non dimenticare di controllare ciò se qualcosa non funziona. Leggere la sezione [#Risoluzione problemi](#Risoluzione_problemi) per dettagli.

### Kernel personalizzati

**Nota:** Se non si ha esperienza o confidenza compilando pacchetti, consulatare la sezione [ABS](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)") del wiki per una guida esaustiva sul metodo da impiegare.

Per installare catalyst su un kernel modificato, occorrerà compilare un proprio pacchetto `catalyst-$kernel` contenente il modulo del kernel compilato specificamente per il proprio kernel.

1.  Scaricare per prima cosa `PKGBUILD` e `catalyst.install` da [AUR](https://aur.archlinux.org/packages.php?ID=29111).

1.  Modificare il PKGBUILD. Bisognerà apportare queste tre modifiche:
    1.  Cambiare `pkgname=catalyst` in `pkgname=catalyst-KERNEL_NAME` dove KERNEL_NAME è il nome che si preferisce (es. IlMioBelKernel)
    2.  Cambiare la dipendeza `linux` in `$kernel_name`.

1.  Infine compilare ed installare il pacchetto. (`makepkg -i` o `makepkg` seguito da `pacman -U pkgname.pkg.tar.gz`

**Nota:**

*   Avendo installati diversi kernel, bisognerà installare i drivers Catalyst su tutti. Non andranno in conflitto tra loro.
*   Catalyst-generator è in grado di rigenerare `catalyst-{kernver}` quindi non sarà necessario rifare questa procedura sempre. Per maggiori informazioni, seguire la sezione [strumenti](#Strumenti).

### Supporto a PowerXpress

La tecnologia PowerXpress permette di switchare da schede grafiche integrate (IGP) a schede discrete sui notebooks, aumentando così la durata della batteria e migliorare le capacità 3D.

Per usare questa funzione su Arch Linux:

*   Installare [catalyst-total-pxp](https://aur.archlinux.org/packages/catalyst-total-pxp/) da [AUR](/index.php/AUR "AUR"), or
*   Installare **catalyst-utils-pxp** dal repository [catalyst] (più **lib32-catalyst-utils-pxp**, se necessario).

Per abilitare lo switch su schede integrate Intel, installare i pacchetti [mesa-libgl](https://www.archlinux.org/packages/?name=mesa-libgl), [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) e [mesa](https://www.archlinux.org/packages/?name=mesa).

**Nota:** **La nuova release di Catalyst (13.1) (no Catalyst legacy) supporta xorg-xserver 1.13.1, mesa 9.0.1 e xf86-video-intel 2.20.18**

Con le versioni precedenti di Catalyst ci sono alcuni problemi con le ultime release dei driver Intel e, per adesso, l'ultima versione funzionante è la **xf86-video-intel-2.20.2-2**, quindi si dovrà procedere al downgrade se si stanno utilizzando gli ultimi rilasciati dai repo di Arch (in ogni caso provare ad ogni aggiornamento i nuovi driver, potrebbero funzionare).

È possibile usare **xf86-video-intel 2.20.2-2** da [qui](http://catalyst.apocalypsus.net/files/xf86-video-intel-2.20.2/); scaricare il pacchetto sul proprio sistema e installarlo con `pacman -U`.

Notare che **xf86-video-intel 2.20.2-2** funziona con **xorg-server 1.12**, quindi sarà necessario effettuare il downgrade anche di questo pacchetto. Per altre informazioni, vedere [[#Il repository [xorg]]].

Ora si può switchare tra le due GPU così:

```
# aticonfig --px-igpu    # GPU integrata
# aticonfig --px-dgpu    # GPU discreta
```

Ricordarsi che fglrx va configurato in `/etc/X11/xorg.conf`.

È possibile installare anche **pxp_switch_catalyst** che è uno script per lo switch che permette anche maggiori funzioni:

*   Switching xorg.conf - it will rename xorg.conf into xorg.conf.cat (if there's fglrx inside) or xorg.conf.oth (if there's intel inside) and then it will create a symlink to xorg.conf, depending on what you chose.
*   Running `aticonfig --px-Xgpu`.
*   Running `switchlibGL`.
*   Adding/removing fglrx into/from `/etc/modules-load.d/catalyst.conf`.

Uso:

```
# pxp_switch_catalyst amd
# pxp_switch_catalyst intel
```

Se si hanno problemi lanciando X con la scheda Intel, prvare a forzare l'accelerazione **UXA**; quindi inserire quanto segue in `xorg.conf`

```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
   #Option      "AccelMethod"  "sna"
   Option      "AccelMethod"  "uxa"
   #Option      "AccelMethod"  "xaa"
EndSection
```

#### Running two X servers (one using the Intel driver, another one using fglrx) simultaneously (inglese)

Because fglrx is crash-prone (regarding PowerXpress), it could be a good idea to use the Intel driver in the main X server and have a secondary X server using fglrx when 3D acceleration is needed. However, simply switching to the discrete GPU from the integrated GPU using `aticonfig` or `amdcccle` will cause all sorts of weird bugs when starting the second X.

To run two X servers at the same time (each using different drivers), you should firstly set up a fully working X with Catalyst and then move its `xorg.conf` to a temporary place (for example, `/etc/X11/xorg.conf.fglrx`. The next time X is started, it will use the Intel driver by default instead of fglrx.

To start a second X server using fglrx, simply move `xorg.conf` back to the proper place (`/etc/X11/xorg.conf`) before starting X. This method even allows you to switch between running X sessions. When you are done using fglrx, move `xorg.conf` somewhere else again.

The only disadvantage of this method is not having 3D acceleration using the Intel driver. 2D acceleration, however, is fully functional. Other than that, this will provide us with a completely stable desktop.

#### Issues with PowerXpress laptops running in AMD mode (pxp_switch_catalyst amd) with external / secondary monitor (inglese)

When using a PowerXpress laptop in AMD-only mode (ie, setting the discrete card to render everything) you sometimes run into issues with artifacting/duplicating between displays. This is a known issue, and seems to effect 7xxxM series cards.

The artifacting disappears when you transform one of the monitors by either rotating or scaling. So you can use xrandr to fix this:

 `xrandr --output HDMI1 --left-of LVDS1 --primary --scale 1x1 --output LVDS1 --scale 1.0001x1.0001` 

## Repository xorg-server

È noto che Catalyst abbia uno sviluppo molto lento. È facile che un aggiornamento di tale pacchetto interrompa la compatibilità con Xorg. Questo significa che gli utenti di Catalyst devono bloccare l'aggiornamento di X o usare dei repo, anch'essi gestiti da Vi0L0, che mantengano una versione di X compatibile con Catalyst.

Se si intende aggiornare normalmente la propria Arch Linux si dovrà ricorrere a un repository esterno. Ognuno di questi repositories dovrà essere aggiunto a `/etc/pacman.conf` sopra ogni altro repo ma sotto all'eventuale [Catalyst].

### [xorg114]

Catalyst < 14.1 non supporta xorg-server 1.15.

```
[xorg114]
Server = http://catalyst.wirephire.com/repo/xorg114/$arch

```

### [xorg113]

Catalyst < 13.6 non supporta xorg-server 1.14.

```
[xorg113]
Server = http://catalyst.wirephire.com/repo/xorg113/$arch

```

### [xorg112]

Catalyst < 12.10 al momento non supporta xorg-server 1.13

```
[xorg112]
Server = http://catalyst.wirephire.com/repo/xorg112/$arch
```

## Strumenti

### Catalyst-hook

Con [catalyst-hook](https://aur.archlinux.org/packages/catalyst-hook/) la funzione di ricompilazione automatica è affidata all' HOOKS **fglrx** tramite [mkinitcpio](/index.php/Mkinitcpio_(Italiano) "Mkinitcpio (Italiano)"). *Questo sostanzialmente è la stessa cosa che fa catalyst-dkms da [community]*. Prima di aggiornare il modulo fglrx, si aggiorni il pacchetto [linux-headers](https://www.archlinux.org/packages/?name=linux-headers).

Questo hook richiamerà il comando **catalyst_build_module** per aggiornare il modulo fglrx alla versione del proprio nuovo kernel, ed in aggiunta lancerà il comando *catalyst_build_module remove* per rimuovere i moduli fglrx non più necessari.

**Nota:** Se si utilizza questa funzionalità è **importante** controllare il processo di installazione di **linux** (o qualsiasi altro kernel). fglrx-hook vi informerà dell'esito positivo.

**Nota:** Se state utilizzando un **kernel personalizzato** e si utilizza un file di configurazione di mkinitcpio **non standard** (Es. il linux-zen utilizza `/etc/mkinitcpio-zen.conf`), bisogna aggiungere manualmente **fglrx** alla stringa *HOOKS* nel file di configurazione per abilitare l'auto-ricompilazione all'aggiornamento del kernel.

**Nota:** Se si sta usando un kernel non stock, è necessario rimuovere *linux-header* da `SyncFirst` in `/etc/pacman.conf` dopo aver eseguito 'catalyst_build_module auto'.

### Catalyst-generator

[catalyst-generator](https://aur.archlinux.org/packages/catalyst-generator/) è un pacchetto in grado di costruire e installare i moduli *fglrx* generando un pacchetto fruibile da pacman. La differenza tra questo metodo e catalyst-hook è che questo è completamente manuale mentre catalyst-hook fa tutto in automatico.

Il suo scopo è generare il pacchetto **catalyst-{kernver}** utilizzando [makepkg](/index.php/Makepkg_(Italiano) "Makepkg (Italiano)") e installarlo con l'ausilio di [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)"); {kernver} è la versione del kernel con il quale è stato compilato il pacchetto, ad esempio : il pacchetto catalyst-2.6.35-ARCH è stato compilato sul kernel 2.6.35-ARCH .

Per compilare ed installare il pacchetto catalyst-{kernver} per il kernel avviato come **utente senza privilegi** (metodo sicuro) usare ilc comando: `catalyst_build_module`. Vi verrà chiesta la password di root per procedere all'installazione.

Ecco il sommario delle operazioni da svolgere:

1.  Con i privilegi di root:`# catalyst_build_module remove`. Questo comando eliminerà i pacchetti `catalyst-{kernver}` non utilizzati
2.  Poi come utente senza privilegi:`$ catalyst_build_module ''nuova-versione-kernel''` dove *nuova-versione-kernel''*è la versione del kernel che avete appena aggiornato/installato, Es:`catalyst_build_module 2.6.36-ARCH` oppure: `catalyst_build_module all` il quale compilerà il pacchetto catalyst-{kernver} per tutti i kernel presenti.
3.  Se volete rimuovere `catalyst-generator` - si **consiglia** di eseguire da root questo comando: `catalyst_build_module remove_all`

*prima di rimuovere catalyst-generator (con questo comando si* elimineranno tutti i pacchetti catalyst-{kernver} presenti nel sistema)

catalyst-generator non è in grado di rimuovere tutti i pacchetti catalyst-{kernver} automaticamente mentre lo si rimuove perché non ci può essere ad esempio più di una istanza di pacman in esecuzione. Se si dimentica di dare il comando `catalyst_build_module remove_all` prima di digitare `pacman -R catalyst-generator` - catalyst-generator vi chiederà quale pacchetto catalyst-{kernver} si dovrà rimuovere dopo la rimozione di catalyst-generator.

{{Nota| Se si visualizza un errore del tipo:

```
**WARNING:** Package contains reference to $srcdir
**WARNING:** '.pkg' is not a valid archive extension.

```

mentre si compila il pacchetto catalyst-{kernver} - non c'è da preoccuparsi, è un normale avvertimento. }}

## Caratteristiche

### Desktop senza Tearing

Presentata con i **Catalyst 11.1**, la funzione 'Desktop senza Tearing' riduce il tearing nelle applicazioni 2d, 3d e video. Per quanto è possibile saperne, ogni frame renderizzato che passa per il server X viene memorizzato in un triplo buffer e sincronizzato col refresh verticale del monitor. Tenere presente che questa procedura occupa risorse supplementari.

Per abilitare la funzione 'Desktop senza Tearing' eseguire `amdcccle` e andare su:`Display Options` ~~> `Tear Free`.

oppure da utente root eseguire:

```
 aticonfig --set-pcs-u32=DDX,EnableTearFreeDesktop,1

```

Per disabilitarla utilizzare `amdcccle` oppure da utente root eseguire:

```
 aticonfig --del-pcs-key=DDX,EnableTearFreeDesktop

```

### Accelerazione video

**[Video Acceleration API](https://en.wikipedia.org/wiki/Video_Acceleration_API "wikipedia:Video Acceleration API") (VA API)** è una libreria open source ("libVA") compresa di specifiche API che permette l'accesso all'**accelerazione grafica hardware (GPU)** per il processing dei contenuti video su sistemi Linux e basati su UNIX. L'obiettivo principale delle VA API è di permettere la decodifica di video mediante hardware a vari entry-points (VLD, IDCT, Motion Compensation, deblocking) per quanto riguarda i principali codec odierni (MPEG-2, MPEG-4 ASP/H.263, MPEG-4 AVC/H.264, e VC-1/WMV3).

Nel mese di Novembre 2009, le VA-API hanno ottenuto un nuovo backend proprietario, **xvba-video**, che permette alle applicazioni abilitate all'uso delle VA-API di sfruttare i chipset AMD Radeon UVD2 attraverso la libreria [X-Video Bitstream Acceleration API di AMD](https://en.wikipedia.org/wiki/XvBA_XvBA "wikipedia:XvBA XvBA").

Il supporto a XvBA e a xvba-video è ancora in fase di sviluppo, nonostante ciò **mplayer** (e relativi frontend) garantiscono un funzionamento decisamente soddisfacente. Per avvalersi delle funzionalità VA-API rese disponibili da mplayer è necessario compilare il pacchetto [http://[xvba-video](https://aur.archlinux.org/packages.php?ID=31723) ed installare mplayer-vaapi (disponibile nel repo community) & libva (disponibile nel repository extra).

Installati questi pacchetti è sufficiente impostare come output video il parametro **vaapi:gl**.

Esempio: per **Mplayer**:

```
$ mplayer -vo vaapi:gl movie.avi

```

Queste opzioni possono essere inserite nel file di configurazione di MPlayer. Vedere [Mplayer](/index.php/MPlayer_(Italiano) "MPlayer (Italiano)") per ulteriori informazioni.

Esempio: per **smplayer**:

```
Opzioni -> Preferenze -> Generale -> Video (tab) -> Driver di uscita: Definito dall'utente... : vaapi:gl
Opzioni -> Preferenze -> Generale -> Video (tab) -> Doppio Buffering **on**
Opzioni -> Preferenze -> Avanzate -> Opzioni per MPlayer -> Opzioni: -vo vaapi
Opzioni -> Preferenze -> Generale -> togliere il segno di spunta da "abilita schermata"

```

Opzioni -> Preferenze -> Performance -> decoding (inserire il **numero** dellaa CPU)

**Nota:** Se l'opzione Desktop Senza Tearing è abilitata, è preferibile utilizzare
```
Options -> Preferences -> General -> Video (tab) -> Output driver: vaapi 

```

**Nota:** Se l'uscita video **vaapi:gl** non funziona - controllare
```
 **vaapi**, **vaapi:gl2** or simply **xv(0 - AMD Radeon [AVIVO Video](https://en.wikipedia.org/wiki/Avivo "wikipedia:Avivo"))**

```

Ad esempio per VLC:

```
Tools -> Preferences -> Input & Codecs -> Use GPU accelerated decoding

```

Non dimenticate di attivare v-sync in **amdcccle**:

```
3D -> More Settings -> Wait for vertical refresh = Always On

```

**Nota:** Se si utilizza **compiz/kwin** tenere presente che l'unico modo di evitare il "flickering" dei video consiste nell'eseguire la riproduzione a pieno schermo, abilitando l'opzione "**Unredirect Fullscreen is off**".

In **compiz**, è necessario impostare "**Redirected Direct Rendering**" nelle "Opzioni Generali" del pannello di gestione ccsm. Nel caso dovessero verificarsi episodi di **flickering** provare a disabilitare quest'opzione nel ccsm.

In **kwin** è disabilitato di default, ma se si dovesse verificare il **flickering**, provare a modificare il valore di "Suspend desktop effects for fullscreen windows" in System Settings -> Desktop Effects -> Advanced.

### Strumenti per la frequenza GPU/Mem, Temperatura, Velocità ventole, Overclock utilities

Si possono ottenere i clock GPU/Mem tramite il comando: `$ aticonfig --od-getclocks`

Velocità ventole: `aticonfig --pplib-cmd "get fanspeed 0"`

Temperatura: `$ aticonfig --od-gettemperature`

Per settare la velocità delle ventole: `$ aticonfig --pplib-cmd "set fanspeed 0 50"` Dove 50 è la velocità in percentuale.

Per operazioni di underclock/overclock è più semplice utilizzare programmi ad interfaccia grafica, come **ATi Overclocking Utility**, che è molto semplice da usare ma richiede le librerie QT per funzionare [qui](http://kde-apps.org/content/show.php/ATI+Overclock?content=47796)

Un'altro, strumento per operare questo tipo di modifiche è **AMDOverdriveCtrl**. La sua homepage è [qui](http://sourceforge.net/projects/amdovdrvctrl), si possono reperire i pacchetti per arch su [AUR](https://aur.archlinux.org/packages.php?ID=45298) o dal repository [catalyst].

### Double Screen (Dual Head / Dual Screen / Xinerama)

#### Introduzione

**Attenzione:** Prima di tutto: bisogna sapere che non esiste una singola soluzione, le configurazioni possono essere diverse. È quindi necessario adattare questo paragrafo alle proprie esigenze. Non è da escludere che dovranno essere fatti più tentativi. **Pertanto salvare il file `/etc/X11/xorg.conf` attuale prima di iniziare ogni cambiamento. Sarebbe utile anche saper recuperare la vecchia configurazione da tty**

*   In questa sezione si vedrà come installare due schermi di diverse dimensioni su una sola scheda grafica con 2 differenti output (DVI + HDMI) usando la configurazione "Big desktop".

*   La soluzione Xinerama ha degli inconvenienti, specialmente perchè non è compatibile con XrandR. Per questo motivo, tale soluzione non è consigliata.

*   La soluzione "Dual Head" permette di avere due differenti sessioni (una per schermo). Potrebbe questa essere una soluzione preferibile anche se non da la possibilità di spostare le finestre da uno schermo all'altro. Se si ha un solo schermo si dovrà definire il mouse all'interno di Xorg per le 2 sessioni all'interno della sezione Server Layout.

[Documentazione ATI](http://support.amd.com/us/kbarticles/Pages/1105-HowCanIConfigureMultip.aspx)

#### ATI Catalyst Control Center

La GUI fornita da ATI è uno strumento veramente utile e versatile. Per usarla laciare da terminale

```
amdcccle

```

**Nota:** Funziona tranquillamente anche con *gksu* se usate GNOME o altri DE/WM

**Attenzione:** Non lanciate `amdcccle` con il comando *sudo* perchè sudo rende amministratori ma usa le informazioni dell'account utente. Con kdesu si diventa root in tutto e per tutto

#### Installazione

Facile ma importante: assicurarsi che tutto sia collegato correttamente, che tutto sia acceso, e di conoscere le caratterische fondamentali dell'hardware in questione (dimensione, risoluzione, frequenza di aggiornamento ...) Normalmente, gli schermi vengono riconosciuti al boot ma non sempre la loro configurazione risulta essere corretta, specialmente se si sta usando una configurazione base di Xorg.

Il primo passo è quello di assicurarsi che essi saranno riconosciuti dal vostro DE / Xorg. Per questo, è necessario generare un file per X per i 2 schermi :

```
$ aticonfig --initial --desktop-setup=horizontal --overlay-on=1

```

o

```
$ aticonfig --initial=dual-head --screen-layout=left

```

**Nota:** La sovrapposizione `overlay` è molto importante in quanto permette di condivire un pixel (o più) tra i due schermi.

**Tip:** Per tutte le configurazioni possibili, non si esiti a dare un `aticonfig` in un terminale per prendere visioni di tutte le possibili opzioni.

Normalmente, si dovrebbe avere un file base che è possibile editare per aggiungere le risoluzioni desiderate. È importante precisare la risoluzione voluta specialmente se si hanno schermi di dimensioni diverse. Aggiungere nella sezione "screen":

```
SubSection "Display"
Depth 24
Modes "1200x800"
EndSubSection

```

Da ora in poi non modificare manualmente `xorg.conf`, usare la GUI di ATI. Riavviare X e assicurarsi che i due schermi siano supportati e che la risoluzione sia corretta. (Gli schermi sono indipendenti).

#### Configurazione

Dopo aver lanciato ATI control center come root si potrà accedere ai menù e scegliere la configurazione che si preferisce per il proprio sistema. Alla fine, riavviare X e tutto dovrebbe funzionare.

Non esitate a controllare più volte `xorg.conf` prima di riavviare il server grafico. A questo punto, nella sotto sezione "Display" della sezione "Screen" si può vedere "Virtual" command line. La risoluzione deve essere la somma di entrambi gli schermi. La sezione "Server Layout" dice tutto il resto.

## Risoluzione problemi

Se si hanno problemi con i driver, la causa più probabile è una configurazione errata del file `xorg.conf`.

È possibile parsare il file `/var/log/Xorg.0.log` in cerca di errori tramite questi comandi:

```
grep '(EE)' /var/log/Xorg.0.log
grep '(WW)' /var/log/Xorg.0.log

```

### Freeze delle applicazioni 3D Wine

Se si usano applicazioni 3D con Wine e si riscontrano problemi, provare a disabilitare il TLS. Per fare ciò, usare `aticonfig` o editare `/etc/X11/xorg.conf`. Usando `aticonfig`:

```
# aticonfig --tls=off

```

O editando `/etc/X11/xorg.conf`; aggiungendo `Option "UseFastTLS" "off"` alla sezione *Device*.

Riavviare X.

### Problemi con i colori video

Si può ancora usare vaapi:gl per evitare lo sfarfallio video, ma senza accelerazione video.

Eseguire **mplayer** senza l'opzione **-vo vaapi**.

Per **smplayer** rimuovere **-vo vaapi** dalle opzioni -> Preferenze -> Avanzate -> Opzioni per MPlayer -> Opzioni: -vo vaapi

Inoltre per **smplayer** è possibile tranquillamente attivare lo screenshot.

### KWin e composite

È possibile utilizzare XRender se il rendering con OpenGL è lento. Tuttavia, XRender potrebbe anche essere più lento di OpenGL a seconda della scheda. XRender risolve anche problemi di artefatti grafici in alcuni casi, come ad esempio il ridimensionamento di Konsole.

### Schermo nero con completo blocco dopo riavvio o startx

Assicurarsi di aver abilitato l'opzione **nomodeset** sulla linea del kernel nel file di configurazione del proprio bootloader (vedere [#Configurazione](#Configurazione) per ulteriore informazioni).

Se si usano i driver legacy (catalyst-hd234k) e si ha questo problema provare il downgrade di xorg-server alla versione 1.11 usando il repository **[xorg111]**.

#### Chiamate hardware ACPI difettose

E' possibile che fglrx non cooperi bene con le chiamate hardware ACPI del sistema, quinid si autodisabilita e non vi è alcun output su schermo.

Provare ad eseguire:

```
  aticonfig --acpi-services=off

```

### KDM scompare dopo il logout

Se si sta eseguendo il driver proprietario **catalyst** e si ottiene una console (tty1) invece della schermata KDM quando si effettua il logout, bisogna indicare a KDM di riavviare il server X dopo ogni logout, editare il file `/usr/share/config/kdm/kdmrc` e decommentare la seguente linea sotto la sezione [X-:*-Core]:

```
TerminateServer=True

```

KDM dovrebbe adesso apparire quando si effettua il logout da KDE.

### Il Direct Rendering non funziona

Questo problema può accadere utilizzando i driver proprietari **catalyst**.

**Attenzione:** Quest'errore può anche accadere nel caso in cui non si sia **riavviato** il sistema dopo l'installazione o l'aggiornamento dei driver catalyst. Il sistema cerca di caricare il modulo fglrx.ko in modo tale da far funzionare il driver.

Se si hanno problemi con il direct rendering, si lanci da terminale:

```
   $ LIBGL_DEBUG=verbose glxinfo > /dev/null

```

All'inizio dell'output solitamente viene dato un messaggio d'errore che spiega il perchè del mancato funzionamento del direct rendering.

Gli errori più comuni e le relative soluzioni sono:

```
   **libGL error: XF86DRIQueryDirectRenderingCapable returned false**

```

*   Assicurarsi di caricare il modulo agp corretto per il proprio chipset AGP prima di avviare il modulo kernel fglrx. Per determinare il modulo agp necessario, si lanci `hwdetect --show-agp`, quindi assicurarsi che tutti i moduli elencati col pnellrecedente comando siano caricati **prima** di fglrx in `/etc/modules-load.d/fglrx.conf`.

```
   **libGL error: failed to open DRM: Operation not permitted**
   **libGL error: reverting to (slow) indirect rendering**

```

```
   **libGL: OpenDriver: trying /usr/lib/xorg/modules/dri//fglrx_dri.so**
   **libGL error: dlopen /usr/lib/xorg/modules/dri//fglrx_dri.so failed**
   **(/usr/lib/xorg/modules/dri//fglrx_dri.so: cannot open shared object file: No such file or directory)**
   **libGL error: unable to find driver: fglrx_dri.so**   

```

*   Qualcosa non è stato installato correttamente. Se il percorso nel messaggio d'errore precedente è `/usr/X11R6/lib/modules/dri/fglrx_dri.so`, allora assicurarsi di uscire completamente dal sistema e quindi rientrare. Nel caso in cui si usi un manager di login grafico (gdm, kdm, xdm), assicurarsi che `/etc/profile` venga creato ogni volta che si effettua il login. Questo solitamente si realizza aggiungendo `source /etc/profile` in `/.xsession` o `~/.xinitrc`, ma potrebbe variare a seconda dei manager di login.

*   Se il percorso del messaggio d'errore è `/usr/lib/xorg/modules/dri/fglrx_dri.so`, allora qualcosa non è stato installato correttamente. Si provi a reinstallare il pacchetto catalyst.

Errori come:

```
   **fglrx: libGL version undetermined - OpenGL module is using glapi fallback**

```

potrebbero essere causati dall'avere più versioni di `libGL.so` sul proprio sistema. Si lanci:

```
   # updatedb
   $ locate libGL.so

```

Ciò dovrebbe dare il seguente output:

```
   $ locate libGL.so
   /usr/lib/libGL.so
   /usr/lib/libGL.so.1
   /usr/lib/libGL.so.1.2
   $

```

Questi sono i soli tre libGL.so file che si dovrebbero avere nel proprio sistema. Se se ne hanno di più (es. `/usr/X11R6/lib/libGL.so.1.2`), allora si provveda a rimuoverli. Questo dovrebbe risolvere il problema.

Nel caso in cui non si dovessero ottenere errori che indichino la presenza di problemi. Se si usa X11R7, ci si assicuri di **non** avere questi file sul proprio sistema:

```
   /usr/X11R6/lib/libGL.so.1.2
   /usr/X11R6/lib/libGL.so.1

```

### Problemi con l'ibernazione/sospensione

#### La parte video fallisce nel tentativo di di riprendersi dal suspend2ram

I driver proprietari ATI `catalyst` non riescono a riavviarsi dalla sospensione se il framebuffer è abilitato. Per disabilitare il framebuffer, si aggiunga **vga=0** all'opzione kernel in `/boot/grub/menu.lst`, ad esempio:

```
kernel /vmlinuz-linux root=/dev/sda3 resume=/dev/sda2 ro ***vga=0***

```

### Blocco del sistema/Hard lock

*   I driver del framebuffer `radeonfb` erano noti per causare problemi di questa natura. Se il kernel è stato compilato con il supporto per radeonfb, può essere utile provare un kernel diverso per vedere se i problemi si risolvono.

*   Se si notano freeze del sistema durante spegnimento, riavvio, passaggio a tty o altre operazioni in cui si "esce" dal DE, attivare il [KMS](/index.php/KMS "KMS") come indicato nella sezione [#Configurazione](#Configurazione).

### Conflitti hardware

Le schede radeon usate insieme ad alcune versione del chipset nForce3 (per esempio, nForce 3 250Gb) non hanno l'accelerazione 3D. Attualmente la causa di questo problema è sconosciuta, ma alcune fonti indicano che è possibile ottenere l'accelerazione con questa combinazione hardware avviando Windows con i drive di nVIDIA e poi riavviando il sistema. Si può controllare il chipset dando questo comando da root:

```
# dmesg | grep agp

```

Se si ottiene qualcosa di simile:

```
agpgart: Detected AGP bridge 0
agpgart: Setting up Nforce3 AGP.
agpgart: aperture base > 4G

```

si sta utilizzando il chipset nForce3.

Se, inoltre, dando questo comando:

```
$ tail -n 100 /var/log/Xorg.0.log | grep agp

```

si ottiene qualcosa del tipo:

```
(EE) fglrx(0): [agp] unable to acquire AGP, error "xf86_ENODEV"

```

allora si è affetti da questo bug.

Altre fonti indicano che in alcune situazioni può essere utile fare il downgrade del BIOS della scheda madre, ma ciò non può essere verificato in tutti i casi. Oltretutto, un downgrade del BIOS andato male può rendere inutilizzabile l'hardware, quindi prestare attenzione.

Vedere il bug [http://bugzilla.kernel.org/show_bug.cgi?id=6350](http://bugzilla.kernel.org/show_bug.cgi?id=6350) per ulteriori informazioni e possibili soluzioni.

### Blocchi temporanei durante l'esecuzione di video

Questo problema può verificarsi quando si utilizzano i driver proprietari catalyst.

Se si verificano in modo casuale blocchi temporanei della durata di pochi secondi fino a parecchi minuti, durante l'esecuzione di video con mplayer, controllare `/var/log/messages.log` per messaggi simili a questo:

```
Nov 28 18:31:56 pandemonium [<c01c64a6>] ? proc_get_sb+0xc6/0x160
Nov 28 18:31:56 pandemonium [<c01c64a6>] ? proc_get_sb+0xc6/0x160
Nov 28 18:31:56 pandemonium [<f8bc628c>] ? ip_firegl_ioctl+0x1c/0x30 [fglrx]
Nov 28 18:31:56 pandemonium [<c01c64a6>] ? proc_get_sb+0xc6/0x160
Nov 28 18:31:56 pandemonium [<c0197038>] ? vfs_ioctl+0x78/0x90
Nov 28 18:31:56 pandemonium [<c01970b7>] ? do_vfs_ioctl+0x67/0x2f0
Nov 28 18:31:56 pandemonium [<c01973a6>] ? sys_ioctl+0x66/0x70
Nov 28 18:31:56 pandemonium [<c0103ef3>] ? sysenter_do_call+0x12/0x33
Nov 28 18:31:56 pandemonium [<c01c64a6>] ? proc_get_sb+0xc6/0x160
Nov 28 18:31:56 pandemonium =======================

```

L'aggiunta dell'opzione `nopat` a `/boot/grub/menu.lst` e il riavvio hanno risolto il problema, almeno nel mio caso.

### "aticonfig: No supported adaptaters detected"

Se quando viene lanciato il comando:

```
# aticonfig --initial

```

si ottiene come output:

```
aticonfig: No supported adaptaters detected

```

è ragionevole pensare che i driver Catalyst possano funzionare lo stesso.

Copiare un vecchio file control: Scaricare una vecchia versione di fglrc da AMD e lanciarlo con lo switch "--extract driver". Copiare driver/common/etc/ati/control sul file di sistema e riavviare Xorg. Si può provare con diverse versioni di quel file. Aggiungere il proprio modello a mano in`xorg.conf`:

```
Section "Device"
 Identifier "ATI radeon ****"
 Driver "fglrx"
EndSection

```

dove ****** va rimpiazzato con il modello della propria scheda, ad esempio 6870 per la HD 6870 e 6310 per la E-350.

Xorg ora si avvierà ed sarà possibile utilizzare `amdcccle` invece di `aticonfig` anche se risulterà un avviso: "AMD Unsupported hardware".

È possibile rimuovere questo avviso utilizzando il seguente script:

```
#!/bin/sh
DRIVER=/usr/lib/xorg/modules/drivers/fglrx_drv.so
for x in $(objdump -d $DRIVER|awk '/call/&&/EnableLogo/{print "\\x"$2"\\x"$3"\\x"$4"\\x"$5"\\x"$6}'); do
 sed -i "s/$x/\x90\x90\x90\x90\x90/g" $DRIVER
done

```

Riavviare!

### Supporto a WebGL in Chromium

Per qualche ragione Google ha messo in balcklist il driver Catalyst per Linux per ciò che concerne l'accelerazione WebGL nei browser Chromium/Chrome.

Per ovviare a ciò è possibile modificare il file `/usr/share/applications/chromium.desktop` ed aggiungere la flag `--ignore-gpu-blacklist` alla riga `Exec` in modo che appaia così:

 `/usr/share/applications/chromium.desktop` 
```
....
Exec=chromium %U --ignore-gpu-blacklist
....
```

È anche possibile eseguire il browser da riga di comando direttamente con la flag `$--ignore-gpu-blacklist`:

```
$ chromium --ignore-gpu-blacklist

```

### Freeze guardando video flash con flashplugin

Modificare `/etc/adobe/mms.cfg` per renderlo simile a questo:

```
#EnableLinuxHWVideoDecode=1
OverrideGPUValidation=true

```

Se si usa KDE è consigliabile disabilitare gli effetti delle finestre quando queste sono in "full screen" dalle impostazioni di Sistema. System Settings->Workspace Appearance and Behaviour->Desktop Effects->Advanced.

### Artefatti e movimenti lenti delle finestre con GNOME 3

È possibile provare questa soluzione che sembra essere una buona soluzione per molti utenti. Aggiungere la linea:

```
export CLUTTER_VBLANK=none

```

nel file `~/.profile` o in `/etc/profile`.

Riavviare X o tutto il sistema.

### Impossibile usare la modalità fullscreen con risoluzione 1920x1080

Usando la GUI amdcccle è possibile selezionare il Display, cliccare su adjustament e settare Underscan su 0% (di default è 15%).

In alternativa, disabilitare l'underscanning con `aticonfig`

```
aticonfig --set-pcs-val=MCIL,DigitalHDTVDefaultUnderscan,0

```

Per le versioni più recenti (dalla 12.11 in poi), se il Catalyst Control Center dovesse fallire nel salvataggio dell'overscan editare `/etc/ati/amdpcsdb`:

```
 TVEnableOverscan=V0

```

Riavviare X.

## Altre risorse

*   [Unofficial Wiki for the ATI Linux Driver](http://wiki.cchtml.com/index.php/Main_Page)
*   [Unofficial ATI Linux Driver Bugzilla](http://ati.cchtml.com/query.cgi)