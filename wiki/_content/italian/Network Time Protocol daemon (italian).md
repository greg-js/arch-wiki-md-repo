Questo articolo descrive come configurare ed eseguire NTPd (Network Time Protocol daemon), il metodo più diffuso per sincronizzare l'[orologio software](/index.php/System_time "System time") di un sistema GNU/Linux con dei time server utilizzando il [Network Time Protocol](https://en.wikipedia.org/wiki/Network_Time_Protocol "wikipedia:Network Time Protocol"); se appositamente configurato, NTPd può far funzionare il computer stesso come un time server.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Configurare la connessione per server NTP](#Configurare_la_connessione_per_server_NTP)
    *   [2.2 Configurare il proprio server NTP](#Configurare_il_proprio_server_NTP)
    *   [2.3 Altre risorse inerenti la configurazione NTP](#Altre_risorse_inerenti_la_configurazione_NTP)
*   [3 Utilizzo senza demone](#Utilizzo_senza_demone)
    *   [3.1 Sincronizzare una volta in fase di boot](#Sincronizzare_una_volta_in_fase_di_boot)
*   [4 Avvio come demone](#Avvio_come_demone)
    *   [4.1 Avvio di ntpd sysvinit](#Avvio_di_ntpd_sysvinit)
    *   [4.2 Abilitare demone ntpd sul sistema Native systemd](#Abilitare_demone_ntpd_sul_sistema_Native_systemd)
    *   [4.3 Controllare se il demone sta sincronizzando correttamente](#Controllare_se_il_demone_sta_sincronizzando_correttamente)
    *   [4.4 NetworkManager](#NetworkManager)
    *   [4.5 Esecuzione in chroot](#Esecuzione_in_chroot)
*   [5 Alternative](#Alternative)
*   [6 Vedere anche](#Vedere_anche)
*   [7 Link esterni](#Link_esterni)

## Installazione

[Installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") [ntp](https://www.archlinux.org/packages/?name=ntp), disponibile nei [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

## Configurazione

**Suggerimento:** Il pacchetto [ntp](https://www.archlinux.org/packages/?name=ntp) è installato di default con `/etc/ntp.conf`, che dovrebbe far funzionare NTPd senza apportare alcuna configurazione.

### Configurare la connessione per server NTP

La prima cosa che bisogna definire in `/etc/ntp.conf` sono i server con cui il computer dovrà sincronizzarsi.

I server NTP sono classificati in un sistema gerarchico con vari livelli chiamati *stratum*: i dispositivi che sono considerati sorgenti indipendenti dell'orario sono classificati come *stratum 0*; i server direttamente connessi ai dispositivi *stratum 0* sono classificati come *stratum 1*; i server connessi a loro volta a dispositivi *stratum 1* sono classificati come *stratum 2* e così via.

È necessario comprendere che lo *stratum* di un server non può essere considerato un'indicazione della sua precisione o affidabilità. Tipicamente, per scopi generici di sincronizzazione sono utilizzati server dello *stratum 2*: a meno che non si conoscano già i server a cui connettersi, è bene utilizzare quelli forniti da [pool.ntp.org](http://www.pool.ntp.org/) ([link alternativo](http://support.ntp.org/bin/view/Servers/NTPPoolServers)) scegliendo il pool di server più vicino alla propria posizione geografica.

Le seguenti linee sono un esempio:

 `/etc/ntp.conf` 
```

 server 0.pool.ntp.org iburst
 server 1.pool.ntp.org iburst
 server 2.pool.ntp.org iburst
 server 3.pool.ntp.org iburst

```

L'opzione `iburst` è consigliata, e invia una serie (burst) di pacchetti solo se non riesce ad ottenere una connessione al primo tentativo. L'opzione `burst` agisce sempre così, anche al primo tentativo, e non dovrebbe essere mai usata senza un'esplicita autorizzazione, perché potrebbe causare l'inserimento in blacklist.

### Configurare il proprio server NTP

Se si sta configurando un server ntp, è necessario aggiungere [*local clock*](http://www.ntp.org/ntpfaq/NTP-s-refclk.htm#Q-LOCAL-CLOCK) come server, in maniera che, nel caso il computer perda la connessione ad internet, non smetta comunque di inviare l'orario al network; è bene aggiungere *localhost* come un server *stratum 10* (utilizzando il comando *fudge*) in maniera che non sia mai usato a meno che sia perso l'accesso ad internet:

```
server 127.127.1.0
fudge  127.127.1.0 stratum 10

```

La prossima cosa da fare è definire le regole che permetteranno ai vari client di connettersi al servizio (anche *localhost* è considerato un client) utilizzando il comando *restrict*; nel file dovrebbe già essere presente una linea simile a questa:

```
restrict default nomodify nopeer

```

Questa linea nega a chiunque il permesso di modificare qualunque cosa ed impedisce di interrogare lo stato del time server: `nomodify` impedisce la riconfigurazione di ntpd (con *ntpq* oppure *ntpdc*) e `noquery` impedisce il dumping dei dati da ntpd (sempre con *ntpq* oppure *ntpdc*).

È possibile aggiungere anche altre opzioni:

```
restrict default kod nomodify notrap nopeer noquery

```

**Nota:** Questo permetterà ad altre persone di interrogare il proprio time server. E' necessario aggiungere `noserve` per fermare il serving time.

La documentazione completa per l'opzione "restrict" è reperibile in [ntp_acc()](https://jlk.fjfi.cvut.cz/arch/manpages/man/ntp_acc.). Per istruzioni dettagliate vedere [https://support.ntp.org/bin/view/Support/AccessRestrictions](https://support.ntp.org/bin/view/Support/AccessRestrictions).

La linea seguente serve ad indicare a *ntpd* cosa può attraversare il proprio server; la seguente riga è sufficiente se non si sta configurando un server NTP:

```
restrict 127.0.0.1

```

Se si vuole forzare la risoluzione DNS al namespace IPv6, scrivere `-6` davanti all'indirizzo IP o l'host name `-4` forza l'IPv4), ad esempio:

```
restrict -6 default nomodify nopeer
restrict -6 ::1    # ::1 is the IPv6 equivalent for 127.0.0.1

```

A questo punto rimane solo da aggiungere il percorso del file per il drift (che tiene conto della deviazione dell'orario di sistema) ed eventualmente il percorso del file di log:

```
driftfile /var/lib/ntp/ntp.drift
logfile /var/log/ntp.log

```

Una configurazione basilare, sarà simile a questa (**tutti i commenti sono stati eliminati per chiarezza**):

 `/etc/ntp.conf` 
```
server 0.pool.ntp.org iburst
server 1.pool.ntp.org iburst
server 2.pool.ntp.org iburst
server 3.pool.ntp.org iburst

restrict default kod nomodify notrap nopeer noquery
restrict -6 default kod nomodify notrap nopeer noquery

restrict 127.0.0.1
restrict -6 ::1  

driftfile /var/lib/ntp/ntp.drift
logfile /var/log/ntp.log

```

**Nota:** Definire il file di log non è obbligatorio, ma è sempre una buona idea avere dei feedback per operazioni *ntpd*.

### Altre risorse inerenti la configurazione NTP

Infine, mai dimenticarsi delle pagine di manuale: c'è la possibilità che [ntp.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ntp.conf.5) possa rispondere a molti dubbi che siano rimasti (leggere anche le pagine di manuale correlate: `man {ntpd|ntp_auth|ntp_mon|ntp_acc|ntp_clock|ntp_misc}`).

## Utilizzo senza demone

Per sincronizzare l'orologio di sistema una sola volta, senza avviare il demone NTP, eseguire:

```
# ntpd -qg

```

Questo ha lo stesso effetto del programma `ntpdate`, [che ora è deprecato](http://support.ntp.org/bin/view/Dev/DeprecatingNtpdate).

L'opzione `-g` permette di spostare l'orologio oltre la soglia di panico (15 minuti di default) senza un avvertimento. Si noti che la compensazione è anormale e potrebbe indicare un'errata impostazione del fuso orario, il guasto del chip orologio, o semplicemente un lunghissimo periodo di abbandono. Se in questi casi non si vuole impostare l'orologio e riportare l'errore in syslog, rimuovere `-g`.

Dopo aver aggiornato l'orologio di sistema, per salvare l'ora nell'orologio hardware per mantenerlo al riavvio:

```
# hwclock -w

```

### Sincronizzare una volta in fase di boot

**Attenzione:**

*   Utilizzare questo metodo è fortemente sconsigliato su server e in generale su macchine che devono funzionare continuativamente per periodi maggiori di 2 o 3 giorni, infatti l'orologio di sistema viene aggiornato solo una volta durante il boot.
*   Lanciare `ntpd -qg` come un evento di *cron* è da evitare assolutamente, a meno di essere perfettamente consapevoli del comportamento delle proprie applicazioni avviate in caso di modifiche istantanee dell'orologio di sistema.

Se si vuole sincronizzare l'orologio di sistema ogni volta che il sistema si avvia, si può aggiungere la riga `ntpd -qg &` al proprio `/etc/rc.local`. Vedere [Autostarting](/index.php/Autostarting "Autostarting") per i metodi alternativi:

```
ntpd -qg &

```

Si dovrebbe anche aggiungere il demone `hwclock` al proprio [DAEMONS array](/index.php/Daemon_(Italiano)#SEsecuzione_automatica_all.27avvio "Daemon (Italiano)"), a meno che qualcos'altro, ad esempio un altro sistema operativo in dual boot, non aggiorni già l'orologio hardware. Vedere [System time#hwclock daemon](/index.php/System_time#hwclock_daemon "System time") per maggiori informazioni.

Affinché questo metodo funzioni è necessario fare in modo che, quando `rc.local` viene eseguito, la connessione di rete sia già stata inizializzata (ad esempio, non si dovrebbero avere in background demoni correlati alla rete in `/etc/rc.conf`)

Se per qualche ragione non si vuole eseguire il demoone `hwclock`, aggiungere le seguenti linee in `/etc/rc.local` al posto di `ntpd -qg &`:

```
{ ntpd -qg; hwclock -w; } &

```

Questa sintassi fà in modo che entrambi i comandi siano eseguiti in background, ma assicura che vengono eseguiti in ordine (e non contemporaneamente). Si noti che eseguir il comando `hwclock -w` all'avvio, non è equivalente all'esecuzione del demone {{ic|hwclock}, che esegue invece `hwclock --adjust` allo spegnimento.

Note that running the `hwclock -w` command at boot is not equivalent to executing the `hwclock` daemon, which instead runs `hwclock --adjust` at shutdown.

## Avvio come demone

### Avvio di ntpd sysvinit

ntpd imposta la modalità 11 minuti, che sincronizza l'orologio di sistema con l'hardware ogni 11 minuti. Il demone hwclock misura l'orologio hardware e lo sincronizza, creando conflitti con ntpd.

Fermare il demone hwclock (se in esecuzione):

 `# rc.d stop hwclock` 

Avviare il demone ntpd:

 `# rc.d start ntpd` 

Aggiungere *ntpd* alla lista DAEMONS per avviarlo automaticamente al boot e assicurarsi di disabilitare hwclock:

 `/etc/rc.conf`  `DAEMONS=(... !hwclock **ntpd** ...)` 

### Abilitare demone ntpd sul sistema Native systemd

E' possibile abilitare il demone ntpd all'avvio con il seguente comando:

 `# systemctl enable ntpd` 

Oppure, in alternativa, utilizzare:

 `# timedatectl set-ntp 1` 

### Controllare se il demone sta sincronizzando correttamente

Utilizzare l'utility ntpq per visualizzare la lista dei peers configurati:

 `$ ntpq -np` 

Il ritardo, l'offset e le colonne jitter dovrebbero essere diverse da zero. I server ntpd che si stanno sincronizzando sono preceduti da un asterisco.

### NetworkManager

**Nota:** ntpd dovrebbe restare in esecuzione quando la rete non funziona, se il demone hwclock è disabilitato, quindi questo non dovrebbe essere necessario.

*ntpd* può essere acceso/spento a seconda della connessione internet attraverso l'uso dei [dispatcher script di NetworkManager](/index.php/NetworkManager_(Italiano)#Servizi_di_rete_con_NetworkManager_Dispatcher "NetworkManager (Italiano)"). È possibile installare gli script necessari dal repo [community]:

 `# pacman -S networkmanager-dispatcher-ntpd` 

### Esecuzione in chroot

**Nota:** ntpd dovrebbe essere eseguito senza i privilegi di amministratore, prima di tentare nell'ambiente chroot (di default, nel pacchetto vanilla di Arch Linux, poiché chroot è relativamente inutile per garantire i processi in esecuzione come utente root.

Editare `/etc/conf.d/ntpd.conf` e modificare

```
NTPD_ARGS="-g -u ntp:ntp"

```

in

```
NTPD_ARGS="-g -i /var/lib/ntp -u ntp:ntp"

```

Quindi, editare`/etc/ntp.conf` per cambiare il percorso del driftfile ed indirizzarlo alla directory chroot, anzichè alla cartella radice reale. Cambiare:

```
driftfile       /var/lib/ntp/ntp.drift

```

in

```
driftfile       /ntp.drift

```

Creare un ambiente chroot adatto, di modo che getaddrinfo() funzionerà creando idonee cartelle e file (da root):

```
# mkdir /var/lib/ntp/etc /var/lib/ntp/lib /var/lib/ntp/proc
# touch /var/lib/ntp/etc/resolv.conf /var/lib/ntp/etc/services
```

ed esegueno il collegamento-montaggio dei suddetti file:

 `/etc/fstab` 
```
...
#ntpd chroot mounts
/etc/resolv.conf  /var/lib/ntp/etc/resolv.conf none bind 0 0
/etc/services	  /var/lib/ntp/etc/services none bind 0 0
/lib		          /var/lib/ntp/lib none bind 0 0
/proc		  /var/lib/ntp/proc none bind 0 0

```
 `# mount -a` 

Infine, riavviare nuovamente il demone:

 `# rc.d restart ntpd` 

E' relativamente difficile essere sicuri che la configurazione driftfile sta funionando, senza attendere un po' di tempo, perchè ntpd non legge né scrive molto spesso. Se qualcosa è andato storto, si registrerà un errore; se funziona tutto bene, il timestamp si aggiornerà. Se non si ottengono errori dopo un'intera giornata ed il timestamp viene aggiornato, si dovrebbe essere sicuri del successo.

## Alternative

Possibili alternative ad NTPd sono [Chrony](/index.php/Chrony "Chrony"), una connessione dial-up semplice e specificatamente progettata per sistemi che non sono sempre online, e [OpenNTPD](/index.php/OpenNTPD_(Italiano) "OpenNTPD (Italiano)"), parte del progetto OpenBSD e attualmente non mantenuto per Linux.

## Vedere anche

*   [System time](/index.php/System_time "System time") (per maggiori informazioni sulla gestione del tempo nel computer)

## Link esterni

*   [http://www.ntp.org/](http://www.ntp.org/)
*   [http://support.ntp.org/](http://support.ntp.org/)
*   [http://www.pool.ntp.org/](http://www.pool.ntp.org/)
*   [http://www.eecis.udel.edu/~mills/ntp/html/index.html](http://www.eecis.udel.edu/~mills/ntp/html/index.html)
*   [http://www.akadia.com/services/ntp_synchronize.html](http://www.akadia.com/services/ntp_synchronize.html)