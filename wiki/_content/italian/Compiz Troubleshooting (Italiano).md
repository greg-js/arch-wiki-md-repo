## Contents

*   [1 Tornare indietro](#Tornare_indietro)
    *   [1.1 Tornare indietro con KDE](#Tornare_indietro_con_KDE)
    *   [1.2 Tornare indietro con GNOME](#Tornare_indietro_con_GNOME)
    *   [1.3 Tornare indietro con XFCE](#Tornare_indietro_con_XFCE)
*   [2 Missing GLX_EXT_texture_from_pixmaps](#Missing_GLX_EXT_texture_from_pixmaps)
    *   [2.1 Con schede video ATI (prima soluzione)](#Con_schede_video_ATI_.28prima_soluzione.29)
    *   [2.2 Con schede video ATI (seconda soluzione)](#Con_schede_video_ATI_.28seconda_soluzione.29)
    *   [2.3 Con i chip Intel](#Con_i_chip_Intel)
*   [3 Fusion-Icon mostra una "X" rossa nella barra di stato e non viene visualizzata l'icona nei menù](#Fusion-Icon_mostra_una_.22X.22_rossa_nella_barra_di_stato_e_non_viene_visualizzata_l.27icona_nei_men.C3.B9)
*   [4 Compiz è avviato, ma non è visibile nessun effetto](#Compiz_.C3.A8_avviato.2C_ma_non_.C3.A8_visibile_nessun_effetto)
*   [5 Compiz si avvia, diversamente da gtk-window-decorator](#Compiz_si_avvia.2C_diversamente_da_gtk-window-decorator)
*   [6 Compiz sembra avviarsi, ma non ci sono i bordi delle finestre](#Compiz_sembra_avviarsi.2C_ma_non_ci_sono_i_bordi_delle_finestre)
*   [7 Compiz si avvia e i bordi appaiono, ma le finestre non si muovono](#Compiz_si_avvia_e_i_bordi_appaiono.2C_ma_le_finestre_non_si_muovono)
*   [8 Schermo vuoto quando il computer si riprende dalla suspend-to-ram utilizzando i driver binari di Nvidia](#Schermo_vuoto_quando_il_computer_si_riprende_dalla_suspend-to-ram_utilizzando_i_driver_binari_di_Nvidia)
*   [9 fusion-icon non si avvia](#fusion-icon_non_si_avvia)
*   [10 Animazioni instabili, nonostante tutto sia stato configurato correttamente](#Animazioni_instabili.2C_nonostante_tutto_sia_stato_configurato_correttamente)
*   [11 Risolvere gli screenshot in Gnome](#Risolvere_gli_screenshot_in_Gnome)
*   [12 Far funzionare con Compiz-Fusion il GNOME Workspace Switcher](#Far_funzionare_con_Compiz-Fusion_il_GNOME_Workspace_Switcher)
*   [13 Lo schermo lampeggia con scheda video NVIDIA](#Lo_schermo_lampeggia_con_scheda_video_NVIDIA)
*   [14 Risolvere il tema del cursore di base in Gnome 2.30](#Risolvere_il_tema_del_cursore_di_base_in_Gnome_2.30)
*   [15 Artefatti dello schermo in Firefox / Thunderbird](#Artefatti_dello_schermo_in_Firefox_.2F_Thunderbird)
*   [16 Impostare di nuovo Metacity come gestore di finestre dopo la disinstallazione](#Impostare_di_nuovo_Metacity_come_gestore_di_finestre_dopo_la_disinstallazione)
*   [17 Wallpaper del desktop e xorg-server 1.9](#Wallpaper_del_desktop_e_xorg-server_1.9)
*   [18 Il menu contestuale in alcune applicazioni (firefox, ...?) scompare quando il mouse ci passa sopra](#Il_menu_contestuale_in_alcune_applicazioni_.28firefox.2C_....3F.29_scompare_quando_il_mouse_ci_passa_sopra)
*   [19 Note esterne](#Note_esterne)

## Tornare indietro

### Tornare indietro con KDE

Se si sta utilizzando KDE e qualcosa non va per il verso giusto, ad esempio non si riescono a visualizzare i bordi delle finestre, si può tornare a kwin con questo comando:

```
 kwin --replace

```

### Tornare indietro con GNOME

Se si sta utilizzando GNOME e qualcosa non va per il verso giusto, ad esempio non si riescono a visualizzare i bordi delle finestre, si può tornare a metacity con questo comando:

```
metacity --replace

```

### Tornare indietro con XFCE

Se si sta utilizzando XFCE e qualcosa non va per il verso giusto, ad esempio non si riescono a visualizzare i bordi delle finestre, si può tornare a xfce window manager (xfwm4) con questo comando:

```
xfwm4 --replace

```

## Missing GLX_EXT_texture_from_pixmaps

### Con schede video ATI (prima soluzione)

[https://bbs.archlinux.org/viewtopic.php?id=50073](https://bbs.archlinux.org/viewtopic.php?id=50073) Se si ottiene il seguente errore mentre si cerca di avviare Compiz Fusion con una scheda video ATI:

```
Missing GLX_EXT_texture_from_pixmap

```

Ciò è dovuto al fatto che il file binario di Compiz Fusion è stato compilato per le librerie OpenGL di Mesa piuttosto che quelle OpenGL di ATI (che sono quelle che si stanno utilizzando). Si reinstalli quindi libgl-dri (sì, è necessario momentaneamente disinstallare anche fglrx) per ottenere le librerie OpenGL dei driver Mesa.

Copiare quindi le librerie in una cartella per mantenerle dal momento che i driver ATI andranno a sovrascriversi ad esse.

```
mkdir /lib/mesa
cp /usr/lib/libGL.so.1.2 /lib/mesa

```

Una volta copiate, è possibile reinstallare i propri driver fglrx (dovrebbero essere stati rimossi quando si è installato il pacchetto libgl-dri). Ora si può avviare Compiz Fusion utilizzando la seguente sintassi d'esempio:

```
LD_PRELOAD=/lib/mesa/libGL.so.1.2 compiz --replace &

```

### Con schede video ATI (seconda soluzione)

Un altro problema può sorgere riguardo GLX_EXT_texture_from_pixmap, è infatti possibile che la scheda video sia in grado di renderle solamente in maniera indiretta, in questo caso è necessario passare un'opzione come questa al proprio libgl:

```
 LIBGL_ALWAYS_INDIRECT=1 compiz --replace ccp &

```

(Soluzione verificata sulle seguenti schede video: ATI Technologies Inc Radeon R250 [Mobility FireGL 9000] (rev 02))

### Con i chip Intel

Innanzitutto, assicurarsi di utilizzare i driver intel piuttosto che gli i810\. Quindi, lanciare il seguente comando per avviare compiz (dovrà essere fatto ogni volta).

```
LIBGL_ALWAYS_INDIRECT=true compiz --replace --sm-disable ccp &

```

Se non si riesce a visualizzare i bordi, lanciare

```
emerald --replace

```

Dal 17-Ott-07 il [Compiz-Fusion Wiki](http://wiki.compiz-fusion.org/Troubleshooting) dichiara: _"Se si sta utilizzando una scheda video Intel GMA con AIGLX, è necessario avviare Compiz Fusion con l'opzione LIBGL_ALWAYS_INDIRECT=1._"

## Fusion-Icon mostra una "X" rossa nella barra di stato e non viene visualizzata l'icona nei menù

La cache delle icone GTK necessita di essere aggiornata (sperando che l'icona sia stata aggiunta dal file .install del pacchetto). Lanciare il comando seguente:

```
# gtk-update-icon-cache -f /usr/share/icons/hicolor

```

se questa soluzione non dovesse risolvere il problema, provare ad installare il pacchetto hicolor-icon-theme:

```
# pacman -S hicolor-icon-theme

```

Risolto con il nuovo pacchetto in community.

## Compiz è avviato, ma non è visibile nessun effetto

Nel caso si abbia installato il pacchetto compiz-decorator-gtk: assicurarsi che lo schema GConf sia stato installato correttamente:

```
 gconftool-2 -R /apps/compiz/plugins | grep plugins

```

assicurarsi quindi che tutti i plugin siano elencati (non solo scoloriti!). Nel caso non lo siano, provare ad installare manualmente lo schema di compiz (farlo da utente normale, non da root!!!):

```
 gconftool-2 --install-schema-file=/usr/share/gconf/schemas/compiz-decorator-gtk.schemas

```

Note: I plugin base di Compiz non sono abilitati di base. Occorre abilitare i plugin "Move Window", "Resize Window", e "Window decoration" nel gestore delle impostazioni attraverso la fusion-icon per ottenere un gestore di finestre funzionante.

## Compiz si avvia, diversamente da gtk-window-decorator

Questo è un problema di configurazione per gconf e gconfd. Un utente afferma di poter risolvere rimuovendo la cartella ".gconf" nella propria home, ma lui usava KDE. Nel caso si utilizzi Gnome si dovrebbe entrare nella propria cartella ".gconf" e rimuovere tutte le voci relative a compiz. Ciò cancellerà le impostazioni di compiz, così da permettere la riconfigurazione. Alla fine si esegua da utente:

```
 gconftool-2 --install-schema-file=/usr/share/gconf/schemas/compiz-decorator-gtk.schemas

```

## Compiz sembra avviarsi, ma non ci sono i bordi delle finestre

Se si avvia fusion-icon da riga di comando, e l'output è qualcosa di simile:

```
* Detected Session: gnome
* Searching for installed applications...
* NVIDIA on Xorg detected, exporting: __GL_YIELD=NOTHING
* Using the GTK Interface
* Metacity is already running
* Setting window manager to Compiz
... executing: compiz --replace --sm-disable --ignore-desktop-hints ccp
compiz (core) - Warn: No GLXFBConfig for depth 32
compiz (core) - Warn: No GLXFBConfig for depth 32
compiz (core) - Warn: No GLXFBConfig for depth 32
compiz (core) - Warn: No GLXFBConfig for depth 32
compiz (core) - Warn: No GLXFBConfig for depth 32
compiz (core) - Warn: No GLXFBConfig for depth 32

```

Tutto ciò che serve è di modificare il proprio /etc/X11/xorg.conf trovando l'istruzione "Depth" nella sezione "Screen" e cambiando tutti i valori a 24\. Questo problema si è presentato ad alcuni utenti che avevano come valore della colour depth impostata a 16; ma si presenta anche quando questo valore è impostato a 32.

* * *

Si potrebbe provare anche ad aggiungere _Option "AddARGBGLXVisuals" "True"_ & _Option "DisableGLXRootClipping" "True"_ alla propria sezione "Screen" nel caso si utilizzino i driver binari di Nvidia. (Quelli radeon, e i driver open 'nv' non funzioneranno con questa opzione per quanto ne sappia). Nel caso si utilizzi qualsiasi altra Options da qualche parte nel xorg.conf per far funzionare compiz ma ancora senza fortuna, si provi a decommentarla e ad usare solamente la suddetta opzione ARGBGLXVisuals e GLXRootClipping.

**Note**: Assicurarsi che i plugin "Window decoration", "Move" e "Resize" siano abilitati con il gestore d'effetti di Compiz o con gconf-editor.

Con gconf-editor è facilmente possibile abilitare i plugin "Window decoration", "Move" e "Resize".

```
 $ gconf-editor

```

Si navighi in apps/compiz/general/allscreens/options

Si aggiunga/Si modifichi "active_plugins" Key (Name: active_plugins, Type: List, List type: String).

Si aggiunga "decoration", "move", e "resize" alla lista.

* * *

**Un'altra maniera per risolvere questo problema**:

*   Si apra **ccsm** (lo si avvii come un comando dal terminale, o lo si avvii attraverso il menù Sistema).
*   Si trovi la voce **windows decoration** e assicurarsi che sia abilitata.
*   Ora la si selezioni per modificarne le opzioni.
*   Se lo spazio dopo **command** è vuoto, mettere lì il valore **gtk-window-decorator**.
    *   Le alternative sono **kde-window-decorator** e **emerald**
*   Si selezioni **Indietro** e **Chiudere**
*   Se tutto è andato per il verso giusto, i bordi dovrebbero apparire.

## Compiz si avvia e i bordi appaiono, ma le finestre non si muovono

Assicurarsi di aver installato il plugin "Move Window" e di averlo abilitato nel gestore delle impostazioni di compiz.

## Schermo vuoto quando il computer si riprende dalla suspend-to-ram utilizzando i driver binari di Nvidia

Se si ottiene uno schermo vuoto con un cursore reattivo dopo il risveglio, si provi a disabilitare la sincronizzazione con vblank:

```
gconftool -s /apps/compiz/general/screen0/options/sync_to_vblank-t boolean false

```

## fusion-icon non si avvia

Nel caso si ottenga un output come questo dalla linea di comando:

```
[andy@andylaptop ~]$ fusion-icon
 * Detected Session: gnome
 * Searching for installed applications...
Traceback (most recent call last):
  File "/usr/bin/fusion-icon", line 57, in <module>
    from FusionIcon.interface import choose_interface
  File "/usr/lib/python2.5/site-packages/FusionIcon/interface.py", line 23, in <module>
    import start
  File "/usr/lib/python2.5/site-packages/FusionIcon/start.py", line 36, in <module>
    config.check()
  File "/usr/lib/python2.5/site-packages/FusionIcon/util.py", line 362, in check
    os.makedirs(self.config_folder)
  File "/usr/lib/python2.5/os.py", line 172, in makedirs
    mkdir(name, mode)
OSError: [Errno 13] Permission denied: '/home/andy/.config/compiz'

```

il problema è con i permessi di ~/.config/compiz. È stato infatti impostato root come proprietario di una cartella nella propria area. Per cambiare i permessi, si lanci (da root)

```
chown <username> /home/<username>/.config/compiz

```

## Animazioni instabili, nonostante tutto sia stato configurato correttamente

Se ogni cosa è stata configurata correttamente ma si ottengono ancora performance di basso livello su alcuni effetti, si provi a disabilitare CCSM->General Options->Display Settings->"Detect Refresh Rate" e invece si scelga un valore manualmente. Testato sia su chip nvidia che intel. Può fare miracoli.

Altrimenti, se il proprio chip è nvidia e si nota una frequenza di aggiornamento inadeguata con abilitato in Compiz la "Detect Refresh Rate", il problema è probabilmente dovuto a un'opzione chiamata DynamicTwinView abilitata di base che gioca un ruolo nel riportare correttamente la massima frequenza d'aggiornamento supportata dalla propria scheda video. È possibile disabilitare DynamicTwinView aggiungendo la seguente linea alla sezione "Device" o "Screen" del proprio file xorg.conf, e riavviando il computer:

```
Option "DynamicTwinView" "False"

```

In questo modo si permetterà a XrandR di comunicare accuratamente la frequenza di aggiornamento a qualsiasi cosa la richieda, compreso Compiz. Dovrebbe essere possibile lasciar abilitato "Detect Refresh Rate" ed ottenere performance eccellenti. Un'altra volta ancora, questa soluzione si applica solamente ai chip nvidia.

## Risolvere gli screenshot in Gnome

Per riabilitare gnome-screenshot (il comportamento di base lo si ottiene premendo `PrtScn`) semplicemente si vada in Gestore impostazioni>Comandi e associare 'gnome-screenshot' al tasto 'PrtScn'. Questa soluzione è vantaggiosa perché così è possibile utilizzare contemporaneamente anche il plugin di Compiz-Fusion 'Screenshot' dal momento che l'azione che lo abilita è <Super>Button1 così da offrire due modi per catturare la schemata (uno dei quali fornisce una cattura a schermo intero con una sola battuta).

## Far funzionare con Compiz-Fusion il GNOME Workspace Switcher

Nelle vecchie versioni di Compiz, l'applet del Gnome Workspace Switcher funzionava correttamente con Compiz-Fusion (ad esemio con la rotazione del cubo/movimento ad aeroplano, ecc.), ma con le versioni recenti sembra non funzioni più. Ciò è dovuto ad una nuova caratteristica di Compiz, che permette di separare realmente gli spazi di lavoro. Ad esempio, nel caso si abbia un effetto desktop plane a quattro piani, e si hanno quattro desktop abilitati in Gnome, lui li riassume ad un totale di 16 differenti spazi di lavoro. Al momento, non c'è nessuna animazione collegata con il cambiamento "reale" degli spazi di lavoro. Per far funzionare il cambio degli spazi di lavoro, si seguino le istruzioni seguenti:

In GConf, impostare le seguenti opzioni:

```
/apps/compiz/general/screen0/options/number_of_desktops = **1**
/apps/compiz/general/screen0/options/hsize = 4 (this is an example)
/apps/compiz/general/screen0/options/vsize = 1 (this is an example)

```

## Lo schermo lampeggia con scheda video NVIDIA

Per risolvere, si crei il file /etc/modprobe.d/nvidia.conf e aggiungere la seguente linea:

```
options nvidia NVreg_RegistryDwords="PerfLevelSrc=0x2222"

```

## Risolvere il tema del cursore di base in Gnome 2.30

Si crei o modifichi /usr/share/icons/default/index.theme per tutti gli utenti, o per il singolo user **(non-root)** ~/.icons/default/index.theme, e si aggiungano le seguenti righe:

```
[Icon Theme]
#Name=_foo_
Name=_foo_
#Inherits=_foo_
Inherits=_foo_
[Desktop Entry]
Name[en_US]=index.theme

```

"Foo" è il nome del tema del cursore.

## Artefatti dello schermo in Firefox / Thunderbird

**Nota:** Sebbene questo problema non è strettamente legato a Compiz, è stato aggiunto qui perché secondo una leggenda potrebbe esserne Compiz stesso la causa.

Alcuni utenti hanno notato uno strano comportamento con i driver Catalyst AMD/ATI dalla versione 10.6\. Gli artefatti sono visibili sopratutto nelle applicazioni di Mozilla, dove le GUI presentano macchie nere di grandezza variabile. Ciò è dovuto ad una differente tecnica d'accelerazione 2D introdotta con i Catalyst 10.6. Questo problema può essere risolto seguendo i passi di risoluzione dei problemi nella pagina degli [ATI Catalyst](/index.php/ATI_Catalyst#Black.2Fgrey.2Fwhite_boxes.2Fartifacts_mainly_in_firefox.2Fthunderbird "ATI Catalyst")

## Impostare di nuovo Metacity come gestore di finestre dopo la disinstallazione

Dopo aver rimosso compiz tramite pacman, non viene reimpostato come gestore di finestre metacity. Ciò può portare alla mancanza dei bordi delle finestre, all'impossibilità di minimizzare, e ad una impossibilità a cambiare il fuoco. Per ripristinarlo, lanciare il comando "gconf-editor" nel terminale (occorre installarlo nel caso non lo si avesse già fatto). Si usi questo strumento per impostare il valore della chiave /desktop/gnome/session/required_components/window_manager da "compiz" a "metacity". Si effettui il log out e si rientri in modo tale che i cambiamenti abbiano effetto.

## Wallpaper del desktop e xorg-server 1.9

Al momento il plugin wallpaper di compiz-fusion non funziona correttamente con xorg-server 1.9\. Per risolvere il problema si veda [questa](https://bbs.archlinux.org/viewtopic.php?id=105281) pagina del forum.

## Il menu contestuale in alcune applicazioni (firefox, ...?) scompare quando il mouse ci passa sopra

Provare a disabilitare "focus stealing prevention" (opzioni generali).

## Note esterne

[Pagina risoluzione dei problemi](http://wiki.compiz.org/Troubleshooting) su compiz.org