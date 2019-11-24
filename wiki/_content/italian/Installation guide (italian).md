Questo documento vuole essere una guida per l'installazione di [Arch Linux](/index.php/Arch_Linux_(Italiano) "Arch Linux (Italiano)") utilizzando un sistema *live* avviato con l'immagine ufficiale di installazione. Prima di installare, è consigliato dare una lettura alle [FAQ](/index.php/FAQ_(Italiano) "FAQ (Italiano)"). Per le convenzioni usate leggere [Help:Reading](/index.php/Help:Reading "Help:Reading"). In particolare, gli esempi di codice potrebbero contenere dei segnaposto (formattati in `*corsivo*`) che devono essere sostituiti manualmente.

Per istruzioni piu` dettagliate sui vari programmi vedere le rispettive pagine [ArchWiki](/index.php/ArchWiki:About_(Italiano) "ArchWiki:About (Italiano)") e le [man page](/index.php/Man_page "Man page") dei programmi, entrambe linkate in questa guida. Per un aiuto interattivo sono anche disponibili i [canali IRC](/index.php/IRC_channel "IRC channel"), il [forum internazionale](https://bbs.archlinux.org/) e il [forum italiano](https://www.archlinux.it/forum/).

Arch Linux dovrebbe eseguirsi su qualsiasi computer compatibile [x86_64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64") con un minimo di 512 MiB di RAM. Un'installazione basilare dovrebbe occupare meno di 800 MiB di spazio su disco. Poiché il processo di installazione necessita di recuperare pacchetti da un repository remoto, questa guida assume la presenza di una connessione internet funzionante.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Prima dell'installazione](#Prima_dell'installazione)
    *   [1.1 Verifica della firma](#Verifica_della_firma)
    *   [1.2 Avvio dell'ambiente live](#Avvio_dell'ambiente_live)
    *   [1.3 Impostare il corretto layout della tastiera](#Impostare_il_corretto_layout_della_tastiera)
    *   [1.4 Verificare il boot mode](#Verificare_il_boot_mode)
    *   [1.5 Connettersi ad Internet](#Connettersi_ad_Internet)
    *   [1.6 Aggiornare l'orologio di sistema](#Aggiornare_l'orologio_di_sistema)
    *   [1.7 Partizionare il disco](#Partizionare_il_disco)
    *   [1.8 Formattare le partizioni](#Formattare_le_partizioni)
    *   [1.9 Montare il file system](#Montare_il_file_system)
*   [2 Installazione](#Installazione)
    *   [2.1 Selezionare il mirror corretto](#Selezionare_il_mirror_corretto)
    *   [2.2 Installare i pacchetti base](#Installare_i_pacchetti_base)
*   [3 Configurare il sistema](#Configurare_il_sistema)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Time zone](#Time_zone)
    *   [3.4 Locale](#Locale)
    *   [3.5 Hostname](#Hostname)
    *   [3.6 Configurazione della rete](#Configurazione_della_rete)
    *   [3.7 Initramfs](#Initramfs)
    *   [3.8 Password di root](#Password_di_root)
    *   [3.9 Boot loader](#Boot_loader)
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

Di default la tastiera e` [mappata](/index.php/Console_keymap "Console keymap") su un layout [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "w:File:KB United States-NoAltGr.svg"). La lista dei possibili layout e` disponibile tramite `ls /usr/share/kbd/keymaps/**/*.map.gz`. Per modificare il layout aggiungere il rispettivo filename a [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1), omettendo estensione e percorso completo. Ad esempio, il comando `loadkeys it` impostera` sul sistema il layout italiano.

I [font](/index.php/Console_fonts "Console fonts") utilizzabili sulla console si trovano in `/usr/share/kbd/consolefonts/` e possono essere selezionati tramite [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8).

### Verificare il boot mode

