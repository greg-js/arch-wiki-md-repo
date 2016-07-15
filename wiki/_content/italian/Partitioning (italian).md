Il *partizionamento* del disco fisso permette di dividere logicamente lo spazio disponibile in sezioni che possono essere accessibili indipendentemente l'uno dall'altro.

Un intero disco rigido può essere assegnato a una singola partizione, oppure si può dividere lo spazio di memoria disponibile su più partizioni. Un certo numero di scenari richiedono la creazione di più partizioni: dual- o multi-boot, per esempio, o il mantenimento di un partizione di [swap](/index.php/Swap "Swap"). In altri casi , il partizionamento è usato come mezzo di dati logicamente separati, come ad esempio la creazione di partizioni separate per i file audio e video. Schemi di partizionamento comuni sono discussi in dettaglio qui di seguito .

Ogni partizione deve essere formattata per un [tipo di file system](/index.php/File_systems_(Italiano) "File systems (Italiano)") prima di essere utilizzato.

## Contents

*   [1 Tabella delle partizioni](#Tabella_delle_partizioni)
    *   [1.1 Master Boot Record](#Master_Boot_Record)
    *   [1.2 GUID Partition Table](#GUID_Partition_Table)
    *   [1.3 Scegliere tra GPT e MBR](#Scegliere_tra_GPT_e_MBR)
*   [2 Schema di partizionamento](#Schema_di_partizionamento)
    *   [2.1 Partizione di root singola](#Partizione_di_root_singola)
    *   [2.2 Partizioni separate](#Partizioni_separate)
    *   [2.3 Punti di montaggio](#Punti_di_montaggio)
        *   [2.3.1 Partizione root](#Partizione_root)
        *   [2.3.2 /boot](#.2Fboot)
        *   [2.3.3 /home](#.2Fhome)
        *   [2.3.4 /var](#.2Fvar)
        *   [2.3.5 /tmp](#.2Ftmp)
        *   [2.3.6 Swap](#Swap)
        *   [2.3.7 Quanto grandi dovrebbero essere le mie partizioni?](#Quanto_grandi_dovrebbero_essere_le_mie_partizioni.3F)
*   [3 Strumenti di Partizionamento](#Strumenti_di_Partizionamento)
*   [4 Allineamento delle partizioni](#Allineamento_delle_partizioni)
*   [5 Utilizzando GPT - metodo moderno](#Utilizzando_GPT_-_metodo_moderno)
    *   [5.1 Riepilogo utilizzando Gdisk](#Riepilogo_utilizzando_Gdisk)
*   [6 Utilizzando MBR - metodo legacy](#Utilizzando_MBR_-_metodo_legacy)
    *   [6.1 Riepilogo utilizzando Fdisk](#Riepilogo_utilizzando_Fdisk)
*   [7 Altre fonti](#Altre_fonti)

## Tabella delle partizioni

Le informazioni sulle partizioni vengono memorizzate nella tabella delle partizioni, per la quale ci sono 2 formati in uso oggi. Il classico [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record"), e il moderno [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table"), la quale è una versione migliorata che elimina diversi limiti.

### Master Boot Record

[Wikipedia:Master boot record](https://en.wikipedia.org/wiki/Master_boot_record "wikipedia:Master boot record")

MBR originariamente supporta solo fino a 4 partizioni. Più tardi su sono state introdotte le partizioni estese e logiche per aggirare questa limitazione.

Ci sono tre tipi di partizioni :

*   Primaria
*   Estesa
    *   Logica

Le partizioni **primarie** possono essere avviabili e sono limitati a quattro partizioni per disco o volume RAID. Se uno schema di partizionamento richiede più di quattro partizioni , viene utilizzata una partizione **estesa** che contiene le partizioni **logiche**. La partizione estesa può essere considerata come un contenitore per le partizioni logiche. Un disco rigido può contenere non più di una partizione estesa. La partizione estesa è anche considerata come una partizione primaria, quindi se il disco ha una partizione estesa, sono possibili solo tre partizioni primarie aggiuntive (cioè tre partizioni primarie e una partizione estesa). Il numero di partizioni logiche che risiedono in una partizione estesa è illimitato. Un sistema in dual boot con Windows richiede che Windows risieda in una partizione primaria.

Lo schema di numerazione consueto è quello di creare partizioni primarie *sda1* fino a *sda3* seguita da una partizione estesa **sda4**. Le partizioni logiche su **sda4** sono numerate come **sda5**, **sda6**, ecc

### GUID Partition Table

[Wikipedia:GUID Partition Table](https://en.wikipedia.org/wiki/GUID_Partition_Table "wikipedia:GUID Partition Table")

Supporta solo partizioni di tipo **primaria**. La quantità di partizioni per disco o un volume RAID è illimitato.

### Scegliere tra GPT e MBR

[GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table") (GPT) è un alternativo stile di partizionamento contemporaneo. Esso è destinato a sostituire il vecchio [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") del sistema (MBR). GPT ha diversi vantaggi rispetto MBR, che ha stranezze risalenti ai tempi di MS-DOS. Con i recenti sviluppi degli strumenti di formattazione *fdisk* (MBR) e *gdisk* ( GPT), è altrettanto facile ottenere un partizionamento di tipo GPT o MBR, e di ottenere il massimo delle prestazioni.

La scelta fondamentalmente fra i due tipi di partizionamento si riduce a questo :

*   Se si usa GRUB legacy come bootloader, si deve usare MBR.
*   Per dual-boot con Windows (versioni 32-bit e 64-bit) che utilizza il vecchio BIOS, si deve usare MBR.
*   Per dual-boot di Windows a 64 bit che utilizza [UEFI](/index.php/UEFI "UEFI") al posto del BIOS, si deve usare GPT.
*   Se non si è in nessuna di queste condizioni, scegliere liberamente tra GPT e MBR. Poiché GPT è più moderno, se ne consiglia l'utilizzo.
*   Si consiglia di utilizzare sempre GPT nel caso di sistemi [[Unified Extensible Firmware Interface (Italiano)| UEFI] ], poichè alcuni firmware UEFI non consentono l'accoppiata di avvio UEFI-MBR.

## Schema di partizionamento

Non ci sono regole rigide per il partizionamento di un disco rigido, anche se uno può seguire la guida generale indicata di seguito. Lo schema di partizionamento del disco è determinata da vari fattori quali la flessibilità desiderata, la velocità, la sicurezza, così come i limiti imposti dallo spazio su disco disponibile. Si tratta essenzialmente di preferenze personale. Se si desidera dual boot Arch Linux e un sistema operativo Windows Si prega di vedere [Windows and Arch Dual Boot](/index.php/Windows_and_Arch_Dual_Boot "Windows and Arch Dual Boot").

### Partizione di root singola

Questo schema è il più semplice e dovrebbe essere sufficiente per la maggior parte dei casi di utilizzo. Uno [[swapfile] può essere creato facilmente e ridimensionato come necessario. Di solito ha senso iniziare a considerare un unica partizione `/` per poi separarne fuori altre sulla base di specifici casi d'uso, come RAID, crittografia, una partizione multimediale condivisa, ecc.

### Partizioni separate

Separare un percorso come partizione permette la scelta di un filesystem e opzioni di montaggio. In alcuni casi come una partizione multimediale, possono anche essere condivisi tra sistemi operativi.

### Punti di montaggio

I seguenti punti di montaggio sono possibili scelte per partizioni separate, si può prendere la decisione sulla base di esigenze reali.

#### Partizione root

La directory principale è il vertice della gerarchia il punto in cui il file system primario viene montato, e da cui tutti gli altri filesystem derivano. Tutti i file e le directory sono visualizzati sotto la directory root `/`, anche se sono memorizzati su dispositivi fisici differenti. Il contenuto del filesystem root deve essere adeguato per l'avvio, il ripristino, il recupero e/o per riparare il sistema. Pertanto, alcune directory presenti sotto `/` non sono candidati per partizioni separate.

La partizione `/` o la partizione di root è necessario, ed è la più importante. Le altre partizioni possono essere sostituiti da esso.

**Attenzione:** Le directory essenziali per l'avvio (ad eccezione di `/boot`) **devono** risiedere sulla stessa partizione `/` o montati all'inizio in userspace da [initramfs](/index.php/Initramfs "Initramfs"). Queste directory essenziali sono : `/etc` e `/usr` [[1]](http://freedesktop.org/wiki/Software/systemd/separate-usr-is-broken).

#### /boot

La directory `/boot` contiene le immagini del kernel e del ramdisk così come il file di configurazione del bootloader e le fasi del bootloader stesso. Inoltre, memorizza i dati che vengono utilizzati prima che il kernel inizi l'esecuzione di programmi in spazio utente. `/boot` non è richiesto per il funzionamento normale del sistema, ma solo durante l' avvio e gli aggiornamenti del kernel (quando avviene la rigenerazione del ramdisk iniziale).

Una partizione separata per `/boot` è necessaria se si intende effettuare l'installazione di un software RAID0 (stripe) del sistema.

#### /home

La directory `/home` contiene i file di configurazione specifici dell'utente, cache, dati di applicazioni e file multimediali .

Separare `/home` consente a `/` di essere ri-partizionato separatamente, ma si noti che è ancora possibile reinstallare Arch con una partizione di `/home` intatta, anche se non è separato fisicamente- solo le altre directory di primo livello hanno bisogno di essere rimosse, e quindi pacstrap può essere eseguito.

Si consiglia di non condividere la directory *home* tra utenti su diverse distribuzioni, poiché usano versioni e patch del software incompatibili. Invece, è possibile la condivisione di una partizione multimediale, oppure utilizzare differenti directory *home* sulla stessa partizione `/home`.

#### /var

La directory `/var` archivia dati variabili, come le directory e file di spool, amministrativi e dati di registrazione, la cache di [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)"), l'albero di [ABS](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)"), ecc. É utilizzato, per esempio, per il caching e la registrazione, e quindi spesso sottoposta a lettura e scrittura. Tenendolo in una partizione separata evita di esaurire lo spazio fisico su disco dove risiede `/`, a seguito di log impazziti, ecc

É possibile permettere di montare `/usr` in sola lettura. Tutto ciò che storicamente veniva scritto in `/usr` durante il funzionamento del sistema (tolto la fase di installazione e la manutenzione del software) deve risiedere in `/var`.

**Nota:** `/var` contiene molti file di piccole dimensioni. La scelta del tipo di file system dovrebbe prendere in considerazione questo fatto, se si utilizza una partizione separata.

#### /tmp

Questa è già una partizione separata per impostazione predefinita, in virtù del fatto che viene montata come *tmpfs* da systemd.

#### Swap

Una partizione di [Swap](/index.php/Swap "Swap") fornisce memoria che può essere utilizzata come RAM virtuale. Un [file per Swap](/index.php/Swap#Swap_file "Swap") dovrebbe anche essere considerato, poichè hanno pochissimo sovraccarico di prestazioni rispetto ad una partizione e sono molto più facili da ridimensionare, se necessario. Una partizione di swap può *potenzialmente* essere condivisa tra i sistemi operativi, ma non se si utilizza l'ibernazione.

#### Quanto grandi dovrebbero essere le mie partizioni?

**Nota:** Non esiste una regola per le dettare dimensione delle partizione del disco, e quelle che seguono sono solo raccomandazioni.

	/boot - 200 MB 

	Si richiedono solo circa 100 MB, ma se si pensa di utilizzare più kernel/immagini di boot, allora 200 o 300 MB sono una scelta migliore.

	/ - 15-20 GB 

	Esso contiene tradizionalmente la directory `/usr`, che può crescere in modo significativo a seconda di quanto software è stato installato. 15-20 GB dovrebbero essere sufficienti per la maggior parte degli utenti con i dischi rigidi moderni.

	/var - 8-12 GB 

	Esso conterrà, tra gli altri dati, anche l'albero [ABS](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)") e la cache di [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)"). Mantenere i pacchetti nella cache è utile e versatile in quanto offre la possibilità di effettuare un downgrade. Come risultato, `/var` tende a crescere in dimensioni. La cache di pacman, in particolare, crescerà come il sistema viene ampliato e aggiornato. Ma può, tuttavia, essere cancellata in modo sicuro se lo spazio diventa un problema. 8-12 GB su un sistema desktop dovrebbe essere sufficiente per `/var`, a seconda di quanto verrà installato il software.

	/home - [variabile] 

	É dove risiedono i dati utente, download e file multimediali. Su un sistema desktop, `/home` è in genere il più grande file system sul disco con un ampio margine.

	swap - [variabile] 

	Storicamente, la regola generale per la dimensione della partizione di swap è stata quella di assegnare il doppio della quantità di RAM fisica. Come i computer hanno acquisito capacità di memoria sempre più grandi, questa regola è diventata obsoleta. Su macchine con fino a 512MB di RAM, la regola 2x è di solito sufficiente. Se una quantità sufficiente di RAM (più di 1024 MB) è disponibile, può essere possibile avere una partizione swap più piccola o addirittura eliminarla. Con più di 2 GB di RAM fisica, si può generalmente aspettarsi di avere buone prestazioni senza una partizione di swap.

**Nota:** Se avete intenzione di utilizzare l'ibernazione utilizzando la partizione o un file di Swap, si dovrebbe vedere la pagina [Suspend and hibernate#About swap partition/file size](/index.php/Suspend_and_hibernate#About_swap_partition.2Ffile_size "Suspend and hibernate").

	/data - [variabile] 

	Si può prendere in considerazione il montaggio di una partizione "dati" per coprire vari file per essere condivisi da tutti gli utenti. Utilizzare la partizione `/home` per questo scopo va comunque bene.

**Nota:** Se possibile, un ulteriore 25% di spazio aggiunto ad ogni filesystem fornirà un sicurezza per la futura espansione e aiutare a proteggersi contro la frammentazione.

## Strumenti di Partizionamento

*   **fdisk** — Strumento per il partizionamento da terminale incluso in Linux.

	[https://www.kernel.org/](https://www.kernel.org/) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

*   **cfdisk** — Strumento per il partizionamento da terminale scritto con librerie ncurses.

	[https://www.kernel.org/](https://www.kernel.org/) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

**Attenzione:** La prima partizione creata da *cfdisk* inizia dal settore 63, anziché dal consueto 2048\. Questo può portare a prestazioni ridotte su SSD e unità Advanced Format (4k settore). Causerà problemi con [GRUB2](/index.php/GRUB_(Italiano)#messaggio_d.27errore_msdos-style "GRUB (Italiano)"). Mentre GRUB legacy e Syslinux dovrebbero funzionare bene.

*   **gdisk** — Versione [GPT](/index.php/GPT "GPT") di fdisk.

	[http://www.rodsbooks.com/gdisk/](http://www.rodsbooks.com/gdisk/) || [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk)

*   **cgdisk** — Versione GPT di cfdisk.

	[http://www.rodsbooks.com/gdisk/](http://www.rodsbooks.com/gdisk/) || [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk)

*   **GNU Parted** — Strumento per il partizionamento da terminale.

	[http://www.gnu.org/software/parted/parted.html](http://www.gnu.org/software/parted/parted.html) || [parted](https://www.archlinux.org/packages/?name=parted)

*   **[GParted](/index.php/GParted "GParted")** — Strumento grafico per il partizionamento scritto in GTK.

	[http://gparted.sourceforge.net/](http://gparted.sourceforge.net/) || [gparted](https://www.archlinux.org/packages/?name=gparted)

*   **Partitionmanager** — Strumento grafico per il partizionamento scritto in QT.

	[http://sourceforge.net/projects/partitionman/](http://sourceforge.net/projects/partitionman/) || [partitionmanager](https://www.archlinux.org/packages/?name=partitionmanager)

*   **QtParted** — Simile a Partitionmanager, disponibile su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").

	[http://qtparted.sourceforge.net/](http://qtparted.sourceforge.net/) || [qtparted](https://aur.archlinux.org/packages/qtparted/)

## Allineamento delle partizioni

**Il corretto allineamento delle partizioni è essenziale per ottimizzare le prestazioni e la longevità.** La chiave per l'allineamento è di partizionamento (almeno) per l'EBS (dimensione del blocco di cancellazione) degli SSD.

**Note:**

*   L'EBS è in gran parte determinato dal fornitore, una ricerca su Google sul modello interessato potrebbe essere una buona idea. L'Intel X25-M, per esempio, è pensato per avere un EBS di 512 KB, ma Intel non ha ancora pubblicato nulla di ufficiale a tal fine.
*   Se non si conosce l'EBS del proprio SSD, utilizzare una dimensione di 512 KB. Questi numeri sono maggiori o uguali per quasi tutti i correnti EBS. L'allineamento delle partizioni per un tale EBS si tradurrà in partizioni anche allineate per tutte le dimensioni minori. Questo è il modo in cui Windows 7 e le partizioni Ubuntu "ottimizzano" per lavorare con gli SSD.

Se le partizioni non sono allineate per iniziare a multipli della EBS (512 KB per esempio), l'allineando il sistema dei file è un esercizio inutile, perché tutto viene inclinato all'offset della partizione di avvio. Tradizionalmente, gli hard disk sono stati affrontati indicando il *cilindro*, la *testa*, e il *settore* in cui i dati sono vengono letti o scritti. Questi rappresentavano rispettivamente la posizione radiale, la testina dell'unità (=piatto e laterale) e la posizione assiale dei dati. Con LBA (Logical Block Addressing), questo non è più necessario. Al contrario, l'intero disco rigido viene gestito come un flusso continuo di dati .

## Utilizzando GPT - metodo moderno

### Riepilogo utilizzando Gdisk

Utilizzando GPT, l'utility per la modifica della tabella delle partizioni è chiamato gdisk. Esso può eseguire l'allineamento delle partizioni automaticamente con una base di dimensioni del blocco a 2048 settori (o 1024KiB), che deve essere compatibile con la stragrande maggioranza di SSD, se non tutti. GNU parted supporta anche GPT, ma è [meno facile da usare](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=601813) per l'allineamento delle partizioni . L'ambiente fornito dall'ISO di installazione di Arch include il comando *gdisk*. Se ne avete bisogno più avanti nel sistema già installato, *gdisk* è disponibile nel pacchetto [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk).

Una sintesi del uso tipico di *gdisk*  :

*   Avviare da root *gdisk* sulla vostra unità (*disk-device* può essere ad esempio `/dev/sda`):

```
# gdisk *disk-device*

```

*   Se l'unità è nuova o se si vuole ricominciare da capo, creare una nuova tabella di partizione GUID vuota con il comando {ic|o}}.
*   Creare una nuova partizione con il comando `n` (1° partizione di tipo primario).
*   Supponendo che la partizione è nuova, *gdisk* sceglierà il più alto allineamento possibile. In caso contrario, scegliere la più grande potenza di due che divide tutti gli spostamenti delle partizioni.
*   Se la scelta di inizializzare un settore prima del valore 2048, *gdisk* sposterà automaticamente l'avvio delle partizione per il settore del disco 2048\. Questo per garantire un allineamento 2048-settori (se il settore è 512B, questo sarà un allineamento a 1024KiB che dovrebbe adattarsi qualsiasi cancellazione di blocco SSD NAND).
*   Usare la forma `+*x*{M,G}` per estendere la partizione di *x* mebibyte o gibibyte, se la scelta di una dimensione che non è un multiplo della dimensione di allineamento (1024kiB), *gdisk* ridurrà la partizione al multiplo inferiore più vicino. Ad esempio, se si desidera creare una partizione 15GiB, immettere `+15G`.
*   Selezionare l'ID del tipo di partizione, per valore predefinito, `Linux/Windows data` (code `0700`), dovrebbe andare bene per la maggior parte degli utilizzi. Premere `L` per visualizzare l'elenco dei codici. Se prevedete di usare LVM selezionare `Linux LVM` (`8e00`).
*   Assegnare altre partizioni in modo simile.
*   Scrivere la tabella su disco e uscire attraverso con il comando `w`.
*   Formattare la nuova partizione con un [file system](/index.php/File_systems_(Italiano) "File systems (Italiano)").

**Nota:**

*   Per eseguire l'avvio da un disco partizionato in GPT su un sistema basato su BIOS si deve creare, preferibilmente all'inizio del disco , una [partizione BIOS di boot](/index.php/GRUB2_(Italiano)#Istruzioni_specifiche_per_GUID_Partition_Table_.28GPT.29 "GRUB2 (Italiano)") senza file system e con il tipo di partizione impostato come `BIOS boot` o come partizione `bios_grub` (codice *gdisk* di tipo `EF02`) per l'avvio da disco utilizzando [GRUB](/index.php/GRUB_(Italiano) "GRUB (Italiano)"). Per [Syslinux](/index.php/Syslinux "Syslinux"), non è necessario creare questa partizione `bios_grub`, ma è necessario disporre della partizione `/boot` separata e abilitare l'attributo `Legacy BIOS Bootable partition` per quella partizione (usando *gdisk*).
*   [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") non supporta GPT, gli utenti devono usare [BURG](/index.php/BURG "BURG"), GRUB o Syslinux.

**Attenzione:** Se si sta pianificando di avviare Windows in modalità BIOS (questa è l'unica opzione disponibile per le versioni di Windows a 32 bit e 64-bit di Windows XP), non usare GPT in quanto Windows non supporta il boot da un disco GPT in sistemi BIOS. Avrete bisogno di usare il partizionamento MBR e di avviare in modalità BIOS, come descritto di seguito. Questa limitazione non si applica per l'avvio di una moderna versione di Windows a 64 bit in modalità UEFI.

## Utilizzando MBR - metodo legacy

Utilizzando MBR, l'utility per la modifica della tabella delle partizioni è chiamata *fdisk*. Le recenti versioni di *fdisk* hanno abbandonato il sistema deprecato di utilizzare cilindri come unità di visualizzazione di default, così come la compatibilità MS-DOS per impostazione predefinita. L'ultima versione di *fdisk* allinea automaticamente tutte le partizioni a 2048 settori, o 1024 KiB, che dovrebbe funzionare per tutti i formati EBS che sono noti per essere utilizzati da produttori di SSD. Ciò significa che le impostazioni predefinite vi daranno un corretto allineamento.

Si noti che in passato, *fdisk* usava i cilindri come unità di visualizzazione di default, e mantenuta una compatibilità verso di MS-DOS che coincide con un errato allineamento per SSD. Pertanto si troveranno molte guide su Internet datate 2008-2009, poiché era un grosso problema ottenere l'allineamento in modo corretto. Con l'ultima versione di *fdisk*, le cose sono molto più semplici, come si riflettono in questa guida.

### Riepilogo utilizzando Fdisk

*   Avviare *fdisk* sul proprio dispositivo come root (*disk-device* può essere ad esempio `/dev/sda`):

```
# fdisk *disk-device*

```

*   Se l'unità è nuova o se si vuole ricominciare da capo, creare una nuova tabella delle partizioni DOS vuota con il comando `o`.
*   Creare una nuova partizione con il comando `n` (1° partizione di tipo primario).
*   Usare la forma `+*x*G` per estendere la partizione di *x* gibibytes. Ad esempio, se si desidera creare una partizione 15GiB, immettere `+15G`.
*   Cambiare l'ID di sistema della partizione dal tipo predefinito di Linux (`tipo 83`) al tipo desiderato tramite il comando `t`. Questo è un passaggio facoltativo qualora l'utente desideri creare un altro tipo di partizione, ad esempio swap, NTFS, LVM , ecc. Si noti che un elenco completo di tutti i tipi di partizione validi è disponibile tramite il comando `l`.
*   Assegnare altre partizioni in modo simile.
*   Scrivere la tabella su disco e uscire attraverso con il comando `w`.
*   Formattare la nuova partizione con un [file system](/index.php/File_systems_(Italiano) "File systems (Italiano)").

## Altre fonti

*   [Creazione di partizioni ext4 da zero](/index.php/Ext4#Creating_ext4_partitions_from_scratch "Ext4")
*   [Wikipedia : Partizionamento](https://en.wikipedia.org/wiki/it:Partizione_(informatica) "wikipedia:it:Partizione (informatica)")
*   [Partizionare manualmente il proprio hard disc tramite fdisk](http://www.novell.com/coolsolutions/feature/19350.html)