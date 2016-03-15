Ext4 è l'evoluzione del filesystem Linux più utilizzato, ext3\. Per molti versi, ext4 è un miglioramento più consistente di Ext3 rispetto quello che è stato ext3 su ext2\. Ext3 implementava la nuova funzionalità del journaling a Ext2, ma Ext4 modifica importanti strutture dati nel filesystem, come quelli destinati a memorizzare i file dei dati. Il risultato è un filesystem con un design migliorato, migliori prestazioni, affidabilità e funzionalità.

Fonte: [Ext4 - Linux Kernel Newbies](http://kernelnewbies.org/Ext4)

## Contents

*   [1 Creazione di partizioni ext4 "from scratch"](#Creazione_di_partizioni_ext4_.22from_scratch.22)
*   [2 Migrazione da ext3 a ext4](#Migrazione_da_ext3_a_ext4)
    *   [2.1 Montare partizioni ext3 come ext4 senza convertirle](#Montare_partizioni_ext3_come_ext4_senza_convertirle)
        *   [2.1.1 Fondamento logico](#Fondamento_logico)
        *   [2.1.2 Procedura](#Procedura)
    *   [2.2 Convertire partizioni ext3 a ext4](#Convertire_partizioni_ext3_a_ext4)
        *   [2.2.1 Fondamento logico](#Fondamento_logico_2)
        *   [2.2.2 Prerequisiti](#Prerequisiti)
        *   [2.2.3 Procedura](#Procedura_2)
        *   [2.2.4 Migrare i file all'estensione](#Migrare_i_file_all.27estensione)
*   [3 Suggerimenti](#Suggerimenti)
    *   [3.1 Rimuovere i blocchi riservati](#Rimuovere_i_blocchi_riservati)
*   [4 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [4.1 Kernel Panic](#Kernel_Panic)
    *   [4.2 Corruzione dei dati](#Corruzione_dei_dati)
    *   [4.3 Barrier e performance](#Barrier_e_performance)
        *   [4.3.1 E4rat](#E4rat)

## Creazione di partizioni ext4 "from scratch"

1.  Aggiornare il sistema: `pacman -Syu`
2.  Formattare la partizione: `mkfs.ext4 /dev/sdxY` (sostituire `sdxY` con il dispositivo da formattae (es. `sda1`))
3.  Montare la partizione
4.  Aggiungere una voce a `/etc/fstab`, usando il filesystem "type" ext4

**Tip:** Consultare il mkfs.ext4 man page per ulteriori opzioni; modificare `/etc/mke2fs.conf` per visualizzare/configurare le opzioni di default.

## Migrazione da ext3 a ext4

Ci sono due modi per passare da ext3 a partizioni ext4:

*   mediante il montaggio delle partizioni ext3 come ext4 senza conversione (compatibilità)
*   mediante la conversione da ext3 a ext4 (performance)

Questi due metodi sono descritti di seguito.

### Montare partizioni ext3 come ext4 senza convertirle

#### Fondamento logico

Un compromesso tra convertire completamente a ext4 e rimanere con ext3, è quello di montare le partizioni esistenti ext3 come ext4.

**Pro:**

*   Compatibilità (il filesystem può continuare ad essere montato come ext3) – Questo permette agli utenti di leggere ancora il filesystem da altre distribuzioni/sistemi operativi senza supporto a ext4 (ad esempio, Windows con i driver ext3)
*   Miglioramento delle prestazioni (anche se non tanto quanto una piena conversione a della partizione a ext4) – Consultare [Ext4 - Linux Kernel Newbies](http://kernelnewbies.org/Ext4) per maggiori delucidazioni.

**Contro:**

*   Meno funzionalità complessive di ext4 utilizzate (solo quelle che non cambiano il formato del disco, quali l'assegnazione e la ripartizione multiblock ritardato)

**Note:** Fatta eccezione per la relativa novità di ext4 (che può essere vista come un rischio), **non vi è grave inconveniente a questa tecnica** **.**

#### Procedura

1.  Modificare `/etc/fstab` e cambiare il "type" da ext3 a ext4 per ogni partizione che si desidera montare come ext4.
2.  Rimontare le partizioni in questione.
3.  Fatto.

### Convertire partizioni ext3 a ext4

#### Fondamento logico

Per provare i vantaggi di ext4, deve essere completato un irreversibile processo di conversione.

**Pro:**

*   Prestazioni migliorate e nuove funzionalità – Consultare [Ext4 - Linux Kernel Newbies](http://kernelnewbies.org/Ext4) per maggiori delucidazioni.

**Contro:**

*   L'accesso in sola lettura da Windows può essere fornito da Ext2Explore, ma non c'è attualmente nessun driver per la scrittura dei dati.
*   Irreversibile (le partizioni in ext4 non possono essere ripristinate a ext3)

#### Prerequisiti

Il seguente software è richiesto sul sistema operativo Arch Linux:

*   `kernel >= 2.6.28`
*   `e2fsprogs >= 1.41`

Convertendo la propria partizione /boot a ext4:

*   `grub >= 0.97` (con patch ext4)

**Note:** La patch ext4 è inclusa di default con il pacchetto GRUB di Arch (al momento in cui si sta scrivendo, e questo probabilmente non cambierà). Altrimenti, [GRUB2](/index.php/GRUB2 "GRUB2") è richiesto per l'avvio da una partizione ext4.

**Attenzione:** Fare il boot da una partizione ext4 non è "ufficialmente" supportato da GRUB, e [GRUB2](/index.php/GRUB2 "GRUB2") è ancora in fase di sviluppo. Mentre GRUB è attivo e predefinito, l'opzione "sicura" è fare il boot da una partizione /boot formattata ext2 o ext3 . **CONSIDERATEVI AVVISATI!**

Se si converte la partizione di root (/) a ext4:

*   `mkinitcpio >= 0.5.20`

Se si converte la partizione di root (/) a ext4, anche il seguente software è necessario su un CD/USB:

*   `e2fsprogs >= 1.41`

**Note:** È raccomandabile usare le ultime release di Arch Linux (2009.02). Le immagini di Arch Linux più datate (<= 2008.06) includono versioni di `e2fsprogs` obsolete, anche se è semplice risolvere con `pacman -S e2fsprogs` dall'ambiente live dopo aver configurato la rete. In alternativa, [SystemRescueCd >= 1.1.4](http://www.sysresccd.org/Download) include una versione adatta, ed è un CD utile da avere a portata di mano.

#### Procedura

Queste istruzioni sono state adattate da [http://ext4.wiki.kernel.org/index.php/Ext4_Howto](http://ext4.wiki.kernel.org/index.php/Ext4_Howto) e [https://bbs.archlinux.org/viewtopic.php?id=61602](https://bbs.archlinux.org/viewtopic.php?id=61602). Sono state verificate e confermate da questo autore il 16 gennaio 2009.

*   **UPGRADE!** Eseguire un sysupgrade per garantire che tutti i pacchetti necessari siano aggiornati: `pacman -Syu`
*   **[BACK-UP!](/index.php/Backup_programs "Backup programs")** Eseguire il back up di tutti i dati delle partizioni ext3 che devono essere convertiti in ext4\. Anche se ext4 è considerato "stabile" per un uso generale, è ancora relativamente giovane e non ancora collaudato completamente. Inoltre, questo processo di conversione è stato solo testato su una configurazione relativamente semplice, non è possibile testare ogni singola configurazione delle molte possibili che si potrebbero avere in esecuzione.
*   Modificare `/etc/fstab` e cambiare il "tipo" da ext3 a ext4 per tutte le partizioni che devono essere convertite a ext4.

**Attenzione:** ext4 è retrocompatibile con ext3 fino a che le estensioni ed altre opzioni rimangono abilitate. Se si ha una partizione che viene condivisa con un altro sistema operativo che non può ancora leggere il formato ext4, è possibile montare suddetta partizione come ext4 su Arch e poter ancora usarla come ext3 su altri sistemi. Non sarà più così dopo il seguente passo! Si noti, tuttavia, che ci sono meno vantaggi ad utilizzare ext4 se la partizione non è completamente convertita.

*   Il processo di conversione con `e2fsprogs` deve essere fatto quando l'unità non è montata. Se applicato ad una partizione di root (/), il modo più semplice per raggiungere questo obiettivo è fare il boot da qualche altra supporto live, come descritto nella sezione 'Prerequisiti' sopra.
    *   Avviare il supporto live (se necessario).
    *   Per ogni partizione da convertire in ext4:
        *   Assicurarsi che la partizione **NON** sia montata
        *   Eseguire `tune2fs -O extents,uninit_bg,dir_index /dev/the_partition` (dove `/dev/the_partition` va sostituito con il percorso della partizione desiderata, come `/dev/sda1`)
        *   Eseguire `fsck -fDp /dev/the_partition`

**Note:** Si **DEVE** eseguire un fsck sul filesystem, altrimenti sarà illeggibile! L'esecuzione di fsck è necessaria per restituire al file system uno stato di coerenza. **Verranno trovati errori di checksum nel "descriptors group"** -- questo è previsto. Il parametro "-f" richiede a fsck di forzare il controllo, anche se il file system sembra pulito. Il parametro "-p" richiede a fsck di "riparare automaticamente" (in caso contrario, all'utente verranno richiesti interventi per ogni errore). Potrebbe essere necessario eseguire fsck -f anziché fsck -fp.

*   Riavviare Arch Linux!

**Attenzione:** Se è stata convertita la partizione root (/), si possono verificare dei kernel panic durante il tentativo di avvio. Se questo accade, è sufficiente riavviare con l'initial ramdisk "fallback", e rigenerare l'initial ramdisk predefinito: `mkinitcpio -p linux`

#### Migrare i file all'estensione

**Attenzione:** **NON** utilizzare il seguente metodo con i repository Mercurial che sono stati clonati in locale, poichè in questo modo si possono danneggiare i repository. Si potrebbero inoltre corrompere determinati "hard link" nel filesystem.

Anche se il filesystem risulta ora convertito in ext4, tutti i file scritti prima della conversione non godono dei vantaggi derivanti dalla nuova "estensione" di ext4, che va a migliorare le performance per file grandi e a ridurre la frammentazione e il tempo di controllo del filesystem. Per godere pienamente dei vantaggi di ext4, tutti i file dovrebbero essere riscritti sul disco. Un programma chiamato "e4defrag" è in via di sviluppo e si prenderà cura di questo compito; tuttavia non è ancora pronto per la produzione.

Per fortuna, è possibile utilizzare il programma "chattr", che farà in modo che il kernel riscriva i file utilizzando la nuova estensione. È possibile lanciare il comando su tutti i file e cartelle di una partizione (ad esempio se /home si trova su una partizione dedicata) in questa maniera, da root:

```
find /home -xdev -type f -print0 | xargs -0 chattr +e
find /home -xdev -type d -print0 | xargs -0 chattr +e

```

Si raccomanda di provare questo comando prima su una piccola quantità di file, e controllare che tutto sia andato per il verso giusto. Potrebbe essere anche utile controllare il filesystem dopo la conversione.

Usando il comando *lsattr*, è possibile controllare che i file ora utilizzino l'"estensione". La lettera "e" dovrebbe apparire nella lista attributi dei file elencati.

## Suggerimenti

### Rimuovere i blocchi riservati

Di default, il 5% di un file system è contrassegnato come riservato per l'utente root. Per i moderni dischi ad alta capacità, questo equivale a più del necessario, in particolare se la partizione non viene utilizzata per i file di sistema. È generalmente ritenuto sicuro ridurre la percentuale dei blocchi riservati per liberare spazio sul disco, nei casi in cui la partizione sia:

*   Molto grande (per esempio superiore ai 50 G)
*   Non utilizzata per i file di sistema

Utilizzare a questo scopo l'utilità tune2fs. Il comando d'esempio riportato in seguito, imposta la percentuale dei blocchi riservati sulla partizione /dev/sdXY all' 1.0%:

```
tune2fs -m 1.0 /dev/sdXY

```

## Risoluzione dei problemi

### Kernel Panic

Un problema che quest'autore ha incontrato è quello di un kernel panic dopo aver convertito la partizione di root (/) in ext4\. Ciò è dovuto al fatto che il ramdisk iniziale identifica la partizione come "ext4dev", invece di "ext4". È semplice quindi avviare con il ramdisk "fallback" iniziale e ricreare il ramdisk iniziale di "base":

*   Rimontare la partizione di root in modalità lettura-scrittura; presupponendo che la partizione root sia 'XXX' :

```
# mount /dev/XXX / -o remount,rw

```

*   Montare manualmente la partizione di boot in /boot se si trova su un'altra partizione.
*   Ricreare il ramdisk :

```
# mkinitcpio -p linux

```

Durante il processo di creazione, `mkinitcpio` individuerà correttamente e includerà il modulo ext4 nel ramdisk iniziale.

### Corruzione dei dati

Alcuni dei primi utilizzatori di ext4 si sono imbattuti in corruzioni di dati dopo un reboot forzato. Si legga [Ext4 perdita di dati; spiegazioni e soluzioni](http://www.h-online.com/open/Ext4-data-loss-explanations-and-workarounds--/news/112892) per maggiori informazioni.

Dal kernel 2.6.30, ext4 è considerato "(più) sicuro". Numerose sono le patch utilizzate per aumentare la robustezza di ext4 - sebbene ad un lieve costo in termini di prestazioni. Una nuova opzione di mount (`auto_da_alloc`) può essere utilizzata per disabilitare questo comportamento. Per maggiori informazioni, si legga [Linux 2 6 30 - aumento di performance del filesystem](http://kernelnewbies.org/Linux_2_6_30#head-329ba44b44a7f58c98ae22b8f2730418cdd6630d).

Per le versioni di kernel precedenti alla 2.6.30, si consideri di poter aggiungere `rootflags=data=ordered` alla linea `kernel` nel file di GRUB `menu.lst` come misura preventiva.

### Barrier e performance

A partire dal kernel 2.6.30, le performance di ext4 sono diminuite a causa di cambiamenti atti a migliorare l'integrità dei dati [[1]](http://www.phoronix.com/scan.php?page=article&item=ext4_then_now&num=1).

*La maggior parte dei filesystem (XFS, ext3, ext4, reiserfs) inviano al disco delle barriere in scrittura dopo l'fsync o durante i transaction commits. Le barriere in scrittura inducono ad un corretto ordinamento delle stesse, rendendo sicure all'uso le scritture sulla cache del disco (ad un certo calo delle prestazioni). Se i dischi hanno un qualche vincolo alla batteria, disabilitare le barriere può migliorare le prestazioni.*

*L'invio di barriere in scrittura può essere disabilitato utilizzando l'opzione di mount barrier=0 (per ext3, ext4, e reiserfs), o usando l'opzione di mount nobarrier mount (per XFS)* [[2]](http://doc.opensuse.org/products/draft/SLES/SLES-tuning_sd_draft/cha.tuning.io.html).

**Warning:** Disabilitando le barriere quando i dischi non garantiscono che la cache scriva in caso di mancanza di alimentazione può portare a una grave corruzione del file system e perdita di dati.

Per disattivare le barriere aggiungere l'opzione `barrier=0` al filesystem desiderato in `/etc/fstab`. Ad esempio:

```
# /dev/sda5    /    ext4    noatime,barrier=0    0    1

```

#### E4rat

[E4rat](/index.php/E4rat "E4rat") è un'applicazione di precaricamento progettata per ext4\. Controlla i file aperti durante l'avvio, ottimizza la loro collocazione sulla partizione per migliorare i tempi di accesso e li precarica all'inizio del processo di boot.