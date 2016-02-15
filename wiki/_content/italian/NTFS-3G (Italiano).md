[NTFS-3G](http://www.tuxera.com/community/ntfs-3g-download/) è una implementazione open source del file system NTFS di Microsoft che include il supporto in lettura e scrittura. Gli sviluppatori di NTFS-3G utilizzano il file system FUSE per agevolare lo sviluppo e la portabilità. Questo documento descrive come impostare al meglio NTFS-3G sul proprio computer.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Montaggio manuale](#Montaggio_manuale)
*   [3 Configurazione](#Configurazione)
    *   [3.1 Impostazioni predefinite](#Impostazioni_predefinite)
    *   [3.2 Abilitare Gruppi/Utenti](#Abilitare_Gruppi.2FUtenti)
    *   [3.3 Opzioni NTFS-3G basilari](#Opzioni_NTFS-3G_basilari)
*   [4 Ulteriori configurazioni](#Ulteriori_configurazioni)
    *   [4.1 KDE 4](#KDE_4)
    *   [4.2 NTFS-config](#NTFS-config)
*   [5 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [5.1 Filesystem NTFS danneggiato](#Filesystem_NTFS_danneggiato)
    *   [5.2 Errore in fase di montaggio](#Errore_in_fase_di_montaggio)
*   [6 Ulteriori risorse](#Ulteriori_risorse)

## Installazione

Installare il pacchetto [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) disponibile nel repository `[extra]` con il comando:

```
# pacman -S ntfs-3g

```

## Montaggio manuale

Esistono due opzioni per il montaggio manuale delle partizioni NTFS. Il tradizionale:

```
# mount -t ntfs-3g /dev/<your-NTFS-partition> /{mnt,...}/<folder>

```

Il tipo di montaggio `ntfs-3g` non ha bisogno di essere specificato esplicitamente in Arch. Il comando `mount` utilizzerà in maniera predefinita `/sbin/mount.ntfs` che è collegato (symlink) a `/bin/ntfs-3g` dopo che il pacchetto ntfs-3g è stato installato.

La seconda opzione è quella di richiamare `ntfs-3g` direttamente:

```
# ntfs-3g /dev/<your-NTFS-partition> /<mount-location>

```

## Configurazione

La partizione NTFS può essere configurata per il montaggio automatico, o preconfigurata per poter essere montata in un certo modo secondo le preferenze dell'utente. Questa configurazione può essere effettuata nella configurazione dei filesystem statici ([fstab](/index.php/Fstab "Fstab")) o mediante l'uso di regole udev.

### Impostazioni predefinite

Utilizzando le impostazioni predefinite si monterà la partizione (o partizioni) NTFS in fase di avvio. Con questo metodo, **se** la cartella principale (che è montata), ha impostati correttamente i permessi di utente e gruppo, allora questi ultimi saranno in grado di leggere e scrivere su tale partizione.

Aggiungere la seguente riga in `/etc/fstab`:

```
# <file system>   <dir>		<type>    <options>             <dump>  <pass>
/dev/<NTFS-part>  /mnt/windows  ntfs-3g   defaults		  0       0

```

### Abilitare Gruppi/Utenti

Si possono anche impostare in fstab (per mezzo di ntfs-3g) altre opzioni, come quali utenti sono autorizzati ad accedere (in lettura) alla partizione. Per esempio, per permettere l'accesso ai membri del gruppo **users**:

```
/dev/<NTFS-part>  /mnt/windows  ntfs-3g   gid=users,umask=0022    0       0

```

Per impostazione predefinita, il driver ntfs-3g abilita il supporto in scrivere solo a root. Per abilitare la scrittura agli utenti, utilizzare il parametro dmask:

```
/dev/<NTFS-part>  /mnt/windows  ntfs-3g   gid=users,fmask=113,dmask=002    0       0

```

Nel caso di una macchina con un singolo utente, si può impostare l'utente come proprietario del filesystem:

```
/dev/<NTFS-part>  /mnt/windows  ntfs-3g   uid=USERNAME,gid=users    0       0

```

### Opzioni NTFS-3G basilari

Per la maggior parte dei casi, le impostazioni sopraelencate dovrebbero essere sufficienti. Seguono alcune opzioni di carattere generale utilizzate spesso nei vari filesystem Linux. Per un elenco completo, vedere [qui](http://www.tuxera.com/community/ntfs-3g-manual/#6)

*   **umask**: umask è un comando built-in della shell che imposta automaticamente i permessi dei file su file appena creati. Su Arch la umask predefinita per root e utente è 0022\. Con 0022 le nuove cartelle hanno i permessi 755 e i nuovi file hanno permessi 644\. Per maggiori informazioni sulle autorizzazioni umask vedere [qui](http://www.cyberciti.biz/tips/understanding-linux-unix-umask-value-usage.html).
*   **noauto**: Se impostato, le partizioni NTFS in fstab non vengono montate automaticamente all'avvio.
*   **uid** : il valore decimale dell'utente possessore dei file e delle cartelle di una certa partizione NTFS. Il proprio uid può essere trovato con il comando `id` .
*   **fmask** e **dmask**: simili a **umask** ma con una definizione rispettivamente individuale di file e directory.
*   **locale** : (deprecato da gennaio 2009) - ~~spesso richiesto per rendere visibili file con caratteri "specifici di una certa lingua".~~

## Ulteriori configurazioni

Alcune configurazioni che potrebbero aiutare a configurare la partizione NTFS.

### KDE 4

Su >=KDE 4.4, click destro sul Device Notifier applet e scegliere **Device Notifier Settings** poi da **Removable Devices** selezionare la partizione e scegliere **Automount on login**.

### NTFS-config

[ntfs-config](https://aur.archlinux.org/packages/ntfs-config/) è un programma che può aiutare a configurare le proprie partizioni NTFS se altri metodi non funzionano.

## Risoluzione dei problemi

Alcune idee per risolvere i problemi comuni.

### Filesystem NTFS danneggiato

Se un file system NTFS è affetto da alcuni errori, NTFS-3G lo monta in sola lettura. Per aggiustare un filesystem NTFS, caricare Windows ed eseguire il programma di controllo del disco nativo.

Per poter intervenire su un file system NTFS, il dispositivo deve essere già smontato. Ad esempio, per una partizione NTFS su /dev/sda2:

```
# umount /dev/sda2
# ntfsfix /dev/sda2
Mounting volume... OK
Processing of $MFT and $MFTMirr completed successfully.
NTFS volume version is 3.1.
NTFS partition /dev/sda2 was processed successfully.
# mount /dev/sda2

```

Se tutto è andato bene, il volume sarà ora nuovamente "scrivibile".

### Errore in fase di montaggio

Se non è possibile montare le partizioni NTFS anche dopo aver seguito questa guida, provare ad aggiungere la sezione UUID in `fstab` a tutte le partizioni ntfs.

## Ulteriori risorse

*   [Official NTFS-3G Manual](http://www.tuxera.com/community/ntfs-3g-manual/)