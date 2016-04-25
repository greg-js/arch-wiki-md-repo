**mkinitcpio** è un generatore initramfs di ultima generazione [initramfs](https://it.wikipedia.org/wiki/Initrd).

## Contents

*   [1 Introduzione](#Introduzione)
*   [2 Installazione](#Installazione)
*   [3 Creazione dell'immagine ed attivazione](#Creazione_dell.27immagine_ed_attivazione)
*   [4 Configurazione](#Configurazione)
    *   [4.1 MODULES](#MODULES)
    *   [4.2 BINARIES e FILES](#BINARIES_e_FILES)
    *   [4.3 HOOKS](#HOOKS)
        *   [4.3.1 Build hooks](#Build_hooks)
        *   [4.3.2 Runtime hooks](#Runtime_hooks)
        *   [4.3.3 Hook comuni](#Hook_comuni)
        *   [4.3.4 Hooks deprecati](#Hooks_deprecati)
    *   [4.4 COMPRESSION](#COMPRESSION)
    *   [4.5 COMPRESSION_OPTIONS](#COMPRESSION_OPTIONS)
*   [5 Personalizzazione del runtime](#Personalizzazione_del_runtime)
    *   [5.1 init](#init)
    *   [5.2 Usare RAID](#Usare_RAID)
    *   [5.3 Usare la rete](#Usare_la_rete)
    *   [5.4 Usare LVM](#Usare_LVM)
    *   [5.5 Usare root criptato](#Usare_root_criptato)
    *   [5.6 /usr su una partizione separata](#.2Fusr_su_una_partizione_separata)
*   [6 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [6.1 Estrarre l'immagine](#Estrarre_l.27immagine)
*   [7 Altre Fonti](#Altre_Fonti)
*   [8 Riferimenti esterni](#Riferimenti_esterni)

## Introduzione

mkinitcpio è uno script bash usato per generare un iniziale ambiente ramdisk. Da [mkinitcpio man page](https://projects.archlinux.org/mkinitcpio.git/tree/man/mkinitcpio.8.txt):

	*Il ramdisk iniziale è in sostanza un ambiente molto ridotto ("pre-userspace"), che carica vari moduli del kernel e imposta le operazioni preliminari necessarie prima di consegnare il controllo ad init. In questo modo è possibile avere, ad esempio, filesystem criptati e filesystem su software RAID. L'mkinitcpio permette inoltre estensioni con hooks personalizzati, rilevamento automatico in fase di runtime, e molte altre caratteristiche.*

Tradizionalmente, il kernel è il responsabile del rilevamento dell'hardware e dei compiti di inizializzazione nelle prime fasi del [boot process](/index.php/Arch_boot_process_(Italiano) "Arch boot process (Italiano)"), prima di montare il filesystem root e passare il controllo a `init`. Tuttavia, con il progredire della tecnologia, queste attività sono diventate sempre più complesse.

Al giorno d'ggi, il filesystem root può essere installato su una vasta gamma di hardware, da SCSI a SATA a USB, monitorato da una serie di controller di unità di produttori diversi. Inoltre, il filesystem root può essere compresso o criptato, all'interno di un software RAID o di un gruppo di volumi logici. Il modo più semplice per gestire questa serie di complessità, è passare la gestione all'ambiente userspace: il ramdisk iniziale.

Consultare: [/dev/brain0 » Blog Archive » Early Userspace in Arch Linux](http://archlinux.me/brain0/2010/02/13/early-userspace-in-arch-linux/).

mkinitcpio è uno strumento modulare per la costruzione di un'immagine init ramfs CPIO, che offre molti vantaggi rispetto ai metodi alternativi, tra cui:

*   L'utilizzo di [busybox](http://www.busybox.net/), che fornisce una base minimale e leggera per l'ambiente userspace.
*   Il supporto per **[udev](/index.php/Udev_(Italiano) "Udev (Italiano)")** per il rilevamento automatico dell'hardware in fase di esecuzione, impedendo così il caricamento di moduli non necessari.
*   L'utilizzo di script init espandibili basati su hook; che supportano hooks personalizzati che possono essere facilmente inclusi nei pacchetti [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)").
*   Supporto per **LVM2**, **dm-crypt** per entrambi i volumi legacy e LUKS, **raid**, **mdadm**, e **swsusp** e **suspend2** per la ripresa e l'avvio da dispositivi di archiviazione di massa USB.
*   La capacità di permettere molte caratteristiche per poter essere configurato dalla riga di comando del kernel, senza la necessità di ricostruire l'immagine.

mkinitcpio è stato sviluppato dagli sviluppatori di Arch Linux e da contributi della Comunità. vedere il [public Git repository](https://projects.archlinux.org/mkinitcpio.git/).

## Installazione

Il pacchetto [mkinitcpio](https://www.archlinux.org/packages/?name=mkinitcpio) è disponibile nei [repositories ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)"), ed è installato in modo predefinito in quanto incluso nel gruppo [base](https://www.archlinux.org/groups/x86_64/base/).

Gli utenti avanzati che preferiscono installare l'ultima versione in sviluppo di mkinitcpio da Git:

```
$ git clone [git://projects.archlinux.org/mkinitcpio.git](git://projects.archlinux.org/mkinitcpio.git)

```

**Note:** È **fortemente** consigliabile seguire le [mailing list del progetto Arch](https://mailman.archlinux.org/mailman/listinfo/arch-projects) se si intende utilizzare la versione Git di mkinitcpio!

## Creazione dell'immagine ed attivazione

Per impostazione predefinita, lo script mkinitcpio genera due immagini dopo l'installazione o l'aggiornamento del kernel: `/boot/initramfs-linux.img` e `/boot/initramfs-linux-fallback.img`. L'immagine *fallback* utilizza lo stesso file di configurazione come l'immagine *predefinita*, ad eccezione dell' hook **autodetect** che è saltato durante la creazione, includendo quindi anche una vasta gamma di moduli. L'hook di rilevazione (**autodetect**) automatica rileva i moduli necessari e personalizza l'immagine per hardware specifico, riducendo l'initramfs.

Gli utenti possono creare quante immagini initramfs desiderano, con differenti profili di configurazione. L'immagine desiderata deve essere specificato per il bootloader, spesso nei suoi [file di configurazione](/index.php/Boot_Loader#Configuration_files "Boot Loader"). Dopo le modifiche apportate al file di configurazione, l'immagine deve essere rigenerata. Per lo stock kernel di Arch Linux, [linux](https://www.archlinux.org/packages/?name=linux), questo si ottiene lanciando questo comando con i privilegi di root:

```
# mkinitcpio -p linux

```

L'opzione `-p` indica un *preset* da utilizzare; la maggior parte dei pacchetti kernel fornisce un mkinitcpio predefinito, che si trova in `/etc/mkinitcpio.d` (per esempio `/etc/mkinitcpio.d/linux.preset` per `linux`). Un preset è una definizione predefinita di come creare una immagine initramfs invece di specificare il file di configurazione e il file di output ogni volta.

**Attenzione:** I file `preset` vengono utilizzati per rigenerare automaticamente l'initramfs dopo un aggiornamento del kernel; fare attenzione quando li si modifica.

Gli utenti possono creare manualmente un'immagine utilizzando una configurazione alternativa del file. Ad esempio, il seguente comando genererà una immagine initramfs secondo le direttive esplicate in `/etc/mkinitcpio-custom.conf` e le salverà in `/boot/linux-custom.img`.

```
# mkinitcpio -c /etc/mkinitcpio-custom.conf -g /boot/linux-custom.img

```

Questo genererà l'immagine initramfs per il kernel attualmente in esecuzione per poi salvarli su `/boot/linux-custom.img`.

Per la creazione dell'immagine di un kernel diverso da quello attualmente in esecuzione, aggiungere la versione del kernel alla riga di comando. È possibile visualizzare le versioni del kernel disponibili in `/usr/lib/modules`.

```
# mkinitcpio -g /boot/linux.img -k 3.3.0-ARCH

```

## Configurazione

Il file di configurazione principale di **mkinitcpio** è `/etc/mkinitcpio.conf`. Inoltre, le definizioni di preset sono fornite dai pacchetti del kernel nella cartella `/etc/mkinitcpio.d` (per esempio `/etc/mkinitcpio.d/linux.preset`).

**Attenzione:** **lvm2**, **raid**, **mdadm**, e **encrypt** **NON** sono abilitati di default. Si prega di leggere attentamente questa sezione per le istruzioni, se questi hooks sono richiesti.

**Nota:** Gli utenti con più controller hardware del disco che utilizzano i nomi dei nodi stessi, ma moduli del kernel diversi (ad esempio, due SCSI / SATA o due controller IDE) devono assicurarsi che il corretto ordine dei moduli sia specificato in `/etc/mkinitcpio.conf`. In caso contrario, la posizione della partizione root può variare negli avvii, con conseguente kernel panic. Un'alternativa più elegante è quella di utilizzare nomi di dispositivo non variabili [persistent block device naming](/index.php/Persistent_block_device_naming_(Italiano) "Persistent block device naming (Italiano)"), per garantire che vengano sempre correttamente montati.

Gli utenti possono modificare cinque variabili all'interno del file di configurazione:

	`MODULES`

	Moduli del kernel da caricare prima che gli hooks vengono eseguiti all'avvio.

	`BINARIES`

	Binari supplementari da includere nell'immagine initramfs.

	`FILES`

	File aggiuntivi da inserire nell'immagine initramfs.

	`HOOKS`

	Gli hooks sono script che vengono eseguiti nel ramdisk iniziale.

	`COMPRESSION`

	Utilizzato per comprimere l'immagine initramfs.

	`COMPRESSION_OPTIONS`

	Opzioni da riga di comando da passare al programma `COMPRESSION`.

### MODULES

La stringa MODULES è usata per specificare i moduli da caricare prima di mandare in esecuzione qualsiasi altra cosa.

I moduli con suffisso `?` non restituiranno errori se non trovati. Questo può essere molto utile nel caso si stia compilando un kernel personalizzato che compili i moduli scritti esplicitamente negli HOOKS o nel file di configurazione.

**Nota:** Nel caso si utilizzi **reiser4**, questo *deve* essere aggiunto alla lista dei moduli. E se ci fosse bisogno di un qualsiasi filesystem durante il processo d'avvio, inesistente durante l'esecuzione di mkinitcpio— come nel caso di una chiave criptata LUKS su un filesystem **ext2**, ma senza nessun filesystem **ext2** montato durante l'esecuzione di mkinitcpio— il modulo di quel filesystem deve essere aggiunto alla lista MODULES. Consultare [qui](/index.php/System_Encryption_with_LUKS_for_dm-crypt#Storing_the_Key_File "System Encryption with LUKS for dm-crypt") per maggiori approfondimenti.

### BINARIES e FILES

Queste opzioni consentono all'utente di aggiungere dei file all'immagine. Sia i `BINARIES` che i `FILES` vengono aggiunti prima che gli hook siano eseguiti, e possono essere usati per sovrascrivere i file usati o forniti dagli hook. I BINARIES vengono auto-localizzati in quanto devono essere salvati in un `PATH` standard e sono *analizzatori di dipendenze*, quindi ogni libreria e dipendenza richieste saranno aggiunte di conseguenza. I FILES saranno aggiunti *come stanno*. Per esempio:

```
FILES="/etc/modprobe.d/modprobe.conf"

```

```
BINARIES="kexec"

```

In entrambi i casi, per `BINARIES` e `FILES`, più voci possono essere aggiunte delimitati da spazi.

### HOOKS

La sezione relativa agli `HOOKS`, è l'impostazione più importante del file. Gli Hook sono piccoli script che descrivono ciò che verrà aggiunto all'immagine. Per alcuni hooks, essi dovranno anche contenere una componente di runtime che fornisce un comportamento aggiuntivo, come ad esempio avviare un demone, o l'assemblaggio di un dispositivo a blocchi accatastati. Gli Hook sono indicati con il loro nome, ed eseguiti nell'ordine in cui sono elencati nel file di configurazione alla sezione `HOOKS`.

L'impostazione predefinita degli `HOOKS` dovrebbe essere sufficiente per la maggior parte delle semplici configurazioni di dischi singoli. Per i dispositivi di root che sono accatastati o dispositivi multi-block come [LVM](/index.php/LVM "LVM"), [mdadm](/index.php/Software_RAID_and_LVM "Software RAID and LVM"), o [LUKS](/index.php/LUKS "LUKS"), vedere le rispettive pagine wiki per l'ulteriore configurazione necessaria.

#### Build hooks

I Build hooks sono contenuti nella cartella `/lib/initcpio/install`. questi file vengono generati dalla shell bash durante l'esecuzione di `mkinitcpio` e devono contenere due funzioni : `build` ed `help`. La funzione `build` descrive i moduli, i file e i binari che saranno aggiunti all'immagine. Un'API, documentata da mkinitcpio(8), serve a facilitare l'aggiunta di questi elementi. La funzione `help` emette una descrizione di ciò che l'hook compie.

Per una lista di hooks disponibili, dare il comando:

```
$ mkinitcpio -L

```

Usare l'opzione di mkinitcpio `-H` per ottenere maggiori informazioni riguardo qualche hook specifico. Ad esempio:

```
$ mkinitcpio -H udev

```

#### Runtime hooks

I Runtime hook sono contenuti nella cartella `/usr/lib/initcpio/hooks`. Ad ogni hook runtime dovrebbe sempre corrispondere un build hook con lo stesso nome, il quale, una volta richiamato `add_runscript`, aggiunge l'hook di runtime all'immagine. questi file vengono generati dalla shell ash di busybox durante la prima parte del caricamento in userspace. Con l'eccezione dell'hook di pulitura, essi saranno sempre eseguiti nell'ordine elencato nella sezione `HOOKS`. I runtime hook possono contenere diverse funzioni:

`run_earlyhook`: Gli hook con questa funzione verranno eseguiti una volta che le API dei filesystem sono state montate e la linea di comando del kernel è stato analizzato. Generalmente utilizzato dai demoni addizionali, come udev, che sono necessari per il processo di avvio iniziale

`run_hook`: Gli hook con questa funzione verranno eseguiti poco dopo i primi hooks. Questo è la funzione per gli hook più comunemente usata, e le operazioni come l'assemblaggio di dispositivi a blocchi impilati dovrebbe avvenire on questo modo.

`run_latehook`: Gli hook con questa funzione verranno eseguiti dopo che il dispositivo di root è stato montato. Questo dovrebbe essere usato, con parsimonia, per le impostazioni del dispositivo di root, o per il montaggio di altri filesystem, come ad esempio `/usr`.

`run_cleanuphook`: Gli hook con questa funzione verranno eseguiti il più tardi possibile, ed in ordine inverso di come sono elencati nel file di configurazione, alla sezione `HOOKS`. Questi hook devono essere utilizzati per le operazioni di pulitura dell'ultimo minuto, come l'arresto di tutti i demoni inizializzati da un Hook avviato precedentemente.

#### Hook comuni

Segue una tabella degli hooks più comuni e di come influenzano la creazione di immagini e tempo di esecuzione.

<caption>**Hooks attuali**</caption>
| Hook | Installazione | Tempo di esecuzione |
| **base** | Imposta tutte le cartelle d'avvio ed installa le utilità di base e le librerie. Aggiungere sempre questo hook a meno che non si sappia esattamente cosa si sta facendo. | -- |
| **Systemd** | Questo installerà una configurazione di systemd di base nei vostri initramfs, ed è destinata a sostituire gli hook 'base','usr','udev' 'timestamp'. Altri hook dovrebbero essere inclusi in futuro, ma potrebbero non funzionare come previsto. Si può anche voler includere ancora l'hook 'base' (prima di questo hook), per garantire che una shell di ripristino esistente sul proprio initramfs. | -- |
| **btrfs** | Imposta i moduli necessari per consentire Btrfs per root e l'uso di subvolumes. | Esegue "btrfs device scan" per montare un multi-dispositivo con filesystem btrfs su root, quando nessun hook udev è presente. |
| **udev** | Aggiunge all'immagine udev, udevadm e le regole di udev. | Udev sarà usato per creare il nodo del dispositivo di root e rilevare i moduli necessari per il dispositivo di root. Poiché semplifica le cose, usare udev è raccomandabile. |
| **autodetect** | Riduce l'initramfs mediante autorilevamento dei moduli necessari. Verificare che i moduli inclusi siano tutti presenti e corretti. Questo hook deve essere avviato prima degli altri hook di sottosistema, per sfruttare completamente l'autorilevamento. Ogni hook specificato prima di "autodetect" sarà installato totalmente. | -- |
| **modconf** | -- | Include i file di configurazione di modprobe da `/etc/modprobe.d` e `/usr/lib/modprobe.d` |
| **block** | Aggiunge tutti i moduli dei dispositivi a blocchi, precedentemente forniti separatamente da **fw**, **mmc**, **pata**, **sata**, **scsi** , **usb** and **virtio** hooks. | -- |
| **pcmcia** | Aggiunge i moduli necessari per i dispositivi PCMCIA. È necessario disporre anche di [pcmciautils](https://www.archlinux.org/packages/?name=pcmciautils) per avvalersene. | -- |
| **net** | Aggiunge i moduli necessari per dispositivi di rete. Per dispositivi PCMCIA aggiungere anche l'hook pcmcia. | Fornisce la gestione di una root basata sulfilesystem NFS. |
| **dmraid** | Provvede al supporto per fakeRAID del device root. È necessario aver installato [dmraid](https://www.archlinux.org/packages/?name=dmraid) per poter usare questo hooks. Si noti che si predilige utilizzare `mdadm` con l'hook **mdadm_udev** e fakeraid se il controller lo supporta. | Individua e assembla i dispositivi a blocchi fakeRAID utilizzando `dmraid`. |
| **mdadm** | Fornisce il supporto per il montaggio di sistemi RAID da `/etc/mdadm.conf`, o delrilevamento automatico durante l'avvio . È necessario disporre di [mdadm](https://www.archlinux.org/packages/?name=mdadm) installato per avvalersene. L'hook **mdadm_udev** è preferibile rispetto a questo. | Individua e assembla i dispositivi a blocchi del software RAID che utilizzano `mdassemble`. |
| **mdadm_udev** | mdmon } } nella sezione di binari e aggiungere anche l'hook **shutdown**, al fine di evitare non necessarie raid-rebuilts al riavvio. | Individua e assembla i dispositivi a blocchi del software RAID che utilizzano `udev` e l'assemblaggio incrementale `mdadm`. Questo è il metodo preferito per l'assemblaggio utilizzando mdadm (anziché usare il l'hook mdadm elencato sopra). |
| **keyboard** | Aggiunge i moduli necessari per i dispositivi della tastiera. Utilizzare questa opzione se si dispone di una tastiera USB ed è necessario che sia funzionante nei primi istanti del caricamento userspace (sia per l'immissione di passphrase di crittografia o per l'uso in una shell interattiva). Come effetto collaterale, alcuni moduli per dispositivi di input diversi dalle tastiere potrebbero essere aggiunti, ma questo non dovrebbe essere un problema. | -- |
| **keymap** | Aggiunge keymap e consolefonts da `/etc/vconsole.conf`. | Carica il keymap specificato ed il consolefont da `/etc/vconsole.conf` durante l'avvio in userspace. |
| **encrypt** | Aggiunge il modulo del kernel `dm_crypt` ed il tool `cryptsetup` all'immagine. È necessario disporre di [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) installato per avvalersene. | Rileva e sblocca una partizione di root cifrata. Vedere [#Personalizzazione del runtime](#Personalizzazione_del_runtime) per supporto alla configurazione. |
| **lvm2** | Aggiunge il modulo device mapper kernel, e il tool `lvm` all'immagine. Sarà inoltre necessario avere installato il pacchetto [lvm2](https://www.archlinux.org/packages/?name=lvm2). | Abilita tutti i gruppi di voluni LVM2\. È necessario se il filesystem di root è su LVM. |
| **fsck** | Aggiunge i binari di fsck e degli helpers per il filesystem specifico. Se aggiunto dopo l'hook **autodetect** verrà aggiunto solo l'helper per il filesystem di root. Usare questo hook è **fortemente** consigliato, ed è richiesto con un partizione `/usr` separata. | Lancia fsck sul device "root" (e /usr se separata) prima del mount. |
| **resume** | -- | Tenta di eseguire il ripristino (resume) dallo stato di "sospensione". Funziona in aggiunta a *swsusp* e *[suspend2](/index.php/Suspend2 "Suspend2")*. Consultare [#Personalizzazione del runtime](#Personalizzazione_del_runtime) per supporto alla configurazione. |
| **filesystems** | Include i moduli di filesystem necessari nell'immagine. Questo hook è **richiesto**, a meno che non si specifichino i moduli di filesystem in MODULES. | -- |
| **shutdown** | Aggiunge il supporto allo spegnimento a initramfs. Usare questo hook è altamente raccomandato sei si dispone di una partizione `/usr` separata o di una partizione di root croptata. | Smonta e smonta i dispositivi allo spegnimento. |
| **usr** | Aggiunge il supporto per `/usr` su una partizione separata. | Monta la partizione `/usr` dopo che la reale partizione di root è stata montata. |
| **timestamp** | Aggiunge il binario `systemd-timestamp` all'immagine. Fornisce il supporto RD_TIMESTAMP al caricamento in userspace. RD_TIMESTAMP può essere letto ad esempio da `systemd-analyze` per determinare il tempo di avvio. | -- |

#### Hooks deprecati

Dalla versione 0.13.0 di [mkinitcpio](https://www.archlinux.org/packages/?name=mkinitcpio), l'hook `usbinput` è stato deprecato in favore dell'hook `keyboard`.

Dalla versione 0.12.0 di [mkinitcpio](https://www.archlinux.org/packages/?name=mkinitcpio), i seguenti hook sono stati deprecati, ed è necessario sostituirli con una singola istanza dell'hook `block`.

*   `fw`
*   `mmc`
*   `pata`
*   `sata`
*   `scsi`
*   `usb`
*   `virtio`

Per ulteriori informazioni , è possibile rivedere il Git commit [97368c0e78](https://projects.archlinux.org/mkinitcpio.git/commit/?id=97368c0e78f3a4fe4d62f7aedde88d4be13bfdba) o consultare la [arch-projects mailing list](https://mailman.archlinux.org/pipermail/arch-projects/2012-November/003426.html).

### COMPRESSION

Il kernel supporta vari formati per la compressione dell'initramfs, gzip, bzip2, lzma, xz (o lzma2) e lzo. Nella maggior parte dei casi, gzip o lzop forniscono il miglior equilibrio tra dimensione dell'immagine compressa e velocità di decompressione.

```
COMPRESSION="gzip"
COMPRESSION="bzip2"     # richiede kernel 2.6.30
COMPRESSION="lzma"      # richiede kernel 2.6.30
COMPRESSION="lzop"      # richiede kernel 2.6.34
COMPRESSION="xz"        # richiede kernel 2.6.38
COMPRESSION="lz4c"      # richiede kernel 3.11

```

La mancata specifica del parametro `COMPRESSION` comporterà un file initramfs compresso in gzip. Per creare un'immagine non compressa, specificare `COMPRESSION=cat` nella configurazione o utilizzare `-z cat` dalla riga di comando.

Assicuratevi di avere la corretta utility di compressione file installata per il metodo che si desidera utilizzare .

### COMPRESSION_OPTIONS

Queste sono ulteriori flag che possono essere passate al programma specificato da `COMPRESSION`, come ad esempio:

```
COMPRESSION_OPTIONS='-9'

```

In generale questi non dovrebbero essere necessari, in quanto mkinitcpio farà in modo che qualsiasi metodo di compressione supporti le flag necessarie per produrre una immagine funzionante.

## Personalizzazione del runtime

Le opzioni di configurazione del runtime possono essere inviate a `init` e ad alcuni hooks per mezzo della riga di comando del kernel. I parametri della riga di comando del kernel sono spesso forniti dal bootloader. Le opzioni specificate sotto possono essere apportate alla linea di comando del kernel per alterare il comportamento predefinito. Consultare [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") e [Arch Boot Process](/index.php/Arch_boot_process_(Italiano) "Arch boot process (Italiano)") per ulteriori informazioni.

### init

**Nota:** Le opzioni seguenti alterano il comportamento predefinito di `init` nell'ambiente initramfs. Vedere `/usr/initcpio/init` per maggiori informazioni.

	`root`

	Questo è il parametro più importante da specificare al kernel. Determina quale device deve essere montato come root. mkinitcpio è flessibile e permette diverse sintassi. Per esempio

```
root=/dev/sda1                                                # /dev node
root=LABEL=CorsairF80                                         # label
root=UUID=ea1c4959-406c-45d0-a144-912f4e86b207                # UUID
root=/dev/disk/by-path/pci-0000:00:1f.2-scsi-0:0:0:0-part1    # udev symlink (richiede l'hook **udev** )
root=801                                                      # hex-encoded major/minor number

```

	`break`

	Se è specificato `break=premount`, `init` esegue una pausa iniziale nel processo d'avvio (dopo aver caricato i moduli ma prima di montare root) e lancia una shell interattiva che può essere usata per la risoluzione di eventuali problemi. Questa shell può essere lanciata dopo il mount di root specificando `break=postmount`. La fase di boot continua dopo il logout.

	`disablehooks`

	Disabilita gli hooks al runtime aggiungendo `disablehooks=hook1{,hook2,...}`. Per esempio:

```
disablehooks=resume

```

	`earlymodules`

	Altera l'ordine in cui moduli vengono caricati, specificando quali moduli devono essere caricati prima `earlymodules=mod1{,mod2,...}`. (Questo potrebbe essere usato, per esempio, per assicurare l'ordine corretto delle interfacce di rete multiple).

	`rootdelay=N`

	Fare una pausa di `N` secondi prima di montare il sistema root apponendo il `rootdelay`. (Questo potrebbe essere usato, per esempio, per l'avvio di un disco rigido USB che è lento in fase di avvio).

Si veda anche: [Debugging with GRUB and init](/index.php/Boot_debugging "Boot debugging")

### Usare RAID

Per prima cosa aggiungere l'hook `mdadm` alla lista `HOOKS`, e poi ogni altro modulo raid richiesto (raid456, ext4) alla lista MODULES in `/etc/mkinitcpio.conf`.

**Kernel Parameters:** Usando l'hook `mdadm`, non sarà più necessario configurare la stringa RAID nei parametri [GRUB Legacy](/index.php/GRUB_Legacy_(Italiano) "GRUB Legacy (Italiano)"). L'hook `mdadm` userà il file `/etc/mdadm.conf`, o automaticamente rileverà gli array durante la fase iniziale di boot.

Se si configura tale parametro via udev, è consigliabile usare l'hook `mdadm_udev`. Questo metodo è anche quello consigliato dallo sviluppo in upstream in quanto `/etc/mdadm.conf` sarà letto per nominare i devices connessi, se esistono.

### Usare la rete

**Attenzione:** NFSv4 non è ancora supportato

**Pacchetti richiesti:**

La rete richiede che il pacchetto [mkinitcpio-nfs-utils](https://www.archlinux.org/packages/?name=mkinitcpio-nfs-utils) sia installato dai [repositories ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

**Parametri del Kernel:**

**ip=**

La specificazione di un'interfaccia può essere sia in formato corto, che è solo il nome di un'interfaccia ("eth0" o altro), che in formato allungato.( [Kernel Documentation](https://www.kernel.org/doc/Documentation/filesystems/nfs/nfsroot.txt) ) Il formato allungato può essere costituito fino a sette elementi, separati da due punti:

```
 ip=<client-ip>:<server-ip>:<gw-ip>:<netmask>:<hostname>:<device>:<autoconf>
 nfsaddrs= is an alias to ip= and can be used too.

```

*Spiegazione dei parametri:*

```
 <client-ip>   Indirizzo IP del client. Se vuoto, l'indirizzo sarà
               determinato da RARP/BOOTP/DHCP. Il tipo di protocollo 
               usato dipenderà dal parametro <autoconf>. Se questo
               parametro non è vuoto, sarà usato l'autoconf.

 <server-ip>   Indirizzo IP del server NFS. Se RARP è usato per 
               determinare l'indirizzo del client, e questo parametro 
               non è vuoto, saranno accettate solo risposte dal server
               specificato. Per usare differenti server RARP e NFS
               specificare il server RARP qui (o lasciare lo spazio vuoto), 
               e specificare il server NFS, in "nfsroot", il parametro
               (vedere sopra). Se questa voce è vuota verrà usato l'indirizzo 
               del server RARP/BOOTP che ha risposto alla richiesta DHCP.

 <gw-ip>       Indirizzo IP di un gateway se il server è su una sottorete 
               differente. Se vuoto, non verrà usato nessun gateway e il
               server sarà, presumibilmente, nella rete locale, a meno che 
               non venga ricevuto qualche valore attraverso BOOTP/DHCP.

 <netmask>     Netmask per l'interfaccia di rete locale. Se lasciato vuoto,
               il netmask è derivato dall'indirizzo IP del client che presume
               l'indirizzamento "classful", a meno che venga annullato nella 
               risposta di BOOTP/DHCP.

 <hostname>    Il nome del client. Se vuoto, l'indirizzo
               IP del client è usato nella notazione ASCII, oppure il 
               valore ricevuto da BOOTP/DHCP.

 <device>      Nome del dispositivo di rete da usare. Se vuoto, tutti i
               dispositivi sono usati per le richieste RARP/BOOTP/DHCP, e il
               primo a ricevere una risposta viene configurato. Se si usa
               un'unico dispositivo si può lasciare vuota questa voce.              

 <autoconf>    Metodo da usare per l'autoconfigurazione. Se include sia
               "rarp", "bootp", che "dhcp" il protocollo specificato verrà
               usato.  Se il valore è "both", "all" o vuoto, tutti i
               protocolli verranno usati. "off", "static" o "none" significa
               no autoconfigurazione.

```

*Esempi:*

```
 ip=127.0.0.1:::::lo:none  --> Permettere l'interfaccia loopback.
 ip=192.168.1.1:::::eth2:none --> Permettere l'interfaccia statica eth2.
 ip=:::::eth0:dhcp --> Permettere il protocollo dhcp per la configurazione eth0.

```

**BOOTIF=**

Se si dispone di più schede di rete, questo parametro può includere l'indirizzo MAC dell'interfaccia che si sta avviando. Questo è spesso utile in quanto la numerazione dell'interfaccia può cambiare, o insieme con le opzioni pxelinux IPAPPEND 2 o IPAPPEND 3.

Se non indicato, sarà utilizzato eth0.

*Example:*

```
 BOOTIF=01-A1-B2-C3-D4-E5-F6  # Note the prepended "01-" and capital letters.

```

**nfsroot=**

Se il parametro "nfsroot" non viene dato dalla riga di comando, sarà usato il predefinito "/tftpboot/%s".

```
 nfsroot=[<server-ip>:]<root-dir>[,<nfs-options>]

```

*Spiegazione dei parametri:*

```
 <server-ip>   Specifica l'indirizzo IP del server NFS. Se non specificato,
               l'indirizzo predefinito è determinato dall' "ip" variabile
               (vedere più sotto). Un'utilità di questo valore è per esempio
               la possibilità di usare differenti server per RARP e NFS.
               In generale si può lasciare in bianco.

 <root-dir>    Nome della cartella sul server, da montare come root. Se c'è
               un "%s" nella stringa, il simbolo sarà sostituito dalla
               rappresentazione ASCII dell'indirizzo ip del client.

 <nfs-options> Opzioni standard NFS. Tutte le opzioni sono separate da virgole.
               Se non viene fornita nessuna opzione, saranno usate le 
               seguenti opzioni predefinite:
                       port            = as given by server portmap daemon
                       rsize           = 1024
                       wsize           = 1024
                       timeo           = 7
                       retrans         = 3
                       acregmin        = 3
                       acregmax        = 60
                       acdirmin        = 30
                       acdirmax        = 60
                       flags           = hard, nointr, noposix, cto, ac

```

**root=/dev/nfs**

Se non si utilizzano parametri `nfsroot=` bisognerà configurare `root=/dev/nfs` per avviare un nfs da root per l'auto-configurazione.

### Usare LVM

Se il dispositivo di root è su LVM, bisognerà aggiungere l'hook **lvm2**, e passare il dispositivo di root sulla riga di comando del kernel nel seguente formato

```
root=/dev/mapper/<volume group name>-<logical volume name>

```

per esempio :

```
root=/dev/mapper/myvg-root

```

Inoltre, se il vostro dispositivo di root viene inizializzato lentamente (ad esempio su un dispositivo USB) e/o si riceve un errore durante l'avvio del tipo : "volume group not found", allora potrebbe essere necessario aggiungere la seguente riga di comando per il kernel :

```
lvmwait=/dev/mapper/<volume group name><logical volume name>

```

per esempio :

```
 lvmwait=/dev/mapper/myvg-root

```

In questo modo il processo di avvio attende che LVM riesca a rendere il dispositivo disponibile .

### Usare root criptato

Se il volume di root è codificato, si deve aggiungere l'hook `encrypt`.

Per una partizione criptata utilizzare qualcosa simile a questo:

```
root=/dev/mapper/root cryptdevice=/dev/sda5:root

```

In questo esempioi, `/dev/sda5` è il device crittografato, e diamo un nome arbitrario di `root`, il che significa che il nostro dispositivo di root, una volta sbloccato, è montato come `/dev/mapper/root`. Al boot, verrà richiesto per la passphrase per sbloccarlo. Si veda [LUKS#Configuration_of_initcpio](/index.php/LUKS#Configuration_of_initcpio "LUKS") Per ulteriori dettagli sull'utilizzo di una root criptata.

### /usr su una partizione separata

Se durante l'installazione di Arch Linux si è scelto di montare `/usr` su una partizione separate, è necessario rispettare i seguenti requisiti:

*   Aggiungere l'hook `shutdown`. Il processo di spegnimento salverà una copia dell'initramfs e permetterà a `/usr` (e root) di essere adeguatamente smontata.
*   Aggiungere l'hook `fsck`, contrassegnare `/usr` con un `passno` di valore `0` in `/etc/fstab`. Mentre è consigliato per tutti, è obbligatorio se si desidera che la partizione `/usr` sia controllata al boot. Senza questo hook, `/usr` non verrà mai controllata.
*   Aggiungere l'hook `usr`. Questo monterà la partizione `/usr` dopo che root è montato. Prima della versione 0.9.0, il montaggio di `/usr` sarebbe avvenuto automaticamente nella root reale se fosse stato trovato in `/etc/fstab`.

## Risoluzione dei problemi

### Estrarre l'immagine

Se si è curiosi e si vuole scoprire cosa c'è dentro l'immagine initrd, la si può estrarre, per dare un'occhiata ai file all'interno.

L'immagine initrd è un archivio SVR4 CPIO, generato dai comandi `find` e `bsdcpio`, opzionalmente compresso con uno schema di compressione compreso dal kernel. Per ulteriori informazioni sugli schemi di compressione , vedere [#COMPRESSION](#COMPRESSION).

Mkinitcpio include uno strumento chiamato `lsinitcpio` che elenca ed estrae i contenuti dell'immagine initramfs.

Si possono elencare i file nell'immagine con:

```
$ lsinitcpio /boot/initramfs-linux.img

```

Ed estrarli nella cartella attuale:

```
$ lsinitcpio -x /boot/initramfs-linux.img

```

È anche possibile avere una lista più human-friendly delle più importanti parti dell'immagine:

```
$lsinitcpio -a /boot/initramfs-linux.imq

```

## Altre Fonti

*   [Boot debugging](/index.php/Boot_debugging "Boot debugging") - Debugging with GRUB

## Riferimenti esterni

*   Documentazione del kernel Linux: [initramfs](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=blob;f=Documentation/filesystems/ramfs-rootfs-initramfs.txt;hb=HEAD)
*   Documentazione del kernel Linux: [initrd](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=blob;f=Documentation/initrd.txt;hb=HEAD)
*   Articolo Wikipedia: [initrd](http://it.wikipedia.org/wiki/initrd)