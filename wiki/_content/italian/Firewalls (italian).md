Un firewall é un sistema destinato a prevenire accessi non autorizzati ad una rete privata (che può essere anche una singola macchina) o provenienti da essa. Il firewall può essere realizzato mediante hardware, software o da una combinazione. I firewall sono frequentemente impiegati per impedire ad utenti di internet non autorizzati di connettersi a reti private collegate con internet, specialmente reti intranet. Tutti i pacchetti in entrata ed in uscita dalla intranet passano attraversano il firewall che esamina ogni pacchetto e ne permette l'ingresso, ne permette il transito, oppure lo nega ai pacchetti in base a criteri di sicurezza specificati.

Si può trovare una buona lista di firewalls [quì](http://wiki.debian.org/Firewalls). Ed un confronto tra alcuni firewall [qui](http://www.securityfocus.com/infocus/1410).

Ci sono molti post nei forum riguardo alle differenti applicazioni firewall e scripts, così sono stati riuniti qui in un'unica pagina - per favore aggiungete i vostri commenti riguardo ad ogni firewall, specialmente facilità d'uso e controlli di sicurezza in [Shields Up](https://www.grc.com/x/ne.dll?bh0bkyd2)

**Nota:** I controlli di Shields Up sono solo una valida misura per il proprio router e dovrebbe essercene uno nella propria LAN. Per valutare accuratamente un firewall software, sarà necessario connettere la propria Linux box direttamente sul cavo del modem.

## Contents

*   [1 iptables front-ends](#iptables_front-ends)
    *   [1.1 Arno's Firewall](#Arno.27s_Firewall)
    *   [1.2 ferm](#ferm)
    *   [1.3 Firehol](#Firehol)
    *   [1.4 Firetable](#Firetable)
    *   [1.5 Shorewall](#Shorewall)
    *   [1.6 ufw](#ufw)
    *   [1.7 Vuurmuur](#Vuurmuur)
*   [2 iptables GUIs](#iptables_GUIs)
    *   [2.1 Firestarter](#Firestarter)
    *   [2.2 Uncomplicated firewall (ufw) front-end](#Uncomplicated_firewall_.28ufw.29_front-end)
    *   [2.3 KMyFirewall](#KMyFirewall)
*   [3 Firewall Builder](#Firewall_Builder)
*   [4 Altri](#Altri)

*   **[Iptables](/index.php/Iptables "Iptables")** — Iptables è un potente <a class="mw-selflink selflink">firewall</a> integrato nel kernel Linux ed è una parte del progetto [netfilter](https://en.wikipedia.org/wiki/it:Netfilter "wikipedia:it:Netfilter"). Gli altri firewall sono solamete dei front-end grafici.

	**Vedi anche:**

*   [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall")
*   [Router](/index.php/Router "Router")
*   [iptables(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/iptables.8) – [http://unixhelp.ed.ac.uk/CGI/man-cgi?iptables+8](http://unixhelp.ed.ac.uk/CGI/man-cgi?iptables+8)
*   [http://tldp.org/HOWTO/Masquerading-Simple-HOWTO/](http://tldp.org/HOWTO/Masquerading-Simple-HOWTO/)
*   [http://netfilter.org/documentation/HOWTO/NAT-HOWTO.html](http://netfilter.org/documentation/HOWTO/NAT-HOWTO.html)
*   [http://www.frozentux.net/documents/iptables-tutorial/](http://www.frozentux.net/documents/iptables-tutorial/)

	[http://www.netfilter.org/projects/iptables/index.html](http://www.netfilter.org/projects/iptables/index.html) || [iptables](https://www.archlinux.org/packages/?name=iptables)

## iptables front-ends

### Arno's Firewall

[Arno's IPTABLES Firewall Script](http://rocky.eld.leidenuniv.nl/)é un firewall sicuro sia per macchine singole che multi utente.

Lo script:

*   FACILE da configurare e altamente personalizzabile,
*   script dei demoni inclusi,
*   uno script filtro che rende il file di log maggiormente leggibile.

Supporta:

*   NAT and SNAT
*   port forwarding
*   ADSL ethernet modems con assegnazione degli indirizzi IP sia statica che dinamica
*   MAC address filtering
*   stealth port scan detection
*   DMZ and DMZ-2-LAN forwarding
*   protezione contro SYN/ICMP flooding
*   log definibili dall'utente con cadenze e limiti per evitare di riempire di log il disco.
*   tutti i protocolli IP e VPNs come IPsec
*   supporto per le i plugin per aggiungere funzionalità aggiuntive.

### ferm

[ferm](http://ferm.foo-projects.org/) (acronimo di "For Easy Rule Making") è un tool per gestire firewall complessi senza avere il problema di riscrivere regole complesse innumerevoli volte. ferm permette di salvare l'intero set di regole in un file separato e di caricarlo con un comando. La configurazione del firewaal assomiglia ad un linguaggio di programmazione strutturato, che può contenere livelli e liste.

### Firehol

[FireHOL](http://firehol.sourceforge.net/) è un linguaggio per esprimere le regole del firewall, non solo uno script che produce qualche tipo di firewall. Rende facile costruire anche un sofisticato firewall come si desidera.

[firehol](https://aur.archlinux.org/packages/firehol/) è disponibile nei [[Official Repositories (Italiano)|repository ufficiali].

### Firetable

[Firetable](http://projects.leisink.net/firetable) basato su iptables con una sintassi "human readable".

[firetable](https://aur.archlinux.org/packages/firetable/) è disponibile su [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)").

### Shorewall

Il [Shoreline Firewall](http://www.shorewall.net/), più comunemente conosciuto come "Shorewall", é un'utilità di alto livello per configurare Netfilter. Descrivi le richieste del tuo firewall/gateway utilizzando entrate (using entries) in un set di file di configurazione. Shorewall legge questi file di configurazione e con l'aiuto di iptables utility, configura Netfilter per incontrare le tue richieste. Shorewall può essere usato su un sistema firewall dedicato, un gateway/router/server multifunzione o su un sistema GNU/Linux singolo. Shorewall non usa il (Netfilter's ipchains compatibility mode) e può quindi avvantaggiarsi del tracking dello stato delle connessioni fornito da Netfilter.

[shorewall](https://www.archlinux.org/packages/?name=shorewall) è disponibile nei [[Official Repositories (Italiano)|repository ufficiali].

### ufw

[ufw](https://www.archlinux.org/packages/?name=ufw) (uncomplicated firewall) è un semplice front-end per `iptablesis` ed è disponibile nei [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

Consultare [Uncomplicated Firewall](/index.php/Uncomplicated_Firewall "Uncomplicated Firewall") per maggiori informazioni.

### Vuurmuur

[Vuurmuur](http://www.vuurmuur.org/) è un potente firewall manager costruito per `iptables`. Ha una configurazione semplice e facile da imparare che permette sia configurazioni semplici che complesse. La configurazione può essere effettuata mediante una interfaccia [ncurses](https://www.archlinux.org/packages/?name=ncurses), che permette una configurazione remota sicura tramite [SSH](/index.php/Secure_Shell_(Italiano) "Secure Shell (Italiano)") oppure dalla console. Vuurmuur supporta il traffic shaping, ha funzioni di monitoraggio potenti, che permettono all'amministratore di consultare i log, le connessioni e l'utilizzo della banda in tempo reale.

[Vuurmuur](https://aur.archlinux.org/packages/Vuurmuur/) è disponibile su [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)").

## iptables GUIs

### Firestarter

[Firestarter](http://www.fs-security.com/) è una buona interfaccia grafica per `iptables` scritto in GTK2, ha la possibilità di usare sia una blacklist che una whitelist per regolare il traffico, è molto semplice da usare, e dispone di una buona documentazione sul proprio sito web.

[firestarter](https://aur.archlinux.org/packages/firestarter/) utilizza le dipendenze di [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)") ed è disponibile su [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)").

### Uncomplicated firewall (ufw) front-end

[Gufw](/index.php/Uncomplicated_Firewall#Gufw "Uncomplicated Firewall"), è un front-end basato sulle GTK per [ufw](https://www.archlinux.org/packages/?name=ufw) che è un front-end da linea di comando per `iptables` (gufw->ufw->iptables), ed è molto semplice e facile da usare.

**Nota:** `Gufw` è un semplice rimpiazzo per `tcp_wrappers`, che [attualmente è deprecato](https://www.archlinux.org/news/dropping-tcp_wrappers-support/).

[kcm-ufw](/index.php/Uncomplicated_Firewall#kcm-ufw "Uncomplicated Firewall") è una alternativa per [KDE](/index.php/KDE_(Italiano) "KDE (Italiano)") a Gufw.

Consultare [Uncomplicated Firewall](/index.php/Uncomplicated_Firewall#GUI_frontends "Uncomplicated Firewall") per maggiori informazioni.

### KMyFirewall

[KMyFirewall](http://kmyfirewall.sourceforge.net/) è una interfaccia grafica per KDE3 di `iptables`.

Le modalità di configurazione sono abbastanza semplici per essere adatto ai principianti, ma permette anche sofisticati tweak per la configurazione delle impostazioni del firewall.

[KMyFirewall](https://aur.archlinux.org/packages/KMyFirewall/) richiede [kdelibs3](https://aur.archlinux.org/packages/kdelibs3/) ed è disponibile su [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)").

## Firewall Builder

[Firewall Builder](http://www.fwbuilder.org/) è "una interfaccia di configurazione e gestione che supporta iptables (netfilter), ipfilter, pf, ipfw, Cisco PIX (FWSM, ASA) ed l'extended access list dei router. [...] Questo programma è disponibile per Linux, FreeBSD, OpenBSD, Windows e Mac OS X e può gestire sia firewall locali che remoti." Da: [http://www.fwbuilder.org/](http://www.fwbuilder.org/)

[fwbuilder](https://www.archlinux.org/packages/?name=fwbuilder) è disponibile nei [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

## Altri

*   **[EtherApe](https://en.wikipedia.org/wiki/EtherApe "wikipedia:EtherApe")** — Un monitor di rete grafico per i vari strati OSI e protocolli.

	[http://etherape.sourceforge.net/](http://etherape.sourceforge.net/) || [etherape](https://www.archlinux.org/packages/?name=etherape)

*   **[Fail2ban](/index.php/Fail2ban "Fail2ban")** — Effettua il ban degli indirizzi IP con troppi fallimenti di autenticazione nei confronti dei demoni più comuni.

	[http://www.fail2ban.org/](http://www.fail2ban.org/) || [fail2ban](https://www.archlinux.org/packages/?name=fail2ban)