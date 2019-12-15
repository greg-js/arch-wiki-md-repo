Questo documento vuole essere una guida per l'installazione di [Arch Linux](/index.php/Arch_Linux_(Italiano) "Arch Linux (Italiano)") utilizzando un sistema *live* avviato con l'immagine ufficiale di installazione. Prima di installare, è consigliato dare una lettura alle [FAQ](/index.php/FAQ_(Italiano) "FAQ (Italiano)"). Per le convenzioni usate leggere [Help:Reading](/index.php/Help:Reading "Help:Reading"). In particolare, gli esempi di codice potrebbero contenere dei segnaposto (formattati in `*corsivo*`) che devono essere sostituiti manualmente.

Per istruzioni più dettagliate sui vari programmi vedere le rispettive pagine [ArchWiki](/index.php/ArchWiki:About_(Italiano) "ArchWiki:About (Italiano)") e le [man page](/index.php/Man_page "Man page") dei programmi, entrambe linkate in questa guida. Per un aiuto interattivo sono anche disponibili i [canali IRC](/index.php/IRC_channel "IRC channel"), il [forum internazionale](https://bbs.archlinux.org/) e il [forum italiano](https://www.archlinux.it/forum/).

Arch Linux dovrebbe eseguirsi su qualsiasi computer compatibile [x86_64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64") con un minimo di 512 MiB di RAM. Un'installazione basilare dovrebbe occupare meno di 800 MiB di spazio su disco. Poiché il processo di installazione necessita di recuperare pacchetti da un repository remoto, questa guida assume la presenza di una connessione internet funzionante.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Prima dell'installazione](#Prima_dell'installazione)
    *   [1.1 Verifica della firma](#Verifica_della_firma)
    *   [1.2 Avvio dell'ambiente live](#Avvio_dell'ambiente_live)
    *   [1.3 Impostare il corretto layout della tastiera](#Impostare_il_corretto_layout_della_tastiera)
    *   [1.4 Verificare la modalità di boot](#Verificare_la_modalità_di_boot)
    *   [1.5 Connettersi ad Internet](#Connettersi_ad_Internet)
    *   [1.6 Aggiornare l'orologio di sistema](#Aggiornare_l'orologio_di_sistema)
    *   [1.7 Partizionare il disco](#Partizionare_il_disco)
        *   [1.7.1 Disposizioni di esempio](#Disposizioni_di_esempio)
    *   [1.8 Formattare le partizioni](#Formattare_le_partizioni)
    *   [1.9 Montare il file system](#Montare_il_file_system)
*   [2 Installazione](#Installazione)
    *   [2.1 Selezionare il mirror corretto](#Selezionare_il_mirror_corretto)
    *   [2.2 Installare i pacchetti essenziali](#Installare_i_pacchetti_essenziali)
*   [3 Configurare il sistema](#Configurare_il_sistema)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Time zone](#Time_zone)
    *   [3.4 Locale](#Locale)
    *   [3.5 Configurazione della rete](#Configurazione_della_rete)
    *   [3.6 Initramfs](#Initramfs)
    *   [3.7 Password di root](#Password_di_root)
    *   [3.8 Boot loader](#Boot_loader)
*   [4 Reboot](#Reboot)
*   [5 Post-Installazione](#Post-Installazione)

## Prima dell'installazione

Il supporto di installazione e le sue firme [GnuPG](/index.php/GnuPG "GnuPG") possono essere ottenute dalla pagina [Download](https://archlinux.org/download/).

### Verifica della firma

E' raccomandata la verifica della firma dell'immagine prima dell'utilizzo, specialmente se è stata scaricata da un *mirror HTTP*, dove i download possono essere soggetti ad intercettazioni per [fornire immagini malevoli](https://www2.cs.arizona.edu/stork/packagemanagersecurity/attacks-on-package-managers.html).

Su un sistema con [GnuPG](/index.php/GnuPG "GnuPG") installato, eseguire il comando seguente per scaricare la *firma PGP* (sotto *Checksums*) nella directory col file ISO, e [verificarla](/index.php/GnuPG#Verify_a_signature "GnuPG") con:

```
$ gpg --keyserver-options auto-key-retrieve --verify archlinux-*version*-x86_64.iso.sig

```

In alternativa, da un'installazione esistente di Arch Linux eseguire:

```
$ pacman-key -v archlinux-*version*-x86_64.iso.sig

```

**Note:**

*   La stessa firma potrebbe essere stata manipolata se è stata scaricata da un sito mirror, anziché dalla pagina [archlinux.org](https://archlinux.org/download/) come indicato sopra. In questo caso, assicurarsi che la chiave pubblica, che è utilizzata per decifrare la firma, sia firmata da un'altra chiave di fiducia. Il comando `gpg` riporterà l'impronta (fingerprint) della chiave pubblica.
*   Un altro metodo per verificare l'autenticità della firma è assicurarsi che l'impronta della chiave pubblica sia identica all'impronta della chiave dello [Sviluppatore di Arch Linux](https://www.archlinux.org/people/developers/) che ha firmato il file ISO. Vedi [Wikipedia:Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography "wikipedia:Public-key cryptography") per avere più informazioni sul processo chiave pubblica per autentica delle chiavi.

### Avvio dell'ambiente live

L'ambiente live può essere avviato da una [memoria USB](/index.php/USB_flash_installation_media "USB flash installation media"), un [disco ottico](/index.php/Optical_disc_drive#Burning "Optical disc drive") o da una rete con [PXE](/index.php/PXE "PXE"). Per una spiegazione sulle alternative del processo di installazione vedere [Category:Installation process](/index.php/Category:Installation_process "Category:Installation process").

*   Impostare il dispositivo di avvio ad un'unità contenente il supporto di installazione di Arch Linux, tipicamente premendo un tasto specifico durante la fase [POST](https://en.wikipedia.org/wiki/Power-on_self_test "wikipedia:Power-on self test"), come indicato sulla schermata di avvio. Fare riferimento al manuale della propria scheda madre per i dettagli.
*   Quando il menu di Arch Linux appare, scegliere l'opzione *Boot Arch Linux* e premere `Enter` per accedere all'ambiente di installazione.
*   Vedere [README.bootparams](https://projects.archlinux.org/archiso.git/tree/docs/README.bootparams) per una lista dei [parametri di avvio](/index.php/Kernel_parameters#Configuration "Kernel parameters"), e [packages.x86_64](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) per una lista dei pacchetti inclusi.
*   Sarai connesso alla prima [virtual console](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") con l'utente root, e sarà presentata una shell [Zsh](/index.php/Zsh "Zsh").

Per cambiare ad una console differente, per esempio, per vedere questa guida con [ELinks](/index.php/ELinks "ELinks") durante l'installazione, utilizzare la [scorciatoia](/index.php/Keyboard_shortcuts "Keyboard shortcuts") `Alt+*arrow*`. Per [modificare](/index.php/Textedit "Textedit") file di configurazione sono disponibili [nano](/index.php/Nano#Usage "Nano"), [vi](https://en.wikipedia.org/wiki/vi "wikipedia:vi") e [vim](/index.php/Vim#Usage "Vim").

### Impostare il corretto layout della tastiera

La [mappatura della tastiera](/index.php/Console_keymap "Console keymap") predefinita è quella [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg"). Le disposizioni alternative possono essere elencate con:

```
# ls /usr/share/kbd/keymaps/**/*.map.gz

```

Per modificare la disposizione, aggiungere un nome di file corrispondente al comando [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1), omettendo percorso ed estensione. Per esempio, per impostare una disposizione di tastiera [tedesca](https://en.wikipedia.org/wiki/File:KB_Germany.svg "wikipedia:File:KB Germany.svg"):

```
# loadkeys de-latin1

```

I [font utilizzabili nella console](/index.php/Console_fonts "Console fonts") si trovano su `/usr/share/kbd/consolefonts/` e possono essere impostati analogamente con [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8).

### Verificare la modalità di boot

Se la modalità UEFI è attivata in una scheda madre [UEFI](/index.php/UEFI "UEFI"), [Archiso](/index.php/Archiso "Archiso") [avvierà](/index.php/Boot "Boot") Arch Linux tramite [systemd-boot](/index.php/Systemd-boot "Systemd-boot"). Per verificare, elencare la directory [efivars](/index.php/UEFI#UEFI_variables "UEFI"):

```
# ls /sys/firmware/efi/efivars

```

Se la directory non esiste, il sistema potrebbe essere avviato in modalità [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") o CSM. Fare riferimento al manuale della scheda madre per i dettagli.

### Connettersi ad Internet

Per impostare una connessione di rete, eseguire i passaggi seguenti:

*   Assicurarsi che l'[interfaccia di rete](/index.php/Network_interface "Network interface") sia elencata ed abilitata, per esempio con [ip-link(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-link.8): `# ip link` 
*   Connettersi alla rete. Inserire il cavetto Ethernet o [connettersi alla LAN wireless](/index.php/Wireless_network_configuration "Wireless network configuration").
*   Configurare la connessione di rete:
    *   [Indirizzo IP statico](/index.php/Network_configuration#Static_IP_address "Network configuration")
    *   Indirizzo IP dinamico: utilizzare [DHCP](/index.php/DHCP "DHCP").

    **Note:** L'immagine di nstallazione attiva [dhcpcd](/index.php/Dhcpcd "Dhcpcd") (`dhcpcd@*interface*.service`) per le [periferiche di rete con cavo](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) all'avvio.

*   La conessione può essere verificata usando [ping](https://en.wikipedia.org/wiki/ping "wikipedia:ping"): `# ping archlinux.org` 

### Aggiornare l'orologio di sistema

Utilizzare il comando [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) per assicurarsi che l'orologio sia corretto:

```
# timedatectl set-ntp true

```

Per controllare lo status del servizio, utilizzare `timedatectl status`.

### Partizionare il disco

Quando riconosciuti dal sistema live, i dischi sono assegnati a [dispositivi a blocchi](/index.php/Block_device "Block device") come `/dev/sda` or `/dev/nvme0n1`. Per identificare questi dispositivi, utilizzare [lsblk](/index.php/Lsblk "Lsblk") o *fdisk*.

```
# fdisk -l

```

I risultati che terminano con `rom`, `loop` o `airoot` potrebbero essere ignorati.

Le seguenti [partizioni](/index.php/Partitions "Partitions") sono **richieste** su un dispositivo a scelta:

*   Una partizione per la directory radice `/`.
*   Se [UEFI](/index.php/UEFI "UEFI") è attivato, una [partizione di sistema EFI](/index.php/EFI_system_partition "EFI system partition").

Se si desidera creare un dispositivo a blocchi a cascata per [LVM](/index.php/LVM "LVM"), per la [cifratura del sistema](/index.php/Dm-crypt "Dm-crypt") o per [RAID](/index.php/RAID "RAID"), è necessario farlo adesso.

#### Disposizioni di esempio

| BIOS con [MBR](/index.php/MBR "MBR") |
| Punto di montaggio | Partizione | [Tipo di partizione](https://en.wikipedia.org/wiki/Partition_type "wikipedia:Partition type") | Dimensione suggerita |
| `/mnt` | `/dev/sd*X*1` | Linux | Resto del dispositivo |
| [SWAP] | `/dev/sd*X*2` | Linux swap | Più di 512 MiB |
| UEFI con [GPT](/index.php/GPT "GPT") |
| Punto di montaggio | Partizione | [Tipo di partizione](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table") | Dimensione suggerita |
| `/mnt/boot` or `/mnt/efi` | `/dev/sd*X*1` | [EFI system partition](/index.php/EFI_system_partition "EFI system partition") | 260–512 MiB |
| `/mnt` | `/dev/sd*X*2` | Linux x86-64 root (/) | Resto del dispositivo |
| [SWAP] | `/dev/sd*X*3` | Linux swap | Più di 512 MiB |

Vedere anche [Partitioning#Example layouts](/index.php/Partitioning#Example_layouts "Partitioning").

**Note:**

*   Utilizzare [fdisk](/index.php/Fdisk "Fdisk") o [parted](/index.php/Parted "Parted") per modificare le tabelle delle partizioni, per esempio `fdisk /dev/sd*X*`.
*   Lo spazio di [Swap](/index.php/Swap "Swap") può essere impostato su un [file di swap](/index.php/Swap_file "Swap file") per quei file system che lo supportano.

### Formattare le partizioni

Una volta che le partizioni sono state create, ciascuna deve essere formattata con un [file system](/index.php/File_system "File system") appropriato. Per esempio, se la partizione radice è `/dev/sd*X*1` e conterrà un file system `*ext4*` eseguire:

```
# mkfs.*ext4* /dev/sd*X1*

```

Se hai creato una partizione di swap, inizializzarla *mkswap*:

```
# mkswap /dev/sd*X2*
# swapon /dev/sd*X2*

```

Vedere [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems") per i dettagli.

### Montare il file system

[Montare](/index.php/Mount "Mount") il file system della partizione radice in `/mnt`, per esempio:

```
# mount /dev/sd*X1* /mnt

```

Creare eventuali punti di mount rimanenti (come `/mnt/efi`) e montare le partizioni corrispondenti.

[genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in) successivamente rileverà il file system montato e le partizioni di swap.

## Installazione

### Selezionare il mirror corretto

I pacchetti da installare verranno scaricati da [server mirror](/index.php/Mirrors "Mirrors") che sono definiti in `/etc/pacman.d/mirrorlist`. Sul sistema live, tutti i mirror sono abilitati e sono ordinati in base allo stato di sincronizzazione e alla velocità rilevati al momento della generazione dell'immagine iso.

Il mirror che si troverà più in alto nella lista sarà quello a priorità maggiore quando si andrà a scaricare un pacchetto. Potresti voler modificare questo file, e spostare il mirror più vicino geograficamente in cima alla lista, oppure secondo altri criteri.

Questo file, verrà poi copiato sul nuovo sistema installato da *pacstrap*, pertanto è importante modificarlo correttamente.

### Installare i pacchetti essenziali

Usare [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) per installare il pacchetto [base](https://www.archlinux.org/packages/?name=base), il kernel [linux](https://www.archlinux.org/packages/?name=linux) e i firmware per gli hardware più comuni:

```
# pacstrap /mnt base linux linux-firmware

```

**Tip:** Puoi sostituire il pacchetto [linux](https://www.archlinux.org/packages/?name=linux) con un pacchetto [kernel](/index.php/Kernel "Kernel") a scelta. E' possibile omettere l'installazione del kernel o del pacchetto dei firmware se si è coscienti di ciò che viene fatto.

Il pacchetto [base](https://www.archlinux.org/packages/?name=base) non include tutti gli strumenti presenti sul sistema live di installazione, quindi l'installazione di altri pacchetti potrebbe essere necessaria per avere un sistema base completamente funzionante. In particolare, considerare l'installazione di:

*   utilità utente per la gestione dei [file systems](/index.php/File_systems "File systems") che saranno utilizzati dal sistema,
*   utilità per accedere a partizioni [RAID](/index.php/RAID "RAID") o [LVM](/index.php/LVM "LVM"),
*   firmware specifici per altri dispositivi non inclusi in [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware),
*   software necessari per la [rete](/index.php/Networking "Networking"),
*   un [editor di testo](/index.php/Text_editor "Text editor"),
*   pacchetti per accedere alla documentazione delle pagine [man](/index.php/Man "Man") e [info](/index.php/Info "Info"): [man-db](https://www.archlinux.org/packages/?name=man-db), [man-pages](https://www.archlinux.org/packages/?name=man-pages) e [texinfo](https://www.archlinux.org/packages/?name=texinfo).

Per [installare](/index.php/Install "Install") altri pacchetti o gruppi di pacchetti, aggiungere i nomi (separati da spazio) al comando *pacstrap* precedente o utilizzare [pacman](/index.php/Pacman "Pacman") mentre ci si trova nel [chroot del nuovo sistema](#Chroot). Per confronto, i pacchetti disponibili nel sistema live possono trovarsi su [packages.x86_64](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64).

## Configurare il sistema

### Fstab

Generare un file [fstab](/index.php/Fstab_(Italiano) "Fstab (Italiano)") (usare `-U` o `-L` per definire ci si vuole riferire alla partizioni con [UUID](/index.php/UUID "UUID") o labels rispettivamente):

```
# genfstab -U /mnt >> /mnt/etc/fstab

```

Controllare il risultato in `/mnt/etc/fstab` ed editare in caso di errore.

### Chroot

[Cambiare la radice](/index.php/Chroot "Chroot") nel nuovo sistema:

```
# arch-chroot /mnt

```

### Time zone

Impostare la propria [Time zone](/index.php/Time_zone "Time zone"):

```
# ln -sf /usr/share/zoneinfo/Region/City /etc/localtime

```

Eseguire [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8) per generare `/etc/adjtime`:

```
# hwclock --systohc

```

Questo comando assume che il proprio orologio hardware sia impostato su [UTC](https://en.wikipedia.org/wiki/UTC "wikipedia:UTC"). Per dettagli vedere [System time#Time standard](/index.php/System_time#Time_standard "System time").

### Locale

Decommentare `en_US.UTF-8 UTF-8` e altre [localizzazioni](/index.php/Localization "Localization") necessarie in `/etc/locale.gen` e generarle con:

```
# locale-gen

```

Creare il file [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5), e impostare la [variable](/index.php/Variable "Variable") `LANG`:

 `/etc/locale.conf`  `LANG=*en_US.UTF-8*` 

Se si è [settato un layout della tastiera](#Impostare_il_corretto_layout_della_tastiera), rendere persistente questa modifica in [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5):

 `/etc/vconsole.conf`  `KEYMAP=*it*` 

### Configurazione della rete

Creare il file [hostname(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.5):

 `/etc/hostname` 
```
*mio_hostname*

```

Aggiungere le voci corrispondenti al file [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5):

 `/etc/hosts` 
```
127.0.0.1	localhost
::1		localhost
127.0.1.1	*mio_hostname*.localdomain	*mio_hostname*

```

Se il sistema ha un indirizzo IP permanente, dovrebbe essere indicato anziché `127.0.1.1`.

Completa la [configurazione di rete](/index.php/Network_configuration "Network configuration") per il nuovo ambiente installato, inclusa [l'installazione](/index.php/Install "Install") di pacchetti come [iputils](https://www.archlinux.org/packages/?name=iputils) e il software preferito [per la gestione della rete](/index.php/Network_management "Network management").

### Initramfs

La creazione di un nuovo *initramfs* normalmente non è necessaria, in quanto [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") è stato eseguito durante l'installazione del pacchetto [kernel](/index.php/Kernel "Kernel") con *pacstrap*.

per [LVM](/index.php/LVM#Configure_mkinitcpio "LVM"), [cifratura del sistema](/index.php/Dm-crypt "Dm-crypt") o [RAID](/index.php/RAID#Configure_mkinitcpio "RAID"), modificare [mkinitcpio.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.conf.5) e ricreate l'immagine initramfs:

```
# mkinitcpio -P

```

### Password di root

Impostare una [password](/index.php/Password "Password") per l'utente root:

```
# passwd

```

### Boot loader

Scegliere e installare un [boot loader](/index.php/Boot_loader "Boot loader") compatibile per Linux. Se hai una CPU Intel o AMD, in aggiunta abilita l'aggiornamento del [microcode](/index.php/Microcode "Microcode").

## Reboot

Uscire dall'ambiente chroot con `exit` o premendo `Ctrl+D`.

Opzionalmente smontare a mano le partizioni con `umount -R /mnt`: questo potrebbe portare a qualche warning di partizione "busy" (occupata, quindi impossibile da smontare), trovarne la causa con [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1).

Riavviare la macchina con un `reboot`. Tutte le partizioni vengono smontate automaticamente da systemd. Ricordare di rimuovere il *media* di installazione e di loggarsi sulla nuova Arch Linux tramite l'utente root appena creato.

## Post-Installazione

Vedere [General recommendations](/index.php/General_recommendations "General recommendations") per la gestione del sistema e per tutorials post installazione (gestione di utenti, interfacce grafiche, suoni, configurazione di eventuali touchpad...)

Per una lista di applicazioni che potrebbero tornare utili leggere: [List of applications](/index.php/List_of_applications "List of applications").