Artículos relacionados

*   [Software RAID and LVM](/index.php/Software_RAID_and_LVM "Software RAID and LVM")
*   [Dm-crypt/Encrypting an Entire System (Español)#LVM sobre LUKS](/index.php/Dm-crypt/Encrypting_an_Entire_System_(Espa%C3%B1ol)#LVM_sobre_LUKS "Dm-crypt/Encrypting an Entire System (Español)")
*   [Dm-crypt/Encrypting an Entire System (Español)#LUKS sobre LVM](/index.php/Dm-crypt/Encrypting_an_Entire_System_(Espa%C3%B1ol)#LUKS_sobre_LVM "Dm-crypt/Encrypting an Entire System (Español)")

**Estado de la traducción:** este artículo es una versión traducida de [LVM](/index.php/LVM "LVM"). Fecha de la última traducción/revisión: **2015-06-25**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=LVM&diff=0&oldid=379925).

De [Wikipedia](https://en.wikipedia.org/wiki/es:LVM "wikipedia:es:LVM"):

	LVM es un [gestor de volúmenes lógicos](https://en.wikipedia.org/wiki/logical_volume_management "wikipedia:logical volume management") para el [kérnel de línux](https://en.wikipedia.org/wiki/N%C3%BAcleo_Linux "wikipedia:Núcleo Linux"), que gestiona unidades de disco y dispositivos similares de almacenamiento masivo.

## Contents

*   [1 Bloques para construir LVM](#Bloques_para_construir_LVM)
*   [2 Ventajas](#Ventajas)
*   [3 Desventajas](#Desventajas)
*   [4 Instalando Arch Linux en LVM](#Instalando_Arch_Linux_en_LVM)
    *   [4.1 Particionar discos](#Particionar_discos)
    *   [4.2 Crear volúmenes físicos](#Crear_vol.C3.BAmenes_f.C3.ADsicos)
    *   [4.3 Crear grupo de volúmenes](#Crear_grupo_de_vol.C3.BAmenes)
    *   [4.4 Crear en un solo paso](#Crear_en_un_solo_paso)
    *   [4.5 Crear volúmenes lógicos](#Crear_vol.C3.BAmenes_l.C3.B3gicos)
    *   [4.6 Crear el sistema de archivos y montar los volúmenes lógicos](#Crear_el_sistema_de_archivos_y_montar_los_vol.C3.BAmenes_l.C3.B3gicos)
    *   [4.7 Añadir el hook lvm2 a mkinitcpio.conf para root en LVM](#A.C3.B1adir_el_hook_lvm2_a_mkinitcpio.conf_para_root_en_LVM)
    *   [4.8 Opciones del kérnel](#Opciones_del_k.C3.A9rnel)
*   [5 Operaciones sobre los volúmenes](#Operaciones_sobre_los_vol.C3.BAmenes)
    *   [5.1 Opciones avanzadas](#Opciones_avanzadas)
    *   [5.2 Redimensionar los volúmenes](#Redimensionar_los_vol.C3.BAmenes)
        *   [5.2.1 Volúmenes físicos](#Vol.C3.BAmenes_f.C3.ADsicos)
            *   [5.2.1.1 Agrandar](#Agrandar)
            *   [5.2.1.2 Encoger](#Encoger)
                *   [5.2.1.2.1 Mover extensiones físicas](#Mover_extensiones_f.C3.ADsicas)
                *   [5.2.1.2.2 Redimensionar el volumen físico](#Redimensionar_el_volumen_f.C3.ADsico)
                *   [5.2.1.2.3 Redimensionar la partición](#Redimensionar_la_partici.C3.B3n)
        *   [5.2.2 Volúmenes lógicos](#Vol.C3.BAmenes_l.C3.B3gicos)
            *   [5.2.2.1 Agrandar o encoger con lvresize](#Agrandar_o_encoger_con_lvresize)
            *   [5.2.2.2 Redimensionar por separado el sistema de archivos](#Redimensionar_por_separado_el_sistema_de_archivos)
    *   [5.3 Eliminar volúmenes lógicos](#Eliminar_vol.C3.BAmenes_l.C3.B3gicos)
    *   [5.4 Agregar un volumen físico al grupo de volúmenes](#Agregar_un_volumen_f.C3.ADsico_al_grupo_de_vol.C3.BAmenes)
    *   [5.5 Eliminar una partición de un grupo de volúmenes](#Eliminar_una_partici.C3.B3n_de_un_grupo_de_vol.C3.BAmenes)
    *   [5.6 Desactivar un grupo de volúmenes](#Desactivar_un_grupo_de_vol.C3.BAmenes)
    *   [5.7 Instantáneas/Snapshots](#Instant.C3.A1neas.2FSnapshots)
        *   [5.7.1 Introducción](#Introducci.C3.B3n)
        *   [5.7.2 Configuracion](#Configuracion)
*   [6 Solucionando problemas](#Solucionando_problemas)
    *   [6.1 Cambios que podrían ser necesarios debido a cambios en los valores predeterminados de Arch Linux](#Cambios_que_podr.C3.ADan_ser_necesarios_debido_a_cambios_en_los_valores_predeterminados_de_Arch_Linux)
    *   [6.2 Las órdenes LVM no funcionan](#Las_.C3.B3rdenes_LVM_no_funcionan)
    *   [6.3 No se muestran los volúmenes lógicos](#No_se_muestran_los_vol.C3.BAmenes_l.C3.B3gicos)
    *   [6.4 LVM sobre un medio extraíble](#LVM_sobre_un_medio_extra.C3.ADble)
    *   [6.5 Al redimensionar un volumen lógico contiguo falla](#Al_redimensionar_un_volumen_l.C3.B3gico_contiguo_falla)
    *   [6.6 La orden «grub-mkconfig» informa del error «unknown filesystem»](#La_orden_.C2.ABgrub-mkconfig.C2.BB_informa_del_error_.C2.ABunknown_filesystem.C2.BB)
*   [7 Véase también](#V.C3.A9ase_tambi.C3.A9n)

### Bloques para construir LVM

*Logical Volume Management (LVM)* hace uso de la función [device-mapper](http://sources.redhat.com/dm/) del kérnel de línux para proporcionar un sistema de particiones independientes de la estructura subyacente del disco. Con LVM es posible crear un espacio de almacenamiento abstracto así como distintas «particiones virtuales», por lo que es más fácil de [agrandar/encoger](#Redimensionar_los_vol.C3.BAmenes) particiones (siempre sujeto a posibles limitaciones de su sistema de archivos).

Las particiones virtuales permiten añadir/eliminar particiones sin tener que preocuparse acerca de si se tiene suficiente espacio contiguo en un disco concreto, ni quedar atrapado en el fdisking de un disco en uso (y preguntándose si el kérnel está utilizando una tabla de particiones vieja o nueva), ni tener que mover otras particiones en el camino. Esto es un asunto que afecta estrictamente a la facilidad de gestión: no proporciona ninguna seguridad. Sin embargo, se acomoda muy bien con las otras dos tecnologías que estamos usando.

Los bloques básicos que construyen LVM son:

*   **Physical volume/Volúmenes físicos (PV)**: Son las particiones en el disco duro (o, incluso, el propio disco o un archivo [loopback](https://en.wikipedia.org/wiki/es:Loopback "wikipedia:es:Loopback")) donde se tiene un grupo de volúmenes. Posee una cabecera especial y está dividida en extensiones físicas. Piense en los volúmenes físicos como grandes bloques de construcción utilizados para construir su disco duro.

*   **Volume group/Grupo de volúmenes (VG)**: Los grupos de volúmenes físicos son usados como volúmenes de almacenamiento (como si fueran un solo disco). Contienen volúmenes lógicos. Piense en los grupos de volúmenes como discos duros.

*   **Logical volume/Volúmenes lógicos (LV)**: Es una «partición virtual/lógica» que reside en un grupo de volúmenes y está compuesta por extensiones físicas. Piense en los volúmenes lógicos como particiones normales.

*   **Physical extent/Extensiones físicas (PE)**: Es una pequeña parte de un volumen físico (por defecto, 4MB) que puede ser asignada a un volumen lógico. Piense en las extensiones físicas como partes de los discos que pueden ser asignadas a cualquier partición.

Ejemplo:

```
 **Discos físicos**

  Disco1 (/dev/sda):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
    |Partición1 50GB (Volumen físico) |Partición2 80GB (Volumen físico)       |
    |/dev/sda1                         |/dev/sda2                             |
    |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |

  Disco2 (/dev/sdb):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
    |Partición1 120GB (Volumen físico)                  |
    |/dev/sdb1                                          |
    | _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ __ _ _|

```

```
**Volúmenes lógicos LVM**

  Grupo de volumen1 (/dev/MyStorage/ = /dev/sda1 + /dev/sda2 + /dev/sdb1):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 
    |Volumen lógico1 15GB  |Volumen lógico2 35GB      |Volumen lógico3 200GB               |
    |/dev/MyStorage/rootvol|/dev/MyStorage/homevol    |/dev/MyStorage/mediavol             |
    |_ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |            

```

### Ventajas

LVM le da más flexibilidad que la simple partición de un disco duro para:

*   Poder utilizar cualquier número de discos como un gran disco.
*   Tener volúmenes lógicos estirados sobre varios discos.
*   Crear pequeños volúmenes lógicos y cambiar su tamaño «dinámicamente», cuando se llenen.
*   Cambiar el tamaño de los volúmenes lógicos sin importar su orden en el disco. No depende de la posición del volumen lógico dentro del grupo de volúmenes, ni hay necesidad de asegurar el espacio disponible circundante.
*   Cambiar/crear/borrar el tamaño de los volúmenes lógicos y físicos en línea. Los sistemas de archivos en ellos todavía tendrán que ser redimensionados, pero algunos (como ext4) apoyan el cambio de tamaño en línea.
*   Migración en línea/vivo de volumenes lógicos, siendo utilizado por los servicios para diferentes discos sin tener que reiniciar los servicios.
*   Las instantáneas que permiten hacer copias de respaldo del sistema de archivos, mientras se mantiene el tiempo de inactividad del servicio a un mínimo.
*   Soporte para albergar distintos mapeadores de dispositivos, incluido el cifrado del sistema de archivos transparente y almacenamiento en caché de los datos de uso frecuente.

### Desventajas

*   Los pasos adicionales en la configuración del sistema, que lo hace más complicado.

## Instalando Arch Linux en LVM

Se deben crear los volúmenes LVM entre el [particionado](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)") y el [formateado](/index.php/File_systems#Format_a_device "File systems") durante el procedimiento de instalación. En lugar de dar formato directamente a una partición para que sea su sistema de archivos root, esta operación se hará dentro de un volumen lógico (LV).

Asegúrese de que el paquete [lvm2](https://www.archlinux.org/packages/?name=lvm2) está [instalado](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)").

He aquí un breve resumen:

*   Cree la partición(s) donde residirá su volumen físico (PV). Ajuste el tipo de partición para «Linux LVM», que es 8e si usa MBR y 8e00 para GPT.
*   Cree los volúmenes físicos (PV). Si se tiene un disco lo mejor es simplemente crear un volumen físico en una partición grande. Si tiene varios discos se pueden crear particiones en cada uno de ellos y crear un volumen físico en cada partición.
*   Cree el grupo de volúmenes (VG) y asocie todos los volúmenes físicos (PV) al mismo.
*   Cree volúmenes lógicos (LV) dentro de su grupo de volúmenes (VG).
*   Continúe con el paso «Formatear las particiones» de [Beginners' guide (Español)](/index.php/Beginners%27_guide_(Espa%C3%B1ol) "Beginners' guide (Español)").
*   Cuando llegue al paso «Crear entorno inicial ramdisk» en la Guía para principiantes, agregue el hook `lvm` a `/etc/mkinitcpio.conf` (ver detalles más abajo ).

**Advertencia:** `/boot` no puede residir en LVM cuando se utiliza [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy"), ya que no soporta LVM. Los usuarios de [GRUB](/index.php/GRUB "GRUB") no tienen esta limitación. Si necesita utilizar GRUB Legacy, debe crear una partición `/boot` separada y particionarla directamente.

### Particionar discos

**Nota:** Este paso es opcional y depende de las preferencias de los usuarios. No obstante, en la mayoría de los casos es recomendable particionar el primer dispositivo.

Véase [Partitioning (Español)](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)") para saber cómo crear particiones en el dispositivo.

### Crear volúmenes físicos

Para listar todos los dispositivos capaces de ser utilizados como un volumen físico:

```
# lvmdiskscan

```

**Advertencia:** Asegúrese de indicar bien el dispositivo correcto, o de lo contrario la ejecución de las órdenes de abajo se traducirá en la perdidad de sus datos.

Cree un volumen físico en ellos:

```
# pvcreate *DISPOSITIVO*

```

Esta orden crea una cabecera en cada dispositivo para que se pueda utilizar para LVM. Tal como se define en [#Bloques para construir LVM](#Bloques_para_construir_LVM), el *DISPOSITIVO* puede ser un disco (por ejemplo, `/dev/sda`), una partición (por ejemplo, `/dev/sda2`) o un dispositivo loop back.

Por ejemplo:

```
# pvcreate /dev/sda2

```

Puede hacer un seguimiento de los volúmenes físicos creados con:

```
# pvdisplay

```

**Nota:** Si se utiliza un disco SSD sin particionarlo primero, utilice `pvcreate --dataalignment 1m /dev/sda` (para el tamaño de bloque de borrado de < 1MiB), véase por ejemplo [esto](http://serverfault.com/questions/356534/ssd-erase-block-size-lvm-pv-on-raw-device-alignment).

### Crear grupo de volúmenes

El siguiente paso, será crear un grupo de volúmenes sobre el volumen físico:

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

**Nota:** Se pueden crear más de un grupo de volúmenes si es necesario, pero entonces no tendrá todo su almacenamiento presente como si fuera un disco.

### Crear en un solo paso

LVM le permite la creación de un grupo de volúmenes sobre varios volúmenes físicos en un solo paso. Por ejemplo, para crear el grupo VolGroup00 con los tres dispositivos mencionados anteriormente, puede ejecutar:

```
# vgcreate VolGroup00 /dev/sda2 /dev/sdb1 /dev/sdc

```

Esta orden configurará primero las tres particiones como volúmenes físicos (si es necesario) y luego creará el grupo de volúmenes con los tres volúmenes físicos. La orden le advertirá si detecta un sistema de archivos existente en cualquiera de los dispositivos.

### Crear volúmenes lógicos

Necesitaremos crear volúmenes lógicos en este grupo de volúmenes. Para ello debe utilizar la siguiente orden, proporcionándole como parámetros, su tamaño (-L), el grupo de volúmenes al que pertenecerá, y el nombre (-n) del nuevo volumen lógico:

```
# lvcreate -L <*tamaño*> <*grupo_de_volúmenes*> -n <*volumen_lógico*>

```

Por ejemplo:

```
# lvcreate -L 10G VolGroup00 -n lvolhome

```

Luego, podrá acceder al nuevo volumen lógico creado con `/dev/mapper/Volgroup00-lvolhome` o `/dev/VolGroup00/lvolhome`. Igual que sucede con los grupos de volúmenes, puede ponerle el nombre que desee al volumen lógico cuando lo crea.

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

**Nota:** Es posible que deba cargar el módulo del kérnel *device-mapper* (**modprobe dm-mod**) para que las órdenes anteriores puedan tener éxito.

**Sugerencia:** Se puede comenzar creando volúmenes lógicos relativamente pequeños y ampliarlos más adelante si fuera necesario. Para simplificar, deje un poco de espacio libre en el grupo de volúmenes para tener margen para su expansión.

### Crear el sistema de archivos y montar los volúmenes lógicos

Sus volúmenes lógicos deberian encontrarse en `/dev/mapper/` y `/dev/NombredelGrupodedeVolúmenes`. De no encontrarse, use la siguiente orden para cargar el modulo que crea nodos de dispositivos y hacer que los grupos de volúmenes estén disponibles:

```
# modprobe dm-mod
# vgscan
# vgchange -ay

```

Ahora puede crear el sistema de archivos en los volúmenes lógicos, y montarlos como particiones normales (si está instalando Arch, remítase a [montar las particiones](/index.php/Beginners%27_guide_(Espa%C3%B1ol)#Montar_las_particiones "Beginners' guide (Español)") para obtener información adicional):

```
# mkfs.<*tipo_sistema_archivos*> /dev/mapper/<*grupo_volúmenes*>-<*volumen_lógico*>
# mount /dev/mapper/<*grupo_volúmenes*>-<*volumen_lógico*> /<*punto_montaje*>

```

Por ejemplo:

```
# mkfs.ext4 /dev/mapper/VolGroup00-lvolhome
# mount /dev/mapper/VolGroup00-lvolhome /home

```

**Advertencia:** Al elegir los puntos de montaje, solo tiene que seleccionar los volúmenes lógicos recién creados (utilice: `/dev/mapper/Volgroup00-lvolhome`). **No** seleccione las particiones reales en las que se crearon los volúmenes lógicos (por tanto, no utilice: `/dev/sda2`).

### Añadir el hook lvm2 a mkinitcpio.conf para root en LVM

Tendrá que asegurarse de que los hooks `udev` y `lvm2` en [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") están activados.

`udev` está en el archivo por defecto. Edite el archivo e inserte `lvm2` entre `block` y `filesystem` como sigue:

 `/etc/mkinitcpio.conf`  `HOOKS="base udev ... block **lvm2** filesystems"` 

Después, puede continuar con las instrucciones normales de instalación en el paso [crear imagen ram inicial](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio").

### Opciones del kérnel

Si el sistema de archivos raíz reside en un volumen lógico, el [parámetro del kérnel](/index.php/Kernel_parameter "Kernel parameter") `root=` debe apuntar al dispositivo mapeado, por ejemplo `/dev/mapper/*<nombre_grupovolumenes>*-*<nombre_volumenlógico>*`.

También podría ser necesario `dolvm`.

## Operaciones sobre los volúmenes

### Opciones avanzadas

Si necesita monitorización (necesario para snapshots —instantáneas—) puede activar lvmetad. Para ello establezca `use_lvmetad = 1` en `/etc/lvm/lvm.conf`. Este es el valor predeterminado por ahora.

Puede restringir los volúmenes que se activan de forma automática mediante el establecimiento de la variable `auto_activation_volume_list` en el archivo `/etc/lvm/lvm.conf`. En caso de duda, deje esta opción comentada.

### Redimensionar los volúmenes

#### Volúmenes físicos

Después de aumentar o antes de reducir el tamaño de un dispositivo que tiene sobre él un volumen físico, necesita aumentar o reducir el tamaño del volumen físico mediante `pvresize`.

##### Agrandar

Para ampliar el volumen físico existente sobre el dispositivo `/dev/sda1`, después de aumentar dicha [partición](/index.php/Partitioning "Partitioning"), ejecute:

```
# pvresize /dev/sda1

```

Esto detectará automáticamente el nuevo tamaño del dispositivo y extenderá el volumen físico a su máximo.

**Nota:** Este orden se puede ejecutar mientras el volumen está en línea.

##### Encoger

Para reducir un volumen físico antes de reducir el dispositivo subyacente, agregue el parámetro `--setphysicalvolumesize *tamaño*` a la orden, *por ejemplo*:

```
# pvresize --setphysicalvolumesize 40G /dev/sda1

```

La orden anterior puede arrojar el siguiente error:

```
 /dev/sda1: cannot resize to 25599 extents as later ones are allocated.
 0 physical volume(s) resized / 1 physical volume(s) not resized

```

De hecho `pvresize` se negará a reducir un volumen físico si tiene asignadas extensiones adyacentes a lo que sería su nuevo final. Se tiene que ejecutar [pvmove](#Mover_extensiones_f.C3.ADsicas) de antemano para reubicar estas extensiones en el grupo de volúmenes a otro lugar, si no hay suficiente espacio libre.

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

Se puede observar que el espacio LIBRE se intercala por todo el volumen. Para reducir el tamaño del volumen físico, primero tenemos que mover todos los segmentos utilizados al comienzo.

Aquí, el primer segmento libre es desde 0 a 153.600, lo cual nos deja con 153.601 extensiones libres. Ahora podemos mover este número de segmentos desde la última extensión física de la primera. La orden sería así:

 `# pvmove --alloc anywhere /dev/sdd1:307201-399668 /dev/sdd1:0-92466` 
```
/dev/sdd1: Moved: 0.1 %
/dev/sdd1: Moved: 0.2 %
...
/dev/sdd1: Moved: 99.9 %
/dev/sdd1: Moved: 100,0%
```

**Note:**

*   Esta orden indica que se muevan 92.467 (399.668-307.201) extensiones físicas **desde** el último segmento **al** primer segmento. Esto es posible ya que el primer segmento cerrado LIBRE es de 153.600 extensiones físicas, que puede contener las 92.467 extensiones físicas trasladadas.
*   La opción `--alloc anywhere` se utiliza cuando movemos extensiones físicas dentro de la misma partición. En caso de particiones diferentes, la orden sería algo como esto: `# pvmove /dev/sdb1:1000-1999 /dev/sdc1:0-999`
*   El traslado toma su tiempo (una/dos horas) en el caso de gran tamaño. Puede ser una buena idea ejecutar esta orden en una sesión [Tmux](/index.php/Tmux "Tmux") o [GNU Screen](/index.php/GNU_Screen "GNU Screen"). Cualquier parada no deseada del proceso puede ser fatal.
*   Una vez finalizada la operación, ejecute [Fsck](/index.php/Fsck "Fsck") para asegurarse de que su sistema de archivos es válido.

###### Redimensionar el volumen físico

Una vez que todos sus segmentos físicos libres están en la última extensión física, ejecute `# vgdisplay` y vea su extensión física libre.

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

###### Redimensionar la partición

Último paso, es necesario reducir la partición con su [herramienta de particionado](/index.php/Partitioning#Partitioning_tools "Partitioning") favorita.

#### Volúmenes lógicos

**Note:** *lvresize* proporciona más o menos las mismas opciones que las órdenes especializadas `lvextend` y `lvreduce`, al tiempo que permite hacer ambos tipos de operación. A pesar de esto, todos las utilidades ofrecen una opción `-r, --resizefs` que permite cambiar el tamaño del sistema de archivos junto con el volumen lógico mediante `fsadm(8)` (que soporta *ext2*, [ext3](/index.php/Ext3 "Ext3"), [ext4](/index.php/Ext4 "Ext4"), *ReiserFS* y [XFS](/index.php/XFS "XFS")). Por lo tanto, puede ser más fácil simplemente utilizar `lvresize` para ambas operaciones y utilizar `--resizefs` para simplificar un poco las cosas, excepto si tiene necesidades específicas o desea tener un control total sobre el proceso.

##### Agrandar o encoger con lvresize

**Advertencia:** Si bien la ampliación de un sistema de archivos puede, a menudo, hacerse en línea (*es decir* mientras el mismo está montado), incluso para la partición raíz, en cambio, la reducción necesitará, casi siempre, desmontar primero el sistema de archivos con el fin de evitar pérdida de datos. Asegúrese de que su sistema de archivos apoya lo que está tratando de hacer.

Ampliar 2GB el volumen lógico *nv1* dentro del grupo de volúmenes *vg1* *sin* tocar su sistema de archivos:

```
# lvresize -L +2G vg1/lv1

```

Reducir 500MB el volumen lógico `vg1/nv1` *sin* cambiar el tamaño de su sistema de archivos (asegúrese de que este último [está ya reducido](/index.php/LVM#Resizing_the_file_system_separately "LVM") en este caso):

```
# lvresize -L -500M vg1/lv1

```

Ajustar `vg1/lv1` a 15GB y redimensionar su sistema de archivos *todo a la vez*:

```
# lvresize -L 15G -r vg1/lv1

```

**Nota:** Solo están soportados los [sistemas de archivos](/index.php/File_systems "File systems") *ext2*, [ext3](/index.php/Ext3 "Ext3"), [ext4](/index.php/Ext4 "Ext4"), *ReiserFS* y [XFS](/index.php/XFS "XFS"). Para otros casos mire la [utilidad apropiada](/index.php/File_systems#Arch_Linux_support "File systems").

Si desea ocupar todo el espacio libre de un grupo de volúmenes, utilice la siguiente orden:

```
# lvresize -l +100%FREE *grupovolumen*/*volumenlógico*

```

Vea [lvresize(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvresize.8) para conocer opciones más detalladas.

##### Redimensionar por separado el sistema de archivos

Si no utiliza la opción `-r, --resizefs` para `lv{resize,extend,reduce}` o utiliza un sistema de archivos no soportado por `fsadm(8)` ([Btrfs](/index.php/Btrfs "Btrfs"), [ZFS](/index.php/ZFS "ZFS")...), es necesario cambiar el tamaño del sistema de archivos manualmente antes de encoger el volumen lógico o después de agrandar el mismo.

**Advertencia:** No todos los sistemas de archivos soportan el cambio de tamaño sin pérdida de datos y/o la redimensión online.

Por ejemplo, con los sistemas de archivos ext2/ext3/ext4:

```
# resize2fs *grupovolumenes*/*volumenfísico*

```

se ampliará el sistema de archivos al tamaño máximo del volumen lógico subyacente, mientras que con:

```
# resize2fs -M *grupovolumenes*/*volumenfísico*

```

se contraerá a su tamaño mínimo. Para redimensionar a un tamaño determinado, utilice:

```
# resize2fs *grupovolumenes*/*volumenfísico* *NuevoTamaño*

```

### Eliminar volúmenes lógicos

**Advertencia:** Antes de quitar un volumen lógico, asegúrese de mover todos los datos que desee conservar a otro lugar; ¡de lo contrario, se perderán!

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

No se olvide de actualizar el archivo `/etc/fstab`.

Se puede verificar la eliminación del volumen lógico escribiendo `lvs` como root de nuevo (vea el primer paso de esta sección).

### Agregar un volumen físico al grupo de volúmenes

En primer lugar, cree un nuevo volumen físico en el dispositivo de bloque que desea usar, y luego intégrelo en su grupo de volúmenes:

```
# pvcreate /dev/sdb1
# vgextend VolGroup00 /dev/sdb1

```

Por supuesto, esto aumentará el número total de extensiones físicas en el grupo de volúmenes, que podrá asignar a los volúmenes lógicos como mejor le parezca.

**Nota:** Se considera una buena práctica tener una [tabla de particiones](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)") en el soporte de almacenamiento que aloja LVM. Utilice el código tipo apropiado para su partición: `8e` para MBR, y `8e00` para GPT.

### Eliminar una partición de un grupo de volúmenes

Si ha creado un volumen lógico en la partición, [elimínelo](#Eliminar_vol.C3.BAmenes_l.C3.B3gicos) primero.

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
# vgchange -a <*grupo_volúmenes*>

```

Esto desactivará el grupo de volúmenes y le permitirá desmontar el contenedor donde está almacenado.

### Instantáneas/Snapshots

#### Introducción

LVM permite tomar instantáneas/snapshots de su sitema lo que es mucho más eficiente que el tradicional backup. Podemos hacer esto usando una politica COW (copy-on-write)/(copia-cuando-escribe). La instantánea inicial simplemente contiene enlaces fuertes a los inodos de sus datos actuales. Mientras los datos estén descargados, la instantánea simplemente contará con punteros a sus respectivos inodos y no a los datos en sí mismos. Cada vez que se modifica un archivo o un directorio a la que apunte la isntantanea, LVM automaticamente clonará los datos. Por lo tanto, puede tener instantáneas de un sistema de 35GB de datos usando solo 2GB de espacio libre, mientras sean modificados menos de 2GB de datos (en el original y en la instantánea).

#### Configuracion

Los volúmenes lógicos para las instantáneas se crean igual que los normales:

```
# lvcreate --size 100M --snapshot --name snap01 /dev/mapper/vg0-pv

```

Con dicho volumen, podrá modificar menos de 100MB de datos, antes de que el volumen para las instantáneas se llene.

Para revertir el volumen lógico del «volumen físico» modificado al estado en que se tomó la instantánea «snap01», ejecute:

`# lvconvert --merge /dev/vg0/snap01`

En caso de que el volumen lógico de origen esté activo, la fusión se producirá en el siguiente reinicio. (La fusión se puede hacer, incluso, desde un CD Live)

La instantánea dejará de existir después de la fusión.

Se pueden tomar también varias instantáneas y cada una se puede combinar con el volumen lógico de origen a voluntad.

La instantánea se puede montar y respaldar con **dd** o **tar**. El tamaño del archivo de respaldo hecho con **dd** será equivalente al tamaño de los archivos que residen en el volumen de instantánea. Para restaurar basta con crear una instantánea, montarla y escribir o extraerla de la copia de seguridad. Y luego fusionarla con la de origen.

Es importante tener el modulo *dm-snapshot* agregado en la variable MODULES de `/etc/mkinitcpio.conf`, de otra manera el sistema no iniciara. Si hizo esto en un sistema ya instalado, asegúrese de reconstruir la imagen del kérnel con:

```
# mkinitcpio -g /boot/initramfs-linux.img

```

Todo: scripts to automate snapshots of root before updates, to rollback... updating `menu.lst` to boot snapshots (separate article?)

Las instantáneas se utilizan principalmente para proporcionar una copia congelada de un sistema de archivos para respaldarlo; una copia de seguridad que tome dos horas ofrece una imagen más coherente del sistema de archivos que una copia de respaldo directamente de la partición.

Vea [Create root filesystem snapshots with LVM](/index.php/Create_root_filesystem_snapshots_with_LVM "Create root filesystem snapshots with LVM") para automatizar la creación de instantáneas límpias del sistema de archivos raíz durante el inicio del sistema para respaldar y restaurar.

[Dm-crypt/Encrypting an entire system#LVM on LUKS](/index.php/Dm-crypt/Encrypting_an_entire_system#LVM_on_LUKS "Dm-crypt/Encrypting an entire system") y [Dm-crypt/Encrypting an entire system#LUKS on LVM](/index.php/Dm-crypt/Encrypting_an_entire_system#LUKS_on_LVM "Dm-crypt/Encrypting an entire system").

Si tiene volúmenes LVM no activados a través de [initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)"), [active](#Using_units) el servicio **lvm-monitoring**, proporcionado por el paquete [lvm2](https://www.archlinux.org/packages/?name=lvm2).

## Solucionando problemas

### Cambios que podrían ser necesarios debido a cambios en los valores predeterminados de Arch Linux

El valor `use_lvmetad = 1` debe ser puesto en `/etc/lvm/lvm.conf`. Este es el valor predeterminado ahora, si tiene un archivo `lvm.conf.pacnew` este debe reflejar dicho cambio.

### Las órdenes LVM no funcionan

*   Cargue los modulos apropiados:

```
# modprobe dm-mod

```

El módulo `dm_mod` debería cargarse automáticamente. En caso contrario, pruebe con:

 `/etc/mkinitcpio.conf:`  `MODULES="dm_mod ..."` 

Tendrá que [recompilar](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") la imagen initramfs para que surtan efectos los cambios realizados.

*   Anteponga *lvm* a la orden:

```
# lvm pvdisplay

```

### No se muestran los volúmenes lógicos

Si se está tratando de montar volúmenes lógicos existentes, pero que no se muestran con `lvscan`, puede utilizar las siguientes órdenes para activarlos:

```
# vgscan
# vgchange -ay

```

### LVM sobre un medio extraíble

Síntomas:

```
# vgscan
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

## Véase también

*   [LVM2 Resource Page](http://sourceware.org/lvm2/) on SourceWare.org
*   [LVM HOWTO](http://tldp.org/HOWTO/LVM-HOWTO/) article at The Linux Documentation project
*   [LVM](http://wiki.gentoo.org/wiki/LVM) article at Gentoo wiki
*   [LVM2 Mirrors vs. MD Raid 1](http://www.joshbryan.com/blog/2008/01/02/lvm2-mirrors-vs-md-raid-1/) post by Josh Bryan
*   [Ubuntu LVM Guide Part 1](http://www.tutonics.com/2012/11/ubuntu-lvm-guide-part-1.html)[Part 2 detals snapshots](http://www.tutonics.com/2012/12/lvm-guide-part-2-snapshots.html)