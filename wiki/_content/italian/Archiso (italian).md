**Archiso** è un piccolo set di script bash capace di creare **immagini live CD/DVD e USB basate su Arch Linux**. È uno strumento molto generico, dunque potenzialmente potrebbe essere usato per generare qualsiasi cosa da sistemi di salvataggio, a dischi di installazione, ad interessanti sistemi live CD/DVD/USB speciali e chissà cos'altro. Il cuore e l'anima di Archiso è **mkarchiso**. Tutte le sue opzioni sono documentate nell'output di utilizzo, quindi il suo diretto utilizzo non verrà trattato qui. Questo articolo, invece, vuole essere una guida per creare i propri live media. In seguito a recenti modifiche, adesso **Archiso** creerà automaticamente immagini ISO utilizzabili anche come immagini USB!

**Nota:** Ci sono due metodi per creare il live media in base alle tue intenzioni.

Se vuoi creare un versione live di Arch Linux completamente personalizzata, pre-installata con tutti i tuoi programmi e configurazioni preferiti, vai alla sezione 1.

Se vuoi soltanto creare un live media base, senza pacchetti pacchetti pre-installati e con configurazioni minimali, allora passa alla sezione 2.

## Contents

*   [1 Creare un live media di Arch Linux Personalizzato. (configs/relengs)](#Creare_un_live_media_di_Arch_Linux_Personalizzato._(configs/relengs))
*   [2 Creare il live media di Arch Linux base. (configs/baseline)](#Creare_il_live_media_di_Arch_Linux_base._(configs/baseline))
*   [3 Flusso di lavoro generale (metodo manuale)](#Flusso_di_lavoro_generale_(metodo_manuale))
*   [4 Creare una "pendrive" avviabile che ha più cose di "Arch Linux"](#Creare_una_"pendrive"_avviabile_che_ha_più_cose_di_"Arch_Linux")
*   [5 Configurare il live media](#Configurare_il_live_media)
    *   [5.1 Installare i pacchetti](#Installare_i_pacchetti)
    *   [5.2 Aggiungere un utente](#Aggiungere_un_utente)
    *   [5.3 Popolare la cartella /home dell'utente](#Popolare_la_cartella_/home_dell'utente)
    *   [5.4 mkinitcpio.conf](#mkinitcpio.conf)
    *   [5.5 aitab](#aitab)
    *   [5.6 Boot Loader](#Boot_Loader)
    *   [5.7 Finire la root-image](#Finire_la_root-image)
*   [6 Vedi anche](#Vedi_anche)

## Creare un live media di Arch Linux Personalizzato. (configs/relengs)

*   Alcuni pacchetti sono necessari prima di procedere, installa quindi devtools. Servirà anche git se scegli di installare gli script archiso dal repository git (consigliato) e non da AUR.

```
[host] # pacman -S devtools git --needed

```

*   Crea un ambiente chroot in cui lavorare e installa i pacchetti base in questo chroot

```
[host] # mkarchroot /home/nomeutente/archlive base

```

*   Scarica adesso gli script archiso ed installali nel chroot.

```
[host] # git clone [git://projects.archlinux.org/archiso.git](git://projects.archlinux.org/archiso.git)
[host] # make -C archiso/archiso DESTDIR=/home/nomeutente/archlive install

```

Puoi anche installare archiso da AUR, [qui](https://aur.archlinux.org/packages.php?ID=25996), ma si consiglia il metodo precedente da git.

*   Entra nell'ambiente chroot appena creato

```
[host] # mkarchroot -r bash /home/nomeutente/archlive

```

*   Crea un device node. Nota: Devi fare questo **ogni volta** entri nel chroot.

```
[chroot] # mknod /dev/loop0 b 7 0

```

*   Configura un mirror con il seguente comando, o decommenta quello che preferisci all'interno di /etc/pacman.d/mirrorlist

**Nota:** Sostituisci MIRROR secondo le tue preferenza

```
[chroot] # echo 'Server = MIRROR/archlinux/$repo/os/$arch' >> /etc/pacman.d/mirrorlist

```

*   Adesso siamo all'interno del chroot, installiamo alcuni pacchetti.

```
[chroot] # pacman -S devtools libisoburn squashfs-tools

```

*   Copia gli script archiso installati prima, in una posizione da cui possiamo lavorare, come /tmp.

Tutte le modifiche che faremo all'immagine live verranno effettuate all'interno della cartella /tmp dentro chroot.

```
[chroot] # cp -r /usr/share/archiso/configs/releng/ /tmp

```

*   CD in questa cartella:

```
[chroot] cd /tmp/releng

```

adesso passa a [#Configurare il live media](#Configurare_il_live_media).

## Creare il live media di Arch Linux base. (configs/baseline)

Segui tutte le istruzione qui sopra; tuttavia, invece di copiare /usr/share/archiso/configs/releng nella cartella in cui lavorare, usa /usr/share/archiso/configs/baseline:

```
[chroot] # cp -r /usr/share/archiso/configs/baseline /tmp

```

*   Ora puoi costruire l'immagine, che originerà un file iso in /tmp/out (o in qualsiasi cartella da cui stai lavorando), che può essere scritta su CD o copiata con dd su USB.

```
[chroot] # ./build.sh -v

```

*   Esci da chroot.

```
[chroot] # exit

```

## Flusso di lavoro generale (metodo manuale)

*   Configura un filesystem base

```
mkarchiso -p "base" create

```

*   Installa syslinux

```
mkarchiso -p "syslinux" create

```

*   Installa altri pacchetti (opzionale)

```
mkarchiso -p "pkg1 pkg2 pkg3 ... pkgN" create

```

*   A questo punto, personalizza quello che vuoi in root-image, quindi esci appena hai finito.

```
mkarchroot -n -r bash work/root-image

```

*   Configura l'immagine initramfs.

*   *   Copia gli hook necessari in root-image.

```
cp /lib/initcpio/hooks/archiso work/root-image/lib/initcpio/hooks
cp /lib/initcpio/install/archiso work/root-image/lib/initcpio/install

```

*   *   Crea un config per mkinitcpio **work/root-image/etc/mkinitcpio-archiso.conf**.

```
HOOKS="base udev archiso sata filesystems"
COMPRESSION="xz"

```

*   *   Crea una cartella col nome dell'architettura del tuo PC:

```
mkdir work/root-image/boot/i686

```

*   *   e genera l'immagine initramfs

```
mkarchroot -n -r "mkinitcpio -c /etc/mkinitcpio-archiso.conf -k /boot/vmlinuz-linux -g /boot/i686/archiso.img" work/root-image

```

*   Sposta kernel/initramfs in boot/

```
mkdir -p work/iso/arch/boot/i686
mv work/root-image/boot/vmlinuz-linux work/iso/arch/boot/i686/vmlinuz
mv work/root-image/boot/i686/archiso.img work/iso/arch/boot/i686/archiso.img

```

*   Configura syslinux

*   *   Crea una cartella.

```
 mkdir -p work/iso/arch/boot/syslinux

```

*   *   Crea un file **work/iso/arch/boot/syslinux/syslinux.cfg**.

```
DEFAULT menu.c32
PROMPT 0
MENU TITLE Arch Linux
TIMEOUT 300

LABEL arch
MENU LABEL Arch Linux
LINUX /arch/boot/i686/vmlinuz
INITRD /arch/boot/i686/archiso.img
APPEND archisolabel=MY_ARCH

ONTIMEOUT arch

```

*   *   Copia menu.c32.

```
cp work/root-image/usr/lib/syslinux/menu.c32 work/iso/arch/boot/syslinux/

```

*   Configura isolinux (opzionale, necessario solo per le iso avviabili)

```
mkdir work/iso/isolinux
cp work/root-image/usr/lib/syslinux/isolinux.bin work/iso/isolinux/
cp work/root-image/usr/lib/syslinux/isohdpfx.bin work/iso/isolinux/

```

*   *   Crea **work/iso/isolinux/isolinux.cfg**

```
DEFAULT loadconfig

LABEL loadconfig
  CONFIG /arch/boot/syslinux/syslinux.cfg
  APPEND /arch/boot/syslinux/

```

*   Crea il file **work/iso/arch/aitab**.

```
# <img>         <mnt>                 <arch>   <sfs_comp>  <fs_type>  <fs_size>
root-image      /                     i686     xz          ext4       50%

```

*   Crea tutte le immagini del filesystem specificate in aitab (.fs .fs.sfs .sfs)

```
mkarchiso prepare

```

*   Genera un ISO 9660 con l'immagine d'avvio "El Torito" (opzionale)

```
mkarchiso -L "MY_ARCH" iso "my-arch.iso"

```

## Creare una "pendrive" avviabile che ha più cose di "Arch Linux"

Installa il codice del settore di master boot.

```
dd bs=440 count=1 conv=notrunc if=/usr/lib/syslinux/mbr.bin of=/dev/pen

```

Configura un'etichetta del filesystem (per ext2/3/4)

```
e2label /dev/pen1 MY_ARCH

```

Configura un'etichetta del filesystem (per vfat)

```
dosfslabel /dev/pen1 MY_ARCH

```

Monta e copia la cartella "work/iso/arch"

```
mount /dev/pen1 /mnt/pen1
cp -r work/iso/arch /mnt/pen1

```

Installa extlinux e smontala (la partizione deve essere segnata come avviabile)

```
extlinux -i /mnt/pen1/arch/boot/syslinux
umount /mnt/pen1

```

## Configurare il live media

Dentro l'ambiente chroot e dentro la cartella da cui lavori (/tmp se hai seguito questa guida), vedrai diverse cartelle chiamate root-image; dovrebbero interessare solo alcuni di questi file ed in particolare la cartella root-image; questa cartella farà da overlay ed è dove farai ogni personalizzazione.

### Installare i pacchetti

Vorrai anche creare una lista di pacchetti che vuoi installare sul tuo live CD. Un file pieno di nomi di pacchetti, uno per riga, è il formato per fare questo. Questo è ***grandioso*** per live CD di particolare interesse, dovrai solo specificare i pacchetti che vuoi e scrivere l'immagine. Modifica il file packages.i686 o packages.x86_64 per creare un'immagine, rispettivamente, a 32bit o a 64bit.

**Suggerimento:** Puoi anche creare un **[custom local repository](/index.php/Custom_local_repository "Custom local repository")** allo scopo di preparare pacchetti personalizzati o pacchetti da [AUR](/index.php/AUR "AUR")/[ABS](/index.php/ABS "ABS"). Aggiungi il tuo repository locale alla prima posizione (per la massima priorità) del file **/etc/pacman.conf** in chroot.

### Aggiungere un utente

Ci sono due metodi per creare un utente: attraverso il comando useradd o anche sovrascrivendo /etc/shadow, /etc/passwd e /etc/group. Quest'ultimo metodo è mostrato di seguito.

Copia i tuoi /etc/shadow, /etc/passwd e /etc/group dal tuo sistema **host** a /etc/ all'interno del sistema **chroot**. Esempio

```
[host] $ cp /etc/{shadow,passwd,group} /home/nomeutente/archlive/tmp/root-image/etc/

```

**Attenzione:** Il file passwd contiene le password criptate. Si raccomanda, prima di copiare il file, di cambiare la password del proprio utente host in quella che dovrà avere l'utente live, copiare il file passwd, quindi ripristinare la propria password.

### Popolare la cartella /home dell'utente

Crea la cartella skel all'interno di root-image, copia i file che desideri dalla tua cartella /home ed aggiungi i relativi comandi in rc.local, in questo modo:

*   Crea la cartella skel:

```
[chroot] cd root-image/etc/ && mkdir skel

```

*   Copia i tuoi file da /home/nomeutente:

esempio per .bashrc

```
[host] # cp ~/.bashrc /home/nomeutente/archlive/tmp/root-image/etc/skel/

```

**Nota:** Dovrai fare questo da root, non è possibile cambiare il proprietario dei file da copiare in quanto tutto all'interno della cartella root-image dovrà appartenere all'utente root

*   Dentro la cartella root-image/etc, crea il file rc.local e **assicurati** di renderlo eseguibile:

```
[chroot] # cd root-image/etc/
[chroot] # touch rc.local && chmod +x rc.local

```

*   Adesso modificalo aggiungendo:

```
# Create user directory for live session
if [ ! -d /home/**nomeutente** ]; then
    mkdir /home/**nomeutente** && chown **nomeutente** /home/**nomeutente**
fi
# Copy files over to home
su -c "cp -r /etc/skel/.[a-zA-Z0-9]* /home/**nomeutente**/" **nomeutente**

```

### mkinitcpio.conf

Un *initcpio* è essenziale per creare un sistema che possa avviarsi da CD/DVD/USB, il file predefinito dovrebbe funzionare bene, quindi non dovresti aver bisogno di toccarlo.

Dovrai dunque creare un mkinitcpio.conf che contenga una lista dei tuoi hook:

```
$ vim mkinitcpio.conf

```

Un tipico set di hook per archiso dovrebbe somigliare a questo:

```
HOOKS="base udev memdisk archiso archiso_pxe_nbd archiso_loop_mnt pata scsi sata usb fw pcmcia filesystems usbinput"

```

Questa lista ti permetterà di avere un sistema che può essere avviato da un dispositivo CD/DVD o USB. Ovviamente auto-rilevamento dell'hardware ed altre cose della stessa natura non sono presenti. Solo il necessario a mettere in piedi il sistema e, a parte l'*initcpio*, il resto potrà comunque essere fatto a sistema avviato.

### aitab

Il file aitab contiene informazioni relative alle immagini del filesystem che devono essere create da mkarchiso e montate dall'hook archiso in fase initramfs. Il file di default dovrebbe andar bene e non dovrebbe necessitare di modifiche. Consiste in alcuni campi che definiscono il comportamento delle immagini.

```
# <img>         <mnt>                 <arch>   <sfs_comp>  <fs_type>  <fs_size>

```

	<img>

	Nome dell'immagine senza estensione (.fs .fs.sfs .sfs).

	<mnt>

	Punto di mount.

	<arch>

	Architettura { i686 | x86_64 | any }.

	<sfs_comp>

	compressione SquashFS { gzip | lzo | xz }. Il valore speciale "none" disabilita SquashFS.

	<fs_type>

	Imposta il tipo di filesystem dell'immagine { ext4 | ext3 | ext2 | xfs }. Il valore speciale "none" disabilita l'uso di un filesystem. In questo caso tutti i file sono spostati direttamente al filesystem SquashFS.

	<fs_size>

	Un valore assoluto della grandezza in MiB dell'immagine del file system (esempio: 100, 1000, 4096, etc), un valore relativo dello spazio libero nel file system [in percentuale] {1%..99%} (example 50%, 10%, 7%).

**Nota:** Alcune combinazioni non sono valide. Ad esempio sia sfs_comp che fs_type sono impostate a none

### Boot Loader

Il file presente dovrebbe adattarsi alle tue esigenze.

```
DEFAULT menu.c32
PROMPT 0
MENU TITLE Arch Linux
TIMEOUT 300

LABEL arch
MENU LABEL Arch Linux
LINUX /%INSTALL_DIR%/boot/%ARCH%/vmlinuz
INITRD /%INSTALL_DIR%/boot/%ARCH%/archiso.img
APPEND archisobasedir=%INSTALL_DIR% archisolabel=%ARCHISO_LABEL%

ONTIMEOUT arch

```

Data la natura modulare di isolinux, puoi usare diversi addon dal momento che tutti i file *.c32 sono copiati e disponibili. Dai uno sguardo al [sito ufficiale di syslinux](http://syslinux.zytor.com/wiki/index.php/SYSLINUX) e al [git repo di archiso](https://projects.archlinux.org/archiso.git/tree/configs/syslinux-iso/boot-files). Usando i suddetti addon è possibile rendere i menu visivamente gradevoli e complessi. Vedi [qui](http://syslinux.zytor.com/wiki/index.php/Comboot/menu.c32).

### Finire la root-image

Alcuni consigli che non saranno affrontati in quest'articolo perchè ci sono già altri articoli su questa wiki che lo fanno, ma sentiti pure libero di aggiungerne altri qui.

*   Configurare *inittab* per far partire X all'avvio
*   Configurare il fiel *hosts*
*   Configurare *rc.conf* (non sono richiesti moduli particolari)
*   Configurare *sudoers*
*   Configurare *rc.local*
*   Mettere artwork aggiuntivi sul media
*   Mettere altri file binari in opt/

## Vedi anche

*   [Pagina del progetto Archiso](https://projects.archlinux.org/?p=archiso.git;a=summary)
*   [Archiso come server pxe](/index.php/Archiso_as_pxe_server "Archiso as pxe server")
*   [Guida passo-a-passo per usare ArchISO](https://kroweer.wordpress.com/2011/09/07/creating-a-custom-arch-linux-live-usb)
*   [Una distribuzione live DJ basata su ArchLinux e creata con Archiso](http://didjix.blogspot.com/)