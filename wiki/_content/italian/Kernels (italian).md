Articoli correlati

*   [Kernel modules (Italiano)](/index.php/Kernel_modules_(Italiano) "Kernel modules (Italiano)")
*   [Kernel Panics (Italiano)](/index.php/Kernel_Panics_(Italiano) "Kernel Panics (Italiano)")
*   [Linux-ck](/index.php/Linux-ck "Linux-ck")
*   [sysctl](/index.php/Sysctl "Sysctl")

Da [Wikipedia](https://en.wikipedia.org/wiki/Kernel_(computing) "wikipedia:Kernel (computing)"):

	*il kernel è la componente più importante del sistema operativo; è un ponte tra le applicazioni e l'elaborazione dei dati eseguita a livello hardware. Le responsabilità del kernel comprendono la gestione delle risorse del sistema (la comunicazione tra le componenti hardware e software).*

Esistono diversi kernel alternativi per Arch Linux oltre a quello principale. Questo articolo elenca alcune delle opzioni disponibili nei repository con una breve descrizione per ognuna. È anche presente una descrizione delle patch che possono essere applicate al kernel del sistema. L'articolo termina con una panoramica sulla compilazione dei kernel personalizzati con link ai vari metodi.

## Contents

*   [1 Kernel precompilati](#Kernel_precompilati)
    *   [1.1 Pacchetti ufficiali](#Pacchetti_ufficiali)
    *   [1.2 Pacchetti AUR](#Pacchetti_AUR)
*   [2 Patch e Patchset](#Patch_e_Patchset)
    *   [2.1 Come installare](#Come_installare)
    *   [2.2 Patchset principali](#Patchset_principali)
        *   [2.2.1 -ck](#-ck)
        *   [2.2.2 -rt](#-rt)
        *   [2.2.3 -bld](#-bld)
        *   [2.2.4 -grsecurity](#-grsecurity)
        *   [2.2.5 Tiny-Patch](#Tiny-Patch)
    *   [2.3 Patch individuali](#Patch_individuali)
        *   [2.3.1 Reiser4](#Reiser4)
        *   [2.3.2 Gensplash/fbsplash](#Gensplash.2Ffbsplash)
*   [3 Compilazione](#Compilazione)
    *   [3.1 Usare l'Arch Build System (consigliato)](#Usare_l.27Arch_Build_System_.28consigliato.29)
    *   [3.2 Tradizionale](#Tradizionale)
    *   [3.3 Driver proprietari NVIDIA](#Driver_proprietari_NVIDIA)
*   [4 Vedere anche](#Vedere_anche)

## Kernel precompilati

### Pacchetti ufficiali

	[linux](https://www.archlinux.org/packages/?name=linux)

	Il kernel Linux e i moduli dal repository [core]. Kernel vanilla con [tre patch](https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/linux&id=ef9aa5b9e58936788a9e65e364f00a3cf6497230) (dalla versione 3.1.3-1).

	[linux-lts](https://www.archlinux.org/packages/?name=linux-lts)

	Il kernel linux e i moduli supportati a lungo termine (LTS) dal repository [core].

### Pacchetti AUR

	[linux-bfs](https://aur.archlinux.org/packages/linux-bfs/)

	Il kernel Linux e i moduli con il [Brain Fuck Scheduler](https://en.wikipedia.org/wiki/Brain_Fuck_Scheduler "wikipedia:Brain Fuck Scheduler") (BFS) - creato da Con Kolivas per computer desktop con meno di 4096 cores, con scheduler I/O BFQ opzionale.

	[linux-ck](https://aur.archlinux.org/packages/linux-ck/)

	Il kernel Linux compilato con il patchset di Con Kolivas.

	Le opzioni aggiuntive che possono essere abilitate/disabilitate dal [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") includono: scheduler BFQ, nconfig, localmodconfig utilizzo del config del kernel in esecuzione.

	Queste sono patch progettate per migliorare la reattività del sistema con particolare enfasi nei desktop, ma adattabili a qualsiasi carico di lavoro. Le patch ck includono il BFS.

	Per ulteriori informazioni ed istruzioni per l'installazione, si prega di leggere l'articolo [linux-ck](/index.php/Linux-ck "Linux-ck").

	[linux-fbcondecor](https://aur.archlinux.org/packages/linux-fbcondecor/)

	Il kernel Linux e i moduli con supporto fbcondecor.

	[linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec)

	Il kernel Linux e i moduli con le patch grsecurity e PaX per una maggiore sicurezza.

	[linux-ice](https://aur.archlinux.org/packages/linux-ice/)

	Il kernel Linux e i moduli con il patchset dai sorgenti gentoo e il supporto TuxOnIce.

	[linux-lqx](https://aur.archlinux.org/packages/linux-lqx/)

	[Liquorix](http://liquorix.net) è una distribuzione kernel sostitutiva costruita usando la migliore configurazione e i migliori sorgenti kernel per utilizzo desktop, multimediale e ludico, spesso usato per ottenere migliori prestazioni su Debian Linux. damentz, il mantenitore del patchset Liquorix, è anche sviluppatore del patchset Zen, quindi molti di quei miglioramenti possono essere trovati in questo patchset.

	[linux-pax](https://aur.archlinux.org/packages/linux-pax/)

	Il kernel Linux e i moduli con le patch PaX per aumentare la sicurezza.

	[linux-pf](https://aur.archlinux.org/packages/linux-pf/)

	Il kernel linux e i moduli con il patchset del [pf-kernel](http://pf.natalenko.name/) [patchset -ck (incluso BFS), TuxOnIce, BFQ], aufs2 e squashfs-lzma.

	[linux-vanilla](https://aur.archlinux.org/packages/linux-vanilla/)

	Il kernel Linux vanilla e i moduli senza le patch di Arch Linux.

	[linux-aircrack](https://aur.archlinux.org/packages/linux-aircrack/)

	Il kernel Linux e gli header - patchato per rendere funzionante la suite [aircrack-ng](http://aircrack-ng.org/).

	[linux-zen](https://www.archlinux.org/packages/?name=linux-zen)

	Il [Kernel Zen](http://zen-kernel.org) è il risultato della colaborazione tra kernel hacker per fornire il miglior kernel Linux possibile per i sistemi attuali.

	[kernel-netbook](https://aur.archlinux.org/packages/kernel-netbook/)

	Kernel statico per netbook con Intel Atom N270/N280/N450/N550 come l'Eee PC con l'aggiunta di firmware ([broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl)) e patchset (BFS + TuxOnIce + BFQ optional) esterni - Solo GPU Intel

## Patch e Patchset

Ci sono diverse ragioni per patchare il proprio kernel, le principali riguardano le prestazioni o il supporto per caratteristiche secondarie come il supporto per il file system reiser4\. Altre ragioni possono essere il divertimento e il vedere come funziona e quali sono i miglioramenti.

Comunque è importante notare che il modo migliore per aumentare la velocità del sistema è innanzitutto quello di ottimizzare il kernel per il proprio sistema, specialmente per l'architettura e il tipo del processore. Per queste ragioni è sconsigliato utilizzare versioni pacchetti di kernel personalizzati già pronti con impostazioni per un'architettura generica. Un ulteriore miglioramento può essere il ridurre la grandezza dell'immagine del proprio kernel (e quindi il tempo di compilazione) escludendo il supporto per ciò che non si possiede o non si usa.

### Come installare

Il processo d'installazione dei pacchetti del kernel personalizzato si affida all'Arch Build System (ABS). Riguardo la creazione di pacchetti personalizzati, consultare i seguenti articoli: [Arch Build System (Italiano)](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)") e [Creating packages (Italiano)](/index.php/Creating_packages_(Italiano) "Creating packages (Italiano)").

Applicare patch o personalizzare un kernel non è così complicato come può apparire, ed esistono molti PKGBUILD nel forum per singoli patchset. In ogni caso, è raccomandato cominciare dalle basi facendo ricerche sui vantaggi di ogni patchset piuttosto che installare il primo che capita: in questo modo si acquisiranno molte più conoscenze sulle differenze tra i vari kernel.

Vedere [#Compilazione](#Compilazione).

### Patchset principali

Prima di tutto è importante notare che i patchset sono sviluppati da diverse persono. Alcuni sono fanno effettivamente parte della produzione del kernel Linux, altri sono hobbisti, il che può riflettere il loro livello di affidabilità e stabilità.

È anche importante notare che alcuni patchset sono costruiti dietro altri patchset (il può o meno influenzare la validità della patch). I patchset (e gli aggiornamenti del kernel) possono essere rilasciati **molto** frequentemente e spesso non vale la pena seguirli TUTTI per non impazzire, a meno che non diventi un hobby!

Si possono anche cercare altri patchset tramite google - ricordarsi di utilizzare le virgolette `"-nitro"` per esempio altrimenti google **NON** mostrerà deliberatamente i risultati voluti!

**Nota:** Questa sezione è **solo per informazione** - chiaramente in questa pagina non sono incluse garanzie di stabilità e affidabilità.

#### -ck

Queste sono patch progettate per migliorare la reattività del sistema, in particolar modo per i desktop, ma utilizzabile in ogni sistema. Le patch sono create e mantenute da Con Kolivas, il suo sito internet è [http://users.on.net/~ckolivas/kernel/](http://users.on.net/~ckolivas/kernel/). Con mantiene un set completo, ma fornisce anche singolarmente le patch così da poter aggiungere solo quelle desiderate.

Le patch -ck possono essere trovate su [http://ck.kolivas.org/patches/3.0/](http://ck.kolivas.org/patches/3.0/)

#### -rt

Questo patchset è mantenuto da un piccolo gruppo di sviluppatori core, con a capo Ingo Molnar. Questa patch permette a quasi tutto il kernel di essere prevaricato, ad eccezione di un parte molto piccola di codice ("raw_spinlock critical regions"). Ciò è ottenuto sostituendo la maggior parte degli spinlock con mutex che supportano l'eredità della priorità, ma anche spostando gli interrupt e i software interrupt nelle istanze del kernel.

Inoltre sono presenti timer ad alta risoluzione - un patchset, mantenuto indipendentemente.

[come scritto sulla [Real-Time Linux Wiki](http://rt.wiki.kernel.org/index.php/CONFIG_PREEMPT_RT_Patch)]

patch su [http://www.kernel.org/pub/linux/kernel/projects/rt/](http://www.kernel.org/pub/linux/kernel/projects/rt/)

#### -bld

BLD è meglio descritto come una tecnica di selezione CPU 0(1). Essa consiste nel riordinare le code di esecuzione in base ai carichi delle code. In altre parole, mantiene informato lo scheduler sui cambiamenti di carico, il che lo aiuta a tenere ordinate le code di esecuzione. Questa tecnica non dipende dal funzionamento dello scheduler. Le due cose più semplici in essa sono: tracciamento del carico e riordinamento delle code; le quali sono operazioni abbastanza semplici. Il tracciamento del carico viene eseguito ogni volta in cui avviene un cambiamento del carico di sistema e a seconda di questo cambiamento vengono riordinate le code di esecuzione. Lo scheduler può selezionare la coda più bassa senza dover calcolare e confrontare al momento di inserire un'attività in una coda. Cercando di distribuire il carico allo sched_exec e sched_fork, la scelta migliore è quella di prendere la coda del sistema meno occupata. In tal modo il sistema rimane bilanciato senza dover effettuare un bilanciamento del carico. Al momento del try_to_wake_up selezionare la coda meno attiva ha la massima priorità, ma viene effettuato secondo il dominio per utilizzare la cache della CPU in modo appropriato ed è il punto in cui si richiede una maggiore concentrazione.

Pagina di Google code: [http://code.google.com/p/bld/](http://code.google.com/p/bld/)

È disponibile solo la patch per la versione 3.3-rc3

**Attenzione:** Questo scheduler è in fase elevata di sviluppo.

#### -grsecurity

Grsecurity è un patchset per la sicurezza. Aggiunge numerose feature legate alla sicurezza come Role-Based Access Control e utilizza caratteristiche del progetto PaX. Può essere usato su desktop, ma si trae il maggior beneficio su un server pubblico. Alcune applicazioni sono incompatibili come le misure di sicurezza implementate da questo patchset. In questo caso, è consigliabile usare un livello di sicurezza più basso.

Le patch -grsecurity si trovano su at [http://grsecurity.net](http://grsecurity.net)

#### Tiny-Patch

Lo scopo di [Linux Tiny](http://elinux.org/Linux_Tiny) è di ridurre le tracce nella memoria e sul disco, così come aggiungere feature per permettere di lavorare su sistemi ridotti. Gli utenti designati sono sviluppatori di sistemi integrati e utenti di macchine ridotte o datate come le 386.

I rilasci della patch rispetto a quelli del kernel Linux sono discontinui. Gli sviluppatori hanno scelto di concentrarsi su alcune patch ed utilizzare il proprio tempo per cercare di unirle all'interno del kernel.

### Patch individuali

Queste sono patch che possono essere semplicemente incluse in ogni build del kernel vanilla o incorporate (magari insieme a modifiche maggiori) in altri patchset. Qui sono presenti alcune delle più comuni.

#### Reiser4

[Reiser4](/index.php/Reiser4 "Reiser4")

#### Gensplash/fbsplash

[Gensplash](/index.php/Fbsplash_(Italiano) "Fbsplash (Italiano)") - [http://dev.gentoo.org/~spock/projects/](http://dev.gentoo.org/~spock/projects/)

## Compilazione

Arch Linux fornisce metodi diversi per la compilazione del kernel.

### Usare l'Arch Build System (consigliato)

Usare l'[Arch Build System](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)") è consigliato per poter trarre vantaggio dall'alta qualità del [PKGBUILD](/index.php/PKGBUILD_(Italiano) "PKGBUILD (Italiano)") [linux](https://www.archlinux.org/packages/?name=linux) esistente ed avere i benefici della [sistema di gestione dei pacchetti](https://en.wikipedia.org/wiki/Sistema_di_gestione_dei_pacchetti "wikipedia:Sistema di gestione dei pacchetti"). Il PKGBUILD è strutturato in modo da poter fermare la compilazione appena i sorgenti sono stati scaricati e configurare il kernel.

Vedere [Kernels/Arch Build System (Italiano)](/index.php/Kernels/Arch_Build_System_(Italiano) "Kernels/Arch Build System (Italiano)").

### Tradizionale

Alternativamente è possibile compilare un kernel senza l'[Arch Build System](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)") (metodo tradizionale). Questo metodo comporta lo scaricamento manuale della tarball dei sorgenti e la compilazione nella propria cartella home come normale utente. Una volta configurato, vengono offerti due metodi di compilazione/installazione: quello tradizionale e quello con makepkg/pacman.

Un vantaggio del metodo tradizionale è che funziona su altre distribuzioni Linux.

Vedere [Kernels/Compilation/Traditional](/index.php/Kernels/Compilation/Traditional "Kernels/Compilation/Traditional").

È disponibile uno script che automatizza il metodo non-[Arch Build System](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)"). Vedere [Kernels/Compilation/Script](/index.php/Kernels/Compilation/Script "Kernels/Compilation/Script").

### Driver proprietari NVIDIA

Consultare [NVIDIA (Italiano)#Installazione alternativa: kernel personalizzato](/index.php/NVIDIA_(Italiano)#Installazione_alternativa:_kernel_personalizzato "NVIDIA (Italiano)") per istruzioni riguardo l'utilizzo dei driver proprietari NVIDIA con un kernel personalizzato

## Vedere anche

*   [O'Reilly - Linux Kernel in a Nutshell](http://www.kroah.com/lkn/) (free ebook)