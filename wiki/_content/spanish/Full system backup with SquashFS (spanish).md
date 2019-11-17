**Estado de la traducción**
Este artículo es una traducción de [Full system backup with SquashFS](/index.php/Full_system_backup_with_SquashFS "Full system backup with SquashFS"), revisada por última vez el **2019-11-15**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Full_system_backup_with_SquashFS&diff=0&oldid=588907) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Full system backup with tar (Español)](/index.php/Full_system_backup_with_tar_(Espa%C3%B1ol) "Full system backup with tar (Español)")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Descripción general](#Descripción_general)
*   [2 Preparar CD/DVD/USB live](#Preparar_CD/DVD/USB_live)
*   [3 Realizar copia de seguridad en entorno live](#Realizar_copia_de_seguridad_en_entorno_live)
*   [4 Restaurar (descomprimir)](#Restaurar_(descomprimir))
*   [5 Restaurar (montar y copiar)](#Restaurar_(montar_y_copiar))

## Descripción general

[SquashFS](https://en.wikipedia.org/wiki/es:SquashFS "wikipedia:es:SquashFS") [[1]](http://squashfs.sourceforge.net/) crea archivos de copia de seguridad de solo lectura altamente comprimidos de sistemas completos. Es conveniente ya que puede montarlo y realizar find/grep/cp/tree en él sin descomprimir todo el archivo SquashFS. La copia de seguridad lleva menos tiempo y la sobrecarga de recuperación/recorrido de archivos es menor en comparación con tar, pero modificar un archivo existente es imposible como contrapartida.

## Preparar CD/DVD/USB live

Debería tener [squashfs-tools](https://www.archlinux.org/packages/?name=squashfs-tools) instalado en el CD/DVD/USB live para crear archivos SquashFS. Remítase a [Archiso#Configure the live medium](/index.php/Archiso#Configure_the_live_medium "Archiso") sobre cómo configurar `packages.x86_64` y construir un CD/DVD/USB live con [squashfs-tools](https://www.archlinux.org/packages/?name=squashfs-tools) instalado.

## Realizar copia de seguridad en entorno live

Inicie en un CD/DVD/USB en vivo y monte los sistemas de archivos que desea respaldar.

**Nota:** el siguiente ejemplo es para una instalación de EFI-grub Arch con sdb1 como partición EFI y sdb2 como partición raíz.

```
# fsck /dev/sdb2
# fsck /dev/sdb1
# mount /dev/sdb2 /mnt
# mount /dev/sdb1 /mnt/boot/efi
# /ruta/mksquashfs.sh DIRECTORIO_ORIGEN DIRECTORIO_PARA_ARCHIVAR_RESPALDO

```

donde

 `/ruta/mksquashfs.sh` 
```
#!/usr/bin/env bash

# Precaución
if [ $# -ne 2 ]; then
  echo "invoque: mksquashfs.sh DIRECTORIO_ORIGEN DIRECTORIO_PARA_ARCHIVAR_RESPALDO"
  exit 1
fi
echo -ne "

¿Tiene fsck? "
read

# Respaldo
mksquashfs \
  "$1" "$2/$(date +%Y%m%d_%a).sfs" \
  -comp gzip \
  -xattrs \
  -progress \
  -mem 5G \
  -wildcards \
  -e \
  boot/efi \
  boot/grub \
  boot/initramfs-linux"*".img

```

## Restaurar (descomprimir)

**Advertencia:** lo siguiente está completo pero aún no se ha probado. No lo use antes de que esta señal de advertencia sea eliminada.

```
#!/bin/bash

# Ruta donde extraer archivos
target=/mnt

# Ruta al archivo de respaldo SquashFS
archive=/ruta/backup.sfs

unsquashfs -stat $archive
unsquashfs -force -dest $target $archive
```

**Nota:** para hacer que el sistema arranque después de la restauración, debe:

1.  Arreglar fstab
2.  arch-chroot
    1.  mkinitcpio -p linux
    2.  grub-install
    3.  grub-mkconfig

## Restaurar (montar y copiar)

**Advertencia:** lo siguiente está completo pero aún no se ha probado. No lo use antes de que esta señal de advertencia sea eliminada.

1.  mount somewhere/backup.sfs /mnt
2.  cp /mnt/archivo /ruta/archivo-dañado