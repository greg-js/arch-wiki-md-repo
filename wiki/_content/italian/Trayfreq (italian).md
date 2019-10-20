<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Introduzione](#Introduzione)
    *   [1.1 Versione più recente](#Versione_più_recente)
    *   [1.2 Caratteristiche](#Caratteristiche)
*   [2 Installazione](#Installazione)
    *   [2.1 Configurazione di sistema](#Configurazione_di_sistema)
    *   [2.2 Configurazione di Trayfreq](#Configurazione_di_Trayfreq)
*   [3 Note](#Note)
*   [4 Link esterni](#Link_esterni)

## Introduzione

Trayfreq è un'applicazione GTK+ rilasciata sotto licenza GPL che permette di selezionare i profili di consumo della CPU o la sua frequenza attraverso un'icona dal pannello di sistema, e mostrare informazioni sulla batteria. Trayfreq è pensato per essere indipendente dal Desktop Environment, quindi dipende solo dalle librerie GTK+ e da un pannello di sistema nel quale essere eseguito. Trayfreq è il compagno perfetto per GNOME, Xfce, LXDE, o altri Window Manager (Openbox, Fluxbox, ecc).

### Versione più recente

0.2.x.dev1-3

### Caratteristiche

*   Mostra un'icona che riporta la relativa frequenza della CPU
*   Quando viene cliccata l'icona della CPU con il tasto destro, viene fornito un menu dal quale modificare profili e frequenze della CPU scelta
*   Quando viene cliccata l'icona della CPU con il tasto sinistro, viene eseguito un comando da impostare nel file di configurazione (di default, non viene eseguito nulla)
*   Mostra un'icona che riporta lo stato della batteria (In carica, In scarica, Carica) e la sua carica corrente (opzionale)
*   Gestione dei profili della CPU in base allo stato della batteria.
*   Leggero, indipendente dal Desktop Environment

## Installazione

Installare [trayfreq da AUR](https://aur.archlinux.org/packages.php?ID=26999). Si consiglia di usare uno degli [AUR helpers](/index.php/AUR_helpers "AUR helpers").

### Configurazione di sistema

Lo scaling della CPU richiede un kernel che implementi questa funzione o il caricamento dei moduli adatti in [rc.conf](/index.php/Rc.conf "Rc.conf"). Consultare [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") per maggiori instruzioni sul caricamento dei driver e governor di cpufreq.

### Configurazione di Trayfreq

A questo punto, si deve modificare il file di configurazione di trayfreq.

```
$ cp /usr/share/trayfreq/trayfreq.config ~/.trayfreq.config
$ nano ~/.trayfreq.config

```

Tutte le righe saranno commentate; decommentarle per utilizzare le funzioni proposte. Dando un'occhiata alle opzioni...

*   `[battery]` – il gruppo delle opzioni sull'icona Batteria
    *   `show=1` – impostare 1 per mostrare l'icona, 0 per nasconderla
    *   `governor=powersave` – imposta il profilo da utilizzare "in scarica"
*   `[ac]` – il gruppo in caso la batteria non stia scaricando
    *   `governor=ondemand` – imposta il profilo da utilizzare se la batteria non si scarica
*   `[events]` – il gruppo sugli Eventi
    *   `activate=/usr/bin/xterm` – imposta il comando da attivare quando l'icona viene premuta (con il tasto sinistro)
*   `[governor]` – il gruppo sui Profili
    *   `default=ondemand` – imposta il profilo da attivare quando Trayfreq è avviato
*   `[ac]` – il gruppo delle opzioni sull'alimentazione da rete
    *   `governor=ondemand` – imposta il profilo da utilizzare quando il terminale è alimentato dalla rete elettrica
*   `[frequency]` – il gruppo sulle Frequenze
    *   `default=800000` – imposta la frequenza (in Hertz) da attivare quando Trayfreq è avviato

**Nota:** Si noti che, se quest'ultima opzione è attiva, il profilo corrente viene ignorato.

File d'esempio:

```
[battery]
show=1
governor=powersave
[ac]
governor=ondemand
[events]
activate=/usr/bin/showbatt
[governor]
default=ondemand
#[frequency]
#default=800000

```

Se si desidera, un file di configurazione può essere inserito nella cartella home, ma questo gestisce Trayfreq solo se l'icona nel pannello è attiva. Il file dovrebbe chiamarsi `~/.trayfreq.config`; se esiste, Trayfreq non punterà a `/usr/share/trayfreq/trayfreq.config` per configurarsi.

## Note

Un file .desktop viene generato in `/etc/xdg/autostart/`. Partirà automaticamente una volta installato. Se non si vuole l'avvio automatico, basta aprire lo Startup Manager del Desktop Enviroment (come *Applicazioni d'avvio* in GNOME) e deselezionare Trayfreq.

## Link esterni

*   [Sito web di Trayfreq (in inglese)](http://trayfreq.sourceforge.net)