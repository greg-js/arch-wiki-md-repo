Questo documento vuole essere una guida per l'installazione di [Arch Linux](/index.php/Arch_Linux_(Italiano) "Arch Linux (Italiano)") utilizzando un sistema *live* avviato con l'immagine ufficiale di installazione. Prima di installare, è consigliato dare una lettura alle [FAQ (Italiano)](/index.php/FAQ_(Italiano) "FAQ (Italiano)").

L'[Arch wiki](/index.php/Main_page_(Italiano) "Main page (Italiano)") mantenuto dalla community è una risorsa eccellente e deve essere la prima risorsa da consultare in caso di problemi. Sono disponibili anche il canale [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") ed il [forum italiano](http://www.archlinux.it/forum/) o [internazionale](https://bbs.archlinux.org/) per ricercare ulteriori risposte. Inoltre, assicurarsi di leggere le pagine [man page](/index.php/Man_page "Man page") per qualsiasi comando sconosciuto. Per farsi un'idea di massima sulla configurazione necessaria e` possibile consultare [archlinux(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/archlinux.7).

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
    *   [2.1 Configurare il sistema](#Configurare_il_sistema)
    *   [2.2 Installare e configurare un boot loader](#Installare_e_configurare_un_boot_loader)
    *   [2.3 Smontare le partizioni montate](#Smontare_le_partizioni_montate)
*   [3 Post-Installazione](#Post-Installazione)
    *   [3.1 Gestione Utenti](#Gestione_Utenti)
    *   [3.2 Gestione dei Pacchetti](#Gestione_dei_Pacchetti)
    *   [3.3 Gestione dei Servizi](#Gestione_dei_Servizi)
    *   [3.4 Suono](#Suono)
    *   [3.5 Display server](#Display_server)
    *   [3.6 Font](#Font)
*   [4 Appendice](#Appendice)

## Prima dell'installazione

Arch Linux dovrebbe essere installabile su ogni macchina compatibile con l'architetture [x86_64](https://en.wikipedia.org/wiki/X86-64 "w:X86-64") e con un minimo di 512 MB di RAM. L'installazione base con solo i pacchetti presenti nel gruppo [base](https://www.archlinux.org/groups/x86_64/base/) richiede circa 800 MB di spazio su disco rigido. Siccome durante la fase di installazione vengono scaricati i pacchetti aggiornati direttamente dai repository remoti, una connessione ad internet e` fondamentale durante il processo.

Scaricare e avviare un disco di installazione come spiegato in [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch"). Ora ci si dovrebbe trovare di fronte ad una [console virtuale](https://en.wikipedia.org/wiki/Virtual_Console "w:Virtual Console"). L'utente *root* dovrebbe gia` essere loggato. La shell di default e` [Zsh](/index.php/Zsh "Zsh"). I comandi piu` comuni come [systemctl(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1) possono essere [autocompletati](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion") dal tasto *tab*.

Per switchare su un'altra console - per esempio per visualizzare questa guida tramite [elinks](/index.php/Elinks "Elinks") durante il processo di installazione - usare la [combinazione di tasti](/index.php/Keyboard_shortcuts "Keyboard shortcuts") `Alt+*freccia*`. Per [editare](/index.php/Textedit "Textedit") testo e files [nano](/index.php/Nano#Usage "Nano"), [vi](https://en.wikipedia.org/wiki/vi "w:vi") e [vim](/index.php/Vim#Usage "Vim") sono disponibili.

### Impostare il corretto layout della tastiera

