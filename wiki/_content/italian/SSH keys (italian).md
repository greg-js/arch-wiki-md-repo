Le chiavi SSH sono una implementazione della [crittografia a chiavi pubbliche](https://en.wikipedia.org/wiki/Public-key_cryptography "wikipedia:Public-key cryptography"). Esse risolvono il problema degli attacchi di tipo brute-force sulle password rendendoli impraticabili.In aggiunta, usando le chiavi SSH, si può facilmente connettersi a un server o più server, senza dover inserire la password per ogni sistema.

È possibile impostare le chiavi senza password, tuttavia questo approccio non è raccomandabile, dato che se qualcuno scopre le chiavi le potrebbe utilizzare. Questa guida descrive come configurare un sistema in modo che la passphrase venga usata per criptare la chiave privata e che debba essere inserita per utilizzare la chiave stessa.

## Contents

*   [1 Generare la chiavi SSH](#Generare_la_chiavi_SSH)
*   [2 Copiare la chiave pubblica al server remoto](#Copiare_la_chiave_pubblica_al_server_remoto)
    *   [2.1 Metodo semplice](#Metodo_semplice)
    *   [2.2 Metodo tradizionale](#Metodo_tradizionale)
*   [3 Disabilitare i login con la password](#Disabilitare_i_login_con_la_password)
*   [4 Memorizzare le passphrase delle chiavi](#Memorizzare_le_passphrase_delle_chiavi)
    *   [4.1 ssh-agent](#ssh-agent)
        *   [4.1.1 Uso di GnuPG Agent](#Uso_di_GnuPG_Agent)
        *   [4.1.2 Utilizzo di portachiavi](#Utilizzo_di_portachiavi)
        *   [4.1.3 Utilizzo di ssh-agent e x11-ssh-askpass](#Utilizzo_di_ssh-agent_e_x11-ssh-askpass)
    *   [4.2 GNOME Keyring](#GNOME_Keyring)
*   [5 Risoluzione di problemi](#Risoluzione_di_problemi)
*   [6 Altre risorse](#Altre_risorse)

## Generare la chiavi SSH

Se [openssh](https://www.archlinux.org/packages/?name=openssh) non è già installato sul sistema, provvedere [installandolo](/index.php/Pacman_(Italiano) "Pacman (Italiano)"), dato che adesso non è installato di default su Arch.

Le chiavi possono essere generate eseguendo il comando `ssh-keygen` come utente:

 `$ ssh-keygen -b 521 -t ecdsa -C"$(id -un)@$(hostname)-$(date --rfc-3339=date)"` 
```
Generating public/private ecdsa key pair.
Enter file in which to save the key (/home/mith/.ssh/id_ecdsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/mith/.ssh/id_ecdsa.
Your public key has been saved in /home/mith/.ssh/id_ecdsa.pub.
The key fingerprint is:
3a:43:37:6d:e2:5b:97:e2:6f:e2:80:f9:23:97:70:0c mith@middleearth
```

Verrà chiesto di specificare un percorso (che si dovrebbe lasciare come di default), comunque l'importante è la passphrase. Verranno tralasciate in questa guida, le regole per una buona passphrase, dando per scontato che le si conoscano.

Cosa è successo? Ciò che si è appena ottenuto è una coppia di chiavi a 521 bit di lunghezza (`-b 521`) ECDSA pubblica/privata (`-t ecdsa`) contenente un commento con alcune informazioni (`-C"$(id -un)"@$(hostname)-$(date --rfc-3339=date)`) tramite il comando `ssh-keygen`.

**Nota:** Queste chiavi verranno usate solo per l'autenticazione, la scelta di chiavi più grandi non determinerà un maggiore carico per la CPU nel trasferimento dei dati via SSH.

La crittografia ECDSA(Elliptic Curve Digital Signature Algorithm) fornisce chiavi di dimensioni inferiori ed operazioni più veloci mantenendo alto il livello di sicurezza.Viene introdotto come metodo preferito dalla versione 5.7 di OpenSSH, vedere [OpenSSH 5.7 Note di rilascio](http://openssh.org/txt/release-5.7). Le chiavi ECDSA potrebbero non essere compatibili con sistemi che utilizzano versioni più vecchie di OpenSSH.

Se si desidera creare una coppia di chiavi RSA(da 2048 a 4096 bit di lunghezza) oppure DSA(1024 bit), anziché ECDSA, usare `-t rsa` oppure `-t dsa` e non dimenticare di incrementare la dimensione delle chiavi; eseguire `ssh-keygen` senza l'opzione `-b` solitamente fornirà comunque chiavi di dimensioni ragionevoli.

## Copiare la chiave pubblica al server remoto

Ora che sono state generate le chiavi, bisogna copiarle la chiave pubblica (`*.pub`) sul server remoto. (La chiave privata viene mantenuta sul pc da cui verrà effettuata la connessione.)

### Metodo semplice

**Nota:** Se si utilizza un Ternimal su un Mac, sarà necessario [installare ssh-copy-id](http://phildawson.tumblr.com/post/484798267/ssh-copy-id-in-mac-os-x) prima di procedere.

Se il nome della chiave è `id_rsa.pub` basterà semplicemente invocare il comando

```
$ ssh-copy-id tuo-server.org

```

oppure se si usa un nome utente differente dal proprio

```
$ ssh-copy-id nome-utente-per-accedere@tuo-server.org

```

Se il nome della chiave non è quello standard si otterrà il seguente errore: "/usr/bin/ssh-copy-id: ERROR: No identities found". In questo caso sarà necessario specificare esplicitamente il percorso della chiave:

```
$ ssh-copy-id -i ~/.ssh/id_ecdsa.pub nome-utente-per-accedere@tuo-server.org

```

Se necessario, è possibile specificare la porta nella dichiarazione dell'host:

```
$ ssh-copy-id -i ~/.ssh/id_rsa.pub '-p 221 nomeutente@host'

```

### Metodo tradizionale

Per impostazione predefinita di OpenSSH, la chiave pubblica deve essere concatenata in `~/.ssh/authorized_keys`.

```
$ scp ~/.ssh/id_ecdsa.pub mith@metawire.org:

```

Questo comando copia la chiave pubblica (`id_dsa.pub`) sul server remoto tramite scp (notare il **`:`** alla fine dell'indirizzo del server). Il file finisce nella cartella home, ma è comunque possibile specificare un altro percorso.

A continuazione, sul server remoto, è necessario creare la cartella `~/.ssh` se non esiste, e concatenare il file chiave `authorized_keys`:

```
$ ssh mith@metawire.org
mith@metawire.org's password:
$ mkdir ~/.ssh
$ cat ~/id_ecdsa.pub >> ~/.ssh/authorized_keys
$ rm ~/id_ecdsa.pub
$ chmod 600 ~/.ssh/authorized_keys

```

Gli ultimi due comandi rimuovono la chiave pubblica dal server (non necessaria adesso), e ne definisce i permessi corretti sul file `authorized_keys`.

Se ora ci si disconnette dal server, e si prova a ricollegarsi, dovrebbe venire richiesta la passphrase della chiave:

```
$ ssh mith@metawire.org
Enter passphrase for key '/home/mith/.ssh/id_ecdsa':

```

Se non è possibile effettuare il login con la chiave, controllare i permessi sul file `authorized_keys`.

Controllare anche i permessi della cartella `~/.ssh`, che non dovrebbe avere permessi di scrittura per "group" e "other". Eseguire il seguente comando per disattivare i permessi di scrittura di "group" e "other" alla cartella `~/.ssh`:

```
$ chmod go-w ~/.ssh

```

## Disabilitare i login con la password

Impostare le chiavi SSH non basta per garantire maggiore sicurezza. Sarà necessario disabilitare i login tramite password:

 `/etc/ssh/sshd_config` 
```
PasswordAuthentication no
ChallengeResponseAuthentication no
```

## Memorizzare le passphrase delle chiavi

Ora si può accedere ai propri server utilizzando una chiave invece di una password, ma è realmente più facile, dal momento che c'è ancora bisogno di immettere la key passphrase? La risposta è quella di utilizzare un agente SSH, un programma che ricorda la passphrase delle proprie chiavi! C'è un certo numero di strumenti a disposizione, quindi fare una ricerca e scegliere quello che sembra più adatto alle proprie esigenze.

### ssh-agent

ssh-agent è l'agente predefinito fornito da OpenSSH.

```
$ ssh-agent
SSH_AUTH_SOCK=/tmp/ssh-vEGjCM2147/agent.2147; export SSH_AUTH_SOCK;
SSH_AGENT_PID=2148; export SSH_AGENT_PID;
echo Agent pid 2148;

```

Quando si esegue `ssh-agent` verranno stampate le variabili d'ambiente che si stanno per utilizzare. Per usufruire di queste variabili eseguire il comando tramite `eval`.

```
$ eval `ssh-agent`
Agent pid 2157

```

È possibile aggiungere il seguente comando al file `/etc/profile` in modo che venga eseguito ogni volta che si apre una nuova sessione:

```
$ echo 'eval `ssh-agent`' >> /etc/profile

```

Notare le differenti virgolette, alcune sono apici, altre sono virgolette arricciate!

Ora che `ssh-agent` è in esecuzione, bisognerà istruirlo sull'esistenza di una chiave privata e relativa ubicazione.

```
$ ssh-add ~/.ssh/id_ecdsa
Enter passphrase for /home/user/.ssh/id_ecdsa:
Identity added: /home/user/.ssh/id_ecdsa (/home/user/.ssh/id_ecdsa)

```

Viene richiesta la passphrase, la si immette, ed è finito. Ora si può accedere al server remoto senza dover inserire la password, mentre la chiave privata viene protetta da password.

L'unico aspetto negativo è che una nuova istanza di `ssh-agent` deve essere creata per ogni nuova console (shell) aperta, il che significa che è necessario eseguire `ssh-add` ogni volta su ogni console. C'è una soluzione a questo inconveniente con un programma, o meglio uno script chiamato [keychain](http://www.gentoo.org/proj/en/keychain/index.xml) che è illustrato nella sezione successiva.

#### Uso di GnuPG Agent

L'agente [GnuPG](/index.php/GnuPG "GnuPG"), distribuito con il pacchetto [gnupg](https://www.archlinux.org/packages/?name=gnupg), ha un agente di emulazione OpenSSH. Se si utilizza GPG si potrebbe considerare l'utilizzo di questo agente per la salvaguardia delle proprie chiavi. Altrimenti si potrebbe gradire la voce di dialogo PIN che fornisce una propria gestione passphrase, e che è una cosa differente dal portachiavi.

Per iniziare a utilizzare l'agente GPG per le proprie chiavi SSH si deve prima iniziare la gpg-agent con l'opzione `--enable-ssh-support`. Esempi(non dimenticare di rendere eseguibile il file):

 `/etc/profile.d/gpg-agent.sh` 
```
#!/bin/sh

# Start the GnuPG agent and enable OpenSSH agent emulation
gnupginf="${HOME}/.gnupg/gpg-agent.info"

if pgrep -u "${USER}" gpg-agent >/dev/null 2>&1; then
    eval `cat $gnupginf`
    eval `cut -d= -f1 $gnupginf | xargs echo export`
else
    eval `gpg-agent --enable-ssh-support --daemon`
fi

```

Una volta che gpg-agent è in esecuzione si può usare ssh-add per approvare le chiavi, proprio come con un ssh-agent semplice. L'elenco delle chiavi approvate è memorizzato nel file `~/.gnupg/sshcontrol`. Una volta che la chiave è approvata, si aprirà una finestra di dialogo per l'immissione del PIN ogni volta che è necessaria la password. È possibile controllare le passphrase nel file `~/.gnupg/gpg-agent.conf`. L'esempio seguente mantiene la cache delle chiavi di gpg-agent per 3 ore:

```
 # Cache settings
 default-cache-ttl 10800
 default-cache-ttl-ssh 10800

```

Altre opzioni utili per questo file sono ad esempio, il programma di inserimento del PIN (GTK, QT o versione ncurses), keyboard grabbing, eccetera:

```
 # Environment file
 write-env-file /home/username/.gnupg/gpg-agent.info

 # Keyboard control
 #no-grab

 # PIN entry program
 #pinentry-program /usr/bin/pinentry-curses
 #pinentry-program /usr/bin/pinentry-qt4
 pinentry-program /usr/bin/pinentry-gtk-2

```

#### Utilizzo di portachiavi

[Keychain](http://www.funtoo.org/en/security/keychain/intro/) gestisce una o più chiavi private specifiche. Quando avviato richiederà la passphrase per la chiave (o chiavi) privata e la memorizzerà. In questo modo la chiave privata sarà protetta dalla password, ma non la si dovrà inserire ripetutamente.

[Installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") il pacchetto [keychain](https://www.archlinux.org/packages/?name=keychain) dai [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

Aggiungere il seguente comando nel proprio `.bashrc`,`.bash_profile`, oppure creare il file `/etc/profile.d/keychain.sh` come utente root e renderlo eseguibile (esempio `chmod 755 keychain.sh`).

```
eval `keychain --eval --nogui -Q -q id_rsa`

```

Aggiungendo l'opzione `-q` o `--quiet` al comando keychain non mostrerà l'output del comando nelle nuove sessioni. Notare anche che l'opzione `--agents` non è strettamente necessaria, perché keychain costruirà la lista automaticamente basandosi sull'esistenza di [ssh-agent](https://www.archlinux.org/packages/?name=ssh-agent) o [gpg-agent](https://www.archlinux.org/packages/?name=gpg-agent) nel sistema. Se si desidera una maggiore sicurezza sostituire -Q con --clear, anche se non sarà molto conveniente.

Se necessario, sostituire `~/.ssh/id_ecdsa` con il percorso della propria chiave privata. Per coloro che usano una shell non compatibile con bash, vedere `keychain --help` o [keychain(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/keychain.1) per maggiori informazioni sulle altre shell.

Chiudere la shell ed avviarla di nuovo. Dovrebbe apparire il portachiavi e se è il primo avvio realizzato, verrà richiesta la passphrase della chiave privata specifica.

**Metodo alternativo**

 `/etc/profile.d/keychain.sh` 
```
/usr/bin/keychain -Q -q --nogui ~/.ssh/id_ecdsa
[[ -f $HOME/.keychain/$HOSTNAME-sh ]] && source $HOME/.keychain/$HOSTNAME-sh

```

#### Utilizzo di ssh-agent e x11-ssh-askpass

È necessario avviare ssh-agent ogni volta che si avvia una nuova sessione di X. Ssh-agent verrà spento al termine della sessione X.

Installare una variante di x11-ssh-askpass, che chiederà la password ogni volta che si apre un nuova sessione di X. Sarà possibile scegliere tra l'originale [x11-ssh-askpass](https://www.archlinux.org/packages/?name=x11-ssh-askpass) [ksshaskpass](https://www.archlinux.org/packages/?name=ksshaskpass) (che utilizza [kdelibs](https://aur.archlinux.org/packages/kdelibs/)) oppure [openssh-askpass](https://www.archlinux.org/packages/?name=openssh-askpass) (che utilizza le qt) tutti reperibili dai [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

Dopo aver installato il pacchetto, chiudendo la sessione X ed effettuando nuovamente l'accesso verrà richiesta la password all'avvio della sessione X senza doverla immettere successivamente.

### GNOME Keyring

Se si utilizza il desktop [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)"), lo strumento [GNOME Keyring](http://live.gnome.org/GnomeKeyring) può essere usato come agente SSH. La configurazione è semplice, per prima cosa [installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring).

Successivamente si devono aggiungere le proprie chiavi SSH, ed inserire la parola chiave.

```
$ ssh-add ~/.ssh/id_ecdsa
Enter passphrase for /home/mith/.ssh/id_ecdsa:

```

Quando ci si connette ad un server, la chiave verrà rilevata e una finestra di dialogo richiederà la passphrase. C'è un'opzione per sbloccare la chiave automaticamente quando si effettua il login. Se la si seleziona, non sarà necessario inserire la password di nuovo.

## Risoluzione di problemi

Se sembra che il server SSH stia ignorando le vostre chiavi, assicuratevi che i permessi siano corretti sui file interessati.

Per la macchina locale:

```
$ chmod 700 ~/
$ chmod 700 ~/.ssh
$ chmod 600 ~/.ssh/id_ecdsa

```

Per la macchina remota:

```
$ chmod 700 ~/
$ chmod 700 ~/.ssh
$ chmod 600 ~/.ssh/authorized_keys

```

Se anche questo non aiuta, lanciare il demone `sshd` in modalità debug e monitorare l'output durante la connessione:

```
# /usr/sbin/sshd -d

```

## Altre risorse

*   [HOWTO: impostare le chiavi SSH (in Inglese)](http://www.arches.uga.edu/~pkeck/ssh/)
*   [OpenSSH gestione delle chiavi, Parte 1](http://www-106.ibm.com/developerworks/linux/library/l-keyc.html)
*   [OpenSSH gestione delle chiavi, Parte 2](http://www-106.ibm.com/developerworks/linux/library/l-keyc2/)
*   [OpenSSH gestione delle chiavi, Parte 3](http://www-106.ibm.com/developerworks/library/l-keyc3/)
*   [Introduzione a SSH (in Inglese)](http://kimmo.suominen.com/docs/ssh/)
*   Pagina di Manuale: [ssh-keygen(1)](http://www.openbsd.org/cgi-bin/man.cgi?query=ssh-keygen&apropos=0&sektion=0&manpath=OpenBSD+Current&arch=i386&format=html)
*   [OpenSSH 5.7 Note di rilascio](http://openssh.org/txt/release-5.7)