Articoli correlati

*   [AMD Catalyst (Italiano)](/index.php/AMD_Catalyst_(Italiano) "AMD Catalyst (Italiano)")
*   [KMS](/index.php/KMS "KMS")
*   [Xorg (Italiano)](/index.php/Xorg_(Italiano) "Xorg (Italiano)")

I possessori di schede video **AMD** possono scegliere tra i [driver proprietari](/index.php/AMD_Catalyst_(Italiano) "AMD Catalyst (Italiano)") ATI/AMD ([catalyst](https://aur.archlinux.org/packages/catalyst/)) e i driver open source([xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati)).

Attualmente, le performance dei driver open source non sono *alla pari* con i driver proprietari in termini di prestazioni 3D e mancano di alcune caratteristiche, come il supporto TV-out. Tuttavia, offrono un miglior supporto dual-head, un'eccellente accelerazione 2D, e forniscono l'accelerazione 3D necessaria ai vari [Window Manager](/index.php/Window_manager_(Italiano) "Window manager (Italiano)") che sfruttano le accelerazioni OpenGL, come [Compiz](/index.php/Compiz_(Italiano) "Compiz (Italiano)") o KWin.

In caso si incertezza, provare in primo luogo i driver open source; sono adatti alla maggior parte delle necessità e sono generalmente più flessibili e meno problematici. (vedere la [tabella delle caratteristiche](http://www.x.org/wiki/RadeonFeature) per i dettagli.) Per una panoramica riservata ai driver proprietari ATI "Catalyst" e la loro configurazione, consultare [ATI Catalyst](/index.php/ATI_Catalyst "ATI Catalyst"); questo articolo copre solamente i driver open source. I driver [ATI Catalyst non sono ufficialmente supportati](https://www.archlinux.org/news/439/) in Arch Linux.

## Contents

*   [1 Convenzione dei nomi](#Convenzione_dei_nomi)
*   [2 Panoramica](#Panoramica)
*   [3 Installazione](#Installazione)
    *   [3.1 Installazione di xf86-video-ati](#Installazione_di_xf86-video-ati)
*   [4 Configurazione](#Configurazione)
*   [5 Kernel mode-setting (KMS)](#Kernel_mode-setting_.28KMS.29)
    *   [5.1 Abilitare KMS](#Abilitare_KMS)
        *   [5.1.1 Avvio rapido](#Avvio_rapido)
        *   [5.1.2 Avvio ritardato](#Avvio_ritardato)
    *   [5.2 Errori e risoluzione dei problemi di KMS](#Errori_e_risoluzione_dei_problemi_di_KMS)
        *   [5.2.1 Disabilitare KMS](#Disabilitare_KMS)
        *   [5.2.2 Rinominare xorg.conf](#Rinominare_xorg.conf)
*   [6 Ottimizzazione prestazioni](#Ottimizzazione_prestazioni)
    *   [6.1 Attivare PCI-E 2.0](#Attivare_PCI-E_2.0)
    *   [6.2 Glamor](#Glamor)
*   [7 Gestione risparmio energetico](#Gestione_risparmio_energetico)
    *   [7.1 Con KMS abilitato](#Con_KMS_abilitato)
    *   [7.2 Senza KMS](#Senza_KMS)
*   [8 Uscita TV](#Uscita_TV)
    *   [8.1 Forzare l'utilizzo dell'uscita TV con KMS](#Forzare_l.27utilizzo_dell.27uscita_TV_con_KMS)
*   [9 Audio su HDMI](#Audio_su_HDMI)
*   [10 Configurare la modalità Dual Head](#Configurare_la_modalit.C3.A0_Dual_Head)
    *   [10.1 Schermi indipendenti sotto X](#Schermi_indipendenti_sotto_X)
*   [11 Abilitare l'accelerazione video](#Abilitare_l.27accelerazione_video)
*   [12 Disabilitare il vsync](#Disabilitare_il_vsync)
*   [13 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [13.1 Rilevo artefatti quando effettuo il login nel mio DE o WM](#Rilevo_artefatti_quando_effettuo_il_login_nel_mio_DE_o_WM)
    *   [13.2 Aggiungere risoluzioni non rilevate](#Aggiungere_risoluzioni_non_rilevate)
    *   [13.3 Performance scadenti con driver libero](#Performance_scadenti_con_driver_libero)
    *   [13.4 L'AGP è disabilitato (con il KMS)](#L.27AGP_.C3.A8_disabilitato_.28con_il_KMS.29)
    *   [13.5 Collegando un TV viene mostrato un bordo nero attorno allo schermo](#Collegando_un_TV_viene_mostrato_un_bordo_nero_attorno_allo_schermo)
    *   [13.6 Schermo nero con cursore del mouse visibile al resume dalla sospensione](#Schermo_nero_con_cursore_del_mouse_visibile_al_resume_dalla_sospensione)
    *   [13.7 Nessun effetto desktop in KDE4 con la X1300 ed i driver Radeon](#Nessun_effetto_desktop_in_KDE4_con_la_X1300_ed_i_driver_Radeon)
    *   [13.8 Schermo nero e nessuna console visualizzata, ma X funzionante sotto KMS](#Schermo_nero_e_nessuna_console_visualizzata.2C_ma_X_funzionante_sotto_KMS)
    *   [13.9 Alcune applicazioni 3d vanno in crash o mostrano alcune textures completamente nere](#Alcune_applicazioni_3d_vanno_in_crash_o_mostrano_alcune_textures_completamente_nere)
    *   [13.10 Prestazioni 2D (ad esempio lo scroll) scadenti](#Prestazioni_2D_.28ad_esempio_lo_scroll.29_scadenti)
    *   [13.11 Applicazioni 3d mostrano finestra nera su ATI X1600 (RV530)](#Applicazioni_3d_mostrano_finestra_nera_su_ATI_X1600_.28RV530.29)

## Convenzione dei nomi

Il marchio ATI [Radeon](https://en.wikipedia.org/wiki/Radeon "wikipedia:Radeon") segue uno schema di nomenclatura che collega ogni prodotto ad un settore di mercato. All'interno di questo articolo, si utilizzerà la nomenclatura sia in base al nome del *prodotto* (Es. HD 4850, X1900) che in base al nome in *codice* o del *core* (Es. RV770, R580). Solitamente, una *serie di prodotti* corrisponderà ad una *serie di core* (Es. la serie dei prodotti "X1000" include tutti i prodotti X1300, X1600, X1800, e X1900 i quali utilizzano la dei core della serie "R500" – che includono i core RV515, RV530, R520, e R580).

Per una tabella completa di comparazione tra i nomi dei prodotti ed i relativi core, vedere [Wikipedia:Comparison of AMD graphics processing units](https://en.wikipedia.org/wiki/Comparison_of_AMD_graphics_processing_units "wikipedia:Comparison of AMD graphics processing units").

## Panoramica

I driver `xf86-video-ati` (radeon)

*   Funzionano con i chipset Radeon fino a HD 6xxx e 7xxxM (ultimi chipset Northern Islands).
    *   Le schede della serie HD 77xx (Southern Islands) hanno un supporto solo parziale. Controllare la [feature matrix](http://www.x.org/wiki/RadeonFeature) per verificare quali funzioni non sono supportate.
    *   Le schede Radeon della serie X1xxx sono pienamente supportate, stabili, e forniscono una piena accelerazione 2D e 3D.
    *   Le schede Radeon dalla serie HD2xxx alla HD6xxx hanno pieno supporto all'accelerazione 2D ed una accelerazione 3D funzionale, ma non supportano tutte le caratteristiche che vengono fornite dai driver proprietari.
*   Supportano DRI1, RandR 1.2/1.3, accelerazione EXA e [kernel mode-setting](/index.php/KMS "KMS")/DRI2 (con le ultime versione del kernel Linux, libdrm e Mesa).

Generalmente ,**xf86-video-ati** dovrebbe essere la prima scelta, indipendentemente dalla scheda ATI di cui si è in possesso. In caso sia necessario usare un driver per le nuove schede ATI, si dovrebbe considerare il driver proprietario **Catalyst**.

**Nota:** xf86-video-ati è riconosciuto come "**radeon**" dal kernel e da Xorg (in `xorg.conf`).

## Installazione

### Installazione di xf86-video-ati

[Installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati), disponibile nei [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)"):

La versione GIT di questi drivers più pacchetti aggiuntivi (linux-git, etc.) possono essere scaricati dai [repository radeon](https://bbs.archlinux.org/viewtopic.php?id=79509&p=1) o da [AUR](/index.php/AUR "AUR")

## Configurazione

Xorg caricherà automaticamente il driver e userà l'EDID monitor per impostare la risoluzione nativa. La configurazione è necessaria solo per l'ottimizzazione del driver.

Se si desidera effettuare una configurazione manuale, creare `/etc/X11/xorg.conf.d/20-radeon.conf`, e aggiungere quanto segue:

 `/etc/X11/xorg.conf.d/20-radeon.conf` 
```
 Section "Device"
     Identifier "vga"
     Driver "radeon"
 EndSection
```

Utilizzando questa sezione, è possibile attivare ulteriori funzioni e ottimizzare le impostazioni del driver.

## Kernel mode-setting (KMS)

**Tip:** Se si hanno problemi con la risoluzione, consultare [questa pagina](/index.php/Kernel_mode_setting#Forcing_modes_and_EDID "Kernel mode setting").

[KMS](/index.php/KMS "KMS") abilita la risoluzione nativa nel framebuffer e permette l'interscambio istantaneo tra console (tty). KMS abilita inoltre le più recenti tecnologie (come ad esempio DRI2) riducendone eventuali anomalie ed incrementando le prestazioni 3D, oltre al risparmio energetico in kernel-space.

KMS per le schede video ATI richiede il driver opensource di [Xorg (Italiano)](/index.php/Xorg_(Italiano) "Xorg (Italiano)") [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) versione 6.12.4 o più recente.

### Abilitare KMS

**Nota:** Dal kernel v.2.6.33, KMS è abilitato di default per le schede ATI/AMD autorilevate. Questa sezione rimane per configurazioni al di fuori della norma.

#### Avvio rapido

*Questi due metodi avvieranno KMS il più presto possibile durante il [processo d'avvio](/index.php/Systemd_(Italiano) "Systemd (Italiano)").*

1\. Il primo metodo consiste nell'aggiungere alla riga di boot del kernel il parametro `radeon.modeset=1`. Consultare la pagina relativa al proprio bootloader per sapere come fare.

*   Rimuovere qualsiasi opzione `vga=` dalla linea del *kernel* nel [file di configurazione del bootloader](/index.php/Boot_Loader#Configuration_files "Boot Loader"). L'uso di altri driver del framebuffer (come `[uvesafb](/index.php/Uvesafb_(Italiano) "Uvesafb (Italiano)")` o `radeonfb`) provocherebbe conflitti con KMS.
*   La velocità dell'AGP può essere impostata con il parametro `radeon.agpmode=x`, dove x può assumere i valori 1, 2, 4, 8 (velocità AGP) o -1 (PCI mode).

2\. Altrimenti, quando l'[initramfs](/index.php/Mkinitcpio_(Italiano) "Mkinitcpio (Italiano)") è caricato:

*   Se si utilizza un kernel differente da quello stock `-ARCH` (ad es. linux-zen), ricordarsi di utilizzare un file di configurazione di *mkinitcpio* separato (ad es. `/etc/mkinitcpio-zen.conf`) e non `/etc/mkinitcpio.conf`.
*   Rimuovere ogni modulo relativo al framebuffer dal proprio mkinitcpio.
*   Aggiungere `radeon` alla stringa MODULES del proprio file di configurazione di mkinitcpio.conf. A seconda dal chipset della scheda madre, può essere necessario aggiungere `intel_agp` (o `ali_agp`, `ati_agp`, `amd_agp`, `amd64_agp` etc.) prima del modulo `radeon`.
*   Rigenerare [initramfs](/index.php/Mkinitcpio_(Italiano)#Creazione_dell.27immagine_ed_attivazione "Mkinitcpio (Italiano)"):
*   **Riavviare** il sistema.

#### Avvio ritardato

*Scegliendo questa modalità, KMS verrà avviato quando i moduli vengono caricati durante il [Arch Boot Process (Italiano)|processo d'avvio]].*

Se si sta utilizzando un kernel personalizzato (es:linux-zen), ricordarsi di utilizzare l'appropriato file di configurazione di mkinitcpio. Es: `/etc/mkinitcpio-zen.conf`. Le seguenti istruzioni valgono per il kernel predefinito ([linux](https://www.archlinux.org/packages/?name=linux)).

**Nota:** Per il supporto all'AGP, potrebbe essere necessario aggiungere {ic
, `ali_agp`, `ati_agp`, `amd_agp`, o `amd64_agp`) al file .conf appropriato in `/etc/modules-load.d`.}}

1.  Rimuovere qualsiasi opzione `vga=` dalla linea del *kernel* nel [file di configurazione del bootloader](/index.php/Boot_Loader#Configuration_files "Boot Loader"). L'utilizzo di altri driver del framebuffer (come `[uvesafb](/index.php/Uvesafb_(Italiano) "Uvesafb (Italiano)")` o `radeonfb`) provocherebbe conflitti con KMS. Rimuovere qualsiasi altro modulo relativo al framebuffer da `/etc/mkinitcpio.conf`. `video=` può essere utilizzato in abbinamento a KMS.
2.  Aggiungere `options radeon modeset=1` a `/etc/modprobe.d/modprobe.conf`.
3.  **Riavviare** il sistema.

### Errori e risoluzione dei problemi di KMS

#### Disabilitare KMS

Dalla versione del kernel Linux 3.9, il driver `radeon` **necessita** del kernel mode-setting (il vecchio user mode-setting può ancora essere abilitato in fase di compilazione). Se è presente `radeon.modeset=0` (o `nomodeset`) nella riga di boot del kernel, rimuoverlo. Se è presente`options radeon modeset=0` ovunque in `/etc/modprobe.d`, rimuoverlo.

#### Rinominare `xorg.conf`

Rinominare `/etc/X11/xorg.conf`. Nel caso includa opzioni che vanno in conflitto con KMS, questo forzerà Xorg ad un nuovo e corretto autorilevamento hardware. Dopo averlo rinominato, **riavviare** Xorg.

## Ottimizzazione prestazioni

Applicare le seguenti opzioni a `/etc/X11/xorg.conf.d/**20-radeon.conf**`.

In modo predefinito, xf86-video-ati gira impostando la velocità dell'AGP a 4x. In genere è sicuro cambiare questo parametro. In caso di blocchi, ridurre il valore o rimuovere l'intera linea (valori accettabili sono 1, 2, 4, 8). Se si utilizza KMS, questa opzione viene ignorata, e sovrascritta dall'impostazione passata tramite il parametro del kernel `radeon.agpmode`

```
       Option "AGPMode" "8"

```

**ColorTiling** è totalmente sicuro attivarlo e presumibilmente lo sarà di default. Molti utenti hanno ottenuto un incremento di prestazioni abilitandolo, ma non è ancora supportato su schede con chip R200 e precedenti, sulle quali il carico di lavoro sarà passato alla cpu.

```
       Option "ColorTiling" "on"

```

**Acceleration architecture**; questa opzione sarà disponibile solo su schede video **nuove**. Se non si può accedere ad X una volta abilitato, rimuoverlo.

```
       Option "AccelMethod" "EXA"

```

**Page Flip** È generalmente sicuro. Se usato su schede più datate, disattiverà EXA. Con i drivers più recenti può tranquillamente essere abilitato insieme a EXA.

```
       Option "EnablePageFlip" "on" 

```

**AGPFastWrite** abilita scritture veloci per schede AGP. Potrebbe creare qualche problema, quindi nel caso, rimuoverlo se non si riesce più ad accedere a X.

```
       Option "AGPFastWrite" "yes"

```

**EXAVSync** Questa opzione cerca di "schivare" certe asimmetrie dell'immagine sul monitor, chiamate tearing, creando una situazione di stallo nel motore finchè il controller del display ha oltrepassato la zona di destinazione. Ciò riduce il tearing con un decremento di prestazioni ed è noto che causi instabilità in alcuni tipi di chip. Molto utile abilitare questa opzione se si abilità l'overlay di Xv su video su un desktop con accelerazione 3D. Non è necessario se KMS (quindi l'accelerazione DRI2) è abilitato.

```
Option "EXAVSync" "yes"

```

Un esempio di file di configurazione `/etc/X11/xorg.conf.d/**20-radeon.conf**`:

```
Section "Device"
       Identifier  "My Graphics Card"
        Option	"AGPMode"               "8"   #not used when KMS is on
	Option	"AGPFastWrite"          "off" #could cause instabilities enable it at your own risk
	Option	"SWcursor"              "off" #software cursor might be necessary on some rare occasions, hence set off by default
	Option	"EnablePageFlip"        "on"  #supported on all R/RV/RS4xx and older hardware and set off by default
	Option	"AccelMethod"           "EXA" #valid options are XAA, EXA and Glamor. EXA is the default.
	Option	"RenderAccel"           "on"  #enabled by default on all radeon hardware
	Option	"ColorTiling"           "on"  #enabled by default on RV300 and later radeon cards.
	Option	"EXAVSync"              "off" #default is off, otherwise on. Only works if EXA activated
	Option	"EXAPixmaps"            "on"  #when on icreases 2D performance, but may also cause artifacts on some old cards. Only works if EXA activated
	Option	"AccelDFS"              "on"  #default is off, read the radeon manpage for more information
EndSection

```

La definizione del **gartsize**, se non autorilevata, può essere effettuata aggiungendo l'opzione `radeon.gartsize=32` ai [parametri del kernel](/index.php/Kernel_parameters "Kernel parameters"). La dimensione è espressa in MegaByte, e 32 è un valore valido per schede con chip RV280. In alternativa, è possibile impostarlo tramite `/etc/modprobe.d/radeon.conf`: `options radeon gartsize=32`

**Consultare il manuale per ulteriori configurazioni.**

 `man radeon` 

Un valido strumento da provare è [driconf](https://www.archlinux.org/packages/?name=driconf). Permette di modificare diverse configurazioni, come vsync, anisotropic filtering, texture compression, etc. Con questo utile strumento è anche possibile disabilitare il "Low Impact fallback" necessario ad alcuni programmi (es. Google Earth).

### Attivare PCI-E 2.0

Può portare problemi di instabilità su alcune schede madri o non aggiungere alcun beneficio, se si vuole comunque provarlo di persona è sufficiente aggiungere "radeon.pcie_gen2=1" alla riga di comando del kernel.

**Nota:** A partire dal kernel 3.6 , il PCI-E v2.0 nei driver **radeon** sembra essere attivo di default.

Ulteriori informazioni su questo [Articolo di Phoronix](http://www.phoronix.com/scan.php?page=article&item=amd_pcie_gen2&num=1)

### Glamor

Con le versioni più recenti dei driver radeon è possibile utilizzare un nuovo metodo di accelerazione chiamato *glamor*: è un metodo di accelerazione 2d implementato tramite OpenGL, e dovrebbe funzionare con schede grafiche che montino chip uguali o superiori al R300.

 `Option "AccelMethod"          "glamor"` 

È necessario però aggiungere prima qqueste due voci alla sezione Module

```
Section "Module"
	Load "dri2"
	Load "glamoregl" 
EndSection
```

## Gestione risparmio energetico

La gestione del risparmio energetico è totalmente differente a seconda dell'uso o meno del KMS.

### Con KMS abilitato

Il driver radeon di default disabilita la gestione del risparmio energetico, ma è resa disponibile un'utility "sysfs" per abilitarla.

La gestione del risparmio energetico usando KMS e' ancora in fase di sviluppo. Dovrebbe funzionare, ma alcune schede potrebbero dare problemi. Un problema comune e' quello dello schermo lampeggiante quando si passa da un profilo energetico ad un altro, e in alcune configurazioni potrebbe causare un blocco del sistema. Il metodo UMS e' generalmente piu' stabile, ma le opzioni di risparmio energetico sono inferiori rispetto a quelle disponibile con KMS.

Usare il repository [radeon] (non supportato) per abilitare il risparmio energetico. Questo repository garantisce pacchetti aggiornati del driver radeon e delle sue dipendenze, prelevati principalmente da snapshot dei sorgenti su git.

```
[mesa-git]
Server = [http://pkgbuild.com/~lcarlier/$repo/$arch/](http://pkgbuild.com/~lcarlier/$repo/$arch/)
```

Ecco come selezionare i profili di risparmio energetico tramite sysfs:

Avendo accesso come root, si hanno due possibilità:

1\. **Variazione dinamica della frequenza (a seconda del carico della GPU)**

 `# echo dynpm > /sys/class/drm/card0/device/power_method` 

Il metodo "dynpm" varia dinamicamente le frequenze di clock in base al carico della gpu. In questo modo le performance aumentano quando si stanno eseguendo applicazioni intensive per la gpu, e diminuiscono quando la GPU e' inattiva. La modifica delle frequenze di clock viene tentata durante i periodi di blanking verticale, ma a causa dei timing delle funzioni di reclocking, non sempre si riesce a portarla a termine nel periodo di blanking, questo potrebbe portare ad uno sfarfallio del video. Per questo motivo il profilo dynpm funziona solo quando e' collegato un solo monitor.

**Nota:** L'uso dei "profili" descritto sotto e' meno aggressivo del metodo "dynpm", ma in questo momento e' molto piu' stabile e senza rischi di sfarfallio e funziona anche con piu' monitor collegati.

2\. **Variazione della frequenza, basata su Profili**

 `echo profile > /sys/class/drm/card0/device/power_method` 

Il metodo "profile" permette di selezionare uno dei 5 profili riportati sotto. Ogni profilo modifica la frequenza e/o il voltaggio della scheda video.

*   "default": usa le impostazioni di default (frequenza e voltaggio sono quelli massimi di fabbrica). Questo e' il profilo predefinito.
*   "auto": seleziona il profilo "mid" quando il computer sta funzionando con la batteria, il profilo "high" quando collegato alla rete elettrica e il profilo "low" quando i monitor sono in stato dpms off (sono spenti o in standby).
*   "low": forza la gpu a funzionare sempre in modalita a basso consumo. Il profilo "low" potrebbe causare problemi di visualizzazione su alcuni portatili; per questo motivo il profilo auto usa la modalita' "low" quando i monitor sono spenti.
*   "mid": forza la gpu a funzionare sempre in modalita medio consumo. Il profilo "low" viene usato quando i monitor sono spenti.
*   "high" forza la gpu a funzionare sempre in modalita alto consumo (prestazioni elevate). Il profilo "low" viene usato quando i monitor sono spenti.

Per esempio se vogliamo usare il profilo "low"... eseguiamo questo comando:

 `echo low > /sys/class/drm/card0/device/power_profile` 

Sostituire "low" con uno dei profili possibili.

**Nota:** Impostare un valore in questo file non vale in modo permanente. Per ottenere ciò, usare un [file temporaneo di systemd](/index.php/Systemd_(Italiano)#File_temporanei "Systemd (Italiano)") o una regola di [udev (Italiano)](/index.php/Udev_(Italiano) "Udev (Italiano)")

**Nota:** Gli utenti di Gnome-shell potrebbero essere interessati all'estensione [Radeon Power Profile Manager](https://extensions.gnome.org/extension/356/radeon-power-profile-manager) per il controllo manuale dei profili della GPU.
 `/etc/tmpfiles.d/radeon-pm.conf`  `w /sys/class/drm/card0/device/power_method - - - - dynpm`  `/etc/udev/rules.d/30-local.rules`  `KERNEL=="dri/card0", SUBSYSTEM=="drm", DRIVERS=="radeon", ATTR{device/power_method}="profile", ATTR{device/power_profile}="auto"` 
**Nota:**

*   Se la regola precedente dovesse fallire, provare a rimuovere '/dri' da essa.
*   Un'altra opzione dello stesso autore per utenti che non usano Gnome-shell (con qualche opzione in più) scritta in PyQt4 è Radeon-tray [[1]](https://github.com/StuntsPT/Radeon-tray).

Questa gestione del risparmio energetico e' supportata su tutte le schede (r1xx-evergreen) che includono una tabella degli stati energetici appropriata all'interno del vbios; alcune schede potrebbero non averne il supporto (specialmente alcune vecchie schede per desktop).

Per visualizzare informazioni sulle frequenze di clock della gpu, eseguire questo comando. Si otterrà qualcosa del genere:

 `$ cat /sys/kernel/debug/dri/0/radeon_pm_info` 
```
state: PM_STATE_ENABLED
default engine clock: 300000 kHz
current engine clock: 300720 kHz
default memory clock: 200000 kHz

```

Se `/sys/kernel/debug` fosse vuota, eseguire questo comando:

 `# mount -t debugfs none /sys/kernel/debug` 

Per montare il filesystem permanentemente, aggiungere questa riga ad `/etc/fstab`

 `debugfs  /sys/kernel/debug  debugfs  defaults  0  0` 

Comunque tutto dipende dal modello di scheda video, dalla versione del driver radeon, dalla versione del kernel, etc. Potrebbe capitare di non avere a disposizione molte regolazioni.

I sensori termici sono implementati con chip i2c o tramite sensori termici interni (per esempio nella rv6xx-evergreen). Per avere la temperatura sulle schede che usano chip i2c, bisogna caricare il driver hwmon appropriato per il sensore usato (lm63, lm64, etc.). Il drm cercherà di caricare il driver hwmon appropriato. Sulle schede che usano sensori termici interni, il drm imposterà l'interfaccia hwmon automaticamente. Una volta caricato il driver corretto, le temperature possono essere viste usando i tools lm_sensors o tramite sysfs in /sys/class/hwmon.

C'è una piccola gui per passare da un profilo all'altro: [power-play-switcher](https://aur.archlinux.org/packages/power-play-switcher/)

### Senza KMS

Nel file `xorg.conf`, aggiungere due linee alla sezione *Device*:

```
       Option      "DynamicPM"          "on"
       Option      "ClockGating"        "on"

```

Se le due opzioni vengono attivate con successo, è possibile trovare un riscontro in `/var/log/Xorg.0.log`:

```
       (**) RADEON(0): Option "ClockGating" "on"
       (**) RADEON(0): Option "DynamicPM" "on"

```

```
       Static power management enable success
       (II) RADEON(0): Dynamic Clock Gating Enabled
       (II) RADEON(0): Dynamic Power Management Enabled

```

Se si necessita di un profilo energetico a basso consumo, è possibile aggiungere la linea seguente alla sezione *Device* di `xorg.conf`:

```
       Option      "ForceLowPowerMode"   "on"

```

## Uscita TV

Fino dall'agosto 2007, è disponibile il supporto per l'uscita TV per tutte le schede Radeon con uscita TV integrata.

Per il momento è qualcosa di un po' limitato, non sempre l'autorilevamento del segnale lavora correttamente e solamente il modo NTSC è funzionante.

Per prima cosa, controllare di avere un'uscita S-video: `xrandr` dovrebbe restituire qualcosa di simile a

```
Screen 0: minimum 320x200, current 1024x768, maximum 1280x1200
...
 S-video disconnected (normal left inverted right x axis y axis)

```

Configurare lo standard tv da usare:

 `xrandr --output S-video --set "tv standard" ntsc` 

Aggiungere un modo (attualmente l'unica risoluzione disponibile è 800x600):

 `xrandr --addmode S-video 800x600` 

Si può propendere per un modo "clone":

```
 xrandr --output S-video --same-as VGA-0 
xrandr --output S-video --mode 800x600

```

A questo punto si dovrebbe vedere una versione 800x600 del proprio deskyop sulla TV.

Per disabilitare l'output, dare

 `xrandr --output S-video --off` 

Potrebbe anche verificarsi che il video viene visualizzato solo sul monitor e non sulla TV. Dove la copertura Xv viene inviata e controllata da XV_CRTC.

Per inviare il segnale di output alla TV, dare

 `xvattr -a XV_CRTC -v 1` 
**Note:** È necessario installare [xvattr](https://aur.archlinux.org/packages/xvattr/) per poter eseguire questo comando.

Per tornare indietro al proprio monitor si può cambiare questo a `0`. `-1` è usato per intercambi automatici in configurazioni dualhead.

Consultare [Enabling TV-Out Statically](http://www.x.org/wiki/radeonTV) per informazioni su attivazione uscita TV nel file di configurazione xorg.

### Forzare l'utilizzo dell'uscita TV con KMS

Il kernel riconosce il parametro `video=` nella seguente forma (consultare [KMS](/index.php/KMS "KMS")):

```
video=<conn>:<xres>x<yres>[M][R][-<bpp>][@<refresh>][i][m][eDd]}}

```

Per esempio:

```
video=DVI-I-1:1280x1024-24@60e

```

I parametri contenenti spazi bianchi dovrebbe venire racchiusi tra doppi apici.

```
"video=9-pin DIN-1:1024x768-24@60e"

```

L'attuale implementazione di mkinitcpio richiede anche che un `#` sia posto ad inizio riga. Per esempio:

```
root=/dev/disk/by-uuid/d950a14f-fc0c-451d-b0d4-f95c2adefee3 ro quiet radeon.modeset=1 security=none # video=DVI-I-1:1280x1024-24@60e "video=9-pin DIN-1:1024x768-24@60e"

```

*   Grub riesce a passare il comando così com'è
*   Lilo necessita dell'utilizzo del backslash per il riconoscimento del carattere "doppi apici" (append {ic|1=# \"video=9-pin DIN-1:1024x768-24@60e\"}})

È possibili ottenere una lista delle uscite video disponibili per la propria scheda tramite il comando:

 `$ ls -1 /sys/class/drm/ | grep -E '^card[[:digit:]]+-' | cut -d- -f2-` 

## Audio su HDMI

L'audio HDMI è supportato dai driver video del pacchetto [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati). Di default il modulo necessario è disabilitato nelle versioni del kernel >=3.0\. . In ogni caso, se la propria scheda risulta supportata ([Radeon Feature Matrix](http://www.x.org/wiki/RadeonFeature)) è possibile aggiungere `radeon.audio=1` ai [parametri del kernel](/index.php/Kernel_parameters "Kernel parameters"). Per esempio:

 `/boot/syslinux/syslinux.cfg` 
```
LABEL arch
    MENU LABEL Arch Linux
    LINUX ../vmlinuz-linux
    APPEND root=/dev/sda1 ro radeon.audio=1
    INITRD ../initramfs-linux.img

```

Se l'audio HDMI non dovesse completamente funzionare dopo l'installazione del driver, verificare la propria configurazione seguendo la procedura proposta [qui](/index.php/Advanced_Linux_Sound_Architecture_(Italiano)#L.27uscita_HDMI_non_funziona "Advanced Linux Sound Architecture (Italiano)").

**Nota:** Al momento della stesura di questo articolo (2013-05-20), i driver per le [schede Southern Islands](http://www.x.org/wiki/RadeonFeature#Decoder_ring_for_engineering_vs_marketing_names) non supportano l'audio HDMI.

*   Il modulo del kernel `radeon.audio` funziona solo se il [#Kernel mode-setting (KMS)](#Kernel_mode-setting_.28KMS.29) è abilitato. Di default **xf86-video-ati** abilita il KMS.
*   Se il suono risultasse distorto, provare [a impostare tsched=0](/index.php/PulseAudio_(Italiano)#Artefatti_sonori.2C_audio_intermittente_o_gracchiante "PulseAudio (Italiano)") ed assicurarsi che il demone `rtkit` sia avviato.

## Configurare la modalità Dual Head

### Schermi indipendenti sotto X

Configurazioni indipendenti per il dual-headed possono essere impostate come di consueto. Tuttavia è utile sapere che il driver *radeon* possiede l'opzione "ZaphodHeads", che consente di associare una specifica sezione del dispositivo a un output di vostra scelta, utilizzando per esempio:

```
       Section "Device"
       Identifier     "Device0"
       Driver         "radeon"
       Option         "ZaphodHeads"   "VGA-0"
       VendorName     "ATI"
       BusID          "PCI:1:0:0"
       Screen          0
       EndSection

```

Questo può essere un salva-vita, perché alcune schede che hanno più di due uscite (per esempio una su HDMI, una DVI, una VGA), saranno solo selezionabili e utilizzabili le uscite HDMI+DVI per la configurazione dual-head, a meno che non diversamente specificato tramite 'ZaphodHeads' 'VGA-0'.

Inoltre, questa opzione consente di selezionare facilmente la schermata che si desidera contrassegnare come primario.

## Abilitare l'accelerazione video

L'ultima versione del pacchetto [mesa](https://www.archlinux.org/packages/?name=mesa) ha aggiunto il supporto alla decodifica per MPEG1/2 ai driver liberi, esportandola tramite [libvdpau](https://www.archlinux.org/packages/?name=libvdpau). Dopo averlo installato, assegnare il valore `vdpau` alla variabile d'ambiente `LIBVA_DRIVER_NAME` il nome del core del driver a `VDPAU_DRIVER`, ad es.:

 `~/.bashrc` 
```
export LIBVA_DRIVER_NAME=vdpau
export VDPAU_DRIVER=r600
```

## Disabilitare il vsync

Il driver radeon abiliterà la sincronia verticale di default, scelta adatta ad ogni situazione fuorchè il misuramento delle prestazioni. Per disabilitarla, creare il file `~/.drirc` (o modificarlo se già esistente) ed aggiungere la sezione seguente:

 `~/.drirc` 
```
<driconf>
    <device screen="0" driver="dri2">
        <application name="Default">
            <option name="vblank_mode" value="0" />
        </application>
    </device>
    <!-- Other devices ... -->
</driconf>

```

Come valore del campo driver, bisogna inserire precisamente **dri2**, e non il codice della propria scheda video (come ad es. r600).

## Risoluzione dei problemi

### Rilevo artefatti quando effettuo il login nel mio DE o WM

Se si riscontrano artefatti grafici, per prima cosa provare ad avviare X senza l'ausilio del file `/etc/X11/xorg.conf`. Le ultime versioni di Xorg sono affidabili e in grado di effettuare un rilevamento automatico e auto-configurazione nella maggior parte dei casi l'uso. File `xorg.conf` obsoleti o non correttamente configurati sono noti per causare conflitti.

Per poter funzionare senza un file di configurazione, si raccomanda che il pacchetto del gruppo `xorg-input-drivers` sia installato.

È possibile che questi problemi siano legati a KMS. Se questo è il problema, vedi [Disabilitare KMS.](#Disabilitare_KMS)

Si può anche provare a disabilitare EXAPixmaps nella sezione "Device" di `/etc/X11/xorg.conf.d/20-radeon.conf`::

 `/etc/X11/xorg.conf` 
```
.....
Option "EXAPixmaps" "off"
.....

```

Anche l'opzione AccelDFS sembra essere causa di artefatti, provare a disabilitarla con questa stringa

 `/etc/X11/xorg.conf.d/20-radeon.conf` 
```
.....
Option "AccelDFS" "off"
.....

```

### Aggiungere risoluzioni non rilevate

ad es. se la rilevazione dall'EDID fallisce su una connessione DisplayPort.

Questo problema è affrontato nella pagina di [Xrandr](/index.php/Xrandr#Adding_undetected_resolutions "Xrandr").

### Performance scadenti con driver libero

Alcune schede video possono essere installate di base provando ad usare [KMS](/index.php/ATI#AMD.2FAti_cards_and_kernel_mode-setting_.28KMS.29 "ATI"). È possibile verificare se è questo il caso lanciando:

```
dmesg | egrep "drm|radeon"

```

Questo comando dovrebbe mostrare qualcosa *come* questo, ciò significa che la scheda sta provando ad usare KMS:

```
[drm] radeon default to kernel modesetting.
...
[drm:radeon_driver_load_kms] *ERROR* Failed to initialize radeon, disabling IOCTL

```

Se la scheda non è supportata da KMS (qualunque scheda più vecchia di r100), allora è possibile [disabilitare KMS](#Disabilitare_KMS). Questo dovrebbe risolvere il problema.

### L'AGP è disabilitato (con il KMS)

Se si riscontrano prestazioni scadenti, e dmesg mostra qualcosa del genere

```
[drm:radeon_agp_init] *ERROR* Unable to acquire AGP: -19

```

verificare che il driver AGP della propria scheda madre (ad es., `via_agp`, `intel_agp` etc.) sia caricato prima del modulo `radeon`, consultare [#Abilitare KMS](#Abilitare_KMS)

### Collegando un TV viene mostrato un bordo nero attorno allo schermo

Se collegando un TV ad una Radeon 5770 tramite l'uscita HDMI, viene mostrata un'immagine sfocata con un bordo nero nero di 2-3cm, ciò è dovuto alla protezione da [overscan](https://en.wikipedia.org/wiki/http://en.wikipedia.org/wiki/Overscan#Overscan_in_computers "wikipedia:http://en.wikipedia.org/wiki/Overscan"), che può essere disabilitata tramite xrandr

 `xrandr --output HDMI-0 --set underscan off` 

### Schermo nero con cursore del mouse visibile al resume dalla sospensione

Risvegliando dalla sospensione un sistema dotato di scheda video con un quantitativo di Ram inferiore o uguale a 32 MB, può risultare in uno schermo nero col solo puntatore visibile. Alcune parti dello schermo potrebbero venire rivisualizzate al passaggio del puntatore. Forzando l'abilitazione di `EXAPixmaps` all'interno di `/etc/X11/xorg.conf.d/20-radeon.conf` il problema potrebbe venire risolto. Consultare il paragrafo [Ottimizzazione prestazioni](#Ottimizzazione_prestazioni) per ulteriori informazioni.

### Nessun effetto desktop in KDE4 con la X1300 ed i driver Radeon

Un bug di KDE4 può impedire un controllo video accurato, avendo come conseguenza la disattivazione degli effetti desktop, nonostante la X1300 disponga di una potenza di calcolo ben superiore a quella necessaria. Un workaround potrebbe essere quello di sovrascrivere manualmente tale controllo nei file di configurazione di KDE `/usr/share/kde-settings/kde-profile/default/share/config/kwinrc` e/o `.kde/share/config/kwinrc` aggiungendo il seguente codice alla sezione `[Composoting]`:

```
DisableChecks=true
Enabled=true

```

### Schermo nero e nessuna console visualizzata, ma X funzionante sotto KMS

Questa è una soluzione ad un problema di non visualizzazione della console che potrebbe presentarsi utilizzando 2 o più schede video ATI sullo stesso sistema, come ad esempio il laptop Fujitsu Siemens Amilo PA 3553\. Ciò è dovuto al driver di framebuffer `fbcon` che esegue la propria mappatura sul dispositivo framebuffer riferito alla scheda video sbagliata. Questo problema può essere risolto aggiungendo alla riga di boot del kernel il parametro `fbcon=map:1` In questo modo si istruirà il driver fbcon ad effettuare la mappatura sul dispositivo framebuffer `/dev/fb1` anzichè sul `/dev/fb0`, che nel caso in esame è la scheda sbagliata.

### Alcune applicazioni 3d vanno in crash o mostrano alcune textures completamente nere

Si potrebbe aver bisogno del supporto alle texture compresse, che non è incluso nei driver liberi. Installare [libtxc_dxtn](https://www.archlinux.org/packages/?name=libtxc_dxtn) oppure [lib32-libtxc_dxtn](https://www.archlinux.org/packages/?name=lib32-libtxc_dxtn) per sistemi multilib.

### Prestazioni 2D (ad esempio lo scroll) scadenti

Se si hanno problemi di prestazioni in 2D, ad esempio una lentezza inconsueta nello scrolling all'interno della finestra del browser o di un altro programma, potrebbe essere necessario aggiungere `Option "MigrationHeuristic" "greedy"` nella sezione `"Device"` del proprio file `xorg.conf`. Di seguito è mostrato un esempio di configurazione del file `/etc/X11/xorg.conf.d/**20-radeon.conf**`:

```
Section "Device"
        Identifier  "My Graphics Card"
        Driver  "radeon"
        Option  "MigrationHeuristic"  "greedy"
EndSection

```

### Applicazioni 3d mostrano finestra nera su ATI X1600 (RV530)

Ci sono tre possibili soluzioni:

*   Provare ad aggiungere `pci=nomsi` ai [parametri del kernel](/index.php/Kernel_parameters "Kernel parameters") del proprio boot loader.
*   Se questo non dovesse sortire alcun effetto, provare a inserire `noapic` al posto di `pci=nomsi`.
*   In ultima istanza, si può provare ad eseguire `vblank_mode=0 glxgears` o `vblank_mode=1 glxgears` e verificare quale dei due funziona, quindi installare `driconf` via pacman ed impostare quell'opzione in `~/.drirc`.