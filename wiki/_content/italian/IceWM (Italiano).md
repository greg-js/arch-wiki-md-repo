Secondo [Wikipedia](http://it.wikipedia.org/wiki/Icewm):

	_Negli ambienti Unix, IceWM è un Window manager per l'infrastruttura grafica dell'X Window System, scritto da Marko Maček. È stato creato da zero in C++ ed è rilasciato sotto i termini della GNU Lesser General Public License. È relativamente leggero in termini di consumo di memoria e di CPU, e si presenta con temi che gli consentono di imitare l'interfaccia utente di Windows 95, OS/2, Motif e altre GUI. IceWM è l'ideale per avere un look e atmosfera speciale senza dimenticare aspetti fondamentali come la leggerezza e la personalizzazione._

IceWM è estremamente configurabile ed è quasi equiparabile ad una via di mezzo tra un semplicissimo [DE](/index.php/Desktop_Environment_(Italiano) "Desktop Environment (Italiano)") e un [WM](/index.php/Window_Manager_(Italiano) "Window Manager (Italiano)") molto ricco di features.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Lanciare IceWm in maniera stand-alone](#Lanciare_IceWm_in_maniera_stand-alone)
*   [3 IceWm come WM per un Desktop Environment](#IceWm_come_WM_per_un_Desktop_Environment)
*   [4 Configurazione](#Configurazione)
    *   [4.1 Menù](#Men.C3.B9)
    *   [4.2 Temi](#Temi)
*   [5 File Managers](#File_Managers)
*   [6 Articoli correlati](#Articoli_correlati)

## Installazione

[Installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") [icewm](https://www.archlinux.org/packages/?name=icewm) dai [repositories ufficiali](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)").

In alternativa, l'ultima versione del branch testing ([icewm-testing](https://aur.archlinux.org/packages/icewm-testing/)) e la versione CVS ([icewm-cvs](https://aur.archlinux.org/packages/icewm-cvs/)) sono disponibili in [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)"). Questa versioni aggiungono nuove caratteristiche come il supporto a RandR.

## Lanciare IceWm in maniera stand-alone

Per usare IceWm in maniera stand-standalone aggiungere a `~/.xinitrc`:

 `exec icewm` 

`icewm-session` lancia: `icewm`, `icewmbg`, `icewmtray`, quindi per avere queste funzionalità usare in `~/.xinitrc`:

 `exec icewm-session` 

Vedere [xinitrc](/index.php/Xinitrc_(Italiano) "Xinitrc (Italiano)") per i dettagli su come preservare la sessione logind (utile ad esempio per l'automount dei dispositivi usb).

## IceWm come WM per un Desktop Environment

Per usare IceWM come window manager predefinito per un DE seguire le istruzioni della [pagina wiki di Openbox](/index.php/Openbox_(Italiano)#Gestore_finestre_per_ambienti_desktop "Openbox (Italiano)"). (Questo probabilmente funzionerà per tutti i WM)

## Configurazione

Anche se la configurazione di IceWM è originariamente testuale, sono disponibili strumenti ad interfaccia grafica, come [icewm-utils](https://aur.archlinux.org/packages/icewm-utils/), disponibile in [community]. Comunque questi strumenti sono relativamente vecchi e molti utenti preferiscono semplicemente editare i file di configurazione.

Per cambiare la configurazione di default di icewm, copiare semplicemente i file di default da `/usr/share/icewm/` a `~/.icewm/`, per esempio:

**Nota:** Usare questi comandi come utente normale, non come root.

```
$ mkdir ~/.icewm/
$ cp -R /usr/share/icewm/* ~/.icewm/

```

*   `preferences` è il file di configurazione generale di IceWM.
*   `menu` controlla il contenuto del menù applicazioni di IceWM.
*   `keys` permette di personalizzare le scorciatoie da tastiera.
*   `toolbar` riga di icone e lanciatori nella taskbar.
*   `winoptions` comportamento delle singole applicazioni.
*   `theme` temi percorso/nome
*   `startup` script o comandi (resi eseguibili) da eseguire all'avvio di IceWm
*   `shutdown` script o comandi (resi eseguibili) da eseguire alla chiusura di IceWm

### Menù

*   [menumaker](https://www.archlinux.org/packages/?name=menumaker) (disponibile in [Community]) è uno script Python che riempie automaticamente il proprio menù applicazioni con le applicazioni installate nel sistema. Anche se potrebbe generare un menù con molte voci indesiderate, è più agevole che modificare manualmente il file di configurazione del menù. Quando si esegue Menumaker, utilizzare il flag -f per sovrascrivere il file di configurazione esistente:

```
# mmaker -f icewm

```

*   Un altro tool scritto però in perl è [archlinux-xdg-menu](https://www.archlinux.org/packages/?name=archlinux-xdg-menu):

```
# xdg_menu --format icewm --fullmenu --root-menu /etc/xdg/menus/arch-applications.menu > ~/.icewm/menu

```

### Temi

Anche se alcuni temi sono inclusi di default, una scelta più ampia si trova nel pacchetto [icewm-themes](https://www.archlinux.org/packages/?name=icewm-themes), presente nel repository. Sebbene alcuni hanno un look spartano, 'vecchio Windows'. Alcuni esempi migliori (come [[1]](http://box-look.org/content/show.php/Carbonit+Ice?content=146421%7Cquesto), [[2]](http://box-look.org/content/show.php/IceBuntu?content=62935%7Cquesto) o [[3]](http://box-look.org/content/show.php/IceClearlooks?content=96346%7Cquesto)) possono essere trovati su [box-look.org](http://www.box-look.org/index.php?xcontentmode=7311).

## File Managers

Si noti che IceWM è un window manager puro, quindi non include un file manager. [PCManFM](/index.php/PCManFM "PCManFM") e [Rox Filer](/index.php/ROX "ROX") permettono di avere icone sul desktop, ma anche [iDesk](/index.php/Idesk "Idesk") può compiere questa funzione.

**Nota:** Per una lista più esaustiva di file managers, esaminare [File managers](/index.php/Category:File_managers "Category:File managers") la lista categoria.

## Articoli correlati

*   [Xinitrc](/index.php/Xinitrc_(Italiano) "Xinitrc (Italiano)")
*   [Sito ufficiale di IceWM](http://www.icewm.org/)
*   [IceWM - Wiki di Gentoo Linux](http://en.gentoo-wiki.com/wiki/IceWM)
*   [IceWM - The Cool Window Manager](http://www.osnews.com/story.php/7774/IceWM--The-Cool-Window-Manager/) - Introduzione dettagliata su OSNews
*   [IceWM - A desktop for Windows emigrants](http://polishlinux.org/apps/window-managers/icewm-a-desktop-for-windows-emmigrants/) - Panoramica e tutorial da polishlinux.org