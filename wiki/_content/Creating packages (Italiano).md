# Creating packages (Italiano)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Articoli correlati

*   [Arch Build System (Italiano)](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)")
*   [Arch User Repository (Italiano)](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)")
*   [Arch Packaging Standards (Italiano)](/index.php/Arch_Packaging_Standards_(Italiano) "Arch Packaging Standards (Italiano)")
*   [makepkg (Italiano)](/index.php/Makepkg_(Italiano) "Makepkg (Italiano)")
*   [pacman (Italiano)](/index.php/Pacman_(Italiano) "Pacman (Italiano)")
*   [PKGBUILD (Italiano)](/index.php/PKGBUILD_(Italiano) "PKGBUILD (Italiano)")
*   [VCS PKGBUILD Guidelines](/index.php/VCS_PKGBUILD_Guidelines "VCS PKGBUILD Guidelines")

Questo articolo si propone di assistere gli utenti nella creazione dei propri pacchetti con il sistema di compilazione "ports-like" di Arch Linux. riguarda la creazione di un [PKGBUILD](/index.php/PKGBUILD_(Italiano) "PKGBUILD (Italiano)"), un pacchetto con la descrizione dei file sorgente utilizzato da `makepkg` per creare un pacchetto binario dal codice sorgente. Se si è già in possesso di un `PKGBUILD`, vedere [makepkg](/index.php/Makepkg_(Italiano) "Makepkg (Italiano)").

## Contents

