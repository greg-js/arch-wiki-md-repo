La clonazione del disco è il processo di creare un'immagine di una partizione o di un intero disco rigido. Ciò può tornare utile sia per copiare il disco su un altro computer, sia per finalità di backup\recupero dei dati.

## Contents

*   [1 Usando dd](#Usando_dd)
    *   [1.1 Clonare una partizione](#Clonare_una_partizione)
    *   [1.2 Clonare un intero hard disk](#Clonare_un_intero_hard_disk)
    *   [1.3 Backup del MBR](#Backup_del_MBR)
    *   [1.4 Creare l'immagine di un disco](#Creare_l.27immagine_di_un_disco)
    *   [1.5 Ripristinare il sistema](#Ripristinare_il_sistema)
*   [2 Usando cp](#Usando_cp)
*   [3 Software per la clonazione del disco](#Software_per_la_clonazione_del_disco)
    *   [3.1 Clonazione del disco in Arch](#Clonazione_del_disco_in_Arch)
    *   [3.2 Clonazione del disco all'infuori di Arch](#Clonazione_del_disco_all.27infuori_di_Arch)
*   [4 Link esterni](#Link_esterni)

### Usando dd

Il comando `dd` è un semplice, versatile e potente strumento. Può essere usato per copiare dalla sorgente alla destinazione, blocco per blocco, a prescindere dal tipo di filesystem oppure dal sistema operativo. Un metodo più conveniente è quello di usare `dd` da un ambiente live, come un livecd.

**Attenzione:** Data la natura di questi comandi, è bene essere molto cauti nel loro utilizzo; questi comandi possono distruggere i vostri dati. Ricordare che l'ordine è file di input (if=) e file di output (of=) e non invertiteli! Assicurarsi sempre che il disco/partizione di destinazione (of=) sia uguale o più grande dell'origine (if=).

#### Clonare una partizione

Da un disco fisico `/dev/sda`, la partizione 1, ad un disco fisico `/dev/sdb` sulla partizione 1.

```
dd if=/dev/sda1 of=/dev/sdb1 bs=4096 conv=notrunc,noerror

```

Se il file di output ***`of`*** (`sdb1` nel nostro esempio) non esiste, `dd` lo creerà a partire dall'inizio del disco.

#### Clonare un intero hard disk

Da un dico fisico `/dev/sda` ad un disco fisico `/dev/sdb`:

```
dd if=/dev/sda of=/dev/sdb bs=4096 conv=notrunc,noerror

```

Questo comando clonerà l'intero disco, incluso il [Master Boot Record](/index.php/Master_Boot_Record_(Italiano) "Master Boot Record (Italiano)") (e quindi anche il bootloader), tutte le partizioni ed i dati.

*   `notrunc` o `do not truncate` mantiene l'integrità dei dati imponendo a `dd` di non spezzare nessun dato.
*   `noerror` comunica a `dd` di continuare l'operazione, ignorando tutti gli errori dall'origine. Il comportamento di default di `dd` è quello di fermarsi ad ogni errore.
*   `bs=4096` imposta la dimensione dei blocchi a 4k, la dimensione ottimale ed efficiente per la lettura/scrittura del disco, e quindi della velocità clonazione.

#### Backup del MBR

Il [Master Boot Record](/index.php/Master_Boot_Record_(Italiano) "Master Boot Record (Italiano)") è contenuto nei primi 512 byte del disco. Esso consiste in 3 parti:

1.  I primi 446 byte contengono il bootloader.
2.  I successivi 64 contengono la tavola delle partizioni (4 voci di 16 byte ciascuna, una voce per ogni partizione primaria).
3.  Gli ultimi 2 byte contengono un identificatore.

Per salvare il MBR in un file dal nome `mbr.img`:

```
  # dd if=/dev/hda of=/mnt/sda1/mbr.img bs=512 count=1

```

Per ripristinare (attenzione questo comando potrebbe distruggere la tavola delle partizioni, e quindi impedire l'accesso ai dati presenti sul disco):

```
  # dd if=/mnt/sda1/mbr.img of=/dev/hda

```

Se si desidera soltanto ripristinare il bootloader, ma non la tavola delle partizioni, basterà ripristinare solo i primi 446 byte del MBR:

```
  # dd if=/mnt/sda1/mbr.img of=/dev/hda bs=446 count=1

```

Per ripristinare soltanto la tavola delle partizioni, il comando sarà:

```
  # dd if=/mnt/sda1/mbr.img of=/dev/hda bs=1 skip=446 count=64

```

Sarà possibile estrarre il MBR dall'immagine completa di un disco:

```
  #dd if=/path/to/disk.img of=/mnt/sda1/mbr.img bs=512 count=1

```

#### Creare l'immagine di un disco

1\. Effettuare il boot da un sistema live(liveCD o liveUSB).

2\. Assicurarsi che nessuna partizione sia montata dal disco di origine.

3\. Effettuare il mount di un disco esterno.

4\. Effettuare il backup del disco:

```
 # dd if=/dev/hda conv=sync,noerror bs=64K | gzip -c  > /mnt/sda1/hda.img.gz

```

5\. Salvare alcune informazioni addizionali riguardo al disco, come la sua geometria, sarà necessario per interpretare la tavola delle partizioni salvata nell'immagine. L'informazione più importante è la dimensione dei cilindri.

```
 # fdisk -l /dev/hda > /mnt/sda1/hda_fdisk.info

```

**Nota:** Sarà possibile usare un valore di dimensione dei blocchi (`bs=`) uguale all'ammontare della cache del disco di cui si sta creando l'immagine. Ad esempio, `bs=8192K` funziona per una cache di 8MB. Il valore di 64K menzionato in questo articolo è migliore del valore di default, che è impostato a `bs=512` byte, perché `dd` verrà eseguito più velocemente con un valore di `bs=` maggiore.

#### Ripristinare il sistema

Per ripristinare il sistema:

```
 # gunzip -c /mnt/sda1/hda.img.gz | dd of=/dev/hda

```

### Usando cp

Il programma `cp` può essere usato per clonare un disco, ad una partizione alla volta. Il vantaggio dell'uso di `cp` è che il tipo di filesystem della/delle partizione/i di destinazione può non essere il solito dell'origine. Per sicurezza, effettuare il processo da un ambiente live.

La procedura di base da un ambiente live sarà:

*   Creare le nuove partizioni di destinazione (usando fdisk, cfdisk oppure altri programmi disponibili nell'ambiente live).
*   Creare un filesystem su ogni partizione precedentemente creata. Ad esempio:

```
mkfs -t ext3 /dev/sdb1

```

*   Effettuare il mount dell'origine e della/delle partizione/partizioni di destinazione. Ad esempio:

```
mount -t ext3 /dev/sda1 /mnt/origine
mount -t ext3 /dev/sdb1 /mnt/destinazione

```

*   Copiare i file dalla partizione di origine a quella di destinazione:

```
cp -a /mnt/origine/* /mnt/destinazione

```

L'opzione **`-a`**: preserva i permessi, non segue mai i link simbolici ed copia ricorsivamente

*   Cambiare i punti di mount della partizione appena copiata nel file `/etc/fstab` a seconda delle modifiche effettuate(es. il tipo di filesystem)
*   Infine, installare il bootloader GRUB se necessario. (Consultare [GRUB](/index.php/GRUB_(Italiano) "GRUB (Italiano)"))

## Software per la clonazione del disco

### Clonazione del disco in Arch

Il programma ncurses [PartImage](https://en.wikipedia.org/wiki/Partimage "wikipedia:Partimage") è nel repository community. La sua interfaccia non è eccezionalmente intuitiva, ma funziona. Non ci sono attualmente programmi di clonazione con interfaccia grafica GTK\QT per Linux. Un'altra opzione è quella di utilizzare il comando `dd`, una piccola utility per creare file immagine. Wikipedia ha una lista delle varie versioni di dd, specificatamente orientate a questo tipo di scopo. [wikipedia:Dd_(Unix)#Recovery-oriented_variants_of_dd](https://en.wikipedia.org/wiki/Dd_(Unix)#Recovery-oriented_variants_of_dd "wikipedia:Dd (Unix)"). [dd_rescue](http://www.garloff.de/kurt/linux/ddrescue/) funziona efficientemente con dischi guasti copiando prima le aree prive di errori e successivamente ritentando le aree con errori.

### Clonazione del disco all'infuori di Arch

Se desiderate fare un backup o installare in serie la vostra installazione-tipo di Arch, probabilmente fareste meglio ad usare un altro pc e clonare il disco da li. Alcuni suggerimenti:

*   [PartedMagic](http://partedmagic.com/doku.php?id=start) ha un bel live cd/usb con PartImage ed altri strumenti per il recupero dati.
*   [Mindi](http://www.mondorescue.org/) è una distribuzione Linux specifica per fare delle clonazioni backup dei dischi. È fornita insieme al suo programma specifico, Mondo Rescue.
*   [Acronis True Image](https://en.wikipedia.org/wiki/Acronis_True_Image "wikipedia:Acronis True Image") è un programma commerciale per Windows. Permette di creare un live cd (da Windows), cosicché non avrete necessità di installare Windows sulla macchina che volete clonare per utilizzarlo.
*   [FSArchiver](http://www.fsarchiver.org/Main_Page) permette di salvare il contenuto di un filesystem in un archivio compresso. Può essere trovato su [System Rescue CD](http://www.sysresccd.org/Main_Page).
*   [Clonezilla](http://clonezilla.org/) è un sistema che permette di creare immagini delle partizioni, esso può anche ripristinare interi dischi oppure singole partizioni.

## Link esterni

*   [Articolo sulla clonazione dei dischi da Wikipedia (in inglese)](https://en.wikipedia.org/wiki/List_of_disk_cloning_software "wikipedia:List of disk cloning software")
*   [thread sul forum internazionale di Arch Linux](https://bbs.archlinux.org/viewtopic.php?id=4329)