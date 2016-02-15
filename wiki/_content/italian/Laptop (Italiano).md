Questa pagina dovrebbe contenere collegamenti alle altre pagine necessarie per configurare un laptop per la miglior esperienza d'uso. Configurare un laptop è molto simile per vari aspetti a configurare un desktop pc. Comunque, ci sono alcune differenze chiave. Arch Linux fornisce tutti gli strumenti e i programmi necessari per controllare ogni aspetto del proprio laptop. Questi programmi e utilità sono evidenziato qui sotto, con adeguati esempi.

## Contents

*   [1 Gestione energetica](#Gestione_energetica)
    *   [1.1 Stato della batteria](#Stato_della_batteria)
        *   [1.1.1 ACPI](#ACPI)
        *   [1.1.2 Eventi udev](#Eventi_udev)
    *   [1.2 Sospensione e ibernazione](#Sospensione_e_ibernazione)
        *   [1.2.1 Problema dello spin down dell'hard disk](#Problema_dello_spin_down_dell.27hard_disk)
*   [2 Luminosità dello schermo](#Luminosit.C3.A0_dello_schermo)
*   [3 Touchpad](#Touchpad)
*   [4 Protezione dell' HD dagli urti](#Protezione_dell.27_HD_dagli_urti)
*   [5 Sincronizzare l'orologio attraverso la rete](#Sincronizzare_l.27orologio_attraverso_la_rete)
*   [6 Vedi anche](#Vedi_anche)

## Gestione energetica

**Nota:** Si dovrebbe fare riferimento agli articoli principali [Power management](/index.php/Power_management "Power management") e [Power saving](/index.php/Power_saving "Power saving"). Ulteriori caratteristiche laptop-centriche sono descritte qua sotto.

La gestione energetica è fondamentale per chiunque desideri fare buon uso della capacità della propria batteria. I seguenti strumenti e programmi aiutano ad aumentare la durata della batteria e a mantenere il proprio portatile freddo e silenzioso.

### Stato della batteria

Si può leggere lo stato della batteria in svariati modi. Il classico metodo prevede un demone che periodicamente interroga il livello della batteria tramite l'interfaccia ACPI. In alcuni sistemi, la batteria invia eventi a [udev](/index.php/Udev "Udev") ogni volta che si (s)carica dell' 1%; questo evento può essere connesso a qualche azione, usando una regola udev.

#### ACPI

Lo stato della batteria può essere letto usando l'utility ACPI da terminale. Il comando ACPI viene installato col pacchetto [acpi](https://www.archlinux.org/packages/?name=acpi) . Leggi [ACPI modules](/index.php/ACPI_modules "ACPI modules") per ulteriori informazioni.

*   [batterymon-clone](https://aur.archlinux.org/packages/batterymon-clone/) è un semplice monitor della batteria che sta nella tray.
*   [batti](https://aur.archlinux.org/packages/batti/) è un semplice monitor della batteria per la system tray, simile a batterymon-clone. Diversamente dal precedente `batti` usa UPower, e se non è installato, `DeviceKit.Power`, per le sue informazioni sulla batteria.

#### Eventi udev

Se la tua batteria invia eventi a [udev](/index.php/Udev "Udev") ogni volta che si (s)carica dell' 1%, si può usare una regola udev come questa, per sospendere automaticamente il sistema quando la batteria è a un livello critico, e dunque prevenire la perdita di dati non salvati.

 `/etc/udev/rules.d/lowbat.rules` 

```
# Suspend the system when battery level drops to 2%
SUBSYSTEM=="power_supply", ATTR{status}=="Discharging", ATTR{capacity}=="2", RUN+="/usr/bin/systemctl suspend"

```

Allo stesso modo, la regola può essere modificata per eseguire altre azioni in stati differenti.

### Sospensione e ibernazione

Sospendere manualmente, sia in memoria (standby) che su disco (ibernazione) talvolta è un metodo efficiente per ottimizzare la durata della batteria, dipendente però dal metodo di utilizzo del portatile.

Leggi l'articolo principale [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate").

#### Problema dello spin down dell'hard disk

Documentato [qui](https://bugs.launchpad.net/ubuntu/+source/acpi-support/+bug/59695).

Per prevenire che l'hard disk del laptop si "parcheggi" troppo spesso:

 `/etc/udev/rules.d/75-hdparm.rules` 

```
ACTION=="add", KERNEL=="sd[a-z]", ATTR{queue/rotational}=="1", RUN+="/usr/bin/hdparm -B 254 /dev/$kernel"

```

Leggi `hdparm(8)` per la documentazione riguardante i parametri di [hdparm](/index.php/Hdparm "Hdparm") . Se usi [pm-utils](/index.php/Pm-utils "Pm-utils"), potrebbero interessarti [questi](/index.php/Pm-utils#Having_the_HD_power_management_level_automatically_set_again_on_resume "Pm-utils") esempi.

## Luminosità dello schermo

Leggi [Backlight](/index.php/Backlight "Backlight").

## Touchpad

Per avere il proprio touchpad funzionante a dovere, leggere la pagina [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") . Nota che il laptop potrebbe avere un touchpad ALPS(come ad esempio il DELL Inspiron 6000), e non uno Synaptics. In entrambi i casi, vedere il link sopra.

## Protezione dell' HD dagli urti

Ci sono molto portattili, prodotti da diversi fornitori, caratterizzati dalla funzionalità di protezione dagli urti. Siccome i produttori si sono rifiutati di supportare lo sviluppo open source del software richiesto, fino ad oggi, il supporto di Linux per la protezione dagli urti varia considerevolmente a seconda delle differenti implementazioni hardware.

Al momento, due progetti, [HDAPS](/index.php/Hard_Drive_Active_Protection_System "Hard Drive Active Protection System") e [hpfall](https://aur.archlinux.org/packages/hpfall/) (disponibile in [AUR](/index.php/AUR "AUR")), supportano questo tipo di protezione. HDAPS è per IBM/Lenovo Thinkpads e hpfall per i portatili HP/Compaq.

## Sincronizzare l'orologio attraverso la rete

Per un computer portatile, può essere una buona idea utilizzare [Chrony](/index.php/Chrony "Chrony") come alternativa al [NTPd](/index.php/Network_Time_Protocol_daemon_(Italiano) "Network Time Protocol daemon (Italiano)") per sincronizzare l'orologio attraverso la rete. Chrony è progettato per funzionare bene anche su sistemi senza connessione di rete permanente (come i computer portatili), ed è capace di sincronizzazione l'orologio molto più veloce rispetto allo standard ntp. Chrony ha diversi vantaggi se utilizzato in sistemi in esecuzione su macchine virtuali, come ad esempio una gamma più ampia per la correzione di frequenza per aiutare a correggere gli orologi che vanno rapidamente fuori sincronia, e una migliore risposta ai rapidi cambiamenti nella frequenza di clock. Ha anche una minor richiesta di memoria e non risveglia processi inutili, migliorando l'efficienza energetica.

## Vedi anche

	Generale

*   [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") è una tecnologia usata per lo più dai notebooks che permette al sistema operativo di scalare la frequenza della CPU in base al carico di sistema e/o allo schema energetico.
*   [Display Power Management Signaling](/index.php/Display_Power_Management_Signaling "Display Power Management Signaling") descrive come spegnere automaticamente lo schermo del portatile dopo uno specifico intervallo di inattività (non oscurato con uno screensaver, ma proprio spento del tutto).
*   [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") offre informazioni riguardo alla configurazione del wireless.
*   [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys") descrive la configurazione dei pulsanti Media.

	Pagine specifiche a certi tipi di laptop

*   Fare riferimento a [Category:Laptops](/index.php/Category:Laptops "Category:Laptops") e alle sue sottocategorie per pagine dedicate a specifici modelli/produttori.
*   [Lapsus](/index.php/ASUS_G1#The_Lapsus_daemon_.26_KDE_applet "ASUS G1") è un insieme di programmi che forniscono un facile accesso a svariate caratteristiche di vari laptop. Al momento supporta la maggior parte delle caratteristiche fornite dal modulo del kernel asus-laptop, dal progetto ACPI4Asus, come i led addizionali, scorciatoie da tastiera, controllo della retroilluminazione ecc. Supporta anche alcune caratteristiche dei portatili IBM fornite da IBM ThinkPad ACPI Extras Driver e i dispositivi NVRAM.
*   Tweaks della batteria per i portatili ThinkPads si possono trovare negli articoli [TLP](/index.php/TLP "TLP") e [tp_smapi](/index.php/Tp_smapi "Tp smapi") .
*   [acerhdf](/index.php/Acer_Aspire_One#acerhdf "Acer Aspire One") è un modulo del kernel per controllare la velocità delle ventole sull' Acer Aspire One e su alcuni portatili Packard Bell.

	Risorse esterne

*   [http://www.linux-on-laptops.com/](http://www.linux-on-laptops.com/)
*   [http://www.linlap.com/](http://www.linlap.com/)