Se si boota su una scheda madre sulla quale e` abilitato [UEFI](/index.php/UEFI "UEFI"), [Archiso](/index.php/Archiso "Archiso") [avviera`](/index.php/Boot "Boot") Arch Linux di conseguenza tramite [systemd-boot](/index.php/Systemd-boot "Systemd-boot"). Per verificarlo si possono controllare le [efivars](/index.php/UEFI#UEFI_variables "UEFI") directory:

```
 # ls /sys/firmware/efi/efivars

```

Se questa directory non esiste significa che il boot di Arch Linux e` avvenuto in modalita` [BIOS](https://en.wikipedia.org/wiki/BIOS "w:BIOS"). Per ulteriori dettagli fare riferimento alla documentazione della propria scheda madre.

### Connettersi ad Internet

L'immagine di installazione di Arch Linux di default [abilita](/index.php/Enable "Enable") un demone [dhcpcd](/index.php/Dhcpcd "Dhcpcd") per le intefacce [wired](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules). La connessione puo` essere controllata con

```
# ping archlinux.org

```

Se la connessione risulta non disponibile, [fermare](/index.php/Stop "Stop") il servizio *dhcpcd* con `systemctl stop dhcpcd@`, `Tab` e vedere [Network configuration](/index.php/Network_configuration "Network configuration").

Per connessioni **wireless**, [iw(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/iw.8), [wpa_supplicant(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_supplicant.8) e [netctl](/index.php/Netctl#Wireless_.28WPA-PSK.29 "Netctl") sono disponibili. Vedere [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") per ulteriori informazioni.

### Aggiornare l'orologio di sistema

Usare il comando [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) per assicurarsi che l'orologio sia corretto:

```
# timedatectl set-ntp true

```

Per controllare lo status del servizio: `timedatectl status`.

### Partizionare il disco

Quando riconosciuti dal disco di installazione, ai dischi viene associato un *block device* come `/dev/sda`. Per identificare questi devices, usare [lsblk](/index.php/Lsblk "Lsblk") o *fdisk* — i risultati che finiscono con `rom`, `loop` o `airoot` possono essere ignorati:

```
# fdisk -l

```

Le seguenti *partizioni* (mostrate con un suffisso numerico) sono fondamentali:

*   Una partizione per la directory root `/`.
*   Se [UEFI](/index.php/UEFI "UEFI") e` abilitato, una [EFI system partition](/index.php/EFI_system_partition "EFI system partition").

Opzionalmente una partizione di [Swap](/index.php/Swap_(Italiano) "Swap (Italiano)") puo` essere impostata.

Per modificare la *tabella delle partizioni*, usare [fdisk](/index.php/Fdisk "Fdisk") o [parted](/index.php/Parted "Parted"). Vedere [Partitioning](/index.php/Partitioning "Partitioning") per informazioni piu` accurate.

Se si necessita di [LVM](/index.php/LVM "LVM"), [disk encryption](/index.php/Disk_encryption "Disk encryption") o [RAID](/index.php/RAID "RAID"), agire ora.

### Formattare le partizioni

Una volta che le partizioni sono state create, vanno formattate con un [file system](/index.php/File_system "File system") appropriato. Per esempio, per formattare la root su `/dev/*sda1*` in `*ext4*`, il comando e`:

```
# mkfs.*ext4* /dev/*sda1*

```

Vedere [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems") per dettagli.

### Montare il file system

[Montare](/index.php/Mount "Mount") il file system della partizione di root in `/mnt`, per esempio:

```
# mount /dev/*sda1* /mnt

```

Creare i punti di mount delle altre partizioni create e montarle di conseguenza, Ad esempio:

```
# mkdir /mnt/*boot*
# mount /dev/*sda2* /mnt/*boot*

```

[genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in) rilevera` i punti di mount dei file system e della partizione di swap.

## Installazione

### Selezionare il mirror corretto

I pacchetti da installare verranno scaricati da [server mirror](/index.php/Mirrors "Mirrors") che sono definiti in `/etc/pacman.d/mirrorlist`. Sul sistema live, tutti i mirror sono abilitati e sono ordinati in base allo stato di sincronizzazione e alla velocita` rilevati al momento della generazione dell'immagine iso.

Il mirror che si trovera` piu` in alto nella lista sara` quello a priorita` maggiore quando si andra` a scaricare un pacchetto. E` sicuramente buona norma modificare questo file, inserendo in alto i mirror geograficamente piu` vicini all'Italia.

Questo file, verra` poi copiato sul sistema installato da *pacstrap*.

### Installare i pacchetti base

Usare [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) per installare il pacchetto [base](https://www.archlinux.org/packages/?name=base), il kernel [linux](https://www.archlinux.org/packages/?name=linux) e i firmware per gli hardware più comuni:

```
# pacstrap /mnt base linux linux-firmware

```

Questo gruppo non include tutti i pacchetti disponibili sulla live come [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) o firmware per specifiche schede di rete; vedere [packages.both](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both) per informazioni.

Per [installare](/index.php/Install "Install") altri pacchetti o altri gruppi come ad esempio [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) aggiungere a i loro nomi a *pacstrap* separati da spazi, ad esempio:

```
# pacstrap /mnt base linux linux-firmware base-devel

```

o usare direttamente [pacman](/index.php/Pacman "Pacman") dopo lo step [#Chroot](#Chroot).

## Configurare il sistema

### Fstab

Generare un file [fstab](/index.php/Fstab_(Italiano) "Fstab (Italiano)") (usare `-U` o `-L` per definire ci si vuole riferire alla partizioni con [UUID](/index.php/UUID "UUID") o labels rispettivamente):

```
# genfstab -U /mnt >> /mnt/etc/fstab

```

Controllare il risultato in `/mnt/etc/fstab` ed editare in caso di errore.

### Chroot

Effettuare un [chroot](/index.php/Chroot "Chroot") nel nuovo nuovo sistema:

```
# arch-chroot /mnt

```

### Time zone

Settare la propria [Time zone](/index.php/Time_zone "Time zone"):

```
# ln -sf /usr/share/zoneinfo/Region/City /etc/localtime

```

Lanciare [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8) per generare `/etc/adjtime`:

```
# hwclock --systohc

```

Questo comando assume che il proprio orologio hardware sia impostato su [UTC](https://en.wikipedia.org/wiki/UTC "wikipedia:UTC"). Per dettagli vedere [System time#Time standard](/index.php/System_time#Time_standard "System time").

### Locale

Decommentare `en_US.UTF-8 UTF-8` e altre [localizzazioni](/index.php/Localization "Localization") necessarie in `/etc/locale.gen` e generarle con:

```
# locale-gen

```

Settare la [variabile](/index.php/Variable "Variable") `LANG` in [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5), ad esempio:

 `/etc/locale.conf`  `LANG=*it_IT.UTF-8*` 

Se si è [settato un layout della tastiera](#Impostare_il_corretto_layout_della_tastiera), rendere persistente questa modifica in [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5):

 `/etc/vconsole.conf`  `KEYMAP=*it*` 

### Hostname

Creare il file [hostname(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.5):

 `/etc/hostname` 
```
*mio_hostname*

```

Aggiungere il proprio hostname anche al file [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5):

 `/etc/hosts` 
```
127.0.0.1	localhost.localdomain	localhost
::1		localhost.localdomain	localhost
**127.0.1.1	*mio_hostname*.localdomain	*mio_hostname***

```

Per informazioni piu` approfondite vedere [Network configuration#Set the hostname](/index.php/Network_configuration#Set_the_hostname "Network configuration").

### Configurazione della rete

Il nuovo sistema installato non ha nessuna connessione attiva di default. Vedere [Network configuration#Network management](/index.php/Network_configuration#Network_management "Network configuration").

Per [configurare reti wireless](/index.php/Wireless_configuration "Wireless configuration"), [installare](/index.php/Install "Install") il pacchetto [iw](https://www.archlinux.org/packages/?name=iw) e [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant). Opzionalmente installare [dialog](https://www.archlinux.org/packages/?name=dialog) per poter usare *wifi-menu*.

### Initramfs

Creare una nuova *initramfs* normalmente non e` richiesto, in quanto [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") viene richiamato ad ogni installazione del pacchetto [linux](https://www.archlinux.org/packages/?name=linux) tramite *pacstrap*.

Per configuazioni speciali, modificare il file [mkinitcpio.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.conf.5) e ricreare la initramfs a mano con il comando:

```
# mkinitcpio -p linux

```

### Password di root

Impostare una [password](/index.php/Password "Password") per l'utente root:

```
# passwd

```

### Boot loader

Leggere [Category:Boot loaders](/index.php/Category:Boot_loaders "Category:Boot loaders") per vedere quali siano le principali scelte e configurazioni disponibili.

Se si usa una CPU Intel, installare il pacchetto [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) e [abilitare l'aggiornamento del microcode](/index.php/Microcode#Enabling_Intel_microcode_updates "Microcode").

## Reboot

Uscire dall'ambiente chroot con `exit` o premendo `Ctrl+D`.

Opzionalmente smontare a mano le partizioni con `umount -R /mnt`: questo potrebbe portare a qualche warning di partizione "busy" (occupata, quindi impossibile da smontare), trovarne la causa con [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1).

Riavviare la macchina con un `reboot`. Tutte le partizioni vengono smontate automaticamente da systemd. Ricordare di rimuovere il *media* di installazione e di loggarsi sulla nuova Arch Linux tramite l'utente root appena creato.

## Post-Installazione

Vedere [General recommendations](/index.php/General_recommendations "General recommendations") per la gestione del sistema e per tutorials post installazione (gestione di utenti, interfacce grafiche, suoni, configurazione di eventuali touchpad...)

Per una lista di applicazioni che potrebbero tornare utili leggere: [List of applications](/index.php/List_of_applications "List of applications").