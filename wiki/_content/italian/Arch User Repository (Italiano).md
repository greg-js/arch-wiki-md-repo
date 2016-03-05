**Arch User Repository** (AUR) è un repository sostenuto dalla comunità per utenti Arch. Contiene le descrizioni dei pacchetti (i [PKGBUILD](/index.php/PKGBUILD_(Italiano) "PKGBUILD (Italiano)")) che ti permettono di compilare i sorgenti grazie al comando [makepkg](/index.php/Makepkg_(Italiano) "Makepkg (Italiano)") e quindi installarli con [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)"). AUR È stato creato per creare e scambiare pacchetti tra la comunità e per aiutarne lo sviluppo, inclusi i pacchetti del repository [community](#community). Questo documento spiega come accedere ed installare i pacchetti presenti in AUR.

Un buon numero di nuovi pacchetti che entrano nei repository ufficiali, partono prima in AUR. In AUR gli utenti sono in grado di contribuire con i propri pacchetti (PKGBUILD). La AUR community può votare pro o contro i pacchetti presenti in AUR. Se un pacchetto diventa abbastanza popolare, sempre che venga incontro alle esigenze di pacchettizzazione e alle licenze, può entrare a far parte del repository *community* (direttamente accessibile da [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)") o [abs](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)")).

## Contents

