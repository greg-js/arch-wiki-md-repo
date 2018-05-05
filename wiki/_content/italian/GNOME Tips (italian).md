## Contents

*   [1 Suggerimenti di configurazione](#Suggerimenti_di_configurazione)
    *   [1.1 Aggiungere/modificare la sessione GDM](#Aggiungere.2Fmodificare_la_sessione_GDM)
    *   [1.2 Aspetto GDM](#Aspetto_GDM)
    *   [1.3 Ottimizzazione](#Ottimizzazione)
    *   [1.4 Prestazioni basse](#Prestazioni_basse)
    *   [1.5 Applicazioni predefinite](#Applicazioni_predefinite)
    *   [1.6 Abilitare il controllo del volume come notifica dal vassoio](#Abilitare_il_controllo_del_volume_come_notifica_dal_vassoio)
    *   [1.7 I font appaiono asimmetrici](#I_font_appaiono_asimmetrici)
    *   [1.8 Migliorare l'aspetto dei font](#Migliorare_l.27aspetto_dei_font)
    *   [1.9 Cambiare l'immagine di sfondo predefinita](#Cambiare_l.27immagine_di_sfondo_predefinita)
    *   [1.10 Cambiare il colore di sfondo predefinito, opacità, ecc](#Cambiare_il_colore_di_sfondo_predefinito.2C_opacit.C3.A0.2C_ecc)
    *   [1.11 Aprire le finestre di shell in un formato maggiore](#Aprire_le_finestre_di_shell_in_un_formato_maggiore)
    *   [1.12 Disabilitare la finestra di conferma di chiusura del terminale gnome](#Disabilitare_la_finestra_di_conferma_di_chiusura_del_terminale_gnome)
*   [2 Suggerimenti vari](#Suggerimenti_vari)
    *   [2.1 Blocco monitor](#Blocco_monitor)
    *   [2.2 Suggerimenti per nautilus](#Suggerimenti_per_nautilus)
        *   [2.2.1 Cambiare modalità al browser (vista spaziale)](#Cambiare_modalit.C3.A0_al_browser_.28vista_spaziale.29)
        *   [2.2.2 Vista informazioni musicali (bitrate etc.)](#Vista_informazioni_musicali_.28bitrate_etc..29)
        *   [2.2.3 Fermare il ridisegno di Nautilus sul desktop](#Fermare_il_ridisegno_di_Nautilus_sul_desktop)
        *   [2.2.4 Thumbnails](#Thumbnails)
        *   [2.2.5 Disattivare le autenticazioni necessarie per il montaggio dell'unità interna in Nautilus](#Disattivare_le_autenticazioni_necessarie_per_il_montaggio_dell.27unit.C3.A0_interna_in_Nautilus)
    *   [2.3 Velocizzare vista pannelli](#Velocizzare_vista_pannelli)
        *   [2.3.1 panel_show_delay / panel_hide_delay](#panel_show_delay_.2F_panel_hide_delay)
        *   [2.3.2 Pannello animation_speed](#Pannello_animation_speed)
    *   [2.4 Suggerimenti menu gnome](#Suggerimenti_menu_gnome)
        *   [2.4.1 Rallentamento menu gnome](#Rallentamento_menu_gnome)
        *   [2.4.2 Modifiche al menu](#Modifiche_al_menu)
            *   [2.4.2.1 Menu utente](#Menu_utente)
            *   [2.4.2.2 Group menu, System menu](#Group_menu.2C_System_menu)
        *   [2.4.3 Cambiare l'icona predefinita del menu Gnome con l'icona di Arch](#Cambiare_l.27icona_predefinita_del_menu_Gnome_con_l.27icona_di_Arch)
        *   [2.4.4 Cambiare l'icona predefinita del menu Gnome con l'icona di Arch (senza accesso da root)](#Cambiare_l.27icona_predefinita_del_menu_Gnome_con_l.27icona_di_Arch_.28senza_accesso_da_root.29)
        *   [2.4.5 Icona personalizzata usando gconf-editor](#Icona_personalizzata_usando_gconf-editor)
        *   [2.4.6 Nascondere le icone predefinite dal desktop](#Nascondere_le_icone_predefinite_dal_desktop)
    *   [2.5 Disabilitare lo scroll dalla barra delle applicazioni](#Disabilitare_lo_scroll_dalla_barra_delle_applicazioni)
    *   [2.6 Personalizzare uno sfondo con transizione di immagini.](#Personalizzare_uno_sfondo_con_transizione_di_immagini.)
        *   [2.6.1 Manuale](#Manuale)
        *   [2.6.2 Automatico](#Automatico)
        *   [2.6.3 GUI](#GUI)
    *   [2.7 Cambia la dimensione di default di gnome-terminal](#Cambia_la_dimensione_di_default_di_gnome-terminal)
        *   [2.7.1 Metodo 1](#Metodo_1)
        *   [2.7.2 Metodo 2](#Metodo_2)
    *   [2.8 Installare un tema del cursore](#Installare_un_tema_del_cursore)
*   [3 Utilità aggiuntive](#Utilit.C3.A0_aggiuntive)
    *   [3.1 Masterizzare i CD da Nautilus](#Masterizzare_i_CD_da_Nautilus)
    *   [3.2 Gdesklets: Desktop Candy](#Gdesklets:_Desktop_Candy)
*   [4 gnome-screensaver](#gnome-screensaver)
    *   [4.1 Possibilità di lasciare messaggi nello screensaver di Gnome](#Possibilit.C3.A0_di_lasciare_messaggi_nello_screensaver_di_Gnome)
    *   [4.2 Cambiare lo sfondo dello screensaver di Gnome](#Cambiare_lo_sfondo_dello_screensaver_di_Gnome)
*   [5 Altre Applicazioni](#Altre_Applicazioni)
    *   [5.1 Console a scomparsa](#Console_a_scomparsa)
        *   [5.1.1 Guake](#Guake)
        *   [5.1.2 Tilda](#Tilda)
    *   [5.2 rhythmbox](#rhythmbox)
    *   [5.3 sound-juicer](#sound-juicer)
    *   [5.4 gimp](#gimp)
    *   [5.5 gftp](#gftp)
    *   [5.6 abiword](#abiword)
    *   [5.7 gnumeric](#gnumeric)
    *   [5.8 DevilsPie](#DevilsPie)
*   [6 Consultare inoltre](#Consultare_inoltre)

## Suggerimenti di configurazione

### Aggiungere/modificare la sessione GDM

Ogni sessione si avvale di un file *.desktop contenuto in `/usr/share/xsessions`.

**Per aggiungere una nuova sessione:**

1\. Copiare un file `*.desktop` esistente da usare come modello per una nuova sessione:

```
$ cd /usr/share/xsessions
$ sudo cp gnome.desktop other.desktop

```

2\. Modificare il file modello `*.desktop` per avviare il window manager desiderato:

```
$ sudoedit other.desktop

```

In alternativa, si può avviare la nuova sessione in KDM che creerà il file *.desktop. Ritornare poi a GDM e la nuova sessione sarà disponibile.

### Aspetto GDM

È possibile modificare un'immagine di sfondo, temi gtk/icone manualmente, oppure è possibile utilizzare [gdm2setup](https://aur.archlinux.org/packages/gdm2setup/) da [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)").

### Ottimizzazione

Se le applicazioni di gnome risultano lente e gnome si blocca allo start-up dopo aver "ucciso" la precedente sessione, presumibilmente non si sarà impostato correttamente il file `/etc/hosts` che quindi conterrà:

```
127.0.0.1       localhost.localdomain     localhost      **YOURHOSTNAME**

```

Eseguire poi "`/bin/hostname YOURHOSTNAME`" e "`/sbin/ifconfig lo up`" da **root**.

Consultare inoltre [Configuring network](/index.php/Configuring_network "Configuring network")

### Prestazioni basse

A causa di una scadente codifica di una libreria GNOME, certe azioni di GNOME possono rallentare il sistema. Come per esempio i temi delle icone in formato SVG. Un notevole incremento di prestazioni si può ottenere usando il formato PNG per le icone, o convertendo il proprio tema da SVG a PNG.

### Applicazioni predefinite

Si potrebbe voler configurare un largo spettro di applicazioni predefinite ed associazioni di file. Risulta estremamente utile nel caso si abbiano alcune applicazioni KDE installate, ma si preferisce che siano quelle di GNOME ad essere lanciate in modo predefinito.

Per farlo è possibile installare [gnome-defaults-list](https://aur.archlinux.org/packages/gnome-defaults-list/) da AUR. Il file di configurazione verrà messo in `/etc/gnome/defaults.list`.

Per fare tutto manualmente invece, creare `/usr/share/applications/defaults.list` con il seguente formato:

```
[Default Applications]
application/pdf=evince.desktop
image/jpeg=eog.desktop
...

```

### Abilitare il controllo del volume come notifica dal vassoio

Alcuni utenti avranno notato che non vi è alcun controllo del volume di default. Può essere aggiunto come un oggetto al pannello o come icona di notifica nella systray. Per fare questa modifica si deve sostituire gnome-media con gnome-media-pulse. Verrà installato il gestore di controllo del volume sviluppato da RedHat e utilizzato in distribuzioni come Ubuntu o Fedora.

```
# pacman -S gnome-media-pulse

```

### I font appaiono asimmetrici

Si può modificare il valore DPI dei font in Gnome con un click destro su desktop *→ Cambia sfondo Desktop → Caratteri → Dettagli → Risoluzione*>

```
Risoluzione: [96] dots per inch

```

### Migliorare l'aspetto dei font

Per avere una configurazione di caratteri piacevole e leggibile tutto quello che basta fare è cliccare nuovamente con il pulsante destro del mouse sul desktop *→ Caratteri → Dettagli*. Da qui è possibile impostare i subpixel (LCD) per l'antialiasing ed un basso Hinting per avere una configurazione ottimale. Per essere in grado di impostare LCD vedere il capitolo [LCD Font Configuration](/index.php/Font_configuration#LCD_filter_patched_packages "Font configuration").

### Cambiare l'immagine di sfondo predefinita

L'immagine di sfondo predefinita è il primo piano di una foglia verde. È l'immagine che si avrà come sfondo appena installato gnome, ma più importante, è l'immagine che si visualizzerà quando entra in funzione il blocco del monitor. Dal 25-Apr-2009, l'immagine sarà contenuta in

```
/usr/share/pixmaps/backgrounds/gnome/background-default.jpg

```

Per cambiarla, da **root**, mettere una nuova immagine nella cartella citata e rinominarla come l'originale.

### Cambiare il colore di sfondo predefinito, opacità, ecc

Il colore di sfondo di default è verde. Si potrebbe desiderare di cambiare se si sta utilizzando un PNG trasparente come sfondo.

```
$ sudo gconf-editor

```

Andare su *File → Nuova Finestra di Base* e modificare il valore

```
/desktop/gnome/background/primary_color

```

e

```
/desktop/gnome/background/secondary_color

```

È anche possibile impostare i valori per l'opacità, lo stile dell'ombreggiatura, ecc.

### Aprire le finestre di shell in un formato maggiore

Quando si aggiunge un lanciatore per il terminale, lo si può anche modificare per renderne le dimensioni della finestra più grandi dello standard predefinito. Click destro su lanciatore *→ Proprietà*. Poi, sotto la sezione "Comando", aggiungere il seguente

```
Command: gnome-terminal --geometry 105x25+100+20

```

### Disabilitare la finestra di conferma di chiusura del terminale gnome

Il terminale richiede sempre conferma di chiusura mediante una finestra, mentre si è loggati come root. Per evitare questo, lanciare **gconf-editor** e disabilitare la variabile **confirmation_window_close** in **/apps/gnome-terminal/global**.

## Suggerimenti vari

### Blocco monitor

1.  Assicurarsi che dbus sia in esecuzione (una buona idea è aggiungerlo alla stringa dei demoni in `/etc/rc.conf`).
2.  Installare xscreensaver `# pacman -S xscreensaver` 
3.  Spostarsi in Desktop -> Preferenze -> Screensaver
4.  Abilitare uno o più salvaschermi
5.  Da ora il blocco del monitor attiverà il salvaschermo e richiederà la password per essere sbloccato.

**oppure** si può installare gnome-screensaver:

```
# pacman -S gnome-screensaver

```

Si può anche consultare [qui](http://ubuntuforums.org/showthread.php?t=195557) come rimpiazzare gnome-screensaver con xscreensaver.

### Suggerimenti per nautilus

Per ottenere un certo percorso in una vista spaziale, dare i comandi:

```
Control + L

```

#### Cambiare modalità al browser (vista spaziale)

1.  Lanciare gconf-editor
2.  Spostarsi su `apps/nautilus/preferences`
3.  Cambiare il valore di "always_use_browser" (è un valore yes/no. Impostare il segno di spunta su "false"; per l'ultima impostazione cambiare il valore su "true")

Si può ottenere lo stesso dal menu preferenze:

1.  Nella finestra di nautilus spostarsi su Modifica>>Preferenze
2.  Selezionare la tabella Comportamento
3.  Mettere (o togliere) il segno di spunta su Aprire sempre in finestre di esplorazione

#### Vista informazioni musicali (bitrate etc.)

Nautilus non fornisce la visualizzazione dei metadati per file musicali, in modalità lista. Esiste uno script python per vedere le seguenti colonne:

*   Artist
*   Album
*   Track Title
*   Bit rate

Per prima cosa, installare il pacchetto richiesto.

```
sudo pacman -S mutagen

```

E da AUR, [python-nautilus](https://www.archlinux.org/packages/?name=python-nautilus)

```
wget [https://aur.archlinux.org/packages/python-nautilus/python-nautilus.tar.gz](https://aur.archlinux.org/packages/python-nautilus/python-nautilus.tar.gz)
tar -zxvf python-nautilus.tar.gz
cd python-nautilus
makepkg
sudo pacman -U *.pkg.tar.gz

```

Ora creare una cartella chiamata *python-extensions* in `~/.nautilus`ed aggiungerci il seguente script, chiamato bsc.py. Scaricare lo script da qui: [bsc.py](http://stefanwilkens.eu/bsc.py) Mirror: [bsc.py](http://kclkcl.webege.com/files/bsc.py)

[bas-v2.py](http://ubuntuforums.org/showthread.php?t=878683) aggiunge correzioni e ulteriori supporti (link alla fine del 4º post).
Mirror: [bsc-v2.py](http://www.rnstech.com/mirror/bsc-v2.py)

Riavviare nautilus. Si potrà ora configurare questa nuova funzionalità in Modifica -> Preferenze -> Colonne a Lista

#### Fermare il ridisegno di Nautilus sul desktop

E' necessario aprire *gconf-editor*:

```
apps>nautilus>preferences deselezionare "show_desktop"

```

Cercare la voce:

```
desktop>gnome>background 

```

e deselezionare "*draw_background*"

#### Thumbnails

C'è bisogno di uno strumento per la creazione di miniature, come ad esempio ffmpegthumbnailer. Assicurarsi che i codec necessari siano installati.

Da un terminale, inserire queste due righe:

```
gconftool-2 -s "/desktop/gnome/thumbnailers/video@mpeg/enable" -t boolean "true"
gconftool-2 -s "/desktop/gnome/thumbnailers/video@mpeg/command" -t string "/usr/bin/ffmpegthumbnailer -s %s -i %i -o %o -c png -f -t 10"

```

È possibile sostituire "video@mpeg" in quella riga con qualsiasi tipo di file possa essere aperto da ffmpeg - basta un click destro > Propietà su un file in Nautilus e guardare il bit tra parentesi in 'Type:' field (non dimenticare di sostituire la barra con il simbolo @). Alcuni tipi di file comuni sono video@mpeg, video@x-matroska, video@x-ms-wmv, video@x-flv, video@x-msvideo, video@mp4; che di solito sono .mpg, .mkv, .wmv, .flv, .avi, .mp4 rispettivamente.

#### Disattivare le autenticazioni necessarie per il montaggio dell'unità interna in Nautilus

In Ubuntu e altre distro è permesso montare i dischi interni, cliccando sulle rispettive icone senza la necessità di inserire una password. Per ottenere questo comportamento in gnome standard modificare il seguente file.

```
sudoedit /usr/share/polkit-1/actions/org.freedesktop.udisks.policy

```

Trovare la voce denominata:

```
<action id="org.freedesktop.udisks.filesystem-mount-system-internal">

```

All'interno di tale blocco, modificare il valore:

```
<allow_active>auth_admin_keep</allow_active>

```

a

```
<allow_active>yes</allow_active>

```

### Velocizzare vista pannelli

#### panel_show_delay / panel_hide_delay

Nel caso si noti un rallentamento dei pannelli usando la funzione nascondi/mostra, provare quanto segue:

1.  Avviare gconf-editor
2.  Spostarsi in /apps/panel/global
3.  Impostare panel_hide_delay e panel_show_delay su valori più sensibili. Notare che questi valori sono espressi in millisecondi.

Il valore di panel_hide_delay predefinito di 500 funziona bene nella maggior parte dei casi, ma lo stesso valore per panel_show_delay è terribilmente lento. Dopo un po' di esperimenti, un valore tra 100-200 sembrerebbe funzionare molto meglio.

#### Pannello animation_speed

Ora che il pannello mostra/nascondi compare/scompare in un ragionevole lasso di tempo, perché ci vuole così tanto perchè il pannello faccia il pop up? C'è ancora un'impostazione necessaria per rendere il comportamento del pannello decente. L'impostazione: **animation_speed** Questa impostazione può essere applicata a livello globale o per un singolo pannello proprio come per panel_show_delay e panel_hide_delay. La descrizione ufficiale è:

La velocità con cui avvengono le animazioni del pannello. I valori possibili sono lente, medie e veloci. Questo ha senso solo se è impostata la chiave enable_animations.

Per applicare a livello globale, basta aggiungere o modificare la chiave di animation_speed come (stringa) valore in:

*   /apps/panel/global

Per applicare l'impostazione su una base per-pannello, basta aggiungere/modificare la chiave in:

*   /apps/panel/toplevels/bottom_panel_screen0/ (di solito il nome predefinito per il pannello inferiore)
*   /apps/panel/toplevels/panel_0/ (di solito il nome predefinito per il primo pannello aggiuntivo)

**Nota:** la chiave panel_amination_speed è deprecata, usare: animation_speed.

### Suggerimenti menu gnome

#### Rallentamento menu gnome

È possibile eliminare un possibile rallentamento nel menu di GNOME, dando il seguente comando:

```
echo "gtk-menu-popup-delay = 0" >> ~/.gtkrc-2.0

```

Oppure aggiungendo "`gtk-menu-popup-delay = 0`" a .gtkrc-2.0

Da notare che questo tipo di impostazione può portare al crash "banshee", come anche altri programmi.

#### Modifiche al menu

Molti utenti gnome non sono soddisfatti del menu. I cambiamenti delle voci, sia del menu completo, che di singole voci, che per differenti utenti, non sono ben documentati.

##### Menu utente

Le recenti versioni di Gnome (es. v2.22) hanno un editor di menu dal quale si può deselezionare l'intero menu, ma non aggiungere nuove voci. Con un click destro sul panello del menu si seleziona Modifica menu. Togliendo il segno di spunta da una casella se ne impedirà la visualizzazione nel menu.

Per aggiungere nuove voci al menu, creare un file .desktop in $XDG_DATA_HOME/applications directory (probabilmente $HOME/.local/share). Un semplice file .desktop può essere visto sotto, oppure consultare la [Gnome documentation](http://library.gnome.org/admin/system-admin-guide/stable/menustructure-desktopentry.html.en).

O più facile ancora, installare Alacarte, con il quale si potranno creare, modificare e rimuovere le voci del menu con una semplice interfaccia grafica. Da console, dare:

```
# pacman -S alacarte

```

##### Group menu, System menu

Ci sono delle voci comuni nel menu gnome, come 'appname.desktop' all'interno di una delle cartelle $XDG_DATA_DIRS/applications directories (probabilmente /usr/share/applications). Per aggiungere al menu nuove voci per tutti gli utenti, creare un file 'appname.desktop' in una di quelle cartelle.

*   Modificare una di queste per adattare le proprie necessità ad una nuova applicazione, poi salvare.
*   Salvarla come una voce di menu per tutti gli utenti
    Spesso si imposteranno i permessi per questi file a 644 (root: rw group: r others: r), così tutti gli utenti avranno permesso di lettura.
*   Salvarla come una voce di menu per un gruppo o un singolo utente
    Si possono anche dare differenti permessi per gli utenti; per esempio, alcune voci del menu sarebbero disponibili per un gruppo o per un utente.

Qui un esempio di come potrebbe essere una definizione del file di una voce del menu Scite:

```
[Desktop Entry]
Encoding=UTF-8
Name=SciTE
Comment=SciTE editor
Type=Application
Exec=/usr/bin/scite
Icon=/usr/share/pixmaps/scite_48x48.png
Terminal=false
Categories=GNOME;Application;Development;
StartupNotify=true

```

#### Cambiare l'icona predefinita del menu Gnome con l'icona di Arch

**Nota:** Grazie a arkham che ha pubblicato questo metodo su [questo post](https://bbs.archlinux.org/viewtopic.php?id=74881) e che noi riportiamo qui.

*   Scaricare [questa icona Arch](http://img23.imageshack.us/img23/9679/starthere.png) (il nome del file è `starthere.png`)
*   In alternativa scaricare il pacchetto artwork usando "pacman -S archlinux-artwork", che sistemerà il pacchetto in /usr/share/archlinux directory, e ridimensionerà il logo desiderato a 24x24px
*   Verificare quale set di icone è in uso (click destro su Desktop>Cambiare l'immagine di Sfondo>Temi>Personalizza>Icone). Per esempio, Crux, *GNOME, High Contrast, High Contrast Inverse, Mist, ecc.)
*   Ora fare un backup dell'icona gnome corrente nella cartella corretta. Nell'esempio sotto, si stanno usando le icone gnome, ma nel caso, correggere la struttura ed il percorso delle cartelle con quella corrispondente:

```
# mv /usr/share/icons/gnome/24x24/places/start-here.png /usr/share/icons/gnome/24x24/places/start-here.png-virgin

```

*   Copiare `starthere.png` scaricata nella stessa cartella rinominandola start-here.png

```
# cp /path/to/starthere.png /usr/share/icons/gnome/24x24/places/start-here.png

```

*   Riavviare il pannello gnome e il nuovo logo di Arch verrà visualizzato

```
$ pkill gnome-panel

```

**Nota:** Per far funzionare questo metodo con (gnome 2.28) bisogna probabilmente eliminare il file icon-theme.cache in /usr/share/icons/gnome

#### Cambiare l'icona predefinita del menu Gnome con l'icona di Arch (senza accesso da root)

*   Verificare quale set di icone è in uso (click destro su Desktop>Cambiare l'immagine di Sfondo>Temi>Personalizza>Icone). Per esempio, Crux, *GNOME, High Contrast, High Contrast Inverse, Mist, etc.)
*   Duplicare la struttura della cartella delle icone 24x24/places nella cartella home sotto .icons

```
$ mkdir -p ~/.icons/gnome/24x24/places

```

*   Scaricare [questa icona Arch](http://img23.imageshack.us/img23/9679/starthere.png) in quella cartella, rinominandola 'start-here.png'

```
$ wget -O ~/.icons/gnome/24x24/places/start-here.png [http://img23.imageshack.us/img23/9679/starthere.png](http://img23.imageshack.us/img23/9679/starthere.png)

```

*   In alternativa scaricare il pacchetto artwork usando "pacman -S archlinux-artwork", che sistemerà il pacchetto in /usr/share/archlinux, e ridimensionerà il logo desiderato a 24x24px, rinominandolo "start-here.png".
*   Riavviare il pannello gnome e il nuovo logo di Arch verrà visualizzato

```
$ pkill gnome-panel

```

**Nota:** Per far funzionare questo metodo con (gnome 2.28) bisogna probabilmente eliminare il file icon-theme.cache in /usr/share/icons/gnome

#### Icona personalizzata usando gconf-editor

1.  Aprire l'editor di configurazione di gnome (di norma su System Tools dal menu) o eseguire `gconf-editor`
2.  Nell'editor di configurazione spostarsi su apps > panel > objects > e trovare l'oggetto per il menu (per individuarlo facilmente, dovrebbe avere "Main Menu" nella sezione suggerimenti).
3.  Modificare il percorso all'icona nel campo "Custom_Icon".
4.  Spuntare "Use_Custom_Icon" un pò più sotto.
5.  Per vedere i cambiamenti senza riavviare X, dare da console:

```
$ killall gnome-panel

```

#### Nascondere le icone predefinite dal desktop

A molti utenti piace mantenere il desktop pulito, senza icone. Ecco come rimuovere le cartelle home, computer, cestino e volume dal desktop:

1.  Da terminale dare il comando: gconf-editor
2.  All'apertura dell'editor, spostarsi su: apps > nautilus > desktop
3.  Levare il segno di spunta dalle icone che non si vuole visualizzare
4.  Le icone spariranno dal desktop subito, senza necessità di riavviare o altro

### Disabilitare lo scroll dalla barra delle applicazioni

Da anni un "bug" affligge la taskbar di Gnome: lo scroll del mouse fa cambiare il focus delle finestre. Questo fastidioso problema del mouse classico, diventa un po' un incubo se si stà usando il touchpad. È impossibile usare lo scroll con precisione con il touchpad, così se accidentalmente lo si sfiora quando il cursore è sulla barra, tutte le finestre salteranno in modo incontrollato. Non ci sono impostazioni nelle preferenze di GNOME o in gconf per poter disabilitare questa funzionalità. È così anche su KDE 3, meno sicuro che il problema persista anche su KDE 4\. Una possibile soluzione consiste nell'installare il pannello xfce4, che non possiede alcun tipo di funzionalità scrolling, ma nell'aspetto è simile a quello di default di GNOME. Il bug è descritto dettagliatamente quì [[1]](https://bugs.launchpad.net/ubuntu/+source/gnome-panel/+bug/39328).

Questo bug probabilmente non sarà mai corretto, ma con ABS, è possibile personalizzare il software e poi compilarlo. Installare [ABS](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)") (+70Mb), poi

```
cp -r /var/abs/extra/libwnck /home/{nome-utente}/Desktop/cartella-desiderata

```

spostarsi in quella cartella, poi

```
makepkg --nobuild

```

Così facendo, verranno scaricati e scompattati i sorgenti. Spostarsi in {{ic|src/libwnck-{version}/libwnck}}. Aprire il file `tasklist.c` con un editor di testo, e cercare "scroll-event". Si vedrà qualcosa di simile a

```
g_signal_connect(obj, "scroll-event", G_CALLBACK(wnck_tasklist_scroll_cb), NULL);

```

Questa riga abilita il "gestore degli eventi di scroll"(lo scroll-event handler); commentare la riga (mettendo /* prima e */ dopo la riga). Tornare indietro in `/home/{nome-utente}/Desktop/cartella-desiderata` e

```
makepkg --noextract --syncdeps

```

Sarà necessario avere [sudo](/index.php/Sudo_(Italiano) "Sudo (Italiano)") installato per risolvere le dipendenze mancanti (intltool), altrimenti si potrà comunque usare il comando `pacman -S` per installarle separatamente se non si desidera sincronizzare le dipendenze automaticamente(tramite l'opzione`--syncdep`). L'opzione `--noextract` fa in modo che `makepkg` non estragga i sorgenti ma usi l'esistente cartella `src/`

```
pacman -U libwnck-{version}.pkg.tar.gz

```

Successivamente riavviare la sessione. Cancellare la cartella con i sorgenti dal desktop; si può anche disinstallare abs se non dovesse servire più. Il prossimo passo sarebbe quello di aggiungere l'opzione a gconf, ma questo lo lasciamo ad altri guru di Gnome.

### Personalizzare uno sfondo con transizione di immagini.

Questo creerà uno sfondo che utilizza delle transizioni, simile al background "cosmos" che trovate nel pacchetto [gnome-backgrounds](/index.php/GNOME#Installation "GNOME"). Ci sono due metodi per farlo.

**Nota:** I nomi dei file immagine non devono avere spazi tra loro.

#### Manuale

È possibile creare un file XML simile a quello creato da gnome-backgrounds in `/usr/share/backgrounds/cosmos/`.

```
<background>
  <starttime>
    <hour>00</hour>
    <minute>00</minute>
    <second>01</second>
  </starttime>
<!-- The first section set an arbitrary start time. -->
  <static>
    <duration>1795.0</duration>
    <file>/path/to/background1.jpg</file>
  </static>
  <transition>
    <duration>5.0</duration>
    <from>/path/to/background1.jpg</from>
    <to>/path/to/background2.jpg</to>
  </transition>
  <static>
    <duration>1795.0</duration>
    <file>/path/to/background2.jpg</file>
  </static>
  <transition>
    <duration>5.0</duration>
    <from>/path/to/background2.jpg</from>
    <to>/path/to/background1.jpg</to>
  </transition>
</background>

```

Si noti che il tag **<duration>** imposta ogni immagine come sfondo per 1.795 secondi, o 29 minuti e 55 secondi, e la **<transition>** occupa 5 secondi. È possibile aggiungere qualsiasi numero di immagini fino a quando l'ultima transizione riporta al primo (se si desidera un ciclo completo). Una volta completato, il file XML può essere aggiunto a GNOME in Sistema> Preferenze> Aspetto>scheda Sfondo> Aggiungi.

#### Automatico

Vi è anche uno script che automatizza questo processo:

```
#!/bin/sh
#This script creates xml files that can act as dynamic wallpapers for Gnome by referring to multiple wallpapers
#Coded by David J Krajnik

if [ "$*" = "" ]; then
  echo "This script creates xml files that can act as dynamic backgrounds for Gnome by referring to multiple wallpapers";
  echo "Usage: mkwlppr target-file.xml [duration] pic1 pic2 [pic3 .. picN]";
else
  files=$*;
  #Grab the name of the target xml file
  xmlfile=`echo $files | cut -d " " -f 1`;
  #remove the first item from $files
  files=`echo $files | sed 's/^\<[^ ]*\>//'`;
  if [ "`echo $xmlfile | grep '\.xml$'`" = "" ]; then
    echo "Your target file must be an XML file";
  else
    inputIsValid="true";
    firstItem=`echo $files | cut -d " " -f 1`;
    duration="1795.0";#set the default duration
    if [ "`echo $firstItem | grep '^[0-9]\+\.[0-9]\+$'`" != "" ]; then
      echo "The duration must be an integer";
      files=`echo $files | sed 's/^\<[^ ]*\>//'`;
      inputIsValid="";
    elif [ "`echo $firstItem | grep '^[0-9]\+$'`" != "" ]; then
      #If the item is a number, then use it as the duration for each wallpaper image
      duration="`expr $firstItem - 5`.0";
      #remove the duration from the list of files
      files=`echo $files | sed 's/^\<[^ ]*\>//'`;
    fi
    if [ "$files" = "" ]; then
      echo "You must enter image files to associate with the XML file";
    else
      for file in $files
      do
        if [ ! -f $file ]; then
	  echo "\"$file\" does not exist";
	  inputIsValid="";
        elif [ "`echo $file | sed 's/^.*\.\(jpg\|jpeg\|bmp\|png\|gif\|tif\|tiff\|jif\|jfif\|jp2\|jpx\|j2k\|j2c\)$//'`" != "" ]; then
	  echo "\"$file\" is not an image file";
	  inputIsValid="";
	fi
      done
      if [ $inputIsValid ]; then
        currDir=`pwd`;
        echo "<background>" >> $xmlfile
        echo "  <starttime>
    <year>2009</year>
    <month>08</month>
    <day>04</day>" >> $xmlfile;
        echo "    <hour>00</hour>
    <minute>00</minute>
    <second>00</second>
  </starttime>" >> $xmlfile;
        echo "  <!-- This animation will start at midnight. -->" >> $xmlfile;
        firstFile=`echo $files | cut -d " " -f 1`;#grab the first item
        if [ "`echo $firstFile | sed 's/\(.\).*/\1/'`" != "/" ]; then
          #If the first character in the filename is not '/', then it is a relative path and must have the current directory's path appended
          firstFile="$currDir/$firstFile";
        fi
        firstFile=`echo $firstFile | sed 's/[^/]\+\/\.\.\/\?//g'`;#Remove occurrences of ".." from the filepath
        files=`echo $files | sed 's/^\<[^ ]*\>//'`;#remove the first item
        prevFile=$firstFile;
        currFile="";
        #TODO add absolute path to the filenames
        #if $currFile =~ "^/.*" then the file needs to path appended
        echo "  <static>
    <duration>$duration</duration>
    <file>$firstFile</file>
  </static>" >> $xmlfile;
        for currFile in $files
        do
          if [ "`echo $currFile | sed 's/\(.\).*/\1/'`" != "/" ]; then
            #If the first character in the filename is not '/', then it is a relative path and must have the current directory's path appended
            currFile="$currDir/$currFile";
          fi
          currFile=`echo $currFile | sed 's/[^/]\+\/\.\.\/\?//g'`;#Remove occurrences of ".." from the filepath
          echo "  <transition>
    <duration>5.0</duration>
    <from>$prevFile</from>
    <to>$currFile</to>
  </transition>" >> $xmlfile;
          echo "  <static>
    <duration>$duration</duration>
    <file>$currFile</file>
  </static>" >> $xmlfile;
          prevFile=$currFile;
        done
        echo "  <transition>
    <duration>5.0</duration>
    <from>$currFile</from>
    <to>$firstFile</to>
  </transition>" >> $xmlfile;
        echo "</background>" >> $xmlfile;
      fi
    fi
  fi
fi

```

Copiare il codice di questo script in un file denominato mkwlppr (diminutivo di "make wallpaper"). Rendere lo script eseguibile digitando il comando:

 `sudo chmod 711 mkwlppr` 

Spostare il file in modo che sia possibile eseguire da qualsiasi directory, semplicemente utilizzando il suo nome, come un normale comando:

 `sudo mv mkwlppr /bin` 

Eseguire lo script; esso vi chiederà quali impostazioni sono richieste. Usare lo script con i vostri dati per generare diversi file XML per i vostri sfondi secondo le vostre esigenze.

**Nota:** Dal momento che questo script non è interattivo, è possibile utilizzare i caratteri jolly di Unix, se si desidera utilizzare tutti i file in una directory e non ci si cura dell'ordine delle immagini.

È possibile specificare i percorsi relativi alla directory corrente, e lo script metterà per voi i percorsi assoluti dei file nel file XML, in modo che possiate creare il file XML ovunque si desidera e spostarlo tranquillamente senza preoccuparsi di renderlo inutilizzabile. Se si desidera eseguire lo script all'interno della directory `/usr/share/backgrounds/`, potreste avere problemi con le autorizzazioni a meno che non si esegue il comando con sudo come questo: `sudo mkwlppr -parameters` Se non sapete quale durata specificare per le immagini, semplicemente non fornite nessun parametro, ed il programma userà i valori di default, ossia di 29 minuti e 55 secondi per l'immagine e di 5 secondi per la transizione.

Per ulteriori informazioni, consultate [questa pagina](http://www.linuxjournal.com/content/create-custom-transitioning-background-your-gnome-228-desktop)

#### GUI

Se si preferisce usare un programma da GUI, è possibile installare [CreBS](https://aur.archlinux.org/packages/CreBS/) da AUR, si tratta di un'applicazione in PyGTK per creare presentazioni di sfondi in GNOME.

### Cambia la dimensione di default di gnome-terminal

#### Metodo 1

L'emulatore di terminale gnome-terminal non consente né di impostare una dimensione predefinita, né ricorda l'ultima dimensione utilizzata. Al fine di impostare la dimensione predefinita considerare le seguenti fasi:

1.  Modificare la seguente riga in `/usr/share/vte/termcap/xterm` di conseguenza:
    `:co#80:it#8:li#24:`
    Qui 80 sta per il numero di "**co**lumns" (es. larghezza caratteri) e 24 per il numero di "**li**nes" (es. altezza caratteri).
2.  Per evitare a pacman di sovrascrivere il file quando si aggiorna il pacchetto `vte`, fare entrare le seguenti `/etc/pacman.conf`
    `NoUpgrade = usr/share/vte/termcap/xterm`
3.  Terminare tutti i processi di gnome-terminal per consentire che le modifiche abbiano effetto.

#### Metodo 2

Un'altra opzione è quella di utilizzare semplicemente lo " scambio di geometrie" all'avvio di gnome-terminal (può essere fatto tramite un click destro/proprietà sul programma di avvio, quindi inserire la seguente riga nel campo "Command": gnome-terminal --geometry 105x25+100+20).

### Installare un tema del cursore

Il tema del cursore di default di xorg è piuttosto brutto. Installare il pacchetto seguente per avere il tema del cursore utilizzato su molte altre distribuzioni.

```
$ pacman -S xcursor-vanilla-dmz 

```

Poi spostarsi sul desktop -> click destro -> Modifica sfondo -> Scheda tema - personalizza> - cursore> per applicare il nuovo tema installato.

## Utilità aggiuntive

### Masterizzare i CD da Nautilus

```
# pacman -S nautilus-cd-burner

```

### Gdesklets: Desktop Candy

Inserire un orologio, un calendario, un indicatore meteo e altro sul vostro desktop

```
# pacman -S gdesklets

```

Si possono trovare altri desklets sul sito [gdesklets.org](http://www.gdesklets.de/?q=desklet/browse). Per installarli, scaricare i file corrispondenti. Quindi, nel menù Gnome, aprire Applicazioni->Accessori->gDesklets. Quando apparirà la gDesklets Shell, trascinare il nuovo file gdesklet nel terminale. Se si desidera che i gdesklet vengano caricati al login, accedere al menù sotto Sistema->Preferenze->Applicazioni d'avvio. Scegliere l'opzione Aggiungi e inserire il comando /usr/bin/gdesklets. Controllare che il comando sia giusto eseguendo in terminale

```
whereis gdesklets

```

## gnome-screensaver

### Possibilità di lasciare messaggi nello screensaver di Gnome

Questa è una simpatico funzione di gnome-screensaver fin dalla versione 2.20, chiunque può lasciare un messaggio a video mentre non si è alla scrivania. Si prega di installare notification-daemon per abilitare questa funzione

### Cambiare lo sfondo dello screensaver di Gnome

Non c'è nessuna opzione per cambiare lo sfondo di default dello screensaver. L'unico modo per farlo è:

```
   su
   cd /usr/share/pixmaps/backgrounds/gnome
   rm background-default.jpg
   ln -s /home/utente/mio_sfondo.jpg background-default.jpg

```

## Altre Applicazioni

Ci sono ulteriori applicazioni utili per Gnome non incluse in [GNOME#extras](/index.php/GNOME#extras "GNOME").

#### Console a scomparsa

Gnome dispone di alcune console a scomparsa ispirate da quelle che si trovano in celebri videogiochi FPS quali Quake ed HalfLife (accessibili ad esempio premendo il tasto tilde ~). Ricalcano lo stile di Yakuake (equivalente in KDE), seguono una serie di queste applicazioni native per Gnome.

##### Guake

Guake richiede Python, e può essere installato tramite il seguente comando

```
#pacman -S guake

```

`F12` è il tasto predefinito per mostrare/nascondere il terminale. Guake supporta le schede multiple e nella configurazione predefinita le combinazioni di tasti `Ctrl`+`PgDown` e `Ctrl`+`PgUp` sono utilizzate per navigare tra le schede aperte. È possibile configurare la trasparenza ed altre impostazioni facendo click destro sul terminale e selezionando Preferenze.

Guake può essere lanciato automaticamente all'avvio aggiungendolo alla Sessione di Gnome tramite Sistema -> Preferenze -> Sessione. Selezionare Aggiungi, e utilizzare queste impostazioni di esempio:

*   **Nome** Guake
*   **Comando** guake &
*   **Commento** Terminale a discesa stile Quake.

##### Tilda

Tilda è un altro terminale a scomparsa per Gnome.

```
# pacman -S tilda

```

Tilda necessita di un minor numero di dipendenze rispetto a Guake (non richiede Python), ed ha all'incirca le stesse funzioni; consente un maggior controllo sulle caratteristiche grafiche della finestra di terminale.

### rhythmbox

Un player audio simile ad iTunes.

### sound-juicer

Estrattore di tacce da cd-audio, si integra con rythmbox.

*In caso di ulteriori problemi con SoundJuicer, vedere [qui](/index.php/User:Munk3h "User:Munk3h")*

### gimp

Un alternativa per Linux a Photoshop. Assolutamente necessario se si ha a che fare con la grafica.

### gftp

Un pratico e leggero client FTP per Gnome.

### abiword

Un piccolo, rapido elaboratore di testi compatibile col formato .doc

### gnumeric

Un foglio di calcolo simile ad Excel.

### DevilsPie

Un utile applicazione che può essere eseguita come demone all'interno di Gnome. Gestisce le finestre consentendo di avviare programmi su di un desktop specifico o in una specifica misura, tra le altre cose. DevilsPie fornisce un nuovo livello di controllo all'interno dell'engine Metacitye. C'è un buon How-To a riguardo sull' [homepage](http://live.gnome.org/DevilsPie) del progetto

## Consultare inoltre

*   [Gnome](/index.php/GNOME_(Italiano) "GNOME (Italiano)")