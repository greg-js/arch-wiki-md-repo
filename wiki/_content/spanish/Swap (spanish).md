Artículos relacionados

*   [Swap on video ram](/index.php/Swap_on_video_ram "Swap on video ram")
*   [fstab (Español)](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)")

Definición de swap dada por el artículo [«Todo sobre el espacio swap de Linux»](http://www.linux.com/news/software/applications/8208-all-about-linux-swap-space):

	*Linux divide su memoria física RAM (memoria de acceso aleatorio) en capas de memoria llamadas páginas. El swapping es el proceso por el que una página de memoria se copia en un espacio del disco configurado previamente para ello, llamado espacio de swap (o de intercambio), para liberar esa memoria RAM. Los tamaños combinados de la memoria física y del espacio swap determinan la cantidad de memoria virtual disponible.*

El soporte para swap es proporcionado por el kernel de Linux y utilidades en el espacio de usuario por el paquete [util-linux](https://www.archlinux.org/packages/?name=util-linux).

## Contents

*   [1 Espacio swap](#Espacio_swap)
*   [2 Partición swap](#Partici.C3.B3n_swap)
    *   [2.1 Activación por systemd](#Activaci.C3.B3n_por_systemd)
*   [3 Archivo swap](#Archivo_swap)
    *   [3.1 Creación de un archivo swap](#Creaci.C3.B3n_de_un_archivo_swap)
    *   [3.2 Eliminación de un archivo swap](#Eliminaci.C3.B3n_de_un_archivo_swap)
*   [4 Swap en un dispositivo USB](#Swap_en_un_dispositivo_USB)
*   [5 Optimizar el rendimiento](#Optimizar_el_rendimiento)
    *   [5.1 Swappiness](#Swappiness)
    *   [5.2 Prioridad](#Prioridad)

## Espacio swap

El espacio swap o de intercambio será normalmente una partición del disco, pero también puede ser un archivo. Los usuarios pueden crear un espacio de intercambio durante la instalación de Arch Linux o en cualquier momento posterior, en caso de ser necesario. El espacio de intercambio es generalmente recomendado a los usuarios con menos de 1 GB de RAM, pero es una cuestión de preferencia personal en sistemas con cantidades generosas de memoria RAM física (aunque sí es necesario para utilizar la suspensión en disco).

Para comprobar el estado del swap, utilice la siguiente orden:

```
$ swapon -s

```

O bien:

```
$ free -h

```

**Nota:** No hay ventaja en el rendimiento entre un archivo swap contiguo o una partición, ambos son tratados de la misma manera.

## Partición swap

Una partición swap se puede crear con la mayoría de las herramientas que gestionan las particiones en GNU/Linux (por ejemplo, `fdisk`, `cfdisk`). Las particiones swap son designadas como tipo **82**, sin embargo, es posible utilizar cualquier tipo de partición como swap.

Para configurar un área swap Linux, se utiliza la orden `mkswap`. Por ejemplo:

```
# mkswap /dev/sda2

```

**Advertencia:** Todos los datos en la partición especificada se perderán.

La utilidad *mkswap* genera un UUID de la partición por defecto, utilice la etiqueta `-U` en el caso de que quiera especificar una UUID personalizada:

```
# mkswap -U *custom_UUID* /dev/sda2

```

Para activar el dispositivo para la paginación:

```
# swapon /dev/sda2

```

Para activar esta partición swap en el arranque, añada la entrada siguiente al archivo [fstab](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)"):

 `/etc/fstab`  `/dev/sda2 none swap defaults 0 0` 
**Nota:**

*   Añadir una entrada a fstab is optional es opcional en la mayoría de los casos con systemd. Vea la sección siguiente.
*   Si utiliza un SSD con soporte TRIM, considere usar `defaults,discard` en la línea swap de [fstab (Español)](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)"). Si activa manualmente swap con *swapon*, utilizar el parámetro `-d` o `--discard` producenel mismo efecto. Vea [swapon(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/swapon.8) para más detalles.

### Activación por systemd

systemd activa particiones de intercambio basándose en dos mecanismos diferentes, ambos ejecutables en `/usr/lib/systemd/system-generators`. Los generadores se ejecutan durante la puesta en marcha del sistema y crean unidades nativas de systemd para los montajes. El primero, `systemd-fstab-generator`, lee el archivo fstab para generar unidades, incluyendo una unidad para swap. El segundo, `systemd-gpt-auto-generator` inspecciona el disco raíz para generar unidades. Funciona con discos GPT solamente, y puede identificar particiones por su código tipo **82**.

Esto puede ser resuelto por una de las siguientes opciones:

*   eliminar la entrada swap de `/etc/fstab`;
*   cambiar el código tipo de la partición de intercambio de '*82'* a un código de tipo arbitrario;
*   establecer el atributo de la partición swap a «**63**: no se monta automáticamente».

## Archivo swap

Como una alternativa a la creación de toda una partición, un archivo swap ofrece la posibilidad de variar su tamaño sobre la marcha, y es más fácil de eliminar por completo. Esto puede ser especialmente deseable si el espacio es un bien escaso (por ejemplo, un disco SSD con un tamaño modesto).

**Nota:** El sistema de archivos BTRFS no es compatible actualmente con archivos swap. La inobservancia de esta advertencia puede conducir a un sistema de archivos corrupto. Aunque debe tenerse en cuenta que se puede utilizar un archivo de intercambio formateado con btrfs si se monta a través de un dispositivo loop. Este método puede reducir el rendimiento de swap drásticamente.

### Creación de un archivo swap

Como root, utilice `fallocate` para crear un archivo swap del tamaño de su elección (M = Megabytes, G = Gigabytes) (`dd` también se puede utilizar, pero se necesitará más tiempo). Por ejemplo, para crear un archivo swap de 512 MB, escriba :

```
# fallocate -l 512M /swapfile

```

o

```
# dd if=/dev/zero of=/swapfile bs=1M count=512

```

Establezca los permisos correctos (un archivo swap de lectura global es una enorme vulnerabilidad de seguridad)

```
# chmod 600 /swapfile

```

Después de crear el tamaño correcto del archivo, dé formato a swap:

```
# mkswap /swapfile

```

Active el archivo swap:

```
# swapon /swapfile

```

Edite [fstab](/index.php/Fstab_(Espa%C3%B1ol)#Ejemplo_de_archivo "Fstab (Español)") y añada esta entrada para el archivo swap:

 `/etc/fstab`  `/swapfile none swap defaults 0 0` 

### Eliminación de un archivo swap

**Advertencia:** swap es manejado por systemd y tendrá que reactivarla cada cierto tiempo.

Para eliminar un archivo swap, dicho archivo debe estar desactivado previamente.

Como root:

```
# swapoff -a

```

Elimine el archivo de intercambio:

```
# rm -f /swapfile

```

## Swap en un dispositivo USB

Gracias a la modularidad que ofrece Linux, podemos tener múltiples particiones repartidas en diferentes dispositivos. Si se tiene un disco duro muy lleno, el dispositivo USB puede usarse como partición temporal. Pero este método tiene algunas desventajas graves:

*   El dispositivo USB es más lento que el disco duro.
*   Las memorias flash tienen limitados los ciclos de lectura. Su uso como partición swap acortará su vida útil.
*   Cuando hay otro dispositivo conectado al ordenador, no se puede utilizar swap.

Para añadir un dispositivo USB para usarlo como SWAP, en primer lugar conecte un flah USB y dele formato con una partición swap. Puede utilizar herramientas gráficas como Gparted o herramientas de consola como fdisk. Asegúrese de marcar la partición como SWAP antes de escribir la tabla de particiones.

**Advertencia:** ¡Asegúrese de que está escribiendo la partición para el disco correcto!

A continuación edite el archivo `/etc/fstab`.

Ahora añada una nueva entrada, justo debajo de la entrada existente de swap, de modo que indique la nueva partición swap creada en el dispositivo USB, así:

```
UUID=... none swap defaults,pri=10 0 0

```

donde UUID se toma de la salida de la orden:

```
ls -l /dev/disk/by-uuid/ | grep /dev/sdc1

```

Basta con sustituir sdc1 por la nueva partición swap USB: `sdb1`

**Sugerencia:** Es preferible UUID porque al conectar otros dispositivos al ordenador se podría modificar el orden de los dispositivos periféricos.

Por último, añada

```
pri=0

```

en la entrada swap *originaria* para indicarle que use el archivo swap del disco duro solo cuando la partición swap del USB está llena.

Esta guía se puede aplicar a otras memorias, como tarjetas SD, etc.

## Optimizar el rendimiento

Los valores de swap se pueden ajustar para mejorar el rendimiento.

### Swappiness

El parámetro *swappiness* de [sysctl](/index.php/Sysctl "Sysctl") representa la preferencia del kernel (inhibiéndose) de utilización del espacio swap. Swappiness puede tener un valor entre 0 y 100\. Si se establece un valor bajo reducirá el intercambio desde RAM, y se sabe que mejora la capacidad de respuesta en muchos sistemas.

Para comprobar el valor actual de swappiness:

```
$ cat /proc/sys/vm/swappiness

```

Para ajustar temporalmente el valor swappiness:

```
# sysctl vm.swappiness=10

```

Para establecer de manera permanente el valor swappiness, editar un archivo de configuración *sysctl*:

 `/etc/sysctl.d/99-sysctl.conf`  `vm.swappiness=10` 

Para comprobar que esto puede funciona, eche un vistazo a [este artículo](http://rudd-o.com/en/linux-and-free-software/tales-from-responsivenessland-why-linux-feels-slow-and-how-to-fix-that).

Otro parámetro *sysctl* que afecta al rendimiento de swap es `vm.vfs_cache_pressure`, que controla la tendencia del kernel para reclamar la memoria que se utiliza para el almacenamiento de la caché VFS, frente a la pagecache y swap. Al aumentar este valor, aumenta la velocidad a la que la caché de VFS es demandada. [[1]](http://doc.opensuse.org/products/draft/SLES/SLES-tuning_sd_draft/cha.tuning.memory.html#cha.tuning.memory.vm.reclaim) Para más información, véase [Linux kernel documentation](https://www.kernel.org/doc/Documentation/sysctl/vm.txt).

### Prioridad

Si se tiene más de un archivo o partición swap debería considerar la posibilidad de asignarles un valor de prioridad (0 a 32767) para cada área swap. El sistema utilizará las áreas swap de mayor prioridad antes de utilizar las asignadas como de menor prioridad. Por ejemplo, si se tiene un disco más rápido (`/dev/sda`) y un disco más lento (`/dev/sdb`), asigne una mayor prioridad al área swap que se encuentra en el dispositivo más rápido. Las prioridades se pueden asignar en fstab a través del parámetro `pri`:

```
/dev/sda1 none swap defaults,pri=100 0 0
/dev/sdb2 none swap defaults,pri=10  0 0

```

O mediante los parámetros `−p` (o `−−priority`) de la orden swapon:

```
# swapon -p 100 /dev/sda1

```

Si dos o más áreas tienen la misma prioridad, y tienen asignada la más alta disponible, las páginas se distribuirá de forma *round-robin* entre ellas.