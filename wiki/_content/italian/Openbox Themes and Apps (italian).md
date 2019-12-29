**Nota:** Questo articolo è un supplemento all'articolo originale [Openbox (Italiano)](/index.php/Openbox_(Italiano) "Openbox (Italiano)").

Questo articolo spiega come personalizzare l'aspetto di Openbox su Arch Linux. Sono menzionati anche programmi ausiliari come pannelli e tray.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Temi e aspetto](#Temi_e_aspetto)
    *   [1.1 Temi di Openbox](#Temi_di_Openbox)
    *   [1.2 Aspetto di X11](#Aspetto_di_X11)
    *   [1.3 Cursori per il mouse in X11](#Cursori_per_il_mouse_in_X11)
    *   [1.4 Temi GTK](#Temi_GTK)
        *   [1.4.1 GTK2/GTK+](#GTK2/GTK+)
        *   [1.4.2 GTK1](#GTK1)
        *   [1.4.3 Caratteri GTK](#Caratteri_GTK)
        *   [1.4.4 Icone GTK](#Icone_GTK)
    *   [1.5 Icone sul desktop](#Icone_sul_desktop)
    *   [1.6 Sfondo del desktop](#Sfondo_del_desktop)
*   [2 Programmi consigliati](#Programmi_consigliati)
    *   [2.1 Login Manager](#Login_Manager)
    *   [2.2 Desktop Composite](#Desktop_Composite)
    *   [2.3 Pannelli, vassoi di sistema e paginatori](#Pannelli,_vassoi_di_sistema_e_paginatori)
        *   [2.3.1 Pannelli](#Pannelli)
        *   [2.3.2 Vassoi di sistema](#Vassoi_di_sistema)
        *   [2.3.3 Paginatori](#Paginatori)
    *   [2.4 File Manager](#File_Manager)
    *   [2.5 Lanciatori di applicazioni](#Lanciatori_di_applicazioni)
        *   [2.5.1 dmenu](#dmenu)
        *   [2.5.2 Gmrun](#Gmrun)
        *   [2.5.3 Bashrun](#Bashrun)
        *   [2.5.4 Launchy](#Launchy)
        *   [2.5.5 LXPanel](#LXPanel)
        *   [2.5.6 gnome-panel](#gnome-panel)
    *   [2.6 Clipboard managers](#Clipboard_managers)
    *   [2.7 Gestori del Volume](#Gestori_del_Volume)
        *   [2.7.1 gvolwheel](#gvolwheel)
        *   [2.7.2 gvtray](#gvtray)
        *   [2.7.3 obmixer](#obmixer)
        *   [2.7.4 volti](#volti)
        *   [2.7.5 volumeicon](#volumeicon)
        *   [2.7.6 volwheel](#volwheel)
    *   [2.8 Switcher per il layout della tastiera](#Switcher_per_il_layout_della_tastiera)
        *   [2.8.1 fbxkb](#fbxkb)
        *   [2.8.2 xxkb](#xxkb)
        *   [2.8.3 axkb](#axkb)
        *   [2.8.4 xneur](#xneur)

## Temi e aspetto

### Temi di Openbox

I temi di Openbox controllano l'aspetto dei bordi delle finestre, inclusi la barra del titolo e i tasti della barra. Determinano anche l'aspetto del menu dell'applicazione e dell'on-screen display (OSD). Altri temi sono disponibili nei repository ufficiali:

 `# pacman -S openbox-themes` 

Questo pacchetto non è assolutamente definitivo. Esistono anche altre risorse in rete per reperire temi per Openbox, come:

*   [box-look.org](http://www.box-look.org/index.php?xcontentmode=7402)
*   [customize.org](http://customize.org/browse/tags/openbox)
*   [http://www.minuslab.net/themes/](http://www.minuslab.net/themes/)
*   [http://celo.wordpress.com/themes/](http://celo.wordpress.com/themes/)
*   [http://vault.openmonkey.com/pages/openbox](http://vault.openmonkey.com/pages/openbox)
*   [http://hewphoria.com/?p=submission&type=theme&cat=7](http://hewphoria.com/?p=submission&type=theme&cat=7)

I temi scaricati vanno estratti nella cartella `~/.themes` e possono essere installati o selezionati con lo strumento ObConf.

Creare nuovi temi è alquanto semplice e [ben documentato](http://openbox.org/wiki/Help:Themes).

per un editor grafico dei temi, vedere [ObTheme](http://xyne.archlinux.ca/info/obtheme).

### Aspetto di X11

Se state eseguendo Openbox a se stante, sarà necessario configurare il file `.Xdefaults`. Salvare una copia in `~/.Xdefaults` e in `/home/root/.Xdefaults` per le finestre aperte come root.

Xdefaults è una configurazione dotfile a livello utente, in genere si trova in `~/.Xdefaults`. Quando è presente, viene analizzato dal `xrdb` (database delle risorse di Xorg) programma che viene avviato automaticamente con Xorg, e può essere utilizzato per impostare o ignorare le preferenze per le applicazioni X e X. Si possono fare molte operazioni, tra cui:

*   Definire i colori del terminale.
*   Configurare le preferenze del terminale.
*   Impostare DPI, antialiasing, hinting e altre impostazioni dei caratteri in X.
*   Cambiare il tema Xcursor
*   Impostare un tema xscreensaver
*   Modificare le preferenze di basso livello delle applicazioni in Xs (xclock, xpdf, etc.)

Vedere [Xdefaults Arch WiKi](/index.php/Xdefaults "Xdefaults")

### Cursori per il mouse in X11

Estrarre il tema dell'Xcursor desiderato o nella cartella `/usr/share/icons` (per accesso in tutto il sistema) o `~/.icons` (per accesso al solo utente).Ci sono anche un numero limitato di temi disponibili nel repository community che può essere installato utilizzando pacman.

Aggiungere quanto segue al file `~/.Xdefaults`:

```
Xcursor.theme:  [nome-tema-cursore]

```

dove `[nome-tema-cursore]` è il nome della cartella del tema del cursore. Ad esempio:

```
Xcursor.theme: Vanilla-DMZ-AA

```

Per modificarne le dimensioni:

```
Xcursor.size: [size]

```

A volte è necessario fare un link simbolico dell'icona nella propria directory utente per fare in modo che il windows manager lo utilizzi:

```
$ mkdir ~/.icons
$ ln -s /usr/share/icons/[name-of-cursor-theme] ~/.icons/default

```

Per ulteriori informazioni consultare il wiki [Cursori in X11](/index.php/X11_Cursors_(Italiano) "X11 Cursors (Italiano)")

### Temi GTK

#### GTK2/GTK+

Estrarre il tema desiderato in `/usr/share/themes` (per accesso in tutto il sistema) o in `~/.themes` (per accesso al solo utente). I temi GTK2 possono essere facilmente gestiti con **[lxappearance](/index.php/LXDE "LXDE")**, **gtk-chtheme**, o **switch2**:

```
# pacman -S lxappearance

```

e/o

```
# pacman -S gtk-chtheme

```

e/o

```
# pacman -S gtk-theme-switch2

```

Ora basta eseguire il comando `lxappearance`, `gtk-chtheme` o `switch2` e scegliere il tema desiderato.

#### GTK1

Per i vecchi temi GTK1, installare il pacchetto **gtk-theme-swithch**:

```
# pacman -S gtk-theme-switch

```

Dopodiché eseguire il comando `switch` e selezionare il tema desiderato.

#### Caratteri GTK

Se si vuole cambiare il tipo e la dimensione dei propri caratteri, aggiungere quanto segue al file `~/.gtkrc.mine`:

```
style "user-font"
{
font_name = "[nome-carattere] [dimensione]"
}
widget_class "*" style "user-font"
gtk-font-name = "[nome-carattere] [dimensione]"

```

Dove `[nome-carattere]` e `[dimensione]` sono il carattere desiderato e le dimensioni del testo in pt. Ad esempio:

```
style "user-font"
{
font_name = "DejaVu Sans 8"
}
widget_class "*" style "user-font"
gtk-font-name = "DejaVu Sans 8"

```

I campi `font_name` e `gtk-font-name` sono entrambi richiesti per compatibilità con vecchie applicazioni.

#### Icone GTK

Estrarre il tema di icone desiderato nella cartella `/usr/share/icons<`> (per accesso in tutto il sistema) o <`~/.icons` (per accesso solo per l'utente).

Aggiungere quanto segue al file ~/.gtkrc.mine:

```
gtk-icon-theme-name = "[nome-tema-icone]"

```

dove [nome-tema-icone] è il nome della cartella del tema di icone. Ad esempio:

```
gtk-icon-theme-name = "Tango"

```

Assicurarsi che `~/.gtkrc-2.0` sia configurato per eseguire file `~/.gtkrc.mine`:

```
# ~/.gtkrc-2.0
# -- THEME AUTO-WRITTEN DO NOT EDIT
include "/usr/share/themes/Rezlooks-Gilouche/gtk-2.0/gtkrc"
include "/home/username/.gtkrc.mine"
# -- THEME AUTO-WRITTEN DO NOT EDIT

```

Potete utilizzare **lxappearance** per scegliere i temi delle icone GTK. In tal caso si prega di fare riferimento alla sezione precedente.

Si potrebbe utilizzare [lxappearance2-git](https://aur.archlinux.org/packages.php?ID=39339) reperibile su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") per gestire i cursori del mouse, i temi GTK, set di icone e schemi di colore. Se si installa anche il pacchetto facoltativo [lxappearance-obconf-git](https://aur.archlinux.org/packages/lxappearance-obconf-git/), è possibile configurare le impostazioni del decoratore delle finestre di Openbox direttamente da lxapparence.

### Icone sul desktop

Openbox non provvede un modo di mostrare le icone sul desktop. Xfdesktop, [ROX](http://rox.sourceforge.net), [iDesk](/index.php/Idesk "Idesk"), o anche Nautilus (e il gnome-settings-daemon) possono provvedere questa funzione. ROX ha il vantaggio aggiuntivo di essere un gestore di file leggero.

### Sfondo del desktop

Openbox in sé non include un modo per cambiare lo sfondo del desktop. Questo può essere raggiunto facilmente con programmi come [Feh](/index.php/Feh "Feh") o [Nitrogen](/index.php/Nitrogen "Nitrogen"). Altre opzioni includono ImageMagick, hsetroot e xsetbg. Anche PCManFM e xfdesktop possono provvedere ad impostarlo.

È possibile disattivare il caricamento dello sfondo in gnome-settings-daemon in questo modo:

```
$ gconftool-2 --set /apps/gnome_settings_daemon/plugins/background/active --type bool False

```

## Programmi consigliati

Esiste una [lista di software leggero](/index.php/Lightweight_Applications "Lightweight Applications") sul wiki di Arch, molti dei quali si intonano perfettamente con openbox

### Login Manager

[SLiM](http://slim.berlios.de/) provvede una soluzione di login leggera ed elegante per le configurazioni di Openbox soltanto (senza GNOME o KDE). Fare riferimento alla wiki di Arch su [SLiM](/index.php/SLiM "SLiM") per istruzioni dettagliate.

[Qingy](http://qingy.sourceforge.net/) è un gestore di login grafico ultraleggero ed altamente configurabile. Supporta login sia da console che da sessioni grafiche. Usa [DirectFB](http://www.directfb.org), perciò non avvia la sessione grafica finchè l'utente non lo decide. Ulteriori informazioni [Qingy](/index.php/Qingy "Qingy") sul wiki di Arch.

### Desktop Composite

[xcompmgr](/index.php/Xcompmgr "Xcompmgr") è un composite manager leggero in grado di creare ombre, finestre in dissolvenza e trasparenza sia in Openbox che in altri window manager.(È bene segnalare che xcompmgr non è più mantenuto, sicchè eventuali problemi o bug non saranno risolti) (È noto un conflitto con tint2 0.9, l'icona del vassoio di sistema ha la tendenza a dare qualche problema)

### Pannelli, vassoi di sistema e paginatori

Ci sono un bel numero di pannelli da installare per provvedere una taskbar e un pager per Openbox. I più comuni sono:

#### Pannelli

*   [PyPanel](/index.php/PyPanel "PyPanel")
*   [BMPanel](http://nsf.110mb.com/bmpanel/)
*   [tint2](/index.php/Tint2 "Tint2")
*   [LXPanel](http://www.gnomefiles.org/app.php/LXPanel)
*   [fbpanel](http://fbpanel.sourceforge.net)
*   [PerlPanel](http://freshmeat.net/projects/perlpanel/)
*   [fspanel](http://www.chatjunkies.org/fspanel/)
*   [Xfce4-panel](http://www.xfce.org/projects/xfce4-panel/)
*   [GnomePanel](http://live.gnome.org/GnomePanel/)
*   [avant-window-navigator](https://launchpad.net/awn)
*   [cairo-dock](http://developer.berlios.de/projects/cairo-dock/)
*   [wbar](http://code.google.com/p/wbar/)
*   [screenlets](http://www.screenlets.org/)
*   [pancake](http://www.failedprojects.de/pancake/)

#### Vassoi di sistema

*   [Stalonetray](http://stalonetray.sourceforge.net/)
*   [Trayer](http://download.gna.org/fvwm-crystal/trayer/1.0/)

#### Paginatori

*   [Visibility](http://projects.l3ib.org/trac/visibility)
*   [bbpager](http://bbtools.sourceforge.net/)
*   [netwmpager](https://aur.archlinux.org/packages.php?ID=17563)
*   [IPager](http://useperl.ru/ipager/index.en.html)
*   [neap](http://code.google.com/p/neap/)

Dopo averne scelto uno, aggiungerlo al file di esecuzione automatica. Se si desidera impostare il layout del desktop senza l'utilizzo di un paginatore è possibile utilizzare [obsetlayout](https://aur.archlinux.org/packages/obsetlayout/) che è una versione pacchettizzata di strumento setLayout dal wiki Openbox.

### File Manager

Ci sono diverse possibilità, ma i gestori di file più leggeri e popolari sono:

*   [Thunar](/index.php/Thunar "Thunar") (Supporta funzionalità di auto-mount features e altri plugin)
*   [ROX](http://rox.sourceforge.net) (ROX provvede anche icone sul desktop)

```
# pacman -S rox

```

*   [PCMan](http://pcmanfm.sourceforge.net) (molto leggero e in grado di provvedere icone sul desktop)

```
# pacman -S pcmanfm

```

Per avere accesso al file system NTFS con PCManFM, installare

```
# pacman -S ntfs-3g

```

Per opzioni ancora più leggere, considerare [Gentoo](http://www.obsession.se/gentoo/) o [emelFM](http://emelfm.sourceforge.net/), entrambi dei quali usano la struttura a due pannelli come il Midnight Commander (entrambi richiedono GTK 1.2.x).

Altri: Xfe muCommander

Ovviamente si può utilizzare anche Nautilus. Sebbene sia più lento delle soluzioni elencate, ha il vantaggio addizionale del supporto VFS (ad esempio SSH remoto, connessioni FTP e Samba).

### Lanciatori di applicazioni

#### dmenu

La configurazione di dmenu è descritta nella sezione [dmenu](/index.php/Dmenu "Dmenu") del wiki. Di seguito aggiungere la seguente voce <keyboard> section `~/.config/openbox/rc.xml` per abilitare una scorciatoia d'avvio al dmenu:

```
   <keybind key="W-space">
     <action name="Execute">
       <execute>dmenu_run</execute>
     </action>
   </keybind>

```

#### [Gmrun](/index.php/Gmrun "Gmrun")

[gmrun](http://sourceforge.net/projects/gmrun) fornisce un'ottima finestra d'avvio, simile alla funzione Alt+F2 di GNOME e KDE:

```
# pacman -S gmrun

```

Vedere [Gmrun](/index.php/Gmrun "Gmrun") per maggiori informazioni.

Aggiungere quanto segue alla sezione <keyboard> nel file `~/.config/openbox/rc.xml` per abilitare la funzionalità Alt+F2:

```
<keybind key="A-F2">
<action name="execute"><execute>gmrun</execute></action>
</keybind>

```

#### Bashrun

[bashrun](http://bashrun.sourceforge.net) fornisce un differente, e alquanto basilare approccio, usando una speciale sessione bash in una piccola finestra xterm. È disponibile nei community repository e può essere lanciata in stile Alt+F2 come menzionato sopra. Per rendere l'avvio di bash in uno stile ancora più tradizionalista, aggiungere la seguente voce nella sezione <applicazioni> `~/.config/openbox/rc.xml`:

```
   <application name="bashrun">
     <desktop>all</desktop>
     <decor>no</decor>  # switch to yes if you prefer a bordered window
     <focus>yes</focus>
     <skip_pager>yes</skip_pager>
     <layer>above</layer>
   </application>

```

#### Launchy

[Launchy](http://www.launchy.net/) è già un qualcosa di meno minimalista; è possibile cambiare le interfaccie grafiche e offre altre funzionalità come la calcolatrice, le condizioni meteo, etc. Originariamente destinato a Windows, è simile a Gnome Do.

```
# pacman -S launchy

```

Lo si può lanciare con la combinazione di tasti Ctrl+Space.

#### LXPanel

LXPanel può essere eseguito con

```
lxpanelctl run

```

#### gnome-panel

Gnome-panel può essere eseguito con

```
gnome-panel-control --run-dialog

```

### Clipboard managers

Si potrebbe voler installare un clipboard manager per operazioni come il copia/incolla. **xfce4-clipman-plugin, parcellite,** oppure **glipper-old** possono essere installate con pacman. Aggiungere la propria scelta su autostart.sh. Dal terminale, Ctrl+Insert per il comando copia e Shift+Insert per incolla generalmente funzionano bene. È anche possibile copiare dal terminale Ctrl+Shift+C, e incollare con il bottone centrale del mouse.

### Gestori del Volume

#### gvolwheel

Un mixer audio leggero che permette di controllare il volume audio attraverso un icona nella barra [[1]](https://aur.archlinux.org/packages.php?ID=25502)

#### gvtray

Un mixer per il canale *master* nel vassoio di sistema [[2]](https://aur.archlinux.org/packages.php?ID=6362)

#### obmixer

Obmixer è un appplet mixer scritto in C, che è destinato a essere una alternativa leggera al controllo del volume di gnome [[3]](https://aur.archlinux.org/packages.php?ID=31131)

#### volti

Applicazione GTK+ per controllare il volume audio dalla barra di sistema/area di notifica [[4]](https://aur.archlinux.org/packages.php?ID=33525)

#### volumeicon

Controllo del volume per il vassoio di sistema [[5]](https://aur.archlinux.org/packages.php?ID=35793)

#### volwheel

Icona del vassoio per modificare il volume con il mouse [volwheel](https://aur.archlinux.org/packages/volwheel/)

### Switcher per il layout della tastiera

#### fbxkb

Indicatore di tastiera e switcher [[6]](https://aur.archlinux.org/packages.php?ID=3458)

#### xxkb

Indicatore di tastiera e switcher [xxkb](https://www.archlinux.org/packages/?name=xxkb)

#### axkb

Switcher per il layout della tastiera scritto in QT4 [[7]](https://aur.archlinux.org/packages.php?ID=25555)

#### xneur

X Neural Switcher è un analizzatore di testo, che rileva la lingua di input e la corregge se necessario [[8]](https://aur.archlinux.org/packages.php?ID=9750)