## Introduzione

Benvenuti nella guida Arch Linux Small Business Server (**SBS** per gli amici). Questa guida contiene informazioni su come installare e configurare diversi servizi su Arch Linux allo scopo di realizzare un piccolo server tuttofare nella vostra azienda. È una guida passo-passo, orientata verso i processi per configurare e personalizzare il sistema. Le varie sezioni non vanno necessariamente eseguite in ordine ma secondo esigenza (comunque all'inizio di ogni articolo sono indicati i requisiti). La guida presuppone che :

*   Abbiate già eseguito una installazione base di Arch Linux sul vostro server, magari seguendo la [guida ufficiale](/index.php/Installation_guide "Installation guide").
*   La rete sia configurata e funzionante. Per realizzare il firewall di cui avete sicuramente bisogno dovete installare almeno due adattatori di rete, uno collegato alla vostra rete interna e uno al router ADSL. In caso di problemi consultate la relativa [guida](/index.php/Configuring_network "Configuring network"). Mi raccomando, per il vostro server **utilizzate indirizzi IP statici**.
*   Una connessione ad internet funzionante
*   Una conoscenza almeno di base su Arch Linux e sugli argomenti trattati

Preciso che questa NON è una guida completa ai servizi utilizzati, per approfondirne la conoscenza vi rimando alle guide ufficiali dei pacchetti stessi. Lo scopo principale è dare una traccia principale da seguire, le possibili combinazioni sono talmente tante che è praticamente impossibile trattare ogni singola esigenza.

Nella filosofia Arch, vi avviso che non verrà utilizzata nessuna GUI per configurare il sistema, utilizzerete solo una shell bash. Se questo non fà per voi fermatevi immediatamente qui. Usando una shell per configurare il tutto avrete il grande vantaggio di poter amministrare e risolvere gran parte dei problemi del vostro server da remoto.

Per ultimo un consiglio, anche se sembrerà una cosa ovvia io ve lo dico lo stesso: non mettete le guide in pratica a pappagallo, cercate di capire almeno a grandi linee quello che state facendo. Se stiamo installando il servizio DNS o LDAP almeno documentatevi prima su cosa diavolo siano. Non installate un server in una azienda non capendo gli argomenti trattati, altrimenti (come spesso succede) alla prima difficoltà non saprete che pesci pigliare e meledirete il momento in cui avete deciso di installare un server con Arch Linux (o Linux in generale).

Gli articoli provengono dal [Blog di Steno](http://www.stenoweb.it/taxonomy/term/6), pubblicati con licenza [CC Attribution-ShareAlike](http://creativecommons.org/licenses/by-sa/2.5/it/deed.it).

Sentitevi liberi di contribuire, magari iniziando da una traduzione in inglese per rendere più visibile la guida.

## Indice della guida

Questa è la lista degli articoli pubblicati, buona lettura, e sentitevi liberi di correggere e contribuire alla guida.

1.  [Operazioni Preliminari](/index.php/Small_Business_Server_(Italiano)/Operazioni_Preliminari "Small Business Server (Italiano)/Operazioni Preliminari")
2.  [LDAP Server](/index.php/Small_Business_Server_(Italiano)/LDAP_Server "Small Business Server (Italiano)/LDAP Server")
3.  [DNS dinamico e DHCP Server](/index.php/Small_Business_Server_(Italiano)/DNS_dinamico_e_DHCP "Small Business Server (Italiano)/DNS dinamico e DHCP")
4.  [Firewall](/index.php/Small_Business_Server_(Italiano)/Firewall "Small Business Server (Italiano)/Firewall")
5.  [File Server Domain Controller](/index.php/Small_Business_Server_(Italiano)/File_Server_Domain_Controller "Small Business Server (Italiano)/File Server Domain Controller")
6.  [Mail Server](/index.php/Small_Business_Server_(Italiano)/Mail_Server "Small Business Server (Italiano)/Mail Server")

E questa la lista degli articoli mancanti :

1.  [LAMP Server](/index.php?title=Small_Business_Server_(Italiano)/LAMP_Server&action=edit&redlink=1 "Small Business Server (Italiano)/LAMP Server (page does not exist)")
2.  [Proxy Server](/index.php?title=Small_Business_Server_(Italiano)/Proxy_Server&action=edit&redlink=1 "Small Business Server (Italiano)/Proxy Server (page does not exist)")
3.  [VPN Server](/index.php?title=Small_Business_Server_(Italiano)/VPN_Server&action=edit&redlink=1 "Small Business Server (Italiano)/VPN Server (page does not exist)")
4.  [Fax Server](/index.php?title=Small_Business_Server_(Italiano)/Fax_Server&action=edit&redlink=1 "Small Business Server (Italiano)/Fax Server (page does not exist)")

Iniziamo la configurazione del nostro Arch Linux SBS con delle operazioni preliminari per rendere la nostra box pronta al via.