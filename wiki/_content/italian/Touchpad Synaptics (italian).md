Articoli correlati

*   [Xorg](/index.php/Xorg "Xorg")

Questo articolo spiega il processo di installazione e configurazione de ***Synaptics input driver*** per i touchpad Synaptics (e ALPS) che si trovano sulla maggior parte dei notebook.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Opzioni usate di frequente](#Opzioni_usate_di_frequente)
    *   [2.2 Altre opzioni](#Altre_opzioni)
    *   [2.3 GNOME](#GNOME)
    *   [2.4 MATE](#MATE)
    *   [2.5 Configurazioni al volo](#Configurazioni_al_volo)
        *   [2.5.1 Strumenti da console](#Strumenti_da_console)
        *   [2.5.2 Strumenti grafici](#Strumenti_grafici)
*   [3 Configurazione avanzata](#Configurazione_avanzata)
    *   [3.1 Usare xinput per determinare le funzionalità del touchpad](#Usare_xinput_per_determinare_le_funzionalit.C3.A0_del_touchpad)
    *   [3.2 Synclient](#Synclient)
    *   [3.3 Scrolling Circolare](#Scrolling_Circolare)
    *   [3.4 Scrolling Naturale](#Scrolling_Naturale)
    *   [3.5 Interruttore software](#Interruttore_software)
    *   [3.6 Disabilitare il Trackpad durante la digitazione](#Disabilitare_il_Trackpad_durante_la_digitazione)
        *   [3.6.1 Rilevamento automatico del palmo della mano](#Rilevamento_automatico_del_palmo_della_mano)
        *   [3.6.2 Usando .xinitrc](#Usando_.xinitrc)
        *   [3.6.3 Usando un Login Manager](#Usando_un_Login_Manager)
*   [4 Risoluzione problemi](#Risoluzione_problemi)
    *   [4.1 xorg.conf.d/10-synaptics.conf sembra non essere applicato in GNOME e MATE](#xorg.conf.d.2F10-synaptics.conf_sembra_non_essere_applicato_in_GNOME_e_MATE)
        *   [4.1.1 ALPS Touchpads](#ALPS_Touchpads)
    *   [4.2 Il touchpad non funziona, Xorg.0.log presenta "Query no Synaptics: 6003C8"](#Il_touchpad_non_funziona.2C_Xorg.0.log_presenta_.22Query_no_Synaptics:_6003C8.22)
    *   [4.3 Touchpad rilevato come "PS/2 Generic Mouse" o "Logitech PS/2 mouse"](#Touchpad_rilevato_come_.22PS.2F2_Generic_Mouse.22_o_.22Logitech_PS.2F2_mouse.22)
    *   [4.4 Abilità speciali di Synaptics non-funzionanti (multi-tocco, scrolling, ecc.)](#Abilit.C3.A0_speciali_di_Synaptics_non-funzionanti_.28multi-tocco.2C_scrolling.2C_ecc..29)
    *   [4.5 Disabilitare il touchpad non appena venga rilevato un mouse esterno](#Disabilitare_il_touchpad_non_appena_venga_rilevato_un_mouse_esterno)
    *   [4.6 Il cursore salta](#Il_cursore_salta)
    *   [4.7 Multitouch](#Multitouch)
    *   [4.8 Il dispositivo touchpad non si trova in /dev/input/*](#Il_dispositivo_touchpad_non_si_trova_in_.2Fdev.2Finput.2F.2A)
    *   [4.9 Firefox e azioni speciali per il touchpad](#Firefox_e_azioni_speciali_per_il_touchpad)
    *   [4.10 Opera: problemi di scorrimento orizzontale](#Opera:_problemi_di_scorrimento_orizzontale)
    *   [4.11 Scorrimento e azioni multiple con Synaptics sui portatili LG](#Scorrimento_e_azioni_multiple_con_Synaptics_sui_portatili_LG)
    *   [4.12 Altri problemi con mouse esterni](#Altri_problemi_con_mouse_esterni)
    *   [4.13 Problemi di sincronizzazione del Touchpad](#Problemi_di_sincronizzazione_del_Touchpad)
    *   [4.14 Ritardo tra la pressione sul pulsante e il click effettivo](#Ritardo_tra_la_pressione_sul_pulsante_e_il_click_effettivo)
    *   [4.15 SynPS/2 Synaptics TouchPad can't grab event device, errno=16](#SynPS.2F2_Synaptics_TouchPad_can.27t_grab_event_device.2C_errno.3D16)
    *   [4.16 Synaptics perde il Rilevamento del Multitocco dopo aver effettuato il Reboot da Windows](#Synaptics_perde_il_Rilevamento_del_Multitocco_dopo_aver_effettuato_il_Reboot_da_Windows)
    *   [4.17 Touchpad senza pulsanti (o ClickPad)](#Touchpad_senza_pulsanti_.28o_ClickPad.29)
    *   [4.18 Touchpad rilevato come (touchpad elantech)](#Touchpad_rilevato_come_.28touchpad_elantech.29)
*   [5 Risorse esterne](#Risorse_esterne)

## Installazione

I driver Synaptic sono ora inclusi nel pacchetto [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics), e sono disponibili gli [Official repositories](/index.php/Official_repositories "Official repositories")

## Configurazione

Il metodo principale di configurazione del touchpad è attraverso un file di configurazione del server [Xorg](/index.php/Xorg "Xorg"). Dopo l'installazione di `xf86-input-synaptics`, viene creato un file di configurazione di base in `/etc/X11/xorg.conf.d/10-synaptics.conf`.

Gli utenti possono modificare questo file per configurare le diverse opzioni del driver disponibili, per una lista completa di tutte le variabili gli utenti dovrebbero rivolgersi alla pagina del manuale di synaptic:

 `$ man synaptics` 
**Nota:** Synaptics 1.0 e più recenti supportano la proprietà del dispositivo di input se il driver è avviato su server X 1.6 o più recente. Su queste versioni del driver, l'opzione "SHMConfig" non è necessaria per abilitare la configurazione in run-time. Si veda la pagina del manuale per maggiri informazioni.

### Opzioni usate di frequente

I driver Synaptic permettono di essere modificati in un vasto numero di opzioni. Si noti che tutte queste opzioni possono essere semplicemente aggiunte al file di configurazione principale in `/etc/X11/xorg.conf.d/10-synaptics.conf`, come è possibile notare in questo esempio di file di configurazione, dove si è abilitato lo scrolling verticale, orizzontale e circolare:

 `/etc/X11/xorg.conf.d/10-synaptics.conf` 
```
. 

 Section "InputClass"
       Identifier "touchpad"
       Driver "synaptics"
       MatchIsTouchpad "on"
              Option "TapButton1" "1"
              Option "TapButton2" "2"
              Option "TapButton3" "3"
              Option "VertEdgeScroll" "on"
              Option "VertTwoFingerScroll" "on"
              Option "HorizEdgeScroll" "on"
              Option "HorizTwoFingerScroll" "on"
              Option "CircularScrolling" "on"
              Option "CircScrollTrigger" "2"
              Option "EmulateTwoFingerMinZ" "40"
              Option "EmulateTwoFingerMinW" "8"
              Option "CoastingSpeed" "0"
              ...
 EndSection

```

	**TapButton1**

	(integer) determina quale tasto del mouse venga registrato evitando l'area dell'angolo del touchpad, tocco con un dito.

	**TapButton2**

	(integer) determina quale tasto del mouse venga registrato evitando l'area dell'angolo del touchpad, tocco con due dita.

	**TapButton3**

	(integer) determina quale tasto del mouse venga registrato evitando l'area dell'angolo del touchpad, tocco con tre dita

	**RBCornerButton**

	(integer) determina quale tasto del mouse venga registrato nell'angolo in basso a destra del touchpad, tocco con un dito (si usi `Option "RBCornerButton" "3"` per ottenere il comportamento del tasto destro del mouse nell'angolo più basso a destra del touchpad alla maniera di Ubuntu)

	**RTCornerButton**

	(integer) come sopra, ma per l'angolo in alto a destra, tocco con un dito.

	**VertEdgeScroll**

	(boolean) abilita lo scrolling verticale mentre si trascina il dito lungo il bordo destro del touchpad.

	**HorizEdgeScroll**

	(boolean) abilita lo scrolling orizzontale mentre si trascina il dito lungo il bordo basso del touchpad.

	**VertTwoFingerScroll**

	(boolean) abilita lo scrolling vertucale usando due dita.

	**HorizTwoFingerScroll**

	(boolean) abilita lo scrolling orizzontale usando due dita.

	**EmulateTwoFingerMinZ/W**

	(integer) giocare su questo valore per settare la precisione dello scroll con due dita.

[Un esempio](/index.php?title=Touchpad_Synaptics/10-synaptics.conf_example&action=edit&redlink=1 "Touchpad Synaptics/10-synaptics.conf example (page does not exist)") con una breve descrizione di tutte le opzioni. Come al solito le impostazioni variano a seconda della macchina. Si consiglia di scoprire le differenti opzioni utilizzando [synclient](/index.php/Touchpad_Synaptics#Synclient "Touchpad Synaptics").

**Nota:** Se accade che la propria mano sfiori spesso il touchpad, causando l'attivazione dell'opzione TapButton2 (che copierà più del dovuto dagli appunti), e non si vuole perdere la funzionalità del tocco a due dita, si imposti `TapButton2` a -1.

**Nota:** Le versioni recenti includono una funzione "Coasting", abilitata di default. Essa può causare l'effetto indesiderato di continuare lo scorrimento fino al tocco o al click seguente, anche nel caso in cui non si stia più toccando il touchpad. Ciò significa che per fare scrolling anche appena un po', si deve scorrere (usando l'angolo o un'opzione multitouch) e quindi quasi subito toccare il touchpad. In caso contrario lo scrolling continuerà all'infinito. Se si desidera evitare questo problema, impostare `CoastingSpeed` a 0.

### Altre opzioni

	**VertScrollDelta** e **HorizScrollDelta**

	(integer) configura la velocità di scrolling. È un po' poco intuitivo in quanto valori più alti producono una maggiore precisione e quindi uno scorrimento più lento. Valori negativi generano lo scorrimento naturale come in OS X.

	SHMConfig

	(booleano) Attiva/disattiva la memoria condivisa per il debug run-time. Questa opzione non ha più effetto sulla configurazione run-time ed è utile solo per il debug degli eventi hardware.

### GNOME

Gli utenti di [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)") dovrebbero modificare anche la configurazione di quest'ultimo, dato che, di base, blocca il tocco per cliccare, lo scrolling orizzontale e non permette di disabilitare il touchpad durante la battitura a tastiera.

Per cambiare queste impostazioni in **Gnome 2**:

1.  Si lanci `gconf-editor`
2.  modificare la chiave nella cartella `/desktop/gnome/peripherals/touchpad/`.

Per cambiare queste impostazioni in **Gnome 3**:

1.  Si apra *Impostazioni di Sistema*.
2.  Si selezioni *Mouse e Touchpad*.
3.  Si cambino le impostazioni nella scheda *Touchpad*.

Il demone delle impostazioni Gnome potrebbe sovrascrivere le impostazioni esistenti (ad esempio i settaggio in `xorg.conf.d`) per i quali non ci sono equivalenti in alcuna utilità grafica di configurazione). È possibile fare in modo che gnome non modifichi più le impostazioni mouse:

1.  Avviare `dconf-editor`
2.  Modificare `/org/gnome/settings-daemhttps://wiki.archlinux.org/index.php?title=Touchpad_Synaptics_(Italiano)&action=edit&section=3on/plugins/mouse/`
3.  Deselezionare l'impostazione **attivo**.

Ora sarà rispettata la configurazione esistente per synaptics.

### MATE

Come con [GNOME](/index.php/GNOME "GNOME"), è possibile configurare il modo in cui MATE gestisce il touchpad:

1.  Avviare `mateconf-editor`
2.  Modificare le chiavi nella cartella `desktop/mate/peripherals/touchpad/`.

Affinché il demone di configurazione di Mate non sovrascriva le configurazioni esistenti:

1.  Avviare `mateconf-editor`
2.  Modificare `/apps/mate_settings_daemon/plugins/mouse/`
3.  Sbloccare il settaggio **attivo**.

### Configurazioni al volo

Accanto al metodo tradizionale di configurazione, i driver Synaptic supportano anche la configurazione al volo. Ciò significa che gli utenti possono impostare alcune opzioni attraverso applicazioni software che vengono applicate immediatamente senza dover riavviare X. Questo è molto utile per testare le opzioni di configurazione prima di includerle nel file di configurazione.

**Nota:** L'opzione `SHMConfig` è stata rimossa da Synaptics. La configurazione attraverso `synclient` non è più necessaria.

**Attenzione:** Le configurazioni On-the-fly sono no permanenti e non rimarranno attive al riavvio del sistema, alla sospensione / riavvio o al riavvio di udev. Si dovrebbe usare tale utilità solo per finalità di testing, affinamento o configurazione di script.

#### Strumenti da console

*   **[Synclient](/index.php/Touchpad_Synaptics#Synclient "Touchpad Synaptics") (Raccomandato)** — utilità da riga di comando per configurare e ricercare impostazioni del driver Synaptics su un live system. Lo strumento è sviluppato da i manutentori dei driver synaptics ed è fornito con i driver stessi

	[http://xorg.freedesktop.org/](http://xorg.freedesktop.org/) || [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics)

*   **[xinput](/index.php/Touchpad_Synaptics#xinput "Touchpad Synaptics")** — un piccolo strumento con interfaccia da riga di comando (CLI) per configurare i dispositivi:

	[http://xorg.freedesktop.org/](http://xorg.freedesktop.org/) || [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput)

#### Strumenti grafici

*   **GPointing Device Settings** — fornisce una configurazione al volo grafica per numerosi device di puntamento connessi al sistema, incluso il proprio touchpad synaptic. Questa applicazione rimpiazza GSynaptics come lo strumento principale di configurazione grafica del touchpad attraverso i driver synaptic.

	[http://live.gnome.org/GPointingDeviceSettings](http://live.gnome.org/GPointingDeviceSettings) || [gpointing-device-settings](https://aur.archlinux.org/packages/gpointing-device-settings/)

**Note:** Affinché GPointingDeviceSettings funzioni con i touchpad Synaptics devono essere installati i pacchetti [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) e [libsynaptics](https://aur.archlinux.org/packages/libsynaptics/) !

*   **kcm-touchpad** — E' un recente strumento di configurazione per [KDE](/index.php/KDE "KDE") dalla versione 4.12+

	[https://projects.kde.org/projects/playground/utils/kcm-touchpad/repository](https://projects.kde.org/projects/playground/utils/kcm-touchpad/repository) || [kcm-touchpad](https://www.archlinux.org/packages/?name=kcm-touchpad).

Fornisce un modulo per le impostazioni di sistema. Rimpiazza gli ormai datati [synaptiks](https://aur.archlinux.org/packages/synaptiks/) e [kcm_touchpad](https://aur.archlinux.org/packages/kcm_touchpad/).

## Configurazione avanzata

### Usare xinput per determinare le funzionalità del touchpad

In base al modello, il touchpad synaptics può avere o meno queste caratteristiche. È possibile determinare quali siano supportate dal proprio hardware usando `xinput`:

*   pulsanti hardware sinistro, centrale e destro
*   individuazione di due dita
*   individuazione di tre dita
*   risoluzione configurabile

Prima di tutto, si trovi il nome del proprio touchpad:

 `$ xinput -list` 

Ora su può usare `xinput` per trovare le caratteristiche:

```
$ xinput list-props "SynPS/2 Synaptics TouchPad" | grep Capabilities

      Synaptics Capabillities (309):  1, 0, 1, 0, 0, 1, 1

```

Questi numeri mostrano, da sinistra a destra:

*   (1) il device ha un pulsante sinistro fisico
*   (0) il device non ha un pulsante centrale fisico
*   (1) il device ha un pulsante destro fisico
*   (0) il device non supporta l'individuazione two-finger
*   (0) il device non supporta l'individuazione three-finger
*   (1) il device può configurare la risoluzione verticale
*   (1) il device può configurare la risoluzione orizzontale

Usare `xinput list-props "SynPS/2 Synaptics TouchPad"` per elencare tutte le proprietà del touchpad.

### Synclient

Synclient può configurare ogni opzione a disposizione dell'utente, come documentato in `$ man synaptics`. Si può vedere una lista completa delle impostazioni correnti con:

 `$ synclient -l` 

Ogni opzione di configurazione elencata si può controllare tramite synclient, ad esempio:

```
$ synclient PalmDetect=1 (per abilitare la palm detection)
$ synclient TapButton1=1 (per configurare gli eventi del pulsante)
$ synclient TouchpadOff=1 (per disabilitare il touchpad)

```

Dopo che l'utente ha provato e testato con successo le proprie opzioni da synclient, può rendere i combiamenti permanenti aggiungendoli a `/etc/X11/xorg.conf.d/10-synaptics.conf`.

Il pannello di controllo synclient può mostrare la pressione e la posizione sul touchpad in tempo reale, permettendo la rifinitura delle impostazioni predefinite di Synaptics.

Si può avviare il monitor Synaptics con il seguente comando:

```
$ synclient -m 100

```

Dove l'opzione -m attiva il monitor e il numero seguente specifica l'intervallo di aggiornamento in millesimi di secondo.

Questo monitor fornisce informazioni sullo stato corrente del proprio touchpad. Ad esempio, se il mouse viene mosso attraverso il touchpad, i valori x e y del monitor cambieranno. Con questi dati si potrà facilmente risalire alle dimensioni del proprio touchpad che sono definite nelle opzioni LeftEdge-, RightEdge-, BottomEdge- e TopEdge.

Le abbreviazioni per i parametri sono le seguenti:

| +Abbreviation+ | +Description+ |
| **time** | Tempo in secondi da quando la registrazione è iniziata. |
| **x, y** | Le coordinate x/y del dito sul touchpad. L'origine è nell'angolo in alto a sinistra. |
| **z** | Il valore della pressione. Rappresenta la pressione che si sta usando per navigare sul proprio touchpad. |
| **f** | Numero di dita che stanno toccando il touchpad. |
| **w** | Valore che rappresenta la larghezza del dito. |
| **l,r,u,d,m,multi** | Questi valori rappresentano lo stato della pressione dei tasti sinistra, destra, su, giù, centro e multipli dove il valore zero indica che non vi è stata pressione, mentre uno che vi è stata pressione. |
| **gl,gm,gr** | Per i touchpad che hanno un device ospite, questi valori indicano lo stato dei tasti associati per il tasto ospite sinistro, centro e destro su cui vi è stata pressione (1) o meno (0). |
| **gdx, gdy** | Coordinate x/y per il device ospite. |

Se un valore rimane costante a zero, significa che quell'opzione non è supportata dal proprio device.

Ora si usi `synclient` per testare nuovi valori. Ad esempio, per regolare la velocità minima del puntatore:

```
$ synclient MinSpeed=0.5

```

Il cambiamento non sarà permanente, occorrerà mettere questi valori nel proprio file di configurazione (**/etc/X11/xorg.conf.d/10-synaptics.conf**) per renderli tali.

### Scrolling Circolare

Lo Scrolling Circolare è un'utilità offerta da Synaptics che ricorda da vicino il comportamento degli iPod. Al posto di (o oltre a) scorrere orizzontalmente o verticalmente, è possibile farlo circolarmente. Alcuni utenti lo trovano un sistema più veloce e preciso. Per abilitare lo Scrolling Circolare, si aggiungano le opzioni seguenti alla sezione device del touchpad in `/etc/X11/xorg.conf.d/10-synaptics.conf`:

 `/etc/X11/xorg.conf.d/10-synaptics.conf` 
```
 Section "InputClass"
         ...
         Option      "CircularScrolling"          "on"
         Option      "CircScrollTrigger"          "0"
         ...
 EndSection

```

L'opzione **CircScrollTrigger** può avere uno dei seguenti valori, atti a determinare da che da che bordo parte lo scrolling circolare:

```
0    Ogni bordo
1    Bordo superiore
2    Angolo in alto a destra
3    Bordo destro
4    Angolo in basso a destra
5    Bordo inferiore
6    Angolo in basso a sinistra
7    Bordo sinistro
8    Angolo in alto a sinistra

```

È utile specificare un valore diverso da zero se si desidera utilizzare lo scrolling circolare unitamente all'orizzontale e/o al verticale. Se lo si fa, il tipo di scrolling sarà determinato dal lato da cui si parte.

Per scorrere velocemente, disegnare piccoli cerchi nel centro del proprio touchpad. Per farlo lentamente e con maggior precisione, disegnare cerchi dall'ampio raggio.

### Scrolling Naturale

È possibile abilitare lo Scrolling Naturale attraverso Synaptics. Semplicemente si usino valori negativi per `VertScrollDelta` e `HorizScrollDelta` come segue:

 `/etc/X11/xorg.conf.d/10-synaptics.conf` 
```
Section "InputClass"
         ...
         Option      "VertScrollDelta"          "-111"
         Option      "HorizScrollDelta"         "-111"
         ...
EndSection

```

### Interruttore software

Si potrebbe trovare utile un interruttore software, che accenda o spenga il touchpad, specialmente nel caso in cui sia estremamente sensibile o l'utente digiti spesso. Attenzione: si guardi anche [#Disable touchpad upon external mouse detection](#Disable_touchpad_upon_external_mouse_detection) in quanto questa potrebbe essere la soluzione migliore (questione di gusti). Il vantaggio, in questo caso, è che l'utente ha il controllo della cosa, mentre l'altra soluzione utilizza un demone per determinare quando spegnere il touchpad.

Si potrebbe dover installare [xbindkeys](/index.php/Xbindkeys "Xbindkeys") nel caso in cui non si sia già dotati di un software che gestisca le combinazioni di tasti.

Quindi si salvi questo script in qualcosa come `/sbin/trackpad-toggle.sh`:

 `/sbin/trackpad-toggle.sh` 
```
 #!/bin/bash

 synclient TouchpadOff=$(synclient -l | grep -c 'TouchpadOff.*=.*0')

```

Infine, si aggiunga una combinazione di tasti che lo utilizzi. La cosa migliore è avviarlo con xbindkeys così, in(file `~/.xbindkeysrc`):

 `~/.xbindkeysrc` 
```
 "/sbin/trackpad-toggle.sh"
     m:0x5 + c:65
     Control+Shift + space

```

Ora, si (ri)avvii semplicemente `xbindkeys` e la pressione di `Ctrl`+`Shift`+`Space` avvierà/spegnerà il touchpad!

Ovviamente si può utilizzare il software di gestione delle combinazioni tasti che si desidera, come quelli previsti nel proprio DE/WM.

### Disabilitare il Trackpad durante la digitazione

#### Rilevamento automatico del palmo della mano

Prima di dutto si dovrebbe testare se funziona adeguatamente per il proprio trackpad a se le configurazioni sono accurate:

```
$ synclient PalmDetect=1

```

Quindi si provi a digitare. Si può modificare il rilevamento con:

```
$ synclient PalmMinWidth=

```

che è la larghezza dell'area che il proprio palmo di mano tocca, e

```
$ synclient PalmMinZ=

```

che è la minima distanza Z a cui il rilevamento è messo in atto.

Quando si sono trovati i settaggi adeguati, si salvino in `/etc/X11/xorg.conf.d/10-synaptics.conf` come segue:

```
#synclient PalmDetect=1
Option "PalmDetect" "1"
#synclient PalmMinWidth=10
Option "PalmMinWidth" "10"
#synclient PalmMinZ=200
Option "PalmMinZ" "200"
```

#### Usando .xinitrc

Affinché il touchpad sia disabilitato automaticamente durante la digitazione, si aggiunga la linea seguente al proprio `~/.xinitrc` prima di avviare il proprio window manager (se non si sta utilizzando un login manager):

 `$ syndaemon -t -k -i 2 -d &` 

	**-i 2**

	imposta il tempo idle a 2 secondi. Il tempo idle specifica quanti secondi aspettare dopo l'ultima pressione di un tasto prima di abilitare ancora il touchpad.

	**-t**

	istruisce il demone a non disabilitare il movimento del mouse finché è in corso la digitazione, ma soltanto di disabilitare il tapping e lo scrolling.

	**-k**

	istruisce il demone ad ignorare i pulsanti di modificazione finché è monitorato l'attività della tastiera (es.: permette Ctrl+Sx Click).

	**-d**

	avvia come demone in background.

Maggiori dettagli sono disponibili alla pagina del manuale:

 `$ man syndaemon` 

Se si sta utilizzando un login manager, sarà necessario specificare il comando laddove il proprio WM/DE permette di farlo.

#### Usando un Login Manager

L'opzione "-d" è necessaria per avviare syndaemon con un processo in background.

**Per GNOME: (GDM)**

Per avviare syndaemon è necessario usare il programma delle Preferenze delle Applicazioni di Avvio di Gnome. Effettuare il login a Gnome ed accedere a **Sistema > Preferenze > Applicazioni di Avvio**. Sulla tabella dei Programmi di avvio cliccare sul pulsante **Aggiungi**. Si dia il nome che si preferisce al programma di avvio e si inseriscano i commenti che si ritengono opportuni (o si lasci il campo vuoto). Sullo spazio per il comando aggiungere:

 `$ syndaemon -t -k -i 2 -d &` 
```
In Gnome 3 avviare gnome-session-properties per accedere alla applicazioni di avvio. 

```

Una volta fatto, cliccare su **Aggiungi** nella finestra di dialogo **Aggiungi programma di avvio**. Assicurarsi di spuntare la casella accanto al programma di avvio creato nella lista dei programmi di avvio aggiuntivi. Chiudere la finestra delle **Preferenze delle applicazioni di avvio**.

**For KDE: (KDM)**

Andare in **Opzioni di Sistema > Avvio e Spegnimento > Autostart**, cliccare su **Aggiungi programma**, inserire:

 ` syndaemon -t -k -i 2 -d &` 

Quindi spuntare **Avvia sul terminale**.

## Risoluzione problemi

### xorg.conf.d/10-synaptics.conf sembra non essere applicato in GNOME e MATE

[GNOME](/index.php/GNOME "GNOME") e [MATE](/index.php/MATE "MATE"), come opzione predefinita, sovrascrive varie opzioni per il proprio touchpad. Questo inclide opzioni configurabili per cui non c'è possibilità di configurazione grafica del pannello di controllo di GNOME. Ciò potrebbe far sembrare che `/etc/X11/xorg.conf.d/10-syanaptics.conf` non sia applicato. Si faccia riferimento alla sezione GNOME di questo articolo per prevenire questo comportamento.

*   [Touchpad Synaptics#GNOME](/index.php/Touchpad_Synaptics#GNOME "Touchpad Synaptics")

#### ALPS Touchpads

**Attenzione:** è necessario riscriverlo per udev

Per i touchpad ALPS, nel caso in cui le configurazioni sopra indicate non dessero i risultati desiderati, si provi invece ad utilizzare la seguente configurazione:

 `/etc/X11/xorg.conf.d/10-synaptics.conf` 
```
  Section "ServerLayout"
    ...
    InputDevice    "USB Mouse" "CorePointer"
    InputDevice    "Touchpad"  "SendCoreEvents"
  EndSection

  Section "InputDevice"
        Identifier  "Touchpad"
    Driver  "synaptics"
    Option  "Device"   "/dev/input/mouse0"
    Option  "Protocol"   "auto-dev"
    Option  "LeftEdge"   "130"
    Option  "RightEdge"   "840"
    Option  "TopEdge"   "130"
    Option  "BottomEdge"   "640"
    Option  "FingerLow"   "7"
    Option  "FingerHigh"   "8"
    Option  "MaxTapTime"   "180"
    Option  "MaxTapMove"   "110"
    Option  "EmulateMidButtonTime"   "75"
    Option  "VertScrollDelta"   "20"
    Option  "HorizScrollDelta"   "20"
    Option  "MinSpeed"   "0.25"
    Option  "MaxSpeed"   "0.50"
    Option  "AccelFactor"   "0.010"
    Option  "EdgeMotionMinSpeed"   "200"
    Option  "EdgeMotionMaxSpeed"   "200"
    Option  "UpDownScrolling"   "1"
    Option  "CircularScrolling"   "1"
    Option  "CircScrollDelta"   "0.1"
    Option  "CircScrollTrigger"   "2"
    Option  "SHMConfig"   "on"
    Option  "Emulate3Buttons"   "on"
  EndSection

```

### Il touchpad non funziona, Xorg.0.log presenta "Query no Synaptics: 6003C8"

A causa del modo in cui synaptic è impostato al momento, vengono caricate due istanze del modulo synaptics. Si può riconoscere questa situazione aprendo il file di log di xorg (`/var/log/Xorg.0.log`) e notando questo:

 `/var/log/Xorg.0.log` 
```
 [ 9304.803] (**) SynPS/2 Synaptics TouchPad: Applying InputClass "evdev touchpad catchall"
 [ 9304.803] (**) SynPS/2 Synaptics TouchPad: Applying InputClass "touchpad catchall"

```

Da notare come due istanze dal nome diverso vengano caricate. In alcuni casi questa è la causa del perché il touchpad diventi inutilizzabile.

Si può prevenire il doppio caricamento editando il proprio file `/etc/X11/xorg.conf.d/10-synaptics.conf`. Si dovrebbe aggiungere `MatchDevicePath "/dev/input/event*"`

 `/etc/X11/xorg.conf.d/10-synaptics.conf` 
```
 Section "InputClass"
       Identifier "touchpad catchall"
       Driver "synaptics"
       MatchIsTouchpad "on"
       MatchDevicePath "/dev/input/event*"
             Option "TapButton1" "1"
             Option "TapButton2" "2"
             Option "TapButton3" "3"
 EndSection 

```

Si riavvii X e si ricontrolli i log di xorg, l'errore dovrebbe essere sparito e il touchpad dovrebbe funzionare correttamente.

Bugreport relativo: [FS#20830](https://bugs.archlinux.org/task/20830)

Topic relativi nel forum:

*   [https://bbs.archlinux.org/viewtopic.php?id=104769](https://bbs.archlinux.org/viewtopic.php?id=104769)
*   [https://bbs.archlinux.org/viewtopic.php?pid=825690](https://bbs.archlinux.org/viewtopic.php?pid=825690)

### Touchpad rilevato come "PS/2 Generic Mouse" o "Logitech PS/2 mouse"

Ciò è causato da un [bug del kernel](https://bugzilla.kernel.org/show_bug.cgi?id=27442), corretto a partire dal kernel 3.3\. I touchpad rilevati scorrettamente non si possono configurare con il Synaptic input driver. Per correggere questo errore, si può installare pacchetto [AUR](/index.php/AUR "AUR") [psmouse-alps-driver](https://aur.archlinux.org/packages/psmouse-alps-driver/).

Tra i notebook colpiti ci sono i seguenti modelli:

*   Acer Aspire 7750G
*   Dell Latitude E6230, E6520, E6430 e E6530 (ALPS DualPoint TouchPad), Inspiron N5110 (ALPS GlidePoint), Inspiron 14R Turbo SE7420/SE7520 (ALPS GlidePoint)
*   Samsung NC110/NF210/QX310/QX410/QX510/SF310/SF410/SF510/RF410/RF510/RF710/RV515

Si può verificare se il proprio touchpad è correttamente rilevato con:

 `$ xinput list` 

Per maggiori informazioni si veda [questo thread](https://bbs.archlinux.org/viewtopic.php?id=117109).

### Abilità speciali di Synaptics non-funzionanti (multi-tocco, scrolling, ecc.)

In alcuni casi i touchpad Synaptics funzionano solo parzialmente. Caratteristiche come lo scrolling a due dita o il click centrale con due dita non funzionano persino se configurate correttamente. Ciò è probabilmente dovuto al problema [Il touchpad non funziona](#Il_touchpad_non_funziona.2C_Xorg.0.log_presenta_.22Query_no_Synaptics:_6003C8.22) su menzionato. Si risolva alla stessa maniera evitando il caricamento del doppio modulo.

Se impedire che il modulo parta due volte non risolve il problema, provare a commentare l'opzione "MatchIsTouchpad" (che ora è inclusa di default nel file di configurazione di synaptics).

### Disabilitare il touchpad non appena venga rilevato un mouse esterno

Con l'aiuto di [udev](/index.php/Udev_(Italiano) "Udev (Italiano)"), è possibile disabilitare automaticamente il touchpad nel caso in cui venga inserito un mouse esterno. Per realizzare ciò si aggiunga la seguente regola udev a `/etc/udev/rules.d/01-touchpad.rules`:

 `/etc/udev/rules.d/01-touchpad.rules` 
```
 ACTION=="add", SUBSYSTEM=="input", KERNEL=="mouse[0-9]", ENV{DISPLAY}=":0", ENV{XAUTHORITY}="/home/<your username>/.Xauthority", ENV{ID_CLASS}="mouse", ENV{REMOVE_CMD}="/usr/bin/synclient TouchpadOff=0", RUN+="/usr/bin/synclient TouchpadOff=1" 

```

GDM conserva i file Xauthority in `/var/run/gdm` in una cartella nominata a caso. Per qualche ragione anche i file multipli di authority potrebbero apparire anche per il singolo utente. Quindi sono necessarie regole udev come queste:

```
ACTION=="add", KERNEL=="mouse[0-9]", SUBSYSTEM=="input", PROGRAM="/usr/bin/find /var/run/gdm -name *username* -print -quit", ENV{DISPLAY}=":0.0",
ENV{XAUTHORITY}="$result/database", RUN+="/usr/bin/synclient TouchpadOff=1"
ACTION=="remove", KERNEL=="mouse[0-9]", SUBSYSTEM=="input", PROGRAM="/usr/bin/find /var/run/gdm -name *username* -print -quit", ENV{DISPLAY}=":0.0",
ENV{XAUTHORITY}="$result/database", RUN+="/usr/bin/synclient TouchpadOff=0"

```

**Nota:** le regole di [udev](/index.php/Udev "Udev") devono essere ognuna di una singola riga, per accordarsi al formato.

**Nota:** Queste regole [udev](/index.php/Udev "Udev") vanno in conflitto con syndaemon (si veda [#Usando .xinitrc](#Usando_.xinitrc))

Per disabilitare il touchpad e mandare segnale kill a syndaemon, si può usare una regola come questa:

```
ACTION=="add", KERNEL=="mouse[0-9]", SUBSYSTEM=="input", PROGRAM="/usr/bin/find /var/run/gdm -name *username* -print -quit", ENV{DISPLAY}=":0.0",ENV{XAUTHORITY}="$result/database", RUN+="/bin/sh -c '/usr/bin/synclient TouchpadOff=1 ; sleep 1; /bin/killall syndaemon; '"

```

Se syndaemon si avvia automaticamente alla rimozione del mouse è possibile combinare questa regola a quella di rimozione precedente. Qualora fosse necessario avviare syndaemon, modificare il comando, accordandolo alle proprie opzioni di syndaemon preferite.

### Il cursore salta

Alcuni utenti denunciano un cursore che inspiegabilmente "salta" per tutto lo schermo. Al momento non c'è una patch per questo problema, ma gli sviluppatori sono informati sul problema e ci stanno lavorando.

Un'altra possibilità è che si stiano avendo *IRQ losses* correlate al controller i8042 (questo dispositivo gestisce la tastiera e il touchpad di molti portatili). In questo caso ci sono due possibilità:

1\. rmmod && insmod il modulo psmouse. 2\. instrire i8042.nomux=1 alla riga di boot e riavviare la propria macchina.

### Multitouch

Gesti multitouch come in Mac OS X saranno implementati con versioni future del driver.

### Il dispositivo touchpad non si trova in `/dev/input/*`

Se questo problema si presenta, si può utilizzare questo comando per mostrare le informazioni riguardo il proprio dispositivo di input:

 `$ cat /proc/bus/input/devices` 

Si cerchi quindi un dispositivo di input col nome "SynPS/2 Synaptics TouchPad". La sezione "Handlers" dell'output mostra il nome del device che occorre specificare.

**Esempio d'output:**

 `$ cat /proc/bus/input/devices` 
```
 I: Bus=0011 Vendor=0002 Product=0007 Version=0000
 N: Name="SynPS/2 Synaptics TouchPad"
 P: Phys=isa0060/serio4/input0
 S: Sysfs=/class/input/input1
 H: Handlers=mouse0 event1
 B: EV=b
 B: KEY=6420 0 7000f 0

```

In questo caso, gli `Handlers` sono `mouse0` e `event1`, quindi si dovrà usare `/dev/input/mouse0`.

### Firefox e azioni speciali per il touchpad

Di base, Firefox è impostato per compiere azioni speciali durante lo scrolling o il tocco di alcune zone del touchpad. Si possono editare le impostazioni di queste azioni digitando **about:config** nella barra degli indirizzi di Firefox. Per cambiare queste opzioni, si clicchi due volte sulla linea in questione, cambiando la dicitura da "true" a "false" e vicecersa.

Per evitare che Firefox effettui lo scorrimento (indietro/avanti) attraverso la cronologia invece di effettuare lo scorrimento tra le pagine, si editi queste opzioni come indicato:

```
mousewheel.horizscroll.withnokey.action = 1
mousewheel.horizscroll.withnokey.sysnumlines = true

```

Per evitare che Firefox effettui il reindirizzamento all'URL indicato dai contenuti degli appunti tramite il tocco dell'area in alto a destra del touchpad (o il tasto centrale del mouse), si imposti a "false" la seguente opzione:

```
middlemouse.contentLoadURL = false

```

### Opera: problemi di scorrimento orizzontale

Come sopra. Per risolvere si vada in Impostazioni -> Preferenze -> Avanzate -> Scorciatoie. Si selezionino le impostazioni del mouse "Opera Standard" e si selezioni "Edit". Nella sezione "Applicazioni":

*   assign key "Button 6" to command "Scroll left"
*   assign key "Button 7" to command "Scroll right"

### Scorrimento e azioni multiple con Synaptics sui portatili LG

Questi problemi sembrano accadere su molti modelli di portatile LG. I sintomi includono: quando si preme il tasto del mouse 1, Synaptics lo interpreta come uno ScrollUP e un normale click del tasto 1; lo stesso accade per il tasto 2.

Il problema dello scorrimento può essere risolto inserendo nel xorg.conf:

 `/etc/X11/xorg.conf.d/xorg.conf`  `Option "UpDownScrolling" "0"` 

NOTARE che questo farà sì che Synaptic interpreti la pressione di un tasto come tre pressioni. C'è una patch scritta da Oskar Sandberg[[1]](http://www.math.chalmers.se/~ossa/linux/lg_tx_express.html) che rimuove questi click.

Apparentemente, quando si tenta di compilare questa soluzione all'ultima versione di Synaptic, questa fallisce. La soluzione è di usare il repository GIT per Synaptics[[2]](http://web.telia.com/~u89404340/touchpad/synaptics/.git) .

Si trova anche un pacchetto in AUR per automatizzare il tutto: [xf86-input-synaptics-lg](https://aur.archlinux.org/packages/xf86-input-synaptics-lg/).

Per costruire il pacchetto dopo aver scaricato il tarball e averlo decompresso, si esegua:

 `$ cd synaptics-git`  `$ makepkg` 

### Altri problemi con mouse esterni

Innanzitutto, assicurarsi che la sezione di descrizione del mouse esterno contenga questa linea (o quella che ci assomiglia):

 `/etc/X11/xorg.conf.d/xorg.conf`  `Option     "Device" "/dev/input/mice"` 

Se la linea "Device" è differente, la si cambi con quella sopra indicata e si provi a riavviare X. Se ciò non dovesse risolvere il problema, si imposti **touchpad** come CorePointer nella sezione "Server Layout":

 `/etc/X11/xorg.conf.d/xorg.conf`  `InputDevice    "Touchpad" "CorePointer"` 

e impostare il device esterno come "SendCoreEvents":

 `/etc/X11/xorg.conf.d/xorg.conf`  `InputDevice    "USB Mouse" "SendCoreEvents"` 

alla fine si aggiunga questa linea alla sezione del device esterno:

 `/etc/X11/xorg.conf.d/xorg.conf`  `Option      "SendCoreEvents"    "true"` 

Se tutto quello indicato non dovesse funzionare, per favore si controlli la sezione di bug rilevanti per un possibile bug, o si cerchi tra i post dei forum se qualcuno ha trovato una soluzione migliore.

### Problemi di sincronizzazione del Touchpad

A volte il cursore potrebbe congelarsi per alcuni secondi o iniziare ad agire da solo senza apparente motivo. Questi comportamenti vengono registrati in `/var/log/messages.log`

 `/var/log/messages.log`  `psmouse.c: TouchPad at isa0060/serio1/input0 lost synchronization, throwing 3 bytes away` 

Questo problema non ha una soluzione unica, ma ce ne sono diverse.

*   Se si usa scalare la frequenza della CPU, si eviti di utilizzare il governatore "ondemand" e si usi quello "performance" quando possibile, dal momento che il touchpad potrebbe perdere la sincronizzazione nei momenti di cambio della frequenza della CPU.
*   Si eviti di usare un monitor di batteria ACPI.
*   Si provi a caricare psmouse con l'opzione "proto=imps". Per farlo, si aggiunga questa linea al proprio `/etc/modprobe.d/modprobe.conf`:

 `/etc/modprobe.d/modprobe.conf`  `options psmouse proto=imps` 

*   Si provi con un altro ambiente desktop. Alcuni utenti dichiarano che questo problema accade solamente quando usano XFCE o GNOME, per qualche strano motivo.

### Ritardo tra la pressione sul pulsante e il click effettivo

Se si percepisce un ritardo tra la pressione sul touchpad e il click effettivo che viene registrato occorre abilitare FastTaps:

per farlo occorre aggiungere **Option "FastTaps" "1"** a `/etc/X11/xorg.conf.d/10-synaptics.conf` in modo tale da avere:

 `/etc/X11/xorg.conf.d/10-synaptics.conf` 
```
 Section "InputClass"
      Identifier "Synaptics Touchpad"
      Driver "synaptics"
      ...
      Option "FastTaps" "1"
      ...
 EndSection

```

### SynPS/2 Synaptics TouchPad can't grab event device, errno=16

Se si sta utilizzando Xorg 7.4 si dovrebbe ottenere un warning come questo da `/var/log/Xorg.0.log`, ciò è dovuto al fatto che il driver registra l'evento del device per un uso esclusivo quando si utilizza il protocollo eventi di Linux 2.6\. Quando ciò fallisce, X risponde con questo messaggio d'errore.

Registrare l'evento del device significa che nessun programma né da parte dell'user né da parte del kernel possa vedere l'evento del touchpad. Questo è desiderabile se il file di configurazione di X contiene `/dev/input/mice` come un device di input, ma potrebbe non essere desiderato nel caso in cui si voglia monitorare il device da utente.

Se lo si vuole controllare, si aggiunga o si modifichi l'opzione "GrabEventDevice" nella sezione touchpad in `/etc/X11/xorg.conf.d/10-synaptics.conf`:

 `/etc/X11/xorg.conf.d/10-synaptics.conf` 
```
 ...
 Option "GrabEventDevice" "''boolean''"
 ...

```

Ciò sarà preso in considerazione nel momento in cui X verrà riavviato, sebbene si possa cambiarlo usando synclient. Quando si cambia questo parametro col programma di synclient, il cambiamento non avrà effetto finché non si riavvierà il driver di Synaptics. Ciò lo si può fare passando alla console di testo e quindi tornando a X.

### Synaptics perde il Rilevamento del Multitocco dopo aver effettuato il Reboot da Windows

Molti driver contengono un firmware che viene caricato nella memoria flash quando il computer viene avviato. Questo firmware non viene necessariamente ripulito durante il processo di spegnimento, e spesso non è compatibile con i driver Linux. L'unico modo per pulire la memoria flash è spegnere il computer completamente piuttosto che usare il reboot. È considerata generalmente buona pratica quella di non usare il reboot per passare da un sistema operativo ad un altro.

### Touchpad senza pulsanti (o ClickPad)

Alcuni portatili sono dotati di un tipo speciale di touchpad che ha i pulsanti del mouse integrati alla piastra di rilevamento, anziché averli esterni. Per esempio HP series 4500 ProBooks, ThinkPad X220 e le serie X1 di ThinkPad hanno questo tipo di touchpad. Di default l'intera zona tasto è rilevato come un pulsante sinistro, con il risultato che il secondo è di fatto inutilizzabile e che il trascinamento non funziona. In precedenza, il supporto per questo tipo di dispositivi era gestito usando patch di parti terze, ma dalla versione 1.6.0 i driver synaptics possiedono il supporto multitouch nativo (usando la libreria *mtdev*).

Per abilitare altri pulsanti modificare la sezione touchpad in `/etc/X11/xorg.conf.d/10-synaptics.conf` (o, meglio, del proprio file di configurazione personalizzato preceduto da un prefisso più alto di 10):

 `/etc/X11/xorg.conf.d/10-synaptics.conf` 
```
...
Option "ClickPad"         "true"
Option "EmulateMidButtonTime" "0"
Option "SoftButtonAreas"  "50% 0 82% 0 0 0 0 0"
...

```

Queste tre opzioni sono fondamentali: la prima abilita il supporto multitouch, la seconda disabilita l'emulazione del pulsante centrale (non supportata per i ClickPad) e la terza va a definire le aree pulsante.

Il formato per l'opzione SoftButtonAreas è (fa [synaptics(4)](http://jlk.fjfi.cvut.cz/arch/manpages/man/synaptics.4)):

 `RightButtonAreaLeft RightButtonAreaRight RightButtonAreaTop RightButtonAreaBottom  MiddleButtonAreaLeft MiddleButtonAreaRight MiddleButtonAreaTop MiddleButtonAreaBottom` 

L'esempio di cui sopra si trova comunemente nella documentazione o nei pacchetti synaptics e imposta come pulsante destro il 18% della metà destra della parte bassa del touchpad. È abilitato poi **nessun pulsante centrale**. Se si desidera definire un pulsante centrale, si ricordi una parte fondamentale delle informazioni dal manuale: l'angolo impostato a 0 si estende all'infinito in quella direzione.

Nell'esempio seguente, il pulsante destro occupa il 40% della parte più a destra dell'area pulsante. Ora si procederà ad impostare il pulsante centrale in modo che occupi il 20% del touchpad in una piccola area al centro.

```
   ...
   Option     "SoftButtonAreas"  "60% 0 82% 0 40% 59% 82% 0"
   ...

```

Si può usare `synclient` per controllare le nuove aree dei pulsanti touch:

```
   $ synclient -l | grep -i ButtonArea
       RightButtonAreaLeft     = 3914
       RightButtonAreaRight    = 0
       RightButtonAreaTop      = 3918
       RightButtonAreaBottom   = 0
       MiddleButtonAreaLeft    = 3100
       MiddleButtonAreaRight   = 3873
       MiddleButtonAreaTop     = 3918
       MiddleButtonAreaBottom  = 0

```

Se i propri pulsanti non funzionano, le zone dei pulsanti touch non stanno cambiando. Assicurarsi di non avere un file di configurazione synaptics distribuito da qualche pacchetto che stia sovrascrivendo le proprie impostazioni personalizzate (es. alcuni pacchetti AUR distrubuiscono configurazioni con un prefisso molto alto).

### Touchpad rilevato come (touchpad elantech)

Un problema del genere può capitare ad alcuni portatili con touchpad elantech, ad esempio ASUS x53s. In questa situazione è necessario il pacchetto da [AUR](/index.php/AUR "AUR") [psmouse-elantech](https://aur.archlinux.org/packages/psmouse-elantech/).

## Risorse esterne

Synaptics TouchPad driver: [[3]](http://cgit.freedesktop.org/xorg/driver/xf86-input-synaptics/)