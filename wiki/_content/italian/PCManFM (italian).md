Dal [sito](http://wiki.lxde.org/en/PCManFM) del progetto:

	*PCMan File Manager (PCManFM) è un'applicazione di file manager sviluppata da Hong Jen Yee da Taiwan che è destinata ad essere un sostituto di Nautilus, Konqueror e Thunar. Rilasciato sotto la GNU General Public License , PCManFM è un software libero . PCManFM è il file manager standard di [LXDE](/index.php/LXDE_(Italiano) "LXDE (Italiano)") , che è sviluppato sempre dallo stesso autore in collaborazione con altri sviluppatori.*

## Contents

*   [1 Installazione](#Installazione)
*   [2 Gestione Desktop](#Gestione_Desktop)
    *   [2.1 Preferenze del desktop](#Preferenze_del_desktop)
    *   [2.2 Creare nuove icone](#Creare_nuove_icone)
*   [3 Modalità Daemon](#Modalit.C3.A0_Daemon)
*   [4 Avvio automatico](#Avvio_automatico)
*   [5 Ulteriori caratteristiche e funzionalità](#Ulteriori_caratteristiche_e_funzionalit.C3.A0)
*   [6 Consigli e trucchi](#Consigli_e_trucchi)
    *   [6.1 Un clic per aprire cartelle e files](#Un_clic_per_aprire_cartelle_e_files)
    *   [6.2 Aprire ed estrarre archivi con PCManFM](#Aprire_ed_estrarre_archivi_con_PCManFM)
*   [7 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [7.1 Apertura finestra di dialogo vuota](#Apertura_finestra_di_dialogo_vuota)
    *   [7.2 Nessuna "Applicazione"](#Nessuna_.22Applicazione.22)
    *   [7.3 Nessuna icona](#Nessuna_icona)
    *   [7.4 Nessuna funzionalità "Cartella precedente/successiva" con i pulsanti del mouse](#Nessuna_funzionalit.C3.A0_.22Cartella_precedente.2Fsuccessiva.22_con_i_pulsanti_del_mouse)
    *   [7.5 Paramentri --desktop non funzionano o crash del X-server](#Paramentri_--desktop_non_funzionano_o_crash_del_X-server)
    *   [7.6 Mancato salvataggio delle configurazioni avanzati dell'Emulatore di terminale](#Mancato_salvataggio_delle_configurazioni_avanzati_dell.27Emulatore_di_terminale)
    *   [7.7 Memorizzare impostazioni Ordine files preferite](#Memorizzare_impostazioni_Ordine_files_preferite)
    *   [7.8 Errore "Non autorizzato" all'accesso/montaggio di unità USB](#Errore_.22Non_autorizzato.22_all.27accesso.2Fmontaggio_di_unit.C3.A0_USB)

## Installazione

[pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm) è disponibile negli [official repositories](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

Si consiglia di installare [gvfs](https://www.archlinux.org/packages/?name=gvfs) per il supporto del Cestino, del montaggio con Udisk e dei filesystem remoti.

Varianti di PCManFM degne di nota sono:

*   [pcmanfm-git](https://aur.archlinux.org/packages/pcmanfm-git/) - Development version.
*   [pcmanfm-qt](https://www.archlinux.org/packages/?name=pcmanfm-qt) - New [Qt](/index.php/Qt "Qt") implementation.
*   [pcmanfm-qt-git](https://aur.archlinux.org/packages/pcmanfm-qt-git/) - New Qt implementation, development version.

## Gestione Desktop

Il comando per consentire a PCManFM di impostare sfondi e usare icone sul desktop è:

```
pcmanfm --desktop

```

Il menu del desktop nativo del window manager verrà sostituito con quello fornito da PCManFM. Tuttavia, può essere facilmente ripristinato dal menu di PCManFM selezionando `Preferenze della Scrivania` e abilitando `Mostra i menù forniti dai Windows Manager` nella scheda `Avanzate`.

### Preferenze del desktop

Se si utilizza il menu del desktop nativo offerto da un gestore di finestre, immettere il seguente comando per impostare o modificare le preferenze del desktop in qualsiasi momento:

```
$ pcmanfm --desktop-pref

```

Vale la pena di considerare l'aggiunta di questo comando per effettuare un keybind del menu del desktop nativo per un facile accesso.

### Creare nuove icone

I Contenuti dell'utente come files di testo, documenti, immagini e così via possono essere trascinati direttamente sul desktop. Non è ivece possibile trascinare applicazioni sul Desktop, se si vuole creare un collegamento ad un applicazione sul Desktop sarà necessario copiare il suo file `.desktop` nella cartella `~/Desktop`.:

```
cp /usr/share/applications/<nome applicazione>.desktop ~/Desktop

```

Per esempio per creare un collegamento sul desktop per [lxterminal](https://www.archlinux.org/packages/?name=lxterminal)- se installato - sarebbe stato utilizzato il seguente comando:

```
cp /usr/share/applications/lxterminal.desktop ~/Desktop

```

Per coloro che hanno utilizzato il programma [Xdg user directories](/index.php/Xdg_user_directories "Xdg user directories") per creare la loro `$HOME`, non sarà richiesta alcuna ulteriore configurazione.

## Modalità Daemon

La sessione o comando di avvio automatico per eseguire PCManFM come [demone](/index.php/Daemon_(Italiano) "Daemon (Italiano)")/ processo in background (cioè per l'automount di supporti rimovibili come CD/DVD e flash-drive USB) è :

```
pcmanfm -d

```

## Avvio automatico

La maniera in cui PCManFM può essere avviato come [daemon](/index.php/Daemon_(Italiano) "Daemon (Italiano)") o come gestore del desktop in combinazione con un [window manager](/index.php/Window_manager_(Italiano) "Window manager (Italiano)") indipendente, varia in base al window manager stesso. Per esempio, per abilitare la gestione del desktop da parte di PCManFM utilizzando [Openbox](/index.php/Openbox_(Italiano) "Openbox (Italiano)"), sarà necessario aggiungere questa riga al file `~/.config/openbox/autostart`

 `pcmanfm --desktop &` 

Rivedere l'articolo wiki pertinente e/o l'home page ufficiale per uno specifico window manager. Se un window manager non fornisce un file autostart, PCManFM può essere alternativamente autoavviato modificando uno o entrambi dei seguenti file :

*   [xinitrc](/index.php/Xinitrc "Xinitrc"): Quando si usa [SLiM](/index.php/SLiM_(Italiano) "SLiM (Italiano)") come [display manager](/index.php/Display_manager_(Italiano) "Display manager (Italiano)") o il comando [Startx](/index.php?title=Startx_(Italiano)&action=edit&redlink=1 "Startx (Italiano) (page does not exist)")
*   [xprofile](/index.php/Xprofile "Xprofile"): Quando si usa un display manager come [LXDM](/index.php/LXDM_(Italiano) "LXDM (Italiano)") or [LightDM](/index.php?title=LightDM_(Italiano)&action=edit&redlink=1 "LightDM (Italiano) (page does not exist)")

## Ulteriori caratteristiche e funzionalità

Gli utenti meno esperti dovrebbero essere consapevoli che un file manager da solo - soprattutto quando installato in un autonomo [Window manager](/index.php/Window_manager_(Italiano) "Window manager (Italiano)") come Openbox - non fornirà le caratteristiche e le funzionalità di ambienti desktop completi come Xfce e KDE. Rivedere l'articolo [File manager functionality](/index.php/File_manager_functionality "File manager functionality") per ulteriori informazioni.

## Consigli e trucchi

### Un clic per aprire cartelle e files

Aprire PCManFM in modalità File Explorer, andare in *Modifica> Preferenze>Generali>Comportamento*, e selezionare *Apri i file con un solo click*. Questa opzione funziona anche con le icone del desktop.

### Aprire ed estrarre archivi con PCManFM

Installare [file-roller](https://www.archlinux.org/packages/?name=file-roller) o [xarchiver](https://www.archlinux.org/packages/?name=xarchiver) dagli official repositories.

Aprire PCManFM in modalità File Explorer, andare in *Modifica> Preferenze>Avanzate*, selezionare *Integrazione Archivi* e selezionare l'archiviatore installato.

## Risoluzione dei problemi

### Apertura finestra di dialogo vuota

Se nella finestra di dialogo non sono presenti tutte le applicazioni installate, allora si può provare a rimuovere [gnome-menus](https://www.archlinux.org/packages/?name=gnome-menus) e installare al suo posto [lxmenu-data](https://www.archlinux.org/packages/?name=lxmenu-data). Inoltre, è necessario esportare le seguenti variabili :

```
export XDG_MENU_PREFIX=lxde-
export XDG_CURRENT_DESKTOP=LXDE

```

### Nessuna "Applicazione"

Si può provare questo metodo: Eliminare tutti i file presenti nella cartella `$HOME/.cache/menu` ed eseguire nuovamente PCManFM.

PCManFM richiede la variabile di ambiente *XDG_MENU_PREFIX* da impostare. Il valore della variabile deve essere contenuta all'inizio di un file presente nella cartella `/etc/xdg/menus/`. Ad esempio è possibile impostare il valore nel file `xinitrc` con la riga:

```
export XDG_MENU_PREFIX="lxde-"

```

Vedere questi thread per maggiori informazioni: [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1110903), e in particolare questo post dal forum Linux Mint: [[2]](http://forums.linuxmint.com/viewtopic.php?f=175&t=53986#p501920)

### Nessuna icona

Se si utilizza un WM invece di un DE e non avete le icone per le cartelle e i files, è necessario specificare il tema di icone GTK+ usato.

Se si dispone ad esempio di [oxygen-icons](https://www.archlinux.org/packages/?name=oxygen-icons) installato, modificare `~/.gtkrc-2.0` **o** `/etc/gtk-2.0/gtkrc` e aggiungere la seguente riga:

```
gtk-icon-theme-name = "oxygen"

```

**Note:** Tutte le istanze di PCManFM devono essere riavviate per applicare le modifiche!

Altrimenti, utilizzare un diverso tema (*gnome*, *hicolor*, e *locolor* non funzionano). Per elencare tutti i temi di icone installati, digitare il seguente comando:

```
$ ls ~/.icons/ /usr/share/icons/

```

Se nessuno di essi è adatto, installarne un altro. Per elencare tutti i pacchetti di icone installabili:

```
$ pacman -Ss icon-theme

```

**Tip:** Per una soluzione grafica alternativa, installare [lxappearance](https://www.archlinux.org/packages/?name=lxappearance) e applicare un tema di icone da lì.

### Nessuna funzionalità "Cartella precedente/successiva" con i pulsanti del mouse

Un metodo per risolvere questo problema è usare [Xbindkeys](/index.php/Xbindkeys "Xbindkeys").

Installare [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys) e modificare `~/.xbindkeysrc` aggiungendo le seguenti righe:

```
# Sample .xbindkeysrc for a G9x mouse.
"/usr/bin/xvkbd -text '\[Alt_L]\[Left]'"
 b:8
"/usr/bin/xvkbd -text '\[Alt_L]\[Right]'"
 b:9

```

Altri Codici pulsante possono essere ottenuti con il pacchetto [xorg-xev](https://www.archlinux.org/packages/?name=xorg-xev).

Aggiungere:

```
xbindkeys &

```

al proprio `~/.xinitrc` per eseguire xbindkeys al log-in.

### Paramentri --desktop non funzionano o crash del X-server

Assicurarsi di avere i permessi di proprietà e di scrittura su `~/.config/pcmanfm`.

Impostare lo sfondo utilizzando il parametro `--desktop-pref` o modificando `~/.config/pcmanfm/default/pcmanfm.config` per risolvere il problema.

### Mancato salvataggio delle configurazioni avanzati dell'Emulatore di terminale

Assicurarsi di avere i permessi sul file di configurazione libfm :

```
$ chmod -R 755 ~/.config/libfm
$ chmod 777 ~/.config/libfm/libfm.conf

```

### Memorizzare impostazioni Ordine files preferite

È possibile utilizzare *Visualizza>Ordina file* per cambiare l' ordine in cui PCManFM elenca i file, ma le impostazioni saranno cancellate al successivo avvio di PCManFM. Per memorizzarle, andare su *Modifica> Preferenze* e *Chiudi*. Questo scriverà i valori sort_type e sort_by correnti in `~/.config/pcmanfm/LXDE/pcmanfm.conf`.

### Errore "Non autorizzato" all'accesso/montaggio di unità USB

Guarda la sezione [no password to access partitions and removable media](/index.php/File_manager_functionality#No_password_to_access_partitions_and_removable_Media "File manager functionality") della pagina [File manager functionality](/index.php/File_manager_functionality "File manager functionality").