Tra i pacchetti adottabili sulla propria macchina sicuramente non possono mancare quelli relativi alla diagnostica del proprio hardware, per una semplice ragione: se qualche scheda inizia a comportarsi male si è in grado di intervenire tempestivamente.

Possiamo distinguere e definire due categorie di programmi, per lo meno relativi al contesto in cui siamo, ossia: i programmi agenti e i frontend. I programmi agenti li consideriamo quella classe di programmi che lavora a basso livello e leggono dall'hardware direttamente. I frontend sono semplici interfacce fornite di una gui che semplificano l'uso agendo ad alto livello.

Iniziamo con i programmi agenti.

## Contents

*   [1 Programmi Agenti](#Programmi_Agenti)
    *   [1.1 Temperature](#Temperature)
    *   [1.2 Pulsanti di Alimentazione](#Pulsanti_di_Alimentazione)
    *   [1.3 Ram](#Ram)
    *   [1.4 Hard Disk](#Hard_Disk)
*   [2 Frontend](#Frontend)

## Programmi Agenti

### Temperature

Cominciamo dalle temperature: [lm_sensors](/index.php/Lm_sensors "Lm sensors") configurazione:

```
pacman -S lm_sensors 

```

```
sensors-detect (parte il tutorial)

```

[..] Seguiamo le domande selezionando tra tutto quello che lo script ci propone ciò che serve alla nostra macchina, fino a giungere al riepilogo:

```
Now follows a summary of the probes I have just done. 
Just press ENTER to continue: 

```

continuo. in fine:

```
Do you want to generate /etc/sysconfig/lm_sensors? (yes/NO): yes 

```

Ora controlliamo che tutto funzioni. Da root digitare:

```
modprobe i2c-i801 modprobe eeprom modprobe w83627ehf sensors

```

Con l’ultima riga dovremmo avere l’output del programma. Se tutto va bene inseriamo i moduli nell’array MODULES del file /etc/rc.conf . Ecco il mio array:

```
MODULES=(8139too mii i2c-i801 eeprom w83627ehf).

```

### Pulsanti di Alimentazione

```
pacman -S acpid 

```

migliora la gestione dei pulsanti di accensione del computer. Se premuto più volte lo stesso, la macchina verrà spenta in modo regolare. Per il suo funzionamento sarà necessario inserire il denome @acpid in /etc/rc.conf (consiglio: @ da background). Dentro /proc/acpi trovate delle statistiche sull’utilizzo della macchina, sono molto utili

### Ram

Cosa importante è il memtest, ossia un’immagine da boot per avviare un test sulla ram.

```
pacman -S memtest86+ 

```

Per il suo funzionamento sarà necessario inserire in /boot/grub/menu.lst queste righe:

```
1\. Memtest 
title Memtest86+ [/boot/memtest86+/memtest.bin]
root (hd0,0) kernel /boot/memtest86+/memtest.bin

```

Io uso grub. Se usate lilo dovete editare il file lilo.conf .

### Hard Disk

Per l’hd sarà molto utile il supporto [S.M.A.R.T](/index.php/SMART "SMART"). Prima di tutto va abilitato da bios, potrà tenere sotto controllo lo stato dei dischi se gestito da un programma. Può mostrarsi vitale in certi casi.

```
pacman -S smartmontools 

```

Per il suo funzionamento sarà necessario inserire il demone in /etc/rc.conf:

```
@smartd 

```

Una volta che smartd è attivo datevi una lettura a [questo wiki](http://guide.debianizzati.org/index.php/Gestire_gli_HD:_stato_di_salute,_badblocks_e_ripristino_dati).

Io ho usato subito:

```
smartctl -a /dev/hda smartctl -H /dev/hda

```

Normalmente il demone è disattivato, anche se viene caricato. Per attivarlo sarà necessario farlo attraverso il file dei demoni. Occorre considerare che arch non è del tutto ordinatissima. Normalmente i files per i daemons di startup li trovi su /etc/conf.d Ho detto quasi di proposito non è del tutto ordinata perchè quello di smart si trova su /etc/smartd.conf Qui andremo a decommentare la riga che ci serve. Io ho decommentato questa:

```
/dev/sda -a -d sat -o on -S on -s (S/../.././02|L/../../6/03) -m root@localhost

```

Così facendo istruiamo smartmontools a fare un controllo del disco ogni giorno alle 02.00 e un controllo approfondito ogni sabato alle 03.00\. Inoltre salva i parametri del disco e in caso di anomalie manda una mail a root (se si è configurato sendmail). In caso di più dischi si possono usare orari differenti per effettuare i controlli approfonditi

```
/dev/sda -a -d sat -o on -S on -s (S/../.././02|L/../../6/03) -m root@localhost
/dev/sdb -a -d sat -o on -S on -s (S/../.././02|L/../../6/04) -m root@localhost
/dev/sdc -a -d sat -o on -S on -s (S/../.././02|L/../../6/05) -m root@localhost

```

## Frontend

Parliamo ora dei frontend. Ci sono 3 modi principali per monitorare quanto installato. La scelta è tra le applet del pannello del vostro DE scelto, **conky** oppure **gkrellm**.

**gkrellm** offre una discreta disponibilità di servizi integrati ma è espandibile tramite plugins.

Alcune utili estensioni per gkrellm:

*   **gkhdplop**: mostra l’attività sui dischi tramite effetti grafici, carino da vedere e rende lo stato dei dischi a colpo d’occhio;
*   **gkleds**: rappresentano dei segnalatori di blockNum capsLock e scrollLock attivabili/disattivabili anche tramite click;
*   **gkx86info**: mostra la velocità attuale della cpu;
*   **gkrelltop**: mostra i top-x processi in esecuzione visualizzando il carico di lavoro corrente tramite una barra colorata, molto utile per vedere se usare ad esempio un browser piuttosto che un altro;
*   **gkrellmpager**: visualizza e naviga tra i desktops virtuali;
*   **gkrellmapcupsd**: tiene sottocontrollo lo stato di un gruppo di continuità APC.

**conky**: una volta avviato il demone hddtemp è possibile configurare conky, un desklet configurabile tramite file di testo, a visualizzare la temperatura richiamadosela via telnet; cosa simile avviene con la temperatura del processore che viene richiamata dal desklet via ACPI.

Per concludere, propongo un esempio di array modules e daemons presenti in /etc/rc.conf che permettono di usufruire di questi servizi:

```
MODULES=(8139too mii i2c-i801 eeprom w83627ehf capability thermal)
DAEMONS=(@syslog-ng @network !netfs @crond alsamixer @hal @dbus @acpid @smartd @apcupsd @hddtemp)

```

end.