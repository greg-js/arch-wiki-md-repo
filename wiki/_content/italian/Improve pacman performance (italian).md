## Contents

*   [1 Miglioramento dei tempi d'accesso al database](#Miglioramento_dei_tempi_d.27accesso_al_database)
*   [2 Migliorare la velocità di download](#Migliorare_la_velocit.C3.A0_di_download)
    *   [2.1 Usando Powerpill](#Usando_Powerpill)
    *   [2.2 Usando wget](#Usando_wget)
    *   [2.3 Usando aria2](#Usando_aria2)
    *   [2.4 Usando altre applicazioni](#Usando_altre_applicazioni)
*   [3 Scelta del mirror più veloce](#Scelta_del_mirror_pi.C3.B9_veloce)
*   [4 Condivisione dei pacchetti su rete LAN](#Condivisione_dei_pacchetti_su_rete_LAN)

## Miglioramento dei tempi d'accesso al database

Pacman memorizza tutte le informazioni relative ai pacchetti in piccoli file; uno per pacchetto. Migliorare i tempi d'accesso al database, riduce il tempo necessario a portare a termine le operazioni che ne fanno uso, come la ricerca dei pacchetti e la risoluzione delle dipendenze. Il metodo più sicuro e veloce, è dare il seguente comando come root:

```
# pacman-optimize

```

In questo modo il sistema tenterà di raggruppare tutti i files con le informazioni dei pacchetti, in modo che risiedano nella stessa area dell'hard disk, evitando che le testine si muovano eccessivamente quando devono accedere a tutti i dati. Questo medodo è sicuro, ma non è infallibile. La sua efficacia varia in funzione del filesystem utilizzato, dalla percentuale di utilizzo del disco e dalla frammentazione dello spazio ancora libero. Un'opzione più "aggressiva", sarebbe quella di rimuovere i pacchetti disinstallati e i repository inutilizzati dalla cache, prima di procedere all'ottimizzazione del database:

```
# pacman -Sc && pacman-optimize

```

Se si esegue questo comando periodicamente è consigliabile inserirlo in un cronfile o utilizzare un [timer](https://aur.archlinux.org/packages/systemd-timer-pacman-optimize-git) di systemd, fornito dal pacchetto [systemd-timer-pacman-optimize-git](https://aur.archlinux.org/packages/systemd-timer-pacman-optimize-git/).

## Migliorare la velocità di download

**Nota:** Se la velocità di download è minima, assicurarsi di star utilizzando uno dei [mirror](/index.php/Mirrors_(Italiano) "Mirrors (Italiano)"), e non ftp.archlinux.org, la cui banda è stata ridotta [da marzo 2007](https://www.archlinux.org/news/302/).

La velocità con cui Pacman scarica i pacchetti può essere migliorata usando un'applicazione differente per lo scaricamento, preferendola al downloader built-in.

In ogni caso, assicurarsi di avere l'ultima versione di Pacman prima di effettuare qualsiasi modifica:

```
# pacman -Syu

```

### Usando Powerpill

Powerpill è un wrapper completo per pacman che utilizza il download parallelo da più server per velocizzare il processo di scaricamento. Normalmente pacman scarica un solo pacchetto per volta, aspettando che il download dello stesso sia concluso prima di passare al sucessivo: Powerpill sceglie un approccio differente, cercando di scaricare il maggior numero possibile di pacchetti in contemporanea.

La pagina relativa a [Powerpill](/index.php/Powerpill_(Italiano) "Powerpill (Italiano)") copre la configurazione di base e fornisce vari esempi d'impego.

### Usando wget

Questa opzione è utile se si necessita di impostazioni per i proxy più avanzate rispetto a quelle native di pacman.

Per utilizzare `wget`, si [installi](/index.php/Install "Install") il pacchetto [wget](https://www.archlinux.org/packages/?name=wget) e si modifichi `/etc/pacman.conf` aggiungendo le seguenti linee alla sezione `[options]`:

```
XferCommand = /usr/bin/wget -c -q --show-progress --passive-ftp -O %o %u

```

Invece di inserire i parametri di wget in `/etc/pacman.conf`, è possibile modificare direttamente il relativo file di configurazione (quello globale risiede in `/etc/wgetrc`, mentre la configurazione per utente è contenuta in `$HOME/.wgetrc`).

### Usando aria2

[aria2](/index.php/Aria2 "Aria2") è una utility per il download molto leggera che supporta i download per parti, oltre a consentire la ripresa del download di un file interrotto. Tra I protocolli supportati ci sono HTTP/HTTPS e FTP. aria2 consente inoltre di stabilire più connessioni HTTP/HTTPS o FTP ad un mirror Arch linux, il che dovrebbe consentire un aumento della velocià di download, sia per i file che per i pacchetti.

**Nota:** Inserire `aria2c` in `XferCommand` nel file di configurazione `/etc/pacman.conf` **non** comporta il download parallelo di più pacchetti. Pacman invoca `XferCommand` ad ogni pacchetto e aspetta che il download sia terminato prima di scaricare il successivo. Per scaricare più pacchetti contemporaneamente, si veda la sezione dedicata a [powerpill](#Usando_Powerpill).

Si installi [aria2](https://www.archlinux.org/packages/?name=aria2), quindi si modifichi `/etc/pacman.conf` aggiungendo la seguente linea alla sezione `[options]`:

XferCommand = /usr/bin/aria2c --allow-overwrite=true -c --file-allocation=none --log-level=error -m2 -x2 --max-file-not-found=5 -k5M --no-conf -Rtrue --summary-interval=60 -t5 -d / -o %o %u

**Suggerimento:** * L'utilizzo di questo XferCommand produce output meno utile ma più leggibile:

	`XferCommand = /usr/bin/printf 'Downloading ' && echo %u | awk -F/ '{printf $NF}' && printf '...' && /usr/bin/aria2c -q --allow-overwrite=true -c --file-allocation=none --log-level=error -m2 --max-connection-per-server=2 --max-file-not-found=5 --min-split-size=5M --no-conf --remote-time=true --summary-interval=0 -t5 -d / -o %o %u && echo ' Complete!'`

*   [Configurazione alternativa per l'utilizzo di pacman con aria2](https://bbs.archlinux.org/viewtopic.php?pid=1491879#p1491879): Semplifica la configurazione ed aggiunge altre opzioni.

Spiegazione delle opzioni

	`/usr/bin/aria2c`

	Il percorso completo all'eseguibile di aria2c.

	`--allow-overwrite=true`

	Riavvia un download se il corrispondente file di controllo non esiste. (Default: false)

	`-C, --continue`

	Continua il download di un file parzialmente scaricato, se il relativo file di controllo esiste.

	`--file-allocation=none`

	Non prealloca lo spazio su disco per il file prima dell'inizio del download. (Default:prealloc)

	Su filesystem più recenti come ext4 (con supporto alle estensioni), btrfs e xfs è consigliabile usare `--file-allocation=falloc`, poichè alloca file di grandi dimensioni (GB) quasi istantaneamente. Non utilizzare *falloc* su filesystem legacy come ext3, dal momento che *prealloc* ha lo stesso tempo di esecuzione dell'allocazione standard, ma non consente ad aria2 di iniziare il download finchè l'allocazione non è terminata.

	`--log-level=error`

	Vengono scritti nel file di log solamente gli errori. (Default: debug)

	`m2, --max-tries=2`

	Effettua un massimo di 2 tentativi a mirror per il download di un file specifico. (Default: 1)

	`-x2,--max-connections-per-server=2`

	Imposta un massimo di due connessioni per ogni mirror. (Default:1)

	`--max-file-not-found=5`

	Costringe un download ad essere considerato come "fallito" se non viene ricevuto un singolo byte dopo 5 tentativi. (Default: 0)

	`-k5M,--max-split-size=5M`

	Divide il file se è più grande di 2;5MB = 10MB. (Default: 20M)

	`--no-conf`

	Disabilita il caricamento del file `aria2.conf`, se esistente. (Default:`~/.aria2/aria2.conf`)

	`-Rtrue,--remote-time=true`

	Applica i timestamps dei file(s) remoti a quelli locali. (Default: false)

	`--summary-interval=60`

	visualizza un riassunto dei progressi ogni 60 secondi. (Default: 60)

	`--summary-interval=0` inibisce il riassunto dei progressi e potrebbe migliorare le prestazioni. I logs continueranno ad essere generati secondo il valore di `log-level` impostato.

	`-t5, --timeout=5`

	Imposta 5 secondi di timeout per mirror dopo che viene stabilita una connessione. (Default: 60)

	`-d, --dir`

	La directory dove memorizzare i files scaricati, come specificato da [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)").

	`-o, --out`

	Imposta il nome del/i file/s scaricato/i.

	`%o`

	Variabile che rappresenta il nome del file, come specificato da pacman.

	`%u`

	Variabile che rappresenta l'URL di download, come specificato da pacman.

### Usando altre applicazioni

Esistono altre applicazioni per il download utilizzabili con pacman. Vengono presentate di seguito, con il relativo `XferCommand`:

*   `snarf`: `XferCommand = /usr/bin/snarf -N %u`
*   `lftp`: `XferCommand = /usr/bin/lftp -c pget %u`
*   `axel`: `XferCommand = /usr/bin/axel -n 2 -v -a -o %o %u`

## Scelta del mirror più veloce

Pacman utilizza in sequenza i mirror contenuti in `/etc/pacman.d/mirrorlist` per il download dei pacchetti. Il primo mirror della lista potrebbe tuttavia non essere il più veloce. Per selezionare un mirror più veloce, si consulti [Mirrors](/index.php/Mirrors_(Italiano) "Mirrors (Italiano)")

## Condivisione dei pacchetti su rete LAN

Se si dispone di più macchine con Archlinux collegate ad una rete locale, è possibile condividere i pacchetti per ridurre sensibilmente i tempi di download. Si faccia attenzione a non condividere pacchetti di architetture diverse (es. i686 e x86_64), altrimenti si verificheranno problemi.

Si veda: [pacman tips#Network shared pacman cache](/index.php/Pacman_tips#Network_shared_pacman_cache "Pacman tips").