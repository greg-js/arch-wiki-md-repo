[Feh](https://derf.homelinux.org/~derf/projects/feh/) è un programma leggero e potente per visualizzare immagini che può essere anche utilizzato per la gestione degli sfondi del desktop in window manager standalone che non comprendono questa funzionalità.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Utilizzo](#Utilizzo)
    *   [2.1 Image Browser](#Image_Browser)
        *   [2.1.1 Lanciatore per il visualizzatore di immagini](#Lanciatore_per_il_visualizzatore_di_immagini)
    *   [2.2 Sfondo del Desktop](#Sfondo_del_Desktop)
*   [3 Tips](#Tips)
    *   [3.1 Immagine di sfondo casuale](#Immagine_di_sfondo_casuale)
        *   [3.1.1 Usare uno script](#Usare_uno_script)
            *   [3.1.1.1 Doppio schermo senza Xinerama](#Doppio_schermo_senza_Xinerama)
        *   [3.1.2 Usare cron](#Usare_cron)
        *   [3.1.3 Usare systemd/user](#Usare_systemd.2Fuser)
*   [4 See also](#See_also)

## Installazione

[feh](https://www.archlinux.org/packages/?name=feh) è disponibile nei [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

## Utilizzo

Feh è altamente configurabile, per una lista completa di opzioni eseguire `feh --help`.

### Image Browser

Per visualizzare velocemente le immagini in una specifica directory si può lanciare feh con le seguenti opzioni:

```
$ feh -g 640x480 -d -S filename /percorso/directory

```

*   L'opzione `-g 640x480` forza le immagini di apparire al massimo ad una risoluzione di 640x480
*   L'opzione `-d` stampa il nome del file
*   L'opzione `-S filename` fa si che le immagini siano ordinate per nome

Questo è solo un esempio, è possibile utilizzare molte altre opzioni se si desidera una maggiore flessibilità.

#### Lanciatore per il visualizzatore di immagini

Il seguente script, è molto utile per una visualizzazione più agevole delle immagini: visualizzerà con feh tutte le immagini selezionate tramite il file manager o tutte le immagini di una specifica directory nell'ordine di default. Questo script assume che il primo argomento sia il nome del file da aprire.

 `feh_browser.sh` 
```
#!/bin/bash

shopt -s nullglob

if [[ ! -f $1 ]]; then
        echo "$0: first argument is not a file" >&2
        exit 1
fi

file=$(basename -- "$1")
dir=$(dirname -- "$1")
arr=()
shift

cd -- "$dir"

for i in *; do
        [[ -f $i ]] || continue
        arr+=("$i")
        [[ $i == $file ]] && c=$((${#arr[@]} - 1))
done

exec feh "$@" -- "${arr[@]:c}" "${arr[@]:0:c}"

```

Lo script in questione va usato sul percorso delle immagini selezionate, seguito (volendo) da altre opzioni di feh. Un esempio di come lanciare lo script in un file manager è:

 ` $/percorso/dello/script/feh_browser.sh %f -F -Z` 

dove `-F` e `-Z` sono opzioni di feh:

*   `-F` apre l'immagine a schermo pieno
*   `-Z` setta in modo automatico lo zoom

Aggiungendo `-q` (quiet) non vengono mostrati nel terminale tutti gli errori di feh quando tenta di aprire file che non sono immagini presenti nella directory.

Una semplice, ma meno versatile, alternativa è:

 `feh_browser.sh` 
```
 #! /bin/sh
 feh -. "$(dirname "$1")" --start-at "$1"
```

Tale script non accetta opzioni passategli sulla riga di comando.

### Sfondo del Desktop

Feh può essere utilizzato per gestire lo sfondo del desktop in window manager che non hanno questa possibilità (ad esempio [Openbox](/index.php/Openbox_(Italiano) "Openbox (Italiano)") e [Fluxbox](/index.php/Fluxbox_(Italiano) "Fluxbox (Italiano)")).

Se si sta utilizzando [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)"), è fondamentale disabilitare il controllo che GNOME Files applica sul desktop. Il metodo più semplice e veloce è lanciando in un terminale:

```
$ gconftool-2 --set /apps/nautilus/preferences/show_desktop --type boolean false

```

Il seguente comando è invece un esempio di come impostare uno sfondo con feh:

```
$ feh --bg-scale /percorso/esatto/dello/sfondo.estensione

```

Altre opzioni possibili per lo scaling dell'immagine sono:

```
--bg-tile FILE
--bg-center FILE
--bg-max FILE
--bg-fill FILE

```

Per far si che alla prossima sessione di X lo sfondo venga ripristinato automaticamente, aggingere la seguente riga allo script di avvio (ad esempio: `~/.xinitrc`, `~/.config/openbox/autostart`, `~/.fluxbox/startup` ecc.):

```
sh ~/.fehbg &

```

Per cambiare l'immagine di sfondo sarà quindi sufficiente editare il file `~/.fehbg` creatosi automaticamente dopo aver lanciato il comando `feh --bg-scale /percorso/esatto/dello/sfondo.estensione`.

## Tips

### Immagine di sfondo casuale

#### Usare uno script

Per avere un wallpaper che varia casualmente fra quelli in una determinata directory è necessario creare uno script con il codice riportato qui sotto (ad esempio `wallpaper.sh`), renderlo eseguibile

```
$ chmod -x wallpaper.sh

```

e lanciarlo all'avvio (ad esempio da `~/.xinitrc`). Se non si vuole usare questo script in più al file di startup già presente nel sistema è possibile incollare il codice direttamente in `~/.xinitrc`.

Cambiare la directory `~/.wallpaper` con quella desiderata e i `15m` di pausa con un tempo a piacimento. Per maggiori informazioni consultare il man di sleep dando in un terminale `man sleep`.

 `wallpaper.sh` 
```
#!/bin/bash

while true; do
        find ~/.wallpaper -type f \( -name '*.jpg' -o -name '*.png' \) -print0 |
                shuf -n1 -z | xargs -0 feh --bg-scale
        sleep 15m
done

```

**Nota:** Potrebbe essere necessario trasformare *~/.wallpaper* in *~/.wallpaper***/**

Se questo script non dovesse funzionare, provare il seguente che non cerca ricorsivamente la directory `~/.wallpaper`:

 `wallpaper.sh` 
```
#!/bin/bash

shopt -s nullglob

cd ~/.wallpaper

while true; do
        files=()
        for i in *.jpg *.png; do
                [[ -f $i ]] && files+=("$i")
        done
        range=${#files[@]}

        ((range)) && feh --bg-scale "${files[RANDOM % range]}"

        sleep 15m
done

```

###### Doppio schermo senza Xinerama

Questo script rimpiazza la chiamata a "feh" per aggiungere uno sfondo su sistemi a doppio schermo (ad esempio nvidia twinview):

 `wallpaper.sh` 
```
#!/bin/sh
exec feh --bg-max --no-xinerama "$@"

```

#### Usare cron

Usare cron fa si che si possa avere un risultato molto simile e non ci sia uno script in costante sleep

Dare un `$ crontab -e` e aggiungere:

 ` * * * * *  DISPLAY=:0.0 feh --bg-max "$(find ~/.wallpaper/|shuf -n1)"` 

#### Usare systemd/user

**Nota:** Questo è utile '*solo* se si una *sessione systemd/user*. Vedere [Systemd/User](/index.php/Systemd/User_(Italiano) "Systemd/User (Italiano)") per maggiori dettagli.

Creare questa unità service:

 `$HOME/.config/systemd/user/feh-wallpaper.service` 
```
[Unit]
Description=Random wallpaper with feh

[Service]
Type=oneshot
EnvironmentFile=%h/.wallpaper
ExecStart=/bin/bash -c '/usr/bin/feh --bg-max "$(find ${WALLPATH}|shuf|head -n 1)"'

[Install]
WantedBy=default.target

```

Creare un file *timer*. Cambiare il tempo a piacimento. In questo esempio il tempo è `15 secondi`.

 `$HOME/.config/systemd/user/feh-wallpaper.timer` 
```
[Unit]
Description=Random wallpaper with feh

[Timer]
OnUnitActiveSec=*15s*
Unit=feh-wallpaper.service

[Install]
WantedBy=default.target

```

In questo esempio gli sfondi sono salvati in una directory nascosta nella propria $HOME:

 `$HOME/.wallpaper` 
```
WALLPATH=*/home/user/.wallpaper/*

```

Attivare `feh-wallpaper.timer` e `feh-wallpaper.service`. Leggere [Daemons](/index.php/Daemons "Daemons") per maggiori dettagli.

**Nota:** Ricordarsi che si sta usando una *systemd user session*, quindi è necessario usare il flag `--user` con `systemctl`.

## See also

*   [Forum post with original script for feh_browser](https://bbs.archlinux.org/viewtopic.php?pid=884635#p884635)