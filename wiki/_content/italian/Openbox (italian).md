Openbox è un window manager leggero ed estremamente configurabile con un estensivo supporto di standard. Le sue funzionalità sono ben documentate sul [sito ufficiale](http://openbox.org). Questo articolo riguarderà Openbox su Arch Linux.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Effettuare l'aggiornamento ad Openbox 3.5](#Effettuare_l.27aggiornamento_ad_Openbox_3.5)
*   [3 Usare Openbox come unico gestore](#Usare_Openbox_come_unico_gestore)
*   [4 Gestore finestre per ambienti desktop](#Gestore_finestre_per_ambienti_desktop)
    *   [4.1 GNOME 2.24 e 2.26](#GNOME_2.24_e_2.26)
    *   [4.2 GNOME 2.26 Redux](#GNOME_2.26_Redux)
    *   [4.3 KDE](#KDE)
    *   [4.4 XFCE4](#XFCE4)
*   [5 Openbox per sistemi multihead](#Openbox_per_sistemi_multihead)
*   [6 Configurazione](#Configurazione)
    *   [6.1 Configurazione manuale](#Configurazione_manuale)
    *   [6.2 ObConf](#ObConf)
    *   [6.3 Configurazione delle applicazioni](#Configurazione_delle_applicazioni)
*   [7 Gestione del menu](#Gestione_del_menu)
    *   [7.1 Configurazione manuale dei menù](#Configurazione_manuale_dei_men.C3.B9)
    *   [7.2 Icone nel menù](#Icone_nel_men.C3.B9)
    *   [7.3 MenuMaker](#MenuMaker)
    *   [7.4 Obmenu](#Obmenu)
        *   [7.4.1 obm-xdg](#obm-xdg)
    *   [7.5 Xdg-menu](#Xdg-menu)
        *   [7.5.1 Script menu xdg basato su python](#Script_menu_xdg_basato_su_python)
    *   [7.6 openbox-menu](#openbox-menu)
    *   [7.7 OpenBox Menu Generator](#OpenBox_Menu_Generator)
        *   [7.7.1 obmenugen](#obmenugen)
        *   [7.7.2 obmenu-generator](#obmenu-generator)
    *   [7.8 Pipe menus](#Pipe_menus)
*   [8 Esecuzione automatica](#Esecuzione_automatica)
    *   [8.1 Abilitare l'esecuzione automatica](#Abilitare_l.27esecuzione_automatica)
    *   [8.2 Script d'esecuzione automatica](#Script_d.27esecuzione_automatica)
*   [9 Temi e aspetto](#Temi_e_aspetto)
*   [10 Programmi raccomandati](#Programmi_raccomandati)
*   [11 Suggerimenti](#Suggerimenti)
    *   [11.1 Funzione simile alla "Snap" di Aero](#Funzione_simile_alla_.22Snap.22_di_Aero)
    *   [11.2 Associazione dei file](#Associazione_dei_file)
    *   [11.3 Copia e incolla](#Copia_e_incolla)
    *   [11.4 Trasparenza](#Trasparenza)
    *   [11.5 Valori Xprop per le applicazioni](#Valori_Xprop_per_le_applicazioni)
        *   [11.5.1 Xprop per Firefox](#Xprop_per_Firefox)
    *   [11.6 Associare il menu a un tasto](#Associare_il_menu_a_un_tasto)
    *   [11.7 Urxvt sullo sfondo](#Urxvt_sullo_sfondo)
        *   [11.7.1 Eccezione MostraDesktop](#Eccezione_MostraDesktop)
        *   [11.7.2 Un'altra soluzione](#Un.27altra_soluzione)
    *   [11.8 Controllo del volume da tastiera](#Controllo_del_volume_da_tastiera)
        *   [11.8.1 Pulseaudio](#Pulseaudio)
*   [12 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [12.1 Crash del server X](#Crash_del_server_X)
    *   [12.2 Avvio automatico di applicazioni indesiderate](#Avvio_automatico_di_applicazioni_indesiderate)
    *   [12.3 SSH agent non viene più avviato automaticamente](#SSH_agent_non_viene_pi.C3.B9_avviato_automaticamente)
    *   [12.4 Openbox non registra una sessione D-Bus](#Openbox_non_registra_una_sessione_D-Bus)
    *   [12.5 Finestre che si caricano dietro quella attiva](#Finestre_che_si_caricano_dietro_quella_attiva)
*   [13 Risorse aggiuntive](#Risorse_aggiuntive)

## Installazione

[openbox](https://www.archlinux.org/packages/?name=openbox) è disponibile nel repository community:

 `# pacman -S openbox` 

Una volta installato, pacman vi indicherà di copiare i file di configurazione predefiniti `rc.xml`, `menu.xml`, `autostart`, e `environment` in `~/.config/openbox/`, ad esempio:

**Nota:** fare questo come utente semplice, non come root.

```
$ mkdir -p ~/.config/openbox/
$ cp /etc/xdg/openbox/{rc.xml,menu.xml,autostart,environment} ~/.config/openbox

```

Questi quattro file rappresentano la base della configurazione di openbox. Ogni file copre un determinato ambito della configurazione, e nello specifico i loro ruoli sono i seguenti:

	`rc.xml`

	Questo è il file di configurazione principale di Openbox. Viene usato per gestire le scorciatoie di tastiera, i temi, i desktop virtuali e altre funzioni.

	`menu.xml`

	Questo file controlla il menu di Openbox che appare quando si fa clic con il tasto destro sul desktop. Definisce lanciatori per le applicazioni ed altre scorciatoie. Consultare la sezione [#Menu](#Menu).

	`autostart`

	Questo file viene letto all'avvio di openbox-session. Contiene la lista dei programmi da eseguire all'avvio. È utilizzato solitamente per impostare variabili d'ambiente, lanciare un pannello/dock, impostare lo sfondo del desktop, o eseguire altri script all'avvio. Maggiori dettagli nel [Wiki di Openbox](http://openbox.org/wiki/Help:Autostart).

	`environment`

	Di questo file viene effettuato il source da openbox-session all'avvio. Contiene variabili d'ambiente da impostare nel contesto di Openbox. Ogni variabile specificata in questo file sarà visibile ad Openbox stesso ed a tutti i programmi lanciati tramite il suo menu.

## Effettuare l'aggiornamento ad Openbox 3.5

Se si sta effettuando l'aggiornamento a Openbox 3.5 o successivo da una versione precedente, fare attenzione a questi cambiamenti:

*   C'è un nuovo file di configurazione `environment` che bisogna copiare da `/etc/xdg/openbox` a `~/.config/openbox`.
*   Il file di configurazione precedentemente chiamato `autostart.sh` è ora definito `autostart`. Bisogna rinominare il proprio eliminando l'estensione .sh.
*   Parte della sintassi di configurazione all'interno di `rc.xml` è cambiata. Anche se Openbox sembra interpretare correttamente le vecchie regole, sarebbe bene confrontare il proprio file di configurazione con quello proposto in `/etc/xdg/openbox` e verificare i cambiamenti da apportare.

## Usare Openbox come unico gestore

Openbox può essere utilizzato come window manager indipendente (WM). Fare ciò è solitamente più semplice che installarlo e configurarlo perchè si integri in un DE. Eseguirlo in maniera indipendente può ridurre drasticamente il consumo di cpu e memoria. Basta aggiungere questo comando in fondo al file `~/.xinitrc`:

`exec openbox-session`

Consultare [xinitrc](/index.php/Xinitrc_(Italiano) "Xinitrc (Italiano)") per ulteriori dettagli, ad esempio su come preservare la sessione logind.

Se in precedenza si fosse utilizzato un altro gestore di finestre, come Xfwm, e Openbox non dovesse partire dopo aver effettuato il logout da X, provare a rinominare la cartella di avvio automatico:

 `$ mv ~/.config/autostart ~/.config/autostart-bak` 
**Nota:** Openbox richiede il pacchetto [python2-xdg](https://www.archlinux.org/packages/?name=python2-xdg) per eseguire il suo xdg-autostart

## Gestore finestre per ambienti desktop

Openbox può essere utilizzato per rimpiazzare il gestore di finestre di un Desktop Environment. Il metodo per effettuare la sostituzione, varia in base al DE.

### GNOME 2.24 e 2.26

Creare questo file

 `/usr/share/applications/openbox.desktop` 
```
[Desktop Entry]
 Type=Application
 Encoding=UTF-8
 Name=OpenBox
 Exec=openbox
 NoDisplay=true
 # name of loadable control center module
 X-GNOME-WMSettingsModule=openbox
 # name we put on the WM spec check window
 X-GNOME-WMName=OpenBox
```

In gconf, impostare **`/desktop/gnome/session/required_components/windowmanager`** su **`openbox`:**

 `$ gconftool-2 -s -t string /desktop/gnome/session/required_components/windowmanager openbox` 

Infine selezionare **GNOME** dal menù delle sessioni di GDM.

Se dopo l'installazione di openbox falliscono i tentativi di log in nella sessione 'Gnome/openbox', si può tentare quanto sotto specificato per effettuare l'avvio di openbox come window manager ogni volta che si effettua l'accesso nella sessione 'Gnome' dal proprio login manager (xdm, gdm, kdm, entrance, slim, etc.)

1.  Effettuare l'accesso solamente nella sessione di Gnome (che userà metacity quale unico window manager) per preparare quanto segue.
2.  Installare openbox se non è ancora stato fatto.
3.  Esplorare il menu verso *System → Preferences → Startup Applications* (probabilmente chiamato 'Session' per versioni meno recenti di Gnome)
4.  Selezionare "Applicazioni d'avvio", poi "Aggiungi" ed immettere il testo contenuto nel box sotto, omettendo quello preceduto da #.
5.  Premere "Aggiungi" per completare l'aggiunta della nuova voce ed assicurarsi che sia spuntata nella lista delle applicazioni d'avvio.
6.  Terminare la sessione di Gnome, rieffettuare l'accesso, e si dovrebbe finalmente essere nella nuova sessione di openbox.
7.  Buon divertimento!

```
Nome:    Openbox Windox Manager           # Can be changed
Comando: openbox --replace                # Text should not be removed from this line, but possibly added to it
Commento: Replaces metacity with openbox  # Can be changed

```

Sarà creata una nuova voce di avvio che verrà eseguita da gnome ogni volta che verrà richiamata una particolare sessione di gnome.

### GNOME 2.26 Redux

***Se la guida precedente non dovesse funzionare*** Ecco un altro modo per utilizzare Openbox all'interno della sessione Gnome:

1.  Effettuare il login all'interno della sessione Gnome (dovrebbe usare metacity come wm)
2.  Installare Openbox se non lo si ha ancora fatto.
3.  Navigare fino al menu *System → Preferences → Startup Applications* (potrebbe essere chiamato 'Session' in versioni precedenti di Gnome.
4.  Aprire Startup Application, selezionare '+add' ed inserire il testo mostrato di seguito. Omettere le righe che iniziano con un cancelletto #.
5.  Effettuare il logout dalla sessione Gnome, e ri-effettuare il login.
6.  Si dovrebbe ora stare eseguendo Openbox come window manager.

`Name: Openbox Windox Manager # Can be changed Command: openbox --replace # Text should not be removed from this line, but possibly added to it Comment: Replaces metacity with openbox # Can be changed`

Ciò creerà una voce nella lista di avvio di Gnome che sarà eseguita ogni volta che la sessione Gnome dell'utente sarà avviata.

### KDE

1.  Se si usa KDM, selezionare l'opzione di accesso "KDE/Openbox"
2.  Se si usa startx, aggiungere `exec openbox-kde-session` al file `~/.xinitrc`
3.  Per avviare da shell:

 `$ xinit /usr/bin/openbox-kde-session` 

### XFCE4

Effettuare l'accesso in una normale sessione XFCE4\. Dal terminale dare:

 `$ killall xfwm4 ; openbox & exit` 

Con questo si ucciderà xfwm4, si avvierà Openbox, e si chiuderà il terminale. Terminare la sessione, assicurandosi di spuntare la casella "Salvare la sessione per prossimi accessi". Al prossimo accesso, Xfce4 avvierà Openbox come WM.

Per essere abilitati a terminare la sessione xfce4, modificare il proprio `~/.config/openbox/menu.xml` (se il file non esiste, copiarlo da `/etc/xdg/openbox/menu.xml`). Trovare la seguente voce:

```
 <item label="Exit Openbox">
   <action name="Exit">
     <prompt>yes</prompt>
   </action>
 </item>

```

e modificarla così:

```
 <item label="Exit Openbox">
   <action name="Execute">
     <prompt>yes</prompt>
    <command>xfce4-session-logout</command>
   </action>
 </item>

```

Altrimenti usando la voce "Exit" dal menu si termina l'esecuzione di Openbox, rimanendo senza window manager.

Se c'è qualche problema a cambiare tra desktops virtuali con la rotella del mouse (salta qualche desktop), aprire il file `~/.config/openbox/rc.xml` e spostare i binding delmouse del mouse relativi alle azioni "DesktopPrevious" e "DesktopNext" dal contesto "Desktop" al contesto "Root" (si potrebbe dover definire il contesto *Root*).

Volendo usare il root-menu di Openbox invece di quello di Xfce, è possibile terminare Xfdesktop dando il seguente comando in un terminale:

 `$ xfdesktop --quit` 

In ogni caso, Xfdesktop gestisce gli sfondi e le icone del desktop, obbligando l'utente ad usare per queste funzioni altri strumenti, come ad esempio ROX.

(Quando si termina Xfdesktop, il problema di cui sopra dei desktop virtuali non si dovrebbe ripresentare.)

Se si vuole mantenere un rc.xml separato rispetto a quello utilizzato durante la sessione openbox indipendente, modificare `~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml` o (per rendere la modifica efficace per tutti gli utenti) `/etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml`, sostituendo il comando di avvio di xfwm

```
<property name="Client0_Command" type="array">
  <value type="string" value="xfwm4"/>
</property>

```

con questo:

```
<property name="Client0_Command" type="array">
  <value type="string" value="openbox"/>
  <value type="string" value="--config-file"/>
  <value type="string" value="~/.config/xfce4/openbox/rc.xml"/>
</property>

```

La stessa modifica può essere apportata per il menù, tenendo presente che in questo caso però il file xml del menu personalizzato dovrà essere presente in `~/.config/openbox/`.

## Openbox per sistemi multihead

Anche se Openbox fornisce un supporto al multi-monitor più che soddisfacente, esiste un branch apposito reperibile su [AUR] chiamato [openbox-multihead-git](https://aur.archlinux.org/packages/openbox-multihead-git/) che fornisce un desktop indipendente per ogni monitor. Questo modello non è molto comune tra i window manager floating, in quanto è principalmente riscontrabile in quelli tiling. È ben spiegato sul [sito web di Xmonad](http://xmonad.org/tour.html#workspace%7C). Consultare anche il [readme specifico](https://github.com/BurntSushi/openbox-multihead/blob/multihead/README.MULTIHEAD) per una descrizione più comprensibile delle funzionalità e delle opzioni di configurazione disponibili in Openbox Multihead.

Openbox Multihead funzionerà come il classico Openbox in presenza di un solo monitor.

Una delle controindicazioni dell'utilizzo di Openbox Multihead è che non rispetta l'assunto EWMH che uno ed un solo dektop può essere visibile in un dato istante. Per questo motivo i pager esistenti non funzioneranno correttamente. Per ovviare a ciò è disponibile su [AUR](/index.php/AUR "AUR") [pager-multihead-git](https://aur.archlinux.org/packages/pager-multihead-git/), che è compatibile con Openbox Multihead. [Screenshots](http://imgur.com/a/cnZeq#y04nk).

Infine, su [AUR](/index.php/AUR "AUR") è anche disponibile una nuova versione di [pytile3-git](https://aur.archlinux.org/packages/pytile3-git/) che funziona correttamente con Openbox Multihead.

Sia pytile3 che pager-multihead-git funzioneranno senza Openbox Multihead se è attivo un solo monitor.

## Configurazione

Ci sono diversi metodi per configurare le impostazioni di Openbox.

### Configurazione manuale

Per configurare Openbox manualmente, modificare `~/.config/openbox/rc.xml` con un editor di testi. Il file contiene commenti molto esplicativi al suo interno. Consultare [la documentazione](http://openbox.org/wiki/) per ulteriore documentazione riguardo al file.

### ObConf

[ObConf](http://openbox.org/wiki/ObConf:About) è uno strumento di configurazione per Openbox. È usato per definire la maggior parte delle preferenze più comuni, inclusi temi, desktop virtuali, proprietà delle finestre e margini del desktop.Per installare ObConf:

 `# pacman -S obconf` 

Al momento ObConf non può essere usato per gestire le scorciatoie di tastiera e alcune funzioni avanzate. Per queste modifiche, l'utente deve ricorrere alla modifica manuale del file `rc.xml`. Un'alternativa è l'applicazione [obkey](https://aur.archlinux.org/packages/obkey/) disponibile nei [repository ufficiali](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)")

### Configurazione delle applicazioni

Openbox permette di definire regole per le singole applicazioni. Ad esempio si può:

*   Caricare il web browser preferito in un determinato desktop
*   Avviare il terminale senza i bordi della finestra
*   Posizionare all'avvio il client torrent in una certa posizione del monitor

Queste regole sono definite in `~/.config/openbox/rc.xml`. Le istruzioni sono ben dettagliate all'interno dello stesso file. Documentazione dettagliata può anche essere reperita [qui](http://openbox.org/wiki/Help:Applications)

## Gestione del menu

Il menu di base di Openbox include già molte voci. Molte di queste lancerebbero applicazioni che non si utilizzano e che magari non state neppure installate. Si vorrà certamente personalizzare `menu.xml` prima o poi . Vi sono diversi modi per farlo.

**Note:** Per ricaricare il menù, si può sia eseguire in un terminale "openbox --reconfigure", sia fare click-destro-sul-desktop->Sistema->Riconfigura Openbox

### Configurazione manuale dei menù

È possibile modificare `~/.config/openbox/menu.xml` con il proprio editor di testo. Anche se molti comandi sono facilmente intuibili, potete consultare la [documentazione ufficiale](http://openbox.org/wiki/Help:Menus).

### Icone nel menù

Per avere delle icone a fianco alle voci nel menù. Aggiungere `<showIcons>yes</showIcons>` nella sezione `<menu>` del file `rc.xml`. Modificare quindi le voci del menù in `menu.xml` ed aggiungere `icons="<path>"` alle voci di menù per le quali si desidera l'icona, in questo modo: `<menu id="apps-menu" label="SomeApp" icon="/home/user/.icons/application.png">`

A questo punto eseguire `openbox --reconfigure` per aggiornare il menù.

### MenuMaker

[MenuMaker](http://menumaker.sourceforge.net/) è un potente strumento per creare menù XML per diversi Windows Manager, incluso Openbox. MenuMaker cercherà programmi eseguibili nel computer e creerà un file di menù basato sui risultati. Può essere configurato per escludere alcuni tipi di applicazione (applicazioni di GNOME, KDE, Xfce etc.) se l'utente lo desidera.

MenuMaker è disponibile nel repository [community]:

 `# pacman -S menumaker` 

Una volta installato, si può generare un menu completo (chiamato `menu.xml`) con uno dei seguenti comandi:

 `$ mmaker -v OpenBox3` 

in questo modo non si sovrascriverà un file di menù pre-esistente.

 `$ mmaker -vf OpenBox3` 

l'opzione force permette di sovrascrivere un file di menu pre-esistente

 `mmaker --help` 

visualizza la lista delle opzioni disponibili

MenuMaker vi darà un menu abbastanza approfondito. Ora è possibile modificare il `menu.xml` a mano, o rigenerare la lista ogni volta che si installa nuovo software.

### Obmenu

[Obmenu](http://obmenu.sourceforge.net/) è un editor di menu per Openbox con un'interfaccia grafica. E' una buona opzione per coloro che non amano sporcarsi le mani con codice XML.

E' disponibile nei repository ufficiali:

 `# pacman -S obmenu` 

Una volta installato, basta eseguire il comando `obmenu` e aggiungere o rimuovere le applicazioni desiderate.

#### obm-xdg

`obm-xdg` è uno strumento per riga di comando che viene installato assieme a Obmenu. Può generare un sottomenu categorizzato di applicazioni GTK/GNOME installate.

Per usare obm-xdg con altri menù, aggiungere la riga seguente al file `~/.config/openbox/menu.xml`: {{Ic|<menu execute="obm-xdg" id="xdg-menu" label="xdg"/>

Dopodichè aggiungere la seguente riga sotto la voce 'root-menu' dove si vuole che il menu venga mostrato `<menu id="xdg-menu"/>`

Dopodichè eseguire il comando `openbox --reconfigure` per aggiornare il menu di Opebox. Un sottomenu chiamato **xdg** dovrebbe essere ora apparso nel vostro menu.

Per utilizzare obm-xdg in maniera indipendente, creare `~/.config/openbox/menu.xml` ed aggiungere queste righe: {{Ic|<openbox_menu> <menu execute="obm-xdg" id="root-menu" label="apps"/> </openbox_menu>

Dopodichè eseguire il comando `openbox --reconfigure` per aggiornare il menu di Opebox. Un sottomenu chiamato **xdg** dovrebbe essere ora apparso nel vostro menu.

**Nota:** Se non avete installato GNOME, allora dovete installare il pacchetto **gnome-menus** per utilizzare obm-xdg.

### Xdg-menu

[Xdg-menu](/index.php/Xdg-menu "Xdg-menu") può generare automaticamente un menù per openbox a partire da dei file xdg. Può essere installato col pacchetto [archlinux-xdg-menu](https://www.archlinux.org/packages/?name=archlinux-xdg-menu) presente nei [repository ufficiali](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)"). Per una guida all'utilizzo dei menu XDG consultare [Xdg-menu#OpenBox](/index.php/Xdg-menu#OpenBox "Xdg-menu")

#### Script menu xdg basato su python

Questo script è reperibile nel pacchetto openbox di Fedora. La versione più recente dello script è reperibile [a questo indirizzo](http://pkgs.fedoraproject.org/cgit/openbox.git/tree/xdg-menu).

Scaricarlo e salvarlo dove più fa comodo.

Aprire poi `menu.xml` con un editor di testo e aggiungere la seguente voce dove si preferisce nel nuovo menu (naturalmente è possibile modificare l'etichetta): `<menu id="apps-menu" label="xdg-menu" execute="python2 <path>/xdg-menu"/>`

Salvare il file ed eseguire: `openbox --reconfigure`.

**Nota:** Se non si ha Gnome installato, sarà necessario installare il pacchetto [gnome-menus](https://www.archlinux.org/packages/?name=gnome-menus) perchè xdg-menu funzioni.

### openbox-menu

[Openbox-menu](http://mimasgpc.free.fr/openbox-menu_en.html) utilizza [menu-cache](http://sourceforge.net/projects/lxde/files/menu-cache/) dal progetto LXDE per creare un menu dinamico per Openbox. L'homepage del progetto si trova [http://mimasgpc.free.fr/openbox-menu_en.html qui](http://mimasgpc.free.fr/openbox-menu_en.html), mentre il pacchetto è disponibile su [AUR](/index.php/AUR "AUR") come [openbox-menu](https://aur.archlinux.org/packages/openbox-menu/)

### OpenBox Menu Generator

#### obmenugen

OpenBox Menu Generator, reperibile su [AUR] come [obmenugen-bin](https://aur.archlinux.org/packages/obmenugen-bin/) è un generatore di menu per Openbox che utilizza i file `*.desktop`. Fornisce un file di testo che filtra, usando espressioni regolari di base, le voci di menu che sono nascoste. Per utilizzarlo, lanciare semplicemente:

 `$ obmenugen         #crea un file di menu` 

quindi aggiornare OpenBox con:

 `$ openbox --reconfigure    #per vedere il menu che è stato appena generato` 

#### obmenu-generator

Obmenu-generator è un generatore di menu dinamici/statici per Openbox col supporto alle icone. Può essere installato da [AUR](/index.php/AUR "AUR") tramite il pacchetto [obmenu-generator](https://aur.archlinux.org/packages/obmenu-generator/).

Il seguente comando genera un menù dinamico con icone:

 `obmenu-generator -p -i` 

### Pipe menus

Openbox (ed altri WM come WindowMaker e PekWM) permettono di scrivere degli scripts che generano dinamicamente dei menu. Alcuni esempi sono monitor di sistema, controlli per i media player, e previsioni del tempo. Molti altri esempi possono essere trovati su [questa pagina](http://openbox.org/wiki/Openbox:Pipemenus) del sito di Openbox.

Alcuni interessanti pipe-menu forniti da utenti Openbox:

*   **obfilebrowser** — Pipe menu file browser.

	[http://xyne.archlinux.ca/projects/obfilebrowser/](http://xyne.archlinux.ca/projects/obfilebrowser/) || [obfilebrowser](https://aur.archlinux.org/packages/obfilebrowser/)

*   **wifi-pipe** — Pipe menu for scanning and connecting to wireless hot spots using netcfg.

	[https://github.com/pbrisbin/wifi-pipe](https://github.com/pbrisbin/wifi-pipe) || [wifi-pipe](https://aur.archlinux.org/packages/wifi-pipe/)

*   **obdevicemenu** — Pipe menu for managing removable devices using Udisks.

	[https://bbs.archlinux.org/viewtopic.php?id=114702](https://bbs.archlinux.org/viewtopic.php?id=114702) || [obdevicemenu](https://aur.archlinux.org/packages/obdevicemenu/)

## Esecuzione automatica

Openbox supporta l'esecuzione automatica di programmi all'avvio. Questa funzione è fornita dal comando **openbox-session**.

### Abilitare l'esecuzione automatica

Ci sono due modi per abilitare l'esecuzione automatica:

1.  Se si usa startx/xinit per accedere alla sessione X, modificare ``./xinitrc` in modo che la riga che esegue ***openbox*** esegua invece ***openbox-session*** .
2.  Se si usa GDM/KDM, selezionare la sessione *Openbox* e questa utilizzerà l'esecuzione automatica.

### Script d'esecuzione automatica

Openbox fornisce uno script d'esecuzione automatica per tutto il sistema che viene applicato a tutti gli utenti e si trova in `/etc/xdg/openbox/autostart`. Un utente può comunque creare il proprio script personale che verrà eseguito subito dopo quello generico, creandolo come `~/.config/openbox/autostart`. Quest'ultimo file non viene generato di default, e deve essere espressamente creato dall'utente.

Istruzioni complete sono reperibili in [questo articolo sul sito di Openbox](http://openbox.org/wiki/Help:Autostart).

**Nota:**

*   I file di autostart venivano chiamati autostart.sh fino alla versione 3.5.0 di Openbox. Anche se attualmente questi file sono ancora funzionanti, gli utenti che effettuano un aggiornamento del WM sono invitati ad eliminare il suffisso .sh
*   Tutti i programmi nel file autostart dovrebbero essere eseguiti come demoni o in background, altrimenti gli elementi all'interno di `/etc/xdg/autostart/` non saranno eseguiti.

## Temi e aspetto

L'articolo supplementare **[Openbox Themes and Apps](/index.php/Openbox_Themes_and_Apps_(Italiano) "Openbox Themes and Apps (Italiano)")** contiene informazioni dettagliate sulla modifica della GUI di Openbox.

## Programmi raccomandati

La pagina wiki supplementare **[Openbox Themes and Apps](/index.php/Openbox_Themes_and_Apps#Recommended_programs "Openbox Themes and Apps")** contiene informazioni sui programmi che si possono utilizzare con Openbox.

L'articolo fornisce dettagli su pannelli, gestori della system tray, gestori del volume, ed altri elementi utilizzabili su un sistema desktop.

Visitate anche la [lista di applicazioni](/index.php/List_of_Applications_(Italiano) "List of Applications (Italiano)"). Molte di queste funzionano senza problemi in Openbox.

## Suggerimenti

### Funzione simile alla "Snap" di Aero

Tramite le configurazioni di Openbox, è possibile ottenere un comportamento simile alla funzione Snap di Aero (Windows Vista), cioè che le finestre vadano automaticamente ad occupare solo metà dello schermo. Una spiegazione dettagliata è reperibile [[in questa discussione del forum italiano](http://www.archlinux.it/forum/viewtopic.php?f=17&t=10545)]

### Associazione dei file

Dal momento che Openbox e le applicazioni che si intende utilizzare con esso non sono molto ben integrati si potrebbe incorrere nel problema che il browser non sappia quale programma si suppone di utilizzare per determinati tipi di file. Il pacchetto [gnome-defaults-list](https://aur.archlinux.org/packages/gnome-defaults-list/), scaricabile da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") contiene un elenco di tipi di file e programmi specifici per il desktop GNOME. Una volta installato troverete la lista in `/etc/gnome/defaults.list`

Una volta aperto il file con il proprio editor di testo preferito, sarà necessario solo cercare e sostituire le applicazioni pre-impostate con i programmi voluti. Come ad esempio totem<=>vlc o eog<=>mirage. Salvare il file in `~/.local/share/applications/defaults.list`

Un altro modo è usare il pacchetto [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) dai repository, e richiamare il comando `mimeopen` in questo modo:

 `$ mimeopen -d /percorso/del/file` 
```
Please choose a default application for files of type text/plain
       1) notepad  (wine-extension-txt)
       2) Leafpad  (leafpad)
       3) OpenOffice.org Writer  (writer)
       4) gVim  (gvim)
       5) Other...

```

Verrà chiesto quale applicazione da utilizzare durante l'apertura di */percorso/del/file*: La vostra risposta sarà impostata come gestore predefinito per quel tipo di file. Se non si riesce a trovare `mimeopen`, il suo percorso è:

```
/usr/bin/perlbin/vendor/mimetype

```

### Copia e incolla

Da terminale, `Ctrl`+`Ins` per la funzione copia e `Shift`+`Ins` per incolla funziona bene in genere. Si può anche copiare de terminale con `Ctrl`+`Shift`+`C`, ed incollare con il tasto centrale del mouse.

### Trasparenza

Utilizzando il programma [transset-df](https://www.archlinux.org/packages/?name=transset-df), che è in linea di massima simile a [transset](/index.php?title=Transset&action=edit&redlink=1 "Transset (page does not exist)"),

 `# pacman -S transset-df` 

è possibile abilitare la transparenza delle finestre in modo veloce. Ad esempio modificando quanto segue in `~/.config/openbox/rc.xml` si otterrà che con il movimento della rotella del mouse quando il cursore è sulla barra del titolo (osservare la sezione <mouse>), si faccia variare la trasparenza della finestra.:

 `~/.config/openbox/rc.xml` 
```
<context name="Titlebar">
   . . .
   <mousebind button="Up" action="Click">
     <action name= "Execute" >
       <execute>transset-df -p .2 --inc  </execute>
     </action>
   </mousebind>
   <mousebind button="Down" action="Click">
     <action name= "Execute" >
       <execute>transset-df -p .2 --dec </execute>
     </action>
   </mousebind>
   . . .
</context>
```

Per il momento sembra funzionare bene se non sono stati abilitati altri tipi di funzione nel gruppo action.

### Valori Xprop per le applicazioni

Utilizzando impostazioni personalizzate a seconda del tipo di applicazione, potrebbe essere comodo il bash alias:

`alias xp='xprop | grep "WM_WINDOW_ROLE\|WM_CLASS" && echo "WM_CLASS(STRING) = \"NAME\", \"CLASS\""'`

Per usarlo eseguire **`xp`** e fare click sul programma in esecuzione di cui si vogliono definire le configurazioni per-app. Il risultato visualizzerà solo le informazioni richieste da Openbox, in pratica i valori WM_WINDOW_ROLE e WM_CLASS (nome e tipo):

 `[thayer@dublin:~] $ xp` 
```
WM_WINDOW_ROLE(STRING) = "roster"
WM_CLASS(STRING) = "gajim.py", "Gajim.py"
WM_CLASS(STRING) = "NAME", "CLASS"
```

#### Xprop per Firefox

Per diversi motivi, Firefox e i suoi equivalenti ignorano le regole delle applicazioni (es. <desktop>) a meno che non si usi `class="Firefox*"`. Ciò implica il non rispetto di qualsiasi cosa venga riportata da xprop come attuale valore WM_CLASS del programma.

### Associare il menu a un tasto

Ad alcuni utenti piace associare il menu pricipale di Openbox, o qualsiasi altro, ad un tasto. Potrebbe essere utile, ad esempio, per creare un menu a bottone in un pannello. Sebbene ciò non sia supportato da Openbox, un semplice script reperibile su [AUR], [xdotool](https://www.archlinux.org/packages/?name=xdotool), basta a simulare la pressione di un tasto. Per usarlo, aggiungere semplicemente alla sezione <keyboard> del proprio `rc.xml`:

 `~/.config/openbox/rc.xml` 
```
<keybind key="A-C-q">
  <action name="ShowMenu">
     <menu>root-menu</menu>
  </action>
</keybind>

```

Riavviare/reconfigure Openbox. Si potrà ora magicamente richiamare il menu nella posizione del cursore eseguendo il seguente comando:

 `# xdotool key ctrl+alt+q` 

È ovviamente possibile cambiare le scorciatoie secondo i propri gusti o esigenze.

### Urxvt sullo sfondo

Con Openbox, eseguire un terminale come sfondo del desktop è facile. Non avete bisogno di **devilspie** in questo caso.

Innanzitutto sarà necessario abilitare la trasparenza, aprendo il proprio file `.Xdefaults` (in caso non esistesse, andrà creato nella propria /home).

 `~/.Xdefaults` 
```
URxvt*transparent:true
URxvt*scrollBar:false
URxvt*geometry:124x24  #Dimensioni del terminale. In caso voi lo vogliate full-screen, non usate questa opzione ma guardate sotto
URxvt*borderLess:true
URxvt*foreground:Black #Colore dei font. Da impostare su White in caso di utilizzo di desktop scuri.

```

Infine, bisognerà modificare il proprio file `~/.config/openbox/rc.xml`:

 `~/.config/openbox/rc.xml` 
```
<application name="urxvt">
  <decor>no</decor>
  <focus>yes</focus>
  <position>
    <x>center</x>
    <y>20</y>
  </position>
  <layer>below</layer>
  <desktop>all</desktop>
  <maximized>true</maximized> #In caso si voglia il terminale full-screen.
  <skip_taskbar>true</skip_taskbar> #permette al processo di venire eseguito senzache compaia nel pannello 
</application>

```

La *magia* viene dalla riga `<layer>below</layer>`, che piazzerà il terminale sotto tutte le altre. In questo caso, URxvt sarà visualizzato su tutti i desktop, ovviamente è possibile cambiare questo comportamento.

Notare che, invece di usare `<application name="URxvt">` nella prima riga, è possibile usare un altro nome (*URxvt-bg* ad esempio), e utilizzare l'opzione -name al lancio di uxrvt. In questo modo, solo i terminali che lancerete con l'opzione saranno impostati con le regole scelte nel file rc.xml. Ad esempio:

 `urxvt -name URxvt-bg` 

#### Eccezione MostraDesktop

Se si utilizza MostraDesktop per minimizzare tutte le applicazioni aperte, questo minimizzerà anche la finestra di urxvt. Vi sono diversi metodi per ovviare a ciò, ma nessuno funziona senza problemi:

*   un metodo è spiegato in [questo post](https://bbs.archlinux.org/viewtopic.php?pid=865844#p865844). Prevede la modifica del codice sorgente di urxvt.

**Attenzione:** Questo metodo pare non essere più funzionante dopo un recente aggiornamento, portando ora ad un problema di memory leak quando viene utilizzata la versione patchata di urxvt.

*   il metodo migliore è spiegato [qui](https://bbs.archlinux.org/viewtopic.php?pid=929792#p929792). Ha comunque una grossa controindicazione: rende l'azione MostraDesktop irreversibile, impedendo che le altre applicazioni vengano ri-massimizzate alla successiva invocazione del comando.

#### Un'altra soluzione

Impostazioni della finestra:

 `~/.config/openbox/rc.xml` 
```
<application name="RootTerm">
      <decor>no</decor>
      <skip_taskbar>yes</skip_taskbar>
      <skip_pager>yes</skip_pager>
      <layer>normal</layer>
      <position>
        <x>center</x>
        <y>0</y>
      </position>
      <focus>yes</focus>
      <desktop>all</desktop>
      <maximized>true</maximized>
    </application>
```

Binding dei tasti:

 `~/.config/openbox/rc.xml` 
```
<keybind key="W-d">
  <action name="Execute"> <command>~/.config/openbox/toggle_shell.sh</command> </action>
</keybind>
```

E lo script:

 `~/.config/openbox/toggle_shell.sh` 
```
 wc -l)
	if [ $wind_num -ne 0 ]
	then
		xdotool windowminimize $term_id
		xdotool windowfocus $(xdotool getwindowfocus)
		echo "hide"
	fi
else
	xdotool windowactivate $term_id
	echo "show"
fi

```

Le righe seguenti avviano urxvt al login. Ciò previene la chiusura involontaria di urxvt.

 `~/.config/openbox/autostart` 
```
...
(while :; do urxvt -name RootTerm; done;) &
...
```

### Controllo del volume da tastiera

Se si usa ALSA per l'audio, è possibile usare il programma amixer per regolare il volume dell'audio. Inoltre è possibile usare le associazioni dei tasti di Openbox in modo che si comportino come tasti multimediali. (Alternativamente, si potrebberero cercare i nomi dei tasti multimediali che si hanno e mapparli.) Per esempio, nella sezione `<keyboard>` di rc.xml:

 `~/.config/openbox/rc.xml` 
```
<keybind key="W-Up">
  <action name="Execute">
    <command>amixer set Master 5%+</command>
  </action>
</keybind>

```

Questo vincola i tasti Windows + Freccia Su ad alzare il proprio volume Master ALSA del 5%. La corrispondente associazione per abbassare il volume:

 `~/.config/openbox/rc.xml` 
```
<keybind key="W-Down">
  <action name="Execute">
    <command>amixer set Master 5%-</command>
  </action>
</keybind>

```

In un altro esempio, è possibile anche usare l'associazione dei tasti per XF86Audio:

 `~/.config/openbox/rc.xml` 
```
<keybind key="XF86AudioRaiseVolume">
  <action name="Execute">
    <command>amixer set Master 5%+ unmute</command>
  </action>
</keybind>
<keybind key="XF86AudioLowerVolume">
  <action name="Execute">
    <command>amixer set Master 5%- unmute</command>
  </action>
</keybind>
<keybind key="XF86AudioMute">
  <action name="Execute">
    <command>amixer set Master toggle</command>
  </action>
</keybind>

```

Quest'ultimo esempio dovrebbe funzionare per la maggior parte delle tastiere multimediali. Dovrebbe consentire di alzare, abbassare e disattivare il controllo Master della propria scheda audio usando i rispettivi tasti multimediali. Notare inoltre che in questo esempio:

*   Il tasto "Muto" dovrebbe riattivare il controllo Master se è già disattivato.
*   I tasti "Alzare" e "Abbassare" dovrebbero riattivare il controllo Master se esso è disattivato.

#### Pulseaudio

Se si utilizza Pulseaudio con ALSA come backend, il precedente keybinding deve essere modificato per istruire amixer ad utilizzare pulse

 `~/.config/openbox/rc.xml` 
```
<keybind key="XF86AudioRaiseVolume">
  <action name="Execute">
    <command>amixer -D pulse set Master 5%+ unmute</command>
  </action>
</keybind>
<keybind key="XF86AudioLowerVolume">
  <action name="Execute">
    <command>amixer -D pulse set Master 5%- unmute</command>
  </action>
</keybind>
<keybind key="XF86AudioMute">
  <action name="Execute">
    <command>amixer set Master toggle</command>
  </action>
</keybind>

```

Questo keybinding dovrebbe funzionare per la maggior parte dei sistemi. Altri esempi sono reperibili [qui](http://ubuntuforums.org/showthread.php?t=987149)

## Risoluzione dei problemi

### Crash del server X

Al passaggio alla versione 3.5 di Openbox, sono stati segnalati problemi che portano il server grafico ad andare in crash nel tentativo di eseguire Openbox, con messaggi d'errore simili al seguente

```
(metacity:25137): GLib-WARNING **: In call to g_spawn_sync(), exit status of a child process 
was requested but SIGCHLD action was set to SIG_IGN and ECHILD was received by waitpid(), so exit 
status can't be returned. This is a bug in the program calling g_spawn_sync(); either do not request 
the exit status, or do not set the SIGCHLD action.
xinit: connection to X server lost
waiting for X server to shut down

```

Nel caso particolare utilizzato come esempio, nel quale il problema era da imputare a metacity, la soluzione è stata la rimozione dei pacchetti metacity e compiz-decorator-gtk. Successivamente si è capito che sarebbe stata sufficiente la loro re-installazione.

È possibile trovare in rete molti casi simili, non imputabili a metacity, perciò qualsiasi cosa si utilizzi al posto di metacity, in caso di errori analoghi a quello proposto, si può provare a re-installare il proprio programma.

### Avvio automatico di applicazioni indesiderate

Se si riscontra l'avvio automatico di applicazioni non volute, e che quindi non sono state aggiunte a `~/.config/openbox/autostart script`, verificare che all'interno della directory `~/.config/autostart/` non vi siano residui del precedente utilizzo di DE quali Gnome, KDE etc., ed eventualmente rimuoverli.

### SSH agent non viene più avviato automaticamente

Mentre fino alla versione 3.4.x di Openbox, era possibile eseguire un agente SSH da `~/.config/openbox/autostart.sh`, dalla versione 3.5 questo sembra non funzionare più. È necessario inserire il proprio codice all'interno di `~/.config/openbox/environment`, ad esempio

 `~/.config/openbox/environment` 
```
SSHAGENT="/usr/bin/ssh-agent"
SSHAGENTARGS="-s"
if [ -z "$SSH_AUTH_SOCK" -a -x "$SSHAGENT" ]; then
        eval `$SSHAGENT $SSHAGENTARGS`
        trap "kill $SSH_AGENT_PID" 0
fi
```

### Openbox non registra una sessione D-Bus

Proprio come per l'agente SSH, molti utenti erano abituati a tenere il loro codice per l'esecuzione di una sessione D-Bus all'interno di `~/.config/openbox/autostart.sh`. Questo metodo non funziona più (ad es. Thunar non rileva alcun dispositivo rimovibile).

### Finestre che si caricano dietro quella attiva

Le finestre di alcune applicazioni (come firefox) potrebbero caricarsi alle spalle della finestra attiva, rendendo necessario all'utente clickare sulla finestra appena creata per prenderne il focus. Per risolvere questo problema aggiungere al proprio `~/.config/openbox/rc.xml`, nei tag `<openbox_config>` e `</openbox_config>`:

```
<applications>
  <application class="*">
    <focus>yes</focus>
  </application>
</applications>
```

# Risorse aggiuntive

*   [Openbox Website](http://openbox.org/wiki) - Il sito ufficiale
*   [Planet Openbox](http://planetob.openmonkey.com/) - Il portale delle news di Openbox
*   [Box-Look.org](http://www.box-look.org/) - Una buona risorsa di temi e arte correlata