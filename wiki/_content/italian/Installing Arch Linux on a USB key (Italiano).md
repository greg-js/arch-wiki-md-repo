Questa pagina spiega come effettuare una normale installazione di Arch su una chiave USB (o flash drive). Il risultato sarà un sistema che verrà aggiornato durante il normale utilizzo. Considerare anche l'alternativa di [Installare da supporto USB](/index.php/Installare_da_supporto_USB "Installare da supporto USB").

## Contents

*   [1 Procurarsi una chiave USB sufficientemente grande](#Procurarsi_una_chiave_USB_sufficientemente_grande)
*   [2 Ottenere il CD](#Ottenere_il_CD)
*   [3 Installazione](#Installazione)
*   [4 Configurazione](#Configurazione)
*   [5 Consigli](#Consigli)
    *   [5.1 Avviare senza problemi su macchine diverse senza usare gli UUID](#Avviare_senza_problemi_su_macchine_diverse_senza_usare_gli_UUID)
    *   [5.2 Ottimizzare il tempo di vita delle memorie flash](#Ottimizzare_il_tempo_di_vita_delle_memorie_flash)
*   [6 Da consultare](#Da_consultare)

## Procurarsi una chiave USB sufficientemente grande

Per l'installazione di KDE e di numerose applicazioni sono raccomandati almeno 3 GiB. GNOME e Xfce4, con un tipico insieme di pacchetti per il desktop (GIMP, Pidgin, OpenOffice, Firefox, flashplugin) possono essere installati su una chiave da 2 GiB, lasciando un piccola quantità di spazio per i dati utente.

## Ottenere il CD

Un cd di Arch Linux può essere usato per installare Arch sulla chiave USB, avviando il sistema da CD e lanciando `/arch/setup` per far partire l'AIF. Oppure, se si dispone di un altro computer con Linux (non è necessario che sia Arch), è possibile seguire le istruzioni di [Installazione da un sistema Linux esistente](/index.php/Install_from_existing_Linux_(Italiano) "Install from existing Linux (Italiano)"), e saltare direttamente alla parte di configurazione.

## Installazione

Eseguire l'installer (`/arch/setup`). Il processo di installazione può essere eseguito regolarmente con solo poche attenzioni:

*   E' consigliato partizionare manualmente il disco, dal momento che il partizionamento automatico potrebbe non funzionare, e creare partizioni non necessarie.
*   Se cfdisk dovesse fallire restituendo l'errore fatale "Partition ends in the final partial cylinder", l'unica soluzione è chiudere tutte le partizioni presenti sul supporto USB. Spostarsi in un altro terminale (come ad esempio `Alt + F2`), usare il comando `fdisk /dev/sdX` (dove `sdX` è ovviamente il supporto che si sta utilizzando), stampare la tabella delle partizioni (p), controllare che sia tutto a posto, cancellare (d) e scrivere i cambiamenti (w). Ora tornare a cfdisk.
*   E' altamente consigliato consultare [I consigli per minimizzare letture e scritture](/index.php/SSD#Tips_for_minimizing_disk_reads.2Fwrites "SSD") sugli [SSD)](/index.php/Solid_State_Drives_(Italiano) "Solid State Drives (Italiano)") prima di selezionare un filesystem. Per riassumere, ext4 senza un sistema di journal dovrebbe andare bene. Ricordare che quel tipo di flash ha un numero limitato di scritture e un sistema di journaling utilizzerà una parte di esse. Per la stessa ragione, è meglio anche non utilizzare una partizione di swap. Notare che questo non influenzerà l'installazione su un disco USB.
*   Editare il file `/etc/mkinitcpio.conf` ed aggiungere `usb` alla stringa degli hooks dopo `udev`. Questo serve a compilare adeguatamente il modulo necessario ad ogni aggiornamento del kernel.

## Configurazione

*   Assicurarsi che in `/etc/fstab` siano presenti le informazioni corrette sulla partizione per `/` e su tutte le altre partizioni sul supporto USB. Se tale supporto USB verrà usato su pc differenti tenere conto che la tabella delle partizioni potrà variare molto. Potrebbe quindi essere necessario usare UUID o label.

Per conoscere il UUID appropriato della partizione usare il comando **blkid**.

*   `/boot/grub/menu.lst`, il file di configurazione di Grub, dovrebbe essere modificato nella maniera seguente:

**Nota:** Dal momento che Grub è installato sulla chiave USB, sarà sempre hd0,0

Con lo statico `/dev/sdX`:

```
root (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/sda1 ro 
initrd /boot/initramfs-linux.img

```

Usando label, il file `menu.lst` dovrebbe assomigliare a:

```
root (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/disk/by-label/Arch ro
initrd /boot/initramfs-linux.img

```

Usando UUID invece dovrebbe essere qualcosa tipo:

```
root (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/disk/by-uuid/3a9f8929-627b- 4667-9db4-388c4eaaf9fa ro
initrd /boot/initramfs-linux.img

```

## Consigli

### Avviare senza problemi su macchine diverse senza usare gli UUID

Quando si utilizza la chiave USB su macchine diverse, può essere d'aiuto avere voci multiple in GRUB, per le macchine con differenti configurazioni. Ad esempio, la configurazione di GRUB potrebbe contenere:

```
# (0) Arch Linux
title  Arch Linux (primo drive)
root   (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/sda1 ro
initrd /boot/initramfs-linux.img

```

così come:

```
# (1) Arch Linux
title  Arch Linux (secondo drive)
root   (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/sdb1 ro
initrd /boot/initramfs-linux.img

```

E così via, avendo la possibilità di selezionare la configurazione per macchine diverse. Comunque, modificando l'opzione `root=` in GRUB non viene modificato `/etc/fstab` ed è necessario fare qualcosa (ad esempio utilizzare un link udev simbolico), in modo che la partizione di root venga sempre montata correttamente.

*   Eseguire `udevinfo -p /sys/block/sdx/ -a` (dove sdx indica il nome di periferica della propria chiave usb)
*   Trovare le informazioni uniche della propria chiave usb. Ad esempio `SYSFS{model}=="DataTraveler 2.0"`.
*   Creare un nuovo file:`/etc/udev/udev.rules/10-my-usb-key.rules` e inserire:

```
KERNEL=="sd**", SYSFS{product}=="DataTraveler 2.0", SYMLINK+="WHATEVERYOUWANTOTCALLIT%n"

```

(`KERNEL=="sd**"` è necessario poiché il kernel - in questo caso il 2.6.16 - nomina tutte le periferiche usb sd usando il sottosistema scsi e si vuole trovare e applicare le impostazioni a tutte le partizioni delle periferiche sd), con `SYSFS{model}==` come unico identificatore usato da udevinfo.

*   Eseguire `/etc/start-udev uevents` e assicurarsi che il link simbolico appaia in `/dev`.
*   Se così è, modificare `/etc/fstab`, sostituendo il vecchio sdx con il nuovo link simbolico.

### Ottimizzare il tempo di vita delle memorie flash

*   E' altamente consigliato consultare [Consigli per minimizzare letture e scritture](/index.php/SSD#Tips_for_minimizing_disk_reads.2Fwrites "SSD") sull'artico del wiki dedicato alle [SSD](/index.php/Solid_State_Drives_(Italiano) "Solid State Drives (Italiano)").

## Da consultare

*   [Guida ufficiale di installazione Arch](/index.php/Official_Arch_Linux_Install_Guide_(Italiano) "Official Arch Linux Install Guide (Italiano)")
*   [Installing Arch Linux from VirtualBox](/index.php/Installing_Arch_Linux_from_VirtualBox "Installing Arch Linux from VirtualBox")
*   [SSD](/index.php/Solid_State_Drives_(Italiano) "Solid State Drives (Italiano)")