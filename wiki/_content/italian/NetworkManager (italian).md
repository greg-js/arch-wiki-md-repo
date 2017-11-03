Articoli correlati

*   [Configurare la rete](/index.php/Configuring_Network_(Italiano) "Configuring Network (Italiano)")
*   [Setup wreless](/index.php/Wireless_Setup_(Italiano) "Wireless Setup (Italiano)")
*   [Netctl](/index.php/Netctl "Netctl")
*   [Wicd](/index.php/Wicd_(Italiano) "Wicd (Italiano)")

[NetworkManager](http://projects.gnome.org/NetworkManager/) è un programma per la rilevazione e la configurazione delle reti, e con il quale, i sistemi potranno connettersi automaticamente. La funzionalità di NetworkManager può essere utile sia per reti cablate che wireless. Per quanto riguarda il wireless, NetworkManager predilige le reti conosciute, ed offre la possibilità di passare alla rete più affidabile. Le applicazioni di allerta di NetworkManager possono passare dalla modalità online a quella offline. NetworkManager può inoltre favorire le connessioni cablate a quelle wireless, oltre ad includere il supporto per connessioni modem e certi tipi di VPN. NetworkManager è stato originariamente sviluppato da RedHat ed è ora ospitato dal progetto [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)").

## Contents

*   [1 Installazione di base](#Installazione_di_base)
    *   [1.1 Supporto VPN](#Supporto_VPN)
*   [2 Interfacce grafiche](#Interfacce_grafiche)
    *   [2.1 GNOME e MATE](#GNOME_e_MATE)
    *   [2.2 KDE4](#KDE4)
    *   [2.3 XFCE](#XFCE)
    *   [2.4 Openbox](#Openbox)
    *   [2.5 Altri desktop e Window Manager](#Altri_desktop_e_Window_Manager)
    *   [2.6 Da riga di comando](#Da_riga_di_comando)
*   [3 Configurazione](#Configurazione)
    *   [3.1 Disabilitare la configurazione di rete attuale](#Disabilitare_la_configurazione_di_rete_attuale)
    *   [3.2 Abilitare NetworkManager](#Abilitare_NetworkManager)
    *   [3.3 Impostare i permessi di PolicyKit](#Impostare_i_permessi_di_PolicyKit)
    *   [3.4 Servizi di rete con NetworkManager Dispatcher](#Servizi_di_rete_con_NetworkManager_Dispatcher)
        *   [3.4.1 Avviare openntpd](#Avviare_openntpd)
        *   [3.4.2 Montare cartelle remote con sshfs](#Montare_cartelle_remote_con_sshfs)
        *   [3.4.3 Usare dispatcher per connettersi a rete VPN dopo aver stabilito una connessione](#Usare_dispatcher_per_connettersi_a_rete_VPN_dopo_aver_stabilito_una_connessione)
    *   [3.5 Impostazioni proxy](#Impostazioni_proxy)
*   [4 Testing](#Testing)
*   [5 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [5.1 Problemi con il traffico dati tramite il tunnel PPTP](#Problemi_con_il_traffico_dati_tramite_il_tunnel_PPTP)
    *   [5.2 Gestione di rete disabilitata](#Gestione_di_rete_disabilitata)
    *   [5.3 NetworkManager impedisce a DHCPCD l'uso di resolv.conf.head e resolv.conf.tail](#NetworkManager_impedisce_a_DHCPCD_l.27uso_di_resolv.conf.head_e_resolv.conf.tail)
    *   [5.4 Preservare le modifiche a resolv.conf](#Preservare_le_modifiche_a_resolv.conf)
    *   [5.5 Problemi DHCP](#Problemi_DHCP)
    *   [5.6 Problemi con hostname](#Problemi_con_hostname)
    *   [5.7 Manca il route predefinito](#Manca_il_route_predefinito)
    *   [5.8 Modem 3G non rilevato](#Modem_3G_non_rilevato)
    *   [5.9 Spegnimento WLAN su computer portatili](#Spegnimento_WLAN_su_computer_portatili)
    *   [5.10 Impostazioni IP statico ripristinate a DHCP](#Impostazioni_IP_statico_ripristinate_a_DHCP)
    *   [5.11 È impossibile editare connessioni da utente](#.C3.88_impossibile_editare_connessioni_da_utente)
    *   [5.12 Cancellare una rete nascosta](#Cancellare_una_rete_nascosta)
*   [6 Suggerimenti](#Suggerimenti)
    *   [6.1 Condividere connessione internet su wifi](#Condividere_connessione_internet_su_wifi)
        *   [6.1.1 Ad-hoc](#Ad-hoc)
        *   [6.1.2 Access Point](#Access_Point)
    *   [6.2 Verificare l'attivazione della rete all'interno di un processo cron o script](#Verificare_l.27attivazione_della_rete_all.27interno_di_un_processo_cron_o_script)
    *   [6.3 Sblocco automatico del portachiavi dopo il login](#Sblocco_automatico_del_portachiavi_dopo_il_login)
        *   [6.3.1 Gnome](#Gnome)
        *   [6.3.2 KDE](#KDE)
        *   [6.3.3 SLiM login manager](#SLiM_login_manager)
    *   [6.4 Ignorare dispositivi specifici](#Ignorare_dispositivi_specifici)
    *   [6.5 Connessioni più veloci](#Connessioni_pi.C3.B9_veloci)
        *   [6.5.1 Collegarsi più velocemente disabilitando IPv6](#Collegarsi_pi.C3.B9_velocemente_disabilitando_IPv6)
        *   [6.5.2 Speed up DHCP by disabling ARP probing in dhcpcd](#Speed_up_DHCP_by_disabling_ARP_probing_in_dhcpcd)
        *   [6.5.3 Usare Servers OpenDNS](#Usare_Servers_OpenDNS)

## Installazione di base

[networkmanager](https://www.archlinux.org/packages/?name=networkmanager) è disponibile nei [repositories ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)") ed è quindi installabile tramite [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)").

### Supporto VPN

Networkmanager supporta le reti VPN tramite tre plugin, tutti presenti nei [repositories ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)"):

*   [networkmanager-openvpn](https://www.archlinux.org/packages/?name=networkmanager-openvpn)
*   [networkmanager-pptp](https://www.archlinux.org/packages/?name=networkmanager-pptp)
*   [networkmanager-vpnc](https://www.archlinux.org/packages/?name=networkmanager-vpnc)

## Interfacce grafiche

Per configurare ed avere un facile accesso a NetworkManager, molti utenti vorranno installare un'applet. Quest'interfaccia grafica solitamente risiede nella system tray (o area di notifica) e consente la selezione della rete e la configurazione di NetworkManager. Esistono varie applet per diversi tipi di desktop.

### GNOME e MATE

L'applet GNOME ([network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet)) è abbastanza leggero e funziona in tutti gli ambienti.

Se si desidera memorizzare i dati di autenticazione (Wireless/DSL) e attivare le impostazioni di connessione globale, cioè "a disposizione di tutti gli utenti" è necessario installare [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring").

### KDE4

Il front-end KNetworkManager è stato reso disponibile per la versione KDE 4.4 come un widget di Plasma [kdeplasma-applets-networkmanagement](https://aur.archlinux.org/packages/kdeplasma-applets-networkmanagement/) nei [Repositori Ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)")

La controparte GNOME funziona altrettanto bene, o anche meglio (ha più funzioni e rileva più hardware).

**Nota:** Se si cambia da un altro strumento di gestione di rete come [Wicd](/index.php/Wicd_(Italiano) "Wicd (Italiano)"), non dimenticare di impostare il valore predefinito "Network Management Backend" in System Settings -> Hardware -> Information Sources

Se sul proprio sistema si hanno installati sia KNetworkManager, sia `nm-applet` e non si vuole avere `nm-applet` aperto su KDE, aggiungere questa riga a `/etc/xdg/autostart/nm-applet.desktop`.

```
NotShowIn=KDE

```

### XFCE

`nm-applet` funziona perfettamente anche in XFCE, ma per abilitare le notifiche, *inclusi i messaggi di errore* è necessaria una specifica implementazione di Freedesktop. Vedere [questo](http://www.galago-project.org/specs/notification/0.9/index.html) per visualizzare le notifiche. L'implementazione più usata è data dal pacchetto [xfce4-notifyd](https://www.archlinux.org/packages/?name=xfce4-notifyd).

Senza questo demone, networkmanager stamperà questi errori stdout/stderr:

```
(nm-applet:24209): libnotify-WARNING **: Failed to connect to proxy

```

```
** (nm-applet:24209): WARNING **: get_all_cb: couldn't retrieve
system settings properties: (25) Launch helper exited with unknown
return code 1.

```

```
** (nm-applet:24209): WARNING **: fetch_connections_done: error
fetching connections: (25) Launch helper exited with unknown return
code 1.

```

```
** (nm-applet:24209): WARNING **: Failed to register as an agent:
(25) Launch helper exited with unknown return code 1

```

nm-applet funziona comunque, ma non si avrannò notifiche.

### Openbox

Per usare in modo appropriato networkmanager su [Openbox](/index.php/Openbox_(Italiano) "Openbox (Italiano)") è necessario il demone di notifica [xfce4-notifyd](https://www.archlinux.org/packages/?name=xfce4-notifyd) e il pacchetto [gnome-icon-theme](https://www.archlinux.org/packages/?name=gnome-icon-theme) per abilitare l'icona nella systray.

Se si desidera memorizzare i dati di autenticazione (Wireless/DSL) installare [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring").

**Nota:** Se il demone *networkmanager* è in `/etc/rc.conf`, i seguenti passaggi sono del tutto obsoleti e l'applet verrà avviato due volte.

Per fare in modo che l'autostart di Openbox avvii nm-applet correttamente, potrebbe essere necessario cancellare il file `/etc/xdg/autostart/nm-applet.desktop` (potrebbe essere necessario cancellarlo dopo ogni aggiornamento di network-manager-applet)

Poi in `autostart`, avviare `nm-applet` con questa riga:

```
(sleep 3 && /usr/bin/nm-applet --sm-disable) &

```

Se si riscontrano errori assicurarsi di aver avviato correttamente la sessione di [D-Bus](/index.php/D-Bus "D-Bus").

### Altri desktop e Window Manager

Si consiglia di utilizzare l'applet di GNOME. Assicurarsi inoltre che il pacchetto [gnome-icon-theme](https://www.archlinux.org/packages/?name=gnome-icon-theme) sia installato per essere in grado di visualizzare l'applet .

Per far si che la password sia memorizzata sarà necessario installare anche [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring").

Per utilizzare `nm-applet` senza un vassoi di sistema, si può avvalersi di [trayer](https://www.archlinux.org/packages/?name=trayer) o `stalonetray`. Si può ad esempio aggiungere uno script come questo al proprio percorso:

 `nmgui` 
```
 #!/bin/sh
 nm-applet    > /dev/null 2>/dev/null &
 stalonetray  > /dev/null 2>/dev/null
 killall nm-applet

```

La chiusura della finestra del vassoio, comporterà anche la chiusura di `nm-applet`, in modo che non verrà sprecata memoria inutilmente una volta terminato con le impostazioni di rete.

### Da riga di comando

Il pacchetto networkmanager, dalla versione 0.8.1 contiene [nmcli](http://manpages.ubuntu.com/manpages/maverick/man1/nmcli.1.html)

## Configurazione

NetworkManager richiede alcuni passaggi aggiuntivi per essere eseguito correttamente.

Verificare che il file `/etc/hosts` sia a posto prima di continuare. In caso di aver provato la connessione prima di eseguire questo passo, NetworkManager potrebbe averlo alterato. Un esempio di hostname in `/etc/hosts`:

```
127.0.0.1     localhost
::1           localhost

```

In caso si usi nss-myhostname:

```
127.0.0.1 my-laptop localhost
::1 my-laptop localhost
```

### Disabilitare la configurazione di rete attuale

Si consiglia di disabilitare la presente configurazione di rete per essere in grado di testare adeguatamente NetworkManager.

1.  Stoppare i servizi di rete attivi. Ad esempio:

```
# systemctl stop net-auto-wireless

```

1.  Disabilitare servizi di rete diversi da nm. Ad esempio

```
# systemctl disable net-auto-wireless
# systemctl disable wicd

```

Infine, disattivare il proprio NIC's (Network Interface Controllers, es. schede di rete). Per esempio, con il pacchetto [iproute2](https://www.archlinux.org/packages/?name=iproute2):

```
 # ip link set eth0  down
 # ip link set wlan0 down

```

### Abilitare NetworkManager

È necessario abilitare networkmanager in modo assolutamente coerente con il proprio sistema di Init. Se si ha appena installato Arch Linux si ha sicuramente [Systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)") di default. Una volta che Networkmanager sarà avviato si potrà usufruire da subito dei servizi di rete tramite `nmcli` o un altro applet grafico.

Per avviare immediatamente `NetworkManager` usare il seguente comando:

```
# systemctl start NetworkManager

```

Per abilitare il relativo servizio di [systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)") usare questo comando:

```
# systemctl enable NetworkManager

```

**Nota:** Se si hanno dei servizi che non riescono ad avviarsi correttamente se avviati prima della rete, usare il servizio `NetworkManager-wait-online.service`. Questo, in linea generale, non dovrebbe essere quasi mai necessario.

### Impostare i permessi di PolicyKit

Vedere [questo](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") per maggiori informazioni. Nella configurazione di default, gli utenti non root non sono autorizzati ad aggiungere connessioni di rete. Procedere così:

*Opzione 1.* Avviare un *authentication agent* [PolicyKit](/index.php/PolicyKit "PolicyKit") al login come `/usr/lib/polkit-gnome/polkit-gnome-authentication-agent-1` (necessita di [polkit-gnome](https://www.archlinux.org/packages/?name=polkit-gnome)). Potrebbe essere richiesta una password ad ogni modifica alla connessione.

*Opzione 2.* Aggiungere il proprio utente al gruppo `wheel`. In questo modo nessuna password verrà chiesta ma bisognerà garantire dei permessi particolari all'utente come ad esempio l' *abilità* di non immettere password usando [sudo](/index.php/Sudo_(Italiano) "Sudo (Italiano)").

*Opzione 3.* Aggiungere il proprio utente al gruppo `network` e creare il seguente file:

 `/etc/polkit-1/localauthority/50-local.d/org.freedesktop.NetworkManager.pkla` 
```
polkit.addRule(function(action, subject) {
  if (action.id.indexOf("org.freedesktop.NetworkManager.") == 0 && subject.isInGroup("network")) {
    return polkit.Result.YES;
  }
});
```

Ora tutti gli utenti in tale gruppo (`network`) potranno aggiungere o rimuovere reti senza password. Questo non funziona se si usa systemd senza una sessione di [systemd-logind](/index.php/Systemd_(Italiano)#Usare_systemd-logind "Systemd (Italiano)").

### Servizi di rete con NetworkManager Dispatcher

Ci sono un paio di servizi di rete che non si desiderano in esecuzione fino a quando NetworkManager attiva un'interfaccia. Buoni esempi sono **openntpd** e i vari tipi di montaggi dei filesystem di rete (es. **netfs**). NetworkManager ha la capacità di avviare questi servizi quando ci si connette a una rete (interface up), e fermarli quando non li si sta utilizzando più (interface down).

Per utilizzare questa funzionalità, gli script possono essere aggiunti nella cartella `/etc/NetworkManager/dispatcher.d`. Questi script avranno bisogno dei permessi di esecuzione dell'utente. Per ragioni di sicurezza, è buona prassi renderli di proprietà di **root:root** e scrivibili solo dal proprietario.

Gli script verranno eseguiti in ordine alfabetico al momento della connessione (con argomenti *interface up*), e in ordine alfabetico inverso al momento della disconnessione (*interface down*). Per garantire l'ordine in cui vengono richiamati, è pratica comune utilizzare dei caratteri numerici prima del nome dello script (es. `10_portmap` o `30_netfs` (che assicura che il portmapper sia attivato prima che vengano tentati i montaggi NFS).

**Attenzione:** Per ragioni di sicurezza è necessario disattivare l'accesso in scrittura per il "gruppo" e per "altri". Ad esempio usare 755 mask. In altri casi può essere negata l'esecuzione di script, con il seguente messaggio di errore "nm-dispatcher.action: Script could not be executed: writable by group or other, or set-UID." in `/var/log/messages.log`

**Attenzione:** Se ci si connette da reti pubbliche o estere, bisogna essere consapevoli di quali servizi si stanno avviando e quali server su cui connettersi sono disponibili per loro. Si potrebbe aprire una falla di sicurezza lanciando i servizi sbagliati mentre si è connessi ad una rete pubblica.

#### Avviare openntpd

Lo script seguente è un esempio di come avviare openntpd quando un'interfaccia viene attivata. Salvare il file come `/etc/NetworkManager/dispatcher.d/20_openntpd` e renderlo eseguibile.

```
#!/bin/sh

INTERFACE=$1 # The interface which is brought up or down
STATUS=$2 # The new state of the interface

case "$STATUS" in
    'up') # $INTERFACE is up
	systemctl openntpd start
	;;
    'down') # $INTERFACE is down
	# Check for active interface and down if no one active
	if [ ! `nm-tool|grep State|cut -f2 -d' '` == "connected" ]; then
		systemctl openntpd stop
	fi
	;;
esac

```

#### Montare cartelle remote con sshfs

Dato che lo script viene eseguito in un ambiente ristretto, è necessario esportare `SSH_AUTH_SOCK` per connettere il proprio agente SSH. Esistono diversi modi per compiere adeguatamente questa operazione, per maggiori informazioni [leggere questa discussione sul forum](https://bbs.archlinux.org/viewtopic.php?pid=1042030#p1042030). L'esempio sottostante funziona con [gnome-keyring](/index.php/Gnome-keyring "Gnome-keyring"), che, se non è già stato sbloccato, richiederà la relativa password. Nel caso in cui networkmanager si avvii in modo automatico all'avvio è possibile che gnome-keyring non sia ancora stato inizializzato. È quindi possibile che l'esportazione fallisca (ed entri in sleep). L' `UUID` necessario si trova in `/etc/NetworkManager/system-connections/`.

```
#!/bin/bash
USER=<your sshfs user>
if [ $CONNECTION_UUID == <connection UUID> ]; then
       case "$2" in
               up)
                  #sleep 10
                  export SSH_AUTH_SOCK=$(find /tmp/keyring-*/ -type s -user $USER -gr oup users -name ssh)
                  su $USER -c "/usr/bin/sshfs user@host:/remote/folder /local/folder/"
                ;;
               down)
                  fusermount -u /local/folder
                ;;
       esac
fi

```

#### Usare dispatcher per connettersi a rete VPN dopo aver stabilito una connessione

In questo esempio si desidera connettersi automaticamente a una connessione VPN definita in precedenza con NetworkManager. La prima cosa da fare è creare lo script del dispatcher che definisce che cosa fare dopo aver stabilito la connessione alla rete.

**1)** Creare lo script `/etc/NetworkManager/dispatcher.d/vpn-up` 
```
VPN_NAME=<name of VPN connection defined in NetworkManager>
  ESSID=<wifi network ESSID (not connection name)>
  if [ "$2" = "up" -o "$2" = "vpn-down" ]; then          # -o "$2" = "vpn-down" makes VPN reconnect after VPN connection interrupt
    if [ "$(iwgetid | grep ':"'$ESSID'"')" ]; then       # check for ESSID match
      nmcli con up id "$VPN_NAME";                       # parentheses needed for VPN connection names with spaces
    fi
  elif [ "$2" = "down" ]; then                           # disconnect VPN prior to disconnecting from the network
    if [ "$(iwgetid | grep ':"'$ESSID'"')" ]; then       # check for ESSID match and that VPN is actually connected
      if [ $(nmcli con status id "$VPN_NAME" | grep -c activated) ]; then
        nmcli con down id "$VPN_NAME";
      fi
    fi
  fi

```

Non dimenticare di renderlo eseguibile con chmod +x e di rendere possibile a tutti gli utenti accedere a connessioni vpn.

Provando a connettere networkmanager con questa configurazione si noterà che il risultato sarà: 'no valid vpn secrets'. Questo è causato dal modo in cui [i "secret flag" vengono salvati da vpn](http://projects.gnome.org/NetworkManager/developers/migrating-to-09/secrets-flags.html). È quindi necessario seguire quest altra istruzione:

**2)** Editare il file di configuazione della connessione vpn per rendere NetworkManager in grado di memorizzare i parametri al suo interno invece che in un portachiavi che sarà [inaccessibile a root](https://bugzilla.redhat.com/show_bug.cgi?id=710552):

Aprire quindi `NetworkManager/system-connections/<nome della connessione>` e cambiare `password-flags` e `secret-flags` da `1` a `0`.

**Nota:** Potrebbe essere necessario riaprire l'applet di NetworkManager e re-immettere la password vpn.

### Impostazioni proxy

Network Manager non gestisce direttamente le impostazioni del proxy, ma con il [DE](/index.php/Desktop_environment_(Italiano) "Desktop environment (Italiano)") [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)"), è possibile utilizzare [proxydriver](http://marin.jb.free.fr/proxydriver/) per le impostazioni proxy tramite le informazioni di Network Manager. Il pacchetto [proxydriver](https://aur.archlinux.org/packages/proxydriver/) è disponibile su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").

Per fare in modo che proxydriver sia in grado di modificare le impostazioni del proxy, è necessario eseguire questo comando, dalle applicazioni d'avvio di GNOME (Sistema->Preferenze->Applicazioni d'avvio):

```
xhost +si:localuser:your_username

```

Consultare: [Proxy settings](/index.php/Proxy_settings "Proxy settings")

## Testing

Gli applet NetworkManager sono progettati per essere caricati al momento del login in modo che nessuna ulteriore configurazione dovrebbe essere necessaria per la maggior parte degli utenti. Dopo aver disabilitato le impostazioni di rete precedenti e scollegata la rete, è possibile verificare se NetworkManager funziona. Per prima cosa [avviare](/index.php/Demoni "Demoni") il demone **networkmanager**.

Alcuni applet includono un file `.desktop` in modo da poter essere caricati attraverso il menu delle applicazioni. In caso contrario, bisognerà scoprire il comando da usare o reiniziare una nuova sessione per avviare l'applet. Una volta avviato, stabilirà le connessioni di rete dopo una prima fase di interrogazioni (polling), per poi auto-configurarsi con un server DHCP.

Per avviare l'applet di GNOME in Window Manager non compatibili con xdg come [Awesome](/index.php/Awesome_(Italiano) "Awesome (Italiano)"):

```
nm-applet --sm-disable &

```

Per gli IP statici è necessario configurare NetworkManager ad interpretarli. Solitamente basta un click destro del mouse sull'applet per selezionare "Modifica connessioni".

## Risoluzione dei problemi

Alcune correzioni ai problemi più comuni.

### Problemi con il traffico dati tramite il tunnel PPTP

Può succedere che il login alla connessione PPTP avvenga in maniera corretta, e si veda che l'interfaccia ppp0 ha un IP VPN esatto, ma non si riesca a "pingare" nessun IP remoto. La causa è la mancanza del supporto a MPPE (Microsoft Point-to-Point Encryption) nel pacchetto pppd di Arch.

Sarà sufficiente installare [ppp-mppe](https://aur.archlinux.org/packages/ppp-mppe/) da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").

Prima provare con il pacchetto standard di Arch [ppp](https://www.archlinux.org/packages/?name=ppp), potrebbe funzionare a dovere.

### Gestione di rete disabilitata

A volte, quando NM viene spento, il file del PID (stato) non viene rimosso e si ottiene il messaggio "Network management disabled". Se questo accade, sarà necessario rimuoverlo manualmente:

```
rm /var/lib/NetworkManager/NetworkManager.state

```

Se questo accade al riavvio, è possibile aggiungere un'azione a `etc/rc.local` per farli rimuovere al momento del boot:

```
nmpid=/var/lib/NetworkManager/NetworkManager.state
[ -f $nmpid ] && rm $nmpid
```

### NetworkManager impedisce a DHCPCD l'uso di resolv.conf.head e resolv.conf.tail

A volte è problematico aggiungere elementi statici a `resolv.conf` quando è costantemente riscritto da NM e `dhcpcd`. È possibile utilizzare il pacchetto networkmanager-dhclient di AUR, ma una soluzione migliore è quella di utilizzare questo semplice script:

```
#!/bin/bash
# 
# /etc/NetworkManager/dispatcher.d/99-resolv.conf-head_and_tail
# Include /etc/resolv.conf.head and /etc/resolv.conf.tail to /etc/resolv.conf
#
# scripts in the /etc/NetworkManager/dispatcher.d/ directory
# are called alphabetically and are passed two parameters:
# $1 is the interface name, and $2 is “up” or “down” as the
# case may be.

resolvconf='/etc/resolv.conf';
cat "$resolvconf"{.head,,.tail} 2>/dev/null > "$resolvconf".tmp
mv -f "$resolvconf".tmp "$resolvconf"
```

Alternativamente installare [networkmanager-dispatch-resolv](https://aur.archlinux.org/packages/networkmanager-dispatch-resolv/) da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").

### Preservare le modifiche a resolv.conf

NetworkManager cercherà di scrivere le informazioni del DNS da DHCP in `/etc/resolv.conf`, sovrascrivendone il contenuto esistente. È possibile evitare questo comportamento impostando il "bit immutabile" sul file (da root):

```
# chattr +i /etc/resolv.conf

```

Per modificare il file in futuro, rimuovere per prima cosa il bit immutabile:

```
# chattr -i /etc/resolv.conf

```

### Problemi DHCP

In caso di problemi nell'ottenere un indirizzo IP tramite DHCP, provare ad aggiungere quanto segue al file `/etc/dhclient.conf`:

```
 interface "eth0" {
   send dhcp-client-identifier 01:aa:bb:cc:dd:ee:ff;
 }

```

Dove `aa:bb:cc:dd:ee:ff` è l'indirizzo MAC della scheda di rete. L'indirizzo MAC può essere trovato usando il comando `ip link show eth0`, fornito da [iproute2](https://www.archlinux.org/packages/?name=iproute2).

Con qualche router, risulterà impossibile la connessione senza prima aver decommentato:

```
require dhcp_server_identifier

```

in `/etc/dhcpcd.conf` (notare che questo file è un file distinto da `dhcpd.conf`). Questo non dovrebbe causare problemi con server a DHCP multipli (configurazione non usuale); vedere [questa pagina](http://technet.microsoft.com/en-us/library/cc977442.aspx) per maggiori informazioni.

### Problemi con hostname

Aggiungere la seguente riga al file `/etc/NetworkManager/NetworkManager.conf`:

```
dhcp=dhcpcd

```

e riavviare il [servizio](/index.php/Systemd_(Italiano) "Systemd (Italiano)") di NetworkManager.

### Manca il route predefinito

Se con un sistema con KDE4, nessun percorso di default è stato creato al momento di stabilire le connessioni wireless con NetworkManager, in genere si può risolvere modificando le impostazioni di route della connessione wireless, per rimuovere la selezione di default "Use only for resources on this connection".

### Modem 3G non rilevato

Se NetworkManager (da v0.7.999) non rileva il modem 3G, ma è comunque possibile collegarsi tramite [wvdial](/index.php/Wvdial "Wvdial"), provare ad installare il pacchetto [modemmanager](https://www.archlinux.org/packages/?name=modemmanager) e riavviare il demone NetworkManager con `/etc/rc.d/networkmanager restart`. Ricollegare il modem o riavviare. Questa utilità fornisce il supporto per l'hardware non incluso di default nel database di NetworkManager.

### Spegnimento WLAN su computer portatili

A volte NetworkManager non funziona quando si disattiva l'adattatore Wifi con l'interruttore del portatile e si prova ad abilitarlo nuovamente in seguito.

```
$ watch -n1 rfkill list all

```

per verificare se il driver informa `rfkill` circa lo stato della scheda wireless. Se un identificatore rimane bloccato dopo aver premuto l'adattatore, si potrebbe provare a sbloccarlo manualmente con (dove X è il numero di identificazione fornito dall'output del comando sopra):

```
# rfkill event unblock X

```

### Impostazioni IP statico ripristinate a DHCP

A causa di un bug non risolto, quando si cambia l'impostazione predefinita per le connessioni con IP statico, `nm-applet` potrebbe non memorizzare correttamente la modifica della configurazione, e reimpostare il DHCP automatico. Segue una soluzione per questo problema.

Modificare la connessione predefinita (per esempio "Auto eth0") in `nm-applet`. Cambiare il nome della connessione (ad esempio "la mia eth0"), deselezionare la casella "Disponibile a tutti gli utenti", modificare le impostazioni di IP statico desiderate, quindi fare clic su *Applica*. Ciò salverà una nuova connessione con il nome indicato.

Successivamente, si desidera effettuare la connessione di default e non connettersi automaticamente. Per fare ciò, eseguire

```
$ sudo nm-connection-editor  # si deve usare sudo, non su

```

Nell'editor di connessione, modificare la connessione di default (ad esempio "Auto eth0") e deselezionare "Connetti automaticamente". Fare clic su *Applica* e chiudere l'editor di connessione.

### È impossibile editare connessioni da utente

Vedere [#Impostare i permessi di PolicyKit](#Impostare_i_permessi_di_PolicyKit).

### Cancellare una rete nascosta

Ovviamente una rete a `ESSID` nascosto non compare nella GUI dell'applet. Per rimuoverla quindi usare il seguent comando:

```
# rm /etc/NetworkManager/system-connections/[SSID]

```

Tale comando funziona con ogni rete.

## Suggerimenti

### Condividere connessione internet su wifi

È possibile condividere una connessione (es.: 3G o wired) con pochi click con NetworkManager. Tuttavia le schede wifi supportate sono poche, con Atheros AR9xx e AR5xx non si dovrebbero avere problemi.

#### Ad-hoc

*   Installare [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) dai [repositories ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").
*   Una configurazione personalizzata di `dnsmasq.conf` potrebbe interferire.
*   Clickare sull'applet di nm-applet -> Creare nuova connessione wireless.
*   Seguire il wizard (se si usa WEP assicurarsi di usare o 5 o 13 caratteri come password, password diverse potrebbero fallire)
*   Il setting rimane salvato per i prossimi utilizzi

#### Access Point

Supportato da NetworkManager dalla fine del 2012, tale features equivale all' "HotSpot" dei telefoni android.

Vedere [http://fedoraproject.org/wiki/Features/RealHotspot](http://fedoraproject.org/wiki/Features/RealHotspot) per ulteriori informazioni.

### Verificare l'attivazione della rete all'interno di un processo cron o script

Alcune esecuzioni di cron richiedono la rete per poter funzionare. Si potrebbe evitare l'esecuzione di questi, fino a quando la rete non è nuovamente disponibile. A tale scopo, aggiungere un **if** di prova per le networking query richieste da NetworkManager, che controllano lo stato della rete. Il test qui illustrato funziona con le interfacce attive, e fallisce se non lo sono. Questo può essere utile per i computer portatili che possono essere cablati, wireless, o semplicemente fuori dalla rete.

```
if [ `nm-tool|grep State|cut -f2 -d' '` == "connected" ]; then
       #Whatever you want to do if the network is online
else
       #Whatever you want to do if the network is offline - note, this and the else above are optional
fi

```

Molto utile per uno script cron.hourly che esegue **fpupdate** per l'aggiornamento dello scanner antivirus F-Prot, per esempio. Un'altra possibilità, con delle piccole modifiche, è quello di distinguere tra le reti utilizzando varie parti degli output di **nm-tool**; per esempio, in quanto la rete wireless attiva è indicata con un asterisco, è possibile, con l'utilizzo di "grep", trovare il nome della rete orientando la ricerca "grep" all'asterisco.

### Sblocco automatico del portachiavi dopo il login

#### Gnome

1.  Fare clic destro sull'icona di NM nel pannello e selezionare "Modifica connessioni" per aprire la scheda Wireless
2.  Selezionare la connessione che si desidera e fare clic sul pulsante Modifica
3.  Seleziona le caselle "connessione automatica" e "disponibili a tutti gli utenti"

Disconnettersi ed accedere nuovamente alla sessione.

**Nota:** Il metodo seguente è datato, e noto per non funzionare su alcune macchine!

*   In `/etc/pam.d/gdm` (o il demone corrispondente in /etc/pam.d), aggiungere queste righe alla fine dei blocchi "auth" e "session" in caso non esistano già:

```
 auth            optional        pam_gnome_keyring.so
 session         optional        pam_gnome_keyring.so  auto_start

```

*   In `/etc/pam.d/passwd`, utilizzare questa riga per il blocco della "password":

```
 password    optional    pam_gnome_keyring.so

```

	Al seguente accesso, dovrebbe venir richiesto se si desidera che la password venga sbloccata automaticamente al login.

#### KDE

**Nota:** Vedere [http://live.gnome.org/GnomeKeyring/Pam](http://live.gnome.org/GnomeKeyring/Pam) per maggiori informazioni, e se si utilizza kde / kdm, è possibile avvalersi di pam-keyring-tool da AUR.

*   Mettere uno script come il seguente in `~/.kde4/Autostart`:

```
 $!/bin/sh
 echo PASSWORD | /usr/bin/pam-keyring-tool --unlock --keyring=default -s

```

	Script simili dovrebbero funzionare anche con openbox, LXDE, ecc.

#### SLiM login manager

*   Aggiungere queste righe in `/etc/pam.d/slim`, alla fine dei blocchi "auth" e "session" in caso non siano specificate ancora:

```
 auth            optional        pam_gnome_keyring.so
 session         optional        pam_gnome_keyring.so  auto_start

```

*   In `/etc/pam.d/passwd`, utilizzare questa riga per il blocco 'password':

```
 password    optional    pam_gnome_keyring.so

```

	Al seguente login, verrà richiesto se si desidera che la password venga sbloccata automaticamente al login.

### Ignorare dispositivi specifici

A volte potrebbe tornare utile che network manager ignori alcuni dispositivi e non provi ad ottenere un indirizzo IP.

	1\. Ignorare device dall'indirizzo MAC: usare il seguente modo in {{`/etc/NetworkManager/NetworkManager.conf` :

```
[keyfile]
unmanaged-devices=mac:00:22:68:1c:59:b1;mac:00:1E:65:30:D1:C4

```

	Dopo di ciò [riavviare](/index.php/Demoni "Demoni") NetworkManager e verificarne il funzionamento.

	2\. In alternativa si può usare Hal.

*   Prima di tutto bisogna trovare l'UDI di Hal (es. con `lshal`):

```
 ...
 info.product = 'Networking Interface'  (string)
 info.subsystem = 'net'  (string)
 info.udi = '/org/freedesktop/Hal/devices/net_00_1f_11_01_06_55'  (string)
 linux.hotplug_type = 2  (0x2)  (int)
 linux.subsystem = 'net'  (string)
 ...

```

*   Aggiungere l'UDI a `/etc/NetworkManager/nm-system-settings.conf`:

```
 [keyfile]
   unmanaged-devices=/org/freedesktop/Hal/devices/net_00_1f_11_01_06_55

```

	Possono venire specificati dispositivi multipli, delimitati da punti e virgola:

```
 [keyfile]
   unmanaged-devices=/org/freedesktop/Hal/devices/net_00_1f_11_01_06_55;/org/freedesktop/Hal/devices/net_00_2c_6d_e2_08_af

```

Non è necessario riavviare NetworkManager perchè le modifiche abbiano effetto.

	3\. Ignorare un tipo di dispositivo in fase di boot usando questo script (cambiare `NetworkManager.conf` com `nm-system-settings.conf` per versioni di Networkmanager precedenti alla 0.8.1):

```
  #!/bin/sh
  # author: tim noise <darknoise@drkns.net>
  COUNT=0
  TARGET_FILE="/etc/NetworkManager/nm-system-settings.conf"
  for i in `lshal | grep -A6 'Networking Interface' | awk -F "'" '/info.udi = / {print $2}'`; do
      if [ $COUNT = 0 ]; then
          COUNT=$COUNT+1;
          echo "unmanaged-devices=$i" >> $TARGET_FILE
      else
          echo -n ";$i" >> $TARGET_FILE
      fi
  done
  printf "
" >> $TARGET_FILE

```

	Tale script può essere adattato per ignorare dei Device wireless, usato su filesysten non persistenti, ecc...

### Connessioni più veloci

#### Collegarsi più velocemente disabilitando IPv6

Se non c'è il supporto IPv6 sulla rete locale, la connessione a una rete può richiedere più tempo del normale, mentre Network Manager cerca di stabilire una connessione IPv6 e magari, alla fine, andare in time out. La soluzione è quella di disabilitare IPv6 all'interno di Network Manager. Questo deve essere fatto una sola volta per ogni rete a cui ci si connette.

*   Fare clic destro sull'icona di stato della rete.
*   Cliccare su "Modifica connessioni".
*   Andare su "Wired" o "Wireless", a seconda dei casi.
*   Selezionare il nome della rete.
*   Cliccare su "Modifica".
*   Andare alla sezione "Impostazioni IPv6".
*   Nel menu a discesa "Metodo", scegliere "Ignora".
*   Cliccare su "Salva".

#### Speed up DHCP by disabling ARP probing in dhcpcd

`dhcpcd` contiene un'implementazione di una raccomandazione agli standard DHCP (RFC2131 sezione 2.2) per assicurarsi via ARP che l'IP assegnato non sia già in uso. Potrebbe sembrare inutile in una rete domestica, ma si possono **risparmiare fino a 5 secondi** sul tempo di connessione aggiungendo a `/etc/dhcpcd.conf`:

```
noarp

```

Questo equivale a lanciare dhcpd con il flag *--noarp*, questo disabilita il sondaggio ARP velocizzando la connessione con DHCP.

#### Usare Servers OpenDNS

Creare il file `/etc/resolv.conf.opendns` con i nameservers:

```
nameserver 208.67.222.222
nameserver 208.67.220.220

```

Per sostituire i server DHCP con gli OpenDNS:

 `/etc/NetworkManager/dispatcher.d/dns-servers-opendns` 
```
#!/bin/bash
# Use OpenDNS servers over DHCP discovered servers

cp -f /etc/resolv.conf.opendns /etc/resolv.conf
```

Rendere eseguibile lo script:

```
# chmod +x /etc/NetworkManager/dispatcher.d/dns-servers-opendns

```