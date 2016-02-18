Dalla pagina di manuale [resolv.conf(5)](http://www.kernel.org/doc/man-pages/online/pages/man5/resolv.conf.5.html):

	*"Il resolver è una serie di routine della libreria C, che consentono l'accesso al DNS(Domain Name System). Il file di configurazione contiene le informazioni che verranno lette dalle suddette routine(resolver) ogni volta che un processo le richiama. Il file è strutturato in modo che sia di facile comprensione, esso contiene una lista di parole chiave e di valori che verranno passate al resolver.*

	*In un sistema correttamente configurato questo file potrebbe non essere necessario. L'unico server dei nomi(DNS) che verrà interrogato sarà la macchina stessa; il nome dominio(domain name) è determinato dal nome macchina ed il percorso del dominio di ricerca è costruito dal nome dominio."*

## Contents

*   [1 Mantenere le impostazioni dei DNS](#Mantenere_le_impostazioni_dei_DNS)
    *   [1.1 Modificare la configurazione di dhcpcd](#Modificare_la_configurazione_di_dhcpcd)
    *   [1.2 Usare /etc/resolv.conf.head](#Usare_.2Fetc.2Fresolv.conf.head)
    *   [1.3 Proteggere dalla scrittura /etc/resolv.conf](#Proteggere_dalla_scrittura_.2Fetc.2Fresolv.conf)
    *   [1.4 Usare l'opzione timeout per ridurre il tempo di loockup dei nomi host](#Usare_l.27opzione_timeout_per_ridurre_il_tempo_di_loockup_dei_nomi_host)

## Mantenere le impostazioni dei DNS

[dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd), [NetworkManager](/index.php/NetworkManager_(Italiano) "NetworkManager (Italiano)"), ed altri processi possono sovrascrivere il file `/etc/resolv.conf`. Questo funzionamento spesso è corretto, ma in alcuni casi i DNS devono essere impostati manualmente(ad esempio se si usa un indirizzo IP statico). Ci sono diversi modi per evitare la modifica del file. Se si utilizza Network Manager, consultare [questa discussione sul forum internazionale](https://bbs.archlinux.org/viewtopic.php?id=45394) su come evitare che il file `/etc/resolv.conf` venga modificato.

### Modificare la configurazione di dhcpcd

Il file di configurazione di dhcpcd può essere modificato per impedire di sovrascrivere il file `/etc/resolv.conf`. Per fare ciò sarà necessario aggiungere la seguente linea nell'ultima sezione del file `/etc/dhcpcd.conf`:

```
nohook resolv.conf

```

### Usare /etc/resolv.conf.head

Alternativamente, è possibile creare un file chiamato `/etc/resolv.conf.head` contenente i propri server DNS. dhcpcd inserirà il contenuto del file all'inizio del file `/etc/resolv.conf`. Ecco un esempio del file `/etc/resolv.conf.head` per chi usa [OpenDNS](/index.php/OpenDNS "OpenDNS"):

```
# OpenDNS servers
nameserver 208.67.222.222
nameserver 208.67.220.220

```

Se non si desidera utilizzare i server DNS di OpenDNS è possibile utilizzare in alternativa i [server DNS di Google](http://code.google.com/speed/public-dns/).

```
# Google nameservers
nameserver 8.8.8.8
nameserver 8.8.4.4

```

### Proteggere dalla scrittura /etc/resolv.conf

Un ulteriore metodo per proteggere il proprio `/etc/resolv.conf` dall'essere modificato, consiste nell'impostare l'attributo di protetto da scrittura(write-protection) sul file:

```
chattr +i /etc/resolv.conf

```

### Usare l'opzione timeout per ridurre il tempo di loockup dei nomi host

Se si notano tempi molto lunghi durante il lookup dei nomi host (sia in [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)") che durante la navigazione) spesso può essere utile definire un piccolo timeout dopo il quale verrà utilizzato un diverso `nameserver`. Per fare ciò creare un file chiamato `/etc/resolv.conf.tail` ed inserire la seguente linea:

```
options timeout:1

```

Dopodiché riavviare il demone utilizzato per la rete e controllare se si sono ottenuti dei miglioramenti.