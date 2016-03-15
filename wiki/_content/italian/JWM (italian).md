**JWM** (Joe's Window Manager) è un peso piuma tra i [Window Manager](/index.php/Window_manager_(Italiano) "Window manager (Italiano)") per il [X11 Window System](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System"). scritto in [C](https://en.wikipedia.org/wiki/C_(programming_language) "wikipedia:C (programming language)"); È in uno stato di sviluppo attivo ed è mantenuto da [Joe Wingbermuehle](http://joewing.net/about.shtml). *...Sebbene lo sviluppo di JWM abbia rallentato un po', Joe Wingbermuehle continua a lavorarci...ci sarà probabilmente un nuovo rilascio un giorno di questi*. JWM usa all'incirca 5 MB di memoria in condizioni operative normali. All'inizio del 2009, la dimensione della versione presente nei [repository ufficiali di Arch Linux](/index.php/Official_repositories "Official repositories") è inferiore ai 76 KB (confronto con [dwm](/index.php/Dwm "Dwm") che è sotto i 17 KB) e sotto i 171 KB una volta installato (confronto con dwm che occupa 68 KB).Una versione minimale compilata consuma approssimativamente 136 KB di spazio su disco e occupa al di sotto di 1500 KB di memoria ram.

JWM è generalmente considerato come il più leggero e veloce window manager disponibile per X11 ed è il window manager predefinito per distribuzioni come [Puppy Linux](http://www.puppylinux.org/) e [Damn Small Linux](http://damnsmalllinux.org/). Numerose opzioni permettono layout di grande flessibilità. Alcune tra le maggiori peculiarità di JWM includono la semplicità e facilità di configurazione (in un singolo file [XML](https://en.wikipedia.org/wiki/XML "wikipedia:XML")), supporto nativo per le personalizzazioni di pannelli e bottoni e il modo in cui è stata integrata una dock sul desktop.

 Wingbermuehle, Joe. <u>News</u>. 06 Sep. 2008\. 11 Feb. 2009 <[http://joewing.net/index.shtml](http://joewing.net/index.shtml)>.

## Contents

*   [1 Installazione dei pacchetti](#Installazione_dei_pacchetti)
*   [2 Avviare JWM](#Avviare_JWM)
*   [3 Configurazione](#Configurazione)
    *   [3.1 Creare ~/.jwmrc](#Creare_.7E.2F.jwmrc)
    *   [3.2 Panoramica impostazioni](#Panoramica_impostazioni)
        *   [3.2.1 <Comandi avvio>](#.3CComandi_avvio.3E)
        *   [3.2.2 <Programmi>](#.3CProgrammi.3E)
        *   [3.2.3 <Menu>](#.3CMenu.3E)
        *   [3.2.4 <RootMenu>](#.3CRootMenu.3E)
        *   [3.2.5 <Gruppi>](#.3CGruppi.3E)
            *   [3.2.5.1 Window Class](#Window_Class)
        *   [3.2.6 <TrayButton>](#.3CTrayButton.3E)
        *   [3.2.7 <Swallow>](#.3CSwallow.3E)
        *   [3.2.8 <Vassoio>](#.3CVassoio.3E)
        *   [3.2.9 <Tasti>](#.3CTasti.3E)
        *   [3.2.10 <Include>](#.3CInclude.3E)
        *   [3.2.11 <Comandi di Riavvio>](#.3CComandi_di_Riavvio.3E)
        *   [3.2.12 <Comando di spegnimento>](#.3CComando_di_spegnimento.3E)
    *   [3.3 Verificare eventuali modifiche di configurazione](#Verificare_eventuali_modifiche_di_configurazione)
    *   [3.4 Additional Troubleshooting](#Additional_Troubleshooting)
*   [4 Suggerimenti utili](#Suggerimenti_utili)
    *   [4.1 Ulteriori Applicazioni](#Ulteriori_Applicazioni)
    *   [4.2 Xinitrc applicazioni d'avvio](#Xinitrc_applicazioni_d.27avvio)
    *   [4.3 Migliorare il contrasto <Tasklist>](#Migliorare_il_contrasto_.3CTasklist.3E)
    *   [4.4 Gestione energia](#Gestione_energia)
    *   [4.5 Logout e Refresh](#Logout_e_Refresh)
        *   [4.5.1 Riavvio e Spegnimento](#Riavvio_e_Spegnimento)
    *   [4.6 Compilazione minimale personalizzata](#Compilazione_minimale_personalizzata)
        *   [4.6.1 Minimal PKGBUILD Example](#Minimal_PKGBUILD_Example)
    *   [4.7 Suggerimenti compilazione minimale font](#Suggerimenti_compilazione_minimale_font)
    *   [4.8 Supporto Tiling manuale](#Supporto_Tiling_manuale)
*   [5 Rimozione pacchetti](#Rimozione_pacchetti)
*   [6 Ulteriori risorse](#Ulteriori_risorse)

## Installazione dei pacchetti

[jwm](https://www.archlinux.org/packages/?name=jwm) è disponibile su [official Arch Linux (community/X11) repository](/index.php/Official_repositories "Official repositories").

Installare l'ultima versione di JWM:

```
# pacman -S jwm

```

**Attenzione:** La recente snapshots SVN(e.g. 500) have migrated to Mod key masks (e.g. H to 4).

## Avviare JWM

Lanciando il programma xinit per avviare il server X ed il client JWM:

```
$ xinit /usr/bin/jwm

```

In alternativa includere la voce appropriata (es. `/usr/bin/jwm` o `exec /usr/bin/jwm` nel file [~/.xinitrc](/index.php/Xinitrc_(Italiano) "Xinitrc (Italiano)"). Consultare [avviare il server X al boot](/index.php/Start_X_at_boot_(Italiano) "Start X at boot (Italiano)") per ulteriori informazioni.

# Configurazione

### Creare ~/.jwmrc

Coerentemente con i principi di [The Arch Way](/index.php/The_Arch_Way_(Italiano) "The Arch Way (Italiano)"), il look & feel, oltre che le funzioni del desktop JWM vengono controllati da un unico file di configurazione: `~/.jwmrc`

Un semplice file di configurazione viene installato al momento dell'installazione ed è localizzabile in `/etc/system.jwmrc`. Il file {Filename|~/.jwmrc}} deve essere creato dall'utente:

```
$ touch `~/.jwmrc`

```

o

```
$ cp -i `/etc/system.jwmrc` `~/.jwmrc`

```

Tutto ciò che segue da questo punto in poi è configurare l'ambiente editando il file basato su XML `.jwmrc`.

*   [JWM Configuration](http://joewing.net/programs/jwm/config.shtml) specifica la lista completa di tags, attributi e valori disponibili per JWM.

**Note:** Il contenuto aggiornato della Configurazione di JWM è basato sull'ultima snapshot SVN e potrebbe non riflettere le opzioni disponibili nella versione presente.

### Panoramica impostazioni

#### <Comandi avvio>

*   Carica e aggancia [Parcellite](http://parcellite.sourceforge.net/) come [demone](http://en.wikipedia.org/wiki/Daemon_(computer_software)) in background quando JWM viene avviato:

```
 <StartupCommand>parcellite -d</StartupCommand>

```

*   Collega e aggancia a [urxvtd](/index.php/Rxvt-unicode "Rxvt-unicode") [daemon](http://en.wikipedia.org/wiki/Daemon_(computer_software)) al `$DISPLAY` corrente quando viene avviato JWM

```
 <StartupCommand>urxvtd -q -o -f</StartupCommand>

```

*   Rimozione ricorsiva forzata delle cartelle come misura di carattere generale di pulizia della vostra sessione quando si avvia JWM:

```
<StartupCommand>rm -rf $HOME/.adobe $HOME/.cache $HOME/.local/share/Trash $HOME/.macromedia $HOME/.recently-used.xbel $HOME/.Xauthority</StartupCommand>

```

*   Abilitare il controllo energetico [DPMS](/index.php/DPMS "DPMS") (Energy Star) su un monitor con indirizzo 0:0 dopo 900 secondi di inattività dall'avvio di JWM:

```
<StartupCommand>xset -display :0.0 dpms 0 0 900</StartupCommand>

```

**Note:** Lanciare il comando `xdpyinfo` (incluso nel pacchetto [xorg-utils](https://www.archlinux.org/packages/?name=xorg-utils)) per rilevare l'esatto nome del vostro display in uso.

#### <Programmi>

*   Avviare [Thunar](/index.php/Thunar "Thunar") in una cartella specifica

```
<Program label="Thunar">thunar ~/Desktop</Program>

```

*   Collegarsi tramite interfaccia web al server [CUPS](http://www.cups.org/) usando l'applicazione web preferita ([xdg-open](http://portland.freedesktop.org/xdg-utils-1.0/xdg-open.html)) :

```
<Program label="CUPS Printing">xdg-open [http://localhost:631](http://www.cups.org/articles.php?L274)</Program>

```

*   Iconifica ed avvia [FileZilla](http://filezilla-project.org/) con l'avvio di Site Manager

```
<Program icon="filezilla.png">filezilla -s</Program>

```

#### <Menu>

*   Creare dei contenitori per una lista di programmi addizionali e visualizzarli come sotto-menu all'interno di `<RootMenu>`

```
<Menu label="Sample">
  <Program label="Xfburn">xfburn -d</Program>
  <Program label="urxvt Client">urxvtc</Program>
</Menu>

```

```
<Etichetta menu="Example">
  <Program label="Opera">opera -nolirc -nomail </Program>
  <Program label="Writer">/opt/openoffice.org3/program/swriter -nologo</Program>
</Menu>

```

#### <RootMenu>

*   Creare un contenitore del menu visualizzando `etichetta="Test"` di `altezza="24"` pixels e vincolato dal tasto sinistro del mouse `onroot="1"` sotto `<RootMenu>`

```
<RootMenu labeled="true" label="Test" height="24" onroot="1">
    <Program label="Thunar">thunar ~/Desktop</Program>
    <Program label="CUPS Printing">xdg-open [http://localhost:631](http://localhost:631)</Program>
    <Program icon="filezilla.png">filezilla -s</Program>
  <Menu label="Sample">
    <Program label="Xfburn">xfburn -d</Program>
    <Program label="urxvt Client">urxvtc</Program>
  </Menu>
  <Menu label="Example">
    <Program label="Opera">opera -newprivatetab -noargb -nolirc -nomail </Program>
    <Program label="Writer">/usr/lib/openoffice.org3/program/swriter -nologo</Program>
  </Menu>
</RootMenu>

```

*   Creare un contenitore *nidificato* per il menu senza etichetta, di `altezza="32"` pixels e vincolato dal tasto destro del mouse `onroot="3"` sotto `<RootMenu>`

```
<RootMenu height="32" onroot="3">
    <Program label="Thunar">thunar ~/Desktop</Program>
    <Program label="CUPS Printing">xdg-open [http://localhost:631](http://localhost:631)</Program>
    <Program icon="filezilla.png" label="FileZilla">filezilla -s</Program>
  <Menu label="Sample">
    <Program label="Xfburn">xfburn -d</Program>
    <Program label="urxvt Client">urxvtc</Program>
  <Menu label="Example">
    <Program label="Opera">opera -newprivatetab -noargb -nolirc -nomail </Program>
    <Program label="Writer">/usr/lib/openoffice.org3/program/swriter -nologo</Program>
  </Menu>
  </Menu>
</RootMenu>

```

#### <Gruppi>

*   Conservare della spazio sul pannello non visualizzando `Squeeze` e `Xarchiver` dentro le `<Tasklist>`

```
<Group>
  <Class>Squeeze</Class>
  <Class>Xarchiver</Class>
    <Option>nolist</Option>
</Group>

```

*   Avviare sempre `Firefox` massimizzato sul `desktop:2` senza la barra del titolo

```
<Group>
  <Class>Firefox</Class>
    <Option>maximized</Option>
    <Option>desktop:2</Option>
    <Option>notitle</Option>
</Group>

```

##### Window Class

L'utility [xprop](http://www.xfree86.org/current/xprop.1.html) può gestire le proprietà delle finestre e dei caratteri in un server X.

*   Impostare xprop per visualizzare il nome della classe della finestra di una applicazione:

```
xprop WM_CLASS 

```

*   Fare clic sulla finestra dell'applicazione desiderata per visualizzare il nome della classe della finestra:

```
WM_CLASS(STRING) = "urxvt", "URxvt"

```

xprop è parte del pacchetto[xorg-utils](https://www.archlinux.org/packages/?name=xorg-utils) reperibile nel repositorio [extra] di Arch Linux.

```
# pacman -S xorg-utils

```

#### <TrayButton>

*   Creare un pannello `<TrayButton>` visualizzando l' `etichetta="Pattern"` che lancia il `root:1` menu

```
<TrayButton label="Pattern">root:1</TrayButton>

```

#### <Swallow>

*   Integrare `<Swallow>` nel vassoio il programma il cui nome è `name=wicd-gtk` e permettergli di eseguire il comando `wicd-gtk`

```
<Swallow name="wicd-gtk">
  wicd-gtk
</Swallow>

```

#### <Vassoio>

*   Creare un pannello `<Tray>` di `altezza="24"` pixels offset `x="0"` pixels dalla parte sinistra dello schermo `y="0"` ed in alto. Visualizzare senza il pannello:

1.  Un menu `<TrayButton>` che mostra il `root:1` menu.
2.  Una `<TaskList/>` che mostra applicazioni in esecuzione nel desktop corrente.
3.  Una `<TrayButton>` con il testo `label="X"` che minimizza le finestre aperte per mostrare il desktop.
4.  Un desktop virtuale `<Pager/>` per visualizzare le aree di lavoro disponibili.
5.  L'integrazione `<Swallow>` dell'applet di rete [Wicd](/index.php/Wicd_(Italiano) "Wicd (Italiano)").
    1.  É attualmente raccomandato impostare `wicd-gtk` con il tag <StartupCommand>.
6.  Per le applicazioni supportate, un'icona per l'area di sistema dei programmi `<Dock/>`.
7.  Un orologio `<Clock>` che visualizza data e ora in uno specifico formato.
    1.  Consultare la pagina[Man](https://en.wikipedia.org/wiki/Man_page "wikipedia:Man page") `strftime` per le specifiche sul formato e sul carattere della data e ora.

```
<Tray x="0" y="0" height="24">
  <TrayButton label="Pattern">root:1</TrayButton>
  <TaskList/> 
  <TrayButton label="X">showdesktop</TrayButton>
  <Pager/>
  <Swallow name="wicd-gtk">
    wicd-client
  </Swallow>
  <Dock/>
  <Clock format="%a %b %d %l:%M %p"></Clock>
</Tray>

```

#### <Tasti>

*   Vincolare il tasto `F1` al lancio e visualizzazione del menu `root:3`

```
<Key key="F1">root:1</Key>

```

*   Vincolare la conbinazione di tasti `Super+l` per bloccare il monitor ([XScreenSaver](http://www.jwz.org/xscreensaver/))

```
<Key mask="S" key="l">exec:xscreensaver-command -lock</Key>

```

**Note:** Lanciare il comando `xev` (contenuto nel pacchetto [xorg-utils](https://www.archlinux.org/packages/?name=xorg-utils)) per visualizzare l'output standard è il suo contenuto alla pressione di un tasto.

#### <Include>

*   Elaborare configurazioni di file `<Include>` per facilitare controllo e manutenzione

```
<Key key="F1">root:1</Key>
<Include>./.jwmrc-super-hyper-keys</Include> 
<Key mask="S" key="l">exec:xscreensaver-command -lock</Key>

```

*   Contenuto di un esempio `~/.jwmrc-super-hyper-keys`

```
<Key mask="PH" key="t">exec:thunderbird -addressbook</Key>
<Key mask="PH" key="h">exec:htop -d 10 -u USER --sort-key PERCENT_MEM</Key>
<Key mask="PH" key="c">exec:catfish --hidden --path=/usr</Key>

```

#### <Comandi di Riavvio>

*   Chiamare [sync](http://en.wikipedia.org/wiki/Sync_(Unix)) per svuotare il buffer del file system prima di smontare tutti i volumi montati con [TrueCrypt](/index.php/TrueCrypt "TrueCrypt") quando l'utente si disconnette dalla sessione X corrente:

```
<RestartCommand>sync; truecrypt -d</RestartCommand>

```

*   L'oggetto `<<RestartCommand>`< implementa o può prendere il posto di `$HOME/.bash_logout` per gli utenti che lavorano in una ambiente X.

#### <Comando di spegnimento>

*   Forzare ricorsivamente la rimozione del contenuto della cartella `Trash` quando si spegne JWM

```
 <ShutdownCommand>rm -rf ~/.local/share/Trash/*</ShutdownCommand>

```

**Note:** `<ShutdownCommand>` non sembra comportarsi come previsto quando si utilizzano i comandi `dbus-send`, `Shutdown` o `Stop` .

### Verificare eventuali modifiche di configurazione

```
$ jwm -p

```

Eseguire l'utilità di controllo dei file di configurazione originali di JWM restituendo errori di sintassi (Inclusi i relativi numeri di linea ) nei file di configurazione, nel caso ce ne siano. Se la sintassi è corretta e il file di configurazione è ritenuto correttamente contrassegnato , non verrà restituito alcun codice errato. Cambiamenti nel file di configurazione sono disponibili immediatamente dopo il riavvio, o il refresh di JWM con il comando `<Restart/>`. Non c'è bisogno di riavviare il server X per applicare le modifiche. Il comando `<Restart>` è disponibile agli utenti per l'accesso al menu root iniziale. **Si raccomanda agli utenti di usare questo strumento quando si eseguono cambiamenti di configurazione** al fine di garantire la riuscita degli aggiornamenti ed un ambiente stabile.

### Additional Troubleshooting

Se non si è loggati e non si sta lavorando su `tty1`, la combinazione di tasti `Ctrl+Alt+F1` vi permetterà di rivedere a video i messaggi standard e gli errori. Consultate la pagina MAN del comando `script` per i dettagli di come creare un typescript di quello che si vuole visualizzare sul terminale.

# Suggerimenti utili

### Ulteriori Applicazioni

*   [pal](http://palcal.sourceforge.net/) può essere lanciato con `<Clock>` per implementare il supporto del calendario e della lista degli eventi e delle cose da fare.

```
<Clock format="%a %b %d %l:%M %p">xterm -hold -e pal</Clock>

```

*   [Orage](http://www.xfce.org/projects/orage/) può essere eseguito in JWM `<Clock>` per fornire funzioni di calendario, eventi, caratteristiche.
*   [slock](http://tools.suckless.org/slock) può essere associato a `<Program>` e/o `<Key>` per fornire una soluzione leggere per bloccare lo schermo in X.
*   [Parcellite](http://parcellite.sourceforge.net/) può essere integrato nel vassoio come un leggero [X11](http://en.wikipedia.org/wiki/X_Window_System) gestore per gli appunti.
*   [Conky](/index.php/Conky "Conky") può venir eseguito con `<StartupCommand>` per la visualizzazione di molti tipi di informazioni sul sistema (es. batteria, spazio su disco, ram, cpu, etc).
*   [PCMan File Manager](http://pcmanfm.sourceforge.net/) Si può usare per gestire i file ed il desktop. Il vantaggio di PCMan File Manager è la leggerezza integrata ad un gestore potente come altri più blasonati.
*   [Xfce Desktop Manager](http://www.xfce.org/projects/xfdesktop/) (o xfdesktop) Altra alternativa alla gestione del desktop. Per aggirare il problema di ridisegnare xfdesktop sulla finestra principale del desktop di Conky :

1.  Consultare le [FAQ di Conky](http://conky.sourceforge.net/faq.html) per soluzioni alternative in `~/.conkyrc`
2.  Creare un `<Group>` Conky e specificare i seguenti tag `<Option>` in `~/.jwmrc`

```
<Group>
<Class>Conky</Class>
<Option>nolist</Option>
<Option>noborder</Option>
<Option>notitle</Option>
<Option>sticky</Option>
</Group>

```

### Xinitrc applicazioni d'avvio

Le applicazioni d'avvio possono venir eseguite al di fuori di `<StartupCommand>` includendo le opzioni appropriate in `~./xinitrc`

 `~./xinitrc` 
```

#!/bin/bash
/usr/bin/parcellite -d &
/usr/bin/Thunar --daemon &
/usr/bin/urxvtd -q -f -o &
/usr/bin/xcalib -d :0 /usr/share/color/icc/P221W-Native.icc &
/usr/bin/nvidia-settings -a GPUOverclockingState=1 -a GPU2DClockFreqs=640,655 -a GPU3DClockFreqs=640,655 &
/usr/bin/setxkbmap -option terminate:ctrl_alt_bksp &
export OPERAPLUGINWRAPPER_PRIORITY=0
export OPERA_KEEP_BLOCKED_PLUGIN=0
exec /usr/bin/jwm

```

### Migliorare il contrasto <Tasklist>

Cambiare le impostazioni predefinite `<Tasklist>` per migliorare il contrasto allo stile di default `<MenuStyle>` abilitando `<WindowStyle>`

```
<TaskListStyle>
  ~~<ActiveForeground>black</ActiveForeground>~~
  ~~<ActiveBackground>gray90:gray70</ActiveBackground>~~
</TaskListStyle>

```

```
<TaskListStyle>
  <ActiveForeground>white</ActiveForeground>
  <ActiveBackground>#70849d:#2e3a67</ActiveBackground>
</TaskListStyle>

```

### Gestione energia

Gli eventi della gestione energetica possono essere eseguiti con i tag `<Key>` e/o `<Program>`

### Logout e Refresh

`<Exit/>` (Logout) è il comando del menu per uscire correttamente dalla sessione di X.
`<Restart/>` (Refresh) è il comando del menu che reinizializza la configurazione dei file e aggiorna i menu e i vincoli da tastiera.
`<Restart/>` e `<Exit/>` si trovano nei tasti modificati `Ctrl+Alt` seguendo la sintassi d'esempio sotto:

```
<Key mask="CA" key="r">exec:jwm -restart</Key>
<Key mask="CA" key="e">exec:jwm -exit</Key>

```

#### Riavvio e Spegnimento

Un sistema con [sudo](/index.php/Sudo_(Italiano) "Sudo (Italiano)") installato e propriamente configurato può essere riavviato con le opzioni di menu `Restart` e `Poweroff`.

```
<Program label="Restart">sudo reboot</Program>
<Program label="Poweroff">sudo poweroff</Program>

```

Consultare [ArchWiki entry regarding allowing users to shutdown](/index.php/Allow_users_to_shutdown "Allow users to shutdown") per ulteriori informazioni.

**Note:** Gli utenti che vogliono spegnere completamente il sistema, `poweroff` o `shutdown -P now,` è preferibile a `shutdown -h now` perchè non da luogo ad eventuali dubbi sulle intenzioni dell'utente tramite il comando.

### Compilazione minimale personalizzata

Un incremento di reattività delle interfacce grafiche si può ottenere non usando le icone dei menu e disabilitando l'uso dei [Xft](http://en.wikipedia.org/wiki/Xft) fonts. Un ulteriore guadagno si può ottenere rimuovendo il supporto alle librerie esterne con una compilazione personalizzata. Si avrà inoltre una riduzione di assorbimento delle risorse del sistema. Una compilazione minima con il supporto Xft e usando i font Xft allocca circa tra 3 MB e 1.5 MB di memoria. La stessa compilazione senza il supporto Xft ne occupa rispettivamente tra 1.5 MB e 1.2 MB. Consultare la pagina [Arch Build System](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)") per ulteriori informazioni.

#### Minimal PKGBUILD Example

 `PKGBUILD` 
```
pkgname=jwm
pkgver=2.0.1
pkgrel=100
pkgdesc="A lightweight window manager for the X11 Window System"
arch=('i686' 'x86_64')
url="http://joewing.net/programs/jwm/"
license=('GPL2')
depends=('libx11')
backup=('etc/system.jwmrc')
source=(http://joewing.net/programs/jwm/releases/jwm-$pkgver.tar.bz2)
md5sums=('48f323cd78ea891172b2a61790e8c0ec')

build() {
  cd ${srcdir/${pkgname}-${pkgver}

  ./configure --disable-confirm --disable-icons --disable-png  \ 
  --disable-xpm --disable-jpeg --disable-fribidi --disable-xinerama  \
  --disable-shape --disable-xft --disable-xrender --disable-debug  \ 
  --prefix=/usr --sysconfdir=/etc
  make
  make BINDIR=$pkgdir/usr/bin \
       MANDIR=$pkgdir/usr/share/man \
       SYSCONF=$pkgdir/etc install
}

```

### Suggerimenti compilazione minimale font

```
<WindowStyle>
<Font>-*-fixed-*-r-*-*-10-*-*-*-*-*-*-*</Font>

<TaskListStyle>
<Font>-*-fixed-*-r-*-*-13-*-*-*-*-*-*-*</Font>

<TrayStyle>
<Font>-*-fixed-*-r-*-*-13-*-*-*-*-*-*-*</Font>

```

*   Consultare la pagina *Man* `xfontsel` e l'articolo [X Logical Font Description](https://en.wikipedia.org/wiki/X_logical_font_description "wikipedia:X logical font description") per ulteriori dettagli e le descrizioni del modello.

### Supporto Tiling manuale

Il supporto al tiling può essere aggiunto a JWM usando lo script in python [Poor Man's Tiling Window Manager](http://github.com/TheWanderer/poor-man-s-tiling-window-manager/tree/master). Supponendo che `manage.py` is located in a command directory as part of the local `PATH`, varie azioni di tiling possono essere vincolate a tastiera seguendo l'esempio sotto:

```
<Key mask="H" key="Up">exec:manage.py swap</Key>
<Key mask="H" key="Down">exec:manage.py cycle</Key>
<Key mask="H" key="Left">exec:manage.py left</Key>
<Key mask="H" key="Right">exec:manage.py right</Key>

```

**Note:** Run the `env` command to list the modified environments of the current user.

# Rimozione pacchetti

Per rimuovere il pacchetto JWM conservandone dipendenze e file di configurazione:

```
# pacman -R jwm

```

Per rimuovere il pacchetto JWM e i file di configurazione conservandone le dipendenze:

```
# pacman -Rn jwm

```

Per rimuovere il pacchetto JWM e le dipendenze non richieste da altri pacchetti conservandone i file di configurazione:

```
# pacman -Rs jwm

```

Per rimuovere il pacchetto JWM, i file di configurazione e le dipendenze non richieste da altri pacchetti:

```
# pacman -Rns jwm

```

**Note:** Pacman non rimuove file di configurazione al di fuori di quelli predefiniti creati durante l'installazione dei pacchetti. Ciò include `~/.jwmrc`
}

# Ulteriori risorse

*   [Joe's Window Manager](http://joewing.net/programs/jwm/index.shtml) - Sito ufficiale

Esempi di cosa è possibile realizzare con un po' di creativtà possono essere trovati qui:

*   * [PuppyLinux : JoesWindowManager](http://puppylinux.org/wikka/JoesWindowManager)
*   [Puppy Linux JWM Themes Exchange](http://www.murga-linux.com/puppy/viewtopic.php?t=23260)