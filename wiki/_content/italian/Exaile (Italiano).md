## Contents

*   [1 Introduzione](#Introduzione)
*   [2 Installazione](#Installazione)
*   [3 Abilitare cover, testi e tabulati per chitarra](#Abilitare_cover.2C_testi_e_tabulati_per_chitarra)
*   [4 Riproduzione di CD audio](#Riproduzione_di_CD_audio)
*   [5 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [5.1 La barra temporale si blocca a 0:00](#La_barra_temporale_si_blocca_a_0:00)

# Introduzione

[Exaile](http://www.exaile.org/) è un riproduttore musicale scritto in python che sfrutta le librerie GTK+. Exaile è rilasciato sotto licenza [GPL](http://www.gnu.org/copyleft/gpl.html). Le caratteristiche principali includono:

*   Recupero di cover per album, testi, informazioni sulla traccia e l'artista (via Wikipedia), e tabulati per chitarra (via fretplay.com)
*   Playlist in schede
*   Supporto iPod
*   Support Last.fm
*   Navigazione nelle cartelle SHOUTcast
*   Esclusione tracce

# Installazione

Exaile è disponibile nel repository [community](/index.php/Official_repositories "Official repositories") di Archlinux. Per abilitare il repository community, è necessario decommentare in `/etc/pacman.conf`:

```
[community]
# Add your preferred servers here, they will be used first
 Include = /etc/pacman.d/community

```

Exaile può essere installato tramite [Pacman](/index.php/Pacman "Pacman"):

```
# pacman -S exaile

```

Se si utilizza [ALSA](/index.php/ALSA "ALSA") e si vuole usare alsasink come dispositivo di riproduzione, installare anche gstreamer0.10-base-plugins:

```
# pacman -S gstreamer0.10-base-plugins

```

Ciò potrebbe risolvere il problema se nessun suono viene riprodotto dopo l'installazione o quando si provano a riprodurre molti flussi audio contemporaneamente.

# Abilitare cover, testi e tabulati per chitarra

Mentre l'installazione di Exaile provvederà alla configurazione di tutti i pacchetti necessari alla corretta esecuzione, due pacchetti addizionali ([gnome-python-extras](https://www.archlinux.org/packages/search/?q=gnome-python-extras) e [libgtkhtml](https://www.archlinux.org/packages/search/?q=libgtkhtml)) devono essere installati separatamente, per attivare cover, testi, tabulati per chitarra e le informazioni da Wikipedia.

```
# pacman -S gnome-python-extras libgtkhtml

```

# Riproduzione di CD audio

Exaile richiede 'python-cddb' per riprodurre CD audio. Il pacchetto da installare (da [AUR](/index.php/AUR "AUR")) è [cddb-py](https://aur.archlinux.org/packages.php?do_Details=1&ID=3717&O=0&L=0&C=0&K=cddb&SB=n&SO=a&PP=25&do_MyPackages=0&do_Orphans=0&SeB=ndcddb-py/).

# Risoluzione dei problemi

### La barra temporale si blocca a 0:00

Prima di tutto, assicurarsi che non ci siano problemi con l'architettura audio utilizzata ([ALSA](/index.php/ALSA "ALSA"), [OSS](/index.php/OSS "OSS"), ecc...) e che l'opzione _playback sink_ in Exaile sia impostata correttamente. Provare ad impostarla su Automatica.

Se si sta ascoltando un file MP3, provare a riprodurre un formato differente, come un file .ogg o .flac. Se questi vengono riprodotti correttamente, è necessario installare gstreamer-ugly.

```
# pacman -S gstreamer0.10-ugly gstreamer0.10-ugly-plugins

```