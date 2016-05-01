Sshfs può essere usato per effettuare il mount di file system remoti - accessibili tramite [SSH](/index.php/SSH_(Italiano) "SSH (Italiano)") - in una cartella locale, permettendo quindi di poter effettuare qualsiasi operazione sui file con qualsiasi strumento(copiare, rinominare, modificare con [vim](/index.php/Vim_(Italiano) "Vim (Italiano)") eccetera.). L'uso di sshfs invece di shfs è consigliato comunemente, in quanto shfs non ha avuto nuove versioni dal 2004.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Uso](#Uso)
    *   [2.1 Effettuare il mount](#Effettuare_il_mount)
    *   [2.2 Effettuare l'umount](#Effettuare_l.27umount)
*   [3 Tips](#Tips)
*   [4 Chroot](#Chroot)
*   [5 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [5.1 Connection reset by peer](#Connection_reset_by_peer)
    *   [5.2 Remote host has disconnected](#Remote_host_has_disconnected)
*   [6 fstab](#fstab)
*   [7 Opzioni](#Opzioni)
*   [8 Link correlati](#Link_correlati)

## Installazione

[Installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") il pacchetto [sshfs](https://www.archlinux.org/packages/?name=sshfs). Questo pacchetto ha come sua dipendenza [fuse](https://www.archlinux.org/packages/?name=fuse) e ne richiederà l'installazione (se non è già stato installato).

## Uso

Per prima cosa il modulo necessario al corretto funzionamento dovrebbe essere caricato (come utente *root*):

```
# modprobe fuse

```

(Sarà possibile inserire `fuse` nell'array `MODULES` all'interno del file `/etc/[rc.conf](/index.php/Rc.conf_(Italiano) "Rc.conf (Italiano)")` per farlo caricare automaticamente all'avvio.)

### Effettuare il mount

Si dovrà utilizzare il comando `sshfs`. Per effettuare il mount di una cartella remota:

```
*# sshfs NOMEUTENTE@NOMEMACCHINA_O_INDIRIZZOIP:/PERCORSO PUNTO_DI_MOUNT_LOCALE OPZIONI_SSH*

```

Ad esempio:

```
# sshfs sessy@mycomputer:/home/sessy /mnt/sessy -C -p 9876

```

Dove 9876 è il numero della porta.

Inoltre, assicurarsi prima di connettersi, di aver impostato i giusti permessi sui file, per le cartelle locali dove si vuole effettuare il mount di una cartella remota. Esempio: non lasciare che l'unico proprietario sia root! Sarà possibile utilizzare il comando di mount anche come utente normale, dovrebbe funzionare correttamente.

[SSH](/index.php/SSH_(Italiano) "SSH (Italiano)") richiederà la password, se necessaria. Se non si vuole inserire ogni volta la password, consultare; [Come usare l'autenticazione con una chiave RSA via SSH (in inglese)](http://linuxmafia.com/~karsten/Linux/FAQs/sshrsakey.html), oppure [usare le chiavi SSH](/index.php/SSH_keys_(Italiano) "SSH keys (Italiano)").

### Effettuare l'umount

Per effettuare l'umount delle cartelle remote:

```
*# fusermount -u PUNTO_DI_MOUNT_LOCALE*

```

Esempio:

```
# fusermount -u /mnt/sessy

```

## Tips

Per effettuare un mount rapido di una cartella remota, effettuare alcune operazioni sui file ed effettuare l'umount successivamente, inserire i seguenti comandi in uno script:

```
sshfs NOMEUTENTE@NOMEMACCHINA_O_INDIRIZZOIP:/PERCORSO PUNTO_DI_MOUNT_LOCALE OPZIONI_SSH
mc ~ PUNTO_DI_MOUNT_LOCALE
fusermount -u LOCAL_MOUNT_POINT

```

Questi comandi effettueranno il mount della cartella remota, eseguiranno MC ed infine smonteranno la cartella dopo l'uscita dal file-manager.

Thunar ha un problema con [FAM](/index.php/FAM_(Italiano) "FAM (Italiano)") e gli accessi a file remoti. Se le cartelle remote non vengono visualizzate, e si viene portati alla cartella `home`, oppure si hanno altri problemi di accesso a file remoti, sostituire [fam](https://aur.archlinux.org/packages/fam/) con [gamin](https://www.archlinux.org/packages/?name=gamin). Gamin è derivato da FAM. Installare quindi [gamin](https://www.archlinux.org/packages/?name=gamin) e rimuovere dal caricamento automatico il [demone](/index.php/Daemon_(Italiano) "Daemon (Italiano)") `fam`.

## Chroot

Potrebbe essere necessario abbinare un utente(specifico) ad una cartella. Per effettuare questo, modificare il file `/etc/ssh/sshd_config`:

 `/etc/ssh/sshd_config` 
```
.....
Match User nomeutente 
       ChrootDirectory /chroot/%u
       ForceCommand internal-sftp #per limitare l'utente all'uso di sftp
       AllowTcpForwarding no
       X11Forwarding no
.....
```

**Nota:** La cartella di chroot **deve** essere posseduta da root, altrimenti non sarà possibile connettersi. Per maggiori informazioni consultare le pagine di manuale relative a `Match, ChrootDirectrory` e `ForceCommand`.

## Risoluzione dei problemi

### Connection reset by peer

*   Se si sta tentando di accedere ad un sistema remoto tramite il nome macchina, provare utilizzando l'indirizzo IP, potrebbe essere un problema di risoluzione dei nomi. Assicurarsi di modificare il file `/etc/hosts` aggiungendo l'indirizzo ed il nome del server.
*   Se si stanno utilizzando chiavi con nomi non standard, passare l'opzione con `-i .ssh/my_key`, non funziona. Sarà necessario usare `-o IdentityFile=/home/user/.ssh/my_key`, specificando il percorso assoluto della chiave.
*   Aggiungere l'opzione '`sshfs_debug`' (ad esempio '`sshfs -o sshfs_debug user@server ...`') può aiutare ad avere maggiori informazioni per risolvere il problema.
*   Se si utilizza sshfs in una rete gestita da un router che esegue [DD-WRT](https://en.wikipedia.org/wiki/DD-WRT "wikipedia:DD-WRT") o simile, la soluzione può essere trovata [quì](http://www.dd-wrt.com/wiki/index.php/SFTP_with_DD-WRT).
*   Discussione sul forum internazionale: [sshfs: Connection reset by peer](https://bbs.archlinux.org/viewtopic.php?id=27613)

**Nota:** Quando vengono passate diverse opzioni per sshfs, devono essere separate da una virgola. In questo modo: '`sshfs -o sshfs_debug,IdentityFile=</path/to/key> user@server ...`')

### Remote host has disconnected

*   Se si riceve questo messaggio direttamente appena si tenta di utilizzare sshfs, provare a controllare il percorso del `Sybsystem` elencato nel file `/etc/ssh/sshd_config` sulla macchina remota, e controllare che sia corretto.
*   Sarà possibile constrollare digitando `find / grep XXXX` dove XXXX è il percorso del subsystem.

## fstab

Un esempio di come usare sshfs per montare un filesystem remoto tramite `/etc/[fstab](/index.php/Fstab_(Italiano) "Fstab (Italiano)")`

```
sshfs#NOMEUTENTE@NOMEMACCHINA_O_INDIRIZZOIP:/CARTELLA/REMOTA /PUNTO_DI_MOUNT/LOCALE fuse defaults 0 0

```

Ecco come potrebbe risultare la voce in fstab

```
sshfs#llib@192.168.1.200:/home/llib/FAH /media/FAH2 fuse defaults 0 0

```

Comunque questo non funzionerà automaticamente se non si utilizza una chiave ssh per l'utente. [SSH Keys](/index.php/SSH_keys_(Italiano) "SSH keys (Italiano)").

Se si vuole usare sshfs per diversi utenti:

```
sshfs#user@domain.org:/home/user  /media/user   fuse    defaults,allow_other    0  0

```

**Nota:** Con il precedente metodo, l'umount non verrà effettuato perché il filesystem non si trova in `fstab`. Per evitare questo errore, rimuovere il prefisso '`sshfs#`', cambiare il filesystem da '`fuse`' a '`fuse.sshfs`', quindi creare uno script chiamato '`sbin/mount.fuse.sshfs`': `/sbin/mount.fuse.sshfs` 
```
#!/bin/bash
DEVICE="$1"
MOUNTPOINT="$2"
OPTIONS="$4"

OPTIONS="${OPTIONS/,noauto/}"
OPTIONS="${OPTIONS/,user/}"

# workaround per evitare il conflitto dell'opzione 'user'
# in fstab, specificare 'login=joe' invece di 'user=joe'
OPTIONS="${OPTIONS/,login=/,user=}"

exec /usr/bin/sshfs "$DEVICE" "$MOUNTPOINT" -o "$OPTIONS"
```

Se si ottiene l'errore "connection reset by peer" usando il metodo di fstab, è probabile che il pc non sia connesso ad internet durante quella fase dell'avvio. La soluzione consiste nell'aggiungere alle applicazioni di avvio del proprio DE/WM il comando di mount tramite sshfs. A questo punto dell'avvio la connessione dovrebbe essere stata stabilita.

## Opzioni

sshfs può convertire automaticamente l'id dell'utente locale e remoto, se si aggiunge l'opzione `idmap`:

```
# sshfs -o idmap=user sessy@mycomputer:/home/sessy /mnt/sessy -C -p 9876

```

Se per il server remoto si utilizza un nome utente diverso da quello in uso, può funzionare se viene utilizzata l'opzione ssh `User`:

```
# sshfs -o idmap=user,User=sessy2 sessy@mycomputer:/home/sessy /mnt/sessy -C -p 9876

```

(La prima forma è stata testata, la seconda è basata sulla documentazione, quindi potrebbe risultare leggermente differente.)

## Link correlati

*   [SSH](/index.php/SSH_(Italiano) "SSH (Italiano)")
*   [How to: effettuare il mount di filesystem in chroot tramite SSH(in inglese)](http://wiki.lapipaplena.org/index.php/How_to_mount_SFTP_accesses), con maggiori approfondimenti riguardo ai proprietari ed alle opzioni dei permessi.