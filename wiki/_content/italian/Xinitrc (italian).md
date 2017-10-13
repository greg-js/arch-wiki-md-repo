Articoli correlati

*   [Display Manager (Italiano)](/index.php/Display_Manager_(Italiano) "Display Manager (Italiano)")
*   [Start X at Login (Italiano)](/index.php/Start_X_at_Login_(Italiano) "Start X at Login (Italiano)")
*   [Xorg (Italiano)](/index.php/Xorg_(Italiano) "Xorg (Italiano)")
*   [xprofile](/index.php/Xprofile "Xprofile")

Il file `~/.xinitrc` è uno shell script letto da `xinit` e `startx`. Viene tipicamente utilizzato per eseguire i [window manager](/index.php/Window_manager_(Italiano) "Window manager (Italiano)") e altri programmi all'avvio di X, ad esempio demoni e configurazioni delle variabili d'ambiente. Il programma `xinit` viene utilizzato per avviare l'[X Window System](/index.php/Xorg_(Italiano) "Xorg (Italiano)") e funziona come un primo programma client su sistemi che non possono avviare direttamente X da `/etc/init`, o in ambienti che usano vari window manager.

Una delle funzioni principali di `~/.xinitrc` è quello di dettare quale client per il sistema X Window sarà invocato da `/usr/bin/startx` e/o il programma `/usr/bin/xinit` *a utente singolo*. Ci sono molte altre configurazioni e comandi che possono essere aggiunti a `~/.xinitrc` al fine di personalizzare ulteriormente il proprio sistema.

## Contents

