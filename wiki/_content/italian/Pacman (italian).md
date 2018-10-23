Articoli correlati

*   [Downgrading Packages (Italiano)](/index.php/Downgrading_Packages_(Italiano) "Downgrading Packages (Italiano)")
*   [Improve Pacman Performance (Italiano)](/index.php/Improve_Pacman_Performance_(Italiano) "Improve Pacman Performance (Italiano)")
*   [Pacman GUI Frontends (Italiano)](/index.php/Pacman_GUI_Frontends_(Italiano) "Pacman GUI Frontends (Italiano)")
*   [Pacman Rosetta](/index.php/Pacman_Rosetta "Pacman Rosetta")
*   [Pacman Tips (Italiano)](/index.php/Pacman_Tips_(Italiano) "Pacman Tips (Italiano)")
*   [Pacman package signing](/index.php/Pacman_package_signing "Pacman package signing")
*   [FAQ (Italiano)#Package Management](/index.php/FAQ_(Italiano)#Package_Management "FAQ (Italiano)")

*   [pacman-key (Italiano)](/index.php/Pacman-key_(Italiano) "Pacman-key (Italiano)")
*   [Pacnew and Pacsave Files (Italiano)](/index.php/Pacnew_and_Pacsave_Files_(Italiano) "Pacnew and Pacsave Files (Italiano)")
*   [List of Applications/Utilities (Italiano)#Gestori di pacchetti](/index.php/List_of_Applications/Utilities_(Italiano)#Gestori_di_pacchetti "List of Applications/Utilities (Italiano)")
*   [Arch Build System (Italiano)](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)")
*   [Official Repositories (Italiano)](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)")
*   [Arch User Repository (Italiano)](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)")

Il [gestore di pacchetti](https://en.wikipedia.org/wiki/it:Sistema_di_gestione_dei_pacchetti o compilati dall'utente stesso.

Pacman può tenere un sistema aggiornato sincronizzando le liste di pacchetti con il server principale. Questo modello server/client permette all'utente anche di scaricare/installare pacchetti con un semplice comando, completi di tutte le dipendenze richieste.

Pacman è sviluppato in C, e utilizza il formato `.pkg.tar.xz`.

**Suggerimento:** Il pacchetto ufficiale [pacman](https://www.archlinux.org/packages/?name=pacman) contiene anche altri strumenti utili, come **makepkg**, **pactree**, **vercmp** ed altri. È possibile ottenere la lista completa con `pacman -Ql pacman | grep bin`

## Contents

*   [1 Configurazione](#Configurazione)
    *   [1.1 Opzioni generali](#Opzioni_generali)
        *   [1.1.1 Evitare l'aggiornamento di un pacchetto](#Evitare_l.27aggiornamento_di_un_pacchetto)
        *   [1.1.2 Evitare l'aggiornamento di un gruppo di pacchetti](#Evitare_l.27aggiornamento_di_un_gruppo_di_pacchetti)
        *   [1.1.3 Evitare l'installazione di file nel sistema](#Evitare_l.27installazione_di_file_nel_sistema)
    *   [1.2 Repository](#Repository)
    *   [1.3 Sicurezza dei pacchetti](#Sicurezza_dei_pacchetti)
*   [2 Uso](#Uso)
    *   [2.1 Installare pacchetti](#Installare_pacchetti)
        *   [2.1.1 Installare pacchetti specifici](#Installare_pacchetti_specifici)
        *   [2.1.2 Installare gruppi di pacchetti](#Installare_gruppi_di_pacchetti)
    *   [2.2 Rimuovere i Pacchetti](#Rimuovere_i_Pacchetti)
    *   [2.3 Aggiornare il sistema](#Aggiornare_il_sistema)
    *   [2.4 Interrogare il database dei pacchetti](#Interrogare_il_database_dei_pacchetti)
    *   [2.5 Comandi addizionali](#Comandi_addizionali)
    *   [2.6 Gli aggiornamenti parziali non sono supportati](#Gli_aggiornamenti_parziali_non_sono_supportati)
    *   [2.7 Note generali](#Note_generali)
*   [3 Risoluzione di problemi](#Risoluzione_di_problemi)
    *   [3.1 L'aggiornamento del pacchetto XYZ ha corrotto il mio sistema!](#L.27aggiornamento_del_pacchetto_XYZ_ha_corrotto_il_mio_sistema.21)
    *   [3.2 So che un aggiornamento del pacchetto ABC è stato rilasciato, ma pacman mi dice che il mio sistema è aggiornato!](#So_che_un_aggiornamento_del_pacchetto_ABC_.C3.A8_stato_rilasciato.2C_ma_pacman_mi_dice_che_il_mio_sistema_.C3.A8_aggiornato.21)
    *   [3.3 Aggiornando il sistema ottengo l'errore: "file exists in filesystem"!](#Aggiornando_il_sistema_ottengo_l.27errore:_.22file_exists_in_filesystem.22.21)
    *   [3.4 Ottengo un errore quando si installa un pacchetto: "not found in sync db"](#Ottengo_un_errore_quando_si_installa_un_pacchetto:_.22not_found_in_sync_db.22)
    *   [3.5 Ottengo un errore quando si installa un pacchetto: "target not found"](#Ottengo_un_errore_quando_si_installa_un_pacchetto:_.22target_not_found.22)
    *   [3.6 Pacman mi richiede ripetutamente di aggiornare lo stesso pacchetto!](#Pacman_mi_richiede_ripetutamente_di_aggiornare_lo_stesso_pacchetto.21)
    *   [3.7 Pacman va in crash durante un aggiornamento!](#Pacman_va_in_crash_durante_un_aggiornamento.21)
    *   [3.8 Ho installato un programma utilizzando "make install"; questi file non appartengono ad alcun pacchetto!](#Ho_installato_un_programma_utilizzando_.22make_install.22.3B_questi_file_non_appartengono_ad_alcun_pacchetto.21)
    *   [3.9 Ho bisogno di un pacchetto con un file specifico. Come faccio a sapere da quale viene fornito?](#Ho_bisogno_di_un_pacchetto_con_un_file_specifico._Come_faccio_a_sapere_da_quale_viene_fornito.3F)
    *   [3.10 Pacman è completamente fuori uso! Come faccio a reinstallarlo?](#Pacman_.C3.A8_completamente_fuori_uso.21_Come_faccio_a_reinstallarlo.3F)
    *   [3.11 Dopo aver aggiornato il sistema e riavviato, ottengo l'errore "unable to find root device" e il sistema non riesce più ad avviarsi.](#Dopo_aver_aggiornato_il_sistema_e_riavviato.2C_ottengo_l.27errore_.22unable_to_find_root_device.22_e_il_sistema_non_riesce_pi.C3.B9_ad_avviarsi.)
    *   [3.12 Signature from "User <email@gmail.com>" is unknown trust, installation failed](#Signature_from_.22User_.3Cemail.40gmail.com.3E.22_is_unknown_trust.2C_installation_failed)
    *   [3.13 Continuo ad ottenere "PackageName: signature from "User <email@archlinux.org>" is invalid"](#Continuo_ad_ottenere_.22PackageName:_signature_from_.22User_.3Cemail.40archlinux.org.3E.22_is_invalid.22)
    *   [3.14 Continuo ad ottenere l'errore "failed to commit transaction (invalid or corrupted package)"](#Continuo_ad_ottenere_l.27errore_.22failed_to_commit_transaction_.28invalid_or_corrupted_package.29.22)
    *   [3.15 Ogni volta che uso pacman ottengo l'errore 'warning: current locale is invalid; using default "C" locale'. Cosa faccio?](#Ogni_volta_che_uso_pacman_ottengo_l.27errore_.27warning:_current_locale_is_invalid.3B_using_default_.22C.22_locale.27._Cosa_faccio.3F)
    *   [3.16 Come posso fare in modo che pacman usi la mia configurazione per un proxy?](#Come_posso_fare_in_modo_che_pacman_usi_la_mia_configurazione_per_un_proxy.3F)
    *   [3.17 Come reinstallare tutti i pacchetti, mantenendo memoria di quali pacchetti sono installati esplicitamente e quali come dipendenze?](#Come_reinstallare_tutti_i_pacchetti.2C_mantenendo_memoria_di_quali_pacchetti_sono_installati_esplicitamente_e_quali_come_dipendenze.3F)
*   [4 Altre risorse](#Altre_risorse)

## Configurazione

La configurazione di Pacman è situata in `/etc/pacman.conf`. Questo è il file su cui l'utente configura il programma per farlo funzionare nel modo desiderato. Ulteriori informazioni riguardo il file di configurazione possono essere trovate in [man pacman.conf](https://www.archlinux.org/pacman/pacman.conf.5.html).

### Opzioni generali

Le opzioni generali si trovano nella sezione `[options]` . Consultare la pagina di man o nel `pacman.conf` predefinito per ulteriori informazioni.

#### Evitare l'aggiornamento di un pacchetto

Per evitare che un pacchetto venga aggiornato, specificarlo nell'apposita stringa:

```
IgnorePkg=linux

```

Per ignorare l'aggiornamento di più pacchetti, separarli con uno spazio, oppure utilizzare ulteriori linee `IgnorePkg`.

#### Evitare l'aggiornamento di un gruppo di pacchetti

Così come per un singolo pacchetto, è possibile ignorare l'aggiornamento anche dei pacchetti che sono individuati da un gruppo:

```
IgnoreGroup=gnome

```

#### Evitare l'installazione di file nel sistema

Per evitare l'installazione di specifici file o cartelle, elencarle con `NoExtract`. Ad esempio, per evitare l'installazione delle unità di [systemd](/index.php/Systemd "Systemd"), usare:

```
NoExtract=usr/lib/systemd/system/*

```

### Repository

In questa sezione si può definire quali [repository](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)") usare, come specificato in `/etc/pacman.conf`. Possono essere specificati direttamente qui oppure aggiunti da un altro file (ad esempio `/etc/pacman.d/mirrorlist`), rendendo così necessario mantenere una sola lista. Consultare [questo articolo](/index.php/Mirrors_(Italiano) "Mirrors (Italiano)") per la configurazione dei mirror.

 `/etc/pacman.conf` 
```
#[testing]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

[core]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

[extra]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

#[community-testing]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

[community]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist
# If you want to run 32 bit applications on your x86_64 system,
# enable the multilib repositories as required here.

#[multilib-testing]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

#[multilib]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

# An example of a custom package repository.  See the pacman manpage for
# tips on creating your own repositories.
#[custom]
#SigLevel = Optional TrustAll
#Server = file:///home/custompkgs
```

**Attenzione:** Si deve prestare attenzione quando si utilizza il repository *testing*. Dato che è in continuo sviluppo, gli aggiornamenti possono causare il malfunzionamento di alcuni pacchetti. Gli utenti che usano il repository *testing* sono invitati ad iscriversi alla [mailing list arch-dev-public](https://mailman.archlinux.org/mailman/listinfo/arch-dev-public/) per ottenere informazioni aggiornate.

### Sicurezza dei pacchetti

Pacman 4 supporta i pacchetti firmati, aggiungendo così un ulteriore livello di sicurezza. `SigLevel` può essere usato a livello globale o configurato per ogni repository. La configurazione di default, `SigLevel = Required DatabaseOptional`, abilita la verifica delle firme per tutti i pacchetti a livello globale: questo comportamento può essere cambiato definendo `SigLevel` per ogni repository come mostrato sopra. Per ulteriori dettagli sulle firme dei pacchetti e la loro verifica, consultare [pacman-key](/index.php/Pacman-key_(Italiano) "Pacman-key (Italiano)").

## Uso

Ciò che segue è solo una piccola parte delle operazioni che pacman può eseguire. Per avere altri esempi, consultare [man pacman](https://www.archlinux.org/pacman/pacman.8.html).

### Installare pacchetti

#### Installare pacchetti specifici

Per installare o aggiornare un singolo pacchetto o una lista di pacchetti (incluse le dipendenze), dare il seguente comando:

```
# pacman -S *nome_pacchetto1* *nome_pacchetto2* ...

```

Qualche volta ci sono più versioni di uno stesso pacchetto in differenti repository, ad esempio, *extra* e *testing*. Per installare la versione precedente bisogna specificare il nome del repository:

```
# pacman -S extra/*nome_pacchetto*

```

#### Installare gruppi di pacchetti

Alcuni pacchetti appartengono ad un gruppo, e possono essere installati contemporaneamente. Per esempio, il comando:

```
# pacman -S gnome

```

chiederà di selezionare i pacchetti del gruppo [gnome](https://www.archlinux.org/groups/x86_64/gnome/) che si desidera installare.

In alcuni casi un gruppo contiene un grande numero di pacchetti, e tra questi si potrebbero voler selezionare o deselezionare solamente pochi. Invece di dover digitare tutti i numeri eccetto quelli indesiderati, può essere più semplice selezionare o escludere pacchetti o intervalli di pacchetti con la seguente sintassi:

```
Enter a selection (default=all): 1-10 15

```

che selezionerà per l'installazione i pacchetti da 1 a 10 e 15, oppure:

```
Enter a selection (default=all): ^5-8 ^2

```

che selezionerà per l'installazione tutti i pacchetti eccetto da 5 a 8, né 2.

Si possono visualizzare quali pacchetti appartengono al gruppo gnome eseguendo:

```
# pacman -Sg gnome

```

È inoltre possibile visitare [https://www.archlinux.org/groups/](https://www.archlinux.org/groups/) per vedere quali gruppi di pacchetti sono disponibili.

**Nota:** Se un pacchetto nella lista è già installato sul sistema, verrà reinstallato anche se aggiornato, a meno che non si utilizzi l'opzione `--needed`.

**Attenzione:** Quando si installano dei pacchetti, **non** aggiornare l'elenco dei pacchetti senza [aggiornare](#Aggiornare_il_sistema) il sistema (cioè `pacman -Sy *nome_pacchetto*`); questo può portare a problemi con le dipendenze. Leggere [#Gli aggiornamenti parziali non sono supportati](#Gli_aggiornamenti_parziali_non_sono_supportati) e [[1]](https://bbs.archlinux.org/viewtopic.php?id=89328).

### Rimuovere i Pacchetti

Per rimuovere un singolo pacchetto, lasciando tutte le sue dipendenze installate:

```
# pacman -R *nome_pacchetto*

```

Per rimuovere tutte le dipendenze del pacchetto che non sono usate da nessun'altro pacchetto installato:

```
# pacman -Rs *nome_pacchetto*

```

Per rimuovere un pacchetto, le sue dipendenze e tutti i pacchetti che da esso dipendono:

**Attenzione:** Quest'operazione è ricorsiva, e deve essere usata con cautela in quanto può rimuovere molti pacchetti potenzialmente ancora necessari.

```
# pacman -Rsc *nome_pacchetto*

```

Per rimuovere un pacchetto richiesto da un altro pacchetto, senza rimuovere il pacchetto dipendente:

```
# pacman -Rdd *nome_pacchetto*

```

Pacman salva i file di configurazione importanti durante la rimozione di determinate applicazioni e li rinomina con l'estensione: `.pacsave`. Per evitare che questi file di backup siano creati utilizzare l'opzione `-n`:

```
# pacman -Rn *nome_pacchetto*

```

**Nota:** Pacman non rimuoverà le configurazioni create dall'applicazione stessa (per esempio i file nascosti nella cartella dell'utente).

### Aggiornare il sistema

Pacman può aggiornare tutti i pacchetti del sistema con un solo comando. Questo processo può durare parecchio tempo, in relazione a quanto aggiornato è il sistema. Questo comando può sincronizzare i database dei repository ed aggiornare i pacchetti del sistema (eccetto i pacchetti "locali" che non si trovano nei repository configurati):

```
# pacman -Syu

```

**Attenzione:** Invece di aggiornare sempre immediatamente appena sono disponibili degli aggiornamenti, è bene tenere conto che essendo Arch una distribuzione rolling release, un aggiornamento può avere conseguenze impreviste. Questo significa che non è consigliabile eseguire un aggiornamento se per esempio si avrà bisogno a breve di un sistema stabile per motivi di lavoro; molto meglio aggiornare durante il tempo libero, per poter eventualmente avere il tempo e la calma per risolvere possibili insorgenze.

Pacman è un potente strumento di gestione dei pacchetti, ma non è progettato per gestire e risolvere automaticamente ogni possibile problema. Consultare [The Arch Way](/index.php/The_Arch_Way_(Italiano) "The Arch Way (Italiano)") se non fosse ben chiara la filosofia KISS alla base di Arch. Piuttosto, gli utenti devono essere attenti e assumersi la responsabilità della manutenzione del proprio sistema. **Quando si esegue un aggiornamento del sistema, è essenziale che gli utenti leggano tutte le informazioni generate dall'output di pacman ed usino il proprio buon senso.** Se un file di configurazione modificato dall'utente deve essere aggiornato per una nuova versione di un pacchetto, pacman creerà un file `.pacnew` per evitare di sovrascrivere la configurazione modificata dall'utente. Sarà poi chiesto all'utente di fondere i due file. Questo richiede un intervento manuale dell'utente, ed è buona prassi farlo immediatamente dopo aver aggiornato o rimosso un pacchetto. Leggere [Pacnew and Pacsave Files](/index.php/Pacnew_and_Pacsave_Files_(Italiano) "Pacnew and Pacsave Files (Italiano)") per avere maggiori informazioni.

**Suggerimento:** Si ricorda che l'output di pacman viene salvato nel file di log `/var/log/pacman.log`.

Prima di un aggiornamento è caldamente consigliato leggere le ultime notizie sulla [home page di Arch Linux](http://www.archlinux.it/) (o iscriversi al [feed RSS](http://www.archlinux.it/forum/feed.php), alla [mailing list arch-announce](https://mailman.archlinux.org/mailman/listinfo/arch-announce/), o seguire [@archlinux](https://twitter.com/archlinux) su Twitter): quando gli aggiornamenti richiedono interventi straordinari dell'utente (più di quanto sia esplicitamente richiesto dalle istruzioni fornite da pacman), verrà aggiunta una segnalazione nelle *Ultime Notizie*.

Se si incontrano problemi che non possono essere risolti con queste istruzioni, assicurarsi di cercare nei forum. È probabile che altri abbiano avuto il medesimo problema ed abbiano pubblicato la soluzione per risolverlo.

### Interrogare il database dei pacchetti

Pacman può interrogare il database locale dei pacchetti con l'opzione `-Q`; vedere:

```
$ pacman -Q --help

```

e può interrogare i database sincronizzati con l'opzione `-S`; vedere:

```
$ pacman -S --help

```

Pacman può cercare pacchetti nel database, sia in base al nome del pacchetto che alla sua descrizione:

```
$ pacman -Ss *stringa1* *stringa2* ...

```

Per cercare i pacchetti già installati:

```
$ pacman -Qs *stringa1* *stringa2* ...

```

Per visualizzare informazioni dettagliate su un determinato pacchetto:

```
$ pacman -Si *pacchetto*

```

Per i pacchetti installati localmente:

```
$ pacman -Qi *pacchetto*

```

Con la doppia opzione `-i` si visualizza anche l'elenco dei file di backup e il loro stato di modifica:

```
$ pacman -Qii *pacchetto*

```

Per recuperare un elenco dei file installati da un pacchetto:

```
$ pacman -Ql *pacchetto*

```

Per i pacchetti non installati, usare [pkgfile](/index.php/Pkgfile "Pkgfile").

Si può anche interrogare il database per sapere a quale pacchetto appartiene un determinato file nel sistema:

```
$ pacman -Qo */percorso/al/nome_del_file*

```

Per elencare tutti i pacchetti non più necessari come dipendenze (orfani):

```
$ pacman -Qdt

```

Per mostrare l'albero delle dipendenze di un pacchetto:

```
$ pactree *pacchetto*

```

Per elencare tutti i pacchetti che dipendono da uno specifico pacchetto già installato, usare `whoneeds` da [pkgtools](/index.php/Pkgtools "Pkgtools"):

```
$ whoneeds *pacchetto*

```

### Comandi addizionali

Aggiornare il sistema e installare una lista di pacchetti (one-liner):

```
# pacman -Syu *pacchetto1* *pacchetto2* ...

```

Scaricare un pacchetto senza installarlo:

```
# pacman -Sw *pacchetto*

```

Installare un pacchetto "locale" che non proviene da un repository remoto (ad esempio il pacchetto viene dall'[AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)")):

```
# pacman -U /percorso/al/pacchetto/nomepacchetto-versione.pkg.tar.xz

```

**Suggerimento:** Per tenere una copia del pacchetto locale nella cache di pacman, usare:
```
# pacman -U file://path/to/package/package_name-version.pkg.tar.xz

```

Installare un pacchetto "remoto" (non dai repository definiti in pacman.conf):

```
# pacman -U http://www.example.com/repo/example.pkg.tar.xz

```

Per ripulire la cache dei pacchetti scaricati ed attualmente non installati (`/var/cache/pacman/pkg`):

**Attenzione:** Eseguire quest'operazione solo se si è certi che i pacchetti installati siano stabili e non ci sia bisogno di eseguire eventuali [downgrade](/index.php/Downgrading_packages "Downgrading packages"), dato che tutte le vecchie versioni dalla cartella della cache, lasciando solamente le versioni dei pacchetti attualmente installate. Avere le vecchie versioni dei pacchetti può tornare utile in caso un futuro aggiornamento causi un malfunzionamento.

```
# pacman -Sc

```

Svuota completamente l'intera cache dei pacchetti:

**Attenzione:** Quest'operazione svuota l'intera cache dei pacchetti. Questa è una pratica poco raccomandabile: rende impossibile eseguire il downgrade di un pacchetto direttamente dalla cache. Si sarà forzati ad usare una fonte alternativa di pacchetti obsoleti come l'[Arch Rollback Machine](/index.php/Downgrading_packages#Arch_Rollback_Machine "Downgrading packages").

```
# pacman -Scc

```

**Suggerimento:** Come alternativa alle modalità `-Sc` e `-Scc`, valutare la possibilità di usare `paccache` in [pacman](https://www.archlinux.org/packages/?name=pacman). Questo script offre un controllo maggiore su quanti e quali pacchetti vengono eliminati. Eseguire `paccache -h` per istruzioni.

### Gli aggiornamenti parziali non sono supportati

Arch Linux è rolling release, e le nuove versioni delle [librerie](https://en.wikipedia.org/wiki/Library_(computing) saranno aggiunte al repository. Gli sviluppatori e i Trusted Users ricompileranno conseguentemente tutti i pacchetti interessati nei repository. Se sono stati installati localmente dei pacchetti (come quelli da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)")), sarà necessario ricompilarli da soli quando le loro dipendenze ricevono modifiche a livello [soname](https://en.wikipedia.org/wiki/soname "wikipedia:soname").

Ciò significa che gli aggiornamenti parziali **non sono supportati**. Non usare `pacman -Sy pacchetto` o equivalenti, come `pacman -Sy` e poi `pacman -S pacchetto`. Aggiornare sempre il sistema prima di installare un pacchetto, specialmente se precedentemente è stata eseguita una sincronizzazione con i repository. Si dovrebbe anche, per lo stesso motivo, essere molto attenti quando si usano `IgnorePkg` e `IgnoreGroup`.

Se si esegue un aggiornamento parziale e i binari smettono di funzionare perché non riescono a trovare le librerie corrette, **non provare a risolvere semplicemente creando dei link simbolici**. Le librerie ricevono modifiche [soname](https://en.wikipedia.org/wiki/soname "wikipedia:soname") quando **non sono retrocompatibili**. Un semplice `pacman -Syu` ad un mirror ben sincronizzato risolverà il problema, a meno che pacman stesso sia corrotto.

### Note generali

**Attenzione:** Usare l'opzione `--force` con estrema cautela dato che può causare seri problemi se adoperata incorrettamente. È fortmente raccomandato usarla *solamente* quando le Arch news lo richiedono esplicitamente.

## Risoluzione di problemi

### L'aggiornamento del pacchetto XYZ ha corrotto il mio sistema!

Arch Linux è una distribuzione rolling-release all'avanguardia. Gli aggiornamenti dei pacchetti sono disponibili non appena sono considerati abbastanza stabili per un uso generale. Tuttavia, gli aggiornamenti a volte richiedono l'intervento dell'utente: i file di configurazione possono avere bisogno di essere aggiornati, le dipendenze opzionali possono cambiare, ecc.

La cosa più importante da ricordare è quella di non aggiornare "alla cieca" il sistema. Leggere sempre l'elenco dei pacchetti da aggiornare. Si presti particolare attenzione quando si opera ad aggiornare dei pacchetti "critici" ([linux](https://www.archlinux.org/packages/?name=linux), [xorg-server](https://www.archlinux.org/packages/?name=xorg-server), e così via). In questa situazione è una buona consuetudine verificare eventuali news su [https://www.archlinux.org/](https://www.archlinux.org/) e controllare anche il forum, per vedere se le persone incontrano problemi a causa di un aggiornamento.

Se l'aggiornamento di un pacchetto già prevede dei cambiamenti o è noto che potrebbe causare dei problemi, i responsabili del pacchetto faranno in modo che pacman visualizzi un messaggio appropriato quando viene aggiornato. Se l'aggiornamento non va a buon fine, controllare il log di pacman per riscontrare eventuali messaggi e procedere ad una prima analisi del problema (`/var/log/pacman.log`).

A questo punto,**solo dopo essersi assicurati che non ci sono informazioni disponibili tramite pacman, non ci sono notizie relative su [https://www.archlinux.org/](https://www.archlinux.org/), e non ci sono messaggi nel forum inerenti al proprio problema**, si dovrebbe prendere in considerazione di cercare aiuto sul forum, su [IRC](/index.php/IRC_channel "IRC channel") oppure optare per un [downgrade del pacchetto](/index.php/Downgrading_packages_(Italiano) "Downgrading packages (Italiano)").

### So che un aggiornamento del pacchetto ABC è stato rilasciato, ma pacman mi dice che il mio sistema è aggiornato!

Molto semplicemente questo avviene perchè i vari mirror non sono sincronizzati immediatamente: è possibile che passino anche più di 24 ore affinché un pacchetto sia disponibile nel proprio mirror. Le uniche opzioni sono essere pazienti o utilizzare un altro mirror. [MirrorStatus](https://www.archlinux.org/mirrors/status/) può essere d'aiuto per identificare i mirror aggiornati.

### Aggiornando il sistema ottengo l'errore: "file exists in filesystem"!

*Tratto da [https://bbs.archlinux.org/viewtopic.php?id=56373](https://bbs.archlinux.org/viewtopic.php?id=56373) di Misfit138.*

```
error: could not prepare transaction
error: failed to commit transaction (conflicting files)
package: /path/to/file exists in filesystem
Errors occurred, no packages were upgraded.

```

Il motivo per cui questo accade è che pacman ha rilevato un conflitto tra file, e, per come è stato programmato, non sovrascriverà i file da sé. Si tratta di un comportamento volontariamente implementato, non di un difetto.

La questione è di solito banale da risolvere. Un modo sicuro è quello di controllare prima se un altro pacchetto è proprietario del file (`pacman -Qo /percorso/al/file`). Se il file è di proprietà di un altro pacchetto, si può procedere ad aprire un [bug report](/index.php/Reporting_bug_guidelines "Reporting bug guidelines"). Se il file non è di proprietà di un altro pacchetto, rinominare il file che 'esiste nel filesystem' e rieseguire il comando di aggiornamento. Se tutto va bene, il file può essere rimosso.

Se si fosse installato un programma manualmente senza usare pacman o un suo frontend, bisognerebbe rimuoverlo con tutti i suoi file e reinstallarlo correttamente usando pacman.

Ogni pacchetto installato fornisce il file `/var/lib/pacman/local/$package-$version/files` il quale contiene il metadata del pacchetto. Se questo file si danneggia, è vuoto o non esiste, si avranno errori "file exists in filesystem" nel cercare di aggiornare il pacchetto. Tale errore di solito concerne solo un pacchetto e, invece di rinominare manualmente e poi rimuovere tutti i file che appartengono al pacchetto in questione, si può eseguire `pacman -S --force $package` per forzare pacman a sovrascrivere tali file.

**Non** eseguire `pacman -Syu --force`.

### Ottengo un errore quando si installa un pacchetto: "not found in sync db"

In primo luogo, accertarsi che il pacchetto esista realmente (controllare eventuali errori di battitura!). Se si è certi che il pacchetto esista, allora potrebbe essere che la lista dei pacchetti non sia aggiornata, o i repositori siano configurati in modo errato. Lanciare il comando `pacman -Syyu` per forzare un aggiornamento di tutte le liste dei pacchetti e dei pacchetti stessi.

### Ottengo un errore quando si installa un pacchetto: "target not found"

Anzitutto assicurarsi che il pacchetto esista veramente (e controllare eventuali errori di battitura). Se si è certi che il pacchetto esista, la lista locale dei pacchetti potrebbe essere obsoleta, o il repository che si sta utilizzando potrebbe non essere configurato correttamente. Provare ad eseguire `pacman -Syyu` per forzare l'aggiornamento di tutte le liste dei pacchetti e dei pacchetti stessi.
Potrebbe anche essere che il repository che contiene il pacchetto non sia abilitata sul proprio sistema, ad esempio il pacchetto potrebbe essere nel repository *multilib*, ma *multilib* potrebbe non essere abilitato nel proprio *pacman.conf*.

### Pacman mi richiede ripetutamente di aggiornare lo stesso pacchetto!

Ciò è dovuto a voci duplicate in `/var/lib/pacman/local/`, come ad esempio due istanze di `linux`. Il comando `pacman -Qi` fornisce la versione corrente, ma `pacman -Qu` riconosce la vecchia versione e, pertanto, viene tentato l'aggiornamento.

Soluzione: eliminare la voce duplicata in `/var/lib/pacman/local/`.

**Nota:** La versione 3.4 di Pacman dovrebbe visualizzare un messaggio di errore in caso di voci duplicate, che dovrebbe rendere questa domanda obsoleta.

### Pacman va in crash durante un aggiornamento!

Nel caso in cui pacman si blocchi con un errore di scrittura del database ("database write") durante la rimozione di pacchetti, e la reinstallazione o l'aggiornamento di un pacchetto fallisce:

1.  Avviare il sistema usando il supporto di installazione di Arch.
2.  Montare la propria partizione di root.
3.  Aggiornare il database e i pacchetti usando il comando `pacman -Syyu`.
4.  Installare il pacchetto corrotto tramite `pacman -r /percorso/propria/root -S pacchetto`.

### Ho installato un programma utilizzando "make install"; questi file non appartengono ad alcun pacchetto!

Se si riceve un errore di file in conflitto ("conflicting files"), pacman sovrascriverà il software installato manualmente se lanciato con l'opzione `--force` (ad esempio `pacman -S --force`). Consultare [Pacman tips#Identify files not owned by any package](/index.php/Pacman_tips#Identify_files_not_owned_by_any_package "Pacman tips") per uno script che cerca nel file system i file *orfani*.

**Attenzione:** Fare attenzione nell'usare l'opzione `--force` dato che può causare seri problemi se usata impropriamente. È consigliato usare questa opzione solamente quando richiesto nelle notizie di Arch.

### Ho bisogno di un pacchetto con un file specifico. Come faccio a sapere da quale viene fornito?

Installare [pkgfile](/index.php/Pkgfile "Pkgfile"), che utilizza un database separato con tutti i file ed i pacchetti associati.

### Pacman è completamente fuori uso! Come faccio a reinstallarlo?

Nel caso in cui pacman sia irrimediabilmente guasto, scaricare manualmente o compilare i pacchetti necessari ([openssl](https://www.archlinux.org/packages/?name=openssl), [libarchive](https://www.archlinux.org/packages/?name=libarchive), e [pacman](https://www.archlinux.org/packages/?name=pacman)) ed estrarli in root. I binari di pacman verranno ripristinati con il relativo file di configurazione predefinito. In seguito, reinstallare quei pacchetti con pacman per mantenere l'integrità del database dei pacchetti. Ulteriori informazioni e uno script d'esempio (non aggiornato) che automatizza il processo è disponibile in [questo](https://bbs.archlinux.org/viewtopic.php?id=95007) post del forum.

### Dopo aver aggiornato il sistema e riavviato, ottengo l'errore "unable to find root device" e il sistema non riesce più ad avviarsi.

Molto probabilmente il proprio initramfs si è corrotto durante un update del kernel (una causa può essere l'uso inappropriato dell'opzione `--force` di pacman). Si hanno due possibilità:

**1.** Provare la voce *Fallback*.

**Suggerimento:** Nel caso si sia rimossa questa voce per qualunque motivo, si può comunque premere `Tab` quando appare il menu del bootloader (per Syslinux) o `e` (per GRUB), rinominarla `initramfs-linux-fallback.img` e premere `Enter` o `b` (a seconda del proprio bootloader) per fare il boot con i nuovi parametri.

	Appena il sistema si avvia, eseguire questo comando (per il kernel [linux](https://www.archlinux.org/packages/?name=linux) standard) o dalla console o da un terminale per rigenerare l'immagine initramfs:

	 `# mkinitcpio -p linux` 

**2.** Se ciò non funzionasse, da una release 2012 di Arch (CD/DVD o chiavetta USB), eseguire:

**Nota:** Se non si ha la release 2012 o si ha qualche altra distribuzione "live" di Linux a disposizione, si può usare [chroot](/index.php/Chroot "Chroot") alla vecchia maniera. Ovviamente ci sarà bisogno di più comandi rispetto ad eseguire semplicemente lo script `arch-chroot`.

```
# mount /dev/sdxY /mnt        #La propria partizione root.
# mount /dev/sdxZ /mnt/boot    #Se si usa una partizione /boot separata.
# arch-chroot /mnt
# pacman -Syu mkinitcpio systemd linux
```

	Reinstallare il kernel (il pacchetto [linux](https://www.archlinux.org/packages/?name=linux)) rigenererà automaticamente l'immagine initramfs con `mkinitcpio -p linux`. Non c'è bisogno di rifare ciò separatamente.

	A questo punto è raccomandabile eseguire `exit`, `umount /mnt/{boot,}` e `reboot`.

**Nota:** Se non è possibile accedere all'ambiente arch-chroot o chroot ma si ha bisogno di reinstallare dei pacchetti, si può usare il comando pacman -r /mnt -Syu foo bar per usare pacman nella propria partizione di root.

### Signature from "User <email@gmail.com>" is unknown trust, installation failed

Seguire [Pacman-key (Italiano)#Resettare tutte le chiavi](/index.php/Pacman-key_(Italiano)#Resettare_tutte_le_chiavi "Pacman-key (Italiano)"). Oppure si può provare ad aggiornare prima il pacchetto [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) manualmente eseguendo `pacman -S archlinux-keyring`.

### Continuo ad ottenere "PackageName: signature from "User <email@archlinux.org>" is invalid"

```
error: PackageName: signature from "User <email@archlinux.org>" is invalid
error: failed to commit transaction (invalid or corrupted package (PGP signature))
Errors occured, no packages were upgraded.

```
Questo succede quando l'orologio di sistema non è impostato correttamente. Configurare l'[orario](/index.php/System_time "System time") ed eseguire: `# hwclock -w` prima di provare di nuovo ad installare od aggiornare un pacchetto.

### Continuo ad ottenere l'errore "failed to commit transaction (invalid or corrupted package)"

Cercare i file `*.part` (pacchetti scaricati parzialmente) in `/var/cache/pacman/pkg` e rimuoverli (spesso sono causati da un uso personalizzato di `XferCommand` in `pacman.conf`).

### Ogni volta che uso pacman ottengo l'errore 'warning: current locale is invalid; using default "C" locale'. Cosa faccio?

Come descritto nel messaggio di errore, il tuo locale non è configurato correttamente. Leggere [Locale (Italiano)](/index.php/Locale_(Italiano) "Locale (Italiano)").

### Come posso fare in modo che pacman usi la mia configurazione per un proxy?

Assicurarsi che le pertinenti variabili d'ambiente (`$http_proxy`, `$ftp_proxy` ecc.) siano configurate. Se si usa pacman con [sudo](/index.php/Sudo_(Italiano) "Sudo (Italiano)"), bisogna configurare sudo affinché [passi queste variabili a pacman](/index.php/Sudo_(Italiano)#Variabili_d.27ambiente "Sudo (Italiano)").

### Come reinstallare tutti i pacchetti, mantenendo memoria di quali pacchetti sono installati esplicitamente e quali come dipendenze?

Per reinstallare tutti i pacchetti ufficiali: `pacman -S $(pacman -Qnq)` (l'opzione `-S` mantiene di default il motivo dell'installazione).
È necessario reinstallare tutti i pacchetti non ufficiali manualmente: se ne può ottenere una lista con `pacman -Qmq`.

## Altre risorse

*   [manuale libalpm(3)](https://www.archlinux.org/pacman/libalpm.3.html)
*   [manuale pacman(8)](https://www.archlinux.org/pacman/pacman.8.html)
*   [manuale pacman.conf(5)](https://www.archlinux.org/pacman/pacman.conf.5.html)
*   [manuale repo-add(8)](https://www.archlinux.org/pacman/repo-add.8.html)