Articoli correlati

*   [Installation guide](/index.php/Installation_guide "Installation guide")
*   [Post Installation Tips](/index.php/Post_Installation_Tips "Post Installation Tips")

La procedura per installare Arch Linux su un Macbook è molto simile a quella valida per qualsiasi altro computer. Nonostante ciò, a causa di alcuni componenti hardware specifici del MacBook, bisogna prendere dei particolari accorgimenti. Per informazioni generali sull'installazione, vedi [Installation guide](/index.php/Installation_guide "Installation guide"). Queste istruzioni sono da considerarsi valide per qualsiasi computer Apple il cui harware sia supportato dal kernel Linux. Si consiglia di leggere i relativi articoli (in alto a destra nella pagina), per la risoluzione dei problemi di specifiche versioni di MacBook.

## Contents

*   [1 Panoramica](#Panoramica)
*   [2 Installazione di Mac OS X e aggiornamento firmware](#Installazione_di_Mac_OS_X_e_aggiornamento_firmware)
*   [3 Partizionamento](#Partizionamento)
    *   [3.1 Solo Arch Linux](#Solo_Arch_Linux)
        *   [3.1.1 EFI](#EFI)
        *   [3.1.2 BIOS-compatibility](#BIOS-compatibility)
    *   [3.2 Mac OS X con Arch Linux](#Mac_OS_X_con_Arch_Linux)
        *   [3.2.1 EFI](#EFI_2)
        *   [3.2.2 BIOS-compatibility](#BIOS-compatibility_2)
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

Nel dettaglio, la procedura per installare Arch Linux su un MacBook è:

1.  **[Installazione di Mac OS X](#Installazione_di_Mac_OS_X_e_aggiornamento_firmware)**: Indipendentemente dalla configurazione desiderata, serve per installare Arch Linux a partire da un'installazione "pulita" di Mac OS X.
2.  **[Aggiornamento firmware](#Installazione_di_Mac_OS_X_e_aggiornamento_firmware)**: Riduce la probabilità di errori ed apporta nuove funzioni all'hardware.
3.  **[Partizionamento](#Partizionamento)**: Ridimensiona o elimina la partizione di OS X e crea la partizione per Arch Linux.
4.  **[Installare Arch Linux](#Installazione)**: L'installazione effettiva di Arch Linux
5.  **[Configurazione Post-installazione](#Configurazione_post-installazione)**: Configura l'hardware del MacBook.

**Tip:** rEFIt è un famoso bootloader per computers con firmware EFI (Mac inclusi). Può essere installato in qualsiasi momento durante l'installazione. Per informazioni, vedere [rEFIt](/index.php/MacBook#rEFIt "MacBook").

## Installazione di Mac OS X e aggiornamento firmware

[Apple](http://www.apple.com/it/) fornisce delle ottime istruzioni riguardo all'installazione di Mac OS X. Seguire le loro istruzioni, e una volta che Mac OS X è installato fare click su:

```
Apple Menu --> Software Update

```

Ed aggiornare tutto il software. Una volta finito, riavviare il computer. Ripetere questo procedimento per essere sicuri di avere installato tutti gli aggiornamenti.

Se non si ha intenzione di avere OS X installato, assicurarsi di fare un backup di questi files:

```
/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/AppleUSBVideoSupport.kext/Contents/MacOS/AppleUSBVideoSupport

```

Si necessiterà di questo file più avanti per le funzionalità di iSight.

```
/Library/ColorSync/Profiles/Displays/<FILES HERE>

```

Si avrà bisogno di questi files per la regolazione del [color profile](#Color_Profile).

## Partizionamento

Il passaggio successivo della procedura d'installazione è il ri-partizionamento del disco. Se MAC OS X è stato installato nella sua forma tipica, il disco dovrebbe avere una formattazione GPT e le seguenti partizioni:

*   **EFI**: una partizione di 200 MB all'inizio del disco. Spesso viene riconosciuta come partizione "DOS" o "FAT" da alcuni tool di partizionamento, e solitamente ha label *#1*
*   **Mac OS X**: la partizione *(HFS+)*, che occuperà tutto lo spazio rimasto. Solitamente ha label *#2*.
*   **Recovery**: una partizione per la manutenzione (solo per OS X 10.7 o superiori).

Le modalità per il partizionamento vanno scelte in base al numero di sistemi operativi che si vogliono installare. In questo wiki verranno illustrate:

*   [Solo Arch Linux](#Solo_Arch_Linux) in boot singolo.
*   [Mac OS X e Arch Linux](#Mac_OS_X_con_Arch_Linux) in dual boot.

Se non si è sicuri sulla modalità da scegliere, consigliamo un dualboot, per poter ritornare a OS X in seguito.

### Solo Arch Linux

Questa è la soluzione più semplice da realizzare. Il partizionamento si esegue come su qualsiasi altro computer su cui Arch Linux può essere installato. L'unico accorgimento particolare va preso per il suono del boot . Per assicurarsi che questo suono non sia presente, premere **mute** in OS X prima di procedere. Il firmware memorizzerà questa impostazione, se possibile. Bisogna tener presente che se si elimina la partizione OS X non vi è un modo semplice di aggiornare il firmware, a meno che non si esegua OS X da un drive esterno. Lo si può eseguire con EFI (raccomandato) o in modalità BIOS compatibile, nel dubbio scegliere EFI.

Per installare usando EFI, seguire le istruzioni [instruction to make a EFI bootable media](/index.php/Unified_Extensible_Firmware_Interface#Create_UEFI_bootable_USB_from_ISO "Unified Extensible Firmware Interface"). Una volta fatto verificare che il dispositivo USB parta in modalità EFI [checking the EFI kernel variables](/index.php/Unified_Extensible_Firmware_Interface#UEFI_Variables_Support "Unified Extensible Firmware Interface"). Si dovrà formattare la partizione EFI con `hfsplus` filesystem ([hfsprogs](https://aur.archlinux.org/packages/hfsprogs/)) anzichè vfat altrimenti [mactel-boot](https://aur.archlinux.org/packages/mactel-boot/) non funzionerà, e su un MacBook non si può usare efibootmgr..

#### EFI

*   Richiede [GRUB](/index.php/GRUB "GRUB") per funzionare
*   Scegliere installazione media e passare ad una tty libera.
*   Eseguire **cgdisk** ([gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) package).
*   Creare le partizioni necessarie

**Note:**

*   La partizione di Swap è opzionale su macchine con RAM superiore a 4GB, dato che non influirebbe sulle prestazioni della macchina. Si può comunque creare in un secondo momento [Swap file](/index.php/Swap#Swap_file "Swap").
*   Per ulteriori informazioni sul partizionamento [Partitioning](/index.php/Partitioning "Partitioning")

.

Un semplice esempio (senza LVM criptato):

```
partition  mountpoint  size    type  label
/dev/sda1  /boot/efi   200MiB  vfat  EFI
/dev/sda2  /boot       100MiB  ext2  boot
/dev/sda3  -           adjust  swap  swap
/dev/sda4  /           10GiB   ext4  root
/dev/sda5  /home       remain. ext4  home

```

*   Fatto, si può ora procedere all' [#Installazione](#Installazione)

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