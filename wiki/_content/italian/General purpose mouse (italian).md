Articoli correlati

*   [Daemon (Italiano)](/index.php/Daemon_(Italiano) "Daemon (Italiano)")

GPM, abbreviativo di General Purpose Mouse, è un demone che fornisce supporto al mouse per le console virtuali Linux. È incluso nella maggior parte delle distribuzioni Linux.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installazione](#Installazione)
    *   [1.1 Desktop](#Desktop)
    *   [1.2 Laptop](#Laptop)
*   [2 Configurazione](#Configurazione)

## Installazione

### Desktop

Installare [gpm](https://www.archlinux.org/packages/?name=gpm) con [pacman](/index.php/Pacman "Pacman"):

```
# pacman -S gpm

```

### Laptop

Installare [gpm](https://www.archlinux.org/packages/?name=gpm) e [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) con [pacman](/index.php/Pacman "Pacman"):

```
# pacman -S gpm xf86-input-synaptics

```

## Configurazione

Il parametro `-m` precede la dichiarazione del mouse da utilizzare. Il parametro `-t` precede il tipo di mouse. Per avere un elenco dei tipi disponibili per l'opzione `-t`, eseguire gpm con `-t help`.

```
$ gpm -m /dev/input/mice -t help

```

Se il mouse ha solo 2 tasti, passare il parametro `-2` a `GPM_ARGS` e il secondo tasto sarà abilitato alla funzione "incolla".

Il pacchetto [gpm](https://www.archlinux.org/packages/?name=gpm) deve essere avviato con alcuni parametri. Questi parametri possono essere impostati nel file `/etc/conf.d/gpm`, o usati per eseguire gpm direttamente.

*   For PS/2 mice, replace the existing line with:

```
GPM_ARGS="-m /dev/psaux -t ps2"

```

*   Whereas USB mice should use:

```
GPM_ARGS="-m /dev/input/mice -t imps2"

```

*   And IBM Trackpoints need:

```
GPM_ARGS="-m /dev/input/mice -t ps2"

```

Una volta trovata la configurazione adeguata, aggiungere `gpm` nella stringa `DAEMONS` in `/etc/rc.conf` per avere `gpm` avviato al boot. Esempio:

```
DAEMONS=(syslog-ng **gpm** network netfs crond)

```

Per maggiori informazioni [gpm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gpm.8).