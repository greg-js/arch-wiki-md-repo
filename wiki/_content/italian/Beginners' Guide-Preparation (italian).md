**Suggerimento:** Questa è una parte della versione suddivisa in pagine multiple della Guida per Principianti. [Cliccare qui](/index.php/Guida_per_Principianti "Guida per Principianti") se si preferisce consultare la guida nella sua interezza.

Questa pagina servirà da guida nel processo di installazione di [Arch Linux](/index.php/Arch_Linux_(Italiano) "Arch Linux (Italiano)") utilizzando gli [Arch Install Scripts](https://projects.archlinux.org/arch-install-scripts.git/). Prima di procedere, si consiglia di leggere velocemente le [FAQ](/index.php/FAQ_(Italiano) "FAQ (Italiano)").

Il [wiki di Arch](/index.php/Main_page_(Italiano) "Main page (Italiano)"), mantenuto dalla comunità, è la risorsa primaria che deve essere consultato in caso di problemi. Sono disponibili anche dei canali [IRC channel](/index.php/IRC_channel "IRC channel") (per la comunità italiana: [irc://irc.azzurra.org/archlinux](irc://irc.azzurra.org/archlinux) o [irc://irc.freenode.net/#archlinux.it](irc://irc.freenode.net/#archlinux.it), mentre per il supporto internazionale: [irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)), ed il [forum italiano](http://www.archlinux.it/forum/) o [internazionale](https://bbs.archlinux.org/), che sono eccellenti risorse, nel caso la risposta non possa essere trovata altrove. Seguendo il [metodo Arch](/index.php/The_Arch_Way_(Italiano) "The Arch Way (Italiano)"), si consiglia di digitare `man *comando*` per leggere la pagina `man` pagina di un qualsiasi comando che non si conosce.

## Contents

*   [1 Preparazione](#Preparazione)
    *   [1.1 Requisiti di Sistema](#Requisiti_di_Sistema)
        *   [1.1.1 Preparare il supporto di installazione più recente](#Preparare_il_supporto_di_installazione_pi.C3.B9_recente)
        *   [1.1.2 Installazione tramite Rete](#Installazione_tramite_Rete)
        *   [1.1.3 Installazione da un sistema Linux esistente](#Installazione_da_un_sistema_Linux_esistente)
        *   [1.1.4 Installazione su Macchina Virtuale](#Installazione_su_Macchina_Virtuale)
        *   [1.1.5 Avviare il supporto di installazione](#Avviare_il_supporto_di_installazione)
            *   [1.1.5.1 Controllare se il supporto di installazione si avvia in modalità UEFI](#Controllare_se_il_supporto_di_installazione_si_avvia_in_modalit.C3.A0_UEFI)
        *   [1.1.6 Risoluzione dei problemi di avvio](#Risoluzione_dei_problemi_di_avvio)

## Preparazione

**Nota:** Se si desidera installare da una distribuzione GNU/Linux esistente, si legga [questo articolo](/index.php/Install_from_existing_Linux_(Italiano) "Install from existing Linux (Italiano)"). Ciò può essere utile soprattutto se si prevede di installare Arch Linux tramite [VNC](/index.php/VNC "VNC") o [SSH](/index.php/Secure_Shell_(Italiano) "Secure Shell (Italiano)") remoto. Gli utenti che cercano di eseguire l'installazione di Arch Linux da remoto tramite un connessione [SSH](/index.php/Secure_Shell_(Italiano) "Secure Shell (Italiano)"), dovrebbero leggere [Installare tramite SSH](/index.php/Install_from_SSH_(Italiano) "Install from SSH (Italiano)") per ulteriori suggerimenti.

### Requisiti di Sistema

Arch Linux dovrebbe funzionare su qualsiasi macchina [i686](https://en.wikipedia.org/wiki/it:P6_(microarchitecture) compatibile e con un minimo di 64 MB di RAM. Una installazione di base con tutti i pacchetti dal gruppo *base* dovrebbe prendere circa 500 MB di spazio su disco. Se si lavora con spazio limitato, questo può essere tagliato in modo considerevole, ma dovrete sapere cosa si sta facendo.

#### Preparare il supporto di installazione più recente

L'ultima versione del supporto di installazione può essere ottenuta dalla pagina di [download](https://www.archlinux.org/download/). Si noti che la singola immagine ISO supporta entrambe le architetture a 32 e 64 bit. É altamente raccomandato di utilizzare sempre l'ultima immagine ISO rilasciata.

*   Le immagini da installare sono firmate, e si consiglia vivamente di verificare la loro firma prima dell'uso. Scaricare il file di firma *.sig* dalla pagina di download (o uno dei mirror elencati qui ) per la stessa directory del file *.iso*. Su Arch Linux , usare `pacman-key -v *iso-file*.sig` da root; in altri ambienti usufruire , sempre come root , di gpg2 direttamente con `gpg2 --verify *iso-file.sig*`. Sono inoltre riportate le integrità checksum del file MD5 e SHA1.

**Nota:** La verifica gpg2 fallirà se non avete scaricato la corrispondente chiave pubblica per l'ID della chiave RSA. Vedere [http://sparewotw.wordpress.com/2012/10/31/how-to-verify-signature-using-sig-file/](http://sparewotw.wordpress.com/2012/10/31/how-to-verify-signature-using-sig-file/) per i dettagli.

*   Masterizzare l'immagine ISO su un CD o DVD tramite il vostro software preferito. Su Arch questo può essere fatto seguendo [Optical disc drive (Italiano)#Masterizzare](/index.php/Optical_disc_drive_(Italiano)#Masterizzare "Optical disc drive (Italiano)")

**Nota:** La qualità delle unità ottiche e degli stessi dischi può variare. In generale, per masterizzazioni affidabili è raccomandata una velocità bassa. Se si verifica un comportamento imprevisto del CD, provare a masterizzarne un altro usando la velocità minima.

*   In alternativa potete scrivere l'immagine ISO su un supporto USB. Si veda [Installare da supporto USB](/index.php/Installare_da_supporto_USB "Installare da supporto USB") per maggiori informazioni.

#### Installazione tramite Rete

Invece di scrivere i supporti di avvio di un'unità ottica o USB, è possibile, in alternativa, avviare un'immagine ISO in rete. Questo funziona bene quando si dispone già di un server configurato. Si prega di consultare l'articolo [PXE](/index.php/PXE "PXE") per ulteriori informazioni e quindi continuare l'avvio di [avviare il supporto di installazione di Arch Linux](#Avviare_il_supporto_di_installazione).

#### Installazione da un sistema Linux esistente

In alternativa, è possibile installare da un sistema Linux già in esecuzione. Vedere [Install from existing Linux (Italiano)](/index.php/Install_from_existing_Linux_(Italiano) "Install from existing Linux (Italiano)").

#### Installazione su Macchina Virtuale

L'installazione su una [macchina virtuale](https://en.wikipedia.org/wiki/it:Virtual_machine "wikipedia:it:Virtual machine") è un buon modo per familiarizzare con Arch Linux e la sua procedura di installazione senza lasciare il sistema operativo corrente e ripartizionare il disco rigido. E vi permetterà anche di mantenere questa **Guida per Principianti** aperta nel vostro browser per tutta l'installazione. Alcuni utenti potrebbero trovare vantaggioso avere un autonomo sistema Arch Linux su un drive virtuale a scopo di test.

Esempi di software di virtualizzazione sono [VirtualBox](/index.php/VirtualBox_(Italiano) "VirtualBox (Italiano)"), [VMware](/index.php/VMware_(Italiano) "VMware (Italiano)"), [QEMU](/index.php/QEMU "QEMU"), [Xen](/index.php/Xen "Xen"), [Parallels](/index.php/Parallels "Parallels").

La procedura esatta per la preparazione di una macchina virtuale dipende dal software, ma generalmente attenersi alla seguente procedura:

1.  Creare l'immagine disco virtuale che ospiterà il sistema operativo.
2.  Configurare correttamente i parametri della macchina virtuale.
3.  Avviare l'Immagine ISO scaricata con un drive CD virtuale.
4.  Continuare con [Avviare il supporto di installazione di Arch Linux](#Avviare_il_supporto_di_installazione).

Gli articoli seguenti possono risultare utili:

*   [Arch Linux come guest VirtualBox](/index.php/VirtualBox#Arch_Linux_guests "VirtualBox")
*   [Arch Linux come guest di VirtualBox in un disco fisico](/index.php/VirtualBox_Arch_Linux_Guest_On_Physical_Drive "VirtualBox Arch Linux Guest On Physical Drive")
*   [Arch Linux come guest VMware](/index.php/Installing_Arch_Linux_in_VMware "Installing Arch Linux in VMware")
*   [Spostamento di un'installazione esistente in una macchina virtuale (o viceversa)](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

#### Avviare il supporto di installazione

La maggior parte dei sistemi moderni permettono di selezionare il dispositivo di avvio durante la fase di [POST](https://en.wikipedia.org/wiki/it:Power-on_self_test "wikipedia:it:Power-on self test"), di solito premendo il tasto `F12` mentre la schermata iniziale del BIOS è visibile. Selezionare il dispositivo che contiene l'ISO si Arch Linux. In alternativa, bisogna cambiare l'ordine di avvio dalle impostazioni del BIOS. Premere un tasto (generalmente `Canc`, oppure `F1`,`F2`,`F11` o `F12`) durante la fase [POST](https://en.wikipedia.org/wiki/it:Power-on_self_test "wikipedia:it:Power-on self test") di accensione. Questo vi porterà nella schermata delle impostazioni del BIOS in cui è possibile impostare l'ordine in cui il sistema ricerca i dispositivi di boot. Impostare il dispositivo che contiene l'ISO di ArchLinux come primo dispositivo di avvio.Una volta eseguita tale operazione selezionare "Save & Exit" (o equivalente nel BIOS) e il computer dovrebbe quindi completare il suo normale processo di avvio.

Quando apparirà il menù di Arch, selezionare "Boot Arch Linux" e premere `enter` per avviare l'ambiente live dove verrà eseguita l'installazione vera e propria (se state avviando tramite il supporto in modalità UEFI, l'opzione di avio dovrebbe essere qualcosa di simile :"Arch Linux archiso x86_64 UEFI").

Una volta avviato l'ambiente live, la shell è [Zsh](/index.php/Zsh "Zsh"), questo vi offre completamento avanzato col tasto Tab, e altre caratteristiche come parte della [configurazione grml](http://grml.org/zsh/).

##### Controllare se il supporto di installazione si avvia in modalità UEFI

Nel caso abbiate una scheda madre [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Italiano) "Unified Extensible Firmware Interface (Italiano)") e la modalità di avvio UEFI è attiva (ed è preferibile rispetto alla modalità BIOS/Legacy), il CD/USB lancerà automaticamente il kernel Arch Linux (Kernel [EFISTUB](/index.php/EFISTUB "EFISTUB") tramite il Boot Manager [Gummiboot](/index.php/Gummiboot "Gummiboot")). Per verificare se si è effettuato l'avvio in modalità UEFI controllare che la directory `/sys/firmware/efi/` sia stata creata eseguire:

```
# mount -t efivarfs efivarfs /sys/firmware/efi/efivars              # ignorare se già montati
# efivar -l

```

Se efivar elenca le variabili UEFI correttamente, allora il boot in modalità UEFI è stato eseguito correttamente. Altrimenti controllare tutti che i requisiti elencati in [Unified Extensible Firmware Interface#Requirements for UEFI Variables support to work properly](/index.php/Unified_Extensible_Firmware_Interface#Requirements_for_UEFI_Variables_support_to_work_properly "Unified Extensible Firmware Interface") siano soddisfatti.

#### Risoluzione dei problemi di avvio

*   Se siete in possesso di una scheda grafica Intel e lo schermo rimane vuoto durante il processo di boot, il problema è dovuto probabilmente all'impostazione in modalità [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting"). Una possibile soluzione è quella di riavviare e premere il tasto `e` sulla voce che si sta tentando di eseguire all'avvio ( i686 o x86_64 ). Inserire alla fine della stringa delle opzioni del kernel `nomodeset` e premere `Invio`. In alternativa aggiungere `video=SVIDEO-1:d`, che dovrebbe permettere di poter funzionare senza disattivare il kernel mode setting (KMS). Si può anche provare `i915.modeset=0`. Consultare l'articolo [Intel](/index.php/Intel_(Italiano) "Intel (Italiano)") per ulteriori informazioni.

*   Se lo schermo non si spegne ed il processo di avvio si blocca durante il tentativo di caricare il kernel, riavviare e premere `Tab` sulla voce che si sta tentando di eseguire all'avvio, ed inserire alla fine della stringa delle opzioni del kernel `acpi=off` e premere `Invio`.

**[Guida per Principianti](/index.php/Beginners%27_Guide_(Italiano) "Beginners' Guide (Italiano)")**

* * *

**Preparazione** >> [Installazione](/index.php/Beginners%27_Guide/Installation_(Italiano) "Beginners' Guide/Installation (Italiano)") >> [Post-Installazione](/index.php/Beginners%27_Guide/Post-Installation_(Italiano) "Beginners' Guide/Post-Installation (Italiano)")