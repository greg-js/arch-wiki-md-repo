Articoli correlati

*   [Network configuration (Italiano)](/index.php/Network_configuration_(Italiano) "Network configuration (Italiano)")
*   [Wireless Setup (Italiano)](/index.php/Wireless_Setup_(Italiano) "Wireless Setup (Italiano)")

[wpa_supplicant](http://hostap.epitest.fi/wpa_supplicant/) è un [Supplicant](https://en.wikipedia.org/wiki/Supplicant_(computer) WPA multipiattaforma con supporto a WEP, WPA e WPA2 ([IEEE 802.11i](https://en.wikipedia.org/wiki/IEEE_802.11i "wikipedia:IEEE 802.11i") / RSN (Robust Secure Network)) adatto all'uso con PC desktop, portatili e sistemi embedded. `wpa_supplicant` è il componente IEEE 802.1X/WPA utilizzato dai client, implementa la negoziazione della chiave con un WPA Authenticator, controlla il roaming e l'associazione / autenticazione del driver wireless.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Panoramica](#Panoramica)
*   [3 Connessione tramite wpa_cli](#Connessione_tramite_wpa_cli)
*   [4 Connessione tramite wpa_passphrase](#Connessione_tramite_wpa_passphrase)
*   [5 Utilizzo avanzato](#Utilizzo_avanzato)
    *   [5.1 Configurazione](#Configurazione)
    *   [5.2 Connessione](#Connessione)
        *   [5.2.1 Manuale](#Manuale)
        *   [5.2.2 All'avvio (systemd)](#All.27avvio_.28systemd.29)
    *   [5.3 Action script per wpa_cli](#Action_script_per_wpa_cli)
*   [6 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [6.1 Driver nl80211 non supportato su alcuni modelli](#Driver_nl80211_non_supportato_su_alcuni_modelli)
*   [7 Link utili](#Link_utili)

## Installazione

Si [installi](/index.php/Install "Install") il pacchetto [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant).

È inoltre possibile installare [wpa_supplicant_gui](https://aur.archlinux.org/packages/wpa_supplicant_gui/) che fornisce *wpa_gui*, un frontend grafico per *wpa_supplicant*.

## Panoramica

Affinchè *wpa_supplicant* possa connettersi ad una rete wireless, dovrà prima essere autenticato da un WPA authenticator attraverso l'inserimento delle credenziali corrette.

Una volta che l'associazione con l'access point è completa è possibile collegarsi alla rete ottenendo un indirizzo IP, manualmente tramite la suite [iproute2](/index.php/Core_utilities#ip "Core utilities") o tramite programmi appositi, come [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") o [dhcpcd](/index.php/Dhcpcd "Dhcpcd"), per l'assegnazione automatica di un indirizzo IP tramite DHCP. Si vedano anche gli articoli relativi ad interfacce [wireless](/index.php/Wireless_network_configuration#Systemd_with_wpa_supplicant_and_static_IP "Wireless network configuration") o [via cavo](/index.php/Configuring_Network_(Italiano)#Configurare_l.27indirizzo_IP "Configuring Network (Italiano)").

## Connessione tramite wpa_cli

Questo metodo consente di effettuare una scansione delle reti disponibili utilizzando *wpa_cli*, un tool a riga di comando che è in grado di configurare *wpa_supplicant* a runtime. Si veda [wpa_cli(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_cli.8) per ulteriori informazioni.

Per utilizzare *wpa_cli*, sarà necessario specificare un'interfaccia di controllo per *wpa_supplicant* e dotarla dei permessi per modificare il relativo file di configurazione.

Si crei quindi un file di configurazione minimale:

 `/etc/wpa_supplicant/esempio.conf` 
```
ctrl_interface=/run/wpa_supplicant
update_config=1
```

Si avvii *wpa_supplicant* come segue:

```
# wpa_supplicant -B -i interface -c /etc/wpa_supplicant/esempio.conf

```

**Suggerimento:** Per scoprire il nome della propria interfaccia di rete wireless, si esegua il comando `ip link`.

Si esegua:

```
# wpa_cli

```

Verrà visualizzato un prompt interattivo (`>`) che dispone di tab completion e descrizione dei comandi completati.

**Suggerimento:** Il percorso predefinito del socket di controllo è `/var/run/wpa_supplicant/`. È possibile impostare un percorso personalizzato tramite il parametro `-p`, in modo che corrisponda a quanto contenuto nel file di configurazione. Si può altresì specificare l'interfaccia da configurare con l'opzione `-i`. Se non specificata, *wpa_supplicant* sceglierà la prima interfaccia disponibile.

Si utilizzino i comandi `scan` e `scan_results` per vedere le reti disponibili:

```
> scan
OK
<3>CTRL-EVENT-SCAN-RESULTS
> scan_results
bssid / frequency / signal level / flags / ssid
00:00:00:00:00:00 2462 -49 [WPA2-PSK-CCMP][ESS] MIOSSID
11:11:11:11:11:11 2437 -64 [WPA2-PSK-CCMP][ESS] ALTROSSID

```

Per associarsi con `MIOSSID` si aggiunga la rete, si specifichino le credenziali e la si abiliti:

```
> add_network
0
> set_network 0 ssid "MIOSSID"
> set_network 0 psk "passphrase"
> enable_network 0
<2>CTRL-EVENT-CONNECTED - Connection to 00:00:00:00:00:00 completed (reauth) [id=0 id_str=]

```

Se il SSID a cui ci si connette non utilizza l'autenticazione tramite password sarà necessario configurare la rete come aperta, sostituendo il comando `set_network 0 psk "passphrase"` con `set_network 0 key_mgmt NONE`.

**Nota:**

*   Ogni rete viene identificata da un numero crescente: la prima avrà pertanto indice 0.
*   La [PSK](https://en.wikipedia.org/wiki/Pre-shared_key "wikipedia:Pre-shared key") viene ottenuta dalla stringa "passphrase" immessa sopra e compresa tra doppi apici, come mostrato dal comando [wpa_passphrase](#Connessione_tramite_wpa_passphrase). In ogni caso è possibile immettere la PSK direttamente passandola al comando `psk` *senza* raccoglierla tra doppi apici.

Si salvi infine la rete nel file di configurazione:

```
>save_config
OK

```

Una volta che l'assiociazione è stata effettuata, non resta che ottenere un indirizzo IP, come indicato nella sezione [#Panoramica](#Panoramica); ad esempio:

```
# dhcpcd *interfaccia*

```

## Connessione tramite wpa_passphrase

Questo metodo consente di collegarsi rapidamente ad una rete di cui si conosce già il SSID tramite *wpa_passphrase*, un tool a riga di comando che genera un file di configurazione minimale per *wpa_supplicant*.

Ad esempio:

 `$ wpa_passphrase MIOSSID passphrase` 
```
network={
    ssid="MIOSSID"
    #psk="passphrase"
    psk=59e0d07fa4c7741797a4e394f38a5c321e3bed51d54ad5fcbd3f84bc7415d73d
}
```

È quindi possibile associarsi alla rete tramite *wpa_passphrase* e *wpa_supplicant* in questo modo:

```
# wpa_supplicant -B -i *interfaccia* -c <(wpa_passphrase SSID passphrase)

```

**Nota:** A causa della sostituzione di processo, **non è possibile** eseguire il comando di cui sopra tramite [sudo](/index.php/Sudo_(Italiano) "Sudo (Italiano)"), bensì è necessario usare una shell di root. Si veda anche [Help:Reading#Regular user or root](/index.php/Help:Reading#Regular_user_or_root "Help:Reading").

**Suggerimento:**

*   Utilizzare i doppi apici se l'input contiene spazi. Ad esempio: `"secret passphrase"`.
*   Per scoprire il nome della propria interfaccia di rete wireless, si esegua il comando `ip link`.
*   Alcune passphrase particolarmente complesse potrebbero dover venire immesse scrivendole prima in un file: `wpa_passphrase MIOSSID < passphrase.txt`, o passando la stringa: `wpa_passphrase MIOSSID <<< "passphrase"`.

Infine, non resta che ottenere un indirizzo IP, come indicato nella sezione [#Panoramica](#Panoramica); ad esempio:

```
# dhcpcd *interfaccia*

```

## Utilizzo avanzato

Per reti di varia complessità, che utilizzino [EAP](https://en.wikipedia.org/wiki/Extensible_Authentication_Protocol "wikipedia:Extensible Authentication Protocol") o altro, è consigliabile utilizzare un file di configurazione personalizzato. Per una panoramica del file di configurazione completa di esempi, si veda [wpa_supplicant.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_supplicant.conf.5); per dettagli su tutte le opzioni di configurazione supportate si veda il file di configurazione d'esempio `/etc/wpa_supplicant/wpa_supplicant.conf`.

### Configurazione

Come già evidenziato nel paragrafo [#Connessione tramite wpa_passphrase](#Connessione_tramite_wpa_passphrase), è possibile generare un file di configurazione di base con:

```
# wpa_passphrase MIOSSID passphrase > /etc/wpa_supplicant/esempio.conf

```

Quanto sopra creerà un solo blocco `network`. Un file di configurazione con le opzioni più comuni potrebbe essere simile a questo:

 `/etc/wpa_supplicant/esempio.conf` 
```
ctrl_interface=DIR=/run/wpa_supplicant GROUP=wheel
update_config=1
fast_reauth=1
ap_scan=1
network={
    ssid="MIOSSID"
    #psk="passphrase"
    psk=59e0d07fa4c7741797a4e394f38a5c321e3bed51d54ad5fcbd3f84bc7415d73d
}
```

È possibile aggiungere ulteriori blocchi `network` manualmente o utilizzando *wpa_cli*, come mostrato al paragrafo [#Connessione tramite wpa_cli](#Connessione_tramite_wpa_cli). Per utilizzare quest'ultimo, sarà necessario impostare una interfaccia di controllo tramite l'opzione `ctrl_interface`. Specificare `GROUP=wheel` consente a tutti gli utenti membri di quel gruppo di utilizzare *wpa_cli*. Si aggiunga inoltre `update_config=1`, per consentire al programma di salvare eventuali modifiche in `esempio.conf`. Le opzioni `fast_reauth=1` e `ap_scan=1` vengono attivate globalmente: se servano o meno dipende dal tipo di rete alla quale ci si connette. Se invece si ha la necessità di specificare ulteriori opzioni globali, copiarle semplicemente da `/etc/wpa_supplicant/wpa_supplicant.conf`.

È anche possibile utilizzare `wpa_cli set` per visualizzare il contenuto delle opzioni o modificarlo. Possono essere inseriti più blocchi `network` nel file di configurazione: il supplicant gestirà autonomamente l'associazione e il roaming tra di essi, connettendosi di default al blocco con il segnale più forte, benchè sia possibile utilizzare l'opzione `priority=` per influenzarne il comportamento.

Uno dei vantaggi dell'utilizzare un file di configurazione personalizzato in `/etc/wpa_supplicant/wpa_supplicant.conf` è che quest'ultimo viene letto di default da [dhcpcd](/index.php/Dhcpcd "Dhcpcd"). Nel caso si scelga di utilizzarlo, è consigliabile fare un backup dell'originale ed eliminare i blocchi `network` d'esempio presenti. In caso contrario non ci si sorprenda se la propria interfaccia wireless tenta di collegarsi ai blocchi contenuti nel file di configurazione. Si noti inoltre che eventuali modifiche al file di configurazione dovranno essere [aggregate](/index.php/Pacnew_and_Pacsave_Files_(Italiano) "Pacnew and Pacsave Files (Italiano)").

**Suggerimento:** Per configurare un blocco `network` per una rete con *SSID* nascosto, che quindi non verrà rilevato durante una scansione, si utilizzi l'opzione `scan_ssid=1`.

### Connessione

#### Manuale

Si esegua il comando *wpa_supplicant*, i cui argomenti più comuni sono elencati di seguito:

*   `-B` - Esegue in background.
*   `-c nomefile` - Percorso al file di configurazione.
*   `-i interfaccia` - Interfaccia da configurare.
*   `-D driver` - Opzionale, specifica il driver da utilizzare. Per un elenco di quelli supportati si veda `wpa_supplicant -h`.
    *   `nl80211` è lo standard corrente, ma non è supportato da tutti i chip wireless.
    *   `wext` è deprecato, ma più supportato.

Si veda [wpa_supplicant(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_supplicant.8) per un elenco completo dei parametri.

Esempio:

```
# wpa_supplicant -B -i interface -c /etc/wpa_supplicant/example.conf

```

È ora possibile ottenere un indirizzo IP, come indicato nella sezione [#Panoramica](#Panoramica); ad esempio:

```
# dhcpcd *interfaccia*

```

**Suggerimento:** *dhcpcd* dispone di un hook per il lancio automatico di *wpa_supplicant*. Si veda a tal proposito [dhcpcd#10-wpa_supplicant](/index.php/Dhcpcd#10-wpa_supplicant "Dhcpcd").

#### All'avvio (systemd)

*wpa_supplicant* fornisce diversi servizi per l'avvio:

*   `wpa_supplicant.service` - utilizza [D-Bus](/index.php/D-Bus "D-Bus"), raccomandato per gli utilizzatori di [NetworkManager](/index.php/NetworkManager_(Italiano) "NetworkManager (Italiano)").
*   `wpa_supplicant@.service` - accetta il nome dell'interfaccia come parametro ed avvia il demone *wpa_supplicant* su quest'ultima. Legge il file di configurazione `/etc/wpa_supplicant/wpa_supplicant-*interfaccia*.conf`.
*   `wpa_supplicant-nl80211@.service` - anche questo servizio è specifico per interfaccia, ma forza l'utlilizzo del driver `nl80211`. Il percorso del file di configurazione è `/etc/wpa_supplicant/wpa_supplicant-nl80211-*interfaccia*.conf`.
*   `wpa_supplicant-wired@.service` - specifico per interfaccia, utilizza il driver `wired`. Il file di configurazione si trova in `/etc/wpa_supplicant/wpa_supplicant-wired-interface.conf`

Per abilitare l'interfaccia wireless al boot, si abiliti uno dei servizi di cui sopra.

Ad esempio:

```
# systemctl enable wpa_supplicant@*interfaccia*

```

È ora possibile [abilitare](/index.php/Systemd_(Italiano)#Usare_le_unit.C3.A0 "Systemd (Italiano)") un servizio per ottenere un indirizzo IP per una particolare *interfaccia*, come indicato nella sezione [#Panoramica](#Panoramica). Ad esempio:

```
# systemctl enable dhcpcd@*interfaccia*

```

**Suggerimento:** *dhcpcd* dispone di un hook per il lancio automatico di *wpa_supplicant*. Si veda a tal proposito [dhcpcd#10-wpa_supplicant](/index.php/Dhcpcd#10-wpa_supplicant "Dhcpcd").

### Action script per wpa_cli

È possibile lanciare *wpa_cli* come demone e fargli eseguire degli script basati su eventi provenienti da *wpa_supplicant*. Sono supportate due tipologie di eventi: `CONNECTED` e `DISCONNECTED`. Alcune [variabili d'ambiente](/index.php/Environment_variables "Environment variables") possono essere utilizzate negli script; si consulti [wpa_cli(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_cli.8) per ulteriori informazioni.

L'esempio che segue utilizza le [notifiche del desktop](/index.php/Desktop_notifications "Desktop notifications") per informare l'utente sull'attivazione degli eventi.

```
#!/bin/bash

case "$2" in
    CONNECTED)
        notify-send "WPA supplicant: connection established";
        ;;
    DISCONNECTED)
        notify-send "WPA supplicant: connection lost";
        ;;
esac
</nowiki>

```

Ricordarsi di rendere eseguibile lo script, quindi utilizzare lo switch `-a` per passare lo script a *wpa_cli*.

```
$ wpa_cli -a *percorso allo script*

```

## Risoluzione dei problemi

### Driver nl80211 non supportato su alcuni modelli

Alcune schede particolarmente vecchie potrebbero non funzionare con il driver `nl80211` e *wpa_supplicant* potrebbe mostare il seguente messaggio:

```
Successfully initialized wpa_supplicant
nl80211: Driver does not support authentication/association or connect commands
wlan0: Failed to initialize driver interface

```

che indica il mancato supporto al driver `nl80211`. In questo caso è possibile provare ad utilizzare il driver obsoleto `wext`:

```
# wpa_supplicant -B -i wlan0 **-D wext** -c /etc/wpa_supplicant/example.conf

```

Se il comando di cui sopra funziona e si desidera utilizzare [systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)") per gestire la connessione wireless, è necessario [modificare](/index.php/Systemd#Editing_provided_units "Systemd") il servizio `wpa_supplicant@.service` e modificare di conseguenza il parametro `ExecStart`:

 `/etc/systemd/system/wpa_supplicant@.service.d/wext.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/wpa_supplicant -c/etc/wpa_supplicant/wpa_supplicant-%I.conf -i%I **-Dwext**
```

## Link utili

*   [Homepage di WPA Supplicant](http://hostap.epitest.fi/wpa_supplicant/)
*   [Esempi per l'utilizzo di wpa_cli](https://gist.github.com/buhman/7162560)
*   [wpa_supplicant(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_supplicant.8)
*   [wpa_supplicant.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_supplicant.conf.5)
*   [wpa_cli(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_cli.8)
*   [Documentazione di wpa_supplicant](http://wireless.kernel.org/en/users/Documentation/wpa_supplicant)