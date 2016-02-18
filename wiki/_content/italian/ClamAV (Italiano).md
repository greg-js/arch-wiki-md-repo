[Clam AntiVirus](http://www.clamav.net) è un anti-virus open source (GPL) oer UNIX. Fornisce una serie di utility che includono un demone multi-thread flessibile e scalabile, un'interfaccia da linea di comando ed uno strumento avanzato per l'aggiornamento automatico del database con le definizioni dei virus. Poiché ClamAV viene principalmente usato su file/mail servers Windows esso riconosce sopratutto virus e malware per Windows.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
*   [3 Aggiornamento Database](#Aggiornamento_Database)
*   [4 Installazione Server](#Installazione_Server)
*   [5 Scansione dei Virus](#Scansione_dei_Virus)
*   [6 Risoluzione dei problemi](#Risoluzione_dei_problemi)

## Installazione

Installalo con pacman digitando:

```
# pacman -S clamav

```

## Configurazione

Se hai intenzione di usare ClamAV come demone o come semplice analizzatore di file bisogna commentare la linea che contiene la parola *Example*, di solito si trova all'inizio nel file `/etc/clamav/freshclam.conf`. (probabilmente bisogna fare lo stesso nel file `clamd.conf` che si trova nella stessa directory) ed aggiornare il database dei virus e dei malware.

## Aggiornamento Database

Per aggiornare il database bisogna che il demone sia avviato:

```
# /etc/rc.d/clamav start

```

Dopo aggiorna la definizione dei virus con:

```
# freshclam

```

I file del database sono salvati in:

```
/var/lib/clamav/daily.cvd
/var/lib/clamav/main.cvd

```

## Installazione Server

Per eseguirlo come un server modifica `/etc/clamav/clamd.conf` e `/etc/clamav/freshclam.conf` e commenta il flag *Example*. In `/etc/conf.d/clamav` cambia l'opzione start da "no" a "yes".

```
# change these to "yes" to start
START_FRESHCLAM="yes"
START_CLAMD="yes"

```

*   Per avviare clamav al boot del sistema modifica `/etc/rc.conf` e aggiungi clamav alla linea DAEMONS=(...).

## Scansione dei Virus

`clamscan` può essere usato per eseguire la scansione di alcuni file, della directory home, o di un intero sistema:

```
$ clamscan myfile
$ clamscan -r -i /home
$ clamscan -r -i --exclude-dir=^/sys\|^/proc\|^/dev /

```

Se desideri che `clamscan` rimuova i file infetti usa nel comando l'opzione `--remove`.

## Risoluzione dei problemi

Se dopo aver eseguito {Codeline|freshclam}} ottieni i seguenti messaggi:

```
WARNING: Clamd was NOT notified: Can't connect to clamd through 
/var/lib/clamav/clamd.sock connect(): No such file or directory

```

Aggiungi un sock file per clamav:

```
# touch /var/lib/clamav/clamd.sock
# chown clamav:clamav /var/lib/clamav/clamd.sock

```

Dopo, modifica /etc/clamav/clamd.conf

```
commenta questa linea: #LocalSocket /var/lib/clamav/clamd.sock

```

Salva il file e riavvia il demone (/etc/rc.d/clamav stop; /etc/rc.d/clamav start)

Se quando avvii il demone ottieni il seguente errore:

```
LibClamAV Error: cli_loaddb(): No supported database files found
in /var/lib/clamav ERROR: Not supported data format

```

Esegui freshclam come root:

```
# freshclam -v

```