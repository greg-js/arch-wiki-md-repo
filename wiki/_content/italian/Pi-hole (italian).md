Articoli correlati

*   [Dnsmasq](/index.php/Dnsmasq "Dnsmasq")
*   [Lighttpd](/index.php/Lighttpd "Lighttpd")
*   [Linux_Containers](/index.php/Linux_Containers "Linux Containers")
*   [Nginx](/index.php/Nginx "Nginx")
*   [OpenVPN](/index.php/OpenVPN "OpenVPN")

Pi-hole è un progetto basato su script di shell che gestisce liste di blocco di pubblicità e malware conosciuti e interagisce trasparentemente con dnsmasq per reindirizzare ogni richiesta verso un sostituto. Pi-hole rimpiazza il tuo router come DNS di rete e quindi tutti le richieste saranno gestire da lui senza il bisogno di installare nulla sul lato client. Questa configurazione implementa efficacemente il blocco della pubblicità a livello di rete (es. tutti gli apparati connessi). Il pacchetto offre una webUI ben fatta (unitamente ad una interfaccia CLI) ed è particolarmente leggero e scalabile.

## Contents

*   [1 Pi-hole Server](#Pi-hole_Server)
    *   [1.1 Installazione](#Installazione)
    *   [1.2 Configurazione iniziale](#Configurazione_iniziale)
        *   [1.2.1 Dnsmasq](#Dnsmasq)
        *   [1.2.2 Web Server](#Web_Server)
            *   [1.2.2.1 Lighttpd](#Lighttpd)
            *   [1.2.2.2 Nginx](#Nginx)
        *   [1.2.3 FTL](#FTL)
    *   [1.3 Configurazione del router e di Pi-hole](#Configurazione_del_router_e_di_Pi-hole)
        *   [1.3.1 Metodo consigliato](#Metodo_consigliato)
        *   [1.3.2 Metodo alternativo](#Metodo_alternativo)
            *   [1.3.2.1 Metodo automatico: Impostare il server DNS Server nelle impostazioni del router](#Metodo_automatico:_Impostare_il_server_DNS_Server_nelle_impostazioni_del_router)
            *   [1.3.2.2 Metodo manuale: Configura manualemente il DNS per ogni tuo dispositivo](#Metodo_manuale:_Configura_manualemente_il_DNS_per_ogni_tuo_dispositivo)
        *   [1.3.3 Metodo Pi-hole centrico](#Metodo_Pi-hole_centrico)
    *   [1.4 Usare Pi-hole attraverso OpenVPN](#Usare_Pi-hole_attraverso_OpenVPN)
*   [2 Pi-hole Standalone](#Pi-hole_Standalone)
    *   [2.1 Installazione](#Installazione_2)
    *   [2.2 Configurazione iniziale](#Configurazione_iniziale_2)
        *   [2.2.1 Dnsmasq](#Dnsmasq_2)
        *   [2.2.2 Configurare la risoluzione dei nomi](#Configurare_la_risoluzione_dei_nomi)
            *   [2.2.2.1 Manualmente](#Manualmente)
            *   [2.2.2.2 Openresolve](#Openresolve)
*   [3 Usare Pi-hole](#Usare_Pi-hole)
    *   [3.1 Gestione dei DNS di Pi-hole](#Gestione_dei_DNS_di_Pi-hole)
    *   [3.2 Aggiornamento forzato della lista dei domini pubblicitari](#Aggiornamento_forzato_della_lista_dei_domini_pubblicitari)
    *   [3.3 Proteggere lìaccesso all'interfaccia web (solo pacchetto server)](#Proteggere_l.C3.ACaccesso_all.27interfaccia_web_.28solo_pacchetto_server.29)
    *   [3.4 Disabilitare temporaneamente Pi-hole](#Disabilitare_temporaneamente_Pi-hole)
*   [4 Risorse](#Risorse)

## Pi-hole Server

### Installazione

Installa [pi-hole-ftl](https://aur.archlinux.org/packages/pi-hole-ftl/) e [pi-hole-server](https://aur.archlinux.org/packages/pi-hole-server/).
Il pacchetto Pi-hole server installa 2 timers (e relativi servizi), entrambi abilitati staticamente:

*   pi-hole-gravity.timer aggiornerà settimanalmente la lista nera dei server di Pi-hole.
*   pi-hole-logtruncate.timer ripulirà giornalmente il log delle richieste LAN.

Se non dovessi essere d'accordo con le temporizzazioni predefinite dei timers (ereditate dal progetto principale) puoi, ovviamente, modificarli o evitare che vengano eseguiti mascherandoli.
Devi farli partire manualmente o semplicemente riavvia a configurazione terminata.

### Configurazione iniziale

#### Dnsmasq

Assicurati che la seguente riga in `/etc/dnsmasq.conf` sia non commentata:

 `/etc/dnsmasq.conf` 
```
[...]
conf-dir=/etc/dnsmasq.d/,*.conf

```

**Warning:** Se già usi dnsmasq, dalla versione 3.0 di Pi-hole FTL è richiesto il parametro `log-queries=extra`.

Abilita `dnsmasq.service` e ri/avvia il servizio.

#### Web Server

Opzionalmente, è possibile scegliere un server web per usare l'interfaccia amministrativa di Pi-hole.

**Note:** Pi-hole non richiede forzatamente l'uso dell'interfaccia web in quanto molti comandi sono disponibili via CLI.

File di configurazione già funzionanti sono forniti sia per [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) che per [nginx](https://www.archlinux.org/packages/?name=nginx). Altri server web possono tranquillamente eseguire l'interfaccia web, ma non sono al momento supportati.

Installa [php-sqlite](https://www.archlinux.org/packages/?name=php-sqlite) e abilita le necessarie estensioni di seguito elencate:

 `/etc/php/php.ini` 
```
extension=pdo_sqlite
[...]
extension=sockets.so
extension=sqlite3
```

Per ragioni di sicurezza, se vuoi popolare la direttiva [PHP open_basedir](/index.php/PHP#Configuration "PHP"), l'interfaccia web di amministrazione di Pi-hole necessita l'accesso ai seguenti file e cartelle:

```
 /srv/http/pihole:/run/pihole-ftl/pihole-FTL.port:/run/log/pihole/pihole.log:/run/log/pihole-ftl/pihole-FTL.log:/etc/pihole:/etc/hosts:/etc/hostname:/etc/dnsmasq.d/02-pihole-dhcp.conf:/etc/dnsmasq.d/03-pihole-wildcard.conf:/etc/dnsmasq.d/04-pihole-static-dhcp.conf:/proc/meminfo:/proc/cpuinfo:/sys/class/thermal/thermal_zone0/temp:/tmp

```

##### Lighttpd

Installa [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) e [php-cgi](https://www.archlinux.org/packages/?name=php-cgi).

Copia il file di configurazione fornito dal pacchetto:

```
# cp /usr/share/pihole/configs/lighttpd.example.conf /etc/lighttpd/lighttpd.conf

```

Abilita `lighttpd.service` e ri/avvia il servizio.

##### Nginx

Installa [nginx-mainline](https://www.archlinux.org/packages/?name=nginx-mainline) e [php-fpm](https://www.archlinux.org/packages/?name=php-fpm).

Modifica `/etc/php/php-fpm.d/www.conf` e cambia la direttiva di ascolto come segue:

```
listen = 127.0.0.1:9000  

```

Modifica `/etc/nginx/nginx.conf` in modo da aggiungere ciò che segue nella sezione **http**:

```
gzip            on;
gzip_min_length 1000;
gzip_proxied    expired no-cache no-store private auth;
gzip_types      text/plain application/xml application/json application/javascript application/octet-stream text/css;
include /etc/nginx/conf.d/*.conf;

```

Copia il file di configurazione fornito dal pacchetto:

```
# mkdir /etc/nginx/conf.d
# cp /etc/pihole/configs/nginx.pi-hole.conf /etc/nginx/conf.d/

```

Abilita `nginx.service` `php-fpm.service` e ri/avvia i servizi.

#### FTL

FTL è un interfaccia simil-database/fornitore di API che si occupa di conservare a lungo termine le interrogazioni che l'utente potrà consultare attraverso la sezione "long-term data" dell'interfaccia web. Per essere chiari, i dati vengono raccolti e conservati in due posti:

1.  I dati giornalieri vengono conservati in RAM e sono catturati in tempo reale dal file `/run/log/pihole/pihole.log`
2.  I dati storici (i.e. di diversi giorni/settimane/mesi) sono conservati sul filesystem `/etc/pihole/pihole-FTL.db` aggiornati ad un intervallo deciso dall'utente.

**Tip:** Se Pi-hole è installato su una unità a stato solito (SD dei mini PC, SSD, unità M.2/NVMe, etc...) si raccomanda di settare il valore di DBINTERVAL almeno a 60.0 per minimizzare le scritture sul database.

E' possibile configurare FTL modificando il file `/etc/pihole/pihole-FTL.conf` con i seguenti parametri (la prima opzione è la predefinita):

*   SOCKET_LISTENING=localonly|all (Ascoltare solamente connessioni locali o tutte)
*   TIMEFRAME=rolling24h|yesterday|today (Finestra temporale dei dati ultime 24h relative, fino a 48h (oggi + ieri), o fino a 24h (solo oggi, come in Pi-hole v2.x ))
*   QUERY_DISPLAY=yes|no (Mostrare tutte le richieste? Impostarlo a no per nasconderle)
*   AAAA_QUERY_ANALYSIS=yes|no (Permette a FTL di analizzare le richieste AAAA da pihole.log?)
*   MAXDBDAYS=365 (Per quanto tempo le richieste devono venire conservate nel database?)
*   RESOLVE_IPV6=yes|no (FTL deve provare di risolvere gli indirizzi IPv6?)
*   RESOLVE_IPV4=yes|no (FTL deve provare di risolvere gli indirizzi IPv4?)
*   DBINTERVAL=1.0 (Quanto spesso devono essere scritte le richieste nel database FTL [minuti]?)
*   DBFILE=/etc/pihole/pihole-FTL.db (Specifica percorso e nome del database SQLite a lungo termine di FTL. Impostandolo a DBFILE= disabilita il database)
*   MAXLOGAGE=24.0 (Quante ore di richieste devono essere importate dal database e dai log? Massimo 744 (31 giorni))

`pi-hole-ftl.service` è abilitato staticamente; ri/avvialo.

### Configurazione del router e di Pi-hole

#### Metodo consigliato

La maggior parte degli utenti hanno bisogno delle seguenti funzionalità:

1.  Monitoraggio degli host sulla macchina Pi-hole (p.e.: log delle richieste DNS legate a singole macchine dai rispettivi hostname).
2.  La risoluzione dei nomi sulla LAN.
3.  I servizi di Ad blocking e monitoraggio di rete offerti da Pi-hole.

Per ottenere i servizi suddetti, il router dovrebbe essere configurato in modo da distribuire ai i propri client l'indirizzo IP della macchina Pi-hole come risolutore DNS, ma mantenere la reale risoluzione DNS a *monte* della macchina Pi-hole. La macchina Pi-hole dovrebbe essere configurata per usare il router come *unico* risolutore DNS.

Sul router, configura una voce personalizzata di dnsmasq per distribuire l'IP della macchina Pi-hole. La sintassi è:

```
dhcp-option=6,Pi-hole_IP

```

Se Pi-hole è eseguito su una macchina il cui indirizzo IP è 192.168.1.250, la voce diventerà:

```
dhcp-option=6,192.168.1.250

```

Sulla macchina Pi-hole, entra nell'interfaccia web ([http://pi.hole](http://pi.hole)), seleziona "Settings" e definisci l'indirizzo IP del *router* come unico server DNS. Non definire altre voci DNS per la macchina Pi-hole.

**Tip:** Un semplice controllo per vedere se il router è configurato correttamente consiste nel rinnovare l'indirizzo IP rilasciato dal DHCP e controllare il contenuto di `/etc/resolv.conf` sulla macchina client. Sarebbe corretto vedere l'indirizzo IP della macchina Pi-hole e non l'IP del router.

**Note:** Per una piena funzionalità della rete e di Pi-hole, potrebbe essere necessario disabilitare, se presente nel firmware del router, la funzionalità `dns-rebind`.

**Note:** La configurazione consigliata potrebbe non essere possibile su alcuni router a seconda delle possibilità offerte dal firmware. La configurazione consigliata è confermata funzionante su alcuni popolari firmware open-source come [LEDE/OpenWRT](https://forum.lede-project.org/t/lede-pi-hole-works-perfectly-need-to-understand-why-so-i-can-configure-tomatousb-the-same-way/8274), [DD-WRT](https://www.dd-wrt.com/site/index), e [TomatoUSB](http://www.linksysinfo.org/index.php?threads/redefining-dns-from-router-to-a-box-running-pi-hole.73576/#post-292078) per nominarne alcuni.

#### Metodo alternativo

Gli utenti impossibilitati nel configurare il router come precedentemente indicato possono fare riferimento a [questa guida ufficiale](https://discourse.pi-hole.net/t/how-do-i-configure-my-devices-to-use-pi-hole-as-their-dns-server/245) per le istruzioni sulla configurazione.
Per completezza, un sunto di tale quida viene riportato a seguire.
Possono essere seguiti due metodi:

##### Metodo automatico: Impostare il server DNS Server nelle impostazioni del router

Questa è la via più veloce per fare usare Pi-hole ai tuoi dispositivi. Se imposti in questa maniera le opzioni DHCP del tuo router, qualsiasi dispositivo che si connette alla LAN bloccherà immediatamente la pubblicità.

**Tip:** Assicurati di agire nella sezione **LAN** e non in quella **WAN**.

Vai alla **sezione DHCP Server** del tuo router e imposta l'indirizzo IP della macchina che esegue Pi-hole come unico server DNS per la tua **LAN**.

**Warning:** Se hai già dei dispositivi connessi alla rete al momento di questi cambiamenti, non vedrai la pubblicità bloccata fino al rinnovo delle impostazioni DHCP. Per semplicità, riavvia quei dispositivi.

**Note:** Nota che il tuo Pi-hole dovrebbe risultare l'unico server DNS in quanto è Pi-hole stesso a redirigere le richieste agli altri server. Se imposti altri server sul router, è possibile che il filtraggio della pubblicità ne risenta negativamente.

##### Metodo manuale: Configura manualemente il DNS per ogni tuo dispositivo

E' possibile configurare manulamente ogni dispositivo per far si che usi Pi-hole come suo DNS server. Hai solo bisogno dell'indirizzo IP del tuo Pi-hole e seguire le seguenti istruzioni a seconda del tuo sistema operativo.

**Linux**
In diversi Desktop Environment moderni per Linux, l'impostazione dei DNS è fatta attraverso Network Manager.

1.  Clicca Sistema > Preferenze > Connessioni di rete
2.  Seleziona la connessione che vuoi configurare
3.  Clicca Modifica
4.  Seleziona la linguetta impostazioni IPv4 o IPv6
5.  Se è selezionato il metodo Automatico (DHCP), seleziona invece Automatico (DHCP) solo indirizzi. Se il metodo è impostato su qualcos'altro, non cambiarlo.
6.  Nella casella di testo Server DNS, inserisci l'IP di Pi-hole
7.  Clicca Salva per applicare i cambiamenti
8.  Ripeti la procedura per ogni connesione di rete che vuoi modificare.

Se non usi Network Manager, segui le specifiche istruzioni sul tuo gestore di connesione per la modifica manuale dei DNS.
Se non usi alcun gestore di connesione i tuoi server DNS sono elencati nel file `/etc/resolv.conf`: modificalo in modo da inserire la seguente **unica** voce `nameserver`:

 `/etc/resolv.conf` 
```
[...]
nameserver <Pi-hole_box_IP>

```

dove `<Pi-hole_box_IP>` l'indirizzo IP della macchina che esegue Pi-hole.

**macOS**

1.  Clicca Apple > Preferenze di sistema > Rete
2.  Seleziona la connessione di cui vuoi configurare il DNS
3.  Clicca Avanzate
4.  Seleziona la linguetta DNS
5.  Clicca + per rimpiazzare qualsiasi indirizzo esistente, o aggiungi, l'indirizzo IP di Pi-hole in cima alla lista:
6.  Clicca Applica > OK
7.  Ripeti la procedura per ogni connesione di rete che vuoi modificare.

**Windows**
Le impostazioni DNS sono specificate nelle finestra delle proprietà TCP/IP della connessione di rete selezionata.

1.  Vai al Pannelleo di controllo
2.  Clicca Rete e Internet > Centro di connessione e condivisione di rete > Modifica impostazione scheda
3.  Seleziona la connessione che vuoi configurare
4.  Click col destro sulla connessione > Proprietà
5.  Seleziona la linguetta Rete
6.  Seleziona Protocollo Internet Versione 4 (TCP/IPv4) o Protocollo Internet Versione 6 (TCP/IPv6)
7.  Clicca Proprietà
8.  Clicca Avanzate
9.  Seleziona la linguetta DNS
10.  Clicca OK
11.  Seleziona Usa i seguenti server DNS
12.  Rimpiazza gli indirizzi con quello del tuo Pi-hole
13.  Riavvia la connessione selezionata al punto 3
14.  Ripeti la procedura per ogni connesione di rete che vuoi modificare.

#### Metodo Pi-hole centrico

Può essere seguito anche un altro metodo per configurare la tua LAN. E' possibile impostare la macchina che esegue Pi-hole come server DHCP e disattivare tutti i servizi di rete sul tuo router, relegandolo a semplice gateway/natter.

**Warning:** Dnsmasq dovrebbe essere appena installato o dovrebbe usare il file di configurazione predefinito fornito dal pacchetto Pi-hole. Le seguenti istruzioni potrebbero sovrascrivere le tue personalizzazioni di dnsmasq ove presenti.

Per semplicità di configurazione ed esposizione, sarà seguito solo il metodo di configurazione via interfaccia web:

*   Vai nell'interfaccia di configurazione del tuo router e disabilità il servizio DHCP. Prendi nota dell'indirizzo IP del router.
*   Vai nell'interfaccia web di Pi-hole ([http://pi.hole](http://pi.hole))
*   Vai a **Settings/Pi-hole DHCP Server**
*   Abilita **DHCP server enabled**
*   Imposta l'intervallo DHCP per la tua LAN valorizzando le caselle di testo **From** e **To**. Per esempio: da 192.168.1.2 a 192.168.1.100
*   Imposta l'inrizzo IP del router nella casella di testo **Router**. Per esempio: 192.168.1.1
*   Opzionale: Da **Advanced DHCP settings** abilita **Enable IPv6 support (SLAAC + RA)** se vuoi il supporto e le funzionalità IPv6.
*   Opzionale: Se abbisogni di rilasci statici del DHCP li puoi configurare andando nella sezione **DHCP leases/Static DHCP leases configuration**.
*   Save per applicare i cambiamenti.

**Warning:** Se hai già dei dispositivi connessi alla rete al momento di questi cambiamenti, non vedrai la pubblicità bloccata fino al rinnovo delle impostazioni DHCP. Per semplicità, riavvia quei dispositivi.

### Usare Pi-hole attraverso OpenVPN

E' possibile usare [OpenVPN](/index.php/OpenVPN "OpenVPN") (server) assieme a Pi-hole per redirigere il traffico remoto dei client al DNS di Pi-hole e rimuovere loro la pubblicità. E' logico aspettarsi una riduzione del traffico cellulare in quanto i banner pubblicitari non vengono nemmeno caricati. Assicurati che il file `/etc/openvpn/server/server.conf` contenga le due linee indicate qui sotto sostituendo "xxx.xxx.xxx.xxx" con l'indirizzo IP della macchina che esegue Pi-hole:

```
push "redirect-gateway def1 bypass-dhcp"
push "dhcp-option DNS xxx.xxx.xxx.xxx"

```

Se ancora non dovesse funzionare, provare a creare il file `/etc/dnsmasq.d/00-openvpn.conf` con il seguente contenuto:

```
interface=tun0

```

Questo potrebbe essere necessario per far si che `dnsmasq` sia in ascolto su `tun0`.

## Pi-hole Standalone

La variante Standalone di Pi-hole per Archlinux è nata dalla necessità di usare i servizi di Pi-hole in mobilità. [L'articolo Sky-hole](http://dlaa.me/blog/post/skyhole) è stato di ispirazione.

### Installazione

Installa il pacchetto [pi-hole-standalone](https://aur.archlinux.org/packages/pi-hole-standalone/).
Il pacchetto Pi-hole standalone installa un timer (e relativo service) staticamente abilitato che aggiornerà settimanalmente la lista nera dei server di Pi-hole. Se non dovessi essere d'accordo con le temporizzazioni predefinite del timer (ereditata dal progetto principale) puoi, ovviamente, modificarlo o evitare che venga eseguito mascherandolo.
Devi far partire manualmente `pi-hole-gravity.timer` o semplicemente riavvia a configurazione terminata.

### Configurazione iniziale

#### Dnsmasq

Assicurati che la seguente riga in `/etc/dnsmasq.conf` sia non commentata:

 `/etc/dnsmasq.conf` 
```
[...]
conf-dir=/etc/dnsmasq.d/,*.conf

```

Abilita `dnsmasq.service` e ri/avvia il servizio.

#### Configurare la risoluzione dei nomi

Il pacchetto Pi-hole standalone per funzionare correttamente richiede che sia impostato un unico server DNS sulla tua macchina. L'indirizzo DNS deve essere quello della tua stessa macchina.
Questo può essere fatto in diverse maniere.

##### Manualmente

Se sulla tua macchina nessun servizio gestisce automaticamente il file `/etc/resolv.conf`, puoi facilemente modificarlo in modo da inserire una **unica** voce `nameserver`:

 `/etc/resolv.conf` 
```
[...]
nameserver 127.0.0.1

```

**Note:** nessun'altra voce `nameserver` deve essere presente nel file di configurazione.

##### Openresolve

E' probabile che sia il servizio [openresolv](https://www.archlinux.org/packages/?name=openresolv) a gestire `/etc/resolv.conf` nel caso in cui sia usato un gestore di connessioni come [netctl](https://www.archlinux.org/packages/?name=netctl), [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) o altri. Se è il tuo caso, occorre forzare [openresolv](https://www.archlinux.org/packages/?name=openresolv) ad usare **localhost** come server dei nomi.
Modifica `/etc/resolvconf.conf` in modo da togliere il commento alla riga name_servers:

 `/etc/resolvconf.conf` 
```
[...]
name_servers=127.0.0.1

```

e aggiorna resolvconf:

```
# resolvconf -u

```

## Usare Pi-hole

Come precedentemente menzionato, Pi-hole offre la possibiltà di essere usato e configurato sia da riga di comando sia dalla sua interfaccia web (solo pacchetto server).

### Gestione dei DNS di Pi-hole

Alla prima installazione, Pi-hole è configurato in maniera predefinita per usare i DNS di Google per risolvere i nomi richiesti dalla tua LAN. Se vuoi cambiare i server o semplicemente aggiungerne altri, sulla macchina che esegue Pi-hole puoi eseguire

```
pihole -a setdns [DNS1],[DNS2],...

```

seguito da una lista di server DNS separati da virgole che vuoi che userà Pi-hole. Per esempio, se in aggiunta ai DNS di Google vuoi aggiungere quelli di Comodo esegui

```
pihole -a setdns 8.8.8.8,8.8.4.4,8.26.56.26,8.20.246.20

```

Per il solo pacchetto server, puoi fare la stessa cosa via interfaccia web ([http://pi.hole](http://pi.hole)) andando su **Settings** e aggiungendo i server DNS desiderati nella sezione **Upstream DNS Servers**. **Save** per applicare i cambiamenti.

### Aggiornamento forzato della lista dei domini pubblicitari

Se hai la necessità di aggiornare la lista dei domini bloccati, sulla macchina Pi-hole puoi eseguire

```
pihole -g

```

o, sul solo pacchetto server, via interfaccia web ([http://pi.hole](http://pi.hole)) vai su **Tools/Update Lists** ed esegui **Update Lists**.

### Proteggere lìaccesso all'interfaccia web (solo pacchetto server)

L'interfaccia web di Pi-hole può venire protetta da password contro uni non autorizzati. Sulla macchina Pi-hole puoi eseguire

```
pihole -a -p <pwd>

```

dove `<pwd>` è la password da assegnare. Puoi lascare il campo vuoto per ottenere la classica richiesta e conferma password alla *nix.
Per disattivare la password di accesso riesegui

```
pihole -a -p

```

lasciando **tutto** vuoto.

### Disabilitare temporaneamente Pi-hole

Pi-hole può venire facilmente messo in pausa attraverso la sua intefaccia web ([http://pi.hole](http://pi.hole)): vai su **Disable** e scegli l'opzione di disabilitazione che preferisci.
E' possibile anche via CLI eseguendo

```
pihole disable [time]

```

Lasciando `time` vuoto la disabilitazione sarà permanente fino alla successiva manuale riabilitazione.
`time` può essere espresso in secondi o minuti con la sintassi #s e #m. Per esempio, per disabilitare Pi-hole per soli 5 minuti, puoi eseguire

```
pihole disable 5m

```

In qualsiasi momento è possibile riabilitare Pi-hole con

```
pihole enable

```

o, via interfaccia web, cliccando su **Enable**.

## Risorse

*   [Pi-hole Homepage](https://pi-hole.net/)
*   [Pi-hole GitHub Page](https://github.com/pi-hole/pi-hole)
*   [Pi-hole FTL GitHub Page](https://github.com/pi-hole/FTL)
*   [Sky-Hole, the basic idea under Pi-hole standalone](http://dlaa.me/blog/post/skyhole)