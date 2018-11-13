Articoli correlati

*   [Desktop Environment](/index.php/Desktop_Environment_(Italiano) "Desktop Environment (Italiano)")
*   [Window Manager](/index.php/Window_Manager_(Italiano) "Window Manager (Italiano)")
*   [Xfwm](/index.php/Xfwm "Xfwm")
*   [Thunar](/index.php/Thunar_(Italiano) "Thunar (Italiano)")
*   [LXDE](/index.php/LXDE_(Italiano) "LXDE (Italiano)")
*   [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)")

Tratto da [Xfce - About](http://www.xfce.org/about/):

	*Xfce incarna la filosofia UNIX tradizionale di modularità e riutilizzabilità. Si compone di una serie di componenti che forniscono la completa funzionalità che si può aspettare da un ambiente desktop moderno. Essi sono distribuiti separatamente e si può scegliere tra i pacchetti disponibili per creare un ambiente ottimale di lavoro personale.*

Xfce è un [ambiente Desktop](/index.php/Desktop_environment_(Italiano) "Desktop environment (Italiano)") leggero e modulare, attualmente basato sule GTK+2 anche se in futuro potrebbe essere portato sulle GTK+3\. XFCE include una collezione di applicazioni come un gestore delle, un file manager ed un pannello per fornire un'esperienza utente completa. Xfce è molto popolare ed usato da molti utenti, in parte perché è leggero, ma anche perché una grande quantità delle impostazioni sono gestite tramite una GUI. Questo è in netto contrasto con i desktop come GNOME Shell che nascondono molte delle impostazioni all'utente.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Avviare Xfce](#Avviare_Xfce)
    *   [2.1 Login Grafico](#Login_Grafico)
    *   [2.2 Console virtuale](#Console_virtuale)
*   [3 Configurazione](#Configurazione)
    *   [3.1 Impostazioni di Xfconf](#Impostazioni_di_Xfconf)
        *   [3.1.1 Comandi per il gestore delle configurazioni](#Comandi_per_il_gestore_delle_configurazioni)
    *   [3.2 Menu](#Menu)
        *   [3.2.1 Sostituire l'applet del menu](#Sostituire_l'applet_del_menu)
        *   [3.2.2 Come rimuovere le voci dal menu di sistema](#Come_rimuovere_le_voci_dal_menu_di_sistema)
            *   [3.2.2.1 Metodo 1](#Metodo_1)
            *   [3.2.2.2 Metodo 2](#Metodo_2)
            *   [3.2.2.3 Metodo 3](#Metodo_3)
            *   [3.2.2.4 Metodo 4](#Metodo_4)
        *   [3.2.3 Applicazioni mancanti](#Applicazioni_mancanti)
    *   [3.3 Desktop](#Desktop)
        *   [3.3.1 Usare uno sfondo trasparente per il testo delle icone sul Desktop](#Usare_uno_sfondo_trasparente_per_il_testo_delle_icone_sul_Desktop)
        *   [3.3.2 Nascondere delle partizioni selezionate sul desktop](#Nascondere_delle_partizioni_selezionate_sul_desktop)
        *   [3.3.3 Passare al vecchio menu del tasto destro sul desktop senza le aggiunte di Thunar](#Passare_al_vecchio_menu_del_tasto_destro_sul_desktop_senza_le_aggiunte_di_Thunar)
        *   [3.3.4 Tasto di scelta rapida per uccidere le finestre](#Tasto_di_scelta_rapida_per_uccidere_le_finestre)
        *   [3.3.5 Gestire i tasti di scelta rapida](#Gestire_i_tasti_di_scelta_rapida)
    *   [3.4 Gestore delle finestre](#Gestore_delle_finestre)
        *   [3.4.1 Come attivare il compositor](#Come_attivare_il_compositor)
        *   [3.4.2 Arrotolare la finestra](#Arrotolare_la_finestra)
        *   [3.4.3 Disabilitare il ridisegno delle finestre ai bordi dello schermo](#Disabilitare_il_ridisegno_delle_finestre_ai_bordi_dello_schermo)
        *   [3.4.4 Rimpiazzare il gestore delle finestre nativo](#Rimpiazzare_il_gestore_delle_finestre_nativo)
            *   [3.4.4.1 Riattivazione degli effetti del Compositing](#Riattivazione_degli_effetti_del_Compositing)
    *   [3.5 Sessione](#Sessione)
        *   [3.5.1 Personalizzare l'avvio delle Applicazioni](#Personalizzare_l'avvio_delle_Applicazioni)
            *   [3.5.1.1 Attraverso il menu delle impostazioni](#Attraverso_il_menu_delle_impostazioni)
            *   [3.5.1.2 Attraverso uno script di avvio](#Attraverso_uno_script_di_avvio)
        *   [3.5.2 Bloccare lo schermo](#Bloccare_lo_schermo)
        *   [3.5.3 Cambiare utente](#Cambiare_utente)
        *   [3.5.4 Modificare le impostazioni dei file XML direttamente](#Modificare_le_impostazioni_dei_file_XML_direttamente)
    *   [3.6 Migliorare l'aspetto](#Migliorare_l'aspetto)
        *   [3.6.1 Come aggiungere temi a Xfce](#Come_aggiungere_temi_a_Xfce)
        *   [3.6.2 Integrazione dei temi delle applicazioni](#Integrazione_dei_temi_delle_applicazioni)
        *   [3.6.3 Cursori](#Cursori)
        *   [3.6.4 Icone](#Icone)
        *   [3.6.5 Fonts](#Fonts)
    *   [3.7 Suoni](#Suoni)
        *   [3.7.1 Configurazione di xfce4-mixer](#Configurazione_di_xfce4-mixer)
        *   [3.7.2 Xfce4-mixer con OSS4](#Xfce4-mixer_con_OSS4)
        *   [3.7.3 Cambiare il volume con i tasti multimediali della tastiera](#Cambiare_il_volume_con_i_tasti_multimediali_della_tastiera)
            *   [3.7.3.1 ALSA](#ALSA)
            *   [3.7.3.2 OSS](#OSS)
            *   [3.7.3.3 PulseAudio](#PulseAudio)
            *   [3.7.3.4 Xfce4-volumed](#Xfce4-volumed)
            *   [3.7.3.5 Volumeicon](#Volumeicon)
            *   [3.7.3.6 Tasti extra della tastiera](#Tasti_extra_della_tastiera)
        *   [3.7.4 Aggiungere un suono all'avvio/boot](#Aggiungere_un_suono_all'avvio/boot)
*   [4 Trucchi e Consigli](#Trucchi_e_Consigli)
    *   [4.1 Integrazione xdg-open (Applicazioni preferite)](#Integrazione_xdg-open_(Applicazioni_preferite))
    *   [4.2 Catturare schermate](#Catturare_schermate)
        *   [4.2.1 Catturare lo schermo col tasto stamp](#Catturare_lo_schermo_col_tasto_stamp)
    *   [4.3 Disabilitare le scorciatoie F1 e F11 del terminale](#Disabilitare_le_scorciatoie_F1_e_F11_del_terminale)
    *   [4.4 Temi o tavole di colore del terminale](#Temi_o_tavole_di_colore_del_terminale)
        *   [4.4.1 Cambiare colore del tema di default](#Cambiare_colore_del_tema_di_default)
        *   [4.4.2 Tema di colori tango per Terminal](#Tema_di_colori_tango_per_Terminal)
    *   [4.5 Gestione del colore](#Gestione_del_colore)
        *   [4.5.1 Caricare un profilo](#Caricare_un_profilo)
        *   [4.5.2 Creare un profilo](#Creare_un_profilo)
    *   [4.6 Monitor multipli](#Monitor_multipli)
    *   [4.7 Cartelle utente XDG](#Cartelle_utente_XDG)
    *   [4.8 SSH Agents](#SSH_Agents)
    *   [4.9 Funzionalità Bluetooth](#Funzionalità_Bluetooth)
    *   [4.10 Scorrere una finestra di sfondo , senza azionare il focus su di esso](#Scorrere_una_finestra_di_sfondo_,_senza_azionare_il_focus_su_di_esso)
*   [5 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [5.1 Operazioni " Non Autorizzato" quando si tenta di montare un dispositivo con un file manager](#Operazioni_"_Non_Autorizzato"_quando_si_tenta_di_montare_un_dispositivo_con_un_file_manager)
    *   [5.2 xfce4-power-manager](#xfce4-power-manager)
    *   [5.3 xfce4 continua a spegnere il monitor](#xfce4_continua_a_spegnere_il_monitor)
    *   [5.4 xfce4-xkb-plugin](#xfce4-xkb-plugin)
    *   [5.5 Locales ignorato con GDM](#Locales_ignorato_con_GDM)
    *   [5.6 Ripristinare le impostazioni predefinite](#Ripristinare_le_impostazioni_predefinite)
    *   [5.7 Le icone del desktop si ricompongono in Xfce](#Le_icone_del_desktop_si_ricompongono_in_Xfce)
    *   [5.8 NVIDIA e xfce4-sensors-plugin](#NVIDIA_e_xfce4-sensors-plugin)
    *   [5.9 Fallimento della sessione](#Fallimento_della_sessione)
    *   [5.10 Le preferenze per le applicazioni preferite non hanno effetto](#Le_preferenze_per_le_applicazioni_preferite_non_hanno_effetto)
    *   [5.11 Pulsanti di azione/icone mancanti](#Pulsanti_di_azione/icone_mancanti)
    *   [5.12 Abilitare cedilla ç/Ç al posto di of ć/Ć](#Abilitare_cedilla_ç/Ç_al_posto_di_of_ć/Ć)
    *   [5.13 Caratteri non ASCII al montaggio di penne USB =](#Caratteri_non_ASCII_al_montaggio_di_penne_USB_=)
    *   [5.14 Video tearing quando il composite Xfwm è abilitato](#Video_tearing_quando_il_composite_Xfwm_è_abilitato)
    *   [5.15 Caratteri sfocati e distorti quando compositing è abilitato (schede Intel)](#Caratteri_sfocati_e_distorti_quando_compositing_è_abilitato_(schede_Intel))
    *   [5.16 I temi GTK non funzionano su monitor multipli](#I_temi_GTK_non_funzionano_su_monitor_multipli)
*   [6 Fonti Esterne](#Fonti_Esterne)

## Installazione

Xfce può essere installato dal gruppo [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/), che è disponibile nei repository ufficiali. Si consiglia di installare anche il gruppo [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/) che include plugin aggiuntivi e una serie di utility utili come l'editor [mousepad](https://www.archlinux.org/packages/?name=mousepad).

## Avviare Xfce

### Login Grafico

Semplicemente si scelga la sessione "Xfce" dal proprio [Display Manager](/index.php/Display_manager_(Italiano) "Display manager (Italiano)") utilizzato.

### Console virtuale

Ci sono due metodi per avviare manualmente Xfce :

*   Eseguire `startxfce4` direttamente dalla console.
*   Configurare `~/.xinitrc` aggiungendo `exec startxfce4` ed usare `xinit` o `startx` da console. Vedere [xinitrc](/index.php/Xinitrc_(Italiano) "Xinitrc (Italiano)") per i dettagli.

**Nota:** Il comando corretto per il lancio di Xfce è `startxfce4`, non inizializzatelo direttamente `xfce4-session`, dal momento che è già gestito da `startxfce4` stesso.

## Configurazione

### Impostazioni di Xfconf

Xfconf è il sistema di XFCE per memorizzare le opzioni di configurazione, e molte delle configurazioni di XFCE avviene tramite le modifiche effettuate in xfconf (un modo o nell'altro). Ci sono diversi modi per modificare queste impostazioni :

*   Il modo più ovvio e più semplice è quello di andare su "Impostazioni" nel menu principale e selezionare la categoria che si desidera personalizzare. Tuttavia, non sono disponibili tutte le opzioni di personalizzazione in questo modo.
*   Un modo meno user-friendly, ma più generale è quello di andare in `Main Menu - > Impostazioni -> Editor delle Impostazioni` dove si possono vedere e modificare tutte le opzioni di personalizzazione. Tutte le impostazioni modificate qui avranno effetto immediato. L'Editor delle impostazioni può anche essere lanciato da riga di comando invocando `xfce4-settings-editorxfce4`.
*   La personalizzazione può essere fatta completamente da linea di comando usando il programma `xfconf-query`. Vedere [la documentazione in linea di XFCE](http://docs.xfce.org/xfce/xfconf/xfconf-query) per maggiori informazioni ed esempi e il resto di questa pagina wiki per ulteriori esempi. Le modifiche alle impostazioni modificate effettuate qui avranno effetto immediato.
*   Le impostazioni vengono memorizzate in file XML in `~/.config/xfce4/xfconf/xfce-perchannel-xml/` che possono essere modificati manualmente. Tuttavia, le modifiche apportate qui non avranno effetto immediato.
*   Per maggiori informazioni: [documentazione xfconf](http://docs.xfce.org/xfce/xfconf/start).

#### Comandi per il gestore delle configurazioni

Non c'è una documentazione ufficiale per i comandi eseguiti dal gestore delle configurazioni. Potete dare un'occhiata ai file `.desktop` presenti nella cartella `/usr/share/applications`. Per quelli che vogliono sapere esattamente cosa sta eseguendo il pc, ecco una lista dei comandi che vengono eseguiti, utile per capirne un po' di più:

```
xfce4-accessibility-settings
xfce4-power-manager-settings
xfce4-settings-editor
xfdesktop-settings
xfce4-display-settings
xfce4-keyboard-settings
xfce4-mouse-settings
xfce4-session-settings
xfce4-settings-manager
xfce4-appearance-settings
xfwm4-settings
xfwm4-tweaks-settings
xfwm4-workspace-settings
orage -p

```

Per avere una lista di tutti i comandi installati a disposizione del manager delle configurazioni, eseguite questo comando nel terminale:

```
$ grep '^Exec=' /usr/share/applications/xfce*settings* | sed -e 's_^.*=_ _'

```

### Menu

#### Sostituire l'applet del menu

[Whisker Menu](http://gottcode.org/xfce4-whiskermenu-plugin/) è un sostituto completo per l'applet del menu presente di default in Xfce. Aggiungerlo al proprio pannello ed eventualmente rimuovere il menu di default già presente.

É reperibile su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") con il pacchetto [xfce4-whiskermenu-plugin](https://www.archlinux.org/packages/?name=xfce4-whiskermenu-plugin).

#### Come rimuovere le voci dal menu di sistema

##### Metodo 1

Con l'editor del menu integrato, non potete rimuovere le voci dal menu Sistema. Ecco come fare per nasconderle:

1.  Aprire un terminale (Menu principale > Sistema > Terminale di Xfce) e andare nella cartella `/usr/share/applications`: `$ cd /usr/share/applications` 
2.  Questa cartella sarà piena di file .desktop. Per vedere quanti, usate il comando : `$ ls` 
3.  Aggiungere `NoDisplay=true` al file `.desktop`. Per esempio, supponendo che la voce che si vuole modificare sia Firefox. Scrivere nel terminale: `# echo "NoDisplay=true" >> firefox.desktop` Questo comando inserirà la stringa `NoDisplay=true` al fondo del file `.desktop`.

##### Metodo 2

Un altro metodo consiste nel copiare l'intero contenuto della cartella delle applicazioni globali sopra la propria cartella di applicazioni locali, quindi procedere a modificare e/o disabilitare le scorciatoie .desktop indesiderate. Questo permetterà di mantenere gli aggiornamenti delle applicazioni che scriveranno le modifiche su `/usr/share/applications/`.

1.  In un terminale, copiare tutto da `/usr/share/applications` in `~/.local/share/applications/`: `$ cp /usr/share/applications/* ~/.local/share/applications/` 
2.  Per qualsiasi elemento non desiderato nel menù, aggiungere l'opzione `NoDisplay=true`: `$ echo "NoDisplay=true" >> ~/.local/share/applications/foo.desktop` 

È possibile anche editare la categoria delle applicazioni modificando il file `.desktop` con un editor di testi e modificare la linea `Categories=`.

##### Metodo 3

Il terzo metodo è quello **più pulito** e consigliato nel [wiki di Xfce](http://wiki.xfce.org/howto/customize-menu). Creare il file `~/.config/menus/xfce-applications.menu` e copiarci dentro il seguente contenuto :

```
<!DOCTYPE Menu PUBLIC "-//freedesktop//DTD Menu 1.0//EN"
  "[http://www.freedesktop.org/standards/menu-spec/1.0/menu.dtd](http://www.freedesktop.org/standards/menu-spec/1.0/menu.dtd)">

<Menu>
    <Name>Xfce</Name>
    <MergeFile type="parent">/etc/xdg/menus/xfce-applications.menu</MergeFile>

    <Exclude>
        <Filename>xfce4-run.desktop</Filename>

        <Filename>exo-terminal-emulator.desktop</Filename>
        <Filename>exo-file-manager.desktop</Filename>
        <Filename>exo-mail-reader.desktop</Filename>
        <Filename>exo-web-browser.desktop</Filename>

        <Filename>xfce4-about.desktop</Filename>
        <Filename>xfhelp4.desktop</Filename>
    </Exclude>

    <Layout>
        <Merge type="all"/>
        <Separator/>

        <Menuname>Settings</Menuname>
        <Separator/>

        <Filename>xfce4-session-logout.desktop</Filename>
    </Layout>

</Menu>

```

Il tag `<MergeFile>` include il menu di Xfce di default nel nostro file. Questo è importante.

Il tag `<Exclude>` esclude le applicazioni che non vogliamo visualizzare nel menu. Qui abbiamo escluso alcune scorciatoie predefinite di Xfce, ma è possibile escludere `firefox.desktop` o qualsiasi altra applicazione.

Il tag `<Layout>` definisce il layout del menu . Le applicazioni possono essere organizzati in cartelle o comunque si desiderano. Per maggiori dettagli consultare la pagina wiki di Xfce citata.

##### Metodo 4

Alternativamente può essere utilizzato uno strumento chiamato [xame](http://www.redsquirrel87.com/XAME.html). XAME è uno strumento ad interfaccia grafica scritta in Gambas e progettato specificamente per la modifica dei menu interi in Xfce, non funzionerà in altri ambienti. XAME è disponibile nel pacchetto [xame](https://aur.archlinux.org/packages/xame/) su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)"). Un'alternativa a XAME che funziona abbastanza bene su Xfce è [menulibre](https://aur.archlinux.org/packages/menulibre/).

#### Applicazioni mancanti

Quando sono installate alcune applicazioni (per esempio tramite [Wine](/index.php/Wine "Wine")), non possono essere elencate in `/usr/share/applications`. Alcuni collegamenti che appaiono nella categoria "Altri" si trovano in questa cartella: `~/.local/share/applications/wine/`

### Desktop

#### Usare uno sfondo trasparente per il testo delle icone sul Desktop

Per cambiare lo sfondo bianco di default del testo delle icone sul Desktop con qualcosa di più carino, creare o modificate il file di configurazione GTK

 `~/.gtkrc-2.0` 
```
style "xfdesktop-icon-view" {
    XfdesktopIconView::label-alpha = 10
    base[NORMAL] = "#000000"
    base[SELECTED] = "#71B9FF"
    base[ACTIVE] = "#71B9FF"
    fg[NORMAL] = "#fcfcfc"
    fg[SELECTED] = "#ffffff"
    fg[ACTIVE] = "#ffffff"
}
widget_class "*XfdesktopIconView*" style "xfdesktop-icon-view"

```

#### Nascondere delle partizioni selezionate sul desktop

Se si desidera evitare che alcune partizioni o dispositivi appaiano sul desktop, è possibile creare una regola di udev, ad esempio il file `/etc/udev/rules.d/10-local.rules`:

```
KERNEL=="sda1", ENV{UDISKS_PRESENTATION_HIDE}="1"
KERNEL=="sda2", ENV{UDISKS_PRESENTATION_HIDE}="1"

```

mostrerà sul desktop tutte le partizioni eccetto sda1 e sda2\. Se si utilizza udisk2 quanto sopra non funziona , a causa della UDISKS_PRESENTATION_HIDE essere non più supportato , invece è necessario utilizzare UDISKS_IGNORE come segue:

```
KERNEL=="sda1", ENV{UDISKS_IGNORE}="1"
KERNEL=="sda2", ENV{UDISKS_IGNORE}="1"

```

#### Passare al vecchio menu del tasto destro sul desktop senza le aggiunte di Thunar

```
xfconf-query -c xfce4-desktop -v --create -p /desktop-icons/style -t int -s 0

```

#### Tasto di scelta rapida per uccidere le finestre

Xfce non supporta una scorciatoia per *uccidere le finestre* direttamente, ma è possibile aggiungere una con un semplice script. Assicurarsi di avere installato il pacchetto [xorg-xkill](https://www.archlinux.org/packages/?name=xorg-xkill).

Create uno script `~/.config/xfce4/killwindow.sh` con il seguente contenuto e rendetelo eseguibile (potete usare `chmod 755 killwindow.sh`).

```
xkill -id "`xprop -root -notype | sed -n '/^_NET_ACTIVE_WINDOW/ s/^.*# *\|\,.*$//g p'`"

```

Ora non resta che associare un tasto allo script utilizzando `Impostazioni -> Tastiera`.

#### Gestire i tasti di scelta rapida

Le scorciatoie da tastiera possono essere gestiti con l'applicazione Gestione impostazioni di Xfce, che è disponibile tramite il [pacchetto](/index.php/Pacman_(Italiano)#Installare_pacchetti_specifici "Pacman (Italiano)") [xfce4-settings](https://www.archlinux.org/packages/?name=xfce4-settings) e il [gruppo](/index.php/Pacman_(Italiano)#Installare_gruppi_di_pacchetti "Pacman (Italiano)") [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/). Il Settings Manager può essere avviato dal menu applicazioni ( fare clic su Impostazioni -> Tastiera ) o da riga di comando (`xfce4-keyboard-settings`). La documentazione di Xfce comprende [istruzioni dettagliate](http://docs.xfce.org/xfce/xfce4-settings/keyboard#application_shortcuts) per utilizzare il gestore delle impostazioni.

### Gestore delle finestre

Il gestore delle finestre predefinito di Xfce è [Xfwm](/index.php/Xfwm "Xfwm").

#### Come attivare il compositor

Xfce include un compositor che aggiunge le opzioni per gli effetti delle finestre, le ombre, la trasparenza ecc. Può essere attivato nel menù Window Manager Tweaks ed è attivabile al momento. Non sono necessarie ulteriori impostazioni nel file `/etc/xorg.conf`. Per abilitarlo e configurare le impostazioni andare in:

```
Menu --> Impostazioni --> Regolazioni del gestore delle finestre

```

**Suggerimento:** Il compositor integrato per Xfwm (il window manager di Xfce) è spesso causa di problemi video nelle applicazioni. Se si desidera un compositore leggero, con alcuni effetti minimi, è possibile utilizzare [Compton](/index.php/Compton "Compton").

#### Arrotolare la finestra

Facendo doppio click sulla barra del titolo o cliccando sul menu della finestra e scegliendo 'Arrotola', farà sì che il contenuto della finestra scompaia, lasciando solo la barra del titolo. Se si desidera disattivare questa funzionalità è possibile farlo graficamente usando l'editor xconf o attraverso la linea di comando, come illustrato di seguito , che ottiene lo stesso risultato .

`xfconf-query -c xfwm4 -p /general/mousewheel_rollup -s false`

#### Disabilitare il ridisegno delle finestre ai bordi dello schermo

Xfwm4 ha la capacità di "Riquadrare" una finestra automaticamente quando viene spostato al bordo dello schermo ridimensionandola per riempire la metà superiore dello schermo. (Il sito ufficiale XFCE dice che questa funzione è disattivata per impostazione predefinita in XFCE 4.10, ma sembra essere abilitata di default su Arch Linux.) Questo comportamento può essere attivato o disattivato in `Regolazioni del gestore delle finestre --> Accessibilità --> Riquadra automaticamente le finestre quando raggiungono i bordi dello schermo`, oppure con :

```
xfconf-query -c xfwm4 -p /general/tile_on_move -s false  # per disabilitare
xfconf-query -c xfwm4 -p /general/tile_on_move -s true   # per abilitare

```

#### Rimpiazzare il gestore delle finestre nativo

Per sostituire xfwm4 con un altro [Window manager (Italiano)](/index.php/Window_manager_(Italiano) "Window manager (Italiano)") è possibile utilizzare la sintassi 'nome del window manager ' '-- replace' in un terminale.

Alcuni esempi:

*   Per [openbox](https://www.archlinux.org/packages/?name=openbox) il comando è: `openbox --replace`
*   Per [metacity](https://www.archlinux.org/packages/?name=metacity) il comando è: `metacity --replace`

Per ripristinare il window manager nativo di nuovo, per prima cosa terminare il comando precedente premendo `CTRL` e `c`, quindi immettere il seguente comando :

```
 $ xfwm4 --replace

```

Una volta che l'altro window manager è stato avviato si può semplicemente **salvare la sessione**. L'opzione `Salva sessione per i login futuri` è disponibile nella finestra di dialogo `Esci...` . É anche importante notare che, quando si ripristina `xfwm4` durante una sessione, l'opzione `Salva sessione per i login futuri` dovrà essere attivata in quell'occasione per rendere permanente questa modifica . Non farlo potrebbe causare che il precedente gestore delle finestre sia avviato nuovamente, in quanto verrebbe caricata la sessione precedentemente salvata. Tuttavia, una volta che `xfwm4` è stato reimpostato, dalla prossima sessione in poi non ci sarà più alcuna necessità di salvare le sessioni future.

In alternativa è possibile aggiungere il window manager all'elenco autostart in Xfce. Per fare questo, dal menu principale, selezionare prima `Settings Manager` e quindi `sessione e avvio`. Una volta che si apre la finestra dell'applicazione , selezionare la voce `Application Autostart` per visualizzare tutte le applicazioni e i programmi avviati automaticamente, fare clic sul pulsante `Aggiungi` per far apparire la finestra `Aggiungi Applicazione`.

I seguenti dati possono essere inseriti per ogni campo :

*   **Nome**: openbox-wm
*   **Descrizione**: openbox-wm
*   **Comando**: openbox --replace

**Suggerimento:**

*   Nome e descrizione non sono campi importanti, e sono lì solo per indicare cosa fa il comando. La sezione di comando ha la stessa sintassi come nei precedenti esempi, 'Nome del window manager ' '--replace '.
*   Compiz può esigere comandi diversi da quelli indicati in quanto vi sono diversi modi per avviarlo. Per maggiori informazioni si prega di consultare l'articolo [Compiz](/index.php/Compiz_(Italiano) "Compiz (Italiano)")

Una volta completata, fare clic su `OK`, assicurarsi che la casella di controllo accanto alla voce `openbox-wm` sia spuntata, e quindi riavviare la sessione per rendere la modifica effettiva. Il vantaggio di questo metodo è che le applicazioniavviate automaticamente possono essere facilmente attivate/disattivate a piacimento attraverso le loro caselle di avvio automatico. Di conseguenza, per consentire al window manager nativo - `xfwm4` - di riprendere, basta deselezionare deselezionare la voce `openbox-wm` e riavviare la sessione.

##### Riattivazione degli effetti del Compositing

Se si sostituisce xfwm4 con un gestore di finestre che non dispone di un composite manager , allora è possibile utilizzare un autonomo composite manager come [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") o [Compton](/index.php/Compton "Compton").

### Sessione

#### Personalizzare l'avvio delle Applicazioni

##### Attraverso il menu delle impostazioni

Per avviare un'applicazione automaticamente all'avvio di Xfce, andare su `menu > impostazioni > Sessione e Avvio > Avvio Automatico`. Verrà visualizzato un elenco dei programmi che vengono lanciati all'avvio. Per aggiungere una voce, fare clic sul pulsante "Aggiungi" e compilare il modulo, specificando il percorso di un file eseguibile che si desidera eseguire .

##### Attraverso uno script di avvio

In alternativa è possibile utilizzare questo metodo , per eseguire uno script a riga di comando per avviare le applicazioni . Ciò include l'ottenimento delle variabili d'ambiente necessarie nel tempo d'avvio della GUI.

*   Copiare il file `/etc/xdg/xfce4/xinitrc` in `~/.config/xfce4/`
*   Modificare questo file. Ad esempio, si può aggiungere qualcosa del genere da qualche parte a metà:

```
   source $HOME/.bashrc
   # start rxvt-unicode server
   urxvtd -q -o -f

```

#### Bloccare lo schermo

Per bloccare la sessione di Xfce4 (attraverso `xflock4`), uno tra i seguenti pacchetti deve essere installato : [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver), [gnome-screensaver](https://www.archlinux.org/packages/?name=gnome-screensaver) (le cui impostazioni possono essere modificate con [dconf-editor](/index.php?title=Dconf-editor&action=edit&redlink=1 "Dconf-editor (page does not exist)") sotto org>gnome>desktop>screensaver), [slock](https://www.archlinux.org/packages/?name=slock) o [xlockmore](https://www.archlinux.org/packages/?name=xlockmore). [XScreenSaver](/index.php/XScreenSaver "XScreenSaver") è l'opzione consigliata. Si prega di consultare il relativo wiki per maggiori informazioni.

#### Cambiare utente

Xfce4 ha il supporto per il cambio utente quando viene utilizzato con un [Display manager (Italiano)](/index.php/Display_manager_(Italiano) "Display manager (Italiano)") che ha questa funzionalità - esempi sono [LightDM](/index.php/LightDM "LightDM") e [GDM](/index.php/GDM "GDM"). Si prega di consultare la pagina wiki del display manager per maggiori informazioni. Quando si dispone di un display manager installato e configurato correttamente è possibile cambiare utente dalla voce del menu 'pulsanti di azione' presente nel pannello.

#### Modificare le impostazioni dei file XML direttamente

Potrebbe essere utile, specialmente quando si effettua un aggiornamento, editare manualmente i file con estensione .xml nella cartella `~/.config/xfce4/xfconf/`. Ad esempio per le scorciatoie di tastiera delle applicazioni, il file è `~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-keyboard-shortcuts.xml`.

### Migliorare l'aspetto

#### Come aggiungere temi a Xfce

1\. Andare sul sito [xfce-look.org](http://xfce-look.org) e cliccare "Themes" nella opzioni di scelta a sinistra. Scegliere un tema e cliccare su "Download".

2\. Aprire la cartella dove è stato scaricato il file ed estrarne il contenuto usando gestore di archivi come [file-roller](https://www.archlinux.org/packages/?name=file-roller).

3\. Spostare la cartella estratta in `/usr/share/themes` (per tutti gli utenti) o `~/.themes` (per il proprio utente). All'interno di `/usr/share/themes/abc` c'è una cartella che si crea chiamata xfwm4 che conterrà tutti file che sono inclusi con quel tema.

4\. Selezionare un tema.

*   I temi GTK+ possono essere cambiati in:

```
Menu --> Impostazioni --> Aspetto

```

*   I temi per xfwm4 possono essere cambiati in:

```
Menu --> Impostazioni --> Gestore delle finestre

```

#### Integrazione dei temi delle applicazioni

Le applicazioni non hanno sempre un aspetto coerente . Ci sono due possibili ragioni per questo :

1 . L'applicazione si basa su un toolkit che il tema corrente non supporta. Le applicazioni basate sul toolkit GTK+2 avrà bisogno di un tema GTK+2, mentre le applicazioni basate su GTK+3 avranno bisogno di un tema GTK+3.

2 . Il tema non è aggiornato .

Per ottenere un aspetto uniforme per tutte le applicazioni, è consigliabile utilizzare un tema aggiornato GTK+3 come Advaita, che come tema GTK+3 ha il supporto integrato per le applicazioni GKT+2 . Advaita può essere installato dal pacchetto [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard). Le applicazioni basate sul toolkit Qt sono in grado di simulare l'attuale tema GTK+ usando { {ic|qtconfig-qt4}} .

per maggiori informazioni consultare [GTK+#GTK+ 3.x](/index.php/GTK%2B#GTK+_3.x "GTK+") per GTK3 e [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications") per Qt.

#### Cursori

Si veda [X11 Cursors](/index.php/X11_Cursors "X11 Cursors").

Di base, X usa un cursore nero semplice. Nel caso si abbiano installati cursori di X alternativi, Xfce può trovarli in

```
Menu --> Impostazioni --> Mouse --> Temi

```

#### Icone

1.  Per prima cosa, trovare e scaricare il set di icone desiderato. Link consigliati per scaricare le icone sono da [Customize.org](http://www.customize.org), [Opendesktop.org](http://opendesktop.org) e [Xfce-look.org](http://xfce-look.org/); anche [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") fornisce diversi PKGBUILD per i pacchetti di icone.
2.  Passare alla directory in cui è stato scaricato il set di icone ed estrarlo. Esempio `tar -xzf /home/utente/downloads/icon-pack.tar.gz`.
3.  Spostare la cartella estratta che contiene le icone in `~/.icons` (se si desidera utilizzare le icone solo per il proprio utente) oppure in `/usr/share/icons` (se si desidera che tutti gli utenti su il sistema possono far uso delle icone), e nel caso si consideri la creazione di un [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") per questo.
4.  Opzionale: eseguire `gtk-update-icon-cache -f -t ~/.icons/<theme_name>` per aggiornare la cache delle icone
5.  Impostare le icone andando su :

```
Menu -> Impostazioni -> Aspetto -> Icone 

```

Quando si hanno problemi con un tema di icone, è anche consigliato di installare il pacchetto [hicolor-icon-theme](https://www.archlinux.org/packages/?name=hicolor-icon-theme) se non è stato già installato .

#### Fonts

Se si riscontrano problemi di visualizzazione dei font predefiniti, provate ad aprire Impostazioni -> Aspetto, cliccate sulla scheda "fonts" ed impostate "Usa Hinting" su "Totale"

Si potrebbe anche provare a utilizzare un impostazione DPI personalizzata.

### Suoni

#### Configurazione di xfce4-mixer

[xfce4-mixer](https://www.archlinux.org/packages/?name=xfce4-mixer) è un mixer con GUI che si applica come plugin nel pannello e sviluppata dal team di Xfce . É parte del gruppo xfce4, quindi probabilmente lo avrete già installato. Xfce 4.6 usa GStreamer come backend per controllare il volume, quindi prima bisogna fare in modo che gstreamer cooperi con xfce4-mixer. Uno o più pacchetti del plugin di GStreamer elencati come dipendenze opzionali di xfce4-mixer devino essere installati. Senza uno di questi pacchetti, richiesti dal plugin, apparirà il seguente errore quando si effettua il clic sulla voce del pannello del mixer.

```
 GStreamer was unable to detect any sound devices. Some sound system specific GStreamer packages may be missing. 

```

I plugin richiesti dipendono dall'hardware. Alla maggior parte delle persone dovrebbe andare bene con [gstreamer0.10-base-plugins](https://aur.archlinux.org/packages/gstreamer0.10-base-plugins/) che può essere [installato](/index.php/Pacman_(Italiano) "Pacman (Italiano)") dai [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

Se la voce del pannello xfce4-mixer era già in esecuzione prima di installare uno dei pacchetti di plugin, bisogna uscire dalla sessione e rientrarvi nuovamente per vedere se funziona correttamente, o semplicemente rimuovere il plugin mixer dal pannello e aggiungerlo di nuovo. Se non funziona, potrebbe essere necessario avere più o diversi plugin gstreamer. Provare a installare il pacchetto [gstreamer0.10-good-plugins](https://aur.archlinux.org/packages/gstreamer0.10-good-plugins/) o [gstreamer0.10-bad-plugins](https://aur.archlinux.org/packages/gstreamer0.10-bad-plugins/).

Se si dovesse cambiare la scheda audio di riferimento nel mixer, allora si dovrebbe effettuare il logout e rientrare nella sessione per sentire nuovamente il suono.

Per ulteriori dettagli, ad esempio come impostare la scheda audio di default, vedere [ALSA](/index.php/Advanced_Linux_Sound_Architecture_(Italiano) "Advanced Linux Sound Architecture (Italiano)"). In alternativa è possibile utilizzare [PulseAudio](/index.php/PulseAudio_(Italiano) "PulseAudio (Italiano)") insieme con [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol).

#### Xfce4-mixer con OSS4

Se avete provato la sezione qui sopra per ottenere [xfce4-mixer](https://www.archlinux.org/packages/?name=xfce4-mixer) funzionante ma non funziona comunque, allora potrebbe essere necessario compilarsi per se [gstreamer0.10-good-plugins](https://aur.archlinux.org/packages/gstreamer0.10-good-plugins/). Si scarichi il PKGBUILD e gli altri file necessari da ABS o [qui](https://repos.archlinux.org/wsvn/packages/gstreamer0.10-good/repos/extra-i686/), modificare il PKGBUILD, aggiungendo --enable-oss.

```
./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var \
  **--enable-oss \**
  --disable-static --enable-experimental \
  --disable-schemas-install \
  --disable-hal \
  --with-package-name="GStreamer Good Plugins (Archlinux)" \
  --with-package-origin="[https://www.archlinux.org/](https://www.archlinux.org/)"

```

Successivamente lanciate il comando makepkg -i.

```
 makepkg -i

```

LINK utili: [OSS forum](http://www.4front-tech.com/forum/)

#### Cambiare il volume con i tasti multimediali della tastiera

Andare in

```
Impostazioni > Tastiera

```

Cliccare sulla scheda "Scorciatoie" e successivamente sul pulsante "Aggiungi". Aggiungere inserendo il comando desiderato, quindi premere il tasto corrispondente nella schermata successiva:

##### ALSA

Per il pulsante che aumenta il volume

```
amixer set Master 5%+

```

Per il pulsante che abbassa il volume

```
amixer set Master 5%-

```

Per il pulsante muto/non-muto

```
amixer set Master toggle

```

È possibile anche lanciare questi comandi per impostare i comandi indicati sopra con le scorciatoie standard di XF86Audio:

```
xfconf-query -c xfce4-keyboard-shortcuts -p /commands/custom/XF86AudioRaiseVolume -n -t string -s "amixer set Master 5%+ unmute"
xfconf-query -c xfce4-keyboard-shortcuts -p /commands/custom/XF86AudioLowerVolume -n -t string -s "amixer set Master 5%- unmute"
xfconf-query -c xfce4-keyboard-shortcuts -p /commands/custom/XF86AudioMute -n -t string -s "amixer set Master toggle"

```

Se `amixer set Master toggle` non dovesse funzionare, provare invece con il canale PCM (`amixer set PCM toggle`).

Il canale deve avere una opzione 'mute' per passare il comando. Per verificare se il proprio canale Master supporta la commutazione *mute*, eseguire `alsamixer` in un terminale e cercare la doppia M (MM) con il canale Master. Se non sono presenti non supporta l'opzione muto. Se, per esempio, si desidera cambiare il tasto toggle affinché usi il canale PCM, assicurarsi di impostare anche il canale PCM come Mixer Track nelle proprietà del Mixer di Xfce.

##### OSS

Utilizzare uno di questi scripts: [[1]](http://www.opensound.com/wiki/index.php/Tips_And_Tricks#Using_multimedia_keys_with_OSS)

Se si utilizza ossvol (raccomandato), aggiungere:

```
ossvol -i 1

```

per il pulsante che aumenta il volume

```
ossvol -d 1

```

per il pulsante che diminuisce il volume

```
ossvol -t

```

per il pulsante muto/non-muto

##### PulseAudio

Per il pulsante che aumenta il volume

```
sh -c "pactl set-sink-mute 0 false ; pactl set-sink-volume 0 +1%"

```

Per il pulsante che abbassa il volume

```
sh -c "pactl set-sink-mute 0 false ; pactl -- set-sink-volume 0 -1%"

```

Per il pulsante muto/non-muto

```
pactl set-sink-mute 0 toggle

```

Queste impostazioni assumono il dispositivo che si vuole controllare ha indice 0\. Utilizzare `pactl list sinks short` per la lista.

##### Xfce4-volumed

Il demone [xfce4-volumed](https://aur.archlinux.org/packages/xfce4-volumed/) mappa automaticamente tasti del volume della vostra tastiera per Xfce-mixer. Inoltre si ottiene l'OSD attraverso Xfce4-notifyd quando si cambia il volume. Xfce4-volumed non necessita di alcuna configurazione e viene avviato automaticamente con Xfce.

Se si utilizza PulseAudio e attivando xfce4-volumed non funziona, modificare i comandi di tastiera per i comandi pactl per PulseAudio come indicato sopra nella sezione pulseaudio:

##### Volumeicon

[volumeicon](https://www.archlinux.org/packages/?name=volumeicon) è un'alternativa a xfce4-volumed, reperibile nel repositorio "community", che permette la gestione dei tasti di scelta rapida e le notifiche attraverso [xfce4-notifyd](https://www.archlinux.org/packages/?name=xfce4-notifyd).

##### Tasti extra della tastiera

Se si proviene da un'altra distribuzione, si può essere interessati a consentire tasti aggiuntivi sulla tastiera, vedere [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys").

#### Aggiungere un suono all'avvio/boot

Arch non ha compilato lo strumento di configurazione del suono in avvio, ma c'è una soluzione aggiungendo il seguente comando per le impostazioni di avvio automatico in Avvio e Sessione :

```
aplay /boot/startupsound.wav

```

Il percorso del file e il nome del file può essere quello che si vuole, ma chiamandolo in modo descrittivo e posizionandolo in /boot mantiene le cose in ordine .

## Trucchi e Consigli

### Integrazione xdg-open (Applicazioni preferite)

La maggior parte delle applicazioni si basano su [xdg-open](/index.php/Xdg-open "Xdg-open") per aprire una applicazione preferita per un determinato file o URL. Affinché xdg-open e xdg-settings per rilevino e si integrino correttamente con l'ambiente desktop XFCE, è necessario [installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") il pacchetto [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop).

Se non lo si fa, non verranno rispettate le preferenze delle applicazioni preferite (impostate da da exo-preferred-applications). Invece installare il pacchetto e consentendo ad xdg-open di rilevare ciò che si sta eseguendo su XFCE, inoltrerà tutte le chiamate a exo-open, che utilizzerà correttamente tutte le preferenze delle applicazioni preferite.

Per assicurarsi che l'integrazione xdg-open funzioni correttamente, chiedere ad xdg-settings per il browser web predefinito e vedere che quale sia il :

```
# xdg-settings get default-web-browser

```

Se risponde con :

```
xdg-settings: unknown desktop environment

```

vuol dire che non è riuscita a rilevare XFCE come ambiente desktop, che è probabilmente dovuto al pacchetto [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) mancante .

### Catturare schermate

XFCE ha un proprio strumento di screenshot, [xfce4-screenshooter](https://www.archlinux.org/packages/?name=xfce4-screenshooter). Fa parte del gruppo di [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/).

#### Catturare lo schermo col tasto stamp

Andare in

```
Xfce-menu --> Imnpostazioni --> Tastiera >>>  Scorciatoie Applicazione

```

Aggiungete il comando "xfce4-screenshooter -f" ed impostare il tasto "stamp" (o Print), al fine di catturare una schermata a schermo intero. Vedere la pagina man di screenshooter per altri argomenti opzionali.

In alternativa, un programma di cattura schermo indipendente come [scrot](/index.php/Taking_a_screenshot#scrot "Taking a screenshot") può essere utilizzato.

### Disabilitare le scorciatoie F1 e F11 del terminale

Il terminale di Xfce utilizza F1 e F11 rispettivamente per il menu Help e la funzionalità a tutto schermo, ciò rende difficoltoso utilizzare programmi da terminale come htop. Per disabilitare questi collegamenti, creare o modificare il file di configurazione , poi disconnettersi e riconnettersi dentro. F10 può essere disabilitato nel menu Preferenze.

 `~/.config/xfce4/terminal/accels.scm` 
```
(gtk_accel_path "<Actions>/terminal-window/fullscreen" "")
(gtk_accel_path "<Actions>/terminal-window/contents" "")

```

### Temi o tavole di colore del terminale

Temi o tavole di colore del terminale possono essere modificati tramite interfaccia grafica nella scheda Colori e Aspetto nelle Preferenze. Questi sono i colori che sono disponibili per le maggiori applicazioni da console come [emacs](/index.php/Emacs "Emacs"), [vi](/index.php/Vi "Vi") , e così via . Le loro impostazioni vengono memorizzate individualmente per ogni utente del sistema nel file `~/.config/xfce4/terminal/terminalrc`. Ci sono anche tanti altri temi tra cui scegliere. Controllare la discussione sul forum [Colour Scheme Screenshots](https://bbs.archlinux.org/viewtopic.php?pid=1194644%7CTerminal) per centinaia di scelte e temi disponibili.

#### Cambiare colore del tema di default

Il pacchetto `extra/terminal` di Xfce è dotato di una tavolozza di colori più scuro. Per cambiare questo aspetto, aggiungere quanto segue nel file terminalrc, per un tema di colore più chiaro che è sempre visibile su sfondi scuri in terminal.

```
~/.config/xfce4/terminal/terminalrc

```

```
ColorPalette5=#38d0fcaaf3a9
ColorPalette4=#e013a0a1612f
ColorPalette2=#d456a81b7b42
ColorPalette6=#ffff7062ffff
ColorPalette3=#7ffff7bd7fff
ColorPalette13=#82108210ffff

```

#### Tema di colori tango per Terminal

Per passare al tema del colore tango, aprire con il proprio editor preferito

```
~/.config/xfce4/terminal/terminalrc

```

E aggiungere (sostituire ) queste righe :

```
ColorForeground=White
ColorBackground=#323232323232
ColorPalette1=#2e2e34343636
ColorPalette2=#cccc00000000
ColorPalette3=#4e4e9a9a0606
ColorPalette4=#c4c4a0a00000
ColorPalette5=#34346565a4a4
ColorPalette6=#757550507b7b
ColorPalette7=#060698989a9a
ColorPalette8=#d3d3d7d7cfcf
ColorPalette9=#555557575353
ColorPalette10=#efef29292929
ColorPalette11=#8a8ae2e23434
ColorPalette12=#fcfce9e94f4f
ColorPalette13=#72729f9fcfcf
ColorPalette14=#adad7f7fa8a8
ColorPalette15=#3434e2e2e2e2
ColorPalette16=#eeeeeeeeecec

```

### Gestione del colore

xfce4-settings-manager non ha ancora tutte le impostazioni per la gestione/calibrazione del colore, né vi è alcun programma XFCE specifico per caratterizzare il monitor.

Si può legere un ottimo articolo su come creare [profili colore con dispwin, ecc sotto XFCE](https://encrypted.pcode.nl/blog/2013/11/24/display-color-profiling-on-linux/), di seguito sono elencate le nozioni basilari :

#### Caricare un profilo

Se si desidera **caricare un profilo ICC** (che avete precedentemente creato o scaricato) per calibrare il monitor all'avvio, è possibile scaricare [xcalib](https://aur.archlinux.org/packages/xcalib/) da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)"), quindi aprire Gestione impostazioni di XFCE4, fare clic sull'icona *Sessione e Avvio*, e nella scheda *Avvio automatico* aggiungere una nuova voce in cui il comando sia `/usr/bin/xcalib /percorso/del/file/profilo.icc`. Avete ancora bisogno di impostare nelle vostre applicazioni che utilizzano un profilo, quale deve essere utilizzato per avere le immagini visualizzate con gestione del colore.

Un'altra opzione è dispwin. Dispwin calibra non solo la visualizzazione, ma stabilisce anche un _ICC_PROFILE centrale per X in modo che alcune applicazioni possono utilizzare un profilo di visualizzazione di "sistema " invece di richiedere all'utente di impostare manualmente il profilo di visualizzazione (GIMP, Inkscape, darktable, UFRaw, ecc ). Vedere [ICC profiles#Loading ICC profiles](/index.php/ICC_profiles#Loading_ICC_profiles "ICC profiles") per ulteriori informazioni.

#### Creare un profilo

Se si desidera **creare un profilo ICC** per la visualizzazione ( es. personalizzandolo/caratterizzandolo, ad esempio con ColorHug, o qualche altro colorimetro o uno spettrofotometro, o " a occhio" ), l'opzione più semplice potrebbe essere quella di installare [dispcalgui](https://www.archlinux.org/packages/?name=dispcalgui).

Un'altra opzione è quella di installare [gnome-settings-daemon](https://www.archlinux.org/packages/?name=gnome-settings-daemon) e [gnome-color-manager](https://www.archlinux.org/packages/?name=gnome-color-manager) (disponibili in extra). Al fine di avviare la calibrazione dalla riga di comando, per prima cosa eseguire `/usr/lib/gnome-settings-daemon/gnome-settings-daemon &` (nota: questo potrebbe cambiare il layout della tastiera e chissà che altro, quindi probabilmente è bene sperimentare con un utente creato appositamente), poi `colormgr get-devices` e cercare il "Device ID" nella linea del monitor. Se questo è ad esempio " xrandr-Lenovo Group Limited", allora si avvii la calibrazione con il comando `gcm-calibrate --device "xrandr-Lenovo Group Limited"`

**Nota:** Il motivo per cui è necessario gnome-settings-daemon è perché XFCE non dispone ancora di un componente di sessione per colord: [https://bugzilla.xfce.org/show_bug.cgi?id=8559](https://bugzilla.xfce.org/show_bug.cgi?id=8559) . Un demone leggero, [xiccd](https://github.com/agalakhov/xiccd), può ( e probabilmente dovrebbe ) essere utilizzato in sostituzione.

Vedere [ICC profiles](/index.php/ICC_profiles "ICC profiles") per ulteriori informazioni.

### Monitor multipli

Se si è configurato X.org in modo che il vostro display si estenda su più monitor, di solito quando si accede ad una sessione di **XFCE**, sembrerà come se i monitor siano semplici cloni uno dell'altro. È possibile utilizzare lo strumento **xrandr** per modificare la configurazione, ma se questo non verrà richiamato al momento opportuno nella sequenza di avvio, così alcune funzionalità possono andare perse come parti del vostro display inaccessibili al puntatore del mouse.

Un modo migliore è quello di configurare XFCE per abbinare il vostro arrangiamento di visualizzazione desiderato. Tuttavia, attualmente (xfce-settings 4.10), non vi è alcun strumento a disposizione per assistere con la configurazione di più monitor direttamente.

*   Lo strumento Impostazioni - > Schermo consente la configurazione della risoluzione dello schermo, di rotazione e abilitazione dei singoli monitor ; **Attenzione**: *utilizzando questo strumento per regolare le impostazioni del schermo si resettano o di perdono le impostazioni eseguite manualmente per le proprietà non esplicitamente offerti come pulsanti nello strumento (vedi sotto)*.
*   Impostazioni - > Editor delle Impostazioni la manipolazione di tutti gli elementi di configurazione, in particolare le impostazioni dei display vengono salvati nel file **displays.xml** sottostante

```
~/.config/xfce4/xfconf/xfce-perchannel-xml

```

*   In alternativa, il file *displays.xml* può essere modificato utilizzando il vostro editor preferito.

Il requisito principale per impostare più monitor è la loro disposizione l'uno rispetto all'altro. Questo può essere controllato impostando le proprietà di **Position** (**X** e **Y**) per adattarsi; una posizione *(x,y)* di *0,0* corrisponde come posizione alla parte superiore (*top*) a sinistra (*left*) della schiera dei monitor. Questa è la posizione di default per tutti i monitor, e se diversi monitor sono abilitati essi appariranno come un area di visualizzazione clonata che si estende da questo punto.

Per estendere l'area di visualizzazione correttamente su entrambi i monitor :

*   Per monitor side-by-side (lato per lato), impostare la proprietà X del monitor più a destra per eguagliare la larghezza del monitor più a sinistra
*   Per monitor above-and-below (sopra e sotto), impostare la proprietà Y del monitor inferiore per eguagliare l'altezza del monitor superiore
*   per altri accordi, impostare le proprietà X e Y di ciascun monitor per corrispondere al layout

Le misure sono in *pixel*. Come esempio , una coppia di monitor con dimensioni nominali di 1920x1080 che sono ruotati di 90 e collocati fianco a fianco può essere configurato con un displays.xml come questo:

```
<channel name="displays" version="1.0">
 <property name="Default" type="empty">
   <property name="VGA-1" type="string" value="Idek Iiyama 23"">
     <property name="Active" type="bool" value="true"/>
     <property name="Resolution" type="string" value="1920x1080"/>
     <property name="RefreshRate" type="double" value="60.000000"/>
     <property name="Rotation" type="int" value="90"/>
     <property name="Reflection" type="string" value="0"/>
     <property name="Primary" type="bool" value="false"/>
     <property name="Position" type="empty">
       <property name="X" type="int" value="0"/>
       <property name="Y" type="int" value="0"/>
     </property>
   </property>
   <property name="DVI-0" type="string" value="Digital display">
     <property name="Active" type="bool" value="true"/>
     <property name="Resolution" type="string" value="1920x1080"/>
     <property name="RefreshRate" type="double" value="60.000000"/>
     <property name="Rotation" type="int" value="90"/>
     <property name="Reflection" type="string" value="0"/>
     <property name="Primary" type="bool" value="false"/>
     <property name="Position" type="empty">
       <property name="X" type="int" value="1080"/>
       <property name="Y" type="int" value="0"/>
     </property>
   </property>
 </property>
</channel>

```

Di solito, le impostazioni modificate in questo modo richiedono un logout/login per renderle attive. Un nuovo metodo per la configurazione di più monitor sarà disponibile nel prossimo rilascio di Xfce-Settings 4.12.

### Cartelle utente XDG

freedesktop.org specifica le "ben note directory degli utenti, come la cartella del desktop e la cartella musica. Vedere [XDG user directories](/index.php/XDG_user_directories "XDG user directories") per informazioni dettagliate .

### SSH Agents

Di default Xfce 4.10 cercherà di caricare gpg-agent o ssh-agent in questo ordine durante l'inizializzazione della sessione. Per disabilitare questo comportamento, creare una chiave xfconf utilizzando il seguente comando :

```
xfconf-query -c xfce4-session -p /startup/ssh-agent/enabled -n -t bool -s false

```

Per forzare l'utilizzo di ssh-agent, anche se è installato gpg-agent, eseguire il seguente comando:

xfconf-query -c xfce4-session -p /startup/ssh-agent/type -n -t string -s ssh-agent

Per utilizzare [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring") , selezionare *Launch GNOME services on startup* (avviare servizi di GNOME all'avvio) nella scheda *Avanzate* di *Sessione e Avvio* nelle impostazioni di Xfce. Questo disabiliterà automaticamente anche gpg-agent e ssh-agent .

Fonte : [http://docs.xfce.org/xfce/xfce4-session/advanced](http://docs.xfce.org/xfce/xfce4-session/advanced)

### Funzionalità Bluetooth

Attualmente non esiste una applet bluetooth per Xfce che è compatibile con la versione 5 di [bluez](https://www.archlinux.org/packages/?name=bluez). Gli utenti hanno tre opzioni per l'utilizzo del bluetooth in Xfce :

*   È possibile installare [bluez4](https://aur.archlinux.org/packages/bluez4/) e [blueman-bzr](https://aur.archlinux.org/packages/blueman-bzr/) da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") . L'applet [Blueman](/index.php/Blueman "Blueman") si integra bene con il desktop Xfce, ma **va ricordato che [Bluez4](/index.php/Bluez4 "Bluez4") ( lo stack su cui si basa [Blueman](/index.php/Blueman "Blueman")) è stato abbandonato e non è più supportato**.

*   È possibile installare [gnome-bluetooth](https://www.archlinux.org/packages/?name=gnome-bluetooth) e [gnome-bluetooth-applet-git](https://aur.archlinux.org/packages/gnome-bluetooth-applet-git/). Quest'ultimo pacchetto fornisce l'applet per GNOME Shell non desktop, come il codice applet è stata abbandonato in GNOME 3.8\. Vedere la [[Bluetooth#GNOME_Bluetooth | Sezione GNOME Bluetooth] ] nell'articolo Bluetooth per maggiori informazioni.

*   È possibile accedere a funzionalità Bluetooth utilizzando gli strumenti della riga di comando. Si prega di consultare la pagina [Bluetooth](/index.php/Bluetooth "Bluetooth") per ulteriori informazioni.

### Scorrere una finestra di sfondo , senza azionare il focus su di esso

Andare nel

Menu Principale -> Impostazioni -> Window Manager Tweaks -> Scheda "Accessibilità"

Deselezionare la voce `Sollevare le finestre quando viene premuto un pulsante del mouse`.

## Risoluzione dei problemi

### Operazioni " Non Autorizzato" quando si tenta di montare un dispositivo con un file manager

Un agente di autenticazione polkit è richiesto per questa operazione (insieme a [polkit](/index.php/Polkit "Polkit") e [GVFS](/index.php/GVFS "GVFS")) , ma non è incluso in Xfce. Assicurarsi che uno sia installato e avviarlo automaticamente al login , come spiegato in [polkit#Authentication agents](/index.php/Polkit#Authentication_agents "Polkit").

### xfce4-power-manager

Eventi ACPI relativi alla gestione energetica possono essere configurati tramite opzioni utilizzando [Systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)") in `/etc/systemd/logind.conf` per darne il controllo a xfce4-power-manager.

 `/etc/systemd/logind.conf` 
```
HandlePowerKey=ignore
HandleSuspendKey=ignore
HandleHibernateKey=ignore
HandleLidSwitch=ignore
```

Questo risolve anche il problema quando il computer registra più eventi di sospensione.

### xfce4 continua a spegnere il monitor

Xfce4 (a partire da 4,12 ) non sembra rispettare le impostazioni di alimentazione del monitor in `xfce4-power-manager`, e tenta di eseguire il salvaschermo ogni 10 minuti. È possibile controllare questo leggendo l' output di `$ xset q`. Eseguire `noblank $ xset s` per fermarlo. In alternativa, aggiungere il seguente file di configurazione di `/etc/X11/xorg.conf.d/` (vorrei salvarlo come `20-noblank.conf`).

```
Section "ServerFlags"
	Option "BlankTime" "0"
EndSection

```

### xfce4-xkb-plugin

C'è un bug nella versione [xfce4-xkb-plugin](https://www.archlinux.org/packages/?name=xfce4-xkb-plugin) 0.5.4.1-1 che causa ad xfce4-xkb-plugin di *perdere la tastiera, la mappatura e le impostazioni di composizione delle chiavi*. Come soluzione alternativa si può attivare l'opzione *Usa predefiniti di sistema* in *impostazioni della tastiera* . Per farlo funzionare.

```
xfce4-keyboard-settings

```

Andare nella scheda *Mappatura* e spuntare *Usa predefiniti di sistema*, quindi riconfigurare xfce4-xkb-plugin.

### Locales ignorato con GDM

Aggiungere il proprio locale in `/var/lib/accountsservice/users/$USER` :

```
[User]
Language=it_IT.UTF-8
XSession=xfce

```

Si può farlo anche con sed. Notare il backslash prima di .UTF-8 :

```
# sed -i 's/Language=.*/Language=it_IT\.UTF-8/' /var/lib/AccountsService/users/$USER

```

Riavviare GDM per rendere effetive le modifiche.

### Ripristinare le impostazioni predefinite

Se per qualche ragione si ha la necessità di ripristinare le configurazioni ritornando a quelle predefinite, per prima cosa rinominare i file `~/.config/xfce4-session/` e `~/.config/xfce4/`

```
$ mv ~/.config/xfce4-session/ ~/.config/xfce4-session-bak
$ mv ~/.config/xfce4/ ~/.config/xfce4-bak

```

Uscire e ri-accedere alla sessione per fare in modo che i cambiamenti abbiano effetto. Se durante l'accesso si ottiene una finestra di errore con l'intestazione "Impossibile caricare una sessione protetta", vedere la sezione [#Fallimento della sessione](#Fallimento_della_sessione) in questa pagina.

### Le icone del desktop si ricompongono in Xfce

Potreste scoprire che in certi eventi (come aprire la finestra delle impostazioni del pannello), le icone sul desktop si ricompongono. Questo perché le posizioni delle icone sono determinate da file nella directory `~/.config/xfce4/desktop/`. Ogni volta che viene apportata una modifica al desktop (vengono aggiunte o rimosse icone o ne viene cambiata la posizione) un nuovo file viene generato in questa directory e questi file possono entrare in conflitto.

Per risolvere il problema , passare alla directory ed eliminare tutti i file diversi da quello che definisce correttamente le posizioni delle icone. È possibile determinare quale file definisce le corrette posizioni delle icone aprendolo ed esaminando le posizioni delle icone. La riga più in alto è definito come `row 0` e la colonna più a sinistra è definita da `col 0`. Pertanto una voce di :

```
[Firefox]
row=3
col=0

```

significa che l'icona di Firefox si trova alla quarta riga della colonna più a sinistra.

### NVIDIA e xfce4-sensors-plugin

Per rilevare e utilizzare i sensori delle GPU NVIDIA è necessario installare [libxnvctrl](https://www.archlinux.org/packages/?name=libxnvctrl) e poi ricompilare pacchetto [xfce4-sensors-plugin](https://www.archlinux.org/packages/?name=xfce4-sensors-plugin).

### Fallimento della sessione

Se il gestore di finestre non viene caricato correttamente, forse si ha un errore della sessione. I sintomi tipici di questo possono includere :

*   Il mouse è una X e/o non appare affatto
*   Le decorazioni delle finestre sono scomparse e le finestre non possono essere chiuse
*   Strumento per le impostazioni " Window Manager" (`xfwm4-settings`) non si avvia , riferendo :

```
These settings cannot work with your current window manager (unknown)

```

*   Errori segnalati da `slim` o il tuo login manager come

```
No window manager registered on screen 0

```

Riavviare Xfce o il sistema può risolvere il problema, ma più probabilmente il problema è una sessione corrotta. Eliminare la cartella della sessione sotto la cartella della `.cache`:

```
$ rm -r ~/.cache/sessions/

```

### Le preferenze per le applicazioni preferite non hanno effetto

Se avete impostato le vostre applicazioni preferite con exo-preferred-applications, ma non sembrano essere prese in considerazione, vedere [#Integrazione xdg-open (Applicazioni preferite)](#Integrazione_xdg-open_(Applicazioni_preferite)).

### Pulsanti di azione/icone mancanti

Questo succede se le icone per alcune azioni (sospensione, ibernazione) non sono presenti nel tema di icone, o almeno non hanno i nomi attesi. In primo luogo, trovare il tema di icone attualmente utilizzato in Gestione impostazioni ( → Aspetto → Icone). Abbinare questo con una sottodirectory di `/usr/share/icons`. Ad esempio, se il tema di icone è GNOME, prendere nota del nome della directory `/usr/share/icons/gnome`.

```
icontheme=/usr/share/icons/gnome

```

Assicurarsi che il pacchetto [xfce4-power-manager](https://www.archlinux.org/packages/?name=xfce4-power-manager) sia installato poiché questo contiene le icone necessarie. Ora creare link simbolici dal tema di icone in corso al tema di icone `HiColor`.

```
ln -s /usr/share/icons/hicolor/16x16/actions/xfpm-suspend.png   ${icontheme}/16x16/actions/system-suspend.png
ln -s /usr/share/icons/hicolor/16x16/actions/xfpm-hibernate.png ${icontheme}/16x16/actions/system-hibernate.png
ln -s /usr/share/icons/hicolor/22x22/actions/xfpm-suspend.png   ${icontheme}/22x22/actions/system-suspend.png
ln -s /usr/share/icons/hicolor/22x22/actions/xfpm-hibernate.png ${icontheme}/22x22/actions/system-hibernate.png
ln -s /usr/share/icons/hicolor/24x24/actions/xfpm-suspend.png   ${icontheme}/24x24/actions/system-suspend.png
ln -s /usr/share/icons/hicolor/24x24/actions/xfpm-hibernate.png ${icontheme}/24x24/actions/system-hibernate.png
ln -s /usr/share/icons/hicolor/48x48/actions/xfpm-suspend.png   ${icontheme}/48x48/actions/system-suspend.png
ln -s /usr/share/icons/hicolor/48x48/actions/xfpm-hibernate.png ${icontheme}/48x48/actions/system-hibernate.png

```

Uscire dalla sessione corrente e rientrare dovrebbe bastare per avere tutte le icone per le azioni.

### Abilitare cedilla ç/Ç al posto di of ć/Ć

Quando si seleziona il layout di tastiera " US, alternativa internazionale" in Impostazioni - > Tastiera - > Mappatura per abilitare gli accenti, la combinazione tipica per la cedilla '+ c risultati ć invece di ç. Per cambiare questo comportamento, basta modificare il file gtk-2.0 e immodules.cache per gtk-3.0\. Nella linea che contiene "cedilla " aggiungere "en" nela lista "az:ca:co:fr:gv:oc:pt:sq:tr:wa" ma mantenendone l'ordine alfabetico in `/etc/gtk-2.0/gtk.immodules`

```
"/usr/lib/gtk-2.0/2.10.0/immodules/im-cedilla.so" 
"cedilla" "Cedilla" "gtk20" "/usr/share/locale" "az:ca:co:en:fr:gv:oc:pt:sq:tr:wa"

```

E aggiungerlo anche in `/usr/lib/gtk-3.0/3.0.0/immodules.cache`

```
"/usr/lib/gtk-3.0/3.0.0/immodules/im-cedilla.so" 
"cedilla" "Cedilla" "gtk30" "/usr/share/locale" "az:ca:co:en:fr:gv:oc:pt:sq:tr:wa"

```

Quando terminato, applicare le modifiche con

```
# echo "export GTK_IM_MODULE=cedilla" >> /etc/environment

```

Ora basta semplicemente chiudere e riaprire i programmi GTK come gedit.

### Caratteri non ASCII al montaggio di penne USB =

Un problema comune quando si effettua il montaggio automatico delle chiavette USB formattate con il filesystem FAT è l'incapacità di mostrare correttamente i caratteri come dieresi, ñ, ß, ecc. Questo può essere risolto modificando il iocharset predefinita in UTF-8 , che è fatto facilmente aggiungendo una linea a `/etc/xdg/xfce4/mount.rc` :

```
[vfat]
uid=<auto>
shortname=winnt
**utf8=true**
# FreeBSD specific option
longnames=true
flush=true

```

Si noti che quando si usa UTF -8, il sistema distingue tra caratteri minuscoli superiori, e potenzialmente può corrompere i file, quindi fate attenzione.

É possibile montare dispositivi vfat con opzione *flush*, in modo da scrivere più spesso i dati sul disco, durante la copia da una penna USB, in modo da evitare che la finestre di trasferimento di Thunar venga chiuse mentre i dati non sono ancora stati scritti. Aggiungere *async* invece accelererà la scrittura, ma assicurarsi di utilizzare l'opzione *Disconnetti* in Thunar per smontare il dispositivo. A livello globale, le opzioni di montaggio per i dispositivi di archiviazione presenti al boot, possono essere impostati in [fstab](/index.php/Fstab_(Italiano) "Fstab (Italiano)"), e per altri dispositivi nelle regole [udev](/index.php/Udev_(Italiano) "Udev (Italiano)").

### Video tearing quando il composite Xfwm è abilitato

Questo è un problema noto. Considerare l'utilizzo di un compositore standalone come [Compton](/index.php/Compton "Compton") o [xcompmgr](/index.php/Xcompmgr "Xcompmgr"). In alternativa, si potrebbe sostituire il window manager con qualcosa come [Compiz](/index.php/Compiz "Compiz") o Kwin (([kwin-standalone-git](https://aur.archlinux.org/packages/kwin-standalone-git/))) che forniscono i propri compositori.

### Caratteri sfocati e distorti quando compositing è abilitato (schede Intel)

Gli utenti con schede grafiche Intel possono trovare che il testo diventi sfocato o distorto quando il compositing è abilitato. Ciò è dovuto al driver [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) quando viene utilizzato il backend per l'accelerazione predefinito SNA. Questo errore può essere corretto modificando il backend impostandolo sul vecchio metodo UXA. Vedere la [pagina Intel Graphics](/index.php/Intel_(Italiano)#Scegliere_il_metodo_di_accelerazione "Intel (Italiano)") per ulteriori istruzioni .

### I temi GTK non funzionano su monitor multipli

Alcuni strumenti di configurazione potrebbero corrompere il file displays.xml, che traduce i temi GTK tramite il menu Applicazioni Menu -> Impostazioni -> Aspetto , con il risultato che smettano di funzionare. Per risolvere il problema, eliminare `~/.config/xfce4/xfconf/xfce-perchannel-xml/displays.xml` e riconfigurare i vostri schermi .

## Fonti Esterne

*   [http://docs.xfce.org/](http://docs.xfce.org/) - Documentazione completa.
*   [Xfce-Look](http://www.xfce-look.org/) - Temi, sfondi, ed altro.
*   [Xfce Wikia](http://xfce.wikia.com/wiki/Frequently_Asked_Questions) - Come modificare il menu autogenerato con un editor di menu
*   [Xfce Wiki](http://wiki.xfce.org)