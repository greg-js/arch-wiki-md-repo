| **Summary**  |
| Una guida per l'installazione e la configurazione di netcfg, gli script e il profilo di configurazione della rete. |
| **Overview** |
| Arch Linux fornisce due opzioni per l'amministrazione della rete: [*network*](/index.php/Configuring_Network "Configuring Network") e *[netcfg](/index.php/Netcfg "Netcfg")*. Il demone *network* è una semplice e lineare soluzione per desktop e server cablati. La navigazione tramite [Wireless](/index.php/Wireless_Setup "Wireless Setup") richiede una configurazione ulteriore. Lo script *netcfg* fornisce il supporto roaming per utenti mobili e facilita la gestione dei profili di rete; [NetworkManager](/index.php/NetworkManager "NetworkManager") e [Wicd](/index.php/Wicd "Wicd") sono due popolari alternative. |
| **Resources** |
| [netcfg network scripts repository](https://projects.archlinux.org/netcfg.git/) |

Dalla pagina [netcfg man](https://projects.archlinux.org/netcfg.git/tree/man/netcfg.8):

	***netcfg** viene utilizzato per configurare e gestire le connessioni di rete tramite profili. Ha il supporto plugin per vari tipi di connessione, come il wireless, Ethernet, e ppp. È anche in grado di avviare/arrestare molte connessioni in una, cioè può gestire connessioni multiple all'interno dello stesso profilo, opzionalmente anche con il "bonding".*

netcfg è utile a quegli utenti che cercano un mezzo semplice e robusto per gestire configurazioni di rete multiple (ad esempio gli utenti laptop). Per i sistemi che solitamente si connettono ad una rete unica, il demone [network](/index.php/Network "Network") potrebbe essere più adatto.

**Nota:** Con la versione netcfg-2.8.9 si è interrotta la compatibilità con il file rc.conf. Gli utenti di netcfg dovranno configurare tutte le interfacce nel file `/etc/conf.d/netcfg` invece che in `/etc/rc.conf`.

## Contents

*   [1 Preparazione](#Preparazione)
*   [2 Installazione](#Installazione)
*   [3 Configurazione](#Configurazione)
*   [4 Uso](#Uso)
*   [5 Connessione automatica](#Connessione_automatica)
    *   [5.1 net-profiles](#net-profiles)
    *   [5.2 net-auto-wireless](#net-auto-wireless)
    *   [5.3 net-auto-wired](#net-auto-wired)
    *   [5.4 Supporto a systemd](#Supporto_a_systemd)
*   [6 Suggerimenti utili](#Suggerimenti_utili)
    *   [6.1 Passare argomenti a iwconfig prima di connettersi](#Passare_argomenti_a_iwconfig_prima_di_connettersi)
    *   [6.2 rfkill (abilita/disabilita il wireless)](#rfkill_.28abilita.2Fdisabilita_il_wireless.29)
    *   [6.3 Eseguire comandi prima o dopo che l'interfaccia sia accesa o spenta](#Eseguire_comandi_prima_o_dopo_che_l.27interfaccia_sia_accesa_o_spenta)
    *   [6.4 Errore di connessione intermittente](#Errore_di_connessione_intermittente)
    *   [6.5 Configurazione tramite interfaccia](#Configurazione_tramite_interfaccia)
    *   [6.6 Output hooks](#Output_hooks)
    *   [6.7 ArchAssitant (GUI)](#ArchAssitant_.28GUI.29)
    *   [6.8 Netcfg Easy Wireless LAN (newlan)](#Netcfg_Easy_Wireless_LAN_.28newlan.29)
    *   [6.9 wifi-select](#wifi-select)
    *   [6.10 Passaggio di argomenti a dhcpcd](#Passaggio_di_argomenti_a_dhcpcd)
        *   [6.10.1 Accelerare il DHCP mediante dhcpcd](#Accelerare_il_DHCP_mediante_dhcpcd)
    *   [6.11 Uso di dhclient al posto di dhcpcd](#Uso_di_dhclient_al_posto_di_dhcpcd)
    *   [6.12 Configurare un bridge da usare con macchine virtuali (VMs)](#Configurare_un_bridge_da_usare_con_macchine_virtuali_.28VMs.29)
    *   [6.13 Aggiungere più indirizzi IP ad un'interfaccia](#Aggiungere_pi.C3.B9_indirizzi_IP_ad_un.27interfaccia)
    *   [6.14 Aggiungere indirizzamenti statici](#Aggiungere_indirizzamenti_statici)
        *   [6.14.1 Tethering Bluetooth via *pand*](#Tethering_Bluetooth_via_pand)
*   [7 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [7.1 Debugging](#Debugging)
    *   [7.2 Rete non disponibile](#Rete_non_disponibile)
    *   [7.3 Associazione wireless non riuscita](#Associazione_wireless_non_riuscita)
    *   [7.4 Impossibile ottenere l'indirizzo IP con DHCP](#Impossibile_ottenere_l.27indirizzo_IP_con_DHCP)
    *   [7.5 Connessione non valida, controllo ortografico o guardare gli esempi](#Connessione_non_valida.2C_controllo_ortografico_o_guardare_gli_esempi)
    *   [7.6 Nessuna connessione](#Nessuna_connessione)
        *   [7.6.1 Carrier Timeout](#Carrier_Timeout)
        *   [7.6.2 Skip no carrier](#Skip_no_carrier)
    *   [7.7 Driver quirks](#Driver_quirks)
    *   [7.8 Ralink legacy driver rt2500, rt2400 usando iwpriv](#Ralink_legacy_driver_rt2500.2C_rt2400_usando_iwpriv)
    *   [7.9 Nel caso di: "/var/run/network//suspend/": No such file or directory](#Nel_caso_di:_.22.2Fvar.2Frun.2Fnetwork.2F.2Fsuspend.2F.22:_No_such_file_or_directory)
    *   [7.10 Ancora non funziona, che cosa devo fare?](#Ancora_non_funziona.2C_che_cosa_devo_fare.3F)
*   [8 Domande frequenti](#Domande_frequenti)
    *   [8.1 Perchè netcfg non fa *(alcune cose)*?](#Perch.C3.A8_netcfg_non_fa_.28alcune_cose.29.3F)
    *   [8.2 Perchè netcfg non si comporta in *questo* modo?](#Perch.C3.A8_netcfg_non_si_comporta_in_questo_modo.3F)
    *   [8.3 Ho ancora bisogno di *(qualche cosa)* se sto utilizzando netcfg?](#Ho_ancora_bisogno_di_.28qualche_cosa.29_se_sto_utilizzando_netcfg.3F)

## Preparazione

Nei casi più semplici, gli utenti devono conoscere solamente il nome della/e loro interfaccia/e di rete (es. **eth0**, **wlan0**). Per la configurazione di indirizzi IP statici, bisogna conoscere anche i gateway e i nomi degli indirizzi dei server.

Per la connessione ad una rete wireless, tenere a portata di mano alcune informazioni di base, ossia quale tipo di protezione viene utilizzato, il nome della rete (ESSID), e le eventuali password o chiavi di crittografia. Assicurarsi inoltre che il driver e il firmware corretti siano installati sul proprio dispositivo wireless, come descritto nella sezione [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

## Installazione

Assicurarsi di avere l'ultima versione di netcfg installato. Le versioni più datate sono più soggette a bug e potrebbero non funzionare bene con i driver più recenti. Il pacchetto [netcfg](https://aur.archlinux.org/packages/netcfg/) è disponibile nei [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)"):

```
# pacman -S netcfg

```

Dalla versione 2.5.x, le dipendenze opzionali includono [wpa_actiond](https://www.archlinux.org/packages/?name=wpa_actiond), richiesto per il roaming automatico delle connessioni wireless, e [ifplugd](https://www.archlinux.org/packages/?name=ifplugd), richiesto per la configurazione automatica Ethernet. ([Ulteriori informazioni](https://www.archlinux.org/news/487/))

```
# pacman -S wpa_actiond ifplugd

```

Se sia necessario avere un perfezionamento del supporto [Bash](/index.php/Bash "Bash") di netcfg, installare il pacchetto [bash-completion](https://www.archlinux.org/packages/?name=bash-completion) dai repository ufficiali.

## Configurazione

I profili di rete sono memorizzati nella cartella `/etc/network.d`. Per ridurre al minimo il rischio di errori, copiare una configurazione d'esempio da `/etc/network.d/examples/` a `/etc/network.d/mynetwork`. Il nome del file è il nome del profilo di rete ("mynetwork" è usato come esempio in questo articolo). Il nome non è una configurazione di rete e non deve necessariamente corrispondere al nome della rete wireless (SSID).

A seconda del tipo di connessione e livello di sicurezza, utilizzare uno dei seguenti esempi da `/etc/network.d/examples` come base. Diffidate dagli esempi trovati su Internet in quanto contengono spesso opzioni deprecate che possono causare problemi.

| Connessione tipo/sicurezza | Esempio di profile |
| Wireless; WEP hex key | `wireless-wep` |
| Wireless; WEP string key | `wireless-wep-string-key` |
| Wireless; WPA-Personal (passphrase/pre-shared key) | `wireless-wpa` |
| Wireless; WPA-Enterprise | `wireless-wpa-config` (wpa_supplicant configurazione esterna)
`wireless-wpa-configsection` (wpa_supplicant configurazione salvata su stringa) |
| Cavo; DHCP | `ethernet-dhcp` |
| Cavo; IP statico | `ethernet-static` |
| Cavo; Configurazione iproute | `ethernet-iproute` |

Successivamente, modificare il nuovo file di configurazione, `/etc/network.d/mynetwork`:

*   Impostare `INTERFACE` per l'interfaccia corretta, wireless o Ethernet. Questo può essere controllato con `ifconfig` e `iwconfig`.
*   Assicurarsi che `ESSID` e `KEY` (passphrase) siano impostate correttamente per le connessioni wireless. I caratteri errati in questi campi sono gli errori più comuni.
    *   Notare che le WEP keys *string* (non *hex*) devono essere specificate con all'inizio una `s:` (es. `KEY="s:somepasskey"`).

**Note:** Le configurazioni di Netcfg sono degli script Bash validi. Qualsiasi configurazione che coinvolge caratteri speciali come `$` o `\` deve essere quotata correttamente altrimenti verrà interpretata da Bash. Per evitare che questo si verifichi, usare le virgolette singole o i caratteri di escape backslash, in caso.

**Note:** Le informazioni di connessione (es. wireless passkey) verranno memorizzate in formato testo normale, quindi gli utenti potrebbero preferire cambiare i permessi sul profilo appena creato (es. `chmod 0600 /etc/network.d/mynetwork` per renderlo leggibile solo da root).

**Note:** Per WPA-Personali, è anche possibile usare la chiave di cifratura WPA codificata in una stringa esadecimale, invece che una chiave in testo normale.

Seguire la procedura del [primo esempio alla pagina di WPA supplicant](/index.php/Wpa_supplicant#Classic_method:_.2Fetc.2Fwpa_supplicant.conf "Wpa supplicant") per generare una stringa esadecimale a partire dalla tua chiave WPA.
Salvare la nuova stringa esadecimale nel proprio profilo WPA nel file `/etc/network.d/mynetwork` come valore della variabile `KEY` (assicurarsi che questa sia la sola variabile `KEY` abilitata), per assomigliare a questa (sostituite la stringa con la vostra):

```
KEY='7b271c9a7c8a6ac07d12403a1f0792d7d92b5957ff8dfd56481ced43ec6a6515'

```

Che dovrebbe farlo, senza la necessità di rivelare la chiave di accesso.

## Uso

Per connettere un profilo:

```
# netcfg mynetwork

```

Per disconnettere un profilo:

```
# netcfg down <profile-name>

```

Se stabilita la connessione con successo, gli utenti possono configurare netcfg per la connessione automatica o durante l'avvio. Se la connessione non riesce, consultare [#Risoluzione dei problemi](#Risoluzione_dei_problemi) per possibili soluzioni o su come ottenere aiuto.

Per altre funzioni, vedere:

```
$ netcfg help

```

## Connessione automatica

Sono disponibili diversi metodi per coloro che desiderano connettere automaticamente i profili di rete (ad esempio durante l'avvio o in roaming). Si noti che un profilo di rete deve essere *prima* configurato correttamente nella cartella `/etc/network.d` (consultare [#Configurazione](#Configurazione)).

**Tip:** Se si abilita uno dei seguenti demoni e non sono state eseguite configurazioni nella stringa `INTERFACES` in `/etc/rc.conf`, si può rimuovere il demone `network` dalla stringa `DAEMONS`. Se si montano condivisioni [NFS](/index.php/NFS_(Italiano) "NFS (Italiano)") durante l'avvio, assicurarsi che il demone `netfs` sia comunque specificato (altrimenti la rete verrà abbandonata prima dello smontaggio delle condivisioni durante l'arresto).

### net-profiles

**I `net-profiles` permettono di collegare i profili durante l'avvio.**

Per attivare questa funzione bisogna aggiungere `net-profiles` alla stringa `DAEMONS` in `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")` e specificare i profili da connettere nella stringa `NETWORKS` in `/etc/conf.d/netcfg`:

 `/etc/rc.conf` 
```
DAEMONS=(... net-profiles ...)

```
 `/etc/conf.d/netcfg` 
```
NETWORKS=(mynetwork yournetwork)

```

Un profilo network può anche essere avviato in background aggiungendone il prefisso `@` nella stringa`NETWORKS`. Notare che questo si dovrebbe fare solamente se i profili in background configurino interfacce distinte, altrimenti si potrebbero verificare delle incongruenze.

 `/etc/conf.d/netcfg` 
```
NETWORKS=(@mynetwork @yournetwork)

```

Alternativamente, i `net-profiles` possono essere configurati in modo da ripristinare i profili attivi all'ultimo spegnimento della macchina impostando la stringa `NETWORKS` a `last`, come descritto in seguito.

 `/etc/conf.d/netcfg` 
```
NETWORKS=(last)

```

Infine, i `net-profiles` si possono configurare per mostrare un menu – permettendo agli utenti di scegliere il profilo desiderato – impostando il contenuto della stringa `NETWORKS` a `menu`:

 `/etc/conf.d/netcfg` 
```
NETWORKS=(menu)

```

È richiesto inoltre il pacchetto [dialog](https://www.archlinux.org/packages/?name=dialog).

**Tip:** Accedere al menu in qualsiasi momento eseguendo `netcfg-menu` in un terminale.

### net-auto-wireless

**`net-auto-wireless` consente agli utenti di connettersi automaticamente alle reti wireless con un'adeguato supporto al roaming.**

Per attivare questa funzione, si deve aggiungere `net-auto-wireless` alla stringa `DAEMONS` in `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")`:

 `/etc/rc.conf` 
```
DAEMONS=(... net-auto-wireless ...)

```

e specificare l'interfaccia wireless desiderata nella variabile `WIRELESS_INTERFACE` in `/etc/conf.d/netcfg`:

 `/etc/conf.d/netcfg` 
```
WIRELESS_INTERFACE="wlan0"

```

È inoltre possibile definire una lista delle reti wireless che dovrebbe automaticamente connettersi con la variabile `AUTO_PROFILES` in `/etc/conf.d/netcfg`. Se `AUTO_PROFILES` non è settato, verrà tentata la connessione ad ogni rete wireless.

È richiesto inoltre il pacchetto [wpa_actiond](https://www.archlinux.org/packages/?name=wpa_actiond). Si noti che i profili wpa-config non funzionano con net-auto-wireless. Convertirli perciò in WPA-configsection.

### net-auto-wired

**`net-auto-wired` consente agli utenti di connettersi automaticamente alle reti cablate.**

Per attivare questa funzione, bisogna prima [installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") [ifplugd](https://www.archlinux.org/packages/?name=ifplugd), poi aggiungere `net-auto-wired` alla stringa `DAEMONS` in `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")` e specificare l'interfaccia cablata desiderata nella variabile in `/etc/conf.d/netcfg`:

 `/etc/rc.conf` 
```
DAEMONS=(... net-auto-wired ...)

```
 `/etc/conf.d/netcfg` 
```
WIRED_INTERFACE="eth0"

```

Il demone avvia un processo ifplugd che esegue `/etc/ifplugd/netcfg.action` quando lo stato dell'interfaccia cablata cambia (per esempio quando un cavo è collegato o scollegato). Collegando un cavo, vengono tentati gli avvii di qualsiasi profilo, come `CONNECTION = "ethernet"` o `"ethernet-iproute"` e `INTERFACE = WIRED_INTERFACE`, finchè uno di questi viene eseguito con successo.

**Note:** I profili DHCP vengono provati prima di quelli statici, il che potrebbe portare, in alcuni casi, a risultati indesiderati.

**Note:** Il demone net-auto-wired non può avviare processi multipli ifplugd per interfacce multiple (come invece ifplugd `/etc/rc.d/ifplugd`).

### Supporto a systemd

Dalla versione 2.8.2 [netcfg](https://aur.archlinux.org/packages/netcfg/) fornisce i file *unit* di systemd. I file *service* `net-auto-wireless.service` e `net-auto-wired.service` corrispondono ai demoni `/etc/rc.d/net-auto-wireless` e `/etc/rc.d/net-auto-wired` di [initscripts](https://www.archlinux.org/packages/?name=initscripts) . Per connettere più profili al boot si può usare `netcfg.service` che è equivalente a `/etc/rc.d/net-profiles` e avviare tutti i profili specificati nella stringa `NETWORKS` in `/etc/conf.d/netcfg`. Questi file *service* possono essere abilitati ed avviati con `systemctl` come di consueto.

In alternatica si può usare il file *template service* `netcfg@.service` che permette di connettersi ai profili al boot senza doverlo specificare in `/etc/conf.d/netcfg`. Per definire il profilo desiderato, abilitare il *template service* e usare il nome del profilo di rete da invocare:

```
# systemctl enable netcfg@<profile-name>.service

```

## Suggerimenti utili

### Passare argomenti a iwconfig prima di connettersi

È sufficiente aggiungere ad un profilo le seguenti:

```
IWCONFIG="<arguments>"

```

Dove `<arguments>` può essere qualsiasi argomento `iwconfig` valido. Lo script poi eseguirà `iwconfig $INTERFACE $IWCONFIG`.

Ad esempio, forzare la scheda a registrare uno specifico punto di accesso dato dall'indirizzo MAC:

```
IWCONFIG="ap 12:34:56:78:90:12"

```

Questo sostituisce le opzioni `IWOPTS` e `WEP_OPTS` che non erano implementate completamente.

### rfkill (abilita/disabilita il wireless)

Netcfg può abilitare/disabilitare l'emissione radio delle schede wireless dotate di software di controllo di tale funzionalità. Per le schede wireless con controlli hardware, netcfg può rilevarne l'eventuale stato di spegnimento o disabilitazione, che talvolta può dare luogo ad errori.

Per abilitare il supporto rfkill, è necessario specificare qual'è il tipo di controllo switch dell'interfaccia wireless, cioè se hardware o software. Questo può essere impostato all'interno di un profilo o a livello di interfaccia (`/etc/network.d/interfaces/$INTERFACE`; consultare [#Configurazione tramite interfaccia](#Configurazione_tramite_interfaccia)).

```
RFKILL=soft # può essere sia 'hard' che 'soft'

```

Per alcuni "kill switch" la voce rfkill in `/sys` non è puntata sull'interfaccia e la variabile `RFKILL_NAME` deve essere impostata con il contenuto del corrispondente `/sys/class/rfkill/rfkill#/name`.

Per esempio, su un Eee PC:

```
RFKILL=soft
RFKILL_NAME='eeepc-wlan'

```

On a mid-2011 Thinkpad:

```
RFKILL=hard
RFKILL_NAME='phy0'

```

**Note:** Il demone `net-auto-wireless` richiede un'interfaccia di configurazione a livello di rfkill altrimenti non verrà eseguito.

**Attenzione:** Alcuni dispositivi (almeno alcune schede SiS) possono creare voci a `/sys/class/rfkill/rfkill#` con nomi differenti per ogni switch. Qualcosa come ciò che segue potrà funzionare in tali casi (soluzione solo per il Wifi!): `/etc/network.d/interfaces/wlan0` 
```
RFKILL=hard
RFKILL_NAME=`cat /sys/class/rfkill/rfkill*/name 2> /dev/null || echo ""`
```

### Eseguire comandi prima o dopo che l'interfaccia sia accesa o spenta

Se l'interfaccia richiede azioni speciali prima o dopo l'accesso o abbandono di una connessione, è possibile utilizzare le variabili `PRE_UP`, `POST_UP`, `PRE_DOWN`, and `POST_DOWN`.

Ad esempio, se si desidera configurare la scheda wireless per funzionare in modalità ad-hoc, ma si può cambiare la modalità solo quando l'interfaccia è spenta, si potrebbe usare qualcosa di simile:

```
PRE_UP="ifconfig wlan0 down; iwconfig wlan0 mode ad-hoc"

```

Oppure, per il montaggio delle condivisioni di rete a connessione avvenuta, è possibile utilizzare:

```
POST_UP="sleep 5; mount /mnt/shares/nexus/utorrent 2>/dev/null"

```

A volte potrebbe essere utile poter eseguire qualcosa da netcfg con un altro utente:

```
POST_UP="su -c '/you/own/command' username"

```

**Note:** Se i comandi specificati restituiscono qualcosa diverso da 0 (successo), netcfg interrompe l'operazione corrente. Quindi, se si vuole montare una condivisione di rete che potrebbe non essere disponibile al momento della connessione (restituendo un errore), è possibile creare uno script [Bash](/index.php/Bash "Bash") separato con i comandi per il montaggio e un `exit 0` alla fine. In alternativa si può aggiungere `|| true` alla fine del comando che potrebbe restituire l'errore.

**Note:** Il contenuto di queste variabili viene valutato con una dichiarazione `eval`. Le variabili profili ed interfaccia come `ESSID` sono disponibili all'uso, ma deve essere evitato in modo che la loro valutazione sia rinviata all'eval. Il modo più semplice per far questo è di usare apici singoli. Per esempio: `PRE_UP='echo $ESSID >/tmp/essid'` valuterà correttamente, indipendentemente da dove sia il comando `PRE_UP`.

### Errore di connessione intermittente

Alcune combinazioni driver+hardware possono talvolta interrompere la sincronizzazione. Usare i comandi pre e post per aggiungere/rimuovere il driver e utilizzare uno script come il seguente per aggiustare la connessione corrente:

 `/usr/local/bin/netcfgd` 
```
#!/bin/bash
log() { logger -t "$( basename $0 )" "$*" ; }

main() {
        local host
        while sleep 1; do
                [[ "$( netcfg current )" = "" ]] && continue

                host=$( route -n | awk '/^0.0.0.0/ { print $2 }' )
                ping -c 1 $host && continue

                log "trying to reassociate"
                wpa_cli reassociate
                ping -c 1 $host && continue

                log "reassociate failed, reconfiguring network"
                netcfg -r $( netcfg current )
        done
}

exec 1>/dev/null
[[ $EUID != 0 ]] && { log "must be root"; exit 1; }

for cmd in wpa_cli ping netcfg; do
        ! which $cmd && {
                log "can't find command ${cmd}, exiting..."
                exit 1
        }
done

log 'starting...'
main 

```

### Configurazione tramite interfaccia

Le opzioni di configurazione che si applicano a tutti i profili utilizzando un'interfaccia possono essere impostate con `/etc/network.d/interfaces/$INTERFACE`. Per esempio:

```
/etc/network.d/interfaces/wlan0

```

Può risultare utile per le opzioni `wpa_supplicant`, il supporto switch rfkill, gli script pre/post up/down e `net-auto-wireless`. Queste opzioni vengono caricate *prima* dei profili in modo che tutte le opzioni basate sui profili abbiano la priorità.

`/etc/network.d/interfaces/$INTERFACE` può contenere qualsiasi opzione di profilo valida, anche se è più probabile l'uso di `PRE_UP`/`DOWN` e `POST_UP`/`DOWN` (descritto nella sezione precedente) o una delle opzioni elencate di seguito. Ricordarsi che queste opzioni sono impostate per *tutti* i profili che usano l'interfaccia; ad esempio, se non si desidera effettuare la connessione VPN del proprio ufficio, tenerlo presente, perchè cercherà comunque di connettersi ad *ogni* connessione wireless!

```
WPA_GROUP   - Imposta il gruppo dell'interfaccia wpa_ctrl
WPA_COUNTRY - Impone limiti di regolazione locale e permette l'uso di più canali
WPA_DRIVER  - Di default è wext, può essere utile nl80211 per dispositivi mac80211 

```

**Note:** `POST_UP`/`POST_DOWN` richiede il pacchetto [wpa_actiond](https://www.archlinux.org/packages/?name=wpa_actiond).

### Output hooks

netcfg ha un supporto limitato per caricare gli hooks che si occupano dell'output. Di default viene caricato l'hook `arch` che fornisce l'output che si visualizza normalmente. Viene fornito inoltre un syslog logging hook. Possono essere trovati in `/usr/lib/network/hooks`.

### ArchAssitant (GUI)

Esiste un'utilità grafica per netfg basata sulle Qt chiamata ArchAssistant. Il proposito è quello di gestire e collegare/scollegare i vari profili da un'icona nel vassoio di sistema. È inoltre disponibileIl il rilevamento automatico delle reti wireless. Questo strumento è particolarmente utile per gli utilizzatori di computer portatili.

Collegamenti:

*   [archassistant](https://aur.archlinux.org/packages/archassistant/) in the [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)")
*   [archassistant on kde-apps.org](http://www.kde-apps.org/content/show.php/ArchAssistant?content=76760)

C'è anche un'interfaccia grafica relativamente nuova per netcfg2 su qt-apps.org che si occupa solo della configurazione di rete. È reperibile [qui](http://www.qt-apps.org/content/show.php/netcfgGUI?content=99523).

### Netcfg Easy Wireless LAN (newlan)

newlan è una applicazione mono tramite console che avvia una finestra di configurazione user-friendly per creare i profili [netcfg](/index.php/Netcfg "Netcfg"); supporta inoltre le connesioni cablate.

Installare il pacchetto [newlan](https://aur.archlinux.org/packages/newlan/) da [AUR](/index.php/Arch_User_Repository "Arch User Repository").

`newlan` deve essere avviato con i permessi di root:

```
# newlan -n mynewprofile

```

### wifi-select

Vi è uno strumento da console per la selezione delle reti wireless in "tempo reale" (in modalità [NetworkManager](/index.php/NetworkManager "NetworkManager")) chiamato `wifi-select`. Lo strumento è utile per l'uso negli Internet café o in altri luoghi che si sta visitando per la prima (e forse l'ultima) volta. Con questo strumento, non è necessario creare un profilo per una nuova rete, basta digitare `# wifi-select wlan0` e selezionare la rete che si vuole.

[Installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") il pacchetto [wifi-select](https://aur.archlinux.org/packages/wifi-select/), attualmente disponibile nei [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

[wifi-select](https://aur.archlinux.org/packages/wifi-select/) esegue quanto segue:

*   analizza i risultati di `iwlist scan` e presenta un elenco delle reti con le relative impostazioni di sicurezza (WPA/WEP/none) usando [dialog](https://www.archlinux.org/packages/?name=dialog)
*   Se l'utente seleziona una rete con profilo esistente, basta usare questo profilo per connettersi con `netcfg`
*   Se l'utente seleziona una nuova rete (per esempio, un hotspot Wi-Fi), `wifi-select` genera automaticamente un nuovo profilo con le `$SECURITY` corrispondenti e richiede una password (se necessaria). Utilizza DHCP come `$IP` in maniera predefinita
*   poi, se la connessione riesce, il profilo viene salvato per un utilizzo successivo
*   se la connessione non riesce, all'utente viene comunque richiesto se desidera mantenere il profilo generato per un ulteriore uso (ad esempio per cambiare l'`$IP` a statico o regolare alcune opzioni aggiuntive)

Collegamenti:

*   [Forum thread](https://bbs.archlinux.org/viewtopic.php?id=63973) legati allo sviluppo di `wifi-select`
*   [wifi-select on GitHub](https://github.com/sphynx/wifi-select)

### Passaggio di argomenti a dhcpcd

Per esempio, aggungere

```
DHCP_OPTIONS='-C resolv.conf -G'

```

al profilo desiderato. L'esempio precedente impedisce a [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) di scrivere in `/etc/resolv.conf` ed impostare gli instradamenti di default.

#### Accelerare il DHCP mediante dhcpcd

Di default, `dhcpcd` conferma che l'IP assegnato non è ancora stato preso via ARP. Se si è sicuri che non lo sarà, e.g. nella tua rete domestica, è possibile accelerare il processo di connessione di circa 5 secondi aggiungendo `--noarp` a `DHCP_OPTIONS`:

```
DHCP_OPTIONS="--noarp"

```

Se non si vuole mai che `dhcpcd` effettui tale controllo ad ogni connessione, è possibile configurare globalmente ciò aggiungendo la linea seguente al file `/etc/dhcpcd.conf`:

```
noarp

```

### Uso di dhclient al posto di dhcpcd

Aggiungere semplicemente

```
DHCLIENT=yes

```

nel profilo desiderato.

### Configurare un bridge da usare con macchine virtuali (VMs)

Per configurare un bridge chiamato br0 con IP statico:

 `/etc/network.d/br0` 
```
INTERFACE="br0"
CONNECTION="bridge"
DESCRIPTION="bridge br0 static"
BRIDGE_INTERFACES="eth0"
IP='static'
ADDR='10.0.0.10'
GATEWAY='10.0.0.1'
DNS='10.0.0.1'

```

Per configurare un bridge chiamato br0 con dhcp IP:

 `/etc/network.d/br0` 
```
INTERFACE="br0"
CONNECTION="bridge"
DESCRIPTION="bridge br0 dhcp"
BRIDGE_INTERFACES="eth0"
IP='dhcp'

```

Aggiungere poi il corrispondente nome del bridge al proprio campo `NETWORKS=(...)` in `/etc/conf.d/netcfg`.

Può essere attivato chiamandolo direttamente, o riavviando net-profiles.

```
netcfg br0

```

```
rc.d restart net-profiles

```

### Aggiungere più indirizzi IP ad un'interfaccia

Se si vuole assegnare più di un indirizzo IP ad una specifica interfaccia, questo può essere fatto emettendo il relativo comando `ip` in una dichiarazione `POST_UP` (che come suggerisce il nome verrà eseguito dopo che l'interfaccia è stata attivata). Dichiarazioni multiple possono essere separate con un `;`. Così se ad esempio si voglia assegnare entrambi gli indirizzi 10.0.0.1 e 10.0.0.2 all'interfaccia eth0; la configurazione dovrebbe essere qualcosa come le seguenti righe:

 `/etc/network.d/multiple_ip` 
```
INTERFACE="eth0"
CONNECTION="ethernet"
IP='static'
ADDR='10.0.0.1'
POST_UP='ip addr add 10.0.0.2/24 dev eth0'

```

### Aggiungere indirizzamenti statici

Quando di desideri configurare indirizzamenti statici, ciò può essere fatto emettendo il relativo comando `ip` in una dichiarazione `POSTUP` (che come suggerisce il nome verrà eseguito dopo che l'interfaccia è stata attivata). Facoltativamente, si può aggiungere una dichiarazione `PRE_DOWN` per rimuovere gli indirizzamenti detti quando l'interfaccia viene disattivata. Dichiarazioni multiple possono essere separate da un `;`. Nell'esempio seguente assegneremo 10.0.1.0/24 all'interfaccia eth1 ed in seguito rimuoveremo l'indirizzamento alla disattivazione dell'interfaccia.

 `/etc/network.d/static_routes` 
```
INTERFACE="eth1"
CONNECTION="ethernet"
IP='static'
POST_UP='ip route add 10.0.1.0/24 dev eth1'
PRE_DOWN='ip route del 10.0.1.0/24 dev eth1'

```

#### Tethering Bluetooth via *pand*

È possibile creare un profilo [netcfg](/index.php/Netcfg "Netcfg"), per usufruire semplicemente del tethering tramite il Bluetooth del proprio dispositivo, usando la comune connessione "ethernet" e gestendo la connessione *pand* negli agganci PRE_UP e POST_DOWN. Supponendo che il dispositivo sia già accoppiato con indirizzo '00:00:DE:AD:BE:EF', creare semplicemente un profilo in /etc/network.d nominato - per esempio - 'tether':

```
 CONNECTION="ethernet"
 DESCRIPTION="Ethernet via pand tethering to Bluetooth device"
 INTERFACE="bnep0"
 BTADDR="00:00:DE:AD:BE:EF"
 PRE_UP="pand -E -S -c ${BTADDR} -e ${INTERFACE} -n 2>/dev/null"
 POST_DOWN="pand -k ${BTADDR}"
 IP="dhcp"

```

Quindi, sia con i permessi di root o usando sudo, eseguire:

```
# netcfg tether

```

Per disattivare l'interfaccia e disabilitare il tethering:

```
# netcfg down tether

```

## Risoluzione dei problemi

### Debugging

Per eseguire netcfg con l'output di debug, impostare la variabile `NETCFG_DEBUG` su `"yes"`, per esempio:

```
# NETCFG_DEBUG="yes" netcfg <arguments>

```

Le informazioni di debug per wpa_supplicant possono essere elencate su log usando `WPA_OPTS` all'interno di un profilo, ad esempio:

```
WPA_OPTS="-f/path/to/log"

```

Tutto ciò che è inserito sarà aggiunto al comando quando viene richiamato wpa_supplicant.

### Rete non disponibile

Questo errore è in genere causato da:

*   Fuori campo; oppure
*   Problemi con i driver.

### Associazione wireless non riuscita

Questo errore è in genere causato da:

*   Fuori campo/ricezione;
*   Configurazione errata;
*   Password errata;
*   Problemi con i driver; oppure
*   Tentativo di connessione a una rete nascosta.

Se il problema di connessione è dovuto ad una cattiva ricezione, aumentare la variabile `TIMEOUT` in `/etc/network.d/mynetwork`, come segue:

```
TIMEOUT=60

```

Se viene usato un AP con SSID nascosto, provare:

```
PRE_UP='iwconfig $INTERFACE essid $ESSID'

```

### Impossibile ottenere l'indirizzo IP con DHCP

Questo errore è in genere causato da:

*   Fuori campo/ricezione

Provare ad incrementare la variabile `DHCP_TIMEOUT` nella propria rete `/etc/network.d/profile`.

### Connessione non valida, controllo ortografico o guardare gli esempi

È necessario impostare `CONNECTION` a uno dei tipi di connessione elencati nella cartella `/usr/lib/network/connections`. In alternativa, utilizzare una delle configurazioni d'esempio fornite in `/etc/network.d/examples`.

### Nessuna connessione

#### Carrier Timeout

Se si ottengono vari messaggi di debug simili ai seguenti (ricordando che il nome del profilo e dell'interfaccia può essere differente), può essere che il processo di attivazione dell'interfaccia stia impiegando troppo tempo.

```
 DEBUG: Loading profile eth0-dhcp
 DEBUG: Configuring interface eth0
 :: eth0-dhcp up
 DEBUG: status reported to profile_up as:
 DEBUG: Loading profile eth0-dhcp
 DEBUG: Configuring interface eth0
 DEBUG: ethernet_iproute_up ifup
   > No connection
 DEBUG: profile_up connect failed
  [FAIL]

```

Di default sono 2 secondi. Per allungare il timeout, impostare la variabile CARRIER_TIMEOUT prima di richiamare netcfg.

Questo thread illustra un esempio di questo problema: [https://bbs.archlinux.org/viewtopic.php?id=138615](https://bbs.archlinux.org/viewtopic.php?id=138615)

#### Skip no carrier

Quando si attiva manualmente un'interfaccia ma il log dice „Nessuna Connessione" durante il boot, può essere che la connessione fisica non possa essere rilevata abbastanza velocemente. Provare ad aggiungere:

```
 SKIPNOCARRIER='yes'

```

al proprio profilo. Netcfg assegnerà l'indirizzo IP indipendentemente dal fatto che vi sia una connessione cablata attiva.

### Driver quirks

**Note:** Quasi sicuramente **non** si avrà bisogno dei quirks (arguzie); per prima cosa assicurarsi che la configurazione sia corretta prima di farne uso. I quirks sono destinati ad una ridotta gamma di driver con problemi insoliti, molti dei quali sono obsoleti. Questi sono rimedi alternativi, non soluzioni.

Alcuni driver si comportano stranamente e hanno bisogno di soluzioni alternative per funzionare. I quirks devono essere abilitati manualmente. Le migliori soluzioni sono determinate dalla lettura nei forum, traendo spunto da quello che altri hanno sperimentato, e, se non funziona , riprovare ancora. I quirks possono essere anche vari.

	`prescan`

	Eseguire `iwlist $INTERFACE scan` prima di tentare la connessione (broadcom)

	`preessid`

	Eseguire `iwconfig $INTERFACE essid $ESSID` prima di tentare la connessione (ipw3945, broadcom e Intel PRO/Wireless 4965AGN)

	`wpaessid`

	Come sopra, eseguire prima dell'avvio `wpa_supplicant`. Non più supportato - usare invece `IWCONFIG="essid $ESSID"` (ath9k).

	`predown`

	Neutralizzare l'interfaccia (down) prima dell'associazione e ripristinarla solo in seguito (madwifi)

	`postsleep`

	Aspettare un momento prima di verificare se l'associazione è riuscita

	`postscan`

	Eseguire `iwlist scan` dopo l'associazione

Aggiungere i quirks richiesti al file di configurazione di netcfg `/etc/network.d/mynetwork`, per esempio:

```
QUIRKS=(prescan preessid)

```

Se si ottengono gli errori "Wireless network not found", "Association failed" avendo provato le soluzioni descritte sopra, o se è usato un AP con un SSID nascosto, consultare la sezione precedente [#Associazione wireless non riuscita](#Associazione_wireless_non_riuscita).

### Ralink legacy driver rt2500, rt2400 usando iwpriv

Non ci sono soluzioni per aggiungere il supporto WPA per questi driver. rt2x00 è comunque supportato, e andrà a sostituire questi.

Se è necessario utilizzarli, creare uno script che esegue i comandi necessari `iwpriv` e mettere il suo percorso in `PRE_UP`.

### Nel caso di: "/var/run/network//suspend/": No such file or directory

Se si riceve questo messaggio di errore non preoccuparsi, perché è un bug noto. Creare la directory a mano.

### Ancora non funziona, che cosa devo fare?

Se questo articolo non ha aiutato a risolvere il problema, il miglior posto per chiedere aiuto è il forum o la mailing list.

Per essere in grado di determinare il problema, abbiamo bisogno di informazioni. Quando richiesto, fornire il seguente output:

*   **ALL OUTPUT FROM netcfg**
*   **ALL OUTPUT FROM netcfg**
*   **ALL OUTPUT FROM netcfg**
    *   Questo è assolutamente fondamentale per poter determinare cosa sia andato storto. Il messaggio potrebbe essere breve o inesistente, ma può significare molto.
*   **`/etc/network.d` network profiles**
    *   Questo è anche importante, in quanto molti problemi sono semplici errori di configurazione.
*   **netcfg version**
*   `lsmod`
*   `iwconfig`

## Domande frequenti

### Perchè netcfg non fa *(alcune cose)*?

netcfg non ne ha bisogno, si limita a connettersi alle reti, è modularare e riutilizzabile; consultare `/usr/lib/network` per funzioni di riusabilità con scripts personalizzati.

### Perchè netcfg non si comporta in *questo* modo?

netcfg non impone alcuna regola; Si limita a collegarsi alle reti. Non impone alcun concetto euristico, come "disconnettersi dal wireless se ethernet è collegato". Se si desidera una funzionalità del genere, no dovrebbe essere complicato scrivere uno strumento separato, al di fuori di netcfg. Vedere la domanda di cui sopra.

### Ho ancora bisogno di *(qualche cosa)* se sto utilizzando netcfg?

Questa domanda di solito si riferisce a `/etc/hosts` e la variabile `HOSTNAME` in `/etc/rc.conf`, che sono ancora entrambi necessari. Si può comunque rimuovere `network` dalla stringa `DAEMONS` se tutte le reti sono state configurate con netcfg.