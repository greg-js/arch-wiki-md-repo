OpenNTPD (parte del progetto OpenBSD) è un demone che può essere usato per sincronizzare l'orologio di sistema con time servers in internet utilizzando il Network Time Protocol, e può anche funzionare esso stesso come un time server, se necessario.

**Attenzione:** *OpenNTPD* non è attualmente mantenuto per Linux (leggere [questo thread](https://bbs.archlinux.org/viewtopic.php?id=68627)): gli utenti interessati alle sue funzionalità farebbero meglio ad usare [NTPd](/index.php/NTPd_(Italiano) "NTPd (Italiano)").

## Contents

*   [1 Installazione](#Installazione)
*   [2 Rendere openntpd dipendente dall'accesso al network](#Rendere_openntpd_dipendente_dall.27accesso_al_network)
    *   [2.1 Usando netcfg](#Usando_netcfg)
    *   [2.2 Usando l'invio di NetworkManager](#Usando_l.27invio_di_NetworkManager)
    *   [2.3 Usando wicd](#Usando_wicd)
    *   [2.4 Usando l'hook dhcpcd](#Usando_l.27hook_dhcpcd)
*   [3 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [3.1 Errore nella regolazione dell'ora](#Errore_nella_regolazione_dell.27ora)
    *   [3.2 Aumenti del tempo](#Aumenti_del_tempo)
    *   [3.3 Inizializzazione Fallita](#Inizializzazione_Fallita)
*   [4 Articoli correlati](#Articoli_correlati)
*   [5 Link esterni](#Link_esterni)

## Installazione

[OpenNTPD](http://www.openntpd.org/) può essere installato dal repository [community]:

```
# pacman -S openntpd

```

La configurazione di base è già sufficiente se si vuole solamente sincronizzare l'ora del computer locale. Per impostazioni maggiormente dettagliate, il file `/etc/ntpd.conf` deve essere editato:

Per sincronizzarsi ad un particolare server, decommentare e inserire le direttive del "server". Si possono trovare gli URL dei server della propria area in [www.pool.ntp.org/zone/@](http://www.pool.ntp.org/zone/@).

```
server ntp.example.org

```

Le direttive "servers" lavorano nella stessa maniera della direttiva "server", ma, nel caso in cui il nome del DNS risolvesse indirizzi IP multipli, TUTTI loro sarebbero sincronizzati. Quello di base, "pool.ntp.org" è funzionante e dovrebbe andare bene nella maggioranza dei casi.

```
pool.ntp.org

```

Qualsiasi numero di direttive di "server" o "servers" possono essere usati.

Se si desidera che il proprio computer sul quale è lanciato OpenNTPD sia anche un server d'orario, semplicemente decommentare ed editare la direttiva "listen".

Ad esempio:

```
listen on *

```

resterà in ascolto su tutte le interfacce, e

```
listen on 127.0.0.1

```

resterà in ascolto solo sull'interfaccia loopback.

Il proprio server del tempo comincerà ad offrire il servizio solo dopo essersi sincronizzato a un'alta risoluzione. Ciò può richiedere ore, o giorni, dipende dall'accuratezza del proprio sistema.

Se si desidera lanciare OpenNTPD all'avvio, aggiungere `openntpd` alla lista DAEMONS nel proprio `/etc/rc.conf` dopo il demone del proprio network.

```
DAEMONS=(syslog-ng network **openntpd** ...)

```

Se openntpd è usato solamente per impostare l'ora locale del proprio sistema, può essere tranquillamente messo in background.

```
DAEMONS=(syslog-ng network **@openntpd** ...)

```

Per vedere lo stato della sincronizzazione NTP, si visiti `/var/log/daemon.log` e si cerchino le linee con "ntpd".

OpenNTPD aggiusta l'orologio con piccole variazioni alla volta. Ciò è stato fatto per evitare improvvisi, grandi fluttuazioni di tempo nel proprio sistema, che potrebbero comportare problemi a servizi di sistema (ad esempio, quelli relativi a cron). Perciò, ci può volere un pò prima di correggere l'orario.

Se l'orologio non è funzionante per più di 180 secondi si può provare con "`ntpd -s -d`" lanciato in una console. Se ntpd è già avviato, si può semplicemente riavviarlo con `sudo /etc/rc.d/openntpd restart`, dal momento che il pacchetto Arch di openntpd usa la variabile "-s" di base. Si veda `man ntpd` per maggiori informazioni. Si può anche impostare l'[orologio di sistema](/index.php/Time#Time_Set "Time") il più vicino possibile all'ora attuale e quindi permettere a OpenNTPD di completare la sintonizzazione del tempo.

## Rendere openntpd dipendente dall'accesso al network

Nel caso si abbia un accesso al network intermittente (si è su un laptop, si utilizza dial-up, ecc.), non ha senso avere `openntpd` avviato come demone di sistema all'avvio. Qui ci sono alcune maniere per controllare `openntpd` basandosi sulla connessione network presente. Queste istruzioni dovrebbero funzionare anche per `ntpd` come spiegato più sotto.

### Usando netcfg

Se si sta utilizzando netcfg, si può anche avviare/fermare openntpd come un comando POST_UP/PRE_DOWN nel proprio profilo network:

```
POST_UP="/etc/rc.d/openntpd start || true"
PRE_DOWN="/etc/rc.d/openntpd stop || true"

```

Naturalmente, si dovrà specificare ciò manualmente per ogni profilo network.

### Usando l'invio di NetworkManager

OpenNTPD può essere acceso/spento a seconda della connessione internet attraverso l'uso degli [NetworkManager's dispatcher scripts](/index.php/NetworkManager_(Italiano)#Servizi_di_rete_con_NetworkManager_Dispatcher "NetworkManager (Italiano)"). E' possibile installare gli script necessari dal repo [community]:

```
# pacman -S networkmanager-dispatcher-openntpd

```

### Usando wicd

Queste istruzioni richiedono wicd 1.7.0 o più recente, che è disponibile nei repository standard di Arch. Si necessita anche di avere l'accesso alla scrittura al file `/etc/wicd/scripts`.

**Note:** Ricordarsi di rendere questi due script eseguibili usando `chmod`

Si crei uno script shell dentro `/etc/wicd/scripts/postconnect/openntpd-start.sh` con il seguente contenuto:

```
#!/bin/sh
/etc/rc.d/openntpd start

```

In maniera del tutto simile, si crei un altro script di shell dentro `/etc/wicd/scripts/predisconnect/openntpd-stop.sh` con il contenuto:

```
#!/bin/sh
/etc/rc.d/openntpd stop

```

### Usando l'hook dhcpcd

Un'altra possibilità è quella di usare l'hook dhcpcd per avviare e fermare openntpd. Quando dhcpcd riconosce un cambio nello stato lancerà lo script seguente:
`/etc/dhcpcd.enter-hook`
`/usr/lib/dhcpcd/dhcpcd-hooks/*`
`/etc/dhcpcd.exit-hook`

L'esempio seguente usa `/etc/dhcpcd.exit-hook` per avviare e fermare openntpd a seconda dello stato di dhcp:

```
[ "$interface" != "eth0" ] && exit 0

if $if_up; then
    pgrep ntpd &> /dev/null || /etc/rc.d/openntpd start
elif $if_down; then
    pgrep ntpd &> /dev/null && /etc/rc.d/openntpd stop
fi

```

## Risoluzione dei problemi

### Errore nella regolazione dell'ora

Se si scopre il proprio orario impostato in maniera scorretta e nei log è presente la dicitura:

```
openntpd adjtime failed: Invalid argument

```

Si provi:

```
ntpd -s -d

```

Questa è anche la maniera in cui si potrebbe voler sincronizzare manualmente il proprio sistema.

### Aumenti del tempo

Avviando *openntpd* in background può portare ad errori di sincronizzazione tra l'ora attuale e l'orario salvato nel proprio computer. Se si scopre un aumento di differenza temporale tra l'orologio del desktop e l'ora attuale, si provi ad avviare il demone *openntpd* normalmente e non in background.

### Inizializzazione Fallita

Openntpd potrebbe fallire ad avviarsi correttamente se viene avviato prima che il proprio network sia correttamente configurato. In alcuni casi si potrebbe voler rimuovere `openntpd` dalla lista DAEMONS in `/etc/rc.conf` e aggiungere la linea seguente in `/etc/rc.local`:

```
(sleep 300 && /etc/rc.d/openntpd start) &

```

**Note:** Questo metodo è un'alternativa ai quattro metodi elencati [sopra](#Rendere_openntpd_dipendente_dall.27accesso_al_network). Gli altri metodi sono preferibili e lavorano meglio. Usare questo metodo solo come ultima risorsa.

Ciò farà sì che il sistema aspetti 5 minuti prima di avviare openntpd, in modo tale da dare un tempo sufficiente al sistema per configurare la connessione. Se le proprie impostazioni network cambiano spesso, si potrebbe anche considerare di riavviare il demone regolarmente tramite cron.

## Articoli correlati

*   [Network Time Protocol daemon](/index.php/Network_Time_Protocol_daemon_(Italiano) "Network Time Protocol daemon (Italiano)")

## Link esterni

*   [http://www.openntpd.org](http://www.openntpd.org)