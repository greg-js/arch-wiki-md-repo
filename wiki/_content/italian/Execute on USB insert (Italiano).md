Supponendo di voler eseguire un certo programma all’inserimento di una pennina USB. Personalmente, ho aggiunto questa caratteristica perché mi ero stufato dei blocchi del pc dove tastiera e mouse sono inservibili(ed anche le scorciatoie da tastiera non funzionano).

Quindi ho aggiunto una misura di sicurezza, in modo che solo una chiavetta USB contenente la giusta chiave possa eseguire il programma.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurare una pennina USB](#Configurare_una_pennina_USB)
*   [3 Sicurezza](#Sicurezza)
*   [4 exdongle script](#exdongle_script)
*   [5 Note](#Note)

## Installazione

Mettere una copia dello [script `exdongle`](#exdongle_script) (che trovate più in basso) nella cartella degli eseguibili(uno dei percorsi indicati nella variabile d’ambiente `$PATH` comunemente è consigliato usare `/usr/bin/`).

Aggiungere la seguente linea alla [regola di mount delle periferiche USB](/index.php/Udev_(Italiano)#Mount_automatico_delle_periferiche_USB "Udev (Italiano)") (modificarla a seconda della propria configurazione):

```
ACTION=="add", RUN+="/usr/bin/exdongle run /media/%k-%E{dir_name}"

```

Eseguire l’opzione di configurazione, per esempio

```
exdongle conf -k "$RANDOM$RANDOM$RANDOM$RANDOM$RANDOM$RANDOM$RANDOM$RANDOM" -p "-10" -s "on"

```

Questo imposta la configurazione con chiavi casuali(solo con le chiavi giuste potranno essere eseguiti sul computer i programmi o gli script), e la priorità di esecuzione a -10

## Configurare una pennina USB

Per prima cosa, scrivere lo script che verrà inserito all’inserimento della pennina.

Ad esempio:

 `test.sh` 

```
#!/bin/sh

DISPLAY=:0 xterm

```

Adesso eseguire nuovamente `exdongle` utilizzando l'opzione `new`:

```
exdongle new <punto di mount della pennina USB> test.sh

```

Ora, ogni volta che viene inserita la pennina, una finestra di terminale, lanciata dall’utente root verrà eseguita sul display `:0`. Questo può essere utile per scopi amministrativi.

## Sicurezza

Questa procedura non garantisce la sicurezza del sistema, ed è quindi consigliato utilizzarla solo su pc domestici.

## exdongle script

 `/usr/bin/exdongle` 

```
#!/bin/sh

# exdongle mkexdongle

###############################################################################

CONFFILE="/etc/exdongle.conf"

###############################################################################

function usage() {

 echo ""
 echo "USAGE: $0 new <DIR> <PROG>"
 echo "       $0 del <DIR>"
 echo "       $0 conf [-k KEY] [-p PRIORITY] [-s SWITCH]"
 echo "       $0 run <DIR>"
 echo ""
 echo "  new:"
 echo "    DIR <S>:    The directory on the dongle to execute"
 echo "    SCRIPT <S>: The script to run on dongle"
 echo ""
 echo "  del:"
 echo "    DIR [S]: The directory on the dongle to execute"
 echo ""
 echo "  conf:"
 echo "    -k <S>: specify key"
 echo "    -p <N>: priority to run script at"
 echo "    -s <on|off>: Activate or deactivate exdongle"
 echo ""
 echo "  run:"
 echo "    DIR <S>: Directory to find script in"
 echo ""

 exit 0

}

###############################################################################

function new() {

 if [ ! "$#" -eq 3 ]; then
    usage $@;
    exit 1;
 fi

 DIR="$2"
 PROG="$3"
 PLOC="$DIR/.$(hostname).$key"

 rm "$PLOC" &> /dev/null
 cp "$PROG" "$PLOC"

 exit 0

}

###############################################################################

function del() {

 DIR="$2"
 PLOC="$DIR/.$(hostname).$key"

 if [ -e "$PLOC" ]; then
    rm -f "$PLOC"
 fi

 exit 0

}

###############################################################################

function conf() {

 shift
 while getopts "k:p:s:" optname; do
    case "$optname" in
     k)
       key="$OPTARG"
       ;;
     p)
       priority="$OPTARG"
       ;;
     s)
       if [ "$OPTARG" = "on" ] || [ "$OPTARG" = "off" ]; then
         switch="$OPTARG"
       fi
       ;;
    esac
 done

 echo "# exdongle configuration file" > "$CONFFILE"
 echo "key=\"$key\"" >> "$CONFFILE"
 echo "priority=\"$priority\"" >> "$CONFFILE"
 echo "switch=\"$switch\"" >> "$CONFFILE"

 chmod 0600 "$CONFFILE"

 exit 0

}

###############################################################################

function run() {

 if [ ! "$switch" = "on" ]; then
    exit 0
 fi

 if [ ! "$#" -eq 2 ]; then
    usage $@
    exit 1
 fi

 DIR="$2"
 PLOC="$DIR/.$(hostname).$key"
 ELOC="/tmp/.exdongle.prog"

 if [ ! -e "$PLOC" ]; then
    echo "No executable file found!" 1>&2
    exit 0
 fi

 rm -f "$ELOC"
 cp "$PLOC" "$ELOC"
 chmod 0500 "$ELOC"
 nice -n "$priority" $ELOC
 rm -f "$ELOC"
 exit 0

}

###############################################################################

if [ ! "$UID" == "0" ]; then
 echo "You must be root to perform this operation" 1>&2
 exit 1
fi

if [ -e "$CONFFILE" ]; then
 . "$CONFFILE"
fi

case "$1" in
 new)
    new "$@"
    ;;
 del)
    del "$@"
    ;;
 conf)
    conf "$@"
    ;;
 run)
    run "$@"
    ;;
 *)
    usage "$@"
    ;;
esac

exit 0

```

## Note

Alcune note:

*   I programmi/script usati dovrete fornirveli autonomamente, l’unico file che vi verrà fornito sarà lo script `exdongle`.