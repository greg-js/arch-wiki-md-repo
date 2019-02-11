[acpid](http://acpid.sourceforge.net/) è un demone flessibile ed estensibile per la consegna degli eventi ACPI. Il demone resta in ascolto su /proc/acpi/event e appena si verifica un evento, esegue dei programmi per gestirlo. Questi eventi sono attivati ​​da particolari azioni, quali:

*   Premendo il pulsante di accensione
*   Premendo il tasto Sleep/Suspend
*   Chiusura di un coperchio notebook
*   Collegando un adattatore di alimentazione CA ad un notebook

**Note:**

*   [ambienti desktop](/index.php/Desktop_environment_(Italiano) "Desktop environment (Italiano)"), come [GNOME](/index.php/GNOME "GNOME"), [systemd](/index.php/Systemd#Power_management "Systemd") login manager e alcuni demoni di[gestione dei tasti extra](/index.php/Extra_keyboard_keys "Extra keyboard keys") potrebbero implementare degli schemi per la gestione degli eventi propri, in maniera indipendente da acpid. Eseguendo più di un sistema alla volta, potrebbe provocare comportamenti inaspettati, come una sospensione doppia, due volte in fila dopo una pressione del pulsante per la sospensione. Si dovrebbe essere consapevoli di ciò, e abilitare solamente i gestori desiderati.
*   Siccome di default lo script installato da acpid, **/etc/acpi/handler.sh**, sovrascriverà la funzionalità alla pressione del pulsante di accensione del tuo ambiente desktop, probabilmente vorrai cambiare la routine di acpid, per evitare di spegnere il sistema alla pressione inavvertita del pulsante di accensione.(leggi le istruzioni sotto).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Configurazione alternativa](#Configurazione_alternativa)
*   [3 Tips & Tricks](#Tips_&_Tricks)
    *   [3.1 Esempi di eventi](#Esempi_di_eventi)
    *   [3.2 Abilitare il controllo del volume](#Abilitare_il_controllo_del_volume)
    *   [3.3 Abilitare il controllo della retroilluminazione](#Abilitare_il_controllo_della_retroilluminazione)
    *   [3.4 Abilitare/disattivare Wi-fi](#Abilitare/disattivare_Wi-fi)
    *   [3.5 Spegnere l'alimentazione del monitor di un laptop](#Spegnere_l'alimentazione_del_monitor_di_un_laptop)
    *   [3.6 Ottenere il nome utente del display corrente](#Ottenere_il_nome_utente_del_display_corrente)
    *   [3.7 Tasti di scelta rapida ACPI](#Tasti_di_scelta_rapida_ACPI)
*   [4 Altre risorse](#Altre_risorse)

## Installazione

[Installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") il pacchetto [acpid](https://www.archlinux.org/packages/?name=acpid) reperibile nei [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

Per avere acpid avviato automaticamente, [abilitare](/index.php/Systemd#Using_units "Systemd") `acpid.service`.

## Configurazione

[acpid](https://www.archlinux.org/packages/?name=acpid) viene fornito con una serie di azioni predefinite per gli eventi già attivati​​, come quello che dovrebbe accadere quando si preme il pulsante di accensione sulla vostra macchina. Per impostazione predefinita, queste azioni sono definite in `/etc/acpi/handler.sh`, e vengono eseguite dopo qualsiasi evento ACPI rilevato (come determinato da `/etc/acpi/events/anything`).

Quello che segue è un breve esempio di una azione. In questo caso, quando si preme il pulsante Sleep, acpid esegue il comando `echo -n mem >/sys/power/state` che dovrebbe posizionare il computer allo stato *sleep* (sospensione):

```
button/sleep)
    case "$2" in
        SLPB) echo -n mem >/sys/power/state ;;
	 *)    logger "ACPI action undefined: $2" ;;
    esac
    ;;

```

Sfortunatamente non tutti i computer leggono gli eventi ACPI alla stessa maniera. Ad esempio il pulsante Sleep può essere identificato su alcune macchine come *SLPB* ed in altre come *SBTN*.

Per determinare come i pulsanti o tasti di scelta rapida `Fn` vengono riconosciuti, eseguire il seguente comando da terminale come utente root:

```
# tail -f /var/log/messages.log

```

Ora premere il pulsante di accensione e/o il pulsante Sleep (es. `Fn+Esc`) sulla propria macchina. Il risultato dovrebbe essere simile a questo:

```
logger: ACPI action undefined: PBTN
logger: ACPI action undefined: SBTN

```

Se non dovesse funzionare lanciare il comando:

```
# acpi_listen

```

Premendo il tasto di accensione e dovreste ottenere un output simile:

```
power/button PBTN 00000000 00000b31

```

L'output di `acpi_listen` viene inviato allo script `/etc/acpi/handler.sh` come parametro $1, $2 , $3 & $4 . Esempio:

```
$1 power/button
$2 PBTN
$3 00000000
$4 00000b31

```

Come si può notare, il pulsante Sleep in uscita, nell'esempio, è stato riconosciuto come *SBTN*, piuttosto che con l'etichetta *SLPB*, come specificato nel file `/etc/acpi/handler.sh`. Al fine di far funzionare correttamente il tasto Sleep su questa macchina, avremmo bisogno di sostituire *SLPB)* con *SBTN)*.

Utilizzando queste informazioni come base, si può facilmente personalizzare il file `/etc/acpi/handler.sh` in modo da eseguire una varietà di comandi a seconda di quale evento viene attivato. Si veda la sezione [Tips & Tricks](#Tips_&_Tricks) per altri comandi di uso comune.

### Configurazione alternativa

Per impostazione predefinita, tutti gli eventi ACPI sono passati allo script `/etc/acpi/handler.sh`. Ciò è dovuto al set di regole delineate nel file `/etc/acpi/events/anything`:

```
# Pass all events to our one handler script
event=.*
action=/etc/acpi/handler.sh %e

```

Anche se questo metodo funziona correttamente, alcuni utenti potrebbero preferire definire le regole per gli eventi e le azioni in un proprio script personalizzato. Di seguito un esempio di come utilizzare un singolo file per un evento ed uno script per l'azione corrispondente:

Come utente root, creare il seguente file:

 `/etc/acpi/events/sleep-button` 
```
event=button sleep.*
action=/etc/acpi/actions/sleep-button.sh "%e"

```

Ora creare il seguente file:

 `/etc/acpi/actions/sleep-button.sh` 
```
 #!/bin/sh
 case "$2" in
     SLPB) echo -n mem >/sys/power/state ;;
     *)    logger "ACPI action undefined: $2" ;;
 esac

```

Infine rendere lo script eseguibile:

```
# chmod +x /etc/acpi/actions/sleep-button.sh

```

Utilizzando questo metodo, è facile creare un numero illimitato di singoli script di eventi/azioni.

## Tips & Tricks

**Tip:** Alcune azioni, descritte qua, come spegnimento/accensione del Wi-Fi e controllo della retroilluminazione, potrebbero già essere gestite direttamente dal driver. Consultare quindi la documentazione del modulo del kernel corrispondente, se necessario.

### Esempi di eventi

Di seguito vengono mostrati degli esempi di eventi utilizzando lo script `/etc/acpi/handler.sh` esistente. Questi esempi dovrebbero essere modificati in modo da applicare le specifiche ambientali, ad esempio cambiando i nomi delle variabili evento interpretati da `acpi_listen`.

Bloccare lo schermo con `xscreensaver` quando viene chiuso il portatile:

```
button/lid)
    case $3 in
        close)
            # Il comando di blocco deve essere eseguito come l'utente che possiede il processo xscreensaver e non come root.
            # Vedere: man xscreensaver-command. $xs avrà il valore dell'utente proprietario del processo, se esiste.

            xs=$(ps up $(pidof xscreensaver) | awk '/xscreensaver/ {print $1}')
            if test $xs; then su $xs -c "xscreensaver-command -lock"; fi
            ;;

```

Sospendere il sistema e bloccare lo schermo utilizzando `slimlock` alla chiusura del coperchio:

```
button/lid)
    case $3 in
        close)
            #echo "LID switched!">/dev/tty5 
             /usr/bin/pm-suspend &
             DISPLAY=:0.0 su -c - username /usr/bin/slimlock
             ;;

```

Per impostare la luminosità dello schermo del portatile quando è collegato all'alimentatore o meno (potrebbe essere necessario modificare i valori, si controlli `/sys/class/backlight/acpi_video0/max_brightness`)::

```
ac_adapter)
    case "$2" in
        AC*|AD*)
            case "$4" in
                00000000)
                    echo -n 50 > /sys/class/backlight/acpi_video0/brightness
                    ;;
                00000001)
                    echo -n 100 > /sys/class/backlight/acpi_video0/brightness
                    ;;
            esac

```

### Abilitare il controllo del volume

Scopri l'evento identificativo dei pulsanti del volume (vedi sopra) e sostituiscilo nei files qua sotto. Adesso creiamo un paio di script per controllare il volume (supponendo una scheda audio [ALSA](/index.php/ALSA "ALSA")):

 `/etc/acpi/actions/volume_up.sh` 
```
  #!/bin/bash
  /usr/bin/amixer set Master 5%+

```
 `/etc/acpi/actions/volume_down.sh` 
```
  #!/bin/bash
  /usr/bin/amixer set Master 5%-

```

e linkiamo questi ultimi ai nuovi eventi acpi:

 `/etc/acpi/events/volume_up` 
```
  event=button[ /]volumeup
  action=/etc/acpi/actions/volume_up.sh

```
 `/etc/acpi/events/volume_down` 
```
  event=button[ /]volumedown
  action=/etc/acpi/actions/volume_down.sh

```

e creiamo pure un altro evento per attivare/disattivare l'audio:

 `/etc/acpi/events/volume_mute` 
```
  event=button[ /]volumemute
  action=/usr/bin/amixer set Master toggle

```

### Abilitare il controllo della retroilluminazione

In maniera simile al controllo del volume, tramite acpid è possibile gestire la luminosità dello schermo. Per raggiungere ciò, si devono scrivere alcuni handler, come di seguito:

 `/etc/acpi/handlers/bl` 
```
#!/bin/sh
bl_dev=/sys/class/backlight/acpi_video0
step=1

case $1 in
  -) echo $((`cat $bl_dev/brightness` - $step)) >$bl_dev/brightness;;
  +) echo $((`cat $bl_dev/brightness` + $step)) >$bl_dev/brightness;;
esac

```

e ancora, collegare i tasti agli eventi ACPI:

 `/etc/acpi/events/bl_d` 
```
event=video/brightnessdown
action=/etc/acpi/handlers/bl -

```
 `/etc/acpi/events/bl_u` 
```
event=video/brightnessup
action=/etc/acpi/handlers/bl +

```

### Abilitare/disattivare Wi-fi

Si può anche creare un semplice handler che attiverà/disattiverà il wireless alla pressione del pulsante WLAN. Esempio dell'evento:

 `/etc/acpi/events/wlan` 
```
event=button/wlan
action=/etc/acpi/handlers/wlan

```

e il suo handler:

 `/etc/acpi/handlers/wlan` 
```
#!/bin/sh
rf=/sys/class/rfkill/rfkill0

case `cat $rf/state` in
  0) echo 1 >$rf/state;;
  1) echo 0 >$rf/state;;
esac

```

### Spegnere l'alimentazione del monitor di un laptop

Aggiungendo queste stringhe al fondo del file `/etc/acpi/actions/lm_lid.sh` o alla sezione *button/lid* di `/etc/acpi/handler.sh`, si ottiene lo spegnimento della reto-illuminazione del display LCD quando il coperchio è chiuso, e lo riaccende quando il coperchio si riapre.

```
case $(cat /proc/acpi/button/lid/LID0/state | awk '{print $2}') in
    closed) XAUTHORITY=$(ps -C xinit -f --no-header | sed -n 's/.*-auth //; s/ -[^ ].*//; p') xset -display :0 dpms force off ;;
    open)   XAUTHORITY=$(ps -C xinit -f --no-header | sed -n 's/.*-auth //; s/ -[^ ].*//; p') xset -display :0 dpms force on  ;;
esac

```

Se volete aumentare o diminuire la luminosità o qualcosa dipendente da X, è necessario specificare il display X così come il file *MIT magic cookie* (via XAUTHORITY). L'ultima parte è una credenziale di sicurezza che fornisce la lettura e scrittura al server X, il display e tutti i dispositivi di input.

Con alcune combinazioni di [Xorg](/index.php/Xorg_(Italiano) "Xorg (Italiano)") e hardware problematico, `xset dpms force off` genera un display bianco lasciando la retroilluminazione attiva. Questo può essere risolto utilizzando [vbetool](https://www.archlinux.org/packages/?name=vbetool) dai [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)"). Modificare la sezione LCD come segue:

```
case $(cat /proc/acpi/button/lid/LID0/state | awk '{print $2}') in
    closed) vbetool dpms off ;;
    open)   vbetool dpms on  ;;
esac

```

Se il monitor sembra solo spegnersi brevemente prima di essere ri-alimentato, molto probabilmente ciò è dovuto al fatto che la gestione dell'alimentazione fornita con XScreenSaver va in conflitto con le impostazioni manuali di *DPMS*.

### Ottenere il nome utente del display corrente

Ottenere il nome utente del display corrente

È possibile utilizzare la funzione `getuser` per acquisire la visualizzazione dell'utente corrente:

```
getuser ()
    {
     export DISPLAY=`echo $DISPLAY | cut -c -2`
     user=`who | grep " $DISPLAY" | awk '{print $1}' | tail -n1`
     export XAUTHORITY=/home/$user/.Xauthority
     eval $1=$user
    }

```

Questa funzione può essere utilizzata, ad esempio, quando si preme il pulsante di accensione e si vuole che [KDE](/index.php/KDE_(Italiano) "KDE (Italiano)") effettui lo spegnimento correttamente:

```
button/power)
    case "$2" in
        PBTN)
            getuser "$user"
            echo $user > /dev/tty5
            su $user -c "dcop ksmserver ksmserver logout 0 2 0"
            ;;
          *) logger "ACPI action undefined $2" ;;
    esac
    ;;

```

Nei sistemi che utilizzano systemd, i login in x non sono più necessariamente visualizzati con `who`, quindi la funzione `getuser` qua sopra non funziona. Un'alternativa è usare `loginctl` per ottenere l'informazione richiesta, ad esempio usando [xuserrun](https://github.com/rephorm/xuserrun).

### Tasti di scelta rapida ACPI

E' possibile o modificare a mano `/etc/acpi/handler.sh`, per reagire agli eventi ACPI, oppure lo si può far puntare ad un altro script (i.e. `/etc/acpi/hotkeys.sh`)

Nella sezione:

```
case "$1" in

```

Aggiungi le seguenti righe:

```
hkey)
	case "$4" in
		00000b31)
		echo "PreviousButton pressed!"
		exailectl p
		;;
	00000b32)
		echo "NextButton pressed!"
		exailectl n
		;;
	00000b33)
		echo "Play/PauseButton pressed!"
		exailectl pp
		echo "executed.."
		;;
	00000b30)
		echo "StopButton pressed!"
		exailectl s
		;;
	*)
		echo "Hotkey Else: $4"
		;;
	esac
	;;

```

I valori '00000b31' (ecc. ecc.) sono ottenuti tramite acpi_listen.

Esiste anche lo script exailectl, un breve script shell che ho creato per controllare il music player Exaile. Siccome ACPID è avviato da utente root, si dovrà utilizzare

```
sudo -u (username) exaile

```

per esempio, altrimenti non verrà rilevato il programma a livello utente e ne verrà creato un altro.

## Altre risorse

*   [acpid homepage](http://acpid.sourceforge.net/)