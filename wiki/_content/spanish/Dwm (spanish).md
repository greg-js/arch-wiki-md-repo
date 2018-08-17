Artículos relacionados

*   [dmenu](/index.php/Dmenu "Dmenu")
*   [wmii](/index.php/Wmii "Wmii")

[dwm](http://dwm.suckless.org/) es un gestor de ventanas dinámico para [X](/index.php/X "X"). Permite posicionar las mismas en forma de mosaico (tiling), en forma de pila (stack), y en pantalla completa (monocle), así como en diversas modalidades adicionales mediante la ayuda de parches opcionales. La disposición de las ventanas puede ser aplicada en forma dinámica optimizando así el entorno en función de la aplicación en uso y la tarea a realizar. dwm es extremadamente liviano y rápido, está escrito en C con la premisa de que su código fuente no supere las 2000 líneas. Provee soporte de multi-monitor para xrandr y Xinerama.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 Requerimientos](#Requerimientos)
    *   [1.2 Descarga de los scripts de creación con ABS](#Descarga_de_los_scripts_de_creaci.C3.B3n_con_ABS)
    *   [1.3 Creación e instalación del paquete](#Creaci.C3.B3n_e_instalaci.C3.B3n_del_paquete)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 Método 1: Re-crear con ABS (recomendado)](#M.C3.A9todo_1:_Re-crear_con_ABS_.28recomendado.29)
        *   [2.1.1 Personalizando config.h](#Personalizando_config.h)
        *   [2.1.2 Notas](#Notas)
    *   [2.2 Método 2: Mercurial (avanzado)](#M.C3.A9todo_2:_Mercurial_.28avanzado.29)
*   [3 Iniciando dwm](#Iniciando_dwm)
*   [4 Configuración de la barra de estado (statusbar)](#Configuraci.C3.B3n_de_la_barra_de_estado_.28statusbar.29)
    *   [4.1 Barra de estado básica](#Barra_de_estado_b.C3.A1sica)
    *   [4.2 Barra de estado con conky](#Barra_de_estado_con_conky)
*   [5 Uso extendido](#Uso_extendido)
    *   [5.1 Parches y modos de mosaico (tiling) adicionales](#Parches_y_modos_de_mosaico_.28tiling.29_adicionales)
        *   [5.1.1 Habilitar un posicionamiento (layout) diferente por cada tag](#Habilitar_un_posicionamiento_.28layout.29_diferente_por_cada_tag)
    *   [5.2 Eliminar espacios entre ventanas de las terminales](#Eliminar_espacios_entre_ventanas_de_las_terminales)
        *   [5.2.1 Urxvt](#Urxvt)
    *   [5.3 Reiniciar dwm sin cerrar sesión y programas abiertos](#Reiniciar_dwm_sin_cerrar_sesi.C3.B3n_y_programas_abiertos)
    *   [5.4 Deshabilitar el ganar foco con el ratón (mouse)](#Deshabilitar_el_ganar_foco_con_el_rat.C3.B3n_.28mouse.29)
*   [6 Recursos adicionales](#Recursos_adicionales)

## Instalación

Estas instrucciones le indicarán como instalar dwm utilizando [makepkg](/index.php/Makepkg "Makepkg") junto a al Arch Build System, o [ABS](/index.php/ABS "ABS"). Ésto le permitirá modificar la configuración posteriormente sin complicaciones. Si solamente está interesado en probar dwm, puede simplemente instalar el paquete binario desde los repositorios:

```
# pacman -S dwm

```

Tenga en cuenta que al omitir compilar dwm desde su código fuente la personalización se verá truncada, ya que toda la configuración de dwm es realizada editando el código fuente. Teniendo ésto en cuenta, el resto del artículo asume que dwm ha sido compilado desde el código fuente como será explicado a continuación en ésta sección.

Quizá también quiera considerar instalar [dmenu](/index.php/Dmenu "Dmenu"), un menú dinámico, rápido y liviano para X

1.  pacman -S dmenu

### Requerimientos

Las herramientas básicas de programación presentes en el paquete [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) son requeridas para compilar dwm y crear un paquete de éste, y el paquete de [abs](https://www.archlinux.org/packages/?name=abs) también es un requisito para obtener los scripts de creación:

```
# pacman -S base-devel abs

```

### Descarga de los scripts de creación con ABS

Una vez que los paquetes requeridos están instalados, utilize ABS para obtener los últimos scripts de creación desde los repositorios:

```
# abs community/dwm

```

Por último, copie los scripts de creación de dwm desde el árbol de directorios de ABS a un directorio temporal. Por ejemplo:

```
$ cp -r /var/abs/community/dwm ~/dwm

```

### Creación e instalación del paquete

Use `cd` para acceder al directorio que contiene los scripts de creación (en el ejemplo previo utilizamos `~/dwm`). Luego ejecute:

```
$ makepkg -i

```

Ésto compilará dwm, creará un paquete de Arch Linux conteniendo los archivos resultantes e instalará los paquetes, todo en un sólo paso. De ocurrir un problema durante éste proceso, verifique el mensaje mostrado por pantalla en busca de información relacionada.

**Sugerencia:** Si el directorio (`~/dwm`) es conservado, puede ser utilizado posteriormente para realizar cambios en la configuración por defecto.

## Configuración

Como se mencionó anteriormente, dwm es configurado exclusivamente en tiempo de compilación mediante algunos de sus archvos de código fuente, siendo éstos `config.h` y `config.mk`. Si bien la configuración inicial es funcional, es lógico esperar que en algún momento los usuarios deseen realizar modificaciones y ajustes a sus configuraciones.

### Método 1: Re-crear con ABS (recomendado)

Modificar la configuración de dwm es bastante sencillo utilizando éste procedimiento.

#### Personalizando config.h

Busque y diríjase al directorio que contiene el código fuente de dwm utilizado durante la [instalación](#Instalaci.C3.B3n) (`~/dwm` en el ejemplo anterior). Dentro de ésta carpeta encontramos el archivo `config.h`, en el cual se almacenan las preferencias generales de configuración de dwm. La mayoría de las opciones que encontramos dentro de éste archivo deberían ser auto-descriptivas, pese a que algunas no compartan el mismo rasgo. Para una información detallada de éstas opciones, visite el [http://www.suckless.org/dwm/](http://www.suckless.org/dwm/) sitio de dwm].

**Note:** Asegúrese de realizar una copia de respaldo del archivo `config.h`, en caso de que algo no funcione correctamente.

Una vez que realizamos los cambios , redirigimos el nuevo md5sums a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"):

```
$ makepkg -g >> PKGBUILD

```

Ésto eliminará un error de comparación entre los checksum del archivo `config.h` original y la copia modificada.

El paso siguiente es compilar y re-instalar:

```
$ makepkg -efi

```

Asumiendo que los cambios realizados en la configuración son válidos, éste comando compilará dwm, re-creará y re-instalará el paquete resultante. De ocurrir un problema durante éste proceso, verifique el mensaje mostrado por pantalla en busca de información relacionada.

Finalmente, reiniciamos dwm para aplicar los nuevos cambios.

#### Notas

De ahora en más, en vez de actualizar el md5sum para cada modificación del archivo `config.h`, que es sabido que ocurre frecuentemente, simplemente se podría eliminar el arreglo (array) de md5sum y re-crear dwm con la opción `--skipinteg`:

```
$ makepkg -efi --skipinteg

```

Luego de agregar unas líneas al script de inicio de dwm, es posible [reiniciar dwm sin cerrar sesión y programas abiertos](#Reiniciar_dwm_sin_cerrar_sesi.C3.B3n_y_programas_abiertos).

### Método 2: Mercurial (avanzado)

dwm es mantenido mayoritariamente con una versión de control [Mercurial](http://www.selenic.com/mercurial/wiki/) en [suckless.org](http://hg.suckless.org/dwm). Aquellos ya familiarizados con Mercurial pueden encontrar conveniente mantener las configuraciones y los parches con éste sistema. En el sitio web oficial podemos encontrar un [tutorial avanzado](http://www.suckless.org/dwm/customisation/patch_queue.html) referido al tema.

Antes de crear dwm desde las fuentes Mercurial, asegúrese de modificar el archivo `config.mk` adecuadamente, ya que un error en éste paso puede resultar en la caída del servidor X. Estos son los valores que necesitan ser modificados:

Modify `PREFIX`:

```
PREFIX = /usr

```

The X11 include folder:

```
X11INC = /usr/include/X11

```

And the the X11 lib directory:

```
X11LIB = /usr/lib/X11

```

## Iniciando dwm

Para iniciar dwm con `startx` o con el gestor de inicio de sesión [SLiM](/index.php/SLiM "SLiM"), simplemente agregue las siguientes líneas al archivo `~/.xinitrc`:

```
exec dwm

```

Si utiliza [GDM](/index.php/GDM "GDM"), debe agregar la línea a `~/.Xclients`, y seleccionar "Run XClient Script" del menú Sessions.

## Configuración de la barra de estado (statusbar)

dwm utiliza `xsetroot -name` para mostrar información en su barra de estado (statusbar)

### Barra de estado básica

Este ejemplo indica como mostrar la fecha en formato [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601 "wikipedia:ISO 8601"). Debemos agregar a `~/.xinitrc` or `~/.Xclients` las siguientes líneas:

```
while true; do
   xsetroot -name "$( date +"%F %R" )"
   sleep 1m    # Update time every minute
done &
exec dwm

```

Este ejemplo está pensado para las computadoras portátiles que dependen del paquete [acpi](https://www.archlinux.org/packages/?name=acpi) para mostrar información correspondiente a la batería:

```
while true ; do
    xsetroot -name "$( acpi -b | awk '{ print $3, $4 }' | tr -d ',' )"
    sleep 1m
done &
exec dwm

```

Éste script muestra la cantidad de batería restante, así como de su estado de carga mediante el comando awk para recortar el texto innecesarios de acpi y tr para eliminar las comas.

Una alternativa al script anterior es mostrar el estado de la batería de forma selectiva, en función del estado actual de carga:

```
while sleep 1m; do
  batt=`LC_ALL=C acpi -b`

  case $batt in
    *Discharging*) batt=${batt_main#* * * }; batt="${batt%%, *} " ;;
    *)             batt=''                                        ;;
  esac

  xsetroot -name "$batt`date +"%R"`"
done &
exec dwm

```

**Note:** Debe asegurarse de tener solamente una instancia de dwm en `~/.xinitrc` o `~/.Xclients`.

### Barra de estado con conky

Disponible en [AUR](/index.php/AUR "AUR"), [conky-cli](https://aur.archlinux.org/packages/conky-cli/) es una versión especial de conky que imprime la información a <tt>stdout</tt>. Si ya se encuentra acostumbrado a [conky](/index.php/Conky "Conky"), puede crear una barra de estado con abundante información en cuestión de minutos. Una vez que conky ha sido confiugrado a gusto, simplemente imprima el resultado redirigiendo conky a la barra de estado con `xsetroot -name`:

```
conky | while read -r; do xsetroot -name "$REPLY"; done &
exec dwm

```

El siguiente ejemplo de `.conkyrc` muestra diversa información de una computadora con doble núcleo:

```
background no
out_to_console yes
update_interval 2
total_run_times 0
use_spacer none

TEXT
$mpd_smart :: ${cpu cpu1}% / ${cpu cpu2}%  ${loadavg 1} ${loadavg 2 3} :: ${acpitemp}c :: $memperc% ($mem) :: ${downspeed eth0}K/s ${upspeed eth0}K/s :: ${time %a %b %d %I:%M%P}

```

Es posible también utilizar la versión estándar de [conky](/index.php/Conky "Conky") agregando la opción `out to x no` a la configuración de `.conkyrc`. En el anterior ejemplo se vería así:

```
background no
out_to_x no
out_to_console yes
update_interval 2
total_run_times 0
use_spacer none

TEXT
$mpd_smart :: ${cpu cpu1}% / ${cpu cpu2}%  ${loadavg 1} ${loadavg 2 3} :: ${acpitemp}c :: $memperc% ($mem) :: ${downspeed eth0}K/s ${upspeed eth0}K/s :: ${time %a %b %d %I:%M%P}

```

## Uso extendido

### Parches y modos de mosaico (tiling) adicionales

El sitio oficial tiene varios [parches](http://www.suckless.org/dwm/patches) que pueden agregar funcionalidad adicional a dwm. Los usuarios pueden personalizar fácilmente dwm mediante la aplicación de las modificaciones que deseen. Por ejemplo, el parche [Bottom Stack](http://www.suckless.org/dwm/patches/bottom_stack.html) provee una forma de posicionamiento en mosaico adicional que divide la pantalla en forma horizontal, al contrario de la forma original, que lo hace verticalmente. Así mismo, Bottom Stack divide los mosaicos secundarios en forma horizonta.

El parche [gaplessgrid](http://dwm.suckless.org/patches/gapless_grid) permite que la división en mosaicos sea en forma de grilla.

#### Habilitar un posicionamiento (layout) diferente por cada tag

El comportamiento por defecto de dwm es aplicar el posicionamiento seleccionado a todos los tags en forma simultánea. Para tener diferentes posicionamientos en diferentes tags, debemos utilizar el partche [pertag](http://dwm.suckless.org/patches/pertag).

### Eliminar espacios entre ventanas de las terminales

Si se ven espacios vacíos en el escritorio fuera de las ventanas de las terminales, probablemente se deba al tamaño de la fuente de la terminal. Para solucionar ésto, o bien puede ajustar el tamaño de la fuente hasta encontrar la escala ideal que elimina el hueco, o modificar `resizehints` a *False* en el archivo `config.h`:

```
static Bool resizehints = False; /* False means respect size hints in tiled resizals */

```

Ésto causará que dwm ignore las peticiones de ajuste de tamaño de todas las ventanas, no sólo de las terminales. La desventaja de esta solución es que algunas terminales pueden sufrir anomalías al ser re-dibujadas en pantalla, tales como líneas fantasma o saltos de líneas premators, entre otras.

#### Urxvt

Una opción para los usuarios de [urxvt](/index.php/Urxvt "Urxvt") es aplicar el parche ['hints patch'](/index.php/Urxvt#Fix_maximized_window_gaps "Urxvt") y regresar a dwm a su comportamiento original:

```
static Bool resizehints = **True**;

```

### Reiniciar dwm sin cerrar sesión y programas abiertos

Para reiniciar dwm sin cerrar sesión o cerrar los programas abiertos, modifique o agregue el siguiente código al script de inicio, así dwm carga en un bucle *while*, de la siguiente manera:

```
while true; do
    # Log stderror to a file 
    dwm 2> ~/.dwm.log
    # No error logging
    #dwm >/dev/null 2>&1
done

```

Ahora dwm puede ser reiniciado sin cerrar súbitamente otras ventanas X utilizando la combinaciones de teclas correspondiente (`Mod1+Shift+q` por defecto).

Es una buena idea poner el script anterior en un archivo separado, por ejemplo `~/bin/startdwm`, y ejecutarlo con `~/.xinitrc`. De ésta manera, cuando se desee reiniciar la sesión X, simplemente debe ejecutar `killall startdwm`, o asignarlo a una tecla de su conveniencia.

### Deshabilitar el ganar foco con el ratón (mouse)

Para deshabilitar la posibilidad de ganar foco utilizando el ratón, simplemente hay que comentar la siguiente línea en la definición de la estructura de control en `dwm.c`:

 `[EnterNotify] = enternotify, ` 

## Recursos adicionales

*   [Sitio oficial de dwm](http://www.suckless.org/dwm)
*   [dmenu](/index.php/Dmenu "Dmenu") - Lanzador de aplicaciones dinámico y simple de los desarrolladores de dwm
*   [Hilo de dwm en el foro](https://bbs.archlinux.org/viewtopic.php?id=57549/)
*   [Fondos de pantalla de dwm](http://www.flickr.com/photos/cinderwick/sets/72157604733895131/) y el hilo del foro de [fondos de pantalla de dwm](https://bbs.archlinux.org/viewtopic.php?id=57768/) (en inglés)
*   [HowTo por Snake](http://www.xsnake.net/howto/dwm/dwm-eng.php) (en inglés)
*   [Migrando a dwm](http://0x80.org/blog/?p=72) (en inglés)