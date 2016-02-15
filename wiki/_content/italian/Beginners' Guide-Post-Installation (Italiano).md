**Suggerimento:** Questa è una parte della versione suddivisa in pagine multiple della Guida per Principianti. [Cliccare qui](/index.php/Guida_per_Principianti "Guida per Principianti") se si preferisce consultare la guida nella sua interezza.

## Contents

*   [1 Post-Installazione](#Post-Installazione)
    *   [1.1 Gestione Utenti](#Gestione_Utenti)
    *   [1.2 Gestione dei pacchetti](#Gestione_dei_pacchetti)
    *   [1.3 Gestione dei servizi](#Gestione_dei_servizi)
    *   [1.4 Audio](#Audio)
    *   [1.5 Graphical User Interface (interfaccia grafica utente)](#Graphical_User_Interface_.28interfaccia_grafica_utente.29)
        *   [1.5.1 Installare X](#Installare_X)
        *   [1.5.2 Installare un driver video](#Installare_un_driver_video)
        *   [1.5.3 Installare driver di input](#Installare_driver_di_input)
        *   [1.5.4 Configurare X](#Configurare_X)
        *   [1.5.5 Testare X](#Testare_X)
            *   [1.5.5.1 In caso di errori](#In_caso_di_errori)
        *   [1.5.6 Font](#Font)
        *   [1.5.7 Scegliere ed installare una interfaccia grafica](#Scegliere_ed_installare_una_interfaccia_grafica)
*   [2 Appendice](#Appendice)

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

**[Guida per Principianti](/index.php/Beginners%27_Guide_(Italiano) "Beginners' Guide (Italiano)")**

* * *

[Preparazione](/index.php/Beginners%27_Guide/Preparation_(Italiano) "Beginners' Guide/Preparation (Italiano)") >> [Installazione](/index.php/Beginners%27_Guide/Installation_(Italiano) "Beginners' Guide/Installation (Italiano)") >> **Post-Installazione**