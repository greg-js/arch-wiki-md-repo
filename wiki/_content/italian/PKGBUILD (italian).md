Un `PKGBUILD` è un file di descrizione della costruzione di pacchetti di Arch Linux (è in effetti uno script da shell), usato durante la [creazione dei pacchetti](/index.php/Creating_packages_(Italiano) "Creating packages (Italiano)"). Questo articolo descrive le possibili variabili del `PKGBUILD`.

I pacchetti in Arch Linux sono costruiti utilizzando il comando [makepkg](/index.php/Makepkg "Makepkg") e le informazioni sono memorizzate in un file `PKGBUILD`. Quando `makepkg` viene eseguito, cerca un `PKGBUILD` nella directory corrente e segue le istruzioni ivi contenute sia per compilare che per acquisire i file necessari al confezionamento di un pacchetto (`pkgname.pkg.tar.xz`). Il pacchetto risultante contiene i file binari e le istruzioni di installazione e può essere facilmente installato tramite [pacman](/index.php/Pacman "Pacman").

## Contents

*   [1 Variabili](#Variabili)
    *   [1.1 pkgname](#pkgname)
    *   [1.2 pkgver](#pkgver)
    *   [1.3 pkgrel](#pkgrel)
    *   [1.4 pkgdir](#pkgdir)
    *   [1.5 epoch](#epoch)
    *   [1.6 pkgbase](#pkgbase)
    *   [1.7 pkgdesc](#pkgdesc)
    *   [1.8 arch](#arch)
    *   [1.9 url](#url)
    *   [1.10 license](#license)
    *   [1.11 groups](#groups)
    *   [1.12 depends](#depends)
    *   [1.13 optdepends](#optdepends)
    *   [1.14 makedepends](#makedepends)
    *   [1.15 checkdepends](#checkdepends)
    *   [1.16 provides](#provides)
    *   [1.17 conflicts](#conflicts)
    *   [1.18 replaces](#replaces)
    *   [1.19 backup](#backup)
    *   [1.20 options](#options)
    *   [1.21 install](#install)
    *   [1.22 changelog](#changelog)
    *   [1.23 source](#source)
    *   [1.24 noextract](#noextract)
    *   [1.25 md5sums](#md5sums)
    *   [1.26 sha1sums](#sha1sums)
    *   [1.27 sha256sums, sha384sums, sha512sums](#sha256sums.2C_sha384sums.2C_sha512sums)
*   [2 Consultare anche](#Consultare_anche)

## Variabili

Le seguenti variabili possono essere utilizzate nel file `PKGBUILD`:

È pratica comune inserire nel `PKGBUILD` le variabili nello stesso ordine nel quale sono indicate in questa pagina, anche se ciò non è obbligatorio finchè viene rispettata la sintassi di Bash.

### pkgname

Il nome del pacchetto. Dovrebbe consistere nei soli **caratteri alfanumerici e seguenti simboli @ . _ + - (chiocciola, punto, trattino basso, segno più, trattino)**. Tutte le lettere dovrebbero essere in **minuscolo** e non è consentito che i nomi inizino con un trattino. Per motivi di coerenza, il `pkgname` dovrebbe corrispondere al nome dell'archivio dei sorgenti del software che si sta impacchettando. Per esempio, se il software è in `foobar-2.5.tar.gz`, il valore di `pkgname` dovrebbe essere *foobar*. Anche la directory di lavoro in cui risiede il file `PKGBUILD` dovrebbe corrispondere al `pkgname`.

### pkgver

La versione del pacchetto. Il valore dovrebbe essere lo stesso della versione rilasciata dell'autore del pacchetto. Può contenere lettere, numeri, punti e trattini bassi, ma **NON** può contenere trattini. Se l'autore del pacchetto usa i trattini nello schema di numerazione della versione, si deve sostituirli con degli underscore. Per esempio, se la versione è *0.99-10*, dovrebbe essere cambiata in *0.99_10*. Se la variabile pkgver viene usata successivamente nel PKGBUILD, allora l'underscore può essere facilmente sostituito con un trattino, per esempio:

```
 source=($pkgname-${pkgver/_/-}.tar.gz)

```

### pkgrel

Il numero della versione di rilascio del pacchetto specifico di Arch Linux. Questo valore permette agli utenti di distinguere tra build consecutive della stessa versione del pacchetto. Quando una nuova versione del pacchetto viene rilasciata, il **numero di rilascio parte da 1**. Nel caso in cui si apportino aggiustamenti e ottimizzazioni al file `PKGBUILD`, allora il pacchetto verrà **ri-rilasciato** e il **numero di rilascio** verrà incrementato di 1\. Nel caso in cui esca una nuova versione del pacchetto, il numero di rilascio verrà resettato a 1.

### pkgdir

Questa variabile rappresenta la directory di root di ciò che verrà inserito nel pacchetto. È normalmente usata in `make DESTDIR="$pkgdir" install`.

### epoch

Un valore intero, specifico di Archlinux, che rappresenta "l'età" tramite la quale effettuare un confronto tra numeri di versione. Questo valore consente di ignorare le normali regole di confronto di versione per pacchetti che hanno una numerazione di versione inconsistente, che richiedono un downgrade, che devono cambiare lo schema di numerazione, etc. Per impostazione predefinita, si assume che i pacchetti abbiano un valore di epoch pari a *0*. Non utilizzare questa variabile a meno che non si sia assolutamente sicuri di ciò che si sta facendo.

### pkgbase

Una variabile opzionale è disponibile durante la creazione di pacchetti multipli, pkgbase è utilizzata come riferimento al gruppo di pacchetti nell'output di makepkg e nella nomenclatura dei tarball di soli sorgenti. Se non viene specificata, verrà usato al suo posto il primo elemento dell'array pkgname. Tutte le opzioni e le direttive dei pacchetti multipli assumono di default i valori definiti globalmente nel PKGBUILD. Nonostante questo, le seguenti variabili possono essere ridefinite all'interno della funzione di pacchettizzazione di ogni singolo pacchetto creato: pkgver, pkgrel, epoch, pkgdesc, arch, url, license, groups, depends, optdepends, provides, conflicts, replaces, backup, options, install e changelog. Il nome della variabile non può iniziare con un trattino.

### pkgdesc

La descrizione del pacchetto. La descrizione dovrebbe essere di circa 80 caratteri o meno e non dovrebbe includere il nome del pacchetto stesso. Per esempio, "Nedit è un editor di testo per X11" si dovrebbe scrivere come "un editor di testo per X11."

**Nota:** Non seguire questa regola pedissequamente quando si inviano pacchetti ad [AUR](/index.php/AUR "AUR"). Se per qualche motivo il nome del pacchetto differisce dal nome del programma, l'inclusione del nome completo all'interno della descrizione può essere l'unica maniera per renderlo reperibile tramite la ricerca.

### arch

Una array di architetture contro le quali il file `PKGBUILD` deve essere compilato ed utilizzato. Attualmente, può contenere `i686` e/o `x86_64`, `arch=('i686' 'x86_64')`. E' possibile utilizzare anche il valore `any` per i pacchetti indipendenti dall'architettura.

È possibile accedere a questo valore durante la compilazione e durante la definizione di variabili, con la variabile `$CARCH`. Consultare [FS#16352](https://bugs.archlinux.org/task/16352). Esempio:

```
depends=(foobar)
if test "$CARCH" == x86_64; then
  depends+=(lib32-glibc)
fi

```

### url

L'URL del sito ufficiale del software che si sta pacchettizzando.

### license

La licenza con la quale il software è distribuito. Il pacchetto [licenses](https://www.archlinux.org/packages/?name=licenses) presente in `[core]` fornisce le licenze più comuni in `/usr/share/licenses/common`, per esempio `/usr/share/licenses/common/GPL`. Se un pacchetto è munito di una di queste licenze, il valore dovrebbe essere impostato al nome della directory, per esempio `license=('GPL')`. Se la licenza appropriata non è inclusa del pacchetto ufficiale [licenses](https://www.archlinux.org/packages/?name=licenses), si devono fare alcune cose:

1.  Il file della licenza dovrebbe essere incluso in: `/usr/share/licenses/**pkgname**/`, per esempio `/usr/share/licenses/foobar/LICENSE`.
2.  Se l'archivio dei sorgenti **NON** contiene i dettagli della licenza ed essa è visualizzata altrove, ad esempio su un sito web, allora si doverbbe copiare la licenza su un file da includere.
3.  Aggiungere `custom` all'array delle `license`. Facoltativamente, si può rimpiazzare `custom` con `custom:nome della licenza`. Una volta che la licenza è utilizzata in due o più pacchetti dei repository ufficiali (incluso `[community]`), entrerà a far parte del pacchetto [licenses](https://www.archlinux.org/packages/?name=licenses).

*   Le licenze [BSD](https://en.wikipedia.org/wiki/BSD_License "wikipedia:BSD License"), [MIT](https://en.wikipedia.org/wiki/MIT_License "wikipedia:MIT License"), [zlib/png](https://en.wikipedia.org/wiki/ZLIB_license "wikipedia:ZLIB license") e [Python](https://en.wikipedia.org/wiki/Python_License "wikipedia:Python License") sono casi speciali e potrebbero non essere inclusi nel pacchetto [licenses](https://www.archlinux.org/packages/?name=licenses). Per quanto riguarda l'array `license`, queste vengono trattate come licenze comuni (`license=('BSD')`, `license=('MIT')`, `license=('ZLIB')` e `license=('Python')`) ma tecnicamente ognuna è una licenza custom poiché ha il proprio copyright. Ogni pacchetto munito di una di queste quattro licenze dovrebbe avere la propria salvata in `/usr/share/licenses/**pkgname**`. Alcuni pacchetti potrebbero non essere coperti da una sola licenza. In questi casi, sono possibili più voci nell'array license, ad esempio `license=('GPL' 'custom:nome della licenza')`.
*   Inoltre, le (L)GPL hanno diverse versioni e permutazioni di queste versioni. Per il software (L)GPL, la convenzione è:
    *   (L)GPL - (L)GPLv2 o qualsiasi versione successiva
    *   (L)GPL2 - (L)GPL2 solamente
    *   (L)GPL3 - (L)GPL3 o qualsiasi versione successiva
*   Se non si riesce a determinare la licenza del software che si sta pacchettizzando, `PKGBUILD.proto` consiglia di utilizzare il valore `unknown`. Bisonga comunque contattare il creatore del software per sapere a quali condizioni il prodotto è disponibile (ed a quali non lo è)

**Tip:** Alcuni autori non forniscono un file separato per la licenza e descrivono le regole per la distribuzione all'interno del file ReadMe. Queste informazioni possono essere estratte in un file separato durante la fase di `build` con un comando simile a questo: `sed -n '/**This software**/,/ **thereof.**/p' ReadMe.txt > LICENSE` 

### groups

Il gruppo al quale appartiene il pacchetto. Per esempio, quando si installa il pacchetto [kdebase](https://www.archlinux.org/groups/x86_64/kdebase/), si installano tutti i pacchetti che appartengono al gruppo [kde](https://www.archlinux.org/groups/x86_64/kde/).

### depends

Un array di nomi dei pacchetti che devono essere installati per poter poi lanciare questo software. Se il software richiede una versione minima di una dipendenza, si dovrebbe usare l'operatore `>=` per sottolinearlo, ad esempio: `depends=('foobar>=1.8.0')`. Non è necessario elencare i pacchetti che il software richiede come dipendenza se questi sono già richiesti come tale dagli altri pacchetti elencati nell'array. Per esempio, [gtk2](https://www.archlinux.org/packages/?name=gtk2) dipende da [glib2](https://www.archlinux.org/packages/?name=glib2) e [glibc](https://www.archlinux.org/packages/?name=glibc). Tuttavia, [glibc](https://www.archlinux.org/packages/?name=glibc) non è necessita di essere elencato come dipendenza per [gtk2](https://www.archlinux.org/packages/?name=gtk2) visto che è dipendenza per [glib2](https://www.archlinux.org/packages/?name=glib2).

### optdepends

Un array di nomi dei pacchetti che non sono necessari al software per funzionare ma che forniscono funzionalità aggiuntive. Si dovrebbe aggiungere una piccola descrizione delle funzionalità che ogni pacchetto fornisce. Un'array `optdepends` deve assomigliare a questo:

```
optdepends=('cups: supporto per la stampa'
'sane: supporto per gli scanner'
'libgphoto2: supporto per le fotocamere digitali'
'alsa-lib: supporto per l'audio'
'giflib: supporto per le immagini GIF'
'libjpeg: supporto per le immagini JPEG'
'libpng: supporto per le immagini PNG')

```

### makedepends

Un array di nomi dei pacchetti che devono essere installati per poter compilare il software ma inutili per poter usare il software dopo l'installazione. E' possibile specificare la versione minima di dipendenza del pacchetto nello stesso formato dell'array `depends`.

**Nota:** Non è necessario specificare pacchetti già presenti nell'array `depends`

**Attenzione:** Quando si compila con makepkg, si assume che si abbia già installato nel proprio sistema il gruppo "base-devel" . I membri di "base-devel" **non** devono essere inclusi nell'array `makedepends`.

### checkdepends

Un array di pacchetti dai quali il pacchetto in oggetto dipende solo per l'esecuzione della sua suite di prova, e non per il suo corretto funzionamento. I pacchetti in questa lista seguono le stesse regole di quelli nell'array depends. Queste dipendenze sono prese in considerazione solo quando è presente la funzione `check()` che deve essere eseguita da makepkg.

### provides

Un array di nomi dei pacchetti dei quali questo software fornisce le funzionalità (oppure un pacchetto virtuale come *cron* o *sh*). Se si usa questa variabile, si dovrebbe aggiungere la versione (`pkgver` e magari la `pkgrel`) che questo pacchetto fornisce se le dipendenze possono esserne influenzate. Per esempio, se si vuole fornire una versione modificata di *qt* chiamata *qt-foobar* versione 3.3.8 che fornisce *qt* allora l'array `provides` dovrebbe essere: `provides=('qt=3.3.8')`. Mettere `provides=('qt')` causerà il fallimento di quelle dipendenze che richiedono una specifica versione di *qt*. Non aggiungere `pkgname` all'array provide, viene fatto in automatico.

### conflicts

Un array di nomi dei pacchetti che possono causare problemi con questo pacchetto installato. I pacchetti con questo nome, e tutti quelli che includono questo nome nel loro array `provides` saranno rimossi. Si possono anche specificare le proprietà delle versioni dei pacchetti che vanno in conflitto nello stesso formato dell'array `depends`.

### replaces

Un array di nomi dei pacchetti obsoleti che sono rimpiazzati da questo pacchetto, per esempio: `replaces=('wireshark')` per il pacchetto [wireshark-gtk](https://www.archlinux.org/packages/?name=wireshark-gtk). Dopo aver aggiornato il database con `pacman -Sy`, rimpiazzerà immediatamente un pacchetto installato con un altro pacchetto dei repository, accoppiato relativamente a `replaces`. Se si sta fornendo una versione sostitutiva di un pacchetto esistente, si dovrà usare la variabile `conflicts` la quale è valutata soltanto nel momento in cui si installerà il pacchetto in conflitto.

### backup

Un array di file che potrebbero contenere personalizzazioni effettuate dall'utente e che dovrebbero essere cpnservati anche in caso di aggiornamento o rimozione di un pacchetto, pensato principalmente per il file di configurazione sotto `/etc`. Quando si aggiorna, nuove versioni dei suddetti file potrebbero venire salvate sul disco con l'estensione `file.pacnew` per evitare di sovrascrivere un file che già esiste ed è stato precedentemente modificato dall'utente. In maniera simile, quando il pacchetto viene rimosso, i file modificati dall'utente saranno mantenuti come `file.pacsave`, a meno che il pacchetto non sia stato rimosso passando a pacman lo switch `-n`. I percorsi dei file nell'array dovrebbero essere percorsi relativi (ad es. `etc/pacman.conf`)e non assoluti (`/etc/pacman.conf`). Consultare anche [Pacnew and Pacsave Files (Italiano)](/index.php/Pacnew_and_Pacsave_Files_(Italiano) "Pacnew and Pacsave Files (Italiano)").

### options

Questo array permette di sovrascrivere alcuni dei comportamenti di default di `makepkg`. Per impostare un'opzione, si deve includere il nome dell'opzione nell'array. Per invertire il comportamento di default, si deve mettere un `!` davanti l'opzione. Questo è un elenco delle opzioni che si possono mettere nell'array:

*   ***strip*** - Toglie i simboli dai binari e dalle librerie. Se si utilizzano spesso debugger su programmi e librerie, è più conveniente disabilitare questa opzione.
*   ***docs*** - Salva le directory `/doc`.
*   ***libtool*** - Lascia i file di *libtool* (`.la`) nel pacchetto.
*   ***staticlibs*** - Lascia i file di librerie statiche (.a) nei pacchetti.
*   ***emptydirs*** - Lascia le directory vuote nel pacchetto.
*   ***zipman*** - Comprime le pagine di *man* e *info* con *gzip*.
*   ***purge*** - Rimuove dai pacchetti i file specificati nella variabile `PURGE_TARGETS`
*   ***upx*** - Comprime i file eseguibili binari utilizzando UPX. Opzioni addizionali possono essere passate ad UPX tramite la variabile `UPXFLAGS`
*   ***ccache*** - Permette l'uso di `ccache` durante la compilazione. Utile principalmente nella sua forma negata `!ccache` con i pacchetti che hanno problemi nella compilazione con `ccache`.
*   ***distcc*** - Permette l'uso di `distcc` durante la compilazione. Utile principalmente nella sua forma negata `!distcc` con i pacchetti che hanno problemi nella compilazione con `distcc`.
*   ***buildflags*** - Consente l'utilizzo di `buildflags` specifiche per l'utente (CFLAGS, CXXFLAGS, LDFLAGS) durante la compilazione. Utile principalmente nella sua forma negata `!buildflags` con i pacchetti che hanno problemi nella compilazione con `buildflags`.
*   ***makeflags*** - Permette l'uso di `makeflags` specifiche per l'utente durante la compilazione. Utile principalmente nella sua forma negata `!makeflags` con i pacchetti che hanno problemi nella compilazione con `makeflags` personalizzate.

### install

Il nome dello script di `.install` che deve essere incluso nel pacchetto. *Pacman* ha l'abilità di memorizzare ed eseguire uno script specifico per pacchetto quando installa, rimuove o aggiorna un pacchetto. Lo script contiene le seguenti istruzioni che vengono eseguite in tempi diversi:

*   ***pre_install*** - Lo script è lanciato appena prima dell'estrazione dei file. La nuova versione del pacchetto viene passata come argomento alla funzione.
*   ***post_install*** - Lo script è lanciato appena dopo l'estrazione dei file. La nuova versione del pacchetto viene passata come argomento alla funzione.
*   ***pre_upgrade*** - Lo script è lanciato appena prima dell'estrazione dei file. La nuova e la vecchia versione del pacchetto vengono passate come argomento alla funzione.
*   ***post_upgrade*** - Lo script è lanciato appena dopo dell'estrazione dei file. La nuova e la vecchia versione del pacchetto vengono passate come argomento alla funzione.
*   ***pre_remove*** - Lo script è lanciato appena che i file vengano rimossi. La vecchia versione del pacchetto viene passata come argomento alla funzione.
*   ***post_remove*** - Lo script è lanciato dopo che i file vengano rimossi. La vecchia versione del pacchetto viene passata come argomento alla funzione.

Ogni funzione è eseguita in ambiente chroot all'interno della directory di installazione di pacman. Consultare [questo thread](https://bbs.archlinux.org/viewtopic.php?pid=913891).

**Tip:** Un prototipo `.install` è disponibile al `/usr/share/pacman/proto.install`.

### changelog

Il nome del changelog del pacchetto. Per vedere i changelog dei pacchetti installati (che lo forniscono):

 `pacman -Qc *pkgname*` 
**Tip:** Un prototipo di file changelog è installato in `/usr/share/pacman/ChangeLog.proto`.

### source

un array di file che sono necessari per compilare il pacchetto. Deve contenere la locazione dei sorgenti del software, che in quasi tutte le occasioni è un completo URL HTTP o FTP. Le variabili precendentemente impostatate `pkgname` e `pkgver` possono essere usate efficacemente qui (per esempio `source=(http://example.com/$pkgname-$pkgver.tar.gz)`)

**Nota:** Se si ha il bisogno di fornire file che non sono scaricabili al volo, per esempio patch fatte in proprio, è possibile mettere questi file nella stessa directory del proprio `PKGBUILD` e aggiungere il nome del file a questo array. Qualsiasi percorso viene aggiunto qui è risolto relativamente alla directory in cui giace il `PKGBUILD`. Prima che il processo di compilazione parta, tutti i file che sono riferiti in questo array, verranno scaricati o controllati in sussistenza, e `makepkg` non procederà oltre se qualcuno manca.

**Nota:** È possibile specificare un nome diverso per il file scaricato, nel caso tale file abbia per qualche motivo un nome diverso, come il parametro GET assegnato all'url, con la seguente sintassi: `*filename*::*fileuri*`, ad esempio `$pkgname-$pkgver.zip::http://199.91.152.193/7pd0l2tpkidg/jg2e1cynwii/Warez_collection_16.4.exe`

### noextract

Un array di file elencati nell'array `source` che non dovrebbero essere estratti dal loro archivio da `makepkg`. Per lo più si applica a certi archivi che non possono essere gestiti da `/usr/bin/bsdtar` visto che [libarchive](https://www.archlinux.org/packages/?name=libarchive) processa tutti i file come flussi piuttosto che ad accesso casuale come fa [unzip](https://www.archlinux.org/packages/?name=unzip). In queste situazioni si dovrebbero aggiungere gli strumenti di decompressione alternativi (ad esempio `unzip`, `p7zip`, etc.) all'array `makedepends` e le prime linee della funzione [prepare()](/index.php/Creating_packages_(Italiano)#La_funzione_prepare.28.29 "Creating packages (Italiano)") dovrebbero estrarre l0'archivio di sorgenti manualmente; ad esempio:

```
unzip [source].zip

```

Bisogna tenere presente che mentre l'array `source` accetta degli URL, `noextract` richiede **solo** la porzione col nome del file. Se per esempio si vuole fare qualcosa del genere (semplificazione del [grub2's PKGBUILD](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/PKGBUILD?h=packages/grub)):PKGBUILD di grub2]):

```
source=("http://ftp.archlinux.org/other/grub2/grub2_extras_lua_r20.tar.xz")
noextract=("grub2_extras_lua_r20.tar.xz")

```

Per *non estrarre nulla*, si può utilizzare un espediente come questo ( preso dal [PKGBUILD di firefox-i18n](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/PKGBUILD?h=packages/firefox-i18n#n123)):

```
noextract=(${source[@]%%::*})

```

Da notare che una sostituzione di variabile più conservativa della sintassi Bash avrebbe incluso anche delle virgolette, o addirittura un ciclo che richiamasse `basename`.

### md5sums

Un array di checksum MD5 dei file elencati nell'array `source`. Una volta che tutti i file presenti nell'array `source` saranno disponibili, per ogni file verrà generato automaticamente un hash MD5 e confrontato con il valore di questo array nello stesso ordine in cui appare nell'array `source`. Mentre l'ordine dell'array source non è rilevante, è importante che questo combaci con l'ordine di questo array dato che `makepkg` non può indovinare a quale file sorgente appartenga la checksum. E' possibile generare questo array rapidamente e facilmente usando il comando `updpkgsums` o `makepkg -g` nella directory che contiene il file `PKGBUILD`.

**Nota:** L'algoritmo MD5 è noto per avere falle, quindi si dovrebbero considerare alternative più sicure.

### sha1sums

Un array di checksum SHA-1 a 160-bit. Questa è un'alternativa alle md5sums descritte in precedenza, ma anch'esse sono note per avere delle debolezze, quindi si dovrebbero considerare alternative più sicure. Per abilitare l'uso e la generazione di queste checksums, assicurarsi di impostare l'opzione `INTEGRITY_CHECK` in `makepkg.conf`. Consultare man `makepkg.conf`.

### sha256sums, sha384sums, sha512sums

Un array di checksum SHA-2 con dimensione del digest di 256, 384 e 512 bit rispettivamente. Queste sono delle alternative alle md5sums descritte in precedenza e sono generalmente considerate più sicure. Per abilitare l'uso e la generazione di queste checksums, assicurarsi di impostare l'opzione INTEGRITY_CHECK in makepkg.conf. Vedere man makepkg.conf.

## Consultare anche

*   [Example PKGBUILD file](http://ix.io/66p)
*   [Example .install file](http://ix.io/66o)