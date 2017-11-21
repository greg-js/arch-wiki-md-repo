Arch Linux è una distribuzione GNU/Linux indipendente, sviluppata per un uso general-purpose, rilasciata per l'architettura [x86-64](https://en.wikipedia.org/wiki/it:x86-64 "wikipedia:it:x86-64"). La versione dei pacchetti disponibili per Arch Linux tende ad essere sempre l'ultima stabile possibile. Il modello di sviluppo seguito e` il rolling release. L'installazione di default e` molto minimale, sara` poi l'utente a decidere come dovra` prendere forma il proprio sistema.

## Contents

*   [1 Pricipi](#Pricipi)
    *   [1.1 Semplicita`](#Semplicita.60)
    *   [1.2 Modernita`](#Modernita.60)
    *   [1.3 Pragmatismo](#Pragmatismo)
    *   [1.4 Centralita` dell'utente](#Centralita.60_dell.27utente)
    *   [1.5 Versatilita`](#Versatilita.60)
*   [2 Storia](#Storia)
    *   [2.1 I primi anni](#I_primi_anni)
    *   [2.2 Gli anni di mezzo](#Gli_anni_di_mezzo)
    *   [2.3 Nascita di ArchWiki](#Nascita_di_ArchWiki)
    *   [2.4 L'era di Griffin](#L.27era_di_Griffin)
    *   [2.5 Arch Install Script](#Arch_Install_Script)
    *   [2.6 L'era di Systemd](#L.27era_di_Systemd)
    *   [2.7 Fine del supporto a i686](#Fine_del_supporto_a_i686)

## Pricipi

### Semplicita`

Il concetto di semplicita` a cui si fa riferimento e` *senza aggiunte o modifiche*. Arch Linux rilascia i software come gli sviluppatori originari in [upstream](https://en.wikipedia.org/wiki/Upstream_(software_development)) li hanno pensati. I cambiamenti in downstream sono ridotti all'osso.

Anche le configurazioni di default sono quelle previste dagli sviluppatori in upstream, le eventuali modifiche specifiche della distribuzione sono minime e solitamente si tratta solo di modificare i percorsi dei file di sistema. Non vengono forniti automatismi di nessun genere, ad esempio non viene avviato nessun servizio a seguito dell'installazione di un determinato pacchetto. Alcuni pacchetti vengono *splittati* con il principale scopo di non sprecare troppo spazio su disco. Interfacce grafiche di configurazione non sono ufficialmente fornite (in downstream), gli utenti infatti sono incoraggiati a configurare tramite shell ed editor testuali.

### Modernita`

Arch Linux mantiene nei propri repository solo l'ultima versione stabile di ogni pacchetto. Il sistema di rilascio scelto e` *rolling release* che prevede una sola installazione con continui aggiornamenti.

Arch Linux incorpora tutte le nuove caratteristiche disponibili per ogni utente GNU/Linux, come il sistema di init [systemd](/index.php/Systemd "Systemd"), moderni [file system](/index.php/File_system "File system"), LVM2, software RAID, il tutto supportato dall'ultima versione disponibile del kernel.

### Pragmatismo

Arch Linux prima di essere una distribuzione ideologica e` pragmatica. I principi qui presentati sono solo utili linee guide. Infatti ogni decisione riguardante la pacchettizzazione e` presa caso per caso e con il consenso di piu` sviluppatori. Le analisi tecniche svolte e la discussione sono alla base delle scelte, questo ha la precedenza su politica o opinioni popolari.

Il grande numero dei pacchetti disponibili nei repository ufficiali sono sia open source sia closed in modo che sia l'utente a scegliere quale usare.

### Centralita` dell'utente

Arch Linux e` *user-centric* a differenza di molte altre distribuzioni che sono *user-friendly*. Questa distribuzione e` pensata per coprire le necessita` di chi contribuisce, cercare di aumentare il numero di utenti non e` lo scopo di Arch Linux. Il normale target di utenza e` quello di utenti GNU/Linux avanzati o chiunque abbia una buona attitudine al DIY, alla lettura e alla comprensione della documentazione.

Ogni utente e` incoraggiato a [partecipare](/index.php/Getting_involved "Getting involved") e contribuire alla distribuzione. Ogni aiuto a riportare e risolvere [bug](https://bugs.archlinux.org/) o sviluppare il core [project](https://projects.archlinux.org/) e` apprezzato. Gli sviluppatori di Arch Linux sono volontari e spesso i contributori piu` attivi si ritrovano a diventare parte del team. Gli *archer* possono liberamente contribuire grazie ad [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"), possono contribuire alla [documentazione](/index.php/Main_page "Main page"), partecipare a [forum](https://www.archlinux.it/forum/index.php), mailing list o [canali IRC](/index.php/IRC_Channels "IRC Channels"). Arch Linux e` un sistema operativo globale, usato da molti utente sparsi in tutto il mondo, esistono molte [community internazionali](/index.php/International_communities "International communities") che offrono aiuto e documentazione localizzata.

### Versatilita`

Arch Linux e` general-purpose. Dall'installazione solo l'interfaccia a riga di comando e` disponibile. Invece di fornire molti pacchetti da subito, Arch Linux lascia all'utente la possibilita` di decidere quali pacchetti installare. I [repository](/index.php/Official_repositories "Official repositories") di Arch Linux contengono migliaia di pacchett compilati i per l'architettura [x86-64](https://en.wikipedia.org/wiki/x86-64). Il supporto a [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture)) e` cessato a novembre 2017.

Arch Linux usa come package manager [pacman](/index.php/Pacman "Pacman"), un programma leggero, funzionale e potente, il quale permette di aggiornare tutto il sistema con un solo comando. Arch Linux fornisce anche [Arch Build System](/index.php/Arch_Build_System "Arch Build System"), un sistema *port-like* per aiutare nella ricompilazione da sorgente dei vari pacchetti, il quale puo` essere sincronizzato con un solo comando. In piu`, l' *Arch User Repository* contiene migliaia di [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") supportati dalla comunita`, per poter compilare grazie a [makepkg](/index.php/Makepkg "Makepkg") le applicazioni non presenti nei repository. E` anche possibile mantenere facilmente un proprio repository personalizzato.

## Storia

### I primi anni

Arch Linux è stata fondata dal programmatore canadese Judd Vinet. Il suo primo rilascio formale, Arch Linux 0.1, avvenne l'11 marzo 2002\. Anche se Arch è completamente indipendente, trae ispirazione dalla semplicità di altre distribuzioni, tra cui [Slackware](http://slackware.com), [CRUX](http://www.crux.nu) e [BSD](https://en.wikipedia.org/wiki/Berkeley_Software_Distribution "wikipedia:Berkeley Software Distribution"). Judd inizio` anche a sviluppare un programma, chiamato [pacman](/index.php/Pacman "Pacman") in grado di gestire installazione, rimozione e aggiornamento dei pacchetti.

### Gli anni di mezzo

La crescita della comunita` di Arch Linux tra 2002 e 2011 e` stata costante, come si vede da [questo](https://wiki.archlinux.org/images/8/8d/Archstats2002-2011.png) grafico riguardante il numero di post sui forum e ai bug report.

### Nascita di ArchWiki

L'8 luglio 2005 nasce [ArchWiki](/index.php/ArchWiki:About#History "ArchWiki:About") su piattaforma MediaWiki.

### L'era di Griffin

Nel 2007, Judd Vinet decide di abbandonare il progetto, lasciando le redini a [Aaron Griffin](https://bbs.archlinux.org/viewtopic.php?id=38024), conosciuto sul web come Phrakture, il quale e` leader di Arch Linux tuttora.

Nel corso degli anni la comunita` ha continuato a crescere e maturare ricevendo anche una discreta [notorieta`](/index.php/Arch_Linux_Press_Review "Arch Linux Press Review").

Gli sviluppatori di Arch Linux rimangono comunque volontari non pagati. Non ci sono prospettive di monetizzare in futuro quindi Arch e` *free* in ogni senso. I piu` curiosi sulla storia dello sviluppo di Arch Linux potranno visitare: [Arch entry in the Internet Archive Wayback Machine](http://web.archive.org/web/*/archlinux.org) e [News Archives](https://www.archlinux.org/news/).

### Arch Install Script

Il 15 luglio 2012 viene rilasciata la prima iso senza lo storico [installer](https://www.archlinux.org/news/install-media-20120715-released/) a menu testuale in favore degli Arch Install Scripts.

### L'era di Systemd

Tra il 2012 e il 2013 il tradizionale sistema di init System V viene deprecato in favore di Systemd. [https://www.archlinux.org/news/install-medium-20121006-introduces-systemd/](https://www.archlinux.org/news/install-medium-20121006-introduces-systemd/)][[1]](https://www.archlinux.org/news/systemd-is-now-the-default-on-new-installations/)[[2]](https://www.archlinux.org/news/end-of-initscripts-support/)[[3]](https://www.archlinux.org/news/final-sysvinit-deprecation-warning/)

### Fine del supporto a i686

Il 25 gennaio 2017 viene [annunciato](https://www.archlinux.org/news/phasing-out-i686-support/) che il supporto all'architettura i686 finira` per via del sempre minor interesse di community e sviluppatori.