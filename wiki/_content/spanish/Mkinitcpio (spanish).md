**mkinitcpio** es un creador de [initramfs](https://en.wikipedia.org/wiki/es:initrd "wikipedia:es:initrd") de última generación.

## Contents

*   [1 Introducción](#Introducci.C3.B3n)
*   [2 Instalación](#Instalaci.C3.B3n)
*   [3 Creación de la imagen y activación](#Creaci.C3.B3n_de_la_imagen_y_activaci.C3.B3n)
*   [4 Configuración](#Configuraci.C3.B3n)
    *   [4.1 MÓDULOS](#M.C3.93DULOS)
    *   [4.2 BINARIOS y ARCHIVOS](#BINARIOS_y_ARCHIVOS)
    *   [4.3 HOOKS](#HOOKS)
        *   [4.3.1 Build hooks](#Build_hooks)
        *   [4.3.2 Runtime hooks](#Runtime_hooks)
        *   [4.3.3 Hooks más comunes](#Hooks_m.C3.A1s_comunes)
        *   [4.3.4 Hooks desatendidos](#Hooks_desatendidos)
    *   [4.4 COMPRESION](#COMPRESION)
    *   [4.5 COMPRESSION_OPTIONS](#COMPRESSION_OPTIONS)
*   [5 Personalizar el tiempo de ejecución](#Personalizar_el_tiempo_de_ejecuci.C3.B3n)
    *   [5.1 init](#init)
    *   [5.2 Usar RAID](#Usar_RAID)
    *   [5.3 Usar la red](#Usar_la_red)
    *   [5.4 Utilizar LVM](#Utilizar_LVM)
    *   [5.5 Utilizar root cifrado](#Utilizar_root_cifrado)
    *   [5.6 /usr en una partición separada](#.2Fusr_en_una_partici.C3.B3n_separada)
*   [6 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [6.1 Extraer la imagen](#Extraer_la_imagen)
*   [7 Véase también](#V.C3.A9ase_tambi.C3.A9n)
*   [8 Referencias](#Referencias)

## Introducción

mkinitcpio es un script bash utilizado para generar un ramdisk inicial. En [mkinitcpio man page](https://projects.archlinux.org/mkinitcpio.git/tree/mkinitcpio.8.txt):

	*El ramdisk inicial es básicamente un entorno muy pequeño ("pre-userspace"), que carga varios módulos del kernel y establece los pasos preliminares necesarios antes de entregar el control a init. De esta manera usted puede tener, por ejemplo, sistemas de archivos cifrados y sistemas de archivos en el software RAID. Mkinitcpio también permite extensiones personalizadas con los hooks, la detección automática en tiempo de ejecución, y muchas otras características.*

Tradicionalmente, el kernel es el responsable de la detección de hardware y las tareas de inicialización a principios del [proceso de arranque](/index.php/Boot_process "Boot process"), antes de montar el sistema de archivos root y pasar el control a `init`. Sin embargo, con los avances de la tecnología, estas actividades se han vuelto cada vez más complejas.

A día de hoy, el sistema de ficheros root se puede instalar en una amplia gama de hardware, de SCSI a SATA pasando por USB, el cual es monitoreado por una serie de controladores de unidades de diferentes fabricantes. Además, el sistema de ficheros root se puede comprimir o cifrar, en un software RAID o grupo de volumen lógico. La forma más fácil de manejar este rango de complejidad, es pasar la gestión al entorno userspace: el ramdisk inicial.

Consulte: [/dev/brain0 » Blog Archive » Early Userspace in Arch Linux](http://archlinux.me/brain0/2010/02/13/early-userspace-in-arch-linux/).

mkinitcpio es un instrumento modular para la construcción de una imagen init ramfs cpio, que ofrece muchas ventajas en comparación con métodos alternativos, entre ellos:

*   El uso de [BusyBox](http://www.busybox.net/), que proporciona una base mínima y ligera para el entorno de userspace.
*   Apoyo de **[udev](/index.php/Udev "Udev")** para detectar automáticamente el hardware durante la fase de ejecución, evitando así la carga de módulos innecesarios.
*   Usar init script extensibles sobre la base hook; los hooks pueden ser fácilmente personalizados incluidos en los paquetes [pacman](/index.php/Pacman "Pacman").
*   Apoyo de **LVM2**, **dm-crypt**, tanto para volúmenes legacy y LUKS, **mdadm**, **swsusp** y **suspend2** para la recuperación y el arranque desde dispositivos USB de almacenamiento masivo.
*   La capacidad de permitir que muchas características se puedan configurar desde la línea de comandos del kernel, sin la necesidad de reconstruir la imagen.

mkinitcpio ha sido desarrollado por Arch Linux y con la ayuda de la comunidad de diversas formas. Consulte [public Git repository](https://projects.archlinux.org/mkinitcpio.git/).

## Instalación

El paquete [mkinitcpio](https://www.archlinux.org/packages/?name=mkinitcpio) está disponible en los [repositorios oficiales](/index.php/Official_repositories "Official repositories"), y se instala por defecto en tanto que se incluye en el grupo [base](https://www.archlinux.org/groups/x86_64/base/).

Para los usuarios que prefieren instalar la última versión de desarrollo Git de mkinitcpio:

```
$ git clone [git://projects.archlinux.org/mkinitcpio.git](git://projects.archlinux.org/mkinitcpio.git)

```

**Nota:** ¡Usted debe seguir **seriamente** la lista de correo del proyecto en Arch [arch-projects mailing list](https://mailman.archlinux.org/mailman/listinfo/arch-projects) si va a utilizar la versión de GIT de mkinitcpio!

## Creación de la imagen y activación

Por defecto, el script mkinitcpio genera dos imágenes después de instalar o actualizar el kernel: `/boot/initramfs-linux.img` y `/boot/initramfs-linux-fallback.img`. La imagen *fallback* utiliza el mismo archivo de configuración que la imagen *predeterminada*, con la excepción del hook **autodetect** que se omite durante la creación, incluyendo, por tanto, una amplia gama de módulos. El hook de detección (**autodetect**) detecta automáticamente los módulos necesarios y personaliza la imagen para un hardware específico, lo que reduce el initramfs.

Los usuarios pueden crear cuantas imágenes initramfs deseen, con perfiles de configuración diferentes. La imagen deseada se debe especificar para el gestor de arranque, a menudo en su [archivo de configuración.](/index.php/Boot_Loader#Configuration_files "Boot Loader") Después de realizar los cambios en el fichero de configuración, la imagen debe ser regenerada. Para el valor del kernel de Arch Linux, [linux](https://www.archlinux.org/packages/?name=linux), ésto se hace mediante la ejecución de este comando como root:

```
# mkinitcpio -p linux

```

La opción `-p` indica un "preset" para ser utilizado; la mayoría de los paquetes kernel proveen un mkinitcpio predefinido, que se encuentra en `/etc/mkinitcpio.d` (por ejemplo `/etc/mkinitcpio.d/linux.preset` para `linux`). Un preset es una definición por defecto de cómo crear una imagen initramfs en lugar de especificar el archivo de configuración y el archivo de salida en cada ocasión.

**Advertencia:** El archivo *preset* se utiliza para regenerar el initramfs de forma automática después de una actualización del kernel; tenga cuidado si lo modifica

Los usuarios pueden crear manualmente una imagen con un archivo de configuración alternativo. Por ejemplo, la siguiente orden va a generar una imagen initramfs de acuerdo con las instrucciones de `/etc/mkinitcpio-custom.conf` y guardarlo en `/boot/linux-custom.img`.

```
# mkinitcpio -c /etc/mkinitcpio-custom.conf -g /boot/linux-custom.img

```

Para crear la imagen de un kernel diferente al actualmente en ejecución, agregar la versión del kernel a la línea de órdenes. Puede ver las versiones del kernel disponibles en `/usr/lib/modules`.

```
# mkinitcpio -g /boot/linux.img -k 3.0.0-ARCH

```

## Configuración

El archivo de configuración principal de **mkinitcpio** es `/etc/mkinitcpio.conf`. Además, las definiciones preestablecidas son proporcionadas por los paquetes del kernel en el directorio `/etc/mkinitcpio.d` (por ejemplo `/etc/mkinitcpio.d/linux.preset`).

**Advertencia:** **NO** son activadas por defecto **lvm2**, **mdadm** y **encrypt**. Por favor, lea atentamente esta sección para las instrucciones, si estos hooks son obligatorios.

**Nota:** Usuarios con varios controladores de disco de hardware que utilizan los nombres de los propios nodos, pero módulos del kernel diversos (por ejemplo, dos SCSI/SATA y dos controladores IDE) deben asegurarse de que el orden correcto de los módulos se especifica en `/etc/mkinitcpio.conf`. De lo contrario, la posición de la partición root puede variar, dando lugar a kernel panic. Una alternativa más plausible sería usar nombres de los dispositivos que no cambien [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming"), para asegurar que vengan siempre correctamente montados.

Los usuarios pueden modificar seis variables en el fichero de configuración:

	`MODULES`

	Módulos del kernel que se cargan antes de que los hooks se ejecuten al inicio.

	`BINARIES`

	Binarios suplementarios para incluir la imagen initramfs.

	`FILES`

	Los archivos adicionales que se incluirán en la imagen initramfs.

	`HOOKS`

	Los hooks son los scripts que se ejecutan en el ramdisk inicial.

	`COMPRESSION`

	Se utiliza para comprimir la imagen initramfs.

	`COMPRESSION_OPTIONS`

	Las opciones de la línea de comandos para el programa `COMPRESSION`.

### MÓDULOS

La matriz MODULES se utiliza para especificar los módulos a cargar antes de ejecutar cualquier otra cosa.

Los módulos con el sufijo `?` no devuelven un error si no se les encuentra. Esto puede ser muy útil si está creando un kernel personalizado que compile los módulos escritos explícitamentes en los Hooks, o en el archivo de configuración.

**Nota:** Si utiliza **reiser4**, éste *debe* ser añadido a la lista de los módulos. Adicionalmente, si va a necesitar un sistema de archivos durante el proceso de arranque, inexistente durante la ejecución de **mkinitcpio**, —como en el caso de una clave de cifrado LUKS en un sistema de archivos **ext2**, pero sin ningún sistema de archivos **ext2** montado cuando se ejecuta mkinitcpio—, el módulo de aquel sistema de archivos se debe añadir a la lista de MODULES. Consulte [aquí](/index.php/System_Encryption_with_LUKS_for_dm-crypt#Storing_the_Key_File "System Encryption with LUKS for dm-crypt") para obtener más detalles

### BINARIOS y ARCHIVOS

Estas opciones permiten al usuario añadir archivos a la imagen. Tanto `BINARIES` como `FILES` se agregan antes de que los hooks se ejecutan, y se puede usar para sobrescribir los archivos utilizados o suministrados por el hook. Los binarios son auto-localizados, ya que deben ser almacenados en un `PATH` estándar y son analizadores de dependencias, por lo que las necesidades de cada biblioteca y dependencias se sumarán en consecuencia. Los `FILES` se agregarán *como están*. Por ejemplo:

```
FILES="/etc/modprobe.d/modprobe.conf"

```

```
BINARIES="kexec"

```

### HOOKS

La configuración de los `HOOKS` es la más importante configuración del archivo. Los hooks son pequeños scripts que describen lo que se agregará a la imagen. Algunos hooks, también contienen un componente de tiempo de ejecución, que proporcionan un comportamiento adicional, como iniciar un demonio o ensamblar un dispositivo de bloque apilado. Los hooks son mencionados por su nombre, y se ejecutan en el orden establecido en la línea `HOOKS` del archivo de configuración.

Los ajustes por defecto para los `HOOKS` deberían ser suficientes para la mayoría de las configuraciones de discos únicos. Para los dispositivos root que se apilan o dispositivos multibloques como [LVM](/index.php/LVM "LVM"), [mdadm](/index.php/Software_RAID_and_LVM "Software RAID and LVM") o [LUKS](/index.php/LUKS "LUKS"), consulte las páginas wiki respectivas para la configuración adicional necesaria.

#### Build hooks

Los hooks compilados (*«build hooks»*) se encuentran en `/usr/lib/initcpio/install`. Estos archivos se obtienen por la shell bash durante el tiempo de ejecución de mkinitcpio y contienen dos funciones: `build` y `help`. La función `build` describe los módulos, archivos y binarios que se añadirán a la imagen. Una API, documentado por mkinitcpio (8), sirve para facilitar la adición de estos elementos. La función `help` genera una descripción de lo que el hook puede conseguir.

Para obtener una lista de todos los hooks disponibles:

```
$ mkinitcpio -L

```

El uso de la opción `-H` con mkinitcpio ayuda a mostrar información sobre un hook específico, por ejemplo:

```
$ mkinitcpio -H udev

```

#### Runtime hooks

Los hooks con temporizador (*«runtime hooks»*) se encuentran en `/usr/lib/initcpio/hooks`. Para cualquier runtime hook, siempre debe haber un build hook del mismo nombre, que llama a la función `add_runscript`, la cual añade runtime hook a la imagen. Estos archivos se obtienen por busybox ash shell durante el espacio de usuario inicial (*«early userspace»*). Con la excepción de los hooks de limpieza (*cleanup hooks*), los demás hooks siempre se ejecutan en el orden configurado en que aparecen en la lista `HOOKS`. Los runtime hooks pueden contener varias funciones:

`run_earlyhook`: Las funciones con este nombre se ejecutarán una vez que los sistemas de archivos API se han montado y la línea de comandos del kernel ha sido analizada. Esta es la fase donde se inician normalmente demonios adicionales, como udev, que se necesitan para el proceso de arranque inicial.

`run_hook`: Las funciones con este nombre se ejecutan poco después de los primeros hooks. Este es el punto más normal de actuación de los hooks, dado que las operaciones como montaje de dispositivos de bloques apilados deberían tener lugar aquí.

`run_latehook`: Las funciones con este nombre se ejecutan después de que el dispositivo raíz se ha montado. Esto se debe utilizar, con moderación, para la configuración adicional del dispositivo raíz, o para el montaje de otros sistemas de archivos, como `/usr`.

`run_cleanuphook`: Las funciones con este nombre se ejecutan lo más tarde posible, y en el orden contrario a como se muestran en la línea `HOOKS` del archivo de configuración. Estos hooks se deben utilizar para cualquier limpieza de última hora, como al cierre de cualquier demonio iniciado por un hook temprano.

#### Hooks más comunes

A continuación se muestra una tabla de los hooks más comunes y cómo afectan a la creación de la imagen y su tiempo de ejecución. Tenga en cuenta que esta tabla no es completa, ya que los paquetes pueden proporcionar hooks personalizados.

<caption>**Hooks actuales**</caption>
| Hook | Instalación | Tiempo de ejecución |
| **base** | Establece todos los directorios iniciales e instala los servicios básicos y bibliotecas. Agregue siempre este hook, a menos que sepa exactamente lo que está haciendo. | -- |
| **systemd** | Este instalará una configuración systemd básica en su initramfs, y está destinado a sustituir los hooks «base», «usr», «udev» y «timestamp». Otros hooks (como encryption) tendrán que ser adaptados, y puede que no funcionen según lo previsto. A partir de systemd 207, este hook no funciona como es debido cuando se combina con lvm2 y puede romper su arranque. También puede que desee todavía incluyen el hook «base» (antes de este hook) para asegurar que existe un shell de rescate en su initramfs. | -- |
| **btrfs** | Establece los módulos necesarios para activar Btrfs para root y la utilización de subvolúmenes. | Ejecuta «el escaneo del dispositivo btrfs» para ensamblar un multidispositivo con sistema de archivos root btrfs cuando ningún hook udev está presente. |
| **udev** | Añade udevd, udevadm y un pequeño conjunto de las reglas udev a la imagen. | Inicia el demonio udev y los procesos uevents del kernel; los cuales crean los nodos de los dispositivos. Ya que simplifica el proceso de arranque al no requerir que el usuario especifique explícitamente los módulos necesarios, el uso de este hook es recomendable. |
| **autodetect** | Reduce la imagne initramfs a un tamaño más pequeño mediante la creación de una lista blanca de los módulos mediante el escaneo de sysfs. Verifique que los módulos incluidos son los correctos y no falta ninguno. Este hook se debe iniciar antes que el subsistema de otro hook, para aprovechar al máximo la detección automática. Cada hook especificado en la línea HOOKS, antes de "autodetect", se instalará por completo. | -- |
| **modconf** | Carga los archivos de configuración de modprobe desde `/etc/modprobe.d` y `/usr/lib/modprobe.d` | -- |
| **block** | Agrega todos los módulos de los dispositivos de bloque, anteriormente proporcionados separadamente por los hooks **fw**, **mmc**, **pata**, **sata**, **scsi** , **usb** y **virtio**. | -- |
| **pcmcia** | Agrega los módulos necesarios para dispositivos PCMCIA. Necesitará instalar el paquete [pcmciautils](https://www.archlinux.org/packages/?name=pcmciautils) para usar esta opción. | -- |
| **net** | Agrega los módulos necesarios para un dispositivo de red. Para dispositivos PCMCIA agregue también el hook **PCMCIA**. | Proporciona control para un sistema de ficheros raíz basados en NFS. |
| **dmraid** | Proporciona soporte para proveedores de dispositivos root fakeRAID. Debe instalar el paquete [dmraid](https://www.archlinux.org/packages/?name=dmraid) para poder usar esta opción | Localiza y monta los dispositivos de bloque fakeRAID usando `dmraid`. |
| **mdadm** | Proporciona soporte para el montaje de las matrices RAID de `/etc/mdadm.conf`, o la detección automática durante el arranque. Debe tener [mdadm](https://www.archlinux.org/packages/?name=mdadm) instalado para utilizar esta opción. El hook **mdadm_udev** es preferible a este. | Busca y monta los dispositivos de bloque con software RAID usando `mdassemble`. |
| **madadm_udev** | Proporciona soporte para el montaje de sistemas RAID a través de udev. Si utiliza este hook con una matriz FakeRAID, es recomendable incluir `mdmon` en la sección binaries y añadir el hook **shutdown** a fin de evitar reconstruir innecesariamente RAID al arrancar. | Localiza y monta los dispositivos de bloque con software RAID usando `udev` y `mdadm` asegurando el montaje. Este es el método preferido de montaje mdadm (en lugar de utilizar el hook mdadm anterior). |
| **keyboard** | Añade los módulos necesarios para los dispositivos de teclado. Utilice esta opción si tiene un teclado USB y lo necesita en el espacio de usuario inicial (ya sea para introducir contraseñas de cifrado o para su uso en un shell interactiva). As a side-effect modules for some non-keyboard input devices might be added to, but this should not be relied on. | -- |
| **keymap** | Añade la distribución de teclado y la tipografía a la connsola según lo establecido en `/etc/vconsole.conf`. | Carga la distribución de teclado especificado y la tipografía de la consola de `/etc/vconsole.conf` durante la fase del espacio de usuario inicial. |
| **consolefont** | Agrega el tipo de letra de consola especificado en `/etc/vconsole.conf` a initramfs. | Carga el tipo de letra especificado para la consola en `/etc/vconsole.conf` durante la fase temprana del espacio de usuario. |
| **sd-vconsole** | Agrega la distribución del teclado y el tipo de fuente de la consola especificados en `/etc/vconsole.conf` a initramfs basado en systemd. | Carga la distribución del teclado y el tipo de fuente de la consola especificados durante la fase temprana del espacio de usuario. |
| **encrypt** | Agrega el módulo `dm_crypt` del kernel y la herramienta `cryptsetup` a la imagen. Tendrá que tener instalado el paquete [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) para usar esta opción. | Detecta y desbloquea una partición de root cifrada. Vea [#Personalizar el tiempo de ejecución](#Personalizar_el_tiempo_de_ejecuci.C3.B3n) para ajustar la configuración. |
| **sd-encrypt** | Este hook permite un dispositivo root encriptado con initramfs systemd.

Véase la página del manual de systemd-cryptsetup-generator(8) para conocer las opciones disponibles en línea de órdes del kernel. Alternativamente, si el archivo `/etc/crypttab.initramfs` existe, se añadirá a initramfs como `/etc/crypttab`. Véase la página del manual de crypttab(5) para obtener información sobre la sintaxis de crypttab.

 | -- |
| **lvm2** | Agrega el mapeador del dispositivo al módulo del kernel y la herramienta `lvm` a la imagen. Tendrá que tener instalado el paquete [lvm2](https://www.archlinux.org/packages/?name=lvm2) para usar esta opción. | Habilita todos los grupos de los volúmenes LVM2\. Esto es necesario si el sistema de archivos raíz está en [LVM](/index.php/LVM "LVM"). |
| **fsck** | Añade binarios de fsck y ayudas para el sistema de archivos específico. Si se coloca después del hook **autodetect** sólo se añade la ayuda para el sistema de archivos raiz. Utilizar este hook es **muy** recomendable, y es necesario si tiene una partición `/usr` separada. | Lanza fsck en el dispositivo root (y `/usr` si son distintos) antes del montaje. |
| **resume** | -- | Pretende volver a restaurar (resume) el sistema desde el estado de "suspensión en disco". Funciona conjuntamente con *swsusp* y *[suspend2](/index.php/Suspend2 "Suspend2")*. Vea [#Personalizar el tiempo de ejecución](#Personalizar_el_tiempo_de_ejecuci.C3.B3n) para ajustar configuración. |
| **filesystems** | Este incluye los módulos necesarios del sistema de archivos en la imagen. Este hook es **necesario**, a menos que especifique los módulos del filesystem en la línea MODULES. | -- |
| **shutdown** | Añade soporte al apagado en initramfs. Si se tiene una partición `/usr` separada o root cifrada, este hook es fundamental. | Desmonta y separa los dispositivos en el apagado. |
| **usr** | Añade soporte para la partición `/usr` separada. | Monta la partición `/usr` después de la partición raiz, para que quede correctamente montada. |

#### Hooks desatendidos

A partir de [mkinitcpio](https://www.archlinux.org/packages/?name=mkinitcpio) 0.13.0, el hook `usbinput` está en desuso en favor del hook `keyboard`.

A partir de [mkinitcpio](https://www.archlinux.org/packages/?name=mkinitcpio) 0.12.0, los hooks siguientes están en desuso. Si va a usar cualquiera de estos hooks, necesitará reemplazarlos con una sola instancia del hook `block`.

*   `fw`
*   `mmc`
*   `pata`
*   `sata`
*   `scsi`
*   `usb`
*   `virtio`

Para obtener más información, puede revisar Git commit [97368c0e78](https://projects.archlinux.org/mkinitcpio.git/commit/?id=97368c0e78f3a4fe4d62f7aedde88d4be13bfdba) o véase la [lista de correos de arch-projects](https://mailman.archlinux.org/pipermail/arch-projects/2012-November/003426.html).

### COMPRESION

El kernel soporta varios formatos para la compresión de las initramfs, gzip, bzip2, lzma, xz (también conocido como lzma2) y lzo. En la mayoría de los casos, gzip o lzop proporcionan el mejor equilibrio entre el tamaño de la imagen comprimida y la velocidad de descompresión.

```
COMPRESSION="gzip"
COMPRESSION="bzip2"  # since kernel 2.6.30
COMPRESSION="lzma"   # since kernel 2.6.30
COMPRESSION="lzop"   # since kernel 2.6.34
COMPRESSION="xz"     # since kernel 2.6.38
COMPRESSION="lz4c"   # since kernel 3.11

```

La falta de parámetro `COMPRESSION` dará como resultado un archivo initramfs comprimido en gzip . Para crear una imagen sin comprimir, especifica `COMPRESSION=cat` en la configuración o use la opción `-z cat` en la línea de comandos.

Asegúrese de tener instalada la utilidad de compresión de archivos correcta para el método que desee utilizar.

**Advertencia:** La compresión lz4 **requiere** [mkinitcpio](https://www.archlinux.org/packages/?name=mkinitcpio)>=16-2.

### COMPRESSION_OPTIONS

Estos son indicadores ulteriores que se pueden pasar al programa especificado por `COMPRESSION`, tales como:

```
COMPRESSION_OPTIONS='-9'

```

En general, esto no debería ser necesario, en cuanto que mkinitcpio asegurará que cualquier método de compresión soportará los indicadores necesarios para producir una imagen funcional.

## Personalizar el tiempo de ejecución

Las opciones de configuración sobre el tiempo de ejecución pueden ser enviados a `init` y algunos hooks a través de la línea de comandos del kernel. Los parámetros de la línea de comandos del kernel son a menudo proporcionados por el gestor de arranque. Las opciones que se exponen a continuación se pueden añadir a la línea de comandos del kernel para modificar el comportamiento predefinido. Vea [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") y [Arch boot process](/index.php/Arch_boot_process "Arch boot process") para más información.

### init

**Nota:** Las siguientes opciones alteran el comportamiento predeterminado de `init` en el entorno de initramfs. Vea `/usr/lib/initcpio/init` para obtener más información

	`root`

	Este es el parámetro más importante a especificar al kernel. Determina qué dispositivo debe estar instalado como root. mkinitcpio es flexible y permite una sintaxis diferente. Por ejemplo

```
root=/dev/sda1                                                # /dev node
root=LABEL=CorsairF80                                         # label
root=UUID=ea1c4959-406c-45d0-a144-912f4e86b207                # UUID
root=/dev/disk/by-path/pci-0000:00:1f.2-scsi-0:0:0:0-part1    # udev symlink (requiere el hook **udev** )
root=801                                                      # hex-encoded major/minor number

```

	`break`

	Si se especifica `break` o `break=premount`, `init` hace una pausa inicial en el proceso de arranque (después de cargar el módulos pero antes de montar la raíz) y ejecuta un shell interactivo que se puede utilizar para resolver cualquier problema. Este shell puede ser lanzado después de montar la raíz especificando `break=postmount`. La fase boot continúa después de cerrar la sesión.

	`disablehooks`

	Deshabilita los hooks en tiempo de ejecución mediante la adición de `disablehooks=hook1{,hook2,...}`. Por ejemplo: `disablehooks=resume` 

	`earlymodules`

	Cambia el orden en que se carguen los módulos, especificando los módulos que debe cargar primero `earlymodules=mod1{,mod2,...}`. (Esto podría ser utilizado, por ejemplo, para asegurar el orden correcto de múltiples interfaces de red).

	`rootdelay=N`

	Pausa durante `N` segundos antes de montar el sistema root, poniendo `rootdelay`. (Esto podría ser utilizado, por ejemplo, para el lanzamiento de un disco duro USB que es lento en la fase de arranque).

Vea también: [Depurar con GRUB e init](/index.php/Boot_debugging "Boot debugging")

### Usar RAID

Primero se debe agregar el hook `mdadm` a la matriz de `HOOKS`, y luego cada módulo raid que se requiera a la matriz de MODULES en `/etc/mkinitcpio.conf`.

**Parámetros del kernel:** Con el hook `mdadm`, ya no será necesario configurar la matriz RAID en los parámetros de [GRUB](/index.php/GRUB "GRUB"). El hook `mdadm` utilizará el archivo `/etc/mdadm.conf`, o detectará automáticamente las matrices durante el arranque inicial.

Si este parámetro se configura a través de udev, debe utilizar el hook `mdadm_udev`. Los desarrolladores prefieren este método de montaje `/etc/mdadm.conf` en cuanto que lee el nombre de los dispositivos conectados, en su caso.

### Usar la red

**Advertencia:** NFSv4 ya no es soportado.

**Paquetes requeridos:**

La red requiere que el paquete [mkinitcpio-nfs-utils](https://www.archlinux.org/packages/?name=mkinitcpio-nfs-utils) esté instalado de los [repositorios oficiales.](/index.php/Official_repositories "Official repositories")

**Parámetros del kernel:**

**ip=**

La especificación de una interfaz puede ser en formato corto, que es sólo el nombre de una interfaz ("eth0", o lo que sea), o un formato largo. El formato alargado puede estar constituido por siete elementos, separados por dos puntos:

```
 ip=<client-ip>:<server-ip>:<gw-ip>:<netmask>:<hostname>:<device>:<autoconf>
 nfsaddrs= es un alias para ip= y se puede utilizar también.

```

*Explicación de los parámetros*:

```
 <client-ip>   IP del cliente. Si está vacío, la dirección será
               determinada por RARP/BOOTP/DHCPP. El tipo de protocolo
               utilizado dependerá del parámetro <autoconf> . Si este
               parámetro no está vacío, se utiliza el autoconf.

 <server-ip>   IP del servidor NFS. Si RARP se utiliza para
               determinar la dirección del cliente, y este parámetro
               no está vacío, será aceptada sólo si el servidor
               especificado responde. Para utilizar diferentes RARP y NFS
               especificar el servidor RARP aquí (o dejarlo en blanco),
               y especifique el servidor NFS, en "nfsroot", el parámetro
               (Ver a continuación). Si esta entrada está en blanco se utilizará la dirección del servidor
               RARP/BOOTP/DHCP que respondiera a la solicitud.

 <gw-ip>       puerta de enlace si el servidor está en una subred
               diferente. Si está vacío, no se utilizarán las puertas de enlace y
               el servidor será, presumiblemente, el de la red local, a menos
               que no se reciba algún valor de BOOTP/DHCP.

 <netmask>     Máscara de red para la interfaz de red local. Si se deja en blanco,
               la máscara de red se deriva de la dirección IP del cliente que asume
               el direccionamiento "classful", a menos que sea cancelado por
               respuesta de BOOTP/DHCP.

 <hostname>    El nombre del cliente. Si está vacío, la dirección
               IP del cliente se utiliza en la notación ASCII, o el
               valor recibido por BOOTP/DHCP.

 <device>      Nombre del dispositivo de red para su uso. Si está vacío, todos los
               dispositivos se utilizan para las solicitudes de RARP/BOOTP/DHCP, y
               el primero en recibir una respuesta se configura. Si está utilizando
               un solo dispositivo, puede dejar esta entrada en blanco.

 <autoconf>    Método a utilizar para la configuración automática. Si incluye tanto
               "rarp", "bootp", como "dhcp" el protocolo especificado será
               utilizado. Si el valor es "both", "all" o vacío, todos los
               protocolos se utilizarán. "off", "static" o "none" significa no configurar automáticamente.

```

*Ejemplos:*

```
 ip=127.0.0.1:::::lo:none     --> Permitir interfaz de bucle invertido.
 ip=192.168.1.1:::::eth2:none --> Permitir la interfaz estática eth2.
 ip=:::::eth0:dhcp            --> Habilitar el protocolo dhcp para configurar eth0.

```

**BOOTIF=**

Si tiene varias tarjetas de red, este parámetro puede incluir la dirección MAC de la interfaz que está arrancando. Esto suele ser útil cuando la interfaz puede cambiar de numeración, o en conjunción con pxelinux IPAPPEND 2 o la opción IPAPPEND 3. Si no se da, eth0 va a ser utilizado.

*Ejemplo:*

```
 BOOTIF=01-A1-B2-C3-D4-E5-F6  # Note the prepended "01-" and capital letters.

```

**nfsroot=**

Si el parámetro "nfsroot" no se da en la línea de comandos, se utiliza el valor por defecto `/tftpboot/%s`.

```
 nfsroot=[<server-ip>:]<root-dir>[,<nfs-options>]

```

*Explicación de los parámetros*:

```
 <server-ip>   Especifica la dirección IP del servidor NFS. Si no se especifica,
               la dirección por defecto está determinado por "ip" variable
               (Ver abajo). Una utilidad de este valor es, por ejemplo
               la capacidad de utilizar diferentes servidores de RARP y NFS.
               En general, se puede dejar en blanco.

 <root-dir>    nombre de la carpeta en el servidor para montar como root. Si hay
               un "%s" en la cadena, el símbolo será sustituido por la
               representación ASCII de la dirección IP del cliente.

 <nfs-options> Opciones estándar NFS. Todas las opciones están separadas por comas.
               Si ninguna opción se proporciona, se utilizará
               siguiendo las opciones por defecto:
                       port            = as given by server portmap daemon
                       rsize           = 1024
                       wsize           = 1024
                       timeo           = 7
                       retrans         = 3
                       acregmin        = 3
                       acregmax        = 60
                       acdirmin        = 30
                       acdirmax        = 60
                       flags           = hard, nointr, noposix, cto, ac

```

**root=/dev/nfs**

Si usted no utiliza los parámetros de `nfsroot` debe configurar `root=/dev/nfs` a partir de un NFS de root para la configuración automática.

### Utilizar LVM

Si el dispositivo raíz se encuentra en LVM, usted tiene que agregar el hook **lvm2**, y cambiar el dispositivo raíz en la línea de comandos del kernel con el formato:

```
 root=/dev/mapper/<volume group name>-<logical volume name>

```

por ejemplo:

```
root=/dev/mapper/myvg-root

```

Además, si el dispositivo root puede iniciar lentamente (por ejemplo, un dispositivo USB) y/o recibe un error de "volume group not found" ("grupo de volúmenes que no se encuentra") durante el arranque, es posible que deba añadir lo siguiente a la línea de comandos del kernel:

```
 lvmwait=/dev/mapper/<volume group name><logical volume name>

```

por ejemplo:

```
lvmwait=/dev/mapper/myvg-root

```

Esto permite que el proceso de arranque espere hasta que LVM se las arregla para hacer que el dispositivo esté disponible.

### Utilizar root cifrado

Si el volumen de la raíz está cifrada, debe agregar el hook `encrypt`.

Para un root encriptado, use algo similar a:

```
 root=/dev/mapper/root cryptdevice=/dev/sda5:root

```

En este caso, `/dev/sda5` es el dispositivo cifrado, y le damos un nombre arbitrario de `root`, lo que significa que nuestro dispositivo raíz, una vez desbloqueado, se monta como `/dev/mapper/root`. En el arranque, se le pedirá la contraseña para desbloquear éste. Vea [LUKS#Configuration_of_initcpio](/index.php/LUKS#Configuration_of_initcpio "LUKS") para más detalles sobre el uso de root encriptado.

### /usr en una partición separada

Si durante la instalación de Arch Linux usted eligió montar `/usr` en una partición separada, debe tener en cuenta varias cosas:

*   Añadir el hook `shutdown`. Apagado, initscripts se basará en una copia guardada de initramfs y permitirá a `/usr` (y a la raíz) ser debidamente desmontada desde el VFS.
*   Añadir el hook `fsck`. Recomendado para todos, fundamental si quiere un *fsck* al iniciar la partición `/usr`. Sin este hook, `/etc/rc.sysinit` comenzará *fsck* con `/usr` montada y en consecuencia fallará.
*   A partir de mkinitcpio 0.9.0: Agregue el hook `usr`, además de los hooks de arriba. Esto montará la partición `/usr` después de que la partición raíz está montada. Antes de 0.9.0, el montaje de `/usr` sería automática si se encuentra en la raíz real `/etc/fstab`.

## Solución de problemas

### Extraer la imagen

Si usted es curioso y quiere saber qué hay dentro de la imagen initrd, se puede extraer, para una mirada al interior de los archivos.

La imagen initrd es un archivo SVR4 CPIO, generado por el comando `find` y `bsdcpio` y se comprime con un de los formatos de compresión compatibles con el kernel, llamados **gzip**, **bzip2**, **lzma**, **lzo** o **xz**.

mkinitcpio incluye una herramienta llamada `lsinitcpio`, que muestra y extrae el contenido de la imagen initramfs.

Usted puede listar los archivos de la imagen con:

```
$ lsinitcpio /boot/initramfs-linux.img

```

Y extraerlos en la carpeta actual:

```
$ lsinitcpio -x /boot/initramfs-linux.img

```

Usted también puede tener una lista un poco más amigable de las partes más importantes de la imagen:

```
$lsinitcpio -a /boot/initramfs-linux.imq

```

## Véase también

*   [Boot debugging](/index.php/Boot_debugging "Boot debugging") - Depurar con GRUB

## Referencias

*   Documentación del kernel de Linux: [initramfs](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=blob;f=Documentation/filesystems/ramfs-rootfs-initramfs.txt;hb=HEAD)
*   Documentación del kernel de Linux: [initrd](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=blob;f=Documentation/initrd.txt;hb=HEAD)
*   Artículo de Wikipedia: [initrd](http://es.wikipedia.org/wiki/initrd)