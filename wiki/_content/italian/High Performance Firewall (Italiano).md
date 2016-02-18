La guida è stata realizzata basandosi su un esperienza reale di un utente, quindi il tutto è basato sulla configurazione dell'utente stesso.

Immaginate questo, avete più di due reti separate da un protocollo di Virtual Lan (IEEE 802.1q) o VLAN, a cui fate accesso tramite uno switch con una linea trunk 10/100/1000 MB HD/FD (naturalmente la migliore è 1000 MB FD).

Dovete condividere la rete con un numero MOLTO GRANDE di host, e mantenere delle buone prestazioni. La prima scelta è di separare le reti in altrettante porte e magari con altrettanti firewall. Magari non è la migliore idea per i costi, ma funziona.

La seconda scelta è quella spiegata qui.

## Contents

*   [1 I fatti:](#I_fatti:)
*   [2 Il lavoro](#Il_lavoro)
    *   [2.1 Supporto delle VLAN](#Supporto_delle_VLAN)
    *   [2.2 Il firewall](#Il_firewall)
        *   [2.2.1 Il NAT round robin](#Il_NAT_round_robin)
        *   [2.2.2 Trucchi](#Trucchi)
    *   [2.3 Aumentare le performance](#Aumentare_le_performance)
    *   [2.4 Iproute2](#Iproute2)
*   [3 Conclusioni](#Conclusioni)

### I fatti:

	Abbiamo circa 4 netmask 21 ex. ognuna con 8 classi di tipo C!!! Abbiamo quindi tantissimi MAC address e altrettanti pericolosi BROADCAST.

	Abbiamo inoltre 30 IP pubblici in 3 gruppi

	E una piccola macchina ...solo per fare test.

	Più in la verrà aggiunga una rete di classe C con molte altre subnet.

# Il lavoro

## Supporto delle VLAN

First, create sub-network as in page [VLAN](/index.php/VLAN "VLAN").

## Il firewall

Può essere realizzato un firewall/nat con *iptables* in maniera semplice e ci sono molte guide su questo...

Pensate che dovrete lavorare con molto traffico, questo vuol dire un uso massivo di CPU, quindi mantenete poche regole, solo le strette necessarie. Accept all per default per fare NAT. Probabilmente è meglio favorire alcune porte, (80,443,25,110,21,20,53 etc), ricordatevi che ogni pacchetto che passa per il vostro firewall deve attraversare tutte le regole fino a che non ne trova una che lo riguarda, altrimenti cade nella politica di default.

### Il NAT round robin

Supponiamo di avere un ip: 200.aaa.bbb.6 e il nostro gateway è 200.aaa.bbb.1\. Possiamo tranquillamente mettere questi parametri di default nella nostra configurazione.

Abbiamo detto che abbiamo 3 gruppi con 10 IP ognuno ... definiamo quindi il NEXT HOP nel nostro firewall:

```
Gr1='200.AAA.CCC.10-200.AAA.CCC.20'
Gr2='200.AAA.DDD.10-200.AAA.DDD.20'
Gr3='200.AAA.EEE.10-200.AAA.EEE.20'

```

**Le prossime righe necessarie sono:**

```
iptables -t nat -A POSTROUTING -s 192.168.0.0/21  -j SNAT --to $Gr1 #ACCESS VLAN 10
iptables -t nat -A POSTROUTING -s 192.168.8.0/21  -j SNAT --to $Gr2 #ACCESS VLAN 20
iptables -t nat -A POSTROUTING -s 192.168.15.0/21  -j SNAT --to $Gr1 #ACCESS VLAN 30
.... etc

```

Potrete ripetere i gruppi per gli accessi, suddividete le reti ETC, iptables userà una politica round robin su Gr1, Gr2 e Gr3 per default, non sono necessarie ulteriori modifiche.

Non è necessario creare un interfaccia virtuale (alias) per ogni IP del gruppo.

E' importante che ogni router conosca ogni gruppo e diffonda questo via BGP (o simile) ai vicini.

### Trucchi

Per favorire alcune porte potreste mettere queste regole in cima alla catena di FORWARD

```
iptables -A FORWARD -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A FORWARD -p icmp -o eth0 -j ACCEPT
iptables -A FORWARD -p tcp -m multiport --dports 80,443,110,53 -j ACCEPT  # FAST FAST FAST 
iptables -A FORWARD -p udp  --dport 53 -j ACCEPT

```

Che voglio dire:

*   I pacchetti passano la regola 1 se fanno parte di una connessione già aperta.
*   I pacchetti passano la regola 2 se fanno parte del protocollo icmp (PING o similari)
*   I pacchetti passano la regola 3 se il loro protocollo è http, mail o simile
*   e le richieste al DNS attraverseranno 3 o 4 regolo prima di pasare

I virus potrebbero infastidire al nostra macchina.. quindi...

```
 #VIRUS
iptables -A FORWARD -p tcp --dport 135:139 -j DROP
iptables -A FORWARD -p tcp --dport 445 -j DROP
iptables -A FORWARD -p udp --dport 135:139 -j DROP
iptables -A FORWARD -p udp --dport 445 -j DROP

```

## Aumentare le performance

Siamo arrivate alla parte importate di questo howto.

Abbiamo dimenticato qualcosa durante la nostra corsa

1.  Abbiamo dimenticato che vi è solo un NICs con potenzialmente più di 8000 indirizzi Mac. La memoria della scheda di rete non è adatta per questo!!!
2.  Per default iptable non è in grado di gestire tutte queste richieste contemporaneamente !!!!!

Quindi...

Per il primo problema... La soluzione è questa.. **aumentare la soglia di memoria per i vicini.** Date questo comando e leggete:

```
# cat /proc/sys/net/ipv4/neigh/default/gc_thresh1 
128
# cat /proc/sys/net/ipv4/neigh/default/gc_thresh2 
512
# cat /proc/sys/net/ipv4/neigh/default/gc_thresh3 
1024

```

Dopo di che mettete queste righe nel vostro /etc/sysctrl.conf

```
net.ipv4.neigh.default.gc_thresh1 = 512
net.ipv4.neigh.default.gc_thresh2 = 1024
net.ipv4.neigh.default.gc_thresh3 = 2048

```

e date *sysctl -p* per portarle al doppio!!! (non serve riavviare) con questi non si dovrebbero avere errori!!!!

La prossima parte richiede una comprensione su buckets e conntracks e hashsize (il modo in cui iptable gestisce le connessione nat). Esiste un buon documento su questo [qui](http://www.wallfire.org/misc/netfilter_conntrack_perf.txt) (in Inglese). L'autore consiglia di leggerlo!!!! Qualcosa è cambiato da quanto IPtables è conosciuto come Netfilter.

In breve!!! Mettete questo nella sezione MODULES:

```
MODULES=(8021q 'nf_conntrack hashsize=1048576' nf_conntrack_ftp 
                               ...e gli altri nf_stuff .......)

```

L'ultima è solo per evitare alcuni problemi che abbiamo con con le connessioni ftp.

'**nf_conntrack hashsize=1048576'** aumenta il numero dell' hashsize (aumenta la memoria dedicata al NAT) (è necessario riavviare o **ricaricare il modulo** :-) controllate con *dmesg | grep conntrack*)

Poi mettiamo qualcosa di simile nel file */etc/sysctl.d/99-sysctl.conf*

```
...
net.netfilter.nf_conntrack_max = 1048576
...

```

E diamo il comando

```
# sysctl --system

```

Nel nostro caso i numeri sono gli stessi, ciò vuol dire che ho 1 connessione per bucket!!!!

Nel nostro caso abbiamo circa 600.000 connessioni simultanee in 2 schede da 1 Giga, potrete verificare ciò con il comando

```
# cat /proc/sys/net/netfilter/nf_conntrack_count

```

E mettete questo in un demone snmpd per avere un grafico.

Un esempio [qui](http://carlost.890m.com/conntrack.png).

## Iproute2

Abbiamo 3 grandi accessi ad Internet!!! Questo perchè abbiamo a che fare con 3 gruppi di IP di classe C. Quindi abbiamo 3 traffici in entrata da gestire, ma solo uno in uscita!!! Il nostro gateway di default.

Per prima cosa dobbiamo mettere delle nuove tabelle nel file */etc/iproute2/rt_tables*

```
# echo 200 PRO_1 >> /etc/iproute2/rt_tables
# echo 205 PRO_2 >> /etc/iproute2/rt_tables
# echo 210 PRO_3 >> /etc/iproute2/rt_tables

```

Possono essere più o meno a seconda del traffico.

Secondo.. dobbiamo dare un gateway di default per queste tabelle.

```
# ip route add default via 200.aaa.bbb.2 table PRO_1
# ip route add default via 200.aaa.bbb.3 table PRO_2
# ip route add default via 200.aaa.bbb.4 table PRO_3

```

E' raccomandato ma non necessario mettere una interfaccia di rete per ogni tabella. Se non inserite le prossime righe, non avrete risposta ai ping nella rete locale.

```
# ip route add 192.168.0.0/21 via 192.168.0.1 table PRO_1
# ip route add 192.168.8.0/21 via 192.168.8.1 table PRO_1
# ip route add 192.168.15.0/21 via 192.168.15.1 table PRO_1
.....
lo stesso per PRO_2, e per PRO_3

```

L'ultima cosa da fare è dare un ordine ai pacchetti

```
# ip rule add from 192.168.0.0/21 table PRO_1
....
....

```

Potreste utilizzare PRO_X e persino con mask e submask. Per esempio vogliamo dare solo una classe C all'uscita con PRO_3

```
# ip rule add from 192.168.1.0/24 table PRO_3

```

Da mettere prima di <NET>/21

PROVIAMO IL TUTTO

prendete un PC Windows in una delle reti private e fate un traceroute verso qualcuno!!

Prima potreste andare su qualche sito tipo www.whatismyip.com e vedere il vostro ip attuale, rifarlo dopo un po e vedere che l'ip è cambiato ETC...

# Conclusioni

Ora lo scrittore della guida sta usando un PC con 2G di ram, Intel Pentium 4 2.8GHz Dual e 2 NICs 1Gb (una integrata e una PCI-E), l'utilizzo della CPU non va oltre picchi all'80%...