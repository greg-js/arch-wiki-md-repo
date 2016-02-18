Il file [/etc/fstab](https://en.wikipedia.org/wiki/it:Fstab "wikipedia:it:Fstab") contiene le informazioni sul filesystem. In esso viene definito come le partizioni e le periferiche di archiviazione saranno montate all'interno del sistema. Questo file verrà letto dal comando `mount` per determinare quali opzioni utilizzare per montare una specifica periferica o una partizione.

## Contents

*   [1 Esempio](#Esempio)
*   [2 Definizione dei campi](#Definizione_dei_campi)
*   [3 Identificare i filesystem](#Identificare_i_filesystem)
    *   [3.1 Descrittori del Kernel](#Descrittori_del_Kernel)
    *   [3.2 Etichette](#Etichette)
    *   [3.3 UUID](#UUID)
*   [4 Trucchi e consigli](#Trucchi_e_consigli)
    *   [4.1 UUID per la swap](#UUID_per_la_swap)
    *   [4.2 Utilizzare percorsi contenenti spazi](#Utilizzare_percorsi_contenenti_spazi)
    *   [4.3 Dischi esterni](#Dischi_esterni)
    *   [4.4 opzione atime](#opzione_atime)
    *   [4.5 tmpfs](#tmpfs)
        *   [4.5.1 Utilizzo](#Utilizzo)
            *   [4.5.1.1 Migliorare i tempi di compilazione](#Migliorare_i_tempi_di_compilazione)
    *   [4.6 Scrivere su FAT32 da utente normale](#Scrivere_su_FAT32_da_utente_normale)
    *   [4.7 Effettuare il remount della partizione di root](#Effettuare_il_remount_della_partizione_di_root)
*   [5 Risorse](#Risorse)

## Esempio

Questo è un esempio del file `/etc/fstab` usando i descrittori del kernel:

 `/etc/fstab` 
```
# <file system>        <dir>         <type>    <options>             <dump> <pass>
/dev/sda1              /             ext4      defaults,noatime      0      1
/dev/sda2              none          swap      defaults              0      0
/dev/sda3              /home         ext4      defaults,noatime      0      2
```

## Definizione dei campi

In `/etc/fstab` sono contenuti i seguenti campi separati da spazi o tabulazioni:

```
<file system>	<dir>	<type>	<options>	<dump>	<pass>

```

*   **<file systems>** - definisce la periferica di archiviazione o la partizione.
*   **<dir>** - indica al comando mount la cartella dove sarà montata la partizione(<file system>).
*   **<type>** - indica il tipo di file system della partizione o del dispositivo. Sono supportati diversi file system. Alcuni esempi sono: `ext2`, `ext3`, `reiserfs`, `xfs`, `jfs`, `smbfs`, `iso9660`, `vfat`, `ntfs`, `swap`, ed `auto`. L'opzione `auto` lascia riconoscere al comando mount il tipo di file system da utilizzare, questa opzione e utile in caso di supporti ottici (CD/DVD).
*   **<options>** - indica le opzioni utilizzate dal comando mount sul file system. Alcune [opzioni di mount](http://linux.die.net/man/8/mount) fanno riferimento a specifici file system, altre invece sono generiche:

*   `auto` - Il file system sarà montato automaticamente durante l'avvio del sistema, oppure quando viene lanciato il comando `mount -a`.
*   `noauto` - Il file system non sarà montato automaticamente ma solo manualmente.
*   `exec` - Abilita l'esecuzione dei file eseguibili residenti sulla partizione(abilitata di default).
*   `noexec` - Inibisce la possibilità di eseguire programmi dal file system.
*   `ro` - Il mount del file system avviene in sola lettura.
*   `rw` - Il mount del file system avviene in lettura e scrittura.
*   `user` - Permette a tutti gli utenti di montare il filesystem. Questa opzione include `noexec`, `nosuid`, `nodev`, se non vengono utilizzate le opzioni opposte.
*   `users` - Permette agli utenti appartenenti al gruppo users di montare il filesystem.
*   `nousers` - Permette il mount solo all'utente root.
*   `owner` - Permette il mount al solo proprietario del punto di mount.
*   `sync` - l'I/O sul file system deve essere sincrono.
*   `async` - tutto l'I/O sul file system deve essere asincrono.
*   `dev` - Interpreta le periferiche a blocchi o periferiche speciali all'interno del filesystem.
*   `nodev` - Impedisce l'interpretazione di periferiche a blocchi o periferiche speciali all'interno del filesystem.
*   `suid` - Consente l'uso di operazioni di suid e sgid. Sono comunemente usate per permettere agli utenti di un sistema di eseguire programmi elevando temporaneamente i privilegi [[1]](http://it.wikipedia.org/wiki/Suid).
*   `nosuid` - Impedisce le operazioni di suid e sgid.
*   `noatime` - Non aggiorna l'inode con i tempi di accesso al file system. Può aumentare le prestazioni (vedi [l'opzione `atime`](#opzione_atime)).
*   `nodiratime` - Non aggiorna l'inode delle directory sui tempi di accesso al file system. Può aumentare le prestazioni (vedi [l'opzione `atime`](#opzione_atime)).
*   `relatime` - Aggiorna nell'inode solo i tempi relativi a modifiche o cambiamenti dei file. I tempi di accesso vengono aggiornati solo se l'ultimo accesso è precedente rispetto a quello dell'ultima modifica.(Simile a `noatime` ma non interferisce con programmi come `mutt` che devono sapere se un file è stato letto dopo la sua ultima modifica.) Può aumentare le performance (vedi [l'opzione `atime`](#opzione_atime)).
*   `flush` - Questa è una opzione per il file system FAT, serve a scrivere più spesso i dati sul disco in modo da evitare che le finestre di trasferimento vengano chiuse mentre i dati non sono ancora stati scritti.
*   `defaults` - Assegna le impostazioni di default del filesystem per il comando mount. Le opzioni di default per `ext4` sono `rw`,`suid`,`dev`,`exec`,`auto`,`nouser`,`async`.

*   **<dump>** - Viene utilizzato dal programma dump per decidere quando fare un backup. Quando si installa il sistema(ma non nel caso di una installazione standard di Arch Linux), dump controlla il valore ed usa il numero per decidere se fare un backup del file system. I valori da poter inserire sono 0 ed 1\. Se il valore è impostato a 0 dump ignorerà il file system, mentre se viene impostato ad 1 dump si occuperà di effettuare il backup del file system. La maggior parte degli utenti non avranno dump installato, è quindi consigliato lasciare il valore di <dump> a 0.
*   **<pass>** - [fsck](/index.php/Fsck "Fsck") legge il valore di <pass> e determina l'ordine in cui i file system saranno controllati. I possibili valori sono 0, 1 e 2\. Il file system root(/) deve avere la massima priorità, 1, gli altri file system che dovranno essere controllati avranno come valore 2\. Nel caso in cui il valore di <pass> sia impostato a 0 il file system non sarà controllato da fsck.

## Identificare i filesystem

I filesystem nel file `/etc/fstab` possono essere identificati in tre modi: utilizzando i descrittori del kernel, tramite gli UUID, oppure utilizzando le etichette. Il vantaggio dell'uso degli UUID o delle etichette è che questi non dipendono dall'ordine in cui i dischi sono(fisicamente) collegati alla scheda madre. Risultano utili quindi se si modifica l'ordinamento dei dischi nel BIOS, se vengono cambiati i cablaggi di connessione (esempio dalla porta SATA1 sulla scheda madre alla SATA2 ecc.), oppure nel caso in cui il BIOS non mantenga correttamente l'ordinamento dei dischi. Per maggiori informazioni leggere l'articolo: [persistent block device naming](/index.php/Persistent_block_device_naming_(Italiano) "Persistent block device naming (Italiano)").

Per elencare le alcune informazioni riguardo alle partizioni, eseguire:

 `$ lsblk -f` 
```
NAME   FSTYPE LABEL      UUID                                 MOUNTPOINT
sda                                                           
├─sda1 ext4   Arch_Linux 978e3e81-8048-4ae1-8a06-aa727458e8ff /
├─sda2 ntfs   Windows    6C1093E61093B594                     
└─sda3 ext4   Storage    f838b24e-3a66-4d02-86f4-a2e73e454336 /media/Storage
sdb                                                           
├─sdb1 ntfs   Games      9E68F00568EFD9D3                     
└─sdb2 ext4   Backup     14d50a6c-e083-42f2-b9c4-bc8bae38d274 /media/Backup
sdc                                                           
└─sdc1 vfat   Camera     47FA-4071                            /media/Camera
```

### Descrittori del Kernel

Eseguire `lsblk -f` per elencare le partizioni, ed aggiungere il percorso `/dev` ai nomi visualizzati.

Vedere il [file d'esempio](/index.php/Fstab_(Italiano)#Esempio "Fstab (Italiano)").

### Etichette

**Nota:** Ogni etichetta dovrebbe essere unica, per prevenire ogni possibile conflitto.

Per informazioni dettagliate riguardo l'assegnazione di una etichetta ad una periferica o partizione consultare [questo](/index.php/Persistent_block_device_naming_(Italiano)#By-label "Persistent block device naming (Italiano)") articolo. Per assegnare una etichetta alla partizione di root sarà necessario agire da una distribuzione Linux "live" in quanto la partizione dovrebbe essere smontata prima.

Per elencare le partizioni, utilizzare il comando `lsblk -f` quindi inserire prima del nome dell'etichetta `LABEL=`:

 `/etc/fstab` 
```
# <file system>        <dir>         <type>    <options>             <dump> <pass>
LABEL=Arch_Linux       /             ext4      defaults,noatime      0      1
LABEL=Arch_Swap        none          swap      defaults              0      0
```

### UUID

Tutte le partizioni e periferiche hanno un UUID unico. Gli UUID vengono generati dal programma di generazione del filesystem (ad esempio `mkfs.*`) quando la partizione viene creata o formattata.

Per elencare le partizioni, utilizzare il comando `lsblk -f` quindi inserire prima `UUID=`:

**Tip:** Se si desidera ottenere il valore UUID di una specifica partizione:
```
$ lsblk -no UUID /dev/sda2

```

 `/etc/fstab` 
```
# <file system>                            <dir>     <type>    <options>             <dump> <pass>
UUID=24f28fc6-717e-4bcd-a5f7-32b959024e26  /         ext4      defaults,noatime      0      1
UUID=03ec5dd3-45c0-4f95-a363-61ff321a09ff  /home     ext4      defaults,noatime      0      2
UUID=4209c845-f495-4c43-8a03-5363dd433153  none      swap      defaults              0      0
```

## Trucchi e consigli

### UUID per la swap

Nel caso chel la partizione di swap non abbia un UUID, sarà possibile aggiungerlo manualmente. Questo accade quando l'UUID della partizione di swap non appare con il comando `lsblk -f`. Di seguito verranno mostrati i passaggi per assegnare un UUID alla partizione di swap:

Individuare la swap usando il comando:

```
# swapon -s

```

Disabilitare la swap:

```
# swapoff /dev/sda7

```

Ricreare la partizione di swap con un nuovo UUID assegnato ad essa:

```
# mkswap -U random /dev/sda7

```

Attivare nuovamente la swap:

```
# swapon /dev/sda7

```

### Utilizzare percorsi contenenti spazi

Se un punto di mount contiene degli spazi nel nome, può essere usato il carattere di escape `\` seguito dal codice ottale di tre cifre corrispondente allo spazio `\040` per emularlo:

 `/etc/fstab` 
```
UUID=47FA-4071     /home/username/Camera<font color="grey">\040</font>Pictures   vfat  defaults,noatime       0  0
/dev/sda7          /media/100<font color="grey">\040</font>GB<font color="grey">\040</font>(Storage)       ext4  defaults,noatime,user  0  2
```

### Dischi esterni

I dischi esterni che dovranno essere montati quando presenti, ma ignorati se assenti, avranno bisogno dell'uso dell'opzione `nofail`. Questa opzione inibisce la visualizzazione del messaggio di errore durante l'avvio.

 `/etc/fstab`  `/dev/sdg1        /media/backup    jfs    defaults,nofail    0  2` 

### opzione atime

L'uso di `noatime`, `nodiratime` o `relatime` può aumentare le prestazioni del disco, per i file system ext2, ext3 o ext4\. Linux di default tiene traccia(scrivendolo sul disco) di ogni lettura effettuata `atime`. Questa funzione è più indicata su di un pc server piuttosto che su un pc desktop. L'aspetto peggiore dell'opzione `atime` sta nel fatto che, anche leggendo un file dalla memoria cache(quindi non dal disco direttamente) verrà effettuata una scrittura sul disco! Usando l'opzione `noatime` viene disabilitato l'aggiornamento de tempi di accesso ai file ogni volta che viene letto un file. Questo non interferisce con la maggioranza delle applicazioni, ma [Mutt](/index.php/Mutt_(Italiano) "Mutt (Italiano)") necessita di queste informazioni.Se si usa mutt sarà quindi necessario utilizzare l'opzione `relatime`. L'uso dell'opzione `relatime` abilita l'aggiornamento dei tempi di accesso ai file solo se il file viene modificato (al contrario dell'opzione `noatime` dove i tempi di accesso in lettura al file non verranno aggiornati, e saranno precedenti rispetto ai tempi di modifica del file). L'opzione `nodiratime` disabilitata la scrittura dei tempi di accesso ai file, solo per le cartelle, mentre per i normali file in tempi di accesso verranno aggiornati. Il miglior compromesso potrebbe essere l'uso dell'opzione `relatime` che non influenzerebbe il funzionamento di programmi come [Mutt](/index.php/Mutt_(Italiano) "Mutt (Italiano)"), ma si otterrebbe anche un aumento delle performance, dato che i tempi di accesso ai file verranno aggiornati solo se i file vengono modificati.

**Nota:** l'opzione `noatime` include anche l'opzione `nodiratime`. Non sarà quindi necessario dichiarare entrambe le opzioni. [[2]](http://lwn.net/Articles/244941/)

### tmpfs

[tmpfs](https://en.wikipedia.org/wiki/Tmpfs "wikipedia:Tmpfs") è un filesystem temporaneo che risiede nella memoria, e/o nella/e area/e di swap, a seconda di quanto esso viene riempito. Montare cartelle in tmpfs può essere un buon modo per velocizzare gli accessi in lettura nei file che vi risiedono, o per assicurarsi che il contenuto venga cancellato automaticamente ad ogni riavvio.

Alcune directory dove è comunemente usato tmpfs senza problemi sono [/tmp](http://www.pathname.com/fhs/2.2/fhs-3.15.html), [/var/lock](http://www.pathname.com/fhs/2.2/fhs-5.9.html) ed [/var/run](http://www.pathname.com/fhs/2.2/fhs-5.13.html). NON usare tmpfs per [/var/tmp](http://www.pathname.com/fhs/2.2/fhs-5.15.html), perché questa cartella contiene dei file che devono essere conservati dopo il riavvio. Arch utilizza la cartella `/run` come tmpfs, essa comprende anche `/var/run` e `/var/lock` creati come link simbolici per compatibilità. tmpfs è utilizzata anche per `/tmp` nella configurazione di default del file `/etc/fstab`.

**Nota:** Utilizzando [systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)"), i file e le cartelle temporanee in tmpfs possono essere ricreati all'avvio utilizzando [tmpfiles.d](/index.php/Systemd_(Italiano)#I_files_temporanei "Systemd (Italiano)").

Per default, la partizione tmpfs è impostata della dimensione di metà della RAM totale, ma può essere modificata. Notare che l'effettivo uso di memoria/swap dipende da quanto vengono riempite, la partizione tmpfs non richiede memoria fino a che non viene usata.

Per usare tmpfs per `/tmp`, semplicemente aggiungere questa linea ad `/etc/fstab` (e riavviate il sistema):

 `/etc/fstab`  `tmpfs   /tmp         tmpfs   nodev,nosuid                  0  0` 

Sarà possibile o meno impostare la dimensione, ma sarà necessario lasciare l'opzione `mode` inalterata in questi casi, per essere certi che le cartelle abbiano i giusti permessi(1777). Nell'esempio sopra, `/tmp` sarà impostata per metà della RAM totale. Per impostare esplicitamente la dimensione massima, usare l'opzione `size` del comando `mount`:

 `/etc/fstab`  `tmpfs   /tmp         tmpfs   nodev,nosuid,size=2G          0  0` 

Qui viene mostrato un esempio più avanzato per aggiungere punti di mount tmpfs per gli utenti. Questo è utile per siti web, file tmp di mysql, `~/.vim/`, ed altro. È importante provare a configurare le opzioni ideali per ciò che si vuole fare. L'obiettivo è avere un settaggio il più sicuro possibile per prevenire abusi. Limitare le dimensioni e specificare i modi uid e gid + è una pratica molto sicura. Per maggiori informazioni su questo argomento seguire i link elencati nella sezione [Risorse](#Risorse).

 `/etc/fstab`  `tmpfs   /www/cache    tmpfs  rw,size=1G,nr_inodes=5k,noexec,nodev,nosuid,uid=648,gid=648,mode=1700   0  0` 

Consultare la pagina di manuale relativa al comando `mount` per maggiori informazioni. Cercare di comprendere come minimo l'opzione `default`, molto utile ed utilizzata.

Riavviare per fare in modo che i cambiamenti abbiano effetto. Notare che anche se si è tentati e possa sembrare utile, **NON** usare il comando `mount -a`, perché così facendo ogni file contenuto in precedenza nelle suddette cartelle diventerebbe quindi inaccessibile(ad esempio i file di lock delle applicazioni). Comunque, se queste cartelle sono vuote, sarà possibile eseguire il comando `mount -a` invece di riavviare(oppure effettuare il mount manuale delle cartelle).

Dopo aver effettuato le modifiche, si potrà verificare il funzionamento controllando `/proc/mounts` con il comando `findmnt`:

 `$ findmnt --target /tmp` 
```
TARGET SOURCE FSTYPE OPTIONS
/tmp   tmpfs  tmpfs  rw,nosuid,nodev,relatime
```

#### Utilizzo

Generalmente, i processi ed i programmi con intensive richieste di I/O eseguono frequentemente operazioni di lettura/scrittura possono ottenere benefici utilizzando una cartella come tmpfs. Alcune applicazioni posso ricevere un sostanziale guadagno caricando alcuni (o tutti) i propri dati sulla memoria condivisa. Ad esempio, [spostando il profilo di Firefox sulla RAM](/index.php/Firefox_Ramdisk "Firefox Ramdisk") mostra un significativo guadagno nelle performance.

##### Migliorare i tempi di compilazione

**Nota:** La cartella tmpfs (`/tmp`, in questo caso) defe essere montata senza l'opzione `noexec`, altrimenti impedirà agli script di compilazione o ad altri strumenti di essere eseguiti. Come detto [in precedenza](#tmpfs), la dimensione di default equivale alla metà della RAM disponibile è quindi possibile rimanere senza spazio.

E' possibile eseguire [makepkg](/index.php/Makepkg_(Italiano) "Makepkg (Italiano)") con una cartella tmpfs come cartella per la compilazione (che può essere configurata in `/etc/makepkg.conf`):

```
$ BUILDDIR=/tmp/makepkg makepkg

```

### Scrivere su FAT32 da utente normale

Per poter scrivere su una partizione FAT32 è necessario fare alcuni cambiamenti al proprio file `/etc/fstab`:

 `/etc/fstab`  `/dev/sdxY    /mnt/some_folder  vfat   user,rw,umask=000              0  0` 

Il flag `user` significa che ogni utente (oltre a root) può montare e smontare la partizione `/dev/sdX`. `rw` dà l'accesso in lettura/scrittura.

L'opzione `umask` rimuove i permessi selezionati - ad esempio `umask=111` rimuove i permessi di esecuzione. Il problema è che questa linea rimuove i permessi di esecuzione anche alle cartelle, per cui è necessario correggerla in `dmask=000`. Vedere anche [Umask](/index.php/Umask "Umask").

Senza queste opzioni tutti i file sarebbero eseguibili. Anziché utilizzare umask e dmask è possibile utilizzare l'opzione `showexec`, la quale mostra tutti gli eseguibili di Windows (com, exe, bat) con i colori degli eseguibili.

Ad esempio se la propria partizione FAT32 è `/dev/sda9` e si desidera montarla su `/mnt/fat32` bisogna utilizzare:

 `/etc/fstab`  `/dev/sda9    /mnt/fat32        vfat   user,rw,umask=111,dmask=000    0  0` 

### Effettuare il remount della partizione di root

Se per qualche motivo la partizione di root venisse impropriamente montata in sola lettura, effettuare il remount della partizione di root con accesso di lettura-scrittura con il seguente comando:

```
# mount -o remount,rw /

```

## Risorse

*   [Full device listing including block device](http://www.kernel.org/pub/linux/docs/lanana/device-list/devices-2.6.txt)
*   [Filesystem Hierarchy Standard](http://www.pathname.com/fhs/2.2/index.html)
*   [30x Faster Web-Site Speed](http://www.askapache.com/web-hosting/super-speed-secrets.html) (Detailed tmpfs)