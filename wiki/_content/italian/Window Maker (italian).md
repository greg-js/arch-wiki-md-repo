Articoli correlati

*   [Window Manager (Italiano)](/index.php/Window_Manager_(Italiano) "Window Manager (Italiano)")

Windows Maker è un gestore delle finestre (WM = [Windows Manager](/index.php/Window_manager_(Italiano) "Window manager (Italiano)") per il il server X. È stato progettato per emulare NeXT GUI come un ambiente OpenStep-compatibile ed è caratterizzato da esigenze di bassa memoria e alta flessibilità. Essendo uno dei più leggeri WM è ben adattato per le macchine con modeste specifiche di prestazione.

## Contents

*   [1 Installazione](#Installazione)
    *   [1.1 Avviare Window Maker senza un display manager](#Avviare_Window_Maker_senza_un_display_manager)
    *   [1.2 Avviare Window Maker con un display manager](#Avviare_Window_Maker_con_un_display_manager)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Files](#Files)
    *   [2.2 Stili](#Stili)
*   [3 Dock](#Dock)
*   [4 Clip](#Clip)
*   [5 Dockapps](#Dockapps)
*   [6 Vassoio di sistema](#Vassoio_di_sistema)
*   [7 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [7.1 Le applicazioni non partono sempre](#Le_applicazioni_non_partono_sempre)
    *   [7.2 Non è possibile disabilitare lo *smooth* dei font](#Non_.C3.A8_possibile_disabilitare_lo_smooth_dei_font)
*   [8 Altre fonti](#Altre_fonti)

## Installazione

L'ultima release ufficiale è disponibile nel pacchetto [windowmaker](https://aur.archlinux.org/packages/windowmaker/) presso i [repositori ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

Per installare Window Maker:

 `# pacman -S windowmaker` 

Prima di avviare Window Maker è necessario spendere un pò di tempo per configurare GNUstep e le impostazioni predefinite di Window Maker. Creare una direcotory per le proprie impostazioni di Window Maker. Tradizionalmente so utilizza la cartella `$HOME/GNUstep`.

 `$ mkdir ~/GNUstep` 

Impostare la variabile `GNUSTEP_USER_ROOT` nella propria cartella di impostazioni GNUstep. É possibile impostare questa variabile direttamente in un file come ad esempio in `$HOME/.bashrc`.

```
export GNUSTEP_USER_ROOT="${HOME}/GNUstep"

```

Assicurarsi che limpostazione sia corretta, ad esempio effettuando un logout ed in seguito un login.

Avviare il programma di installazione di Window Maker per impostare del configurazioni predefinite.

 `$ wmaker.inst` 

### Avviare Window Maker senza un display manager

Una volta installato, creare o editare il file [~/.xinitrc](/index.php/~/.xinitrc "~/.xinitrc") aggiungendo quanto segue:

```
exec wmaker

```

Avviare Window Maker:

 `$ startx` 

### Avviare Window Maker con un display manager

Una volta installato il display manager desiderato, è necessario riavviarlo e si sarà in grado di selezionare una sessione di Window Maker.

Il pacchetto windowmaker installa un file .desktop file in `/usr/share/xsessions/wmaker.desktop` 

## Configurazione

### Files

Tutte le impostazioni per Window Maker possono essere trovate nella cartella `GNUSTEP_USER_ROOT`, nelle sotto cartelle `Default` e `Library`. Essi vengono salvate come semplici file di testo. Per modificare le impostazioni tramite interfazzia grafica potete utilizzare la `Preferences Utility` (`WPrefs`), oppure editarli a mano a seconda delle proprie esigenze.

*   `Defaults/WindowMaker` - Le impostazioni correnti di Window Maker.
*   `Defaults/WMGLOBAL`
*   `Defaults/WMRootMenu` - Il menu principale del desktop. Si usa un semplice formato di testo che può essere modificato manualmente. Per ulteriori dettagli, vedere la voce di menu *modifica* nell'applicazione *Utility Prefereces*
*   `Defaults/WMState` - Utilizzato per ripristinare la sessione di Window Maker.
*   `Defaults/WMWindowAttributes` - Da qui è possibile personalizzare le impostazioni individuali per le finestre e le applicazioni, come l'icona dell'applicazione o il titolo della barra. È inoltre possibile accedere a queste modifiche anche facendo clic destro su qualsiasi icona di applicazione o finestra e selezionando la voce "Attributes".
*   `Defaults/WPrefs` - Impostazioni per l'utilità delle preferenze.
*   `Library/Colors/`
*   `Library/Icons/` - Uno dei percorsi predefiniti dove Window Maker cerca le icone per le applicazioni. È possibile salvare le proprie icone personali qui e utilizzarle per cambiare gli attributi applicazione o una finestra.
*   `Library/WindowMaker/autostart` - Qui si possono aggiungere le applicazioni che si desidera avviare automaticamente quando si avvia Window Maker. Assicurarsi di eseguirle in background, utilizzando "&".
*   `Library/exitscript` - Come per l'avvio automatico, ma questa volta le applicazioni verranno lanciate all'uscita di Window Maker.
*   `Library/Backgrounds` - Uno dei percorsi predefiniti dove Window Maker cerca sfondi per il desktop.
*   `Library/Styles` - Uno dei percorsi predefiniti dove Window Maker cerca gli stili.

### Stili

Gli stili sono semplici file di testo nel quale sono indicate le impostazioni per cambiare l'aspetto di Window Maker. Sono molto simili come strutture al file `Defaults/WindowMaker`. Tutte le impostazioni presenti nel file dello stile verranno applicate al file `Defaults/WindowMaker`. Di seguito viene fornito un esempio di stile che imposta in Windows Maker i colori Blu e Grigio che richiamano i colori ufficiali di Arch Linux:

 `Arch.style` 
```
{
  FTitleBack = (solid, "#0088CC");
  FTitleColor = white;
  UTitleBack = (solid, "#333333");
  UTitleColor = "#999999";
  PTitleBack = (solid, "#333333");
  PTitleColor = "#999999";
  MenuTextBack = (solid, "#ECF2F5");
  MenuTextColor = black;
  IconTitleBack = "#333333";
  IconTitleColor = white;
  MenuTitleBack = (solid, "#0088CC");
  MenuTitleColor = white;
  HighlightTextColor = white;
  HighlightColor = "#333333";
  MenuDisabledColor = "#999999";
  ClipTitleColor = black;
  IconBack = (solid, "#ECF2F5");
  ResizebarBack = (solid, "#333333");
  MenuStyle = flat;
  WorkspaceBack = (solid, black);
  ClipTitleFont = "Arial:slant=0:weight=200:width=100:pixelsize=10";
  IconTitleFont = "Arial:slant=0:weight=80:width=100:pixelsize=9";
  LargeDisplayFont = "Arial:slant=0:weight=80:width=100:pixelsize=24";
  MenuTextFont = "Arial:slant=0:weight=80:width=100:pixelsize=12";
  MenuTitleFont = "Arial:slant=0:weight=200:width=100:pixelsize=12";
  WindowTitleFont = "Arial:slant=0:weight=200:width=100:pixelsize=12";
}

```

Gli stili possono anche essere modificati mediante l'applicazione *Preferences Utility*.

## Dock

Un dock è una funzionalità dell'interfaccia grafica di alcuni sistemi operativi che serve ad eseguire programmi e funzionalità del sistema e a passare agevolmente tra le applicazioni in esecuzione.

L'interfaccia utente di Mac OS X ha evoluto lo stile di interfaccia utente che utilizza Window Maker. C'è una *dock* che contiene le icone delle applicazioni che sono *bloccate* da parte dell'utente. Inoltre, può contenere piccole applicazioni speciali chiamate *dockapps*, che si spostano solo all'interno della dock stessa. Per impostazione predefinita, tutte le applicazioni eseguite in Window Maker avranno l'icona dell'applicazione nella dock, con la quale è possibile interagire per eseguire una nuova istanza di essa, nascondere e visualizzare tutte le finestre dell'applicazione, o uccidere l'istanza in esecuzione. L'icona non rappresenta una finestra. Invece, se si minimizza una finestra, una piccola icona che rappresenta la finestra apparirà sul desktop.

Dopo l'avvio di qualsiasi applicazione (per esempio, dalla riga di comando) l'icona viene visualizzata sul desktop. La si può aggiungere alla dock semplicemente selezionandola e trascinandola al suo interno. Per rimuovere l'icona dell'applicazione dalla dock, selezionare e trascinare fuori da essa l'icona dell'istanza. Si modificano le impostazioni, come la possibilità di avviare automaticamente un'applicazione quando si avvia Window Maker, facendo clic col pulsante destro del mouse sull'icona dell'applicazione nella Dock.

L'azione predefinita per attivare le icone delle applicazioni e le icone delle finestra è quella di fare un doppio clic su di loro. É possibile modificare questo comportamento ed impostare un singolo click per l'attivazione delle applicazioni o delle finestre.

## Clip

Il 'clip' è un pulsante che ha l'immagine di una graffetta. È possibile modificare il nome dell'area di lavoro corrente facendo clic destro sulla clip. È possibile cambiare le aree di lavoro facendo clic sulle frecce che si trovano sulla clip.

La clip offre, inoltre, una funzionalità simile alla dock. Le icone delle applicazioni che vengono aggiunte alla dock sono visibili su tutte le aree di lavoro, mentre le icone delle applicazioni che sono collegate al clip sono visibili esclusivamente sull'area di lavoro in cui sono stati aggiunti. Ciò consente di associare comodamente specifiche applicazione a specifiche aree di lavoro.

Fare doppio clic sulla clip per nascondere e visualizzare le icone delle applicazioni che sono collegati ad esso.

## Dockapps

Le Dockapps sono piccole applicazioni che girano all'interno della dock. Di solito sono utilizzate per mostrare informazioni di sistema. Le Dockapps più utilizzate presenti in [AUR](/index.php/AUR "AUR") includono:

*   [wmclockmon](https://aur.archlinux.org/packages/wmclockmon/) - Mostra ora e data.
*   [wmcpuload](https://aur.archlinux.org/packages/wmcpuload/) - Mostra lo stato e l'uso della CPU.
*   [wmnetload](https://aur.archlinux.org/packages/wmnetload/) - Mostra lo stato della rete. Esempio di utilizzo: `wmnetload -i eth0`
*   [wmdiskmon](https://aur.archlinux.org/packages/wmdiskmon/) - Mostra l'utilizzo dei dischi. Esempio di utilizzo: `wmdiskmon -p /dev/sda1 -p /dev/sda2`

Una raccolta di quasi tutte le dockapps possono essere trovate sul sito ufficiale dockapps, è possibile trovare il link in [Risorse aggiuntive](#Risorse_aggiuntive).

## Vassoio di sistema

Nativamente WindowMaker non include un vassoio di sistema, ma esistono varie soluzioni per poter avere un una nm-pllet o similare sul proprio desktop.

Il primo è **stalonetray** che prima della versione 0.8 non funzionava come un contenitore di dock in WindowMaker, ma bisognava usare Docker al suo posto. Inoltre NW è l'unico a crescere ed a funzionare in modo affidabile su WindowMaker, prima di quelle versioni.

Dalla versione 0.8 è stato incluso un supporto base per ma modalità *dockapp* in WindowMaker, e può essere abilitata attraverso l'opzione `--dockapp-mode wmaker`. Sono rischieste le seguenti opzioni: `--slot-size 32 --geometry 2x2 --parent-bg --scrollbars none`.

Esistono però altre soluzioni più semplici:

*   [wmsystray](https://aur.archlinux.org/packages/wmsystray/) : che facilità il lavoro per voi.
*   [wmsystemtray](https://aur.archlinux.org/packages/wmsystemtray/) : Non utilizza i bordi e dovrebbe funzionare anche su altri ambienti desktop.
*   [Peksystray](https://aur.archlinux.org/packages/Peksystray/) : piccolo vassoio di sistema (chiamato anche vassoio di notifiche) progettato per funzionare su tutti i window managers e *supporta il docking* per le applicazioni.

Peksystray fornisce una finestra dove le icone si aggiungono automaticamente a seconda delle richieste delle applicazioni. Entrambe le dimensioni della finestra e le dimensioni delle icone possono essere selezionate dall'utente. Se la finestra è piena, è possibile visualizzare automaticamente un'altra finestra per visualizzare più icone.

## Risoluzione dei problemi

### Le applicazioni non partono sempre

Talvolta può capitare che una applicazione, come Firefox o Thunderbird, si avviino correttamente e a volte capita che l'avvio fallisce restituendo un errore, oppure senza nessun output. Se state utilizzando il pacchetto [windowmaker](https://aur.archlinux.org/packages/windowmaker/), provare ad utilizzare il pacchetto [windowmaker-crm-git](https://aur.archlinux.org/packages/windowmaker-crm-git/) al suo posto.

### Non è possibile disabilitare lo *smooth* dei font

Cancellare (conviene fare una copia di backup) la cartella `~/.fontconfig/` ed il file `~/.fonts.conf`, successivamente riavviare Window Maker.

## Altre fonti

*   [Sito ufficiale](http://www.windowmaker.org/)
*   [Window Maker (Wikipedia)](https://en.wikipedia.org/wiki/Window_Maker "wikipedia:Window Maker")
*   [Dockapps](http://dockapps.windowmaker.org/)