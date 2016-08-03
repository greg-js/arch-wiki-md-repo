iptables je mocan [vatreni zid](/index.php/Firewall "Firewall") ugradjen u linux kernel i deo je [netfilter](https://en.wikipedia.org/wiki/Netfilter "wikipedia:Netfilter") projekta. Moze se podesiti direktno ili upotrebu jednog od mnogih [frontend-ova](/index.php/Firewalls#iptables_front-ends "Firewalls") i [GUI-ja](/index.php/Firewall#iptables_GUIs "Firewall"). ip tabele se koriste za [ipv4](https://en.wikipedia.org/wiki/Ipv4 "wikipedia:Ipv4") i ip6 tabele se koriste za [ipv6](https://en.wikipedia.org/wiki/Ipv6 "wikipedia:Ipv6").

## Contents

*   [1 Instalacija](#Instalacija)
*   [2 Osnovni koncepti](#Osnovni_koncepti)
    *   [2.1 tabele](#tabele)
    *   [2.2 lanci](#lanci)
    *   [2.3 mete](#mete)
    *   [2.4 moduli](#moduli)
*   [3 Konfigurisanje](#Konfigurisanje)
    *   [3.1 Sa komandne linije](#Sa_komandne_linije)
    *   [3.2 Konfiguracioni fajl](#Konfiguracioni_fajl)
    *   [3.3 Cuvanje brojaca](#Cuvanje_brojaca)
    *   [3.4 Uputstva](#Uputstva)
*   [4 Logovanje](#Logovanje)
    *   [4.1 Ogranicavanje ucestalosti logovanja](#Ogranicavanje_ucestalosti_logovanja)
    *   [4.2 syslog-ng](#syslog-ng)
    *   [4.3 ulogd](#ulogd)
    *   [4.4 Dalje citanje](#Dalje_citanje)

## Instalacija

**Note:** Vas kernel mora biti kompajliran sa iptables podrskom. Svi Arch Linux kerneli iz oficijalnih repozitorijuma imaju podrsku za ip tabele.

Prvo, instalirajte korisnicke programe:

```
# pacman -S iptables

```

Sledece, dodajte ip tabele u [DAEMONS niz](/index.php/Daemon "Daemon") u /etc/rc.conf da bi ih ucitali u vasa podesavanja prilikom butovanja:

```
DAEMONS=(... **iptables** network ...)

```

## Osnovni koncepti

### tabele

iptables sadrze cetiri tabele: raw, filter, nat i mangle.

### lanci

Lanci se koriste za zadavanje skupa pravila. Paket pocinje pri vrhu lanca i nastavlja dalje ka dole dok ne pogodi pravilo. Postoje tri ugradjena lanca: INPUT, OUTPUT i FORWARD. Sav odlazni saobracaj prolazi kroz FORWARD lanac i sav dolazeci saobracaj prolazi kroz FORWARD lanac. Tri ugradjena lanca imaju pocetne mete koje se koriste ako ni jedno pravilo nije pogodjeno. Lanci definisani od strane korisnika se mogu dodati da bi se skup pravila ucinio efikasnijim.

### mete

"meta" je rezultat koji se desava kada paket pogodi pravilo. Mete se zadaju upotrebom "skoka" (-j). Najcesce mete su ACCEPT, DROP, REJECT i LOG.

### moduli

Postoje mnogi moduli koji se mogu koristiti za prosirivanje ip tabela poput connlimit, conntrack, limit i recent. Ovi moduli dodaju dodatnu funkcionalnost koja omogucava kompleksna pravila filterovanja.

## Konfigurisanje

### Sa komandne linije

Mozete da proverite trenutni skup pravila i broj pogodaka po pravilu upotrebom komande:

```
# iptables -nvL
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination   

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination    

Chain OUTPUT (policy ACCEPT 0K packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination

```

Ako izlaz izgleda kao gore, onda nema pravila.

Mozete da flush-ujete i resetujete ip tabele na difolt upotrebom ovih komandi:

```
# iptables -P INPUT ACCEPT
# iptables -P FORWARD ACCEPT
# iptables -P OUTPUT ACCEPT
# iptables -F
# iptables -X

```

### Konfiguracioni fajl

Konfiguracioni fajl na /etc/conf.d/iptables pokazuje na lokaciju konfiguracionog fajla. Skup pravila je ucitan kada se daemon startuje.

IPTABLES=/usr/sbin/iptables IP6TABLES=/usr/sbin/ip6tables

IPTABLES_CONF=/etc/iptables/iptables.rules IP6TABLES_CONF=/etc/iptables/ip6tables.rules IPTABLES_FORWARD=0 # enable IP forwarding?

Da sacuvate trenutni skup pravila, upotrebite komandu:

```
# /etc/rc.d/iptables save

```

Da ucitate skup pravila, upotrebite ovu komandu:

```
# /etc/rc.d/iptables restart

```

### Cuvanje brojaca

Mozete takodje, opciono, da sacuvate bajt i paket brojace. Da to uradite, editujte /etc/rc.d/iptables

U **save)** sekciji, izmenite liniju:

```
/usr/sbin/iptables-save > $IPTABLES_CONF

```

na

```
/usr/sbin/iptables-save -c > $IPTABLES_CONF

```

U **stop)** sekciji, dodajte sledece da sacuvate pre stopiranja:

```
stop)
     $0 save
     sleep 2

```

U **start)** sekciji, promenite liniju:

```
/usr/sbin/iptables-restore < $IPTABLES_CONF

```

na

```
/usr/sbin/iptables-restore -c < $IPTABLES_CONF

```

i sacuvajte fajl

### Uputstva

*   [Simple stateful firewall (Српски)](/index.php?title=Simple_stateful_firewall_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)&action=edit&redlink=1 "Simple stateful firewall (Српски) (page does not exist)")
*   [Router (Српски)](/index.php?title=Router_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)&action=edit&redlink=1 "Router (Српски) (page does not exist)")

## Logovanje

LOG meta se moze koristiti za logovanje paketa koji pogadjaju pravilo. Nasuprot drugim metama poput ACCEPT ili DROP, paket ce nastaviti da se krece kroz lanac nakon sto pogodi LOG metu. Ovo znaci da ako hocete da omogucite logovanje svih ispustenih paketa, morate da dodate duplo LOG pravilo pre svakog DROP pravila. Posto ovo umanjuje efikasnost i cini stvari manje jednostavnim, LOGDROP lanac se moze napraviti umesto toga.

```
## /etc/iptables/iptables.rules

*filter
:INPUT DROP [0:0]
:FORWARD DROP [0:0]
:OUTPUT ACCEPT [0:0]

... lanci definisani od strane drugih korisnika ..

## LOGDROP chain
:LOGDROP - [0:0]

-A LOGDROP -m limit --limit 5/m --limit-burst 10 -j LOG
-A LOGDROP -j DROP

... pravila ...

## log i drop paketi koji pogadjaju ovo pravilo:
-A INPUT -m state --state INVALID -j LOGDROP

... jos pravila ...

```

### Ogranicavanje ucestalosti logovanja

Modul za ogranicavanje se koristi za sprecavanje preteranog narastanja vaseg log fajla za ip tabele ili uzrokovanja bespotrebnog pisanja na hard disk. Bez ogranicavanja, napadac bi mogao da ispuni vas hard disk (ili bar vasu /var particiju) tako sto bi izazvao pisanje u log za ip tabele.

**-m limit** se koristi za poziv na modul za ogranicavanje. Mozete da upotrebite --limit da podesite prosecnu stopu i --limit-burst da podesite pocetnu burst stopu. Primer:

```
-A LOGDROP -m limit --limit 5/m --limit-burst 10 -j LOG

```

Ovo zadaje pravilo u LOGDROP lanac koji ce logovati sve pakete koji prolaze kroz njega. Prvih 10 paketa ce biti logovano, a zatim ce samo 5 paketa po minutu biti logovano. "limit burst" je obnovljen za jedan svaki put kada "limit rate" nije narusen.

### syslog-ng

Pretpostavljajuci da koristite syslog-ng koji je difolt u Arch Linux-u, mozete da kontrolisete gde ip tabele loguju izlaz na sledeci nacin:

```
filter f_everything { level(debug..emerg) and not facility(auth, authpriv); };

```

na

```
filter f_everything { level(debug..emerg) and not facility(auth, authpriv) and not filter(f_iptables); };

```

Ovo ce zaustaviti logovanje izlaza ip tabela u /var/log/everything.log.

Ako isto zelite da ip tabele loguju u neki drugi fajl a ne u /var/log/iptables.log, mozete jednostavno da izmenite vrednost fajla destinacije d_iptables ovde (jos uvek u syslog-ng.conf)

```
destination d_iptables { file("/var/log/iptables.log"); };

```

### ulogd

ulogd je specijalizovan daemon za logovanje paketa u korisnickom prostoru za netfilter koji moze da zameni difolt LOG metu.

[stranica projekta](http://www.netfilter.org/projects/ulogd/index.html)

[ulogd](https://www.archlinux.org/packages/?name=ulogd)

### Dalje citanje

*   [Wikipedia clanak za IP tabele](https://en.wikipedia.org/wiki/Iptables "wikipedia:Iptables")

*   [Home stranica za IP tabele](http://www.netfilter.org/projects/iptables/index.html)