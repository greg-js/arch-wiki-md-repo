Related articles

*   [Jumbo frames](/index.php/Jumbo_frames "Jumbo frames")
*   [Firewalls](/index.php/Firewalls "Firewalls")
*   [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")
*   [network bridge](/index.php/Network_bridge "Network bridge")
*   [List of applications/Internet#network managers](/index.php/List_of_applications/Internet#network_managers "List of applications/Internet")
*   [network Debugging](/index.php/Network_Debugging "Network Debugging")

Op deze pagina woordt de installatie van een **bedrade** netwerkaansluiting uitgelegd. Voor configuratie van een **wireless** aansluiting, zie de [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") engelstalige pagina.

## Contents

*   [1 Controleer de kabelaansluiting](#Controleer_de_kabelaansluiting)
*   [2 Device driver](#Device_driver)
    *   [2.1 Controleer de status](#Controleer_de_status)
    *   [2.2 Laadt de module](#Laadt_de_module)
*   [3 Netwerk management](#Netwerk_management)
    *   [3.1 Device namen](#Device_namen)
        *   [3.1.1 Toon de de huidige benaming](#Toon_de_de_huidige_benaming)
        *   [3.1.2 Activeren en De-actieveren van netwerk interfaces](#Activeren_en_De-actieveren_van_netwerk_interfaces)
    *   [3.2 Dynamisch IP adres](#Dynamisch_IP_adres)
    *   [3.3 Statisch IP adres](#Statisch_IP_adres)
        *   [3.3.1 Handmatige toewijzing statisch adres](#Handmatige_toewijzing_statisch_adres)
        *   [3.3.2 Bereken adressen](#Bereken_adressen)
    *   [3.4 netwerk managers](#netwerk_managers)
*   [4 Bepaal de hostnaam](#Bepaal_de_hostnaam)
    *   [4.1 Lokaal netwerk hostnaam resolutie](#Lokaal_netwerk_hostnaam_resolutie)
*   [5 Tips en tricks](#Tips_en_tricks)
    *   [5.1 Device naam wijzigen](#Device_naam_wijzigen)
    *   [5.2 Terug naar de traditionele device namen](#Terug_naar_de_traditionele_device_namen)
    *   [5.3 Instellen van device MTU en queue lengte](#Instellen_van_device_MTU_en_queue_lengte)
    *   [5.4 ifplugd voor laptops](#ifplugd_voor_laptops)
    *   [5.5 Bonding of LAG](#Bonding_of_LAG)
    *   [5.6 IP adres aliasing](#IP_adres_aliasing)
        *   [5.6.1 Voorbeeld](#Voorbeeld)
    *   [5.7 MAC/hardware adres wijzigen](#MAC.2Fhardware_adres_wijzigen)
    *   [5.8 Internet delen](#Internet_delen)
    *   [5.9 Router configuratie](#Router_configuratie)
    *   [5.10 Promiscuous (willekeurig) mode](#Promiscuous_.28willekeurig.29_mode)
*   [6 Foutopsporing](#Foutopsporing)
    *   [6.1 Swapping computers on the cable modem](#Swapping_computers_on_the_cable_modem)
    *   [6.2 Het TCP window scaling probleem](#Het_TCP_window_scaling_probleem)
        *   [6.2.1 How to diagnose the problem](#How_to_diagnose_the_problem)
        *   [6.2.2 Hoe te herstellen](#Hoe_te_herstellen)
            *   [6.2.2.1 Fout](#Fout)
            *   [6.2.2.2 Goed](#Goed)
            *   [6.2.2.3 Best](#Best)
        *   [6.2.3 Aanvullend](#Aanvullend)
    *   [6.3 Realtek geen link / WOL probleem](#Realtek_geen_link_.2F_WOL_probleem)
        *   [6.3.1 Activeren van de NIC in Linux](#Activeren_van_de_NIC_in_Linux)
        *   [6.3.2 Rollback/wijzig de Windows driver](#Rollback.2Fwijzig_de_Windows_driver)
        *   [6.3.3 Activeer WOL in Windows driver](#Activeer_WOL_in_Windows_driver)
        *   [6.3.4 Nieuwe Realtek Linux driver](#Nieuwe_Realtek_Linux_driver)
        *   [6.3.5 Inschakelen *LAN Boot ROM* in BIOS/CMOS](#Inschakelen_LAN_Boot_ROM_in_BIOS.2FCMOS)
    *   [6.4 No interface with Atheros chipsets](#No_interface_with_Atheros_chipsets)
    *   [6.5 Broadcom BCM57780](#Broadcom_BCM57780)
    *   [6.6 Realtek RTL8111/8168B](#Realtek_RTL8111.2F8168B)
    *   [6.7 Gigabyte Motherboard with Realtek 8111/8168/8411](#Gigabyte_Motherboard_with_Realtek_8111.2F8168.2F8411)
*   [7 Zie ook](#Zie_ook)

## Controleer de kabelaansluiting

Deze basis installatie / configuratie gaat uit van een werkende netwerkaansluiting. Gebruik [ping(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ping.8) om de werking te controleren:

 `$ ping www.google.com` 
```
PING www.l.google.com (74.125.132.105) 56(84) bytes of data.
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=1 ttl=50 time=17.0 ms
...
```

Wanneer de ping successvol is (zie het 64 bytes bericht hierboven), dan is het netwerk al geconfigureerd. Druk op `Control-C` om de ping sessie te stoppen.

Echter, indien de ping faalt met een *Unknown hosts* fout, blijkt je computer niet in staat is om de gebruite domeinnaam te vinden. Dit kan geweten worden aan de internet service provider of aan je eigen router/gateway. Probeer eerst eens om een statisch adres te pingen om te bepalen of er toch aansluiting is op het Internet:

 `$ ping 8.8.8.8` 
```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_req=1 ttl=53 time=52.9 ms
...

```

Indien `8.8.8.8` **gepingd** kan worden, maar niet b.v. `www.google.com`, controleer dan de DNS configuratie. Zie [resolv.conf](/index.php/Resolv.conf "Resolv.conf") voor details. De `hosts` regel in `/etc/nsswitch.conf` is ook een optie welke gecontroleerd kan worden.

Indien geen baat, controleer de netwerkkabel op defecten.

**Note:**

*   Een foutmelding als `ping: icmp open socket: Operation not permitted` bij een *ping*, herinstalleer het [iputils](https://www.archlinux.org/packages/?name=iputils) pakket.
*   De `-c *num*` optie kan gebruikt worden voor exacte `*num*` pings, anders kan de ping oneindig doorlopen en zal dan handmatig beeindigd moeten worden. Zie [ping(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ping.8) voor meer informatie.
*   `8.8.8.8` is een statisch adres dat makkelijk te onthouden is. Het betreft hier Google's primary DNS server adres, en kan als betrouwbaar beschouwd worden omdat het gewoonlijk niet geblokkeerd wordt door contentfilters en proxy servers.

## Device driver

### Controleer de status

[udev](/index.php/Udev "Udev") zou de [netwerk interface controller](https://en.wikipedia.org/wiki/netwerk_interface_controller "wikipedia:netwerk interface controller") moeten vinden en bij het opstarten de noodzakelijke module laden. Controleer de "Ethernet controller" regel bij de `lspci -v` output. Als het goed zal kenbaar zijn welke kernelmodule de driver voor de netwerk adapter aanbied. Bijvoorbeeld:

 `$ lspci -v` 
```
02:00.0 Ethernet controller: Attansic Technology Corp. L1 Gigabit Ethernet Adapter (rev b0)
 	...
 	Kernel driver in use: atl1
 	Kernel modules: atl1

```

Controleer nu dat de driver daadwerkelijk geladen is via `dmesg | grep *module_name*`. Bijvoorbeeld:

 `$ dmesg | grep atl1` 
```
...
atl1 0000:02:00.0: eth0 link is up 100 Mbps full duplex

```

Als de driver geladen is, sla dan de volgende sectie over. Zo niet, dan moet achterhaald worden welke module vereist is voor dit model netwerkkaart.

### Laadt de module

Zoek op het Internet naar de benodigde module/driver voor de gebruikte chipset. Algemene modules zijn `8139too` voor kaarten met een Realtek chipset, of `sis900` waneer een SiS chipset gebruikt wordt. Als bekend is welke chipset gebruikt is, probeer de module dan [zelf te laden](/index.php/Kernel_modules#Manual_module_handling "Kernel modules"). Mocht er een foutmelding optreden omdat de module niet gevonden is, dan zou het zomaar kunnen dat deze module niet inbegrepen is in de Arch kernel. Eventueel kan in de [AUR](/index.php/AUR "AUR") kan nog gezocht worden op modulenaam.

Indien udev tijdens het opstarten de juiste module niet detecteert en/of laadt, zie dan [Kernel modules#Automatic module handling](/index.php/Kernel_modules#Automatic_module_handling "Kernel modules").

## Netwerk management

### Device namen

Bij computers met meerdere Netwerk Interfaces (NIC's), is het van belang om vaste device benaming te gebruiken. Als dat niet gebeurt, worden configuratieproblemen veelal veroorzaakt door verandering in de benoeming.

[udev](/index.php/Udev "Udev") zorgt ervoor dat elk device een naam toegewezen krijgt. Systemd gebruikt [Predictable network Interface Names](http://www.freedesktop.org/wiki/Software/systemd/PredictablenetworkInterfaceNames), welk automatisch statische namen toekent aan netwerk devices. Interfaces worden hedentendage vooraf gegaan met `en` (bedraad/[Ethernet](https://en.wikipedia.org/wiki/Ethernet "w:Ethernet")), `wl` (draadloos/WLAN), of `ww` ([WWAN](https://en.wikipedia.org/wiki/Wireless_WAN "w:Wireless WAN")) gevolgd door een automatisch gegenereerde identifier, zoals: `enp0s25`.

**Tip:** Deze wijze van benoemen kan teruggedraaid worden naar de **eth0** of **wlan0** notatie, door `net.ifnames=0` aan de [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") toe te voegen.

**Note:** Vergeet in dat geval vooral niet om alle netwerk gerelateerde configuratiebestanden bij te werken!.

#### Toon de de huidige benaming

Zowel bedrade als wireless device-namen kunnen getoond worden met:

```
$ ls /sys/class/net

```

of via:

```
$ ip link

```

Let erop dat `lo` het [W:Loop_device](https://en.wikipedia.org/wiki/Loop_device "w:Loop device") is, en niet gebruikt wordt om een netwerkverbinding te leggen.

Wireless device-names kunnen eveneens achterhaald worden met `iw dev`. Zie ook [Wireless network configuration#Get the name of the interface](/index.php/Wireless_network_configuration#Get_the_name_of_the_interface "Wireless network configuration").

**Tip:** Teneinde de device-namen te veranderen, zie [#Change device name](#Change_device_name) en [#Revert to traditional device names](#Revert_to_traditional_device_names) (terug naar de traditionele benamingsmethode.

#### Activeren en De-actieveren van netwerk interfaces

Een netwerk interface activeren:

```
# ip link set *interface* up

```

Om te deactiveren gebruik dan:

```
# ip link set *interface* down

```

Om de interface koppeling te controleren `eth0`:

 `$ ip link show dev eth0` 
```
2: eth0: <BROADCAST,MULTICAST,PROMISC,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master br0 state UP mode DEFAULT qlen 1000
...

```

**Note:** In het geval de default route via de interface `eth0` loopt, zal bij deactivatie ook de route verdwijnen, en tevens zal bij re-activatie de default route niet automatisch hersteld worden. Zie [#Manual assignment](#Manual_assignment) om deze handmatig te kunnen herstellen.

### Dynamisch IP adres

Zie [#netwerk managers](#netwerk_managers) voor een opsomming van opties voor een dynamisch IP adres.

### Statisch IP adres

Een statisch IP adres kan via de meeste, standaard, [netwerk managers](#netwerk_managers) geconfigureerd worden. Welke manager ook gebruikt wordt, de volgend informatie zal voorhanden moeten zijn:

*   statisch IP adres
*   Subnet mask, of mogelijk de [CIDR notation](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation "wikipedia:Classless Inter-Domain Routing"), zoals `/24` de CIDR notatie is van het netmask `255.255.255.0`.
*   [Broadcast adres](https://en.wikipedia.org/wiki/Broadcast_address "wikipedia:Broadcast address")
*   [Gateway](https://en.wikipedia.org/wiki/Default_gateway "wikipedia:Default gateway")'s IP adres
*   Nameserver (DNS) IP adresen. Zie ook [resolv.conf](/index.php/Resolv.conf "Resolv.conf").

Bij een prive netwerk, is het een veilige, en standaard, keuze om IP adres bereik `192.168.*.*` te gebruiken, met een subnet mask van `255.255.255.0` en een broadcast address als `192.168.*.255`. De gateway is normaal gesproke `192.168.*.1` of `192.168.*.254`.

Echter, in een netwerk met meerdere guests (computers en/of servers) is het handiger om op de commandline korte adressen te kunnen gebruiken via een IP bereik van 10.0.0.* met als subnet 255.0.0.0 en een gateway/router adres van 10.0.0.1. Let wel dat het 192.* IP bereik in aan te schaffen apparatuur. (printers, routers, IP camera's, etc), altijd als standaard ingesteld is, en dat het even moeite vraagt om deze apparatuur binnen het 10.0.0.0 bereik te kunnen gebruiken.

**Warning:**

*   Wees er zeker van dat handmatig toegekende (statische) adressen niet in conflict komen met de door de DHCP serve toegekende dynamische adressen. Zie [op dit forum](http://www.raspberrypi.org/forums/viewtopic.php?f=28&t=16797) .

**Tip:** adressen kunnen berekend worden met behulp van het [ipcalc](https://www.archlinux.org/packages/?name=ipcalc) pakket; Zie [#Calculating_addresses](#Calculating_addresses).

#### Handmatige toewijzing statisch adres

Kan uitgevoerd worden met gebruik van het [iproute2](https://www.archlinux.org/packages/?name=iproute2) pakket. Dit is tevens een goode manier om de instellingen te testen, daar de aansluiting, op deze manier gemaakt, niet permanent is en bij een herstart verdwijnt. Allereerdt zor dat de [netwerk interface](#Device_namen) geactiveerd is:

```
# ip link set *interface* up

```

Ken, via de commandregel, een statisch IP adres toe:

```
# ip addr add *IP_adres*/*subnet_mask* broadcast *broadcast_adres* dev *interface*

```

Hetzelfde met het gateway IP adres:

```
# ip route add default via *default_gateway*

```

Bijvoorbeeld:

```
# ip link set eth0 up
# ip addr add 192.168.1.2/24 broadcast 192.168.1.255 dev eth0
# ip route add default via 192.168.1.1

```

**Tip:** Mocht zich de foutmelding voordoen: `RTNETLINK answers: netwerk is unreachable`, probeer dan het opzetten van de route in twee stappen te doen:
```
# ip route add 192.168.1.1 dev eth0
# ip route add default via 192.168.1.1 dev eth0

```

Om deze handelinge ongedaan te maken (b.v. alvorens over te gaan tot een dynamisch IP), verwijder alle toegekende IP adressen:

```
# ip addr flush dev *interface*

```

Verwijder daarna de aangegeven gateway:

```
# ip route flush dev *interface*

```

En tenslotte, deactiveer de netwerkkaart:

```
# ip link set *interface* down

```

Voor meerdere opties, zie de [ip(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ip.8). Deze commandline opdrachten kunnen geautomatiseerd uitgevoerd worden via scripts en [systemd units](/index.php/Systemd#Writing_unit_files "Systemd").

#### Bereken adressen

Met behulp van `ipcalc` installeerbaar via het [ipcalc](https://www.archlinux.org/packages/?name=ipcalc) pakket, kunnen IP broadcast, netwerk, netmask, en host bereik berekend worden in meer geavanceerde configuraties. Een voorbeeld kan zijn om Ethernet te gebruiken over Firewire om een Windows machine aan Linux te koppelen. Om veiligheids- en organisatorische redenen zullen beide machines hun eigen netwerk en broadcast gebruiken.

De respectievelijke netmask en broadcastadressen zijn zichtbaar te nmaken met `ipcalc`, door het IP van de Linux NIC in te geven `10.66.66.1` en daarbij het aantal hosts (in dit geval twee:

 `$ ipcalc -nb 10.66.66.1 -s 1` 
```
adres:   10.66.66.1

Netmask:   255.255.255.252 = 30
netwerk:   10.66.66.0/30
HostMin:   10.66.66.1
HostMax:   10.66.66.2
Broadcast: 10.66.66.3
Hosts/Net: 2                     Class A, Private Internet

```

### netwerk managers

Er is een ruime keuze voorhanden, maar hou voor ogen dat er slechts een daemon gestart mag zijn! In onderstaande tabel worden verschillende managers vergeleken. *Automatisch bedrade aansluiting* houdt in dat er voor de gebruiker tenminste 1 mogelijkheid bestaat om op eenvoudige wijze, en zonder configuratiebestand, de daemon op te starten om zo een ethernetaansluiting te realiseren:

| Connection manager | Automatically handles
wired connection | Official
GUI | [Archiso](/index.php/Archiso "Archiso") [[1]](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.both) | Console tools | Systemd units |
| [ConnMan](/index.php/ConnMan "ConnMan") | Yes | No | No | `connmanctl` | `connman.service` |
| [dhcpcd](/index.php/Dhcpcd "Dhcpcd") | Yes | No | Yes ([base](https://www.archlinux.org/groups/x86_64/base/)) | `dhcpcd` | `dhcpcd.service`, `dhcpcd@*interface*.service` |
| [netctl](/index.php/Netctl "Netctl") | Yes | No | Yes ([base](https://www.archlinux.org/groups/x86_64/base/)) | `netctl` | `netctl-ifplugd@*interface*.service` |
| [NetworkManager](/index.php/NetworkManager "NetworkManager") | Yes | Yes | No | `nmcli`,`nmtui` | `NetworkManager.service` |
| [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") | No | No | Yes ([base](https://www.archlinux.org/groups/x86_64/base/)) | `systemd-networkd.service`, `systemd-resolved.service` |
| [Wicd](/index.php/Wicd "Wicd") | Yes | Yes | No | `wicd-curses` | `wicd.service` |

Zie ook de [List of applications#Network_managers](/index.php/List_of_applications#Network_managers "List of applications").

## Bepaal de hostnaam

Een [hostnaam](https://en.wikipedia.org/wiki/Hostname "wikipedia:Hostname") is een unieke naam gegeven aan een apparaat op een netwerk, als aangeduid in `/etc/hostname`—zie [hostname(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.5) en [hostname(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.7) voor details. Het bestand kan eventueel ook de domeinnaam van het systeem/netwerk bevatten. Om de hostnaam in te stellen, [wijzig](/index.php/Textedit "Textedit") `/etc/hostname` en voeg een enkele regel toe met b.v. `*myhostname*`:

 `/etc/hostname` 
```
*myhostname*

```

**Tip:** Advies om een hostnname te kiezen: zie [RFC 1178](https://tools.ietf.org/html/rfc1178).

Als alternatief kan [hostnamectl(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/hostnamectl.1) gebruikt worden:

```
# hostnamectl set-hostname *myhostname*

```

Om een tijdelijke hostnaam toe te kennen, totaan een herstart, gebruik [hostname(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.1) van [inetutils](https://www.archlinux.org/packages/?name=inetutils):

```
# hostname *myhostname*

```

Om de hostnaam, en andere metadata,te verfraaien, zie [machine-info(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/machine-info.5#https%3A%2F%2Fwww.freedesktop.org%2Fsoftware%2Fsystemd%2Fman%2Fmachine-info.html).

### Lokaal netwerk hostnaam resolutie

Allereerst dient [#Set the hostname](#Set_the_hostname) uitgevoerd te zijn, waarmee de hostnaam resolutie in werking gezet wordt op de lokale computer zelf:

 `$ ping *myhostname*` 
```
PING myhostname (192.168.1.2) 56(84) bytes of data.
64 bytes from myhostname (192.168.1.2): icmp_seq=1 ttl=64 time=0.043 ms
```

Om het mogelijk te maken dat andere systemen in het netwerkwerk de computer via de **hostnaam** kunnen bereiken, is het noodzakelijk dat of:

*   het bestand [hosts(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5) geconfigureerd is, of
*   een dienst geactiveerd word welke de hostname kan zoeken en vinden.

**Note:** [systemd](https://www.archlinux.org/packages/?name=systemd) heeft daartoe de mogelijkheid via de `myhostname` nss module, standaard geactiveerd in `/etc/nsswitch.conf`. Echter, sommige systemen gebruiken wellicht toch nog het bestand `/etc/hosts`, zie [[2]](https://lists.debian.org/debian-devel/2013/07/msg00809.html) [[3]](https://bugzilla.mozilla.org/show_bug.cgi?id=87717#c55) voor voorbeelden.

Pas het hosts file aan door de volgende regel toe te voegen aan `/etc/hosts`:

1.  127.0.1.1 *myhostname*.localdomain *myhostname*

Als gevolg waarvan het systeem zichtbaar en bereikbaar is op beide adressen:

 `$ getent hosts` 
```
127.0.0.1       localhost
127.0.1.1       myhostname.localdomain myhostname

```

Overigens kan en mag **localdomain** door willekeurig welke domeinnaam vervangen worden, b.v. thuis,nl, jansen.xx, etc. Wees hierin wel consequent op de aangesloten systemen.

In host file kunnen tevens alle op het netwerk aanwezige systemen, voorzien van een statisch IP adres, opgenomen worden, welke dan eveneens via hunner eigen hostnaam herkend zullen worden, bijvoorbeeld:

{{hc|/etc/hosts| 127.0.0.1 localhost 127.0.1.1 myhostname.local myhostname 10.0.0.6 raspbian.local raspbian 10.0.0.5 xbian.local xbian 10.0.0.107 runeaudio.local runeaudio enz

En als klap op de vuurpijl kunnen ongewenste verbindingen naar de eeuwige jachtvelden gezonden worden door deze te verwijzen naar het niet bestaande 0.0.0.0 of naar het lokale adres 127.0.0.1:

1.  0.0.0.0 p78878.adskape.ru

Een kant en klaar, en regelmatig bijgewerkt, host file is te downloaden op [[4]](http://winhelp2002.mvps.org/hosts2.htm) de MVPhosts site

**Note:** Een optie is om een volledige DNS server zoals [BIND](/index.php/BIND "BIND") of [Unbound](/index.php/Unbound "Unbound"), maar dat is wel overkill en te complex voor de meeste systemen. In het geval van kleine / beperkte netwerken waar dynamisch en flexible hosts kunnen aan- en afkoppelen zijn de [zero-configuration netwerking](https://en.wikipedia.org/wiki/Zero-configuration_netwerking "wikipedia:Zero-configuration netwerking") services, goed toepasbaar:

*   [Samba](/index.php/Samba "Samba") verleent de hostnaam resolutie via Microsoft's **NetBIOS**. Benodigd is slechts de installatie van [samba](https://www.archlinux.org/packages/?name=samba) en activatie van de `nmbd.service` service. Computers met Windows, macOS, en Linux waarop `nmbd` is geinstalleerd, zullen de machine kunnen vinden.
*   [Avahi](/index.php/Avahi "Avahi") voorziet in de hostnaam resolutie via **zeroconf**, ook bekend als Avahi of Bonjour. Het vergt een enigzins complexer configuratie dan met Samba: zie [Avahi#Hostname resolution](/index.php/Avahi#Hostname_resolution "Avahi") voor meer info. Computers met macOS, of Linux met een werkende Avahi daemon, zullen de machine kunnen traceren. Windows beschikt niet over een ingebouwde Avahi client of daemon.

## Tips en tricks

### Device naam wijzigen

De device naam kan handmatig gewijzigd worden door aanmaak van een udev-rule. Bijvoorbeeld:

 `/etc/udev/rules.d/10-netwerk.rules` 
```
SUBSYSTEM=="net", ACTION=="add", ATTR{adres}=="aa:bb:cc:dd:ee:ff", NAME="net1"
SUBSYSTEM=="net", ACTION=="add", ATTR{adres}=="ff:ee:dd:cc:bb:aa", NAME="net0"

```

welke na een reboot automatisch geactiveerd zal worden.

Enkele opmerkingen:

*   Om het MAC adres van een netwerkkaart te verkrijgen, gebruik dit commando: `cat /sys/class/net/*device_name*/adres`
*   Gebruik alleen de in onderkast aangegeven hex waarden in een udev-rule. Hoofdletters worden niet verwerkt.

Indien de netwerkkaart over een dynamisch MAC adres beschikt, kan `DEVPATH` gebruikt worden, bijvoorbeeld:

 `/etc/udev/rules.d/10-netwerk.rules` 
```
SUBSYSTEM=="net", DEVPATH=="/devices/platform/wemac.*", NAME="int"
SUBSYSTEM=="net", DEVPATH=="/devices/pci*/*1c.0/*/net/*", NAME="en"

```

Het pad naar het device dient zowel naar de nieuwe als naar de oude naam te verwijzen, omdat deze rule tijdens het opstarten meer dan eens uitgevoerd kan worden. Zo is bijvoorbeeld `"/devices/pci*/*1c.0/*/net/enp*"` in de tweede regel niet goed, daar deze niet zal werken wanneer de naam veranderd is in `en`. Alleen de systeem-default rule zal deze in tweede instantie starten, waarmee de naam (terug) veranderd wordt in b.v.`enp1s0`.

Om [test](/index.php/Udev#Testing_rules_before_loading "Udev") de rules te testen, kunnen deze vanuit een userspace direct geactiveerd worden, b.v. via `udevadm --debug test /sys/*DEVPATH*`. Let er dan wel op dat de interface welke hernoemd gaat worden, eerst gedeactiveerd wordt(e.g. `ip link set enp1s0 down`).

**Note:** Bij het hernoemen zou **vermeden moeten worden om statische namen als** "eth*X*" and "wlan*X*"**, te gebruiken, daar dit tijdens het opstarten kan leiden tot onverwachte situaties tussen de kernel en udev. Daarvoor is het beter om namen te gebruiken die niet door de kernel gekend zijn, b.v.: `net0`, `net1`, `wifi0`, `wifi1`. Voor meer onformatie zie [systemd](http://www.freedesktop.org/wiki/Software/systemd/PredictablenetwerkInterfaceNames) documentation.**

### Terug naar de traditionele device namen

In het geval de gebruiker b.v. over scripts beschikt waarin verwezen wordt naar de traditionele benaming eth0 of wlan0, dan kan [Predictable netwerk Interface Names](http://www.freedesktop.org/wiki/Software/systemd/PredictablenetwerkInterfaceNames) gedeactiveerd worden via maskering van de udev-rule:

```
 # ln -s /dev/null /etc/udev/rules.d/80-net-setup-link.rules

```

### Instellen van device MTU en queue lengte

De [MTU](https://en.wikipedia.org/wiki/Maximum_transmission_unit "wikipedia:Maximum transmission unit") van het netwerk device en tevens de queue lengte kunnen aangepast worden via een udev-rule. Bijvoorbeeld:

 `/etc/udev/rules.d/10-netwerk.rules` 
```
ACTION=="add", SUBSYSTEM=="net", KERNEL=="wl*", ATTR{mtu}="1500", ATTR{tx_queue_len}="2000"

```

**Note:**

*   `mtu`: Bij PPPoE, dient de MTU niet groter te zijn dan 1492\. MTU kan ook ingesteld worden [systemd.netdev(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.netdev.5).
*   `tx_queue_len`: Gebruik kleine waarden voor langzamere devices met een hoge latency, zoals modem links en ISDN. Hoge waarden worden aanbevolen bij hoge snelheid aansluitingen met veel dataverkeer.

### ifplugd voor laptops

**Tip:** [dhcpcd](/index.php/Dhcpcd "Dhcpcd") voorziet standaard in deze mogelijkheid.

[ifplugd](https://www.archlinux.org/packages/?name=ifplugd) is een daemon welke automatisch een Ethernet device configureerd op het moment er een kabel aangesloten wordt, en de configuratie weer ongedaan maakt als de kabelverbinding weer verbroken wordt. Bijzonder nuttig bij laptops met een ingebouwde netwerk adapter, omdat de interface allen geconfigureerd wordt als er daadwerkelijk een kabelverbinding is. Ook is het handig wanneer alleeb de netwerkaansluiting opnieuw opgestart moet worden, zonder de laptop te hoeven herstarten.

Standaard configuratie geldt voor het `eth0` device. Wijzigingen hierin, bv het device of vertragingsinstellingen, kunnen aangebracht worden in `/etc/ifplugd/ifplugd.conf`.

**Note:** [netctl](/index.php/Netctl "Netctl") pakket is inclusief `netctl-ifplugd@.service`, ook kan `ifplugd@.service` uit het [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) pakket gebruikt worden. Bijvoorbeeld: [enable](/index.php/Enable "Enable") `ifplugd@eth0.service`.

### Bonding of LAG

Zie [netctl#Bonding](/index.php/Netctl#Bonding "Netctl") of [Wireless bonding](/index.php/Wireless_bonding "Wireless bonding").

### IP adres aliasing

Bij IP aliasing wordt meer dan een enkel adres toegevoegd aan aan een netwerk interface. Hierdoor is het mogelijk dat een node op een netwerk meerdere aansluitingen kan hebben met dat netwerk, waarbij elke aansluiting een ander doelkan dienen Deze methode wordt typisch gebruikt bij virtual hosting of Web en FTP servers, of bij herorganisatie van servers, zonder andere machines te hoeven updaten (dit kan erg handig zijn voor naamservers).

#### Voorbeeld

Omhandmatig een alias in te stellen voor een NIC, gebruik [iproute2](https://www.archlinux.org/packages/?name=iproute2), type:

```
# ip addr add 192.168.2.101/24 dev eth0 label eth0:1

```

Om het alias te verwijderen, type:

```
# ip addr del 192.168.2.101/24 dev eth0:1

```

Datapaketten, bedoeld voor een subnet, zullen standaars het primaire alias gebruiken. Wanneer het bestemmings IP zich binnen een subnet of een secondaire alias bevindt, zal het bron IP ook zo ingesteld worden. In het geval er meer dan een NIC is, kunnen de default routes weergegeven worden met `ip route`.

### MAC/hardware adres wijzigen

Zie [MAC address spoofing](/index.php/MAC_address_spoofing "MAC address spoofing").

### Internet delen

Zie [Internet sharing](/index.php/Internet_sharing "Internet sharing").

### Router configuratie

Zie [Router](/index.php/Router "Router").

### Promiscuous (willekeurig) mode

Bij inschakelen van de [promiscuous mode](https://en.wikipedia.org/wiki/Promiscuous_mode "wikipedia:Promiscuous mode") zal een (wireless) NIC alle ontvangen dataverkeer verwerken. Dit in tegenstelling tot de "normale modus" waarin een NIC alle data ,welke het niet geacht is te ontvangen, zal negeren. Willekeurige modus wordt veelal gebruikt bij probleemoplossing in geavanceerde netwerken en bij [packet sniffing](https://en.wikipedia.org/wiki/Packet_sniffing "wikipedia:Packet sniffing").

 `/etc/systemd/system/promiscuous@.service` 
```
[Unit]
Description=Set %i interface in promiscuous mode
After=netwerk.target

[Service]
Type=oneshot
ExecStart=/usr/bin/ip link set dev %i promisc on
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target

```

Activeren van de promiscuous mode op interface `eth0` via [enable](/index.php/Enable "Enable") `promiscuous@eth0.service`.

## Foutopsporing

### Swapping computers on the cable modem

Niet van toepassing op de Europese / Nederlandse markt

### Het TCP window scaling probleem

TCP-pakketten bevatten een "window" -waarde in hun koptekst, waarin wordt aangegeven hoeveel gegevens de andere host mogelijk in ruil zal sturen. Deze waarde wordt alleen weergegeven met slechts 16 bits, dus de venstergrootte bedraagt ​​maximaal 64Kb. TCP-pakketten worden een tijdje in de cache gehouden (ze moeten worden herordend), en aangezien het geheugen beperkt of nog beperkt is, kan een host geheugen tekort komen.

Terug in 1992, toen meer en meer geheugen beschikbaar werd, werd RFC 1323 geschreven om de situatie te verbeteren: Window Scaling. De "window" -waarde, die in alle pakketten wordt geleverd, wordt gewijzigd door een schaalfactor die eenmaal is gedefinieerd, aan het begin van de verbinding. Die 8-bits Scale Factor maakt het venster maximaal 32 keer hoger dan de oorspronkelijke 64Kb.

Het lijkt erop dat sommige oudere routers en firewalls op het internet de Scale Factor omschrijven naar 0, waardoor misverstanden tussen hosts veroorzaakt worden. De Linux kernel 2.6.17 introduceerde een nieuw berekeningsschema dat hogere schaalfactoren oplevert, waardoor de nasleep van de oudere routers en firewalls vrijwel zichtbaar wordt.

De resulterende verbinding is in ieder geval zeer langzaam of gebroken.

#### How to diagnose the problem

Het moge duidelijk zijn dat dit een raar probleem is. In sommige gevallen zal het niet mogelijk zijn om uberhaupt TCP aansluitingen (HTTP, FTP, ...) te gebruiken, en in een ander geval kan slechts met sommige hosts gecommuniceerd worden.

Indien dit probleem zich manifesteert zal de `dmesg`'s output er goed uitzien en de logs zullen leeg blijven, daarbij zal `ip addr` een normale status rapporteren, waardoor er op het eerste gezicht niet aan de hand lijkt te zijn.

Maar wanneer websites niet reageren en het pingen van een willekeurige host geen probleem oplevert, dan is er een grote kans dat we hier met genoemd probleem te maken hebben: ping gebruikt namelijk ICMP en heeft dus geen lastvan de TCP problemen.

Mischien dat [Wireshark](/index.php/Wireshark "Wireshark") iets verduidelijkt. Wellicht wordt UDP en ICMP verkeer zichbaar, maar TCP niet (alleen bij externe hosts).

#### Hoe te herstellen

##### Fout

Op de foute manier kan de `tcp_rmem` waarde, waarop Scale Factor calculatie is gebaseerd, aangepast worden. Alhoewel dit voor de meeste hosts zal werken, is er geen garantie dat dit ook het geval zal zijn voor met name hosts op afstand.

```
# echo "4096 87380 174760" > /proc/sys/net/ipv4/tcp_rmem

```

##### Goed

KISS: simpleweg deactiveren van de Window Scaling. Maar omdat Window Scaling is een fijne TCP feature is, voelt het wellicht niet fijn om het uit te schakelen, zeker als een oudere router er niet mee opgeknapt wordt. Window Scaling kan op meerdere manieren uitgeschakeld worden, maar klaarblijkelijk is de beste manier (en effectief met de meeste kernels), om de volgende regel toe te voegen aan `/etc/sysctl.d/99-disable_window_scaling.conf` (zie ook [sysctl](/index.php/Sysctl "Sysctl")):

```
net.ipv4.tcp_window_scaling = 0

```

##### Best

Omdat het probleem veroorzaakt wordt door een **defecte** router/firewall, is vervanging gewenst. Sommige gebruikers gaven aan dat hun defecte router de DSL router was.

#### Aanvullend

Gebaseerd op het LWN artikel [TCP window scaling and broken routers](http://lwn.net/Articles/92727/) en een Kernel Trap artikel: [Window Scaling on the Internet](http://kerneltrap.org/node/6723).

Meer relevante discussie zijn te vinden op de LKML.

### Realtek geen link / WOL probleem

Gebruikers met Realtek 8168 8169 8101 8111 (C) gebaseerde NIC's (kaarten en aan boord) kunnen het probleem hebben dat de NIC bij het opstarten gedeactiveerd lijkt te zijn en geen Link-lichtje heeft. Dit kan meestal worden gevonden op een dual boot systeem waar Windows ook geïnstalleerd is. Het lijkt erop dat het gebruik van de officiële Realtek-drivers (gedateerd na mei 2007) onder Windows de oorzaak is. Deze nieuwere stuurprogramma's schakelen de functie Wake-On-LAN uit door de NIC uit te schakelen bij de Windows-uitschakeltijd, waar het wordt uitgeschakeld tot de volgende keer dat Windows opstart. U zult kunnen opmerken of dit probleem u beïnvloedt als het Link-lampje uit blijft tot Windows opstart; tijdens het uitschakelen van Windows zal het Link-lampje weer uitschakelen. Normale werking moet zijn dat het verbindingslampje altijd brandt zolang het systeem aan staat, zelfs tijdens POST. Dit probleem heeft ook invloed op andere besturingssystemen zonder nieuwe drivers (bijv. Live CD's). Hier zijn een paar correcties voor dit probleem.

#### Activeren van de NIC in Linux

Ga naar [#Enabling and disabling netwerk interfaces](#Enabling_and_disabling_netwerk_interfaces) om de NIC in te schakelen.

#### Rollback/wijzig de Windows driver

U kunt uw Windows NIC-stuurprogramma terugzetten naar de Microsoft versie, indien beschikbaar, of terugzetten / installeer een officiële Realtek-driver van voor mei 2007 (staat op cd die bij uw hardware is geleverd).

#### Activeer WOL in Windows driver

Waarschijnlijk is de beste en de snelste oplossing om deze instelling in het Windows-stuurprogramma te wijzigen. Op deze manier zou het systeembreed opgelost moeten zijn en niet alleen onder Arch (bijvoorbeeld live CD's, andere besturingssystemen). Zoek in Windows onder Device Manager uw Realtek-netwerkadapter en dubbelklik op het. Onder het tabblad 'Geavanceerd' wijzigt u 'Wake-on-LAN na uitschakelen' in 'Inschakelen'.

In Windows XP (example):

```
Right click my computer and choose "Properties"
--> "Hardware" tab
  --> Device Manager
    --> netwerk Adapters
      --> "double click" Realtek ...
        --> Advanced tab
          --> Wake-On-Lan After Shutdown
            --> Enable

```

**Note:** Nieuwere Realtek Windows-stuurprogramma's (getest met *Realtek 8111/8169 LAN Driver v5.708.1030.2008* , gedateerd 2009/01/22, verkrijgbaar bij GIGABYTE) kunnen deze optie iets anders, zoals *Shutdown Wake-On- LAN -> inschakelen* . Het lijkt erop dat het overschakelen naar `Disable` geen effect heeft (u merkt dat het Link-lampje nog steeds wordt uitgeschakeld bij het uitschakelen van Windows). Eén vieze oplossing is om naar Windows te starten en het systeem opnieuw te resetten (een onhandige herstart / uitschakeling uitvoeren) waardoor de Windows-chauffeur geen kans krijgt om LAN uit te schakelen. Het Link-lampje blijft aan en de LAN-adapter blijft toegankelijk na POST - dat wil zeggen totdat u weer opstart naar Windows en het weer goed afsluit..

#### Nieuwe Realtek Linux driver

Nieuwere drivers voor deze Realtek kaarten zijn verkrijgbaar voor Linux op de Realtek site (ongetest, maar lost waarschijnlijk het probleem wel op).

#### Inschakelen *LAN Boot ROM* in BIOS/CMOS

Het lijkt erop dat de instelling *Integrated Peripherals --> Onboard LAN Boot ROM --> Enabled* in BIOS/CMOS de Realtek LAN chip bij system boot-up reactiveerd, ondanks dat de Windows driver bij afsluiten van het systeem het de-activeerd.

**Note:** Getest op een GIGABYTE GA-G31M-ES2L motherboard, BIOS version F8 released on 2009/02/05.

### No interface with Atheros chipsets

Gebruikers van sommige Atheros ethernet chips melden dat deze niet out-of-the-box werken. (bij installatiemedis van februari 2014). Een werkende oplossing is om vanuit [backports-patched](https://aur.archlinux.org/packages/backports-patched/) te installeren.

### Broadcom BCM57780

Deze Broadcom chipset gedraagt zich iet altijd netjes wanner nier specifiek aangegeven wordt dat de betreffende module geladen dient te worden. Het betreft de mosules `broadcom` en `tg3`, waarbij laatstgenoemde als eerste geladen dient te worden.

Onderstaande stappen bieden een oplossing voor deze chipset:

*   Zoek de NIC in *lspci* output:

 `$ lspci | grep Ethernet` 
```
02:00.0 Ethernet controller: Broadcom Corporation NetLink BCM57780 Gigabit Ethernet PCIe (rev 01)

```

*   Insien de bedrade netwerkaansluiting hapert, probeer het volgende, na eerst de kabel losgekoppeld te hebben:

```
# modprobe -r tg3
# modprobe broadcom
# modprobe tg3

```

*   Koppel de kabel weer aan. Mocht dit de oplossing te zijn geweest, dan kan de procedure permanent gemaakt worden door toevoeging van `broadcom` en `tg3` (in deze volgorde) aan de `MODULES` array in `/etc/mkinitcpio.conf`:

```
MODULES=".. broadcom tg3 .."

```

*   Rebuild the initramfs:

```
# mkinitcpio -p linux

```

*   Als alternatief kan ook een `/etc/modprobe.d/broadcom.conf` aangemaakt worden:

```
softdep tg3 pre: broadcom

```

**Note:** Deze methode kan ook werken voor andere chipsets, zoals de BCM57760.

### Realtek RTL8111/8168B

 `# lspci | grep Ethernet` 
```
03:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168B PCI Express Gigabit Ethernet controller (rev 02)

```

De adapter moet herkend worden door de `r8169` module. Echter, met enkele chiprevisies kan de aansluiting voortdurend aan en uit gaan. Het alternatief [r8168](https://www.archlinux.org/packages/?name=r8168) moet in dit geval gebruikt worden voor een betrouwbare aansluiting. [Blacklist](/index.php/Blacklist "Blacklist") `r8169`, als [r8168](https://www.archlinux.org/packages/?name=r8168) niet automatisch wordt geladen door [udev](/index.php/Udev "Udev"), zie [Kernel modules#Automatic module handling](/index.php/Kernel_modules#Automatic_module_handling "Kernel modules").

Ook kan matige IPv6 ondersteuning de oorzaak zijn bij sommige revisies. [IPv6#Disable functionality](/index.php/IPv6#Disable_functionality "IPv6") kan behulpzaam zijn bij problemen met hangende webpagina's en lage snelheden.

### Gigabyte Motherboard with Realtek 8111/8168/8411

Met moederborden zoals de Gigabyte GA-990FXA-UD3, opstartend met IOMMU uitgeschakeld (wat de standaard kan zijn) zorgt ervoor dat de netwerkinterface onbetrouwbaar is, vaak niet aansluit of aansluiting heeft, maar geen doorvoer mogelijk maakt. Dit geldt niet alleen voor de NIC aan boord, maar ook voor andere pci-NIC's, omdat de instelling van de IOMMU de gehele netwerkinterface op het bord beïnvloedt. Als u IOMMU inschakelt en opstart met de installatiemedia, worden AMD I-10 / xhci pagina-defecten voor een seconde gebroken, maar start daarna wel normaal op, wat resulteert in een volledig functionele interne NIC (zelfs bij de r8169-module).

Voeg `iommu=soft` als een [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") toe om bij het opstarten foutmeldingen te onderdrukken en de USB3.0-functionaliteit te herstellen.

## Zie ook

*   [Debian Reference: netwerk setup](https://www.debian.org/doc/manuals/debian-reference/ch05.en.html)
*   [RHEL7: netwerking Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/netwerking_Guide/)