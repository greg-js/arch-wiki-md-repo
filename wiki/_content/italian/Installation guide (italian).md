Questo documento vuole essere una guida per l'installazione di [Arch Linux](/index.php/Arch_Linux_(Italiano) "Arch Linux (Italiano)") utilizzando un sistema *live* avviato con l'immagine ufficiale di installazione. Prima di installare, è consigliato dare una lettura alle [FAQ](/index.php/FAQ_(Italiano) "FAQ (Italiano)"). Per le convenzioni usate leggere [Help:Reading](/index.php/Help:Reading "Help:Reading").

Per istruzioni piu` dettagliate sui vari programmi vedere le rispettive [man page](/index.php/Man_page "Man page") e le rispettive pagine [ArchWiki](/index.php/ArchWiki:About_(Italiano) "ArchWiki:About (Italiano)") che normalmente verranno linkate di volta in volta nella guida. Per un aiuto piu` interattivo si possono sfruttare i [canali IRC](/index.php/IRC_channel "IRC channel"), il [forum internazionale](https://bbs.archlinux.org/) e il [forum italiano](https://www.archlinux.it/forum/).

## Contents

*   [1 Prima dell'installazione](#Prima_dell.27installazione)
    *   [1.1 Impostare il corretto layout della tastiera](#Impostare_il_corretto_layout_della_tastiera)
    *   [1.2 Verificare il boot mode](#Verificare_il_boot_mode)
    *   [1.3 Connettersi ad Internet](#Connettersi_ad_Internet)
    *   [1.4 Aggiornare l'orologio di sistema](#Aggiornare_l.27orologio_di_sistema)
    *   [1.5 Partizionare il disco](#Partizionare_il_disco)
    *   [1.6 Formattare le partizioni](#Formattare_le_partizioni)
    *   [1.7 Mount the file systems](#Mount_the_file_systems)
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

Arch Linux dovrebbe essere installabile su ogni macchina compatibile con l'architettura [x86_64](https://en.wikipedia.org/wiki/X86-64 "w:X86-64") e con un minimo di 512 MB di RAM. L'installazione base con solo i pacchetti presenti nel gruppo [base](https://www.archlinux.org/groups/x86_64/base/) richiede circa 800 MB di spazio su disco rigido. Siccome durante la fase di installazione vengono scaricati i pacchetti aggiornati direttamente dai repository remoti, una connessione ad internet e` fondamentale durante il processo.

Scaricare e avviare un disco di installazione come spiegato in [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch"). Ora ci si dovrebbe trovare di fronte ad una [console virtuale](https://en.wikipedia.org/wiki/Virtual_Console "w:Virtual Console"). L'utente *root* dovrebbe gia` essere loggato. La shell di default e` [Zsh](/index.php/Zsh "Zsh"). I comandi piu` comuni come [systemctl(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1) possono essere [autocompletati](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion") dal tasto *tab*.

Per switchare su un'altra console - per esempio per visualizzare questa guida tramite [ELinks](/index.php/ELinks "ELinks") durante il processo di installazione - usare la [combinazione di tasti](/index.php/Keyboard_shortcuts "Keyboard shortcuts") `Alt+*freccia*`. Per [editare](/index.php/Textedit "Textedit") testo e files sono disponibili gli editor: [nano](/index.php/Nano#Usage "Nano"), [vi](https://en.wikipedia.org/wiki/vi "w:vi") e [vim](/index.php/Vim#Usage "Vim").

### Impostare il corretto layout della tastiera

Di default la tastiera e` [mappata](/index.php/Console_keymap "Console keymap") su un layout [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "w:File:KB United States-NoAltGr.svg"). La lista dei possibili layout e` disponibile tramite `ls /usr/share/kbd/keymaps/**/*.map.gz`. Per modificare il layout aggiungere il rispettivo filename a [loadkeys(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1), omettendo estensione e percorso completo. Ad esempio, il comando `loadkeys it` impostera` sul sistema il layout italiano.

I [font](/index.php/Console_fonts "Console fonts") utilizzabili sulla console si trovano in `/usr/share/kbd/consolefonts/` e possono essere selezionati tramite [setfont(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8).

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

Per connessioni **wireless**, [iw(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/iw.8), [wpa_supplicant(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_supplicant.8) e [netctl](/index.php/Netctl#Wireless_.28WPA-PSK.29 "Netctl") sono disponibili. Vedere [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") per ulteriori informazioni.

### Aggiornare l'orologio di sistema

Usare il comando [timedatectl(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) per assicurarsi che l'orologio sia corretto:

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
*   Se [UEFI](/index.php/UEFI "UEFI") e` abilitato, una [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition").

Opzionalmente una partizione di [Swap](/index.php/Swap_(Italiano) "Swap (Italiano)") puo` essere impostata.

Per modificare la *tabella delle partizioni*, usare [fdisk](/index.php/Fdisk "Fdisk") o [parted](/index.php/Parted "Parted"). Vedere [Partitioning](/index.php/Partitioning "Partitioning") per informazioni piu` accurate.

Se si necessita di [LVM](/index.php/LVM "LVM"), [disk encryption](/index.php/Disk_encryption "Disk encryption") o [RAID](/index.php/RAID "RAID"), agire ora.

### Formattare le partizioni

Una volta che le partizioni sono state create, vanno formattate con un [file system](/index.php/File_system "File system") appropriato. Per esempio, per formattare la root su `/dev/*sda1*` in `*ext4*`, il comando e`:

```
# mkfs.*ext4* /dev/*sda1*

```

Vedere [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems") per dettagli.

### Mount the file systems

[Montare](/index.php/Mount "Mount") il filesiste della partizione di root in `/mnt`, per esempio:

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

Usare [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) per installare il gruppo di pacchetti [base](https://www.archlinux.org/groups/x86_64/base/):

```
# pacstrap /mnt base 

```

Questo gruppo non include tutti i pacchetti disponibili sulla live come [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) o firmware per specifiche schede di rete; vedere [packages.both](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both) per informazioni.

Per [installare](/index.php/Install "Install") altri pacchetti o altri gruppi come ad esempio [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) aggiungere a i loro nomi a *pacstrap* separati da spazi, ad esempio:

```
# pacstrap /mnt base base-devel

```

o usare direttamente [pacman](/index.php/Pacman "Pacman") dopo lo step [#Chroot](#Chroot).

## Configurare il sistema

### Fstab

Generare un file [fstab](/index.php/Fstab_(Italiano) "Fstab (Italiano)") (usare `-U` o `-L` per definire ci si vuole riferire alla partizioni con [UUID](/index.php/UUID "UUID") o labels rispettivamente):

```
# genfstab -p /mnt >> /mnt/etc/fstab

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

Lanciare [hwclock(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8) per generare `/etc/adjtime`:

```
# hwclock --systohc

```

Questo comando assume che il proprio orologio hardware sia impostato su [UTC](https://en.wikipedia.org/wiki/UTC). Per dettagli vedere [Time#Time standard](/index.php/Time#Time_standard "Time").

### Locale

Decommentare `en_US.UTF-8 UTF-8` e altre [localizzazioni](/index.php/Localization "Localization") necessarie in `/etc/locale.gen` e generarle con:

```
# locale-gen

```

Settare la [variabile](/index.php/Variable "Variable") `LANG` in [locale.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5), ad esempio:

 `/etc/locale.conf`  `LANG=*it_IT.UTF-8*` 

Se si e` [settato un layout della tastiera](#Impostare_il_corretto_layout_della_tastiera), rendere persistente questa modifica in [vconsole.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5):

 `/etc/vconsole.conf`  `KEYMAP=*us'*` 

### Hostname

Creare il file [hostname(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.5):

 `/etc/hostname` 
```
*mio_hostname*

```

Aggiungere il proprio hostname anche al file [hosts(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5):

 `/etc/hosts` 
```
127.0.0.1	localhost.localdomain	localhost
::1		localhost.localdomain	localhost
**127.0.1.1	*mio_hostname*.localdomain	*mio_hostname***

```

Per informazioni piu` approfondite vedere [Network configuration#Set the hostname](/index.php/Network_configuration#Set_the_hostname "Network configuration").

### Configurazione della rete

Il nuovo sistema installato non ha nessuna connessione attiva di default. Vedere [Network configuration#Network managers](/index.php/Network_configuration#Network_managers "Network configuration").

Per [configurare reti wireless](/index.php/Wireless_configuration "Wireless configuration"), [installare](/index.php/Install "Install") il pacchetto [iw](https://www.archlinux.org/packages/?name=iw) e [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant). Opzionalmente installare [dialog](https://www.archlinux.org/packages/?name=dialog) per poter usare *wifi-menu*.

### Initramfs

Creare una nuova *initramfs* normalmente non e` richiesto, in quanto [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") viene richiamato ad ogni installazione del pacchetto [linux](https://www.archlinux.org/packages/?name=linux) tramite *pacstrap*.

Per configuazioni speciali, modificare il file [mkinitcpio.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.conf.5) e ricreare la initramfs a mano con il comando:

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

Opzionalmente smontare a mano le partizioni con `umount -R /mnt`: questo potrebbe portare a qualche warning di partizione "busy" (occupata, quindi impossibile da smontare), trovarne la causa con [fuser(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1).

Riavviare la macchina con un `reboot`. Tutte le partizioni vengono smontate automaticamente da systemd. Ricordare di rimuovere il *media* di installazione e di loggarsi sulla nuova Arch Linux tramite l'utente root appena creato.

## Post-Installazione

Vedere [General recommendations](/index.php/General_recommendations "General recommendations") per la gestione del sistema e per tutorials post installazione (gestione di utenti, interfacce grafiche, suoni, configurazione di eventuali touchpad...)

Per una lista di applicazioni che potrebbero tornare utili leggere: [List of applications](/index.php/List_of_applications "List of applications").