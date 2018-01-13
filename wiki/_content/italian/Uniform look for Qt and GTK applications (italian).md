Articoli correlati

*   [GTK+_(Italiano)](/index.php/GTK%2B_(Italiano) "GTK+ (Italiano)")

Questo articolo descrive la configurazione dettagliata delle Qt e GTK+ per assicurare uno stile delle applicazioni uniforme. Questo articolo copre configurazione, motore dei temi, trucchi e troubleshooting.

## Contents

*   [1 Introduzione](#Introduzione)
*   [2 Stile per Qt e GTK+](#Stile_per_Qt_e_GTK.2B)
    *   [2.1 KDE4 Oxygen](#KDE4_Oxygen)
    *   [2.2 QtCurve](#QtCurve)
    *   [2.3 Altri](#Altri)
*   [3 Come posso configurare lo stile per ogni toolkit?](#Come_posso_configurare_lo_stile_per_ogni_toolkit.3F)
    *   [3.1 Stili QT3](#Stili_QT3)
    *   [3.2 Stili QT4](#Stili_QT4)
    *   [3.3 Stili GTK2](#Stili_GTK2)
    *   [3.4 Stili GTK1](#Stili_GTK1)
*   [4 Motore dei temi](#Motore_dei_temi)
    *   [4.1 GTK-QT-Engine](#GTK-QT-Engine)
        *   [4.1.1 Funzionamento con OpenOffice](#Funzionamento_con_OpenOffice)
    *   [4.2 QGtkStyle](#QGtkStyle)
        *   [4.2.1 Possibili problemi con le applicazioni Qt che utilizzano QGtkStyle](#Possibili_problemi_con_le_applicazioni_Qt_che_utilizzano_QGtkStyle)
*   [5 Altri trucchi](#Altri_trucchi)
    *   [5.1 Menu di KDE per le applicazioni GTK2](#Menu_di_KDE_per_le_applicazioni_GTK2)
    *   [5.2 Usare uno stile GTK personalizzato](#Usare_uno_stile_GTK_personalizzato)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 I temi non funzionano nelle applicazioni GTK](#I_temi_non_funzionano_nelle_applicazioni_GTK)

# Introduzione

I programmi basati su [Qt](https://it.wikipedia.org/wiki/Qt_(toolkit))- e [GTK+](/index.php/GTK%2B_(Italiano) "GTK+ (Italiano)") utilizzano diversi widget toolkit per renderizzare l'interfaccia grafica utente. Ognuno di default è fornito di diversi temi, stili e set di icone così il "look & feel" è significativamente differente. Questo articolo vi aiuterà nel rendere le applicazioni Qt e GTK+ simili tra loro in modo da ottenere un'esperienza desktop più "integrata" e razionale.

*"Qt (pronuncia "cute") è un framework di sviluppo applicazioni cross-platform largamente usato per sviluppare sia applicazioni basate su GUI (in questo caso esso è noto come widget toolkit) che applicazioni "non-GUI" come strumenti per console e server."*

*   **Tema** - Raccolta di uno stile, un tema di icone e un tema di colori.
*   **Stile** - Layout grafico; look.
*   **Tema delle icone** - Set di icone.
*   **Tema dei colori** - Set di colori usato in associazione allo stile.

# Stile per Qt e GTK+

Esistono dei set di stili creati con lo scopo dell'integrazione in quanto scritti e distribuiti per le principali versioni di Qt e GTK+. Con essi è possibile avere un look uniforme per tutte le applicazioni indipendentemente dal toolkit con cui sono state scritte.

## KDE4 Oxygen

[Oxygen](http://www.oxygen-icons.org/) è lo stile Qt4 preinstallato con KDE4. Esiste anche una versione GTK+ chiamata [oxygen-molecule](http://kde-look.org/content/show.php?content=103741) disponibile attraverso [AUR](/index.php/AUR "AUR") as [oxygen-molecule-theme](https://aur.archlinux.org/packages/oxygen-molecule-theme/). Il suo obiettivo è quello di fornire un look uniforme alle applicazioni GTK+ quando usate in KDE attraverso gtk-engine-pixbuf, una dipendenza anch'essa disponibile in [AUR](/index.php/AUR "AUR") as [gtk-engine-pixbuf](https://aur.archlinux.org/packages/gtk-engine-pixbuf/). Il pacchetto AUR fornisce semplici ma sufficienti informazioni per completare l'installazione. Per informazioni più dettagliate scaricare [oxygen-molecule](http://kde-look.org/content/show.php?content=103741) da KDE-look.

Un altro port GTK+ è il pacchetto [oxygen-gtk2](https://www.archlinux.org/packages/?name=oxygen-gtk2). Il suo obiettivo principale è assicurare una grafica uniforme tra applicazioni Qt e GTK+ nell'ambiente KDE. Un obiettivo secondario è fornire un tema gtk attraente e che si comporti bene sui vari Desktop Environment. Sfortunatamente come per tutti gli altri tentativi di portare il tema oxygen in gtk esso non dipende dalle Qt (attraverso un qualche motore di conversione tra Qt e Gtk), e non renderizza l'aspetto dei widget tramite pixmaps pre-impostati. Inoltre crea problemi ogni volta che vene cambiata qualche impostazione in kde.

## QtCurve

QtCurve è uno stile altamente configurabile e molto popolare. Dispone di molti controlli e opzioni che permettono di configurare diverse cose a partire dall'aspetto dei pulsanti fino alla forma delle barre di scorrimento. Disponibile per *qt4* (kde4), *qt3* (kde3), e *gtk2* (gnome) nel repository **[extra]**, si può installare con pacman:

```
# pacman -S qtcurve-gtk2 qtcurve-kde3 qtcurve-kde4

```

## Altri

I set di stile simili sono quelli che, scritti sia per Qt che per GTK (ma non necessariamente dallo stesso sviluppatore), si somigliano tra loro. Potrebbe essere necessario effettuare qualche modifica minore per ottenere lo stesso look. Di seguito ne sono elencati alcuni:

*   klearlooks (qt3); clearlooks (gtk2)

# Come posso configurare lo stile per ogni toolkit?

E' possibile usare i seguenti metodi per cambiare il tema in ogni ambiente.

## Stili QT3

*   Usando il *Centro di controllo di KDE3* (kcontrol):

	--> Aspetto & Temi --> Stile --> Stile del Widget

*   kde-config --style [nome dello stile]
*   *Qt Configuration* (qt3config | /opt/qt/bin/qtconfig)

	--> Aspetto --> Seleziona stile della GUI

## Stili QT4

*   Usando *Impostazioni di sistema di KDE4* (/usr/bin/systemsettings)

	--> Aspetto e comportamento comune --> Aspetto delle applicazioni --> Stile --> Stile del Widget

*   *Qt Configuration* (/usr/bin/qtconfig)

	--> Aspetto --> Seleziona stile della GUI

## Stili GTK2

*   [gtk-kde4](https://aur.archlinux.org/packages/gtk-kde4/) (permette di cambiare stile e font delle applicazioni GTK in KDE4)
*   [lxappearance](https://www.archlinux.org/packages/?name=lxappearance) (un tool di configurazione indipendente dal DE e messo a disposizione dal LXDE project. Esso non richiede nessun altro componente di LXDE)
*   [gtk-chtheme](https://www.archlinux.org/packages/?name=gtk-chtheme) (considerarlo come una migliore alternativa a switch2)
*   [gtk2_prefs](https://aur.archlinux.org/packages/gtk2_prefs/)
*   [gtk-theme-switch2](https://www.archlinux.org/packages/?name=gtk-theme-switch2)
*   [Configurazione manuale](/index.php/GTK%2B#GTK.2B_2.x "GTK+")

## Stili GTK1

*   [gtk-theme-switch](https://aur.archlinux.org/packages/gtk-theme-switch/) pacchetto from the [AUR](/index.php/AUR "AUR")

# Motore dei temi

Un motore temi può essere pensato come ad un sottile strato di API usato per tradurre i temi (escluse le icone) tra diversi toolkit. Questi motori aggiungono del codice in più nel processo ed è una scelta discutibile in quanto è una soluzione poco elegante ed efficiente rispetto ad uno stile nativo.

## GTK-QT-Engine

Questo motore può essere usato dalle applicazioni GTK+ nell'ambiente KDE, questo fondamentalmente significa che è per KDE. Esso applica tutte le impostazioni Qt (stili, fonts ma non icone) alle applicazioni GTK+ e usa direttamente i plugin dello stile. Notare che esistono problemi di rendering con alcuni stili Qt.

```
# pacman -S gtk-qt-engine

```

E' possibile accedere ad esso da:

	*Centro di controllo (kcontrol) --> Aspetto & Temi --> Font e Stili GTK*

Se lo si vuole rimuovere completamente si dovrebbero rimuovere i seguenti file:

*   ~/.gtkrc2.0-kde
*   ~/.kde4/env/gtk-qt-engine.rc.sh
*   ~/gtk-qt-engine.rc

### Funzionamento con OpenOffice

Digitare (come root):

```
export SAL_GTK_USE_PIXMAPPAINT=1

```

nel file /etc/profile. Nelle Impostazioni di sistema di KDE4 assicurarsi che in Aspetto > Stile GTK e fonts sia selezionato "utilizza lo stile KDE nelle applicazioni GTK".

## QGtkStyle

Questo è uno stile Qt che intende rendere le applicazioni perfettamente armonizzate nel desktop GNOME tramite l'uso delle GTK per renderizzare tutti i componenti. Per usare questo stile si dovrebbe avere almeno GTK+ 2.0 e Qt 4.3 anche se le Qt 4.4 sono consigliate.

**Note:** A partire dalla versione 4.5 questo stile è incluso nelle Qt per cui non è necessario installare questo pacchetto. Per quelli interessati è disponibile comunque un pacchetto in AUR: [qgtkstyle-svn](https://aur.archlinux.org/packages/qgtkstyle-svn/).

### Possibili problemi con le applicazioni Qt che utilizzano QGtkStyle

Le Qt non applicano correttamente lo stile QGtkStyle se le GTK usano [GTK-QT-Engine](/index.php/Uniform_look_for_Qt_and_GTK_applications#GTK-QT-Engine "Uniform look for Qt and GTK applications"). Qt determina se [GTK-QT-Engine](/index.php/Uniform_look_for_Qt_and_GTK_applications#GTK-QT-Engine "Uniform look for Qt and GTK applications") è in uso leggendo il file di configurazione delle GTK contenuto nella variabile di sistema **GTK2_RC_FILES**. Se questa variabile non è impostata correttamente Qt suppone che si stia usando [GTK-QT-Engine](/index.php/Uniform_look_for_Qt_and_GTK_applications#GTK-QT-Engine "Uniform look for Qt and GTK applications"), inoltre configura QGtkStyle in modo che utilizzi lo stile GTK *Clearlooks* e visualizza il seguente messaggio di errore:

```
QGtkStyle cannot be used together with the GTK_Qt engine.

```

Un altro errore che si potrebbe incontrare dopo aver lanciato qtconfig dalla shell e selezionato lo stile Gtk+ è:

```
QGtkStyle was unable to detect the current GTK+ theme.

```

Gli utenti di [Openbox](/index.php/Openbox "Openbox") e degli altri sistemi non-GNOME potrebbero incontrare facilmente questo problema. Una soluzione può essere:

*   Dire a Qt dove cercare il file di configurazione GTK aggiungendo le seguenti linee nel file `.xinitrc`:
    *   Per aggiungere più percorsi separarli con un due punti.
    *   La variabile $HOME deve contenere il percorso della home del proprio utente. L'utilizzo del simbolo ~ non funziona.

 `.xinitrc` 
```
...
export GTK2_RC_FILES="$HOME/.gtkrc-2.0"
...
```

*   Nel file `.gtkrc-2.0` va specificato un tema GTK. Ad esempio:
    *   Normalmente questo viene fatto tramite un'[applicazione per impostare i temi GTK2](/index.php/Uniform_look_for_Qt_and_GTK_applications#GTK2_styles "Uniform look for Qt and GTK applications")
    *   Se il file `~/.gtkrc-2.0` non esiste basta semplicemente crearlo ed aggiungere le seguenti linee:

 `.gtkrc-2.0` 
```
...
gtk-theme-name="Crux"
...
```

Comunque sembra che a volte questi tool inseriscono solamente una direttiva del tipo:

 `.gtkrc-2.0` 
```
...
include "/usr/share/themes/SomeTheme/gtk-2.0/gtkrc"
...
```
che apparentemente non viene riconosciuta da tutte le versioni di QGtkStyle. Una soluzione è inserire manualmente il nome del tema gtk nel file .gtkrc-2.0 come sopra. Notare che comunque durante l'utilizzo delle applicazioni per la modifica degli stili GTK2 queste modifiche potrebbero essere perse.

Per scegliere il proprio tema GTK nelle applicazioni Qt si deve eseguire:

```
qtconfig

```

# Altri trucchi

## Menu di KDE per le applicazioni GTK2

KGtk è uno script wrapper che sfrutta LD_PRELOAD per forzare i menu di KDE (apri, salva, ecc) nelle applicazioni GTK2\. Se si sta usando KDE e si preferiscono i suoi menu sulle applicazioni GTK è possibile installare kgtk da AUR. Una volta installato è possibile eseguire le applicazioni GTK2 tramite kgtk-wrapper in due modi (nell'esempio useremo gimp).

Chiamando kgtk-wrapper direttamente e usando i binari GTK2 come argomento

```
/usr/bin/kgtk-wrapper gimp

```

OPPURE

Creando un link simbolico alle kgtk usando il nome dei binari GTK2\. In seguito è possibile eseguire /usr/local/bin/gimp per eseguire gimp con i menu di KDE.

```
ln -s /usr/bin/kgtk-wrapper /usr/local/bin/gimp
/usr/bin/gimp

```

## Usare uno stile GTK personalizzato

E' possibile usare uno stile personalizzato per le applicazioni GTK2\. Per fare questo usare GTK2_RC_FILES=/path/to/theme/gtk-2.0/gtkrc nomeApplicazione

Ad esempio:

```
GTK2_RC_FILES=/usr/share/themes/QtCurve/gtk-2.0/gtkrc firefox

```

Esegue firefox con il tema QtCurve.

# Troubleshooting

## I temi non funzionano nelle applicazioni GTK

Se lo stile o il motore dei temi configurato non visualizza le applicazioni GTK il problema potrebbe essere che le impostazioni GTK per qualche ragione non vengono caricate. Si può verificare dove il sistema si aspetta di trovare questi file digitando:

```
$ export | grep gtk

```

Di solito, per le GTK2, i file dovrebbero trovarsi in ~/.gtkrc for GTK1, ~/.gtkrc2.0 or ~/.gtkrc2.0-kde

Le nuove versioni di gtk-qt-engine usano ~/.gtkrc2.0-kde, inoltre impostano ed esportano ~/.kde/env/gtk-qt-engine.rc.sh Se si è recentemente rimosso gtk-qt-engine e si sta' tentando di impostare un tema GTK, per prima cosa si dovrebbe rimuovere ~/.kde/env/gtk-qt-engine.rc.sh e riavviare. Questo assicura che le GTK cerchino le proprie impostazioni in ~/.gtkrc2.0 al posto di ~/.gtkrc2.0-kde.