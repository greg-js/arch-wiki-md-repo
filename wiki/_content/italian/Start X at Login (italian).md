Questo articolo spiega come avviare automaticamente il [Server X](/index.php/Xorg_(Italiano) "Xorg (Italiano)") dopo il login in un terminale virtuale attraverso l'utilizzo del comando *startx*, il cui comportamento può essere modificato come riportato nella pagina relativa a [xinitrc](/index.php/Xinitrc_(Italiano) "Xinitrc (Italiano)"), ad esempio per scegliere quale [window manager](/index.php/Window_manager_(Italiano) "Window manager (Italiano)") avviare.

In alternativa, è possibile utilizzare un [display manager](/index.php/Display_manager_(Italiano) "Display manager (Italiano)") per avviare automaticamente X e fornire un login grafico.

## Contents

*   [1 File di configurazione delle shell](#File_di_configurazione_delle_shell)
*   [2 Utilizzando systemd](#Utilizzando_systemd)
*   [3 Suggerimenti](#Suggerimenti)
*   [4 Riferimenti](#Riferimenti)

## File di configurazione delle shell

**Nota:** Il comando di cui sotto avvia X nella stessa tty dal quale si effettua il login, condizione necessaria per mantenere la sessione di login.

Se si usa [Bash](/index.php/Bash_(Italiano) "Bash (Italiano)"), aggiungere il comando al proprio `~/.bash_profile`. Se il file non esiste lo si copi da `/etc/skel/.bash_profile`. Se si usa [Zsh](/index.php/Zsh "Zsh") aggiungere il comando al file `~/.zlogin` o `~/.zprofile`.

```
[[ -z $DISPLAY && $XDG_VTNR -eq 1 ]] && exec startx

```

**Nota:**

*   È possibile sostituire `-eq 1` con `-le 3` (per i vt dal 1 al 3) se si desidera avvalersi del login grafico su più di un terminale virtuale.
*   X deve essere sempre avviato dalla stessa tty dove si è effettuato il login, in modo che la sessione di logind venga mantenuta. Questo comportamento è garantito dal file `/etc/X11/xinit/xserverrc`.
*   `xinit` è generalmente più veloce di `startx`, ma è necessario specificare manualmente dei parametri aggiuntivi come `-nolisten tcp`.

Se si utilizza la [Fish](/index.php/Fish "Fish") shell, è necessario aggiungere quanto segue in fondo al proprio `~/.config/fish/config.fish`

```
# start X at login
if status --is-login
    if test -z "$DISPLAY" -a $XDG_VTNR -eq 1
        exec startx -- -keeptty
    end
end

```

**Nota:** `startx` richiede il parametro `-keeptty` quando si utilizza fish. Si veda [questo](https://github.com/fish-shell/fish-shell/issues/1772) bug report.

## Utilizzando systemd

Si crei un file .service (ad esempio `/etc/systemd/system/xinit@.service`):

```
[Unit]
Description=startx for user %i
After=x@vt7.service systemd-user-sessions.service
Wants=x@vt7.service
Conflicts=getty@tty7.service

[Service]
User=%i
TTYPath=/dev/tty7
PAMName=login
Environment=DISPLAY=:0
WorkingDirectory=/home/%I
Nice=0
ExecStart=/bin/bash -l -c "cd; startx >/dev/null 2>&1"

[Install]
WantedBy=graphical.target

```

Assicurarsi che `~.xinitrc` esista e sia configurato in modo corretto.

Si abiliti ed [attivi](/index.php/Systemd_(Italiano)#Usare_le_unit.C3.A0 "Systemd (Italiano)") quindi il servizio.

**Suggerimento:** Rimuovere `>/dev/null 2>&1` per effettuare il debug.

## Suggerimenti

*   Il metodo appena presentato può essere combinato con [il login automatico da console virtuale](/index.php/Automatic_login_to_virtual_console_(Italiano) "Automatic login to virtual console (Italiano)"). Quando si utilizza questo metodo sarà necessario modificare il servizio di systemd per l'autologin in modo che DBus venga avviato prima della lettura di `~/.xinitrc`, per permettere così l'avvio di PulseAudio. (si veda [BBS#155416](https://bbs.archlinux.org/viewtopic.php?id=155416))

*   Se si desidera mantenere il login su TTY quando la sessione di X viene terminata, si rimuova `exec`.

*   Per redirigere l'output della sessione di X su un file, si crei un [alias](/index.php/Bash_(Italiano)#Alias "Bash (Italiano)"):

	 `alias startx='startx & > ~/.xlog'` 

**Nota:** la ridirezione dello *stderr* (`startx &>`) crea problemi all'avvio di X da utente normale. Si veda a tal proposito [Xorg#Rootless Xorg (v1.16)](/index.php/Xorg#Rootless_Xorg_.28v1.16.29 "Xorg").

## Riferimenti

[Avvio di X dopo l'autologin](http://unix.stackexchange.com/questions/62722/start-x-after-automatic-login)