Arch Linux è una distribuzione indipendente sviluppata per [i686](https://en.wikipedia.org/wiki/it:i686 "wikipedia:it:i686")/[x86-64](https://en.wikipedia.org/wiki/it:x86-64 "wikipedia:it:x86-64"), abbastanza versatile ed adatta ad ogni ruolo. Il suo sviluppo si concentra sulla semplicità, il minimalismo e l'eleganza del codice. Arch è installato come sistema di base minimale (configurato dall'utente) sul quale viene costruito il proprio ambiente ideale, installando solo ciò che è necessario in base alle proprie necessità. Le GUI delle utility di configurazione non sono fornite ufficialmente e la maggior parte della configurazione del sistema viene eseguita dalla Shell e da un editor di testo. Basata sul modello rolling-release, Arch si sforza di rimanere all'avanguardia, e di solito offre le ultime versioni stabili della maggior parte dei software.

## Contents

*   [1 Storia](#Storia)
*   [2 Semplicità](#Semplicit.C3.A0)
*   [3 Modernità](#Modernit.C3.A0)
*   [4 Gestore Pacchetti](#Gestore_Pacchetti)
*   [5 Integrità Sorgenti](#Integrit.C3.A0_Sorgenti)
*   [6 Comunità](#Comunit.C3.A0)
*   [7 Sommario](#Sommario)

## Storia

	*Articolo principale: [Storia di Arch Linux](/index.php?title=History_of_Arch_Linux_(Italiano)&action=edit&redlink=1 "History of Arch Linux (Italiano) (page does not exist)")*

Arch Linux è stata fondata dal programmatore canadese Judd Vinet. Il suo primo rilascio formale, Arch Linux 0.1, avvenne l'11 marzo 2002\. Anche se Arch è completamente indipendente, trae ispirazione dalla semplicità di altre distribuzioni, tra cui [Slackware](http://slackware.com), [CRUX](http://www.crux.nu) e [BSD](https://en.wikipedia.org/wiki/Berkeley_Software_Distribution "wikipedia:Berkeley Software Distribution"). Nel 2007, Judd Vinet si è dimesso da Project Lead per perseguire altri interessi ed è stato sostituito dal programmatore Americano Aaron Griffin, che oggi continua a portare avanti il progetto.

## Semplicità

Seguendo [Il Metodo Arch](/index.php/Il_Metodo_Arch "Il Metodo Arch"), Arch Linux è leggera, flessibile, semplice e mira ad essere molto simile a UNIX. Al momento dell'installazione viene fornito un ambiente minimale (senza GUI) compilato per architetture i686/x86-64: invece di andare a rimuovere i pacchetti non necessari e non desiderati, all'utente corrente viene offerta la possibilità di costruire tutto dalle fondamenta, senza alcun modello di default scelto preventivamente. La sua filosofia di progettazione e realizzazione la rendono facilmente estendibile ed adattabile a qualsiasi sistema si vuole ottenere, da una console minimalista al più grandioso degli ambienti desktop disponibili: è l’utente che decide cosa diventerà il suo sistema Arch.

Il semplice sistema di init di Arch è fortemente ispirato dal metodo *BSD, incorporando tutti i riferimenti in un solo file *single file* ([rc.conf](/index.php/Rc.conf_(Italiano) "Rc.conf (Italiano)")) piuttosto che in una struttura di directory SysVinit che contengono dozzine di link simbolici per ogni runlevel. La configurazione del sistema è ottenuta attraverso la modifica di semplici file di testo.

## Modernità

Arch Linux si sforza di mantenere gli ultimi rilasci delle versioni stabili del software fornito, fino a quando ciò non causerà errori di sistema. Esso è basato su un sistema [rolling-release](https://en.wikipedia.org/wiki/it:Rolling_release "wikipedia:it:Rolling release"), che consente di installare una sola volta con costanti aggiornamenti, senza mai dover reinstallare o eseguire elaborati upgrade di sistema inclusi nel passaggio da una versione all'altra. Mediante l'esecuzione di un comando, il sistema Arch sarà aggiornato ed all'avanguardia.

Arch include molte delle tecnologie più recenti disponibili per gli utenti GNU/Linux, tra cui il sistema init [systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)"), file systems moderni (Ext2/3/4, Reiser, XFS, JFS, BTRFS), LVM2/EVMS, software RAID, il supporto a udev e initcpio (con [mkinitcpio](/index.php/Mkinitcpio_(Italiano) "Mkinitcpio (Italiano)")), oltre alle ultime versioni del kernel disponibili.

## Gestore Pacchetti

Arch è sostenuto da [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)"), un semplice [gestore di pacchetti](https://en.wikipedia.org/wiki/it:Package_manager "wikipedia:it:Package manager") binari, che permette di aggiornare l'intero sistema con un solo comando. Pacman è scritto in *C* e progettato da zero per essere leggero, semplice e molto veloce. Arch offre anche la [Arch Build System](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)"), un porte-like per rendere più facile la compilazione e l'installazione dei pacchetti da sorgenti, che può anche essere sincronizzato con un unico comando. È anche possibile ricompilare l'intero sistema soltanto con un comando.

Supportando architetture i686 e x86-64,i [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)") forniscono diverse migliaia di pacchetti di alta qualità per soddisfare le varie esigenze software. Inoltre, Arch incoraggia la crescita della comunità ed il contributo, offrendo l'[Arch User Repository](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)"), che contiene molte migliaia di utenti manteiner di script PKGBUILD, la compilazione e l'installazione dei pacchetti da sorgenti, utilizzando l'applicazione *makepkg*. È anche possibile, per tutti gli utenti, creare e gestire facilmente i propri repository personalizzati.

## Integrità Sorgenti

Arch fornisce software vanilla senza patch; i pacchetti fanno riferimento a sorgenti [upstream](https://en.wikipedia.org/wiki/upstream_(software_development) puri, come l’autore originario intendeva distribuirli. Solo in rari casi i pacchetti vengono patchati, per evitare errori gravi in caso di disallineamenti di versioni che possono verificarsi in un modello rolling-release.

## Comunità

La comunità Arch è molto affidabile, vivace ed accogliente: tutti gli "Arcieri" sono invitati a partecipare e dare il loro contributo alla distribuzione, partecipando allo sviluppo del software di base, alla manutenzione dei pacchetti, alla segnalazione e risoluzione dei [bugs](https://bugs.archlinux.org/), al miglioramento della [documentazione ArchWiki](/index.php/Main_page_(Italiano) "Main page (Italiano)") , aiutando gli altri utenti alla soluzione di problemi o semplicemente scambiando opinioni nel [forum](https://bbs.archlinux.org/), nella [mailing lists](https://mailman.archlinux.org/mailman/listinfo/), nei [canali IRC](/index.php?title=IRC_Channels_(Italiano)&action=edit&redlink=1 "IRC Channels (Italiano) (page does not exist)"), o tramite la condivisione della propria conoscenza o addirittura tramite lo sviluppo autonomo di applicazioni. Arch Linux è il sistema operativo scelto da molte persone in tutto il mondo, ed esistono diverse [comunità internazionali](/index.php?title=International_Communities_(Italiano)&action=edit&redlink=1 "International Communities (Italiano) (page does not exist)") che danno una mano per offrire e fornire la documentazione in diverse lingue.

Vedere [Getting Involved](/index.php/Getting_involved_(Italiano) "Getting involved (Italiano)") per diventare un membro attivo della comunità.

## Sommario

Per riassumere: Arch Linux è una distribuzione semplice e versatile, progettata per soddisfare le esigenze degli utenti Linux più competenti. È potente e facile da gestire, rendendola una distro ideale per server e workstation. Si è liberi di fare la propria scelta: se si condivide questa visione di ciò che dovrebbe essere una distribuzione GNU/Linux, allora siete benvenuti ed incoraggiati ad utilizzarla liberamente, ad essere coinvolti ed a contribuire alla comunità. Benvenuti in Arch!