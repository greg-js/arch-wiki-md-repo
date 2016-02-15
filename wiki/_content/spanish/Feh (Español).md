## Contents

*   [1 Introducción](#Introducci.C3.B3n)
*   [2 Instalación](#Instalaci.C3.B3n)
*   [3 Modo de uso](#Modo_de_uso)
    *   [3.1 Navegador de imágenes](#Navegador_de_im.C3.A1genes)
    *   [3.2 Fondo de pantalla](#Fondo_de_pantalla)

# Introducción

Feh es un visor de imágenes potente y ligero que también puede ser utilizado para gestionar el fondo de pantalla para aquellos gestores de ventanas que carecen de tal característica.

# Instalación

```
# pacman -S feh

```

# Modo de uso

feh es altamente configurable. Para obtener una lista completa de opciones, ejecute **feh --help**.

## Navegador de imágenes

Para visualizar rápidamente las imágenes contenidas en un directorio específico, puede lanzar feh con los siguientes argumentos:

```
$ feh -g 640x480 -d -S filename /ruta/al/archivo-de-imagen

```

*   La opción -g fuerza que las imagenes aparezcan con un tamaño no mayor de 640x480
*   La opción -S filename ordena las imágenes por nombre de archivo

Esto es tan sólo un ejemplo y hay disponibles muchas más opciones, si deseara más flexibilidad.

## Fondo de pantalla

Se puede utilizar feh para que gestione el fondo de pantalla con aquellos gestores de ventanas que carecen de características de escritorio, tales como [Openbox](/index.php/Openbox "Openbox") y [Fluxbox](/index.php/Fluxbox "Fluxbox"). El siguiente comando es un ejemplo de como establecer el fondo de pantalla inicial:

```
$ feh --bg-scale /ruta/al/archivo-de-imagen

```

Otras opciones de ajuste incluyen:

```
--bg-tile IMAGEN
--bg-center IMAGEN
--bg-seamless IMAGEN

```

Para conservar el fondo de pantalla en la siguiente sessión, añada lo siguiente a su archivo de arranque gráfico (p.ej. ~/.xinitrc, ~/.config/openbox/autostart, etc.):

```
eval `cat ~/.fehbg` &

```