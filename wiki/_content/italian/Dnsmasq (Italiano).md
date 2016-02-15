dnsmasq fornisce un servizio di cache DNS e di server DHCP. Come Domain Name Server (DNS), può conservare i risultati delle richieste di risoluzione per migliorare la velocità di connessione ai siti già visitati. Come server DHCP. [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) può essere usato per fornire indirizzi IP interni ed instradare i computer in una LAN. Uno o entrambi questi servizi possono essere utilizzati. dnsmasq è considerato leggero e semplice da configurare; è progettato sia per l'uso su di un personal computer, che per una rete con meno di 50 computer. Fornisce anche il servizio di server [PXE](/index.php/PXE "PXE").

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione della cache DNS](#Configurazione_della_cache_DNS)
    *   [2.1 File degli indirizzi DNS](#File_degli_indirizzi_DNS)
    *   [2.2 dhcpcd](#dhcpcd)
    *   [2.3 dhclient](#dhclient)
        *   [2.3.1 NetworkManager](#NetworkManager)
            *   [2.3.1.1 Altri metodi](#Altri_metodi)
            *   [2.3.1.2 Configurazione personalizzata](#Configurazione_personalizzata)
*   [3 DHCP Server Setup](#DHCP_Server_Setup)
*   [4 Avviare il demone](#Avviare_il_demone)
*   [5 Test](#Test)
    *   [5.1 DNS Caching](#DNS_Caching)
*   [6 DHCP Server](#DHCP_Server)
*   [7 Trucchi e consigli](#Trucchi_e_consigli)
    *   [7.1 Prevenire che OpenDNS reindirizzino le query a Google](#Prevenire_che_OpenDNS_reindirizzino_le_query_a_Google)
    *   [7.2 Visualizzare i lease](#Visualizzare_i_lease)

## Installazione

[Installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") il pacchetto [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) dai [repository ufficiali](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)").

## Configurazione della cache DNS

Per configurare dnsmasq come demone per la cache delle richieste DNS su un singolo computer modificare il file `/etc/dnsmasq.conf` aggiungendo o de commentando l'indirizzo di localhost in ascolto:

```
listen-address=127.0.0.1

```

Per utilizzare questo computer come server DNS specificare l'indirizzo IP fisso sulla rete:

```
listen-address=<192.168.1.1> #IP di Esempio

```

### File degli indirizzi DNS

Dopo aver configurato dnsmasq il client DHCP dovrà dare precedenza all'indirizzo di localhost rispetto agli indirizzi contenuti nel file di configurazione dei DNS (`/etc/resolv.conf`). Facendo questo, tutte le richieste verranno inviate a dnsmasq prima di provare a risolverle mediante DNS esterni. Dopo che è stato configurato il client DHCP sarà necessario riavviare il servizio di rete affinché le modifiche abbiano effetto.

### dhcpcd

[dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) ha la caratteristica di preporre o posporre i nameserver al file `/etc/resolv.conf` creando o modificando rispettivamente i file `/etc/resolv.conf.head` e `/etc/resolv.conf.tail`:

```
echo "nameserver 127.0.0.1" > /etc/resolv.conf.head

```

### dhclient

Per dhclient, de commentare nel file (o crearlo) `/etc/dhclient.conf`:

```
prepend domain-name-servers 127.0.0.1;

```

#### NetworkManager

NetworkManager ha la capacità di avviare `dnsmasq` dal suo file di configurazione. Aggiungere l'opzione `dns=dnsmasq` al file `NetworkManager.conf` (nella sezione `[main]` del file) e togliere dnsmasq dall'avvio automatico:

 `/etc/NetworkManager/NetworkManager.conf` 

```
[main]
plugins=keyfile
dns=dnsmasq

```

Creare la cartella di configurazione di dnsmasq per NetworkManager se non esiste:

```
mkdir /etc/NetworkManager/dnsmasq.d

```

##### Altri metodi

Se si utilizza il demone dnsmasq, allora sarà necessario aggiungere l'indirizzo di localhost al file `resolv.conf` (che NetworkManager andrà ad interrogare).

Dopo l'aggiornamento di [NetworkManager](/index.php/NetworkManager_(Italiano) "NetworkManager (Italiano)") alla versione 0.7, Arch Linux adesso richiama [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) direttamente invece di [dhclient](https://www.archlinux.org/packages/?name=dhclient) più comunemente utilizzato come default. Dati gli argomenti utilizzati con [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd), esso non legge più le configurazioni in `/etc/resolv.conf.head`, e `/etc/resolv.conf.tail` per scelta dei server DNS. Diverse opzioni sono disponibili.

La prima opzione potrebbe essere l'aggiunta di uno script al dispatcher di NetworkManager di preporre localhost in `resolv.conf`:

 `/etc/NetworkManager/dispatcher.d/localhost-prepend` 

```
#!/bin/bash                                       
# Prepone localhost in resolv.conf per dnsmasq

if [[ ! $(grep 127.0.0.1 /etc/resolv.conf) ]]; then
  sed -i '1s|^|nameserver 127.0.0.1\n|' /etc/resolv.conf
fi
```

renderlo eseguibile:

```
# chmod +x /etc/NetworkManager/dispatcher.d/localhost-prepend

```

La seconda opzione consiste nell'aprire le impostazioni di NetworkManager (solitamente facendo click con il tasto destro sopra l'applet) ed inserire le impostazioni manualmente. La configurazione dipenderà dal tipo di front-end utilizzato; il processo solitamente consiste nel fare click con li tasto destro sull'applet, modificare (o creare) un profilo, e successivamente impostare il tipo di DHCP in 'Automatic (specify addresses).' Gli indirizzi DNS dovranno essere inseriti e solitamente si utilizza questa forma: `127.0.0.1, DNS-server-one, ...`.

Ed infine, NetworkManager può essere usato con dhclient usando ([networkmanager-dhclient](https://aur.archlinux.org/packages/networkmanager-dhclient/)).

##### Configurazione personalizzata

A partire da NetworkManager 0.9.6 è possibile creare una configurazione personalizzata per dnsmasq creando i file di configurazione nella cartella `/etc/NetworkManager/dnsmasq.d/`

## DHCP Server Setup

Per default dnsmasq ha la funzionalità di server DHCP disabilitata, se si desidera utilizzarla dovrà essere attivata nel file `/etc/dnsmasq.conf`. Di seguito sono riportate le impostazioni più importanti:

```
# Ascolta solamente sulla interfaccia LAN NIC.  Così facendo apre per i 
# protocolli tcp/udp la porta 53 a localhost e per il protocollo udp la porta 67 all'esterno:
interface=<LAN-NIC>

# dnsmasq aprirà per i protocolli tcp/udp la porta 53 e udp la porta 67 all'esterno
# per aiutare con le interfacce dinamiche (assegnazione dinamica degli ip).
# Dnsmasq rifiuterà le richieste esterne, ma la paranoia può essere tale da 
# chiuderle e lasciare al kernel occuparsene:
bind-interfaces

# Range degli indirizzi IP da rendere disponibili ai pc della LAN
dhcp-range=192.168.111.50,192.168.111.100,12h

# Se si necessita di assegnare indirizzi statici, effettuare il bind tramite
# il MAC address della scheda:
dhcp-host=aa:bb:cc:dd:ee:ff,192.168.111.50
```

## Avviare il demone

Per avviare dnsmasq all'avvio:

 `# systemctl enable dnsmasq` 

Per avviarlo immediatamente:

 `# systemctl start dnsmasq` 

Per verificare se dnsmasq è stato avviato correttamente, controllare il log; dnsmasq inoltra i suoi messaggi al file `/var/log/messages.log`. La configurazione di rete dovrà essere riavviata affinché il client DHCP possa creare un nouvo `/etc/resolv.conf`.

## Test

### DNS Caching

Per effettuare un test di velocità per il lookup ad un sito che ancora non è stato visitato dall'avvio di dnsmasq (`dig` fa parte del pacchetto [dnsutils](https://www.archlinux.org/packages/?name=dnsutils)):

```
$ dig archlinux.org | grep "Query time"

```

Eseguendo ancora il comando verrà utilizzato l'indirizzo IP dalla cache DNS ed il tempo di lookup sarà molto inferiore se dnsmasq è configurato correttamente.

## DHCP Server

Da un computer che è collegato ad quello con dnsmasq, configurarlo per ottenere l'assegnamento dell'indirizzo IP mediante DHCP, successivamente tentare di accedere alla rete come di solito.

## Trucchi e consigli

### Prevenire che OpenDNS reindirizzino le query a Google

Per impedire che OpenDNS rediriga tutte le richieste a Google ai propri server di ricerca, aggiungere al file `/etc/dnsmasq.conf`:

 `server=/www.google.com/<IP DNS ISP>` 

### Visualizzare i lease

 `$ cat /var/lib/misc/dnsmasq.leases`