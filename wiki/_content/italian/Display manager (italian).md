Articoli correlati

*   [Desktop Environment (Italiano)](/index.php/Desktop_Environment_(Italiano) "Desktop Environment (Italiano)")
*   [Window Manager (Italiano)](/index.php/Window_Manager_(Italiano) "Window Manager (Italiano)")
*   [Start X at Login (Italiano)](/index.php/Start_X_at_Login_(Italiano) "Start X at Login (Italiano)")

Un [display manager](https://en.wikipedia.org/wiki/X_display_manager_(program_type) e [gestori di finestre](/index.php/Window_manager_(Italiano) "Window manager (Italiano)"). Solitamente è possibile, entro certi limiti, personalizzare il loro aspetto.

## Contents

*   [1 Lista dei display manager disponibili](#Lista_dei_display_manager_disponibili)
    *   [1.1 Testuali](#Testuali)
    *   [1.2 Grafici](#Grafici)
*   [2 Avviare il display manager](#Avviare_il_display_manager)
    *   [2.1 Utilizzo di systemd-logind](#Utilizzo_di_systemd-logind)
*   [3 Consigli utili](#Consigli_utili)
    *   [3.1 Elenco sessioni avviabili](#Elenco_sessioni_avviabili)
    *   [3.2 Avvio di applicazioni senza window manager](#Avvio_di_applicazioni_senza_window_manager)
    *   [3.3 Avvio automatico](#Avvio_automatico)
    *   [3.4 Impostazione della lingua](#Impostazione_della_lingua)
*   [4 Problemi noti](#Problemi_noti)
    *   [4.1 Incompatibilità con systemd](#Incompatibilità_con_systemd)

## Lista dei display manager disponibili

### Testuali

*   **[CDM](/index.php/CDM "CDM") (Console Display Manager)** — login manager minimale ma dalle molte funzioni, scritto in bash

	[https://github.com/ghost1227/cdm](https://github.com/ghost1227/cdm) || [cdm-git](https://aur.archlinux.org/packages/cdm-git/)

*   **[Console TDM](/index.php/Console_TDM "Console TDM")** — Estensione per xinit scritta completamente in bash

	[http://code.google.com/p/t-display-manager/](http://code.google.com/p/t-display-manager/) || [console-tdm](https://aur.archlinux.org/packages/console-tdm/)

*   **[nodm](/index.php/Nodm "Nodm")** — Display manager minimale per login automatici.

	[http://enricozini.org/sw/nodm/](http://enricozini.org/sw/nodm/) || [nodm](https://www.archlinux.org/packages/?name=nodm)

### Grafici

*   **[Entrance](/index.php/Enlightenment "Enlightenment")** — Un display manager basato sulle EFL, altamente sperimentale

	[http://enlightenment.org/](http://enlightenment.org/) || [entrance-git](https://aur.archlinux.org/packages/entrance-git/)

*   **[GDM](/index.php/GDM "GDM")** — [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)") Display Manager

	[http://projects.gnome.org/gdm/](http://projects.gnome.org/gdm/) || [gdm](https://www.archlinux.org/packages/?name=gdm)

*   **[KDM](/index.php/KDM_(Italiano) "KDM (Italiano)")** — [KDE](/index.php/KDE_(Italiano) "KDE (Italiano)") Display Manager

	[http://www.kde.org/](http://www.kde.org/) || [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/)

*   **[LightDM](/index.php/LightDM "LightDM")** — Light Display Manager è un display manager cross-desktop; può utilizzare frontend scritti con qualsiasi toolkit

	[http://www.freedesktop.org/wiki/Software/LightDM](http://www.freedesktop.org/wiki/Software/LightDM) || [lightdm](https://www.archlinux.org/packages/?name=lightdm), [lightdm-bzr](https://aur.archlinux.org/packages/lightdm-bzr/)

*   **[LXDM](/index.php/LXDM_(Italiano) "LXDM (Italiano)")** — [LXDE](/index.php/LXDE_(Italiano) "LXDE (Italiano)") Display Manager. Indipendente dall'ambiente desktop scelto

	[http://sourceforge.net/projects/lxdm/](http://sourceforge.net/projects/lxdm/) || [lxdm](https://www.archlinux.org/packages/?name=lxdm)

*   **MDM** — MDM Display Manager, usato in Linux Mint e fork di GDM 2

	[https://github.com/linuxmint/mdm](https://github.com/linuxmint/mdm) || [mdm-display-manager](https://aur.archlinux.org/packages/mdm-display-manager/)

*   **[Qingy](/index.php/Qingy "Qingy")** — login manager grafico molto leggero ed altamente configurabile, indipendente da X Windows (usa DirectFB)

	[http://quingy.sourceforge.net/](http://quingy.sourceforge.net/) || [qingy](https://aur.archlinux.org/packages/qingy/)

*   **[SDDM](/index.php/SDDM "SDDM")** — Display manager basato su QML e successore di KDM; si abbina a Plasma.

	[https://github.com/sddm/sddm](https://github.com/sddm/sddm) || [sddm](https://www.archlinux.org/packages/?name=sddm)

*   **[SLiM](/index.php/SLiM_(Italiano) "SLiM (Italiano)") (Simple Login Manager)** — leggera ed elegante soluzione per il login grafico

	[http://sourceforge.net/projects/slim.berlios/](http://sourceforge.net/projects/slim.berlios/) || [slim](https://www.archlinux.org/packages/?name=slim)

*   **[XDM](/index.php/XDM "XDM")** — X Display Manager con supporto a XDMCP e host chooser.

	[http://www.x.org/archive/X11R7.5/doc/man/man1/xdm.1.html](http://www.x.org/archive/X11R7.5/doc/man/man1/xdm.1.html) || [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)

## Avviare il display manager

Per abilitare il login grafico, si [attivi](/index.php/Systemd_(Italiano)#Usare_le_unità "Systemd (Italiano)") il relativo servizio di systemd. Ad esempio, per KDM, attivare `kdm.service`.

Il comando di cui sopra dovrebbe funzionare senza problemi. Se così non fosse, probabilmente si è creato il file `default.target` manualmente o come residuo di precedenti installazioni:

 `# ls -l /etc/systemd/system/default.target`  `/etc/systemd/system/default.target -> /usr/lib/systemd/system/graphical.target` 

Si elimini semplicemente il link simbolico e *systemd* utilizzerà il proprio `default.target` di default (nella fattispecie, `graphical.target`)

```
# rm /etc/systemd/system/default.target

```

Una volta effettuata l'abilitazione di kdm, dovrebbe essere presente un link simbolico nella cartella `/etc/systemd/system`

 `# ls -l /etc/systemd/system/display-manager.service`  `/etc/systemd/system/display-manager.service -> /usr/lib/systemd/system/kdm.service` 

### Utilizzo di systemd-logind

Per controllare lo stato della propria sessione utente è possibile utilizzare `loginctl`. Tutte le azioni di [polkit](/index.php/Polkit "Polkit") come la sospensione o il monitoraggio dei dispositivi removibili dovrebbero funzionare senza ulteriori interventi.

## Consigli utili

### Elenco sessioni avviabili

Molti display managers leggono l'elenco delle sessioni avviabili dalla directory `/usr/share/xsessions/`, che contiene dei file [desktop standard](http://standards.freedesktop.org/desktop-entry-spec/latest/) per ogni DE/WM.

Per aggiungere/rimuovere voci dall'elenco sessioni del vostro display manager, si creino/rimuovano i file `.desktop` in `/usr/share/xsessions/`.

Esempio:

```
[Desktop Entry]
Encoding=UTF-8
Name=Openbox
Comment=Log in using the Openbox window manager (without a session manager)
Exec=/usr/bin/openbox-session
TryExec=/usr/bin/openbox-session
Icon=openbox.png
Type=XSession

```

### Avvio di applicazioni senza window manager

È possibile avviare applicazioni senza decorazioni o gestori di finestre attivi. ad esempio, per lanciare [google-chrome](https://aur.archlinux.org/packages/google-chrome/), si crei un file `web-browser.desktop` nella directory `/usr/share/xsessions`, in questo modo:

 `/usr/share/xsessions/web-browser.desktop` 
```
[Desktop Entry]
Encoding=UTF-8
Name=Web Browser
Comment=Use a web browser as your session
Exec=/usr/bin/google-chrome --auto-launch-at-startup
TryExec=/usr/bin/google-chrome --auto-launch-at-startup
Icon=google-chrome

```

In questo caso, una volta effettuato il login, l'applicazione specificata dopo il parametro `Exec` verrà avviata immediatamente. Una volta chiusa l'applicazione, si verrà portati nuovamente al loginmanager (come accade quando si effettua il logout da un DE/WM classico).

È importante ricordare che la maggior parte delle applicazioni grafiche non sono state progettate per essere lanciate in questo modo e potrebbe essere necessario modificare manualmente alcune impostazioni o si potrebbe essere soggetti a limitazioni (ad esempio, se non si sta utilizzando alcun Window Manager, non sarà possibile spostare le finestre, incluse quelle di dialogo. In ogni caso potrebbe comunque essere possibile impostare la geometria della finestra nei file di configurazione dell'applicazione.

Si veda inoltre [xinitrc#Starting applications without a window manager](/index.php/Xinitrc#Starting_applications_without_a_window_manager "Xinitrc").

### Avvio automatico

La maggior parte dei display manager effettuano il source di `/etc/xprofile`, `~/.xprofile` e `/etc/X11/xinit/xinitrc.d/`. Per ulteriori dettagli consultare [xprofile](/index.php/Xprofile "Xprofile").

### Impostazione della lingua

Per i Display Manager che utilizzano [AccountsService](http://freedesktop.org/wiki/Software/AccountsService/), è possibile impostare il [locale](/index.php/Locale_(Italiano) "Locale (Italiano)") modificando `/var/lib/AccountsService/users/$USER`:

```
[User]
Language=*locale_scelto*

```

Dove *locale_scelto* è un valore come `it_IT.UTF-8"`.

Si riavvii il Display Manager in uso per rendere effettive le modifiche.

## Problemi noti

### Incompatibilità con systemd

*Display Manager colpiti: Entrance, MDM.*

Alcuni display manager non sono pienamente compatibili con systemd, dal momento che riutilizzano la sessione di PAM. Questo comportamento causa diversi problemi come:

*   L'applet di NetworkManager non funziona
*   Impossibilità di modificare il volume di PulseAudio
*   Impossibilità ad effettuare il login in GNOME con un altro utente