Un [software repository](https://en.wikipedia.org/wiki/software_repository "wikipedia:software repository") è un "magazzino" di dati da cui i pacchetti di software possono essere recuperati e installati su un computer. Gli Arch Linux [package maintainers](/index.php/Package_Maintainer "Package Maintainer") (sviluppatori e [Trusted Users](/index.php/Trusted_Users "Trusted Users")) mantengono un certo numero di repository ufficiali, contenenti i pacchetti del software, da quello più essenziale a quello extra, facilmente accessibili via [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)"). Questo articolo delinea questi repository ufficialmente supportati.

## Contents

*   [1 Cenni storici](#Cenni_storici)
*   [2 [core]](#.5Bcore.5D)
*   [3 [extra]](#.5Bextra.5D)
*   [4 [community]](#.5Bcommunity.5D)
*   [5 [multilib]](#.5Bmultilib.5D)
*   [6 [testing]](#.5Btesting.5D)
*   [7 [community-testing]](#.5Bcommunity-testing.5D)
*   [8 [multilib-testing]](#.5Bmultilib-testing.5D)

## Cenni storici

La maggioranza delle suddivisioni dei repository (depositi di software) esistono per motivi storici. Originariamente, quando Arch Linux era usata da pochissimi utenti, esisteva un solo repo, che ora è **[core]**, chiamato *[official]*. Questo repository conteneva originariamente le applicazioni preferite di Judd Vinet, il creatore della distribuzione. Oggi è destinato a contenere un programma per ogni tipo di applicazione: un window manager, uno dei principali browser e così via.

In passato, alcuni utenti non gradirono la selezione di Judd, così quando [Arch Build System](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)") diventò così semplice da usare cominciarono a creare pacchetti da soli. Questi pacchetti andarono in un repository chiamato *[unofficial]*, che fu mantenuto da altri sviluppatori oltre Judd. Alla fine, i due repo vennero entrambi considerati ugualmente supportati dagli sviluppatori, cosicchè i nomi [official] e [unofficial] non erano più adatti; furono quindi rinominati rispettivamente *[current]* ed *[extra]* alla versione 0.5.

In breve tempo, dopo la versione 2007.8.1, [current] cambiò nome in [core] per evitare confusione su cosa esattamente contenesse. I due repo sono ora praticamente uguali agli occhi degli sviluppatori e della comunità, anche se [core] ha qualche differenza; la principale è che i pacchetti conenuti nell'Install CD e nelle release snapshots sono presi solo da [core]. Questo infatti garantisce un sistema Linux completo, anche se potrebbe non essere quello desiderato.

Tra le versioni 0.5 e 0.6, ci accorse che c'erano molti pacchetti che gli sviluppatori non volevano mantenere. Uno di questi (Xentac) preparò i "Trusted User Repositories", repo non ufficiali nei quali i Trusted Users (utenti fidati) potevano inserire i pacchetti da loro creati. Un repo, *[staging]*, ospitava i pacchetti che potevano essere promossi da uno degli sviluppatori di Arch Linux per il passaggio ai depositi ufficiali ma, a parte questo, sviluppatori e Trusted Users restarono più o meno distinti.

Il sistema funzionò per un certo periodo, successivamente i Trusted Users cominciarono a trascurare i loro repo mentre dei normali utenti desideravano condividere i propri pacchetti. Questo portò allo sviluppo di [AUR](https://aur.archlinux.org/) e i Trusted Users furono aggregati in un gruppo più unito che ora mantiene il repo **[community]**. I Trusted Users sono ancora un gruppo separato dagli svilupptori di Arch Linux e non c'è molto dialogo tra di loro. Comunque, i pacchetti più popolari sono ancora talvolta promossi da [community] ad **[extra]** [AUR](https://aur.archlinux.org/) permette anche ai normali utenti di inviare PKGBUILDs.

Dopo [i numerosi problemi](https://www.archlinux.org/news/please-avoid-kernel-261614-1/) causati dall'inserimento di un kernel in **[core]**, fu introdotta la "core signoff policy". Da allora, tutti i pacchetti aggiornati per [core] devono necessariamente passare prima attraverso il repository **[testing]** e, solo dopo diverse autorizzazioni dei vari sviluppatori, possono muoversi nell'altro repo. Nel corso del tempo, si è notato che vari pacchetti [core] venivano utilizzati di rado, ciò, unitamente alla mancanza di segnalazioni di errori, divenne un criterio informale per l'accettazione dei pacchetti stessi.

Veso la fine 2009/inizio 2010, con l'avvento di alcuni nuovi filesystem (ed il desiderio di supportarli durante il processo di installazione), la realizzazione di [core] non fu mai chiaramente definita (semplicemente "pacchetti importanti, selezionati accuratamente dagli sviluppatori"); il repository è stato descritto più dettagliatamente (vedere più avanti).

## [core]

Questo repository [core] può essere trovato in `.../core/os/`, nel proprio mirror preferito.

Esso è sottoposto a rigidi requisiti di qualità:

*   Sviluppatori e/o utenti hanno bisogno di un'autorizzazione per gli aggiornamenti dei pacchetti, prima che questi ultimi vengano accettati.
*   Per i pacchetti utilizzati di rado, è necessaria un'esposizione ragionevole (ad esempio: notifiche agli utenti degli aggiornamenti, richiesta di autorizzazioni, periodi di prova di una settimana, a seconda della rilevanza dei cambiamenti, la mancanza di segnalazioni di errori, insieme all'implicita autorizzazione del manteiner del pacchetto).

Esso contiene i pacchetti che:

*   sono necessari all'avvio di un qualsiasi sistema supportato da Arch.
*   possono essere necessari per connettersi ad internet.
*   sono essenziali per la compilazione di altri pacchetti.
*   possono gestire e controllare/riparare i filesystems supportati.
*   sono necessari nelle prime fasi del processo di installazione (ad esempio [openssh](https://www.archlinux.org/packages/?name=openssh)).
*   dipendono dai punti precedenti (ma non sono necessariamente makedepends).

**Nota:** Questo repository, utilizzato per essere incluso nel supporto di installazione core, in modo da poter costruire un sistema di base completamente funzionante senza accesso ad Internet, ora non è più necessario. L'accesso ad Internet è ora necessaria per installare un nuovo sistema. Vedere [qui](/index.php/Pacman_tips#Installing_packages_from_a_CD.2FDVD_or_USB_stick "Pacman tips") se si vuole creare un repository locale con pacchetti provenienti da [core] o da uno degli altri repository.

## [extra]

Questo repository pu èssere trovato in `.../extra/os/` nel proprio mirror preferito.

Esso contiene tutti i pacchetti che non sono contenuti in [core]. Esempio: Xorg, window managers, browser web, media players, strumenti per linguaggi tipo Python, Ruby e molti altri.

## [community]

Questo repository può essere trovato in `.../community/os/` sul mirrror preferito.

Esso contiene i pacchetti provenienti dall'[Arch User Repository](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)") che hanno avuto abbastanza voti e sono stati adottati da un [Trusted User](/index.php/Trusted_Users "Trusted Users").

## [multilib]

Questo repository può essere trovato in `.../multilib/os/` del mirror preferito.

Esso contiene software a 32 bit e librerie che possono essere utilizzate per eseguire e sviluppare applicazioni a 32 bit su 64 bit (ad esempio [wine](https://www.archlinux.org/packages/?name=wine), [skype](https://www.archlinux.org/packages/?name=skype), ecc).

Per maggiori informazioni, vedere [Multilib](/index.php/Multilib "Multilib").

## [testing]

**Attenzione:** Fare attenzione quando si abilita il repository [testing]. Il sistema potrebbe diventare instabile dopo l'esecuzione di un aggiornamento con [testing] abilitato e, per questo, solo utenti esperti dovrebbero usarlo.

Questo repository può essere trovato in `../testing/os/` sul proprio mirrror preferito.

Esso è speciale perchè contiene i pacchetti che sono candidati per i repository [core] o [extra].

I nuovi pacchetti vanno in [testing] se:

*   Possano rovinare qualcosa durante un aggiornamento e hanno bisogno di essere testati prima.
*   Richiedono altri pacchetti per la ricompilazione. In questo caso, tutti i pacchetti che necessitano di ricompilazione sono messi prima in [testing] e vengono spostati di nuovo agli altri repo quando questa è stata effettuata.

Questo è l'unico repository che può avere conflitti di nome con gli altri repo ufficiali. Se abilitato, deve essere il primo della lista nel file `/etc/pacman.conf`.

Si noti che non è creato per contenere le "ultimissime versioni" dei pacchetti. Parte del suo scopo è quello di controllare gli aggiornamenti dei pacchetti che hanno il potenziale per causare la "rottura del sistema", sia per far parte del set dei pacchetti contenuti in [core], o per essere critici in altri modi. Come tale, gli utenti del repository [testing] sono "caldamente invitati" ad iscriversi alla mailing list [arch-dev-public](https://mailman.archlinux.org/mailman/listinfo/arch-dev-public), a visitare il [testing] Repo Forum ed a segnalare tutti i bug al bug tracker.

Se si abilita [testing], si deve abilitare anche [community-testing].

## [community-testing]

Il repository [community-testing] è come il repository [testing], ma riguarda i pacchetti che sono candidati per entrare nel repository [community].

Se lo si si abilita, si deve abilitare anche [testing].

## [multilib-testing]

Questo repository è come il repository [testing], ma dedicato ai pacchetti candidati per il repository [multilib].

Se lo si abilita, si edve abilitare anche [testing].