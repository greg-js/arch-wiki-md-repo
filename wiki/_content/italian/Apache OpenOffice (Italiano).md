**Attenzione:** In traduzione e sistemazione: pagina non aggiornata. Fare riferimento al wiki inglese per adesso

[OpenOffice](http://www.openoffice.org/) è il principale pacchetto open-source di software per l'ufficio, fornendo applicazioni per la videoscrittura, fogli di calcolo, presentazioni, grafica, gestione di database e altro ancora.

## Contents

*   [1 OpenOffice in Arch Linux](#OpenOffice_in_Arch_Linux)
*   [2 Installazione](#Installazione)
    *   [2.1 Pacchetti del linguaggio e del controllo ortografico per versioni stabili](#Pacchetti_del_linguaggio_e_del_controllo_ortografico_per_versioni_stabili)
    *   [2.2 Extension management and spell checking for OpenOffice 3.x](#Extension_management_and_spell_checking_for_OpenOffice_3.x)
        *   [2.2.1 Other extensions installed by default](#Other_extensions_installed_by_default)
    *   [2.3 Set OOo environment variable](#Set_OOo_environment_variable)
        *   [2.3.1 Configure OOo environment globally](#Configure_OOo_environment_globally)
        *   [2.3.2 Environment variable scripts](#Environment_variable_scripts)
    *   [2.4 KDE4 look and feel for OpenOffice](#KDE4_look_and_feel_for_OpenOffice)
        *   [2.4.1 Alternative configuration](#Alternative_configuration)
*   [3 Running OpenOffice](#Running_OpenOffice)
*   [4 Speed up OpenOffice](#Speed_up_OpenOffice)
*   [5 Trouble-shooting](#Trouble-shooting)
    *   [5.1 Font substitution](#Font_substitution)
    *   [5.2 Anti-aliasing](#Anti-aliasing)
    *   [5.3 TrueType font detection](#TrueType_font_detection)
    *   [5.4 Qt looks with KDE >4](#Qt_looks_with_KDE_.3E4)
    *   [5.5 French dictionary](#French_dictionary)
    *   [5.6 Dark GTK themes and gtk-qt-engine](#Dark_GTK_themes_and_gtk-qt-engine)
    *   [5.7 Hanging when using NFS shares](#Hanging_when_using_NFS_shares)
    *   [5.8 Gestione delle estensioni e correttore ortografico per OpenOffice 3.x](#Gestione_delle_estensioni_e_correttore_ortografico_per_OpenOffice_3.x)
    *   [5.9 Configurare le variabili d'ambiente per OpenOffice.org](#Configurare_le_variabili_d.27ambiente_per_OpenOffice.org)
    *   [5.10 KDE4 look & feel per OpenOffice](#KDE4_look_.26_feel_per_OpenOffice)
    *   [5.11 Aggiungere supporto multimediale a OpenOffice.org 2](#Aggiungere_supporto_multimediale_a_OpenOffice.org_2)
    *   [5.12 Installazione Manuale dei dizionari](#Installazione_Manuale_dei_dizionari)
*   [6 Eseguire un programma della Suite](#Eseguire_un_programma_della_Suite)
*   [7 Problemi Noti](#Problemi_Noti)

## OpenOffice in Arch Linux

Arch Linux offre 4 rami di pacchetti binari per OpenOffice, con pacchetti denominati in maniera differente:

**openoffice-base**

Questo pacchetto conterrà sempre l'ultima versione stabile di OpenOffice.
Versione corrente: 3.1.0
È possibile eseguire il programma con il comando "soffice" o dal menu del vostro DE
I pacchetti per la localizzazione e il controllo ortografico dipenderanno da questo pacchetto.

**openoffice-base-beta**

Questo pacchetto sarà presente solo quando è imminente il rilascio di una nuova versione di OpenOffice. Sarà man mano aggiornato ad ogni rilascio alpha, beta e RC fino al rilascio della versione stabile.
Versione corrente: 3.2.1_ooo320_m12-1 (verso la =3.1.1rc1) (versione staccata dalla DEV300_m40 che porterà alla prossima versione stabile 3.2.x)
È possibile eseguire il programma con il comando "soffice-beta" o dal menu del vostro DE
Si può tranquillamente installare anche in contemporanea con la versione stabile e quella devel.
Testatela con prudenze e segnalate eventuali bug relativi sia al software stesso, sia al "packaging" del software stesso
vedere [http://wiki.services.openoffice.org/wiki/OOoRelease30](http://wiki.services.openoffice.org/wiki/OOoRelease30) per la roadmap di sviluppo

**openoffice-base-devel**

Questo pacchetto sarà aggiornato di tanto in tanto e costituisce un *banco di prova* per il mantainer del pacchetto e per testare le ultime caratteristiche. Per favore, testate pure il pacchetto e segnalate bugs o problemi presso [http://www.openoffice.org/issues/query.cgi](http://www.openoffice.org/issues/query.cgi)
Versione corrente: 3.3_dev300_m70-1 / snapshot DEV300_m70 (*snapshots* successivi al ramo che porta alla versione 3.2 stabile e che porterà alla release 3.3 e oltre
È possibile eseguire il programma con il comando "soffice-devel" o dal menu del vostro DE
Si può tranquillamente installare anche in contemporanea con la versione stabile e quella beta.
Fare riferimento alla pagina [http://wiki.services.openoffice.org/wiki/OOoRelease33](http://wiki.services.openoffice.org/wiki/OOoRelease33) per un dettaglio dei rilasci previsti.

**go-openoffice**

Infine, c'è la possibilità di installare go-openoffice, altresì detto ooo-build - la versione Novell di OpenOffice, che include elementi presenti nelle versioni di Oo fornite con OpenSuse, Ubuntu e altre distribuzioni. Per utenti di Arch provenienti da altre distribuzioni, usare go-openoffice può risultare più familiare. Questo pacchetto sarà sempre aggiornato alla pari con la versione di Oo presente in extra. Eventuali future versioni beta\devel saranno messe nel repository testing.

Ora come ora, go-openoffice non può essere installato in contemporanea ad altre versioni di openoffice. Va considerato come un rimpiazzo delle versioni ufficiali.

**Note:** In caso utilizziate diverse versioni di OpenOffice in contemporanea, è altamente consigliato farsi un backup periodico delle cartelle di configurazione ~/.openoffice{2,3}!

## Installazione

*   Innanzitutto, installate il Java Runtime Environment (opzionale, ma altamente raccomandato). Riferirsi a: [Java](/index.php/Java "Java")
*   Assicuratevi inoltre di aver installato dei font di base, altrimenti potreste visualizzare solo rettangoli al posto dei caratteri:

```
# pacman -S ttf-dejavu artwiz-fonts ttf-ms-fonts (e altri font eventualmente richiesti dalla vostra lingua.)

```

*   Poi procedete all'installazione di openoffice in una (o più) delle sue versioni:

```
# pacman -S openoffice-base openoffice-base-beta openoffice-base-devel

```

### Pacchetti del linguaggio e del controllo ortografico per versioni stabili

*   Installate uno o più pacchetti linguaggio. L'inglese (en_US) è incluso di default nel pacchetto -base:

```
# pacman -S openoffice-XX (dove XX è un linguaggio)

```

per l'italiano:

```
# pacman -S openoffice-it

```

**Note:** Per go-openoffice, è disponibile il pacchetto [go-openoffice-it](https://aur.archlinux.org/packages/go-openoffice-it/) su [AUR](/index.php/AUR "AUR")

### Extension management and spell checking for OpenOffice 3.x

The Arch package is now shipped with some dictionaries. Check Extension manager if your language is already there simply by loading up any OO program (Writer for example) and access the Extension Manager from the Tools menu. From there enter the following location to install a spell check dictionary:

```
/usr/lib/openoffice/share/extension/install/

```

**Note:** If you installed go-openoffice, the path will be /usr/lib/go-openoffice/share/extension/install/ instead.

Alternatively, there are several ways to accomplish this:

*   1) Use the Extension manager from OOo menu for download and installation - installs only for the user into his ~/.openoffice.org/3/user/uno_packages/cache
*   2) Download the extension and install it using "/usr/lib/openoffice/program/unopkg add extension" for the user or
*   3) Download the extension and install it using "/usr/lib/openoffice/program/unopkg add --shared extension" for every user on the system (requires root permission)

##### Other extensions installed by default

(This list is valid for go-openoffice)

*   pdfimport.oxt: ability to import PDF files in Draw and Impress
*   presenter-screen.oxt: when using two displays this plugin provides more control over slideshow
*   sun-presentation-minimizer.oxt: reduce file size of current presentation
*   wiki-publisher.oxt: allows to create Wiki articles on MediaWiki servers without having to know the synthax of the MediaWiki markup language

### Set OOo environment variable

OpenOffice supports to use several toolkits for drawing and integrates into different desktop environments in a clean way. To choose by hand, you need to set the OOO_FORCE_DESKTOP environment variable.

To run OpenOffice.org in GTK2 mode(this is default and already preset), you can issue (using bash):

```
 # OOO_FORCE_DESKTOP=gnome soffice

```

To run OpenOffice.org in QT/KDE3 mode, you can issue (using bash):

```
 # OOO_FORCE_DESKTOP=kde soffice

```

To run OpenOffice.org in QT4/KDE4 mode, you can issue (using bash):

```
 # OOO_FORCE_DESKTOP=kde4 soffice

```

**Note:** As KDE look was removed in Openoffice3 it is highly recommended to use the GTK mode for all users. KDE4 integration is in experimental state in go-openoffice and in openoffice-base-devel (starting from m56)

#### Configure OOo environment globally

To configure the look for anytime OpenOffice gets started, you can export the **<tt>OOO_FORCE_DESKTOP</tt>** variable in /etc/profile.d/openoffice.sh, or in /usr/bin/soffice, with the value **<tt>gnome</tt>**, **<tt>kde</tt>**, or **<tt>kde4</tt>**.

#### Environment variable scripts

If for whatever reason you do not want to configure the look globaly, as a non-GNOME/KDE user you may run into problems when trying to add the environment variable to the command in a *box menu, as such menus do not seem to like environment variables.

This script will run openoffice using the GTK look while still accepting command line options like -writer.

```
#!/bin/sh

#### openoffice-gtk - A script to start openoffice with the GNOME/GTK environment

OOO_FORCE_DESKTOP=gnome /usr/bin/soffice "$@"

```

Just use this script as a command (e.g, /usr/bin/openoffice-gtk) for your menu or whatever other sort of launcher you use.

**Note:** If you open a file in a filemanager, for example Thunar, the default look will be used, as the file association will not use your personal script.

### KDE4 look and feel for OpenOffice

OOO_FORCE_DESKTOP=gnome never did the trick for me. A good workaround is to set (as root):

```
export SAL_GTK_USE_PIXMAPPAINT=1

```

into /etc/profile.d/openoffice.sh. In KDE4 systemsettings, make sure "use my KDE style in GTK applications" is selected in Appearance > GTK styles and fonts (you must install gtk-qt-engine first).

#### Alternative configuration

You may wish to set the Xorg server dots-per-inch in the [KDM](/index.php/KDM "KDM") configuration.

Do not select "use my KDE style in GTK applications". Instead choose a native syle and font for GTK2 applications.

```
# pacman -S gtk-chtheme
# pacman -S gtk-engines

```

Use gtk-chtheme to select a style (in general different from KDE) and a font (may be the same as your KDE general system font). There are also other GTK engine packages available.

There are two relevant parts of the OOo options dialog, View and Fonts:

*   View
    *   set scale to 100%
    *   set use system font OFF (otherwise replacement table will not be used)
    *   set antialiasing OFF

*   Fonts
    *   select "Use replacement table"
    *   replace "Andale Sans UI" (you *must* type this in -- it is not in the drop down list) with another font (your KDE system font or another if this looks bad)
    *   Press the tick symbol to update the list
    *   Select "always" and "screen only"
    *   Press OK

When choosing fonts for OpenOffice note that the poor font rendering engine included in the package may not render a particular font in the same way as other apps on the desktop. Use the `kmag` magnifying glass to examine shape of each letter.

## Running OpenOffice

If you want to run a specific module of OpenOffice.org (instead of the soffice default Startcenter), for example the word processor (Write), spreadsheet application (Calc) or presentation program (Impress), check for the following script front-ends:

Writer

```
 /usr/bin/soffice -writer

```

Calc

```
 /usr/bin/soffice -calc

```

Impress

```
 /usr/bin/soffice -impress

```

Draw

```
 /usr/bin/soffice -draw

```

Math (Formula Editor)

```
 /usr/bin/soffice -math

```

Base (Database frontend)

```
 /usr/bin/soffice -base

```

Printer Administration (Recommended to run as root)

```
 /usr/bin/spadmin

```

## Speed up OpenOffice

Some settings may improve OpenOffice's loading time and responsiveness. However, some also increase RAM usage, so use them carefully. They can all be accessed under *Tools > Options*.

*   Under *Memory*:
    *   Reduce the number of Undo steps to a figure lower than 100, to something like 20 or 30 steps.
    *   Under Graphics cache, set Use for OpenOffice.org to 128 MB (up from the original 20MB).
    *   Set Memory per object to 20MB (up from the default 5MB).
    *   If you use OpenOffice often, check OpenOffice.org Quickstarter.
*   Under *Java*, uncheck Use a Java runtime environment.

## Trouble-shooting

### Font substitution

These settings can be changed in the OpenOffice.org options. From the drop-down menu, select *Tools > Options > OpenOffice.org > Fonts*. Check the box that says *Apply Replacement Table*. Type `Andale Sans UI` in the font box and choose your desired font for the *Replace with* option. When done, click the *checkmark*. Then choose the *Always* and *Screen only* options in the box below. Click OK. You will then need to go to *Tools > Options > OpenOffice.org > View*, and uncheck "Use system font for user interface". If you use a non-antialised font, such as Arial, you will also need to uncheck "Screen font antialiasing" before menu fonts render correctly.

### Anti-aliasing

Execute

```
$ echo "Xft.lcdfilter: lcddefault" | xrdb -merge

```

To make the change persistent, add "`Xft.lcdfilter: lcddefault`" to your `~/.Xresources` file. [[1]](https://bugs.launchpad.net/ubuntu/+source/openoffice.org/+bug/271283/comments/19).

If this doesn't work you can also try adding "`Xft.lcdfilter: lcddefault`" to your `~/.Xdefaults`. If you do not have this file, you will have to create it.

### TrueType font detection

See [Font configuration#Programs can no longer access TrueType fonts](/index.php/Font_configuration#Programs_can_no_longer_access_TrueType_fonts "Font configuration"). To add fonts to those already available in OpenOffice, run `spadmin`.

### Qt looks with KDE >4

OpenOffice has transitioned to Qt 4, and as such the look of the applications can not be set with Qt 3 tools.

### French dictionary

As of openoffice 3.0.0-2 the french dictionary is buggy due to a character encoding problem. To solve this problem, first execute the following commands (you will need **zip** and **unzip** packages):

```
$ cp /usr/lib/openoffice/share/extension/install/dict-fr.oxt dict-fr.oxt
$ unzip dict-fr.oxt -d dict-fr
$ cd dict-fr
$ iconv -f ISO-8859-15 -t UTF-8 dictionaries.xcu > dictionaries.xcu.utf
$ mv dictionaries.xcu.utf dictionaries.xcu
$ zip ../dict-fr.oxt *
$ cd ../
$ rm -r dict-fr

```

then go in the openoffice extension manager (Tools menu) and install the dictionary from the new dict-fr.oxt file.

### Dark GTK themes and gtk-qt-engine

For a quick fix, see [openoffice-dark-gtk-fix](https://aur.archlinux.org/packages/openoffice-dark-gtk-fix/) or if you have go-openoffice see [go-openoffice-dark-gtk-fix](https://aur.archlinux.org/packages.php?ID=28879) on the AUR. This also sets 'OOO_FORCE_DESKTOP=gnome'. Another fix is to export SAL_USE_VCLPLUGIN=gen (generic X11). See [for more info](http://user.services.openoffice.org/en/forum/viewtopic.php?f=16&t=27216#p123942)

### Hanging when using NFS shares

If OpenOffice hangs when trying to open/save a document located on a NFS share, try prepending the following lines with a "#" in /usr/lib/openoffice/program/soffice:

```
# file locking now enabled by default
SAL_ENABLE_FILE_LOCKING=1
export SAL_ENABLE_FILE_LOCKING

```

Original post [here](http://www.crazysquirrel.com/computing/debian/bugs/openoffice-over-nfs.jspx)

### Gestione delle estensioni e correttore ortografico per OpenOffice 3.x

*   Vedere [il sito OpenOffice Extension](http://extensions.services.openoffice.org/getmore?cid=920794)
*   I vecchi pacchetti openoffice-spell sono obsoleti.
*   La correzione ortografica è effettuata ora tramite le nuove [estensioni](http://extensions.services.openoffice.org/dictionary). Ci sono 3 modi diversi per installare queste estensioni:
*   1) Usare il Manager delle Estensioni dal menu di Oo per scaricarle e installarle - in questo modo, l'estensione viene installata solo per l'utente corrente in ~/.openoffice.org/3/user/uno_packages/cache
*   2) Scaricare l'estensione e installarla usando il comando "unopkg add extension" per l'utente corrente oppure...
*   3) Scaricare l'estensione e installarla usando il comando "unopkg add --shared extension" per tutti gli utenti del sistema (questo comando richiede i privilegi di root)
*   4) I pacchetti di Arch sono provvisti di alcuni dizionari e questi ultimi vengono caricati automaticamente. Controllate il Gestore delle Estensioni per vedere se il vostro linguaggio è già presente.

### Configurare le variabili d'ambiente per OpenOffice.org

OpenOffice2 ha introdotto la funzionalità di utilizzare una pluralità di toolkit differenti per disegnare l'interfaccia e integrarsi nei differenti ambienti desktop in maniera pulita. Per scegliere a mano quale toolkit utilizzare, avrete bisogno di impostare la variabile d'ambiente OOO_FORCE_DESKTOP, o per tutto il sistema (inserendo i seguenti comandi in uno fra /etc/profile, rc.local, o ~/.bashrc o qualcosa come /etc/profile.d/openoffice) o nella specifica shell nella quale OpenOffice.org sta operando (vedere i messaggi restituiti da pacman che appaiono quando viene installato\aggiornato il pacchetto openoffice-base).

Per eseguire OpenOffice.org nella modalità GTK2, potete usare (usando una shell bash):

```
 # OOO_FORCE_DESKTOP=gnome soffice

```

Per eseguire OpenOffice.org nella modalità QT/KDE3, potete usare (usando una shell bash):

```
 # OOO_FORCE_DESKTOP=kde soffice

```

Il look KDE sarà rimosso da Openoffice nella versione 3\. È altamente raccomandato che facciate l'export di OOO_FORCE_DESKTOP=gnome per tutti gli utenti (si, anche sotto KDE4) dalle versioni di OpenOffice >=3.x o potreste subire presto dei crash relativi alle librerie glib\gtk.

### KDE4 look & feel per OpenOffice

OOO_FORCE_DESKTOP=gnome non ha mai funzionato in questo caso. Un buon miglioramento lo si ottiene impostando (da root):

```
export SAL_GTK_USE_PIXMAPPAINT=1

```

nell'/etc/profile. Nelle impostazioni di sistema di KDE4, assicuratevi di selezionare "usa lo stile KDE nelle applicazioni GTK" nella scheda riguardante le impostazioni sull'aspetto > Stili GTK e caratteri (dovete installare il pacchetto gtk-qt-engine per avere questa scheda).

### Aggiungere supporto multimediale a OpenOffice.org 2

Se volete usare suoni e video nelle presentazioni create con OpenOffice.org Impress, avete bisogno di installare il [Java Media Framework](/index.php/Java_Media_Framework "Java Media Framework") e di [configurare OpenOffice.org per usarla](/index.php/Java_Media_Framework#Adding_media_support_to_OpenOffice.org "Java Media Framework")

### Installazione Manuale dei dizionari

Se per qualche ragione volete procedere ad installare manualmente dei dizionari (ad esempio perchè non trovate pacchetti di dizionari nel vostro linguaggio), seguite queste istruzioni:

*   Scaricate un dizionario per il vostro linguaggio. Una lista dei dizionari disponibili è presente alla pagina [Dizionari per OpenOffice](http://wiki.services.openoffice.org/wiki/Dictionaries)
*   Estraete i dizionari nella cartella /opt/openoffice/share/dict/ooo/

I file necessari sono di norma denominati come *en_US.dic* ed *en_US.aff* per il controllo ortografico, hyph_en_US.dic per i dizionari di sillabazione, e infine *th_en_US.dat* e *th_en_US.idx* per i file del thesaurus.

*   Aprite /opt/openoffice/share/dict/ooo/dictionary.lst con il vostro editor di testi preferito, e aggiungete i dizionari alla lista seguendo le seguenti regole:

```
 # List of All Dictionaries to be Loaded by OpenOffice
 # ---------------------------------------------------
 # Each Entry in the list have the following space delimited fields
 #
 # Field 1: Entry Type "DICT" - spellchecking dictionary
 # "HYPH" - hyphenation dictionary
 # "THES" - thesaurus files
 #
 # Field 2: Language code from Locale "en" or "de" or "pt" ... 
 #
 # Field 3: Country Code from Locale "US" or "GB" or "PT"
 #
 # Field 4: Root name of file(s) "en_US" or "hyph_de" or "th_en_US
 # (do not add extensions to the name)

```

*   Un esempio usando i dizionari Americani sarebbe come:

```
 ### start en
 DICT en US en_US
 HYPH en US hyph_en_US
 THES en US th_en_US
 ### end en

```

*   Salvate il file e riavviate OpenOffice. Assicuratevi che tutti i processi OpenOffice siano stati fermati, altrimenti i dizionari appena installati potrebbero non essere visualizzati.

## Eseguire un programma della Suite

Se volete eseguire un modulo specifico di OpenOffice.org (invece del programma di default soffice), ad esempio il solo editor di testo Write, il foglio di calcolo (Calc) o l'editor di presentazioni (Impress), ecco i comandi da eseguire:

Writer

```
 /opt/openoffice/program/swriter

```

Calc

```
 /opt/openoffice/program/scalc

```

Impress

```
 /opt/openoffice/program/simpress

```

Math (Editor di formule matematiche)

```
 /opt/openoffice/program/smath

```

Base (Interfaccia per Database)

```
 /opt/openoffice/program/sbase

```

Amministratore di Stampa (si raccomanda di eseguirlo da root)

```
 /opt/openoffice/program/spadmin

```

## Problemi Noti

*   gestione estensioni in versioni >=3.0
*   il *qt look'n feel* dall'uscita di KDE4