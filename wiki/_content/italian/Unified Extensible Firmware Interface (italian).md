L'**Unified Extensible Firmware Interface** (UEFI in breve) è un nuovo firmware inizialmente progettato da Intel (con il nome EFI) per i sistemi basati su processori Itanium. Esso introduce un nuovo metodo di avvio del SO che si distingue dal tradizionale "codice di avvio MBR" utilizzato dal BIOS. La versione di EFI 1.x fu presentata da Intel e successivamente un gruppo di aziende chiamato "the UEFI forum" si assunse il ruolo di svilupparlo e, per questo, a partire dalla versione 2.0 venne chiamato Unified EFI. Dal 23 Maggio 2012, la versione più recente è la 2.3.1

**Nota:** Salvo specificare esplicitamente EFI 1.x i termini EFI e UEFI sono attualmente usati entrambi per indicare il firmware UEFI 2.0\. Le istruzioni contenute in questa guida sono generali e non specifiche per Mac, se non specificato esplicitamente. Molti passaggi potrebbero essere differenti su un Mac, in quanto l'implementazione Apple di EFI è un mix tra EFI 1.x e UEFI 2.0\. SI tratta quindi di un firmware non conferme agli standard UEFI.

## Contents

*   [1 Avviare un SO usando il BIOS](#Avviare_un_SO_usando_il_BIOS)
    *   [1.1 Avvio multiplo con BIOS](#Avvio_multiplo_con_BIOS)
*   [2 Avviare un SO usando UEFI](#Avviare_un_SO_usando_UEFI)
    *   [2.1 Avvio multiplo con UEFI](#Avvio_multiplo_con_UEFI)
        *   [2.1.1 Linux Windows x86_64 UEFI-GPT Multiboot](#Linux_Windows_x86_64_UEFI-GPT_Multiboot)
*   [3 Processo di boot con UEFI](#Processo_di_boot_con_UEFI)
*   [4 Identificare l'architettura del firmware UEFI](#Identificare_l'architettura_del_firmware_UEFI)
*   [5 Supporto del Kernel Linux per UEFI](#Supporto_del_Kernel_Linux_per_UEFI)
    *   [5.1 Configurazioni del Kernel Linux per UEFI](#Configurazioni_del_Kernel_Linux_per_UEFI)
*   [6 Supporto per le variabili UEFI](#Supporto_per_le_variabili_UEFI)
    *   [6.1 Strumenti in ambiente Userspace](#Strumenti_in_ambiente_Userspace)
    *   [6.2 Sistemi UEFI Non-Mac](#Sistemi_UEFI_Non-Mac)
        *   [6.2.1 efibootmgr](#efibootmgr)
*   [7 Bootloader Linux per UEFI](#Bootloader_Linux_per_UEFI)
*   [8 Creare una partizione di sistema UEFI con Linux](#Creare_una_partizione_di_sistema_UEFI_con_Linux)
    *   [8.1 Per dischi partizionati GPT](#Per_dischi_partizionati_GPT)
    *   [8.2 Per dischi partizionati MBR](#Per_dischi_partizionati_MBR)
*   [9 UEFI Shell](#UEFI_Shell)
    *   [9.1 Collegamenti per il download di UEFI Shell](#Collegamenti_per_il_download_di_UEFI_Shell)
    *   [9.2 Avviare UEFI Shell](#Avviare_UEFI_Shell)
    *   [9.3 Comandi importanti della Shell UEFI](#Comandi_importanti_della_Shell_UEFI)
        *   [9.3.1 bcfg](#bcfg)
        *   [9.3.2 edit](#edit)
*   [10 Creare un dispositivo USB avviabile con UEFI dalla ISO](#Creare_un_dispositivo_USB_avviabile_con_UEFI_dalla_ISO)
    *   [10.1 Risoluzione degli errori](#Risoluzione_degli_errori)
*   [11 Rimuovere il supporto per il boot UEFI dalla ISO](#Rimuovere_il_supporto_per_il_boot_UEFI_dalla_ISO)
*   [12 Altre risorse](#Altre_risorse)

## Avviare un SO usando il BIOS

Il BIOS (Basic Input-Output System) è il primo programma che viene eseguito all'accensione del PC. Quando tutto l'hardware è stato avviato e le operazioni POST sono state completate, il BIOS esegue il primo codice di avvio presente sulla prima periferica specificata nella lista di avvio (booting list).

Se il primo elemento della lista è un lettore CD/DVD, viene eseguita l'estensione El-Torito(codice di avvio) presente sul CD. Se il primo elemento è un HDD, il BIOS esegue i primi 440 byte cioè il codice di avvio [MBR](/index.php/Master_Boot_Record_(Italiano) "Master Boot Record (Italiano)"). Il codice di avvio effettua un chainload oppure il bootstrap di un bootloader più complesso che poi avvia il SO.

Il BIOS non sa come leggere la tabella delle partizioni o un filesystem, ma si limita ad inizializzare l'hardware ed eseguire il codice d'avvio.

### Avvio multiplo con BIOS

Dato che si può ottenere poco da un programma deve occupare solo i primi 440 bytes disponibili, per l'avvio multiplo usando il BIOS è necessario un bootloader che gestisca l'avvio multiplo(si intende l'avvio di più di un sistema operativo, non l'avvio di un Kernel nel formato Multiboot). Per questo motivo il BIOS si limita ad avviare un bootloader come [GRUB](/index.php/GRUB2_(Italiano) "GRUB2 (Italiano)"), [Syslinux](/index.php/Syslinux_(Italiano) "Syslinux (Italiano)") oppure [LILO](/index.php/LILO "LILO") il quale in seguito si occupa di caricare il sistema operativo attraverso un chainload(caricamento di un altro bootloader) oppure direttamente caricando il kernel.

## Avviare un SO usando UEFI

Il firmware UEFI non avvia il sistema con il metodo sopra menzionato (l'unico supportato dal BIOS), difatti UEFI ha la capacità di leggere la tavola delle partizioni e quella di riconoscere i singoli filesystem.

I firmware UEFI comunemente utilizzati supportano entrambi i sistemi di partizionamento [MBR](/index.php/Master_Boot_Record_(Italiano) "Master Boot Record (Italiano)") e [GPT](/index.php/GPT "GPT"). L'EFI Apple supporta anche la mappa di partizionamento Apple. La maggior parte dei firmware UEFI supportano i filesystem FAT12 (floppy disks), FAT16 e FAT32 negli HHD inoltre ISO9660(e UDF) nei CD/DVD. Il firmware EFI nei sistemi Apple supporta in aggiunta i filesystem HFS/HFS+.

UEFI non lancia nessun codice dall'MBR sia che il codice esista o meno. Utilizza invece una speciale partizione chiamata "EFI SYSTEM PARTITION" che contiene i file che verranno avviati dal firmware. Ogni produttore può archiviare i propri file nella cartella <EFI SYSTEM PARTITION>/EFI/<PRODUTTORE>/ e usare il firmware (oppure la propria shell UEFI) per lanciare il programma di avvio. La partizione di sistema EFI ha normalmente come filesystem FAT32.

In ambiente UEFI, tutti i programmi che siano loader per un Sistema Operativo o altri strumenti (come programmi per il test della memoria) o strumenti di recovery al di fuori del sistema operativo, dovrebbero essere applicazioni UEFI corrispondenti all'architettura del firmware EFI. Molti dei firmware UEFI sul mercato, inclusi i recenti Mac di Apple utilizzano un firmware UEFI x86_64\. Solo alcuni vecchi Mac utilizzano un firmware EFI i386 mentre i sistemi UEFI non Apple sono risaputi utilizzare firmware EFI i386.

**Nota:** Alcune vecchie schede Server Intel sono note operare con un firmware Intel EFI 1.10, e richiedono applicazioni EFI i386.

Un firmware EFI x86_64 non include il supporto per il lancio di applicazioni EFI a 32-bit, diversamente dai sistemi Linux o Windows 64-bit che includono questo supporto. Comunque il bootloader dovrà essere compilato per la corretta architettura.

### Avvio multiplo con UEFI

Dato che ogni SO o produttore può mantenere i propri file nella partizione del sistema EFI(EFI SYSTEM PARTITION) senza modificarne altri, il multiboot mediante UEFI consiste nel lanciare una differente applicazione UEFI corrispondente al bootloader di un determinato sistema operativo. Questo rende non necessari i meccanismi di chainload dei bootloader per avviare altri sistemi operativi.

#### Linux Windows x86_64 UEFI-GPT Multiboot

Le versioni Windows Vista (SP1+), Windows 7 Professional e Windows 8 x86_64 supportano nativamente il boot da un firmware UEFI. Ma per questo è necessario un partizionamento di tipo [GPT](/index.php/GPT "GPT") sul disco utilizzato per il boot con UEFI. Le versioni 32-bit di Windows supportano solamente il boot di tipo BIOS-MBR. Seguire le istruzioni fornite nel link del forum nella sezione altre risorse, per informazioni su come procedere. Consultare [http://support.microsoft.com/default.aspx?scid=kb;EN-US;2581408](http://support.microsoft.com/default.aspx?scid=kb;EN-US;2581408) per maggiori informazioni.

Questa limitazione non esiste per il Kernel Linux ma piuttosto per il bootloader utilizzato. Per il bene dell'avvio di Windows, il bootloader Linux dovrebbe essere installato in modalità UEFI-GPT se si avviano entrambi dal solito disco.

## Processo di boot con UEFI

1.  Accensione del sistema - Power On Self Test, o processo POST.
2.  Viene caricato il firmware UEFI.
3.  Il firmware legge il suo Boot Manager per determinare quale applicazione UEFI avviare e da dove avviare (ad esempio da quale disco e partizione).
4.  Il firmware avvia l'applicazione UEFI dalla partizione UEFISYS formattata FAT32 come definito nella voce di avvio del boot manager del firmware.
5.  L'applicazione UEFI può avviare un'altra applicazione (nel caso di UEFI Shell o un boot manager come rEFInd) oppure il kernel e l'initramfs (nel caso di un bootloader come GRUB) a seconda di come è stata configurata l'applicazione UEFI.

## Identificare l'architettura del firmware UEFI

Se si possiede un sistema UEFI non mac, allora si ha un firmware UEFI 2.x x86_64 (detto anche 64-bit).

Alcuni dei più noti firmware UEFI 2.x x86_64 sono Phoenix SecureCore Tiano, AMI Aptio, Insyde H2O.

Alcuni dei più noti sistemi che utilizzano questi firmware sono Asus EZ Mode BIOS (schede madri con Sandy Bridge P67 e H67 ), MSI ClickBIOS, HP EliteBooks, Sony Vaio Z series, alcune schede madri Desktop e Server di Intel.

I Mac prodotti prima del 2008 per lo più hanno firmware i386-efi mentre quelli prodotti dopo hanno firmware x86_64-efi. Tutti i Mac capaci di eseguire il kernel di Mac OS X Snow Leopard 64-bit hanno un firmware x86_64 EFI 1.x.

Per individuare l'architettura del firmware efi in un Mac, avviare Mac OS X e digitare il seguente comando:

```
ioreg -l -p IODeviceTree | grep firmware-abi

```

Se la risposta del comando è EFI32 allora il firmware sarà i386 EFI 1.x. Se risponde EFI64 allora il firmware sarà x86_64 EFI 1.x. I Mac non hanno un firmware UEFI 2.x perché l'implementazione di Aplle del firmware EFI non soddisfa pienamente le specifiche UEFI.

## Supporto del Kernel Linux per UEFI

### Configurazioni del Kernel Linux per UEFI

Le configurazioni del Kernel Linux richieste per utilizzare UEFI sono:

```
CONFIG_EFI=y
CONFIG_EFI_STUB=y
CONFIG_RELOCATABLE=y
CONFIG_FB_EFI=y
CONFIG_FRAMEBUFFER_CONSOLE=y

```

Supporto per le variabili/servizi di runtime - il modulo del kernel 'efivars'. Questa opzione è importante perché richiesta per accedere e variare le variabili di Runtime UEFI utilizzando strumenti come **efibootmgr**.

```
CONFIG_EFI_VARS=m

```

**Nota:** In questa opzione è compilato come modulo come nei kernel di Arch reperibili in core/testing.

**Nota:** Per permettere a Linux di accedere ai servizi di runtime UEFI, l'architettura del firmware UEFI e quella del Kernel Linux devono coincidere. Non dipende dal bootloader utilizzato.

**Nota:** Se l'architettura del firmware UEFI e quella del Kernel Linux sono diverse, utilizzare il parametro "**noefi**" nella linea kernel per evitare kernel panic ed avviare correttamente. L'opzione "noefi" comunica al kernel di non accedere ai servizi di runtime UEFI.

Opzione di configurazione per la tavola delle partizioni [GPT](/index.php/GPT "GPT")(GUID Partition Table) - obbligatoria per il supporto ad UEFI:

```
CONFIG_EFI_PARTITION=y

```

**Nota:** Tutte le opzioni sopra sono richieste per avviare Linux tramite UEFI, e sono abilitate nei kernel presenti nei repository ufficiali di ArchLinux.

Informazioni ottenute da [http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=blob_plain;f=Documentation/x86/x86_64/uefi.txt;hb=HEAD](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=blob_plain;f=Documentation/x86/x86_64/uefi.txt;hb=HEAD) .

## Supporto per le variabili UEFI

UEFI definisce delle variabili tramite cui il sistema operativo può interagire con il firmware. Le variabili di boot UEFI sono utilizzate dal boot-loader e dal sistema operativo durante la prima fase di avvio. Le variabili di runtime UEFI permettono al sistema operativo di gestire certe impostazioni del firmware come il Boot Manager UEFI o gestire le chiavi per il Secure Boot Protocol eccetera.

**Nota:** I seguenti passaggio non funzioneranno se il sistema è stato avviato in modalità BIOS, e non funzioneranno nemmeno se l'architettura del firmware UEFI e quella del Kernel Linux non coincidono, ad esempio firmware UEFI x86_64 + kernel x86 32-bit o viceversa. Questo è vero per il modulo del kernel efivar e per efibootmgr. Gli altri passaggi (ad esempio configurare <UEFISYS>/EFI/arch/refind/{refindx64.efi,refind.conf} ) possono essere effettuati anche se si è avviato in modalità BIOS/Legacy.

L'accesso ai servizi di runtime UEFI è fornito dal modulo del kernel "efivars" che è abilitato dalla configurazione del kernel `CONFIG_EFI_VAR=m`. Questo modulo una volta caricato garantirà l'accesso alle variabili popolando la cartella `/sys/firmware/efi/vars`. Un modo per controllare che il sistema sia avviato in modalità UEFI consiste nel caricare in memoria il modulo "efivars" e controllare l'esistenza ed il contenuto della cartella `/sys/firmware/efi/vars` il cui contenuto sarà simile a questo:

```
Output di esempio (x86_64-UEFI 2.3.1 con kernel x86_64):

# ls -1 /sys/firmware/efi/vars/
Boot0000-8be4df61-93ca-11d2-aa0d-00e098032b8c/
BootCurrent-8be4df61-93ca-11d2-aa0d-00e098032b8c/
BootOptionSupport-8be4df61-93ca-11d2-aa0d-00e098032b8c/
BootOrder-8be4df61-93ca-11d2-aa0d-00e098032b8c/
ConIn-8be4df61-93ca-11d2-aa0d-00e098032b8c/
ConInDev-8be4df61-93ca-11d2-aa0d-00e098032b8c/
ConOut-8be4df61-93ca-11d2-aa0d-00e098032b8c/
ConOutDev-8be4df61-93ca-11d2-aa0d-00e098032b8c/
ErrOutDev-8be4df61-93ca-11d2-aa0d-00e098032b8c/
Lang-8be4df61-93ca-11d2-aa0d-00e098032b8c/
LangCodes-8be4df61-93ca-11d2-aa0d-00e098032b8c/
MTC-eb704011-1402-11d3-8e77-00a0c969723b/
MemoryTypeInformation-4c19049f-4137-4dd3-9c10-8b97a83ffdfa/
PlatformLang-8be4df61-93ca-11d2-aa0d-00e098032b8c/
PlatformLangCodes-8be4df61-93ca-11d2-aa0d-00e098032b8c/
RTC-378d7b65-8da9-4773-b6e4-a47826a833e1/
del_var
new_var

```

Le variabili di runtime UEFI non saranno reperibili se è stato utilizzato il parametro "noefi" nella linea del kernel dal menù del bootloader. Questo parametro comunica al kernel di ignorare i servizi di runtime UEFI.

### Strumenti in ambiente Userspace

Esistono alcuni strumenti che possono accedere/modificare le variabili UEFI, e sono:

1.  efibootmgr - Utilizzato per creare/modificare le voci di avvio del Boot Manager UEFI - [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) oppure [efibootmgr-git](https://aur.archlinux.org/packages/efibootmgr-git/)
2.  uefivars - semplicemente accede alle variabili - [uefivars-git](https://aur.archlinux.org/packages/uefivars-git/) - utilizza la libreria efibootmgr
3.  Ubuntu's Firmware Test Suite - fwts - [fwts-git](https://aur.archlinux.org/packages/fwts-git/) - il comando uefidump - `fwts uefidump`

### Sistemi UEFI Non-Mac

#### efibootmgr

**Attenzione:** Utilizzando `efibootmgr` su di un Mac Apple verrà danneggiato (briked) il firmware e potrebbe essere necessario flashare nuovamente la ROM della scheda madre. Esistono segnalazioni di bug riguardante l'argomento sul bug tracker di Ubuntu/Lanunchpad. Utilizzare solamente il comando bless in caso si abbia un Mac. Lo strumento sperimentale "bless" per Linux è sviluppato dagli sviluppatori di Fedora - [mactel-boot](https://aur.archlinux.org/packages/mactel-boot/).

**Nota:** Il comando `efibootmgr` funzionerà soltanto se si è avviato il sistema in modalità UEFI, dato che **richiede l'accesso alle variabili di runtime UEFI** che sono **accessibili solo se si avvia in modalità UEFI** (senza l'uso del parametro del kernel "noefi"). Altrimenti verrà visualizzato l'errore `Fatal: Couldn't open either sysfs or procfs directories for accessing EFI variables`.

**Nota:** Se risulta impossibile utilizzare `efibootmgr`, alcuni firmware UEFI permettono agli utenti di gestire direttamente le opzioni di boot uefi dalla configurazione. Ad esempio alcuni firmware ASUS hanno l'opzione "Add New Boot Option" che permette di selezionare una partizione EFI di sistema locale, e di impostare manualmente l'applicazione EFI. (ad esempio '\EFI\refind\refind_x64.efi')

Inizialmente potrebbe dover avviare il boot-loader dal firmware stesso (utilizzando la UEFI Shell) se il boot-loader è stato installato quando il sistema era avviato in modalità BIOS. Successivamente `efibootmgr` dovrebbe essere eseguito per rendere il boot-loader UEFI la voce di avvio di default nel Boot Manager UEFI.

Per utilizzare efibootmgr, prima sarà necessario caricare il modulo del kernel 'efivars':

```
# modprobe efivars

```

Se con questo comando si ottiene l'errore **no such device found**, allora significa che il sistema non è stato avviato in modalità UEFI o che per qualche motivo il kernel non riesce ad accedere alle variabili di runtime UEFI(noefi?).

Verificare l'esistenza dei file nella cartella */sys/firmware/efi/vars/*. Questa cartella ed il suo contenuto sono creati dal modulo del kernel "efivars" ed esisteranno soltanto se si è avviato in modalità UEFI, senza il parametro del kernel "noefi".

Se la cartella */sys/firmware/efi/vars/* è vuota o non esiste, allora il comando `efibootmgr` non funzionerà. Se non si riesce ad avviare la ISO/CD/DVD/USB in modalità UEFI consultare [Creare un dispositivo USB avviabile con UEFI dalla ISO](#Creare_un_dispositivo_USB_avviabile_con_UEFI_dalla_ISO) .

**Nota:** I seguenti comandi utilizzano il boot-loader [gummiboot](https://www.archlinux.org/packages/?name=gummiboot) come esempio.

Ipotizzando che il file del boot-loader da avviare sia `/boot/efi/EFI/gummiboot/gummibootx64.efi`. Il percorso `/boot/efi/EFI/gummiboot/gummibootx64.efi` può essere diviso in due parti `/boot/efi` and `/EFI/gummiboot/gummibootx64.efi`, dove `/boot/efi` è il punto di mount della partizione di sistema UEFI, che si presume essere `/dev/sdXY` (nell'esempio X e Y sono soltanto simbolici per i reali valori - ad esempio: `/dev/sda1`. X=a Y=1).

Per determinare l'attuale percorso per la partizione di sistema UEFI(dovrebbe essre nella forma `/dev/sdXY`), provare il comando:

```
# findmnt /boot/efi
TARGET SOURCE  FSTYPE OPTIONS
/boot/efi /dev/sdXY vfat        rw,flush,tz=UTC

```

Per creare la voce di avvio utilizzando efibootmgr usare il seguente comando:

```
# efibootmgr -c -g -d /dev/sdX -p Y -w -L "Gummiboot" -l '\EFI\gummiboot\gummibootx64.efi'

```

Nel comando precedente `/boot/efi/EFI/gummiboot/gummibootx64.efi` viene interpretato come `/boot/efi` e `/EFI/gummiboot/gummibootx64.efi` che a sua volta si interpreta come disco `/dev/sdX` -> partizione `Y` -> file `/EFI/gummiboot/gummibootx64.efi`.

UEFI utilizza il backslash (\) come separatore per i percorsi (come nei percorsi Windows).

L'etichetta è il nome della voce del menù visualizzata nel menù di avvio UEFI. Questo nome è scelta dell'utente e non influisce sull'avvio del sistema. Maggiori informazioni posso esse ottenute da [efibootmgr GIT README](http://linux.dell.com/cgi-bin/gitweb/gitweb.cgi?p=efibootmgr.git;a=blob_plain;f=README;hb=HEAD) .

Il filesystem FAT32 non è case-sensitive(non fa distinzione tra maiuscole e minuscole) dato che non utilizza la codifica UTF-8 come default. In questo caso il firmware utilizza lettere maiuscole 'EFI' invece di 'efi', pertanto utilizzare {{ic|\EFI\gummiboot\gummibootx64.efi} o {{ic|\efi\gummiboot\gummibootx64.efi} non fa differenza (cambierebbe invece se la codifica del filesystem fosse UTF-8).

## Bootloader Linux per UEFI

Consultare [Arch boot process#Boot loader](/index.php/Arch_boot_process#Boot_loader "Arch boot process").

## Creare una partizione di sistema UEFI con Linux

**Nota:** La partizione UEFISYS puà essere creata di qualsiasi dimensione supportata dal filesystem FAT32\. In accordo con la documentazione di Microsoft, la dimensione minima per il filesystem FAT32 è di 512 MiB. Pertanto è consigliato che la partizione UEFISYS sia grande almeno 512 MiB. Partizioni più grandi vanno bene, specialmente se si utilizzano svariati bootloader, oppure se diversi sistemi operativi sono avviati tramite UEFI, quindi ci sarà abbastanza spazio per contenere tutti i file correlati. Se si utilizza l'avvio EFISTUB, allora assicurarsi che ci sia abbastanza spazio per il kernel e l'initramfs nella partizione UEFISYS.

### Per dischi partizionati GPT

Due scelte:

*   Usando GNU Parted/GParted: Creare una partizione FAT32\. Contrassegnala come "avviabile".
*   Usando GPT fdisk (chiamato anche gdisk): Creare una partizione con gdisk con codice di tipo partizione "EF00". Successivamente formattare la partizione come FAT32 usando `mkfs.vfat -F32 /dev/<PARTIZIONE>`

**Nota:** Contrassegnando come "avviabile" una partizione in un disco partizionato MBR essa viene marcata come attiva, mentre in una partizione GPT marca la partizione come "UEFI System Partition".

**Attenzione:** Non utilizzare i comandi di util-linux fdisk, cfdisk o sfdisk per cambiare i tipi partizione in un disco GPT. Ugualmente non usare gptfdisk gdisk, cgdisk o sgdisk su un disco MBR, il disco verrebbe automaticamente convertito in un disco GPT (nessuna perdita di dati, ma il sistema non si avvierebbe).

### Per dischi partizionati MBR

Due scelte:

*   Usando GNU Parted/GParted: Creare una partizione FAT32\. Cambiare il tipo partizione della partizione in 0xEF usando fdisk, cfdisk or sfdisk.
*   Usando fdisk: Creare una partizione con il tipo partizione 0xEF e formattarla in FAT32 usando `mkfs.vfat -F32 /dev/<PARTIZIONE>`

**Nota:** E' raccomandato usare sempre partizioni GPT per il boot UEFI poiché alcuni firmware UEFI non accettano il boot UEFI-MBR.

## UEFI Shell

La UEFI Shell è una shell/terminale per il firmware essa avvia le applicazioni uefi che includono i boot-loader uefi. Oltre a questo la shell può anche essere utilizzata per ottenere altre informazioni riguardo al sistema o il firmware come la mappatura della memoria (memmap), modificare le variabili del boot manager (bcfg), eseguire programmi di partizionamento (diskpart), caricare driver uefi, modificare file di testo (edit), hexedit eccetera.

### Collegamenti per il download di UEFI Shell

E' possibile scaricare una UEFI Shell con licenza BSD rilasciata dal progetto di Intel Tianocore UDK/EDK2 Sourceforge.net.

*   [x86_64 UEFI Shell 2.0 (Beta)](https://edk2.svn.sourceforge.net/svnroot/edk2/trunk/edk2/ShellBinPkg/UefiShell/X64/Shell.efi)
*   [x86_64 UEFI Shell 1.0 (Old)](https://edk2.svn.sourceforge.net/svnroot/edk2/trunk/edk2/EdkShellBinPkg/FullShell/X64/Shell_Full.efi)
*   [i386 UEFI Shell 2.0 (Beta)](https://edk2.svn.sourceforge.net/svnroot/edk2/trunk/edk2/ShellBinPkg/UefiShell/Ia32/Shell.efi)
*   [i386 UEFI Shell 1.0 (Old)](https://edk2.svn.sourceforge.net/svnroot/edk2/trunk/edk2/EdkShellBinPkg/FullShell/Ia32/Shell_Full.efi)

La versione 2.0 della Shell funziona solamente con le versioni di firmware UEFI maggiore di 2.3, ed è consigliato al posto della Shell 1.0 in questo tipo di sistemi. La Shell 1.0 dovrebbe funzionare su tutti i sistemi UEFI senza particolare riguardo alla versione del firmware. Maggiori informazioni in [ShellPkg](http://sourceforge.net/apps/mediawiki/tianocore/index.php?title=ShellPkg) ed in [questa mail](http://sourceforge.net/mailarchive/message.php?msg_id=28690732)

### Avviare UEFI Shell

Alcune schede madri Asus ed altre basate su firmware UEFI AMI Aptio x86_64 (a partire dalle schede con Sandy Bridge) forniscono una opzione chiamata `"Launch EFI Shell from filesystem device"`. Per queste schede madri, scaricare la Shell UEFI e copiarla sulla partizione di sistema UEFI come `<UEFI_SYSTEM_PARTITION>/shellx64.efi` (comunemente `/boot/efi/shellx64.efi`).

I sistemi con un firmware UEFI Phoenix SecureCore Tiano sono noti per avere una Shell UEFI integrata che può essere avviata premendo un tasto come F6, F11 oppure F12.

**Nota:** Se non fosse possibile avviare la Shell UEFI direttamente dal firmware utilizzando uno dei precedenti metodi, creare una pennina USB formattata FAT32 contenente Shell.efi nel percorso (USB)/efi/boot/bootx64.efi La penna USB dovrebbe comparire nel menù di avvio del firmware UEFI. Avviando questa opzione verrà avviata la Shell UEFI.

### Comandi importanti della Shell UEFI

I comandi della Shell UEFI solitamente supportano l'opzione `-b` che ferma lo scorrimento dell'output alla fine della pagina. `map` elenca i filesystem riconosciuti (`fs0`, ...) ed i dispositivi di archiviazione (`blk0`, ...). Eseguire `help -b` per elencare i comandi disponibili.

Maggiori informazioni su [questo sito](http://software.intel.com/en-us/articles/efi-shells-and-scripting/).

#### bcfg

Il comando BCFG viene utilizzato per modificare i valori nella NVRAM UEFI, il che permette all'utente di cambiare le voci di avvio o le opzioni dei driver. Questo comando è descritto in modo dettagliato alla pagina 83(Sezione 5.3) del documento pdf "UEFI Shell Specification 2.0".

**Nota:** Si raccomanda gli utenti di utilizzare `bcfg` solamente se `efibootmgr` fallisce nel creare voci di avvio funzionanti sul proprio sistema.

**Nota:** La versione 1.0 della Shell UEFI non supporta il comando `bcfg`.

Per ottenere una lista delle attuali voci di avvio:

```
Shell> bcfg boot dump -v

```

Per aggiungere la voce di avvio per rEFInd (ad esempio) come quarta (la numerazione comincia da 0) opzione nel menù di boot:

```
Shell> bcfg boot add 3 fs0:\EFI\arch\refind\refindx64.efi "Arch Linux (rEFInd)"

```

dove fs0: è la mappatura corrispondente alla partizione di sistema UEFI System Partition e \EFI\arch\refind\refindx64.efi è il file da avviare.

Per rimuovere la quarta opzione di boot:

```
Shell> bcfg boot rm 3

```

Per spostare l'opzione numero 3 al posto dell'opzione numero 0 (cioè la prima opzione o l'opzione di default nel menù di avvio UEFI):

```
Shell> bcfg boot mv 3 0

```

Per il testo di aiuto di bcfg

```
Shell> help bcfg -v -b

```

oppure

```
Shell> bcfg -? -v -b

```

#### edit

Il comando EDIT fornisce un editor di testo semplice con un interfaccia simile all'editor nano, ma leggermente meno funzionale. Esso supporta la codifica UTF-8 e si occupa dei fine riga LF(line feed) contro i CRLF(carriage return + line feed).

Per modificare, ad esempio il file di rEFInd `refind.conf` nella partizione di sistema UEFI (fs0: nel firmware):

```
Shell> fs0:
FS0:\> cd \EFI\arch\refind
FS0:\EFI\arch\refind\> edit refind.conf

```

Digitare `Ctrl-E` per aiuto.

## Creare un dispositivo USB avviabile con UEFI dalla ISO

**Nota:** Il dispositivo USB può utilizzare il partizionamento MBR che GPT (è quindi possibile utilizzare anche un dispositivo USB già partizionato), il filesystem dovebbe essere FAT32(raccomandato), FAT16\. FAT12 è stato ideato per i dischi Floppy e quindi non è consigliato per le periferiche USB.

Per prima cosa creare una tavola delle partizioni MBR ed almeno una prtizione sul dispositivo USB. Effettuare il mount della ISO scaricata dalla [pagina dei download di Arch Linux](https://www.archlinux.org/download/).

```
# mkdir -p /mnt/{usb,iso}
# mount -o loop archlinux-2012.12.01-dual.iso /mnt/iso

```

Quindi creare un filesystem FAT32 nella partizione del dispositivo USB (effettuarne l'umount prima se necessario) avente la stessa etichetta utilizzata nella configurazione della Archiso. Ottenere l'etichetta dal file `/mnt/iso/loader/entries/archiso-x86_64.conf`; questo è utilizzato dall'hook `archiso` nell'initramfs per identificare il percorso udev per il media di installazione. `mkfs.vfat` è parte del pacchetto [dosfstools](https://www.archlinux.org/packages/?name=dosfstools).

```
# awk 'BEGIN {FS="="} /archisolabel/ {print $3}' /mnt/iso/loader/entries/archiso-x86_64.conf | xargs mkfs.vfat -F32 /dev/sdXY -n

```

Effettuare il mount del filesystem FAT32 appena creato, e copiare il contenuto della iso di installazione sull dispositivo USB.

```
# mount /dev/sdXY /mnt/usb
# cp -a /mnt/iso/* /mnt/usb
# sync
# umount /mnt/{usb,iso}

```

### Risoluzione degli errori

Se si incorre nell'errore *"No loader found. Configuration files in /loader/entries/*.conf are needed."* Una possibile soluzione consiste nell'usare un bootloader uefi diverso da quello incluso, gummiboot.

Scaricare [il pacchetto refind-efi](https://www.archlinux.org/packages/extra/any/refind-efi/download/) ed estrarre il the file `/usr/lib/refind/refind_x64.efi` dal pacchetto in `(USB)/EFI/boot/bootx64.efi` (sovrascrivere o rinominare ogni file esistente `(USB)/EFI/boot/bootx64.efi`).

Quindi copiare questo testo in `EFI/boot/refind.conf`. Verificare che l'etichetta nella sezione del menu Arch (`ARCH_201302` in questo esempio) coincida con quella della vostra usb.

 `refind.conf` 
```
timeout 5
textonly

showtools about,reboot,shutdown,exit
# scan_driver_dirs EFI/tools/drivers_x64
scanfor manual,internal,external,optical

scan_delay 1
dont_scan_dirs EFI/boot

max_tags 0
default_selection "Arch Linux Archiso x86_64 UEFI USB"

menuentry "Arch Linux Archiso x86_64 UEFI USB" {
  loader /arch/boot/x86_64/vmlinuz
  initrd /arch/boot/x86_64/archiso.img
  ostype Linux
  graphics off
  options "archisobasedir=arch archisolabel=ARCH_201302 add_efi_memmap"
}

menuentry "UEFI x86_64 Shell v2" {
  loader /EFI/shellx64_v2.efi
  graphics off
}

menuentry "UEFI x86_64 Shell v1" {
  loader /EFI/shellx64_v1.efi
  graphics off
}

```

Dovrebbe essere adesso possibile avviare correttamente, ed avere la possibilità di scegliere quale programma EFI avviare.

## Rimuovere il supporto per il boot UEFI dalla ISO

**Attenzione:** Nella condizione in cui i supporti UEFI+isohybrid El Torito/MBR causino realmente problemi, sarà ideale effettuare il boot UEFI utilizzando una pennina USB come spiegato nella sezione precedente.

Molti sistemi Mac con EFI 32-bi ed alcuni Mac con EFI 64-bit rifiutano di avviarsi da un CD/DVD avviabile UEFI(x64)+BIOS. In questo caso la iso dovrebbe essere ricostruita senza il supporto per il boot UEFI, mantenendo solamente il boot da BIOS.

Effettuare il mount del supporto di installazione ed ottenere il valore di `archisolabel` come illustrato nella sezione precedente.

Ricostruire la ISO utilizzando `xorriso` contenuto nel pacchetto [libisoburn](https://www.archlinux.org/packages/?name=libisoburn):

```
$ xorriso -as mkisofs -iso-level 3 \
    -full-iso9660-filenames\
    -volid "ARCH_201212" \
    -appid "Arch Linux CD" \
    -publisher "Arch Linux <https://www.archlinux.org>" \
    -preparer "prepared like a BAWSE" \
    -eltorito-boot isolinux/isolinux.bin \
    -eltorito-catalog isolinux/boot.cat \
    -no-emul-boot -boot-load-size 4 -boot-info-table \
    -isohybrid-mbr "/mnt/iso/isolinux/isohdpfx.bin" \
    -output "~/archiso.iso" "/mnt/iso/"
```

Masterizzare `~/archiso.iso` su un dispositivo ottico e procedere normalmente con l'installazione.

## Altre risorse

*   Pagina di Wikipedia(inglese) su [UEFI](https://en.wikipedia.org/wiki/UEFI "wikipedia:UEFI")
*   Pagina di Wikipedia(inglese) su [UEFI SYSTEM Partition](https://en.wikipedia.org/wiki/EFI_System_partition "wikipedia:EFI System partition")
*   [Linux Kernel UEFI Documentation](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=blob_plain;f=Documentation/x86/x86_64/uefi.txt;hb=HEAD)
*   [UEFI Forum](http://www.uefi.org/home/) - contiene le [Specifiche UEFI](http://www.uefi.org/specs/) ufficiali - GUID Partition Table è una delle Specifiche UEFI
*   [Tianocore Project di Intel](http://sourceforge.net/apps/mediawiki/tianocore/index.php?title=Welcome_to_TianoCore) per i firmware UEFI Open-Source che includono DuetPkg per gli avvii basati sul BIOS e OvmfPkg utilizzato in in QEMU ed Oracle VirtualBox
*   [Pagina di Intel su EFI](http://www.intel.com/technology/efi/)
*   [FGA: Il processo di avvio EFI](http://homepage.ntlworld.com/jonathan.deboynepollard/FGA/efi-boot-process.html)
*   [Microsoft's Windows and GPT FAQ](http://www.microsoft.com/whdc/device/storage/GPT_FAQ.mspx) - Contiene anche informazioni sull'avvio di Windows in modalità UEFI.
*   [Convertire l'avvio di Windows Vista SP1+ o 7 x86_64 dalla modalità BIOS-MBR alla modalità UEFI-GPT senza reinstallare](https://gitorious.org/tianocore_uefi_duet_builds/pages/Windows_x64_BIOS_to_UEFI)
*   [Creare un drive USB avviabile per Linux BIOS+UEFI e per Windows x64 BIOS+UEFI](https://gitorious.org/tianocore_uefi_duet_builds/pages/Linux_Windows_BIOS_UEFI_boot_USB)
*   [Rod Smith - Una trasformazione da BIOS a UEFI](http://rodsbooks.com/bios2uefi/)
*   [Problemi di avvio UEFI su alcune nuove macchine (LKML)](https://lkml.org/lkml/2011/6/8/322)
*   [EFI Shells e Scripting - Documentazione Intel](http://software.intel.com/en-us/articles/efi-shells-and-scripting/)
*   [UEFI Shell - Documentazione Intel](http://software.intel.com/en-us/articles/uefi-shell/)
*   [UEFI Shell - informazioni sul comando bcfg](http://www.hpuxtips.es/?q=node/293)
*   [Alcune applicazioni utili per UEFI Shell 32-bit](http://hackthejoggler.freeforums.org/download/file.php?id=28)
*   [LPC 2012 Plumbing UEFI into Linux](http://linuxplumbers.ubicast.tv/videos/plumbing-uefi-into-linux/)
*   [LPC 2012 UEFI Tutorial : parte 1](http://linuxplumbers.ubicast.tv/videos/uefi-tutorial-part-1/)
*   [LPC 2012 UEFI Tutorial : parte 2](http://linuxplumbers.ubicast.tv/videos/uefi-tutorial-part-2/)