**Estado de la traducción**
Este artículo es una traducción de [Ktorrent](/index.php/Ktorrent "Ktorrent"), revisada por última vez el **2019-04-12**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Ktorrent&diff=0&oldid=570955) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Ktorrent](https://www.kde.org/applications/internet/ktorrent/) es un cliente de BitTorrent para KDE.

## Instalación

Instale el paquete [ktorrent](https://www.archlinux.org/packages/?name=ktorrent).

## Script para administrarlo en línea de órdenes

Dado que Ktorrent es una aplicación de solo GUI, afortunadamente tiene una interfaz DBUS, por lo que puede usar scripts para administrarlo en línea de órdenes (por ejemplo desde SSH).

Aquí está el script que uso. Lo encontré en internet en un foro de OpenSuse (creado por amaurea) e integré nuevas órdenes para establecer velocidad máxima de subida/descarga y para suspender/reanudar la actividad de ktorrent.

 `/usr/local/bin/kt` 
```
#!/usr/bin/env bash
#
# Public domain script by amaurea/amaur on IRC (freenode for example).
#   Modified by trapanator to support download/upload rate setting and
#                          to suspend/resume ktorrent network activity
#
# gary example
#   qdbus org.kde.ktorrent /core startAll

case $1 in
        help)
                echo "kt: A simple console interface for ktorrent.
Usage: In the following \"id\" indicates either a torrent hash or index.
       [] indicates optional arguments.

       kt start [id]: If ktorrent is not running, start it. Otherwise,
                      if id is given, start that torrent, otherwise start
                      all torrents.
       kt quit: Quit ktorrent.
       kt load url: Load the torrent given by url. Note that the torrent must
                    be manually startet afterwards.
       kt ls: Print a list of all torrents, of the format: index hash name.
       kt info [id]: Print more detailed info about the selected (or all)
                     torrent(s).
       kt stop [id]: Stop the torrent given by id, or all if id is missing.
       kt name [id]: Like ls, but names only.
       kt remove id: Remove the torrent given by id (but not the actual files).
       kt clear: Remove all torrents.
       kt files [id]: List information about the files of the selected torrent.
       kt pri [id] [priority]: Give the selected torrent the given priority.
       kt pri [id] [file index] [priority]: Set the priority of the given file.
       kt pri [id] equal: Give all files of the torrent the same priority.
       kt pri [id] first: Download the first files in the torrent first.
       kt stu [n] set upload rate to n.
       kt sdu [n] set download rate to n.
       kt suspend   suspend all torrents.
       kt resume    resume all torrents."
       exit ;;
esac
pid=$(pidof ktorrent)
if [ ! $pid ]; then
    case "$1" in
        start)
            ktorrent --display :0.0 ;;
        *)
            echo "ktorrent is not running!" ;;
    esac
    exit
fi
eval "export $(perl -pne 's/\0/
/g' /proc/$(pidof ktorrent)/environ | fgrep -a DBUS_SESSION_BUS_ADDRESS)"
loc="org.kde.ktorrent"
cmd="qdbus $loc"
case "$1" in
 stu)
  if [ "$2" ]; then
   qdbus org.kde.ktorrent /settings setMaxUploadRate $2
   qdbus org.kde.ktorrent /settings apply
  else echo "upload rate missing!" ;  fi ;;
 std)
  if [ "$2" ]; then
   qdbus org.kde.ktorrent /settings setMaxDownloadRate $2
   qdbus org.kde.ktorrent /settings apply
  else echo "download rate missing!" ;  fi ;;
 suspend)
  qdbus org.kde.ktorrent /core org.ktorrent.core.setSuspended true ;;
 resume)
  qdbus org.kde.ktorrent /core org.ktorrent.core.setSuspended false ;;
    load)
        res=$($cmd /core loadSilently "$2" 1) ;;
    list|ls)
        torrents=$($cmd /core torrents)
        i=0
        for torrent in $torrents; do
            name=$($cmd /torrent/$torrent name)
            printf "%d %s %s
" $i $torrent "$name"
            i=$(($i+1))
        done ;;
    info)
        if [ "$2" ]; then
            if (( ${#2} < 4 )); then
                torrents=($($cmd /core torrents))
                torrents=${torrents[$2]}
            else torrents=$2; fi
        else torrents=$($cmd /core torrents); fi
        i=0
        for torrent in $torrents; do
            name=$($cmd /torrent/$torrent name)
            size=$($cmd /torrent/$torrent totalSize)
            dsize=$($cmd /torrent/$torrent bytesToDownload)
            prog=$($cmd /torrent/$torrent bytesDownloaded)
            speed=$($cmd /torrent/$torrent downloadSpeed)
            seed=$($cmd /torrent/$torrent seedersConnected)
            leech=$($cmd /torrent/$torrent leechersConnected)
            priority=$($cmd /torrent/$torrent priority)
            sl=$(printf "[%d|%d]" $seed $leech)
            pri=$(printf "(%d)" $priority)
            printf "%3.0lf%% of %11d %4.0lf kb/s %8s %4s %s
" $((100*$prog/$dsize)) $dsize $(($speed/1000)) $sl $pri "$name"
            i=$(($i+1))
        done ;;
    name|stop|start|remove|files)
        if (( ${#2} < 4 )); then
            torrents=($($cmd /core torrents))
            torrent=${torrents[$2]}
        else torrent=$2; fi
        case "$1" in
            name)
                $cmd /torrent/$torrent name ;;
            start)
                if [ "$2" ]; then res=$($cmd /core start $torrent)
                else res=$($cmd /core startAll); fi;;
            stop)
                if [ "$2" ]; then res=$($cmd /core stop $torrent)
                else res=$($cmd /core stopAll); fi;;
            remove)
                # qdbus boolean bug workaround: use dbus-send instead
                res=$(dbus-send --type=method_call --dest=$loc /core org.ktorrent.core.remove string:"$torrent" boolean:false) ;;
            files)
                n=$($cmd /torrent/$torrent numFiles)
                for (( i=0; i < $n; i++ )); do
                    path=$($cmd /torrent/$torrent filePath $i)
                    pct=$($cmd /torrent/$torrent filePercentage $i)
                    size=$($cmd /torrent/$torrent fileSize $i)
                    priority=$($cmd /torrent/$torrent filePriority $i)
                    printf "%d %3.0lf%% of %11d [%d] %s
" $i $pct $size $priority "$path"
                done ;;
        esac ;;
    pri|priority|prioritize)
        if [ $3 ]; then
            if (( ${#2} < 4 )); then
                torrents=($($cmd /core torrents))
                torrent=${torrents[$2]}
            else torrent=$2; fi
            if [ ! $torrent ]; then exit; fi
            n=$($cmd /torrent/$torrent numFiles)
            if [ $4 ]; then
                res=$($cmd /torrent/$torrent setFilePriority $3 $4)
            else
                case $3 in
                    equal|equalize)
                        for (( i=0; i < $n; i++ )); do
                            res=$($cmd /torrent/$torrent setFilePriority $i 40)
                        done ;;
                    inc|increasing)
                        for (( i=0; i < $n; i++ )); do
                            pri=$(printf "%2.0lf" $(((4*$i/$n+3)*10)))
                            res=$($cmd /torrent/$torrent setFilePriority $i $pri)
                        done ;;
                    dec|decreasing)
                        for (( i=0; i < $n; i++ )); do
                            pri=$(printf "%2.0lf" $(((4*($n-$i-1)/$n+3)*10)))
                            res=$($cmd /torrent/$torrent setFilePriority $i $pri)
                        done ;;
                    first)
                        m=$(($n < 3 ? $n : 3))
                        for (( i=0; i < $m; i++ )); do
                            res=$($cmd /torrent/$torrent setFilePriority $i $(((6-$i)*10)))
                        done
                        for (( i=3; i < $n; i++ )) do
                            res=$($cmd /torrent/$torrent setFilePriority $i 30)
                        done ;;
                    *)
                        res=$($cmd /torrent/$torrent setPriority $3) ;;
                esac
            fi
        else echo Too few arguments!; fi ;;
    clear)
        torrents=$($cmd /core torrents)
        for torrent in $torrents; do
            res=$(dbus-send --type=method_call --dest=$loc /core org.ktorrent.core.remove string:"$torrent" boolean:false)
        done ;;
    quit)
        res=$($cmd /MainApplication quit) ;;
    *)
        echo "Unrecognized command: '$1'" ;;
esac

```