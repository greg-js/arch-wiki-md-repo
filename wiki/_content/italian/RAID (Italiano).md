## Contents

*   [1 Introduzione](#Introduzione)
    *   [1.1 Livelli RAID Standard](#Livelli_RAID_Standard)
    *   [1.2 Livelli RAID annidati](#Livelli_RAID_annidati)
    *   [1.3 Ridondanza](#Ridondanza)
    *   [1.4 Comparazione tra i livelli RAID](#Comparazione_tra_i_livelli_RAID)
*   [2 Installazione](#Installazione)
    *   [2.1 Preparare il dispositivo](#Preparare_il_dispositivo)
    *   [2.2 Creare la tabella delle partizioni](#Creare_la_tabella_delle_partizioni)
        *   [2.2.1 Codice delle partizioni](#Codice_delle_partizioni)
    *   [2.3 Copiare la tabella delle partizioni](#Copiare_la_tabella_delle_partizioni)
    *   [2.4 Costruire l'array](#Costruire_l.27array)
    *   [2.5 Aggiornare il file di configurazione](#Aggiornare_il_file_di_configurazione)
    *   [2.6 Configurare il filesystem](#Configurare_il_filesystem)
    *   [2.7 Assemblare l'array al boot](#Assemblare_l.27array_al_boot)
    *   [2.8 Aggiungere all'immagine del kernel](#Aggiungere_all.27immagine_del_kernel)
*   [3 Montaggio da un Live CD](#Montaggio_da_un_Live_CD)
*   [4 Rimozione di un dispositivo, smettere di usare l'array](#Rimozione_di_un_dispositivo.2C_smettere_di_usare_l.27array)
*   [5 Aggiunta di un dispositivo all'array](#Aggiunta_di_un_dispositivo_all.27array)
*   [6 Monitoraggio](#Monitoraggio)
    *   [6.1 Utilizzare mdstat](#Utilizzare_mdstat)
    *   [6.2 Tracciamento IO con iotop](#Tracciamento_IO_con_iotop)
    *   [6.3 Inviare mail in caso di eventi](#Inviare_mail_in_caso_di_eventi)
*   [7 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [7.1 Avviare l'array in sola lettura](#Avviare_l.27array_in_sola_lettura)
    *   [7.2 Ripristino da un disco rotto o mancante nel raid](#Ripristino_da_un_disco_rotto_o_mancante_nel_raid)
*   [8 Analisi delle prestazioni](#Analisi_delle_prestazioni)
*   [9 Ulteriori riferimenti](#Ulteriori_riferimenti)

## Introduzione

**Nota:** Si veda l'articolo di [Wikipedia](http://it.wikipedia.org)su questo argomento per maggiori informazioni:[wikipedia:it:RAID](https://en.wikipedia.org/wiki/it:RAID "wikipedia:it:RAID").

I dispositivi RAID (Redundant Array of Independent Disks - insieme ridondante di dischi indipendenti) sono dispositivi virtuali creati da due o più dispositivi a blocchi reali . Questo consente a più dispositivi (in genere unità disco o partizioni di esse) per essere combinati in un unico blocco per contenere (ad esempio) un singolo filesystem. RAID è progettato per impedire la perdita di dati nel caso di un guasto del disco rigido. Vi sono diversi [livelli di RAID](http://it.wikipedia.org/wiki/RAID#Livelli_RAID_standard).

### Livelli RAID Standard

	[RAID-0](https://en.wikipedia.org/wiki/it:RAID#RAID_0_.28Striping.29 "wikipedia:it:RAID")

	Utilizza lo striping per combinare i dischi. Non propriamente un sistema RAID, in quanto *non fornisce alcuna ridondanza*. Essa, tuttavia , offre *un grande vantaggio in velocità*. In questo esempio si utilizza RAID-0 per lo swap, partendo dal presupposto che un sistema desktop è in uso, in cui l'aumento della velocità vale la possibilità di arresto anomalo del sistema se uno dei dischi si guasta. Su un server, un RAID-1 o RAID-5 è più appropriato. L'affidabilità di un dato sistema RAID-0 è uguale all'affidabilità media dei dischi diviso per il numero di dischi presenti. Quindi l'affidabilità, misurata come tempo medio tra due guasti (MTBF) è inversamente proporzionale al numero degli elementi; cioè un sistema di due dischi è affidabile la metà di un disco solo.

	[RAID-1](https://en.wikipedia.org/wiki/it:RAID#RAID_1_.28Mirroring.29 "wikipedia:it:RAID")

	Il livello RAID più semplice: mirroring puro. Come con altri livelli RAID, ha senso solo se le partizioni risiedono sono su disci fisici diverse. Se uno di questi dischi si guasta, il dispositivo a blocchi fornito dal sistema RAID continuerà a funzionare normalmente. L'esempio utilizza RAID-1 per tutto tranne che per swap. Si noti che RAID-1 è l'unica opzione utilizzabile per la partizione di boot, perché un bootloader (che legge la partizione di avvio) non riconosce il RAID, ma una partizione componente del RAID-1 può essere letta come una normale partizione. La dimensione di un sistema RAID-1 equivale alla dimensione della partizione più piccola che lo compone.

	[RAID-5](https://en.wikipedia.org/wiki/it:RAID#RAID_5_.28Distributed_Parity.29 "wikipedia:it:RAID")

	Funziona con 3 o più unità fisiche, e fornisce la ridondanza di RAID-1 in combinazione con incrementi di velocità e dimensioni di RAID-0\. RAID-5 utilizza lo striping, come RAID-0, ma memorizza anche blocchi di parità distribuiti su ogni disco che lo compone. Nel caso di un disco guasto, questi blocchi di parità sono utilizzati per ricostruire i dati su un disco sostitutivo. RAID-5 in grado di sopportare la perdita di un disco che lo compone.

**Nota:** RAID-5 è comunemente scelto per la sua combinazione tra velocità e ridondanza dei dati. L'avvertenza è che se 1 unità dovesse fallire, e prima che essa venga sostituita, un'altra unità dovesse fallire, tutti i dati saranno persi. Per informazioni esaustive, riguardo a questo argomento, si veda la discussione *[RAID5 Risks](http://ubuntuforums.org/showthread.php?t=1588106)* sul forum di Ubuntu. La migliore alternativa a RAID-5, quando la ridondanza è di fondamentale importanza, è RAID-10.

### Livelli RAID annidati

	[RAID 1+0](https://en.wikipedia.org/wiki/it:RAID#RAID_1.2B0 "wikipedia:it:RAID")

	Comunemente chiamato RAID-10, è un RAID nidificato che combina due dei livelli standard di RAID per ottenere prestazioni e ridondanza supplementari.

### Ridondanza

**Attenzione:** L'installazione di un sistema con RAID è un processo complesso che può distruggere i dati. Assicurarsi di eseguire il backup di tutti i dati prima di procedere.

RAID non fornisce una garanzia che i dati siano al sicuro. In caso di incendio, se il computer viene rubato oppure se più di un disco fallisce, RAID non proteggerà i dati. Pertanto, è importante fare delle copie di backup (vedi i [programmi di backup](/index.php/Backup_programs "Backup programs")). Se si utilizzano unità a nastro, DVD, CDROM o un altro computer, mantenere una copia aggiornata dei vostri dati dal vostro computer (e preferibilmente fuori sede). Si prenda l'abitudine di fare backup regolari. È anche possibile dividere i dati sul computer in directory correnti e archiviati. Quindi eseguire il backup dei dati correnti in modo frequente, e di tanto in tanto dei dati archiviati .

### Comparazione tra i livelli RAID

| Livello RAID | Ridondanza Dati | Utilizzo fisico delle unità | Prestazioni in lettura | Prestazioni in scrittura | Unità Min |
| **0** | **No** | 100% | **Superiore** | **Superiore** | 1 |
| **1** | Si | 50% | Molto alta | Molto alta | 2 |
| **5** | Si | 67% - 94% | **Superiore** | Alta | 3 |
| **6** | Si | 50% - 88% | Molto alta | Alta | 4 |
| **10** | Si | 50% | Molto alta | Molto alta | 4 |

## Installazione

[Installare](/index.php/Pacman "Pacman") [mdadm](https://www.archlinux.org/packages/?name=mdadm) e [parted](https://www.archlinux.org/packages/?name=parted), disponibili nei [Depositi ufficiali](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)").

### Preparare il dispositivo

Per evitare possibili problemi di ogni sorta, si dovrebbe considerare l'eventualità di cancellare l'intero disco prima di impostare un RAID. Questo dovrebbe essere ripetuto per ogni disco che si prevede di utilizzare per il RAID, questi comandi cancellano completamente qualsiasi cosa sia attualmente sul dispositivo!

**Attenzione:** I seguenti passaggi elimineranno qualsiasi dato sul `/dev/disco-da-cancellare`, quindi digitate con attenzione

Cancellare qualsiasi vecchia informazioni di configurazione RAID

 `# mdadm --zero-superblock /dev/disk-to-clean` 

Cancellare tutti i dati della tabella delle partizioni

 `# dd if=/dev/zero of=/dev/disk-to-clean bs=4096 count=1` 

Assicurarsi di cancellare le vecchie voci del kernel

 `# partprobe -s` 

Verificare le voci in `/etc/fstab` e `/etc/mdadm.conf`

Con un RAID software, disabilitare la cache del disco rigido aiuta a prevenire la perdita di dati in caso di perdita di corrente, fino a quando non si utilizza un gruppo di continuità [UPS](https://en.wikipedia.org/wiki/it:Uninterruptible_power_supply "wikipedia:it:Uninterruptible power supply"). Ripetere il comando per ogni unità dell'array. Si noti tuttavia che ciò diminuisce le prestazioni .

 `# hdparm -W 0 /dev/path_to_disk` 

### Creare la tabella delle partizioni

La configurazione RAID varia in base ai diversi livelli di RAID. Se si sa che tipo di RAID si desidera e si è già impostato di conseguenza il proprio hardware, si può procedere con la formattazione dei dischi che si desidera inserire nell'array. E' anche possibile creare un'array RAID direttamente sui dischi grezzi (senza partizioni), ma non è raccomandato perché può causare problemi durante la sostituzione di un disco guasto.

Quando si sostituisce un disco guasto di un array RAID , il nuovo disco deve essere esattamente della stessa dimensione del disco guasto o più grande - altrimenti il processo di ricreazione dell'array non funzionerà. Anche i dischi rigidi della stessa marca e modello possono avere delle piccole differenze di dimensioni. Lasciare un piccolo spazio alla fine del disco non allocato può compensare le differenze dimensionali tra le unità, il che rende facile la scelta di un modello di unità di sostituzione. Pertanto, è buona norma lasciare circa 100 MB di spazio non allocato alla fine del disco.

Formattare una delle unità dell'array con il vostro strumento preferito. Per esempio,

 `# cfdisk /dev/path_to_disk` 
**Tip:** Utilizzare GParted per creare le partizioni e allinearle al cilindro, creerà l'allineamento ottimale del disco. Ciò può essere ottenuto utilizzando [Gnome Partition Editor Live Media](http://gparted.sourceforge.net/livecd.php).

#### Codice delle partizioni

I due [tipi di partizioni](https://en.wikipedia.org/wiki/partition_type "wikipedia:partition type") applicabili ai dispositivi RAID sono Non-FS data e Linux RAID auto. Si raccomanda l'uso di "Non-FS data", così il vostro array non sarà assemblato automaticamente durante l'avvio. Utilizzando "Linux RAID Auto" si può incorrere in problemi avviando un live-cd o attivando un array RAID degradato in un sistema diverso (nal peggiore dei casi, in presenza di altri array RAID degradati), dato che Linux cercherà di assemblare e sincronizzare l'array, e quindi potrebbe rendere i dati illeggibili nel caso assemblasse l'array in modo errato.

**Nota:** cfdisk e mkpart utilizzano una serie di "tipi di filesystem" per impostare i codici di partizione. Ogni tipo corrisponde ad un codice di partizione ( vedere il [manuale utente di Parted](http://www.gnu.org/software/parted/manual/html_node/mkpart.html#mkpart)). Esso utilizza il tipo `da` per denotare non-FS data e `fd` per Linux RAID auto.

### Copiare la tabella delle partizioni

Una volta che si dispone di un disco partizionato e allineato in modo corretto, è possibile copiare la configurazione su qualsiasi altro disco.

Verificare che le partizioni soddisfino i requisiti di base:

 `# sfdisk -lRV /dev/percorso_array_del_disco_formattato` 

Effettuare un Dump della tabella delle partizioni del disco formattato in un file::

 `# sfdisk -d /dev/percorso_array_del_disco_formattato > ~/array_formattata.dump` 

Copiare la tabella di partizione dal file dump del disco per tutti i dischi che compongono l'array:

 `# sfdisk /dev/percorso_array_del_disco_'''non'''_formattato < ~/array_formattata.dump` 

Dopo aver ripetuto il comando per ogni disco non formattato dell'array, verificare che i dischi siano identici con:

```
# fdisk -l

```

o

```
# sfdisk -l -u S

```

### Costruire l'array

Ora si costruirà l'array (e.g. [post sulla configurazione RAID5](http://fomori.org/blog/blog/2011/10/19/raid5-server-to-hold-all-your-data-%e2%80%94-the-nas-alternative/)).

**Attenzione:** Assicurarsi di modificare i **valori in grassetto** qui sotto per farli corrispondere alla vostra configurazione.
 ` # mdadm --create --verbose /dev/md/vostra_array --level=**5** --metadata=**1.2** --chunk=**256** --raid-devices=**5 /dev/percorso_array_del_disco-1 /dev/percorso_array_del_disco-2 /dev/percorso_array_del_disco-3 /dev/percorso_array_del_disco-4 /dev/percorso_array_del_disco-5** ` 

L'array viene creato sotto la periferica virtuale */dev/md/vostra_array*, assemblato e pronto per l'uso (in modalità degradata). Si può direttamente iniziare ad usarlo mentre mdadm sincronizza l'array in background. La sincronizzazione può richiedere molto tempo per ripristinare la parità, è possibile controllare lo stato dell'avanzamento con:

 `$ cat /proc/mdstat` 

### Aggiornare il file di configurazione

Dal momento che il programma di installazione crea initrd utilizzando il file `/etc/mdadm.conf` nel sistema di destinazione, è necessario aggiornare il file di configurazione predefinito. Il file predefinito può essere sovrascritto con l'operatore di reindirizzamento, perché contiene solo commenti esplicativi.

Reindirizzare il contenuto dei metadati memorizzati sui dispositivi con nome al file di configurazione :

```
# mdadm --examine --scan > /etc/mdadm.conf

```

**Nota:** Se si sta aggiornando la configurazione RAID all'interno del programma di installazione di Arch, passando ad un'altra TTY, sarà necessario assicurarsi che si stia scrivendo nel file `mdadm.conf` corretto.

```
# mdadm --examine --scan > /mnt/etc/mdadm.conf

```

Una volta che il file di configurazione è stato aggiornato, l'array può essere assemblato usando mdadm:

```
# mdadm --assemble --scan

```

### Configurare il filesystem

L'array può essere formattato come qualsiasi altro disco, basta considerare che:

*   A causa delle dimensioni del volume di grandi dimensioni, non tutti i file system sono adatti (si veda: [File system limits](https://en.wikipedia.org/wiki/Comparison_of_file_systems#Limits "wikipedia:Comparison of file systems")).
*   Il filesystem dovrebbe supportare il ridimensionamento mentre è online (si veda: [File system features](https://en.wikipedia.org/wiki/Comparison_of_file_systems#Features "wikipedia:Comparison of file systems")).
*   Il guadagno maggiore delle prestazioni che si può ottenere su un'array RAID è quello di assicurarsi di formattare il volume allineato alle dimensioni striping RAID (si veda: [RAID Math](http://wiki.centos.org/HowTos/Disk_Optimization)).

### Assemblare l'array al boot

Se è stato selezionato "non-FS data" come codice della partizione, l'array non verrà assemblato automaticamente dopo l'avvio successivo. Per assemblare l'array immettere il seguente comando:

 ` # mdadm --assemble --scan /dev/vostra_array --uuid=vostra_array_uuid ` 

o scriverlo in `rc.local`.

### Aggiungere all'immagine del kernel

Consultare [mkinitcpio](/index.php/Mkinitcpio_(Italiano) "Mkinitcpio (Italiano)") per maggiori informazioni.

Aggiungere **mdadm** oppure **mdadm_udev** nella sezione *HOOKS=* del file `/etc/mkinitcpio.conf` prima dell'hook filesystem. Questo aggiungerà il supporto per mdadm direttamente nell'immagine.

 `HOOKS="base udev autodetect block **mdadm_udev** filesystems usbinput fsck"` Si possono visualizzare gli hook disponibili per la sezione *HOOKS=* con il comando `# mkinitcpio -L` ed ottenere informazioni riguardo ogni hook con: `# mkinitcpio -H mdadm_udev` 

Aggiungere il modulo **raid456** ed il modulo del filesystem utilizzato sul raid (ext4) nella sezione *MODULES=* del file `/etc/mkinitcpio.conf`. Questo inserirà i moduli nell'immagine del kernel.

 `MODULES="**ext4 raid456**"` Successivamente rigenerare initrd con il comando: `# mkinitcpio -p linux` oppure se si utilizza [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) `# mkinitcpio -p linux-lts` 

## Montaggio da un Live CD

Se si desidera montare la partizione RAID da un CD Live, utilizzare

```
# mdadm --assemble /dev/md0 /dev/sda3 /dev/sdb3 /dev/sdc3

```

(o un qualsiasi mdX e dispositivi, corrispondenti ai vostri)

**Note:** Live CD come [SystemRescueCd](http://www.sysresccd.org/Main_Page) assemblano gli array RAID automaticamente all'avvio del sistema , se è stata utilizzata la partizione di tipo fd durante l'installazione dell'array)

## Rimozione di un dispositivo, smettere di usare l'array

È possibile rimuovere un dispositivo dall'array dopo averlo marcato come difettoso.

```
# mdadm --fail /dev/md0 /dev/sdxx

```

Successivamente è possibile rimuoverlo dall'array.

```
# mdadm -r /dev/md0 /dev/sdxx

```

Se si vuole rimuovere il dispositivo in modo permanente (ad esempio nel caso in cui si desidera utilizzarlo individualmente da ora in poi). Eseguire i due comandi sopra descritti e in seguito:

```
# mdadm --zero-superblock /dev/sdxx

```

In questo modo si può utilizzare il disco normalmente come prima della creazione dell'array.

**Attenzione:** Se si riutilizza il disco rimosso senza effettuare l'azzeramento del superblocco verranno **PERSI** tutti i dati dopo il successivo ri-avvio (poichè mdadm tenta di utilizzarlo come membro del raid). **NON** eseguire questo comando su array di tipo linear o RAID0 altrimenti verranno **PERSI** tutti i dati sul raid.

Smettere di usare l'array:

1.  Smontare l'array interessato
2.  Fermare l'array con: `mdadm --stop /dev/md0`
3.  Ripetere i tre comandi descritti all'inizio di questa sezione su ogni dispositivo.
4.  Rimuovere la linea corrispondente dal file `/etc/mdadm.conf`.

## Aggiunta di un dispositivo all'array

L'aggiunta di nuovi dispositivi con mdadm può essere effettuata su di un sistema avviato e con i dispositivi montati. Partizionare il nuovo dispositivo `/dev/sdx` utilizzando lo stesso layout di uno di quelli appartenenti all'array `/dev/sda`.

```
# sfdisk -d /dev/sda > table
# sfdisk /dev/sdx < table

```

Assemblare gli array RAID, se non sono già assemblati:

```
# mdadm --assemble /dev/md1 /dev/sda1 /dev/sdb1 /dev/sdc1
# mdadm --assemble /dev/md2 /dev/sda2 /dev/sdb2 /dev/sdc2
# mdadm --assemble /dev/md0 /dev/sda3 /dev/sdb3 /dev/sdc3

```

In primo luogo, aggiungere il nuovo dispositivo come dispositivo di riserva(Spare Device) per tutti gli array. Si assume di aver seguito la guida e si utilizzino array separati per `/boot` RAID-1 (/dev/md1), `swap` RAID-1 (/dev/md2) e `root` RAID-5 (/dev/md0).

```
# mdadm --add /dev/md1 /dev/sdx1
# mdadm --add /dev/md2 /dev/sdx2
# mdadm --add /dev/md0 /dev/sdx3

```

Questo procedimento eseguito con mdadm non dovrebbe impiegare troppo tempo. Verificare lo stato di avanzamento con:

```
# cat /proc/mdstat

```

Verificare che il dispositivo sia stato aggiunto con il comando:

```
# mdadm --misc --detail /dev/md0

```

Dovrebbe essere elencato come un dispositivo di riserva.

Istruire mdadm per espandere gli array da 3 a 4 dispositivi (o comunque al numero di dispositivi che si desidera utilizzare):

```
# mdadm --grow -n 4 /dev/md1
# mdadm --grow -n 4 /dev/md2
# mdadm --grow -n 4 /dev/md0

```

Il procedimento probabilmente richiederà diverse ore. È necessario attendere la fine del processo prima di poter continuare. Controllare lo stato di avanzamento in `/proc/mdstat`. Gli array di tipo RAID-1 dovrebbero sincronizzarsi automaticamente `/boot` e `swap`, ma sarà necessario installare manualmente GRUB sull'MBR del nuovo dispositivo. Si veda [Installare il bootloader su un dispositivo alternativo per l'avvio](/index.php/Installing_with_Software_RAID_or_LVM#Install_the_bootloader_on_the_Alternate_Boot_Drives "Installing with Software RAID or LVM").

Il resto di questa guida spiegherà come ridimensionare il volume LVM e il filesystem sull'array RAID-5.

**Nota:** Non vi è la certezza che questo procedimento possa essere effettuato con i volumi montati e si assume che si stia operando da un live-cd/usb

Se si hanno i volumi LVM cifrati con LUKS, bisogna ridimensionare innanzitutto il volume LUKS per primo. In caso contrario, ignorare questo punto.

```
# cryptsetup luksOpen /dev/md0 cryptedlvm
# cryptsetup resize cryptedlvm

```

Attivare i gruppi di volumi LVM:

```
# vgscan
# vgchange -ay

```

Ridimensionare il volume fisico LVM(Physical Volume) `/dev/md0` (o ad esempio `/dev/mapper/cryptedlvm` se usate LUKS) per occupare tutto lo spazio disponibile sull'array. Si possono elencare con il comando `pvdisplay`.

```
# pvresize /dev/md0

```

Ridimensionare il volume logico(Logical Volume) a cui si desidera assegnare il nuovo spazio. Si possono elencare con "lvdisplay" . Supponendo che si vuole assegnarlo tutto al volume `/home`:

```
# lvresize -l +100%FREE /dev/array/home

```

Per ridimensionare il filesystem, per allocare il nuovo spazio, utilizzare lo strumento appropriato. Se si utilizza ext2 è possibile ridimensionare un filesystem montato con ext2online. Nel caso di ext3 è possibile utilizzare resize2fs o ext2resize ma non mentre è montata.

Si dovrebbe effettuare un check del filesystem prima di ridimensionarlo.

```
# e2fsck -f /dev/array/home
# resize2fs /dev/array/home

```

Leggere i manuali di lvresize e resize2fs se si desidera personalizzare le dimensioni per i volumi.

## Monitoraggio

Un semplice comando lienare che stampa lo stato dei dispositivi RAID:

```
awk '/^md/ {printf "%s: ", $1}; /blocks/ {print $NF}' </proc/mdstat

```

```
md1: [UU]
md0: [UU]

```

### Utilizzare mdstat

 `watch -t 'cat /proc/mdstat'` 

O se preferite usare [tmux](https://www.archlinux.org/packages/?name=tmux)

 `tmux split-window -l 12 "watch -t 'cat /proc/mdstat'"` 

### Tracciamento IO con iotop

Il pacchetto [iotop](https://www.archlinux.org/packages/?name=iotop) consente di visualizzare le statistiche di input/output dei processi. Utilizzare questo comando per visualizzare l'I/O per i processi relativi al raid.

```
# iotop -a -p $(sed 's, , -p ,g' <<<`pgrep "_raid|_resync|jbd2"`)

```

### Inviare mail in caso di eventi

Sarà necessario un server smtp (sendmail) oppure almeno un email forwarder (ssmtp/msmtp). Assicurarsi di aver configurato una email in `/etc/mdadm.conf`

```
# mdadm --monitor --scan --test

```

Quando tutto sarà pronto sarà possibile abilitare l'avvio del servizio:

```
# systemctl enable mdadm.service

```

## Risoluzione dei problemi

Se al riavvio si riscontra l'errore "invalid raid superblock magic" e si dispone di ulteriori dischi rigidi diversi da quelli su cui è configurato il RAID, verificare che l'ordine dei dischi rigidi sia corretto. Durante l'installazione, i dispositivi RAID possono essere hdd, hde e hdf, ma durante l'avvio possono essere hda, hdb e hdc. Regolare la linea del kernel di GRUB di conseguenza.

### Avviare l'array in sola lettura

Quando un'array md viene avviata, il superblock sarà scritto, e potrebbe avviarsi la sincronizzazione. Per inizializzare in sola lettura, impostare il modulo del kernel `md_mod` con il parametro `start_ro`. Quando è impostato, i nuovi array verranno attivati in modalità 'auto -ro', che disabilita tutti gli I/O interni (aggiornamenti superblocco, resync, recupero) e passa automaticamente a 'rw' quando arriva la prima richiesta di scrittura.

**Nota:** L'array può essere impostato sulla modalità 'ro' utilizzando `mdadm -r` prima che avvenga la richiesta di scrittura, oppure si può avviare la sincronizzazione senza una richiesta di scrittura utilizzando `mdadm -w`.

Per impostare il parametro al boot, aggiungerlo `md_mod.start_ro=1` alla linea del kernel.

O impostare il modulo in fase di caricamento dal file `/etc/modprobe.d/` o direttamente da `/sys/`.

```
echo 1 > /sys/module/md_mod/parameters/start_ro

```

### Ripristino da un disco rotto o mancante nel raid

Si potrebbe ottenere l'errore menzionato sopra anche quando una delle unità si interrompe per una qualsiasi ragione. In questo caso si dovrà quindi attivare il raid anche in assenza di un disco. Digitare quanto segue (modificare se necessario):

```
# mdadm --manage /dev/md0 --run

```

Ora si dovrebbe essere in grado di montarlo nuovamente con qualcosa di simile (se presente al relativa voce in fstab ):

```
# mount /dev/md0

```

Ora il raid dovrebbe funzionare di nuovo e sarà disponibile per l'utilizzo, ma con un disco in meno! Quindi, dopo averlo partizionato come descritto in [Preparare il dispositivo](#_Preparare_il_dispositivo). Una volta fattto questo sarà possibile aggiungere il nuovo disco al raid digitando:

```
# mdadm --manage --add /dev/md0 /dev/sdd1

```

Se si digita:

```
# cat /proc/mdstat

```

probabilmente si vedrà che il raid è ora attivo e in ricostruzione.

Si potrebbe anche voler aggiornare la configurazione (vedi: [Aggiornare il file di configurazione](#Aggiornare_il_file_di_configurazione)).

## Analisi delle prestazioni

Ci sono diversi strumenti per misurare le prestazioni di un RAID. Il miglioramento più evidente è l'aumento di velocità di lettura di più thread sul volume del RAID.

[Tiobench](http://sourceforge.net/projects/tiobench/) è un programma che misura le prestazioni di lettura multi-threaded.

[Bonnie++](http://www.coker.com.au/bonnie++/) analizza l'accesso ad uno o più file, come se fossero un database, la creazione, lettura e cancellazione di file piccoli in modo da simulare il comportamento di programmi quali Squid, INN o file Maildir. Il programma [ZCAV](http://www.coker.com.au/bonnie++/zcav/) analizza le prestazioni di diverse zone di un hard disk senza scritture.

`hdparm` **non** dovrebbe essere utilizzato per le analisi sul RAID, in quanto fornisce risultati molto incoerenti.

## Ulteriori riferimenti

*   [RAID/Software](http://en.gentoo-wiki.com/wiki/RAID/Software) sul Wiki di Gentoo
*   [Software RAID Install](http://en.gentoo-wiki.com/wiki/Software_RAID_Install) sul Wiki di Gentoo
*   [Software RAID in the new Linux 2.4 kernel, Part 1](http://www.gentoo.org/doc/en/articles/software-raid-p1.xml) e [Part 2](http://www.gentoo.org/doc/en/articles/software-raid-p2.xml) nella documentazione di Gentoo
*   [Linux RAID wiki entry](http://raid.wiki.kernel.org/index.php/Linux_Raid) negli archivi del Linux Kernel
*   [Arch Linux software RAID installation guide](http://linux-101.org/howto/arch-linux-software-raid-installation-guide) su Linux 101
*   [Chapter 15: Redundant Array of Independent Disks (RAID)](http://docs.redhat.com/docs/en-US/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/ch-raid.html) nella documentazione di Red Hat Enterprise Linux 6
*   [Linux-RAID FAQ](http://tldp.org/FAQ/Linux-RAID-FAQ/x37.html) nel Linux Documentation Project
*   [Dell.com Raid Tutorial](http://support.dell.com/support/topics/global.aspx/support/entvideos/raid?c=us&l=en&s=gen) - Guida interattiva sul Raid
*   [BAARF](http://www.miracleas.com/BAARF/) e *[Why should I not use RAID 5?](http://www.miracleas.com/BAARF/RAID5_versus_RAID10.txt)* di Art S. Kagel
*   [Introduction to RAID](http://www.linux-mag.com/id/7924/), [Nested-RAID: RAID-5 and RAID-6 Based Configurations](http://www.linux-mag.com/id/7931/), [Intro to Nested-RAID: RAID-01 and RAID-10](http://www.linux-mag.com/id/7928/), and [Nested-RAID: The Triple Lindy](http://www.linux-mag.com/id/7932/) su Linux Magazine

**mdadm**

*   [Debian mdadm FAQ](http://anonscm.debian.org/gitweb/?p=pkg-mdadm/mdadm.git;a=blob_plain;f=debian/FAQ;hb=HEAD)
*   [mdadm source code](http://www.kernel.org/pub/linux/utils/raid/mdadm/)
*   [Software RAID on Linux with mdadm](http://www.linux-mag.com/id/7939/) su Linux Magazine

**Thread sui forum**

*   [Raid Performance Improvements with bitmaps](http://forums.overclockers.com.au/showthread.php?t=865333)
*   2011-08-28 - Arch Linux - [GRUB and GRUB2](https://bbs.archlinux.org/viewtopic.php?id=125445)
*   2011-08-03 - Arch Linux - [Can't install grub2 on software RAID](https://bbs.archlinux.org/viewtopic.php?id=123698)
*   2011-07-29 - Gentoo - [Use RAID metadata 1.2 in boot and root partition](http://forums.gentoo.org/viewtopic-t-888624-start-0.html)

**RAID con crittografia**

*   [Linux/Fedora: Encrypt /home and swap over RAID with dm-crypt](http://www.shimari.com/dm-crypt-on-raid/) di Justin Wells