Articoli correlati

*   [Disk Encryption (Italiano)](/index.php/Disk_Encryption_(Italiano) "Disk Encryption (Italiano)")
*   [Removing System Encryption](/index.php/Removing_System_Encryption "Removing System Encryption")

Questo articolo si concentra su come configurare un sistema completamente crittografato su Arch Linux, usando dm-crypt con LUKS.

**dm-crypt** è il device-mapper standard per le funzionalità di crittografia fornito dal kernel Linux. Può essere utilizzato direttamente da chi desidera avere un completo controllo degli aspetti del partizionamento e della gestione delle chiavi.

**LUKS** è un comodo strato aggiuntivo il quale archivia tutte le informazioni necessarie alla configurazione di dm-crypt sul disco stesso e si occupa anche della gestione delle partizioni e delle chiavi nel tentativo di facilitarne l’uso.

Per maggiori dettagli sui paragoni tra dm-crypt+LUKS e gli altri metodi di crittografia, consultare [la tavola comparativa](/index.php/Disk_encryption#Comparison_table "Disk encryption").

## Contents

*   [1 Avvertenze](#Avvertenze)
*   [2 Configurazione iniziale](#Configurazione_iniziale)
    *   [2.1 Panoramica e preparazione](#Panoramica_e_preparazione)
    *   [2.2 Cancellazione sicura del/degli hard disk](#Cancellazione_sicura_del.2Fdegli_hard_disk)
        *   [2.2.1 Usare un contenitore LUKS come generatore di numeri pseudo-casuali (alternativa)](#Usare_un_contenitore_LUKS_come_generatore_di_numeri_pseudo-casuali_.28alternativa.29)
            *   [2.2.1.1 Cancellare lo spazio libero con un file criptato dopo l'installazione](#Cancellare_lo_spazio_libero_con_un_file_criptato_dopo_l.27installazione)
        *   [2.2.2 Cancellare i keyslot LUKS](#Cancellare_i_keyslot_LUKS)
        *   [2.2.3 Cancellare i LUKS header](#Cancellare_i_LUKS_header)
        *   [2.2.4 Supporto per discard/TRIM per i dischi a stato solido (SSD)](#Supporto_per_discard.2FTRIM_per_i_dischi_a_stato_solido_.28SSD.29)
    *   [2.3 Partizionamento](#Partizionamento)
        *   [2.3.1 Partizioni standard](#Partizioni_standard)
        *   [2.3.2 LVM: Logical Volume Manager](#LVM:_Logical_Volume_Manager)
            *   [2.3.2.1 LVM on LUKS](#LVM_on_LUKS)
            *   [2.3.2.2 LUKS on LVM](#LUKS_on_LVM)
        *   [2.3.3 Creare le partizioni sul disco](#Creare_le_partizioni_sul_disco)
            *   [2.3.3.1 Sistemi con singolo disco](#Sistemi_con_singolo_disco)
            *   [2.3.3.2 Sistemi con dischi multipli](#Sistemi_con_dischi_multipli)
*   [3 Configurare LUKS](#Configurare_LUKS)
    *   [3.1 Mappare le partizioni fisiche con LUKS](#Mappare_le_partizioni_fisiche_con_LUKS)
        *   [3.1.1 Usare LUKS per formattare partizioni con la parola d'ordine](#Usare_LUKS_per_formattare_partizioni_con_la_parola_d.27ordine)
        *   [3.1.2 Using LUKS to Format Partitions with a Keyfile](#Using_LUKS_to_Format_Partitions_with_a_Keyfile)
        *   [3.1.3 Adding Additional Passphrases or Keyfiles to a LUKS Encrypted Partition](#Adding_Additional_Passphrases_or_Keyfiles_to_a_LUKS_Encrypted_Partition)
    *   [3.2 Storing the Key File](#Storing_the_Key_File)
        *   [3.2.1 External Storage on a USB Drive](#External_Storage_on_a_USB_Drive)
            *   [3.2.1.1 Preparation for Persistent block device naming](#Preparation_for_Persistent_block_device_naming)
            *   [3.2.1.2 Persistent symlinks](#Persistent_symlinks)
            *   [3.2.1.3 Persistent udev rule](#Persistent_udev_rule)
        *   [3.2.2 Generating the keyfile](#Generating_the_keyfile)
        *   [3.2.3 Storing the keyfile](#Storing_the_keyfile)
        *   [3.2.4 Configuration of initcpio](#Configuration_of_initcpio)
        *   [3.2.5 Storing the key as a plain (visible) file](#Storing_the_key_as_a_plain_.28visible.29_file)
        *   [3.2.6 Storing the key between MBR and 1st partition](#Storing_the_key_between_MBR_and_1st_partition)
    *   [3.3 Encrypting the Swap partition](#Encrypting_the_Swap_partition)
        *   [3.3.1 Without suspend-to-disk support](#Without_suspend-to-disk_support)
        *   [3.3.2 With suspend-to-disk support](#With_suspend-to-disk_support)
        *   [3.3.3 Using a swap file for suspend-to-disk support](#Using_a_swap_file_for_suspend-to-disk_support)
*   [4 Installing the system](#Installing_the_system)
    *   [4.1 Prepare hard drive for Arch Install Scripts](#Prepare_hard_drive_for_Arch_Install_Scripts)
    *   [4.2 Configure initramfs](#Configure_initramfs)
    *   [4.3 Kernel parameter configuration of the bootloader](#Kernel_parameter_configuration_of_the_bootloader)
        *   [4.3.1 GRUB2](#GRUB2)
        *   [4.3.2 Syslinux](#Syslinux)
        *   [4.3.3 GRUB Legacy](#GRUB_Legacy)
        *   [4.3.4 LILO](#LILO)
    *   [4.4 Fstab](#Fstab)
*   [5 Remote unlocking of the root (or other) partition](#Remote_unlocking_of_the_root_.28or_other.29_partition)
*   [6 Backup the cryptheader](#Backup_the_cryptheader)
    *   [6.1 Backup](#Backup)
        *   [6.1.1 Using cryptsetup](#Using_cryptsetup)
        *   [6.1.2 Manually](#Manually)
    *   [6.2 Restore](#Restore)
        *   [6.2.1 Using cryptsetup](#Using_cryptsetup_2)
        *   [6.2.2 Manually](#Manually_2)
*   [7 Encrypting a loopback filesystem](#Encrypting_a_loopback_filesystem)
    *   [7.1 Preparation and mapping](#Preparation_and_mapping)
    *   [7.2 Encrypt using a key-file](#Encrypt_using_a_key-file)
    *   [7.3 Resizing the loopback filesystem](#Resizing_the_loopback_filesystem)
*   [8 Encrypting a LVM setup](#Encrypting_a_LVM_setup)
    *   [8.1 LVM with Arch Linux Installer (>2009.08 <2012.07.15)](#LVM_with_Arch_Linux_Installer_.28.3E2009.08_.3C2012.07.15.29)
        *   [8.1.1 The partition and filesystem choice](#The_partition_and_filesystem_choice)
        *   [8.1.2 The configuration stage](#The_configuration_stage)
    *   [8.2 Applying this to a non-root partition](#Applying_this_to_a_non-root_partition)
    *   [8.3 LVM and dm-crypt manually (short version)](#LVM_and_dm-crypt_manually_.28short_version.29)
        *   [8.3.1 Notes](#Notes)
        *   [8.3.2 Partitioning scheme](#Partitioning_scheme)
        *   [8.3.3 The commands](#The_commands)
        *   [8.3.4 Install Arch Linux](#Install_Arch_Linux)
        *   [8.3.5 Configuration](#Configuration)
            *   [8.3.5.1 /etc/rc.conf](#.2Fetc.2Frc.conf)
            *   [8.3.5.2 /etc/mkinitcpio.conf](#.2Fetc.2Fmkinitcpio.conf)
            *   [8.3.5.3 /boot/grub/menu.lst](#.2Fboot.2Fgrub.2Fmenu.lst)
            *   [8.3.5.4 /etc/fstab](#.2Fetc.2Ffstab)
            *   [8.3.5.5 /etc/crypttab](#.2Fetc.2Fcrypttab)
        *   [8.3.6 After rebooting](#After_rebooting)
            *   [8.3.6.1 The commands](#The_commands_2)
            *   [8.3.6.2 /etc/crypttab](#.2Fetc.2Fcrypttab_2)
            *   [8.3.6.3 /etc/fstab](#.2Fetc.2Ffstab_2)
    *   [8.4 / on LVM on LUKS](#.2F_on_LVM_on_LUKS)
*   [9 Using GPG or OpenSSL Encrypted Keyfiles](#Using_GPG_or_OpenSSL_Encrypted_Keyfiles)
*   [10 Securing the unencrypted boot partition](#Securing_the_unencrypted_boot_partition)
*   [11 Automount user homes on login](#Automount_user_homes_on_login)
*   [12 Resources](#Resources)

## Avvertenze

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

Usage:

```
# cryptsetup [OPTION...] <action> <action-specific>

```

Example:

```
# cryptsetup --cipher aes-xts-plain64 --key-size 512 --hash sha512 --iter-time 5000 --use-random --verify-passphrase luksFormat <device> 

```

Common options used with luksFormat:

| Available options | Cryptsetup defaults | Comment | Example | Comment |
| --cipher, -c | `aes-cbc-essiv:sha256` | Use the AES-[cipher](/index.php/Disk_encryption#Ciphers_and_modes_of_operation "Disk encryption") with [CBC/ESSIV](https://en.wikipedia.org/wiki/Disk_encryption_theory#Cipher-block_chaining_.28CBC.29 "wikipedia:Disk encryption theory"). | `aes-xts-plain64` | [XTS](https://en.wikipedia.org/wiki/Disk_encryption_theory#XEX-based_tweaked-codebook_mode_with_ciphertext_stealing_.28XTS.29 "wikipedia:Disk encryption theory"). For volumes >2TiB use `aes-xts-plain64` (requires kernel >= 2.6.33). |
| --key-size, -s | `256` | The cipher is used with 256 bit key-size. | `512` | [XTS splits the supplied key](https://en.wikipedia.org/wiki/XEX-TCB-CTS#Issues_with_XTS "wikipedia:XEX-TCB-CTS") into fraternal twins. For an effective AES-256 the XTS key-size must be `512`. |
| --hash, -h | `sha1` | Hash algorithm used for [PBKDF2](/index.php/Disk_encryption#Keys.2C_keyfiles_and_passphrases "Disk encryption"). | `sha512` |
| --iter-time, -i | `1000` | Number of milliseconds to spend with PBKDF2 passphrase processing. | `5000` | Using a hash stronger than sha1 results in less iterations if iter-time is not increased. |
| --use-random | `--use-**u**random` | /dev/u[random](/index.php/Random "Random") is used as randomness source for the (long-term) volume master key. | `--use-random` | Avoid generating an insecure master key if low on entropy. Will block if the entropy pool is used up. |
| --verify-passphrase, -y | Yes | Default only for luksFormat and luksAddKey. | - | No need to type for archlinux at the moment. |

When comparing the defaults with the example, it has to be taken into account that a number of the options stated affect system performance just for creating the initial crypt-blockdevice or opening it, but not the disk-io operations when the system is running. A full list of options `cryptsetup` accepts can be found in the [manpage](http://www.dsm.fordham.edu/cgi-bin/man-cgi.pl?topic=cryptsetup).

In the following examples for creating LUKS partitions, we will use the AES cipher in XTS mode; at present this is most generally used preferred cipher. Other ciphers can be used with cryptsetup, and details about them can be found here: [Wikipedia:Block_cipher](https://en.wikipedia.org/wiki/Block_cipher "wikipedia:Block cipher")

**Formatting LUKS Partitions**

First of all make sure the device mapper kernel module is loaded by executing the following: `# modprobe dm_mod`

In order to format a desired partition as an encrypted LUKS partition execute:

 `# cryptsetup -c *cipher* -y -s *key_size* luksFormat /dev/*partition_name*` 
```
Enter passphrase: *password*
Verify passphrase: *password*

```

Check results:

```
# cryptsetup luksDump /dev/*drive*

```

This should be repeated for all partitions except for `/boot` and possibly swap.

The example below will create an encrypted root partition using the AES cipher in XTS mode (generally referred to as *XTS-AES*).

 `# cryptsetup -c aes-xts-plain -y -s 512 luksFormat /dev/sda2` 
**Note:** If hibernation usage is planned, swap must be encrypted in this fashion; otherwise, if hibernation is not a planned feature for the system, encrypting the swap file will be performed in a alternative manner.

**Warning:** Irrespective of the chosen partitioning method, the `/boot` partition must remain separate and unencrypted in order to load the kernel and boot the system.

**Unlocking/Mapping LUKS Partitions with the Device Mapper**

Once the LUKS partitions have been created it is time to unlock them.

The unlocking process will map the partitions to a new device name using the device mapper. This alerts the kernel that `/dev/*partition*` is actually an encrypted device and should be addressed through LUKS using the `/dev/mapper/*name*` so as not to overwrite the encrypted data. To guard against accidental overwriting, read about the possibilities to [backup the cryptheader](/index.php/LUKS#Backup_the_cryptheader "LUKS") after finishing setup.

In order to open an encrypted LUKS partition execute:

 `# cryptsetup luksOpen /dev/*partition_name* *device-mapper_name*` 
```
Enter any LUKS passphrase: *password*
key slot 0 unlocked.
Command successful.
```

Usually the device mapped name is descriptive of the function of the partition that is mapped, example:

	cryptsetup luksOpen /dev/sda2 swap

	Once opened, the swap partition device address would be `/dev/mapper/swap` instead of `/dev/sda2`.

	cryptsetup luksOpen /dev/sda3 root

	Once opened, the root partition device address would be `/dev/mapper/root` instead of `/dev/sda3`.

	cryptsetup luksOpen /dev/sda3 lvmpool (alternate)

	For setting up [LVM](#LVM:_Logical_Volume_Manager) ontop the encryption layer the device file for the decrypted volume group would be anything like `/dev/mapper/lvmpool` instead of `/dev/sda3`. LVM will then give additional names to all logical volumes created, e.g. `/dev/mapper/lvmpool-root` and `/dev/mapper/lvmpool-swap`.

In order to write encrypted data into the partition it must be accessed through the device mapped name.

**Note:** Since `/boot` is not encrypted, it does not need a device mapped name and will be addressed as `/dev/sda1`.

#### Using LUKS to Format Partitions with a Keyfile

**Note:** This section describes using a plaintext keyfile, if you want to encrypt your keyfile giving you two factor authentication see [Section 9](/index.php/System_Encryption_with_LUKS#Using_GPG_or_OpenSSL_Encrypted_Keyfiles "System Encryption with LUKS") for details, but please still read this section.

**What is a Keyfile?**

A keyfile is any file in which the data contained within it is used as the passphrase to unlock an encrypted volume. Therefore if these files are lost or changed, decrypting the volume will no longer be possible.

**Tip:** Define a passphrase in addition to the keyfile for backup access to encrypted volumes in the event the defined keyfile is lost or changed.

**Why use a Keyfile?**

There are many kinds of keyfile. Each type of keyfile used has benefits and disadvantages summarized below:

	**keyfile.passphrase:**

	this is my passphrase I would have typed during boot but I have placed it in a file instead

This is a keyfile containing a simple passphrase. The benefit of this type of keyfile is that if the file is lost the data it contained is known and hopefully easily remembered by the owner of the encrypted volume. However the disadvantage is that this does not add any security over entering a passphrase during the initial system start.

	**keyfile.randomtext:**

	fjqweifj830149-57 819y4my1- 38t1934yt8-91m 34co3;t8y;9p3y-

This is a keyfile containing a block of random characters. The benefit of this type of keyfile is that it is much more resistant to dictionary attacks than a simple passphrase. An additional strength of keyfiles can be utilized in this situation which is the length of data used. Since this is not a string meant to be memorized by a person for entry, it is trivial to create files containing thousands of random characters as the key. The disadvantage is that if this file is lost or changed, it will most likely not be possible to access the encrypted volume without a backup passphrase.

	**keyfile.binary:**

	where any binary file, images, text, video could be chosen as the keyfile

This is a binary file that has been defined as a keyfile. When identifying files as candidates for a keyfile, it is recommended to choose files that are relatively static such as photos, music, video clips. The benefit of these files is that they serve a dual function which can make them harder to identify as keyfiles. Instead of having a text file with a large amount of random text, the keyfile would look like a regular image file or music clip to the casual observer. The disadvantage is that if this file is lost or changed, it will most likely not be possible to access the encrypted volume without a backup passphrase. Additionally, there is a theoretical loss of randomness when compared to a randomly generated text file. This is due to the fact that images, videos and music have some intrinsic relationship between neighboring bits of data that does not exist for a text file. However this is controversial and has never been exploited publicly.

**Creating a Keyfile with Random Characters**

Here `dd` is used to generate a keyfile of 2048 bits of random characters.

```
# dd if=/dev/urandom of=mykeyfile bs=512 count=4

```

The usage of `dd` is similar to initially wiping the volume with random data prior to encryption.

**Warning:** Do not use [badblocks](/index.php/Badblocks "Badblocks") here. It only generate a random pattern which just repeats its randomness over and over again.

**Creating a new LUKS encrypted partition with a Keyfile**

When creating a new LUKS encrypted partition, a keyfile may be associated with the partition on its creation using:

```
# cryptsetup -c <desired cipher> -s <key size> luksFormat /dev/<volume to encrypt> **/path/to/mykeyfile**

```

This is accomplished by appending the bold area to the standard cryptsetup command which defines where the keyfile is located.

#### Adding Additional Passphrases or Keyfiles to a LUKS Encrypted Partition

LUKS supports the association of up to 8 keyslots with any single encrypted volume. Keyslots can be either keyfiles or passphrases.

Once an encrypted partition has been created, the initial keyslot 0 is created. Additional keyslots are numbered from 1 to 7.

Adding new keyslots is accomplished using cryptsetup with the `luksAddKey` action.

Don't forget wiping unused keyslots with `luksKillSlot` as described in [#Wipe LUKS keyslots](#Wipe_LUKS_keyslots).)

 `# cryptsetup luksAddKey /dev/mapper/*device* (/path/to/additionalkeyfile)` 
```
Enter any passphrase:
Enter new passphrase for key slot:
Verify passphrase:
```

Where `*device*` is the volume containing the LUKS header to wich the new keyslot is added. This works on header backup files as well.

If `/path/to/additionalkeyfile` is given, cryptsetup will add a new keyslot for additionalkeyfile. Otherwise a new passphrase will be prompted for twice.

For adding keyslots cryptsetup has to decrypt the master key from an existing keyslot so it first asks for "any passphrase" (of an existing keyslot).

For getting the master key from an existing keyfile keyslot the `--key-file` or `-d` option followed by the "old" keyfile will try to unlock all available keyfile keyslots.

```
# cryptsetup luksAddKey /dev/mapper/*device* (/path/to/additionalkeyfile) -d /path/to/keyfile

```

### Storing the Key File

#### External Storage on a USB Drive

##### Preparation for Persistent block device naming

For reading the file from an external storage device it is very convenient to access it through udev's [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") features and not by ordinary device nodes like `/dev/sdb1` whose naming depends on the order in which devices are plugged in. So in order to assure that the `encrypt` HOOK in the initcpio finds your keyfile, you must use a permanent device name.

##### Persistent symlinks

A quick method (as opposed to setting up a [udev](/index.php/Udev "Udev") rule) for doing so involves referencing the right partition by its UUID, id (based on hardware info and serial number) or filesystem label.

Plug the device in and print every file name under /dev/disk:

 `#ls -lR /dev/disk/` 
```
/dev/disk/:
total 0
drwxr-xr-x 2 root root 180 Feb 12 10:11 by-id
drwxr-xr-x 2 root root  60 Feb 12 10:11 by-label
drwxr-xr-x 2 root root 100 Feb 12 10:11 by-path
drwxr-xr-x 2 root root 180 Feb 12 10:11 by-uuid

/dev/disk/by-id:
total 0
lrwxrwxrwx 1 root root  9 Feb 12 10:11 usb-Generic_STORAGE_DEVICE_000000014583-0:0 -> ../../sdb
lrwxrwxrwx 1 root root 10 Feb 12 10:11 usb-Generic_STORAGE_DEVICE_000000014583-0:0-part1 -> ../../sdb1

/dev/disk/by-label:
total 0
lrwxrwxrwx 1 root root 10 Feb 12 10:11 Keys -> ../../sdb1

/dev/disk/by-path:
total 0
lrwxrwxrwx 1 root root  9 Feb 12 10:11 pci-0000:00:1d.7-usb-0:1:1.0-scsi-0:0:0:0 -> ../../sdb
lrwxrwxrwx 1 root root 10 Feb 12 10:11 pci-0000:00:1d.7-usb-0:1:1.0-scsi-0:0:0:0-part1 -> ../../sdb1

/dev/disk/by-uuid:
total 0
lrwxrwxrwx 1 root root 10 Feb 12 10:11 baa07781-2a10-43a7-b876-c1715aba9d54 -> ../../sdb1
```

**UUID**

Using the filesystem UUID for persistent block device naming is considered very reliable. Filesystem UUIDs are stored in the filesystem itself, meaning that the UUID will be the same if you plug it into any other computer, and that a dd backup of it will always have the same UUID since dd does a bitwise copy.

The right device node for what is now `/dev/sdb1` will always get symlinked by `/dev/disk/by-uuid/baa07781-2a10-43a7-b876-c1715aba9d54`. Symlinks can be used in the bootloaders "cryptkey" kernel option or anywhere else.

For legacy filesystems like FAT the UUID will be much shorter but collision is still unlikely to happen if not mounting many different FAT filesystems at once.

**Label**

In the following example a FAT partition is labeled as "Keys" and will always get symlinked by `/dev/disk/by-label/Keys`:

```
#mkdosfs -n >volume-name< /dev/sdb1

```
 `#blkid -o list` 
```
device     fs_type label    mount point    UUID
-------------------------------------------------------
/dev/sdb1  vfat    Keys     (not mounted)  221E-09C0
```

**Note:** If you plan to store the keyfile between [MBR and the 1st partition](#Storing_the_key_between_MBR_and_1st_partition) you **cannot use this method**, since it only allows access to the partitions (`sdb1`, `sdb2`, ...) but not to the USB device (`sdb`) itself. Use something like `/dev/disk/by-id/*` or alternatively create a udev rule as described in the following section.

##### Persistent udev rule

Optionally you may choose to set up your flash drive with a [udev](/index.php/Udev "Udev") rule. There is some documentation in the Arch wiki about that already; if you want more in-depth, structural info, read [this guide](http://reactivated.net/writing_udev_rules.html). Here is quickly how it goes.

Get the serial number from your USB flash drive:

```
lsusb -v | grep -A 5 Vendor

```

Create a udev rule for it by adding the following to a file in `/etc/udev/rules.d/`, such as `8-usbstick.rules`:

```
KERNEL=="sd*", ATTRS{serial}=="$SERIAL", SYMLINK+="$SYMLINK%n"

```

Replace `$SYMLINK` and `$SERIAL` with their respective values. `%n` will expand to the partition (just like sda is subdivided into sda1, sda2, ...). You do not need to go with the 'serial' attribute. If you have a custom rule of your own, you can put it in as well (e.g. using the vendor name).

Rescan your sysfs:

```
udevadm trigger

```

Now check the contents of `/dev`:

```
ls /dev

```

It should show your device with your desired name.

#### Generating the keyfile

Optionally you can mount a tmpfs for storing the temporary keyfile.

```
# mkdir ./mytmpfs
# mount tmpfs ./mytmpfs -t tmpfs -o size=32m
# cd ./mytmpfs

```

The advantage is that it resides in RAM and not on a physical disk, so after unmounting your keyfile is securly gone. So copy your keyfile to some place you consider as secure before unmounting. If you are planning to store the keyfile as a plain file on your USB device, you can also simply execute the following command in the corresponding directory, e.g. `/media/sdb1`

The keyfile can be of arbitrary content and size. We will generate a random temporary keyfile of 2048 bytes:

```
# dd if=/dev/urandom of=secretkey bs=512 count=4

```

If you stored your temporary keyfile on a physical storage device, remember to not just (re)move the keyfile later on, but use something like

```
cp secretkey /destination/path
shred --remove --zero secretkey

```

to securely overwrite it. For overaged filesystems like FAT or ext2 this will suffice while in the case of journaling filesystems, flash memory hardware and other cases it is highly recommended to [wipe the entire device](/index.php/Securely_wipe_disk "Securely wipe disk") or at least the keyfiles partition.

Add a keyslot for the temporary keyfile to the LUKS header:

 `# cryptsetup luksAddKey /dev/sda2 secretkey` 
```
Enter any LUKS passphrase:
key slot 0 unlocked.
Command successful.
```

#### Storing the keyfile

To store the key file, you have two options. The first is less risky than the other, but perhaps a bit more secure (if you consider security by obscurity as more secure). In any case you have to do some further configuration, if not already done above.

#### Configuration of initcpio

You have to add two extra modules in your `/etc/mkinitcpio.conf`, one for the drive's file system and one for the codepage. Further if you created a udev rule, you should tell `mkinitcpio` about it:

```
MODULES="ata_generic ata_piix nls_cp437 vfat"
FILES="/etc/udev/rules.d/8-usbstick.rules"

```

In this example it is assumed that you use a FAT formatted USB drive. Replace those module names if you use another file system on your USB stick (e.g. ext2) or another codepage. Users running the stock Arch kernel should stick to the codepage mentioned here.

Additionally, insert the `usb` hook somewhere before the `encrypt` hook.

```
HOOKS="... **usb** encrypt ... filesystems ..."

```

If you have a non-US keyboard, it might prove useful to load your keyboard layout before you are prompted to enter the password to unlock the root partition at boot. For this, you will need the `keymap` hook before `encrypt`.

Generate a new image (maybe you should backup a copy of your old `/boot/initramfs-linux.img` first):

```
# mkinitcpio -p linux

```

#### Storing the key as a plain (visible) file

Be sure to choose a plain name for your key – a bit of 'security through obscurity' is always nice ;-). Avoid using dotfiles (hidden files) – the `encrypt` hook will fail to find the keyfile during the boot process.

You have to add a kernel parameter in your `/boot/grub/menu.lst` ([GRUB](/index.php/GRUB "GRUB")). It should look something like this:

```
kernel /vmlinuz-linux cryptdevice=/dev/sda3:root root=/dev/mapper/root ro cryptkey=/dev/usbstick:vfat:/secretkey

```

This assumes `/dev/usbstick` is the FAT partition of your choice. Replace it with `/dev/disk/by-...` or whatever your device is.

That is all, reboot and have fun!

#### Storing the key between MBR and 1st partition

We will write the key directly between the Master Boot Record (MBR) and the first partition.

**Warning:** You should only follow this step if you know what you are doing -- **it can cause data loss and damage your partitions or MBR on the stick!**

If you have a bootloader installed on your drive you have to adjust the values. E.g. [GRUB](/index.php/GRUB "GRUB") needs the first 16 sectors (actually, it depends on the type of the file system, so do not rely on this too much), so you would have to replace `seek=4` with `seek=16`; otherwise you would overwrite parts of your GRUB installation. When in doubt, take a look at the first 64 sectors of your drive and decide on your own where to place your key.

*Optional* If you do not know if you have enough free space before the first partition, you can do

```
dd if=/dev/usbstick of=64sectors bs=512 count=64   # gives you copy of your first 64 sectors
hexcurse 64sectors                                 # determine free space
xxd 64sectors | less                               # alternative hex viewer

```

Write your key to the disk:

```
dd if=secretkey of=/dev/usbstick bs=512 seek=4

```

If everything went fine you can now overwrite and delete your temporary secretkey as noted above. You should not simply use `rm` as the keyfile would only be unlinked from your filesystem and be left physically intact.

Now you have to add a kernel parameter in your `/boot/grub/menu.lst` file (GRUB); it should look something like this:

```
 kernel /vmlinuz-linux cryptdevice=/dev/sda3:root root=/dev/mapper/root ro cryptkey=/dev/usb:2048:2048

```

Format for the `cryptkey` option:

```
cryptkey=BLOCKDEVICE:OFFSET:SIZE

```

`OFFSET` and `SIZE` match in this example, but this is just coincidence - they can differ (and often will). An other possible example could be

```
kernel /vmlinuz-linux cryptdevice=/dev/sda3:root root=/dev/mapper/root ro cryptkey=/dev/usb:8192:2048

```

That is all, reboot and have fun! And look if your partitions still work after that ;-).

### Encrypting the Swap partition

#### Without suspend-to-disk support

In systems where suspend to disk is not a desired feature, it is possible to create a swap file that will have a random master key with each boot. This is accomplished by using dm-crypt directly without LUKS extensions.

The `/etc/crypttab` is well commented and you can basically just uncomment the swap line and change device to a persistent symlink.

 `/etc/crypttab` 
```
# name       device         password              options
# swap         /dev/hdx4        /dev/urandom            swap,cipher=aes-cbc-essiv:sha256,size=256
```

Where:

	name

	Represents the name (`/dev/mapper/*name*`) to list in /etc/fstab.

	device

	Should be the symlink to the actual partition's device file.

	password

	`/dev/urandom` sets the dm-crypt master key to be randomized on every volume recreation.

	options

	The `swap` option runs mkswap after cryptographic's are setup.

**Warning:** You should use persistent block device naming (in example ID's) for device because if there are multiple hard drives installed in the system, their naming order (sda, sdb,...) can occasionally be scrambled upon boot and thus the swap would be created over a valuable file system, destroying its content.

Persistent block device naming is implemented with simple symlinks. Using UUID's or filesystem-labels is not possible as plain dm-crypt writes only encrypted data without a persistent header like LUKS. If you are not familar with one of the directories under `/dev/disk/` read on in the section on [#Preparation for Persistent block device naming](#Preparation_for_Persistent_block_device_naming)

 `#ls -l /dev/disk/*/* | grep sda2`  `lrwxrwxrwx 1 root root 10 Oct 12 16:54 /dev/disk/by-id/ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-part2 -> ../../sda2` 

Example line for the `/dev/sda2` symlink from above:

 `/etc/crypttab` 
```
# name                      device                                   password     options
  swap  /dev/disk/by-id/ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-part2  /dev/urandom   swap,cipher=aes-cbc-essiv:sha256,size=256
```

This will map `/dev/sda2` to `/dev/mapper/swap` as a swap partition that can be added in `/etc/fstab` like a normal swap.

If the partition chosen for swap was previously a LUKS partition, crypttab will not overwrite the partition to create a swap partition. This is a safety measure to prevent data loss from accidental mis-identification of the swap partition in crypttab. In order to use such a partition the [LUKS header must be overwritten](#Wipe_LUKS_header) once.

#### With suspend-to-disk support

To be able to resume after suspending the computer to disk (hibernate), it is required to keep the swap filesystem intact. Therefore, it is required to have a pre-existent LUKS swap partition, which can be stored on the disk or input manually at startup. Because the resume takes place before `/etc/crypttab` can be used, it is required to create a hook in `/etc/mkinitcpio.conf` to open the swap LUKS device before resuming.

If you want to use a partition which is currently used by the system, you have to disable it first:

```
# swapoff /dev/*device*

```

Also make sure you remove any line in `/etc/crypttab` pointing to this device.

A simple way to realize encrypted swap with suspend-to-disk support is by using [LVM](/index.php/LVM "LVM") ontop the encryption layer, so one encrypted partition can contain infinite filesystems (root, swap, home, ...). Follow the instructions on [#Encrypting a LVM setup](#Encrypting_a_LVM_setup).

The following setup has the disadvantage of having to insert an additional passphrase for the swap partition manually on every boot.

**Warning:** Do not use this setup with a key file. Please read about the issue reported [here](/index.php/Talk:System_Encryption_with_LUKS_for_dm-crypt#Suspend_to_disk_instructions_are_insecure "Talk:System Encryption with LUKS for dm-crypt")

To format the encrypted container for the swap partition, follow steps similar to those described in [#Configurare LUKS](#Configurare_LUKS) above and create keyslot for a user-memorizable passphrase.

Open the partition in `/dev/mapper`:

```
# cryptsetup luksOpen /dev/*device* swapDevice

```

Create a swap filesystem inside the mapped partition:

```
# mkswap /dev/mapper/swapDevice

```

Now you have to create a hook to open the swap at boot time.

*   Create a hook file containing the open command:

 `/lib/initcpio/hooks/openswap` 
```
 # vim: set ft=sh:
 run_hook ()
 {
     cryptsetup luksOpen /dev/<device> swapDevice
 }

```

**Note:** If swap is on a Solid State Disk (SSD) and Discard/TRIM is desired the option `--allow-discards` has to get added to the cryptsetup line in the openswap hook above. See [Discard/TRIM support for solid state disks (SSD)](#Discard.2FTRIM_support_for_solid_state_disks_.28SSD.29) or [SSD](/index.php/SSD "SSD") for more information on discard. Additionally you have to add the mount option 'discard' to your fstab entry for the swap device.

*   Then create and edit the hook setup file:

 `/lib/initcpio/install/openswap` 
```
 # vim: set ft=sh:
 build ()
 {
     add_runscript
 }
 help ()
 {
 cat<<HELPEOF
   This opens the swap encrypted partition /dev/<device> in /dev/mapper/swapDevice
 HELPEOF
 }

```

*   Add the hook `openswap` in the `HOOKS` array in `/etc/mkinitcpio.conf`, before `filesystem` but after `encrypt`. Do not forget to add the `resume` hook after `openswap`.

```
HOOKS="... encrypt openswap resume filesystems ..."

```

*   Regenerate the boot image:

```
# mkinitcpio -p linux

```

*   Add the mapped partition to `/etc/fstab` by adding the following line:

```
/dev/mapper/swapDevice swap swap defaults 0 0

```

*   Set up your system to resume from `/dev/mapper/swapDevice`. For example, if you use [GRUB](/index.php/GRUB "GRUB") with kernel hibernation support, add `resume=/dev/mapper/swapDevice` to the kernel line in `/boot/grub/menu.lst`. A line with encrypted root and swap partitions can look like this:

```
kernel /vmlinuz-linux cryptdevice=/dev/sda2:rootDevice root=/dev/mapper/rootDevice resume=/dev/mapper/swapDevice ro

```

At boot time, the `openswap` hook will open the swap partition so the kernel resume may use it. If you use special hooks for resuming from hibernation, make sure they are placed **after** `openswap` in the `HOOKS` array. Please note that because of initrd opening swap, there is no entry for swapDevice in `/etc/crypttab` needed in this case.

#### Using a swap file for suspend-to-disk support

*   Choose a mapped partition (e.g. `/dev/mapper/rootDevice`) whose mounted filesystem (e.g. `/`) contains enough free space to hold the entire contents of your system's RAM. For example, if your system has 4 GiB RAM, then you need at least that much free space on the mounted filesystem of your chosen mapped partition for the swap file.

*   [Create the swap file](/index.php/HOW_TO:_Create_swap_file#Swap_file_creation "HOW TO: Create swap file") (e.g. `/swapfile`) inside the mounted filesystem of your chosen mapped partition. Be sure to activate it with `swapon` and also add it to your `/etc/fstab` file afterward.

*   Set up your system to resume from your chosen mapped partition. For example, if you use [GRUB](/index.php/GRUB "GRUB") with kernel hibernation support, add `resume=`*your chosen mapped partition* and `resume_offset=`*see calculation command below* to the kernel line in `/boot/grub/menu.lst`. A line with encrypted root partition can look like this:

```
kernel /vmlinuz-linux cryptdevice=/dev/sda2:rootDevice root=/dev/mapper/rootDevice resume=/dev/mapper/rootDevice resume_offset=123456789 ro

```

You can calculate the `resume_offset` of your swap file like this:

```
# filefrag -v /swapfile | awk '{if($1==0){print $3}}'

```

*   Add the `resume` hook to your `etc/mkinitcpio.conf` file and [rebuild the image](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") afterward:

```
HOOKS="... encrypt **resume** ... filesystems ..."

```

*   If you use a USB keyboard to enter your decryption password, then the `usbinput` module **must** appear in front of the `encrypt` hook, as shown below. Otherwise, you will not be able to boot your computer because you couldn't enter your decryption password to decrypt your Linux root partition!

```
HOOKS="... **usbinput** encrypt ..."

```

## Installing the system

**Note:** Most of the installation can be carried out normally. However, there are a few areas where it is important to make certain selections. These are marked below.

### Prepare hard drive for Arch Install Scripts

This assumes you want to install an encrypted system with the Arch Install Scripts, have created partitions for `/` (e.g. `/dev/sdaX`) and `/boot` (`/dev/sdaY`) at least, following the [Installation Guide](/index.php/Installation_guide "Installation guide") and deciding against [using LVM](/index.php/LUKS#LVM:_Logical_Volume_Manager "LUKS"). Prior to creating the partitions you have done a [preparation](/index.php/LUKS#Secure_erasure_of_the_hard_disk_drive "LUKS") of the disk for encryption according to your necessities (the necessary tools are on the installation-ISO).

First check, if the blockdevice mapper `dm_mod` is loaded with

```
# lsmod | grep mod 

```

If one wants to use the default LUKS-cipher algorithm, there is no need to specify one for the luksFormat. At the time of writing the default is set to an AES variant with 256 bit key-length. With that a dm-crypt/LUKS blockdevice for the crypted root can be created

```
# cryptsetup -y -v luksFormat /dev/sdaX

```

opened

```
# cryptsetup luksOpen /dev/sdaX cryptroot

```

formatted with your desired filesystem

```
# mkfs -t ext4 /dev/mapper/cryptroot

```

and mounted

```
# mount -t ext4 /dev/mapper/cryptroot /mnt

```

At this point, just before installing the base system, it might be useful to check the mapping works as intended:

```
# umount /mnt
# cryptsetup luksClose cryptroot

```

and mount it again to check.

If you created a separate `/home` partition, the steps have to be adapted and repeated for that. What you do have to setup is a non-encrypted `/boot` partition, which is needed for a crypted root. For a standard [MBR/non-EFI](/index.php/EFI "EFI") `/boot` partition that may be achieved by formatting

```
# mkfs -t ext2 /dev/sdaY

```

creating a mount-point for installation

```
# mkdir /mnt/boot

```

and mounting it

```
# mount -t ext2 /dev/sdaY /mnt/boot

```

That is basically what is necessary at this point before installing the base system with the [Arch Install Scripts](/index.php/Installation_guide#Mount_the_partitions "Installation guide"). Take care to install the bootloader to `/mnt/boot` with the `pacstrap` script. Additional configuration steps must be followed before booting the installed system.

### Configure initramfs

One important point is to add the hooks relevant for your particular install in the correct order to `/etc/mkinitcpio.conf`. The one you *have* to add when encrypting the root filesystem is `encrypt`. A recommended hook for LUKS encrypted blockdevices is `shutdown` to ensure controlled unmounting during system shutdown. Others needed, e.g. `keymap`, should be clear from other manual steps you follow during the installation and further details in the following. For detailed information about initramfs configuration and available Hooks refer to [Mkinitcpio#HOOKS](/index.php/Mkinitcpio#HOOKS "Mkinitcpio").

**Note:** The `encrypt` hook is only needed if your **root** partition is a *LUKS* partition (or a LUKS partition that needs to be mounted *before* root). The `encrypt` hook is not needed for any other encrypted partitions (swap, for example). System initialization scripts (`/etc/rc.sysinit` and `/etc/crypttab` among others) take care of those.

It is important that the `encrypt` hook comes *before* the `filesystems` hook (in case you are using **LVM on LUKS**, the order should be: `encrypt lvm2 filesystems`), so make sure that your `HOOKS` array looks something like this:

 `etc/mkinitcpio.conf`  `HOOKS="(base udev) ... **encrypt** ... filesystems ..."` 

If you need support for foreign keymaps for your encryption password, you have to specify the hook `keymap` as well before `encrypt`.

If you have a USB keyboard, you will need the `usbinput` hook. Without it, no USB keyboard will work in early userspace.

If the encrypted root container has keyslots for [keyfiles loaded from external usb devices](#Storing_the_Key_File) or root itself is on usb storage the `usb` hook is needed before encrypt.

```
HOOKS="... **usb** encrypt ... filesystems ..."

```

In the same file, you may want to add to "MODULES" **dm_mod** and the filesystem types used, e.g: `MODULES="dm_mod ext4"`

After you are done don't forget:

```
mkinitcpio -p linux

```

### Kernel parameter configuration of the bootloader

#### GRUB2

The article on GRUB2 gives a brief introduction and features [a small section on configuration for system encryption](/index.php/GRUB2#Encryption "GRUB2").

The recommended way for configuring GRUB is `/etc/default/grub` where the kernel line has to be adjusted so GRUB can pass to the kernel how to map the (encrypted) root device.

The syntax for **cryptdevice** is:

```
cryptdevice=*device:dmname*

```

	device

	The path to the raw encrypted device. Usage of [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") is advisable.

	dmname

	The name given to the device after decryption, will be available as `/dev/mapper/*dmname*`. (**DO NOT** set dmname to a name you already used for your LVM partitions!)

So if the encrypted root device is in example `/dev/sda2` and the decrypted one should be mapped to `/dev/mapper/cryptroot` the kernel line must look like:

 `/etc/default/grub`  `GRUB_CMDLINE_LINUX="cryptdevice=/dev/sda2:cryptroot"` 

Depending on the setup other parameters are required as well:

```
GRUB_CMDLINE_LINUX="cryptdevice=*device:dmname* root=*device* resume=*device* cryptkey=*device:fstype:path*"

```

	root=*device*

	The device file of the actual (decrypted) root filesystem. If the filesystem is formatted directly on the decrypted device file this will be `/dev/mapper/*dmname*`. If LVM is in between sth. like `/dev/mapper/*volgroup-pvol*` or `/dev/*volgroup/pvol*` does the trick.

	resume=*device*

	The device file of the decrypted (swap) filesystem used for suspend2disk.

	cryptkey=*device:fstype:path*

	Required for reading a [keyfile](#Storing_the_Key_File) from a filesystem.

The syntax for the optional **cryptkey** parameter is:

```
cryptkey=*device:fstype:path*

```

	device

	The raw block device where the key exists.

	fstype

	The filesystem type of device (or auto).

	path

	The absolute path of the keyfile within the device.

Make sure to regenerate your configuration file after editing with:

```
grub-mkconfig -o /boot/grub/grub.cfg

```

The device name your harddrive should be mapped to depends on your setup and configuration. If you are directly decrypting your root partition, the parameter `root=/dev/mapper/cryptroot` will indicate the expected name. In case of [LVM](/index.php/LVM "LVM") this name can be any arbitrary name, as LVM will parse all available devices if specified as the next hook.

#### Syslinux

The Article on Syslinux describes in [the basic config-section](/index.php/Syslinux#Basic_Config "Syslinux") how to use LUKS for system encryption (added 2012):

```
APPEND root=/dev/mapper/*name* cryptdevice=/dev/sda2:*name* ro

```

#### GRUB Legacy

**[GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy"):** You have to make some small changes to the entries generated by the installer by replacing `/dev/mapper/root` with `/dev/sda3`. The important point to remember here is to use the same `cryptdevice` name you assigned when you initially unlocked your device. In this example, the device name is `cryptroot`; customize yours accordingly:

```
# (0) Arch Linux
title Arch Linux
root (hd0,0)
kernel /vmlinuz-linux cryptdevice=/dev/sda3:cryptroot root=/dev/mapper/cryptroot ro
initrd /initramfs-linux.img

```

For kernels older than 2.6.37, the syntax is:

```
# (0) Arch Linux
title Arch Linux
root (hd0,0)
kernel /vmlinuz26 root=/dev/sda3 ro
initrd /kernel26.img

```

#### LILO

**LILO:** Edit the Arch Linux section in `/etc/lilo.conf` and include a line for the `append` option, over the initrd, with the `root=/dev/sda3` parameter. The `append` section makes the same kernel line as in GRUB. Also, you can omit the `root` option above the `image` option. The section looks like this:

```
# Arch Linux lilo section
image = /vmlinuz-linux
# root = /dev/sda3
 label = Arch
 initrd = /initramfs-linux.img
 append = "root=/dev/sda3"
 read-only

```

**Note:** If you want to use a USB flash drive with a keyfile, you have to append the `cryptkey` option. See the corresponding section below.

### Fstab

Further, double-check the `gen[fstab](/index.php/Fstab "Fstab")` scripts result for your `/dev/mapper/cryptroot` and other mounts.

## Remote unlocking of the root (or other) partition

If you want to be able to reboot a fully LUKS-encrypted system remotely, or start it with a Wake-on-LAN service, you will need a way to enter a passphrase for the root partition/volume at startup. This can be achieved by running the `net` hook along with an [SSH](/index.php/SSH "SSH") server in initrd. Install the [dropbear_initrd_encrypt](https://aur.archlinux.org/packages/dropbear_initrd_encrypt/) package from the [AUR](/index.php/Arch_User_Repository "Arch User Repository") and follow the post-installation instructions. Replace the `encrypt` hook with `dropbear encryptssh` in `/etc/mkinitcpio.conf`. Put the `net` hook early in the HOOKS array if your DHCP server takes a long time to lease IP addresses.

If you would simply like a nice solution to mount other encrypted partitions (such as `/home`)remotely, you may want to look at [this forum thread](https://bbs.archlinux.org/viewtopic.php?pid=880484).

**Note:** Acutally trim will not work with this script because it is not yet updated to the latest encrypt hook, so it is not able to parse `-–allow-discards` from `/boot/grub/menu.lst`. (Version: dropbear_initrd_encrypt 0.8-16). You won't notice any error when using online discard, but you see an error when you try to use `fstrim`.For a temporary solution just add `-–allow-discards` to every cryptsetup line of `/lib/initcpio/install/dropbear`(1 line) and `/lib/initcpio/hooks/encryptssh`(3 lines)

## Backup the cryptheader

If the header of your encrypted partition gets destroyed, you will not be able to decrypt your data. It is just as much as a dilemma as forgetting the passphrase or damaging a key-file used to unlock the partition. A damage may occur by your own fault while re-partitioning the disk later or by third-party programs misinterpreting the partition table.

Therefore, having a backup of the headers and storing them on another disk might be a good idea.

**Attention:** Many people recommend NOT backing up the cryptheader, but even so it's a single point of failure! In short, the problem is that LUKS is not aware of the duplicated cryptheader, which contains the master key which is used to encrypt all files on your partition. Of course this master key is encrypted with your passphrases or keyfiles. But if one of those gets compromised and you want to revoke it you have to do this on all copies of the cryptheader! I.e. if someone has got your cryptheader and one of your keys he can decrypt the master key and access all your data. Of course the same is true for all backups you create of your partions. So you decide if you are one of those paranoids brave enough to go without a backup for the sake of security or not. See also the [LUKS FAQ](http://code.google.com/p/cryptsetup/wiki/FrequentlyAskedQuestions#6._Backup_and_Data_Recovery%7C) for further details on this.

### Backup

#### Using cryptsetup

Cryptsetups `luksHeaderBackup` action stores a binary backup of the LUKS header and keyslot area:

```
# cryptsetup luksHeaderBackup /dev/*device* --header-backup-file /mnt/*backup/file*.img

```

where *device* is the partition containing the LUKS volume.

**Note:** Using `-` as header backup file writes to a file named `-`.

**Tip:** You can also back up the plaintext header into ramfs and encrypt it in example with gpg before writing to persistent backup storage by executing the following commands.

```
# mkdir /root/*tmp*/
# mount ramfs /root/*tmp*/ -t ramfs
# cryptsetup luksHeaderBackup /dev/*device* --header-backup-file /root/*tmp/file*.img
# gpg2 --recipient <User ID> --encrypt /root/*tmp/file*.img 
# cp /root/*tmp*/*file*.img.gpg /mnt/*backup*/
# umount /root/*tmp*
```

**Warning:** Tmpfs can swap to harddisk if low on memory so it is not recommended here.

#### Manually

First you have to find out the payload offset of the crypted partition:

 `# cryptsetup luksDump /dev/*device* | grep "Payload offset"`  ` Payload offset:	4040` 

Now that you know the value, you can backup the header with a simple dd command:

```
dd if=/dev/*device* of=/path/to/*file*.img bs=512 count=4040

```

### Restore

Be careful before restore: make sure that you chose the right partition (again replace sdaX with the corresponding partition). Restoring the wrong header or restoring to an unencrypted partition will cause data loss.

#### Using cryptsetup

Or you can use the luksHeaderRestore command:

```
cryptsetup luksHeaderRestore /dev/sdaX --header-backup-file ./backup.img

```

**Note:** All the keyslot areas are overwritten; only active keyslots from the backup file are available after issuing this command.

#### Manually

Again, you will need to the same values as when backing up:

```
dd if=./backup.img of=/dev/sdX bs=512 count=4040

```

## Encrypting a loopback filesystem

*[This paragraph has been merged from another page; its consistency with the other paragraphs should be improved]*

### Preparation and mapping

First, start by creating an encrypted container!

```
dd if=/dev/urandom of=/bigsecret bs=1M count=10

```

This will create the file `bigsecret` with a size of 10 megabytes.

```
losetup /dev/loop0 /bigsecret

```

This will create the device node `/dev/loop0`, so that we can mount/use our container.

**Note:** If it gives you the error `/dev/loop0: No such file or directory`, you need to first load the kernel module with `modprobe loop`. These days (Kernel 3.2) loop devices are created on demand. Ask for a new loop device with `losetup -f`.

```
cryptsetup luksFormat /dev/loop0

```

This will ask you for a password for your new container file.

**Note:** If you get an error like `Command failed: Failed to setup dm-crypt key mapping. Check kernel for support for the aes-cbc-essiv:sha256 cipher spec and verify that /dev/loop0 contains at least 133 sectors`, then run `modprobe dm-mod`.

```
cryptsetup luksOpen /dev/loop0 secret

```

The encrypted container is now available through the device file `/dev/mapper/secret`. Now we are able to create a partition in the container:

```
mkfs.ext2 /dev/mapper/secret

```

and mount it...

```
mkdir /mnt/secret
mount -t ext2 /dev/mapper/secret /mnt/secret

```

We can now use the container as if it was a normal partition! To unmount the container:

```
umount /mnt/secret
cryptsetup luksClose secret
losetup -d /dev/loop0 # free the loopdevice.

```

so, if you want to mount the container again, you just apply the following commands:

```
losetup /dev/loop0 /bigsecret
cryptsetup luksOpen /dev/loop0 secret
mount -t ext2 /dev/mapper/secret /mnt/secret

```

### Encrypt using a key-file

Let us first generate a 2048 byte random keyfile:

```
dd if=/dev/urandom of=keyfile bs=1k count=2

```

We can now format our container using this key

```
cryptsetup luksFormat /dev/loop0 keyfile

```

or our partition :

```
cryptsetup luksFormat /dev/hda2 keyfile

```

Once formatted, we can now open the LUKS device using the key:

```
cryptsetup -d keyfile luksOpen /dev/loop0 container

```

You can now like before format the device `/dev/mapper/container` with your favorite filesystem and then mount it just as easily.

The keyfile is now the only key to your file. I personally advise encrypting your keyfile using your private GPG key and storing an off-site secured copy of the file.

### Resizing the loopback filesystem

First we should unmount the encrypted container:

```
umount /mnt/secret
cryptsetup luksClose secret
losetup -d /dev/loop0 # free the loopdevice.

```

After this we need to expand our container file with the size of the data we want to add:

```
dd if=/dev/urandom bs=1M count=1024 | cat - >> /bigsecret

```

Be careful to really use TWO `>`, or you will override your current container!

You could use `/dev/zero` instead of `/dev/urandom` to significantly speed up the process, but with `/dev/zero` your encrypted filesystems will *not be as secure*. (A better option to create random data quicker than `/dev/urandom` is `frandom` [[1]](https://aur.archlinux.org/packages.php?ID=9869), available from the [AUR](/index.php/AUR "AUR")). A faster (almost instant) method than dd is `truncate` , but its use has the same security implications as using /dev/zero. The size passed to truncate is the final size to make the file, so don't use a value less than that of the current file or you will lose data. e.g. to increase a 20G file by 10G: truncate -s 30G filename.

Now we have to map the container to the loop device:

```
losetup /dev/loop0 /bigsecret
cryptsetup luksOpen /dev/loop0 secret

```

After this we will resize the encrypted part of the container to the maximum size of the container file:

```
cryptsetup resize secret

```

Finally, we can resize the filesystem. Here is an example for ext2/3/4:

```
e2fsck -f /dev/mapper/secret # Just doing a filesystem check, because it's a bad idea to resize a broken fs
resize2fs /dev/mapper/secret

```

You can now mount your container again:

```
mount /dev/mapper/secret /mnt/secret

```

## Encrypting a LVM setup

It's really easy to use encryption with [LVM](/index.php/LVM "LVM"). If you do not know how to set up LVM, then read [Installing with Software RAID or LVM](/index.php/Installing_with_Software_RAID_or_LVM "Installing with Software RAID or LVM").

**LVM on LUKS**

The easiest and best method is to set up LVM on top of the encrypted partition instead of the other way round. This link here is easy to follow and explains everything: [Arch Linux: LVM on top of an encrypted partition](http://www.pindarsign.de/webblog/?p=767)

The most important thing in setting LVM on **top** of encryption is to [configure the initramfs](#Configure_initramfs) for running the `encrypt` hook **before** the `lvm2` hook (and those two before the `filesystems` hook).

**LUKS on LVM**

To use encryption on top of LVM, you have to first set up your LVM volumes and then use them as the base for the encrypted partitions. That means, in short, that you have to set up LVM first. Then follow this guide, but replace all occurrences of `/dev/sdXy` in the guide with its LVM counterpart. (E.g.: `/dev/sda5` -> `/dev/<volume group name>/home`). This is used to setup partitions (inside the LVM) which can be unlocked separately or a mixture of encrypted and non-encrypted partitions.

For encrypted partitions inside an LVM, the LVM-hook has to run first, before the respective encrypted logical volumes can be unlocked. So for this add the `encrypt` hook in `/etc/mkinitcpio.conf` **after** the `lvm2` hook, if you chose to set up encrypted partitions on **top** of LVM. Also remember to change `USELVM` in `/etc/rc.conf` to `"yes"`.

### LVM with Arch Linux Installer (>2009.08 <2012.07.15)

In between Arch Linux installation media release 2009.08 and 2012.07.15 LVM and dm_crypt had been supported by the installer out of the box. This made it very easy to configure a system for [LVM](/index.php/LVM "LVM") on dm-crypt or vice versa. Actually the configuration is done exactly as without LVM: see the [corresponding](#Arch_Linux_Installer_.28.3E2009.08_.3C2012.07.15.29) section above. It differs only in two aspects.

#### The partition and filesystem choice

Create a small, unencrypted boot partition and use the remaining space for a single partition which can later be split up into multiple logic volumes by [LVM](/index.php/LVM "LVM").

For a LVM-on-dm-crypt system set up the filesystems and mounting points for example like this:

```
/dev/sda1   raw->ext2;yes;/boot;no_opts;no_label;no_params
/dev/sda2   raw->dm_crypt;yes;no_mountpoint;no_opts;sda2crypt;-c_aes-xts-plain_-y_-s_512
/dev/mapper/sda2crypt   dm_crypt->lvm-vg;yes;no_mountpoint;no_opts;no_label;no_params
/dev/mapper/sda2crypt+  lvm-pv->lvm-vg;yes;no_mountpoint;no_opts;cryptpool;no_params
/dev/mapper/cryptpool   lvm-vg(cryptpool)->lvm-lv;yes;no_mountpoint;no_opts;cryptroot;10000M|lvm-lv;yes;no_mountpoint;no_opts;crypthome;20000M
/dev/mapper/cryptpool-cryptroot   lvm-lv(cryptroot)->ext3;yes;/;no_opts;cryptroot;no_params
/dev/mapper/cryptpool-crypthome   lvm-lv(crypthome)->ext3;yes;/home;no_opts;cryptroot;no_params

```

#### The configuration stage

*   In `/etc/mkinitcpio.conf` add the `encrypt` hook **before** the `lvm2` hook in the `HOOKS` array, if you set up LVM on top of the encrypted partition.

That is it for the LVM & dm_crypt specific part. The rest is done as usual.

*   In `/etc/rc.conf` set `USELVM` to `"yes"`.

### Applying this to a non-root partition

You might get tempted to apply all this fancy stuff to a non-root partition. Arch does not support this out of the box, however, you can easily change the cryptdev and cryptname values in `/lib/initcpio/hooks/encrypt` (the first one to your `/dev/sd*` partition, the second to the name you want to attribute). That should be enough.

The big advantage is you can have everything automated, while setting up `/etc/crypttab` with an external key file (i.e. the keyfile is not on any internal hard drive partition) can be a pain - you need to make sure the USB/FireWire/... device gets mounted before the encrypted partition, which means you have to change the order of `/etc/fstab` (at least).

Of course, if the [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) package gets upgraded, you will have to change this script again. However, this solution is to be preferred over hacking `/etc/rc.sysinit` or similar files. Unlike `/etc/crypttab`, only one partition is supported, but with some further hacking one should be able to have multiple partitions unlocked.

If you want to do this on a software RAID partition, there is one more thing you need to do. Just setting the `/dev/mdX` device in `/lib/initcpio/hooks/encrypt` is not enough; the `encrypt` hook will fail to find the key for some reason, and not prompt for a passphrase either. It looks like the RAID devices are not brought up until after the `encrypt` hook is run. You can solve this by putting the RAID array in `/boot/grub/menu.lst`, like

```
kernel /boot/vmlinuz-linux md=1,/dev/hda5,/dev/hdb5

```

If you set up your root partition as a RAID, you will notice the similarities with that setup ;-). [GRUB](/index.php/GRUB "GRUB") can handle multiple array definitions just fine:

```
kernel /boot/vmlinuz-linux root=/dev/md0 ro md=0,/dev/sda1,/dev/sdb1 md=1,/dev/sda5,/dev/sdb5,/dev/sdc5

```

### LVM and dm-crypt manually (short version)

#### Notes

If you are smart enough for this, you will be smart enough to ignore/replace LVM-specific things if you do not want to use LVM.

**Note:** This brief uses reiserfs for some of the partitions, so change this accordingly if you want to use a more "normal" file system, like ext4.

#### Partitioning scheme

```
`/dev/sda1` -> `/boot`
`/dev/sda2` -> LVM

```

#### The commands

```
cryptsetup -d /dev/random -c aes-xts-plain -s 512 create lvm /dev/sda2
dd if=/dev/urandom of=/dev/mapper/lvm
cryptsetup remove lvm
lvm pvcreate /dev/sda2
lvm vgcreate lvm /dev/sda2
lvm lvcreate -L 10G -n root lvm
lvm lvcreate -L 500M -n swap lvm
lvm lvcreate -L 500M -n tmp lvm
lvm lvcreate -l 100%FREE -n home lvm
cryptsetup luksFormat -c aes-xts-plain -s 512 /dev/lvm/root
cryptsetup luksOpen /dev/lvm/root root
mkreiserfs /dev/mapper/root
mount /dev/mapper/root /mnt
dd if=/dev/zero of=/dev/sda1 bs=1M
mkreiserfs /dev/sda1
mkdir /mnt/boot
mount /dev/sda1 /mnt/boot
mkdir -p -m 700 /mnt/etc/luks-keys
dd if=/dev/random of=/mnt/etc/luks-keys/home bs=1 count=256

```

#### Install Arch Linux

Run `/arch/setup`

#### Configuration

##### /etc/rc.conf

Change `USELVM="no"` to `USELVM="yes"`.

##### /etc/mkinitcpio.conf

Put `lvm2` and `encrypt` (in that order) before `filesystems` in the `HOOKS` array. Again, note that you are setting encryption on **top** of LVM.)

if you want install the system on a usb stick, you need to put `usb` just after `udev`.

##### /boot/grub/menu.lst

Change `root=/dev/hda3` to `root=/dev/lvm/root`.

For kernel >= 2.6.30, you should change `root=/dev/hda3` to the following:

```
cryptdevice=/dev/lvm/root:root root=/dev/mapper/root

```

if you want install the system on a usb stick, you need to add `lvmdelay=/dev/mapper/lvm-root`

##### /etc/fstab

```
/dev/mapper/root        /       reiserfs        defaults        0       1
/dev/sda1               /boot   reiserfs        defaults        0       2
/dev/mapper/tmp         /tmp    tmpfs           defaults        0       0
/dev/mapper/swap        none    swap            sw              0       0

```

##### /etc/crypttab

```
swap	/dev/lvm/swap	SWAP		-c aes-xts-plain -h whirlpool -s 512
tmp	/dev/lvm/tmp	/dev/urandom	-c aes-xts-plain -s 512

```

#### After rebooting

##### The commands

```
cryptsetup luksFormat -c aes-xts-plain -s 512 /dev/lvm/home /etc/luks-keys/home
cryptsetup luksOpen -d /etc/luks-keys/home /dev/lvm/home home
mkreiserfs /dev/mapper/home
mount /dev/mapper/home /home

```

##### /etc/crypttab

```
home	/dev/lvm/home   /etc/luks-keys/home

```

##### /etc/fstab

```
/dev/mapper/home        /home   reiserfs        defaults        0       0

```

### / on LVM on LUKS

Make sure your kernel command line looks like this:

```
root=/dev/mapper/<volume-group>-<logical-volume> cryptdevice=/dev/<luks-part>:<volume-group>

```

For example:

```
root=/dev/mapper/vg-arch cryptdevice=/dev/sda4:vg

```

Or like this:

```
cryptdevice=/dev/<volume-group>/<logical-volume>:root root=/dev/mapper/root

```

## Using GPG or OpenSSL Encrypted Keyfiles

The following forum posts give instructions to use two factor authentication, gpg or openssl encrypted keyfiles, instead of a plaintext keyfile described earlier in this wiki article [System Encryption using LUKS with GPG encrypted keys](https://bbs.archlinux.org/viewtopic.php?id=120243):

*   GnuPG: [Post regarding GPG encrypted keys](https://bbs.archlinux.org/viewtopic.php?pid=943338#p943338) This post has the generic instructions.
*   OpenSSL: [Post regarding OpenSSL encrypted keys](https://bbs.archlinux.org/viewtopic.php?pid=947805#p947805) This post only has the `ssldec` hooks.
*   OpenSSL: [Post regarding OpenSSL salted bf-cbc encrypted keys](https://bbs.archlinux.org/viewtopic.php?id=155393) This post has the `bfkf` initcpio hooks, install, and encrypted keyfile generator scripts.

Note that:

*   You can follow the above instructions with only two primary partitions one boot partition

(required because of LVM), and one primary LVM partition. Within the LVM partition you can have as many partitions as you need, but most importantly it should contain at least root, swap, and home logical volume partitions. This has the added benefit of having only one keyfile for all your partitions, and having the ability to hibernate your computer (suspend to disk) where the swap partition is encrypted. If you decide to do so your hooks in `/etc/mkinitcpio.conf` should look like `HOOKS=" ... usb usbinput (etwo or ssldec) encrypt(if using openssl) lvm2 resume ... "` and you should add to your `kernel` line(if using grub, `/boot/grub/menu.lst`) or `GRUB_CMD_LINE`(if using grub2, `/etc/default/grub`): `"resume=/dev/mapper/*VolumeGroupName-LVNameOfSwap*"`

*   If you need to temporarily store the unecrypted keyfile somewhere, do not store them on an

unencrytped disk. Even better make sure to store them to RAM such as `/dev/shm`.

*   If you want to use a GPG encrypted keyfile, you need to use a statically compiled GnuPG version 1.4 or you could edit the hooks and use this AUR package [gnupg1](https://aur.archlinux.org/packages.php?ID=58030)
*   It is possible that an update to OpenSSL could break the custom `ssldec` mentioned in the second forum post.

## Securing the unencrypted boot partition

Referring to an article from the ct-magazine (Issue 3/12, page 146, 01.16.2012 [http://www.heise.de/ct/inhalt/2012/03/6/](http://www.heise.de/ct/inhalt/2012/03/6/)) the following script checks all files under `/boot` for changes of SHA-1 hash, inode and occupied blocks on the hard drive. It also checks the MBR.

The script with installation instructions is available here: [ftp://ftp.heise.de/pub/ct/listings/1203-146.zip](ftp://ftp.heise.de/pub/ct/listings/1203-146.zip) (Author: Juergen Schmidt, ju at heisec.de; License: GPLv2). There is also an AUR package: [chkboot](https://aur.archlinux.org/packages/chkboot/)

After installation:

*   For classical sysvinit: add `/usr/local/bin/chkboot.sh &` to your `/etc/rc.local`
*   For systemd: add a service file and enable the service: [systemd](/index.php/Systemd "Systemd"). The service file might look like:

```
[Unit]
Description=Check that boot is what we want
Requires=systemd-remount-fs.service
After=systemd-remount-fs.service

[Service]
Type=oneshot
ExecStart=/usr/local/bin/chkboot.sh

[Install]
WantedBy=multi-user.target

```

There is a small caveat for systemd: At the time of writing the original `chkboot.sh` script provided contains an empty space at the beginning of `#!/bin/bash` which has to be removed for the service to start successfully.

As `/usr/local/bin/chkboot_user.sh` need to be excuted after login, add it to the autostart (e.g. under KDE -> System Settings -> Startup and Shutdown -> Autostart; Gnome3: gnome-session-properties).

With Arch Linux changes to `/boot` are pretty frequent, for example by new kernels rolling-in. Therefore it may be helpful to use the scripts with every full system update. One way to do so:

```
#!/bin/bash
#
# Note: Insert your <user>  and execute it with sudo for pacman & chkboot to work automagically
#
echo "Pacman update [1] Quickcheck before updating" & 
sudo -u <user> /usr/local/bin/chkboot_user.sh		# insert your logged on <user> 
/usr/local/bin/chkboot.sh
sync							# sync disks with any results 
sudo -u <user> /usr/local/bin/chkboot_user.sh		# insert your logged on <user> 
echo "Pacman update [2] Syncing repos for pacman" 
pacman -Syu
/usr/local/bin/chkboot.sh
sync	
sudo -u <user> /usr/local/bin/chkboot_user.sh		# insert your logged on <user>
echo "Pacman update [3] All done, let's roll on ..."

```

## Automount user homes on login

See [pam_mount](/index.php/Pam_mount "Pam mount").

## Resources

*   [cryptsetup FAQ](http://code.google.com/p/cryptsetup/wiki/FrequentlyAskedQuestions) - The main and foremost help resource, directly from the developers.
*   [FreeOTFE](http://www.freeotfe.org/) - Supports unlocking LUKS encrypted volumes in Microsoft Windows.

*   [Arch cryptsetup example video](http://vimeo.com/40694871) - A HowTo video on setting up an encrypted Arch system from scratch. The video still shows an installation with AIF, which is at the time of writing deprecated / not developed further. The important partitioning and cryptsetup are shown outside AIF though.
*   [Install Arch Linux on top of RAID1, LVM2, and encrypted partitions](http://yannickloth.be/blog/2010/08/01/installing-archlinux-with-software-raid1-encrypted-filesystem-and-lvm2/) - The HowTo instructs to make a full Fedora 13 Install only to set up the mapping. Then legacy AIF is used.