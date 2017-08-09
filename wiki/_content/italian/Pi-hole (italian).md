Pi-hole è un progetto basato su script di shell che gestisce liste di blocco di pubblicità e malware conosciuti e interagisce trasparentemente con dnsmasq per reindirizzare ogni richiesta verso un sostituto. Pi-hole rimpiazza il tuo router come DNS di rete e quindi tutti le richieste saranno gestire da lui senza il bisogno di installare nulla sul lato client. Questa configurazione implementa efficacemente il blocco della pubblicità a livello di rete (es. tutti gli apparati connessi). Il pacchetto offre una webUI ben fatta (unitamente ad una interfaccia CLI) ed è particolarmente leggero e scalabile.

## Contents

*   [1 Pi-hole Server](#Pi-hole_Server)
    *   [1.1 Installazione](#Installazione)
    *   [1.2 Configurazione iniziale](#Configurazione_iniziale)
        *   [1.2.1 Dnsmasq](#Dnsmasq)
        *   [1.2.2 Router](#Router)
        *   [1.2.3 Web Server](#Web_Server)
            *   [1.2.3.1 Lighttpd](#Lighttpd)
            *   [1.2.3.2 Nginx](#Nginx)
    *   [1.3 Web interface](#Web_interface)
    *   [1.4 FTL](#FTL)
*   [2 Usare Pi-hole attraverso OpenVPN](#Usare_Pi-hole_attraverso_OpenVPN)
*   [3 Pi-hole Standalone](#Pi-hole_Standalone)
    *   [3.1 Installazione](#Installazione_2)
    *   [3.2 Configurazione iniziale](#Configurazione_iniziale_2)
        *   [3.2.1 Dnsmasq](#Dnsmasq_2)
        *   [3.2.2 Openresolve](#Openresolve)
*   [4 Risorse](#Risorse)

## Pi-hole Server

### Installazione

Installa [pi-hole-ftl](https://aur.archlinux.org/packages/pi-hole-ftl/) e [pi-hole-server](https://aur.archlinux.org/packages/pi-hole-server/).

### Configurazione iniziale

#### Dnsmasq

Pi-hole interagisce con [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) per risolvere le richieste DNS della tua LAN e si occuperà del filtraggio della pubblicità. Assicurati che la seguente riga in `/etc/dnsmasq.conf` sia non commentata:

 `/etc/dnsmasq.conf` 
```
[...]
conf-dir=/etc/dnsmasq.d/,*.conf

```

Abilita `dnsmasq.service` e ri/avvia il servizio.

#### Router

Pi-hole deve essere il DNS della LAN per poter funzionare correttamente. La tipica utenza casalinga o i piccoli uffici si affidano al proprio router per risolvere le richieste DNS. Il metodo migliore è semplicemente ridefinire i DNS **sul router** indicando di usare l'indirizzo IP della macchina che esegue Pi-hole. Configurare il router è fuori dagli scopi di questo articolo. In alternativa è possibile configurare i DNS di ogni macchina o apparato che si connette al router anche se può essere noioso. Vedi [Come configurare i miei apparati per usare Pi-hole come DNS server?](https://discourse.pi-hole.net/t/how-do-i-configure-my-devices-to-use-pi-hole-as-their-dns-server/245) per maggiori dettagli.

#### Web Server

Opzionalmente, è possibile scegliere un server web per usare l'interfaccia amministrativa di pi-hole.

**Note:** Pi-hole non richiede forzatamente l'uso dell'interfaccia web in quanto molti comandi sono disponibili via CLI.

Il pacchetto AUR fornisce file di configurazione di esempio sia per [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) che per [nginx](https://www.archlinux.org/packages/?name=nginx). Altri server web possono tranquillamente eseguire l'interfaccia web, ma non sono al momento supportati.

Tutti i server web abbisognano della seguente modifica per abilitate l'estensione per i socket:

 `/etc/php/php.ini` 
```
[...]
extension=sockets.so
[...]
```

##### Lighttpd

Installa [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) e [php-cgi](https://www.archlinux.org/packages/?name=php-cgi).

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

`pi-hole-ftl.service` è abilitato staticamente; ri/avvialo.

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

### Configurazione iniziale

#### Dnsmasq

La configurazione è identica ai passaggi descritti in [#Dnsmasq](#Dnsmasq).

#### Openresolve

Modifica `/etc/resolvconf.conf` e rimuovi il commento alla linea name_servers:

 `/etc/resolvconf.conf` 
```
[...]
name_servers=127.0.0.1

```

e aggiorna resolvconf:

```
# resolvconf -u

```

## Risorse

*   [Pi-hole Homepage](https://pi-hole.net/)
*   [Pi-hole GitHub Page](https://github.com/pi-hole/pi-hole)
*   [Pi-hole FTL GitHub Page](https://github.com/pi-hole/FTL)
*   [Sky-Hole, the basic idea under Pi-hole standalone](http://dlaa.me/blog/post/skyhole)