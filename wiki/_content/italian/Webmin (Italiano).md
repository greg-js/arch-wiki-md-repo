Webmin viene eseguito come servizio. Tramite [webmin](https://aur.archlinux.org/packages/webmin/), è possibile amministrare gli altri servizi e server configurati, sia dal server stesso che da remoto.

Dal sito ufficiale di [Webmin](http://www.webmin.com/)

	_Webmin is a web-based interface for system administration for Unix. Using any modern web browser, you can setup user accounts, Apache, DNS, file sharing and much more. Webmin removes the need to manually edit Unix configuration files like /etc/passwd, and lets you manage a system from the console or remotely._

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
*   [3 Avvio](#Avvio)
*   [4 Uso](#Uso)

## Installazione

[Installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") il pacchetto [webmin](https://aur.archlinux.org/packages/webmin/) e come sua dipendenza installare anche il pacchetto [perl-net-ssleay](https://www.archlinux.org/packages/?name=perl-net-ssleay), sarà necessario per abilitare l’accesso tramite [https](https://en.wikipedia.org/wiki/https "wikipedia:https").

## Configurazione

Per permettere l'accesso a Webmin da un PC remoto, modificare il file `/etc/webmin/miniserv.conf` ed inserire l'indirizzo della propria rete.

**Nota:** L'indirizzo di loopback 127.0.0.1 sarà presente di default.

```
allow=127.0.0.1 192.168.1.0

```

Nel precedente esempio tutti i computer appartenenti alla rete 192.168.1.0 potranno accedere a Webmin.

## Avvio

Per avviare Webmin eseguire

```
# rc.d start webmin

```

Inserire il [demone](/index.php/Daemon_(Italiano) "Daemon (Italiano)") `webmin` all'interno dell'array `DAEMONS` nel file `/etc/rc.conf` per farlo avviare durante il boot.

```
DAEMONS=(.. vsftpd **webmin** ...)

```

## Uso

In un browser web, inserire l'indirizzo https del server seguito dalla porta 10000(impostata di default) per accedere a Webmin. Ad esempio:

https://192.168.1.1:10000 -oppure- https://myserver.example.net:10000

Sarà necessario inserire la password di root del server che esegue Webmin per poter accedere all'interfaccia di Webmin ed amministrare il server.