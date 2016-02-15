Per avviare Linux è necessario aver installato nel [Master Boot Record](/index.php/Master_Boot_Record_(Italiano) "Master Boot Record (Italiano)") o nella [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table") un [boot loader](/index.php/Boot_loaders "Boot loaders") compatibile con Linux, come [GRUB](/index.php/GRUB_(Italiano) "GRUB (Italiano)") o [Syslinux](/index.php/Syslinux_(Italiano) "Syslinux (Italiano)"). Il boot loader è responsabile per il caricamento del kernel e il [ramdisk iniziale](/index.php/Mkinitcpio_(Italiano) "Mkinitcpio (Italiano)") prima di iniziare il processo di boot. La procedura è piuttosto differente tra sistemi [BIOS](https://en.wikipedia.org/wiki/it:BIOS "wikipedia:it:BIOS") e [UEFI](/index.php/UEFI "UEFI"), e la descrizione dettagliata è presentata in questa pagina o quelle collegate.

## Contents

*   [1 Processo di boot](#Processo_di_boot)
    *   [1.1 Con BIOS](#Con_BIOS)
    *   [1.2 Con UEFI](#Con_UEFI)
*   [2 Kernel](#Kernel)
*   [3 initramfs](#initramfs)
*   [4 Processo init](#Processo_init)
*   [5 Altre risorse](#Altre_risorse)

## Processo di boot

### Con BIOS

1.  Accensione del sistema - [Power-on self-test](https://en.wikipedia.org/wiki/it:Power-on_self-test "wikipedia:it:Power-on self-test") o POST
2.  Dopo il POST, il BIOS inizializza l'hardware necessario per il boot (dischi, controller della tastiera ecc.)
3.  Il BIOS esegue i primi 440 byte ([Master Boot Record](/index.php/Master_Boot_Record_(Italiano) "Master Boot Record (Italiano)")) del primo disco rigido secondo l'ordine del BIOS
4.  Il codice di boot nell'MBR prende quindi il controllo dal BIOS e esegue il prossimo blocco di codice (se esistente) (in genere un [boot loader](/index.php/Boot_loaders "Boot loaders"))
5.  Il secondo codice lanciato (il vero boot loader) legge quindi i suoi file ausiliari e di configurazione
6.  Basandosi sui valori nei propri file di configurazione, il boot loader carica il kernel e l'initramfs nella memoria di sistema (RAM) ed infine esegue il kernel

### Con UEFI

Leggere [Unified Extensible Firmware Interface (Italiano)#Processo di boot con UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Italiano)#Processo_di_boot_con_UEFI "Unified Extensible Firmware Interface (Italiano)").

## Kernel

Il kernel è il cuore di un sistema operativo. Esso lavora a basso livello (_kernelspace_) interagendo tra le periferiche della macchina, ed i programmi che ne richiedono le risorse per funzionare. Per sfruttare la CPU in modo efficiente, il kernel usa un sistema di pianificazione per decidere a quale processo assegnare la priorità e quando, creando così l'illusione (per l'occhio umano) che i processi vengano eseguiti contemporaneamente.

## initramfs

Dopo essere stato caricato, il kernel decomprime l'[initramfs](/index.php/Initramfs "Initramfs") (initial RAM filesystem), che diventa il file system di root iniziale. Il kernel successivamente esegue `/init` come primo processo. La fase _early userspace_ inizia.

L'obiettivo di initramfs è di effettuare il bootstrap del sistema fino a che quest'ultimo non sia in gradi di accedere al filesystem di root (vedi [FHS](/index.php/Filesystem_Hierarchy_Standard_(Italiano) "Filesystem Hierarchy Standard (Italiano)") per maggiori informazioni). Ciò significa che ogni modulo richiesto dalle periferiche come dischi IDE, SCSI, o SATA (oppure USB/FireWire, se si effettua il boot da una di queste periferiche) deve essere caricabile dall'initramfs se non è stato compilato all'interno del kernel; Una volta che sono caricati i moduli necessari, (sia da un programma, sia con uno script, o tramite [udev](/index.php/Udev_(Italiano) "Udev (Italiano)")), il processo di boot continua. Per questa ragione nell'initramfs è necessaria la sola presenza dei moduli assolutamente indispensabili per l'accesso al filesystem di root; non è quindi necessario che contenga tutti i moduli che servono al completo funzionamento della macchina. La maggior parte dei moduli sarà caricata in seguito da udev, durante la fase di init.

## Processo init

Alla fase finale della _early userspace_, la vera root è stata montata, e si sostituisce al file system di root iniziale. `/sbin/init` è eseguito, sostituendo il processo `/init`. Arch usa [systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)") come processo init.

## Altre risorse

*   [Early Userspace in Arch Linux](http://archlinux.me/brain0/2010/02/13/early-userspace-in-arch-linux/)
*   [Inside the Linux boot process](http://www.ibm.com/developerworks/linux/library/l-linuxboot/)
*   [Boot with GRUB](http://www.linuxjournal.com/article/4622)
*   [Wikipedia:Linux startup process](https://en.wikipedia.org/wiki/Linux_startup_process "wikipedia:Linux startup process")
*   [Wikipedia:it:initrd](https://en.wikipedia.org/wiki/it:initrd "wikipedia:it:initrd")
*   [Boot Linux Grub Into Single User Mode](http://www.cyberciti.biz/faq/grub-boot-into-single-user-mode/)