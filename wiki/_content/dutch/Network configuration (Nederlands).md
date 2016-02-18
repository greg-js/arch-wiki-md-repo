## Contents

*   [1 Apparaatmodules laden](#Apparaatmodules_laden)
*   [2 IP-adres configureren](#IP-adres_configureren)
    *   [2.1 DHCP](#DHCP)
    *   [2.2 Statisch](#Statisch)
*   [3 Alternatieven](#Alternatieven)
*   [4 Computernaam instellen](#Computernaam_instellen)
*   [5 Hostnaam/IP instellen](#Hostnaam.2FIP_instellen)
*   [6 Configuratie laden](#Configuratie_laden)
*   [7 Nog meer instellingen](#Nog_meer_instellingen)
    *   [7.1 Draadloos netwerk configureren](#Draadloos_netwerk_configureren)
    *   [7.2 Firewall](#Firewall)
    *   [7.3 Ifplugd](#Ifplugd)
    *   [7.4 Koppelen van netwerkkaarten](#Koppelen_van_netwerkkaarten)
    *   [7.5 Meerdere IP-adressen op meerdere netwerkkaarten](#Meerdere_IP-adressen_op_meerdere_netwerkkaarten)
*   [8 Problemen oplossen](#Problemen_oplossen)
    *   [8.1 Wisselen van computers op een kabelmodem](#Wisselen_van_computers_op_een_kabelmodem)
    *   [8.2 Het TCP Window Scaling probleem](#Het_TCP_Window_Scaling_probleem)
        *   [8.2.1 Hoe een probleem te constateren?](#Hoe_een_probleem_te_constateren.3F)
        *   [8.2.2 Hoe een probleem op te lossen? (De slechte manier)](#Hoe_een_probleem_op_te_lossen.3F_.28De_slechte_manier.29)
        *   [8.2.3 Hoe een probleem op te lossen? (De goede manier)](#Hoe_een_probleem_op_te_lossen.3F_.28De_goede_manier.29)
        *   [8.2.4 Hoe een probleem op te lossen? (De beste manier)](#Hoe_een_probleem_op_te_lossen.3F_.28De_beste_manier.29)
        *   [8.2.5 Meer informatie?](#Meer_informatie.3F)
    *   [8.3 Realtek geen link / WOL problemen](#Realtek_geen_link_.2F_WOL_problemen)
        *   [8.3.1 Methode 1 - Windows driver terugrollen of veranderen](#Methode_1_-_Windows_driver_terugrollen_of_veranderen)
        *   [8.3.2 Methode 2 - WOL activeren in Windows driver](#Methode_2_-_WOL_activeren_in_Windows_driver)
        *   [8.3.3 Methode 3 - Nieuwere Realtek Linux driver](#Methode_3_-_Nieuwere_Realtek_Linux_driver)
        *   [8.3.4 Methode 4 - *LAN Boot ROM* activeren in BIOS/CMOS](#Methode_4_-_LAN_Boot_ROM_activeren_in_BIOS.2FCMOS)
    *   [8.4 DLink G604T/DLink G502T DNS probleem](#DLink_G604T.2FDLink_G502T_DNS_probleem)
        *   [8.4.1 Hoe het probleem te constateren?](#Hoe_het_probleem_te_constateren.3F)
        *   [8.4.2 Hoe het probleem op te lossen?](#Hoe_het_probleem_op_te_lossen.3F)
        *   [8.4.3 Meer informatie?](#Meer_informatie.3F_2)

## Apparaatmodules laden

Udev zou de modules voor je netwerkkaart automatisch moeten detecteren en laden tijdens het opstarten. Indien dit niet het geval is, moet je weten welke module jou netwerkkaart nodig heeft:

```
hwdetect --show-net

```

Als je nu weet welke module nodig hebt voor je netwerkkaart, kun je die laden met:

```
# modprobe <modulename>

```

Als udev de juiste module niet automatisch detecteert en laad, dan kun je de module toevoegen aan de **MODULES=** array in `/etc/rc.conf`, zodat je de module niet elke keer hoeft te modproben na het opstarten. Bijvoorbeeld, als tg3 de netwerkmodule is:

```
MODULES=(!usbserial tg3 snd-cmipci)

```

Andere veel voorkomende modules zijn 8139too voor netwerkkaarten met de Realtek chipset, of sis900 voor SiS netwerkkaarten.

## IP-adres configureren

### DHCP

Om DHCP te gebruiken, heb je het dhcpcd pakket nodig (al geinstalleerd op de meeste installaties). Wijzig `/etc/rc.conf` zoals hier:

```
eth0="dhcp"
INTERFACES=(eth0)
ROUTES=(!gateway)

```

Als je DHCP gebruikt en je jou DNS servers **niet** elke keer automatisch toegewezen wilt krijgen als je je netwerk start, verzeker jezelf er dan van dat je de "-C" parameter gebruikt in **DHCPCD_ARGS** in `/etc/conf.d/dhcpcd` (wordt gebruikt door `/etc/rc.d/network`). Dit weerhoudt dhcpcd ervan om de inhoud van `/etc/resolv.conf` elke keer te overschrijven:

```
DHCPCD_ARGS="**-C resolv.conf** -q"

```

Let op: in vorige dhcpcd versies werdt de nu achterhaalde **-R** parameter nog gebruikt:

```
DHCPCD_ARGS="-R -t 30 -h $HOSTNAME"

```

Verzeker jezelf er ook van dat je (een) geldige nameserver(s) aan `/etc/resolv.conf` toevoegt. Een voorbeeld van een `/etc/resolv.conf`:

```
#DHCP met door de gebruiker gedefinieerde DNS servers
nameserver 4.2.2.2
nameserver 4.2.2.4

```

**LET OP**

De nieuwe dhcpcd (>= 4.0.2) werkt niet langer met de **-R** parameter, aangezien deze parameter achterhaald is (werkt alleen nog als dhcpcd wordt gecompileerd in compatibility mode). In plaats hiervan moet je je eigen DNS servers in het bestand `/etc/resolv.conf.head` plaatsen. dhcpcd zal dit bestand dan toevoegen bovenin de normale `/etc/resolv.conf`.

Als laatste, als je niet wilt rebooten, test dan je nieuwe instellingen door de `/etc/rc.d/network` daemon te stoppen en starten, in plaats van het down en weer up brengen van je netwerk interface en het handmatig starten van dhcp. Om de network daemon te herstarten:

```
/etc/rc.d/network restart

```

**LET OP** Je zou het openresolv pakket (van AUR) kunnen gebruiken, als meerdere softwarepakketten proberen om resolv.conf te veranderen (bijvoorbeeld dhcpcd en een VPN client). Er is geen verdere configuratie nodig voor dhcpcd als je openresolv gebruikt.

### Statisch

Als je je internetverbinding deelt vanaf een Windows machine zonder gebruik van een router, wees er dan zeker van dat je een statisch IP-adres gebruikt op beide computers. Ander zul je waarschijnlijk LAN problemen hebben.

Je hebt nodig:

*   Je statische IP-adres
*   Het netmask
*   Het broadcast address
*   Je gateway
*   Het IP-adres van je nameserver
*   Je domeinnaam

Als je een privè-netwerk draait, is het veilig om IP-adressen in het 192.168.*.* bereik te gebruiken, met een netmask van 255.255.0.0 en broadcast addres 192.168.255.255\. Tenzij je netwerk een router heeft, maakt het gateway adres niets uit. Wijzig `/etc/rc.conf` zoals dit, waarbij je je eigen waardes invult voor het IP-adres, netmask, broadcast adres en gateway:

```
eth0="eth0 82.137.129.59 netmask 255.255.255.0 broadcast 82.137.129.255"
INTERFACES=(eth0)
gateway="default gw 82.137.129.1"
ROUTES=(gateway)

```

En je `/etc/resolv.conf` zoals dit, waarbij je je eigen waardes invult voor je nameserver's IP-adres en je domeinnaam:

```
nameserver 61.23.173.5
nameserver 61.95.849.8
search example.com

```

Je mag zoveel nameserver regels toevoegen als je wilt.

## Alternatieven

Als om onduidelijke redenen dhcpcd eth0 mislukt, installeer dan dhclient (pacman -S dhclient) en gebruik `dhclient eth0` in de plaats van `dhcpcd eth0`.

## Computernaam instellen

Verander `/etc/rc.conf` en zet in **HOSTNAME** je gewenste computernaam:

```
HOSTNAME="banana"

```

## Hostnaam/IP instellen

Wijzig `/etc/hosts` en voeg dezelfde HOSTNAME toe, die je in `/etc/rc.conf` hebt neergezet:

```
127.0.0.1      banana.domain.org   localhost.localdomain      localhost    banana

```

Dit formaat, inclusief de localhost regel, is vereist voor compatibiliteit met sommige programma's.

## Configuratie laden

Om je instellingen te testen kun je je computer herstarten, of als root `/etc/rc.d/network restart` uitvoeren. Probeer vervolgens om je gateway, DNS server, ISP provider en andere websites te pingen, om er zeker van te zijn dat je internetverbinding goed functioneert.

## Nog meer instellingen

### Draadloos netwerk configureren

Zie [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") voor meer informatie.

### Firewall

Je kunt een [firewall](/index.php/Firewalls "Firewalls") installeren en configureren, om je zekerder te voelen. ;-)

### Ifplugd

Je kunt een daemon installeren, die je netwerkkaart automatisch configureert als er een kabel ingeplugt is en die je netwerkkaart automatisch deconfigureert als de kabel eruit getrokken wordt. Dit is handig op laptops met onboard netwerkkaarten, omdat het alleen je netwerkkaart configureert als er daadwerkelijk een kabel ingeplugt is. Ook is het handig als je alleen je netwerk wilt herstarten, maar niet door je computer te herstarten of de shell te gebruiken; je trekt de kabel eruit en plugt de kabel er vervolgens weer in, ifplugd doet de rest.

De installatie van ifplugd is erg makkelijk, omdat het in [extra] zit:

```
# pacman -S ifplugd

```

Standaard is ifplugd geconfigureerd om voor de netwerkkaart eth0 te werken. Deze instellen, alsmede andere instellingen als vertragingen, kunnen worden geconfigureeerd in `/etc/ifplugd/ifplugd.conf`.

Start ifplugd met:

```
# /etc/rc.d/ifplugd start

```

Of voeg ifplugd toe aan de **DAEMONS=** array in `/etc/rc.conf`.

### Koppelen van netwerkkaarten

Je kunt **ifenslave** installeren om twee echte netwerkkaarten te koppelen met één IP-adres. /etc/conf.d/bonding

```
bond_bond0="eth0 eth1"
BOND_INTERFACES=(bond0)

```

/etc/modprobe.d/modprobe.conf:

```
options bonding miimon=100

```

/etc/rc.conf

```
MODULES=(... bonding ...)
bond0="bond0 192.168.1.1 netmask 255.255.255.0 broadcast 192.168.1.255"
INTERFACES=(bond0)

```

Herstart het netwerk met:

```
/etc/rc.d/network restart

```

### Meerdere IP-adressen op meerdere netwerkkaarten

Eén IP-adres op één kaart:

```
vi /etc/rc.conf
 eth0="eth0 192.168.0.1 netmask 255.255.255.0 broadcast 192.168.0.255"
 INTERFACES=(lo eth0)

```

Twee IP-adressen op één kaart (BUG:/etc/rc.d/network stop)

```
vi /etc/rc.conf
 eth0="eth0 192.168.0.1 netmask 255.255.255.0 broadcast 192.168.0.255"
 eth0_0="eth0:0 192.168.0.2 netmask 255.255.255.0 broadcast 192.168.0.255"
 INTERFACES=(lo eth0 eth0_0)

```

Eén IP-adres op twee kaarten:

```
pacman -S ifenslave
vi /etc/rc.conf
 bond0="bond0 192.168.0.1 netmask 255.255.255.0 broadcast 192.168.0.255"
 INTERFACES=(lo bond0)
 MODULES=(... bonding ...)

```

Twee IP-adressen op twee kaarten (BUG:/etc/rc.d/network stop):

```
pacman -S ifenslave
vi /etc/rc.conf
 bond0="bond0 192.168.0.1 netmask 255.255.255.0 broadcast 192.168.0.255"
 bond01="bond0:1 192.168.0.2 netmask 255.255.255.0 broadcast 192.168.0.255"
 INTERFACES=(lo bond0 bond01)
 MODULES=(... bonding ...)

```

**Note:** Nadat je dit soort opties hebt geconfigureerd (koppelen, etcetera), zou het kunnen dat je je firewall instellingen moet veranderen om het netwerk goed te laten werken.

## Problemen oplossen

### Wisselen van computers op een kabelmodem

De meeste huishouden-gerichte internetproviders (waaronder videotron en @home) maken gebruik van een kabelmodem dat geconfigureerd is, om slechts één PC te herkennen, door het MAC-adres van de netwerkkaart van die computer te onthouden. Zodra het kabelmodem het MAC-adres van de computer heeft geleerd, waarmee het het eerste heeft gecommuniceerd, zal het niet meer willen communiceren met andere MAC-adressen (lees: andere computers/netwerkkaarten). Als je dus een PC (of router) vervangt door een andere PC of router, dan zal de nieuwe PC of router niet worden herkend door het kabelmodem. Om het kabelmodem te resetten, moet je eerst de PC en het kabelmodem uitschakelen, dan het kabelmodem inschakelen en wachten tot het weer helemaal opgestart en online gegaan is. Start dan de nieuwe PC of router op, zodat het een DHCP aanvraag doet. Het kabelmodem zal dan de nieuwe PC of router herkennen.

### Het TCP Window Scaling probleem

TCP pakketten bevatten een "window" waarde in hun headers, dat aangeeft hoeveel gegevens de andere host mag terugsturen. Deze waarde wordt vertegenwoordigd met slechts 16 bits, waardoor de window grootte maximaal 64Kb kan zijn. TCP pakketten worden tijdelijk gecached (omdat ze gesorteerd moeten worden), en omdat het beschikbare geheugen daarvoor gelimiteerd is, zou het kunnen voorkomen dat een host een tekort aan geheugen krijgt.

Rond 1992, toen er steeds meer geheugen beschikbaar kwam, was [RFC 1323](http://www.faqs.org/rfcs/rfc1323.html) geschreven, om de situatie te verbeteren: Window Scaling. De "window" waarde, die in alle pakketten aanwezig is, zou eenmalig worden gewijzigd door een "Scale Factor" (schaal factor), helemaal aan het begin van de connectie.

Deze 8-bit Scale Factor staat een window toe om tot 32 keer groter te worden als de initiële 64Kb.

Het lijkt erop dat sommige niet goed functionerende routers en firewalls op het internet de Scale Factor herschrijven naar 0, waardoor er communicatieproblemen tussen hosts ontstaat.

Versie 2.6.17 van de Linux kernel introduceerde een nieuw berekeningsschema, die hogere Scale Factors genereert, waardoor de effecten van de niet goed functionerende routers en firewalls beter zichtbaar zijn. De resulterende verbinding is op zijn best erg traag of helemaal niet aanwezig.

#### Hoe een probleem te constateren?

Als eerste is het belangrijk om duidelijk te maken dat de symptomen van dit probleem erg onvoorspelbaar zijn. In sommige gevallen zul je geen TCP connecties kunnen gebruiken (HTTP, FTP, ...) en in sommige andere gevallen zul je slechts met een beperkt aantal hosts kunnen communiceren.

**Waarschuwing**: `dmesg`'s uitvoer is OK, de logbestanden zijn schoon en de uitvoer van `ifconfig` geeft een normale status terug; het lijkt erop dat alles OK is.

Als je naar geen enkele websit kunt browsen, maar slechts een paar hosts kunt pingen, dan is de kans groot dat je dit probleem hebt: ping maakt gebruik van het ICMP protocol en wordt niet beinvloed door de TCP problemen.

Je kunt proberen om WireShark te gebruiken. Je zult mischien een aantal succesvolle UDP en ICMP communicaties zien, maar onsuccesvolle TCP communicaties zien (naar vreemde hosts).

#### Hoe een probleem op te lossen? (De slechte manier)

Om het probleem op de slechte manier op te lossen, kun je de tcp_rmem waarde veranderen, waarop de Scale Factor is gebaseerd. Alhoewel deze oplossing zou moeten werken voor de meeste hosts, is het niet gegarandeerd, in het bijzonder voor hosts die ver weg zijn.

```
echo "4096 87380 174760" > /proc/sys/net/ipv4/tcp_rmem

```

#### Hoe een probleem op te lossen? (De goede manier)

De goede manier is om window scaling te deactiveren. Zelfs al is window scaling een leuke TCP feature, het kan oncomfortabel zijn als je de defecte routers en firewalls in de verbinding niet kan repareren. Er zijn meerdere manieren om window scaling te deactiveren, en het lijkt erop dat de beste methode is, om de volgende regels aan je `/etc/rc.local` toe te voegen:

```
echo 0 > /proc/sys/net/ipv4/tcp_window_scaling

```

#### Hoe een probleem op te lossen? (De beste manier)

Het probleem wordt veroorzaakt door niet goed functionerende routers en firewalls, dus die zouden gerepareerd of vervangen moeten worden. Sommige gebruikers hebben gemeld, dat de niet goed functionerende router of firewall hun eigen DSL router was.

#### Meer informatie?

Dit onderdeel is gebaseerd op het LWN artikel [TCP window scaling and broken routers](http://lwn.net/Articles/92727/) en een artikel van Kernel Trap: [Window Scaling on the Internet](http://kerneltrap.org/node/6723).

Recentelijk zijn een aantal Arch Linux gebruikers getroffen door dit probleem:

*   [Odd network issue](https://www.archlinux.org/pipermail/arch/2006-June/011250.html)
*   [Kernel 2.6.17 and TCP window scaling](https://www.archlinux.org/pipermail/arch/2006-September/011943.html) — het topic dat dit artikel begon

Er zijn ook diverse relevante threads op LKML te vinden.

### Realtek geen link / WOL problemen

Gebruikers met netwerkkaarten die gebaseerd zijn op Realtek 8168 8169 8101 8111(C) chips, kunnen een probleem constateren, waarbij de netwerkkaart lijkt te zijn gedeactiveert bij het opstarten en geen Link lampje laat branden. Dit probleem komt vaak voor op dualboot systemen met Windows geinstalleerd. Het lijkt erop dat het gebruik van de officiële Realtek drivers (alle drivers van na mei 2007) de oorzaak is. Deze nieuwe drivers deactiveren de Wake-On-LAN functionaliteit, door de netwerkkaart te deactiveren als Windows afsluit, waarbij de netwerkkaart blijft gedeactiveert tot Windows weer opnieuw opstart. Bij het afsluiten van Windows zal het Link lampje uit gaan; de normale situatie is dat het Link lampje altijd aan is, zelfs bij POST (Power On Self Test). Dit probleem beinvloed ook andere besturingssystemen zonder nieuwere drivers (waaronder Linux/BSD Live CD's). Hier zijn een aantal oplossingen voor het probleem:

#### Methode 1 - Windows driver terugrollen of veranderen

Je kunt je Windows netwerkkaartdriver terugrollen naar de door Microsoft aangeleverde driver (indien beschikbaar), of een officiële Realtek driver van voor mei 2007 installeren (bijvoorbeeld van de cd die bij je netwerkkaart kwam).

#### Methode 2 - WOL activeren in Windows driver

Waarschijnlijk is de beste en snelste manier, om de gewraakte instelling in de Windows driver te veranderen. Op deze manier zou het probleem op het gehele systeem opgelost moeten zijn (en niet alleen onder Arch Linux). Zoek in Windows, onder Apparaatbeheer, naar je Realtek netwerkkaart en dubbelklik erop. Onder het tabblad geadvanceerd moet je de optie "Wake-on-LAN after shutdown" op Enable of Activeren zetten.

```
 In Windows XP (example)
 Right click my computer
 --> Hardware tab
   --> Device Manager
     --> Network Adapters
       --> "double click" Realtek ...
         --> Advanced tab
           --> Wake-On-Lan After Shutdown
             --> Enable

```

*   **Let op**: nieuwere Realtek Windows drivers (getest met *Realtek 8111/8169 LAN Driver v5.708.1030.2008*, dated 2009/01/22, available from GIGABYTE) kunnen iets anders naar deze optie verwijzen, bijvoorbeeld *Shutdown Wake-On-LAN --> Enable*. Een workaround is om Windows te booten en het systeem eenvoudigweg te resetten (zonder gebruik te maken van afsluiten of herstarten), waardoor de Windows driver niet de kans krijgt om de Link te deactiveren. Het Link lampje zal geactiveerd blijven en de netwerkkaart zal toegankelijk blijven na POST - zolang je Windows niet opstart en op de normale manier afsluit.

#### Methode 3 - Nieuwere Realtek Linux driver

Op de Realtek website zijn er nieuwere drivers voor de Realtek kaarten te vinden. Deze drivers zijn nog niet getest, maar het wordt aangenomen dat deze nieuwe drivers de problemen oplossen.

#### Methode 4 - *LAN Boot ROM* activeren in BIOS/CMOS

Het lijkt erop dat het instellen van *Integrated Peripherals --> Onboard LAN Boot ROM --> Enabled* in het BIOS/CMOS de Realtek LAN chip activeert bij het POSTen van het systeem, ondanks het deactiveren van de kaart door de Windows driver tijdens het afsluiten.

<small>Dit is meerdere malen succesvol getest met een GIGABYTE system board GA-G31M-ES2L met BIOS versie F8 vrijgegeven op 2009/02/05\. YMMV.</small>

### DLink G604T/DLink G502T DNS probleem

Gebruikers met een DLink G604T/DLink G502T router, die DHCP gebruiken en een firmware versie v2.00+ hebben (over het algemeen gebruikers met AUS firmware), kunnen problemen ervaren met bepaalde programma's die geen DNS resolven. Eén van deze programma's is helaas pacman. Het probleem is dat de router in bepaalde situaties de DNS gegevens niet juist via DHCP verstuurd, waardoor de programma's opnieuw proberen verbinding te maken met servers met een IP-adres 1.0.0.0 en uiteindelijk stoppen met een "connection timed out" foutmelding.

#### Hoe het probleem te constateren?

De beste manier om het probleem te constateren, is om een webbrowser te gebruiken en om wget voor pacman te activeren. Als je op een verse installatie van Arch Linux werkt, dan zou je kunnen overwegen om **links** te installen via de live CD.

Als eerste, activeer wget voor pacman (omdat het informatie geeft over pacman als het pakketten download) Open /etc/pacman.conf met je favoriete teksteditor en uncomment de volgende regel (verwijder het hekje (#) als het aanwezig is)

```
XferCommand = /usr/bin/wget --passive-ftp -c -O %o %u

```

Terwijl je in pacman.conf bent, noteer dan de standaard spiegelserver, die pacman gebruikt om pakketten te downloaden.

Open nu de standaard spiegelserver in een webbrowser, om te controleren of de spiegelserver werkt. Als het werkt, probeer dan een **pacman -Syy**. Als de spiegelserver niet werkt in je browser, kies dan een andere werkende spiegelserver en maak dat de standaard spiegelserver voor pacman. Als je iets krijgt wat lijkt op het volgende (let op de 1.0.0.0):

```
ftp://mirror.pacific.net.au/linux/archlinux/extra/os/i686/extra.db.tar.gz                                                            
           => `/var/lib/pacman/community.db.tar.gz.part'                            
Resolving mirror.pacific.net.au... 1.0.0.0

```

Dan heb je hoogstwaarschijnlijk last van het probleem. De 1.0.0.0 betekent dat het niet in staat is om de DNS te resolven, dus moeten we de DNS handmatig toevoegen aan resolv.conf.

#### Hoe het probleem op te lossen?

Het oplossen van het probleem komt erop neer dat je handmatig de DNS server aan je /etc/resolv.conf bestand moet toevoegen. Het probleem is dat DHCP automatisch de inhoud van resolv.conf verwijdert, als er een nieuwe DHCP lease wordt aangevraagd, dus we moeten `/etc/conf.d/dhcpcd` wijzigen en een parameter veranderen, om ervoor te zorgen dat dhcpcd dit niet meer doet:

Als je `/etc/conf.d/dhcpcd` opent, zou je iets moeten zien dat lijkt op het volgende:

```
DHCPCD_ARGS="-t 30 -h $HOSTNAME"

```

Voeg de -R parameter toe aan het argument:

```
DHCPCD_ARGS="-R -t 30 -h $HOSTNAME"

```

**LET OP**: Als je een dhcpcd >= 4.0.2 gebruikt, dan is de -R parameter achterhaald. Kijk dan even in de TODO sectie van deze pagina om te zien hoe je een aangepaste resolv.conf kunt gebruiken.

Bewaar en sluit het bestand en open vervolgens `/etc/resolv.conf`. Je zou slects één namespace moeten zien (hoogstwaarschijnlijk 10.1.1.1), namelijk de gateway naar je router, waar we verbinding mee moeten maken, om de DNS van je internetprovider te krijgen. Plak het IP-adres in je browser en log in op je router. Ga naar het DNS-gedeelte, waar je een IP-adres zou moeten zien in het "Preferred DNS Server" gedeelte (Voorkeurs DNS server). Kopier het IP-adres en plak het in resolv.conf als een namespace, boven het huidige gateway adres:

De bestaande resolv.conf zou er ongeveer zo uit moeten zien:

```
namespace 10.1.1.1

```

Als je Primary DNS Server 211.29.132.12 is, verander dan resolv.conf naar:

```
namespace 211.29.132.12
namespace 10.1.1.1

```

Herstart nu je network daemon met `/etc/rc.d/network restart` en voer een **pacman -Syy** uit. Als pacman synchroniseert met de spiegelserver, dan is het probleem opgelost.

#### Meer informatie?

Een linkje naar het whirpool forum (Australische internetprovider gemeenschap), waar gesproken wordt over het probleem en de oplossing:

```
[http://forums.whirlpool.net.au/forum-replies-archive.cfm/461625.html](http://forums.whirlpool.net.au/forum-replies-archive.cfm/461625.html)

```