**Secure Shell** (**SSH**) è un protocollo di rete che consente lo scambio di dati su un canale protetto tra due computer. Encryption si incarica della riservatezza e l'integrità dei dati. SSH utilizza la crittografia a chiave pubblica per autenticare il computer remoto e permettere allo stesso di autenticarne l'utente, se necessario.

SSH è in genere utilizzato per accedere a una macchina remota ed eseguire comandi, ma supporta anche il tunneling, l'inoltro (forwarding arbitrary) su porte TCP e connessioni X11; il trasferimento dei file può essere eseguito utilizzando i protocolli associati SFTP o SCP.

Un server SSH rimane, in maniera predefinita, in ascolto sulla porta standard TCP 22\. Un programma client SSH viene in genere utilizzato per stabilire le connessioni a un demone sshd che accetta connessioni remote. Entrambi sono comunemente presenti nei sistemi operativi più moderni, incluso Mac OS X, GNU/Linux, Solaris e OpenVMS. Esistono versioni proprietarie, freeware e open source a vari livelli, sia di complessità che di completezza.

(Fonte: [Wikipedia:Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell "wikipedia:Secure Shell"))

## Contents

*   [1 OpenSSH](#OpenSSH)
    *   [1.1 Installazione di OpenSSH](#Installazione_di_OpenSSH)
    *   [1.2 Configurazione di SSH](#Configurazione_di_SSH)
        *   [1.2.1 Client](#Client)
        *   [1.2.2 Daemon](#Daemon)
    *   [1.3 Gestione demone SSHD](#Gestione_demone_SSHD)
    *   [1.4 Connessione al server](#Connessione_al_server)
*   [2 Trucchi e consigli](#Trucchi_e_consigli)
    *   [2.1 Tunnel criptati](#Tunnel_criptati)
        *   [2.1.1 Step 1: Avviare la connessione](#Step_1:_Avviare_la_connessione)
        *   [2.1.2 Step 2: Configurare il Browser (o altri programmi)](#Step_2:_Configurare_il_Browser_.28o_altri_programmi.29)
    *   [2.2 X11 Forwarding](#X11_Forwarding)
    *   [2.3 Effettuare il Forwarding di altre porte](#Effettuare_il_Forwarding_di_altre_porte)
    *   [2.4 Velocizzare SSH](#Velocizzare_SSH)
        *   [2.4.1 Risoluzione di problemi](#Risoluzione_di_problemi)
    *   [2.5 Montaggio di un filesystem remoto con SSHFS](#Montaggio_di_un_filesystem_remoto_con_SSHFS)
    *   [2.6 Mantenere la sessione attiva](#Mantenere_la_sessione_attiva)
    *   [2.7 Salvare i dati di connessione in .ssh/config](#Salvare_i_dati_di_connessione_in_.ssh.2Fconfig)
    *   [2.8 Cambiare la promt di accesso di SSH](#Cambiare_la_promt_di_accesso_di_SSH)
    *   [2.9 Effettuare il logout automatico degli utenti ssh quando il server si spegne](#Effettuare_il_logout_automatico_degli_utenti_ssh_quando_il_server_si_spegne)
*   [3 Risoluzione di problemi](#Risoluzione_di_problemi_2)
    *   [3.1 Connection Refused](#Connection_Refused)
        *   [3.1.1 Is SSH running and listening?](#Is_SSH_running_and_listening.3F)
        *   [3.1.2 Le regole del firewall stanno bloccando la connessione?](#Le_regole_del_firewall_stanno_bloccando_la_connessione.3F)
        *   [3.1.3 Il computer è raggiungibile dalle richieste?](#Il_computer_.C3.A8_raggiungibile_dalle_richieste.3F)
        *   [3.1.4 Read from socket failed: Connection reset by peer](#Read_from_socket_failed:_Connection_reset_by_peer)
    *   [3.2 "[nome della shell in uso]: No such file or directory" / ssh_exchange_identification Problem](#.22.5Bnome_della_shell_in_uso.5D:_No_such_file_or_directory.22_.2F_ssh_exchange_identification_Problem)
*   [4 Altre risorse](#Altre_risorse)
*   [5 Link e riferimenti](#Link_e_riferimenti)

## OpenSSH

OpenSSH (OpenBSD Secure Shell) è un insieme di programmi per computer che forniscono sessioni di comunicazione criptate su una rete di computer usando il protocollo SSH. È stato creato come alternativa open source al software proprietario Secure Shell suite, offerto da SSH Communications Security. OpenSSH è sviluppato come parte del progetto OpenBSD, che è guidato da Theo de Raadt.

OpenSSH è a volte confuso con OpenSSL per la somiglianza del nome, tuttavia, i progetti hanno scopi diversi e sono sviluppati da team differenti. La similitudine del nome è derivata solamente da obiettivi simili.

### Installazione di OpenSSH

[Installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") il pacchetto [openssh](https://www.archlinux.org/packages/?name=openssh)

### Configurazione di SSH

#### Client

Il file di configurazione del client SSH può essere trovato e modificato in `/etc/ssh/ssh_config`.

Un esempio di configurazione:

 `/etc/ssh/ssh_config` 
```
#	$OpenBSD: ssh_config,v 1.26 2010/01/11 01:39:46 dtucker Exp $

# This is the ssh client system-wide configuration file.  See
# ssh_config(5) for more information.  This file provides defaults for
# users, and the values can be changed in per-user configuration files
# or on the command line.

# Configuration data is parsed as follows:
#  1\. command line options
#  2\. user-specific file
#  3\. system-wide file
# Any configuration value is only changed the first time it is set.
# Thus, host-specific definitions should be at the beginning of the
# configuration file, and defaults at the end.

# Site-wide defaults for some commonly used options.  For a comprehensive
# list of available options, their meanings and defaults, please see the
# ssh_config(5) man page.

# Host *
#   ForwardAgent no
#   ForwardX11 no
#   RhostsRSAAuthentication no
#   RSAAuthentication yes
#   PasswordAuthentication yes
#   HostbasedAuthentication no
#   GSSAPIAuthentication no
#   GSSAPIDelegateCredentials no
#   BatchMode no
#   CheckHostIP yes
#   AddressFamily any
#   ConnectTimeout 0
#   StrictHostKeyChecking ask
#   IdentityFile ~/.ssh/identity
#   IdentityFile ~/.ssh/id_rsa
#   IdentityFile ~/.ssh/id_dsa
#   Port 22
#   Protocol 2,1
#   Cipher 3des
#   Ciphers aes128-ctr,aes192-ctr,aes256-ctr,arcfour256,arcfour128,aes128-cbc,3des-cbc
#   MACs hmac-md5,hmac-sha1,umac-64@openssh.com,hmac-ripemd160
#   EscapeChar ~
#   Tunnel no
#   TunnelDevice any:any
#   PermitLocalCommand no
#   VisualHostKey no
#   ProxyCommand ssh -q -W %h:%p gateway.example.com
```

Si consiglia di modificare la riga del protocollo in questo modo:

```
Protocol 2

```

Ciò significa che sarà utilizzato solo il protocollo 2, dal momento che il protocollo 1 è considerato poco sicuro.

#### Daemon

Il file di configurazione del demone SSH può essere trovato e modificato in `/etc/ssh/ssh**d**_config`.

Un esempio di configurazione:

 `/etc/ssh/sshd_config` 
```
#	$OpenBSD: sshd_config,v 1.82 2010/09/06 17:10:19 naddy Exp $

# This is the sshd server system-wide configuration file.  See
# sshd_config(5) for more information.

# This sshd was compiled with PATH=/usr/bin:/bin:/usr/sbin:/sbin

# The strategy used for options in the default sshd_config shipped with
# OpenSSH is to specify options with their default value where
# possible, but leave them commented.  Uncommented options change a
# default value.

#Port 22
#AddressFamily any
#ListenAddress 0.0.0.0
#ListenAddress ::

# The default requires explicit activation of protocol 1
#Protocol 2

# HostKey for protocol version 1
#HostKey /etc/ssh/ssh_host_key
# HostKeys for protocol version 2
#HostKey /etc/ssh/ssh_host_rsa_key
#HostKey /etc/ssh/ssh_host_dsa_key
#HostKey /etc/ssh/ssh_host_ecdsa_key

# Lifetime and size of ephemeral version 1 server key
#KeyRegenerationInterval 1h
#ServerKeyBits 1024

# Logging
# obsoletes QuietMode and FascistLogging
#SyslogFacility AUTH
#LogLevel INFO

# Authentication:

#LoginGraceTime 2m
#PermitRootLogin yes
#StrictModes yes
#MaxAuthTries 6
#MaxSessions 10

#RSAAuthentication yes
#PubkeyAuthentication yes
#AuthorizedKeysFile	.ssh/authorized_keys

# For this to work you will also need host keys in /etc/ssh/ssh_known_hosts
#RhostsRSAAuthentication no
# similar for protocol version 2
#HostbasedAuthentication no
# Change to yes if you don't trust ~/.ssh/known_hosts for
# RhostsRSAAuthentication and HostbasedAuthentication
#IgnoreUserKnownHosts no
# Don't read the user's ~/.rhosts and ~/.shosts files
#IgnoreRhosts yes

# To disable tunneled clear text passwords, change to no here!
#PasswordAuthentication yes
#PermitEmptyPasswords no

# Change to no to disable s/key passwords
ChallengeResponseAuthentication no

# Kerberos options
#KerberosAuthentication no
#KerberosOrLocalPasswd yes
#KerberosTicketCleanup yes
#KerberosGetAFSToken no

# GSSAPI options
#GSSAPIAuthentication no
#GSSAPICleanupCredentials yes

# Set this to 'yes' to enable PAM authentication, account processing, 
# and session processing. If this is enabled, PAM authentication will 
# be allowed through the ChallengeResponseAuthentication and
# PasswordAuthentication.  Depending on your PAM configuration,
# PAM authentication via ChallengeResponseAuthentication may bypass
# the setting of "PermitRootLogin without-password".
# If you just want the PAM account and session checks to run without
# PAM authentication, then enable this but set PasswordAuthentication
# and ChallengeResponseAuthentication to 'no'.
UsePAM yes

#AllowAgentForwarding yes
#AllowTcpForwarding yes
#GatewayPorts no
#X11Forwarding no
#X11DisplayOffset 10
#X11UseLocalhost yes
#PrintMotd yes
#PrintLastLog yes
#TCPKeepAlive yes
#UseLogin no
#UsePrivilegeSeparation yes
#PermitUserEnvironment no
#Compression delayed
#ClientAliveInterval 0
#ClientAliveCountMax 3
#UseDNS yes
#PidFile /var/run/sshd.pid
#MaxStartups 10
#PermitTunnel no
#ChrootDirectory none

# no default banner path
#Banner none

# override default of no subsystems
Subsystem	sftp	/usr/lib/ssh/sftp-server

# Example of overriding settings on a per-user basis
#Match User anoncvs
#	X11Forwarding no
#	AllowTcpForwarding no
#	ForceCommand cvs serveri
```

Per consentire l'accesso solo ad alcuni utenti aggiungere questa riga:

```
AllowUsers    user1 user2

```

Per disabilitare l'accesso SSH per l'utente *root*, aggiungere la seguente linea:

```
PermitRootLogin no

```

Si potrebbe anche rimuovere l'opzione BANNER e modificare il file `/etc/issue` per un gradevole messaggio di benvenuto.

**Tip:** Si consiglia di modificare la porta di default 22 ad una di numero più alto (consultare [security through obscurity](https://en.wikipedia.org/wiki/Security_through_obscurity "wikipedia:Security through obscurity")).

Anche se la porta SSH è in esecuzione e può essere rilevata utilizzando un port scanner come nmap, cambiandola si ridurrà il numero di voci del registro di log, causato dai tentativi di autenticazione automatica. Per un aiuto sulla scelta della porta consultare la [lista dei numeri delle porte TCP ed UDP](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers "wikipedia:List of TCP and UDP port numbers").

**Tip:** Disabilitando gli accessi con la password, aumenta il livello di sicurezza. (consultare [SSH Keys](/index.php/SSH_keys_(Italiano) "SSH keys (Italiano)")).

### Gestione demone SSHD

Aggiungere `sshd` alla lista di [demoni](/index.php/Demoni "Demoni") caricati all'avvio con:

```
# systemctl enable sshd

```

Per avviare/riavviare/fermare il demone, usare il seguente comando (da root):

```
# systemctl (start/restart/stop) sshd

```

### Connessione al server

Per connettersi ad un server, dare il comando:

```
$ ssh -p port user@server-address

```

## Trucchi e consigli

### Tunnel criptati

Questo tipo di collegamento è molto utile per, ad esempio, l'utenza laptop collegata a varie connessioni wireless non sicure. L'unica cosa necessaria è un server SSH in esecuzione in un qualche luogo sicuro, come casa o il luogo di lavoro. Potrebbe essere utile l'utilizzo di un servizio DNS dinamico come [DynDNS](http://www.dyndns.org/) in modo da non dover ricordare l'indirizzo IP a cui ci si vuole collegare.

#### Step 1: Avviare la connessione

È sufficiente eseguire questo comando nel terminale preferito per avviare la connessione:

```
$ ssh -ND 4711 user@host

```

dove `"user"` è il nome utente del server SSH in esecuzione sull' `"host"`. Verrà richiesta la password, e la connessione sarà stabilita! Il flag `"N"` disabilita il prompt interattivo, il flag `"D"` specifica la porta locale su cui ascoltare (si può scegliere qualsiasi numero di porta).

Un modo per facilitare questa operazione è quello di mettere una riga di "alias" nel file `~/.bashrc` come segue:

```
alias sshtunnel="ssh -ND 4711 -v user@host"

```

Può risultare utile aggiungere il flag "verbose" `"-v"`, in modo da poter verificare dall'output che si è realmente connessi. Ora basta eseguire il comando `"sshtunnel"`

#### Step 2: Configurare il Browser (o altri programmi)

Il passo precedente è del tutto inutile se non si configura il browser web (o altri programmi) da utilizzare con il tunnel appena creato. A partire dalla corrente versione di SSH sono supportati sia SOCKS4 che SOCKS5 sarà possibile scegliere uno dei due.

*   Per Firefox: *Modificare → Preferenze → Avanzate → Rete → Connessione → Impostazioni*:

	Controllare il bottone *"Configurazione manuale del proxy"*, ed immettere "localhost" nel campo testuale *"SOCKS host"*, ed immettere infine il numero della porta nel prossimo campo testuale (usata in questo caso la 4711, come sopra).

Firefox non effettua automaticamente le richieste DNS attraverso il tunnel. Questo inconveniente riguardo alla privacy può essere ovviato con questi passi:

1.  digitare `about:config` nella barra dell'indirizzo di Firefox.

1.  cercare la chiave `network.proxy.socks_remote_dns`

1.  impostare il valore a `true`-

1.  riavviare il browser.

*   Per Chromium: è possibile configurare le impostazioni del SOCKS come variabili di ambiente oppure come opzione di lancio da riga di comando. Il metodo raccomandato consiste nell'inserire una delle seguenti funzioni nel proprio `.bashrc`:

```
function secure_chromium {
  port=4711
  export SOCKS_SERVER=localhost:$port
  export SOCKS_VERSION=5
  chromium &
  exit
}

```

oppure

```
function secure_chromium {
  port=4711
  chromium --proxy-server="socks://localhost:$port" &
}

```

In questo modo basterà digitare nel terminale:

```
$ secure_chromium

```

Godetevi il vostro tunnel sicuro!

### X11 Forwarding

Per eseguire programmi grafici tramite una connessione SSH è possibile attivare X11 forwarding. Un'opzione dovrà essere impostata nel file di configurazione sul server e client (dove "client" significa la propria macchina (desktop) sulla quale il server X11 è in esecuzione, e le applicazioni in X verranno eseguite sul "server").

Installare il pacchetto [xorg-xauth](https://www.archlinux.org/packages/?name=xorg-xauth) sul server.

*   Abilitare l'opzione **AllowTcpForwarding** in `sshd_config` sul **server**.
*   Abilitare l'opzione **X11Forwarding** in `sshd_config` sul **server**.
*   Abilitare l'opzione **X11DisplayOffset** in `sshd_config` sul **server** e impostare su 10.
*   Abilitare l'opzione **X11UseLocalhost** in `sshd_config` sul **server**.

Inoltre sarà necessario:

*   Abilitare l'opzione **ForwardX11** in `ssh_config` sul **client**.

Abilitare l'opzione **ForwardX11Trusted** può essere utile nel caso che le interfacce grafiche vengano visualizzate male.

Per usare il forwarding, accedere al server con SSH:

```
$ ssh -X -p port user@server-address

```

Nel caso vengano restituiti degli errori avviando applicazioni grafiche, provare con il trusted forwarding:

```
$ ssh -Y -p port user@server-address

```

Sarà possibile avviare ora qualsiasi programma X sul server remoto, l'output sarà trasmesso alla sessione locale:

```
$ xclock

```

Se si ottiene l'errore "Cannot open display" provare i seguenti comandi come utente normale, non come root:

```
$ xhost +

```

Il precedente comando consentira a tutti i client di effettuare il forward delle applicazioni grafiche(X11). Per restringere l'accesso a determinati client:

```
$ xhost +nomemacchina

```

Dove *nomemacchina* è il nome della macchina a cui si vuole garantire l'accesso. Digitare "`man xhost`" per maggiori informazioni.

Alcune applicazioni verificano la presenza di altre istanze sulla macchina locale. Ad esempio Firefox. Sarà necessario quindi chiudere l'applicazione oppure usare la seguente opzione per avviare una sessione remota dalla macchina locale.

```
$ firefox -no-remote

```

### Effettuare il Forwarding di altre porte

In aggiunta al supporto nativo per X11, SSH può essere usato per incanalare in un tunnel sicuro qualsiasi connessione TCP, usando il forwarding locale o remoto.

Il forwarding locale apre una porta sulla macchina locale, tutte le connessioni ad essa saranno inviate all'host remoto e da quindi ad una specifica destinazione. Molto spesso, la destinazione finale sarà la solita dell'host remoto, questo fornisce una shell sicura ed, ad esempio, una connessione VNC sicura, alla stessa macchina. Il forwarding locale viene specificato mediante l'uso dell'opzione `-L` e seguita dalle appropriate impostazioni per il forwarding in questa forma `<porta tunnel>:<indirizzo destinazione>:<porta destinazione>`.

Ad esempio:

```
$ ssh -L 1000:mail.google.com:25 192.168.0.100

```

utilizzerà SSH per effettuare il login ad una shell remota sul server 192.168.0.100, ed inoltre creerà un tunnel dalla porta 1000 TCP locale alla destinazione remota mail.google.com alla porta 25\. Una volta stabilita la connessione, tutte le connessioni a localhost:1000 verranno indirizzate al servizio SMTP di Gmail. A Google, risulterà che ogni richiesta (ma non necessariamente i dati inviati dalla connessione) provenga da 192.168.0.100, inoltre questi dati saranno criptati nel transito dalla macchina locale al server 192.168.0.100, ma non oltre 192.168.0.100, a meno che non vengano presi provvedimenti al riguardo.

Similmente:

```
$ ssh -L 2000:192.168.0.100:6001 192.168.0.100

```

permetterà alle connessioni verso localhost:2000 di essere inviate all'host remoto alla porta 6001\. Il precedente esempio è molto utile per le connessioni VNC, ad esempio, usando l'utility `vncserver` (parte delle applicazioni fornite dal pacchetto [tightvnc](https://aur.archlinux.org/packages/tightvnc/), il quale non fornisce misure di sicurezza proprie.

Il remote forwarding permette alla macchina remota di connettersi ad un host tramite il tunnel SSH e la la macchina locale, fornendo una funzione inversa al forwarding locale, questo risulta utile, ad esempio, nel caso in cui l'host remoto ha una connettività limitata a causa di un firewall. Il remote forwarding viene specificato dall'opzione `-R` ed alle impostazioni del forwarding nella forma `<porta tunnel>:<indirizzo destinazione>:<porta destinazione>`.

Ad esempio:

```
$ ssh -R 3000:irc.freenode.net:6667 192.168.0.200

```

aprirà una shell sul server 195.168.0.200, e le connessioni provenienti da 192.168.0.200 a se stesso sulla porta 3000(parlando in termini remoti localhost:3000) verranno inviate attraverso il tunnel verso la macchina locale e poi verso irc.freenode.net alla porta 6667, quindi, in questo esempio, permetterà l'uso dei programmi IRC sulla macchina remota anche se normalmente la porta 6667 sarebbe chiusa.

Entrambi i tipi di forwarding locale e remoto possono essere usati per creare un "gateway" sicuro permettendo agli altri computer di godere dei vantaggi di un tunnel SSH, senza dover eseguire un client SSH oppure un demone SSH fornendo un indirizzo di ascolto per definire l'inizio del tunnel come argomento del forwarding, nella forma: `<indirizzo tunnel>:<porta tunnel>:<indirizzo destinazione>:<porta destinazione>`.

`<indirizzo tunnel>` può essere un qualsiasi indirizzo sulla macchina all'inizio del tunnel, `localhost`, `*` (oppure lasciato in bianco), che rispettivamente, permettono connessioni tramite uno specifico indirizzo, tramite l'interfaccia di loopback, oppure tramite qualunque interfaccia. Come default, il forwarding è limitato alle connessioni provenienti dalla macchina all'inizio del tunnel, quindi `<tunnel address>` è impostato su `localhost`. Il forwarding locale non richiede configurazioni addizionali, mentre il forwarding remoto è condizionato dalle configurazioni del demone SSH sulla macchina remota. Per maggiori informazioni consultare le informazioni riguardo all'opzione `GatewayPorts` nella pagina di manuale `sshd_config(5)`.

### Velocizzare SSH

Sarà possibile che tutte le sessioni con lo stesso host utilizzino una singola connessione, il che velocizza notevolmente i login successivi, aggiungendo queste righe nell'host appropriato in `/etc/ssh/ssh_config`:

```
ControlMaster auto
ControlPath ~/.ssh/socket-%r@%h:%p

```

Modificando i valori usati da SSH per una minore richiesta di risorse cpu può aumentarne la velocità. Sotto questo aspetto, le scelte migliori ricadono su arcfour e blowfish-cbc. **Non usare queste opzioni a meno che non si sappia ciò che si sta facendo; arcfour ha alcune vulnerabilità note.** Per provarli, avviare SSH con il flag `"c"`, in questo modo:

```
$ ssh -c arcfour,blowfish-cbc user@server-address

```

Per renderne l'utilizzo predefinito, aggiungere questa riga sotto il proper host in `/etc/ssh/ssh_config`:

```
Ciphers arcfour,blowfish-cbc

```

Un'altra opzione per aumentare la velocità è abilitare la compressione con il flag `"C"`. Una soluzione permanente è aggiungere questa riga nell'host appropriato in `/etc/ssh/ssh_config`:

```
Compression yes

```

Il tempo di login può essere diminuito usando il flag `"4"`, che bypassa IPv6 lookup. Ciò può essere reso permanente con l'aggiunta di questa riga nell'host appropriato in `/etc/ssh/ssh_config`:

```
AddressFamily inet

```

Un altro modo di fare queste modifiche è sempre quella di creare un alias in `~/.bashrc`:

```
alias ssh='ssh -C4c arcfour,blowfish-cbc'

```

#### Risoluzione di problemi

Assicurarsi che la stringa DISPLAY punti sul server remoto:

```
ssh -X user@server-address
server$ echo $DISPLAY
localhost:10.0
server$ telnet localhost 6010
localhost/6010: lookup failure: Temporary failure in name resolution   

```

la soluzione possibile consiste nell'aggiungere `localhost` al file `/etc/hosts`.

### Montaggio di un filesystem remoto con SSHFS

Installare il pacchetto [sshfs](https://www.archlinux.org/packages/?name=sshfs)

Caricare il modulo `fuse`

```
# modprobe fuse

```

Aggiungere `fuse` all'array `MODULES` nel file `/etc/rc.conf` per caricarlo ad ogni avvio del sistema.

Montare la cartella remota con sshfs

```
# mkdir ~/remote_folder
# sshfs USER@remote_server:/tmp ~/remote_folder

```

Il comando sopra farà sì che la cartella /tmp sul server remoto verrà montata come ~/remote_folder sulla macchina locale. La copia di qualsiasi file in questa cartella, comporterà una copia trasparente attraverso la rete utilizzando SFTP. Lo stesso si avrà per la modifica dei file, la copia e l'eliminazione.

Una volta terminato il lavoro con il file system remoto, si può smontare la cartella remota mediante il comando:

```
# fusermount -u ~/remote_folder

```

Avendo la necessità di lavorare su questa cartella quotidianamente, può risultare comodo aggiungerla alla tabella di montaggio di `/etc/fstab`. In questo modo la si può avere montata automaticamente all'avvio del sistema o da montare manualmente (se si sceglie l'opzione `noauto`), senza la necessità di specificare la posizione remota ogni volta. Ecco un esempio di voce aggiunta nella tabella:

```
sshfs#USER@remote_server:/tmp /full/path/to/directory fuse    defaults,auto,allow_other    0 0

```

### Mantenere la sessione attiva

La sessione SSH effettuerà automaticamente un log out dopo un certo tempo di inattività. Per mantenere la connessione attiva aggiungere in `~/.ssh/config` o in `/etc/ssh/ssh_config` del client, la seguente riga:

```
ServerAliveInterval 120

```

Questo invierà un segnale di "mantenimento di stato attivo" al server ogni 120 secondi.

Invece per mantenere le connessioni in entrata attive, si può impostare

```
ClientAliveInterval 120

```

(oppure un qualsiasi numero maggiore di 0) nel file `/etc/ssh/sshd_config` del server.

### Salvare i dati di connessione in .ssh/config

Ogni volta che ci si connette ad un server SSH, è necessario digitare il suo indirizzo ed il nome utente. Per evitare di scrivere questi dati ogni volta per i server a cui siamo soliti connetterci, è possibile utilizzare il file `$HOME/.ssh/config` oppure il file di configurazione globale `/etc/ssh/ssh_config` come nel seguente esempio:

 `$HOME/.ssh/config` 
```
Host myserver
    HostName 123.123.123.123
    Port 12345
    User bob
Host other_server
    HostName test.something.org
    User alice
    CheckHostIP no
    Cipher blowfish

```

Adesso sarà possibile connettersi al server usando il nome che si è specificato:

```
$ ssh myserver

```

Per una lista completa delle opzioni che si posso utilizzare, consultare il manuale di ssh_config del proprio sistema oppure [la documentazione di ssh_config](http://www.openbsd.org/cgi-bin/man.cgi?query=ssh_config) sul sito ufficiale.

### Cambiare la promt di accesso di SSH

Può essere utile distinguere la shell locale da quella remota, in particolare quando entrambe sono configurate allo stesso modo. Per fare ciò basterà semplicemente inserire questo nel proprio bashrc:

 `$HOME/.bashrc` 
```

if [ -n "$SSH_CLIENT" ]; then
        PS1='\[\e[0;33m\]\u@\h:\wSSH$\[\e[m\] '
else
        PS1='\[\e[0;32m\]\u\[\e[m\] \[\e[1;34m\]\w\[\e[m\] \[\e[1;32m\]\$\[\    e[m\] '
fi
```

Vedi [Color Bash Promt](/index.php/Color_Bash_Prompt_(Italiano) "Color Bash Prompt (Italiano)") per maggiori informazioni riguardo alla personalizzazione della variabile PS1.

### Effettuare il logout automatico degli utenti ssh quando il server si spegne

Per chiudere automaticamente le connessioni degli utenti collegati via SSH quando il server viene spento o per un riavvio, aggiungere questa linea al file `/etc/rc.local.shutdown` del server SSH:

```
who | cut -d " " -f1 | uniq | xargs pkill -KILL -u

```

Questo evita che i terminali dei client restino bloccati per un lungo tempo, ed eventualmente terminino con il messaggio:

```
Write failed: Broken pipe

```

## Risoluzione di problemi

### Connection Refused

#### Is SSH running and listening?

```
$ ss -tnlp

```

If the above command do not show SSH port is open, SSH is NOT running. Check `/var/log/messages` for errors etc.

#### Le regole del firewall stanno bloccando la connessione?

Fermare il firewall per assicurarsi che non sia esso a bloccare le connessioni in entrata:

```
# rc.d stop iptables

```

oppure

```
# iptables -P INPUT ACCEPT
# iptables -P OUTPUT ACCEPT
# iptables -F INPUT
# iptables -F OUTPUT

```

#### Il computer è raggiungibile dalle richieste?

Avviare un dump del traffico sul server che restituisce l'errore:

```
# tcpdump -lnn -i any port ssh and tcp-syn

```

Questo comando dovrebbe mostrare alcune informazioni di base, fino a che non si ottengo le informazioni relative al traffico(in questo caso al traffico di SSH). Se non si ottiene nessun risultato nel tentare la connessione, allora qualcosa al di fuori del computer blocca il traffico (es. firewall hardware, NAT, router ecc.).

#### Read from socket failed: Connection reset by peer

Le recenti versioni di OpenSSH a volte, falliscono segnalando il precedente messaggio di errore, a causa di un bug riguardante la crittografia ECDSA. In questo caso, modificare il file `~/.ssh/config` o crearlo, se non esiste. Aggiungere la seguente linea:

 `~/.ssh/config` 
```
.....
HostKeyAlgorithms ssh-rsa-cert-v01@openssh.com,ssh-dss-cert-v01@openssh.com,ssh-rsa-cert-v00@openssh.com,ssh-dss-cert-v00@openssh.com,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,ssh-rsa,ssh-dss
.....
```

Dalla versione 5.9 di OpenSSH, il fix precedente non funziona. Inserire invece le seguenti righe nel file `~/.ssh/config`

```
Ciphers aes128-ctr,aes192-ctr,aes256-ctr,aes128-cbc,3des-cbc 
MACs hmac-md5,hmac-sha1,hmac-ripemd160

```

Leggere anche [la discussione](http://www.gossamer-threads.com/lists/openssh/dev/51339) sul forum dei bug di OpenSSH.

### "[nome della shell in uso]: No such file or directory" / ssh_exchange_identification Problem

Una possibile causa di questo errore, è causata da alcuni client SSH che necessitano di un cammino assoluto (può essere ottenuto con il comando `whereis -b [nome della shell in uso]`, ad esempio) nella variabile `$SHELL`, anche se l'eseguibile della shell si trova all'interno di uno dei percorsi specificati nella variabile `$PATH`. Un altra ragione può essere che l'utente non appartiene al [gruppo](/index.php/Users_and_Groups_(Italiano)#Gruppi "Users and Groups (Italiano)") `network`.

## Altre risorse

*   [Chiavi SSH](/index.php/SSH_Keys_(Italiano) "SSH Keys (Italiano)")
*   [Pam_abl](/index.php/Pam_abl "Pam abl")
*   [fail2ban](/index.php/Fail2ban "Fail2ban")
*   [sshguard](/index.php/Sshguard "Sshguard")
*   [Sshfs](/index.php/Sshfs_(Italiano) "Sshfs (Italiano)")

## Link e riferimenti

*   [Rimedi ai comuni attacchi di accesso a SSH](http://www.soloport.com/iptables.html)
*   [Usare il proprio browser come client SSH](http://webssh.cz.cc)
*   [Difenersi dagli attacchi di tipo brute force](http://www.la-samhna.de/library/brutessh.html)