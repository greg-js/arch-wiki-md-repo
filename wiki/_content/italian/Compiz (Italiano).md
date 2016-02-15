Compiz è un [gestore di finestre composito](http://it.wikipedia.org/wiki/Compositing_window_manager). Fornisce il suo proprio gestore di finestre [Emerald](/index.php/Emerald "Emerald"), quindi non può essere utilizzato insieme ad altri programmi dello stesso tipo come [Openbox](/index.php/Openbox_(Italiano) "Openbox (Italiano)"), [Fluxbox](/index.php/Fluxbox_(Italiano) "Fluxbox (Italiano)"), [Enlightenment](/index.php/Enlightenment_(Italiano) "Enlightenment (Italiano)"). Gli utenti che vogliono mantenere i propri gestori di finestre potrebbero vole provare [Xcompmgr](/index.php/Xcompmgr "Xcompmgr").

Compiz è il cuore del progetto Compiz-Fusion, il quale aveva l'obiettivo di aggiungere funzionalità e plugin al WM e che da un po' di tempo è stato riassorbito dal progetto Compiz originale. Entrambi i progetti sono attivi e in costante sviluppo. Per maggiori informazioni, riferirsi all'articolo (in inglese) [Compiz Fusion vs. Compiz](http://wiki.compiz-fusion.org/CompizFusionVsCompiz).

## Contents

*   [1 Requisiti](#Requisiti)
*   [2 Installazione](#Installazione)
    *   [2.1 Configurazione iniziale](#Configurazione_iniziale)
*   [3 Software aggiuntivo](#Software_aggiuntivo)
    *   [3.1 Decoratori](#Decoratori)
    *   [3.2 Altro](#Altro)
*   [4 Avviare Compiz Fusion](#Avviare_Compiz_Fusion)
    *   [4.1 Avvio manuale (con "fusion-icon")](#Avvio_manuale_.28con_.22fusion-icon.22.29)
    *   [4.2 Avvio Manuale (senza "fusion-icon")](#Avvio_Manuale_.28senza_.22fusion-icon.22.29)
    *   [4.3 KDE](#KDE)
        *   [4.3.1 Utilizzando Impostazioni di sistema(semplice)](#Utilizzando_Impostazioni_di_sistema.28semplice.29)
        *   [4.3.2 Autostart (con "fusion-icon")](#Autostart_.28con_.22fusion-icon.22.29)
        *   [4.3.3 Autostart (senza "fusion-icon")](#Autostart_.28senza_.22fusion-icon.22.29)
        *   [4.3.4 Esportazione della variabile KDEWM (Metodo Ottimale)](#Esportazione_della_variabile_KDEWM_.28Metodo_Ottimale.29)
    *   [4.4 GNOME](#GNOME)
        *   [4.4.1 Autostart (senza "fusion-icon") (Metodo Ottimale)](#Autostart_.28senza_.22fusion-icon.22.29_.28Metodo_Ottimale.29)
        *   [4.4.2 Autostart (senza "fusion-icon", Gnome <= 2.24)](#Autostart_.28senza_.22fusion-icon.22.2C_Gnome_.3C.3D_2.24.29)
        *   [4.4.3 Autostart (con "fusion-icon")](#Autostart_.28con_.22fusion-icon.22.29_2)
    *   [4.5 XFCE](#XFCE)
        *   [4.5.1 Autostart in XFCE (senza "fusion-icon")](#Autostart_in_XFCE_.28senza_.22fusion-icon.22.29)
        *   [4.5.2 Autostart in XFCE (con "fusion-icon")](#Autostart_in_XFCE_.28con_.22fusion-icon.22.29)
        *   [4.5.3 Metodo 1:](#Metodo_1:)
        *   [4.5.4 Metodo 2:](#Metodo_2:)
        *   [4.5.5 Metodo 3:](#Metodo_3:)
    *   [4.6 Compiz come gestore di finestre autonomo](#Compiz_come_gestore_di_finestre_autonomo)
        *   [4.6.1 Aggiungere un menu radice](#Aggiungere_un_menu_radice)
*   [5 Varie](#Varie)
    *   [5.1 Impostate i plugin di base se volete usare Compiz!!](#Impostate_i_plugin_di_base_se_volete_usare_Compiz.21.21)
    *   [5.2 Usare Compiz-Manager](#Usare_Compiz-Manager)
    *   [5.3 Usare gtk-window-decorator](#Usare_gtk-window-decorator)
    *   [5.4 gconf: Configurazioni aggiuntive per Compiz](#gconf:_Configurazioni_aggiuntive_per_Compiz)
    *   [5.5 Scorciatoie da tastiera](#Scorciatoie_da_tastiera)
    *   [5.6 Note per ATI R600/R700](#Note_per_ATI_R600.2FR700)
*   [6 Risorse Aggiuntive](#Risorse_Aggiuntive)

## Requisiti

Gli utenti dei più diffusi [DE](/index.php/Desktop_Environment_(Italiano) "Desktop Environment (Italiano)") possono utilizzare [compiz-manager](https://aur.archlinux.org/packages/compiz-manager/), che permette di effettuare un breve controllo dei requisiti ed eventualmente ripristinare un window manager alternativo.

## Installazione

É necessario installare i seguenti [pacchetti](https://aur.archlinux.org/packages.php?K=compiz), disponibili in [AUR](/index.php/AUR "AUR") (pacchetti più aggiornati: [compiz-bzr](https://aur.archlinux.org/packages/compiz-bzr/)).

Gli utenti che vogliono selezionare i pacchetti individualmente possono iniziare con [compiz-core](https://aur.archlinux.org/packages/compiz-core/) e un decorator.

**Nota:** Un decoratore di finestre non configurato può rendere lo spazio di lavoro [X](/index.php/Xorg_(Italiano) "Xorg (Italiano)") inutilizzabile.

### Configurazione iniziale

Mentre l' aspetto delle finestre e il loro contenuto dipende da [GTK+](/index.php/GTK%2B_(Italiano) "GTK+ (Italiano)") o [Qt](/index.php/Qt "Qt"), i frame attorno alle finestre sono controllati dal plugin di decorazione delle finestre. Per utilizzarlo assicurarsi di aver installato un decoratore di finestre. In base al pacchetto scaricato è possibile scegliere tra diversi decoratori. I più comuni sono Emerald, kde-window-decorator e gtk-window-decorator. Emerald ha il vantaggio di adattarsi meglio alla gestione dello schermo di Compiz e offre effetti di trasparenza. Per impostare il decoratore di default inserire il seguente comando nella sezione "Windows Decorations" delle impostazioni del plugin sotto il campo "Command".

Assicurarsi che il plugin "Window decorator" sia abilitato nella scheda "effects" di ccsm. Per poter avviare un decorator è necessario riempire il campo "Command".

Per impostare **emerald** come decoratore di default inserire:

```
$ emerald --replace

```

Per impostare **kde-window-decorator** come alternativa ad emerald inserire:

```
kde4-window-decorator --replace

```

Per impostare **compiz-decorator-gtk** come alternativa ad emerald inserire:

```
$ gtk-window-decorator --replace

```

**Note:** **Attivare plugin importanti:** spesso è necessario attivare alcuni plugin che forniscono un comportamento base del gestore di finestre altrimenti non sarà possibile trascinare, ridimensionare o chiudere le finestre con Compiz attivo. Alcuni di questi plugin sono "Window Decoration" sotto Effects e "Move Window" & "Resize Window" sotto Window Management. Il comando _ccsm_ può essere usato per attivare queste funzionalità. Basta inserire la spunta sui plugin che si desidera attivare.

## Software aggiuntivo

### Decoratori

*   **[Emerald](/index.php/Emerald "Emerald")** — Il decoratore di finestre di Compiz, con poche dipendenze. (Nota: Funziona ma presenta dei bug e non è più sviluppato)

	[http://www.compiz.org](http://www.compiz.org) || [emerald](https://aur.archlinux.org/packages/emerald/)

*   **compiz-decorator-gtk, compiz-decorator-kde** — Alternative a Emerald, che permettono di usare la configurazione e l' aspetto del proprio ambiente desktop.

	[http://www.compiz.org](http://www.compiz.org) || [compiz-bzr](https://aur.archlinux.org/packages/compiz-bzr/).

### Altro

*   [ccsm](https://aur.archlinux.org/packages/ccsm/) (gestore delle impostazioni CompizConfig) - Applicazione con interfaccia grafica che permette di configurare tutti i plugin di Compiz.
*   [fusion-icon](https://aur.archlinux.org/packages/fusion-icon/) - Tray icon che permette di avviare facilmente compiz, ccsm e cambiare il WM / Window Decorator

**Note:** _fusion-icon_ non funziona a causa di un bug introdotto con _glib2_ 2.36.1 ([FS#34892](https://bugs.archlinux.org/task/34892)), ed è stato rimosso dai repository. Se si vuole utilizzare comunque _fusion-icon_, bisogna installare [fusion-icon-fixed](https://aur.archlinux.org/packages/fusion-icon-fixed/) dall' [AUR](/index.php/AUR "AUR").

## Avviare Compiz Fusion

### Avvio manuale (con "fusion-icon")

Avviate la tray icon di Compiz:

```
 $ fusion-icon

```

Se si presentano errori relativi ai permessi, visitare [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting").

Cliccando poi col destro sull'icona nel pannello, nella voce "select window manager", selezionare poi "compiz" nel caso non fosse già selezionato, e a questo punto lo stesso dovrebbe partire.

Se tutto ciò fallisce, si può avviare compiz-fusion anche usando uno dei seguenti comandi alternativi:

```
 $ emerald --replace

```

oppure

```
 $ compiz-manager

```

**Ricordate:** se volete usare compiz assicuratevi prima di averlo configurato tramite il pannello, attivando plugin fondamentalil quali "Decorazione Finestre" e "Muovi Finestre" altrimenti il tutto sarà abbastanza inutilizzabile.

### Avvio Manuale (senza "fusion-icon")

Avviate Compiz con il seguente comando (ciò sostituirà il window manager in esecuzione):

```
$ compiz --replace ccp &

```

Alcuni utili parametri da riga di comando:

*   `--indirect-rendering`: utilizza indirect-rendering (AIGLX)
*   `--loose-binding`: può risolvere problemi grafici (NVIDIA?)
*   `--replace`: rimpiazza l' attuale window-manager
*   `--keep-window-hints`: mantiene gconf-settings del window-manager di gnome per i viewport disponibili ...
*   `--sm-disable`: disabilita il session-management
*   `ccp`: il comando "ccp" carica l' utlima configurazione usata da ccsm (CompizConfig Settings Manager) altrimenti Compiz verrà caricato senza nessuna configurazione salvata e non si potrà ineragire con le finestre.

### KDE

#### Utilizzando Impostazioni di sistema(semplice)

Andare su _Impostazioni di sistema > Applicazioni predefinite > Gestore Finestre > Utilizza un gestore finestre differente_.

Se avete bisogno di avviare compiz con delle impostazioni personalizzate selezionare "Compiz custom" ( quando avviate `fusion-icon` da terminale è possibile vedere la riga di comando da cui è stato avviato. Bisogna creare un file chiamato "compiz-kde-launcher" in `/usr/local/bin`, e rendere il file eseguibile: `chmod +x /usr/bin/compiz-kde-launcher`.

Ad esempio:

 `/usr/local/bin/compiz-kde-launcher` 

```
#!/bin/bash
LIBGL_ALWAYS_INDIRECT=1
compiz --replace ccp &
wait

```

#### Autostart (con "fusion-icon")

Aggiungete un link simbolico, che punta all'eseguibile di fusion-icon, nella vostra cartella Autostart di KDE (solitamente si trova in `~/.kde/Autostart`):

```
$ ln -s /usr/bin/fusion-icon ~/.kde/Autostart/fusion-icon

```

Al prossimo avvio di KDE, fusion-icon (e quindi compiz) verrà caricato automaticamente.

**Nota:** Questo metodo può essere un po' lento poichè KDE deve caricare prima il suo window-manager (Kwin), per poi sostituirlo con Compiz lanciato da fusion-icon. Quindi, impiega in parole povere il tempo che serve a caricare due window manager invece di uno. Ci sono altri metodi un po' più rapidi di questo,e sono descritti in seguito.

#### Autostart (senza "fusion-icon")

**Nota:** NON create il file compiz.desktop se intendete installare compiz-decorator-gtk; si creerebbe un conflitto al momento di installare il pacchetto.

*   Potete assicurarvi che Compiz Fusion parta sempre al login aggiungendo una voce nella cartella Autostart di KDE. Se questa voce non esiste (dovrebbe), create voi stessi un file `~/.kde/Autostart/compiz.desktop` con il contenuto seguente:

```
[Desktop Entry]
Encoding=UTF-8
Exec=compiz --replace ccp #Make sure ccp is included so that Compiz loads your previous settings.
StartupNotify=false
Terminal=false
Type=Application
X-KDE-autostart-after=kdesktop

```

**Nota:** Se il file `compiz.desktop` esiste già, potreste dover aggiungere "--replace" e\o "ccp" alla variabile Exec. Senza "--replace", Compiz non partirebbe visto che rileverebbe un altro window manager già in esecuzione, mentre senza "cpp" non verrebbero caricati i plugin abilitati tramite il Ccsm e compiz stesso sarebbe inutilizzabile.

**Nota:** Questo metodo può essere un po' lento poichè KDE deve caricare prima il suo window-manager (Kwin), per poi sostituirlo con Compiz lanciato appunto tramite questo collegamento. Quindi, impiega in parole povere il tempo che serve a caricare due window manager invece di uno. Ci sono altri metodi un po' più rapidi di questo,e sono descritti in seguito.

*   If you want to use the optional <tt>fusion-icon</tt> application, launch _fusion-icon_. If you log out normally with _fusion-icon_ running, KDE should restore your session and launch _fusion-icon_ the next time you log in if this setting is enabled. If it doesn't appear to be working, ensure you have the following line in `~/.kde/share/config/ksmserverrc`:

```
loginMode=restorePreviousLogout

```

**Nota:** This is a KDE specific setting that will allow you to restore other apps next time you log in, not just fusion-icon.

#### Esportazione della variabile KDEWM (Metodo Ottimale)

**Nota:** Usando questo metodo, Compiz verrà caricato come window manager di default al posto di Kwin. Questo metodo è dunque più veloce rispetto agli altri, poichè evita di caricare prima appunto, il window manager di default Kwin. Inoltre, alcuni piccoli malfunzionamenti o difetti noiosi come come alcuni brevi sfarfallii dello schermo (nel momento in cui Compiz va a sostituire Kwin) che si possono verificare con gli altri metodi.

Come utente Root, sarà necessario creare il breve script seguente, il quale vi permetterà di caricare Compiz direttamente: ciò è necessario perchè il vecchio metodo di impostare la variabile di sistema KDEWM con `export KDEWM="compiz --replace ccp --sm-disable"` pare non funzionare più.

```
$ echo "compiz --replace ccp --sm-disable &" > /usr/bin/compiz-fusion

```

**Nota:** Se questo comando non funziona, assicuratevi di aver installato il pacchetto "fusion-icon" e provate quest'altro comando:

```
$ echo "fusion-icon &" > /usr/bin/compiz-fusion

```

Assicuratevi però di aver completato tutti i passi descritti per questo metodo, prima di provare questa alternativa.

Assicuratevi che `/usr/bin/compiz-fusion` abbia i permessi di esecuzione.

```
$ chmod a+x /usr/bin/compiz-fusion

```

Scegliete poi una delle vie seguenti:

	1) Compiz solo per il vostro utente --> Modificate il file `~/.kde4/env/compiz.sh` e aggiungete la riga seguente così che KDE possa caricare compiz attraverso lo script che avete appena creato, invece di caricare KWin:

	 `KDEWM="compiz-fusion"` 

	2) Compiz per tutti gli utenti --> Modificate il file `/usr/env/compiz.sh` e aggiungete la riga seguente così che KDE possa caricare compiz attraverso lo script che avete appena creato, invece di caricare KWin:

	 `KDEWM="compiz-fusion"` 

**Nota:** Se il metodo proposto non funziona, provate l'alternativa al primo script descritta sopra.

**Nota:** Se nemmeno l'alternativa funziona, un ulteriore metodo consiste nell'inserire la riga `export KDEWM="compiz-fusion"` nel file `~/.bashrc` presente nella Home del vostro utente.

**Nota:** Se notate ancora malfunzionamenti e sul vostro sistema usate la directory `/usr/local/bin`, provate ad esportare lo script che avete creato usando il percorso completo: `export KDEWM="/usr/local/bin/compiz-fusion"` 

### GNOME

#### Autostart (senza "fusion-icon") (Metodo Ottimale)

**1)** Se già non esiste, create il file `/usr/share/applications/compiz.desktop` contenente:

```
[Desktop Entry]
Type=Application
Encoding=UTF-8
Name=Compiz
Exec=/usr/bin/compiz ccp  #Make sure ccp is included so that Compiz loads your previous settings.
NoDisplay=true
# name of loadable control center module
X-GNOME-WMSettingsModule=compiz
# autostart phase
X-GNOME-Autostart-Phase=WindowManager
X-GNOME-Provides=windowmanager
# name we put on the WM spec check window
X-GNOME-WMName=Compiz
# back compat only
X-GnomeWMSettingsLibrary=compiz

```

**Nota:** Se il file `compiz.desktop` esiste già, potreste dover aggiungere "--replace" e\o "ccp" alla variabile Exec. Senza "--replace", Compiz non partirebbe visto che rileverebbe un altro window manager già in esecuzione, mentre senza "cpp" non verrebbero caricati i plugin abilitati tramite il Ccsm e compiz stesso sarebbe inutilizzabile.

Se il metodo appena descritto non funziona, provate a mettere:

```
Exec=/usr/bin/compiz ccp --indirect-rendering

```

oppure

```
Exec=/usr/bin/compiz --replace --sm-disable --ignore-desktop-hints ccp --indirect-rendering

```

invece di

```
Exec=/usr/bin/compiz ccp

```

Alcuni notano un ritardo di 4-10 secondi quando si effettua il login da un login manager. La soluzione a questo problema è cambiare il comando in:

 `Exec=bash -c "compiz ccp --indirect-rendering --sm-client-id $DESKTOP_AUTOSTART_ID"` 

come consigliato [nel forum internazionale](https://bbs.archlinux.org/viewtopic.php?pid=655237#p655237).

**2)** Sarà poi necessario impostare alcuni parametri in Gconf tramite il tool da linea di comando oppure tramite la GUI Configuration Editor (gconf-editor). Le istruzioni indicate sono per il primo metodo, modificate quindi le chiavi indicate se usate l'interfaccia grafica:

**Nota:** Dato che queste impostazioni saranno relative ad un solo utente, **dovete** fare il logout dall'eventuale account root e fare il login con l'utente che appunto sarà interessato a questo procedimento.

Innanzitutto, il primo :

```
gconftool-2 --set -t string /desktop/gnome/session/required_components/windowmanager compiz

```

I comandi seguenti nondovrebbero essere necessari (le loro chiavi sono state rese deprecate da GNOME 2.12), ma in caso di insuccesso con il primo comando, si può sempre provarli:

```
gconftool-2 --set -t string /desktop/gnome/applications/window_manager/current /usr/bin/compiz
gconftool-2 --set -t string /desktop/gnome/applications/window_manager/default /usr/bin/compiz

```

#### Autostart (senza "fusion-icon", Gnome <= 2.24)

Questo metodo funziona se utilizzate GDM (e probabilmente anche KDM).

Create il file `/usr/local/bin/compiz-start-boot` con questo contenuto:

```
#!/bin/bash
export WINDOW_MANAGER="compiz ccp"
exec gnome-session

```

e rendetelo eseguibile con (`chmod +x /usr/local/bin/compiz-start-boot`). Poi create il file `/etc/X11/sessions/Compiz.desktop` e scrivetevi dentro:

```
[Desktop Entry]
Version=1.0
Encoding=UTF-8
Name=Compiz on GNOME
Exec=/usr/local/bin/compiz-start-boot
Icon=
Type=Application

```

Dopo un riavvio di GDM, dal menu delle sessioni selezionate quindi _Compiz on Gnome_ e dovreste aver concluso.

#### Autostart (con "fusion-icon")

Per avviare Compiz Fusion automaticamente quando si effettua il login, aggiungere in Sistema > Preferenze > Sessioni > Programmi d'Avvio una nuova voce di Nome:

```
Compiz Fusion

```

e Comando:

```
fusion-icon

```

il commento si può lasciarlo vuoto.

**Nota:** Si può anche mettere "compiz --replace ccp" invece di "fusion-icon" per caricare compiz ma non si avrà la icona di fusion-icon nella tray. l'opzione ccp indicherà a compiz di caricare le impostazioni scelte con il CompizConfig Settings Manager (ccsm).

Aggiungere "Compiz Fusion" alla lista dei programmi all'avvio è una buona idea per cambiare velocemente tra Metacity e Compiz tramite la apposita icona nella tray bar.

Potreste inoltre dover disattivare il compositor integrato di Metacity per far si che Compiz venga caricato automaticamente. Per fare ciò, si può usare il seguente comando da terminale:

```
gconftool-2 --type bool --set /apps/metacity/general/compositing_manager false

```

**Nota:** Questo metodo è più lento degli altri, visto che GNOME dovrà prima caricare metacity e poi sostituirlo con Compiz, impiegando dunque il tempo di caricamento di due gestori finestre anzichè di uno solo: per questo motivo gli altri metodi potrebbero essere una scelta migliore.

### XFCE

#### Autostart in XFCE (senza "fusion-icon")

Questo metodo farà partire Compiz direttamente tramite il gestore di sessione di XFCE senza caricare Xfwm.

Notare la modifica al file di configurazione xml necessaria per XFCE >= 4.2

Per installare il gestore della sessione di XFCE, installate il pacchetto xfce4-session

```
# pacman -S xfce4-session

```

Bisognerà procedere poi alla configurazione della sessione di default di XFCE, modificando innanzitutto il file con un editor di testo come nano:

```
$ nano ~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml

```

O alternativamente, per rendere la modifica effettiva per tutti gli utenti del sistema (serviranno i permessi di root)

```
# nano /etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml

```

Sostituite poi il comando di inizializzazione di xfwm

```
 <property name="Client0_Command" type="array">
   <value type="string" value="xfwm4"/>
 </property>

```

con il seguente:

```
 <property name="Client0_Command" type="array">
   <value type="string" value="compiz"/>
   <value type="string" value="ccp"/>
 </property>

```

**Nota:** il valore 'ccp' serve a far si che Compiz carichi le vostre impostazioni settate con ccsm.

Per evitare che la sessione appena creata venga sovrascritta, potreste voler aggiungere anche:

```
 <property name="general" type="empty">
   ...
   ...
   <property name="SaveOnExit" type="bool" value="false"/>
 </property>

```

Per rimuovere le sessioni esistenti, si dovrà eseguire il comando

```
$ rm -r ~/.cache/sessions

```

#### Autostart in XFCE (con "fusion-icon")

#### Metodo 1:

Questo metodo caricherà Xfwm, sostituiendolo poi con Compiz.

Aprite il XFCE Settings Manager, poi aprite _Sessions & Startup_. cliccate infine sulla scheda _Application Autostart_.

Aggiungete

```
  (Name:) Compiz Fusion

```

```
  (Command:) fusion-icon

```

**Nota:** Potete usare anche il comando "compiz --replace ccp" invece di "fusion-icon" per caricare solo compiz senza la fusion-icon. Il valore 'ccp' serve a far si che Compiz carichi le vostre impostazioni settate con ccsm.

**Nota:** Questo metodo è meno preferibile rispetto all'altro poichè carica due gestori finestre invece che uno. Tutti gli altri metodi caricano solo Compiz senza caricare prima Xfwm.

#### Metodo 2:

Modificate il file di configurazione seguente :

```
nano ~/.config/xfce4-session/xfce4-session.rc

```

O nel caso vogliate rendere le impostazioni definite per tutti gli utenti (tramite permessi di root)

```
# nano /etc/xdg/xfce4-session/xfce4-session.rc

```

Aggiungete poi la parte seguente

```
[Failsafe Session]
Client0_Command=fusion-icon

```

Commentate la riga

```
Client0_Command=xfwm4

```

se esiste.

Così facendo, XFCE caricherà direttamente compiz invece di XFwm quando non sarà rilevata una sessione attiva.

Per evitare che la sessione di default appena creata venga in qualche modo sovrascritta, potreste aggiungere le righe

```
[General]
AutoSave=false
SaveOnExit=false

```

Per rimuovere le sessioni esistenti, si dovrà eseguire il comando

```
rm -r ~/.cache/sessions

```

#### Metodo 3:

Controllate l'esistenza del file

```
~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml

```

Se questo file non esiste, createlo copiandolo dal file di default:

```
cp /etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml ~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml

```

e poi apritelo per modificarlo:

```
nano ~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml

```

o, per fare le modifiche in modo che coinvolgano tutti gli utenti, (tramite permessi di root):

```
# nano /etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml

```

Modificate poi la riga Client0_Command di modo da renderla così:

```
<property name="Client0_Command" type="array">
    <value type="string" value="fusion-icon"/>
    <value type="string" value="--force-compiz"/>
</property>

```

se non dovesse funzionare, al posto di **--force-compiz** provate **compiz --replace --sm-disable --ignore-desktop-hints ccp**.

Aggiungete poi la riga **SaveOnExit property** se mancante e impostatela a **false** come nell'esempio:

```
<property name="general" type="empty">
   <property name="FailsafeSessionName" type="string" value="Failsafe"/>
   <property name="SessionName" type="string" value="Default"/>
   <property name="SaveOnExit" type="bool" value="false"/>
 </property>

```

infine, rimuovete le vecchie sessioni XFCE:

```
rm -r ~/.cache/sessions

```

Ora XFCE dovrebbe caricare Compiz invece di Xfwm.

### Compiz come gestore di finestre autonomo

Configurate lo ~/.xinitrc per far si che lanci fusion-icon all'avvio.

```
exec fusion-icon

```

Come metodo alternativo, usate un semplice script che chiamerete **start-fusion.sh**:

```
#!/bin/sh
# add more apps here if necessary or start another panel, tray like pypanel, bmpanel, stalonetray
xfce4-panel&
fusion-icon

```

Se questo script non funzionasse, o nel caso abbiate problemi con la sessione dbus, provate questo:

```
#!/bin/sh
cd /home/<yourusername>
#
/usr/bin/X :0.0 -br -audit 0 -nolisten tcp vt7 &
#
export DISPLAY=:0.0
#
sleep 1
#
compiz-manager decoration move resize > /tmp/compiz.log 2>&1 &
# add more apps here if necessary or start another panel, tray like pypanel, bmpanel, stalonetray
xfce4-panel&
fusion-icon

```

Rendete questo script eseguibile e aggiungetelo allo ~/.xinitrc, così:

```
exec start-fusion.sh

```

Sentitevi liberi di personalizzare questi esempi come più vi aggrada, aggiungendo le varie applicazioni che volete caricare all'avvio. Vedere il thread sul [forum internazionale](https://bbs.archlinux.org/viewtopic.php?id=51282) o questo sul [forum italiano](http://www.archlinux.it/forum/viewtopic.php?pid=71729) per maggior informazioni.

#### Aggiungere un menu radice

Per aggiungere al desktop un menu simile a quello che appare in Openbox e similari, dovete installare il pacchetto [compiz-deskmenu](https://aur.archlinux.org/packages/compiz-deskmenu/) da [AUR](/index.php/AUR "AUR"). Una volta installato e configurato, avrete un menu che funzionerà come quello di openbox (clic sul desktop e appare il menu).

Se non vi funzionerà automaticamente, dovrete impostare a mano l'avvio del deskmenu. La procedura corretta per farlo, tramite ccsm, è:

- nel plugin "Comandi" (Commands) impostare nella "Command Line 0" a "compiz-deskmenu", nelle altre schede disabilitate qualsiasi scorciatoia di tasti o di mouse

- nel plugin "Selettore Area Visibile", ultima scheda, impostare "azione inizializzazione plugin" al tasto del mouse che volete utilizzare per aprire il menu (ad esempio, per il tasto centrale, impostare Button5"; nella riga sotto "Plugin per inizializzazione azione" scrivere "commands" e nella riga sotto ancora, la "Nome azione per inizia" mettete "run_command0_key"

Una alternativa a deskmenu può essere [mygtkmenu](https://aur.archlinux.org/packages/mygtkmenu/),anch'esso presente in [AUR](/index.php/AUR "AUR").

# Varie

## Impostate i plugin di base se volete usare Compiz!!

Assicuratevi di attivare alla prima configurazione di Compiz tramite il CCSM, i plugin "Decorazione Finestra", "Muovi Finestra", e "Ridimensiona Finestre". Depending on what packages you have downloaded you can choose between serveral window decorators. The most common ones are Emerald, kde-window-decorator, and gtk-window-decorator. The emerald decorator has the advantage that it fits better to compiz's screen handling and offers transparency effects. Use CompizConfig Settings Manager (ccsm) to change the default decorator: Window Decorator -> Command: "emerald --replace" or "kde4-window-decorator --replace" or "gtk-window-decorator --replace".

## Usare Compiz-Manager

Per usare compiz-manager, avrete innanzitutto bisogno di installarlo da community:

```
pacman -S compiz-manager

```

Compiz-manager, che sarà installato in `/usr/bin/compiz-manager`, è un semplice lanciatore per Compiz e TUTTE le sue opzioni. Per esempio, provate a lanciarlo da terminale

```
compiz-manager 

```

e guardate cosa viene restituito sul terminale stesso. Potete usarlo in tutti gli script che usate per lanciare compiz, in maniera molto semplice!

## Usare gtk-window-decorator

Per utilizzare gtk-window-decorator, installate il pacchetto _compiz-decorator-gtk_ e scegliete poi "GTK Window Decorator" invece di "Emerald" come vostro decoratore di finestre di default tramite fusion-icon o qualsiasi programma\script voi utilizziate per lanciare compiz.

## gconf: Configurazioni aggiuntive per Compiz

Per ottenere il massimo da Compiz, alcune impostazioni nascoste sono disponibili tramite gconf-editor:

```
$ gconf-editor

```

Notare che compiz-core non è compilato di default con supporto a gconf; lo è solo se installato tramite il pacchetto compiz-decorator-gtk. Dunque, se volete usare queste impostazioni tramite gconf, dovrete installarlo in questa maniera. Le configurazioni di Compiz sono sotto la chiave **apps** > **compiz** > **general** > **allscreens** > **options**.

"Active plugins" è dove è possibile specificare i plugin che vogliamo utilizzare. Semplicemente modificare dunque la lista (riferirsi alla chiave **apps** > **compiz** > **plugins** per vedere quali plugin è possibile attivare). Alcuni plugin utili possono essere screenshot, png, fade, e Minimizza.

## Scorciatoie da tastiera

Alcune scorciatoie di default (ovviamente i plugin relativi devono essere abilitati)

*   Switch finestres = Alt + Tab
*   Switch desktop sul cubo = Ctrl + Alt + freccia sinistra\destra
*   Muovi finestra = Alt + click sinistro
*   Ridimensiona finestra = Alt + click destro

Una lista più dettagliata la si può trovare sotto [CommonKeyboardShortcuts](http://wiki.compiz-fusion.org/CommonKeyboardShortcuts) nel wiki di Compiz, oppure potete semplicemente aprire il pannello di configurazione di ogni singolo plugin (sotto ccsm).

## Note per ATI R600/R700

Usando Fusion-icon non dovreste aver problemi, dato che questa utility si occupa automaticamente delle configurazioni per la vostra scheda. Se invece usate un altro metodo di avvio per Compiz, potreste avere dei piccoli malfunzionamenti. Per esempio, usando il metodo autostart di XFCE modificando, come sopra descritto, il file ~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml, vi accorgerete che Compiz non si avvierà. Dovete invece editare quel file e renderlo così

```
<property name="Client0_Command" type="array">
 <value type="string" value="LIBGL_ALWAYS_INDIRECT=1"/>
 <value type="string" value="compiz"/>
 <value type="string" value="--sm-disable"/>
 <value type="string" value="--ignore-desktop-hints"/>
 <value type="string" value="ccp"/>
 <value type="string" value="--indirect-rendering"/>
</property>

```

Questo esempio è specifico per XFCE, ma può essere adattato agli altri metodi, dovete solo aggiungere le varie opzioni descritte in questo esempio nel posto giusto. In particolare, dovete fare in modo che il comando lanciato per avviare compiz sia uguale a questo:

```
LIBGL_ALWAYS_INDIRECT=1 compiz --sm-disable --ignore-desktop-hints ccp --indirect-rendering

```

Che è il comando che XFCE fa partire interpretando il file di configurazione nell'esempio qui sopra. Notare che non avete bisogno del flag --replace perchè non state avviando Xfwm e poi Compiz, ma solo direttamente quest'ultimo.

# Risorse Aggiuntive

*   [Compiz Website](http://compiz.org) -- inclusi Wiki e Forum
*   [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") -- Un semplice gestore del composito

*   Wikipedia: [Compositing Window Managers](https://en.wikipedia.org/wiki/Compositing_window_manager "wikipedia:Compositing window manager")