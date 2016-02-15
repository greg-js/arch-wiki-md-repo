El Master Boot Record (MBR) comprende los primeros 512 bytes de un dispositivo de almacenamiento. El MBR no es una partición; está reservada al cargador de arranque del sistema operativo y a la tabla de particiones del dispositivo de almacenamiento. El MBR puede llegar a ser eventualmente reemplazado por la [GUID Partition Table (GPT)](/index.php/GUID_Partition_Table "GUID Partition Table"), que es parte de la especificación de la [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface") .

## Contents

*   [1 Proceso de arranque](#Proceso_de_arranque)
*   [2 Historia](#Historia)
*   [3 Copia de seguridad y restauración](#Copia_de_seguridad_y_restauraci.C3.B3n)
*   [4 Restaurar un registro de inicio de Windows](#Restaurar_un_registro_de_inicio_de_Windows)
*   [5 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Proceso de arranque

El arranque es un proceso multietapa. La mayoría de los PC de hoy inicializan los dispositivos del sistema con un firmware llamado [BIOS](http://en.wikipedia.org/wiki/BIOS) (Basic Input/Output System), que normalmente se almacena en un chip ROM dedicado en la placa base. Después que los dispositivos del sistema se han inicializado, la BIOS busca el gestor de arranque (bootloader) en el MBR del primer dispositivo de almacenamiento reconocido (unidad de disco duro -HDD-, unidad de estado sólido -SSD-, CD/DVD, USB ...) o en la primera partición del dispositivo. A continuación, ejecuta el programa. El cargador de arranque lee la tabla de particiones, y es entonces capaz de cargar el sistema(s) operativo(s). Los gestores de arranque más comunes bajo GNU/Linux son [GRUB](/index.php/GRUB "GRUB") y [Syslinux](/index.php/Syslinux "Syslinux").

## Historia

El MBR consiste en un pequeño fragmento de código ensamblador (el gestor de arranque inicial - 446 bytes), una tabla de particiones para las 4 particiones primarias (16 bytes por cada una) y un **centinela** (0xAA55).

El código del gestor de arranque "clásico", en el MBR de Windows/DOS, comprueba la tabla de particiones para buscar una, y sólo una, partición _activa_, lee X sectores de la partición y luego transfiere el control al sistema operativo. El gestor de arranque de Windows/DOS _no_ puede arrancar una partición de Arch Linux, ya que no está diseñado para cargar el kernel de Linux, y sólo puede atender a una partición _activa_ y _primaria_ (estas características no afectan a GRUB).

El [GRand Unified Bootloader (GRUB)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") es el gestor de arranque estándar de facto para GNU/Linux, y se recomienda al usuario que lo instale en el MBR para permitir el arranque de _cualquier_ partición, ya sea primaria o lógica.

## Copia de seguridad y restauración

Debido a que el MBR se encuentra en el disco, se pueden hacer copias de seguridad y recuperar más tarde.

Para hacer una copia del MBR:

```
dd if=/dev/sda of=/path/mbr-backup bs=512 count=1

```

Para restaurar el MBR:

```
dd if=/path/mbr-backup of=/dev/sda bs=512 count=1

```

**Advertencia:** Restaurar el MBR con una tabla de particiones diferente hará que sus datos sean ilegibles y casi imposible de recuperar. Si usted simplemente necesita restaurar el gestor de arranque consulte [GRUB](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") o [Syslinux](/index.php/Syslinux_(Espa%C3%B1ol) "Syslinux (Español)").

Para borrar el MBR (puede ser útil si tiene que hacer una reinstalación completa de otro sistema operativo) bastará con borrar los primeros 446 bits porque el resto de byte del MBR contienen la tabla de particiones:

```
dd if=/dev/zero of=/dev/sda bs=446 count=1

```

## Restaurar un registro de inicio de Windows

Windows por convenio (y para facilitar la instalación) se suele instalar en la primera partición e instala su tabla de particiones y referencia a su gestor de arranque en el primer sector de la partición. Si accidentalmente instala un gestor de arranque como GRUB en la partición de Windows o daña el registro de arranque (boot record) de alguna otra manera, tendrá que utilizar una utilidad para repararlo. Microsoft, en el CD de recuperación y, algunas veces, en los CD de instalación, incluye una utilidad para reparar el boot sector `FIXBOOT` y una utilidad para reparar el MBR llamada `FIXMBR`. Con este método se puede, respectivamente, reparar la referencia al sector de arranque de la primera partición en el archivo bootloader y reparar la referencia en el MBR de la primera partición. Después de hacer ésto será necesario [reinstalar GRUB](/index.php/GRUB#Bootloader_installation "GRUB") en el MBR si se pretende efectuar el arranque desde él (GRUB puede ser configurado para cargar el bootloader de Windows).

Si desea volver a utilizar el MBR y el bootloader de Windows, puede utilizar el comando `FIXBOOT` que asocia el MBR al sector de arranque de la primera partición consiguiendo iniciar automáticamente el sistema operativo Windows.

Es de destacar que hay una utilidad Linux llamada `ms-sys` (esto es, el paquete [ms-sys](https://aur.archlinux.org/packages/ms-sys/) disponible en [AUR](/index.php/Arch_User_Repository "Arch User Repository")) que permite instalar MBR. Sin embargo, esta utilidad sólo está actualmente capacitada para escribir un nuevo MBR (todos los sistemas operativos y sistemas de archivos son compatibles) y nuevos sectores de arranque (es decir, también conocido como boot record equivalente a usar `FIXBOOT`) para sistemas de archivos FAT. La mayoría de los LiveCDs no tienen esta utilidad por defecto, por lo que tendrá que ser instalado por primera vez, o será necesario buscar un sistema live que la contenga como [Parted Magic](http://partedmagic.com/).

Primero, escriba la información de la partición (tabla de particiones) de nuevo con el comando:

```
ms-sys --partition /dev/sda1

```

Posteriormente, escriba un MBR para Windows 2000/XP/2003:

```
ms-sys --mbr /dev/sda # Lea las opciones para las diferentes versiones

```

A continuación, escriba el nuevo sector de arranque (boot record):

```
ms-sys -(1-6)         # Lea las opciones para descubrir el tipo correcto de registro FAT

```

`ms-sys` también puede escribir MBR para Windows 98, ME, Vista y 7, consulte `ms-sys -h`.

## Véase también

*   [¿Qué es el Master Boot Record (MBR)? (en inglés)](http://kb.iu.edu/data/aijw.html)