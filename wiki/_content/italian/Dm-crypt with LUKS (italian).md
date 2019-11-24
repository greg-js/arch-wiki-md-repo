Articoli correlati

*   [Disk Encryption (Italiano)](/index.php/Disk_Encryption_(Italiano) "Disk Encryption (Italiano)")
*   [Removing System Encryption](/index.php/Removing_System_Encryption "Removing System Encryption")

Questo articolo si concentra su come configurare un sistema completamente crittografato su Arch Linux, usando dm-crypt con LUKS.

**dm-crypt** è il device-mapper standard per le funzionalità di crittografia fornito dal kernel Linux. Può essere utilizzato direttamente da chi desidera avere un completo controllo degli aspetti del partizionamento e della gestione delle chiavi.

**LUKS** è un comodo strato aggiuntivo il quale archivia tutte le informazioni necessarie alla configurazione di dm-crypt sul disco stesso e si occupa anche della gestione delle partizioni e delle chiavi nel tentativo di facilitarne l’uso.

Per maggiori dettagli sui paragoni tra dm-crypt+LUKS e gli altri metodi di crittografia, consultare [la tavola comparativa](/index.php/Disk_encryption#Comparison_table "Disk encryption").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configurazione iniziale](#Configurazione_iniziale)
    *   [1.1 Panoramica e preparazione](#Panoramica_e_preparazione)
    *   [1.2 Cancellazione sicura del/degli hard disk](#Cancellazione_sicura_del/degli_hard_disk)
        *   [1.2.1 Usare un contenitore LUKS come generatore di numeri pseudo-casuali (alternativa)](#Usare_un_contenitore_LUKS_come_generatore_di_numeri_pseudo-casuali_(alternativa))
            *   [1.2.1.1 Cancellare lo spazio libero con un file criptato dopo l'installazione](#Cancellare_lo_spazio_libero_con_un_file_criptato_dopo_l'installazione)
        *   [1.2.2 Cancellare i keyslot LUKS](#Cancellare_i_keyslot_LUKS)
        *   [1.2.3 Cancellare i LUKS header](#Cancellare_i_LUKS_header)
        *   [1.2.4 Supporto per discard/TRIM per i dischi a stato solido (SSD)](#Supporto_per_discard/TRIM_per_i_dischi_a_stato_solido_(SSD))
    *   [1.3 Partizionamento](#Partizionamento)
        *   [1.3.1 Partizioni standard](#Partizioni_standard)
        *   [1.3.2 LVM: Logical Volume Manager](#LVM:_Logical_Volume_Manager)
            *   [1.3.2.1 LVM on LUKS](#LVM_on_LUKS)
            *   [1.3.2.2 LUKS on LVM](#LUKS_on_LVM)
        *   [1.3.3 Creare le partizioni sul disco](#Creare_le_partizioni_sul_disco)
            *   [1.3.3.1 Sistemi con singolo disco](#Sistemi_con_singolo_disco)
            *   [1.3.3.2 Sistemi con dischi multipli](#Sistemi_con_dischi_multipli)
*   [2 Configurare LUKS](#Configurare_LUKS)
    *   [2.1 Mappare le partizioni fisiche con LUKS](#Mappare_le_partizioni_fisiche_con_LUKS)
        *   [2.1.1 Usare LUKS per formattare partizioni con la parola d'ordine](#Usare_LUKS_per_formattare_partizioni_con_la_parola_d'ordine)

## Configurazione iniziale

### Panoramica e preparazione

Il supporto di installazione di Arch comprende gli strumenti necessari per la crittografia del sistema. L’installazione di un sistema crittografato è in gran parte simile ad una normale installazione, sarà quindi possibile seguire la [Guida all’installazione di Arch Linux](/index.php/Official_Arch_Linux_Install_Guide_(Italiano) "Official Arch Linux Install Guide (Italiano)") oppure la [Beginners' Guide](/index.php/Beginners%27_guide_(Italiano) "Beginners' guide (Italiano)") dopo aver configurato le partizioni crittografate. Sarà necessario sistemare la configurazione del sistema per far si che possa avviarsi dai volumi Luks.

La routine di creazione di un sistema criptato segue questi passaggi generali:

*   Cancellazione sicura del/degli hard disk
*   Partizionamento e configurazione della crittografia ([LVM](/index.php/LVM_(Italiano) "LVM (Italiano)") è opzionale)
*   Selezione ed installazione dei pacchetti
*   Configurazione del sistema

**Attenzione:** Crittografando una partizione verrà cancellato tutto il suo contenuto. Si consiglia di effettuare i backup necessari prima di iniziare.

### Cancellazione sicura del/degli hard disk

**Nota:** I seguenti metodi sono specifici per dm-crypt/LUKS. Per istruzioni più dettagliate su come cancellare e preparare un disco consultare [Securely wipe disk](/index.php/Securely_wipe_disk "Securely wipe disk")

Si consiglia di cancellare in modo sicuro i dati accessibili nelle partizioni o dischi utilizzando dati casuali. I dati casuali saranno scritti per motivi di sicurezza perché sono indistinguibili dai dati successivamente scritti da dm-crypt. La cancellazione sicura dei dischi implica la sovrascrittura dell’intero disco con dati casuali.

Entrambi i dischi sia nuovi che usati dovrebbero essere sovrascritti in maniera sicura. Questo aiuta ad assicurare la privacy dei dati che si trovano sulle partizioni criptate. Il contenuto dei dischi comprati dal produttore non è assicurato. Se il disco è stato riempito con bit di valore zero e successivamente usato per dati criptati, allora sarà relativamente semplice identificare dove finiscono i dati criptati e dove iniziano gli zeri. Dato che una partizione criptata si suppone essere indistinguibile da dati casuali, la mancanza di dati casuali su di un disco sovrascritto con degli zeri rende il disco criptato un facile bersaglio per la cripto analisi.

Ripartizionare o riformattare un disco usato rimuove solamente la struttura del file system che serve per identificare dove fisicamente sono collocati i dati, ma lascia i dati intatti sul disco. Sarà relativamente semplice utilizzando programmi di [recupero file](/index.php/File_recovery "File recovery") accedere ai dati rimasti. Quindi i dischi dovrebbero essere sovrascritti in modo sicuro con dati casuali prima di effettuare la cifratura per evitare il recupero dei dati.

Nel decidere quale metodo utilizzare per la cancellazione sicura del disco, notare che non sarà necessario eseguirlo più di una volta fintanto che il disco viene utilizzato come disco criptato.

#### Usare un contenitore LUKS come generatore di numeri pseudo-casuali (alternativa)

Le [FAQ di cryptsetup](http://code.google.com/p/cryptsetup/wiki/FrequentlyAskedQuestions#5._Security_Aspects) menzionano una procedura molto semplice che consiste nell'utilizzare un volume dm-crypt esistente per cancellare tutto lo spazio libero accessibile sul disco sottostante. Questa procedura inoltre mira a proteggere contro la rilevazione dei pattern ripetuti utilizzati per la cancellazione.

 `# dd if=/dev/zero of=/dev/mapper/luks-container` 

##### Cancellare lo spazio libero con un file criptato dopo l'installazione

Il solito effetto può essere ottenuto creando su tutte le partizioni un file che le riempia completamente dopo che il sistema è stato installato, avviato e con tutte le partizioni criptate montate. Questo perché i dati criptati sono indistinguibili dai dati casuali.

```
# dd if=/dev/zero of=/file/su/contenitore-luks
# rm /file/su/contenitore-luks
```

Ovviamente sarà necessario ripetere il precedente processo per ogni contenitore criptato creato.

#### Cancellare i keyslot LUKS

```
#cryptsetup luksKillSlot *device* *numero_key_slot*

```

Questo cancellerà solamente un singolo keyslot.

#### Cancellare i LUKS header

Le partizioni formattate con dm-crypt/LUKS contengono un header contenete la cifratura e le opzioni utilizzate da `dm-mod` quando viene aperta la periferica. Dopo l'header iniziano i dati criptati. Quindi, quando si dismette un disco (ad esempio se si vende il PC, sostituzione del disco, eccetera) *potrebbe* essere sufficiente cancellare l'header della partizione, anziché sovrascrivere l'intero disco - che potrebbe essere un processo molto lungo.

Cancellando l'header LUKS verrà cancellata anche la chiave principale PBKDF2-criptata (AES), salts ed altre.

**Nota:** It is crucial to write to the LUKS encrypted partition (`/dev/sda**1**` in this example) and not directly to the disks device node. If you did set up encryption as a device-mapper layer on top of others, e.g. LVM on LUKS on RAID then write to RAID respectively.

Un header con un singolo keyslot di dimensione 256 bit di sarà grande 1024KB. E' consigliato di sovrascrivere inoltre i primi 4KB scritti da dm-crypt, quindi sarà necessario cancellare 1028KB. Che sono `1052672` Byte.

Per sovrascrivere con zero usare:

```
#head -c 1052672 /dev/zero > /dev/sda1; sync

```

Per chiavi lunghe 512 bit (ad esempio per aes-xts-plain con chiavi da 512 bit) l'header è grande 2MB.

In caso di dubbi, è meglio essere generosi e sovrascrivere i primi 10MB o all'incirca.

```
#dd if=/dev/zero of=/dev/sda1 bs=512 count=20480

```

**Nota:** Con una copia di backup dell'header i dati possono essere recuperati ma il filesystem sarà danneggiato in quanto i primi settori criptati sono stati sovrascritti. Consultare le sezioni seguenti su come creare un backup dei blocchi cruciali dell'header.

Quando si cancella l'header con dati casuali e l'header è seguito da dati criptati scritti sopra dati casuali, tutto ciò che resta saranno dati casuali.

#### Supporto per discard/TRIM per i dischi a stato solido (SSD)

Gli utenti con dischi a stato solido dovrebbero essere consapevoli che per default, il meccanismo di cifratura del kernel Linux *non* invierà i comandi TRIM dal filesystem al disco sottostante. Gli sviluppatori del device-mapper hanno chiarito che il supporto per TRIM non sarà mai abilitato per default sul device dm-crypt a causa di potenziali problemi di sicurezza.

Molti utenti vorranno comunque utilizzare TRIM sui propri dischi SSD criptati. Questo crea un minimo di dispersione di informazioni riguardo ai blocchi liberati, comunque sufficienti a determinare il filesystem utilizzato, in caso TRIM sia abilitato. Una immagine ed una discussione del problema derivante dall'attivazione di TRIM è disponibile nel [blog](http://asalor.blogspot.de/2011/08/trim-dm-crypt-problems.html) di uno sviluppatore di `cryptsetup`.

As a semi-tangential caveat, it is worth noting that because TRIM provides information to the disk firmware about which blocks contain data, encryption schemes that rely on plausible deniability, like TrueCrypt's hidden volumes, should never be used on a device that utilizes TRIM. This is probably also valid for TC containers within a LUKS encrypted device that uses TRIM.

Gli sviluppatori di TrueCrypt sconsigliano l'uso di qualsiasi volume TC su un volume che effettua tecniche wear-leveling per estendere la vita del disco; molte periferiche flash inclusi i dischi SSD e le USB flash, utilizzano obbligatoriamente il wear-leveling a livello firmware. I device LUKS sono probabilmente non vulnerabili ai problemi derivanti dal wear-leveling se l'intero device viene cancellato prima dell'inizializzazione della partizione LUKS. Consultare [questo articolo su trim](http://www.truecrypt.org/docs/?s=trim-operation) e [questo articolo sul wear-leveling](http://www.truecrypt.org/docs/?s=wear-leveling) per maggiori informazioni.

A partire dalla versione 3.1 di [linux](https://www.archlinux.org/packages/?name=linux), il supporto di dm-crypt per l'inoltro dei comandi TRIM può essere attivata sul device alla creazione oppure durante il mount tramite dmsetup. Il supporto per questa opzione è presente anche in [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) a partire dalla versione 1.4.0\. Per attivare il supporto durante l'avvio, sarà necessario aggiungere `:allow-discards` come opzione al `cryptdevice`. Un esempio di device con abilitato TRIM sarà simile a questa:

```
cryptdevice=/dev/mapper/root:root:allow-discards

```

Per le principali configurazioni del `cryptdevice` prima di `:allow-discards` consultare i paragrafi che seguono.

### Partizionamento

Dopo che il disco è stato sovrascritto in modo sicuro, è il momento di creare le partizioni e iniziare la configurazione del sistema criptato.

Ci sono diversi modi di creare partizioni sul disco:

*   Partizioni standard
*   [LVM](/index.php/LVM_(Italiano) "LVM (Italiano)")
*   [RAID](/index.php/RAID_(Italiano) "RAID (Italiano)")

LUKS è compatibile con sistemi che necessitano di LVM e/o RAID come con le partizioni standard che siano primarie, estese, e logiche.

#### Partizioni standard

Queste sono le partizioni con cui la maggior parte degli utenti avrà maggiore familiarità. Esse possono essere di tre tipi: partizioni primarie, partizioni estese e partizioni logiche.

	Partizioni primarie

	Sono le normali partizioni riconosciute dal BIOS. Possono esserne presenti fino a quattro in un partizionamento MBR.

	Partizioni estese

	Sono partizioni primarie che definiscono al loro interno altre partizioni. Le partizioni estese sono state create per ovviare il limite delle quattro partizioni primarie.

	Partizioni logiche

	Sono le partizioni definite nelle partizioni estese.

#### LVM: Logical Volume Manager

Il gestore di volumi logici(LVM) permette la creazione di gruppi di volumi per sistemi che richiedono complesse combinazioni di dischi multipli e partizioni che non si possono ottenere con le partizioni standard. LVM è spiegato più dettagliatamente nell'[articolo del Wiki di Arch Linux](/index.php/LVM_(Italiano) "LVM (Italiano)") che si consiglia di leggere prima di procedere con le istruzioni che seguiranno riguardanti la configurazione di LUKS con LVM.

**Tip:** Btrfs has a built-in [Subvolume-Feature](/index.php/Btrfs#Subvolumes "Btrfs") that fully replaces the need for LVM if no other filesystems are required. An encrypted swap is not possible this way and swap files are [not supported](https://btrfs.wiki.kernel.org/index.php/FAQ#Does_btrfs_support_swap_files.3F) by btrfs up to now.

##### LVM on LUKS

There is a growing preference towards logical volume management of LUKS encrypted physical media (LVM on LUKS). The deployment of LVM on LUKS is considered much more generalizable. In a LVM on LUKS scenario, the LUKS-partition has to be opened and mapped before LVM can access the underlaying setup volumes.

One reason for this is that using LUKS as the lowest level of infrastructure most closely approximates the deployment of physical disks with built-in hardware encryption. In that case, logical volume management would be layered on top of the hardware encryption - usage of LUKS would be superfluous.

##### LUKS on LVM

It is possible there may exist usage scenarios where encrypting logical volumes rather than physical disks is required (LUKS on LVM). A usage scenario for LUKS on LVM exists where utmost flexibility for assigning available diskspace or a mix of unencrypted and encrypted volumes is desired. Upon boot the LVM is setup and assigned before the LUKS-encrypted volumes are opened. In order to manage changes of volumes in a LUKS on LVM setup, both module layers' setup have to be taken into account, i.e. shrinking or expanding an encrypted volume has to include the resizing of the encrypted LUKS blockdevice to ensure integrity of it and the filesystem. That said, in simpler scenarios the usage of LVM may be superfluous.

#### Creare le partizioni sul disco

Le partizioni del disco vengono create utilizzando:

```
# cfdisk

```

Questo comando avvierà una interfaccia grafica per la creazione delle partizioni.

Ci sono due partizioni necessarie ad un sistema criptato:

	Il filesystem di root

	`**/**` sarà criptata e conterrà tutti i dati utente e di sistema (`/usr`, `/bin`, `/var`, `/home`, etc.)

	Una partizione di boot per l'avvio

	la partizione `**/boot**` *non* sarà criptata; il bootloader necessita di accedere alla cartella `/boot` da cui caricherà il ramdisk iniziale i moduli per la crittografia e quelli necessari per l'avvio del sistema che *sarà* criptato (consultare [mkinitcpio](/index.php/Mkinitcpio_(Italiano) "Mkinitcpio (Italiano)") per maggiori informazioni). Per questa ragione, è necessario che `/boot` risieda su di una propria partizione non criptata.

**Nota:** La partizione di swap è opzionale; può essere criptata con dm-crypt/LUKS. Consultare [Criptare la partizione di swap](#Criptare_la_partizione_di_swap) per maggiori informazioni.

##### Sistemi con singolo disco

A seconda delle necessità del sistema, possono essere create altre partizioni. Queste partizioni possono essere create individualmente a questo livello definendo partizioni primarie oppure estese/logiche. Comunque, se si intende utilizzare LVM, lo spazio rimasto dopo la creazione della partizione di `/boot` e quella di swap dovrebbe essere definito come una singola grande partizione che sarà suddivisa successivamente al livello LVM.

##### Sistemi con dischi multipli

Nei sistemi che utilizzano molteplici dischi, sono valide le opzioni elencate per un singolo disco. Dopo la creazione della partizione di `/boot` e la partizione di swap, il rimanente spazio libero può essere diviso in partizioni a questo livello oppure grandi partizioni possono definire tutto lo spazio libero per ogni singolo disco con lo scopo di suddividerle mediante LVM.

## Configurare LUKS

Questa sezione del Wiki l'uso della linea di comando per criptare manualmente il sistema utilizzando LUKS.

I passaggi necessari utilizzando l'installer grafico sono molto simili e possono essere trovati nella configurazione manuale del disco.

### Mappare le partizioni fisiche con LUKS

Una volta create le partizioni necessarie, sarà il momento di formattarle come partizioni LUKS e successivamente effettuarne il mount mediante il device mapper.

Quando viene creata una partizione LUKS deve essere associata ad una chiave. La chiave verrà utilizzata per sbloccare l'header della partizione criptata con LUKS.

Una chiave può essere:

*   Una parola d'ordine(Passphrase)
*   Un file chiave(Keyfile)

Sarà possibile definire fino ad 8 differenti chiavi per ogni partizione LUKS. Questo permette all'utente di creare chiavi di accesso per effettuare i backup. Inoltre una chiave differente può essere creata per garantire l'accesso alla partizione ad un utente e successivamente revocata senza bisogno di criptare nuovamente la partizione.

#### Usare LUKS per formattare partizioni con la parola d'ordine

**Nota:** Usare una parola d'ordine in `/etc/crypttab` per decriptare partizioni LUKS automaticamente è [deprecato.](http://www.mail-archive.com/arch-projects@archlinux.org/msg02115.html)

Cryptsetup viene utilizzato per formattare, effettuare il mount e l'umount delle partizioni criptate.