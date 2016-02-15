Il progetto GNOME è ripartito dalle fondamenta ed ha creato un desktop completamente nuovo chiamato GNOME 3\. Esso ha:

*   Tema grafico e font moderni
*   Un'interfaccia che fornisce accesso a tutte le finestre ed applicazioni
*   Un sistema di notifiche ed un discreto pannello superiore
*   Un migliorato file manager GNOME Files
*   Servizi di messaggistica integrati nel desktop
*   Un nuovo sistema di impostazioni delle applicazioni
*   Una funzione di ricerca delle attività
*   Modalità simili alla funzione Aero Snap di Windows

[ulteriori dettagli sul sito [GNOME3](http://www.gnome3.org/)]

## Contents

*   [1 Introduzione](#Introduzione)
*   [2 Installazione](#Installazione)
    *   [2.1 Demoni e moduli richiesti da GNOME](#Demoni_e_moduli_richiesti_da_GNOME)
    *   [2.2 Eseguire GNOME](#Eseguire_GNOME)
*   [3 Utilizzare gnome-shell](#Utilizzare_gnome-shell)
    *   [3.1 Riavviare la shell](#Riavviare_la_shell)
    *   [3.2 Crashes della Shell](#Crashes_della_Shell)
*   [4 Personalizzazione grafica di Gnome](#Personalizzazione_grafica_di_Gnome)
    *   [4.1 Aspetti generali](#Aspetti_generali)
        *   [4.1.1 Gsettings](#Gsettings)
        *   [4.1.2 Gnome-tweak-tool](#Gnome-tweak-tool)
        *   [4.1.3 Temi GTK3 tramite settings.ini](#Temi_GTK3_tramite_settings.ini)
        *   [4.1.4 Tema delle icone](#Tema_delle_icone)
    *   [4.2 GNOME Files](#GNOME_Files)
        *   [4.2.1 Rimuovere le cartelle dalla places sidebar](#Rimuovere_le_cartelle_dalla_places_sidebar)
        *   [4.2.2 Visualizzare il percorso file come testo](#Visualizzare_il_percorso_file_come_testo)
    *   [4.3 Pannello GNOME](#Pannello_GNOME)
        *   [4.3.1 Visualizzare la data nella barra superiore](#Visualizzare_la_data_nella_barra_superiore)
        *   [4.3.2 Nascondere icone della barra superiore](#Nascondere_icone_della_barra_superiore)
        *   [4.3.3 Disabilitare la "Sospensione" nello status menu](#Disabilitare_la_.22Sospensione.22_nello_status_menu)
        *   [4.3.4 Eliminare tempo di attesa durante il logging out](#Eliminare_tempo_di_attesa_durante_il_logging_out)
        *   [4.3.5 Visualizzare il system monitor](#Visualizzare_il_system_monitor)
        *   [4.3.6 Visualizza informazioni sul tempo](#Visualizza_informazioni_sul_tempo)
    *   [4.4 Activity view](#Activity_view)
        *   [4.4.1 Rimuovere le voci dall'Applications view](#Rimuovere_le_voci_dall.27Applications_view)
        *   [4.4.2 Ridurre la dimensione delle icone delle applicazioni](#Ridurre_la_dimensione_delle_icone_delle_applicazioni)
        *   [4.4.3 Disabilitare Activity View all'angolo dello schermo](#Disabilitare_Activity_View_all.27angolo_dello_schermo)
    *   [4.5 Titlebar](#Titlebar)
        *   [4.5.1 Ridurre l'altezza della barra del titolo](#Ridurre_l.27altezza_della_barra_del_titolo)
        *   [4.5.2 Riordinare i pulsanti della titlebar](#Riordinare_i_pulsanti_della_titlebar)
        *   [4.5.3 Nascondere la titlebar con le finestre fullscreen (maximized)](#Nascondere_la_titlebar_con_le_finestre_fullscreen_.28maximized.29)
        *   [4.5.4 Immagine di sfondo](#Immagine_di_sfondo)
        *   [4.5.5 Font più grandi al login](#Font_pi.C3.B9_grandi_al_login)
        *   [4.5.6 Disabilitare audio all'avvio](#Disabilitare_audio_all.27avvio)
        *   [4.5.7 Rendere il pulsante power interattivo](#Rendere_il_pulsante_power_interattivo)
        *   [4.5.8 Layout tastiera GDM](#Layout_tastiera_GDM)
    *   [4.6 Altre tips](#Altre_tips)
*   [5 Impostazioni varie](#Impostazioni_varie)
    *   [5.1 Lancio automatico dei programmi al login](#Lancio_automatico_dei_programmi_al_login)
    *   [5.2 Attivare il numlock dopo il login automaticamente](#Attivare_il_numlock_dopo_il_login_automaticamente)
    *   [5.3 Spostare le dialog windows](#Spostare_le_dialog_windows)
    *   [5.4 Abilitare le estensioni della shell](#Abilitare_le_estensioni_della_shell)
    *   [5.5 Impostare il terminale predefinito da console](#Impostare_il_terminale_predefinito_da_console)
    *   [5.6 Emulazione del tasto centrale](#Emulazione_del_tasto_centrale)
    *   [5.7 Xmonad](#Xmonad)
    *   [5.8 Wmii](#Wmii)
*   [6 Abilitare funzioni nascoste](#Abilitare_funzioni_nascoste)
    *   [6.1 Modificare gli Hotkeys](#Modificare_gli_Hotkeys)
    *   [6.2 Shutdown via status menu](#Shutdown_via_status_menu)
*   [7 Integrare la messaggistica (Empathy)](#Integrare_la_messaggistica_.28Empathy.29)
*   [8 Abilitare la modalità fallback](#Abilitare_la_modalit.C3.A0_fallback)
*   [9 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [9.1 Tempo di login in GNOME molto lungo](#Tempo_di_login_in_GNOME_molto_lungo)
    *   [9.2 Quando le estensioni disturbano GNOME](#Quando_le_estensioni_disturbano_GNOME)
    *   [9.3 Le estensioni non funzionano dopo aver aggiornato Gnome](#Le_estensioni_non_funzionano_dopo_aver_aggiornato_Gnome)
    *   [9.4 Schermo non bloccato dopo sospensione/ibernazione](#Schermo_non_bloccato_dopo_sospensione.2Fibernazione)
    *   [9.5 Le applicazioni GTK2+ vanno in segmentation fault](#Le_applicazioni_GTK2.2B_vanno_in_segmentation_fault)
    *   [9.6 Artefatti con driver Catalyst su Gnome-Shell](#Artefatti_con_driver_Catalyst_su_Gnome-Shell)
    *   [9.7 Xf86-video-ati driver: sfarfallio](#Xf86-video-ati_driver:_sfarfallio)
    *   [9.8 Le nuove finestre si aprono dietro altre finestre quando uso schermi multipli](#Le_nuove_finestre_si_aprono_dietro_altre_finestre_quando_uso_schermi_multipli)
    *   [9.9 Monitor multipli e Dock extensions](#Monitor_multipli_e_Dock_extensions)
    *   [9.10 Nessuna notifica sonora con Empathy ed altri programmi](#Nessuna_notifica_sonora_con_Empathy_ed_altri_programmi)
    *   [9.11 Editere hotkeys via can-change-accels non funziona](#Editere_hotkeys_via_can-change-accels_non_funziona)
    *   [9.12 Pannelli ed applet non rispondono al click destro](#Pannelli_ed_applet_non_rispondono_al_click_destro)
    *   [9.13 Mostra Desktop: la scorciatoia da tastiera non funziona](#Mostra_Desktop:_la_scorciatoia_da_tastiera_non_funziona)
    *   [9.14 GNOME Files non si avvia](#GNOME_Files_non_si_avvia)
    *   [9.15 Impossibile applicare la configurazione memorizzata per i monitor](#Impossibile_applicare_la_configurazione_memorizzata_per_i_monitor)
    *   [9.16 Pulsante di blocco non riesce a riattivare touchpad](#Pulsante_di_blocco_non_riesce_a_riattivare_touchpad)
    *   [9.17 Ctrl + V incolla il percorso invece dei files in GNOME Files](#Ctrl_.2B_V_incolla_il_percorso_invece_dei_files_in_GNOME_Files)
    *   [9.18 Impossibile collegarsi ad una rete wi-fi protetta](#Impossibile_collegarsi_ad_una_rete_wi-fi_protetta)
    *   [9.19 "Ogni comando è stato definito 33"](#.22Ogni_comando_.C3.A8_stato_definito_33.22)
    *   [9.20 GDM e Gnome usano il cursore di X11](#GDM_e_Gnome_usano_il_cursore_di_X11)
*   [10 Links esterni](#Links_esterni)

## Introduzione

Gnome 3 fornisce **due** interfacce, **gnome-shell** (il nuovo layout standard) e modalità **fallback**. Gnome-session rileverà automaticamente se la macchina in uso è in grado di usare gnome-shell, altrimenti avvierà la modalità fallback.

La modalità **fallback** ha un aspetto molto simile al vecchio Gnome2 (utilizza un porting in gtk3 di gnome panel + metacity, anzichè gnome-shell e mutter).

Se si utilizza la modalità fallback, è ancora possibile modificare il window manager predefinito con quello che si preferisce.

## Installazione

GNOME 3 è in [extra]. È possibile installarlo con il seguente comando:

```
# pacman -Syu
# pacman -S gnome
```

Per installare applicazioni supplementari

 `# pacman -S gnome-extra` 

### Demoni e moduli richiesti da GNOME

Il Desktop GNOME richiede un demone per operare in maniera corretta, **DBUS**.

Per avviare il demone DBUS:

 `# rc.d start dbus` 

Oppure aggiungere questo demone all'array **DAEMONS** di `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")`, in modo che venga automaticamente eseguito all'avvio:

 `/etc/rc.conf` 

```
......
DAEMONS=(syslog-ng **dbus** network crond)
......
```

**GVFS** consente ad altre applicazioni, incluso il file manager di GNOME Files, di utilizzare filesystem virtuali (ad es. filesystem montati su FTP o SMB). Ciò è possibile grazie all'utilizzo di **FUSE**: un modulo del kernel che fornisce un layer in userspace per i filesystem virtuali.

Per caricare il modulo del kernel FUSE:

 `# modprobe fuse` 

Oppure aggiungere il modulo all'array **MODULES** in `/etc/rc.conf` in modo che venga caricato automaticamente all'avvio. Ad es.

 `/etc/rc.conf` 

```
.....
MODULES=(**fuse**)
.....
```

**Nota:** FUSE è un modulo del kernel, non un demone.

### Eseguire GNOME

Per una migliore integrazione col desktop, è consigliato l'uso di **GDM**.

 `# pacman -S gdm` 

Consultare la pagina [Display Manager](/index.php/Display_Manager_(Italiano) "Display Manager (Italiano)") per capire come eseguirlo correttamente.

Se si preferisce eseguirlo da console, aggiungere la seguente righe a `~/.xinitrc`, accertandosi che sia l'ultima del file e che sia l'unica ad iniziare con _exec_(Consultare la pagina [xinitrc](/index.php/Xinitrc_(Italiano) "Xinitrc (Italiano)")):

 ``/.xinitrc` 

```
.....
exec gnome-session
.....

```

In questo modo GNOME verrà eseguito all'inserimento di questo comando:

 `$ startx` 

## Utilizzare gnome-shell

Per maggiori informazioni consultare [https://live.gnome.org/GnomeShell/CheatSheet](https://live.gnome.org/GnomeShell/CheatSheet)

### Riavviare la shell

Dopo aver apportato delle modifiche all'aspetto di Gnome tramite tweaks, potrebbe essere richiesto di riavviare la Gnome shell. Invece di effettuare il log out per riaprire la nuova sessione, è più semplice e veloce eseguire i seguenti comandi da tastiera:

Riavviate la shell premendo `Alt` + `F2` poi `r` ed infine `Enter`

### Crashes della Shell

Alcune modifiche e/o ripetuti riavvii della shell possono causare dei crash. In questi casi sarete informati riguardo l'errore e poi sarete forzati ad effettuare il log out. Alcuni cambiamenti della shell, come il passaggio da _**GNOME Shell**_ a _**fallback mode**_ non possono essere realizzati tramite tastiera, ma si deve effettuare il log out e poi di nuovo il log in perché abbiano effetto.

Anche se lo dice il buon senso, vale la pena ripetere che i documenti di valore dovrebbero essere salvati (o addirittura è consigliato chiudere l'intera applicazione con cui si sta lavorando), prima di tentare un riavvio della shell. Non è strettamente necessario; i documenti e le finestre aperte normalmente rimangono intatte dopo il riavvio della shell.

## Personalizzazione grafica di Gnome

### Aspetti generali

Al momento non esiste uno strumento onnicomprensivo per configurare Gnome 3\. Il nuovo strumento System Settings è un grande miglioramento rispetto ai pannelli di controllo precedenti, ma dovrete operare manualmente su alcune configurazioni per avere un miglior controllo sull'aspetto grafico di Gnome.

Gli attuali strumenti di configurazione vi saranno familiari: alcuni di questi funzionano ancora, molti altri no. Alcune impostazioni non sono facilmente raggiungibili per essere modificate. Sicuramente molte impostazioni saranno disponibili successivamente tramite l'utilizzo di nuovi strumenti (tools), che saranno realizzati con il passare del tempo durante lo sviluppo di Gnome 3, grazie ad una comunità sempre più ampia.

#### Gsettings

Un nuovo strumento da linea di comando memorizza i dati in formato binario, a differenza dei precedenti strumenti che utilizzavano file XML. Il tutorial [Customizing the GNOME Shell](http://blog.fpmurphy.com/2011/03/customizing-the-gnome-3-shell.html) mette in evidenza le potenzialità di Gsettings.

#### Gnome-tweak-tool

 `# pacman -S gnome-tweak-tool` 

Questo strumento consente di personalizzare font, temi, tasti di massimizzazione e minimizzazione ed altre utili impostazioni, come le azioni da intraprendere alla chiusura del coperchio di un notebook. Una buona fonte di informazioni riguardo la personalizzazione è reperibile a questo indirizzo [[1]](http://blog.fpmurphy.com/2011/03/customizing-the-gnome-3-shell.html)

A causa di un [bug](https://bugzilla.gnome.org/show_bug.cgi?id=647132) la versione 3.0.3 funziona solo se gnome-shell è installato.

#### Temi GTK3 tramite settings.ini

Come **`~/.gtkrc-2.0`** per GTK2+, è possibile settare un tema GTK3 tramite **`${XDG_CONFIG_HOME}/gtk-3.0/settings.ini`**.

La variabile `$XDG_CONFIG_HOME` normalmente assume il valore **~/.config**

_Adwaita,_ il tema di default in GNOME 3, fa parte di uno dei **gnome-themes-standard** (temi standard di gnome). Altri temi per GTK3 possono essere trovati sul sito [Deviantart web site.](http://browse.deviantart.com/customization/skins/linuxutil/desktopenv/gnome/gtk3/)

Ad esempio si può inserire:

```
 [Settings]
 gtk-theme-name = Adwaita
 gtk-fallback-icon-theme = gnome
 # La prossima opzione è applicabile solo se il tema selezionato la supporta
 gtk-application-prefer-dark-theme = true
 # Imposta i nomi dei font e la dimensione
 gtk-font-name = Sans 10

```

È necessario [riavviare la shell di Gnome](#Riavviare_la_shell) per far si che le nuove impostazioni siano applicate. Molte altre opzioni di GTK possono essere consultate sul sito [GNOME developer documentation.](http://developer.gnome.org/gtk3/3.0/GtkSettings.html#GtkSettings.properties)

#### Tema delle icone

**Nota:** Utilizzando gnome-tweak-tool v. 3.0.3 e superiori, potete installare il vostro tema delle icone preferito all'interno della cartella **`~/.icons`**.

GNOME 3 è compatibile con i temi delle icone di GNOME 2, quindi non siete obbligati ad usare il tema delle icone di default. Per installare un nuovo set di icone, copiate il tema che desiderate nella cartella dei temi delle icone **`~/.icons`**. Per esempio in questo modo:

 ` $ cp -R /home/user/Desktop/my_icon_theme ~/.icons` 

Il nuovo tema _my_icon_theme_ ora sarà selezionabile utilizzando **gnome-tweak-tool** sotto la voce _**interface**_ (_interfaccia_).

In alternativa, potete selezionare il vostro nuovo tema senza aver bisogno di utilizzare gnome-tweak-tool. Per fare questo, aggiungete il vostro tema delle icone GTK al file **`${XDG_CONFIG_HOME}/gtk-3.0/settings.ini`**.

 `${XDG_CONFIG_HOME}/gtk-3.0/settings.ini` 

```
... linee precedenti ...

gtk-icon-theme-name = my_new_icon_theme
```

### GNOME Files

#### Rimuovere le cartelle dalla places sidebar

La visualizzazion delle cartele è specificata in `~/.config/user-dirs.dirs` e può essere modificata con un qualsiasi editor di testo. Eseguendo il comando `xdg-user-dirs-update` aggiorneremo lo stato della sidebar con le nuove impostazioni, per questo è consigliato settare il permesso del file su sola lettura (read-only).

#### Visualizzare il percorso file come testo

La toolbar standard di GNOME Files visualizza una barra con un'interfaccia basata su dei bottoni per la navigazione nel percorso dei file.

Per entrare in una specifica posizione del percorso file utilizzando la _tastiera_, dovete visualizzare il campo per inserire il testo con la vostra locazione da raggiungere premendo i tasti `Ctrl` + `L`.

Per rendere permanente la visualizzazione del campo percorso come testo, utilizzate gsettings come di seguito.

 `$ gsettings set org.gnome.nautilus.preferences always-use-location-entry true` 
**Note:** una volta effettuato questo cambiamento non sarà più possibile visualizzare la barra con i bottoni (pulsanti) che vi è di base. Solo quando è settata a **false** potete utilizzare entrambi i modi per la visualizzazione del percorso.

### Pannello GNOME

#### Visualizzare la data nella barra superiore

Di default Gnome visualizza solo il giorno della settimana e l'ora sulla barra in alto. Questo può essere modificato con il seguente comando. Gli effetti si vedranno immediatamente.

 `# gsettings set org.gnome.shell.clock show-date true` 

#### Nascondere icone della barra superiore

Quando effettuate l'installazione di Gnome, potrebbero essere visualizzate sul pannello delle icone che non volete utilizzare. Per rimuovere queste icone, dovete modificare l'apposito script del pannello.

Per esempio, per rimuovere l' **icona di accesso universale**, rimuovete 'a11y' dalla linea AREA_ORDER e commentate 'a11y' alla linea AREA_SHELL_IMPLEMENTATION.

 `/usr/share/gnome-shell/js/ui/panel.js` 

```
const STANDARD_STATUS_AREA_ORDER = ['a11y', 'keyboard', 'volume', 'network', 'bluetooth', 'battery', 'userMenu'];
const STANDARD_STATUS_AREA_SHELL_IMPLEMENTATION = {
    'a11y': imports.ui.status.accessibility.ATIndicator
    'volume': imports.ui.status.volume.Indicator,
    'battery': imports.ui.status.power.Indicator,
    'keyboard': imports.ui.status.keyboard.XKBIndicator,
    'userMenu': imports.ui.userMenu.UserMenuButton
};

```

Il file deve diventare come il seguente:

 `/usr/share/gnome-shell/js/ui/panel.js` 

```
const STANDARD_STATUS_AREA_ORDER = ['keyboard', 'volume', 'network', 'bluetooth' 'battery', 'userMenu'];
const STANDARD_STATUS_AREA_SHELL_IMPLEMENTATION = {
    //'a11y': imports.ui.status.accessibility.ATIndicator
    'volume': imports.ui.status.volume.Indicator,
    'battery': imports.ui.status.power.Indicator,
    'keyboard': imports.ui.status.keyboard.XKBIndicator,
    'userMenu': imports.ui.userMenu.UserMenuButton
};

```

Salvate le vostre modifiche e [riavviate la shell di GNOME](#Riavviare_la_shell) per vedere i vostri cambiamenti.

#### Disabilitare la "Sospensione" nello status menu

Un modo veloce per farlo è cambiare la linea 153 di **`/usr/share/gnome-shell/js/ui/statusMenu.js`**. Questo cambiamento ha effetto al prossimo avvio della Gnome shell.

 `/usr/share/gnome-shell/js/ui/statusMenu.js` 

```
 // this._haveSuspend = this._upClient.get_can_suspend(); // Commentate questa linea.
 this._haveSuspend = false; // Scrivete questa linea.

```

Comunque gli effetti non saranno visibili fino all'aggiornamento di Gnome. Un modo non definitivo per raggiungere questa soluzione è quello di installare [alternative status menu](#GNOME_shell_extensions).

 `# pacman -S gnome-shell-extension-alternative-status-menu` 

#### Eliminare tempo di attesa durante il logging out

La seguente modifica rimuove il dialogo di conferma ed i sessanta secondi di attesa per il logging out.

Il messaggio normalmente appare quanto si effettua il logout dallo status menu. Questa modifica incide anche sul dialogo che riguarda il _**Power Off**_. Non è una modifica a livello di sistema; ha effetto solo sull'utente che utilizza questo comando. Gli effetti si possono notare subito dopo l'esecuzione del seguente comando.

 `$ gsettings set org.gnome.SessionManager logout-prompt 'false'` 

#### Visualizzare il system monitor

Installare l'estensione [gnome-shell-system-monitor-applet-git](https://aur.archlinux.org/packages/gnome-shell-system-monitor-applet-git/) disponibile su AUR.

#### Visualizza informazioni sul tempo

Installare [gnome-shell-extension-weather-git](https://aur.archlinux.org/packages/gnome-shell-extension-weather-git/) da [AUR](/index.php/AUR "AUR").

### Activity view

#### Rimuovere le voci dall'Applications view

Come altri ambienti desktop, GNOME utilizza i .desktop files per popolare la sua vista delle applicazioni (Applications view). Questi file di testo si trovano in **`/usr/share/applications`**. Non è possibile modificare questi file visualizzandoli normalmente in GNOME Files, perché quest'ultimo non tratta le sue icone come file di testo. Usate quindi un terminale per visualizzare o editare le voci nel file .desktop.

```
# ls /usr/share/applications
# nano /usr/share/applications/foo.desktop

```

Per le modifiche a livello di sistema, editate i files in **`/usr/share/applications`**. Per una modifica locale, create una copia del file _foo.desktop_ nella vostra cartella home.

```
$ cp /usr/share/applications/foo.desktop ~/.local/share/applications/

```

Modificate il file .desktop per soddisfare i vostri bisogni. **Nota:** rimuovere un file .desktop non coporta la disinstallazione dell'applicazione rimossa, ma rimuove solamente la sua integrazione con il desktop: MIME types, scorciatoie e così via.

Il seguente comando aggiunge una linea di codice al file .desktop e nasconde l'icona associata all'Applications view:

```
$ echo "NoDisplay=true" >> foo.desktop

```

#### Ridurre la dimensione delle icone delle applicazioni

Una scelta imbarazzante dei progettisti GNOME è stata quella di utilizzare icone di grandi dimensioni per la visualizzazione delle applicazioni. Questa visione è controproducente quando si lavora con piccoli schermi che contengono molte applicazioni con icone di grandi dimensioni. C'è un modo per ridurre la grandezza di queste icone ed è quello di modificare il tema della Gnome-Shell.

Modificate i vostri file direttamente (ricordatevi di effettuare prima un backup) o copiate i file del tema in una cartella locale e modificateli. Per il tema principale dovete modificare il file :**`/usr/share/gnome-shell/theme/gnome-shell.css`**

Per il tema utente modificate :**`/usr/share/themes/_user_theme_/gnome-shell/gnome-shell.css`**

Apportate cambiamenti a _gnome-shell.css_ sostituendo i seguenti valori. Successivamente [riavviate la Gnome-Shell.](#Riavviare_la_shell)

 `gnome-shell.css` 

```
 .icon-grid {
     spacing: 18px;
     -shell-grid-item-size: 82px;
 }

 .icon-grid .overview-icon {
     icon-size: 48px;
 }

```

Un clone del tema base della Gnome-Shell con icone più piccole è disponibile [su AUR](https://aur.archlinux.org/packages.php?ID=51586).

#### Disabilitare Activity View all'angolo dello schermo

Per disabilitare l'Activity View automatica quando si raggiunge con il mouse l'angolo in alto a sinistra dello schermo, modificate **`/usr/share/gnome-shell/js/ui/layout.js`** (che corrisponde a _panel.js_ in Gnome 3.0.x) :

 `layout.js` 

```
 this._corner = new Clutter.Rectangle({ name: 'hot-corner',
                                       width: 1,
                                       height: 1,
                                       opacity: 0,
                                       reactive: true });icon-size: 48px;
 }

```

Dovete settare _reactive_ a _false_. Successivamente dovete [riavviate la Gnome-Shell.](#Riavviare_la_shell)

### Titlebar

#### Ridurre l'altezza della barra del titolo

```
# sed -i '/title_vertical_pad/s|value="[0-9]\{1,2\}"|value="0"|g' /usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml

```

[Riavviare la shell di Gnome.](#Riavviare_la_shell) Il comando precedente cambia il padding verticale da 14 a 0, per dare alle finestre un'spetto più sottile.

Per ripristinare i valori originali:

 `$ sudo pacman -S gnome-themes-standard` 

#### Riordinare i pulsanti della titlebar

Al momento l'unica possibilità per cambiare questa impostazione è attraverso **gconf-editor.**

Per esempio, spostiamo il pulsante di chiusura e della minimizzazione sul lato sinistro della titlebar.

Aprite **gconf-editor** e localizzate la chiave che riguarda _**desktop.gnome.shell.windows.button_layout**_. Cambiate il suo valore in **`close,minimize:`** (I due punti rappresentano lo spazio designato tra la parte sinistra e la destra della titlebar). Utilizzate qualsiasi pulsante nell'ordine che preferite. Non potete utilizzare un pulsante più di una volta. Tenete anche in mente che alcuni bottoni potrebbero essere deprecati. [Riavviate la shell di Gnome](#Riavviare_la_shell) per vedere i cambiamenti apportati.

#### Nascondere la titlebar con le finestre fullscreen (maximized)

```
 # sed -i -r 's|(<frame_geometry name="max")|\1 has_title="false"|' /usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml

```

[Riavviare la shell di Gnome.](#Riavviare_la_shell) Dopo questa modifica, potreste trovare difficoltoso demassimizzare la finestra, visto che non c'è nessuna titlebar da afferrare.

Per uscire da questa situazione potete utilizzare una delle seguenti combinazioni di tasti : `Alt` + `F5`, `Alt` + `F10` , `Alt` + `Space`

Per prevenire la sovrascrittura del file **`metacity-theme-3.xml`** ogni volta che viene aggiornato il pacchetto "gnome-themes-standard", aggiungete questo nome a **`/etc/pacman.conf`** con il parametro `NoUpgrade`.

 `/etc/pacman.conf` 

```
... linee precedenti ...

# Pacman won't upgrade packages listed in IgnorePkg and members of IgnoreGroup
# IgnorePkg =
# IgnoreGroup =

NoUpgrade = usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml #Non aggiungere il primo slash

... altre linee ...
```

Per ripristinare i valori originali di Adwaita:

 `# pacman -S gnome-themes-standard` 

#### Immagine di sfondo

Una volta esportate le variabili di aimbiente nella sessione come spiegato sopra, si possono dare comandi per recuperare o impostare gli elementi utilizzati da GDM.

Il modo più semplice per cambiare impostazioni è lanciare il Configuration Editor con il seguente comando :

 `$ dconf-editor` 

La posizione di ogni impostazione è la stessa nello stile di configurazione della linea di comando mostrato qui sotto:

quello che segue rispecchia l'approccio da linea di comando per recuperare o impostare il nome del file utilizzato per il wallpaper.

```
$ GSETTINGS_BACKEND=dconf gsettings get org.gnome.desktop.background picture-uri
$ GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.background picture-uri "file:///usr/share/backgrounds/gnome/SundownDunes.jpg"

$ GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.background picture-options 'zoom'
## Possibili valori: centered, none, scaled, spanned, stretched, wallpaper, zoom
```

**Nota:** Si deve specificare un file che l'utente 'gdm' è in grado di leggere. GDM non può leggere i file nella vostra home directory.

Un'alternativa grafica per cambiare il tema (gtk3, icone e cursore), lo sfondo ed altre impostazioni minori è [gdm3setup](https://aur.archlinux.org/packages.php?ID=50232) disponibile in AUR.

#### Font più grandi al login

Questo tweak aumenta i font di login di un fattore scalare. E' lo stesso modo applicato dall' _Accessibility Manager_ presente sul desktop.

Dovete prima esportare le variabili della sessione GDM per effettuare questa modifica.

 `$ GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.interface text-scaling-factor '1.25'` 

#### Disabilitare audio all'avvio

Questo tweak permette di non udire il suono di feedback che si sente alla schermata di avvio quando si aggiusta l'audio tramite tastiera. Dovete prima esportare le variabili per la sessione GDM.

 `$ GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.sound event-sounds false` 

Se quanto detto sopra non funziona per voi o non siete in grado di esportare le variabili della sessione GDM, c'è sempre la soluzione più semplice per risolvere il problema: disattivare o abbassare il suono, mentre si è nella schermata di login GDM, utilizzando i tasti multimediali (se sono a disposizione sulla tastiera).

#### Rendere il pulsante power interattivo

L'installazione di default setta il pulsante di accensione per sospendere il systema. Spegnerlo o visualizzare una finestra di dialogo sarebbe una scelta migliore. Per settare questa impostazione dovete esportare le variabili di ambiente di GDM.

```
 $ GSETTINGS_BACKEND=dconf gsettings set org.gnome.settings-daemon.plugins.power button-power 'interactive'
 $ GSETTINGS_BACKEND=dconf gsettings set org.gnome.settings-daemon.plugins.power button-hibernate 'interactive'
 $ gsettings list-recursively org.gnome.settings-daemon.plugins.power
```

#### Layout tastiera GDM

GDM non conosce le impostazioni riguardo la vostra tastiera in Gnome3\. Per cambiare le impostazioni della tastiera utilizzata da GDM, modificate il vostro layout utilizzando i file di configurazione di Xorg. Fate riferimento a questa sezione per la modifica : [Beginner's Guide.](/index.php/Beginners%27_guide#Non-US_keyboard "Beginners' guide")

### Altre tips

Guardate [GNOME Tips](/index.php/GNOME_Tips "GNOME Tips").

## Impostazioni varie

#### Lancio automatico dei programmi al login

È possibile specificare quali programmi avviare automaticamente dopo il login utilizzando lo strumento **gnome-session-properties**, che fa parte del pacchetto **gnome-session**.

 `$ gnome-session-properties` 
**Nota:** Potete avviarlo premendo `Alt` + `F2`, poi digitate `gnome-session-properties` ed infine premete `Invio`.

#### Attivare il numlock dopo il login automaticamente

Installate numlockx dal repository **[community]**. Poi aggiungete ai programmi di avvio il comando numlockx.

```
# pacman -S numlockx
$ gnome-session-properties
```

I comandi seguenti aprono l'applet **Startup Applications Preferences**. Cliccate su _**Add**_ (aggiungi) e aggiungete le righe seguenti:

| Name: | _Numlockx_ |
| Command: | _/usr/bin/numlockx on_ |
| Comment: | _Turns on numlock._ |

Questo non è un tweak a livello di sistema, quindi dovete ripetere questi passaggi per ogni utente che utilizza il sistema operativo.

#### Spostare le dialog windows

La configurazione di default per i dialoghi non permette di muoverli, questo può causare problemi in alcuni casi. Per cambiare questa impostazione dovete utilizzare **gconf-editor** e cambiare la seguente opzione :

```
{{/desktop/gnome/shell/windows/attach_modal_dialogs}}

```

Una volta finito dovete [riavviare la GNOME shell](#Riavviare_la_shell) per notare i cambiamenti.

#### Abilitare le estensioni della shell

La Gnome Shell può essere personalizzata con delle estensioni scritte da altri utenti. Queste aggiungono funzionalità come una dock aggiuntiva o un tema differente.

molte estensioni sono collezionate e ospitate da [gnome.org](https://extensions.gnome.org/). Possono essere visualizzate tramite browser e installate semplicemente attivandole da quest'ultimo.

Altri dettagli sulle estensioni disponibili possono essere trovati sul sito [WEBUPD8](http://www.webupd8.org/2011/04/gnome-shell-extensions-additional.html). Gli articoli più recenti possono essere consultati utilizzando il seguente [WEBUPD8 search link.](http://www.webupd8.org/search/label/gnome%20shell%20extensions?max-results=20)

I [repositories ufficiali](/index.php/Official_repositories "Official repositories") hanno dozzine di estensioni che possono essere installate individualmente (è preferibile installare la snapshot dell'ultima versione dell'estensione desiderata) [List here.](https://www.archlinux.org/packages/?sort=&q=gnome-shell-extension&maintainer=&last_update=&flagged=&limit=50)

La lista delle estensioni disponibili in pacman è disponibile digitando il comando:

 ` $ pacman -Ss gnome-shell-extension` 

Altri links utili : [WEBUPD8 search link](http://www.webupd8.org/search/label/gnome%20shell%20extensions?max-results=20) - [WEBUPD8](http://www.webupd8.org/2011/04/gnome-shell-extensions-additional.html)

Ecco alcune estensioni utili reperibili in [AUR](/index.php/AUR "AUR"):

| Package | Description |
| [gnome-shell-extension-presentation-mode-git](https://aur.archlinux.org/packages/gnome-shell-extension-presentation-mode-git/) | Aggiunge l'opzione di disabilitare lo screensaver dal menu della batteria (battery icon). |
| [gnome-shell-extension-weather-git](https://aur.archlinux.org/packages/gnome-shell-extension-weather-git/) | Visualizza notifiche meteo. |
| [gnome-shell-extension-alternative-status-menu-git](https://aur.archlinux.org/packages/gnome-shell-extension-alternative-status-menu-git/) | Aggiunge le opzioni "Iberna" e "Spegni" allo status menu. |
| [gnome-shell-extension-theme-selector](https://aur.archlinux.org/packages/gnome-shell-extension-theme-selector/) | Seleziona un tema nella panoramica di Activities. Per installare un tema personalizzato con GNOME Tweak Tool, dovete installare l'estensione [gnome-shell-extension-user-theme](https://www.archlinux.org/packages/?name=gnome-shell-extension-user-theme) dal repository ufficiale [official repositories](/index.php/Official_repositories "Official repositories"). |
| [gnome-shell-frippery](https://aur.archlinux.org/packages/gnome-shell-frippery/) | Un'estensione non ufficiale che implementa le caratteristiche di GNOME 2 in GNOME3. |

[Riavviate la GNOME Shell](#Riavviare_la_shell) dopo aver installato un'estensione. Guardate ["Quando le estensioni disturbano GNOME"](#Quando_le_estensioni_disturbano_GNOME) per informazioni quando avete un problema.

### Impostare il terminale predefinito da console

`gsettings`, che rimpiazza `gconftool-2` in Gnome 3, è usato ad esempio per impostare manualmente il terminale predefinito. Questa impostazione viene presa in considerazione dal comando _nautilus-open-terminal_.

I comandi per eseguire [urxvt](/index.php/Rxvt-unicode "Rxvt-unicode") come daemon:

```
$ gsettings set org.gnome.desktop.default-applications.terminal exec urxvtc
$ gsettings set org.gnome.desktop.default-applications.terminal exec-arg "'-e'"
```

**Nota:** Per _nautilus-open-terminal_, si potrebbe rendere necessario l'uso di una flag (es. `-e`) ad indicare che a seguire è presente un comando: _nautilus-open-terminal_ passa un comando `cd` in modo da spostarsi nella directory corretta.

### Emulazione del tasto centrale

Di default, Gnome3 disabilita l'emulazione del tasto centrale del mouse indipendentemente dal valore impostato per la variabile di Xorg (**Emulate3Buttons**). Per abilitarlo utilizzare il seguente comando:

 `gsettings set org.gnome.settings-daemon.peripherals.mouse middle-button-enabled true` 

### Xmonad

Effettuando l'aggiornamento a GNOME3, si riscontrerà sicuramente il non funzionamento della sessione [Xmonad](/index.php/Xmonad "Xmonad"). Si può utilizzarla di nuovo eseguendo GNOME in [modalità fallback](#Abilitare_la_modalit.C3.A0_fallback) (vedere sotto) e creando i due seguenti file:

 `/usr/share/gnome-session/sessions/xmonad.session` 

```
[GNOME Session]
Name=Xmonad session
RequiredComponents=gnome-panel;gnome-settings-daemon;
RequiredProviders=windowmanager;notifications;
DefaultProvider-windowmanager=xmonad
DefaultProvider-notifications=notification-daemon
```

 `/usr/share/xsessions/xmonad-gnome-session.desktop` 

```
[Desktop Entry]
Name=Xmonad GNOME
Comment=Tiling window manager
TryExec=/usr/bin/gnome-session
Exec=gnome-session --session=xmonad
Type=XSession
```

Al successivo log-in si avrà la possibilità di selezionare Xmonad GNOME come sessione.

### Wmii

[wmii](/index.php/Wmii "Wmii") è un manager per la piastrellatura (affiancamento) delle finestreis .

Potete utilizzare wmii con gnome [abilitando forzatamente il fallback mode](#Abilitare_la_modalit.C3.A0_fallback) e creando i seguenti tre file:

 `/usr/share/applications/wmii.desktop` 

```
[Desktop Entry]
Version=1.0
Type=Application
Name=wmii
TryExec=wmii
Exec=wmii
```

 `/usr/share/xsessions/gnome-wmii.desktop` 

```
[Desktop Entry]
Name=GNOME-wmii
Comment=GNOME with wmii as window manager
TryExec=gnome-session
Exec=gnome-session --session=wmii
Type=Application
```

 `/usr/share/gnome-session/sessions/wmii.session` 

```
[GNOME Session]
Name=wmii
RequiredComponents=gnome-panel;gnome-settings-daemon;
RequiredProviders=windowmanager;notifications;
DefaultProvider-windowmanager=wmii
DefaultProvider-notifications=notification-daemon
```

Al prossimo login dovreste avere abilitata la possibilità di sceglere _Gnome-wmii_ come sessione.

Le informazioni originali sono state prese da [running-the-awesome-window-manager-within-gnome](http://makandra.com/notes/1367-running-the-awesome-window-manager-within-gnome), dove potete trovare altre info.

Potete anche trovare notizie e tutorial riguardo:

- creare un **per session** (wmii, gnome, gnome-wmii, etc) dconf database (utile se volete utilizzare lo gnome regolare)

- Rimuovere il pulsante dal Gnome panel (con la task list)

- Muovere il pannello superiore (con i menus) in fondo

- Deselezionare l'opzione di espandere

- Impostarla su autohide

## Abilitare funzioni nascoste

Gnome 3 nasconde molte funzioni utili, che possono essere personalizzate tramite **dconf-editor**, o **gconf-editor** per quelle per cui non è stata ancora effettuata la migrazione.

### Modificare gli Hotkeys

In `dconf-editor`, abilitare `org.gnome.desktop.interface can-change-accels`.

Un esempio per modificare l'hotkey di cancellazione: Lanciare GNOME Files, selezionare un file qualsiasi, cliccare su `Modifica` nella barra dei menu, e posizionare il mouse sull'elemento `Sposta nel cestino`. Col puntatore fermo sull'elemento, premere il tasto `Canc`, per cancellare l'acceleratore predefinito. Premere ora il tasto che si vuole assegnare alla funzione. Ad esempio, premendo di nuovo il tasto `Canc`, l'acceleratore da tastiera dovrebbe ora cambiare da `Ctrl`+`Canc` a `Canc`.

Assicurarsi di aver selezionato un file, altrimenti `Sposta nel cestino` risulterà grigio e non cliccabile. È ora possibile disabilitare nuovamente `can-change-accels`, per evitare modifiche involontarie di altri acceleratori da tastiera.

### Shutdown via status menu

Attualmente i designers di Gnome hanno nascosto l'opzione di Spegnimento del computer nello status menù. Per spegnere il vostro sistema dallo status menù, cliccate sul menù tenendo premuto il tasto `Alt`. Noterete in questo modo che **Suspend** cambierà in **Power Off**, che premendolo farà visualizzare un dialogo per spegnere o riavviare la macchina.

Se avete disabilitato la Sospensione dal menù nel [seguente modo](#Disabilitare_la_.22Sospensione.22_nello_status_menu) non avete bisogno di effettuare questa operazione.

Un'alternativa è quella di installare l'estensione _Alternative Status Menu_. Guardate la sezione [che riguarda le estensioni](#Abilitare_le_estensioni_della_shell) per installare il menù che non nasconde il pulsante **Power Off**.

## Integrare la messaggistica (Empathy)

Empathy, l'engine integrato per i messaggi e per tutte le impostazioni di sistema basato su account di messaggistica non verrà visualizzato a meno che **telepathy** ed il suo gruppo di o almeno un suo backends (**telepathy-gabble**, oppure **telepathy-haze**, per esempio) sia installato.

Questi pacchetti non sono inclusi di default nell'installazione di Gnome in Arch, ma potete installare **telepathy** ed i suoi **backend** così :

 `# pacman -S telepathy` 

Senza **telepathy**, **Empathy** non aprirà l'account management dialog e si potrebbe bloccare in questo stato. Se questo accade, anche dopo essere usciti in modo pulito da Empathy, l'applicazione **/usr/bin/empathy-accounts** può rimanere **running** e sarà necessario killarla prima di aprire un altro account.

Potete vedere una descrizione dei componenti di telepathy su [Freedesktop.org Telepathy Wiki.](http://telepathy.freedesktop.org/wiki/Components)

## Abilitare la modalità fallback

La sessione di fallback viene avviata automaticamente quando la **gnome-shell** non è presente oppure quando l'hardware non supporta l'accelerazione grafica, per esempio a causa di una macchina virtuale oppure su un vecchio computer.

Se volete utilizzare la modalità fallback mentre avete già installato **gnome-shell**, effettuate i seguenti cambiamenti:

Aprite **gnome-control-center.** Cliccate sull'icona _System Info_ e poi su Graphics. Cambiate _Forced Fallback Mode_ in `ON.`

In alternativa potete scegliere il tipo di sessione dal terminale con il comando _gsettings_:

 `$ gsettings set org.gnome.desktop.session session-name 'gnome-fallback'` 

Dovete effettuare il logout dopo i cambiamenti, così da vederli applicati al vostro prossimo login.

Per disabilitare la modalità forced-fallback (che lancia una normale Gnome Shell), usate il valore 'gnome' al posto di 'gnome-fallback'

## Risoluzione dei problemi

### Tempo di login in GNOME molto lungo

Controllate se avete abilitato _PulseAudio Network_ nelle impostazioni in **paprefs**. Quando le impostazioni di una network audio sono abilitate, GNOME si blocca per qualche minuto dopo il login.

Una soluzione è quella di creare un nuovo utente ed entrare con quell'account. Un'altra soluzione è quella di muovere la vostre cartelle **~/.gconf**, **~/.gconfd** e **~/.conf/dconf** in una sorta di contenitore. Riloggatevi e controllate che il ritardo non avvenga più.

Se il tempo di attesa diventa eccessivo, cercare di determinare le cause utilizzando trial-and-error.

### Quando le estensioni disturbano GNOME

Quando si abilita una estensione della shell, Gnome potrebbe crashare. Per prima cosa dovete rimuovere le estensioni _user-theme_ e_auto-move-windows_ dalla loro directory di installazione.

La directory di installazione potrebbe essere una delle seguenti:**`~/.local/share/gnome‑shell/extensions,`** **`/usr/share/gnome‑shell/extensions,`** oppure **`/usr/local/share/gnome‑shell/extensions`**. Rimuovendo queste due estensioni l'errore dovrebbe sparire, altrimenti cercate di isolare il problema con trial‑and‑error.

La rimozione o l'aggiunta di una estensione nell cartella sopra citate rimuove o aggiunge l'estensione corrispondente al vostro sistema. Dettagli su Gnome Shell estensioni sono disponibili su [GNOME web site.](https://live.gnome.org/GnomeShell/Extensions)

### Le estensioni non funzionano dopo aver aggiornato Gnome

Localizzate la cartella dove le vostre estensioni sono installate. Dovrebbe essere una delle seguenti : **`~/.local/share/gnome-shell/extensions`** oppure **`/usr/share/gnome-shell/extensions`**.

Editate ogni occorrenza di **`metadata.json`** che appare in ogni estensione nella sotto directory.

| Inserite: | **`"shell-version": ["3.0"]`** |
| Al posto di (per esempio): | **`"shell-version": ["3.0.1"]`** |
| Potete anche scrivere: | **`"shell-version": ["3.0.0", "3.0.1", "3.0.2"]`** |

**"3.0"** è la migliore soluzione. Questa indica che l'estensione lavora con qualsiasi versione della shell Gnome come segue _**3.0.x**_.

### Schermo non bloccato dopo sospensione/ibernazione

Il blocco dello schermo funziona solo se la procedura di sospensione/ibernazione viene eseguita tramite il menù di stato di Gnome. Se si sospende o iberna tramite tasto d'accensione o altro, la funzionalità di blocca schermo non viene attivata.

Ciò avviene a causa di configurazione sbagliata in dconf. Per risolvere questo inconveniente è sufficiente modificare tramite dconf-editor il valore della chiave `lock-use screensaver` impostandolo a `false` (togliendo la spunta). Al resume lo schermo verrà ora bloccato indipendentemente dal metodo utilizzato per la messa in sospensione/ibernazione. Per ulteriori informazioni consultare il bugreport [Screen gets no more locked after suspend#Comment 8](https://bugzilla.redhat.com/show_bug.cgi?id=698135#c8)

Il comando per eseguirlo da terminale è :

 `# gsettings set org.gnome.power-manager lock-use-screensaver 'false'` 

### Le applicazioni GTK2+ vanno in segmentation fault

Solitamente succede quando si è installato **oxygen-gtk**. Questo tema va in qualche modo in conflitto con le impostazioni di GNOME3 e/o di GTK3, e quando viene impostato come tema GTK2+, le applicazioni GTK2+ vanno in segfault mostrando errori simili a questi:

```
(firefox-bin:14345): GLib-GObject-WARNING **: invalid (NULL) pointer instance
(firefox-bin:14345): GLib-GObject-CRITICAL **: g_signal_connect_data: assertion `G_TYPE_CHECK_INSTANCE (instance)' failed
(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_screen_get_default_colormap: assertion `GDK_IS_SCREEN (screen)' failed
(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_colormap_get_visual: assertion `GDK_IS_COLORMAP (colormap)' failed
(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_screen_get_default_colormap: assertion `GDK_IS_SCREEN (screen)' failed
(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_screen_get_root_window: assertion `GDK_IS_SCREEN (screen)' failed
(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_screen_get_root_window: assertion `GDK_IS_SCREEN (screen)' failed
(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_window_new: assertion `GDK_IS_WINDOW (parent)' failed
Segmentation fault

```

Attualmente l'unico workaround consiste nell'**eliminare** completamente dal sistema **oxygen-gtk** ed impostare un altro tema per le applicazioni.

### Artefatti con driver Catalyst su Gnome-Shell

Al momento, non è consigliabile utilizzare i driver Catalyst se si sceglie di eseguire Gnome-Shell. Il driver ATI opensource, xf86-video-ati, sembra invece funzionare adeguatamente col compositing di Gnome3

### Xf86-video-ati driver: sfarfallio

Se volete utilizzare questo driver, il vostro desktop potrebbe avere un effetto di sfarfallio (intermittenza) quando si posizione il mouse nell'angolo in basso a destra ed anche quando avviate gdm.

Scrivete le seguenti linee in **`/etc/X11/xorg.conf.d/20-radeon.conf`** e controllate che non lo faccia più successivamente:

```
Section "Device"
       Identifier "Radeon"
       Driver "radeon"
       Option "EnablePageFlip" "off"
EndSection

```

### Le nuove finestre si aprono dietro altre finestre quando uso schermi multipli

Questo può essere un possibile bug della gnome shell e causa l'apertura delle nuove finestre dietro alle altre già a perte. Deselezionate "workspaces_only_on_primary" in _desktop/gnome/shell/windows_ usando _gconf-editor_ per risolvere questo problema.

### Monitor multipli e Dock extensions

Se si hanno monitor multipli configurati tramite Nvidia Twinview, l'estensione Dock potrebbe risultare incastrata in mezzo ad essi. È possibile modificare il codice sorgente di questa estensione per spostare la dock in qualsiasi posizione a nostro piacimento. Modificare `/usr/share/gnome-shell/extensions/dock@gnome-shell-extensions.gnome.org/extension.js` e trovare nel sorgente questa riga:

 `/usr/share/gnome-shell/extensions/dock@gnome-shell-extensions.gnome.org/extension.js` 

```
..........
this.actor.set_position(primary.width-this._item_size-this._spacing-2, (primary.height-height)/2);
..........

```

Il primo parametro è la posizione rispetto all'asse X della dock sul monitor, è possibile fare varie prove con diverse coordinate X,Y fino ad ottenere l'effetto desiderato.

Per esempio :

 `/usr/share/gnome-shell/extensions/dock@gnome-shell-extensions.gnome.org/extension.js` 

```
..........
this.actor.set_position(primary.width-this._item_size-this._spacing-15, (primary.height-height)/2);
....

```

### Nessuna notifica sonora con Empathy ed altri programmi

Se si utilizza [OSS](/index.php/OSS "OSS"), è necessario installare `libcanberra-oss` [da AUR](https://aur.archlinux.org/packages.php?ID=31163).

### Editere hotkeys via can-change-accels non funziona

E' possibile cambiare manualmente le chiavi tramite un'applicazione chiamata accel map file. Dove si trova dipende dall'applicazione: per esempio in Thunar si trova in `~/.config/Thunar/accels.scm`, mentre in GNOME Files la troviamo in `~/.gnome2/accels/nautilus`. Il file dovrebbe contenere una lista delle possibili hotkey, con ogni linea immutata commentata con un header ";" che deve essere rimosso per attuare i cambiamenti (farlo diventare attivo).

### Pannelli ed applet non rispondono al click destro

Controllare la configurazione con un editor: /apps/metacity/general/mouse_button_modifier. Questi modificatori(`Alt`, `Super`, etc) sono utilizzati, oltre che per le normali finestre, anche per i pannelli e le applet.

### Mostra Desktop: la scorciatoia da tastiera non funziona

Gli sviluppatori GNOME hanno considerato l'associazione tasti corrispondente alla stregua di un [bug](https://bugzilla.gnome.org/show_bug.cgi?id=643609), visto che la funzione di minimizzazione è considerata deprecata. Per utilizzare di nuovo la funzione Mostra Desktop, assegnare la combinazione `ALT` + `CTRL` + `D` al comando "Hide all normal windows" facendo così:

Aprire `System Settings` (Clickare sul proprio nome → system settings) → `Keyboard` → `Shortcuts` → `Windows` → `Hide all normal windows`

### GNOME Files non si avvia

1.  Premere `ALT`+`F2`
2.  Inserire `gnome-tweak-tool`
3.  Selezionare il _File Manager_ tab.
4.  Localizzate l'opzione _Have file manager handle the desktop_ ed assicuratevi che sia settata su **off**.

### Impossibile applicare la configurazione memorizzata per i monitor

Se avete questo messaggio provate a disabilitare il plugin xrandr di gnome-settings-daemon:

 `$ dconf write /org/gnome/settings-daemon/plugins/xrandr/active false` 

### Pulsante di blocco non riesce a riattivare touchpad

Alcuni portatili hanno un pulsante di blocco del touchpad che disabilita il touchpad in modo che gli utenti possono digitare senza preoccuparsi di toccare il touchpad. Sembra che al momento Gnome possa bloccare il touchpad ma non sbloccarlo. In questo caso seguite le seguenti operazioni :

1.  Aprite un terminale. Potete farlo premendo `ALT`+`F2` , poi digitando `gnome-terminal` ed infine premere `ENTER`
2.  Scrivete il seguente comando :

 `$ xinput set-prop "SynPS/2 Synaptics TouchPad" "Device Enabled" 1` 

### Ctrl + V incolla il percorso invece dei files in GNOME Files

Se siete affetti da questo problema, editate `~/.gnome2/accels/nautilus` dove troverete le seguenti linee per Ctrl+V :

 `~/.gnome2/accels/nautilus` 

```
(gtk_accel_path "<Actions>/DirViewActions/Paste" "<Control>v")
...
(gtk_accel_path "<Actions>/ClipboardActions/Paste" "<Control>v")

```

Il problema sembra scaturire dalla seconda stringa, cancellate quella linea (la seconda) ed il problema sarà temporalmente risolto. Dovete ripetere questa fix dopo ogni update di Gnome.

Un'alternativa è quella di assegnare una differente combinazione di tasti a questa a zione.

### Impossibile collegarsi ad una rete wi-fi protetta

Potete vedere la lista delle connesioni network, ma scegliendo una rete protetta il programma va in errore e non riesce a mostrare la finestra di dialogo per l'ingresso della chiave. Potreste aver bisogno di installare network-manager-applet. Guardate anche [GNOME NetworkManager setup](/index.php/NetworkManager#GNOME "NetworkManager").

### "Ogni comando è stato definito 33"

Quando si preme `Stamp` per fare lo screenshot dello schermo e avete questo messaggio di ritorno : "Any command has been defined 33", installate metacity:

 `# pacman -S metacity` 

### GDM e Gnome usano il cursore di X11

Per correggere questo problema, avrete bisogno di eseguire i seguenti comandi come root in un terminale:

```
$ mkdir /usr/share/icons/default
$ cd /usr/share/icons/default
$ echo "[Icon Theme]" >> index.theme
$ echo "Inherits=Adwaita" >> index.theme
```

Alternativamente potete installare [gnome-cursors-fix](https://aur.archlinux.org/packages/gnome-cursors-fix/) da [AUR](/index.php/AUR "AUR").

## Links esterni

*   [Sito ufficiale di GNOME](http://www.gnome.org/)
*   Temi, icone e sfondi:
    *   [GNOME Art](http://art.gnome.org/)
    *   [GNOME Look](http://www.gnome-look.org/)
*   Programmi GTK/GNOME:
    *   [GNOME Files](http://www.gnomefiles.org/)
    *   [GNOME Project Listing](http://www.gnome.org/projects/)