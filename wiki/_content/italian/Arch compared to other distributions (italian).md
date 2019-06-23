Questa pagina raccoglie alcune delle somiglianze e delle differenze tra Arch e le altre distribuzioni GNU/Linux.
Nota: il modo migliore per confrontare Arch con le altre distribuzioni è quello di installarla e provarla in prima persona. Arch ha una magnifica comunità di utenti sempre pronta ad aiutare i nuovi arrivati. Le informazioni qui sotto sono pensate per aiutarti a decidere se Arch sia giusta per te.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Source-Based](#Source-Based)
    *   [1.1 Arch vs Gentoo](#Arch_vs_Gentoo)
    *   [1.2 Arch vs Sorcerer/Lunar-linux/Sourcemage](#Arch_vs_Sorcerer/Lunar-linux/Sourcemage)
*   [2 Minimali](#Minimali)
    *   [2.1 Arch vs LFS](#Arch_vs_LFS)
    *   [2.2 Arch vs CRUX](#Arch_vs_CRUX)
    *   [2.3 Arch vs Slackware](#Arch_vs_Slackware)
*   [3 Distribuzioni Grafiche](#Distribuzioni_Grafiche)
    *   [3.1 Arch vs Ubuntu](#Arch_vs_Ubuntu)
    *   [3.2 Arch vs Fedora](#Arch_vs_Fedora)
    *   [3.3 Arch vs Mandriva](#Arch_vs_Mandriva)
    *   [3.4 Arch vs SUSE](#Arch_vs_SUSE)
    *   [3.5 Arch vs PCLinuxOS](#Arch_vs_PCLinuxOS)
*   [4 I *BSD](#I_*BSD)
    *   [4.1 Arch vs FreeBSD](#Arch_vs_FreeBSD)
    *   [4.2 Arch vs NetBSD](#Arch_vs_NetBSD)
    *   [4.3 Arch vs OpenBSD](#Arch_vs_OpenBSD)
*   [5 Altre](#Altre)
    *   [5.1 Arch vs Debian GNU/Linux](#Arch_vs_Debian_GNU/Linux)
    *   [5.2 Arch vs Frugalware](#Arch_vs_Frugalware)

# Source-Based

Le distribuzioni basate su sorgenti sono altamente portabili, hanno il vantaggio di controllare e compilare l'intero SO e i pacchetti secondo una particolare architettura del processore e secondo le modalità d'uso del sistema, hanno però lo svantaggio di richiedere molto tempo in fase di compilazione. Arch e tutti i pacchetti sono ottimizzati per le architetture i686 e x86-64, offrendo un significativo incremento di prestazioni rispetto alle distribuzioni basate su pacchetti i386/i486/i586 binari, con il vantaggio di installazioni rapide.

## Arch vs Gentoo

Siccome Arch distribuisce pacchetti binari, richiede molto meno tempo rispetto a Gentoo. Sia Gentoo che Arch dispongono di pacchetti binari e sorgenti così come funzioni 'makeworld'; tuttavia, Gentoo è basata su sorgenti mentre Arch su pacchetti binari. Entrambe sono sistemi 'rolling-release'. I PKGBUILD di Arch sono notoriamente percepiti più semplici e veloci da creare rispetto agli ebuild di Gentoo. Gentoo supporta architetture x86, ppc, sparc, alpha, amd64, mips, hppa e itanium, Arch solo i686 e x86-64\. Arch è progettata secondo un approccio orientato alla semplicità ed al minimalismo, Gentoo invece si propone di controllare ogni singolo aspetto della compilazione di sorgenti. Entrambe le distribuzioni permettono un alto grado di manipolazione, di conseguenza, gli utenti Gentoo si sentiranno particolarmente ad agio con molti aspetti di Arch.

## Arch vs Sorcerer/Lunar-linux/Sourcemage

Sorcerer/Lunar-linux/Sourcemage (SLS) sono tutte distribuzioni basate su sorgenti, proprio come Gentoo, ma sono collegate originariamente ad un'altra. La distro SLS usa un insieme di script piuttosto semplici da utilizzare per creare pacchetti e descrizioni, e usa un file di configurazione globale per configurare il processo di compilazione, in modo molto simile al sistema ABS di Arch. I tool di SLS garantiscono un pieno controllo delle dipendenze (compresa la gestione di caratteristiche opzionali), e il monitoraggio dei pacchetti (e disinstallazione/aggiornamento). Non ci sono pacchetti binari per una qualsiasi distro appartenente alla famiglia SLS, anche se tutti possono facilmente effettuare un rollback a pacchetti installati precedentemente.

L'installazione implica l'installazione di un sistema di base (un po' come Arch: ottimizzazione i686, CLI e menu ncurses, solo strumenti essenziali), quindi successivamente una ricompilazione del sistema di base (opzionale). Non c'è ovviamente uno 'standard' WM/DE/DM e non installano un server X durante l'installazione di base, ma permettono di installare in modo semplice una delle diverse alternative disponibili per un server X (xorg 6.8 oppure 7, xfree86).

SLS ha una storia davvero complicata. Il migliore articolo che ne parli lo si può trovare qui: [http://wiki.sourcemage.org/Our_History](http://wiki.sourcemage.org/Our_History)

Lunar Linux: [http://lunar-linux.org/](http://lunar-linux.org/)
SourceMage: [http://www.sourcemage.org/](http://www.sourcemage.org/)
Sorcerer: [http://sorcerer.berlios.de/](http://sorcerer.berlios.de/)

# Minimali

Le distribuzioni minimali sono altamente comparabili con Arch, condividendone diverse somiglianze. Tutte possono essere considerate 'semplici' da un punto di vista tecnico.

## Arch vs LFS

LFS, o Linux From Scratch, è semplicemente questo; un insieme di applicazioni base per un sistema funzionale GNU/Linux, compilato manualmente e configurato da zero. LFS è quanto di più minimale ci possa essere, offre un modo eccellente ed educativo di sviluppare un sistema basilare. Arch propone gli stessi pacchetti di base, più la gestione degli init stile BSD, alcuni strumenti extra ed il potente gestore di pacchetti pacman come sistema iniziale, già compilati per i686/x86-64\. LFS non dispone di repository online; i sorgenti vanno ottenuti manualmente, compilati ed installati tramite make (Esistono diversi metodi manuali per la gestione dei pacchetti che sono menzionati su LFS Hints). Oltre al minimale sistema iniziale, gli sviluppatori di Arch e la sua community distribuiscono migliaia di pacchetti binari installabili tramite pacman, così come gli script PKGBUILD da usare con ABS - the Arch (source) Build System. Arch include inoltre lo strumento makepkg per compilare o manipolare i pacchetti .pkg.tar.gz, che possono essere prontamente installati via pacman. Judd Vinet ha sviluppato Arch "from scratch", e ha scritto pacman in C. Alcune volte Arch, infatti, è semplicemente descritto come "Linux, with a nice package manager."

## Arch vs CRUX

*   Q: Arch è Basata su CRUX?
*   A: No. Arch è sviluppata indipendentemente, è stato costruito da zero e non si basa su nessun'altra distribuzione GNU/Linux.

Prima di creare Arch, Judd Vinet ha ammirato ed utilizzato CRUX, una distribuzione minimale, creata da Per Lidén. Originariamente ispirate da idee in comune con CRUX, Arch è stata costruita da zero, e poi pacman è stato codificato in C. Entrambe condividono alcuni principi guida; ad esempio, tutte e due sono ottimizzate per alcune architetture, minimali e K.I.S.S. Entrambe dispongono di sistemi 'ports-like', gestiscono il sistema init stile *BSD e, come *BSD, forniscono una base minimale su cui sviluppare il sistema operativo. Arch propone pacman, il quale gestisce i pacchetti binari e lavora in simbiosi con ABS, il sistema 'ports-like' di Arch. CRUX fa uso di prt-get, al quale contribuisce la community, in combinazione con il proprio sistema 'port', che risolve le dipendenze ma compila pacchetti sorgenti (anche se l'installazione base di CRUX avviene tramite pacchetti binari i686). Arch supporta ufficialmente i686 e x86-64, mentre CRUX solo i686\. Arch è di tipo 'rolling release' e fornisce un grande insieme di 'repository' di pacchetti binari così come AUR. CRUX fornisce un ridotto numero di applicazioni supportate in aggiunta a modesti 'repository' gestiti dalla community.

## Arch vs Slackware

Slackware e Arch sono molto simili per il fatto che entrambe sono distribuzioni semplici orientate all'eleganza ed al minimalismo. Slackware è famosa per la sua mancanza di 'branding' e pacchetti 'vanilla', a partire dal kernel. Arch tipicamente applica patch solo per ovviare a seri problemi e per preservare la funzionalità, quindi solo se strettamente necessario. Entrambe usano gli script init stile *BSD. Arch dispone del gestore di pacchetti pacman che, al contrario degli strumenti standard di Slackware, risolve automaticamente le dipendenze e permette di aggiornare il sistema in maniera automatica. Gli utenti Slackware tipicamente preferiscono il loro metodo manuale di risoluzione delle dipendenze, poiché garantisce loro un certo grado di controllo. Arch è 'rolling-release'. Slackware è molto rigida nelle fasi di rilascio software, preferendo una collaudata stabilità dei suoi pacchetti. Arch è 'bleeding edge' in questo aspetto. Arch offre [ABS](/index.php/ABS "ABS"), un sistema 'ports-like'. Slackbuild (non ufficiale) ha caratteristiche simili a [AUR](/index.php/AUR "AUR") di Arch. Gli utenti Slackware si sentiranno particolarmente ad agio con molti aspetti di Arch.

# Distribuzioni Grafiche

Alcune volte chiamate distro "newbie", le distribuzioni grafiche hanno molte somiglianze tra loro, mentre Arch è piuttosto differente. Arch può essere una scelta migliore se si vogliono imparare i vari aspetti di GNU/Linux sviluppando un sistema partendo da una base minimale, infatti inizialmente Arch installa veramente pochi pacchetti. Le distribuzioni grafiche di solito affidano l'installazione ad una interfaccia grafica (come Anaconda per Fedora) così come la configurazione (YaST di SuSe). Le differenze specifiche sono indicate di seguito.

## Arch vs Ubuntu

Ubuntu è una distribuzione immensamente popolare basata su Debian e sponsorizzata da Canonical Ltd., mentre Arch è sviluppata da zero come progetto indipendente. Se ti piace compilare il kernel, provare applicazioni alle ultime versioni così come progetti CVS, o di tanto in tanto compilare un programma da sorgente, Arch è la scelta migliore. Se preferisci un sistema funzionante alla svelta e non sei molto interessato alle dinamiche del sistema, Ubuntu è la scelta migliore. Arch si presenta come un progetto molto più minimale dall'installazione iniziale in poi, lasciando all'utente la possibilità di modificare il proprio sistema secondo le proprie esigenze. In generale, sviluppatori ed utenti impegnati preferiranno probabilmente Arch ad Ubuntu, anche se alcuni utenti di Arch dichiarano di aver cominciato con Ubuntu per poi cambiare. Ubuntu rilascia una nuova versione ogni 6 mesi circa, Arch è di tipo 'rolling-release'. Arch offre un sistema 'ports-like' per la compilazione di sorgenti, ABS, Ubuntu no. Anche le community differiscono in alcuni aspetti. La community di Arch è molto più piccola ed è fortemente incoraggiata ad essere attiva; una grande percentuale contribuisce allo sviluppo. Al contrario, la community di Ubuntu è molto vasta e può permettere alla maggioranza di utenti di non contribuire allo sviluppo del sistema, dei pacchetti o alla gestione dei 'repository'.

## Arch vs Fedora

Fedora è una costola della distribuzione Red Hat ed è stata nel tempo una delle distribuzioni più note. Pertanto, c'è una enorme comunità, molti pacchetti precompilati e supporto disponibile. I pacchetti di Fedora son del tipo RPM, ed usa YUM come gestore. Arch usa pacman per gestire i pacchetti .tar.gz. Notoriamente Fedora non supporta il formato mp3 a causa di problemi di licenze. Arch è più permissiva rispetto al formato mp3 e ad altri formati multimediali. Fedora fornisce di default una 'gui' per l'installazione. Arch non offre un interfaccia grafica per l'installazione, ma piuttosto, un interfaccia basata su 'ncurses', permettendo all'utente un certo grado di configurazione. Fedora rilascia nuove versioni ciclicamente. Arch è 'rolling-release'. Arch è progettata secondo un approccio mirato all'eleganza ed al minimalismo piuttosto che all'autoconfigurazione. Fedora si è recentemente rinnovata integrando SELinux ed i pacchetti compilati GCJ così da eliminare la necessità di JRE della Sun. Fedora non supporta né JFS né ReiserFS 'out of the box'.

## Arch vs Mandriva

Mandriva (precedentemente Mandrake), fu creata nel 1998 con l'obiettivo di rendere GNU/Linux facile per tutti. È basata su pacchetti RPM ed usa il gestore urpmi. Ancora, Arch predilige un approccio più semplice, essendo basata su linea di comando e permettendo un certo grado di configurazione. Arch è mirata all'utente intermedio ed avanzato.

## Arch vs SUSE

SUSE è centrata attorno al suo tool di configurazione Yast, il quale è sufficiente per le esigenze di configurazione della maggior parte degli utenti. Arch non offre un tool così funzionale perché non rispetterebbe [Il Metodo Arch](/index.php/Il_Metodo_Arch "Il Metodo Arch"). Tuttavia SUSE è considerata una distribuzione più appropriata per gli utenti con meno esperienza, o per coloro che vogliono un sistema più orientato all'interfaccia grafica, autoconfigurazione e funzionalità 'out of the box'.

## Arch vs PCLinuxOS

PCLinuxOS è una popolare distribuzione basata su Mandriva che propone un completo DE, progettata per semplicità e facilità d'uso, anche se questa definizione di semplicità è molto lontana da quella di Arch. Arch è progettata come sistema di base semplice per poi essere modificata dal basso verso l'alto e mirata ad utenti intermedi/avanzati. PCLOS usa il gestore di pacchetti apt come 'wrapper' per gli RPM. Arch usa pacman, un gestore di pacchetti .tar.gz sviluppato indipendentemente. PCLOS è molto orientata alle interfacce grafiche, dispone di 'gui' per la configurazione dell'hardware e del gestore di pacchetti Synaptic come 'front end', e dichiara di essere minimamente assoggettata alla linea di comando. Arch è orientata alla 'shell' e progettata per un approccio più semplice alla configurazione di sistema, gestione e manutenzione. PCLOS raccomanda 256MB di memoria RAM relativamente alla parte dei requisiti di sistema. Essendo più leggera, Arch può essere installata su sistemi con molta memoria in meno, richiedendo solo 64MB di RAM per una installazione di base i686, di conseguenza può essere installata senza problemi su sistemi moderni.

# I *BSD

Sia Arch che *BSD offrono una forte base integrata e sistemi 'port' in combinazione con la disponibilità di pacchetti binari. I BSD derivano dalla Berkeley UNIX. Perciò, *BSD non sono distribuzioni GNU/Linux, ma piuttosto, sistemi operativi 'UNIX-like'.

## Arch vs FreeBSD

Sia Arch che [FreeBSD](http://www.freebsd.org/about.html) offrono software ottenibile in forma binaria compilabile con un sistema di 'port'. Entrambi condividono un sistema init molto simile. FreeBSD vanta ciò che può essere considerato un sistema concepito globalmente, confrontato con le varie distribuzioni GNU/Linux, con ogni applicazione 'port-ata' su FreeBSD e verificata per il suo funzionamento. Da questo punto di vista Arch è invece focalizzata più sul rilascio di software di ultima generazione. Entrambi usano /etc/rc.conf come file di configurazione principale. La licenza di FreeBSD è più stile facci-quello-che-vuoi apprezzata da molti utenti GNU/Linux. Arch è invece rilasciata sotto la GPL. In FreeBSD, come in Arch, le decisioni sono lasciate all'utente esperto. Questo è il confronto più significativo rispetto ad Arch dato che sono paragonabili sia per quanto riguarda la modernità del sistema di pacchetti che per tipo di comunità. Entrambi i sistemi condividono molte similitudini e gli utenti FreeBSD si trovano generalmente a loro agio con Arch.

## Arch vs NetBSD

NetBSD è un SO UNIX-like libero, sicuro e altamente portabile, disponibile per oltre 50 piattaforme, da macchine Opteron 64-bit e sistemi desktop fino a dispositivi 'embeded'. Il suo disegno chiaro e le sue caratteristiche avanzate fanno di NetBSD un prodotto eccellente sia per sistemi di produzioni che di ricerca. Molte applicazioni sono disponibili attraverso pgsrc, la collezione di pacchetti di NetBSD. Arch può non operare sulla vastità di dispositivi sui quali opera NetBSD, ma per un sistema i686/x86-64 può offrire anche un maggior numero di applicazioni. Inoltre, il metodo di installazione di default di pkgsrc è quello di ottenere e compilare sorgenti, mentre Arch offre pacchetti binari. Arch condivide molte somiglianze con NetBSD; entrambi usano /etc/rc.conf come file di configurazione principale, sono minimali e leggeri, offrono sistemi 'port' così come binari ed entrambi hanno sviluppatori e community attive. Il sistema init di Arch è ispirato a quello dei *BSD.

## Arch vs OpenBSD

Il progetto OpenBSD fornisce un SO UNIX-like libero, multi-piattaforma '4.4BSD-based'. Lo sviluppo è concentrato sulla portabilità, standardizzazione, correttezza del codice, sicurezza e crittografia integrata. Al contrario, Arch mira più alla semplicità, eleganza, minimalismo e 'bleeding-edge' software. OpenBSD supporta l'emulazione binaria della maggioranza dei programmi di SVR4 (Solaris), FreeBSD, GNU/Linux, BSD/OS, SunOS e HP-UX. OpenBSD è forse il numero 1 per quanto concerne la sicurezza. In comune con Arch, OpenBSD offre una piccola ed elegante installazione di base e usa un sistema 'port' e 'packaging' per permettere una facile installazione e gestione dei programmi non facenti parte del sistema operativo di base. In contrasto con sistemi GNU/Linux quali Arch, ma in comune con altri sistemi operativi BSD, il kernel di OpenBSD e programmi per gli utenti, come la 'shell' e altri strumenti (come ls, cp, cat e ps), sono distribuiti in un singolo 'repository' sorgente.

# Altre

Queste distribuzioni rientrano nella categoria 'altre'.

## Arch vs Debian GNU/Linux

Debian è un progetto molto vasto, così come la community, offre oltre 20,000 pacchetti binari divisi nelle branche Stable, Testing e Unstable. Arch non divide i suoi pacchetti in -dev e -common come Debian, come conseguenza, i repository di Arch sembreranno più piccoli. Debian ha una forte posizione sul software libero. Arch è più permissiva riguardo i pacchetti 'non-free' come definiti da GNU. Debian è progettata secondo un approccio mirato alla stabilità e al testing. Arch si concentra sulla semplicità, minimalismo ed offre software 'bleeding-edge'. I pacchetti distribuiti da Arch sono più recenti dei Debian Stable e Testing, tipicamente sono circa uguali ai Debian Unstable. Sia Arch che Debian offrono un ottimo sistema per la gestione dei pacchetti. Arch è di tipo 'rolling-release', mentre Debian è rilasciata con pacchetti "congelati". Debian è disponibile per molte architetture, include alpha, arm, hppa, i386, x86_64, ia64, m68k, mips, mipsel, powerpc, s390, e sparc, mentre Arch supporta solo i686 e x86-64\. Arch dispone di un rapido supporto per compilare, modificare ed installare pacchetti da sorgenti esterne, con un sistema 'port-like' quale ABS. Debian non offre un sistema 'port', certo sono presenti anche gli stessi pachetti binari anche in formato sorgente, ma di base si affida alla enorme quantità di repository binari. L'installazione iniziale di Arch propone un sistema base minimale, esposto in maniera trasparente durante la configurazione del sistema, Debian invece prevede più autoconfigurazione così come diversi metodi di installazione alternativi.

## Arch vs Frugalware

Arch è 'text-based' e orientata alla linea di comando; Frugalware ha adottato pacman di Arch come gestore di pacchetti, ma usa 'bzipped-tarballs'. Arch, invece, usa 'gzipped-tarballs', con lo scopo di velocizzare l'installazione. Frugalware di default non supporta il file system JFS. Frugalware non è più basata su Slackware ma piuttosto una distribuzione indipendente, è ottimizzata per i686. Arch è fondamentalmente un sistema differente, l'installazione iniziale fornisce un sistema di base con pacman in aggiunta alle scelte ed alle necessità dell'utente. Frugalware è installata tramite DVD con applicazioni e sistemi desktop di default. Frugalware è rilasciata ciclicamente. Arch è di tipo 'rolling-release'.