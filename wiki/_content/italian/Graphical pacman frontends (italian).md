Quella qui riportata è una lista di interfacce grafiche per Pacman, progettate per costituire una versione grafica dello strumento di gestione pacchetti CLI (*Command Line Interface*) pacman. La lista include software basato su Gtk2, Qt, e una varietà di indicatori per pannelli di sistema. **Nessuno di questi software è ufficialmente supportato dal team di Archlinux**.

## Contents

*   [1 Interfacce grafiche per Gnome/Gtk2](#Interfacce_grafiche_per_Gnome/Gtk2)
    *   [1.1 GtkPacman](#GtkPacman)
*   [2 Interfacce grafiche per KDE/Qt](#Interfacce_grafiche_per_KDE/Qt)
    *   [2.1 Shaman](#Shaman)
    *   [2.2 AppSet](#AppSet)
    *   [2.3 Pacman / AUR Package Browser](#Pacman_/_AUR_Package_Browser)
*   [3 Indicatori per pannelli di sistema](#Indicatori_per_pannelli_di_sistema)
    *   [3.1 archup](#archup)
    *   [3.2 Chase](#Chase)
    *   [3.3 alunn](#alunn)
    *   [3.4 pacman-notifier](#pacman-notifier)
    *   [3.5 pacupdate](#pacupdate)
    *   [3.6 ZenMan](#ZenMan)
*   [4 Gestori grafici inattivi](#Gestori_grafici_inattivi)

# Interfacce grafiche per Gnome/Gtk2

### GtkPacman

GtkPacman è un'interfaccia semplice ma potente per il gestore di pacchetti di Archinux. È scritto in python, utilizzando pygtk, ed è rapido e stabile. Con gtkPacman, la gestione del sistema si riduce alla semplice pressione di pochi pulsanti. L'ultimo rilascio di GtkPacman è datato Febbraio 2008.

*   Homepage: [http://gtkpacman.berlios.de/](http://gtkpacman.berlios.de/)
*   Dettagli del pacchetto in AUR: [https://aur.archlinux.org/packages.php?ID=8027](https://aur.archlinux.org/packages.php?ID=8027)
*   Screenshots: [http://developer.berlios.de/screenshots/?group_id=4808](http://developer.berlios.de/screenshots/?group_id=4808)

**ATTTENZIONE:** Questo programma rimuove i pacchetti con l'opzione -d attiva, il che vuol dire che pacman NON controlla le dipendenze per il pacchetto in rimozione. Usare questo programma può compromettere seriamente il sistema. --[Falcata](/index.php?title=User:Falcata&action=edit&redlink=1 "User:Falcata (page does not exist)") 12:35, 29 May 2010 (EDT)

# Interfacce grafiche per KDE/Qt

### Shaman

Shaman è una GUI (*Graphical User Interface*) per la gestione dei pacchetti per Archlinux. È basato su libalpm. Ciò rappresenta un grande vantaggio, dall'integrazione nel sistema alla velocità. Inoltre, le richieste e le ricerche sono più rapide di pacman, il tutto con un alto livello di personalizzazione. Shaman soddisfa tutte le necessità di qualsiasi manager di pacchetti, come:

	Installazione/rimozione/aggiornamento dei pacchetti

	Ricerca/filtraggio dei pacchetti

	Informazioni sui pacchetti

	Operazioni di manutenzione del database

Inoltre Shaman supporta la pianificazione di aggiornamenti del database, un RSS-feed reader per i pacchetti di Archlinux e la modifica dei file di configurazione di pacman.

*   Homepage: [http://chakra-project.org/tools-shaman.html](http://chakra-project.org/tools-shaman.html)
*   Dettagli del pacchetto in AUR: [https://aur.archlinux.org/packages.php?ID=15422](https://aur.archlinux.org/packages.php?ID=15422)
*   Screenshots: [http://chakra-project.org/screenshots/tools_shaman.png](http://chakra-project.org/screenshots/tools_shaman.png)

### AppSet

AppSet è un frontend avanzato e ricco di funzioni progettato per funzionare con tutti i gestori di pacchetti di tutte le distribuzioni linux. AppSet possiede le seguenti caratteristiche:

*   Sezioni software (giochi, ufficio, multimedia, internet etc.)
*   Mostra le homepage dei pacchetti selezionati in un web browser integrato
*   Mostra le news della distribuzione in un feed reader integrato
*   Aggiorna, installa e rimuove pacchetti
*   Mostra gli aggiornamenti disponibili mediante una Tray Icon
*   Aggiorna il database dei pacchetti periodicamente
*   Informa sulle dipendenze (per esempio quando si tenta di rimuovere un pacchetto richiesto da altri già installati)
*   Comando per pulire la cache dei pacchetti (per liberare spazio su disco)
*   Avviatore intelligente che usa quello che è già installato per ottenere i privilegi di amministrazione (cercando kdesu, gksu o almeno per un xterm dove si avvia con il comando sudo)
*   Ora con il supporto ad AUR tramite Packer come backend

AppSet necessita solo delle librerie Qt come dipendenza di installazione. Può essere usato su qualunque ambiente desktop. Attualmente funziona solo sfruttando pacman su Archlinux.

**Homepage:** [http://appset.sourceforge.net/](http://appset.sourceforge.net/)
**AUR Package:** [https://aur.archlinux.org/packages.php?ID=43869](https://aur.archlinux.org/packages.php?ID=43869)
**Screenshots** [http://sourceforge.net/project/screenshots.php?group_id=376825](http://sourceforge.net/project/screenshots.php?group_id=376825)

## Pacman / AUR Package Browser

*   **PkgBrowser** — applicazione per cercare/guardare i pachetti nei repositori ed in AUR

	**Forum:** [https://bbs.archlinux.org/viewtopic.php?id=117297](https://bbs.archlinux.org/viewtopic.php?id=117297)

	[https://code.google.com/p/pkgbrowser/](https://code.google.com/p/pkgbrowser/) || [pkgbrowser](https://aur.archlinux.org/packages/pkgbrowser/)

Per installarla basta scaricare il pachetto da AUR, decomprimerlo in una directory, posizionarvisi dentro e digitare

```
makepkg -s 

```

Naturalmente si verificheranno le dipendenze, qualora non dovessero essere presenti, il sistema provvederà a richiederne il download. Fatto questo, si creerà il pacchetto pkgbrowser...pkg.tar.xz, quindi da terminale nella stessa directory, digitare

```
pacman -U pkgbrowser...pkg.tar.xz

```

Tutto qui.

# Indicatori per pannelli di sistema

### archup

Archup è una piccola (solo 44 linee di codice) applicazione in C. È sviluppato in modo da essere leggero e minimalista: notifica semplicemente la disponibilità di nuovi aggiornamenti. Archup usa GTk+ e libnotify per mostrare un popup se nuovi aggiornamenti sono disponibili.

*   Homepage: [archup](/index.php/Archup "Archup")
*   Dettagli del pacchetto in AUR: [https://aur.archlinux.org/packages.php?ID=35792](https://aur.archlinux.org/packages.php?ID=35792)
*   Screenshots: [http://developer.berlios.de/dbimage.php?id=4687](http://developer.berlios.de/dbimage.php?id=4687) , [http://developer.berlios.de/dbimage.php?id=4688](http://developer.berlios.de/dbimage.php?id=4688)

### Chase

Chase è un demone per KDE4, creato dal progetto Chakra. Chase usa libapm per gestire gli aggiornamenti, è completamente configurabile ed è integrato con Shaman e KDE4.

*   Homepage: [http://chakra-project.org/bbs/viewtopic.php?id=1303](http://chakra-project.org/bbs/viewtopic.php?id=1303)
*   Dettagli del pacchetto in AUR: [https://aur.archlinux.org/packages.php?ID=29567](https://aur.archlinux.org/packages.php?ID=29567)
*   Screenshots: [http://chakra-project.org/bbs/viewtopic.php?id=1303](http://chakra-project.org/bbs/viewtopic.php?id=1303)

### alunn

Alunn è una semplice applicazione da pannello di sistema per Archlinux. L'applet avverte l'utente ogni qualvolta ci sono pacchetti da aggiornare per pacman o quando ci sono novità sulla homepage di Archlinux. Comandi personalizzabili per aggiornare il sistema o leggere le news possono venire eseguiti con un clic sull'icona di notifica.

*   Homepage: [http://nedrebo.org/code/alunn/](http://nedrebo.org/code/alunn/)
*   Dettagli del pacchetto in AUR: [https://aur.archlinux.org/packages.php?ID=6098](https://aur.archlinux.org/packages.php?ID=6098)
*   Screenshots: [http://nedrebo.org/code/alunn/](http://nedrebo.org/code/alunn/)

### pacman-notifier

Scritto in Ruby, usa Gtk. Mostra un'icona nel pannello di sistema e mostra popup (attraverso libnotify) per la notifica di nuovi pacchetti.

*   Homepage: [http://code.google.com/p/pacman-notifier/](http://code.google.com/p/pacman-notifier/)
*   Dettagli del pacchetto in AUR: [https://aur.archlinux.org/packages.php?ID=15193](https://aur.archlinux.org/packages.php?ID=15193)
*   Screenshots: [http://code.google.com/p/pacman-notifier/](http://code.google.com/p/pacman-notifier/)

### pacupdate

Pacupdate è una piccola applicazione che notifica l'utente sugli aggiornamenti disponibili per Archlinux. Se pacupdate trova un aggiornamento per un pacchetto, mostra un popup di notifica nel pannello di sistema.

*   Homepage: [http://code.google.com/p/pacupdate/](http://code.google.com/p/pacupdate/)
*   Dettagli del pacchetto in AUR: [https://aur.archlinux.org/packages.php?ID=19068](https://aur.archlinux.org/packages.php?ID=19068)
*   Screenshots:

### ZenMan

Indicatore di aggiornamenti per il pannello di sistema, usa GTK/GNOME/zenity/libnotify.

*   Homepage:
*   Dettagli del pacchetto in AUR:[https://aur.archlinux.org/packages.php?ID=25948](https://aur.archlinux.org/packages.php?ID=25948)
*   Screenshots:[http://show.harvie.cz/screenshots/zenman-screenshot-2.png](http://show.harvie.cz/screenshots/zenman-screenshot-2.png)

# Gestori grafici inattivi

*   [Guzuta](http://guzuta.berlios.de/)
*   [PacmanManager](https://opensvn.csie.org/PacmanManager/)
*   [pacmon](http://code.google.com/p/pacmon/)
*   [Paku](https://gna.org/projects/paku/)
*   [YAPG](http://www.kde-apps.org/content/show.php/YAPG+-+Yet+Another+Pacman+Gui+?content=60052)
*   [zenity_pacgui](http://sourceforge.net/projects/zenitypacgui/)