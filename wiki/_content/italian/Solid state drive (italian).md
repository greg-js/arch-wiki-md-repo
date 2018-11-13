**Attenzione:** Questa pagina è in fase di revisione e potrebbe non essere aggiornata. Seguite per ora le istruzioni della versione inglese.

Articoli correlati

*   [SSD Benchmarking](/index.php/SSD_Benchmarking "SSD Benchmarking")
*   [SSD Memory Cell Clearing](/index.php/SSD_Memory_Cell_Clearing "SSD Memory Cell Clearing")

Questo articolo copre molti aspetti degli SSD (drive a stato solido) in relazione a Linux ; comunque, i principi di base e gli insegnamenti chiave presentati sono abbastanza generali per essere applicati anche agli utenti che utilizzano SSD con altri sistemi operativi come la famiglia dei prodotti Windows o quelli MacOS X. A parte le informazioni appena menzionate gli utenti Linux potranno beneficiare delle ottimizzazioni qui presentate.

## Contents

*   [1 Introduzione](#Introduzione)
    *   [1.1 Vantaggi rispetto agli Hard Disk](#Vantaggi_rispetto_agli_Hard_Disk)
    *   [1.2 Limitazioni](#Limitazioni)
*   [2 Consigli per l'acquisto](#Consigli_per_l'acquisto)
    *   [2.1 Caratteristiche chiave](#Caratteristiche_chiave)
    *   [2.2 Approfondimenti](#Approfondimenti)
*   [3 Consigli per massimizzare le prestazioni degli SSD](#Consigli_per_massimizzare_le_prestazioni_degli_SSD)
    *   [3.1 Allineamento della partizione](#Allineamento_della_partizione)
        *   [3.1.1 Descrizione ad alto livello](#Descrizione_ad_alto_livello)
    *   [3.2 Usare GPT - METODO RACCOMANDATO](#Usare_GPT_-_METODO_RACCOMANDATO)
        *   [3.2.1 Esempio di Utilizzo Dettagliato](#Esempio_di_Utilizzo_Dettagliato)
        *   [3.2.2 Usare MBR - METODO DEPRECATO - L'utilizzo di GPT è Raccomandato](#Usare_MBR_-_METODO_DEPRECATO_-_L'utilizzo_di_GPT_è_Raccomandato)
            *   [3.2.2.1 Schema di Utilizzo di Fdisk](#Schema_di_Utilizzo_di_Fdisk)
                *   [3.2.2.1.1 Esempio di Utilizzo Dettagliato](#Esempio_di_Utilizzo_Dettagliato_2)
                *   [3.2.2.1.2 Considerazioni Speciali per Partizioni Logiche](#Considerazioni_Speciali_per_Partizioni_Logiche)
                *   [3.2.2.1.3 Considerazioni Speciali per RAID0 con SSD Multipli](#Considerazioni_Speciali_per_RAID0_con_SSD_Multipli)
    *   [3.3 Partizioni cifrate](#Partizioni_cifrate)
    *   [3.4 Opzioni di Mount](#Opzioni_di_Mount)
        *   [3.4.1 Considerazioni speciali per computer Mac](#Considerazioni_speciali_per_computer_Mac)
    *   [3.5 Scheduler I/O](#Scheduler_I/O)
        *   [3.5.1 Usare il filesystem virtuale sys](#Usare_il_filesystem_virtuale_sys)
        *   [3.5.2 Parametro del Kernel](#Parametro_del_Kernel)
    *   [3.6 Spazio di Swap su SSD](#Spazio_di_Swap_su_SSD)
    *   [3.7 Pulizia delle Celle di Memoria degli SSD](#Pulizia_delle_Celle_di_Memoria_degli_SSD)
*   [4 Consigli per Minimizzare Letture/Scritture su SSD](#Consigli_per_Minimizzare_Letture/Scritture_su_SSD)
    *   [4.1 Schema di Partizionamento Intelligente](#Schema_di_Partizionamento_Intelligente)
    *   [4.2 L'Opzione di Mount noatime](#L'Opzione_di_Mount_noatime)
    *   [4.3 Posizionare /tmp in RAM](#Posizionare_/tmp_in_RAM)
    *   [4.4 Posizionare i Profili del Browser in RAM](#Posizionare_i_Profili_del_Browser_in_RAM)
    *   [4.5 Compilare in /dev/shm](#Compilare_in_/dev/shm)
    *   [4.6 Disabilitare il Journaling sul Filesystem?](#Disabilitare_il_Journaling_sul_Filesystem?)
    *   [4.7 Scelta del Filesystem](#Scelta_del_Filesystem)
        *   [4.7.1 Btrfs](#Btrfs)
        *   [4.7.2 Ext4](#Ext4)
*   [5 Misurare le Prestazioni degli SSD](#Misurare_le_Prestazioni_degli_SSD)
*   [6 Aggiornamenti del Firmware](#Aggiornamenti_del_Firmware)
    *   [6.1 OCZ](#OCZ)

## Introduzione

I Drive a Stato Solido non sono componenti Plug&Play. Sono necessari accorgimenti particolari come l'allineamento delle partizioni, la scelta del file system, il supporto a TRIM, etc. per impostare gli SSD per le prestazioni ottimali. Questo articolo tenta di spiegare i passaggi chiave per permettere agli utenti di ottenere il massimo dai propri SSD sotto Linux. Gli utenti sono incoraggiati a leggere questo articolo per intero prima di mettere in pratica le impostazioni dal momento che il contenuto è organizzato per argomento e non segue necessariamente un ordine sistematico o cronologico.

**Note:** Questo articolo è orientato verso gli utenti Linux, ma la maggior parte del suo contenuto è sensibile anche per i nostri amici che utilizzano Windows o Mac OS X.

### Vantaggi rispetto agli Hard Disk

*   Velocità di lettura maggiore - 2 - 3 volte più veloce di un HDD desktop attuale (7,200 RPM con interfaccia SATA2).
*   Velocità di lettura costante - Nessun decremento di velocità in lettura su tutta l'interezza del drive. Le prestazioni degli HDD tendono a diminuire con il movimento della testina dalle parti più esterne a quelle più interne dei dischi
*   Tempo di accesso minimo - Circa 100 volte più veloce di un HDD. Per esempio, 0.1 ms (100 ns) contro 12-20 ms (12,000-20,000 ns) per HDD desktop.
*   Alto grado di affidabilità.
*   Nessuna parte in movimento.
*   Produzione di calore minima.
*   Consumo di corrent elettrica minimo - Frazioni di un Watt in condizione di riposo e 1-2 Watt in lettura/scrittura contro 10-30 Watt for un HDD a seconda delle rotazioni RPM.
*   Leggerezza - ideale per i computer portatili.

### Limitazioni

*   Costo per capacità (dollari per GB, contro spiccioli per GB per HDD classici).
*   Capacità dei modelli in commercio inferiore rispetto agli HDD classici.
*   Celle di memoria grandi richiedono diverse ottimizzazioni dei file system rispetto ai driver rotatori. L'accesso alla flash di basso livello che potrebbe essere usato dai moderni sistemi operativi per ottimizzarne l'accesso è nascosto da un livello di traslazione flash.
*   Partizioni e filesystem necessitano di ottimizzazioni specifiche. La dimensione della pagina e la dimensione della pagina di eliminazione non sono riconosciute automaticamente.
*   Le celle sono sottoposte a usura.Le celle per uso consumer MLC prodotte con processo a 50nm possono gestire ciascuna 10000 scritture, quelle a 35nm generalmente gestiscono 5000 scritture e quelle a 25nm circa 3000 (processi di produzione più piccoli significano maggiore densità e minor prezzo). Se le scritture sono correttamente organizzate, non sono troppo piccole, e sono allineate con le celle, questo si traduce in volume di scritture totali supportato per gli SSD multiplo della propria capacità. Volumi di scritture quotidiani devono essere bilanciati in relazione all'aspettativa di durata.
*   I firmware e i controllori sono complessi. Occasionalmente possono avere dei bug. Quelli più moderni consumano una quantità di energia paragonabile agli HDD classici. Essi [implementano](https://lwn.net/Articles/353411/) l'equivalente di un file system strutturato su log con una gestione dello spazio non più utilizzato. Essi traducono i tradizionali comandi SATA pensati per driver rotatori. Alcuni di essi sono capaci di effettuare la compressione in tempo reale. Gestiscono scritture ripetute su l'intera superficie della flash, per prevenire l'usura prematura delle celle. Sono anche in grado di unire più scritture insieme in modo che piccole scritture non diano luogo a lunghi cicli di cancellazioni su celle grandi. Infine hanno la capacità di spostare le celle che contengono dati in modo da prevenirne la perdita nel tempo.
*   Le prestazioni possono degradare con lo spazio occupato. La gestione dello spazio non più utilizzato non è universalmente ben implementata e lo spazio libero non sempre è organizzato su celle interamente vuote

## Consigli per l'acquisto

Ci sono alcune caratteristiche chiave da considerare prima di procedere all'acquisto di un SSD attuale.

### Caratteristiche chiave

*   Il supporto nativo al [TRIM](https://en.wikipedia.org/wiki/TRIM "wikipedia:TRIM") è una caratteristica fondamentale sia per prolungare la vita degli SSD sia per ridurre la perdita di prestazioni in scrittura nel tempo.
*   Comprare SSD della giusta dimensione è fondamentale. Con qualsiasi filesystem, l'occupazione massima di ogni partizione non deve superare il 75% per garantirne un uso efficiente da parte del kernel.

### Approfondimenti

Questa sezione non intende essere omni comprensiva ma comprende alcune analisi importanti

*   [SSD Anthology (history lesson, a bit dated)](http://www.anandtech.com/show/2738)
*   [SSD Relapse (refresher and more up to date](http://www.anandtech.com/show/2829))
*   [One user's recommendations](http://forums.anandtech.com/showthread.php?t=2069761)
*   [Enabling and testing TIM in linux](http://techgage.com/article/enabling_and_testing_ssd_trim_support_under_linux/)

## Consigli per massimizzare le prestazioni degli SSD

### Allineamento della partizione

##### Descrizione ad alto livello

**Un corretto allineamento della partizione è essenziale per prestazione ottimali e longevità.** La chiave per l'allineamento è partizionare almeno alla dimensione dell' EBS (erase block size) del SSD.

**Note:** L'EBS è per lo più dipendente dal costruttore; una ricerca su Google sul modello di interesse potrebbe essere un'ottima idea! L'Intel X25-M per esempio si presuppone avere un EBS di 512 KiB, ma Intel non ha ancora pubblicato niente di ufficiale a riguardo.

**Note:** Se non si conosce l'EBS del proprio SSD, è comunque possibile usare una dimensione di 512 KiB (o 1024 KiB se si vuole essere sicuri e non ci si preoccupa di perdere il primo MiB del proprio disco). Queste dimensioni sono maggiori o uguali di tutti i correnti EBS. Allineare le partizioni per l'EBS produrrà partizioni allineate anche per dimensioni più piccole. Windows 7 e Ubuntu utilizzano questo stratagemma per ottimizzare le partizioni per lavorare con gli SSD.

Se le partizioni non sono allineate per iniziare ad un multiplo dell'EBS (per esempio 512 KiB), l'allineamento del file system è soltanto un esercizio senza senso in quanto l'intero allineamento è rovinato dallo scarto iniziale della partizione. Generalmente, i dischi fissi sono indirizzati tramite *cilindri*, *testine* e *settori* nei quali i dati vengono letti e scritti. Questi rappresentano rispettivamente la posizione radiale, la testina del disco (piatto e lato) e la posizione assiale dei dati. Con l' LBA (logical block addressing), questo non è più vero. L'intero disco fisso è indirizzato come un flusso continuo di dati.

### Usare GPT - METODO RACCOMANDATO

[GPT](/index.php/GPT "GPT") è uno stile di partizionamento alternativo e attuale. Il tool compatibile con GPT equivalente a fdisk, gdisk, è in grado di allineare automaticamente le partizioni su un blocco base di dimensioni di 2048 settori (o 1024KiB) compatibile con la gran parte degli SSD se non tutti. Anche GNU parted supporta GPT, ma è [meno intuitivo](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=601813) per allineare le partizioni.

Schema di Utilizzo di Gdisk:

*   Installare gdisk dal repository extra.
*   Avviare gdisk passando come argomento proprio SSD
*   Se l' SSD è nuovo o si vuole reinizializzare, creare una nuova tabella delle partizioni GUID (GPT) con il comando 'o'.
*   Creare una nuova partizione con il comando 'n' (primary type/1st partition).
*   Assumendo che la partizione è nuova, gdisk utilizzerà l'allineamento più alto possibile. Altrimenti sceglierà la più grande potenza di due che divide tutti gli scarti delle partizioni.
*   Se si sceglie di iniziare su un settore precedente al 2048esimo gdisk sposterà automaticamente l'inizio della partizione al 2048esimo settore. Questo per assicurarsi un allineamento su 2048 settori (dal momento che un settore è 512B, questo è un allineamento di 1024 KiB che dovrebbe contemplare ogni possibile ESB degli SSD).
*   Usare il formato +x{M,G} per estendere la partizione di x megabyte o gigabyte. Se si sceglie una dimensione che non è un multiplo della dimensione di allineamento (1024kiB) gdisk adatterà la partizione al più vicino e piccolo multiplo.
*   Selezionare il tipo della partizione, il default 'Linux/Windows data' (code 0700) dovrebbe andar bene per la maggior parte degli utilizzi. Premere L per vedere una lista dei tipi disponibili.
*   Creare altre partizione seguendo lo stesso procedimento.
*   Scrivere la tabella delle partizioni sul disco e uscire con il comando 'w'.
*   Creare i filesystem normalmente.

**Warning:** Se si ha in programma di utilizzare il disco come disco di boot su un sistema basato sul BIOS (la maggior parte dei sistemi ad eccezione dei computer APPLE e di alcuni rari modelli di schede madri con chipset INTEL) è necessario creare, possibilmente all'inizio del disco, una partizione di 1MiB di tipo BIOS boot partition (code ef02). Questo è necessario per l'utilizzo di [GRUB2](/index.php/GRUB2_(Italiano) "GRUB2 (Italiano)"), mentre per [Syslinux](/index.php/Syslinux "Syslinux") è sufficiente preparare una partizione di /boot distinta. Vedere [GPT](/index.php/GPT "GPT") per maggiori informazioni.

**Warning:** GRUB legacy non supporta lo schema di partizionamento GUID, si deve usare [burg](/index.php/Burg_(Italiano) "Burg (Italiano)"), [GRUB2](/index.php/GRUB2_(Italiano) "GRUB2 (Italiano)") or [Syslinux](/index.php/Syslinux "Syslinux").

**Warning:** Se si ha intenzione di avere un dual boot con Windows (XP, Vista or 7) non usare GPT dal momento che non supportano il boot da dischi GPT! E' necessario usare il metodo deprecato del MBR descritto successivamente. Questa limitazione non si applica se si utilizza un sistema EFI e Windows Vista (64bits) o Seven (sia 32 che 64bits).

#### Esempio di Utilizzo Dettagliato

**Note:** La seguente sezione ha lo scopo di illustrare il processo di partizionamento di un Crucial C300 Real SSD con una singola partizione: 10GiB, partizione Linux. Anche se si dovrebbe applicare ad ogni SSD, adattare al proprio schema di partizionamento. Ancora, non dimenticare di aggiungere una partizione di 1MiB di tipo BIOS boot come prima partizione se necessario.

Installare gdisk:

```
# pacman -S gptfdisk

```

Eseguire gdisk sul proprio SSD assunto essere /dev/sda:

```
[root@archlinux ~]# gdisk /dev/sda
GPT fdisk (gdisk) version 0.6.13

Partition table scan:
  MBR: not present
  BSD: not present
  APM: not present
  GPT: not present

Creating new GPT entries.

```

Creare una nuova tabella di partizioni GUID:

```
Command (? for help): o
This option deletes all partitions and creates a new protective MBR.
Proceed? (Y/N): y
```

Creare le partizioni:

```
Command (? for help): n
Partition number (1-128, default 1): #pressed enter to accept default#
First sector (34-125045424, default = 34) or {+-}size{KMGTP}: #pressed enter to accept default#
Information: Moved requested sector from 34 to 2048 in
order to align on 2048-sector boundaries.
Use 'l' on the experts' menu to adjust alignment
Last sector (2048-125045424, default = 125045424) or {+-}size{KMGTP}: +10G  
Current type is 'Linux/Windows data'
Hex code or GUID (L to show codes, Enter = 0700): #pressed enter to accept default#
Changed type of partition to 'Linux/Windows data'

```

Risultato:

```
Command (? for help): p
Disk /dev/sda: 125045424 sectors, 59.6 GiB
Logical sector size: 512 bytes
Disk identifier (GUID): A89B4292-8ED7-40CB-BD45-58A160E090EE
Partition table holds up to 128 entries
First usable sector is 34, last usable sector is 125045390
Partitions will be aligned on 2048-sector boundaries
Total free space is 2014 sectors (1007.0 KiB)

Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048        20973567   10.0 GiB    0700  Linux/Windows data
```

Scrivere la tabella delle partizioni ed uscire:

```
ommand (? for help): w

Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING
PARTITIONS!!

Do you want to proceed, possibly destroying your data? (Y/N): y
OK; writing new GUID partition table (GPT).
Warning: The kernel is still using the old partition table.
The new table will be used at the next reboot.
The operation has completed successfully.
[root@archlinux ~]#
```
Adesso è possibile creare il file system seguendo la maniera usuale: `# mkfs.ext4 /dev/sda1` 

#### Usare MBR - METODO DEPRECATO - L'utilizzo di GPT è Raccomandato

L'utilità di sistema Linux fdisk, comunque, continua ad utilizzare il sistema C-H-S dove gli utenti possono definire un qualsiasi numero di testine e settori (i cilindri sono calcolati automaticamente in base alla capacità del dispositivo), con partizioni che iniziano e finiscono sempre allo stesso intervallo di testine e cilindri. **Quindi, è necessario scegliere un numero di testine e settori sottomultipli della dimensione dell' EBS del SSD.** Questo viene ottenuto impostando il numero delle testine (o tracce per cilindro) e i settori (per traccia) in modo da coincidere con l'EBS.

Ted Tso raccomanda di utilizzare un impostazione di [224*56](http://ldn.linuxfoundation.org/blog-entry/aligning-filesystems-ssd%E2%80%99s-erase-block-size) (=2^8*49) ottenendo un allineamento di (2^8*512=) 128 KiB:

```
# fdisk -H 224 -S 56 /dev/sdX

```

Mentre altri raccomandano di utilizzare un impostazione di [32*32](http://www.nuclex.org/blog/personal/80-aligning-an-ssd-on-linux) ottenendo un allineamento di (2^10*512=) 512 KiB:

```
# fdisk -H 32 -S 32 /dev/sdX

```

Come funzionano questi calcoli? Il numero per l'allineamento è la più grande potenza di due che divide le posizioni del cilindro di confine sul disco. La dimensione in byte dei cilindri è H*S*512 = (traccie per cilindro) * (settori per traccia) * (dimensione dei settori). Fattorializzare H, S e la dimensione dei settori (512=2^9) in fattori primi e prendere tutti i 2s. Nel primo caso descritto è necessario ignorare il fattore che non è potenza di due, 7^2=49.

**Note:** Per motivi di compatibilità MS-DOS, una partizione che inizi dal primo cilindro non deve conto di un traccia, riducendo il suo allineamento a livello della traccia (4k per -S 56 e 16k per -S 32). Il modo più semplice per allineare la prima partizione è farla iniziare al cilindro 2 piuttosto che al cilindro 1 come di default come visto nell'esempio precedente.

##### Schema di Utilizzo di Fdisk

*   Avviare fdisk usando i valori corretti per H e S specifici per il proprio SSD come descritto precedentemente.
*   Se l'SSD è nuovo, creare una nuova partizione vuota DOS con il comando 'o'.
*   Creare una nuova partizione con il comando 'n'(primary type/1st partition).
*   Iniziare dal settore 2 invece che dal settore 1 per assicurare compatibilità con MS-DOS se questa è richiesta, altrimenti accettare il valore di default.
*   Usare il formato +xG per estendere la partizione di x gigabyte.
*   Cambiare l'id del tipo di partizione dal valore di default Linux (type 83) al tipo desiderato tramite il comando 't'. Questo è un passaggio opzionale per gli utenti che vogliano creare un altro tipo di partizione come ad esemepio swap, NTFS, ecc. Una lista complete delle alternative disponibili è disponibile tramite il comando 'l'.
*   Creare altre partizione seguendo lo stesso procedimento.
*   Scrivere la tabella delle partizioni sul disco e uscire con il comando 'w'.

Quando finito, gli utenti possono formattare le loro nuove partizioni con 'mkfs.x /dev/sdXN' dove x è il tipo di filesystem, X e la lettera del drive e N e il numero della partizione. Il seguente esempio formatta la prima partizione del primo disco in ext4 utilizzando le opzioni di default definite in `/etc/mke2fs.conf`:

```
# mkfs.ext4 /dev/sda1

```

**Warning:** L'utilizzo del comando mkfs può essere pericoloso dal momento che un semplice errore può causare la formattazione della partizione SBAGLIATA e la perdita di dati. Controllare TRE volte la partizione scelta prima di premere il tasto Enter!

###### Esempio di Utilizzo Dettagliato

**Note:** La seguente sezione ha lo scopo di illustrare il processo di partizionamento di un SSD Intel X25-M con una singola partizione Linux da 12 GiB. Non è in nessun modo il metodo definitivo per farlo nè gli switch utilizzati per avviare fdisk in questo specifico esempio hanno necessariamente i valori corretti per altri modelli e marche di SSD!

```
# fdisk -H 32 -S 32 /dev/sdb

The number of cylinders for this disk is set to 15711.
There is nothing wrong with that, but this is larger than 1024,
and could in certain setups cause problems with:
1) software that runs at boot time (e.g., old versions of LILO)
2) booting and partitioning software from other OSs
   (e.g., DOS FDISK, OS/2 FDISK)

Command (m for help): o
Building a new DOS disklabel with disk identifier 0x8cb3d286.
Changes will remain in memory only, until you decide to write them.
After that, of course, the previous content won't be recoverable.

The number of cylinders for this disk is set to 15711.
There is nothing wrong with that, but this is larger than 1024,
and could in certain setups cause problems with:
1) software that runs at boot time (e.g., old versions of LILO)
2) booting and partitioning software from other OSs
   (e.g., DOS FDISK, OS/2 FDISK)
Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

Command (m for help): n
Command action
   e   extended
   p   primary partition (1-4)
p
Partition number (1-4): 1
First cylinder (1-15711, default 1): 2
Last cylinder, +cylinders or +size{K,M,G} (2-15711, default 15711): +12G

Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks.
```

Il resto dell'SSD è stato partizionato in maniera simile utilizzando in totale due partizioni. Ecco come si presenta l'output del comando list di fdisk:

```
# fdisk -l /dev/sdb

Disk /dev/sdb: 80.0 GB, 80026361856 bytes
32 heads, 32 sectors/track, 152638 cylinders
Units = cylinders of 1024 * 512 = 524288 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x76b978dc

   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1               2       24578    12583424   83  Linux
/dev/sdb2           24579      152638    65566720   83  Linux
```

E del comando di fdisk -lu:

```
# fdisk -lu /dev/sdb

Disk /dev/sdb: 80.0 GB, 80026361856 bytes
32 heads, 32 sectors/track, 152638 cylinders, total 156301488 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x76b978dc

   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1            1024    25167871    12583424   83  Linux
/dev/sdb2        25167872   156301311    65566720   83  Linux
```

**Warning:** Prestare attenzione all'ultimo step per testare lo stato di salute. Se le testine e i settori/traccia non rimangono 32/32, questo è dovuto o ad un bug in fdisk o a una ragione sconosciuta. Vedere la pagine del wiki [using cfdisk/post process observation](/index.php/SSD_memory_cell_clearing#Post_Process_Observation "SSD memory cell clearing") per una soluzione.

###### Considerazioni Speciali per Partizioni Logiche

---Segnaposto per contenuti.

###### Considerazioni Speciali per RAID0 con SSD Multipli

---Segnaposto per contenuti.

### Partizioni cifrate

Se si utilizza cryptsetup, definire un payload sufficiente([vedere qui](http://www.spinics.net/lists/dm-crypt/msg02421.html)):

```
cryptsetup luksFormat --align-payload=8192 ...

```

Ma ricordarsi che la funzionalità DISCARD/TRIM non è supportata da device-mapper (anche se è in lavorazione [vedere qui](http://news.gmane.org/find-root.php?group=gmane.linux.kernel.device-mapper.dm-crypt&article=4075))

### Opzioni di Mount

Ci sono alcune opzioni chiave di mount da usare per le partizioni su SSD in `/etc/fstab`.

*   **noatime** - Accessi in lettura al filesystem non causeranno più un aggiornamento alle informzioni di atime associate al file. L'importanza dell'impostazione noatime consiste nell'eliminazione della necessità del sistema di effettuare accessi in scrittura al filesystem anche per la lettura di file. Dal momento che le scritture sono costose come descritto nella precedente sezione, in questo modo è possibile avere un discreto aumento di prestazioni. Notare che nonostante questa opzione il tempo dell'ultima modifica di un file continua ad essere aggiornato.
*   **discard** - L'opzione discard abilita i benefici del comando TRIM purchè si utilizzi una versione del kernel >=2.6.33\. Questa impostazione non funzione con ext3, l'utilizzo dell'opzione discard con una partizione di root con filesystem ext3 ne determinerà l'accesso in sola lettura.

```
/dev/sda1 / ext4 defaults,noatime,discard 0 1
/dev/sda2 /home ext4 defaults,noatime,discard 0 1

```

**Note:** E' possibile impostare l'opzione discard anche con tune2fs: tune2fs -o discard /dev/sda1.

**Warning:** E' fondamentale che gli utenti impostino il controller che pilota l'SSD in AHCI mode (no in IDE mode) per assicurarsi che il kernel sia in grado di utilizzare il comando TRIM.

**Warning:** Gli utenti di devono assicurare di utilizzare una versione del kernel maggiore o uguale alla 2.6.33 e che il proprio SSD supporti il comando TRIM prima di provare a montare una partizione con l'opzione discard. Altrimenti sono possibili perdite di dati!.

**Warning:** Con l'utilizzo di un SSD OCZ Vertex II (che supporta TRIM) e il kernel 2.6.37.4 alcuni utenti su Arch hanno avuto problemi con l'opzione **discad**: tutti le modifiche fatte al filesystem sono scomparse dopo un riavvio. Secondo [questo](http://www.mjmwired.net/kernel/Documentation/filesystems/ext4.txt#356), l'opzione **discard** è disattivata di default perchè non sufficientemente stabile.

#### Considerazioni speciali per computer Mac

Per default, il firmware APPLE imposta la modalità SATA in IDE mode (piuttosto che in AHCI) all'avvio di ogni sistema operativo ad eccezione di Mac OS. E' comunque semplice ritornare nella modalità AHCI se si utilizza un controller SATA Intel e [GRUB2](/index.php/GRUB2_(Italiano) "GRUB2 (Italiano)").

Per prima cosa determinare l'identificativo PCI del proprio controller SATA. Eseguire il comando:

```
# lspci -nn

```

e trovare la linea che indica "SATA AHCI Controller". L'identificativo PCI è fra parentesi quadre e dovrebbe apparire come 8086:27c4 (anche se le ultime cifre potrebbero differire).

Adesso modificare /boot/grub/grub.cfg aggiungendo la linea

```
# setpci -d 8086:27c4 90.b=40

```

immediatamente prima la linea "set root" di ogni sistema operativo per il quale si vuole abilitare la modalita AHCI. Assicurarsi di sostituire con l'identificativo PCI appropriato.

(fonte: [http://darkfader.blogspot.com/2010/04/windows-on-intel-mac-and-ahci-mode.html](http://darkfader.blogspot.com/2010/04/windows-on-intel-mac-and-ahci-mode.html))

### Scheduler I/O

**Note:** Questa configurazione non dovrebbe essere necessaria dal momento che lo scheduler cfq controlla se il drive non è rotazionale e si comporta in maniera corretta per gli SSD.

Considerare di passare dallo scheduler di default, che in Arch è cfs (completely fair queuing), a scheduler noop o deadline per un SSD. Con l'utilizzo dello scheduler noop, per esempio, le richieste vengono processate semplicemente in ordine di arrivo, senza nessuna considerazione su dove i dati risiedono fisicamente sul disco. Questa opzione è pensata per essere vantaggiosa per gli SSD dal momento che il tempo di accesso è identico per tutti i settori dell'SSD.

Comunque, per alcuni SSD, in particolare i primi basati su JMicron, ci potrebbero essere prestazioni migliori con lo scheduler di default (vedere [qui](http://www.alphatek.info/2009/02/02/io-scheduler-and-ssd-part-2/) per una situazione del genere); per questi, nonostante i tempi di accesso siano simili per tutti i settori, il carico per gli accessi casuali è sufficientemente grande da superare qualsiasi vantaggio. Se il proprio SSD è stato costruito nell'ultimo anno o è stato costruito da Intel, questo probabilmente non è il vostro caso.

Per maggior informazioni sugli scheduler vedere [questo](http://www.linux-mag.com/id/7564/1) articolo del Linux Magazine (è necessaria la registrazione).

Per informazione sullo scheduler di default con gli SSS: [https://bugs.archlinux.org/task/22605](https://bugs.archlinux.org/task/22605)

Su Arch lo scheduler cfq è abilitato di default. E possibile verificarlo osservando il contenuto di /sys/block/sda/queue/scheduler:

```
$ cat /sys/block/sdX/queue/scheduler
noop deadline [cfq]

```

Lo scheduler attualmente utilizzato è indicato fra parentesi quadre.

Ci sono diverse possibilità per cambiare il tipo di scheduler.

**Note:** Cambiare il tipo di scheduler soltanto per gli SSD. Mantener lo scheduler cfq per tutti gli altri HDD fisici è *altamente* consigliato.

##### Usare il filesystem virtuale sys

Questo metodo è da preferirsi quando il sistema system ha diverse periferiche di memorizzazione (ad esempio un SSD e un HDD) Aggiungere la seguente linea in `/etc/rc.local`:

```
echo noop > /sys/block/sdX/queue/scheduler

```

Dove X è la lettera del SSD.

##### Parametro del Kernel

Se l'unica periferica di memorizzazione nel sistema è un SSD, valutare di impostare lo scheduler di I/O per l'intero sistema tramite il parametro del kernel elevator:

```
elevator=noop

```

Per esempio, con GRUB, in `/boot/grub/menu.lst`:

```
kernel /vmlinuz26 root=/dev/sda3 ro elevator=noop

```

o con GRUB2, in `/etc/default/grub`: (ricordarsi di eseguire update-grub successivamente)

```
GRUB_CMDLINE_LINUX="elevator=noop"

```

### Spazio di Swap su SSD

E' possibile posizionare la partizione di swap su un SSD. Considerare comunque che i sistemi desktop moderni che hanno generalmente piu di 2 GiB di memoria raramente utilizzando lo spazio di swap. L'eccezione degna di nota sono i sistemi che utilizzano la funzionalità di ibernazione. Il seguente è l'impostazione consigliata per una partizione di Swap su SSD che riduce lo "swapiness" del sistema in modo da evitare le scritture in swap.

```
# echo 1 > /proc/sys/vm/swappiness

```

O più semplicemente modificare `/etc/sysctl.d/99-sysctl.conf` come indicato nell'articolo del wiki [Maximizing Performance](/index.php/Improving_performance#Swappiness "Improving performance").

```
vm.swappiness=1
vm.vfs_cache_pressure=50

```

### Pulizia delle Celle di Memoria degli SSD

In alcune occasioni, si potrebbe volere resettare completamente le celle di un SSD allo stesso stato iniziale che avevano al momento dell'installazione per ripristinarle alle loro [prestazioni di fabbrica in scrittura](http://www.anandtech.com/storage/showdoc.aspx?i=3531&p=8). Le prestazioni in scrittura tendono a degradare con l'andare del tempo anche su SSD con supporto TRIM. Il TRIM si limita a salvaguardare contro la cancellazione dei file, non contro le sostituzioni come nel caso di un salvataggio incrementale.

La prcoedura di reset è facilmente realizzabile in tree passi indicati sull'articolo del wiki [SSD memory cell clearing](/index.php/SSD_memory_cell_clearing "SSD memory cell clearing").

## Consigli per Minimizzare Letture/Scritture su SSD

Uno schema di utilizzo per gli SSD dovrebbe basarsi sulla 'semplicità' di posizionare le operazioni che richiedono numerose letture e scritture in RAM (Random Access Memory) o su un HDD fisico piuttosto che sul SSD. Così facendo si aumenta la longevità del SSD. Questo è principalmente dovuto ad un erase block size grande (512 KiB in alcuni casi); molte piccole scritture causano un numero gigante di effettive scritture.

**Note:** Un SSD da 32GB con un fattore di amplificazione di scrittura di 10x, un ciclo standard di 10000 scritture/cancellazioni, e **10GB di dati scritti al giorno**, darebbero **un aspettativa di vita di 8 anni**. La situazione migliora con SSD più grandi e controller moderni con fattori di amplificazione di scrittura minori.

Usare "iotop -oPa" e ordinare in base alle scritture su disco per vedere quanto i programmi stanno scrivendo su disco.

### Schema di Partizionamento Intelligente

Valutare di spostare la partizione dove risiede /var su un disco fisico del sistema piuttosto che sul SSD per prevenire l'usura a causa di letture e scritture. La maggior parte degli utenti può tenere soltanto / e /home sul SSD (anche /boot) posizionando /var e /tmp su un HDD fisico.

```
# SSD
/
/home

# HDD
/boot
/var
/media/data (and other extra partitions, etc.)
```

Se l'SSD è l'unica periferica di memorizzazione presente sul sistema (nessun HDD), valutare di preparare una partizione dedicata per /var in modo da permettere un miglior recupero del sistema, per esempio nel caso che un programma difettoso utilizzi tutto lo spazio presente su / o che tutto lo spazio venga occupato dai log.

Un'altra possibilità intelligente è quella di posizionare /tmp in RAM se il sistema ha sufficiente memoria. Vedere la prossima sezione per questa opzione.

### L'Opzione di Mount noatime

Assegnare l'opzione **noatime** alle partizioni che risiedono su SSD. Vedere la sezione [Opzioni di Mount](#Mount_Flags) più avanti per maggiori informazioni.

### Posizionare /tmp in RAM

Per sistemi con almeno 2 giga di memoria, posizionare /tmp in RAM è consigliato e anche facilmente realizzabile cancellando il contenuto della partizione fisica per /tmp e successivamente montarla su tmpfs (RAM) in `/etc/fstab`. La seguente linea ne è un esempio:

```
none	/tmp	tmpfs	nodev,nosuid,noatime,size=1000M,mode=1777	0	0

```

### Posizionare i Profili del Browser in RAM

E' possibile montare facilmente i profili dei browser come firefox, chromium, ecc. in RAM attraverso tmpfs e usare rsync per tenerli sincronizzati con i backup presenti su HDD. Per maggiori informazioni su questa procedura, vedere l'articolo [Velocizzare Firefox Usando tmpfs](/index.php/Speed-up_Firefox_using_tmpfs "Speed-up Firefox using tmpfs"). Oltre all'ovvio incremento di velocità, in questo modo, sarà anche possibile prevenire cicli di lettura e scrittura sul proprio SSD.

### Compilare in /dev/shm

Compilare intenzionalmente in /dev/shm è un'ottima idea per minimizzare questo problema. Per sistemi con almeno 4 Giga di memoria, la linea relativa a shm presente in `/etc/fstab` può essere modificata in modo da usare più della metà della memoria fisica disponibile grazie all'utilizzo dell'opzione size.

Esempio di una macchina con 8 GiB di memoria fisica:

```
shm                    /dev/shm      tmpfs     nodev,nosuid,size=6G        0      0

```

### Disabilitare il Journaling sul Filesystem?

L'utilizzo di un filesystem con journaling come ext3 o ext4 su un SSD SENZA il journal è un opzione per diminuire letture/scritture. L'ovvia controindicazione dell'utilizzo di un filesystem con il journaling disabilitato è una perdita di dati in caso di un dismount problematico (ad esempio un'interruzione di alimentazione, blocco del kernel, ecc.). Con i moderni SSD [Ted Tso](http://thunk.org/tytso/blog/2009/03/01/ssds-journaling-and-noatimerelatime) argomenta che il journaling può essere abilitato con il minimo di numero di letture/scritture supplementare nella maggior parte delle circostanze:

**Quantità di dati scritti (in megabyte) su un file system ext4 montato con l'opzione noatime.**

| operazione | con journal | senza journal | differenza percentuale |
| git clone | 367.0 | 353.0 | 3.81 % |
| make | 207.6 | 199.4 | 3.95 % |
| make clean | 6.45 | 3.73 | 42.17 % |

*"Quello che i risultati dimostrano è che carichi di lavoro pesanti per i metadati, come un make clean, raddoppiano la quantità di dati scritti sul disco. Questo è naturale, dal momento che tutt i cambiamenti ai blocchi dei metadati sono prima scritti sul journal e la transazione del journal viene completata prima che i metadati vengano scritti nella loro posizione finale sul disco. Comunque per carichi di lavoro più comuni dove avvengono scritture e modifiche di blocchi metadati, la differenza è molto più piccola."*

**Note:** L'esempio di make clean della tabella precedente enfatizza l'importanza di compilare intenzionalmente in /dev/shm come raccomandato nella [precedente sezione](#Compilare_in_.2Fdev.2Fshm) di questo articolo!

### Scelta del Filesystem

Esistono molte opzioni per i filesystem inclusi ext2, ext3, ext4, btrfs, ecc.

#### Btrfs

Il supporto a [Btrfs](https://it.wikipedia.org/wiki/Btrfs) è stato incluso con la release principale del kernel Linux versione 2.6.29\. Qualcuno sostiene che non sia abbastanza maturo per l'utilizzo in ambienti di produzione mentre altri già da tempo utilizzano questo potenziale successore di ext4\. Notare che quando questo articolo è stato originariamente scritto (27-Giugno-2010), una versione stabile di btfrs non esiste. Vedere [questo](http://www.madeo.co.uk/?p=346) articolo di blog per maggiori informazioni su btfrs. Assicurarsi di leggere anche il [wiki di btfrs](https://btrfs.wiki.kernel.org/index.php/Main_Page).

**Warning:** Al momento in cui questo è stato scritto (21-Nov-2010) non esiste un utility fsck per diagnosticare e correggere errori sulle partizioni btrfs. Mentre Btrfs è stabile su una macchina stabile, è attualmente possibile corrompere irrimediabilmente un filesystem nel caso di crash o interruzione di alimentazione ai dischi che non gestiscono le richieste di flush correttamente.

#### Ext4

[Ext4](https://it.wikipedia.org/wiki/Ext4) è un altro filsesystem che supporta gli SSD. Viene considerato stabile a partire dalla versione 2.6.28 ed è sufficientemente maturo per un uso quotidiano. Contrariamente a btrfs, ext4 non riconosce automaticamente la natura del disco ed è necessario abilitare esplicitamente il supporto al comando TRIM attraverso l'opzione di mount **discard** in [fstab](/index.php/Fstab_(Italiano) "Fstab (Italiano)") (oppure con tune2fs -o discard /dev/sdaX). Vedere la [documentazione ufficiale del kernel](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=blob;f=Documentation/filesystems/btrfs.txt;h=64087c34327fe0ba11e790e0a41224b8e7c1d30c;hb=HEAD) per maggiori informazioni su ext4.

## Misurare le Prestazioni degli SSD

Vedere l'articolo [SSD Benchmarking](/index.php/SSD_Benchmarking "SSD Benchmarking") per una procedura generale per misurare le prestazioni del proprio SSD o per vedere le prestazioni di alcuni SSD presenti nel database.

## Aggiornamenti del Firmware

### OCZ

OCZ ha una utility da riga di comando disponibile per linux (i686 e x86_64) sul proprio forum [qui](http://www.ocztechnologyforum.com/forum/showthread.php?82289-1st-Public-beta-test-of-OCZ-Sandforce-Linux-based-firmware-upddate-tool).