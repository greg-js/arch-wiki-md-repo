Se avete dimenticato la password di root questa guida vi aiutera' a recuperarla. Ci sono diversi metodi per ottenere il risultato desiderato:

## Contents

*   [1 Usare un LiveCD](#Usare_un_LiveCD)
    *   [1.1 Change Root](#Change_Root)
    *   [1.2 Eliminare la password](#Eliminare_la_password)
*   [2 Utilizzare GRUB per richiamare Bash](#Utilizzare_GRUB_per_richiamare_Bash)
*   [3 Risorse ( in inglese)](#Risorse_.28_in_inglese.29)

## Usare un LiveCD

Utilizzando un LiveCd ci sono un paio di metodi: utilizzare "change root" ed eseguire il comando `passwd` oppure eliminare il campo password. Può essere utilizzato qualunque LiveCd, tuttavia per utilizzare il metodo "chroot" si deve usarne uno che abbia lo stesso tipo di architettura.

### Change Root

1.  Avviare il LiveCD , quindi [change root](/index.php/Change_root "Change root").
2.  Utilizzare il comando `passwd` per resettare la password di root
3.  Exit [change root](/index.php/Change_root "Change root").
4.  Riavviare (non dimenticando la nuova password!)

### Eliminare la password

1 Avviare un LiveCD e montare la partizione principale ( **/** ). Ad esempio:

```
mkdir /mnt/arch
mount /dev/sda2 /mnt/arch

```

2\. Modificare il file password utilizzando un editor. Ad esempio vim:

```
vim /mnt/etc/shadow

```

3\. Eliminare il secondo campo nella linea contenente root ( in [vim](/index.php/Vim_(Italiano) "Vim (Italiano)") e' possibile farlo andando sulla prima lettera/simbolo del campo e premendo **d/:/** e poi **Enter**):

```
root:**$1$9gDquXRP$gbOHLXuqslL.rw81q4pHc1**:14589::::::

```

4\. Salvare il file (**:x** in vim).

5\. Riavviare . Il login come "root" non richiederà la password.

## Utilizzare GRUB per richiamare Bash

1\. Selezionare l'appropriata riga di avvio nel menù di GRUB e premere **e** per modificare la riga.

2\. Selezionare la riga del kernel e premere nuovamente **e** per modificarne il contenuto.

3\. Aggiungere `init=/bin/bash` alla fine della riga.

4\. Premere **b** per avviare il sistema (il cambiamento sara' temporaneo e non verrà salvato nel menu.lst). Dopo l'avvio vi troverete ad un bash prompt.

5\. Il file system principale sarà probabilmente montato in sola lettura, quindi rimontatelo in lettura/scrittura:

```
# mount -n -o remount,rw /

```

6\. Usate il comando `passwd` per creare una nuova password di root.

7\. Riavviare (e non dimenticate la nuova password!)

**Note:** Con questo metodo alcune tastiere potrebbero non essere caricate correttamente dal system init e potreste non essere in grado di scrivere nulla al prompt. In tal caso utilizzate un altro metodo.

## Risorse ( in inglese)

*   vedere [questa guida](http://www.howtoforge.com/how-to-reset-a-forgotten-root-password-with-knoppix-p2) come esempio.