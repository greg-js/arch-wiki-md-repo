Articoli correlati

*   [Creare Pacchetti](/index.php/Creating_Packages_(Italiano) "Creating Packages (Italiano)")
*   [PKGBUILD](/index.php/PKGBUILD_(Italiano) "PKGBUILD (Italiano)")
*   [Arch User Repository](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)")
*   [Pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)")
*   [Repository Ufficiali](/index.php/Official_repositories "Official repositories")
*   [Arch Build System](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)")

makepkg è utilizzato per compilare e creare pacchetti installabili da [Pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)"), il gestore pacchetti di Arch Linux. makepkg è uno script che automatizza la creazione dei pacchetti; esso può scaricare e verificare i sorgenti dei file, controllare le dipendenze, configurare le impostazioni, compilare i sorgenti, installare in una directory temporanea, personalizzare i pacchetti, generare meta-informazioni e pacchettizzare il tutto.

makepkg è incluso nel pacchetto [pacman](https://www.archlinux.org/packages/?name=pacman).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configurazione](#Configurazione)
    *   [1.1 Flag di compilazione e architettura](#Flag_di_compilazione_e_architettura)
        *   [1.1.1 MAKEFLAGS](#MAKEFLAGS)
    *   [1.2 Output del pacchetto](#Output_del_pacchetto)
    *   [1.3 Controllo firma](#Controllo_firma)
*   [2 Utilizzo](#Utilizzo)
*   [3 Trucchi e consigli](#Trucchi_e_consigli)
    *   [3.1 Sostituzione automatica checksums nel PKGBUILD](#Sostituzione_automatica_checksums_nel_PKGBUILD)
        *   [3.1.1 Opzione 1](#Opzione_1)
        *   [3.1.2 Opzione 2](#Opzione_2)
    *   [3.2 ATTENZIONE: Il pacchetto contiene riferimenti a $srcdir](#ATTENZIONE:_Il_pacchetto_contiene_riferimenti_a_$srcdir)
*   [4 Altre risorse](#Altre_risorse)

## Configurazione

`/etc/makepkg.conf` è il principale file di configurazione di makepkg. La maggior parte degli utenti vorrà personalizzare il file di configurazione di makepkg prima di iniziare a compilare qualsiasi pacchetto.

### Flag di compilazione e architettura

Le variabili `MAKEFLAGS`, `CFLAGS` e `CXXFLAGS` vengono usate da [make](https://www.archlinux.org/packages/?name=make), [gcc](https://www.archlinux.org/packages/?name=gcc), e `g++` mentre eseguono la compilazione del software con makepkg. Per impostazione predefinita, queste opzioni creano pacchetti generici che possono essere poi installati su una vasta gamma di macchine. Un miglioramento delle prestazioni può essere ottenuto mediante l'ottimizzazione della opzioni di compilazione per il computer host. Il rovescio della medaglia è che i pacchetti compilati appositamente per il processore host potrebbero non funzionare su altre macchine.

**Nota:** Tenere a mente che non tutti i sistemi di compilazione utilizzeranno le variabili esportate. Alcune di esse potrebbero essere sovrascritte nei Makefiles originali o nel [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").
 `/etc/makepkg.conf` 
```
...

#########################################################################
# ARCHITECTURE, COMPILE FLAGS
#########################################################################
#
CARCH="x86_64"
CHOST="x86_64-unknown-linux-gnu"

#-- Exclusive: will only run on x86_64
# -march (or -mcpu) builds exclusively for an architecture
# -mtune optimizes for an architecture, but builds for whole processor family
CFLAGS="-march=x86-64 -mtune=generic -O2 -pipe -fstack-protector --param=ssp-buffer-size=4 -D_FORTIFY_SOURCE=2"
CXXFLAGS="-march=x86-64 -mtune=generic -O2 -pipe -fstack-protector --param=ssp-buffer-size=4 -D_FORTIFY_SOURCE=2"
LDFLAGS="-Wl,-O1,--sort-common,--as-needed,-z,relro,--hash-style=gnu"
#-- Make Flags: change this for DistCC/SMP systems
#MAKEFLAGS="-j2"

...

```

I `CFLAGS` e i `CXXFLAGS` predefiniti di makepkg.conf sono compatibili con tutte le macchine e le loro rispettive architetture.

Su machcine x86_64, raramente ci sono vantaggi in termini di prestazioni che giustifichino il tempo di ricompilazione dei pacchetti ufficiali.

A partire dalla versione 4.3.0, GCC offre lo switch `-march=native` che abilita l'autorilevamento della CPU e seleziona automaticamente le ottimizzazioni supportate dalla macchina locale in fase di runtime GCC. Per utilizzarlo, è sufficiente modificare le impostazioni di default modificando le linee `CFLAGS` e `CXXFLAGS` come segue:

```
# -march=native also sets the correct -mtune=
CFLAGS="-march=native -O2 -pipe -fstack-protector --param=ssp-buffer-size=4 -D_FORTIFY_SOURCE=2"
CXXFLAGS="${CFLAGS}"

```

Le opzioni CFLAGS and CXXFLAGS di default su makepkg.conf, sono compatibili con tutte le macchine delle loro rispettive architetture.

Ulteriori ottimizzazioni per tipo di CPU, possono teoricamente migliorare le prestazioni `-march=` abilitando tutti i set di istruzioni disponibili e migliorando lo scheduling per particolari CPU. Ciò è evidente specialmente quando si creano pacchetti (ad esempio strumenti di codifica audio/video, applicazioni scientifiche, semplici programmi matematici, ecc..) che potrebbero sfruttare pesantemente i nuovi set di istruzioni, non abilitati quando si utilizzano le opzioni predefinite (o i pacchetti) forniti da Arch Linux.

E' molto facile ridurre le prestazioni utilizzando CFLAGS fuori standard, perchè GCC il più delle volte manderà in loop codice di grande dimensioni, vettorizzandolo in maniera errata, ecc.., a seconda delle opzioni del compilatore. Finchè non si verificherà/misurerà che qualcosa è più veloce, c'è una buona possibilità che non lo sia!

Vedere la pagina man di GCC per una lista completa delle opzioni disponibili. La[Compilation Optimization Guide](http://www.gentoo.org/doc/en/gcc-optimization.xml) di Gentoo e l'articolo wiki [Safe Cflags](http://wiki.gentoo.org/wiki/Safe_CFLAGS) forniscono informazioni più dettagliate.

#### MAKEFLAGS

L'opzione `MAKEFLAGS` può essere utilizzata per specificare delle opzioni aggiuntive a "make". Gli utenti con sistemi multi-core/multi-processore possono specificare il numero di operazioni da eseguire simultaneamente. Generalmente `-j2`, più 1 per ogni core/processore aggiuntivo, è una scelta ragionevole. Alcuni [PKGBUILD](/index.php/PKGBUILD_(Italiano) "PKGBUILD (Italiano)") sono specificatamente contraddistinti con `-j1`, richiesto da alcune versioni, o semplicemente perchè non supportati. I pacchetti che, a causa di questo, non si riescono a compilare, vanno [segnalati](/index.php/Reporting_bug_guidelines "Reporting bug guidelines") tramite il bug tracker, dopo essersi assicurati che l'errore non è causato dal proprio MAKEFLAGS.

Consultare [make(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/make.1) per un elenco completo delle opzioni disponibili.

### Output del pacchetto

Si può quindi impostare dove mettere i sorgenti ed i pacchetti per farli riconoscere dal packager. Questo passaggio è opzionale; i pacchetti verranno creati nella directory di lavoro dove makepkg viene eseguito di default.

 `/etc/makepkg.conf` 
```
...

#########################################################################
# PACKAGE OUTPUT
#########################################################################
#
# Default: put built package and cached source in build directory
#
#-- Destination: specify a fixed directory where all packages will be placed
#PKGDEST=/home/packages
#-- Source cache: specify a fixed directory where source files will be cached
#SRCDEST=/home/sources
#-- Source packages: specify a fixed directory where all src packages will be placed
#SRCPKGDEST=/home/srcpackages
#-- Packager: name/email of the person or organization building packages
#PACKAGER="John Doe <john@doe.com>"

...

```

Ad esempio, creare la directory:

```
$ mkdir /home/$USER/packages

```

Poi modificare di conseguenza la variabile `PKGDEST` in `/etc/makepkg.conf`.

La variabile `PACKAGER` imposterà il valore del `packager` all'interno del file metadata dei pacchetti compilati `.PKGINFO`. Per impostazione predefinita, i pacchetti compilati dagli utenti indicheranno:

 `pacman -Qi package` 
```
...
Packager       : Unknown Packager
...

```

Poi:

 `pacman -Qi package` 
```
...
Packager       : John Doe <john@doe.com>
...

```

Ciò è utile se più utenti compilano pacchetti su un sistema, o si stanno distribuendo i propri pacchetti ad altri utenti.

### Controllo firma

La procedura che segue non è necessaria per compilare con makepkg, per la configurazione iniziale procedere con [Utilizzo](#Usage_(Italiano)). Per disabilitare temporaneamente il controllo della firma, richiamare il comando di makpkg con l'opzione `--skippgpcheck`.

Se il file della firma con estensione .sig è parte dell'array sorgenti del [PKGBUILD](/index.php/PKGBUILD_(Italiano) "PKGBUILD (Italiano)"), makepkg valida l'autenticità dei file sorgente. Ad esempio, la firma pkgname-pkgver.tar.gz.sig è utilizzata per controllare l'integrità del file pkgname-pkgver.tar.gz con il programma gpg. Se si vuole, le firme di altri sviluppatori possono essere aggiunte manualmente al keyring gpg. Per maggiori informazioni vedere l'articolo [GnuPG](/index.php/GnuPG "GnuPG").

**Nota:** Il controllo della firma implementato in makepkg non utilizza il keyring di pacman. Per consentire a makepkg di leggere il keyring di pacman, configurare gpg come spiegato di seguito.

Le chiavi gpg dovrebbero essere memorizzate nel file utente `~/.gnupg/pubring.gpg`. Nel caso in cui non dovesse contenerle, makepkg mostrerà un avviso.

 `makepkg` 
```
...
==> Verifying source file signatures with gpg...
pkgname-pkgver.tar.gz ... FAILED (unknown public key 1234567890)
==> WARNING: Warnings have occurred while verifying the signatures.
    Please make sure you really trust them.
...

```

Per visualizzare la lista corrente delle chiavi gpg, utilizzare il comando gpg.

 `gpg --list-keys` 

Se il file pubring.gpg non esiste, esso verrà creato immediatamente.

E' possibile procedere con la configurazione di gpg per consentire la compilazione dei pacchetti AUR inviati dagli sviluppatori Arch Linux con la firma verificata con successo.

Aggiungere la seguente linea alla fine del file di configurazione gpg, per includere il keyring di pacman nel keyring personale utente.

 `~/.gnupg/gpg.conf` 
```
...
keyring /etc/pacman.d/gnupg/pubring.gpg

```

Una volta configurato come indicato, l'output di `gpg --list-keys` contiene una lista di chiavi e sviluppatori. Ora makepkg può compilare i pacchetti AUR inviati dagli sviluppatori Arch Linux con la firma verificata con successo.

## Utilizzo

Prima di continuare, assicurarsi che sia installato il gruppo di strumenti [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) siano installati. I pacchetti appartenenti a questo gruppo non sono tenuti ad essere elencati come dipendenze nei file [PKGBUILD](/index.php/PKGBUILD_(Italiano) "PKGBUILD (Italiano)"). Installare "base-devel" con il comando (da root):

```
# pacman -S base-devel

```

**Nota:** Prima di lamentarsi di eventuali mancanze di (make)dipendenze, ricordare che si assume che il gruppo di pacchetti [base](https://www.archlinux.org/packages/?name=base) sia correttamente installato sul sistema Arch Linux. Il gruppo "base-devel" è fondamentale per poter compilare e creare pacchetti con **makepkg**.

Per creare un pacchetto, si deve innanzitutto creare un [PKGBUILD](/index.php/PKGBUILD_(Italiano) "PKGBUILD (Italiano)"), o creare uno script, così come descritto in [Creating Packages](/index.php/Creating_packages_(Italiano) "Creating packages (Italiano)"), oppure ottenerne uno da [ABS](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)"), da [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)"), o da altre fonti.

**Attenzione:** Compilare e/o installare pacchetti solo da fonti sicure.

Una volta in possesso di un `PKGBUILD`, spostarsi nella cartella nel quale è posizionato e digitare il seguente comando per creare il pacchetto descritto nel `PKGBUILD` stesso:

```
$ makepkg

```

Per pulire makepkg da file e cartelle, come ad esempio i file estratti in $srcdir, aggiungere l'opzione che segue. Ciò è utile per molteplici compilazioni dello stesso pacchetto o per l'aggiornamento di versione, utilizzando la stessa cartella di compilazione. Esso impedisce che i file residui ed obsoleti vengano riportati nel nuovo processo di compilazione.

```
$ makepkg -c

```

Se non verranno rilevate tutte le dipendenze richieste, makepkg darà un avviso, prima di fallire la compilazione. Per compilare il pacchetto a installare automaticamente le dipendenze necessarie, utilizzare il comando:

```
$ makepkg -s

```

Si noti che queste dipendenze devono essere disponibili nei repository configurati; vedere [pacman#Repositories](/index.php/Pacman_(Italiano)#Repository "Pacman (Italiano)") per i dettagli. Altrimenti, si si possono installare manualmente le dipendenze prima della compilazione (`pacman -S --asdeps dep1 dep2`).

Quando tutte le dipendenze sono soddisfatte ed il pacchetto compilato correttamente, verrà creato, nella directory di lavoro, il file del pacchetto (`pkgname-pkgver.pkg.tar.gz`). Per installarlo, eseguire (da root):

```
# pacman -U pkgname-pkgver.pkg.tar.gz

```

In alternativa, un metodo più semplice è utilizzare il flag `-i`, anzichè `pacman -U pkgname-pkgver.pkg.tar.xz`, come riportato di seguito:

```
$ makepkg -i

```

## Trucchi e consigli

### Sostituzione automatica checksums nel PKGBUILD

#### Opzione 1

Di seguito uno script molto utile che genererà nuovi checksum per i file aggiornati e li sosituirà dentro il PKGBUILD in un'unica fase.

```
#!/bin/bash
# Script by Falconindy
# https://bbs.archlinux.org/viewtopic.php?id=131666

awk -v newsums="$(makepkg -g)" '
BEGIN {
  if (!newsums) exit 1
}

/^[[:blank:]]*(md|sha)[[:digit:]]+sums=/,/\)[[:blank:]]*$/ {
  if (!i) print newsums; i++
  next
}

1
' PKGBUILD > PKGBUILD.new && mv PKGBUILD{.new,}
```

#### Opzione 2

```
setconf PKGBUILD $(makepkg -g 2>/dev/null | pee "head -1 | cut -d= -f1" "cut -d= -f2") ')'

```

Questo funziona bene, ma ha lo svantaggio di richiedere il paccketto setconf (appena 364 KiB) e non funziona con sum multipli (ad esempio, sia md5sums che sha256sums nello stesso PKGBUILD).

La velocità è buona o migliore rispetto agli script che utilizzano awk, anche se makepkg viene chiamato due volte.

### ATTENZIONE: Il pacchetto contiene riferimenti a $srcdir

In qualche modo, le stringhe letterali `$srcdir` o `$pkgdir` sono finite in uno dei file installati nel pacchetto.

Per individuare tale file, eseguire il seguente comando nella cartella di compilazione del makepkg:

```
grep -R "$(pwd)/src" pkg/

```

[Link](http://www.mail-archive.com/arch-general@archlinux.org/msg15561.html) al thread della discussione.

## Altre risorse

*   [makepkg(8) Manual Page](https://www.archlinux.org/pacman/makepkg.8.html)
*   [makepkg.conf(5) Manual Page](https://www.archlinux.org/pacman/makepkg.conf.5.html)