Di default la tastiera e` [mappata](/index.php/Console_keymap "Console keymap") su un layout [statunitense](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "w:File:KB United States-NoAltGr.svg"). La lista dei possibili layout e` disponibile tramite `ls /usr/share/kbd/keymaps/**/*.map.gz`. Per modificare il layout aggiungere il rispettivo filename a [loadkeys(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1), omettendo estensione e percorso completo. Ad esempio, il comando `loadkeys it` impostera` sul sistema il layout italiano.

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

Prima di procedere è necessario modificare il file `/etc/pacman.d/mirrorlist` per usare i [mirror](/index.php/Mirrors_(Italiano) "Mirrors (Italiano)") di vostro gradimento. Questa copia del mirrorlist sarà pure installato sul vostro nuovo sistema da `pacstrap`, quindi conviene impostarlo come si deve.

Utilizzando lo script [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) potete installare il sistema base.

```
# pacstrap /mnt base 

```

Altri pacchetti possono essere installati aggiungendo i loro nomi al comando precedente (separati da uno spazio), incluso il bootloader che si desidera.

### Configurare il sistema

*   Generare un file [fstab](/index.php/Fstab_(Italiano) "Fstab (Italiano)") con il seguente comando (sarebbe preferibile utilizzare come nomenclatura gli UUID o i label, nel caso aggiungere rispettivamente le opzioni `-U` o `-L`):

	 `# genfstab -p /mnt >> /mnt/etc/fstab` 

*   Effettuare un [chroot](/index.php/Chroot "Chroot") nel nostro nuovo sistema appena installato:

	 `# arch-chroot /mnt` 

*   Scrivere il proprio hostname in `/etc/hostname`.
*   Creare un link simbolico di `/usr/share/zoneinfo/Zone/SubZone` in `/etc/localtime` . Rimpiazzare `Zone` e `Subzone` in base alle vostre esigenze. Per esempio:

	 `# ln -s /usr/share/zoneinfo/Europe/Rome /etc/localtime` 

*   De-commentare i *locale* che si vuole utilizzare in `/etc/locale.gen` e generarlo con il comando `locale-gen`.
*   Impostare le proprie [preferenze sul locale](/index.php/Locale_(Italiano)#Impostare_il_locale_a_livello_di_sistema "Locale (Italiano)") in `/etc/locale.conf`.
*   Aggiungere un [font](/index.php/Fonts#Console_fonts "Fonts") e una [mappatura della tastiera](/index.php/KEYMAP "KEYMAP") che si desidera utilizzare per la console in `/etc/vconsole.conf`
*   Configurare `/etc/mkinitcpio.conf` in base alle proprie esigenze (si legga [mkinitcpio](/index.php/Mkinitcpio_(Italiano) "Mkinitcpio (Italiano)")) e creare un RAM disk iniziale con:

	 `# mkinitcpio -p linux` 

*   Impostare una password di *root* con `passwd`.
*   Configurare nuovamente la connessione di rete per l'ambiente appena installato. Si consultino [Configurazione della Rete](/index.php/Configurazione_della_Rete "Configurazione della Rete") e [Wireless Setup](/index.php/Wireless_Setup_(Italiano) "Wireless Setup (Italiano)").

### Installare e configurare un boot loader

Si veda la pagina [Boot loaders](/index.php/Boot_loaders "Boot loaders") per le scelte disponibili.

### Smontare le partizioni montate

Se si è ancora in ambiente environment, digitare prima di tutto `exit` o `Ctrl+D` per uscire da chroot. Prima si sono montate le partizioni sotto `/mnt`. In questa fase procederemo a smontarle tutte.

```
# umount -R /mnt

```

Si riavvii il sistema e si prosegua nella configurazione del proprio sistema.

## Post-Installazione

### Gestione Utenti

Aggiungere gli account utente che si richiedono come come descritto in [Gestione degli utenti](/index.php/Users_and_groups_(Italiano)#Gestione_degli_utenti "Users and groups (Italiano)"). Non è consigliabile utilizzare l'account di root per un uso regolare, o esporlo tramite [SSH](/index.php/Secure_Shell_(Italiano) "Secure Shell (Italiano)") su un server. L'account di root deve essere utilizzato solo per le attività amministrative.

### Gestione dei Pacchetti

Leggere [Pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)") e [FAQ-Gestione dei Pacchettiper](/index.php/FAQ_(Italiano)#Gestione_Pacchetti "FAQ (Italiano)") avere le risposte in materia di installazione dei pacchetti, l'aggiornamento e la gestione.

### Gestione dei Servizi

Arch Linux usa come init [systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)"), he è il sistema responsabile dei servizi per Linux. Per mantenere la vostra installazione di Arch Linux, è una buona idea per imparare le basi sul suo utilizzo. L'interazione con systemd è fatto attraverso il comando `systemctl`. Si legga [Uso base di systemctl](/index.php/Systemd_(Italiano)#Uso_base_di_systemctl "Systemd (Italiano)") per ulteriori informazioni.

### Suono

[ALSA](/index.php/Advanced_Linux_Sound_Architecture_(Italiano) "Advanced Linux Sound Architecture (Italiano)") di solito funziona automaticamente. Ha bisogno solo di essere riattivato. Installare [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) (che contiene `alsamixer`) e seguire [queste](/index.php/Advanced_Linux_Sound_Architecture_(Italiano)#Togliere_il_muto_ai_canali "Advanced Linux Sound Architecture (Italiano)") istruzioni.

ALSA è incluso con il kernel ed è raccomandato. Se non dovesse funzionare, [OSS](/index.php/Open_Sound_System_(Italiano) "Open Sound System (Italiano)") è una valida alternativa. Se si dispone di avanzati requisiti audio, dare un'occhiata al [sistema audio](/index.php/Sound_system_(Italiano) "Sound system (Italiano)") per una panoramica dei vari articoli.

### Display server

L'X Window System (comunemente chiamato **X11**, o semplicemente **X**) consente di disegnare su schermo le finestre. Fornisce il toolkit standard per visualizzare interfacce utente grafiche (Graphical User Interface, GUI). Si veda [Xorg](/index.php/Xorg_(Italiano) "Xorg (Italiano)") per maggiori informazioni.

[Wayland](/index.php/Wayland "Wayland") è un nuovo protocollo server display e l'implementazione di riferimento Weston è disponibile. Il supporto per le applicazioni è molto scarsa in questa fase iniziale di sviluppo.

### Font

Si potrebbe desiderare di installare un set di caratteri TrueType, in quanto solo font bitmap non scalabili sono inclusi di default. Dejavu è un font di uso generico di alta qualità e con una buona copertura [Unicode](https://en.wikipedia.org/wiki/it:Unicode "wikipedia:it:Unicode") :

```
# pacman -S ttf-dejavu

```

Fare riferimento a [Font Configuration](/index.php/Font_configuration_(Italiano) "Font configuration (Italiano)") per sapere come configurare il rendering dei font e a [Fonts](/index.php/Fonts_(Italiano) "Fonts (Italiano)") per i suggerimenti sui tipi di caratteri e le istruzioni di installazione.

## Appendice

Per un elenco dei programmi maggiormente utilizzati e si veda l'articolo [applicazioni comuni](/index.php/List_of_applications_(Italiano) "List of applications (Italiano)").

Si veda anche [Raccomandazioni Generali](/index.php/Raccomandazioni_Generali "Raccomandazioni Generali") per consigli post-installazione, come la configurazione del touchpad o il rendering dei font.