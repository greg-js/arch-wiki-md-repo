Questa pagina illustra come posizionare un media d'installazione di Arch su un supporto USB: *chiavette USB*, HD esterni ecc. Il risultato sarà simile ad un LiveCD che perderà tutti i cambiamenti e le impostazioni una volta rimosso.

Nel caso si sia interessati ad installare Arch Linux su un supporto USB si veda [questa pagina](/index.php/Installing_Arch_Linux_on_a_USB_key_(Italiano) "Installing Arch Linux on a USB key (Italiano)").

**Nota:** Per i sistemi [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Italiano) "Unified Extensible Firmware Interface (Italiano)") creare un supporto USB avviabile seguendo [queste](/index.php/Unified_Extensible_Firmware_Interface_(Italiano)#Creare_un_dispositivo_USB_avviabile_con_UEFI_dalla_ISO "Unified Extensible Firmware Interface (Italiano)") istruzioni.

## Contents

*   [1 Su GNU/Linux](#Su_GNU.2FLinux)
    *   [1.1 Sovrascrivendo i dati presenti sul supporto USB](#Sovrascrivendo_i_dati_presenti_sul_supporto_USB)
        *   [1.1.1 Riportare il supporto USB al suo stato originale](#Riportare_il_supporto_USB_al_suo_stato_originale)
    *   [1.2 Senza sovrascrivere tutti i dati presenti sul supporto USB](#Senza_sovrascrivere_tutti_i_dati_presenti_sul_supporto_USB)
        *   [1.2.1 UNetbootin (Metodo sconsigliato)](#UNetbootin_.28Metodo_sconsigliato.29)
*   [2 Su Mac OS X](#Su_Mac_OS_X)
*   [3 Su Windows](#Su_Windows)
    *   [3.1 Image Writer per Windows](#Image_Writer_per_Windows)
    *   [3.2 USBWriter per Windows](#USBWriter_per_Windows)
    *   [3.3 Rufus per Windows](#Rufus_per_Windows)
    *   [3.4 Metodo Flashnul](#Metodo_Flashnul)
    *   [3.5 Metodo Cygwin](#Metodo_Cygwin)
    *   [3.6 dd per Windows](#dd_per_Windows)
    *   [3.7 Avviare l'intera ISO dalla memoria RAM](#Avviare_l.27intera_ISO_dalla_memoria_RAM)
*   [4 Risoluzione problemi](#Risoluzione_problemi)
*   [5 Vedere Anche](#Vedere_Anche)

## Su GNU/Linux

### Sovrascrivendo i dati presenti sul supporto USB

**Attenzione:** Questo distruggerà definitivamente tutti i dati presenti su `/dev/sdx`.

**Nota:** Questo metodo non supporta boot UEFI.

**Nota:** Controllare con `lsblk` che il supporto USB **non** sia montato e assicurarsi di utilizzare `/dev/sdx` e NON `/dev/sdx1`. **Questo è un errore molto comune!**

```
# dd if=/percorso/a/archlinux.iso of=/dev/sd[x] bs=4M

```

**Nota:** Alcuni vecchi firmware hanno problemi con isohybrid. vedere [https://bugs.archlinux.org/task/32189](https://bugs.archlinux.org/task/32189) per un fix riguardante isohybrid.pl.

dove `archlinux.iso` è il percorso del file iso e `/dev/sd[x]` quello del dispositivo USB.

#### Riportare il supporto USB al suo stato originale

Finita l'installazione di Arch Linux, potrebbe essere necessario riformattare il supporto usb. Lo spazio rimanente infatti risulta inaccessibile. Per azzerare completamente la memoria USB usare il comando:

```
# dd count=1 bs=512 if=/dev/zero of=/dev/sdx

```

Ora creare una nuova tabella delle partizioni (ad esempio "msdos") e un filesystem (ad esempio EXT$, FAT32) usando uno strumento a piacere come [gparted](https://www.archlinux.org/packages/?name=gparted), [cfdisk](https://www.archlinux.org/packages/?name=cfdisk):

*   Per EXT2/3/4:

```
# cfdisk /dev/sdx
# mkfs.ext4 /dev/sdx1
# e2label /dev/sdx1 USB_STICK
```

*   Per FAT32, installare il pacchetto [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) e lanciare:

```
# cfdisk /dev/sdx
# mkfs.vfat -F32 /dev/sdx1
# dosfslabel /dev/sdx1 USB_STICK
```

### Senza sovrascrivere tutti i dati presenti sul supporto USB

La procedura è leggermente più complessa del semplice `dd` ma permette di usare il supporto USB anche per l'archivizione di dati diversi dall'immagine che si va a masterizzare. Prima di iniziare è di fondamentale importanza che il supporto che verrà occupato dall'immagine di Arch sia formattato in FAT32, FAT(16), ext2/3/4 o brtfs. Per boot [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Italiano) "Unified Extensible Firmware Interface (Italiano)") o per l'interoperabilità fra sistemi operativi la scelta migliore è FAT32\. Assicurarsi inoltre di aver [installato](/index.php/Pacman_(Italiano) "Pacman (Italiano)") il pacchetto [syslinux](https://www.archlinux.org/packages/?name=syslinux) >= 4.04 disponibile nei [repositotories ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

**1.** Estrarre la directory `arch` dalla iso e copiarla sul dispositivo USB. Per motherboard UEFI seguire [queste](/index.php/Unified_Extensible_Firmware_Interface_(Italiano)#Creare_un_dispositivo_USB_avviabile_con_UEFI_dalla_ISO "Unified Extensible Firmware Interface (Italiano)") istruzioni.

**2.** Installare il bootloader *Syslinux*:

**Attenzione:** Quando si usa il comando `dd` bisogna sempre specificare l'intero dispositivo e non la prima partizione. **Questo è un errore molto comune**

**Nota:** Su alcune distribuzioni il file `mbr.bin` si trova in `/usr/**share**/syslinux/mbr.bin`.

```
# cp /usr/lib/syslinux/bios/*.c32 /mnt/usb/arch/boot/syslinux
# extlinux --install /mnt/usb/arch/boot/syslinux
# dd bs=440 conv=notrunc count=1 if=/usr/lib/syslinux/bios/mbr.bin of=/dev/sdx
# parted /dev/sdx toggle 1 boot

```

**3.** Sistemare i file di configurazione:

**Nota:** È *possibile* etichettare il disco USB con la *label* "`ARCH_2013XX`" (con l'appropriata release mensile) nel file */mnt/usb/loader/entries/archiso-x86_64.conf* ma l'approccio migliore potrebbe essere l'uso degli [UUID](/index.php/Persistent_block_device_naming_(Italiano)#By-uuid "Persistent block device naming (Italiano)"). Non usare gli UUID potrebbe portare al famoso errore: **30 seconds error**.

Per modificare `archisolabel=ARCH_2013XX` nel equivalente `archiso**device**=/dev/disk/by-uuid/47FA-4071` in tutti i file di configurazione allo stesso tempo usando un solo comando.

**Nota:** Impostare in modo corretto `/dev/sdx1` prima di procedere o l'operazione non andrà a buon fine.

```
$ sed -i "s|label=ARCH_.*|device=/dev/disk/by-uuid/$(blkid -o value -s UUID /dev/sdx1)|" archiso_sys{32,64}.cfg

```

Se si ha sul proprio sistema *syslinux<4.06* un workaround per EXT2 (inutile per EXT4) è modificare la riga `APPEND` del file `syslinux.cfg` così:

```
$ sed -i "s|../../|/arch|" syslinux.cfg

```

#### UNetbootin (Metodo sconsigliato)

**Attenzione:** Usare UNetBootIn è FORTEMENTE SCONSIGLIATO. Tale programma infatti sovrascrive il file `syslinux.cfg` creando problemi al boot.

[UNetbootin](http://unetbootin.sourceforge.net/) è un software multipiattaforma il cui scopo è facilitare la creazione di dispositivi USB avviabili; funziona con moltissime distribuzioni GNU/Linux.

Se si sta usando UNetbootin e si ha il classico [*30 seconds error*](https://bbs.archlinux.org/viewtopic.php?id=127031), sarà necessario editare il file `syslinux.cfg` creato da UNetbootin sulla partizione *root* del dispositivo USB. Aggiungere `archisolabel=*LABEL*` alla fine della riga `append`, dove `*LABEL*` dovrà essere il nome del dispositivo USB, impostato al momento della formattazione. Supponendo che il nome del dispositivo sia "USB_DRIVE", il proprio file `syslinux.cfg` dovrebbe essere così:

```
 default menu.c32
 prompt 0
 menu title UNetbootin
 timeout 100

 label unetbootindefault
 menu label Default
 kernel /ubnkern
 append initrd=/ubninit ../../ archisolabel=USB_DRIVE

```

UNetbootin crea un secondo menu item chiamato `loadconfig` che è possibile rimuovere semplicemente cancellando le relative linee in `syslinux.cfg`.

## Su Mac OS X

Su un sistema MAC, per poter utilizzare il comando dd sul dispositivo USB, è necessario fare alcune operazioni speciali. Prima di tutto occorre inserire il dispositivo, che verrà automaticamente montato dal sistema operativo, ed eseguire:

```
diskutil list

```

in Terminal.app. Successivamente bisogna capire come viene indicato il dispositivo USB - ad esempio /dev/disk1\. (Usare semplicemente il comando `mount` o `sudo dmesg | tail`.) Ora eseguire:

```
diskutil unmountDisk /dev/disk1

```

per smontare la partizione sul dispositivo (ad esempio, /dev/disk1s1) lasciando intatta quella corretta (ad esempio, /dev/disk1). Ora si può continuare seguendo le istruzioni per Linux riportate sopra (ma usando bs=8192 nel caso si utilizzi `dd` di OS X, il numero si ottiene da 1024*8).

```
 dd if=image.iso of=/dev/disk1 bs=8192
 20480+0 records in
 20480+0 records out
 167772160 bytes transferred in 220.016918 secs (762542 bytes/sec)

```

espellere il supporto prima di rimuoverlo fisicamente con:

```
 diskutil eject /dev/disk1

```

## Su Windows

### Image Writer per Windows

Scaricare win32 disk imager da [http://sourceforge.net/projects/win32diskimager/](http://sourceforge.net/projects/win32diskimager/). Eseguire il programma. Selezionare il file immagine di Arch ed il dispositivo USB. Win32 Disk Imager individua i file immagine con estensione *.img*, perciò se si ha un'immagine *.iso*, occorrerà rinominarla manualmente; la modifica è solo "estetica", per cui la scrittura sarà eseguita regolarmente. Cliccare sul tasto "Scrivi". Ora si dovrebbe essere in grado di eseguire il boot dal dispositivo USB ed installare Arch.

### USBWriter per Windows

Scaricare il programma da [http://sourceforge.net/projects/usbwriter/](http://sourceforge.net/projects/usbwriter/) e lanciarlo. Selezionare l'immagine *.iso di Arch, il supporto usb scelto e premere il pulsante `write`. Ora, a processo ultimato, si dovrebbe essere in grado di effettuare il boot con questo supporto usb e installare Arch Linux.

### Rufus per Windows

[rufus](http://rufus.akeo.ie/?locale=it_IT) è una utility dotata di interfaccia grafica che permette di creare immagini usb di svariate distribuzioni linux. A differenza di altri programmi non sono necessarie modifiche ai file o al bootloader, e il Live CD parte senza nessun problema. Per far partire l'installazione selezionare il supporto usb e cliccare sull'immagine del CD vicino alla scritta "Immagine ISO" in basso, e selezionare l'immagine .iso di Arch Linux, poi cliccare su Avvia. Durante l'installazione viene richiesto il download di Syslinux 6\. Dare l'ok per procedere con l'installazione.

### Metodo Flashnul

[flashnul](http://shounen.ru/soft/flashnul/) è una utility che permette di verificare il funzionamento delle memorie Flash (USB-Flash, IDE-Flash, SecureDigital, MMC, MemoryStick, SmartMedia, XD, CompactFlash ecc).

Dal prompt dei comandi eseguire `flashnul` con `-p`, per determinare l'indice del dispositivo USB. Per esempio, si otterrà una cosa simile a questa:

```
C:\>flashnul -p

Avaible physical drives:
Avaible logical disks:
C:\
D:\
E:\

```

In questo caso il dispositivo è indicato con E:

Una volta individuato il dispositivo corretto si può scrivere l'immagine sul disco, eseguendo il comando `flashnul` seguito dall'indice del dispositivo, da `-L` e dal percorso dell'immagine. Nel caso precedente, sarà:

```
C:\>flashnul E: -L percorso\della\arch.iso

```

Quando si è sicuri di voler procedere con la scrittura, digitare "yes", ed attendere il termine del processo di scrittura. Nel caso si ottenga un errore di accesso negato, chiudere qualsiasi finestra d'Explorer aperta.

Nel caso si utilizzi Vista o Win7, sarà necessario aprire la console da amministratore, altrimenti flashnul non riuscirà ad accedere al dispositivo e si sarà abilitati a scrivere solo attraverso il gestore dischi fornito da Windows

**Nota:** è necessario usare le lettere del dispositivo al posto dei numeri. flashnul 1rc1, Windows 7 x64\. -bgalakazam

### Metodo Cygwin

Assicurarsi che l'installazione di [Cygwin](http://www.cygwin.com/) contenga il pacchetto dd. Oppure, se non si vuole installare Cygwin, si può semplicemente scaricare dd per Windows da [http://www.chrysocome.net/dd](http://www.chrysocome.net/dd).

Posizionare il file immagine nella home, ad esempio:

```
C:\cygwin\home\John\

```

Eseguire cygwin come amministratore (richiesto da cygwin per accedere all'hardware). Per scrivere sul dispositivo USB utilizzare il seguente comando:

```
dd if=image.iso of=\\.\[x]:

```

dove `image.iso` è il percorso dell'immagine ISO inserito nella cartella cygwin e \\.\[x]: è il dispositivo USB, dove x è la lettera ad esso assegnata, ad esempio "\\.\d:".

Con cygwin 6.0 la partizione corretta si trova con

```
cat /proc/partitions

```

quindi scrivere l'immagine ISO con le informazioni ricevute nell'output del comando precedente. Ad esempio:

**Attenzione:** Il comando distruggerà definitivamente tutti i dati presenti sul supporto USB, perciò assicurarsi che non siano presenti dati importanti su quest'ultimo prima di procedere.

```
dd if=image.iso of=/dev/sdb

```

### dd per Windows

Una versione con licenza GPL di *dd* per Windows è disponibile [qui](http://www.chrysocome.net/dd). Il vantaggio rispetto a Cygwin è semplicemente che il download risulta essere più leggero. È possibile usare le istruzioni di Cygwin del paragrafo precedente.

### Avviare l'intera ISO dalla memoria RAM

Questo metodo usa [Syslinux](/index.php/Syslinux "Syslinux") e [MEMDISK](http://www.syslinux.org/wiki/index.php/MEMDISK#ISO_images) per caricare tutta l'immagine ISO in RAM, quindi accertarsi di avere ram a sufficienza. A processo ultimato si vedrà il menu grafico e il supporto USB può essere rimosso ed essere usato anche su un pc diverso per riavviare lo stesso processo. Questo permette di installare Arch da (e su) la stessa chiavetta.

**1.** Formattare il supporto USB in FAT32 e creare le seguenti directories:

```
X:\Boot
X:\Boot\ISOs
X:\Boot\Settings 

```

**2.** Copiare l'immagine ISO desiderata nella cartella ISOs (Ad esempio: *archlinux-2013.04.01-dual.iso*) e da **[qui](http://www.kernel.org/pub/linux/utils/boot/syslinux/)** la versione più recente si *syslinux* e copiare:

*   `./win32/syslinux.exe` sul desktop, o dove si vuole.
*   `./memdisk/memdisk` nella cartella "Settings" e, nel mentre, creare il file `syslinux.cfg` che contenga:

 `X:\Boot\Settings\syslinux.cfg` 
```
DEFAULT arch_iso

  LABEL arch_iso
    MENU LABEL Arch Linux Setup
    LINUX memdisk
    INITRD /Boot/ISOs/archlinux-2013.04.01-dual.iso
    APPEND iso
```

**Tip:** Se si vuole aggiungere un'altra distribuzione *(Debian e Parted Magic sono state testate)* è possibile farlo editando il presente file. Vedere la pagina [Syslinux](/index.php/Syslinux_(Italiano) "Syslinux (Italiano)") per maggiori dettagli.

**3.** Creare un file `*.bat` nella stessa directory di *syslinux.exe* e lanciare:

 `C:\Documents and Settings\username\Desktop\install.bat` 
```
@echo off
 syslinux.exe -m -a -d /Boot/Settings X:
```

Fatto!

## Risoluzione problemi

**Nota:** Con il metodo MEMDISK, se si ottiene il classico errore **30 seconds error** (specialmente con la versione i686), premere `Tab` sulla voce `Boot Arch Linux (i686)` e aggiungere `vmalloc=256M` alla fine per immagini netinstall e `vmalloc=448M` per immagini core. Questo è da applicare solo al metodo MEMDISK. Per riferimento: *Se l'immagine è più grossa di 128MiB e si ha un OS a 32-bit, è necessario incrementare la memoria di vmalloc*. [(*)](http://www.syslinux.org/wiki/index.php/MEMDISK#-_memdiskfind_in_combination_with_phram_and_mtdblock)

**Nota:**

## Vedere Anche

*   [Gentoo liveusb document](http://www.gentoo.org/doc/en/liveusb.xml)