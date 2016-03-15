Il Master Boot Record (MBR) comprende i primi 512 byte di un dispositivo di memorizzazione. Il MBR non è una partizione; è riservato al bootloader del sistema operativo e alla tabella delle partizioni del dispositivo di memorizzazione. Una nuova alternativa a MBR può essere la [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table"), che fa parte delle specifiche dell'[Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface_(Italiano) "Unified Extensible Firmware Interface (Italiano)").

## Contents

*   [1 Processo di Boot](#Processo_di_Boot)
*   [2 Storia](#Storia)
*   [3 Backup e ripristino](#Backup_e_ripristino)
*   [4 Ripristinare un boot record Windows](#Ripristinare_un_boot_record_Windows)
*   [5 Altre risorse](#Altre_risorse)

## Processo di Boot

L'avvio è un processo con più fasi. La maggior parte dei PC oggi inizializzano i dispositivi di sistema con un firmware chiamato [BIOS](https://en.wikipedia.org/wiki/BIOS e [Syslinux](/index.php/Syslinux_(Italiano) "Syslinux (Italiano)").

## Storia

L'MBR consiste in una piccola porzione di codice assembly (il bootloader - 446 byte), la tavola delle partizioni per le 4 partizioni primarie (16 byte ciascuna) ed una chiusura detta *sentinel* (0xAA55).

Il codice del bootloader "Convenzionale" sull'MBR di sistemi Windows/DOS controlla la tavola delle partizioni alla ricerca di una, e solo una, partizione *attiva*, legge X settori da essa è trasferisce il controllo al sistema operativo. Il bootloader di Windows/DOS *non* effettua il boot da una partizione di Arch Linux perché non è progettato per avviare il kernel Linux, e può occuparsi di una partizione *attiva* e *primaria* (queste caratteristiche non influenzano GRUB).

Il bootloader [GRand Unified Bootloader (GRUB)](/index.php/GRUB_(Italiano) "GRUB (Italiano)") è di fatto il bootloader per sistemi GNU/Linux, e gli utenti sono invitati ad installarlo sull'MBR per permettere il boot da *qualsiasi* partizione, che sia primaria o logica.

## Backup e ripristino

Dato che l'MBR è situato sul disco, può esserne effettuato il backup e successivamente ripristinato.

Per effettuare il backup dell'MBR:

```
dd if=/dev/hda of=/path/mbr-backup bs=512 count=1

```

Per ripristinare l'MBR:

```
dd if=/path/mbr-backup of=/dev/hda bs=512 count=1

```

**Attenzione:** Ripristinare l'MBR con una tavola delle partizioni differente renderà i dati illeggibili e quasi impossibili da recuperare. Se si ha la necessità di reinstallare il bootloader consultare [GRUB](/index.php/GRUB_(Italiano) "GRUB (Italiano)") o [Syslinux](/index.php/Syslinux_(Italiano) "Syslinux (Italiano)").

Per cancellare l'MBR (può essere utile se si desidera fare una completa installazione di un altro sistema operativo) basterà cancellare i primi 446 byte perché negli altri byte dell'MBR è memorizzata la tavola delle partizioni:

```
dd if=/dev/zero of=/dev/hda bs=446 count=1

```

## Ripristinare un boot record Windows

Per convenzione (e per facilitare l'installazione), Windows viene installato sulla prima partizione ed installa la sua tavola delle partizioni ed il suo bootloader punta al primo settore di questa partizione. Se accidentalmente si installa un bootloader come GRUB sulla partizione Windows o il boot record viene danneggiato in altri modi, sarà necessario usare un utility per ripararlo. Microsoft nei recovery CD ed a volte nei CD di installazione, include un utility per riparare il boot sector `FIXBOOT` ed un utility per riparare l'MBR chiamata `FIXMBR`. Usando questo metodo si può rispettivamente riparare il riferimento al settore di boot della prima partizione nel file del bootloader e riparare il riferimento alla prima partizione sull'MBR. Dopo aver fatto questo, sarà necessario [reinstallare GRUB](/index.php/GRUB_(Italiano)#Installazione "GRUB (Italiano)") sull'MBR se si desidera effettuare il boot da esso (GRUB può essere configurato per caricare il bootloader di Windows).

Se si desidera ritornare ad utilizzare l'MBR ed il bootloader di Windows, sarà possibile usare il comando `FIXBOOT` che collega l'MBR al settore di boot della prima partizione così avviando in automatico il sistema Windows.

Esiste anche una utility per Linux chiamata `ms-sys` (il pacchetto [ms-sys](https://aur.archlinux.org/packages/ms-sys/) è disponibile su [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)")), questa utility permette di installare MBR. Comunque questa utility è attualmente capace di scrivere nuovi MBR (tutti i sistemi operativi ed i file system sono supportati) e nuovi settori di avvio(anche detti boot record ad esempio come eseguire il comando `FIXBOOT`) per file systems FAT. Molti live CD non hanno questa utility per default quindi sarà necessario installarla prima, oppure sarà necessario cercare un sistema live che la contenga come [Parted Magic](http://partedmagic.com/).

Per primo riscrivere le informazioni delle partizioni (tavola delle partizioni) con il comando:

```
ms-sys --partition /dev/sda1

```

Successivamente scrivere un MBR per Windoows 2000/XP/2003:

```
ms-sys --mbr /dev/sda  # Leggere le opzioni per versioni differenti

```

Poi scrivere il nuovo settore di avvio (boot record)

```
ms-sys -(1-6)          # Leggere le opzioni per scoprire il corretto tipo di record FAT

```

`ms-sys` può anche scrivere MBR per Windows 98, ME, Vista, e 7 MBR, consultare `ms-sys -h`.

## Altre risorse

*   [Cosa è il Master Boot Record (MBR)? (in Inglese)](http://kb.iu.edu/data/aijw.html)