Prima di tutto assicurarsi che il modulo "bottone" venga caricato (controllare l'output di lsmod). Se non lo è, caricarlo manualmente

```
# modprobe button

```

oppure aggiungere al proprio [/etc/rc.conf MODULES array](/index.php/Rc.conf#Hardware "Rc.conf") in modo che sia caricato automaticamente all'avvio del sistema.

## Contents

*   [1 Prima soluzione](#Prima_soluzione)
    *   [1.1 KDE 3](#KDE_3)
    *   [1.2 KDE 4](#KDE_4)
    *   [1.3 XFCE](#XFCE)
*   [2 Seconda soluzione](#Seconda_soluzione)
*   [3 TODO](#TODO)

## Prima soluzione

Se si vuole spegnere il sistema semplicemente premendo il pulsante di accensione, effettuare quanto segue:

1.  Installare il pacchetto [acpid](/index.php/Acpid "Acpid").
2.  Aggiungere acpid alla stringa DAEMONS in [rc.conf](/index.php/Rc.conf "Rc.conf").
3.  Creare un file in _/etc/acpi/events/_ chiamandolo _power_ con il seguente contenuto:

```
# /etc/acpi/events/power
# Questo viene richiamato quando l'utente preme il pulsante di accensione

event=button/power (PWR.||PBTN)
action=/sbin/poweroff

```

Per essere in grado di provarlo, accertarsi che il demone acpid sia avviato

Avviare il demone acpid:

```
# /etc/rc.d/acpid start

```

Da ora in poi, premendo il pulsante di accensione (non per qualche secondo) dovrebbe arrestarsi correttamente il sistema. Se l'**ibernazione** è configurata e funzionante si consiglia di cambiare l'ultima riga con:

```
action=/usr/sbin/hibernate

```

**Warning:** Non aggiungere il demone acpid alla stringa DAEMON in "/etc/rc.conf" se hal è ancora presente. Si otterrà un messaggio di errore all'avvio quando il computer tenta di ricaricare il demone acpi già in esecuzione.

Se si utilizza un WM più sofisticato, si dovrebbe usare il suo sistema di richiamata d'arresto, in modo che possa salvare la sessione, ecc.

### KDE 3

Modificare l'azione (in `/etc/acpi/events/power`) a:

```
action=/opt/kde/bin/dcop --all-users --all-sessions ksmserver ksmserver logout 0 2 0

```

### KDE 4

A partire da KDE 4.4, è comunque possibile utilizzare dcop come mostrato sopra.

In alternativa, è possibile utilizzare `PowerDevil`:

1.  Cancellare (o commentare) `/etc/acpi/events/power`.
2.  Aprire le Impostazioni di sistema.
3.  Andare su Avanzate>> Power Management.
4.  Selezionare "Modificare Profili" e scegliere il profilo corrente. (In KDE 4.4, il profilo di default è "risparmio energia".)
5.  Selezionare "Shutdown", come azione per "Quando si preme il pulsante di accensione".
6.  Premere Applica.

**Note:** 1) Con dcop e PowerDevil, il pulsante di accensione funziona _solo_ quando KDE è in esecuzione. Inoltre, KDE ha bisogno di essere avviato da KDM (probabilmente funziona anche quando lanciato da GDM). Non funziona se si avvia KDE con il comando "startx".

**Note:** 2) La configurazione di PowerDevil è _per utente_. Ripetere questi passaggi per ognuno di loro.

**Todo:** Aggiungere operazioni di configurazione multi-utente.

### XFCE

Per **XFCE4.4** cambiare la riga di azione per:

```
_action=echo POWEROFF | /usr/lib/xfce4/xfsm-shutdown-helper_

```

Per **XFCE4.8** cambiare la riga di azione per:

```
_action=echo POWEROFF | /usr/lib/xfce4/session/xfsm-shutdown-helper_

```

_**Note:** Per una soluzione più robusta (in caso di frequenti crash del WM o su un PC utilizzato per lo sviluppo o test del software...), si dovrebbe dare un'occhiata a "/usr/src/linux/Documentation/sysrq.txt", che è una funzionalità del kernel utilizzata per qualsiasi lavoro di salvataggio._

## Seconda soluzione

(In caso la prima non funzioni)

1.  Installare acpid.
2.  Aggiungere acpid alla stringa DAEMONS in rc.conf.
3.  Editare /etc/acpi/handler.sh (da root):

```
...
case "$1" in
   button/power)
       #echo "PowerButton pressed!">/dev/tty5
       case "$2" in
           PWRF)   logger "PowerButton pressed: $2" 
		    /sbin/poweroff;;
           *)      logger "ACPI action undefined: $2" ;;
       esac
       ;;
...

```

Per essere in grado di provarlo, accertarsi che il demone acpid sia avviato.

Avviare il demone acpid:

```
# /etc/rc.d/acpid start

```

## TODO

Aggiungere una tecnica che funzioni indipendentemente dal VM (Gnome/KDE/xcfe/openbox/ecc). Copiare lo script `/etc/acpi/events/power` da Ubuntu