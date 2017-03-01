**Samba** è una re implementazione del protocollo di rete SMB/CIFS, serve per facilitare la condivisione di file e stampanti tra sistemi Linux e Windows, come alternativa ad [NFS](/index.php/NFS_(Italiano) "NFS (Italiano)"). Samba è facilmente configurabile e le opzioni sono molto chiare. In ogni caso, gli utenti meno esperti potrebbero incontrare problemi per la sua complessità e per i meccanismi non intuitivi. Si consiglia quindi di attenersi alle seguenti indicazioni.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Configrazione base](#Configrazione_base)
    *   [2.2 Opzioni della shell](#Opzioni_della_shell)
        *   [2.2.1 Aggiungere gli utenti](#Aggiungere_gli_utenti)
    *   [2.3 Opzioni web](#Opzioni_web)
        *   [2.3.1 SWAT: Samba web administration tool](#SWAT:_Samba_web_administration_tool)
*   [3 Accedere alle condivisioni](#Accedere_alle_condivisioni)
    *   [3.1 Accedere alle condivisioni Samba da GNOME/Xfce4](#Accedere_alle_condivisioni_Samba_da_GNOME.2FXfce4)
    *   [3.2 Accedere alle condivisioni da altri ambienti grafici](#Accedere_alle_condivisioni_da_altri_ambienti_grafici)
    *   [3.3 Accedere ad una condivisione Samba tramite shell](#Accedere_ad_una_condivisione_Samba_tramite_shell)
        *   [3.3.1 Mount automatico](#Mount_automatico)
            *   [3.3.1.1 smbnetfs](#smbnetfs)
            *   [3.3.1.2 fusesmb](#fusesmb)
            *   [3.3.1.3 Autofs](#Autofs)
        *   [3.3.2 Montare manualmente una condivisione](#Montare_manualmente_una_condivisione)
            *   [3.3.2.1 Aggiungere una condivisione in fstab](#Aggiungere_una_condivisione_in_fstab)
            *   [3.3.2.2 Permettere agli utenti di montare le condivisioni](#Permettere_agli_utenti_di_montare_le_condivisioni)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Condividere file sulla propria rete senza la richiesta di utente e password](#Condividere_file_sulla_propria_rete_senza_la_richiesta_di_utente_e_password)
        *   [4.1.1 Opzione 1 - Forzare le connessioni guest](#Opzione_1_-_Forzare_le_connessioni_guest)
        *   [4.1.2 Opzione 2 - Permettere le connessioni guest ed Utente](#Opzione_2_-_Permettere_le_connessioni_guest_ed_Utente)
    *   [4.2 Esempio di configurazione](#Esempio_di_configurazione)
        *   [4.2.1 Global Parameters](#Global_Parameters)
        *   [4.2.2 Condivisioni](#Condivisioni)
    *   [4.3 Individuare le condivisioni di rete](#Individuare_le_condivisioni_di_rete)
    *   [4.4 Controllare da remoto i computer Windows](#Controllare_da_remoto_i_computer_Windows)
    *   [4.5 Bloccare determinate estenzioni di file extensions sulle condivisioni samba](#Bloccare_determinate_estenzioni_di_file_extensions_sulle_condivisioni_samba)
*   [5 Risoluzione di problemi](#Risoluzione_di_problemi)
    *   [5.1 Windows 7 problemi di connettività - mount error(12): cannot allocate memory](#Windows_7_problemi_di_connettivit.C3.A0_-_mount_error.2812.29:_cannot_allocate_memory)
    *   [5.2 Problemi con gli accessi da Windows a condivisioni protette da password](#Problemi_con_gli_accessi_da_Windows_a_condivisioni_protette_da_password)
    *   [5.3 Lentezza nell'apparsa della finestra per l'accesso](#Lentezza_nell.27apparsa_della_finestra_per_l.27accesso)
    *   [5.4 Cambiamenti in Samba versione 3.4.0](#Cambiamenti_in_Samba_versione_3.4.0)
    *   [5.5 Error: Value too large for defined data type](#Error:_Value_too_large_for_defined_data_type)
    *   [5.6 Devo riavviare Samba per rendere le condivisioni visibili agli altri pc](#Devo_riavviare_Samba_per_rendere_le_condivisioni_visibili_agli_altri_pc)
*   [6 Risorse](#Risorse)

## Installazione

Installare [smbclient](https://www.archlinux.org/packages/?name=smbclient) per l'installazione del solo **client** è sufficiente per quei computer che non dovranno condividere file, ma solo accedervi.

Per poter condividere delle cartelle, installare il pacchetto **server** [samba](https://www.archlinux.org/packages/?name=samba) (che include anche [smbclient](https://www.archlinux.org/packages/?name=smbclient) come sua dipendenza).

## Configurazione

### Configrazione base

Il file `/etc/samba/smb.conf` deve essere creato prima di avviare il demone. Una volta creato, gli utenti possono optare per una interfaccia di configurazione avanzata come [SWAT](#SWAT:_Samba_web_administration_tool), invece di editare il file manualmente.

Da root, copiare il file di configurazione di default in `/etc/samba/smb.conf`:

```
# cp /etc/samba/smb.conf.default /etc/samba/smb.conf

```

Aprire il file `smb.conf` e modificarlo secondo le necessità. La configurazione di default prevede la condivisione della cartella `home` di ogni utente. Crea inoltre una condivisione per le stampanti.

Maggiori informazioni riguardo alle opzioni disponibili possono essere trovate eseguendo il comando:

```
$ man smb.conf

```

Per avviare automaticamente `samba` all'avvio, aggiungerlo all'array `[DAEMONS](/index.php/Daemon_(Italiano) "Daemon (Italiano)")` in `/etc/rc.conf`.

### Opzioni della shell

#### Aggiungere gli utenti

Per accedere ad una condivisione Samba, sarà necessario aggiungere un utente samba.

Per Samba a partire dalla versione 3.4.0 e successive:

```
# pdbedit -a -u <user>

```

Per le precedenti versioni di Samba:

```
# smbpasswd -a <user>

```

Il database delle password smbpasswd può anche essere [convertito al nuovo formato](#Cambiamenti_in_Samba_versione_3.4.0).

L'utente dovrà avere già un account di sistema sul server. Se l'utente non esiste si otterrà un errore:

```
Failed to modify password entry for user "<user>"

```

Per aggiungere un nuovo utente di sistema Linux si può usare [adduser](/index.php/Users_and_groups_(Italiano)#Gestione_degli_utenti "Users and groups (Italiano)"). Questo articolo non spiega come aggiungere utenti su sistemi Windows.

**Nota:** smbpasswd non è più il metodo di default per le autenticazioni Samba a partire da [Samba versione 3.4.0](#Cambiamenti_in_Samba_versione_3.4.0)

### Opzioni web

#### SWAT: Samba web administration tool

[SWAT](http://samba.xsec.it/samba/docs/man/Samba-HOWTO-Collection/SWAT.html) è una comodità per Samba. Il programma principale si chiama swat e viene avviato attraverso il demone [xinetd](https://en.wikipedia.org/wiki/xinetd "wikipedia:xinetd") (ovvero eXtended InterNET Daemon).

Ci sono diverse opinioni riguardo l'effettiva utilità di SWAT. Non importa quanto impegno si metta per produrre un tool di configurazione perfetto, rimarrà sempre una questione soggettiva ritenerlo utile. SWAT è un tool che attraverso un interfaccia Web, permette di configurare Samba. Sarà possibile effettuare una configurazione guidata per velocizzare e semplificare la configurazione, dispone dell'aiuto contestuale per ogni parametro del file `smb.conf`, permette inoltre di monitorare il corrente stato delle connessioni, ed anche di gestire le password di rete MS Windows [[1]](http://samba.xsec.it/samba/docs/man/Samba-HOWTO-Collection/SWAT.html).

**Nota:** In caso di problemi con SWAT, si può usare il più ampio tool di configurazione [Webmin](/index.php/Webmin_(Italiano) "Webmin (Italiano)"), e semplicemente caricare il relativo modulo SWAT.

**Attenzione:** Prima di usare SWAT. SWAT sostituirà se esiste il file `smb.conf` con un file più ottimizzato contenente i soli valori non di default e privo di commenti(anche di quelli inseriti dall'utente) .

Per usare SWAT, si dovrà prima installare il pacchetto [xinetd](https://www.archlinux.org/packages/?name=xinetd).

Modificare con un editor di testo il file `/etc/xinetd.d/swat`. Per abilitare SWAT, cambiare la linea `disable = yes` in `disable = no`.

```
service swat
{
        type                    = UNLISTED
        protocol                = tcp
        port                    = 901
        socket_type             = stream
        wait                    = no
        user                    = root
        server                  = /usr/sbin/swat
        log_on_success          += HOST DURATION
        log_on_failure          += HOST
        disable                 = no
}

```

In alternativa è possibile aggiungere il servizio swat e la relativa porta al file `/etc/services` ed omettere le prime 3 righe della configurazione.

Successivamente avviare il [demone](/index.php/Daemon_(Italiano) "Daemon (Italiano)") xinetd.

L'interfaccia web è raggiungibile dalla porta di default, 901,

```
[http://localhost:901/](http://localhost:901/)

```

## Accedere alle condivisioni

Le risorse condivise dagli altri computer sulla rete sono accessibili e posso essere montate tramite interfacce grafiche(GUI) oppure attraverso la linea di comando(CLI). L’uso dell’interfaccia grafica è meno diffusa. Solo alcuni Desktop Environments dispongono di apposite utility per accedere alle risorse condivise. Comunque la maggior parte non ne dispone. Infatti, i più leggeri DE e Window Manager non dispongono di metodi grafici nativi.

Ci sono due fasi nell’accesso alle condivisioni. La prima è il meccanismo di basso livello del file system, e la seconda è l’interfaccia grafica che consente all’utente di montare le risorse condivise. Alcuni Desktop Environments hanno la prima parte integrata in essi.

Se si usa KDE, si ha la possibilità di vedere le condivisioni Samba. Non sarà quindi necessario installare pacchetti addizionali (comunque per avere un'interfaccia per la configurazione all'interno della schermata "Impostazioni di Sistema" sarà necessario installare il pacchetto kdenetwork-filesharing dal repository [extra]. Un'alternativa è SMB4K.). Se invece, si vuole accedere alle condivisioni da GNOME oppure dalla shell, sarà necessario installare dei pacchetti aggiuntivi.

### Accedere alle condivisioni Samba da GNOME/Xfce4

Per poter accedere alle condivisioni Samba da GNOME Files sarà necessario installare i pacchetti [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb) e [gnome-vfs](https://aur.archlinux.org/packages/gnome-vfs/)

Per potervi accedere usando thunar in Xfce4 sarà necessario installare solamente [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb)

Dalla finestra di Files/Thunar, premere `Ctrl`+`l` oppure andare sul menù "Vai" e selezionare "Posizione..." -- entrambe le azioni porteranno il cursore nella barra del percorso. Digitare:

```
smb://nome_server/condivisione

```

**Nota:** Se non è stato inserito il nome server nel file `/etc/hosts`, si dovrà inserire l'indirizzo IP del server invece del nome.

Un altro programma per GNOME è Gnomba.

Se si utilizza [iptables](https://www.archlinux.org/packages/?name=iptables) sul proprio sistema, sarà necessario aver caricato il modulo `nf_conntrack_netbios_ns`

```
modprobe nf_conntrack_netbios_ns

```

### Accedere alle condivisioni da altri ambienti grafici

Ci sono diversi programmi utili, ma sarà necessario compilarsi il pacchetto per installarli. Ciò può essere fatto tramite gli strumenti di pacchettizzazione di Arch. Un vantaggio di questi programmi è che non necessitano di particolari ambienti per essere supportati, e quindi non hanno molte dipendenze.

LinNeighborhood è non è legato a nessun DE o WM. Può essere visto come un semplice generico browser di rete con interfaccia grafica, che permette il mount delle condivisioni. Non molto curato graficamente, ma efficiente.

Altri possibili programmi includono pyneighborhood e RUmba, inoltre anche il plugin xffm-samba per Xffm.

### Accedere ad una condivisione Samba tramite shell

Si può accedere alle condivisioni montandole automaticamente oppure [manualmente](#Montare_manualmente_una_condivisione).

#### Mount automatico

Ci sono diverse alternative per un accesso semplice alle condivisioni.

##### smbnetfs

1\. Installare [smbnetfs](https://www.archlinux.org/packages/?name=smbnetfs).

2\. Aggiungere la seguente linea al file `/etc/fuse.conf`:

```
user_allow_other

```

3\. Caricare il modulo `fuse`:

```
# modprobe fuse

```

4\. Avviare il [demone](/index.php/Daemon_(Italiano) "Daemon (Italiano)") `smbnetfs`.

Tutte le condivisioni nella rete saranno montate automaticamente in `/mnt/smbnet`.

Modificare il file il file `/etc/rc.conf` per montare le condivisioni durante l'avvio del sistema, aggiungendo il modulo `fuse` all'array `MODULES` ed il [demone](/index.php/Daemon_(Italiano) "Daemon (Italiano)") `smbnetfs` all'array `DAEMONS`.

Se le condivisioni necessitano di un utente ed una password per l'accesso, sarà necessario modificare il file `/etc/smbnetfs/.smb/smbnetfs.conf` de commentando la linea che inizia con "auth", e modificandola secondo le esigenze:

```
auth			"WORKGROUP/username" "password"

```

Può essere necessario la modificare i permessi sul file `/etc/smbnetfs/.smb/smbnetfs.conf`, e di tutti i file inclusi in esso, per far sì che il sevizio funzioni correttamente:

```
# chmod 600 /etc/smbnetfs/.smb/smbnetfs.conf

```

##### fusesmb

**Nota:** Dato che `smbclient 3.2.x` non funziona correttamente con `fusesmb`, è preferibile effettuare il downgrade se necessario. Consultare il [topic sul forum](https://bbs.archlinux.org/viewtopic.php?id=58434) per maggiori informazioni.

1\. Installare [fusesmb](https://aur.archlinux.org/packages/fusesmb/) da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").

2\. Creare il punto di mount:

```
# mkdir /mnt/fusesmb

```

3\. Caricare il modulo `fuse`:

```
# modprobe fuse

```

4\. Montare la condivisione:

```
# fusesmb -o allow_other /mnt/fusesmb

```

Per effettuare il mount automaticamente all'avvio, aggiungere il comando precedente nel file `/etc/rc.local` ed aggiungere il modulo `fuse` nell'array `MODULES` nel file `/etc/rc.conf`.

##### Autofs

Consultare la pagina relativa ad [Autofs](/index.php/Autofs_(Italiano) "Autofs (Italiano)") per maggiori informazioni riguardo al mount automatico implementato nel kernel Linux.

#### Montare manualmente una condivisione

1\. Usare [smbclient](https://www.archlinux.org/packages/?name=smbclient) per esplorare le condivisioni dalla shell. Per ottenere l'elenco delle condivisioni pubbliche da un server:

```
$ smbclient -L <hostname> -U%

```

2\. Creare il punto di mount per la condivisione:

```
# mkdir /mnt/PUNTODIMOUNT

```

3\. Montare la condivisione usando `mount.cifs`. Ricordare che non tutte le opzioni sono sempre necessarie o consigliate, ad esempio l'opzione `password`:

```
# mount -t cifs //*SERVER*/*CONDIVISIONE* *PUNTODIMOUNT* -o user=*NOMEUTENTE*,password=*PASSWORD*,workgroup=*WORKGROUP*,ip=*IPSERVER*

```

	`SERVER`

	Il nome macchina Windows

	`CONDIVISIONE`

	Nome della condivisione

	`PUNTODIMOUNT`

	La cartella locale dove sarà montata la condivisione

	`-o [options]`

	Specifica la presenza di opzioni al comando `mount.cifs`

	`user`

	Il nome utente necessario per l'accesso alla condivisione

	`password`

	La password di accesso alla condivisione

	`workgroup`

	Serve per specificare il gruppo di lavoro Windows

	`ip`

	L'indirizzo IP del server --Se il sistema non può identificare il server tramite il nome(DNS, WINS, il file hosts, etc.)

**Nota:** Evitare di usare i delimitatori delle cartelle (**/**) alla fine del percorso. Usando `//SERVER/CONDIVISIONE**/**` non funzionerà.

Dato che CIFS rifiuta di effettuare il mount [di condivisioni samba non protette](http://jmatrix.net/dao/case/case.jsp?case=7F000001-1766806-11E30195CFB-2593), si deve utilizzare l'opzione `sec=none`(ed il nome utente e la password dalla lista delle opzioni precedente dovranno essere rimosse).

Se il comando `mount` non riesce a risolvere l'indirizzo del server, ma `smbclient` può, aggiungere la voce `wins` alla linea `hosts` nel file `/etc/[nsswitch.conf](/index.php?title=Nsswitch.conf&action=edit&redlink=1 "Nsswitch.conf (page does not exist)")` può aiutare. Il corrispondente driver `/lib/libnss_wins.so` deve essere presente, esso è fornito dal pacchetto (del servizio) [samba](https://www.archlinux.org/packages/?name=samba).

4\. Per smontare la condivisione usare il comando:

```
# umount /mnt/PUNTODIMOUNT

```

##### Aggiungere una condivisione in fstab

Aggiungere la seguente linea al file `/etc/[fstab](/index.php/Fstab_(Italiano) "Fstab (Italiano)")` per un mount rapido:

```
//SERVER/CONDIVISIONE /mnt/PUNTODIMOUNT cifs noauto,noatime,username=NOMEUTENTE,password=PASSWORD,workgroup=WORKGROUP,ip=SERVERIP 0 0

```

L'opzione `noauto` impedisce il mount automatico all'avvio mentre `noatime` aumenta le prestazioni non aggiornando i tempi di accesso ai file.

Dopo aver aggiunto la precedente linea, la sintassi del comando `mount` diventa più semplice:

```
# mount /mnt/PUNTODIMOUNT

```

Un'altra opzione, per non avere le password in chiaro, è quella di usare l'opzione `credentials`:

```
//SERVER/CONDIVISIONE /percorso/di/MOUNT cifs noauto,noatime,credentials=/percorso/per/credenzialismb 0 0

```

Il file delle credenziali dovrebbe contenere il seguente testo:

```
username=USERNAME
password=PASSWORD

```

Per maggiore sicurezza è possibile assegnare i permessi tramite il comando `chmod 700` a questo file in modo da impedirne la lettura e la scrittura da parte di altri utenti.

Se si aggiunge una condivisione nel file `fstab`, il demone `netfs` dovrà essere aggiunto nell'array `DAEMONS` in rc.conf, dopo [network](/index.php/Configuring_Network_(Italiano) "Configuring Network (Italiano)"). Il demone `netfs` si occuperà di montare le condivisioni durante la fase di avvio e, cosa più importante, di smontarle durante la fase di arresto del sistema. Anche se viene utilizzata l'opzione `noauto` in `fstab`, il demone `netfs` dovrebbe essere usato. Senza di esso se una condivisione fosse montata, durante la fase di spegnimento porterebbe il demone `network` ad attendere il time out della connessione, aumentando quindi la durata di arresto del sistema.

##### Permettere agli utenti di montare le condivisioni

Prima abilitare l'accesso al comando mount, il file `fstab` dovrà essere modificato. Aggiungere l'opzione `users` nella voce in `/etc/fstab`:

```
//SERVER/CONDIVISIONE /percorso/del/PUNTODIMOUNT cifs **users**,noauto,noatime,username=NOMEUTENTE,password=PASSWORD,workgroup=WORKGROUP,ip=SERVERIP 0 0

```

**Nota:** Questa è l'opzione `user**s**`(al plurale). Per altri tipi di filesystem, questa opzione è *user*, senza la "**s**".

Questo permetterà agli utenti di montatre la condivisione se il suo punto di mount si trova in una cartella *controllabile* dall'utente; ad esempio la propria cartella home. Per montare le condivisioni Samba in punti di mount che non si posseggono, utilizzare [#smbnetfs](#smbnetfs) oppure elevare i privilegi tramite [sudo](/index.php/Sudo_(Italiano) "Sudo (Italiano)").

## Tips and tricks

### Condividere file sulla propria rete senza la richiesta di utente e password

#### Opzione 1 - Forzare le connessioni guest

Modificare il file `/etc/samba/smb.conf` cambiando la seguente linea:

```
security = user

```

in

```
security = share

```

#### Opzione 2 - Permettere le connessioni guest ed Utente

Modificare il file `/etc/samba/smb.conf` aggiungendo la seguente linea:

```
map to guest = Bad User

```

Dopo questa linea

```
security = user

```

Se si vuole restringere la condivisione ad una specifica interfaccia di rete, sostituire:

```
;   interfaces = 192.168.12.2/24 192.168.13.2/24

```

con:

```
interfaces = lo eth0
bind interfaces only = true

```

(cambiando `eth0` con il nome dell'interfaccia connessa alla rete con la quale si vuole effettuare la condivisione)

Se si vuole è possibile modificare l'account che accede alle condivisioni, cambiando la seguente linea:

```
;   guest account = nobody

```

L'ultimo passo consiste nel creare le condivisioni(per garantire il permesso in scrittura usare l'opzione `writable = yes`):

```
[Public Share]
path = /percorso/alla/condivisione_pubblica
available = yes
browsable = yes
public = yes
writable = no

```

### Esempio di configurazione

Questo è un esempio di configurazione funzionante:

```
[global]
workgroup = WORKGROUP
server string = Samba Server
netbios name = PC_NAME
security = share
; la seguente linea è importante! In caso di problemi di permessi
; assicurarsi che l'utente di seguito sia il solito che possiede
; la cartella che si condivide
guest account = mark
username map = /etc/samba/smbusers
name resolve order = hosts wins bcast
wins support = no

[public]
comment = Public Share
path = /path/to/public/share
available = yes
browsable = yes
public = yes
writable = no

```

#### Global Parameters

La prima sezione del file `smb.conf` serve a configurare i parametri globali, la gran parte delle modifiche sarà effettuata qua. Segue un esempio di sezione Global Parameters:

```
#Global Parameters
workgroup = HOME
netbios name = nome-della-macchina
encrypt passwords = yes

```

Il parametro *workgroup* imposta il nome del gruppo di lavoro al quale volete che la macchina appartenga. Il parametro *encrypt passwords* deve essere mantenuto a *yes* a meno che in rete non siano presenti macchine Windows 95 o Windows 98, questi due sistemi infatti non supportano le password criptate. Infine il parametro "netbios name" è il nome che desiderate assegnare alla macchina su cui state lavorando all'interno della rete.

#### Condivisioni

A seguito si trova la configurazione delle condivisioni. La condivisione più semplice possibile sarà quella in cui un utente può accedere e scrivere nella propria home direcotry. Per fare ciò nel file smb.conf saranno presenti le righe:

```
[homes]
browseable = no
read only = no

```

Se si vuole che tutti possano vedere i file, ma solo gli utenti appartenenti ad alcuni gruppi abbiano diritto di scrittura, allora sarà necessario cambiare le righe precedenti in:

```
[homes]
public = yes
writable = yes
write list = @nome-gruppo

```

Se vogliamo che gli utenti windows una volta loggati vedano una direcotry home "pulita" (ovvero non i file nascosti, es: `~/.bashrc`), allora la sezione homes potrebbe essere:

```
[homes]
path = /home/%u/smb
browseable = no
read only = no

```

In questo caso però assicurasi di aggiungere la cartella `smb` alle home directory degli utenti. Inoltre aggiungere `smb` alla direcotry `/etc/skel`, in modo che tutti i nuovi utenti abbiano `~/smb` aggiunto in automatico alla creazione:

```
# mkdir /etc/skel/smb

```

Aggiungere altre condivisioni differenti dalle direcotry home non è più difficile, anzi. Per aggiungere un'ulteriore condivisione:

```
[music]
path = /mnt/windows/Music/
browseable = yes
read only = yes
valid users = Bryan, Michael, David, Jane

```

Il parametro `path` indica la posizione della direcotry che si vuole condividere. Il parametro `valid users` comunica a samba quali utenti hanno diritto di accedere a questa condivisione. Una volta aggiunte tutte le condivisioni necessarie, salvare il file ed uscire dall'editor.

**Nota:** I nomi utente inseriti nel file di configurazione **devono** coincidere con gli utenti di sistema della macchina Linux ed **è consigliato** che coincidano anche con quelli presenti sulle macchine Windows.

### Individuare le condivisioni di rete

Se non si conosce la struttura della rete locale, e gli strumenti di automazione come [#smbnetfs](#smbnetfs) non sono disponibili, i seguenti metodi permetteranno di individuare le condivisioni Samba.

1\. Per prima cosa, [installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") [nmap](https://www.archlinux.org/packages/?name=nmap) e [smbclient](https://www.archlinux.org/packages/?name=smbclient).

2\. `nmap` controlla quali porte sono aperte:

```
# nmap -sT 192.168.1.*

```

In questo esempio verrà scansionata l'intera classe di indirizzi 192.168.1.*. Ecco il risultato:

 `$ nmap -sT 192.168.1.*` 
```
Starting nmap 3.78 ( http://www.insecure.org/nmap/ ) at 2005-02-15 11:45 PHT
Interesting ports on 192.168.1.1:
(The 1661 ports scanned but not shown below are in state: closed)
PORT     STATE SERVICE
'''139/tcp  open  netbios-ssn'''
5000/tcp open  UPnP

Interesting ports on 192.168.1.5:
(The 1662 ports scanned but not shown below are in state: closed)
PORT     STATE SERVICE
6000/tcp open  X11

Nmap run completed -- 256 IP addresses (2 hosts up) scanned in 7.255 seconds

```

Il primo indirizzo(192.168.1.1) è un altro pc, mentre il secondo è il computer da cui è stata lanciata la scansione.

3\. Adesso verso il sistema che risulta avere la porta 139 aperta, sarà usato `nmblookup` per ottenere i nomi delle condivisioni(NetBIOS names):

 `$ nmblookup -A 192.168.1.1` 
```
Looking up status of 192.168.1.1
        PUTER           <00> -         B <ACTIVE>
        HOMENET         <00> - <GROUP> B <ACTIVE>
        PUTER           <03> -         B <ACTIVE>
        '''PUTER           <20> -         B <ACTIVE>'''
        HOMENET         <1e> - <GROUP> B <ACTIVE>
        USERNAME        <03> -         B <ACTIVE>
        HOMENET         <1d> -         B <ACTIVE>
        MSBROWSE        <01> - <GROUP> B <ACTIVE>

```

Senza preoccuparsi dei vari risultati, cercare il valore **<20>**, che indica la macchina con la condivisione file attiva.

4\. Usare `smbclient` per elencare quali servizi sono condivisi da *PUTER*. Nel caso fosse richiesta una password, premendo invio verrà comunque mostrata la lista:

 `$ smbclient -L \\PUTER` 
```
Sharename       Type      Comment
---------       ----      -------
MY_MUSIC        Disk
SHAREDDOCS      Disk
PRINTER$        Disk
PRINTER         Printer
IPC$            IPC       Remote Inter Process Communication

Server               Comment
---------            -------
PUTER

Workgroup            Master
---------            -------
HOMENET               PUTER

```

Questo mostra quali cartelle sono condivise, e quindi possono essere montate localmente. Vedi [#Accedere alle condivisioni](#Accedere_alle_condivisioni)

### Controllare da remoto i computer Windows

Samba offre una serie di strumenti per comunicare con Windows. Questi possono essere utili nel caso no si possa prendere il controllo di questi tramite il desktop remoto, ecco alcuni esempi.

*   Inviare il segnale di shutdown con un commento:

```
$ net rpc shutdown -C "commento" -I INDIRIZZOIP -U NOMEUTENTE%PASSWORD

```

Se si preferisce forzare lo spegnimento, sostituire l'opzione `-C "commento"` con `-f`. In caso si voglia eseguire un riavvio aggiungere `-r`, seguito da `-C "commento"` oppure `-f`.

*   Fermare ed avviare servizi:

```
$ net rpc service stop NOMESERVIZIO -I INDIRIZZOIP -U NOMEUTENTE%PASSWORD

```

*   Per vedere tutti i possibili comandi `net rpc`:

```
$ net rpc

```

### Bloccare determinate estenzioni di file extensions sulle condivisioni samba

Samba permette come opzione di bloccare i file corrispondenti ad un determinato pattern, come un estensione. Questa opzione può essere usata per impedire la diffusione di virus oppure dissuadere gli utenti dallo spercare spazio con determinati file:

```
Veto files = /*.exe/*.com/*.dll/*.bat/*.vbs/*.tmp/*.mp3/*.avi/*.mp4/*.wmv/*.wma/

```

## Risoluzione di problemi

### Windows 7 problemi di connettività - mount error(12): cannot allocate memory

Un noto bug di Windows 7 che causa l'errore "mount error(12): cannot allocate memory" su di una condivisione cifs perfettamente configrata dal lato Linux, può essere risolto impostando alcune chiavi di regitro sul pc Windows come di seguito:

*   HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management\LargeSystemCache (impostata a 1)

*   HKLM\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters\Size (impostata a 3)

Riavviare il pc Windows per applicare le modifiche.

**Nota:** Cercando su Google si otterranno diversi tweak сhe consigliano agli utenti di aggiungere una chiave per modificare la dimensione "IRPStackSize". Questo non è corretto per sistemare questo problema su Windows 7\. Non lo fate.

[Collegamento](http://alan.lamielle.net/2009/09/03/windows-7-nonpaged-pool-srv-error-2017) all'articolo originale.

### Problemi con gli accessi da Windows a condivisioni protette da password

In caso di problemi di accesso da Windows alle condivisioni protette da password, provare ad aggiungere queste righe al file `/etc/samba/smb.conf`:[[2]](http://blogs.computerworld.com/networking_nightmare_ii_adding_linux)

Notare che si dovrà modificare il file smb.conf **locale** non quello del server

```
[global]
# lanman fix
client lanman auth = yes
client ntlmv2 auth = no

```

### Lentezza nell'apparsa della finestra per l'accesso

Si sono verificati ritardi anche di circa 30 secondi, dalla richiesta di connessione all'apparsa della finestra di accesso, sia utilizzando Windows XP che Windows 7\. E analizzando il log `error.log` compare:

```
[2009/11/11 06:20:12,  0] printing/print_cups.c:cups_connect(103)
Unable to connect to CUPS server localhost:631 - Interrupted system call

```

Dato che il problema si verificava anche se sul server non erano connesse stampanti, la soluzione consiste nell'aggiungere queste righe nella sezione global del file `/etc/samba/smb.conf`

```
load printers = no
printing = bsd
disable spoolss = yes
printcap name = /dev/null

```

```
Non c'è la certezza che tutte queste righe siano effettivamente necessarie, ma in questo modo funziona.

```

### Cambiamenti in Samba versione 3.4.0

Tra le [maggiori innovazioni in Samba 3.4.0](http://www.samba.org/samba/history/samba-3.4.0.html):

Il programma di gestione delle password di default è stato cambiato in favore di 'tdbsam'! Di conseguenza tutte le configurazioni esistenti, che invece utilizzano 'smbpasswd', senza una dichiarazione esplicita risultano non funzionanti.

Se si vuole utilizzare 'smbpasswd' modificare il file `/etc/samba/smb.conf`:

```
passdb backend = smbpasswd

```

oppure convertire a `tdbsam` gli accessi:

```
sudo pdbedit -i smbpasswd -e tdbsam

```

### Error: Value too large for defined data type

Con alcune applicazioni si può ottenere questo errore provando ad aprire un file da una condivisione smbfs/cifs:

```
 Value too large for defined data type

```

La soluzione[[3]](https://bugs.launchpad.net/ubuntu/+bug/479266/comments/5), è aggiungere questa opzione al mount delle condivisioni smbfs/cifs(all'interno del file `/etc/fstab` ad esempio):

```
 ,nounix,noserverino

```

*Testato su Arch Linux aggiornata al 02/12/2009*

### Devo riavviare Samba per rendere le condivisioni visibili agli altri pc

Se dopo l'avvio del computer, le condivisioni samba configurate non sono accessibili da nessun client, controllare:

*   di non aver dimenticato di inserire il demone `samba` all'interno dell'array `DAEMONS` nel file `/etc/rc.conf` (dopo il demone `network` o qualsiasi sia il demone di gestione della rete es.[wicd](https://www.archlinux.org/packages/?name=wicd),[networkmanager](https://www.archlinux.org/packages/?name=networkmanager))
*   che il demone *network* non sia avviato in background (quindi non deve essere preceduto dal simbolo `@` all'interno del suddetto array). Rimuovere il simbolo '`@`' può risolvere il problema. Riavviare e controllare.

Si presume che: quando samba viene avviato, probabilmente il demone `network` non ha ancora finito di avviarsi correttamente, quindi il server samba non identifica l'interfaccia di rete sulla quale stare in ascolto, e quindi fallisce la sua inizializzazione.

## Risorse

*   [Sito ufficiale di Samba (in inglese)](http://www.samba.org/)
*   [Samba: Introduzione (in inglese)](http://www.samba.org/samba/docs/SambaIntro.html)