## Contents

*   [1 Xmame](#Xmame)
    *   [1.1 Introducción](#Introducci.C3.B3n)
    *   [1.2 Instalación y configuración](#Instalaci.C3.B3n_y_configuraci.C3.B3n)
    *   [1.3 Descargar las imágenes ROM](#Descargar_las_im.C3.A1genes_ROM)
    *   [1.4 Iniciar la emulación](#Iniciar_la_emulaci.C3.B3n)

## Xmame

### Introducción

[Xmame](http://x.mame.net)es un emulador para Linux de las máquinas "arcade". Junto con los ROM apropiados, Xmame se presenta con una serie de emuladores y más de 5000 juegos. desafortunadamente, la imágenes ROM individuales de los juegos están en una zona gris de la legalidad para los usuarios de PC. Queda advertido, si piensa descargar dichas imágenes ROM.

### Instalación y configuración

Descarge Xmame utilizando pacman:

```
#pacman -S xmame-sdl

```

Pase a ser un usuario sin privilegios con **su** y genere el archivo de configuración:

```
$xmame -showconfig > ~/.xmame/xmamerc

```

El archivo de configuración generado ya debería tener las entradas básicas para poder comenzar la emulación. Xmame utiliza una variable llamada **rompath'** para almacenar, con ":" como separador, los directorios donde encontrar las imágenes ROM. Para poner distintos tipos de roms en directorios específicos, sólo tiene que añadir el directorio a la línea **rompath**

### Descargar las imágenes ROM

*   Las imágenes ROMs están protegidas por las leyes de Propiedad Intelectual, así que es ilegal descargarlas. Si comprende esto, y quiere asumir el riesgo, siga las siguientes instrucciones para adaptarlas a xmame:

1.  Para imágenes ROM de emulador, ponga los archivos zip en **/usr/share/xmame/roms**.
2.  Para imágenes ROM de juegos, almacénelas en sus directorios específicos, o simplemente colóquelas en **/usr/share/xmame/roms**.

### Iniciar la emulación

Para jugar a **nombre de juego**, ejecute la siguiente orden desde el indicador de la línea de órdenes.

```
$xmame game.zip 

```

Pulse TAB para personalizar las teclas de control una vez iniciado el juego. Feliz emulación!