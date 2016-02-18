`/etc/rc.conf` è il file di configurazione di sistema per le impostazioni specifiche di Arch. Al suo interno è possibile impostare alcuni dei settaggi più comuni come timezone, keymap, moduli del kernel e demoni da caricare all'avvio, etc.

## Contents

*   [1 Introduzione](#Introduzione)
*   [2 Localizzazione](#Localizzazione)
*   [3 Hardware](#Hardware)
*   [4 Gestione della rete](#Gestione_della_rete)
    *   [4.1 Interfaccia Singola](#Interfaccia_Singola)
    *   [4.2 Interfacce Multiple](#Interfacce_Multiple)
    *   [4.3 Network Persist](#Network_Persist)
*   [5 Demoni](#Demoni)

## Introduzione

L'aspetto generale del file `rc.conf` è molto cambiato nel corso di Gennaio 2012\. Molti dei commenti sono stati rimossi e trasferiti in maniera più esplicativa all'interno della pagina di manuale relativa. Di seguito un esempio di come apparirà il file `/etc/rc.conf` su di un sistema aggiornato (([versione corrente](https://projects.archlinux.org/initscripts.git/tree/rc.conf)):

 `/etc/rc.conf` 
```
#
# /etc/rc.conf - Main Configuration for Arch Linux
#	
# See 'man 5 rc.conf' for more details
# 

# LOCALIZATION
# ------
HARDWARECLOCK="UTC"
TIMEZONE="Europe/Rome"
KEYMAP="us"
CONSOLEFONT=
CONSOLEMAP=
LOCALE="it_IT.UTF-8"
DAEMON_LOCALE="yes"
USECOLOR="yes"

# HARDWARE
# -------
MODULES=()
USEDMRAID="no"
USEBTRFS="no"
USELVM="no"

# NETWORKING
# --------
HOSTNAME="myhost"
interface=
address=
netmask=
broadcast=
gateway=

NETWORK_PERSIST="no"

# DAEMONS
# --------
#
DAEMONS=(syslog-ng network crond)

```

## Localizzazione

	`HARDWARECLOCK` (OPZIONALE)

	specifica se l'orologio di sistema, che viene sincronizzato ad ogni avvio e spegnimento del sistema, utilizza il formato `UTC` o `localtime`. Se questa variabile non viene impostata, il sistema utilizzerà il valore memorizzato da `hwclock` all'interno di `/var/lib/hwclock/adjtime`. Consultare [Time](/index.php/Time "Time") per ulteriori informazioni

1.  `UTC` semplifica di molto la gestione del fuso orario e del cambio ora solare/legale. Linux effettuerà questo scambio automaticamente, indipendentemente dall'orario in corso nel momento in cui è stato avviato.
2.  `localtime` è necessario se si utilizza in dual-boot un sistema operativo che gestisce l'orario solo in modalità `localtime` (come windows). Linux non si occuperà di modificare l'orario, dando per scontato che sia presente su quella macchina un dual-boot, e che l'altro sistema oèerativo si occuperà di gestire il passaggio ora legale/solare. Se questo non dovesse avvenire, sarebbe necessario effettuare il cambiamento manualmente.
3.  vuoto: viene impostato al valore presente in `/var/lib/hwclock/adjtime`, che di default è quello di UTC. È raccomandato, in quanto altri utenti di hwclock potrebbero modificare il file adjtime e rendere quindi rc.conf ed adjtime non sincronizzati.
4.  qualsiasi altro valore comporterà che l'orologio hardware venga lasciato inalterato. (utile per la virtualizzazione).

	`[TIMEZONE](/index.php/TIMEZONE "TIMEZONE")`

	Specifica il proprio fuso orario. I possibili valori sono i percorsi relativi al proprio fuso orario all'interno della directory `/usr/share/zoneinfo`. Il fuso orario standard italiano sarà quindi `Europe/Rome`, che fa riferimento al file `/usr/share/zoneinfo/Europe/Rome`.

**Tip:** Se questa variabile non viene impostata, la timezone viene lasciata così com'è, e può essere resettata modificando manualmente `/etc/localtime`.

	`[KEYMAP](/index.php/KEYMAP "KEYMAP")`

	Il layout di tastiera che si desidera utilizzare. Lo standard italiano è "it". I possibili valori sono consultabili in `/usr/share/kbd/keymaps`.

**Nota:** Il settaggio di questo campo imposta la tastiera solo ed esclusivamente per la console, non è valido per il server grafico X.

	`[CONSOLEFONT](/index.php/Fonts#Console_fonts "Fonts")` Definisce il font che deve essere caricato all'avvio tramite il comando setfont per essere utilizzato nella console. I possibili valori sono consultabili in `/usr/share/kbd/consolefonts`. Per maggiori informazioni cosultare

	[Fonts in console](/index.php/Fonts#Fonts_in_virtual_console "Fonts")

	`[CONSOLEMAP](/index.php/Fonts#Console_fonts "Fonts")`

	Definisce la mappa di console da caricare all'avvio con il comando setfont. Le possibili mappe sono consultabili in `/usr/share/kbd/consoletrans`. E' consigliabile impostare una mappa compatibile con il proprio locale (8859-1 per Latin1, ad esempio).

**Nota:** Se normalmente utilizzate X11 non preoccupatevene, questa impostazione influenza solo ed esclusivamente la console.

	`[LOCALE](/index.php/LOCALE "LOCALE")`

	Qui viene impostata la lingua di sistema, che verrà utilizzata da tutte le applicazioni i18n-compatibili. Potete avere un elenco completo di tutte le lingue disponibili eseguendo `locale -a` da linea di comando. All'inizio troverete l'impostazione per l'inglese US, per impostare l'italiano come lingua di sistema inserite "it_IT.utf8" (ricordatevi poi di decommentare la relativa linea nel file `/etc/locale.gen` e di eseguire il comando `locale-gen` per rigenerare i file di sistema relativi alla lingua). La variabile `LANG` all'interno di `[/etc/locale.conf](/index.php/Locale.conf "Locale.conf")`, se impostata ha la precedenza, e gli utenti di shell di login che non possono effettuare il source di `/etc/rc.conf`, dovrebbero servirsi di quest'ultima.

	`DAEMON_LOCALE`

	Se impostato su Yes, utilizza `$LOCALE` come localizzazione durante l'avvio. Se impostato su No, verrà utilizzata la localizzazione **C**. Il valore di default è Yes.

	`USECOLOR`

	Abilita (o disabilita) i messaggi di stato colorati all'avvio.

## Hardware

	`MODULES`

	In questa lista vanno elencati tutti i moduli che si vogliono caricare all'avvio in aggiunta a quelli caricati automaticamente. Per il blacklisting dei moduli, consultare [Kernel modules (Italiano)#Blacklist](/index.php/Kernel_modules_(Italiano)#Blacklist "Kernel modules (Italiano)")

**Nota:** `MOD_AUTOLOAD` è deprecato a partire dalla versione 2011.06.1-1 del pacchetto initscripts e non ha effetto. È possibile utilizzare le regole di [udev](/index.php/Udev_(Italiano) "Udev (Italiano)") per ottenere le stesse funzionalità.

**Tip:** Non è detto che i moduli qui elencati, vengano effettivamente caricati nello stesso ordine, in quanto potrebbero anche venire caricati su richiesta da [udev](/index.php/Udev "Udev"). Ad es., per essere certi che le interfacce di rete non cambino nome ad ogni riavvio, la cosa migliore è creare [una regola di udev apposita](/index.php/Udev_(Italiano)#Ordinamento_delle_periferiche.2C_schede_di_rete.2Faudio_che_cambiano_ordine_ad_ogni_avvio "Udev (Italiano)").

	`USEDMRAID`

	Controlla la presenza di volumi FakeRAID (dmraid) all'avvio (esegue `dmraid -i -ay`).

	`USEBTRFS`

	Controlla la presenza di volumi BTRFS all'avvio. . Esegue `btrfs device scan` da `/etc/rc.sysinit`.

	`USELVM`

	Scansiona i volumi [LVM](/index.php/LVM "LVM") all'avvio, necessario se usate LVM. Se impostato a `YES` effettua `vgchange --sysinit -a y` (gestito dalla funzione activate_vgs()) durante il sysinit.

## Gestione della rete

	`[HOSTNAME](/index.php/HOSTNAME "HOSTNAME")`

	Imposta il nome dell'host, tralasciando il dominio. Può essere impostato arbitrariamente, utilizzando però solo caratteri tipo lettere, numeri e pochi altri come "-". Può essere impostato anche all'interno di `/etc/hosts`. Il contenuto di `/etc/hosts` (se non vuoto) ha la precedenza.

*   Sono disponibili due metodi per configurare la gestione della rete tramite `/etc/rc.conf`. Il metodo "A Interfaccia Singola" (interface,address,netmask,gateway), ed il metodo `NETWORKS`/ [netcfg](/index.php/Netcfg_(Italiano) "Netcfg (Italiano)"). La variabile `DAEMONS` dovrebbe riflettere il metodo scelto.

### Interfaccia Singola

	`interface`

	nome del dispositivo (richiesto)

	`address`

	indirizzo IP (lasciare vuoto per DHCP)

	`netmask`

	maschera di sottorete (ignorata per DHCP) (opzionale, di defaults impostata a 255.255.255.0)

	`broadcast`

	indirizzo di broadcast (ignorato per DHCP) (opzionale)

	`gateway`

	default route (ignorato per DHCP)

 `Static IP Example` 
```
interface=eth0
address=192.168.0.2
netmask=255.255.255.0
broadcast=192.168.0.255
gateway=192.168.0.1
```
 `DHCP example` 
```
interface=eth0
address=
netmask=
gateway=
```

**Nota:** Assicurarsi di aggiungere `network` a `DAEMONS` `DAEMONS=(... network sshd)` 

### Interfacce Multiple

Il pacchetto [netcfg](/index.php/Netcfg_(Italiano) "Netcfg (Italiano)") è utilizzato per configurare interfacce multiple creando un profilo per ognuna di esse.

1.  Creare un profilo di rete `/etc/network.d/profilename` per ogni interfaccia
    1.  Esempio statico: `/etc/network.d/eth0-static`
        ```
        CONNECTION='ethernet'
        DESCRIPTION='Una connessione ethernet statica per l'interfaccia eth0'
        INTERFACE='eth0'
        IP='static'
        ADDR='192.168.1.24'
        NETMASK='255.255.255.0'
        BROADCAST='192.168.1.255'
        GATEWAY='192.168.1.1'
        ```

    2.  Esempio DHCP: `/etc/network.d/eth1-dhcp`
        ```
        CONNECTION='ethernet'
        DESCRIPTION='Una connessione dhcp di base su eth1'
        INTERFACE='eth1'
        IP='dhcp'
        ```

2.  Aggiungere ogni profilo di rete all'array `NETWORKS`. `NETWORKS=(eth0-static eth1-dhcp)` 
3.  Aggiungere `net-profiles` alla lista `DAEMONS`. `DAEMONS=(... net-profiles sshd)` 

### Network Persist

La variabile `NETWORK_PERSIST` indica al sistema se impedire o meno lo spegnimento delle interfacce di rete. È indispensabile se la partizione di root è su un volume NFS. Di default è impostata su"no".

```
# default
NETWORK_PERSIST="no"

# NFS-based root device
# NETWORK_PERSIST="yes"

```

## Demoni

	`[DAEMONS](/index.php/DAEMONS "DAEMONS")`

	Questo array è una semplice lista di nomi, corrispondenti ai nomi dei file contenuti in `/etc/rc.d/`, utili all'avvio dei demoni desiderati durante il bootup del sistema. Di solito non è necessario modificare le impostazioni predefinite per ottenere un sistema funzionante, ma si dovrà modificare questa stringa ogni volta che si installa un qualche servizio di sistema, come ad esempio `sshd`, e si vuole avviarlo automaticamente durante il boot. Questa è la modalità in cui Arch gestisce quello che normalmente le altre distribuzioni gestiscono tramite collegamenti simbolici ad una directory `init.d`. Per ulteriori informazioni, consultare [Writing rc.d scripts](/index.php/Writing_rc.d_scripts "Writing rc.d scripts")

1.  Se il nome di un demone viene preceduto da un "!" il corrispettivo script non sarà avviato.
2.  Se viene usato il prefisso "@" il demone verrà avviato in background, ovvero la sequenza di boot non attenderà il termine dell'esecuzione del relativo script per proseguire.

	Esempio:

	 `DAEMONS=(@syslog-ng !network net-profiles crond sshd)` 

**Nota:** L'ordine di comparsa all'interno dell'array è importante, in quanto si tratta dell'ordine esatto in cui i demoni verranno avviati.