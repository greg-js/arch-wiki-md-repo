## import

Una manera fácil de tomar una captura de pantalla de su sistema actual utiliza el comando Import:

```
$ import -window root screenshot.jpg

```

`import` es parte del paquete [imagemagick](https://www.archlinux.org/packages/?name=imagemagick).

En caso de que usted sólo desea tomar una sola ventana, puede utilizar la herramienta `xwininfo` para encontrar ID de la ventana. Sólo tiene que ejecutar el siguiente comando y haga clic en la ventana que desee tomar una captura de pantalla.

```
$ import -window `xwininfo | grep 'Window id:' | cut -d" " -f4` screenshot.jpg

```

Si ejecuta TwinView o DualHead, simplemente tome la captura de pantalla dos veces y use`imagemagick` para pegarlos juntos:

```
$ import -window root -display :0.0 -screen /tmp/0.png
$ import -window root -display :0.1 -screen /tmp/1.png
$ convert +append /tmp/0.png /tmp/1.png screenshot.png
$ rm /tmp/{0,1}.png

```

### Captura de la ventana de trabajo

El Siguiente script toma una captura de la ventana actual de trabajo. El script se usara la fecha actual como nombre de la captura, para evitar sobre escribir capturas anteriores.

```
 #!/bin/bash
 activeWinLine=$(xprop -root | grep "_NET_ACTIVE_WINDOW(WINDOW)")
 activeWinId="${activeWinLine:40}"
 import -window $activeWinId /tmp/`date +%F_%H%M%S_%N`.jpg

```

## Scrot

[scrot](https://www.archlinux.org/packages/?name=scrot), esta disponible en el repositorios de `[extra]`, permite tomar capturas de pantalla de la CLI, y ofrece características tales como definir retardo de tiempo. A menos que se indique lo contrario, se guarda el archivo en el directorio de trabajo actual.

```
 $ scrot-t 20-d 5

```

El comando anterior guarda archivo`.png` como nombre la fecha actual, y en miniatura (20% del original), para las publicaciones en la web. Proporciona un retardo de cinco segundos antes de la captura, en este caso.

Vea la pagina del manual de `scrot` para mas informacion

```
$ man scrot

```