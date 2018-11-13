Il **MATE Desktop Environment** è un derivato di GNOME2 con lo scopo di creare un desktop attraente e intuitivo utilizzando modelli tradizionali e quindi adatti ad un utenza più vasta. Per maggior informazioni è consigliata la lettura di [questa discussione](https://bbs.archlinux.org/viewtopic.php?id=121162) sul forum inglese.

## Contents

*   [1 Preparazione](#Preparazione)
*   [2 Installazione](#Installazione)
*   [3 Lanciare Mate](#Lanciare_Mate)
    *   [3.1 Manualmente](#Manualmente)
    *   [3.2 Automaticamente all'avvio](#Automaticamente_all'avvio)
        *   [3.2.1 GDM (vecchio)](#GDM_(vecchio))
        *   [3.2.2 LXDM](#LXDM)
        *   [3.2.3 MATE Display Manager](#MATE_Display_Manager)
        *   [3.2.4 KDM (Italiano)](#KDM_(Italiano))
        *   [3.2.5 SLiM (Italiano)](#SLiM_(Italiano))
*   [4 Applicazioni](#Applicazioni)
    *   [4.1 Applicazioni Base](#Applicazioni_Base)
    *   [4.2 Applicazioni Extra](#Applicazioni_Extra)
*   [5 Usare Compiz Fusion sans Emerald](#Usare_Compiz_Fusion_sans_Emerald)
*   [6 Problemi Frequenti](#Problemi_Frequenti)
    *   [6.1 Generazione continua di richieste del gestore di file](#Generazione_continua_di_richieste_del_gestore_di_file)
    *   [6.2 Applicazioni QT](#Applicazioni_QT)
    *   [6.3 Evolution Email non funziona](#Evolution_Email_non_funziona)
    *   [6.4 Sticky Notes persi durante riavvio](#Sticky_Notes_persi_durante_riavvio)

## Preparazione

MATE è attualmente sviluppato [qui](https://github.com/Perberos/Mate-Desktop-Environment) ed è possibile installarlo tramite due mirror di pacman:

*   [http://packages.mate-desktop.org/repo/archlinux/](http://packages.mate-desktop.org/repo/archlinux/) — Pacchetti stabili numerati in base alla versione.
*   [http://packages.mate-desktop.org/repo/archlinux/development](http://packages.mate-desktop.org/repo/archlinux/development) — Pacchetti non stabili numerati in base alla data di pubblicazione

I pacchetti non ancora stabili sono disponibili anche su ([mate-desktop-environment](https://aur.archlinux.org/packages/mate-desktop-environment/)).

**Attenzione:** È disponibile nei repository una nuova serie di pacchetti del 10 Febbraio 2012 con una diversa numerazione basata sulla versione. Per un aggiornamento sicuro del sistema è necessario digitare da terminale:
```
# pacman -Syuu

```

Altrimenti Pacman vi avviserà della disponibilità di nuovi pacchetti locali più nuovi rispetto a quelli disponibili nei repository. I vecchi pacchetti sono ora considerati instabili e saranno aggiornati sporadicamente! Se si vogliono tenere è necessario modificare pacman.conf come segue:

```
[mate]
Server = http://packages.mate-desktop.org/repo/archlinux/development/$arch

```

## Installazione

Per installare la versione stabile di MATE tramite [pacman](/index.php/Pacman "Pacman") aggiungere le seguenti linee al vostro `/etc/pacman.conf`:

```
[mate]
Server = http://repo.mate-desktop.org/archlinux/$arch

```

Digitare

```
# pacman -Syy

```

e successivamente

```
# pacman -S mate

```

Per installare anche i pacchetti del gruppo **mate-extra** (molti sono i corrispettivi del gruppo [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/):

**Nota:** Attualmente, sono presenti due gruppi extra nel repository: **mate-extra** e **mate-extras**. È consigliato controllare il contenuto di entrambi per ottenere tutte le applicazioni desiderate finchè non verranno uniti in un unico pacchetto extra.

```
# pacman -S mate-extra

```

**oppure**

```
# pacman -S mate-extras

```

Probabilmente si riceveranno messaggi di conflitto durante l'installazione. Si rinominino i file in questione oppure si installi con l'opzione `--force`. È necessario [dbus](/index.php/Dbus "Dbus").

**Nota:** Attualmente, molti pacchetti di MATE non vanno in conflitto e non sostituiscono alcun pacchetto di GNOME.

## Lanciare Mate

Accertarsi di avere dbus tra i DAEMONS in rc.conf prima di lanciare MATE.

### Manualmente

Per lanciare Mate manualmente è necessario aggiungere

```
exec mate-session

```

al proprio `[~/.xinitrc](/index.php/Xinitrc "Xinitrc")` file e successivamente digitare

```
$ startx

```

### Automaticamente all'avvio

È consigliata la lettura di [Display manager (Italiano)](/index.php/Display_manager_(Italiano) "Display manager (Italiano)") e [Start X at Boot (Italiano)](/index.php/Start_X_at_Boot_(Italiano) "Start X at Boot (Italiano)") per maggiori dettagli.

#### GDM (vecchio)

Se si sta usando [gdm-old](https://aur.archlinux.org/packages/gdm-old/) da AUR, si scelga semplicemente la sessione MATE dalla Sessions list. La prima volta che si lancia MATE, accertarsi di cliccare "Just this session" quando indicato.

#### LXDM

È sufficiente selezionare MATE dalla Sessions list.

#### MATE Display Manager

Il MATE Display Manager (MDM) è il corrispetto di MATE del GNOME Display Manager (GDM). Il pacchetto 'mate-display-manager' è presente nel gruppo **mate-extra** oppure nel pacchetto AUR [mate-display-manager](https://aur.archlinux.org/packages/mate-display-manager/). Funzionava abbastanza bene, ma sfortunatamente il sottoprogetto è stato abbandonato e attualmente MDM non è più disponibile (01/07/2012).

#### [KDM (Italiano)](/index.php/KDM_(Italiano) "KDM (Italiano)")

Per lanciare MATE con [KDM (Italiano)](/index.php/KDM_(Italiano) "KDM (Italiano)"), il Display Manager di [KDE (Italiano)](/index.php/KDE_(Italiano) "KDE (Italiano)") , è necessario modicare la configurazione di KDM. Da root, modificare il file di configurazione `/usr/share/config/kdm/kdmrc` . Aggiungere `/usr/share/xsessions` alla lista del paramentro **SessionsDir**. Dovrebbe essere simile a questo:

```
SessionsDirs=/usr/share/config/kdm/sessions,/usr/share/apps/kdm/sessions,/usr/share/xsessions

```

riavvia KDM e seleziona MATE dalla lista.

#### [SLiM (Italiano)](/index.php/SLiM_(Italiano) "SLiM (Italiano)")

Si segua il tutorial di [SLiM (Italiano)](/index.php/SLiM_(Italiano) "SLiM (Italiano)") per installazione e modifica del file .xinitrc. Si aggiunga solo la seguente linea al file .xinitrc:

```
exec mate-session

```

## Applicazioni

### Applicazioni Base

È fondamentale notare che molte applicazioni di GNOME sono rinnovate per MATE, come i termini della licenza. Queste sono le applicazioni più importanti riprese da GNOME:

*   Nautilus rinominato **caja**
*   Metacity rinominato **marco**
*   Gconf rinominato **mate-conf**

Altre applicazioni e componenti fondamentali aventi GNOME come prefisso (GNOME panel,GNOME terminal..) hanno semplicemente il prefisso cambiato in MATE.

### Applicazioni Extra

Not tutte le applicazioni extra di GNOME sono disponibili per ora. Sono disponibili le seguenti: Not all of the GNOME extra applications (built for GTK2) have been forked yet. The following extra applications **are** available in MATE:

*   Totem (mate-video-player)
*   Eye of GNOME (mate-image-viewer)
*   Gedit (mate-text-editor)
*   File Roller (mate-file-archiver)
*   GNOME Panel applets (mate-applets)
*   GNOME Terminal (mate-terminal)

Se si usa NetworkManager per la connessione, è possibile installare [network-manager-applet-gtk2](https://aur.archlinux.org/packages/network-manager-applet-gtk2/) da AUR per nm-applet. È necessario modificare il PKGBUILD affinchè dipenda da mate-bluetooth al posto di gnome-bluetooth per evitare dipendenze recursive.

## Usare Compiz Fusion sans Emerald

Se si volesse usare Mate con [Compiz (Italiano)](/index.php/Compiz_(Italiano) "Compiz (Italiano)"), installare e lanciare Compiz Fusion normalmente,installare il pacchetto *gtk-window-decorator* e digitare il seguente comando per creare un symlink:

```
# ln -s /usr/lib/libmarco-private.so.0 /usr/lib/libmetacity-private.so.0

```

Abilitare il Window Decoration plugin nelle impostazioni di Compiz e usare

```
gtk-window-decorator --replace

```

come comando. Senza ricompilare gtk-window-decorator, le chiavi metaconf necessarie non saranno create e si rimarrà bloccati alle decorazioni di base Cairo. È possibile creare autonomamente le chiavi.

## Problemi Frequenti

### Generazione continua di richieste del gestore di file

È possibile trovare questo errore appena loggati, il file manager Caja continua a generare richeste senza fine. Una riparazione temporanea la si ottiene con il seguente comando:

```
# ln -s /usr/lib/libgnutls.so /usr/lib/libgnutls.so.26

```

Riloggarsi dopo aver digitato il comando.

Questo comando può risolvere anche il problema dell'orologio che non appare sul pannello.

### Applicazioni QT

Le applicazioni Qt4 potrebbero non ereditare il tema GTK2\. Questo problema si può sistemare facilmente installando [libgnomeui](https://aur.archlinux.org/packages/libgnomeui/) con l'opzione `--force`. Se il problema persiste, lancia qtconfig e assicurarsi che lo stile GUI selezionato sia GTK+.

### Evolution Email non funziona

si guardi [Evolution#Using Evolution Outside Of GNOME](/index.php/Evolution#Using_Evolution_Outside_Of_GNOME "Evolution").

### Sticky Notes persi durante riavvio

Dalla versione 1.1.0, l'applet Sticky Notes non salva le note create. Per risolvere il problema, digitare questi due comandi:

```
$ mkdir /home/username/.config/mate/
$ touch /home/username/.config/mate/stickynotes_applet

```

Per maggiori informazioni, consulate [questa discussione](http://forums.mate-desktop.org/viewtopic.php?f=7&t=15) sul forum ufficiale di MATE.