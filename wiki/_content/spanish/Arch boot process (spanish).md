**Estado de la traducción:** este artículo es una versión traducida de [Arch boot process](/index.php/Arch_boot_process "Arch boot process"). Fecha de la última traducción/revisión: **2018-09-26**. Puede ayudar a actualizar la traducción, si advierte que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Arch_boot_process&diff=0&oldid=543767).

Artículos relacionados

*   [Master Boot Record](/index.php/Master_Boot_Record_(Espa%C3%B1ol) "Master Boot Record (Español)")
*   [GUID Partition Table](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)")
*   [mkinitcpio](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)")
*   [init](/index.php/Init "Init")
*   [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)")
*   [fstab](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)")
*   [Autostarting](/index.php/Autostarting_(Espa%C3%B1ol) "Autostarting (Español)")

Para iniciar Arch Linux, un [gestor de arranque](/index.php/Boot_loader "Boot loader") capaz de iniciar Linux como [GRUB](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") o [Syslinux](/index.php/Syslinux_(Espa%C3%B1ol) "Syslinux (Español)"), debe instalarse en el [Master Boot Record](/index.php/Master_Boot_Record_(Espa%C3%B1ol) "Master Boot Record (Español)") o en la [GUID Partition Table](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)"). El gestor de arranque es el responsable de cargar el kernel y el [disco ram inicial](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") antes de iniciar el proceso de arranque. El proceso es bastante diferente para los sistemas [BIOS](https://en.wikipedia.org/wiki/es:BIOS "wikipedia:es:BIOS") y [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)"), cuyos detalles se describen en esta página o en las enlazadas.

## Contents

