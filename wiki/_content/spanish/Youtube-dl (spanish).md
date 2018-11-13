**Estado de la traducción**
Este artículo es una traducción de [Youtube-dl](/index.php/Youtube-dl "Youtube-dl"), revisada por última vez el **2018-10-05**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Youtube-dl&diff=0&oldid=545853) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [mpv](/index.php/Mpv "Mpv")
*   [FFmpeg](/index.php/FFmpeg "FFmpeg")

[youtube-dl](https://youtube-dl.org/) es un programa de línea de comandos que le permite descargar fácilmente videos y audio de más de mil sitios web. Consulte la [lista de sitios compatibles](https://github.com/rg3/youtube-dl/blob/master/docs/supportedsites.md).

## Contents

*   [1 Instalación](#Instalación)
*   [2 Utilización](#Utilización)
    *   [2.1 Selección de formato](#Selección_de_formato)
    *   [2.2 Extraer audio](#Extraer_audio)
*   [3 Configuración](#Configuración)
*   [4 Consejos y trucos](#Consejos_y_trucos)
    *   [4.1 Aumento de las velocidades de descarga](#Aumento_de_las_velocidades_de_descarga)
    *   [4.2 Recortar (descarga parcial)](#Recortar_(descarga_parcial))
    *   [4.3 URL del portapapeles](#URL_del_portapapeles)
*   [5 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [youtube-dl](https://www.archlinux.org/packages/?name=youtube-dl), o [youtube-dl-git](https://aur.archlinux.org/packages/youtube-dl-git/) para la versión de desarrollo.

## Utilización

Ver [youtube-dl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/youtube-dl.1).

```
$ youtube-dl [OPTIONS] *URL*

```

**Sugerencia:** En algunos casos (como YouTube) la *URL* puede sustituirse por el *ID* del video.

### Selección de formato

En los casos en que haya múltiples formatos de video disponibles, youtube-dl usará por defecto la descarga de la mejor versión posible. Si desea elegir un formato específico para descargar, primero obtenga una lista de los formatos disponibles:

```
$ youtube-dl -F *URL*

```

Anote el código de formato para la versión que desea y luego ejecute:

```
$ youtube-dl -f *format* *URL*

```

A menudo puede descargar formatos de solo audio o solo de video de esta manera. Si tiene [FFmpeg](/index.php/FFmpeg "FFmpeg"), puede descargar un formato solo de video y solo de audio y mezclarlos en un solo archivo:

```
$ youtube-dl -f *video_format*+*audio_format* *URL*

```

### Extraer audio

Utilice `-x` para descargar solo el audio(requiere [FFmpeg](/index.php/FFmpeg "FFmpeg")).

```
$ youtube-dl -x -f bestaudio *URL*

```

**Sugerencia:** Puede crear un [alias](/index.php/Alias_(Espa%C3%B1ol) "Alias (Español)") que busca la URL desde el portapapeles con [xclip](/index.php/Xclip_(Espa%C3%B1ol) "Xclip (Español)") usando `"$(xclip -o)"`.

## Configuración

El archivo de configuración de todo el sistema es `/etc/youtube-dl.conf` y el archivo de configuración específico del usuario es `~/.config/youtube-dl/config`. La sintaxis es simplemente una opción de línea de comando por línea. Ejemplo de configuración:

 `~/.config/youtube-dl/config` 
```
# Guardar en ~/Videos
-o ~/Videos/%(title)s.%(ext)s

# Prefiere resoluciones de 1080p o más bajas
-f (bestvideo[height<=1080]/bestvideo)+bestaudio/best[height<=1080]/best
```

Ver [[1]](https://github.com/rg3/youtube-dl/blob/master/README.md#configuration) Para más información.

## Consejos y trucos

### Aumento de las velocidades de descarga

Algunos sitios web aceleran las velocidades de descarga. A menudo puede aumentar la velocidad usando [Aria2](/index.php/Aria2 "Aria2"), un descargador externo que admite descargas de conexión múltiple. Ejemplo:

```
$ youtube-dl --external-downloader aria2c --external-downloader-args '-c -x 5 -k 2M' *URL*

```

### Recortar (descarga parcial)

Partes de [DASH](https://en.wikipedia.org/wiki/Dynamic_Adaptive_Streaming_over_HTTP "wikipedia:Dynamic Adaptive Streaming over HTTP") se pueden descargar usando la salida de `youtube-dl -g -f format URL` *como entrada* ffmpeg *con las opciones `-ss`, `-t` y `-c copy` [opciones](http://ffmpeg.org/ffmpeg.html#Main-options).*

### URL del portapapeles

Se puede configurar un alias de shell o un método abreviado de teclado para descargar un video (o audio) de una URL seleccionada (o copiada) emitiéndolo desde la [X selection](https://en.wikipedia.org/wiki/X_Window_selection "wikipedia:X Window selection"). Véase [herramientas de portapapeles](/index.php/Clipboard_(Espa%C3%B1ol)#Herramientas "Clipboard (Español)").

## Véase también

*   [repositorio GitHub](https://github.com/rg3/youtube-dl) para documentación.