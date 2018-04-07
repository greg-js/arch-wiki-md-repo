Articoli correlati

*   [Apache OpenOffice](/index.php/Apache_OpenOffice "Apache OpenOffice")

Da [Home - LibreOffice](https://it.libreoffice.org/):

	*LibreOffice è la suite Open Source di produttività personale per Windows, Macintosh e Linux, che offre sei applicazioni ricche di funzionalità per tutte le necessità di produzione di documenti ed elaborazione dati: Writer, Calc, Impress, Draw, Math e Base. La nostra grande comunità dedicata di utenti, contributori e sviluppatori offre gratuitamente [supporto](https://it.libreoffice.org/supporto/) e [documentazione](https://it.libreoffice.org/supporto/documentazione/). Anche voi potete [contribuire](https://it.libreoffice.org/contribuire/)!*

## Contents

*   [1 LibreOffice in Arch Linux](#LibreOffice_in_Arch_Linux)
*   [2 Installazione](#Installazione)
    *   [2.1 Fonts Microsoft](#Fonts_Microsoft)
*   [3 Temi](#Temi)
    *   [3.1 Temi di Firefox](#Temi_di_Firefox)
*   [4 Gestione delle estensioni](#Gestione_delle_estensioni)
*   [5 Ausili alla scrittura](#Ausili_alla_scrittura)
    *   [5.1 Correttore lessicale](#Correttore_lessicale)
    *   [5.2 Regole di sillabazione](#Regole_di_sillabazione)
    *   [5.3 Thesaurus](#Thesaurus)
    *   [5.4 Controllo grammaticale](#Controllo_grammaticale)
*   [6 Installare macro](#Installare_macro)
*   [7 Aumentare la velocità di LibreOffice](#Aumentare_la_velocit.C3.A0_di_LibreOffice)
*   [8 Risoluzione di problemi](#Risoluzione_di_problemi)
    *   [8.1 Rimpiazzo dei fonts](#Rimpiazzo_dei_fonts)
    *   [8.2 Anti-aliasing](#Anti-aliasing)
    *   [8.3 Rallentamenti mentre si usa NFSv3](#Rallentamenti_mentre_si_usa_NFSv3)
    *   [8.4 Risolvere l'errore Java Framework](#Risolvere_l.27errore_Java_Framework)
    *   [8.5 LibreOffice non rileva i miei certificati](#LibreOffice_non_rileva_i_miei_certificati)
    *   [8.6 Aprire i file .pps in modalità di modifica senza avviare la presentazione](#Aprire_i_file_.pps_in_modalit.C3.A0_di_modifica_senza_avviare_la_presentazione)
    *   [8.7 Problema Bibliography](#Problema_Bibliography)
    *   [8.8 Video support](#Video_support)

## LibreOffice in Arch Linux

Arch Linux ha terminato il supporto a [OpenOffice.org](/index.php/OpenOffice.org "OpenOffice.org") in favore di LibreOffice, il fork curato da "Document Foundation", che include miglioramenti e nuove strumenti. Annuncio: [Dropping Oracle OpenOffice (arch-general)](https://mailman.archlinux.org/pipermail/arch-general/2011-March/018819.html).

## Installazione

LibreOffice è adesso presente in due versioni:

*   [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh) è il ramo con più funzionalità e miglioramenti.
*   [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) è il ramo di supporto e manutenzione della versione precedente.

LibreOffice è stato diviso in molti pacchetti. Quando si [installa](/index.php/Pacman "Pacman") [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) si aprirà un menu per permettere la scelta dei componenti desiderati mentre [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh) non è diviso in gruppi ed esistono i pacchetti per le lingue.

**Note:**

*   Si deve scegliere un pacchetto per la lingua dell'interfaccia: il primo in ordine alfabetico è l'Afrikaans, l'italiano è il numero 44 per fresh (163 per still) , l'inglese (en-GB) è il numero 25 per fresh (139 per still). Un errore comune consite nell'installare il pacchetto [libreoffice-still-uk](https://www.archlinux.org/packages/?name=libreoffice-still-uk)

Verificate le dipendenze raccomandate. Per esempio, Java Runtime Environment (opzionale, fortemente raccomandato). Vedi: [Java](/index.php/Java_(Italiano) "Java (Italiano)"). Per usare [alcuni moduli](https://wiki.documentfoundation.org/Base#Java_and_HSQLDB) di LibreOffice Base può servire [hsqldb2-java](https://aur.archlinux.org/packages/hsqldb2-java/).

### Fonts Microsoft

I fonts Microsoft sono utili a evitare problemi di impaginazione. Per informazioni consultate la pagina [MS Fonts](/index.php/MS_Fonts "MS Fonts").

## Temi

Per l'integrazione con Qt, installate [libreoffice-still-kde4](https://www.archlinux.org/packages/?name=libreoffice-still-kde4). Per l'integrazione con GTK+ installate [libreoffice-still-gnome](https://www.archlinux.org/packages/?name=libreoffice-still-gnome).

**Note:**

*   Qt è in grado di usare il tema GTK+. Questa scelta si attua nella finestra di dialogo che si apre con il comando `qtconfig-qt4`.
*   Questi pacchetti sono indipendenti dagli ambienti grafici in uso. Si possono usare per ottenere un aspetto più piacevole di quello predefinito (simile a Windows 95).

Da LibreOffice 3.5.x, il programma tenta di capire quale ambiente desktop è utilizzato con la seguente priorità:

```
 gtk3 > gtk2 > kde4 > generico

```

Per forzare un tipo di interfaccia bisogna anteporre la variabile `SAL_USE_VCLPLUGIN` al nome del programma e attribuirle un valore in questo modo:

```
SAL_USE_VCLPLUGIN=gen lowriter
SAL_USE_VCLPLUGIN=kde4 lowriter 
SAL_USE_VCLPLUGIN=gtk lowriter 
SAL_USE_VCLPLUGIN=gtk3 lowriter

```

Per salvare la scelta si deve salvare il valore della variabile in un file di configurazione della shell: `/etc/bash.bashrc` o `~/.bashrc` se si usa bash.

**Note:** L'interfaccia GTK+ 3 è ancora sperimentale: per abilitarla è necessario abilitare "experimental features" nella finestra delle opzioni di di LibreOffice. Se comunque rimane un'interfaccia in stile Windows 95 deselezionate "Automatically detect high contrast mode of the system" in *Strumenti > Opzioni > Accessibilità*.

### Temi di Firefox

LibreOffice 4.x può usare i temi di Firefox. Aprite *Strumenti > Opzioni* in LibreOffice, scegliete "Personalizzazione > Scegli Personas" e incollate l'indirizzo URL del vostro tema preferito. Un opportuno bottone nella finestra di scelta vi permetterà di aprire il browser.

## Gestione delle estensioni

Attualmente si trovano nei repository di Arch Linux alcune estensioni per LibreOffice:

*   [libreoffice-still-extension-nlpsolver](https://www.archlinux.org/packages/?name=libreoffice-still-extension-nlpsolver)
*   [libreoffice-still-extension-wiki-publisher](https://www.archlinux.org/packages/?name=libreoffice-still-extension-wiki-publisher)

Per ottenere un maggior numero di estensioni si può usare [AUR](/index.php/AUR "AUR") oppure il gestore incluso in LibreOffice o visitare [[1]](http://extensions.libreoffice.org/extension-center) o [[2]](http://libreplanet.org/wiki/Group:OpenOfficeExtensions/List).

## Ausili alla scrittura

### Correttore lessicale

Per la correzione lessicale si deve installare [hunspell](https://www.archlinux.org/packages/?name=hunspell) e un pacchetto relativo alla lingua, come [hunspell-en](https://www.archlinux.org/packages/?name=hunspell-en) per l'inglese o [hunspell-it](https://www.archlinux.org/packages/?name=hunspell-it) per l'italiano.

### Regole di sillabazione

Per la sillabazione servono il pacchetto [hyphen](https://www.archlinux.org/packages/?name=hyphen) e un insieme di regole come ([hyphen-en](https://www.archlinux.org/packages/?name=hyphen-en) per l'inglese, [hyphen-it](https://www.archlinux.org/packages/?name=hyphen-it) per l'italiano, etc.

### Thesaurus

Per avere la possibilità di usare thesaurus, installate [libmythes](https://www.archlinux.org/packages/?name=libmythes) e un pacchetto mythes come [mythes-en](https://www.archlinux.org/packages/?name=mythes-en) per l'inglese, [mythes-it](https://www.archlinux.org/packages/?name=mythes-it) per l'italiano, etc.

### Controllo grammaticale

Per il controllo grammaticale, serve un estensione come LanguageTool che si trova [AUR](/index.php/Arch_User_Repository "Arch User Repository"): [libreoffice-extension-languagetool](https://aur.archlinux.org/packages/libreoffice-extension-languagetool/) oppure nel [sito di LanguageTool](http://www.languagetool.org/).

Le possibili alternative si trovano nella [pagina delle estensioni](http://libreplanet.org/wiki/Group:OpenOfficeExtensions/List) o nel sito di [OpenOffice](http://lingucomponent.openoffice.org/grammar.html), ma non è garantito che le estensioni per OpenOffice funzionino su LibreOffice.

## Installare macro

Se si vuole usare macro occorre un Java Runtime Environment. Si può abilitarlo dal menu a prezzo di perdere [velocità di avvio](#Speed_up_LibreOffice). Il percorso predefinito per le macro su Arch Linux è diverso da quello di molte altre distribuzioni ed è:

```
~/.config/libreoffice/4/user/Scripts/

```

## Aumentare la velocità di LibreOffice

Alcune impostazioni possono migliorare il tempo di caricamento e di risposta di LibreOffice, ma alcuni aumentano l'uso di RAM, quindi usateli con cautela. Scegliete *Strumenti > Opzioni*.

*   Sotto *Memoria*:
    *   Riducete il numero di *Undo steps* a 30.
    *   Sotto *Cache grafica* aumentate a 128 MB dai 20MB originari.
    *   Aumentate la memoria per oggetto a 20MB dai 5MB originari.
    *   Se usate spesso LibreOffice, scegliete *LibreOffice Quickstarter*.
*   Sotto *Avanzate*, deselezionate *Use a Java runtime environment*.

**Note:** Per una lista di funzionalità realizzate esclusivamente in Java controllate [https://wiki.documentfoundation.org/Development/Java](https://wiki.documentfoundation.org/Development/Java)

## Risoluzione di problemi

### Rimpiazzo dei fonts

Queste impostazioni si trovano in *Strumenti > Opzioni > LibreOffice > Fonts*. Selezionate la casella *Applica Tavola di Rimpiazzi*. Scegliete il font da rimpiazzare e il rimpiazzo con l'opzione *Rimpiazza con* e confermate. Scegliete *Sempre* o *Solo Schermo*. Confermate. Visitate i menu *Strumenti > Opzioni > LibreOffice > Vista* e deselezionate "Usa i font di sistema per l'interfaccia". Se usate font senza antialias, come Arial, deselezionate anche "Screen font antialiasing" per avere l'effetto desiderato.

### Anti-aliasing

Eseguite:

```
$ echo "Xft.lcdfilter: lcddefault" | xrdb -merge

```

Per rendere persistente il cambiamento, aggiungete `Xft.lcdfilter: lcddefault` a `~/.Xresources` file e successivamente eseguite:

```
$ xrdb -merge ~/.Xresources

```

[Referenze](https://bugs.launchpad.net/ubuntu/+source/openoffice.org/+bug/271283/comments/19). Visitate [X resources](/index.php/X_resources "X resources") per maggiori dettagli.

Se non funziona, provate ad aggiungere `Xft.lcdfilter: lcddefault` a `~/.Xdefaults`. Se `~/.Xresources` e `~/.Xdefaults` non sono presenti è necessario crearli.

### Rallentamenti mentre si usa NFSv3

Se LibreOffice rallenta quando si apre o si salva un documento su una cartella condivisa di tipo NFS, provate ad anteporre `#` alle seguenti linee nel file `/usr/lib/libreoffice/program/soffice`:

```
# file locking now enabled by default
SAL_ENABLE_FILE_LOCKING=1
export SAL_ENABLE_FILE_LOCKING

```

Per evitare sovrascritture durante gli aggiornamenti, copiate `/usr/lib/libreoffice/program/soffice` in `/usr/local/bin`. Riferimento originale [qui](http://www.crazysquirrel.com/computing/debian/bugs/openoffice-over-nfs.jspx).

### Risolvere l'errore Java Framework

Nel caso di un errore all'avvio del tipo:

```
[Java framework] Error in function createSettingsDocument (elements.cxx).
javaldx failed!

```

cambiate i permessi di `~/.config/` in questo modo:

```
# chown -vR username:users ~/.config

```

[Post nel forum di Arch Linux](https://bbs.archlinux.org/viewtopic.php?id=93168).

### LibreOffice non rileva i miei certificati

Se non si vedono i certificati quando si prova a firmare un documento, occorre avere i certificati configurati in Mozilla Firefox (o Thunderbird). Se comunque LibreOffice non li mostra, indicateli esplicitamente con la variabile `MOZILLA_CERTIFICATE_FOLDER` indicando il profilo di Firefox o Thunderbird:

```
export MOZILLA_CERTIFICATE_FOLDER=$HOME/.mozilla/firefox/XXXXXX.default/

```

[Referenze](http://wiki.services.openoffice.org/wiki/Certificate_Detection).

### Aprire i file .pps in modalità di modifica senza avviare la presentazione

Un workaround consiste nel rinominare i file .pps in .ppt

Il seguente script può essere usato per effettuare rinomina e apertura al volo ed è utile da usare anche da un browser per aprire i .pps senza salvarli in modo permanente.

```
#!/bin/bash

f=$(mktemp)

cp "$1" "${f}.ppt" && libreoffice "${f}.ppt" && rm -f "${f}.ppt"

```

### Problema Bibliography

Se Writer si interrompe bruscamente mentre si tenta di accedere a *Strumenti > Bibliography Database* e mostra il seguente errore:

```
com::sun::star::loader::CannotActivateFactoryException

```

installate [libreoffice-still-base](https://www.archlinux.org/packages/?name=libreoffice-still-base) come workaround. Probabilmente è un difetto dovuto al bug [[3]](http://cgit.freedesktop.org/libreoffice/core/commit/?id=1889c1af41650576a29c587a0b2cdeaf0d297587).

### Video support

Se non funzionano i video inclusi nei documenti e si vedono solo riquadri grigi assicuratevi di acere installato [gst-plugins-base-libs](https://www.archlinux.org/packages/?name=gst-plugins-base-libs), *gst-plugins-[base|good|bad|ugly]* e [gst-libav](https://www.archlinux.org/packages/?name=gst-libav).