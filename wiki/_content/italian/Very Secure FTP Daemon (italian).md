**vsftpd** (Very Secure FTP Daemon) è un server FTP leggero, stabile e sicuro per sistemi UNIX-like.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Abilitare l'upload](#Abilitare_l.27upload)
    *   [2.2 Accesso utenti locali](#Accesso_utenti_locali)
    *   [2.3 Accesso anonimi](#Accesso_anonimi)
    *   [2.4 Limitare navigabilità con chroot](#Limitare_navigabilit.C3.A0_con_chroot)
    *   [2.5 Limitare il login degli utenti](#Limitare_il_login_degli_utenti)
    *   [2.6 Limitare le connessioni](#Limitare_le_connessioni)
    *   [2.7 Utilizzo di xinetd](#Utilizzo_di_xinetd)
    *   [2.8 Utilizzo di SSL per la sicurezza dell'FTP](#Utilizzo_di_SSL_per_la_sicurezza_dell.27FTP)
*   [3 Suggerimenti](#Suggerimenti)
    *   [3.1 PAM con utenti virtuali](#PAM_con_utenti_virtuali)
        *   [3.1.1 Aggiungere cartelle private per gli utenti virtuali](#Aggiungere_cartelle_private_per_gli_utenti_virtuali)
*   [4 Ulteriori risorse](#Ulteriori_risorse)

## Installazione

`vsftpd` è incluso nel repository ufficiale. Basta installarlo con pacman:

```
# pacman -S vsftpd

```

Il server può essere avviato utilizzando il seguente comando:

```
# systemctl start vsftpd.service

```

Inoltre se si vuole che venga avviato automaticamente al boot è necessario abilitarlo in questo modo:

```
# systemctl enable vsftpd.service

```

Per usare `vsftpd` con `xinetd`, vedere la sezione sottostante per le procedure adatte.

## Configurazione

La maggior parte delle impostazioni in `vsftpd` sono fatte modificando il file `/etc/vsftpd.conf`. Il file è di per se stesso ben documentato, per cui questa sezione mette in luce solo alcuni importanti cambiamenti che si potrebbe voler effettuare. Per tutte le opzioni disponibili e la documentazione, sfogliare [vsftpd.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/vsftpd.conf.5) (5).

### Abilitare l'upload

Il flag `WRITE_ENABLE` deve essere impostato su YES in `/etc/vsftpd.conf` con il fine di consentire le modifiche al filesystem, come ad esempio il caricamento:

```
write_enable=YES

```

### Accesso utenti locali

Bisogna impostare la seguente riga in `/etc/vsftpd.conf` per consentire agli utenti membri in `/etc/passwd` di accedere al sistema:

```
local_enable=YES

```

### Accesso anonimi

La seguente riga in `/etc/vsftpd.conf` controlla se gli utenti anonimi possono effettuare il login:

```
anonymous_enable=YES # Consentire l'accesso anonimo
no_anon_password=YES # Nessuna password è richiesta per un login anonimo
anon_max_rate=30000  # Velocità massima di trasferimento per un client anonimo in byte al secondo

```

### Limitare navigabilità con chroot

Si può impostare un ambiente chroot che impedisce all'utente di lasciare la sua home directory. A tal fine, aggiungere le seguenti righe a `/etc/vsftpd.conf`:

```
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd.chroot_list

```

La variabile `chroot_list_file` specifica il file che contiene le direttive per gli utenti da circoscrivere.

Per una direttiva ancora più restrittiva, si può specificare la riga:

```
chroot_local_user=YES

```

In questo modo gli utenti locali rimarranno limitati in via predefinita, e il file specificato da `chroot_list_file` elenca gli utenti che **non** rientrano nell'area limitativa chroot.

### Limitare il login degli utenti

È possibile impedire agli utenti di accedere al server FTP con l'aggiunta di due righe `/etc/vsftpd.conf`:

```
userlist_enable=YES
userlist_file=/etc/vsftpd.user_list

```

`userlist_file` specifica ora il file che elenca gli utenti che non sono autorizzati ad effettuare il login. Se si desidera consentire l'accesso solo ad alcuni utenti, aggiungere la riga:

```
userlist_deny=NO

```

Il file specificato da `userlist_file` contiene ora gli utenti che sono autorizzati ad effettuare il login.

### Limitare le connessioni

Si può limitare la velocità di trasferimento dati, il numero di client e connessioni per IP di utenti locali, aggiungendo le informazioni in `/etc/vsftpd.conf`:

```
local_max_rate=1000000 # Massima velocità di trasferimento dati in byte al secondo
max_clients=50         # Numero massimo di client che possono essere collegati
max_per_ip=2           # Numero massimo di connessioni per IP

```

### Utilizzo di xinetd

Se si vuole usare `vsftpd` con `xinetd`, aggiungere le seguenti righe a `/etc/xinetd.d/vsftpd`:

```
service ftp
{
        socket_type             = stream
        wait                    = no
        user                    = root
        server                  = /usr/sbin/vsftpd
        log_on_success  += HOST DURATION
        log_on_failure  += HOST
        disable                 = no
}

```

L'opzione sottostante deve essere impostata in `/etc/vsftpd.conf`:

```
pam_service_name=ftp

```

Infine, aggiungere `xinetd` alla stringa demoni in `/etc/rc.conf`. Non è necessario aggiungere `vsftpd`, poichè verrà chiamato da `xinetd` quando necessario.

In caso di errori del genere durante la connessione al server:

```
500 OOPS: cap_set_proc

```

Sarà necessario aggiungere il modulo *capability* nella stringa MODULES in `/etc/rc.conf`.

Durante l'aggiornamento alla versione 2.1.0 si potrebbe ottenere un errore come questo quando ci si connette al server da un client:

```
500 OOPS: could not bind listening IPv4 socket

```

Nelle versioni precedenti era sufficiente lasciare le seguenti righe commentate:

```
# Use this to use vsftpd in standalone mode, otherwise it runs through (x)inetd
# listen=YES

```

In questa nuova versione, e forse anche nelle prossime, è necessario configurare esplicitamente come **non** eseguibile in modalità standalone, in questo modo:

```
# Use this to use vsftpd in standalone mode, otherwise it runs through (x)inetd
listen=NO

```

### Utilizzo di SSL per la sicurezza dell'FTP

Generare un certificato SSL in questo modo:

```
# cd /etc/ssl/certs
# openssl req -x509 -nodes -days 7300 -newkey rsa:2048 -keyout /etc/ssl/certs/vsftpd.pem -out /etc/ssl/certs/vsftpd.pem
# chmod 600 /etc/ssl/certs/vsftpd.pem

```

Verranno fatte varie domande sulla propria azienda, ecc, ma dato che il proprio certificato non è noto, non importa cosa si risponde durante la compilazione; lo si utilizzerà solo per la crittografia! Se si prevede di doverlo utilizzare con garanzie di fiducia (trusted), meglio ottenerne uno da compagnie come Thawte, Verisign ecc.

modificare la configurazione in `/etc/vsftpd.conf`

```
#this is important
ssl_enable=YES

#choose what you like, if you accept anon-connections
# you may want to enable this
# allow_anon_ssl=NO

#choose what you like,
# it's a matter of performance i guess
# force_local_data_ssl=NO

#choose what you like
force_local_logins_ssl=YES

#you should at least enable this if you enable ssl...
ssl_tlsv1=YES
#choose what you like
ssl_sslv2=YES
#choose what you like
ssl_sslv3=YES
#give the correct path to your currently generated *.pem file
rsa_cert_file=/etc/ssl/certs/vsftpd.pem
#the *.pem file contains both the key and cert
rsa_private_key_file=/etc/ssl/certs/vsftpd.pem

```

## Suggerimenti

### PAM con utenti virtuali

L'utilizzo di utenti virtuali ha il vantaggio di non richiedere un vero account per il login sul sistema. Mantenere l'ambiente in un contenitore è naturalmente una scelta più sicura.

Un database virtuale degli utenti deve essere creato facendo prima di tutto un semplice file di testo come questo:

```
utente1
password1
utente2
password2

```

Includere quanti utenti virtuali si preferisca, secondo la struttura nell'esempio. Salvarlo come `logins.txt`; il nome del file non ha alcun significato. Il passo successivo dipende dal sistema database Berkeley, che è incluso nel sistema principale di Arch. Come root creare il database effettivo con l'aiuto del file `logins.txt`, o come è stato chiamato:

```
# db_load -T -t hash -f logins.txt /etc/vsftpd_login.db

```

Si raccomanda di limitare le autorizzazioni per l'ormai creato file `vsftpd_login.db`:

```
# chmod 600 /etc/vsftpd_login.db

```

**Warning:** Fare attenzione sul fatto che conservare password in file di testo normale non è sicuro. Non dimenticare quindi di rimuovere il file temporaneo con `rm logins.txt`.

PAM dovrebbe ora essere impostato per poter utilizzare vsftpd_login.db. Per fare in modo che PAM controlli l'autenticazione utente, creare un file chiamato ftp nella cartella `/etc/pam.d/` con le seguenti informazioni:

```
auth required pam_userdb.so db=/etc/vsftpd_login crypt=hash 
account required pam_userdb.so db=/etc/vsftpd_login crypt=hash

```

**Note:** Si usi /etc/vsftpd_login senza l'estensione .db nella configurazione di PAM!

Ora è il momento di creare una home per gli utenti virtuali. Nell'esempio `/srv/ftp` è adibito ad ospitare i dati degli utenti virtuali, concetto che riflette anche la struttura delle directory di default di Arch. Per prima cosa creare l'utente virtuale generale e fare di `/srv/ftp` la sua home:

```
# useradd -d /srv/ftp virtual

```

Rendere virtuale il proprietario:

```
# chown virtual:virtual /srv/ftp

```

configurare vsftpd per utilizzare l'ambiente creato modificando `/etc/vsftpd.conf`. Queste sono le impostazioni necessarie per ottenere che `vsftpd` limiti l'accesso agli utenti virtuali, attraverso nomi utente e password, e circoscriva il loro accesso alla zona specificata `/srv/ftp`:

```
anonymous_enable=NO
local_enable=YES
chroot_local_user=YES
guest_enable=YES
guest_username=virtual
virtual_use_local_privs=YES

```

Se viene utilizzato il metodo `xinetd`, avviare il servizio. Ora si dovrebbe essere autorizzati solo al login con nome utente e password in base al database creato.

#### Aggiungere cartelle private per gli utenti virtuali

Innanzitutto creare le directory per gli utenti:

```
# mkdir /srv/ftp/user1
# mkdir /srv/ftp/user2
# chown virtual:virtual /srv/ftp/user?/

```

Quindi, aggiungere le seguenti righe a `/etc/vsftpd.conf`:

```
local_root=/srv/ftp/$USER
user_sub_token=$USER

```

## Ulteriori risorse

*   [vsftpd official homepage](http://vsftpd.beasts.org/)
*   [vsftpd.conf man page](http://vsftpd.beasts.org/vsftpd_conf.html)