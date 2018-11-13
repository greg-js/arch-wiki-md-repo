Related articles

*   [VLAN](/index.php/VLAN "VLAN")

Dit artikel behandelt de basis stappen voor het troubleshooten van netwerk connectiviteit.

**Note:** Voor het bekijken van de netwerk configuratie zijn geen root-rechten vereist. Voor het maken van wijzigingen wel.

## Contents

*   [1 iproute2](#iproute2)
*   [2 Netwerk Interfaces](#Netwerk_Interfaces)
*   [3 Link status](#Link_status)
*   [4 IP adres](#IP_adres)
*   [5 Route table](#Route_table)
*   [6 DNS Servers](#DNS_Servers)
*   [7 Ping & Tracepath/Traceroute](#Ping_&_Tracepath/Traceroute)

## iproute2

Vele Linux gebruikers kennen utilities zoals `ifconfig` en `route`, maar deze worden al geruime tijd ontraden. Alle functionaliteit is onder gebracht in een set utilities die zich bevinden in de `iproute2` package.

Inmiddels wordt in Arch Linux iproute2 standaard geinstalleerd en maakt bijvoorbeeld ook [netcfg](/index.php/Netcfg "Netcfg") hier gebruik van.

## Netwerk Interfaces

Bij het troubleshooten van netwerk is de eerste stap de snelle identificatie van de netwerk interfaces, dit kan met het volgende commando:

```
ip a

```

Dit geeft bijvoorbeeld de volgende output:

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 16436 qdisc noqueue state UNKNOWN 
   link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
   inet 127.0.0.1/8 scope host lo
   inet6 ::1/128 scope host 
      valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP qlen 1000
   link/ether 70:5a:b6:8a:a0:87 brd ff:ff:ff:ff:ff:ff
   inet 192.168.1.143/24 brd 192.168.1.255 scope global eth0
   inet6 fe80::725a:b6ff:fe8a:a087/64 scope link 
      valid_lft forever preferred_lft forever
3: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP qlen 1000
   link/ether 00:26:82:5a:6f:d9 brd ff:ff:ff:ff:ff:ff
   inet 192.168.1.148/24 brd 192.168.1.255 scope global wlan0
   inet6 fe80::226:82ff:fe5a:6fd9/64 scope link 
      valid_lft forever preferred_lft forever

```

## Link status

In het overzicht van het `ip a` commando zie je de link status al, maar je kunt deze ook op vragen met:

```
ip link show dev eth0

```

Dit geeft bijvoorbeeld de volgende output:

```
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state DOWN qlen 1000
   link/ether 70:5a:b6:8a:a0:87 brd ff:ff:ff:ff:ff:ff

```

Je kunt nu de interface online brengen met:

```
sudo ip link set dev eth0 up

```

## IP adres

In het overzicht van het `ip a` commando zie je het ip adres al, maar je kunt deze ook op vragen met:

```
ip addr show dev eth0

```

Dit geeft bijvoorbeeld de volgende output:

```
 2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP qlen 1000
   link/ether 70:5a:b6:8a:a0:87 brd ff:ff:ff:ff:ff:ff
   inet 192.168.1.143/24 brd 192.168.1.255 scope global eth0
   inet6 fe80::725a:b6ff:fe8a:a087/64 scope link 
      valid_lft forever preferred_lft forever

```

Een ip adres tijdelijk (na een reboot is de configuratie weg) toevoegen:

```
sudo ip addr add 192.168.1.143/24 dev eth0

```

Een ip adres verwijderen:

```
sudo ip addr del 192.168.1.143/24 dev eth0

```

## Route table

De route tabel kun je opvragen met:

```
ip route show

```

Of voor een specifieke interface:

```
ip route show dev eth0

```

Dit geeft bijvoorbeeld de volgende output:

```
default via 192.168.1.1  proto static 
192.168.1.0/24  proto kernel  scope link  src 192.168.1.143

```

De default gateway configureren:

```
sudo ip route add 0/0 via 192.168.1.1 dev eth0

```

De default gateway verwijderen:

```
sudo ip route del 0/0 via 192.168.1.1 dev eth0

```

## DNS Servers

DNS servers converteren domein namen in IP addressen. Wanneer je in staat bent IP adressen te pingen, maar websites openen etc. lukt niet, dan is de kans groot dat de dns configuratie foutief is. Je kunt de bestaande configuratie bekijken met:

```
cat /etc/resolv.conf

```

Dit geeft bijvoorbeeld de volgende output:

```
domain example.com
search example.com
nameserver 192.168.1.1

```

*   De regel '`nameserver`' is het relevante gedeelte, meerdere nameservers zijn mogelijk
*   De '`domain`' regel en `search` zijn optioneel
*   Vaak is de '`nameserver`' gelijk aan de default gateway, maar niet noodzakelijk.
*   Bij twijfel kun je gebruik maken van Google DNS als de default DNS Servers:

```
nameserver 8.8.8.8
nameserver 8.8.4.4

```

Testen of de dns server werkt kan eenvoudig met het `host` commando:

```
host www.archlinux.org 8.8.4.4

```

Bovenstaand commando doet een dns lookup op www.bbc.co.uk op de dns server 8.8.4.4 en geeft bijvoorbeeld de volgende output:

```
Using domain server:
Name: 8.8.4.4
Address: 8.8.4.4#53
Aliases: 

```

```
www.archlinux.org is an alias for gudrun.archlinux.org.
gudrun.archlinux.org has address 66.211.214.131

```

## Ping & Tracepath/Traceroute

Het ping commando kan helpen om de connectiviteit naar een bepaalde host te controleren.

De eerste stap in de controle is het pingen van de default gateway (vervang het onderstaande ip adres met de eigen default gateway):

```
ping -c4 192.168.1.1

```

Wanneer de parameter -c4 weg gelaten wordt, wordt er "eindeloos" gepinged. Dit kun je met CTRL+C onderbreken.

```
PING 192.168.1.1 (192.168.1.1) 56(84) bytes of data.
64 bytes from 192.168.1.1: icmp_req=1 ttl=64 time=0.193 ms
64 bytes from 192.168.1.1: icmp_req=2 ttl=64 time=0.190 ms
64 bytes from 192.168.1.1: icmp_req=3 ttl=64 time=0.192 ms
64 bytes from 192.168.1.1: icmp_req=4 ttl=64 time=0.189 ms

--- 192.168.1.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 2999ms
rtt min/avg/max/mdev = 0.165/0.184/0.193/0.014 ms

```

Bovenstaande uitvoer betekent dat de gateway bereikbaar is. Wanneer je in plaats daarvan "`Destination Host Unreachable`" krijgt, controleer dan het IP adres met bijbehorend netmask en de default gateway. Overigens kan deze melding ook verschijnen wanneer de firewall of router ICMP traffic blokkeert.

De volgende stap is het pingen van de dns server. Wanneer deze niet antwoordt kan `tracepath` of `traceroute` gebruikt worden om te zien waar in de routering naar de host toe het fout gaat.

```
traceroute 8.8.4.4

```

Ook hier geldt dat routers ICMP kunnen blokkeren en daarom er "no reply" antwoorden zijn.