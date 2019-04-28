<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 TTY (Teletype) Console 1-6](#TTY_(Teletype)_Console_1-6)
*   [2 X.org](#X.org)
    *   [2.1 KDM](#KDM)
    *   [2.2 KDE4](#KDE4)
        *   [2.2.1 Metodo alternativo](#Metodo_alternativo)
    *   [2.3 GDM](#GDM)
    *   [2.4 SLiM](#SLiM)

## TTY (Teletype) Console 1-6

Per attivare il NumLock durante il normale avvio dalle console 1-6 (tty1 -> tty6), aggiungere la seguente linea al file `/etc/rc.local`:

```
for tty in /dev/tty?; do /usr/bin/setleds -D +num < "$tty"; done

```

Se si verificano comportamenti strani (il led del NumLock è acceso, ma all'effettivo viene interpretato come se non lo fosse), probabilmente c'è un conflitto tra `setleds` ed Xserver. Limitare il ciclo `for` solamente alla console impostata nel file `/etc/inittab`. Ad esempio, per le prime 6 console (quelle di default):

```
for tty in /dev/tty{1..6}; do ...

```

## X.org

Se si usa `startx` per avviare la sessione X, basterà semplicemente installare il pacchetto [numlockx](https://www.archlinux.org/packages/?name=numlockx) ed aggiungerlo al proprio `~/.xinitrc`.

Installare [numlockx](https://www.archlinux.org/packages/?name=numlockx):

```
# pacman -S numlockx

```

Aggiungerlo al file `~/.xinitrc` prima del comando `exec`:

```
#!/bin/sh
#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)
#

numlockx &

exec your_window_manager

```

### KDM

Se si usa KDM come login manager, aggiungere:

```
numlockx on

```

al proprio `/usr/share/config/kdm/Xsetup`, oppure al file `/opt/kde/share/config/kdm/Xsetup` se si usa KDM3.

**Nota:** questo file risiede al di fuori dall'area protetta di Pacman, quindi potrebbe essere sovrascritto in caso di aggiornamento senza avvertimenti o senza la creazione di un file `.pacnew`. Se questo comportamento non è gradito aggiungere la seguente linea al proprio `/etc/pacman.conf` (omettere lo slash all'inizio del percorso):
```
NoUpgrade = usr/share/config/kdm/Xsetup

```

### KDE4

Andare in "Impostazioni di Sistema", selezionare "Dispositivi di immissione" nella sezione "Tastiera" nel tab "Hardware" è possibile impostare il comportamento del NumLock.

#### Metodo alternativo

In alternativa è possibile aggiungere uno script alla propria cartella `~/.kde4/Autostart`:

```
$ nano ~/.kde4/Autostart/numlockx

```

Aggiungere le seguenti linee:

```
#!/bin/sh
numlockx on

```

Rendere il file eseguibile:

```
$ chmod +x ~/.kde4/Autostart/numlockx

```

### GDM

Assicurarsi di aver installato [numlockx](https://www.archlinux.org/packages/?name=numlockx) (dal reopository extra). Nel caso si usi GDM è possibile aggiungere il seguente codice al file `/etc/gdm/Init/Default`:

```
if [ -x /usr/bin/numlockx ]; then
      /usr/bin/numlockx on
fi

```

### SLiM

Nel file `/etc/slim.conf` individuare la linea:

```
#numlock             on

```

e de commentarla rimuovendo il simbolo `#`.