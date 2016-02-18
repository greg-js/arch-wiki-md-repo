## Contents

*   [1 Instalace](#Instalace)
*   [2 Grafické nadstavby](#Grafick.C3.A9_nadstavby)
    *   [2.1 Blueman](#Blueman)
    *   [2.2 gnome-bluetooth](#gnome-bluetooth)
    *   [2.3 bluedevil](#bluedevil)
    *   [2.4 Fluxbox, openbox a další](#Fluxbox.2C_openbox_a_dal.C5.A1.C3.AD)
*   [3 Manuální konfigurace](#Manu.C3.A1ln.C3.AD_konfigurace)
*   [4 Párování](#P.C3.A1rov.C3.A1n.C3.AD)
*   [5 Použití Obex pro posílání a příjímání souborů](#Pou.C5.BEit.C3.AD_Obex_pro_pos.C3.ADl.C3.A1n.C3.AD_a_p.C5.99.C3.ADj.C3.ADm.C3.A1n.C3.AD_soubor.C5.AF)
*   [6 Příklady](#P.C5.99.C3.ADklady)
    *   [6.1 Siemens S55](#Siemens_S55)
    *   [6.2 Myš Logitech MX Laser / M555b](#My.C5.A1_Logitech_MX_Laser_.2F_M555b)
    *   [6.3 Motorola V900](#Motorola_V900)
    *   [6.4 Motorola RAZ](#Motorola_RAZ)
    *   [6.5 Párování iPhone použitím bluez-simple-agenta](#P.C3.A1rov.C3.A1n.C3.AD_iPhone_pou.C5.BEit.C3.ADm_bluez-simple-agenta)
*   [7 Řešení problémů](#.C5.98e.C5.A1en.C3.AD_probl.C3.A9m.C5.AF)
    *   [7.1 passkey-agent](#passkey-agent)
    *   [7.2 Blueman](#Blueman_2)
    *   [7.3 gnome-bluetooth](#gnome-bluetooth_2)
    *   [7.4 Bluetooth USB klíčenka](#Bluetooth_USB_kl.C3.AD.C4.8Denka)
    *   [7.5 hcitool scan: Device not found](#hcitool_scan:_Device_not_found)
    *   [7.6 Nelze nalézt počítač](#Nelze_nal.C3.A9zt_po.C4.8D.C3.ADta.C4.8D)
    *   [7.7 Nautilus nemůže procházet soubory](#Nautilus_nem.C5.AF.C5.BEe_proch.C3.A1zet_soubory)
*   [8 Zdroje](#Zdroje)

## Instalace

Pro použití bluetooth musíte mít nainstalován balíček [bluez](http://www.bluez.org):

```
# pacman -S bluez

```

Jakmile je balík bluez nainstalován, musí se spustit bluetooth a dbus daemon:

```
# /etc/rc.d/dbus start
# /etc/rc.d/bluetooth start

```

Dbus daemon se používá ke čtení nastavení a pro párování zařízení. Bluetooth daemon je potřeba pro komunikaci přes protokol Bluetooth. Je důležité, aby byl dbus spušten **dříve** než bluetooth. Jesliže dbus neběží a bluetooth daemon byl spuštěn, nastartujte znovu dbus a bluetooth daemona restartujte:

```
# /etc/rc.d/bluetooth restart

```

Pokud chcete spouštět bluetooth automaticky při startu počítače, přidejte bluetooth mezi pole daemonů v souboru [Rc.conf (Česky)](/index.php/Rc.conf_(%C4%8Cesky) "Rc.conf (Česky)") (daemon musí být umístěn až za dbus):

```
DAEMONS=(... bluetooth)

```

## Grafické nadstavby

Následující balíčky vám umožní využívat grafické prostředí k nastavování Bluetooth.

### Blueman

[blueman](/index.php/Blueman "Blueman") je program pro správu Bluetooth. Je naprogramován v GTK a používá se hlavně v [GNOME](/index.php/GNOME "GNOME") nebo [Xfce](/index.php/Xfce "Xfce"). Nainstalujte [blueman](https://www.archlinux.org/packages/?name=blueman) nebo [blueman-git](https://aur.archlinux.org/packages/blueman-git/) z [AUR](/index.php/AUR_(%C4%8Cesky) "AUR (Česky)").

Ujistěte se, že *bluetooth* daemon běží a spusťte příkaz *blueman-applet*. Pokud chcete, aby se applet spouštěl automaticky při přihlášení přidejte *blueman-applet* do *System -> Preferences -> Startup Applications* (GNOME) nebo v *Xfce Menu -> Settings -> Session and Startup* (Xfce).

Pozn.: Pokud nepoužíváte nautilus, může vám být užitečné toto:

```
#!/bin/bash
fusermount -u ~/bluetooth
obexfs -b $1 ~/bluetooth
thunar ~/bluetooth

```

bez fusermount -u /mountpoint pravděpodobně skončí s chybovou hláškou způsobenou nesprávným odpojením fuse filesystému.

Následně budete muset přesunout skript (obex_thunar.sh) do /usr/bin, a potom spustit:

```
$ chmod +x /usr/bin/obex_thunar.sh

```

Jako poslední věc byste měli změnit řádek v Local Services > Transfer > Advanced to obex_thunar.sh %d

### gnome-bluetooth

[gnome-bluetooth](https://www.archlinux.org/packages/?name=gnome-bluetooth) je odnož starého *bluez-gnome* a je zameřeno na integraci s desktopovým prostředím GNOME. Nejdříve nainstalujte gnome-bluetooth:

```
# pacman -S gnome-bluetooth gnome-user-share

```

Spusťte příkaz *bluetooth-applet*. Měla by se vám objevit malá ikonka bluetooth v tray. Kliknutím pravým tlačítkem na ikonu je možné přidávat a spravovat nová zařízení nebo posílat soubory. Pokud chcete, aby se applet spouštěl po přihlášení, přidejte ho do *System -> Preferences -> Startup Applications*.

### bluedevil

Hlavním nástorojem pro správu Bluetooth v KDE4 je program bluedevil. Pro instalaci spusťte:

```
# pacman -S bluedevil

```

Ujistěte se, že vám v pozadí běží daemon pro práci s bluetooth. Po spuštění programu by se měla objevit ikona v Dolphinu a v tray. Odteď pomocí ní můžete konfigurovat bluedevil a spravovat bluetooth zářízení. To můžete také z nastavení systému v KDE.

### Fluxbox, openbox a další

Samozřejmě, že můžete používat předchozí aplikace, i když jako svoje grafické nepoužíváte GNOME, Xfce nebo KDE.

Tento seznam by vám měl pomoci porozumět tomu, co jaká aplikace dělá:

*   bluetooth-applet -- tray ikona s možností nastavení bluetooth, párováním nových zařízení a správou zařízení zpárovaných
*   /usr/lib/gnome-user-share/gnome-user-share -- musí běžet pokud chcete příjímat soubory přes obexBT ze spárovaného zařízení

pokud se v průběhu přenosu ukazuje chyba nebo pokud se žádný soubor nakonec nepřenese, přidejte následující kus kódu do souboru

<tt>/etc/dbus-1/system.d/bluetooth.conf</tt>

```
 <policy user="vase_uzivatelske_id">
   <allow own="org.bluez"/>
   <allow send_destination="org.bluez"/>
   <allow send_interface="org.bluez.Agent"/>
 </policy>

```

*   bluetooth-wizard -- užívá se pro párování nových zařízení
*   bluetooth-properties -- je přístupný i přes ikonu bluetooth-appletu
*   gnome-file-share-properties -- nastavení oprávnění pro příjímání souborů přes bluetooth
*   bluez-sendto -- grafické rozhraní pro posílání souborů vzdáleným bluetooth zařízením

## Manuální konfigurace

Pro manuální konfiguraci bluetooth (<tt>bluez</tt>), budete potřebovat upravit konfigurační soubory v <tt>/etc/bluetooth</tt>. Jedná se o soubory:

```
audio.conf
input.conf
main.conf
network.conf
rfcomm.conf

```

Defaultní konfigurace by měla fungovat bez problémů. Většina výše zmíněných konfiguračních souborů je velice dobře zdokumentovaná, proto by poupravení parametrů neměl být problém. Hlavní nastavení bluetooth je v souboru <tt>main.conf</tt> - tím začněte.

## Párování

**Note:** Toto řešení nemusí být úplně to nejlepší. Vřelé díky Gattschardo za jeho řešení.

Většina bluetooth zařízení vyžaduje [párování](http://en.wikipedia.org/wiki/Bluetooth#Pairing). Způsob párování počítače s mobilním telefonem:

*   Počítač pošle telefonu žádost o připojení.
*   Pin/Klíč, který určí počítač, se musí zadat na telefonu (telefon si ho sám vyžádá)
*   Stejný klíč musí být znovu zadán na počítači

Pro skenování okolních zařízení proveďte příkaz

```
 $ hcitool scan

```

Pro spárování zařízení bez použití grafického rozhraní balíku gnome-bluez budete muset použít nástroj zvaný *bluez-simple-agent*, který je součástí balíku bluez. Dále budete potřebovat několik souvisejících python balíčků - [python2-dbus](https://www.archlinux.org/packages/?name=python2-dbus) a [python2-gobject2](https://www.archlinux.org/packages/?name=python2-gobject2). Pokud máte vše připraveno, můžete spustit program pro párování (musí být spušten pod uživatelem root).

```
 $ bluez-simple-agent

```

Pokud se vše zdařilo, měla by se vám v konzoli zobrazit hlaška "Agent registered". Následně můžete začít párování ze svého mobilního telefonu. Skript se vás v konzoli zeptá na tzv. passcode, vložte ho a potvrďte enterem - voalá, povedlo se. Teď už můžete ukončit agenta použitím klávesy *Ctrl+C* (^C-c). Agenta jsme použili pouze pro párování, nebudeme ho potřebovat při každém připojení zařízení. Pokud váš telefon nemuže naleznout počítač, pokračujte do [řešení problémů](/index.php/Bluetooth_(%C4%8Cesky)#Nelze_nal.C3.A9zt_po.C4.8D.C3.ADta.C4.8D "Bluetooth (Česky)").

Pro příklad spárování přejděte do sekce *příklady*.

## Použití Obex pro posílání a příjímání souborů

Obexfs vám umožňuje připojit váš telefon jako část vašeho filesystému. Pro použití Obexfs budete potřebovat zařízení, které podporuje službu ObexFTP.

Pro instalaci spusťte:

```
# pacman -S obexfs

```

a následně připojte svůj telefon spuštěním (jako root):

```
# obexfs -b <mac_addresa_zarizeni> /mountpoint

```

Pro další možnosti připojení filesystému pomocí ObexFS koukněte [sem](http://dev.zuckschwerdt.org/openobex/wiki/ObexFs).

## Příklady

### Siemens S55

Ukázka připojení telefonu S55.

*   Kroky po instalaci

```
  $> hcitool scan
  Scanning ...
          XX:XX:XX:XX:XX:XX  JMENO_ZARIZENI
  $> B=XX:XX:XX:XX:XX:XX

```

Spustil jsem simple-agent v dalším terminálu

```
  $> su -c bluez-simple-agent 
  Password: 
  Agent registered

```

A následně se vrátil k terminálu prvnímu

```
  $> obexftp -b $B -l "Address book"
  # Telefon se v této části zeptal na pin. Vložil jsem ho a stisknul OK.
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

### Myš Logitech MX Laser / M555b

Pro rychlé otestování připojení:

```
$> hidd --connect XX:XX:XX:XX:XX:XX

```

Pro konfiguraci automatického připojení myši použijte svého desktopového průvodce. Pokud ve vašem prostředí nemáte tuto možnost, koukněte na [Bluetooth_myš](/index.php/Bluetooth_my%C5%A1 "Bluetooth myš").

### Motorola V900

Po instalaci programu blueman a spuštění appletu blueman-applet, klikněte na "find me" pod položkou connections -> bluetooth v zařízení motorola. V programu blueman-applet vyhledejte zařízení, najděte svou motorolu a klikněte na "přidat". Potom kliněte na spárovat a vložte nějaký pin. Až se telefon zeptá, vložte ten samý pin vložte do telefonu motorola. V terminálu:

```
  cd ~/
  mkdir bluetooth-temp
  obexfs -n xx:yy:zz:... ~/bluetooth-temp
  cd ~/bluetooth-temp

```

a můžete brouzdat svým filesystémem na telefonu.

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

**Upozornění: Ujistěte se, že máte zaplé bluetooh a telefon máte ve viditelném módu!**

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
> hcitool JMENO  00:1A:1B:82:9B:6D
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

**Upravte si konfigurační soubor main.conf a vložte novou položku pro váš telefon ( Class = 0x100100 ):**

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

**Párování se dělá pouze jednou programem bluez-simple-agent. Jakmile se vaše motorola zeptá na pin, zadejte 0000.**

```
> /usr/bin/bluez-simple-agent hci0 00:1A:1B:82:9B:6D
RequestPinCode (/org/bluez/10768/hci0/dev_00_1A_1B_82_9B_6D)
Enter PIN Code: 0000
Release
New device (/org/bluez/10768/hci0/dev_00_1A_1B_82_9B_6D)

```

**Teď můžete brouzdat filesystémem ve svém telefonu pomocí programu obexftp:**

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

**Nebo můžete načíst/mountnout svůj telefon do nějakého adresáře na svém počítači a pracovat s ním jako s normálním filesystémem:**

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

### Párování iPhone použitím bluez-simple-agenta

Příklad zařízení pojmenovaného jako hci0 a iPhonu, který byl rozpoznán programem hcitool jako '00:00:DE:AD:BE:EF':

```
   # bluez-simple-agent hci0 00:00:DE:AD:BE:EF
   Passcode:

```

## Řešení problémů

### passkey-agent

```
$> passkey-agent --default 1234
Can't register passkey agent
The name org.bluez was not provided by any .service files

```

Pravděpodobně jste spustili <tt>/etc/rc.d/bluetooth</tt> dříve než <tt>/etc/rc.d/dbus</tt>

```
$> hciconfig dev
# (no listing)

```

Zkuste spustit <tt>hciconfig hc0 up</tt>

### Blueman

Jeslitliže blueman-applet skončí s chybou, zkuste odstranit veškerý obsah adresáře */var/lib/bluetooth* a restartovat systém (nebo pouze daemony hal, dbus a bluetooth).

```
# rm -rf /var/lib/bluetooth
# reboot

```

### gnome-bluetooth

Jesliže se vám ukazuje následující chyba, když příjímate soubory v bluetooth-properties:

```
 Bluetooth OBEX start failed: Invalid path
 Bluetooth FTP start failed: Invalid path

```

Pak spusťte příkazy:

```
 # pacman -S xdg-user-dirs
 $ xdg-user-dirs-update

```

Můžete také upravit cesty použitím:

```
 $ vi ~/.config/user-dirs.dirs

```

### Bluetooth USB klíčenka

Pokud používáte bluetooth USB klíčenku, měli byste zkontrolovat, jestli ji váš systém rozpoznal. To provedete po zapojení klíčenky do USB prozkoumáním logů v `/var/log/messages.log`. Mělo by tam být něco jako toto (Koukejte po hci):

```
# tail -f /var/log/messages.log
May  2 23:36:40 tatooine usb 4-1: new full speed USB device using uhci_hcd and address 9
May  2 23:36:40 tatooine usb 4-1: configuration #1 chosen from 1 choice
May  2 23:36:41 tatooine hcid[8109]: HCI dev 0 registered
May  2 23:36:41 tatooine hcid[8109]: HCI dev 0 up
May  2 23:36:41 tatooine hcid[8109]: Device hci0 has been added
May  2 23:36:41 tatooine hcid[8109]: Starting security manager 0
May  2 23:36:41 tatooine hcid[8109]: Device hci0 has been activated

```

Pro seznam podporovaného hardware pokračujte do sekce [zdroje](/index.php/Bluetooth_(%C4%8Cesky)#Zdroje "Bluetooth (Česky)") na této stránce. Pokud vidíte pouze dvě první řádky logu výše, znamená to, že zařízení bylo nalezeno, ale musí se ješte zapnout. Příklad:

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

Pro kontrolu, jestli bylo zařízení detekováno použijte nástroj `hcitool`, který je součástí balíku [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils). Následujícím příkazem dostanete seznam dostupných zařízení, identifikátorů a jejich MAC adres.

```
$ hcitool dev
Devices:
        hci0	00:1B:DC:0F:DB:40

```

Pokud byste si přáli zobrazit o zařízení více informací, můžete použít `hciconfig`.

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

### hcitool scan: Device not found

*   Na některých počítačích Dell (e.g. Studio 15) musíte přepnout mód Bluetooth z HID na HCI použitím

```
# hid2hci

```

*   Občas může pomoci i tento jednoduchý příkaz:

```
# hciconfig hci0 up

```

### Nelze nalézt počítač

Stále váš telefon nechce nálezt zařízení počítače? Zapněte PSCAN a ISCAN:

```
# zapnutí PSCAN a ISCAN
$ hciconfig hci0 piscan 
# mrkněte, jestli se nastavení změnilo
$ hciconfig 
hci0:   Type: USB
        BD Address: 00:12:34:56:78:9A ACL MTU: 192:8 SCO MTU: 64:8
        **UP RUNNING PSCAN ISCAN**
        RX bytes:20425 acl:115 sco:0 events:526 errors:0
        TX bytes:5543 acl:84 sco:0 commands:340 errors:0

```

**Note:** Zkontrolujte volbu DiscoverableTimeout a PairableTimeout v souboru /etc/bluetooth/main.conf

Nebo můžete zkusit změnit nastavení *Class* v souboru `/etc/bluetooth/main.conf` následovně

```
# Default device class. Only the major and minor device class bits are
# considered.
#Class = 0x000100 (from default config)
Class = 0x100100

```

### Nautilus nemůže procházet soubory

Pokud se nautilus neotevře a ukáže tuto chybu:

```
Nautilus cannot handle obex: locations. Couldn't display "obex://[XX:XX:XX:XX:XX:XX]/".

```

Nainstalujte balík gvfs-obexftp:

```
# pacman -S gvfs-obexftp

```

## Zdroje

*   [Official Linux Bluetooth protocol stack](http://www.bluez.org)
*   [openSUSE Bluetooth Hardware Compatibility List (HCL)](http://en.opensuse.org/HCL/Bluetooth_Adapters)
*   [Gentoo wiki is usually good](http://www.gentoo.org/doc/en/bluetooth-guide.xml)
*   [Accessing a Bluetooth phone on Linux Gazette](http://linuxgazette.net/109/oregan3.html)
*   [Bluetooth computer visibility](http://www.adamish.com/blog/#a000361)