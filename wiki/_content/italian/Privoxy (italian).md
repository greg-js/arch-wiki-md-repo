Articoli correlati

*   [Tor](/index.php/Tor "Tor")
*   [Polipo](/index.php/Polipo "Polipo")

Ci potrebbero essere delle situazioni in cui vorresti avere un completo anonimato mentre usi Internet. Un modo per averlo è usare Tor e Privoxy.

## Contents

*   [1 Introduzione](#Introduzione)
*   [2 Installazione e setup](#Installazione_e_setup)
*   [3 Ad Blocking con Privoxy](#Ad_Blocking_con_Privoxy)
*   [4 Uso](#Uso)
*   [5 Risoluzione dei problemi](#Risoluzione_dei_problemi)
*   [6 Link Esterni](#Link_Esterni)

## Introduzione

**Privoxy** è un proxy di filtraggio per il protocollo HTTP, usato frequentemente in combinazione con [Tor](/index.php/Tor "Tor"). Privoxy è un proxy web con capacità di filtraggio avanzate per proteggere la privacy, filtrare il contenuto di pagine web, gestire i cookies, controllare gli accessi e rimuovere annunci, banner, pop-up ed altro. Supporta sia sistemi a sé stanti sia network multiutenti.

L'uso di Privoxy è necessario perché i browser fanno trapelare le richieste DNS quando usano direttamente un proxy SOCKS, e ciò non è buono per mantenere l'anonimato.

## Installazione e setup

Come utente root installare il pacchetto `privoxy` da l repository `[community]`.

```
# pacman -S privoxy

```

Prima di tutto, andare su [http://whatsmyip.net/](http://whatsmyip.net/) e prendere nota del proprio indirizzo IP. Modificare il file `/etc/privoxy/config` e aggiungere questa riga alla fine (sii sicuro di inserire il . alla fine e mantieni il proprietario del file e il gruppo "privoxy"):

```
forward-socks5 / localhost:9050 .

```

Assicurarsi che `/etc/hosts` sia configurato correttamente. Di default in Arch, `hostname` ha il nome `localhost` ma è necessario che abbia il nome usato in `/etc/rc.conf`.

Es. nel file `rc.conf` di Arch di default HOSTNAME="myhost", così in `/etc/hosts` dovrebbe essere:

```
#<ip-address>   <hostname.domain.org>   <hostname>
127.0.0.1       myhost.localdomain      myhost localhost

```

Se è necessario rendere disponibile privoxy ad altri computer nella propria rete, è sufficiente aggiungere:

```
listen-address [SERVER-IP]:[PORT]

```

Per esempio:

```
listen-address 192.168.1.1:8118

```

## Ad Blocking con Privoxy

Usare un'estensione per il blocco degli ad in un browser web può aumentare il tempo di caricamento delle pagine. Inoltre, estensioni come AdBlock Plus non sono supportate da tutti i browser. Un'alternativa ragionevole è installare un ad blocking di sistema impostando un indirizzo proxy nel proprio browser preferito.

Una volta che Privoxy è stato installato, scaricare e installare un importatore di easylist di AdBlock Plus da [AUR](/index.php/AUR "AUR") (es. [privoxy-blocklist](https://aur.archlinux.org/packages/privoxy-blocklist/)). Altrimenti si può usare [AUR Helper](/index.php/AUR_Helper "AUR Helper") per farlo.

## Uso

Fare partire il server Privoxy:

```
# rc.d start privoxy

```

Aggiungre Privoxy alla serie di `DAEMONS` in `/etc/rc.conf`

```
DAEMONS=(... privoxy ...)

```

Configurare il proprio programma per usare Privoxy. L'indirizzo predefinito è:

```
localhost:8118

```

Per Firefox andare su:

```
Preferences > Advanced > Network > Settings

```

Per Chromium è possibile usare:

```
$ chromium --proxy-server="localhost:8118"

```

## Risoluzione dei problemi

Se appaiono errori quando si accede a `/var/log/privoxy/`, l'utente può aggiungere questo dopo `/bin/bash` in `/etc/rc.d/privoxy` e poi riavviare Privoxy.

```
if [ ! -d /var/log/privoxy ] then
   mkdir /var/log/privoxy
   touch /var/log/privoxy/errorfile
   touch /var/log/privoxy/logfile
   chown -R privoxy:adm /var/log/privoxy
fi

```

## Link Esterni

*   [Sito ufficiale (en)](http://www.privoxy.org/)
*   [Blocking ads with Privoxy](http://thestegemans.com/archives/2011/06/03/blocking_ads_on_arch_linux_with_privoxy/) di Mike Stegeman (en)