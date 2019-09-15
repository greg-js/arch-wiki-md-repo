Articoli correlati

*   [Arch Boot Process (Italiano)](/index.php/Arch_Boot_Process_(Italiano) "Arch Boot Process (Italiano)")
*   [Boot loader)](/index.php?title=Boot_loader)&action=edit&redlink=1 "Boot loader) (page does not exist)")

[Syslinux](https://en.wikipedia.org/wiki/SYSLINUX [Wikipedia:FAT](https://en.wikipedia.org/wiki/FAT e [Btrfs](/index.php/Btrfs "Btrfs").

**Nota:** Syslinux non può accedere a files che non si trovino nella partizione sulla quale è installato. Se si necessita della funzionalità multi-fs, si utilizzi un bootloader alternativo come [GRUB](/index.php/GRUB_(Italiano) "GRUB (Italiano)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Sistemi BIOS](#Sistemi_BIOS)
    *   [1.1 Visione d'insieme del processo di boot](#Visione_d'insieme_del_processo_di_boot)
    *   [1.2 Limitazioni di Syslinux su sistemi BIOS](#Limitazioni_di_Syslinux_su_sistemi_BIOS)
    *   [1.3 Installazione](#Installazione)
        *   [1.3.1 Installazione automatica](#Installazione_automatica)
        *   [1.3.2 Installazione manuale](#Installazione_manuale)
            *   [1.3.2.1 Tabella partizioni in formato MBR](#Tabella_partizioni_in_formato_MBR)
            *   [1.3.2.2 Tabella partizioni GUID](#Tabella_partizioni_GUID)
*   [2 Sistemi UEFI](#Sistemi_UEFI)
    *   [2.1 Limitazioni di Syslinux in modalità UEFI](#Limitazioni_di_Syslinux_in_modalità_UEFI)
    *   [2.2 Installazione](#Installazione_2)
*   [3 Configurazione](#Configurazione)
    *   [3.1 Esempi](#Esempi)
        *   [3.1.1 Prompt di boot](#Prompt_di_boot)
        *   [3.1.2 Menù testuale](#Menù_testuale)
        *   [3.1.3 Menù grafico](#Menù_grafico)
    *   [3.2 Parametri del kernel](#Parametri_del_kernel)
    *   [3.3 Boot automatico](#Boot_automatico)
    *   [3.4 Sicurezza](#Sicurezza)
    *   [3.5 Chainloading](#Chainloading)
    *   [3.6 Chainloading di un altro sistema Linux](#Chainloading_di_un_altro_sistema_Linux)
    *   [3.7 Usare memtest](#Usare_memtest)
    *   [3.8 HDT](#HDT)
    *   [3.9 Riavvio e spegnimento](#Riavvio_e_spegnimento)
    *   [3.10 Menù pulito](#Menù_pulito)
    *   [3.11 Mappatura tastiera](#Mappatura_tastiera)
    *   [3.12 Nascondere il menu](#Nascondere_il_menu)
    *   [3.13 Pxelinux](#Pxelinux)
    *   [3.14 Avviare un'immagine ISO 9660 tramite memdisk](#Avviare_un'immagine_ISO_9660_tramite_memdisk)
    *   [3.15 Utilizzare la console seriale](#Utilizzare_la_console_seriale)
*   [4 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [4.1 Utilizzare il prompt di Syslinux](#Utilizzare_il_prompt_di_Syslinux)
    *   [4.2 Il fsck fallisce sulla partizione root](#Il_fsck_fallisce_sulla_partizione_root)
    *   [4.3 DEFAULT o UI non trovati](#DEFAULT_o_UI_non_trovati)
    *   [4.4 Missing Operating System](#Missing_Operating_System)
    *   [4.5 Viene eseguito Windows al posto di Syslinux!](#Viene_eseguito_Windows_al_posto_di_Syslinux!)
    *   [4.6 Le voci del menù non hanno effetto](#Le_voci_del_menù_non_hanno_effetto)
    *   [4.7 Impossibile rimuovere ldlinux.sys](#Impossibile_rimuovere_ldlinux.sys)
    *   [4.8 Viene visualizzato un quadretto bianco nell'angolo in alto a sinistra dello schermo quando si sta usando vesamenu](#Viene_visualizzato_un_quadretto_bianco_nell'angolo_in_alto_a_sinistra_dello_schermo_quando_si_sta_usando_vesamenu)
    *   [4.9 Il chainloading del bootloader di Windows non funziona quando Windows si trova su un drive diverso](#Il_chainloading_del_bootloader_di_Windows_non_funziona_quando_Windows_si_trova_su_un_drive_diverso)
    *   [4.10 Leggere i log del bootloader](#Leggere_i_log_del_bootloader)
    *   [4.11 Compressione BTRFS](#Compressione_BTRFS)
*   [5 Vedere anche](#Vedere_anche)

## Sistemi BIOS

### Visione d'insieme del processo di boot

1.  **Fase 1 : Parte 1 - Caricamento del MBR** - Durante l'avvio, il BIOS legge il boot code contenuto nel [Wikipedia:MBR](https://en.wikipedia.org/wiki/MBR "wikipedia:MBR"), la regione di 440 byte situata all'inizio del disco (contenente il file `/usr/lib/syslinux/bios/mbr.bin` o `/usr/lib/syslinux/bios/gptmbr.bin`).
2.  **Fase 1: Parte 2 - Ricerca della partizione attiva** - Il **boot code Stage 1** cerca la partizione segnata come attiva (flag `boot` nei dischi MBR). Nell'esempio si assume che tale partizione corrisponda a quella di `/boot`.
3.  **Fase 2 : Parte 1 - Esecuzione del Volume Boot Record** - Il **boot code Stage 1** esegue il Volume Boot Record (VBR) della partizione `/boot`. Nel caso di Syslinux, il VBR è il settore iniziale del file `/boot/syslinux/ldlinux.sys`, creato dal comando `extlinux --install`. Si noti che `ldlinux.sys` e `ldlinux.c32` sono due cose diverse.
4.  **Fase 2 : Parte 2 - Esecuzione del file `/boot/syslinux/ldlinux.sys`** - Il VBR carica il resto del file `/boot/syslinux/ldlinux.sys`, la cui posizione su disco non deve cambiare, pena l'impossibilità di effettuare il boot con Syslinux.
    **Nota:** Se si utilizza il file system [Btrfs](/index.php/Btrfs "Btrfs") i metodi scritti sopra non funzioneranno in quanto i files vengono continuamente spostati, variando di conseguenza la posizione del file `ldlinux.sys`. Per questo motivo, in presenza di un file system BTRFS, l'intero boot code di `ldlinux.sys` viene copiato nello spazio che segue il VBR e non viene installato nel percorso canonico come avviene con altri file systems.

5.  **Fase 3 - Caricamento del file `/boot/syslinux/ldlinux.c32`** - Il file `/boot/syslinux/ldlinux.sys` caricherà `/boot/syslinux/ldlinux.c32` (modulo principale) che contiene la parte di Syslinux che non è stato possibile inserire nel `ldlinux.sys` (a causa di limitazioni sulla grandezza dei files). Il file `ldlinux.c32` dovrebbe essere presente in ogni installazione di Syslinux/Extlinux e la sua versione dovrebbe corrispondere a quella del file `ldlinux.sys` installato, pena l'impossibilità di effettuare il boot. Si veda [http://bugzilla.syslinux.org/show_bug.cgi?id=7](http://bugzilla.syslinux.org/show_bug.cgi?id=7) per ulteriori informazioni.
6.  **Fase 4 - Ricerca e caricamento del file di configurazione** - Una volta effettuato il caricamento di Syslinux, verrà cercato il file `/boot/syslinux/syslinux.cfg` (o, in certi casi, `/boot/syslinux/extlinux.conf`) e caricato, se presente. In caso di assenza del suddetto file, si verrà lasciati al prompt `boot:` di Syslinux. Quanto descritto in questa fase e il resto delle componenti secondarie di Syslinux (i moduli `/boot/syslinux/*.c32`, esclusi `lib*.c32` e `ldlinux.c32`) richiedono che i moduli libreria `/boot/syslinux/lib*.c32` siano presenti ([https://wiki.syslinux.org/wiki/index.php/Common_Problems#ELF](https://wiki.syslinux.org/wiki/index.php/Common_Problems#ELF)). Come sopra, la versione dei moduli libreria `lib*.c32` e dei moduli secondari `*.c32` deve combaciare con quella di `ldlinux.sys`.

### Limitazioni di Syslinux su sistemi BIOS

Su questi sistemi, syslinux utilizza delle funzionalità fornite dal BIOS della propria scheda madre per accedere al contenuto dei dischi rigidi. Sfortunatamente, tali funzionalità hanno [limitazioni](http://www.win.tue.nl/~aeb/linux/Large-Disk-4.html) che variano in funzione all'età del BIOS. La maggior parte dei BIOS moderni posono accedere solo ai primi 1024 cilindri, il che corrisponde ad una capacità approssimativa di 8,5 GB. Se la propria partizione `/boot` si trova in un settore sopra tale limite, syslinux potrebbe non essere in grado di caricare i file `syslinux.cfg`, l'`initramfs` o il file `vmlinuz`. Sarà quindi necessario posizionare la partizione `/boot` all'inizio del disco.

Altri bootloaders come [grub](https://www.archlinux.org/packages/?name=grub) utilizzano un "trucco" chiamato *stage 1.5 bootloading*, dove GRUB crea un piccolo programma di circa 32 KB che contiene i driver del disco e lo inserisce all'inizio della tabella partizioni, nello spazio inutilizzato (che su sistemi MBR è chiamato *MBR gap*) oppure, su sistemi GPT, nella partizione di boot BIOS. Il procedimento avviene in questo modo: il boot code nel MBR carica lo *stage 1.5*, inizializza i dischi e vi accede tramite interfaccia SATA, evitando così le limitazioni del BIOS per il caricamento del kernel. Ciò consente di posizionare la partizione `/boot` dovunque sul disco rigido. Sfortunatamente [syslinux](https://www.archlinux.org/packages/?name=syslinux) non dispone di tale funzionalità e si avvale delle funzionalità fornite dal BIOS per il caricamento di `/boot`.

### Installazione

*   Installare i pacchetti [syslinux](https://www.archlinux.org/packages/?name=syslinux) e [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) dai [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

**Nota:**

*   A partire dalla versione 4, EXTLINUX e SYSLINUX sono la stessa cosa.
*   È necessario utilizzare [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) per avvalersi del supporto a [GPT](https://en.wikipedia.org/wiki/GUID_Partition_Table "wikipedia:GUID Partition Table").
*   Se la propria partizione di boot è formattata in FAT, sarà necessario installare il pacchetto [mtools](https://www.archlinux.org/packages/?name=mtools).

#### Installazione automatica

**Nota:** Lo script `syslinux-install_update` è specifico di Arch Linux e non è supportato upstream. Si prega di riportare eventuali bug sul Bug Tracker di Arch Linux e non upstream.

*   Dopo aver eseguito lo script `syslinux-install_update`, ricordarsi di modificare il file `/boot/syslinux/syslinux.cfg`, seguendo [#Configurazione](#Configurazione) e [#Parametri del kernel](#Parametri_del_kernel).

**Attenzione:** Lo script `syslinux-install_update` utilizza come partizione root di default un valore che potrebbe non corrispondere a quello del vostro sistema. Pertanto è importante indicare a Syslinux la partizione root corretta modificando `/boot/syslinux/syslinux.cfg`. In caso contrario, il sistema operativo non si avvierà. Si veda [#Parametri del kernel](#Parametri_del_kernel).

Lo script `syslinux-install_update` si occuperà dell'installazione di Syslinux, della copia dei moduli `*.c32` in `/boot/syslinux`, dell'impostazione della flag di boot e dell'installazione de boot code nel MBR. Può gestire schemi di partizionamento [MBR](/index.php/Master_Boot_Record_(Italiano) "Master Boot Record (Italiano)") e [GPT](/index.php/GUID_Partition_Table "GUID Partition Table") e RAID software.

Se si utilizza una partizione di boot separata, assicurarsi che sia montata. Si controlli con `lsblk`; se non si vede nessun mount point che punta a `/boot`, si monti la partizione prima di procedere.

Si esegua lo script `syslinux-install_update` con gli argomenti `-i` (installa i files) `-a` (imposta la partizione come "attiva") `-m` (installa il boot code nel MBR):

 `# syslinux-install_update -i -a -m` 

Se il comando di cui sopra restituisce l'errore `Syslinux BIOS install failed` è probabile che l'eseguibile `extlinux` non sia riuscito ad individuare la partizione contenente `/boot`:

```
 # extlinux --install /boot/syslinux
 extlinux: cannot find device for path /boot/syslinux
 extlinux: cannot open device (null) 
```

Questo problema può verificarsi quando si effettua l'upgrade da [LILO](/index.php/LILO "LILO") e si utilizza un kernel personalizzato. Può infatti accadere che LILO modifichi il parametro `root=` del kernel da (ad esempio) `root=/dev/sda1` al suo equivalente numerico, come `root=801`, come riportato dall'output di `/proc/cmdline` e `mount`. È possibile risolvere il problema effettuando l'installazione manuale descritta sotto, avendo cura di specificare il parametro `--device=/dev/sda1` a `extlinux`, oppure utilizzando un kernel stock di Arch, dal momento che l'utilizzo di un initramfs da parte di quest'ultimo evita il verificarsi dell'errore.

**Nota:**

*   Se si riavvia il proprio sistema ora, si otterrà solamente il prompt di Syslinux. Per ottenere un menù grafico sarà necessario creare un file di configurazione adatto.

*   Se ci si trova su una directory root differente (ad esempio si sta utilizzando un disco di installazione), si installi syslinux puntando all'ambiente di chroot:

```
# syslinux-install_update.sh -i -a -m -c /mnt

```

A questo punto modificare il file `/boot/syslinux/syslinux.cfg` come indicato in [#Configurazione](#Configurazione) e [#Parametri del kernel](#Parametri_del_kernel).

#### Installazione manuale

**Nota:**

*   Se non si è sicuri dello schema di partizionamento utilizzato (MBR o GPT), è possibile verificare con questo comando:

```
# blkid -s PTTYPE -o value /dev/sda

```

*   Se si sta cercando di ripristinare il sistema tramite LiveCD, ci si assicuri di effettuare il [chroot](/index.php/Chroot "Chroot") prima di eseguire i comandi che seguono.

Se non si effettua il chroot, sarà necessario aggiungere il punto di mount a tutti i percorsi specificati sotto (tranne quelli che iniziano con `/dev`.

La partizione di boot dove si intende installare Syslinux deve avere filesystem fat, ext2, ext3, ext4 o btrfs. L'installazione deve avvenire in una directory montata, e non su `/dev/sdXY`. Non è necessario installarlo nella root directory di un file system: se ad esempio si ha la partizione `/dev/sda1` montata su `/boot`, è possibile installare Syslinux nella directory `syslinux`:

```
# mkdir /boot/syslinux
# cp -r /usr/lib/syslinux/bios/*.c32 /boot/syslinux/ ## si copino TUTTI i files *.c32 da /usr/lib/syslinux/bios/, NON CREARE LINK SIMBOLICI 
# extlinux --install /boot/syslinux

```

Dopo l'esecuzione dei comandi di cui sopra, sarà necessario installare nella regione del disco di 440 byte chiamata Master Boot Record (da non confondersi con lo schema di partizionamento MBR) il boot code di Syslinux `mbr.bin` o `gptmbr.bin`, come descritto nella sezione successiva.

##### Tabella partizioni in formato MBR

Si faccia riferimento a: [Master Boot Record](/index.php/Master_Boot_Record_(Italiano) "Master Boot Record (Italiano)").

Sarà quindi necessario contrassegnare la propria partizione di boot come attiva: `fdisk`, `cfdisk`, `sfdisk` e `gparted` sono applicazioni in grado di compiere questa operazione (flag `boot`).

Una volta effettuata l'operazione, la tabella partizioni dovrebbe essere simile alla seguente:

 `# fdisk -l /dev/sda` 
```
[...]
  Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *        2048      104447       51200   83  Linux
/dev/sda2          104448   625142447   312519000   83  Linux

```

Si installi Syslinux nel MBR:

```
# dd bs=440 count=1 if=/usr/lib/syslinux/bios/mbr.bin of=/dev/sda

```

Syslinux offre inoltre un MBR alternativo: `altmbr.bin`. Quest'ultimo non effettua la ricerca di una partizione avviabile, ma fa riferimento all'ultimo byte del MBR per ricavare la partizione dalla quale effettuare il boot. Ecco un esempio di utilizzo:

```
# printf '\x5' | cat /usr/lib/syslinux/bios/altmbr.bin - | dd bs=440 count=1 iflag=fullblock of=/dev/sda

```

In questo caso, un singolo byte avente valore `5` (esadecimale) viene inserito alla fine del file `altmbr.bin` e i 440 byte risultanti vengono scritti nel MBR del disco `/dev/sda`.

Syslinux è stato quindi installato nella prima partizione logica (`/dev/sda5`) del disco.

##### Tabella partizioni GUID

Si faccia riferimento a: [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table").

È necessario impostare il bit 2 (`legacy_boot`) degli attributi relativi alla partizione `/boot`:

```
# sgdisk /dev/sda --attributes=1:set:2

```

Così facendo, si rende il dispositivo avviabile.

Verificare che l'operazione sia stata eseguita correttamente:

```
# sgdisk /dev/sda --attributes=1:show
1:2:1 (legacy BIOS bootable)

```

Installazione nel MBR:

```
# dd bs=440 conv=notrunc count=1 if=/usr/lib/syslinux/bios/gptmbr.bin of=/dev/sda

```

Se il comando di cui sopra non funziona è possibile provare ad utilizzare:

```
# syslinux-install_update -i -m

```

## Sistemi UEFI

**Nota:**

*   `$esp` identifica il punto di mount della partizione EFI di sistema
*   `efi64` identifica i sistemi UEFI con architettura x86_64; in caso si utilizzino sistemi IA32 (a 32 bit), sostituire ogni occorrenza di `efi64` con `efi32`.
*   Syslinux richiede che il kernel e l'initrd risiedano sulla partizione EFI di sistema, in quanto a causa di un bug non può accedere a files che non si trovino sulla partizione nella quale è installato. È pertanto consigliabile montare la partizione EFI di sistema in `/boot`.
*   Lo script di installazione automatico `/usr/bin/syslinux-install_update` non supporta UEFI.
*   La sintassi del file di configurazione `syslinux.cfg` è la stessa dei sistemi BIOS.

### Limitazioni di Syslinux in modalità UEFI

*   L'applicazione UEFI di Syslinux (`syslinux.efi`) non può essere firmata da `sbsign` (pacchetto *sbsigntool*) per l'uso con il Secure Boot. Bug report - [http://bugzilla.syslinux.org/show_bug.cgi?id=8](http://bugzilla.syslinux.org/show_bug.cgi?id=8)
*   L'utilizzo del tasto `TAB` per la modifica dei parametri del kernel in modalità UEFI crea artefatti a schermo e testo sovrapposto. Bug report - [http://bugzilla.syslinux.org/show_bug.cgi?id=9](http://bugzilla.syslinux.org/show_bug.cgi?id=9)
*   Syslinux UEFI non supporta il chainloading di altre applicazioni UEFI come {{ic|UEFI Shell} o `Windows Boot Manager`. Bug report - [http://bugzilla.syslinux.org/show_bug.cgi?id=17](http://bugzilla.syslinux.org/show_bug.cgi?id=17)
*   Syslinux UEFI potrebbe non effettuare il boot in alcune macchine virtuali, come QEMU/OVMF o Virtualbox, oppure in alcune versioni dei prodotti VMware, oltre ad alcuni ambienti UEFI emulati come DUET. Un contributore di Syslinux ha confermato che non ci sono problemi su VMware Workstation 10.0.2 e Syslinux-6.02\. Bug reports - [http://bugzilla.syslinux.org/show_bug.cgi?id=21](http://bugzilla.syslinux.org/show_bug.cgi?id=21) e [http://bugzilla.syslinux.org/show_bug.cgi?id=23](http://bugzilla.syslinux.org/show_bug.cgi?id=23)
*   Memdisk non è disponibile in modalità UEFI. Bug report - [http://bugzilla.syslinux.org/show_bug.cgi?id=30](http://bugzilla.syslinux.org/show_bug.cgi?id=30)

### Installazione

*   Installare [syslinux](https://www.archlinux.org/packages/?name=syslinux) ed [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) dai [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)"), quindi si installi Syslinux nella partizione EFI di sistema come mostrato sotto.

*   Copiare i file di Syslinux nella partizione EFI di sistema (sostituire a `$esp` il punto di mount della partizione, solitamente `/boot`):

```
# mkdir -p $esp/EFI/syslinux
# cp -r /usr/lib/syslinux/efi64/* $esp/EFI/syslinux

```

*   Si crei una voce di avvio per Syslinux utilizzando [Unified Extensible Firmware Interface#efibootmgr](/index.php/Unified_Extensible_Firmware_Interface#efibootmgr "Unified Extensible Firmware Interface"):

```
# efibootmgr -c -d /dev/sdX -p Y -l /EFI/syslinux/syslinux.efi -L "Syslinux"

```

dove `/dev/sdXY` è la partizione che contiene il bootloader.

*   Si crei o modifichi il file `$esp/EFI/syslinux/syslinux.cfg` seguendo le istruzioni in [#Configurazione](#Configurazione).

**Nota:** il file di configurazione su sistemi UEFI è `$esp/EFI/syslinux/syslinux.cfg` e non `/boot/syslinux/syslinux.cfg`. I file contenuti nella directory `/boot` sono specifici dei sistemi BIOS.

## Configurazione

Il file di configurazione di Syslinux, `syslinux.cfg`, dovrebbe essere creato nella stesa directory dove risiede Syslinux che corrisponde a `/boot/syslinux` per sistemi BIOS e `$esp/EFI/syslinux/` per sistemi UEFI. Il bootloader controllerà l'esistenza del file `syslinux.cfg` (preferito) o `extlinux.conf`.

**Suggerimento:**

*   È possibile usare la keyword `LINUX` al posto di `KERNEL`. La differenza è che `KERNEL` cerca di identificare il tipo di file, mentre `LINUX` si aspetta un kernel Linux come parametro.
*   Il valore `TIMEOUT` è in unità da un decimo di secondo.

### Esempi

**Nota:** I file di configurazione di cui sotto dovranno essere modificati passando al kernel i parametri corretti. Si veda la sezione [#Parametri del kernel](#Parametri_del_kernel).

#### Prompt di boot

Di seguito viene presentato un semplice file di configurazione che visualizza il prompt `boot:` ed esegue il boot automaticamente dopo 5 secondi. Se si vuole effettuare il boot direttamente senza visualizzare un prompt, si imposti `PROMPT` a `0`.

Configurazione:

 `/boot/syslinux/syslinux.cfg` 
```

PROMPT 1
TIMEOUT 50
DEFAULT arch

LABEL arch
        LINUX ../vmlinuz-linux
        APPEND root=/dev/sda2 ro
        INITRD ../initramfs-linux.img

LABEL archfallback
        LINUX ../vmlinuz-linux
        APPEND root=/dev/sda2 ro
        INITRD ../initramfs-linux-fallback.img

```

#### Menù testuale

Syslinux consente di utilizzare un menù testuale. Per utilizzarlo si copi il modulo `menu` nella propria directory di Syslinux:

```
# cp /usr/lib/syslinux/bios/menu.c32 /boot/syslinux/

```

Configurazione:

 `/boot/syslinux/syslinux.cfg` 
```

UI menu.c32
PROMPT 0

MENU TITLE Boot Menu
TIMEOUT 50
DEFAULT arch

LABEL arch
        MENU LABEL Arch Linux
        LINUX ../vmlinuz-linux
        APPEND root=/dev/sda2 ro
        INITRD ../initramfs-linux.img

LABEL archfallback
        MENU LABEL Arch Linux Fallback
        LINUX ../vmlinuz-linux
        APPEND root=/dev/sda2 ro
        INITRD ../initramfs-linux-fallback.img

```

Per ulteriori dettagli sul menù, si veda [la documentazione di Syslinux](http://git.kernel.org/?p=boot/syslinux/syslinux.git;a=blob;f=doc/menu.txt) o il [wiki](https://wiki.syslinux.org/wiki/index.php/Menu) di Syslinux.

#### Menù grafico

È disponibile un menù grafico. Per utilizzarlo, si copi il modulo COM32 `vesamenu` nella propria directory di Syslinux:

```
# cp /usr/lib/syslinux/bios/vesamenu.c32 /boot/syslinux/

```

**Nota:** Se si utilizza [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Italiano) "Unified Extensible Firmware Interface (Italiano)"), assicurarsi di copiare il file `efi32` dalla directory `/usr/lib/syslinux/efi64/`, altrimenti si otterrà solamente una schermata nera. Nel caso si verificasse il problema, avviare il pc tramite LiveCD ed utilizzare [chroot](/index.php/Chroot "Chroot") per effettuare le dovute modifiche.

Questo file di configurazione utilizza lo stesso design del CD di installazione di Arch Linux, e può essere scaricato da [projects.archlinux.org](https://projects.archlinux.org/archiso.git/tree/configs/releng/syslinux). L'immagine di sfondo può essere [scaricata dallo stesso sito](https://projects.archlinux.org/archiso.git/plain/configs/releng/syslinux/splash.png). La si copi quindi in `/boot/syslinux/splash.png`

Configurazione:

 `/boot/syslinux/syslinux.cfg` 
```

UI vesamenu.c32
DEFAULT arch
PROMPT 0
MENU TITLE Boot Menu
MENU BACKGROUND splash.png
TIMEOUT 50

MENU WIDTH 78
MENU MARGIN 4
MENU ROWS 5
MENU VSHIFT 10
MENU TIMEOUTROW 13
MENU TABMSGROW 11
MENU CMDLINEROW 11
MENU HELPMSGROW 16
MENU HELPMSGENDROW 29

# Refer to https://wiki.syslinux.org/wiki/index.php/Comboot/menu.c32

MENU COLOR border       30;44   #40ffffff #a0000000 std
MENU COLOR title        1;36;44 #9033ccff #a0000000 std
MENU COLOR sel          7;37;40 #e0ffffff #20ffffff all
MENU COLOR unsel        37;44   #50ffffff #a0000000 std
MENU COLOR help         37;40   #c0ffffff #a0000000 std
MENU COLOR timeout_msg  37;40   #80ffffff #00000000 std
MENU COLOR timeout      1;37;40 #c0ffffff #00000000 std
MENU COLOR msg07        37;40   #90ffffff #a0000000 std
MENU COLOR tabmsg       31;40   #30ffffff #00000000 std

LABEL arch
        MENU LABEL Arch Linux
        LINUX ../vmlinuz-linux
        APPEND root=/dev/sda2 ro
        INITRD ../initramfs-linux.img

LABEL archfallback
        MENU LABEL Arch Linux Fallback
        LINUX ../vmlinuz-linux
        APPEND root=/dev/sda2 ro
        INITRD ../initramfs-linux-fallback.img

```

Dalla versione 3.84 di Syslinux, `vesamenu.c32` supporta il parametro `MENU RESOLUTION $ALTEZZA $LARGHEZZA`. Per utilizzarlo, si inserisca ad esempio `MENU RESOLUTION 900 1440` nel proprio file di configurazione. Si noti tuttavia che l'immagine di sfondo dovrà essere della stessa risoluzione, altrimenti Syslinux si rifiuterà di caricare il menù.

Per centrare il menù e modificare la risoluzione, si utilizzino i comandi `MENU RESOLUTION`, `MENU HSHIFT $N` e `MENU VSHIFT $N`, dove `$N` è un intero positivo. I valori di default sono `0`, che corrispondono all'angolo in alto a sinistra del monitor. Similmente, inserire un numero positivo posizionerà il testo dal lato opposto dello schermo (ad esempio, `VHSHIFT -4` posiziona il cursore 4 righe sotto il fondo dello schermo).

Per centrare il menù, si utilizzino questi valori:

 `/boot/syslinux/syslinux.cfg` 
```
MENU RESOLUTION 800 600 # inserire la risoluzione in uso
MENU WIDTH 78           # larghezza menù richiesta per il corretto dimensionamento del menù box
MENU VSHIFT 10          # muove il menù verso il basso
MENU HSHIFT 10          # muove il menù vero l'alto

```

Gli standard VESA prevedono una dimensione massima di 25 righe e 80 colonne. Impostare valori più alti potrebbe impedire la corretta visualizzazione del menù, richiedendo la modifica del file di configurazione da un LiveCD.

### Parametri del kernel

È possibile passare [parametri](/index.php/Kernel_parameters "Kernel parameters") al kernel utilizzando la variabile `APPEND` in `syslinux.cfg`. È raccomandabile applicare le stesse modifiche alla voce per il boot dell'immagine fallback.

**Nel caso più semplice**, sarà necessario sostituire il valore del parametro `root`: si modifichi quindi `/dev/sda2` con il valore corretto.

**Se si desidera usare gli [UUID](/index.php/Persistent_block_device_naming_(Italiano)#By-uuid "Persistent block device naming (Italiano)")** per la [nomenclatura persistende dei dispositivi a blocchi](/index.php/Persistent_block_device_naming_(Italiano) "Persistent block device naming (Italiano)") si modifichi la riga APPEND inserendo l'UUID della propria partizione root:

```
APPEND root=UUID=*1234* rw

```

**Se si usa il sistema di cifratura [LUKS](/index.php/LUKS "LUKS")**, si modifichi la riga `APPEND` affinchè Syslinux utilizzi il volume criptato:

```
APPEND root=/dev/mapper/*gruppo*-*nome* cryptdevice=/dev/sda2:*nome* rw

```

Se si utilizza un [Wikipedia:RAID](https://en.wikipedia.org/wiki/RAID "wikipedia:RAID") software attraverso [mdadm](http://neil.brown.name/blog/mdadm), si modifichi la linea `APPEND` in modo da comprendere gli array del vostro RAID.

Nell'esempio che segue vengono utilizzati tre array in RAID 1 e impostato quello corretto come root:

```
APPEND root=/dev/md1 rw md=0,/dev/sda2,/dev/sdb2 md=1,/dev/sda3,/dev/sdb3 md=2,/dev/sda4,/dev/sdb4

```

Se si riscontrano problemi con il boot da una partizione situata su un raid software usando il metodo di cui sopra, si provino ad utilizzare le etichette delle partizioni:

```
 APPEND root=LABEL=ETICHETTA_PARTIZIONE_ROOT ro

```

**Se si utilizza un sottovolume [btrfs](/index.php/Btrfs "Btrfs")**, si modifichi la riga `APPEND` come segue: `rootflags=subvol=<sottovolume root>`. Ad esempio, se `/dev/sda2` è stato montato come sottovolume btrfs chiamato 'ROOT' (esempio: `mount -o noatime,subvol=ROOT /dev/sda2 /mnt`):

```
APPEND root=/dev/sda2 rw rootflags=subvol=ROOT

```

La mancata applicazione delle modifiche di cui sopra, causerà il seguente messaggio di errore: `ERROR: Root device mounted successfully, but /sbin/init does not exist.`.

### Boot automatico

Se non si desidera visualizzare il menù di Syslinux ed effettuare direttamente il boot, si veda [#Prompt di boot](#Prompt_di_boot), ci si assicuri che `PROMPT` abbia valore `0` e si commentino eventuali tutte le voci di menu `UI`. Potrebbe essere utile assegnare al parametro `TIMEOUT` il valore `0`. Assicurarsi inoltre che il parametro `DEFAULT` esista nel proprio `syslinux.cfg`.

### Sicurezza

Syslinux dispone di due livelli di sicurezza: una master password per il menu ed una per ogni singola voce di avvio. Si inserisca in `syslinux.cfg` quanto segue:

```
MENU MASTER PASSWD passwd

```

per impostare una master password e:

```
MENU PASSWD passwd

```

all'interno di un blocco `LABEL` per proteggere con password voci individuali.

La password può essere espressa in chiaro o tramite il suo hash. Si veda in tal senso la [documentazione ufficiale](https://wiki.syslinux.org/wiki/index.php/Comboot/menu.c32).

### Chainloading

**Nota:** Syslinux BIOS non è in grado di effettuare il chainload dei files su partizioni differenti da quella di installazione, tutavia il modulo `chain.c32` può avviare il boot sector delle partizioni (VBR).

Se si desidera effettuare il chainload di altri sistemi operativi (ad esempio Windows) o altri bootloader, si copi il modulo `chain.c32` nella directory di Syslinux (per i dettagli si consulti la sezione precedente). Si crei quindi la seguente sezione nel file di configurazione:

 `/boot/syslinux/syslinux.cfg` 
```

LABEL windows
        MENU LABEL Windows
        COM32 chain.c32
        APPEND hd0 3

```

`hd0 3` rappresenta la terza partizione del primo disco identificato dal BIOS. I dischi sono contati partendo da zero, mentre le partizioni da uno.

**Nota:** Le operazioni di cui sopra inibiscono il funzionamento del boot manager di Windows `bootmgr`, necessario per la corretta applicazione di alcuni aggiornamenti (ad esempio [qui](http://support.microsoft.com/kb/2883200)). In questi casi potrebbe essere utile impostare temporaneamente il flag Boot sulla partizione di Windows utilizzando [GParted](/index.php/GParted "GParted"), applicare l'aggiornamento e poi reimpostare il flag boot sulla partizione di Syslinux. (esempio con [DiskPart](http://www.online-tech-tips.com/computer-tips/set-active-partition-vista-xp) per Windows).

Se non si è sicuri di quale drive venga identificato dal vostro BIOS come primo, è possibile utilizzare l'identificativo MBR oppure, se si usa GPT, l'etichetta del filesystem. Per utilizzare l'identificativo MBR si utilizzi il comando:

```
# fdisk -l /dev/sdb

Disk /dev/sdb: 128.0 GB, 128035676160 bytes 
255 heads, 63 sectors/track, 15566 cylinders, total 250069680 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0xf00f1fd3

Device Boot      Start         End      Blocks   Id  System
/dev/sdb1            2048     4196351     2097152    7  HPFS/NTFS/exFAT
/dev/sdb2         4196352   250066943   122935296    7  HPFS/NTFS/exFAT

```

sostituendo `/dev/sdb` all'identificativo del drive del quale si vuole effettuare il chainload. Utilizzando il valore esadecimale reperibile in `Disk identifier:`, la sintassi del `syslinux.cfg` sarà:

```
 LABEL windows
        MENU LABEL Windows
        COM32 chain.c32
        APPEND mbr:0xf00f1fd3

```

Per ulteriori dettagli sul chainloading si veda: [[1]](http://syslinux.zytor.com/wiki/index.php/Comboot/chain.c32).

Se [GRUB2](/index.php/GRUB2_(Italiano) "GRUB2 (Italiano)") è installato nella propria partizione di boot, è possibile effettuarne il chainload utilizzando:

 `/boot/syslinux/syslinux.cfg` 
```

LABEL grub2
       MENU LABEL Grub2
       COM32 chain.c32
       append file=../grub/boot.img

```

In alternativa, è possibile caricare [GRUB](/index.php/GRUB_(Italiano) "GRUB (Italiano)") come kernel linux, facendo precedere `lnxboot.img` a `core.img`. Il file `lnxboot.img` fa parte del pacchetto [grub](https://www.archlinux.org/packages/?name=grub) e può essere trovato in `/usr/lib/grub/i386-pc`.

 `/boot/syslinux/syslinux.cfg` 
```
...
 LABEL grub2lnx
        MENU LABEL Grub2 (lnxboot)
        LINUX ../grub/i386-pc/lnxboot.img
        INITRD ../grub/i386-pc/core.img
...

```

Quanto sopra potrebbe essere necessario per avviare immagini ISO.

### Chainloading di un altro sistema Linux

Quando si effettua il chainloading di un bootloader come quello di Windows, non ci sono problemi, in quanto si dispone di un bootloader da avviare, mentre Syslinux è in grado di caricare files che risiedono sulla stessa partizione del file di configurazione. Se quindi si ha un'altra versione di Linux installata su una partizione differente e senza `/boot` separata, è *necessario* utilizzare Extlinux al posto del bootloader di default (ad esempio GRUB). In poche parole, è possibile installare Extlinux sul superblocco della partizione/[VBR](https://en.wikipedia.org/wiki/Volume_boot_record "wikipedia:Volume boot record") per poi essere richiamato come *bootloader separato* dal Syslinux installato nel MBR. Extlinux fa parte del progetto Syslinux ed è incluso nel pacchetto [syslinux](https://www.archlinux.org/packages/?name=syslinux).

Le seguenti istruzioni presuppongono che si sia già installato Syslinux, che il path al file di configurazione sia `/boot/syslinux` e che il sistema di cui effettuare il chainload risieda su `/dev/sda3`.

Una volta avviata la distribuzione che Syslinux avvia di default, si monti la partizione di root dell'altra distribuzione su un mount point a piacere. In questo esempio si utilizzerà `/mnt`; si noti che se si usa una partizione di boot separata sarà necessario montarla: l'esempio assume che questa sia `/dev/sda2`.

```
# mount /dev/sda3 /mnt
# mount /dev/sda2 /mnt/boot (necessario solamente per /boot separata)

```

Si installi Extlinux nel VBR della partizione e si copino i moduli `*.c32` necesari:

```
# extlinux -i /mnt/boot/syslinux (creare la directory, se necessario)
# cp /usr/lib/syslinux/bios/*.c32 /mnt/boot/syslinux

```

Si crei `/mnt/boot/syslinux/syslinux.cfg`. È possibile utilizzare come riferimento il file menu del sistema madre (segue esempio):

```
/boot/syslinux/syslinux.cfg **su /dev/sda3**

```

```
timeout 10
ui menu.c32

label Other Linux
    linux /boot/vmlinuz-linux
    initrd /boot/initramfs-linux.img
    append root=/dev/sda3 ro quiet

label MAIN
    com32 chain.c32
    append hd0 0

```

Tratta dalla [pagina utente](/index.php/User:Djgera "User:Djgera") di Djgera.

Si noti che la voce relativa all'altro sistema in `<altro-OS>/boot/syslinux/syslinux.cfg` dovrà essere modificata ogni volta che se ne aggiorna il kernel, dal momento che sti sta avviando direttamente quest'ultimo, al posto di effettuare il chainloading del bootloader di default.

### Usare memtest

Si installi [memtest86+](https://www.archlinux.org/packages/?name=memtest86%2B) dai [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

Si utilizzi questa sezione `LABEL` per effettuare il boot di memtest.

 `/boot/syslinux/syslinux.cfg` 
```

LABEL memtest
        MENU LABEL Memtest86+
        LINUX ../memtest86+/memtest.bin

```

**Nota:** Se si utilizza pxelinux, si cambi il nome del file da `memtest.bin` a `memtest`, poichè pxelinux tratta i files con estensione `.bin` come boot sector e ne carica solo i primi 2 KiB.

### HDT

[HDT (Hardware Detection Tool)](http://hdt-project.org/) è uno strumento per visualizzare informazioni sull'hardware. Come sempre, il rispettivo modulo `.c32` dovrà essere copiato in `/boot/syslinux`. Per i dispositivi PCI, si copi `/usr/share/hwdata/pci.ids` in `/boot/syslinux/pci.ids` e si aggiunga quanto segue al proprio file di configurazione:

 `/boot/syslinux/syslinux.cfg` 
```

LABEL hdt
        MENU LABEL Hardware Info
        COM32 hdt.c32

```

### Riavvio e spegnimento

**Nota:** A partire da Syslinux 6.03, `poweroff.c32` funziona solamente con APM e non con ACPI. Per una possibile soluzione si veda [questa discussione](http://www.syslinux.org/archives/2012-March/017661.html).

Si usino le seguenti sezioni per riavviare o spegnere la macchina:

 `/boot/syslinux/syslinux.cfg` 
```

LABEL reboot
        MENU LABEL Reboot
        COM32 reboot.c32

LABEL poweroff
        MENU LABEL Power Off
        COM32 poweroff.c32

```

### Menù pulito

Per pulire lo schermo dopo l'uscita dal menù, si aggiunga la seguente riga al file di configurazione:

```
MENU CLEAR

```

### Mappatura tastiera

Se si necessita di modificare continuamente i propri parametri di boot, si potrebbe voler cambiare la mappatura della tastaera, affinchè risulti più facile inserire i caratteri `=`, `/` ed altri su una tastiera non americana.

Innanzitutto si deve creare una mappatura compatibile (nell'esempio si utilizzerà quella tedesca):

**Nota:** Sarà necessario creare anche `us.keymap`, o l'esempio non funzionerà.

```
$ cp /usr/share/kbd/keymaps/i386/qwertz/de.map.gz .
$ cp /usr/share/kbd/keymaps/i386/qwerty/us.map.gz .
$ gunzip de.map.gz
$ gunzip us.map.gz
$ mv de.map de.kmap
$ mv us.map us.kmap
# keytab-lilo us de > de.ktl

```

Si copi `de.ktl` in `/boot/syslinux` e si imposti il proprietario a `root`:

```
# chown root:root /boot/syslinux/de.ktl

```

Ora si modifichi il proprio `syslinux.cfg` aggiungendo:

 `/boot/syslinux/syslinux.cfg` 
```
KBDMAP de.ktl

```

### Nascondere il menu

Si utilizzi l'opzione

 `/boot/syslinux/syslinuxcfg`  `MENU HIDDEN` 

per nascondere il menu e visualizzare solamente il timeout. Si prema un tasto qualsiasi per mostrarlo nuovamente.

### Pxelinux

**Nota:** Su sistemi UEFI, Syslunux utilizza lo stesso eseguibile sia per il boot da disco che per quello via rete. Sarà necessario avviare Syslinux in modalità di rete per il trasferimento di eventuali files tramite TFTP o altri protocolli di rete.

Pxelinux è fornito dal pacchetto [syslinux](https://www.archlinux.org/packages/?name=syslinux).

Si copi il bootloader `pxelinux.0` (fornito dal pacchetto [syslinux](https://www.archlinux.org/packages/?name=syslinux) nella directory `/boot` del client. Per versioni 5.00 e successive, si copi inoltre il file `ldlinux.c32` dallo stesso pacchetto:

```
# cp /usr/lib/syslinux/bios/pxelinux.0 "$root/boot"
# cp /usr/lib/syslinux/bios/ldlinux.c32 "$root/boot"
# mkdir "$root/boot/pxelinux.cfg"

```

Si noti la creazione della directory `pxelinux.cfg`, dove PXELINUX cerca il file di configurazione di default. Dal momento che non si intende fare differenze tra i MAC dei vari host, sarà creato il file di configurazione `default`.

 `# vim "$root/boot/pxelinux.cfg/default"` 
```
default linux

label linux
kernel vmlinuz-linux
append initrd=initramfs-linux.img quiet ip=:::::eth0:dhcp nfsroot=10.0.0.1:/arch

```

Se si utilizza NBD, modificare la riga `append` come segue:

```
append ro initrd=initramfs-linux.img ip=:::::eth0:dhcp nbd_host=10.0.0.1 nbd_name=arch root=/dev/nbd0

```

**Nota:** Sarà necessario modificare `nbd_host` e `nfsroot` a seconda della configurazione della propria rete, ovvero a seconda dell'indirizzo del proprio server NFS/NBD.

La sintassi del file di configurazione di PXELINUX è identica a quella di Syslinux: si faccia riferimento alla documentazione ufficiale per ulteriori informazioni.

Il kernel e l'initrd saranno trasmessi via TFTP, perciò i percorsi saranno relativi alla root del server TFTP, oppure il filesystem root potrebbe essere proprio quello montato tramite NFS: in questo caso i percorsi saranno relativi alla root del server NFS.

Per avviare pxelinux, si sostituisca `filename "/grub/i386-pc/core.0";` nel file `/etc/dhcpd.conf` con `filename "/pxelinux.0"`.

### Avviare un'immagine ISO 9660 tramite memdisk

Syslinux supporta l'avvio di immagini ISO tramite il modulo [memdisk](https://wiki.syslinux.org/wiki/index.php/MEMDISK); si veda [Multiboot USB drive#Using Syslinux and memdisk](/index.php/Multiboot_USB_drive#Using_Syslinux_and_memdisk "Multiboot USB drive") per ulteriori esempi.

### Utilizzare la console seriale

Per abilitare la console seriale, si aggiunga `SERIAL port [baudrate]` in cima al proprio `syslinux.cfg`. *port* è un numero (0 per `/dev/ttyS0`). Se *baudrate* viene omesso, il default è 9600 bps. I parametri per la trasmissione seriale sono preimpostati a 8 bit, nessuna parità e 1 bit di stop. [[2]](https://wiki.syslinux.org/wiki/index.php/SYSLINUX#SERIAL_port_.5Bbaudrate_.5Bflowcontrol.5D.5D.)

 `syslinux.cfg` 
```
SERIAL 0 115200

```

Si abiliti la console seriale all'avvio aggiungendo `console=tty0 console=ttyS0,115200n8` al parametro `APPEND`. [[3]](http://www.mjmwired.net/kernel/Documentation/kernel-parameters.txt#681)

 `syslinux.cfg`  `APPEND root=UUID=126ca36d-c853-4f3a-9f46-cdd49d034ce4 rw console=tty0 console=ttyS0,115200n8` 

Abilitare la console seriale su GRUB: [Working with the serial console#GRUB2 and systemd](/index.php/Working_with_the_serial_console#GRUB2_and_systemd "Working with the serial console").

## Risoluzione dei problemi

### Utilizzare il prompt di Syslinux

È possiblie scrivere il valore del parametro `LABEL` corrispondente al sistema operativo che si vuole eseguire. Se si sono utilizzate le configurazioni d'esempio, si scriva:

```
boot: arch

```

Se si ottiene un errore di caricamento del file di configurazione, èp possibile passare manualmente i parametri di boot:

```
boot: ../vmlinuz-linux root=/dev/sda2 ro initrd=../initramfs-linux.img

```

Se non si ha accesso a `boot:` in [ramfs](/index.php/Ramdisk "Ramdisk") e si è quindi impossibilitati ad effettuare il boot del kernel, si proceda come segue:

	1\. Si crei una directory temporanea per montare la propria partizione root (se non esiste già):

```
# mkdir -p /new_root

```

	2\. Si monti `/` in `/new_root` (Se boot è si una partizione separata, si dovrà montare anche quest'ultima):

**Nota:** Busybox non può montare `/boot` se quest'ultima si trova su una partizione ext2 dedicata.

```
# mount /dev/sd[a-z][1-9] /new_root

```

	3\. Si utilizzi `vim` e si modifichi il proprio `syslinux.cfg` secondo le proprie preferenze e si salvi.

	4\. Riavviare.

### Il fsck fallisce sulla partizione root

Nell'eventualità di una partizione root corrotta (con danni al journal) si monti il filesystem di root nella shell di emergenza del ramfs:

```
# mount /dev/*partizione root* /new_root;  ## Si monti la partizione root

```

Procurarsi l'eseguibile tune2fs dalla partizione root (non è incluso in syslinux):

```
# cp /new_root/sbin/tune2fs /sbin/;

```

Si seguano quindi le [seguenti](/index.php/Fsck#ext2fs_:_no_external_journal "Fsck") istruzioni per creare un nuovo journal per la partizione root.

### DEFAULT o UI non trovati

Alcuni produttori di schede madri non hanno un buon supporto al boot da dispositivi USB. Se, ad esempio, un drive USB formattato in Ext4 potrebbe bootare tranquillamente su un PC più recente, macchine più vecchie potrebbero bloccarsi se la partizione di boot contenente "kernel" e "initrd" non si trova su una partizione FAT16\. Per ovviare al problema, si crei una partizione FAT16 (con dimensione minore o uguale a 2GB) e la si formatti con [dosfstools](https://www.archlinux.org/packages/?name=dosfstools):

```
# mkfs.dosfs -F 16 /dev/sda1

```

Poi si installi e configuri Syslinux.

### Missing Operating System

*   Si verifichi di aver installato `gptmbr.bin` per sistemi di partizionamento GPT o `mbr.bin` per tabelle partizioni DOS. `mbr.bin` visualizza il messaggio d'errore *Missing operating system*, mentre `gptmbr.bin` mostra *Missing OS*.

*   Si verifichi se la partizione che contiene `/boot` è contrassegnata come avviabile.

*   Si verifichi tramite `fdisk -l` se la prima partizione del disco avviabile inizia al settore 1 al posto del settore 63 o 2048\. In questo caso è possibile spostare le partizioni tramite `gparted` utilizzando un disco di ripristino. Se si dispone di una partizione `/boot` separata, è possibile effettuarne il backup tramite:

```
# cp -a /boot /boot.bak

```

Si effettui quindi il boot con il disco di installazione di Arch. Si usi poi `cfdisk` per cancellare la partizione di `/boot` e la si ricrei: ora dovrebbe iniziare al settore giusto (63). Si montino quindi le proprie partizioni e si effettui il chroot nel sistema Arch installato su disco, come descritto nella Beginners guide. Si ripristini il backup di `/boot` con:

```
# cp -a /boot.bak/* /boot

```

Si controlli se `/etc/fstab` è corretto e poi si esegua:

```
# syslinux-install_update -iam

```

Si riavvii quindi il sistema.

È possibile ottenere questo errore anche se si prova ad effettuare il boot da un array [RAID](/index.php/RAID_(Italiano) "RAID (Italiano)") `md1` creato con una versione dei metadata non supportata da Syslinux. A partire da Agosto 2013, [mdadm](https://www.archlinux.org/packages/?name=mdadm) crea un array con la versione metadata `1.2`, mentre Syslinux supporta solo la `1.0`. Sarà quindi necessario ricreare il proprio array RAID passando l'opzione `--metadata=1.0` a `mdadm`.

### Viene eseguito Windows al posto di Syslinux!

**Soluzione:** Assicurarsi che la partizione di `/boot` abbia la flag di boot attiva e che quella di Windows non la abbia. Si veda la sezione "Installazione" di questo articolo per ulteriori dettagli.

Il MBR che fornisce Syslinux cerca la prima partizione attiva ad avere la flag di boot abilitata, quindi è probabile che quella di Windows sia stata trovata per prima e che avesse la flag di boot attiva. Se lo si desidera, è possbiile utilizzare anche il MBR fornito da Windows o MS-DOS fdisk.

### Le voci del menù non hanno effetto

Se si seleziona una voce del menù di boot e non succede niente a parte il ricaricamento dello stesso, è probabile che si abbia un errore nel proprio `syslinux.cfg`. Si prema `tab` per modificare i propri parametri di boot. In alternativa si prema `esc` e si scriva il valore del parametro `LABEL` corrispondente al sistema da avviare (ad esempio `arch`).

Il problema potrebbe anche essere causato dall'assenza di un kernel. Si acceda al proprio filesystem tramite LiveCD, si monti la propria partizione `/boot` ed assicurarsi che `/puntodimount/vmlinuz-linux` esista e non abbia dimensione 0\. In caso procedere con [Kernel Panics#Option 2: Reinstall kernel](/index.php/Kernel_Panics#Option_2:_Reinstall_kernel "Kernel Panics").

### Impossibile rimuovere ldlinux.sys

Il file `ldlinux.sys` ha l'attributo *immutable* impostato, che ne impedisce la rimozione o sovrascrittura. Questo comportamento si verifica poichè il settore sul quale risiede il file in questione non deve cambiare, altrimenti Syslinux dovrà essere reinstallato.

Per rimuovere il file si esegua:

```
# chattr -i /boot/syslinux/ldlinux.sys
# rm /boot/syslinux/ldlinux.sys

```

### Viene visualizzato un quadretto bianco nell'angolo in alto a sinistra dello schermo quando si sta usando vesamenu

Problema:

*A partire da linux-3.0, il driver del modesetting tenta di mantenere il contenuto corrente dello schermo dopo il cambio di risoluzione (o almeno questo si verifica sulla mia Intel, quando utilizzo Syslinux in modalità testuale). Pare che tale comportamento crei problemi se si usa il modulo vesamenu di Syslinux (il quadrato bianco rappresenta infatti un tentativo di salvare il menù di Syslinux, ma il driver non riesce a catturare l'immagine dalla modalità grafica VESA)*.

Se si è scelta una risoluzione personalizzata e si utilizza vesamenu assieme al modesetting, si provi ad inserire la seguente riga nel `syslinux.cfg` per rimuovere il quadretto bianco e continuare il boot in modalità grafica:

```
APPEND root=/dev/sda6 ro 5 **vga=current** quiet splash

```

### Il chainloading del bootloader di Windows non funziona quando Windows si trova su un drive diverso

Se Windows è installato in un hard disk diverso da Arch e si riscontrano problemi nel chainloading, si provi con la seguente configurazione:

```
LABEL Windows
        MENU LABEL Windows
        COM32 chain.c32
        APPEND mbr:0xdfc1ba9e swap

```

si sostituisca il codice MBR con quello del drive dove è installato Windows (Si veda [sopra](#Chainloading)), e si aggiunga `swap` alle opzioni.

### Leggere i log del bootloader

In alcuni casi (ad esempio quando il bootloader non è in grado di effettuare il boot del kernel, è utile poter ottenere più informazioni sul processo di avvio. *Syslinux* stampa eventuali messaggi d'errore a schermo, che vengono però subito sostituiti dal menu. Per evitare di perdere queste informazioni sarà necessario disabilitare l'interfaccia del menu in `syslinux.cfg` e utilizzare il prompt d'avvio di default, il che si traduce nell'evitare:

*   direttive `UI`
*   `ONTIMEOUT`
*   `ONERROR`
*   `MENU CLEAR`

*   aumentare il valore di `TIMEOUT`
*   utilizzare `PROMPT 1`
*   utilizzare `DEFAULT <label che causa il problema>`

Per ottenere informazioni di debug più dettagliate sarà necessario ricompilare [syslinux](https://www.archlinux.org/packages/?name=syslinux) con CFLAGS aggiuntive:

```
-DDEBUG_STDIO=1 -DCORE_DEBUG=1

```

### Compressione BTRFS

L'avvio da partizioni BTRFS compresse non è supportato. [[4]](https://wiki.syslinux.org/wiki/index.php/Syslinux_4_Changelog#Changes_in_4.02)

Verrà visualizzato il seguente messaggio d'errore:

```
btrfs: found compressed data, cannot continue!
invalid or corrupt kernel image.

```

[GRUB](/index.php/GRUB_(Italiano) "GRUB (Italiano)") supporta l'avvio da partizioni BTRFS compresse.

## Vedere anche

*   Il [sito](http://www.syslinux.org/) del progetto Syslinux.
*   [configurazione di PXELinux](http://www.josephn.net/scrapbook/pxelinux_stuff)
*   [Penna USB Multiboot utilizzando Syslinux](http://blog.jak.me/2013/01/03/creating-a-multiboot-usb-stick-using-syslinux/)