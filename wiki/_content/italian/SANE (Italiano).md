Sane fornisce una libreria e uno strumento da riga di comando per utilizzare gli scanner sotto GNU/Linux. [Qua](http://www.sane-project.org/sane-supported-devices.html) è possibili verificare se il vostro scanner è supportato.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Per dispositivi Acer/BenQ](#Per_dispositivi_Acer.2FBenQ)
    *   [2.2 Per dispositivi HP](#Per_dispositivi_HP)
    *   [2.3 Per dispositivi Brother](#Per_dispositivi_Brother)
    *   [2.4 Per dispostivi Epson](#Per_dispostivi_Epson)
    *   [2.5 Per dispositivi Samsung](#Per_dispositivi_Samsung)
    *   [2.6 Per scanner plustek](#Per_scanner_plustek)
    *   [2.7 Per scanner microtek](#Per_scanner_microtek)
*   [3 Firmware](#Firmware)
*   [4 Installare un frontend](#Installare_un_frontend)
*   [5 Scansione di rete](#Scansione_di_rete)
    *   [5.1 Condivisione dello scanner su una rete](#Condivisione_dello_scanner_su_una_rete)
    *   [5.2 Configurare xinetd per sane](#Configurare_xinetd_per_sane)
    *   [5.3 Accesso allo scanner da una workstation remota](#Accesso_allo_scanner_da_una_workstation_remota)
    *   [5.4 Scansione in rete con Canon Pixma all-in-one printer/scanners](#Scansione_in_rete_con_Canon_Pixma_all-in-one_printer.2Fscanners)
*   [6 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [6.1 Invalid argument](#Invalid_argument)
        *   [6.1.1 Firmware mancante](#Firmware_mancante)
        *   [6.1.2 Permessi errati sul firmware](#Permessi_errati_sul_firmware)
        *   [6.1.3 Uso multiplo di diversi backends](#Uso_multiplo_di_diversi_backends)
    *   [6.2 Avvio lento](#Avvio_lento)
    *   [6.3 Problemi di permessi](#Problemi_di_permessi)
    *   [6.4 Epson Perfection 1270](#Epson_Perfection_1270)
    *   [6.5 Blocco durante la scansione a causa di XHCI in modalità di pre-boot](#Blocco_durante_la_scansione_a_causa_di_XHCI_in_modalit.C3.A0_di_pre-boot)

## Installazione

[Installare](/index.php/Pacman "Pacman") [sane](https://www.archlinux.org/packages/?name=sane) dagli [official repositories](/index.php/Official_repositories "Official repositories").

## Configurazione

Prima di tutto si può provare a vedere se SANE riconosce lo scanner

```
$ scanimage -L

```

Se non funziona, controllare che lo scanner sia collegato al computer. Potrebbe anche essere necessario scollegare/collegare lo scanner per farlo riconoscere da `/etc/udev/rules.d/sane.rules`

Dopodiché è possibile verificare se funziona effettivamente

```
$ scanimage --format=tiff > test.tiff

```

Se la scansione non riesce e appare il messaggio `scanimage: sane_start: Invalid argument` potrebbe essere necessario specificare il dispositivo.

 `$ scanimage -L` 

```
device `v4l:/dev/video0' is a Noname Video WebCam virtual device
device `pixma:04A91749_247936' is a CANON Canon PIXMA MG5200 multi-function peripheral
```

Allora si dovrebbe eseguire:

```
$ scanimage --device pixma:04A91749_247936 --format=tiff > test.tiff

```

### Per dispositivi Acer/BenQ

Se si possiede uno scanner USB Acer (ora BenQ), è necessario scaricare un apposito binario del firmware e configurare `/etc/sane.d/snapscan.conf`

*   Scoprire quale modello si possiede e prendere nota dell'ID USB:

 `$ lsusb`  `Bus 002 Device 010: ID 04a5:20b0 Acer Peripherals Inc. (now BenQ Corp.) S2W 3300U/4300U` 

*   Andare sul sito [snapscan](http://snapscan.sourceforge.net/) e vedere se lo scanner è supportato e di che firmware si ha bisogno (ad esempio , `u176v046.bin`).
*   Cercare l'immagine del firmware su internet e scaricarlo nella cartella `/usr/share/sane/snapscan/`.
*   Modificare l'inizio di `/etc/sane.d/snapscan.conf` e configurare le seguenti due righe:

```
firmware /usr/share/sane/snapscan/u176v046.bin
/dev/usb/scanner0 bus=usb

```

### Per dispositivi HP

Per l'hardware HP potrebbe anche essere necessario installare [hplip](https://www.archlinux.org/packages/?name=hplip) fagli [official repositories](/index.php/Official_repositories "Official repositories") (vedere [hplib supported devices](http://hplipopensource.com/hplip-web/supported_devices/index.html)) e/o [hpoj](https://aur.archlinux.org/packages/hpoj/) da [AUR](/index.php/Arch_User_Repository "Arch User Repository") (vedere [hpoj supported devices](http://hpoj.sourceforge.net/suplist.shtml)).

*   Rimuovere il commento o aggiungere `hpaio` e `hpoj` in una nuova riga su `/etc/sane.d/dll.conf`.
*   Eseguire `hp-setup` da root può aiutarvi ad aggiungere il dispositivo.
*   `hp-plugin` è l_HPLIP Plugin Download and Install Utility'._
*   `hp-scan` è l_HPLIP Scan Utility'._

Per Hewlett-Packard OfficeJet, PSC, LaserJet, e stampanti multifuzione PhotoSmart, esguire `ptal-init setup` da root è seguire le istruzioni. Quindi avviare il demone **ptal-init** [daemon](/index.php/Daemon "Daemon").

### Per dispositivi Brother

Per installare uno scanner Brother è necessario il driver giusto (si può trovare su AUR). Ci sono solo quattro drivers tra cui scegliere (brscan1-4). Al fine di trovare quello giusto si dovrebbe cercare il proprio modello su [brother linux scanner page](http://welcome.solutions.brother.com/bsc/public_s/id/linux/en/download_scn.html).

Dopo aver installato il driver è necessario eseguire (es. setupSaneScan2 per dispositivi brscan2 compatibili):

```
# /usr/local/Brother/sane/setupSaneScan2 -i

```

in modo che il driver/scanner siano riconosciuti da SANE.

Per scanner di rete, Brother fornisce uno strumento di configurazione diverso per ogni versione di brscan (es. brsaneconfig2 per brscan2 e compatibili):

```
# brsaneconfig2 -a name=<ScannerName> model=<ScannerModel> ip=<ScannerIP>

```

Esempio:

```
# brsaneconfig2 -a name=SCANNER_DCP770CW model=DCP-770CW ip=192.168.0.110

```

### Per dispostivi Epson

Per scanner di rete (inclusa Wi-Fi), è possibile usare "Image Scan! for Linux".

Installare [iscan](https://www.archlinux.org/packages/?name=iscan), [iscan-data](https://www.archlinux.org/packages/?name=iscan-data) e [iscan-plugin-network](https://aur.archlinux.org/packages/iscan-plugin-network/) da [AUR](/index.php/AUR "AUR"), ed editare `/etc/sane.d/epkowa.conf` aggiungendo la linea:

```
net {IP_OF_SCANNER}

```

### Per dispositivi Samsung

Per alcune stampanti Samsung MFP potrebbe essere necessario modificare `/etc/sane.d/xerox_mfp.conf`.

Esempio:

```
#Samsung SCX-3200
usb 0x04e8 0x3441

```

Cambiare il modello della stampante, se necessario. È possibile ottenere il codice idVendor e idProduct con `lsusb`. Vedere [questo topic](https://bbs.archlinux.org/viewtopic.php?id=123934).

Quando si collega una stampante/scanner USB2 ad una interfaccia USB3 vi è attualmente un bug nel codice del kernel xHCI che causa il blocco del processo xsane quando è collegato lo scanner. Nel caso di una stampante Samsung multifunzione avente un ethernet o interfaccia wireless allora è possibile accedere allo scanner sulla rete, invece che tramite interfaccia USB, aggiungendo una riga al file /etc/sane.d/xerox_mfp.conf come questa:

```
#Samsung scx4500w wireless ip network address
tcp xx.xx.xx.xx

```

Dove xx.xx.xx.xx l'indirizzo ip statico della stampante.

Poi, quando si avvia xsane è possibile scegliere l' opzione di accesso tcp rete al posto della linea usb, e lo scanner sarà accessibile tramite la rete anziché la porta usb per evitare gli attuali problemi con USB3.

### Per scanner plustek

Alcuni scanner Plustek (come i CanoScan) , richiedono una directory di blocco. Assicurarsi che in /var/lock esista la cartella /sane , che i permessi siano 660, e che sia di proprietà dell'utente" scanner. Se le autorizzazioni per la directory sono sbagliate, solo l'utente root sarà in grado di utilizzare lo scanner. Sembra (almeno su x86-64) che alcuni programmi che usano libusb (tipo xsane e kooka) hanno bisogno di permessi di rw al gruppo scanner anche per l'accesso a /proc/bus/usb per lavorare come utente normale.

### Per scanner microtek

Alcuni scanner MICROTEK richiedono il modulo `sg`, che dovrebbe essere caricato automaticamente. Se non viene caricato dal sistema, provare a caricarlo manualmente (vedere [Kernel modules#Configuration](/index.php/Kernel_modules#Configuration "Kernel modules") per dettagli).

Controllare se lo scanner viene riconosciuto , si dovrebbe ottenere il seguente output:

 `scanimage -L` 

```
device `microtek2:/dev/sg5' is a Microtek Phantom 636cx / C6 flatbed scanner

```

## Firmware

**Note:** Questa sezione è necessaria solo se avete bisogno di aggiornare il firmware dello scanner.

Solitamente i firmware hanno estensione **`.bin`**

In primo luogo è necessario mettere il firmware in un posto sicuro, si consiglia di metterlo in una sottodirectory di `/usr/share/sane`.

Allora sarà necessario dire a SANE dove si trova il firmware:

*   Trovare il nome del backend per il proprio scanner da [sane supported devices list](http://www.sane-project.org/sane-supported-devices.html).
*   Aprire il file `/etc/sane.d/<backend-name>.conf`.
*   Assicurarsi che la voce firmware non sia commentata(#) e inserire il percorso in cui si trova il firmware. Assicurarsi che i membri del gruppo `scanner` abbiano accesso al file `/etc/sane.d/<backend-name>.conf`.

Se il backend del vostro scanner non fa parte del pacchetto sane (come hpaio.conf che fa parte di hplip), è necessario togliere il commento alla voce corrispondente in /etc/sane.d/dll.d

## Installare un frontend

Esistono molti frontend per SANE, un elenco non esaustivo può essere trovato su [sane-project website](http://www.sane-project.org/sane-frontends.html). Un altro modo per trovarli è quello di utilizzare la funzione cerca di `pacman` con parole tipo "sane" or "scanner":

```
$ pacman -Ss sane

```

*   **[gscan2pdf](https://en.wikipedia.org/wiki/Scanner_Access_Now_Easy#gscan2pdf "wikipedia:Scanner Access Now Easy")** — Una GUI basata su GTK2 per produrre file PDF, TIFF o DjVus da documenti acquisiti. È inoltre in grado di applicare OCR nel processo utilizzando diversi motori . Dipende da alcuni pacchetti Perl per funzionare, alcuni dei quali si trovano su [AUR](/index.php/AUR "AUR").

	[http://gscan2pdf.sourceforge.net/](http://gscan2pdf.sourceforge.net/) || [gscan2pdf](https://aur.archlinux.org/packages/gscan2pdf/)

*   **[Simple Scan](https://en.wikipedia.org/wiki/Scanner_Access_Now_Easy#Simple_Scan "wikipedia:Scanner Access Now Easy")** — Una GUI semplificata che è destinata ad essere più facile da usare e meglio integrata di Xsane nel desktop GNOME. Inizialmente è stata scritta per Ubuntu ed è mantenuta da Robert Ancell di Canonical Ltd. per GNU/Linux.

	[http://launchpad.net/simple-scan](http://launchpad.net/simple-scan) || [simple-scan](https://www.archlinux.org/packages/?name=simple-scan)

*   **[Skanlite](https://en.wikipedia.org/wiki/Skanlite "wikipedia:Skanlite")** — Skanlite è un semplice programma per scansionare e salvare immagini, basato su KSane.

	[http://www.kde.org/applications/graphics/skanlite](http://www.kde.org/applications/graphics/skanlite) || [skanlite](https://www.archlinux.org/packages/?name=skanlite)

*   **[XSane](https://en.wikipedia.org/wiki/Scanner_Access_Now_Easy#XSane "wikipedia:Scanner Access Now Easy")** — Un frontend GTK-based full-optional, un po' vecchio ma con ampie funzionalità.

	[http://www.xsane.org/](http://www.xsane.org/) || [xsane](https://www.archlinux.org/packages/?name=xsane)

**Note:** Scansionare direttamente in PDF utilizzando XSane in modalità colore 16 bit produrrà un [file corrotto](https://bugs.launchpad.net/ubuntu/+source/xsane/+bug/539162), una nota su `pacman` avverte di questo bug. La modalità 8bit invece sembra funzionare.

## Scansione di rete

#### Condivisione dello scanner su una rete

E' possibile condividere il proprio scanner con altri host della rete che utilizzano sane, xsane o xsane-Gimp. Per impostare il server, bisogna prima indicare a quali hosts dare i permessi di accesso.

Modificare il file `/etc/sane.d/saned.conf` a proprio piacimento, per esempio:

```
# required
localhost
# allow local subnet
192.168.0.0/24

```

Inserire il modulo `nf_conntrack_sane` per iptables per consentire al firewall di traccaire la connessione di saned.

Le richieste di scansione vengono gestite da saned. Questo può essere eseguito come un demone con `saned -a` o eseguito quando necessario da xinetd:

#### Configurare xinetd per sane

[Installare](/index.php/Pacman "Pacman") [xinetd](https://www.archlinux.org/packages/?name=xinetd) dagli [official repositories](/index.php/Official_repositories "Official repositories").

Quindi, assicurarsi che il file `/etc/xinetd.d/sane` esista e che la riga disable sia settata su NO:

```
service sane-port
{
   port        = 6566
   socket_type = stream
   wait        = no
   user        = nobody
   group       = scanner
   server      = /usr/bin/saned
   disable     = no
}

```

L'utente normale ('nobody' nel file incluso nel pacchetto si sane) deve solitamente essere un membro del gruppo scanner per avere il permesso di accedere allo scanner :

```
# usermod -a -G scanner nobody

```

Per alcuni scanner - tipo le stampanti HP multifunzione - l'utente deve essere anche un membro del gruppo lp, che dovrebbe anche essere usato al posto dello scanner nel file di servizio .

Aggiungere la seguente linea a `/etc/services` se non è già presente:

```
sane-port 6566/tcp

```

Avviare il [demone](/index.php/Daemon_(Italiano) "Daemon (Italiano)") **xinetd**.

Lo scanner può ora essere utilizzato da altre stazioni di lavoro, attraverso la vostra rete locale .

#### Accesso allo scanner da una workstation remota

E' possibile accedere al proprio scanner di rete da una workstation Arch Linux remota.

Per configurare la postazione di lavoro, [installare](/index.php?title=Pacman_(Italiano))&action=edit&redlink=1 "Pacman (Italiano)) (page does not exist)") [xsane](https://www.archlinux.org/packages/?name=xsane) dagli [official repositories](/index.php/Official_repositories "Official repositories").

Quindi, specificare il nome host del server o l'indirizzo IP nel file `/etc/sane.d/net.conf` :

```
# static IP address
192.168.0.1
# or host name
stratus

```

Ora verificare la connessione dalla workstation tramite un terminale (non root):

```
$ xsane

```

oppure

```
$ scanimage -L

```

Dopo un po', xsane dovrebbe trovare il vostro scanner remoto e visualizzare le solite finestre, ora è tutto pronto per la scansione di rete!

Per le stampanti/scanner/fax HP All in one è necessario effettuare la configurazione tramite :

```
$ hp-setup <printer ip>

```

#### Scansione in rete con Canon Pixma all-in-one printer/scanners

Scoprire l'indirizzo IP dello scanner/stampante, e aggiungerlo su una nuova linea a /etc/sane.d/pixma.conf nel formato 'bjnp://10.0.0.20'.

Sane dovrebbe ora essere in grado di trovare il dispositivo. Per maggiori dettagli consultare 'man sane-pixma'.

## Risoluzione dei problemi

### Invalid argument

Se si ottiene un errore "Invalid argument" con xsane o una altro front-end, questo potrebbe eseere causanto da uno dei seguenti motivi:

#### Firmware mancante

Nessun file del firmware è stato fornito per lo scanner utilizzato (vedi sopra per i dettagli).

#### Permessi errati sul firmware

Le autorizzazioni per il file del firmware usati sono sbagliati . Correggerli utilizzando

```
# chown root:scanner /usr/share/sane/SCANNER_MODEL/FIRMWARE_FILE
# chmod ug+r /usr/share/sane/SCANNER_MODEL/FIRMWARE_FILE

```

#### Uso multiplo di diversi backends

Può accadere che il vostro scanner supporti i backend multipli, e SANE scelga uno che non funziona bene (lo scanner non verrà visualizzato in scanimage -L allora) . Questo accade con i vecchi scanner Epson e con i backend `epson2` e `epson`. In questo caso , la soluzione è quella di commentare il backend indesiderato in `/etc/sane.d/dll.conf`. Nel caso di Epson, bisognerebbe cambiare:

```
 epson2
 #epson

```

in

```
 #epson2
 epson

```

### Avvio lento

Se si verificano problemi di avvio lento (ad esempio se `xsane` e `scanimage -L` impiegano troppo tempo per rilevare lo scanner) può essere che uno o più driver supportati siano abilitati contemporaneamente.

Dare un'occhiata a `/etc/sane.d/dll.conf` e provare a commentarne uno (se per esempio si ha epson, epson2 e epkowa abilitati allo stesso tempo, provare a lasciare abilitati solo epson e epkowa)

### Problemi di permessi

Se vedete il vostro scanner solo quando si esegue `lsusb` da root, potrebbe essere necessario aggiungere il vostro utente al gruppo `scanner` e/o `lp`.

```
# gpasswd -a username scanner
# gpasswd -a username lp

```

Questo è segnalato come funzionante nei modelli HP all-in-one(es. PSC 1315 e PSC 2355).

Potete anche provare a cambiare i permessi dei dispositivo usb ma questo non è consigliato, la soluzione migliore è quella di fissare le regole di Udev in modo che lo scanner sia riconosciuto.

Esempio:

In primo luogo, come root, controllare i dispositivi USB collegati con `lsusb`:

```
#Bus 006 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
#Bus 005 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
#Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
#Bus 003 Device 003: ID 04d9:1603 Holtek Semiconductor, Inc. 
#Bus 003 Device 002: ID 04fc:0538 Sunplus Technology Co., Ltd 
#Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
#Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
#Bus 001 Device 006: ID 03f0:2504 Hewlett-Packard 
#Bus 001 Device 002: ID 046d:0802 Logitech, Inc. Webcam C200
#Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

In questo esempio abbiamo lo scanner - '**Bus 001 Device 006: ID 03f0:2504 Hewlett-Packard'**

Ora aprire il file `/lib/udev/rules.d/53-sane.rules` e cercare la prima parte del numero ID trovata in precedenza e verificare se c'è una riga che riporta anche la seconda parte del numero (numero del modello ). In questo esempio è 2504\. Se non c'è, aggiungere una riga e immettere il idVendor e idProduct dello scanner, in questo esempio potrebbe essere:

```
# Hewlett-Packard ScanJet 4100C
ATTRS{idVendor}=="03f0", ATTRS{idProduct}=="2504", MODE="0664", GROUP="scanner",
  ENV{libsane_matched}="yes"

```

Salvare il file, scollegare e ricollegare lo scanner e le autorizzazioni del file dovrebbero essere ora corrette.

Un altro suggerimento potrebbe essere quello di aggiungere il dispositivo (scanner) nel file di backend:

Aggiungere '**usb 0x03f0 0x2504'** a `/etc/sane.d/hp4200.conf` in modo che somigli a questo:

```
#
# Configuration file for the hp4200 backend
#
#
# HP4200
#usb 0x03f0 0x0105
usb 0x03f0 0x2504

```

### Epson Perfection 1270

Per Epson Perfection 1270, è necessario anche un firmware denominato `esfw3e.bin`. Esso può essere ottenuto installando il driver di Windows.

Modificare il file di configurazione del backend Snapscan, `/etc/sane.d/snapscan.conf`. Modificare la linea del percorso firmware con la vostra :

```
# Change to the fully qualified filename of your firmware file, if
# firmware upload is needed by the scanner
firmware /mnt/mydata/Backups/firmware/esfw3e.bin

```

E aggiungere la seguente riga alla fine, o dovunque vuoi

```
# Epson Perfection 1270
usb 0x04b8 0x0120

```

È possibile ottenere tali informazioni di codice (`usb 0x04b8 0x0120`) dal comando _sane-find-scanner_.

Aggiungere anche tali linee di informazione su `/etc/hotplug/usb/libsane.usermap` per impostare il privilegio, come :

```
# Epson Perfection 1270
libusbscanner 0x0003 0x04b8 0x0120 0x0000 0x0000 0x00 0x00 0x00 0x00 0x00 0x00 0x00000000

```

Ricollegare scanner, Ora hai un Epson Perfection 1270 funzionante.

**Note:** Posso scannerizzare un'immagine se io definisco il valore X e Y , ma poi si verifica un messaggio di errore del tipo: `scanimage: sane_start: Error during device I/O`, se qualcuno conosce il motivo, per favore aggiungerli a questa sezione.

*   Per prevenire l'errore `scanimage: sane_start: Error during device I/O` e blocco dello scanner stesso quando si cerca di eseguire la scansione con ADF (alimentatore automatico ) abilitato, ho dovuto rimuovere o commentare tutti i backend da `/etc/sane.d/dll.conf` e aggiungere questa riga: `snapscan` 

Finalmente! Se avete ancora errori di `Error I/O`, controllate il transportation lock dello scanner . È sul fondo dello scanner. Va aperto .

### Blocco durante la scansione a causa di XHCI in modalità di pre-boot

Se si ottiene un problema in cui viene rilevato lo scanner durante l'esecuzione di `lsusb` o `scanimage -L` e anche nelle applicazioni GUI, ma quando si tenta di eseguire la scansione poco dopo si blocca o si blocca durante la scansione, potrebbe essere necessaria questa correzione:

È inoltre possibile ottenere questo errore durante il tentativo di eseguire la scansione:

```
kernel: usb 1-2: new high-speed USB device number 8 using xhci_hcd
kernel: WARNING! power/level is deprecated; use power/control instead

```

La correzione è: Nelle impostazioni del UEFI/BIOS cambiare le impostazioni sotto _USB configuration_, _xhci pre-boot mode_ da enabled a disabled.