Articoli correlati

*   [Software RAID and LVM](/index.php/Software_RAID_and_LVM "Software RAID and LVM")
*   [System Encryption with LUKS](/index.php/System_Encryption_with_LUKS "System Encryption with LUKS")

Questo articolo fornirà un esempio su come installare e configurare Arch Linux utilizzando il Logical Volume Manager (LVM).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Introduzione](#Introduzione)
*   [2 Vantaggi](#Vantaggi)
*   [3 Installazione](#Installazione)
    *   [3.1 Installare Arch Linux su LVM](#Installare_Arch_Linux_su_LVM)
    *   [3.2 Partizionare i dischi](#Partizionare_i_dischi)
    *   [3.3 Creare i volumi fisici(Physical volumes)](#Creare_i_volumi_fisici(Physical_volumes))
    *   [3.4 Creare gruppi di volumi (Volume group)](#Creare_gruppi_di_volumi_(Volume_group))
    *   [3.5 Creare i volumi logici (Logical Volumes)](#Creare_i_volumi_logici_(Logical_Volumes))
    *   [3.6 Creare i filesystem ed effettuare il mount dei volumi logici](#Creare_i_filesystem_ed_effettuare_il_mount_dei_volumi_logici)
    *   [3.7 Impostare i filesystem ed i punti di mount](#Impostare_i_filesystem_ed_i_punti_di_mount)
    *   [3.8 Configurare il sistema](#Configurare_il_sistema)
*   [4 Configurazione](#Configurazione)
    *   [4.1 Ingrandire un volume logico](#Ingrandire_un_volume_logico)
    *   [4.2 Ridurre un volume logico](#Ridurre_un_volume_logico)
    *   [4.3 Rimuovere volumi logici](#Rimuovere_volumi_logici)
    *   [4.4 Aggiungere un volume fisico ad un gruppo di volumi](#Aggiungere_un_volume_fisico_ad_un_gruppo_di_volumi)
    *   [4.5 Rimuovere una partizione da un gruppo di volumi](#Rimuovere_una_partizione_da_un_gruppo_di_volumi)
    *   [4.6 Snapshots](#Snapshots)
        *   [4.6.1 Introduzione](#Introduzione_2)
        *   [4.6.2 Configurazione](#Configurazione_2)
*   [5 Risoluzione di problemi](#Risoluzione_di_problemi)
    *   [5.1 I comandi LVM commands non funzionano](#I_comandi_LVM_commands_non_funzionano)
    *   [5.2 Nela pagina Set Filesystem Mountpoints i volumi logici non sono mostrati](#Nela_pagina_Set_Filesystem_Mountpoints_i_volumi_logici_non_sono_mostrati)
    *   [5.3 LVM su periferiche rimovibili](#LVM_su_periferiche_rimovibili)
*   [6 Altre risorse](#Altre_risorse)

## Introduzione

[Wikipedia:Logical Volume Manager (Linux)](https://en.wikipedia.org/wiki/Logical_Volume_Manager_(Linux) "wikipedia:Logical Volume Manager (Linux)")

**LVM** (Logical Volume Management) utilizza la funzione di [device-mapper](http://sources.redhat.com/dm/) del kernel Linux per fornire un sistema di partizioni che sia indipendente dalla sottostante struttura del disco fisico. Con LVM è possibile crere uno spazio di archiviazione astratto ed avere "partizioni virtuali" il che rende più facile ingrandirene o ridurne la dimensione (sempre che il filesystem che vi risede lo permetta) permette inoltre di aggiungere/rimuovere partizioni senza preoccuparsi di avere spazio contiguo a disposizione su uno specifico disco, senza incorrere nel problema di effettuare un fdisk su un disco in uso (senza preoccuparsi se il kernel stia usando la vecchia o la nuova tavola delle partizioni) e senza aver bisogno di spostare altre partizioni dal loro posto. Questo è una semplificazione nella gestione: non fornisce nessuna sicurezza per i dati. Comunque, si integra bene con le altre due tecnologie che vengono utilizzate.

Nota che LVM non è utilizzato per la partizione `/boot`, a causa di problemi con il bootloader.

**Tip:** /boot non può risiedere su di una partizione LVM se viene utilizzato [GRUB Legacy](/index.php/GRUB_Legacy_(Italiano) "GRUB Legacy (Italiano)"), il quale non supporta LVM. Se si vuole utilizzare LVM anche per la partizione di /boot sarà necessario utilizzare [GRUB2](/index.php/GRUB2_(Italiano) "GRUB2 (Italiano)").

Le componenti base di LVM sono:

*   **Volume Fisico(Physical volume (PV))**: Partizione del disco(oppure anche l'intero disco o un file di loopback) sul quale è possibile creare un gruppo di volumi. Ha un header speciale ed è diviso in estensioni fisiche. Si pensi al volume fisico come grandi blocchi che possono essere usati per costruire il nostro hard drive.
*   **Gruppo di Volumi(Volume group (VG))**: Un insieme di volumi fisici usati come un unico volume di archiviazione(come un disco). Essi contengono i volumi logici.Si pensi ai gruppi di volumi come agli hard drive.
*   **Volume Logico(Logical volume (LV))**: Una "partizione virtuale/logica" che risiede in un volume logico ed è composta da estensioni fisiche. Si pensi ai volumi logici come una normale partizione.
*   **Estensione Fisica(Physical extent (PE))**: Una piccola porzione di un disco (solitamente 4MB) che può assegnata ad un volume logico. Si pensi alle estensioni fisiche come porzioni di dischi che posso essere allocate ad una qualsiasi partizione.

Con LVM sarà più facile gestire le proprie partizioni (volumi logici) rispetto ad un disco partizionato normalmente. Ad esempio, sarà possibile:

*   Usare *un qualsiasi numero* di dischi come un grande disco(VG)
*   Avere partizioni(LV) sparse *sopra* a diversi dischi (possono essere grandi quanto la capacità di archiviazione di tutti i dischi insieme)
*   Ridimensionare/creare/eliminare partizioni(LV) e dischi(VG) *come si vuole* (non esiste il vincolo della posizione dei volumi logici nel gruppo di volumi come invece per le normali partizioni)
*   Ridimensionare/creare/cancellare partizioni(LV) e dischi(VG) *online* (i filesystem che risiedono su di essi dovranno essere ridimensionati, ma solo alcuni supportano il ridimensionamento online)
*   *Chiamare* i propri dischi(VG) e le proprie partizioni(LV) come si desidera
*   Creare piccole partizioni(LV) e ridimensionarle "*dinamicamente*" appena esse si riempono (l'allargamento del filesystem dovrà essere eseguito a mano, ma può essere effettuato online con alcuni filesystem)
*   ...

Esempio:

```
**Dischi fisici**

  Disco1 (/dev/sda):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
    |Partizione1 50GB (Volume fisico)  |Partizione2 80GB (Volume fisico)      |
    |/dev/sda1                         |/dev/sda2                             |
    |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |

  Disco2 (/dev/sdb):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
    |Partizione1 120GB (Volume fisico)                  |
    |/dev/sdb1                                          |
    | _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ __ _ _|

```

```
**Volumi logici LVM**

  Gruppo di volumi1 (/dev/MyStorage/ = /dev/sda1 + /dev/sda2 + /dev/sdb1):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 
    |Volume logico1  15GB  |volume logico2 35GB       |Volume logico3  200GB               |
    |/dev/MyStorage/rootvol|/dev/MyStorage/homevol    |/dev/MyStorage/mediavol             |
    |_ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |

```

Per riassumere: con LVM si può utilizzare tutto il proprio spazio di archiviazione come un unico grande disco (gruppo di volumi) ed avere una maggiore flessibilità nella gestione delle partizioni (volumi logici).

## Vantaggi

Qui sono elencate alcune cose che è possibile realizzare con LVM che non possono (oppure non sono facilmente realizzabili) con il semplice uso di mdadm, partizioni MBR, partizioni GPT, parted/gparted e strumenti a livello file come rsync.

1.  Ridimensionamento online/live.
2.  Non sono più necessarie partizioni estese (non lo sono nemmeno per i partizionamenti GPT)
3.  Ridimensionare le partizioni senza il problema del loro ordine sul disco (non è necessario preoccuparsi dello spazio contiguo disponibile)
4.  Migrazione online/live delle partizioni usate da servizi senza dover riavviare i servizi.

Questo può essere molto utile su di un server, senza interfaccia grafica quindi, ma sarà necessario decidere se le sue caratteristiche valgono l'astrazione.

## Installazione

Prima poter procedere sarà necessario caricare il modulo appropriato:

```
# modprobe dm-mod

```

Se Arch Linux è già installata e si vuole solamente provare/aggiungere una partizione usando LVM, saltare al paragrafo [Partizionare i dischi](#Partizionare_i_dischi).

### Installare Arch Linux su LVM

Prima di eseguire gli script di installazione di Arch Linux (`/arch/setup`), sarà necessario partizionare il disco con `cfdisk` (oppure un altro strumento a piacimento). Dato che grub legacy (GRUB avente un numero versione minore di 1.0) non può effettuare il boot da volumi logici LVM non sarà possibile avere la partizione `/boot` su LVM, creare quindi una partizione dedicata. 100 MB dovrebbero bastare. Una alternativa consiste nell'utilizzare LILO oppure GRUB versione 1.95 o maggiore.

### Partizionare i dischi

Successivamente sarà necessario creare una partizione per LVM. Il suo filesystem dovrebbe essere 'Linux LVM', usare quindi l'identificazione di partizione 0x8e (tipo di filesystem: 8e). Sarà necessario creare solo una partizione LVM su ogni disco che si intende utilizzare con LVM. I dischi logici risiederanno all'interno di queste partizioni quindi scegliere le dimensioni in modo adeguato. Se si intende utilizzare solo LVM e nessuna partizione esterna, usare tutto lo spazio libero su ogni disco.

**Attenzione:** /boot non può risiedere su LVM se viene utilizzato [GRUB Legacy](/index.php/GRUB_Legacy_(Italiano) "GRUB Legacy (Italiano)"), il quale non supporta LVM. Se si vuole utilizzare LVM anche per la partizione di /boot sarà necessario utilizzare [GRUB2](/index.php/GRUB2_(Italiano) "GRUB2 (Italiano)").

**Tip:** Tutte le partizioni LVM su tutti i dischi possono essere configurate per apparire come un unico grande disco.

### Creare i volumi fisici(Physical volumes)

Adesso sarà necessario inizializzare le partizioni così che possano essere utilizzate da LVM. Usare `fdisk -l` per determinare quali partizioni hanno come tipo di filesystem 'Linux LVM' e creare il volume fisico su di esse:

```
# pvcreate /dev/sda2

```

Sostituire `/dev/sda2` con le partizioni su cui si vuole creare il volume fisico. Questo comando crea un intestazione su tutte le partizioni così che possano essere usate per LVM. Si possono monitorare i volumi fisici creati con il comando:

```
# pvdisplay

```

**Nota:** Se si utilizza un disco SSD utilizzare `pvcreate --dataalignment 1m /dev/sda2` (per cancellare block size < 1MiB), consultare ad esempio [questa discussione](http://serverfault.com/questions/356534/ssd-erase-block-size-lvm-pv-on-raw-device-alignment)

### Creare gruppi di volumi (Volume group)

Il prossimo passo consiste nel creare un gruppo di volumi su questo volume fisico. Prima si dovrà creare un gruppo di volumi su una delle nuove partizioni e successivamente aggiungere gli altri volumi fisici che lo comporranno:

```
# vgcreate VolGroup00 /dev/sda2
# vgextend VolGroup00 /dev/sdb1

```

Sarà possibile utilizzare un qualsiasi altro nome invece di VolGroup00 per il gruppo di volumi durante la sua creazione. Sarà possibile controllare come si stanno espandendo i gruppi di volumi con il comando:

```
# vgdisplay

```

**Nota:** Sarà possibile creare più di un gruppo di volumi se necessario, ma così il nostro storage non sarà più rappresentato come un solo dico..

### Creare i volumi logici (Logical Volumes)

Adesso verranno creati i volumi logici su questo gruppo di volumi. Creare il volume logico con il seguente comando specificando il nome del volume logico, la sua dimensione, ed il gruppo di volumi dove risiederà:

```
# lvcreate -L 10G VolGroup00 -n lvolhome

```

Questo comando creerà un volume logico al quale sarà possibile accedere con `/dev/mapper/VolGroup00-lvolhome` o `/dev/VolGroup00/lvolhome`. Come per il gruppo di volumi, sarà possibile utilizzare qualsiasi nome per il volume logico durante la sua creazione.

Per creare una partizione di swap su di un volume logico, sarà necessario un argomento aggiuntivo:

```
# lvcreate -C y -L 10G VolGroup00 -n lvolswap

```

L'opzione `-C y` è usata per creare una partizione contigua, cioè la partizione di swap non sarà allocata su più di un disco oppure su estensioni fisiche (PE) non contigue.

Se si vuole riempire tutto lo spazio libero rimasto in un gruppo di volumi, utilizzare il seguente comando:

```
# lvcreate -l +100%FREE VolGroup00 -n lvolmedia

```

Si può controllare i volumi logici creati con:

```
# lvdisplay

```

**Nota:** Potrebbe essere necessario caricare il modulo *device-mapper* del kernel (**modprobe dm-mod**) affinché il comando sopra citato abbia successo.

**Tip:** Sarà possibile iniziare con relativamente piccole dimensioni per i volumi logici ed espanderli successivamente se necessario. Per semplicità lasciare dello spazio libero nel gruppo di volumi così da avere spazio per le espansioni dei volumi logici.

### Creare i filesystem ed effettuare il mount dei volumi logici

Adesso i volumi logici dovrebbero essere situati in `/dev/mapper/` e `/dev/NomeGruppoDiVolumi`. Se non fosse possibile trovarli, usare il prossimo comando per caricare il modulo per la creazione dei nodi dei device e per rendere accessibili i gruppi di volumi:

```
# modprobe dm-mod
# vgscan
# vgchange -ay

```

Adesso sarà possibile creare i filesystem sui volumi logici ed effettuarne il mount come per le normali partizioni (se si sta installando Arch Linux, fare riferimento al paragrafo [montare le partizioni](/index.php/Beginners%27_guide_(Italiano)#Montare_le_partizioni "Beginners' guide (Italiano)") per maggiori dettagli):

```
# mkfs.ext3 /dev/mapper/VolGroup00-lvolhome
# mount /dev/mapper/VolGroup00-lvolhome /home

```

~~Se si sta installando Arch Linux, avviare `/arch/setup`, selezionare *Prepare Hard Drive* direttamente al passaggio 3 *Set Filesystem Mountpoints* e ***leggere le seguenti [sezioni](#_Impostare_i_filesystem_ed_i_punti_di_mount) prima di procedere con l'installazione!***~~

### Impostare i filesystem ed i punti di mount

*   Quando si sceglie il punto di mount, selezionare il volume logico appena creato (utilizzare: `/dev/mapper/Volgroup00-lvolhome`).
    NON selezionare le partizioni usate per creare il volume logico (non utilizzare: `/dev/sda2`).

### Configurare il sistema

L'opzione `use_lvmetad = 1` deve essere impostata nel file `/etc/lvm/lvm.conf`. Come di default nelle nuove configurazioni fornite dal pacchetto [lvm2](https://www.archlinux.org/packages/?name=lvm2) - nel caso sia presente il file `lvm.conf.pacnew`, sarà necessario confrontare i cambiamenti dei file.

In caso si abbia necessità del monitoraggio dei volumi(necessario per l'uso degli snapshots):

```
# systemctl enable lvm-monitoring.service

```

Se si utilizza LVM su un device criptato, sarà necessario utilizzare invece:

```
# systemctl enable lvm-on-crypt.service

```

Oppure, se si utilizza sysvinit, modificare il valore di `USELVM` in modo appropriato:

 `# vim /etc/rc.conf`  `USELVM="yes"` 

A partire dal 02.12.2013 saranno necessarie le segueti modifiche. Sarà necessario assicurarsi che gli hook `lvm2` ed `udev` in [mkinitcpio](/index.php/Mkinitcpio_(Italiano) "Mkinitcpio (Italiano)") siano abilitati.

 `/etc/mkinitcpio.conf`  `HOOKS="base udev ... lvm2 filesystems"` 

Assicurarsi anche che sia abilitato il modulo `dm_mod`.

 `/etc/mkinitcpio.conf:`  `MODULES="dm_mod ..."` 

In caso siano state effettuate delle modifiche al file, sarà necessario [ricreare](/index.php/Mkinitcpio_(Italiano)#Creazione_dell'immagine_ed_attivazione "Mkinitcpio (Italiano)") l'initramfs, in modo da renderle effetive.

Può essere necessario aggiongere alle opzioni del kernel, `dolvm`. `root=` dovrebbe essere impostato sul volume logico, ad esempio `/dev/mapper/{vg-name}-{lv-name}`

## Configurazione

### Ingrandire un volume logico

Per ingrandire un volume logico prima sarà necessario ingrandire il volume logico e poi il filesystem per poter usare il nuovo spazio libero. Ipotizzando di avere un volume logico di 15GB con un filesystem ext3 e si vuole ingrandirlo a 20GB. Saranno necessario seguire i seguenti passaggi:

```
# lvextend -L 20G VolGroup00/lvolhome (oppure lvresize -L +5G VolGroup00/lvolhome)
# resize2fs /dev/VolGroup00/lvolhome

```

Sarà possibile usare `lvresize` invece di `lvextend`.

Se si vuole utilizzare tutto lo spazio libero in un gruppo di volumi, usare il seguente comando:

```
# lvextend -l +100%FREE VolGroup00/lvolhome

```

**Attenzione:** Non tutti i filesystem supportano l'ingrandimento senza perdite di dati e/o il ridimensionamento online.

**Nota:** Se non si ridimensiona il filesystem, si avrà un volume della solita dimensione precedente al ridimensionamento (il volume sarà più grande ma parzialmente inutilizzato).

### Ridurre un volume logico

Dato che probabilmente il filesystem sarà grande quanto il volume logico su cui risiede, sarà necessario prima ridurre il filesystem e dopo il volume logico. A seconda del filesystem utilizzato, potrebbe essere necessario effettuare l'umount prima. Ipotizzando di avere un volume logico di 15GB avente un filesystem ext3 e si desidera ridurlo a 10GB. Sarà necessario seguire i seguenti passaggi:

```
# resize2fs /dev/VolGroup00/lvolhome 9G
# lvreduce -L 10G VolGroup00/lvolhome (oppure lvresize -L -5G VolGroup00/lvolhome)
# resize2fs /dev/VolGroup00/lvolhome

```

In questo caso il filesystem viene ridotto in maniera maggiore di quanto viene ridotto il volume logico così non verrà accidentalmente tagliata fuori la fine del filesystem. Dopo sarà possibile espandere il filesystem fino a riempire lo spazio libero rimasto sul volume logico. Può essere utilizzato `lvresize` invece di `lvreduce`.

**Attenzione:**

*   Non ridurre la dimensione del filesystem fino ad essere minore del volume dei dati in esso contenuti altrimenti si rischia una perdita di dati.
*   Non tutti i filesystem supportano la riduzione senza perdita di dati e/o la riduzione online.

**Nota:** E' meglio ridurre il filesystem ad una dimensione minore rispetto al volume logico, così riducendo successivamente il volume logico, non verranno tagliati fuori alcuni dei dati alla fine del filesystem.

### Rimuovere volumi logici

**Attenzione:** Prima di rimuovere un volume logico, assicurarsi di trasferire altrove tutti i dati che si desidera mantenere, altrimenti andranno persi!

Prima, identificare il nome del volume logico che si desidera rimuovere. Si può ottenere una lista di tutti i volumi logici presenti nel sistema con:

 `# lvs` 

Poi, controllare il punto di mount per il volume logico scelto...:

 `$ df -h` 

... ed effettuare l'umount:

 `# umount /punto_di_mount` 

Infine, rimuovere il volume logico:

 `# lvremove /dev/yourVG/yourLV` 

Confermare premendo `y` e sarà rimosso.

Non dimenticare di aggiornare il file `/etc/fstab`!

Sarà possibile verificare la rimozione del volume logico utilizzando nuovamente come utente root il comando "lvs" (vedere il primo passaggio di questa sezione).

### Aggiungere un volume fisico ad un gruppo di volumi

Per prima cosa creare un volume fisico sulla periferica a blocchi che verrà utilizzata, successivamente estendere il gruppo di volumi:

```
# pvcreate /dev/sdb1
 # vgextend VolGroup00 /dev/sdb1
```

Questo aumenterà il numero totale di estensioni fisiche(Piscal Extens) del gruppo di volumi, che potranno essere allocate dai volumi logici.

**Nota:** E' considerata buona norma utilizzare il corretto codice partizione per la propria tavola delle partizioni: `8e` per il partizionamento MBR, e `8e00` per il partizionamento GPT.

### Rimuovere una partizione da un gruppo di volumi

Tutti i dati su questa partizione devono essere spostati su di una altra partizione. Fortunatamente, LVM rende questo più facile:

```
# pvmove /dev/sdb1

```

Se si desidera che i dati risiedano su di un determinato volume fisico, specificarlo come secondo argomento al comando `pvmove`:

```
# pvmove /dev/sdb1 /dev/sdf1

```

Poi il volume fisico che deve essere rimosso dal gruppo di volumi:

```
# vgreduce myVg /dev/sdb1

```

Oppure rimuovere tutti i volumi fisici vuoti:

```
# vgreduce --all vg0

```

Ed infine, se si desidera utilizzare le partizioni in altro modo, per evitare che LVM veda la partizione come un volume fisico:

```
# pvremove /dev/sdb1

```

### Snapshots

#### Introduzione

LVM permette di creare uno snapshot del sistema in maniera molto più efficiente dei tradizionali metodi di backup. Questa efficenza è data dall'utilizzo della policy COW (copy-no-write). Lo snapshot iniziale conterrà hard-link agli inode dei dati attuali. Fino a che i dati restano invariati, lo snapshot conterrà solo i link agli inode e non i dati stessi. Quando verrà modificato un file o una cartella ai quali lo snapshot punta, LVM automaticamente clonerà i dati, la vecchia copia referenziata dallo snapshot, e la nuova copia referenziata dall'attuale sistema. In questo modo, è possibile effettuare uno snapshot di un sistema di 35GB di dati usando solamente 2GB di spazio libero fino a che le modifiche effettuate saranno inferiori ai 2 GB (in entrambi l'originale e lo snapshot).

#### Configurazione

Creare uno volume logico snapshot come i normali volumi logici.

```
# lvcreate --size 100M --snapshot --name snap01 /dev/mapper/vg0-pv

```

Con questo volume, si potranno modificare meno di 100 M di dati, prima che il volume si riempa.

E’ importante inserire il modulo *dm-snapshot* nell’array MODULES nel file `/etc/mkinitcpio.conf`, altrimenti il sistema non si avvierà. Se si effettua la modifica ad un sistema già installato ricostruire l’immagine con il comando:

```
# mkinitcpio -g /boot/initramfs-linux.img

```

Todo: script per automatizzare lo snapshot della partizione di root prima degli aggiornamenti, per tornare allo stato precedente... aggiornare il file `menu.lst` per effettuare il boot dagli snapshot (articolo separato?)

gli snapshot sono principalmente usati per fornire una copia congelata del filesystem per effetuare i backup; un backup impiega due ore e fornisce un immagine più consistente del filesystem piuttosto che effettuare il backup diretto della partizione.

## Risoluzione di problemi

### I comandi LVM commands non funzionano

*   Caricare il modulo appropriato:

```
# modprobe dm_mod

```

*   Provare ad anteporre *lvm* ai comandi in questo modo:

```
# lvm pvdisplay

```

### Nela pagina Set Filesystem Mountpoints i volumi logici non sono mostrati

Se si sta installando un sistema dove è già presente un gruppo di volumi, potrebbe non essere accessibile anche dopo il comando "modprobe dm-mod" ed i volumi logici non vengono rilevati.

In questo caso, potrebbe essere necessario eseguire:

```
# vgscan

```

oppure:

```
# vgchange -ay <volgroup>

```

in modo da attivare il gruppo di volumi e rendere i volumi logici accessibili.

### LVM su periferiche rimovibili

Sintomi:

```
~$ sudo vgscan
 Reading all physical volumes.  This may take a while...
 /dev/backupdrive1/backup: read failed after 0 of 4096 at 319836585984: Input/output error
 /dev/backupdrive1/backup: read failed after 0 of 4096 at 319836643328: Input/output error
 /dev/backupdrive1/backup: read failed after 0 of 4096 at 0: Input/output error
 /dev/backupdrive1/backup: read failed after 0 of 4096 at 4096: Input/output error
 Found volume group "backupdrive1" using metadata type lvm2
 Found volume group "networkdrive" using metadata type lvm2

```

Cause:

	Rimuovendo un disco esterno con LVM senza disattivare il gruppo(i) di volumi prima. Prima di disconnettere, assicurarsi di:

```
# vgchange -an <volume group name>

```

Soluzione: (ipotizzando che sia già stato provato ad attivare il gruppo di volumi con il comando vgchange -ay <vg>, e siano stati restituiti degli errori di Input/output

```
# vgchange -an <volume group name>

```

	Scollegare il disco esterno ed aspettare alcuni minuti

```
# vgscan
# vgchange -ay <volume group name>

```

## Altre risorse

*   [LVM2 Resource Page](http://sourceware.org/lvm2/) su SourceWare.org
*   [LVM HOWTO](http://tldp.org/HOWTO/LVM-HOWTO/) articolo del Linux Documentation Project
*   [LVM](http://wiki.gentoo.org/wiki/LVM) articolo del Wiki di Gentoo
*   [Mirrors vs. MD Raid 1](http://www.joshbryan.com/blog/2008/01/02/lvm2-mirrors-vs-md-raid-1LVM2) post by Josh Bryan