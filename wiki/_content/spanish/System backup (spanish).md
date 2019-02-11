**Estado de la traducción**
Este artículo es una traducción de [System backup](/index.php/System_backup "System backup"), revisada por última vez el **2018-12-16**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=System_backup&diff=0&oldid=559218) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs")
*   [System maintenance#Backup](/index.php/System_maintenance#Backup "System maintenance")
*   [Disk cloning](/index.php/Disk_cloning "Disk cloning")
*   [Migrate installation to new hardware](/index.php/Migrate_installation_to_new_hardware "Migrate installation to new hardware")
*   [File recovery](/index.php/File_recovery "File recovery")

Es importante hacer regularmente una copia de seguridad de los datos del sistema y del usuario, almacenados, por ejemplo, en `/etc`, `/home`, `/var` y, para las instalaciones del servidor, también en `/srv`.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Utilizar instantáneas de Btrfs](#Utilizar_instantáneas_de_Btrfs)
*   [2 Utilizar instantáneas de LVM](#Utilizar_instantáneas_de_LVM)
*   [3 Utilizar rsync](#Utilizar_rsync)
*   [4 Utilizar tar](#Utilizar_tar)
*   [5 Copia de seguridad arrancable](#Copia_de_seguridad_arrancable)
    *   [5.1 Actualizar el archivo fstab](#Actualizar_el_archivo_fstab)
    *   [5.2 Actualizar el archivo de configuración del gestor de arranque](#Actualizar_el_archivo_de_configuración_del_gestor_de_arranque)
    *   [5.3 Primer arranque](#Primer_arranque)

## Utilizar instantáneas de Btrfs

Véanse [Btrfs#Snapshots](/index.php/Btrfs#Snapshots "Btrfs") y [Snapper](/index.php/Snapper "Snapper").

## Utilizar instantáneas de LVM

Véanse [LVM (Español)#Instantáneas/Snapshots](/index.php/LVM_(Espa%C3%B1ol)#Instantáneas/Snapshots "LVM (Español)") y [Create root filesystem snapshots with LVM](/index.php/Create_root_filesystem_snapshots_with_LVM "Create root filesystem snapshots with LVM").

## Utilizar rsync

Véase [rsync#As a backup utility](/index.php/Rsync#As_a_backup_utility "Rsync").

## Utilizar tar

Véase [Full system backup with tar](/index.php/Full_system_backup_with_tar "Full system backup with tar").

## Copia de seguridad arrancable

Tener una copia de seguridad arrancable puede ser útil en caso de que el sistema de archivos se corrompa o si una actualización rompe el sistema. La copia de seguridad también se puede usar como un banco de pruebas para realizar actualizaciones, con el repositorio *testing* activado, etc. Si transfirió el sistema a una partición o unidad diferente y desea iniciarlo, el proceso es tan simple como actualizar el archivo `/etc/fstab` para la copia de seguridad y el archivo de configuración para el gestor de arranque.

Esta sección asume que realizó una copia de seguridad del sistema en otra unidad o partición, que su gestor de arranque actual funciona bien y que igualmente desea arrancar desde la copia de seguridad.

### Actualizar el archivo fstab

Sin reiniciar, modifique [fstab](/index.php/Fstab "Fstab") para la copia de seguridad comentando o eliminando las entradas existentes. Agregue una entrada para la partición que contiene la copia de seguridad como en el ejemplo que sigue:

```
/dev/sda*X*    /             *ext4*      defaults                 0   1

```

Recuerde utilizar el nombre del dispositivo y el tipo de sistema de archivos adecuados.

### Actualizar el archivo de configuración del gestor de arranque

Para [Syslinux (Español)](/index.php/Syslinux_(Espa%C3%B1ol) "Syslinux (Español)"), todo lo que necesita hacer es duplicar la entrada actual, con la excepción de que apuntará a una unidad o partición diferente.

**Sugerencia:** en lugar de modificar `syslinux.cfg`, también puede editar provisionalmente el menú durante el arranque. Cuando aparezca el menú, presione la tecla `Tab` y cambie las entradas que le interesen. Las particiones se cuentan desde uno, las unidades desde cero.

Para [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)"), es recomendable [generar el archivo de configuración principal](/index.php/GRUB_(Espa%C3%B1ol)#Generar_el_archivo_de_configuración_principal "GRUB (Español)") automáticamente. Si desea instalar todos los archivos de GRUB en otro lugar que no sea `/boot`, como por ejemplo `/mnt/newroot/boot`, utilice el parámetro `--boot-directory`.

Verifique también la nueva entrada del menú en `/boot/grub/grub.cfg`. Asegúrese de que el UUID coincida con el de la nueva partición, de lo contrario aún podría iniciar el sistema anterior. Encuentre el UUID de una partición con la orden [lsblk](/index.php/Lsblk_(Espa%C3%B1ol) "Lsblk (Español)"):

```
$ lsblk -no NAME,UUID /dev/sdb3

```

donde debe sustituir «/dev/sdb3» por la partición deseada. Para listar los UUID de las particiones que GRUB cree que puede iniciar, utilice la orden grep:

```
# grep UUID= /boot/grub/grub.cfg

```

### Primer arranque

Reinicie el equipo y seleccione la entrada adecuada en el gestor de arranque. Esto cargará el sistema por primera vez. Deberían detectarse todos los periféricos y rellenarse las carpetas vacías en `/`.

Ahora puede reeditar `/etc/fstab` para agregar las particiones y los puntos de montaje eliminados anteriormente.