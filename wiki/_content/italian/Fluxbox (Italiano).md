Fluxbox è un gestore di finestre per X. È basato sul codice di Blackbox 0.61.1\. Fluxbox assomiglia a blackbox e gestisce elementi come lo stile, i colori, il posizionamento delle finestre e altre cose simili, esattamente come blackbox (la compatibilità dei temi/stile è del 100%). Fluxbox ha una sintassi facile da imparare ed è estremamente leggero. Arch + Fluxbox infatti può infatti rendere molto usabile un vecchio pentium con 256 MB di ram.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Avviare Fluxbox](#Avviare_Fluxbox)
    *   [2.1 Metodo 1: KDM/GDM](#Metodo_1:_KDM.2FGDM)
    *   [2.2 Metodo 2: ~/.xinitrc](#Metodo_2:_.7E.2F.xinitrc)
*   [3 Configurazione](#Configurazione)
    *   [3.1 Gestione del Menu](#Gestione_del_Menu)
        *   [3.1.1 Metodo incorporato](#Metodo_incorporato)
        *   [3.1.2 MenuMaker](#MenuMaker)
        *   [3.1.3 Arch Linux Xdg menu](#Arch_Linux_Xdg_menu)
        *   [3.1.4 Creare e modificare manualmente il menu](#Creare_e_modificare_manualmente_il_menu)
    *   [3.2 Init](#Init)
    *   [3.3 Scorciatoie da tastiera](#Scorciatoie_da_tastiera)
    *   [3.4 Aree di lavoro](#Aree_di_lavoro)
    *   [3.5 Schede e gruppi](#Schede_e_gruppi)
    *   [3.6 Background](#Background)
        *   [3.6.1 Note per chi ama cambiare spesso sfondo](#Note_per_chi_ama_cambiare_spesso_sfondo)
        *   [3.6.2 Feh](#Feh)
    *   [3.7 Temi](#Temi)
    *   [3.8 Slit](#Slit)
    *   [3.9 Avvio automatico delle applicazioni](#Avvio_automatico_delle_applicazioni)
    *   [3.10 Altri menu](#Altri_menu)
    *   [3.11 Vera trasparenza](#Vera_trasparenza)
    *   [3.12 Notifiche](#Notifiche)
    *   [3.13 Una vita dopo xorg.conf](#Una_vita_dopo_xorg.conf)
        *   [3.13.1 Impostare correttamente la propria tastiera](#Impostare_correttamente_la_propria_tastiera)
*   [4 Altre risorse](#Altre_risorse)

## Installazione

Il pacchetto [fluxbox](https://www.archlinux.org/packages/?name=fluxbox) è presente nei [repositories ufficiali](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)"). Installarlo quindi con [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)").

Se non si ha ancora installaro [xorg](/index.php/Xorg_(Italiano) "Xorg (Italiano)"), farlo ora.

## Avviare Fluxbox

### Metodo 1: KDM/GDM

Gli utenti di [KDM](/index.php/KDM_(Italiano) "KDM (Italiano)"), [GDM](/index.php/GDM "GDM") o [Lightdm](/index.php/Lightdm "Lightdm") troveranno una nuova voce di fluxbox aggiunta automaticamente al loro menù di sessione. Si scelga semplicemente l'opzione fluxbox durante la fase del login.

### Metodo 2: ~/.xinitrc

Si modifichi il file `~/.xinitrc` e si aggiunga la seguente riga:

```
exec startfluxbox

```

Vedere [xinitrc](/index.php/Xinitrc_(Italiano) "Xinitrc (Italiano)") per i dettagli su come preservare la sessione logind (utile ad esempio per l'automount dei dispositivi usb).

## Configurazione

I file di configurazione generali di fluxbox (quindi validi per tutti gli utenti del sistema) sono contenuti in `/usr/share/fluxbox`, mentre quelli vlidi a livello del solo utente sono contenuti in `~/.fluxbox`.

Quindi dare da user:

```
$ mkdir ~/.fluxbox
$ cp /usr/share/fluxbox/* ~/.fluxbox/

```

per copiare tutti i file nella directory dell'utente.

Nello specifico, i file sono:

*   init: il file principale di fluxbox. Vedere [Editare il file _init_](http://fluxbox-wiki.org/index.php?title=Editing_the_init_file)
*   menu: file di configurazione del menu di fluxbox. Vedere sotto e [Editare il file _menu_](http://fluxbox-wiki.org/index.php?title=Editing_the_menu)
*   keys: file di configurazione delle scorciatoie da tastiera di fluxbox (hotkeys). Vedere sotto e [qui](http://fluxbox-wiki.org/index.php?title=Keyboard_shortcuts)
*   startup: file nel quale è possibile decidere quali programmi si vogliono avviare all'inizio della sessione. Vedere anche [xinitrc](/index.php/Xinitrc_(Italiano) "Xinitrc (Italiano)") e [questo articolo](http://fluxbox-wiki.org/index.php?title=Editing_the_startup_file)
*   overlay: file di configurazione per gli _elementi di stile_. Vedere anche [qui](http://fluxbox-wiki.org/index.php?title=Style_overlay).
*   apps: file che permette a fluxbox di ricordare le impostazioni delle singole finestre. Vedere [qui](http://fluxbox-wiki.org/index.php?title=Editing_the_apps_file)
*   windowmenu: file per modificare la finestra del menu: per maggiori informazioni leggere [leggere questo articolo](http://fluxbox-wiki.org/index.php?title=Editing_the_windowmenu)

### Gestione del Menu

Quando si installa fluxbox la prima volta, il menù sarà davvero minimale. Inoltre essendo un WM non ha nessuno strumento per aggiornare il menu ogni qual volta si installa o disintalla qualcosa. Il menu, raggiungibile con il click destro del mouse sul desktop, va quindi creato o modificato a mano ~/.fluxbox/menu. Esistono comunque dei metodi automatici per la sua creazione.

#### Metodo incorporato

Comando incorporato:

```
$ fluxbox-generate_menu

```

Questo comando genera un file ~/.fluxbox/menu/ basato sui propri programmi installati. C'è anche un "aiuto / rigenerazione menu" nel menu di fluxbox.

#### MenuMaker

[MenuMaker](http://menumaker.sourceforge.net/) è un potento strumento che crea menu basati su codice XML per vari gestori di finestre, Fluxbox incluso. MenuMaker eseguirà una ricerca di programmi avviabili sul sistema ed in base al risultato creerà il menu. Può anche essere configurato per escludere applicazioni basate su Legacy X, GNOME, KDE, o Xfce, se desiderato.

MenuMaker è presente nel repository [community] di pacman:

```
# pacman -S menumaker

```

Una volta installato, si può generare un menu completo eseguendo:

```
$ mmaker -f Fluxbox

```

Per una lista completa di tutte le opzioni possibili si digiti da terminale: $ mmaker --help

#### Arch Linux Xdg menu

Richiede [archlinux-xdg-menu](https://www.archlinux.org/packages/?name=archlinux-xdg-menu), installabile con pacman:

```
# pacman -S archlinux-xdg-menu

```

Per creare il menu lanciare in un terminale (da utente):

```
$ xdg_menu --fullmenu --format fluxbox --root-menu /etc/xdg/menus/arch-applications.menu >~/.fluxbox/menu

```

Per maggiori informazioni:

```
$ xdg_menu --help

```

_Si veda anche: [XdgMenu](/index.php/XdgMenu "XdgMenu")_

#### Creare e modificare manualmente il menu

Si usi il comando:

```
$ nano ~/.fluxbox/menu

```

**Nota:** non è fondamentale usare _nano_, va bene un qualunque editor.

La sintassi base del file è:

```
[exec] (name) {command} <percorso icona>

```

dove _name_ è il testo che apparirà sul menu e _command_ è il percorso dei binari, ad esempio:

```
[exec] (Firefox Browser) {/usr/bin/firefox} <percorso esatto all'icona di firefox>

```

**Nota:** per determinare il percorso dei binari usare _pacman -Ql_

Notare che "<percorso all'icona>" non è fondamentale. Se si desidera creare un sottomenù usare la seguente sintassi:

```
[submenu] (Name)
...
...
[end]

```

Una volta finito, salvare ed uscire. Non è necessario riavviare fluxbox. Per maggiori informazioni leggere [editare il menu di fluxbox](http://fluxbox-wiki.org/index.php?title=Editing_the_menu).

### Init

Il file `~/.fluxbox/init` è la _base_ di Fluxbox. Da qui si possono cambiare tutte le funzionalità di base come finestre, toolbar, focus ecc... Alcuni di questi parametri sono modificabili anche tramite il _Configuration Menu_. Per maggiori informazioni leggere [editare il file _init_](http://fluxbox-wiki.org/index.php?title=Editing_the_init_file).

### Scorciatoie da tastiera

Fluxbox offre funzionalità base di scorciatoie da tastiera. Il file dei tasti di fluxbox è situato in:

```
~/.fluxbox/keys

```

La chiave Control è rappresentata da "Control". Mod1 corrisponde ad Alt e Mod4 corrisponde a Meta (non è una chiave standard ma molti stabiliscono una corrispondenza tra meta e il tasto di windows)

Qui c'è un metodo veloce per controllare il volume del canale _master_ utilizzando i tastiCTRL-ALT+ Freccia su e giù:

```
Control Mod1 Up :Exec amixer set Master,0 5%+  
Control Mod1 Down :Exec amixer set Master,0 5%-  

```

### Aree di lavoro

Di base fluxbox dispone di quattro aree di lavoro. Queste sono accessibili usando la scorciatoia Ctrl+F1-F4, o con la freccia sulla toolbar vicino alla scritta che dice **uno**.

Cliccando con il destro sul desktop e andando nel proprio menù Workspace (gli utenti di menumaker: FluxBox>Workspaces, gli utenti di fluxconf: il titolo aree di lavoro) sarà possibile interagire con le aree di lavoro.

Menù delle aree di lavoro:

```
Icons – mostra le applicazioni minimizzate
--separator--
Workspaces names (default: one,two,three,four) – Mostra tutte le applicazioni su quel desktop
--separator--
New Workspace – Aggiunge un'area di lavoro
Edit Current workspace name – permette di impostare il nome che si desidera per le aree di lavoro. Sarà mostrato sul lato sinistro della toolbar
Remove Last - Rimuove l'ultima area di lavoro della lista, sposta tutte le applicazioni di quel desktop su quello precedente

```

### Schede e gruppi

Con almeno due finestre aperte sullo spazio di lavoro è possibile tramite `Ctrl + Click destro` unire le due finestre in una sola. In questo modo, un operazione sulla finestra agirà su entramenbe le schede raggruppate. Per effettuare l'operazione inversa usare sempre `Ctrl + Click Destro` su una scheda e trascinarsa su una parte libera del desktop.

### Background

Per impostare lo sfondo è necessario usare un programma dedicato che si può installare con uno di questi pacchetti:

*   eterm
*   feh

Ce ne sono anche altri, ma questi sono i due raccomandati, per gli altri è possibile consultare la documentazione di fbsetbg nella sezione "Additional Links section" Per impostare lo sfondo:

```
$ fbsetbg /percorso/all'/immagine.di.sfondo

```

Si può anche aggiungere (o modificare) la linea seguente nel file ~/.fluxbox/init in modo da risultare:

```
session.screen0.rootCommand:	fbsetbg /percorso/al/wallpaper

```

O semplicemente:

```
session.screen0.rootCommand:	fbsetbg -l

```

#### Note per chi ama cambiare spesso sfondo

Posizionare questo sottomenù nel proprio menù di fluxbox

```
[submenu] (Backgrounds)
[wallpapers] (~/.fluxbox/backgrounds) {feh --bg-scale}
[wallpapers] (/usr/share/fluxbox/backgrounds) {feh --bg-scale}
[end]

```

Ora mettere le proprie immagini di sfondo in `~/.fluxbox/backgrounds` o in una qualsiasi altra cartella si abbia specificato, ora appariranno allo stesso modo degli stili.

Si proceda in maniera analoga per i sistemi a doppio schermo senza 'xinerama' (ad esempio NVidio TwinView):

```
[submenu] (Backgrounds)
[wallpapers] (/path/to/your/backgrounds) {feh --bg-scale --no-xinerama }
[end]

```

#### Feh

Installare [feh](https://www.archlinux.org/packages/?name=feh) con [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)").

Per assicurarsi che fluxbox carichi lo sfondo di feh al prossimo avvio:

**1.** Rendere `.fehbg` eseguibile:

```
$ chmod 770 ~/.fehbg

```

**2.** Aggiungere poi (o modificare) la seguente linea al file `~/.fluxbox/init`:

```
session.screen0.rootCommand:	~/.fehbg

```

**3.** o aggiungere (o modificare) la seguente linea al file `~/.fluxbox/startup`:

```
~/.fehbg

```

### Temi

Per installare un tema si estragga l'archivio in una cartella di stile, quelle di default sono:

*   globale - /usr/share/fluxbox/styles
*   solo dell'utente - ~/.fluxbox/styles

Su [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)") è presente il pacchetto [fluxmod-styles](https://aur.archlinux.org/packages/fluxmod-styles/) che include parecchi temi. Una volta installato comparirà in Fluxbox -> Styles nel menu.

Per creare un proprio tema, seguire le pagine [Fluxbox Style Guide](/index.php/Fluxbox_Style_Guide_(Italiano) "Fluxbox Style Guide (Italiano)") e [Style Guide](http://tenr.de/howto/style_fluxbox/style_fluxbox.html).

Se si usa `mmaker -f FluxBox` per creare il proprio menu non si troverà poi la sezione per il cambio di tema. Aggiungere quindi a `~/.fluxbox/menu`:

```
[submenu] (System Styles) {Choose a style...}
  [stylesdir] (/usr/share/fluxbox/styles)
[end]
[submenu] (User Styles) {Choose a style...}
  [stylesdir] (~/.fluxbox/styles)
[end]

```

### Slit

Fluxbox, WindowMaker, Openbox e pochi altri window managers hanno "Slit". In pratica una parte della dock, visibile su ogni spazio di lavoro in cui le applicazioni sono ancorate. Visitare: [dockapps.windowmaker.org](http://dockapps.windowmaker.org/).

### Avvio automatico delle applicazioni

Gli utenti di [Xinitrc](/index.php/Xinitrc_(Italiano) "Xinitrc (Italiano)") dovrebbero inserire tutto il codice in `~/.xinitrc`. Ad ogni modo, fluxbox offre la possibilità di avviare automaticamente le applicazioni da solo.

Il file `~/.fluxbox/startup` è uno script per l'avvio delle applicazioni contemporaneamente all'avvio stesso di fluxbox. Il simbolo # denota un commento. (il cancelletto denota un commento)

Un file d'esempio:

```
fbsetbg -l # imposta lo sfondo.
# il simbolo (&) nei comandi sottostanti permette ai programmi avviati di non stopparsi subito e a fluxbox di avviarsi in modo corretto
idesk & 
xterm &
exec /usr/bin/startfluxbox
# o se si vuole un log:
# exec /usr/bin/fluxbox -log ~/.fluxbox/log

```

### Altri menu

In the "Menu Management" section (above) we were discussing the main "Applications" Menu, called the "Root" menu in fluxbox lingo. FluxBox also has other menus available to the user:

*   Workspaces Menu: click tasto centrale mouse sul desktop.
*   Configuration Menu: located within the "Fluxbox" section of the "Root" menu.
*   Window menu: click destro sul bordo di una finestra. Può essere modificato. Vedere la pagina _man_ di fluxbox-menu.
*   Toolbar menu: click destro su una parte vuota della toolbar. Modificabile attraverso un sotto-menu in Configuration Menu.
*   Slit Menu: si trova in una sotto sezione di Configuration Menu.

### Vera trasparenza

Per abilitare la vera trasparenza in fluxbox è necessario un compositor per X come [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") disponibile nei [repository ufficiali](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)").

### Notifiche

Per abilitare le notifiche a schermo per fluxbox leggere [questo topic del forum internazionale di Arch](https://bbs.archlinux.org/viewtopic.php?id=138616).

### Una vita dopo xorg.conf

Xorg non richiede più il file xorg.conf. Tradizionalmente è qui che si configurerebbero le impostazioni della tastiera e quelle per il risparmio energetico. Fortunatamente esistono altre soluzioni efficaci senza xorg.conf.

#### Impostare correttamente la propria tastiera

Si aggiunga semplicemente la linea seguente in `~/.fluxbox/startup`:

```
setxkbmap us -variant intl & # to have a us keyboard with special characters enabled (like éóíáú)

```

Al posto di 'us' si può inserire il codice della propria lingua e rimuovere le opzioni diverse (ad esempio: 'us_intl', che funziona come il comando precedente in alcuni setup). Si veda il man di setxkbmap per maggiori informazioni.

Per creare una funzione d'aiuto nel proprio menù, si aggiunga in `~/.fluxbox/menu`:

```
[submenu] (Keyboard)
      [exec] (normal) {setxkbmap us}
      [exec] (international) {setxkbmap us -variant intl}
[end]

```

## Altre risorse

*   [Fluxbox Homepage](http://fluxbox.org/)
*   [Gentoo Wiki about Fluxbox](http://wiki.gentoo.org/wiki/Fluxbox)
*   [Themes for Fluxbox](http://box-look.org/)
*   [Fluxbox Wiki](http://fluxbox-wiki.org/)
*   [fbsetbg documentation](http://www.xs4all.nl/~hanb/software/fbsetbg/fbsetbg.html)
*   [Application recommendations](http://archux.com/page/application-recommendations)
*   [Fluxbox Style Guide](/index.php/Fluxbox_Style_Guide_(Italiano) "Fluxbox Style Guide (Italiano)")