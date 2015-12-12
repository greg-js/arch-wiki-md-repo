# Beginners' guide (Español)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Artículos relacionados

*   [Category:Accessibility](/index.php/Category:Accessibility "Category:Accessibility")
*   [Help:Reading](/index.php/Help:Reading "Help:Reading")
*   [Installation guide (Español)](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)")
*   [General recommendations (Español)](/index.php/General_recommendations_(Espa%C3%B1ol) "General recommendations (Español)")
*   [General troubleshooting (Español)](/index.php/General_troubleshooting_(Espa%C3%B1ol) "General troubleshooting (Español)")
*   [Boot debugging](/index.php/Boot_debugging "Boot debugging")
*   [pacman#Troubleshooting](/index.php/Pacman#Troubleshooting "Pacman")
*   [pacman-key#Troubleshooting](/index.php/Pacman-key#Troubleshooting "Pacman-key")

**Estado de la traducción:** este artículo es una versión traducida de [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide"). Fecha de la última traducción/revisión: **2015-10-13**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Beginners%27_guide&diff=0&oldid=404349).

Este documento le guiará a través del proceso de instalación de [Arch Linux](/index.php/Arch_Linux_(Espa%C3%B1ol) "Arch Linux (Español)") usando los [Scripts de Instalación de Arch](https://github.com/falconindy/arch-install-scripts). Antes de proceder a la instalación, es recomendable la lectura del artículo sobre las preguntas más frecuentes ([FAQ (Español)](/index.php/FAQ_(Espa%C3%B1ol) "FAQ (Español)")).

La [wiki de Arch](/index.php/Main_Page_(Espa%C3%B1ol) "Main Page (Español)"), mantenida por la comunidad, es un recurso excelente que debería ser consultada para realizar los primeros pasos. También están disponibles el canal [IRC](https://en.wikipedia.org/wiki/es:Internet_Relay_Chat "wikipedia:es:Internet Relay Chat") ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)) y el [fórum](https://bbs.archlinux.org/) los cuales son igualmente buenos recursos si no ha podido encontrar la respuesta en otro lugar. Siguiendo [el método de Arch](/index.php/The_Arch_Way_(Espa%C3%B1ol) "The Arch Way (Español)"), se le aconseja que escriba `man _orden_` para leer la página del manual ([man page](/index.php/Man_page "Man page")), respecto de cualquier orden con la que no esté familiarizado.

## Contents

*   [1 Preparación](#Preparaci.C3.B3n)
*   [2 Iniciar el soporte de instalación](#Iniciar_el_soporte_de_instalaci.C3.B3n)
    *   [2.1 Arrancar en modalidad UEFI](#Arrancar_en_modalidad_UEFI)
    *   [2.2 Cambiar la distribución del teclado](#Cambiar_la_distribuci.C3.B3n_del_teclado)
    *   [2.3 Establecer una conexión a Internet](#Establecer_una_conexi.C3.B3n_a_Internet)
    *   [2.4 Actualizar el reloj del sistema](#Actualizar_el_reloj_del_sistema)
*   [3 Preparar los dispositivos de almacenamiento](#Preparar_los_dispositivos_de_almacenamiento)
    *   [3.1 Identificar los dispositivos](#Identificar_los_dispositivos)
    *   [3.2 Tipos de tablas de particiones](#Tipos_de_tablas_de_particiones)
    *   [3.3 Herramientas de particionado](#Herramientas_de_particionado)
        *   [3.3.1 Utilizar parted en modo interactivo](#Utilizar_parted_en_modo_interactivo)
    *   [3.4 Crear nueva tabla de particiones](#Crear_nueva_tabla_de_particiones)
    *   [3.5 Esquemas de particionado](#Esquemas_de_particionado)
        *   [3.5.1 Ejemplos UEFI/GPT](#Ejemplos_UEFI.2FGPT)
        *   [3.5.2 Ejemplos BIOS/MBR](#Ejemplos_BIOS.2FMBR)
    *   [3.6 Sistemas de archivos y swap](#Sistemas_de_archivos_y_swap)
*   [4 Instalar el sistema base](#Instalar_el_sistema_base)
    *   [4.1 Servidores de réplicas](#Servidores_de_r.C3.A9plicas)
    *   [4.2 Pacstrap](#Pacstrap)
*   [5 Configurar el sistema base](#Configurar_el_sistema_base)
    *   [5.1 Fstab](#Fstab)
    *   [5.2 Chroot](#Chroot)
    *   [5.3 Idioma](#Idioma)
    *   [5.4 Fecha y hora](#Fecha_y_hora)
    *   [5.5 Initramfs](#Initramfs)
    *   [5.6 Gestor de arranque](#Gestor_de_arranque)
        *   [5.6.1 BIOS/MBR](#BIOS.2FMBR)
        *   [5.6.2 UEFI/GPT](#UEFI.2FGPT)
    *   [5.7 Configurar la conexión de red](#Configurar_la_conexi.C3.B3n_de_red)
        *   [5.7.1 Nombre del equipo](#Nombre_del_equipo)
        *   [5.7.2 Red cableada](#Red_cableada)
        *   [5.7.3 Red inalámbrica](#Red_inal.C3.A1mbrica)
*   [6 Desmontar las particiones y reiniciar](#Desmontar_las_particiones_y_reiniciar)
*   [7 Posinstalación](#Posinstalaci.C3.B3n)

## Preparación

Arch Linux puede ser ejecutado en cualquier máquina [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) "wikipedia:P6 (microarchitecture)") compatible, con un mínimo de 256 MB de RAM. Una instalación básica con todos los paquetes del grupo [base](https://www.archlinux.org/groups/x86_64/base/) puede tomar alrededor de 800 MB de espacio en disco.

Vease [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch") para obtener instrucciones sobre cómo descargar el soporte de instalación y los métodos para iniciarlo en la máquina(s) de destino. Esta guía asume que utiliza la última versión disponible.

## Iniciar el soporte de instalación

Hay que indicar el dispositivo de arranque donde se encuentre el que contiene el soporte de instalación de Arch. Esto se logra, normalmente, presionando una tecla durante la fase [POST](https://en.wikipedia.org/wiki/es:Power-on_self_test "wikipedia:es:Power-on self test"), tecla que suele indicarse en la pantalla de presentación (del ordenador). Remítase el manual de su placa base para más detalles.

Cuando aparezca el menú de Arch, seleccione _Boot Arch Linux_ y pulse `Intro` para entrar en el entorno live de la instalación. Vea [README.bootparams](https://projects.archlinux.org/archiso.git/tree/docs/README.bootparams) para conocer un listado de los [parámetros de arranque](/index.php/Kernel_parameters_(Espa%C3%B1ol)#Configuraci.C3.B3n "Kernel parameters (Español)").

Iniciará sesión automáticamente como usuario root y aparecerá un intérprete de órdenes [Zsh](/index.php/Zsh "Zsh"). _Zsh_ le permitirá acceder a opciones avanzadas mediante la tecla Tab ([tab completion](http://zsh.sourceforge.net/Guide/zshguide06.html)) además de otras características como parte de la [configuración grml](http://grml.org/zsh/). Para la creación o modificación de archivos de configuración, normalmente en `/etc`, se sugiere utilizar [nano](/index.php/Nano_(Espa%C3%B1ol)#Uso "Nano (Español)") y [vim](/index.php/Vim#Usage "Vim").

### Arrancar en modalidad UEFI

En caso de tener una placa base [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)") con el modo de arranque UEFI activado, el CD/USB iniciará automáticamente Arch Linux con [systemd-boot](http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/).

Para asegurarnos de que hemos arrancado en modo UEFI, compruebe que el directorio siguiente tiene contenido:

```
# ls /sys/firmware/efi/efivars

```

Consulte [UEFI#UEFI Variables](/index.php/UEFI#UEFI_Variables "UEFI") para obtener más detalles.

### Cambiar la distribución del teclado

La distribución del teclado, por defecto, está establecida para [us](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg"). Las opciones disponibles se pueden enumerar con `localectl list-keymaps`.

Por ejemplo, para cambiar la distribución del teclado a `de-latin1`, ejecute:

```
# loadkeys _de-latin1_

```

Si algunos caracteres se muestran como cuadrados blancos u otros símbolos, puede cambiar el [tipo de letra de la consola](/index.php/Console_fonts "Console fonts"). Por ejemplo:

```
# setfont _lat9w-16_

```

### Establecer una conexión a Internet

El demonio de red [dhcpcd](/index.php/Dhcpcd "Dhcpcd") se inicia automáticamente en el arranque e intenta establecer una conexión cableada, si está disponible. Para acceder a los formularios de inicio de sesión de un [portal cautivo](https://en.wikipedia.org/wiki/es:Portal_cautivo "wikipedia:es:Portal cautivo"), utilice el navegador web [Elinks](/index.php/Elinks "Elinks").

Compruebe que se ha establecido una conexión, por ejemplo con la utilidad _ping_. Si no arroja resultado positivo, detenga el servicio _dhcpcd_ y [configure la conexión de red](/index.php/Network_configuration "Network configuration") manualmente. En el siguiente ejemplo se utiliza [netctl](/index.php/Netctl "Netctl") para este propósito.

```
# systemctl stop dhcpcd@_nombre_interfaz_.service

```

Las [interfaces](/index.php/Network_configuration#Device_names "Network configuration") de red pueden ser enumeradas con `ip link`, o `iw dev` a fin de encontrar las relativas a los dispositivos de red inalámbrica. Estas vienen precedidas por el prefijo `en` (ethernet), `wl` (WLAN), o `ww` (WWAN), dando como resultado nombres de interfaces como `enp0s25`.

Para conservar las configuraciones, copie los archivos de configuración modificados al nuevo sistema, antes de [[#Configurar el sistema base]|configurar el sistema base]].

Conexión a redes inalámbricas

Enumere las redes [wireless](/index.php/Wireless "Wireless") disponibles y conéctese una de ellas:

```
# wifi-menu -o _interfaz_de_red_

```

El archivo de configuración resultante de esta operación es guardado en `/etc/netctl`. Cuando la conexión de red requiera tanto un nombre de usuario como una contraseña, consulte [WPA2 Enterprise#netctl](/index.php/WPA2_Enterprise#netctl "WPA2 Enterprise").

Perfiles de conexiones de red

Hay disponibles distintos perfiles de ejemplo, tales como para configurar [direcciones IP estáticas](/index.php/Network_configuration#Static_IP_address "Network configuration"). Copie uno de los que necesite a `/etc/netctl`, por ejemplo `ethernet-static`:

```
# cp /etc/netctl/examples/_ethernet-static_ /etc/netctl

```

Ajuste la copia según sus necesidades, y actívela:

```
# netctl start _ethernet-static_

```

### Actualizar el reloj del sistema

Utilice [systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd") para asegurarse de que el reloj del sistema tiene la hora correcta. Para iniciarlo:

```
# timedatectl set-ntp true

```

Para comprobar el estado del servicio, utilice `timedatectl status`.

## Preparar los dispositivos de almacenamiento

**Advertencia:**

*   En general, particionar o formatear hará que los datos existentes sean inaccesibles y sujetos a ser sobrescritos, es decir destruidos, por las operaciones posteriores. Por esta razón, todos los datos que necesiten ser preservados deben ser respaldados antes de proceder.
*   Si Arch y Windows comparten arranque dual en el mismo disco con un sistema UEFI/GPT, evite formatear la partición UEFI, ya que incluye los archivos _.efi_ de Windows necesarios para arrancarlo. Además, Arch debería seguir la misma combinación de particionado y modalidad de arranque del firmware que la utilizada por Windows instalado en el disco. Vea [Windows and Arch Dual Boot#Important information](/index.php/Windows_and_Arch_Dual_Boot#Important_information "Windows and Arch Dual Boot").

En este paso, se prepararán los dispositivos de almacenamiento que serán utilizados por el nuevo sistema. Lea [Partitioning (Español)](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)") para obtener una visión más general.

Los usuarios que tengan la intención de crear dispositivos de bloques apilados para [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)"), [disk encryption (Español)](/index.php/Disk_encryption_(Espa%C3%B1ol) "Disk encryption (Español)") o [RAID (Español)](/index.php/RAID_(Espa%C3%B1ol) "RAID (Español)"), deben tener en cuenta las instrucciones de dichos artículos al preparar las particiones. Si su intención es instalar Arch en una memoria flash USB, consulte [Installing Arch Linux on a USB key (Español)](/index.php/Installing_Arch_Linux_on_a_USB_key_(Espa%C3%B1ol) "Installing Arch Linux on a USB key (Español)").

### Identificar los dispositivos

El primer paso es identificar los dispositivos en los que se instalará el nuevo sistema. La siguiente orden mostrará todos los dispositivos disponibles:

```
# lsblk

```

Esto mostrará una lista de todos los dispositivos conectados a su sistema junto con sus esquemas de particionado, incluido el dispositivo utilizado para acoger —y arrancar— el soporte de instalación live de Arch (por ejemplo, una unidad USB). No todos los dispositivos enumerados por la salida de la orden anterior serán medios viables o apropiados para la instalación. Los resultados que terminen en `rom`, `loop` o `airoot` pueden ser ignorados.

Los dispositivos (por ejemplo, discos duros) se enumerarán como `sd_x_ `, donde `_x_` es una letra minúscula partiendo de `a` para el primer dispositivo (`sda`), `b` para el segundo dispositivo (`sdb`), y así sucesivamente. Las particiones existentes en esos dispositivos serán listadas como `sd_xY_`, donde `_Y_` es un número a partir de `1` para la primera partición, `2` para la segunda, y así sucesivamente. En el ejemplo siguiente, solo un dispositivo está disponible (`sda`), y el dispositivo utiliza una sola partición (`sda1`):

```
NAME            MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda               8:0    0    80G  0 disk 
└─sda1            8:1    0    80G  0 part

```

La convención `sd_xY_` será utilizada en los ejemplos que figuran a continuación para las tablas de particionado, particiones y sistemas de archivos. Como son solo ejemplos, es importante que se asegure de realizar los cambios necesarios en los nombres de sus dispositivos, números y/o tamaño de sus particiones, etc. Es decir, no copie y pegue sin más las órdenes de abajo.

Si el esquema de particionado existente no necesita ser cambiado, vaya a [#Sistemas de archivos y swap](#Sistemas_de_archivos_y_swap), de lo contrario continúe leyendo la siguiente sección.

### Tipos de tablas de particiones

Si va a instalar Arch junto a otra instalación ya presente (es decir, hablamos de un arranque dual), ya estará en uso una tabla de particiones. En otro caso, si los dispositivos no están particionados, o el esquema o tabla de particionado vigente necesita ser cambiado, tendrá que determinar primero las tablas de particionado (una por cada dispositivo) que se están usando o que se van a utilizar.

Hay dos tipos de tabla de particiones:

*   [MBR](/index.php/Master_Boot_Record_(Espa%C3%B1ol) "Master Boot Record (Español)")
*   [GPT](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)")

Cualquier tabla de particionado existente puede identificarse con la siguiente orden invocada respecto a cada dispositivo:

```
# parted /dev/sd_x_ print

```

### Herramientas de particionado

**Advertencia:** Utilizar una herramienta de particionado que sea incompatible con su tipo de tabla de particiones dará como resultado la destrucción de dicha tabla, además de las particiones/datos existentes.

Para cada dispositivo que va a particionar, debe elegir una herramienta apropiada de acuerdo a la tabla de particiones que se piensa usar. Existen distintas herramientas de particionado que se proporcionan por el soporte de instalación de Arch, que son:

*   [parted](/index.php/Parted "Parted"): para MBR y GPT
*   [fdisk](/index.php/Partitioning_(Espa%C3%B1ol)#Resumen_del_uso_de_fdisk "Partitioning (Español)"), **cfdisk**, **sfdisk**: para MBR y GPT
*   [gdisk](/index.php/Partitioning_(Espa%C3%B1ol)#Resumen_del_uso_de_gdisk "Partitioning (Español)"), **cgdisk**, **sgdisk**: para GPT

Los dispositivos también puede ser particionados antes de arrancar el soporte de instalación, por ejemplo, utilizando herramientas como [GParted](/index.php/GParted "GParted") (que además se ofrece como un [CD live](http://gparted.sourceforge.net/livecd.php)).

#### Utilizar parted en modo interactivo

Todos los ejemplos proporcionados a continuación hacen uso de _parted_, ya que puede ser utilizado tanto para sistemas BIOS/MBR como para UEFI/GPT. Dicha herramienta será lanzada en _modo interactivo_, lo que simplificará el proceso de particionado y reducirá la repetición innecesaria de órdenes, al automatizar la aplicación de todas las órdenes de particionado a los dispositivos especificados.

Con el fin de comenzar a operar sobre un dispositivo, ejecute:

```
# parted /dev/sd_x_

```

Advertirá que el símbolo de la línea de órdenes cambia de (`#`) a `(parted)`: esto también significa que el nuevo prompt (que aparece en los ejemplos) no es una orden que deba introducirse manualmente junto a la ejecución de las órdenes de los ejemplos.

Para ver una lista de las órdenes disponibles, escriba:

```
(parted) help

```

Cuando haya terminado, o si desea implementar una tabla o esquema de particionado para otro dispositivo, salga de parted con:

```
(parted) quit

```

Después de salir, el símbolo de la línea de órdenes cambiará de nuevo a `#`.

### Crear nueva tabla de particiones

Es necesario (re)crear la tabla de particiones de un dispositivo cuando nunca ha sido particionado antes, o cuando se desea cambiar su tipo de tabla de particiones. Recrear la tabla de particiones de un dispositivo también es útil cuando el esquema de partición necesita ser reestructurado a partir de cero.

Abra cada dispositivo cuya tabla de particiones desea (re)crear con:

```
# parted /dev/sd_x_

```

Para crear, una vez iniciada sesión con _parted_, una nueva tabla de particiones MBR/msdos para sistemas BIOS, utilice la siguiente orden:

```
(parted) mklabel msdos

```

Para crear una nueva tabla de particiones GPT para sistemas UEFI en su lugar, utilice:

```
(parted) mklabel gpt

```

### Esquemas de particionado

Puede decidir el número y el tamaño de las particiones en los que va a dividir sus dispositivos, y los directorios que se utilizaránn para montar las particiones en el sistema instalado (también conocido como _puntos de montaje_). La asignación de las particiones a los directorios es a lo que denominamos [esquema de particionado](/index.php/Partitioning_(Espa%C3%B1ol)#Esquemas_de_particionado "Partitioning (Español)"), que deberá cumplir con los siguientes requisitos:

*   Se **debe** crear, al menos, una partición para el directorio `/` (_root_).
*   Cuando se utiliza una placa base UEFI, se **debe** crear una [EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface").

En los ejemplos siguientes partimos del supuesto de que tenemos un esquema de particionado nuevo y contiguo que se aplica a un solo dispositivo. También se crearán algunas particiones (que son opcionales) para los directorios `/boot` y `/home`: ver también [Arch filesystem hierarchy](/index.php/Arch_filesystem_hierarchy "Arch filesystem hierarchy") para una explicación de los propósitos de los diferentes directorios; si no se han creado particiones separadas para directorios tales como `/boot` o `/home`, estos simplemente vendrán contenidos en la partición `/`. También se ilustrará en esta guía la creación de una particion opcional para el [espacio swap](/index.php/Swap_(Espa%C3%B1ol) "Swap (Español)").

Si no tiene abierta ya una sesión interactiva con _parted_, abra una para cada dispositivo que va a ser particionado:

```
# parted /dev/sd_x_

```

La siguiente orden se utiliza para crear las particiones:

```
(parted) mkpart _part-type_ _fs-type_ _start_ _end_

```

*   `_part-type_` define la partición como `primary`, `extended` o `logical`, y es significativo solo para las tablas de particiones MBR.
*   `_fs-type_` define uno de los sistemas de archivos soportados de los enumerados en el [manual](http://www.gnu.org/software/parted/manual/parted.html#mkpart). Veremos cómo se formatea correctamente la partición en la sección [#Sistemas de archivos y swap](#Sistemas_de_archivos_y_swap). La orden _mkpart_ no crea realmente el sistema de archivos: el parámetro `_fs-type_` simplemente será utilizado por _parted_ para establecer un código de 1-byte que será usado por los gestores de arranque como «vista previa» para saber qué tipo de datos se encontrará en la partición y actuar en consecuencia si fuera necesario. Vea también [tipos de particiones](https://en.wikipedia.org/wiki/Disk_partitioning#PC_partition_types "wikipedia:Disk partitioning").

**Sugerencia:** La mayoría de los [sistemas de archivos nativos de Línux](https://en.wikipedia.org/wiki/File_system#Linux "wikipedia:File system") mapean con el mismo código de partición ([0x83](https://en.wikipedia.org/wiki/Partition_type#PID_83h "wikipedia:Partition type")), por lo que es perfectamente seguro, por ejemplo, utilizar `ext2` para una partición formateada con _ext4_.

*   `_start_` es el principio de la partición contado desde el inicio del dispositivo. Se compone de un número seguido de una [unidad](http://www.gnu.org/software/parted/manual/parted.html#unit), por ejemplo `1M` significa que la partición comienza después de 1MiB.
*   `_end_` es el final de la partición contado desde el inicio del dispositivo. (_no_ desde el valor `_start_`). Tiene la misma sintaxis que `_start_`, por ejemplo `100%` significa que el final de la partición alcanza el final del dispositivo (esto es, utiliza todo el espacio restante).

**Advertencia:** Es importante que las particiones no se solapen entre sí: si no quiere dejar espacio sin utilizar en el dispositivo, asegúrese de que cada partición comienza donde termina la anterior.

**Nota:** _parted_ podrá emitir una advertencia como esta:

```
Warning: The resulting partition is not properly aligned for best performance.
Ignore/Cancel?

```

En este caso, lea [Partitioning (Español)#Alineamiento de las particiones](/index.php/Partitioning_(Espa%C3%B1ol)#Alineamiento_de_las_particiones "Partitioning (Español)") y continue en [GNU Parted#Alignment](/index.php/GNU_Parted#Alignment "GNU Parted") para arreglarlo.

La siguiente orden se utiliza para etiquetar la partición que contiene el directorio `/boot` como de arranque:

```
(parted) set _partition_ boot on

```

*   `_partition_` es el número de la partición que se etiqueta (ver la salida de la orden `print`).

#### Ejemplos UEFI/GPT

En todos los casos, es necesario crear una partición especial llamada [EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#EFI_System_Partition "Unified Extensible Firmware Interface (Español)") con capacidad de arranque.

Si crea una nueva EFI System Partition, utilice la orden siguiente (el tamaño recomendado es 512MiB):

```
(parted) mkpart ESP fat32 1M 513M
(parted) set 1 boot on

```

El esquema de partición restante es de creación totalmente libre. Para crear otra partición utilizando el 100% del espacio restante, escriba:

```
(parted) mkpart primary ext3 513M 100%

```

Para crear una partición `/` (20GiB) y otra `/home` (todo el espacio restante), escriba:

```
(parted) mkpart primary ext3 513M 20.5G
(parted) mkpart primary ext3 20.5G 100%

```

Y, para crear una partición `/` (20GiB), otra swap (4Gib) y otra `/home` (todo el espacio restante), escriba:

```
(parted) mkpart primary ext3 513M 20.5G
(parted) mkpart primary linux-swap 20.5G 24.5G
(parted) mkpart primary ext3 24.5G 100%

```

#### Ejemplos BIOS/MBR

Para una única partición primaria, utilizando todo el espacio disponible, se utilizaría la siguiente orden:

```
(parted) mkpart primary ext3 1M 100%
(parted) set 1 boot on

```

En el siguiente ejemplo, se creará una partición `/` de 20Gib, seguida por una partición `/home` para todo el espacio restante:

```
(parted) mkpart primary ext3 1M 20G
(parted) set 1 boot on
(parted) mkpart primary ext3 20G 100%

```

En el último ejemplo, se creará una partición separada `/boot` (100MiB), seguida de otra `/` (20Gib), otra swap (4GiB), y una última `/home` (para todo el espacio restante):

```
(parted) mkpart primary ext3 1M 100M
(parted) set 1 boot on
(parted) mkpart primary ext3 100M 20G
(parted) mkpart primary linux-swap 20G 24G
(parted) mkpart primary ext3 24G 100%

```

### Sistemas de archivos y swap

Una vez creadas las particiones, cada una de ellas debe ser formateada con un [sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)") adecuado, excepto para las particiones de intercambio (swap). Todas las particiones disponibles en el dispositivo destinado a la instalación pueden ser listadas con la siguiente orden:

```
# lsblk /dev/sd_x_

```

Con las excepciones indicadas a continuación, se recomienda utilizar el sistema de archivos `ext4`:

```
# mkfs.ext4 /dev/sd_xY_

```

_Si_ se ha creado una nueva partición UEFI del sistema sobre un sistema UEFI/GPT, la misma **debe** estar formateada con el sistema de archivos `fat32`:

```
# mkfs.fat -F32 /dev/sd_xY_

```

_Si_ se ha creado una partición de intercambio (swap), se debe configurar y activar con:

```
# mkswap /dev/sd_xY_
# swapon /dev/sd_xY_

```

Monte la partición root en el directorio `/mnt` del entorno live de instalación:

```
# mount /dev/sd_xY_ /mnt

```

Las [particiones](#Esquemas_de_particionado) restantes (excepto _swap_) pueden ser montadas en cualquier orden, después de crear sus respectivos puntos de montajes. Por ejemplo, cuando se utiliza una partición `/boot` separada:

```
# mkdir -p /mnt/boot
# mount /dev/sd_xZ_ /mnt/boot

```

Se recomienda también utilizar `/boot` para montar la partición EFI del sistema («EFI System Partition») en sistemas UEFI/GPT. Vea [EFISTUB (Español)](/index.php/EFISTUB_(Espa%C3%B1ol) "EFISTUB (Español)") y artículos relacionados para conocer alternativas.

## Instalar el sistema base

### Servidores de réplicas

Es posible que desee modificar el archivo `mirrorlist` y colocar el servidor de réplica preferido por encima de los demás. Una copia de este archivo se instalará en su nuevo sistema por _pacstrap_, de modo que conviene hacerlo bien.

 `/etc/pacman.d/mirrorlist` 

```
##
## Arch Linux repository mirrorlist
## Sorted by mirror score from mirror status page
## Generated on YYYY-MM-DD
##

Server = http://mirror.example.xyz/archlinux/$repo/os/$arch
...
```

Si lo desea, puede hacer que el servidor seleccionado sea el _único_ disposible, borrando el resto de líneas, pero, por lo general, es una buena práctica tener varios, para el caso de que el primero se desconecte. Vea [Mirrors (Español)](/index.php/Mirrors_(Espa%C3%B1ol) "Mirrors (Español)") para obtener más información.

### Pacstrap

El script _pacstrap_ instalará el sistema base. Para compilar paquetes de [AUR](/index.php/AUR "AUR") o con [ABS](/index.php/ABS "ABS"), requerirá también el grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/).

No todas las herramientas presentes en el entorno live de instalación(ver [packages.both](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both)) son parte del grupo [base](https://www.archlinux.org/groups/x86_64/base/). Los paquetes deseados pueden ser [instalados](/index.php/Install "Install") más tarde con _pacman_, o añadiendo sus nombres después de la orden _pacstrap_.

```
# pacstrap -i /mnt base base-devel

```

El parámetro `-i` se utiliza para pedir confirmación antes de instalar los paquetes solicitados.

## Configurar el sistema base

### Fstab

Para identificar el sistema de archivos, genere un archivo [fstab (Español)](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)"). La opción `-U` identifica las UUID: vea [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming"). Si, en su lugar, prefiere utilizar etiquetas (_«labels»_), sustituya la opción `-U` por `-L`.

```
# genfstab -U /mnt > /mnt/etc/fstab

```

El archivo `fstab` siempre se debe revisar después de su generación, y modificarse en caso de advertirse errores.

### Chroot

Los pasos siguientes se realizan enjaulando el nuevo sistema mediante [change root](/index.php/Change_root "Change root"), esto es, cambiando la raíz:

```
# arch-chroot /mnt /bin/bash

```

### Idioma

El [Locale](/index.php/Locale "Locale") define el idioma que utiliza el sistema y otras consideraciones regionales tales como la denominación de la moneda, los números y los conjuntos de caracteres.

Los valores posibles están presentes en `/etc/locale.gen`. Descomente la línea `en_US.UTF-8 UTF-8`, así como otras localizaciones que pueda necesitar. Guarde el archivo y genere los nuevos valores locales:

```
# locale-gen

```

Cree el archivo `/etc/locale.conf`, con el parámetro `LANG` como _primera entrada_ sin comentar en `/etc/locale.gen`. :

 `/etc/locale.conf`  `LANG=_es_ES.UTF-8_` 

Si ha cambiado [la tipografía y el mapa de teclado](#Keyboard_layout) por defecto para la consola, cree el archivo `/etc/vconsole.conf` para hacer permanentes esos cambios en el nuevo sistema. Por ejemplo, si `de-latin1` es el valor inicialmente fijado con la orden _loadkeys_, y `lat9w-16` con _setfont_, asigne a `KEYMAP` y `FONT`, respectivamente, las variables correspondientes:

 `/etc/vconsole.conf` 

```
KEYMAP=_de-latin1_
FONT=_lat9w-16_
```

### Fecha y hora

Seleccione un [huso horario](/index.php/Time_(Espa%C3%B1ol)#Huso_horario "Time (Español)"):

```
# tzselect

```

Cree el enlace simbólico `/etc/localtime`, donde `Zona/Subzona` es el valor `TZ` de _tzselect_:

```
# ln -sf /usr/share/zoneinfo/_Zona_/_SubZona_ /etc/localtime

```

Se recomienda corregir la desviación horaria y establecer el estándar horario a UTC:

```
# hwclock --systohc --utc

```

Si hay otros sistemas operativos instalados en el equipo, se deben configurar en consecuencia. Véase [Time](/index.php/Time "Time") para más detalles.

### Initramfs

Dado que [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") se ha ejecutado cuando se instaló [linux](https://www.archlinux.org/packages/?name=linux) con _pacstrap_, la mayoría de los usuarios pueden omitir este paso y utilizar los valores por defecto proporcionados en `mkinitcpio.conf`.

Para configuraciones especiales, ajuste correctamente los [hooks](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") en `/etc/mkinitcpio.conf` y [regenere](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") la imagen initramfs:

```
# mkinitcpio -p linux

```

### Gestor de arranque

Vea [Boot loaders](/index.php/Boot_loaders "Boot loaders") para conocer las opciones y configuraciones disponibles. Las actualizaciones de [Microcode](/index.php/Microcode "Microcode") para las CPU de Intel también _deben_ ser configuradas después de instalar el gestor de arranque.

#### BIOS/MBR

Instale el paquete [grub](https://www.archlinux.org/packages/?name=grub). Para hacer que GRUB busque otros sistemas operativos instalados, instale también el paquete [os-prober](https://www.archlinux.org/packages/?name=os-prober):

```
# pacman -S grub os-prober

```

Instale el gestor de arranque en la _unidad_ donde se haya instalado Arch:

```
# grub-install --recheck _/dev/sda_

```

Genere automáticamente el archivo `grub.cfg`:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

Para más información consulte [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)").

#### UEFI/GPT

En este punto, se presume que la unidad de instalación está particionada con GPT, que se tiene una partición [EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") (tipo `EF00` con gdisk, formateada con FAT32) montada en `/boot`.

_bootctl_ es parte de systemd, y como tal, parte de la instalación del sistema base.

```
# bootctl install

```

Cree una entrada de arranque en `/boot/loader/entries/arch.conf`, sustituyendo `/dev/sda2` con la partición **root**:

 `/boot/loader/entries/arch.conf` 

```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=**/dev/sda2** rw
```

Modifique `/boot/loader/loader.conf` para seleccionar la entrada por defecto (sin el sufijo `.conf`):

 `/boot/loader/loader.conf` 

```
timeout 3
default arch
```

Vea [systemd-boot](/index.php/Systemd-boot "Systemd-boot") para más información.

### Configurar la conexión de red

Configure la conexión de red para el nuevo entorno recién instalado. El procedimiento es similar al seguido en [#Establecer una conexión a Internet](#Establecer_una_conexi.C3.B3n_a_Internet), con la excepción de que las modificaciones quedarán permanentes para los subsiguientes arranques. Seleccione **un** demonio para manejar las conexiones de red.

#### Nombre del equipo

Establezca el [hostname](/index.php/Hostname "Hostname") que prefiera:

 `/etc/hostname`  `_myhostname_` 

Es recomendable añadir una entrada en `/etc/hosts` con el mismo nombre de equipo que en `localhost`. Vea [Network configuration#Local network hostname resolution](/index.php/Network_configuration#Local_network_hostname_resolution "Network configuration").

#### Red cableada

Cuando solo necesite una única conexión de red cableada, active el servicio [dhcpcd](/index.php/Dhcpcd "Dhcpcd"):

```
# systemctl enable dhcpcd@_nombre_interfaz_.service

```

Donde `_nombre_interfaz_` se refiere al [nombre del dispositivo](/index.php/Network_configuration#Device_names "Network configuration") de ethernet.

Vea [Network configuration#Configure the IP address](/index.php/Network_configuration#Configure_the_IP_address "Network configuration") para conocer otros métodos disponibles.

#### Red inalámbrica

Instale [iw](https://www.archlinux.org/packages/?name=iw), [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant), y (para _wifi-menu_) [dialog](https://www.archlinux.org/packages/?name=dialog):

```
# pacman -S iw wpa_supplicant dialog

```

Adicionalmente, también pueden ser necesarios los [paquetes de firmware](/index.php/Wireless#Installing_driver.2Ffirmware "Wireless").

Si ha utilizado _wifi-menu_ conforme a lo dispuesto en [Conexión a redes inalámbricas](#Establecer_una_conexi.C3.B3n_a_Internet) del entorno live, repita **posteriormente** dichos pasos para finalizar la instalación y reinicie, para evitar conflictos con otros procesos en curso.

Vea [Netctl](/index.php/Netctl "Netctl") y [Wireless#Wireless management](/index.php/Wireless#Wireless_management "Wireless") para obtener más información.

## Desmontar las particiones y reiniciar

Salga del entorno chroot:

```
# exit

```

Las particiones se desmontan automáticamente por _systemd_ durante el apagado. No obstante, puede hacerlo de forma manual como medida de seguridad:

```
# umount -R /mnt

```

Si la partición está «busy» (_ocupada_), puede encontrar la causa con [fuser](https://en.wikipedia.org/wiki/fuser_(Unix) "wikipedia:fuser (Unix)"). Reinicie el equipo:

```
# reboot

```

Retire el soporte de instalación, o puede que arranque de nuevo desde el mismo. Puede acceder a su sistema recién instalado como _root_, utilizando la contraseña especificada con _passwd_.

## Posinstalación

Su nuevo sistema base Arch Linux es ahora un entorno GNU/Linux funcional listo para ser integrado a sus necesidades o propósitos. A partir de aquí es _altamente_ aconsejable que lea [General recommendations (Español)](/index.php/General_recommendations_(Espa%C3%B1ol) "General recommendations (Español)"), especialmente las dos primera secciones. El resto de secciones del artículo proporcionan enlaces para conocer tutoriales posinstalación, como la configuración de una interfaz gráfica de usuario, el sonido o el panel táctil.

Para obtener una lista de aplicaciones que pueden serle de interés, consulte [List of applications (Español)](/index.php/List_of_applications_(Espa%C3%B1ol) "List of applications (Español)").

Retrieved from "[https://wiki.archlinux.org/index.php?title=Beginners%27_guide_(Español)&oldid=411522](https://wiki.archlinux.org/index.php?title=Beginners%27_guide_(Español)&oldid=411522)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Getting and installing Arch (Español)](/index.php/Category:Getting_and_installing_Arch_(Espa%C3%B1ol) "Category:Getting and installing Arch (Español)")