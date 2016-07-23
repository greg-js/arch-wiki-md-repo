Un [Desktop environment](https://en.wikipedia.org/wiki/it:Desktop_environment "wikipedia:it:Desktop environment") fornisce una *completa* interfaccia Grafica Utente (GUI) per un sistema, abbinando insieme una serie di client [X](https://en.wikipedia.org/wiki/it:X_Window_System "wikipedia:it:X Window System") scritti utilizzando widget-toolkit ed insiemi di librerie comuni.

## Contents

*   [1 X Window System](#X_Window_System)
*   [2 Ambienti Desktop](#Ambienti_Desktop)
    *   [2.1 Lista degli Ambienti Desktop](#Lista_degli_Ambienti_Desktop)
        *   [2.1.1 Supportati ufficialmente](#Supportati_ufficialmente)
        *   [2.1.2 Non supportati ufficialmente](#Non_supportati_ufficialmente)
    *   [2.2 Comparazione tra i vari Ambienti Desktop](#Comparazione_tra_i_vari_Ambienti_Desktop)
        *   [2.2.1 Peso delle risorse di sistema](#Peso_delle_risorse_di_sistema)
        *   [2.2.2 Familiarità degli Ambienti Desktop](#Familiarit.C3.A0_degli_Ambienti_Desktop)
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

	[http://gnustep.org/](http://gnustep.org/) || [windowmaker](https://www.archlinux.org/packages/?name=windowmaker)

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

	[http://wiki.sugarlabs.org/](http://wiki.sugarlabs.org/) || [sugar](https://aur.archlinux.org/packages/sugar/)

*   **[Trinity](/index.php/Trinity "Trinity")** — Il progetto "Trinity Desktop Environment" (TDE) è un ambiente desktop per computer che utilizzano sistemi operativi Unix-like, con l'obbiettivo primario di conservare l'aspetto e il sistema di KDE 3.5.

	[http://www.trinitydesktop.org/](http://www.trinitydesktop.org/) || See [Trinity](/index.php/Trinity "Trinity")

*   **[Unity](/index.php/Unity "Unity")** — Unity è una shell per GNOME disegnata da Canonical per Ubuntu.

	[http://unity.ubuntu.com/](http://unity.ubuntu.com/) || [unity](https://aur.archlinux.org/packages/unity/)

### Comparazione tra i vari Ambienti Desktop

*Questa sezione cerca di tracciare un confronto tra i più diffusi ambienti desktop. Si noti che l'esperienza in prima persona è l'unico modo efficace per valutare se davvero un ambiente desktop più adatta alle vostre esigenze.*

[confronto fra i vari Ambienti Desktop](https://en.wikipedia.org/wiki/it:Comparison_of_X_Window_System_desktop_environments "wikipedia:it:Comparison of X Window System desktop environments")

<caption>Panoramica sugli ambienti desktop</caption>
| Ambiente desktop | Libreria di Sviluppo | Gestore delle finestre | Barra delle applicazioni | Emulatore di Terminale | File manager | calcolatrice | Editor di testo | Visualizzatore di immagini | Lettore multimediale | Browser Web | Gestore della sessione |
| [Cinnamon](/index.php/Cinnamon "Cinnamon") | [GTK+](/index.php/GTK%2B "GTK+") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | Muffin
[muffin](https://www.archlinux.org/packages/?name=muffin) | Cinnamon
[cinnamon](https://www.archlinux.org/packages/?name=cinnamon) | [GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) | [Nemo](/index.php/Nemo "Nemo")
[nemo](https://www.archlinux.org/packages/?name=nemo) | [Calculator](https://en.wikipedia.org/wiki/GCalctool "wikipedia:GCalctool")
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](/index.php/Gedit "Gedit")
[gedit](https://www.archlinux.org/packages/?name=gedit) | [Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")
[eog](https://www.archlinux.org/packages/?name=eog) | [Totem](https://en.wikipedia.org/wiki/Totem_(software) "wikipedia:Totem (software)")
[totem](https://www.archlinux.org/packages/?name=totem) | [Firefox](/index.php/Firefox "Firefox")
[firefox](https://www.archlinux.org/packages/?name=firefox) | [LightDM](/index.php/LightDM "LightDM") GTK+ Greeter
[lightdm-gtk3-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk3-greeter) |
| [Deepin](/index.php/Deepin "Deepin") | [GTK+](/index.php/GTK%2B "GTK+") 2/3
[gtk2](https://www.archlinux.org/packages/?name=gtk2) [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [Compiz](/index.php/Compiz "Compiz")
[compiz-devel](https://aur.archlinux.org/packages/compiz-devel/) | Dock
[deepin-desktop-environment](https://aur.archlinux.org/packages/deepin-desktop-environment/) | Deepin Terminal
[deepin-terminal](https://www.archlinux.org/packages/?name=deepin-terminal) | [GNOME Files](/index.php/GNOME_Files "GNOME Files")
[nautilus](https://www.archlinux.org/packages/?name=nautilus) | [Calculator](https://en.wikipedia.org/wiki/GCalctool "wikipedia:GCalctool")
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](/index.php/Gedit "Gedit")
[gedit](https://www.archlinux.org/packages/?name=gedit) | [Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")
[eog](https://www.archlinux.org/packages/?name=eog) | DPlayer
[deepin-media-player](https://aur.archlinux.org/packages/deepin-media-player/) | [Firefox](/index.php/Firefox "Firefox")
[firefox](https://www.archlinux.org/packages/?name=firefox) | [LightDM](/index.php/LightDM "LightDM") Deepin Greeter
[deepin-desktop-environment](https://aur.archlinux.org/packages/deepin-desktop-environment/) |
| [EDE](/index.php/Equinox_Desktop_Environment "Equinox Desktop Environment") | [FLTK](http://www.fltk.org/)
[fltk](https://www.archlinux.org/packages/?name=fltk) | [PekWM](/index.php/PekWM "PekWM")
[ede](https://aur.archlinux.org/packages/ede/) | EDE Panel
[ede](https://aur.archlinux.org/packages/ede/) | [XTerm](/index.php/Xterm "Xterm")
[xterm](https://www.archlinux.org/packages/?name=xterm) | Fluff
[fluff](https://aur.archlinux.org/packages/fluff/) | Calculator
[ede](https://aur.archlinux.org/packages/ede/) | Editor
[fltk-editor](https://aur.archlinux.org/packages/fltk-editor/) | Image Viewer
[ede](https://aur.archlinux.org/packages/ede/) | flmusic
[flmusic](https://aur.archlinux.org/packages/flmusic/) | [Dillo](/index.php/Dillo "Dillo")
[dillo](https://www.archlinux.org/packages/?name=dillo) | [XDM](/index.php/XDM "XDM")
[xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm) |
| [Enlightenment](/index.php/Enlightenment_(Italiano) "Enlightenment (Italiano)") | [Elementary](https://phab.enlightenment.org/w/elementary/)
[elementary](https://www.archlinux.org/packages/?name=elementary) | Enlightenment
[enlightenment](https://www.archlinux.org/packages/?name=enlightenment) | Enlightenment
[enlightenment](https://www.archlinux.org/packages/?name=enlightenment) | [Terminology](http://www.enlightenment.org/p.php?p=about/terminology)
[terminology](https://www.archlinux.org/packages/?name=terminology) | [EFM](https://trac.enlightenment.org/e/wiki/EFM)
[enlightenment](https://www.archlinux.org/packages/?name=enlightenment) | Equate
[equate-git](https://aur.archlinux.org/packages/equate-git/) | Ecrire
[ecrire-git](https://aur.archlinux.org/packages/ecrire-git/) | [Ephoto](https://trac.enlightenment.org/e/wiki/Ephoto)
[ephoto-git](https://aur.archlinux.org/packages/ephoto-git/) | [Enjoy](https://trac.enlightenment.org/e/wiki/Enjoy)
[enjoy-git](https://aur.archlinux.org/packages/enjoy-git/) | [Eve](https://trac.enlightenment.org/e/wiki/Eve)
[eve-git](https://aur.archlinux.org/packages/eve-git/) | [XDM](/index.php/XDM "XDM")
[xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm) |
| [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)") | [GTK+](/index.php/GTK%2B "GTK+") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | [Mutter](https://en.wikipedia.org/wiki/Mutter_(window_manager) "wikipedia:Mutter (window manager)")
[mutter](https://www.archlinux.org/packages/?name=mutter) | [GNOME Shell](https://en.wikipedia.org/wiki/GNOME_Shell "wikipedia:GNOME Shell")
[gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell) | [GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) | [GNOME Files](/index.php/GNOME_Files "GNOME Files")
[nautilus](https://www.archlinux.org/packages/?name=nautilus) | [Calculator](https://en.wikipedia.org/wiki/GCalctool "wikipedia:GCalctool")
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](/index.php/Gedit "Gedit")
[gedit](https://www.archlinux.org/packages/?name=gedit) | [Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")
[eog](https://www.archlinux.org/packages/?name=eog) | [Totem](https://en.wikipedia.org/wiki/Totem_(software) "wikipedia:Totem (software)")
[totem](https://www.archlinux.org/packages/?name=totem) | [Epiphany](/index.php/Epiphany "Epiphany")
[epiphany](https://www.archlinux.org/packages/?name=epiphany) | [GDM](/index.php/GDM "GDM")
[gdm](https://www.archlinux.org/packages/?name=gdm) |
| [GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback") | [GTK+](/index.php/GTK%2B "GTK+") 2/3
[gtk2](https://www.archlinux.org/packages/?name=gtk2) [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [Metacity](https://en.wikipedia.org/wiki/Metacity "wikipedia:Metacity")
[metacity](https://www.archlinux.org/packages/?name=metacity) | [GNOME Panel](https://en.wikipedia.org/wiki/GNOME_Panel "wikipedia:GNOME Panel")
[gnome-panel](https://www.archlinux.org/packages/?name=gnome-panel) | [GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) | [GNOME Files](/index.php/GNOME_Files "GNOME Files")
[nautilus](https://www.archlinux.org/packages/?name=nautilus) | [Calculator](https://en.wikipedia.org/wiki/GCalctool "wikipedia:GCalctool")
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](/index.php/Gedit "Gedit")
[gedit](https://www.archlinux.org/packages/?name=gedit) | [Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")
[eog](https://www.archlinux.org/packages/?name=eog) | [Totem](https://en.wikipedia.org/wiki/Totem_(software) "wikipedia:Totem (software)")
[totem](https://www.archlinux.org/packages/?name=totem) | [Epiphany](/index.php/Epiphany "Epiphany")
[epiphany](https://www.archlinux.org/packages/?name=epiphany) | [GDM](/index.php/GDM "GDM")
[gdm](https://www.archlinux.org/packages/?name=gdm) |
| [GNUstep](/index.php?title=GNUstep&action=edit&redlink=1 "GNUstep (page does not exist)") | [GNUstep](http://gnustep.org/)
[gnustep-core](https://www.archlinux.org/groups/x86_64/gnustep-core/) | [Window Maker](/index.php/Window_Maker "Window Maker")
[windowmaker](https://www.archlinux.org/packages/?name=windowmaker) | [Window Maker](/index.php/Window_Maker "Window Maker")
[windowmaker](https://www.archlinux.org/packages/?name=windowmaker) | [Terminal](http://gap.nongnu.org/terminal/index.html)
[gnustep-terminal](https://aur.archlinux.org/packages/gnustep-terminal/) | [GWorkspace](http://www.gnustep.org/experience/GWorkspace.html)
[gworkspace](https://aur.archlinux.org/packages/gworkspace/) | [Calculator](http://www.gnustep.org/experience/examples.html)
[gnustep-examples](https://aur.archlinux.org/packages/gnustep-examples/) | [Ink](http://www.gnustep.org/experience/examples.html)
[gnustep-examples](https://aur.archlinux.org/packages/gnustep-examples/) | [LaternaMagica](http://gap.nongnu.org/laternamagica/index.html)
[laternamagica](https://aur.archlinux.org/packages/laternamagica/) | [Cynthiune](http://gap.nongnu.org/cynthiune/index.html)
[cynthiune](https://aur.archlinux.org/packages/cynthiune/) | [SWK Browser](http://wiki.gnustep.org/index.php/SimpleWebKit)
[swkbrowser-svn](https://aur.archlinux.org/packages/swkbrowser-svn/) | [XDM](/index.php/XDM "XDM")
[xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm) |
| [Hawaii](/index.php/Hawaii "Hawaii") | [Qt](/index.php/Qt "Qt") 5
[qt5](https://www.archlinux.org/groups/x86_64/qt5/) | Weston
[weston](https://www.archlinux.org/packages/?name=weston) | Hawaii Shell
[hawaii-shell-git](https://aur.archlinux.org/packages/hawaii-shell-git/) | Terminal
[hawaii-terminal-git](https://aur.archlinux.org/packages/hawaii-terminal-git/) | Swordfish
[swordfish-git](https://aur.archlinux.org/packages/swordfish-git/) | Calculator
<small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=qt5-calculator)</small> | TEA
<small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=tea-qt5)</small> | EyeSight
[eyesight-git](https://aur.archlinux.org/packages/eyesight-git/) | Cinema
<small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=cinema-git)</small> | QupZilla
[qupzilla](https://www.archlinux.org/packages/?name=qupzilla) | SDDM
[sddm](https://www.archlinux.org/packages/?name=sddm) |
| [KDE](/index.php/KDE_(Italiano) "KDE (Italiano)") | [Qt](/index.php/Qt "Qt") 4
[qt4](https://www.archlinux.org/packages/?name=qt4) | [KWin](https://en.wikipedia.org/wiki/KWin "wikipedia:KWin")
[kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/) | [Plasma Desktop](https://en.wikipedia.org/wiki/KDE_Plasma_Workspaces#Desktop "wikipedia:KDE Plasma Workspaces")
[kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/) | [Konsole](http://konsole.kde.org/)
[kdebase-konsole](https://www.archlinux.org/packages/?name=kdebase-konsole) | [Dolphin](http://dolphin.kde.org/)
[kdebase-dolphin](https://www.archlinux.org/packages/?name=kdebase-dolphin) | [KCalc](http://www.kde.org/applications/utilities/kcalc/)
[kdeutils-kcalc](https://www.archlinux.org/packages/?name=kdeutils-kcalc) | [KWrite/Kate](http://kate-editor.org/)
[kdebase-kwrite](https://www.archlinux.org/packages/?name=kdebase-kwrite) [kdesdk-kate](https://www.archlinux.org/packages/?name=kdesdk-kate) | [Gwenview](http://gwenview.sourceforge.net/)
[kdegraphics-gwenview](https://www.archlinux.org/packages/?name=kdegraphics-gwenview) | [Dragon Player](http://www.kde.org/applications/multimedia/dragonplayer/)
[kdemultimedia-dragonplayer](https://www.archlinux.org/packages/?name=kdemultimedia-dragonplayer) | [Konqueror](http://www.konqueror.org/)
[kdebase-konqueror](https://www.archlinux.org/packages/?name=kdebase-konqueror) | [KDM](/index.php/KDM "KDM")
[kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/) |
| [LXDE](/index.php/LXDE_(Italiano) "LXDE (Italiano)") | [GTK+](/index.php/GTK%2B "GTK+") 2
[gtk2](https://www.archlinux.org/packages/?name=gtk2) | [Openbox](/index.php/Openbox "Openbox")
[openbox](https://www.archlinux.org/packages/?name=openbox) | [LXPanel](http://wiki.lxde.org/en/LXPanel)
[lxpanel](https://www.archlinux.org/packages/?name=lxpanel) | [LXTerminal](http://wiki.lxde.org/en/LXTerminal)
[lxterminal](https://www.archlinux.org/packages/?name=lxterminal) | [PCManFM](/index.php/PCManFM "PCManFM")
[pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm) | [Galculator](http://galculator.sourceforge.net/)
[galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2) | [Leafpad](http://tarot.freeshell.org/leafpad/)
[leafpad](https://www.archlinux.org/packages/?name=leafpad) | [GPicView](http://wiki.lxde.org/en/GPicView)
[gpicview](https://www.archlinux.org/packages/?name=gpicview) | [LXMusic](http://wiki.lxde.org/en/LXMusic)
[lxmusic](https://www.archlinux.org/packages/?name=lxmusic) | [Firefox](/index.php/Firefox "Firefox")
[firefox](https://www.archlinux.org/packages/?name=firefox) | [LXDM](/index.php/LXDM "LXDM")
[lxdm](https://www.archlinux.org/packages/?name=lxdm) |
| [MATE](/index.php/MATE_(Italiano) "MATE (Italiano)") | [GTK+](/index.php/GTK%2B "GTK+") 2
[gtk2](https://www.archlinux.org/packages/?name=gtk2) | Marco
[mate-window-manager](https://www.archlinux.org/packages/?name=mate-window-manager) | MATE Panel
[mate-panel](https://www.archlinux.org/packages/?name=mate-panel) | MATE Terminal
[mate-terminal](https://www.archlinux.org/packages/?name=mate-terminal) | Caja
[mate-file-manager](https://www.archlinux.org/packages/?name=mate-file-manager) | Calculator
[mate-calc](https://www.archlinux.org/packages/?name=mate-calc) | pluma
[mate-text-editor](https://www.archlinux.org/packages/?name=mate-text-editor) | Eye of MATE
[mate-image-viewer](https://www.archlinux.org/packages/?name=mate-image-viewer) | Whaaw!
[whaawmp](https://www.archlinux.org/packages/?name=whaawmp) | [Midori](/index.php/Midori "Midori")
[midori](https://www.archlinux.org/packages/?name=midori) | [LightDM](/index.php/LightDM "LightDM") GTK+ Greeter
[lightdm-gtk2-greeter](https://aur.archlinux.org/packages/lightdm-gtk2-greeter/) |
| [Pantheon](/index.php/Pantheon "Pantheon") | [GTK+](/index.php/GTK%2B "GTK+") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | [Gala](https://launchpad.net/gala)
[gala-bzr](https://aur.archlinux.org/packages/gala-bzr/) | [Plank](https://launchpad.net/plank)/[Wingpanel](https://launchpad.net/wingpanel)
[plank](https://www.archlinux.org/packages/?name=plank) [wingpanel](https://aur.archlinux.org/packages/wingpanel/) | [Pantheon Terminal](https://launchpad.net/pantheon-terminal)
[pantheon-terminal](https://www.archlinux.org/packages/?name=pantheon-terminal) | [Pantheon Files](https://launchpad.net/pantheon-files)
[pantheon-files](https://www.archlinux.org/packages/?name=pantheon-files) | [Calculator](https://en.wikipedia.org/wiki/GCalctool "wikipedia:GCalctool")
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [Scratch](https://launchpad.net/scratch)
[scratch-text-editor](https://www.archlinux.org/packages/?name=scratch-text-editor) | [Shotwell](https://en.wikipedia.org/wiki/Shotwell_(software) "wikipedia:Shotwell (software)")
[shotwell](https://www.archlinux.org/packages/?name=shotwell) | [Totem](https://en.wikipedia.org/wiki/Totem_(software) "wikipedia:Totem (software)")
[totem](https://www.archlinux.org/packages/?name=totem) | [Midori](/index.php/Midori "Midori")
[midori-gtk3](https://www.archlinux.org/packages/?name=midori-gtk3) | [LightDM](/index.php/LightDM "LightDM") Pantheon Greeter
[lightdm-pantheon-greeter](https://aur.archlinux.org/packages/lightdm-pantheon-greeter/) |
| [Razor-qt](/index.php/Razor-qt "Razor-qt") (LXDE-Qt) | [Qt](/index.php/Qt "Qt") 4
[qt4](https://www.archlinux.org/packages/?name=qt4) | [Openbox](/index.php/Openbox "Openbox")
[openbox](https://www.archlinux.org/packages/?name=openbox) | Razor Panel
[razor-qt](https://aur.archlinux.org/packages/razor-qt/)
([lxqt-panel-git](https://aur.archlinux.org/packages/lxqt-panel-git/)) | QTerminal
[qterminal-git](https://aur.archlinux.org/packages/qterminal-git/) | PCManFM-Qt
[pcmanfm-qt-git](https://aur.archlinux.org/packages/pcmanfm-qt-git/) | [SpeedCrunch](http://speedcrunch.org/)
[speedcrunch](https://www.archlinux.org/packages/?name=speedcrunch) | JuffEd
[juffed](https://aur.archlinux.org/packages/juffed/) | LxImage-Qt
[lximage-qt-git](https://aur.archlinux.org/packages/lximage-qt-git/) | Qmmp
[qmmp](https://www.archlinux.org/packages/?name=qmmp) | QupZilla
[qupzilla](https://www.archlinux.org/packages/?name=qupzilla) | [LightDM](/index.php/LightDM "LightDM") Razor-qt Greeter (SDDM)
[lightdm-razor-greeter](https://aur.archlinux.org/packages/lightdm-razor-greeter/)
([sddm](https://www.archlinux.org/packages/?name=sddm)) |
| [ROX](/index.php/ROX "ROX") | [GTK+](/index.php/GTK%2B "GTK+") 2
[gtk2](https://www.archlinux.org/packages/?name=gtk2) | [OroboROX](http://rox.sourceforge.net/desktop/OroboROX.html)
[oroborox](https://aur.archlinux.org/packages/oroborox/) | [ROX-Filer](http://rox.sourceforge.net/desktop/ROX-Filer.html)
[rox](https://www.archlinux.org/packages/?name=rox) | [ROXTerm](http://roxterm.sourceforge.net/)
[roxterm](https://www.archlinux.org/packages/?name=roxterm) ([roxterm-gtk2](https://aur.archlinux.org/packages/roxterm-gtk2/)) | [ROX-Filer](http://rox.sourceforge.net/desktop/ROX-Filer.html)
[rox](https://www.archlinux.org/packages/?name=rox) | [Galculator](http://galculator.sourceforge.net/)
[galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2) | [Edit](http://rox.sourceforge.net/desktop/Edit.html)
[rox-edit](https://aur.archlinux.org/packages/rox-edit/) | [Picky](http://rox.sourceforge.net/desktop/picky.html)
<small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=picky)</small> | [MusicBox](http://rox.sourceforge.net/desktop/Software/Audio_Video/MusicBox.html)
<small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=musicbox)</small> | [Midori](/index.php/Midori "Midori")
[midori](https://www.archlinux.org/packages/?name=midori) | [LightDM](/index.php/LightDM "LightDM") GTK+ Greeter
[lightdm-gtk2-greeter](https://aur.archlinux.org/packages/lightdm-gtk2-greeter/) |
| [Sugar](/index.php/Sugar_(Italiano) "Sugar (Italiano)") | [GTK+](/index.php/GTK%2B "GTK+") 2/3
[gtk2](https://www.archlinux.org/packages/?name=gtk2) [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [Metacity](https://en.wikipedia.org/wiki/Metacity "wikipedia:Metacity")
[metacity](https://www.archlinux.org/packages/?name=metacity) | Sugar
[sugar](https://aur.archlinux.org/packages/sugar/) | Terminal
[sugar-activity-terminal](https://aur.archlinux.org/packages/sugar-activity-terminal/) | Sugar Journal
[sugar](https://aur.archlinux.org/packages/sugar/) | Calculate
[sugar-activity-calculate](https://aur.archlinux.org/packages/sugar-activity-calculate/) | Write
[sugar-activity-write](https://aur.archlinux.org/packages/sugar-activity-write/) | ImageViewer
[sugar-activity-imageviewer](https://aur.archlinux.org/packages/sugar-activity-imageviewer/) | Jukebox
[sugar-activity-jukebox](https://aur.archlinux.org/packages/sugar-activity-jukebox/) | Browse
[sugar-activity-browse](https://aur.archlinux.org/packages/sugar-activity-browse/) | [LightDM](/index.php/LightDM "LightDM") GTK+ Greeter
[lightdm-gtk3-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk3-greeter) |
| [Trinity](/index.php/Trinity "Trinity") | [Qt](/index.php/Qt "Qt") 3 | TWin | Kicker | Konsole | Konqueror | KCalc | Kwrite / Kate | Kuickshow | Kaffeine | Konqueror | TDM |
| [Unity](/index.php/Unity "Unity") | [GTK+](/index.php/GTK%2B "GTK+") 2/3
[gtk2](https://www.archlinux.org/packages/?name=gtk2) [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [Compiz](/index.php/Compiz "Compiz")
[compiz-devel](https://aur.archlinux.org/packages/compiz-devel/) | Unity
[unity](https://aur.archlinux.org/packages/unity/) | [GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) | [GNOME Files](/index.php/GNOME_Files "GNOME Files")
[nautilus](https://www.archlinux.org/packages/?name=nautilus) | [Calculator](https://en.wikipedia.org/wiki/GCalctool "wikipedia:GCalctool")
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](/index.php/Gedit "Gedit")
[gedit](https://www.archlinux.org/packages/?name=gedit) | [Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")
[eog](https://www.archlinux.org/packages/?name=eog) | [Totem](https://en.wikipedia.org/wiki/Totem_(software) "wikipedia:Totem (software)")
[totem](https://www.archlinux.org/packages/?name=totem) | [Firefox](/index.php/Firefox "Firefox")
[firefox](https://www.archlinux.org/packages/?name=firefox) | [LightDM](/index.php/LightDM "LightDM") Unity Greeter
[lightdm-unity-greeter](https://aur.archlinux.org/packages/lightdm-unity-greeter/) |
| [Xfce](/index.php/Xfce_(Italiano) "Xfce (Italiano)") | [GTK+](/index.php/GTK%2B "GTK+") 2
[gtk2](https://www.archlinux.org/packages/?name=gtk2) | [Xfwm4](http://docs.xfce.org/xfce/xfwm4/start)
[xfwm4](https://www.archlinux.org/packages/?name=xfwm4) | [Xfce Panel](http://docs.xfce.org/xfce/xfce4-panel/start)
[xfce4-panel](https://www.archlinux.org/packages/?name=xfce4-panel) | [Terminal](http://www.xfce.org/projects/terminal)
[xfce4-terminal](https://www.archlinux.org/packages/?name=xfce4-terminal) | [Thunar](/index.php/Thunar "Thunar")
[thunar](https://www.archlinux.org/packages/?name=thunar) | [Galculator](http://galculator.sourceforge.net/)
[galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2) | Mousepad
[mousepad](https://www.archlinux.org/packages/?name=mousepad) | [Ristretto](http://goodies.xfce.org/projects/applications/ristretto)
[ristretto](https://www.archlinux.org/packages/?name=ristretto) | [Parole](http://goodies.xfce.org/projects/applications/parole)
[parole](https://www.archlinux.org/packages/?name=parole) | [Midori](/index.php/Midori "Midori")
[midori](https://www.archlinux.org/packages/?name=midori) | [LightDM](/index.php/LightDM "LightDM") GTK+ Greeter
[lightdm-gtk2-greeter](https://aur.archlinux.org/packages/lightdm-gtk2-greeter/) |

#### Peso delle risorse di sistema

In termini di risorse di sistema, GNOME e KDE sono ambienti desktop più *pesanti*. Non solo installazioni complete consumano più spazio su disco rispetto alle alternative leggere (Enlightenment, LXDE, Xfce e Razor-qt), ma anche più risorse di CPU e memoria durante il loro utilizzo. Questo perché GNOME e KDE sono da considerarsi come ambienti *full-optional'*: ovvero offrono un contesto più completo e ben integrato.

D'altro canto Enlightenment, LXDE,Xfce e Razor-qt, sono mabienti desktop più *leggeri*. Sono progettati per lavorare bene su hardware di età superiore o basso consumo e generalmente consumano meno risorse di sistema durante l'uso. Ciò si ottiene non includendo le caratteristiche *extra* (che si potrebbero definire una *gonfiatura*, o comunque superflui).

#### Familiarità degli Ambienti Desktop

Molti utenti descrivono KDE come ambiente *simile a Windows* e GNOME come *Simile a Mac*. Questo paragone è molto soggettivo e non corrisponde allo stato reale, dal momento che entrambi gli ambienti desktop possono essere personalizzati per emulare i sistemi operativi Windows o Mac. Vedere *[É KDE più simile a Windows rispetto a Gnome?](http://www.psychocats.net/ubuntucat/is-kde-more-windows-like-than-gnome/)* e *[KDE vs Gnome](http://www.jeffwu.net/?p=71)* per ulteriori informazioni. ([Linux non è Windows](http://linux.oneandoneis2.org/LNW.htm) è un'altra interessante risorsa da consultare.)

## Ambienti Personalizzati

Gli ambienti desktop rappresentano il mezzo più semplice di installare un*ambiente*grafico completo. Tuttavia, gli utenti sono liberi di costruire e personalizzare il proprio ambiente grafico in molti modi, se nessuno dei più diffusi ambienti desktop soddisfano le proprie esigenze. In generale, la costruzione di un ambiente personalizzato comporta la selezione di un idoneo [Window Manager](/index.php/Window_manager_(Italiano) "Window manager (Italiano)") un [List of Applications#Taskbars / Panels / Docks|taskbar]], e un numero di applicazioni leggere (una scelta minimalista di solito comprende un [emulatore di terminale](/index.php/List_of_applications_(Italiano)#Emulatori_di_terminale "List of applications (Italiano)"), un [file manager](/index.php/List_of_applications_(Italiano)#File_manager "List of applications (Italiano)") e un [editor di testi](/index.php/List_of_applications_(Italiano)#Editor_di_Testi "List of applications (Italiano)")).