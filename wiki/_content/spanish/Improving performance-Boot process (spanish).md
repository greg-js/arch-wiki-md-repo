Artículos relacionados

*   [Improving performance](/index.php/Improving_performance "Improving performance")
*   [Silent boot](/index.php/Silent_boot "Silent boot")
*   [Daemon](/index.php/Daemon "Daemon")
*   [e4rat](/index.php/E4rat "E4rat")
*   [Kexec](/index.php/Kexec "Kexec")

Mejorar el rendimiento de arranque de un sistema puede proporcionar que los tiempos de espera de arranque sean reducidos, para aprender más acerca de cómo ciertos archivos y scripts del sistema interactúan entre sí. En este artículo se intentará agregar métodos sobre cómo mejorar el rendimiento de arranque de un sistema Arch Linux.

## Contents

*   [1 Analizando los procesos de inicio](#Analizando_los_procesos_de_inicio)
    *   [1.1 Usando systemd-analyze](#Usando_systemd-analyze)
*   [2 Usando systemd-bootchart](#Usando_systemd-bootchart)
*   [3 Usando bootchart2](#Usando_bootchart2)
*   [4 Leer por adelantado (Readahead)](#Leer_por_adelantado_(Readahead))
*   [5 Compilando un custom kernel](#Compilando_un_custom_kernel)
*   [6 Initramfs](#Initramfs)
*   [7 Cominezo rápido de los serivicios](#Cominezo_rápido_de_los_serivicios)
*   [8 Escalonar spin-up](#Escalonar_spin-up)
*   [9 Montaje de sistemas de archivos](#Montaje_de_sistemas_de_archivos)
*   [10 Menos salida durante el arranque](#Menos_salida_durante_el_arranque)
*   [11 Suspensión de la RAM](#Suspensión_de_la_RAM)

## Analizando los procesos de inicio

### Usando systemd-analyze

[systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") proporciona una herramienta llamada `systemd-analyze` que se puede utilizar para mostrar los detalles de temporización sobre los procesos de arranque, incluyendo un diagrama que muestra en SVG, las unidades en espera de sus dependencias. También podemos ver qué archivos de unidades están causando el proceso de arranque para reducir la velocidad. A continuación, puede optimizar su sistema en consecuencia.

Para ver la cantidad de tiempo que hay en el espacio del núcleo y el espacio de usuario en el arranque, basta con utilizar:

```
$ systemd-analyze

```

**Sugerencia:** Si se inicia vía [Unified Extensible Firmware Interface (Español)](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)") (UEFI) y utiliza un gestor de arranque que implementa systemd [Boot Loader Interface](http://www.freedesktop.org/wiki/Software/systemd/BootLoaderInterface) (que actualmente [Systemd-boot (Español)](/index.php/Systemd-boot_(Espa%C3%B1ol) "Systemd-boot (Español)") y [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") do), *systemd-analyze* puede mostrar cuán rápido inició el firmware EFI y el porpio gestor de arranque.

Para listar los archivos en las unidades iniciadas, ordenadas por el tiempo que les tomó iniciar a cada uno:

```
$ systemd-analyze blame

```

En algunos puntos del proceso de arranque, las cosas no pueden continuar hasta que una determinada unidad tiene éxito. Para ver qué unidades se encuentran en éstos puntos críticos en la cadena de inicio, usamos:

```
$ systemd-analyze critical-chain

```

También podemos crear un archivo SVG que describe el proceso de arranque de forma gráfica simila a [Bootchart](/index.php/Bootchart "Bootchart"):

```
$ systemd-analyze plot > plot.svg

```

Ver [systemd-analyze(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-analyze.1) para más detalles.

## Usando systemd-bootchart

Bootchart se fusionó con **systemd** desde Octubre de 2012 y se puede usar para arrancar tal como lo haría con el bootchart original. Agregamos ésto a nuestro kernel:

```
initcall_debug printk.time=y init=/usr/lib/systemd/systemd-bootchart

```

Después de recoger una cierta cantidad de datos (configurable) las paradas de registro y un gráfico que se genera a partir de la información registrada. Este gráfico contiene pistas vitales en cuanto a que se utilizan los recursos (por defecto I/O, CPU y el inicio del Kernel), en qué orden y donde existen posibles problemas en la secuencia de arranque del sistema. Es esencialmente una versión más detallada de la función de parcela systemd-analizar.

Bootchart graphs escribe de manera predeterminada el time-stamped en /run/log y se guarda en journal como MESSAGE_ID=9f26aa562cf440c2b16c773d0479b518\. BOOTCHART= contiene el bootchart en format SVG.

Mirá la [manpage](http://www.freedesktop.org/software/systemd/man/systemd-bootchart.html) para más información.

## Usando bootchart2

También es posible usar una versión de bootchart para visualizar la secuencia de arranque. Puesto que no es capaz de poner un segundo inicio en la línea de comandos del kernel que no será capaz de utilizar cualquiera de las configuraciones estándar de Bootchart. Sin embargo el paquete [bootchart2-git](https://aur.archlinux.org/packages/bootchart2-git/) desde [AUR](/index.php/AUR "AUR") viene con servicio systemd deshabilitado. Luego de haber instalado bootchart2 hacemos:

```
# systemctl enable bootchart2

```

Podés visualizar los resultados por apertura */var/log/bootchart.png*, o si deseas más detalles de la ejecución:

```
$ pybootchartgui -i

```

Leer la [bootchart2 documentacion](https://github.com/mmeeks/bootchart) para más detalles sobre el uso de ésta versión de bootchart.

## Leer por adelantado (Readahead)

[systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") llegó hasta la versión 216 con su propia aplicación readahead que debería, en principio, mejorar el tiempo de arranque. Hay dos servicios `systemd-readahead-collect`, que recoge la información sobre la que se utilizan los archivos durante el arranque, y `systemd-readahead-replay`, que tira de estos archivos en la memoria caché temprano en el proceso de arranque.

Para habilitar systemd readahead instalamos el paquete [systemd-readahead](https://aur.archlinux.org/packages/systemd-readahead/) desde [AUR](/index.php/AUR "AUR") y escribimos:

```
# systemctl enable systemd-readahead-collect systemd-readahead-replay

```

**Nota:**

*   Es necesario reinciar un par de veces así systemd-readahead-collect pueda recoger suficiente información para que systemd-readahead-pleay trabaje con eficacia.
*   Dependiendo de la versión del kernel y el tipo de disco duro, su experiencia puede variar (por ejemplo, con un SSD verá poco o ningún beneficio o incluso puede ver un peor rendimiento).

## Compilando un custom kernel

Compilar un kernel personalizado puede reducir el tiempo de arranque y el uso de memoria. A pesar de la normalización de la arquitectura de 64 bits y la naturaleza modular del núcleo de Linux, estos beneficios pueden no ser tan grande como se esperaba. [Read more about compiling a kernel](/index.php/Kernel_Compilation_(Espa%C3%B1ol) "Kernel Compilation (Español)")

## Initramfs

Parecido a [#Compilando un custom kernel](#Compilando_un_custom_kernel), el initramfs puede ser más ligero. Una forma sencilla es incluir el [mkinitcpio (Español)](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") `autodetect` hook. Si querés ir más allá de éso puedes ver [Minimal initramfs](/index.php/Minimal_initramfs "Minimal initramfs").

## Cominezo rápido de los serivicios

Una característica central de systemd es [D-Bus (Español)](/index.php/D-Bus_(Espa%C3%B1ol) "D-Bus (Español)") y la activación de socket. Esto hace que los servicios sean arrancados cuando se accede a la primera y en general ésto es positivo. Sin embargo, si se sabe que un servicio (como ser [UPower](/index.php/UPower "UPower")) siempre se pondrá en marcha durante el arranque, el tiempo total de arranque podría reducirse si la comienza tan pronto como sea posible. Esto se puede lograr (si el archivo de servicio está configurado para ello, que en la mayoría de los casos es) de la siguiente manera:

```
# systemctl enable upower

```

Ésto hará que systemd inicie UPower tan pronto como sea posible sin causar ningún percance con los sockets o la activación de D-Bus.

## Escalonar spin-up

Algunos equipos implementan [staggered spin-up](https://en.wikipedia.org/wiki/Spin-up#Staggered_spin-up "wikipedia:Spin-up"), que hace que el sistema operativo a la sonda interfaces de ATA en serie, que se puede girar hasta las unidades de una en una y reducir el uso de energía de pico. Esto ralentiza la velocidad de arranque, y en la mayoría de los consumidores de hardware no proporciona ningún beneficio en absoluto ya que las unidades serán ya volver a acelerarse inmediatamente cuando la alimentación está activada. Para comprobar si se está utilizando SSS:

```
$ dmesg | grep SSS

```

Si no se utiliza durante el arranque, no habrá salida.

Para deshabilitarlo agregamos `libahci.ignore_sss=1` a nuestra [kernel line](/index.php/Kernel_line "Kernel line").

## Montaje de sistemas de archivos

Gracias a [mkinitcpio (Español)](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)")'s `fsck` hook, se puede evitar que se monte de difícil manera cambiando `ro` a `rw` en la línea del kernel y sacarlo de `/etc/fstab`. Las opciones que se pueden setear con `rootflags=mount options...` en nuestro kernel. Recuerda que debes eliminar la entrada de tu archivo `/etc/fstab` de lo contrario `systemd-remount-fs.service` seguirá trabajando. Alternativamente se podría de enmascarar ésa unidad.

Si btrfs está en uso para el sistema de ficheros raíz, no hay necesidad de un fsck en cada arranque al igual que otros sistemas de ficheros. Si este es el caso, [mkinitcpio (Español)](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)")'s `fsck` hook puede ser eliminado. También es posible que desee enmascarar el `systemd-fsck-root.service`, o decirle que no realice el *fsck* en nuestro sistema usando la línea `fsck.mode=skip`. Sin [mkinitcpio (Español)](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)")'s `fsck` hook, systemd seguirá usando fsckk sin ningún inconveniente con `systemd-fsck@.service`

También puedes eliminar la API desde el sistema desde `/etc/fstab`, como systemd los monta (ver `pacman -Ql systemd | grep '\.mount$'` para un listado). No es raro que los usuarios que tienen un /tmp viniendo de sysvinit, pero en el comando anterior puedes ver que systemd se encargó de éso. Ergo, puede ser removido de manera segura.

Otros sistemas de archivos como `/home` se pueden montar con unidadesd e montaje personalizados. Agregando `noauto,x-systemd.automount` para montar opciones amortiguar todos los accesos a la partición y se fsck y montarlo en el primer acceso, lo que reduce el número de sistemas de archivos que debe fsck / montaje durante el proceso de arranque.

**Nota:**

*   Ésto hará que su `/home` use el sistema de archivos con `autofs`, el cual se ignora con [mlocate](/index.php/Mlocate "Mlocate") por defecto. The speedup of automounting `/home` may not be more than a second or two, depending on your system, so this trick may not be worth it.

Si el sistema está instalado dentro de un [Btrfs](/index.php/Btrfs "Btrfs") (Especialmente: el directorio root `/` éste sería un volumen secundario) y `/home` se encuentra separado del sistema, aunque también es posible que desee evitar la creación de `/home` subvolume. Protegemos el `home.conf` tmpfile: `ln -s /dev/null /etc/tmpfiles.d/home.conf`.

## Menos salida durante el arranque

Cambiar `verbose` a `quiet` en el inicio de nuestro kernel. En algunos sistemas, en particlar aquellos con un SSD, el lento rendimiento de la TTY es en realidad un cuello de botella y por menos producción significa arranque más rápido.

## Suspensión de la RAM

La mejor manera de reducr el tiempo de booteo es que no inicie totalmente. Consideremos en cambio ésto: [suspending your system to RAM](/index.php/Suspend_and_hibernate#Suspend_to_RAM "Suspend and hibernate").