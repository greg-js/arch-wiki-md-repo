Articoli correlati

*   [Wireless Setup](/index.php/Wireless_Setup "Wireless Setup")

[ConnMan](http://connman.net/) è un gestore delle connessioni alternativo a [NetworkManager](/index.php/NetworkManager_(Italiano) "NetworkManager (Italiano)") e [Wicd](/index.php/Wicd_(Italiano) "Wicd (Italiano)"), creato da Intel e il progetto Moblin per l'utilizzo con dispositivi embedded.

## Installazione

Installare [connman](https://www.archlinux.org/packages/?name=connman) prelevandolo da [AUR](/index.php/AUR "AUR").

## Configurazione

Per utilizzare ConnMan come un regolare utente, aggiungere le seguenti linee al file `/etc/dbus-1/system.d/connman.conf` sotto il blocco che definisce le policy user="root".

```
  <policy group="network">
       <allow send_destination="org.moblin.connman"/>
       <allow send_interface="org.moblin.connman.Agent"/>
       <allow send_interface="org.moblin.connman.Counter"/>
   </policy>

```

## Utilizzo di ConnMan

Sfortunatamente, al momento di stilare questo articolo, ConnMan non dispone di un applet per poter lavorare. Per poter controllare ConnMan si possono utilizzare gli script di inclusi nel pacchetto.

Avete bisogno di python e python-dbus per poterli eseguire.

Avviare connmanm, spostetevi in un terminale e aprite la cartella di test presente nel pacchetto di origine.

Per avere un elenco delle reti disponibili eseguire:

```
  ./test-connman services

```

Si vedrà qualcosa di simile a questo (non i risultati reali):

```
 MyWiFi         { wifi_8945762986259dfgs9hsd9bgs9e_managed_wep }
 Another Wifi         { wifi_8asd356w3asdgdfgs9hsd9bgs9e_managed_wep }

```

Il codice dopo il SSID è importante. Questo identifica la rete a cui si desidera connettersi. Per collegarsi a questa rete in primo luogo, inserire la password con:

```
   ./test-connman passphrase wifi_8945762986259dfgs9hsd9bgs9e_managed_wep PASSWORDHERE

```

E connettersi con:

```
   ./test-connman connect wifi_8945762986259dfgs9hsd9bgs9e_managed_wep

```

Ora si dovrebbe essere collegati alla rete. Potete controllare con `ifconfig`.