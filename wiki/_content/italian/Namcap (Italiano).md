Namcap è uno strumento per controllare pacchetti binari ed codice sorgente di PKGBUILD alla ricerca di errori comuni nella pacchettizzazione; lo si può anche abilitare in modalità automatica. Namcap è stato scritto da [Jason Chu](https://www.archlinux.org/fellows/#jason).

**Cambiamenti**: Il file [NEWS](https://projects.archlinux.org/namcap.git/tree/NEWS) nei repository git contiene le novità introdotte dalla versione precedente.

**Sezione di sviluppo**: [https://projects.archlinux.org/?p=namcap.git;a=summary](https://projects.archlinux.org/?p=namcap.git;a=summary)

Per **segnalare un bug** o **richiedere nuove funzionalità** per namcap, inviare un bug nella sezione _Packages:Extra_ di Arch Linux [bugtracker](https://bugs.archlinux.org) specificandone priorità ed importanza. Quando si segnalano bug è importante fornire esempi concreti dei pacchetti dove si verificano gli errori e non si dimentichi di comunicare il numero di versione.

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

Si può anche consultare il manuale namcap(1) digitando _man namcap_ dalla riga di comando.

## Comprendere il significato dell'output

Namcap usa un sistema di **tags** per classificare gli output. Attualmente, i tags sono di tre tipi, _errors_ (identificati da E), _warnings_ (identificati da W) e _informational_ (identificati da I). Gli errori sono importanti e dovrebbero essere corretti immediatamente; nella maggior parte dei casi sono relativi ad un insufficiente livello di sicurezza, licenze mancanti o problemi di permessi.

Normalmente namcap stampa una spiegazione "umanamente comprensibile" (talvolta con suggerimenti per la risoluzione dei problemi). Se si preferisce un output che possa essere facilmente interpretato da un programma aggiungere la flag -m (_machine-readable_) a namcap (questa funzionalità è attualmente in fase di sviluppo).

## Tags

### Link simbolici

*   **symlink-found** (_informational_) Segnala ogni **link simbolico** presente nel pacchetto.
*   **hardlink-found** (_informational_) Segnala ogni **link reale** presente nel pacchetto.
*   **dangling-symlink** (_error_) Segnala le inesattezze dei link simbolici che si dirigono verso un file che non è presente nel pacchetto.
*   **dangling-hardlink** (_error_) Segnala le inesattezze dei link reali che si dirigono verso un file che non è presente nel pacchetto.

### Dipendenze

*   **link-level-dependence** (_informational_) Fornisce informazioni su una libreria verso la quale un pacchetto punta il link dinamicamente.
*   **dependency-is-testing-release** (_warning_) La dipendenza del pacchetto elencata è nei repository [testing]. I pacchetti vengono compilati per i repository ufficiali di Arch Linux (core, extra e community), mentre **non dovrebbero venir compilati** i pacchetti di [testing]. Per i pacchetti [core] e [extra], la compilazione degli appartenenti a [testing] dovrebbero essere messi nei repository [testing].
*   **dependency-covered-by-link-dependence** (_informational_) Dipendenza coperta da altre dipendenze dal relativo link. Può essere definita una dipendenza ridondante.
*   **dependency-detected-not-included** (_error_) Il file ha una dipendenza non elencata nell'array delle dipendenze. Ignorare l'errore se la dipendenza è elencata nella stringa delle dipendenze opzionali.
*   **dependency-already-satisfied** (_warning_) La dipendenza è già installata (come dipendenza di qualche altro pacchetto, per esempio) e quindi ridondante. Si può usare lo strumento `pactree` da [pacman](https://www.archlinux.org/packages/?name=pacman) per vedere l'albero delle dipendenze del pacchetto.
*   **dependency-not-needed** (_warning_) Questa dipendenza non è richiesta da nessun file presente nel programma (entro i limiti di ciò che namcap può dedurre). Non funziona ancora bene con gli script (come per pacchetti python o perl); in tal caso bisognerà fare il calcolo delle dipendenze da soli.
*   **depends-by-namcap-sight** (_informational_) Una lista di dipendenze d'accordo con lo standard di namcap.

### Licenze

*   **missing-license** (_error_) A questo pacchetto manca una licenza. Le licenze dovrebbero essere messe nella stringa `license=()` del PKGBUILD. Consultare [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards") per ulteriori informazioni. È **molto importante** correggere questo errore il prima possibile, dal momento che non includere una licenza è in molti casi una violazione del copyright.
*   **missing-custom-license-dir** (_error_) La licenza specificata è _custom_ ma non è stata trovata la cartella della licenza in _/usr/share/licenses/_ come specificato nelle linee guida del pacchetto.
*   **missing-custom-license-file** (_error_) La licenza specificata è _custom_ ma non è stato trovato il file con la licenza in _/usr/share/licenses/$pkgname_.
*   **not-a-common-license** (_error_) La licenza specificata **non** è _custom_ e non è presente nel pacchetto [licenses](https://www.archlinux.org/packages/core/any/licenses/) incluso nella distribuzione Arch Linux.

### File

Questa sezione descrive i tag relativi alle autorizzazioni non corrette dei file, o ai file non installati in conformità alle linee guida di FHS.

*   **script-link-detected** (_informational_) Il seguente file è uno script.
*   **file-in-non-standard-dir** (_warning_) Il seguente file è in una directory non standard rispetto a quelle definite dalle [FHS guidelines](http://proton.pathname.com/fhs/pub/fhs-2.3.html). Le directory permesse sono: _bin/_, _etc/_, _usr/bin/_, _usr/sbin/_, _usr/lib_, _usr/include/_, _usr/share/_, _opt/_, _lib/_, _sbin/_, _srv/_, _var/lib/_, _var/opt/_, _var/spool/_, _var/lock/_, _var/state/_, _var/run/_, _var/log/_.
*   **elffile-not-in-allowed-dirs** (_error_) I file ELF dovrebbero stare solo in queste directory: _/lib_, _/bin_, _/sbin_, _/usr/bin_, _/usr/sbin_, _/lib_, _/usr/lib_, _/opt/$pkgname/_.
*   **empty-directory** (_warning_) La seguente directory nel pacchetto è vuota.
*   **non-fhs-man-page** (_error_) Il pacchetto installa le pagine di manuale in un luogo diverso da _/usr/share/man_ che è la directory per le pagine di manuale in base a [FHS guidelines](http://www.pathname.com/fhs/pub/fhs-2.3.html#USRSHAREMANMANUALPAGES).
*   **potential-non-fhs-man-page** (_warning_) Questo file sembra essere una pagina di manuale che non è installato in _/usr/share/man_ anche se namcap non è troppo sicuro a riguardo.
*   **non-fhs-info-page** (_error_) Il pacchetto installa le pagine informative in una posizione diversa da _/usr/share/info_ che è dove devono essere installati i dati indipendenti dall'architettura secondo le [FHS guidelines](http://www.pathname.com/fhs/pub/fhs-2.3.html#USRSHAREARCHITECTUREINDEPENDENTDATA).
*   **potential-non-fhs-info-page** (_warning_) Questo file sembra essere una pagina di informazioni che non è installata in _/usr/share/info_ anche se namcap non è troppo sicuro a riguardo.
*   **incorrect-permissions** (_error_) Questo file ha permessi non corretti. I file in pacchetti binari dovrebbero appartenere a `root/root`.
*   **file-not-world-readable** (_warning_) Il file non è leggibile da tutti; di solito non dovrebbe essere così.
*   **file-world-writable** (_warning_) Chiunque può scrivere su questo file; anche in questo caso, non è la norma.
*   **directory-not-world-executable** (_warning_) La directory non ha impostato il bit eseguibile. Questo non consente l'accesso alla directory per i programmi in esecuzione con privilegi di utente.
*   **incorrect-library-permissions** (_warning_) Il file della libreria non ha il permesso 644 (lettura e scrittura da root, lettura da chiunque altro).
*   **libtool-file-present** (_warning_) Questo file è di tipo libtool (.la) e di norma non dovrebbe essere presente. Si può utilizzare l'opzione `!libtool` nella stringa _opzioni_ del PKGBUILD per rimuovere questi file automaticamente.
*   **perllocal-pod-present** (_error_) I file perllocal.pod non dovrebbero essere presenti in un pacchetto perl; consultare [Perl Package Guidelines](/index.php/Perl_Package_Guidelines "Perl Package Guidelines") per ulteriori informazioni.
*   **scrollkeeper-dir-exists** (_error_) Una directory scrollkeeper è stata trovata nel pacchetto. scrollkeeper non dovrebbe essere eseguito fino al post {install,upgrade,remove}.
*   **info-dir-file-present** (_error_) Il file della directory info /usr/share/info/dir è stato trovato nel pacchetto. Questo file non dovrebbe essere presente.
*   **gnome-mime-file** (_error_) Il file è del tipo autogenerato da GNOME mime e non dovrebbe essere presente nel pacchetto.

### Varie

*   **mime-cache-not-updated** (_error_) Il pacchetto installa i file mime, ma non richiama update-mime-database per aggiornarli.
*   **hicolor-icon-cache-not-updated** (_error_) Ci sono file in /usr/share/icons/hicolor ma la cache delle icone hicolor non è stata aggiornata. Si dovrebbe usare _gtk-update-icon-cache_ (per i pacchetti dipendenti da gtk) o _xdg-icon-resource_ per aggiornare la cache delle icone. Se si utilizza _xdg-icon-resource_ allora si dovrebbe dichiarare una dipendenza da [xdg-utils](https://www.archlinux.org/packages/extra/i686/xdg-utils/).
*   **insecure-rpath** (_error_) Un RPATH (per un eseguibile) è al di fuori di _/usr/lib_. Un RPATH in una posizione non sicura è un potenziale problema di sicurezza. Consultare [FS#14049](https://bugs.archlinux.org/14049).

### PKGBUILDs

Questi sono i tag relativi ai PKGBUILD. Alcuni di questi possono essere applicati anche per i pacchetti binari.

*   **variable-not-array** (_warning_) La variabile dovrebbe essere un array di bash, invece di una stringa. Queste sono le variabili che devono essere scritte come array: _arch_, _license_, _depends_, _makedepends_, _optdepends_, _provides_, _conflicts_, _replaces_, _backup_, _source_, _noextract_, _md5sums_.
*   **backups-preceding-slashes** (_error_) Il file menzionato nell'array di backup inizia con una barra (/).
*   **package-name-in-uppercase** (_error_) Non ci dovrebbe essere nessuna lettera maiuscola nei nomi dei pacchetti.
*   **specific-host-type-used** (_warning_) Invece di utilizzare un host specifico (come i686 o x86_64) utilizzare la variabile generica $CARCH.
*   **extra-var-begins-without-underscore** (_warning_) La variabile non è standard come definito nel manuale PKGBUILD poiché non inizia con un underscore.
*   **file-referred-in-startdir** (_error_) È stato fatto riferimento a un file in _$startdir_, al di fuori di _$startdir/pkg_ e _$startdir/src_.
*   **missing-md5sums** (_error_) Mancano gli MD5sum corrispondenti ai file sorgente. Questi possono essere aggiunti al PKGBUILD con `updpkgsums`.
*   **not-enough-md5sums** (_error_) Ci sono più file sorgente che MD5sum forniti nel PKGBUILD.
*   **too-many-md5sums** (_error_) Ci sono più MD5sum che file sorgente nel PKGBUILD.
*   **improper-md5sum** (_error_) È stato trovato un MD5sum incorretto. Gli MD5sum sono di 32 caratteri di lunghezza.
*   **specific-sourceforge-mirror** (_warning_) PKGBUILD usa un mirror sourceforge specifico. Bisognerebbe usare [http://downloads.sourceforge.net](http://downloads.sourceforge.net).
*   **using-dl-sourceforge** (_warning_) Il dominio deprecato [http://dl.sourceforge.net](http://dl.sourceforge.net) viene usato nell'array sorgente. Dovrebbe essere usato [http://downloads.sourceforge.net](http://downloads.sourceforge.net) al suo posto.
*   **missing-contributor** (_warning_) Manca il tag del fornitore.
*   **missing-maintainer** (_warning_) Manca il tag del maintainer.
*   **missing-url** (_error_) Il pacchetto non dispone di un upstream homepage. Utilizzare la variabile `url`.
*   **pkgname-in-description** (_warning_) La descrizione non dovrebbe contenere il nome del pacchetto.
*   **recommend-use-pkgdir** (_informational_) _$startdir/pkg_ è deprecato, usare _$pkgdir_.
*   **recommend-use-srcdir** (_informational_) _$startdir/src_ è deprecato, usare _$srcdir_.

### Unreleased

Attualmente non ci sono nuovi tag nella versione di sviluppo.

## Creazione di un modulo namcap

Questa sezione documenta namcap internamente e specifica come creare un nuovo modulo namcap.

Il programma principale di namcap, namcap.py, prende come parametri il nome del file di un pacchetto o un PKGBUILD e lo converte in un oggetto pkginfo, che lo passa ad un elenco di regole definite nel `__tarball__` e nel `__pkgbuild__`.

*   ___tarball___ definisce le regole che elaborano pacchetti binari.
*   ___pkgbuild___ definisce le regole che elaborano i PKGBUILDs.

Una volta che il modulo è finalizzato, ricordarsi di aggiungerlo all'array relativo (___tarball___ o ___pkgbuild___) definito in _Namcap/init.py_

Un esempio di modulo namcap è questo (_Namcap/url.py_):

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