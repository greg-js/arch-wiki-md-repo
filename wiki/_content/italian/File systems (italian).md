Articoli correlati

*   [Partizionamento](/index.php/Partitioning_(Italiano) "Partitioning (Italiano)")

Da [Wikipedia](https://en.wikipedia.org/wiki/it:File_system "wikipedia:it:File system"):

	*In informatica, un file system è, informalmente, un meccanismo con il quale i file sono immagazzinati e organizzati su un dispositivo di archiviazione, come un disco rigido o un CD-ROM. Più formalmente, un file system è l'insieme dei tipi di dati astratti necessari per la memorizzazione, l'organizzazione gerarchica, la manipolazione, la navigazione, l'accesso e la lettura dei dati. Di fatto, alcuni file system (come NFS) non interagiscono direttamente con i dispositivi di archiviazione.*

Ogni singola partizione del disco può essere configurata utilizzando uno dei tanti file system disponibili. Ognuno ha i propri vantaggi, svantaggi, e idiosincrasie uniche. Segue una breve panoramica dei filesystem supportati, i link puntano alle pagine di wikipedia che forniscono molte più informazioni:

Prima di essere formattato, un disco deve essere [partizionato](/index.php/Partitioning_(Italiano) "Partitioning (Italiano)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Tipi di File System](#Tipi_di_File_System)
    *   [1.1 Journaling](#Journaling)
    *   [1.2 Supporto su Arch Linux](#Supporto_su_Arch_Linux)
*   [2 Formattare un dispositivo](#Formattare_un_dispositivo)
    *   [2.1 Requisiti](#Requisiti)
    *   [2.2 Strumenti da console](#Strumenti_da_console)
    *   [2.3 Strumenti ad interfaccia grafica](#Strumenti_ad_interfaccia_grafica)

## Tipi di File System

*   [Btrfs](https://en.wikipedia.org/wiki/Btrfs "wikipedia:Btrfs") - Conosciuto anche come "Better FS", **Btrfs** è un nuovo filesystem con notevoli e potenti caratteristiche, simili all'eccellente ZFS sviluppato da Sun/Oracle. Questi comprendono la creazione di istantanee (snapshots), lo striping e mirroring multi-disco (RAID software fondamentalmente senza mdadm), checksuming, backup incrementale, e la compressione on-the-fly integrata, che può dare un impulso significativo delle prestazioni, nonché di risparmiare spazio. A partire da gennaio 2011 Btrfs è ancora considerato "instabile" anche se è stato inserito nella ramo principale del kernel con uno stato sperimentale. Btrfs sembra essere il futuro del filesystem di GNU/Linux, ed è presente come scelta opzionale per il filesystem di root nelle installazioni delle maggiori distribuzioni.
*   [exFAT](https://en.wikipedia.org/wiki/exFAT "wikipedia:exFAT") - **File system di Microsoft ottimizzata per le unità flash**. A differenza di NTFS, exFAT non può pre-allocare lo spazio su disco per un file da solo, segnando lo spazio sul disco arbitrariamente come 'assegnato'. Come in FAT, quando si crea un file di lunghezza nota, exFAT deve eseguire una completa scrittura fisica pari alla dimensione del file.
*   [ext2](https://en.wikipedia.org/wiki/it:ext2 "wikipedia:it:ext2") - **Second Extended Filesystem**- È un filesystem GNU/Linux maturo e molto stabile, ma ha l'inconveniente di non avere il supporto al *journaling* e ai "Barriers". L'assenza del supporto al journaling può causare la perdita di dati in caso di mancanza di corrente o di un crash di sistema. Può essere **sconveniente** utilizzarlo per le partizioni root (`/`) e `/home`, e ciò è dovuto al suo controllo dell'integrità molto lungo. Un filesystem ext2 può facilmente essere [convertito in ext3](/index.php/Convert_ext2_to_ext3 "Convert ext2 to ext3").
*   [ext3](https://en.wikipedia.org/wiki/ext3 "wikipedia:ext3") - **Third Extended Filesystem**- Essenzialmente è il file system ext2, ma con il supporto per il journaling e alla scrittura dei barrier. Ext3 è completamente compatibile con Ext2 ed è ben collaudato ed estremamente stabile.
*   [ext4](https://en.wikipedia.org/wiki/ext4 "wikipedia:ext4") - **Fourth Extended Filesystem**- É un filesystem più recente ed è retro-compatibile con le versioni ext2 ed ext3\. Introduce il supporto per i volumi con dimensioni fino a 1 exabyte(cioè 1.048.576 terabyte) e file con dimensioni fino a 16 terabyte. Aumenta il limite da 32.000 sottodirectory di ext3 a 64.000\. Offre capacità di deframmentazione in linea.
*   [F2FS](https://en.wikipedia.org/wiki/F2FS "wikipedia:F2FS") - **Flash-Friendly File System** è un file system per supporti flash creato da Kim Jaegeuk (Hangul:김재극) da Samsung per il kernel del sistema operativo Linux. La motivazione per F2FS era quello di costruire un file system che da subito prende in considerazione le caratteristiche dei dispositivi di memoria NAND flash memory-based (come ad esempio i dischi a stato solido, eMMC, e schede SD), che sono ampiamente in uso nei sistemi dei computer che vanno dai dispositivi mobili ai server .
*   [JFS](https://en.wikipedia.org/wiki/it:JFS "wikipedia:it:JFS") - É il **FilesySystem journaling** di IBM. JFS è stato il primo filesystem ad offrire il journaling, ed è stato impiegato per molti anni nel sistema operativo IBM AIX® prima di accedere a GNU/Linux. JFS è il filesystem che occupa meno risorse CPU tra tutti quelli disponibili per GNU/Linux. Veloce nella formattazione, montaggio e controllo integrità (fsck). JFS offre ottime prestazioni in generale, specialmente in associazione con il "deadline I/O scheduler".) Non così largamente supportato come i filesystem Ext o ReiserFS, ma ben collaudato e stabile.
    **Nota:** Si noti che il filesystem JFS non può essere ridimensionato tramite utility come **gparted**.

*   [NILFS2](https://en.wikipedia.org/wiki/NILFS "wikipedia:NILFS") - **New Implementation of a Log-structured File System** (Nuova implementazione di un file system con struttura a log), è stato sviluppato da NTT. Si registrano tutti i dati in un formato continuo simile ad un file-log che subisce solo aggiunte e non è mai sovrascritto. È stato progettato per ridurre i tempi di ricerca e minimizzare il tipo di perdita di dati che si verifica dopo un incidente con i tradizionali filesystem Linux.
*   [NTFS](https://en.wikipedia.org/wiki/NTFS "wikipedia:NTFS") - **File System utilizzato da Windows**. NTFS ha diversi miglioramenti tecnici rispetto FAT e HPFS (High Performance File System), come il supporto migliorato per i metadati, l'uso di strutture dati avanzate per migliorare le prestazioni, l'affidabilità e l'utilizzo dello spazio su disco, più estensioni aggiuntive, come le liste per il controllo di accesso di sicurezza ( ACL ) e journaling del file system .
*   [Reiser4](https://en.wikipedia.org/wiki/Reiser4 "wikipedia:Reiser4") - **Successore del file system ReiserFS**, sviluppato da zero da Namesys e sponsorizzato dalla DARPA e Linspire, utilizza B*-trees in combinazione con l'impostazione di bilanciamento dell'albero delle directory, in cui non saranno fusi nodi sotto-popolate fino a quando non si effettua un flush su disco, se non sotto la pressione di memoria o a termine di una transazione. Tale sistema permette anche a ReiserFS4 di creare file e directory senza dover perdere tempo e lo spazio attraverso blocchi fissi.
*   [ReiserFS](https://en.wikipedia.org/wiki/ReiserFS "wikipedia:ReiserFS") - Il **file system con journaling (v3) ad alte prestazioni di Hans Reiser** usa un metodo di manipolazione dati molto interessante, basato su un algoritmo non convenzionale e creativo. ReiserFS è pubblicizzato come molto veloce, soprattutto nella gestione di molti file di piccole dimensioni. ReiserFS è veloce per quanto riguarda la formattazione, ma relativamente lento nel montaggio. Da considerarsi maturo e stabile, ReiserFS(V3) non è più attivamente sviluppato in questo momento. In genere rappresenta una buona scelta per le partizioni `/var`.
*   [Swap](https://en.wikipedia.org/wiki/Paging "wikipedia:Paging") - Filesystem utilizzato per le partizioni di swap.
*   [VFAT](https://en.wikipedia.org/wiki/File_Allocation_Table#VFAT "wikipedia:File Allocation Table") - **Virtual File Allocation Table** è tecnicamente semplice e supportato da quasi tutti i sistemi operativi esistenti. Questo lo rende un formato utile per le solid-state memory card ed è pratico per condividere dati tra i sistemi operativi.
*   [XFS](https://en.wikipedia.org/wiki/it:XFS "wikipedia:it:XFS") - **Uno dei primi filesystem con journaling, sviluppato originariamente da Silicon Graphics** per il sistema operativo IRIX e portato poi su GNU/Linux. XFS offre una gestione molto veloce su file di grandi dimensioni, ed è un filesystem molto veloce in fase di formattazione e montaggio. Test di benchmark comparativi hanno evidenziato di essere più lento quando lavora con molti file di piccole dimensioni. XFS è ben collaudato e supporta servizi di deframmentazione online.
*   [ZFS](https://en.wikipedia.org/wiki/ZFS "wikipedia:ZFS") - **File system combinato e logical volume manager progettato da Sun Microsystems**. Le caratteristiche di ZFS comprendono la protezione contro il danneggiamento dei dati, il supporto per elevate capacità di memorizzazione, l'integrazione dei concetti di filesystem e la gestione del volume, snapshot e clonazione copy-on-write, il controllo dell'integrità continuo e la riparazione automatica, RAID-Z e ACL NFSv4 nativo.

### Journaling

Tutti i filesystem sopra citati, ad eccezione di ext2, FAT16/32, utilizzano il [journaling](https://en.wikipedia.org/wiki/it:Journaling "wikipedia:it:Journaling"). I file system con journaling, utilizzano un "diario" per registrare le modifiche prima che queste siano inviate al file system. Nel caso di un crash del sistema o di una interruzione di corrente tale procedura è più veloce per riportare on-line il sistema e a meno probabilità di avere perdita di dati o di essere danneggiato.

Non tutte le tecniche di journaling sono uguali: in particolare, solo ext3 ed ext4 si avvalgono della modalità *data-mode*, che annota sia i **dati** che i **meta-dati**. Il journaling in modalità Data-mode soffre di una penalizzazione di velocità significativa e non è abilitata di default. Gli altri filesystem supportano unicamente la modalità *ordered-mode-journaling*, che registra solo i meta-dati. Mentre tutti i journaling restituiranno un filesystem ad uno stato valido dopo un crash, il journaling in modalità Data-mode offre la massima protezione contro la corruzione e la perdita di dati. Vi è quindi un compromesso in termini di prestazioni del sistema in quanto il journaling in modalità data-mode effettua due operazioni di scrittura: prima al journaling e poi al disco. Il [Trade-off](https://en.wikipedia.org/wiki/it:Trade-off "wikipedia:it:Trade-off") tra la velocità del sistema e la sicurezza dei dati deve essere preso in considerazione quando si sceglie il tipo di filesystem.

### Supporto su Arch Linux

*   **btrfs-progs** — Supporto [Btrfs](/index.php/Btrfs "Btrfs").

	[http://btrfs.wiki.kernel.org/](http://btrfs.wiki.kernel.org/) || [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs)

*   **dosfstools** — Supporto VFAT.

	[http://www.daniel-baumann.ch/software/dosfstools/](http://www.daniel-baumann.ch/software/dosfstools/) || [dosfstools](https://www.archlinux.org/packages/?name=dosfstools)

*   **exfat-utils** — Supporto exFAT.

	[http://code.google.com/p/exfat/](http://code.google.com/p/exfat/) || [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils)

*   **f2fs-tools** — Supporto [F2FS](/index.php/F2FS "F2FS").

	[https://git.kernel.org/cgit/linux/kernel/git/jaegeuk/f2fs-tools.git](https://git.kernel.org/cgit/linux/kernel/git/jaegeuk/f2fs-tools.git) || [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools)

*   **fuse-exfat** — Supporto per il montaggio exFAT.

	[http://code.google.com/p/exfat/](http://code.google.com/p/exfat/) || [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils)

*   **e2fsprogs** — Supporto per ext2, [ext3](/index.php/Ext3 "Ext3"), [ext4](/index.php/Ext4 "Ext4").

	[http://e2fsprogs.sourceforge.net](http://e2fsprogs.sourceforge.net) || [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs)

*   **jfsutils** — Supporto [JFS](/index.php/JFS "JFS").

	[http://jfs.sourceforge.net](http://jfs.sourceforge.net) || [jfsutils](https://www.archlinux.org/packages/?name=jfsutils)

*   **nilfs-utils** — Supporto NILFS.

	[http://www.nilfs.org/](http://www.nilfs.org/) || [nilfs-utils](https://www.archlinux.org/packages/?name=nilfs-utils)

*   **ntfs-3g** — Supporto [NTFS](/index.php/NTFS "NTFS").

	[http://www.tuxera.com/community/ntfs-3g-download/](http://www.tuxera.com/community/ntfs-3g-download/) || [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g)

*   **reiser4progs** — Supporto [ReiserFSv4](/index.php/Reiser4 "Reiser4").

	[http://sourceforge.net/projects/reiser4/](http://sourceforge.net/projects/reiser4/) || [reiser4progs](https://aur.archlinux.org/packages/reiser4progs/)

*   **reiserfsprogs** — Supporto ReiserFSv3.

	[https://www.kernel.org/](https://www.kernel.org/) || [reiserfsprogs](https://www.archlinux.org/packages/?name=reiserfsprogs)

*   **util-linux** — Supporto [Swap](/index.php/Swap "Swap").

	[http://www.kernel.org/pub/linux/utils/util-linux/](http://www.kernel.org/pub/linux/utils/util-linux/) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

*   **xfsprogs** — Supporto [XFS](/index.php/XFS "XFS").

	[http://oss.sgi.com/projects/xfs/](http://oss.sgi.com/projects/xfs/) || [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs)

*   **zfs** — Supporto [ZFS](/index.php/ZFS "ZFS").

	[http://zfsonlinux.org/](http://zfsonlinux.org/) || [zfs](https://aur.archlinux.org/packages/zfs/)

*   **zfs-fuse** — [Supporto ZFS via FUSE](/index.php/ZFS_on_FUSE "ZFS on FUSE").

	[http://zfs-fuse.net/](http://zfs-fuse.net/) || [zfs-fuse](https://aur.archlinux.org/packages/zfs-fuse/)

**Nota:** Il filesystem ZFS non può essere ridimensionato da utility per la gestione del disco come gparted.

## Formattare un dispositivo

**Attenzione:** Formattando un dispositivo, si rimuove qualsiasi cosa sia contenuta in esso, assicurarsi di effettuare un back up per i dati che si intende conservare.

### Requisiti

Prima di continuare bisogna conoscere come vengono nominati i dispositivi su Linux. Hard disk e chiavette USB vengono mostrate come `/dev/sd*x*`, dove "x" è una lettera minuscola, mentre le partizioni vengono mostrate come `/dev/sd*xY*`, dove "Y" è un numero.

Se il dispositivo che si desidera formattare è montato, verrà visualizzato nella colonna *MOUNTPOINT* da:

```
$ lsblk

```

Per montare il vostro dispositivo:

```
# mount /dev/sd*xY* /some/directory

```

Per smontarlo è possibile utilizzare *umount* sul disco dove è montata la directory:

```
# umount /some/directory

```

**Nota:** Per formattare e creare una nuovo file system, il vostro dispositivo deve essere smontato.

Manipolare la tabella delle partizioni in base alle vostre esigenze. Per questo si può utilizzare **fdisk** per MBR o **gdisk** per GPT, oppure [tool grafici](#GUI_tools). Si veda la pagina sul [partizionamento](/index.php/Partitioning_(Italiano) "Partitioning (Italiano)") per maggiori informazioni.

Ora è possibile creare nuovi file system attraverso strumenti da console o tramite strumenti ad interfaccia grafica .

### Strumenti da console

Per creare un file system è sufficiente utilizzare *mkfs*, che altro non è che un front-end unificato per i differenti tool `mkfs.*fstype*`. Esempio:

```
 # mkfs -t ext4 /dev/*partizione*

```

Per creare un file di swap, utilizzare il comando **mkswap**:

```
# mkswap /dev/*partitizione*

```

### Strumenti ad interfaccia grafica

Esistono diverse GUI per la gestione del partizionamento:

*   **[GParted](/index.php/GParted "GParted")** — Clone GTK+ di Partition Magic, frontend di GNU Parted.

	[http://gparted.sourceforge.net](http://gparted.sourceforge.net) || [gparted](https://www.archlinux.org/packages/?name=gparted)

*   **gnome-disk-utility** — Utility per la gestione del disco parte del desktop GNOME.

	[http://www.gnome.org](http://www.gnome.org) || [gnome-disk-utility](https://www.archlinux.org/packages/?name=gnome-disk-utility)

*   **KDE Partition Manager** — Utility per KDE che permette di gestire le unità disco, le partizioni e i file system.

	[https://sourceforge.net/projects/partitionman/](https://sourceforge.net/projects/partitionman/) || [partitionmanager](https://www.archlinux.org/packages/?name=partitionmanager)