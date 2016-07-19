[Bluetooth](http://www.bluetooth.org/) è uno standard per l'interconnessione a corto raggio senza fili dei telefoni cellulari, dei computer e di altri dispositivi elettronici. In Linux, il protocollo Bluetooth è implementato da [BlueZ](http://www.bluez.org/)

## Contents

*   [1 Installazione](#Installazione)
*   [2 Interfacce grafiche](#Interfacce_grafiche)
    *   [2.1 Blueman](#Blueman)
        *   [2.1.1 Script per Thunar](#Script_per_Thunar)
    *   [2.2 GNOME Bluetooth](#GNOME_Bluetooth)
    *   [2.3 BlueDevil](#BlueDevil)
    *   [2.4 Fluxbox, Openbox, ed altri WM](#Fluxbox.2C_Openbox.2C_ed_altri_WM)
*   [3 Configurazione manuale](#Configurazione_manuale)
    *   [3.1 Streaming Audio](#Streaming_Audio)
*   [4 Pairing](#Pairing)
*   [5 Usare Obex per l'invio e la ricezione dei files](#Usare_Obex_per_l.27invio_e_la_ricezione_dei_files)
*   [6 Esempi](#Esempi)
    *   [6.1 Siemens S55](#Siemens_S55)
    *   [6.2 Logitech Mouse MX Laser / M555b](#Logitech_Mouse_MX_Laser_.2F_M555b)
    *   [6.3 Motorola V900](#Motorola_V900)
    *   [6.4 Motorola RAZ](#Motorola_RAZ)
    *   [6.5 Sincronizzare un iPhone utilizzando bluez-simple-agent](#Sincronizzare_un_iPhone_utilizzando_bluez-simple-agent)
    *   [6.6 Auricolari e Dispositivi Alsa](#Auricolari_e_Dispositivi_Alsa)
*   [7 Errori e risoluzione di problemi](#Errori_e_risoluzione_di_problemi)
    *   [7.1 Segfaults in Bluez 4.95](#Segfaults_in_Bluez_4.95)
    *   [7.2 passkey-agent](#passkey-agent)
    *   [7.3 Blueman](#Blueman_2)
    *   [7.4 gnome-bluetooth](#gnome-bluetooth)
    *   [7.5 Bluetooth USB Dongle](#Bluetooth_USB_Dongle)
    *   [7.6 Logitech Bluetooth USB Dongle](#Logitech_Bluetooth_USB_Dongle)
    *   [7.7 hcitool scan: Dispositivo non rilevato](#hcitool_scan:_Dispositivo_non_rilevato)
    *   [7.8 Il mio computer non è visibile](#Il_mio_computer_non_.C3.A8_visibile)
    *   [7.9 GNOME Files non può sfogliare file](#GNOME_Files_non_pu.C3.B2_sfogliare_file)
    *   [7.10 Bluetooth disabilitato all'avvio di gnome](#Bluetooth_disabilitato_all.27avvio_di_gnome)
    *   [7.11 Problemi di connessione con Sennheiser MM400 Headset](#Problemi_di_connessione_con_Sennheiser_MM400_Headset)
    *   [7.12 Il dispositivo è sincronizzato ma non emette alcun suono](#Il_dispositivo_.C3.A8_sincronizzato_ma_non_emette_alcun_suono)
*   [8 Ulteriori Risorse](#Ulteriori_Risorse)

## Installazione

Per utilizzare il Bluetooth, [installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") [bluez](https://www.archlinux.org/packages/?name=bluez), disponibile nei [Repository Ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)"). Una volta che il pacchetto è stato installato, i [demoni](/index.php/Daemon_(Italiano) "Daemon (Italiano)") `dbus` ed `bluetooth` devono essere, **nell'ordine** avviati.

**Nota:** E' importante che `dbus` sia avviato **prima** di `bluetooth`.

Il demone `dbus` dè utilizzato per leggere le impostazioni e per eseguire il pairing del PIN, mentre il demone `bluetooth` è richiesto per il protocollo Bluetooth.

Per avviare/riavviare/fermare il demone manualmente, utilizzare:

```
# rc.d {start|stop|restart} bluetooth

```

Se si utilizza [systemd](/index.php/Systemd "Systemd"), potrebbe essere necessario abilitare il servizio bluetooth:

```
 # systemctl enable bluetooth.service 
 # systemctl start bluetooth.service

```

## Interfacce grafiche

I seguenti pacchetti includono delle interfacce grafiche per la personalizzazione del Bluetooth.

### Blueman

[Blueman](http://blueman-project.org) è un manager completo e dotato di tutte le funzionalità per il Bluetooth, scritto in [GTK+](/index.php/GTK%2B_(Italiano) "GTK+ (Italiano)") e, come tale, raccomandabile per [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)") o [Xfce](/index.php/Xfce_(Italiano) "Xfce (Italiano)"). E' possibile installare Blueman con il pacchetto [blueman](https://www.archlinux.org/packages/?name=blueman), disponibile nei [Repository Ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

Assicurarsi che il demone `bluetooth` sia avviato come descritto sopra (aggiunto in rc.conf dopo dbus) ed avviare `blueman-applet`. Per avviare l'applet al login aggiungere `blueman-applet` in *System -> Preferences -> Startup Applications* (GNOME) o *Xfce Menu -> Settings -> Session and Startup* (Xfce).

Per consentire ad un utente di aggiungere e gestire i dispositivi Bluetooth utilizzando Blueman, l'utente deve essere aggiunto al gruppo 'lp'. Vedere /etc/dbus-1/system.d/bluetooth.conf per la sezione che permette agli utenti del gruppo 'lp' di comunicare con il demone Bluetooth.

**Nota:** Se si esegue Blueman al di fuori di GNOME/GDM, ad esempio in Xfce utilizzando il comando `startx`, si dovrebbe aggiungere `. /etc/X11/xinit/xinitrc.d/*` all'inizio del proprio `~/.xinitrc` per abilitare GNOME Files ad esplorare i dispositivi.

Per ricevere i file non dimenticarsi di cliccare con il tasto destro del mouse su *Blueman tray icon -> Local Services -> Transfer -> File Receiving" e flaggare la casellina "Enabled".*

#### Script per Thunar

Se non si utilizza GNOME Files (ad esempio Thunar) potrebbe risultare molto utile il seguente script:

 `obex_thunar.sh` 
```
 #!/bin/bash
 fusermount -u ~/bluetooth
 obexfs -b $1 ~/bluetooth
 thunar ~/bluetooth

```

Ora bisognerà posizionare lo script nella directory appropriata (ad esempio, `/usr/bin`). Dopodichè, renderlo eseguibile:

 `chmod +x /usr/bin/obex_thunar.sh` 

L'ultimo passo è quello di cambiare la riga in *Local Services > Transfer > Advanced* in `obex_thunar.sh %d`.

### GNOME Bluetooth

[gnome-bluetooth](http://live.gnome.org/GnomeBluetooth) è un fork del datato *bluez-gnome*, ed è orientato ad integrarsi perfettamente in [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)"). GNOME Bluetooth è richiesto da [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell), percio, se si utilizza GNOME 3, già dovrebbe essere installato. Comunque, lo si può installare con il pacchetto [gnome-bluetooth](https://www.archlinux.org/packages/?name=gnome-bluetooth).

Eseguire `bluetooth-applet` per avere una gradevole applet Bluetooth. Si dovrebbe ora essere in grado di configurare i dispositivi ed inviare file cliccando col tasto destro sull'icona Bluetooth. Per avviare l'applet al login, aggiungerla a *System -> Preferences -> Startup Applications*.

Per aggiungere una voce "Inviare a" nel menu del Bluetooth, nel file di configurazione del menù di Thunar, consultare [questa pagina](http://thunar.xfce.org/pwiki/documentation/sendto_menu).

### BlueDevil

Lo strumento di gestione Bluetooth per [KDE](/index.php/KDE_(Italiano) "KDE (Italiano)") è [BlueDevil](https://projects.kde.org/projects/extragear/base/bluedevil). Esso può essere installato con il pacchetto [bluedevil](https://www.archlinux.org/packages/?name=bluedevil), disponibile nei [Repository Ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

Assicurarsi che il demone `bluetooth` sia in esecuzione, come descritto sopra. Dovrebbe apparire un'icona Bluetooth sia in Dolphin sia nel vassoio di sistema, da cui è possibile configurare BlueDevil e rilevare i dispositivi Bluetooth. E' possibile configurare BlueDevil anche da Impostazioni di Sistema di KDE.

### Fluxbox, Openbox, ed altri WM

Naturalmente è sempre possibile utilizzare le precedenti applicazioni anche se non si utilizzano GNOME, Xfce o KDE. Questo elenco dovrebbe aiutare a capire quale applicazione è più adatta alle proprie esigenze:

*   bluetooth-applet -- icona di vassoio con funzionalità di configurazione, sincronizzazione guidata, gestione dei dispositivi conosciuti.
*   /usr/lib/gnome-user-share/gnome-user-share -- deve essere in esecuzione se si è in procinto di ricevere file via obexBT da un dispositivo associato

se appare un errore durante la trasmissione e/o non ci sono i file ricevuti, aggiungere quanto segue, al file:

`/etc/dbus-1/system.d/bluetooth.conf`

```
 <policy user="your_user_id">
   <allow own="org.bluez"/>
   <allow send_destination="org.bluez"/>
   <allow send_interface="org.bluez.Agent"/>
 </policy>

```

*   bluetooth-wizard -- per i nuovi dispositivi da accoppiare
*   bluetooth-properties -- accessibile anche tramite l'icona bluetooth-applet
*   gnome-file-share-properties -- autorizzazioni per la ricezione di file via bluetooth
*   bluez-sendto -- GUI per l'invio di file a un dispositivo remoto

## Configurazione manuale

Per configurare manualmente BlueZ, è necessario modificare i file di configurazione presenti in `/etc/bluetooth`. Ossia:

```
audio.conf
input.conf
main.conf
network.conf
rfcomm.conf

```

La configurazione di default dovrebbe andar bene per la maggior parte dei casi. Le opzioni di configurazione possibili sono già ben documentate all'interno dei file stessi, quindi per un'eventuale modifica alle opzioni dovrebbe bastare leggere le relative descrizioni. Per le opzioni generali, iniziare con `main.conf`.

### Streaming Audio

Se si vuole abilitare lo streaming audio dal proprio dispositivo al computer, è necessario modificare `audio.conf` ed aggiungere quanto segue nella sezione `[General]`:

```
 Enable=Source

```

With bluez 4.98 and alsa-lib 1.0.24.1, you may have to try with:

```
 Enable=Socket

```

## Pairing

**Nota:** Questa sezione non è del tutto completa. Grazie Gattschardo per la soluzione del pin

Molti dispositivi bluetooth richiedono [pairing](https://en.wikipedia.org/wiki/Bluetooth#Pairing "wikipedia:Bluetooth"). L'esatto procedimento dipende, tra le altre cose, dai dispositivi utilizzati e dalle loro funzionalità. Il procedimento per collegare un telefono cellulare potrebbe essere una cosa di questo tipo:

*   Il computer invia una richiesta di connessione al telefono.
*   Il pin, determinato dal computer, viene accettato dal telefono
*   Lo stesso deve essere riconfermato dal computer.

Per eseguire una scansione in cerca di dispositivi, dare

```
 $> hcitool scan

```

Per sincronizzare un dispositivo senza usare il gnome-bluez package si può usare uno strumento chiamato *bluez-simple-agent* che fa parte di bluez package. Per poterlo utilizzare saranno necessari alcuni pacchetti python dai repositories ufficiali: dbus-python e pygobject. Una volta installati e pronti si può iniziare lo script da root:

```
 $> bluez-simple-agent

```

Se tutto funziona correttemente, si dovrebbe ottenere il messaggio "Agent registered" sulla console. Sarà possibile quindi iniziare la sincronizzazione dal dispositivo mobile, lo script vi richiederà il codice di accesso sulla console, lo si scriverà e confermerà con enter - fatto. Ora si potrà anche spegnere l' agent usando ^C-c, dato che è necessario solo per la prima sincronizzazione e non per ogni seguente connessione. Se non si possono rilevare computer dal telefono cellulare, consultare la sezione [Errori e risoluzione di problemi](#Il_mio_computer_non_.C3.A8_visibile).

Se si vuole associare un dispositivo "passivo" come un auricolare, è possibile fornire il relativo indirizzo per tentare l'associazione dal proprio computer:

```
$> bluez-simple-agent hci0 00:11:22:33:AA:BB

```

Alcuni esempi sono illustrati in basso nella relativa sezione.

## Usare Obex per l'invio e la ricezione dei files

Altra possibilità, piuttosto che utilizzare i pacchetti Bluetooth di KDE o GNOME, è Obexfs che permette il montaggio del telefono e lo considera come fosse parte del filesystem. Si noti che l'utilizzo di Obexfs richiede che il dispositivo supporti un servizio FTP Obex.

Per installarlo;

```
# pacman -S obexfs

```

il telefono può ora essere montato dando da root

```
# obexfs -b <devices mac address> /mountpoint

```

Per ulteriori opzioni di montaggio consultare [http://dev.zuckschwerdt.org/openobex/wiki/ObexFs](http://dev.zuckschwerdt.org/openobex/wiki/ObexFs)

Per i dispositivi che non supportanto il servizio Obex FTP, controllare se è supportato l'Obex Object Push.

```
# sdptool browse XX:XX:XX:XX:XX:XX

```

Leggere l'output, cercare Obex Object Push ed annotarsi il canale inerente quel servizio. Se supportao, è possibile utilizzare ussp-push per inviare file al dispositivo:

```
# ussp-push XX:XX:XX:XX:XX:XX@CHANNEL file wanted_file_name_on_phone

```

## Esempi

### Siemens S55

Passi eseguiti per la connessione di un S55\. (Non è stabilito come iniziare la connessione dal telefono)

*   Passi dopo l'installazione

```
  $> hcitool scan
  Scanning ...
          XX:XX:XX:XX:XX:XX  NAME
  $> B=XX:XX:XX:XX:XX:XX

```

Lanciare il simple-agent in un secondo terminale

```
  $> su -c bluez-simple-agent 
  Password: 
  Agent registered

```

Ritornare alla prima console

```
  $> obexftp -b $B -l "Address book"
  # Phone ask for pin, I enter it and answer yes when asked if I want to save the device
  ...
  <file name="5F07.adr" size="78712" modified="20030101T001858" user-perm="WD" group-perm="" />
  ...
  $> obexftp -b 00:01:E3:6B:FF:D7 -g "Address book/5F07.adr"
  Browsing 00:01:E3:6B:FF:D7 ...
  Channel: 5
  Connecting...done
  Receiving "Address book/5F07.adr"... Sending "Address book"... done
  Disconnecting...done
  $> obexftp -b 00:01:E3:6B:FF:D7 -p a                      
  ...
  Sending "a"... done
  Disconnecting...done

```

### Logitech Mouse MX Laser / M555b

Per verificare rapidamente la connessione:

```
$> hidd --connect XX:XX:XX:XX:XX:XX

```

Per la riconnessione automatica, utilizzare il desktop wizard per configurare il mouse bluetooth. Se l'ambiente desktop non include il supporto per questa attività, vedere la guida [Bluetooth mouse manual configuration](/index.php/Bluetooth_mouse_manual_configuration "Bluetooth mouse manual configuration").

### Motorola V900

Dopo aver installato blueman e avviato Blueman-applet, fare clic su "find me" sotto connessioni > bluetooth nel dispositivo motorola. In blueman-applet, eseguire una ricerca dei dispositivi, trovare motorola e cliccare su "aggiungi" nell'applet di blueman. Di seguito cliccare su "bond", digitare l'eventuale pin, e ridigitarlo nel motorola quando richiesto. Da terminale:

```
  cd ~/
  mkdir bluetooth-temp
  obexfs -n xx:yy:zz:... ~/bluetooth-temp
  cd ~/bluetooth-temp

```

e passare all'esplorazione. Sono disponibili solo immagini, audio e video quando si esegue questa operazione.

### Motorola RAZ

```
> pacman -S obextool obexfs obexftp openobex bluez

```

```
> lsusb
Bus 005 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 002 Device 002: ID 03f0:171d Hewlett-Packard Wireless (Bluetooth + WLAN) Interface [Integrated Module]
Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

```
> hciconfig hci0 up

```

```
> hciconfig
hci0:   Type: BR/EDR  Bus: USB
        BD Address: 00:16:41:97:BA:5E  ACL MTU: 1017:8  SCO MTU: 64:8
        UP RUNNING
        RX bytes:348 acl:0 sco:0 events:11 errors:0
        TX bytes:38 acl:0 sco:0 commands:11 errors:0

```

```
> hcitool dev
Devices:
        hci0    00:16:41:97:BA:5E

```

**Attenzione: assicurarsi che la funzione Bluetooth del telefono sia attivata e che il telefono sia visibile!**

```
> hcitool scan
Scanning ...
        00:1A:1B:82:9B:6D       [quirxi]

```

```
> hcitool inq
Inquiring ...
        00:1A:1B:82:9B:6D       clock offset: 0x1ee4    class: 0x522204

```

```
> l2ping 00:1A:1B:82:9B:6D
Ping: 00:1A:1B:82:9B:6D from 00:16:41:97:BA:5E (data size 44) ...
44 bytes from 00:1A:1B:82:9B:6D id 0 time 23.94ms
44 bytes from 00:1A:1B:82:9B:6D id 1 time 18.85ms
44 bytes from 00:1A:1B:82:9B:6D id 2 time 30.88ms
44 bytes from 00:1A:1B:82:9B:6D id 3 time 18.88ms
44 bytes from 00:1A:1B:82:9B:6D id 4 time 17.88ms
44 bytes from 00:1A:1B:82:9B:6D id 5 time 17.88ms
6 sent, 6 received, 0% loss

```

```
> hcitool name  00:1A:1B:82:9B:6D
[quirxi]

```

```
# hciconfig -a hci0
hci0:   Type: BR/EDR  Bus: USB
        BD Address: 00:16:41:97:BA:5E  ACL MTU: 1017:8  SCO MTU: 64:8
        UP RUNNING
        RX bytes:9740 acl:122 sco:0 events:170 errors:0
        TX bytes:2920 acl:125 sco:0 commands:53 errors:0
        Features: 0xff 0xff 0x8d 0xfe 0x9b 0xf9 0x00 0x80
        Packet type: DM1 DM3 DM5 DH1 DH3 DH5 HV1 HV2 HV3
        Link policy:
        Link mode: SLAVE ACCEPT
        Name: 'BCM2045'
        Class: 0x000000
        Service Classes: Unspecified
        Device Class: Miscellaneous,
        HCI Version: 2.0 (0x3)  Revision: 0x204a
        LMP Version: 2.0 (0x3)  Subversion: 0x4176
        Manufacturer: Broadcoml / Corporation (15)

```

```
> hcitool info 00:1A:1B:82:9B:6D
Requesting information ...
        BD Address:  00:1A:1B:82:9B:6D
        Device Name: [quirxi]
        LMP Version: 1.2 (0x2) LMP Subversion: 0x309
        Manufacturer: Broadcom Corporation (15)
        Features: 0xff 0xfe 0x0d 0x00 0x08 0x08 0x00 0x00
                <3-slot packets> <5-slot packets> <encryption> <slot offset>
                <timing accuracy> <role switch> <hold mode> <sniff mode>
                <RSSI> <channel quality> <SCO link> <HV2 packets>
                <HV3 packets> <A-law log> <CVSD> <power control>
                <transparent SCO> <AFH cap. slave> <AFH cap. master>

```

**Modificare il file main.conf e inserire la classe adatta al proprio cellulare ( Class = 0x100100 ):**

```
> vim /etc/bluetooth/main.conf

```

```
  # Default device class. Only the major and minor device class bits are
  # considered.
  #Class = 0x000100
  Class =  0x100100

```

```
> /etc/rc.d/dbus start
:: Starting D-BUS system messagebus 
[DONE]

```

```
> /etc/rc.d/bluetooth start
:: Stopping bluetooth subsystem:  pand dund rfcomm hidd  bluetoothd
[DONE]
:: Starting bluetooth subsystem:  bluetoothd

```

**La sincronizzazione con bluez-simple-agent deve essere fatta solo una volta. Immettere sul telefono cellulare Motorola il pin 0000 quando richiesto !!**

```
> /usr/bin/bluez-simple-agent hci0 00:1A:1B:82:9B:6D
RequestPinCode (/org/bluez/10768/hci0/dev_00_1A_1B_82_9B_6D)
Enter PIN Code: 0000
Release
New device (/org/bluez/10768/hci0/dev_00_1A_1B_82_9B_6D)

```

**Ora è possibile navigare il filesystem del telefono con obexftp:**

```
> obexftp -v -b 00:1A:1B:82:9B:6D -B 9 -l
Connecting..\done
Tried to connect for 448ms
Receiving "(null)"...-<?xml version="1.0" ?>
<!DOCTYPE folder-listing SYSTEM "obex-folder-listing.dtd">
<folder-listing>
<parent-folder />
<folder name="audio" size="0" type="folder" modified="20101010T132323Z" user-perm="RW" />
<folder name="video" size="0" type="folder" modified="20101010T132323Z" user-perm="RW" />
<folder name="picture" size="0" type="folder" modified="20101010T132323Z" user-perm="RW" />
</folder-listing>
done
Disconnecting..\done

```

**Oppure si può montare il cellulare in una directory del computer e operarvi come in un normale file system:**

```
> groupadd bluetooth
> mkdir /mnt/bluetooth
> chown root:bluetooth /mnt/bluetooth
> chmod 775 /mnt/bluetooth
> usermod -a -G bluetooth arno

```

```
> obexfs -b 00:1A:1B:82:9B:6D /mnt/bluetooth/
> l /mnt/bluetooth/
total 6
drwxr-xr-x 1 root root    0 10\. Okt 13:25 .
drwxr-xr-x 5 root root 4096 10\. Okt 10:08 ..
drwxr-xr-x 1 root root    0 10\. Okt 2010  audio
drwxr-xr-x 1 root root    0 10\. Okt 2010  picture
drwxr-xr-x 1 root root    0 10\. Okt 2010  video

```

### Sincronizzare un iPhone utilizzando bluez-simple-agent

Supponendo si abbia un dispositivo bluetooth chiamato hci0 e un iPhone visualizzato in uno scan hcitool come '00:00:DE:AD:BE:EF':

```
   # bluez-simple-agent hci0 00:00:DE:AD:BE:EF
   Passcode:

```

### Auricolari e Dispositivi Alsa

1\. Se non è stato già fatto, installare bluez

```
# pacman -S bluez 	 	

```

2\. Effettuare lo scan del dispositivo

```
$ hcitool (-i <optional hci#>***) scan

```

3\. Sincronizzare l'auricolare con il dispositivo

```
$ bluez-simple-agent (optional hci# ***) XX:XX:XX:XX:XX:XX
ed inserire il codice pin (0000 oppure 1234, ecc)

```

4\. Aggiungere quanto segue al file /etc/asound.conf

```
#/etc/asound.conf

pcm.btheadset {
   type plug
   slave {
       pcm {
	    type bluetooth
	    device XX:XX:XX:XX:XX:XX
	    profile "auto"
	} 
   } 
   hint {
	 show on
	 description "BT Headset"
   } 
}
ctl.btheadset {
  type bluetooth
}

```

5\. Controllare se il dispositivo è stato aggiunto ai dispositivi alsa

```
$ aplay -L

```

6\. Ora avviare la riproduzione con aplay:

```
$ aplay -D btheadset /path/to/audio/file 

```

oppure Mplayer:

```
$ mplayer -ao alsa:device=btheadset /path/to/audio/or/video/file

```

*   *   *   Per trovare hci# per l'usb, digitare

```
$ hcitool dev

```

## Errori e risoluzione di problemi

### Segfaults in Bluez 4.95

Se bluetoothd smette di funzionare dopo aver abilitato o disabilitato tramite rfkill o la gnome-bluetooth applet il dispositivo bluetooth, vedere l'output di dmesg. Se è simile a questo:

```
bluetoothd[2330]: segfault at 1 ip 00007fcef2327b75 sp 00007fff9f769cb0 error 4 in libglib-2.0.so.0.2800.8[7fcef22ca000+e9000]

```

allora si dovrebbe prendere in considerazione l'idea di effettuare un downgrade alla versione 4.94 (semplicemente prendere il PKGBUILD/etc da arch, modificare la versione alla 4.94 e correggere l'md5sum di bluez) oppure attendere un aggiornamento di bluez. [Qui](https://bugs.archlinux.org/task/25088?project=1&openedfrom=-1+week) c'è un bugreport (arch) inerente l'argomento.

### passkey-agent

```
$> passkey-agent --default 1234
Can't register passkey agent
The name org.bluez was not provided by any .service files

```

Probabilmente è stato avviato `/etc/rc.d/bluetooth` prima di `/etc/rc.d/dbus`

```
$> hciconfig dev
# (no listing)

```

Provare a lanciare `hciconfig hc0 up`

### Blueman

Se blueman-applet non si avvia, provare a rimuovere l'intera cartella */var/lib/bluetooth* e riavviare la macchina (o solo HAL, dbus, e servizi bluetooth).

```
# rm -rf /var/lib/bluetooth
# reboot

```

### gnome-bluetooth

Se mentre si abilita la ricezione dei files in bluetooth-properties si visualizza:

```
 Bluetooth OBEX start failed: Invalid path
 Bluetooth FTP start failed: Invalid path

```

Quindi eseguire:

```
 # pacman -S xdg-user-dirs
 $ xdg-user-dirs-update

```

Si può visualizzare il percorso con:

```
 $ vi ~/.config/user-dirs.dirs

```

### Bluetooth USB Dongle

Se si utilizza un USB dongle, sarebbe bene controllare che il Bluetooth dongle venga riconosciuto. Lo si può fare verificando `/var/log/messages.log` quando si collega l'USB dongle. Dovrebbe assomigliare a qualcosa del genere (cercando hci):

```
# tail -f /var/log/messages.log
Feb 20 15:00:24 hostname kernel: [ 2661.349823] usb 4-1: new full-speed USB device number 3 using uhci_hcd
Feb 20 15:00:24 hostname bluetoothd[4568]: HCI dev 0 registered
Feb 20 15:00:24 hostname bluetoothd[4568]: Listening for HCI events on hci0
Feb 20 15:00:25 hostname bluetoothd[4568]: HCI dev 0 up
Feb 20 15:00:25 hostname bluetoothd[4568]: Adapter /org/bluez/4568/hci0 has been enabled

```

Per una lista di hardware supportato consultare la sezione [fonti](/index.php/Bluetooth_(Italiano)#Fonti "Bluetooth (Italiano)") in questa pagina.

Se si ottengono solo le prime due righe, si può osservare che il dispositivo è stato rilevato, ma è necessario "attivarlo". Esempio:

```
hciconfig -a hci0
hci0:	Type: USB
	BD Address: 00:00:00:00:00:00 ACL MTU: 0:0 SCO MTU: 0:0
	DOWN 
	RX bytes:0 acl:0 sco:0 events:0 errors:0
	TX bytes:0 acl:0 sco:0 commands:0 errors:
sudo hciconfig hci0 up
hciconfig -a hci0
hci0:	Type: USB
	BD Address: 00:02:72:C4:7C:06 ACL MTU: 377:10 SCO MTU: 64:8
	UP RUNNING 
	RX bytes:348 acl:0 sco:0 events:11 errors:0
	TX bytes:38 acl:0 sco:0 commands:11 errors:0

```

Se si ottiene un errore simile a questo:

```
 Operation not possible due to RF-kill 

```

potrebbe essere dovuto all'utility `rfkill`, in tal si dovrebbe risolvere con

```
 # rfkill unblock all 

```

oppure, potrebbe semplicemente essere dovuto allo switch hardware del computer. Lo switch hardware bluetooth (almeno a volte) controlla anche l'accesso al dongle bluetooth USB. Premere lo switch e riprovare nuovamente con il dispositivo.

Per verificare che il dispositivo è stato rilevato è possibile adoperare `hcitool` appartenente a `bluez-utils`. Si ottiene una lista di dispositivi, gli identificativi e gli indirizzi MAC:

```
$ hcitool dev
Devices:
        hci0	00:1B:DC:0F:DB:40

```

Ulteriori informazioni dettagliate circa i dispositivi possono essere ottenute con `hciconfig`.

```
$ hciconfig -a hci0
hci0:   Type: USB
        BD Address: 00:1B:DC:0F:DB:40 ACL MTU: 310:10 SCO MTU: 64:8
        UP RUNNING PSCAN ISCAN 
        RX bytes:1226 acl:0 sco:0 events:27 errors:0
        TX bytes:351 acl:0 sco:0 commands:26 errors:0
        Features: 0xff 0xff 0x8f 0xfe 0x9b 0xf9 0x00 0x80
        Packet type: DM1 DM3 DM5 DH1 DH3 DH5 HV1 HV2 HV3 
        Link policy: RSWITCH HOLD SNIFF PARK 
        Link mode: SLAVE ACCEPT 
        Name: 'BlueZ (0)'
        Class: 0x000100
        Service Classes: Unspecified
        Device Class: Computer, Uncategorized
        HCI Ver: 2.0 (0x3) HCI Rev: 0xc5c LMP Ver: 2.0 (0x3) LMP Subver: 0xc5c
        Manufacturer: Cambridge Silicon Radio (10)

```

### Logitech Bluetooth USB Dongle

Ci sono dongle Logitech (ad es. Logitech MX5000) che possono funzionare in due modalità: Embedded ed HCI. In modalità embedded il dongle emula un dispositivo USB, quindi sembrerà che il proprio PC stia utilizzando un/una normale mouse/tastiera USB.

Se si tiene premuto il piccolo Bottone rosso sul mini-ricevitore BT USB verrà abilitata l'altra modalità. Tenere premuto il pulsante rosso sul dongle BT e collegarlo al computer, dopo 3-5 secondi che si tiene premuto il pulsante, l'icona Bluetooth apparirà nel vassoio di sistema. [Discussione](http://ubuntuforums.org/showthread.php?t=1332197)

### hcitool scan: Dispositivo non rilevato

Su alcuni portatili Dell (per esempio Studio 15) è necessario scambiare il Bluetooth mode da HID a HCI usando

```
# hid2hci

```

**Nota:** hid2hci si trova in /lib/udev/hid2hci, ed udev si occuperà di avviarlo automaticamente.

*   Se il dispositivo non risulta attivo e sulla propria macchina si ha un sistema Windows, provare ad avviarlo ed attivare l'adattatore bluetooth da Windows.

*   A volte anche questo semplice comando risulta utile:

```
# hciconfig hci0 up

```

### Il mio computer non è visibile

Se non è possibile rilevarere il computer dal cellulare, si possono abilitare PSCAN e iSCAN:

```
# enable PSCAN and ISCAN
$ hciconfig hci0 piscan 
# check it worked
$ hciconfig 
hci0:   Type: USB
        BD Address: 00:12:34:56:78:9A ACL MTU: 192:8 SCO MTU: 64:8
        **UP RUNNING PSCAN ISCAN**
        RX bytes:20425 acl:115 sco:0 events:526 errors:0
        TX bytes:5543 acl:84 sco:0 commands:340 errors:0

```

**Nota:** Controllare DiscoverableTimeout e PairableTimeout in /etc/bluetooth/main.conf

Provare a modificare, in /etc/bluetooth/main.conf, la classe del dispositivo, come segue:

```
# Default device class. Only the major and minor device class bits are
# considered.
#Class = 0x000100 (from default config)
Class = 0x100100

```

Per alcuni è stata l'unica soluzione per rendere visibile il pc dal telefono.

### GNOME Files non può sfogliare file

Se GNOME Files non si apre e mostra questo errore:

```
Nautilus cannot handle obex: locations. Couldn't display "obex://[XX:XX:XX:XX:XX:XX]/".

```

Installare il pacchetto gvfs-obexftp:

```
# pacman -S gvfs-obexftp

```

### Bluetooth disabilitato all'avvio di gnome

Se si hanno `dbus` e `bluetooth` avviati in background (@) nel proprio array `DAEMONS` nel file `/etc/rc.conf`, potrebbe accadere che il `bluetooth` venga disabilitato all'avvio di GNOME. Per risovlere, assicurarsi che `dbus` non venga avviato in background.

### Problemi di connessione con Sennheiser MM400 Headset

Se il proprio `Sennheiser MM400 Headset` si disconnette immediatamente dopo essersi connesso come `Headset Service` con Blueman, provare a connetterlo come `Audio Sink`. In altre parole è possibile cambiare `Audio Profile` in `Telephony Duplex` con il tasto destro in Blueman. Con questa opzione, la funzionalità dell'auricolare sarà disponibile anche se collegato solo come `Audio Sink` al primo posto e non avverrà alcuna disconnessione (testato con bluez 4.96-3, pulseaudio 1.1-1 e blueman 1.23-2).

### Il dispositivo è sincronizzato ma non emette alcun suono

Provare a leggere il file di log: **/var/log/messages.log**

```
# tail /var/log/messages.log
Jan 12 20:08:58 localhost pulseaudio[1584]: [pulseaudio] module-bluetooth-device.c: Service not connected
Jan 12 20:08:58 localhost pulseaudio[1584]: [pulseaudio] module-bluetooth-device.c: Bluetooth audio service not available
```

Se si visualizzano questi messaggi, provare:

 `# pactl load-module module-bluetooth-device` 

Se il modulo non viene caricato, utilizare questa procedura: Aprire **/etc/bluetooth/audio.conf** ed aggiungere dopo **[General]** (in una nuova riga)

 `Enable=Socket` 

Quindi riavviare il demone Bluetooth con `/etc/rc.d/bluetooth restart`. Sincronizzare nuovamente il dispositivo; lo si dovrebbe trovare nelle impostazioni di pulseaudio (impostazioni avanzate per il suono)

[Maggiori informazioni sul Wiki di Gentoo](http://wiki.gentoo.org/index.php?title=Bluetooth_Headset&redirect=no)

Se nonostante questo si continua a non udire alcun suono, provare ad utilizzare blueman (l'unico metodo che sembra funzionare), assicurarsi che notify-osd sia installato, o si potrebbe ottenere un messaggio di errore simile a questo: "Stream setup failed"

fail (/usr/lib/python2.7/site-packages/blueman/gui/manager/ManagerDeviceMenu.py:134) fail (DBusException(dbus.String(u'Stream setup failed'),),)

## Ulteriori Risorse

*   [Guida Bluetooth di Gentoo](http://www.gentoo.org/doc/en/bluetooth-guide.xml)
*   [Lista di compatibilità hardware su openSUSE](http://en.opensuse.org/HCL:Bluetooth)
*   [Accedere a telefoni Bluetooth (Linux Gazette)](http://linuxgazette.net/109/oregan3.html)
*   [Visibilità computer Bluetooth](http://www.adamish.com/blog/#a000361)