Questo documento evidenzia la procedura necessaria per configurare AutoFS, un pacchetto che permette l'automount di periferiche rimovibili o cartelle di rete quando inserite o accessibili.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Periferiche rimovibili](#Periferiche_rimovibili)
    *   [2.2 Mount delle condivisioni NFS](#Mount_delle_condivisioni_NFS)
    *   [2.3 Samba](#Samba)
    *   [2.4 FTP ed SSH (usando FUSE)](#FTP_ed_SSH_.28usando_FUSE.29)
        *   [2.4.1 Server remoti FTP](#Server_remoti_FTP)
        *   [2.4.2 Server remoti SSH](#Server_remoti_SSH)
*   [3 Risoluzione di problemi](#Risoluzione_di_problemi)
    *   [3.1 Uso di NIS](#Uso_di_NIS)
    *   [3.2 Parametri Opzionali](#Parametri_Opzionali)
    *   [3.3 Identificare le periferiche rimovibili](#Identificare_le_periferiche_rimovibili)
    *   [3.4 Permessi per AutoFS](#Permessi_per_AutoFS)
*   [4 Altre risorse](#Altre_risorse)
*   [5 Alternative ad AutoFS](#Alternative_ad_AutoFS)

## Installazione

*   Installare il pacchetto [autofs](https://www.archlinux.org/packages/?name=autofs).

*   Caricare il [modulo](/index.php/Kernel_modules_(Italiano) "Kernel modules (Italiano)") `autofs4`.

## Configurazione

AutoFS usa dei file template per la configurazione, questi file posso essere trovati in `/etc/autofs`. Il template principale si chiama `auto.master`, che può fare riferimento ad uno o più template per determinate periferiche.

*   Aprire il file `/etc/autofs/auto.master` con il proprio editor di testo preferito, conterrà qualcosa di simile a questo:

 `/etc/autofs/auto.master` 
```
/var/autofs/misc	/etc/autofs/auto.misc
/var/autofs/net  	/etc/autofs/auto.net
```

La prima parte di ogni riga determina la cartella dove verranno effettuati i mount delle periferiche, il secondo parametro indica il template da utilizzare. Il valore di default è `/var/autofs`, ma può essere cambiato con una qualsiasi cartella a piacimento. Per esempio:

 `/etc/autofs/auto.master` 
```
/media/misc     /etc/autofs/auto.misc     --timeout=5 --ghost
/media/net      /etc/autofs/auto.net      --timeout=60 --ghost
```

I parametri opzionali `timeout` impostano dopo quanti secondi verrà effettuato l'umount delle cartelle. Il parametro `ghost` imposta la visualizzazione permanente dei mount delle periferiche configurati, invece di essere mostrati solo se inseriti o accessibili. Può essere utile se non è possibile ricordare i nomi delle periferiche rimovibili o delle condivisioni di rete.

Le cartelle indicate nel file devono esistere nel sistema e devono essere vuote, dato che il loro contenuto sarà cambiato dinamicamente al caricamento delle periferiche. Questa procedure comunque non sovrascrive di dati contenuti nelle cartelle, quindi se si effettua l'automount di una periferica su di una cartella *attiva* sarà possibile cambiarne il punto di mount nel file `auto.master` e riavviare AutoFS per poter accedere nuovamente al suo contenuto originale.

**Nota:** Assicurarsi di lasciare una riga vuota alla fine dei ogni file template (premendo `Invio` dopo l'ultima parola del file). Se AutoFS non trova un EndOfFile(EOF) corretto, non sarà caricato correttamente.

*   Aprire il file `/etc/nsswitch.conf` ed aggiungere l'opzione per l'automount:

```
automount: files

```

*   Quando la configurazione è terminata, avviare il [demone](/index.php/Daemon_(Italiano) "Daemon (Italiano)") AutoFS come utente root.

Per avviare il demone durante il boot sarà necessario aggiungere `autofs` all'interno dell'array `DAEMONS` nel file `/etc/rc.conf`, ed il modulo `autofs4` nell'array `MODULES` sempre nel solito file.

Le periferiche verranno ora montate automaticamente quando accessibili, rimarranno montate fino a che l'accesso ad esse è garantito.

### Periferiche rimovibili

*   Aprire il file `/etc/autofs/auto.misc` ed aggiungere, rimuovere o modificare le varie periferiche. Ad esempio:

 `/etc/autofs/auto.misc` 
```
#kernel   -ro                                        ftp.kernel.org:/pub/linux
#boot     -fstype=ext2                               :/dev/hda1
usbstick  -fstype=auto,async,nodev,nosuid,umask=000  :/dev/sdb1
cdrom     -fstype=iso9660,ro                         :/dev/cdrom
#floppy   -fstype=auto                               :/dev/fd0
```

Nel caso sia presente un lettore combo CD/DVD sarà necessario cambiare la riga `cdrom` con `-fstype=auto` per avere l'auto-riconoscimento delle periferiche inserite.

### Mount delle condivisioni NFS

AutoFS fornisce un metodo aggiuntivo di localizzare e montare le condivisioni [NFS](/index.php/NFS_(Italiano) "NFS (Italiano)") dai server remoti (il template per la rete di AutoFS `/etc/autofs/auto.net` è stato rimosso in autofs dalla versione 5 e successive). Per abilitare l'automagic discovery(servizio che permette di trovare le condivisioni) e di montare le cartelle condivise da tutti i server accessibili senza ulteriori configurazioni, sarà necessario aggiungere la seguente linea al file `/etc/autofs/auto.master`:

```
/net -hosts --timeout=60

```

Tutti i nomi host devono essere risolvibili, es. aggiungendo l'indirizzo IP ed il nome host nel file `/etc/hosts` oppure tramite [DNS](https://en.wikipedia.org/wiki/Domain_Name_System "wikipedia:Domain Name System") quindi assicurarsi di aver installato ed avviato [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils).

Ad esempio, nel caso in cui un server remoto *fileserver* avente una condivisione [NFS](/index.php/NFS_(Italiano) "NFS (Italiano)") chiamata */home/share*, sarà possibile accedere alla condivisione semplicemente digitando:

```
# cd /net/fileserver/home/share

```

**Nota:** Si prega di notare che utilizzando l'opzione `ghost`, quindi la creazione delle cartelle contenitrici prima del mount delle condivisioni è abilitata di default, anche se nell'installazione di AutoFS viene rimossa questa opzione dal file `/etc/conf.d/autofs` per poter avviare il demone AutoFS.

L'opzione `-host` usa un meccanismo simile al comando `showmount`, per identificare le condivisioni di rete. Sarà possibile visualizzare le condivisioni esportate digitando:

```
# showmount <nomeserver> -e 

```

Sostituendo *<nomeserver>* con il nome del proprio server.

### Samba

Il pacchetto di AutoFS fornito da Arch non fornisce nessun template/script per le condivisioni [Samba](/index.php/Samba_(Italiano) "Samba (Italiano)") o CIFS(23/07/2009), ma quanto riportato di seguito funziona per una singola condivisione:

aggiungere la seguente linea al file `/etc/autofs/auto.master`

```
/media/[my_server] /etc/autofs/auto.[my_server]

```

e creare il file `/etc/autofs/auto.[my_server]`

```
[any_name] -fstype=cifs,[other_options] ://[remote_server]/[remote_share_name]

```

Sarà possibile specificare un nome utente ed una password da utilizzare per la condivisione nella sezione `other_options`

```
[any_name] -fstype=cifs,username=[username],password=[password],[other_options] ://[remote_server]

```

**Nota:** Antecedere il carttere di escape per $, e gli altri caratteri speciali, usando il backslash dove necessario.

### FTP ed SSH (usando FUSE)

I server FTP ed [SSH](/index.php/SSH_(Italiano) "SSH (Italiano)") sono accessibili da AutoFS tramite l'uso di [FUSE](https://en.wikipedia.org/wiki/FUSE "wikipedia:FUSE"), un gestore di filesystem virtuali.

#### Server remoti FTP

Per prima cosa, installare [curlftpfs](https://www.archlinux.org/packages/?name=curlftpfs) dai [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

Caricare il [modulo](/index.php/Kernel_modules_(Italiano) "Kernel modules (Italiano)") `fuse`.

Aggiungere `fuse` all'array `MODULES` nel file `/etc/rc.conf` in modo che sia caricato all'avvio del sistema.

Successivamente, aggiungere una nuova linea per i server FTP nel file `/etc/autofs/auto.master`:

```
/media/ftp        /etc/autofs/auto.ftp    --timeout=60 --ghost

```

Creare il file `/etc/autofs/auto.ftp` ed aggiungere un server usando il formato `[ftp://myuser:mypassword@host:port/path](ftp://myuser:mypassword@host:port/path)`:

```
servername -fstype=curl,rw,allow_other,nodev,nonempty,noatime    :ftp\://myuser\:mypassword\@remoteserver

```

**Nota:** Le password saranno visibili in chiare per chiunque possa lanciare il comando `df` (nel momento in cui i server sono montati), oppure visualizzando il contenuto del file `/etc/autofs.ftp`.

Per aumentare il livello di sicurezza, sarà possibile creare il file `~root/.netrc` ed inserire le password in esso. Le password saranno sempre in chiaro, ma sarà possibile cambiare i permessi sul file in 600, ed il comando `df` non permetterà di mostrarle, sia che i server siano montanti o meno. Questo metodo ha meno problemi con i caratteri speciali (che altrimenti devono essere preceduti dal carattere di escape) all'interno delle password. Il formato è:

```
machine remoteserver  
login myuser
password mypassword

```

La linea nel file `/etc/autofs/auto.ftp` sarà quindi così senza utenti e password:

```
servername -fstype=curl,allow_other    :ftp\://remoteserver

```

Creare il file `/sbin/mount.curl` inserendo questo codice:

 `/sbin/mount.curl` 
```
#! /bin/sh
curlftpfs $1 $2 -o $4,disable_eprt
```

Creare il file `/sbin/umount.curl` inserendo questo codice:

 `/sbin/umount.curl` 
```
#! /bin/sh
fusermount -u $1
```

Impostare i permessi sui file:

```
# chmod 755 /sbin/mount.curl
# chmod 755 /sbin/umount.curl

```

Dopo un riavvio sarà possibile accedere ai server FTP in `/media/ftp/servername`

#### Server remoti SSH

Queste sono le istruzioni base per accedere al [filesystem remoto](/index.php/SSHFS "SSHFS") tramite [SSH](/index.php/SSH_(Italiano) "SSH (Italiano)") usando AutoFS.

**Nota:** L'esempio seguente non contempla l'uso di ssh-passphrase, per semplificare la procedura di installazione, notare che può essere un rischio sotto il punto di vista della sicurezza dell'integrità del sistema.

Installare [sshfs](https://www.archlinux.org/packages/?name=sshfs) dai [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

Caricare il modulo `fuse`.

Aggiungere il `fuse` all'interno dell'array `MODULES` nel file `/etc/rc.conf` così verrà caricato ad ogni avvio del sistema:

Installare [openssh](https://www.archlinux.org/packages/?name=openssh). Generare dunque una coppia di [chiavi SSH](/index.php/SSH_keys_(Italiano) "SSH keys (Italiano)"):

```
$ ssh-keygen -t dsa

```

Quando il generatore di chiavi chiederà la passphrase, premere `Invio`. L'uso delle chiavi SSH senza passphrase non è sicuro, d'altro canto usare AutoFS con chiavi protette da passphrase aggiunge delle difficoltà d'uso che non sono(ancora) affrontate in questo articolo.

Successivamente, copiare la chiave pubblica sul server remoto:

```
$ ssh-copy-id -i /home/username/.ssh/id_dsa.pub username@remotehost

```

Controllare che il collegamento con il server non abbia bisogno dell'immissione della password:

```
$ sudo ssh -i /home/username/.ssh/id_dsa username@remotehost

```

**Nota:** Il precedente comando è necessario per aggiungere il server remoto alla lista dei `known_hosts` dell'utente root. Alternativamente può essere aggiunto all'interno del file `/etc/ssh/ssh_known_hosts`.

Creare una nuova voce per i server SSH nel file `/etc/autofs/auto.master`:

```
/media/ssh		/etc/autofs/auto.ssh	--timeout=60 --ghost

```

Creare il file `/etc/autofs/auto.ssh` ed aggiungere un server SSH:

```
servername     -fstype=fuse,rw,allow_other,IdentityFile=/home/username/.ssh/id_dsa :sshfs\#username@host\:/

```

Dopo aver riavviato, il server SSH sarà accessibile in `/media/ssh/servername`.

## Risoluzione di problemi

Questa sezione contiene alcune soluzioni ai problemi comuni con AutoFS.

### Uso di NIS

A partire dalla versione 5.0.5 di AutoFS è stato introdotto un supporto avanzato per [NIS](/index.php/NIS "NIS"). Per usare AutoFs insieme a NIS, aggiungere `yp:` prima del nome indicato nel file `/etc/autofs/auto.master`:

```
/home   yp:auto_home    --timeout=60 
/sbtn   yp:auto_sbtn    --timeout=60
+auto.master

```

Nelle precedenti versioni(prima della 5.0.4) per usare NIS, sarà necessario aggiungere `nis` al file `/etc/nsswitch.conf`:

```
automount: files nis

```

### Parametri Opzionali

Sarà possibile usare parametri opzionali come `timeount` per tutte le periferiche gestite da AutoFS in `/etc/conf.d/autofs`:

*   Aprire il file `/etc/conf.d/autofs` e modificare la linea `daemonoptions`:

```
daemonoptions='--timeout=5'

```

*   Per abilitare il log (di default non è abilitato nessun log), aggiungere `--verbose` alla linea `daemonoptions` nel file `/etc/conf.d/autofs`, ad esempio:

```
daemonoptions='--verbose --timeout=5'

```

Dopo aver riavviato il demone `autofs`, i messaggi delle attività sarranno visibili in `/var/log/daemon.log`.

### Identificare le periferiche rimovibili

Se si utilizzano molte periferiche rimovibili come pennine/dischi USB e si vogliono distinguere, sarà possibile usare AutoFS per impostare i punti di mount ed [Udev](/index.php/Udev_(Italiano) "Udev (Italiano)") per creare nomi differenti per le periferiche USB. Consultare [questo articolo](/index.php/Map_Custom_Device_Entries_with_udev "Map Custom Device Entries with udev") per informazioni sulle configurazioni delle regole di Udev.

### Permessi per AutoFS

Se AutoFS non funziona correttamente, assicurarsi che i permessi dei file template siano corretti, altrimenti AutoFS non si avvierà. Questo può succedere ad esempio se si è ripristinato un backup effettuato senza mantenere i permessi dei file. Qui sono elencati gli schemi dei permessi che dovrebbero avere i file:

*   0644 - /etc/autofs/auto.master
*   0644 - /etc/autofs/auto.media
*   0644 - /etc/autofs/auto.misc
*   0644 - /etc/conf.d/autofs

In generale, gli script(come il precedente `auto.net` dovranno essere eseguibili (`chown a+x filename` mentre l'elenco dei mount no.

Se nel file `/var/log/daemon.log` sono presenti messaggi simili a questi, allora sono presenti problemi con i permessi.

```
May  7 19:44:16 peterix automount[15218]: lookup(program): lookup for petr failed
May  7 19:44:16 peterix automount[15218]: failed to mount /media/cifs/petr

```

## Altre risorse

*   Le informazioni originali di questa pagina sono basate su [questo topic](https://bbs.archlinux.org/viewtopic.php?t=7630), con informazioni aggiuntive prese da [questa pagina](http://libranet.com/support/2.8/0381)
*   L'uso dei server FTP ed SSH con AutoFS è basato su [questo articolo](https://web.archive.org/web/20130414074212/http://en.gentoo-wiki.com/wiki/Mounting_SFTP_and_FTP_shares) del Wiki di Gentoo.
*   Maggiori informazioni riguardo a SSH possono essere trovate nelle pagine del wiki [SSH](/index.php/SSH_(Italiano) "SSH (Italiano)") ed [Uso delle chiavi SSH](/index.php/SSH_keys_(Italiano) "SSH keys (Italiano)").
*   Le informazioni per configurare NFS possono essere trovate nella pagina di wiki [NFS](/index.php/NFS_(Italiano) "NFS (Italiano)").

## Alternative ad AutoFS

*   [Thunar Volume Manager](/index.php/Thunar_(Italiano)#Thunar_Volume_Manager "Thunar (Italiano)") è un sistema di automount per gli utenti del file manager [Thunar](/index.php/Thunar_(Italiano) "Thunar (Italiano)").
*   [PCManFM](/index.php/PCManFM_(Italiano) "PCManFM (Italiano)") è un file manager leggero con integrato il supporto per accedere alle condivisioni di rete.
*   [udiskie](/index.php/Udiskie "Udiskie") è un servizio minimalistico per il mount automatico dei dischi, utilizza udisks