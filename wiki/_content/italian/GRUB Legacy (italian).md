Articoli correlati

*   [Boot debugging](/index.php/Boot_debugging "Boot debugging")
*   [GRUB2 (Italiano)](/index.php/GRUB2_(Italiano) "GRUB2 (Italiano)")
*   [grub-gfx (Italiano)](/index.php/Grub-gfx_(Italiano) "Grub-gfx (Italiano)")
*   [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters")
*   [LILO](/index.php/LILO "LILO")
*   [MBR](/index.php/MBR "MBR")

[GNU GRUB (Legacy)](http://www.gnu.org/software/grub/grub-legacy.html) è un bootloader [multiboot](http://www.gnu.org/software/grub/manual/multiboot/) mantenuto dal [GNU Project](/index.php/GNU_Project "GNU Project"). Deriva da GRUB, il GRand Unified Bootloader, che è stato originariamente progettato e realizzato da Erich Stefan Boleyn.

Brevemente, il *bootloader* è il primo programma che si avvia quando si accende il computer. È il responsabile del controllo di caricamento e di trasferimento al kernel Linux. Il kernel, a sua volta, inizializza il resto del sistema operativo.

**Nota:** GRUB Legacy è completamente deprecato e rimpiazzato da [GRUB 2.x](/index.php/GRUB2_(Italiano) "GRUB2 (Italiano)"). Si consiglia di prendere visione di [questa](http://www.archlinux.it/forum/viewtopic.php?f=15&t=15043) news. Si raccomanda l'utilizzo di [GRUB2](/index.php/GRUB2_(Italiano) "GRUB2 (Italiano)") o [Syslinux](/index.php/Syslinux "Syslinux").

## Contents

*   [1 Installazione](#Installazione)
*   [2 Aggiornamento a GRUB(2)](#Aggiornamento_a_GRUB.282.29)
    *   [2.1 È necessario aggiornare?](#.C3.88_necessario_aggiornare.3F)
    *   [2.2 Come effettuare l'aggiornamento](#Come_effettuare_l.27aggiornamento)
*   [3 Configurazione](#Configurazione)
    *   [3.1 Trovare la root di GRUB](#Trovare_la_root_di_GRUB)
    *   [3.2 Dual booting con Windows](#Dual_booting_con_Windows)
    *   [3.3 Dual booting con GNU/Linux](#Dual_booting_con_GNU.2FLinux)
    *   [3.4 chainloader e configfile](#chainloader_e_configfile)
    *   [3.5 Dual boot con GNU/Linux (Grub2)](#Dual_boot_con_GNU.2FLinux_.28Grub2.29)
*   [4 Installazione del bootloader](#Installazione_del_bootloader)
    *   [4.1 Recupero manuale di GRUB libs](#Recupero_manuale_di_GRUB_libs)
    *   [4.2 Note generali di installazione del bootloader](#Note_generali_di_installazione_del_bootloader)
    *   [4.3 Installazione nel MBR](#Installazione_nel_MBR)
    *   [4.4 Installazione su una partizione](#Installazione_su_una_partizione)
    *   [4.5 Metodo alternativo (installazione di grub)](#Metodo_alternativo_.28installazione_di_grub.29)
*   [5 Suggerimenti](#Suggerimenti)
    *   [5.1 Avvio grafico](#Avvio_grafico)
    *   [5.2 Risoluzione framebuffer](#Risoluzione_framebuffer)
        *   [5.2.1 Valore riconosciuto del GRUB](#Valore_riconosciuto_del_GRUB)
        *   [5.2.2 hwinfo](#hwinfo)
        *   [5.2.3 vbetest](#vbetest)
    *   [5.3 Nominare le partizioni](#Nominare_le_partizioni)
        *   [5.3.1 Per etichetta](#Per_etichetta)
        *   [5.3.2 Per UUID](#Per_UUID)
    *   [5.4 Eseguire il boot come root (single-user mode)](#Eseguire_il_boot_come_root_.28single-user_mode.29)
    *   [5.5 Protezione con password](#Protezione_con_password)
    *   [5.6 Riavviare con la scelta nominale di boot](#Riavviare_con_la_scelta_nominale_di_boot)
    *   [5.7 Interazione LILO e GRUB](#Interazione_LILO_e_GRUB)
    *   [5.8 GRUB boot disk](#GRUB_boot_disk)
    *   [5.9 Nascondere il menu di GRUB](#Nascondere_il_menu_di_GRUB)
*   [6 Modalità debug avanzata](#Modalit.C3.A0_debug_avanzata)
*   [7 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [7.1 GRUB Errore 17](#GRUB_Errore_17)
    *   [7.2 /boot/grub/stage1 not read correctly](#.2Fboot.2Fgrub.2Fstage1_not_read_correctly)
    *   [7.3 Installazione accidentale in una partizione Windows](#Installazione_accidentale_in_una_partizione_Windows)
    *   [7.4 Modificare le voci GRUB nel menu di avvio](#Modificare_le_voci_GRUB_nel_menu_di_avvio)
    *   [7.5 Errore device.map](#Errore_device.map)
    *   [7.6 Errore sotto-menu di KDE al riavvio](#Errore_sotto-menu_di_KDE_al_riavvio)
    *   [7.7 GRUB non riesce a trovare o installare qualsiasi virtio /dev/vd* o altri dispositivi non-BIOS](#GRUB_non_riesce_a_trovare_o_installare_qualsiasi_virtio_.2Fdev.2Fvd.2A_o_altri_dispositivi_non-BIOS)
*   [8 Risorse esterne](#Risorse_esterne)

## Installazione

[grub-legacy](https://aur.archlinux.org/packages/grub-legacy/) era installato di base quando si installava Arch Linux. Ora il suo supporto è terminato ed è stato spostato su [aur](/index.php/AUR_(Italiano) "AUR (Italiano)").

GRUB deve essere installato nel settore di boot di un'unità o di una partizione per funzionare come bootloader. Ciò è spiegato nella sezione [#Installazione del bootloader](#Installazione_del_bootloader).

## Aggiornamento a [GRUB](/index.php/GRUB "GRUB")(2)

### È necessario aggiornare?

La risposta breve è no. GRUB legacy non sarà rimosso dal sistema e continuerà a funzionare.

D'altra parte però, come ogni pacchetto non più supportato dall'upstream, eventuali bug non verranno risolti. Per questo motivo è necessario prendere in considerazione l'idea di aggiornare GRUB alla versione 2.x, o un altro [Boot Loader](/index.php/Boot_Loader "Boot Loader") supportato.

GRUB Legacy non supporta partizioni [GPT](/index.php/GPT "GPT"), il filesystem [Btrfs](/index.php/Btrfs "Btrfs") e il firmware [UEFI](/index.php?title=UEFI_(Italiano)&action=edit&redlink=1 "UEFI (Italiano) (page does not exist)").

### Come effettuare l'aggiornamento

Aggiornare da GRUB Legacy a [GRUB 2.x](/index.php/GRUB_(Italiano) "GRUB (Italiano)")) è la stessa cosa che installare GRUB 2.x da un sistema Arch avviato. Tutti i dettagli sono sulla relativa pagina [GRUB (Italiano)#Installazione](/index.php/GRUB_(Italiano)#Installazione "GRUB (Italiano)").

## Configurazione

Il file di configurazione si trova in `/boot/grub/menu.lst`. Modificare questo file in base alle proprie esigenze.

*   `timeout #` -- tempo d'attesa (in secondi) prima che il sistema operativo di `default` venga automaticamente caricato.
*   `default #` -- la voce d'avvio di default che viene scelta quando il `timeout` termina.

Una configurazione d'esempio (con `/boot` su una partizione separata):

```
/boot/grub/menu.lst

```

```
# Config file for GRUB - The GNU GRand Unified Bootloader
# /boot/grub/menu.lst

# DEVICE NAME CONVERSIONS
#
#  Linux           GRUB
# -------------------------
#  /dev/fd0        (fd0)
#  /dev/sda        (hd0)
#  /dev/sdb2       (hd1,1)
#  /dev/sda3       (hd0,2) (hd0,0
#

#  FRAMEBUFFER RESOLUTION SETTINGS
#     +-------------------------------------------------+
#          | 640x480    800x600    1024x768   1280x1024
#      ----+--------------------------------------------
#      256 | 0x301=769  0x303=771  0x305=773   0x307=775
#      32K | 0x310=784  0x313=787  0x316=790   0x319=793
#      64K | 0x311=785  0x314=788  0x317=791   0x31A=794
#      16M | 0x312=786  0x315=789  0x318=792   0x31B=795
#     +-------------------------------------------------+
#  for more details and different resolutions see
#  https://wiki.archlinux.org/index.php/GRUB#Framebuffer_Resolution

# general configuration:
timeout   5
default   0
color light-blue/black light-cyan/blue

# boot sections follow
# each is implicitly numbered from 0 in the order of appearance below
#
# TIP: If you want a 1024x768 framebuffer, add "vga=773" to your kernel line.
#
#-*

# (0) Arch Linux
title  Arch Linux
root   (hd0,0)
kernel /vmlinuz-linux root=/dev/sda3 ro
initrd /initramfs-linux.img

# (1) Windows
#title Windows
#rootnoverify (hd0,0)
#makeactive
#chainloader +1

```

### Trovare la root di GRUB

GRUB deve conoscere dove si trovano i suoi file nel sistema, dal momento che potrebbero esistere più istanze (ad esempio, in ambienti multi-boot). I file di GRUB risiedono sempre sotto `/boot`, che potrebbe trovarsi su una partizione dedicata.

**Note:** GRUB definisce i dispositivi d'archiviazione in maniera diversa da come lo fa il kernel.

*   Gli Hard disk sono definiti come **(hdX)**, questo si riferisce anche a qualsiasi dispositivo d'archiviazione USB.
*   La numerazione dei dispositivi e delle partizioni comincia da zero. Ad esempio, il primo hard disk riconosciuto dal BIOS sarà definito come **(hd0)**. Il secondo dispositivo sarà chiamato **(hd1)**. Ciò viene applicato anche alle partizioni. Quindi, la seconda partizione nel primo hard disk sarà definita come **(hd0,1)**.

Se non si è sicuri della posizione di `/boot`, si usi il comando della shell di GRUB `find` per individuare i file di GRUB. Si entri nella shell di GRUB da root con:

 `# grub` 

L'esempio seguente è per sistemi "senza" una partizione separata di `/boot`, dove `/boot` è semplicemente una cartella sotto `/`:

 `grub> find /boot/grub/stage1` 

L'esempio seguente è per sistemi "con" una partizione di `/boot` separata:

 `grub> find /grub/stage1` 

GRUB troverà i file, ed indicherà la corretta posizione del file `stage1`. Ad esempio:

 `grub> find /grub/stage1`  ` (hd0,0)` 

Questo valore deve essere inserito nella linea `root` nel proprio file di configurazione. Si digiti `quit` per uscire dalla shell.

### Dual booting con Windows

Si aggiunga ciò che segue alla fine del file `/boot/grub/menu.lst` (presupponendo che la partizione di Windows si trovi sulla prima partizione del primo dispositivo d'archiviazione):

 `/boot/grub/menu.lst` 
```
 title Windows
 rootnoverify (hd0,0)
 makeactive chainloader +1

```

**Nota:** Se sul proprio computer si ha in dual-boot ArchLinux e Windows 7, si dovrà commentare la linea `makeactive`

**Note:** Windows 2000 e le versioni successive NON hanno bisogno di trovarsi nella prima partizione per essere avviate (contrariamente alla credenza popolare). Se la partizione di Windows dovesse cambiare (ad esempio se si aggiunge una partizione prima di quella di Windows), sarà necessario editare il file di Windows `boot.ini` per indicarne il cambiamento (si veda [questo articolo](http://vlaurie.com/computers2/Articles/bootini.htm) per i dettagli su come farlo).

Nel caso in cui Windows si trovi su un'altro hard disk, occorre usare il comando `map`. Ciò farà si che l'installatore di Windows pensi di trovarsi sul primo dispositivo. Supponendo che la partizione di Windows si trovi sulla prima partizione del secondo dispositivo d'archiviazione:

 `/boot/grub/menu.lst` 
```
 title Windows
 map (hd0) (hd1)
 map (hd1) (hd0)
 rootnoverify (hd1,0)
 makeactive
 chainloader +1

```

**Nota:** Se sul proprio computer si ha in dual-boot ArchLinux e Windows 7, si dovrà commentare la linea `makeactive`

### Dual booting con GNU/Linux

Ciò può essere fatto nella stessa maniera in cui viene definita un'installazione di Arch Linux. Ad esempio:

 `/boot/grub/menu.lst` 
```
 title Other Linux
 root (hd0,2)
 kernel /path/to/kernel root=/dev/sda3 ro
 initrd /path/to/initrd

```

**Note:** Comunque, potrebbero esserci altre opzioni necessarie, e potrebbe non essere usato un iniziale RAM disk. Si analizzi il `/boot/grub/menu.lst` delle altre distribuzioni per aggiungerne le opzioni d'avvio, o si veda [#chainloader e configfile](#chainloader_e_configfile) (raccomandato).

### `chainloader` e `configfile`

Per facilitare la manutenzione del sistema, il comando `chainloader` o `configfile` dovrebbe essere usato per avviare un'altra distribuzione Linux che fornisce un meccanismo di configurazione GRUB "automatico" (ad esempio Debian, Ubuntu, openSUSE). Ciò permette alla distribuzione di mantenere il proprio `menu.lst` e le opzioni di boot.

*   Il comando `chainloader` avvierà un altro bootloader (piuttosto che un'immagine kernel); utile se un'altro bootloader è installato in un settore di boot di una partizione (GRUB, ad esempio). Ciò permette di installare un'istanza "principale" di GRUB nel [MBR](/index.php/MBR "MBR") e istanze di GRUB specifiche delle distribuzioni in ogni settore boot di partizione (PBR).

*   Il comando `configfile` avvisa l'istanza corrente di GRUB di caricare il file di configurazione specificato. Ciò può essere usato per avviare il `menu.lst` di un'altra distribuzione senza un'installazione separata di GRUB. Il problema di quest'approccio è che l'altro `menu.lst` potrebbe non essere compatibile con la versione installata di GRUB; alcune distribuzioni creano infatti pesanti patch alla propria versione di GRUB.

Ad esempio, GRUB deve essere installato nel [MBR](/index.php/MBR "MBR") e qualche altro bootloader (sia esso GRUB o [LILO](/index.php/LILO "LILO")) è già installato nel settore boot di `(hd0,2)`.

```
---------------------------------------------
|   |           |           |   %           |
| M |           |           | B %           |
| B |  (hd0,0)  |  (hd0,1)  | L %  (hd0,2)  |
| R |           |           |   %           |
|   |           |           |   %           |
---------------------------------------------
  |                           ^
  |       chainloading        |
  -----------------------------

```

Si può semplicemente includere in `menu.lst`:

```
title Altro Linux
root (hd0,2)
chainloader +1

```

O, se il bootloader in `(hd0,2)` è GRUB:

```
title Altro Linux
root (hd0,2)
configfile /boot/grub/menu.lst

```

Il comando `chainloader` può anche essere usato per caricare l'MBR di un secondo dispositivo:

```
title Altro Disposisitivo
rootnoverify (hd1)
chainloader +1

```

### Dual boot con GNU/Linux (Grub2)

Se l'altra distribuzione Linux utilizza Grub2 (es. Ubuntu 9.10+), e si ha installato il relativo boot loader per la relativa partizione di root, è possibile aggiungere una voce come questa nel `/boot/grub/menu.lst`:

 `/boot/grub/menu.lst` 
```
 # Altra distribuzione Linux che usa Grub2
 title Ubuntu
 root (hd0,2)
 kernel /boot/grub/core.img

```

Selezionando questa voce dal menu di avvio verrà caricato il menu di Grub2 dell'altra distribuzione, assumendo che questa sia installata su `/dev/sda3`.

## Installazione del bootloader

### Recupero manuale di GRUB libs

Normalmente i file interessati (`*stage*`) dovrebbero essere in `/boot/grub`, salvo nei casi in cui il bootloader non sia stato installato durante l'installazione del sistema o la partizione/filesystem sia danneggiato, o accidentalmente cancellato.

Copiare manualmente le librerie grub così:

 `# cp -a /usr/lib/grub/i386-pc/* /boot/grub` 
**Note:** Non dimenticare di installare la partizione di boot del sistema se il programma di installazione utilizza una partizione separata! Quanto sopra presuppone che o la partizione di boot risiede sul filesystem di root o è montata in /boot nel file system di root!

### Note generali di installazione del bootloader

GRUB può essere installato da un supporto separato (ad esempio un live CD), o direttamente da un'installazione di arch in esecuzione. È *raramente* necessario che il bootloader GRUB debba essere reinstallato, e l'installazione *non* è necessaria quando:

*   Il file di configurazione viene aggiornato.
*   Il pacchetto [grub](https://www.archlinux.org/packages/?name=grub) è aggiornato.

L'installazione è *necessaria* quando:

*   Un bootloader non è già installato.
*   Un altro sistema operativo sovrascrive il bootloader di Linux.
*   Il bootloader fallisce per qualche motivo sconosciuto.

Prima di continuare, alcune osservazioni:

*   Assicurarsi che la configurazione di GRUB sia corretta (`/boot/grub/menu.lst`) prima di procedere. Fare riferimento a [#Trovare la root di GRUB](#Trovare_la_root_di_GRUB) per verificare che i dispositivi siano definiti in modo corretto.
*   GRUB deve essere installato nel MBR [MBR](/index.php/MBR "MBR") (primo settore del disco rigido), o la prima partizione della periferica di archiviazione per poter essere riconosciuto dalla maggior parte dei BIOS. Per consentire alle distribuzioni la capacità di gestire i propri menu di GRUB, possono essere utilizzate più istanze di GRUB. Si veda [#chainloader e configfile](#chainloader_e_configfile).
*   Per installare il bootloader GRUB, può essere necessario intervenire dall'interno di un ambiente `chroot` (cioè da un ambiente installato tramite un supporto separato) per casi come configurazioni RAID o se si è dimenticata o danneggiata l'installazione di GRUB. Sarà necessario eseguire l'operazione di [Change root](/index.php/Change_root "Change root") da un LiveCD o da un'altra installazione di Linux per poterlo fare.

In primo luogo, inserire la shell di GRUB:

 `# grub` 

Utilizzare il comando `root` con l'output del comando `find` (consultare [#Trovare la root di GRUB](#Trovare_la_root_di_GRUB)) per istruire GRUB su quale partizione contiene lo stage1 (e quindi, `/boot`):

 `grub> root (hd1,0)` 
**Tip:** La shell di GRUB supporta anche la scheda di completamento. Se si digita "root hd" e si preme due volte **Tab** si potranno vedere le periferiche di archiviazione disponibili, e lo stesso può essere fatto anche per le partizioni. La tab-completion funziona anche dal menu di avvio di GRUB. Se c'è un errore nel file di configurazione è possibile modificarlo nel menù di avvio, e aiutandosi con la scheda di completamento, trovare i dispositivi e le partizioni. Consultare [#Modificare le voci GRUB nel menu di avvio](#Modificare_le_voci_GRUB_nel_menu_di_avvio).

### Installazione nel MBR

L'esempio seguente installa GRUB nel [MBR](/index.php/MBR "MBR") del primo disco:

 `grub> setup (hd0)` 

### Installazione su una partizione

L'esempio seguente installa GRUB sulla prima partizione del primo disco:

 `grub> setup (hd0,0)` 

Dopo aver eseguito il programma di installazione `setup`, digitare `quit` per uscire dalla shell. Se si è in ambiente chroot, [uscire da chroot e smontare le partizioni](/index.php/Change_root "Change root"). Adesso riavviare per fare un test.

### Metodo alternativo (installazione di grub)

**Nota:** Questa procedura è nota per essere meno affidabile, il metodo consigliato è quello di utilizzare la shell di GRUB.

Utilizzare il comando `grub-install` seguito dal percorso su cui installare il bootloader. Ad esempio, per installare il bootloader GRUB nel MBR del primo disco:

 `# grub-install /dev/sda` 

GRUB viene indicato se installato correttamente. Se così non fosse, si dovrà utilizzare il metodo shell di GRUB.

## Suggerimenti

Note di configurazione aggiuntive.

### Avvio grafico

Per coloro che desiderano un aspetto grafico esteticamente più rifinito, consultare [grub-gfx](/index.php/Grub-gfx_(Italiano) "Grub-gfx (Italiano)"). [GRUB2](/index.php/GRUB2_(Italiano) "GRUB2 (Italiano)") offre funzionalità grafiche avanzate, come immagini di sfondo e caratteri bitmap.

### Risoluzione framebuffer

Si può utilizzare la risoluzione fornite nel `menu.lst`, ma si può eventualmente utilizzare il proprio LCD wide-screen a la sua risoluzione nativa. Ecco cosa si può fare per ottenere questo risultato:

Su [Wikipedia](https://en.wikipedia.org/wiki/VESA_BIOS_Extensions#Linux_video_mode_numbers "wikipedia:VESA BIOS Extensions") c'è una lista di risoluzioni framebuffer esteso (cioè oltre quelle standard VBE). Ma, per esempio, quella che si vuole usare per 1440x900 (`vga=867`) non funziona. Questo perché il produttori di schede grafiche sono liberi di scegliere qualsiasi numero desiderano, in quanto questo non fa parte dello standard VBE 3\. Questo è il motivo per cui questi codici possono variare da una scheda all'altra (eventualmente anche per il produttore stesso).

Così, invece di usare quella tabella, è possibile utilizzare uno degli strumenti indicati in seguito per ottenere il codice corretto:

#### Valore riconosciuto del GRUB

Questo è un modo semplice per trovare il codice di risoluzione usando solo GRUB.

Sulla riga del kernel, specificare che il kernel richieda quale modalità utilizzare.

```
kernel /vmlinuz-linux root=/dev/sda1 ro **vga=ask**

```

Adesso riavviare. GRUB presenterà ora un elenco di codici adatti per l'uso, oltre l'opzione per cercarne altri.

Scegliere il codice che si desidera utilizzare (non dimenticarlo, in quanto necessario per il passaggio successivo) e avviare utilizzandolo.

Ora sostituire `ask` nella riga del kernel con quello che si è scelto.

Per esempio la riga del kernel per `[369] 1680x1050x32` sarebbe:

```
kernel /vmlinuz-linux root=/dev/sda1 ro **vga=0x369**

```

#### hwinfo

1.  Installare [hwinfo](https://www.archlinux.org/packages/?name=hwinfo) da **[community]**.
2.  Eseguire `hwinfo --framebuffer` da root.
3.  Utilizzare il codice corrispondente alla risoluzione desiderata.
4.  Utilizzare il codice a 6 cifre con prefisso 0x nell'opzione del kernel `vga=` in `menu.lst`. O convertirlo in decimale per evitare l'uso del prefisso 0x.

Esempio dell'output di **hwinfo**:

```
Mode 0x0364: 1440x900 (+1440), 8 bits
Mode 0x0365: 1440x900 (+5760), 24 bits

```

E la riga del kernel:

```
kernel /vmlinuz-linux root=/dev/sda1 ro **vga=0x0365**

```

**Note:** *vbetest* dà la modalità VESA a cui si deve aggiungere 512 per ottenere il valore corretto da utilizzare nella riga del kernel, mentre *hwinfo* dà direttamente il valore corretto necessario al kernel.

#### vbetest

1.  Installare il pacchetto [lrmi](https://aur.archlinux.org/packages/lrmi/) da [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)") contenente il tool **vbetest** (gli utenti x86_64 dovranno utilizzare [#hwinfo](#hwinfo) sotto).
2.  Avviare `vbetest` da root
3.  Prendere nota del numero in [ ] corrispondente alla risoluzione desiderata.
4.  Premere 'q' per uscire dal prompt interattivo di **vbetest**.
    1.  Come opzione, in una console come root, è possibile testare la modalità che appena scelta eseguendo `vbetest -m <yourcode>` e vedere un modello come [questo](http://www.phoronix.net/image.php?id=803&image=x_vbespy_5)
5.  Aggiungere **512** al valore preso in precedenza ed usare il valore complessivo per definire il parametro `vga=` nelle opzioni del kernel di `menu.lst`.
6.  Riavviare per godersi il risultato

Esempio di **vbetest** su un computer:

```
[356] 1440x900 (256 color palette)
[357] 1440x900 (8:8:8)

```

Quindi, il valore che si desidera è 357\. Poi, 357 + 512 = 869, quindi sarà necessario utilizzare **vga=869**. Aggiungere il valore alla fine della riga del kernel in `menu.lst` come indicato di seguito:

```
kernel /vmlinuz-linux root=/dev/sda1 ro vga=869

```

**Note:**

*   (8:8:8) is for 24-bit color (24bit is 32bit)
*   (5:6:5) is for 16-bit color
*   (5:5:5) is for 15-bit color

### Nominare le partizioni

#### Per etichetta

Se si altera (o si prevede di modificare) le dimensioni delle partizioni di tanto in tanto, potrebbe essere utile la definizione dei dispositivi e partizioni per mezzo delle etichette. È possibile assegnare delle etichette alle partizioni ext2, ext3, ext4 con:

```
e2label </dev/drive|partition> label

```

Il nome dell'etichetta può essere lungo fino a 16 caratteri, ma non deve avere spazi, altrimenti GRUB potrebbe non riconoscerlo. Infine, definirlo in `menu.lst`:

```
kernel /boot/vmlinuz-linux root=/dev/disk/by-label/Arch_Linux ro

```

#### Per UUID

Gli [UUID](/index.php/UUID "UUID") (Universally Unique IDentifier) di una partizione possono essere scoperti con il comando `blkid` o `ls -l /dev/disk/by-uuid`. Possono essere definiti in `menu.lst` così:

```
kernel /boot/vmlinuz-linux root=/dev/disk/by-uuid/<uuid number>

```

o

```
kernel /boot/vmlinuz-linux root=UUID=<uuid number>

```

### Eseguire il boot come root (single-user mode)

Quando appare il menù di GRUB, selezionare la voce che si desidera e premere il tasto `e`, aggiungere alle opzioni del kernel:

```
[...] single init=/bin/bash

```

ed eseguire il boot. Questo farà partire (solo per questa sessione) il kernel in *sigle-user mode* (init 1). Alla fine del processo di boot ci si troverà in un prompt di root senza che venga richiesta alcuna password.

Questo procedimento può essere utile ad esempio per cambiare la password di root. Tuttavia è una notevole "falla nella sicurezza" se non si ha impostato una [password a GRUB](#Protezione_con_password).

### Protezione con password

È possibile abilitare la protezione con password nel file di configurazione di GRUB per i sistemi operativi che si desidera avere protetti. La protezione tramite password al bootloader può essere richiesta se il BIOS non ha tale funzionalità e si ha bisogno di maggiore sicurezza.

In primo luogo, scegliere una password facile da ricordare e poi cifrarla:

```
# grub-md5-crypt
Password:
Retype password:
$1$ZOGor$GABXUQ/hnzns/d5JYqqjw

```

Poi aggiungere la password all'inizio del file di configurazione di GRUB (la password deve essere all'inizio del file di configurazione di GRUB per poter essere riconosciuta):

```
# general configuration
timeout   5
default   0
color light-blue/black light-cyan/blue

password --md5 $1$ZOGor$GABXUQ/hnzns/d5JYqqjw

```

**Nota:** Ricordare che grub usa come layout predefinito della tastiera lo standard qwerty.

Poi, per ogni sistema operativo che si desidera proteggere, aggiungere il comando `lock`:

```
# (0) Arch Linux
title  Arch Linux
lock
root   (hd0,1)
kernel /boot/vmlinuz-linux root=/dev/disk/by-label/Arch_Linux ro
initrd /boot/initramfs-linux.img
```

**Attenzione:** Se si disattiva l'avvio da altri dispositivi di avvio (come un disco CD) nelle impostazioni del BIOS, e poi si attivano con password tutte le voci dei sistemi operativi, potrebbe essere difficile riabilitare di nuovo i boot di tali sistemi se le password vengono dimenticate.

È comunque sempre possibile resettare il BIOS del proprio pc. Per farlo si dovrà seguire la documentazione della propria scheda madre (che è specifica del modello usato).

### Riavviare con la scelta nominale di boot

Spesso la necessità di passare ad un altro sistema operativo non-predefinito (ad esempio Windows), dover riavviare e attendere che il menu di GRUB appaia è noioso. GRUB offre un modo per registrare la scelta del sistema operativo al riavvio invece di aspettare il menu, designando un nuovo default temporaneo, che verrà ripristinato non appena usato.

Supponendo una semplice configurazione `menu.lst` come questa:

```
/boot/grub/menu.lst

```

```
# general configuration:
timeout 10
default 0
color light-blue/black light-cyan/blue

# (0) Arch
title  Arch Linux
root (hd0,1)
kernel /boot/vmlinuz-linux root=/dev/disk/by-label/ARCH ro
initrd /boot/initramfs-linux.img

# (1) Windows
title Windows XP
rootnoverify (hd0,0)
makeactive
chainloader +1

```

Arch è l'impostazione predefinita (0). Si vuole riavviare Windows. Cambiare `default 0` a `default saved`. Questo registra il default corrente in un file di `default` nella directory di GRUB quando è usato il comando **savedefault**. A questo punto aggiungere la riga `savedefault 0` al fondo della voce di Windows. Ogni volta che Windows viene avviato, sarà reimpostato il valore predefinito di Arch, rendendo quindi provvisorio, il default di Windows.

Ora tutto quello che serve è un modo per cambiare facilmente il default manualmente. Ciò può essere eseguito utilizzando il comando `grub-set-default`. Quindi, per riavviare Windows, eseguire il seguente comando:

 `$ sudo grub-set-default 1 && sudo shutdown -r now` 

Per facilità d'uso, potrebbe essere comodo abilitare "[Allow user to shutdown](/index.php/Allow_users_to_shutdown_(Italiano) "Allow users to shutdown (Italiano)") fix" (includendo `/sbin/grub-set-default` tra i comandi sono consentite all'utente le operazioni di spegnimento senza dover fornire la password).

### Interazione LILO e GRUB

Se il pacchetto [LILO](/index.php/LILO "LILO") è installato sul sistema, rimuoverlo con

 `# pacman -R lilo` 

Alcuni tipi di attività (ad esempio, la compilazione del kernel usando `make all`), effettuano una richiamata a LILO, che potrebbe pertanto essere sovrascritto su GRUB. LILO può essere stato incluso nel sistema di base, a seconda della versione dell'installer o se è stato selezionato/deselezionato durante la fase di selezione dei pacchetti.

**Note:** `pacman-R lilo` potrebbe non rimuovere LILO dal MBR se vi è stato installato, ma si limiterà a rimuovere il pacchetto [lilo](https://aur.archlinux.org/packages/lilo/). LILO verrà sovrascritto definitivamente quando sarà reinstallato GRUB (o un altro bootloader).

### GRUB boot disk

In primo luogo, formattare un disco floppy:

```
 fdformat /dev/fd0
 mke2fs /dev/fd0

```

Ora montare il disco:

```
 mount -t ext2 /dev/fd0 /mnt/fl

```

Installare GRUB sul disco:

```
 grub-install --root-directory=/mnt/fl '(fd0)'

```

Copiare il file `menu.lst` sul disco:

```
 cp /boot/grub/menu.lst /mnt/fl/boot/grub/menu.lst

```

Infine, smontare il floppy:

```
 umount /mnt/fl

```

Ora si dovrebbe essere in grado di riavviare il computer con il disco nel lettore e si dovrebbe avviare GRUB. Assicurarsi ovviamente, che il floppy sia impostato per avere la priorità d'avvio rispetto gli altri dispositivi nel BIOS.

Consultare inoltre: [Super GRUB Disk](http://www.supergrubdisk.org/)

### Nascondere il menu di GRUB

L'opzione `hiddenmenu` può essere usata per nascondere il menu di default. Nascondendo il menu viene automaticamente selezionata la voce di default appena trascorso il tempo impostato. Per mostrare il menu sarà sufficiente premere `Esc`. Per usare questa caratteristica è sufficiente aggiungere la seguente riga a `/boot/grub/menu.lst`:

```
hiddenmenu

```

## Modalità debug avanzata

L'intera sezione è in [Boot debugging (Italiano)](/index.php/Boot_debugging_(Italiano) "Boot debugging (Italiano)")

## Risoluzione dei problemi

### GRUB Errore 17

**Note:** La soluzione qui illustrata funziona anche per il "GRUB Error 15"

**Il primo controllo da fare è scollegare qualsiasi unità esterna. Sembra ovvio, ma a volte capita!)**

Se la tabella delle partizioni non è ben configurata, uno spiacevole messaggio "GRUB error 17" potrebbe essere l'unica cosa che vi apparirà al seguente riavvio. Ci sono un certo numero di motivi per cui la tabella delle partizioni potrebbe risultare disordinata. Comunemente, gli utenti che manipolano le partizioni con [GParted](/index.php/GParted "GParted") (le unità logiche in particolare) possono invertire l'ordine delle partizioni. Ad esempio, eliminando `/dev/sda6` e ridimensionando `/dev/sda7`, per poi ricreare quello che era `/dev/sda6`, ed ottenendolo tuttavia in fondo alla lista, come `/dev/sda9`. Anche se l'ordine fisico delle partizioni/unità logiche, non è cambiata, lo è l'ordine in cui vengono riconosciute.

La correzione della tabella delle partizioni è un'operazione facile. Basta avviare il sistema dal cd di Arch, eseguire il login come root e modificare adeguatamente la tabella delle partizioni:

```
# fdisk /dev/sda

```

Una volta selezionata la partizione, immettere [**x**] per la modalità extra/expert, [**f**] per correggere l'ordine delle partizioni, ed infine [**w**] per sovrascrivere la tabella delle partizioni e uscire.

È possibile verificare che la tabella delle partizioni è stata correttamente modificata con `fdisk -l`. Ora c'è solo bisogno di verificare GRUB. Consultare la sezione[#Installazione del bootloader](#Installazione_del_bootloader) sopra.

Fondamentalmente si deve istruire GRUB sul percorso corretto del file `/boot` e poi riscrivere GRUB nel [MBR](/index.php/MBR "MBR") del disco.

Per esempio:

```
# grub

```

```
grub> root (hd0,6)
grub> setup (hd0)
grub> quit

```

Consultare [questa pagina](http://stringofthoughts.wordpress.com/2009/05/24/grub-error-17-debianubuntu) per una sintesi più approfondita di questa sezione.

### /boot/grub/stage1 not read correctly

Se appare messaggio di errore durante il tentativo di setup del grub e non si utilizza una tabella delle partizioni aggiornata, vale la pena eseguire un controllo.

```
# fdisk -l /dev/sda

```

Questo mostrerà la tabella delle partizioni per /dev/sda. Quindi controllare qui, anche se i valori "Id" delle partizioni dovessero essere corretti. La colonna "System" mostrerà la descrizione dei valori "Id".

Se la partizione di avvio è segnata come "HPFS/NTFS", per esempio, allora si deve cambiare con "Linux". Per fare questo, dare il comando fdisk

```
# fdisk /dev/sda

```

cambiare l'Id del sistema di una partizione con [t], selezionare il numero e tipo di partizione nel nuovo id di sistema (Linux = 83). È anche possibile vedere tutti gli ID di sistema disponibili digitando "L" invece di system id.

Se si cambia l'Id di sistema di qualche partizione, bisognerebbe [v]erificare la tabella delle partizioni prima di confermare [w]rite.

Ora si può provare a installare grub di nuovo.

[Qui](https://bbs.archlinux.org/viewtopic.php?pid=799930) c'è un post nel forum che riporta il problema.

### Installazione accidentale in una partizione Windows

Se accidentalmente si installa GRUB sulla partizione Windows, GRUB scriverà alcune informazioni al settore di avvio della partizione, cancellando il riferimento al bootloader di Windows. (Questo è vero per NTLDR, il bootloader di Windows XP e precedenti, non troppo sicuro per le versioni successive).

Per risolvere questo problema è necessario utilizzare la console di ripristino di Windows per la propria versione. Poiché molti produttori di computer non includono questa funzionalità nel loro prodotto (molti scelgono di utilizzare una partizione di ripristino), Microsoft ne ha reso disponibile il download. Se si utilizza XP, consultare [questa pagina](http://tips.vlaurie.com/2006/05/recovery-console-for-those-without-an-xp-disk/) per essere in grado di avviare i dischi floppy come un CD di ripristino. Avviare il CD di ripristino (o attivare la modalità di ripristino di Windows) ed eseguire fixboot per riparare il settore di avvio della partizione. Per ultimo, sarà necessario installare nuovamente GRUB (questa volta nel MBR, e non nella partizione di Windows) per avviare Linux.

Consultare [ulteriori discussioni qui](/index.php/MBR#Restoring_a_Windows_boot_record "MBR").

### Modificare le voci GRUB nel menu di avvio

Dopo aver selezionato una voce dal menu di avvio, è possibile modificarla premendo il tasto `e`. Usare la tab-completion (scheda di completamento) se si ha bisogno di rilevare altri dispositivi, quindi `Esc` per uscire. Allora si può provare ad avviare premendo `b`.

**Nota:** Queste impostazioni **non verranno salvate**.

### Errore device.map

Se viene generato un errore che riporta `/boot/grub/device.map` durante l'installazione o l'avvio, eseguire:

```
# grub-install --recheck /dev/sda

```

per forzare GRUB a ricontrollare la mappa dei dispositivi, anche se esiste già. Questo può essere necessario dopo il ridimensionamento delle partizioni o l'aggiunta/rimozione di dischi.

### Errore sotto-menu di KDE al riavvio

Se dopo l'apertura di un sotto-menu con l'elenco di tutti i sistemi operativi configurati in GRUB, e la conseguente selezione, al riavvio è nuovamente attivo il sistema operativo predefinito, allora si dovrebbe controllare di avere la riga:

```
default saved

```

in `/boot/grub/menu.lst`.

### GRUB non riesce a trovare o installare qualsiasi virtio /dev/vd* o altri dispositivi non-BIOS

Esempio di problemi all'installazione di GRUB, quando si installa Arch Linux in una macchina KVM virtuale utilizzando un dispositivo virtio per hard disk. Per installare GRUB, procedere come segue: Inserire una console virtuale digitando `Ctrl` + `Alt` + `F2` o qualsiasi altro tasto F per una console virtuale libera. Supponendo che il file system root sia montato nella cartella `/mnt` e il file di avvio del sistema sia montato o memorizzato nella cartella `/mnt/boot`.

1\. Verificare che tutti i file di GRUB necessari siano presenti nella directory di avvio (supponendo siano montati nella cartella `/mnt/boot`) con il comando:

```
# ls /mnt/boot/grub

```

2\. Se la cartella `/mnt/boot/grub` contiene già tutti i file necessari, saltare al passo 3\. In caso contrario, effettuare i seguenti comandi (sostituendo `/mnt`, il `kernel` e l'`initrd` con i percorsi reali e nomi dei file). Si dovrebbe anche avere il file `menu.lst` scritto nella cartella:

```
# mkdir -p /mnt/boot/grub                # if the folder is not yet present
# cp -r /boot/grub/stage1 /boot/grub/stage2 /mnt/boot/grub
# cp -r your_kernel your_initrd /mnt/boot

```

3\. Avviare la shell di GRUB con il seguente comando:

```
# grub --device-map=/dev/null

```

4\. Immettere i seguenti comandi, sostituendo `/dev/vda`, e `(hd0,0)` con il dispositivo corretto e la partizione corrispondente alla propria installazione.

```
device (hd0) /dev/vda
root (hd0,0)
setup (hd0)
quit

```

5\. Se GRUB non riporta nessun messaggio di errore, probabilmente l'operazione è andata a buon fine. Potrebbe inoltre essere necessario aggiungere gli opportuni moduli a ramdisk. Per ulteriori informazioni, si prega di consultare la guida KVM su [Preparing Arch Linux guest](/index.php/KVM#Preparing_an_.28Arch.29_Linux_guest "KVM")

## Risorse esterne

*   [GNU GRUB](http://www.gnu.org/software/grub/)
*   [GRUB Grotto](http://www.troubleshooters.com/linux/grub/index.htm)
*   [Guida agli errori di GRUB](http://linuxmx.it/guide-linux/14-generiche/222-analizziamo-gli-errori-di-grub.html)
*   [Boot Debug](/index.php/Boot_debugging_(Italiano) "Boot debugging (Italiano)") - Debug con GRUB.