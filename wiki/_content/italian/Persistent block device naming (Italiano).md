Questo articolo descrive come utilizzare dei nomi univoci e non modificabili per l'identificazione delle periferiche(o partizioni). Questo è stato reso possibile con l'introduzione di udev, e risulta vantaggioso anche rispetto ai nomi basati sul bus di connessione. Se la macchina ha più di un controller per i dischi SATA, SCSI o IDE, può succedere che l'ordine dei file nodo creati sia casuale. Questo può comportare ad esempio che le periferiche `/dev/**sda**` ed `/dev/**sdb**` siano invertite in modo casuale ad ogni avvio, impedendo al sistema di avviarsi, oppure determinando la scomparsa dei dispositivi a blocchi che vengono erroneamente rilevati. L'uso di nomi univoci risolve quindi il problema.

**Nota:** Non è necessario seguire questa guida nel caso in cui si stia utilizzando [LVM2](/index.php/LVM_(Italiano) "LVM (Italiano)"), dato che LVM2 si occupa anche di questo automaticamente.

## Contents

*   [1 Metodi di nomenclatura univoca](#Metodi_di_nomenclatura_univoca)
    *   [1.1 By-label](#By-label)
    *   [1.2 By-uuid](#By-uuid)
    *   [1.3 By-id e by-path](#By-id_e_by-path)
*   [2 Utilizzare i nomi univoci](#Utilizzare_i_nomi_univoci)
    *   [2.1 fstab](#fstab)
    *   [2.2 Boot manager](#Boot_manager)

## Metodi di nomenclatura univoca

Ci sono quattro differenti modi per assegnare dei nomi univoci alle periferiche:by-label,by-uuid,by-id e by-path. Nei paragrafi successivi verranno descritte le differenze tra i vari metodi e come vengono utilizzati.

### By-label

Quasi tutti i filesystem supportano le etichette. Tutte le partizioni che ne hanno una sono elencate nella cartella `/dev/disk/by-label`.

**Nota:** Questa cartella viene creata (e rimossa) dinamicamente, a seconda delle partizioni presenti ed aventi una etichetta.

 `$ ls -lF /dev/disk/by-label` 

```
total 0
lrwxrwxrwx 1 root root 10 Oct 16 10:27 data -> ../../sdb2
lrwxrwxrwx 1 root root 10 Oct 16 10:27 data2 -> ../../sda2
lrwxrwxrwx 1 root root 10 Oct 16 10:27 fat -> ../../sda6
lrwxrwxrwx 1 root root 10 Oct 16 10:27 home -> ../../sda7
lrwxrwxrwx 1 root root 10 Oct 16 10:27 root -> ../../sda1
lrwxrwxrwx 1 root root 10 Oct 16 10:27 swap -> ../../sda5
lrwxrwxrwx 1 root root 10 Oct 16 10:27 windows -> ../../sdb1

```

Le etichette possono essere cambiate utilizzando i seguenti comandi:

	swap 

```
# mkswap -L <label> /dev/XXX

```

**Attenzione:** Questo comando cancellerà l'area di swap.

Se la swap è montata, eseguire `swapoff /dev/XXX` prima e `swapon /dev/XXX` dopo.

	ext2/ext3/ext4 

```
# e2label /dev/XXX <label>

```

	btrfs 

```
# btrfs filesystem label /dev/XXX <label>

```

	reiserfs 

```
# reiserfstune -l <label> /dev/XXX

```

	jfs 

```
# jfs_tune -L <label> /dev/XXX

```

	xfs 

```
# xfs_admin -L <label> /dev/XXX

```

	fat/vfat (contenuto nel pacchetto mtools) 

```
# mlabel -i /dev/XXX ::<label>

```

	ntfs (contenuto nel pacchetto [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g)) 

```
# ntfslabel /dev/XXX <label>

```

**Attenzione:** Le etichette dovranno essere uniche per rendere efficace questo metodo, e non superare i 16 caratteri.

### By-uuid

Gli [UUID](http://en.wikipedia.org/wiki/UUID), ovvero _Universally Unique Identifier(identificatore unico universale)_, è un meccanismo che assegna ad ogni filesystem un identificatore unico. Esso è studiato in modo da evitare conflitti. Tutti i filesystem GNU/Linux (inclusa l'area di swap) supportano gli UUID. I filesystem FAT ed NTFS non supportano gli UUID, ma sono comunque elencate in `/dev/disk/by-uuid` con un identificatore unico:

 `$ ls -lF /dev/disk/by-uuid/` 

```
total 0
lrwxrwxrwx 1 root root 10 Oct 16 10:27 2d781b26-0285-421a-b9d0-d4a0d3b55680 -> ../../sda1
lrwxrwxrwx 1 root root 10 Oct 16 10:27 31f8eb0d-612b-4805-835e-0e6d8b8c5591 -> ../../sda7
lrwxrwxrwx 1 root root 10 Oct 16 10:27 3FC2-3DDB -> ../../sda6
lrwxrwxrwx 1 root root 10 Oct 16 10:27 5090093f-e023-4a93-b2b6-8a9568dd23dc -> ../../sda2
lrwxrwxrwx 1 root root 10 Oct 16 10:27 912c7844-5430-4eea-b55c-e23f8959a8ee -> ../../sda5
lrwxrwxrwx 1 root root 10 Oct 16 10:27 B0DC1977DC193954 -> ../../sdb1
lrwxrwxrwx 1 root root 10 Oct 16 10:27 bae98338-ec29-4beb-aacf-107e44599b2e -> ../../sdb2

```

Come si può notare, le partizioni FAT ed NTFS (le partizioni aventi etichetta _fat_ e _windows_ nell'esempio precedente) hanno nomi più corti, ma vengono comunque elencate. Il vantaggio nell'uso degli UUID sta nel fatto che è molto meno probabile avere conflitti rispetto al metodo delle etichette. Uno svantaggio è invece che i nomi sono molto meno immediati da leggere o ricordare.

### By-id e by-path

In `by-id` viene creato un nome dipendente dal numero seriale dell'hardware. In `by-path` invece viene creato un nome unico dipendente dal più corto percorso fisico (secondo sysfs). In entrambi i percorsi sono contenute delle stringhe per indicare il tipo a cui appartengono(es. "-ide-" in 'by-path', ed "-ata-" in 'by-id'), comunque entrambi i metodi non sono adatti alla risoluzione del problema menzionato all'inizio dell'articolo. Non saranno quindi approfonditi oltre.

## Utilizzare i nomi univoci

A seconda del metodo scelto, ecco come abilitarlo sul proprio sistema:

### fstab

Per abilitare i nomi univoci in `/etc/fstab` sostituire il nome della periferica assegnata dal kernel nella prima colonna con il corrispondente percorso:

```
/dev/disk/by-label/home ...
/dev/disk/by-uuid/31f8eb0d-612b-4805-835e-0e6d8b8c5591 ...

```

oppure specificare direttamente il nome univoco usando un prefisso:

```
LABEL=home ...
UUID=1f8eb0d-612b-4805-835e-0e6d8b8c5591 ...

```

### Boot manager

Per usare i nomi univoci nel proprio boot manager, sarà necessario soddisfare i seguenti requisiti:

*   Il sistema usa un initramfs creato mediante [mkinitcpio](/index.php/Mkinitcpio_(Italiano) "Mkinitcpio (Italiano)")
*   Nel file `/etc/mkinitcpio.conf` sia abilitato l'hook udev
*   L'immagine initramfs è stata generata, con una versione di _klibc-udev_ superiore alla **101-3**(**con le versioni precedenti i nomi univoci non funzionano correttamente.**). Se si aggiorna _klibc-udev_ da una versione precedente e si intende usare i nomi univoci, rigenerare l'immagine initramfs prima di riavviare.

Nell'esempio precedente, `/dev/sda1` è la partizione di root. Nel file `/boot/grub/menu.lst` di [GRUB Legacy](/index.php/GRUB_Legacy_(Italiano) "GRUB Legacy (Italiano)"), la riga _kernel_ sarà simile a questa:

```
kernel /boot/vmlinuz-linux root=/dev/sda1 ro quiet

```

A seconda del metodo che si intende utilizzare, cambiare la riga come una delle seguenti:

```
kernel /boot/vmlinuz-linux root=/dev/disk/by-label/root ro quiet

```

oppure

```
kernel /boot/vmlinuz-linux root=/dev/disk/by-uuid/2d781b26-0285-421a-b9d0-d4a0d3b55680 ro quiet

```

Se si usa [LILO](/index.php/LILO "LILO"), non inserire il nome univoco nell'opzione `root=...`, non funzionerebbe. Sarà invece necessario usare le opzioni `append="root=..."` o `addappend="root=..."`. Consultare il manuale di LILO per maggiori informazioni riguardo alle opzioni _append_ ed _addappend_.

C'è un metodo alternativo per usare le etichette dei filesystem. Ad esempio se (come nell'esempio) il filesystem `/dev/sda1` ha l'etichetta "root", sarà possibile usare la seguente linea in GRUB:

```
 kernel /boot/vmlinuz-linux root=LABEL=root ro quiet

```