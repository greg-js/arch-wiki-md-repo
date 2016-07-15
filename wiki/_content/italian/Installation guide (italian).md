Questo documento vi guiderà attraverso il processo di installazione di [Arch Linux](/index.php/Arch_Linux_(Italiano) "Arch Linux (Italiano)") utilizzando il sistema live avviato con l'immagine ufficiale di installazione. Prima di installare, è consigliato dare una lettura alle [FAQ (Italiano)](/index.php/FAQ_(Italiano) "FAQ (Italiano)").

[Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch") contiene diverse altre guide all'installazione per casi specifici.

L'[Arch wiki](/index.php/Main_page_(Italiano) "Main page (Italiano)") mantenuto dalla community è una risorsa eccellente e deve essere la prima risorsa da consultare in caso di problemi. Sono disponibili anche il canale [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") (per la comunità italiana: [irc://irc.azzurra.org/archlinux](irc://irc.azzurra.org/archlinux) o [irc://irc.freenode.net/#archlinux.it](irc://irc.freenode.net/#archlinux.it), mentre per il supporto internazionale: [irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)), ed il [forum italiano](http://www.archlinux.it/forum/) o [internazionale](https://bbs.archlinux.org/) per ricercare ulteriori risposte. Inoltre, assicurarsi di leggere le pagine `man` per qualsiasi comando sconosciuto; di solito può essere invocato tramite `man "command"`.

## Contents

*   [1 Download](#Download)
*   [2 Installazione](#Installazione)
    *   [2.1 Layout di tastiera](#Layout_di_tastiera)
    *   [2.2 Partizionare i dischi](#Partizionare_i_dischi)
    *   [2.3 Formattare le partizioni](#Formattare_le_partizioni)
    *   [2.4 Montare le partizioni](#Montare_le_partizioni)
    *   [2.5 Connessione alla rete](#Connessione_alla_rete)
        *   [2.5.1 Wireless](#Wireless)
    *   [2.6 Installare il sistema base](#Installare_il_sistema_base)
    *   [2.7 Configurare il sistema](#Configurare_il_sistema)
    *   [2.8 Installare e configurare un boot loader](#Installare_e_configurare_un_boot_loader)
    *   [2.9 Smontare le partizioni montate](#Smontare_le_partizioni_montate)
*   [3 Post-Installazione](#Post-Installazione)
    *   [3.1 Gestione Utenti](#Gestione_Utenti)
    *   [3.2 Gestione dei Pacchetti](#Gestione_dei_Pacchetti)
    *   [3.3 Gestione dei Servizi](#Gestione_dei_Servizi)
    *   [3.4 Suono](#Suono)
    *   [3.5 Display server](#Display_server)
    *   [3.6 Font](#Font)
*   [4 Appendice](#Appendice)

## Download

Scarica la nuova ISO di Arch Linux ISO dalla [pagina di download](http://www.archlinux.it/download/).

*   Viene distribuita una sola immagine da essere utilizzata su architetture i686 e x86_64 per installare Arch Linux tramite la rete. Le immagini che contenevano il repository [core] non sono più distribuite.
*   Le immagini sono firmate ed è altamente raccomandato verificare la firma prima di usarle: questo si può fare scaricando il file *.sig* dalla pagina di download (o uno dei mirror elencati qui ) per la stessa directory del file *.iso* e quindi verificarlo tramite `pacman-key -v *iso-file*.sig`
*   Le immagini possono essere masterizzate su CD, montate come ISO, o scritte direttamente [su penna USB](/index.php/USB_Installation_Media_(Italiano) "USB Installation Media (Italiano)"). Le ISO servono ad installare un nuovo sistema di Arch Linux; un sistema Arch Linux può sempre essere aggiornato tramite `pacman -Syu`.

## Installazione

### Layout di tastiera

Sono disponibili diverse mappature per molti paesi e tipi di tastiere, e un comando come `loadkeys it` basta per impostare la mappatura desiderata.

```
# loadkeys it

```

Ulteriori file per la mappatura dei tasti possono essere trovati in `/usr/share/kbd/keymaps/` (è possibile omettere il percorso keymap e l'estensione del file quando si utilizza loadkeys).

### Partizionare i dischi

Si legga la pagina sul [partizionamento](/index.php/Partitioning_(Italiano) "Partitioning (Italiano)") per maggiori dettagli.

Ricordarsi di creare tutti i dispositivi a blocchi accatastati per [LVM](/index.php/LVM_(Italiano) "LVM (Italiano)"), [disk encryption](/index.php/Disk_encryption "Disk encryption"), o [RAID](/index.php/RAID_(Italiano) "RAID (Italiano)"), prima di procedere.

### Formattare le partizioni

Si legga [file system](/index.php/File_systems_(Italiano)#Step_2:_creare_il_nuovo_file_system "File systems (Italiano)") e opzionalmente [Swap](/index.php/Swap_(Italiano) "Swap (Italiano)") per maggiori dettagli.

Se si sta utilizzando (U) EFI avrete probabilmente bisogno di un'altra partizione per ospitare la partizione di sistema UEFI. Si legga [questo articolo](/index.php/Unified_Extensible_Firmware_Interface_(Italiano)#Creare_una_partizione_di_sistema_UEFI_con_Linux "Unified Extensible Firmware Interface (Italiano)").

### Montare le partizioni

Ora si deve montare la partizione di root su `/mnt`. Dopodiche si dovrebbero anche creare le directory per montare le altre partizioni (`/mnt/boot`, `/mnt/home`, ..) e attivare la partizione di "swap *se si desidera che vengano rilevate da "genfstab".*

### Connessione alla rete

Un servizio di DHCP è già abilitato per tutti i dispositivi disponibili. Se è necessario impostare un indirizzo IP statico o utilizzare strumenti di gestione, come [Netctl](/index.php/Netctl "Netctl"), si dovrebbe fermare in primo luogo di questo primo servizio: `systemctl stop dhcpcd.service`. Per maggiori informazioni si veda la pagina [Configurazione della Rete](/index.php/Configurazione_della_Rete "Configurazione della Rete").

#### Wireless

Eseguire `wifi-menu` per impostare una connessione senza fili, per maggiori dettagli si leggano le pagine [Configurazione Wireless](/index.php/Wireless_Setup_(Italiano) "Wireless Setup (Italiano)") e [Netctl](/index.php/Netctl "Netctl").

### Installare il sistema base

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