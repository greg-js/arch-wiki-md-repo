Articoli correlati

*   [Desktop Environment](/index.php/Desktop_Environment_(Italiano) "Desktop Environment (Italiano)")
*   [Display Manager](/index.php/Display_Manager_(Italiano) "Display Manager (Italiano)")
*   [Window Manager](/index.php/Window_Manager_(Italiano) "Window Manager (Italiano)")
*   [Plasma](/index.php/Plasma_(Italiano) "Plasma (Italiano)")
*   [Qt](/index.php/Qt "Qt")
*   [KDevelop 4](/index.php/KDevelop_4 "KDevelop 4")
*   [Integrazione dei temi di KDE 4 con le applicationi GTK](/index.php/Uniform_Look_for_Qt_and_GTK_Applications_(Italiano) "Uniform Look for Qt and GTK Applications (Italiano)")

Tratto da [KDE - KDE Software Compilation](http://www.kde.org/community/whatiskde/softwarecompilation.php) e [Getting KDE Software](http://www.kde.org/download/):

	*Il KDE Software Compilation è l'insieme di strutture, aree di lavoro e applicazioni prodotte da KDE. Nella sua creazione, KDE è nato per realizzare un bellissimo, funzionale e gratuito ambiente di elaborazione desktop per Linux e sistemi operativi analoghi. KDE è costituito da un gran numero di applicazioni individuali e da uno spazio di lavoro desktop, inteso come un guscio all'interno del quale è possibile eseguire queste applicazioni in modo integrato.*

Il progetto KDE fornisce a monte un ottimo [UserBase wiki](http://userbase.kde.org/Welcome_to_KDE_UserBase/it), dove gli utenti possono ottenere informazioni dettagliate sulla maggior parte delle applicazioni integrate in KDE.

## Contents

*   [1 Installazione](#Installazione)
    *   [1.1 Plasma Desktop](#Plasma_Desktop)
    *   [1.2 Aggiornare Plasma 4 a 5](#Aggiornare_Plasma_4_a_5)
    *   [1.3 Applicazioni KDE e pacchetti lingua](#Applicazioni_KDE_e_pacchetti_lingua)
*   [2 Avviare Plasma](#Avviare_Plasma)
*   [3 Configurazione](#Configurazione)
    *   [3.1 Personalizzazione](#Personalizzazione)
        *   [3.1.1 Plasma Desktop](#Plasma_Desktop_2)
            *   [3.1.1.1 Temi](#Temi)
            *   [3.1.1.2 Widgets (Plasmoidi)](#Widgets_.28Plasmoidi.29)
            *   [3.1.1.3 Applet per il suono nella barra delle applicazioni](#Applet_per_il_suono_nella_barra_delle_applicazioni)
            *   [3.1.1.4 Aggiunta di un menu globale sul desktop](#Aggiunta_di_un_menu_globale_sul_desktop)
        *   [3.1.2 Decorazioni delle finestre](#Decorazioni_delle_finestre)
        *   [3.1.3 Temi Icone](#Temi_Icone)
        *   [3.1.4 Caratteri](#Caratteri)
            *   [3.1.4.1 Caratteri visivamente brutti in KDE](#Caratteri_visivamente_brutti_in_KDE)
            *   [3.1.4.2 I caratteri sono grandi o sembrano sproporzionati](#I_caratteri_sono_grandi_o_sembrano_sproporzionati)
        *   [3.1.5 Efficienza dello spazio di lavoro](#Efficienza_dello_spazio_di_lavoro)
    *   [3.2 Networking](#Networking)
    *   [3.3 Stampa](#Stampa)
    *   [3.4 Supporto a Samba/Windows](#Supporto_a_Samba.2FWindows)
    *   [3.5 Attività Desktop di KDE](#Attivit.C3.A0_Desktop_di_KDE)
    *   [3.6 Risparmio energetico](#Risparmio_energetico)
    *   [3.7 Monitorare i cambiamenti su file locali e cartelle](#Monitorare_i_cambiamenti_su_file_locali_e_cartelle)
*   [4 Amministrazione del Sistema](#Amministrazione_del_Sistema)
    *   [4.1 Impostare il layout per cambiare la mappatura della tastiera](#Impostare_il_layout_per_cambiare_la_mappatura_della_tastiera)
    *   [4.2 Terminare Xorg-server attraverso le impostazioni di sistema di KDE](#Terminare_Xorg-server_attraverso_le_impostazioni_di_sistema_di_KDE)
    *   [4.3 Moduli kcm utili](#Moduli_kcm_utili)
*   [5 Ricerca Desktop e Desktop Semantico](#Ricerca_Desktop_e_Desktop_Semantico)
    *   [5.1 Virtuoso e Soprano](#Virtuoso_e_Soprano)
    *   [5.2 Nepomuk](#Nepomuk)
        *   [5.2.1 Utilizzare e configurare Nepomuk](#Utilizzare_e_configurare_Nepomuk)
        *   [5.2.2 KDE senza Nepomuk](#KDE_senza_Nepomuk)
    *   [5.3 Akonadi](#Akonadi)
        *   [5.3.1 Disabilitare Akonadi](#Disabilitare_Akonadi)
        *   [5.3.2 Configurare il database](#Configurare_il_database)
        *   [5.3.3 Esecuzione di KDE senza Akonadi](#Esecuzione_di_KDE_senza_Akonadi)
*   [6 Phonon](#Phonon)
    *   [6.1 Cos'è Phonon ?](#Cos.27.C3.A8_Phonon_.3F)
    *   [6.2 Quale backend si dovrebbe scegliere?](#Quale_backend_si_dovrebbe_scegliere.3F)
*   [7 Applicazioni utili](#Applicazioni_utili)
    *   [7.1 Yakuake](#Yakuake)
    *   [7.2 KDE Telepathy](#KDE_Telepathy)
*   [8 Trucchi e Consigli](#Trucchi_e_Consigli)
    *   [8.1 Utilizzare Openbox in KDE](#Utilizzare_Openbox_in_KDE)
        *   [8.1.1 Riattivare gli effetti del compositing](#Riattivare_gli_effetti_del_compositing)
    *   [8.2 Integrare Android con il desktop KDE](#Integrare_Android_con_il_desktop_KDE)
    *   [8.3 Ricevere le notifiche per gli aggiornamenti software](#Ricevere_le_notifiche_per_gli_aggiornamenti_software)
    *   [8.4 Configurare KWin per utilizzare le OpenGL ES](#Configurare_KWin_per_utilizzare_le_OpenGL_ES)
    *   [8.5 Abilitare le anteprime audio/video nei file manager Konqueror e Dolphin](#Abilitare_le_anteprime_audio.2Fvideo_nei_file_manager_Konqueror_e_Dolphin)
    *   [8.6 Velocizzare l'avvio delle applicazioni](#Velocizzare_l.27avvio_delle_applicazioni)
    *   [8.7 Nascondere partizioni](#Nascondere_partizioni)
    *   [8.8 Suggerimenti per Konqueror](#Suggerimenti_per_Konqueror)
        *   [8.8.1 Disabilitare i Tooltips (Browser)](#Disabilitare_i_Tooltips_.28Browser.29)
        *   [8.8.2 Usare WebKit](#Usare_WebKit)
    *   [8.9 Integrazione di Firefox](#Integrazione_di_Firefox)
    *   [8.10 Impostare lo sfondo del LockScreen per avere lo stesso sfondo del desktop](#Impostare_lo_sfondo_del_LockScreen_per_avere_lo_stesso_sfondo_del_desktop)
    *   [8.11 Impostare l'immagine del lockscreen ad una arbitraria](#Impostare_l.27immagine_del_lockscreen_ad_una_arbitraria)
*   [9 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [9.1 Correlati alla configurazione](#Correlati_alla_configurazione)
        *   [9.1.1 Ripristinare tutte le configurazioni di KDE](#Ripristinare_tutte_le_configurazioni_di_KDE)
        *   [9.1.2 Il servizio di indicizzazione dei file non funziona anche dopo aver abilitato tutto correttamente](#Il_servizio_di_indicizzazione_dei_file_non_funziona_anche_dopo_aver_abilitato_tutto_correttamente)
        *   [9.1.3 Il desktop Plasma si comporta stranamente](#Il_desktop_Plasma_si_comporta_stranamente)
        *   [9.1.4 Pulire la cache per risolvere i problemi di aggiornamento](#Pulire_la_cache_per_risolvere_i_problemi_di_aggiornamento)
    *   [9.2 Pulire al configurazione di Akonadi per ripristinare Kmail](#Pulire_al_configurazione_di_Akonadi_per_ripristinare_Kmail)
    *   [9.3 Come ottenere informazioni sullo stato di KWin per il supporto e il debug](#Come_ottenere_informazioni_sullo_stato_di_KWin_per_il_supporto_e_il_debug)
    *   [9.4 KDE4 non termina il caricamento](#KDE4_non_termina_il_caricamento)
    *   [9.5 KDE ed i programmi in Qt vengono visualizzati in maniera errata con gestori di finestre differenti](#KDE_ed_i_programmi_in_Qt_vengono_visualizzati_in_maniera_errata_con_gestori_di_finestre_differenti)
    *   [9.6 Problemi legati all'aspetto grafico](#Problemi_legati_all.27aspetto_grafico)
        *   [9.6.1 Performance desktop 2D scadenti (o) appaiono Artefatti durante il 2D](#Performance_desktop_2D_scadenti_.28o.29_appaiono_Artefatti_durante_il_2D)
            *   [9.6.1.1 Problema con i driver GPU](#Problema_con_i_driver_GPU)
            *   [9.6.1.2 Utilizzare il motore Raster](#Utilizzare_il_motore_Raster)
        *   [9.6.2 Performance 3D scadenti](#Performance_3D_scadenti)
        *   [9.6.3 Il Composite per il Desktop è disabilitato con una recente schede video Nvidia](#Il_Composite_per_il_Desktop_.C3.A8_disabilitato_con_una_recente_schede_video_Nvidia)
        *   [9.6.4 Tremolio in fullscreen quando il Composite è attivato](#Tremolio_in_fullscreen_quando_il_Composite_.C3.A8_attivato)
        *   [9.6.5 Tearing dello schermo con gli effetti desktop abilitati](#Tearing_dello_schermo_con_gli_effetti_desktop_abilitati)
        *   [9.6.6 Impostazioni di visualizzazione perse al riavvio (monitor multipli)](#Impostazioni_di_visualizzazione_perse_al_riavvio_.28monitor_multipli.29)
    *   [9.7 Problemi sonori in KDE](#Problemi_sonori_in_KDE)
        *   [9.7.1 Problemi legati ad ALSA](#Problemi_legati_ad_ALSA)
            *   [9.7.1.1 Comparsa di messaggi "Falling back to default" quando si prova ad ascoltare qualsiasi suono in KDE](#Comparsa_di_messaggi_.22Falling_back_to_default.22_quando_si_prova_ad_ascoltare_qualsiasi_suono_in_KDE)
            *   [9.7.1.2 Non riesco a riprodurre file MP3 quando imposto come backend Gstreamer in Qt Phonon](#Non_riesco_a_riprodurre_file_MP3_quando_imposto_come_backend_Gstreamer_in_Qt_Phonon)
    *   [9.8 Konsole non salva la lista dei comandi](#Konsole_non_salva_la_lista_dei_comandi)
    *   [9.9 Le password in KDE mostrano tre pallini per ogni lettera](#Le_password_in_KDE_mostrano_tre_pallini_per_ogni_lettera)
    *   [9.10 Il processo di Nepomukserver si avvia automaticamente anche se il desktop semantico è disabilitato](#Il_processo_di_Nepomukserver_si_avvia_automaticamente_anche_se_il_desktop_semantico_.C3.A8_disabilitato)
    *   [9.11 Dolphin e le finestre di dialogo sono estremamente lente ad inizializzarsi ogni volta](#Dolphin_e_le_finestre_di_dialogo_sono_estremamente_lente_ad_inizializzarsi_ogni_volta)
    *   [9.12 Visualizzatore PDF di default nelle applicazioni GTK sotto KDE](#Visualizzatore_PDF_di_default_nelle_applicazioni_GTK_sotto_KDE)
*   [10 Versione KDE instabile](#Versione_KDE_instabile)
*   [11 Altri progetti su KDE =](#Altri_progetti_su_KDE_.3D)
    *   [11.1 Trinity](#Trinity)
*   [12 Bugs](#Bugs)
*   [13 Links Esterni](#Links_Esterni)

## Installazione

### Plasma Desktop

**Note:**

*   Plasma 5 non è installabile con Plasma 4.
*   Il desktop Plasma 4 è fuori manutenzione dall' Agosto 2015.[[1]](https://www.kde.org/announcements/announce-applications-15.08.0.php) Non è più nei repository ufficiali dal Dicembre 2015.[[2]](https://www.archlinux.org/news/dropping-plasma-4/)
*   KDM non è più disponibile per Plasma 5\. KDE [raccomanda](http://blog.davidedmundson.co.uk/blog/display_managers_finale) di usare il display manager [SDDM](/index.php/SDDM "SDDM") poichè supporta l'integrazione con il tema di Plasma 5.

Prima di installare Plasma, assicurati di avere un' installazione funzionante di [Xorg](/index.php/Xorg "Xorg") nel tuo sistema.

Installa il meta-pacchetto [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) o il gruppo [plasma](https://www.archlinux.org/groups/x86_64/plasma/). per le differenze tra [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) e [plasma](https://www.archlinux.org/groups/x86_64/plasma/) consulta [Creating packages#Meta packages and groups](/index.php/Creating_packages#Meta_packages_and_groups "Creating packages"). Altrimenti, per una installazione più minimale di Plasma,installa il pacchetto [plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop) .

### Aggiornare Plasma 4 a 5

1.  Isola `multi-user.target` `# systemctl isolate multi-user.target` 
2.  Se usi KDM come display manager, disabilitalo `# systemctl disable kdm` 
3.  Disinstalla il pacchetto kde-workspace `# pacman -Rc kdebase-workspace` 
4.  Installa il pacchetto [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) o il gruppo [plasma](https://www.archlinux.org/groups/x86_64/plasma/).
5.  Abilita [SDDM](/index.php/SDDM "SDDM") `# systemctl enable sddm` o installa e abilita qualcun altro [display manager](/index.php/Display_manager "Display manager").
6.  Riavvia o semplicemente scrivi `# systemctl start sddm` nel terminale.

**Note:** La configurazione Plasma 4 non è migrata automaticamente al Plasma 5, in modo da configurare il desktop da zero.

### Applicazioni KDE e pacchetti lingua

Per installare tutte le applicazioni di KDE, installa il gruppo [kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/) o il meta-pacchetto [kde-applications-meta](https://www.archlinux.org/packages/?name=kde-applications-meta) per installare moduli specifici. Nota che questo installerà solo le applicazioni, non installerà alcuna versione del Desktop Plasma.

Se hai bisogno di un pacchetto lingua, installa `kde-l10n-**tualingua**` (e.g. [kde-l10n-it](https://www.archlinux.org/packages/?name=kde-l10n-it) per il linguaggio italiano). Per una lista completa di linguaggi disponibili, guarda [questo link](https://www.archlinux.org/packages/extra/any/kde-l10n/).

## Avviare Plasma

**Suggerimento:** Per integrare meglio SDDM con Plasma, è raccomandato di modificare `/etc/sddm.conf` per usare il tema breeze. Consulta [SDDM#Theme settings](/index.php/SDDM#Theme_settings "SDDM") per istruzioni.

**Nota:** La configurazione Plasma 4 non è automaticamente migrata a Plasma 5, quindi dovrai configurare il tuo desktop da zero.

Per lanciare una sessione PLasma 5, scegli *Plasma* nel menu del tuo [display manager](/index.php/Display_manager "Display manager") .

Altrimenti, per avviare Plasma con *startx*, aggiungi `exec startkde` al tuo file `.xinitrc`. Se vuoi avviare Xorg al login, guarda [Start X at login](/index.php/Start_X_at_login "Start X at login").

## Configurazione

Tutta la configurazione di KDE viene salvato nella cartella `~/.Kde4`. Se KDE comincia a dare parecchi problemi o se volete una nuova installazione di KDE, eliminate o rinominate questa cartella e riavviare la sessione di X. KDE creerà nuovamente questa cartella con tutti i file di configurazione di default. Se si desidera che un controllo molto fine sui propri programmi di KDE, allora si può decidere di modificare i file in questa cartella.

La configurazione di KDE si effettua principalmente da '**Impostazioni di Sistema'**. Ci sono poche altre opzioni disponibili per il desktop in '**Impostazioni predefinite del Desktop'** quando si clicca con il tasto destro del mouse sul desktop.

Per le altre opzioni di personalizzazione non trattate qui sotto, come le attività, differenti sfondi su un cubo, ecc. si prega di fare riferimento alla pagina wiki di [Plasma](/index.php/Plasma "Plasma")

### Personalizzazione

Come impostare il desktop di KDE a seconda del proprio stile personale; si possono usare differenti temi di Plasma, decorazioni di finestre e temi di icone.

#### Plasma Desktop

[Plasma](/index.php/Plasma_(Italiano) "Plasma (Italiano)") è una tecnologia di integrazione desktop che fornisce molte funzioni, come visualizzare lo sfondo, aggiungere widget sul desktop, manipolare i pannelli o la "barra delle applicazioni".

##### Temi

[I temi di Plasma](http://kde-look.org/index.php?xcontentmode=76) possono esseri installati attraverso il pannello di controllo delle impostazioni del Desktop. I temi di plasma definiscono l'aspetto dei pannelli e dei plasmoidi. Per una installazione facilitata a livello di sistema, alcuni di questi temi sono disponibili sia nei repository ufficiali che in [AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmatheme&do_Search=Go).

##### Widgets (Plasmoidi)

I **Plasmoidi** sono piccoli script (plasmoid scripts) o codici (plasmoid binaries) di applicazioni di KDE che migliorano la funzionalità del desktop.

I file binari possono essere installati usando i PKGBUILDs da [AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmoid&do_Search=Go&PP=25&SO=d&SB=v), oppure scrivendo il proprio PKGBUILD.

Il modo più semplice per installare i plasmoidi basati su script è quello di cliccare col tasto destro del mouse su un pannello o sul desktop e quindi:

```
Aggiungi Oggetti > Prendi nuovi Oggetti > Scarica nuovi oggetti di Plasma

```

Ciò aprirà un'interfaccia collegata a [kde-look.org](http://www.kde-look.org/) choke permetterà la (dis)installazione o l'aggiornamento di script da terze parti con l'utilizzo di un solo click.

La maggior parte dei plasmoidi difatti non è creata ufficialmente dagli sviluppatori di KDE. Si potrebbe anche provare ad installare i widget di Mac Os X, quelli di Microsoft Windows Vista/7, quelli di Google e persino quelli di SuperKaramba.

##### Applet per il suono nella barra delle applicazioni

Installare Kmix ([kmix](https://www.archlinux.org/packages/?name=kmix)) dai repository ufficiali e avviarlo dal launcher delle applicazioni. Da sempre KDE, per impostazione predefinita , avvia automaticamente i programmi della sessione precedente, non ha bisogno di essere avviati manualmente ad ogni login.

**Note:** Per impostare [lo step per aumentare/diminuire il volume](https://bugs.kde.org/show_bug.cgi?id=313579#c28), aggiungere ad esempio `VolumePercentageStep=1` nella sezione `[Global]` di `~/.kde4/share/config/kmixrc`

##### Aggiunta di un menu globale sul desktop

Installare [appmenu-qt4](https://www.archlinux.org/packages/?name=appmenu-qt4) dai repository ufficiali e [appmenu-gtk](https://aur.archlinux.org/packages/appmenu-gtk/) e [appmenu-QT5](https://aur.archlinux.org/packages/appmenu-QT5/) da AUR al fine di completare i preliminari per avere sempre un menu globale stile Mac OS X. Per far in modo che Firefox e LibreOffice utilizzino il menu globale, installare [firefox-extension-globalmenu](https://aur.archlinux.org/packages/firefox-extension-globalmenu/) e [libreoffice-extension-menubar](https://aur.archlinux.org/packages/libreoffice-extension-menubar/) da AUR.

**Attenzione:** [firefox-extension-globalmenu](https://aur.archlinux.org/packages/firefox-extension-globalmenu/) è stato deprecato a partire da Firefox 25 e non c'è altro metodo consigliato per ottenere il menu globale. Tuttavia, vi è un pacchetto di patch, [firefox-ubuntu](https://aur.archlinux.org/packages/firefox-ubuntu/). Disponibile su AUR che ha la patch di Canonical per ottenere il menu globale di lavorare con la versione attuale di Firefox (al momento della scrittura)

Per ottenere effettivamente il menu globale, installare [kdeplasma-applet-menubar](https://aur.archlinux.org/packages/kdeplasma-applet-menubar/) da AUR. Creare un pannello plasma sulla parte superiore dello schermo e aggiungere l'applet "barra dei menu" al pannello. Per esportare i menu al menu globale, andare in *Impostazioni sistema> Applicazioni > Aspetto > Stile*, e cliccare sulla scheda "Regolazione Fine *e usare l'elenco a discesa per selezionare* solo esportazione *come proprio stile per la barra dei menu.*

#### Decorazioni delle finestre

[Le decorazioni delle finestre](http://kde-look.org/index.php?xcontentmode=75) possono essere cambiate in

```
Impostazioni di sistema -> Aspetto dello spazio di lavoro -> Decorazioni delle finestre

```

È possibile comunque scaricare direttamente ed installare i temi con un click e alcuni sono disponibili su [AUR](https://aur.archlinux.org/packages.php?O=0&K=kdestyle&do_Search=Go&PP=25&SO=d&SB=v).

#### Temi Icone

Non ci sono tanti temi per le icone di sistema disponibili per KDE 4\. E' possibile aprire *Impostazioni di sistema > Aspetto > Icone* per cercarne uno nuovo oppure installarlo manualmente. Molti temi si possono trovare su [kde-look.org](http://www.kde-look.org/).

I loghi ufficiali, icone, copertine CD e altre grafiche di Arch Linux sono disponibili nel pacchetto [archlinux-artwork](https://aur.archlinux.org/packages/archlinux-artwork/). Sopo l'installazione potete trovarli in `/usr/share/archlinux/`

#### Caratteri

##### Caratteri visivamente brutti in KDE

Provare ad installare i pacchetti [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) e [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation).

Dopo l'installazione, assicurarsi di uscire e rientrare dalla sessione. Non dovrebbe essere necessario modificare le impostazioni del pannello "Caratteri" in "Impostazioni di Sistema".

Se si è impostato manualmente il rendering dei [Fonts](/index.php/Fonts "Fonts"), prestare attenzione dal momento che le Impostazioni di Sistema possono alterare il loro aspetto. Quando si entra in *Impostazioni di Sistema > Aspetto > Caratteri*, Impostazioni di Sistema altera il file di configurazione (`fonts.conf`).

Non c'è modo di prevenirlo, ma se si imposta il valore in modo da uguagliare il file `fonts.conf`, si otterrà il rendering del font voluto (sarà richiesto di riavviare le proprio applicazioni o in alcuni casi di riavviare il proprio desktop).

Notare che pure le Preferenze dei Caratteri di Gnome ha questo comportamento, se si usano entrambi gli ambienti desktop.

##### I caratteri sono grandi o sembrano sproporzionati

Provare a forzare il DPI dei caratteri a **96** andando im *Impostazioni di sistema > Aspetto delle applicazioni > Caratteri.*

Se non dovesse funzionare, provare a impostare il valore di DPI direttamente tramite la configurazione di [Xorg](/index.php/Xorg_(Italiano)#Impostazione_manuale_DPI "Xorg (Italiano)").

#### Efficienza dello spazio di lavoro

Gli utenti che utilizzano schermi piccoli (come i Netbooks) possono cambiare alcune impostazioni per rendere più efficiente lo spazio di lavoro di KDE. Si veda [Utilizzo con schermi piccoli (es. netbook)](http://userbase.kde.org/KWin/it#Utilizzo_con_schermi_piccoli_.28es._netbook.29) per maggiori informazioni. In alternativa potete utilizzare [la modalità Plasma Netbook di KDE](http://www.kde.org/workspaces/plasmanetbook/), la quale offre un ambiente di lavoro realizzato appositamente per piccoli e leggeri dispositivi netbook.

### Networking

Potete scegliere tra i seguenti tool:

*   NetworkManager. Si veda [NetworkManager](/index.php/NetworkManager_(Italiano)#KDE4Networkmanager "NetworkManager (Italiano)") per maggiori informazioni.
*   Wicd. Si veda la pagina [Wicd](/index.php/Wicd_(Italiano) "Wicd (Italiano)") per ulteriori informazioni.

### Stampa

**Suggerimento:** Utilizzare l'interfaccia web di [CUPS](/index.php/CUPS_(Italiano) "CUPS (Italiano)") per una configurazione più rapida. Le stampanti configurate in questo modo possono essere utilizzati nelle applicazioni KDE.

Si può anche scegliere la configurazione della stampante attraverso *Impostazioni di sistema > configurazione delle stampanti*. Per poter utilizzare questo metodo, è necessario installare prima i pacchetti [kdeutils-print-manager](https://www.archlinux.org/packages/?name=kdeutils-print-manager) e [cups](https://www.archlinux.org/packages/?name=cups).

Si necessità di avviare per prima cosa il demone `avahi-daemon` e `cupsd` altrimenti incorrerete nel seguente messaggio di errore:

```
The service 'Printer Configuration' does not provide an interface 'KCModule' 
with keyword 'system-config- printer-kde/system-config-printer-kde.py' 
The factory does not support creating components of the specified type.

```

Se riscontrate il seguente errore, significa che è necessario dare i diritti utente per gestire le stampanti.

```
There was an error during CUPS operation: 'cups-authorization-canceled'

```

Per CUPS, questo viene impostato in {ic|/etc/cups/cups-files.conf}}.

Aggiungere `lp` a `SystemGroup` permette a chiunque di poter configurare una stampante. É possibile, ovviamente, aggiungere un altro gruppo al posto di `lp`.

 `/etc/cups/cups-files.conf` 
```
# Administrator user group...
SystemGroup sys root lp
```

{{Suggerimento|Si legga l'articolo [CUPS](/index.php/CUPS_(Italiano) "CUPS (Italiano)") per maggiori dettagli su come configurare CUPS.

### Supporto a Samba/Windows

Se si desidera accedere ai servizi Windows installare [Samaba](/index.php/Samba_(Italiano) "Samba (Italiano)") (pacchetto [samba](https://www.archlinux.org/packages/?name=samba)

Si possono quindi configurare le condivisioni di Samba attraverso

```
 Impostazioni di sistema -> Condivisione -> Samba

```

### Attività Desktop di KDE

Le attività Desktop di KDE sono dei set di Plasma Widget strutturati come "Desktop Virtuali" basati su Plasma, dove si possono configurare autonomamente i widget come se si avesse più di un monitor o di un desktop.

Sul proprio desktop fare clic sulla *Casella degli Strumenti* (Cashew) e sul pop-up selezionare "Attività".

Una barra di plasma verrà visualizzata nella parte inferiore dello schermo che presenterà le varie Attività Plasma-Desktop esistenti. È quindi possibile spostarsi tra loro, premendo l'icona corrispondente.

### Risparmio energetico

KDE ha un servizio di risparmio energetico integrato chiamato "**Powerdevil Power Management**" con il quale è possibile modificare il profilo di risparmio energetico del sistema e/o la luminosità dello schermo (se supportata).

Dalla versione KDE 4.6, CPU frequency scaling non è più gestito da KDE. Si presuppone che sia gestito automaticamente dal hardware e/o dal kernel. Dalla versione del kernel 3.3, Arch Linux utilizza `ondemand` come governatore predefinito per Cpufreq. Leggere attentamente il [CPU frequency scaling (Italiano)](/index.php/CPU_frequency_scaling_(Italiano) "CPU frequency scaling (Italiano)").

### Monitorare i cambiamenti su file locali e cartelle

KDE utilizza **inotify** direttamente dal kernel usando **kdirwatch** (incluso in kdelibs), in questo modo sia Gamin che FAM non sono più necessari. Si potrebbe voler installare il pacchetto [kdirwatch](https://aur.archlinux.org/packages/kdirwatch/) da AUR, si tratta di un'interfaccia grafica a kdirwatch.

## Amministrazione del Sistema

### Impostare il layout per cambiare la mappatura della tastiera

Per impostare la tastiera si vada in:

```
   Impostazioni di Sistema > Dispositivi di Immissione > Tastiera

```

Nella prima scheda potete scegliere il modello della tastiera.

Qui innanzitutto si deve scegliere il modello della propria tastiera.

Nella scheda"**Mappatura**", si può abilitare la mappatura della tastiera e scegliere la lingua desiderata, semplicemente cliccando sul tasto "Aggiungi mappatura".

Nella scheda "**Avanzate**", è possibile scegliere la combinazione di tasti da utilizzare per modificare la mappatura della tastiera presente nel sotto menù "Scorciatoie per cambiare la mappatura".

### Terminare Xorg-server attraverso le impostazioni di sistema di KDE

Si vada nel sottomenu:

```
   Impostazioni di Sistema > Dispositivi di Immissione > Tastiera > (Scheda) Avanzate > Sotto-menu "Sequenza dei tasti per terminare il server X"

```

Spuntare l'opzione e premere su "Applica".

### Moduli kcm utili

KCM significa **KC**onfig **M**odule. Questi moduli possono aiutare a configurare il vostro sistema fornendo una interfaccia in Impostazioni di sistema.

**Configurare l'aspetto delle applicazioni gtk.**

*   [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config)
*   [kcm-gtk](https://aur.archlinux.org/packages/kcm-gtk/)
*   [kcm-qt-graphicssystem](https://aur.archlinux.org/packages/kcm-qt-graphicssystem/)

**Configurare il bootloader GRUB**

*   [grub2-editor](https://aur.archlinux.org/packages/grub2-editor/)
*   [kcm-grub2](https://aur.archlinux.org/packages/kcm-grub2/)

**Configurare il driver Synaptics per il touchpad.**

*   [synaptiks](https://aur.archlinux.org/packages/synaptiks/)
*   [kcm_touchpad](https://aur.archlinux.org/packages/kcm_touchpad/)

**Configurare il Firewall [Uncomplicated Firewall](/index.php/Uncomplicated_Firewall "Uncomplicated Firewall") (UFW)**

*   [kcm-ufw](https://aur.archlinux.org/packages/kcm-ufw/)

**Configurazioni per [PolicyKit](/index.php/PolicyKit "PolicyKit")**

*   [kcm-polkit-kde-git](https://aur.archlinux.org/packages/kcm-polkit-kde-git/)

**Configurazioni per tavolette Wacom**

*   [kcm-wacomtablet](https://aur.archlinux.org/packages/kcm-wacomtablet/)

Altri KCM possono essere trovati in [kde-apps.org](http://kde-apps.org/index.php?xcontentmode=273).

## Ricerca Desktop e Desktop Semantico

Secondo [Wikipedia](https://en.wikipedia.org/wiki/Semantic_desktop "wikipedia:Semantic desktop"), "*il Desktop Semantico è un termine che si riferisce a idee e metodi per modificare l'interfaccia utente di un computer e gestione in modo nuovo i dati, in modo che tali dati siano più facilmente condivisi tra le diverse applicazioni o le attività e capaci di essere elaborati automaticamente."*

L'implementazione di KDE di questo concetto è legato (come di KDE 4.10) a due grandi pezzi di software, Akonadi e Nepomuk. Tra di loro, questi programmi permettono di guardare i propri dati e creare un indice facilmente consultabile di esso. L' idea alla base di questi software è quello di rendere il vostro sistema di "conoscenza" dei propri dati e darne contesto usando metadati e tag forniti dall'utente.

Soprano e Virtuoso sono due dipendenze del Nepomuk Semantic Desktop. Dal momento che il rapporto tra le due componenti principali e le loro dipendenze non è molto chiaro, le seguenti sezioni cercheranno di far luce sul loro funzionamento interno.

### Virtuoso e Soprano

Il database utilizzato per memorizzare tutti i metadati utilizzati dal desktop semantico è un database '[Resource Description Framework (RDF)](https://en.wikipedia.org/wiki/Resource_Description_Framework "wikipedia:Resource Description Framework") *chiamato Virtuoso. Internamente, Virtuoso può essere considerato come un database relazionale. (Un [relational database](https://en.wikipedia.org/wiki/Relational_model "wikipedia:Relational model") è diverso da un database tradizionale basato su una singola tabella, nel senso che utilizza più tabelle correlate da un singolo tasto per memorizzare i dati). Esso è attualmente controllata da OpenLink, ed è disponibile sia sotto licenza commerciale, sia sotto licenza open source.*

Tratto da [KDE Techbase](http://techbase.kde.org/Projects/Nepomuk/ComponentOverview#Soprano), *Soprano è una astrazione Qt che lavora sulle banche dati. Fornisce un'API amichevole basata sulle QT per l'accesso a diversi dati RDF. Attualmente supporta 3 backend di database - Sesame, Redland e Virtuoso . Lo Stack Semantico di KDE funziona solo con Virtuoso. Soprano offre inoltre funzionalità aggiuntive come la serializzazione, l'analisi dei dati RDF, e una architettura client-server che viene molto utilizzato in Nepomuk.*

### Nepomuk

Nepomuk è l'acronimo di "Networked Environment for Personal, Ontology-based Management of Unified Knowledge". Nepomuk è ciò che permette agli utenti la marcatura e l'etichettatura dei file, nonche di come siano posizionati. Inoltre serve anche a leggere effettivamente il database Virtuoso. Esso fornisce una API per gli sviluppatori di applicazioni che permettono di leggere i dati raccolti da esso.

In passato , il servizio "Strigi" è stato utilizzato per raccogliere i dati sui vari file presenti sul sistema. Tuttavia, a causa di molte ragioni , la più importante delle quali è l'utilizzo di CPU e della memoria, Strigi è stato sostituito da un servizio di indicizzazione interno che è integrato con Nepomuk-Core.

Per ulteriori informazioni su Nepomuk [questa pagina](http://techbase.kde.org/Projects/Nepomuk/ComponentOverview#Nepomuk_Components) è un'ottima risorsa. Tuttavia, alcune delle informazioni nella pagina precedente è stato reso obsoleto secondo [questo post](http://vhanda.in/blog/2012/11/nepomuk-without-strigi/).

#### Utilizzare e configurare Nepomuk

Per utilizzare la ricerca usando Nepouk sul desktop KDE, premere `ALT+ F2` e digitare la query. Nepomuk è abilitato di default. Può essere attivato e disattivato in

```
Impostazioni di Sistema -> Ricerca Desktop

```

Nepomuk è in grado di mantenere la traccia di un numero elevato di file e perciò si raccomanda di aumentare il numero di file che possono essere osservati con inotify, per fare ciò:

```
# sysctl fs.inotify.max_user_watches=524288

```

Per renderlo persistente:

```
# echo "fs.inotify.max_user_watches = 524288" >> /etc/sysctl.d/99-inotify.conf

```

Riavviare Nepomuk per vederne i cambiamenti.

#### KDE senza Nepomuk

Se si desidera eseguire KDE senza Nepomuk , esiste il pacchetto [nepomuk-core-fake](https://aur.archlinux.org/packages/nepomuk-core-fake/) su AUR.

**Attenzione:** A partire da ora , Dolphin dipende da [nepomuk-widgets](https://aur.archlinux.org/packages/nepomuk-widgets/) e quindi si romperà se utilizzato con il pacchetto Nepomuk-fake

### Akonadi

Akonadi è un sistema destinato a funzionare da cache locale per dati PIM, indipendentemente dalla sua origine, che può essere poi usata da altre applicazioni. Questo include e-mail dell'utente, contatti, calendari, riviste, eventi, allarmi, note e così via. Si interfaccia con le librerie Nepomuk per fornire capacità di ricerca .

Akonadi non memorizza i dati di per sé : il formato di memorizzazione dipende dalla natura dei dati (per esempio, i contatti possono essere memorizzati in formato vCard ).

Per ulteriori informazioni su Akonadi e il suo rapporto con Nepomuk, vedere [[3]](http://blogs.kde.org/node/4503) e [[4]](http://cmollekopf.wordpress.com/2013/02/13/kontact-nepomuk-integration-why-data-from-akonadi-is-indexed-in-nepomuk/).

#### Disabilitare Akonadi

Si veda l'apposita sezione nel [manuale utente di KDE](http://userbase.kde.org/Akonadi/it#Disattivare_il_sottosistema_Akonadi).

#### Configurare il database

Avviare `akonaditray` incluso nel pacchetto [kdepim-runtime](https://www.archlinux.org/packages/?name=kdepim-runtime), cliccare col tasto destro sull'icona e selezionare **configura**. Nella scheda di configurazione del server Akonadi potrete:

*   Configurare Akonadi per utilizzare un server MySQL/MariaDB in esecuzione sul sistema.
*   Configurare Akonadi per utilizzare un server SQLite
*   Configurare Akonadi per utilizzare un server PostgreSQL

#### Esecuzione di KDE senza Akonadi

Il pacchetto [akonadi-fake](https://aur.archlinux.org/packages/akonadi-fake/) è una buona opzione per coloro che desiderano eseguire KDE senza Akonadi.

## Phonon

### Cos'è Phonon ?

Da [Wikipedia](https://en.wikipedia.org/wiki/it:Phonon "wikipedia:it:Phonon"):

*Phonon è l'API multimediale di KDE 4\. Phonon è stato creato per permettere a KDE 4 di essere indipendente da qualsiasi framework multimediale come GStreamer oppure xine e per fornire delle API stabili per la durata di vita di KDE 4\. E' stato creato per varie ragioni: per creare una semplice API multimediale con stile KDE/Qt, per supportare meglio i framework multimediali nativi su Windows e Mac OS X, e per risolvere i problemi dei framework non più mantenuti o con API e ABI instabili.*

**Phonon** è usato largamente in KDE, sia per le applicazioni audio (come ad esempio le notificazioni di sistema o gli applicativi audio di KDE) sia per quelle video (come ad esempio l'anteprima video di Dolphin).

### Quale backend si dovrebbe scegliere?

Si possono utilizzare diversi backend come [GStreamer](/index.php/GStreamer "GStreamer") ([phonon-qt4-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt4-gstreamer)) e [VLC](/index.php/VLC "VLC") ([phonon-qt4-vlc](https://www.archlinux.org/packages/?name=phonon-qt4-vlc)) disponibili nei [Depositi Ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)"), mentre QuickTime ([phonon-quicktime-git](https://aur.archlinux.org/packages/phonon-quicktime-git/)), e [AVKode](http://martinsandsmark.wordpress.com/2012/07/07/akademy/) ([phonon-avkode-git](https://aur.archlinux.org/packages/phonon-avkode-git/)) sono reperibili su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").

La maggior parte degli utenti preferisce GStreamer o VLC, poiché sono maggiormente supportati. Si noti che possono essere installati più backend in una sola volta, e sceglierne uno in *Impostazioni di Sistema > Multimedia > Phonon > Backend*.

**Nota:**

*   In relazione alla [Feature Matrix](http://community.kde.org/Phonon/FeatureMatrix), il backend GStreamer ha alcune caratteristiche in più rispetto al backend VLC.
*   Come annunciato in [KDE UserBase](http://userbase.kde.org/Phonon#Backend_libraries), Phonon-MPlayer non è attualmente mantenuto.

## Applicazioni utili

Il set ufficiale di applicazioni KDE possono essere trovato [qui](http://www.kde.org/applications/).

### Yakuake

[Yakuake](/index.php/Yakuake "Yakuake") fornisce un emulatore di terminale in stile Quake, che viene attivata e resa visibile utilizzando il tasto `F12`. Yakuake supporta schede multiple e può essere installato con il pacchetto [yakuake](https://www.archlinux.org/packages/?name=yakuake).

### KDE Telepathy

[KDE Telepathy](http://community.kde.org/KTp) è un progetto con l' obiettivo di integrare strettamente Instant Messaging con il desktop KDE . Utilizza il framework Telepathy come back-end, ed è destinato a sostituire Kopete .

Per avere tutti i protocolli disponibili per Telepathy, installare il gruppo [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/). Per usare il client Telepathy per KDE, installare il pacchetto [kde-telepathy-meta](https://www.archlinux.org/packages/?name=kde-telepathy-meta) che include tutti i pacchetti presenti nel gruppo [kde-telepathy](https://www.archlinux.org/groups/x86_64/kde-telepathy/).

## Trucchi e Consigli

### Utilizzare Openbox in KDE

**Suggerimento:** Il gestore delle finestre nativo per KDE è `kwin`.

Il gestore delle finestre [Openbox](/index.php/Openbox_(Italiano) "Openbox (Italiano)") opera molto bene all'interno di KDE, combinato con un miglioramento significativo della prestazioni e della reattività. Per impostazione predefinita, una sessione `KDE/Openbox` sessione sarà reso automaticamente disponibile dopo l'installazione di Openbox, anche se l'ambiente KDE stesso non è stato installato. La maggior parte dei display manager popolari permetteranno dunque di avviare KDE con Openbox come window manager e di essere selezionato come una sessione.

Per avviare manualmente KDE con Openbox come window manager - come sessione predefinita per [SLiM](/index.php/SLiM "SLiM"), o se non si utilizza un display manager - aggiungere il seguente comando al file [Xinitrc](/index.php/Xinitrc_(Italiano) "Xinitrc (Italiano)") :

```
exec openbox-kde-session

```

#### Riattivare gli effetti del compositing

Qualora si sostituisce il nativo gestore delle finestre `KWin` con Openbox , eventuali effetti di composite del desktop - come la trasparenza - saranno persi. Questo perché Openbox stesso non fornisce alcuna funzionalità di composite. Tuttavia, è facilmente possibile utilizzare un programma di compositing separato per [[Openbox#Compositing_effects | riattivare compositing ] ].

### Integrare Android con il desktop KDE

Installare [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect) e [KDE Connect](https://play.google.com/store/apps/details?id=org.kde.kdeconnect_tp) dal Play Store per una miglior integrazione tra Android e KDE.

### Ricevere le notifiche per gli aggiornamenti software

Installare [apper](https://www.archlinux.org/packages/?name=apper) per ottenere le notifiche sugli aggiornamenti dei pacchetti nella barra delle applicazioni di KDE e di una GUI semplice per la gestione dei pacchetti. Vedere il [PackageKit sito](http://www.packagekit.org) per ulteriori informazioni.

### Configurare KWin per utilizzare le OpenGL ES

A partire dalla versione 4,8 di KWin è possibile utilizzare i binari compilati separatamente per poter utilizzare **kwin_gles** in sostituzione di KWin. Esso si comporta quasi come l'eseguibile kwin in modalità OpenGL2, con la leggera differenza che utilizza *egl* anziché *glx* come l'interfaccia della piattaforma nativa. Per testare kwin_gles è sufficiente eseguire `kwin_gles --replace` in Konsole.

se volete rendere questo cambiamento permanente dovete create uno script in `$(kde4-config --localprefix)/env/` che esporti `KDEWM=kwin_gles`.

### Abilitare le anteprime audio/video nei file manager Konqueror e Dolphin

Per usufruire delle anteprima audio nei file manager Konqueror e Dolphin, installare il pacchetto [audiothumbs](https://aur.archlinux.org/packages/audiothumbs/) da AUR.

Per avere le anteprime dei video in konqueror e dolphin, installare [kdemultimedia-mplayerthumbs](https://www.archlinux.org/packages/?name=kdemultimedia-mplayerthumbs) o [ffmpegthumbs](https://www.archlinux.org/packages/?name=ffmpegthumbs).

### Velocizzare l'avvio delle applicazioni

L'utente Rob ha scritto nel suo blog questo "[magic suggerimento](http://kdemonkey.blogspot.nl/2008/04/magic-trick.html)" per migliorare l'avvio delle applicazioni di 50-150ms.

Per abilitarlo basta creare la seguente cartella nella propria home:

```
$ mkdir -p ~/.compose-cache

```

**Nota:** Per chi fosse curioso di quello che si è fatto, questo permette una ottimizzazione che Lubos ha introdotto tempo fa e che, riscritta, è stata integrata in libx11\. Normalmente allo startup le applicazioni leggono le informazioni sui metodi di input da `/usr/share/X11/locale/<your locale>/Compose`. Questo file è veramente lungo (>5000 linee per il file en_US.UTF-8) e ci vuole tempo perché venga processato. Libx11 può creare una cache delle informazioni parsate che sia più veloce da leggere sequenzialmente, ma sarà in grado di riutilizzare una cache esistente o crearne una nuova in `~/.comporre-cache` solo se la directory esiste già.

### Nascondere partizioni

In Dolphin, si effettua semplicemente cliccando col tasto destro su un `dispositivo` nella barra laterale e selezionare `Nascondi *dispositivo*`, altrimenti...

Se si desidera prevenire la comparsa delle partizioni interne nel proprio file manager, è possibile creare una regola di udev:

 `/etc/udev/rules.d/10-local.rules`  `KERNEL=="sda[0-9]", ENV{UDISKS_IGNORE}="1"` 

La stessa cosa per una partizione specifica:

```
KERNEL=="sda1", ENV{UDISKS_IGNORE}="1"
KERNEL=="sda2", ENV{UDISKS_IGNORE}="1"

```

### Suggerimenti per Konqueror

#### Disabilitare i Tooltips (Browser)

Per disabilitare questa piccola chiave per i tooltips in Konqueror (alla pressione di `CTRL` su una pagina web), andare in *Impostazioni > Configura Konqueror > Navigazione Web* e deselezionare *Abilita l'attivazione attraverso il tasto CTRL dei tasti di accesso*, oppure

 `~/.kde4/share/config/konquerorrc` 
```
[Access Keys]
 Enabled=false
```

#### Usare WebKit

É possibile utilizzare WebKit in konqueror al posto di KHTML, per prima cosa installare il pacchetto [kwebkitpart](https://www.archlinux.org/packages/?name=kwebkitpart).

Quindi dopo aver eseguito Konqueror, si prema *Impostazioni > Configura Konqueror*, navigare nel sotto-menù *Generale*, e si selezioni `WebKit` come *Motore di base del browser web*.

### Integrazione di Firefox

Vedere l'articolo [Firefox](/index.php/Firefox#KDE_integration "Firefox").

### Impostare lo sfondo del LockScreen per avere lo stesso sfondo del desktop

Lo sfondo di Kscreensaver può essere cambiato da quello predefinito.

KDE [non è abilita](https://bugs.kde.org/show_bug.cgi?id=312828) il cambiamento dello sfondo per la schermata del lockscreen, ma un [workaround](http://lists.opensuse.org/opensuse-kde/2013-02/msg00082.html) [esiste](http://forum.kde.org/viewtopic.php?f=66&t=110039):

 `/usr/share/apps/ksmserver/screenlocker/org.kde.passworddialog/contents/ui/` 
```
[...]
        *#source: theme.wallpaperPathForSize(parent.width, parent.height)*
        source: "1920x1080.jpg"
[...]

```

Ora si copi l'immagine di sfondo corrente come `"1920x1080.jpg "`.

Nota È necessario ripetere questa operazione per ogni aggiornamento del pacchetto [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/).

### Impostare l'immagine del lockscreen ad una arbitraria

Copiare un profilo wallpaper esistente come modello :

```
$ cp -r /usr/share/wallpapers/*ExistingWallpaper* ~/.kde4/share/wallpapers/

```

Modificare il nome della directory , e modificare `metadata.desktop`:

 `~/.kde4/share/wallpapers/*MyWallpaper*/metadata.desktop` 
```
[Desktop Entry]
Name=MyWallpaper
X-KDE-PluginInfo-Name=MyWallpaper
```

Rimuovere l'immagine esistente (`contents/screenshot.png` e `images/*`) :

```
$ rm ~/.kde4/share/wallpapers/MyWallpaper/contents/screenshot.png
$ rm ~/.kde4/share/wallpapers/MyWallpaper/contents/images/*

```

Copiare la nuova immagine :

```
$ cp *path/to/MyWallpaper.png* MyWallpaper/contents/images/1920x1080.png

```

Modificare il profilo di metadati per il tema corrente :

 `~/.kde4/share/apps/desktoptheme/MyTheme/metadata.desktop` 
```
[Wallpaper]
defaultWallpaperTheme=MyWallpaper
defaultFileSuffix=.png
defaultWidth=1920
defaultHeight=1080
```

Bloccare lo schermo per verificarne il funzionamento.

**Nota:** Questo metodo imposta lo sfondo per il lockscreen senza modificare le impostazioni a livello di sistema. Per un cambiamento a livello di sistema , creare un nuovo profilo wallpaper in `/usr/share/wallpapers`.

## Risoluzione dei problemi

### Correlati alla configurazione

Molti problemi in KDE sono legate alla configurazione. Quindi si consiglia di verificare con la configurazione predefinita.

#### Ripristinare tutte le configurazioni di KDE

Per verificare se la propria configurazione sia il problema, provare ad uscire dalla vostra sessione di KDE e, in un terminale, eseguire

```
$ cp ~/.kde4 ~/.kde4.safekeeping
$ rm .kde4/{cache,socket,tmp}-$(hostname)

```

Il comando *rm* rimuoverà solo i collegamenti simbolici che verranno ricreati automaticamente da KDE. Ora inizia una nuova sessione di KDE per vedere i risultati.

Se il problema viene risolto, si avrà un nuovo e senza problemi `~/.Kde4`. Gradualmente è possibile spostare le parti della precedente configurazione salvata, riavviare la sessione regolarmente per effettuare un test, e per identificare le parti problematiche della vostra configurazione. Alcuni file qui sono chiamati dopo le applicazioni in modo che si sarà probabilmente in grado di testare questi senza dover riavviare KDE.

#### Il servizio di indicizzazione dei file non funziona anche dopo aver abilitato tutto correttamente

Ciò è dovuto a causa di un database di Nepomuk danneggiato. Esso può essere sanato spostando il database o leliminandolo del tutto. Uscire da KDE e scrivere questo comando da una console virtuale:

```
 $ mv ~/.kde4/share/apps/nepomuk ~/.kde4/share/apps/nepomuk_backup

```

per spostare il vostro del database Nepomuk esistente (e corrotto). Esso verrà ricreato quando si accede nuovamente .

#### Il desktop Plasma si comporta stranamente

I problemi di Plasma sono causati principalmente da **plasmoidi** instabili o **temi di plasma**. Innanzitutto, si cerchi di risalire all'ultimo plasmoide o tema di plasma installato e lo si disabiliti oppure lo si rimuova direttamente.

Quindi, se il vostro desktop si chiude improvvisamente, questo è probabilmente causato da un problema relativo ad un widget installato. Se non si riesce a ricordare quale widget è stato installato prima che il problema ha cominciato a presentarsi (a volte può essere un problema irregolare), cercare di rintracciarlo, eliminando ogni widget finché il problema non cessa. Quindi è possibile disinstallare il widget problematico, ed effettuare un bug report (bugs.kde.org) **solo se si tratta di un widget ufficiale**. Se non lo è, si consiglia di segnalare il problema sulla voce relativa al plasmoide incriminato su kde-look.org e informare gli sviluppatori sulla questione (dettagliando i passi per riprodurre, ecc.).

Se non si riesce a risalire al problema, e non si vuole perdere tutte le configurazioni di KDE, si dia:

```
 $ rm -r ~/.kde4/share/config/plasma*

```

Questo comando **cancellerà tutte le configurazioni di plasma** dell'utente e quando si effettuerà nuovamente il login in KDE, si avranno di nuovo le impostazioni di **default**. Si deve sapere che questa azione **non può essere annullata**. Si dovrebbe creare una cartella di backup e copiarci tutti i file di configurazione di plasma.

#### Pulire la cache per risolvere i problemi di aggiornamento

Il [problema](https://bbs.archlinux.org/viewtopic.php?id=135301) potrebbe essere causato dalla vecchia cache. A volte dopo un aggiornamento, la vecchia cache potrebbe introdurre dei problemi, difficoltà ad eseguire il debug di un comportamento, come una shell non killabile, problemi di blocco quando si cambiano varie impostazioni, e vari altri problemi, come ark che non è più in grado di utilizzare unrar o unzip, oppure Amarok non riconosce più le proprie musiche.

Questa soluzione può anche risolvere i problemi con i programmi KDE e QT che si visualizzano male dopo un aggiornamento.

Ricostruire la cache con i seguenti comandi :

```
$ rm ~/.config/Trolltech.conf
$ kbuildsycoca4 --noincremental

```

Speriamo che i vostri problemi siano ora risolti.

### Pulire al configurazione di Akonadi per ripristinare Kmail

In primo luogo , assicurarsi che KMail non sia in esecuzione. Poi effettuare un backup delle configurazioni :

```
$ mv ~/.local/share/akonadi  ~/.local/share/akonadi-old
$ mv ~/.config/akonadi ~/.config/akonadi-old

```

Andare in `Impostazioni di Sistema -> Informazioni Personali` e rimuovere tutte le risorse. Poi da Dolphin eliminare le cartelle originali `~/.local/share/akonadi` e `~/.config/akonadi` per cui si è fatto il backup.

Ora ritornare in `Impostazioni di Sistema -> Informazioni Personali` e con attenzione aggiungere le risorse desiderate. Si dovrebbe vedere la risorse in lettura delle cartelle di posta. Quindi avviare Kmail/Kontact per verificare il corretto funzionamento.

### Come ottenere informazioni sullo stato di KWin per il supporto e il debug

Questo comando stampa una meravigliosa sintesi dello stato attuale di KWin comprese le opzioni utilizzate , backend del compositing utilizzati e le relative funzionalità dei driver OpenGL. [Si veda il blog di Martin](http://blog.martin-graesslin.com/blog/2012/03/on-getting-help-for-kwin-and-helping-kwin/).

```
qdbus org.kde.kwin /KWin supportInformation

```

### KDE4 non termina il caricamento

Ci potrebbe essere una situazione in cui il driver grafico potrebbe creare un conflitto all'avvio di KDE4\. Questa situazione si verifica dopo il login, ma prima di terminare il caricamento del desktop, rendendo l'utente ad attendere all'infinito la schermata che termini la schermata di caricamento. Fino ad ora gli unici utenti che hanno confermato di essere colpiti da questo problema utilizzano driver [Nvidia](/index.php?title=Nvidia_(Italiano)&action=edit&redlink=1 "Nvidia (Italiano) (page does not exist)") e KDE4.

Una soluzione per gli utenti Nvidia è :

 `~/.kde4/share/config/kwinrc` 
```
[Compositing]
Enabled=false
```

Per ulteriori informazioni consultare questa [discussione](https://bbs.archlinux.org/viewtopic.php?pid=932598).

Se si è effettuata una installazione minimale di KDE, assicurarsi di installare il font richiesto dal vostro backend phonon, come elencato elencato [qui](#Installazione_minimale)

### KDE ed i programmi in Qt vengono visualizzati in maniera errata con gestori di finestre differenti

Se si stanno utilizzando programmi di KDE o Qt ma non in una sessione di KDE (in maniera specifica, non è stato lanciato `startkde`, allora, a partire da KDE 4.6.1 sarà necessario istruire Qt affinché trovi gli stili di KDE (Oxygen, QtCurve ecc.)

È necessario solamente impostare la variabile d'ambiente `QT_PLUGIN_PATH`. Ad esempio mettere

```
export QT_PLUGIN_PATH=$HOME/.kde4/lib/kde4/plugins/:/usr/lib/kde4/plugins/

```

nel proprio `/etc/profile` (o in `~/.profile` nel caso non si abbia accesso root). qtconfig dovrebbe essere quindi in grado di trovare gli stili di kde e la visualizzazione dovrebbe tornare perfetta!

In alternativa si può creare un link simbolico degli stili di KDE nella directory degli stili utilizzati da QT:

```
# ln -s /usr/lib/kde4/plugins/styles/ /usr/lib/qt/plugins/styles

```

Sotto Gnome si può provare a installare il pacchetto libgnomeui.

### Problemi legati all'aspetto grafico

#### Performance desktop 2D scadenti (o) appaiono Artefatti durante il 2D

##### Problema con i driver GPU

Assicurarsi di aver installato il driver corretto per la propria scheda video, in modo tale che il desktop abbia almeno l'accelerazione 2D. Si seguino questi articoli per maggiori informazioni: [ATI](/index.php/ATI_(Italiano) "ATI (Italiano)"), [NVIDIA](/index.php/NVIDIA_(Italiano) "NVIDIA (Italiano)"), [Intel](/index.php/Intel_(Italiano) "Intel (Italiano)"), in modo tale da essere sicuri che tutto sia configurato per il meglio. I driver open ATI e Intel e i driver proprietari Nvidia dovrebbero assicurare teoricamente la miglior accelerazione 2D e 3D.

##### Utilizzare il motore Raster

Se questo non risolve i problemi, forse il driver non fornisce una buona accelerazione **XRender** che è l'attuale motore grafico su cui Qt si basa di default.

È possibile modificare il motore grafico basandolo solo su un uso software invocando l'applicazione con la linea di comando `raster-graphicssystem`. Questo motore di rendering può essere impostato come quello di default ricompilando Qt con la stessa opzione di configurazione, `-graphicssystem raster`.

Il motore di rendering raster permette alla CPU di eseguire la maggior parte della grafica, sottraendo tale carico dalla GPU. In questo modo è possibile ottenere prestazioni migliori, a seconda del vostro sistema. Questo è fondamentalmente un work-around per i driver stack non performanti su Linux, dato che la CPU non dovrebbe, ovviamente, fare calcoli grafici visto che è progettata per un numero di threads di maggiore complessità, rispetto alla GPU, che seppur elabora molti thread questi sono di minore potenza di calcolo. Quindi, utilizzare il motore Raster solo se si hanno problemi o la propria GPU è molto più lenta della CPU, altrimenti è meglio utilizzare XRender.

Dalla versione Qt 4.7 e successive, la ricompilazione di Qt non è necessaria. Basta utilizzare `QT_GRAPHICSSYSTEM=raster`, `opengl`, o `native` (per quello di base). Raster dipende della CPU, *OpenGL* dipende dalla GPU e necessita di un ottimo supporto dei driver, mentre *native* semplicemente utilizza il rendering X11 (solitamente misto).

**Il miglior modo per automizzare tutto quanto** è installare [kcm-qt-graphicssystem](https://aur.archlinux.org/packages/kcm-qt-graphicssystem/) da AUR e configurare questa particolare impostazione di Qt attraverso:

```
 Impostazioni di Sistema > Qt Graphics System

```

Per maggiori informazioni consultare [KDE Developer blog entry](http://apachelog.wordpress.com/2010/09/05/qt-graphics-system-kcm/) e/o questo [Qt Developer blog entry](http://labs.trolltech.com/blogs/2009/12/18/qt-graphics-and-performance-the-raster-engine/).

#### Performance 3D scadenti

KDE si avvia con gli effetti desktop attivi. Le schede video più vecchie potrebbero non essere adatte per l'accelerazione desktop 3D. Si possono disabilitare gli effetti in

```
Impostazioni di Sistema > Effetti Desktop 

```

e si possono disabilitare con `Alt+Shift+F12`

**Nota:** Si potrebbero incontrare problemi con le performance desktop 3D anche usando una scheda video più potente, ma usando i driver proprietari catalyst (`fglrx`). Questi driver sono conosciuti per avere problemi con l'accelerazione 3D. Si veda [la pagina del Wiki ATI](/index.php/ATI "ATI") per la risoluzione dei problemi.

#### Il Composite per il Desktop è disabilitato con una recente schede video Nvidia

Talvolta, KWin potrebbe avere delle impostazioni nel suo file di configurazione (`kwinrc`) che *possono causare* un problema di riattivazione del composite `OpenGL` per il desktop 3D. Questo problema si presenta casualmente (ad esempio a causa di un crash improvviso di Xorg o di un semplice riavvio del sistema, che corrompe il file), se ciò accadesse, cancellare il file `~/.kde4/share/config/kwinrc` e ri-effettuare il login. In questo modo KWin genererà un nuovo file con impostazioni predefinite di KDE ed il problema dovrebbe risolversi.

#### Tremolio in fullscreen quando il Composite è attivato

A partire da KDE SC 4.6.0, c'è un'opzione in *Impostazioni di Sistema -> Effetti Desktop -> Avanzate -> Sospendi gli effetti desktop per le finestre a schermo intero".* Deselezionandolo si dirà a kwin di disabilitare lo schermo intero indiretto.

#### Tearing dello schermo con gli effetti desktop abilitati

**Nota:** Con il recente aggiornamento di KDE alla versione 4.11, sono state aggiunte diverse nuove opzioni per il Vsync, che possono aiutare con il problema del tearing.

KWin può soffrire di screen tearing, mentre gli effetti desktop sono abilitati. Deselezionare l'opzione VSync in Impostazioni di Sistema > Effetti Desktop > Avanzate > "Usa Vsync ".

Per gli utenti che utilizzano driver proprietari, assicurarsi che l'opzione VSync sia abilitata ( amdccle per gli utenti [Catalyst](/index.php/AMD_Catalyst_(Italiano) "AMD Catalyst (Italiano)") e nvidia-settings per gli utenti [Nvidia](/index.php/NVIDIA_(Italiano) "NVIDIA (Italiano)")).

#### Impostazioni di visualizzazione perse al riavvio (monitor multipli)

Installare il pacchetto [kscreen](https://www.archlinux.org/packages/?name=kscreen) potrebbe risolvere il problema a meno che i vostri schermi condividono lo stesso EDID. Kscreen è il migliore software di gestione dello schermo per KDE, ulteriori informazioni possono essere trovate [qui](https://fedoraproject.org/wiki/Changes/KScreen?rd=Features/KScreen).

### Problemi sonori in KDE

#### Problemi legati ad ALSA

**Nota:** Assicurarsi innanzitutto d'aver installato [alsa-lib](https://www.archlinux.org/packages/?name=alsa-lib) e [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils).

##### Comparsa di messaggi "Falling back to default" quando si prova ad ascoltare qualsiasi suono in KDE

Quando si incontrano questi messaggi:

	Il device di riproduzione audio *nome_del_dispositivo_sonoro* non funziona.

	Per ripristinare quello di default

Si vada in

```
Impostazioni di Sistema > Multimedia -> Phonon

```

e si imposti il device chiamato `default` prima di tutti gli altri device in ogni opzione disponibile.

##### Non riesco a riprodurre file MP3 quando imposto come backend Gstreamer in Qt Phonon

Si può risolvere installando i gstreamer plugins (pacchetto [gstreamer0.10-plugins](https://www.archlinux.org/groups/x86_64/gstreamer0.10-plugins/)). Se si dovessero incontrare altri problemi, si potrebbe provare a cambiare il backend utilizzato da Phonon, installandone un altro come [phonon-qt4-vlc](https://www.archlinux.org/packages/?name=phonon-qt4-vlc)

L'odine di preferenza del backend può essere cambiato in:

```
 Impostazioni di Sistema -> Multimedia -> Phonon -> (finestra) Backend

```

### Konsole non salva la lista dei comandi

Di base la storia dei comandi nella console viene salvata solamente quando si digita 'exit' nella console. Quando si chiude la Konsole con il bottone 'x' nell'angolo ciò non acccade. Per abilitare il salvataggio automatico dopo ogni esecuzione di comandi :

 `~/.bashrc` 
```
 shopt -s histappend
 [[ "${PROMPT_COMMAND}" ]] && PROMPT_COMMAND="$PROMPT_COMMAND;history -a" || PROMPT_COMMAND="history -a"

```

### Le password in KDE mostrano tre pallini per ogni lettera

Potete cambiare questo comportamento andando in **Impostazioni di Sistema > Dettagli dell'Account**. Alla voce **Password e account utente** sono disponibili tre opzioni:

*   Mostra un punto per ogni lettera
*   Mostra tre punti per ogni lettera
*   Non mostrare nulla

### Il processo di Nepomukserver si avvia automaticamente anche se il desktop semantico è disabilitato

Andare in ' *Impostazioni di Sistema > Avvio e spegnimento > Service Manager > Gestione dei servizi* e spuntare la voce relativa al "Modulo di ricerca di Nepomuk".

### Dolphin e le finestre di dialogo sono estremamente lente ad inizializzarsi ogni volta

Può essere causato dal servizio upower. Se il servizio upower non è necessaria per il vostro sistema, può essere disabilitata :

```
# systemctl disable upower
# systemctl mask upower

```

Ovviamente questo non avrà nessun effetto collaterale su un sistema desktop.

### Visualizzatore PDF di default nelle applicazioni GTK sotto KDE

In alcuni casi, quando si installano [Inkscape](/index.php/Inkscape "Inkscape"), [GIMP](/index.php/GIMP "GIMP") o altri programmi di elaborazione grafica, le applicazioni GTK ([Firefox](/index.php/Firefox_(Italiano) "Firefox (Italiano)") ad esempio) potrebbero non selezionare più Okular come il visualizzatore PDF di default, e non seguiranno le impostazioni di KDE circa le applicazioni di default. Il seguente comando utente può essere usato per ripristinare Okular come default per i PDF.

```
$ xdg-mime default kde4-okularApplication_pdf.desktop application/pdf

```

Se si sta usando un visualizzatore PDF diverso, o questo comportamento scorretto è generato da un diverso mime-type, è necessario sostituire nel comando precedente `kde4-okularApplication_pdf.desktop` e `application/pdf` rispettivamente in modo che seguano le proprie necessità.

Per maggiori informazioni, si può consultare [questa pagina](/index.php/Default_applications "Default applications").

## Versione KDE instabile

Quando KDE raggiunge la versione beta o RC milestone (.90), i pacchetti di KDE "unstable" vengono caricati nel repositorio chiamato [kde-unstable], e lì vi rimangono fino a quando KDE viene dichiarato stabile, successivamente passano nel repositorio [extra].

Si può aggiunge [kde-unstable] con:

 `/etc/pacman.conf` 
```
[kde-unstable]
 Include = /etc/pacman.d/mirrorlist
```

1.  kde-unstable è basato su testing. Pertanto è necessario abilitare i repositori nel seguente ordine: [kde-unstable], [testing], [core], [extra], [community-testing], [community].

1.  Per aggiornare da una installazione precedente di KDE, eseguire: `pacman -Syu` oppure `pacman -S kde-unstable/kde`

1.  Se non avete installato KDE, potreste avere difficoltà a installarlo utilizzando i gruppi (limitazione di pacman)

1.  **Iscrivetevi e leggete la [arch-dev-public](https://mailman.archlinux.org/pipermail/arch-dev-public/) mailing list**

1.  Controllare [segnalare un bug](#Segnalazione_di_bug_relativi_a_Distro_e_Upstream) se si incontra qualche problema.

## Altri progetti su KDE =

### Trinity

Dal rilascio di KDE 4.x , gli sviluppatori hanno cessato il supporto per KDE 3.5.x. Trinity Desktop Environment è un fork di KDE3 sviluppato da Timothy Pearson ([trinitydesktop.org](http://trinitydesktop.org/)) . Questo progetto mira a mantenere lo stile di elaborazione KDE 3.5 vivo , così come rispolverare eventuali asperità che erano presenti come in KDE 3.5.10\. Vedi [Trinity](/index.php/Trinity "Trinity") per ulteriori informazioni .

Trinity Desktop Environment is a fork of KDE3 developed by Timothy Pearson ([trinitydesktop.org](http://trinitydesktop.org/)). This project aims to keep the KDE3.5 computing style alive, as well as polish off any rough edges that were present as of KDE 3.5.10\. See [Trinity](/index.php/Trinity "Trinity") for more info.

**Attenzione:** KDE 3 non è più mantenuta e supportata dagli sviluppatori di KDE. "Trinity KDE" è mantenuto dalla comunità del progetto Trinity. Quindi lo utilizzerete KDE3 a vostro rischio e pericolo, per quanto riguarda eventuali bug, problemi di prestazioni o rischi per la sicurezza.

## Bugs

È preferibile, nel caso in cui si incontri un bug minore o serio, visitare [il Arch Bug Tracker](https://bugs.archlinux.org) o/e [il KDE Bug Tracker](http://bugs.kde.org) in maniera da segnalarlo. Assicurarsi di essere chiari su cosa si desideri riportare.

Nel caso in cui si abbiano problemi e si scriva sul forum di Arch, assicurarsi innanzitutto di aver aggiornato **COMPLETAMENTE** il sistema usando un mirror ben sincronizzato (guardare [qui](https://www.archlinux.de/?page=MirrorStatus)) o provare [Reflector](/index.php/Reflector "Reflector").

## Links Esterni

*   [[5]](http://www.kde.org) - KDE homepage
*   [[6]](https://bugs.kde.org) - KDE bug tracker
*   [[7]](https://bugs.archlinux.org) - Arch Linux bug tracker
*   [[8]](https://projects.kde.org) - KDE Projects