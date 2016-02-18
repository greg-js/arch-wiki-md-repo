Sudo (su "do") consente all'amministratore di sistema di delegare a certi utenti (o gruppi di utenti) il permesso e potere di eseguire alcuni, o tutti, i comandi in qualità di root, fornendo nel contempo traccia di tutti i comandi e le azioni eseguite.[[1]](http://www.gratisoft.us/sudo/)

## Contents

*   [1 Logica di base](#Logica_di_base)
*   [2 Installazione](#Installazione)
*   [3 Utilizzo](#Utilizzo)
*   [4 Configurazione](#Configurazione)
    *   [4.1 Utilizzare visudo](#Utilizzare_visudo)
    *   [4.2 Sudoers: il file dei permessi predefinito](#Sudoers:_il_file_dei_permessi_predefinito)
    *   [4.3 Password timeout](#Password_timeout)
*   [5 Suggerimenti](#Suggerimenti)
    *   [5.1 Abilitare il completamento con TAB per gli utenti sudo](#Abilitare_il_completamento_con_TAB_per_gli_utenti_sudo)
    *   [5.2 Eseguire applicazioni X11 con sudo](#Eseguire_applicazioni_X11_con_sudo)
    *   [5.3 Disabilitare sudo ad ogni terminale](#Disabilitare_sudo_ad_ogni_terminale)
    *   [5.4 Variabili d'ambiente](#Variabili_d.27ambiente)
    *   [5.5 Aggiungere /sbin e /usr/sbin al percorso di root](#Aggiungere_.2Fsbin_e_.2Fusr.2Fsbin_al_percorso_di_root)
    *   [5.6 Abilitare alias](#Abilitare_alias)
    *   [5.7 Insulti](#Insulti)
    *   [5.8 Password di root](#Password_di_root)
    *   [5.9 Disabilitare il login root](#Disabilitare_il_login_root)
        *   [5.9.1 kdesu](#kdesu)
        *   [5.9.2 Policykit](#Policykit)
*   [6 Sudo in modalità debug](#Sudo_in_modalit.C3.A0_debug)
    *   [6.1 Problemi SSH TTY](#Problemi_SSH_TTY)
    *   [6.2 Visualizzare privilegi utente](#Visualizzare_privilegi_utente)
    *   [6.3 Umask permissivo](#Umask_permissivo)
*   [7 Esempio di sudoers](#Esempio_di_sudoers)

## Logica di base

Sudo è un'alternativa sicura per il comando [su](/index.php/Su "Su") tradizionale. Molto spesso l'utente utilizza su (super user) per ottenere i privilegi di root. In generale, si ritiene imprudente eseguire il login come root, "il superutente", per periodi di tempo prolungati. L'utente root gode di controllo completo e assoluto su tutto il sistema, ma a grande rischio! Alcuni semplici errori possono facilmente rendere un sistema inutilizzabile, e tutte le applicazioni in esecuzione con privilegi di root consentiranno un libero accesso all'intera struttura gerarchica del file system.

Sudo invece, concede dei privilegi *temporanei* per un singolo comando (sia come root che come altro utente), ristabilendo alla fine dell'operazione lo stato di utente normale, senza privilegi di root e rendendo di conseguenza, il sistema nuovamente "in salvo" da azioni e stati a rischio. Sudo fornisce inoltre, come livello sicurezza aggiuntivo, traccia di tutti i comandi eseguiti, come anche di ogni tentativo di accesso fallito.

## Installazione

Per installare Sudo:

```
pacman -S sudo

```

In maniera predefinita, gli utenti non sono autorizzati a poter utilizzare sudo. Consultare [#Configurazione](#Configurazione) per ulteriori dettagli.

## Utilizzo

Con sudo installato e configurato, gli utenti sono idonei a eseguire comandi con `sudo` per acquisire privilegi di superutente (o anche altri). Per esempio:

```
$ sudo pacman -Syu

```

Consultare [sudo manual](http://www.gratisoft.us/sudo/man/sudo.html) per maggiori informazioni.

## Configurazione

Il file di configurazione di sudo è `/etc/sudoers`. **Questo file non deve mai essere modificato direttamente!**

### Utilizzare visudo

Il file di configurazione di sudo è `/etc/sudoers`, e dovrebbe essere sempre modificato con il comando `visudo`, che apre una copia temporanea del file di configurazione in `/etc/sudoers`, e controlla la sintassi prima di salvare le modifiche in quella reale. È imperativo che `sudoers` sia privo di errori di sintassi poiché sudo non verrà altrimenti eseguito.

**Warning:** Eventuali errori in `/etc/sudoers` possono rendere sudo inutilizzabile. Editarlo **sempre** con `visudo` per prevenirli.

L'editor predefinito è `vi`, che sarà utilizzato se non si prefissa il comando con *EDITOR=<editor>*. Si possono utilizzare altri editor, ad esempio, gedit:

```
# EDITOR=gedit visudo

```

Si può modificare in modo permanente l'impostazione a livello di sistema, per esempio `vim` aggiungendo

```
export EDITOR=vim

```

al file `~/.bashrc`. Si noti che questo non avrà effetto sulle shell già in esecuzione.

O per fare in modo che il comando `visudo` utilizzi il proprio EDITOR favorito in modo permanente, aggiungendo a `/etc/sudoers` il seguente:

```
# Defaults specification
# Reset environment by default
Defaults      env_reset
# Set default EDITOR to vim, and do not allow visudo to use EDITOR/VISUAL.
Defaults      editor=/usr/bin/vim, !env_editor

```

Notare che è necessario comunque lanciare il comando `visudo` sempre da root, anche se si utilizza un differente editor.

Prima che l'utente possa utilizzare il comando "sudo" con privilegi di root, bisogna aggiungerlo alla seguenti righe:

```
USER_NAME   ALL=(ALL) ALL

```

Permette all'utente l'accesso sudo solamente dalla macchina locale:

```
USER_NAME   HOSTNAME=(ALL) ALL

```

Permette ai membri del [gruppo](/index.php/Users_and_Groups_(Italiano)#Gruppi "Users and Groups (Italiano)") wheel l'accesso sudo senza richiedere la password:

```
%wheel      ALL=(ALL) NOPASSWD: ALL

```

dove USER_NAME è il nome utente individuale.

Un breve esempio per abilitare un utente a qualche privilegio:

```
USER_NAME HOST_NAME=/sbin/halt,/sbin/poweroff,/sbin/reboot,/usr/bin/pacman -Syu

```

L'utente è abilitato ad eseguire solo halt, poweroff, reboot e aggiornamento del sistema tramite il comando pacman, sul computer host specifico.

Un `sudoers` dettagliato d'esempio, è reperibile su [qui](http://www.gratisoft.us/sudo/sample.sudoers). Altrimenti, consultare [sudoers manual](http://www.gratisoft.us/sudo/man/sudoers.html) per ulteriori informazioni.

### Sudoers: il file dei permessi predefinito

Il proprietario e il gruppo del file sudoers devono essere impostati entrambi 0\. Il file dei permessi dovrebbe essere impostato 0440\. Questi permessi sono impostati di default, ma se modificati accidentalmente, dovrebbero essere nuovamente riconfigurati.

```
 # chown -c root:root /etc/sudoers
 # chmod -c 0440 /etc/sudoers

```

### Password timeout

Alcuni utenti potrebbero voler modificare il timeout predefinito prima che la password scada. È possibile farlo aggiungendo la riga seguente a `/etc/sudoers` (`visudo`) per esempio:

```
Defaults:USER_NAME timestamp_timeout=20

```

nel cui caso la password dell'utente USER_NAME scade se non usata per 20 minuti. Sono ammessi anche i valori tra 0 e 1.

**Tip:** Per assicurarsi che sudo richieda sempre la password, impostare il timeout a zero.

## Suggerimenti

### Abilitare il completamento con TAB per gli utenti sudo

Il completamento con TAB, di default, non funzionerà quando un utente è stato aggiunto inizialmente al file dei sudoers. Ad esempio, normalmente, Marco deve soltanto digitare:

```
fir<TAB>

```

e la shell completerà il comando come segue:

```
firefox

```

Se, comunque, Marco fosse aggiunto al file dei sudoers e digitasse:

```
sudo fir<TAB>

```

la shell non farebbe niente.

Per abilitare il completamento automatico con sudo, aggiungere il seguente al proprio `~/.bashrc`:

```
complete -cf sudo

```

In alternativa, si potrebbe anche installare e attivare bash-completion per i comandi come sudo, vedere [questo articolo](/index.php/Bash_(Italiano)#Auto-completamento "Bash (Italiano)") per ulteriori informazioni.

### Eseguire applicazioni X11 con sudo

Per consentire a sudo di avviare un'applicazione grafica in X11, è necessario aggiungere

```
Defaults env_keep += "HOME"

```

a visudo.

### Disabilitare sudo ad ogni terminale

**Attenzione:** Questo permetterà a tutti i processi di utilizzare la sessione sudo

Se infastiditi dalle impostazioni di defaults di sudo, che richiedono l'inserimento della password ogni volta che si apre un nuovo terminale, disabilitare **tty_tickets**:

```
Defaults !tty_tickets

```

### Variabili d'ambiente

Se ci si ritrova con molte variabili d'ambiente, o si esportano le impostazioni del proxy con <tt>export http_proxy="..."</tt>, quando si usa sudo queste variabili non vengono accettate da root se non si esegue sudo con l'opzione `-E`.

```
$ sudo -E pacman -Syu

```

Per questo motivo potrebbe essere utile aggiungere un alias in `~/.bashrc`:

```
alias sudo="sudo -E"

```

Un'altra modo analogo è l'aggiunta in `/etc/sudoers` di:

```
Defaults !env_reset

```

Volendo solamente passare le variabili `*_proxy`, aggiungere il seguente:

```
Defaults env_keep += "ftp_proxy http_proxy https_proxy no_proxy"

```

### Aggiungere /sbin e /usr/sbin al percorso di root

Se si desidera eseguire comandi amministrativi (quelli in `/sbin` o `/usr/sbin`) con sudo senza utilizzare il loro percorso completo, aggiungere:

```
Defaults secure_path="/bin:/sbin:/usr/bin:/usr/sbin" 

```

in `/etc/sudoers`

Questo permette di dare il comando

```
$ sudo command

```

invece di:

```
$ sudo /sbin/command

```

o:

```
$ sudo /usr/sbin/command

```

### Abilitare alias

Se si utilizzano vari alias, si noterà che non vengono accettati da root usando sudo. Tuttavia, vi è un modo semplice per farli funzionare. Basta aggiungere quanto segue a `~/.bashrc` o `/etc/bash.bashrc`:

```
alias sudo='sudo '

```

### Insulti

È possibile configurare sudo per visualizzare degli "insulti intelligenti" quando viene immessa una password errata, al posto dell'output di default "wrong password". Trovare la linea di default in `/etc/sudoers` e aggiungere "insults", separandola con una virgola dalle voci esistenti. Il risultato dovrebbe essere simile a questo:

```
#Defaults specification
Defaults insults

```

Per fare una prova, scrivere `sudo -K` per terminare la sessione corrente e lasciare che sudo chieda nuovamente la password.

### Password di root

Si può istruire sudo a richiedere la password di root invece di quella dell'utente normale aggiungendo "rootpw" alla linea di defaults in `/etc/sudoers`:

```
Defaults timestamp_timeout=0,rootpw

```

### Disabilitare il login root

**Attenzione:** Arch Linux non è stato sviluppato per funzionare con l'account root disabilitato. Con questo metodo si rischiano possibili ed eventuali problemi.

Con sudo installato e configurato, qualcuno potrebbe voler disabilitare il login di root. Senza root, eventuali malintenzionati dovrebbero prima individuare un nome utente configurato come sudoer, e poi la password dell'utente.

**Attenzione:** Assicurarsi che l'utente sia correttamente configurato come sudoer *prima* di disabilitare l'account di root!

L'account può essere bloccato con `passwd`:

```
# passwd -l root

```

Un comando simile sblocca root.

```
$ sudo passwd -u root

```

In alternativa, modificare `/etc/shadow` e sostituire la password di root criptata con "!":

```
root:!:12345::::::

```

Per abilitare il login di root di nuovo:

```
$ sudo passwd root

```

#### kdesu

kdesu può essere usato con KDE per lanciare applicazioni grafiche con privilegi di root. In maniera predefinita, è possibile che kdesu provi ad usare su anche se l'account di root è disabilitato. Fortunatamente si può istruire kdesu ad usare sudo invece di su. Creare o modificare il file `/usr/share/config/kdesurc`:

```
[super-user-command]
super-user-command=sudo

```

#### Policykit

Disabilitando l'account root, diventa necessario modificare la configurazione [PolicyKit](/index.php/PolicyKit "PolicyKit") per fare in modo che le autorizzazioni locali agiscano di conseguenza. L'impostazione predefinita è chiedere la password di root, di modo che questo deve essere modificato. Con polkit-1, ciò può essere ottenuto modificando `/etc/polkit-1/localauthority.conf.d/50-localauthority.conf` così:

```
AdminIdentities=unix-user:0

```

è sostituito da qualcosa d'altro, a seconda della configurazione del sistema. Può essere un elenco di utenti e gruppi, per esempio

```
AdminIdentities=unix-group:wheel

```

oppure

```
AdminIdentities=unix-user:me;unixuser:mom;unix-group:wheel

```

Per ulteriori informazioni, consultare `man pklocalauthority`

## Sudo in modalità debug

### Problemi SSH TTY

SSH non assegna una tty per impostazione predefinita quando si esegue un comando remoto. Senza un terminale, sudo non può disabilitare echo quando viene richiesta una password. Si può usare ssh con l'opzione "-tt" per forzarlo a destinare una tty. (usare -tt due volte).

L'opzione di default requiretty consente solo agli utenti di eseguire sudo se hanno una tty

```
# Disable "ssh hostname sudo <cmd>", because it will show the password in clear. You have to run "ssh -t hostname sudo <cmd>".
#
#Defaults    requiretty

```

### Visualizzare privilegi utente

Si possono controllare i privilegi di un utente specifico con il seguente comando:

```
 sudo -lU proprionomeutente

```

O visualizzare i propri con

```
 sudo -l

```

```
Matching Defaults entries for proprionomeutente on this host:
    loglinelen=0, logfile=/var/log/sudo.log, log_year, syslog=auth, mailto=sqpt.webmaster@gmail.com, mail_badpass, mail_no_user, mail_no_perms, env_reset, always_set_home, tty_tickets, lecture=always, pwfeedback, rootpw, set_home

L'utente proprionomeutente può eseguire i seguenti comandi su questo host:
    (ALL) ALL, 
    (ALL) NOPASSWD: /usr/sbin/lsof, /bin/nice, /usr/sbin/ss, /usr/bin/su, /usr/bin/locate, /usr/bin/find, /usr/bin/rsync, /usr/bin/strace, 
    (ALL) /bin/nice, /bin/kill, /usr/bin/nice, /usr/bin/ionice, /usr/bin/top, /usr/bin/kill, /usr/bin/killall, /usr/bin/ps, /usr/bin/pkill, 
    (ALL) /usr/sbin/gparted, /usr/bin/pacman, /usr/bin/powerpill, 
    (ALL) /usr/local/bin/synergyc, /usr/local/bin/synergys, 
    (ALL) /usr/bin/vim, /usr/bin/nano, /usr/bin/cat
    (root) NOPASSWD: /usr/local/bin/synergyc

```

### Umask permissivo

Sudo riunisce il valore [umask](/index.php/Umask "Umask") dell'utente con il proprio (che per impostazione predefinita è 0022). Questo impedisce a sudo di creare file con più autorizzazioni di quante l'umask dell'utente permetta. Nonostante sia un valore predefinito accettabile se non ci sono umask personalizzati in uso, potrebbe portare a situazioni in cui un programma gestito con sudo crei dei file con autorizzazioni diverse da quelle ottenute se fosse stato eseguito da root. Se si incorre in questo tipo di errori, sudo fornisce un mezzo per fissare l'umask, anche nel caso l'umask sia più permissivo rispetto all'umask specificato dall'utente. L'aggiunta delle seguenti righe (usando `visudo`) modificheranno tale comportamento predefinito di sudo

```
Defaults umask = 0022
Defaults umask_override

```

impostandone i valori umask predefiniti a quelli di root (0022).

## Esempio di sudoers

Ciò è particolarmente utile a coloro che usano i terminali multiplexer come screen, tmux, o ratpoison, o che usano sudo da scripts e/o cronjobs.

```

Cmnd_Alias WHEELER = /usr/sbin/lsof, /bin/nice, /bin/ps, /usr/bin/top, /usr/local/bin/nano, /usr/sbin/ss, /usr/bin/locate, /usr/bin/find, /usr/bin/rsync
Cmnd_Alias PROCESSES = /bin/nice, /bin/kill, /usr/bin/nice, /usr/bin/ionice, /usr/bin/top, /usr/bin/kill, /usr/bin/killall, /usr/bin/ps, /usr/bin/pkill
Cmnd_Alias EDITS = /usr/bin/vim, /usr/bin/nano, /usr/bin/cat, /usr/bin/vi
Cmnd_Alias ARCHLINUX = /usr/sbin/gparted, /usr/bin/pacman, /usr/bin/powerpill

root ALL = (ALL) ALL
proprionomeutente ALL = (ALL) ALL, NOPASSWD: WHEELER, NOPASSWD: PROCESSES, NOPASSWD: ARCHLINUX, NOPASSWD: EDITS

Defaults !requiretty, !tty_tickets, !umask
Defaults visiblepw, path_info, insults, lecture=always
Defaults loglinelen = 0, logfile =/var/log/sudo.log, log_year, log_host, syslog=auth
Defaults mailto=webmaster@proprionomeutente.com, mail_badpass, mail_no_user, mail_no_perms
Defaults passwd_tries = 8, passwd_timeout = 1
Defaults env_reset, always_set_home, set_home, set_logname
Defaults !env_editor, editor="/usr/bin/vim:/usr/bin/vi:/usr/bin/nano"
Defaults timestamp_timeout=360
Defaults passprompt="Sudo invoked by [%u] on [%H] - Cmd run as %U - Password for user %p:"

```