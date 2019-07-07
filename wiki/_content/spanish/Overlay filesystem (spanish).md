Desde [el commit del kernel inicial](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=e9be9d5e76e34872f0c37d72e25bc27fe9e2c54c)

	Overlayfs permite tener un árbol de directorios, usualmente de lectura-escritura, que es sobrepuesto sobre otro árbol de directorios de lectura-escritura. Todas las modificaciones van a una capa superior de escritura. Este tipo de mecanismo es mas común de ver en live CDs, pero tiene otra variedad de usos.

	La implementación difiere de otras implementaciones "union filesystem" (sistemas de archivos unificados) en que después de tener un archivo abierto, todas las operaciones van directamente a la capas del sistema de archivo superior o inferior. Esto simplifica la implementación y permite una performance nativa in varios casos.

Overlayfs fue incluido en la versión del kenkel 3.18.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Uso](#Uso)
    *   [2.1 overlay de solo lectura](#overlay_de_solo_lectura)
*   [3 Vea también](#Vea_también)

## Instalación

Overlayfs está habilitado en el kernel por defecto y el módulo de `overly` es automáticamente cargado pudiendolo utilizar con el comando mount.

## Uso

Para montar un overlay use las siguientes opciones de `mount`:

```
# mount -t overlay overlay -o lowerdir=*/lower*,upperdir=*/upper*,workdir=*/work* */merged*

```

**Note:** El directorio de trabajo (`workdir`) necesita ser un directorio vacío dentro del mismo sistema de archivos en el que está montado el directorio superior (upper).

El directorio inferior (lower) puede de hecho ser una lista de directorios separados por `:`, todos los cambios en el directorio `merged`, serán reflejados en el `upper`.

Ejemplo:

```
# mount -t overlay overlay -o lowerdir=*/lower1:/lower2:/lower3*,upperdir=*/upper*,workdir=*/work* */merged*

```

**Note:** El orden de los directorios inferiores (lower) va del mas inferior a la derecha, por lo tanto, el directorio superior (upper) está encima del primer directorio en la lista de directorios inferiores (lower) de izquierda a derecha; NO encima del último directorio de la lista, ya que el orden (o lógica) podría parecer sugerir.

En el siguiente ejemplo vamos a tener este orden;

```
/upper
/lower1 
/lower2
/lower3

```

Para agregar la entrada a `/etc/fstab` se usa el siguiente formato:

 `/etc/fstab`  `overlay */merged* overlay noauto,x-systemd.automount,lowerdir=*/lower*,upperdir=*/upper*,workdir=*/work* 0 0` 

Las opciones `noauto` y `x-systemd.automont` son necesarias para evitar que systemd se bloquee en el arranque al fallar el montaje del overlay. El overlay ahora se montará cada vez que se acceda por primera vez y las solicitudes se almacenen en el buffer hasta que esté listo. Vea [Fstab_(Español)#Montaje_automático_con_systemd](/index.php/Fstab_(Espa%C3%B1ol)#Montaje_automático_con_systemd "Fstab (Español)").

### overlay de solo lectura

En el caso de necesitar crear solo una vista en solo lectura de una combinacion de dos o mas directorios, se puede hacer de forma mas censilla, ya que en este caso los directorios `upper` y `work` **no** son necesarios:

```
# mount -t overlay overlay -o lowerdir=*/lower1:/lower2* */merged*

```

Cuando `upperdir` no es espesificado, overlay montará automáticamente como solo lectura.

## Vea también

*   [Overlay Filesystem documentation](https://www.kernel.org/doc/Documentation/filesystems/overlayfs.txt)