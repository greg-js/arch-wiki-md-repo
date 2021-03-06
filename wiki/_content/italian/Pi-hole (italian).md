Articoli correlati

*   [Dnsmasq](/index.php/Dnsmasq "Dnsmasq")
*   [Lighttpd](/index.php/Lighttpd "Lighttpd")
*   [Linux_Containers](/index.php/Linux_Containers "Linux Containers")
*   [Nginx](/index.php/Nginx "Nginx")
*   [OpenVPN](/index.php/OpenVPN "OpenVPN")

[Pi-hole](https://pi-hole.net/) è un [DNS sinkhole](https://en.wikipedia.org/wiki/DNS_sinkhole "wikipedia:DNS sinkhole") che redige una lista di blocco di domini conosciuti per offrire pubblicità e malware da sorgenti multiple di terze parti. Pi-hole, attraverso l'uso di [dnsmasq](/index.php/Dnsmasq "Dnsmasq"), elimina semplicemente tutte le richieste di domini nella sua lista di blocco. Questa configurazione implementa efficacemente il blocco della pubblicità a livello di rete senza dover configurare ogni singolo client. Il pacchetto offre una interfaccia web e una a riga di comando.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Pi-hole Server](#Pi-hole_Server)
    *   [1.1 Installazione](#Installazione)
    *   [1.2 Configurazione iniziale](#Configurazione_iniziale)
        *   [1.2.1 FTL](#FTL)
        *   [1.2.2 Web Server](#Web_Server)
            *   [1.2.2.1 Lighttpd](#Lighttpd)
            *   [1.2.2.2 Nginx](#Nginx)
        *   [1.2.3 /etc/hosts](#/etc/hosts)
    *   [1.3 Far usare Pi-hole ai propri apparati](#Far_usare_Pi-hole_ai_propri_apparati)
        *   [1.3.1 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [1.4 Usare Pi-hole attraverso OpenVPN](#Usare_Pi-hole_attraverso_OpenVPN)
    *   [1.5 Proteggere con password l'interfaccia web](#Proteggere_con_password_l'interfaccia_web)
    *   [1.6 Usare DNS Over HTTPS (DOH)](#Usare_DNS_Over_HTTPS_(DOH))
*   [2 Pi-hole Standalone](#Pi-hole_Standalone)
    *   [2.1 Installazione](#Installazione_2)
    *   [2.2 Configurazione iniziale](#Configurazione_iniziale_2)
        *   [2.2.1 Dnsmasq](#Dnsmasq)
        *   [2.2.2 Configurare la risoluzione dei nomi](#Configurare_la_risoluzione_dei_nomi)
            *   [2.2.2.1 Manualmente](#Manualmente)
            *   [2.2.2.2 Openresolve](#Openresolve)
*   [3 Usare Pi-hole](#Usare_Pi-hole)
    *   [3.1 Gestione dei DNS di Pi-hole](#Gestione_dei_DNS_di_Pi-hole)
    *   [3.2 Aggiornamento forzato della lista dei domini pubblicitari](#Aggiornamento_forzato_della_lista_dei_domini_pubblicitari)
    *   [3.3 Disabilitare temporaneamente Pi-hole](#Disabilitare_temporaneamente_Pi-hole)
*   [4 Risoluzione di problemi](#Risoluzione_di_problemi)
    *   [4.1 Perdita di dati su riavvio](#Perdita_di_dati_su_riavvio)
*   [5 Risorse](#Risorse)

## Pi-hole Server

**Note:** [pi-hole-server](https://aur.archlinux.org/packages/pi-hole-server/) non è ufficialmente supportato dal progetto Pi-hole.

### Installazione

Installa il pacchetto [pi-hole-server](https://aur.archlinux.org/packages/pi-hole-server/).

### Configurazione iniziale

#### FTL

[Pi-hole FTL](https://github.com/pi-hole/FTL) ([pi-hole-ftl](https://aur.archlinux.org/packages/pi-hole-ftl/)) è una dipendenza del progetto Pi-hole.

FTL è un DNS server/forwarder e una interfaccia simil-database/fornitore di API che si occupa del salvataggio a lungo termine delle richieste che gli utenti possono richiedere "long-term data" section of the WebGUI. To be clear, data are collected and stored in two places:

1.  I dati giornalieri vengono conservati in RAM e sono catturati in tempo reale dal file `/run/log/pihole/pihole.log`
2.  I dati storici (i.e. di diversi giorni/settimane/mesi) sono conservati sul filesystem `/etc/pihole/pihole-FTL.db` aggiornati ad un intervallo deciso dall'utente.

`pi-hole-ftl.service` è abilitato staticamente; ri/avvialo. Consultare la [documentazione ufficiale](https://docs.pi-hole.net/ftldns/configfile/) per come configurare FTL.

**Tip:** Se Pi-hole è installato su una unità a stato solito (SD dei mini PC, SSD, unità M.2/NVMe, etc...) si raccomanda di settare il valore di DBINTERVAL almeno a 60.0 per minimizzare le scritture sul database.

**Note:** Dalla versione 4.0, Pi-hole-FTL integra un fork privato di dnsmasq. Il pacchetto originale [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) ora confligge con [pi-hole-ftl](https://aur.archlinux.org/packages/pi-hole-ftl/) e sarà disinstallato su aggiornamento da una precedente versione. E' ancora possibile usare i precedenti file di configurazione di dnsmasq, assicurati solamente che la riga `conf-dir=/etc/dnsmasq.d/,*.conf` nel file originale `/etc/dnsmasq.conf` non sia commentata.

#### Web Server

Opzionalmente è possibile scegliere un server web per usare l'interfaccia web di Pi-hole.

**Note:** Pi-hole non richiede forzatamente l'uso dell'interfaccia web in quanto molti comandi sono disponibili via CLI.

File di configurazione già funzionanti sono forniti sia per [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) che per [nginx](https://www.archlinux.org/packages/?name=nginx). Altri server web possono tranquillamente eseguire l'interfaccia web, ma non sono al momento supportati.

Installa [php-sqlite](https://www.archlinux.org/packages/?name=php-sqlite) e abilita le necessarie estensioni di seguito elencate:

 `/etc/php/php.ini` 
```
[...]
extension=pdo_sqlite
[...]
extension=sockets
extension=sqlite3
[...]
```

Per ragioni di sicurezza, se vuoi popolare la direttiva [PHP open_basedir](/index.php/PHP#Configuration "PHP"), l'interfaccia web di amministrazione di Pi-hole necessita l'accesso ai seguenti file e cartelle:

```
/srv/http/pihole
/run/pihole-ftl/pihole-FTL.port
/run/log/pihole/pihole.log
/run/log/pihole-ftl/pihole-FTL.log
/etc/pihole
/etc/hosts
/etc/hostname
/etc/dnsmasq.d/02-pihole-dhcp.conf
/etc/dnsmasq.d/03-pihole-wildcard.conf
/etc/dnsmasq.d/04-pihole-static-dhcp.conf
/proc/meminfo
/proc/cpuinfo
/sys/class/thermal/thermal_zone0/temp
/tmp

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

#### /etc/hosts

[filesystem](https://www.archlinux.org/packages/?name=filesystem) contiene il file `/etc/hosts` vuoto, condizione nota ad impedire a Pi-hole il recupero delle liste. E' possibile risolvere aggiungendovi quanto segue assicurando il corretto funzionamento, notando bene che *indirizzo.ip.di.pihole* dovrà essere l'attuale indirizzo IP della macchina che esegue Pi-hole (es. 192.168.1.250) e *myhostname* il suo relativo hostname.

```
127.0.0.1                localhost
indirizzo.ip.di.pihole   pi.hole myhostname

```

Per approfondire, leggi [Issue#1800](https://github.com/pi-hole/pi-hole/issues/1800).

### Far usare Pi-hole ai propri apparati

[La documentazione ufficiale](https://discourse.pi-hole.net/t/how-do-i-configure-my-devices-to-use-pi-hole-as-their-dns-server/245) descrive quattro metodi diversi:

1.  Definire l'indirizzo IP di Pi-hole come unico server DNS nel router
2.  Rendere noto l'indirizzo IP di Pi-hole attraverso dnsmasq nel router (se supportato)
3.  Configurare manualmente ogni apparato in modo che usi Pi-hole com server DNS
4.  [Usare il DHCP integrato di Pi-hole](https://discourse.pi-hole.net/t/how-do-i-use-pi-holes-built-in-dhcp-server-and-why-would-i-want-to/3026)

#### Risoluzione dei problemi

*   Se configuri usando il metodo del DHCP server e su un apparato il blocco della pubblicità non funziona, potrebbe avere ancora un rilascio DHCP obsoleto. Se non sai come rinnovarlo, prova a riavviare l'apparato.
*   Un semplice metodo per capire se il router è configurato correttamente è per prima cosa rinnovare il rilascio DHCP, quindi verificare il contenuto del file `/etc/resolv.conf` su un client Linux. Si dovrebbe vedere l'indirizzo IP di Pi-hole e non l'indirizzo del router.
*   Se hai problemi con il secondo metodo, prova a disabilitare il `dns-rebind` sul router (se presente).

### Usare Pi-hole attraverso OpenVPN

Un server [OpenVPN](/index.php/OpenVPN "OpenVPN") può essere configurato per informare i sui client della presenza di Pi-hole. Aggiungi le due seguenti linee al tuo `/etc/openvpn/server/server.conf`:

```
push "redirect-gateway def1 bypass-dhcp"
push "dhcp-option DNS *Pi-Hole-IP*"

```

Se ancora non dovesse funzionare, provare a creare il file `/etc/dnsmasq.d/00-openvpn.conf` con il seguente contenuto:

```
interface=tun0

```

Questo potrebbe essere necessario per far si che `dnsmasq` sia in ascolto su `tun0`.

### Proteggere con password l'interfaccia web

Per proteggere con password l'interfaccia web di Pi-hole, esegui il seguente comando e inserisci la tua password:

```
pihole -a -p

```

Per disabilitare la protezione inserisci una password vuota.

### Usare DNS Over HTTPS (DOH)

Le richieste DNS possono anche essere eseguite [via HTTPS](https://en.wikipedia.org/wiki/DNS_over_HTTPS "wikipedia:DNS over HTTPS") usando un privacy-first DNS [1.1.1.1](https://1.1.1.1/) di [Cloudflare](https://www.cloudflare.com/). Installa [cloudflared-bin](https://aur.archlinux.org/packages/cloudflared-bin/) e segui [la documentatione del progetto](https://docs.pi-hole.net/guides/dns-over-https/).

## Pi-hole Standalone

**Note:** [pi-hole-standalone](https://aur.archlinux.org/packages/pi-hole-standalone/) non è ufficialmente supportato dal progetto Pi-hole.

La variante Standalone di Pi-hole per Archlinux è nata dalla necessità di usare i servizi di Pi-hole in mobilità. [L'articolo Sky-hole](http://dlaa.me/blog/post/skyhole) è stato di ispirazione.

### Installazione

Installa il pacchetto [pi-hole-standalone](https://aur.archlinux.org/packages/pi-hole-standalone/). Il pacchetto Pi-hole standalone installa un timer (e relativo service) staticamente abilitato che aggiornerà settimanalmente la lista nera dei server di Pi-hole. Se non dovessi essere d'accordo con le temporizzazioni predefinite del timer (ereditata dal progetto principale) puoi, ovviamente, modificarlo o evitare che venga eseguito mascherandolo. Devi far partire manualmente `pi-hole-gravity.timer` o semplicemente riavvia a configurazione terminata.

### Configurazione iniziale

#### Dnsmasq

Assicurati che la seguente riga in `/etc/dnsmasq.conf` sia non commentata:

```
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

**Note:** No other `nameserver` items need to be present in the config file.

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

By default Pi-hole uses the Google DNS server. You can change which DNS servers Pi-hole uses with:

```
$ pihole -a setdns *server*

```

You can specify multiple DNS servers by separating their addresses with commas.

Per il solo pacchetto server, puoi fare la stessa cosa via interfaccia web ([http://pi.hole](http://pi.hole)) andando su *Settings* e aggiungendo i server DNS desiderati nella sezione *Upstream DNS Servers*. *Save* per applicare i cambiamenti.

### Aggiornamento forzato della lista dei domini pubblicitari

Se hai la necessità di aggiornare la lista dei domini bloccati, sulla macchina Pi-hole puoi eseguire

```
pihole -g

```

o, sul solo pacchetto server, via interfaccia web ([http://pi.hole](http://pi.hole)) vai su *Tools/Update Lists* ed esegui *Update Lists*.

### Disabilitare temporaneamente Pi-hole

Pi-hole può venire facilmente messo in pausa attraverso la sua intefaccia web ([http://pi.hole](http://pi.hole)): vai su *Disable* e scegli l'opzione di disabilitazione che preferisci.
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

o, via interfaccia web, cliccando su *Enable*.

## Risoluzione di problemi

### Perdita di dati su riavvio

I sistemi senza il [RTC](/index.php/RTC "RTC") come alcuni dispositivi ARM è probabile che possano perdere dati dal log delle query durante un riavvio. Quando un sistema senza [RTC](/index.php/RTC "RTC") si avvia, l'orologio di sistema è impostato *dopo* l'esecuzione della rete e del resolver. Alcune parti di Pi-hole possono avviarsi prima che questo accada portando alla perdita di dati. Anche un valore [RTC](/index.php/RTC "RTC") sbagliato può causare problemi. Vedi: [Installation guide#Time zone](/index.php/Installation_guide#Time_zone "Installation guide") and [System time](/index.php/System_time "System time"). Per dispositivi senza [RTC](/index.php/RTC "RTC"): Una possibile soluzione può essere l'uso di [Systemd#Drop-in files](/index.php/Systemd#Drop-in_files "Systemd") su `pihole-FTL.service` usando una chiamata ritardata `/usr/bin/sleep x` con una direttiva `ExecStartPre`. Da notare che il valore di "x" dipende da quanto tempo il tuo sistema impiega ad effettuare un time sync. Al momento la segnalazione [Issue#11008](https://github.com/systemd/systemd/issues/11008) su systemd-timesyncd sta impedento l'uso di *time-sync.target* per automatizzare il tutto.

## Risorse

*   [Homepage di Pi-hole](https://pi-hole.net/)
*   [Pagina GitHub di Pi-hole](https://github.com/pi-hole/pi-hole)
*   [Pagina GitHub di Pi-hole FTL](https://github.com/pi-hole/FTL)
*   [Sky-Hole, l'idea di base sotto Pi-hole standalone](http://dlaa.me/blog/post/skyhole)