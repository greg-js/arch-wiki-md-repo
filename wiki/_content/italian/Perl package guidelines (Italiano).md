**[Linee guida per la creazione di pacchetti](/index.php/Creating_Packages_(Italiano) "Creating Packages (Italiano)")**

* * *

[Eclipse](/index.php/Eclipse_Plugin_Package_Guidelines_(Italiano) "Eclipse Plugin Package Guidelines (Italiano)") – [GNOME](/index.php/Gnome_Package_Guidelines_(Italiano) "Gnome Package Guidelines (Italiano)") – [Haskell](/index.php/Haskell_Package_Guidelines_(Italiano) "Haskell Package Guidelines (Italiano)") – [Java](/index.php/Java_Package_Guidelines_(Italiano) "Java Package Guidelines (Italiano)") – [Kernel](/index.php/Kernel_Module_Package_Guidelines_(Italiano) "Kernel Module Package Guidelines (Italiano)") – [Lisp](/index.php/Lisp_Package_Guidelines_(Italiano) "Lisp Package Guidelines (Italiano)") – [MinGW](/index.php?title=MinGW_PKGBUILD_Guidelines_(Italiano)&action=edit&redlink=1 "MinGW PKGBUILD Guidelines (Italiano) (page does not exist)") – [OCaml](/index.php/OCaml_Package_Guidelines_(Italiano) "OCaml Package Guidelines (Italiano)") – [Perl](/index.php/Perl_Package_Guidelines_(Italiano) "Perl Package Guidelines (Italiano)") – [Python](/index.php/Python_Package_Guidelines_(Italiano) "Python Package Guidelines (Italiano)") – [Ruby](/index.php/Ruby_Gem_Package_Guidelines_(Italiano) "Ruby Gem Package Guidelines (Italiano)") – [VCS](/index.php/VCS_PKGBUILD_Guidelines_(Italiano) "VCS PKGBUILD Guidelines (Italiano)") – [Wine](/index.php/Wine_PKGBUILD_Guidelines_(Italiano) "Wine PKGBUILD Guidelines (Italiano)") – [Other](/index.php?title=Nonfree_Applications_Package_Guidelines_(Italiano)&action=edit&redlink=1 "Nonfree Applications Package Guidelines (Italiano) (page does not exist)")

