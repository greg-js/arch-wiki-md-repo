Di seguito è riportato un elenco di domande frequenti su Arch Linux a 64-bit.

## Contents

*   [1 Come posso determinare se il mio processore è compatibile con un sistema x86_64?](#Come_posso_determinare_se_il_mio_processore_.C3.A8_compatibile_con_un_sistema_x86_64.3F)
    *   [1.1 Untenti Linux](#Untenti_Linux)
    *   [1.2 Untenti Windows](#Untenti_Windows)
*   [2 Devo utilizzare una versione a 32-bit o a 64-bit di Arch Linux?](#Devo_utilizzare_una_versione_a_32-bit_o_a_64-bit_di_Arch_Linux.3F)
*   [3 Come faccio a installare Arch64?](#Come_faccio_a_installare_Arch64.3F)
*   [4 A che punto è il trasferimento del software?](#A_che_punto_.C3.A8_il_trasferimento_del_software.3F)
*   [5 Avrò tutti i pacchetti della mia versione 32-bit di Arch che sono abituato ad utilizzare?](#Avr.C3.B2_tutti_i_pacchetti_della_mia_versione_32-bit_di_Arch_che_sono_abituato_ad_utilizzare.3F)
*   [6 Perché 64-bit?](#Perch.C3.A9_64-bit.3F)
*   [7 Come faccio a segnalare un bug?](#Come_faccio_a_segnalare_un_bug.3F)
*   [8 Quali repository dovrei utilizzare per pacman?](#Quali_repository_dovrei_utilizzare_per_pacman.3F)
*   [9 Come posso modificare i PKGBUILD per usarli con Arch64?](#Come_posso_modificare_i_PKGBUILD_per_usarli_con_Arch64.3F)
*   [10 Cosa mi mancherà in Arch64?](#Cosa_mi_mancher.C3.A0_in_Arch64.3F)
*   [11 Posso eseguire applicazioni 32-bit all'interno di Arch64?](#Posso_eseguire_applicazioni_32-bit_all.27interno_di_Arch64.3F)
*   [12 Posso compilare un pacchetto 32-bit per architettura i686 all'interno di Arch64?](#Posso_compilare_un_pacchetto_32-bit_per_architettura_i686_all.27interno_di_Arch64.3F)
    *   [12.1 Deposito Multilib](#Deposito_Multilib)
    *   [12.2 Chroot](#Chroot)
*   [13 Posso aggiornare/migrare il mio sistema da i686 a x86_64 senza reinstallare?](#Posso_aggiornare.2Fmigrare_il_mio_sistema_da_i686_a_x86_64_senza_reinstallare.3F)

## Come posso determinare se il mio processore è compatibile con un sistema x86_64?

### Untenti Linux

Lanciare il seguente comando:

```
$ less /proc/cpuinfo

```

Controllare la voce `flags`. Se tra le varie voci è presente `lm`, allora il vostro processore è x86_64 compatibile.

In alternativa potete eseguire questo comando:

```
  $ grep -q "^flags.*\blm\b" /proc/cpuinfo && echo "x86_64" || echo "not x86_64"

```

### Untenti Windows

Utilizzando il programma gratuito [CPU-Z](http://www.cpuid.com/cpuz.php) è possibile determinare se il vostra CPU sia un processore 64-bit compatibile. I processori AMD con set di istruzioni "AMD64" o le soluzioni Intel "EM64T" risultano compatibili con la versione x86_64 e i relativi pacchetti binari.

## Devo utilizzare una versione a 32-bit o a 64-bit di Arch Linux?

Se il vostro processore è [x86_64](https://en.wikipedia.org/wiki/it:X86-64 "wikipedia:it:X86-64") compatibile è necessario considerare l'utilizzo di Arch64.

## Come faccio a installare Arch64?

Basta utilizzare il nostro [CD di installazione ufficiale](https://www.archlinux.org/download/).

## A che punto è il trasferimento del software?

Arch64 è pronto per l'uso quotidiano in un ambiente desktop o server.

## Avrò tutti i pacchetti della mia versione 32-bit di Arch che sono abituato ad utilizzare?

I repository sono tutti stati migrati e praticamente tutto dovrebbe funzionare come previsto.

Raramente un vecchio pacchetto presente in [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") potrebbe contenere solo l'architettura `'i686'`, ma spesso è in grado di essere compilato sui sistemi a 64-bit, basta aggiungere `'x86_64'`.

## Perché 64-bit?

È solitamente più veloce nella maggior parte delle ciscostanze ed inoltre è leggermente più sicuro a causa della natura dell'[Address space layout randomization (ASLR)](https://en.wikipedia.org/wiki/it:ASLR "wikipedia:it:ASLR") in combinazione con [Position-independent code (PIC)](https://en.wikipedia.org/wiki/Position-independent_code "wikipedia:Position-independent code") e [NX Bit](https://en.wikipedia.org/wiki/it:NX_Bit "wikipedia:it:NX Bit") che non è disponibile nel kernel i686 a causa di disabilità PAE. Se nel vostro computer sono presenti 4GB di RAM o più utilizzabile, dovreste seriamente considerare l'utilizzo della versione a 64-bit, poichè il quantitativo di RAM superiore ai 3GB non verrà utilizzato da un sistema operativo a 32-bit.

Anche i programmatori tendono sempre meno ad interessarsi all'architettura 32-bit ("legacy"), così come le "nuove" CPU x86 di solito supportano le estensioni a 64-bit.

Ci sono molti altri motivi che potremmo elencare qui per dirvi di evitare 32-bit, ma tra kernel, ambiente userspace e programmi individuali, risulta impraticabile elencare ogni cosa che un sistema a 64-bit fa molto meglio.

Per ulteriori dettagli si può consultare il nostro [report delle differenze](https://www.archlinux.org/packages/differences/). Dove potrete trovare una lista di comparazione della versione dei pacchetti 32/64-bit.

## Come faccio a segnalare un bug?

Semplicemente utilizzando Arch's [Flyspray](https://bugs.archlinux.org/), ma selezionate `x86_64` nel campo dell'architettura se pensate che sia un problema relativo al port del programma.

## Quali repository dovrei utilizzare per pacman?

Tutti i repository sono supportati per la versione 64-bit.

## Come posso modificare i PKGBUILD per usarli con Arch64?

Aggiungere ad ogni pacchetto la variabile:

```
arch=('i686' '**x86_64'**) 

```

Aggiungete piccole patch direttamente ai sorgenti e all'area md5 ma usate sorgenti completamente differenti rispetto a quelle per i686:

```
[ "$CARCH" = "x86_64" ] && source=(${source[@]} 'other source')
[ "$CARCH" = "x86_64" ] && md5sums=(${md5sums[@]} 'other md5sum')

```

Per qualsiasi piccolo fix, usate questo nella sezione 'build':

```
[ "$CARCH" = "x86_64" ] && (patch -Np0 -i ../foo_x86_64.patch)

```

O quando avete bisogno di più cambiamenti:

```
if [ "$CARCH" = "x86_64" ]; then
    configure/patch/sed      # for x86_64
  else configure/patch/sed   # for i686
fi

```

## Cosa mi mancherà in Arch64?

Niente. Quasi tutte le applicazioni supportano 64-bit per ora o sono nella fase di transizione per diventare a 64-bit compatibile.

Il problema più grande sono i pacchetti che sono **closed source** o contiene x86 specifico assembly che è ingombrante per essere trasposto a 64-bit (tipico per gli emulatori).

Alcune applicazioni erano problematiche, ma sono ora disponibili su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") e funzionano bene:

*   Acrobat Reader non è disponibile in 64-bit, ma è possibile eseguire la versione a 32-bit in modalità compatibile. Ci sono anche molte altre alternative open source che si possono utilizzare per leggere i file PDF.

Tutto il resto dovrebbe funzionare perfettamente bene. Se vi dovesse mancare un pacchetto Arch32 nel nostro repository e si sa che si può compilare su x86_64 (forse l'avete trovato come pacchetti nativi in un altra distribuzione a 64-bit), basta contattare gli sviluppatori o richiedere un nuovo pacchetto nel forum.

## Posso eseguire applicazioni 32-bit all'interno di Arch64?

Certamente.

*   Potete installare le librerie `lib32-*` dal repsository `[multilib]`. Per poter usare questo repositorio de-commentare le seguenti linee al proprio `/etc/pacman.conf`.

```
[multilib]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

```

Attualmente (dicembre 2011) [multilib] contiene wine e Skype. Inoltre è disponibile un compilatore in multilib.

*   In alternativa potete creare un sistema a 32-bit con chroot (si veda [Arch64 Install bundled 32bit system](/index.php/Arch64_Install_bundled_32bit_system "Arch64 Install bundled 32bit system")):

Avviare il sistema Arch64, aprire un terminale e digitare:

```
$ xhost +local:
$ su
# mount /dev/sda1 /mnt/arch32
# mount --bind /proc /mnt/arch32/proc
# chroot /mnt/arch32
# su il-proprio-32bit-nomeutente
$ /usr/bin/comando che volete # ad esempio: /opt/mozilla/bin/firefox

```

Alcune applicazioni a 32-bit (come OpenOffice) possono richiedere ulteriori binding. Le righe seguenti può essere posizionato in `/etc/rc.local` per essere sicuri di ottenere tutto il necessario per le applicazioni a 32-bit (si presuppone che `/mnt/arch32` sia montato in `/etc/fstab`):

```
mount --bind /dev /mnt/arch32/dev
mount --bind /dev/pts /mnt/arch32/dev/pts
mount --bind /dev/shm /mnt/arch32/dev/shm
mount --bind /proc /mnt/arch32/proc
mount --bind /proc/bus/usb /mnt/arch32/proc/bus/usb
mount --bind /sys /mnt/arch32/sys
mount --bind /tmp /mnt/arch32/tmp
#commentare la linea successiva se non si vuole utilizzare la cartella home
mount --bind /home /mnt/arch32/home

```

Ora è possibile digitare in un terminale:

```
$ xhost +localhost
$ sudo chroot /mnt/arch32 su il-proprio-32bit-nomeutente /opt/openoffice/program/soffice

```

## Posso compilare un pacchetto 32-bit per architettura i686 all'interno di Arch64?

Certamente, è possibile utilizzare:

*   le versioni multilib dei pacchetti interessati dal repository [multilib]
*   una sessione chroot i686

### Deposito [Multilib](/index.php/Multilib "Multilib")

Per utilizzare il repository [multilib], editare il proprio `/etc/pacman.conf` e decommentare quanto segue:

```
[multilib]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

```

Aggiornare il sistema con `pacman -Syu` e installare il pacchetto [gcc-multilib](https://www.archlinux.org/packages/?name=gcc-multilib).

**Nota:**

*   Se nel sistema è installato il gruppo `base-devel`, gli utenti devono sostituire le versioni [extra] con le versioni presenti in [multilib], come mostrato in seguito.
*   [gcc-multilib](https://www.archlinux.org/packages/?name=gcc-multilib) è in grado di costruire codice a 32-bit e 64-bit. Si può installare `multilib-devel` e sostituire i pacchetti indicati qui di seguito, ma `base-devel` è ancora necessario per gli altri pacchetti che include. Vedere https://bbs.archlinux.org/viewtopic.php?id=102828 per ulteriori informazioni.

 `# pacman -S gcc-multilib` 

```
resolving dependencies...
warning: dependency cycle detected:
warning: lib32-gcc-libs will be installed before its gcc-libs-multilib dependency
looking for inter-conflicts...
:: gcc-libs-multilib and gcc-libs are in conflict. Remove gcc-libs? [y/N] y
:: binutils-multilib and binutils are in conflict. Remove binutils? [y/N] y
:: gcc-multilib and gcc are in conflict. Remove gcc? [y/N] y
:: libtool-multilib and libtool are in conflict. Remove libtool? [y/N] y

Remove (4): gcc-libs-4.6.1-1  binutils-2.21.1-1  gcc-4.6.1-1  libtool-2.4-4

Total Removed Size:   87.65 MB

Targets (7): lib32-glibc-2.14-4  lib32-gcc-libs-4.6.1-1  gcc-libs-multilib-4.6.1-1  binutils-multilib-2.21.1-1
             gcc-multilib-4.6.1-1  lib32-libtool-2.4-2  libtool-multilib-2.4-2

Total Download Size:    25.04 MB
Total Installed Size:   108.27 MB

Proceed with installation? [Y/n]
```

Compilare un pacchetto su x86_64 per architettura i686 risulta semplice aggiungendo le seguenti linee in un file di configurazione alternativo, ad esempio `~/.makepkg.i686.conf`.

```
CARCH="i686"
CHOST="i686-pc-linux-gnu"
CFLAGS="-m32 -march=i686 -mtune=generic -O2 -pipe -fstack-protector --param=ssp-buffer-size=4 -D_FORTIFY_SOURCE=2"
CXXFLAGS="${CFLAGS}"

```

E successivamente invocare `makepkg` come segue:

```
$ linux32 makepkg -src --config ~/.makepkg.i686.conf

```

### Chroot

Per utilizzare un chroot i686 (Un modo veloce e raccomandato è quello di effettuare una installazione con una iso i686 "QuickInstall" all'interno Arch64 o vedere [Arch64 Install bundled 32bit system](/index.php/Arch64_Install_bundled_32bit_system "Arch64 Install bundled 32bit system")), installare il corrente pacchetto "linux32" per il wrapper per fare il chroot e si comporterà come un vero e proprio sistema i686\. Quindi utilizzare questo script per il login nell'ambiente chroot come root:

```
#!/bin/bash
mount --bind /dev /path-to-your-chroot/dev
mount --bind /dev/pts /path-to-your-chroot/dev/pts
mount --bind /dev/shm /path-to-your-chroot/dev/shm
mount -t proc none /path-to-your-chroot/proc
mount -t sysfs none /path-to-your-chroot/sys
linux32 chroot /path-to-your-chroot

```

Se si mantengono i sorgenti sul sistema host x86_64 si può aggiungere

```
mount --bind /percorso-dei-sorgenti-d'origine /percorso-del-chroot/percorso-dei-sorgenti-di-destinazione

```

per poter condividere i sorgenti dal sistema host al sistema chroot per poter compilare i pacchetti utilizzando `/etc/makepkg.conf`.

## Posso aggiornare/migrare il mio sistema da i686 a x86_64 senza reinstallare?

No. In senso stretto alcun tipo di migrazione implica che tutti i pacchetti o quasi tutti i pacchetti devono essere reinstallati per l'architettura più recente. Tuttavia, è possibile spostare il sistema senza eseguire una nuova installazione, anche all'interno dell'installazione corrente . Una [discussione](https://bbs.archlinux.org/viewtopic.php?id=64485) sul forum è stata creata e che delinea misure adottate per migrare con successo un'installazione 32/64-bit, senza perdere alcun file di configurazione/impostazioni/dati. Nota: un grande disco esterno è stato utilizzato per il trasferimento.

Tuttavia, è anche possibile avviare il sistema con l'installazione Arch64 CD, montare il disco, è consigliato effettuare un backup di qualsiasi cosa che non sia un binario a 32-bit (ad esempio: `/home` e `/etc`), e installare.

Si consiglia inoltre di leggere [Migrazione tra architetture senza dover reinstallare](/index.php/Migrating_Between_Architectures_Without_Reinstalling "Migrating Between Architectures Without Reinstalling").