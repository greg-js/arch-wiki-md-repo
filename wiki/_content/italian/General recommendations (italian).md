Articoli correlati

*   [FAQ (Italiano)](/index.php/FAQ_(Italiano) "FAQ (Italiano)")
*   [Beginners' Guide (Italiano)](/index.php/Beginners%27_Guide_(Italiano) "Beginners' Guide (Italiano)")
*   [List of Applications (Italiano)](/index.php/List_of_Applications_(Italiano) "List of Applications (Italiano)")

Questa pagina è un indice ragionato di altri articoli e di informazioni rilevanti. Diverse pagine qui elencate richiedono l'utilizzo di [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)") per installare pacchetti addizionali presenti nei [repositori ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)"), e di altri non ufficiali da [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") per mezzo di [makepkg](/index.php/Makepkg "Makepkg") con l'aiuto opzionale di un [AUR helper](/index.php/AUR_helper "AUR helper"). Quindi il concetto di gestione dei pacchetti deve essere perfettamente compreso prima di continuare.

Si assume che i lettori abbiano letto e seguito la [Guida per Principianti](/index.php/Guida_per_Principianti "Guida per Principianti") oppure la [Guida Ufficiale all'Installazione](/index.php/Guida_Ufficiale_all%27Installazione "Guida Ufficiale all'Installazione") per installare un sistema Arch Linux base. Inoltre ci sono diversi altri pacchetti software normalmente considerati fondamentali per un sistema completo e funzionale. Ad esempio, qualora si desideri un interfaccia grafica, si legga prima la pagina dedicata a [Xorg](/index.php/Xorg_(Italiano) "Xorg (Italiano)"), mentre chi fosse interessato alla possibilità di stampare consideri di leggere anche la pagina su [Cups](/index.php/CUPS_(Italiano) "CUPS (Italiano)"). Tutti gli utenti possono familiarizzare con la struttura del file system leggendo [Filesystem Hierarchy Standard](/index.php/Filesystem_Hierarchy_Standard_(Italiano) "Filesystem Hierarchy Standard (Italiano)").

## Contents

*   [1 Aspetto](#Aspetto)
    *   [1.1 Output a colori](#Output_a_colori)
        *   [1.1.1 Console prompt](#Console_prompt)
        *   [1.1.2 Programmi di base](#Programmi_di_base)
        *   [1.1.3 Emacs shell](#Emacs_shell)
        *   [1.1.4 Pagine di man](#Pagine_di_man)
    *   [1.2 Caratteri](#Caratteri)
        *   [1.2.1 Caratteri per la console](#Caratteri_per_la_console)
        *   [1.2.2 Patch per la visualizzazione dei font](#Patch_per_la_visualizzazione_dei_font)
*   [2 Audio/video](#Audio/video)
    *   [2.1 Browser plugin](#Browser_plugin)
    *   [2.2 Codec](#Codec)
*   [3 Fase di *boot*](#Fase_di_boot)
    *   [3.1 Avviare i *daemon* in background](#Avviare_i_daemon_in_background)
    *   [3.2 Riconoscimento automatico dell'hardware](#Riconoscimento_automatico_dell'hardware)
    *   [3.3 Attivare *Num Lock* all'avvio](#Attivare_Num_Lock_all'avvio)
    *   [3.4 Mantenere i messaggi di boot](#Mantenere_i_messaggi_di_boot)
    *   [3.5 Lanciare X all'avvio](#Lanciare_X_all'avvio)
*   [4 Migliorie per la console](#Migliorie_per_la_console)
    *   [4.1 Alias](#Alias)
    *   [4.2 Complementi per Bash](#Complementi_per_Bash)
    *   [4.3 File compressi](#File_compressi)
    *   [4.4 Supporto per il mouse](#Supporto_per_il_mouse)
    *   [4.5 Scrollback buffer](#Scrollback_buffer)
    *   [4.6 Gestione delle sessioni](#Gestione_delle_sessioni)
*   [5 Input](#Input)
    *   [5.1 Configurare tutti i pulsanti del mouse](#Configurare_tutti_i_pulsanti_del_mouse)
    *   [5.2 Mappatura della tastiera](#Mappatura_della_tastiera)
    *   [5.3 Touchpad nei laptop](#Touchpad_nei_laptop)
*   [6 Networking](#Networking)
    *   [6.1 Sincronizzazione dell'orologio](#Sincronizzazione_dell'orologio)
    *   [6.2 Disabilitare IPv6](#Disabilitare_IPv6)
    *   [6.3 Aumentare la velocità dei DNS](#Aumentare_la_velocità_dei_DNS)
    *   [6.4 Convalida DNSSEC](#Convalida_DNSSEC)
*   [7 Ottimizzazione](#Ottimizzazione)
    *   [7.1 Benchmarking](#Benchmarking)
    *   [7.2 Massimizzare le performance](#Massimizzare_le_performance)
*   [8 Gestione pacchetti](#Gestione_pacchetti)
    *   [8.1 Alias per pacman](#Alias_per_pacman)
    *   [8.2 Arch Build System](#Arch_Build_System)
    *   [8.3 Arch User Repository](#Arch_User_Repository)
    *   [8.4 Mirror](#Mirror)
*   [9 Gestione dell'alimentazione](#Gestione_dell'alimentazione)
    *   [9.1 acpid](#acpid)
    *   [9.2 Regolazione della frequenza della CPU](#Regolazione_della_frequenza_della_CPU)
    *   [9.3 Laptop](#Laptop)
*   [10 Amministrazione del sistema](#Amministrazione_del_sistema)
    *   [10.1 Mantenimento dei log](#Mantenimento_dei_log)
    *   [10.2 Privilege escalation](#Privilege_escalation)
    *   [10.3 Utenti e gruppi](#Utenti_e_gruppi)
    *   [10.4 Accesso a reti Windows](#Accesso_a_reti_Windows)
*   [11 Servizi di sistema](#Servizi_di_sistema)
    *   [11.1 Distribuzione di posta elettronica in locale](#Distribuzione_di_posta_elettronica_in_locale)
*   [12 Sistema grafico X](#Sistema_grafico_X)
    *   [12.1 Ambienti desktop](#Ambienti_desktop)
    *   [12.2 Driver video](#Driver_video)
    *   [12.3 Window manager](#Window_manager)

## Aspetto

*Questa sezione contiene modifiche viste di frequente per migliorare l'esperienza estetica su Arch. Per ulteriori informazioni si veda [Category:Eye candy (Italiano)](/index.php/Category:Eye_candy_(Italiano) "Category:Eye candy (Italiano)").*

### Output a colori

Anche se un gran numero di applicazioni prevede il supporto il colore, si può considerare l'uso di un wrapper come cope per colorare l'output dei comandi. Si può installare [cope](https://aur.archlinux.org/packages/cope/) oppure [cope-git](https://aur.archlinux.org/packages/cope-git/), la versione più aggiornata presa da [Git](/index.php/Git "Git"), direttamente da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)"). [acoc](https://aur.archlinux.org/packages/acoc/) e [cw](https://aur.archlinux.org/packages/cw/) sono alternative simili.

#### Console prompt

Il console prompt (PS1) può essere personalizzato in molte varianti. Si può trarre qualche idea dalla discussione [What's your PS1?](https://bbs.archlinux.org/viewtopic.php?id=50885) (in inglese). Si veda anche [Color Bash Prompt](/index.php/Color_Bash_Prompt "Color Bash Prompt") oppure [Zsh#Prompts](/index.php/Zsh#Prompts "Zsh"), nel caso si usi Zsh anzichè Bash.

#### Programmi di base

Per colorare l'output di alcuni programmi specifici come **grep** and **ls** si segua l'articolo sulle [Core utilities](/index.php/Core_utilities "Core utilities").

#### Emacs shell

Emacs è noto per includere delle opzioni ulteriori rispetto ai normali editor di testo, una di queste è quella di poter rappresentare un sostituto completo per la shell. Si guardi [Emacs#Colored output issues](/index.php/Emacs#Colored_output_issues "Emacs") per risolvere eventuali problemi con caratteri rovinati per via dell'output a colori.

#### Pagine di man

Le pagine di man sono una tra le risorse più utili disponibili per gli utenti di GNU/Linux. Per migliorare la leggibilità, il programma può essere configurato per rendere testo a colori come spiegato in [man page#Colored man pages](/index.php/Man_page#Colored_man_pages "Man page").

### Caratteri

Informazioni sull'argomento possono essere trovati alle pagine [Fonts (Italiano)](/index.php/Fonts_(Italiano) "Fonts (Italiano)") e [Configurazione dei font](/index.php/Font_configuration_(Italiano) "Font configuration (Italiano)").

#### Caratteri per la console

Se si passa molto tempo lavorando in una console virtuale (cioè al di fuori del server X), si può desiderare di cambiare il carattere della console per migliorare la leggibilità; si veda [Fonts (Italiano)#Fonts in virtual console](/index.php/Fonts_(Italiano)#Fonts_in_virtual_console "Fonts (Italiano)").

#### Patch per la visualizzazione dei font

Le librerie che gestiscono i font possono essere compilate con patch per migliorare la rappresentazione dei caratteri rispetto ai pacchetti standard; si veda [Font configuration (Italiano)#Pacchetti con patch](/index.php/Font_configuration_(Italiano)#Pacchetti_con_patch "Font configuration (Italiano)").

## Audio/video

*[Category:Multimedia (Italiano)](/index.php/Category:Multimedia_(Italiano) "Category:Multimedia (Italiano)") include ulteriori risorse sulle componenti multimediali.*

### Browser plugin

Per usufruire dei contenuti web multimediali e per un'esperienza web *completa*, si possono installare dei [plugin per il browser](/index.php/Browser_plugins "Browser plugins") come Adobe Acrobat Reader, Adobe Flash Player e Java.

### Codec

I [codec](/index.php/Codecs_(Italiano) "Codecs (Italiano)") vengono utilizzati dalle applicazioni multimediali per decodificare flussi audio e video. Per riprodurre questo tipo di file gli utenti devono curarsi di aver installato un codec appropriato.

## Fase di *boot*

*Questa sezione contiene informazioni riguardanti il processo di boot (avvio). Una spiegazione del processo di boot di Arch si può trovare alla pagina [Arch boot process (Italiano)](/index.php/Arch_boot_process_(Italiano) "Arch boot process (Italiano)"). Per altro, si guardi [Category:Boot process (Italiano)](/index.php/Category:Boot_process_(Italiano) "Category:Boot process (Italiano)").*

### Avviare i *daemon* in background

I *daemon* (demoni) sono programmi che girano in background, e normalmente vengono avviati durante la fase di boot. Allo scopo di velocizzare le fasi di avvio, alcuni daemon possono essere avviati in background, consentendo così al processo di boot di proseguire durante il loro caricamento. Si veda [Daemon (Italiano)](/index.php/Daemon_(Italiano) "Daemon (Italiano)") per una spiegazione esaustiva.

### Riconoscimento automatico dell'hardware

Durante il processo di boot, l'hardware dovrebbe essere riconosciuto automaticamente da [Udev](/index.php/Udev_(Italiano) "Udev (Italiano)"). Una potenziale riduzione del tempo di avvio può essere ottenuta disabilitando il caricamento automatico dei moduli a specificando i moduli richiesti manualmente in rc.conf. Anche [Xorg](/index.php/Xorg_(Italiano) "Xorg (Italiano)") dovrebbe essere in grado di determinare automaticamente i driver richiesti grazie a udev, ma l'utente ha comunque la possibilità di configurare il server X manualmente.

### Attivare *Num Lock* all'avvio

Per attivare la funzione *Num Lock* all'avvio del sistema, si segua [Activating Numlock on Bootup](/index.php/Activating_Numlock_on_Bootup "Activating Numlock on Bootup").

### Mantenere i messaggi di boot

Una volta che il processo di boot si conclude, lo schermo viene pulito per visualizzare la schermata di login, privando gli utenti della possibilità di recuperare informazioni sul processo di boot. Per superare questa limitazione si veda [Disable clearing of boot messages](/index.php/Disable_clearing_of_boot_messages "Disable clearing of boot messages").

### Lanciare X all'avvio

Se si utilizza un server [X](/index.php/X "X") per avere un interfaccia grafica, l'utente potrebbe desiderare di lanciare questo server durante il processo di avvio anzichè manualmente dopo il login. Si veda [Display manager (Italiano)](/index.php/Display_manager_(Italiano) "Display manager (Italiano)") se si desidera un login grafico oppure [Start X at boot (Italiano)](/index.php/Start_X_at_boot_(Italiano) "Start X at boot (Italiano)") per metodi che non richiedono un display manager.

## Migliorie per la console

*Questa sezione è dedicata a piccole modifiche per migliorare l'usabilità dei programmi per la riga di comando. Per ulteriori approfondimenti si guardi [Category:Command shells (Italiano)](/index.php/Category:Command_shells_(Italiano) "Category:Command shells (Italiano)") and [Category:Utilities (Italiano)](/index.php?title=Category:Utilities_(Italiano)&action=edit&redlink=1 "Category:Utilities (Italiano) (page does not exist)").*

### Alias

Gli utenti possono definire delle scorciatoie tramite un comando della shell per evitare di dover riscrivere ogni volta per intero i comandi usati più di frequente. Alcuni alias di uso comune si possono trovare in [Core utilities#alias](/index.php/Core_utilities#alias "Core utilities").

### Complementi per Bash

Un elenco di varie impostazioni per Bash, inclusi l'auto-completamento e la ricerca nello storico, disponibile alla voce [Bash (Italiano)#Trucchi e Consigli](/index.php/Bash_(Italiano)#Trucchi_e_Consigli "Bash (Italiano)").

### File compressi

I file compressi, o archivi, si trovano di frequente nell'utilizzo di un sistema GNU/Linux. [Tar](/index.php/Tar "Tar") è un programma di archiviazione tra i più comunemente usati e gli utenti dovrebbero avere una certa famigliarità con la relativa sintassi (i pacchetti di Arch Linux, per esempio, non sono altro che file tarball poi compressi con xzip). Si veda [Core utilities#extract](/index.php/Core_utilities#extract "Core utilities") per altri utili comandi.

### Supporto per il mouse

Usare il mouse per le operazioni di copia e incolla nella console può essere preferibile alla tradizionale modalità di copia di [GNU Screen](/index.php/GNU_Screen "GNU Screen"). Si guardi [Console mouse support (Italiano)](/index.php/Console_mouse_support_(Italiano) "Console mouse support (Italiano)") per istruzioni a riguardo.

### Scrollback buffer

Per poter salvare e visionare le schermate di testo precedenti che sono state passate, si consulti [Scrollback buffer](/index.php/Scrollback_buffer "Scrollback buffer").

### Gestione delle sessioni

Usando terminali in multiplexing come reso possibile da [tmux](/index.php/Tmux "Tmux") o [GNU Screen](/index.php/GNU_Screen "GNU Screen") si possono organizzare i programmi in tab o pannelli che possono essere richiamati all'occorenza; così se l'utente dovesse chiudere l'emulatore di terminale, terminare [Xorg](/index.php/Xorg_(Italiano) "Xorg (Italiano)"), o uscire, i programmi associati alla sessione continueranno a girare in background fino a che il server del terminal multiplexer è attivo. Per poter di nuovo interagire con i programmi è necessario riconnettersi alla sessione.

## Input

*Questa sezione illustra alcune configurazioni comuni per i vari dispositivi di input. Per altro si segua [Category:Input devices (Italiano)](/index.php/Category:Input_devices_(Italiano) "Category:Input devices (Italiano)").*

### Configurare tutti i pulsanti del mouse

I possessori di mouse avanzati, o comunque inusuali, potrebbero non trovare tutti i pulsanti del dispositivo riconosciuti di default, oppure potrebbero voler assegnare differenti azioni per i pulsanti in più. Le istruzioni per far ciò possono essere trovare in [Get All Mouse Buttons Working](/index.php/Get_All_Mouse_Buttons_Working "Get All Mouse Buttons Working").

### Mappatura della tastiera

Di default le tastiere diverse da quella standard inglese possono funzionare diversamente da come ci si aspetta. Per definire la mappatura della tastiera nelle console virtuali, bisogna settare la variabile [KEYMAP](/index.php/KEYMAP "KEYMAP") nel file rc.conf. Per gli utenti di [Xorg](/index.php/Xorg_(Italiano) "Xorg (Italiano)"), le modifiche richieste sono descritte in [Xorg (Italiano)#Impostazioni della tastiera](/index.php/Xorg_(Italiano)#Impostazioni_della_tastiera "Xorg (Italiano)").

### Touchpad nei laptop

Gran parte dei pc portatili usa dispositivi di puntamento "touchpad" [Synaptics](http://www.synaptics.com/) o [[[http://www.alps.com/](http://www.alps.com/) ALPS. Questi ed altri modelli compatibili utilizzano il driver Synaptics; si veda [Touchpad Synaptics (Italiano)](/index.php/Touchpad_Synaptics_(Italiano) "Touchpad Synaptics (Italiano)") per l'installazione e i dettagli di configurazione.

## Networking

*Questa sezione si limita a illustrare semplici procedure per migliorare la connettività di rete. Si segua [Network](/index.php/Network "Network") per una guida completa. Per altro, si veda [Category:Networking (Italiano)](/index.php/Category:Networking_(Italiano) "Category:Networking (Italiano)").*

### Sincronizzazione dell'orologio

Il [Network Time Protocol](/index.php/Network_Time_Protocol_(Italiano) "Network Time Protocol (Italiano)") (NTP) è un protocollo per sincronizzare automaticamente l'orologio di sistema attraverso una rete a commutazione di pacchetto.

### Disabilitare IPv6

Il modulo IPv6 non solo occupa circa 250kb di memoria, ma si riscontra che disabilitarne il funzionamento velocizza visibilmente l'accesso alla rete per i programmi che erroneamente cercano di accedere ai server con questa nuova versione. Anche [Firefox](/index.php/Firefox_(Italiano) "Firefox (Italiano)") è tra le applicazioni influenzate. Quindi finchè non ci sarà un'ampia adozione di IPv6, si può trarre beneficio [disabilitando il modulo](/index.php/IPv6_-_Disabling_the_Module "IPv6 - Disabling the Module").

### Aumentare la velocità dei DNS

Per migliorare il tempo di caricamento tenendo la cache per le *query*, si usi [pdnsd](/index.php/Pdnsd "Pdnsd"), Un server DNS senza l'ambizione di soddisfare ogni necessità. Oppure si installi [dnsmasq](/index.php/Dnsmasq "Dnsmasq"), Una scelta di più ampio utilizzo che permette anche di rendere il sistema un server DHCP.

### Convalida DNSSEC

Per una migliore sicurezza durante la navigazione nel web, i pagamenti online, la connessione a servizi [SSH](/index.php/SSH_(Italiano) "SSH (Italiano)") e impieghi simili, si può considerare l'utilizzo di software abilitato per [DNSSEC](/index.php/DNSSEC "DNSSEC") che può convalidare firme certificate per i [DNS](/index.php/DNS "DNS")...

## Ottimizzazione

*Questa sezione raccoglie trucchi e strumenti utili per migliorare le performance del sistema e delle applicazioni.*

### Benchmarking

Il [Benchmarking](/index.php/Benchmarking "Benchmarking") è il processo di misura, attraverso una procedura unica e ben definita, e di relativo confronto con il risultato di un altro sistema o con uno standard di riferimento

### Massimizzare le performance

L'articolo [Improving performance](/index.php/Improving_performance "Improving performance") raccoglie molte idee per ottenere un guadagno sulle performance in Arch Linux.

## Gestione pacchetti

*Questa sezione contiene utili informazioni sulla gestione dei pacchetti. Tutti gli utenti dovrebbero essere a loro agio con il gestore di pacchetti [pacman](/index.php/Pacman "Pacman"). Si veda anche [Category:Package management (Italiano)](/index.php/Category:Package_management_(Italiano) "Category:Package management (Italiano)").*

### Alias per pacman

Creare un alias per un comando è un modo per risparmiare tempo quando si usa la console. Questo è specialmente utile per compiti ripetitivi che non necessitano una modifica significativa dei parametri tra le varie esecuzioni. Vari alias per pacman aliases sono suggeriti in [pacman tips](/index.php/Pacman_tips "Pacman tips"), insieme ad altri strumenti consigliati.

### Arch Build System

Le distribuzioni BSD furono le prime ad introdurre il sistema di *port* che consiste nella raccolta, organizzata in una struttura di cartelle residente sul disco, di script per la compilazione. In parole semplici, un port non è nient'altro che uno script che permette di installare un applicazione; questo script, per essere facilmente rintracciabile, si trova all'interno di una cartella il cui nome indica l'applicazione.

[ABS](/index.php/ABS "ABS") offre la stessa funzionalità attraverso script per la compilazione detti [PKGBUILD](/index.php/PKGBUILD_(Italiano) "PKGBUILD (Italiano)") che contengono le informazioni necessarie per un certo software: controlli di integrità, indirizzo del progetto, versione, licenza e i comandi di compilazione. I PKGBUILD devono essere processati da [makepkg](/index.php/Makepkg_(Italiano) "Makepkg (Italiano)"), il programma che genera pacchetti gestibili da pacman.

Qualsiasi pacchetto nei repositori così come quelli presenti in AUR è compilabile con makepkg.

### Arch User Repository

Mentre [ABS](/index.php/ABS "ABS") permette di compilare software disponibile nei repositori ufficiali, [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") lo permette per pacchetti inviati dagli utenti. Si tratta di un repositori di script non supportati a cui si può accedere mediante l'[interfaccia web](https://aur.archlinux.org/index.php) o cono un [AUR helper](/index.php/AUR_helper "AUR helper").

Gli [AUR helper](/index.php/AUR_helper "AUR helper") gestiscono un accesso trasparente ad AUR, possono avere funzionalità differenti ma tutti aiutano la ricerca, il download, la compilazione e l'installazione degli oltre 20.000 PKGBUILD nei repositori non ufficiali.

### Mirror

Si visiti [Mirrors (Italiano)](/index.php/Mirrors_(Italiano) "Mirrors (Italiano)") per istruzioni su come trarre il massimo vantaggio dall'usare i mirror per pacman più veloci ed aggiornati. Come spiegato nell'articolo, è buona abitudine controllare periodicamente [[1]](https://www.archlinux.org/mirrors/status/) oppure [Mirror status](http://www.archlinux.de/?page=MirrorStatus) per una lista di mirror che sono stati sincronizzati di recente.

## Gestione dell'alimentazione

*Questa sezione può essere utile per i possessori di computer laptop o comunque a chi è interessato al controllo del consumo di energia. Per approfondimenti si veda [Category:Power management (Italiano)](/index.php/Category:Power_management_(Italiano) "Category:Power management (Italiano)").*

### acpid

Gli utenti possono configurare le risposte del sistema ad eventi ACPI come la pressione del pulsante di spegnimento o la chiusura del laptop tramite [acpid](/index.php/Acpid "Acpid").

### Regolazione della frequenza della CPU

I processori moderni possono ridurre la propria frequenza e tensione per ridurre temperatura e consumi. Mantenendo temperature più basse si ottiene un sistema più silenzioso e si prolunga la vita delle componenti hardware. [cpufrequtils](/index.php/Cpufrequtils_(Italiano) "Cpufrequtils (Italiano)") è un set di programmi pensati per gestire la regolazione della frequenza della CPU.

### Laptop

Per pagine dedicate ai computer portatili, insieme a guide di installazione specifiche per un determinato modello, si veda [Category:Laptops (Italiano)](/index.php/Category:Laptops_(Italiano) "Category:Laptops (Italiano)"). Per uno sguardo globale sulle raccomandazioni d'uso per i laptop si veda [Laptop (Italiano)](/index.php/Laptop_(Italiano) "Laptop (Italiano)").

## Amministrazione del sistema

*Questa sezione tratta le attività di amministrazione e di gestione del sistema. Si veda anche [Category:System administration (Italiano)](/index.php/Category:System_administration_(Italiano) "Category:System administration (Italiano)").*

### Mantenimento dei log

Per default, i file di log files sono archiviati grazie a [logrotate](/index.php/Logrotate "Logrotate"), che rinomina i file di log postponendo al nome un numero e pulisce i file originali. Logrotate viene eseguito normalmente per mezzo di [cron](/index.php/Cron "Cron"); gli utenti si assicurino che il demone cron sia in esecuzione per usare logrotate.

Gli utenti che utilizzano [syslog-ng](https://www.archlinux.org/packages/?name=syslog-ng) potrebbero volere configurare i [timestamps ISO 8601](/index.php/Syslog-ng#ISO_8601_timestamps "Syslog-ng") (aaaa-mm-ggThh:mm:ss-zz:zz) per i file di log.

### Privilege escalation

Un'installazione nuova lascia gli utenti con il solo account di super utente, meglio conosciuto come root. Autenticarsi come root per periodi prolungati è ampiamente riconosciuto come pericoloso se non folle. Gli utenti dovrebbero invece [creare](/index.php/User_Management_(Italiano) "User Management (Italiano)") ed usare account utente non privilegiati per la maggior parte delle attività, usando l'account di root solo per l'amministrazione del sistema. Il comando [su](/index.php/Su "Su") (*substitute user*) permette di assumere l'identità di un altro utente sul sistema (normalmete root) nella propria shell, mentre il comando [sudo](/index.php/Sudo "Sudo") (*super user do*) garantisce privilegi per uno specifico comando.

### Utenti e gruppi

[Utenti](/index.php/User_Management_(Italiano) "User Management (Italiano)") e [gruppi](/index.php/Groups_(Italiano) "Groups (Italiano)") si usano su GNU/Linux per controllare accessi e privilegi; gli amministratori possono aggiustare finemente l'appartenenza a gruppi e le proprietà per permettere o negare ad utenti e a programmi di accedere a determinate risorse del sistema. L'accesso a periferiche come drive CD/DVD e schede audio spesso richiede l'appartenenza a determinati gruppi.

### Accesso a reti Windows

Per abilitare la comunicazione tra macchine Windows e Linux attraverso una rete, si può utilizzare [Samba](/index.php/Samba_(Italiano) "Samba (Italiano)"); una reimplementazione del protocollo di rete SMB/CIFS.

## Servizi di sistema

*Questa sezione è collegata a [daemons](/index.php/Daemons "Daemons"). Per approfondire si veda [Category:Daemons and system services (Italiano)](/index.php/Category:Daemons_and_system_services_(Italiano) "Category:Daemons and system services (Italiano)").*

### Distribuzione di posta elettronica in locale

Un'installazione di base non offre alcun mezzo per la sincronizzazione della posta elettronica. Per configurare Postfix al fine di gestire una semplice casella di posta locale si veda [Local Mail Delivery with Postfix](/index.php/Local_Mail_Delivery_with_Postfix "Local Mail Delivery with Postfix"). Altre opzioni sono [SSMTP](/index.php/SSMTP "SSMTP"), [Msmtp](/index.php/Msmtp "Msmtp") e [fdm](/index.php/Fdm "Fdm").

## Sistema grafico X

*[Xorg](/index.php/Xorg_(Italiano) "Xorg (Italiano)") è l'implementazione open source della versione 11 di X Window System. Se si deisdera un'interfaccia grafica, la maggior parte degli utenti useranno Xorg. Si veda [Category:X Server (Italiano)](/index.php?title=Category:X_Server_(Italiano)&action=edit&redlink=1 "Category:X Server (Italiano) (page does not exist)") per ulteriori risorse.*

### Ambienti desktop

Mentre [Xorg](/index.php/Xorg_(Italiano) "Xorg (Italiano)") costituisce le fondamenta per costruire un ambiente grafico, ci sono componenti aggiuntivi che possono essere considerati necessari per un'esperienza utente completa. Gli [ambienti desktop](/index.php/Desktop_environment "Desktop environment") come ad esempio [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)"), [KDE](/index.php/KDE_(Italiano) "KDE (Italiano)"), [LXDE](/index.php/LXDE_(Italiano) "LXDE (Italiano)") e [Xfce](/index.php/Xfce_(Italiano) "Xfce (Italiano)") riuniscono assieme un'ampia gamma di programmi come window manager, pannelli, file manager, emulatore di terminale, editor di testo, icone e altre utilities. Si consulti [Category:Desktop environments (Italiano)](/index.php/Category:Desktop_environments_(Italiano) "Category:Desktop environments (Italiano)") per una lista completa di risorse aggiuntive.

### Driver video

Il driver video *vesa* predisosto di default funziona con la maggior parte delle schede grafiche, ma le performance possono essere migliorate visibilmente installando il driver più appropriato per prodotti [ATI](/index.php/ATI_(Italiano) "ATI (Italiano)"), [Intel](/index.php/Intel_(Italiano) "Intel (Italiano)"), or [NVIDIA](/index.php/NVIDIA_(Italiano) "NVIDIA (Italiano)") products.

### Window manager

Un [ambiente desktop](/index.php/Desktop_environment "Desktop environment") fornisce un'interfaccia grafica completa e consistente, ma tende a consumare un gran quantitativo di risorse di sistema. Gli utenti che cercano di massimizzare le performance o di semplificare il proprio ambiente grafico possono scegliere di installare un [window manager](/index.php/Window_manager "Window manager") e scegliere uno per uno i programmi desiderati. Un window manager alternativo può essere anche usato com la maggior parte degli ambienti desktop. Window manager di tipo [dinamico](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs"), [stacking](/index.php/Category:Stacking_WMs_(Italiano) "Category:Stacking WMs (Italiano)"), e [tiling](/index.php/Category:Tiling_WMs "Category:Tiling WMs") differiscono per il modo di gestire il posizionamento delle finestre.