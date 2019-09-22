**Estado de la traducción**
Este artículo es una traducción de [Removing system encryption](/index.php/Removing_system_encryption "Removing system encryption"), revisada por última vez el **2019-09-18**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Removing_system_encryption&diff=0&oldid=560740) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Eliminar el cifrado de un sistema encriptado con [dm-crypt y LUKS](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Requisitos previos](#Requisitos_previos)
*   [2 Arrancar en un entorno Live](#Arrancar_en_un_entorno_Live)
*   [3 Activar las particiones](#Activar_las_particiones)
    *   [3.1 Nota sobre diferentes configuraciones](#Nota_sobre_diferentes_configuraciones)
    *   [3.2 Una vez localizadas las particiones](#Una_vez_localizadas_las_particiones)
        *   [3.2.1 Montar el espacio de respaldo](#Montar_el_espacio_de_respaldo)
*   [4 Realizar una copia de respaldo de los datos](#Realizar_una_copia_de_respaldo_de_los_datos)
*   [5 Revertir el cifrado](#Revertir_el_cifrado)
*   [6 Restaurar los datos](#Restaurar_los_datos)
*   [7 Reconfigurar el sistema operativo](#Reconfigurar_el_sistema_operativo)

## Requisitos previos

*   Un sistema de archivos raíz encriptado u otro sistema de archivos que no se monte mientras se inicia en el sistema operativo.
*   Suficiente espacio de disco para almacenar una copia de seguridad.
*   Un soporte (CD/USB) live de Arch Linux (u otro).
*   Unas pocas horas.

**Nota:** a finales de 2012, se han agregado nuevas herramientas a `cryptsetup` para añadir o eliminar el cifrado a/desde un sistema de archivos existente. Si bien aún se consideran experimentales, pueden ayudar considerablemente a tal propósito. Dispone de más información en [cryptsetup-reencrypt(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cryptsetup-reencrypt.8).

## Arrancar en un entorno Live

Descargue y grabe la última imagen de Arch, reinicie el sistema y arraánquela desde el soporte.

## Activar las particiones

### Nota sobre diferentes configuraciones

He aquí una configuración de muestra:

| disco |
| ntfs | grupo de volúmenes (lvm) | ntfs |
| otro so | cryptswap (volumen lógico) | cryptroot (volumen lógico) | Compartido |
| luks | luks |
| swap | root (xfs) |

Las secciones grises solo agregan un marco de referencia y se pueden ignorar. Las particiones verdes serán modificadas. El texto verde debe coincidir con la configuración de su sistema. La partición amarilla se utilizará como espacio de almacenamiento y se puede cambiar a voluntad. En el sistema de ejemplo: myvg contiene volúmenes lógicos llamados cryptroot y cryptswap. Están ubicados en /dev/myvg/cryptroot y /dev/myvg/cryptswap. En el arranque, luks se usa junto con algunas entradas de crypttab para crear /dev/mapper/root y /dev/mapper/swap. El espacio intercambio no se desencriptará como parte de esta guía, ya que deshacer el cifrado de intercambio no requiere una copia de seguridad o restauración complejas.

El sistema de ejemplo no es indicativo de todos los sistemas. Diferentes sistemas de archivos requieren diferentes herramientas para realizar copias de seguridad y restaurar sus datos de manera efectiva. LVM puede ignorarse si no se usa. XFS requiere xfs_copy para garantizar una copia de seguridad y una restauración eficaces, DD no es suficiente. DD se puede usar con ext2,3 y 4 (por favor, que alguien comente sobre jfs, reiserfs y reiser4fs).

### Una vez localizadas las particiones

Cargar los módulos necesarios:

```
modprobe dm-mod #device mapper/lvm
modprobe dm-crypt #luks

```

Activar el grupo de volúmenes lvm:

```
pvscan #eescaneo de volúmenes físicos
vgscan #escaneo de grupo de volúmenes
lvscan #escaneo de volúmenes lógicos
lvchange -ay myvg/cryptroot

```

Abra el sistema de archivos encriptado con luks para que pueda leerse:

```
cryptSetup luksOpen /dev/myvg/cryptroot root

```

Introduzca la contraseña. Nota: la única partición en la que se operará que debe montarse en este punto es la partición de respaldo. Si ya está montada una partición distinta de la partición de respaldo, ahora se puede desmontar de manera segura.

#### Montar el espacio de respaldo

Solo si se utiliza NTFS para almacenar la copia de seguridad

```
# pacman -S ntfs-3g

```

El siguiente paso es importante para el almacenamiento de respaldo.

```
# mount -t ntfs-3g -o rw <u>/dev/sda5 /media/Shared</u>

```

o utilice netcat para almacenar la copia de seguridad en un sistema remoto

TODO: añadir instrucciones netcat.

## Realizar una copia de respaldo de los datos

Utilizar xfs_copy:

```
xfs_copy -db /dev/mapper/root <u>/media/Shared/backup_root.img</u>

```

Nota: el indicador -d conserva los uuids y -b garantiza que no se intente realizar E/S directa en ninguno de los archivos de destino.

Utilizar dd:

```
dd if=/dev/mapper/root of=<u>/media/Shared/backup_root.img</u>

```

## Revertir el cifrado

Ahora llega el momento crucial, el punto de no retorno por decirlo así. Asegúrese de que está listo para realizar esta operación. Si planea deshacerlo más adelante, tendrá que comenzar casi desde cero. Y no se imagina lo divertido que puede ser eso.

```
cryptsetup luksClose root
lvm lvremove myvg/cryptroot

```

## Restaurar los datos

Tenemos que crear un nuevo volumen lógico para alojar nuestro sistema de archivos raíz, luego lo restauraremos.

```
lvm lvcreate -l 100%FREE -n root myvg
xfs_copy -db <u>/media/Shared/backup_root.img</u> /dev/myvg/root #advierta que el segundo nombre de unidad se cambia ahora.

```

## Reconfigurar el sistema operativo

Debe iniciar su sistema operativo y modificar /etc/crypttab, /etc/mkinitcpio.conf, /etc/fstab, y posiblemente /boot/grub/menu.lst.