Definizione dello swap tratta da quest'articolo [All about Linux swap space](http://www.linux.com/news/software/applications/8208-all-about-linux-swap-space):

	_Linux suddivide la memoria fisica RAM (Memoria ad accesso casuale) in blocchi chiamate pagine. Lo swapping è il processo durante il quale una pagina di memoria viene copiata su uno spazio di disco, chiamata area di swap, per liberare memoria RAM. Le dimensioni combinate della memoria fisica e dell'area di swap è la quantità di memoria virtuale disponibile._

## Contents

*   [1 Area di swap](#Area_di_swap)
*   [2 Partizione dello swap](#Partizione_dello_swap)
*   [3 File dello swap](#File_dello_swap)
    *   [3.1 Creazione di un file di swap](#Creazione_di_un_file_di_swap)
    *   [3.2 Rimuovere il file di swap](#Rimuovere_il_file_di_swap)
    *   [3.3 Ripristino dal file di swap](#Ripristino_dal_file_di_swap)
*   [4 Swap su una periferica USB](#Swap_su_una_periferica_USB)
*   [5 Ottimizzazione delle prestazioni](#Ottimizzazione_delle_prestazioni)
    *   [5.1 Swappiness](#Swappiness)
    *   [5.2 Priorità](#Priorit.C3.A0)

## Area di swap

L'area di swap è di solito una partizione del disco, ma può anche essere un file. Gli utenti possono creare uno spazio di swap durante l'installazione di Arch Linux o in qualsiasi momento in caso di necessità. Lo spazio di swap è generalmente raccomandato per gli utenti con meno di 1 GB di RAM, ma diventa più una questione di preferenza personale su sistemi con una quantità di RAM fisica gratuiti (anche se è necessaria per poter utilizzare la sospensione su disco).

Per verificare lo stato dello swap, usare il seguente comando:

```
$ swapon -s

```

Oppure：

```
$ free -m

```

## Partizione dello swap

Una partizione dello swap può essere creata con la maggior parte dei programmi di gestioni delle partizioni (ad es. `fdisk`, `cfdisk`). Queste partizioni hanno come numero identificativo **82**.

Per impostare un'area di swap, si utilizza il comando `mkswap`:

```
# mkswap /dev/sda2

```

**Attenzione:** Tutti i dati nella partizione specificata andranno perduti.

Per abilitare la partizione per lo swap:

```
# swapon /dev/sda2

```

Per abilitare la partizione per lo swap durante l'avvio del sistema, aggiungere questa riga al file [fstab](/index.php/Fstab "Fstab"):

```
/dev/sda2 none swap defaults 0 0

```

## File dello swap

Come alternativa alla creazione di una partizione, un file di scambio offre la possibilità di variare la dimensione al volo, e lo si può rimuovere più facilmente. Questo può essere particolarmente utile se lo spazio su disco è prezioso (ad esempio un SSD di modeste dimensioni).

**Nota:** Il filesystem BTRFS non supporta attualmente i file di swap.

### Creazione di un file di swap

Da root utilizzare `fallocate` per creare un file di swap di dimensioni a tua scelta (M = Megabytes, G = Gigabytes) (Si può utilizzare anche `dd`, ma richiede più tempo). Ad esempio, per creare un file di swap di 512 MB:

```
# fallocate -l 512M /swapfile
# dd if=/dev/zero of=/swapfile bs=1M count=512

```

Impostare le autorizzazioni giuste (un file di swap leggibile da tutti è una grande vulnerabilità di sicurezza):

```
# chmod 600 /swapfile

```

Dopo aver creato il file dalle dimensioni adeguate, formattarlo:

```
# mkswap /swapfile

```

Attivare il file di swap:

```
# swapon /swapfile

```

Modificare il file `/etc/fstab` e aggiungere questa riga:

```
/swapfile none swap defaults 0 0

```

### Rimuovere il file di swap

Per rimuovere il file di swap, bisogna prima disattivarlo.

Da root:

```
# swapoff -a

```

Cancellare il file di swap:

```
# rm -rf /swapfile

```

### Ripristino dal file di swap

Per ripristinare il sistema da un file di swap dopo un'ibernazione, richiede l'aggiunta di un parametro al kernel. Questo parametro è `resume_offset=<Swap File Offset>`.

Il valore di `<Swap File Offset>` può essere ricavato dal comando `filefrag -v` che mostrerà una tabella. Il valore richiesto si trova alla colonna `physical` della prima riga. Ad esempio:

```
# filefrag -v /swapfile
Filesystem type is: ef53
File size of /swapfile is 4290772992 (1047552 blocks, blocksize 4096)
ext logical  physical  expected  length flags
  0       0     7546880                6144 
  1    6144  7557120  7553023   2048 
  2    8192  7567360  7559167   2048 
...

```

Dall'esempio, il valore di `<Swap FIle Offset>` è `7546880`.

**Nota:** Nel parametro del kernel `resume` bisogna inserire la partizione (es. `resume=/dev/sda1`), non il percorso al file di swap! Il parametro `resume_offset` serve ad indicare il blocco sul disco dove inizia il file di swap (es. `resume_offset=7546880`).

## Swap su una periferica USB

Grazie alla modularità offerta da Linux, siamo in grado di avere una partizione di swap su diversi dispositivi. Se si dispone di un disco rigido molto pieno, il dispositivo USB può essere utilizzato come partizione temporaneamente. Questo metodo ha qualche svantaggio:

*   Il dispositivo USB è più lento del disco rigido.
*   Le memorie flash hanno cicli limitati di scrittura. Utilizzandole come partizione di swap ridurranno la loro vita.
*   Quando un altro dispositivo è collegato al computer, non può essere utilizzato lo swap.

Per aggiungere un dispositivo USB per lo swap, in primo luogo prendere un flash USB e formattarlo con una partizione di swap. E' possibile utilizzare programmi come Gparted o fdisk. Assicurarsi di etichettare la partizione come swap prima di scrivere la tabella delle partizioni.

**Attenzione:** Accertarsi di farlo sul disco giusto!

Successivamente, modificare il file `fstab`

```
# nano /etc/fstab

```

Aggiungere una riga sotto l'attuale partizione di swap:

```
UUID=... none swap defaults,pri=10 0 0

```

Dove UUID è ottenuto dal comando:

```
ls -l /dev/disk/by-uuid/ | grep /dev/sdc1

```

Sostituire sdc1 con la partizione di swap su USB. `sdb1`

**Suggerimento:** E' preferibile utilizzare la UUID perché quando si collegano altri dispositivi al computer si potrebbe modificare l'ordine delle periferiche

Infine, aggiungere

```
pri=0

```

nella voce attuale dello swap nel file fstab, per utilizzare il file di swap sull'hard disk quando la partizione su USB è piena.

## Ottimizzazione delle prestazioni

I parametri dello swap possono essere regolati per aumentare le prestazioni.

### Swappiness

Il parametro dello _swappiness_ [sysctl](/index.php/Sysctl "Sysctl") rappresenta la preferenza (o l'inibizione) del kernel di utilizzare lo spazio di swap. Swappiness può avere un valore compreso tra 0 e 100\. L'impostazione di questo parametro ad un valore basso riduce lo scambio di RAM, ed è noto per migliorare la risposta su molti sistemi.

```
/etc/sysctl.d/90-swappiness.conf

```

```
vm.swappiness=1
vm.vfs_cache_pressure=50

```

### Priorità

Se si dispone di più di un file di swap o una partizione di swap si dovrebbe prendere in considerazione l'assegnazione di un valore di priorità (da 0 a 32767) per ogni area di swap. Il sistema utilizzerà aree di swap di priorità più elevata prima di utilizzare aree di swap di priorità inferiore. Ad esempio, se si dispone di un disco più veloce (`/dev/sda`) ed un disco lento (`/dev/sdb`), assegnare una priorità superiore per l'area di swap trova sul dispositivo veloce. Le priorità possono essere assegnati in fstab attraverso il parametro `pri`:

```
/dev/sda1 none swap defaults,pri=100 0 0
/dev/sdb2 none swap defaults,pri=10  0 0

```

Oppure attraverso il parametro di swapon `−p` (o `−−priority`):

```
# swapon -p 100 /dev/sda1

```

Se due o più aree hanno la stessa priorità, ed è la massima priorità disponibili, le pagine sono allocate su un round-robin tra di loro.