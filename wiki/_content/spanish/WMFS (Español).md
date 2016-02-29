**Advertencia:** WMFS se encuentra obsoleto y sin soporte, por lo que se recomienda usar [WMFS2](/index.php/WMFS2_(Espa%C3%B1ol) "WMFS2 (Español)")

## Contents

*   [1 Introducción](#Introducci.C3.B3n)
*   [2 Instalación](#Instalaci.C3.B3n)
*   [3 Configuración](#Configuraci.C3.B3n)
    *   [3.1 Archivo de Configuración](#Archivo_de_Configuraci.C3.B3n)
    *   [3.2 Tags & Reglas](#Tags_.26_Reglas)
    *   [3.3 Combinación de Teclas](#Combinaci.C3.B3n_de_Teclas)
        *   [3.3.1 Scratchpad](#Scratchpad)
    *   [3.4 Configuración de la Barra de Estado](#Configuraci.C3.B3n_de_la_Barra_de_Estado)
    *   [3.5 Conky](#Conky)
    *   [3.6 WMFS Status Toolkit](#WMFS_Status_Toolkit)
*   [4 Uso](#Uso)
*   [5 Recursos](#Recursos)

## Introducción

[WMFS](http://wmfs.info/) (Window Manager From Scratch) es un gestor de ventanas en mosaico, ligero y altamente configurable para las X's. Este puede ser configurado mediante un archivo de configuración de nombre `wmfsrc`, soporta fuentes Xft ([Freetype](http://www.freetype.org/)) y es compatible con las especificaciones ([EWMH](http://standards.freedesktop.org/wm-spec/wm-spec-1.3.html)). Todavía se encuentra en un proceso de desarrollo intenso

## Instalación

WMFS se encuentra en [AUR](/index.php/AUR "AUR"). Debido al elevado ritmo de desarrollo es recomendable usar la versión [git](https://aur.archlinux.org/packages.php?ID=26924).

Puede ser instalado con algún ayudante de AUR o mediante el PKGBUILD.

Instalando WMFS con ayuda de yaourt:

```
$ yaourt -S wmfs-git

```

WMFS buscará un archivo de configuración en `$XDG_CONFIG_HOME/wmfs`. Para configurar WMFS a su gusto, tendrá que editar el archivo de configuración; para la mayoría de los usuarios el archivo se encuentra en `~/.config/wmfs/wmfsrc`. Si el archivo `~/.config/wmfs` no existe, puede crearlo:

```
$ mkdir -p ~/.config/wmfs

```

El archivo de configuración de nombre wmfsrc, por defecto se encuentra en el directorio XDG en `/etc/xdg/wmfs`. Copie el archivo al recientemente creado directorio `~/.config/wmfs` para empezar a modificarlo.

```
$ cp /etc/xdg/wmfs/wmfsrc ~/.config/wmfs

```

Para usar WMFS como el gestor de ventanas por defecto, añadalo a su `.xinitrc`:

```
$ echo "exec wmfs" >> ~/.xinitrc

```

## Configuración

### Archivo de Configuración

El archivo de configuración esta bien comentado. Haga pequeños cambios acumulativos y recargue WMFS (las teclas por defecto para recargar el ambiente son (`Alt`+`Ctrl`+`r`)) para probar los cambios.

Por defecto son usados 2 diferentes Modkeys para usar las combinaciones de teclas(`Ctrl` y `Alt`) que pueden entrar en conflicto con su ya existente configuración. Estas se pueden cambiar en el archivo `wmfsrc`. Por ejemplo, si desea usar la tecla de “Windows” en ves de la tecla “Alt”, reemplacé “Alt” con “Super” o con “Mod4” en el archivo de configuración.

```
[key] mod = { "Super" } key = "p" func = "launcher" cmd = "launcher_exec" [/key]

```

O con un solo comando:

```
sed --in-place=.bak 's/"Alt"/"Mod4"/' wmfsrc

```

Para enlazar comandos con símbolos especiales necesita especificar su nombre, como "slash" por "/". Usted puede encontrar los nombres de los símbolos utilizando xev y escribiendo el símbolo en cuestión:

```
xev | grep keycode
   state 0x10, keycode 61 (keysym 0x2f, slash), same_screen YES,
   state 0x10, keycode 60 (keysym 0x2e, period), same_screen YES,
   state 0x10, keycode 59 (keysym 0x2c, comma), same_screen YES,

```

### Tags & Reglas

Asignar clientes a un tag, eje: Para tener [Uzbl](/index.php/Uzbl "Uzbl") abierto en el tag 2 se hacen mediante nuestro archivo `wmfsrc`, escribiendo una nueva regla en la sección [rules]:

```
[rule] instance = "Uzbl" screen = 0  tag = "2"  max =  "false" [/rule]

```

Esto abrirá Uzbl en el tag 2 desmaximizado. Para especificar un determinado layout para ese tag se agrega una linea en la sección [tags] como la siguiente :

```
[tag] name = "WWW"  screen = 0 layout = "tile_right" [/tag] 

```

Para algunas reglas, eje, cuando una aplicación se abre en una terminal, usted necesita especificar tanto la “clase” como la “instancia”:

```
[rule] instance = "mutt" class = "mutt" screen = 0  tag = "3"  max = "true" [/rule]

```

Use [xprop](http://www.xfree86.org/current/xprop.1.html) para determinar el valor para su regla.

### Combinación de Teclas

La sección [keys] del archivo `wmfsrc` le permite personalizar sus combinaciones de teclas. Como se describió anteriormente, esto podría significar simplemente cambiar el modificador por defecto de `Alt` a `Super`.

Por defecto, WMFS está configurado para recorrer los 9 layouts disponibles. Usted podría, por ejemplo, desear incluir alguna combinación de teclas que configure un especifico layout, digamos tile_right (el clásico modo mosaico). Usted puede enlazar esa función a `Super`+`t` de este modo:

```
[key] mod = {"Mod4"} key = "t" func = "set_layout" cmd = "tile_right" [/key]

```

Del mismo modo, puede personalizar las combinaciones de teclas para cualquiera de las otras funciones. Una lista completa de las funciones se pueden encontrar en `/ src /config.c` busque por "func_name_list_t".

#### Scratchpad

Combinando un regla con una combinación de teclas, usted puede crear un scratchpad básico – una terminal vinculada a una presión de teclas que la abrirá en modo flotante en cualquier tag en una posición especifica; por ejemplo:

```
[key] mod = {"Control", "Alt"} key = "p" func = "spawn" cmd = "urxvtc -name scratchpad -geometry 64x10+480+34" [/key]

[rule] instance = "scratchpad"  name  = "scratchpad"   free = "true"  [/rule]

```

### Configuración de la Barra de Estado

El texto que se muestra en la barra de estado (o barra de información) se encuentra corriendo en una instancia de wmfs usando el comando “wmfs -s”. Usted puede establecer una barra diferente para cada pantalla. Las barras también pueden ser posicionadas en la parte superior o inferior de cada tag editando el archivo de configuración. Por ejemplo:

```
wmfs -s "hola mundo, soy visible en todas las pantallas"
wmfs -s 3 "hola mundo, solo soy visible en la pantalla 4" # las pantallas empiezan en 0

```

Los **Colores** pueden ser asignados de la siguiente forma:

```
wmfs -s "Este texto es de color \\#ff0000\\rojo, \\#00ff00\\verde y \\#0000ff\\azul"

```

Los **Rectángulos** pueden ser dibujados de la siguiente forma:

```
wmfs -s "<--mira rectángulos \b[700;9;14;5;#00ff00]\ \b[715;4;14;10;#00ff00]\ \b[730;3;14;11;#ff0000]\ "

```

El formato es \b[xx;yy;ww;hh;#cccccc]\ donde “xx” y “yy” son relativas a las posiciones de “x” y “y”, “ww” y “hh” son largo y alto respectivamente, y #cccccc es el color. Esta característica puede ser usada para crear gráficos de barras. Nota:La posición absoluta hace que sea difícil la precisión de la interpolación de texto y gráficos.

Las **Imágenes** pueden ser añadidas de la siguiente forma:

```
 wmfs -s "Esta es una gran imagen \i[x;y;alto;largo;/home/tu/imagen]\ "

```

(La altura y largo por defecto de la imagen puede ser ajustada con altura=0 y con largo=0 en la secuencia.)

Las **Gráficas** pueden ser añadidas de la siguiente forma:

```
wmfs -s "graph \g[x;y;largo;alto;#color;data1;data2;...;datan]\ "

```

Para mas información acerca de imágenes o gráficas en la barra de estada: [http://fu.rootards.org/viewtopic.php?pid=14#p14](http://fu.rootards.org/viewtopic.php?pid=14#p14)

Para conectar información con la barra, escriba un script de bash con la información relevante que desea mostrar en su `wmfsrc`. WMFS llamara al script con el intervalo que usted especifique:

```
status_path = ".config/wmfs/wmfs-status"
status_timing = 5

```

Nota: La salida del status.sh es como se explicado anteriormente.

```
wmfs -s "Lo que desea que se muestre"

```

Algunos ejemplos de barras de estado se pueden encontrar en la pagina de [WMFS](http://wmfs.info/)

### Conky

Usted puede usar [conky](/index.php/Conky "Conky") para encanalar la salida a la barra de estado de WMFS con el comando:

```
conky | while read -r; do wmfs -s -name "$REPLY"; done

```

Puede agregar ese comando a su `.xinitrc` para lanzar conky en la barra de estado.

### WMFS Status Toolkit

[https://aur.archlinux.org/packages.php?ID=38463](https://aur.archlinux.org/packages.php?ID=38463)

## Uso

La combinación de teclas `Alt`+`p` inicia un lanzador en la barra de título (similar a[dmenu](/index.php/Dmenu "Dmenu")). Soporta la complementación-tab y parámetros de linea de comandos. Múltiples presiones a la tecla “Tab” , literalmente nos arroja posibles terminaciones del comando introducido

WMFS puede ser controlado desde la línea de comandos con órdenes tales como:

```
wmfs -V :ln

```

La cual selecciona el siguiente layout. De manera equivalente de presionar `Alt`+`Escape` seguido de ":ln". Escriba "wmfs -V help" para ver la lista completa.

## Recursos

*   [WMFS](http://wmfs.info/) página web
*   [WMFS Forum Thread](https://bbs.archlinux.org/viewtopic.php?pid=870703#p870703)
*   #wmfs en Freenode