*   [1 Per iniziare](#Per_iniziare)
    *   [1.1 Effettuare la scelta fra i DE/WM](#Effettuare_la_scelta_fra_i_DE.2FWM)
    *   [1.2 Preservare la sessione](#Preservare_la_sessione)
*   [2 File d'esempio](#File_d.27esempio)
*   [3 Configurazione del file](#Configurazione_del_file)
    *   [3.1 Dalla riga di comando](#Dalla_riga_di_comando)
    *   [3.2 All'avvio](#All.27avvio)

## Per iniziare

`/etc/skel/` contiene i file e le directory necessari a fornire valori predefiniti per gli account appena creati. (Il nome *skel* è derivato dalla parola *skeleton*, perché i file contenuti costituiscono la struttura di base per le home directory degli utenti.) Il pacchetto [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit) provvederà a salvare in `/etc/skel` uno `.xinitrc` di esempio.

**Note:** `~/.xinitrc` è un cosiddetto "dot" (.) file. Nei sistemi *nix, i file che sono preceduti da un punto (.) sono "nascosti" e non compaiono con un normale comando `ls`, di solito allo scopo di tenere ordinate le directory. I file nascosti possono essere visualizzati con `ls -a`. Il suffisso "rc" significa *Run Commands* e indica semplicemente che è un file di configurazione. Dal momento che controlla il modo in cui un programma viene eseguito, può inoltre (anche se storicamente inesatto) essere interpretato come "Run Control".

Copiare il file d'esempio `/etc/skel/.xinitrc` nella home directory:

```
$ cp /etc/skel/.xinitrc ~

```

Quindi editare `~/.xinitrc` e decommentare la riga corrispondente al proprio [ambiente desktop](/index.php/Desktop_environment_(Italiano) "Desktop environment (Italiano)"). Per esempio, se si utilizza [Xterm](/index.php/Xterm "Xterm"), sarà simile a questo:

```
#!/bin/sh
#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)

if [ -d /etc/X11/xinit/xinitrc.d ]; then
  for f in /etc/X11/xinit/xinitrc.d/*; do
    [ -x "$f" ] && . "$f"
  done
  unset f
fi

# exec gnome-session
# exec startkde
# exec startxfce4
# exec wmaker
# exec icewm
# exec blackbox
# exec fluxbox
# exec openbox-session
# ...or the Window Manager of your choice
exec xterm
```

**Nota:** Assicurarsi di aver decommentato solo *una* riga `exec` in `~/.xinitrc`.

Dopo aver editato `.xinitrc` si è pronti a lanciare X. Avviarlo da utente *normale, non-root* con:

```
$ startx
$ xinit
$ xinit -- :1

```

**Nota:** `xinit` non può avviare sessioni multiple. Per questo può essere necessario l'uso di `-- :<session_no>`. In pratica questo è necessario se si ha già un'altra sessione di X aperta sul proprio sistema.

Il [DE](/index.php/Desktop_environment_(Italiano) "Desktop environment (Italiano)") o [WM](/index.php/Window_manager_(Italiano) "Window manager (Italiano)") scelto dovrebbe essersi avviato. È possibile provare la tastiera e la sua configurazione. Provare a spostare il mouse intorno per verificarne il funzionamento.

### Effettuare la scelta fra i DE/WM

Se non si usa un [display manager](/index.php/Display_manager_(Italiano) "Display manager (Italiano)") e non si vuole usarne uno, `~/.xinitrc` è di fondamentale importanza. Questo è un esempio di `xinitrc` pronto per lanciare sessioni diversi in base agli argomenti che gli vengono forniti sulla riga di comando.

```
#!/bin/sh
#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)

if [ -d /etc/X11/xinit/xinitrc.d ]; then
  for f in /etc/X11/xinit/xinitrc.d/*; do
    [ -x "$f" ] && . "$f"
  done
  unset f
fi

# XFCE in questo caso è il default
case $1 in
    gnome) exec gnome-session;;
    kde) exec startkde;;
    xfce);;
    *) exec startxfce4;;
esac

```

Ora, `~/.xinitrc` può essere invocato in questo modo.

```
$ xinit
$ xinit gnome
$ xinit kde
$ xinit xfce -- :1

```

### Preservare la sessione

X deve essere avviato nella stessa tty in cui viene effettuato il login per preservare la sessione di `logind`. Questo aspetto è gestito di default da `/etc/X11/xinit/xserverrc`. Vedere anche [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") per i relativi problemi

## File d'esempio

Quello che segue è un semplice file `~/.xinitrc` d'esempio, compresi alcuni programmi in avvio automatico:

```
~/.xinitrc

```

```
#!/bin/sh

if [ -d /etc/X11/xinit/xinitrc.d ]; then
  for f in /etc/X11/xinit/xinitrc.d/*; do
    [ -x "$f" ] && . "$f"
  done
  unset f
fi

xrdb -merge ~/.Xresources         # aggiorna x resources db

xscreensaver -no-splash &         # avvia il demone di xscreensaver
xsetroot -cursor_name left_ptr &  # setta il cursore di X
sh ~/.fehbg &                     # setta lo sfondo con feh

exec openbox-session              # avvia il window manager
```

Anteporre `exec` è raccomandato in quanto sostituisce il processo corrente con il gestore, in tal modo nessun processo viene forkato in background.

## Configurazione del file

Quando non viene utilizzato un display manager, è importante ricordare che la vita della sessione di X inizia e finisce con lo script `.xinitrc`. Ciò significa che una volta terminato lo script, X termina indipendentemente dai programmi che stanno ancora girando (compreso il gestore delle finestre). È importante perciò che la chiusura del gestore delle finestre e di X coincidano. Ciò può essere facilmente realizzato lanciando il gestore finestre come ultimo programma nello script.

Si noti che nel primo esempio di cui sopra, programmi come `cairo-compmgr`, `xscreensaver`, `xsetroot` e `sh` vengono eseguiti in background (con aggiunto il suffisso `&`). Altrimenti, lo script potrebbe fermarsi e attendere che ogni programma e demone termini prima di eseguire `openbox-session`. Notare inotre che `openbox-session` non è in background. Questo garantisce che lo script non si chiuderà prima di openbox stesso.

Nelle sezioni seguenti verrà spiegato come configurare `~/.xinitrc` per De e WM multipli.

### Dalla riga di comando

Se si dispone di un `~/.xinitrc` funzionante, ma si desidera provare altri WM/DE, è possibile farlo mediante l'esecuzione di `xinit` seguito dal percorso del window manager:

```
xinit /full/path/to/window-manager

```

Si noti che il percorso completo è **richiesto**. Opzionalmente, è possibile passare delle opzioni al server X con l'aggiunta di `--`, ad es.:

```
xinit /usr/bin/enlightenment -- -br +bs -dpi 96

```

Il file `~/.xinitrc` seguente, mostra come avviare un particolare window manager con un argomento:

```
~/.xinitrc

```

```
#!/bin/sh
#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)

if [ -d /etc/X11/xinit/xinitrc.d ]; then
  for f in /etc/X11/xinit/xinitrc.d/*; do
    [ -x "$f" ] && . "$f"
  done
  unset f
fi

if [[ $1 == "fluxbox" ]]
then
  exec startfluxbox
elif [[ $1 == "spectrwm" ]]
then
  exec spectrwm
else
  echo "Choose a window manager"
fi

```

Utilizzando questo esempio è possibile avviare fluxbox o spectrwm con il comando `xinit fluxbox` o `xinit spectrwm`.

### All'avvio

Vedere [Avviare X al Login](/index.php/Start_X_at_Login_(Italiano) "Start X at Login (Italiano)")