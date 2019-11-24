**Estado de la traducción**
Este artículo es una traducción de [ImageMagick](/index.php/ImageMagick "ImageMagick"), revisada por última vez el **2019-11-17**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=ImageMagick&diff=0&oldid=589220) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Según [Wikipedia](https://en.wikipedia.org/wiki/ImageMagick "wikipedia:ImageMagick"):

	ImageMagick es una suite de software gratuito y de código abierto para mostrar, convertir y editar archivos de [imágenes rasterizadas](https://en.wikipedia.org/wiki/es:Rasterizaci%C3%B3n "wikipedia:es:Rasterización") e [imágenes vectoriales](https://en.wikipedia.org/wiki/es:Gr%C3%A1fico_vectorial "wikipedia:es:Gráfico vectorial"). Puede leer y escribir más de 200 formatos de archivo de imagen.

**Nota:** [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) utiliza [Ghostscript](/index.php/Ghostscript "Ghostscript") para el análisis de PDF, EPS, PS y XPS. Debido a que ha habido múltiples vulnerabilidades con Ghostscript[[1]](https://security.archlinux.org/package/ghostscript), se compila sin la biblioteca Ghostscript. En su lugar, se recurre a la orden `gs` pero la misma está desactivada por defecto en `/etc/ImageMagick-7/policy.xml` con la siguiente línea:
```
<policy domain="delegate" rights="none" pattern="gs" />

```
Véase también [FS#59778](https://bugs.archlinux.org/task/59778), [FS#62171](https://bugs.archlinux.org/task/62171).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Utilización](#Utilización)
    *   [2.1 Captura de pantalla](#Captura_de_pantalla)
        *   [2.1.1 Captura de pantalla de múltiples pantallas X](#Captura_de_pantalla_de_múltiples_pantallas_X)
        *   [2.1.2 Captura de pantalla de encabezados individuales de Xinerama](#Captura_de_pantalla_de_encabezados_individuales_de_Xinerama)
        *   [2.1.3 Captura de pantalla de la ventana activa/enfocada](#Captura_de_pantalla_de_la_ventana_activa/enfocada)
*   [3 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [imagemagick](https://www.archlinux.org/packages/?name=imagemagick). Alternativamente, instale [graphicsmagick](https://www.archlinux.org/packages/?name=graphicsmagick) para [GraphicsMagick](https://en.wikipedia.org/wiki/es:GraphicsMagick "wikipedia:es:GraphicsMagick"), el cual es una derivación de [ImageMagick](https://en.wikipedia.org/wiki/es:ImageMagick "wikipedia:es:ImageMagick"), que enfatiza la estabilidad de la programación API y la interfaz de línea de órdenes.

## Utilización

Consulte [ImageMagick(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ImageMagick.1), o [gm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gm.1) para GraphicsMagick.

Las operaciones más populares incluyen `-append`, `-resize`, `-rotate`, `-quality` y algunas más. Por ejemplo, para combinar varias imágenes en una:

```
$ convert -append *input.pngs* *output.png*

```

**Nota:** el signo antes de una opción es importante. Las operaciones opuestas se pueden realizar utilizando un signo *más*, en lugar de un *menos*.

Para recortar parte de varias imágenes y convertirlas a otro formato:

```
$ mogrify -crop *ANCHO*x*ALTO*+*X*+*Y* -format jpg *.png

```

Donde *ANCHO* y *ALTO* es el tamaño de la imagen de salida recortada, y *X* e *Y* son los márgenes del tamaño de la imagen de entrada.

### Captura de pantalla

Una manera fácil de tomar una captura de pantalla de su sistema actual es utilizar la orden [import(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/import.1):

```
$ import -window root screenshot.jpg

```

`import` es parte del paquete [imagemagick](https://www.archlinux.org/packages/?name=imagemagick).

Ejecutar `import` sin la opción `-window` permite seleccionar una ventana o una región arbitraria de forma interactiva.

**Nota:** si prefiere la alternativa **graphicsmagick**, basta con anteponer «gm», por ejemplo, `$ gm import -window root screenshot.jpg`.

#### Captura de pantalla de múltiples pantallas X

Si ejecuta twinview o dualhead, simplemente tome la captura de pantalla dos veces y use `imagemagick` para pegarlas:

```
import -window root -display :0.0 -screen /tmp/0.png
import -window root -display :0.1 -screen /tmp/1.png
convert +append /tmp/0.png /tmp/1.png screenshot.png
rm /tmp/{0,1}.png

```

#### Captura de pantalla de encabezados individuales de Xinerama

Las configuraciones de múltiples encabezados basadas en Xinerama tienen solo una pantalla virtual. Si las pantallas físicas están en diferentes alturas, encontrará un espacio muerto en la captura de pantalla. En este caso, es posible que desee tomar una captura de pantalla de cada pantalla física individualmente. Mientras la información de Xinerama esté disponible desde el servidor X, funcionará lo siguiente:

```
#!/bin/sh
xdpyinfo -ext XINERAMA | sed '/^  head #/!d;s///' |
while IFS=' :x@,' read i w h x y; do
        import -window root -crop ${w}x$h+$x+$y head_$i.png
done

```

#### Captura de pantalla de la ventana activa/enfocada

El siguiente script toma una captura de pantalla de la ventana actualmente enfocada. Funciona con gestores de ventanas de X compatibles con EWMH/NetWM. Para evitar sobrescribir capturas de pantalla anteriores, la fecha actual se utiliza como nombre del archivo.

```
#!/bin/sh
activeWinLine=$(xprop -root | grep "_NET_ACTIVE_WINDOW(WINDOW)")
activeWinId=${activeWinLine:40}
import -window "$activeWinId" /tmp/$(date +%F_%H%M%S_%N).png

```

Alternativamente, lo siguiente debería funcionar independientemente del soporte EWMH:

```
$ import -window "$(xdotool getwindowfocus -f)" /tmp/$(date +%F_%H%M%S_%N).png

```

**Nota:** si las capturas de pantalla de algunos programas (dwb y zathura) aparecen en blanco, intente añadir `-frame` o eliminar `-f` de la orden `xdotool`.

## Véase también

*   [ImageMagick website](http://www.imagemagick.org/) para obtener una extensa lista de opciones y ejemplos.
*   [List of applications/Multimedia#Image processing](/index.php/List_of_applications/Multimedia#Image_processing "List of applications/Multimedia")