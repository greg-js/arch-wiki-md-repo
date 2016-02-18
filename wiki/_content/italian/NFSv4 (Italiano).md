**NFSv4**, *n*etwork *f*ile *s*ystem *v*ersione 4, è la nuova versione di NFS (per configurare un vecchio NFSv3, guarda su [Nfs (Italiano)](/index.php/Nfs_(Italiano) "Nfs (Italiano)") con nuove funzionalità come autenticazione sicura e integrità via Kerberos e SPKM-3, prestazioni migliorate, file caching sicuro, lock migration, UTF-8, ACLs e un miglior supporto per la semantica di condivisione file di Windows.

Questo articolo si occupa dell'installazione e della configurazione di NFSv4.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Server](#Server)
        *   [2.1.1 Export](#Export)
            *   [2.1.1.1 Exporting directories outside your NFS root](#Exporting_directories_outside_your_NFS_root)
        *   [2.1.2 Mappatura ID](#Mappatura_ID)
        *   [2.1.3 Avviare il server](#Avviare_il_server)
    *   [2.2 Client](#Client)
        *   [2.2.1 Mappatura ID del client](#Mappatura_ID_del_client)
        *   [2.2.2 Montare le condivisioni sul client](#Montare_le_condivisioni_sul_client)
    *   [2.3 Client & Server: sincronizzazione orari](#Client_.26_Server:_sincronizzazione_orari)
*   [3 Risoluzione problemi](#Risoluzione_problemi)
    *   [3.1 messages.log contiene "nfsdopenone: Opening /proc/net/rpc/nfs4.nametoid/channel failed: errno 2 (No such file or directory)"](#messages.log_contiene_.22nfsdopenone:_Opening_.2Fproc.2Fnet.2Frpc.2Fnfs4.nametoid.2Fchannel_failed:_errno_2_.28No_such_file_or_directory.29.22)
    *   [3.2 exportfs: /etc/exports:2: syntax error: bad option list](#exportfs:_.2Fetc.2Fexports:2:_syntax_error:_bad_option_list)
    *   [3.3 mount.nfs4: No such device](#mount.nfs4:_No_such_device)
    *   [3.4 mount.nfs4: access denied by server while mounting](#mount.nfs4:_access_denied_by_server_while_mounting)
    *   [3.5 Problemi di permessi](#Problemi_di_permessi)
    *   [3.6 Problemi di permessi Group/gid](#Problemi_di_permessi_Group.2Fgid)

## Installazione

Sia i client che i servers richiedono il pacchetto [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils). Installa [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils) con [pacman](/index.php/Pacman "Pacman").

## Configurazione

### Server

La configurazione del server è molto fine.

#### Export

Prima di tutto dobbiamo modificare i nostri export *(*esportazione*, ma preferisco il termine inglese)* in `/etc/exports`.

Un tipico export di NFSv4 dovrebbe sembrare come questo:

```
/export    192.168.0.12(rw,fsid=0,no_subtree_check,async,no_root_squash)
/export/music 192.168.0.12(rw,no_subtree_check,async,no_root_squash)

```

**Note:** `fsid=0` è richiesto dal filesystem di root per essere esportato.

**Note:** Per ammettere un intervallo di indirizzi, lo schema vecchio stile 192.168.0.* *non è più* supportato con NFSv4\. Usa 192.168.0.0/24 o simili per specificare tali export. (Ciò funzionava con export non NFSv4, ma non funziona più. *L'errore riportato è "no such file or directory"* nel montaggio, cosa che rende problematico la risoluzione dei problemi.)

`/export` nel nostro caso è la radice NFS (grazie all'opzione `fsid=0`). Qualunque altra cosa si voglia condividere tramite NFS deve essere accessibile sotto `/export`.

**Note:** Specificare una radice NFS sembra essere necessario.

Per esportare cartelle al di fuori della radice NFS guarda più sotto.

**Note:** L'opzione `no_root_squash` significa che l'utente root sul client è considerato utente root anche sul server. Ovviamente ciò è un rischio per la sicurezza. Rimuovila se non ne hai bisogno.

##### Exporting directories outside your NFS root

Per fare questo si dovranno usare i montaggi *legati (bind)*. Per esempio, per legare `/home/john` a `/export/john`:

```
# mount --bind /home/john /export/john

```

Ed ora dobbiamo aggiungere `/export/john` a `/etc/exports`:

```
/export    192.168.0.12(rw,fsid=0,no_subtree_check,async,no_root_squash)
/export/music 192.168.0.12(rw,no_subtree_check,async,no_root_squash)
/export/john 192.168.0.12(rw,no_subtree_check,async,no_root_squash,**nohide**)

```

L'opzione `nohide` è **necessaria**, poiché il kernel del server NFS nasconde automaticamente le cartelle montate. Per aggiungere il montaggio legato a `/etc/fstab`:

```
/home/john    /export/john    none    bind  0 0

```

#### Mappatura ID

A questo punto dobbiamo modificare `/etc/idmapd.conf`. Come minimo si dovrà specificare il proprio domainio. Per esempio:

```
[General]

Verbosity = 1
Pipefs-Directory = /var/lib/nfs/rpc_pipefs
**Domain = archlinux.org**

[Mapping]

Nobody-User = nobody
Nobody-Group = nobody

```

#### Avviare il server

Per avviare il server NFS, semplicemente fai:

```
# /etc/rc.d/rpcbind start
# /etc/rc.d/nfs-common start
# /etc/rc.d/nfs-server start

```

Se vuoi sistemare la configurazione, sentiti libero di modificare `/etc/conf.d/nfs-server.conf` per adattarlo ai tuoi bisogni.

### Client

La configurazione del client è molto più semplice

#### Mappatura ID del client

Bisogna modificare `/etc/idmapd.conf` su tutti i client **e la voce del domainio dovrebbe essere identica a quella del server**. Per esempio:

```
[General]

Verbosity = 1
Pipefs-Directory = /var/lib/nfs/rpc_pipefs
**Domain = archlinux.org**

[Mapping]

Nobody-User = nobody
Nobody-Group = nobody

[Translation]
Method = nsswitch

```

**Note:** In una configurazione solo client sii sicuro che rpc.idmapd sia in esecuzione. Il demone nfs-common normalmente rileva in automatico se rpc.idmapd deve essere avviato, ma potrebbe fallire se non ci sono voci di montaggio NFSv4 in `/etc/fstab` o se `/etc/exports` è vuoto (che potrebbero accadere insieme se si usa [autofs](/index.php/Autofs "Autofs") per montare le condivisioni NFSv4). In questo caso imposta **NEED_IDMAPD="yes"** in `/etc/conf.d/nfs-common.conf`.

#### Montare le condivisioni sul client

Sul client, per montare le condivisioni NFSv4: assicurati che il modulo nfs sia caricato (lsmod | grep nfs). Altrimenti esegui il comando "modprobe nfs"

```
# /etc/rc.d/rpcbind start
# /etc/rc.d/nfs-common start
# mount -t nfs4 server:/ /mnt/server/
# mount -t nfs4 server:/music /mnt/music/
# mount -t nfs4 server:/john /mnt/john

```

Rimpazza 'server' con il nome host o l'indirizzo IP del tuo server NFS ed ovviamente 'server', 'music' e 'john' con i nomi delle cartelle hai esportato nel server.

Se vuoi che i columi NFS si montino automaticamente al boot, aggiungili in `fstab`. Per esempio:

```
server: /mnt/server nfs4 async,user 0 0

```

Ricordati di aggiungere netfs alla lista di demoni nel /etc/rc.conf.

**Note:** la radice del percorso sul server è la radice NFS specificata; tutti i percorsi devono essere specificati a lei relativi.

### Client & Server: sincronizzazione orari

Per funzionare in modo appropriato, sia il server che il client devono avere valori di orario molto vicini. Se l'orologio del client è troppo differente da quello del server, allora funzioni base come la copia dei file può rimanere in sospeso a lungo lasciando il sistema inutilizzabile finché non riprende. Gli orologi non devono coincidere al micro/nano secondo, ma per dare un'idea dovrebbero essere entro un secondo l'uno dall'altro.

Si raccomanda il sistema [NTP](/index.php/NTP "NTP") per sincronizzare sia il server che il client agli accurati server NTP disponibili in Internet. Per sistemi piccoli come una rete domestica, l'utility ntpdate potrebbe essere usata per sincronizzare entrambi allo stesso orologio. Per sistemi più grandi potrebbe essere desiderabile installare un server OpenNTP (guarda [NTP](/index.php/NTP "NTP")) nella stessa macchina che funge da server NFS, e quindi tutti i client dovrebbero sincronizzare i valori di orario dal server. Questo ha il vantaggio di abbassare lo stess sui server NTP esterni, e di assicurare che i client NFS useranno esattamente lo stesso orario che ha il server NFS, anche se il server NFS dovesse sperimentare qualche deriva.

## Risoluzione problemi

### messages.log contiene "nfsdopenone: Opening /proc/net/rpc/nfs4.nametoid/channel failed: errno 2 (No such file or directory)"

Aggiungi `nfsd` alla lista MODULES in `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")`.

**Note:** Potresti dover aggiungere `Verbosity = 3` in `/etc/idmapd.conf` e riavviare i servizi per rilevare l'errore.

### exportfs: /etc/exports:2: syntax error: bad option list

Cancella tutti gli spazi dalla lista di opzioni in `/etc/exports`

### mount.nfs4: No such device

controlla che sia stato caricato il modulo `nfs`

```
lsmod | grep nfs

```

e se con il comando precedente non risulta nulla o solo nfsd-stuff dai il comando

```
modprobe nfs

```

### mount.nfs4: access denied by server while mounting

Controlla che i permessi nella cartella del client siano corretti. Prova ad usare 755.

### Problemi di permessi

Se scopri che non puoi impostare adeguatamente i pemessi nei file, assicurati che l'utente/gruppo che stai impostando siano sia sul client che sul server. Se ciò non aiuta, prova a modificare queste linee in `/etc/conf.d/nfs-common.conf`

```
# /etc/conf.d/nfs-common.conf

# Do you want to start the statd daemon? It is not needed for NFSv4.
NEED_STATD="no"

# Do you want to start the idmapd daemon? It is only needed for NFSv4.
NEED_IDMAPD="yes"

```

Riavvia il modulo nfs-common daemon affinché i cambiamenti abbiano effetto. Io riavvierei tutti gli altri demoni, giusto per essere sicuri.

### Problemi di permessi Group/gid

Se le condivisioni NFS si montano senza problemi, e sono pienamente accessibili al proprietario, ma non ai membri del gruppo, controlla il numero di gruppi a cui l'utente appartiene. NFS ha un limite di 16 nel numero di gruppi a cui può appartenere un utente. Se hai utenti con più di tale numero, devi abilitare il flag di avvio `--manage-gids` per `rpc.mountd` nel server NFS.

```
/etc/conf.d/nfs-server.conf

# Options for rpc.mountd.
# If you have a port-based firewall, you might want to set up
# a fixed port here using the --port option.
# See rpc.mountd(8) for more details.

MOUNTD_OPTS="--manage-gids"

```