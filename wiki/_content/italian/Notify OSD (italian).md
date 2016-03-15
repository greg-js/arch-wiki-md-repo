**Notify OSD** (Notify **O**n **S**creen **D**isplay) è un sistema di notifiche creato per Ubuntu dalla Canonical e più precisamente dai Team Design e Desktop Experience. Prevede la notifica degli eventi di maggior interesse per l'utente sotto forma di avvisi a schermo migliorati rispetto alle vecchie notifiche standard fornite con GNOME sotto un profilo di usabilità e di bellezza grafica.

## Contents

*   [1 Installazione](#Installazione)
    *   [1.1 GNOME](#GNOME)
        *   [1.1.1 Sfarfallamento delle notifiche con Compiz attivo](#Sfarfallamento_delle_notifiche_con_Compiz_attivo)
    *   [1.2 XFCE](#XFCE)
*   [2 Links](#Links)

# Installazione

[Notify-OSD](https://aur.archlinux.org/packages.php?ID=25256) è presente in [AUR](/index.php/AUR "AUR") questo indirizzo]. Per installarlo sarà dunque necessario utilizzare uno dei metodi per installare un programma a partire da un PKGBUILD di [AUR](/index.php/AUR "AUR"), come ad esempio makepkg o yaourt. Oltre a questo pacchetto che fornisce il sistema di notifiche vero e proprio, su [AUR](/index.php/AUR "AUR") si possono trovare vari programmi patchati per funzionare con queste notifiche.

## GNOME

Sotto GNOME, Notify-OSD andrà a sostituire l'originale **notification-daemon**. Prima di procedere alla sua installazione sarà dunque necessario eliminare questo pacchetto tramite il comando

```
# pacman -Rd notification-daemon

```

**Attenzione:** Con GNOME 2.30, i passi seguenti non sono più necessari. Le patch sono state infatti integrate in GNOME stesso. Basta solo aver installato notify-osd e avrete le notifiche stile Ubuntu.

Per avere tutti le notifiche presenti su Ubuntu - come le notifiche relative a variazione del livello del volume, della luminosità, o del collegamento/rimozione di dispositivi usb - sarà necessario installare vari pacchetti patchati, contenenti vari componenti di GNOME patchati per il funzionamento con queste notifiche. Questi pacchetti andranno a sostituire quelli originali, i quali andranno preventivamente rimossi tramite il sistema descritto in precedenza

```
# pacman -Rd gnome-power-manager gnome-settings-daemon gnome-mount

```

I pacchetti patchati sono:

*   [gnome-power-manager-notify-osd](https://aur.archlinux.org/packages/gnome-power-manager-notify-osd/)
*   [gnome-settings-daemon-notify-osd](https://aur.archlinux.org/packages/gnome-settings-daemon-notify-osd/)
*   [gnome-mount-notify-osd](https://aur.archlinux.org/packages/gnome-mount-notify-osd/)

Una volta riavviato GNOME dovreste avere il nuovo sistema di notifiche funzionante.

### Sfarfallamento delle notifiche con Compiz attivo

Nel caso utilizziate Compiz, è possibile notare un effetto sfarfallamento alla fine dell'effetto di dissolvenza della notifica. Per evitare ciò, è necessario che Compiz non applichi le animazioni alla categoria "notifications". Per ottenere questo, procedere come segue:

1.  aprire **CompizConfig Settings Manager (CCSM)**
2.  Aprire le impostazioni della plugin **Animations**
3.  Noterete le stringhe di configurazione, e in particolare una stringa simile a *(type=Menu | PopupMenu | notifications | DropdownMenu)*. E' sufficiente rimuovere **notifications** dalla stringa. Ricordate di effettuare l'operazione sia per la tab **Open Animation** che per la tab **Close Animation**.

## XFCE

XFCE viene installato con un proprio sistema di notifiche, **Xfce-notifyd**. Il pacchetto è incompatibile con Notify-OSD e pertanto va rimosso, ovviamente senza le sue dipendenze.

```
# pacman -Rd xfce4-notifyd

```

A questo punto è necessario installare una versione di Notify-OSD che sia stata modificata in modo tale da far riferimento non a gconf, quanto, piuttosto a xfconf, il demone che si occupa della configurazione di Xfce. Troverete su [AUR](/index.php/AUR "AUR") il pacchetto che fa per voi, cioè il pacchetto [notify-osd-xfconf-bzr](https://aur.archlinux.org/packages/notify-osd-xfconf-bzr/)

Attualmente l'integrazione tra XFCE e Notify-OSD è ancora incompleta ed installare i pacchetti di GNOME, cui si faceva riferimento sopra non servirà a nulla. Per far si che Notify-OSD notifichi le modifiche al livello del volume audio è possibile installare, sempre tramite [AUR](/index.php/AUR "AUR"), il pacchetto [xfce4-volumed](https://aur.archlinux.org/packages/xfce4-volumed/).

# Links

Sito di riferimento: [https://wiki.ubuntu.com/NotifyOSD](https://wiki.ubuntu.com/NotifyOSD)