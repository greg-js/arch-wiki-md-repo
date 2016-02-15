Questo articolo descrive l'esecuzione di [VirtualBox](https://en.wikipedia.org/wiki/VirtualBox "wikipedia:VirtualBox") in Arch, si potrebbe essere interessati anche a [Arch Linux come Guest di VirtualBox](/index.php/Arch_Linux_VirtualBox_Guest "Arch Linux VirtualBox Guest").

[VirtualBox](http://www.virtualbox.org) è un emulatore di macchine virtuali simile a [VMware](/index.php/VMware "VMware"), ne possiede la maggior parte delle caratteristiche e in più ne aggiunge di nuove. E' costantemente in sviluppo e vengono aggiunte continuamente nuove funzionalità. Ad esempio la versione 2.2 ha introdotto il supporto all'accelerazione grafica 3D OpenGL sia per le macchine guest Linux che Solaris. Dispone di un'ottima GUI (QT o SDL) e di strumenti a linea di comando per la gestione delle macchine virtuali. Sono consentite anche operazioni senza un'uscita video (headless).

## Contents

*   [1 Installazione](#Installazione)
    *   [1.1 Installare le estensioni per VirtualBox](#Installare_le_estensioni_per_VirtualBox)
*   [2 Avviare VirtualBox](#Avviare_VirtualBox)
    *   [2.1 Risolvere l'impossibilità di eseguire rc.d setup vboxdrv](#Risolvere_l.27impossibilit.C3.A0_di_eseguire_rc.d_setup_vboxdrv)
*   [3 Configurazione](#Configurazione)
    *   [3.1 Rete](#Rete)
        *   [3.1.1 NAT](#NAT)
        *   [3.1.2 Bridged](#Bridged)
    *   [3.2 Guest Additions](#Guest_Additions)
        *   [3.2.1 Arch Linux Guests](#Arch_Linux_Guests)
        *   [3.2.2 Windows Guests](#Windows_Guests)
    *   [3.3 Tastiera e mouse tra host e guest](#Tastiera_e_mouse_tra_host_e_guest)
    *   [3.4 Usare la risoluzione massima del sistema host nel sistema guest](#Usare_la_risoluzione_massima_del_sistema_host_nel_sistema_guest)
    *   [3.5 Condividere le cartelle tra host e guest](#Condividere_le_cartelle_tra_host_e_guest)
    *   [3.6 Far funzionare l'audio nella macchina guest](#Far_funzionare_l.27audio_nella_macchina_guest)
    *   [3.7 Impostare la RAM e la memoria video nella macchina guest](#Impostare_la_RAM_e_la_memoria_video_nella_macchina_guest)
    *   [3.8 Impostare il CD-ROM nella macchina guest](#Impostare_il_CD-ROM_nella_macchina_guest)
    *   [3.9 Abilitare l'accelerazione D3D nelle macchine guest Windows](#Abilitare_l.27accelerazione_D3D_nelle_macchine_guest_Windows)
*   [4 Configurazione di un OS virtualizzato](#Configurazione_di_un_OS_virtualizzato)
    *   [4.1 Test di un CD/DVD live](#Test_di_un_CD.2FDVD_live)
*   [5 Manutenzione](#Manutenzione)
    *   [5.1 Ricompilare il modulo vboxdrv](#Ricompilare_il_modulo_vboxdrv)
    *   [5.2 Compattare un hard disk virtuale](#Compattare_un_hard_disk_virtuale)
        *   [5.2.1 Linux Guests](#Linux_Guests)
        *   [5.2.2 Windows Guests](#Windows_Guests_2)
    *   [5.3 Aumentare le dimensioni di un hard disk virtuale in un ambiente guest Windows](#Aumentare_le_dimensioni_di_un_hard_disk_virtuale_in_un_ambiente_guest_Windows)
    *   [5.4 Windows XP e telefoni Nokia](#Windows_XP_e_telefoni_Nokia)
*   [6 Migrare da un'altra VM](#Migrare_da_un.27altra_VM)
    *   [6.1 Convertire immagini QEMU](#Convertire_immagini_QEMU)
    *   [6.2 Convertire da immagini VMware](#Convertire_da_immagini_VMware)
*   [7 Tips & Tricks](#Tips_.26_Tricks)
    *   [7.1 Rendere possibile l'individuazione di Web-Cam e altre periferiche USB](#Rendere_possibile_l.27individuazione_di_Web-Cam_e_altre_periferiche_USB)
    *   [7.2 Inviare CTRL+ALT+F1 alla macchina guest](#Inviare_CTRL.2BALT.2BF1_alla_macchina_guest)
    *   [7.3 Avviare la VM all'avvio del sistema in un server senza uscita video (headless)](#Avviare_la_VM_all.27avvio_del_sistema_in_un_server_senza_uscita_video_.28headless.29)
    *   [7.4 Demone gestione guest](#Demone_gestione_guest)
    *   [7.5 Accedere a un server su una VM dall'host](#Accedere_a_un_server_su_una_VM_dall.27host)
    *   [7.6 DAEMON Tools](#DAEMON_Tools)
    *   [7.7 Usare VirtualBox su una memoria USB](#Usare_VirtualBox_su_una_memoria_USB)
    *   [7.8 phpVirtualBox](#phpVirtualBox)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 OpenBSD](#OpenBSD)
*   [9 Link Esterni](#Link_Esterni)

## Installazione

	[virtualbox](https://www.archlinux.org/packages/?name=virtualbox)

	Questa è la versione con licensa GPL di VirtualBox che può essere trovata nel repository community.

Installare il pacchetto base:

```
# pacman -S virtualbox

```

Per usufruire dell'interfaccia grafica installare anche il pacchetto [qt4](https://www.archlinux.org/packages/?name=qt4):

```
# pacman -S qt4

```

### Installare le estensioni per VirtualBox

VirtualBox necessita di un extension pack (VirtualBox Oracle VM VirtualBox Extension Pack) per offrire supporto a RDP, USB2.0, avvio PXE per schede video Intel, ecc. Esso è disponibile al seguente indirizzo: [Virtualbox Downloads](http://www.virtualbox.org/wiki/Downloads). L'extension pack è disponibile con licenza PUEL gratuita per uso personale. Per installare l'extension pack scaricato avviare VirtualBox, cliccare su preferenze e sul lato sinistro selezionare estensioni. Sul lato destro cliccare sull'icona aggiungi estensione ed aprire la cartella che contiene il pacchetto scaricato.

In alternativa è possibile installare l'Extension Pack dalla linea di comando usando VBoxManage.

```
VBoxManage extpack install <tarball> |

                   uninstall [--force] <name> |

                   cleanup

```

Oppure è possibile usare [virtualbox-ext-oracle](https://aur.archlinux.org/packages/virtualbox-ext-oracle/) da AUR.

## Avviare VirtualBox

A questo punto aggiungere gli utenti a cui si vuol consentire l'esecuzione di VirtualBox al gruppo _vboxusers_:

```
# gpasswd -a USERNAME vboxusers

```

Compilare i moduli richiesti:

```
# vboxbuild

```

Infine editare `/etc/[rc.conf](/index.php/Rc.conf_(Italiano) "Rc.conf (Italiano)")` ed aggiungere _vboxdrv_ nell'array MODULES per caricare il driver di VirtualBox all'avvio del sistema:

```
MODULES=(... _vboxdrv_)

```

Per caricare i moduli manualmente:

```
# modprobe vboxdrv

```

Per avviare VirtualBox:

```
$ virtualbox

```

### Risolvere l'impossibilità di eseguire rc.d setup vboxdrv

In alcuni casi dopo un'installazione di VirtualBox pulita non è possibile compilare i moduli ed appariranno dei messaggi di errore del tipo:

```
# rc.d setup vboxdrv
:: Unloading VirtualBox kernel modules [DONE]
:: Recompiling VirtualBox kernel modules [BUSY]
Look at /var/log/vbox-install.log to find out what went wrong
Look at /var/log/vbox-install.log to find out what went wrong
Look at /var/log/vbox-install.log to find out what went wrong
[DONE]
:: Reloading VirtualBox kernel modules}
```

con il file di log menzionato che conterrà:

```
Makefile:169: *** Error: unable to find the sources of your current Linux kernel. Specify KERN_DIR=<directory> and run Make again.  Stop.
cp: cannot stat `/tmp/vboxdrv-Module.symvers': No such file or directory
Makefile:94: *** Error: unable to find the sources of your current Linux kernel. Specify KERN_DIR=<directory> and run Make again.  Stop.
cp: cannot stat `/tmp/vboxdrv-Module.symvers': No such file or directory
Makefile:90: *** Error: unable to find the sources of your current Linux kernel. Specify KERN_DIR=<directory> and run Make again.  Stop.
```

Una soluzione è installare gli header del proprio kernel:

```
pacman -S linux-headers

```

oppure, se si ha una versione lts del kernel :

```
pacman -S linux-lts-headers

```

Successivamente potrebbe essere utile riavviare il sistema (ma potrebbe non essere necessario) e seguire i passi precedenti. La macchina virtuale a questo punto dovrebbe avviarsi.

## Configurazione

### Rete

La macchina guest può essere connessa in rete tramite vari metodi; tra questi troviamo reti [#NAT](#NAT) e [#Bridged](#Bridged). L'uso della rete [#NAT](#NAT) è il metodo più semplice e quello predefinito per le nuove macchine virtuali.

Per usare le modalità host-only e internal network è necessario caricare il modulo del kernel vboxnetadp. Il [manuale di VirtualBox](http://www.virtualbox.org/manual/UserManual.html) copre le varie opzioni disponibili per questi due tipi di reti. Queste non verranno trattate dato che per come sono fatte sono in gran parte indipendenti dall'OS.

#### NAT

Da VirtualBox:

*   accedere al menu _Impostazioni_ della VM;
*   dalla lista sulla sinistra cliccare su _Rete_; infine,
*   nel menu a discesa _Connessa a_ selezionare _NAT_.

Il server DHCP incluso in VirtualBox permette al sistema guest di essere configurato tramite DHCP. L'indirizzo IP NAT della prima scheda di rete è 10.0.2.0, quello della seconda scheda 10.0.3.0 e così via.

#### Bridged

La rete Bridged può essere impostata in vari modi, tra questi esiste una impostazione nativa che richiede una configurazione minima al prezzo di un minore controllo. Dalle ultime versioni VirtualBox può effettuare connessioni Bridged tra una macchina guest e un'interfaccia host wireless senza l'aiuto di utility di terze parti.

Prima di continuare caricare i moduli necessari:

```
# modprobe vboxnetflt

```

Da VirtualBox:

*   accedere al menu _Impostazioni_ della VM;
*   cliccare su _Rete_ dal menu sulla sinistra;
*   selezionare _Scheda con bridge_ nel menu a discesa _Connessa a_; infine,
*   nella lista a discesa _Nome_ selezionare il nome dell'interfaccia host connessa alla rete di cui si vuole faccia parte l'OS guest.

Avviare la macchina virtuale e configurare la rete normalmente; ad es. DHCP o IP statico.

### Guest Additions

Le Guest Additions permettono di condividere le cartelle, migliorare il supporto all'accelerazione grafica e abilitare gli appunti (clipboard) bidirezionali tra macchina guest e host. Un'altra caratteristica è l'integrazione del mouse che evita di doverlo rilasciare ogni volta che lo si usa nell' OS guest.

#### Arch Linux Guests

Fare riferimento a [Arch Linux VirtualBox Guest](/index.php/Arch_Linux_VirtualBox_Guest "Arch Linux VirtualBox Guest").

#### Windows Guests

Dopo aver installato Windows (XP, ecc.) sulla macchina virtuale selezionare _Devices → Install Guest Additions..._

Questo monterà l'immagine iso e Windows lancerà l'installer delle Guest Addition automaticamente. A questo punto seguire le istruzioni fino a completare l'installazione. Se si hanno le Guest Additions installate per una macchina virtuale e si vuole installarle per un'altra non è necessario scaricare di nuovo il file .iso. Selezionare "Periferiche → Dispositivi CD/DVD → Selezionare CD/DVD virtuale" e navigare in ~/.VirtualBox dove è situata l'immagine.

### Tastiera e mouse tra host e guest

*   Per catturare il mouse e la tastiera cliccare con il mouse all'interno della finestra della macchina virtuale.
*   Per disattivare la cattura premere il tasto `Ctrl` destro.

Per avere l'integrazione del mouse automatica tra host e guest installare le [#Guest Additions](#Guest_Additions) sulla macchina guest.

Quando si genera il file `xorg.conf` nella macchina guest tramite il comando `X -configure` la sezione InputDevice dovrebbe contenere il driver `mouse`. Dopo aver installato le Guest Additions sostituire `mouse` con `vboxmouse` quindi riavviare X o direttamente la macchina guest.

Atrimenti inserire manualmente le seguenti righe nel file `xorg.conf` della macchina guest:

```
Section "InputDevice"
   Identifier   "Mouse0"
   Driver       "vboxmouse"
   Option       "Protocol" "auto"
   Option       "Device" "/dev/input/mice"
   Option       "ZAxisMapping" "4 5 6 7"
EndSection

Section         "ServerLayout"
   Identifier   "X.org Configured"
   Screen     0 "Screen0" 0 0
   InputDevice  "Mouse0" "CorePointer"
   InputDevice  "Keyboard0" "CoreKeyboard"
EndSection

```

### Usare la risoluzione massima del sistema host nel sistema guest

Impostare la risoluzione del sistema guest nello script di `/boot/grub/menu.lst`, aggiungendo il codice vga corretto alla riga del kernel. Per una risoluzione di 1280x1024 ad es. sarà

```
# kernel /vmlinuz-linux root=/dev/disk/by-uuid/7bdc5dee-8fb0-4260-bc43-60ac6e4e4a54 ro vga=795

```

Aggiungere la risoluzione nel file `/etc/X11/xorg.conf`, ad es.

```
Section "Screen"
...
	SubSection "Display"
		Viewport   0 0
		Depth     24
		Modes "1280x1024" "1024x768"
	EndSubSection
...
EndSection

```

Se si incontrano problemi con la risoluzione e il sistema torna indietro alla risoluzione successiva più bassa nella riga 'Modes' omettere semplicemente quest'ultima. Esempio

```
               Modes "1280x1024"

```

### Condividere le cartelle tra host e guest

Nelle impostazioni della macchina virtuale andare nel tab Cartelle condivise e aggiungere qui le cartelle che si vogliono condividere.

*   NOTA: è necessario installare le Guest Additions prima di poter usare le cartelle condivise.

```
In un host Linux _Dispositivi → Installa Guest Additions_
Si (quando viene chiesto di scaricare l'immagine del CD)
Mount (quando viene chiesto di registrarsi e ed effettuare il mount)

```

In un host Linux creare una o più cartelle per condividere i file e impostare queste cartelle come condivise attraverso il menu di VirtualBox.

In una guest Windows a partire da VirtualBox 1.5.0 le cartelle condivise sono esplorabili e visibili da Esplora risorse. Aprire Esplora risorse e cercare le cartelle condivise in _Risorse di rete → Tutta la rete → VirtualBox Shared Folders_

Lanciare Esplora risorse (digitare explorer da esegui) per sfogliare le Risorse di rete -> espandere l'albero tramite il segno (+): Tutta la rete → Virtualbox Shared Folder → **Vboxsvr** → qui è possibile trovare tutte le cartelle condivise e impostare dei collegamenti per essi nella macchina guest. In alternativa è possibile usare "Aggiungi risorsa di rete _e cercare "Vboxsvr"._

In alternativa nel Prompt dei comandi di Windows digitare:

```
net use x: \\VBOXSVR\sharename

```

Sostituire `x:` con la lettera del drive che si vuole utilizzare per la condivisione e sharename con il nome specificato in VBoxManage.

In una macchina guest Windows per velocizzare il caricamento e il salvataggio dei file (ad es. per Microsoft Office) nelle cartelle condivise editare il file _c:\windows\system32\drivers\etc\hosts_ come segue:

```
127.0.0.1 localhost vboxsvr

```

In una guest Linux digitare il seguente comando:

```
# mount -t vboxsf [-o OPTIONS] sharename mountpoint

```

**Nota:** sharename è opzionale o è lo stesso scelto nelle impostazioni di VirtualBox, mountpoint è il punto di mount della cartella condivisa

	Il montaggio automatico delle cartelle condivise nella linux-guest è possibile editando il file /etc/fstab. E' possibile anche specificare uid=# e gid=# (dove # va sostituito con dal valore numerico di uid e gid) per montare le cartelle condivise senza bisogno dei permessi di root.

(può essere utile per montare parti della ~/home del sistema host per l'uso nel sistema guest Linux. Per fare questo aggiungere una riga nel seguente formato nel file /etc/fstab della macchina guest:

```
sharename mountpoint vboxsf uid=#,gid=# 0 0

```

Sostituire `sharename` con il nome assegnato alla cartella condivisa in VBoxManage, e mountpoint con il percorso in cui si vuole montare la cartella condivisa (es. /mnt/share). Valgono le regole tipiche di mount, quindi se la cartella non esiste va prima creata. Se è stato detto a VirtualBox di montare automaticamente le cartelle condivise questo passo non è necessario e le cartelle dovrebbero trovarsi da qualche parte dentro la directory /media.

Oltre alle opzioni standard fornite dal comando mount sono disponibili anche:

```
iocharset=CHARSET

```

per impostare il set di caratteri usati per le operazioni di I/O (di default utf8) e

```
convertcp=CHARSET

```

per specificare il set di caratteri usato nel nome della cartella condivisa (di default utf8).

### Far funzionare l'audio nella macchina guest

Nelle impostazioni della macchina recarsi nel tab audio e selezionare il driver adatto al proprio sistema audio (ALSA, OSS o PulseAudio).

### Impostare la RAM e la memoria video nella macchina guest

E' possibile cambiare le impostazioni di default andando in _Impostazioni → Generale_.

### Impostare il CD-ROM nella macchina guest

E' possibile cambiare le impostazioni di default andando in _Impostazioni → Archiviazione_.

Spuntare mount CD/DVD drive e selezionare una delle opzioni successive.

### Abilitare l'accelerazione D3D nelle macchine guest Windows

Le ultime versioni di VirtualBox offrono il supporto all'accelerazione OpenGL all'interno della macchina guest. Essa può essere abilitata spuntando la relativa opzione situata appena sotto l'impostazione della memoria video nel menu Impostazioni della macchina e installando le Guest Addition. Tuttavia la maggior parte dei giochi Windows usa le Direct3D (parte delle DirectX) e non le OpenGL e quindi non si trae vantaggio da questa funzionalità. Comunque è possibile ottenere l'accelerazione Direct3D prendendo in prestito le librerie d3d da Wine, in modo da poter tradurre le chiamate alle d3d in OpenGL che beneficiano dell'accelerazione hardware.

Dopo aver ablitato l'accelerazione OpenGL come descritto sopra andare all'indirizzo [http://www.nongnu.org/wined3d/](http://www.nongnu.org/wined3d/) dalla macchina Windows e scaricare "Latest version (Installer):". Riavviare la macchina guest in modalità provvisoria (premere F8 prima che appaia la schermata di Windows ma dopo che sia scomparsa la schermata VirtualBox) e installare wined3d, accettando le impostazioni di default durante l'installazione (volendo si può selezionare il supporto alle DirectX10, non modificare nient'altro). Riavviare in modalità normale e sarà disponibile l'accelerazione Direct3D.

**Nota:** Questo hack potrebbe non funzionare con alcuni giochi, in base ai controlli hardware che effettua e alle parti delle D3D che utilizza.

**Nota:** Questo hack è stato testato solo su windows XP e Windows 7 RC guests AFAIK e non funziona su macchine guest Windows 7\. Se hai effettuato dei test con altre versioni di Windows per favore aggiungi i tuoi risultati qui.

## Configurazione di un OS virtualizzato

VirtualBox necessita di essere configurato per virtualizzare un altro sistema operativo.

### Test di un CD/DVD live

Cliccare su 'Nuova' per creare un nuovo ambiente virtuale. Assegnargli un nome e impostare il tipo di sistema operativo e la versione. Selezionare la dimensione della memoria (nota: la maggior parte dei sistemi operativi richiede almeno 512MB per funzionare al meglio). Creare un nuovo disco fisso virtuale (un disco fisso virtuale è un file che conterrà il filesystem e i file del sistema operativo).

Quando il disco fisso è stato creato cliccare su 'Impostazioni', quindi CD/DVD-ROM e spuntare 'Monta periferica CD/DVD'. Infine selezionare l'immagine ISO.

## Manutenzione

### Ricompilare il modulo vboxdrv

Ogni volta che la versione del kernel cambia (a causa di un aggiornamento, una ricompilazione, ecc.) il modulo vboxdrv deve essere ricompilato.

Assicurarsi che _linux-headers_ sia già installato ed eseguire il seguente comando:

```
# rc.d setup vboxdrv

```

Questo compilerà il modulo del kernel di VirtualBox per il _kernel in esecuzione_; se si è appena aggiornato il kernel riavviare il sistema prima di ricompilare il modulo di VirtualBox.

Dopo aver ricompilato il modulo non dimenticare di ricaricarlo:

```
# modprobe vboxdrv

```

_vboxdrv_ e vboxnetflt _dovrebbe trovarsi nella sezione MODULES=() del file /etc/rc.conf_

Se si sta compilando un vecchio pacchetto virtualbox_bin compilato da AUR eseguire:

```
# vbox_build_module

```

Se è necessario ricompilare le Guest Additions in un'installazione guest di Arch Linux usare il seguente comando:

```
# rc.d setup rc.vboxadd

```

### Compattare un hard disk virtuale

#### Linux Guests

Avviare la VM Linux ed eliminare tutto il superfluo (pacchetti non voluti, file temporanei, ecc.). Successivamente pulire lo spazio libero usando dd o meglio dclfdd:

```
$ dcfldd if=/dev/zero of=fillfile bs=4M

```

Quando il fillfile raggiunge il limite dell'hdd virtuale la maggior parte dello sapzio utente (blocchi non riservati) viene riempito. In alternativa eseguire il comando come root per ottenerlo tutto. Un esempio di messaggio che si potrebbe ottenere è: "8192 blocks (8192Mb) written.dcfldd:: No space left on device."

Arrivati a questo punto è necessario rimuovere il fillfile e spegnere la VM:

```
$ rm -f fillfile && sudo shutdown -hF now

```

**Nota:** L'opzione F forza una verifica del disco al riavvio, che è consigliato dopo un'operazione di compattazione.

A questo punto compattare il disco:

```
$ VBoxManage modifyhd /path/to/your.vdi --compact

```

#### Windows Guests

Vedere [How to compact a VirtualBox virtual disk image (VDI)](http://my.opera.com/locksley90/blog/2008/06/01/how-to-compact-a-virtualbox-virtual-disk-image-vdi)

### Aumentare le dimensioni di un hard disk virtuale in un ambiente guest Windows

ATTENZIONE: TESTATO SOLO SU MACCHINE GUEST XP

Se lo spazio libero sul disco rigido virtuale creato inizia ad essere poco è possibile è possibile seguire i seguenti passi:

Creare un nuovo vdi in ~/.VirtualBox/HardDisks digitando nel terminale:

```
# cd ~/.VirtualBox/HardDisks
# VBoxManage createhd -filename new.vdi --size 10000 --remember

```

Dove size è in mb, in questo esempio 10000MB ~= 10GB e new.vdi è il nome del disco rigido appena creato.

In seguito il vecchio vdi deve essere clonato nel nuovo vdi, questo processo necessita di un po' di tempo:

```
# VBoxManage clonehd old.vdi new.vdi --existing

```

Scollegare il vecchio disco rigido e collegare il nuovo, sostituire VMName con il nome della propria VM:

```
# VBoxManage modifyvm VMName --hda none
# VBoxManage modifyvm VMName --hda new.vdi

```

Avviare la VM, eseguire Partition Wizard 5 per ridimensionare la partizione al volo e riavviare.

Rimuovere il vecchio vdi da VirtualBox ed eliminare il file:

```
# VBoxManage closemedium disk old.vdi
# rm old.vdi

```

### Windows XP e telefoni Nokia

Per far funzionare i telefoni Nokia tramite la modalità PC Suite in Windows XP VirtualBox necessita di due semplici passi:

**1.** Aggiungere una regola ad udev tramite `/etc/udev/rules.d/40-permissions.rules`:

```
LABEL="usb_serial_start"
ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", \
GROUP="usbfs", MODE="0660", GROUP="dialout"
LABEL="usb_serial_end"

```

**2.** Creare il gruppo usbfs e aggiungere il proprio utente ad esso:

```
$ sudo groupadd usbfs
$ sudo usermod -a -G usbfs $USER

```

Dopo il logout connettere un telefono Nokia in modalità PC Suite ed avviare XP per testare la nuova regola.

## Migrare da un'altra VM

Il programma `qemu-img` può essere usato per convertire immagini da un formato ad un altro, o per comprimere o criptare un'immagine.

```
  # pacman -S qemu

```

### Convertire immagini QEMU

Per convertire immagini QEMU per poterle usare in VirtualBox per prima cosa convertirle in formato _raw_, successivamente usare l'utilità di conversione di VirtualBox per convertire e comprimere l'immagine nel formato nativo.

```
  $ qemu-img convert -O raw test.qcow2 test.raw
  $ VBoxManage modifyvdi /full/path/to/test.vdi compact
oppure
  $ qemu-img convert -O raw test.qcow2 test.raw
    (of course you must have installed qemu package for that)
  $ VBoxManage convertfromraw /full/path/to/test.raw /full/path/to/test.vdi
  $ VBoxManage modifyvdi      /full/path/to/test.vdi compact

```

### Convertire da immagini VMware

Eseguire

```
  $ VBoxManage clonehd source.vmdk target.vdi --format VDI

```

Questo comando potrebbe non essere più necessario con le versioni più recenti di VirtualBox (da confermare)

## Tips & Tricks

### Rendere possibile l'individuazione di Web-Cam e altre periferiche USB

Assicurarsi che si stia filtrando qualunque periferica tranne mouse e tastiere così che esse non partano all'avvio. In questo modo Windows individuerà le periferiche all'avvio.

### Inviare CTRL+ALT+F1 alla macchina guest

Se il SO guest è una distro Linux e si vorrebbe aprire una nuova tty o uscire da X digitando `Ctrl`+`Alt`+`F1`, si può inviare facilmente questo comando all'OS guest semplicemente premendo il 'tasto Host' (di solito `Ctrl` nel lato destro della tastiera) + `F1` o `F2`, ecc.

### Avviare la VM all'avvio del sistema in un server senza uscita video (headless)

Aggiungere la seguente linea in /etc/rc.local

```
exec /bin/su -c 'VBoxManage startvm --type headless <_UUID|NAME_>' _PREFERED_USER_ >/dev/null 2>&1

```

dove <UUID|NAME> è l'identificativo della macchina guest e PREFERRED_USER è il profilo utente che contiene la VM e i file .vdi.

Dato che exec sostituisce il processo attualmente avviato non sarà possibile far partire una seconda VM o eseguire qualunque altro programma dopo di esso. Se questo è un problema provare le righe seguenti:

```
su -c 'VBoxHeadless -s <UUID|NAME> &' -s /bin/sh PREFERED_USER >/dev/null 2>&1

```

E' consigliabile usare per su e VBoxHeadless un percorso completo. Aggiungere ulteriori righe come quella di sopra per avviare più VM. I comandi successivi presenti nel file rc.local saranno eseguiti.

Per determinare le VM disponibili per un utente digitare:

```
su -c 'VBoxManage list vms' PREFERED_USER

```

Per salvare lo stato di una VM avviata:

```
su -c 'VBoxManage controlvm <UUID|NAME> savestate' PREFERED_USER

```

Un buon punto dove posizionare questa riga potrebbe essere rc.local.shutdown.

### Demone gestione guest

Di seguito è elencato un [demone](/index.php/Daemon_(Italiano) "Daemon (Italiano)") per automatizzare la gestione delle VM. Le macchine guest verranno avviate al boot e il loro stato verrà salvato in chiusura. All'avvio del daemon se esso non funziona si otterrà il messaggio "./vbox_service: line 31: out[${m[1]}]: bad array subscript".

Il file di configurazione:

 `/etc/conf.d/vbox_service` 

```
# Guests to manage:
#VB_GUESTS=('OpenBSD' 'Slackware' 'Windows XP')
#
# Disable a guest by prepending a bang:
#VB_GUESTS=('OpenBSD' 'Slackware' !'Windows XP')
#
# Default value matches none:
VB_GUESTS=()

# User to run Virtual Box as:
VB_USER='vbox'

```

Lo script:

 `/etc/rc.d/vbox_service` 

```
#!/bin/bash

. /etc/rc.conf
. /etc/rc.d/functions

unset VB_GUESTS
unset VB_USER
[[ -r /etc/conf.d/vbox_service ]] && . /etc/conf.d/vbox_service
[[ ${VB_GUESTS[@]} ]] || VB_GUESTS=()
[[ ${VB_USER[@]} ]]   || VB_USER='vbox'

match() {
 [[ $REPLY =~ $1 ]] && m=("${BASH_REMATCH[@]}")
}

vm_raw() {
 local argv=''
 printf -v argv ' %q ' "$@"
 su -c "/usr/bin/VBoxManage $argv" -s /bin/sh "$VB_USER"
}

vm_ls() {
 local -A out=''
 local -i ret=1

 local m=()
 while read -r; do
   match '^"(.+)" \{(.+)\}$'
   out[${m[1]}]=${m[2]}
 done < <(vm_raw list vms)

 local i=''
 for i in "${VB_GUESTS[@]##!*}"; do
   if [[ ${out[$i]} ]]; then
     printf ' %q ' "${out[$i]}"
     ret=0
   fi
 done

 return $ret
}

vm_envinit() {
 local m=()
 while read -r; do
   match '^(.+)="?([^"]+)'
   env[$1:${m[1]}]=${m[2]}
 done < <(vm_raw showvminfo --machinereadable "$1")
}

start() {
 if [[ ${env[$1:VMState]} != 'running' ]]; then
   vm_raw startvm --type headless "$1"
 fi
}

stop() {
 if [[ ${env[$1:VMState]} == 'running' ]]; then
   vm_raw controlvm "$1" savestate
 fi
}

restart() {
 stop "$1"
 sleep 3
 start "$1"
}

usage() {
 printf '%s\n' "usage: $0 <start|stop|restart> [name|uuid]..." >&2
}

if [[ ! $1 =~ ^(start|stop|restart)$ ]]; then
  usage
  exit 2
fi
cmd=$1
shift
(($#)) || eval set -- "$(vm_ls)"

stat_busy "${cmd^}ing VMs:"
trap 'stat_die' ERR
set -Ee

declare -A env=''

for i; do
  [[ $i ]]
  vm_envinit  "$i"
  stat_append "${env[$i:name]}, "
  $cmd        "${env[$i:UUID]}" &>/dev/null
done

stat_done

```

### Accedere a un server su una VM dall'host

Per accedere ad Apache su una VM SOLO dalla macchina host, eseguire semplicemente i seguenti comandi sull'host:

```
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/pcnet/0/LUN#0/Config/Apache/HostPort" 8888
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/pcnet/0/LUN#0/Config/Apache/GuestPort" 80
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/pcnet/0/LUN#0/Config/Apache/Protocol" TCP

```

Dove 8888 è la porta su cui è in ascolto l'host e 80 è la porta della VM a cui Apache invia i segnali. Lo stesso procedimento vale per configurare SSH, ecc. cambiando "Apache" con il servizio desiderato e usando differenti porte.

Nota: "pcnet" si riferisce alla scheda di rete della VM. Se nella propria VM si sta usando una scheda Intel sostituire "pcnet" con "e1000"

*   da [[1]](http://mydebian.blogdns.org/?p=111)

### DAEMON Tools

Anche se VirtualBox può montare senza problemi le immagini ISO alcuni formati immagine non possono essere convertiti in formato ISO. Ad esempio ccd2iso ignora i file .ccd e .sub, il che può portare ad immagini ISO danneggiate. cdemu, fuseiso e MagicISO si comportano allo stesso modo. In questi casi non c'è altra scelta che usare i Daemon Tools all'interno di VirtualBox.

Le recenti versioni di Daemon Tools rifiutano di installarsi per cui usare la seguente versione: [[2]](http://www.disc-tools.com/download/daemon347+hashcalc)

### Usare VirtualBox su una memoria USB

Quando si usa VirtualBox su una memoria USB, ad esempio per avviare una macchina installata con un'immagine ISO è necessario creare manualmente i VDMK dai file esistenti. Tuttavia una volta che i nuovi VMDK sono stati creati e ci si sposta su un'altra macchina possono verificarsi dei problemi lanciando la macchina virtuale. Per sbarazzarsi di questo problema è possibile usare il seguente script per avviare VirtualBox. Questo script ripulisce i vecchi file VMDK e ne crea dei nuovi per voi:

```
#!/bin/bash

# Erase old VMDK entries
rm ~/.VirtualBox/*.vmdk

# Clean up VBox-Registry
sed -i '/sd/d' ~/.VirtualBox/VirtualBox.xml

# Remove old harddisks from existing machines
find ~/.VirtualBox/Machines -name \*.xml | while read file; do
  line=`grep -e "type\=\"HardDisk\"" -n $file | cut -d ':' -f 1`
  if [ -n "$line" ]; then
    sed -i ${line}d $file
    sed -i ${line}d $file
    sed -i ${line}d $file
  fi
  sed -i "/rg/d" $file
done

# Delete prev-files created by VirtualBox
find  ~/.VirtualBox/Machines -name \*-prev -exec rm '{}' \;

# Recreate VMDKs
ls -l /dev/disk/by-uuid | cut -d ' ' -f 9,11 | while read ln; do
  if [ -n "$ln" ]; then
    uuid=`echo "$ln" | cut -d ' ' -f 1`
    device=`echo "$ln" | cut -d ' ' -f 2 | cut -d '/' -f 3 | cut -b 1-3`

    # determine whether drive is mounted already
    checkstr1=`mount | grep $uuid`
    checkstr2=`mount | grep $device`
    checkstr3=`ls ~/.VirtualBox/*.vmdk | grep $device`
    if [[ -z "$checkstr1" && -z "$checkstr2" && -z "$checkstr3" ]]; then
      VBoxManage internalcommands createrawvmdk -filename ~/.VirtualBox/$device.vmdk -rawdisk /dev/$device -register
    fi
  fi
done

# Start VirtualBox
VirtualBox

```

Notare che il proprio utente deve essere aggiunto al gruppo "disk" per creare i VMDK di unità esistenti.

### phpVirtualBox

Un'implementazione AJAX open source dell'interfaccia utente di VirtualBox scritta in PHP. Come ogni moderna interfaccia web consente di accedere e controllare VirtualBox da remoto. Gran parte del suo codice è basato sul progetto (inattivo) vboxweb. Consente all'amministratore in remoto, graficamente, di amministrare la macchina virtuale senza il bisogno di loggarsi all'interno del proprio server headless di VirtualBox.

E' richiesta la versione PUEL di VirtualBox.

Una guida di installazione è disponibile qui: [http://code.google.com/p/phpvirtualbox/wiki/Installation](http://code.google.com/p/phpvirtualbox/wiki/Installation)

Gli utenti di Arch Linux dovrebbero decommentare le seguenti 2 estensioni in _/etc/php/php.ini_

```
extension=json.so
extension=soap.so

```

## Troubleshooting

### OpenBSD

Alcuni utenti con macchine datate potrebbero avere problemi nell'esecuzione di VM OpenBSD che si manifesterebbero con molti segmentation fault e totale instabilità. Avviare VirtualBox con l'argomento -norawr0 potrebbe risolvere il problema:

```
$ VBoxSDL -norawr0 -vm NameOfYourOpenBSDVM

```

Vedere anche [PhpVirtualBox](/index.php/PhpVirtualBox "PhpVirtualBox")

## Link Esterni

*   [VirtualBox User Manual](http://www.virtualbox.org/manual/UserManual.html)