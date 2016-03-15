Da [http://www.x.org/wiki/](http://www.x.org/wiki/):

	*Il progetto X.Org fornisce un'implementazione open source del sistema X Window. Il lavoro di sviluppo è stato fatto in collaborazione con la comunità freedesktop.org. La Fondazione X.Org è l' organizzazione no-profit educativa, il cui Consiglio serve questo sforzo, e in cui tutti i membri conducono questo lavoro.*

**Xorg** è un'applicazione pubblica e open-source del sistema X-window versione 11\. Dal momento che Xorg è la scelta più popolare tra gli utenti Linux, la sua ubiquità ha portato a renderlo un requisito sempre presente per le applicazioni GUI, con conseguente adozione massiccia dalla maggior parte delle distribuzioni. Consultare l'articolo di Wikipedia [Xorg](https://en.wikipedia.org/wiki/X.Org_Server "wikipedia:X.Org Server") o visitare [Xorg website](http://www.x.org/wiki/) per ulteriori informazioni.

## Contents

*   [1 Installazione](#Installazione)
    *   [1.1 Installazione dei Driver](#Installazione_dei_Driver)
*   [2 Avvio](#Avvio)
*   [3 Configurazione](#Configurazione)
    *   [3.1 Utilizzando i file .conf](#Utilizzando_i_file_.conf)
    *   [3.2 Usare xorg.conf](#Usare_xorg.conf)
    *   [3.3 Configurazioni di esempio](#Configurazioni_di_esempio)
*   [4 Dispositivi di input](#Dispositivi_di_input)
    *   [4.1 Mouse acceleration](#Mouse_acceleration)
    *   [4.2 Extra mouse buttons](#Extra_mouse_buttons)
    *   [4.3 Touchpad Synaptics](#Touchpad_Synaptics)
    *   [4.4 Keyboard settings](#Keyboard_settings)
*   [5 Impostazioni del monitor](#Impostazioni_del_monitor)
    *   [5.1 Come iniziare](#Come_iniziare)
    *   [5.2 Monitor multipli](#Monitor_multipli)
        *   [5.2.1 Con più di una scheda grafica](#Con_pi.C3.B9_di_una_scheda_grafica)
    *   [5.3 Dimensione dello schermo e DPI](#Dimensione_dello_schermo_e_DPI)
        *   [5.3.1 Impostazione manuale DPI](#Impostazione_manuale_DPI)
    *   [5.4 DPMS](#DPMS)
*   [6 Composite](#Composite)
*   [7 Consigli utili](#Consigli_utili)
    *   [7.1 Modifiche allo script di avvio di X](#Modifiche_allo_script_di_avvio_di_X)
    *   [7.2 Sessioni di X una dentro l'altra](#Sessioni_di_X_una_dentro_l.27altra)
    *   [7.3 Avvio programmi con interfaccia grafica in remoto](#Avvio_programmi_con_interfaccia_grafica_in_remoto)
    *   [7.4 Disattivazione e attivazione a richiesta delle sorgenti di ingresso](#Disattivazione_e_attivazione_a_richiesta_delle_sorgenti_di_ingresso)
*   [8 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [8.1 Problemi comuni](#Problemi_comuni)
    *   [8.2 Ctrl destro non funziona con tastiera oss](#Ctrl_destro_non_funziona_con_tastiera_oss)
    *   [8.3 Errore avviando il client X con "su"](#Errore_avviando_il_client_X_con_.22su.22)
    *   [8.4 Programmi che richiedono "font '(null)'"](#Programmi_che_richiedono_.22font_.27.28null.29.27.22)
    *   [8.5 Problemi con la modalità Frame-buffer](#Problemi_con_la_modalit.C3.A0_Frame-buffer)
    *   [8.6 DRI smette di funzionare con le schede Matrox](#DRI_smette_di_funzionare_con_le_schede_Matrox)
    *   [8.7 Ripristino: disattivare Xorg prima della schermata di login](#Ripristino:_disattivare_Xorg_prima_della_schermata_di_login)
    *   [8.8 Errore di X all'avvio : Inizializzazione della tastiera fallito](#Errore_di_X_all.27avvio_:_Inizializzazione_della_tastiera_fallito)
    *   [8.9 Schermo nero, nessun protocollo specificato .., Risorsa temporaneamente non disponibile per tutti o alcuni utenti](#Schermo_nero.2C_nessun_protocollo_specificato_...2C_Risorsa_temporaneamente_non_disponibile_per_tutti_o_alcuni_utenti)

## Installazione

È necessario [installare](/index.php/Pacman "Pacman") il pacchetto essenziale [xorg-server](https://www.archlinux.org/packages/?name=xorg-server), reperibile nei [Depositi ufficiali](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)").

Inoltre alcuni pacchetti del gruppo [xorg-apps](https://www.archlinux.org/groups/x86_64/xorg-apps/) sono utili per alcune attività di configurazione, essi sono segnalati nella sezione/pagina dedicata.

```
# pacman -Syu xorg-server

```

**Suggerimento:** L' ambiente di default X è piuttosto spoglia , e si cercherà in linea di installare un [window manager](/index.php/Window_Manager_(Italiano) "Window Manager (Italiano)") or a [desktop environment](/index.php/Desktop_Environment_(Italiano) "Desktop Environment (Italiano)") in supplemento ad X.

### Installazione dei Driver

Il kernel Linux include driver video open-source e il supporto per il framebuffer hardware accelerato. Tuttavia, il supporto in spazio utente è necessario per OpenGL e l'accelerazione 2D in X11 .

Per prima cosa, identificare la vostra scheda:

```
$ lspci | grep "VGA"

```

Quindi, installare un driver appropriato. È possibile cercare nel database dei pacchetti per un elenco completo dei driver video open-source:

```
# pacman -Ss xf86-video

```

Il driver grafico predefinito è *VESA* ( pacchetto [xf86-video-vesa](https://www.archlinux.org/packages/?name=xf86-video-vesa)), che gestisce un gran numero di chipset, ma non include alcuna accelerazione 2D o 3D. Se un driver migliore non può essere trovato o non viene caricato, Xorg ricadrà su *vesa*.

Al fine di poter usufruire dell'accelerazione video per lavorare, e spesso per poter usufruire di tutte le modalità che la GPU può impostare, è necessario un driver video corretto:

| Marca | Tipo | Driver | Pacchetti [Multilib](/index.php/Multilib "Multilib")
(Per eseguire applicazioni 32 bit su Arch x86_64) |  Documentazione  |
| ** AMD/ATI ** |  Open source  | [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [ATI (Italiano)](/index.php/ATI_(Italiano) "ATI (Italiano)") |
| Proprietary | [catalyst](https://aur.archlinux.org/packages/catalyst/) | [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/) | [ATI Catalyst (Italiano)](/index.php/ATI_Catalyst_(Italiano) "ATI Catalyst (Italiano)") |
| **Intel** | Open source | [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [Intel (Italiano)](/index.php/Intel_(Italiano) "Intel (Italiano)") |
| **Nvidia** | Open source | [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [Nouveau (Italiano)](/index.php/Nouveau_(Italiano) "Nouveau (Italiano)") |
| Proprietary | [nvidia](https://www.archlinux.org/packages/?name=nvidia) | [lib32-nvidia-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-libgl) | [NVIDIA (Italiano)](/index.php/NVIDIA_(Italiano) "NVIDIA (Italiano)") |
| [nvidia-304xx](https://www.archlinux.org/packages/?name=nvidia-304xx) | [lib32-nvidia-304xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-304xx-utils) |
| [nvidia-173xx](https://aur.archlinux.org/packages/nvidia-173xx/) | [lib32-nvidia-173xx-utils](https://aur.archlinux.org/packages/lib32-nvidia-173xx-utils/) |
| [nvidia-96xx](https://aur.archlinux.org/packages/nvidia-96xx/) | [lib32-nvidia-96xx-utils](https://aur.archlinux.org/packages/lib32-nvidia-96xx-utils/) |
| **VIA** | Open source | [xf86-video-openchrome](https://www.archlinux.org/packages/?name=xf86-video-openchrome) | – | [VIA](/index.php/Via "Via") |

Xorg dovrebbe funzionare senza problemi senza i driver "closed source", che in genere sono necessari solo per funzioni avanzate come il fast rendering con accelerazione 3D per i giochi, configurazioni dual-screen e TV-out.

## Avvio

	*Si veda anche: [Avviare X al login](/index.php/Start_X_at_Login_(Italiano) "Start X at Login (Italiano)")*

**Suggerimento:** Il modo più semplice per avviare X è quello di utilizzare un [display manager](/index.php/Display_Manager_(Italiano) "Display Manager (Italiano)"), come [GDM](/index.php/GDM "GDM"), [KDM](/index.php/KDM "KDM") o [SLiM](/index.php/SLiM "SLiM").

Se si desidera avviare X senza l'ausilio di un display manager, si installi il pacchetto [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit). Opzionalmente anche i pacchetti [xorg-twm](https://www.archlinux.org/packages/?name=xorg-twm), [xorg-xclock](https://www.archlinux.org/packages/?name=xorg-xclock) e [xterm](https://www.archlinux.org/packages/?name=xterm), che permettono di avere un ambiente di lavoro predefinito, come descritto in seguito.

I comandi `startx` e `xinit` permettono di avviare il server X ed il lato client (lo script `startx` è solamente un front end al comando `xinit`). Per determinare il client da avviare, `startx`/`xinit` cercherà prima di analizzare un file `~/.xinitrc` nella directory home dell'utente. In assenza del file `~/.xinitrc`, analizzerà il file globale predefinito `/etc/X11/xinit/xinitrc`, che ha come valore predefinito, quello di iniziare un ambiente di base con il window manager [Twm](/index.php/Twm_(Italiano) "Twm (Italiano)"), [Xclock](https://en.wikipedia.org/wiki/Xclock "wikipedia:Xclock") e [Xterm](/index.php/Xterm "Xterm").

Per maggiori informazioni, si veda [xinitrc](/index.php/Xinitrc_(Italiano) "Xinitrc (Italiano)").

**Nota:**

*   X deve sempre essere eseguito sulla stessa tty in cui si è verificato il login, per preservare la sessione logind. Questo è gestito in modo predefinito da `/etc/X11/xinit/xserverrc`.
*   Se si verifica un problema, potete visualizzare il log di registro di `/var/log/Xorg.0.log`. Cercate tutte le linee che iniziano con `(EE)`, che identificano la presenza di un errore, e anche le linee che iniziano cone `(WW)`, che sono dei warnings che possono identificare un eventuale problema.
*   Se avete un file `.xinitrc` *vuoto* nella vostra `$HOME`, eliminatelo o modificatelo al fine di avviare X correttamente. Se non si esegue questa operazione X mostrerà una schermata vuota e nel vostro `Xorg.0.log` non riscontrerete nessun errore rilevante. Semplicemente eliminandolo farà sì che X sia in grado di funzionare con un ambiente predefinito.

**Attenzione:** Se si sceglie di utilizzare `xinit` al posto di `startx`, siate responsabili di passare il parametro `-nolisten tcp` e di garantire che la sessione non si rompa avviando X su una tty diversa.

## Configurazione

**Note:** Arch Linux fornisce dei file di configurazione predefiniti in `/etc/X11/xorg.conf.d`, e nessuna configurazione aggiuntiva è necessaria per la maggior parte delle configurazioni.

Xorg usa un file di configurazione chiamato `xorg.conf` e file che terminano con il suffisso `.conf` per la sua configurazione iniziale : l' elenco completo delle cartelle in cui i file vengono cercati può essere trovato [qui](http://www.x.org/releases/current/doc/man/man5/xorg.conf.5.xhtml) o eseguendo `man xorg.conf`, insieme ad una spiegazione dettagliata di tutte le le opzioni disponibili.

### Utilizzando i file .conf

La cartella `/etc/X11/xorg.conf.d/` include configurazioni specifiche dell'utente. Siete liberi di aggiungere i file di configurazione nella directory, ma devono avere un suffiso `.conf`: i file vengono letti in ordine ASCII, e per convenzione i loro nomi devono iniziare con `**XX**-` (due cifre ed un trattino, in modo che per esempio 10 viene letto prima di 20). Questi file vengono analizzati dal server X all'avvio e sono trattati come parte del tradizionale file di configurazione `xorg.conf`. Il server X tratta essenzialmente la raccolta di file di configurazione, come un unico grande file con le voci di `xorg.conf` alla fine.

### Usare xorg.conf

Xorg può anche essere configurato tramite `/etc/X11/xorg.conf` o `/etc/xorg.conf`. Potete generare uno scheletro di xorg.conf tramite:

```
 # Xorg :0 -configure

```

Questo dovrebbe creare un file `xorg.conf.new` in `/root/` che dovrete copiare come `/etc/X11/xorg.conf`, per maggiori informazioni si veda `man xorg.conf`.

In alternativa, i driver proprietari della scheda video potrebbero includere uno strumento per configurare automaticamente Xorg. Si veda l'articolo relativo al proprio driver video, [NVIDIA](/index.php/NVIDIA_(Italiano) "NVIDIA (Italiano)") o [AMD Catalyst](/index.php/AMD_Catalyst_(Italiano) "AMD Catalyst (Italiano)") per i dettagli.

**Nota:** Le parole chiavi del file di configurazione sono case-insensitive, e i caratteri "_" vengono ignorati. La maggior parte delle stringhe (compresi i nomi di Option ) sono case-insensitive, e insensibili agli spazi bianchi e caratteri "_".

### Configurazioni di esempio

*   `xorg.conf`

	[Sample 1](http://pastebin.com/raw.php?i=EuSKahkn)

**Nota:** Le sezioni "InputDevice" sono commentate, questo perché ora sarà `/etc/X11/xorg.conf.d/10-evdev.conf` a farsi carico della configurazione del layout della tastiera.

*   `/etc/X11/xorg.conf.d/10-evdev.conf`

	[Sample 1](http://pastebin.com/raw.php?i=4mPY35Mw)

**Nota:** Questo è il file `10-evdev.conf` che va in abbinamento all'esempio 1 del file xorg.conf

*   `/etc/X11/xorg.conf.d/10-monitor.conf`

1.  [VMware](http://pastebin.com/raw.php?i=fJv8EXGb)
2.  [KVM](http://pastebin.com/raw.php?i=NRz7v0Kn)
3.  [NVIDIA](https://gist.github.com/daemox/6325050)

**Nota:** I driver binari nvidia-ck ( V325 ); dual GPU, doppio monitor, Dual Screen; Twinview No, No Xinerama, ruotato e posizionato verticalmente screen1 sopra Screen0.

## Dispositivi di input

[Udev](/index.php/Udev_(Italiano) "Udev (Italiano)") sarà in grado di rilevare tutto l'hardware ed [evdev](https://en.wikipedia.org/wiki/evdev è fornito da [systemd](https://www.archlinux.org/packages/?name=systemd) e [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev) è richiesto dal pacchetto [xorg-server](https://www.archlinux.org/packages/?name=xorg-server), quindi l'installazione dei driver di input non è necessaria per la maggior parte dell'hardware. Tuttavia, se evdev non supporta il dispositivo, installare il driver necessario dal gruppo [xorg-drivers](https://www.archlinux.org/groups/x86_64/xorg-drivers/) (lanciare `pacman -Sg xorg-drivers` per averne un elenco).

Si dovrebbe avere il file `10-evdev.conf` nella directory `/etc/X11/xorg.conf.d/`, che gestisce tastiera, mouse, touchpad e touchscreen.

Vedere le pagine seguenti per istruzioni specifiche , o il [Fedora wiki](https://fedoraproject.org/wiki/Input_device_configuration) per ulteriori esempi.

### Mouse acceleration

Si veda la pagina principale: [Mouse acceleration](/index.php/Mouse_acceleration "Mouse acceleration")

### Extra mouse buttons

Si veda la pagina principale: [All Mouse Buttons Working](/index.php/All_Mouse_Buttons_Working "All Mouse Buttons Working")

### Touchpad Synaptics

Si veda la pagina principale: [Touchpad Synaptics](/index.php/Touchpad_Synaptics_(Italiano) "Touchpad Synaptics (Italiano)")

### Keyboard settings

Si veda la pagina principale: [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg")

## Impostazioni del monitor

### Come iniziare

**Note:** Le nuove versioni di Xorg sono auto-configuransti, non dovrebbe essere necessario utilizzare questo passaggio.

Per prima cosa, creare un nuovo file di configurazione, `/etc/X11/xorg.conf.d/10-monitor.conf`.

Inserire il codice riportato in seguito nel file creato sopra:

 `/etc/X11/xorg.conf.d/10-monitor.conf` 
```
Section "Monitor"
    Identifier             "Monitor0"
EndSection

Section "Device"
    Identifier             "Device0"
    Driver                 "vesa" #Choose the driver used for this monitor
EndSection

Section "Screen"
    Identifier             "Screen0"  #Collapse Monitor and Device section to Screen section
    Device                 "Device0"
    Monitor                "Monitor0"
    DefaultDepth            16 #Choose the depth (16||24)
    SubSection             "Display"
        Depth               16
        Modes              "1024x768_75.00" #Choose the resolution
    EndSubSection
EndSection

```

### Monitor multipli

Si veda l'articolo principale [Multihead](/index.php/Multihead "Multihead") per informazioni generali.

*   [NVIDIA (Italiano)#Monitor multipli](/index.php/NVIDIA_(Italiano)#Monitor_multipli "NVIDIA (Italiano)").
*   [Nouveau_(Italiano)#Dual_Head](/index.php/Nouveau_(Italiano)#Dual_Head "Nouveau (Italiano)")
*   [AMD_Catalyst_(Italiano)#Double_Screen_.28Dual_Head_.2F_Dual_Screen_.2F_Xinerama.29](/index.php/AMD_Catalyst_(Italiano)#Double_Screen_.28Dual_Head_.2F_Dual_Screen_.2F_Xinerama.29 "AMD Catalyst (Italiano)")
*   [ATI_(Italiano)#Configurare_la_modalit.C3.A0_Dual_Head](/index.php/ATI_(Italiano)#Configurare_la_modalit.C3.A0_Dual_Head "ATI (Italiano)")

#### Con più di una scheda grafica

È necessario definire il driver da utilizzare ed aggiungere l'ID bus della scheda grafica.

```
Section "Device"
    Identifier      "Screen0"
    Driver          "nouveau"
    BusID           "PCI:0:12:0"
EndSection

Section "Device"
    Identifier      "Screen1"
    Driver          "radeon"
    BusID           "PCI:1:0:0"
EndSection

```

Per ottenere l'ID bus :

 `$ lspci | grep VGA` 
```
 01:00.0 VGA compatible controller: nVidia Corporation G96 [GeForce 9600M GT] (rev a1)

```

Nell'esempio, l'ID bus è 1:0:0.

### Dimensione dello schermo e DPI

Il DPI dell'X server è determinato nel modo seguente:

1.  L'opzione riga di comando -dpi ha la massima priorità.
2.  Se questa non viene utilizzata, l'impostazione della dimensione dello schermo nel file di configurazione di X, è utilizzata per determinare il DPI, data la risoluzione dello schermo.
3.  Se non viene fornita la dimensione schermo, i valori di dimensione del monitor DDC vengono utilizzati per ricavare la DPI, data la risoluzione dello schermo.
4.  Se il DDC non specifica una dimensione, il valore DPI 75 viene utilizzato di default.

Per ottenere una corretta impostazione dei "punti per pollice" (DPI), la dimensione del display deve essere conosciuta oppure impostata. Impostare correttamente il DPI è necessario soprattutto quando è richiesta una risoluzione fine (come per il rendering dei font). In precedenza i produttori cercavano di creare uno standard per 96 DPI (un monitor 10.3 " in diagonale sarebbe 800x600, un monitor 13,2" 1024x768). I monitor attuali possono essere di un qualsiasi numero di DPI e questo non può corrispondere orizzontalmente e verticalmente. Ad esempio, un LCD 19" widescreen 1440x900 può avere un DPI di 89x87\. Per essere in grado di impostare il DPI, il server Xorg tenta di rilevare automaticamente la dimensione fisica dello schermo del monitor tramite la scheda grafica con [DDC](https://en.wikipedia.org/wiki/Display_Data_Channel "wikipedia:Display Data Channel"). ~~Quando il server Xorg sarà a conoscenza della dimensione fisica dello schermo, sarà anche in grado di impostare il corretto DPI a seconda delle dimensioni di risoluzione.~~

Per verificare se le dimensioni del display e DPI sono rilevati e calcolati correttamente:

```
$ xdpyinfo | grep -B2 resolution

```

Verificare che le dimensioni corrispondano alla dimensione di visualizzazione. Se il server Xorg non è in grado di calcolare correttamente le dimensioni dello schermo, il valore verrà predefinito a 75x75 DPI e si dovrà calcolarlo ed impostarlo manualmente.

Se si dispone di indicazioni sulla dimensione fisica dello schermo, possono essere inserite nel file di configurazione di Xorg, in modo che il DPI corretto venga calcolato come segue:

```
Section "Monitor"
    Identifier "Monitor0"
    DisplaySize 286 179    # In millimeters
EndSection

```

Se si desidera inserire solamente le specifiche del monitor senza creare un file xorg.conf completo, in primo luogo creare un nuovo file di configurazione, per esempio, `/etc/X11/xorg.conf.d/90-monitor.conf`:

```
Section "Monitor"
    Identifier "<default monitor>"
    DisplaySize 286 179    # In millimeters
EndSection

```

Se non si dispone di specifiche per la larghezza e l'altezza dello schermo orizzontale e fisico (attualmente la maggior parte delle specifiche sono elencate solo per dimensione diagonale), è possibile utilizzare la risoluzione nativa del monitor (o rapporto di aspetto) e di lunghezza diagonale per calcolare le dimensioni fisiche orizzontali e verticali. Utilizzando il teorema di Pitagora in uno schermo con diagonale 13,3", con risoluzione nativa 1280x800 (o aspect ratio 16:10):

```
$ echo 'scale=5;sqrt(1280^2+800^2)' | bc  # 1509.43698

```

Questo darà la lunghezza della diagonale in pixel e con questo valore si possono ottenere le lunghezze fisiche orizzontali e verticali (e convertirle in millimetri):

```
$ echo 'scale=5;(13.3/1509)*1280*25.4' | bc  # 286.43072
$ echo 'scale=5;(13.3/1509)*800*25.4' | bc   # 179.01920

```

**Nota:** Questo calcolo funziona per le dimensioni di più tipi di monitor, tuttavia vi sono monitor più economici che di rado possono comprimere il rapporto di aspetto (per esempio la risoluzione 16:10 a 16:9) in tal caso si dovrebbe misurare la dimensione dello schermo manualmente.

#### Impostazione manuale DPI

Il DPI può essere impostato manualmente solo se si prevede di utilizzare una risoluzione [DPI calculator](http://pxcalc.com/)):

```
Section "Monitor"
    Identifier "Monitor0"
    Option   "DPI" "96 x 96"
EndSection

```

Se si utilizza una scheda Nvidia, è possibile impostare manualmente il DPI aggiungendo le seguenti opzioni su */etc/X11/xorg.conf.d/20-nvidia.conf* (nella sezione **Device**):

```
Option "UseEdidDpi" "False"
Option  "DPI" "96 x 96"

```

Per i driver compatibili con RandR, è possibile impostare:

```
$ xrandr --dpi 96

```

Consultare [Execute commands after X start](/index.php/Execute_commands_after_X_start "Execute commands after X start") per salvare le modifiche.

**Nota:** Mentre è possibile impostare qualsiasi dpi a piacimento le applicazioni che utilizzando Qt e GTK le scaleranno di conseguenza, si consiglia quindi di impostarlo su 96, 120 (25 % in più), 144 (il 50 % in più), 168 (il 75 % in più), 192 (100 % in più) , ecc , per ridurre gli artefatti di scaling di GUI che utilizzano immagini bitmap. Riducendola sotto 96 dpi non può ridurre la dimensione di elementi grafici di interfaccia grafica come in genere la più bassa dpi utilizzata per le icone sono fatte per 96.

### DPMS

Il DPMS (Display Power Management Signaling) è una tecnologia che permette il risparmio energetico dei monitor quando il computer non è in uso. Ciò permetterà di avere monitor che vanno automaticamente in standby dopo un determinato periodo . Si veda: [DPMS](/index.php/DPMS "DPMS")

## Composite

L'estensione Composite per X provoca un intero sotto-albero della gerarchia della finestra per eseguire il rendering di un buffer fuori schermo. Le applicazioni possono poi prendere il contenuto di questo buffer e farne ciò che vogliono. Il buffer off-screen può essere fatto confluire automaticamente nella finestra padre o fusa per programmi esterni, chiamati manager compositing. Vedere le pagine seguenti per ulteriori informazioni .

*   [Compiz](/index.php/Compiz_(Italiano) "Compiz (Italiano)") -- L'originale composite/window manager creato da Novell
*   [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") -- Semplice composite manager capace di ombreggiature e primitive trasparenze
*   [Compton](/index.php/Compton "Compton") -- Un fork di [xcompmgr](/index.php/Xcompmgr "Xcompmgr") con funzioni migliorate e bug fix
*   [Cairo Composite Manager](/index.php/Cairo_Compmgr "Cairo Compmgr") -- Un versatile ed estensibile composite manager che utilizza cairo per il rendering.
*   [Wikipedia:it:Compositing window manager](https://en.wikipedia.org/wiki/it:Compositing_window_manager "wikipedia:it:Compositing window manager")

## Consigli utili

### Modifiche allo script di avvio di X

Per le opzioni di X si consulti:

```
$ man Xserver

```

Le seguenti opzioni devono essere aggiunte alla variabile `"defaultserverargs"` nel file `/usr/bin/startx`.

*   abilitare il caricamento ritardato dei glyph per i font a 16 bit:

```
-deferglyphs 16

```

**Nota:** Se si avvia X con kdm, sembra che lo script startx non venga eseguito. Queste opzioni devono essere aggiunte alla variabile `"ServerArgsLocal"` o `"ServerCmd"` nel file `/usr/share/config/kdm/kdmrc`. Le opzioni di kdm predefinite sono:
```
ServerArgsLocal=-nolisten tcp
ServerCmd=/usr/bin/X
```

### Sessioni di X una dentro l'altra

Per avviare una sessione di X di un altro desktop environment dentro la presente:

```
$ /usr/bin/Xnest :1 -geometry 1024x768+0+0 -ac -name Windowmaker & wmaker -display :1

```

Questo lancerà una sessione Window Maker in una finestra 1024x768 dentro la sessione corrente di X.

Richiede l'installazione del pacchetto [xorg-server-xnest](https://www.archlinux.org/packages/?name=xorg-server-xnest).

### Avvio programmi con interfaccia grafica in remoto

Si veda l'articolo principale: [SSH#X11 forwarding](/index.php/SSH#X11_forwarding "SSH").

### Disattivazione e attivazione a richiesta delle sorgenti di ingresso

Con l'aiuto di *xinput* è possibile disabilitare o abilitare le sorgenti di ingresso temporaneamente. Questo potrebbe essere utile, ad esempio, su sistemi che hanno più di un mouse, come ad esempio i ThinkPad, e si preferisce utilizzarne solo uno per evitare clic indesiderati del mouse. Vediamo come eseguire questa operazione .

[Installare](/index.php/Pacman "Pacman") il pacchetto [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput) contenuto nei [repositori ufficiali](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)").

Trovare l'ID del dispositivo che si intende disabilitare:

```
$ xinput

```

Per esempio in un Lenovo ThinkPad T500, l'output del comando sarà simile a questo:

 `$ xinput` 
```
⎡ Virtual core pointer                          id=2    [master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer                id=4    [slave  pointer  (2)]
⎜   ↳ TPPS/2 IBM TrackPoint                     id=11   [slave  pointer  (2)]
⎜   ↳ SynPS/2 Synaptics TouchPad                id=10   [slave  pointer  (2)]
⎣ Virtual core keyboard                         id=3    [master keyboard (2)]
    ↳ Virtual core XTEST keyboard               id=5    [slave  keyboard (3)]
    ↳ Power Button                              id=6    [slave  keyboard (3)]
    ↳ Video Bus                                 id=7    [slave  keyboard (3)]
    ↳ Sleep Button                              id=8    [slave  keyboard (3)]
    ↳ AT Translated Set 2 keyboard              id=9    [slave  keyboard (3)]
    ↳ ThinkPad Extra Buttons                    id=12   [slave  keyboard (3)]

```

Disabilitare il dispositivo con `xinput --disable *device_id*`, dove per *device_id* si intende l'ID del dispistico che si vuole disabilitare. In questo esempio proverem,o a disabilitare il touchpad Synaptics, che ha come valore di ID 10:

```
$ xinput --disable 10

```

Per riabilitare il dispositivo basta dare il comando opposto:

```
$ xinput --enable 10

```

## Risoluzione dei problemi

### Problemi comuni

Se Xorg non dovesse avviarsi, o lo schermo fosse completamente nero, non funzionassero tastiera e mouse, ecc., innanzitutto si effettuino questi semplici passaggi:

*   Controllare il file di log: `cat /var/log/Xorg.0.log`
*   Controllare la pagina specifica in [Category:Input devices](/index.php/Category:Input_devices "Category:Input devices"), se riscontrate problemi con tastiera, mouse, touchpad, ecc.
*   Alla fine, cercare i problemi più comuni negli articoli riguardanti [ATI](/index.php/ATI_(Italiano) "ATI (Italiano)"), [Intel](/index.php/Intel_(Italiano) "Intel (Italiano)") e [NVIDIA](/index.php/NVIDIA_(Italiano) "NVIDIA (Italiano)").

### Ctrl destro non funziona con tastiera oss

Editare come root il file `/usr/share/X11/xkb/symbols/fr`, e cambiare la linea :

```
include "level5(rctrl_switch)"

```

in

```
// include "level5(rctrl_switch)"

```

Riavviare X oppure il sistema, oppure eseguire:

```
setxkbmap fr oss

```

### Errore avviando il client X con "su"

Se ottenete il messaggio di errore "Client is not authorized to connect to server" (il client non è autorizzato a connettersi al server), provate ad aggiungere la seguente stringa:

```
session        optional        pam_xauth.so

```

al file `/etc/pam.d/su`. `pam_xauth` sarà quindi impostato per gestire le chiavi di `xauth` e le variabili d'ambiente.

### Programmi che richiedono "font '(null)'"

*   Messaggio di errore: "*unable to load font `(null)'.*" (Impossibile caricare il tipo di carattere (null))

Alcuni programmi funzionano solo con i font bitmap. Sono disponibili due pacchetti principali con i font bitmap, [xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi) e [xorg-fonts-100dpi](https://www.archlinux.org/packages/?name=xorg-fonts-100dpi). Non vi è la necessità di installarli entrambi: uno solo di essi dovrebbe essere sufficiente. Per scoprire quale dei due pacchetti è più indicato per le vostre esigenze, lanciate il seguente comando in un terminale:

```
$ xdpyinfo | grep resolution

```

quindi installate il pacchetto che più si avvicina al vostro dato (75 o 100 al posto di XX)

```
# pacman -S xorg-fonts-XXdpi

```

### Problemi con la modalità Frame-buffer

Se il server X fallisce all'avvio e controllando il corrispettivo file log (`/var/log/Xorg.0.log`), notate il seguente messaggio:

```
(WW) Falling back to old probe method for fbdev
(II) Loading sub module "fbdevhw"
(II) LoadModule: "fbdevhw"
(II) Loading /usr/lib/xorg/modules/linux//libfbdevhw.so
(II) Module fbdevhw: vendor="X.Org Foundation"
       compiled for 1.6.1, module version=0.0.2
       ABI class: X.Org Video Driver, version 5.0
(II) FBDEV(1): using default device

Fatal server error:
Cannot run in framebuffer mode. Please specify busIDs for all framebuffer devices
```

Disinstallate fbdev:

```
# pacman -R xf86-video-fbdev

```

### DRI smette di funzionare con le schede Matrox

Se usate una scheda Matrox e DRI smette di funzionare dopo aver aggiornato Xorg, provate ad aggiungere la riga:

```
Option "OldDmaInit" "On"

```

alla sezione Device che fa riferimento alla vostra scheda video nello `xorg.conf`.

### Ripristino: disattivare Xorg prima della schermata di login

Se Xorg è impostato per avviarsi automaticamente e per qualche motivo è necessario evitare che si avvii prima che si presenti la schermata di login o che si entri nella propria sessione grafica (se ad esempio `rc.conf` è erroneamente configurato e Xorg non riconosce il mouse o la tastiera), è possibile disattivare il suo caricamento in due modi.

*   Cambia destinazione predefinita per rescue.target. Vedere [Systemd_(Italiano)#Cambiare_il_target_predefinito_all'avvio](/index.php/Systemd_(Italiano)#Cambiare_il_target_predefinito_all.27avvio "Systemd (Italiano)").
*   If you have not only a faulty system that makes Xorg unusable, but you have also set the GRUB menu wait time to zero, or cannot otherwise use GRUB to prevent Xorg from booting, you can use the Arch Linux live CD. Boot up the live CD and log in as root. You need a mount point, such as `/mnt`, and you need to know the name of the partition you want to mount.

Potete utilizzare il comando,

```
 # fdisk -l

```

per vedere le vostre partizioni. Di solito, quello che si desidera sarà simile a `/dev/sda1`. Dopodiché montate la vostra partizione in `/mnt`, utilizzando il comando

```
 # mount /dev/sda1 /mnt

```

In questo modo il file-system verrà visualizzato sotto `/mnt`. Da qui potate eliminare il modulo `gdm` ( o similare) per impedire l'avvio di Xorg normalmente, o apportare altre modifiche necessarie.

### Errore di X all'avvio : Inizializzazione della tastiera fallito

Se il disco rigido è pieno, startx fallisce. La fine di `/var/log/Xorg.0.log` sarà:

```
 (EE) Error compiling keymap (server-0)
 (EE) XKB: Couldn't compile keymap
 (EE) XKB: Failed to load keymap. Loading default keymap instead.
 (EE) Error compiling keymap (server-0)
 (EE) XKB: Couldn't compile keymap
 XKB: Failed to compile keymap
 Keyboard initialization failed. This could be a missing or incorrect setup of xkeyboard-config.
 Fatal server error:
 Failed to activate core devices.
 Please consult the The X.Org Foundation support  at [http://wiki.x.org](http://wiki.x.org)
 for help.
 Please also check the log file at "/var/log/Xorg.0.log" for additional information.
  (II) AIGLX: Suspending AIGLX clients for VT switch

```

Liberare un po' di spazio sulla partizione root e X verrà eseguito.

### Schermo nero, nessun protocollo specificato .., Risorsa temporaneamente non disponibile per tutti o alcuni utenti

X crea i file di configurazione e temporanei nella directory home dell'utente corrente. Assicurarsi che ci sia spazio libero su disco disponibile nella partizione dive la directory home risiede. Purtroppo, in questo caso, il server X non fornisce informazioni più evidenti per la mancanza di spazio su disco.