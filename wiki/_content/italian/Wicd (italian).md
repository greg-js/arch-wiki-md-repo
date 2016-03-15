[Wicd](http://www.wicd.net/) è un gestore delle connessioni capace di gestire sia le interfacce wireless che quelle cablate, simile ed alternativo a [Network Manager](/index.php/NetworkManager_(Italiano) "NetworkManager (Italiano)"). Wicd è scritto in [Python](/index.php/Python "Python") e [GTK+](/index.php/GTK%2B_(Italiano) "GTK+ (Italiano)"), e necessita dell'installazione di un minor numero di dipendenze rispetto agli altri network manager. Alternativamente, una versione di Wicd per [KDE](/index.php/KDE_(Italiano) "KDE (Italiano)"), scritta con le Qt, è disponibile su [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)"). Wicd può anche essere eseguito da terminale, utilizzando una interfaccia disegnata con le librerie curses, non necessita di un server grafico avviato oppure un di un vassoio di sistema o di un area di notifica (si veda il paragrafo [Eseguire Wicd](/index.php/Wicd_(Italiano)#Eseguire_Wicd "Wicd (Italiano)")).

## Contents

*   [1 Installazione](#Installazione)
    *   [1.1 Alternative](#Alternative)
*   [2 Per Iniziare](#Per_Iniziare)
    *   [2.1 Configurazione Iniziale](#Configurazione_Iniziale)
    *   [2.2 Eseguire Wicd in modalità grafica](#Eseguire_Wicd_in_modalit.C3.A0_grafica)
    *   [2.3 Eseguire Wicd in modalità testuale](#Eseguire_Wicd_in_modalit.C3.A0_testuale)
*   [3 Risoluzione di problemi](#Risoluzione_di_problemi)
    *   [3.1 Errore nell'acquisizione dell'indirizzo IP](#Errore_nell.27acquisizione_dell.27indirizzo_IP)
    *   [3.2 Importing pynotify failed, notifications disabled](#Importing_pynotify_failed.2C_notifications_disabled)
    *   [3.3 Messaggio di errore di connessione con Dbus](#Messaggio_di_errore_di_connessione_con_Dbus)
    *   [3.4 Problemi dopo l'aggiornamento del pacchetto](#Problemi_dopo_l.27aggiornamento_del_pacchetto)
    *   [3.5 Alcune note sui front-end grafici per sudo](#Alcune_note_sui_front-end_grafici_per_sudo)
    *   [3.6 Configurare wicd per eduroam](#Configurare_wicd_per_eduroam)
    *   [3.7 Problemi al passaggio da wicd ad un altro network manager](#Problemi_al_passaggio_da_wicd_ad_un_altro_network_manager)
    *   [3.8 Due processi wicd-client (ed eventualmente due icone nell'aria di notifica)](#Due_processi_wicd-client_.28ed_eventualmente_due_icone_nell.27aria_di_notifica.29)
    *   [3.9 Password errata usando PEAP con TKIP/MSCHAPV2](#Password_errata_usando_PEAP_con_TKIP.2FMSCHAPV2)
*   [4 Altre risorse](#Altre_risorse)

## Installazione

[Installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") il pacchetto [wicd](https://www.archlinux.org/packages/?name=wicd) dai [repository ufficiali](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)").

Questo installerà Wicd (**il client da linea di comando, l'interfaccia ncurses ed il demone**) e tutte le dipendenze necessarie.

Se non si utilizza [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)") (oppure il suo demone di notifica), è possibile installare [xfce4-notifyd](https://www.archlinux.org/packages/?name=xfce4-notifyd) dai [reopository ufficiali](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)"), prima di installare l'interfaccia [wicd-gtk](https://www.archlinux.org/packages/?name=wicd-gtk) per evitare di installare il demone di notifica di GNOME e le sue relative dipendenze, che non sempre sono necessarie.

Installare quindi il pacchetto [wicd-gtk](https://www.archlinux.org/packages/?name=wicd-gtk) per ottenere **l'interfaccia scritta in GTK e l'icona nell'aria di notifica**.

**Nota:** Questo pacchetto comprende solo l'interfaccia scritta in GTK, non è quindi necessario se si intende utilizzare Wicd tramite l'interfaccia da linea di comando (CLI).

Per installare il client per [KDE](/index.php/KDE_(Italiano) "KDE (Italiano)") sarà necessario il pacchetto [wicd-kde](https://aur.archlinux.org/packages/wicd-kde/) presente su [AUR](/index.php/Arch_User_Repository "Arch User Repository").

**Nota:** Questo pacchetto comprende solo l'interfaccia per KDE ed installerà wicd come dipendenza.

**Nota:** A partire dal 20-3-2011 il pacchetto "wicd" dai repositroy standard è stato suddiviso in più pacchetti:

[wicd](https://www.archlinux.org/packages/?name=wicd): Include tutto il necessario per eseguire il demone wicd, il client per linea di comando(`wicd-cli`) e l'interfaccia da terminale(`wicd-curses`).

[wicd-gtk](https://www.archlinux.org/packages/?name=wicd-gtk): Include il necessario per eseguire la sola interfaccia GTK di wicd ed il file per l'avvio automatico per l'icona nell'aria di notifica.

### Alternative

Lo script di build [wicd-bzr](https://aur.archlinux.org/packages/wicd-bzr/) è disponibile su [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)"), il quale effettuerà la compilazione dell'ultimo ramo di sviluppo.

Se si necessita di una versione alternativa o se si vuole modificare il pacchetto, sarà possibile compilarlo in maniera semplice usando [ABS](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)").

## Per Iniziare

### Configurazione Iniziale

Wicd fornisce un demone che deve essere avviato.

**Attenzione:** Eseguire diversi network manager contemporaneamente *porterà* problemi, quindi è importante *disabilitare l'avvio di tutti gli altri demoni di gestione delle reti* (tipo netctl, netcfg, dhcpcd, NetworkManager).

Avviare il [demone](/index.php/Daemon_(Italiano) "Daemon (Italiano)") di wicd e abilitarlo all'avvio del sistema:

```
# systemctl start wicd
# systemctl enable wicd

```

Aggiungere il proprio account al gruppo users: (potrebbe essere necessario effettuare nuovamente il login)

```
# gpasswd -a USERNAME users

```

### Eseguire Wicd in modalità grafica

Per avviare l'interfaccia grafica di Wicd, eseguire:

```
$ wicd-client

```

Per forzare l'avvio minimizzato in un area di notifica, eseguire:

```
$ wicd-client --tray

```

Oppure se il proprio desktop environment non comprende una area di notifica, eseguire:

```
$ wicd-client -n

```

**Nota:** Questo funziona solo se è stato installato [wicd-gtk](https://www.archlinux.org/packages/?name=wicd-gtk). Se non è stato installato, allora usare i comandi `wicd-cli` oppure `wicd-curses`.

Sarà possibile aggiungere `wicd-client` nell'avvio automatico del proprio DE/WM, in modo da avviare il programma ad ogni accesso.

**Nota:** Alcuni utenti hanno ricontrato che il programma viene avviato due volte usando questo metodo. Esiste una discussione al riguardo nel forum internazionale di Arch ed su Arch bug reports (vedere [Collegamenti esterni](/index.php/Wicd_(Italiano)#Collegamenti_esterni "Wicd (Italiano)")).

Sembra che il pacchetto wicd inserisca un file nel percorso `/etc/xdg/autostart/wicd-tray.desktop`, che avvierà il client all'accesso del proprio DE/WM. Se ci si trova in questo caso si avranno due processi `wicd-client` in esecuzione, se si è aggiunto manualmente l'avvio del client al proprio DE/WM.

Se dovesse succedere, questo conferma l'esistenza del file `wicd-tray.desktop` nel percorso `/etc/xdg/autostart`; quindi, sarà sufficiente aver inserito `wicd` nella lista di demoni in `/etc/rc.conf`.

### Eseguire Wicd in modalità testuale

E' possibile eseguire wicd da terminale con il seguente comando:

```
$ wicd-cli

```

oppure con:

```
$ wicd-curses

```

**Nota:** Wicd non richiederà l'inserimento di chiavi per le reti wireless. Per accedere a reti criptate (WPA/WEP), sarà necessario utilizzare le opzioni avanzate della rete alla quale ci si vuole connettere ed inserire le informazioni necessarie. Espandere la rete a cui ci si vuole connettere, cliccare il pulsante **Advanced** ed inserire le informazioni necessarie.

## Risoluzione di problemi

### Errore nell'acquisizione dell'indirizzo IP

Se wicd ripetutamente fallisce nell'acquisizione di un indirizzo IP usando il client di default `dhcpcd`, provare installando ed usando [dhclient](https://www.archlinux.org/packages/?name=dhclient):

```
# pacman -S dhclient

```

Non dimenticare di selezionare `dhclient` come client dhcp predefinito, all'interno delle impostazioni di wicd.

Se wicd riesce ad ottenere un indirizzo IP per l'interfaccia cablata ma rimane inutilizzabile per le interfacce wireless, provare a disabilitare le impostazioni di risparmio energetico della scheda wireless:

```
# iwconfig wlan0 power off

```

### Importing pynotify failed, notifications disabled

Nel caso che il pacchetto non venga installato automaticamente -- il nome del pacchetto è [python-notify](https://www.archlinux.org/packages/?name=python-notify):

### Messaggio di errore di connessione con Dbus

Se wicd smette improvvisamente di funzionare ed il responsabile è dbus, è molto probabile che sia necessario rimuovere completamente wicd, incluse le sue configurazioni, e successivamente reinstallarlo:

```
# pacman -R wicd
# rm -rf /etc/wicd /var/log/wicd /etc/dbus-1/system.d/wicd*
# pacman -S wicd

```

Visitare [questo sito](https://bbs.archlinux.org/viewtopic.php?pid=577141#p577141) per maggiori dettagli.

Wicd-client restituisce messaggi di errore relativi a dbus ("Could not connect to wicd's D-Bus interface.") quando il demone `wicd` non è in esecuzione a causa di un problema con un file di configurazione. Può capitare che un account vuoto venga aggiunto al file `/etc/wicd/wired-settings.conf`, in questo caso basterà modificare il file rimuovendo questa linea:

```
[] 

```

e riavviare wicd.

### Problemi dopo l'aggiornamento del pacchetto

A volte il client di wicd non si avvia dopo un aggiornamento, a causa di errori di dbus.

Una soluzione consiste nel rimuovere i file di configurazione nella directory `/etc/wicd/`

```
# rc.d stop wicd
# rm /etc/wicd/*.conf
# rc.d start wicd

```

### Alcune note sui front-end grafici per sudo

Se si ottiene un errore da wicd, che non trova un programma grafico per `sudo`, eseguire uno dei seguenti comandi:

```
$ ktsuss wicd-client -n

```

```
$ gksudo wicd-client -n

```

```
$ kdesu wicd-client -n

```

Questi comandi richiedono rispettivamente l'installazione del pacchetto [ktsuss](https://aur.archlinux.org/packages/ktsuss/) (che si trova su AUR), [gksu](https://www.archlinux.org/packages/?name=gksu) e [kdesu](https://www.archlinux.org/packages/?name=kdesu).

### Configurare wicd per eduroam

**Nota:** Si consiglia di provare prima il pacchetto presente su AUR [wicd-eduroam](https://aur.archlinux.org/packages/wicd-eduroam/). Apparirà in wicd l'opzione per "eduroam". Se non funziona, provare la seguente procedura.

Questo profilo funzionerà solamente per le istituzioni [eduroam](https://en.wikipedia.org/wiki/eduroam "wikipedia:eduroam") che usano il protocollo [TTLS](https://en.wikipedia.org/wiki/TTLS "wikipedia:TTLS") ma non funzionerà nel caso venga usato il protocollo [PEAP](https://en.wikipedia.org/wiki/Protected_Extensible_Authentication_Protocol "wikipedia:Protected Extensible Authentication Protocol")

Creare il seguente file `/etc/wicd/encryption/templates/ttls-80211`

 `/etc/wicd/encryption/templates/ttls-80211` 
```
name = TTLS for Wireless
author = Alexander Clouter
version = 1
require anon_identity *Anonymous_Username identity *Identity password *Password 
optional ca_cert *Path_to_CA_Cert cert_subject *Certificate_Subject
-----
ctrl_interface=/var/run/wpa_supplicant
network={
       ssid="$_ESSID"
       scan_ssid=$_SCAN

       key_mgmt=WPA-EAP
       eap=TTLS

       ca_cert="$_CA_CERT"
       subject_match="$_CERT_SUBJECT"

       phase2="auth=MSCHAPv2 auth=PAP"

       anonymous_identity="$_ANON_IDENTITY"
       identity="$_IDENTITY"
       password="$_PASSWORD"
}
```

Aprire un terminale e digitare:

```
cd /etc/wicd/encryption/templates
echo ttls-80211 >> active

```

Aprire wicd, scegliere TTLS per la cifratura, nelle impostazioni del profilo eduroam ed inserire i parametri appropriati per la propria connessione. Il formato per il soggetto dovrebbe essere un valore simile a "/CN=server.example.com".

**Nota:** Questa impostazione funziona in alcuni casi commentando `subject_match`, che rende la connessione meno sicura, però garantisce comunque la connessione.

### Problemi al passaggio da wicd ad un altro network manager

Per passare ad un altro demone di gestione delle reti (senza disinstallare wicd), modificare il file `/etc/rc.conf` ed anteporre il simbolo di `!` al demone `wicd` e rimuovere quello che precede il gestore di rete che si intende utilizzare (oppure inserire il demone nell'array se non è presente). Dopo aver riavviato, il demone `wicd` non verrà caricato, però alcuni utenti hanno riscontrato che il client cerca sempre di avviarsi, restituendo un errore di mancata esecuzione del demone. Questo anche se non si è inserito il client nel proprio autostart, il problema risiede in `/etc/xdg/autostart`, quindi editare il file:

```
# nano /etc/xdg/autostart/wicd-tray.desktop

```

e rendere nascosto l'avvio dell'applicazione, oppure se si pensa di non avviare automaticamente wicd-client, sarà possibile cancellare il file.

### Due processi wicd-client (ed eventualmente due icone nell'aria di notifica)

Leggere le note nel paragrafo [Eseguire Wicd](/index.php/Wicd_(Italiano)#Eseguire_Wicd "Wicd (Italiano)") riguardo all'avvio automatico ed al file nella cartella `/etc/xdg/autostart`, consultare anche il post sul forum internazionale ed il bug report indicati in [Collegamenti esterni](/index.php/Wicd_(Italiano)#Collegamenti_esterni "Wicd (Italiano)"). Essenzialmente, se il file `/etc/xdg/autostart/wicd-tray.desktop` è presente sul proprio sistema, basterà inserire il demone `wicd` nella lista dei demoni in avvio nel file `/etc/rc.conf`, e **non** sarà necessario avviare il client nel file (o nelle configurazioni) di avvio automatico del proprio DE/WM.

### Password errata usando PEAP con TKIP/MSCHAPV2

Il template di connessione PEAP con TKIP/MSCHAPV2 richiede che l'utente inserisca il percorso per un certificato emesso da una CA oltre a richiedere un nome utente ed una password. Tuttavia questo può causare problemi e wicd notificherà un errore di password errata [*](https://bbs.archlinux.org/viewtopic.php?pid=990385). Una possibile soluzione consiste nell'uso di PEAP con GTC anzichè TKIP/MSCHAPV2 dato che esso non necessita del certificato.

## Altre risorse

*   [Nota sulle interfacce nel sito ufficiale](http://www.wicd.net/download.php) -- in inglese.
*   [Discussione sul forum internazionale riguardo alla doppia esecuzione di wicd-client e /etc/xdg/autostart](https://bbs.archlinux.org/viewtopic.php?id=114803) -- in inglese.
*   [Bug report riguardo a /etc/xdg/autostart ed i comportamenti di wicd-client](https://bugs.archlinux.org/task/22423) -- in inglese.