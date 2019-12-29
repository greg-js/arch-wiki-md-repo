Un [demone](https://it.wikipedia.org/wiki/Demone_(informatica)) è un programma che viene eseguito in background, in attesa che si verifichino determinati eventi e offrendo servizi. Un buon esempio è un server web in attesa di fornire una pagina richiesta o un server ssh in attesa di qualcuno che esegua il login. Anche se queste sono applicazioni particolari con ampie funzionalità, ci sono demoni il cui lavoro non è così visibile come il demone che scrive messaggi in un file di log (ad esempio, syslog, metalog), o il demone che controlla l'accuratezza del tempo del sistema (ad esempio,[ntpd](/index.php/Network_Time_Protocol_daemon_(Italiano) "Network Time Protocol daemon (Italiano)")).

**Note:** Il termine demone è talvolta usato per una classe di programmi che vengono avviati al boot, ma non hanno alcun processo che rimanga in memoria. Sono chiamati demoni semplicemente perché usano la stessa struttura di avvio e arresto (ad esempio i servizi di systemd di tipo oneshot) usata per avviare i demoni tradizionali. Per esempio, i files per il servizio `alsa-store` e `alsa-restore` forniscono il supporto per una configurazione persistente ma non avviano ulteriori processi in background a richiesta del servizio o per risposta ad eventi.

Dalla prospettiva di un utente la distinzione solitamente è insignificante fino a quando l'utente stesso non tenta di cercare il "demone" in una lista dei processi.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Systemd](#Systemd)
    *   [1.1 Avvio al boot](#Avvio_al_boot)
    *   [1.2 Avvio manuale](#Avvio_manuale)
*   [2 Lista dei demoni](#Lista_dei_demoni)
*   [3 Vedi anche](#Vedi_anche)

## Systemd

### Avvio al boot

Una installazione di default di Arch Linux lascia pochissimi servizi (o demoni) attivi al boot. E' possibile aggiungere o rimuovere servizi da avviare al boot con:

```
# systemctl enable <name>

```

o

```
# systemctl disable <name>

```

I servizi stessi contengono tutte le necessarie informazioni, cosicché non c'è bisogno di configurarli manualmente.

I files dei Servizi sono immagazzinati in `/{etc,usr/lib,run}/systemd/system`. Si può visualizzare la lista dei servizi disponibili nel proprio sistema assieme al loro attuale stato, con:

```
$ systemctl list-unit-files

```

Per vedere una lista delle unità attive (alcune delle quali possono essere demoni, tra le altre cose), digitare:

```
$ systemctl list-units

```

Per vedere tutte quelle disponibili, aggiungere `--all` alla fine del comando.

### Avvio manuale

Per avviare o fermare servizi in fase di esecuzione, si può rimpiazzare `enable`/`disable` con `start`/`stop` nei precedenti comandi.

Si può approfondire alla sezione [systemctl del wiki di systemd](/index.php/Systemd_(Italiano)#Uso_base_di_systemctl "Systemd (Italiano)").

## Lista dei demoni

Vedere [Daemons List](/index.php/Daemons_List "Daemons List") per una lista dei demoni con il nome del servizio e il vecchio script rc.d.

## Vedi anche

*   [systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)")