**Estado de la traducción**
Este artículo es una traducción de [LVM](/index.php/LVM "LVM"), revisada por última vez el **2019-01-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=LVM&diff=0&oldid=561890) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Software RAID and LVM](/index.php/Software_RAID_and_LVM "Software RAID and LVM")
*   [Dm-crypt/Encrypting an Entire System (Español)#LVM sobre LUKS](/index.php/Dm-crypt/Encrypting_an_Entire_System_(Espa%C3%B1ol)#LVM_sobre_LUKS "Dm-crypt/Encrypting an Entire System (Español)")
*   [Dm-crypt/Encrypting an Entire System (Español)#LUKS sobre LVM](/index.php/Dm-crypt/Encrypting_an_Entire_System_(Espa%C3%B1ol)#LUKS_sobre_LVM "Dm-crypt/Encrypting an Entire System (Español)")
*   [Resizing LVM-on-LUKS](/index.php/Resizing_LVM-on-LUKS "Resizing LVM-on-LUKS")
*   [Create root filesystem snapshots with LVM](/index.php/Create_root_filesystem_snapshots_with_LVM "Create root filesystem snapshots with LVM")

De [Wikipedia:Logical Volume Manager (Linux)](https://en.wikipedia.org/wiki/Logical_Volume_Manager_(Linux) "wikipedia:Logical Volume Manager (Linux)"):

	LVM es un [gestor de volúmenes lógicos](https://en.wikipedia.org/wiki/logical_volume_management "wikipedia:logical volume management") para el [kernel de Linux](https://en.wikipedia.org/wiki/N%C3%BAcleo_Linux "wikipedia:Núcleo Linux"), que gestiona unidades de disco y dispositivos similares de almacenamiento masivo.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Bloques para construir LVM](#Bloques_para_construir_LVM)
*   [2 Ventajas](#Ventajas)
*   [3 Desventajas](#Desventajas)
*   [4 Primeros pasos](#Primeros_pasos)
*   [5 Instalar Arch Linux sobre LVM](#Instalar_Arch_Linux_sobre_LVM)
    *   [5.1 Crear particiones](#Crear_particiones)
    *   [5.2 Crear volúmenes físicos](#Crear_volúmenes_físicos)
    *   [5.3 Crear grupo de volúmenes](#Crear_grupo_de_volúmenes)
    *   [5.4 Crear en un solo paso](#Crear_en_un_solo_paso)
    *   [5.5 Crear volúmenes lógicos](#Crear_volúmenes_lógicos)
    *   [5.6 Crear sistemas de archivos y montar los volúmenes lógicos](#Crear_sistemas_de_archivos_y_montar_los_volúmenes_lógicos)
    *   [5.7 Configurar mkinitcpio](#Configurar_mkinitcpio)
    *   [5.8 Opciones del kernel](#Opciones_del_kernel)
*   [6 Operaciones sobre los volúmenes](#Operaciones_sobre_los_volúmenes)
    *   [6.1 Opciones avanzadas](#Opciones_avanzadas)
    *   [6.2 Redimensionar volúmenes](#Redimensionar_volúmenes)
        *   [6.2.1 Volúmenes físicos](#Volúmenes_físicos)
            *   [6.2.1.1 Agrandar](#Agrandar)
            *   [6.2.1.2 Encoger](#Encoger)
                *   [6.2.1.2.1 Mover extensiones físicas](#Mover_extensiones_físicas)
                *   [6.2.1.2.2 Redimensionar volumen físico](#Redimensionar_volumen_físico)
                *   [6.2.1.2.3 Redimensionar partición](#Redimensionar_partición)
        *   [6.2.2 Volúmenes lógicos](#Volúmenes_lógicos)
            *   [6.2.2.1 Cambiar el tamaño del volumen lógico y del sistema de archivos a la vez](#Cambiar_el_tamaño_del_volumen_lógico_y_del_sistema_de_archivos_a_la_vez)
            *   [6.2.2.2 Cambiar el tamaño del volumen lógico y del sistema de archivos separadamente](#Cambiar_el_tamaño_del_volumen_lógico_y_del_sistema_de_archivos_separadamente)
    *   [6.3 Renombrar volúmenes](#Renombrar_volúmenes)
        *   [6.3.1 Renombrar un grupo de volúmenes](#Renombrar_un_grupo_de_volúmenes)
        *   [6.3.2 Renombrar volúmenes lógicos](#Renombrar_volúmenes_lógicos)
    *   [6.4 Eliminar volúmenes lógicos](#Eliminar_volúmenes_lógicos)
    *   [6.5 Agregar un volumen físico a un grupo de volúmenes](#Agregar_un_volumen_físico_a_un_grupo_de_volúmenes)
    *   [6.6 Eliminar una partición de un grupo de volúmenes](#Eliminar_una_partición_de_un_grupo_de_volúmenes)
    *   [6.7 Desactivar un grupo de volúmenes](#Desactivar_un_grupo_de_volúmenes)
*   [7 Tipos de volúmenes lógicos](#Tipos_de_volúmenes_lógicos)
    *   [7.1 Instantáneas/Snapshots](#Instantáneas/Snapshots)
        *   [7.1.1 Configuración](#Configuración)
    *   [7.2 La memoria caché de LVM](#La_memoria_caché_de_LVM)
        *   [7.2.1 Crear la memoria caché](#Crear_la_memoria_caché)
        *   [7.2.2 Eliminar la memoria caché](#Eliminar_la_memoria_caché)
    *   [7.3 RAID](#RAID)
        *   [7.3.1 Configurar RAID](#Configurar_RAID)
        *   [7.3.2 Configurar mkinitcpio para RAID](#Configurar_mkinitcpio_para_RAID)
*   [8 Configuración gráfica](#Configuración_gráfica)
*   [9 Solución de problemas](#Solución_de_problemas)
    *   [9.1 Problemas de arranque/apagado debido a lvmetad desactivado](#Problemas_de_arranque/apagado_debido_a_lvmetad_desactivado)
    *   [9.2 Las órdenes LVM no funcionan](#Las_órdenes_LVM_no_funcionan)
    *   [9.3 No se muestran los volúmenes lógicos](#No_se_muestran_los_volúmenes_lógicos)
    *   [9.4 LVM sobre un medio extraíble](#LVM_sobre_un_medio_extraíble)
    *   [9.5 Al redimensionar un volumen lógico contiguo falla](#Al_redimensionar_un_volumen_lógico_contiguo_falla)
    *   [9.6 La orden «grub-mkconfig» informa del error «unknown filesystem»](#La_orden_«grub-mkconfig»_informa_del_error_«unknown_filesystem»)
    *   [9.7 Dispositivo de volumen raíz aprovisionado Getting started para agotar tiempo de espera](#Dispositivo_de_volumen_raíz_aprovisionado_Getting_started_para_agotar_tiempo_de_espera)
    *   [9.8 Demora al apagar](#Demora_al_apagar)
*   [10 Véase también](#Véase_también)

## Bloques para construir LVM

*Logical Volume Management* (en adelante LVM, siglas en inglés) hace uso de la función [device-mapper](http://sources.redhat.com/dm/) del kernel de Linux para proporcionar un sistema de particiones independientes de la estructura subyacente del disco. Con LVM es posible crear un espacio de almacenamiento abstracto así como distintas «particiones virtuales», por lo que es más fácil de [agrandar/encoger](#Redimensionar_volúmenes) particiones (siempre sujeto a posibles limitaciones de su sistema de archivos).

Las particiones virtuales permiten añadir/eliminar particiones sin tener que preocuparse acerca de si se tiene suficiente espacio contiguo en un disco concreto, ni quedar atrapado en el fdisking de un disco en uso (y preguntándose si el kernel está utilizando una tabla de particiones vieja o nueva), ni tener que mover otras particiones en el camino. Esto es un asunto que afecta estrictamente a la facilidad de gestión: LVM no proporciona ninguna seguridad.

Los bloques básicos que construyen LVM son:

	Physical volume —*volúmenes físicos*— (en adelante PV)

	Nodo de dispositivo de bloque de Unix, utilizable para almacenamiento por LVM. Ejemplos: un disco duro, una [partición](/index.php/Partition "Partition") MBR o GPT, un archivo loopback, un dispositivo mapeador de dispositivos (por ejemplo, [dm-crypt (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)")). Alberga un encabezado LVM.

	Volume group —*grupo de volúmenes*— (en adelante VG)

	Grupo de volúmenes físicos que sirve de contenedor para volúmenes lógicos. Las extensiones físicas se asignan desde un grupo de volúmenes para un volumen lógico.

	Logical volume —*volúmenes lógicos*— (en adelante LV)

	«Partición virtual/lógica» que reside en un grupo de volúmenes y está compuesta de extensiones físicas. Los volúmenes lógicos son dispositivos de bloque de Unix análogos a las particiones físicas, por ejemplo, se pueden formatear directamente con un [sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)").

	Physical extent —*extensiones físicas*— (en adelante PE)

	La extensión contigua más pequeña (por defecto 4 MiB) en el volumen físico que se puede asignar a un volumen lógico. Piense en las extensiones físicas como partes de los volúmenes físicos que pueden asignarse a cualquier volúmen lógico.

Ejemplo:

```
 **Discos físicos**

  Disco1 (/dev/sda):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
    |Partición1 50 GiB (Volumen físico) |Partición2 80 GiB (Volumen físico)   |
    |/dev/sda1                          |/dev/sda2                            |
    |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _  _ _ |

  Disco2 (/dev/sdb):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
    |Partición1 120 GiB (Volumen físico)                |
    |/dev/sdb1                                          |
    | _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ __ _ _|

```

```
**Volúmenes lógicos LVM**

  Grupo de volumen1 (/dev/MyStorage/ = /dev/sda1 + /dev/sda2 + /dev/sdb1):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
    |Volumen lógico1 15 GiB  |Volumen lógico2 35 GiB      |Volumen lógico3 200 GiB              |
    |/dev/MyVolGroup/rootvol |/dev/MyVolGroup/homevol     |/dev/MyVolGroup/mediavol             |
    |_ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|

```

## Ventajas

LVM le da más flexibilidad que la simple partición de un disco duro para:

*   Poder utilizar cualquier número de discos como un gran disco.
*   Tener volúmenes lógicos estirados sobre varios discos.
*   Crear pequeños volúmenes lógicos y cambiar su tamaño «dinámicamente», cuando se llenen.
*   Cambiar el tamaño de los volúmenes lógicos sin importar su orden en el disco. No depende de la posición del volumen lógico dentro del grupo de volúmenes, ni hay necesidad de asegurar el espacio disponible circundante.
*   Redimensionar/crear/borrar el tamaño de los volúmenes lógicos y físicos en línea. Los sistemas de archivos en ellos todavía tendrán que ser redimensionados, pero algunos (como ext4) apoyan el cambio de tamaño en línea.
*   Migración en línea/vivo de volumenes lógicos, siendo utilizado por los servicios para diferentes discos sin tener que reiniciar los servicios.
*   Realizar instantáneas que permiten hacer copias de respaldo del sistema de archivos, mientras se mantiene el tiempo de inactividad del servicio a un mínimo.
*   Soporte para albergar distintos mapeadores de dispositivos, incluido el cifrado del sistema de archivos transparente y almacenamiento en caché de los datos de uso frecuente. Esto permite crear un sistema con (uno o más) discos físicos (cifrados con LUKS) y [LVM en la parte superior](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#LVM_sobre_LUKS "Dm-crypt/Encrypting an entire system (Español)") para permitir el cambio de tamaño y la administración de volúmenes separados (por ejemplo, para `/`, `/home`, `/backup`, etc.) sin la molestia de introducir una clave varias veces al arrancar.

## Desventajas

*   Los pasos adicionales en la configuración del sistema, que lo hace más complicado.
*   Si tiene un arranque dual, tenga en cuenta que Windows no es compatible con LVM; no podrá acceder a ninguna partición LVM desde Windows.

## Primeros pasos

Asegúrese de que el paquete [lvm2](https://www.archlinux.org/packages/?name=lvm2) está [instalado](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalación_de_paquetes "Help:Reading (Español)").

## Instalar Arch Linux sobre LVM

Se deben crear los volúmenes LVM entre el [particionado](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)") y el [formateado](/index.php/File_systems_(Espa%C3%B1ol)#Crear_un_sistema_de_archivos "File systems (Español)") durante el procedimiento de instalación. En lugar de dar formato directamente a una partición para que sea su sistema de archivos root, esta operación se hará dentro de un volumen lógico (LV).

Remítase primero a «Primeros pasos».

He aquí un breve resumen:

*   Cree la partición(s) donde residirá su volumen físico (PV). Ajuste el tipo de partición para «Linux LVM», que es 8e si usa MBR y 8e00 para GPT.
*   Cree los volúmenes físicos (PV). Si se tiene un disco lo mejor es simplemente crear un volumen físico en una partición grande. Si tiene varios discos se pueden crear particiones en cada uno de ellos y crear un volumen físico en cada partición.
*   Cree el grupo de volúmenes (VG) y asocie todos los volúmenes físicos (PV) al mismo.
*   Cree volúmenes lógicos (LV) dentro de su grupo de volúmenes (VG).
*   Continúe con el paso «Formatear las particiones» de [Installation guide (Español)#Formatear las particiones](/index.php/Installation_guide_(Espa%C3%B1ol)#Formatear_las_particiones "Installation guide (Español)").
*   Cuando llegue al paso «Crear entorno inicial ramdisk» en la guía de instalación, agregue el hook `lvm` a `/etc/mkinitcpio.conf` (vea detalles más abajo ).

**Advertencia:** `/boot` no puede residir en LVM cuando se utiliza un gestor de arranque que no soporta LVM. Puede crear una partición `/boot` separada y formatearla directamente. Que se conozca, solo [GRUB](/index.php/GRUB "GRUB") soporta LVM.

### Crear particiones

Es necesario [particionar](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)") el dispositivo antes de configurar LVM.

Cree las particiones:

*   Si utiliza la tabla de particionado Master Boot Record, ajuste el [ID del tipo de partición](https://en.wikipedia.org/wiki/Partition_type "wikipedia:Partition type") a `8e` (tipo de partición `Linux LVM` en *fdisk*).
*   Si utiliza la tabla de particionado GUID, ajuste el [ID del tipo de partición](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table") a `E6D6D379-F507-44C2-A23C-238F2A3DF928` (tipo de partición `Linux LVM` en *fdisk* y `8e00` en *gdisk*).

### Crear volúmenes físicos

Para listar todos los dispositivos capaces de ser utilizados como un volumen físico, lance:

```
# lvmdiskscan

```

**Advertencia:** asegúrese de indicar bien el dispositivo correcto, o de lo contrario la ejecución de las órdenes de abajo se traducirán en la perdidad de sus datos.

Cree un volumen físico en ellos:

```
# pvcreate *DISPOSITIVO*

```

Esta orden crea una cabecera en cada dispositivo para que se pueda utilizar para LVM. Tal como se define en [#Bloques para construir LVM](#Bloques_para_construir_LVM), el *DISPOSITIVO* puede ser un disco (por ejemplo, `/dev/sda`), una partición (por ejemplo, `/dev/sda2`) o un dispositivo Loopback.

Por ejemplo:

```
# pvcreate /dev/sda2

```

Puede hacer un seguimiento de los volúmenes físicos creados con:

```
# pvdisplay

```

**Nota:** si se utiliza un disco SSD sin particionarlo primero, utilice `pvcreate --dataalignment 1m /dev/sda` (para el tamaño de bloque de borrado de < 1MiB), véase por ejemplo [esto](http://serverfault.com/questions/356534/ssd-erase-block-size-lvm-pv-on-raw-device-alignment).

### Crear grupo de volúmenes

El siguiente paso será crear un grupo de volúmenes sobre el volumen físico:

Lo primero que se necesita es crear un grupo de volúmenes sobre uno de los volúmenes físicos:

```
# vgcreate <*grupo_de_volúmenes*> <*volumen_físico*>

```

Por ejemplo:

```
# vgcreate VolGroup00 /dev/sda2

```

A continuación, puede añadir a dicho grupo de volúmenes tantos volúmenes físicos como desee tener en el mismo (a modo de una sola unidad):

```
# vgextend <*grupo_de_volúmenes*> <*volumen_físico*>
# vgextend <*grupo_de_volúmenes*> <*otro_volumen_físico*>
# ...

```

Por ejemplo:

```
# vgextend VolGroup00 /dev/sdb1
# vgextend VolGroup00 /dev/sdc

```

Puede hacer un seguimiento de cómo su grupo de volúmenes ha crecido con:

```
# vgdisplay

```

**Nota:** se pueden crear más de un grupo de volúmenes si es necesario, pero entonces no tendrá todo su almacenamiento presente como si fuera un disco.

### Crear en un solo paso

LVM le permite la creación de un grupo de volúmenes sobre varios volúmenes físicos en un solo paso. Por ejemplo, para crear el grupo VolGroup00 con los tres dispositivos mencionados anteriormente, puede ejecutar:

```
# vgcreate VolGroup00 /dev/sda2 /dev/sdb1 /dev/sdc

```

Esta orden configurará primero las tres particiones como volúmenes físicos (si es necesario) y luego creará el grupo de volúmenes con los tres volúmenes físicos. La orden le advertirá si detecta un sistema de archivos existente en cualquiera de los dispositivos.

### Crear volúmenes lógicos

**Sugerencia:** si desea utilizar instantáneas, volúmenes lógicos para almacenamiento caché, volúmenes lógicos de aprovisionamiento ligero o RAID, consulte [#Tipos de volúmenes lógicos](#Tipos_de_volúmenes_lógicos).

Ahora necesitaremos crear volúmenes lógicos en el mencionado grupo de volúmenes. Para ello debe utilizar la siguiente orden, proporcionándole como parámetros, su tamaño (-L), el grupo de volúmenes al que pertenecerá, y el nombre (-n) que queremos darle al nuevo volumen lógico:

```
# lvcreate -L <*tamaño*> <*grupo_de_volúmenes*> -n <*volumen_lógico*>

```

Por ejemplo:

```
# lvcreate -L 10G VolGroup00 -n lvolhome

```

Luego, podrá acceder al nuevo volumen lógico creado con `/dev/VolGroup00/lvolhome`. Igual que sucede con los grupos de volúmenes, puede ponerle el nombre que desee al volumen lógico cuando lo crea, salvo algunas excepciones enumeradas en [lvm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvm.8#VALID_NAMES).

También puede especificar uno o más volúmenes físicos para limitar donde quiere que LVM asigne los datos. Por ejemplo, es posible que desee crear un volumen lógico para el sistema de archivos raíz en SSD (si es pequeño), y el volumen de su home en una unidad mecánica más grande y lenta. Tan solo tiene que añadir el dispositivo del volumen físico a la línea de órdenes, por ejemplo:

```
# lvcreate -L 10G VolGroup00 -n lvolhome /dev/sdc1

```

Si desea ocupar todo el espacio libre que queda del grupo de volúmenes, utilice la siguiente orden:

```
# lvcreate -l +100%FREE  <*grupo_de_volúmenes*> -n <*volumen_lógico*>

```

Puede hacer un seguimiento de los volúmenes lógicos creados con:

```
# lvdisplay

```

**Nota:** es posible que deba cargar el módulo del kernel *device-mapper* (`modprobe dm_mod`) para que las órdenes anteriores puedan tener éxito.

**Sugerencia:** se puede comenzar creando volúmenes lógicos relativamente pequeños y ampliarlos más adelante si fuera necesario. Para simplificar, deje un poco de espacio libre en el grupo de volúmenes para tener margen para su expansión.

### Crear sistemas de archivos y montar los volúmenes lógicos

Sus volúmenes lógicos deberian encontrarse en `/dev/NombredelGrupodedeVolúmenes/`. De no encontrarse, utilice la siguiente orden para cargar el modulo que crea nodos de dispositivos y hacer que los grupos de volúmenes estén disponibles:

```
# modprobe dm-mod
# vgscan
# vgchange -ay

```

Ahora puede crear el sistema de archivos en los volúmenes lógicos, y montarlos como particiones normales (si está instalando Arch, remítase a [montar las particiones](/index.php/File_systems#Mount_a_file_system "File systems") para obtener información adicional):

```
# mkfs.<*tipo_sistema_archivos*> /dev/<*grupo_de_volúmenes*>/<*volumen_lógico*>
# mount /dev/<*grupo_de_volúmenes*>/<*volumen_lógico*> /<*punto_de_montaje*>

```

Por ejemplo:

```
# mkfs.ext4 /dev/VolGroup00/lvolhome
# mount /dev/VolGroup00/lvolhome /home

```

**Advertencia:** al elegir los puntos de montaje, solo tiene que seleccionar los volúmenes lógicos recién creados (utilice: `/dev/Volgroup00/lvolhome`). **No** seleccione las particiones reales sobre las que se crearon los volúmenes lógicos (por tanto, no utilice: `/dev/sda2`).

### Configurar mkinitcpio

En caso de que su sistema de archivos raíz esté sobre LVM, tendrá que activar los hooks de [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") apropiados, de lo contrario su sistema podría no arrancar. Active:

*   `udev` y `lvm2` predeterminados para initramfs basado en busybox.
*   `systemd` y `sd-lvm2` para initramfs basado en systemd.

`udev` está presente de forma predeterminada. Edite el archivo e inserte `lvm2` entre `block` y `filesystems` como sigue:

 `/etc/mkinitcpio.conf`  `HOOKS=(base **udev** ... block **lvm2** filesystems)` 

Para initramfs basado en systemd :

 `/etc/mkinitcpio.conf`  `HOOKS=(base **systemd** ... block **sd-lvm2** filesystems)` 

Después, puede continuar con las instrucciones de instalación normales en el paso [crear una imagen ramdisk inicial](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Creación_de_la_imagen_y_activación "Mkinitcpio (Español)").

**Sugerencia:**

*   Los hooks `lvm2` y `sd-lvm2` serán instalados por el paquete [lvm2](https://www.archlinux.org/packages/?name=lvm2), no por [mkinitcpio](https://www.archlinux.org/packages/?name=mkinitcpio). Si está ejecutando *mkinitcpio* en un entrono *arch-chroot* para una nueva instalación, [lvm2](https://www.archlinux.org/packages/?name=lvm2) debe estar instalado dentro del entorno *arch-chroot* para *mkinitcpio* con el fin de encontrar el hook `lvm2` o `sd-lvm2`. Si [lvm2](https://www.archlinux.org/packages/?name=lvm2) se instala fuera del entorno *arch-chroot*, *mkinitcpio* generará la salida `Error: Hook 'lvm2' cannot be found`.
*   Si su sistema de archivos raíz está en LVM sobre RAID, consulte [#Configurar mkinitcpio para RAID](#Configurar_mkinitcpio_para_RAID).

### Opciones del kernel

Si el sistema de archivos raíz reside en un volumen lógico, el [Kernel parameters (Español)](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") `root=` debe apuntar al dispositivo mapeado, por ejemplo `/dev/*<nombre_grupodevolúmenes>*/*<nombre_volumenlógico>*`.

También podría ser necesario `dolvm`.

## Operaciones sobre los volúmenes

### Opciones avanzadas

Puede restringir los volúmenes que se activan de forma automática mediante el establecimiento de la variable `auto_activation_volume_list` en el archivo `/etc/lvm/lvm.conf`. En caso de duda, deje esta opción comentada.

### Redimensionar volúmenes

#### Volúmenes físicos

Después de aumentar o antes de reducir el tamaño de un dispositivo que tiene sobre él un volumen físico, necesita aumentar o reducir el tamaño del volumen físico mediante `pvresize`.

##### Agrandar

Para ampliar el volumen físico existente sobre el dispositivo `/dev/sda1`, después de aumentar dicha [partición](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)"), ejecute:

```
# pvresize /dev/sda1

```

Esto detectará automáticamente el nuevo tamaño del dispositivo y extenderá el volumen físico a su máximo.

**Nota:** esta orden se puede ejecutar mientras el volumen está en línea.

##### Encoger

Para reducir un volumen físico antes de reducir el dispositivo subyacente, agregue el parámetro `--setphysicalvolumesize *<tamaño>*` a la orden, *por ejemplo*:

```
# pvresize --setphysicalvolumesize 40G /dev/sda1

```

La orden anterior puede arrojar el siguiente error:

```
 /dev/sda1: cannot resize to 25599 extents as later ones are allocated.
 0 physical volume(s) resized / 1 physical volume(s) not resized

```

De hecho `pvresize` se negará a reducir un volumen físico si tiene asignadas extensiones adyacentes a lo que sería su nuevo final. Se tiene que ejecutar [pvmove](#Mover_extensiones_físicas) de antemano para reubicar estas extensiones en el grupo de volúmenes a otro lugar, si no hay suficiente espacio libre.

###### Mover extensiones físicas

Antes de mover extensiones libres al final del volumen, se debe ejecutar `# pvdisplay -v -m` para ver los segmentos físicos. En el siguiente ejemplo, hay un volumen físico sobre `/dev/sdd1`, un grupo de volumen `vg1` y un volumen lógico `backup`.

 `# pvdisplay -v -m` 
```
    Finding all volume groups.
    Using physical volume(s) on command line.
  --- Physical volume ---
  PV Name               /dev/sdd1
  VG Name               vg1
  PV Size               1.52 TiB / not usable 1.97 MiB
  Allocatable           yes 
  PE Size               4.00 MiB
  Total PE              399669
  Free PE               153600
  Allocated PE          246069
  PV UUID               MR9J0X-zQB4-wi3k-EnaV-5ksf-hN1P-Jkm5mW

  --- Physical Segments ---
  Physical extent 0 to 153600:
    FREE
  Physical extent 153601 to 307199:
    Logical volume	/dev/vg1/backup
    Logical extents	1 to 153599
  Physical extent 307200 to 307200:
    FREE
  Physical extent 307201 to 399668:
    Logical volume	/dev/vg1/backup
    Logical extents	153601 to 246068

```

Se puede observar que el espacio FREE (LIBRE) se intercala por todo el volumen. Para reducir el tamaño del volumen físico, primero tenemos que mover todos los segmentos utilizados al comienzo.

Aquí, el primer segmento libre es desde 0 a 153.600, lo cual nos deja con 153.601 extensiones libres. Ahora podemos mover este número de segmentos desde la última extensión física de la primera. La orden sería así:

 `# pvmove --alloc anywhere /dev/sdd1:307201-399668 /dev/sdd1:0-92467` 
```
/dev/sdd1: Moved: 0.1 %
/dev/sdd1: Moved: 0.2 %
...
/dev/sdd1: Moved: 99.9 %
/dev/sdd1: Moved: 100,0%

```

**Nota:**

*   Esta orden indica que se muevan 399.668 - 307.201 + 1 = 92.468 extensiones físicas **desde** el último segmento **al** primer segmento. Esto es posible ya que el primer segmento cerrado LIBRE es de 153.600 extensiones físicas, que puede contener las 92.467 - 0 + 1 = 92.468 extensiones físicas trasladadas.
*   La opción `--alloc anywhere` se utiliza cuando movemos extensiones físicas dentro de la misma partición. En caso de particiones diferentes, la orden sería algo como esto: `# pvmove /dev/sdb1:1000-1999 /dev/sdc1:0-999` 
*   El traslado toma su tiempo (una/dos horas) en el caso de gran tamaño. Puede ser una buena idea ejecutar esta orden en una sesión [Tmux](/index.php/Tmux "Tmux") o [GNU Screen](/index.php/GNU_Screen "GNU Screen"). Cualquier parada no deseada del proceso puede ser fatal.
*   Una vez finalizada la operación, ejecute [fsck](/index.php/Fsck "Fsck") para asegurarse de que su sistema de archivos es válido.

###### Redimensionar volumen físico

Una vez que todos sus segmentos físicos libres estén en las últimas extensiones físicas, ejecute `vgdisplay` y vea su extensión física libre.

Entonces, podrá ejecutar de nuevo la orden:

```
# pvresize --setphysicalvolumesize *tamaño* *VolumenFísico*

```

Vea el resultado:

 `# pvs` 
```
  PV         VG   Fmt  Attr PSize    PFree 
  /dev/sdd1  vg1  lvm2 a--     1t     500g

```

###### Redimensionar partición

Último paso, es necesario reducir la partición con su [herramienta de particionado](/index.php/Partitioning#Partitioning_tools "Partitioning") favorita.

#### Volúmenes lógicos

**Nota:** [lvresize(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvresize.8) proporciona, más o menos, las mismas opciones que las órdenes especializadas de [lvextend(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvextend.8) y [lvreduce(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvreduce.8), al tiempo que permite hacer ambos tipos de operaciones. A pesar de esto, todos las utilidades ofrecen una opción `-r, --resizefs` que permite cambiar el tamaño del sistema de archivos junto con el volumen lógico, mediante `fsadm(8)` (que soporta *ext2*, [ext3](/index.php/Ext3 "Ext3"), [ext4](/index.php/Ext4 "Ext4"), *ReiserFS* y [XFS](/index.php/XFS "XFS")). Por lo tanto, puede ser más fácil simplemente utilizar `lvresize` para ambas operaciones y utilizar `--resizefs` para simplificar un poco las cosas, excepto si tiene necesidades específicas o desea tener un control total sobre el proceso.

**Advertencia:** si bien la ampliación de un sistema de archivos, a menudo, puede hacerse en línea (*es decir* mientras está montado), incluso para la partición raíz, la reducción, casi siempre, requerirá primero desmontar el sistema de archivos para evitar pérdida de datos. Asegúrese de que su sistema de archivos sea compatible con lo que está tratando de hacer.

##### Cambiar el tamaño del volumen lógico y del sistema de archivos a la vez

**Nota:** solo los [sistemas de archivos](/index.php/File_systems "File systems") *ext2*, [ext3](/index.php/Ext3 "Ext3"), [ext4](/index.php/Ext4 "Ext4"), *ReiserFS* y [XFS](/index.php/XFS "XFS") son ​​compatibles. Para un tipo diferente de sistema de archivos, consulte [#Cambiar el tamaño del volumen lógico y del sistema de archivos separadamente](#Cambiar_el_tamaño_del_volumen_lógico_y_del_sistema_de_archivos_separadamente).

Extienda el volumen lógico `mediavol` del grupo de volúmenes `MyVolGroup` en 10 GiB y redimensione *a la vez* su sistema de archivos :

```
# lvresize -L +10G --resizefs MyVolGroup/mediavol

```

Establezca el tamaño del volumen lógico `mediavol` presente en `MyVolGroup` a 15 GiB y redimensione *a la vez* su sistema de archivos:

```
# lvresize -L 15G --resizefs MyVolGroup/mediavol

```

Si desea ocupar todo el espacio libre con un grupo de volúmenes, utilice la siguiente orden:

```
# lvresize -l +100%FREE --resizefs MyVolGroup/mediavol

```

Consulte [lvresize(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvresize.8) para obtener más opciones detalladas.

##### Cambiar el tamaño del volumen lógico y del sistema de archivos separadamente

Para los sistemas de archivos no admitidos por [fsadm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fsadm.8) necesitará utilizar la [utilidad apropiada](/index.php/File_systems#Types_of_file_systems "File systems") para cambiar el tamaño del sistema de archivos antes de reducir el volumen lógico o después de expandirlo.

Para extender el volumen lógico `mediavol` dentro del grupo de volúmenes `MyVolGroup` en 2 GiB *sin* tocar su sistema de archivos:

```
# lvresize -L +2G MyVolGroup/mediavol

```

Ahora expanda el sistema de archivos ([ext4](/index.php/Ext4 "Ext4") en este ejemplo) al tamaño máximo del volumen lógico subyacente:

```
# resize2fs /dev/MyVolGroup/mediavol

```

Para reducir el tamaño del volumen lógico `mediavol` en `MyVolGroup` en 500 MiB, primero calcule el tamaño del sistema de archivos resultante y reduzca el tamaño del sistema de archivos ([ext4](/index.php/Ext4 "Ext4") en este ejemplo) al nuevo tamaño:

```
# resize2fs /dev/MyVolGroup/mediavol *NewSize*

```

Una vez encogido el sistema de archivos, reduzca el tamaño del volumen lógico:

```
# lvresize -L -500M MyVolGroup/mediavol

```

Consulte [lvresize(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvresize.8) para obtener más opciones detalladas.

### Renombrar volúmenes

#### Renombrar un grupo de volúmenes

Utilice la orden [vgrename(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vgrename.8) para cambiar el nombre de un grupo de volúmenes existente.

Cualquiera de las siguientes órdenes cambia el nombre del grupo de volúmenes existente `vg02` a `my_volume_group`

```
# vgrename /dev/vg02 /dev/my_volume_group

```

```
# vgrename vg02 my_volume_group

```

#### Renombrar volúmenes lógicos

Para cambiar el nombre de un volumen lógico existente, utilice la orden [lvrename(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvrename.8).

Cualquiera de las siguientes órdenes cambia el nombre del volumen lógico `lvold` presente en el grupo de volúmenes `vg02` a `lvnew`.

```
# lvrename /dev/vg02/lvold /dev/vg02/lvnew

```

```
# lvrename vg02 lvold lvnew

```

### Eliminar volúmenes lógicos

**Advertencia:** antes de quitar un volumen lógico, asegúrese de mover todos los datos que desee conservar a otro lugar; ¡de lo contrario, se perderán!

En primer lugar, averigüe el nombre del volumen lógico que desea eliminar. Se puede obtener una lista de todos los volúmenes lógicos instalados en el sistema con:

```
# lvs

```

A continuación, busque el punto de montaje del volumen lógico elegido, con:

```
$ lsblk

```

Ahora, desmonte el sistema de archivos del volumen lógico:

```
# umount /<*punto_montaje*>

```

Por último, elimine el volumen lógico:

```
# lvremove <*grupo_volúmenes*>/<*volumen_lógico*>

```

Por ejemplo:

```
# lvremove VolGroup00/lvolhome

```

Confirme la operación escribiendo `y`.

No se olvide actualizar el archivo `/etc/fstab`.

Se puede verificar la eliminación del volumen lógico escribiendo `lvs` con privilegios de root de nuevo (vea el primer paso de esta sección).

### Agregar un volumen físico a un grupo de volúmenes

En primer lugar, cree un nuevo volumen físico en el dispositivo de bloque que desea usar, y luego intégrelo en su grupo de volúmenes:

```
# pvcreate /dev/sdb1
# vgextend VolGroup00 /dev/sdb1

```

Por supuesto, esto aumentará el número total de extensiones físicas en el grupo de volúmenes, que podrá asignar a los volúmenes lógicos como mejor le parezca.

**Nota:** se considera una buena práctica tener una [tabla de particiones](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)") en el soporte de almacenamiento que aloja LVM. Utilice el tipo de código apropiado para su partición: `8e` para MBR, y `8e00` para.

### Eliminar una partición de un grupo de volúmenes

Si ha creado un volumen lógico en la partición, [elimínelo](#Eliminar_volúmenes_lógicos) primero.

Todos los datos de la partición deben ser movidos a otra partición. Afortunadamente, LVM lo hace sencillo:

```
# pvmove /dev/sdb1

```

Si quiere tener los datos en un volumen fisico específico, agréguelo como segundo argumento a `pvmove`:

```
# pvmove /dev/sdb1 /dev/sdf1

```

Luego, eliminamos los volúmenes físicos del grupo de volúmenes:

```
# vgreduce myVg /dev/sdb1

```

O, eliminamos todos los volúmenes vacíos:

```
# vgreduce --all vg0

```

Por último, si quiere usar la partición para algo más, y quiere evitar a LVM, piense que esa partición es un volumen fisico más:

```
# pvremove /dev/sdb1

```

### Desactivar un grupo de volúmenes

Basta con invocar la orden:

```
# vgchange -a n <*grupo_de_volúmenes*>

```

Esto desactivará el grupo de volúmenes y le permitirá desmontar el contenedor donde está almacenado.

## Tipos de volúmenes lógicos

Además de volúmenes lógicos simples, LVM admite instantáneas, volúmenes lógicos para almacenamiento caché, volúmenes lógicos de aprovisionamiento ligero y RAID.

### Instantáneas/Snapshots

LVM permite tomar instantáneas («*snapshots*») de su sitema, lo que es mucho más eficiente que las tradicionales copias de respaldo («*backup*»). Podemos hacer esto usando una politica COW (copy-on-write/*copia-cuando-escribe*). La instantánea inicial simplemente contiene enlaces fuertes a los inodos de sus datos actuales. Mientras los datos estén descargados, la instantánea simplemente contará con punteros a sus respectivos inodos y no a los datos en sí mismos. Cada vez que se modifica un archivo o un directorio a la que apunte la isntantanea, LVM automaticamente clonará los datos. Por lo tanto, puede tener instantáneas de un sistema de 35 GiB de datos usando solo 2 GiB de espacio libre, mientras sean modificados menos de 2GiB de datos (en el original y en la instantánea). Para poder crear instantáneas necesita tener espacio no asignado en su grupo de volúmenes. La instantánea, como cualquier otro volumen, ocupará espacio en el grupo de volúmenes. Por lo tanto, si planea usar instantáneas para hacer una copia de seguridad de su partición raíz, no asigne el 100% de su grupo de volúmenes para el volumen lógico raíz.

#### Configuración

Los volúmenes lógicos para las instantáneas se crean igual que los normales:

```
# lvcreate --size 100M --snapshot --name snap01 /dev/mapper/vg0-pv

```

Con dicho volumen, podrá modificar hasta de 100 MiB de datos, antes de que el volumen para las instantáneas se llene.

Para revertir el volumen lógico del «volumen físico» modificado al estado en que se tomó la instantánea «snap01», ejecute:

```
# lvconvert --merge /dev/vg0/snap01

```

En caso de que el volumen lógico de origen esté activo, la fusión se producirá en el siguiente reinicio (la fusión se puede hacer, incluso, desde un CD Live)

**Nota:** la instantánea dejará de existir después de la fusión.

Se pueden tomar también varias instantáneas y cada una se puede combinar con el volumen lógico de origen a voluntad.

La instantánea se puede montar y respaldar con **dd** o **tar**. El tamaño del archivo de respaldo hecho con **dd** será equivalente al tamaño de los archivos que residen en el volumen de instantánea. Para restaurar basta con crear una instantánea, montarla y escribir o extraerla de la copia de seguridad. Y luego fusionarla con la de origen.

Las instantáneas se utilizan principalmente para proporcionar una copia congelada de un sistema de archivos para respaldarlo; una copia de seguridad que tome dos horas ofrece una imagen más coherente del sistema de archivos que una copia de respaldo directamente de la partición.

Vea [Create root filesystem snapshots with LVM](/index.php/Create_root_filesystem_snapshots_with_LVM "Create root filesystem snapshots with LVM") para automatizar la creación de instantáneas límpias del sistema de archivos raíz durante el inicio del sistema para respaldar y restaurar.

[dm-crypt/Encrypting an entire system#LVM on LUKS](/index.php/Dm-crypt/Encrypting_an_entire_system#LVM_on_LUKS "Dm-crypt/Encrypting an entire system") y [dm-crypt/Encrypting an entire system#LUKS on LVM](/index.php/Dm-crypt/Encrypting_an_entire_system#LUKS_on_LVM "Dm-crypt/Encrypting an entire system").

Si tiene volúmenes LVM no activados a través de [initramfs](/index.php/Initramfs "Initramfs"), [active](/index.php/Enable "Enable") el servicio `lvm-monitoring.service`, proporcionado por el paquete [lvm2](https://www.archlinux.org/packages/?name=lvm2).

### La memoria caché de LVM

De [lvmcache(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvmcache.7):

	El tipo de volumen lógico de caché utiliza un volumen lógico pequeño y rápido para mejorar el rendimiento de un volumen lógico grande y lento. Lo hace almacenando en el volumen lógico más rápido los bloques utilizados con más frecuencia (del volumen lógico grande). LVM se refiere al volumen lógico pequeño y rápido como un volumen lógico que actúa como un contenedor de memoria caché. El volumen lógico lento se llama volumen lógico de origen. Debido a los requisitos de dm-cache (el controlador del kernel), LVM divide aún más el volumen lógico que sirve de contenedor de la memoria caché en dos dispositivos: el volumen lógico para la caché de datos y el volumen lógico para la caché de metadatos. El volumen lógico para la caché de datos es donde se guardan copias de bloques de datos del volumen lógico de origen para aumentar la velocidad. El volumen lógico para la memoria caché de los metadatos contiene la información de recuento que especifica dónde se almacenan los bloques de datos (por ejemplo, en el volumen lógico de origen o en el volumen lógico para la caché de los datos). Los usuarios deben estar familiarizados con estos volúmenes lógicos si desean crear los mejores y más robustos volúmenes lógicos como almacenamientos de caché. Todos estos volúmenes lógicos asociados deben estar en el mismo grupo de volúmenes.

#### Crear la memoria caché

El método rápido es crear un volumen físico (si es necesario) en el disco y agregarlo al grupo de volúmenes existente:

```
# vgextend dataVG /dev/sdx

```

Cree un contenedor de caché con metadatos automáticos en sdb y convierta el volumen lógico existente (dataLV) a un volumen de almacenamiento caché, todo en un solo paso:

```
# lvcreate --type cache --cachemode writethrough -L 20G -n dataLV_cachepool dataVG/dataLV /dev/sdx

```

Obviamente, si desea que su caché sea más grande, puede cambiar el parámetro `-L` a un tamaño diferente.

**Nota:** Cachemode tiene dos opciones posibles:

*   `writethrough` asegura que todos los datos escritos se almacenarán tanto en el volúmen lógico que actúa como contenedor para la memoria caché como en el volúmen lógico de origen. La pérdida de un dispositivo asociado con el volúmen lógico de la memoria caché, en este caso, no significaría la pérdida de ningún dato;
*   `writeback` garantiza un mejor rendimiento, pero a costa de un mayor riesgo de pérdida de datos en caso de que la unidad utilizada para la caché falle.

Si no se indica un valor `--cachemode` específico, el sistema asumirá el parámetro `writethrough` como predeterminado.

#### Eliminar la memoria caché

Si alguna vez necesita deshacer la operación anterior en un solo paso :

```
# lvconvert --uncache dataVG/dataLV

```

Esto confirma las escrituras pendientes que aún están en la memoria caché para que vuelvan al volumen lógico de origen, luego elimina la caché. Otras opciones están disponibles y se describen en [lvmcache(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvmcache.7).

### RAID

De [lvmraid(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvmraid.7):

	[lvm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvm.8) RAID es una forma de crear un volumen lógico (LV) que utiliza varios dispositivos físicos para mejorar el rendimiento o tolerar los posibles fallos de alguno de los dispositivos. En LVM, los dispositivos físicos son volúmenes físicos (PV) integrados un solo grupo de volúmenes (VG).

RAID sobre LVM admite RAID 0, RAID 1, RAID 4, RAID 5, RAID 6 y RAID 10\. Consulte [Wikipedia:Standard RAID levels](https://en.wikipedia.org/wiki/Standard_RAID_levels "wikipedia:Standard RAID levels") para obtener detalles sobre cada nivel.

#### Configurar RAID

Cree los volúmenes físicos:

```
# pvcreate /dev/sda2 /dev/sdb2

```

Cree un grupo de volúmenes con los volúmenes físicos:

```
# vgcreate VolGroup00 /dev/sda2 /dev/sdb2

```

Cree volúmenes lógicos con `lvcreate --type *raidlevel*`, consulte [lvmraid(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvmraid.7) y [lvcreate(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvcreate.8) para obtener más opciones.

```
# lvcreate --type RaidLevel [OPTIONS] -n Name -L Size VG [PVs]

```

Por ejemplo:

```
# lvcreate --type raid1 --mirrors 1 -L 20G -n myraid1vol VolGroup00 /dev/sda2 /dev/sdb2

```

creará un volumen lógico replicado de 20 GiB llamado «myraid1vol» en VolGroup00 sobre `/dev/sda2` y `/dev/sdb2`.

#### Configurar mkinitcpio para RAID

Si su sistema de archivos raíz está en LVM sobre RAID además de los hooks `lvm2` o `sd-lvm2`, debe agregar `dm-raid` y los módulos RAID apropiados (por ejemplo, `raid0`, `raid1`, `raid10` y/o `raid456`) a la matriz MODULES en `mkinitcpio.conf`.

Para initramfs basado en busybox:

 `/etc/mkinitcpio.conf` 
```
MODULES=(**dm-raid raid0 raid1 raid10 raid456**)
HOOKS=(base **udev** ... block **lvm2** filesystems)
```

Para initramfs basado en systemd:

 `/etc/mkinitcpio.conf` 
```
MODULES=(**dm-raid raid0 raid1 raid10 raid456**)
HOOKS=(base **systemd** ... block **sd-lvm2** filesystems)
```

## Configuración gráfica

No existe una interfaz gráfica «oficial» para administrar volúmenes LVM, pero [system-config-lvm](https://aur.archlinux.org/packages/system-config-lvm/) cubre la mayoría de las operaciones comunes y proporciona visualizaciones simples del estado del volumen. Puede cambiar automáticamente el tamaño de muchos sistemas de archivos cuando redimensiona los volúmenes lógicos.

## Solución de problemas

### Problemas de arranque/apagado debido a lvmetad desactivado

El parámetro `use_lvmetad = 1` **debe** ajustarse en `/etc/lvm/lvm.conf`. Este es el valor predeterminado ahora: si tiene un archivo `lvm.conf.pacnew`, debe fusionarlos.

### Las órdenes LVM no funcionan

*   Cargue los modulos apropiados:

```
# modprobe dm-mod

```

El módulo `dm_mod` debería cargarse automáticamente. En caso contrario, pruebe con:

 `/etc/mkinitcpio.conf`  `MODULES=(dm_mod ...)` 

Tendrá que [volver a crear](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") la imagen initramfs para que surtan efectos los cambios realizados.

*   Anteponga *lvm* a la orden:

```
# lvm pvdisplay

```

### No se muestran los volúmenes lógicos

Si se está tratando de montar volúmenes lógicos existentes, pero no se muestran con `lvscan`, puede utilizar las siguientes órdenes para activarlos:

```
# vgscan
# vgchange -ay

```

### LVM sobre un medio extraíble

Síntomas:

 `# vgscan` 
```
  Reading all physical volumes.  This may take a while...
  /dev/backupdrive1/backup: read failed after 0 of 4096 at 319836585984: Input/output error
  /dev/backupdrive1/backup: read failed after 0 of 4096 at 319836643328: Input/output error
  /dev/backupdrive1/backup: read failed after 0 of 4096 at 0: Input/output error
  /dev/backupdrive1/backup: read failed after 0 of 4096 at 4096: Input/output error
  Found volume group "backupdrive1" using metadata type lvm2
  Found volume group "networkdrive" using metadata type lvm2

```

Causa:

	Extraer una unidad externa con LVM sin ​​desactivar el grupo(s) de volúmenes primero. Antes de desconectar el medio, asegúrese de ejecutar:

```
# vgchange -an *nombre_del_grupo_de_volumen*

```

Arreglo:

	Asumiendo que ya ha intentado activar el grupo de volúmenes con `# vgchange -ay *vg*`, y se siguen recibiendo los errores de entrada/salida, ejecute:

```
# vgchange -an *nombre_del_grupo_de_volumen*

```

	Desconecte la unidad externa y espere unos minutos:

```
# vgscan
# vgchange -ay *nombre_del_grupo_de_volumen*

```

### Al redimensionar un volumen lógico contiguo falla

Si al intentar extender un volumen lógico produce errores con:

```
" Insufficient suitable contiguous allocatable extents for logical volume "

```

La razón es que el volumen lógico se creó con una explícita política de asignación contigua (con las opciones `-C y` o `--alloc contiguous`) y no hay extensiones contiguas adyacentes adicionales disponibles (vea también [reference](http://www.hostatic.ro/2010/02/15/lvm-inherit-and-contiguous-policies/)).

Para solucionar este problema, antes de extender el volumen lógico, cambie su política de asignación con `lvchange --alloc inherit <volumen_lógico>`. Si necesita mantener la política de asignación contigua, un método alternativo consistiría en mover el volumen a un área del disco con suficientes extensiones libres (vea [[1]](http://superuser.com/questions/435075/how-to-align-logical-volumes-on-contiguous-physical-extents)).

### La orden «grub-mkconfig» informa del error «unknown filesystem»

Asegúrese de retirar los volúmenes de instantáneas antes de generar grub.cfg

### Dispositivo de volumen raíz aprovisionado Getting started para agotar tiempo de espera

Con una gran cantidad de instantáneas, `thin_check` se ejecuta durante un tiempo suficientemente prolongado para que se agote el tiempo de espera del dispositivo raíz. Para compensar, agregue el parámetro de arranque del kernel `rootdelay=60` a la configuración de su gestor de arranque.

### Demora al apagar

Si utiliza RAID, instantáneas o aprovisionamiento, y experimenta un retraso en el apagado, asegúrese de que `lvm2-monitor.service` está [iniciado](/index.php/Started "Started"). Consulte [FS#50420](https://bugs.archlinux.org/task/50420).

## Véase también

*   [Página de recursos de LVM2](http://sourceware.org/lvm2/) en SourceWare.org
*   [LVM](http://wiki.gentoo.org/wiki/LVM) artículo en Gentoo wiki
*   [Guía de Ubuntu LVM, parte 1](http://www.tutonics.com/2012/11/ubuntu-lvm-guide-part-1.html)[Parte 2 detalles de instantáneas](http://www.tutonics.com/2012/12/lvm-guide-part-2-snapshots.html)
*   [Red Hat: Logical Volume Manager Administration](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Logical_Volume_Manager_Administration/index.html)