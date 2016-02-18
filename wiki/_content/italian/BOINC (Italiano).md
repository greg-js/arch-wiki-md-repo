## Contents

*   [1 Cos'è BOINC](#Cos.27.C3.A8_BOINC)
    *   [1.1 Installare BOINC](#Installare_BOINC)
        *   [1.1.1 Istruzioni](#Istruzioni)
    *   [1.2 Come usare BOINC](#Come_usare_BOINC)
        *   [1.2.1 BOINC attraverso l'interfaccia grafica](#BOINC_attraverso_l.27interfaccia_grafica)
            *   [1.2.1.1 Suggerimenti](#Suggerimenti)
        *   [1.2.2 BOINC attraverso riga di comando](#BOINC_attraverso_riga_di_comando)
    *   [1.3 File di log](#File_di_log)
    *   [1.4 Scelta dei progetti](#Scelta_dei_progetti)
    *   [1.5 Link](#Link)

## Cos'è BOINC

Dal sito ufficiale di BOINC: *Sfrutta il tempo morto del tuo pc (Linux, Mac o Windows) per curare malattie, studi sull'effetto serra, scoprire stelle e astri nel cielo, e aiutare tanti altri tipi di ricerca scientifica. E' sicuro e molto semplice.*

Wikipedia: *Il Berkeley Open Infrastructure for Network Computing (BOINC) è un'applicazione software di calcolo distribuito creata per gestire progetti di ricerca che richiedono una potenza di calcolo così elevata da essere da essere difficilmente raggiungibile persino con un supercomputer, ma accessibile attraverso la collaborazione di migliaia di personal computer sparsi in tutto il mondo, coordinati attraverso Internet. Viene sviluppata da un gruppo di lavoro dell'Università di Berkeley diretto da David Anderson.*

### Installare BOINC

Boinc è installato come un demone(*daemon*) e per ragioni di sicurezza lavorerà sotto il nuovo user creato, *boinc* appunto. Aggiungere tramire riga di comando il nostro user al gruppo boinc e creare un link al file password per poterlo far funzionare tramite interfaccia grafica (GUI).

#### Istruzioni

Innanzitutto installare il pacchetto boinc da pacman:

```
# pacman -S boinc

```

Come prima annunciato boinc funzionerà come demone, per farlo partire all'avvio aggiungerlo nella sezione daemons in /etc/rc.conf:

```
# DAEMONS=(...boinc...)

```

Inserire il proprio utente al gruppo *boinc*. Per dare effetto a questo ultimo comando bisogna effettuare un log out.

```
#gpasswd -a *nomeutente* boinc

```

Effettuato il log out, si può controllare se il nostro utente adesso fa parte del gruppo *boinc* eseguendo questo comando:

```
# groups

```

Se non si vuole far partire BOINC all'avvio si può semplicemente avviare il demone:

```
# /etc/rc.d/boinc start

```

### Come usare BOINC

#### BOINC attraverso l'interfaccia grafica

Come di default, una password viene creata in /var/lib/boinc/gui_rpc_auth.cfg per la connessione al demone. Per semplificare la connessione della GUI con il demone, riportarsi nella directory della home, creare un link al file e successivamente cambiare i permessi per abilitare l'accesso in lettura ai membri del gruppo *boinc*.

```
$cd
$ ln -s /var/lib/boinc/gui_rpc_auth.cfg gui_rpc_auth.cfg
# chmod 640 gui_rpc_auth.cfg

```

Se si preferisce un'altra password, o nessuna proprio, si può editare /var/lib/gui_rpc_auth.cfg. Per avviare la GUI, basta semplicemente eseguire:

```
$boinc_gui

```

BOINC dovrebbe presentare la schermata per l'aggiunta di nuovi progetti. '*NB: alcuni progetti richiedono la registrazione di un account in remoto attraverso la GUI, mentre alcuni lo richiedono in partenza. Questo si può fare semplicemente via web senza nessun problema. **Si può inserire più di un progetto se si posseggono le risorse (spazio del disco, tempo, CPU). Per l'aggiunta di altri progetti si può cliccare il bottone** ***add project *dalla* Simple view *oppure dall****advanced view* dal menu cliccare *Tools->Attach to project*.

##### Suggerimenti

Se BOINC non chiede la connessione ad un progetto, controllare se si è connessi al demone. Andare sul menu di *Advanced view* *Advanced->Select computer*, editare il proprio hostname ed inserire la password. (Per evitare tutto ciò controllare che il passo della modifica del file gui_rpc_auth.cfg sopracitato sia stato fatto).

#### BOINC attraverso riga di comando

Con la versione 2.6.15, le pagine di aiuto (man pages) ed i comandi CLI non sono coerenti l'uno con l'altro.

```
**Man Page	CLI equivalent**
boinc		boinc_client
boinccmd	boinc_cmd
boincmgr	boinc_gui

```

### File di log

BOINC sistema tutti i file in /var/lib/boinc:

```
/var/lib/boinc/stderrdae.txt
/var/lib/boinc/stdoutdae.txt

```

### Scelta dei progetti

I progetti hanno una differente richiesta dei requisiti minimi (CPU, spazio del disco), e un differente tempo di lavoro. Se non si finisce completamente un lavoro questo sarà inviato a qualcun altro. E' consigliato cercare un progetto che tra i tanti veste meglio con il proprio pc onde evitare il passaggio del progetto con l'eventuale perdita degli evtuali crediti che si potevano ottenere. Un altro consiglio è di guardare i risultati (*check your results*) pubblicati sulla pagina web del proprio account.

### Link

*   [BOINC homepage](http://boinc.berkeley.edu/)
*   [Lista dei progetti BOINC molto interessante](http://boinc.berkeley.edu/projects.php)
*   [Pagina di Wikipedia riguardo BOINC in iinglese](http://en.wikipedia.org/wiki/BOINC)
*   [Pagina di Wikipedia riguardo BOINC in italiano](http://it.wikipedia.org/wiki/BOINC)