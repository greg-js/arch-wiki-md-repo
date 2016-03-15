**Attenzione:** Dal [sito internet](http://www.freedesktop.org/wiki/Software/ConsoleKit) di Consolekit:

	*ConsoleKit non è più sviluppato attivamente. L'attenzione si è spostata sulla funzione integrata seat/user/session del software/systemd chiamato systemd-loginctl.*

ConsoleKit è un framework per gestire i permessi e le sessioni degli utenti. I compiti che più comunemente vengono affidati a ConsoleKit sono: abilitare gli utenti non-root a montare dispositivi usb e permettere loro sospensione e spegnimento del pc (ad esempio [Thunar](/index.php/Thunar_(Italiano) "Thunar (Italiano)"), Nautilus e il menu di spegnimento di [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)") fanno uso di ConsoleKit).

Considerando che Consolekit non è più sviluppato, potrebbe essere una buona idea prendere in considerazione le varie alternative: [udev](/index.php/Udev_(Italiano) "Udev (Italiano)"), [udiskie](/index.php/Udiskie "Udiskie") e [polkit](/index.php/Polkit "Polkit"). Altrimenti si prenda in considerazione di switchare completamente su [Systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)").

## Contents

*   [1 Installazione](#Installazione)
*   [2 Rimpiazzare ConsoleKit con systemd-logind](#Rimpiazzare_ConsoleKit_con_systemd-logind)
*   [3 ConsoleKit e i Display Manager](#ConsoleKit_e_i_Display_Manager)
    *   [3.1 ck-launch-session](#ck-launch-session)
    *   [3.2 Lanciare applicazioni direttamente da ~/.xinitrc](#Lanciare_applicazioni_direttamente_da_.7E.2F.xinitrc)
    *   [3.3 No display manager](#No_display_manager)
*   [4 Usare dbus per operazioni di sospensione/spegnimento/riavvio ecc](#Usare_dbus_per_operazioni_di_sospensione.2Fspegnimento.2Friavvio_ecc)
*   [5 Ulteriori risorse](#Ulteriori_risorse)

## Installazione

Consolekit non è più nei repository di Arch in quanto non più attivamente sviluppato. Usare consolekit è quindi **fortemenente sconsigliato**.

## Rimpiazzare ConsoleKit con systemd-logind

**Nota:** A partire da [polkit](https://www.archlinux.org/packages/?name=polkit) 0.107-4, **Consolekit** è completamente rimpiazzato da `systemd-logind`, quindi perchè il proprio sistema funzioni correttamente è consigliato usare [systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)").

Un buon metodo per rimuovere **Consolekit** è effettuare un [Login Automatico in una console virtuale](/index.php/Login_Automatico_in_una_console_virtuale "Login Automatico in una console virtuale") e [avviare X da qui](/index.php/Start_X_at_Boot_(Italiano) "Start X at Boot (Italiano)"). È molto importante che il server grafico sia avviato sulla stessa console nella quale viene effettuato l'accesso, in caso contrario infatti, logind non sarà in grado di tenere traccia della sessione utente. Rimuovere quindi `ck-launch-session` da `~/.xinitrc` (vedere [Xinitrc](/index.php/Xinitrc_(Italiano) "Xinitrc (Italiano)") per ulteriori informazioni).

Per verificare lo stato della propria sessione è possibile usare il comando `loginctl`. Tale comando mostrerà se la sessione di `logind` è attiva, mostrando in questo caso un `Active=yes`. Tutte le operazioni di [Policykit](/index.php/Policykit "Policykit") (spegnimento/ibernazione ecc) e di [Udisks](/index.php/Udisks "Udisks") (mount dei dispositivi) ora dovrebbero funzionare in automatico

```
$ loginctl show-session $XDG_SESSION_ID

```

## ConsoleKit e i [Display Manager](/index.php/Display_Manager_(Italiano) "Display Manager (Italiano)")

### ck-launch-session

Per lanciare la sessione di [Xorg](/index.php/Xorg_(Italiano) "Xorg (Italiano)") con consolekit aggiungere alla riga `exec` di `~/.xinitrc` ad esempio:

```
exec ck-launch-session openbox-session

```

Questo lancerà una sessione di [Openbox](/index.php/Openbox_(Italiano) "Openbox (Italiano)") con le variabili d'ambiente appropriate in modo tale da abilitare ConsoleKit a tutti i processi conseguenti.

[Display managers](/index.php/Display_Manager_(Italiano) "Display Manager (Italiano)") come [KDM](/index.php/KDM_(Italiano) "KDM (Italiano)"), [GDM](/index.php/GDM "GDM"), [SLiM](/index.php/SLiM_(Italiano) "SLiM (Italiano)") e [LXDM](/index.php/LXDM "LXDM") lanciano ConsoleKit automaticamente con ogni sessione di X.

**Nota:**

*   Se il proprio DM fornisce già una sessione di consolekit non provare ad avviarne un'altra, il risultato sarebbe un crash dello stesso consolekit.
*   In particolare, è fondamentale, NON inserire `ck-launch-session` nel file `~/.xinitrc` se si usa [SLiM](/index.php/SLiM_(Italiano) "SLiM (Italiano)").

### Lanciare applicazioni direttamente da ~/.xinitrc

Se si usa il file [Xinitrc](/index.php/Xinitrc_(Italiano) "Xinitrc (Italiano)") per lanciare delle applicazioni nella propria sessione di X, non è detto che tutte queste vengano eseguite con le variabili d'ambiente appropriate per abilitare correttamente la sessione di ConsoleKit. Nel seguente esempio solo i processi "figli" di Compiz saranno correttamente abilitati all'uso di ConsoleKit, mentre i figli di Xterm non lo saranno.

 `~/.xinitrc` 
```
xterm &
exec ck-launch-session compiz ccp
```

Tipicamente, questo problema riguarda Compiz standalone e alcune altre applicazioni cone i launchers, (gnome-do, kupfer, gmrun, xbindkeys, ecc.) che non saranno quindi abilitati all'uso di ConsoleKit. Il metodo per aggirare questo problema è avviare tutta la sessione in un secondo script, ad esempio `~/.xstart`. Non dimenticare `dbus-launch` se necessario. Esempio:

 `~/.xinitrc` 
```
exec ck-launch-session dbus-launch $HOME/.xstart

```
 `~/.xstart` 
```
compiz ccp &
Thunar &
Terminal

```

È importante non dimenticare di rendere `~/.xstart` eseguibile, dando da root:

```
$ chmod +x ~/.xstart

```

Per vedere se la sessione è partita correttamente usare il seguente comando:

```
$ ck-list-sessions

```

L'output dovrebbe essere qualcosa tipo:

```
Session18:
       unix-user = '1000'
       realname = 'Your Name'
       seat = 'Seat1'
       session-type = 
       active = TRUE
       x11-display = ':0'
       x11-display-device = '/dev/tty2'
       display-device = '/dev/tty1'
       remote-host-name = 
       is-local = TRUE
       on-since = '2011-11-16T12:01:50.104764Z'
       login-session-id = '7'

```

### No display manager

Se non si usa un [Display Manager](/index.php/Display_Manager_(Italiano) "Display Manager (Italiano)"), ma si avvia X con `startx`, o da `/etc/inittab` e si nota che consolekit non è avviato (il comando `ck-list-sessions` mostrerà `active = FALSE`), sarà necessario usare il metodo: "[Bash_profile](/index.php/Start_X_at_Boot_(Italiano)#bash_profile "Start X at Boot (Italiano)")".

Vedere [xinitrc](/index.php/Xinitrc_(Italiano) "Xinitrc (Italiano)") per ulteriori informazioni.

## Usare dbus per operazioni di sospensione/spegnimento/riavvio ecc

*   spegnimento:

 `dbus-send --system --print-reply --dest="org.freedesktop.ConsoleKit" /org/freedesktop/ConsoleKit/Manager org.freedesktop.ConsoleKit.Manager.Stop` 

*   riavvio:

 `dbus-send --system --print-reply --dest="org.freedesktop.ConsoleKit" /org/freedesktop/ConsoleKit/Manager org.freedesktop.ConsoleKit.Manager.Restart` 

*   sospensione:

 `dbus-send --system --print-reply --dest="org.freedesktop.UPower" /org/freedesktop/UPower org.freedesktop.UPower.Suspend` 

*   ibernazione (sospensione su disco):

 `dbus-send --system --print-reply --dest="org.freedesktop.UPower" /org/freedesktop/UPower org.freedesktop.UPower.Hibernate` 

Questo metodo da per scontato che l'utente abbia i permessi di policy kit. Il gruppo di default per questa funzionalità è "wheel". Per cambiare ciò, editare `/etc/polkit-1/localauthority.conf.d/50-localauthority.conf`

**Nota:** L'utilizzo di dbus per sospensione e ibernazione richiede [upower](https://www.archlinux.org/packages/?name=upower).

## Ulteriori risorse

*   [ck-launch-session, Compiz, e mounting con Thunar/udisks](https://bbs.archlinux.org/viewtopic.php?id=116853)