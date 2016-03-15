Questo documento mostra come utilizzare le memory stick USB con Linux. In ogni caso, funziona anche per altre periferiche, come le macchine digitali che agiscono come se fossero periferiche di archiviazione USB

## Contents

*   [1 Scaricare un Kernel che supporti l'usb storage](#Scaricare_un_Kernel_che_supporti_l.27usb_storage)
*   [2 Montare una periferica di memoria USB](#Montare_una_periferica_di_memoria_USB)
*   [3 Ripartizionare la Chiavetta USB](#Ripartizionare_la_Chiavetta_USB)
*   [4 Montare una penna USB come utente normale](#Montare_una_penna_USB_come_utente_normale)

## Scaricare un Kernel che supporti l'usb storage

Se non utilizzate un kernel realizzato ad-hox da voi stessti, avete già tutto l'occorrente poichè i kernel standard di Arch Linux sono già correttamente configurati. Se invece utilizzate un vostro kernel, assicuratevi che sia stato compilato con il supporto SCSI, SCSI-Disk-Support e usb_storage. Se usate l'ultima versione di [udev](/index.php/Udev "Udev"), sarà necessario solamente collegare la periferica alla porta USB, e il sistema caricherà automaticamente tutti i moduli del kernel necessari. Le versioni più vecchie di udev potrebbero necessitare anche dell'installazione di [hotplug](/index.php?title=HotPlug&action=edit&redlink=1 "HotPlug (page does not exist)") o in alternativa, potreste caricare manualmente il modulo:

```
# modprobe usb-storage
# modprobe sd_mod      (solo per kernel non-SCSI)

```

## Montare una periferica di memoria USB

Dopo aver inserito lo spinotto nella porta USB, potete montare la periferica da root con

```
# mount -t vfat /dev/sda1 /mnt/usbstick

```

Nota: /dev/sda1 è variabile. Se il vostro Hard Disk principale è identificato come /dev/sda1, probabilmente dovrete usare /dev/sdb1 al suo posto. Per capire con certezza a quale device sia collegata la vostra periferica esterna, utilizzate il comando dmesg | grep /dev/sd . Usate inoltre il comando lsusb per verificare che la periferica sia effettivamente riconosciuta dal sistema, se avete a che fare con degli errori.

L'opzione `-t` specifica il tipo di filesystem. Se la periferica è formattata come fat32, usate il parametro `vfat`. Di default, una periferica `sdx` si assume come formattata come fat32, quindi in questo caso questa opzione potrebbe essere omessa.

**Nota:** la cartella dove volete montare la periferica, deve essere già esistente prima che diate il comando di montaggio.

Se usate [KDE](/index.php/KDE_(Italiano) "KDE (Italiano)") o [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)"), essi dovrebbero visualizzare automaticamente la periferica inserita sul desktop, quindi non vi sarà necessario montarla manualmente.

Se ottenete un errore del tipo "Error org.freedesktop.DBus.Error.AccessDenied.", provate ad aggiungere il vostro utente al gruppo `storage`:

```
# gpasswd -a nomeutente storage

```

## Ripartizionare la Chiavetta USB

A volte una chiavetta può essere suddivisa in più partizioni, fino a 4, e il sistema Linux non riesce a leggere nulla. Per sistemare la faccenda, sarà necessario ripartizionare la chiavetta con `fdisk`. Assicuratevi che non siano rimasti più file importanti sulla chiavetta prima di cominciare (se l'avete ad esempio usata su un sistema Windows, MacOs o altro). Ecco cosa fare:

```
# modprobe usb_storage
# fdisk /dev/sda

```

Rimuovete tutte le partizioni presenti (tasto `d` e il numero della partizione), create una nuova partizione unica col tasto `n` (è suggerita un'unica partizione), infine premete `q` per scrivere il tutto sulla chiavetta, e per poi chiudere.

Create dunque un filesystem sulla chiavetta:

```
# mkfs.vfat /dev/sda1

```

Se non avete il comando `mkfs.vfat` sul vostro sistema, potreste aver bisogno di installare con pacman il pacchetto [dosfstools](https://www.archlinux.org/packages/?name=dosfstools):

```
# pacman -S dosfstools

```

Adesso la chiavetta dovrebbe montare e smontare come già descritto sopra.

## Montare una penna USB come utente normale

Se desiderate che i normali utenti non-root siano abilitati a montare delle penne USB, aggiungete la seguente riga al file `/etc/fstab`:

```
/dev/sda1 /mnt/usbstick vfat noauto,user 0 0

```

potete sostituire `/mnt/usbstick` con la cartella che preferite.