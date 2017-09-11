Articoli correlati

*   [Configuring Network (Italiano)](/index.php/Configuring_Network_(Italiano) "Configuring Network (Italiano)")
*   [Software access point](/index.php/Software_access_point "Software access point")
*   [Ad-hoc networking](/index.php/Ad-hoc_networking "Ad-hoc networking")
*   [Internet Share (Italiano)](/index.php/Internet_Share_(Italiano) "Internet Share (Italiano)")

La configurazione dei dispositivi wireless è un processo suddiviso in due parti: innanzitutto occorre identificare la propria scheda di rete wireless e assicurarsi che i relativi driver (reperibili sull'immagine di installazione) siano caricati, quindi occorre configurarla. La seconda parte consiste nella scelta di un metodo di gestione delle connessioni wireless. Questa pagina coprirà entrambi i punti e fornirà link aggiuntivi ai vari tool di gestione.

## Contents

*   [1 Drivers](#Drivers)
    *   [1.1 Verificare se il driver per la propria periferica è stato caricato](#Verificare_se_il_driver_per_la_propria_periferica_.C3.A8_stato_caricato)
    *   [1.2 Installazione drivers/firmware](#Installazione_drivers.2Ffirmware)
*   [2 Gestione Wireless](#Gestione_Wireless)
    *   [2.1 Metodi di gestione](#Metodi_di_gestione)
    *   [2.2 Configurazione Manuale](#Configurazione_Manuale)
        *   [2.2.1 Ottenere informazioni utili](#Ottenere_informazioni_utili)
        *   [2.2.2 Attivazione dell'interfaccia](#Attivazione_dell.27interfaccia)
        *   [2.2.3 Ricerca degli Access Points](#Ricerca_degli_Access_Points)
        *   [2.2.4 Modalità di funzionamento](#Modalit.C3.A0_di_funzionamento)
        *   [2.2.5 Associazione](#Associazione)
        *   [2.2.6 Ottenere un indirizzo IP](#Ottenere_un_indirizzo_IP)
        *   [2.2.7 Script di configurazione/avvio personalizzati](#Script_di_configurazione.2Favvio_personalizzati)
            *   [2.2.7.1 Connessione wireless manuale al boot utilizzando systemd e dhcpcd](#Connessione_wireless_manuale_al_boot_utilizzando_systemd_e_dhcpcd)
        *   [2.2.8 Systemd più wpa_supplicant con IP statico](#Systemd_pi.C3.B9_wpa_supplicant_con_IP_statico)
    *   [2.3 Configurazione automatica](#Configurazione_automatica)
        *   [2.3.1 Netctl](#Netctl)
        *   [2.3.2 Wicd](#Wicd)
        *   [2.3.3 NetworkManager](#NetworkManager)
        *   [2.3.4 Wifi Radar](#Wifi_Radar)
        *   [2.3.5 Wlassistant](#Wlassistant)
*   [3 Risparmio energetico](#Risparmio_energetico)
*   [4 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [4.1 Impossibile ottenere un indirizzo IP](#Impossibile_ottenere_un_indirizzo_IP)
    *   [4.2 La connessione va sempre in timeout](#La_connessione_va_sempre_in_timeout)
        *   [4.2.1 Ridurre la velocità di trasmissione](#Ridurre_la_velocit.C3.A0_di_trasmissione)
        *   [4.2.2 Ridurre la potenza di trasmissione](#Ridurre_la_potenza_di_trasmissione)
        *   [4.2.3 Impostazione di rts e fragmentation treshold](#Impostazione_di_rts_e_fragmentation_treshold)
    *   [4.3 Disconnessioni casuali](#Disconnessioni_casuali)
        *   [4.3.1 Causa 1](#Causa_1)
        *   [4.3.2 Causa 2](#Causa_2)
*   [5 Risoluzione dei problemi di drivers e firmware](#Risoluzione_dei_problemi_di_drivers_e_firmware)
    *   [5.1 Ralink](#Ralink)
        *   [5.1.1 rt2x00](#rt2x00)
        *   [5.1.2 rt2860 e rt2870](#rt2860_e_rt2870)
        *   [5.1.3 rt3090](#rt3090)
        *   [5.1.4 rt3290](#rt3290)
        *   [5.1.5 rt3573](#rt3573)
        *   [5.1.6 rt5572](#rt5572)
    *   [5.2 Realtek](#Realtek)
        *   [5.2.1 rtl8192cu](#rtl8192cu)
        *   [5.2.2 rtl8192e](#rtl8192e)
        *   [5.2.3 rtl8192s](#rtl8192s)
    *   [5.3 Atheros](#Atheros)
        *   [5.3.1 madwifi-ng](#madwifi-ng)
        *   [5.3.2 ath5k](#ath5k)
        *   [5.3.3 ath9k](#ath9k)
        *   [5.3.4 ath9k_htc](#ath9k_htc)
    *   [5.4 Intel](#Intel)
        *   [5.4.1 ipw2100 e ipw2200](#ipw2100_e_ipw2200)
        *   [5.4.2 iwl3945, iwl4965 e serie-iwl5000](#iwl3945.2C_iwl4965_e_serie-iwl5000)
            *   [5.4.2.1 Caricamento del Driver](#Caricamento_del_Driver)
            *   [5.4.2.2 Disattivazione del lampeggio dei LED](#Disattivazione_del_lampeggio_dei_LED)
        *   [5.4.3 Altre osservazioni](#Altre_osservazioni)
    *   [5.5 Broadcom](#Broadcom)
    *   [5.6 Altri drivers/dispositivi](#Altri_drivers.2Fdispositivi)
        *   [5.6.1 w322u](#w322u)
        *   [5.6.2 orinoco](#orinoco)
        *   [5.6.3 prism54](#prism54)
        *   [5.6.4 ACX100/111](#ACX100.2F111)
        *   [5.6.5 zd1211rw](#zd1211rw)
        *   [5.6.6 carl9170](#carl9170)
        *   [5.6.7 hostap_cs](#hostap_cs)
    *   [5.7 ndiswrapper](#ndiswrapper)
    *   [5.8 compat-drivers-patched](#compat-drivers-patched)
    *   [5.9 Link utili](#Link_utili)

## Drivers

Il kernel di Arch è *modulare*, il che significa che la maggior parte dei driver per l'hardware della macchina risiedono sull'hard disk e sono disponibili come *[moduli](/index.php/Kernel_modules_(Italiano) "Kernel modules (Italiano)")*. All'avvio, [udev](/index.php/Udev_(Italiano) "Udev (Italiano)") fa un inventario dell'hardware presente. Lo stesso udev carica quindi i moduli (i driver) per l'hardware corrispondente, e il driver, di contro, permette la creazione di una *kernel interface*.

Alcuni chipset wireless richiedono oltre al driver l'installazione di un firmware, alcuni dei quali sono contenuti nel pacchetto [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware), installato di default. Tuttavia, alcuni firmware sono proprietari e dovranno essere installati separatamente, come spiegato in [#Installazione drivers/firmware](#Installazione_drivers.2Ffirmware)

**Nota:**

*   Udev non è perfetto. Se il modulo appropriato non è caricato all'avvio, basta [caricarlo manualmente](/index.php/Kernel_modules_(Italiano)#Caricamento "Kernel modules (Italiano)"). Si noti inoltre che udev può occasionalmente caricare più di un driver per una periferica, e il conflitto risultante impedirebbe una configurazione corretta della periferica. Asicurarsi quindi di mettere in [blacklist](/index.php/Kernel_modules_(Italiano)#Blacklist "Kernel modules (Italiano)") eventuali moduli non necessari.
*   Il nome dell'interfaccia varia in base al driver e al chipset installato. Alcuni esempi sono `wlan0`, `eth1`, o `ath0`.

**Suggerimento:** Benchè non sia strettamente necessario, è utile installare innanzitutto i tools in user-space menzionati alla sezione [#Configurazione Manuale](#Configurazione_Manuale), soprattutto nel caso in cui dovessero verificarsi problemi.

### Verificare se il driver per la propria periferica è stato caricato

Per verificare che il driver per la propria scheda di rete wireless sia stato caricato, si controlli l'output del comando `lspci -k`, dal quale si può desumere il driver del kernel in uso.

Ad esempio:

 `$ lspci -k` 
```
06:00.0 Network controller: Intel Corporation WiFi Link 5100
	Subsystem: Intel Corporation WiFi Link 5100 AGN
	Kernel driver in use: iwlwifi
	Kernel modules: iwlwifi

```

**Nota:** La scheda Wi-Fi integrata in alcuni portatili potrebbe essere un dispositivo USB, perciò è utile controllare l'output dei seguenti comandi:

*   `lsusb -v`
*   `dmesg | grep usbcore` (dovrebbe essere visualizzato un messaggio simile a `usbcore: registered new interface driver rtl8187`.

Controllare inoltre l'output del comando `ip link` per verificare l'avvenuta creazione di un'interfaccia wireless (ad esempio `wlan0`, `wlp2s1`, `ath0`) ed attivarla con `ip link set <interfaccia> up`. Ad esempio, se l'interfaccia è `wlan0`:

```
# ip link set dev wlan0 up

```

Se si ottiene un messaggio d'errore simile al seguente: `SIOCSIFFLAGS: No such file or directory`, sarà quasi sicuramente necessario caricare il firmware adeguato.

Si controllino eventuali messaggi del kernel relativi al caricamento del firmware:

 `$ dmesg | grep firmware` 
```
[   7.148259] iwlwifi 0000:02:00.0: loaded firmware version 39.30.4.1 build 35138 op_mode iwldvm

```

L'output di `dmesg` dovrebbe essere corredato dal nome del modulo in uso, il che può essere d'aiuto nel risolvere eventuali problemi.

Se il modulo del kernel è stato correttamente caricato e l'interfaccia è attiva, si salti tranquillamente la prossima sezione.

### Installazione drivers/firmware

*   Sul [Wiki di Ubuntu](https://help.ubuntu.com/community/WifiDocs/WirelessCardsSupported) c'è una buona lista di schede wireless con relativa indicazione del supporto o meno da parte del Kernel o sulla disponibilità di un driver in user-space (incluso il nome del driver).
*   Anche [Linux Wireless Support](http://linux-wless.passys.nl/) e le "Linux Questions" in [Hardware Compatibility List](http://www.linuxquestions.org/hcl/index.php?cat=10) (HCL) contengono un elenco di hardware wireless supportato.
*   Inoltre, questa [pagina](http://wireless.kernel.org/en/users/Devices) contiene una matrice addizionale di hardware supportato.

Se la propria scheda di rete wireless compare in uno degli elenchi di cui sopra, si consulti la sezione [#Risoluzione dei problemi di drivers e firmware](#Risoluzione_dei_problemi_di_drivers_e_firmware), che contiene informazioni sull'installazione di drivers e firmware per schede specifiche. Si effettuino quindi nuovamente le operazioni descritte in [#Verificare se il driver per la propria periferica è stato caricato](#Verificare_se_il_driver_per_la_propria_periferica_.C3.A8_stato_caricato).

Se la scheda wireless non è elencata sopra, è probabile che sia supportata solo da Windows (come alcune Broadcom, 3com, ecc). Per queste schede è possibile provare ad utilizzare *ndiswrapper*. Si consulti la sezione [#ndiswrapper](#ndiswrapper) per ulteriori informazioni.

## Gestione Wireless

Dando per scontato che abbiate installato correttamente i driver, ora si avrà bisogno di un metodo per gestire la connettività wifi. Le seguenti sottosezioni vi aiuteranno a capire quale di essi sarà più adatto alle vostre necessità.

La procedure e gli strumenti di cui avrete bisogno dipendono da una pluralità di fattori:

*   La facilità di configurazione e gestione, da un approccio completamente manuale che dovrete ripetere ad ogni riavvio fino alla gestione automatica tramite frontend grafici
*   Il tipo di protezione (o nessuna) che protegge la vostra rete wireless.
*   La necessità o meno dei profili di rete, es. se il vostro pc cambia frequentemente la rete a cui connettersi (come fa un portatile).

**Suggerimento:**

*   Qualunque sia la scelta, dovreste provare a connettervi innanzitutto col metodo manuale. Questo vi aiuterà a capire i vari passi necessari per una connessione, oltre ad individuare più facilmente eventuali problemi che possono sorgere. Un altro consiglio.
*   Se possibile (es. se avete i poteri di amministrazione del vostro access point), provate innanzitutto a connettervi senza crittazione, per assicurarvi che tutto funzioni. Quindi provare a utilizzare la crittografia, sia WEP (più semplice da configurare, ma violabile in pochi minuti, anche se quasi più sicura di una connessione non crittografata), sia WPA o WPA2.

### Metodi di gestione

Questa tabella mostra i differenti metodi che possono essere utilizzati per attivare e gestire una connessione wireless, a seconda del tipo di crittazione e del metodo di gestione che si vuole utilizzare, e i vari strumenti che sono necessari per ogni caso. Anche se ci sono possibilità ulteriori, queste sono quelle utilizzate più di frequente:

| Gestione | Senza Crittazione/WEP | WPA/WPA2 PSK |
| Manuale | [iproute2](https://www.archlinux.org/packages/?name=iproute2) + `iwconfig` + `dhcpcd`/`iproute2` | `iproute2` + `iwconfig` + [wpa_supplicant](/index.php/WPA_supplicant_(Italiano) "WPA supplicant (Italiano)") + `dhcpcd`/`iproute2` |
| Automatica, con supporto ai profili di rete | [netctl](/index.php/Netctl "Netctl"), [wicd](/index.php/Wicd_(Italiano) "Wicd (Italiano)"), [NetworkManager](/index.php/NetworkManager_(Italiano) "NetworkManager (Italiano)"), ecc… |

Altri metodi:

| Gestione | Connessione automatica al boot | Riconnessione automatica se si perde la connessione
o si cambia posizione | Supporta i Modem 3G | GUI | Tool da riga di comando |
| [Netctl](/index.php/Netctl "Netctl") | Sì | Sì | - | Sì | `netctl` |
| [Wicd](/index.php/Wicd_(Italiano) "Wicd (Italiano)") | Sì | Sì | - | Sì | `wicd-curses` |
| [NetworkManager](/index.php/NetworkManager_(Italiano) "NetworkManager (Italiano)") +
[network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) | Sì | Sì | Sì | Sì | `nmcli` |

### Configurazione Manuale

Il pacchetto [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools) fornisce un set base di strumenti utili a configurare una rete wireless, anche se questi ultimi sono deprecati in favore del tool [iw](https://www.archlinux.org/packages/?name=iw). Se `iw` non funziona con la propria scheda di rete, è comunque possibile utilizzare `wireless_tools`. La tabella presentata sotto fornisce una comparazione tra i due tool; si veda [[1]](http://wireless.kernel.org/en/users/Documentation/iw/replace-iwconfig%7Cquesta) pagina per ulteriori informazioni. Se necessitate di crittazione WPA\WPA2, sarà inoltre necessario il pacchetto [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant). Questi potenti strumenti funzionano egregiamente e permettono un controllo pressochè totale delle connessioni da linea di comando.

**Nota:**

*   Negli esempi seguenti, si presume che la periferica wireless sia `wlan0` e che ci si stia connettendo all'access point `"your_essid"`. Si sostituiscano i due valori di conseguenza.
*   Si noti inoltre che la maggior parte dei comandi proposti dovrà essere eseguita con [i permessi di root](/index.php/Users_and_groups_(Italiano) "Users and groups (Italiano)"). In caso contrario, alcuni comandi come `iwlist` potrebbero terminare correttamente ma senza produrre l'output corretto, creando confusione.

| Comando *iw* | Comando *wireless_tools* | Descrizione |
| iw dev wlan0 link | iwconfig wlan0 | Informazioni sullo stato del collegamento. |
| iw dev wlan0 scan | iwlist wlan0 scan | Scansione degli access points disponibili. |
| iw wlan0 set type ibss | iwconfig wlan0 mode ad-hoc | Attiva la modalità *ad-hoc*. |
| iw wlan0 connect *your_essid* | iwconfig wlan0 essid *your_essid* | Connessione ad una rete senza password. |
| iw wlan0 connect *your_essid* 2432 | iwconfig wlan0 essid *your_essid* freq 2432M | Connessione ad una rete senza password specificando il canale. |
| iw wlan0 connect *your_essid* key 0:*your_key* | iwconfig wlan0 essid *your_essid* key *your_key* | Connessione ad una rete protetta tramite WEP con una chiave esadecimale. |
| iw wlan0 connect *your_essid* key 0:*your_key* | iwconfig wlan0 essid *your_essid* key s:*your_key* | Connessione ad una rete protetta tramite WEP con una chiave ASCII. |
| iw dev wlan0 set power_save on | iwconfig wlan0 power on | Abilita il risparmio energetico. |

**Nota:** A seconda del vostro hardware e del metodo di protezione scelto, alcuni dei passi seguenti potrebbero non essere necessari. Alcune schede sono famose per necessitare dell'attivazione dell'interfaccia e/o della rilevazione degli access points prima di essere associate ad un access point ed a un indirizzo IP. Potrebbe dunque essere necessario qualche tentativo. Ad esempio, chi utilizza WPA/WPA2, può direttamente seguire i passi a partire dalla sezione [#Associazione](#Associazione).

#### Ottenere informazioni utili

**Suggerimento:** Si consulti la [documentazione ufficiale](http://wireless.kernel.org/en/users/Documentation/iw) di `iw` per ulteriori informazioni.

*   La prima cosa da fare è trovare il nome della propria scheda di rete wireless. È possibile farlo con il seguente comando:

 `$ iw dev` 
```
Connected to 12:34:56:78:9a:bc (on wlan0)
	SSID: MyESSID
	freq: 2412
	RX: 33016518 bytes (152703 packets)
	TX: 2024638 bytes (11477 packets)
	signal: -53 dBm
	tx bitrate: 150.0 MBit/s MCS 7 40MHz short GI

	bss flags:	short-preamble short-slot-time
	dtim period:	1
	beacon int:	100

```

*   Per verificare lo stato del collegamento, utilizzare il seguente comando. Se si è associati ad un Access Point, l'output sarà il seguente:

 `$ iw dev wlan0 link` 
```
Not connected.

```

Quando si è associati, l'output diventa:

 `$ iw dev wlan0 link` 
```
Connected to 12:34:56:78:9a:bc (on wlan0)
	SSID: MyESSID
	freq: 2412
	RX: 33016518 bytes (152703 packets)
	TX: 2024638 bytes (11477 packets)
	signal: -53 dBm
	tx bitrate: 150.0 MBit/s MCS 7 40MHz short GI

	bss flags:	short-preamble short-slot-time
	dtim period:	1
	beacon int:	100

```

*   È possibile visualizzare varie statistiche, come il numero di byte trasmessi/ricevuti, la potenza del segnale e altro. con il seguente comando:

 `$ iw dev wlan0 station dump` 
```
Station 12:34:56:78:9a:bc (on wlan0)
	inactive time:	1450 ms
	rx bytes:	24668671
	rx packets:	114373
	tx bytes:	1606991
	tx packets:	8557
	tx retries:	623
	tx failed:	1425
	signal:  	-52 dBm
	signal avg:	-53 dBm
	tx bitrate:	150.0 MBit/s MCS 7 40MHz short GI
	authorized:	yes
	authenticated:	yes
	preamble:	long
	WMM/WME:	yes
	MFP:		no
	TDLS peer:	no

```

#### Attivazione dell'interfaccia

*(Opzionale, ma può essere richiesto)*

Molte schede necessitano che l'interfaccia del kernel venga attivata prima di poter utilizzare i `wireless_tools`:

```
# ip link set wlan0 up

```

**Nota:** Se si ottengono errori simili a `RTNETLINK answers: Operation not possible due to RF-kill`, assicurarsi che l'interruttore hardware che controlla la scheda wireless sia su "ON". È anche possibile che la scheda sia bloccata via software, nel qual caso sarà necessario installare [rfkill](https://www.archlinux.org/packages/?name=rfkill) e controllare con `rfkill list all`.

#### Ricerca degli Access Points

Controllate quali access points sono disponibili:

```
# iw dev wlan0 scan | less

```

Comando alternativo:

```
$ iwlist wlan0 scanning | less

```

**Nota:** Se viene visualizzato '**Interface doesn't support scanning'** probabilmente non si è installato il firmware. In alcuni casi lo stesso messaggio potrebbe apparire se il comando non viene eseguito come utente root.

Voci importanti:

*   ESSID: indica il nome dell'access point.
*   Quality: è generalmente consigliabile connettersi ad una rete con un valore pari o superiore a 40/70
*   Encryption key: se ha valore "on", si controlli la presenza di linee riguardanti:
    *   WEP, WPA o RSN. Si noti che RSN e WPA2 sono nomi differenti dello stesso protocollo.
    *   Group cipher: ha valori TKIP, CCMP, entrambi, altri.
    *   Pairwise ciphers: ha valori: TKIP, CCMP, entrambi, altri. Non ha necessariamente lo stesso valore di "Group cipher.
    *   Authentication Suites: ha valore PSK, 802.1x, altri. Utilizzando un router domestico, sarà solitamente visualizzato il valore PSK (ovvero "passphrase"). Nelle università, è più probabile trovare la suite 802.1x, che richiede un login ed una password. Sarà poi necessario conoscere il tipo di metodo per la gestione delle chiavi da utilizzare (ad esempio EAP) e quale incapsulazione esso utilizza (ad esempio PEAP). Per ulteriori dettagli consultare [wikipedia:List_of_authentication_protocols](https://en.wikipedia.org/wiki/List_of_authentication_protocols "wikipedia:List of authentication protocols").

#### Modalità di funzionamento

*(Opzionale, ma può essere richiesto)*

A questo punto potrebbe essere necessario impostare la corretta modalità di funzionamento della scheda wireless. Più specificamente, se avete intenzione di collegarvi ad una rete ad-hoc, potrebbe essere necessario impostare la modalità di funzionamento a *ad-hoc:*

```
# iw wlan0 set type ibss

```

**Nota:** Prima di cambiare la modalità di funzionamento potrebbe essere necessario disattivare la scheda prima di procedere: `ip link set wlan0 down`.

#### Associazione

A seconda del tipo di crittazione, sarà necessario associare la vostra scheda wifi con l'access point da utilizzare, e inserire la chiave di crittazione.

*   **Nessuna crittazione**

```
# iw dev wlan0 connect MyEssid

```

*   **WEP**

con una chiave esadecimale:

```
# iw wlan0 connect your_essid key 0:*your_key*

```

con una chiave ASCII, specificando la terza chiave come default (le chiavi sono contate a partire da 0):

```
# iw wlan0 connect your_essid key d:2:*your_key*

```

*   **WPA/WPA2**

Sarà necessario modificare il file `/etc/wpa_supplicant.conf` come descritto nella pagina [WPA Supplicant](/index.php/WPA_supplicant_(Italiano) "WPA supplicant (Italiano)"). Quindi, eseguire il comando:

```
# wpa_supplicant -i wlan0 -c /etc/wpa_supplicant.conf

```

Ciò è valido presupponendo che la periferica utilizzi il driver `wext`. In caso di problemi, si controllino le opzioni. Se la connessione funziona correttamente, continuare in un nuovo terminale (o uscire da `wpa_supplicant` con `Ctrl+c` e aggiungere l'opzione `-B` al comando precedente per farlo funzionare in background).

Controllare la pagina relativa a [WPA Supplicant](/index.php/WPA_supplicant_(Italiano) "WPA supplicant (Italiano)") per maggiori informazioni e suggerimenti.

Indipendentemente dal metodo utilizzato, è possibile verificare l'avvenuta associazione con:

```
# iw dev wlan0 link

```

#### Ottenere un indirizzo IP

**Nota:** Si legga la pagina [Configuring Network (Italiano)#Configurare l'indirizzo IP](/index.php/Configuring_Network_(Italiano)#Configurare_l.27indirizzo_IP "Configuring Network (Italiano)") per ulteriori esempi.
.

Infine, associate la vostra interfaccia di rete ad un indirizzo IP. Alcuni semplici esempi:

```
# dhcpcd wlan0

```

per il DHCP, oppure

```
# ip addr add 192.168.0.2/24 dev wlan0
# ip route add default via 192.168.0.1

```

per un indirizzo IP statico.

**Nota:** Se si verifica un errore di timeout a causa di un errore *waiting for carrier* allora potrebbe essere necessario impostare la modalità del canale a `auto` per il dispositivo specifico.
```
# iwconfig wlan0 channel auto

```
Prima di impostare il canale su `auto`, assicurarsi che la propria scheda di rete wireless sia disattivata. Una volta effettuato il cambiamento, sarà possibile riattivarla.

#### Script di configurazione/avvio personalizzati

Benchè la configurazione manuale renda più semplice la risoluzione di eventuali problemi, sarà necessario riscrivere tutti i comandi ad ogni riavvio. È anche possibile scrivere un semplice script di shell per automatizzare l'intera procedura, il che è comunque un buon metodo per gestire la propria connessione di rete mantenendo allo stesso tempo il controllo sulla propria configurazione.

Nella sezione successiva sarà possibile trovare alcuni esempi.

##### Connessione wireless manuale al boot utilizzando systemd e dhcpcd

Questo esempio utilizza [systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)") per l'avvio, `dhcpcd` e [WPA Supplicant](/index.php/WPA_supplicant_(Italiano) "WPA supplicant (Italiano)") per la connessione.

Si crei un servizio per systemd, ad esempio `/etc/systemd/system/network@.service`:

 `/etc/systemd/system/network@.service` 
```
[Unit]
Description=Network Connectivity (%i)
Wants=network.target
Before=network.target
BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

[Service]
Type=oneshot
RemainAfterExit=yes
EnvironmentFile=/etc/conf.d/network
ExecStart=/usr/bin/ip link set dev %i up
ExecStart=/usr/bin/wpa_supplicant -B -i %i -c /etc/wpa_supplicant.conf
ExecStart=/usr/bin/dhcpcd %i

[Install]
WantedBy=multi-user.target

```

Si abiliti il servizio e lo si avvii, passandogli il nome dell'interfaccia:

```
# systemctl enable network@wlp0s26f7u3.service
# systemctl start network@wlp0s26f7u3.service

```

#### Systemd più wpa_supplicant con IP statico

Si crei il file `/etc/conf.d/network`:

 `/etc/conf.d/network` 
```
address=192.168.0.10
netmask=24
broadcast=192.168.0.255
gateway=192.168.0.1

```

Assicurarsi che [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) sia installato e creare il file `/etc/wpa_supplicant.conf`. Si faccia riferimento a [WPA Supplicant](/index.php/WPA_supplicant_(Italiano) "WPA supplicant (Italiano)").

 `/etc/wpa_supplicant.conf` 
```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=network
update_config=1
network={
        ssid="My-Wireless"
        psk=b705a6bfcd5639d5c40cd972cd4048cfb94572987f30d324c82036317b91a138
}

```

Si crei un servizio di systemd:

 `/etc/systemd/system/network@.service` 
```
[Unit]
Description=Network Connectivity (%i)
Wants=network.target
Before=network.target
BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

[Service]
Type=oneshot
RemainAfterExit=yes
EnvironmentFile=/etc/conf.d/network
ExecStart=/usr/bin/ip link set dev %i up
ExecStart=/usr/bin/wpa_supplicant -B -i %i -c /etc/wpa_supplicant.conf
ExecStart=/usr/bin/ip addr add ${address}/${netmask} broadcast ${broadcast} dev %i
ExecStart=/usr/bin/ip route add default via ${gateway}
ExecStop=/usr/bin/ip addr flush dev %i
ExecStop=/usr/bin/ip link set dev %i down

[Install]
WantedBy=multi-user.target

```

Si abiliti il servizio e lo si avvii, passandogli il nome dell'interfaccia:

```
# systemctl enable network@wlp0s26f7u3.service
# systemctl start network@wlp0s26f7u3.service

```

### Configurazione automatica

Ci sono molte soluzioni tra cui scegliere, ma si ricordi che tutte si escludono a vicenda: non si dovrebbero tenere in esecuzione due demoni contemporaneamente.

#### Netctl

`netctl` sostituisce il vecchio `netcfg` e funziona egregiamente con systemd. Utilizza un setup basato su profili ed è in grado di rilevare e connettersi ad un'ampia varietà di reti. Il suo utilizzo non è da considerarsi più complicato rispetto a tool grafici.

Si veda [Netctl](/index.php/Netctl "Netctl").

#### Wicd

Wicd è un gestore di reti che può gestire sia connessioni via cavo che wireless. E' scritto in Python e Gtk, con meno dipendenze rispetto a NetworkManager, rendendolo una soluzione ideale per coloro che desiderano utilizzare un ambiente desktop leggero. Wicd è disponibile nel repository `[extra]` sia per sistemi i686 che per x86_64.

Si veda [Wicd](/index.php/Wicd_(Italiano) "Wicd (Italiano)").

#### NetworkManager

NetworkManager è un avanzato tool di gestione delle reti che è disponibile di default in molte distribuzioni Linux. Oltre a gestire le connessioni via cavo, NetworkManager offre un sistema per gestire il roaming wifi tramite una semplice interfaccia grafica senza dover preoccuparsi di modificare file o dover usare comandi da console.

Se non si utilizza [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)") ma un window manager come [Openbox](/index.php/Openbox_(Italiano) "Openbox (Italiano)") o [xmonad](/index.php/Xmonad "Xmonad"), non dimenticarsi di [installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") [polkit-gnome](https://www.archlinux.org/packages/?name=polkit-gnome), [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring), [libgnome-keyring](https://www.archlinux.org/packages/?name=libgnome-keyring) e [pyxdg](https://www.archlinux.org/packages/?name=pyxdg) per gestire le connessioni WEP, WPA, e WPA2:

Si veda [NetworkManager](/index.php/NetworkManager_(Italiano) "NetworkManager (Italiano)").

#### Wifi Radar

WiFi Radar è una utility Python/PyGTK2 per gestire diversi profili wireless (e *solo* wireless). E' in grado di effettuare lo scan delle reti wireless disponibili e di creare profili per le vostre reti preferite.

Si veda [Wifi Radar](/index.php/Wifi_Radar "Wifi Radar").

#### Wlassistant

Wlassistant è un'interfaccia grafica molto intuitiva per gestire le connessioni wireless.

Installare il pacchetto [wlassistant](https://aur.archlinux.org/packages/wlassistant/) da [AUR](/index.php/AUR "AUR").

Wlassistant deve essere eseguito con privilegi di amministratore:

```
# wlassistant

```

Un metodo per usare wlassistant è quello di configurare la scheda wireless attraverso `/etc/rc.conf`, specificando l'access point utilizzato più spesso. All'avvio, la scheda sarà automaticamente configurata per il SSID scelto, e se dovessero servire od essere disponibili altre reti, `wlassistant` potrà comunque essere eseguito per connettervisi. Mettere il demone network in background con un `@` davanti nell'`/etc/rc.conf` per evitare inutili attese durante il boot.

## Risparmio energetico

Si veda [Power saving#Network interfaces](/index.php/Power_saving#Network_interfaces "Power saving").

## Risoluzione dei problemi

Questa sezione contiene informazioni generali relative alla risoluzione dei problemi non correlate a problemi con drivers e firmware, trattati nella sezione successiva.

### Impossibile ottenere un indirizzo IP

Se non si riesce ad ottenere un indirizzo IP tramite il client di default [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd), si provi con [dhclient](https://www.archlinux.org/packages/?name=dhclient). Ricordarsi di selezionare `dhclient` come client DHCP predefinito nel proprio [gestore di rete](#Configurazione_automatica).

Se si riesce ad ottenere un indirizzo tramite interfaccia Ethernet ma non tramite Wifi, si provi a disabilitare il risparmio energetico della scheda wireless:

1.  iwconfig wlan0 power off

### La connessione va sempre in timeout

Il driver potrebbe essere messo a dura prova da eventuali tentativi eccessivi di trasmissione o errori di "invalid misc" che causano la perdita di pacchetti e continue disconnessioni, talvolta istantanee. I seguenti consigli potrebbero essere utili.

#### Ridurre la velocità di trasmissione

Si esegua:

```
# iwconfig wlan0 rate 5.5M auto

```

L'opzione `fixed` dovrebbe bloccare la velocità in base a quanto scelto, impedendo al driver di cambiarla a proprio piacimento e rendendo così la connessione più stabile.

#### Ridurre la potenza di trasmissione

È inoltre possibile provare a ridurre la potenza di trasmissione, il che contribuisce anche al risparmio energetico:

```
# iwconfig wlan0 txpower 5

```

Valori validi vanno da `0` a `20`, `auto` e `off`.

#### Impostazione di rts e fragmentation treshold

Le impostazioni di default di iwconfig disabilitano rts e il fragmentation treshold. Queste opzioni sono particolarmente efficaci se si è in presenza di numerosi Access Points o se ci si trova in un ambiente con molte interferenze.

Il valore minimo per fragmentation è `256`, mentre il massimo è `2346`. In numerosi drivers per Windows, il massimo è il valore di default.

```
# iwconfig wlan0 frag 2346

```

Per quanto riguarda rts, il minimo è `0` e il massimo è `2347`. Anche in questo caso, i drivers per Windows spesso utilizzano il valore massimo:

```
# iwconfig wlan0 rts 2347

```

### Disconnessioni casuali

#### Causa 1

Se {ic|dmesg}} riporta `wlan0: deauthenticating from MAC by local choice (reason=3)` è probabile che le impostazioni di risparmio energetico siano troppo aggressive ([[2]](http://us.generation-nt.com/answer/gentoo-user-wireless-deauthenticating-by-local-choice-help-204640041.html).). Si provi a disabilitare il risparmio energetico:

```
# iwconfig wlan0 power off

```

Si veda [Power saving](/index.php/Power_saving "Power saving") per rendere permanenti le impostazioni (si specifichi semplicemente `off` invece di `on`).

Se la propria scheda di rete non supporta le funzionalità di risparmio energetico, si controllino le relative impostazioni del BIOS. Ad esempio, disabilitare il risparmio energetico per lo slot PCI-Express su un Lenovo W520 ha risolto il problema.

#### Causa 2

Se si verificano frequenti disconnessioni e `dmesg` mostra: `ieee80211 phy0: wlan0: No probe response from AP xx:xx:xx:xx:xx:xx after 500ms, disconnecting`, si provi a cambiare la banda del canale a `20 MHz` dal pannello di configurazione del router.

## Risoluzione dei problemi di drivers e firmware

Questa sezione tratta dei metodi e delle procedure di installazione di moduli del kernel e firmware per chipsets specifici, la cui procedura differisce da quella standard.

Si veda [Kernel modules](/index.php/Kernel_modules_(Italiano) "Kernel modules (Italiano)") per ulteriori informazioni sui moduli.

#### Ralink

##### rt2x00

Il driver unificato per i chipset Ralink (rimpiazza i vari driver separati per `rt2500`,`rt61`,`rt73` ecc.). Questo driver è compatibile con gli strumenti `wpa_supplicant` e `iwconfig` ed è incluso nel kernel dalla versione 2.6.24\. È semplicemente necessario caricare il modulo adeguato per il chipset in uso: `rt2400pci`, `rt2500pci`, `rt2500usb`, `rt61pci` o `rt73usb`, i quali caricheranno automaticamente i rispettivi moduli `rt2x00`.

Un elenco dei dispositivi supportati da questi moduli è reperibile sulla [homepage](http://rt2x00.serialmonkey.com/wiki/index.php/Hardware) del progetto.

##### rt2860 e rt2870

Dalla versione del kernel linux 3.0, il driver `rt2860sta` è stato sostituito dal driver `rt2800pci`, e `rt2870sta` da `rt2800usb`. Fonte: [Kernel commit](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=commitdiff;h=fefecc6989b4b24276797270c0e229c07be02ad3). Il driver `rt2800` funziona automaticamente con dispositivi che utilizzano il chipset `rt2870`.

Ha una vasta gamma di opzioni che possono essere configurate con `iwpriv`. Queste sono ben documentate nei [tarballs dei sorgenti](http://www.ralinktech.com/ralink/Home/Support/Linux.html) resi disponibili da Ralink

##### rt3090

I dispositivi dotati di chipset rt3090 potrebbero funzionare con il driver `rt2870sta`. `rt2800pci`, il driver di riferimento, non funziona molto bene con questo chipset e potrebbe non essere possibile andare oltre i 2 Mb/s di banda.

È consigliabile installare il driver [rt3090](https://aur.archlinux.org/packages/rt3090/) da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") e cancellare/spostare il file del firmware `/etc/Wireless/RT2860STA/RT2860STA.dat` per consentire l'installazione del pacchetto [rt3090](https://aur.archlinux.org/packages/rt3090/). Si metta in [blacklist](/index.php/Kernel_modules_(Italiano)#Blacklist "Kernel modules (Italiano)") il modulo `rt2860sta` e si abiliti il [caricamento](/index.php/Kernel_modules_(Italiano)#Caricamento "Kernel modules (Italiano)") del modulo `rt3090` al boot.

**Nota:** È possibile utilizzare questo driver anche con chipsets rt3062.

##### rt3290

Il chipset rt3290 utilizza il modulo del kernel `rt2800pci`, anche se alcuni utenti segnalano problemi che possono essere risolti [utilizzando](https://bbs.archlinux.org/viewtopic.php?id=161952) il driver Ralink proprietario opportunamente patchato.

##### rt3573

Nuovo chipset (2012). Potrebbe richiedere un driver proprietario fornito da Ralink. Differenti produttori lo utilizzano: si veda per esempio il [Belkin N750](https://bbs.archlinux.org/viewtopic.php?pid=1164228#p1164228).

##### rt5572

Nuovo chipset (2012) con supporto ai 5 Ghz. Potrebbe richiedere driver proprietari forniti da Ralink. Al momento, è disponibile un HOWTO sulla compilazione valido per la D-Link DWA-160 rev. B2, [qui](http://bernaerts.dyndns.org/linux/229-ubuntu-precise-dlink-dwa160-revb2).

#### Realtek

##### rtl8192cu

Il driver è parte del kernel attuale, anche se diversi utenti hanno riscontrato l'impossibilità di stabilire una connessione, mentre non ci sono problemi nella scansione delle reti.

Il pacchetto [dkms-8192cu](https://aur.archlinux.org/packages/dkms-8192cu/) presente su AUR potrebbe funzionare meglio per alcuni utenti.

##### rtl8192e

Il driver è parte del kernel attuale.

L'inizializzazione del modulo potrebbe non riuscire in fase di boot dando questo messaggio di errore:

```
rtl819xE:ERR in CPUcheck_firmware_ready()
rtl819xE:ERR in init_firmware() step 2
rtl819xE:ERR!!! _rtl8192_up(): initialization is failed!
r8169 0000:03:00.0: eth0: link down

```

Una semplice soluzione è quella di scaricare il modulo:

```
# modprobe -r r8192e_pci

```

e ricaricarlo (dopo una pausa):

```
# modprobe r8192e_pci

```

##### rtl8192s

Il driver è parte del kernel attuale. Può essere necessario aggiungere manualmente il firmware in caso `/usr/lib/firmware/RTL8192SU/rtl8192sfw.bin` non esista. (`dmesg` riporterebbe *"rtl819xU:FirmwareRequest92S(): failed"* se mancasse il firmware)

Per scaricare e installare il firmware:

```
$ wget [http://launchpadlibrarian.net/33927923/rtl8192se_linux_2.6.0010.1012.2009.tar.gz](http://launchpadlibrarian.net/33927923/rtl8192se_linux_2.6.0010.1012.2009.tar.gz)
# mkdir /lib/firmware/RTL8192SU
# tar -xzOf rtl8192se_linux_2.6.0010.1012.2009.tar.gz \
 rtl8192se_linux_2.6.0010.1012.2009/firmware/RTL8192SE/rtl8192sfw.bin > \
 /usr/lib/firmware/RTL8192SU/rtl8192sfw.bin

```

**Nota:** Può essere trovata una versione alternativa del firmware [qui](http://launchpadlibrarian.net/37387612/rtl8192sfw.bin.gz), ma questa versione può causare l'interruzione delle connessioni.

#### Atheros

##### madwifi-ng

Esistono tre moduli, correntemente mantenuti dal team MadWifi:

*   `ath_pci`, il driver più vecchio
*   **`ath5k`**, destinato a sostituire `ath_pci`. Attualmente è una scelta migliore per alcuni chipsets, ma non tutti sono supportati (si veda sotto)
*   **`ath9k`**, il nuovo driver ufficiale per dispositivi con chipset Atheros (si veda sotto)

Per utilizzare il vecchio driver `ath_pci`, si installi il pacchetto [madwifi](https://www.archlinux.org/packages/?name=madwifi) ed opzionalmente [madwifi-utils-svn](https://aur.archlinux.org/packages/madwifi-utils-svn/). Poi:

```
# modprobe ath_pci

```

Se si sta utilizzando questo driver, potrebbe essere necessario mettere in blacklist `ath5k`. Si veda [Kernel modules (Italiano)#Blacklist](/index.php/Kernel_modules_(Italiano)#Blacklist "Kernel modules (Italiano)") per ulteriori informazioni.

Alcuni utenti potrebbero dover specificare l'opzione `countrycode` al caricamento del driver MadWifi, al fine di scegliere canali e potenza di trasmissione legali nel paese di appartenenza. Se ad esempio ci si trova nei paesi bassi, il modulo andrà caricato in questo modo:

```
# modprobe ath_pci countrycode=528

```

Si possono verificare le impostazioni con il comando {{ic|iwlist}. Si veda [iwlist(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/iwlist.8) e la [pagina](http://madwifi-project.org/wiki/UserDocs/CountryCode) relativa ai CountryCode sul wiki di MadWifi. Per applicare queste impostazioni automaticamente al boot, si aggiunga la seguente riga ad `/etc/modprobe.d/modprobe.conf`:

```
options ath_pci countrycode=528

```

Si consulti il [metodo](http://madwifi-project.org/wiki/UserDocs/FirstTimeHowTo) di installazione del progetto MadWifi, se si riscontrano difficoltà dopo la lettura di questo articolo.

##### ath5k

`ath5k` è il driver preferito per i chipset AR5xxx compresi quelli già funzionanti con `madwifi-ng` e per alcuni chipset più datati dei AR5xxx.

Se `ath5k` è in conflitto con `ath_pci` sul proprio sistema, mettere in [blacklist](/index.php/Kernel_modules_(Italiano)#Blacklist "Kernel modules (Italiano)") (e rimuovere con `rmmod` o riavviare) i seguenti driver in `/etc/modprobe.d/modprobe.conf`:

```
ath_hal
ath_pci
ath_rate_amrr
ath_rate_onoe
ath_rate_sample
wlan
wlan_acl
wlan_ccmp
wlan_scan_ap
wlan_scan_sta
wlan_tkip
wlan_wep
wlan_xauth

```

Poi caricare il modulo manualmente con `modprobe ath5k` o riavviare. *wlan0* (o *wlanX*) dovrebbe apparire ed essere pronta all'uso in modalità STA.

Se il dispositivo non è in grado di ottenere un indirizzo IP dopo essere stato avviato, si provi a caricare il modulo con `modprobe ath5k nohwcrypt=1`. Si veda sotto per ulteriori dettagli sul parametro `nohwcrypt`.

Info:

*   [http://wireless.kernel.org/en/users/Drivers/ath5k](http://wireless.kernel.org/en/users/Drivers/ath5k)
*   [http://wiki.debian.org/ath5k](http://wiki.debian.org/ath5k)

**Nota:** Alcuni portatili hanno dei problemi con il led Wireless che lampeggia rosso e blu. Per risolvere questo problema:
```
echo none > "/sys/class/leds/ath5k-phy0::tx/trigger"
echo none > "/sys/class/leds/ath5k-phy0::rx/trigger"

```
Per ricerche alternative consultare [qui](https://bugzilla.redhat.com/show_bug.cgi?id=618232).

**Nota:** Se le pagine vengono caricate molto lentamente su Firefox/Opera/Chromium, oppure se il dispositivo ha problemi nell'ottenere un indirizzo IP, si provi ad utilizzare la crittografia software in luogo di quella hardware:
```
rmmod ath5k
modprobe ath5k nohwcrypt

```

E si riavvii la connessione. Se il problema è risolto, si renda la modifica permanente aggiungendo questa riga al file `/etc/modprobe.d/010-ath5k.conf`:

```
options ath5k nohwcrypt

```
Ulteriori informazioni sulle opzioni di `modprobe` sono disponibili [qui](/index.php/Modprobe_(Italiano)#Opzioni "Modprobe (Italiano)").

##### ath9k

`ath9k` è il driver Atheros ufficialmente supportato per i più recenti chipset 802.11n. Tutti i chip con capacità 802.11n sono supportati, con un throughput massimo di circa 180 Mbps. Per vedere un elenco completo dell'hardware supportato, controllare questa [pagina](http://wireless.kernel.org/en/users/Drivers/ath9k).

Modalità di funzionamento: Station, AP e Adhoc.

`ath9k` è stato incluso nel kernel dal 2.6.27\. Nell'improbabile caso in cui si riscontrino problemi di stabilità, si potrebbe provare a utilizzare il pacchetto [compat-wireless](http://wireless.kernel.org/en/users/Download). Esiste inoltre [ath9k mailing list](https://lists.ath9k.org/mailman/listinfo/ath9k-devel) che fornisce supporto e discussioni relative allo sviluppo.

Info:

*   [http://wireless.kernel.org/en/users/Drivers/ath9k](http://wireless.kernel.org/en/users/Drivers/ath9k)
*   [http://wiki.debian.org/ath9k](http://wiki.debian.org/ath9k)

##### ath9k_htc

`ath9k_htc` è il driver Atheros ufficialmente supportato per i dispositivi USB 802.11n. Sono supportate le modalità "station" e "ad-Hoc". Il driver è stato implementato dal kernel linux 2.6.35\. Per maggiori informazioni si veda [http://wireless.kernel.org/en/users/Drivers/ath9k_htc](http://wireless.kernel.org/en/users/Drivers/ath9k_htc).

#### Intel

##### ipw2100 e ipw2200

Pienamente supportato nel kernel, ma richiede il firmware aggiuntivo. A seconda del chip della propria scheda, utilizzare [ipw2100-fw](https://www.archlinux.org/packages/?name=ipw2100-fw) o [ipw2200-fw](https://www.archlinux.org/packages/?name=ipw2200-fw) e [caricare](/index.php/Kernel_modules_(Italiano)#Caricamento "Kernel modules (Italiano)") il modulo corretto.

**Suggerimento:** È possibile passare i seguenti [parametri](/index.php/Kernel_modules_(Italiano)#Impostazione_delle_opzioni "Kernel modules (Italiano)") ai moduli:

*   `rtap_iface=1` per utilizzare l'interfaccia radiotap
*   `led=1` per abilitare un LED frontale che indica lo stato della connessione

##### iwl3945, iwl4965 e serie-iwl5000

Il progetto [Intel iwlwifi](http://intellinuxwireless.org/?p=iwlwifi) (con iwl che sta per **I**ntel's open source **W**iFi drivers for **L**inux) fornisce dei driver, direttamente inclusi nei kernel 2.6.24 e successivi, che funzionano per entrambi i chipset 3945 e 4965\. Inoltre, la serie di schede iwl5000 (che include i chipset 5100BG, 5100ABG, 5100AGN, 5300AGN and 5350AGN) è supportata con un modulo nel nuovo kernel 2.6.27, grazie al driver **iwlagn**.

###### Caricamento del Driver

[udev](/index.php/Udev_(Italiano) "Udev (Italiano)") dovrebbe caricare il driver automaticamente. In caso contrario si carichino i moduli `iwl3945` o `iwl4965` manualmente. Si consulti [Kernel modules (Italiano)#Caricamento](/index.php/Kernel_modules_(Italiano)#Caricamento "Kernel modules (Italiano)") per ulteriori informazioni.

###### Disattivazione del lampeggio dei LED

Le impostazioni predefinite del modulo attivano il lampeggio del LED di default. Alcune persone trovano questo fatto estremamente fastidioso. Per avere il LED acceso se wifi è attivo (funziona anche su sistemi che non utilizzano systemd):

```
# echo 'w /sys/class/leds/phy0-led/trigger - - - - phy0radio' > /etc/tmpfiles.d/phy0-led.conf
# systemd-tmpfiles --create phy0-led.conf

```

Se non si dispone di `/sys/class/leds/py0-led`:

```
# echo "options iwlcore led_mode=1" >> /etc/modprobe.d/modprobe.conf
# rmmod iwlagn
# rmmod iwlcore
# modprobe iwlcore
# modprobe iwlagn

```

Dal kernel 2.6.39.1-1 in poi, il modulo `iwlcore` module è deprecato. Usare piuttosto `options iwlagn led_mode=1` o `options iwl_legacy led_mode=1` (capire quale modulo viene caricato con `lsmod`).

**Nota:** `iwl_legacy` è stato rinominato in `iwlegacy` a partire dalla versione 3.3.1 del kernel linux: sarà quindi necessario utilizzare: `options iwlegacy led_mode=1`.

##### Altre osservazioni

*   Di default `iwl3945` è configurato per funzionare solo con le reti sui canali 1-11\. Gamme superiori non sono ammesse in alcune parti del mondo (Stati Uniti). Nell'UE tuttavia, i canali 12 e 13 sono utilizzati abbastanza comunemente. Per fare in modo che `iwl3945` esegua le scansioni per tutti i canali, aggiungere `options cfg80211 ieee80211_regdom=EU` a `/etc/modprobe.d/modprobe.conf`. Con `iwlist f` è possibile controllare quali canali sono ammessi.
*   Se si desidera attivare più canali su Intel Wifi 5100 (e possibilmente anche altre schede) è possibile farlo con il pacchetto `crda`. Dopo l'installazione, modificare `/etc/conf.d/wireless-regdom` e decommentare la riga in cui si trova il codice del paese. Aggiungere `wireless-regdom` alla stringa `DAEMONS` in `/etc/rc.conf` e riavviare (che è la cosa più facile da fare). Si dovrebbe ora, dopo aver dato il comando `sudo iwlist wlan0 channel`, avere accesso a più canali (a seconda della propria località).

#### Broadcom

Si veda [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless").

#### Altri drivers/dispositivi

##### w322u

Per questa scheda Tenda, avvalersi delle istruzioni riguardanti `rt2870sta`. Consultare: [Rt2870](/index.php/Rt2870 "Rt2870")

##### orinoco

Questo driver fa già parte del pacchetto del kernel e quindi dovrebbe già essere installato.

**Nota:** Alcuni chipset orinoco sono Hermes I/II. È possibile installare il pacchetto [wl_lkm](https://aur.archlinux.org/packages/wl_lkm/) da AUR per sostituire il driver `orinoco` ed ottenere il supporto WPA. Consultare [questo post](http://ubuntuforums.org/showthread.php?p=2154534#post2154534) per ulteriori informazioni.

Per utilizzare il driver, mettere in [blacklist](/index.php/Kernel_modules_(Italiano)#Blacklist "Kernel modules (Italiano)") `orinoco_cs` e poi aggiungere `wlags49_h1_cs`.

##### prism54

Scaricate il firmware del driver appropriato per la vostra scheda da [questo sito](http://linuxwireless.org/en/users/Drivers/p54). Rinominate poi il file in `isl3890`. Se non esiste, sarà necessario creare la cartella `/lib/firmware` e spostare li dentro il firmware appena rinominato. Questo procedimento dovrebbe funzionare. [[3]](https://bbs.archlinux.org/viewtopic.php?t=16569&start=0&postdays=0&postorder=asc&highlight=siocsifflags+such+file++directory)

Se così non funziona, riprovare in questo modo:

*   Ricaricare il modulo prism (`modprobe p54usb` o `modprobe p54pci`, dipendendo dal proprio hardware)

in alternativa, rimuovere la scheda wifi e poi ricollegarla.

*   Usare il comando `dmesg`, e osservare verso la fine dell'output restituito.

Cercare una sezione simile a questa:

```
firmware: requesting **isl3887usb_bare**
p54: LM86 firmware
p54: FW rev 2.5.8.0 - Softmac protocol 3.0

```

e provare a rinominare il file del firmware con il nome corrispondente alla parte in grassetto qui.

Se si riceve il messaggio

```
SIOCSIFFLAGS: Operation not permitted

```

durante l'esecuzione di `ip link set wlan0 up`, oppure si visualizza

```
prism54: Your card/socket may be faulty, or IRQ line too busy :(

```

in `dmesg`, la causa può essere il caricamento simultaneo del vecchio modulo del kernel `prism54` e dei più recenti `p54pci` o `p54usb`, e quindi in contrapposizione tra loro per aggiudicarsi l'IRQ. Utilizzare il comando `lsmod` per vedere se viene effettivamente caricato il modulo deprecato, nel qual caso bisognerà bloccarne il caricamento aggiungendolo in [blacklist](/index.php/Kernel_modules_(Italiano)#Blacklist "Kernel modules (Italiano)"). Ci sono diversi modi per farlo, descritti in altre sezioni del wiki. Una volta aggiunto alla blacklist, si dovrà probabilmente rinominare il firmware `prism54` e `p54pci`/`p54usb` a seconda dei differenti nomi dei file firmware (ricontrollare `dmesg` dopo aver eseguito `ip link set eth0 up`).

##### ACX100/111

Installate innanzitutto i pacchetti: `tiacx` `tiacx-firmware`

Il driver dovrebbe dirvi di quale firmware ha bisogno: controllate `/var/log/messages.log` oppure usate il comando `dmesg`.

Spostate quindi il firmware corretto nella cartella `/lib/firmware`:

```
ln -s /usr/share/tiacx/acx111_2.3.1.31/tiacx111c16 /lib/firmware

```

Un altro modo di determinare quale numero di revisione del firmware utilizzare, è vedere la sezione ["Which firmware"](http://acx100.sourceforge.net/wiki/Firmware) del wiki acx100.sourceforge. Per ACX100, è possibile seguire i link forniti, e convergenti ad una tabella di modelli di schede. "firmware noto per funzionare"; si può capire il numero rev. di cui si ha bisogno, guardando il suffisso. Es. una dlink_dwl650+ usa "1.9.8.b", nel qual caso si farebbe questo:

```
ln -s /usr/share/tiacx/acx100_1.9.8.b/* /usr/lib/firmware

```

Se pensate che questo driver riempia di messaggi inutili il vostro kernel log, ad esempio se state utilizzando Kismet con il channel-hopping, potete mettere questa opzione nel file `/etc/modprobe.d/modprobe.conf`:

```
options acx debug=0

```

**Nota:** Il driver open-source `acx` non supporta la criptazione WPA/RSN. Ndiswrapper dovrà essere utilizzato con il driver di Windows per abilitare la crittografia avanzata. Vedere ndiswrapper per maggiori informazioni.

##### zd1211rw

[`**zd1211rw**`](http://zd1211.wiki.sourceforge.net/) è il driver per il chipset ZyDAS ZD1211 802.11b/g USB WLAN ed è incluso nelle recenti versioni del kernel Linux. Vedere [[4]](http://www.linuxwireless.org/en/users/Drivers/zd1211rw/devices) per una lista delle schede supportate. Avrete solo bisogno di installare il firmware appropriato per la scheda, contenuto nel pacchetto [zd1211-firmware](https://www.archlinux.org/packages/?name=zd1211-firmware).

##### carl9170

[`**carl9170**`](http://wireless.kernel.org/en/users/Drivers/carl9170/) è il driver USB 802.11n con firmware GPLv2 per i dispositivi Atheros USB AR9170\. Supporta questi [dispositivi](http://wireless.kernel.org/en/users/Drivers/carl9170#available_devices). Il **firmware** non è ancora incluso nel pacchetto `linux-firmware`, ma è disponibile su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") ([carl9170-fw](https://aur.archlinux.org/packages/carl9170-fw/)). Il driver è incluso nel kernel dalla versione 2.6.37.

E' inoltre necessario inserire in [blacklist](/index.php/Kernel_modules_(Italiano)#Blacklist "Kernel modules (Italiano)") i seguenti moduli:

*   `arusb_lnx`
*   `ar9170usb`

##### hostap_cs

Host AP è il driver Linux per schede wireless con chipset Prism2/2.5/3 come WCP11\. `hostap_cs` dovrebbe essere incluso nel pacchetto `linux` e quindi già installato.

`orinico_cs` può causare problemi, quindi deve essere aggiunto in [blacklist](/index.php/Kernel_modules_(Italiano)#Blacklist "Kernel modules (Italiano)"). Dopodichè il driver dovrebbe funzionare.

Ulteriori informazioni sul driver possono essere trovate [qui](http://hostap.epitest.fi/).

#### ndiswrapper

Ndiswrapper è un wrapper che permette di utilizzare alcuni dei driver di Windows sotto Linux. L'elenco dei dispositivi supportati è reperibile [qui](http://ndiswrapper.sourceforge.net/mediawiki/index.php/List). Saranno necessari i files `.inf` e `.sys` del driver di Windows. Assicurarsi di scegliere il driver adatto all'architettura in uso (`x86` o `x86_64`).

**Suggerimento:** Se si ha la necessità di estrarre questi files da un `.exe`, è possibile utilizzare [cabextract](https://www.archlinux.org/packages/?name=cabextract).

Per installare ndiswrapper è necessario seguire questi passi:

1\. Installare i driver in `/etc/ndiswrapper/*`

```
ndiswrapper -i filename.inf

```

2\. Elencare tutti i driver installati per ndiswrapper

```
ndiswrapper -l

```

3\. Scrivere i file di configurazione in `/etc/modprobe.d/ndiswrapper.conf`

```
ndiswrapper -m
depmod -a

```

Ora che l'installazione di ndiswrapper è quasi finita, si segua [Kernel modules (Italiano)#Caricamento](/index.php/Kernel_modules_(Italiano)#Caricamento "Kernel modules (Italiano)") per caricare automaticamente il modulo al boot.

L'importante è semplicemente che ndiswrapper sia presente nella lista dei moduli da caricare. Salvato il file, sarà utile (per non dover riavviare subito) caricare manualmente il modulo con il comando:

```
modprobe ndiswrapper
iwconfig

```

dovremmo vedere presente il device *wlan0*. Se avete problemi, consultate il [wiki d'installazione Ndiswrapper](http://ndiswrapper.sourceforge.net/joomla/index.php?/component/option,com_openwiki/Itemid,33/id,installation/).

#### compat-drivers-patched

Il pacchetto "compat-drivers-patched" corregge il problema del "canale fisso -1", fornendo al contempo una migliore funzionalità. Installare il pacchetto [compat-drivers-patched](https://aur.archlinux.org/packages/compat-drivers-patched/) da AUR.

[compat-wireless-patched](https://aur.archlinux.org/packages/compat-wireless-patched/) non va in conflitto con nessun altro pacchetto e i moduli compilati risiedono in `/usr/lib/modules/*versione-kernel*/updates`.

Questi driver con patch incluse provengono da [Linux Wireless project](http://wireless.kernel.org/) e supportano molti dei chip menzionati sopra, tra i quali:

```
ath5k ath9k_htc carl9170 b43 zd1211rw rt2x00 wl1251 wl12xx ath6kl brcm80211

```

Gruppi supportati:

```
atheros ath iwlagn rtl818x rtlwifi wl12xx atlxx bt

```

È anche possibile compilare un modulo o driver specifico appartenente ad un gruppo di driver modificando il [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), decommentando la **riga #46**. Ecco un esempio di compilazione del gruppo Atheros:

```
scripts/driver-select atheros

```

Leggere accuratamente le istruzioni del [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") per qualsiasi altre possibile modifica prima della compilazione e installazione.

#### Link utili

*   [Il metodo per installare MadWifi secondo i suoi autori](http://madwifi-project.org/wiki/UserDocs/FirstTimeHowTo), utile se avete problemi ad installarlo tramite il metodo-Arch