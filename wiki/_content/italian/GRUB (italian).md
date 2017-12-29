Articoli correlati

*   [GRUB Legacy (Italiano)](/index.php/GRUB_Legacy_(Italiano) "GRUB Legacy (Italiano)")
*   [Arch boot process](/index.php/Arch_boot_process "Arch boot process")
*   [Boot loaders](/index.php/Boot_loaders "Boot loaders")
*   [Master Boot Record (Italiano)](/index.php/Master_Boot_Record_(Italiano) "Master Boot Record (Italiano)")
*   [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table")
*   [Unified Extensible Firmware Interface (Italiano)](/index.php/Unified_Extensible_Firmware_Interface_(Italiano) "Unified Extensible Firmware Interface (Italiano)")
*   [GRUB EFI Examples](/index.php/GRUB_EFI_Examples "GRUB EFI Examples")

[GRUB](http://www.gnu.org/software/grub/) - da non confondere con [GRUB Legacy](/index.php/GRUB_Legacy_(Italiano) "GRUB Legacy (Italiano)") - è la nuova versione del GRand Unified Bootloader. GRUB deriva da [PUPA](http://www.nongnu.org/pupa/), un progetto di ricerca mirato al miglioramento di GRUB Legacy: esso è stato infatti totalmente riscritto, ripulendo il codice assicurando al tempo stesso una maggior modularità e portabilità. [[1]](http://www.gnu.org/software/grub/grub-faq.html#q1)

In sintesi, il *bootloader* è il primo programma ad essere eseguito quando il computer si avvia. Ha il compito di caricare e trasferire il controllo al Kernel Linux, il quale, di contro, inizializza il resto del sistema operativo.

## Contents

*   [1 Prefazione](#Prefazione)
    *   [1.1 Note per gli utenti di GRUB Legacy](#Note_per_gli_utenti_di_GRUB_Legacy)
        *   [1.1.1 Effetuare un backup dei dati importanti](#Effetuare_un_backup_dei_dati_importanti)
    *   [1.2 Prerequisiti per GRUB2](#Prerequisiti_per_GRUB2)
        *   [1.2.1 Sistemi BIOS](#Sistemi_BIOS)
            *   [1.2.1.1 Istruzioni specifiche per GUID Partition Table (GPT)](#Istruzioni_specifiche_per_GUID_Partition_Table_.28GPT.29)
            *   [1.2.1.2 Istruzioni specifiche per Master Boot Record (MBR)](#Istruzioni_specifiche_per_Master_Boot_Record_.28MBR.29)
        *   [1.2.2 Sistemi UEFI](#Sistemi_UEFI)
            *   [1.2.2.1 Controllare se si sta utilizzando GPT ed una partizione EFI di sistema](#Controllare_se_si_sta_utilizzando_GPT_ed_una_partizione_EFI_di_sistema)
            *   [1.2.2.2 Creazione di una partizione EFI di sistema](#Creazione_di_una_partizione_EFI_di_sistema)
*   [2 Installazione](#Installazione)
    *   [2.1 Sistemi BIOS](#Sistemi_BIOS_2)
        *   [2.1.1 Installare i file di boot](#Installare_i_file_di_boot)
            *   [2.1.1.1 Installazione su disco](#Installazione_su_disco)
            *   [2.1.1.2 Installazione su chiavetta USB](#Installazione_su_chiavetta_USB)
            *   [2.1.1.3 Installazione su una partizione o su un disco partitionless](#Installazione_su_una_partizione_o_su_un_disco_partitionless)
            *   [2.1.1.4 Generazione del solo core.img](#Generazione_del_solo_core.img)
    *   [2.2 Sistemi UEFI](#Sistemi_UEFI_2)
        *   [2.2.1 Metodo di installazione consigliato](#Metodo_di_installazione_consigliato)
            *   [2.2.1.1 Workaround per alcuni firmware UEFI](#Workaround_per_alcuni_firmware_UEFI)
            *   [2.2.1.2 Metodo alternativo](#Metodo_alternativo)
        *   [2.2.2 Creare una voce per GRUB nel Firmware Boot Manager](#Creare_una_voce_per_GRUB_nel_Firmware_Boot_Manager)
        *   [2.2.3 GRUB Standalone](#GRUB_Standalone)
            *   [2.2.3.1 GRUB Standalone - Informazioni tecniche](#GRUB_Standalone_-_Informazioni_tecniche)
*   [3 Generazione del file di configurazione principale](#Generazione_del_file_di_configurazione_principale)
    *   [3.1 Conversione del file di configurazione di GRUB Legacy al nuovo formato](#Conversione_del_file_di_configurazione_di_GRUB_Legacy_al_nuovo_formato)
*   [4 Configurazione di base](#Configurazione_di_base)
    *   [4.1 Argomenti aggiuntivi](#Argomenti_aggiuntivi)
    *   [4.2 Configurazione dell'aspetto](#Configurazione_dell.27aspetto)
        *   [4.2.1 Impostare la risoluzione del framebuffer](#Impostare_la_risoluzione_del_framebuffer)
        *   [4.2.2 Hack 915resolution](#Hack_915resolution)
        *   [4.2.3 Immagine di sfondo e caratteri bitmap](#Immagine_di_sfondo_e_caratteri_bitmap)
        *   [4.2.4 Temi](#Temi)
        *   [4.2.5 Colori del Menù](#Colori_del_Men.C3.B9)
        *   [4.2.6 Menù nascosto](#Men.C3.B9_nascosto)
        *   [4.2.7 Disabilitare il framebuffer](#Disabilitare_il_framebuffer)
    *   [4.3 Nomenclatura permanente dei dispositivi a blocchi](#Nomenclatura_permanente_dei_dispositivi_a_blocchi)
    *   [4.4 Richiamare l'ultimo sistema avviato](#Richiamare_l.27ultimo_sistema_avviato)
    *   [4.5 Cambiare la voce di menu predefinita](#Cambiare_la_voce_di_menu_predefinita)
    *   [4.6 Disabilitare il sottomenu](#Disabilitare_il_sottomenu)
    *   [4.7 Cifratura della partizione root](#Cifratura_della_partizione_root)
    *   [4.8 Effettuare il boot di una voce non default per una sola volta](#Effettuare_il_boot_di_una_voce_non_default_per_una_sola_volta)
*   [5 Configurazione avanzata](#Configurazione_avanzata)
    *   [5.1 Creazione manuale del grub.cfg](#Creazione_manuale_del_grub.cfg)
    *   [5.2 Dual-booting](#Dual-booting)
        *   [5.2.1 Generazione automatica utilizzando il file /etc/grub.d/40_custom e grub-mkconfig](#Generazione_automatica_utilizzando_il_file_.2Fetc.2Fgrub.d.2F40_custom_e_grub-mkconfig)
            *   [5.2.1.1 Voce di menù per GNU/Linux](#Voce_di_men.C3.B9_per_GNU.2FLinux)
            *   [5.2.1.2 Voce di menù per FreeBSD](#Voce_di_men.C3.B9_per_FreeBSD)
            *   [5.2.1.3 Voce di menù per Windows XP](#Voce_di_men.C3.B9_per_Windows_XP)
            *   [5.2.1.4 Voce di menù per Windows installato in modalità UEFI-GPT](#Voce_di_men.C3.B9_per_Windows_installato_in_modalit.C3.A0_UEFI-GPT)
            *   [5.2.1.5 Voce di menù per lo spegnimento del sistema](#Voce_di_men.C3.B9_per_lo_spegnimento_del_sistema)
            *   [5.2.1.6 Voce di menù per il riavvio del sistema](#Voce_di_men.C3.B9_per_il_riavvio_del_sistema)
            *   [5.2.1.7 Windows installato in modalità BIOS-MBR](#Windows_installato_in_modalit.C3.A0_BIOS-MBR)
        *   [5.2.2 Con Windows usando EasyBCD e NeoGRUB](#Con_Windows_usando_EasyBCD_e_NeoGRUB)
    *   [5.3 Avviare un'immagine ISO9660 direttamente da GRUB](#Avviare_un.27immagine_ISO9660_direttamente_da_GRUB)
    *   [5.4 LVM](#LVM)
    *   [5.5 RAID](#RAID)
    *   [5.6 Usare le etichette](#Usare_le_etichette)
    *   [5.7 Proteggere con una password il menu di GRUB](#Proteggere_con_una_password_il_menu_di_GRUB)
    *   [5.8 Nascondere il menu di GRUB e farlo apparire alla pressione del tasto Shift](#Nascondere_il_menu_di_GRUB_e_farlo_apparire_alla_pressione_del_tasto_Shift)
*   [6 Combinare UUID e scripting](#Combinare_UUID_e_scripting)
*   [7 Usare la shell](#Usare_la_shell)
    *   [7.1 Supporto al Pager](#Supporto_al_Pager)
    *   [7.2 Utilizzare la shell dei comanti per avviare altri sistemi operativi](#Utilizzare_la_shell_dei_comanti_per_avviare_altri_sistemi_operativi)
        *   [7.2.1 Effettuare il chainloading di una partizione](#Effettuare_il_chainloading_di_una_partizione)
        *   [7.2.2 Effettuare il chainloading di un disco/drive](#Effettuare_il_chainloading_di_un_disco.2Fdrive)
        *   [7.2.3 Effettuare il chainloading di sistemi Windows/Linux installati in modalità UEFI](#Effettuare_il_chainloading_di_sistemi_Windows.2FLinux_installati_in_modalit.C3.A0_UEFI)
        *   [7.2.4 Avvio normale](#Avvio_normale)
*   [8 Tools grafici per la configurazione](#Tools_grafici_per_la_configurazione)
*   [9 parttool per hide/unhide](#parttool_per_hide.2Funhide)
*   [10 Usare la console di emergenza](#Usare_la_console_di_emergenza)
*   [11 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [11.1 Sistemi con BIOS Intel non effettuano il boot da partizioni GPT](#Sistemi_con_BIOS_Intel_non_effettuano_il_boot_da_partizioni_GPT)
        *   [11.1.1 MBR](#MBR)
        *   [11.1.2 EFI](#EFI)
    *   [11.2 Abilitare i messaggi di debug in GRUB](#Abilitare_i_messaggi_di_debug_in_GRUB)
    *   [11.3 Correggere l'errore di GRUB "no suitable mode found"](#Correggere_l.27errore_di_GRUB_.22no_suitable_mode_found.22)
    *   [11.4 messaggio d'errore msdos-style](#messaggio_d.27errore_msdos-style)
    *   [11.5 GRUB UEFI torna alla shell](#GRUB_UEFI_torna_alla_shell)
    *   [11.6 GRUB UEFI non viene caricato](#GRUB_UEFI_non_viene_caricato)
    *   [11.7 Invalid signature](#Invalid_signature)
    *   [11.8 Freeze al boot](#Freeze_al_boot)
    *   [11.9 Ripristinare GRUB Legacy](#Ripristinare_GRUB_Legacy)
    *   [11.10 Arch non rilevata da altre distribuzioni](#Arch_non_rilevata_da_altre_distribuzioni)
*   [12 Riferimenti](#Riferimenti)

## Prefazione

*   Il nome *GRUB* si riferisce ufficialmente alla versione 2 del software (si veda [[2]](http://www.gnu.org/software/grub/)). Se si sta cercando l'articolo relativo alla versione Legacy, si veda [GRUB Legacy](/index.php/GRUB_Legacy_(Italiano) "GRUB Legacy (Italiano)").

*   E' supportato l'uso del filesystem [Btrfs](/index.php/Btrfs "Btrfs") per la root (eliminando quindi la necessità di una partizione /boot separata con un filesystem diverso). Sono inoltre supportati gli algoritmi di compressione zlib o LZO.

*   GRUB non supporta partizioni root formattate in [F2FS](/index.php/F2FS "F2FS"), perciò sarà necessario creare una partizione `/boot` separata usando un filesystem supportato.

### Note per gli utenti di GRUB Legacy

*   Aggiornare [GRUB Legacy](/index.php/GRUB_Legacy_(Italiano) "GRUB Legacy (Italiano)") a [GRUB](/index.php/GRUB2_(Italiano) "GRUB2 (Italiano)")(2) è un procedimento molto simile ad un installazione ex-novo di GRUB2, argomento trattato [qui](#Installazione).

*   Vi sono differenze nei comandi di GRUB e GRUB2\. Si consiglia di familiarizzare con i [comandi di GRUB2](http://www.gnu.org/software/grub/manual/grub.html#Commands) prima di procedere. (ad esempio, "find" è stato rimpiazzato da "search").
*   GRUB2 è ora *modulare* e non richiede più lo "stage 1.5". Di conseguenza, il bootloader dispone di capacità limitate e i moduli sono caricati dal disco rigido in caso di necessità (ad esempio, se si necessita del supporto [LVM](/index.php/LVM_(Italiano) "LVM (Italiano)") o RAID).
*   La modalità di nomenclatura dei dispositivi è cambiata da GRUB a GRUB2: gli hard disk sono ancora numerati a partire da 0, mentre le partizioni partono da 1 e sono seguite dal nome del sistema di partizionamento usato. Ad esempio, a `/dev/sda1` corrisponde `(hd0,msdos1)` (per sistemi che usano MBR) o `(hd0,gpt1)` (per sistemi GPT).
*   GRUB occupa molto più spazio rispetto a GRUB Legacy (circa 13Mb di spazio occupato in `/boot`). Se si effettua il boot da una partizione `/boot` separata con una dimensione inferiore ai 32 Mb si avranno problemi di spazio e pacman si rifiuterà di installare eventuali nuovi kernel, ad esempio.

#### Effetuare un backup dei dati importanti

In genere, l'installazione di grub dovrebbe andare a buon fine, ma è consigliabile conservare i files di GRUB-legacy prima di installare [grub](https://www.archlinux.org/packages/?name=grub).

```
mv /boot/grub /boot/grub-legay

```

Effettuare il backup del MBR che contiene il boot code e la tabella partizioni (Si sostituisca `/dev/sdX` con l'identificativo del proprio disco):

```
# dd if=/dev/sdX of=/path/to/backup/mbr_backup bs=512 count=1

```

Solamente i primi 446 bytes del MBR contengono il boot code, mentre i restanti 64 sono dedicati alla tabella delle partizioni. Se non si desidera sovrascriverla durante un eventuale ripristino, è fortemente consigliato effettuare il backup del solo boot code:

```
# dd if=/dev/sdX of=/path/to/backup/bootcode_backup bs=446 count=1

```

Se non si è stati in grado di installare GRUB2 correttamente, si veda [#Ripristinare GRUB Legacy](#Ripristinare_GRUB_Legacy)

### Prerequisiti per GRUB2

#### Sistemi BIOS

##### Istruzioni specifiche per GUID Partition Table (GPT)

Su sistemi [GPT](/index.php/GPT "GPT") è necessario creare una [partizione di boot BIOS](http://www.gnu.org/software/grub/manual/html_node/BIOS-installation.html) dove GRUB possa inserire il proprio `core.img`

**Nota:**

*   Prima di provare questo metodo si tenga presente che non tutti i sistemi supportano questa configurazione. Ulteriori informazioni sulle [tabelle partizioni GUID](/index.php/GUID_Partition_Table#BIOS_systems "GUID Partition Table").
*   La partizione in questione è necessaria solo per le combinazioni BIOS/GPT. In precedenza, su schemi di partizionamento BIOS/MBR, GRUB utilizzava il *post-MBR gap* per inserire il proprio `core.img`. GRUB per GPT non utilizza tale spazio per rispettare le specifiche GPT sull'allineamento tra le partizioni (1 Mebibyte/2048 settori).
*   Su sistemi [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Italiano) "Unified Extensible Firmware Interface (Italiano)") tale partizione non è richiesta in quanto in questo caso non si verifica l'*embedding* dei settori di boot.

Si crei una partizione da un mebibyte (`+1MiB` con `gdisk`) su un disco senza filesystem e le si assegni il tipo `ef02` (oppure `bios_grub` se si utilizza `parted`). Si noti che la partizione può trovare in qualsiasi posizione entro i primi 2 TiB del disco e deve essere creata prima dell'installazione. Una volta creata la aprtizione, si installi il bootloader seguendo le istruzioni sotto e assicurarsi di specificare l'opzione `--target=i386-pc` (altrimentri GRUB potrebbe pensare di trovarsi su un sistema EFI-GPT).

È possibile utilizzare il *post-MBR gap* come partizione di boot BIOS, anche se tale operazione non rispetta le specifiche GPT sull'allineamento delle partizioni. Dal momento che il contenuto di tale partizione non verrà letto spesso è possibile ignorare l'impatto sulle prestazioni, anche se alcune utility per il partizionamento visualizzeranno un messaggio d'avvertimento. In `gdisk` si crei una **n**uova partizione che inizia al settore 34 e arriva al 2047, e le si assegni il tipo. Per fare in modo che le partizioni visibili partano dall'inizio, si crei questa partizione per ultima.

##### Istruzioni specifiche per Master Boot Record (MBR)

Solitamente, il gap dopo il [MBR](/index.php/Master_Boot_Record_(Italiano) "Master Boot Record (Italiano)") (dopo i 512 byte ad esso dedicati, e prima dell'inizio della prima partizione), è di 31 KiB, quando eventuali problemi di allineamento dei cilindri sono risolti nella tabella partizioni. Tuttavia, è consigliato mantenere un gap di circa 1 MiB per fornire sufficiente spazio al `core.img` di GRUB. ([FS#24103](https://bugs.archlinux.org/task/24103)). È consigliabile usare un tool di partizionamento che supporti l'allineamento partizioni di 1 MiB dopo l'MBR per ottenere lo spazio necessario, e risolvere di conseguenza altri problemi, comunque non relativi all'embedding di `core.img`.

#### Sistemi UEFI

**Nota:** Per ulteriori informazioni su GRUB2 UEFI, è consigliabile leggere le pagine [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Italiano) "Unified Extensible Firmware Interface (Italiano)"), [GPT](/index.php/GPT "GPT") e [UEFI Bootloaders](/index.php/UEFI_Bootloaders "UEFI Bootloaders") prima di proseguire con questo articolo.

##### Controllare se si sta utilizzando GPT ed una partizione EFI di sistema

È necessaria una partizione EFI di sistema (*ESP*) in ogni disco fisso dal quale si desideri effettuare il boot in modalità EFI. GPT non è strettamente necessario, ma ne è raccomandato l'utilizzo, in quanto è l'unico metodo supportato da questo articolo.

Se si sta installando Arch Linux su un PC con supporto EFI dove sia già stato installato un altro sistema operativo, è probabile che si disponga già di una ESP. Si controlli utilizzando `parted` per stampare la tabella partizioni del disco dal quale si effettua il boot (nell'esempio si utilizzerà `/dev/sda`):

```
# parted /dev/sda print

```

Se si utilizza GPT, il comando dovrebbe riportare `Partition Table: GPT`. Per EFI, invece, individuare una piccola partizione (512 MiB o meno) con filesystem `vfat` e il flag `boot` attivo contenente una cartella chiamata *EFI*. In caso i criteri di cui sopra vengano soddisfatti, ricordarsi del numero assegnato alla partizione, in quanto sarà necessario per identificare la stessa quando dovrà essere montata per l'installazione di GRUB.

##### Creazione di una partizione EFI di sistema

Se non si dispone di una ESP, sarà necesario crearla. Si veda [Unified Extensible Firmware Interface#EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") per le istruzioni su come procedere.

## Installazione

**Nota:** Se si sta [installando](/index.php/Installation_guide_(Italiano) "Installation guide (Italiano)") Arch Linux da LiveCD assicurarsi di aver effettuato il chroot nel sistema appena installato prima di installare GRUB: se si utilizzano gli script di installazione contenuti nel LiveCD potrebbe venir generato un `grub.cfg` errato o potrebbero verificarsi altri problemi che non consentirebbero al sistema di avviarsi.

### Sistemi BIOS

E' possibile [installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") GRUB attraverso il pacchetto [grub](https://www.archlinux.org/packages/?name=grub), il quale sostituirà [grub-legacy](https://aur.archlinux.org/packages/grub-legacy/), se installato.

**Nota:** La sola installazione del pacchetto non aggiornerà il file `/boot/grub/i386-pc/core.img` o i moduli di GRUB2 in `/boot/grub`. È necessario aggiornare il `core.img` e i moduli manualmente usando `grub-install`, come spiegato sotto.

#### Installare i file di boot

Ci sono quattro modi per installare i files di boot di GRUB su sistemi BIOS

*   [Installazione su disco](#Installazione_su_disco) (consigliata)
*   [Installazione su chiavetta USB](#Installazione_su_chiavetta_USB) (per ripristino)
*   [Installazione su una partizione o su un disco partitionless](#Installazione_su_una_partizione_o_su_un_disco_partitionless) (sconsigliata)
*   [Generazione del solo core.img](#Generazione_del_solo_core.img) (metodo più sicuro, ma richiede un altro bootloader come [GRUB Legacy](/index.php/GRUB_Legacy_(Italiano) "GRUB Legacy (Italiano)") o [Syslinux](/index.php/Syslinux "Syslinux"), che effettui il chainload di `/boot/grub/i386-pc/core.img`).

**Nota:** Si consulti [http://www.gnu.org/software/grub/manual/html_node/BIOS-installation.html](http://www.gnu.org/software/grub/manual/html_node/BIOS-installation.html) per ulteriori informazioni.

##### Installazione su disco

**Nota:** Questo metodo tratta l'installazione di GRUB in un disco già partizionato (con MBR o GPT), GRUB installato in `/boot/grub` e il relativo codice installato nella regione di 440 byte del MBR (non è da confondere con la tabella partizioni MBR). Per l'installazione su dischi partitionless (super-floppy), si faccia riferimento a [#Installazione su una partizione o su un disco partitionless](#Installazione_su_una_partizione_o_su_un_disco_partitionless).

Per installare `grub` nella regione di 440 byte relativa al boot code, chiamata anche Master Boot Record, popolare la directory `/boot/grub`, generare il `/boot/grub/i386-pc/core.img` e inserirlo nel gap di 31KiB (la dimensione varia a seconda dell'allineamento delle partizioni) post-MBR (o nella partizione di boot del BIOS nel caso di sistemi partizionati con GPT, identificata tramite il flag `grub_bios` in parted e con il codice `EF02` in gdisk) si esegua:

```
# grub-install --target=i386-pc --recheck --debug /dev/sd*x*
# grub-mkconfig -o /boot/grub/grub.cfg

```

**Nota:** L'opzione `--target=i386-pc` indica a `grub-install` di effettuare un'installazione per sistemi BIOS, ed è consigliato specificarla sempre per evitare ambiguità durante l'installazione.

Se si utilizza [LVM](/index.php/LVM_(Italiano) "LVM (Italiano)") per la propria partizione di `/boot`, è possibile installare GRUB su più dischi fissi.

##### Installazione su chiavetta USB

Si assuma che la prima partizione della propria chiavetta USB sia formattata in FAT32 e che tale partizione sia `/dev/sdy1`:

```
#  mkdir -p /mnt/usb ; mount /dev/sdy1 /mnt/usb 
# grub-install --target=i386-pc --recheck --debug --boot-directory=/mnt/usb/boot /dev/sdy
# grub-mkconfig -o /mnt/usb/boot/grub/grub.cfg

```

```
# opzionale, backup dei file di configurazione per grub.cfg
# mkdir -p /mnt/usb/etc/default
# cp /etc/default/grub /mnt/usb/etc/default
# cp -a /etc/grub.d /mnt/usb/etc

```

```
#  sync ; umount /mnt/usb

```

##### Installazione su una partizione o su un disco partitionless

**Nota:** GRUB non incoraggia gli utenti ad effettuare l'installazione nel boot sector di una partizione o su un disco partitionless, al contrario di quanto fanno GRUB Legacy o syslinux. Questa opzione non è consigliata nemmeno dagli sviluppatori di Arch Linux.

Per installare GRUB nel boot sector di una partizione o su un disco senza partizioni (es. superfloppy), si esegua (si assume che il dispositivo sia `/dev/sdaX` e che corrisponda alla partizione di `/boot`):

```
# chattr -i /boot/grub/i386-pc/core.img
# grub-install --target=i386-pc --recheck --debug --force /dev/sdaX
# chattr +i /boot/grub/i386-pc/core.img
```

**Nota:**

*   `/dev/sda` viene usato a titolo di esempio: sostituirlo con il valore corretto in caso fosse diverso.
*   L'opzione `--target=i386-pc` indica a `grub-install` di effettuare un'installazione per sistemi BIOS, ed è consigliato specificarla sempre per evitare ambiguità durante l'installazione.

Sarà necessaria l'opzione `--force` per consentire l'uso delle blocklists, mentre non si dovrà usare `--grub-setup=/bin/true`, che equivale a generare il solo `core.img`.

Si riceveranno dei messaggi d'avvertimento che servono a spiegare i rischi di questo approccio:

```
/sbin/grub-setup: warn: Attempting to install GRUB to a partitionless disk or to a partition.  This is a BAD idea.
/sbin/grub-setup: warn: Embedding is not possible.  GRUB can only be installed in this setup by using blocklists. 
However, blocklists are UNRELIABLE and their use is discouraged.

```

Senza l'opzione `--force`, si riceverà il esguente errore e `grub-setup` non installerà il proprio codice nel MBR.

```
/sbin/grub-setup: error: will not proceed with blocklists

```

Specificando `--force`, invece, si dovrebbe ottenere:

```
Installation finished. No error reported.

```

`grub-setup` non effettua automaticamente questa operazione in caso di installazione del boot loader su una partizione, oppure su un disco partitionless, poichè lo stesso fa affidamento sulle embedded blocklists nel settore di boot della partizione per individuare il `/boot/grub/i386-pc/core.img` e il percorso della directory `/boot/grub`. I settori contenenti i files sopra menzionati potrebbero cambiare in caso di alterazione della partizione (in caso di copia o eliminazione di files, eccetera). Per ulteriori informazioni si veda [https://bugzilla.redhat.com/show_bug.cgi?id=728742](https://bugzilla.redhat.com/show_bug.cgi?id=728742).

La soluzione proposta è quella di impostare il flag immutable al `/boot/grub/i386-pc/core.img`, in modo che la posizione del `core.img` sul disco non venga alterata. Tale flag deve essere impostata solo se `grub` viene installato su una partizione o su un disco partitionless, e NON in caso di semplice installazione nel MBR o di generazione del `core.img`.

Sfortunatamente il `grub.cfg` generato non contiene gli UUID corretti, anche se non viene visualizzato nessun messaggio di errore (si veda [https://bbs.archlinux.org/viewtopic.php?pid=1294604#p1294604](https://bbs.archlinux.org/viewtopic.php?pid=1294604#p1294604))

Per risolvere il problema si esegua:

```
# mount /dev/sdxY /mnt        # Partizione root
# mount /dev/sdxZ /mnt/boot  # Partizione /boot (se in uso)
# arch-chroot /mnt
# pacman -S linux
# grub-mkconfig -o /boot/grub/grub.cfg

```

##### Generazione del solo core.img

Per popolare la directory `/boot/grub` e generare un `/boot/grub/i386-pc/core.img` SENZA installare GRUB nel MBR, si aggiunga `--grub-setup=/bin/true` a `grub-install`:

```
# modprobe dm-mod
# grub-install --target=i386-pc --grub-setup=/bin/true --recheck --debug /dev/sda

```

**Nota:**

*   `/dev/sda` viene usato a titolo di esempio: sostituirlo con il valore corretto in caso fosse diverso.
*   L'opzione `--target=i386-pc` indica a `grub-install` di effettuare un'installazione per sistemi BIOS, ed è consigliato specificarla sempre per evitare ambiguità durante l'installazione.

Sarà quindi possibile effettuare il chainload del `core.img` di GRUB da GRUB Legacy o da syslinux come fosse un kernel Linux o un kernel multiboot.

### Sistemi UEFI

**Nota:** I firmware UEFI non sono implementati in modo consistente tra i vari produttori di hardware. Gli esempi proposti di seguito sono pensati per funzionare con il maggior numero possibile di sistemi UEFI. Se si dovessero riscontrare problemi nonostante si siano seguiti i passaggi è consigliabile raccogliere informazioni dettagliate sulla propria configurazione hardware, specialmente quando si riesce a risolvere il problema. A questo scopo, è stata creata una pagina con [esempi per GRUB EFI](/index.php/GRUB_EFI_Examples "GRUB EFI Examples").

Si installino i pacchetti [grub](https://www.archlinux.org/packages/?name=grub), [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) (per la manipolazione di partizioni UEFI dopo l'installazione) ed [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) (per la creazione di file `.efi` avviabili, utilizzati dallo script di installazione di GRUB).

La semplice installazione del pacchetto non aggiornerà il file `core.efi` e il moduli di GRUB nella partizione UEFI. Sarà necessario aggiornarli manualmente usando lo script di installazione di GRUB, come spiegato sotto.

#### Metodo di installazione consigliato

**Nota:** I comandi seguenti assumono che si stia installando GRUB su sistemi a 64 bit. (`x86_64-efi`) Per sistemi i686 si sostituisca ogni occorrenza di `x86_64-efi` con `i386-efi`. Sarà inoltre necessario assicurarsi che il supporto di installazione sia stato avviato in modalità UEFI e non Legacy, altrimente l'installazione potrebbe non andare a buon fine.

Assicurarsi che la partizione UEFI sia stata montata (ad esempio creata come `/boot` o `/boot/efi`). GRUB non pone limitazioni sul punto di mount della partizione, perciò si è liberi di scegliere quello che si preferisce. Una volta montata la partizione, si esegua il comando di cui sotto per installare l'applicazione UEFI di GRUB in `$esp/EFI/grub`, installarne i moduli in `/boot/grub/x86_64-efi` e copiare l'immagine avviabile `grubx64.efi` in `$esp/EFI/arch_grub`:

```
# grub-install --target=x86_64-efi --efi-directory=$esp --bootloader-id=arch_grub --recheck --debug

```

**Nota:**

*   Se si riscontrano problemi nell'utilizzo di `grub-install` e lo script ci consiglia di caricare il modulo efivars, si provi con [Unified Extensible Firmware Interface#Switch_to_efivarfs](/index.php/Unified_Extensible_Firmware_Interface#Switch_to_efivarfs "Unified Extensible Firmware Interface")
*   Se si sta installando GRUB in un ambiente chroot su un sistema che utilizza LVM è possibile che vengano visualizzati messaggi simili a questo: `/run/lvm/lvmetad.socket: connect failed: No such file or directory` o `WARNING: failed to connect to lvmetad: No such file or directory. Falling back to internal scanning.`.

Questi messaggi sono causati dalla mancanza della directory `/run` nell'ambiente di chroot ma non pregiudicano l'avvio del sistema, percui è possibile proseguire tranquillamente con l'installazione.

*   Se non vengono specificate le opzioni `--target` o `--directory`, `grub-install` non riuscirà a determinare il tipo di firmware sul quale GRUB verrà installato, mostrando perciò il seguente messaggio d'errore: `source_dir doesn't exist. Please specify --target or --directory`.
*   Le opzioni `--efi-directory` e `--botloader-id` sono specifiche di GRUB UEFI. `--efi-directory` indica il punto di mount della partizione EFI di sistema e sostituisce la vecchia opzione `--root-directory`, deprecata. `--bootloader-id` contiene il percorso alla directory che ospita il file `grubx64.efi`.
*   Si noti l'assenza di un riferimento a qualsivoglia disco rigido (es. `/dev/sda`) durante l'esecuzione di `grub-install`, a differenza di quanto avviene per sistemi BIOS. Eventuali riferimenti a dischi rigidi saranno ignorati dallo script di installazione, in quanto i bootloader UEFI non utilizzano MBR o i boot sector delle partizioni.

A questo punto, GRUB è stato installato. Non dimenticarsi di [generare il file di configurazione principale](#Generazione_del_file_di_configurazione_principale).

##### Workaround per alcuni firmware UEFI

Alcuni firmare UEFI richiedono che il file `.efi` avviabile abbia un nome ben definito e si trovi in una posizione specifica: `$esp/EFI/boot/bootx64.efi` (dove `$esp` corrisponde al punto di mount della partizione UEFI). In caso non si rispettino queste regole il sistema non riuscirà ad avviarsi. Si noti che questi accorgimenti non creano problemi con altri firmware, e sono pertanto da considerarsi come il metodo di installazione ufficiale.

Creare la cartella richiesta, quindi copiare il file `.efi` di GRUB rinominandolo nel modo corretto:

```
# mkdir $esp/EFI/boot
# cp $esp/EFI/arch_grub/grubx64.efi  $esp/EFI/boot/bootx64.efi

```

##### Metodo alternativo

Generalmente, GRUB posiziona i propri files, compresi quelli di configurazione, in `/boot`, a prescindere dal punto di mount della partizione EFI di sistema.

Se si desidera memorizzare tali file nella partizione EFI di sistema, si aggiunga `--boot-directory=$esp` al comando `grub-install`:

```
# grub-install --target=x86_64-efi --efi-directory=$esp --bootloader-id=grub --boot-directory=$esp --recheck --debug

```

Quanto sopra include tutti i files di GRUB in `$esp/grub`, invece di utilizzare `/boot/grub`. Quando si utilizza questo metodo, assicurarsi che `grub-mkconfig` generi il file di configurazione nella posizione corretta:

```
# grub-mkconfig -o $esp/grub/grub.cfg

```

Il resto della configurazione è identica.

#### Creare una voce per GRUB nel Firmware Boot Manager

Lo script `grub-install` cerca di creare automaticamente una voce di menù nel boot manager. Se ciò non dovesse avvenire, si consulti [UEFI#efibootmgr](/index.php/UEFI#efibootmgr "UEFI") per istruzioni su come utilizzare `efibootmgr` per creare una voce.

In ogni caso, il problema è solitamente relativo al mancato avvio dell'immagine di installazione in modalità UEFI, come descritto in [Unified Extensible Firmware Interface#Creare un dispositivo USB avviabile con UEFI dalla ISO](/index.php/Unified_Extensible_Firmware_Interface_(Italiano)#Creare_un_dispositivo_USB_avviabile_con_UEFI_dalla_ISO "Unified Extensible Firmware Interface (Italiano)").

#### GRUB Standalone

È possibile creare una applicazione EFI standalone (grubx64_standalone.efi) che comprende tutti i moduli necessari in un archivio tar al suo interno, eliminando di fatto, la necessità di avere una directory separata contenente tutti i moduli UEFI di GRUB ed altri files ad essi relativi. Per raggiungere l'obiettivo, verrà utilizzato il comando `grub-mkstandalone`, incluso in [grub](https://www.archlinux.org/packages/?name=grub):

```
# echo 'configfile ${cmdpath}/grub.cfg' > /tmp/grub.cfg                                ## utilizzare apici singoli, ${cmdpath}/grub.cfg dovrebbe essere lasciato così com'è
# grub-mkstandalone -d /usr/lib/grub/x86_64-efi/ -O x86_64-efi --modules="part_gpt part_msdos" --fonts="unicode" --locales="en@quot" --themes="" -o "$esp/EFI/grub/grubx64_standalone.efi"  "boot/grub/grub.cfg=/tmp/grub.cfg" -v

```

Si copi quindi il file di configurazione di GRUB in `$esp/EFI/grub/grub.cfg` e si crei una voce nell'UEFI Boot Manager per il file `$esp/EFI/grub/grubx64_standalone.efi` utilizzando [efibootmgr](/index.php/Unified_Extensible_Firmware_Interface_(Italiano)#efibootmgr "Unified Extensible Firmware Interface (Italiano)").

**Nota:** L'opzione `--modules="part_gpt part_msdos"` (doppi apici compresi) è necessaria affinchè `${cmdpath`} funzioni correttamente.

**Attenzione:** Potrebbe capitare che il file `grub.cfg` non venga caricato a causa della mancanza dello slash finale da `${cmdpath`} (es. `(hd1,msdos2)EFI/Boot` invece di `(hd1,msdos2)/EFI/Boot`), e si venga lasciati nella shell di GRUB. Se si ha questo problema si verifichi il contenuto della variabile `${cmdpath}` (`echo ${cmdpath}` ) e si proceda al caricamento manuale del file di configurazione (es. `configfile (hd1,msdos2)/EFI/Boot/grub.cfg`).

##### GRUB Standalone - Informazioni tecniche

L'applicazione EFI di GRUB assume che il relativo file di configurazione si trovi in `${prefix}/grub.cfg`. Tuttavia, nel file dell'applicazione Standalone, `${prefix}` è contenuto all'interno di un archivio tar dentro al suddetto file (identificato nell'ambiente GRUB come `"(memdisk)"`, senza doppi apici). L'archivio contiene tutti i files che normalmente si troverebbero sotto `/boot/grub` nel caso di un'installazione di GRUB EFI classica.

A causa dell'embedding del contenuto di `/boot/grub` nell'immagine standalone, essa è completamente indipendente dal contenuto di una directory `/boot/grub` esterna. Ne consegue che per l'immagine EFI Standalone `${prefix}==(memdisk)/boot/grub`, quindi il file di configurazione dovrà trovarsi in `${prefix}/grub.cfg==(memdisk)/boot/grub/grub.cfg`.

Per fare in modo che l'immagine EFI Standalone legga un `grub.cfg` esterno posizionato nella stessa directory dell'immagine (identificata nell'ambiente GRUB come `${cmdpath}` , verrà creato un file `/tmp/grub.cfg` che costringe grub ad utilizzare `${cmdpath}/grub.cfg` come file di configurazione (il comando che esegue questa operazione è `configfile ${cmdpath}/grub.cfg`, contenuto in `(memdisk)/boot/grub/grub.cfg`). Infine, si indica a `grub-mkstandalone` di copiare il file `/tmp/grub.cfg` in `${prefix}/grub.cfg` (ovvero `(memdisk)/boot/grub/grub.cfg`) utilizzando l'opzione `"/boot/grub/grub.cfg=/tmp/grub.cfg"`.

Così facendo, l'immagine Efi Standalone e il relativo `grub.cfg` possono essere memorizzati in qualsiasi directory della partizione EFI di sistema (a patto che i due file si trovino nella stessa directory), rendendoli di fatto portabili.

## Generazione del file di configurazione principale

Dopo l'installazione sarà necessario generare il file di configurazione principale `grub.cfg`. Il processo di creazione del suddetto file può essere influenzato dalle opzioni contenute in `/etc/default/grub` e dagli script in `/etc/grub.d`. È possibile reperire ulteriori informazioni leggendo i paragrafi [#Configurazione di base](#Configurazione_di_base) o [#Configurazione avanzata](#Configurazione_avanzata).

**Nota:** Si ricordi che sarà necessario rigenerare il file `grub.cfg` dopo ogni cambiamento ad `/etc/default/grub` o ai files in `/etc/grub.d/*`.

Utilizzare il tool *grub-mkconfig* per generare il `grub.cfg`:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

**Nota:**

*   Il percorso al file di configurazione è `/boot/grub/grub.cfg`, e NON `/boot/grub/i386-pc/grub.cfg`.
*   Se si sta cercando di effettuare questa operazione da dentro un ambiente di chroot o da un container `systemd-nspawn`, è possibile che `grub-probe` mostri un errore relativo all'impossibilità di ottenere il path di `/dev/sdaX`. In questo caso si provi ad utilizzare `arch-chroot` come spiegato in [questo](https://bbs.archlinux.org/viewtopic.php?pid=1225067#p1225067) thread.
*   Quando si genera il file di configurazione di GRUB su un sistema LVM dall'interno di un ambiente di chroot (anche *arch-chroot*, utilizzato durante l'installazione), è possibile che vengano visualizzati messaggi come `/run/lvm/lvmetad.socket: connect failed: No such file or directory` o `WARNING: failed to connect to lvmetad: No such file or directory. Falling back to internal scanning.`. Ciò è dovuto alla mancanza di `/run` nell'ambiente di chroot. Tali messaggi non impediranno al sistema di avviarsi, a patto che tutti i passaggi siano stati completati correttamente, quindi è possibile procedere con l'installazione.

Di default, lo script di generazione aggiunge automaticamente le voci di menù per Arch Linux a qualsiasi configurazione venga generata, mentre ciò non accade per eventuali voci relative ad altri sistemi operativi. Su sistemi BIOS, si installi il pacchetto [os-prober](https://www.archlinux.org/packages/?name=os-prober), che individua i sistemi operativi installati sulla macchina e li aggiunge al `grub.cfg` durante l'esecuzione di `grub-mkconfig`. Si veda [#Dual-booting](#Dual-booting) per eventuali configurazioni avanzate.

### Conversione del file di configurazione di GRUB Legacy al nuovo formato

Se `grub-mkconfig` non funziona, si converta il proprio `/boot/grub/menu.lst` nel `/boot/grub/grub.cfg` eseguendo:

```
# grub-menulst2cfg /boot/grub/menu.lst /boot/grub/grub.cfg

```

**Nota:** Questa operazione funziona solamente su sistemi BIOS.

Ad esempio:

 `/boot/grub/menu.lst` 
```
default=0
timeout=5

title  Arch Linux Stock Kernel
root   (hd0,0)
kernel /vmlinuz-linux root=/dev/sda2 ro
initrd /initramfs-linux.img

title  Arch Linux Stock Kernel Fallback
root   (hd0,0)
kernel /vmlinuz-linux root=/dev/sda2 ro
initrd /initramfs-linux-fallback.img

```
 `/boot/grub/grub.cfg` 
```
set default='0'; if [ x"$default" = xsaved ]; then load_env; set default="$saved_entry"; fi
set timeout=5

menuentry 'Arch Linux Stock Kernel' {
  set root='(hd0,1)'; set legacy_hdbias='0'
  legacy_kernel   '/vmlinuz-linux' '/vmlinuz-linux' 'root=/dev/sda2' 'ro'
  legacy_initrd '/initramfs-linux.img' '/initramfs-linux.img'
}

menuentry 'Arch Linux Stock Kernel Fallback' {
  set root='(hd0,1)'; set legacy_hdbias='0'
  legacy_kernel   '/vmlinuz-linux' '/vmlinuz-linux' 'root=/dev/sda2' 'ro'
  legacy_initrd '/initramfs-linux-fallback.img' '/initramfs-linux-fallback.img'
}

```

Se si è riavviato il sistema dimenticandosi di creare il `/boot/grub/grub.cfg`, si eseguano questi comandi nella shell di GRUB che apparirà al riavvio:

```
sh:grub> insmod legacycfg
sh:grub> legacy_configfile ${prefix}/menu.lst

```

Procedere quindi all'avvio di Arch Linux e si generi il file `/boot/grub/grub.cfg`.

## Configurazione di base

Questa sezione copre le sole modifiche al file `/etc/default/grub`. Si veda [#Configurazione avanzata](#Configurazione_avanzata) per ulteriori approfondimenti.

**Nota:** Ricordarsi di [rigenerare](#Generazione_del_file_di_configurazione_principale) il file di configurazione principale dopo qualsiasi cambiamento ad `/etc/default/grub`.

#### Argomenti aggiuntivi

Se si ha la necessità di passare dei parametri particolari all'immagine del kernel, è necessario inserirli nelle variabili `GRUB_CMDLINE_LINUX` e `GRUB_CMDLINE_LINUX_DEFAULT` contenute nel file `/etc/default/grub`. I valori delle due variabili vengono inseriti uno di seguito all'altro per le voci di avvio standard. Per quanto riguarda la generazione delle voci di avvio di ripristino, viene utilizzato solamente `GRUB_CMDLINE_LINUX`.

Non è necessario utilizzarli entrambi, ma può risultare utile: ad esempio, è possibile abilitare il resume dopo l'ibernazione tramite `GRUB_CMDLINE_LINUX_DEFAULT="resume=/dev/sdaX quiet"` dove `sdaX` indica la propria partizione di swap.

In questo modo verrebbe generata una voce di ripristino senza il supporto al resume e senza il parametro `quiet` che elimina i messaggi del kernel durante il boot. Di contro, la voce d'avvio standard mantiene i parametri di cui sopra.

Per generare la voce di ripristino è necessario commentare l'opzione `GRUB_DISABLE_RECOVERY=true` in `/etc/default/grub`.

E' anche possibile utilizzare `GRUB_CMDLINE_LINUX="resume=/dev/disk/by-uuid/${swap_uuid}"`, dove `${swap_uuid`} si riferisce all'[uuid](/index.php/Persistent_block_device_naming_(Italiano) "Persistent block device naming (Italiano)") della propria partizione di swap.

Si veda [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") per ulteriori informazioni.

### Configurazione dell'aspetto

In GRUB è possibile cambiare l'aspetto del menu. Ci si assicuri di aver inizializzato il terminale grafico di GRUB (gfxterm), usando una modalità video appropriata (gfxmode). Ulteriori informazioni sono reperibili nella sezione [#Correggere l'errore di GRUB "no suitable mode found"](#Correggere_l.27errore_di_GRUB_.22no_suitable_mode_found.22). La modalità video impostata di seguito, verrà passata al kernel via `gfxpayload`; di conseguenza, questa sarà richiesta affinchè ogni configurazione dell'aspetto abbia effetto.

#### Impostare la risoluzione del framebuffer

GRUB può impostare il framebuffer sia per sé stesso che per il kernel. Il vecchio parametro `vga=` è deprecato. Il metodo consigliato è modificare `/etc/default/grub` come segue:

```
GRUB_GFXMODE=1024x768x32
GRUB_GFXPAYLOAD_LINUX=keep
```

È possibile specificare diverse risoluzioni, incluso il valore di default `auto`. È quindi consigliabile che la variabile `GRUB_GFXMODE` abbia un valore simile a `GRUB_GFXMODE=<risoluzione desiderata>,<fallback, ad esempio 1024x768>,auto`. Per ulteriori informazioni, consultare la [documentazione di GRUB relativa a gfxmode](https://www.gnu.org/software/grub/manual/html_node/gfxmode.html#gfxmode). L'opzione [gfxpayload](https://www.gnu.org/software/grub/manual/html_node/gfxpayload.html#gfxpayload) farà si che il kernel mantenga la risoluzione.

**Nota:** È possibile utilizzare solamente le risoluzioni che la scheda grafica supporta tramite le [estensioni VESA BIOS](https://en.wikipedia.org/wiki/VESA_BIOS_Extensions "wikipedia:VESA BIOS Extensions"). Per ottenere un elenco delle risoluzioni supportate, si installi [hwinfo](https://www.archlinux.org/packages/?name=hwinfo) e si esegua `hwinfo --framebuffer` come utente root. In alternativa, si entri nella riga di comando di GRUB e si esegua `vbeinfo`.

Se quanto sopra non funziona, è possibile utilizzare il vecchio parametro `vga=`. Lo si aggiunga semplicemente alla variabile `"GRUB_CMDLINE_LINUX_DEFAULT="` in `/etc/default/grub`: ad esempio: `"GRUB_CMDLINE_LINUX_DEFAULT="quiet splash vga=792"` imposterà una risoluzione di `1024x768`.

#### Hack 915resolution

Se si stanno utilizzando schede grafiche Intel, può accadere che nè `# hwinfo --framebuffer` nè `vbeinfo` mostrino la risoluzione desiderata. In questo caso, è possibile utilizzare l'hack proposto, che modificherà temporaneamente il BIOS della scheda video aggiungendo la risoluzione richiesta. Si veda la home page di [915resolution](http://915resolution.mango-lang.org/).

Innanzitutto è necessario scegliere una modalità video da modificare più tardi. Si avvii quindi `915resolution` nella shell di GRUB:

 `sh:grub> 915resolution -l` 
```
Intel 800/900 Series VBIOS Hack : version 0.5.3
[...]
Mode 30 : 640x480, 8 bits/pixel
[...]

```

L'obiettivo è quello di sovrascrivere la modalità 30 con la risoluzione `1440x900`:

 `/etc/grub/00_header` 
```
[...]
**915resolution 30 1440 900 # linea aggiunta**
set gfxmode=${GRUB_GFXMODE}
[...]

```

Sarà ora necessario impostare il valore di `GRUB_GFXMODE`, come spiegato in precedenza e rigenerare il file di configurazione di GRUB:

```
# grub-mkconfig -o /boot/grub/grub.cfg
# reboot

```

#### Immagine di sfondo e caratteri bitmap

GRUB supporta le immagini di sfondo e i caratteri bitmap nel formato `pf2`. Il font unifont è incluso nel pacchetto [grub](https://www.archlinux.org/packages/?name=grub) con nome `unicode.pf2` oppure, in soli caratteri ASCII con nome `ascii.pf2`.

I formati di immagine supportati includono tga, png e jpeg, a patto che i rispettivi moduli siano caricati. La risoluzione massima applicabile dipende dall'hardware in uso.

Prima di procedere, seguire quanto indicato in [#Impostare la risoluzione del framebuffer](#Impostare_la_risoluzione_del_framebuffer).

Si modifichi quindi il file `/etc/default/grub` come segue:

```
GRUB_BACKGROUND="/boot/grub/miaimmagine"
#GRUB_THEME="/path/to/gfxtheme"
GRUB_FONT="/path/to/font.pf2"

```

**Nota:** Se si è installato GRUB in una partizione separata, `/boot/grub/miaimmagine` diventa `/grub/miaimmagine`.

Per applicare le modifiche al `grub.cfg`, si esegua:

```
grub-mkconfig -o /boot/grub/grub.cfg

```

Se l'inserimento dell'immagine è avvenuto con successo, dovrebbe essere visualizzato il messaggio `Found background image...`, durante l'esecuzione del precedente comando. Se questo non accade, significa che l'immagine non è stata incorporata nel grub.cfg.

In tal caso, si controlli che:

*   il percorso e il nome dell'immagine in `/etc/default/grub` siano corretti
*   l'immagine abbia dimensioni e formato adeguati (tga, png, png a 8 bit)
*   l'immagine sia stata salvata in modalità RGB e non sia indicizzata
*   la modalità console non sia stata abilitata in /etc/default/grub
*   il comando `grub-mkconfig` sia stato eseguito per inserire le informazioni relative allo sfondo nell file `/boot/grub/grub.cfg`.

#### Temi

Di seguito viene proposto un esempio per la configurazione di GRUB con il tema Starfield, incluso nel pacchetto fornito con Arch.

Si modifichi `/etc/default/grub`:

```
GRUB_THEME="/usr/share/grub/themes/starfield/theme.txt"

```

Si applichino le modifiche:

```
grub-mkconfig -o /boot/grub/grub.cfg

```

Se il tema è stato applicato correttamente, apparirà a video il messaggio `Found theme: /usr/share/grub/themes/starfield/theme.txt`.

#### Colori del Menù

In GRUB è possibile cambiare i colori del menù. L'elenco dei colori disponibili è reperibile [qui](http://www.gnu.org/software/grub/manual/html_node/Theme-file-format.html#Theme-file-format). Di seguito, un esempio:

Si modifichi `/etc/default/grub` come segue:

```
GRUB_COLOR_NORMAL="light-blue/black"
GRUB_COLOR_HIGHLIGHT="light-cyan/blue"
```

Per rendere effettivi i cambiamenti si esegua:

```
grub-mkconfig -o /boot/grub/grub.cfg

```

#### Menù nascosto

Una delle caratteristiche proprie di GRUB è la possibilità di nascondere il menù e renderlo visibile attraverso la pressione del tasto `Esc`, se necessario. È anche possibile decidere se visualizzare o meno il countdown.

Si modifichi `/etc/default/grub`. Nell'esempio che segue, il countdown è stato impostato a 5 secondi e reso visibile all'utente:

```
GRUB_TIMEOUT=0
GRUB_HIDDEN_TIMEOUT=5
GRUB_HIDDEN_TIMEOUT_QUIET=false
```

La variabile `GRUB_HIDDEN_TIMEOUT` specifica quanti secondi aspettare prima di mostrare il menu. Sarà necessario impostare `GRUB_TIMEOUT=0` se lo si vuole nascondere.

Si esegua:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

#### Disabilitare il framebuffer

Se si usano i driver proprietari NVIDIA, potrebbe essere necessario disabilitare il framebuffer di GRUB, poichè potrebbe interferire con il driver.

Per disabilitarlo, si modifichi `/etc/default/grub` decommentando la seguente linea:

```
GRUB_TERMINAL_OUTPUT=console

```

Si esegua poi:

```
grub-mkconfig -o /boot/grub/grub.cfg

```

Se si vuole comunque avviare GRUB in framebuffer è possibile tornare in modalità testuale prima dell'avvio del kernel. A tal proposito si modifichi la relativa variabile in `/etc/default/grub`:

```
GRUB_GFXPAYLOAD_LINUX=text

```

Si rigeneri quindi il file di configurazione come visto sopra.

### Nomenclatura permanente dei dispositivi a blocchi

Un modo per identificare con una [nomenclatura persistente i dispositivi a blocchi](/index.php/Persistent_block_device_naming_(Italiano) "Persistent block device naming (Italiano)") è quello di utilizzare degli UUID univoci per le partizioni, invece dei vecchi valori `/dev/sd*`. I vantaggi sono spiegati nel link fornito sopra.

GRUB utilizza di default gli UUID dei filesystems per identificare in modo permanente i dispositivi a blocchi.

**Nota:** È necessario rigenerare il file `/boot/grub/grub.cfg` affinchè vengano aggiornati gli UUID ogni volta che una partizione viene ridimensionata o formattata. Si tenga a mente questo particolare ogni volta che si modificano le partizioni con un LiveCD.

L'uso degli UUID è controllato da un'opzione in `/etc/default/grub`:

```
# GRUB_DISABLE_LINUX_UUID=true

```

In ogni caso, ci si ricordi di applicare i cambiamenti:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

### Richiamare l'ultimo sistema avviato

GRUB è in grado di ricordarsi l'ultimo sistema avviato ed usarlo come default la prossima volta che si eseguirà il boot. Questa funzionalità è utile se si dispone di kernel multipli (ad esempio il kernel corrente di Arch e il LTS come fallback) o più sistemi operativi. Si modifichi `/etc/default/grub` e si cambi il valore di `GRUB_DEFAULT`:

```
GRUB_DEFAULT=saved

```

Ciò consentirà a GRUB di avviare il sistema operativo salvato. Per abilibare il salvataggio, si aggiunga la linea seguente ad `/etc/default/grub`:

```
GRUB_SAVEDEFAULT=true

```

**Nota:** Le voci di menù aggiunte manualmente in `/etc/grub.d/40_custom` o `/boot/grub/custom.cfg` (ad esempio Windows), richiederanno l'opzione `savedefault`.

Ci si ricordi di [rigenerare](#Generare_un_file_di_configurazione) il file di configurazione di GRUB.

### Cambiare la voce di menu predefinita

Per cambiare la voce selezionata in modo predefinito, si modifichi la variabile `GRUB_DEFAULT` in `/etc/default/grub`:

Utilizzando numeri progressivi:

```
GRUB_DEFAULT=0

```

GRUB enumera le voci che appaiono nel menu partendo da zero, il che significa che 0 selezionerà la prima voce, 1 la seconda e così via.

Oppure utilizzando i titoli delle voci:

```
GRUB_DEFAULT='Arch Linux, with Linux core repo kernel'

```

**Nota:** Ricordarsi di [rigenerare](#Generare_un_file_di_configurazione) il file di configurazione di GRUB.

### Disabilitare il sottomenu

Se si hanno più kernel installati (ad esempio linux e linux-lts), `grub-mkconfig` li raggrupperà in un sottomenù.

Se non si desidera utilizzare questa funzionalità si aggiunga la seguente linea al file `/etc/default/grub`:

```
GRUB_DISABLE_SUBMENU=y

```

### Cifratura della partizione root

Per far sì che GRUB passi automaticamente al kernel i parametri necessari per la cifratura della root, si aggiunga `cryptdevice=/dev/device:etichetta` a `GRUB_CMDLINE_LINUX` in `/etc/default/grub`.

Si veda inoltre [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") per ulteriori informazioni.

**Suggerimento:** Se si sta effettuando l'aggiornamento da GRUB Legacy, si controlli il file `/boot/grub/menu.lst.pacsave` per l'identificativo dispositivo o l'etichetta corretta da inserire. Si cerchi dopo la riga `kernel /vmlinuz-linux`.

Un esempio con la root mappata su `/dev/mapper/root`:

```
GRUB_CMDLINE_LINUX="cryptdevice=/dev/sda2:root"

```

Se si riscontrano problemi nell'effettuare il boot con `dm-crypt` su sistemi UEFI-GPT Si disabiliti l'uso degli UUID per il file system di root:

```
GRUB_DISABLE_LINUX_UUID=true

```

Ed assicurarsi di non utilizzare riferimenti agli UUID (ad esempio, utilizzare `/dev/sdb3` al posto di `/dev/disk/by-uuid/42d934c7-6199-4f11-9e01-807530111df6 o UUID=42d934c7-6199-4f11-9e01-807530111df6`).

Rigenerare quindi il file di configurazione di GRUB.

### Effettuare il boot di una voce non default per una sola volta

Il comando `grub-reboot` è molto utile per avviare una voce diversa da quella di default. GRUB caricherà la voce specificata come primo argomento del comando e il sistema operativo corrispondente verrà avviato al prossimo avvio. Si noti che GRUB effettuerà il boot della scelta di default per tutti i riavvii successivi a quello effettuato subito dopo l'esecuzione del comando. Non è necessario modificare il file di configurazione di GRUB o scegliere una voce nel menù di avvio.

**Nota:** Quanto sopra richiede l'opzione `GRUB_DEFAULT=saved` in `/etc/default/grub` (e successiva rigenerazione del `grub.cfg`) o, in caso di un `grub.cfg` scritto manualmente, la linea `set default="${saved_entry}"`.

## Configurazione avanzata

Questa sezione si occupa delle modifiche manuali al `grub.cfg`, della scrittura di script personalizzati in `/etc/grub.d` e di altre impostazioni avanzate.

### Creazione manuale del grub.cfg

**Attenzione:** La modifica manuale di questo file è fortemente sconsigliata. Il `grub.cfg` è generato dal comando `grub-mkconfig`, ed è preferibile modificare il file `/etc/default/grub` o uno degli script contenuti nella cartella `/etc/grub.d`.

Un `grub.cfg` di base contiene le seguenti opzioni:

*   `(hdX,Y)` indica la partizione Y sul disco X. La numerazione delle partizioni parte da 1, mentre quella dei dischi da 0
*   `set default=N` permette di scegliere quale entry avviare in modo predefinito
*   `set timeout=N` indica il limite di tempo in secondi prima che la scelta predefinita venga avviata
*   `menuentry "title" {opzioni`} è un'entry di nome `title`
*   `set root=(hdX,Y)` imposta la partizione di boot, ossia quella contenente il kernel e i moduli di GRUB (non è necessario disporre di una partizione separata: `/boot` può essere contenuta all'interno della partizione di root).

Una configurazione d'esempio:

```
/boot/grub/grub.cfg

```

```
# Config file for GRUB - The GNU GRand Unified Bootloader
# /boot/grub/grub.cfg

# DEVICE NAME CONVERSIONS
#
#  Linux           Grub
# -------------------------
#  /dev/fd0        (fd0)
#  /dev/sda        (hd0)
#  /dev/sdb2       (hd1,2)
#  /dev/sda3       (hd0,3)
#

# Timeout for menu
set timeout=5

# Set default boot entry as Entry 0
set default=0

# (0) Arch Linux
menuentry "Arch Linux" {
set root=(hd0,1)
linux /vmlinuz-linux root=/dev/sda3 ro
initrd /initramfs-linux.img
}

## (1) Windows
#menuentry "Windows" {
#set root=(hd0,3)
#chainloader +1
#}
```

### Dual-booting

**Suggerimento:** Se si desidera che GRUB ricerchi automaticamente i sistemi operativi installati, è necessario installare [os-prober](https://www.archlinux.org/packages/?name=os-prober).

#### Generazione automatica utilizzando il file /etc/grub.d/40_custom e grub-mkconfig

Il modo migliore per aggiungere altre voci è modificare il file `/etc/grub.d/40_custom` oppure `/boot/grub/custom.cfg`, in modo che esse vengano automaticamente aggiunte al `grub.cfg` quando si lancia `grub-mkconfig`. Dopo aver effettuato le modifiche, si esegua:

 `# grub-mkconfig -o /boot/grub/grub.cfg` 

Oppure, per sistemi UEFI-GPT (come descritto nel metodo alternativo):

 `# grub-mkconfig -o /boot/efi/EFI/GRUB/grub.cfg` 

Per generare un `grub.cfg` aggiornato.

Un file `/etc/grub.d/40_custom` generico potrebbe avere una struttura simile a quello postato sotto, creato per un [HP Pavilion 15-e056sl notebook](http://h10025.www1.hp.com/ewfrf/wc/product?cc=us&destPage=product&lc=en&product=5402703&tmp_docname=) con Windows 8 preinstallato. Ogni voce `menuentry` dovrebbe mantenere una struttura simile a quanto segue.

Si noti inoltre che la partizione `/dev/sda2` viene identificata da GRUB come `hd0,gpt2` e `ahci0,gpt2`. Si consulti [GRUB#Voce di menù per Windows installato in modalità UEFI-GPT](/index.php/GRUB#Voce_di_men.C3.B9_per_Windows_installato_in_modalit.C3.A0_UEFI-GPT "GRUB") per ulteriori informazioni.

 `/etc/grub.d/40_custom` 
```
#!/bin/sh
exec tail -n +3 $0
# This file provides an easy way to add custom menu entries.  Simply type the
# menu entries you want to add after this comment.  Be careful not to change
# the 'exec tail' line above.

menuentry "HP / Microsoft Windows 8" {
	echo "Sto avviando HP / Microsoft Windows 8..."
	insmod part_gpt
	insmod fat
	insmod search_fs_uuid
	insmod chain
	search --fs-uuid --no-floppy --set=root --hint-bios=hd0,gpt2 --hint-efi=hd0,gpt2 --hint-baremetal=ahci0,gpt2 763A-9CB6
	chainloader (${root})/EFI/Microsoft/Boot/bootmgfw.efi
}

menuentry "Centro di controllo HP / Microsoft" {
	echo "Sto avviando Centro di controllo HP / Microsoft..."
	insmod part_gpt
	insmod fat
	insmod search_fs_uuid
	insmod chain
	search --fs-uuid --no-floppy --set=root --hint-bios=hd0,gpt2 --hint-efi=hd0,gpt2 --hint-baremetal=ahci0,gpt2 763A-9CB6
	chainloader (${root})/EFI/HP/boot/bootmgfw.efi
}

menuentry "Spegnimento del computer" {
	echo "Sto spegnendo il computer..."
	halt
}

menuentry "Riavvio del computer" {
	echo "Sto riavvinado il computer..."
	reboot
}
```

##### Voce di menù per GNU/Linux

Se l'altra distro è in `/dev/sda2`:

```
menuentry "Other Linux" {
	set root=(hd0,2)
	linux /boot/vmlinuz (si aggiungano altre opzioni da passare al kernel, se richieste)
	initrd /boot/initrd.img (se il kernel lo richiede)
}
```

##### Voce di menù per FreeBSD

Richiede che FreeBSD sia installato su una singola partizione formattata come UFS. Se FreeBSD risiede su `sda4`:

```
menuentry "FreeBSD" {
	set root=(hd0,4)
	chainloader +1
}
```

##### Voce di menù per Windows XP

Se windows è installato in `/dev/sda3`:

**Nota:** Si ricordi che è necessario puntare i comandi `set root` e `chainloader` alla partizione riservata di sistema, ossia quella che crea Windows durante l'installazione, e non alla partizione sulla quale risiede effettivamente Windows. L'esempio trattato sotto funziona se la vostra partizione riservata è `sda3`.

```
menuentry "Windows XP" {
	set root="(hd0,3)"
	chainloader +1
}
```

Se il bootloader di Windows è su un disco rigido differente da quello di GRUB, potrebbe essere necessario ingannare Windows per fargli credere di risiedere nel primo drive. Ciò era possibile utilizzando `drivemap`. Assumendo che GRUB si trovi su `hd0` e Windows su `hd2`, sarà necessario aggiungere la seguente riga dopo `set root`:

 `drivemap -s hd0 hd2` 

##### Voce di menù per Windows installato in modalità UEFI-GPT

**Nota:** Questa voce funzionerà solo se il sistema viene avviato in modalità UEFI e solo se la "bitness" di Windows corrisponde a quella di UEFI. Si noti che tale voce NON funzionerà su GRUB per sistemi BIOS. A tal proposito si legga [qui](/index.php/Windows_and_Arch_Dual_Boot#Windows_UEFI_vs_BIOS_limitations "Windows and Arch Dual Boot") e [qui](/index.php/Windows_and_Arch_Dual_Boot#Bootloader_UEFI_vs_BIOS_limitations "Windows and Arch Dual Boot") per ulteriori informazioni.

```
if [ "${grub_platform}" == "efi" ]; then
	menuentry "Microsoft Windows Vista/7/8/8.1 x86_64 UEFI-GPT" {
		insmod part_gpt
		insmod fat
		insmod search_fs_uuid
		insmod chain
		search --fs-uuid --set=root $hints_string $fs_uuid
		chainloader /EFI/Microsoft/Boot/bootmgfw.efi
	}
fi

```

Il valore delle variabili `$hints_string` e `$fs_uuid` si ottiene con i seguenti comandi: Per `$fs_uuid`:

```
# grub-probe --target=fs_uuid $esp/EFI/Microsoft/Boot/bootmgfw.efi
1ce5-7f28
```

Per `$hints_string`:

```
# grub-probe --target=hints_string $esp/EFI/Microsoft/Boot/bootmgfw.efi
--hint-bios=hd0,gpt1 --hint-efi=hd0,gpt1 --hint-baremetal=ahci0,gpt1
```

I due comandi di cui sopra assumono che la ESP di Windows sia montata in `$esp`. Si noti che potrebbero esserci differenze tra lettere maiuscole e minuscole nel percorso che identifica la posizione del file EFI di Windows.

##### Voce di menù per lo spegnimento del sistema

```
menuentry "System shutdown" {
	echo "System shutting down..."
	halt
}
```

##### Voce di menù per il riavvio del sistema

```
menuentry "System restart" {
	echo "System rebooting..."
	reboot
}
```

##### Windows installato in modalità BIOS-MBR

**Nota:** GRUB supporta l'avvio diretto di `bootmgr` e il chainload del settore di boot non è più richiesto per avviare Windows su configurazioni BIOS-MBR.

**Attenzione:** Si noti che `bootmgr` è contenuto nella partizione di sistema, non in quella principale che ospita i file di sistema di Windows (C:). Quando si elencano tutti gli UUIDs con `blkid` la partizione viene evidenziata come `LABEL="SYSTEM RESERVED"` o `LABEL="SYSTEM"` ed ha una dimensione che varia dai 100 ai 200 MB, similmente alla partizione di boot di Arch. Si consulti [wikipedia:System_partition_and_boot_partition](https://en.wikipedia.org/wiki/System_partition_and_boot_partition "wikipedia:System partition and boot partition") per ulteriori informazioni.

Per tutto il resto della sezione, si assumerà che la propria partizione di Windows sia `/dev/sda1`. Partizioni differenti varieranno di conseguenza anche il valore di `hd0,msdos1`. Si individui l'UUID della partizione di sistema di windows, dove bootmgr e i suoi files risiedono. Per esempio, se `bootmgr` si trova in `/media/SYSTEM_RESERVED/bootmgr`:

Per Windows Vista/7/8/8.1:

```
# grub-probe --target=fs_uuid /media/SYSTEM_RESERVED/bootmgr
69B235F6749E84CE

```

```
# grub-probe --target=hints_string /media/SYSTEM_RESERVED/bootmgr
--hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1

```

**Nota:** Se si utilizza Windows XP, si sostituisca `bootmgr` con `ntldr` nei comandi di cui sopra. Si noti inoltre che potrebbe non essere presente una partizione di sistema separata: si effettui la ricerca del file NTLDR sulla partizione principale di Windows.

Si aggiunga quindi il codice sotto riportato al file `/etc/grub.d/40-custom` o `/boot/grub/custom.cfg` e si rigeneri il `grub.cfg` con `grub-mkconfig` come spiegato sopra per effettuare il chainload di Windows (XP, Vista, 7 o 8) installato in modalità BIOS-MBR:

**Nota:** Le voci sotto riportate NON funzioneranno su GRUB per sistemi BIOS. A tal proposito si legga [qui](/index.php/Windows_and_Arch_Dual_Boot#Windows_UEFI_vs_BIOS_limitations "Windows and Arch Dual Boot") e [qui](/index.php/Windows_and_Arch_Dual_Boot#Bootloader_UEFI_vs_BIOS_limitations "Windows and Arch Dual Boot") per ulteriori informazioni.

Per Windows Vista/7/8/8.1:

```
if [ "${grub_platform}" == "pc" ]; then
  menuentry "Microsoft Windows Vista/7/8/8.1 BIOS-MBR" {
    insmod part_msdos
    insmod ntfs
    insmod search_fs_uuid
    insmod ntldr     
    search --fs-uuid --set=root --hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1 69B235F6749E84CE
    ntldr /bootmgr
  }
fi
```

Per Windows XP:

```
if [ "${grub_platform}" == "pc" ]; then
  menuentry "Microsoft Windows XP" {
    insmod part_msdos
    insmod ntfs
    insmod search_fs_uuid
    insmod ntldr     
    search --fs-uuid --set=root --hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1 69B235F6749E84CE
    ntldr /bootmgr
  }
fi
```

**Nota:** `nn` dovrebbe avere un valore superiore a `06` affinchè gli script di sistema siano eseguiti per primi.

**Nota:** In alcuni casi (ad esempio se GRUB viene installato prima di Windows 8), potrebbe verificarsi un errore riguardante `\boot\bcd` (codice errore `0xC000000F`) durante l'avvio di Windows. È possibile risolvere il problema avviando la console di ripristino di Windows (si utilizzi il suo disco di installazione) ed eseguendo:
```
x:\>bootrec.exe /fixboot
x:\>bootrec.exe /rebuildbcd

```

**Attenzione:** Non utilizzare `bootrec.exe /Fixmbr`, poichè cancellerebbe GRUB.

Il file `/etc/grub.d/40_custom` può essere utilizzato come template per creare `/etc/grub.d/nn_custom`, dove il numero `nn` definisce l'ordine in cui gli script sono eseguiti, determinando di conseguenza il posizionamento delle voci nel menu di GRUB.

**Nota:** Il numero `nn` dovrebbe avere un valore maggiore di 6, affinchè vengano prima eseguiti altri script necessari.

#### Con Windows usando EasyBCD e NeoGRUB

Poichè NeoGRUB non capisce il nuovo formato dei menu di GRUB, sarà necessario effettuare il chainload di GRUB, sostituendo il contenuto del vostro `C:\NST\menu.lst` con:

```
default 0
timeout 1

```

```
title       Chainload into GRUB v2
root        (hd0,7)
kernel      /boot/grub/i386-pc/core.img

```

### Avviare un'immagine ISO9660 direttamente da GRUB

GRUB supporta l'avvio di immagini ISO attraveso l'utilizzo di dispositivi di loopback. Si veda a tal proposito [Multiboot USB drive#Using GRUB and loopback devices](/index.php/Multiboot_USB_drive#Using_GRUB_and_loopback_devices "Multiboot USB drive").

### LVM

Se si usa [LVM](/index.php/LVM_(Italiano) "LVM (Italiano)") per la propria `/boot`, si aggiunga la seguente linea prima delle varie voci:

```
insmod lvm

```

e si specifichi la propria root nella menuentry in questo modo:

```
set root=lvm/"nome_gruppo_lvm"-"nome_partizione_logica_di_boot_lvm"

```

Esempio:

```
# (0) Arch Linux
menuentry "Arch Linux" {
insmod lvm
set root=lvm/VolumeGroup-lv_boot
# you can only set following two lines
linux /vmlinuz-linux root=/dev/mapper/VolumeGroup-root ro
initrd /initramfs-linux.img
}
```

### RAID

GRUB permette di trattare i volumi in configurazione RAID in modo semplice. Si aggiunga `insmod mdraid` al `grub.cfg` che consentirà di riferirsi al volume in modo nativo. Ad esempio, `/dev/md0` diventa:

```
set root=(md/0)

```

mentre un volume RAID partizionato (es. `/dev/md0p1` diventa:

```
set root=(md/0,1)

```

Per installare GRUB su una partizione `/boot` in RAID1 (o comunque se `/boot` si trova su una partizione root in RAID1) su sistemi con GPT e partizione di boot BIOS ef02, si esegua `grub-install` su ciascuna unità.

Ad esempio:

```
# grub-install --target=i386-pc --recheck --debug /dev/sda && grub-install --target=i386-pc --recheck --debug /dev/sdb

```

Dove l'array RAID1 che ospita la partizione `/boot` è formato da `/dev/sda` e `/dev/sdb`.

### Usare le etichette

È possibile usare le etichette (stringhe che identificano le partizioni in una maniera leggibile dall'utente), usando l'opzione `--label` del comando `search`. Innanzitutto, si apponga un'etichetta alle proprie partizioni:

```
# tune2fs -L *ETICHETTA* *PARTIZIONE*

```

Poi si aggiunga una voce usando le etichette:

```
menuentry "Arch Linux, session texte" {
    search --label --set=root archroot
    linux /boot/vmlinuz-linux root=/dev/disk/by-label/archroot ro
    initrd /boot/initramfs-linux.img
}
```

### Proteggere con una password il menu di GRUB

Se si desidera rendere più sicuro GRUB e fare in modo che nessuno possa cambiare i parametri di boot od usare la riga di comando, è possibile aggiungere un nome utente e password ai files di configurazione di GRUB. A tal fine, si esegua `grub-mkpasswd_pbkdf2`. Si inserisca una password e la si confermi.

 `grub-mkpasswd-pbkdf2` 
```
[...]
Your PBKDF2 is grub.pbkdf2.sha512.10000.C8ABD3E93C4DFC83138B0C7A3D719BC650E6234310DA069E6FDB0DD4156313DA3D0D9BFFC2846C21D5A2DDA515114CF6378F8A064C94198D0618E70D23717E82.509BFA8A4217EAD0B33C87432524C0B6B64B34FBAD22D3E6E6874D9B101996C5F98AB1746FE7C7199147ECF4ABD8661C222EEEDB7D14A843261FFF2C07B1269A
```

Si aggiungano le seguenti stringhe a `/etc/grub.d/40_custom`:

 `/etc/grub.d/40_custom` 
```
set superusers="**username**"
password_pbkdf2 **username** **<password>**
```

Dove a <password> corrisponde la stringa generata con `grub-mkpasswd_pbkdf2`.

Si rigeneri il file di configurazione. La riga di comando e i parametri di boot di GRUB sono ora protetti.

Le impostazioni di cui sopra possono essere rese meno restrittive e personalizzate aggiungendo più utenti, come spiegato nel capitolo "Security" del [manuale di GRUB](https://www.gnu.org/software/grub/manual/grub.html#Security).

### Nascondere il menu di GRUB e farlo apparire alla pressione del tasto Shift

Per ridurre al minimo i tempi di boot è possibile nascondere il menu di GRUB, invece di aspettare lo scadere del timeout. È possibile nascondere il menu di default e farlo apparire solo qualora venga premuto il tasto `Shift` durante l'avvio di GRUB.

Per ottenere questo risultato, aggiungere quanto segue al proprio `/etc/default/grub`:

```
GRUB_FORCE_HIDDEN_MENU="true"

```

Sarà inoltre necessario creare e rendere eseguibile il seguente file:

 `/etc/grub.d/31_hold_shift` 
```
#! /bin/sh
set -e

# grub-mkconfig helper script.
# Copyright (C) 2006,2007,2008,2009  Free Software Foundation, Inc.
#
# GRUB is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# GRUB is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with GRUB.  If not, see <http://www.gnu.org/licenses/>.

prefix="/usr"
exec_prefix="${prefix}"
datarootdir="${prefix}/share"

export TEXTDOMAIN=grub
export TEXTDOMAINDIR="${datarootdir}/locale"

source "${datarootdir}/grub/grub-mkconfig_lib"

found_other_os=

make_timeout () {

  if [ "x${GRUB_FORCE_HIDDEN_MENU}" = "xtrue" ] ; then 
    if [ "x${1}" != "x" ] ; then
      if [ "x${GRUB_HIDDEN_TIMEOUT_QUIET}" = "xtrue" ] ; then
    verbose=
      else
    verbose=" --verbose"
      fi

      if [ "x${1}" = "x0" ] ; then
    cat <<EOF
if [ "x\${timeout}" != "x-1" ]; then
  if keystatus; then
    if keystatus --shift; then
      set timeout=-1
    else
      set timeout=0
    fi
  else
    if sleep$verbose --interruptible 3 ; then
      set timeout=0
    fi
  fi
fi
EOF
      else
    cat << EOF
if [ "x\${timeout}" != "x-1" ]; then
  if sleep$verbose --interruptible ${GRUB_HIDDEN_TIMEOUT} ; then
    set timeout=0
  fi
fi
EOF
      fi
    fi
  fi
}

adjust_timeout () {
  if [ "x$GRUB_BUTTON_CMOS_ADDRESS" != "x" ]; then
    cat <<EOF
if cmostest $GRUB_BUTTON_CMOS_ADDRESS ; then
EOF
    make_timeout "${GRUB_HIDDEN_TIMEOUT_BUTTON}" "${GRUB_TIMEOUT_BUTTON}"
    echo else
    make_timeout "${GRUB_HIDDEN_TIMEOUT}" "${GRUB_TIMEOUT}"
    echo fi
  else
    make_timeout "${GRUB_HIDDEN_TIMEOUT}" "${GRUB_TIMEOUT}"
  fi
}

  adjust_timeout

    cat <<EOF
if [ "x\${timeout}" != "x-1" ]; then
  if keystatus; then
    if keystatus --shift; then
      set timeout=-1
    else
      set timeout=0
    fi
  else
    if sleep$verbose --interruptible 3 ; then
      set timeout=0
    fi
  fi
fi
EOF

```

Si renda eseguibile lo script e si rigeneri il file di configurazione di GRUB:

```
# chmod a+x /etc/grub.d/31_hold_shift
# grub-mkconfig -o /boot/grub/grub.cfg

```

## Combinare UUID e scripting

Se si vogliono usare gli UUID per sopperire al mapping inaffidabile dei dispositivi effettuato dal BIOS, oppure si stanno avendo difficoltà con la sintassi di GRUB, ecco un esempio che usa gli UUID e un piccolo script per far puntare GRUB alle giuste partizioni. Tutto ciò che si dovrà fare, sarà sostituire gli UUID dell'esempio con quelli corretti per il proprio sistema (L'esempio si applica a sistemi con una partizione di boot separata e va modificato di conseguenza in caso di partizioni aggiuntive).

```
menuentry "Arch Linux 64" {
     # Si impostino gli UUID delle proprie partizioni di boot e root
     set the_boot_uuid=ece0448f-bb08-486d-9864-ac3271bd8d07   
     set the_root_uuid=c55da16f-e2af-4603-9e0b-03f5f565ec4a

     # (Nota: In caso non si disponga di una partizione di boot separata, i due UUID saranno uguali)

     # Otteniamo gli identificativi dei dispositivi contenenti le partizioni di boot/root e li impostiamo nelle variabili "grub_boot" e "root"
     search --fs-uuid $the_root_uuid --set=root       
     search --fs-uuid $the_boot_uuid --set=grub_boot

     # Controllo per verificare che boot e root siano uguali
     # Se lo sono, allora aggiungo "/boot" a $grub_root, dal momento che $grub_root è effettivamente la partizione di root
     if [ $the_boot_uuid == $the_root_uuid] ; then
         set grub_boot=$grub_boot/boot
     else
         set grub_boot=($grub_boot)
     fi

     # $grub_boot indica ora il dispositivo corretto e i seguenti comandi saranno in grado di trovare il kernel e l'immagine initrd senza problemi
     linux ($grub_boot)/vmlinuz-linux root=/dev/disk/by-uuid/$uuid_os_root ro
     initrd ($grub_boot)/initramfs-linux.img
 }
```

## Usare la shell

Poichè l'MBR è troppo piccolo per contenere tutti i moduli di GRUB, solo il menù e i comandi fondamentali risiedono lì. La maggior parte delle funzionalità di GRUB è contenuta nei moduli in `/boot/grub`, che sono caricati quando necessario. In caso di errori (ad esempio se viene alterata la tabella delle partizioni), GRUB potrebbe non riuscire ad effettuare il boot, ed avviare una shell al posto del menù classico.

GRUB offre diversi tipi di shell. Se vi sono problemi nella lettura del menu, ma il bootloader è comunque in grado di trovare il disco dove GRUB risiede, è probabile che si sarà lasciati nella shell "normale":

```
sh:grub>

```

In caso di problemi più seri (GRUB non riesce a trovare i files richiesti), potrebbe venir visualizzata la shell di emergenza:

```
grub rescue>

```

La shell di emergenza è una versione ridotta di quella normale, ed offre di conseguenza, un numero ridotto di funzionalità. Si provi a caricare il modulo `normal`, e poi ad avviare la shell classica:

```
grub rescue> set prefix=(hdX,Y)/boot/grub
grub rescue> insmod (hdX,Y)/boot/grub/normal.mod
rescue:grub> normal
```

#### Supporto al Pager

GRUB supporta il pager per rendere agevole la lettura di output lunghi. Si noti che questa funzionalità è disponibile solamente nella shell normale, e non in quella d'emergenza. Per attivarla, si scriva:

```
sh:grub> set pager=1

```

### Utilizzare la shell dei comanti per avviare altri sistemi operativi

```
grub>

```

È possibile utilizzare la shell di GRUB per avviare altri sistemi operativi, come ad esempio sistemi Windows o Linux installati su partizione e avviarli tramite **chainloading**.

Il *chainloading* consiste nell'avviare un bootloader, che può trovarsi all'inizio del disco (per sistemi MBR) o all'inizio di una partizione, tramite un altro bootloader.

#### Effettuare il chainloading di una partizione

```
set root=(hdX,Y)
chainloader +1
boot

```

Dove `X` indica il disco fisso da cui avviare l'altro bootloader ed ha valori che partono da 0, mentre `Y` identifica il numero della partizione che ci interessa.

L'esempio seguente mostra come avviare un'installazione di Windows situata nella prima partizione del primo hard disk:

```
set root=(hd0,1)
chainloader +1
boot

```

È inoltre possibile avviare un'installazione di GRUB in una partizione utilizzando lo stesso metodo di cui sopra.

#### Effettuare il chainloading di un disco/drive

```
set root=hdX
chainloader +1
boot

```

#### Effettuare il chainloading di sistemi Windows/Linux installati in modalità UEFI

```
insmod ntfs
set root=(hd0,gpt4)
chainloader (${root})/EFI/Microsoft/Boot/bootmgfw.efi
boot

```

`insmod ntfs` viene utilizzato per caricare il modulo NTFS necessario al caricamento di Windows.

`(hd0,gpt4)` o `/dev/sda4` identifica la partizione EFI di sistema (ESP).

Il percorso che segue la voce `chainloader` identifica il file .efi del quale si vuole fare il chainloading.

#### Avvio normale

Si vedano gli esempi in [#Usare la console di emergenza](#Usare_la_console_di_emergenza).

## Tools grafici per la configurazione

È possibile installare i seguenti pacchetti:

*   **grub-customizer** — Consente di personalizzare il bootloader (GRUB o BURG)

	[https://launchpad.net/grub-customizer](https://launchpad.net/grub-customizer) || [grub-customizer](https://aur.archlinux.org/packages/grub-customizer/)

*   **grub2-editor** — Control module di KDE4 per configurare GRUB

	[http://kde-apps.org/content/show.php?content=139643](http://kde-apps.org/content/show.php?content=139643) || [grub2-editor](https://aur.archlinux.org/packages/grub2-editor/)

*   **startupmanager** — Applicazione grafica per cambiare le impostazioni di GRUB Legacy, GRUB, Usplash e Splashy ([abbandonato](https://launchpad.net/startup-manager/+announcement/8300))

	[http://sourceforge.net/projects/startup-manager/](http://sourceforge.net/projects/startup-manager/) || [startupmanager](https://aur.archlinux.org/packages/startupmanager/)

## parttool per hide/unhide

Se si hanno sistemi Windows 9x installati con dischi `C:\` nascosti, GRUB dispone delle opzioni `hide/unhide` attraverso `parttool`. Ad esempio, per effettuare ilboot del terzo disco `C:\` di tre sistemi Windows 9x installati, si avvii la shell e:

```
parttool hd0,1 hidden+ boot-
parttool hd0,2 hidden+ boot-
parttool hd0,3 hidden- boot+
set root=hd0,3
chainloader +1
boot
```

## Usare la console di emergenza

Si veda innanzitutto [#Usare la shell](#Usare_la_shell). Se non si è in grado di avviare la shell standard, una possibile soluzione è quella di effettuare il boot tramite LiveCD o con qualche altro disco di ripristino per correggere gli errori di configurazione e reinstallare GRUB. Tuttavia, un disco di ripristino non è sempre disponibile (né tantomeno necessario), e la console di emergenza è sorprendentemente robusta.

I comandi disponibili in questa modalità includono `insmod`, `ls`, `set` e `unset`. Questo esempio usa `set` ed `insmod`. `set` modifica il valore delle variabili, mentre `insmod` aggiunge nuovi moduli per espandere le funzionalità di base.

Prima di iniziare, è necessario che l'utente sappia la posizione della propria partizione di `/boot` (sia essa separata o una sottodirectory della partizione root):

```
grub rescue> set prefix=(hdX,Y)/boot/grub

```

Dove X è il numero relativo al drive ed Y quello della partizione. Per espandere le funzionalità della console, si inserisca il modulo `linux`.

```
grub rescue> insmod i386-pc/linux.mod

```

**Nota:** Se si sta usando una partizione di boot separata, si ometta `/boot` dal percorso. (esempio: `set prefix=(hdX,Y)/grub`).

Ciò rende disponibili i comandi `linux` ed `initrd`, che dovrebbero essere familiari (si veda [#Configurazione avanzata](#Configurazione_avanzata)).

Un esempio, avvio di Arch Linux:

```
set root=(hd0,5)
linux /boot/vmlinuz-linux root=/dev/sda5
initrd /boot/initramfs-linux.img
boot
```

Di nuovo, in caso di partizione di boot separata, si cambino i comandi di conseguenza:

```
set root=(hd0,5)
linux /vmlinuz-linux root=/dev/sda6
initrd /initramfs-linux.img
boot
```

**Nota:** Se si riscontra l'errore `error: premature end of file /NOME_KERNEL` durante l'esecuzione del comando `linux` è possibile provare ad utilizzare il comando `linux16` al suo posto.

Dopo aver avviato con successo l'installazione di Arch Linux, è possibile correggere `grub.cfg` e procedere con la reinstallazione di GRUB.

Per reinstallare GRUB nel MBR, cambiando `/dev/sda` secondo le proprie esigenze. Si veda [#Installazione](#Installazione) per i dettagli.

## Risoluzione dei problemi

### Sistemi con BIOS Intel non effettuano il boot da partizioni GPT

#### MBR

Alcuni BIOS Intel richiedono la presenza al boot di una partizione MBR contrassegnata come "avviabile", cosa che rende di fatto inusabili configurazioni basate su GPT.

È possibile aggirare il problema utilizzando (ad esempio) `fdisk` per segnare una delle partizioni GPT (preferibilmente la partizione da 1007 KiB che si è creata per GRUB) come avviabile. Si utilizzi `fdisk` puntandolo all'HD relativo (ad esempio `/dev/sda`), quindi si prema `a` e si selezioni la partizione da contrassegnare come avviabile (probabilmente la prima) utilizzando il numero corrispondente e infine si prema `w` per scrivere le modifiche nel MBR.

**Nota:** Il procedimento di cui sopra deve essere eseguito in `fdisk` o tools simili e NON via GParted o altri, dal momento che questi non impostano il flag "avviabile" nel MBR.

Ulteriori informazioni sono disponibili a [questo](http://www.rodsbooks.com/gdisk/bios.html) indirizzo.

#### EFI

Alcuni firmware UEFI richiedono la presenza di un'immagine avviabile in un percorso specifico prima di poter mostrare le voci di avvio. Se si rientra in questa categoria `grub-install` segnalerà che `efibootmgr` ha agiunto una voce per l'avvio di GRUB, ma quest'ultima non verrà poi visualizzata all'interno del menu di VisualBIOS per la scelta dell'ordine di boot. La soluzione consiste nel posizionare un'ìmmagine in uno dei percorsi in questione. Assumendo che la propria partizione EFI sia in `/boot/efi`, i seguenti comandi risolveranno il problema:

```
mkdir /boot/efi/EFI/boot
cp /boot/efi/EFI/grub/grubx64.efi /boot/efi/EFI/boot/bootx64.efi

```

La soluzione proposta ha funzionato su una scheda madre Intel DH87MC con firmware datato Gennaio 2014.

### Abilitare i messaggi di debug in GRUB

Si aggiunga:

```
set pager=1
set debug=all

```

Al `grub.cfg`.

### Correggere l'errore di GRUB "no suitable mode found"

Se si ottiene questo errore alla scelta di un'opzione di boot:

```
error: no suitable mode found
Booting however

```

Allora sarà necessario inizializzare il terminale grafico di GRUB (gfxterm), usando una modalità video appropriata (gfxmode). Quest'ultima viene passata da GRUB al kernel linux usando l'opzione `gfxpayload`. Sui sistemi UEFI, se la modalità video di GRUB non viene inizializzata, non verranno visualizzati i messaggi di boot del kernel (almeno fino all'attivazione del KMS).

Si copi `/usr/share/grub/unicode.pf2` in `${GRUB_PREFIX_DIR`} (`/boot/grub` su sistemi BIOS e UEFI. Se GRUB UEFI è stato installato con l'opzione `--boot-directory=$esp/EFI` abilitata, allora il percorso sarà `$esp/EFI/grub`).

```
# cp /usr/share/grub/unicode.pf2 ${GRUB_PREFIX_DIR}

```

Se il file `/usr/share/grub/unicode.pf2` non esiste, si installi il pacchetto [bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont) e si proceda alla creazione e copia dello stesso in `${GRUB_PREFIX_DIR`}.

```
# grub-mkfont -o unicode.pf2 /usr/share/fonts/misc/unifont.bdf

```

Nel file `grub.cfg`, si aggiungano le seguenti linee per consentire a GRUB di passare correttamente la modalità video al kernel, altrimenti si otterrà uno schermo nero, benchè il boot sia effettuato regolarmente senza che il sistema si blocchi:

Sistemi BIOS

```
insmod vbe

```

Sistemi UEFI

```
insmod efi_gop
insmod efi_uga

```

Si aggiunga poi il seguente codice (comune a sistemi BIOS e UEFI)

```
insmod font

```

```
if loadfont ${prefix}/fonts/unicode.pf2
then
    insmod gfxterm
    set gfxmode=auto
    set gfxpayload=keep
    terminal_output gfxterm
fi
```

Come si può notare, affinchè `gfxterm` funzioni correttamente, il font `unicode.pf2` deve esistere in `${GRUB_PREFIX_DIR`}.

### messaggio d'errore msdos-style

```
grub-setup: warn: This msdos-style partition label has no post-MBR gap; embedding won't be possible!
grub-setup: warn: Embedding is not possible. GRUB can only be installed in this setup by using blocklists.
            However, blocklists are UNRELIABLE and its use is discouraged.
grub-setup: error: If you really want blocklists, use --force.

```

Questo problema si verifica quando si tenta di installare GRUB in VMWare. Ulteriori informazioni [qui](https://bbs.archlinux.org/viewtopic.php?pid=581760#p581760). Si spera in un fix in tempi brevi.

Può anche verificarsi quando la partizione inizia subito dopo l'MBR (blocco 63), senza lasciare uno spazio di circa 1MB (2048 blocchi) prima dell'inizio della prima partizione. Si veda [#Istruzioni specifiche per Master Boot Record (MBR)](#Istruzioni_specifiche_per_Master_Boot_Record_.28MBR.29)

### GRUB UEFI torna alla shell

Se GRUB viene caricato, ma torna alla shell di ripristino senza errori, il `grub.cfg` potrebbe trovarsi in una posizione sbagliata o non esistere del tutto. Questo problema potrebbe verificarsi se GRUB UEFI è stato installato con l'opzione `--boot-directory` abilitata, e il file `grub.cfg` non esiste, OPPURE se il numero identificativo della partizione di boot è cambiato (tale valore è infatti "hardcoded" nel file `grubx64.efi`).

### GRUB UEFI non viene caricato

Esempio di un sistema EFI funzionante:

 `# efibootmgr -v` 
```
BootCurrent: 0000
Timeout: 3 seconds
BootOrder: 0000,0001,0002
Boot0000* Grub HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\efi\grub\grub.efi)
Boot0001* Shell HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\EfiShell.efi)
Boot0002* Festplatte BIOS(2,0,00)P0: SAMSUNG HD204UI

```

Se lo schermo diveta nero per qualche secondo e GRUB passa alla prossima opzione di boot, come scritto [in questo post](https://bbs.archlinux.org/viewtopic.php?pid=981560#p981560), spostare GRUB sulla partizione di root potrebbe aiutare.

L'opzione di boot deve essere eliminata e ricreata dopo l'operazione. Il campo relativo a grub dovrebbe ora essere simile a questo:

```
Boot0000* Grub HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\grub.efi)

```

### Invalid signature

Se si riceve l'errore "invalid signature" cercando di avviare Windows, ad esempio dopo aver alterato la tabella partizioni o aver aggiunto altri hard disks, si provi a rimuovere la configurazione dei dispositivi di GRUB e lasciare che lo stesso la rigeneri:

```
# mv /boot/grub/device.map /boot/grub/device.map-old
# grub-mkconfig -o /boot/grub/grub.cfg

```

`grub-mkconfig` dovrebbe ora mostrare tutte le opzioni di boot, incluso Windows. Se il problema è risolto, si rimuova `/boot/grub/device.map-old`.

### Freeze al boot

Se il boot si blocca senza errori dopo che GRUB carica il kernel e l'eventuale ramdisk, si provi a rimuovere il parametro del kernel `add_efi_memmap`.

### Ripristinare GRUB Legacy

*   Spostare i files di GRUB Legacy o GRUB:

```
# mv /boot/grub /boot/grub.nonfunctional

```

*   Ripristinare il backup di GRUB Legacy in `/boot`:

```
# cp -a /path/to/backup/grub /boot/

```

*   Ripristinare il MBR e i 62 settori successivi del disco sda (PERICOLOSO):

```
# dd if=/path/to/backup/first-sectors of=/dev/sdX bs=512 count=1

```

**Attenzione:** Il comando sopra riportato ripristina anche la tabella delle partizioni. Si proceda con cautela.

Una soluzione più sicura è il ripristino del solo MBR:

```
# dd if=/path/to/backup/mbr-boot-code of=/dev/sdX bs=446 count=1

```

### Arch non rilevata da altre distribuzioni

Alcuni utenti hanno riportato che altre distribuzioni hanno problemi a rilevare Arch Linux automaticamente tramite `os-prober`. È possibile mitigare la situazione attraverso la creazione del file `/etc/lsb-release`: il file in questione e relativo tool per l'aggiornamento dello stesso sono disponibili nel pacchetto [lsb-release](https://www.archlinux.org/packages/?name=lsb-release), disponibile nei [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

## Riferimenti

1.  Manuale ufficiale di GRUB - [http://www.gnu.org/software/grub/manual/grub.html](http://www.gnu.org/software/grub/manual/grub.html)
2.  Pagina del wiki di Ubuntu su GRUB - [https://help.ubuntu.com/community/Grub2](https://help.ubuntu.com/community/Grub2)
3.  Pagina del wiki di GRUB che spiega come compilarlo per sistemi UEFI - [http://help.ubuntu.com/community/UEFIBooting](http://help.ubuntu.com/community/UEFIBooting)
4.  La pagina di Wikipedia relativa alla [partizione di Boot del BIOS](https://en.wikipedia.org/wiki/BIOS_Boot_partition "wikipedia:BIOS Boot partition").