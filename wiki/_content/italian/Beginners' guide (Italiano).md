**Suggerimento:** Questa pagina è disponibile anche in una versione suddivisa in pagine multiple, piuttosto che in una sola. Se si preferisce consultarla nella maniera alternativa, iniziare da [qui](/index.php/Guida_per_Principianti/Preparazione "Guida per Principianti/Preparazione").

Questa pagina servirà da guida nel processo di installazione di [Arch Linux](/index.php/Arch_Linux_(Italiano) "Arch Linux (Italiano)") utilizzando gli [Arch Install Scripts](https://projects.archlinux.org/arch-install-scripts.git/). Prima di procedere, si consiglia di leggere velocemente le [FAQ](/index.php/FAQ_(Italiano) "FAQ (Italiano)").

Il [wiki di Arch](/index.php/Main_Page_(Italiano) "Main Page (Italiano)"), mantenuto dalla comunità, è la risorsa primaria che deve essere consultato in caso di problemi. Sono disponibili anche dei canali [IRC Channel](/index.php/IRC_Channel "IRC Channel") (per la comunità italiana: [irc://irc.azzurra.org/archlinux](irc://irc.azzurra.org/archlinux) o [irc://irc.freenode.net/#archlinux.it](irc://irc.freenode.net/#archlinux.it), mentre per il supporto internazionale: [irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)), ed il [forum italiano](http://www.archlinux.it/forum/) o [internazionale](https://bbs.archlinux.org/), che sono eccellenti risorse, nel caso la risposta non possa essere trovata altrove. Seguendo il [metodo Arch](/index.php/The_Arch_Way_(Italiano) "The Arch Way (Italiano)"), si consiglia di digitare `man _comando_` per leggere la pagina `man` pagina di un qualsiasi comando che non si conosce.

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
*   [2 Installazione](#Installazione)
    *   [2.1 Cambiare la mappatura della tastiera](#Cambiare_la_mappatura_della_tastiera)
    *   [2.2 Stabilire una connessione di rete](#Stabilire_una_connessione_di_rete)
        *   [2.2.1 Wired](#Wired)
        *   [2.2.2 Wireless](#Wireless)
            *   [2.2.2.1 Senza wifi-menu](#Senza_wifi-menu)
        *   [2.2.3 Modem analogici, ISDN o PPPoE DSL](#Modem_analogici.2C_ISDN_o_PPPoE_DSL)
        *   [2.2.4 Reti dietro un Server Proxy](#Reti_dietro_un_Server_Proxy)
    *   [2.3 Preparare l'unità di archiviazione](#Preparare_l.27unit.C3.A0_di_archiviazione)
        *   [2.3.1 Scegliere un tipo di tabella delle partizioni](#Scegliere_un_tipo_di_tabella_delle_partizioni)
        *   [2.3.2 Strumenti di partizionamento](#Strumenti_di_partizionamento)
        *   [2.3.3 Schema di partizionamento](#Schema_di_partizionamento)
        *   [2.3.4 Considerazioni per un dualboot con Windows](#Considerazioni_per_un_dualboot_con_Windows)
        *   [2.3.5 Esempio](#Esempio)
            *   [2.3.5.1 Usando cgdisk per creare le partizioni GPT](#Usando_cgdisk_per_creare_le_partizioni_GPT)
            *   [2.3.5.2 Usare fdisk per creare le partizioni MBR](#Usare_fdisk_per_creare_le_partizioni_MBR)
        *   [2.3.6 Creare filesystem](#Creare_filesystem)
    *   [2.4 Montare le partizioni](#Montare_le_partizioni)
    *   [2.5 Selezionare un mirror](#Selezionare_un_mirror)
    *   [2.6 Installare il sistema base](#Installare_il_sistema_base)
    *   [2.7 Generare il file fstab](#Generare_il_file_fstab)
    *   [2.8 Effettuare Chroot e configurare il sistema di base](#Effettuare_Chroot_e_configurare_il_sistema_di_base)
        *   [2.8.1 Locale](#Locale)
        *   [2.8.2 Mappatura e Font per la Console](#Mappatura_e_Font_per_la_Console)
        *   [2.8.3 Time zone](#Time_zone)
        *   [2.8.4 Hardware clock](#Hardware_clock)
        *   [2.8.5 Moduli del Kernel](#Moduli_del_Kernel)
        *   [2.8.6 Hostname](#Hostname)
    *   [2.9 Configurare la rete](#Configurare_la_rete)
        *   [2.9.1 Reti Wired](#Reti_Wired)
            *   [2.9.1.1 IP Dinamico](#IP_Dinamico)
            *   [2.9.1.2 Ip Statico](#Ip_Statico)
        *   [2.9.2 Reti Wireless](#Reti_Wireless)
            *   [2.9.2.1 Aggiungere connessioni wireless](#Aggiungere_connessioni_wireless)
            *   [2.9.2.2 Connettersi automaticamente a reti conosciute](#Connettersi_automaticamente_a_reti_conosciute)
        *   [2.9.3 Modem analogici, ISDN o PPPoe DSL](#Modem_analogici.2C_ISDN_o_PPPoe_DSL_2)
    *   [2.10 Creare un ambiente iniziale ramdisk](#Creare_un_ambiente_iniziale_ramdisk)
    *   [2.11 Impostare la password di Root](#Impostare_la_password_di_Root)
    *   [2.12 Installare e configurare un bootloader](#Installare_e_configurare_un_bootloader)
        *   [2.12.1 Schede Madri BIOS](#Schede_Madri_BIOS)
            *   [2.12.1.1 Syslinux](#Syslinux)
            *   [2.12.1.2 GRUB](#GRUB)
        *   [2.12.2 Per schede madri con UEFI](#Per_schede_madri_con_UEFI)
            *   [2.12.2.1 Gummiboot](#Gummiboot)
            *   [2.12.2.2 GRUB](#GRUB_2)
    *   [2.13 Smontare le partizioni montate](#Smontare_le_partizioni_montate)
*   [3 Post-Installazione](#Post-Installazione)
    *   [3.1 Gestione Utenti](#Gestione_Utenti)
    *   [3.2 Gestione dei pacchetti](#Gestione_dei_pacchetti)
    *   [3.3 Gestione dei servizi](#Gestione_dei_servizi)
    *   [3.4 Audio](#Audio)
    *   [3.5 Graphical User Interface (interfaccia grafica utente)](#Graphical_User_Interface_.28interfaccia_grafica_utente.29)
        *   [3.5.1 Installare X](#Installare_X)
        *   [3.5.2 Installare un driver video](#Installare_un_driver_video)
        *   [3.5.3 Installare driver di input](#Installare_driver_di_input)
        *   [3.5.4 Configurare X](#Configurare_X)
        *   [3.5.5 Testare X](#Testare_X)
            *   [3.5.5.1 In caso di errori](#In_caso_di_errori)
        *   [3.5.6 Font](#Font)
        *   [3.5.7 Scegliere ed installare una interfaccia grafica](#Scegliere_ed_installare_una_interfaccia_grafica)
*   [4 Appendice](#Appendice)

## Preparazione

**Nota:** Se si desidera installare da una distribuzione GNU/Linux esistente, si legga [questo articolo](/index.php/Install_from_Existing_Linux_(Italiano) "Install from Existing Linux (Italiano)"). Ciò può essere utile soprattutto se si prevede di installare Arch Linux tramite [VNC](/index.php/VNC "VNC") o [SSH](/index.php/Secure_Shell_(Italiano) "Secure Shell (Italiano)") remoto. Gli utenti che cercano di eseguire l'installazione di Arch Linux da remoto tramite un connessione [SSH](/index.php/Secure_Shell_(Italiano) "Secure Shell (Italiano)"), dovrebbero leggere [Installare tramite SSH](/index.php/Install_from_SSH_(Italiano) "Install from SSH (Italiano)") per ulteriori suggerimenti.

### Requisiti di Sistema

Arch Linux dovrebbe funzionare su qualsiasi macchina [i686](https://en.wikipedia.org/wiki/it:P6_(microarchitecture) "wikipedia:it:P6 (microarchitecture)") compatibile e con un minimo di 64 MB di RAM. Una installazione di base con tutti i pacchetti dal gruppo _base_ dovrebbe prendere circa 500 MB di spazio su disco. Se si lavora con spazio limitato, questo può essere tagliato in modo considerevole, ma dovrete sapere cosa si sta facendo.

#### Preparare il supporto di installazione più recente

L'ultima versione del supporto di installazione può essere ottenuta dalla pagina di [download](https://www.archlinux.org/download/). Si noti che la singola immagine ISO supporta entrambe le architetture a 32 e 64 bit. É altamente raccomandato di utilizzare sempre l'ultima immagine ISO rilasciata.

*   Le immagini da installare sono firmate, e si consiglia vivamente di verificare la loro firma prima dell'uso. Scaricare il file di firma _.sig_ dalla pagina di download (o uno dei mirror elencati qui ) per la stessa directory del file _.iso_. Su Arch Linux , usare `pacman-key -v _iso-file_.sig` da root; in altri ambienti usufruire , sempre come root , di gpg2 direttamente con `gpg2 --verify _iso-file.sig_`. Sono inoltre riportate le integrità checksum del file MD5 e SHA1.

**Nota:** La verifica gpg2 fallirà se non avete scaricato la corrispondente chiave pubblica per l'ID della chiave RSA. Vedere [http://sparewotw.wordpress.com/2012/10/31/how-to-verify-signature-using-sig-file/](http://sparewotw.wordpress.com/2012/10/31/how-to-verify-signature-using-sig-file/) per i dettagli.

*   Masterizzare l'immagine ISO su un CD o DVD tramite il vostro software preferito. Su Arch questo può essere fatto seguendo [Optical_Disc_Drive_(Italiano)#Masterizzare](/index.php/Optical_Disc_Drive_(Italiano)#Masterizzare "Optical Disc Drive (Italiano)")

**Nota:** La qualità delle unità ottiche e degli stessi dischi può variare. In generale, per masterizzazioni affidabili è raccomandata una velocità bassa. Se si verifica un comportamento imprevisto del CD, provare a masterizzarne un altro usando la velocità minima.

*   In alternativa potete scrivere l'immagine ISO su un supporto USB. Si veda [Installare da supporto USB](/index.php/Installare_da_supporto_USB "Installare da supporto USB") per maggiori informazioni.

#### Installazione tramite Rete

Invece di scrivere i supporti di avvio di un'unità ottica o USB, è possibile, in alternativa, avviare un'immagine ISO in rete. Questo funziona bene quando si dispone già di un server configurato. Si prega di consultare l'articolo [PXE](/index.php/PXE "PXE") per ulteriori informazioni e quindi continuare l'avvio di [avviare il supporto di installazione di Arch Linux](#Avviare_il_supporto_di_installazione_di_Arch_Linux).

#### Installazione da un sistema Linux esistente

In alternativa, è possibile installare da un sistema Linux già in esecuzione. Vedere [Install from Existing Linux (Italiano)](/index.php/Install_from_Existing_Linux_(Italiano) "Install from Existing Linux (Italiano)").

#### Installazione su Macchina Virtuale

L'installazione su una [macchina virtuale](https://en.wikipedia.org/wiki/it:Virtual_machine "wikipedia:it:Virtual machine") è un buon modo per familiarizzare con Arch Linux e la sua procedura di installazione senza lasciare il sistema operativo corrente e ripartizionare il disco rigido. E vi permetterà anche di mantenere questa **Guida per Principianti** aperta nel vostro browser per tutta l'installazione. Alcuni utenti potrebbero trovare vantaggioso avere un autonomo sistema Arch Linux su un drive virtuale a scopo di test.

Esempi di software di virtualizzazione sono [VirtualBox](/index.php/VirtualBox_(Italiano) "VirtualBox (Italiano)"), [VMware](/index.php/VMware_(Italiano) "VMware (Italiano)"), [QEMU](/index.php/QEMU "QEMU"), [Xen](/index.php/Xen "Xen"), [Parallels](/index.php/Parallels "Parallels").

La procedura esatta per la preparazione di una macchina virtuale dipende dal software, ma generalmente attenersi alla seguente procedura:

1.  Creare l'immagine disco virtuale che ospiterà il sistema operativo.
2.  Configurare correttamente i parametri della macchina virtuale.
3.  Avviare l'Immagine ISO scaricata con un drive CD virtuale.
4.  Continuare con [Avviare il supporto di installazione di Arch Linux](#Avviare_il_supporto_di_installazione_di_Arch_Linux).

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

*   Se siete in possesso di una scheda grafica Intel e lo schermo rimane vuoto durante il processo di boot, il problema è dovuto probabilmente all'impostazione in modalità [Kernel Mode Setting](/index.php/Kernel_Mode_Setting "Kernel Mode Setting"). Una possibile soluzione è quella di riavviare e premere il tasto `e` sulla voce che si sta tentando di eseguire all'avvio ( i686 o x86_64 ). Inserire alla fine della stringa delle opzioni del kernel `nomodeset` e premere `Invio`. In alternativa aggiungere `video=SVIDEO-1:d`, che dovrebbe permettere di poter funzionare senza disattivare il kernel mode setting (KMS). Si può anche provare `i915.modeset=0`. Consultare l'articolo [Intel](/index.php/Intel_(Italiano) "Intel (Italiano)") per ulteriori informazioni.

*   Se lo schermo non si spegne ed il processo di avvio si blocca durante il tentativo di caricare il kernel, riavviare e premere `Tab` sulla voce che si sta tentando di eseguire all'avvio, ed inserire alla fine della stringa delle opzioni del kernel `acpi=off` e premere `Invio`.

## Installazione

Vi verrà visualizzato un prompt in una shell e sarete loggati automaticamente come root. Per la modifica dei file di testo si consiglia l'editor da console nano. Se non si ha familiarità con esso, vedere [Utilizzo di Nano](/index.php/Nano_(Italiano)#Utilizzo_di_nano "Nano (Italiano)")

### Cambiare la mappatura della tastiera

**Tip:** Questo passaggio è facoltativo per la maggioranza degli utenti.. Utile solo se si ha intenzione di scrivere nella propria lingua in uno dei file di configurazione, se si utilizzano segni diacritici per la password wifi, o se si desidera ricevere i messaggi di sistema (ad esempio, i possibili errori) nella propria lingua. Le modifiche qui impostate hanno effetto _solo_ per il processo di installazione.

Per impostazione predefinita, il layout della tastiera è impostato su `us`. Se non avete una tastiera americana [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg") è possibile cambiare il layout eseguendo:

```
# loadkeys _layout_

```

Dove _layout_ corrisponde al vostro tipo di tastiera, come `it`, `uk`, `dvorak`, `be-latin1`, etc. Si veda [|qui](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements "wikipedia:ISO 3166-1 alpha-2") per un elenco completo dei codici internazionali a due lettere. Utilizzare il comando `localectl list-keymaps` per una lista delle mappature disponibili.

Il tipo di carattere deve essere cambiato, perché la maggior parte delle lingue usa più glifi rispetto alle 26 lettere dell'[alfabeto inglese](https://en.wikipedia.org/wiki/English_alphabet "wikipedia:English alphabet"). In caso contrario, alcuni caratteri stranieri possono apparire come quadrati bianchi o altri simboli . Si noti che il nome è case-sensitive, quindi digitarlo _esattamente_ come lo vedete:

```
# setfont Lat2-Terminus16

```

Per impostazione predefinita, la lingua è impostata su Inglese (US). Se si desidera cambiare la lingua per il processo di installazione _(Italiano, in questo esempio)_, rimuovere il simbolo `#` davanti al [locale](/index.php/Locale "Locale") che si desidera nel file `/etc/locale.gen`, insieme con l'inglese (US). Si prega di scegliere la voce `UTF-8`.

 `# nano /etc/locale.gen` 

```
en_US.UTF-8 UTF-8
it_IT.UTF-8 UTF-8
```

```
# locale-gen
# echo "LANG=it_IT.UTF-8" > /etc/locale.conf

```

### Stabilire una connessione di rete

**Attenzione:** Dalla versione 197, udev non assegna i nomi delle interfacce di rete in base al tradizionale schema di denominazione wlanX e ethX. Se si proviene da una diversa distribuzione o si reinstalla Arch e non si è a conoscenza del nuovo metodo di denominazione delle interfacce, per favore non date per scontato che la vostra interfaccia wireless si chiama wlan0, o che l'interfaccia cablata sia denominata eth0\. È possibile utilizzare il comando `ip addr show` per scoprire i nomi delle interfacce.

Il demone `dhcpcd` della rete viene avviato automaticamente durante la fase boot e tenterà di avviare una connessione cablata, se disponibile. Provare a eseguire il ping di un sito web per vedere se ha avuto successo. E dal momento che Google è sempre attivo ...

 `# ping -c 3 www.google.com` 

```
PING www.l.google.com (74.125.132.105) 56(84) bytes of data.
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=1 ttl=50 time=17.0 ms
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=2 ttl=50 time=18.2 ms
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=3 ttl=50 time=16.6 ms
--- www.l.google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 16.660/17.320/18.254/0.678 ms
```

Se si ottiene un errore `ping: unknown host`, per prima cosa verificare se c'è qualche problema con il cavo, o se controllare la potenza del segnale wireless, altrimenti configurare la rete manualmente, come spiegato in seguito. Quando la connessione viene stabilita si continui con il paragrafo [Preparare l'unità di archiviazione](#Preparare_l.27unit.C3.A0_di_archiviazione).

#### Wired

Seguire questa procedura se si necessita di impostare una connessione cablata tramite un indirizzo IP statico.

Per prima cosa disattivare il servizio dhcpcd che è stato avviato automaticamente al boot:

```
# systemctl stop dhcpcd.service

```

Poi si identifichi il nome della propria interfaccia ethernet.

 `# ip link` 

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT 
     link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: enp2s0f0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN mode DEFAULT qlen 1000 
     link/ether 00:11:25:31:69:20 brd ff:ff:ff:ff:ff:ff
3: wlp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DORMANT qlen 1000 
     link/ether 01:02:03:04:05:06 brd ff:ff:ff:ff:ff:ff
```

In questo esempio l'interfaccia Ethernet è denominata `enp2s0f0`. Se non siete sicuri, è probabile che le proprie interfacce Ethernet iniziano con la lettera "e", è improbabile che inizino con la lettera "lo" o con la lettera "w".

È inoltre necessario conoscere le seguenti impostazioni:

*   Indirizzo IP statico
*   Subnet mask
*   Indirizzo IP del Gateway
*   Nome indirizzi IP del server (DNS)
*   Nome di dominio (se non si tratta di una LAN locale, nel qual caso si può mettere up).

Attivare la connessione all'interfaccia Ethernet (es. `enp2s0f0`):

```
# ip link set enp2s0f0 up

```

Aggiungere l'indirizzo:

```
# ip addr add _Indirizzo IP_/_mask_bits_ dev _nome_interfaccia_

```

Ad esempio:

```
# ip addr add 192.168.1.2/24 dev enp2s0f0

```

Per maggiori opzioni, eseguire `man ip`

Allo stesso modo aggiungere il vostro gateway, sostituendo <Indirizzo IP> col l'indirizzo IP del vostro gateway.:

```
# ip route add default via _Indirizzo IP_

```

Ad esempio:

```
# ip route add default via 192.168.1.1

```

Modificare il file `/etc/resolv.conf` immettendo il vostro nome di indirizzi IP del server (DNS) e il vostro nome di dominio:

 `# nano /etc/resolv.conf` 

```
 nameserver 61.23.173.5
 nameserver 61.95.849.8
 search example.com

```

**Nota:** Attualmente è possibile aggiungere al massimo tre linee per il `nameserver`. Per superare questa limitazione, è possibile utilizzare un caching per i nameserver localmente come [Dnsmasq](/index.php/Dnsmasq "Dnsmasq").

Ora si dovrebbe avere una connessione di rete funzionante . In caso contrario, controllare in dettaglio la pagina [Configurazione della Rete](/index.php/Configurazione_della_Rete "Configurazione della Rete").

#### Wireless

Seguire la seguente procedura si necessita di una connessione wireless (WiFi) durante l'installazione.

Per prima cosa bisogna identificare la propria interfaccia wireless:

 `# iw dev` 

```
phy#0
        Interface wlp3s0
                ifindex 3
                wdev 0x1
                addr 00:11:22:33:44:55
                type managed
```

In questo esempio, `wlp3s0` è l'interfaccia wireless disponibile. Se non siete sicuri, è probabile che la vostra interfaccia wireless inizi con la lettera " w", e improbabile che sia "lo" o che inizi con la lettera "e".

**Nota:** Se non vedete qualcosa di simile, allora il driver wireless non è stato caricato. Se questo è il vostro caso, allora è necessario caricare il driver. Si prega di consultare [Configurazione Wireless](/index.php/Configurazione_Wireless "Configurazione Wireless") per informazioni più dettagliate.

Accendere l'interfaccia con:

```
# ip link set wlp3s0 up

```

Per verificare che l'interfaccia è attiva , controllare l'output del seguente comando :

 `# ip link show wlp3s0` 

```
3: wlp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state DOWN mode DORMANT group default qlen 1000
    link/ether 00:11:22:33:44:55 brd ff:ff:ff:ff:ff:ff

```

La voce `UP` in `<BROADCAST,MULTICAST,UP,LOWER_UP>` indica che l'interfaccia è attiva, non confonderla con la successiva voce `state DOWN`.

Molti chipset wireless richiedono un firmware oltre al corrispondente driver. Il kernel cercherà di identificarlo e caricarlo automaticamente. Se si ottiene un output come `SIOCSIFFLAGS: No such file or directory`, questo significa che è necessario caricare manualmente il firmware. Se non si è sicuri, eseguire `dmesg` per interrogare il log del kernel per una richiesta di firmware da parte del chipset wireless. Ad esempio , se si dispone di un chipset Intel che necessita ed ha richiesto un firmware al kernel all'avvio.

 `# dmesg | grep firmware`  `firmware: requesting iwlwifi-5000-1.ucode` 

Se non vi è output, si può concludere che il chipset wireless del sistema non richiede firmware..

**Attenzione:** I pacchetti dei firmware dei chipset per il wireless (per le schede che lo necessitano) sono preinstallati in `/lib/firmware` nell'ambiente live, (su CD o supporto USB) _ma dovranno essere esplicitamente installati sul sistema definitivo per fornire funzionalità wireless all'avvio!_ La selezione e installazione dei pacchetti è spiegata in seguito. Accertarsi di aver spuntato sia il modulo sia il firmware durante la selezione dei pacchetti! Consultare [Wireless Setup](/index.php/Wireless_Setup_(Italiano) "Wireless Setup (Italiano)") se non si è sicuri riguardo l'installazione del particolare firmware per la propria scheda.

Successivamente utilizzare `wifi-menu` fornito da [netctl](/index.php/Netctl "Netctl") per connettersi ad una rete:

```
# wifi-menu wlp3s0

```

Ora si dovrebbe avere una connessione di rete funzionante. In caso contrario controllare la dettagliata pagina [Wireless Setup](/index.php/Wireless_Setup "Wireless Setup").

##### Senza wifi-menu

In alternativa utilizzare `iw dev wlp3s0 scan | grep SSID` per eseguire la scansione delle reti disponibili, e successivamente utilizzare connettersi ad una rete con:

```
# wpa_supplicant -B -i wlp3s0 -c <(wpa_passphrase "_ssid_" "_psk_")

```

È necessario sostituire l' _ESSID_ con il nome della connessione di rete (ad esempio, "Linksys ecc .."), e _"psk"_ con la propria password. **Lasciare le virgolette attorno al nome di rete e la password.**

Infine,si deve dare alla vostra interfaccia un indirizzo IP. Questo può essere impostato manualmente o mediante DHCP:

```
# dhcpcd wlp3s0

```

Se non dovesse funzionare, eseguire i seguenti comandi :

```
# echo 'ctrl_interface=DIR=/run/wpa_supplicant' > /etc/wpa_supplicant.conf
# wpa_passphrase <ssid> <passphrase> >> /etc/wpa_supplicant.conf
# ip link set <nome_interfaccia> up # Può non essere necessario, ma sempre meglio assicurarsi che sia attiva.
# wpa_supplicant -B -D nl80211 -c /foobar.conf -i <nome_interfaccia>
# dhcpcd -A <nome_interfaccia>

```

#### Modem analogici, ISDN o PPPoE DSL

Se si dispone di una connessione dial-up, o ISDN, consultare la pagina [Direct Modem Connection](/index.php/Direct_Modem_Connection "Direct Modem Connection").

#### Reti dietro un Server Proxy

Se si è dietro ad un server proxy, è necessario esportare le variabili di ambiente `http_proxy` e `ftp_proxy`. Si consulti il wiki [Proxy settings](/index.php/Proxy_settings "Proxy settings") per ulteriori informazioni.

### Preparare l'unità di archiviazione

**Attenzione:** Il partizionamento può distruggere i dati presenti. È **fortemente** consigliato fare prima una copia di sicurezza dei dati importanti prima di procedere.

**Nota:** Se si sta installando su dispositivi USB flash, consultare " [Installare Arch Linux su dispositivi USB](/index.php/Installing_Arch_Linux_on_a_USB_key_(Italiano) "Installing Arch Linux on a USB key (Italiano)")".

#### Scegliere un tipo di tabella delle partizioni

Si può scegliere tra [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table") (GPT) e [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") (MBR). GPT è più moderno e consigliato per le nuove installazioni.

*   Se si desidera configurare un sistema in dual boot con Windows, questo deve essere preso in considerazione come spiegato in [Scegliere tra GPT e MBR](/index.php/Partitioning_(Italiano)#Scegliere_tra_GPT_e_MBR "Partitioning (Italiano)").
*   Si raccomanda di usare sempre GPT per l'avvio UEFI, in quanto alcuni firmware UEFI non consentono il boot UEFI-MBR.
*   Alcuni sistemi BIOS possono avere problemi con GPT. Si veda [http://mjg59.dreamwidth.org/8035.html](http://mjg59.dreamwidth.org/8035.html) e [http://rodsbooks.com/gdisk/bios.html](http://rodsbooks.com/gdisk/bios.html) per maggiori informazioni e possibili soluzioni.

#### Strumenti di partizionamento

Coloro che non hanno dimestichezza con tool a riga di comando, e i novizi, sono incoraggiati ad utilizzare uno strumento grafico di partizionamento. [GParted](http://gparted.sourceforge.net/download.php) è un buon esempio ed è [disponibile con un CD "Live"](http://gparted.sourceforge.net/livecd.php). Inoltre è anche incluso nei CD live della maggior parte dei distributioni Linux, come [Ubuntu](https://en.wikipedia.org/wiki/Ubuntu_(operating_system) "wikipedia:Ubuntu (operating system)") e [Linux Mint](https://en.wikipedia.org/wiki/Linux_Mint "wikipedia:Linux Mint"). Un dispositivo deve prima di tutto essere [partizionato](/index.php/Partitioning_(Italiano) "Partitioning (Italiano)"), e successivamente le partizioni devono essere formattate con un [file system](/index.php/File_Systems_(Italiano) "File Systems (Italiano)").

**Suggerimento:** Quando si usa Gparted, selezionando l' opzione per creare una nuova tabella delle partizioni essa creerà per impostazione predefinita una tabella delle partizioni "msdos". Se avete intenzione di seguire il consiglio di creare una tabella di partizione GPT, allora avete bisogno di scegliere "Avanzate" (Advanced) e quindi selezionare "gpt" dal menu a discesa.

Mentre gparted può essere più facile da usare, se si vuole solo creare un paio di partizioni su un nuovo disco è possibile ottenere il partizionamento rapidamente solo utilizzando una delle [varianti a fdisk](/index.php/Partitioning_(Italiano)#Strumenti_di_partizionamento "Partitioning (Italiano)") che sono inclusi nel supporto di installazione. Nella sezione successiva ci sono le istruzioni di utilizzo , sia per [gdisk](/index.php/Partitioning_(Italiano)#Riepilogo_utilizzando_Gdisk "Partitioning (Italiano)") che per [fdisk](/index.php/Partitioning_(Italiano)#Riepilogo_utilizzando_Fdisk "Partitioning (Italiano)").

#### Schema di partizionamento

Si può decidere in quante partizioni il disco dovrebbe essere diviso, e a quale directory ogni partizione dovrebbe essere associata nel sistema. La mappatura delle partizioni di directory (spesso chiamati " punti di mount ") è lo [schema di partizionamento](/index.php/Partitioning_(Italiano)#Schema_di_partizionamento "Partitioning (Italiano)"). Il più semplice, e non è una cattiva scelta, è di fare un solo enorme partizione per `/`. Un'altra scelta popolare è quello di avere una partizione sia per `/` che per `/home`.

**Note relative al partizionamento:**

*   Se si dispone di una scheda madre UEFI è necessaria un'altra partizione per ospitare la [partizione di sistema EFI](/index.php/Unified_Extensible_Firmware_Interface_(Italiano)#Creare_una_partizione_di_sistema_UEFI_con_Linux "Unified Extensible Firmware Interface (Italiano)").
*   Se si dispone di una scheda madre BIOS (o si ha intenzione di avviare la macchina in modalità di compatibilità BIOS) e si desidera installare GRUB con partizionamento GPT, allora avete bisogno di creare una partizione extra ([BIOS Boot Partition](/index.php/GRUB2_(Italiano)#Istruzioni_specifiche_per_GPT "GRUB2 (Italiano)"))) della grandezza di 1 o 2 MiB e come tipo `EF02`. Si veda. Syslinux non ne ha bisogno.
*   Se avete deciso di utilizzare un [disco crittografato](/index.php/Disk_encryption "Disk encryption") per il sistema stesso, ciò deve riflettersi nel vostro schema di partizione. Non è un problema aggiungere cartelle crittografate, contenitori o directory home, dopo che il sistema è stato installato.
*   Se avete intenzione di utilizzare un qualsiasi filesystem di root diverso da ext4 (-3,-2), si dovrebbe verificare in primo luogo se GRUB lo supporta. Se non è supportato è necessario creare una partizione compatibile GRUB ( ad esempio [ext4](/index.php/Ext4 "Ext4")) e usarlo per la partizione di `/boot`.

Si veda [Swap](/index.php/Swap "Swap") per i dettagli, se si desidera creare una partizione di swap o un file di swap . Un file di swap è più facile da ridimensionare di una partizione e può essere creato in qualsiasi momento dopo l'installazione , ma non può essere utilizzato con un filesystem Btrfs .

#### Considerazioni per un dualboot con Windows

Se si dispone di un'installazione esistente del sistema operativo, si prega di tenere presente che, se si deve scrivere semplicemente una nuova tabella delle partizioni su disco, tutti i dati precedentemente presenti sul disco andrebbero persi.

Il metodo consigliato per impostare un sistema dual boot Linux/Windows è quello di installare prima Windows, utilizzando solo una parte del disco per le sue partizioni. Una volta terminata l'installazione di Windows, avviare l'ambiente di installazione di Linux in cui è possibile creare ulteriori partizioni per Linux, lasciando le partizioni Windows esistenti intatte.

Inoltre, alcuni computer più recenti sono pre-installati con Windows 8, che utilizzerà Secure Boot. Arch Linux attualmente non supporta il Secure Boot, ma è stato riscontrato che alcune installazioni di Windows 8 non si avviano se il Secure Boot è disattivato nel BIOS. In alcuni casi è necessario spegnere sia Secure Boot che Fastboot dalle opzioni del BIOS, in modo da consentire a Windows 8 di avviarsi senza Secure Boot. Tuttavia ci sono potenziali rischi per la sicurezza spegnendo Secure Boot per l'avvio di Windows 8\. Pertanto, può essere una scelta migliore quella di mantenere l'installazione di Windows 8 intatta e utilizzare un secondo disco rigido indipendente per l'installazione di Linux, che può poi essere ripartizionato da zero utilizzando una tabella di partizioni GPT. Una volta fatto ciò, la creazione di più partizioni ext4/FAT32/swap sul secondo disco può essere il modo migliore di proseguire se il computer dispone di due unità a disposizione. Questo non è spesso facile o possibile su un piccolo computer portatile. Attualmente, Secure Boot non è ancora in uno stato completamente stabile per il funzionamento affidabile, anche p,-er le distribuzioni Linux che lo supportano.

**Attenzione:** Windows 8 include una nuova funzionalità denominata Fast Startup, che trasforma le operazioni di spegnimento in suspend-to-disk (sospensione su disco). Il risultato è che i filesystem condivisi tra Windows 8 e qualsiasi altro OS saranno quasi certamente danneggiati durante l'avvio tra i due sistemi operativi. Anche se non avete intenzione di condividere i filesystem, la partizione di sistema EFI è probabile che sia danneggiata su un sistema EFI. Pertanto, è necessario disattivare questa modalità di avvio veloce, come descritto [qui](http://www.eightforums.com/tutorials/6320-fast-startup-turn-off-windows-8-a.html), prima di installare Linux su qualsiasi computer che utilizza Windows 8.

Se avete già effettuato questa procedura, si proceda con [Montare le partizioni](#Montare_le_partizioni).

In caso contrario, vedere il seguente esempio.

#### Esempio

L'attuale supporto di installazione di Arch Linux include i seguenti tool di partizionamento: `fdisk`, `gdisk`, `cfdisk`, `cgdisk`, `parted`.

**Suggerimento:** Utilizzare il comando `lsblk -f` o `lsblk -o NAME,FSTYPE,SIZE,LABEL` per elencare i dischi rigidi collegati al sistema, insieme con le dimensioni delle loro partizioni esistenti. Questo vi aiuterà ad essere sicuri che si sta partizionando il disco giusto.

Il sistema di esempio conterrà una partizione root da 15 GB, e una partizione [home](/index.php/Partitioning_(Italiano)#Home "Partitioning (Italiano)") per lo spazio su disco rimanente. Scegliere [MBR](/index.php/MBR "MBR") o [GPT](/index.php/GPT "GPT"). Non scegliere entrambi!

Si sottolinea ancora una volta che il partizionamento è una scelta personale e questo esempio è solo a scopo illustrativo. Si consulti la pagina sul [partizionamento](/index.php/Partitioning_(Italiano) "Partitioning (Italiano)").

##### Usando cgdisk per creare le partizioni GPT

```
# cgdisk /dev/sda

```

	Root

*   Scegliere _New_ (o premere `N`) - premere `Enter` per il primo settore (2048) - Digitare la grandezza in `15G` - premere `Enter` per il codice esadecimale di default (8300) - premere `Enter` per lasciare vuoto il nome della partizione.

	Home

*   Muoversi col tasto freccia in basso selezionando lo spazio libero
*   Scegliere `New` (o premere `N`) - premere `Enter` per il primo settore - premere `Enter` per utilizzare tutto lo spazio rimanente sul disco (oppure indicare la grandezza desiderata, per esempio `30G`) - premere `Enter` per il codice esadecimale di default (8300) - premere `Enter` per lasciare vuoto il nome della partizione.

Ecco come dovrebbe apparire:

```
Part. #     Size        Partition Type            Partition Name
----------------------------------------------------------------
            1007.0 KiB  free space
   1        15.0 GiB    Linux filesystem
   2        123.45 GiB  Linux filesystem

```

Ricontrollate tutto il lavoro e assicuratevi che le dimensioni delle partizioni, così come la tabella delle partizioni, siano quelle volute, prima di continuare.

Se volete ricominciare da capo, si può semplicemente selezionare _Quit_ (o premere `Q`) per uscire senza salvare le modifiche e quindi riavviare _cgdisk_.

Se si è soddisfatti, selezionare _Write_ (o premere `Shift+W`) per finalizzare e scrivere la tabella delle partizioni sul disco. Premere `yes` e scegliere _Quit_ ( o premere `Q`) per uscire da cfdisk, senza apportare più modifiche.

**Nota:** In fase di installazione in modelità UEFI, è consigliato l'uso di **gdisk** per la creazione della partizione di /boot con codice **ef00** e **Last sector** +512M

##### Usare fdisk per creare le partizioni MBR

**Nota:** C'è anche _cfdisk_, che è simile nell'uso a _cgdisk_. Tuttavia, ma al momento non si allinea correttamente la prima partizione in modo automatico. Per questo motivo useremo il classico strumento _fdisk_.

Eseguire _fdisk_ con:

```
# fdisk /dev/sda

```

Creare la tabella delle partizioni:

*   `Command (m for help):` tipo `o` e premere `Enter`

Creare la prima partizione:

1.  `Command (m for help):` digitare `n` e premere `Enter`
2.  Tipo di partizione: `Select (default p):` premere `Enter`
3.  `Partition number (1-4, default 1):` premere `Enter`
4.  `First sector (2048-209715199, default 2048):` premere `Enter`
5.  `Last sector, +sectors or +size{K,M,G} (2048-209715199....., default 209715199):` digitare `+15G` e premere `Enter`

Creare la seconda partizione:

1.  `Command (m for help):` digitare `n` e premere `Enter`
2.  Tipo di partizione: `Select (default p):` premere `Enter`
3.  `Partition number (1-4, default 2):` premere `Enter`
4.  `First sector (31459328-209715199, default 31459328):` premere `Enter`
5.  `Last sector, +sectors or +size{K,M,G} (31459328-209715199....., default 209715199):` premere `Enter`

Anteprima della nuova tabella delle partizioni :

*   `Command (m for help):` digitare `p` e premere `Enter`

```
Disk /dev/sda: 107.4 GB, 107374182400 bytes, 209715200 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x5698d902

   Device Boot     Start         End     Blocks   Id  System
/dev/sda1           2048    31459327   15728640   83   Linux
/dev/sda2       31459328   209715199   89127936   83   Linux

```

Scrivere le modifiche sul disco :

*   `Command (m for help):` digitare `w` e premere `Enter`

Se tutto è andato buon fine fdisk mostrerà il seguente messaggio :

```
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks. 

```

Nel caso in cui non funzioni, vuol dire che _fdisk_ ha rilevato un errore, è possibile utilizzare il comando `q` per uscire.

#### Creare filesystem

Il semplice partizionamento non è sufficiente, utilizzare l'utility `mkfs` per formattare le partizioni con un [File Systems](/index.php/File_Systems_(Italiano) "File Systems (Italiano)"). Per formattare le partizioni con filesystem `ext4`:

**Attenzione:** Controllate effettivamente che sia `/dev/sda1` che `/dev/sda2` siano le partizioni che si vogliono formattare. Il comando `lsblk` può aiutarvi in questo.

```
# mkfs.ext4 /dev/sda1
# mkfs.ext4 /dev/sda2

```

Se si è creata una partizione dedicata per swap (code 82), non si dimentichi di formattarla e attivarla con:

```
# mkswap /dev/sda_X_
# swapon /dev/sda_X_

```

Per UEFI , è necessario formattare la partizione di sistema EFI (ad esempio /dev/sd_XY_) con :

```
# mkfs.fat -F32 /dev/sd_XY_

```

### Montare le partizioni

Ogni partizione è identificata con un suffisso numerico. Ad esempio, `sda1` specifica la prima partizione del primo disco, mentre `sda` indica l'intero disco.

Per visualizzare lo schema delle partizioni correnti:

```
#  lsblk -f

```

Fate attenzione, perché l'ordine di montaggio è importante. Per prima cosa, montare la partizione di root su `/mnt`. Seguendo l'esempio precedente (il vostro potrebbe essere diverso):

```
# mount /dev/sda1 /mnt

```

In seguito montare la partizione `/home` e qualsiasi altra partizione separata (`/boot`, `/var`, etc. ), se ne avete.

```
# mkdir /mnt/home 
# mount /dev/sda2 /mnt/home

```

Nel caso si abbia una scheda madre UEFI, montare la partizione di sistema EFI sul proprio punto di montaggio preferito (nell'esempio useremo `/boot`)

```
 # mkdir /mnt/boot
 # mount /dev/sd_XY_ /mnt/boot

```

### Selezionare un mirror

Prima di procedere è necessario modificare il file `mirrorlist` e inserire il vostro mirror preferito in cima alla lista . una copia di questo file sarà pure installato sul vostro nuovo sistema da `pacstrap`, quindi conviene impostarlo come si deve.

 `# nano /etc/pacman.d/mirrorlist` 

```
##
## Arch Linux repository mirrorlist
## Sorted by mirror score from mirror status page
## Generated on 2012-MM-DD
##

Server = http://mirror.example.xyz/archlinux/$repo/os/$arch
...
```

Se si desidera, è possibile rendere il mirror copiato _l'unico_ disponibile e cancellare tutte le altre linee, ma di solito è una buona idea averne qualcuno in più, nel caso in cui il primo risulti offline.

**Suggerimento:**

*   Potete utilizzare [Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) per ottenere un elenco aggiornato per il vostro paese. I mirror HTTP sono più veloci dei FTP, a causa di qualcosa di una procedura chiamata [keepalive](https://en.wikipedia.org/wiki/Keepalive "wikipedia:Keepalive"). Con FTP, pacman deve inviare un segnale ogni volta che si scarica un pacchetto, con conseguenza che si genera una breve pausa. Per conoscere altri modi per generare un elenco dei mirror, vedere [Scelta e selezione dei mirrors](/index.php/Mirrors_(Italiano)#Scelta_e_selezione_dei_mirrors "Mirrors (Italiano)") e [Reflector](/index.php/Reflector "Reflector").
*   [Arch Linux MirrorStatus](https://archlinux.org/mirrors/status/) rapporta diversi informazioni sui mirror, come problemi di rete con un server, problemi di raccolta dei dati, l'ultima volta che un mirror è stato sincronizzato, ecc.

**Nota:** * Ogni volta che in futuro si modifica la lista di mirror (mirrorlist), ricordate di aggiornare tutti gli elenchi dei pacchetti con `pacman -Syy`, per garantire che le liste dei pacchetti vengono aggiornati costantemente. Si veda [Mirrors](/index.php/Mirrors_(Italiano) "Mirrors (Italiano)") per ulteriori informazioni.

*   Se il supporto di installazione che state utilizzando è vecchio, la vostra lista dei server mirror potrebbe essere superata, ciò potrebbe portare a problemi durante l'aggiornamento di Arch-Linux tramite pacman (Si veda il [FS#22510](https://bugs.archlinux.org/task/22510)). Pertanto si consiglia di ottenere una versione aggiornata del mirrorlist, come descritto sopra.
*   Sono stati segnalati alcuni problemi sul [forum di Arch Linux](https://bbs.archlinux.org/) per quanto concerne dei problemi di rete che impediscono a pacman di aggiornare/sincronizzare i repository (si veda [[1]](https://bbs.archlinux.org/viewtopic.php?id=68944) e [[2]](https://bbs.archlinux.org/viewtopic.php?id=65728) ). Quando si installa nativamente Arch, questi problemi sono stati risolti sostituendo il la variabile predefinita per lo scaricamento dei pacchetti di pacman con uno alternativo (si veda [migliorare le prestazioni di Pacman](/index.php/Improve_pacman_performance "Improve pacman performance") per maggiori dettagli). Quando si installa Arch come un sistema operativo Guest in [Virtualbox](/index.php/VirtualBox_(Italiano) "VirtualBox (Italiano)"), questo problema è stato risolto utilizzando "interfaccia host" invece di "NAT" nelle proprietà della macchina virtuale.

### Installare il sistema base

Il sistema base viene installato tramite l'ausilio dello script _pacstrap_. L'opzione `-i` può essere omessa se ​​si desidera installare tutti i pacchetti del gruppo [base](https://www.archlinux.org/groups/x86_64/base/) senza chiedere conferma. Si consiglia inoltre di includere [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), avrete bisogno di questi pacchetti se ci vogliono compilare da AUR .

```
 # pacstrap -i /mnt base

```

**Nota:**

*   Se pacman non riesce a verificare i pacchetti, fermare il processo premendo `CTRL+C` e controllate l'ora del vostro sistema con `cal`. Se la data di sistema non è valida (ad esempio, mostra l'anno 2010), le chiavi per la firma dei pacchetti verranno considerate scadute (o non valide), i controlli sulle firme dei pacchetti falliranno e l'installazione verrà interrotta. Assicurarsi di correggere l'ora del sistema, usare il comando `ntpd -gg`, e ripetere l'esecuzione del comando pacstrap. Fare riferimento a alla pagina [Time](/index.php/Time "Time") per ulteriori informazioni sulla correzione di ora di sistema.
*   Se pacman si lamenta che `error: failed to commit transaction (invalid or corrupted package)`, eseguire il seguente comando :

```
 # pacman-key --init && pacman-key --populate archlinux

```

Questo vi consentirà di avere un sistema base di Arch Linux. Altri pacchetti possono essere installati in seguito tramite [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)").

### Generare il file fstab

Generare un file [fstab](/index.php/Fstab_(Italiano) "Fstab (Italiano)") con il seguente comando. Saranno utilizzati gli `UUID` perché hanno alcuni vantaggi (si veda [Identificare i filesystem](/index.php/Fstab_(Italiano)#Identificare_i_filesystem "Fstab (Italiano)")). Se invece si preferisce utilizzare le etichette, sostituire l'opzione `-U` con il parametro `-L`.

```
 # genfstab -U -p /mnt >> /mnt/etc/fstab
 # nano /mnt/etc/fstab

```

**Attenzione:** Il file fstab dovrebbe sempre essere controllato dopo che è stato generato. Se si verificano errori lanciando genfstab oppure più avanti nella fase di installazione, **non** ripetere nuovamente il comando genfstab, ma modificate manualmente il file fstab.

Alcune considerazioni :

*   L'ultimo campo determina l'ordine in cui le partizioni vengono controllati all'avvio: utilizzare `1` per la partizione di root (non-`btrfs`), che verranno controllati per prima; `2` per tutte le altre partizioni che verranno controllare all'avvio; e `0` per non effettuare nessun controllo (si veda [Definizione dei campi](/index.php/Fstab_(Italiano)#Definizione_dei_campi "Fstab (Italiano)")).
*   Tutte le partizioni con filesystem [btrfs](/index.php/Btrfs "Btrfs") devono avere valore `0` in questo campo. Solitamente anche la partizione di _swap_ viene impostata con valore `0`.

### Effettuare Chroot e configurare il sistema di base

Successivamente bisogna entrare tramite [chroot](/index.php/Chroot "Chroot") nel vostro nuovo sistema installato.

```
# arch-chroot /mnt /bin/bash

```

**Nota:** Omettere `/bin/bash` per avere chroot in una shell sh.

In questa fase dell'installazione, sarà possibile configurare i file di configurazione principali del proprio sistema base di Arch Linux. Questi possono essere creati, se non esistono, o modificati, se si desidera modificare le impostazioni predefinite .

Seguire da vicino e comprendere questi passaggi è di fondamentale importanza per garantire un sistema configurato correttamente.

#### Locale

I **Locale** sono utilizzati da **glibc** ed altri programmi o librerie per generare le localizzazioni specifiche, il rendering del testo, i simboli specifici della lingua, visualizzare correttamente i valori monetari regionali, ora e formato della data, idiosincrasie alfabetiche, e le altre impostazioni internazionali specifiche.

Ci sono due file che hanno bisogno di essere modificati: `locale.gen` e `locale.conf` .

Decommentate le righe necessarie. Rimuovere il simbolo `#` davanti alle stringhe che si intende attivare. Utilizzare la codifica `UTF-8` è molto più raccomandato rispetto alla codifica `ISO-8859`:

 `# nano /etc/locale.gen` 

```
#is_IS ISO-8859-1
#it_CH.UTF-8 UTF-8
#it_CH ISO-8859-1
it_IT.UTF-8 UTF-8
#it_IT ISO-8859-1
#it_IT@euro ISO-8859-15
#iu_CA UTF-8
#iw_IL.UTF-8 UTF-8

```

**Nota:** Il file `locale.gen` è tutto commentata per impostazione predefinita.

Generate i locale(i) specificati in precedenza in `/etc/locale.gen`:

```
 # locale-gen

```

**Nota:** Questo verrà eseguito ad ogni aggiornamento di **glibc**.

Creare il file `/etc/locale.conf` sostituendo la localizzazione scelta:

```
 # echo LANG=it_IT.UTF-8 > /etc/locale.conf

```

**Nota:**

*   Le impostazioni internazionali specificate nella variabile `LANG` devono essere già state de-commentate in precedenza in `/etc/locale.gen`
*   Il file `locale.conf` non esiste per impostazione predefinita. Impostare solo la variabile `LANG` dovrebbe essere sufficiente in quanto fungerà da valore di default per tutte le altre variabili.

```
 # export LANG=it_IT.UTF-8

```

**Suggerimento:** Per impostare altri locali per le variabili `LC_*`, eseguire prima il comando `locale` per visualizzare le opzioni disponibili e aggiungerli a `locale.conf`. Non è consigliabile impostare la variabile `LC_ALL`. Vedere [Impostare il locale a livello di sistema](/index.php/Locale_(Italiano)#Impostare_il_locale_a_livello_di_sistema "Locale (Italiano)") per maggiori dettagli.

#### Mappatura e Font per la Console

Se avete impostato una mappatura della tastiera all'[inizio](#Cambiare_la_mappatura_della_tastiera) del processo di installazione, caricarlo ora, poiché l'ambiente è cambiato. Per esempio :

```
# loadkeys _it_
# setfont Lat2-Terminus16

```

Per rendere disponibili le modifiche dopo il riavvio, editare il file `/etc/vconsole.conf` (crearlo se non esiste).

 `# nano /etc/vconsole.conf` 

```
KEYMAP=it
FONT=Lat2-Terminus16
```

*   `KEYMAP` - Si prega di notare che questa impostazione è valida solo per le TTY, non per tutti i gestori di finestre grafici o per Xorg.

*   `FONT` - I font disponibili per la console sono elencati in `/usr/share/kbd/consolefonts/`. Il valore predefinito (vuoto) è sicuro. ma alcuni caratteri stranieri possono apparire come quadrati bianchi o altri simboli. Si consiglia di cambiare come `Lat2-Terminus16`. Poiché, come citato in `/usr/share/kbd/consolefonts/README.Lat2-Terminus16`, dovrebbe sostenere "circa 110 gruppi linguistici".

*   Opzione aggiuntiva `FONT_MAP` - Definisce la mappatura per la console da caricare con il programma setfont al boot. Si legga `man setfont`. Il valore predefinito (vuoto) o la sua rimozione è sicura e non crea problemi.

Si veda [Font per Console](/index.php/Fonts_(Italiano)#Font_per_console "Fonts (Italiano)") e `man vconsole.conf` per avere maggiori informazioni.

#### Time zone

I fusi orari disponibili e le regioni possono essere trovati nelle directory `/usr/share/zoneinfo/<Zone>/<SubZone>`.

Per poter visualizzare le _zone_ disponibili, controllando la directory `/usr/share/zoneinfo/` :

```
# ls /usr/share/zoneinfo/

```

Allo stesso modo potete controllare il contenuto della directory appartenente ad una _SubZone_:

```
# ls /usr/share/zoneinfo/Europe

```

Creare un collegamento simbolico a `/etc/localtime` con il file corrispondente alla vostre esigenze, `/usr/share/zoneinfo/<Zone>/<SubZone>`, usando questo comando:

```
# ln -s /usr/share/zoneinfo/<Zone>/<SubZone> /etc/localtime

```

**Esempio:**

```
# ln -s /usr/share/zoneinfo/Europe/Rome /etc/localtime

```

#### Hardware clock

Impostare la modalità orologio hardware in modo uniforme tra i sistemi operativi sulla stessa macchina. Altrimenti l'orario può essere sovrascritto e causare sfasamenti di orario.

Potete generare il file `/etc/adjtime` automaticamente utilizzando uno dei seguenti comandi:

*   **UTC** (raccomandato)

**Nota:** Utilizzare [UTC](https://en.wikipedia.org/wiki/it:Coordinated_Universal_Time "wikipedia:it:Coordinated Universal Time") per l'orologio hardware non significa che verrà utilizzato UTC nel software.

	 `# hwclock --systohc --utc` 

*   **localtime** (Altamente Sconsigliato) - utilizzato di default in Windows.

**Attenzione:** Utilizzare _localtime_ può portare a diversi e irreparabili bug. Tuttavia, non ci sono piani per l'abbandono del supporto di _localtime_.

	 `# hwclock --systohc --localtime` 

**Suggerimento:** Se avete un sistema dual-boot con Windows (o avete in previsione di averlo):

*   **Raccomandato**. Impostare sia Arch Linux che Windows in modo che utilizzino UTC. Si necessita una [correzione del registro](/index.php/Time#UTC_in_Windows "Time") di Windows. Inoltre, assicurarsi di impedire a Windows di sincronizzare l'orologio da internet, in modo che l'orologio hardware utilizzi nuovamente _localtime_.
*   **Sconsigliato**. Impostare Arch Linux su _localtime_ e disabilitare ogni servizio relativo all'impostazione dell'orologio, come [NTPd](/index.php/Network_Time_Protocol_daemon_(Italiano) "Network Time Protocol daemon (Italiano)"). Questo permetterà a Windows di prendersi cura della correzione dell'ora hardware e sarà necessario ricordarsi di avviare Windows almeno due volte l'anno (in primavera e autunno), quando [DTS](https://en.wikipedia.org/wiki/Daylight_savings_time "wikipedia:Daylight savings time") elabora l'ora legale. Quindi, per favore non chiedere sul forum perchè l'orologio è un'ora indietro o in avanti se utilizzate questo sistema e siete soliti passare molto tempo senza avviare Windows.

#### Moduli del Kernel

**Suggerimento:** Questo è solo un esempio, non è necessario impostarlo. Normalmente tutti i moduli necessari sono caricati automaticamente da udev, quindi raramente si avrà bisogno di aggiungerne qualcuno. Si aggiungano solamente i moduli di cui si conosce la mancanza

Per aggiungere i moduli del kernel da caricare durante l'avvio, creare un file `*.Conf` in `/etc/modules-load.d/`, con un nome in base al programma che li utilizza .

 `# nano /etc/modules-load.d/virtio-net.conf` 

```
# Carica il modulo 'virtio-net.ko' al boot.
virtio-net
```

Se ci sono più moduli da caricare per `*.conf`, I nomi dei moduli possono essere separati andando a capo. Un buon esempio risulta [VirtualBox Guest Additions](/index.php/VirtualBox#Arch_Linux_guests "VirtualBox").

Le righe vuote e linee il cui primo carattere è `#` o `;`, vengono ignorate.

#### Hostname

Impostare l'[hostname](https://en.wikipedia.org/wiki/it:hostname "wikipedia:it:hostname") a vostro piacimento (ad esempio "arch"):

```
# echo _myhostname_ > /etc/hostname

```

**Nota:** Non è più necessario modificare `/etc/hosts`. Il pacchetto [nss-myhostname](https://www.archlinux.org/packages/?name=nss-myhostname) provvederà alla risoluzione del nome host, ed è installato su tutti i sistemi per impostazione predefinita.

### Configurare la rete

È necessario configurare la rete ancora una volta, ma questa volta per l'ambiente appena installato. La procedura e prerequisiti sono molto simili a quella descritta [precedentemente](#Stabilire_una_connessione_di_rete), eccetto che stiamo per renderla persistente ed eseguita automaticamente all'avvio.

**Nota:**

*   Per informazioni più approfondite, consultare le pagine [Configurazione della Rete](/index.php/Configurazione_della_Rete "Configurazione della Rete") e [Wireless Setup](/index.php/Wireless_Setup "Wireless Setup").
*   Se si desidera utilizzare il vecchio schema di denominazione delle interfacce (es. eth* e wlan*), potete creare di un file vuoto in `/etc/udev/rules.d/80-net-name-slot.rules` (dalla versione 209 di systemd , questo file dovrebbe essere `/etc/udev/rules.d/80-net-setup-link.rules`) che maschera il file con lo stesso nome situato sotto `/usr/lib/udev/rules.d`.

#### Reti Wired

##### IP Dinamico

	Utilizzando dhcpcd

Se si utilizza solo un singolo collegamento di rete fissa cablata, non avete bisogno di un servizio di gestione della rete e si può semplicemente attivare il servizio `dhcpcd`.

```
 # systemctl enable dhcpcd.service

```

**Nota:** Se non dovesse funzionare: usare `# systemctl enable dhcpcd@_nome_interfaccia_.service`

	Utilizzando netctl

Copiare un profilo campione da `/etc/netctl/examples` a `/etc/netctl`:

```
 # cd /etc/netctl
 # cp examples/ethernet-dhcp rete_domestica

```

Modificare il profilo in base alle proprie esigenze (impostando `Interface` da `eth0` all'ID del proprio adattatore di rete, mostrato eseguendo `ip link`) :

```
# nano rete_domestica

```

Abilitare il profilo `rete_domestica`:

```
 # netctl enable rete_domestica

```

**Nota:** Si otterrà il messaggio "Running in chroot, ignoring request.". Questo può essere ignorato per ora.

	Utilizzando netctl-ifplugd

**Attenzione:** Non è possibile utilizzare questo metodo in combinazione con i comandi che che consentono in modo esplicito un profilo, come ad esempio `netctl enable <profilo>`.

In alternativa, è possibile utilizzare il servizio `netctl-ifplugd`, che gestisce con egregiamente le connessioni dinamiche a nuove reti:

Installare [ifplugd](https://www.archlinux.org/packages/?name=ifplugd), che è richiesto per `net-auto-wired`:

```
# pacman -S ifplugd

```

Quindi attivare per l'interfaccia che si desidera:

```
# systemctl enable netctl-ifplugd@<interfaccia>.service

```

**Suggerimento:** [Netctl](/index.php/Netctl "Netctl") fornisce anche `netctl-auto`, che può essere utilizzato per gestire profili di rete wired in congiunzione con `netctl-ifplugd`.

##### Ip Statico

	Connessione manuale al boot utilizzando netctl

Copiare un profilo di esempio da `/etc/netctl/examples` a `/etc/netctl`:

```
# cd /etc/netctl
# cp examples/ethernet-static rete_domestica.

```

Modificare il profilo in base alle proprie esigenze (impostando `Interface`, `Addr`, `Gateway` e `DNS`):

```
# nano rete_domestica

```

*   Si noti la `/24` in `Address` che è la [notazione CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation "wikipedia:Classless Inter-Domain Routing") della netmask `255.255.255.0`.

Abilitare il profilo creato sopra per avviarlo ad ogni avvio:

```
# netctl enable rete_domestica

```

	Connessione manuale al boot utilizzando systemd

Vedere [Network configuration#Manual connection at boot using systemd](/index.php/Network_configuration#Manual_connection_at_boot_using_systemd "Network configuration").

#### Reti Wireless

**Nota:** Se il proprio adattatore wireless richiede un firmware (come descritto nella sezione su [stabilire una connessione Wireless](#Wireless) e [Drivers e firmware](/index.php/Wireless_Setup_(Italiano)#Drivers_e_firmware "Wireless Setup (Italiano)")), installare il pacchetto contenente il proprio firmware. Nella maggior parte dei casi il pacchetto [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) conterrà il firmware necessario. Tuttavia per alcuni dispositivi, il firmware richiesto potrebbe essere nel proprio pacchetto. Per esempio : `# pacman -S zd1211-firmware` Vedere [Wireless Setup](/index.php/Wireless_Setup_(Italiano) "Wireless Setup (Italiano)") per ulteriori informazioni.

Installare [iw](https://www.archlinux.org/packages/?name=iw) e [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant), che saranno necessari per stabilire una connessione di rete.

```
# pacman -S iw wpa_supplicant

```

##### Aggiungere connessioni wireless

	Utilizzando wifi-menu

Installare [dialog](https://www.archlinux.org/packages/?name=dialog), che è richiesto per usare `wifi-menu`:

```
 # pacman -S dialog

```

Dopo aver terminato il resto di questa installazione e riavviato il sistema, è possibile collegarsi alla rete con `wifi-menu _nome_interfaccia_` (dove `_nome_interfaccia_` è l'interfaccia del vostro chipset wireless).

```
# wifi-menu _nome_interfaccia_

```

**Attenzione:** Questo deve essere fatto **dopo** il riavvio del sistema e quando non si è più in ambiente chroot. Il processo generato da questo comando va in conflitto con quello che viene eseguita al di fuori del chroot. In alternativa, si può solo configurare un profilo di rete manualmente utilizzando i modelli menzionati in seguito, in modo da non doversi preoccupare di usare `wifi-menu` a tutti i costi.

	Utilizzando un profilo con netctl

Copiare un profilo di rete da `/etc/netctl/examples` a `/etc/netctl`:

```
# cd /etc/netctl

```

```
# cp examples/wireless-wpa rete_wireless

```

Modificare il profilo in base alle vostre necessità (modificando `Interface`, `ESSID` e `Key`):

```
# nano rete_wireless

```

Per attivare il profilo creato sopra e avviarlo ad ogni avvio :

```
# netctl enable rete_wireless

```

##### Connettersi automaticamente a reti conosciute

**Attenzione:** Non è possibile utilizzare questo metodo in combinazione con i comandi che che consentono in modo esplicito un profilo, come ad esempio `netctl enable <profilo>`.

Installare [wpa_actiond](https://www.archlinux.org/packages/?name=wpa_actiond), il quale è richiesto da `netctl-auto`:

```
# pacman -S wpa_actiond

```

Abilitare il servizio `netctl-auto`, che si collegherà alle reti conosciute, e gestirà ordinatamente il roaming e la disconnessione:

```
# systemctl enable netctl-auto@_nome_interfaccia_.service

```

**Suggerimento:** [netctl](/index.php/Netctl "Netctl") fornisce anche il servizio `netctl-ifplugd`, che può essere usato in combinazione con `netctl-auto`.

#### Modem analogici, ISDN o PPPoe DSL

Per attivare una connessione a modem xDSL, dial-up e ISDN, consultare il wiki [Direct Modem Connection](/index.php/Direct_Modem_Connection "Direct Modem Connection").

### Creare un ambiente iniziale ramdisk

**Suggerimento:** La maggior parte degli utenti possono saltare questo passaggio e utilizzare i valori predefiniti forniti in `/etc/mkinitcpio.conf`. L'immagine initramfs (nella cartella di `/boot`) è già stato generato in base a questo file quando il pacchetto [linux](https://www.archlinux.org/packages/?name=linux) (il kernel Linux) è stato installato precedentemente con `pacstrap`.

Qui è necessario impostare i giusti [hooks](/index.php/Mkinitcpio_(Italiano)#HOOKS "Mkinitcpio (Italiano)") se root risiede su un disco USB, se si utilizza un sistema RAID, LVM, o se `/usr` è in una partizione separata.

Modificare `/etc/mkinitcpio.conf` in base alle proprie esigenze e ri-generare l'immagine initramfs con

```
# mkinitcpio -p linux

```

**Nota:** Per le installazioni di Arch VPS su QEMU (es. utilizzando `virtual-manager`), potrebbe necessitare dell'aggiunta dei moduli `virtio` in `mkinitcpio.conf` per essere in grado di avviarsi. `# nano /etc/mkinitcpio.conf`  `MODULES="virtio virtio_blk virtio_pci virtio_net"` 

### Impostare la password di Root

Potete impostare la password di root con

```
# passwd

```

### Installare e configurare un bootloader

#### Schede Madri BIOS

Per i sistemi BIOS sono disponibili diversi bootloader, vedere [Boot loaders](/index.php/Boot_loaders "Boot loaders") per una lista completa.  : syslinux e GRUB. Si scelga il bootloader secondo le vostre esigenze. Qui , diamo due delle possibilità come esempi :

*   Syslinux è (attualmente) limitato a caricare solo i file dalla partizione in cui è stato installato. Il suo file di configurazione è considerato più facile da capire. Esempi di configurazione possono essere trovati [qui](https://bbs.archlinux.org/viewtopic.php?pid=1109328#p1109328).

*   GRUB è più ricco di funzionalità e supporta scenari più complessi. Il suo file di configurazione è più simile ad un linguaggio di scripting 'sh', e modificarli manualmente può essere difficile per i principianti. Si raccomanda di generarne automaticamente uno.

##### Syslinux

Se avete optato per una tabella di partizione GUID (GPT) per il disco rigido in precedenza, è necessario installare il pacchetto [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) ora per far si che l'installazione di syslinux abbia successo.

```
# pacman -S gptfdisk

```

Installare il pacchetto [syslinux](https://www.archlinux.org/packages/?name=syslinux) e successivamente utilizzare lo script `syslinux-install_update` per _installare_ automaticamente il bootloader (`-i`), marcare la partizione come _active_ impostandola con il flag di _boot_ (`-a`), e installarlo sul codice di avvio _MBR_ (`-m`):

```
 # pacman -S syslinux 
 # syslinux-install_update -i -a -m 

```

Configurare il file `syslinux.cfg` per puntare alla giusta partizione di `/root`. Questo passaggio è fondamentale. Se dovesse puntare alla partizione sbagliata, Arch Linux non si avvierà. Cambiare `/dev/sda3` in modo che coincida con la vostra partizione root designata (se avete partizionato il disco come abbiamo fatto nell'[esempio](#Preparare_l.27unit.C3.A0_di_archiviazione), la vostra partizione di root sarà `/dev/sda1`). Fare lo stesso per la voce fallback.

 `# nano /boot/syslinux/syslinux.cfg` 

```
...
LABEL arch
        ...
        APPEND root=/dev/**sda3** rw
        ...
```

Per di ulteriori informazioni su come configurare e utilizzare Syslinux, consultare la pagina [Syslinux](/index.php/Syslinux_(Italiano) "Syslinux (Italiano)").

##### GRUB

Installare il pacchetto [grub](https://www.archlinux.org/packages/?name=grub) e quindi eseguire `grub-install` per installare il bootloader:

```
# pacman -S grub
# grub-install --target=i386-pc --recheck **/dev/sda**

```

**Nota:**

*   Cambiare `/dev/sda` in modo che rifletta il dispositivo su cui è stato installato Arch. Non aggiungere un numero alla partizione (non utilizzare `sda_X_`).
*   Per dispositivi partizionati in GPT su schede madri con BIOS, GRUB necessità di una partizione "BIOS Boot Partition". Si veda [Istruzioni specifiche per GPT](/index.php/GRUB2_(Italiano)#Istruzioni_specifiche_per_GPT "GRUB2 (Italiano)") e [Installazione nella partizione di boot BIOS con schema di partizionamento GPT](/index.php/GRUB2_(Italiano)#Installazione_nella_partizione_di_boot_BIOS_con_schema_di_partizionamento_GPT "GRUB2 (Italiano)") nella pagina di GRUB.

Mentre è possibile utilizzare un file `grub.cfg` creato manualmente, si raccomanda per i principianti di generarne uno automaticamente:

**Suggerimento:** Se volete che questo comando ricerchi automaticamente eventuali altri sistemi operativi presenti nel vostro computer, installare prima il pacchetto [os-prober](https://www.archlinux.org/packages/?name=os-prober) (`pacman -S os-prober`) prima di eseguire il comando successivo.

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

**Nota:** È possibile che risultino più voci di menu ridondanti. Si veda [Voci di menu ridondanti](/index.php/GRUB2_(Italiano)#Voci_di_menu_ridondanti "GRUB2 (Italiano)") per risolvere questo problema.

Per di ulteriori informazioni su come configurare e utilizzare GRUB, si veda la pagina [GRUB](/index.php/GRUB_(Italiano) "GRUB (Italiano)").

#### Per schede madri con UEFI

Per i sistemi UEFI, sono disponibili diverse opzioni. Una lista completa delle opzioni è disponibile alla pagina [Boot loaders](/index.php/Boot_loaders "Boot loaders"). Potreste scoprire che alcune opzioni funzionano, mentre altre no. In caso contrario, sceglierne uno secondo la vostra convenienza. Qui, diamo due delle possibilità come esempi :

*   [gummiboot](/index.php/Gummiboot "Gummiboot") è un semplice boot manager che fornisce fondamentalmente un menu dei kernel per [EFISTUB](/index.php/EFISTUB "EFISTUB") e altre applicazioni UEFI. Questo è il metodo di avvio UEFI consigliato.
*   GRUB è un bootloader più completo, utile se si hanno problemi ad eseguire Gummiboot.

**Nota:** Per un avvio da UEFI, il disco deve essere partizionato in GPT, e una "[partizione di sistema EFI](/index.php/Unified_Extensible_Firmware_Interface_(Italiano)#Creare_una_partizione_di_sistema_UEFI_con_Linux "Unified Extensible Firmware Interface (Italiano)")" (512 MiB o superiore, di tipo `EF00`, formattata in FAT32") deve essere presente. Per gli esempi seguenti, questa partizione deve essere montata su `/boot`. Se avete seguito questa guida dall'inizio, avete già effettuato questo passaggio.

##### Gummiboot

Recentemente systemd, ha integrato al proprio interno gummiboot, per cui non è più necessario installare alcun pacchetto

```
# mount -t efivarfs efivarfs /sys/firmware/efi/efivars              # ignorare se già montato
# bootctl --path=/boot/$esp install

```

Sarà necessario creare manualmente un file di configurazione per aggiungere una voce per Arch Linux per il manager gummiboot. Creare `/boot/loader/entries/arch.conf` e aggiungere i seguenti contenuti, sostituendo `/dev/sdaX` con la vostra partizione di root, di solito `/dev/sda2`:

 `# nano /boot/loader/entries/arch.conf` 

```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=**/dev/sdaX** rw
```

Per ulteriori informazioni su come configurare ed utilizzare gummiboot, consultare [Gummiboot](/index.php/Gummiboot "Gummiboot").

##### GRUB

Installare i pacchetti [grub](https://www.archlinux.org/packages/?name=grub) e [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr), ed eseguire `grub-install` per installare il bootloader :

```
# mount -t efivarfs efivarfs /sys/firmware/efi/efivars              # ignora se già montato
# pacman -S grub efibootmgr
# grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=arch_grub --recheck

```

Poi, creare manualmente un file `grub.cfg` è assolutamente indicato, si raccomanda che i principianti ne generino automaticamente uno:

{{Suggerimento|Per la ricerca automatica di altri sistemi operativi sul computer, installare [os-prober](https://www.archlinux.org/packages/?name=os-prober), tuttavia os-prober è noto per non riuscire a rilevare correttamente tutti i sistemi operativi in ambiente UEFI.

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

Per ulteriori informazioni sulla configurazione e l'utilizzo di GRUB, vedere [GRUB](/index.php/GRUB_(Italiano) "GRUB (Italiano)").

### Smontare le partizioni montate

Uscire dall'ambiente chroot:

```
# exit

```

Precedentemente, come esempio, si sono montate le partizioni sotto `/mnt`. In questa fase procedere a smontarle tutte.

```
# umount -R /mnt

```

Riavviare il computer:

```
# reboot

```

**Suggerimento:** Assicurarsi di rimuovere il supporto di installazione altrimenti si rischia di avviare nuovamente il supporto di installazione.

## Post-Installazione

Il nuovo sistema di base Arch Linux è ora un funzionale sistema operativo GNU/Linux pronto per essere personalizzato con quello che si desidera o in base ai vostri scopi. Se siete nuovi a Linux , potrebbe essere utile dare uno sguardo alle [principali utility](/index.php/Core_utilities "Core utilities") in dotazione con il nuovo sistema.

### Gestione Utenti

Aggiungere gli account utente che si desiderano, oltre a root, come descritto in [Gestione degli utenti](/index.php/Users_and_Groups_(Italiano)#Gestione_degli_utenti "Users and Groups (Italiano)"). Non è consigliabile utilizzare l'account di root per un uso regolare, o esporlo tramite [SSH](/index.php/Secure_Shell_(Italiano) "Secure Shell (Italiano)") su un server. L'account di root deve essere utilizzato solo per le attività amministrative.

In un tipico sistema desktop per aggiungere un nuovo utente denominato _archie_ specificando [bash](/index.php/Bash_(Italiano) "Bash (Italiano)") come shell di login

```
# useradd -m -s /bin/bash archie

```

Questo comando creerà automaticamente un gruppo denominato `archie` con lo stesso GID pari all' UID dell'utente `archie` e ne fa di questo il gruppo predefinito dell'utente `archie` al login.

Altri scenari sono possibili, si veda [Utenti e gruppi](/index.php/Users_and_Groups_(Italiano) "Users and Groups (Italiano)") per maggiori dettagli e potenziali rischi per la sicurezza.

### Gestione dei pacchetti

Pacman è il **pac**kage **man**ager di Arch Linux. Si faccia riferimento alla pagina di [Pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)") e alle relative [FAQ](/index.php/FAQ_(Italiano)#Gestione_Pacchetti "FAQ (Italiano)") per le risposte inerenti l'aggiornamento, l'installazione e la gestione dei pacchetti.

Poichè il metodo Arch prevede la [correttezza del codice oltre la convenienza](/index.php/The_Arch_Way_(Italiano)#Correttezza_del_codice_oltre_la_convenienza "The Arch Way (Italiano)"), **prima** di effettuare un aggiornamento del sistema è **indispensabile** mantenersi aggiornati con i cambiamenti in Arch Linux che richiedono un intervento manuale. Questo può essere fatto iscrivendovi alla [arch-announce mailing list](https://mailman.archlinux.org/mailman/listinfo/arch-announce/) o controllando la pagina [Arch news](https://www.archlinux.org/). In alternativa, può essere utile iscriversi a [questo feed RSS](https://www.archlinux.org/feeds/news/) o seguire [@archlinux](https://twitter.com/archlinux) su Twitter.

Se si è installato Arch Linux x86_64, si consiglia di [abilitare il deposito [multilib]](/index.php/Multilib "Multilib") , se si pensa di utilizzare le applicazioni a 32 bit .

Si veda [Repositories Ufficiali](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)") per dettagli maggiori su ogni deposito.

### Gestione dei servizi

Arch Linux utilizza [systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)") come metodo di init, che oltre al sistema di init è il responsabile della gestione dei servizi per Linux. Per il mantenimento della vostra installazione di Arch Linux, è caldamente consigliato imparare le basi su del suo funzionamento. L'interazione con systemd è garantita tramite il comando `systemctl`. Si legga il paragrafo [Uso base di systemctl](/index.php/Systemd_(Italiano)#Uso_base_di_systemctl "Systemd (Italiano)") per ulteriori informazioni.

### Audio

[ALSA](/index.php/Advanced_Linux_Sound_Architecture_(Italiano) "Advanced Linux Sound Architecture (Italiano)") di solito funziona tranquillamente, ha solo bisogno di essere riattivato. Installare [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) (il quale fornisce `alsamixer`) e seguire [queste](/index.php/Advanced_Linux_Sound_Architecture_(Italiano)#Togliere_il_muto_ai_canali "Advanced Linux Sound Architecture (Italiano)") istruzioni.

ALSA è incluso con il kernel e si consiglia di provarlo per primo. Tuttavia, se non funziona, [OSS](/index.php/OSS_(Italiano) "OSS (Italiano)") è una valida alternativa. Se si dispone di avanzati requisiti di audio, si dia un'occhiata alla pagina [Audio](/index.php/Sound_system_(Italiano) "Sound system (Italiano)") per una panoramica dei diversi articoli.

### Graphical User Interface (interfaccia grafica utente)

#### Installare X

L'[X Window System](https://en.wikipedia.org/wiki/it:X_Window_System "wikipedia:it:X Window System") (comunemente chiamato **X11**, o semplicemente **X**) consente di disegnare su schermo le finestre. Fornisce il toolkit standard per visualizzare interfacce utente grafiche (Graphical User Interface, GUI).

Per installare i pacchetti base di [Xorg](/index.php/Xorg "Xorg"):

```
# pacman -S xorg-server xorg-server-utils xorg-xinit

```

Installare [mesa](https://en.wikipedia.org/wiki/it:Mesa_(computer_graphics) "wikipedia:it:Mesa (computer graphics)") per il supporto 3D:

```
# pacman -S mesa

```

#### Installare un driver video

**Nota:** Se si sta installando Arch Linux come _guest_ su _virtualbox_, non è necessario installare un driver video. Consultare la pagina [Arch Linux guests](/index.php/VirtualBox#Arch_Linux_guests "VirtualBox") per installare ed impostare le Guest Additions, e saltare alla parte [Impostare il layout della tastiera](#Configurare_X) descritto di seguito.

Il kernel Linux include driver video open-source e il supporto per il framebuffer hardware accelerato. Tuttavia, il supporto in spazio utente è necessario per OpenGL e l'accelerazione 2D in X11 .

Se non si conosce la scheda grafica disponibile sul vostro computer, è possibile eseguire:

```
$ lspci | grep VGA

```

Per una lista completa di driver video open-source, cercare nel database dei pacchetti:

```
$ pacman -Ss xf86-video | less

```

Il driver `vesa` è un generico mode-setting driver che funziona con quasi tutte le GPU, ma non fornisce alcuna accelerazione 2D o 3D. Se un driver migliore non può essere trovato o non viene caricato, Xorg ripiegherà a vesa . Per installarlo:

```
# pacman -S xf86-video-vesa

```

Al fine di poter usufruire dell'accelerazione video per lavorare, e spesso per poter usufruire di tutte le modalità che la GPU può impostare, è necessario un driver video corretto. Si veda [Xorg_(Italiano)#Installazione_dei_Driver](/index.php/Xorg_(Italiano)#Installazione_dei_Driver "Xorg (Italiano)") per una tabella dei driver video più frequentemente utilizzati.

#### Installare driver di input

Udev dovrebbe essere in grado di rilevare l'hardware senza problemi. Il driver `evdev` ([xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev)) è il moderno driver di input hot-plugging per quasi tutti i dispositivi, quindi, nella maggior parte dei casi, l'installazione di driver di input specifici non è più necessaria. A questo punto `evdev` è già astato installato come dipendenza del pacchetto [xorg-server](https://www.archlinux.org/packages/?name=xorg-server).

Gli utenti notebook (o utilizzatori di un touchscreen) avranno inoltre bisogno del pacchetto [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) per permettere ad X di configurare il touchpad/touchscreen:

```
# pacman -S xf86-input-synaptics

```

Per maggiori informazioni su particolari configurazioni o riguardo alla risoluzione di problemi nella configurazione del touchpad, consultare il wiki [Touchpad Synaptics](/index.php/Touchpad_Synaptics_(Italiano) "Touchpad Synaptics (Italiano)").

#### Configurare X

**Attenzione:** I driver proprietari di solito richiedono un riavvio dopo la loro installazione. Si veda [NVIDIA](/index.php/NVIDIA_(Italiano) "NVIDIA (Italiano)") o [ATI Catalyst](/index.php/ATI_Catalyst_(Italiano) "ATI Catalyst (Italiano)") per i dettagli.

Xorg contempla l'auto-configurazione. Pertanto, in molti casi, potrebbe tranquillamente funzionare senza l'ausilio di un file `xorg.conf`. Se si desidera configurare il Server X, consultare la documentazione di [Xorg](/index.php/Xorg_(Italiano) "Xorg (Italiano)").

Potrebbe essere necessario impostare un Qui è possibile impostare un [[[layout per la tastiera](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg") se non si utilizza una tastiera standard [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg").

**Nota:** Il valore da inserire in `XkbLayout` può differire dal codice keymap solitamente usato dai comandi `loadkeys`. Un elenco dei layout di tastiera e le loro varianti possono essere trovati in `/usr/share/X11/xkb/rules/base.lst` (si veda il testo subito dopo la linea `! layout`). Ad esempio il valore: `gb` corrisponde a English (UK), mentre per la console era `loadkeys uk`.

#### Testare X

**Suggerimento:** Questi passaggi sono opzionali . Utile solo se si sta installando Arch Linux per la prima volta o per l'hardware più recente.

**Nota:** Se i dispositivi di input non funzionano durante il test, installare il driver necessario dal gruppo [xorg-drivers](https://www.archlinux.org/groups/x86_64/xorg-drivers/), e riprovare. Per un elenco completo di driver di input disponibili, richiamare una ricerca con pacman (premere `Q` per uscire ):

```
$ pacman -Ss xf86-input | less

```

Se avete intenzione di disattivare l'[hot-plugging](https://en.wikipedia.org/wiki/Hot-plugging "wikipedia:Hot-plugging"), avete bisogno solamente dei pacchetti [xf86-input-keyboard](https://www.archlinux.org/packages/?name=xf86-input-keyboard) o [xf86-input-mouse](https://www.archlinux.org/packages/?name=xf86-input-mouse), altrimenti `evdev` agirà come driver di ingresso principale (consigliato).

Installare un Ambiente di test predefinito.

```
# pacman -S xorg-twm xorg-xclock xterm

```

Se Xorg è stato installato prima della creazione del proprio utente non-root e si avrà un modello di file `.Xinitrc` vuoto nella propria $HOME che è necessario eliminare o commentare in modo da avviare un ambiente desktop. Semplicemente eliminandolo **X** avvierà l'esecuzione di un ambiente predefinito installato.

```
$ rm ~/.xinitrc

```

**Nota:** X deve sempre essere eseguito sulla stessa tty in cui si è effettuato il login, per preservare la sessione logind. Questo è gestito dal file predefinito `/etc/X11/xinit/xserverrc`.

Per avviare una sessione (di test) di Xorg, eseguire:

```
$ startx 

```

Alcune finestre mobili dovrebbe apparire, e il vostro mouse dovrebbe funzionare correttamente. Una volta verificato che l'installazione **X** è stato un successo, si può uscire da **X** con il comando `exit` al prompt e si ritornerà alla console.

```
$ exit

```

Se lo schermo dovesse diventare nero, si può provare a spostarsi su un'altra console virtuale (`CTRL-Alt-F2` ad esempio), ed effettuare un login "cieco" come root, premendo poi `Enter`, ed immettendo la password di root confermata di nuovo con `Enter`.

Si può anche provare a terminare la sessione **X** con `/usr/bin/pkill` (si noti che è una X maiuscola):

```
# pkill X

```

Se pkill non funziona, riavviare alla cieca con:

```
# reboot

```

##### In caso di errori

Se si verificano problemi, cercare gli errori in `Xorg.0.log`. Al suo interno si ricerchino le linee che iniziano con `(EE)` che rappresentano gli errori, ed anche `(WW)` che sono avvertimenti che potrebbero indicare altri problemi.

```
$ grep EE /var/log/Xorg.0.log

```

Se dopo aver consultato l'articolo inerente la configurazione di [Xorg](/index.php/Xorg_(Italiano) "Xorg (Italiano)") si hanno ancora dei problemi e si necessita di richiedere assistenza sul forum di Arch o sul canale IRC, ci si assicuri di installare e utilizzare [wgetpaste](https://www.archlinux.org/packages/?name=wgetpaste), postando anche i collegamenti dei seguenti file:

```
# pacman -S wgetpaste
$ wgetpaste ~/.xinitrc
$ wgetpaste /etc/X11/xorg.conf
$ wgetpaste /var/log/Xorg.0.log

```

**Nota:** È estremamente importante fornire più dettagli possibili (hardware, informazioni sui driver, etc) quando si chiede assistenza.

#### Font

Si potrebbe desiderare di installare un set di caratteri TrueType, in quanto solo font bitmap non scalabili sono inclusi di default. Tuttavia, se si utilizza un [Ambiente Desktop](/index.php/Desktop_Environment_(Italiano) "Desktop Environment (Italiano)") completo come [KDE](/index.php/KDE_(Italiano) "KDE (Italiano)"), questo passaggio potrebbe non essere necessario. Dejavu è un font di uso generico di alta qualità e con una buona copertura [Unicode](https://en.wikipedia.org/wiki/it:Unicode "wikipedia:it:Unicode") :

```
# pacman -S ttf-dejavu

```

Fare riferimento a [Font Configuration](/index.php/Font_Configuration_(Italiano) "Font Configuration (Italiano)") per sapere come configurare il rendering dei font e a [Fonts](/index.php/Fonts_(Italiano) "Fonts (Italiano)") per i suggerimenti sui tipi di caratteri e le istruzioni di installazione.

#### Scegliere ed installare una interfaccia grafica

Mentre il sistema **X** Window fornisce il quadro di base per la costruzione di una _Graphicals User Interface_ (GUI).

**Nota:** La scelta di un DE o WM è una decisione molto soggettiva e personale. Si scelga l'ambiente migliore in base alle _proprie_ esigenze. É possibile costruire il proprio ambiente desktop (DE) utilizzando un Window Manager (WM) e le applicazioni di propria scelta.

*   Un [Window Manager](/index.php/Window_Manager_(Italiano) "Window Manager (Italiano)") (Gestore delle finestre) controlla il posizionamento e l'aspetto delle finestre dell'applicazione in combinazione con il sistema X Window.

*   Un [Desktop Environment](/index.php/Desktop_Environment_(Italiano) "Desktop Environment (Italiano)") (Ambiente desktop), lavora in cima e in collaborazione con **X**, per fornire una completa interfaccia grafica funzionale e dinamica. Un ambiente desktop contiene in genere un gestore di finestre, icone, applets, finestre, barre degli strumenti, cartelle, wallpapers, una suite di applicazioni e capacità come il drag and drop.

Al posto di lanciare X manualmente tramite `startx` da [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit), si veda [Display Manager](/index.php/Display_Manager_(Italiano) "Display Manager (Italiano)") per le istruzioni su come utilizzare un gestore grafico delle sessioni, oppure si veda [Far partire X al boot](/index.php/Far_partire_X_al_boot "Far partire X al boot") per l'utilizzo di un terminale virtuale esistente come equivalente ad un display manager ..

## Appendice

Per un elenco dei programmi maggiormente utilizzati e si veda l'articolo [Lista delle Applicazioni](/index.php/List_of_Applications_(Italiano) "List of Applications (Italiano)").

Si veda anche [Raccomandazioni Generali](/index.php/Raccomandazioni_Generali "Raccomandazioni Generali") per consigli post-installazione, come la configurazione del touchpad o il rendering dei font.