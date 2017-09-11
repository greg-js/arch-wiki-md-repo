Articoli correlati

*   [Ambienti desktop](/index.php/Desktop_Environment_(Italiano) "Desktop Environment (Italiano)")
*   [Gestori delle sessioni](/index.php/Display_Manager_(Italiano) "Display Manager (Italiano)")
*   [Gestori delle finestre](/index.php/Window_Manager_(Italiano) "Window Manager (Italiano)")

Tratto dalla [documentazione di Enlightenment](http://trac.enlightenment.org/e/wiki/Enlightenment):

	*L'ambiente di lavoro Enlightenment fornisce un window manager efficiente e mozzafiato basato sul Enlightenment Foundation Libraries (EFL) insieme ad altri componenti del desktop essenziali, come un file manager, le icone del desktop e widget. Vanta un livello senza precedenti di capacità di eseguire temi grafici, pur essendo in grado di eseguirli con hardware più vecchio o su dispositivi embedded.*

## Contents

*   [1 Enlightenment](#Enlightenment)
    *   [1.1 Installazione](#Installazione)
        *   [1.1.1 Da AUR](#Da_AUR)
    *   [1.2 Avviare enlightenment](#Avviare_enlightenment)
        *   [1.2.1 Log-in grafico](#Log-in_grafico)
        *   [1.2.2 Avviare enlightenment manualmente](#Avviare_enlightenment_manualmente)
    *   [1.3 Configurazione](#Configurazione)
        *   [1.3.1 Rete](#Rete)
        *   [1.3.2 Polkit agent](#Polkit_agent)
        *   [1.3.3 Integrazione con Gnome Keyring](#Integrazione_con_Gnome_Keyring)
    *   [1.4 Temi](#Temi)
    *   [1.5 Moduli e gadgets](#Moduli_e_gadgets)
        *   [1.5.1 Moduli "Extra"](#Moduli_.22Extra.22)
    *   [1.6 Risoluzione dei Problemi](#Risoluzione_dei_Problemi)
        *   [1.6.1 Compositing](#Compositing)
        *   [1.6.2 Caratteri illeggibili](#Caratteri_illeggibili)
*   [2 Enlightenment DR16](#Enlightenment_DR16)
    *   [2.1 Installare E16](#Installare_E16)
    *   [2.2 Configurazione di base](#Configurazione_di_base)
        *   [2.2.1 Immagini di sfondo](#Immagini_di_sfondo)
        *   [2.2.2 Script di Avvio/Riavvio/Stop](#Script_di_Avvio.2FRiavvio.2FStop)
        *   [2.2.3 Composite](#Composite)
*   [3 Vedi anche](#Vedi_anche)

## Enlightenment

Enlightenment comprende sia il [window manager](/index.php/Window_manager_(Italiano) "Window manager (Italiano)") che le librerie Enlightenment Foundation Libraries ( EFL), le quali forniscono ulteriori funzionalità desktop dell'ambiente, così come una serie di strumenti, come un toolkit, e gli oggetti astratti. E 'stato in fase di sviluppo dal 2005, ma nel mese di febbraio 2011 le principali librerie EFL videro la loro prima versione stabile 1.0\.

### Installazione

Enlightenment può essere [installato](/index.php/Pacman "Pacman") con il pacchetto [enlightenment](https://www.archlinux.org/packages/?name=enlightenment) , disponibile nei [depositi ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

Si potrebbe anche voler installare [terminology](https://www.archlinux.org/packages/?name=terminology), che è un emulatore di terminale basato su EFL, e si integra bene con Enlightenment.

#### Da AUR

**Attenzione:** Alcuni di questi PKGBUILD utilizzano codice di sviluppo instabile. Usarli a proprio rischio.

I PKGBUILD di sviluppo che scaricheranno e installeranno il codice di sviluppo più recenti sono disponibili su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") come [enlightenment-git](https://aur.archlinux.org/packages/enlightenment-git/) e le sue dipendenze.

Le applicazioni seguenti sono basate su EFL, la maggior parte di loro è in fase iniziale di sviluppo e non ancora stati rilasciati stabilmente:

*   [ecrire-git](https://aur.archlinux.org/packages/ecrire-git/) – Ecrire text editor
*   [emprint-git](https://aur.archlinux.org/packages/emprint-git/) – Emprint screenshot tool
*   [enjoy-git](https://aur.archlinux.org/packages/enjoy-git/) – [Enjoy](https://trac.enlightenment.org/e/wiki/Enjoy) music player
*   [eperiodique](https://aur.archlinux.org/packages/eperiodique/) - [Eperiodique](http://eperiodique.sourceforge.net/) periodic table viewer
*   [ephoto-git](https://aur.archlinux.org/packages/ephoto-git/) – [Ephoto](https://trac.enlightenment.org/e/wiki/Ephoto) picture viewer
*   [epour](https://aur.archlinux.org/packages/epour/) & [epour-git](https://aur.archlinux.org/packages/epour-git/) – Epour Bittorrent client
*   [equate-git](https://aur.archlinux.org/packages/equate-git/) – Equate calculator
*   [eruler-git](https://aur.archlinux.org/packages/eruler-git/) – Eruler on-screen ruler and measurement tools
*   [efbb-git](https://aur.archlinux.org/packages/efbb-git/) – Escape from Booty Bay angry birds style game
*   [elemines-git](https://aur.archlinux.org/packages/elemines-git/) – [Elemines](http://elemines.sourceforge.net/) minesweeper style game
*   [espionage-git](https://aur.archlinux.org/packages/espionage-git/) – Espionage D-Bus inspector
*   [ev-git](https://aur.archlinux.org/packages/ev-git/) – ev simple picture viewer
*   [eve-git](https://aur.archlinux.org/packages/eve-git/) – [Eve](https://trac.enlightenment.org/e/wiki/Eve) web browser
*   [rage-git](https://aur.archlinux.org/packages/rage-git/) - Rage video player

### Avviare enlightenment

#### Log-in grafico

Basta scegliere la sessione *enlightenment* dal proprio [gestore delle sessioni](/index.php/Display_manager_(Italiano) "Display manager (Italiano)") preferito.

**Entrance**

**Attenzione:** Entrance è altamente sperimentale, e non ha un adeguato sostegno a systemd. Usatelo a vostro rischio e pericolo.

Per Enlightenment è ora disponibile un nuovo display manager chiamato Entrance, che è disponibile su AUR tramite il pacchetto [entrance-git](https://aur.archlinux.org/packages/entrance-git/). Entrance è piuttosto sofisticato e la sua configurazione è controllata dal file `/etc/entrance.conf`. Per utilizzare Entrance abilitare il servizio `entrance.service` [utilizzando systemd](/index.php/Systemd#Using_units "Systemd").

#### Avviare enlightenment manualmente

Se preferite avviare enlightenment manualmente da console, aggiungere la seguente linea al vostro file `~/.xinitrc`:

 `~/.xinitrc` 
```
 exec enlightenment_start

```

Dopo di che Enlightenment può essere lanciato digitando `startx`. Per i dettagli, vedere [xinitrc](/index.php/Xinitrc_(Italiano) "Xinitrc (Italiano)").

### Configurazione

Enlightenment ha un sistema di configurazione sofisticato che si può accedere dal sottomenu *Impostazioni* del menu principale.

#### Rete

**ConnMan**

Il gestore di rete predefinito di Enlightenment è [ConnMan](/index.php/Connman_(Italiano) "Connman (Italiano)"), che è reperibile nel [deposito ufficiale](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)") con il pacchetto [connman](https://www.archlinux.org/packages/?name=connman). Seguire le istruzioni presenti nella pagina [ConnMan](/index.php/Connman_(Italiano) "Connman (Italiano)"), per la sua configurazione.

Per la configurazione estesa con il modulo predefinito Enlightenment di Rete, si può anche installare EConnman ( disponibile in AUR come [econnman](https://aur.archlinux.org/packages/econnman/) o [econnman-git](https://aur.archlinux.org/packages/econnman-git/)), ed è associato come dipendenza.

**NetworkManager**

É possibile anche utilizzare [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) per gestire le proprie connessioni di rete.Seguire le istruzioni riportate sulla pagina [NetworkManager](/index.php/NetworkManager_(Italiano) "NetworkManager (Italiano)")

Per la sua configurazione. Potrebbe essere necessaria l'installazione del pacchetto [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) per essere facilitati sulla configurazione e scelta delle impostazioni.Si consiglia di aggiungerlo all'avvio della sessione, in modo ogni volta che si avvia Enlightenment appaia sulla barra delle applicazioni. Per fare questo andare in *Impostazioni > Pannello impostazioni > Applicazioni > Applicazioni per l'avvio > Sistema > Network*

#### Polkit agent

Enlightenment non ha un [agente di autenticazione polkit grafico](/index.php/Polkit#Authentication_agents "Polkit"), quindi se si vuole accedere ad alcune azioni privilegiate (ad esempio montare un filesystem su un dispositivo del sistema), è necessario installare uno , e autoavviarlo. Per questo si dovrebbe andare per *Impostazioni, Pannello - > Applicazioni - > Applicazioni d'avvio - > Sistema* e attivarlo.

#### Integrazione con Gnome Keyring

E ' possibile usare gnome-keyring in Enlightenment. Tuttavia, allo stato attuale vi è bisogno di un piccolo hack per farlo funzionare correttamente. In primo luogo si deve dire a Enlightenment di avviare automaticamente gnome-kering. Per questo si dovrebbe andare in *Impostazioni-Pannello->Applicazioni->Applicazioni di avvio* e attivare *certificato e memorizzazione delle chiavi*, *Agente password GPG*, *Agente di chiavi SSH* e *servizio di archiviazione Secret*.

Successivamente si dovrebbe modificare il file `~/.profile` e aggiungere quanto segue :

```
  if [ -n "$DESKTOP_SESSION" ];then 
     # No point to start gnome-keyring-daemon if ssh-agent is not up 
     if [ -n "$SSH_AGENT_PID" ];then 
         eval $(gnome-keyring-daemon --start) 
         export SSH_AUTH_SOCK export GPG_AGENT_INFO
         export GNOME_KEYRING_CONTROL
     fi
 fi

```

Questo dovrebbe esportare le variabili necessarie per la gestione delle chiavi al vostro prossimo login. Un ringraziamento particolare va a [[1]](http://dingyichen.wordpress.com/2013/11/20/properly-use-gnome-keyring-daemon-enlightenment-e-17-with-ssh-agent-support/) per aver torvato il sistema adatto per farlo funzionare.

Ulteriori informazioni su questo argomento li potete nell'articolo [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring").

### Temi

Sono disponibili diversi temi per personalizzare l'aspetto di Enlightenment e reperibili presso:

*   [exchange.enlightenment.org](http://exchange.enlightenment.org/theme)
*   [e17-stuff.org](http://www.e17-stuff.org/index.php?xcontentmode=7000)
*   [relighted.c0n.de](http://relighted.c0n.de/#100) per il tema di default in 200 colori diversi
*   [[2]](http://git.enlightenment.org/themes.enlightenment.org) (git clone il tema che ti piace, eseguire 'make' e si finisce con un file di tema .edj )
*   [packages.bodhilinux.com](http://packages.bodhilinux.com/bodhi/pool/stable/b/) ha una buona raccolta ( è necessario estrarre il file edj dal .deb; bsdtar può fare questo e fa parte dell'installazione base di ArchLinux). Un bel catalogo di anteprima può essere visto nel loro [wiki](http://art.bodhilinux.com/doku.php).

É possibile installare i temi (che sono in formato .edj) utilizzando la finestra di dialogo di configurazione del tema o spostandoli in `~/.E/e/themes`.

**Nota:** Enlightenment non fornisce un API stabile per la creazione dei temi e ci sono stati numerosi cambiamenti all'API dei temi nel corso degli anni, anche dopo che E17 è stato rilasciato. È improbabile che i temi non aggiornati regolarmente funzionino.

### Moduli e gadgets

	Module

	Nome usato in enlightenment in riferimento al codice "supportato" da un determinato gadget.

	Gadget

	Front-end o una interfaccia utente che dovrebbe aiutare gli utenti finali di Enlightenment in determinate azioni.

Molti moduli forniscono dei Gadgets che possono essere aggiunti al proprio desktop o sulla mensola (shelf). Alcuni moduli (come CPUFreq) forniscono solamente un singolo Gadget, mentre altri (come Composite) forniscono caratteristiche aggiuntive senza nessun gadgets. Si noti che alcuni gadgets (come ad esempio Systray) possono essere aggiunti solo nella mensola, mentre altri (come il gadget Moon) può essere aggiunto solo sul desktop.

#### Moduli "Extra"

**Attenzione:** Si tratta di moduli di terze parti e non ufficialmente supportato dagli sviluppatori di Enlightenment. Essi sono vengono prelevati direttamente dal ramo SVN, questo fa si che il codice può risultare sempre in sviluppo e possono o non possono funzionare in qualsiasi momento. Utilizzare a proprio rischio e pericolo.

Al di là dei moduli qui descritti, altri moduli *extra* sono disponibili su AUR, come parte di [e-modules-extra-git](https://aur.archlinux.org/packages/e-modules-extra-git/).

**Places**

Places è un gadget che ti aiuterà a navigare tra i file su diversi dispositivi che si potrebbero collegare al computer, come i telefoni, macchine fotografiche o altri dispositivi di memorizzazione diversi inseriti nella porta usb.

Disponibile come [places](https://aur.archlinux.org/packages/places/) oppure come [places-git](https://aur.archlinux.org/packages/places-git/).

**Nota:** Questo modulo non è più necessario per l'auto-montaggio dei dispositivi esterni in Enlightenment.

**Scale Windows**

Il modulo *Scale Windows*, che richiede che il compositing sia abilitato, aggiunge diverse funzionalità. L' effetto di scala finestre riduce tutte le finestre aperte e li porta tutti in vista. L'effetto "scale pager" effettua uno zoom in fuori e mostra tutti i desktop come un muro, come il plugin compiz expo. Entrambi possono essere aggiunti al desktop come un gadget o legati ad una combinazione di tasti, ad una combinazione del mouse o ad un bordo dello schermo.

A molti utenti piace cambiare la scorciatoia predefinita `ALT + Tab` usata per selezionare le finestre, a favore del di Scale Windows per selezionare una finestra. Per cambiare questa impostazione, andare su *Menu > Impostazioni > Pannello impostazioni > Input > Tasti*. Da qui è possibile impostare la combinazione di tasti desiderata.

Per sostituire la funzionalità del tasto di scelta rapida per la selezione delle finestre con Scale Windows, scorrere nel pannello a sinistra fino a trovare la sezione *ALT*, e selezionare `ALT + Tab`. Successivamente scorrere attraverso il pannello di destra fino a trovare la sezione "Scale Windows", e scegliere uno delle seguenti opzioni : *Select Next* oppure *Select Next (All)*, a seconda se si desidera vedere le finestre da un solo desktop corrente o da tutti i desktop e cliccare su *Apply* per salvare l'associazione.

Disponibile come [comp-scale-git](https://aur.archlinux.org/packages/comp-scale-git/).

**Engage**

Engage è una dock stile CairoDock/GLX-Dock sia per i lanciatori delle applicazioni che per le applicazioni aperte. Si richiede il compositing per essere attivato e dispone di controlli completi per la trasparenza, dimensioni, livelli di zoom, e altro ancora.

Disponibile come [engage-git](https://aur.archlinux.org/packages/engage-git/)

### Risoluzione dei Problemi

Se trovate alcuni comportamenti inaspettati, ci sono alcuni accorgimenti che si possono fare:

1.  provare a vedere se lo stesso comportamento persiste con il tema di default
2.  disattivare tutti i moduli di terze parti eventualmente installati
3.  fare un backup `~/.e` e rimuoverlo (e.s. `mv ~/.e ~/.e.back`).

Se sei sicuro di aver trovato un bug si prega di segnalarlo [direttamente agli sviluppatori](http://trac.enlightenment.org/e/report).

#### Compositing

Quando la configurazione risulta incasinato e la finestre delle impostazioni non può più essere visualizzata correttamente, la configurazione per il compositor può essere resettata dalla combinazione di tasti `Ctrl + Alt + Shift + Home`.

#### Caratteri illeggibili

Se i caratteri sono troppo piccoli e lo schermo è illeggibile, assicurarsi i seguenti pacchetti font sono installati. [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) e [ttf-bitstream-vera](https://www.archlinux.org/packages/?name=ttf-bitstream-vera) sono dei validi font.

È possibile impostare il ridimensionamento in *Impostazioni - > impostazioni del pannello - > Aspetto - > Scaling* .

## Enlightenment DR16

Il primo rilascio di sviluppo di Enlightenment DR16 è avvenuto nel 2000, e la versione 1.0 è stata rilasciata nel 2009\. In origine, il nome DR16 si riferiva alla versione 0.16 del progetto Enlightenment. Ora lo si trova semplicemente come "Enlightenment" nei repository di Arch, Si può affermare che è ancora oggi in fase di sviluppo. Regolarmente aggiornata dal suo sviluppatore Kim 'kwo' Woelders comprende l'uso del compositing, ombre e trasparenze. E16 ha conservato tutta la velocità originale, come quando fu presentato dal suo fondatore Carsten "Rasterman" Haitzler, ma con rifiniture moderne.

### Installare E16

Per installare [enlightenment16](https://www.archlinux.org/packages/?name=enlightenment16).

Enlightenment può risultare molto differente dagli altri gestori delle finestre, leggere `/usr/share/doc/e16/e16.html` dopo l'installazione per maggiori dettagli. La pagina manuale è [e16(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/e16.1) ed analizza solo le opzioni di avvio.

### Configurazione di base

La maggior parte dei file di configurazione di E16 risiede in `~/.e16` sotto forma di testo semplice, modificabili a piacimento. Essi includo anche il Menu.

I tasti di scelta rapida, possono essere modificati manualmente o tramite il programma *e16keyedit* reperibile come sorgenti dalla pagina [sourceforge](http://sourceforge.net/projects/enlightenment/) del progetto e16, o installando [e16keyedit](https://aur.archlinux.org/packages/e16keyedit/) da AUR.

#### Immagini di sfondo

Copiate l'immagine di sondo desiderata in `~/.e16/backgrounds/`

Premendo il tasto centrale del mouse od il tasto destro, in un punto qualsiasi del desktop, accedere al menu delle impostazioni e selezionate `/Desktop/Backgrounds/`.

Ogni nuova immagine sarà copiata nella cartella `~/.e16/backgrounds/` che aggiornerà automaticamente automaticamente la lista degli sfondi disponibili. Selezionate lo sfondo desiderato dal menu a discesa. All'interno della scheda appropriata nelle impostazioni globali di E16 è possibile regolare l'affiancamento dell'immagine di sfondo, il riempimento dello schermo e così via.

#### Script di Avvio/Riavvio/Stop

Create una cartella **Init** , **Start** e **Stop** in `~/.e16`: qualsiasi script .sh script inserito verrà eseguito all'avvio (se presente nella cartella Init), al riavvio (se presente nella cartella Start), o allo spegnimento (se presente nella cartella Stop); a condizione che siano stati resi eseguibili con il comando `chmod +x **yourscript.sh**` e abilitati tramite l'apposito menu /settings/session/ <enable scripts> raggiungibile premendo il tasto centrale del mouse. Esempi tipici sono l'inizializzazione di pulseaudio o del vostro gestore di rete preferito.

#### Composite

Ombre ed effetti di trasparenza sono abilitabili nella voce Composite nel menu /Setings, raggiungibile col tasto centrale del mouse o col tasto destro.

## Vedi anche

*   [Enlightenment Homepage](http://www.enlightenment.org/)
*   [Enlightenment Exchange](http://exchange.enlightenment.org/)
*   [Enlightenment Developer Documentation](http://docs.enlightenment.org/)
*   [Bodhi Guide to Enlightenment](http://www.bodhilinux.com/e17guide/e17guideEN/)
*   [E17-Stuff](http://www.e17-stuff.org/)
*   [DR16 download resource](http://sourceforge.net/projects/enlightenment/)
*   [Enlightenment users mail list](https://lists.sourceforge.net/lists/listinfo/enlightenment-users)
*   [Enlightenment developer mail list](https://lists.sourceforge.net/lists/listinfo/enlightenment-devel)
*   [irc://irc.freenode.net#e](irc://irc.freenode.net#e)