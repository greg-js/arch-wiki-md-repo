Iptables è un potente [firewall](/index.php/Firewalls_(Italiano) "Firewalls (Italiano)") integrato nel kernel Linux ed è una parte del progetto [netfilter](https://en.wikipedia.org/wiki/it:Netfilter oppure una delle [GUI](/index.php/Firewalls_(Italiano)#iptables_GUIs "Firewalls (Italiano)"). iptables è utilizzato per gli [IPv4](https://en.wikipedia.org/wiki/it:IPv4 "wikipedia:it:IPv4") mentre ip6tables è usato per gli [IPv6](https://en.wikipedia.org/wiki/it:IPv6 "wikipedia:it:IPv6").

## Contents

*   [1 Installazione](#Installazione)
*   [2 Concetti di base](#Concetti_di_base)
    *   [2.1 tabelle](#tabelle)
    *   [2.2 catene](#catene)
    *   [2.3 destinazione](#destinazione)
    *   [2.4 moduli](#moduli)
*   [3 Configurazione](#Configurazione)
    *   [3.1 Da linea di comando](#Da_linea_di_comando)
    *   [3.2 Salvare i contatori](#Salvare_i_contatori)
    *   [3.3 Guide](#Guide)
*   [4 Log](#Log)
    *   [4.1 Limitare le dimensioni del log](#Limitare_le_dimensioni_del_log)
    *   [4.2 syslog-ng](#syslog-ng)
    *   [4.3 ulogd](#ulogd)
*   [5 Ulteriori risorse](#Ulteriori_risorse)

## Installazione

**Nota:** Il proprio kernel dovrà essere compilato con il supporto per iptables. Tutti i kernel stock di Arch Linux hanno il supporto per iptables.

Per prima cosa, installare il pacchetto [iptables](https://www.archlinux.org/packages/?name=iptables) dai [repository ufficiali](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)"):

Successivamente, abilitare ed avviare il file service di `iptables` per systemd:

```
# systemctl enable iptables
# systemctl start iptables

```

Se si desidera il supporto per IPv6, abilitare ed avviare il file service di `ip6tables` per systemd:

```
# systemctl enable ip6tables
# systemctl start ip6tables

```

## Concetti di base

### tabelle

iptables contiene quattro tabelle: raw, filter, nat e mangle.

### catene

Le catene sono utilizzate per indicare una serie di regole. Un pacchetto viene comparato dall'inizio della catena fino a che non soddisfa una regola. Ci sono tre catene principali: `INPUT, OUTPUT` e `FORWARD`. Tutti i pacchetti generati dal sistema ed in uscita, passano attraverso la catena `OUTPUT`, tutti i pacchetti in entrata e destinati al sistema stesso passano attraverso la catena `INPUT`, mentre i pacchetti che transitano per il sistema ma sono destinati ad altri sistemi passano dalla catena `FORWARD`. Queste catene hanno destinazioni di default nel caso nessuna regola venga soddisfatta. Catene personalizzate dagli utenti possono essere aggiunte per aumentare l'efficienza delle regole.

### destinazione

Una destinazione è il risultato che si ottiene quando un pacchetto soddisfa una regola. Le destinazioni sono specificate mediante l'uso di "jump" (-j). Le destinazioni più comuni sono ACCEPT, DROP, REJECT oppure LOG.

### moduli

Esistono diversi moduli che possono essere usati per rafforzare iptables, come connlimit, conntrack, limit e recent. Questi moduli forniscono funzionalità aggiuntive per permettere l'uso di regole di filtraggio più complesse.

## Configurazione

### Da linea di comando

Sarà possibile controllare le regole in uso ed il numero di pacchetti che hanno soddisfatto le regole usando il comando:

 `# iptables -nvL` 
```
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination   

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination    

Chain OUTPUT (policy ACCEPT 0K packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination
```

Se l'output ottenuto è simile a quello nell'esemprio, allora non sono state configurate regole.

Le regole possono essere resettate alle impostazioni di default usando questi comandi:

```
# iptables -P INPUT ACCEPT
# iptables -P FORWARD ACCEPT
# iptables -P OUTPUT ACCEPT
# iptables -F
# iptables -X

```

### Salvare i contatori

**Nota:** Questa procedura non funzionerà se si utilizza [systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)"). Sarà necessario modificare i file service di systemd.

Sarà possibile, opzionalmente, salvare i contatori di pacchetti e dei byte. Per poterlo fare, modificare il file `/etc/rc.d/iptables`

Nella sezione **save)** cambiare la linea:

```
/usr/sbin/iptables-save > $IPTABLES_CONF

```

in

```
/usr/sbin/iptables-save -c > $IPTABLES_CONF

```

Nella sezione **stop)**, aggiugnere le seguenti linee per salvare prima dello stop del demone:

```
stop)
     $0 save
     sleep 2

```

Nella sezione **start)**, cambiare la linea:

```
/usr/sbin/iptables-restore < $IPTABLES_CONF

```

in

```
/usr/sbin/iptables-restore -c < $IPTABLES_CONF

```

e salvare il file.

### Guide

*   [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall")
*   [Router](/index.php/Router "Router")

## Log

La destinazione LOG può essere utilizzata per registrare i pacchetti che soddisfano una regola. Diversamente dalle altre destinazioni come ACCEPT o DROP, il pacchetto continua a muoversi sulla catena dopo essere passato dalla destinazione LOG. Questo significa che per registrare tutti i pacchetti bloccati, sarà necessario aggiungere una regola duplicata con destinazione LOG prima di ogni regola con destinazione DROP. Dato che questo riduce l'efficienza e rende le cose meno semplici, una catena LOGDROP potrà essere creata al suo posto.

```
## /etc/iptables/iptables.rules

*filter
:INPUT DROP [0:0]
:FORWARD DROP [0:0]
:OUTPUT ACCEPT [0:0]

... altre catene definite dall'utente ..

## catena LOGDROP
:LOGDROP - [0:0]

-A LOGDROP -m limit --limit 5/m --limit-burst 10 -j LOG
-A LOGDROP -j DROP

... regole ...

## effettua il log ED effettua il drop dei pacchetti che soddisfano questa regola:
-A INPUT -m state --state INVALID -j LOGDROP

... altre regole ...

```

### Limitare le dimensioni del log

Il modulo limit viene usato per impedire che il log di iptables cresca troppo o causi inutili scritture sul disco. Senza usare limiti, un attaccante potrebbe riempire il disco (oppure la sola partizione `/var`) facendo scrivere log ad iptables.

**-m limit** viene usato per attivare il modulo limit. Si può utilizzare l'opzione --limit per impostare un lasso di tempo medio, l'opzione --limit-burst serve per impostare il limite di pacchetti per i log. Ad esempio:

```
-A LOGDROP -m limit --limit 5/m --limit-burst 10 -j LOG

```

Questo aggiunge una regola alla catena LOGDROP che registrerà nel log tutti i pacchetti che passano da essa. I primi 10 pacchetti verranno registrati, e dopo di essi solo 5 pacchetti per minuto verranno registrati. Il "limit-burst" viene ripristinato ogni volta che il non viene superato il "tempo di limit".

### syslog-ng

Presumendo che si utilizzi [syslog-ng](/index.php/Syslog-ng "Syslog-ng"), come di default su Archlinux, è possibile controllare dove sarà salvato il log di iptables in questo modo:

```
filter f_everything { level(debug..emerg) and not facility(auth, authpriv); };

```

in

```
filter f_everything { level(debug..emerg) and not facility(auth, authpriv) and not filter(f_iptables); };

```

Questo fermerà il log di `iptables` nel file `/var/log/everything.log`.

Se si desidera che i log di iptables vadano in un file diverso da `/var/log/iptables.log`, basterà modificare il valore di destinazione di d_iptables (sempre nel file `syslog-ng.conf`)

```
destination d_iptables { file("/var/log/iptables.log"); };

```

### ulogd

[ulogd](http://www.netfilter.org/projects/ulogd/index.html) è uno demone eseguito in userspace il suo scopo è quello di effettuare il log dei pacchetti per netfilter, questo demone può rimpiazzare la destinazione di default LOG. Il pacchetto [ulogd](https://www.archlinux.org/packages/?name=ulogd) è disponibile nel repository `[community]`

## Ulteriori risorse

[Wikipedia:iptables](https://en.wikipedia.org/wiki/iptables "wikipedia:iptables")

*   [Sito ufficiale di iptables](http://www.netfilter.org/projects/iptables/index.html)
*   [iptables Tutorial 1.2.2](http://www.frozentux.net/iptables-tutorial/iptables-tutorial.html) by Oskar Andreasson
*   [iptables Debian](http://wiki.debian.org/iptables) Wiki di Debian