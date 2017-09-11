**Warning:** Le informazioni di questa pagina sono attualmente obsolete. Per ora, fare riferimento alla [versione inglese](/index.php/Network_configuration "Network configuration").

Articoli correlati

*   [Jumbo frames](/index.php/Jumbo_frames "Jumbo frames")
*   [Firewalls](/index.php/Firewalls "Firewalls")
*   [Samba (Italiano)](/index.php/Samba_(Italiano) "Samba (Italiano)")
*   [Wireless Setup (Italiano)](/index.php/Wireless_Setup_(Italiano) "Wireless Setup (Italiano)")
*   [List of applications#Network Managers](/index.php/List_of_applications#Network_Managers "List of applications")

Una semplice guida per la configurazione di rete e risoluzione di problemi annessi.

## Contents

*   [1 Primo controllo](#Primo_controllo)
*   [2 Impostare l'host name](#Impostare_l.27host_name)
*   [3 Driver dispositivo](#Driver_dispositivo)
    *   [3.1 Controllo stato driver](#Controllo_stato_driver)
    *   [3.2 Caricare il modulo del dispositivo](#Caricare_il_modulo_del_dispositivo)
*   [4 Interfacce di rete](#Interfacce_di_rete)
    *   [4.1 Nomi dispositivi persistenti](#Nomi_dispositivi_persistenti)
    *   [4.2 Ottenere il nome corrente del dispositivo](#Ottenere_il_nome_corrente_del_dispositivo)
    *   [4.3 Abilitare/disabilitare l'interfaccia](#Abilitare.2Fdisabilitare_l.27interfaccia)
*   [5 Configurare l'indirizzo IP](#Configurare_l.27indirizzo_IP)
    *   [5.1 Indirizzo IP dinamico](#Indirizzo_IP_dinamico)
        *   [5.1.1 Esecuzione manuale del Demone Client DHCP](#Esecuzione_manuale_del_Demone_Client_DHCP)
        *   [5.1.2 Esecuzione all'avvio di DHCP](#Esecuzione_all.27avvio_di_DHCP)
    *   [5.2 Indirizzo IP Statico](#Indirizzo_IP_Statico)
        *   [5.2.1 Assegnazione manuale](#Assegnazione_manuale)
        *   [5.2.2 Calcolo indirizzi](#Calcolo_indirizzi)
*   [6 Caricare la configurazione](#Caricare_la_configurazione)
*   [7 Impostazioni aggiuntive](#Impostazioni_aggiuntive)
    *   [7.1 ifplugd per laptops](#ifplugd_per_laptops)
    *   [7.2 Bonding o LAG](#Bonding_o_LAG)
    *   [7.3 Aliasing indirizzo IP](#Aliasing_indirizzo_IP)
        *   [7.3.1 Esempio](#Esempio)
    *   [7.4 Cambiare MAC/hardware address](#Cambiare_MAC.2Fhardware_address)
*   [8 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [8.1 Scambio computer/modem via cavo](#Scambio_computer.2Fmodem_via_cavo)
    *   [8.2 Il problema del TCP Window Scaling](#Il_problema_del_TCP_Window_Scaling)
        *   [8.2.1 Come diagnosticare questo problema?](#Come_diagnosticare_questo_problema.3F)
        *   [8.2.2 Come risolverlo? (La strada sbagliata)](#Come_risolverlo.3F_.28La_strada_sbagliata.29)
        *   [8.2.3 Come risolverlo? (Il metodo corretto)](#Come_risolverlo.3F_.28Il_metodo_corretto.29)
        *   [8.2.4 Come risolverlo? (Il metodo migliore)](#Come_risolverlo.3F_.28Il_metodo_migliore.29)
        *   [8.2.5 Ulteriori informazioni](#Ulteriori_informazioni)
    *   [8.3 Problema No Link / WOL schede Realtek](#Problema_No_Link_.2F_WOL_schede_Realtek)
        *   [8.3.1 Metodo 1 - Ripristino driver Windows](#Metodo_1_-_Ripristino_driver_Windows)
        *   [8.3.2 Metodo 2 - Abilitare il Wake on Lan nel driver Windows](#Metodo_2_-_Abilitare_il_Wake_on_Lan_nel_driver_Windows)
        *   [8.3.3 Metodo 3 - Aggiornare il driver Linux Realtek](#Metodo_3_-_Aggiornare_il_driver_Linux_Realtek)
        *   [8.3.4 Metodo 4 - Abilitare *LAN Boot ROM* nel BIOS/CMOS](#Metodo_4_-_Abilitare_LAN_Boot_ROM_nel_BIOS.2FCMOS)
    *   [8.4 Problema con DLink G604T/DLink G502T DNS](#Problema_con_DLink_G604T.2FDLink_G502T_DNS)
        *   [8.4.1 Come diagnosticare il problema](#Come_diagnosticare_il_problema)
        *   [8.4.2 Come risolvere il problema](#Come_risolvere_il_problema)
        *   [8.4.3 Maggiori informazioni](#Maggiori_informazioni)
    *   [8.5 Controllo problemi DHCP prima del rilascio dell'IP](#Controllo_problemi_DHCP_prima_del_rilascio_dell.27IP)
*   [9 Wiki Correlati](#Wiki_Correlati)

## Primo controllo

Molte volte, l’installazione di base ha già creato una configurazione di rete funzionante. Per verificare, utilizzare il seguente comando:

 `ping -c 3 www.google.com` 
```
PING www.l.google.com (74.125.224.146) 56(84) bytes of data.
64 bytes from 74.125.224.146: icmp_req=1 ttl=50 time=437 ms
64 bytes from 74.125.224.146: icmp_req=2 ttl=50 time=385 ms
64 bytes from 74.125.224.146: icmp_req=3 ttl=50 time=298 ms

--- www.l.google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 1999ms
rtt min/avg/max/mdev = 298.107/373.642/437.202/57.415 ms

```

**Suggerimento:** L'opzione `-c 3` esegue `ping` 3 volte. Vedere[ping(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ping.8) per maggiori informazioni.

Se funziona, si possono personalizzare le impostazioni con le opzioni che seguono.

Se il comando precedente riporta errori di host sconosciuti, significa che il pc non è riuscito a risolvere il nome di dominio. Ciò potrebbe dipendere dal proprio provider o dal proprio router/gateway. Si può provare a pingare un indirizzo IP statico, per accertarsi che la macchina abbia accesso ad Internet.

```

$ ping -c 3 8.8.8.8 
```

```

PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.

64 bytes from 8.8.8.8: icmp_req=1 ttl=53 time=52.9 ms

64 bytes from 8.8.8.8: icmp_req=2 ttl=53 time=72.5 ms

64 bytes from 8.8.8.8: icmp_req=3 ttl=53 time=70.6 ms

--- 8.8.8.8 ping statistics ---

3 packets transmitted, 3 received, 0% packet loss, time 2002ms

rtt min/avg/max/mdev = 52.975/65.375/72.543/8.803 ms
```

**Suggerimento:** 8.8.8.8 è un indirizzo statico semplice da ricordare. Si tratta dell'indirizzo del principale server DNS di Google, quindi può essere considerato affidabile, e generalmente non è bloccato da filtri sui contenuti e da proxy.

Se si riesce a pingare quell'indirizzo, si può provare ad [aggiungere questo nameserver al proprio file resolv.conf](#Indirizzo_IP_dinamico).

## Impostare l'host name

Un host name è un nome univoco creato per identificare un pc in rete. Con Arch Linux, l’host name del pc è impostabile in `/etc/rc.conf` o, fino a quando non si riavvia, con il comando `hostname`. Per gli host names si possono utilizzare solo caratteri alfanumerici. Il trattino (`-`) può essere utilizzato, ma né all’inizio né alla fine dell’host name. La lunghezza di quest'ultimo è limitata a 63 caratteri.

Semplicemente inserire il proprio host name in `/etc/hostname`; non inserire il nome di dominio in `/etc/hostname`. Qualora non esistesse, creare il file, come nell'esempio `archlinux` è l'host name:

 `/etc/hostname` 
```

archlinux

```

Dopo aver impostato l’host name, è importante includere lo stesso in `/etc/hosts`. Questo aiuterà i processi che fanno riferimento al computer attraverso il suo hostname per trovarne l’indirizzo IP, così come faranno i programmi che si basano sulla chiamata di sistema `gethostname ()` per determinare l'host name del sistema.

Editare `/etc/hosts` ed aggiungere lo stesso HOSTNAME che è stato inserito in `hostname`:

```
127.0.0.1      archlinux.domain.org   localhost.localdomain      localhost    archlinux

```

**Nota:** Il nome di dominio completo (FQDN) dovrebbe essere **il primo elemento dopo l'indirizzo IP**. Tutti i nomi sul lato destro sono solo alias per il nome host/dominio situato più a sinistra. Potete controllare se questo è stato configurato correttamente eseguendo `hostname --fqdn`.

Per impostare l’hostname temporaneamente (fino al successivo riavvio), utilizzare il comando `hostname` dal pacchetto [inetutils](https://www.archlinux.org/packages/?name=inetutils) da root:

 `# hostname archlinux` 

## Driver dispositivo

### Controllo stato driver

Udev dovrebbe riconoscere il modulo dell’interfaccia di rete (NIC) e caricarlo automaticamente al boot. Controllare la voce "Ethernet controller" nell'output di `lspci -v`. Esso dovrebbe indicare quali moduli del kernel contengono il driver del proprio dispositivo di rete. Ad esempio:

 `lspci -v` 
```
 02:00.0 Ethernet controller: Attansic Technology Corp. L1 Gigabit Ethernet Adapter (rev b0)

 	...
  	Kernel driver in use: atl1 
 	Kernel modules: atl1

```

Dopodichè, controllare che sia caricato il modulo, tramite *dmesg | grep <module name>*. Ad esempio:

```
dmesg |grep atl1

```

```
   ...
   atl1 0000:02:00.0: eth0 link is up 100 Mbps full duplex

```

Se il driver è caricato correttamente, saltare questa sezione. Altrimenti, è necessario individuare quale modulo è necessario per il proprio particolare modello.

### Caricare il modulo del dispositivo

Utilizzare Google per individuare il modulo/driver corretto per il chip. Una volta individuato il modulo da utilizzare, è possibile caricarlo con:

```
 # modprobe <modulename> 

```

## Interfacce di rete

### Nomi dispositivi persistenti

Per le schede madri con schede di rete NICs integrate, è importante conoscere quale NIC è considerata primaria (ad esempio, "eth0") e quale NIC è considerata secondaria (ad esempio, "eth1"). Molti problemi di configurazione sono causati da utenti che non impostano correttamente la configurazione di "eth0" nel file `/etc/rc.conf`, quando in realtà, hanno il cavo Ethernet collegato in "eth1".

[Udev](/index.php/Udev_(Italiano) "Udev (Italiano)") è responsabile dell'assegnazione dei nomi ai dispositivo. Con Udev ed i driver di rete modulari, la numerazione dell'interfaccia di rete non è persistente anche dopo un riavvio, perché i driver vengono caricati in parallelo e, quindi, in ordine casuale. Configurare la connessione di rete è difficile se non si sa se ​​la propria scheda verrà chiamata `eth0` oppure `eth1`. E' possibile risolvere utilizzando `ifrename`, vedere [Rename network interfaces](/index.php/Rename_network_interfaces "Rename network interfaces"). E' anche possibile creare manualmente delle regole udev che assegnino alle interfacce nomi basati sull'interfaccia degli indirizzi MAC. Vedere [Persistent Device Names](/index.php/Udev#Network_device "Udev").

### Ottenere il nome corrente del dispositivo

Il nome attuale NIC può essere individuato con il tool *ip*.

 `$ ip addr | sed '/^[0-9]/!d;s/: <.*$//'` 
```

1: lo
2: eth1
3: eth0
4: firewire0
```

### Abilitare/disabilitare l'interfaccia

È possibili abilitare o disabilitare l'interfaccia di rete:

```
ip link set <interface> up/down

```

Controllare il risultato con `ip addr show dev eth0`. Ad esempio:

 `ip addr show dev eth0` 
```
   2: eth0: <BROADCAST,MULTICAST,PROMISC,UP,LOWER_UP> mtu 1500 qdisc vboxnetflt state UP qlen 1000
   [...]

```

## Configurare l'indirizzo IP

Ci sono due opzioni: l'assegnazione dinamica dell'indirizzo utilizzando DHCP oppure un indirizzo "statico" che non cambia. Vedere [Wikipedia:DHCP](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol "wikipedia:Dynamic Host Configuration Protocol") per maggiori informazioni.

### Indirizzo IP dinamico

#### Esecuzione manuale del Demone Client DHCP

Si noti che dhcpcd non è dhcpd.

 `dhcpcd eth0` 
```

  dhcpcd: version 5.1.1 starting 
  dhcpcd: eth0: broadcasting for a lease
  ... 
  dhcpcd: eth0: leased 192.168.1.70 for 86400 seconds 

```

Ed ora `ip addr show dev <interface>` dovrebbe mostrare il proprio indirizzo inet.

Per alcune persone, il pacchetto `dhclient` (disponibile in [extra]) ha funzionato dove`dhcpcd` ha fallito.

#### Esecuzione all'avvio di DHCP

In questo caso è necessario il pacchetto [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) (già disponibile nella maggior parte delle installazioni). Inoltre, è necessario editare `/etc/rc.conf` in questo modo:

```
interface="eth0"
address=
netmask=
gateway=

```

Va definita solo l'interfaccia, le altre opzioni saranno impostate tramite DHCP..

Se si utilizza DHCP e **non** si vuole che i server DNS vengano automaticamente assegnati ogni volta che si avvia la rete, assicurarsi di aggiungere all'ultima sezione del file `/etc/dhcpcd.conf` quanto segue:

```
nohook resolv.conf

```

Per evitare che dhcpcd aggiunga server di nomi di dominio al file resolve.conf, utilizzare l'opzione nooption in `/etc/dhcpcd.conf`:

```
nooption donmain_name_servers

```

Quindi aggiungere il proprio server DNS in `/etc/resolv.conf`.

Si può utilizzare il pacchetto [openresolv](https://www.archlinux.org/packages/?name=openresolv) per controllare molti processi tramite `/etc/resolv.conf` (ad esempio, [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) ed un client VPN). Per utilizzare [openresolv](https://www.archlinux.org/packages/?name=openresolv), non è necessaria alcuna configurazione aggiuntiva per [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd).

{{Nota|1=È possibile avere un indirizzo IP statico utilizzando [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd). È sufficiente modificare il file `/etc/conf.d/dhcpcd` e cercare qualcosa simile a (dove xxxx è l’indirizzo IP desiderato):

```
DHCPCD_ARGS="-q -s x.x.x.x"

```

### Indirizzo IP Statico

Ci sono vari motivi per cui si potrebbe voler assegnare indirizzi IP statici alla rete. Per esempio, si può ottenere un certo livello di prevedibilità. Oppure si potrebbe non volere che il demone dhcp venga sempre eseguito.

**Nota:** Se si condivide la connessione internet con un pc Windows senza un router, assicurarsi di utilizzare indirizzi IP statici su entrambi i computer, onde evitare problemi con la LAN.

In questo caso è necessario conoscere:

*   Indirizzo IP statico,
*   Subnet mask,
*   Indirizzo di broadcast,
*   Indirizzo IP del gateway,
*   Nome indirizzi IP del server,
*   Nome di dominio (se non si tratta di una LAN locale, nel qual caso si può mettere up).

Se la rete è privata, è sufficiente utilizzare un indirizzo IP del tipo 192.168.*.'*, una subnet mask 255.255.0.0 e un indirizzo di broadcast 192.168.255.255\. A meno che non si utilizzi un router l'indirizzo IP del gateway non è necessario. A questo punto, editare `/etc/rc.conf` in questo modo, sostituendo indirizzo IP, netmask, broadcast e gateway:

```
interface=eth0
address=192.68.0.2
netmask=255.255.255.0
broadcast=192.168.1.255
gateway=192.168.22.1

```

Editare il file `/etc/resolv.conf`, inserendo l'indirizzo IP del proprio name server ed il proprio dominio locale:

```
nameserver 61.23.173.5
nameserver 61.95.849.8
search example.com

```

**Nota:** Attualmente è possibile inserire massimo 3 righe di `nameserver`.

**Nota:** Coloro che vogliono visionare il rendimento/benchmark, possono dare un'occhiata a [GRC's DNS Benchmark](https://www.grc.com/dns/benchmark.htm) .

#### Assegnazione manuale

Si può assegnare l’indirizzo IP dalla console:

```
 # ip addr add <ip address>/<netmask> dev <interface>

```

Ad esempio:

```
 # ip addr add 192.168.1.2/24 dev eth0

```

Per altre opzioni, vedere: [ip(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ip.7)

Aggiungere il proprio gateway in questo modo:

```
 # ip route add default via <ip address>

```

(Sostituire <ip> con il proprio indirizzo IP del gateway

Ad esempio:

```
 # ip route add default via 192.168.1.1

```

Se si ottiene l'errore "No such process", significa che è necessario eseguire `# ip link set dev eth0 up`.

#### Calcolo indirizzi

E' possibile utilizzare *ipcalc* fornito dal pacchetto ipcalc package per calcolare l'IP broadcast, network, netmask, ed i range di host host per le configurazioni più avanzate. Ad esempio, è possiblie utilizzare l'ethernet tramite firewire per connettere un pc windows ad arch. Per la sicurezza e l'organizzazione della rete, è possibile posizionarli su una propria rete, configurare netmask e broadcast in modo che siano le uniche 2 macchine su di essa. Per mostrare gli indirizzi netmask e broadcast, si può utilizzare ipcalc, fornendo con l'IP arch del firewire nic 10.66.66.1, e specificando ipcalc, dovrebbe creare una rete di 2 soli host.

 `$ ipcalc -nb 10.66.66.1 -s 1` 
```
Address:   10.66.66.1
Netmask:   255.255.255.252 = 30
Network:   10.66.66.0/30
HostMin:   10.66.66.1
HostMax:   10.66.66.2
Broadcast: 10.66.66.3
Hosts/Net: 2                     Class A, Private Internet
```

## Caricare la configurazione

Per testare le configurazioni, riavviare il computer o, da root, eseguire:

 `rc.d restart network` 

Provare a pingare il gateway, il server DNS, l’ISP e altri siti Internet, in questo ordine, per rilevare eventuali problemi di collegamento lungo la strada, ad esempio:

 `ping -c 3 www.google.com` 

## Impostazioni aggiuntive

### ifplugd per laptops

[ifplugd](https://www.archlinux.org/packages/?name=ifplugd) nei [Official Repositories (Italiano)Repository Ufficiali](/index.php?title=Official_Repositories_(Italiano)Repository_Ufficiali&action=edit&redlink=1 "Official Repositories (Italiano)Repository Ufficiali (page does not exist)") è un demone che configura automaticamente il dispositivo Ethernet quando viene collegato il cavo e che sconfigura il dispositivo quando il cavo viene scollegato. Ciò è utile su portatili con schede di rete integrate, così verrà creata una configurazione solo quando si collegherà il cavo. Questo sistema può essere utilizzato anche quando si vuole riavviare la rete, senza riavviare il computer e senza utilizzare la shell.

Di default è configurato per funzionare per il dispositivo `eth0`. Questa ed altre impostazioni come i ritardi, possono essere configurati in `/etc/ifplugd/ifplugd.conf`.

[Avviare il demone ifplugd](/index.php/Daemon_(Italiano)#Avvio_e_blocco_manuale "Daemon (Italiano)") ed aggiungere `ifplugd` al proprio [DAEMONS array](/index.php/Daemon_(Italiano)#Esecuzione_automatica_all.27avvio "Daemon (Italiano)") di modo da farlo partire automaticamento all'avvio del sistema.

In alternativa, abilitando`net-auto-wired.service` ifplugd si dovrebbe avviare al boot, se si ha [netcfg](https://aur.archlinux.org/packages/netcfg/) installato, altrimenti è possibile utilizzare `ifplugd@eth0.service`.

### Bonding o LAG

Sarà necessario installare [ifenslave](https://www.archlinux.org/packages/?name=ifenslave) dai [Repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)"), così come il pacchetto [netcfg-bonding](https://aur.archlinux.org/packages/netcfg-bonding/) da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").

Modificare/creare ciascuno dei seguenti files:

```
/etc/network.d/bonded

```

```
  CONNECTION="bonding"
  INTERFACE="bond0"
  SLAVES="eth0 eth1"
  IP="dhcp"
  DHCP_TIMEOUT=10

```

```
/etc/rc.conf

```

```
  MODULES=(... bonding ...)

...
 interface=bond0 #commentare le altre linee (indirizzo,netmask,gateway,...)
...
 NETWORKS=(... bonded ...)
...

DAEMONS=(... net-profiles ...) #sostituire network 

```

**Nota:** Per cambiare la modalità bonding (di default è round robin), ad esempio in aggregazione dinamica del link:

Creare `/etc/modprobe.d/bonding.conf`:

```
/etc/modprobe.d/bonding.conf

```

```

options bonding mode=4
options bonding miimon=100

```
Per maggiori informazioni inerenti le differenti policy di bonding (ed impostazioni di altri driver) consultare l'[Linux Ethernet Bonding Driver HOWTO](http://sourceforge.net/projects/bonding/files/Documentation/).

Per attivare le nuove porte, eseguire il modprobe di `bonding`, fermare `network` ed avviare il servizio `net-profiles`:

```
 # modprobe bonding

```

```
 # rc.d stop network

```

```
 # rc.d start net-profiles

```

Per controllare lo stato:

```
 cat /proc/net/bonding/bond0

```

### Aliasing indirizzo IP

l'aliasing IP è il processo per l'aggiunta di più di un indirizzo IP all'interfaccia di rete. Così facendo, un nodo su una rete può avere connessioni multiple nella rete stessa, ciascuna con una funzione diversa.

Per utilizzare l'IP aliasing da [*netcfg*](/index.php/Netcfg_(Italiano) "Netcfg (Italiano)"), cambiare i comandi `POST_UP` e `PRE_DOWN` sul profilo dell'interfaccia di rete per configurare manualmente gli indirizzi IP aggiuntivi. Vedere [qui](https://bbs.archlinux.org/viewtopic.php?pid=1036395#p1036395) per maggiori dettagli.

#### Esempio

Sarà necessario [netcfg](https://aur.archlinux.org/packages/netcfg/), disponibile nei [Repository Ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)")

 `# pacman -S netcfg` 

Preparare la configurazione

```
/etc/network.d/mynetwork

```

```

CONNECTION='ethernet'
DESCRIPTION='Five different addresses on the same NIC.'
INTERFACE='eth0'
IP='static'
ADDR='192.168.1.10'
GATEWAY='192.168.1.1'
DNS=('192.168.1.1')
DOMAIN=''
POST_UP='x=0; for i in 11 12 13 14 ; do ip addr add 192.168.1.$i/24 brd 192.168.1.255 dev eth0 label eth0:$((x++)); done'
PRE_DOWN='for i in 11 12 13 14 ; do ip addr del 192.168.1.$i/24 dev eth0 ; done'

```

```
/etc/rc.conf

```

```
NETWORKS=(mynetwork)

...

DAEMONS=(... net-profiles ...)

```

### Cambiare MAC/hardware address

Non è più possibile cambiare il proprio MAC address tramite `/etc/rc.conf`. Vedere [MAC address spoofing](/index.php/MAC_address_spoofing "MAC address spoofing") per maggiori dettagli.

## Risoluzione dei problemi

### Scambio computer/modem via cavo

La maggior parte degli ISP (videotron for example) ha il modem via cavo configurato per riconoscere un solo PC client, attraverso il MAC Address della sua interfaccia di rete. Una volta che il modem via cavo ha acquisito il MAC Address del primo PC, o della relativa periferica, non risponderà in alcun modo ad un altro MAC Address. Pertanto, se si cambia un PC con un altro (o router), il nuovo PC (o router) non funzionerà con il modem via cavo, in quanto ha un MAC Address diverso dal precedente. Per effettuare il reset del modem via cavo in modo che riconosca il nuovo PC, è necessario spegnerlo e riaccenderlo. Una volta che il modem via cavo si è riavviato ed è ritornato completamente in linea (le spie luminose sono stabili), riavviare il nuovo computer in modo da effettuare una nuova richiesta DHCP, o effettuarla manualmente.

Se questo metodo non funziona, è necessario clonare il MAC Address del pc originario. Vedere quindi [#Cambiare MAC/hardware address](#Cambiare_MAC.2Fhardware_address).

### Il problema del TCP Window Scaling

I pacchetti TCP contengono nell'header un campo "window" che indica la quantità di dati che deve restituire l'altro host. Questo campo è di 16 bit, dato che la dimensione della finestra è al massimo 64kb. I pacchetti TCP vengono mantenuti in cache per un certo tempo e, se la memoria è (o era) limitata, è probabile che l'host la finisca rapidamente.

Nel 1992, quando cominciò ad essere disponibile molta memoria, per migliorare la situazione, fu scritta la [RFC 1323](http://www.faqs.org/rfcs/rfc1323.html): fu introdotto in "Window Scaling". Il valore "window", presente in tutti i pacchetti, viene modificato da uno "Scale Factor" definito una sola volta all'inizio della connessione. Questo campo, di 8 bit, permette alla finestra di essere fino a 32 volte più grande dei 64Kb iniziali.

Sembra che alcuni router e firewall riscrivano lo Scale Factor a 0 che causa "incomprensioni" tra gli host.

Il kernel 2.6.17 ha introdotto un nuovo algoritmo che genera Scale Factors più alti, in modo tale da rendere il problema di questi router e firewall virtualmente più visibile.

La connessione, in questi casi, si interrompe o è, al più, molto lenta.

#### Come diagnosticare questo problema?

Prima di tutto chiariamo: è molto difficile. In alcuni casi, non sarà possibile effettuare connessioni TCP (HTTP, FTP, ...), in altri sarà possibile comunicare solo con alcuni host (molto pochi).

Quando si ha questo problema, l'output di `dmesg` è ok, i log sono puliti e `ip addr` riporta una configurazione corretta... quindi sembra tutto normale.

Se non è possibile raggiungere nessun sito Web, ma è possibile pingare alcuni host, probabilmente si è incappati in questo problema: il ping utilizza il protocollo ICMP e non è affetto da problemi TCP.

Si può provare ad utilizzare Wireshark. Si possono vedere comunicazioni UDP e ICMP che avvengono correttamente e le connessioni TCP che non vanno a buon fine (solo verso host 'esterni').

#### Come risolverlo? (La strada sbagliata)

Per risolvere il problema, si può cambiare il valore tcp_rmem, su cui si basa il calcolo dello Scale Factor. Sebbene dovrebbe funzionare per la maggior parte degli host, non è sicuro che funzioni in tutti i casi, specialmente per host molto distanti.

```
echo "4096 87380 174760" > /proc/sys/net/ipv4/tcp_rmem

```

#### Come risolverlo? (Il metodo corretto)

Semplicemente, disabilitare il Window Scaling. Anche se è una caratteristica carina, può rivelarsi scomoda se non si può sistemare il router malfunzionante. Ci sono diversi metodi per disabiltare il Window Scaling, e sembra che il più sicuro (che funziona sui kernel più recenti) sia aggiungere la seguente linea in `/etc/sysctl.d/99-disable_window_scaling.conf`: (vedere anche [sysctl](/index.php/Sysctl "Sysctl"))

```
net.ipv4.tcp_window_scaling = 0

```

#### Come risolverlo? (Il metodo migliore)

Questo problema è causato da router/firewall malfunzionanti, quindi vanno cambiati.

#### Ulteriori informazioni

Questa sezione si basa sull'articolo LWN [TCP window scaling and broken routers](http://lwn.net/Articles/92727/) e sull’articolo di Kernel Trap : [Window Scaling on the Internet](http://kerneltrap.org/node/6723).

Altre discussioni pertinenti sono presenti su LKML.

### Problema No Link / WOL schede Realtek

Gli utenti che hanno schede di rete con chipset Realtek 8168/8169/8101/8111 possono avere il problema che l'interfaccia sembri disabilitata in fase di avvio e il led sia spento. Questo, di solito, accade in caso di dual boot insieme a Windows. Sembra che il problema sia dovuto all' utilizzo dei driver ufficiali Relatek (qualsiasi versione successiva al Maggio 2007) in ambiente Windows. Questi driver disabiltano il Wake-on-Lan in fase di spegnimento di Windows, lasciandola in questo modo finchè Windows non viene riavviato. Per verificare se il problema affligge anche la nostra scheda semplicemente notando che il led dell'interfaccia rimane spento a meno che non si avvii Windows. In condizioni normali il led dovrebbe essere sempre acceso finchè il Pc è acceso, anche durante il POST. Questo problema affliggerà tutti i sistemi che non hanno driver aggiornati (esempio i live CD). Ecco alcune possibili soluzioni al problema:

#### Metodo 1 - Ripristino driver Windows

E' possibile fare un ripristino del driver Windows alla versione fornita da Microsoft (se disponibile), o ripristinare una versione del driver Realtek a precedente al Maggio 2007 (che probabilmente si trova sul CD di installazione dell'hardware).

#### Metodo 2 - Abilitare il Wake on Lan nel driver Windows

Probabilmente il metodo migliore e più veloce è cambiare questa impostazione nel driver Windows. Questo metodo dovrebbe anche risolvere il problema non soltanto per Arch, ma anche per altri sistemi, come Live CD ed altri. In Windows, sotto "Gestione Periferiche", trovate la scheda Realtek e selezionatela. Nella scheda "Avanzate" abilitate "Wake-on-lan after shutdown".

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

**Nota:** I nuovi driver Realtek di Windows (testato con Realtek 8111/8169 Driver LAN v5.708.1030.2008, datato 2009/01/22, disponibile da GIGABYTE) potrebbero fare riferimento a questa opzione in modo leggermente diverso, come *Shutdown Wake-On-LAN --> Enable*. Sembra che cambiare in `Disable` non produca alcun effetto (si noterà che la luce Link rimarrà accesa fino alla chiusura di Windows). Una soluzione, non proprio pulitissima, è avviare Windows e semplicemente resettarlo (eseguendo un brutale riavvio/spegnimento), non dando quindi al driver di Windows la possibilità di disabilitare la LAN. La luce Link rimarrà accesa e l’adattatore LAN rimarrà accessibile dopo il POST – cioè fino a quando non si avvierà Windows e lo si spegnerà correttamente.

#### Metodo 3 - Aggiornare il driver Linux Realtek

Scaricare ed installare una nuova versione del driver dal sito ufficiale Realtek. (non testato ma dovrebbe risolvere il problema).

#### Metodo 4 - Abilitare *LAN Boot ROM* nel BIOS/CMOS

Sembra che abilitando nel BIOS/CMOS l’impostazione *Integrated Peripherals --> Onboard LAN Boot ROM* si riattivi il chip Realtek LAN all’avvio del sistema, nonostante il driver di Windows lo disabiliti allo spegnimento.
<small>Ciò è stato testato più volte e con successo con una GIGABYTE GA-G31M-ES2L su un BIOS versione F8 rilasciato il 2009/02/05\. Formato data YMMV.</small>

### Problema con DLink G604T/DLink G502T DNS

Gli utenti che posseggono un router DLink G604T/DLink G502T, utilizzano DHCP ed hanno un firmware v2.00+ (in genere utenti con firmware AUS), possono avere problemi con alcuni programmi nel risolvere i DNS. Uno di questi programmi, sfortunatamente, è pacman. Fondamentalmente il problema è che il router, in certe situazioni, non invia correttamente i DNS al DHCP, ciò fa sì che i programmi provino a connettersi al server con IP 1.0.0.0 ricevendo un errore di connessione scaduta.

#### Come diagnosticare il problema

Il metodo migliore per diagnosticare il problema è utilizzare Firefox/Konqueror/links/seamonkey ed abilitare wget per pacman. Se questa è una nuova installazione di Arch Linux, allora si può prendere in considerazione l’idea di installare `links` attraverso il live CD.

Prima di tutto, abilitare wget per pacman (in modo da ricevere informazioni inerenti il download dei pacchetti da parte di pacman). Aprire `/etc/pacman.conf` con l’editor di testo che si preferisce e decommentare la seguente linea (eliminare il cancelletto #):

```
XferCommand=/usr/bin/wget --passive-ftp -c -O %o %u

```

Mentre si edita il file `/etc/pacman.conf` controllare che il mirror predefinito che pacman utilizza per il download dei pacchetti.

Ora aprire il mirror predefinito in un browser Internet per verificare se esso funziona. Se funziona, eseguire `pacman -Syy` (altrimenti scegliere un altro mirror ed impostarlo come predefinito di pacman), se si ottiene qualcosa di simile a quanto segue (notare 1.0.0.0):

```
ftp://mirror.pacific.net.au/linux/archlinux/extra/os/i686/extra.db.tar.gz                                                            
           => `/var/lib/pacman/community.db.tar.gz.part'
Resolving mirror.pacific.net.au... 1.0.0.0

```

allora molto probabilmente si tratta di questo problema. 1.0.0.0 significa che non è stato possibile risolvere i DNS, perciò essi vanno aggiunti a `/etc/resolv.conf`.

#### Come risolvere il problema

Fondamentalmente bisogna aggiungere manualmente i server DNS al file `/etc/resolv.conf`, il problema è che DHCP elimina automaticamente e sostituisce il file all'avvio, perciò è necessario editare `/etc/conf.d/dhcpcd` e modificare i flag per impedire che ciò accada:

Quando si apre il file `/etc/conf.d/dhcpcd`, si dovrebbe vedere qualcosa di simile a quanto segue:

```
DHCPCD_ARGS="-t 30 -h $HOSTNAME"

```

Aggiungere il flag –R agli argomenti, ad esempio:

```
DHCPCD_ARGS="-R -t 30 -h $HOSTNAME"

```

**Nota:** Se si utilizza [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) >=4.0.2 il flag `–R` è obsoleto. Si prega di vedere la sezione [Per l'indirizzo IP assegnato da DHCP](#Per_l.27indirizzo_IP_assegnato_da_DHCP) per informazioni su come utilizzare e modificare il file `/etc/resolv.conf`

Salvare e chiudere il file, poi aprire `/etc/resolv.conf`. Si dovrebbe visualizzare un singolo nameserver (molto probabilmente 10.1.1.1). Questo è il gateway al router, a cui è necessario per ottenere i server DNS del proprio ISP. Incollare l'indirizzo IP nel browser ed effettuare il login al proprio router. Andando nella sezione DNS si dovrebbe vedere un indirizzo IP alla voce Primary DNS Server (Server DNS preferito), copiarlo ed incollarlo come voce nameserver, **SOPRA** il gateway corrente.

Ad esempio, il file `/etc/resolv.conf` dovrebbe essere simile a:

```
nameserver 10.1.1.1

```

Se il proprio DNS primario è 211.29.132.12, cambiare `/etc/resolv.conf` in:

```
nameserver 211.29.132.12
nameserver 10.1.1.1

```

Ora riavviare il demone di rete eseguendo `{ic` e `pacman -Syy`. Se si sincronizza correttamente con il server, allora il problema è risolto.

#### Maggiori informazioni

Questo è il forum whirlpool (Comunità Australiana ISP) che parla del problema e suggerisce la medesima soluzione

```
[http://forums.whirlpool.net.au/forum-replies-archive.cfm/461625.html](http://forums.whirlpool.net.au/forum-replies-archive.cfm/461625.html)

```

### Controllo problemi DHCP prima del rilascio dell'IP

Il probleme potrebbe presentarsi quando DHCP ottiene un'assegnazione errata dell'IP. Ad esempio quando due router sono collegati insieme tramite VPN. Il router connesso tramite VPN può assegnare un indirizzo IP. C’è un modo per risolvere il problema. In una console, da root, rilasciare l'indirizzo IP:

```
 # dhcpcd -k

```

Quindi richeiderne uno nuovo:

```
 # dhcpcd 

```

Potrebbe essere necessario eseguire questi due comandi più volte.

## Wiki Correlati

[Samba (Italiano)](/index.php/Samba_(Italiano) "Samba (Italiano)")