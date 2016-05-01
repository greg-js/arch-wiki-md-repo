XScreenSaver è uno screensaver e locker per il server X.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione di Xscreensaver](#Configurazione_di_Xscreensaver)
    *   [2.1 DPMS settings](#DPMS_settings)
*   [3 Avvio di Xscreensaver](#Avvio_di_Xscreensaver)
    *   [3.1 Sistemi con utente unico](#Sistemi_con_utente_unico)
    *   [3.2 Sistemi con più utenti](#Sistemi_con_pi.C3.B9_utenti)
*   [4 Blocca schermo](#Blocca_schermo)
*   [5 Disabilitare Xscreensaver per le applicazioni multimediali](#Disabilitare_Xscreensaver_per_le_applicazioni_multimediali)
    *   [5.1 mplayer](#mplayer)
    *   [5.2 XBMC](#XBMC)
    *   [5.3 Adobe Flash/MPlayer/VLC](#Adobe_Flash.2FMPlayer.2FVLC)
*   [6 Usare xscreensaver come wallpaper animato](#Usare_xscreensaver_come_wallpaper_animato)
    *   [6.1 Usare xscreensaver come wallpaper sotto xcompmgr](#Usare_xscreensaver_come_wallpaper_sotto_xcompmgr)
*   [7 Temi](#Temi)
*   [8 Cambio utente da "look screen"](#Cambio_utente_da_.22look_screen.22)
    *   [8.1 LXDM](#LXDM)
    *   [8.2 Lightdm](#Lightdm)
*   [9 Risorse esterne](#Risorse_esterne)

## Installazione

Il pacchetto [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver) è presente nei [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)"), quindi è facilmente con [Pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)").

In alternativa, esiste una versione patchata con il logo Archlinux su [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)") che si chiama [xscreensaver-arch-logo](https://aur.archlinux.org/packages/xscreensaver-arch-logo/). L'utilizzo di questo pacchetto al posto della versione del repository **extra** è vantaggioso per diversi motivi:

1.  Dal momento che makepkg compila da codice sorgente, il pacchetto risultante conterrà ottimizzazioni specifiche uniche per il *proprio* sistema, supponendo che si configuri il [makepkg.conf](/index.php/Makepkg_(Italiano) "Makepkg (Italiano)") con le apposite [CFLAGS](http://wiki.gentoo.org/wiki/Safe_CFLAGS) e CXXFLAGS.
2.  Questo pacchetto è marchiato Arch (screensaver, schermata di blocco, ecc.)
3.  Se si utilizza [Gnome](/index.php/GNOME_(Italiano) "GNOME (Italiano)"), questo pacchetto fornirà un'icona per accedere alle preferenze di xscreensaver da Sistema>Preferenze>Screensaver, a differenza del pacchetto del [repository ufficiale](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

## Configurazione di Xscreensaver

Le impostazioni globali si trovano in `/usr/share/X11/app-defaults/XScreenSaver`. Se si vuole usare una configurazione standard non è necessario toccare questo file. Inoltre molte impostazioni sono modificabili via gui per ogni utente semplicemente lanciando

```
$ xscreensaver-demo

```

### DPMS settings

XScreenSaver gestisce il risparmio energetico del display ([DPMS](/index.php/DPMS "DPMS")) independentemente da X, di cui ne sovrascrive i parametri. Per configurare il tempo di standby, spegnimento dello schermo e altro, usare `xscreensaver-demo` o editare il file `~/.xscreensaver`,

```
timeout:	1:00:00
cycle:		0:05:00
lock:		False
lockTimeout:	0:00:00
passwdTimeout:	0:00:30
fade:		True
unfade:		False
fadeSeconds:	0:00:03
fadeTicks:	20
dpmsEnabled:	True
dpmsStandby:	2:00:00
dpmsSuspend:	2:00:00
dpmsOff:	4:00:00

```

## Avvio di Xscreensaver

### Sistemi con utente unico

La sola [installazione](/index.php/Pacman_(Italiano) "Pacman (Italiano)") del pacchetto [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver) non è sufficiente a farlo avviare automaticamente. Il programma `xscreensaver` deve essere avviato, operazione eseguita in genere dall'ambiente desktop, su sistemi ad utente unico, tramite una riga in `~/.xinitrc` così:

```
/usr/bin/xscreensaver -no-splash &

```

La e commerciale `&` fa eseguire xscreensaver in background, ed è quindi necessaria.

**Note:** Xscreensaver viene avviato automaticamente da [Xfce](/index.php/Xfce_(Italiano) "Xfce (Italiano)") per mezzo di `/etc/xdg/xfce4/xinitrc`: assicurarsi che venga eseguito con `startxfce4` e non `xfce4-session`.
```
exec startxfce4

```

### Sistemi con più utenti

Se si opera su un sistema multi-utente con un [display manager](/index.php/Display_manager_(Italiano) "Display manager (Italiano)") (es. [SLiM](/index.php/SLiM_(Italiano) "SLiM (Italiano)"), [GDM](/index.php/GDM "GDM"), [KDM](/index.php/KDM_(Italiano) "KDM (Italiano)")) è meglio avviare xscreensaver tramite l'interfaccia di gestione screensaver nativa. Questo permette la gestione completa al cambio utenti. Per esempio, se si utilizza [Gnome](/index.php/GNOME_(Italiano) "GNOME (Italiano)"), e si installa [gnome-screensaver](https://www.archlinux.org/packages/?name=gnome-screensaver) e [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver), solo `gnome-screensaver` risulta attivo. Questo permette di poter selezionare tutti gli screensaver, e mantenere la funzionalità di "switch-user, in caso un utente abbia lo schermo bloccato, e un altro utente vuole "cambiare utente" accedendo alla casella.

**Note:** Alcune funzionalità native di xscreensaver andranno perdute, come il cattura schermo, l'utilizzo di foto in un percorso predefinito, e/o la visualizzazione di testi personalizzati durante l'esecuzione dello screensaver specifico del DM in uso con un sottoinsieme di funzionalità di xscreensaver (per esempio, schermo 3D Flip, photopile, ecc.)

Un'altra opzione per mantenere il supporto multi-utente, senza dover installare un secondo salvaschermo, è quello di modificare o `~/.xscreensaver`, cioè le impostazioni personali dell'utente, o `/usr/share/X11/app-defaults/XScreenSaver`, cioè le impostazioni per l'intero sistema. Aggiungere la seguente riga:

 `newLoginCommand: /usr/bin/gdmflexiserver` 
**Note:** Il comando è valido per gdm; per gestori di accesso differenti, sarà necessario modificare il comando con l'opzione adeguata corrispondente.

## Blocca schermo

Si può immediatamente attivare `xscreensaver`, se è in esecuzione, e bloccare lo schermo con il seguente comando

```
$ xscreensaver-command --lock

```

## Disabilitare Xscreensaver per le applicazioni multimediali

### mplayer

Aggiungere quanto segue a `~/.mplayer/config`

```
heartbeat-cmd="xscreensaver-command -deactivate >&- 2>&- &"

```

### XBMC

Non c'è supporto nativo all'interno di XBMC per disabilitare xscreensaver (tuttavia XBMC è fornito con un proprio screensaver). Un'applicazione di terze parti è disponibile su [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)"), ed è chiamata [caffeine-bzr](https://aur.archlinux.org/packages/caffeine-bzr/). Una volta in esecuzione, è sufficiente aggiungere `xbmc.bin` alla lista delle applicazioni per ottenerne l'attivazione automatica.

### Adobe Flash/MPlayer/VLC

Non esiste un metodo che nativamente impedisca l'avvio di xscreensaver per i filmati flash, ma è possibile usare uno script chiamato [lightsOn](https://github.com/iye/lightsOn) sviluppato per il flashplugin di Firefox, Chromium, MPlayer, e VLC.

## Usare xscreensaver come wallpaper animato

È possibile lanciare `xscreensaver` in background, come fosse un wallpaper. Prima di tutto sarà necessario killare ogni tipo di processo che stia controllando lo sfondo del desktop. Localizzare l'eseguibile di xscreensaver (generalmente `/usr/lib/xscreensaver/`) e lanciarlo con il flag `-root`. Un esempio:

```
$ /usr/lib/xscreensaver/glslideshow -root &

```

### Usare xscreensaver come wallpaper sotto xcompmgr

xcompmgr potrebbe causare dei problemi con xscreensaver. È necessario usare xwinwrap per lanciare il wallpaper. Il pacchetto in questione è [shantz-xwinwrap-bzr](https://aur.archlinux.org/packages/shantz-xwinwrap-bzr/) ed è presente in [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)").

Lanciare con in seguente comando:

```
$ xwinwrap -b -fs -sp -fs -nf -ov  -- /usr/lib/xscreensaver/glslideshow -root -window-id WID &

```

## Temi

La schermata di sblocco di XScreensaver può essere personalizzata con temi [X resources](/index.php/X_resources "X resources") (vedere: [Xscreensaver resources](/index.php/X_resources#Xscreensaver_resources "X resources")).

## Cambio utente da "look screen"

Di default, il bottone "New Login" di Xscreensaver nella schermata di sblocco richiama `/usr/bin/gdmflexiserver` a permettere tale operazione. Ciò funziona tuttavia solo con se si usa GDM. Altri display manager come lightdm e lxdm supportano questa funzionalità ma va configurata.

### LXDM

Incollare questa stringa in `~/.Xresources` per poter usare la funzionalità di cambio utente di LXDM:

```
*newLoginCommand: lxdm -c USER_SWITCH

```

### Lightdm

Incollare questa stringa in `~/.Xresource` per poter usare la funzionalità di cambio utente di lightdm:

```
*newLoginCommand: dm-tool switch-to-greeter

```

## Risorse esterne

[PanicLock](http://wiki.gotux.net/downloads/paniclock) -- Bloccare lo schermo e chiudere programmi determinati in background.