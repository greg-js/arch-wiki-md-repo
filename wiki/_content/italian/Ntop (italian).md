## Contents

*   [1 Introduzione](#Introduzione)
*   [2 Installazione e configurazione](#Installazione_e_configurazione)
*   [3 Trucchi e suggerimenti](#Trucchi_e_suggerimenti)
    *   [3.1 Accedere all'interfaccia web di ntop](#Accedere_all.27interfaccia_web_di_ntop)
*   [4 Risoluzione dei problemi](#Risoluzione_dei_problemi)

## Introduzione

Ntop è un analizzatore del traffico di rete basato su [libcap](http://www.tcpdump.org/), che offre statistiche sul traffico accessibili tramite una comoda interfaccia web, come avviene in RMON. La [homepage](http://www.ntop.org/overview.html) è disponibile per dare uno sguardo alle funzionalità del programma.

## Installazione e configurazione

*   Ntop è disponibile nel repository extra:

```
# pacman -S ntop

```

*   Prima di eseguire ntop, è necessario impostare la password d'amministratore:

```
# ntop --set-admin-password=*password*

```

*   Avviare quindi il demone:

```
# /etc/rc.d/ntop start

```

*   Se si ritiene necessario, è possibile aggiungere ntop all'array DAEMONS in [/etc/rc.conf](/index.php/Rc.conf_(Italiano) "Rc.conf (Italiano)") per avviare automaticamente il demone di ntop all'avvio.

## Trucchi e suggerimenti

### Accedere all'interfaccia web di ntop

*   Per accedere all'interfaccia web di ntop, basta inserire `[http://127.0.0.1:3000/](http://127.0.0.1:3000/)` nella barra indirizzi di un qualsiasi web browser. Per effettuare modifiche alla configurazione del web server, è necessario fornire username (predefinito = *admin*) e password.

## Risoluzione dei problemi

```
  **ERROR** RRD: Disabled - unable to create base directory (err 13, /var/lib/ntop/rrd)

```

La cartella `/var/lib/ntop/rrd` potrebbe non esistere. Crearla

```
# mkdir /var/lib/ntop/rrd

```

e assicurarsi che questa appartenga all'utente `nobody`.

```
# chown nobody /var/lib/ntop/rrd

```