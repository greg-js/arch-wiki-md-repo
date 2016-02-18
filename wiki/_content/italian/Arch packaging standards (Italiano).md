## Contents

*   [1 Standard di Pacchettizzazione](#Standard_di_Pacchettizzazione)
    *   [1.1 Prototipo di PKGBUILD](#Prototipo_di_PKGBUILD)
    *   [1.2 Etichetta del pacchetto](#Etichetta_del_pacchetto)
    *   [1.3 Denominazione pacchetto](#Denominazione_pacchetto)
    *   [1.4 Directory](#Directory)
    *   [1.5 Compiti di Makepkg](#Compiti_di_Makepkg)
    *   [1.6 Architetture](#Architetture)
    *   [1.7 Licenses](#Licenses)
    *   [1.8 Invio di pacchetti ad AUR](#Invio_di_pacchetti_ad_AUR)
*   [2 Linee guida supplementari](#Linee_guida_supplementari)
    *   [2.1 CVS/SVN Packages](#CVS.2FSVN_Packages)
    *   [2.2 Eclipse Plugin Packages](#Eclipse_Plugin_Packages)
    *   [2.3 Gnome Packages](#Gnome_Packages)
    *   [2.4 Haskell Packages](#Haskell_Packages)
    *   [2.5 Java Packages](#Java_Packages)
    *   [2.6 Kernel Module Packages](#Kernel_Module_Packages)
    *   [2.7 Lisp Packages](#Lisp_Packages)
    *   [2.8 OCaml Packages](#OCaml_Packages)
    *   [2.9 Perl Packages](#Perl_Packages)
    *   [2.10 Python Packages](#Python_Packages)
    *   [2.11 Ruby Gem Packages](#Ruby_Gem_Packages)
    *   [2.12 Wine Packages](#Wine_Packages)

## Standard di Pacchettizzazione

**I PKGBUILD messi su AUR dagli utenti NON DEVONO riferirsi ad applicazioni già presenti nei repository ufficiali in nessuna circostanza. Eccezione a questa regola sono quei pacchetti compilati con particolari funzionalità abilitate e/o patch applicate differenti da quelle dei pacchetti ufficiali. In questi casi, la voce pkgname deve essere differente, in modo da comunicare chiaramente le differenze dai pacchetti presenti nei repo.**

Nella realizzazione di pacchetti per Arch Linux, si dovrebbe **aderire alle linee guida per la pacchettizzazione** elencate qui sotto, soprattutto se avete intenzione di caricare il vostro PKGBUILD su [AUR](/index.php/AUR "AUR"). Fare riferimento inoltre alle pagine di manuale di [PKGBUILD](https://archlinux.org/pacman/PKGBUILD.5.html) e di [makepkg](https://archlinux.org/pacman/makepkg.8.html).

#### Prototipo di PKGBUILD

```
# Maintainer: Your Name <youremail at domain dot com>

pkgname=NAME
pkgver=VERSION
pkgrel=1
pkgdesc=""
arch=('i686' 'x86_64')
url="http://ADDRESS/"
license=('GPL')
groups=()
depends=()
makedepends=()
optdepends=()
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=
source=($pkgname-$pkgver.tar.gz)
noextract=()
md5sums=() #generate with 'makepkg -g'

build() {
  cd $srcdir/$pkgname-$pkgver
  ./configure --prefix=/usr
  make
}

package() {
  cd $srcdir/$pkgname-$pkgver
  make DESTDIR=$pkgdir install
}

```

Altri prototipi sono reperibili in /usr/share/pacman dai pacchetti di pacman e abs.

#### Etichetta del pacchetto

*   I pacchetti non dovrebbero **mai** essere installati in `/usr/local`
*   **Non introdurre nuove variabili** negli script di compilazione `PKGBUILD`, a meno che il pacchetto non possa essere compilato senza, dato che queste potrebbero generare dei **conflitti** con le variabili utilizzate in makepkg. Se una nuova variabile è assolutamente necessaria, **sottolineare il nome della variabile** (`_`), ad esempio: `_customvariable=` 

    AUR non può rilevare l'uso di variabili personalizzate e quindi non le può utilizzare per le sostituzioni. Lo si può osservare spesso, ad esempio in:

     `http://downloads.sourceforge.net/directxwine/$patchname.$patchver.diff.bz2` 

    Tale situazione contrasta con l'effettiva funzionalità di AUR.

*   **Evitare** l'utilizzo di `/usr/libexec/` per nulla. Usare piuttosto `/usr/lib/${pkgname}/`.
*   Il campo `packager` del file meta pacchetto può essere **personalizzato** dal compilatore del pacchetto modificando l'apposita opzione nel file `/etc/makepkg.conf`, o in alternativa sovrascriverlo creando ~/.makepkg.conf
*   Tutti i messaggi importanti dovrebbero essere visualizzati (con echo) durante l'installazione utilizzando un file **.install**. Ad esempio, se un pacchetto ha bisogno di impostazioni extra per poter funzionare, tali indicazioni dovrebbero essere incluse.
*   Qualsiasi **dipendenza opzionale** non richiesta necessariamente per eseguire il pacchetto o con funzioni generali non dovrebbe essere inclusa; l'informazione dovrebbe invece essere aggiunta all'array **optdepends**:
    ```
    optdepends=('cups: printing support'
                'sane: scanners support'
                'libgphoto2: digital cameras support'
                'alsa-lib: sound support'
                'giflib: GIF images support'
                'libjpeg: JPEG images support'
                'libpng: PNG images support')

    ```

    L'esempio precedente è stato preso dal pacchetto **wine** in <tt>extra</tt>. Le informazioni "optdepends" vengono automaticamente stampate durante l'installazione/aggiornamento perciò **non** si dovrebbe mettere questo tipo di informazioni nei file .install.

*   Quando si crea una **descrizione del pacchetto**, non includere il nome del pacchetto in modo autoreferenziale. Per esempio, "Nedit è un editor di testo per X11" potrebbe essere semplificato con "Un editor di testo per X11". Tentare anche di mantenere le descrizioni a ~80 caratteri o meno.
*   Tentare di mantenere inoltre la **lunghezza della riga** nel PKGBUILD al di sotto dei 100 caratteri.
*   Laddove possibile, **rimuovere le righe vuote** dal `PKGBUILD` (`provides`, `replaces`, ecc.)
*   È pratica comune **preservare l'ordine** dei campi `PKGBUILD` come indicato sopra. Tuttavia, questo non è obbligatorio, in quanto l'unico requisito in questo contesto è la **corretta sintassi bash**.

#### Denominazione pacchetto

*   I nomi del pacchetto devono essere composti solo da **caratteri alfanumerici**; tutte le lettere devono essere **minuscole**.
*   Le versioni del pacchetto **dovrebbero essere la stessa della versione rilasciata dall'autore**. Le versioni possono comprendere lettere, se necessario (ad esempio, la versione nmap è 2.54BETA32). **I tag della versione non dovrebbero includere trattini!**, ma solo lettere, numeri e punti.
*   Le release dei pacchetti sono **specifiche per i pacchetti Arch Linux**. Queste permettono agli utenti di distinguere le build del pacchetto nuove dalle vecchie. Quando viene rilasciata una nuova versione del pacchetto, il **conto della release parte da 1**. Poi, quando vengono eseguite correzioni ed ottimizzazioni, il pacchetto viene **rilasciato** nuovamente all'utenza di Arch Linux ed il **numero di release verrà incrementato**. Quando esce una nuova versione, il conteggio del rilascio viene azzerato a 1\. Il tag del rilascio dei pacchetti segue le **stesse limitazioni di nominazione che i tag di versione**.

#### Directory

*   **I file di configurazione** dovrebbero essere messi nella directory `/etc`. Se c'è più di un file di configurazione, è consuetudine **utilizzare una sottodirectory** in modo da mantenere `/etc` il più pulita possibile. Utilizzare `/etc/{pkgname}/`, dove `{pkgname}` è il nome del pacchetto (oppure un'alternativa valida, per esempio apache usa `/etc/httpd/`).
*   I pacchetti dovrebbero seguire queste **linee guida delle directory generali**:

| `/etc` | 

**File essenziali** di configurazione del sistema

 |
| `/usr/bin` | Applicazioni binarie |
| `/usr/sbin` | Binari di sistema |
| `/usr/lib` | Librerie |
| `/usr/include` | Header file |
| `/usr/lib/{pkg}` | Moduli, plugin, ecc. |
| `/usr/share/doc/{pkg}` | Documentazione delle applicazioni |
| `/usr/share/info` | Informazioni file di sistema |
| `/usr/share/man` | Pagine di manuale |
| `/usr/share/{pkg}` | Dati delle applicazioni |
| `/var/lib/{pkg}` | Memorizzazione applicazioni persistenti |
| `/etc/{pkg}` | File di configurazione per `{pkg}` |
| `/opt/{pkg}` | 

Pacchetti autonomi grandi, come Java, ecc.

 |

*   Il pacchetto non dovrebbe contenere le seguenti directory:
    *   /dev
    *   /home
    *   /srv
    *   /media
    *   /mnt
    *   /proc
    *   /root
    *   /selinux
    *   /sys
    *   /tmp
    *   /var/tmp

#### Compiti di [Makepkg](/index.php/Makepkg "Makepkg")

Quando si utilizza makepkg per la compilazione di un pacchetto, quello che fa automaticamente è:

1.  Verificare che i pacchetti **dependencies** e **makedepends** siano installati
2.  **Scaricare i sorgenti** dai server
3.  **Verificare l'integrità** dei file sorgente
4.  **Decomprimere** i file sorgente
5.  Eseguire tutte le operazioni necessarie di **patching**
6.  **Compilare** il software e lo installa in una directory fake root
7.  **Rimuovere** i simboli dai binari
8.  **Rimuovere** i simboli di debug dalle librerie
9.  **Comprimere** i manuali e/o le pagine info
10.  Generare il **file meta pacchetto** che è incluso in ogni pacchetto
11.  **Comprimere** la fake root nel pacchetto
12.  **Memorizzare** i file del pacchetto nella directory di destinazione configurata (cwd è quella di default)

#### Architetture

L'array <tt>arch</tt> dovrebbe contenere <tt>"i686"</tt> e/o <tt>"x86_64"</tt> a seconda di qual è l'architettura di destinazione. È inoltre possibile utilizzare <tt>"any"</tt> per i pacchetti idonei ad entrambi i tipi di architettura.

#### [Licenses](/index.php/Licenses "Licenses")

L'array della licenza è in corso di implementazione nei repo ufficiali, e **dovrebbe** essere utilizzato pure nei propri pacchetti. Specificare come segue:

*   Un pacchetto licenze è stato creato in [core] e contiene licenze comuni in /usr/share/licenses/common, ad esempio /usr/share/licenses/common/GPL. Se un pacchetto è rilasciato sotto una di queste licenze, la variabile licenze dovrà essere impostata con il nome della directory, ad esempio license=("GPL")
*   Se la licenza appropriata non è inclusa nel pacchetto licenze ufficiali, si dovranno fare diverse altre cose:
    1.  I file delle licenze dovrebbero essere inclusi in /usr/share/licenses/$pkgname/, ad esempio /usr/share/licenses/dibfoo/LICENSE. Un buon modo per farlo è tramite: `install -D -m644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"` 
    2.  Se l'archivio dei sorgenti non contiene i dettagli della licenza, ma la si può ad esempio visualizzare su un sito web, copiarla in un file e inserirla. Ricordarsi anche di nominarla in modo appropriato.
    3.  Aggiungere "custom" all'array licenze. Opzionalmente, è possibile sostituire "custom" con custom:"name of license".
*   Una volta che viene utilizzata una licenza in due o più pacchetti in un repo ufficiale, incluso [community], diviene "common"
*   Le licenze MIT, BSD, zlib/libpng e Python sono casi particolari e non possono essere incluse nel pacchetto "common license". A causa della variabile della licenza, è trattata come una licenza comune (license=('BSD'), license=('MIT'), license=('ZLIB') or license=('Python')) ma per il bene del filesystem, è una licenza personalizzata, perché ognuno ha una propria linea di diritto d'autore. Ogni pacchetto licenze MIT, BSD, zlib/libpng o Python dovrebbe avere la propria licenza unica conservata in /usr/share/licenses/$pkgname/.
*   Alcuni pacchetti non possono essere oggetto di una singola licenza. In questi casi possono essere immesse più voci nell'array licenza, per esempio license=("GPL" "custom:some commercial license"). Per la maggior parte dei pacchetti queste licenze si applicano in diversi casi, invece di applicarle allo stesso tempo. Una volta che a pacman sarà aggiuntà la possibilità di filtrare i risultati in base alle licenze (in modo da poter scegliere ad esempio: "voglio solo software rilasciato sotto licenze BSD e GPL"), software rilasciati sotto licenze duplici (o multiple) saranno trattati da pacman con logica OR piuttosto che AND, in modo che pacman prenda in considerazione nell'esempio succitato tutti i software rilasciati almeno sotto una delle due licenze GPL e BSD, tralasciando tutti gli altri.
*   La (L)GPL ha molte versioni e permutazioni di tali versioni. Per il software (L)GPL, la convenzione è:
    *   (L)GPL - (L)GPLv2 od ogni versione successiva
    *   (L)GPL2 - (L)GPL2 solo
    *   (L)GPL3 - (L)GPL3 od ogni versione successiva

#### Invio di pacchetti ad AUR

Si osservino le seguenti specifiche prima di inviare qualsiasi pacchetto ad AUR:

1.  I PKGBUILD inviati **NON** devono assolutamente essere già presenti in nessuno dei repository binari ufficiali. L'unica eccezione a questa rigorosa regola può essere solo quella di pacchetti con caratteristiche o funzionalità extra, e/o con eventuali patch che li contraddistinguono da quelli ufficiali. In tali occasioni l'array pkgname dovrebbe essere diverso per specificare queste differenze. Esempio: Un PKGBUILD con uno schermo GNU inviato con la patch sidebar, potrebbe essere chiamato screen-sidebar ecc. Inoltre, l'array del PKGBUILD **provides=('screen')** dovrebbe essere utilizzato al fine di evitare conflitti con il pacchetto ufficiale.
2.  Per garantire la sicurezza dei pacchetti inviati ad AUR si prega di **verificare** di aver compilato correttamente il campo `md5sum`. L'`md5sum` può essere generato utilizzando il comando `makepkg -g`.
3.  Si prega di **aggiungere una riga di commento** nella parte superiore del file `PKGBUILD` che segue questo formato. Ricordarsi di mascherare il proprio indirizzo e-mail per evitare lo spam: `# Maintainer: Your Name <address at domain dot com>` 

    Se si sta assumendo il ruolo di manutentore di un PKGBUILD esistente, aggiungere il proprio nome in cima come descritto sopra e cambiare il titolo del precedente Maintainer a Contributor:

    ```
    # Maintainer: Your Name <address at domain dot com>
    # Contributor: Previous Name <address at domain dot com>
    ```

4.  Verificare le **dipendenze** del pacchetto (ad esempio, eseguire `ldd` su eseguibili dinamici, controllare i tool richiesti dagli script, ecc). I TU raccomandano **vivamente** l'utilizzo dell'utilità `namcap`, elaborato da [Jason Chu](https://www.archlinux.org/fellows/#jason), per analizzare lo stato dei pacchetti. `Namcap` avviserà riguardo permessi errati, dipendenze mancanti, dipendenze non richieste, ed altri errori comuni. Si può installare il pacchetto `namcap` con `pacman`. Ricordare inoltre che `namcap` può essere usato per controllare sia file pkg.tar.gz che PKGBUILD.
5.  Le **dipendenze** sono tra gli errori più comuni riguardo la pacchettizzazione. Namcap può aiutare a rilevarle, ma non è sempre infallibile. Verificare le dipendenze consultando la documentazione dei sorgenti e il sito web del programma.
6.  **Non utilizzare <tt>replaces</tt>** in un PKGBUILD a meno che il pacchetto debba essere rinominato, per esempio quando *Ethereal* diventa *Wireshark*. Se il pacchetto è una versione alternativa di un pacchetto già esistente, usare <tt>conflicts</tt> (e <tt>provides</tt> se tale pacchetto è richiesto da altri). La differenza principale è che dopo la sincronizzazione (-Sy), pacman vuole subito sostituire il pacchetto installato, per trovare un pacchetto con il "matching" <tt>replaces</tt> da qualche parte nei suoi repository; <tt>conflicts</tt> d'altra parte viene considerato solo quando ha effettivamente luogo l'installazione del pacchetto, che di solito è il comportamento desiderato, dato che è meno invasivo.
7.  Tutti i file caricati su AUR devono essere contenuti in un **file tar compresso** contenente una directory con il **`PKGBUILD`** e i **file di compilazione aggiuntivi** (patch, install, ...).
    ```
    foo/PKGBUILD
    foo/foo.install
    foo/foo_bar.diff
    foo/foo.rc.conf
    ```

    Il nome dell'archivio dovrebbe contenere il nome del pacchetto, ad esempio foo.tar.gz.

    Si può facilmente compilare un archivio contenente tutti i file richiesti utilizzando <tt>makepkg --source</tt>. Questo rinominerà un tarball <tt>$pkgname-$pkgver-$pkgrel.src.tar.gz</tt>, che può essere poi caricato su AUR.

    Il tarball **non dovrebbe** contenere nè il tarball binario creato da makepkg, né la filelist.

## Linee guida supplementari

Si raccomanda di leggere per prima cosa le linee guida descritte sopra: molti concetti importanti sono spiegati in questa pagina e non verranno ripetuti nelle seguenti guide specifiche, che sono intese come un complemento agli standard elencati in questa pagina.

#### CVS/SVN Packages

Si prega di consultare [Arch CVS & SVN PKGBUILD guidelines](/index.php/Arch_CVS_%26_SVN_PKGBUILD_guidelines "Arch CVS & SVN PKGBUILD guidelines")

#### Eclipse Plugin Packages

Si prega di consultare [Eclipse plugin package guidelines](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines")

#### Gnome Packages

Si prega di consultare [Gnome package guidelines](/index.php/Gnome_package_guidelines "Gnome package guidelines")

#### Haskell Packages

Si prega di consultare [Haskell package guidelines](/index.php/Haskell_package_guidelines "Haskell package guidelines")

#### Java Packages

Si prega di consultare [Java Package Guidelines](/index.php/Java_Package_Guidelines "Java Package Guidelines")

#### Kernel Module Packages

Si prega di consultare [Kernel Module Package Guidelines](/index.php/Kernel_Module_Package_Guidelines "Kernel Module Package Guidelines")

#### Lisp Packages

Si prega di consultare [Lisp Package Guidelines](/index.php/Lisp_Package_Guidelines "Lisp Package Guidelines")

#### OCaml Packages

Si prega di consultare [OCaml_Package_Guidelines](/index.php/OCaml_Package_Guidelines "OCaml Package Guidelines")

#### Perl Packages

Si prega di consultare [Perl Package Guidelines](/index.php/Perl_Package_Guidelines "Perl Package Guidelines")

#### Python Packages

Si prega di consultare [Python Package Guidelines](/index.php/Python_Package_Guidelines "Python Package Guidelines")

#### Ruby Gem Packages

Si prega di consultare [Ruby Gem Package Guidelines](/index.php/Ruby_Gem_Package_Guidelines "Ruby Gem Package Guidelines")

#### Wine Packages

Si prega di consultare [Arch wine PKGBUILD guidelines](/index.php/Arch_wine_PKGBUILD_guidelines "Arch wine PKGBUILD guidelines")