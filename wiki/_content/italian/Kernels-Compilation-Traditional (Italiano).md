Il riepilogo in basso è utile per compilare kernel personalizzati da **kernel.org sources**. Questo metodo di compilazione dei kernel è un metodo tradizionale comune a tutte le distribuzioni; comunque è anche presente un metodo per installare in modo pulito il kernel personalizzato con makepkg.

Alternativamente, si puù usare ABS per compilare ed installare il proprio kernel; vedere: [Kernels_(Italiano)#Compilazione](/index.php/Kernels_(Italiano)#Compilazione "Kernels (Italiano)"). Usare l'esistente PKGBUILD di [linux](https://www.archlinux.org/packages/?name=linux) automatizzerà quasi tutto il processo e si otterrà un pacchetto. Tuttavia, alcuni utenti Arch preferiscono la via _tradizionale_.

## Contents

*   [1 Recupero dei sorgenti](#Recupero_dei_sorgenti)
    *   [1.1 Riguardo /usr/src/](#Riguardo_.2Fusr.2Fsrc.2F)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Ottenere un file .config](#Ottenere_un_file_.config)
    *   [2.2 Configurare il proprio kernel](#Configurare_il_proprio_kernel)
        *   [2.2.1 Versione locale](#Versione_locale)
*   [3 Compilazione ed installazione](#Compilazione_ed_installazione)
    *   [3.1 Compilare](#Compilare)
    *   [3.2 Installare i moduli](#Installare_i_moduli)
    *   [3.3 Copiare il kernel nella cartella /boot](#Copiare_il_kernel_nella_cartella_.2Fboot)
    *   [3.4 Creare un initial RAM disk](#Creare_un_initial_RAM_disk)
    *   [3.5 Copiare System.map](#Copiare_System.map)
*   [4 Configurazione del bootloader](#Configurazione_del_bootloader)
*   [5 Usare il driver video NVIDIA con il proprio kernel personalizzato](#Usare_il_driver_video_NVIDIA_con_il_proprio_kernel_personalizzato)

## Recupero dei sorgenti

*   Scaricare i sorgenti del kernel da `ftp.xx.kernel.org/pub/linux/kernel/`, dove xx è il chiave del tuo paese (per esempio 'it', 'us', 'uk', 'de', ... - Controllare [[1]](http://www.kernel.org/mirrors/) per una lista dei mirror completa). Se non si ha alcuna gui ftp, si può utilizzare `wget`. Per questo esempio si prenderà e compilerà il 3.2.9; dovrebbe essere necessario cambiare solo la versione per ottenere un kernel diverso.

Ad esempio:

```
$ wget -c [http://www.kernel.org/pub/linux/kernel/v3.0/linux-3.2.9.tar.bz2](http://www.kernel.org/pub/linux/kernel/v3.0/linux-3.2.9.tar.bz2)

```

*   È sempre una buona idea verificare la firma di ogni tarball scaricata. Vedere [kernel.org/signature](http://kernel.org/signature.html#using-gnupg-to-verify-kernel-signatures) sul funzionamento e altri dettagli.

*   Copiare il sorgente del kernel nella propria cartella di compilazione, ad esempio:

```
$ cp linux-3.2.9.tar.bz2 ~/kernelbuild/

```

*   Estrarlo ed entrare nella cartella del sorgente:

```
$ cd ~/kernelbuild
$ tar -xvjf linux-3.2.9.tar.bz2
$ cd linux-3.2.9

```

Preparare la compilazione eseguendo il seguente comando:

```
make mrproper

```

Ciò assicura che l'albero del kernel sia assolutamente pulito. Il kernel team raccomanda che tale comando sia eseguito prima di ogni compilazione del kernel. Non si faccia affidamento sul fatto che l'albero del sorgente sia pulito dopo averlo estratto.

### Riguardo /usr/src/

Usare la cartella /usr/src/ per la compilazione del kernel da root, insieme alla creazione del symlink corrispondente, è considerata una cattiva pratica da alcuni kernel hacker. Questi ritengono che il metodo più pulito sia usare semplicemente la propria cartella home. Se ci si trova d'accordo con questo punto di vista, compilare e configurare il proprio kernel come utente normale ed installarlo come root, o [con makepkg e pacman](/index.php/Kernels/Arch_Build_System_(Italiano) "Kernels/Arch Build System (Italiano)").

Comunque, questo concetto è stato oggetto di dibattito e altri hacker di grande esperienza considerano completamente sicura, accettabile ed addirittura preferibile, la pratica di compilazione da root.

Si usi qualunque metodo con cui ci si senta a proprio agio.

## Configurazione

Questo è un passo cruciale nella personalizzazione del kernel per riflettere le precise specifiche del proprio computer. Impostando opportunamente le configurazioni in 'menuconfig', il kernel ed il computer funzioneranno più efficientemente.

### Ottenere un file .config

Opzionale. Copiare il file .config dal kernel in esecuzione, se si vogliono modificare le impostazioni di default di Arch.

```
 $ zcat /proc/config.gz > .config

```

### Configurare il proprio kernel

Ci sono due scelte:

*   Il tradizionale menuconfig

```
$ make menuconfig        (Inizierà con un '.config' nuovo. Le dipendenze opzionali sono di solito selezionate automaticamente.)

```

Apportare le proprie modifiche e salvare il file config. È una buona idea fare una copia di backup poichè è facile dover fare ciò diverse volte prima di avere tutte le giuste opzioni. Se non si riesce ad avviare il nuovo kernel compilato, vedere la lista dei config item necessari [qui](https://www.archlinux.org/news/users-of-unofficial-kernels-must-enable-devtmpfs-support/). Eseguire $ lspci -k # da liveCD elencherà i nomi dei moduli del kernel in uso.

*   localmodconfig

Dal kernel 2.6.32 viene fornito localmodconfig per facilitare la configurazione del kernel:

```
$ make oldconfig         (Funziona solo con il vecchio file '.config', copiato nella cartella di compilazione. Inoltre marca le opzione precedentemente inutilizzate come 'NEW'.)
$ make localmodconfig    (Prova ad estrarre /proc/config.gz dal kernel in esecuzione. Pre-seleziona opzioni/moduli in uso.)
$ make localyesconfig    (Come sopra, eccetto che vengono compilati nel kernel più moduli possibili.)
$ make xconfig           (Dipende da Qt. Una migliore interfaccia. Controllo delle dipendenze non verificato.)
$ make gconfig           (Dipende da GTK. Come xconfig.)
$ make help              (Elenca TUTTI i target disponibili.)

```

Per ulteriori informazioni riguardo "localmodconfig" fare riferimento alle [note di rilascio del 2.6.32](http://kernelnewbies.org/Linux_2_6_32#head-11f54cdac41ad6150ef817fd68597554d9d05a5f).

#### Versione locale

Se si sta compilando un kernel utilizzanto il file config corrente, non si dimentichi di rinominare la versione del kernel, o si potrebbe sostituire per errore quello esistente.

```
$ make menuconfig
General setup  --->
 (-ARCH) Local version - append to kernel release '3.n.n-RCn'

```

## Compilazione ed installazione

Per compilare il kernel manualmente, seguire questi passi:

### Compilare

**Attenzione:** Non eseguire `make all` se si usa GRUB e si ha ancora LILO installato; esso configurerà LILO alla fine e non si sarà più in grado di avviare la propria macchina! Rimuovere LILO (pacman -R lilo) prima di lanciare `make all` se si usa GRUB!

```
$ make      (Come make vmlinux && make modules && make bzImage - consultare 'make help' per ulteriori informazioni.)

```

oppure

```
$ make -jN   (N = # di processori + 1) (Questo utilizza al 100% tutte le CPU. Un Dual-core[-j3] da 2.8Ghz compila in meno di 15 minuti.)

```

### Installare i moduli

Deve essere fatto da root.

```
# make modules_install

```

Questo copia i moduli compilati in una cartella in /lib/modules con lo stesso nome della versione del kernel ed aggiunge la stringa che è stata scelta in menuconfig. In tal modo i moduli sono tenuti separati da quelli usati da altri kernel della propria macchina.

### Copiare il kernel nella cartella /boot

```
# cp -v arch/x86/boot/bzImage /boot/vmlinuz-NomeTuoKernel

```

### Creare un initial RAM disk

L'initial RAM disk (opzione initrd nel menu GRUB o il file "initramfs-NomeTuoKernel.img") è un root file system iniziale che viene montato prima che il vero root file system sia disponibile. L'initrd è legato al kernel ed è caricato come parte della procedura d'avvio dello stesso. Il kernel quindi monta questo initrd come parte di un processo a due stadi per caricare i moduli per rendere disponibile il file system reale. L'initrd contiene un set minimo di cartelle ed eseguibili per permettere tutto questo, come lo strumento insmod per installare i moduli nel kernel. Nel caso di sistemi Linux desktop o server, l'initrd è un file system di transizione. La sua durata di vita è breve, servendo soltanto come ponte al vero root file system. In sistemi integrati senza memoria mutevole, l'initrd è il root file system permanente.

Se si necessita di moduli caricati in modo tale da montare il root filesystem, compilare un a ramdisk (la maggior parte degli utenti ne hanno bisogno). Il parametro -k accetta la versione del kernel e la stringa aggiunta che è stata impostata con menuconfig ed è usato per localizzare i moduli in /lib/modules:

```
# mkinitcpio -k NomeKernelCompleto -g /boot/initramfs-NomeTuoKernel.img

```

Si è liberi di nominare i file in /boot come si vuole. Tuttavia, usare lo schema [kernel-major-minor-revision] aiuta a mantenere un ordine se si hanno kernel multipli, si usa spesso mkinitcpio, si compilano moduli di terze parti.

Se si sta usando LILO e questo non riesce a comunicare con il driver device-mapper del kernel, si esegua prima `modprobe dm-mod`.

### Copiare System.map

Il file System.map non è richiesto per l'avvio di Linux. È una sorta di "elenco telefonico" in cui sono elencate le funzioni si una particolare compilazione del kernel. System.map contiene una lista dei simboli del kernel (per esempio i nomi delle funzioni, i nomi delle variabili ecc...) e i loro indirizzi corrispondenti. Questo "symbol-name to address mapping" è usato da:

*   Alcuni processi come klogd, ksymoops ecc
*   Dal OOPS handler quando l'informazione deve essere scaricata su schermo durante un crash del kernel (ad esempio informazioni come in quale funzione è crashato).

Copiare System.map in /boot e creare un symlink

```
# cp System.map /boot/System.map-NomeTuoKernel

```

Dopo aver completato i passi qui sopra, si dovrebbero avere i 3 file seguenti ed 1 soft symlink nella propria cartella /boot insieme agli altri file già esistenti:

```
vmlinuz-NomeTuoKernel          (Kernel)
initramfs-NomeTuoKernel.img    (Ramdisk)
System.map-NomeTuoKernel       (System Map)

```

## Configurazione del bootloader

Aggiungere una voce per il nuovo kernel nel file di configurazione del proprio bootloader - vedere [GRUB](/index.php/GRUB_Legacy_(Italiano) "GRUB Legacy (Italiano)"), [LILO](/index.php/LILO "LILO"), [GRUB2](/index.php/GRUB2_(Italiano) "GRUB2 (Italiano)") o [Syslinux](/index.php/Syslinux "Syslinux") come esempi. Notare che, se si usa LILO, il sorgente del kernel include uno script per automatizzare il processo:

```
$ arch/i386/boot/install.sh

```

Se si usa LILO, ricordarsi di digitare `lilo` come root al prompt per aggiornarlo.

## Usare il driver video NVIDIA con il proprio kernel personalizzato

Vedere: [Installazione alternativa: kernel personalizzato](/index.php/NVIDIA_(Italiano)#Installazione_alternativa:_kernel_personalizzato "NVIDIA (Italiano)"). Si possono anche installare i driver NVIDIA da AUR.