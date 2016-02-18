Namcap è uno strumento per controllare pacchetti binari ed codice sorgente di PKGBUILD alla ricerca di errori comuni nella pacchettizzazione; lo si può anche abilitare in modalità automatica. Namcap è stato scritto da [Jason Chu](https://www.archlinux.org/fellows/#jason).

**Cambiamenti**: Il file [NEWS](https://projects.archlinux.org/namcap.git/tree/NEWS) nei repository git contiene le novità introdotte dalla versione precedente.

**Sezione di sviluppo**: [https://projects.archlinux.org/?p=namcap.git;a=summary](https://projects.archlinux.org/?p=namcap.git;a=summary)

Per **segnalare un bug** o **richiedere nuove funzionalità** per namcap, inviare un bug nella sezione *Packages:Extra* di Arch Linux [bugtracker](https://bugs.archlinux.org) specificandone priorità ed importanza. Quando si segnalano bug è importante fornire esempi concreti dei pacchetti dove si verificano gli errori e non si dimentichi di comunicare il numero di versione.

Se si possono fornire delle patch (per correzione di bug o per nuovi moduli namcap), è possibile inviarle alla mailing list [arch-projects](mailto:arch-projects@archlinux.org). Lo sviluppo di Namcap viene gestito con git, quindi sono preferibili le patch in formato git.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Come usarlo](#Come_usarlo)
*   [3 Comprendere il significato dell'output](#Comprendere_il_significato_dell.27output)
*   [4 Tags](#Tags)
    *   [4.1 Link simbolici](#Link_simbolici)
    *   [4.2 Dipendenze](#Dipendenze)
    *   [4.3 Licenze](#Licenze)
    *   [4.4 File](#File)
    *   [4.5 Varie](#Varie)
    *   [4.6 PKGBUILDs](#PKGBUILDs)
    *   [4.7 Unreleased](#Unreleased)
*   [5 Creazione di un modulo namcap](#Creazione_di_un_modulo_namcap)
*   [6 Namcap reports](#Namcap_reports)

## Installazione

[Installare](/index.php/Pacman "Pacman") il pacchetto [namcap](https://www.archlinux.org/packages/?name=namcap) dagli [official repositories](/index.php/Official_repositories "Official repositories").

## Come usarlo

Per lanciare namcap su un PKGBUILD o su un pacchetto binario pkg.tar.xz:

```
$ namcap FILENAME

```

Per visualizzare messaggi con ulteriori informazioni, invocare namcap con la flag `-i`:

```
$ namcap -i FILENAME

```

Si può anche consultare il manuale namcap(1) digitando *man namcap* dalla riga di comando.

## Comprendere il significato dell'output

Namcap usa un sistema di **tags** per classificare gli output. Attualmente, i tags sono di tre tipi, *errors* (identificati da E), *warnings* (identificati da W) e *informational* (identificati da I). Gli errori sono importanti e dovrebbero essere corretti immediatamente; nella maggior parte dei casi sono relativi ad un insufficiente livello di sicurezza, licenze mancanti o problemi di permessi.

Normalmente namcap stampa una spiegazione "umanamente comprensibile" (talvolta con suggerimenti per la risoluzione dei problemi). Se si preferisce un output che possa essere facilmente interpretato da un programma aggiungere la flag -m (*machine-readable*) a namcap (questa funzionalità è attualmente in fase di sviluppo).

## Tags

### Link simbolici

*   **symlink-found** (*informational*) Segnala ogni **link simbolico** presente nel pacchetto.
*   **hardlink-found** (*informational*) Segnala ogni **link reale** presente nel pacchetto.
*   **dangling-symlink** (*error*) Segnala le inesattezze dei link simbolici che si dirigono verso un file che non è presente nel pacchetto.
*   **dangling-hardlink** (*error*) Segnala le inesattezze dei link reali che si dirigono verso un file che non è presente nel pacchetto.

### Dipendenze

*   **link-level-dependence** (*informational*) Fornisce informazioni su una libreria verso la quale un pacchetto punta il link dinamicamente.
*   **dependency-is-testing-release** (*warning*) La dipendenza del pacchetto elencata è nei repository [testing]. I pacchetti vengono compilati per i repository ufficiali di Arch Linux (core, extra e community), mentre **non dovrebbero venir compilati** i pacchetti di [testing]. Per i pacchetti [core] e [extra], la compilazione degli appartenenti a [testing] dovrebbero essere messi nei repository [testing].
*   **dependency-covered-by-link-dependence** (*informational*) Dipendenza coperta da altre dipendenze dal relativo link. Può essere definita una dipendenza ridondante.
*   **dependency-detected-not-included** (*error*) Il file ha una dipendenza non elencata nell'array delle dipendenze. Ignorare l'errore se la dipendenza è elencata nella stringa delle dipendenze opzionali.
*   **dependency-already-satisfied** (*warning*) La dipendenza è già installata (come dipendenza di qualche altro pacchetto, per esempio) e quindi ridondante. Si può usare lo strumento `pactree` da [pacman](https://www.archlinux.org/packages/?name=pacman) per vedere l'albero delle dipendenze del pacchetto.
*   **dependency-not-needed** (*warning*) Questa dipendenza non è richiesta da nessun file presente nel programma (entro i limiti di ciò che namcap può dedurre). Non funziona ancora bene con gli script (come per pacchetti python o perl); in tal caso bisognerà fare il calcolo delle dipendenze da soli.
*   **depends-by-namcap-sight** (*informational*) Una lista di dipendenze d'accordo con lo standard di namcap.

### Licenze

*   **missing-license** (*error*) A questo pacchetto manca una licenza. Le licenze dovrebbero essere messe nella stringa `license=()` del PKGBUILD. Consultare [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards") per ulteriori informazioni. È **molto importante** correggere questo errore il prima possibile, dal momento che non includere una licenza è in molti casi una violazione del copyright.
*   **missing-custom-license-dir** (*error*) La licenza specificata è *custom* ma non è stata trovata la cartella della licenza in */usr/share/licenses/* come specificato nelle linee guida del pacchetto.
*   **missing-custom-license-file** (*error*) La licenza specificata è *custom* ma non è stato trovato il file con la licenza in */usr/share/licenses/$pkgname*.
*   **not-a-common-license** (*error*) La licenza specificata **non** è *custom* e non è presente nel pacchetto [licenses](https://www.archlinux.org/packages/core/any/licenses/) incluso nella distribuzione Arch Linux.

### File

Questa sezione descrive i tag relativi alle autorizzazioni non corrette dei file, o ai file non installati in conformità alle linee guida di FHS.

*   **script-link-detected** (*informational*) Il seguente file è uno script.
*   **file-in-non-standard-dir** (*warning*) Il seguente file è in una directory non standard rispetto a quelle definite dalle [FHS guidelines](http://proton.pathname.com/fhs/pub/fhs-2.3.html). Le directory permesse sono: *bin/*, *etc/*, *usr/bin/*, *usr/sbin/*, *usr/lib*, *usr/include/*, *usr/share/*, *opt/*, *lib/*, *sbin/*, *srv/*, *var/lib/*, *var/opt/*, *var/spool/*, *var/lock/*, *var/state/*, *var/run/*, *var/log/*.
*   **elffile-not-in-allowed-dirs** (*error*) I file ELF dovrebbero stare solo in queste directory: */lib*, */bin*, */sbin*, */usr/bin*, */usr/sbin*, */lib*, */usr/lib*, */opt/$pkgname/*.
*   **empty-directory** (*warning*) La seguente directory nel pacchetto è vuota.
*   **non-fhs-man-page** (*error*) Il pacchetto installa le pagine di manuale in un luogo diverso da */usr/share/man* che è la directory per le pagine di manuale in base a [FHS guidelines](http://www.pathname.com/fhs/pub/fhs-2.3.html#USRSHAREMANMANUALPAGES).
*   **potential-non-fhs-man-page** (*warning*) Questo file sembra essere una pagina di manuale che non è installato in */usr/share/man* anche se namcap non è troppo sicuro a riguardo.
*   **non-fhs-info-page** (*error*) Il pacchetto installa le pagine informative in una posizione diversa da */usr/share/info* che è dove devono essere installati i dati indipendenti dall'architettura secondo le [FHS guidelines](http://www.pathname.com/fhs/pub/fhs-2.3.html#USRSHAREARCHITECTUREINDEPENDENTDATA).
*   **potential-non-fhs-info-page** (*warning*) Questo file sembra essere una pagina di informazioni che non è installata in */usr/share/info* anche se namcap non è troppo sicuro a riguardo.
*   **incorrect-permissions** (*error*) Questo file ha permessi non corretti. I file in pacchetti binari dovrebbero appartenere a `root/root`.
*   **file-not-world-readable** (*warning*) Il file non è leggibile da tutti; di solito non dovrebbe essere così.
*   **file-world-writable** (*warning*) Chiunque può scrivere su questo file; anche in questo caso, non è la norma.
*   **directory-not-world-executable** (*warning*) La directory non ha impostato il bit eseguibile. Questo non consente l'accesso alla directory per i programmi in esecuzione con privilegi di utente.
*   **incorrect-library-permissions** (*warning*) Il file della libreria non ha il permesso 644 (lettura e scrittura da root, lettura da chiunque altro).
*   **libtool-file-present** (*warning*) Questo file è di tipo libtool (.la) e di norma non dovrebbe essere presente. Si può utilizzare l'opzione `!libtool` nella stringa *opzioni* del PKGBUILD per rimuovere questi file automaticamente.
*   **perllocal-pod-present** (*error*) I file perllocal.pod non dovrebbero essere presenti in un pacchetto perl; consultare [Perl Package Guidelines](/index.php/Perl_Package_Guidelines "Perl Package Guidelines") per ulteriori informazioni.
*   **scrollkeeper-dir-exists** (*error*) Una directory scrollkeeper è stata trovata nel pacchetto. scrollkeeper non dovrebbe essere eseguito fino al post {install,upgrade,remove}.
*   **info-dir-file-present** (*error*) Il file della directory info /usr/share/info/dir è stato trovato nel pacchetto. Questo file non dovrebbe essere presente.
*   **gnome-mime-file** (*error*) Il file è del tipo autogenerato da GNOME mime e non dovrebbe essere presente nel pacchetto.

### Varie

*   **mime-cache-not-updated** (*error*) Il pacchetto installa i file mime, ma non richiama update-mime-database per aggiornarli.
*   **hicolor-icon-cache-not-updated** (*error*) Ci sono file in /usr/share/icons/hicolor ma la cache delle icone hicolor non è stata aggiornata. Si dovrebbe usare *gtk-update-icon-cache* (per i pacchetti dipendenti da gtk) o *xdg-icon-resource* per aggiornare la cache delle icone. Se si utilizza *xdg-icon-resource* allora si dovrebbe dichiarare una dipendenza da [xdg-utils](https://www.archlinux.org/packages/extra/i686/xdg-utils/).
*   **insecure-rpath** (*error*) Un RPATH (per un eseguibile) è al di fuori di */usr/lib*. Un RPATH in una posizione non sicura è un potenziale problema di sicurezza. Consultare [FS#14049](https://bugs.archlinux.org/14049).

### PKGBUILDs

Questi sono i tag relativi ai PKGBUILD. Alcuni di questi possono essere applicati anche per i pacchetti binari.

*   **variable-not-array** (*warning*) La variabile dovrebbe essere un array di bash, invece di una stringa. Queste sono le variabili che devono essere scritte come array: *arch*, *license*, *depends*, *makedepends*, *optdepends*, *provides*, *conflicts*, *replaces*, *backup*, *source*, *noextract*, *md5sums*.
*   **backups-preceding-slashes** (*error*) Il file menzionato nell'array di backup inizia con una barra (/).
*   **package-name-in-uppercase** (*error*) Non ci dovrebbe essere nessuna lettera maiuscola nei nomi dei pacchetti.
*   **specific-host-type-used** (*warning*) Invece di utilizzare un host specifico (come i686 o x86_64) utilizzare la variabile generica $CARCH.
*   **extra-var-begins-without-underscore** (*warning*) La variabile non è standard come definito nel manuale PKGBUILD poiché non inizia con un underscore.
*   **file-referred-in-startdir** (*error*) È stato fatto riferimento a un file in *$startdir*, al di fuori di *$startdir/pkg* e *$startdir/src*.
*   **missing-md5sums** (*error*) Mancano gli MD5sum corrispondenti ai file sorgente. Questi possono essere aggiunti al PKGBUILD con `updpkgsums`.
*   **not-enough-md5sums** (*error*) Ci sono più file sorgente che MD5sum forniti nel PKGBUILD.
*   **too-many-md5sums** (*error*) Ci sono più MD5sum che file sorgente nel PKGBUILD.
*   **improper-md5sum** (*error*) È stato trovato un MD5sum incorretto. Gli MD5sum sono di 32 caratteri di lunghezza.
*   **specific-sourceforge-mirror** (*warning*) PKGBUILD usa un mirror sourceforge specifico. Bisognerebbe usare [http://downloads.sourceforge.net](http://downloads.sourceforge.net).
*   **using-dl-sourceforge** (*warning*) Il dominio deprecato [http://dl.sourceforge.net](http://dl.sourceforge.net) viene usato nell'array sorgente. Dovrebbe essere usato [http://downloads.sourceforge.net](http://downloads.sourceforge.net) al suo posto.
*   **missing-contributor** (*warning*) Manca il tag del fornitore.
*   **missing-maintainer** (*warning*) Manca il tag del maintainer.
*   **missing-url** (*error*) Il pacchetto non dispone di un upstream homepage. Utilizzare la variabile `url`.
*   **pkgname-in-description** (*warning*) La descrizione non dovrebbe contenere il nome del pacchetto.
*   **recommend-use-pkgdir** (*informational*) *$startdir/pkg* è deprecato, usare *$pkgdir*.
*   **recommend-use-srcdir** (*informational*) *$startdir/src* è deprecato, usare *$srcdir*.

### Unreleased

Attualmente non ci sono nuovi tag nella versione di sviluppo.

## Creazione di un modulo namcap

Questa sezione documenta namcap internamente e specifica come creare un nuovo modulo namcap.

Il programma principale di namcap, namcap.py, prende come parametri il nome del file di un pacchetto o un PKGBUILD e lo converte in un oggetto pkginfo, che lo passa ad un elenco di regole definite nel `__tarball__` e nel `__pkgbuild__`.

*   *__tarball__* definisce le regole che elaborano pacchetti binari.
*   *__pkgbuild__* definisce le regole che elaborano i PKGBUILDs.

Una volta che il modulo è finalizzato, ricordarsi di aggiungerlo all'array relativo (*__tarball__* o *__pkgbuild__*) definito in *Namcap/init.py*

Un esempio di modulo namcap è questo (*Namcap/url.py*):

import pacman

```
 class package:
 	def short_name(self):

```

return "url" def long_name(self): return "Verifies url is included in a PKGBUILD" def prereq(self): return "" def analyze(self, pkginfo, tar): ret = [[],[],[]] if not hasattr(pkginfo, 'url'): ret[0].append(("missing-url", ())) return ret def type(self): return "pkgbuild"

Fondamentalmente, il codice si spiega da sé. Di seguito viene riportato l'elenco dei metodi che ogni modulo namcap deve avere:

*   **short_name**(self) Restituisce una stringa contenente un nome breve del modulo. Di solito, questo equivale al nome di base del file modulo.
*   **long_name**(self) Restituisce una stringa contenente una descrizione sintetica del modulo. Tale descrizione è utilizzata quando si elencano tutte le regole con `namcap -r list`.
*   **prereq**(self) Restituisce una stringa contenente i prerequisiti necessari al modulo per funzionare correttamente. Solitamente "" per moduli di elaborazione PKGBUILD e "tar" per moduli di elaborazione di file pacchetto. "extract" deve essere specificato se il contenuto del pacchetto deve essere estratto in una directory temporanea prima di procedere.
*   **analyze**(self, pkginfo, tar) Dovrebbe restituire un elenco che comprende, a sua volta tre elenchi: errore di tag, etichette di avvertimento e di informazione. Ogni membro di questi elenchi tag deve essere una tupla composta da due componenti: **la forma breve con trattini** del tag con gli appropriati specificatori di formato (%s, etc.) La prima parola di questa stringa deve essere il nome del tag. La forma "umanamente" leggibile del tag deve essere messa nel file tags. Il formato del file tags è descritta di seguito; i **parametri** che dovrebbero sostituire il formato specifico rimangono nell'output finale.

*   **type**(self) "pkgbuild" per un modulo di elaborazione dei PKGBUILDs, "tarball" per un modulo di elaborazione di un pacchetto binario.

Il file dei tag è costituito da righe che riportano la forma "umanamente" leggibile dei tag a fianco della forma scritta coi trattini del codice namcap. Una riga che inizia con un '#' viene considerata commentata. In caso contrario, il formato del file è:

```
 machine-parseable-tag %s :: This is machine parseable tag %s

```

Si noti che un "doppio due punti" (::) è utilizzato per separare i tag scritti con trattini dalla descrizione leggibile.

## Namcap reports

**namcap-reports** è un report generato automaticamente ed ottenuto dopo l'esecuzione di namcap rispetto a core, extra e community.

Come funziona:

*   namcap viene eseguito rispetto all'intero albero [ABS](/index.php/ABS "ABS") per generare `namcap.log`.
*   I pacchetti in core, extra e community vengono messi in file chiamati core, extra e community (usando `pacman -Slq`).
*   `namcap-report.py` prende il codice e prepara il report e i feed RSS, per essere poi copiato nel server web.