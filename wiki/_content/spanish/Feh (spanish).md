Related articles

*   [Nitrogen (Español)](/index.php/Nitrogen_(Espa%C3%B1ol) "Nitrogen (Español)")
*   [sxiv](/index.php/Sxiv "Sxiv")

Feh es un potente y ligero visor de imágenes que también puede ser utilizado para gestionar el fondo de pantalla para aquellos gestores de ventanas que carecen de tal opción.

## Contents

*   [1 Instalación](#Instalación)
*   [2 Modo de uso](#Modo_de_uso)
    *   [2.1 Navegador de imágenes](#Navegador_de_imágenes)
    *   [2.2 Fondo de pantalla](#Fondo_de_pantalla)
    *   [2.3 Imágenes SVG](#Imágenes_SVG)
    *   [2.4 Fondo de pantalla aleatorio](#Fondo_de_pantalla_aleatorio)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [feh](https://www.archlinux.org/packages/?name=feh).

## Modo de uso

feh es altamente configurable. Para obtener una lista completa de opciones, ejecute `feh --help` o véase [feh(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/feh.1) [man page (Español)](/index.php/Man_page_(Espa%C3%B1ol) "Man page (Español)").

### Navegador de imágenes

Para visualizar rápidamente las imágenes contenidas en un directorio específico, puede lanzar feh con los siguientes argumentos:

```
$ feh -g 640x480 -d -S filename /ruta/al/archivo-de-imagen

```

*   La opción `-g` fuerza que las imagenes aparezcan con un tamaño no mayor de 640x480
*   La opción `-d` obtiene el nombre del archivo
*   La opción `-S filename` ordena las imágenes por nombre de archivo

Esto es tan sólo un ejemplo y hay muchas más opciones disponibles, si más flexibilidad es deseada.

**Sugerencia:** La opción `--start-at` mostrará la imagen seleccionada mientras se permite navegar las otras imágenes en el directorio, así cuando se ordena `feh --start-at ./foo.jpg .`, se verán todas las imágenes en el directoria actual empezando con `*foo*.jpg`.

### Fondo de pantalla

Se puede utilizar `feh` para que gestione el fondo de pantalla con aquellos [gestores de ventanas](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)") que carecen de características de escritorio, tales como [Openbox](/index.php/Openbox_(Espa%C3%B1ol) "Openbox (Español)") y [Fluxbox](/index.php/Fluxbox_(Espa%C3%B1ol) "Fluxbox (Español)").

El siguiente comando es un ejemplo de como establecer el fondo de pantalla inicial:

```
$ feh --bg-scale /ruta/al/archivo-de-imagen

```

Otras opciones de ajuste incluyen:

```
--bg-tile IMAGEN
--bg-center IMAGEN
--bg-max IMAGEN
--bg-fill IMAGEN

```

Para restaurar el fondo de pantalla en la siguiente sesión, añada lo siguiente a su archivo de arranque gráfico (p.ej. `~/.xinitrc`, `~/.config/openbox/autostart`, etc.):

```
~/.fehbg &

```

Para cambiar el el fondo de pantalla, edite el archivo `~/.fehbg`, que ha sido creado al ejecutar el comando `feh --bg-scale /ruta/al/archivo-de-imagen` mencionado anteriormente.

Es posible deshabilitar explícitamente la creación del archivo `~/.fehbg`, al pasar la opción `--no-fehbg`.

Para establecer diferentes imágenes para diferentes monitores, se deben pasar tantas imágenes como monitores disponibles. Así, el comando para dos monitores sería:

```
$ feh --bg-center /ruta/para/imagen-primer-monitor /ruta/para/imagen-segundo-monitor

```

### Imágenes SVG

 `$ feh --magick-timeout 1 archivo.svg` 

Nótese que este comando requiere el paquete [imagemagick](https://www.archlinux.org/packages/?name=imagemagick).

### Fondo de pantalla aleatorio

Es posible que `feh` seleccione un fondo de pantalla aleatoria mente pasando la opción `--randomize`, junto con una de las opciones `--bg-foo`. Por ejemplo:

 `$ feh --randomize --bg-fill ~/.fondosDePantalla/*` 

El comando anterior le ordena a `feh` que liste los archivos en el directorio `~/.fondosDePantalla/` de manera aleatoria. Escogiendo el fondo de pantalla de esta lista, una imagen por monitor.

Es posible hacer esto de manera recursiva, si se tienen imágenes en divididas en diferentes carpetas:

 `$ feh --recursive --randomize --bg-fill ~/.fondosDePantalla` 

Para mostrar un fondo de pantalla diferente al inicio de cada sesión, agregue lo siguiente a su archivo `.xinitrc`:

 `$ feh --bg-max --randomize ~/.fondosDePantalla/* &` 

Otra manera de seleccionar su fondo de pantalla de manera aleatoria el inicio de su sesión X.org, es editando `~/.fehbg`:

 `$HOME/.fehbg` 
```
 feh --bg-max --randomize --no-fehbg ~/.fondosDePantalla/* 

```

**Sugerencia:** Para cambiar fondos de panatalla periodicamente, use un script. Véase [while loop](https://mywiki.wooledge.org/BashGuide/TestsAndConditionals#Conditional_Loops_.28while.2C_until_and_for.29 "gregswiki:BashGuide/TestsAndConditionals"), [cron](/index.php/Cron "Cron"), o [systemd timer](/index.php/Systemd/Timers "Systemd/Timers") para ejecutar el comando en en intervalo deseado.