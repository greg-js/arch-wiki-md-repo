Dal [Sito di GTK+](http://www.gtk.org):

	_GTK+, o The GIMP Toolkit, è un toolkit multi-piattaforma per creare interfacce utente (UI) grafiche. In quanto offre un set completo di strumenti, GTK+ è adatto per ogni progetto, da piccoli strumenti unici a interfacce complete di applicazioni._

GTK+, The GIMP Toolkit, fu creato inizialmente dal [Progetto GNU](/index.php/GNU_Project "GNU Project") per il [GIMP](/index.php/GIMP "GIMP"), ma ora è un toolkit molto famoso con supporto per molte lingue.

## Contents

*   [1 Programmi di configurazione](#Programmi_di_configurazione)
*   [2 Temi](#Temi)
    *   [2.1 GTK+ 1.x](#GTK.2B_1.x)
    *   [2.2 GTK+ 2.x](#GTK.2B_2.x)
    *   [2.3 GTK+ 3.x](#GTK.2B_3.x)
    *   [2.4 GTK+ e QT](#GTK.2B_e_QT)
*   [3 Configuration file](#Configuration_file)
    *   [3.1 Attivare scorciatoie da tastiera](#Attivare_scorciatoie_da_tastiera)
    *   [3.2 Velocizzare l'apertura dei menu di GNOME](#Velocizzare_l.27apertura_dei_menu_di_GNOME)
    *   [3.3 Diminuire la grandezza dei Widget](#Diminuire_la_grandezza_dei_Widget)
*   [4 Sviluppo](#Sviluppo)
    *   [4.1 Write a simple message dialog app](#Write_a_simple_message_dialog_app)
        *   [4.1.1 Bash](#Bash)
        *   [4.1.2 C](#C)
        *   [4.1.3 C++](#C.2B.2B)
        *   [4.1.4 Genie](#Genie)
        *   [4.1.5 JavaScript](#JavaScript)
        *   [4.1.6 Python](#Python)
        *   [4.1.7 Vala](#Vala)
*   [5 Resources](#Resources)

## Programmi di configurazione

Questi programmi GUI (Graphic User Interface) permettono la selezione del tema oltre alla personalizzazione del font e del cursore. Generalmente sovrascrivono il file `~/.gtkrc-2.0`.

*   [lxappearance](https://www.archlinux.org/packages/?name=lxappearance): Un tool di configurazione dal progetto [LXDE](/index.php/LXDE_(Italiano) "LXDE (Italiano)"), che non richiede altre parti di LXDE o di altri ambienti desktop (DE). Offre una personalizzazione più flessibile rispetto ad altri programmi.
*   [gtk-chtheme](https://www.archlinux.org/packages/?name=gtk-chtheme)
*   [gtk-theme-switch2](https://www.archlinux.org/packages/?name=gtk-theme-switch2)
*   [gtk2_prefs](https://www.archlinux.org/packages/?name=gtk2_prefs)

Un comando d'installazione d'esempio:

```
# pacman -S gtk-theme-switch2

```

Può essere utile guardare anche [Uniformare il look di applicazioni QT e GTK - Come posso configurare lo stile per ogni toolkit](/index.php/Uniform_Look_for_QT_and_GTK_Applications_(Italiano)#Come_posso_configurare_lo_stile_per_ogni_toolkit.3F "Uniform Look for QT and GTK Applications (Italiano)")

## Temi

### GTK+ 1.x

Le vecchia applicazioni GTK+ 1 (come xmms) quasi sempre non hanno un bel look all'inizio. La causa è data dal fatto che usano di default dei temi poco gradevoli. Per cambiare la sitazione, è necessario:

1.  scaricare ed installare dei bei temi
2.  cambiare il tema di default

Molti temi gradevoli si trovano in [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)"). Per installarli, si veda [gtk-smooth-engine](https://aur.archlinux.org/packages/gtk-smooth-engine/).

Per cambiare il tema è possibile usare _gtk-theme-switch2_. Per avviarlo basta usare il comando 'switch'.

### GTK+ 2.x

I maggiori [ambienti desktop](/index.php/Desktop_Environment_(Italiano) "Desktop Environment (Italiano)") muniscono l'utente di strumenti per configurare il tema GTK+, le icone, il font e la sua dimensione. In alternativa, si possono usare programmi come quelli appena menzionati.

È raccomandato anche [installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") alcuni temi GTK+ 2\. Il famoso tema _Clearlooks_ è incluso al pacchetto [gtk-engines](https://www.archlinux.org/packages/?name=gtk-engines).

Altri temi si possono trovare in [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)"):

*   [https://aur.archlinux.org/packages.php?O=0&K=gtk2-theme&do_Search=Go](https://aur.archlinux.org/packages.php?O=0&K=gtk2-theme&do_Search=Go)
*   [https://aur.archlinux.org/packages.php?O=0&K=gtk-theme&do_Search=Go](https://aur.archlinux.org/packages.php?O=0&K=gtk-theme&do_Search=Go)

In alternativa, le impostazioni di GTK+ possono essere configurate manualmente modificando `~/.gtkrc-2.0`. Una lista di impostazioni GTK+ possono essere trovate in [GNOME library](http://library.gnome.org/devel/gtk/stable/GtkSettings.html). Per cambiare manualmente il tema GTK+, le icone, i font e la loro grandezza, basta aggiungere le righe seguenti a `~/.gtkrc-2.0`:

 `~/.gtkrc-2.0` 

```
gtk-icon-theme-name = "[nome-del-tema-icone]"
gtk-theme-name = "[nome-del-tema]"
gtk-font-name = "[nome-del-font] [grandezza]"
```

Ad esempio:

 `~/.gtkrc-2.0` 

```
gtk-icon-theme-name = "Tango"
gtk-theme-name = "Murrine-Gray"
gtk-font-name = "DejaVu Sans 8"
```

**Note:** L'esempio appena riportato richiede i pacchetti [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu), [tango-icon-theme](https://aur.archlinux.org/packages/tango-icon-theme/), [gtk-engine-murrine](https://www.archlinux.org/packages/?name=gtk-engine-murrine) da [repository ufficiali](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)"), e [murrine-themes-collection](https://aur.archlinux.org/packages/murrine-themes-collection/) da [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)").

### GTK+ 3.x

Se state usando Gnome 3, il tema può essere modificato usando [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool).

Se state usando [Xfce](/index.php/Xfce_(Italiano) "Xfce (Italiano)") 4.8, sia i temi GTK+ 3.x and GTK+ 2.x possono essere modificati tramite l'Appearance Tool. Andate in Impostazioni-->Aspetto. Se lo stile scelto ha sia il tema GTK+ 2.x e GTK+ 3.x verranno usati entrambi. Se lo stile selezionate avesse soltanto il tema GTK+ 2.x, questo verrà usato mentre per le applicazioni GTK+ 3.x verrà usato il tema di default. Stessa cosa nel caso di un tema solo GTK+ 3.0\. Per avere un interfaccia regolare conviene usare stili per le GTK+ 2.0 e GTK+ 3.0, potete controllare i pacchetti in [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)"). Un esempio di questi temi è [clearwaita-gtk-theme](https://aur.archlinux.org/packages/clearwaita-gtk-theme/).

Se usate DE basati sulle GTK+, come [Xfce](/index.php/Xfce_(Italiano) "Xfce (Italiano)"), [LXDE](/index.php/LXDE_(Italiano) "LXDE (Italiano)"), gnome-tweak-tool non funzionerà; controllate su [FS#23644](https://bugs.archlinux.org/task/23644). Dovrete quindi utilizzare [install](/index.php/Pacman "Pacman") [librsvg](https://www.archlinux.org/packages/?name=librsvg), e selezionare manualmente il vostro tema in `{XDG_CONFIG_HOME}/gtk-3.0/settings.ini` (generalmente `~/.config/gtk-3.0/settings.ini`. Un esempio `settings.ini`:

 `{XDG_CONFIG_HOME}/gtk-3.0/settings.ini` 

```
[Settings]
gtk-application-prefer-dark-theme = false
gtk-theme-name = Zukitwo
gtk-fallback-icon-theme = gnome
gtk-icon-theme-name = [icon theme name]
gtk-font-name = [font name] [font size]
```

Se questo ancora non funzionasse cancellate la vecchia cartella gtk-3.0 contenuta in {XDG_CONFIG_HOME} e copiate la cartella gtk-3.0 in /path-to-the-theme to {XDG_CONFIG_HOME}. esempio:

```
rm -r ~/.config/gtk-3.0/
cp -r /usr/share/themes/Zukitwo/gtk-3.0/ ~/.config/  

```

Dopo questo avete bisogno di settare il vostro tema nelle configurazione dell'aspetto. Non sono molti i temi che offrono un aspetto uniforme sia per le applicazioni in GTK+ 3.x che per GTK+ 2.x. Tra questi ci sono:

1.  Adwaita per GTK+ 3 e Advaicium per GTK+ 2
2.  Newlooks per GKT+ 3 e Clearlooks per GTK+ 2
3.  Zukitwo
4.  Elegant Brit
5.  Atolm
6.  Hope

Potete scoprire quali temi sono istallati sul vostro computer che hanno una versione sia per le GTK2 che per le GTK3 usando questo comando (non funziona se nel nome del file sono contenuti spazi) :

```
find $(find ~/.themes /usr/share/themes/ -wholename "*/gtk-3.0" | sed -e "s/^\(.*\)\/gtk-3.0$/\1/")\
-wholename "*/gtk-2.0" | sed -e "s/.*\/\(.*\)\/gtk-2.0/\1"/

```

**Note:** Ci sono probabilmente altri temi, alcuni di questi sono presenti nei repository AUR, qualcuno potrebbe creare problemi a causa della sovrapposizione dei colori (bianco su sfondi luminosi), in questo caso dovreste usare [panel background](http://i.imgur.com/QmeyN.png).

### GTK+ e QT

Se avete applicazioni sia in GTK+ che QT (KDE) allora dovreste sapere che i loro look non vanno molto daccordo. Potete seguire questa guida per uniformarli [Uniform Look for QT and GTK Applications](/index.php/Uniform_Look_for_QT_and_GTK_Applications "Uniform Look for QT and GTK Applications").

## Configuration file

**Note:** Controllate il [_GtkSettings_](http://library.gnome.org/devel/gtk/stable/GtkSettings.html#GtkSettings.properties) nel manuale di riferimento per le GTK+ per la lista completa sulle configurazioni.

Lo scopo di questa sezione è di raccogliere le configurazioni delle applicazioni in GTK, il file da modificare è `~/.gtkrc-2.0`.

### Attivare scorciatoie da tastiera

Potete modificare le scorciatoie da tastiera per le applicazioni GTK (nel linguaggio GTK vengono definiti _accelerators_)portando il vostro mouse su un elemento di menu e premendo la combinazione di tasti desiderata. L'opzione è disativata di default per abilitarla:

```
gtk-can-change-accels = 1

```

### Velocizzare l'apertura dei menu di GNOME

Questo controllo server per velocizzare l'apertura dei menu di GNOME. Cambiate il valore come preferite. I numeri sono in millisecondo quindi 250 sono un quarto di secondo

```
gtk-menu-popup-delay = 0

```

### Diminuire la grandezza dei Widget

Nel caso voleste modificare la configurazione classica dei widgets o delle icone (es. rimpicciolirle), Per avere le icone senza il testo nella toolbar usate:

```
gtk-toolbar-style = GTK_TOOLBAR_ICONS

```

Per usare icone più piccole create una linea del genere:

```
gtk-icon-sizes = "panel-menu=16,16:panel=16,16:gtk-menu=16,16:gtk-large-toolbar=16,16\
:gtk-small-toolbar=16,16:gtk-button=16,16"

```

Per rimuovere completamente le icone:

```
gtk-button-images = 0

```

Potete anche rimuovere le icone solamente dal menu:

```
gtk-menu-images = 0

```

Ci sono ancora altre modifiche al tema gtkrc come spiegato in [qui](http://martin.ankerl.com/2008/10/10/how-to-make-a-compact-gnome-theme/) oppure [tema](http://gnome-look.org/content/show.php/Simple+eGTK?content=119812) che fa tutto.

## Sviluppo

Quando scrivere un programma GTK+3 da zero usando C è necessario aggiungere i CFLAGS per gcc:

```
gcc -g -Wall `pkg-config --cflags --libs gtk+-3.0` -o base base.c

```

i parametri -g e -Wall non sono necessari da quando sono utili soltanto per i parametri di debug. Potete provare l'ufficiale [Hello World example](http://developer.gnome.org/gtk-tutorial/stable/c39.html#SEC-HELLOWORLD).

### Write a simple message dialog app

Potete scrivere la vostra finestra di dialogo in GTk+ 3 usando numerosi codici di programmazione tramite i GObject-Introspection o bindings, oppure usare semplicemente il bash.

Gli esempi seguenti creano un programma che mostra la scritta "Hello World" in una finestra di dialogo.

#### Bash

*   Dependency: [zenity](https://www.archlinux.org/packages/?name=zenity)

 `hello_world.sh` 

```
#!/bin/bash
zenity --info --title='Hello world!' --text='This is an example dialog.'
```

#### C

*   Dependency: [gtk3](https://www.archlinux.org/packages/?name=gtk3)
*   Build with: `gcc -o hello_world `pkg-config --cflags --libs gtk+-3.0` hello_world.c`

 `hello_world.c` 

```
#include <gtk/gtk.h>
void main (int argc, char *argv[]) {
	gtk_init (&argc, &argv);
        GtkWidget *hello = gtk_message_dialog_new (NULL, GTK_DIALOG_MODAL, GTK_MESSAGE_INFO, GTK_BUTTONS_OK, "Hello world!");
	gtk_message_dialog_format_secondary_text (GTK_MESSAGE_DIALOG (hello), "This is an example dialog.");
        gtk_dialog_run(GTK_DIALOG (hello));
}
```

#### C++

*   Dependency: [gtkmm3](https://www.archlinux.org/packages/?name=gtkmm3)
*   Build with: `g++ -o hello_world `pkg-config --cflags --libs gtkmm-3.0` hello_world.cc`

 `hello_world.cc` 

```
#include <gtkmm.h>
#include <gtkmm/messagedialog.h>
int main(int argc, char *argv[]) {
	Gtk::Main kit(argc, argv);
	Gtk::MessageDialog Hello("Hello world!", false, Gtk::MESSAGE_INFO, Gtk::BUTTONS_OK);
	Hello.set_secondary_text("This is an example dialog.");
	Hello.run();
}
```

#### Genie

*   Dependency: [gtk3](https://www.archlinux.org/packages/?name=gtk3)
*   Makedependency: [vala](https://www.archlinux.org/packages/?name=vala)
*   Build with: `valac --pkg gtk+-3.0 hello_world.gs`

 `hello_world.gs` 

```
uses 
	Gtk
init
	Gtk.init (ref args)
	var Hello=new MessageDialog (null, Gtk.DialogFlags.MODAL, Gtk.MessageType.INFO, Gtk.ButtonsType.OK, "Hello world!")
	Hello.format_secondary_text ("This is an example dialog.")
	Hello.run ()
```

#### JavaScript

*   Dependencies: [gtk3](https://www.archlinux.org/packages/?name=gtk3), [gjs](https://www.archlinux.org/packages/?name=gjs) (works also with [seed](https://www.archlinux.org/packages/?name=seed))

 `hello_world.js` 

```
#!/usr/bin/gjs
Gtk = imports.gi.Gtk
Gtk.init(null, null)
Hello = new Gtk.MessageDialog({type: Gtk.MessageType.INFO,
                               buttons: Gtk.ButtonsType.OK,
                               text: "Hello world!",
                               "secondary-text": "This is an example dialog."})
Hello.run()
```

#### Python

*   Dependencies: [gtk3](https://www.archlinux.org/packages/?name=gtk3), [python-gobject](https://www.archlinux.org/packages/?name=python-gobject)

 `hello_world.py` 

```
#!/usr/bin/python
from gi.repository import Gtk
Gtk.init(None)
Hello=Gtk.MessageDialog(None, Gtk.DialogFlags.MODAL, Gtk.MessageType.INFO, Gtk.ButtonsType.CLOSE, "Hello world!")
Hello.format_secondary_text("This is an example dialog.")
Hello.run()
```

#### Vala

*   Dependency: [gtk3](https://www.archlinux.org/packages/?name=gtk3)
*   Makedependency: [vala](https://www.archlinux.org/packages/?name=vala)
*   Build with: `valac --pkg gtk+-3.0 hello_world.vala`

 `hello_world.vala` 

```
using Gtk;
public class HelloWorld {
	static void main (string[] args) {
		Gtk.init (ref args);
		var Hello=new MessageDialog (null, Gtk.DialogFlags.MODAL, Gtk.MessageType.INFO, Gtk.ButtonsType.OK, "Hello world!");
		Hello.format_secondary_text ("This is an example dialog.");
		Hello.run ();
	}
}
```

## Resources

*   [The official GTK+ website](http://www.gtk.org/)
*   [Wikipedia article about GTK+](https://en.wikipedia.org/wiki/GTK%2B "wikipedia:GTK+")
*   [GTK+ 2.0 Tutorial](http://developer.gnome.org/gtk-tutorial/stable/)
*   [GTK+ 3 Reference Manual](http://developer.gnome.org/gtk3/stable/)
*   [gtkmm Tutorial](http://developer.gnome.org/gtkmm-tutorial/stable/)
*   [gtkmm Reference Manual](http://developer.gnome.org/gtkmm/stable/)