Crezione di [PKGBUILDs](/index.php/PKGBUILD_(Italiano) "PKGBUILD (Italiano)") per software scritto in [Perl](https://en.wikipedia.org/wiki/Perl "wikipedia:Perl").

## Contents

*   [1 Nomenclatura pacchetti](#Nomenclatura_pacchetti)
*   [2 Posizione dei files](#Posizione_dei_files)
*   [3 Note](#Note)
*   [4 Esempio](#Esempio)
*   [5 Automatizzazione](#Automatizzazione)
*   [6 Dipendenze dei moduli](#Dipendenze_dei_moduli)
    *   [6.1 Implementazione](#Implementazione)
    *   [6.2 Definizione delle dipendenze](#Definizione_delle_dipendenze)
    *   [6.3 Informazioni Metadata](#Informazioni_Metadata)
*   [7 Perl e versioning di Pacman](#Perl_e_versioning_di_Pacman)
*   [8 Argomenti avanzati](#Argomenti_avanzati)
    *   [8.1 Glossario](#Glossario)
        *   [8.1.1 Modulo](#Modulo)
        *   [8.1.2 Core Module](#Core_Module)
        *   [8.1.3 Dist Packages](#Dist_Packages)
    *   [8.2 Installazione di Perl locale](#Installazione_di_Perl_locale)
    *   [8.3 Moduli per l'installazione di moduli Perl](#Moduli_per_l.27installazione_di_moduli_Perl)
        *   [8.3.1 ExtUtils::MakeMaker](#ExtUtils::MakeMaker)
        *   [8.3.2 Module::Build](#Module::Build)
        *   [8.3.3 Module::Install](#Module::Install)
    *   [8.4 Variabili d'ambiente](#Variabili_d.27ambiente)
        *   [8.4.1 PERL_MM_USE_DEFAULT](#PERL_MM_USE_DEFAULT)
        *   [8.4.2 PERL_AUTOINSTALL](#PERL_AUTOINSTALL)
        *   [8.4.3 PERL_MM_OPT](#PERL_MM_OPT)
        *   [8.4.4 PERL_MB_OPT](#PERL_MB_OPT)
        *   [8.4.5 MODULEBUILDRC](#MODULEBUILDRC)
        *   [8.4.6 PERL5LIB](#PERL5LIB)
        *   [8.4.7 PERL_LOCAL_LIB_ROOT](#PERL_LOCAL_LIB_ROOT)
    *   [8.5 Esempio migliorato](#Esempio_migliorato)

## Nomenclatura pacchetti

Per quanto riguarda i moduli, il nome del pacchetto dovrebbe iniziare con `perl-`, mentre il resto dovrebbe essere ricavato dal nome del modulo scritto in minuscolo, sostituendo i due punti con dei trattini. Per esempio, il nome pacchetto corrispondente al modulo `HTML::Parser` sarà `perl-html-parser`. Le applicazioni in Perl, dovrebbero mantenere il loro nome, avendo però cura di scriverlo in minuscolo.

## Posizione dei files

I moduli Perl dovrebbero installare i propri files in `/usr/lib/perl5/vendor_perl/` (questo comportamento si può ottenere impostando la variabile `INSTALLDIRS`, come mostrato sotto). Nessun file dovrebbe essere inserito in `/usr/lib/perl5/site_perl/`, poichè quella directory è riservata ai pacchetti Perl non installati tramite il package manager. I files `perllocal.pod` e `.packlist` dovrebbero essere presenti. Le operazioni sopra elencate vengono eseguite nel PKGBUILD d'esempio mostrato sotto.

## Note

E' consigliabile inserire `any` nell'array `arch`, poichè la maggior parte dei pacchetti perl sono indipendenti dall'architettura del sistema installato.

## Esempio

E' possibile trovare un PKGBUILD d'esempio in `/usr/share/pacman/PKGBUILD-perl.proto`, fornito dal pacchetto [abs](https://www.archlinux.org/packages/?name=abs).

## Automatizzazione

Poichè Perl si basa su [CPAN](http://www.cpan.org/), esistono alcuni script che eseguono quanto scritto sopra automaticamente, risparmiandovi dallo scrivere i PKGBUILD a mano.

CPANPLUS (disponibile come [perl-cpanplus-dist-arch](https://www.archlinux.org/packages/?name=perl-cpanplus-dist-arch) nel repository [community]), è un plugin a CPAN che pacchettizza al volo i moduli installati tramite lo stesso. E' possibile consultare la documentazione online all'indirizzo: [https://metacpan.org/release/CPANPLUS-Dist-Arch](https://metacpan.org/release/CPANPLUS-Dist-Arch)

## Dipendenze dei moduli

Perl ha un modo particolare per definire le dipendenze di un pacchetto, rispetto ad altri sistemi come le python eggs o le ruby gems: un egg dipende da altri eggs; una gem da altre gems, mentre le varie Distribuzioni Perl dipendono dai moduli. I moduli sono disponibili esclusivamente tramite distribuzioni CPAN, ma una distribuzione dipende da altre distribuzioni in maniera indiretta: un modulo può definire una propria versione indipendente da quella della distribuzione a cui appartiene, specificandola all'interno del codice sorgente. Allo scopo, viene usata la variabile `$VERSION` che, quando si usano `strics` e `warnings`, viene indicata con la keyword `our`. Ad esempio:

```
package Foo::Module;
use warnings;
use strict;
our $VERSION = '1.00';

```

I moduli possono cambiare la propria versione a piacimento, ed essere indipendenti da quela della distribuzione. L'utilità di questo comportamento è alquanto dubbia, ma è importante tenerlo a mente. Le versioni dei vari moduli sono difficili da determinare all'infuori dell'interprete perl e richiedono il parsing del codice del modulo, o persino il caricamento dello stesso in perl. Tuttavia, dall'interno dell'interprete perl, determinare la versione di un modulo è molto semplice. Ad esempio:

```
use Foo::Module;
print $Foo::Module::VERSION, "\n";

```

### Implementazione

CPAN è l'acronimo di "Centralized Network for Perl Authors". Ogni mirror CPAN, contiene gli indici delle distribuzioni disponibili su CPAN, i moduli in esse contenuti e il nome dell'autore che le ha caricate, il tutto contenuto in semplici files di testo. L'indice più utile risiede in `/modules/02packages.details.txt.gz`, disponibile in ogni mirror CPAN. Il termine "packages" si riferisce alla keyword `package` propria del linguaggio perl, e non ad un entità simile ai pacchetti pacman. La shell CPAN, scritta in minuscolo è semplicemente uno script Perl che naviga tali indici alla ricerca dei moduli che si desidera installare.

I moduli sono elencati nel file `02packages.details.txt.gz`. Sulla stessa linea del nome del modulo/pacchetto, c'è il percorso al tarball della distribuzione contenente il modulo. Quando si richiede l'installazione di un modulo tramite _cpan_, quest'ultimo verrà cercato nell'elenco e sarà installata la relativa distribuzione. Durante l'installazione, verrà generata una lista di dipendenze. _Cpan_ proverà quindi a caricare ogni dipendenza nell'interprete perl: se un modulo della versione specificata non può essere caricato, il processo si ripete.

La shell _cpan_ non deve preoccuparsi di quale versione del modulo richiesto stia installando, poichè l'ultima versione del modulo soddisferà sicuramente la richiesta del modulo di cui era stata inizialmente richiesta l'installazione. Solamente l'ultima versione di ogni modulo viene elencata nel file `02packages.details.txt.gz` ma, sfortunatamente per l'autore di un pacchetto perl, non è sempre possibile fare affidamento sul fatto che i nostri pacchetti offrano l'ultima versione di una distribuzione perl e dei relativi moduli, poichè il controllo sulle dipendenze operato da Pacman, è molto più statico e rigido.

### Definizione delle dipendenze

Le dipendenze di una distribuzione Perl sono definite nei file `Makefile.PL` o `Build.PL`. Ad esempio, all'interno dello script `Makefile.PL`, viene chiamata la funzione `WriteMakeFile`, che genera il corrispondente `Makefile`:

```
use ExtUtils::MakeMaker;
WriteMakeFile(
    'NAME' => 'ArchLinux::Module',
    'VERSION' => '0.01',
    'PREREQ_PM' => { 'POSIX' => '0.01' },
);

```

Benchè il seguente sia un esempio un pò forzato, è importante capire che le dipendenze non vengono finalizzate fino all'esecuzione degli script `Makefile.PL` o `Build.PL`. Le dipendenze sono comunque specificate a runtime, il che significa che possono essere alterate o modificate sfruttando la potenza offerta da Perl. L'autore del modulo può, ad esempio, aggiungere, rimuovere o modificare la versione delle dipendenze richieste esattamente prima che la distribuzione sia installata. Alcune distribuzioni multipiattaforma dipendono da moduli specifici del sistema operativo sul quale sono eseguite.

Ad esempio, la distribuzione CPANPLUS verifica quali plugin del modulo `CPANPLUS::Dist` sono stati installati. Se vengono rilevati plugins per la versione di CPANPLUS correntemente installata sul sistema, essi vengono aggiunti ai prerequisiti della nuova versione di CPANPLUS. Fortunatamente per il pacchettizzatore Perl, la maggior parte delle dipendenze sono statiche come nell'esempio sopra citato, che richiede il modulo `POSIX` alla versione minima `0.01`.

### Informazioni Metadata

I file Meta contengono informazioni relative ad una specifica distribuzione, come nome, autore, descrizione astratta e moduli richiesti. Precedentemente, venivano utilizzati dei files nel formato YAML (`META.yml`), ma recentemente è stato completato il passaggio al formato JSON (`META.json`). Questi files possono essere modificati a mano, anche se vengono solitamente generati dagli script `Makefile.PL` o `Build.PL` quando si pacchettizza una distribuzione per il rilascio. L'ultima versione della specifica è descritta nella relativa [documentazione online](http://search.cpan.org/perldoc?CPAN::Meta::Spec)

Si ricordi che le dipendenze possono essere cambiate a runtime! Per questo motivo, viene generato un altro file contenente i metadata dopo aver eseguito gli script di pacchettizzazione. Il file è chiamato `MYMETA.json` e contiene i cambiamenti effettuati a runtime dallo script; quindi potrebbe differire dal file meta generato durante la pacchettizzazione per CPAN.

Distribuzioni più datate di CPAN non disponevano di file meta, e i prerequisiti venivano semplicemente descritti nel `Makefile.PL`.

## Perl e versioning di Pacman

In Perl le versioni sono numeri, mentre in pacman stringhe.

Perl ammette versioni decimali nel formato `5.002006`, oppure utilizzando i punti (`5.2.6`). Potrebbe essere difficile comparare i due formati, perciò Perl converte la notazione puntata in versione decimale usando gli zeri come padding. Ogni punto separa fino a tre cifre e `5.2.6` diventa `5.002006`. E' ora semplice effettuare un confronto con un pò di aritmetica! La [documentazione](https://metacpan.org/module/version::Internals) per il modulo `version.pm` descrive nel dettaglio la conversione.

La cosa importante da ricordare è che Perl compara le versioni esattamente come farebbe con due numeri. `5.10 = 5.1` Semplice, no? Con la notazione puntata, le cose non sono così semplici. `5.1.1 == 5.001001`. La cosa peggiore in tutto questo è che la maggior parte degli altri sistemi considerano le versioni come stringhe, facendo apparire Perl come un estraneo.

Pacman funziona meglio utilizzando la notazione puntata, poichè i componenti sono divisi in caratteri non alfanumerici e confrontati uno ad uno come interi. Il primo componente non uguale determina quale versione è minore o maggiore dell'altra. Il componente dalla lunghezza più lunga, preso come stringa, è considerato maggiore, il che significa che `5.0001` è più grande di `5.1`. `5.10` è quindi maggiore di `5.1`.

Il problema è che cambiare la lunghezza della stringa di versione confonde pacman. Si considerino i rilasci di [AnyEvent](https://metacpan.org/release/AnyEvent):

1.  6.01 (2011-08-26)
2.  6.02 (2011-08-26)
3.  6.1 (2011-10-24)
4.  6.11 (2011-11-22)
5.  6.12 (2011-12-12)

Il `6.1` centrale può causare problemi, in quanto la lunghezza della stringa è diminuita. Nel mondo di pacman, `6.1` è minore di `6.02`. Se un pacchetto dipende da `perl-anyevent>=6.02` e la versione `6.1` è disponibile nei repository, allora non sarà possibile soddisfare la dipendenza.

Una soluzione è quella di utilizzare degli zeri come padding, e riservare lo stesso trattamento alle dipendenze. La versione `6.1` diventerà quindi `6.10`.

## Argomenti avanzati

Una volta che si è acquisita dimestichezza con la creazione di pacchetti perl, è possibile leggere la sezione sottostante, che potrebbe offrire parecchi spunti interessanti. Le informazioni sotto riportate potrebbero inoltre essere utili per risolvere i problemi di pacchettizzazione.

### Glossario

Si dovrebbe aver già acquisito familiarità con i seguenti termini:

#### Modulo

In Perl, moduli sono dichiarati con la parola chiave `package`. Essi sono contenuti all'interno di un file con estensione `.pm`, che può a sua volta ospitare diversi moduli al suo interno. I namespace dei moduli sono separati da `::`, (due doppi punti), ad esempio: `Archlinux::Modulo`. Quando si carica un modulo, i due doppi punti sono sostituiti con uno slash. Per esempio, il modulo `Archlinux::Modulo` caricherà il file `Archlinux/Modulo.pm`.

#### Core Module

I Core Modules sono quelli inclusi in un'installazione di Perl, ed alcuni di essi sono disponibili _solamente_ con Perl stesso. Altri moduli possono invece essere scaricati tramite CPAN.

#### Dist Packages

Sono l'equivalente Perl di un pacchetto di Archlinux. I dist packages sono archivi `.tar.gz` pieni di files con estensione .pm, tests, documentazione, e tutto il necessario per i moduli ivi contenuti.

### Installazione di Perl locale

Il fatto che i programmatori perl potrebbero voler installare diverse versioni di perl potrebbe rappresentare un problema, benchè ciò sia utile per verificare la retrocompatibilità dei programmi. Compilare una propria versione di perl potrebbe garantire inoltre benefici prestazionali. Inoltre, poichè spesso il perl di sistema non è all'ultima versione disponibile, l'utente potrebbe decidere di voler provare una versione più recente.

Se l'utente ha l'eseguibile perl nel proprio `$PATH`, esso verrà eseguito quando si scrive il comando "perl" nella shell. Inoltre, questo verrà eseguito anche all'interno del `PKGBUILD`, cosa che potrebbe causare problemi di difficile individuazione.

Il problema principale risiede nei moduli XS, che fungono da bridge tra Perl e C, usando le API proprie del Perl. Poichè queste ultime possono cambiare in modo significativo tra due versioni di Perl, se l'utente compila dei moduli XS con la propria versione dell'interprete, questi saranno incompatibili con il Perl di sistema, il quale darà luogo ad un errore di linkin quando si proverà a caricarli.

Una soluzione potrebbe essere quella di specificare il path assoluto dell'interprete di sistema (`/usr/bin/perl`) quando si richiama il comando perl nel `PKGBUILD`.

### Moduli per l'installazione di moduli Perl

Uno dei maggiori vantaggi del Perl, è la grande varietà di moduli/dist packages installabili tramite CPAN. Tra gli altri, esistono moduli che si occupano dell'installazione di... moduli!

Ne esistono di diversi tipi, ma generalmente il procedimento è sempre lo stesso e si basa sull'inserimento di un piccolo build script nel pacchetto contenente il modulo perl: avviando questo script, il processo di compilazione e installazione ha inizio.

Di seguito, un elenco dei moduli più comuni:

#### ExtUtils::MakeMaker

	Build script

	`MakeFile.PL`

	CPAN Link

	[http://search.cpan.org/dist/ExtUtils-MakeMaker](http://search.cpan.org/dist/ExtUtils-MakeMaker)

Il primo, e più vecchio è sicuramente `ExtUtils::MakeMaker`. Il principale svantaggio di questo sistema, è che richiede l'utility `make` affinché possa compilare ed installare il tutto. Benchè questo non sia un grande problema su un sistema Linux, può diventare problematico per utenti Windows! La comunità Perl sta cercando di incoraggiare l'uso di moduli più nuovi, che non hanno questo problema.

#### Module::Build

	Build Script

	`Build.PL`

	CPAN Link

	[http://search.cpan.org/dist/Module-Build](http://search.cpan.org/dist/Module-Build)

Il vantaggio principale derivante dall'uso di questo modulo, è che usa solamente perl e perciò non richiede l'utility `make` per funzionare. Un tempo, la sua installazione era abbastanza difficoltosa, poichè non era possibile eseguire il build script senza averlo prima installato. Ad oggi, ciò non rappresenta più un problema, visto `Module::Build` fa parte dei core modules.

#### Module::Install

	Build Script

	`Makefile.PL`

	CPAN Link

	[http://search.cpan.org/dist/Module-Install](http://search.cpan.org/dist/Module-Install)

Di recente introduzione, `Module::Install` richiede che `make` sia installato per funzionare. È stato scritto per essere un sostituto naturale di `ExtUtils::MakeMaker`, oltre che per compensare ad alcune delle sue mancanze.

Una caratteristica molto interessante di questo modulo, è che ne viene fornita una copia all'interno del dist package, cosicchè, a differenza dei moduli sopra menzionati, non sia necessario installarlo nel sistema.

Un'altra caratteristica di rilievo è l'auto-install. _Anche se l'uso di questa feature non è raccomandato, questa viene usata molto spesso_. Quando l'autore del modulo ne abilita l'uso, `Module::Install` procederà alla ricerca e all'installazione di tutti i moduli richiesti che non siano presenti al momento dell'esecuzione di `Makefile.PL`. Benchè questa funzione venga disabilitata quando `Module::Install` viene eseguito da `CPAN` o `CPANPLUS`, ciò non accade se viene utilizzato all'interno di un **PKGBUILD**! Si veda [PERL_AUTOINSTALL](#PERL_AUTOINSTALL) per risolvere il problema.

### Variabili d'ambiente

Alcune variabili di sistema, possono influenzare il modo in cui i moduli sono compilati o installati, e potrebbero causare problemi inaspettati se usate in modo scorretto, specialmente all'interno di un `PKGBUILD`.

#### PERL_MM_USE_DEFAULT

Quando questa variabile ha valore "true", i sistemi di installazione dei moduli descritti sopra, risponderanno ad eventuali domande con una risposta affermativa.

#### PERL_AUTOINSTALL

È possibile passare degli argomenti a linea di comando aggiuntivi a `Module::Install` attraverso questa variabile. Per disattivare l'auto-install (_altamente consigliato_), si assegni il valore `--skipdeps` a questa variabile.

```
export PERL_AUTOINSTALL="--skipdeps"

```

#### PERL_MM_OPT

Questa variabile consente, similmente a PERL_AUTOINSTALL, di passare degli argomenti al sistema di build. Per esempio, è possibile installare i moduli nella propria home directory usando:

```
export PERL_MM_OPT=INSTALLBASE=~/perl5

```

#### PERL_MB_OPT

Uguale a PERL_MM_OPT, questa variabile è riservata a `Module::Build`. Come sopra, per installare i moduli nella propria home directory:

```
export PERL_MB_OPT=--install_base=~/perl5

```

#### MODULEBUILDRC

`Module::Build` permette di scavalcare gli argomenti a riga di comando con un file di configurazione. Di default, questo è `~/.modulebuildrc`. È possibile definire un file di configurazione personalizzato inserendone il percorso in `MODULEBUILDRC`.

#### PERL5LIB

È possibile definire le directory in cui le librerie verranno cercate (in particolare se le stesse utilizzano `Local::Lib`) definendo `PERL5LIB`. Si azzeri il valore della variabile prima di procedere con la compilazione.

#### PERL_LOCAL_LIB_ROOT

Se l'utente usa `Local::Lib`, la variabile `PERL_LOCAL_LIB_ROOT` sarà automaticamente definita. Si azzeri il suo valore prima di procedere con la compilazione.

### Esempio migliorato

Usando le nozioni appena acquisite, è possibile creare un PKGBUILD che resisterà a qualunque tentativo di sabotaggio da parte delle variabili d'ambiente:

 `PKGBUILD` 

```
# Contributor: Your Name <youremail@domain.com>
pkgname=perl-foo-bar
pkgver=VERSION
pkgrel=1
pkgdesc='This is the awesome Foo::Bar module!'
arch=('any')
url='http://search.cpan.org/dist/Foo-Bar'
license=('GPL' 'PerlArtistic')
depends=('perl>=5.10.0')
makedepends=()
provides=()
conflicts=()
replaces=()
backup=()
options=('!emptydirs')
install=
source=("http://search.cpan.org/CPAN/authors/id/***/***-$pkgver.tar.gz")
md5sums=()

build() {
  cd "$srcdir/***-$pkgver"

  # Setting these env variables overwrites any command-line-options we don't want...
  export PERL_MM_USE_DEFAULT=1 PERL_AUTOINSTALL=--skipdeps \
    PERL_MM_OPT="INSTALLDIRS=vendor DESTDIR='$pkgdir'" \
    PERL_MB_OPT="--installdirs vendor --destdir '$pkgdir'" \
    MODULEBUILDRC=/dev/null

  # If using Makefile.PL
  { /usr/bin/perl Makefile.PL &&
    make &&
    make test &&
    make install; } || return 1

  # If using Build.PL
  { /usr/bin/perl Build.PL &&
    ./Build &&
    ./Build test &&
    ./Build install; } || return 1
}

```