*   [1 Introduzione](#Introduzione)
*   [2 Preparazione](#Preparazione)
    *   [2.1 Prerequisiti software](#Prerequisiti_software)
    *   [2.2 Scaricamento e test dell'installazione](#Scaricamento_e_test_dell.27installazione)
*   [3 Creazione di un PKGBUILD](#Creazione_di_un_PKGBUILD)
    *   [3.1 Definizione delle variabili PKGBUILD](#Definizione_delle_variabili_PKGBUILD)
    *   [3.2 La funzione build()](#La_funzione_build.28.29)
    *   [3.3 La funzione package()](#La_funzione_package.28.29)
    *   [3.4 Informazioni aggiuntive](#Informazioni_aggiuntive)
*   [4 Testare il PKGBUILD](#Testare_il_PKGBUILD)
    *   [4.1 ldd e namcap](#ldd_e_namcap)
*   [5 Invio di pacchetti di AUR](#Invio_di_pacchetti_di_AUR)
*   [6 Per ricapitolare](#Per_ricapitolare)
    *   [6.1 Avvertenze](#Avvertenze)
*   [7 Consultare inoltre](#Consultare_inoltre)

## Introduzione

I pacchetti in Arch Linux sono compilati utilizzando l'utilità [makepkg](/index.php/Makepkg_(Italiano) "Makepkg (Italiano)") e le informazioni memorizzate in un file [PKGBUILD](/index.php/PKGBUILD_(Italiano) "PKGBUILD (Italiano)"). Quando avviato, `makepkg` va alla ricerca di un `PKGBUILD` nella presente directory e segue le istruzioni per o compilare, o acquisire i file necessari ad essere impacchettati all'interno di un file pacchetto (`pkgname.pkg.tar.xz`). Il pacchetto risultante contiene i file binari e le istruzioni di installazione, facilmente installabili con [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)").

Un pacchetto di Arch non è altro che un archivio tar compresso utilizzando "xz", o "tarball", che contiene:

*   I file binari per l'installazione

*   `.PKGINFO`: contiene tutti i metadati necessari a pacman per gestire i pacchetti, le dipendenze, ecc.

*   `.INSTALL`: un file opzionale utilizzato per eseguire comandi dopo l'installazione, aggiornamento o rimozione degli stage. (Questo file è presente solo se specificato nel `PKGBUILD`)

*   `.Changelog`: un file opzionale conservato dal manutentore del pacchetto che documenta i cambiamenti dello stesso. (Non è presente in tutti i pacchetti)

## Preparazione

### Prerequisiti software

Prima di tutto assicurarsi che gli strumenti necessari siano installati. I pacchetti del gruppo "base-devel" dovrebbero essere sufficienti, in quanto includono _make_ e gli strumenti aggiuntivi necessari per la compilazione da sorgenti.

```
# pacman -S base-devel

```

Uno degli strumenti chiave per la creazione dei pacchetti è [makepkg](/index.php/Makepkg_(Italiano) "Makepkg (Italiano)") (fornito da [pacman](https://www.archlinux.org/packages/?name=pacman)) che esegue le seguenti operazioni:

1.  Controlla se le dipendenze dei pacchetti sono installate.
2.  Scarica i file sorgente dai server specificati.
3.  Scompatta il file sorgente.
4.  Compila il software e lo installa in un ambiente fakeroot.
5.  Identifica simboli da binari e librerie.
6.  Genera il file meta pacchetto, che è incluso in ogni pacchetto.
7.  Comprime l'ambiente fakeroot in un file pacchetto.
8.  Memorizza il file pacchetto nella directory di destinazione configurata, che è la directory di lavoro di default.

### Scaricamento e test dell'installazione

Scaricare il tarball sorgente del software desiderato, estrarlo, e seguire la procedura dell'autore per installare il programma. Prendere nota di tutti i comandi e/o passaggi necessari per la compilazione e l'installazione. Quegli stessi comandi verranno ripetuti nel file _PKGBUILD_.

La maggior parte degli autori di software aderisce al ciclo dei 3 passi di compilazione:

```
./configure
make
make install

```

Questo è un buon momento per assicurarsi che il programma funzioni correttamente.

## Creazione di un PKGBUILD

Quando `makepkg` viene eseguito, cercherà un file `PKGBUILD` nella directory di lavoro attuale. Se viene trovato un `PKGBUILD` verrà scaricato il codice sorgente del software e compilato seguendo le istruzioni specificate nel `PKGBUILD`. Le istruzioni devono essere interamente interpretabili dalla shell [Bash](https://en.wikipedia.org/wiki/Bash "wikipedia:Bash"). Dopo l'avvenuto completamento, i binari risultanti e metadati del pacchetto, ad esempio la versione del pacchetto e le dipendenze, verranno impacchettate in un file `pkgname.pkg.tar.xz` che può essere installato con `pacman -U [nome_pacchetto]`.

Per iniziare con un nuovo pacchetto, si deve prima creare una directory di lavoro vuota, (preferibilmente `~/abs/**pkgname**`), spostarsi in quella directory, e creare un file `PKGBUILD`. È possibile anche copiare il prototipo di PKGBUILD `/usr/share/pacman/PKGBUILD.proto` nella directory di lavoro o copiare un `PKGBUILD` da un pacchetto simile. Quest'ultimo può essere utile avendo solo bisogno di cambiare alcune opzioni.

### Definizione delle variabili PKGBUILD

Il file `PKGBUILD` contiene i metadati relativi a un pacchetto. Si tratta di un file di testo. Il seguente è un prototipo di `PKGBUILD`. È possibile trovarlo in `/usr/share/pacman` insieme ad altri modelli.

 `/usr/share/pacman/PKGBUILD.proto` 

```
# Questo è un esempio di file PKGBUILD. Utilizzare questo come un inizio di creare i propri,
#  rimuovere questi commenti. Per ulteriori informazioni, consultare 'man PKGBUILD'.
# NOTE: Si prega di compilare il campo licenza per il proprio pacchetto! Se è sconosciuto,
# si prega di mettere "sconosciuto".

# Maintainer: Your Name <youremail@domain.com>
pkgname=NAME
pkgver=VERSION
pkgrel=1
epoch=
pkgdesc=""
arch=()
url=""
license=('GPL')
groups=()
depends=()
makedepends=()
checkdepends=()
optdepends=()
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=
changelog=
source=($pkgname-$pkgver.tar.gz)
noextract=()
md5sums=() #generate with 'makepkg -g'

build() {
  cd "$srcdir/$pkgname-$pkgver"
  ./configure --prefix=/usr
  make
}

check() {
  cd "$srcdir/$pkgname-$pkgver"
  make -k check
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make DESTDIR="$pkgdir/" install
}

```

_makepkg_ definisce tre variabili che si dovrebbe usare come parte del processo di installazione e di compilazione:

`startdir`

Contiene il percorso assoluto della directory in cui è contenuto il file `PKGBUILD`. Questa variabile esiste per essere usata in combinazione con `/src` o i postfix `/pkg`, ma l'uso delle variabili `srcdir` e `pkgdir` è il metodo moderno. `$startdir/src` **non** è garantito per essere lo stesso di `$srcdir`, e così pure per `$pkgdir`. L'uso di questa variabile è obsoleto e fortemente scoraggiato.

`srcdir`

Questo punta alla directory in cui _makepkg_ estrae o copia tutti i file sorgente.

`pkgdir`

Questo punta alla directory in cui _makepkg_ sistema il pacchetto installato, che diventa la directory radice del pacchetto compilato.

**Note:** _makepkg_, e quindi le funzioni `build()` e `package()`, sono destinate ad essere non-interattive. Le utilità interattive o gli script richiamati in tali funzioni possono danneggiare _makepkg_, soprattutto se richiamate con il build-logging attivo (`-l`). (Consultare [Arch Linux Bug #13214](https://bugs.archlinux.org/task/13214))

Note: a parte il pacchetto maintainer attuale, vi possono essere precedenti manutentori sopra elencati come contributori.

Una spiegazione delle variabili `PKGBUILD` possibili può essere trovata nell'articolo [PKGBUILD](/index.php/PKGBUILD_(Italiano) "PKGBUILD (Italiano)").

### La funzione `build()`

Ora è necessario implementare la funzione `build()` nel file `PKGBUILD`. Questa funzione utilizza i comandi di shell comuni nella sintassi [Bash](http://en.wikipedia.org/wiki/Bash_%28Unix_shell%29) per compilare automaticamente il software e creare una directory `pkg` per installare il software. Questo permette a _makepkg_ di impacchettare i file senza dover passare al setaccio il filesystem.

Il primo passo della funzione `build()` è quello di spostarsi nella directory creata durante la decompressione dei sorgenti. Nella maggior parte dei casi il primo comando sarà simile a questo:

```
cd $srcdir/$pkgname-$pkgver

```

Ora sarà necessario elencare gli stessi comandi usati durante la compilazione manuale del software. La funzione `build()` in sostanza, consente di automatizzare tutto ciò che si è fatto a mano e compila il software nell'ambiente fakeroot di compilazione. Se il software che si è impacchettato usa uno script di configurazione, è buona norma usare `--prefix=/usr` quando si compilano i pacchetti per _pacman_. Moltissimi software installano i file relativi alla directory `/usr/local`, cosa che dovrebbe essere fatta solo avendo compilato manualmente dai sorgenti. Tutti i pacchetti Arch Linux dovrebbe usare la directory `/usr`. Come si vede nel file `/usr/share/pacman/PKGBUILD.proto`, le successive due righe sono spesso simili a questa:

```
./configure --prefix=/usr
make

```

### La funzione `package()`

Il passo finale è quello di mettere i file compilati in una directory in cui _makepkg_ sia in grado di recuperarli per creare un pacchetto. Questa, per impostazione predefinita è la directory `pkg`, un semplice ambiente fakeroot. La directory `pkg` replica la gerarchia del file system root nel percorso del software installato. Dovendo spostare manualmente i file sotto la root del filesystem, si dovrebbe installarli nella directory `pkg` sotto la stessa struttura della directory. Ad esempio, se si desidera installare un file in `/usr/bin`, dovrebbe invece essere messo in `$pkgdir/usr/bin`. Solo alcune procedure d'installazione richiedono all'utente di copiare decine di file manualmente. Al contrario, per la maggior parte del software, invocando `make install` verrà eseguito così. L'ultima riga dovrebbe essere simile alla seguente per installare correttamente il software nella directory `pkg`:

```
make DESTDIR=$pkgdir install

```

**Note:** A volte capita che `DESTDIR` non è utilizzato nel `Makefile`; potrebbe invece essere necessario utilizzare il `prefix`. Se il pacchetto è compilato con _autoconf_/_automake_, utilizzare `DESTDIR`; questo è ciò che è [documentato](http://sources.redhat.com/automake/automake.html#Install) nei manuali. Se `DESTDIR` non funziona, provare a compilare con `make prefix="$pkgdir/usr/" install`. Se questo non funziona, si dovranno fare degli approfondimenti per i comandi di installazione che vengono eseguiti da "`make <...> install`".

In alcuni rari casi, il software si aspetta di essere eseguito da una singola directory. In tali casi, è bene copiare semplicemente questi in `$pkgdir/opt`.

Molto spesso, il processo di installazione del software creerà una sottodirectory in `pkg`. Se così non fosse però, _makepkg_ genererà un sacco di errori e sarà necessario creare manualmente le sottodirectory aggiungendo gli appropriati comandi `mkdir -p` nella funzione `build()` prima che venga eseguita la procedura di installazione.

Nei pacchetti datati, non vi era alcuna funzione `package()`, e così, sistemare i file compilati veniva fatto alla fine della funzione `build()`. Se `package()` non è presente, eseguire `build()` tramite _fakeroot_. Se invece `package()` è presente, eseguire `build()` da utente con _makepkg_, `package()` tramite _fakeroot_.

`makepkg --repackage` esegue solo la funzione `package()`, così crea un file `*.pkg.*` senza compilare il pacchetto. Questo può risparmiare tempo, ad esempio avendo appena cambiato la variabile `depends` del pacchetto.

### Informazioni aggiuntive

Si prega di leggere [Arch Packaging Standards](/index.php/Arch_Packaging_Standards_(Italiano) "Arch Packaging Standards (Italiano)") per approfondimenti e considerazioni aggiuntive.

## Testare il PKGBUILD

Mentre si scrive la funzione `build()`, si vorrà collaudare frequentemente i cambiamenti, per essere sicuri che non ci siano bug. Questo si può fare usando il comando `makepkg` nella directory contenente il `PKGBUILD`. Con un `PKGBUILD`, propriamente formattato, makepkg creerà un pacchetto; ma con uno errato o non finito, restituirà un errore.

Se il processo di makepkg è finito correttamente, creerà un nuovo file chiamato `pkgname-pkgver.pkg.tar.xz` nella directory di lavoro. Questo è un pacchetto di pacman e può essere installato con `pacman -U`. Notare che il fatto che il pacchetto sia stato compilato non significa che funzioni! È plausibile che contenga solo la directory e nessun file se, per esempio, un `prefix` è stato specificato impropriamente. Si possono usare le funzioni di ricerca di pacman per visualizzare una lista di file contenuti nel pacchetto e le dipendenze da esso richieste con `pacman -Qlp [package file]` e `pacman -Qip [package file]`.

Se il pacchetto sembra essere valido, è tutto. Comunque, se si pensa di rilasciare il `PKGBUILD`, è obbligatorio controllare e ricontrollare e ricontrollare ancora i contenuti dell'array `depends`.

Assicurarsi inoltre che i pacchetti binari _funzionino_ effettivamente senza problemi È fastidioso rilasciare un pacchetto che contiene tutti i file necessari, ma si blocca a causa di qualche opzione di configurazione che non funziona bene con il resto del sistema. Se si sta compilando dei pacchetti per il proprio sistema, però, non c'è bisogno di preoccuparsi troppo di questo passaggio di controllo della qualità, essendo in questo caso, il creatore, l'unico a riportare tali errori.

### `ldd` e `namcap`

Le dipendenze sono l'errore più comune riguardo l'impacchettamento. Ci sono due ottimi strumenti che è possibile utilizzare per controllare le dipendenze. Il primo è _ldd_, che mostrerà le dipendenze delle librerie condivise dei file dinamici eseguibili:

```
$ ldd gcc
linux-gate.so.1 =>  (0xb7f33000)
libc.so.6 => /lib/libc.so.6 (0xb7de0000)
/lib/ld-linux.so.2 (0xb7f34000)

```

L'altro strumento è [namcap](/index.php/Namcap_(Italiano) "Namcap (Italiano)"), che non solo controlla le dipendenze ma l'integrità complessiva del pacchetto. Si prega di leggere l'articolo [namcap](/index.php/Namcap_(Italiano) "Namcap (Italiano)") per una descrizione dettagliata.

## Invio di pacchetti di AUR

Si prega di leggere [AUR User Guidelines#SCondividere i PKGBUILD su UNSUPPORTED](https://wiki.archlinux.org/index.php/Arch_User_Repository_%28Italiano%29#Condividere_i_PKGBUILD_su_UNSUPPORTED) per una descrizione dettagliata del processo di invio.

## Per ricapitolare

1.  Scaricare i tarball sorgenti del programma che si vuole impacchettare.
2.  Provare a compilare il pacchetto e installarlo in una directory arbitraria.
3.  Copiare il prototipo `/usr/share/pacman/PKGBUILD.proto` e rinominarlo in `PKGBUILD` in una directory di lavoro temporanea, preferibilmente `~/abs/`.
4.  Modificare il `PKGBUILD` secondo le necessità del proprio pacchetto.
5.  Lanciare `makepkg` e vedere se il pacchetto risultante è complilato correttamente.
6.  In caso contrario, ripetere gli ultimi due passi.

### Avvertenze

*   Prima di poter automatizzare il processo di compilazione di un pacchetto, bisognerebbe averlo fatto manualmente almeno una volta a meno di non conoscere _esattamente_ cosa si sta facendo _a priori_, nel qual caso non si starebbe leggendo questo articolo come primo passo. Sfortunatamente, nonostante un buon gruppo di programmatori si attengano al ciclo di compilazione in tre passi di "`./configure`; `make`; `make install`", questo non accade sempre, e le cose possono diventare davvero pessime se bisogna applicare patch per far funzionare tutto. Regola empirica: se non si riesce a compilare il programma dal tarball sorgente e farlo installare da sè in una sottodirectory temporanea definita, non bisogna neanche provare a impacchettarlo. Non c'è nessuna polvere magica in `makepkg` che risolva i problemi dei sorgenti.
*   In qualche caso, i pacchetti non sono nemmeno disponibili come sorgenti e bisogna usare qualcosa come `sh installer.run` per farli funzionare. Si dovrà fare un po' di lavoro di ricerca (leggere i README, le istruzioni di INSTALL, pagine man, magari ebuild da Gentoo o altri gestori di pacchetti, eventualmente persino i MAKEFILE o il codice sorgente) per metterli a posto. In certi casi, davvero spiacevoli, bisogna modificare i file sorgenti per far funzionare tutto bene. Comunque, `makepkg` deve essere completamente autonomo, senza alcun input da utente. Perciò se si devono modificare i Makefile, si potrebbe dover creare una patch personalizzata con il `PKGBUILD` ed installarla da dentro la funzione `build()`, o si potrebbe dover inserire alcuni comandi `sed` da dentro la stessa funzione.

## Consultare inoltre

*   [How to correctly create a patch file](https://bbs.archlinux.org/viewtopic.php?id=91408).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Creating_packages_(Italiano)&oldid=411562](https://wiki.archlinux.org/index.php?title=Creating_packages_(Italiano)&oldid=411562)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [About Arch (Italiano)](/index.php/Category:About_Arch_(Italiano) "Category:About Arch (Italiano)")
*   [Package development (Italiano)](/index.php/Category:Package_development_(Italiano) "Category:Package development (Italiano)")