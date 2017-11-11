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
*   [2 Configurazione del router e di Pi-hole](#Configurazione_del_router_e_di_Pi-hole)
    *   [2.1 Metodo consigliato](#Metodo_consigliato)
    *   [2.2 Metodo alternativo](#Metodo_alternativo)
*   [3 Usare Pi-hole attraverso OpenVPN](#Usare_Pi-hole_attraverso_OpenVPN)
*   [4 Pi-hole Standalone](#Pi-hole_Standalone)
    *   [4.1 Installazione](#Installazione_2)
    *   [4.2 Configurazione iniziale](#Configurazione_iniziale_2)
        *   [4.2.1 Dnsmasq](#Dnsmasq_2)
        *   [4.2.2 Openresolve](#Openresolve)
*   [5 Risorse](#Risorse)

## Pi-hole Server

### Installazione

Installa [pi-hole-ftl](https://aur.archlinux.org/packages/pi-hole-ftl/) e [pi-hole-server](https://aur.archlinux.org/packages/pi-hole-server/).

### Configurazione iniziale

#### Dnsmasq

Assicurati che la seguente riga in `/etc/dnsmasq.conf` sia non commentata:

 `/etc/dnsmasq.conf` 
```
[...]
conf-dir=/etc/dnsmasq.d/,*.conf

```

Abilita `dnsmasq.service` e ri/avvia il servizio.

#### Web Server

Opzionalmente, è possibile scegliere un server web per usare l'interfaccia amministrativa di Pi-hole.

**Note:** Pi-hole non richiede forzatamente l'uso dell'interfaccia web in quanto molti comandi sono disponibili via CLI.

Il pacchetto AUR fornisce file di configurazione di esempio sia per [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) che per [nginx](https://www.archlinux.org/packages/?name=nginx). Altri server web possono tranquillamente eseguire l'interfaccia web, ma non sono al momento supportati.

Tutti i server web abbisognano della seguente modifica per abilitate l'estensione per i socket:

 `/etc/php/php.ini` 
```
[...]
extension=sockets.so
[...]
```

Per ragioni di sicurezza, se vuoi popolare la direttiva [PHP open_basedir](/index.php/PHP#Configuration "PHP"), l'interfaccia web di amministrazione di Pi-hole necessita l'accesso ai seguenti file e cartelle:

```
/srv/http/pihole:/run/pihole-ftl/pihole-FTL.port:/run/log/pihole/pihole.log:/run/log/pihole-ftl/pihole-FTL.log:/etc/pihole:/etc/hosts:/etc/hostname:/etc/dnsmasq.d/03-pihole-wildcard.conf:/proc/meminfo:/proc/cpuinfo:/sys/class/thermal/thermal_zone0/temp:/tmp

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

#### FTL

FTL è parte del progetto Pi-hole. E' un interfaccia simil-database/fornitore di API sul log delle richieste DNS di Pi-hole. E' possibile configurare FTL attraverso il file `/etc/pihole/pihole-FTL.conf`. [Leggi](https://github.com/pi-hole/FTL#ftls-config-file) la documentazione del progetto per i dettagli.

`pi-hole-ftl.service` è abilitato staticamente; ri/avvialo.

## Configurazione del router e di Pi-hole

### Metodo consigliato

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

### Metodo alternativo

**Note:** La configurazione consigliata potrebbe non essere possibile su alcuni router a seconda delle possibilità offerte dal firmware. La configurazione consigliata è confermata funzionante su alcuni popolari firmware open-source come [LEDE/OpenWRT](https://forum.lede-project.org/t/lede-pi-hole-works-perfectly-need-to-understand-why-so-i-can-configure-tomatousb-the-same-way/8274), [DD-WRT](https://www.dd-wrt.com/site/index), e [TomatoUSB](http://www.linksysinfo.org/index.php?threads/redefining-dns-from-router-to-a-box-running-pi-hole.73576/#post-292078) per nominarne alcuni.

Gli utenti impossibilitati di configurare il router come precedentemente esposto possono fare riferimento a [questa guida](https://discourse.pi-hole.net/t/how-do-i-configure-my-devices-to-use-pi-hole-as-their-dns-server/245) per ottenere quasi tutte le funzionalità richieste. Le limitazioni chiave di utilizzo di questo metodo includono:

1.  Monitoraggio degli host sulla macchina Pi-hole (p.e.: log delle richieste DNS legate a singole macchine dai rispettivi hostname).
2.  La risoluzione dei nomi sulla LAN.

## Usare Pi-hole attraverso OpenVPN

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