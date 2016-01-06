# Java package guidelines (Italiano)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

_Questo documento definisce uno standard proposto per pacchettizzare i programmi Java sotto Arch Linux. I programmi Java sono notoriamente difficili da pacchettizzare in maniera pulita senza sovrascrivere dipendenze. Questo documento descrive un metodo per rimediare a questa situazione. Queste linee guida sono flessibili nell'ottica di coprire i molti possibili scenari che si possono verificare quando si ha a che fare con applicazioni Java._

## Contents

*   [1 Introduzione](#Introduzione)
*   [2 Struttura di una tipica Applicazione Java](#Struttura_di_una_tipica_Applicazione_Java)
*   [3 Arch Java Packaging](#Arch_Java_Packaging)
    *   [3.1 Implementazione di API multiple](#Implementazione_di_API_multiple)
    *   [3.2 Esempio di albero di directory](#Esempio_di_albero_di_directory)
    *   [3.3 Dipendenze](#Dipendenze)

## Introduzione

I packagers Arch Linux non sembrano trovare un accordo su come gestire i pacchetti Java. Vari metodi sono utilizzati nei `PKGBUILD` che si trovano sui repository ufficiali, in quelli non ufficiali e su [AUR](https://aur.archlinux.org/). Queste soluzioni includono la presenza dell'intero pacchetto in `/opt` con script da shelli in `/usr/bin` o profili posizionati in `/etc/profile`. Altri pacchetti sono collocati nelle directories in `/usr/share` con script posizionati in `/usr/bin`. Molti aggiungono file non necessari a `CLASSPATH` and `PATH`.

## Struttura di una tipica Applicazione Java

La maggior parte delle applicazioni desktop Java ha una struttura simile. Esse sono installate da un installer indipendente dal sistema (ma dipendente dal pacchetto!). Questo installer solitamente installa tutto in una singola directory con sottodirectory chiamate `bin`, `lib`, `jar`, `conf`, etc. Solitamente c'è un file jar primario che contiene le principali classi eseguibili. Solitamente viene fornito uno script che esegue le classi fondamentali così che l'utente non debba invocare l'interprete Java direttamente. Questo script è solitamente abbastanza complesso, dato che è generico per tutte le distribuzioni, e spesso include opzioni particolari per i differenti sistemi (es: CYGWIN).

La directory `lib` spesso contiene dei file jar collegati tra loro che soddisfano le dipendenze dell'applicazione Java. Ciò rende semplice per l'utente installare il programma (essendo incluse tutte le dipendenze), ma rende il pacchetto un incubo per lo sviluppatore. È uno spreco di spazio quando diversi pacchetti contengono la stessa dipendenza. In passato, quando c'erano meno applicazioni e librerie Java, e quelle esistenti tendevano comunque ad essere molto grandi, non rappresentava un problema rilevante. Ora però le cose sono cambiate...

Altri file necessari ad eseguire il programma sono solitamente inclusi nella stessa cartella del file jar primario, in una sua sottodirectory. Dal momento che i programmi Java non sanno da dove le loro classi vengono prese, solitamente c'è bisogno di eseguirli nella stessa directory (per esempio uno scrpt potrebbe dare `cd` nella directory), oppure deve essere impostata una variabile d'ambiente che indichi la posizione della directory.

## Arch Java Packaging

Pacchettizzare applicazioni Java in Arch richiederà un po' più di lavoro per i manutentori rispetto a quanto ne richieda attualmente. Tuttavia ne varrà la pena, dal momento che si otterrà un filesystem più pulito e con meno dipendenze inglobate (e man mano che sempre più librerie Java saranno ricompilate nei loro pacchetti, pacchettizzare diventerà sempre più facile). Nel creare un pacchetto Java per Arch Linux si dovrebbero seguire le seguenti linee guida:

*   Se una libreria Java ha un nome generico, il nome del pacchetto dovrebbe avere il prefisso `java-` in modo da distinguerlo dalle altre librerie. Ciò non è necessario per i pacchetti dal nome univoco (come JUnit), per i programmi end-user (come Eclipse), o per le librerie che possono essere descritte con un altro prefisso (come jakarta-commons-collections or apache-ant).

*   Non è necessario compilare le applicazioni Java dai sorgenti. Nel processo di compilazione ci va pochissima compilazione, come per i binari creati da gcc. Se il pacchetto originario fornisce un metodo semplice di costruire da sorgente, va usato quello; ma se è più semplice prendere semplicemente una release binaria di un file jar o un installer, si può usare anche quel metodo.

*   Tutti i file jar (e solo quelli) distrubuiti col programma vanno posizionati nella directory `/usr/share/java/myprogram`. Ciò comprende tutte i file jar dipendenti distribuiti con l'applicazione. Va comunque fatto lo sforzo di mettere le dipendenze comuni o le grandi librerie dentro i loro rispettivi pacchetti. Ciò può avvenire solo se il programma non dipende da una specifica versione di una libreria dipendente.

Questa regola rende possibile il refactoring iterarivo delle dipendenze. Cioè, il pacchetto e tutte le sue dipendendenze possono essere inizilamente messi dentro una sola directory, Dopo il test, le principali dipendenze possono essere sottoposte a refactoring una alla volta. È da notare come alcune applicazioni includono dipendenze bundle all'interno del file jar primario (cioè estraggono dal jar le dipendenze e le inglobano nel loro jar). Tali dipendenze sono solitamente poco ingombranti e vi è poco vantaggio nel sottoporle a refactoring.

*   Se il programma deve essere eseguito dall'utente, scrivere uno script personalizzato che esegua il file jar primario. Questo script dovrebbe essere posizionato in `/usr/bin`. Le librerie generalmente non richiedono script. È meglio scrivere lo script da zero piuttosto che usarne uno incluso nel programma. Rimuovere il codice che controlla l'esistenza di di ambienti personalizzati (come CYGWIN), e il codice che tenta di determinare se la variabile `JAVA_HOME` è stata inizializzata (il pacchetto J2RE assicura che `JAVA_HOME` venga adeguatamente inizializzata)

Uno script con queste caratteristiche dovrebbe apparire così per i jar:

```
#!/bin/sh
"$JAVA_HOME/bin/java" -jar '/usr/share/java/PROGRAMNAME/PROGRAMNAME.jar'

```

e così per i singoli file delle classi:

```
#!/bin/sh
"$JAVA_HOME/bin/java" '/usr/share/java/PROGRAMNAME/PROGRAMCLASSNAME'

```

*   Impostare il il `CLASSPATH` mediante l'opzione `-cp` nell'interprete Java, am meno che non vi sia una motivazione esplicita di non farlo (per esempio: il `CLASSPATH` è usato come un plugin ). Il `CLASSPATH` dovrebbe includere tutti i file jar nella directory `/usr/share/java/myprogram`, così come i file jar derivanti da librerie dipendenti che sono state sottoposte a refactoring in altre directory. Si potrebbe usare qualcosa di simile al codice seguente:

```
for name in /usr/share/java/myprogram/*.jar ; do
  CP=$CP:$name
done
CP=$CP:/usr/share/java/dep1/dep1.jar
java -cp $CP myprogram.java.MainClass

```

*   Assicurarsi che lo script sia eseguibile!

*   Altri files distribuiti col pacchetto dovrebbero essere archiviati in una directory col nome del pacchetto dentro a `/usr/share`. La posizione di tale directory potrebbe essere impostata in una variabile come `MYPROJECT_HOME` dentre lo script. Questa regola assume che il programma si aspetti che tutti i files siano nella stessa directory (come è lo standard per i pacchetti Java ). Se sembra più naturale mettere un file di configurazione da un'altra parte (per esempio, un demone in `/etc/rc.d` o dei log in `/var/log`), si è liberi di farlo.

Tenere a mente che `/usr` potrebbe essere montata in modalità read-only in alcuni sistemi. Se ci sono file nella directory condivisa che necessitano di essere scritti dall'applicazione, questi potrebbero essere riposizionati sotto `/etc`, `/var`, o la home dell'utente.

*   Come è lo standard per i pacchetti Arch Linux, se non si può aderire agli standard proposti sopra senza un considerevole lavoro, il pacchetto dovrebbe essere installato nella maniera preferita, con la directory risultante posizionata sotto `/opt`.

Ciò è utile per programmi che includono JREs o versioni personalizzate delle dipendenze, o altri strani o difficili sistemi.

### Implementazione di API multiple

Se il paccheto distribuisce api la cui implementazione è di uso comune (come il driver jdbc), la libreria dovrebbe essere posizionata in /usr/share/java/<apiname>. In tal modo le applicazioni che permetto all'utente di scegliere tra varie implementazioni sapranno dove andarle a cercare. Questo percorso andrebbe utilizzato solo per pacchetti grezzi di librerie. Se una tale implementazione è parte della distribuzione dell'applicazione, **non** collocare il file jar nel percorso comune, ma utilizzare la struttura di pacchetto ordinaria.

### Esempio di albero di directory

Per chiarire meglio il concetto, ecco un esempio dell'albero di directory per un ipotetico programma chiamato `pippo`. Dal momento che `pippo` è un nome comune, il pacchetto è chiamato `java-pippo`, ma occorre notare che ciò non si riflette enlla struttura delle directory:

*   `/usr/share/java/pippo/`
*   `/usr/share/java/pippo/pippo.jar`
*   `/usr/share/java/pippo/bar.jar` (incluse le dipendenze di `java-pippo`)
*   `/usr/share/pippo/`
*   `/usr/share/pippo/*.*` (file generici richiesti da `java-pippo`)
*   `/usr/bin/pippo` (script eseguibile da terminale)

### Dipendenze

I pacchetti Java potrebbero specificare _java-runtime_ o _java-environment_ come dipendenze, a seconda delle occorrenze.

Per la maggioranza dei pacchetti, _java-runtime_ è tutto quanto è necessario per eseguire un software scritto in java.

**java-runtime** è una dipendenza virtuale fornita da:

*   [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) (free)
*   [java-gcj-compat](https://aur.archlinux.org/packages/java-gcj-compat/)<sup><small>AUR</small></sup> (free)
*   [jre](https://aur.archlinux.org/packages/jre/)<sup><small>AUR</small></sup> (non-free)

_java-environment_ è richiesto da quei pacchetti che necessitano di compilare il codice sorgente di java nel bytecode.

**java-environment** è una dipendenza virtuale fornita da:

*   [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) (free)
*   [jdk](https://aur.archlinux.org/packages/jdk/)<sup><small>AUR</small></sup> (non-free)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Java_package_guidelines_(Italiano)&oldid=414485](https://wiki.archlinux.org/index.php?title=Java_package_guidelines_(Italiano)&oldid=414485)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package development (Italiano)](/index.php/Category:Package_development_(Italiano) "Category:Package development (Italiano)")