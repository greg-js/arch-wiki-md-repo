Questa guida è destinata a integrare ed aggiornare le tre guide di installazione alternativa già esistenti su questo wiki. È destinata a chiunque voglia installare Arch Linux da qualsiasi altro sistema Linux in esecuzione, al di fuori di un LiveCD o un'installazione pre-esistente di una distribuzione diversa.

## Contents

*   [1 Generale](#Generale)
*   [2 Setup del sistema host](#Setup_del_sistema_host)
    *   [2.1 Ottenere i pacchetti necessari](#Ottenere_i_pacchetti_necessari)
        *   [2.1.1 Introduzione](#Introduzione)
        *   [2.1.2 Scarica i binari di pacman e le librerie condivise](#Scarica_i_binari_di_pacman_e_le_librerie_condivise)
        *   [2.1.3 Installare pacman nel sistema host](#Installare_pacman_nel_sistema_host)
    *   [2.2 Configurare il sistema host](#Configurare_il_sistema_host)
*   [3 Installazione del sistema di destinazione](#Installazione_del_sistema_di_destinazione)
    *   [3.1 Preparare una partizione per Arch](#Preparare_una_partizione_per_Arch)
    *   [3.2 Installare il core](#Installare_il_core)
    *   [3.3 Preparare i /dev nodes](#Preparare_i_.2Fdev_nodes)
    *   [3.4 Chroot](#Chroot)
    *   [3.5 Installare il resto](#Installare_il_resto)
    *   [3.6 Configurare il sistema di destinazione](#Configurare_il_sistema_di_destinazione)
    *   [3.7 Installazione di grub](#Installazione_di_grub)
        *   [3.7.1 Ripristino manuale di GRUB libs](#Ripristino_manuale_di_GRUB_libs)
    *   [3.8 Ritocchi finali](#Ritocchi_finali)
*   [4 Un terzo (e più semplice) metodo](#Un_terzo_.28e_pi.C3.B9_semplice.29_metodo)
*   [5 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [5.1 Kernel Panic](#Kernel_Panic)
    *   [5.2 Il dispositivo root "/dev/sd??" non esiste](#Il_dispositivo_root_.22.2Fdev.2Fsd.3F.3F.22_non_esiste)
*   [6 Un metodo alternativo: Installazione da un sistema Linux esistente con l'immagine di Arch](#Un_metodo_alternativo:_Installazione_da_un_sistema_Linux_esistente_con_l.27immagine_di_Arch)
    *   [6.1 Preparare l'ambiente di installazione](#Preparare_l.27ambiente_di_installazione)
    *   [6.2 Installare dal nuovo ambiente](#Installare_dal_nuovo_ambiente)
    *   [6.3 Aggiornamento e installazione dei pacchetti dal sistema host via chroot](#Aggiornamento_e_installazione_dei_pacchetti_dal_sistema_host_via_chroot)

## Generale

[Pacman](/index.php/Pacman "Pacman") può essere configurato con l'opzione (-r) per operare in una qualsiasi directory, usandola come contesto di "root" durante l'esecuzione.

Ciò è utile per creare un nuovo sistema Arch Linux dal disco live di un'altra distro o da un'installazione esistente. È altresì utile per creare nuovi ambienti chroot in un sistema "host", mantenendo una "golden-master" per lo sviluppo e la distribuzione, o altri divertenti motivi come rootfs-over-NFS per macchine senza disco.

In questa guida il requisito necessario è che il sistema host esistente sia in grado di eseguire i programmi con l'architettura del target Arch Linux. Nel caso di un host x86_64, è comunque possibile usare un pacman i686 per creare un ambiente chroot a 32bit. Consultare [Arch64 Install bundled 32bit system](/index.php/Arch64_Install_bundled_32bit_system "Arch64 Install bundled 32bit system"). Tuttavia non è così facile compilare un ambiente a 64 bit quando l'host supporta in esecuzione solo programmi a 32 bit.

In questa guida inoltre, ci si riferisce a partizioni come /dev/hdxx o /dev/sdxx, ossia ad una qualunque dev si abbia nel proprio sistema per la partizione in questione. La convenzione è:

```
Drive 1, Partition 1:  /dev/hda1 o /dev/sda1
Drive 1, Partition 2:  /dev/hda2 o /dev/sda2
Drive 2, Partition 1:  /dev/hdb1 o /dev/sdb1

```

ecc...

In genere verrà utilizzata /dev/sdxx , ma si faccia attenzione che sul proprio sistema quella voce potrebbe essere /dev/hdxx.

In questo articolo,

	host

	si riferisce al computer che è usato per creare l'installazione.

	target

	è il computer dove si vuole installare Arch.

Questi potrebbero essere lo stesso computer. Non è necessario che l'host sia una distribuzione Arch, potrebbe essere Debian o un sistema Redhat. La sezione inititolata "Setup del sistema host" spiega come installare pacman nell'host. La sezione seguente intitolata "Setup del sistema target" spiega come usare pacman dal sistema host per installare Arch Linux nel computer target. Quindi se il proprio sistema è già Arch Linux, si può procedere alla sezione "Setup del sistema target".

## Setup del sistema host

È necessario installare il pacchetto pacman di Archlinux nel proprio ambiente linux (host).Inoltre si dovrà recuperare la lista dei mirrors site [[1]](https://www.archlinux.org/mirrorlist/) che pacman utilizzerà per scaricare i pacchetti del sistema. Se sei già utilizzando Arch, saltare questo passaggio e andare a [Install from Existing Linux (Italiano)#Installazione del sistema di destinazione](/index.php/Install_from_Existing_Linux_(Italiano)#Installazione_del_sistema_di_destinazione "Install from Existing Linux (Italiano)")

### Ottenere i pacchetti necessari

#### Introduzione

Si devono recuperare i pacchetti richiesti dal proprio ambiente linux ospitante. Nell'esempio si presuppone si stia usando un ambiente i686\. **Se si sta utilizzando un sistema linux a 64bit si dovrà cambiare a ogni evenienza "i686" con "x86_64".**

Tutte i numeri di versione utilizzati qui possono essere cambiati. Si prega di controllare i numeri di versione in principio e annotarli. I numeri della versione possono essere trovati:

*   pacman [32 bit](https://www.archlinux.org/packages/core/i686/pacman/) e [64 bit](https://www.archlinux.org/packages/core/x86_64/pacman/),
*   pacman-mirrolist per [tutte](https://www.archlinux.org/packages/core/any/pacman-mirrorlist/) le architetture.

Una volta certi dei numeri di versione, si scarichino i pacchetti richiesti (cambiare il valore di ARCH a seconda delle proprie esigenze):

```
ARCH=i686
base_chroot=/tmp
mkdir ${base_chroot}/archlinux
cd ${base_chroot}/archlinux

```

#### Scarica i binari di pacman e le librerie condivise

Ora si scarichino i pacchetti richiesti per installare [pacman](/index.php/Pacman "Pacman"), per essere poi in grado di aggiungere altro software alla nuova directory di base:

```
wget [https://www.archlinux.org/packages/core/$ARCH/pacman/download/](https://www.archlinux.org/packages/core/$ARCH/pacman/download/) --no-check-certificate
wget [https://www.archlinux.org/packages/core/any/pacman-mirrorlist/download/](https://www.archlinux.org/packages/core/any/pacman-mirrorlist/download/) --no-check-certificate

```

Note: Se wget non riesce a recuperare i nomi dei file correttamente, riprovare wget con --trust-server-names. Suggerimento: è possibile usare un alias:

```
alias wget='wget --trust-server-names'

```

Permette di scaricare i file con i nomi proposti dal server. Si veda la [man page](http://pwet.fr/man/linux/commandes/wget) e il [manuale ufficiale](http://www.gnu.org/software/wget/manual/wget.html) di wget per ulteriori approfondimenti.

Note: In caso di problemi con lo scaricamento di **pacman-mirrorlist** riprovare con questo modo più diretto con lftp:

```
link_name=[http://mirrors.kernel.org/archlinux/core/os/x86_64/](http://mirrors.kernel.org/archlinux/core/os/x86_64/)
lftp -e "mget pacman-mirrorlist-*.tar.gz" "${link_name}"

```

o in questo modo diretto (prestare attenzione alla stringa "data" nel nome del file) :

```
wget [http://mirrors.kernel.org/archlinux/core/os/x86_64/pacman-mirrorlist-20110703-1-any.pkg.tar.gz](http://mirrors.kernel.org/archlinux/core/os/x86_64/pacman-mirrorlist-20110703-1-any.pkg.tar.gz)

```

Potrebbero essere necessarie ulteriori librerie aggiuntive per far funzionare pacman:

```
for software_name in libfetch libarchive openssl xz expat ; do wget [https://www.archlinux.org/packages/core/$ARCH/${software_name}/download/](https://www.archlinux.org/packages/core/$ARCH/${software_name}/download/) ; done

```

Spacchettare tutti i pacchetti necessari:

```
for f in *.tar.gz ; do tar xzvf $f ; done

```

Prima di usare pacman, ricordarsi di modificare `/tmp/archlinux/etc/pacman.conf` in modo da puntare a `/tmp/archlinux/etc/pacman.d/mirrorlist` e selezionare il proprio mirror prescelto. Per facilitare le cose (presupponendo si stia utilizzando `bash` o `zsh`), si può configurare l'ambiente in tal modo

```
export PATH=${base_chroot}/archlinux/usr/bin:$PATH
export LD_LIBRARY_PATH=${base_chroot}/archlinux/usr/lib:$LD_LIBRARY_PATH
alias pacman="pacman --config ${base_chroot}/archlinux/etc/pacman.conf"

```

#### Installare pacman nel sistema host

Se non vi importa mettere in disordine il proprio sistema host, si possono estrarre tutti i tarball scaricati nella propria directory root dando da root questi comandi:

```
cd /
for f in /tmp/archlinux/pacman-*pkg.tar.gz ; do
  tar xzf $f
done

```

Tuttavia, tenere presente che questa operazione potrebbe cancellare alcuni file, e danneggiare il sistema.

1.  Se si sta installando da Ubuntu 9.10 LiveCD (o forse anche da altre versioni), saranno necessari non solo i file di pacman (shared libs) per usarlo. Usare lo script di Lucky descritto in [[questo thread](https://bbs.archlinux.org/viewtopic.php?pid=759166)] per scaricarli!

2.  n alternativa, si possono trasformare questi archivi in pacchetti per la propria distribuzione con il tool [alien](http://kitenet.net/~joey/code/alien/). Vedere la man page dello strumento per le istruzioni. I pacchetti creati in questo modo possono essere installati nella distribuzione host utilizzando i soliti strumenti di gestione dei pacchetti disponibili. Questo approccio offre una migliore integrazione nell'ambiente Linux host. Per un sistema basato pacchetto debian questo è fatto con i seguenti comandi:

    ```
    cd /tmp/archlinux
    alien -d pacman-3.3.3-1-i686.pkg.tar.gz
    alien -d pacman-mirrorlist-20101223-1-any.pkg.tar.gz

    ```

    Per i sistemi basati su RPM sarà necessario sostituire il parametro "-d" con "-r".

    Questi pacchetti possono quindi venire installati usando il normale gestore pacchetti dell'ambiente Linux host.

3.  Con Fedora 12, non è stato possibile installare pacman con uno qualsiasi degli altri metodi. Ma con l'ottimo script su [https://bbs.archlinux.org/viewtopic.php?pid=734336#p734336](https://bbs.archlinux.org/viewtopic.php?pid=734336#p734336), verrà scaricato e installato.

4.  Con [Gentoo](http://gentoo.org/): basta "smascherare" pacman aggiungendo <tt>sys-apps/pacman</tt> a <tt>/etc/portage/package.keywords</tt>. Ora basta eseguire <tt>emerge -av pacman</tt>.

    C'è anche una [guida ben dettagliata](http://ohnopub.net/~ohnobinki/gentoo/arch/).

5.  Un metodo più vecchio è [discusso qui](/index.php?title=Quick_Custom_Installation&action=edit&redlink=1 "Quick Custom Installation (page does not exist)").

### Configurare il sistema host

L'obiettivo principale di questa operazione è di fare una corretta configurazione di pacman.

Configurare il file /etc/pacman.conf a proprio gradimento, e rimuovere i mirror non necessari dal file /etc/pacman.d/mirrorlist. Abilitare inoltre come minimo un paio di mirror, necessari per non incorrere in errori, dovuti alla loro mancanza, durante la sincronizzazione. Si consiglia di risolvere manualmente i DNS nel file /etc/pacman.d/mirrorlist, dato che pacman per i686 potrebbe non trovare le informazioni degli indirizzi su sistemi x86_64.

Se si sta installando da un LiveCD, e si dispone di un sistema con una bassa quantità di RAM e swap (<1 GB), assicurarsi di impostare la cachedir in /etc/pacman.conf nella nuova partizione di Arch (es. `/newarch/var/cache/pacman/pkg`). Altrimenti si potrebbe esaurire la memoria tra il sovraccarico della distro esistente e il download dei pacchetti necessari per installare.

## Installazione del sistema di destinazione

### Preparare una partizione per Arch

Non è _necessario_ installare Arch su una partizione separata. Si potrebbe invece creare un filesystem di root in una directory normale, e quindi creare una tarball master da questa, o trasferirla attraverso la rete.

Tuttavia, la maggior parte degli utenti preferiranno l'installazione di Arch nella propria partizione.

Preparare tutte le partizioni e i filesystem necessari per l'installazione. Se il sistema host ha un interfaccia grafica per questo, come gparted, cfdisk, o mandrakes diskdrake, usarli senza problemi.

Per formattare una partizione come ext3, si esegue (dove /dev/sdxx è la partizione che si desidera preparare):

```
mkfs.ext3 /dev/sdxx 

```

Per formattare con ext3 con journaling e dir_index:

```
mkfs.ext3 -j -O dir_index /dev/sdxx 

```

Per formattare con reiserfs:

```
mkreiserfs /dev/sdxx 

```

Per formattare una partizione di swap, e iniziare ad usarlo:

```
mkswap /dev/sdxx 
swapon /dev/sdxx

```

La maggior parte degli altri filesystem può essere configurata con la variante mkfs, date uno sguardo con il completamento automatico. I filesystem disponibili dipendono interamente dal proprio sistema host.

Una volta completata la configurazione dei file system, montarli. In questa guida, si farà riferimento alla nuova directory root come /newarch, tuttavia la si può mettere dove si preferisce.

```
new_arch=/newarch
mkdir ${new_arch}
mount /dev/sdxx ${new_arch}

```

### Installare il core

Aggiornare pacman. Potrebbe essere necessario creare la cartella `/newarch/var/lib/pacman` per farlo funzionare ("vedere "Setup the host system" di cui sopra):

```
mkdir -p ${new_arch}/var/lib/pacman 
pacman -Sy -r ${new_arch}

```

**Attenzione:** Problemi durante l'esecuzione di pacman host a 64 bit: Se l'esecuzione di pacman termina con **/tmp/archlinux/usr/bin/pacman: No such file or directory** creare un symlink a ld-linux-x86-64.so.2: **ln -s /lib64/ld-linux-x86-64.so.2 /lib/**

Installare il gruppo "base" di pacchetti:

```
mkdir -p ${new_arch}/var/cache/pacman/pkg
pacman  -Su base --cachedir ${new_arch}/var/cache/pacman/pkg -r ${new_arch}

```

### Preparare i /dev nodes

In primo luogo, assicurarsi che siano stati creati i /dev nodes corretti per udev:

```
ls -alF ${new_arch}/dev

```

Questo risulta in un elenco contenente delle righe simili alle seguenti (le date saranno diverse per voi):

```
crw-------  1 root root 5, 1 2008-12-27 21:40 console
crw-rw-rw-  1 root root 1, 3 2008-12-27 21:42 null
crw-rw-rw-  1 root root 1, 5 2008-12-27 21:40 zero

```

Eliminare e ricreare qualsiasi dispositivo che abbia un diverso insieme di permessi (i contenuti con crw-... più le due voci di root) e numeri maggiori/minori (i due prima della data).

```
cd ${new_arch}/dev 
rm console ; mknod -m 600 console c 5 1 
rm null ; mknod -m 666 null c 1 3 
rm zero ; mknod -m 666 zero c 1 5

```

Tutti i nodi di dispositivo dovrebbe essere già stati creati con i permessi giusti e non dovrebbe essere necessario ricreare qualsiasi di essi.

### Chroot

Ora si effettua il [chroot into the new Arch system](/index.php/Change_root "Change root").

Al fine di far funzionare correttamente i DNS è necessario modificare `${new_arch}/etc/resolv.conf` or replace it with the resolv.conf from your running distribution

```
cp /etc/resolv.conf ${new_arch}/etc/

```

C'è noltre bisogno di copiare un'installazione corretta dei mirrorlist nel nuovo sistema:

```
cp /etc/pacman.d/mirrorlist ${new_arch}/etc/pacman.d

```

Infine modificare i files di configurazione di pacman `${new_arch}/etc/pacman.conf` definendo l'architettura del sistema. Le impostazioni automatiche di default potrebbero fallire se sono differenti dal sistema ospite.

```
Architecture = i686 or x86_64

```

Montare vari filesystem nel nuovo sistema Arch:

```
mount -t proc proc ${new_arch}/proc
mount -t sysfs sys ${new_arch}/sys
mount -o bind /dev ${new_arch}/dev

```

Per una partizione di `/boot` separata, bisognerà probabilmente montare anche quella. Vedere [Change root](/index.php/Change_root "Change root") per maggiori informazioni.

Quando tutto è pronto, effettuare il chroot nel nuovo filesystem:

```
chroot ${new_arch} /bin/bash

```

### Installare il resto

Installare il kernel preferito, e tutti gli altri pacchetti di cui si ha bisogno. Per il kernel di default (che è già installato!):

```
pacman -S --needed linux 

```

Se si desidera installare i pacchetti extra ora, si può farlo con:

```
pacman -S packagename

```

### Configurare il sistema di destinazione

Modificare il `/etc/fstab`, ricordando di aggiungere /, swap e qualsiasi altra partizione si possa voler utilizzare. Assicurarsi di usare il /dev/sd* (sda1, sda2, sdb1, etc) per le partizioni al posto di /dev/hd*, dal momento che Arch utilizza la convenzione sdxx per tutte le unità.

Modificare i file `/etc/rc.conf`, `/etc/hosts` e `/etc/mkinitcpio.conf` a seconda delle proprie esigenze. Poi rigenerare l'immagine initcpio:

```
mkinitcpio -p linux

```

Modificare `/etc/locale.gen`, decommentando qualsiasi locale si desideri avere a disposizione, e compilare le versioni locali:

```
locale-gen

```

### Installazione di grub

Per usare [GRUB](/index.php/GRUB "GRUB") durante il chroot, è necessario che `/etc/mtab` sia a aggiornato:

```
diff /etc/mtab /proc/mounts

```

Se si ottiene qualsiasi risultato dal precedente comando, inserisci:

```
grep -v rootfs /proc/mounts > /etc/mtab  

```

È ora possibile eseguire:

```
grub-install /dev/sdx

```

Se grub-install non riesce, è possibile installarlo manualmente:

```
grub 
grub> find /boot/grub/stage1     (You should see some results here if you have done everything right so far.   If not, back up and retrace your steps.)
grub> root (hd0,X) 
grub> setup (hd0) 
grub> quit 

```

Controllare molto attentamente il file `/boot/grub/menu.lst`. A seconda dell'host, potrebbe essere necessario correggere da hda to sda, oltre al prefisso /boot nel percorso.

#### Ripristino manuale di GRUB libs

I file `*stage*` dovrebbero essere in `/boot/grub`, ma può non essere il caso se il bootloader non è stato installato durante l'installazione del sistema o se la partizione/filesystem erano danneggiati, cancellati accidentalmente, ecc.

Copiare manualmente le librerie grub in questo modo:

```
# cp -a /usr/lib/grub/i386-pc/* /boot/grub

```

**Note:** Non dimenticare di montare la partizione di boot se l'installazione del sistema utilizza una separata! Quanto sopra presuppone che la partizione di boot risieda sul filesystem di root o che sia montata in /boot sul filesystem di root!

Istruzioni dettagliate per [GRUB](/index.php/GRUB "GRUB") e [LILO](/index.php/LILO "LILO") sono disponibili in altre sezioni di questo wiki.

### Ritocchi finali

Consultare [Beginners Guide:Configure your System](/index.php/Beginners%27_guide#Configure_the_System "Beginners' guide"). È possibile ignorare il punto 2.11, ma il resto della guida dovrebbe essere utile nelle configurazioni post-installazione del sistema.

[Uscire da chroot](/index.php/Change_root#Cleaning_up "Change root"):

```
exit
umount ${new_arch}/boot   # if you mounted this or any other separate partitions
umount ${new_arch}/{proc,sys,dev}
umount ${new_arch}

```

Riavviare il nuovo sistema Arch!

## Un terzo (e più semplice) metodo

Questo metodo è stato testato per la versione 1-4-12. Per questo metodo la situazione migliore è quella dell'ambiente LiveCD (o, nel caso di server, un ambiente di recupero basato su gnu/Linux).

Prima di tutto c'è bisogno di montare il disco che si vuole usare per l'installazione di Archlinux in /mnt. In questo esempio viene usato /dev/sda1

```
mnt /dev/sda1 /mnt
cd ~
wget [http://tokland.googlecode.com/svn/trunk/archlinux/arch-bootstrap.sh](http://tokland.googlecode.com/svn/trunk/archlinux/arch-bootstrap.sh) && chmod +x arch-bootstrap.sh

```

Per installare un sistema a 32-bit:

```
./arch-bootstrap.sh /mnt/ i686 "[ftp://ftp.hosteurope.de/mirror/ftp.archlinux.org](ftp://ftp.hosteurope.de/mirror/ftp.archlinux.org)"

```

Per un sistema a 64-bit:

```
./arch-bootstrap.sh /mnt/ x86_64 "[ftp://ftp.hosteurope.de/mirror/ftp.archlinux.org](ftp://ftp.hosteurope.de/mirror/ftp.archlinux.org)"

```

L'avvio richiederà circa 2-5 minuti a seconda della velocità del sistema.

```
mount -t proc none /mnt/proc
mount -t sysfs none /mnt/sys
mount -o bind /dev /mnt/dev

```

Queste operazioni di mount sono essenziali per l'installazione successiva bootloader. Adesso viene la parte divertente, chroot dentro la nuova installazione di Arch:

```
chroot /mnt bash
pacman -Sy base
mkinitcpio -p linux

```

Scegliere un bootloader. Si possono trovare le istruzioni di installazione nelle pagine dedicate. ([Syslinux](/index.php/Syslinux "Syslinux"), [Grub](/index.php/Grub "Grub"), [Grub2](/index.php/Grub2 "Grub2"), etc.).

**Ricorda:** C'è ancora bisogno di fare la configurazioni finali come in una normale installazione Arch.

_Si ringrazia il sito turco: [Raptiye](http://raptiye.org/blog/2011/3/27/hetznerde-arch-linux-kurulumu/) per la guida originale._

## Risoluzione dei problemi

### Kernel Panic

Se quando si riavvia il nuovo sistema si ottiene un kernel panic dicendo la console non ha potuto aprire:

```
kinit: couldn't open console, no such file... 

```

Questo significa che non si sono seguite le istruzioni di cui sopra. Seguire la procedura per creare i nodi dei dispositivo di base all'inizio della preparazione.

### Il dispositivo root "/dev/sd??" non esiste

Se quando si riavvia il nuovo sistema si ottiene un messaggio di errore come questo:

```
Root device '/dev/sda1' doesn't exist, attempting to create it... etc. 

```

Questo significa che le unità vengono visualizzate come "hda1" invece di "sda1" In questo caso modificare le impostazioni di GRUB o LILO per l'uso "hd??" o provare quanto segue.

Modificare /etc/mkinitcpio.conf e sostituire "ide" con "pata" nella riga "HOOKS=". Quindi rigenerare il proprio initrd. (Assicurarsi di essere entrati prima in ambiente chroot nel nuovo sistema.)

```
mkinitcpio -p linux

```

Se si usa LVM assicurati di aggiungere "lvm2" nella riga HOOKS. Rigenera l'initrd come sopra.

Se si sta installando su un dispositivo che ha bisogno dell'hook PATA assicurarsi che sia posizionato prima dell'hook autodetect in mkinitcpio.conf.

Se la partizione root è su un dispositivo USB, è necessario aggiungere "usb" nella riga "HOOKS=" prima di ogni altra cosa, incluso "base".

# Un metodo alternativo: Installazione da un sistema Linux esistente con l'immagine di Arch

### Preparare l'ambiente di installazione

È possibile procurarsi qualsiasi immagine dalla pagina di download di Arch ed ottenere il contenuto dell'immagine per montare il loopback:

Immagine CD i686:

```
$ mkdir -v /mnt/image
$ mount -o loop archlinux-2011.08.19-core-i686.iso /mnt/image

```

creare le directory per l'estrazione dell'immagine e l'ambiente chroot

```
$ mkdir -v /mnt/extract
$ mkdir -pv /mnt/archlinux/lib/modules
$ mkdir -pv /mnt/archlinux/usr/share
$ mkdir -pv /mnt/archlinux/repo/core/{i686,any} 

```

estrarre il contenuto dell'immagine:

```
$ cd /mnt/image/arch/i686/

# root-image 
$ unsquashfs -dest /mnt/extract/root root-image.fs.sfs 
$ mount -t ext4 /mnt/extract/root/root-image.fs /mnt/archlinux

# lib-modules 
$ unsquashfs -dest /mnt/extract/modules lib-modules.fs.sfs 
$ mount -t ext4 /mnt/extract/modules/lib-modules.fs /mnt/archlinux/lib/modules

# repo-core-i686 
$ mount -o loop -t squashfs repo-core-i686.sfs /mnt/archlinux/repo/core/i686

$ cd /mnt/image/arch/any/

# usr-share 
$ unsquashfs -dest /mnt/extract/share usr-share.fs.sfs 
$ mount -t ext4 /mnt/extract/share/usr-share.fs /mnt/archlinux/usr/share

# repo-core-any 
$ mount -o loop -t squashfs repo-core-any.sfs /mnt/archlinux/repo/core/any

```

dopo questa fase, si avrà una nuova cartella archlinux contenente il nuovo sistema Arch.

### Installare dal nuovo ambiente

Ora eseguire il [chroot into the new Arch system](/index.php/Change_root "Change root"):

```
$ mount -t proc /proc /mnt/archlinux/proc
$ mount -t sysfs /sys /mnt/archlinux/sys
$ mount -o bind /dev /mnt/archlinux/dev 
$ chroot /mnt/archlinux /bin/bash

```

A questo punto, andare avanti e lanciare l'installer aif di Arch!

```
$ aif -p interactive

```

ed è possibile installare Arch normalmente (da CD o da Internet) con il seguente puntatore:

*   Your target partition must not be being used by host system

Dopo aver installato Arch dall'ambiente chroot, è necessario smontare le partizioni montate da aif prima di uscire dal chroot:

```
$ umount /mnt/boot,home...
$ exit
$ umount /mnt/archlinux/{dev,sys,proc} 
$ umount /mnt/archlinux/lib/modules
$ umount /mnt/archlinux/usr/share
$ umount /mnt/archlinux/repo/core/{i686,any}
$ umount /mnt/archlinux
$ umount /mnt/image
$ rm -r /mnt/{archlinux,extract} 

```

È indispensabile smontare le partizioni prima di uscire da chroot, altrimenti non si sarà in grado di smontare la directory chroot.

### Aggiornamento e installazione dei pacchetti dal sistema host via chroot

Aggiungere una voce al menu.lst del Grub esistente, o se è stato installato un nuovo Grub durante il processo di installazione, aggiungerlo al file /boot/grub/menu.lst del filesystem di Arch.

Ora riavviare o entrare in [chroot](/index.php/Change_root "Change root") nella nuova partizione di Arch per installare i pacchetti aggiuntivi:

```
$ mkdir /mnt/arch
$ mount /dev/sdxx /mnt/arch
$ mount -t proc proc /mnt/arch/proc
$ mount -t sysfs sys /mnt/arch/sys
$ mount -o bind /dev /mnt/arch/dev 
$ chroot /mnt/arch /bin/bash

```

Aggiornare e installare nuovi pacchetti:

```
# pacman -Syu

```