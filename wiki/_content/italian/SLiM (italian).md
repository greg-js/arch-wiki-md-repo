Articoli correlati

*   [Display Manager (Italiano)](/index.php/Display_Manager_(Italiano) "Display Manager (Italiano)")

[SLiM](http://slim.berlios.de/) è l'acronimo di Simple Login Manager (semplice gestore di login). SLiM è un login manager semplice, leggero e facilmente configurabile, adatto per essere usato su piattaforme con poche risorse. SLiM è molto utile anche a chi vuole un login manager che non dipenda da [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)") o [KDE](/index.php/KDE_(Italiano) "KDE (Italiano)"), ed è perfetto per chi usa [Xfce](/index.php/Xfce_(Italiano) "Xfce (Italiano)"), [openbox](/index.php/Openbox_(Italiano) "Openbox (Italiano)"), [fluxbox](/index.php/Fluxbox_(Italiano) "Fluxbox (Italiano)") ecc.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Abilitare SLiM](#Abilitare_SLiM)
    *   [2.2 Singolo ambiente desktop](#Singolo_ambiente_desktop)
    *   [2.3 Autologin](#Autologin)
    *   [2.4 Zsh](#Zsh)
    *   [2.5 Ambienti multipli](#Ambienti_multipli)
    *   [2.6 Temi](#Temi)
        *   [2.6.1 Setup schermo](#Setup_schermo)
*   [3 Altre opzioni](#Altre_opzioni)
    *   [3.1 Cambiare il cursore](#Cambiare_il_cursore)
    *   [3.2 Condividere lo sfondo tra desktop e Slim](#Condividere_lo_sfondo_tra_desktop_e_Slim)
    *   [3.3 Spegnere, Riavviare, Sospendere, Uscire, Aprire un terminale da SLiM](#Spegnere.2C_Riavviare.2C_Sospendere.2C_Uscire.2C_Aprire_un_terminale_da_SLiM)
    *   [3.4 Errore di SLiM eseguito come demone](#Errore_di_SLiM_eseguito_come_demone)
    *   [3.5 Errore allo spegnimento con Splashy](#Errore_allo_spegnimento_con_Splashy)
    *   [3.6 L'icona per lo spegnimento non funziona](#L.27icona_per_lo_spegnimento_non_funziona)
    *   [3.7 Informazioni di login](#Informazioni_di_login)
    *   [3.8 Comandi di login personalizzati](#Comandi_di_login_personalizzati)
    *   [3.9 SLiM e Gnome Keyring](#SLiM_e_Gnome_Keyring)
    *   [3.10 Settare DPI di SLiM](#Settare_DPI_di_SLiM)
    *   [3.11 Usare un tema casuale](#Usare_un_tema_casuale)
    *   [3.12 Spostare l'intera sessione su un altra console](#Spostare_l.27intera_sessione_su_un_altra_console)
    *   [3.13 Montare /home al login](#Montare_.2Fhome_al_login)
*   [4 Tutte le opzioni di SLiM](#Tutte_le_opzioni_di_SLiM)
*   [5 Disinstallazione](#Disinstallazione)
*   [6 Vedere anche](#Vedere_anche)

## Installazione

[slim](https://www.archlinux.org/packages/?name=slim) è contenuti nei [Repository Ufficiali](/index.php/Repository_Ufficiali "Repository Ufficiali"), si installa quindi facilmente con [Pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)").

## Configurazione

### Abilitare SLiM

**Nota:** Ora fa uso di `systemd-logind` quindi è fondamentale usare [systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)") come sistema di init.

Per avviare SLiM al boot, [abilitare](/index.php/Systemd_(Italiano) "Systemd (Italiano)") il servizio `slim`.

Si noti che dall'avvento di systemd il file `/etc/inittab` non esiste più, quindi l'unico modo per avviare slim è usare:

```
# systemctl enable slim

```

Vedere [systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)") per ottenere più informazioni.

### Singolo ambiente desktop

Per configurare SLiM per caricare un particolare ambiente, semplicemente editare il file `~/.[xinitrc](/index.php/Xinitrc_(Italiano) "Xinitrc (Italiano)")`, in modo che sia simile al seguente:

```
#!/bin/sh

#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)
#

exec [session-command]
```

Sostituire *[session-command]* con il comando appropriato. Per esempio:

```
exec awesome
exec dwm
exec startfluxbox
exec fvwm2
exec gnome-session
exec openbox-session
exec startkde
exec startlxde
exec startxfce4
exec enlightenment_start

```

Per i dettagli su come avviare il proprio ambiente, fare riferimento alla relativa pagina wiki.

Il file appena creato va reso eseguibile dando, da root:

```
# chmod -x ~/.xinitrc

```

### Autologin

Per avere un autologin con SLiM di un utente predefinito, senza che venga richiesta la password, le seguenti righe di `/etc/slim.conf`:

```
# default_user	               simone

```

Decommentare la riga e cambiare "simone" con l'utente che si a cui si vuole applicare l'autologin.

```
# auto_login	               no

```

Decommentare la riga e cambiare "no" in "yes" per abilitare l'autologin.

### Zsh

**Nota:** Se non si sa cosa sia Zsh, non si necessita di questo paragrafo.

Il comando di login di default non inizializza correttamente questo ambiente ([fonte](http://www.edsel.nu/2010/06/04/slim-simple-login-manager-on-freebsd/)). Cambiare quindi la riga `login_cmd` in:

```
#login_cmd           exec /bin/sh - ~/.xinitrc %session
login_cmd           exec /bin/zsh -l ~/.xinitrc %session

```

### Ambienti multipli

Se si ha il bisogno di caricare più ambienti desktop, SLiM può essere configurato in modo da poter scegliere quale.

Inserire un case statement simile a questo nel vostro file `~/.xinitrc` ed editare la sessions variable in `/etc/slim.conf`. Si potrà scegliere la sessione al login premendo F1. Tenere in considerazione che questa caratteristica è sperimentale.

```
# La seguente variabile definisce la sessione che partirà se l'utente non sceglierà espicitatamente una sessione
# Source: [http://svn.berlios.de/svnroot/repos/slim/trunk/xinitrc.sample](http://svn.berlios.de/svnroot/repos/slim/trunk/xinitrc.sample)

DEFAULT_SESSION=kde

case $1 in
kde)
	exec startkde
	;;
xfce4)
	exec startxfce4
	;;
icewm)
	icewmbg &
	icewmtray &
	exec icewm
	;;
wmaker)
	exec wmaker
	;;
blackbox)
	exec blackbox
	;;
*)
	exec $DEFAULT_SESSION
	;;
esac
```

**Nota:** nella versione 1.3.5, SLiM sembra non essere in grado di preservare la sessione di logind. Quindi è necessario aggiungere la variabile *DEFAULT_SESSION* in `~/.xinitrc`.

### Temi

Installare il pacchetto [slim-themes](https://www.archlinux.org/packages/?name=slim-themes):

```
# pacman -S slim-themes archlinux-themes-slim

```

Il pacchetto [archlinux-themes-slim](https://www.archlinux.org/packages/?name=archlinux-themes-slim) contiene numerosi temi ([slimthemes.png](http://imageshack.us/photo/my-images/27/slimthemes.png/)). I temi saranno estratti in `/usr/share/slim/themes`. Modificare la linea `current_theme` in `/etc/slim.conf` :

```
#current_theme       default
current_theme       archlinux-simplyblack

```

Per un anteprima:

```
$ slim -p /usr/share/slim/themes/<theme name>

```

Per chiudere, scrivere 'exit' nella riga di login e premere Invio. Molti temi per SLiM sono disponibili su [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)").

#### Setup schermo

È possibile personalizzare il tema di SLiM in `/usr/share/slim/themes/<your-theme>/slim.theme` modificando questi valori in percentuale: (il riquadro è 450 pixels per 250)

```
input_panel_x		50%
input_panel_y		50%

```

in valori espressi in pixels:

```
# Questi valori servono a impostare il pannello *archlinux-simplyblack* nel centro di uno schermo 1440x900
input_panel_x		495
input_panle_y		325

```

```
# Questi valori servono a impostare il pannello *archlinux-retro* nel centro di un

```

o schermo 1680x1050

```
input_panel_x          615
input_panle_y          400

```

## Altre opzioni

Alcune cose che potrebbe essere carino provare.

### Cambiare il cursore

Se si vuole cambiare il cursore di default del server grafico X è possibile installare da [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)") il pacchetto [slim-cursor](https://aur.archlinux.org/packages/slim-cursor/).

Ad installazione ultimata, editare il file `/etc/slim.conf` e decommentare la seguente riga:

```
cursor		left_ptr

```

Questo farà apparire un cursore "normale". La configurazione è data da `xsetroot -cursor_name`. È possibile cercare i nomi dei possibili cursori [qui](http://cvsweb.xfree86.org/cvsweb/*checkout*/xc/lib/X11/cursorfont.h?rev=HEAD&content-type=text/plain) o in `/usr/share/icons/<your-cursor-theme>/cursors/`.

### Condividere lo sfondo tra desktop e Slim

Un modo semplice per condividere il wallpaper tra il desktop e Slim è creare un link simbolico dal file del wallpaper del desktop al tema di default di Slim:

```
#  mv /usr/share/slim/themes/default/background.jpg /usr/share/slim/themes/default/background.old.jpg
# ln -s /path/to/mywallpaper.jpg /usr/share/slim/themes/default/background.jpg

```

### Spegnere, Riavviare, Sospendere, Uscire, Aprire un terminale da SLiM

Si può spegnere, riavviare, sospendere, uscire o aprire un terminale dalla schermata di accesso di SLiM. Per farlo, inserire il valore appropriato nel campo username, e la password di root nel campo password:

*   Per aprire un il terminale, inserire **console** come username (xterm di defaults, altri vanno installati separatamente... editare <tt>/etc/slim.conf</tt> per cambiare le preferenze riguardanti il terminale)
*   Per spegnere il pc, inserire **halt** come username
*   Per riavviare il pc, inserire **reboot** come username
*   Per uscire al bash, inserire **exit** come username
*   Per sospendere il pc, inserire **suspend** come username (La sospensione è disabilitata per default, editare `/etc/slim.conf` come utente root per decommentare la linea `suspend_cmd` e, se necessario, modificare il comando suspend (per esempio cambiare `/usr/sbin/suspend` in `sudo /usr/sbin/pm-suspend`))

### Errore di SLiM eseguito come demone

Se si avvia SLiM come demone da `/etc/rc.conf` e si ha un errore all'avvio potrebbe essere un problema del file di *lock*. SLiM crea un file *lock* ogni qual volta viene lanciato in `/var/lock/`. È quindi fondamentale che tale directory esista, in caso contrario crearla ora:

```
# mkdir /var/lock/ 

```

### Errore allo spegnimento con Splashy

Se si usa Splashy in accoppiata con SLiM, qualche volta risulterà impossibile spegnere o riavviare il proprio computer. Controllare che `/etc/slim.conf` e `/etc/splash.conf` siano correttamente settati su tty7 così: `DEFAULT_TTY=7` e `xserver_arguments vt07`.

### L'icona per lo spegnimento non funziona

Se l'icona in questione non dovesse funzionare potrebbe essere un problema di permessi. Per avviare questa icona con i privilegi di root, modificare `/etc/slim.conf` come segue

```
sessionstart_cmd	/percorso/dell/immagine &

```

### Informazioni di login

Di default SLiM non stampa alcun log. Per abilitare i log modificare così `/etc/slim.conf`:

```
 sessionstart_cmd    /usr/bin/sessreg -a -l $DISPLAY %user
 sessionstop_cmd     /usr/bin/sessreg -d -l $DISPLAY %user

```

### Comandi di login personalizzati

È possibile usare sessionstart_cmd/sessionstop_cmd in `/etc/slim.conf` per avere specifiche informazioni, come ad esempio sessione, user, tema...:

```
 sessionstop_cmd /usr/bin/logger -i -t ASKAPACHE "(sessionstop_cmd: u:%user s:%session t:%theme)"
 sessionstart_cmd /usr/bin/logger -i -t ASKAPACHE "(sessionstart_cmd: u:%user s:%session t:%theme)"

```

O se si vuole un suono all'avvio di SLiM (il programma beep va installato a parte):

```
 sessionstart_cmd /usr/bin/beep -f 659 -l 460 -n -f 784 -l 340 -n -f 659 -l 230 -n -f 659 -l 110

```

### SLiM e Gnome Keyring

**Note:** slim 1.3.5-1 ships with `/etc/pam.d/slim` preconfigured to unlock keyring upon login. Users no longer need to modify the file.

**Warning:** If auto login is enabled, the GNOME keyring will not be unlocked automatically on login. This will cause dependent applications, such as Chrome/Chromium and NetworkManager, to misbehave (see [https://bbs.archlinux.org/viewtopic.php?id=167579](https://bbs.archlinux.org/viewtopic.php?id=167579)).

See [GNOME Keyring#Use Without GNOME, and without a display manager](/index.php/GNOME_Keyring#Use_Without_GNOME.2C_and_without_a_display_manager "GNOME Keyring") to use GNOME Keyring in a custom session.

### Settare DPI di SLiM

Di solito ci pensa X ad impostare i DPI, volendo però si può impostare una preferenza su SLiM. Settare i DPI con *-dpi 96* in `/etc/X11/xinit/xserverrc` non funzionerà su SLiM. Si può però modificare questa riga di `slim.conf` da:

```
 xserver_arguments   -nolisten tcp vt07 

```

a

```
 xserver_arguments   -nolisten tcp vt07 -dpi 96

```

### Usare un tema casuale

La variabile `current_theme` supporta l'utilizzo della virgola. Scrivere quindi separati da una virgola i temi che si intende usare. SLiM ne sceglierà uno a caso ogni volta.

### Spostare l'intera sessione su un altra console

Se si avesse commentato alcuni terminali, come ad esempio 3, 4, 5 e 6, sarebbe possibile usarli come schermi. (Si potrebbe usare più display e un solo terminale) Per spostare il server grafico è necessario modifcare `/etc/slim.conf` . L'unica linea da modificare è:

```
xserver_arguments -nolisten tcp vt07

```

Cambiare semplicemente vt07 in vt03 (per avere X sulla tty3). Non deve esserci agetty attivo.

### Montare /home al login

Si può usare [pam_mount](/index.php/Pam_mount#Slim "Pam mount").

## Tutte le opzioni di SLiM

Qui c'è una lista di tutte le opzioni di configurazione di SLiM con tutte le variabili necessarie.

**Nota:** welcome_msg permette 2 variabili **%host** e **%domain**
sessionstart_cmd permette **%user** e può anche ammettere in sessionstop_cmd
login_cmd allows **%session** e **%theme**

| Option Name | Default Value |
| default_path | `/bin:/usr/bin:/usr/local/bin` |
| default_xserver | `/usr/bin/X` |
| xserver_arguments | `vt07 -auth /var/run/slim.auth` |
| numlock |
| daemon | `yes` |
| xauth_path | `/usr/bin/xauth` |
| login_cmd | `exec /bin/bash -login ~/.xinitrc %session` |
| halt_cmd | `/sbin/shutdown -h now` |
| reboot_cmd | `/sbin/shutdown -r now` |
| suspend_cmd |
| sessionstart_cmd |
| sessionstop_cmd |
| console_cmd | `/usr/bin/xterm -C -fg white -bg black +sb -g %dx%d+%d+%d -fn %dx%d -T` |
| screenshot_cmd | `import -window root /slim.png` |
| welcome_msg | `Welcome to %host` |
| session_msg | `Session:` |
| default_user |
| focus_password | `no` |
| auto_login | `no` |
| current_theme | `default` |
| lockfile | `/var/run/slim.lock` |
| logfile | `/var/log/slim.log` |
| authfile | `/var/run/slim.auth` |
| shutdown_msg | `The system is halting...` |
| reboot_msg | `The system is rebooting...` |
| sessions | `wmaker,blackbox,icewm` |
| sessiondir |
| hidecursor | `false` |
| input_panel_x | `50%` |
| input_panel_y | `40%` |
| input_name_x | `200` |
| input_name_y | `154` |
| input_pass_x | `-1` |
| input_pass_y | `-1` |
| input_font | `Verdana:size=11` |
| input_color | `#000000` |
| input_cursor_height | `20` |
| input_maxlength_name | `20` |
| input_maxlength_passwd | `20` |
| input_shadow_xoffset | `0` |
| input_shadow_yoffset | `0` |
| input_shadow_color | `#FFFFFF` |
| welcome_font | `Verdana:size=14` |
| welcome_color | `#FFFFFF` |
| welcome_x | `-1` |
| welcome_y | `-1` |
| welcome_shadow_xoffset | `0` |
| welcome_shadow_yoffset | `0` |
| welcome_shadow_color | `#FFFFFF` |
| intro_msg |
| intro_font | `Verdana:size=14` |
| intro_color | `#FFFFFF` |
| intro_x | `-1` |
| intro_y | `-1` |
| background_style | `stretch` |
| background_color | `#CCCCCC` |
| username_font | `Verdana:size=12` |
| username_color | `#FFFFFF` |
| username_x | `-1` |
| username_y | `-1` |
| username_msg | `Please enter your username` |
| username_shadow_xoffset | `0` |
| username_shadow_yoffset | `0` |
| username_shadow_color | `#FFFFFF` |
| password_x | `-1` |
| password_y | `-1` |
| password_msg | `Please enter your password` |
| msg_color | `#FFFFFF` |
| msg_font | `Verdana:size=16:bold` |
| msg_x | `40` |
| msg_y | `40` |
| msg_shadow_xoffset | `0` |
| msg_shadow_yoffset | `0` |
| msg_shadow_color | `#FFFFFF` |
| session_color | `#FFFFFF` |
| session_font | `Verdana:size=16:bold` |
| session_x | `50%` |
| session_y | `90%` |
| session_shadow_xoffset | `0` |
| session_shadow_yoffset | `0` |
| session_shadow_color | `#FFFFFF` |

## Disinstallazione

Per rimuovere completamente SLiM dal proprio sistema:

 `# pacman -Rns slim` 

## Vedere anche

*   [Homepage di SLiM](http://slim.berlios.de/)
*   [Documentazione di SLiM](http://slim.berlios.de/manual.php)