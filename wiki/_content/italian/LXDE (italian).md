From [LXDE.org | Lightweight X11 Desktop Environment](http://lxde.org/):

	*Il 'Lightweight X11 Desktop Environment' è un ambiente desktop estremamente veloce , performante e con un buon risparmio energetico. Gestito da una comunità internazionale di sviluppatori, si presenta con una bella interfaccia, supporto multi-lingua, tasti di scelta rapida standard e funzionalità aggiuntive come la navigazione a schede dei file. LXDE utilizza meno CPU e RAM di altri ambienti desktop. E 'progettato appositamente per i computer cloud con basse specifiche hardware, come i netbook, i dispositivi MID (Mobile ad esempio) o computer datati.*

## Contents

*   [1 Installazione](#Installazione)
*   [2 Avviare LXDE](#Avviare_LXDE)
    *   [2.1 Display Manager](#Display_Manager)
    *   [2.2 Console](#Console)
*   [3 Suggerimenti](#Suggerimenti)
    *   [3.1 Configurazione menu applicazioni](#Configurazione_menu_applicazioni)
    *   [3.2 Auto Mount](#Auto_Mount)
    *   [3.3 Avvio automatico dei programmi](#Avvio_automatico_dei_programmi)
    *   [3.4 Cursori](#Cursori)
        *   [3.4.1 Icone delle cartelle personalizzate nella $HOME](#Icone_delle_cartelle_personalizzate_nella_.24HOME)
    *   [3.5 Impostazioni applet orologio digitale](#Impostazioni_applet_orologio_digitale)
    *   [3.6 Impostazioni dei caratteri](#Impostazioni_dei_caratteri)
    *   [3.7 Layout della tastiera](#Layout_della_tastiera)
        *   [3.7.1 Aggiungere il "modificatore del layout della tastiera" alla task-bar (barra dei processi)](#Aggiungere_il_.22modificatore_del_layout_della_tastiera.22_alla_task-bar_.28barra_dei_processi.29)
    *   [3.8 Gnome-screensaver in LXDE](#Gnome-screensaver_in_LXDE)
    *   [3.9 Icone di lxpanel](#Icone_di_lxpanel)
    *   [3.10 LXDM](#LXDM)
        *   [3.10.1 Autologin](#Autologin)
    *   [3.11 LXNM](#LXNM)
    *   [3.12 PCManFM](#PCManFM)
    *   [3.13 Cambiare Window Manager](#Cambiare_Window_Manager)
    *   [3.14 Spegnimento e Riavvio con LXDE](#Spegnimento_e_Riavvio_con_LXDE)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 NTFS e caratteri Cinesi](#NTFS_e_caratteri_Cinesi)
    *   [4.2 Problemi GTK+ con l'aggiornamento alla versione 0.4.1 di lxsession](#Problemi_GTK.2B_con_l.27aggiornamento_alla_versione_0.4.1_di_lxsession)
    *   [4.3 LXsession completo](#LXsession_completo)
    *   [4.4 Usare applicazioni KDEmod3 sotto LXDE](#Usare_applicazioni_KDEmod3_sotto_LXDE)
*   [5 Risorse esterne](#Risorse_esterne)

## Installazione

LXDE è particolarmente modulare, in modo da poter scegliere i pacchetti di cui si ha maggiormente bisogno. I pacchetti minimi da installare obbligatoriamente sono [lxde-common](https://www.archlinux.org/packages/?name=lxde-common), [lxsession](https://www.archlinux.org/packages/?name=lxsession), [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils), ed un gestore di finestre:

Si può installare il gruppo LXDE con:

```
# pacman -S lxde

```

Questo comando installerà i seguenti pacchetti:

*   [gpicview](https://www.archlinux.org/packages/?name=gpicview): Un leggero visualizzatore di immagini
*   [lxappearance](https://www.archlinux.org/packages/?name=lxappearance): Uno strumento per configurare temi, icone e font per applicazioni GTK +
*   [lxde-common](https://www.archlinux.org/packages/?name=lxde-common): Le impostazioni predefinite per l'integrazione dei diversi componenti di LXDE
*   [lxde-icon-theme](https://www.archlinux.org/packages/?name=lxde-icon-theme): Un tema di icone per LXDE
*   [lxlauncher](https://www.archlinux.org/packages/?name=lxlauncher): Un lanciatore pensato principalmente per i netbook
*   [lxmenu-data](https://www.archlinux.org/packages/?name=lxmenu-data): Una raccolta di file pensati per adeguare le specifiche di menu a freedesktop.org
*   [lxpanel](https://www.archlinux.org/packages/?name=lxpanel): Un pannello per il desktop per LXDE
*   [lxrandr](https://www.archlinux.org/packages/?name=lxrandr): Un gestore per lo schermo
*   [lxtask](https://www.archlinux.org/packages/?name=lxtask): Un leggero task manager
*   [lxterminal](https://www.archlinux.org/packages/?name=lxterminal): Un leggero emulatore di terminale
*   [menu-cache](https://www.archlinux.org/packages/?name=menu-cache): Un demone che genera automaticamente il menu di LXDE
*   [openbox](https://www.archlinux.org/packages/?name=openbox): Un window manager standard leggero e altamente configurabile, solitamente utilizzato in ambiente LXDE
*   [pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm): Il leggero file manager predefinito di LXDE, che prevede anche l'integrazione col desktop

Al termine dell'installazione, sarà necessario copiare i tre file elencati da pacman (menu.xml, rc.xml e autostart, reperibili in /etc/xdg/openbox) in ~/.config/openbox, eventualmente con il seguente comando:

```
# cp /etc/xdg/openbox/menu.xml /etc/xdg/openbox/rc.xml /etc/xdg/openbox/autostart ~/.config/openbox

```

Sarà inoltre necessario installare [Gamin](/index.php/Gamin "Gamin"), un sistema di monitoraggio di file e directory, pensato come un sottoinsieme di FAM. Viene invocato dai programmi stessi, non avendo così bisogno, al contrario di FAM, di un demone specifico in esecuzione in background. Se FAM è già stato installato, è necessario rimuoverlo dalla sezione DAEMONS in /etc/rc.conf, fermare il demone ed installare e poi installare gamin:

```
# pacman -S gamin

```

Alcune [applicazioni leggere](/index.php/List_of_applications_(Italiano) "List of applications (Italiano)") che si potrebbero voler installare sono:

```
# pacman -S leafpad xarchiver obconf epdfview

```

Si noti che alcuni pacchetti per LXDE sono sperimentali e sarà necessario installarli da [AUR](/index.php/AUR "AUR").

## Avviare LXDE

### Display Manager

Si si utilizza un display manager come [SLiM](/index.php/SLiM "SLiM") o [GDM](/index.php/GDM "GDM"), lo si configuri per avviare una sessione di LXDE. Per ulteriori informazioni fare riferimento alla pagina wiki del proprio display manaqger.

### Console

Per poter avviare una sessione desktop da console, vi sono varie alternative.

Per usare **startx** bisognerà impostare LXDE nel file `~/.xinitrc`:

```
exec startlxde

```

Per avviare LXDE da linea di comando senza `~/.xinitrc`:

```
$ xinit /usr/bin/startlxde

```

(questo metodo non funzionerà se è già presente il file `~/.xinitrc`)

Se si vuole eseguire **startx** automaticamente al boot, riferirsi alla guida [Avviare X al boot](/index.php/Start_X_at_login#Starting_X_as_preferred_user_without_logging_in "Start X at login").

Per le altre attività si accerti che dbus sia in esecuzione come demone.

## Suggerimenti

### Configurazione menu applicazioni

Il menù delle applicazioni funziona tramite la risoluzione dei file `.desktop` situati in `/usr/share/applications`. Molti ambienti desktop eseguono programmi che ignorano queste configurazioni per consentire le personalizzazioni del menu. LXDE deve ancora sviluppare un'applicazione per la gestione del menu, ma si può comunque intervenire manualmente per la sua creazione, se lo si desidera.

Per aggiungere un programma al menu (o modificarne una voce), creare un link al file `.desktop` in `~/.local/share/applications`, o crearne uno nuovo. Consultare [Specifiche per i desktop entry](http://standards.freedesktop.org/desktop-entry-spec/latest/) su freedesktop.org per informazioni sulla struttura di un file `.desktop` .

Per rimuovere voci dal menu, invece di eliminare il file `.desktop`, è possibile modificarlo, aggiungendo la seguente linea :

```
NoDisplay=true.

```

Per velocizzare quest'operazione per un certo numero di file si può creare un ciclo. Per esempio:

```
cd /usr/share/applications
for i in program1.desktop program2.desktop ...; do cp /usr/share/applications/$i \
/home/user/.local/share/applications/; echo "NoDisplay=true" >> \
/home/user/.local/share/applications/$i; done

```

Questo funzionerà con tutte le applicazioni eccetto quelle di KDE. Per queste ultime l'unico modo di rimuoverle dal menu è effettuare l'accesso in KDE ed usare il suo gestore di menu. Per ogni voce che non si vuole visualizzare nel menù, spuntare l'opzione "mostrare solo su KDE".

### Auto Mount

[PCManFM#Volume_handling](/index.php/PCManFM#Volume_handling "PCManFM")

### Avvio automatico dei programmi

	.desktop files

Per prima cosa, è possibile creare un link al file `.desktop` dell'applicazione contenuto in `/usr/share/applications` in `~/.config/autostart/`. Ad esempio per eseguire lxterminal in automatico all'avvio:

```
$ ln -s /usr/share/applications/lxterminal.desktop ~/.config/autostart/

```

Una volta che i file `.desktop` sono stati aggiunti è possibile manipolarli con lo strumento grafico di configurazione [lxsession-edit](https://aur.archlinux.org/packages/lxsession-edit/).

	autostart file

Il secondo metodo è usare il file `~/.config/lxsession/LXDE/autostart`. Questo file non è uno script della shell, ma ogni riga rappresenta un comando da eseguire. Se la linea inizia con @, il comando che segue verrà automaticamente rieseguito in caso di crash. Ad esempio per eseguire lxterminal e leafpad automaticamente all'avvio:

 `~/.config/lxsession/LXDE/autostart` 
```
@lxterminal
@leafpad

```

**Note:** I comandi **non** devono terminare con il simbolo **&**.

Vi è anche un file file globale per l'avvio automatico : `/etc/xdg/lxsession/LXDE/autostart`. Se sono presenti entrambi verranno eseguite tutte le voci di entrambi i file.

### Cursori

L'ultima versione del pacchetto[lxappearance2-git](https://aur.archlinux.org/packages/lxappearance2-git/) presente in [AUR](/index.php/AUR "AUR") include la funzionalità di poter cambiare il tema del cursore. Se non si desidera installare il nuovo e sperimentale lxappearance2, allora si dovrà definire il tema di cursori da utilizzare nel file `~/.Xdefaults` . Vedere [Configurare i temi del cursore](/index.php/X11_Cursors_(Italiano)#Configurare_il_tema_del_cursore "X11 Cursors (Italiano)").

Una maniera diretta per farlo è aggiungere il cursore ai temi predefiniti. Per prima cosa occorrerà creare la cartella:

```
# mkdir /usr/share/icons/default

```

Poi si potrà specificare di aggiungere ai temi delle icone il cursore. Così si metterà in uso il tema cursore [xcursor-bluecurve](https://www.archlinux.org/packages/?name=xcursor-bluecurve):

 `/usr/share/icons/default/index.theme` 
```
[icon theme]
Inherits=Bluecurve
```

#### Icone delle cartelle personalizzate nella $HOME

Attualmente sembra che PCManFM non supporti questa funzione: [https://bbs.archlinux.org/viewtopic.php?pid=851397#p851397](https://bbs.archlinux.org/viewtopic.php?pid=851397#p851397)

### Impostazioni applet orologio digitale

È possibile fare clic destro sulla applet dell'orologio digitale sul pannello e impostare la modalità di visualizzazione dell'ora corrente. Ad esempio, per visualizzare il tempo in modalità standard invece che militare nel formato HH: MM: SS:

```
%I:%M

```

E per il formato YYYY/MM/DD HH:MM:SS :

```
%Y/%m/%d %H:%M:%S

```

Per ulteriori opzioni consultare : `strftime (3)`

### Impostazioni dei caratteri

Molti utenti LXDE usano normalmente programmi GTK+ perchè GTK+ è usato come backend (i.e.: base) per LXDE. Per selezionare i caratteri, si può usare [lxappearance](https://www.archlinux.org/packages/?name=lxappearance) e scegliere il font principale, ma per impostazioni più avanzate sarà necessario usare "Preferenze caratteri" nel pannello di controllo Gnome . Per installarlo:

```
pacman -S gnome-control-center

```

Dopo aver impostato le proprie preferenze, si potrà anche disinstallare il programma, in quanto le preferenze impostate rimarranno memorizzate.

### Layout della tastiera

Modalità n.1:

Agginugere in /etc/xdg/lxsession/LXDE/autostart la seguente linea prima di @lxpanel --profile LXDE:

```
@setxkbmap -option grp:switch,grp:alt_shift_toggle,grp_led:scroll us,ru

```

o in ~/.config/lxsession/LXDE/autostart (per utenti a parte):

```
setxkbmap -option grp:switch,grp:alt_shift_toggle,grp_led:scroll us,ru

```

N.B.: "us" e "ru" stanno ovviamente in questo casa per i layout della tastiera statunitense e russo.

Modalità n.2:

Creare /etc/xdg/autostart/setxkmap.desktop come segue:

```
[Desktop Entry]
Version=1.0
Encoding=UTF-8
Name=Fix keyboard settings
Exec=setxkbmap -rules xorg -layout "us,ru" -variant ",winkeys" -option "grp:ctrl_shift_toggle"
Terminal=false
Type=Application

```

Modalità n.3:

Modificare ~/.Xkbmap per l'utente corrente o /etc/X11/Xkbmap per applicare invece modifiche globali di sistema. Aggiungere:

```
-option grp:ctrl_shift_toggle,grp_led:scroll us,ru

```

Modalità n.4:

Aggiungere la linea seguente in /etc/X11/xinit/xinitrc o ~/.xinitrc:

```
setxkbmap -option grp:ctrl_shift_toggle,grp_led:scroll us,ru

```

Modalità n.5:

Installare [fbxkb](http://fbxkb.sourceforge.net/) da [AUR](/index.php/AUR "AUR").

Modalità n.6:

[Xorg#Switching_Between_Keyboard_Layouts](/index.php/Xorg#Switching_Between_Keyboard_Layouts "Xorg")

#### Aggiungere il "modificatore del layout della tastiera" alla task-bar (barra dei processi)

1.  Clic destro sulla task-bar
2.  Scegliere "Aggiungi/Rimuovi oggetti del pannello"
3.  Scegliere "Aggiungi"
4.  Scegliere "modificatore del layout della tastiera" (i.e.: keyboard layout switcher).

### Gnome-screensaver in LXDE

Installare i pacchetti:

```
pacman -S gnome-screensaver gnome-session

```

Creare un semplice lanciatore per gnome-session per permettere allo screen-saver di funzionare in `~/.config/autostart/gnome-session.desktop`

```
[Desktop Entry]
Exec=/usr/bin/gnome-session

```

Eseguire il logout e poi loggarsi di nuovo in lxde per rendere effettivo il funzionamento di gnome-screensaver.

### Icone di lxpanel

Le icone utilizzate da lxpanle sono memorizzate di default in `/usr/share/pixmaps` e ogni icona che si vuole utilizzare in lxpanel va salvata in questo percorso.

È possibile cambiare le icone di default di un'applicazione seguendo i seguenti passi:

1.  Salvare la nuova icona in `/usr/share/pixmaps`
2.  Usare un editor di testi e aprire il file `.desktop` relativo al programma di cui vogliamo cambiare icona in `/usr/share/applications`.
3.  Modificare

```
Icon=/default/icon/.png 

```

con

```
Icon=/name/of/new/icon/added/to/pixmaps/.png

```

### LXDM

LXDE fornisce ora un gestore di diplasy sperimantale chiamato LXDM. É realizzato in GTK+ e [supporta i temi](http://blog.lxde.org/?p=595). Per installare LXDM:

```
# sudo pacman -S lxdm

```

Dopodichè cambiare la seguente riga di `/etc/inittab`:

```
x:5:respawn:/usr/sbin/lxdm >& /dev/null

```

#### Autologin

Modificare il proprio /etc/lxdm/lxdm.conf come segue:

```
[base]
autologin=username

```

### LXNM

**Note:** LXNM non è più in fase di sviluppo. Si [suggerisce](http://wiki.lxde.org/en/LXNM) l'uso di NetworkManager e nm-applet.

LXNM è un programma basato su alcuni script che si occupa delle gestione delle connessioni di rete, con l'obiettivo di rendere la loro configurazione il più automatizzata possibile, anche se non si tratta di un'applicazione così sviluppata come [NetworkManager](/index.php/NetworkManager "NetworkManager"). Se si desidera un magiore controllo, [Wicd](/index.php/Wicd "Wicd") e la versione di Gnome [NetworkManager](/index.php/NetworkManager "NetworkManager") si integrano perfettamente con LXDE. Si può installare LXNM dal repository [community] :

```
# pacman -S lxnm

```

Lo script principale deve essere eseguito da root. Se si pensa di utilizzarlo abitualmente, è preferibile aggiungerlo in `/etc/rc.conf`. LXNM lavora in parallelo con il Network Status Monitor di Lxpanel , quindi bisognerà aggiungerlo al pannello. LXNM funziona generalmente bene, malgrado talvolta possa tardare un po' nello stabilire una connessione.

### PCManFM

Wiki [PCManFM](/index.php/PCManFM_(Italiano) "PCManFM (Italiano)")

Se si vuole essere in grado di accedere al cestino, montare volumi e monitorare cartelle e file si dovrà aggiungere il supporto GVFS:

```
# pacman -S polkit-gnome gvfs

```

polkit-gnome fornisce un'autenticazione e dovrà essere avviato al login:

```
mkdir -p ~/.config/autostart
cp /etc/xdg/autostart/polkit-gnome-authentication-agent-1.desktop ~/.config/autostart

```

Attualmente il polkit-gnome-authentication-agent-1.desktop presente in Arch può non supportare alcuni desktop. Se si riscontrano problemi per avviarlo, rimuovere la riga:

```
OnlyShowIn=GNOME;XFCE;

```

[PCManFM @ LXDE wiki](http://wiki.lxde.org/en/PCManFM_build_and_setup_guide#Setup_Runtime_Environment_Correctly)

### Cambiare Window Manager

[OpenBox](/index.php/Openbox_(Italiano) "Openbox (Italiano)"), il window manager di default di LXDE, può essere sostituito in maniera semplice da altri, come fvwm, icewm, dwm, etc..

LXDE tenterà di utilizzare il windows manager specificato dal file di configurazione utente lxsession `~/.config/lxsession/LXDE/desktop.conf`. Se questo non esiste, allora tenterà di utilizzare quanto specificato nel file di configurazione globale `/etc/xdg/lxsession/LXDE/desktop.conf`.

Sostituire il comando `openbox-lxde` con quello del windows manager da voi scelto:

```
 [Session]
 window_manager=openbox-lxde

```

Per metacity:

```
window_manager=metacity

```

Per compiz:

```
window_manager=compiz ccp --indirect-rendering

```

### Spegnimento e Riavvio con LXDE

Per poter eseguire lo spegnimento, il riavvio e la sospensione da lxde è necessario che DBus e HAL siano attivi. Poi aggiungere l'utente al gruppo power.

```
# gpasswd -a <USERNAME> power

```

Assicurarsi di avere il proprio file `~/.xinitrc` configurato come mostrato nella sezione [Avviare LXDE](#Avviare_LXDE) e di avere il supporto HAL:

```
exec startlxde

```

## Troubleshooting

### NTFS e caratteri Cinesi

Se si vuole utilizzare un disco removibile con un filesystem NTFS, deve essere installato [NTFS-3G](/index.php/NTFS_Write_Support "NTFS Write Support"). In genere, PCManFM gestisce senza problemi i filesystem NTFS, tuttavia esiste un bug che affligge gli utenti NTFS, a causa del quale se si hanno file o cartelle su un filesystem NTFS aventi nomi con carattiri non-latin (p.e. caratteri cinesi), i suddetti file o cartelle potrebbero non essere visibili quando si apre (o si esegue l'automount del) volume NTFS. Questo accade perché il mount-helper dilxsession (o lxsession-lite) non interpreta correttamente le i meccanismi di utilizzo (i.e.: policies) e le opzioni locali. Una soluzione al problema è la seguente:

*   Rimuovere `/sbin/mount.ntfs-3g` (è un link simbolico).

```
 # rm /sbin/mount.ntfs-3g

```

*   Creare un nuovo `/sbin/mount.ntfs-3g` contenente il seguente script bash:

 `/sbin/mount.ntfs-3g` 
```
#!/bin/bash
 /bin/ntfs-3g $1 $2 -o locale=en_US.UTF-8
```

*   Dopodichè renderlo eseguibile:

```
 # chmod +x /sbin/mount.ntfs-3g 

```

*   Aggiungere quanto segue al file `/etc/pacman.conf` nella sezione "[options]", in modo da prevenire modifiche al file in caso di aggiornamento.

```
NoUpgrade = sbin/mount.ntfs-3

```

### Problemi GTK+ con l'aggiornamento alla versione 0.4.1 di lxsession

Quando avviando programmi GTK2 si ottiene:

```
 Il tema delle icone GTK+ non è correttemente configurato 

```

```
 Generalmente questo significa che non vi è un XSETTINGS manager in esecuziione. Ambienti desktop come GNOME o XFCE eseguono 
 automaticamente i loro gestori XSETTING, come gnome-settings-daemon o xfce-mcs-manager.

```

Questo è causato dallo spostamento dei file di configurazione di lxde-settings-daemon a lxsession. Personalizzazioni di questi file di configurazione richiedono l'unione dei file:

*   `/usr/share/lxde/config`
*   `~/.config/lxde/config`

in

*   `etc/xdg/lxsession/LXDE/desktop.conf`
*   `~/.config/lxsession/LXDE/desktop.conf`

In alternativa, è anche possibile usare lxappearance dai repository community per risolvere questo problema.

### LXsession completo

È noto che esistono alcuni bug in lxsession in relazione allla gestione delle sessioni. ***lxsession-lite*** è una versione di lxsession che non ha capacità di gestione delle sessioni. La stabilità di lxsession-lite è migliore di quella di lxsession, tuttavia non è in grado di salvare e ripristinare le sessioni. Quindi sarebbe raccomandabile adoperare ***lxsession-lite*** fino a che i problemi in lxsession non saranno risolti.

### Usare applicazioni KDEmod3 sotto LXDE

Poichè versioni più datate diKDEmod3[-legacy] vengono installate sotto `/opt/kde/bin`, queste non vengono riconosciute automaticamente dal LXDE. Per usarle, si può modificare la variabile d'ambiente PATH con il seguente comando:

```
# echo 'PATH=$PATH:/opt/kde/bin' >> /etc/rc.local

```

o aggiungere il seguente script a `/etc/profile.d/kde3path.sh`:

 `/etc/profile.d/kde3path.sh` 
```
#!/bin/sh
 PATH=$PATH:/opt/kde/bin
```

Dopodichè renderlo eseguibile:

```
# chmod a+x /etc/profile.d/kde3path.sh

```

## Risorse esterne

*   [voce wiki di LXDE riferite ad Arch Linux](http://wiki.lxde.org/en/ArchLinux)
*   [Progetto LXDE (Sourceforge)](http://lxde.sourceforge.net)
*   [LXDE Forum](http://forum.lxde.org)
*   [Gli utlimi pacchetti lx*](https://sourceforge.net/project/showfiles.php?group_id=180858)
*   [PCMan File Manager](https://sourceforge.net/project/showfiles.php?group_id=156956)