*   [1 Per iniziare](#Per_iniziare)
*   [2 Storia](#Storia)
*   [3 Ricerche su AUR](#Ricerche_su_AUR)
*   [4 Installare i pacchetti da AUR](#Installare_i_pacchetti_da_AUR)
    *   [4.1 Requisiti](#Requisiti)
    *   [4.2 Ottenere i file necessari](#Ottenere_i_file_necessari)
    *   [4.3 Compilare il pacchetto](#Compilare_il_pacchetto)
    *   [4.4 Installazione del pacchetto](#Installazione_del_pacchetto)
*   [5 Feedback](#Feedback)
*   [6 Condividere e mantenere i pacchetti](#Condividere_e_mantenere_i_pacchetti)
    *   [6.1 Aggiungere pacchetti](#Aggiungere_pacchetti)
        *   [6.1.1 Regole per la sottomissione dei pacchetti](#Regole_per_la_sottomissione_dei_pacchetti)
        *   [6.1.2 Creare un nuovo pacchetto](#Creare_un_nuovo_pacchetto)
    *   [6.2 Mantenere i pacchetti](#Mantenere_i_pacchetti)
    *   [6.3 Altri tipi di richieste](#Altri_tipi_di_richieste)
*   [7 community](#community)
*   [8 Git Repo](#Git_Repo)
*   [9 FAQ](#FAQ)
    *   [9.1 Cos'è AUR?](#Cos.27.C3.A8_AUR.3F)
    *   [9.2 Che tipo di pacchetti sono permessi su AUR?](#Che_tipo_di_pacchetti_sono_permessi_su_AUR.3F)
    *   [9.3 Come si votano i pacchetti in AUR?](#Come_si_votano_i_pacchetti_in_AUR.3F)
    *   [9.4 Cos'è un TU?](#Cos.27.C3.A8_un_TU.3F)
    *   [9.5 Che differenza c'è tra Arch User Repository e community?](#Che_differenza_c.27.C3.A8_tra_Arch_User_Repository_e_community.3F)
    *   [9.6 Quanti voti servono per far spostare un PKGBUILD in community?](#Quanti_voti_servono_per_far_spostare_un_PKGBUILD_in_community.3F)
    *   [9.7 Come si fa un PKGBUILD?](#Come_si_fa_un_PKGBUILD.3F)
    *   [9.8 Ho dato il comando "pacman -S foo"; non funziona, ma sono sicuro che si trova in community](#Ho_dato_il_comando_.22pacman_-S_foo.22.3B_non_funziona.2C_ma_sono_sicuro_che_si_trova_in_community)
    *   [9.9 In AUR, un pacchetto non è aggiornato; cosa devo fare?](#In_AUR.2C_un_pacchetto_non_.C3.A8_aggiornato.3B_cosa_devo_fare.3F)
    *   [9.10 Ho un PKGBUILD che vorrei inviare; qualcuno può controllarlo per vedere se ci sono errori?](#Ho_un_PKGBUILD_che_vorrei_inviare.3B_qualcuno_pu.C3.B2_controllarlo_per_vedere_se_ci_sono_errori.3F)
    *   [9.11 Il pacchetto Foo in AUR non compila quando lancio makepkg; cosa dovrei fare?](#Il_pacchetto_Foo_in_AUR_non_compila_quando_lancio_makepkg.3B_cosa_dovrei_fare.3F)
    *   [9.12 Come posso accelerare i ripetuti processi di compilazione?](#Come_posso_accelerare_i_ripetuti_processi_di_compilazione.3F)
    *   [9.13 Come faccio ad accedere ai pacchetti di unsupported](#Come_faccio_ad_accedere_ai_pacchetti_di_unsupported)
    *   [9.14 Come faccio a mandare un PKGBUILD ad AUR senza usare l'interfaccia web?](#Come_faccio_a_mandare_un_PKGBUILD_ad_AUR_senza_usare_l.27interfaccia_web.3F)
*   [10 AUR 4](#AUR_4)
    *   [10.1 Prima di inviare i pacchetti ad aur4.archlinux.org](#Prima_di_inviare_i_pacchetti_ad_aur4.archlinux.org)
    *   [10.2 Inviare i pacchetti ad aur4.archlinux.org](#Inviare_i_pacchetti_ad_aur4.archlinux.org)
    *   [10.3 Script per la migrazione](#Script_per_la_migrazione)
*   [11 Altre risorse](#Altre_risorse)

## Per iniziare

Gli utenti possono cercare e scaricare i PKGBUILD dal [sito Web di AUR](https://aur.archlinux.org). Questi PKGBUILD possono essere compilati in pacchetti installabili usando [makepkg](/index.php/Makepkg_(Italiano) "Makepkg (Italiano)") e successivamente installati con pacman.

*   Assicurarsi di aver installato il gruppo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) (`pacman -S --needed base-devel`).
*   Leggere il resto di questo articolo per ulteriori informazioni e un breve tutorial su come installare i pacchetti AUR.
*   Visitare il [sito Web di AUR](https://aur.archlinux.org) per informarsi riguardo agli aggiornamenti ed agli eventi. Lì troverete anche statistiche ed una lista aggiornata delle ultime versioni disponibili per i pacchetti di AUR.
*   Dare un occhiata alle [#FAQ](#FAQ) in cerca di risposte alle domande più comuni.
*   Modificare il file `/etc/makepkg.conf` per ottimizzare al meglio le priorità del tuo processore per la compilazione dei pacchetti da AUR. Un significativo miglioramento nei tempi di compilazione può essere ottenuto, con i processori multi-core, impostando correttamente la variabile MAKEFLAGS. Gli utenti possono anche abilitare ottimizzazioni specifiche per l'hardware in GCC attraverso la variabile CFLAGS. Vedi [makepkg.conf](/index.php/Makepkg.conf "Makepkg.conf") per ulteriori informazioni.

## Storia

I seguenti stumenti sono stati riportati solo per motivazioni storiche, e sono stati sostituiti da AUR e non più disponibili.

Agli inizi c'era `ftp://ftp.archlinux.org/incoming` e le persone vi hanno contribuito semplicemente inviando i PKGBUILD, i file necessari ed i file compilati stessi sul server. I pacchetti ed i file associati rimanevano lì fino a quando un [Package Maintainer](/index.php/Package_Maintainer "Package Maintainer") li vedeva e li adottava.

Quindi nacquero i Trusted User Repositories (repositori per utenti fidati). Ad alcuni utenti della community era permesso di ospitare i loro personali repository per condividerli con gli altri. AUR si è espanso su questa base, con l'obbiettivo di rendere contemporaneamente più flessibile e semplice il suo utilizzo. Infatti, i manutentori di AUR sono ancora definiti TUs ([Trusted Users](/index.php/Trusted_Users "Trusted Users")).

## Ricerche su AUR

Il sito Web di AUR può essere trovato [qui](https://aur.archlinux.org/), ed un'interfaccia per l'accesso ad AUR tramite uno script (ad esempio) può essere trovata [qui](https://aur.archlinux.org/rpc.php).

Le ricerche avvengono all'interno dei nomi e delle descrizioni attraverso un metodo simile a quello di MYSQL. Questo permette l'uso di criteri di ricerca più flessibili (es. provare a cercare 'tool%like%grep%' invece di 'tool like grep'). Se si ha bisogno di ricercare una descrizione che contenga '%', usare il carattere di escape così '\%'.

## Installare i pacchetti da AUR

Installare i pacchetti da AUR è un processo relativamente semplice. Essenzialmente:

1.  Ottenere il tarball contenente il [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") e gli eventuali altri file necessari come unità di systemd e patch (ma spesso non i sorgenti di per sè).
2.  Estrarre il tarball (preferibilmente in una cartella a parte da usare solo per le compilazioni di AUR) con `tar -xvzf foo.tar.gz`.
3.  Verificare che il PKGBUILD e i file che lo accompagnano non siano pericolosi o inattendibili.
4.  Lanciare il comando `makepkg` all'interno della directory contenente i file scaricati (il comando "`makepkg -s`" si occuperà di risolvere automaticamente le dipendenze tramite pacman). Questo scaricherà e compilerà il codice, infine creerà il pacchetto.
5.  Leggere l'eventuale file README in `src/`, dato che potrebbe contenere informazioni utili più avanti.
6.  Installare il pacchetto ottenuto tramite [pacman](/index.php/Pacman "Pacman"):

	 `$ pacman -U /percorso/per/il/pacchetto.tar.xz` 

Gli [AUR helpers](/index.php/AUR_helpers "AUR helpers") garantiscono un accesso simile ad AUR. Sono svariati nelle loro caratteristiche, ma possono facilitare nella ricerca, nel download, nella compilazione e nell'installazione dei pacchetti tramite i [PKGBUILD](/index.php/PKGBUILD_(Italiano) "PKGBUILD (Italiano)") disponibili su AUR. Tutti questi script possono essere trovati in AUR.

**Note:** Non c'è e non ci sarà mai un meccanismo *ufficiale* per l'installazione di materiale precompilato da AUR. **Tutti gli utenti di AUR dovrebbero essere pratici del processo di compilazione.**

### Requisiti

Per prima cosa, assicurarsi che gli strumenti necessari siano installati. Il gruppo di pacchetti [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) dovrebbe essere sufficiente; include [make](https://www.archlinux.org/packages/?name=make) ed altri pacchetti necessari alla compilazione dai sorgenti.

**Attenzione:** I pacchetti su AUR presumono che il gruppo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) sia già stato installato, cioè essi non riporteranno i componenti di questo gruppo tra le dipendenze, anche se il pacchetto non può essere compilato senza di essi. Siete pregati di assicurarvi che questo gruppo sia installato prima di denunciare fallimenti nelle compilazioni.

```
# pacman -S --needed base-devel

```

Successivamente scegliere una cartella appropriata per la compilazione. Una cartella di compilazione è semplicemente una cartella dove il pacchetto viene compilato o "creato" e può essere una qualsiasi cartella. Un esempio di uso comune è:

```
~/builds

```

oppure se si utilizza ABS ( [Arch Build System](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)") ):

```
/var/abs/local

```

Per maggiori informazioni su ABS leggete la guida [Arch Build System](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)"). L'esempio userà `~/builds` come cartella di compilazione.

### Ottenere i file necessari

Trovare il pacchetto su AUR. Ciò può essere fatto usando lo strumento di ricerca (la casella di testo in alto nella [home page di AUR](https://aur.archlinux.org/)). Cliccando sul nome del pacchetto nei risultati della ricerca si aprirà la pagina informativa relativa al pacchetto. Leggere la descrizione per assicurarsi che si tratti del pacchetto che si stà cercando, controllare quando il pacchetto è stato aggiornato l'ultima volta, e leggere i relativi commenti.

Ci sono tre metodi per ottenere i file necessari per la compilazione, senza la necessità di utilizzare un AUR helper:

*   Scaricare i file necessari per la compilazione cliccando sul link "Scarica lo snapshot" nel riquadro "Azioni del pacchetto" a destra. Questo file dovrebbe essere salvato nella cartella di compilazione o quantomeno vi andrebbe copiato al termine del download. In questo esempio si suppone di avere il file chiamato "foo.tar.gz"(il formato standard è *nomepacchetto*.tar.gz, se è stato inviato correttamente).

*   In alternativa è possibile scaricare il tarball dal terminale, dopo essersi spostati nella cartella di compilazione:

```
$ cd ~/builds
$ curl -L -O https://aur.archlinux.org/packages/fo/foo/foo.tar.gz

```

*   E' anche possibile clonare il repository [Git](/index.php/Git "Git"), che è denominato "Git Clone URL" nei "Dettagli del pacchetto":

```
$ cd ~/build-repos
$ git clone [https://aur.archlinux.org/foo.git](https://aur.archlinux.org/foo.git)

```

### Compilare il pacchetto

Spostarsi nella cartella di compilazione se non si fosse già lì, poi estrarre l'archivio precedentemente scaricato:

```
$ cd ~/builds
$ tar -xvzf foo.tar.xz

```

Questo creerà una cartella di nome "foo" all'interno della directory di compilazione.

**Note:** Nel caso di clone del git, il processio di estrazione non è necesseario. Il clone git ha già creato la directory `foo`.

**Attenzione:** **Controllare accuratamente tutti i file.** Spostarsi nella nuova cartella appena creata e controllare accuratamente il `PKGBUILD` ed eventuali `.install` verificando che non contengano comandi potenzialmente pericolosi. I `PKGBUILD` sono script bash che contengono funzioni che verranno eseguite da `makepkg`: queste funzioni possono contenere un qualsiasi comando valido o sintassi di Bash, quindi è del tutto possibile che un `PKGBUILD` contenga comandi pericolosi all'insaputa dell'autore. Da quando `makepkg` utilizza fakeroot (e non dovrebbe mai essere eseguito da root), c'è un certo livello di protezione, ma non si dovrebbe mai farci troppo affidamento. In caso di dubbi NON compilare il pacchetto e cercare consigli sui forum o sulle mailing list.

```
$ cd foo
$ nano PKGBUILD
$ nano foo.install

```

Dopo aver verificato l'integrità dei file, eseguire [makepkg](/index.php/Makepkg "Makepkg") come normale utente.

```
$ makepkg -s

```

L'opzione switch `-s` utilizzerà [sudo](/index.php/Sudo "Sudo") per l'installazione di eventuali dipendenze. Se non si intende utilizzare [sudo](/index.php/Sudo "Sudo"), si dovrà provvedere ad installare manualmente le eventuali dipendenze richieste e successivamente eseguire il comando sopra suggerito, omettendo l'opzione `-s`.

### Installazione del pacchetto

Installare il pacchettto usando pacman. L'archivio dovrebbe essere stato creato ed avere il nome secondo il seguente schema:

```
<*nome applicazione*>-<*numero versione*>-<*numero revisione pacchetto*>-<*architettura*>.pkg.tar.xz

```

Questo pacchetto può essere installato usando l'opzione "upgrade" di pacman:

```
# pacman -U foo-0.1-i686.pkg.tar.xz   

```

I pacchetti installati manualmente sono chiamati *foreign packages*, letteralmente "pacchetti stranieri", infatti non provengono da nessun repository noto a pacman. Per elencare tutti i foreign packages:

```
$ pacman -Qm

```

**Note:** L'esempio precedente è solo un breve riassunto del processo di compilazione. Una lettura alle pagine relative a [makepkg](/index.php/Makepkg_(Italiano) "Makepkg (Italiano)") ed [ABS](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)") forniranno maggiori dettagli ed è caldamente raccomandato farlo (specialmete per gli utenti che non hanno mai compilato).

## Feedback

La gestione dei commenti [AUR Web Interface](https://aur.archlinux.org) facilita gli utenti a dare suggerimenti e responsi su possibili miglioramenti ai manutenitori dei [PKGBUILD](/index.php/PKGBUILD_(Italiano) "PKGBUILD (Italiano)"). Evitare di incollare patch o PKGBUILD nella sezione dei commenti. Questi commenti diventano velocemente obsoleti e senza utilità occupando molto spazio. E' quindi preferibile inviarli per email al manutentore oppure usare [pastebin](/index.php/Pastebin_Clients "Pastebin Clients").

Una delle essenziali attività di **tutti** gli utenti di Arch è consultare tra i pacchetti di AUR e **votare** per i pacchetti preferiti attraverso il sito web di AUR. Tutti i pacchetti possonno essere adottati da un TU ( un utente fidato - Trusted User) per una eventuale inclusione nel repostory [community](#community), ed il conteggio dei voti è uno degli aspetti di questo processo; è quindi nell'interesse di tutti esprimere il proprio voto!

## Condividere e mantenere i pacchetti

Gli utenti giocano un ruolo fondamentale in AUR, il quale non sfrutterebbe il suo potenziale senza il supporto, il coinvolgimento ed i contributi dalla più ampia comunità di utenti. Il ciclo vitale di un pacchetto su AUR comincia e finisce con l'utente e richiede il suo contributo in diversi modi.

Gli utenti possono **condividere** i PKGBUILD usando l'interfaccia di AUR. L'Arch User Repository non contiene nessun pacchetto compilato ma consente agli utenti di inviare i PKGBUILD così che possano essere scaricati dagli altri utenti. Questi PKGBUILD sono completamente *non ufficiali* e non sono stati controllati a fondo, quindi saranno usati a proprio rischio e pericolo.

### Aggiungere pacchetti

**Attenzione:** Prima di sottomettere un pacchetto ci si aspetta che tu abbia familiarizzato con [Arch Packaging Standards (Italiano)](/index.php/Arch_Packaging_Standards_(Italiano) "Arch Packaging Standards (Italiano)").

Dopo aver effettuato l'accesso sul sito di AUR, un utente può [spedire](https://aur.archlinux.org/pkgsubmit.php) un archivio tar compresso con gzip (`.tar.gz`) di una directory contenente i file necessari alla compilazione del pacchetto. La directory all'interno dell'archivio deve contenere un `PKGBUILD`, eventuali file `.install`, le patch, eccetera (**assolutamente** nessun file compilato). Un esempio di come questa cartella dovrebbe essere può essere trovato all'interno di `/var/abs` nel caso in cui sia stato installato [ABS](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)").

L'archivio può essere creato con il seguente comando:

```
$ makepkg --source 

```

Notare che questo pacchetto è compresso con gzip; presumendo che si stia inviando un pacchetto chiamato *libfoo*, quando verrà creato l'archivio dovrà essere simile a questo:

 `$ tar tf libfoo-0.1-1.src.tar.gz` 
```
libfoo/
libfoo/PKGBUILD
libfoo/libfoo.install
```

#### Regole per la sottomissione dei pacchetti

Quando si invia un pacchetto, attenersi alle seguenti regole:

*   Cercare il pacchetto nel [database ufficiale](https://www.archlinux.org/packages/). Se **una qualunque versione** è già presente, **non** inviare il pacchetto. Se il pacchetto ufficiale non è aggiornato, marcarlo con l'apposito link. Se il pacchetto ufficiale è danneggiato o privo di alcune funzionalità è raccomandato aprire un [bug report](https://bugs.archlinux.org/).
*   Controllare **AUR** alla ricerca del pacchetto. Nel caso in cui sia già mantenuto da un utente, lo si può contattare lasciando un commento. Se il pacchetto è orfano allora può essere adottato ed aggiornato se necessario. Non creare pacchetti "doppioni".
*   Verificare accuratamente che il file spedito sia quello giusto. Tutti gli utenti nello scrivere un PKGBUILD devono aver letto ed attenersi agli [standard di pacchettizazione di Arch](/index.php/Arch_Packaging_Standards_(Italiano) "Arch Packaging Standards (Italiano)"). Tutto questo è essenziale per il corretto funzionamento e per il successo di AUR. Ricordare che non si guadagnano né credito né rispetto dagli utenti facendo loro perdere tempo con pessimi PKGBUILD.
*   I pacchetti che contengono file compilati o scritti poco accuratamente possono essere cancellati senza preavviso.
*   Se non si è sicuri riguardo al pacchetto (oppure al processo di compilazione o di spedizione), inviare il PKGBUILD sulla [Mailing List di AUR](https://mailman.archlinux.org/mailman/listinfo/) o postarlo nelle apposite [sezioni di AUR](https://bbs.archlinux.org/viewforum.php?id=4) dei forum per ottenere consigli, prima di inviare il pacchetto su AUR.
*   Assicurarsi che il pacchetto abbia una utilità. Qualcun'altro vorrà usare questo pacchetto? Se un buon numero di utenti possono trovare utile il paccehtto, allora è appropriato per la spedizione.
*   L'AUR e i repository ufficiali sono concepiti per pacchetti che installano generalmente software e contenuti correlati, compresi uno o più tra i seguenti: eseguibili; file di configurazione; dcumentazione online o offline per software specifici o per la distribuzione Arch Linux intera; file multimediali utilizzati direttamente dal software.
*   Accumulare esperienza prima di spedire pacchetti. Compilare alcuni pacchetti per imparare il meccanismo ed allora spedirlo.
*   Se si spedisce `pacchetto.tar.gz` con all'interno un file di nome `pacchetto` si otterrà un errore: "Could not change to directory `/home/aur/unsupported/pacchetto/pacchetto`". Per evitare questo errore rinominare il file chiamato `pacchetto` ad esempio in `pacchetto.rc` o simili. Quando sarà estratto nella cartella `pkg` sarà possibile rinominarlo nuovamente come `pacchetto`. Assicurarsi di leggere anche [Arch Packaging Standards (Italiano)#Invio di pacchetti ad AUR](/index.php/Arch_Packaging_Standards_(Italiano)#Invio_di_pacchetti_ad_AUR "Arch Packaging Standards (Italiano)").

#### Creare un nuovo pacchetto

Per avere accesso in scrittura ad AUR, gli utenti hanno bisogno di avere una coppia di [SSH keys](/index.php/SSH_keys "SSH keys"). E' necessario copiare il contenuto della chiave pubblica nel profilo utente in *Il mio account*, e configurare la chiave privata corrispondente, per l'host `aur.archlinux.org`. Ad esempio:

 `~/.ssh/config` 
```
Host aur.archlinux.org
  IdentityFile ~/.ssh/aur
  User aur
```

Si raccomanda di [creare una nuova coppia](/index.php/SSH_keys#Generating_an_SSH_key_pair "SSH keys") piuttosto che usarne una esistente, in modo da poter revocare le chiavi selettivamente nel caso in cui succeda qualcosa.

Per inviare un pacchetto, è semplicemente necessario clonare il repository Git col nome corrispondente:

```
$ git clone ssh://aur@aur.archlinux.org/*foobar*.git

```

Eseguire il cloning, o il pushing, di un repository non esistente ne creerà automaticamente uno nuovo.

E' possibile adesso aggiungere i file sorgenti nella copia locale del repository Git. Quando si effettuano modifiche al repository, accertarsi di includere sempre il `PKGBUILD` e `.SRCINFO` nella directory di livello piu' alto. E' possibile creare file `.SRCINFO` usando `makepkg --printsrcinfo` (stampato sullo standard output) o utilizzando `mksrcinfo`, fornito da [pkgbuild-introspection](https://www.archlinux.org/packages/?name=pkgbuild-introspection) (scritto su file).

**Note:** `.SRCINFO` contiene metadata del pacchetto sorgente, vedere [#AUR metadata](#AUR_metadata) per i dettagli.

### Mantenere i pacchetti

*   Se si mantiene un pacchetto e si vuole aggiornare il PKGBUILD dello stesso, basta ripresentarlo.
*   Controllare le opinioni ed i commenti degli utenti, provare ad implementare eventuali miglioramenti suggeriti; considerare questa come una possibiltà per imparare!
*   Non spedire e poi dimenticarsi dei pacchetti! È responsabilità del "maintainer" mantenere e controllare il pacchetto, seguendo gli aggiornamenti ed ottimizzando il PKGBUILD.
*   Se non si vuole più mantenere un pacchetto per qualsiasi ragione, `abbandonare` il pacchetto dalla propria pagina sul sito di AUR e postare un messaggio sulla mailing list.

### Altri tipi di richieste

*   Le richieste di disconoscimento e di rimozione vanno inviate ad Aur General Mailing List dove i TU ed altri utenti decideranno.
*   **Includere il nome del pacchetto e l'URL alla pagina AUR**, preferibilmente con una nota [1].
*   Le richieste di disconoscimento saranno concesse due settimane dopo che l'attuale responsabile sia stato contattato via e-mail e non abbia risposto.
*   **La rinomina pacchetti non è ancora implementata**, così gli utenti devono ripresentare un pacchetto con un nuovo nome e richiedere la rimozione della vecchia versione alla mailing list.
*   Le richieste di rimozione necessitano delle seguenti informazioni:
    *   Nome del pacchetto e URL alla pagina AUR.
    *   Motivo della cancellazione, almeno una breve nota
        **Notice:** Anche se i commenti di un pacchetto sono motivo sufficiente per la cancellazione di un pacchetto. Non appena interviene un TU, l'unico luogo in cui tali informazioni possono essere ottenute è la aur generale mailing list.
    *   Includere dettagli informativi, ad esempio se il pacchetto è incluso da qualche altra parte, se si è il manutentore, se il pacchetto è rinominato e il proprietario originale è d'accordo, ecc.

Le richieste di rimozione possono essere disapprovate, nel qual caso probabilmente verrà consigliato di abbandonare il pacchetto per riferimento futuro.

## community

Il repository *community* è mantenuto dai [Trusted Users](/index.php/Trusted_Users "Trusted Users"), e contiene i pacchetti più famosi provenienti da AUR. E' abilitato di default in `pacman.conf`. Se fosse disabilitato o rimosso, può essere abilitato decommentando o aggiungendo queste due linee:

```
/etc/pacman.conf

```

```
...
[community]
Include = /etc/pacman.d/mirrorlist
...
```

Questo repository, contrariamente ad AUR, contiene pacchetti compilati che possono essere installati direttamente con [pacman](/index.php/Pacman "Pacman"), ed i file necessari alla compilazione sono reperibili tramite [ABS](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)"). Alcuni di questi pacchetti possono eventualmente essere trasferiti in *core* o in *extra* se gli sviluppatori li considerano necessari alla distribuzione.

Gli utenti possono accedere ai file per la compilazione dei pacchetti di *community* editando `/etc/abs.conf` ed abilitando il repository *community* all'interno dell'array `REPOS`.

## Git Repo

Un repository Git di AUR è mantenuto da Thomas Dziedzic, e fornisce, tra le altre cose, lo storico dei pacchetti. Viene aggiornato almeno una volta al giorno. Per clonare il repository (varie centinaia di MB):

```
$ git clone git://pkgbuild.com/aur.git

```

Per maggiori informazioni: [interfaccia web](http://pkgbuild.com/git/aur.git/), [forum thread](https://bbs.archlinux.org/viewtopic.php?id=113099)

## FAQ

### Cos'è AUR?

AUR (Arch User Repository) è una locazione dove la comunità di ArchLinux può mandare i [PKGBUILD](/index.php/PKGBUILD_(Italiano) "PKGBUILD (Italiano)") di applicazioni, librerie, etc. e condividerli con l'intera comunità. Gli altri utenti possono votare i loro favoriti per proporne lo spostamento nei repository *community* in modo da essere diffusi in formato binario.

### Che tipo di pacchetti sono permessi su AUR?

I pacchetti di AUR sono semplicemente degli "script di compilazione", ossia le istruzioni per compilare i binari per pacman. Nella maggior parte dei casi non ci sono limitazioni, se non le sopracitate linee guida sull'utilità e la finalità, e la richiesta di conformità con i termini di licenza del contenuto. In alcuni casi, quando si menziona che "non si può collegare il link" del download, come quando il contenuto non è ridistribuibile, si può utilizzare solo il nome del file stesso come fonte. Questo significa che gli utenti devono avere già i sorgenti nella directory indicata prima di iniziare il processo di compilazione del pacchetto. In caso di dubbi, chiedere.

### Come si votano i pacchetti in AUR?

Registrando un account sul [website di AUR](https://aur.archlinux.org/) si abilita un link per votare un pacchetto nella rispettiva pagina.

### Cos'è un TU?

Un [TU (Trusted User)](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines") è una persona che è stata scelta per supervisionare l'AUR e i repository *community*. Sono coloro che mantengono PKGBUILDs famosi in *community*, segnano quali PKGBUILDs sono sicuri e, soprattutto, fanno funzionare AUR.

### Che differenza c'è tra Arch User Repository e community?

L'Arch User Repository è il sito che contiene i PKGBUILDs inviati dagli utenti; essi devono essere compilati manualmente con [makepkg](/index.php/Makepkg_(Italiano) "Makepkg (Italiano)"). Quando un PKGBUILD riceve sufficiente interesse dalla comunità e il supporto di un Trusted User, viene spostato nel repository *community* (gestito dai TU), da dove il pacchetto binario può essere installato con [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)").

### Quanti voti servono per far spostare un PKGBUILD in community?

Di solito, sono richiesti almeno 10 voti per spostare qualcosa in *community*. Comunque, se un TU vuole mantenere un pacchetto, sarà possibile trovarlo in *community*.

### Come si fa un PKGBUILD?

Guarda la voce [Creating Packages (Italiano)](/index.php/Creating_Packages_(Italiano) "Creating Packages (Italiano)"). Ricorda di guardare su AUR se c'è già il PKGBUILD che cerchi.

### Ho dato il comando "pacman -S foo"; non funziona, ma sono sicuro che si trova in community

Probabilmente non hai abilitato il repository *community* in `/etc/pacman.conf`. È sufficiente decommentare le relative linee. Se *community* è abilitato in `/etc/pacman.conf` provare per prima cosa ad eseguire `pacman -Syu` per sincronizzare la pkgcache e aggiornare il sistema prima di provare nuovamente ad installare "foo".

### In AUR, un pacchetto non è aggiornato; cosa devo fare?

Innanzitutto puoi segnalare il pacchetto come out-of-date. Se rimane out-of-date per molto tempo, la cosa migliore da fare è mandare un'email al mantainer. Se non c'è risposta dal mantainer, puoi mandare una mail alla mailing list aur-general per chiedere a un Trusted User di rendere orfano quel PKGBUILD. Se vuoi, puoi chiedere di essere tu a mantenere quel PKGBUILD. Nel caso di pacchetti segnalati come out-of-date da più di 3 mesi o in generale non aggiornati da molto tempo, si prega di aggiungere quest'informazione nella richiesta.

### Ho un PKGBUILD che vorrei inviare; qualcuno può controllarlo per vedere se ci sono errori?

Puoi chiedere sulla mailing list aur-general, in modo da ricevere pareri dai Trusted User e da altri utenti di AUR. Puoi anche andare su [IRC](/index.php/ArchChannel "ArchChannel"), #archlinux su irc.freenode.net. [namcap](/index.php/Namcap "Namcap"), infine, controllerà il tuo PKGBUILD e il pacchetto generato, segnalando eventuali errori.

### Il pacchetto Foo in AUR non compila quando lancio makepkg; cosa dovrei fare?

Probabilmente hai dimenticato qualcosa:

1.  Lancia `pacman -Syyu` prima di compilare, dato che il problema potrebbe essere nel non aver aggiornato il tuo sistema.
2.  Controlla di aver installato sia il gruppo "base" sia "base-devel".
3.  Prova ad usare l'opzione "`-s`" di `makepkg` per controllare e installare le dipendenze necessarie prima di iniziare la compilazione.

Il motivo, comunque, potrebbe non essere banale. CFLAGS, LDFLAGS e MAKEFLAGS personalizzati possono causare errori. È anche possibile che il PKGBUILD sia semplicemente buggato. Se non riesci a capire qual è il problema, fallo presente al mantainer.

### Come posso accelerare i ripetuti processi di compilazione?

Se compili frequentemente del codice che utiliza `gcc` come ad esempio pacchetti git o SVN - puoi trovare utile utilizzare [ccache](/index.php/Ccache "Ccache"), abbreviazione di "compiler cache".

### Come faccio ad accedere ai pacchetti di unsupported

Leggi [#Installare i pacchetti da AUR](#Installare_i_pacchetti_da_AUR).

### Come faccio a mandare un PKGBUILD ad AUR senza usare l'interfaccia web?

Puoi usare [burp](https://www.archlinux.org/packages/?name=burp), *aurploader* ([python3-aur](https://aur.archlinux.org/packages/python3-aur/)) o [aurup](https://aur.archlinux.org/packages/aurup/), tutti con interfaccia da linea di comando.

## AUR 4

Dalla vesione 4.0.0, aurweb userà dei repository Git per i pacchetti AUR e questo implica che il processo per l'invio dei pacchetti sarà differente. Mentre [aur.archlinux.org](https://aur.archlinux.org/) continua ad utilizzare aurweb 3.5.1, un versione release candidate di aurweb 4.0.0 è disponibile all'indirizzo [aur4.archlinux.org](https://aur4.archlinux.org/). I manutentori dei pacchetti AUR dovranno migrare i propri pacchetti da [aur.archlinux.org](https://aur.archlinux.org/) a [aur4.archlinux.org](https://aur4.archlinux.org/) nel periodo compreso tra l'8 Giugno e l'8 Luglio. L'8 agosto, [aur4.archlinux.org](https://aur4.archlinux.org/) diventerà il nuovo AUR ufficiale (e verrà quindi spostato al sottodominio *aur*).

### Prima di inviare i pacchetti ad aur4.archlinux.org

Prima di inviare per la prima volta un pacchetto, è necessario creare una nuova coppia di chiavi SSH. Si consiglia di creare una nuova coppia di chiavi, invece di utilizzarne una esistente, in modo che si possa revocarla selettivamente in caso di necessità.

Per creare una nuova coppia di chiavi SSH, usare il comando:

```
$ ssh-keygen -f ~/.ssh/id_rsa-aur

```

Accedere quindi all'interfaccia web dell'AUR, spostarsi nella sezione *My Account* e copiare il contenuto di `~/.ssh/id_rsa-aur.pub` (o di qualsiasi altra chiave si voglia utilizzare) nel campo *SSH Public Key*. Infine cliccare *Update* per salvare la chiave. Si consiglia anche di aggiungere le seguenti linee al file `~/.ssh/config` così da non dover specificare quale utente e chiave utilizzare ogni qualvolta ci si connette all'interfaccia SSH dell'AUR:

```
Host aur4.archlinux.org
IdentityFile ~/.ssh/id_rsa-aur
User aur

```

### Inviare i pacchetti ad aur4.archlinux.org

**Attenzione:** Prima di inviare un pacchetto è opportuno familiarizzare con l'[Arch Packaging Standards](/index.php/Arch_Packaging_Standards_(Italiano) "Arch Packaging Standards (Italiano)") e leggere tutti gli articoli in esso menzionati

Per inviare un pacchetto, basta semplicemente clonare il repository Git con il nome corrispondente:

```
$ git clone aur@aur4.archlinux.org:/*foobar*.git

```

oppure, equivalentemente

```
$ git clone ssh://aur@aur4.archlinux.org/*foobar*.git

```

Si possono quindi aggiungere i file sorgenti alla copia locale del repository Git. Quando si effettuano modifiche al repository, bisogna fare attenzione che nella directory principale siano sempre presenti i file `PKGBUILD` e `.SRCINFO`. Il file `.SRCINFO` può essere generato usando `mksrcinfo`, fornito da [pkgbuild-introspection-git](https://aur.archlinux.org/packages/pkgbuild-introspection-git/). Per inviare una nuova versione del pacchetto basta effettuare un commit contenete dei nuovi `PKGBUILD`, `.SRCINFO` e, se necessario, dei file aggiuntivi (come lo script di installazione) ed eseguire il comando `git push`. Per esempio, dopo aver aggiunto il `PKGBUILD` al repository appena creato, si possono eseguire i seguenti comandi per creare la commit iniziale:

```
$ mksrcinfo
$ git add PKGBUILD .SRCINFO
$ git commit -m 'Initial import'
$ git push

```

Per aggiornare un pacchetto invece, basta aggiornare il `PKGBUILD` ed eseguire i comandi seguenti per aggiornare inviare cambiamenti al repository Git nell'AUR:

```
$ mksrcinfo
$ git commit -am 'Update to *1.0.0'*
$ git push

```

### Script per la migrazione

Esistono diversi script per facilitare la migrazione da AUR ad AUR4:

*   [bbidulock's script](https://gist.github.com/bbidulock/82ab6f5347f021136054) to migrate from a .backup directory with all packages.
*   [aur2git](https://github.com/voidus/aur2git) - A ruby gem to download and submit your existing packages.
*   [import-to-aur4](https://github.com/ido/packages-archlinux/blob/master/bin/import-to-aur4.sh) to split an existing single git repository and retain the history.

Si noti comunque che sono tutti creati da altri utenti e che quindi nessuno di essi e ufficialmente supportato!

## Altre risorse

*   [AUR Web Interface](https://aur.archlinux.org)
*   [AUR Mailing List](https://www.archlinux.org/mailman/listinfo/aur-general)