*   [1 Tipos de firmware](#Tipos_de_firmware)
    *   [1.1 BIOS](#BIOS)
    *   [1.2 UEFI](#UEFI)
*   [2 Procesos de arranque](#Procesos_de_arranque)
    *   [2.1 Bajo BIOS](#Bajo_BIOS)
    *   [2.2 Bajo UEFI](#Bajo_UEFI)
*   [3 Gestor de arranque](#Gestor_de_arranque)
    *   [3.1 Comparación de características](#Comparaci.C3.B3n_de_caracter.C3.ADsticas)
    *   [3.2 Véase también](#V.C3.A9ase_tambi.C3.A9n)
*   [4 Kernel](#Kernel)
*   [5 initramfs](#initramfs)
*   [6 Fase init](#Fase_init)
*   [7 Getty](#Getty)
*   [8 Gestor de pantallas](#Gestor_de_pantallas)
*   [9 Login](#Login)
*   [10 Shell](#Shell)
*   [11 GUI, xinit o wayland](#GUI.2C_xinit_o_wayland)
*   [12 Véase también](#V.C3.A9ase_tambi.C3.A9n_2)

## Tipos de firmware

### BIOS

Una BIOS o *«Basic Input-Output System»* es el primer programa (firmware) que se ejecuta cuando el sistema es puesto en marcha. En la mayoría de los casos, este se almacena en una memoria flash en la propia placa base e independiente del almacenamiento del sistema. La BIOS lanza los primeros 440 bytes ([Master Boot Record](/index.php/Master_Boot_Record_(Espa%C3%B1ol) "Master Boot Record (Español)")) del primer disco según el orden de discos de la BIOS. Dado que se puede obtener muy poco de un programa que debe adaptarse solo a los primeros 440 bytes del disco, por lo general, un gestor de arranque común como [GRUB](/index.php/GRUB2_(Espa%C3%B1ol) "GRUB2 (Español)"), [Syslinux](/index.php/Syslinux_(Espa%C3%B1ol) "Syslinux (Español)") o [LILO](/index.php/LILO "LILO") sería cargado por la BIOS, el cual, seguidamente, se ocuparía de cargar el sistema operativo, ya sea cargando los sistemas en cadena, ya sea cargando directamente el kernel.

### UEFI

UEFI tiene la capacidad de leer tanto la tabla de particiones, como de reconocer los sistemas de archivos. Por lo tanto, no está restringido por la limitación del código de los 440 bytes (código de arranque del MBR) como en los sistemas BIOS. No utiliza el código de arranque MBR en absoluto.

Los firmwares UEFI comunmente utilizados dan apoyo tanto a los sistemas de particionado MBR como GPT. Las EFI de Apple son conocidas por apoyar mapas de particionado Apple, además de MBR y GPT. La mayoría de los firmwares UEFI tienen soporte para acceder a sistemas de archivos FAT12 (disquetes), FAT16 y FAT32 en discos duros, y ISO9660 (y UDF) en CD/DVD. El firmware EFI en Apple puede acceder también a HFS/HFS+, aparte de los mencionados.

UEFI no ejecuta ningún código de arranque del MBR, tanto si existe como si no. En su lugar, utiliza una partición especial de la tabla de particiones, llamada **EFI SYSTEM PARTITION** (partición del sistema EFI), en la que se guardan los archivos necesarios para ser lanzado el firmware. Cada proveedor puede almacenar sus archivos en la carpeta `<EFI SYSTEM PARTITION>/EFI/<FABRICANTE>/` y pueden usar el firmware o la shell (shell de UEFI) para iniciar el programa de arranque. Una partición del sistema EFI usa, por lo general, el formato FAT32 (principalmente) o FAT16.

Bajo UEFI, todos los programas que son cargados por un sistema operativo o por otros instrumentos (como aplicaciones de pruebas de memoria) o herramientas de recuperación fuera del sistema operativo, deben ser aplicaciones UEFI correspondiente a la arquitectura del firmware EFI. La mayor parte de los firmware UEFI en el mercado, incluyendo los recientes Mac de Apple, usan un firmware EFI x86_64\. Solo algunos Mac antiguos (anteriores a 2008) que funcionan utilizando EFI IA32 (32-bit), algunos ultrabooks recientes de Intel Cloverfield y algunas placas bases de Intel Servers, son conocidos por operar con un firmware EFI 1.10 de Intel.

Un firmware EFI x86_64 no incluye el soporte para lanzar aplicaciones de 32-bit (a diferencia del EFI de Linux y de Windows x86_64 que incluyen dicho apoyo). En definitiva, la aplicación UEFI (esto es, el gestor de arranque) debe ser compilada para la arquitectura correcta.

## Procesos de arranque

### Bajo BIOS

1.  Encendido del sistema —Power On Self Test—, o proceso [POST](https://en.wikipedia.org/wiki/es:POST "wikipedia:es:POST").
2.  Después del POST la BIOS inicializa el hardware necesario para el arranque del sistema (disco, controladores del teclado, etc.).
3.  La BIOS ejecuta el código de los primeros 440 bytes (la región del código de arranque del MBR) del primer disco de los que aparecen ordenados en la BIOS.
4.  El código de arranque del MBR entonces toma el control desde la BIOS y ejecuta el código de la siguiente etapa (en su caso) (normalmente, el código del gestor de arranque).
5.  El código (segunda etapa) lanzado (el gestor de arranque presente) entonces lee los archivos de configuración y apoyo.
6.  En base a los datos de los archivos de configuración, el gestor de arranque carga el kernel e initramfs en la memoria del sistema (RAM), e inicia el kernel.

### Bajo UEFI

Véase la página principal: [Proceso de arranque bajo UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#Proceso_de_arranque_bajo_UEFI "Unified Extensible Firmware Interface (Español)") .

## Gestor de arranque

El [gestor de arranque](/index.php/Boot_loader_(Espa%C3%B1ol) "Boot loader (Español)") es la primera pieza de software iniciada por [BIOS](https://en.wikipedia.org/wiki/BIOS deseados, y el [disco RAM inicial](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") en función de los archivos de configuración.

**Nota:** La carga de las actualizaciones de [microcódigo](/index.php/Microcode_(Espa%C3%B1ol) "Microcode (Español)") requiere unos ajustes en la configuración del gestor de arranque. [[1]](https://www.archlinux.org/news/changes-to-intel-microcodeupdates/)

### Comparación de características

**Nota:**

*   Los gestores de arranque solo necesitan soporte del sistema de archivos en el que residen el kernel e initramfs (el sistema de archivos en el que se encuentra `/boot`).
*   Como GPT es parte de la especificación UEFI, todos los gestores de arranque UEFI soportan discos GPT. Es posible usar GPT en sistemas BIOS mediante el "arranque híbrido" con [MBR híbrido](https://www.rodsbooks.com/gdisk/hybrid.html), o el nuevo protocolo [GPT-only](http://repo.or.cz/syslinux.git/blob/HEAD:/doc/gpt.txt). Sin embargo, este protocolo puede causar problemas con ciertas implementaciones de BIOS; consulte [rodsbooks](http://www.rodsbooks.com/gdisk/bios.html#bios) para más detalles.
*   El cifrado mencionado en la compatibilidad del sistema de archivos es un [cifrado a nivel de sistema de archivos](https://en.wikipedia.org/wiki/Filesystem-level_encryption "wikipedia:Filesystem-level encryption"), no tiene relación con el [cifrado a nivel de bloque](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)").

| Nombre | Firmware | Multi-arranque | [Sistemas de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)") | Notas |
| BIOS | [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)") | [Btrfs](/index.php/Btrfs "Btrfs") | [ext4](/index.php/Ext4_(Espa%C3%B1ol) "Ext4 (Español)") | ReiserFS v3 | [VFAT](/index.php/VFAT "VFAT") | [XFS](/index.php/XFS "XFS") |
| [EFISTUB](/index.php/EFISTUB_(Espa%C3%B1ol) "EFISTUB (Español)") | – | Si | – | – | – | – | Solo ESP | – | Kernel convertido en ejecutable EFI para ser iniciado directamente desde el firmware [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)") u otro gestor de arranque. |
| [Clover](/index.php/Clover "Clover") | Emula UEFI | Si | Si | No | Sin cifrado | No | Si | No | Bifurcación de rEFIt modificada para ejecutar [macOS en hardware que no es de Apple](https://en.wikipedia.org/wiki/es:Hackintosh "wikipedia:es:Hackintosh"). |
| [GRUB](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") | Si | Si | Si | Sin compresión zstd | Si | Si | Si | Si | En la configuración de BIOS/GPT requiere una [partición de arranque BIOS](/index.php/BIOS_boot_partition "BIOS boot partition").
Soporta RAID, LUKS1 y LVM (pero no volúmenes aprovisionados ligeros). |
| [rEFInd](/index.php/REFInd "REFInd") | No | Si | Si | Sin: cifrado, compresión zstd | Sin cifrado | Sin características *tail-packing* | Si | No | Soporta autodetección de kernel y parámetros sin configuración explícita. |
| [Syslinux](/index.php/Syslinux_(Espa%C3%B1ol) "Syslinux (Español)") | Si | [Parcial](/index.php/Syslinux_(Espa%C3%B1ol)#Limitaciones_de_Syslinux_en_la_modalidad_UEFI "Syslinux (Español)") | [Parcial](/index.php/Syslinux_(Espa%C3%B1ol)#Chainloading "Syslinux (Español)") | Sin: volúmenes multi-dispositivo, compresión, cifrado | Sin cifrado | No | Si | v4 en [MBR](/index.php/Partitioning_(Espa%C3%B1ol)#Master_Boot_Record "Partitioning (Español)") solo | No admite ciertas características de los [sistemas de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)") [[2]](http://www.syslinux.org/wiki/index.php?title=Filesystem) |
| [systemd-boot](/index.php/Systemd-boot_(Espa%C3%B1ol) "Systemd-boot (Español)") | No | Si | Si | No | No | No | Solo ESP | No | No se pueden ejecutar binarios desde particiones que no sean [ESP](/index.php/EFI_system_partition "EFI system partition"). |
| [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") | Sin GPT | No | Si | No | No | Si | Si | Solo v4 | [Descontinuado](https://www.gnu.org/software/grub/grub-legacy.html) a favor de [GRUB](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)"). |
| [LILO](/index.php/LILO_(Espa%C3%B1ol) "LILO (Español)") | Sin GPT | No | Si | No | Sin cifrado | Si | Si | Solo MBR [[3]](http://xfs.org/index.php/XFS_FAQ#Q:_Does_LILO_work_with_XFS.3F) | [Descontinuado](http://web.archive.org/web/20180323163248/http://lilo.alioth.debian.org/) debido a sus limitaciones (por ejemplo, con Btrfs, GPT, RAID). |

### Véase también

*   [Rod Smith - Administrando EFI Boot Loaders para Linux](http://www.rodsbooks.com/efi-bootloaders/)
*   [Comparación de administradores de arranque](https://en.wikipedia.org/wiki/Comparison_of_boot_loaders "wikipedia:Comparison of boot loaders")

## Kernel

El kernel es el núcleo de un sistema operativo. Funciona en un nivel bajo (*kernelspace*) que interactúa entre el hardware de la máquina y los programas que utilizan los recursos del hardware para funcionar. Para hacer un uso eficiente de la CPU, el kernel utiliza un sistema de programación para arbitrar qué tareas tienen prioridad en un momento dado, creando la ilusión (para la precepción humana) que varias tareas se están ejecutando simultáneamente.

## initramfs

Después de estar cargado, el Kernel descomprime la imagen [initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") (sistema de archivos RAM inicial), que se convierte en el sistema de ficheros root inicial. El kernel seguidamente ejecuta `/init` como el primer proceso. El primer espacio de usuario (*«early userspace»*) comienza.

El propósito de initramfs es arrancar el sistema hasta el punto donde se puede acceder al sistema de archivos raíz (consulte [FHS](/index.php/Frequently_asked_questions_(Espa%C3%B1ol)#.C2.BFSigue_Arch_el_est.C3.A1ndar_de_jerarqu.C3.ADa_del_sistema_de_archivos_de_la_Fundaci.C3.B3n_Linux_.28FHS.29.3F "Frequently asked questions (Español)") para más detalles). Esto significa que los módulos que se requieren para dispositivos como IDE, SCSI, SATA, USB/FW (si el arranque se realiza desde una unidad externa) deben ser cargados desde initramfs si no están compilados en el kernel; una vez que los módulos necesarios se cargan (ya sea de forma explícita a través de un programa o script, o implícitamente a través de [udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)")), el proceso de arranque continúa. Por esta razón, el initramfs sólo debe contener los módulos necesarios para acceder al sistema de archivos raíz, no tiene por qué contener todos los módulos que sirven al completo funcionamiento de la máquina. La mayoría de los módulos se cargarán más tarde por udev, durante la fase init.

## Fase init

En la etapa final del *«early userspace»*, el verdadero sistema de archivos root es montado, y pasa a sustituir al sistema de archivos root inicial. `/sbin/init` se ejecuta, sustituyendo al proceso `/init`. Arch Linux utiliza [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") como proceso init.

## Getty

[init](/index.php/Init "Init") lanza las [getty](/index.php/Getty "Getty"), una para cada [terminal virtual](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") (normalmente seis de ellas), las cuales inicializan cada tty pidiendo el nombre de usuario y contraseña. Una vez que se proporcionan el nombre de usuario y la contraseña, getty los compara con las que se encuentran en `/etc/passwd`, llamando a continuación al programa [login](#Login), para que, una vez inicida la sesión de usuario, lance la shell de usuario de acuerdo con lo definido en `/etc/passwd`. Alternativamente, getty puede iniciar directamente un gestor de pantallas si existe uno presente en el sistema.

## Gestor de pantallas

Si hay un [gestor de pantallas (o gestor de inicio de sesión)](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)") instalado, este se ejecutará en la tty configurada, reemplazando el prompt de inicio de la getty. En su defecto, si no hay un gestor de pantallas, se mostrará el prompt de getty que pedirá en modo texto al usuario las credenciales, para poder realizar [inicio de sesión](#Login).

## Login

El programa *login* inicia una sesión para el usuario mediante el establecimiento de las variables de entorno y arranca la shell del usuario, basada en `/etc/passwd`.

## Shell

Una vez que la [shell](/index.php/Shell "Shell") del usuario se inicia, normalmente ejecuta un archivo de configuración runtime, como por ejemplo [.bashrc](/index.php/.bashrc ".bashrc"), antes de presentar un prompt para el usuario. Si la cuenta está configurada para [iniciar X al iniciar sesión](/index.php/Start_X_at_login_(Espa%C3%B1ol) "Start X at login (Español)"), el archivo de configuración mencionado llamará a [startx](/index.php/Startx "Startx") o [xinit](/index.php/Xinit "Xinit").

## GUI, xinit o wayland

[xinit](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)") ejecuta el archivo de configuración [xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)") del usuario , que normalmente inicia un [administrador de ventanas](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)"). Cuando el usuario finaliza y sale del administrador de ventanas, xinit, startx, el shell y el inicio de sesión finalizarán en ese orden, volviendo a getty.

## Véase también

*   [Early Userspace en Arch Linux](https://web.archive.org/web/20150430223035/http://archlinux.me/brain0/2010/02/13/early-userspace-in-arch-linux/)
*   [El Proceso de Arranque de Linux desde Dentro](http://www.ibm.com/developerworks/linux/library/l-linuxboot/)
*   [Wikipedia: Proceso de inicio de Linux](https://en.wikipedia.org/wiki/es:Proceso_de_arranque_en_Linux "wikipedia:es:Proceso de arranque en Linux")
*   [Wikipedia: initrd](https://en.wikipedia.org/wiki/es:initrd "wikipedia:es:initrd")
*   [Del Arranque de Linux con GRUB en Modo Single User](http://www.cyberciti.biz/faq/grub-boot-into-single-user-mode/)
*   [NeoSmart: El proceso de arranque BIOS/MBR](https://neosmart.net/wiki/mbr-boot-process/)
*   [Kernel Newbie Corner: initrd e initramfs](https://www.linux.com/learn/kernel-newbie-corner-initrd-and-initramfs-whats)