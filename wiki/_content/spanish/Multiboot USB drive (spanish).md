**Estado de la traducción**
Este artículo es una traducción de [Multiboot USB drive](/index.php/Multiboot_USB_drive "Multiboot USB drive"), revisada por última vez el **2018-11-06**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Multiboot_USB_drive&diff=0&oldid=552215) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)")
*   [Syslinux (Español)](/index.php/Syslinux_(Espa%C3%B1ol) "Syslinux (Español)")
*   [Archiso (Español)](/index.php/Archiso_(Espa%C3%B1ol) "Archiso (Español)")

Una unidad [flash](https://en.wikipedia.org/wiki/es:Memoria_flash "wikipedia:es:Memoria flash") [USB](https://en.wikipedia.org/wiki/es:Universal_Serial_Bus "wikipedia:es:Universal Serial Bus") multiarranque permite arrancar múltiples [archivos ISO](https://en.wikipedia.org/wiki/es:Imagen_ISO "wikipedia:es:Imagen ISO") desde un solo dispositivo. Los archivos ISO se pueden copiar al dispositivo y arrancar directamente sin descomprimirlos primero. Hay varios métodos disponibles, pero es posible que no funcionen con todas las imágenes ISO.

## Contents

*   [1 Utilizar GRUB y dispositivos loopback](#Utilizar_GRUB_y_dispositivos_loopback)
    *   [1.1 Preparación](#Preparaci.C3.B3n)
    *   [1.2 Instalar GRUB](#Instalar_GRUB)
        *   [1.2.1 Instalación simple](#Instalaci.C3.B3n_simple)
        *   [1.2.2 Arranque híbrido UEFI GPT + BIOS GPT/MBR](#Arranque_h.C3.ADbrido_UEFI_GPT_.2B_BIOS_GPT.2FMBR)
    *   [1.3 Configurar GRUB](#Configurar_GRUB)
        *   [1.3.1 Utilizar una plantilla](#Utilizar_una_plantilla)
        *   [1.3.2 Configuración manual](#Configuraci.C3.B3n_manual)
    *   [1.4 Entradas de arranque](#Entradas_de_arranque)
        *   [1.4.1 Lanzamiento mensual de Arch Linu](#Lanzamiento_mensual_de_Arch_Linu)
        *   [1.4.2 archboot](#archboot)
*   [2 Utilizar Syslinux y memdisk](#Utilizar_Syslinux_y_memdisk)
    *   [2.1 Preparación](#Preparaci.C3.B3n_2)
    *   [2.2 Instalar el módulo memdisk](#Instalar_el_m.C3.B3dulo_memdisk)
    *   [2.3 Configuración](#Configuraci.C3.B3n)
    *   [2.4 Precaución para sistemas de 32 bits](#Precauci.C3.B3n_para_sistemas_de_32_bits)
*   [3 Herramientas automatizadas](#Herramientas_automatizadas)
*   [4 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Utilizar GRUB y dispositivos loopback

Ventajas:

*   solo se requiere una partición;
*   todos los archivos ISO se encuentran en un directorio;
*   añadir y eliminar archivos ISO es simple.

Desventajas:

*   no todas las imágenes ISO son compatibles;
*   el menú de arranque original para el archivo ISO no se muestra;
*   puede ser difícil encontrar una entrada de arranque que funcione.

### Preparación

Cree, al menos, una partición y un sistema de archivos compatible con [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") en la unidad USB. Consulte [Partitioning (Español)](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)") y [File systems (Español)#Crear un sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol)#Crear_un_sistema_de_archivos "File systems (Español)"). Elija el tamaño en función del tamaño total de los archivos ISO que desea almacenar en la unidad y planifique el espacio adicional para el cargador de arranque.

### Instalar GRUB

#### Instalación simple

Monte el sistema de archivos en la unidad USB:

```
# mount /dev/sdXY /mnt

```

Cree el directorio /boot:

```
# mkdir /mnt/boot

```

Instale GRUB en la unidad USB:

```
# grub-install --target=i386-pc --recheck --boot-directory=/mnt/boot /dev/sdX

```

En caso de que desee arrancar imágenes ISO en modo UEFI, debe instalar grub para el objetivo UEFI :

```
# grub-install --target x86_64-efi --removable --boot-directory=/mnt/boot --efi-directory=/mnt

```

Para UEFI, la partición debe ser la primera en una tabla de particiones MBR y formateada con FAT32.

#### Arranque híbrido UEFI GPT + BIOS GPT/MBR

Esta configuración es útil para crear una memoria USB universal, que arranque en todos los equipos. En primer lugar, debe crear una tabla de particionado [GPT](/index.php/Partitioning_(Espa%C3%B1ol)#GUID_Partition_Table "Partitioning (Español)") en su dispositivo. Necesita al menos 3 particiones:

1.  Una partición «BIOS boot partition» (código tipo para gdisk `EF02`). Esta partición debe tener un tamaño de 1 MiB.
2.  Una partición «EFI System partition» (código tipo para gdisk `EF00` con un sistema de archivos [FAT32](/index.php/EFI_system_partition_(Espa%C3%B1ol)#Formatear_la_partici.C3.B3n "EFI system partition (Español)")). Esta partición puede ser tan pequeña como 50 MiB.

1.  Una partición de datos (use un sistema de archivos compatible con [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)")). Esta partición puede ocupar el resto del espacio de su disco.

A continuación, debe crear una tabla de particionado MBR híbrida, ya que la configuración del indicador de arranque («boot») en la partición «*MBR protective*» podría no ser suficiente.

Ejemplo de creación de tabla de particionado híbrida MBR usando [gdisk](/index.php/Gdisk "Gdisk"):

```
# gdisk /dev/sdX

Command (? for help): r
Recovery/transformation command (? for help): h

WARNING! Hybrid MBRs are flaky and dangerous! If you decide not to use one,
just hit the Enter key at the below prompt and your MBR partition table will
be untouched.

Type from one to three GPT partition numbers, separated by spaces, to be added to the hybrid MBR, in sequence: 1 2 3
Place EFI GPT (0xEE) partition first in MBR (good for GRUB)? (Y/N): N

Creating entry for GPT partition #1 (MBR partition #1)
Enter an MBR hex code (default EF): 
Set the bootable flag? (Y/N): N

Creating entry for GPT partition #2 (MBR partition #2)
Enter an MBR hex code (default EF): 
Set the bootable flag? (Y/N): N

Creating entry for GPT partition #3 (MBR partition #3)
Enter an MBR hex code (default 83): 
Set the bootable flag? (Y/N): Y

Recovery/transformation command (? for help): x
Expert command (? for help): h
Expert command (? for help): w

Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING
PARTITIONS!!

Do you want to proceed? (Y/N): Y

```

No se olvide de formatear las particiones:

```
# mkfs.fat -F32 /dev/sdX2
# mkfs.ext4 /dev/sdX3

```

Ahora puede instalar GRUB para que sea compatible tanto con EFI + GPT como con BIOS + GPT/MBR. La configuración de GRUB (--boot-directory) se puede mantener en el mismo lugar.

Primero, debe montar la partición EFI del sistema (ESP) y la partición de datos de su unidad USB. Luego, puede instalar GRUB para UEFI con la orden:

```
# grub-install --target=x86_64-efi --recheck --removable --efi-directory=/*EFI_MOUNTPOINT* --boot-directory=/*DATA_MOUNTPOINT*/boot

```

Y para BIOS con:

```
# grub-install --target=i386-pc --recheck --boot-directory=/*DATA_MOUNTPOINT*/boot /dev/sd*X*

```

Como respaldo adicional, también puede instalar GRUB en el «*MBR-bootable*» de su partición de datos:

```
# grub-install --target=i386-pc --recheck --boot-directory=/*DATA_MOUNTPOINT*/boot /dev/*sdX3*

```

### Configurar GRUB

#### Utilizar una plantilla

Hay algunos proyectos git que proporcionan archivos de configuración de GRUB preexistentes, y un archivo `grub.cfg` genérico que se puede utilizar para cargar las otras entradas de arranque bajo demanda, mostrándolas solo si los archivos ISO especificados —o carpetas que los contienen— están presentes en el disco.

USB multiarranque: [https://github.com/aguslr/multibootusb](https://github.com/aguslr/multibootusb)

GLIM (GRUB2 Live ISO Multiboot): [https://github.com/thias/glim](https://github.com/thias/glim)

#### Configuración manual

Para el propósito de la unidad USB multiarranque, es más fácil modificar el archivo `grub.cfg` manualmente en lugar de generarlo automáticamente. Alternativamente, realice los siguientes cambios en `/etc/grub.d/40_custom` o `/mnt/boot/grub/custom.cfg` y genere `/mnt/boot/grub/grub.cfg` utilizando la orden [grub-mkconfig](/index.php/GRUB_(Espa%C3%B1ol)#Generar_el_archivo_de_configuraci.C3.B3n_principal "GRUB (Español)").

Como se recomienda usar un [nombre permanente](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol) "Persistent block device naming (Español)") en lugar de `/dev/sd*xY*` para identificar la partición en la unidad USB donde se encuentran los archivos de imágenes, defina una variable de conveniencia para mantener el valor. Si las imágenes ISO están en la misma partición que GRUB, use lo siguiente para leer el UUID en el momento del arranque:

 `/mnt/boot/grub/grub.cfg` 
```
# ruta a la partición que contiene imágenes ISO (usando UUID)
probe -u $root --set=rootuuid
set imgdevpath="/dev/disk/by-uuid/$rootuuid"
```

O especifique el UUID explícitamente:

 `/mnt/boot/grub/grub.cfg` 
```
# ruta a la partición que contiene imágenes ISO (usando UUID)
set imgdevpath="/dev/disk/by-uuid/*UUID_value*"
```

Alternativamente, use la etiqueta del dispositivo en lugar de UUID:

 `/mnt/boot/grub/grub.cfg` 
```
# ruta a la partición que contiene imágenes ISO (usando etiquetas)
set imgdevpath="/dev/disk/by-label/*label_value*"
```

El UUID o la etiqueta necesarios se pueden encontrar usando `lsblk -f`. No utilice la misma etiqueta que la ISO de Arch para el dispositivo USB, de lo contrario, el proceso de arranque fallará.

Para completar la configuración, se debe agregar una entrada de arranque para cada imagen ISO debajo de este encabezado, consulte la siguiente sección para ver ejemplos.

### Entradas de arranque

Se supone que las imágenes ISO se almacenan en el directorio `boot/iso/` en el mismo sistema de archivos donde está instalado GRUB. De lo contrario, sería necesario prefijar la ruta al archivo ISO con la identificación del dispositivo al usar la orden `loopback`, por ejemplo, `loopback loop **(hd1,2)**$isofile`. Como esta identificación de dispositivos no es [persistente](/index.php/Persistent_block_device_naming "Persistent block device naming"), no se utiliza en los ejemplos de esta sección.

Se pueden usar nombres de dispositivo de bloque persistente como tal. Reemplace UUID de acuerdo con el UUID de su sistema de archivos.

```
# definir globalmente (es decir, fuera de cualquier menuentry)
insmod search_fs_uuid
search --no-floppy --set=**isopart** --fs-uuid *123-456*
# luego usar dentro de cada menuentry en su lugar
loopback loop **($isopart)**$isofile
```

**Sugerencia:** para obtener una lista de los parámetros del kernel, consulte [kernel-parameters.rst](https://www.kernel.org/doc/Documentation/admin-guide/kernel-parameters.rst) y [kernel-parameters.txt](https://www.kernel.org/doc/Documentation/admin-guide/kernel-parameters.txt) (aún incompleto). Para obtener más ejemplos de entradas de arranque, consulte la [documentación de los desarrolladores de GRUB](https://www.gnu.org/software/grub/manual/grub.html#Multi_002dboot-manual-config) o la documentación de la distribución que desea iniciar.

#### Lanzamiento mensual de Arch Linu

Vea también [archiso (Español)](/index.php/Archiso_(Espa%C3%B1ol) "Archiso (Español)").

```
menuentry '[loopback]archlinux-2017.10.01-x86_64.iso' {
	set isofile='/boot/iso/archlinux-2017.10.01-x86_64.iso'
	loopback loop $isofile
	linux (loop)/arch/boot/x86_64/vmlinuz img_dev=$imgdevpath img_loop=$isofile earlymodules=loop
	initrd (loop)/arch/boot/intel_ucode.img (loop)/arch/boot/amd_ucode.img (loop)/arch/boot/x86_64/archiso.img
}
```

Consulte [README.bootparams](https://git.archlinux.org/archiso.git/tree/docs/README.bootparams) para ver las opciones de archiso admitidas en la línea de órdenes del kernel.

#### archboot

Vea también [archboot (Español)](/index.php/Archboot_(Espa%C3%B1ol) "Archboot (Español)").

```
menuentry '[loopback]archlinux-2014.11-1-archboot' {
	set isofile='/boot/iso/archlinux-2014.11-1-archboot.iso'
	loopback loop $isofile
	linux (loop)/boot/vmlinuz_**x86_64** iso_loop_dev=$imgdevpath iso_loop_path=$isofile
	initrd (loop)/boot/initramfs_**x86_64**.img
}
```

## Utilizar Syslinux y memdisk

Usando el módulo [memdisk](http://www.syslinux.org/wiki/index.php/MEMDISK), la imagen ISO se carga en la memoria y esta carga el gestor de arranque. Asegúrese de que el sistema que arrancará esta unidad USB tenga suficiente memoria para el archivo de imagen y el sistema operativo que se va a ejecutar.

### Preparación

Asegúrese de que la unidad USB esté correctamente [particionada](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)") y que haya una partición con un [sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)") compatible con Syslinux, por ejemplo fat32 o ext4\. Luego instale Syslinux en esta partición, vea [Syslinux (Español)#Instalación](/index.php/Syslinux_(Espa%C3%B1ol)#Instalaci.C3.B3n "Syslinux (Español)").

### Instalar el módulo memdisk

El módulo memdisk no se instalará durante la instalación de Syslinux, por lo que se debe instalar manualmente. Monte la partición donde esté ubicado Syslinux en `/mnt/` y copie el módulo memdisk en el mismo directorio donde esté instalado Syslinux:

```
# cp /usr/lib/syslinux/bios/memdisk /mnt/boot/syslinux/

```

### Configuración

Después de copiar los archivos ISO en la unidad USB, edite el [archivo de configuración de Syslinux](/index.php/Syslinux_(Espa%C3%B1ol)#Configuraci.C3.B3n "Syslinux (Español)") y cree entradas de menú para las imágenes ISO. La entrada básica se verá así:

 `boot/syslinux/syslinux.cfg` 
```
LABEL *some_label*
    LINUX memdisk
    INITRD */path/to/image.iso*
    APPEND iso

```

Consulte [memdisk en la wiki de Syslinux](http://www.syslinux.org/wiki/index.php/MEMDISK) para más opciones de configuración.

### Precaución para sistemas de 32 bits

Al arrancar un sistema de 32 bits desde una imagen de más de 128MiB, es necesario aumentar el uso máximo de memoria virtual («vmalloc»). Esto se hace agregando `vmalloc=*value*M` a los parámetros del kernel, donde `*value*` debe ser más grande que el tamaño de la imagen ISO en MiB.[[1]](http://www.syslinux.org/wiki/index.php/MEMDISK#-_memdiskfind_in_combination_with_phram_and_mtdblock)

Por ejemplo, al arrancar el sistema de 32 bits desde la [ISO de instalación de Arch](https://www.archlinux.org/download/), presione la tecla `Tab` sobre la entrada `Boot Arch Linux (i686)` y agregue `vmalloc=768M` al final. Si omite este paso, se producirá el siguiente error durante el arranque:

```
modprobe: ERROR: could not insert 'phram': Input/output error

```

## Herramientas automatizadas

*   **liveusb-builder** — Un conjunto de scripts para crear un dispositivo USB multiarranque para distribuciones GNU/Linux

	[https://github.com/mytbk/liveusb-builder](https://github.com/mytbk/liveusb-builder) || [liveusb-builder-git](https://aur.archlinux.org/packages/liveusb-builder-git/)

*   **MultiSystem** — Una herramienta gráfica que permite instalar, administrar y eliminar múltiples imágenes ISO en un dispositivo USB.

	[http://liveusb.info/dotclear/](http://liveusb.info/dotclear/) || [multisystem](https://aur.archlinux.org/packages/multisystem/)

*   **MultiBootUSB** — Un software multiplataforma escrito en [Python](https://en.wikipedia.org/wiki/es:Python "wikipedia:es:Python") con interfaces [CLI](https://en.wikipedia.org/wiki/es:Interfaz_de_l%C3%ADnea_de_comandos "wikipedia:es:Interfaz de línea de comandos") y [GUI](https://en.wikipedia.org/wiki/es:Interfaz_gr%C3%A1fica_de_usuario "wikipedia:es:Interfaz gráfica de usuario") que permite instalar y eliminar múltiples imágenes de Linux live en una memoria USB.

	[http://multibootusb.org/](http://multibootusb.org/) || [multibootusb](https://aur.archlinux.org/packages/multibootusb/)

## Véase también

*   GRUB:
    *   [https://help.ubuntu.com/community/Grub2/ISOBoot/Examples](https://help.ubuntu.com/community/Grub2/ISOBoot/Examples)
    *   [https://help.ubuntu.com/community/Grub2/ISOBoot](https://help.ubuntu.com/community/Grub2/ISOBoot)
    *   [GRUB Live ISO Multiboot](https://github.com/thias/glim) — Configuraciones de GRUB para el arranque de imágenes ISO
*   Syslinux:
    *   [Arrancar una imagen ISO](http://www.syslinux.org/wiki/index.php?title=Boot_an_Iso_image)