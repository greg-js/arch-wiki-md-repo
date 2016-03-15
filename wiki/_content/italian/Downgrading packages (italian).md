Questa guida vi mostrerà come effettuare il downgrade di un pacchetto ad una versione precedente. Il declassamento di un pacchetto non viene normalmente raccomandato ed è spesso necessario solo quando viene introdotto un bug nel pacchetto corrente.

Prima di iniziare l'operazione di declassamento, considerare il perché lo si sta facendo. Se la causa è un bug, si prega di aiutare sia Arch che gli sviluppatori, dedicando pochi minuti del proprio tempo per inviare la notifica dei bug nel bug tracker Arch o sul progetto madre del programma stesso. Dal momento che Arch è una distribuzione rolling release, probabilmente si lavora di continuo con pacchetti nuovissimi e talvolta è possibile incappare in qualche problema di bug.

Sia noi che gli sviluppatori apprezzeremo lo sforzo. Quel po' di informazioni in più ci potrebbe risparmiare ore di test e debug, e ci aiuterebbe a rilasciare software sempre più stabile.

## Contents

*   [1 Ragioni](#Ragioni)
*   [2 I dettagli](#I_dettagli)
*   [3 Come effettuare il downgrade di un pacchetto](#Come_effettuare_il_downgrade_di_un_pacchetto)
    *   [3.1 Effettuare il downgrade del kernel](#Effettuare_il_downgrade_del_kernel)
*   [4 Trovare la versione precedente](#Trovare_la_versione_precedente)
    *   [4.1 Mirror non aggiornati](#Mirror_non_aggiornati)
    *   [4.2 Arch Rollback Machine](#Arch_Rollback_Machine)
    *   [4.3 Ricompilare il pacchetto](#Ricompilare_il_pacchetto)
*   [5 Cambiare Repository](#Cambiare_Repository)
*   [6 FAQ](#FAQ)
    *   [6.1 Non riesco a declassare un pacchetto, a causa delle dipendenze.](#Non_riesco_a_declassare_un_pacchetto.2C_a_causa_delle_dipendenze.)
    *   [6.2 Come è possibile impedire a Pacman di aggiornare i pacchetti scaricati?](#Come_.C3.A8_possibile_impedire_a_Pacman_di_aggiornare_i_pacchetti_scaricati.3F)
    *   [6.3 Vorrei tornare a come era il mio sistema ieri.](#Vorrei_tornare_a_come_era_il_mio_sistema_ieri.)

## Ragioni

Il processo di declassamento è quello di disinstallare il pacchetto attuale e installare una versione precedente. La versione precedente può essere una versione immediata (l'ultima versione precedente del pacchetto) o un certo numero di versioni precedenti.

Le ragioni del declassamento includono (tra le altre): che l'attuale versione ha un bug, non contiene al momento la funzionalità desiderata, o la si sta usando per motivi di sperimentazione. In ognuno di questi casi, l'utente ha scelto che può essere meno problematico tornare ad una versione precedente e aspettare una nuova release.

Il declassamento di un pacchetto può significare che altri pacchetti potrebbero venir declassati, in quanto richiesti come dipendenze. Per coloro che hanno installato una notevole quantità di pacchetti sperimentali o di test, ed eseguito molte configurazioni, può essere preferibile reinstallare il sistema piuttosto che cercare di eseguire il downgrade.

## I dettagli

Tuttavia, l'utente deve tenere a mente i seguenti punti:

*   Considerare le dipendenze di ogni programma. Le librerie necessarie, che così spesso cambiano con ogni versione, e la funzionalità dei file associati, che possono essere completamente diversi da quelli precedenti. La soluzione richiede anche la loro modifica, per le versioni precedenti.

*   Considerare se i file necessari sono stati rimossi dal sistema o se addirittura sono ancora disponibili da altre fonti. I repository del sistema rolling release di Arch Linux vengono automaticamente aggiornati, senza salvare le vecchie versioni. Vedere ulteriori informazioni su questo problema qui sotto.

*   Fare attenzione con le modifiche ai file di configurazione e script. Su questo punto, ci si baserà su pacman che gestirà questo per noi, seguendo le indicazioni e gli avvisi di sicurezza che verranno proposti.

Il concetto di "Arch Rollback Machine" è tuttora in via di sviluppo ed in attesa di un inserimento utile in pacman. Quando succederà, diventerà automatico.

## Come effettuare il downgrade di un pacchetto

*   D: Ho appena eseguito `pacman -Syu` e il pacchetto "XYZ" è stato aggiornato alla versione N dalla versione M. Questo pacchetto è causa di problemi sul mio computer, come posso fare il downgrade dalla versione N alla versione precedente M?
*   R: Può essere possibile effettuare il downgrade del pacchetto esplorando semplicemente `/var/cache/pacman/pkg` sul proprio sistema e vedere se la vecchia versione del pacchetto è presente. (Se non è stato eseguito `pacman -Scc` di recente, dovrebbe essere lì). Se il pacchetto è lì, è possibile reinstallare la versione con il comando `pacman -U /var/cache/pacman/pkg/pkgname-olderpkgver.pkg.tar.gz`.

Questo processo rimuoverà il pacchetto attuale, calcolerà attentamente tutte le dipendenza modificate, e reinstallerà la versione precedente scelta con le dipendenze corrette su tutta la linea.

**Nota:** Se si modifica una parte fondamentale del sistema operativo, ci si può ritrovare a dover estrarre decine di pacchetti e sostituirli con le loro versioni precedenti. Oppure potrebbero non essere più disponibili e si dovrà rimetterli manualmente, facendo attenzione che un particolare aggiornamento, non reinstalli la versione del pacchetto indesiderata.

C'è anche un pacchetto in [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)"), chiamato [downgrade](https://aur.archlinux.org/packages/downgrade/). Si tratta di un semplice script Bash che verificherà la presenza, nella propria cache, di versioni precedenti dei pacchetti. Qualora non fossero trovati pacchetti nella cache, lo script cercherà anche in [A.R.M.](/index.php/Downgrading_Packages_(Italiano)#ARM "Downgrading Packages (Italiano)") Si potrà quindi selezionare il pacchetto da installare. Sostanzialmete si tratta di un'automatizzazione dei processi descritti qui. Vedere `downgrade --help` per informazioni sull'utilizzo.

Un altro strumento utile è [downgrader](https://aur.archlinux.org/packages/downgrader/), esso funziona con i log di pacman, può effettuare il downgrade dei pacchetti da ARM, dalla cache locale, e funziona con la lista dei pacchetti (se il sistema risulta instabile dopo l'aggiornamento di alcuni pacchetti e si è insicuri circa il loro nome).

### Effettuare il downgrade del kernel

Se dopo l'aggiornamento del kernel non si riesce ad avviare il sistema, si può effettuare il downgrade del kernel tramite il live cd. Utilizzare un supporto di installazione Arch Linux abbastanza recente. Una volta avviato, montare la partizione del proprio sistema, ad esempio /mnt e se si ha /boot oppure /var in partizioni separate, montarle entrambe (<tt>mount /dev/sdc3 /mnt/boot</tt>). Quindi montare proc, ecc..

## Trovare la versione precedente

Ci sono tre modi per farlo.

### Mirror non aggiornati

Se non si trovano le versioni precedenti sul proprio sistema, verificare se uno dei mirror non è ben sincronizzato con gli aggiornamenti, e ottenere i pacchetti da lì. Cliccare qui per visualizzare lo [stato dei mirror](https://www.archlinux.org/mirrors/status/).

È inoltre possibile controllare questo mirror che mantiene pacchetti datati:

*   [http://schlunix.org/?page_id=11](http://schlunix.org/?page_id=11)

### Arch Rollback Machine

L' [Arch Rollback Machine](ftp://seblu.net/archlinux/arm/) (ARM) contiene delle specie di istantanee archiviate dei repository risalenti al 1 novembre 2009\. Il sito è in continuo mutamento alla data odierna (21 November 2009), ed è stato rimosso il materiale risalente fino al 1 ° ottobre 2008, come precedentemente riportato.

Chi fosse interessato ad ARM, può vedere l'annuncio introduttivo sul forum e la discussione, in modo da mantenersi aggiornato sul progetto. Il thread del forum è [qui](https://bbs.archlinux.org/viewtopic.php?id=53665).

In sintesi si illustra l'obiettivo, che è quello di creare degli URL in modo da facilitare l'esecuzione di pacman + wget script per ottenere il "roll back", cioè un ripristino del sistema ad una data specifica. Il processo di automazione non è stato ancora spiegato. Per cercare manualmente un particolare pacchetto, si può usare la pagina di ricerca fornita su [ARM Search](http://arm.konnichi.com/search/).

### Ricompilare il pacchetto

Nella peggiore delle ipotesi, se il pacchetto non è reperibile altrove, sarà necessario compilare la versione precedente da soli. Per fare questo è necessario un PKGBUILD per il file; si può modificare il PKGBUILD esistente fornito da ABS per utilizzare i vecchi sorgenti, o si può visitare [https://www.archlinux.org/packages/](https://www.archlinux.org/packages/) e cercare il pacchetto di cui si desidera effettuare il downgrade. Una volta trovato, cliccare "View Changes" e selezionare "log". Individuare la versione desiderata e fare clic sul percorso. Poi basta scaricare i file che si trovano in tale directory e compilarli con makepkg.

Per i pacchetti AUR, attualmente l'unico metodo per ottenere i vecchi PKGBUILDs è prenderli da [http://pkgbuild.com/git/aur-mirror.git/](http://pkgbuild.com/git/aur-mirror.git/) oppure controllare l'[Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories") per i binari precompilati (a volte non sono aggiornati).

## Cambiare Repository

Per cambiare repository in ARM, occorre commentare la riga obsoleta ed aggiungere il percorso dell'idonea directory nel seguente formato:

```
[core]
#Server=http://mirrors.gigenet.com/archlinux/core/os/i686
Server=http://arm.konnichi.com/2009/11/01/core/os/i686

```

In questo esempio, la sezione data istruisce a prendere qualsiasi pacchetto disponibile dal 1 novembre 2009\. Si prega di notare che tutti i repository sono gli snapshot dei repository ufficiali. Basta modificare il mirror in `/etc/pacman.d/mirrorlist`, e spostare un mirror ARM in alto, per esempio http://arm.konnichi.com/2009/11/01/$repo/os/i686 per sincronizzare tutti i repository ufficiali elencati in `/etc/pacman.conf` al mirror ARM scelto. Infine aggiornarlo con:

```
pacman -Syy  # ricarica la sincronizzazione dei database
pacman -Suu  # declassa tutti i pacchetti ad una versione inferiore nei repo

```

Questo da solo non garantisce un rollback completo, dato che a volte ci possono essere conflitti tra i vari pacchetti per quanto riguarda i numeri di versione, ecc. Se si conosce il repository può essere più facile visitare il mirror globale, per esempio [http://arm.konnichi.com/core/os/i686](http://arm.konnichi.com/core/os/i686). Notare l'omissione della data.

Per maggiori informazioni si prega di vedere [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)").

## FAQ

### Non riesco a declassare un pacchetto, a causa delle dipendenze.

È possibile ignorare le dipendenze durante l'aggiornamento o la rimozione con l'opzione "d". Esempio: **pacman -Ud pkgpkgname-olderpkgver.pkg.tar.gz** ma questo potrebbe danneggiare ulteriormente il sistema.

### Come è possibile impedire a Pacman di aggiornare i pacchetti scaricati?

`IgnorePkg = package1 package2` nel proprio `pacman.conf` indicherà a Pacman, quando si esegue --sysupgrade, di ignorare ogni aggiornamento per i pacchetti selezionati.

### Vorrei tornare a come era il mio sistema ieri.

È facilmente ottenibile se si sono eseguiti gli snapshot periodici forniti da [LVM](/index.php/LVM_(Italiano) "LVM (Italiano)").