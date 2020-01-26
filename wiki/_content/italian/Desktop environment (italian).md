Articoli correlati

*   [Display Manager](/index.php/Display_Manager_(Italiano) "Display Manager (Italiano)")
*   [Window Manager](/index.php/Window_Manager_(Italiano) "Window Manager (Italiano)")
*   [Default applications](/index.php/Default_applications "Default applications")

Un [Desktop environment](https://en.wikipedia.org/wiki/it:Desktop_environment "wikipedia:it:Desktop environment") fornisce una *completa* interfaccia Grafica Utente (GUI) per un sistema, abbinando insieme una serie di client [X](https://en.wikipedia.org/wiki/it:X_Window_System "wikipedia:it:X Window System") scritti utilizzando widget-toolkit ed insiemi di librerie comuni.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 X Window System](#X_Window_System)
*   [2 Ambienti Desktop](#Ambienti_Desktop)
    *   [2.1 Lista degli Ambienti Desktop](#Lista_degli_Ambienti_Desktop)
        *   [2.1.1 Supportati ufficialmente](#Supportati_ufficialmente)
        *   [2.1.2 Non supportati ufficialmente](#Non_supportati_ufficialmente)
    *   [2.2 Comparazione tra i vari Ambienti Desktop](#Comparazione_tra_i_vari_Ambienti_Desktop)
        *   [2.2.1 Peso delle risorse di sistema](#Peso_delle_risorse_di_sistema)
        *   [2.2.2 Familiarità degli Ambienti Desktop](#Familiarità_degli_Ambienti_Desktop)
*   [3 Ambienti Personalizzati](#Ambienti_Personalizzati)

## X Window System

Il sistema [X Window](https://en.wikipedia.org/wiki/it:X_Window_System per ulteriori informazioni.

	*X fornisce il framework basico, o primitive, per costruire ambienti GUI: spazi di interazione con un mouse, una tastiera o altri input per finestre sullo schermo. X non controlla l'interfaccia utente per ciascuna applicazione, ogni programma ha un suo client se ne occupa. Come tale, lo stile visivo di ambienti basati su X varia molto; diversi programmi possono presentare interfacce radicalmente diverse. X è costruito come un ulteriore (applicazione) livello di astrazione sopra il kernel del sistema operativo.*

L'utente è libero di configurare l'aspetto grafico del proprio ambiente in molti modi. Gli ambienti desktop, semplicemente, forniscono uno strumento completo e conveniente per svolgere tale compito.

## Ambienti Desktop

Un **ambiente desktop** di serie, insieme ad una serie di client X, forniscono elementi comuni dell'interfaccia utente grafica, come icone, finestre, barre degli strumenti, sfondi e widget sul desktop. Inoltre maggior parte degli ambienti desktop include un set di applicazioni integrate e di servizi.

Si noti che gli utenti sono liberi di creare un mix di applicazioni provenienti da diversi ambienti desktop. Ad esempio, un utente KDE può installare ed eseguire applicazioni di GNOME, come il browser web Epiphany, se lo si preferisce al browser web Konqueror installato di default con KDE. Uno svantaggio di questo approccio è che molte applicazioni, offerte dai diversi ambienti desktop, dipendono in larga misura alla base, dalle rispettive librerie di sviluppo. Come risultato, l'installazione di applicazioni da una vasta gamma di ambienti desktop richiederà l'installazione di un maggior numero di dipendenze. Gli utenti che cercano di risparmiare spazio su disco ed evitare di [gonfiare il software](https://en.wikipedia.org/wiki/it:software_bloat "wikipedia:it:software bloat"), spesso evitano questo tipo di approccio, oppure ricercano soluzioni alternative più leggere ed indipendenti.

Inoltre, le applicazioni condizionate al DE, tendono a integrarsi meglio con i loro ambienti nativi. Superficialmente l'utilizzo di *ambienti misti*, che utilizzano diversi librerie di sviluppo, si tradurrà in discrepanze visive (cioè, le interfacce useranno icone e stili diversi). In termini di esperienza utente, applicazioni provenienti da ambienti misti, non possono comportarsi in modo simile causando potenzialmente confusione o un comportamento imprevisto (ad esempio il comportamento del singolo clic rispetto al doppio clic sulle icone, o la funzionalità drag-and-drop).

### Lista degli Ambienti Desktop

#### Supportati ufficialmente

*   **[Budgie](/index.php/Budgie_Desktop_(Italiano) "Budgie Desktop (Italiano)")** — Budgie è un'interfaccia utente disegnata per l'utente moderno, è basato sulla semplicità ed eleganza.

	[https://solus-project.com/budgie/](https://solus-project.com/budgie/) || [budgie-desktop](https://www.archlinux.org/packages/?name=budgie-desktop)

*   **[Cinnamon](/index.php/Cinnamon "Cinnamon")** — Cinnamon è un fork di Gnome 3\. Cinnamon si sforza di fornire un esperienza utente tradizionale, simile a Gnome 2.

	[http://cinnamon.linuxmint.com/](http://cinnamon.linuxmint.com/) || [cinnamon](https://www.archlinux.org/packages/?name=cinnamon)

*   **[Deepin](/index.php/Deepin "Deepin")** — Deepin è una interfaccia desktop con applicazioni caratterizzate da un design intuitivo ed elegante. Intuitivo, semplice ed elegante ed usarlo è una gioiosa esperienza.

	[deepin](https://www.archlinux.org/groups/x86_64/deepin/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[Enlightenment](/index.php/Enlightenment_(Italiano) "Enlightenment (Italiano)")** — L'ambiente di lavoro Enlightenment fornisce un window manager efficiente e mozzafiato basato sul Enlightenment Foundation Libraries (EFL) insieme ad altri componenti del desktop essenziali, come un file manager, le icone del desktop e widget. Vanta un livello senza precedenti di capacità di eseguire temi grafici, pur essendo in grado di eseguirli con hardware più vecchio o su dispositivi embedded.

	[http://www.enlightenment.org/](http://www.enlightenment.org/) || [enlightenment](https://www.archlinux.org/packages/?name=enlightenment)

*   **[GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)")** — Il progetto GNOME fornisce un intuitivo e completo ambiente desktop, e una piattaforma di sviluppo per la creazione di applicazioni da integrare nel resto del desktop. GNOME è gratuito, usabile, accessibile, internazionale, semplice per gli sviluppatori, organizzato, sostenuto ed è una comunità.

	[http://www.gnome.org/about/](http://www.gnome.org/about/) || [gnome](https://www.archlinux.org/groups/x86_64/gnome/)

*   **GNUstep** — GNUstep è un ambiente libero, orientato agli oggetti, sviluppato multi-piattaforma che si sforza di essere semplice ed elegante.

	[http://gnustep.org/](http://gnustep.org/) || [windowmaker](https://aur.archlinux.org/packages/windowmaker/)

*   **[KDE SC](/index.php/KDE_(Italiano) "KDE (Italiano)")** — Kde Software Compilation è costituito da un gran numero di applicazioni individuali ed uno spazio di lavoro desktop, inteso come un guscio all'interno del quale è possibile eseguire queste applicazioni in modo integrato. È possibile eseguire bene le applicazioni KDE su qualsiasi ambiente desktop. Le applicazioni di KDE sono costruite per integrarsi al meglio con i componenti del sistema. Con l'utilizzo anche dello spazio di lavoro KDE, si ottiene una migliore integrazione delle applicazioni con l'ambiente di lavoro, consentendo di diminuire le esigenze di risorse di sistema.

	[http://www.kde.org/](http://www.kde.org/) || [kdebase](https://www.archlinux.org/groups/x86_64/kdebase/)

*   **[LXDE](/index.php/LXDE_(Italiano) "LXDE (Italiano)")** — *Il **L**ightweight **X**11 **D**esktop **E**nvironment* è un ambiente desktop estremamente veloce, performante e con un buon risparmio energetico. Gestito da una comunità internazionale di sviluppatori, si presenta con una bella interfaccia, supporto multi-lingua, tasti di scelta rapida standard e funzionalità aggiuntive come la navigazione a schede dei file. LXDE utilizza meno CPU e RAM di altri ambienti desktop. È progettato appositamente per i computer cloud con basse specifiche hardware, come i netbook, i dispositivi MID (Mobile ad esempio) o computer datati.

	[http://lxde.org/](http://lxde.org/) || [lxde](https://www.archlinux.org/groups/x86_64/lxde/)

*   **[MATE](/index.php/MATE "MATE")** — Mate è un fork di Gnome 2\. Mate fornisce un desktop intuitivo e attraente per gli utenti Linux che utilizzano metafore tradizionali.

	[http://www.mate-desktop.org/](http://www.mate-desktop.org/) || [mate](https://www.archlinux.org/groups/x86_64/mate/)

*   **[Xfce](/index.php/Xfce_(Italiano) "Xfce (Italiano)")** — Xfce incarna la filosofia UNIX tradizionali di modularità e riutilizzabilità. Si compone di una serie di componenti che forniscono la completa funzionalità che si può aspettare da un ambiente desktop moderno. Essi sono distribuiti separatamente e si può scegliere tra i pacchetti disponibili per creare un ambiente ottimale di lavoro personale.

	[http://www.xfce.org/](http://www.xfce.org/) || [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/)

#### Non supportati ufficialmente

*   **[EDE](/index.php/Equinox_Desktop_Environment "Equinox Desktop Environment")** — "Equinox Desktop Environment" è un DE designato per essere semplice, estremamente leggero e veloce.

	[http://equinox-project.org/](http://equinox-project.org/) || [ede](https://aur.archlinux.org/packages/ede/)

*   **[GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback")** — GNOME Flashback è una shell per GNOME 3, la quale era inizialmente chiamata "modalità GNOME fallback". Il layout del desktop e la sottostante tecnologia è simile a GNOME 2.

	[https://wiki.gnome.org/GnomeFlashback](https://wiki.gnome.org/GnomeFlashback) || [gnome-panel](https://www.archlinux.org/packages/?name=gnome-panel)

*   **Hawaii** — Hawaii è un ambiente desktop leggero , coerente e veloce che si basa su Qt 5 , QtQuick e Wayland ed è stato progettato per offrire la migliore UX per il dispositivo in cui è in esecuzione.

	[http://www.maui-project.org/](http://www.maui-project.org/) || [hawaii-meta-git](https://aur.archlinux.org/packages/hawaii-meta-git/)

*   **[LXQt](/index.php/LXQt "LXQt")** — Lxqt è la versione di sviluppo di un nuovo ambiente desktop LXDE, scritto dagli sviluppatori di Razor-qt. Si basa su tecnologie Qt.

	||

*   **[Pantheon](/index.php/Pantheon "Pantheon")** — Pantheon è l'ambiente desktop predefinito e originariamente creato per la distribuzione Elementary OS. Esso è scritto da zero utilizzando Vala e il toolkit GTK3\. Per quanto riguarda l'usabilità e l'aspetto, il desktop ha alcune somiglianze con GNOME Shell e Mac OS X.

	[http://elementaryos.org/](http://elementaryos.org/) || [pantheon-session-bzr](https://aur.archlinux.org/packages/pantheon-session-bzr/)

*   **[Razor-qt](/index.php/Razor-qt "Razor-qt")** — É un ambiente deskto avanzato, veloce e facile da usare, e si basa sulle tecnologie Qt. E 'stato pensato per utenti che apprezzano la semplicità, velocità e un'interfaccia intuitiva. Razor-qt è un nuovo progetto e contiene già tutti i componenti chiave per un ambiente desktop.

	[http://razor-qt.org/](http://razor-qt.org/) || [razor-qt](https://aur.archlinux.org/packages/razor-qt/)

*   **[ROX](/index.php/ROX "ROX")** — ROX è un Desktop facile da usare, veloce e che fa ampio uso di drag-and-drop. L'interfaccia ruota attorno al file manager, o filer, in seguito alla visione tradizionale di Unix che 'tutto è un file' piuttosto che cercare di nascondere il file system sotto menu start o assistenti di configurazione. L'obiettivo è di creare un sistema che è ben progettato e che ben si presenti. Lo stile di ROX favorisce utilizzando diversi piccoli programmi insieme invece di creare mega-applicazione che comprenda di tutto.

	[http://rox.sourceforge.net/desktop/](http://rox.sourceforge.net/desktop/) || [rox-](https://aur.archlinux.org/packages/rox-/)

*   **[Sugar](/index.php/Sugar_(Italiano) "Sugar (Italiano)")** — La piattaforma di apprendimento Sugar, è un ambiente informatico composto da attività che contribuiscono ai bambini da 5 a 12 anni di imparare insieme attraverso l'espressione rich-media. Sugar è il componente principale di uno sforzo mondiale per fornire ad ogni bambino l'opportunità di una formazione di qualità - è attualmente utilizzato da circa un milione di bambini in tutto il mondo che parlano 25 lingue in oltre 40 paesi. Sugar fornisce i mezzi per aiutare le persone a condurre una vita soddisfacente attraverso l'accesso ad un'istruzione di qualità, ciò che attualmente è vista come una mancanza da parte di molti.

	[http://wiki.sugarlabs.org/](http://wiki.sugarlabs.org/) || [sugar](https://www.archlinux.org/packages/?name=sugar)

*   **[Trinity](/index.php/Trinity "Trinity")** — Il progetto "Trinity Desktop Environment" (TDE) è un ambiente desktop per computer che utilizzano sistemi operativi Unix-like, con l'obbiettivo primario di conservare l'aspetto e il sistema di KDE 3.5.

	[http://www.trinitydesktop.org/](http://www.trinitydesktop.org/) || See [Trinity](/index.php/Trinity "Trinity")

*   **[Unity](/index.php/Unity "Unity")** — Unity è una shell per GNOME disegnata da Canonical per Ubuntu.

	[http://unity.ubuntu.com/](http://unity.ubuntu.com/) || [unity](https://aur.archlinux.org/packages/unity/)

### Comparazione tra i vari Ambienti Desktop

*Questa sezione cerca di tracciare un confronto tra i più diffusi ambienti desktop. Si noti che l'esperienza in prima persona è l'unico modo efficace per valutare se davvero un ambiente desktop più adatta alle vostre esigenze.*

[confronto fra i vari Ambienti Desktop](https://en.wikipedia.org/wiki/it:Comparison_of_X_Window_System_desktop_environments "wikipedia:it:Comparison of X Window System desktop environments")

<caption>Panoramica sugli ambienti desktop</caption>
| Ambiente desktop | Libreria di Sviluppo | Gestore delle finestre | Barra delle applicazioni | Emulatore di Terminale | File manager | calcolatrice | Editor di testo | Visualizzatore di immagini | Lettore multimediale | Browser Web | Gestore della sessione |
| [Budgie](/index.php/Budgie_Desktop_(Italiano) "Budgie Desktop (Italiano)") | [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [budgie-desktop](https://www.archlinux.org/packages/?name=budgie-desktop) | [budgie-desktop](https://www.archlinux.org/packages/?name=budgie-desktop) | [gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) | [nautilus](https://www.archlinux.org/packages/?name=nautilus) | [gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](/index.php/Gedit "Gedit") | [eog](https://www.archlinux.org/packages/?name=eog) | [totem](https://www.archlinux.org/packages/?name=totem) | [epiphany](https://www.archlinux.org/packages/?name=epiphany) | [gdm](https://www.archlinux.org/packages/?name=gdm) |
| Cinnamon | [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [muffin](https://www.archlinux.org/packages/?name=muffin) | [cinnamon](https://www.archlinux.org/packages/?name=cinnamon) | [gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) | [nemo](https://www.archlinux.org/packages/?name=nemo) | [gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](https://www.archlinux.org/packages/?name=gedit) | [eog](https://www.archlinux.org/packages/?name=eog) | [totem](https://www.archlinux.org/packages/?name=totem) | [firefox](https://www.archlinux.org/packages/?name=firefox) | [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) |
| Deepin | [gtk2](https://www.archlinux.org/packages/?name=gtk2) [gtk3](https://www.archlinux.org/packages/?name=gtk3) [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) | [deepin-wm](https://www.archlinux.org/packages/?name=deepin-wm) | [deepin-dock](https://www.archlinux.org/packages/?name=deepin-dock) | [deepin-terminal](https://www.archlinux.org/packages/?name=deepin-terminal) | [deepin-file-manager](https://www.archlinux.org/packages/?name=deepin-file-manager) | [gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](https://www.archlinux.org/packages/?name=gedit) | [deepin-image-viewer](https://www.archlinux.org/packages/?name=deepin-image-viewer) | [deepin-movie](https://www.archlinux.org/packages/?name=deepin-movie) | [chromium](https://www.archlinux.org/packages/?name=chromium) | [deepin-session-ui](https://www.archlinux.org/packages/?name=deepin-session-ui) |
| EDE | [fltk](https://www.archlinux.org/packages/?name=fltk) | [pekwm](https://www.archlinux.org/packages/?name=pekwm) | [ede](https://aur.archlinux.org/packages/ede/) | [xterm](https://www.archlinux.org/packages/?name=xterm) | [fluff](https://aur.archlinux.org/packages/fluff/) | [zalc](https://aur.archlinux.org/packages/zalc/) | [fltk-editor](https://aur.archlinux.org/packages/fltk-editor/) | [ede](https://aur.archlinux.org/packages/ede/) | [flmusic](https://aur.archlinux.org/packages/flmusic/) | [dillo](https://www.archlinux.org/packages/?name=dillo) | [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm) |
| [Enlightenment](/index.php/Enlightenment_(Italiano) "Enlightenment (Italiano)") | [efl](https://www.archlinux.org/packages/?name=efl) | [enlightenment](https://www.archlinux.org/packages/?name=enlightenment) | [enlightenment](https://www.archlinux.org/packages/?name=enlightenment) | [terminology](https://www.archlinux.org/packages/?name=terminology) | [enlightenment](https://www.archlinux.org/packages/?name=enlightenment) | [equate-git](https://aur.archlinux.org/packages/equate-git/) | [ecrire-git](https://aur.archlinux.org/packages/ecrire-git/) | [ephoto-git](https://aur.archlinux.org/packages/ephoto-git/) | [rage](https://aur.archlinux.org/packages/rage/) | [links](https://www.archlinux.org/packages/?name=links) | [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm) |
| [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)") | [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [mutter](https://www.archlinux.org/packages/?name=mutter) | [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell) | [gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) | [nautilus](https://www.archlinux.org/packages/?name=nautilus) | [gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](https://www.archlinux.org/packages/?name=gedit) | [eog](https://www.archlinux.org/packages/?name=eog) | [totem](https://www.archlinux.org/packages/?name=totem) | [epiphany](https://www.archlinux.org/packages/?name=epiphany) | [gdm](https://www.archlinux.org/packages/?name=gdm) |
| GNOME Flashback | [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [metacity](https://www.archlinux.org/packages/?name=metacity) | [gnome-panel](https://www.archlinux.org/packages/?name=gnome-panel) | [gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) | [nautilus](https://www.archlinux.org/packages/?name=nautilus) | [gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](https://www.archlinux.org/packages/?name=gedit) | [eog](https://www.archlinux.org/packages/?name=eog) | [totem](https://www.archlinux.org/packages/?name=totem) | [epiphany](https://www.archlinux.org/packages/?name=epiphany) | [gdm](https://www.archlinux.org/packages/?name=gdm) |
| [KDE Plasma](/index.php/KDE_(Italiano) "KDE (Italiano)") | [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) | [kwin](https://www.archlinux.org/packages/?name=kwin) | [plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop) | [konsole](https://www.archlinux.org/packages/?name=konsole) | [dolphin](https://www.archlinux.org/packages/?name=dolphin) | [kcalc](https://www.archlinux.org/packages/?name=kcalc) | [kwrite](https://www.archlinux.org/packages/?name=kwrite) [kate](https://www.archlinux.org/packages/?name=kate) | [gwenview](https://www.archlinux.org/packages/?name=gwenview) | [dragon](https://www.archlinux.org/packages/?name=dragon) | [konqueror](https://www.archlinux.org/packages/?name=konqueror) | [sddm](https://www.archlinux.org/packages/?name=sddm) |
| Liri | [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) | [greenisland](https://aur.archlinux.org/packages/greenisland/) | [liri-shell-git](https://aur.archlinux.org/packages/liri-shell-git/) | [liri-terminal-git](https://aur.archlinux.org/packages/liri-terminal-git/) | [liri-files-git](https://aur.archlinux.org/packages/liri-files-git/) | [liri-calculator-git](https://aur.archlinux.org/packages/liri-calculator-git/) | [liri-text-git](https://aur.archlinux.org/packages/liri-text-git/) | [eyesight](https://aur.archlinux.org/packages/eyesight/) | liri-player | [liri-browser-git](https://aur.archlinux.org/packages/liri-browser-git/) | [sddm](https://www.archlinux.org/packages/?name=sddm) |
| [LXDE](/index.php/LXDE_(Italiano) "LXDE (Italiano)") GTK+ 2 | [gtk2](https://www.archlinux.org/packages/?name=gtk2) | [openbox](https://www.archlinux.org/packages/?name=openbox) | [lxpanel](https://www.archlinux.org/packages/?name=lxpanel) | [lxterminal](https://www.archlinux.org/packages/?name=lxterminal) | [pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm) | [galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2) | [leafpad](https://www.archlinux.org/packages/?name=leafpad) | [gpicview](https://www.archlinux.org/packages/?name=gpicview) | [lxmusic](https://www.archlinux.org/packages/?name=lxmusic) | [midori](https://www.archlinux.org/packages/?name=midori) | [lxdm](https://www.archlinux.org/packages/?name=lxdm) |
| [LXDE](/index.php/LXDE_(Italiano) "LXDE (Italiano)") GTK+ 3 | [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [openbox](https://www.archlinux.org/packages/?name=openbox) | [lxpanel-gtk3](https://www.archlinux.org/packages/?name=lxpanel-gtk3) | [lxterminal-gtk3](https://www.archlinux.org/packages/?name=lxterminal-gtk3) | [pcmanfm-gtk3](https://www.archlinux.org/packages/?name=pcmanfm-gtk3) | [galculator](https://www.archlinux.org/packages/?name=galculator) | [l3afpad](https://www.archlinux.org/packages/?name=l3afpad) | [gpicview-gtk3](https://www.archlinux.org/packages/?name=gpicview-gtk3) | [lxmusic-gtk3](https://www.archlinux.org/packages/?name=lxmusic-gtk3) | [midori](https://www.archlinux.org/packages/?name=midori) | [lxdm-gtk3](https://www.archlinux.org/packages/?name=lxdm-gtk3) |
| LXQt | [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) | [openbox](https://www.archlinux.org/packages/?name=openbox) | [lxqt-panel](https://www.archlinux.org/packages/?name=lxqt-panel) | [qterminal](https://www.archlinux.org/packages/?name=qterminal) | [pcmanfm-qt](https://www.archlinux.org/packages/?name=pcmanfm-qt) | [speedcrunch](https://www.archlinux.org/packages/?name=speedcrunch) | [notepadqq](https://www.archlinux.org/packages/?name=notepadqq) | [lximage-qt](https://www.archlinux.org/packages/?name=lximage-qt) | [smplayer](https://www.archlinux.org/packages/?name=smplayer) | [qupzilla](https://www.archlinux.org/packages/?name=qupzilla) | [sddm](https://www.archlinux.org/packages/?name=sddm) |
| [MATE](/index.php/MATE_(Italiano) "MATE (Italiano)") | [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [marco](https://www.archlinux.org/packages/?name=marco) | [mate-panel](https://www.archlinux.org/packages/?name=mate-panel) | [mate-terminal](https://www.archlinux.org/packages/?name=mate-terminal) | [caja](https://www.archlinux.org/packages/?name=caja) | [mate-calc](https://www.archlinux.org/packages/?name=mate-calc) | [pluma](https://www.archlinux.org/packages/?name=pluma) | [eom](https://www.archlinux.org/packages/?name=eom) | [parole](https://www.archlinux.org/packages/?name=parole) | [midori](https://www.archlinux.org/packages/?name=midori) | [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) |
| Pantheon | [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [gala-git](https://aur.archlinux.org/packages/gala-git/) | [plank](https://www.archlinux.org/packages/?name=plank) [wingpanel](https://www.archlinux.org/packages/?name=wingpanel) | [pantheon-terminal](https://www.archlinux.org/packages/?name=pantheon-terminal) | [pantheon-files](https://www.archlinux.org/packages/?name=pantheon-files) | [pantheon-calculator](https://www.archlinux.org/packages/?name=pantheon-calculator) | [scratch-text-editor](https://www.archlinux.org/packages/?name=scratch-text-editor) | [pantheon-photos](https://www.archlinux.org/packages/?name=pantheon-photos) | [pantheon-videos](https://www.archlinux.org/packages/?name=pantheon-videos) | [epiphany](https://www.archlinux.org/packages/?name=epiphany) | 

[lightdm-pantheon-greeter](https://aur.archlinux.org/packages/lightdm-pantheon-greeter/)

 |
| [Sugar](/index.php/Sugar_(Italiano) "Sugar (Italiano)") | [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [metacity](https://www.archlinux.org/packages/?name=metacity) | [sugar](https://www.archlinux.org/packages/?name=sugar) | [sugar-activity-terminal](https://www.archlinux.org/packages/?name=sugar-activity-terminal) | [sugar](https://www.archlinux.org/packages/?name=sugar) | [sugar-activity-calculate](https://www.archlinux.org/packages/?name=sugar-activity-calculate) | [sugar-activity-write](https://www.archlinux.org/packages/?name=sugar-activity-write) | [sugar-activity-imageviewer](https://www.archlinux.org/packages/?name=sugar-activity-imageviewer) | [sugar-activity-jukebox](https://www.archlinux.org/packages/?name=sugar-activity-jukebox) | [sugar-activity-browse](https://www.archlinux.org/packages/?name=sugar-activity-browse) | [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) |
| theShell | [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) | [kwin](https://www.archlinux.org/packages/?name=kwin) | [theshell](https://aur.archlinux.org/packages/theshell/) | [theterminal](https://aur.archlinux.org/packages/theterminal/) | [thefile](https://aur.archlinux.org/packages/thefile/) | [thecalculator](https://aur.archlinux.org/packages/thecalculator/) | [kwrite](https://www.archlinux.org/packages/?name=kwrite) [kate](https://www.archlinux.org/packages/?name=kate) | [gwenview](https://www.archlinux.org/packages/?name=gwenview) | [themedia](https://aur.archlinux.org/packages/themedia/) | [konqueror](https://www.archlinux.org/packages/?name=konqueror) | [lightdm-webkit-theme-contemporary](https://aur.archlinux.org/packages/lightdm-webkit-theme-contemporary/) |
| Trinity | TQt | TWin | Kicker | Konsole | Konqueror | KCalc | Kwrite Kate | Kuickshow | Kaffeine | Konqueror | TDM |
| [Xfce](/index.php/Xfce_(Italiano) "Xfce (Italiano)") | [gtk2](https://www.archlinux.org/packages/?name=gtk2) [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [xfwm4](https://www.archlinux.org/packages/?name=xfwm4) | [xfce4-panel](https://www.archlinux.org/packages/?name=xfce4-panel) | [xfce4-terminal](https://www.archlinux.org/packages/?name=xfce4-terminal) | [thunar](https://www.archlinux.org/packages/?name=thunar) | [galculator](https://www.archlinux.org/packages/?name=galculator) | [mousepad](https://www.archlinux.org/packages/?name=mousepad) | [ristretto](https://www.archlinux.org/packages/?name=ristretto) | [parole](https://www.archlinux.org/packages/?name=parole) | [midori](https://www.archlinux.org/packages/?name=midori) | [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) |

#### Peso delle risorse di sistema

In termini di risorse di sistema, GNOME e KDE sono ambienti desktop più *pesanti*. Non solo installazioni complete consumano più spazio su disco rispetto alle alternative leggere (Enlightenment, LXDE, Xfce e Razor-qt), ma anche più risorse di CPU e memoria durante il loro utilizzo. Questo perché GNOME e KDE sono da considerarsi come ambienti *full-optional'*: ovvero offrono un contesto più completo e ben integrato.

D'altro canto Enlightenment, LXDE,Xfce e Razor-qt, sono mabienti desktop più *leggeri*. Sono progettati per lavorare bene su hardware di età superiore o basso consumo e generalmente consumano meno risorse di sistema durante l'uso. Ciò si ottiene non includendo le caratteristiche *extra* (che si potrebbero definire una *gonfiatura*, o comunque superflui).

#### Familiarità degli Ambienti Desktop

Molti utenti descrivono KDE come ambiente *simile a Windows* e GNOME come *Simile a Mac*. Questo paragone è molto soggettivo e non corrisponde allo stato reale, dal momento che entrambi gli ambienti desktop possono essere personalizzati per emulare i sistemi operativi Windows o Mac. Vedere *[É KDE più simile a Windows rispetto a Gnome?](http://www.psychocats.net/ubuntucat/is-kde-more-windows-like-than-gnome/)* e *[KDE vs Gnome](http://www.jeffwu.net/?p=71)* per ulteriori informazioni. ([Linux non è Windows](http://linux.oneandoneis2.org/LNW.htm) è un'altra interessante risorsa da consultare.)

## Ambienti Personalizzati

Gli ambienti desktop rappresentano il mezzo più semplice di installare un*ambiente*grafico completo. Tuttavia, gli utenti sono liberi di costruire e personalizzare il proprio ambiente grafico in molti modi, se nessuno dei più diffusi ambienti desktop soddisfano le proprie esigenze. In generale, la costruzione di un ambiente personalizzato comporta la selezione di un idoneo [Window Manager](/index.php/Window_manager_(Italiano) "Window manager (Italiano)") un [List of Applications#Taskbars / Panels / Docks|taskbar]], e un numero di applicazioni leggere (una scelta minimalista di solito comprende un [emulatore di terminale](/index.php/List_of_applications_(Italiano)#Emulatori_di_terminale "List of applications (Italiano)"), un [file manager](/index.php/List_of_applications_(Italiano)#File_manager "List of applications (Italiano)") e un [editor di testi](/index.php/List_of_applications_(Italiano)#Editor_di_Testi "List of applications (Italiano)")).