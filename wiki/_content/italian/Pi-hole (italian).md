Dal file [README.md del repository GitHub di Pi-hole](https://github.com/pi-hole/pi-hole):

	The Pi-Hole™ è un DNS/Web server con gestione della pubblicità. Se viene richiesto un dominio contenente pubblicità, una piccola pagina o una GIF viene offerta in sostituzione.

	Lo script gravity.sh esegue la maggior parte del lavoro. Lo script raccoglie i domini pubblicitari da più sorgenti e li compila in una singola lista di più di 1.6 milioni di voci (se decidi di usare la lista di mahakala). Lo script è controllato dal comando pihole. Esegui pihole -h per leggere quali comandi sono disponibili.

Questa pagina wiki tenta di fornire istruzioni di uso e configurazione per questo adattamento per Archlinux di Pi-hole non ufficialmente supportato dal progetto principale. Per bug, problemi e comunicazioni varie, rivolgiti alla [pagina AUR di pi-hole-server](https://aur.archlinux.org/packages/pi-hole-server/) per il pacchetto server o alla [pagina AUR di pi-hole-standalone](https://aur.archlinux.org/packages/pi-hole-standalone/) per il pacchetto standalone.

## Contents

*   [1 Pi-hole Server](#Pi-hole_Server)
    *   [1.1 Installazione](#Installazione)
    *   [1.2 Configurazione di prima installazione](#Configurazione_di_prima_installazione)
        *   [1.2.1 Dnsmasq](#Dnsmasq)
        *   [1.2.2 Web Server](#Web_Server)
            *   [1.2.2.1 Lighttpd](#Lighttpd)
            *   [1.2.2.2 Nginx](#Nginx)
    *   [1.3 Configurazione su aggiornamento](#Configurazione_su_aggiornamento)
    *   [1.4 Web interface](#Web_interface)
    *   [1.5 FTL](#FTL)
*   [2 Usare Pi-hole attraverso OpenVPN](#Usare_Pi-hole_attraverso_OpenVPN)
*   [3 Pi-hole Standalone](#Pi-hole_Standalone)
    *   [3.1 Installazione](#Installazione_2)
    *   [3.2 Configurazione di prima installazione](#Configurazione_di_prima_installazione_2)
        *   [3.2.1 Dnsmasq](#Dnsmasq_2)
        *   [3.2.2 Openresolve](#Openresolve)
    *   [3.3 Configurazione su aggiornamento](#Configurazione_su_aggiornamento_2)
*   [4 Risorse](#Risorse)

## Pi-hole Server

### Installazione

Installa [pi-hole-ftl](https://aur.archlinux.org/packages/pi-hole-ftl/) e [pi-hole-server](https://aur.archlinux.org/packages/pi-hole-server/).

### Configurazione di prima installazione

#### Dnsmasq

Configura dnsmasq che risolverà le richieste DNS per la tua LAN e si occuperà del filtraggio della pubblicità attraverso pi-hole.

**Utenti che usano già dnsmasq**: modifica `/etc/dnsmasq.conf` rimuovendo il commento all'ultima linea, includendo così i file di configurazione di pi-hole che si trovano nella directory `/etc/dnsmasq.d`:

```
# sed -i 's|#conf-dir=/etc/dnsmasq.d/,\*.conf|conf-dir=/etc/dnsmasq.d/,\*.conf|' /etc/dnsmasq.conf

```

**Utenti che non usavano dnsmasq prima dell'installazione Pi-hole**: copia il file di configurazione fornito dal pacchetto in sostituzione del predefinito (o semplicemente fai un diff dei due):

```
# cp /etc/pihole/configs/dnsmasq.main /etc/dnsmasq.conf

```

Se necessario, attiva `dnsmasq.service` e ri/avvia il servizio. Pi-hole deve essere il DNS della tua LAN. Con ogni probabilità, è il tuo router a fornire i DNS ai client della tua LAN in questo momento, quindi come DNS primario sul router dovresti impostare l'indirizzo IP della macchina che esegue pi-hole. La configurazione del router va oltre lo scopo di questo articolo, ma rimane un passo obbligatorio.

#### Web Server

Opzionalmente, è possibile scegliere un server web per usare l'interfaccia amministrativa di pi-hole.

**Note:** Pi-hole non richiede forzatamente l'uso dell'interfaccia web in quanto molti comandi sono disponibili via CLI.

Il progetto originale supporta ufficialmente [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) offrendone già un file di configurazione. Il pacchetto AUR ne fornisce uno anche per [nginx](https://www.archlinux.org/packages/?name=nginx), rendendoli di fatto supportati entrambi. Altri server web possono tranquillamente eseguire l'interfaccia web, ma non sono supportati.

Tutti i server web abbisognano della seguente modifica per abilitate l'estensione per i socket:

 `/etc/php/php.ini` 
```
[...]
extension=sockets.so
[...]
```

##### Lighttpd

Installa [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) e [php-cgi](https://www.archlinux.org/packages/?name=php-cgi). Salva i file di configurazione originali e copia quelli di pi-hole:

```
# cp /etc/lighttpd/lighttpd.conf /etc/lighttpd/lighttpd.orig
# cp /etc/pihole/configs/lighttpd.conf /etc/lighttpd/lighttpd.conf

```

Se necessario, abilita `lighttpd.service` e ri/avvia il servizio.

##### Nginx

[Install](/index.php/Install "Install") [nginx](https://www.archlinux.org/packages/?name=nginx) or [nginx-mainline](https://www.archlinux.org/packages/?name=nginx-mainline) and [php-fpm](https://www.archlinux.org/packages/?name=php-fpm).

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

Se necessario, abilita `nginx.service` `php-fpm.service` e ri/avvia i servizi.

### Configurazione su aggiornamento

**Tip:** Se aggiornando non leggi alcun messaggio a fine installazione che avverte della modifica dei file di configurazione di dnsmasq o dei server web, puoi saltare questo passaggio.

Se necessario, aggiorna il file di configurazione di dnsmasq

```
# [ -f /etc/dnsmasq.orig ] && cp /etc/pihole/configs/dnsmasq.main /etc/dnsmasq.conf

```

e ri/avvia il servizio.

Se necessario, aggiorna il file di configurazione di lighttpd

```
# [ -f /etc/lighttpd/lighttpd.orig ] && cp /etc/pihole/configs/lighttpd.conf /etc/lighttpd/lighttpd.conf

```

e ri/avvia il servizio.

Se necessario, aggiorna il file di configurazione di nginx

```
# cp /etc/pihole/configs/nginx.pi-hole.conf /etc/nginx/conf.d/

```

e ri/avvia il servizio.

### Web interface

L'interfaccia web di pi-hole è particolarmente completa e ben fatta. Si può usare per configurare quasi ogni aspetto di [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq), eseguire molti dei comandi disponibili di pi-hole, gestire le white e blacklist e monitorare il filtraggio della pubblicità. Per connetterti all'interfaccia

```
http://<IP/Hostname della macchina Pi-hole>/admin/

```

o

```
[http://pi.hole/admin](http://pi.hole/admin)

```

### FTL

FTL è parte del progetto Pi-hole. E' un interfaccia simil-database/fornitore di API sul log delle richieste DNS di Pi-hole. E' possibile configurare FTL attraverso il file `/etc/pihole/pihole-FTL.conf`. [Leggi](https://github.com/pi-hole/FTL#ftls-config-file) la documentazione del progetto per i dettagli.

## Usare Pi-hole attraverso OpenVPN

E' possibile usare [OpenVPN](/index.php/OpenVPN "OpenVPN") (server) assieme a Pi-hole per redirigere il traffico remoto dei client al DNS di Pi-hole e rimuovere loro la pubblicità. E' logico aspettarsi una riduzione del traffico cellulare in quanto i banner pubblicitari non vengono nemmeno caricati. Assicurati che il file `/etc/openvpn/server/server.conf` contenga le due linee indicate qui sotto sostituendo "xxx.xxx.xxx.xxx" con l'indirizzo IP della macchina che esegue Pi-hole:

```
push "redirect-gateway def1 bypass-dhcp"
push "dhcp-option DNS xxx.xxx.xxx.xxx"

```

**Note:** Questa dovrebbe essere l'unica modifica richiesta.

## Pi-hole Standalone

La variante Standalone di Pi-hole per Archlinux è nata dalla necessità di usare i servizi di pi-hole in mobilità. [L'articolo Sky-hole](http://dlaa.me/blog/post/skyhole) è stato di ispirazione.

### Installazione

Installa il pacchetto [pi-hole-standalone](https://aur.archlinux.org/packages/pi-hole-standalone/).

### Configurazione di prima installazione

#### Dnsmasq

Come primo passo, è necessario configurare dnsmasq. Risolverà le richieste DNS per la tua macchina filtrando la pubblicità con pi-hole.

**Se usi già dnsmasq**, modifica `/etc/dnsmasq.conf` rimuovendo il commento all'ultima linea, includendo così i file di configurazione di pi-hole che si trovano nella directory /etc/dnsmasq.d:

```
# sed -i 's|#conf-dir=/etc/dnsmasq.d/,\*.conf|conf-dir=/etc/dnsmasq.d/,\*.conf|' /etc/dnsmasq.conf

```

**Se hai installato dnsmasq con Pi-hole per la prima volta**, fai una copia di salvataggio del file di configurazione originale di dnsmasq e copia quello di pi-hole:

```
# cp /etc/dnsmasq.conf /etc/dnsmasq.orig
# cp /etc/pihole/configs/dnsmasq.main /etc/dnsmasq.conf

```

Se necessario, abilita `dnsmasq.service` e ri/avvia il servizio:

#### Openresolve

Modifica `/etc/resolvconf.conf` e rimuovi il commento alla linea name_servers (l'ultima) e aggiorna resolvconf:

```
# sed -i 's|#name_servers=127.0.0.1|name_servers=127.0.0.1|' /etc/resolvconf.conf
# resolvconf -u

```

ora risolverai sempre le richieste DNS attraverso localhost, e [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) sarà in ascolto.

### Configurazione su aggiornamento

**Tip:** Se aggiornando non leggi alcun messaggio a fine installazione che avverte della modifica dei file di configurazione di dnsmasq, puoi saltare questo passaggio.

Se necessario, aggiorna il file di configurazione di dnsmasq

```
# [ -f /etc/dnsmasq.orig ] && cp /etc/pihole/configs/dnsmasq.main /etc/dnsmasq.conf

```

e ri/avvia il servizio.

## Risorse

*   [Pi-hole Homepage](https://pi-hole.net/)
*   [Pi-hole GitHub Page](https://github.com/pi-hole/pi-hole)
*   [Pi-hole FTL GitHub Page](https://github.com/pi-hole/FTL)
*   [Sky-Hole, the basic idea under Pi-hole standalone](http://dlaa.me/blog/post/skyhole)