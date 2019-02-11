Questa è una guida veloce all'installazione di [TuxOnIce](http://www.tuxonice.net) (conosciuto anche come suspend2), un framework avanzato per la sospensione/ibernazione, che supporta l'ibernazione in una partizione swap o in un normale file con una compressione veloce LZO. Visita il sito di TuxOnIce per una lista completa delle [caratteristiche](http://www.tuxonice.net/features).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Preparazione del kernel](#Preparazione_del_kernel)
*   [2 Ricreare initramfs](#Ricreare_initramfs)
*   [3 Configurazione del Boot Loader](#Configurazione_del_Boot_Loader)
    *   [3.1 Ibernazione in una partizione di Swap](#Ibernazione_in_una_partizione_di_Swap)
    *   [3.2 Ibernazione su un file di swap](#Ibernazione_su_un_file_di_swap)
    *   [3.3 Sospensione su file](#Sospensione_su_file)
*   [4 Sospensione e Resuming](#Sospensione_e_Resuming)
*   [5 Configurazioni addizionali di pm-utils](#Configurazioni_addizionali_di_pm-utils)
*   [6 Usare UserUI - Un'Interfaccia Utente per TuxOnIce (Opzionale)](#Usare_UserUI_-_Un'Interfaccia_Utente_per_TuxOnIce_(Opzionale))
*   [7 Riferimenti](#Riferimenti)

## Preparazione del kernel

TuxOnIce consiste in una patch del kernel, più un'interfaccia utente aggiuntiva. Solo la patch è necessaria, l'interfaccia utente fornisce un'interfaccia testuale o grafica durante il ciclo di sospensione/ibernazione.

È possibile usare il pacchetto [linux-ice](https://aur.archlinux.org/packages/linux-ice/) o [linux-pf](https://aur.archlinux.org/packages/linux-pf/) presenti su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)"). Questo automatizza la procedura di patch, compilazione ed installazione del kernel, e la generazione della initramfs con un hook adeguato. In questo modo si ha un buon controllo del processo di installazione e volendo si può personalizzare apportando i cambiamenti voluti.

Altrimenti, sarà necessario applicare la patch, configurare e compilare il proprio kernel, visitare le pagine [Kernel Compilation From Source](/index.php/Kernel_Compilation_From_Source "Kernel Compilation From Source") e [Kernel Compilation with ABS](/index.php/Kernel_Compilation_with_ABS "Kernel Compilation with ABS") per maggiori informazioni. Le patch necessarie possono essere ottenute presso il sito TuxOnIce di cui sopra.

Ora è necessario installare il pacchetto [hibernate-script](https://aur.archlinux.org/packages/hibernate-script/) da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") che verrà richiamato da TuxOnIce. Questo pacchetto è lo script ufficiale fornito dal team di TuxOnIce.

I file di configurazione di hibernate-script sono in `/etc/hibernate`.

## Ricreare initramfs

Se si vuole usare un initramfs (cosa che Arch fa di default) è necessario aggiungere "resume" agli HOOKS di [mkinitcpio](/index.php/Mkinitcpio_(Italiano) "Mkinitcpio (Italiano)"). In più, se si vuole usare la compressione veloce LZO aggiungere "lzo" all'array MODULES dello stesso file. Un esempio di `/etc/mkinitcpio.conf`:

```
MODULES="lzo"
HOOKS="base udev autodetect block resume filesystems"

```

Ricreare ora l'initramfs:

```
# mkinitcpio -p linux-ice

```

o

```
# mkinitcpio -p linux-pf

```

## Configurazione del Boot Loader

Prima che si possa usare la funzione di sospensione, bisogna aggiungere il parametro `resume` ai parametri passati al kernel nel file di configurazione del boot loader (se si sta usando un sistema con una partizione swap "specificata" nella configurazione del kernel questo passaggio non è necessario). Questo punterà alla partizione di swap o al file di ibernazione.

### Ibernazione in una partizione di Swap

**Note:** A partire l'ultima versione di TuxOnIce (3.0.99.44), aggiungere il parametro "resume" al kernel non è più necessario, sarà rilevato automaticamente se l'unità di swap contiene un'immagine avviabile. Ci sarà solo bisogno di impostare il metodo di swap adeguatamente. Per maggiori informazioni, visitare [[1]](http://www.tuxonice.net/).

Quindi configurare il metodo swap (assicurarsi che sia specificata la partizione giusta) in `/etc/hibernate/tuxonice.conf`

```
SuspendDevice swap:/dev/sda3

```

### Ibernazione su un file di swap

**Note:** L'autorilevamento, come detto in precedenza, non sembra funzionare con i file di swap; sarà dunque necessario impostare manualmente il parametro "resume" del kernel.

Se si utilizza un file di swap invece di una partizione di swap, sarà necessario passare il percorso dei suoi header a TuxOnIce. TuxOnIce è in grado di elencare tutti gli header di swap disponibile.

```
cat /sys/power/tuxonice/swap/headerlocations

```

Utilizzare la stringa data così com'è in `/etc/hibernate/tuxonice.conf` e passarla al kernel come parametro "resume".

```
SuspendDevice swap:/dev/sda7:0x1087070

```

Aggiungere la seguente riga nei parametri del kernel nel file di configurazione del bootloader:

```
resume=swap:/dev/sda7:0x1087070

```

**Note:** Specificare il dispositivo di "resume" per mezzo degli UUID dovrebbe funzionare, ma non è del tutto garantito. Questo potrebbe essere un problema di TuxOnIce o di mkinitcpio. Specificando `/dev/sdxx` dovrebbe invece funzionare in tutti i casi.

### Sospensione su file

Per l'allocatore di file, si dovrà preparare un file di ibernazione. Questo è diverso dal file di swap standard dato che questo file viene utilizzato SOLO per l'ibernazione e non come file di swap del sistema generale. Il metodo precedente è raccomandata per essere più efficiente in termini di spazio su disco. Configurare il file `/etc/hibernate/tuxonice.conf` e decommentare l'opzione "FilewriterLocation":

```
FilewriterLocation /suspend_file 1000

```

1000 è la quantità di spazio su disco riservato per il file di ibernazione, in questo caso 1000 megabyte. Di solito un valore pari al 50%-75% della quantità totale di RAM è sufficiente.

Successivamente, eseguire il seguente comando per creare il file di ibernazione:

```
# hibernate --no-suspend

```

Dare un'occhiata a `/sys/power/tuxonice/resume` per vedere cosa passare al kernel. Si dovrebbe vedere qualche file del genere:`file:/dev/hda7:0x10011f`, nel qual caso si dovrebbe aggiungere `resume=file:/dev/hda7:0x10011f` come parametro del kernel nel file `/etc/lilo.conf` (per [LILO](/index.php/LILO "LILO")) o `/boot/grub/menu.lst` (per [GRUB](/index.php/GRUB_Legacy_(Italiano) "GRUB Legacy (Italiano)")) o `/boot/grub/menu.cfg` (per [GRUB2](/index.php/GRUB2_(Italiano) "GRUB2 (Italiano)")).

## Sospensione e Resuming

Con gli hibernate-script, il metodo di ibernazione preferito può essere configurato nel file `/etc/hibernate/hibernate.conf`. Se si elencano diversi metodi, il primo sarà quello utilizzato. Notare che *hibernate* può essere anche usato con [Suspend to RAM](/index.php/Suspend_to_RAM "Suspend to RAM") o vanilla swsusp, ma questo non è parte della guida.

Per TuxOnIce usare:

```
TryMethod tuxonice.conf

```

Le opzioni specifiche per TuxOnIce sono nel file `/etc/hibernate/tuxonice.conf`. Assicurarsi che le seguenti righe siano decommentate e configurate adeguatamente:

```
UseTuxOnIce yes
Compressor lzo

```

Ci sono altre opzioni aggiuntive e trucchi che possono essere impostati in `/etc/hibernate/tuxonice.conf` e `/etc/hibernate/common.conf`, informazioni più dettagliate possono essere trovate sul sito ufficiale di [TuxOnIce](http://www.tuxonice.net/HOWTO-4.html) o nella pagina [Suspend to Disk](/index.php/Suspend_to_Disk "Suspend to Disk") di questo wiki.

Provare quindi l'ibernazione di TuxOnIce con questo comando:

```
# hibernate -F /etc/hibernate/tuxonice.conf

```

Si può uscire dal ciclo di sospensione premendo il pulsante `Esc`. Premendo `Shift + R`, si forzerà il sistema a riavviarsi dopo l'ibernazione.

Se tutto è andato bene, dovresti essere in grado di effettuare il resuming usando la stessa voce del menù di Grub che usi normalmente per avviare il sistema. Se imposti questa opzione come default, effettuerai sempre il resuming se un file di ibernazione è disponibile su disco o sulla swap. È bene testare la sospensione/ibernazione prima da terminale, e dopo essersi assicurati che funziona, provarla da X.

**Attenzione:** Non usare mai un kernel differente per effettuare il resume da quello che hai usato per l'ibernazione! Se pacman aggiorna il tuo kernel, non ibernare prima che tu abbia riavviato la macchina e avviato il nuovo kernel.

Si può rendere questa pratica più sicura aggiungendo il demone *hibernate-cleanup* nella stringa DAEMONS in `/etc/rc.conf`. Questo script verifica che qualsiasi vecchia immagine per il resume sia cancellata della partizione di swap durante l'avvio. Questo dovrebbe rendere più sicuro il sistema anche nel caso si scelga il kernel sbagliato dal menù di Grub. Il demone hibernate-cleanup è incluso nel pacchetto hibernate-script.

## Configurazioni addizionali di pm-utils

Se si usa [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)") come [DE](/index.php/Desktop_environment_(Italiano) "Desktop environment (Italiano)"), o un qualunque altro DE che richieda [pm-utils](/index.php/Pm-utils_(Italiano) "Pm-utils (Italiano)") per spegnere e sospendere sono necessarie ulteriori configurazioni per TuxOnIce.

Tali configurazioni vanno fatte in `/etc/hibernate/hibernate.conf` e dovrebbero funzionare. Alcune configurazioni però possono dare problemi con pm-utils. La compressione, per esempio, è di default lzo a meno che si intervenga manualmente. Editare il file sotto `/etc/pm/sleep.d/` è un'ottima alternativa per far si che le configurazioni vengano lette correttamente.

Per cambiare la compressione usata da TuxOnIce, per esempio, editare `/etc/pm/sleep.d/00doit` e aggiungere qualcosa del genere:

```
#!/bin/bash
case $1 in
hibernate)
#Possible compressors include lzo, lzf, and none
echo none > /sys/power/tuxonice/compression/algorithm
;;

```

Linee addizionali possono essere usate per cambiare altre opzioni come ad esempio il logging level di default (in `/sys/power/tuxonice/user_interface/default_console_level`).

## Usare UserUI - Un'Interfaccia Utente per TuxOnIce (Opzionale)

È anche possibile utilizzare un'interfaccia utente testuale o grafica ([fbsplash](/index.php/Fbsplash_(Italiano) "Fbsplash (Italiano)")) con una barra di avanzamento. Per fare questo, installare il pacchetto [tuxonice-userui](https://aur.archlinux.org/packages/tuxonice-userui/) da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)"). Questo pacchetto dipende dalla libreria statica freetype2, fornita dal pacchetto [freetype2-static](https://aur.archlinux.org/packages/freetype2-static/) (anche questo da AUR).

Nel file `/etc/hibernate/tuxonice.conf`, imposta l'interfaccia utente desiderata:

```
ProcSetting user_interface/program "/usr/sbin/tuxoniceui"  #Interfaccia Testuale

```

o

```
ProcSetting user_interface/program "/usr/sbin/tuxoniceui -f"  #Interfaccia Grafica con fbsplash

```

L'interfaccia con fbsplash necessita di un symlink al tema fbsplash, in questo modo:

```
# ln -s /etc/splash/arch-banner-noicons/ /etc/splash/tuxonice

```

Senza questo symlink, non ci saranno indicatori di progresso durante il suspend/resume.

Probabilmente sarà necessario rigenerare l'initramfs dopo aver cambiato il link simbolico sopra.

L'interfaccia testuale può essere utile per il debug di TuxOnIce, in quanto visualizza alcuni messaggi.

Non si vedrà un'interfaccia utente durante i primi secondi del processo di ripristino a meno che non si aggiunga l'hook **userui** alla propria configurazione mkinitcpio (prima dell'hook **resume**) e si rigeneri l'initramfs, ma anche questo è opzionale.

Generate initramfs:

```
# mkinitcpio -p linux-ice

```

Per verificare se la userui funziona, da terminale eseguite:

```
# tuxoniceui_test --test

```

Per l'interfaccia grafica eseguite:

```
# tuxoniceui_fbsplash --test

```

## Riferimenti

*   Il sito di [TuxOnIce](http://www.tuxonice.net) e la sua [wiki](http://wiki.tuxonice.net) sono un ottima fonte di informazioni.
*   Altre informazioni generali sulla sospensione/ibernazione con gli hibernate-script si possono trovare nella pagina [Suspend to Disk](/index.php/Suspend_to_Disk "Suspend to Disk") di questa wiki. Questa tratta argomenti avanzati come problemi con certe configurazioni hardware.