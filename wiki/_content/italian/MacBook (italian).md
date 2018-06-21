Articoli correlati

*   [Installation guide](/index.php/Installation_guide "Installation guide")
*   [Post Installation Tips](/index.php/Post_Installation_Tips "Post Installation Tips")

La procedura per installare Arch Linux su un Macbook (12"/Air/Pro) o su un iMac, è molto simile a quella valida per qualsiasi altro computer. Nonostante ciò, a causa di alcuni componenti hardware specifici del Mac, ci sono alcune speciali considerazioni che meritano una guida separata. Per ulteriori informazioni di base, consultare la [guida all'installazione](/index.php/Installation_guide_(Italiano) "Installation guide (Italiano)") e [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Italiano) "Unified Extensible Firmware Interface (Italiano)"). Questa guida contiene istruzioni di installazione utilizzabili su qualsiasi computer Apple, il cui hardware è supportato dal kernel Linux.

## Contents

*   [1 Panoramica](#Panoramica)
*   [2 Aggiornamento Firmware](#Aggiornamento_Firmware)
*   [3 Partizionamento](#Partizionamento)
    *   [3.1 Solo Arch Linux](#Solo_Arch_Linux)
    *   [3.2 Arch Linux con OS X o altro sistema operativo](#Arch_Linux_con_OS_X_o_altro_sistema_operativo)
        *   [3.2.1 Opzione 1: EFI](#Opzione_1:_EFI)
        *   [3.2.2 BIOS-compatibility](#BIOS-compatibility)
    *   [3.3 Mac OS X con Arch Linux](#Mac_OS_X_con_Arch_Linux)
        *   [3.3.1 EFI](#EFI)
        *   [3.3.2 BIOS-compatibility](#BIOS-compatibility_2)
*   [4 Installazione](#Installazione)
*   [5 Configurazione post-installazione](#Configurazione_post-installazione)
    *   [5.1 Xorg](#Xorg)
        *   [5.1.1 Video](#Video)
        *   [5.1.2 Touchpad](#Touchpad)
        *   [5.1.3 Keyboard](#Keyboard)
    *   [5.2 Wifi](#Wifi)
    *   [5.3 Audio](#Audio)
    *   [5.4 Bluetooth](#Bluetooth)
    *   [5.5 iSight](#iSight)
    *   [5.6 Sensori della Temperatura](#Sensori_della_Temperatura)
    *   [5.7 Profilo Colore](#Profilo_Colore)
    *   [5.8 Apple Remote](#Apple_Remote)
    *   [5.9 Condivisione Partizioni Hfs](#Condivisione_Partizioni_Hfs)
    *   [5.10 Condivisione della Home](#Condivisione_della_Home)
        *   [5.10.1 In OS X](#In_OS_X)
            *   [5.10.1.1 Passaggio 1: Cambiare UID e GID(s)](#Passaggio_1:_Cambiare_UID_e_GID.28s.29)
            *   [5.10.1.2 Passaggio 2: Cambiare i permessi di 'HOME'](#Passaggio_2:_Cambiare_i_permessi_di_.27HOME.27)
        *   [5.10.2 In Arch](#In_Arch)
*   [6 rEFIt](#rEFIt)

## Panoramica

Nel dettaglio, la procedura per installare Arch Linux su un MacBook si divide in:

1.  **[Aggiornamento Firmware](#Aggiornamento_Firmware)**: È sempre utile iniziare da un'installazione pulita e aggiornata di OS X.
2.  **[Partizionamento](#Partizionamento)**: Ridimensionamento o eliminazione della partizione OS X per creare le partizioni per Arch Linux.
3.  **[Installare Arch Linux](#Installazione)**: L'installazione effettiva di Arch Linux
4.  **[Configurazione Post-installazione](#Configurazione_post-installazione)**: Configura l'hardware del MacBook.

## Aggiornamento Firmware

Prima di procedere con l'installazione di Arch Linux, è importante assicurarsi che siano installati gli aggiornamenti firmware più recenti sul proprio Mac. Questa procedura richiede OS X. In OS X, aprire l'App Store e verificare l'eventuale presenza di aggiornamenti. Se Mac trova e installa degli aggiornamenti, assicurarsi di **riavviare** il computer, quindi controllare nuovamente gli aggiornamenti per assicurarsi di aver installato tutto.

**Nota:** Se si è disinstallato OS X o lo si vuole installare nuovamente, [Apple](https://support.apple.com/it-it/HT204904) ha delle ottime istruzioni.

Si consiglia di mantenere OS X installato, poiché gli aggiornamenti del firmware MacBook possono essere installati solo tramite OS X. Tuttavia, se si intende rimuovere completamente OS X, eseguire i backup di questi file, necessari in Linux per regolare il [color profile](#Color_Profile):

```
/Library/ColorSync/Profiles/Displays/*

```

Continuare a [#Partizionamento](#Partizionamento)

## Partizionamento

Il partizionamento del disco di un Mac non è diverso da altri PC o laptop. Tuttavia, se si vuole mantenere OS X per il dual boot, si deve considerare che il disco di un Mac, per impostazione predefinita,è formattato usando GPT e contiene almeno 3 partizioni:

*   **EFI**: ~200 MB [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition").
*   **OS X**: la partizione principale contenente l'installazione di OS X. È formattata in [HFS+](/index.php/File_systems_(Italiano) "File systems (Italiano)").
*   **Recovery**: una partizione di ripristino presente in quasi tutti i Mac con OS X 10.7 o successivi. Di solito è nascosta, ma può essere visualizzata con strumenti di partizionamento.

**Nota:** Nei Mac che montano [Apple Fusion Drive](/index.php/Apple_Fusion_Drive "Apple Fusion Drive"), lo schema di partizione potrebbe essere differente.

Come partizionare il disco dipende da quanti sistemi operativi si desidera installare. Verranno illustrate le seguenti opzioni:

*   Single boot: [#Solo Arch Linux](#Solo_Arch_Linux)
*   Doppio boot: [#Arch Linux con OS X o altro sistema operativo](#Arch_Linux_con_OS_X_o_altro_sistema_operativo) *(raccomandato, così sarà possibile ritornare a OS X quando necessario)*
*   triplo boot: [#OS X, Windows XP, e Arch Linux triplo boot](#OS_X.2C_Windows_XP.2C_e_Arch_Linux_triplo_boot)

### Solo Arch Linux

Questa situazione è la più facile da affrontare. Il partizionamento è uguale a qualsiasi altro hardware su cui può essere installato Arch Linux. Fare riferimento alla standard [guida all'installazione](/index.php/Installation_guide_(Italiano) "Installation guide (Italiano)") per i dettagli.

**Nota:** È consigliato **disabilitare** il suono di avvio del Mac prima di procedere con il partizionamento. Basta avviare in OS X, disattivare l'audio del sistema e riavviare nuovamente il programma di installazione di Arch Linux. Si prega di tenere presente che il volume del suono di avvio può essere modificato in modo affidabile solo in OS X.

Se si desidera configurare il proprio sistema per avere la crittografia completa del disco, consultare la pagina [Dm-crypt / Encrypting an whole system](/index.php?title=Dm-crypt_/_Encrypting_an_whole_system&action=edit&redlink=1 "Dm-crypt / Encrypting an whole system (page does not exist)") per i dettagli.

Un esempio di partizionamento base, che non considera una partizione `/home` separata ne crittografia o LVM, è il seguente:

```
partition  mountpoint  size    type  label
/dev/sda1  /boot       200MiB  vfat  EFI
/dev/sda2  /swap       adjust  swap  swap
/dev/sda3  /           remain  ext4  root

```

*   Una volta fatto, si può proseguire all' [#Installazione](#Installazione)

### Arch Linux con OS X o altro sistema operativo

È necessario partizionare il disco rigido mantenendo le partizioni utilizzate per OS X / Windows. Se si desidera mantenere OS X, il modo più semplice è utilizzare gli strumenti di partizionamento in OS X e quindi terminare con gli strumenti di Arch Linux.

**Attenzione:** Se la partizione di OS X è criptata con FileVault 2, **bisogna** disabilitare il tutto prima di procedere. Dopo che la partizione di OS X è stata ridimensionata, FileVault 2 potrà essere riabilitato.

**Procedimento**:

*   In OS X, eseguire *Utility Disco.app* (situata in `/Applicazioni/Utilità`)
*   Selezionare il disco da partizionare nella colonna di sinistra (non la partizione!). Premere sul pulsante **Partiziona**.
*   Aggiungere una nuova partizione premendo il pulsante **+** e scegliere quanto spazio lasciare per OS X, e quanto per la nuova partizione. Si tenga presente che la nuova partizione sarà formattata in Arch Linux, per cui si può scegliere il tipo di partizione che si vuole.
*   Se tutto è stato fatto fino a qui con successo, si può procedere. Altrimenti, si dovrà prima riparare la partizione da OS X.
*   Avviare l'immagine di installazione di Arch mediante cd o [LiveUSB](/index.php/USB_flash_installation_media_(Italiano) "USB flash installation media (Italiano)") tenendo premuto `Alt` **durante l'avvio**. Procedere con l'[#Installazione](#Installazione).

È possibile ridimensionare la partizione appena creata tramite il programma di installazione di Arch, o cancellarla per procedere con la creazione di altre partizione (es. swap).

**Tip:** Invece di ingombrare l'unità con una partizione diversa, è possibile utilizzare uno [swapfile](/index.php/Swapfile "Swapfile") invece di una partizione dedicata. Un'altra soluzione può essere configurare [LVM](/index.php/LVM "LVM") per utilizzare la partizione appena creata come contenitore. Si prega di fare riferimento agli articoli collegati.

#### Opzione 1: EFI

*   Eseguire *cgdisk*

*   Cancellare la partizione creata in precedenza con *Utility Disco* e creare le partizioni necessarie per Arch Linux. OS X usa un gap di 128 MiB dopo le partizioni, per cui quando si creerà la prima partizione dopo l'ultima partizione di OS X, digitare **+128M** quando cgdisk chiederà il primo settore per la partizione. Maggiori informazioni sulla policy di partizione di Apple si possono trovare [qui](https://developer.apple.com/library/mac/technotes/tn2166/_index.html#//apple_ref/doc/uid/DTS10003927-CH1-SUBSECTION5). Un semplice esempio (senza LVM, senza criptazione):

#### BIOS-compatibility

*   Lanciare il boot e passare ad una tty libera.
*   Eseguire **parted**. Il metodo più semplice consiste nello scegliere una partizione di tipo **msdos** e partizionare normalmente. GRUB è compatibile con GPT.
*   Creare le partizioni necessarie.
*   Fatto! Ora è possibile continuare con l' [#Installazione](#Installazione)

### Mac OS X con Arch Linux

Il modo più semplice di partizionare il tuo hard drive, per fare in modo che Arch Linux e Mac convivano, è quello di preparare le partizioni con il tool di Mac OS X e poi terminare con i tools di Arch Linux

**Attenzione:** E' molto consigliato effettuare questa operazione dopo un'installazione pulita di Mac OS X . Eseguire questo procedimento su un sistema pre esistente può avere effetti indesiderati..

**Procedimento**:

*   In Mac OS X, avviare **Disk Utility** (in /Applications/Utilities)

*   Selezionare il Disco che si vuole partizionare nella colonna a sinistra (il disco, non le partizioni!). Cliccare sul pulsante "partiziona" sulla destra.

*   Selezionare il volume da ridimensionare nello **schema volumi**.

*   Decidere quanto spazio dedicare a MAC OS X, e quanto ad Arch Linux. Ricordarsi che un'installazione standard di Mac OS X necessita circa di 15-20 Gib, in base al numero di files e di software installati.

*   Infine, inserire la nuova dimensione della partizione di MAC OS X e cliccare su **applica**. Così verrà creata una nuova partizione nello spazio libero del disco. La partizione verrà poi cancellata più avanti.

**Note:** Se si volesse creare una partizione condivisa tra Mac OS X e Arch Linux, eseguire ora i passi aggiuntivi descritti in [Partizioni Condivise](#Partizioni_Condivise).

*   Se si sono eseguiti con successo i passi descritti fino ad ora, è possibile continuare. Altrimenti, si dovrà riparare le partizioni da Mac OS X.

*   Eseguire il Boot dal CD di Arch tenendo premuto il tasto Alt. Seguire una delle procedure in base alla tipo di boot che si è scelto.

#### EFI

*   Eseguire **cgdisk**

*   Cancellare la partizione precedentemente fatta con Utilità disco e creare le partizioni necessarie per Arch. OS X lascia un gap di 128MB dopo l'ultima sua partizione, per cui quando si creerà la prima partizione dopo quella di OS X, digitare **+128M** quando cgdisk chiederà il primo settore della nuova partizione. Un semplice esempio (no LVM, crypto):

**Note:**

*   La partizione di swap è opzionale, su macchine con ram superiori a 4GB. Buone performance si possono ottenere anche senza questa partizione. Si può tuttavia crearla in seguito [Swap#Swap file](/index.php/Swap#Swap_file "Swap").
*   L'opzione di dual boot più semplice consiste nell'installare refind da OS X, nella sua directory di root (solitamente install.sh). In seguito, copiare la cartella contenente i driver dal tarball di installazione verso il luogo in cui si installa refind, e decommentare le linee "scan_all_linux_kernels" e "also_scan_dirs" in refind.conf. La configurazione delle opzioni di boot possono essere fatte tramite refind_linux.conf situato nella /boot directory di Arch.
*   Se si vuole eseguire GRUB dal bootloader di Apple, bisogna creare una piccola partizione hfs+ (per convenienza, usare OS X per formattarla tramite Utilità Disco.app). Seguire la procedura d'installazione di GRUB EFI, e montare la `/boot/efi` directory nella partizione hfs+ appena creata. Infine uscire e ritornare in OS X. Questo imposterà GRUB come bootloader predefinito (tenendo premuto ALT si tornerà alla solita schermata di boot del Mac. Vedere [http://mjg59.dreamwidth.org/7468.html](http://mjg59.dreamwidth.org/7468.html))
*   Per ulteriori informazioni sul partizionamento, vedere [Partitioning](/index.php/Partitioning "Partitioning").
*   La partizione EFI di OS X può essere condivisa con Arch, rendendo la creazione di un'ulteriore partizione EFI dedicata ad Arch opzionale

```
partition  mountpoint  size       type  label
/dev/sda1  /boot/efi   200MiB     vfat  EFI
/dev/sda2  -           ?          hfs+  Mac OS X
/dev/sda3  -           ?          hfs+  Recovery
/dev/sda4  -           100MiB     hfs+  Boot Arch Linux from the Apple boot loader (optional)
/dev/sda5  /boot       100MiB     boot  boot
/dev/sda6  -           ?          swap  swap (optional)
/dev/sda7  /           10GiB      ext4  root
/dev/sda8  /home       remaining  ext4  home

```

*   Fatto, si può continuare con l' [#Installazione](#Installazione)

#### BIOS-compatibility

*   Eseguire **parted** come root.

*   Cancellare lo spazio libero e partizionarlo come faremmo per qualunque altra installazione. Tenere presente che MBR può gestire solamente 4 partizioni primarie (inclusa la partizione EFI). Questo ci lascia solo 2 partizioni per Arch. Una strategia consiste nell'avere una partizione system e una partizione home, e usare un file di swap. Un'altra tecnica consiste nel creare una partizione rendendola condivisa (vedere qui di seguito).

*   In seguito creare un filesystem sulle partizioni che lo necessitano, in special modo quella che conterrà /boot. Se non si è sicuri su come farlo usando `mkfs.ext2` (or whatever), eseguire `/arch/setup` e procedere fino a Prepare Hard Drive ed utilizzare l'opzione "Manually configure block devices...", dopodiché uscire dall'installer. Ciò è necessario poiché rEFIt imposterà il giusto tipo di partizione in MBR nel prossimo passaggio (senza un filesystem altrimenti, ignorerebbe la partizione impostata con parted), senza il quale GRUB rifiuterebbe l'installazione nella partizione corretta.

*   A questo punto si dovrebbe riavviare il computer per permettere a rEFIt di sistemare le tabelle di partizione sul disco. (Se non lo si fa, si dovrà reinstallare GRUB successivamente al fine di permettere al Mac di riconoscere la partizione Linux.) Quando si è dentro il menu rEFIt, selezionare **update partition table**, e premere Y. Riavviare.

*   Procedere all' [#Installazione](#Installazione)

## Installazione

*   Esegui il boot dal CD di Arch Linux. inserisci **arch vga=773** per avere una console ad alta risoluzione.

```
boot: arch vga=773

```

**Note:** alcuni utenti hanno riportato strani comportamenti della testiera, come lunghi ritardi e sdoppiamenti dei caratteri. Se hai questo problema, esegui il boot con queste opzioni.

```
boot: arch noapic irqpoll acpi=force

```

*   Esegui il login come **root**

*   Avvia l'installer:

```
/arch/setup

```

*   Procedi per l'installazione come descritto nell' [Installation guide](/index.php/Installation_guide "Installation guide"), eccetto questi passaggi:
    *   Nel passaggio per la [preparazione degli hard drives](/index.php/Installation_guide#Prepare_Hard_Drive "Installation guide") esegui solo "[set filesystem mountpoints](/index.php/Installation_guide#Set_Filesystem_Mountpoints "Installation guide")" stando attento ad assegnare le giuste partizioni.
    *   Durante l'[installazione del boot loader](/index.php/Installation_guide#Install_a_boot_loader "Installation guide") modifica il file menu.lst e aggiungi **reboot=pci** alla fine delle linee **kernel** lines, per esempio: `kernel /vmlinuz26 root=/dev/sda5 ro reboot=pci` Questo ti consentirà di riavviare correttamente da Arch.
    *   Durante l'[installazione del boot loader](/index.php/Installation_guide#Install_a_boot_loader "Installation guide") installa GRUB nella partizione con <tt>/boot</tt>.
        **Attenzione:** Non installare GRUB in */dev/sda* !!! Facendolo rischi di avere un ambiente post-configurazione instabile!!.

    *   Nella [configurazione del sistema](/index.php/Installation_guide#Configure_the_system "Installation guide"), modifica /etc/mkinitcpio.conf e aggiungi l'hook **usbinput** nella riga degli**HOOKS** line in qualsiasi posizione dopo l'hook **autodetect**. Questo caricherà i drivers della tastiera nel caso che ti serva prima del boot di Arch Linux.

*   Quando hai completato l'installazione, riavvia il sistema.

```
# reboot

```

## Configurazione post-installazione

**Tip:** i MacBooks richiedono del software aggiuntivo da [AUR](/index.php/AUR "AUR"). Per installare rapidamente il software da AUR, puoi utilizzare [Yaourt](/index.php/Yaourt "Yaourt").

**Tip:** Questo software e la sua configurazione devono essere eseguiti da root. Per velocizzare questa operazione, ti consiglio di installare [Sudo](/index.php/Sudo "Sudo").

**Tip:** segui una sezione alla volta.

### Xorg

Installa e configura Xorg seguendo l'articolo [Xorg](/index.php/Xorg "Xorg").

#### Video

MacBooks diversi hanno la scheda grafica diversa.

Per sapere quale scheda grafica monta il tuo MacBook, digita in un terminale

```
# lspci | grep VGA

```

Se risponde **intel** hai bisogno del driver **xf86-video-intel**. Lo puoi installare digitando da terminale:

```
# pacman -S xf86-video-intel

```

Se risponde **nvidia**

```
# pacman -S nvidia

```

Invece, se risponde **ATI**

```
# yaourt catalyst

```

Gli utenti con scheda grafica**intel** non hanno bisogno di nesun'altra confugurazione; invece gli altri utenti hanno bisogno di un file **xorg** di base dove specificare i ldriver corretto da usare. Per configurarlo, vedi [ATI](/index.php/ATI "ATI") o [NVIDIA](/index.php/NVIDIA "NVIDIA").

#### Touchpad

Dalla versione 2.6.30 del kernel, il touchpad funziona in multitouch, permettendo click destro a due dita, tap centrale a tre dita e scrolling a due dita

#### Keyboard

La tastiera funziona da subito. solo i tasti funzione non vengono riconosciuti.

Per configurare i tasti funzione, installate pommed:

```
# yaourt pommed

```

to install it, after

```
modifica the **/etc/pommed.conf** in base all'hardware del tuo MacBook, compilandolo

```

dai files di esempio **/etc/pommed.conf.mac** o **/etc/pommed.conf.ppc**.

poi

```
Inserisci **pommed** alla fine della lista **DAEMONS** in **/etc/rc.conf**

```

alla fine riavvia il sistema.

**Tip:** se i tasti funzione per la luminosità non funzionano, installa i drivers nvidia-bl da aur.

```
$ yaourt -S nvidia-bl

```

**Tip:** se usi GNOME o KDE, puoi settare *funzionalità di 3° livello*, *multimedia key*, etc. in **Preferenze Tastiera**.

**Note:** vedi [Xorg input hotplugging](/index.php/Xorg_input_hotplugging "Xorg input hotplugging") per altre informazioni sulla configurazione.

### Wifi

Diversi modelli hanno diverse schede wi-fi.

Puoi scoprire che scheda wireless hai tramite

```
# lspci | grep Network

```

*   se hai una Atheros tutto funziona dall'inizio.

*   Invece, se hai una Broadcom, vedi la pagina [Broadcom BCM4312](/index.php/Broadcom_BCM4312 "Broadcom BCM4312").

### Audio

Prima di tutto segui la wiki di [ALSA](/index.php/ALSA "ALSA"), poi, se qualcosa non funziona correttamente, continua a leggere qui.

Modifica **/etc/modprobe.d/50-sound.conf**, aggiungendo:

```
options snd_hda_intel model=intel-mac-auto

```

Questo dovrebbe specificare automaticamente il codec del tuo MacBook.

Se la tua scheda audio non è stata ancora riconosciuta, esegui questi comandi da terminale:

```
$ wget [ftp://ftp.kernel.org/pub/linux/kernel/people/tiwai/snapshot/alsa-driver-snapshot.tar.gz](ftp://ftp.kernel.org/pub/linux/kernel/people/tiwai/snapshot/alsa-driver-snapshot.tar.gz)
$ tar xf alsa-driver-snapshot.tar.gz
$ cd alsa-driver 
# ./configure --enable-dynamic-minors --without-oss –with-cards="hda-intel"
# make
# make install

```

In questo modo sono stati installati i drivers per ALSA

**Note:** Puoi provare a specificare altre opzioni, in accordo con il tuo hardware. Tutte le possibili configurazioni sono elencate nella pagina 'Kernel Documentation', disponibile online:

*   [ALSA-Configuration.txt](http://www.kernel.org/doc/Documentation/sound/alsa/ALSA-Configuration.txt)
*   [HD-Audio.txt](http://www.kernel.org/doc/Documentation/sound/alsa/HD-Audio.txt)
*   [HD-Audio-Models.txt](http://www.kernel.org/doc/Documentation/sound/alsa/HD-Audio-Models.txt).

Alla fine riavvia.

### Bluetooth

Vedi l'articolo [Bluetooth](/index.php/Bluetooth "Bluetooth") per installare e configurare tutto il software necessario.

Poi, se il bluetooth non funziona, puoi modificare **/etc/conf.d/bluetooth** ed abilitare **hid2hci** decommentando la riga seguente:

```
HID2HCI_ENABLE="true"

```

Poi riavvia il demone del bluetooth (o il computer, direttamente)

**Tip:** Per maggiori informazioni, vedi la pagina [Bluetooth](/index.php/Bluetooth "Bluetooth").

### iSight

iSight funziona senza modifiche sin da subito.

Se non funziona, prova ad eseguire un aggiornamento del sistema:

```
# pacman -Syu 

```

### Sensori della Temperatura

Per fare riconoscere i sensori ad Arch Linux, basta installare e configurare **lm_sensors**. vedi [lm_sensors](/index.php/Lm_sensors "Lm sensors").

### Profilo Colore

Si può usare il profilo colore di Mac OS X.

Prima installa **xcalib** da AUR:

```
# yaourt xcalib

```

Poi copia il profilo colore di Mac OS X da **/Library/ColorSync/Profiles/Displays/** nella partizione Mac OS X in **~/colorprofiles/** per esempio.

Ci sono profili del colore diversi in base al modello del MacBook. Seleziona quello giusto:

*   **Color LCD-4271800.icc** for MacBook Pro with CoreDuo CPU
*   **Color LCD-4271880.icc** for MacBook with Core2Duo
*   **Color LCD-4271780.icc** for MacBook (not Pro) based on CoreDuo or Core2Duo.

**Tip:** Mac OS consente di salvare il profilo del colore corrente dalla sezione **Displays -> Color** del **Mac OS System Preferences**, in questo caso il file è salvato in **/Users/<username>/Library/ColorSync/Profiles**.

Ora puoi attivarlo eseguendo;

```
# xcalib ~/colorprofile.icc

```

**Attenzione:** il comando precedente imposta il nuovo profilo del colore solo per la sessione attuale; Per attivarlo in automatico devi inserire il comando nelle **applicazioni d'avvio**

**Note:** vedi **xcalib** man pages per più informazioni.

### Apple Remote

Prima di tutto, installa a configura il software **lirc** , per informazioni vedi [LIRC](/index.php/LIRC "LIRC").

Ora configura LIRC per utilizzare **/dev/usb/hiddev0** (o **/dev/hiddev0**), modificando **/etc/conf.d/lircd**.

Utilizza **irrecord** (disponibile quando installi LIRC) per creare un file di configurazione compatibile con il segnale del tuo Apple Remote.

Avvia **lircd** ed esegui **irw** per assicurarti che funzioni

esempio di un **/etc/lircd.conf**:

```
begin remote

  name  lircd.conf.macbook
  bits            8
  eps            30
  aeps          100

  one             0     0
  zero            0     0
  pre_data_bits   24
  pre_data       0x87EEFD
  gap          211994
  toggle_bit_mask 0x87EEFD01

      begin codes
          Repeat                   0x01
          Menu                     0x03
          Play                     0x05
          Prev                     0x09
          Next                     0x06
          Up                       0x0A
          Down                     0x0C
      end codes

end remote

```

((esegui **appleir** se non è simile a questo.))

### Condivisione Partizioni Hfs

Prima di tutto, devi conoscere le tue partizioni. Esegui

```
fdisk -l /dev/sda

```

output di esempio:

```
# fdisk -l /dev/sda
    Device  Boot     Start         End      Blocks   Id  Type
 /dev/sda1               1          26      204819   ee  GPT
 /dev/sda2              26       13602   109051903+  af  Unknown
 /dev/sda3   *       13602       14478     7031250   83  Linux
 /dev/sda4           14478       14594      932832+  82  Linux swap / Solaris

```

In questo caso, la partizione "Unknown" è la partizione di Mac OS X, la quale si trova in `/dev/sda2`.

Crea una cartella "mac" in /media:

```
sudo mkdir /media/mac

```

Aggiungi alla fine di */etc/fstab* questa riga:

```
/dev/sda2    /media/mac     hfsplus rw,exec,auto,users   0 0

```

Monta "mac":

```
mount /media/mac

```

ed esegui un check:

```
ls /media/mac

```

### Condivisione della Home

***Sincronizzazione UID***

#### In OS X

**Note:** E' consigliato modificare UID/GID subito dopo avere creato un nuovo account, sia in OS X che in Arch Linux.

##### Passaggio 1: Cambiare UID e GID(s)

***Pre-Leopard***

1.  Apri **NetInfo Manager** , nella cartella */Applications/Utilities* .

1.  Se non l'hai ancora fatto, abilità l'accesso alle operazioni agli utenti clickando sul lucchetto in fondo alla finestra, e inserisci la password del tuo accounr o la password di root se hai creato un account root.

1.  Vai in */users/<new user name>* dove <new user name> è il nome dell'account che avrà permessi di lettura/scrittura nella partizione che sarà condivisacon l'utente di Arch.

1.  Cambia il valore di **UID** in 1000 (Il valore usato di default per il primo utente creato in Arch).

1.  Altrimenti cambia il valore di**GID** in 1000 (il valore usato di default per la creazione di nuovi utenti in Arch).

1.  Vai in */groups/<new user name>*, salvando le modifiche fatte finora.

**Note:** Se un errore ti avvisa che le operazioni non sono permesse, esegui un log out e poi riesegui un login.

***Leopard***

In Leopard, l'applicazione **NetInfo Manager** non è presente. Per la sincronizzazione degli UID, bisogna procedere in un altro modo:

1.  Apri **System Preferences**.

1.  Clicka su **Accounts**.

1.  Sblocca il pannello se non lo hai gia fatto.

1.  click destro sull'utente desiderato, e seleziona **Advanced Options**.

1.  Prendi nota del campo **User ID**, ne avrai bisogno. Cambia UID e GID per farli coincidere con l'account che si vuole condividere in Arch. (1000 di default per il orimo utente creato in Arch Linux).

##### Passaggio 2: Cambiare i permessi di 'HOME'

1.  Apri un **Terminale** ed entra nella cartella */Applications/Utilities*.

1.  Inserisci i seguenti comandi per modificare le impostazioni dei permessi della tua home, sostituendo <your username> con il tuo username, <your user group> con il gruppo a cui appartiene il tuo account e <your old UID> con il vecchio valore di UID.

```
find /User/<your user name> -user <your old UID> -exec chown <your user name>:<your user group>

```

#### In Arch

Per sincronizzare il tuo UID in Arch Linux, è consigliato eseguuire questa operazione *mentre crei un nuovo acount*. E' inoltre consigliato farlo subito dopo avere installato Arch Linux.

Adesso devi sostituire la home di Arch con la home di Mac, modificando il file */etc/fstab*.

## rEFIt

Ora installa rEFIt, se non lo hai gia fatto.

**Note:** rEFIt non è indispensabile. Ti consente solo (tramite un gradevole menu) di scegliere se eseguire il boot da MacOS X o da Arch Linux ad ogni avvio.

In OS X, scarica il file ".dmg" da -> [Refit Homepage](http://refit.sourceforge.net/) ed installalo.

**Note:** Se hai gia partizionato il tuo hard disk per prepararlo per l'installazione di Arch, rEFIt non sarà attivato di default. In tal caso, devi avviare lo script "enable.sh" installato in /efi/refit/.

Adesso apri un **terminale** ed inserisci:

```
cd /efi/refit; ./enable.sh

```