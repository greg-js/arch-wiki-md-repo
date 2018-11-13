Quest'articolo fornisce una panoramica dell' Arch Build System insieme ad una guida passo passo per principianti. Non è una guida di riferimento completa! Se si necessita di ulteriori informazioni, si è pregati di consultare il manuale.

**Nota:** ABS viene sincronizzato una volta al giorno, per questo motivo è fisiologico un ritardo nell'aggiornamento rispetto ai pacchetti presenti effettivamente nei repository.

## Contents

*   [1 Cosa è ABS?](#Cosa_è_ABS?)
    *   [1.1 Cos'è un sistema ports-like?](#Cos'è_un_sistema_ports-like?)
    *   [1.2 **ABS** è un concetto simile](#ABS_è_un_concetto_simile)
    *   [1.3 Descrizione generale di ABS](#Descrizione_generale_di_ABS)
*   [2 Perchè dovrei usare ABS?](#Perchè_dovrei_usare_ABS?)
*   [3 Come usare ABS?](#Come_usare_ABS?)
    *   [3.1 Strumenti d'installazione](#Strumenti_d'installazione)
    *   [3.2 /etc/abs.conf](#/etc/abs.conf)
    *   [3.3 L'albero ABS](#L'albero_ABS)
    *   [3.4 Scaricare l'albero ABS](#Scaricare_l'albero_ABS)
    *   [3.5 /etc/makepkg.conf](#/etc/makepkg.conf)
        *   [3.5.1 Impostare la variabile PACKAGER all'interno di /etc/makepkg.conf](#Impostare_la_variabile_PACKAGER_all'interno_di_/etc/makepkg.conf)
            *   [3.5.1.1 Mostrare tutti i pacchetti (inclusi quelli presi da AUR)](#Mostrare_tutti_i_pacchetti_(inclusi_quelli_presi_da_AUR))
            *   [3.5.1.2 Mostrare solo i pacchetti contenuti nei repository](#Mostrare_solo_i_pacchetti_contenuti_nei_repository)
    *   [3.6 Creare una directory di compilazione](#Creare_una_directory_di_compilazione)
    *   [3.7 Compilazione del pacchetto](#Compilazione_del_pacchetto)
        *   [3.7.1 fakeroot](#fakeroot)

## Cosa è ABS?

ABS è l'acronimo di "**A**rch **B**uild **S**ystem", cioè *Sistema di costruzione (dei pacchetti) di Arch*. E' un sistema per fare pacchetti del codice sorgente. Mentre [pacman](/index.php/Pacman "Pacman") è il tool di Arch specializzato nella gestione dei pacchetti binari (inclusi i pacchetti fatti con ABS), ABS è il tool specializzato nella compilazione dei sorgenti in un pacchetto `.pkg.tar.xz` installabile.

### Cos'è un sistema ports-like?

*Ports* è il sistema usato da FreeBSD per l'automazione della generazione di pacchetti a partire dal codice sorgente. Il sistema usa un *port* per scaricare, scompattare, patchare, compilare e installare il software desiderato. Un *port* è solo una piccola directory nel computer dell'utente, chiamata come il corrispondente software che vi verrà installato, che contiene un po' di file con le istruzioni per scaricare ed installare il pacchetto dai sorgenti. Questo rende possibile la la generazione del pacchetto con un semplice `make` o `make install clean` all'interno della directory port.

### **ABS** è un concetto simile

"ABS" è costituito da un albero di directory ("ABS Tree"), situato in `/var/abs`, che contiene molte sottodirectory, ognuna dentro una categoria, e ognuna chiamata con il rispettivo pacchetto installabile contenuto al suo interno. Quest'albero rappresenta (ma non contiene) tutto il *software ufficialmente disponibile in Arch*, reperibile tramite sistema SVN. Si può considerare ogni sottodirectory chiamata come un pacchetto un *ABS*, più o meno allo stesso modo con cui ci si potrebbe riferire ad un *Port*. Questi *ABS*, o sottodirectory, non contengono il pacchetto nè il codice sorgente del software, bensì un file [PKGBUILD](/index.php/PKGBUILD_(Italiano) "PKGBUILD (Italiano)") (e a volte altri file). Un PKGBUILD è un semplice script, un file di testo contenente le istruzioni per la compilazione e la pacchettizzazione, ma anche l'url dell'apposito **tarball di sorgenti** da scaricare. (I componenti più importanti di ABS sono proprio i PKGBUILD). Utilizzando il comando di ABS [makepkg](/index.php/Makepkg_(Italiano) "Makepkg (Italiano)"), il software viene prima compilato e poi *pacchettizzato* all'interno della directory di compilazione, prima di poter essere installato. Da questo momento si potrà usare [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)"), il gestore pacchetti di Arch Linux per installare, aggiornare, e rimuovere il nuovo pacchetto.

### Descrizione generale di ABS

"ABS" potrebbe essere usato come un termine "ad ombrello", in quanto include, ed è formato, da molti altri componenti. Pertanto, parlando in termini non proprio tecnici, "ABS" fa riferimento alla seguente struttura come un toolkit completo:

	L'albero ABS

	La struttura di directory di ABS; una gerarchia SVN sotto `/var/abs/` sul proprio sistema locale. Contiene molte sottodirectory, chiamate con il nome di ogni software disponibile per arch nei repository specificati in `/etc/abs.conf`, ma non i pacchetti stessi. L'albero è creato dopo aver installato il pacchetto [abs](https://www.archlinux.org/packages/?name=abs) tramite pacman e dopo aver eseguito lo script `abs`

	[PKGBUILD](/index.php/PKGBUILD_(Italiano) "PKGBUILD (Italiano)")

	Script in BASH contenente le istruzioni per costruire i pacchetti e l'URL dei sorgenti.

	[Makepkg](/index.php/Makepkg_(Italiano) "Makepkg (Italiano)")

	Il comando da shell di ABS che legge il PKGBUILD, scarica e compila il sorgente e crea il `.pkg.tar.gz or .pkg.tar.xz`, in accordo con l'array `PKGEXT` all'interno di `makepkg.conf`. È anche possibile utilizzare makepkg per compilare i propri pacchetti da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") o da fonti esterne. (Consultare l'articolo [Creating packages (Italiano)](/index.php/Creating_packages_(Italiano) "Creating packages (Italiano)"))

**Strumenti correlati**

	[Pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)")

	Pacman è completamente separato, ma è necessario invocarlo o dal makepkg o manualmente, per installare e rimuovere i pacchetti costruiti, e per risolvere le dipendenze.

	[AUR](/index.php/AUR_(Italiano) "AUR (Italiano)")

	Il repository degli utenti della comunità di Arch è separato da ABS, ma i PKGBUILD non supportati di [AUR](/index.php/AUR "AUR") (unsupported) possono essere usati con il tool **makepkg** di ABS, per compilare e impacchettare il software. A differenza dell'albero ABS presente in locale, AUR esiste come interfaccia web. Contiene migliaia di PKGBUILD degli utenti per pacchettizzare software non presente come pacchetto ufficiale di Arch. Avendo bisogno di compilare un pacchetto al di fuori delle strutture ufficiali di Arch, è molto probabile poterlo trovare su AUR.

## Perchè dovrei usare ABS?

L'Arch Build System (abbreviato con ABS) è usato per:

*   Compilare o ri-compilare un pacchetto per qualsiasi motivo
*   Creare nuovi pacchetti da codice sorgente, di software per i quali non sono ancora disponibili pacchetti (Vedi anche [Creating Packages](/index.php/Creating_packages_(Italiano) "Creating packages (Italiano)"))
*   Modificare pacchetti esistenti per adattarli ai propri bisogni (abilitando o disabilitando opzioni, applicando patch)
*   Ricompilare il tuo intero sistema utilizzando flag di compilazione "a la FreeBSD" (ad esempio con [pacbuilder](/index.php/Pacbuilder "Pacbuilder"))
*   Pacchettizzare e installare in modo pulito il proprio kernel personalizzato. (Consultare [Kernel Compilation](/index.php/Kernel_Compilation "Kernel Compilation") così come [Custom Kernel Compilation with ABS](/index.php/Custom_Kernel_Compilation_with_ABS "Custom Kernel Compilation with ABS"))
*   Utilizzare moduli del kernel che funzionino col proprio kernel personalizzato
*   Compilare ed installare facilmente un pacchetto per Arch più recente, più vecchio, in beta testing, o in sviluppo modificando il numero di versione nel PKGBUILD.

ABS non è necessario per usare Arch Linux, ma è utile per un processo sicuro di compilazione dei sorgenti.

## Come usare ABS?

La compilazione di pacchetti tramite ABS consta dei seguenti passaggi:

1.  Installare il pacchetto [abs](https://www.archlinux.org/packages/?name=abs) tramite [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)")
2.  Eseguire `abs` da utente root in modo da creare l'albero ABS sincronizzato con i server di Arch Linux
3.  Copiare i file di compilazione (che solitamente si trovano sotto `/var/abs/<repo>/<pkgname>`) in una directory di compilazione a scelta
4.  Portarsi nella suddetta directory, modificare il PKGBUILD secondo le proprie esigenze (se necessario), ed eseguire **makepkg**
5.  makepkg, basandosi sulle istruzioni presenti nel PKGBUILD, scaricherà i sorgenti appropriati, li decomprimerà, applicherà eventuali patch, compilerà secondo le `CFLAGS` specificate nel file `makepkg.conf` ed infine comprimerà i file compilati all'interno di un pacchetto con estensione `.pkg.tar.gz` o `.pkg.tar.xz` in base a come specificato all'interno di `makepkg.conf`
6.  L'installazione del pacchetto creato è semplice quanto eseguire `pacman -U <.pkg.tar.xz file>`. La rimozione del pacchetto è gestita in maniera classica da pacman.

### Strumenti d'installazione

Per utilizzare ABS, bisogna innanzitutto [installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") il pacchetto [abs](https://www.archlinux.org/packages/?name=abs) dai [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)")

Ciò installerà gli script di sincronizzazione di ABS, vari script di compilazione, ed [rsync](/index.php/Rsync "Rsync") (come dipendenza, nel caso non fosse già installato).

Prima di poter effettivamente compilare qualcosa, comunque, è necessario [installare](/index.php/Pacman_(Italiano)#Installare_gruppi_di_pacchetti "Pacman (Italiano)") anche i programmi di compilazione di base. Questi ultimi sono raccolti all'interno del gruppo **base-devel**.

### /etc/abs.conf

Con privilegi di root modifica `/etc/abs.conf` per includere i repository che desideri aggiungere:

Rimuovere il `!` davanti ai repository che vuoi abilitare (esempio): `REPOS=(core extra community !testing)`

### L'albero ABS

L'albero ABS è una gerarchia di directory SVN situata in `/var/abs` con una struttura simile a questa

```
| -- core/
|     || -- acl/
|     ||     || -- PKGBUILD
|     || -- attr/
|     ||     || -- PKGBUILD
|     || -- abs/
|     ||     || -- PKGBUILD
|     || -- autoconf/
|     ||     || -- PKGBUILD
|     || -- ...
| -- extra/
|     || -- acpid/
|     ||     || -- PKGBUILD
|     || -- apache/
|     ||     || -- PKGBUILD
|     || -- ...
| -- community/
|     || -- ...

```

In pratica l'albero ABS ha la stessa struttura del database dei pacchetti:

*   Primo livello: nome del Repository
*   Secondo livello: directory dei nomi dei pacchetti
*   Terzo livello: PKGBUILD (contiene le informazioni necessarie alla compilazione dei pacchetti) ed altri file correlati (patch ed altri file necessari alla compilazione)

Il codice sorgente non e' presente nelle directory ABS. È invece il file **PKGBUILD** che contiene un URL dal quale verrà scaricato il codice sorgente al momento della compilazione. Per questo motivo la dimensione dell'albero ABS è relativamente contenuta.

### Scaricare l'albero ABS

Da root, digitare:

 `# abs` 

L'albero ABS verrà creato in `/var/abs`. Da notare come ogni ramo di questo albero corrisponda ai repository abilitati in `/etc/abs.conf`.

Il comando abs dovrebbe essere usato periodicamente per sincronizzare l'albero ABS locale con i repository ufficiali. Singoli pacchetti ABS possono essere scaricati con

 `# abs <repository>/<package>` 

In questo modo non è necessario controllare l'intero albero ABS per compilare un solo pacchetto.

### `/etc/makepkg.conf`

`/etc/makepkg.conf` e' un file che specifica le variabili d'ambiente e i flag del compilatore che magari si vuole modificare se si utilizza un sistema SMP, o per specificare altre ottimizzazioni. Le impostazioni di default sono ottimizzate per le architetture i686 e x86_64, e andranno generalmente bene per i sistemi con una sola cpu. (vanno bene anche per le macchina SMP, ma useranno soltanto una cpu- consultare [makepkg](/index.php/Makepkg_(Italiano) "Makepkg (Italiano)").)

#### Impostare la variabile PACKAGER all'interno di /etc/makepkg.conf

L'impostazione della variabile PACKAGER all'interno di `/etc/makepkg.conf` è un'operazione opzionale ma caldamente consigliata. Abilita una "flag" che consente la rapida identificazione di tutti i pacchetti compilati ed installati in locale dall'utente stesso, anzichè dal maintainer ufficiale. Ciò è ottenibile in maniera molto semplice utilizzando [expac](https://www.archlinux.org/packages/?name=expac) presente nel repo community.

##### Mostrare tutti i pacchetti (inclusi quelli presi da AUR)

```
$ grep myname /etc/makepkg.conf
PACKAGER="myname <myemail@myserver.com>

```

```
$ expac "%n %p" | grep "myname" | column -t
archey3 myname
binutils myname
gcc myname
gcc-libs myname
glibc myname
tar myname

```

##### Mostrare solo i pacchetti contenuti nei repository

Questo esempio nostra solo i pacchetti presenti nei repository specificati in `/etc/pacman.conf`:

```
$ . /etc/makepkg.conf; grep -xvFf <(pacman -Qqm) <(expac "%n\t%p" | grep "$PACKAGER$" | cut -f1)
binutils
gcc
gcc-libs
glibc
tar

```

### Creare una directory di compilazione

Si raccomanda di creare una directory dove avra' luogo la compilazione; non bisognerebbe mai modificare l'albero di ABS compilando i pacchetti al suo interno, poiché questi dati verranno sovrascritti al primo aggiornamento dell'albero ABS. E' buona norma usare la propria directory home, mentre alcuni utenti preferiscono creare una directory 'local' sotto `/var/abs/` , impostando l'utente semplice come proprietario.

Come detto, creare la directory di compilazione, ad es.:

 `$ mkdir -p $HOME/abs` 

Copiare l'albero ABS (`/var/abs/<repository>/<pkgname>`) nella directory di compilazione.

### Compilazione del pacchetto

In questo esempio verrà mostrato come compilare il pacchetto del display manager "slim".

Copiare l'ABS di slim nella directory di compilazione.

 `$ cp -r /var/abs/extra/slim/ ~/abs` 

Accedere alla directory.

 `$ cd ~/abs/slim` 

Modificare il PKGBUILD per aggiungere o rimuovere il supporto a determinati componenti, per applicare patch, per cambiare la versione del pacchetto, etc. (opzionale)

 `$ nano PKGBUILD` 

Eseguire makepkg da utente normale (con lo switch `-s` per installare con la risoluzione automatica delle dipendenze (richiede la presenza del pacchetto [sudo](https://www.archlinux.org/packages/?name=sudo).)

 `$ makepkg -s` 
**Attenzione:** Prima di lamentarsi riguardo la mancanza delle dipendenze di compilazione. ricordarsi che il gruppo [base](https://www.archlinux.org/groups/x86_64/base/) si suppone già installato su qualsiasi sistema Arch Linux. Il gruppo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) si suppone già installato quando si compila con makepkg. Consultare [#Strumenti d'installazione](#Strumenti_d'installazione)

Installare da root:

 `# pacman -U slim-1.3.0-2-i686.pkg.tar.xz` 

Fatto. Si è appena compilato slim da sorgenti e lo si è installato nel sistema attraverso pacman, anche la rimozione è gestita da pacman --

(`pacman -R slim`).

Il metodo ABS aggiunge un livello di convenienza ed automazione, mantenendo però sempre la completa trasparenza e controllo delle funzioni di compilazione includendole nel PKGBUILD.

#### fakeroot

Essenzialmente, si sono eseguiti gli stessi passaggi della compilazione tradizionale (che generalmente includono `./configure, make, make install` ) ma il software è stato installato in un ambiente `fake root`. ( Un ambiente di *fake root* non è altro che una sottodirectory della directory di compilazione che funziona e si comporta come se fosse la directory root del sistema. In cooperazione con il programma ***fakeroot***, makepkg crea una falsa directory root, e vi installa i binari compilati e i file correlati, con **root** come proprietario.) Il *fake root*, o l'abero di sottodirectory contenente il software compilato, viene quindi compresso in un archivio con estensione `.pkg.tar.xz`, o *pacchetto*. Quando richiamato, pacman estrae il pacchetto (lo installa) nella directory root reale del sistema (`/`).