[systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)") offre agli utenti la possibilità di gestire i servizi sotto il controllo dell'utente tramite una istanza di systemd per singolo utente, che consente agli stessi di avviare, fermare, abilitare e disabilitare le proprie unità. Questa caratteristica è utile per demoni e altre operazioni automatiche come lo scaricamento della posta. È inoltre possibile, con alcune modifiche, avviare Xorg e il window manager in uso direttamente tramite i servizi utente.

## Contents

*   [1 Come funziona](#Come_funziona)
*   [2 Configurazione di base](#Configurazione_di_base)
    *   [2.1 D-Bus](#D-Bus)
    *   [2.2 Variabili d'ambiente](#Variabili_d.27ambiente)
        *   [2.2.1 DISPLAY e XAUTHORITY](#DISPLAY_e_XAUTHORITY)
        *   [2.2.2 PATH](#PATH)
    *   [2.3 Avvio automatico delle istanze utente di systemd](#Avvio_automatico_delle_istanze_utente_di_systemd)
*   [3 Xorg e systemd](#Xorg_e_systemd)
    *   [3.1 Login automatico in Xorg senza display manager](#Login_automatico_in_Xorg_senza_display_manager)
    *   [3.2 Avvio di Xorg come servizio utente](#Avvio_di_Xorg_come_servizio_utente)
*   [4 Scrivere servizi utente](#Scrivere_servizi_utente)
    *   [4.1 Esempio](#Esempio)
    *   [4.2 Esempio con variabili](#Esempio_con_variabili)
    *   [4.3 Nota per applicazioni X11](#Nota_per_applicazioni_X11)
*   [5 Esempi d'uso](#Esempi_d.27uso)
    *   [5.1 Multiplexer di terminale persistente](#Multiplexer_di_terminale_persistente)
    *   [5.2 Window manager](#Window_manager)
*   [6 Riferimenti](#Riferimenti)

## Come funziona

Secondo la configurazione di default in `/etc/pam.d/system-login`, il modulo `pam_systemd` avvia automaticamente una istanza di `systemd --user` al primo login dell'utente. Tale processo rimarrà in esecuzione fin tanto che l'utente sarà coneesso, e verrà terminato quando l'utente effettua il logout. Quando l'[#Avvio automatico delle istanze utente di systemd](#Avvio_automatico_delle_istanze_utente_di_systemd) è abilitato, l'istanza viene avviata al boot e non più terminata. L'istanza utente di systemd si occupa di gestire i servizi utente, utilizzabili per avviare demoni o compiere operazioni automatiche, disponendo comunque di tutti i benefici di systemd, come l'attivazione socket, timers, dipendenze o controllo processi tramite cgroups. Similmente a quanto accade con in servizi di sistema, i servizi utente risiedono nelle directory seguenti (ordinate per preferenza crescente):

*   `/usr/lib/systemd/user/` directory per i servizi forniti dai pacchetti.
*   `/etc/systemd/user/` directory per i servizi definiti dall'amministratore di sistema.
*   `~/.config/systemd/user/` directory per i servizi utente.

All'avvio di una istanza utente di systemd, viene caricato il target `default.target`; è ora possibile controllare manualmente i servizi utente tramite `systemctl --user`.

**Attenzione:**

*   Si noti che, a partire dalla versione 206, l'istanza utente `systemd --user` è un processo dedicato per utente, e non per sessione. Ne consegue che la maggior parte delle risorse gestite dai servizi utenti, come sockets o file di stato, riguardano un singolo utente (sono difatti situati nella home directory dello stesso) e non una sessione. Ciò significa che tutti i servizi utente vengono eseguiti al di fuori di una sessione; per questo motivo, i programmi che necessitano di essere eseguiti per ogni singola sessione probabilmente non funzioneranno con le istanze utente di systemd. La gestione delle sessioni da parte di systemd varia continuamente. Si legga [[1]](https://mail.gnome.org/archives/desktop-devel-list/2014-January/msg00079.html) e [[2]](http://lists.freedesktop.org/archives/systemd-devel/2014-March/017552.html) per avere un'idea generale sullo sviluppo di questa funzionalità.
*   `systemd --user` viene eseguito come processo separato rispetto a `systemd --system`. I servizi utente non possono pertanto riferirsi o dipendere da servizi di sistema.

## Configurazione di base

Tutti i servizi utente devono essere inseriti in `~/.config/systemd/user`. Se si vuole avviare une servizio automaticamente al login, si esegua `systemctl --user enable _servizio_` per ogni servizio.

### D-Bus

Alcune applicazioni necessitano di un messagebus [D-Bus](/index.php/D-Bus "D-Bus"), tradizionalmente avviato quando si esegue un desktop environment tramite `dbus-launch`. A partire dalla versione 226, systemd è divenuto il gestore del messagebus utente. [[3]](https://www.archlinux.org/news/d-bus-now-launches-user-buses/) Il demone _dbus-daemon_ viene avviato una volta per ogni sessione utente utilizzando le unità utente `dbus.socket` e `dbus.service`.

**Nota:** Se precedentemente si sono creati tali file manualmente nella cartella `/etc/systemd/user/` o `~/.config/systemd/user/`, è ora possibile rimuoverli.

### Variabili d'ambiente

L'istanza utente di systemd non eredita le [variabili d'ambiente](/index.php/Environment_variables "Environment variables") definite in `.bashrc` e similari. Vi sono quattro modi per definire variabili d'ambiente per istanze utente di systemd:

1.  Per gli utenti che abbiano una propria home directory, si specifichi l'opzione `DefaultEnvironment` in `~/.config/systemd/user.conf`. Viene applicata solo alle unità utente di un utente specifico.
2.  Utilizzare l'opzione `DefaultEnvironment` in `/etc/systemd/user.conf`. Viene applicata a tutti i servizi utente.
3.  Creare un file di configurazione in `/etc/systemd/system/user@.service.d/`. Viene applicata a tutti i servizi utente.
4.  In qualsiasi momento, tramite i comandi `systemctl --user set-environment` o `systemctl --user import-environment`. Applicata a tutti i servizi avviati dopo l'esecuzione dei comandi di cui sopra, ma non a quelli già avviati.

**Suggerimento:** Per definire più variabili contemporaneamente, si crei un file di configurazione contentente una lista di coppie _chiave=valore_, separate da uno spazio, e si aggiunga `xargs systemctl --user set-environment < /path/to/file.conf` al file di configurazione utente della shell in uso.

Una variabile che si potrebbe voler definire è `PATH`.

#### DISPLAY e XAUTHORITY

La variabile `DISPLAY` viene utilizzata da qualsiasi applicazione X per individuare il display da utilizare, mentre `XAUTHORITY` identifica il percorso al file `.Xauthority` dell'utente corrente, e di conseguenza il cookie necessario per accedere a X. Se si intende lanciare applicazioni grafiche tramite servizi di systemd, sarà necessario definire tali variabili. A partire dalla [versione 219](http://cgit.freedesktop.org/systemd/systemd/tree/NEWS?id=v219#n194), systemd fornisce uno script situato in `/etc/X11/xinit/xinitrc.d/50-systemd-user.sh` per importarle nella sessione utente di systemd all'avvio di X. Ne consegue che, a meno che X non venga avviato tramite procedure non standard, i servizi utenti dovrebbero essere già al corrente dei valori delle due variabili.

#### PATH

Come tutte le variabili d'ambiente definite tramite `.bashrc` o `.bash_profile`, anche `PATH` non è visibile a systemd. Se si modifica il valore di tale variabile e si intende avviare applicazioni che se ne avvalgano come servizi di systemd, sarà necessario notificare systemd della sua modifica. È consigliabile farlo aggiungendo la seguente riga al proprio `.bash_profile`, dopo aver definito la variabile `PATH`:

 `~/.bash_profile` 

```
systemctl --user import-environment PATH

```

### Avvio automatico delle istanze utente di systemd

L'istanza utente di systemd viene avviata dopo il primo login di un utente, e fermata alla chiusura dell'ultima sessione di quell'utente. Potrebbe essere talvolta necesario avviarla subito dopo il boot, e mantenerla attiva alla chiusura dell'ultima sessione utente relativa, ad esempio per avere processi utente attivi senza alcuna sesione utente in corso. Si esegua a tal proposito il seguente comando per abilitare tale comportamento per un singolo utente:

```
# loginctl enable-linger _nomeutente_

```

**Attenzione:** I servizi systemd **non** sono sessioni, dal momento che vengono eseguiti al di fuori di _logind_. Non si utilizzi la funzionalità di lingering per abilitare il login autometico, dal momento che questo [renderà inutilizzabile la sessione](/index.php/General_troubleshooting#Session_permissions "General troubleshooting").

## Xorg e systemd

Vi sono diversi metodi per avviare Xorg tramite systemd. Di seguito due possibilità: l'avvio di una sessione utente con un processo di Xorg o l'avvio di quest'ultimo come servizio utente.

### Login automatico in Xorg senza display manager

Quanto sotto avvierà una sessione utente ed il server Xorg come unità di sistema e provvederà poi a leggere il contenuto di `~/.xinitrc`, avviare il window manager, ecc.

Sarà necessario configurare [#D-Bus](#D-Bus) nel modo corretto ed installare il pacchetto [xlogin-git](https://aur.archlinux.org/packages/xlogin-git/).

Si crei il proprio file [xinitrc](/index.php/Xinitrc_(Italiano) "Xinitrc (Italiano)") da quello di default, in modo che effettui il source dei files in `/etc/X11/xinit/xinitrc.d/`. È necessario che l'esecuzione del priorio `~/.xinitrc` non ritorni, quindi si inserisca `wait` come ultimo comando, o si aggiunga `exec` all'ultimo comando (ad esempio, il proprio window manager).

Questa sessione utilizzerà il proprio demone D-Bus, ma varie utility di systemd si connetteranno automaticamente all'istanza avviata dal servizio `dbus.service`

Si abiliti infine (**come root**) il servizio _xlogin_ per ottenere il login automatico al boot:

```
# systemctl enable xlogin@_username_

```

La sessione utente viene eseguita interamente in un ambiente systemd, quindi tutto dovrebbe funzionare nel modo corretto.

### Avvio di Xorg come servizio utente

In alternativa, è possibile avviare [xorg](/index.php/Xorg_(Italiano) "Xorg (Italiano)") come servizio utente, avendo il vantaggio di poter definire il servizio in questione come dipendenza di altre unità che lo necessitino. Questo approccio, tuttavia, non è esente da difetti, elencati sotto:

A partire dalla versione 1.16, [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) si integra in modo migliore con systemd in due modi:

*   Può essere avviato senza privilegi di root, delegando la gestione dei dispositivi a logind (si vedano i commit di Hans de Goede [this qui](http://cgit.freedesktop.org/xorg/xserver/commit/?id=82863656ec449644cd34a86388ba40f36cea11e9)).
*   Può essere avviato come servizio attivato tramite socket (si veda [questo commit](http://cgit.freedesktop.org/xorg/xserver/commit/?id=b3d3ffd19937827bcbdb833a628f9b1814a6e189)).

Sfortunatamente, per avviare Xorg senza privilegi di amministratore, è necessario essere in una sessione, perciò, in questo momento, è necessario avviare Xorg come amministratore per poterlo gestire tramite i servizi utente (come per versioni precedenti la 1.16).

**Nota:** Si noti che quanto sopra non è una restrizione imposta da logind: Xorg necessita infatti di sapere di quale sessione appropriarsi e, ad ora, ottiene questa informazione chiamando la funzione `GetSessionByPID` di [logind](http://www.freedesktop.org/wiki/Software/systemd/logind), utilizzando il proprio PID come argomento. Si vedano [questo thread](http://lists.x.org/archives/xorg-devel/2014-February/040476.html) e [i sorgenti di Xorg](http://cgit.freedesktop.org/xorg/xserver/tree/hw/xfree86/os-support/linux/systemd-logind.c). È probabilmente possibile modificare Xorg in modo che ottenga la sessione dalla tty sulla quale viene avviata.

Di seguito le istruzioni per avviare Xorg come servizio utente

1\. Assicurarsi che Xorg possa venire avviato con privilegi da amministratore da qualsiasi utente, modificando `/etc/X11/Xwrapper.config`:

 `/etc/X11/Xwrapper.config` 

```
allowed_users=anybody
needs_root_rights=yes

```

2\. Creare le seguenti unità in `~/.config/systemd/user`:

 `~/.config/systemd/user/xorg@.socket` 

```
[Unit]
Description=Socket for xorg at display %i

[Socket]
ListenStream=/tmp/.X11-unix/X%i

```

 `~/.config/systemd/user/xorg@.service` 

```
[Unit]
Description=Xorg server at display %i

Requires=xorg@%i.socket
After=xorg@%i.socket

[Service]
Type=simple
SuccessExitStatus=0 1

ExecStart=/usr/bin/Xorg :%i -nolisten tcp -noreset -verbose 2 "vt${XDG_VTNR}"

```

Dove `${XDG_VTNR`} è il terminale virtuale dove Xorg verrà eseguito, definito all'interno del servizio utente, o specificato come variabile d'ambiente in systemd tramite:

```
$ systemctl --user set-environment XDG_VTNR=1

```

**Nota:** Xorg dovrebbe essere lanciato dallo stesso terminale virtuale dove si è effettuato il login, altrimenti loging considererà la sessione come inattiva.

3\. Assicurarsi di definire la variabile d'ambiente `DISPLAY` come spiegato [sopra](#DISPLAY).

4\. Per abilitare l'attivazione socket per Xorg sul display 0 e tty2, si procederebbe come segue:

```
$ systemctl --user set-environment XDG_VTNR=2     # Per dichiarare a xorg@.service quale terminale utilizzare
$ systemctl --user start xorg@0.socket            # Resta in ascolto sul socket del display 0

```

A questo punto, qualsiasi applicazione X11 verrà eseguita automaticamente sul terminale virtuale 2.

La variabile d'ambiente `XDG_VTNR` può essere definita nell'ambiente di systemd partendo da `.bash_profile`, cosa che renderebbe possibile avviare qualsiasi applicazione X11, compreso un window manager, come unità utente systemd, inserendo una dipendenza a `xorg@0.socket`.

**Attenzione:** Al momento, l'esecuzione di un window manager come servizio utente ne comporta l'avvio al di fuori della sessione, con tutti i problemi che ciò comporta: [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting"). Sembra però che gli sviluppatori di systemd stiano tentando di rendere possibile tale comportamento. Si veda a tal proposito [[4]](https://mail.gnome.org/archives/desktop-devel-list/2014-January/msg00079.html) e [[5]](http://lists.freedesktop.org/archives/systemd-devel/2014-March/017552.html).

## Scrivere servizi utente

### Esempio

Di seguito un esempio per l'avvio di mpd come servizio utente:

 `~/.config/systemd/user/mpd.service` 

```
[Unit]
Description=Music Player Daemon

[Service]
ExecStart=/usr/bin/mpd --no-daemon

[Install]
WantedBy=default.target

```

### Esempio con variabili

Esempio di avvio di `sickbeard` come servizio utente, con definizione di una variabile utente per la directory home dove Sickbeard reperisce alcuni file di configurazione:

 `~/.config/systemd/user/sickbeard.service` 

```
[Unit]
Description=SickBeard Daemon

[Service]
ExecStart=/usr/bin/env python2 /opt/sickbeard/SickBeard.py --config %h/.sickbeard/config.ini --datadir %h/.sickbeard

[Install]
WantedBy=default.target

```

Come specificato in `man systemd.unit`, la variabile `%h` viene sostituita con la home directory dell'utente che esegue il servizio. Vi sono altre variabili disponibili, spiegate in dettaglio nelle pagine di manuale di [systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)").

### Nota per applicazioni X11

La maggior parte delle applicazioni X11, necessitano della variabile `DISPLAY` per essere eseguite. Vedere a tal proposito la sezione [#DISPLAY e XAUTHORITY](#DISPLAY_e_XAUTHORITY).

## Esempi d'uso

### Multiplexer di terminale persistente

You may wish your user session to default to running a terminal multiplexer, such as [GNU Screen](/index.php/GNU_Screen "GNU Screen") or [Tmux](/index.php/Tmux "Tmux"), in the background rather than logging you into a window manager session. Separating login from X login is most likely only useful for those who boot to a TTY instead of to a display manager (in which case you can simply bundle everything you start in with myStuff.target).

To create this type of user session, procede as above, but instead of creating wm.target, create multiplexer.target:

```
[Unit]
Description=Terminal multiplexer
Documentation=info:screen man:screen(1) man:tmux(1)
After=cruft.target
Wants=cruft.target

[Install]
Alias=default.target
```

`cruft.target`, like `mystuff.target` above, should start anything you think should run before tmux or screen starts (or which you want started at boot regardless of timing), such as a GnuPG daemon session.

You then need to create a service for your multiplexer session. Here is a sample service, using tmux as an example and sourcing a gpg-agent session which wrote its information to `/tmp/gpg-agent-info`. This sample session, when you start X, will also be able to run X programs, since DISPLAY is set.

```
[Unit]
Description=tmux: A terminal multiplixer
Documentation=man:tmux(1)
After=gpg-agent.service
Wants=gpg-agent.service

[Service]
Type=forking
ExecStart=/usr/bin/tmux start
ExecStop=/usr/bin/tmux kill-server
Environment=DISPLAY=:0
EnvironmentFile=/tmp/gpg-agent-info

[Install]
WantedBy=multiplexer.target
```

Once this is done, `systemctl --user enable` `tmux.service`, `multiplexer.target` and any services you created to be run by `cruft.target` and you should be set to go! Activated `user-session@.service` as described above, but be sure to remove the `Conflicts=getty@tty1.service` from `user-session@.service`, since your user session will not be taking over a TTY. Congratulations! You have a running terminal multiplexer and some other useful programs ready to start at boot!

### Window manager

Per eseguire un window manager come servizio di systemd, sarà necessario [avviare Xorg come servizio utente](#Avvio_di_Xorg_come_servizio_utente). Di seguito, un esempio utilizzando awesome:

 `~/.config/systemd/user/awesome.service` 

```
[Unit]
Description=Awesome window manager
After=xorg.target
Requires=xorg.target

[Service]
ExecStart=/usr/bin/awesome
Restart=always
RestartSec=10

[Install]
WantedBy=wm.target

```

**Nota:** La sezione `[Install]` include una direttiva `WantedBy`. All'utilizzo di `systemctl --user enable`, verrà creato il link `~/.config/systemd/user/wm.target.wants/_window_manager_.service`, consentendo l'avvio al login. Si raccomanda l'abilitazione di questo servizio, e non la creazione manuale del link simbolico.

## Riferimenti

*   [Wiki Bitbucket di KaiSforza](https://bitbucket.org/KaiSforza/systemd-user-units/wiki/Home)
*   [Servizi di Zoqaeski su GitHub](https://github.com/zoqaeski/systemd-user-units)
*   [Collezione di servizi utente systemd](https://github.com/grawity/systemd-user-units)
*   [Discussione sul forum di Arch a seguito dei cambiamenti introdotti a partire da systemd 206](https://bbs.archlinux.org/viewtopic.php?id=167115)