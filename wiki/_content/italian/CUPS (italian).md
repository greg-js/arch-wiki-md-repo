Dal sito di [CUPS](http://www.cups.org/index.php):

	"*[CUPS](https://en.wikipedia.org/wiki/it:CUPS "wikipedia:it:CUPS") è il sistema di stampa, standard e open source, sviluppato da Apple Inc. per Mac OS® X e altri sistemi operativi UNIX®-like.*"

Anche se ci sono altri sistemi di stampa come LPRNG, il Common Unix Printing System è la scelta più popolare per la sua relativa facilità d'uso.

## Contents

*   [1 Cups Linux Printing workflow](#Cups_Linux_Printing_workflow)
*   [2 Installare il client](#Installare_il_client)
    *   [2.1 Configurazione avanzata della rete](#Configurazione_avanzata_della_rete)
*   [3 Installare il server](#Installare_il_server)
    *   [3.1 Driver per la stampante](#Driver_per_la_stampante)
        *   [3.1.1 Scaricare il PPD della stampante](#Scaricare_il_PPD_della_stampante)
        *   [3.1.2 Un'altra risorsa per i driver](#Un.27altra_risorsa_per_i_driver)
*   [4 Configurazione e supporto hardware](#Configurazione_e_supporto_hardware)
    *   [4.1 Moduli del kernel](#Moduli_del_kernel)
        *   [4.1.1 Stampanti USB](#Stampanti_USB)
        *   [4.1.2 Auto-loading](#Auto-loading)
        *   [4.1.3 Stampanti con porta parallela](#Stampanti_con_porta_parallela)
    *   [4.2 Stampanti HP](#Stampanti_HP)
*   [5 Configurazione](#Configurazione)
    *   [5.1 Avviare CUPS al boot](#Avviare_CUPS_al_boot)
    *   [5.2 Interfaccia web e strumenti](#Interfaccia_web_e_strumenti)
        *   [5.2.1 Amministrazione di CUPS](#Amministrazione_di_CUPS)
        *   [5.2.2 Accesso remoto all'interfaccia web](#Accesso_remoto_all.27interfaccia_web)
    *   [5.3 Configurazione CLI](#Configurazione_CLI)
    *   [5.4 Interfaccia CUPS di GNOME](#Interfaccia_CUPS_di_GNOME)
*   [6 Stampante virtuale PDF](#Stampante_virtuale_PDF)
    *   [6.1 Stampare su Postscript](#Stampare_su_Postscript)
*   [7 Risoluzione dei Problemi](#Risoluzione_dei_Problemi)
    *   [7.1 Problemi legati all'aggiornamento](#Problemi_legati_all.27aggiornamento)
        *   [7.1.1 CUPS smette di funzionare](#CUPS_smette_di_funzionare)
        *   [7.1.2 Tutti i lavori sono "fermati"](#Tutti_i_lavori_sono_.22fermati.22)
        *   [7.1.3 Tutti i lavori convergono in un "The printer is not responding"](#Tutti_i_lavori_convergono_in_un_.22The_printer_is_not_responding.22)
        *   [7.1.4 La versione PPD non è compatibile con gutenprint](#La_versione_PPD_non_.C3.A8_compatibile_con_gutenprint)
    *   [7.2 Altro](#Altro)
        *   [7.2.1 Errori di permessi CUPS](#Errori_di_permessi_CUPS)
        *   [7.2.2 La stampante HPLIP invia come errore "/usr/lib/cups/backend/hp failed"](#La_stampante_HPLIP_invia_come_errore_.22.2Fusr.2Flib.2Fcups.2Fbackend.2Fhp_failed.22)
        *   [7.2.3 HPLIP tutti i lavori vengono segnati come ultimati ma non si è riusciti a stampare niente](#HPLIP_tutti_i_lavori_vengono_segnati_come_ultimati_ma_non_si_.C3.A8_riusciti_a_stampare_niente)
        *   [7.2.4 hp-toolbox invia come errore, "Unable to communicate with device"](#hp-toolbox_invia_come_errore.2C_.22Unable_to_communicate_with_device.22)
        *   [7.2.5 CUPS risponde '"foomatic-rip" not available/stopped with status 3' con una stampante HP](#CUPS_risponde_.27.22foomatic-rip.22_not_available.2Fstopped_with_status_3.27_con_una_stampante_HP)
        *   [7.2.6 La stampa fallisce segnalando errori di autorizzazione](#La_stampa_fallisce_segnalando_errori_di_autorizzazione)
        *   [7.2.7 Pulsante Stampa bloccato nelle applicazioni GNOME](#Pulsante_Stampa_bloccato_nelle_applicazioni_GNOME)
        *   [7.2.8 Formato supportato sconosciuto: application/postscript](#Formato_supportato_sconosciuto:_application.2Fpostscript)
        *   [7.2.9 Trovare gli URI per i server di stampa Windows](#Trovare_gli_URI_per_i_server_di_stampa_Windows)
        *   [7.2.10 Errore di stampa client-error-document-format-not-supported](#Errore_di_stampa_client-error-document-format-not-supported)
        *   [7.2.11 Errore /usr/lib/cups/backend/hp](#Errore_.2Fusr.2Flib.2Fcups.2Fbackend.2Fhp)
        *   [7.2.12 "Unable to get list of printer drivers"](#.22Unable_to_get_list_of_printer_drivers.22)
        *   [7.2.13 lp: Error - Scheduler Not Responding](#lp:_Error_-_Scheduler_Not_Responding)
        *   [7.2.14 CUPS stampa una pagina vuota e una di errore con HP Laserjet](#CUPS_stampa_una_pagina_vuota_e_una_di_errore_con_HP_Laserjet)
        *   [7.2.15 Errore: "Using invalid Host"](#Errore:_.22Using_invalid_Host.22)
        *   [7.2.16 La stampante non lavora e restituisce come errore "Filter Failed" sull'interfaccia web di CUPS](#La_stampante_non_lavora_e_restituisce_come_errore_.22Filter_Failed.22_sull.27interfaccia_web_di_CUPS)
        *   [7.2.17 La stampante non viene riconosciuta da cups](#La_stampante_non_viene_riconosciuta_da_cups)
*   [8 Vedere anche](#Vedere_anche)

## Cups Linux Printing workflow

Dalla versione 1.5.3-3 di [cups](https://www.archlinux.org/packages/?name=cups), Arch Linux fa uso del nuovo sistema di stampa completamente pdf-based. Per ulteriori informazioni leggere [PDF standard printing job format](http://www.linuxfoundation.org/collaborate/workgroups/openprinting/pdfasstandardprintjobformat) e [Cups filtering chart](https://wiki.linuxfoundation.org/en/OpenPrinting/Database/CUPS-Filter-Chart). Un ottimo punto di partenza per capire meglio come viene gestito l'intero processo di stampa è [questo articolo](http://www.linuxfoundation.org/collaborate/workgroups/openprinting).

Ci sono due modi per configurare una stampante:

*   Se nella propria rete è presente un server linux per la stampa che condivide una stampante, sarà necessario installare solo il client.
*   Se la stampante è collegata direttamente al proprio sistema, o si ha accesso IPP alla stampante, sarà necessario installare un server cups localmente.

## Installare il client

[libcups](https://www.archlinux.org/packages/?name=libcups) è il solo pacchetto necessario ed è possibile installarlo con [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)"). Aggiungere ora l'IP del server o l'hostname nel file `/etc/cups/client.conf`. Finito! Ora ogni applicazione rileverà la stampante condivisa correttamente.

**Nota:** Non è chiaro se questo passaggio funzioni correttamente con cups > 1.6.x, per maggiori informazioni vedere la pagina wiki [CUPS printer sharing](/index.php/CUPS_printer_sharing "CUPS printer sharing").

### Configurazione avanzata della rete

È possibile lanciare l'istanza *cupsd*+*cups-browserd* sul proprio client con l'aiuto di [Avahi](/index.php/Avahi "Avahi") per rintracciare l'IP della stampante. Tale operazione non ha senso che venga svolta su una rete domestica dove si presuppone si conosca a priori la posizione della stampante. Può invece essere molto utile in caso di grandi reti lan, dove IP e hostname della stampante sono ignoti.

**Nota:** Questa caratteristica non è cambiata dalle precedenti versioni di [cups](https://www.archlinux.org/packages/?name=cups) (<1.6.x). L'unica differenza infatti è che fino a CUPS 1.5.x l'interfaccia web non necessitava del demone [avahi](/index.php/Avahi "Avahi"). Per poter cercare con il browser le stampanti condivise della rete da un server cups remoto è necessario avviare anche *cups-browserd* (da cups-filters =< 1.0.26).

## Installare il server

Sono richiesti i seguenti pacchetti che sono tutti [installabili](/index.php/Pacman_(Italiano) "Pacman (Italiano)") dai [repositories ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

*   [cups](https://www.archlinux.org/packages/?name=cups) - Il software CUPS vero e proprio (demone)
*   [ghostscript](https://www.archlinux.org/packages/?name=ghostscript) - L'interprete per il linguaggio PostScript
*   [gsfonts](https://www.archlinux.org/packages/?name=gsfonts) - I font standard GhostScript Type1

Per poter usare le stampanti in rete è necessario installare [avahi](https://www.archlinux.org/packages/?name=avahi). Assicurarsi che **avahi-demon** prima di **cupsd**.

Se il sistema è collegato ad una stampante di rete utilizzando il protocollo [Samba](/index.php/Samba_(Italiano) "Samba (Italiano)") o se il sistema deve essere un server di stampa per i client Windows, installare anche [samba](https://www.archlinux.org/packages/?name=samba).

### Driver per la stampante

Di seguito alcuni pacchetti per i driver. Scegliere il driver appropriato per la stampante da configurare:

*   **[gutenprint](https://www.archlinux.org/packages/?name=gutenprint)** - Una raccolta di driver di alta qualità per stampanti Canon, Epson, Lexmark, Sony, Olympus, e PCL per l'utilizzo con GhostSscript, CUPS, Foomatic, e [GIMP](/index.php/GIMP "GIMP")
*   **[foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db), [foomatic-db-engine](https://www.archlinux.org/packages/?name=foomatic-db-engine), [foomatic-db-nonfree](https://www.archlinux.org/packages/?name=foomatic-db-nonfree), e [cups-filters](https://www.archlinux.org/packages/?name=cups-filters)** - Foomatic è un sistema basato su database per l'integrazione di driver liberi di stampanti con spooler comune in ambiente Unix. L'installazione di foomatic-filters dovrebbe risolvere eventuali problemi se gli errori nei log riportano "stopped with status 22!".
*   **[foo2zjs](https://aur.archlinux.org/packages/foo2zjs/)**- Driver per il protocollo Zjstreame usato dalle stampanti come la HP Laserjet 1018\. Per maggiori informazioni visitare [questo sito](http://foo2zjs.rkkda.com). Foo2zsj è installabile da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").
*   **[hplip](https://www.archlinux.org/packages/?name=hplip)** - Driver GNU/Linux per HP inkjet. Fornisce supporto per le serie DeskJet, OfficeJet, Photosmart, Business Inkjet, alcuni modelli LaserJet e alcune Brother.
*   **[splix](https://www.archlinux.org/packages/?name=splix)** - Driver Samsung per stampanti SPL (Samsung Printer Language).
*   **[samsung-unified-driver](https://aur.archlinux.org/packages/samsung-unified-driver/) - Pacchetto unico per le nuove stampanti Samsung. Tale pacchetto è disponibile su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").**
*   [hpoj](https://aur.archlinux.org/packages/hpoj/) - Se si utilizza una HP Officejet, si dovrebbe installare anche questo pacchetto e seguire le istruzioni per evitare problemi. Leggere questo [thread](https://answers.launchpad.net/hplip/+question/133425) su launchpad/hplip per maggiori informazioni.
*   **[ufr2](https://aur.archlinux.org/packages/ufr2/)** or **[cndrvcups-lb](https://aur.archlinux.org/packages/cndrvcups-lb/)** - Driver Canon UFR2 con supporto per le stampanti serie LBP, iR e MF. I pacchetti sono disponibili su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").
*   **[cups-pdf](https://www.archlinux.org/packages/?name=cups-pdf)** - Un pacchetto che permette di configurare una stampante PDF virtuale e che genera un file PDF dai dati ricevuti in modo automatico.

Se non si è sicuri di quale driver installare o se l'attuale driver non funziona, può essere più semplice installare tutti i driver, dal momento che alcuni dei nomi dei pacchetti sono fuorvianti, in quanto anche stampanti di altre marche possono essere supportate. Per esempio, la Brother HL-2140 ha bisogno del driver HPLIP installato.

#### Scaricare il PPD della stampante

A seconda della stampante, questo passo è opzionale e potrebbe non essere necessario, dal momento che l'installazione standard di CUPS include già un certo numero di file PPD (Postscript Printer Description). Inoltre, i pacchetti *foomatic-filters*, *gimp-print* e *hplip* includono a loro volta dei file PPD, che verranno rilevati automaticamente da CUPS.

Ecco una spiegazione dal sito di stampa di Linux sul significato dei file PPD:

	"*Per ogni PostScript di una stampante, i costruttori forniscono un file PPD, che contiene tutte le informazioni specifiche del particolare modello della stampante: caratteristiche di base della stampante, come ad esempio se è una stampante a colori, i caratteri, il livello PostScript, ecc, e soprattutto le opzioni configurabili dall'utente , la dimensione della carta, la risoluzione, ecc.*"

Se il PPD per la stampante *non* è già incluso in CUPS:

*   controllare su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") per verificare se ci sono i pacchetti per la stampante e/o produttore
*   visitare il database [OpenPrinting](http://www.openprinting.org/printers) e selezionare il produttore e il modello della stampante
*   visitare il sito del produttore per effettuare una ricerca dei driver per GNU/Linux

**Note:** I file PPD sono ubicati in `/usr/share/cups/model/`

#### Un'altra risorsa per i driver

[Turboprint](http://www.turboprint.de/english.html) è una raccolta di driver proprietari per stampanti che normalmente non avrebbero alcun supporto su GNU/Linux (Canon i*, per esempio). Sfortunatamente CUPS, magari, "marchia" con il logo di Turboprint le stampe ad alta qualità agli utenti che non hanno pagato i driver.

## Configurazione e supporto hardware

Si può avere accesso alle stampanti USB in due modi : il modulo del kernel `usbpl` e `lilusb`. Il primo è il metodo classico ed è il più semplice. I dati vengono inviati alla stampante tramite un semplice stream di dati seriali. Lo stesso file ha un accesso "bidirezionale", in modo da consentire di vedere il livello di inchiostro, lo status della stampante ecc. Questo metodo funziona molto bene per le stampanti semplici, non son però supportate stampanti multifunzione, inoltre, alcuni produttori come ad esempio HP forniscono i loro backend. (Per maggiori informazioni cosultare: [questo sito](http://lists.linuxfoundation.org/pipermail/printing-architecture/2012/002412.html)).

### Moduli del kernel

Prima di utilizzare l'interfaccia web di CUPS, si devono installare i moduli del kernel. Le seguenti operazioni sono tratte dalla documentazione di Gentoo.

Questa sezione può non essere necessaria a seconda del kernel utilizzato. Il modulo del kernel può essere caricato automaticamente dopo aver collegato la stampante. Utilizzare il comando `tail` (descritto più sotto) per vedere se la stampante è già stata rilevata. Anche l'utilità `lsmod` può essere utilizzata per vedere quali moduli sono stati caricati.

#### Stampanti USB

**Dalla versione 1.6.0 di cups, non dovrebbe più essere necessario blacklistare `usblp`.** Se si dovesse notare che mettere in blacklist tale modulo fosse l'unica soluzione ad un problema, si prega di riportare un bug all'upstream di Cups. Vedere [questo bug](http://cups.org/str.php?L4128) per maggiori informazioni.

Alcuni utenti, potrebbero comunque ancora voler mettere in blacklist il modulo `usblp`:

 `/etc/modprobe.d/blacklist.conf`  `blacklist usblp` 

Per i kernel personalizzati, potrebbe essere necessario caricare manualmente il modulo `usbcore` prima di procedere:

```
# modprobe usbcore

```

Una volta che i moduli sono installati, collegare la stampante e controllare se il kernel li ha rilevati eseguendo il seguente:

```
# tail /var/log/messages.log

```

o

```
# dmesg

```

Se si sta utilizzando `usblp`, l'uscita dovrebbe indicare che la stampante è stata rilevata in questo modo:

```
Feb 19 20:17:11 kernel: printer.c: usblp0: USB Bidirectional
printer dev 2 if 0 alt 0 proto 2 vid 0x04E8 pid 0x300E
Feb 19 20:17:11 kernel: usb.c: usblp driver claimed interface cfef3920
Feb 19 20:17:11 kernel: printer.c: v0.13: USB Printer Device Class driver

```

Se si ha inserito `usblp` in blacklist, dovrebbe venir restituito un output simile a:

```
usb 3-2: new full speed USB device using uhci_hcd and address 3
usb 3-2: configuration #1 chosen from 1 choice

```

#### Auto-loading

Per caricare automaticamente al boot i moduli necessari creare il file `/etc/modules-load.d/printing.conf` che contenga:

```
lp
parport
parport_pc

```

#### Stampanti con porta parallela

Per l'utilizzo delle stampanti con parallela porta, si noti che la configurazione è praticamente la stessa, fatta eccezione per i moduli:

```
# modprobe lp
# modprobe parport
# modprobe parport_pc

```

Ancora una volta, controllare l'installazione eseguendo:

```
# tail /var/log/messages.log

```

Si dovrebbe vedere qualcosa del genere:

```
lp0: using parport0 (polling).

```

Se si utilizza un adattatore USB per porta parallela, CUPS non sarà in grado di rilevare la stampante. Per risolvere il problema, aggiungere la stampante tramite un altro tipo di connessione e quindi modificare il DeviceID in `/etc/cups/printers.conf`:

```
DeviceID = parallel:/dev/usb/lp0

```

### Stampanti HP

Le stampanti HP possono essere settate su Linux tramtite un proprio tool. (Sono necessari `python-qt2` `pygobject`).

Se si vuole usare il front-end in QT lanciare in un terminale:

```
# hp-setup -u

```

Se si vuole usare il front-end CLI lanciare in un terminale:

```
# hp-setup -i

```

## Configurazione

Ora che CUPS è installato, ci sono una varietà di opzioni su come configurare le soluzioni di stampa. Come sempre, il collaudato metodo da riga di comando è a disposizione. Allo stesso modo, diversi ambienti desktop come GNOME e KDE dispongono di utilità che possono aiutare a gestire le stampanti. Tuttavia, al fine di rendere questo processo più facile per un più vasto numero di utenti, questo articolo si focalizzerà sul metodo dell'interfaccia web di CUPS.

Se si pianifica un collegamento ad una stampante di rete, piuttosto che un collegamento diretto al computer, si potrebbe leggere per prima la pagina [CUPS printer sharing](/index.php/CUPS_printer_sharing "CUPS printer sharing"). La condivisione della stampante tra sistemi GNU/Linux è abbastanza semplice e prevede poche configurazioni, mentre la condivisione tra sistemi Windows e GNU/Linux richiede qualche sforzo in più.

### Avviare CUPS al boot

**Note:** Dalla versione di [cups](https://www.archlinux.org/packages/?name=cups) 2.0.0, il servizio è stato rinominato in `org.cups.cupsd.socket`.

Dopo aver installato cups, basterà abilitare e lanciare il servizio come qualsiasi demone gestito da systemd.

Se passate da una versione precedente, ricordatevi di disabilitare il servizio cups, per non lasciare link morti nell'alberatura di systemd.

L'integrazione con Avahi per il discover delle stampanti in lan è ora gestito come servizio separato, e può essere avviato ed abilitato utilizzando il nome del servizio: `cups-browsed.service`.

### Interfaccia web e strumenti

Una volta avviato il demone, aprire un brower ed inserire nella barra dell'indirizzo: [http://localhost:631](http://localhost:631) (*Al posto di **localhost** può essere necessario inserire il nome host presente in* `/etc/hostname`.

A questo punto. seguire le varie procedure guidate per aggiungere la stampante. Una procedura consueta è quella di iniziare facendo click sul pulsante *Aggiungere stampanti e classi* e poi su *Aggiungi Stampante*. Quando vengono richieste le credenziali inserire quelle di root. Il nome assegnato alla stampante non è rilevante, come i campi "ubicazione"' e "descrizione". Successivamente si presenterà un elenco di stampanti tra cui scegliere. L'attuale nome della stampante sarà presente vicino all'etichetta (ad esempio *USB Printer #1* per le stampanti USB). Infine selezionare il driver appropriato per completare la configurazione.

Ora, testare la configurazione premendo il menù a discesa *Amministrazione* e scegliere *Stampa pagina di prova*. Se non stampa e le configurazioni sono corrette, probabilmente il driver selezionato non è quello appropriato.

**Tip:** Vedere [#Interfacce alternative per CUPS](#Interfacce_alternative_per_CUPS) per altri tipi di interfaccia.

**Note:** Quando si configura una stampante USB, essa dovrebbe essere elncata nella pagina *Aggiungi Stampante*. Se è invece elencata solo una "Stampante SCSI", probabilmente CUPS ha fallito nel riconoscere la stampante.

#### Amministrazione di CUPS

Per poter amministrare le stampanti tramite l'interfaccia web è necessario fornire un nome utente e la password, ad esempio: per aggiungere o rimuovere stampanti, per interrompere i processi di stampa eccetera. L'utente di default è quello appartenente al gruppo *sys* oppure root (per cambiare il gruppo modificare `/etc/cups/cupsd.conf` alla riga *SystemGroup*).

Se l'utente root è stato bloccato (per esempio se si usa solo `sudo`), non sarà possibile accedere all'interfaccia di amministrazione con il proprio utente e password. In questo caso seguire quanto descritto [nelle faq](http://www.cups.org/articles.php?L237+T+Qprintadmin) di CUPS e leggere [questo post sul forum internazionale](https://bbs.archlinux.org/viewtopic.php?id=35567).

#### Accesso remoto all'interfaccia web

Di default, l'interfaccia web di configurazione di CUPS è accessibile solo da *localhost*; cioè dal computer su cui è installato. Per consentire l'accesso da remoto, sarà necessario effettuare le seguenti modifiche al file `/etc/cups/cupsd.conf`. Sostituire la seguente riga:

```
Listen localhost:631

```

con

```
port 631

```

così che CUPS stia in ascolto anche per le richieste esterne.

Ci sono tre livelli di accesso che possono essere garantiti:

```
<Location />           #accesso al server
<Location /admin>	#accesso alla pagina di amministrazione
<Location /admin/conf>	#accesso alla pagina di configurazione

```

Per concedere ad un host remoto di accedere ad uno di questi tre livelli si dovrà aggiungere una regola di `Allow` (concessione dell'accesso) per il relativo livello. Una regola di `Allow` può essere formulata in diversi modi, ad esempio:

```
Allow all
Allow host.domain.com
Allow *.domain.com
Allow ip-address
Allow ip-address/netmask

```

Possono essere usate le regole di accesso negato (`Deny`), se si intende dare agli host della rete 192.168.1.0/255.255.255.0 il pieno accesso, il file `/etc/cups/cupsd.conf` includerà le seguenti linee:

```
# Limita l'accesso al server....
# Il default permette solo a locahost di accedre
<Location />
   Order allow,deny
   Allow From localhost
   **Allow From 192.168.1.0/255.255.255.0**
</Location>

# Limita l'accesso alla pagina di amministrazione...
<Location /admin>
   # La cifratura è disbilitata di default
   #Encryption Required
   Order allow,deny
   Allow From localhost
   **Allow From 192.168.1.0/255.255.255.0**
</Location>

# Limita l'accesso alla pagina di configurazione...
<Location /admin/conf>
   AuthType Basic
   Require user @SYSTEM
   Order allow,deny
   Allow From localhost
   **Allow From 192.168.1.0/255.255.255.0**
</Location>

```

Potrebbe anche essere necessario aggiungere:

```
DefaultEncryption Never

```

Questo dovrebbe evitare l'errore: 426 - L'aggiornamento è obbligatorio quando si utilizza l'interfaccia web di CUPS da una macchina remota.

### Configurazione CLI

CUPS può essere interamente controllato via riga di comando.

Su Arch Linux, le più comuni shell permettono l'autocompletamento. Notare però che gli switches non possono essere raggruppati.

	Lista dei devices

```
# lpinfo -v

```

	Lista dei driver

```
# lpinfo -m

```

	Aggiungere una nuova stampante

```
# lpadmin -p <printer> -E -v <device> -P <ppd>

```

<printer> è il nome e lo sceglie l'utente. <device> lo si trova con il comando 'lpinfo -i'. Esempio:

```
# lpadmin -p HP_DESKJET_940C -E -v "usb://HP/DESKJET%20940C?serial=CN16E6C364BH"  -P /usr/share/ppd/HP/hp-deskjet_940c.ppd.gz

```

Nell'esempio seguente, <printer> è il nome scelto in precedenza.

	Imposta <printer> come predefinita

```
$ lpoptions -d <printer>

```

	Controlla lo status della stampante

```
$ lpstat -s
$ lpstat -p <printer>

```

	Disatttiva una stampante

```
# cupsdisable <printer>

```

	Attiva una stampante

```
# cupsenable <printer>

```

	Rimuove una stampante

Rigetta ogni nuova richiesta di lavoro:

```
# cupsreject <printer>

```

Disabilita la stampante:

```
# cupsdisable <printer>

```

Rimuove la stampante:

```
# lpadmin -x <printer>

```

	Stampa un file

```
$ lpr <file>
$ lpr -# 17 <file>              # stampa il file 17 volte
$ echo "Hello, world!" | lpr -p # stampa l'output del comando. Lo switch -p aggiunge l'header.

```

	Controlla la coda di stampa

```
$ lpq
$ lpq -a # on all printers

```

	Cancella la coda di stampa

```
# lprm   # remove last entry only
# lprm - # remove all entries

```

### Interfaccia CUPS di GNOME

Se si utilizza [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)"), una possibilità è di gestire e configurare le stampanti [installando](/index.php/Pacman_(Italiano) "Pacman (Italiano)") il pacchetto [system-config-printer](https://www.archlinux.org/packages/?name=system-config-printer).

Per rendere system-config-printer realmente funzionante, può rendersi necessario eseguirlo come root (sfruttando sudo o gksu), o in alternativa impostare i permessi per lasciar controllare CUPS ad un normale utente. Se si vuol affontare questa seconda scelta, **seguire i passaggi 1-3**:

*   1\. Creare il gruppo, quindi aggiungere l'utente desiderato:

```
# groupadd lpadmin
# usermod -aG lpadmin <username>

```

*   2\. Aggiungere "lpadmin" (senza le virgolette) a questa linea nel file `/etc/cups/cupsd.conf`

```
SystemGroup sys root <inserire qui>

```

*   3\. Riavviare CUPS, effettuare il logout, quindi nuovamente il login (o, in alternativa, riavviare il computer)

 `# systemctl restart cupsd` 

Gli utenti [KDE](/index.php/KDE_(Italiano) "KDE (Italiano)") possono gestire le stampanti nel Centro di Controllo. Entrambi gli utenti (GNOME o KDE), dovrebbero riferirsi alla documentazione dei rispettivi *Desktop Environment* per maggiori informazioni su come gestire l'interfaccia.

Un'altra interfaccia utile è [gtklp](https://aur.archlinux.org/packages/gtklp/) disponibile su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").

## Stampante virtuale PDF

[cups-pdf](https://www.archlinux.org/packages/?name=cups-pdf) è un pacchetto interessante, che permette all'utente di impostare una stampante virtuale, la quale genera PDF da qualsiasi dato le venga inviato. Ovviamente questo pacchetto non è strettamente necessario, ma può rivelarsi discretamente utile.

Dopo l'installazione settare la stampante dalla web interface di cups: [http://localhost:631/](http://localhost:631/) e selezionare:

```
Administration -> Add Printer
Select CUPS-PDF (Virtual PDF), choose for the make and  driver:
Make:	Generic
Driver:	Generic CUPS-PDF Printer

```

I documenti PDF generati si vanno ad allocare in una sottocartella di `/var/spool/cups-pdf`. Generalmente, la sottocartella porta il nome dell'utente che ha richiesto la creazione dei documenti contenuti. Un piccolo trucco per trovare i documenti stampati in formato PDF con più facilità: Modificare /etc/cups/cups-pdf.conf cambiando la riga

```
#Out /var/spool/cups-pdf/${USER}

```

a

```
Out /home/${USER}

```

### Stampare su Postscript

Generare documenti PDF in applicazioni come OpenOffice è un'operazione molto semplice; spesso basta premere un pulsante. Diversamente, generare file Postscript da un documento può richiedere qualche attenzione in più. Per applicazioni come OpenOffice, nelle quali stampare con kprinter è un vero problema, esiste una valida via di fuga. CUPS-PDF (stampante virtuale di PDF) crea, nel suo processo di elaborazione, un file Postscript che viene poi convertito nel PDF richiesto alla stampa. Per generare un file Postscript attraverso CUPS-PDF, ciò di cui si ha bisogno è di catturare il file Postscript intermedio creato da CUPS-PDF. Questo risultato può essere facilmente raggiunto selezionando l'opzione "Stampa su file" nella finestra di stampa. Dopo aver selezionato "Stampa su file", scegliere il nome del file, la sua estensione, quindi cliccare su "Stampa". Questa procedura è utile per fax, stampe da ufficio, ecc...

## Risoluzione dei Problemi

Il modo migliore per far funzionare la stampante consiste nell'impostare "LogLevel" in `/etc/cups/cupsd.conf` così:

```
LogLevel debug

```

E quindi controllare i dati dal file `/var/log/cups/error_log` in questo modo:

```
# tail -n 100 -f /var/log/cups/error_log

```

I caratteri alla sinistra del risultato stanno per:

*   D=Debug
*   E=Errore
*   I=Informazioni
*   E così via

Questi file potrebbero anche dimostrarsi utili:

*   `/var/log/cups/page_log` - Riproduce un nuovo appunto ogni volta che la stampa avviene correttamente
*   `/var/log/cups/access_log` - Elenca tutta l'attività del server cupsd http1.1

Naturalmente, è importante conoscere come funziona CUPS per far fronte ad eventuali problemi:

1.  Un'applicazione manda un file .ps (PostScript, un linguaggio script che indica come deve apparire la pagina) a CUPS quando l'opzione "stampa" viene selezionata (ciò avviene con la maggior parte dei programmi).
2.  CUPS quindi analizza il file PPD della stampante (file di descrizione della stampante) e trova i filtri necessari per convertire il file .ps nel linguaggio comprensibile alla stampante (come PJL, PCL), solitamente GhostScript.
3.  GhostScript riceve l'input e capisce quali filtri debba usare, quindi li applica e converte il file .ps nel formato compreso dalla stampante.
4.  Quindi manda un back-end. Ad esempio, se la stampante è connessa tramite porta USB, utilizza il back-end USB.

Si stampi un documento e si analizzi `error_log` per avere un'immagine più dettagliate e corretta del processo di stampa.

### Problemi legati all'aggiornamento

*Problemi che appaiono dopo che i pacchetti CUPS e i relativi programmi vengono aggiornati ad una versione più recente*

#### CUPS smette di funzionare

Potrebbe succedere che a seguito di un aggiornamento ci siano dei cambiamenti nei file di congifurazione. Messaggi come "404 - page not found" potrebbero apparire provando ad amministrare CUPS via localhost:631, ad esempio.

Per usare la nuova configurazione, copiare `/etc/cups/cupsd.conf.default` in `/etc/cups/cupsd.conf` (salvare la vecchia configurazione se necessario) e riavviare CUPS per abilitare le nuove configurazioni.

#### Tutti i lavori sono "fermati"

Se tutti i lavori inviati alla stampante risultano "stopped", si elimini la stampante e quindi la si riaggiunga. Si usi [l'interfaccia web di CUPS](http://localhost:631), si vada in Stampante > Elimina Stampante.

Per controllare la configurazione della stampante di vada in *Stampanti*, quindi *Modificare Stampante*. Trascrivere le informazioni mostrate, selezionare 'Modificare Stampante' per procedere alle pagine successive, e così via.

#### Tutti i lavori convergono in un "The printer is not responding"

Sulle stampanti di rete si dovrebbe verificare che il nome che CUPS utilizza come URI di connessione si risolva in IP della stampante tramite DNS. Ad esempio, se la connessione della stampante si presenta così:

```
lpd://BRN_020554/BINARY_P1

```

l'hostname "BRN_020554" deve risolvere l'IP della stampante dal server che esegue CUPS

#### La versione PPD non è compatibile con gutenprint

Lanciare:

```
# /usr/sbin/cups-genppdupdate

```

e riavviare CUPS (come evidenziato dal messaggio post-installazione di guternprint)

### Altro

##### Errori di permessi CUPS

*   Alcuni utenti risolvono errori del tipo 'NT_STATUS_ACCESS_DENIED' (client Windows) usando una sintassi leggermente diversa:

```
smb://workgroup/username:password@hostname/printer_name

```

*   Qualche volta, l'intero dispositivo ha permessi sbagliati:

```
# ls /dev/usb/
lp0
# chgrp lp /dev/usb/lp0

```

#### La stampante HPLIP invia come errore "/usr/lib/cups/backend/hp failed"

Assicurarsi d'aver installato dbus e di averlo avviato. Se ci fossero ancora problemi, avviare il service di avahi-daemons.

Provare ad aggiungere la stampante come Stampante di Rete (Network Printer) usando il protocollo http://. Generare l'URI della stampante con `hp-makeuri`.

**Nota:** C'è la possibilità che si renda necessario cambiare i permessi di CUPS. Si segua quanto scritto [qui](#Permessi_del_device_node).

#### HPLIP tutti i lavori vengono segnati come ultimati ma non si è riusciti a stampare niente

Questo succede su stampanti HP quando viene selezionato il vecchio driver `hpijs` (ad esempio per le stampati della serie Deskjet D1600). Quindi, quando si aggiunge una stampante, selezionare il driver `hpcups`.

Alcune stampanti, come le HP Laserjet, richiedono che il proprio firmware venga scaricato ad ogni accensione. Esiste un workaround, lanciare il comando:

```
# hp-firmware -n

```

#### hp-toolbox invia come errore, "Unable to communicate with device"

Se lanciando hp-toolbox come utente normale si ottiene:

```
# hp-toolbox
# error: Unable to communicate with device (code=12): hp:/usb/<printer id>

```

o, "`Unable to communicate with device"`", allora potrebbe essere necessario [aggiungere l'utente al gruppo lp](/index.php/Utenti_e_Gruppi#Gestione_dei_gruppi "Utenti e Gruppi").

Questo può tornare utile anche per stampanti come la P1102 che fornisce un virtual cd-rom con i driver per MS-Windows. Il device compare e scompare. In questo caso provare i pacchetti da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") [usb-modeswitch](https://aur.archlinux.org/packages/usb-modeswitch/) and [usb-modeswitch-data](https://aur.archlinux.org/packages/usb-modeswitch-data/), che permettono uno "switch off" di "Smart Drive" (la regola di udev inclusa in questi pacchetti).

Questo potrebbe succedere anche se il demone [avahi-daemon](/index.php/Avahi "Avahi") non è avviato.

#### CUPS risponde '"foomatic-rip" not available/stopped with status 3' con una stampante HP

Se si riceve qualsiasi dei seguenti messaggi d'errore in `/var/log/cups/error_log` durante l'utilizzo di una stampante HP, con i lavori che sembrano essere avviati mentre invece non vengo terminati e il loro stato è impostato a 'stopped':

```
Filter "foomatic-rip" for printer "<printer_name>" not available: No such file or director

```

o:

```
PID 5771 (/usr/lib/cups/filter/foomatic-rip) stopped with status 3!

```

assicurarsi che **[hplip](https://www.archlinux.org/packages/?name=hplip)** sia stato installato, in aggiunta al [pacchetto menzionato sopra](#Installazione), **net-snmp** è anche necessario. Si veda [questo post nel forum internazionale](https://bbs.archlinux.org/viewtopic.php?id=65615).

#### La stampa fallisce segnalando errori di autorizzazione

Se l'utente è stato aggiunto al gruppo lp, e gli è permesso stampare (impostato in `cupsd.conf`), allora il probema si trova nel file `/etc/cups/printers.conf`. Questa potrebbe essere la linea colpevole:

```
AuthInfoRequired negotiate

```

La si commenti e si riavvii CUPS.

#### Pulsante Stampa bloccato nelle applicazioni GNOME

	*<small>Fonte (in inglese): [Non posso stampare nelle applicazioni GNOME. - Arch Forums](https://bbs.archlinux.org/viewtopic.php?id=70418)</small>*

Assicurarsi che il pacchetto [libgnomeprint](https://aur.archlinux.org/packages/libgnomeprint/) sia installato.

Modificare il file `/etc/cups/cupsd.conf`, aggiungendo

```
# HostNameLookups Double

```

Riavviare quindi CUPS:

```
# systemctl restart cupsd

```

#### Formato supportato sconosciuto: application/postscript

Commentare le linee:

```
application/octet-stream        application/vnd.cups-raw        0      -

```

nel file `/etc/cups/mime.convs`, e:

```
application/octet-stream

```

in `/etc/cups/mime.types`.

#### Trovare gli URI per i server di stampa Windows

Spesso Windows è poco intuitivo nella definizione esatta degli URI (la posizione dei dispositivi).Se si riscontrano problemi nello specificare la corretta posizione di un dispositivo in CUPS, eseguire il seguente comando per mostrare una lista di tutte le condivisioni disponibili per un dato utente di Windows:

```
$ smbtree -U *utentewindows*

```

Questo comando mostrerà ogni risorsa condivisa disponibile per il dato utente di Windows sulla rete LAN, dato come prerequisito che Samba sia installato e correttamente funzionante. L'output dovrebbe essere simile al qui proposto:

```
 WORKGROUP
	\\REGULATOR-PC   		
		\\REGULATOR-PC\Z              	
		\\REGULATOR-PC\Public         	
		\\REGULATOR-PC\print$         	Printer Drivers
		\\REGULATOR-PC\G              	
		\\REGULATOR-PC\EPSON Stylus CX8400 Series	EPSON Stylus CX8400 Series
```

Ciò di cui si ha bisogno nell'esempio è la prima parte dell'ultima riga, la risorsa che coincide con la descrizione della stampante. In questo caso, per mandare in stampa la EPSON Stylus, bisogna inserire come URI:

```
smb://username.password@REGULATOR-PC/EPSON Stylus CX8400 Series

```

in CUPS. Si noti che negli URI gli spazi bianchi sono permessi, mentre gli back-slash (\) vanno sostituiti con gli slash classici (/). Nel caso in cui ci siano dei problemi provare a sostituire gli spazi con `%20`.

#### Errore di stampa client-error-document-format-not-supported

Provare a installare i pacchetti foomatic e utilizzare un driver foomatic.

#### Errore /usr/lib/cups/backend/hp

Modificare

```
 SystemGroup sys root

```

con

```
 SystemGroup lp root

```

in /etc/cups/cupsd.conf

#### "Unable to get list of printer drivers"

Provare a riumuovere i driver Footmatic.

#### lp: Error - Scheduler Not Responding

Se si riceve questo errore durante la stampa di un documento, provare con questo comando:

```
$ lp document-to-print

```

Provare a settare la variabile d'ambiente CUPS_SERVER:

```
$ export CUPS_SERVER=localhost

```

Se quest'ultimo passaggio funziona, è possibile rendere permanente tale modifica aggiungendo la linea `export CUPS_SERVER=localhost` nel file `~/.bash_profile` o nel relativo file della propria shell, come ad esempio `~/.zprofile` e si usa [Zsh](/index.php/Zsh "Zsh").

#### CUPS stampa una pagina vuota e una di errore con HP Laserjet

Questo è un bug conosciuto di cups. La prima pagina risulta essere bianca, la seconda riporta:

```
ERROR:
invalidaccess
OFFENDING COMMAND:
filter
STACK:
/SubFileDecode
endstream
...

```

Per risolvere dare questo comando da root:

```
#  lpadmin -p <printer> -o pdftops-renderer-default=pdftops

```

#### Errore: "Using invalid Host"

Aggiungere `ServerAlias*` in `cupsd.conf`.

#### La stampante non lavora e restituisce come errore "Filter Failed" sull'interfaccia web di CUPS

Cambiare permessi sulla porta USB: Cercare bus e device number con lsusb e dare un:

```
# chmod 0666 /dev/bus/usb/<bus number>/<device number>

```

#### La stampante non viene riconosciuta da cups

Se la propria stampante non viene riconosciuta da CUPS (ovvero non è presente nella lista che si ha cliccando sul pulsante "Add Printers" dell'interfaccia web di CUPS), provare questo metodo (suggerito [sul forum internazionale](https://bbs.archlinux.org/viewtopic.php?pid=1037279#p1037279)):

1.  Fermare cups
2.  Creare questa regola di udev: `/etc/udev/rules.d/10-cups_device_link.rules`

che contenga:

```
KERNEL=="lp[0-9]", SYMLINK+="%k", GROUP="lp"}}

```

1.  Scollegare e ricollegare la stampante.
2.  Riavviare cups.

## Vedere anche

*   [Documentazione Ufficiale di CUPS](http://localhost:631/documentation.html), *Installata Localmente*
*   [Sito ufficiale di CUPS](http://www.cups.org/)
*   [Linux Printing](http://www.linuxprinting.org/), *[The Linux Foundation](http://www.linuxfoundation.org)*
*   [Guida alla stampa di Gentoo](http://www.gentoo.org/doc/en/printing-howto.xml), *[Documentazione di Gentoo](http://www.gentoo.org/doc/en)*
*   [Forum internazionale di Arch Linux](https://bbs.archlinux.org/)