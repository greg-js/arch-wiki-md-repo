**Estado de la traducción**
Este artículo es una traducción de [Arch boot process](/index.php/Arch_boot_process "Arch boot process"), revisada por última vez el **2018-10-08**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Arch_boot_process&diff=0&oldid=546665) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Master Boot Record](/index.php/Master_Boot_Record_(Espa%C3%B1ol) "Master Boot Record (Español)")
*   [GUID Partition Table](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)")
*   [mkinitcpio](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)")
*   [init](/index.php/Init "Init")
*   [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)")
*   [fstab](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)")
*   [Autostarting](/index.php/Autostarting_(Espa%C3%B1ol) "Autostarting (Español)")

Para iniciar Arch Linux, debe configurarse un [gestor de arranque](#Gestor_de_arranque) capaz de iniciar Linux. El gestor de arranque es el responsable de cargar el kernel y el [disco ram inicial](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") antes de iniciar el proceso de arranque. El proceso es bastante diferente para los sistemas [BIOS](https://en.wikipedia.org/wiki/es:BIOS "wikipedia:es:BIOS") y [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)"), cuyos detalles se describen en esta página o en las enlazadas.

## Contents

*   [1 Tipos de firmware](#Tipos_de_firmware)
    *   [1.1 BIOS](#BIOS)
    *   [1.2 UEFI](#UEFI)
*   [2 Inicialización del sistema](#Inicializaci.C3.B3n_del_sistema)
    *   [2.1 Bajo BIOS](#Bajo_BIOS)
    *   [2.2 Bajo UEFI](#Bajo_UEFI)
    *   [2.3 Arranque múltiple en UEFI](#Arranque_m.C3.BAltiple_en_UEFI)
*   [3 Gestor de arranque](#Gestor_de_arranque)
    *   [3.1 Comparación de características](#Comparaci.C3.B3n_de_caracter.C3.ADsticas)
*   [4 Kernel](#Kernel)
*   [5 initramfs](#initramfs)
*   [6 Proceso de inicio (Init)](#Proceso_de_inicio_.28Init.29)
*   [7 Getty](#Getty)
*   [8 Gestor de pantallas](#Gestor_de_pantallas)
*   [9 Inicio de sesión](#Inicio_de_sesi.C3.B3n)
*   [10 Intérprete de órdenes](#Int.C3.A9rprete_de_.C3.B3rdenes)
*   [11 GUI, xinit o wayland](#GUI.2C_xinit_o_wayland)
*   [12 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Tipos de firmware

### BIOS

Una [BIOS](https://en.wikipedia.org/wiki/es:BIOS "wikipedia:es:BIOS") o sistema básico de entrada-salida *(Basic Input-Output System)* es el primer programa (firmware) que se ejecuta una vez que se enciende el sistema. En la mayoría de los casos, se almacena en una memoria flash en la propia placa base e independiente del almacenamiento del sistema.

### UEFI

[UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)") tiene soporte para leer tanto la tabla de particiones como los sistemas de archivos. UEFI no ejecuta ningún código de arranque en el MBR, exista o no, en su lugar el arranque depende de las entradas de arranque en la NVRAM.

La especificación UEFI exige el soporte para los sistemas de archivos [FAT12, FAT16, y FAT32](/index.php/FAT "FAT") (véase [Especificación UEFI versión 2.7, sección 13.3.1.1](http://www.uefi.org/sites/default/files/resources/UEFI%20Spec%202_7_A%20Sept%206.pdf#G17.1019485)), pero cualquier proveedor puede añadir opcionalmente soporte para sistemas de archivos adicionales; por ejemplo, Apple [Mac](/index.php/Mac "Mac") admite (y de forma predeterminada) sus propios controladores de sistema de archivos HFS+. Las implementaciones UEFI también son compatibles con ISO-9660 para discos ópticos.

UEFI lanza aplicaciones EFI, por ejemplo. [gestores de arranque](#Gestor_de_arranque), [intérpretes de órdenes UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#Int.C3.A9rprete_de_.C3.B3rdenes_UEFI "Unified Extensible Firmware Interface (Español)"), etc. Estas aplicaciones generalmente se almacenan como archivos en la [partición del sistema EFI](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)"). Cada proveedor puede almacenar sus archivos en la partición del sistema EFI en la carpeta `/EFI/*nombre del proveedor*`. Las aplicaciones se pueden iniciar añadiendo una entrada de arranque a la NVRAM o desde el intérprete de órdenes UEFI.

## Inicialización del sistema

### Bajo BIOS

1.  Encendido del sistema, se ejecuta la [autoprueba de encendido (POST)](https://en.wikipedia.org/wiki/es:POST "wikipedia:es:POST").
2.  Después del POST, la BIOS inicializa el hardware del sistema necesario para el inicio (disco, controladores de teclado, etc.).
3.  BIOS inicia los primeros 440 bytes ([el área del código de arranque del MBR](/index.php/Partitioning#Master_Boot_Record_.28bootstrap_code.29 "Partitioning")) del primer disco según el orden de la BIOS.
4.  La primera etapa del cargador de arranque en el código de arranque del MBR, luego inicia el código de su segunda etapa (si existe) desde:
    *   sectores de discos siguientes tras el MBR, por ejemplo la denominada brecha posterior al MBR (solo en la tabla de particiones MBR).
    *   un disco de partición o un disco sin partición [volume boot record (VBR)](https://en.wikipedia.org/wiki/Volume_boot_record "wikipedia:Volume boot record").
    *   la [partición de inicio de BIOS](/index.php/BIOS_boot_partition_(Espa%C3%B1ol) "BIOS boot partition (Español)") ([GRUB](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") solo en BIOS/GPT).
5.  Se inicia el [gestor de arranque](#Gestor_de_arranque).
6.  El gestor de arranque carga un sistema operativo ya sea en cadena o cargando directamente el kernel del sistema operativo.

### Bajo UEFI

1.  Encendido del sistema, se ejecuta la [autoprueba de encendido (POST)](https://en.wikipedia.org/wiki/es:POST "wikipedia:es:POST").
2.  UEFI inicializa el hardware requerido para el arranque.
3.  El firmware lee las entradas de arranque en la NVRAM para determinar qué aplicación EFI se lanzará y desde dónde (por ejemplo, desde qué disco y partición).
    *   Una entrada de arranque podría simplemente ser un disco. En este caso, el firmware busca una [partición del sistema EFI](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)") en ese disco e intenta encontrar una aplicación EFI en la ruta de arranque alternativa `\EFI\BOOT\BOOTX64.EFI` (`BOOTIA32.EFI` en [IA32 (32 bits) sistemas EFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#Firmware_de_UEFI "Unified Extensible Firmware Interface (Español)")). Así es como funcionan los medios extraíbles de arranque UEFI.
4.  El firmware lanza la aplicación EFI.
    *   Podría ser un [gestor de arranque](#Gestor_de_arranque) o el [kernel](/index.php/Kernel_(Espa%C3%B1ol) "Kernel (Español)") de Arch usando [EFISTUB](/index.php/EFISTUB_(Espa%C3%B1ol) "EFISTUB (Español)").
    *   Podría ser alguna otra aplicación EFI, como un intérprete de órdenes UEFI o un [gestor de arranque](#Gestor_de_arranque) como [systemd-boot](/index.php/Systemd-boot_(Espa%C3%B1ol) "Systemd-boot (Español)") o [rEFInd](/index.php/REFInd "REFInd").

Si el [inicio seguro](/index.php/Secure_Boot "Secure Boot") está habilitado, el proceso de arranque verificará la autenticidad del binario EFI por la firma.

**Nota:** Algunos sistemas UEFI solo pueden arrancar desde la ruta de inicio alternativa.

### Arranque múltiple en UEFI

Dado que cada sistema operativo o proveedor puede mantener sus propios archivos dentro de la partición del sistema EFI sin afectar al otro, el arranque múltiple con UEFI es simplemente una cuestión de iniciar una aplicación EFI diferente correspondiente al gestor de arranque del sistema operativo en particular. Esto elimina la necesidad de confiar en los mecanismos de carga en cadena de un [gestor de arranque](#Gestor_de_arranque) para cargar otro sistema operativo.

Véase también [Arranque dual con Windows](/index.php/Dual_boot_with_Windows_(Espa%C3%B1ol) "Dual boot with Windows (Español)").

## Gestor de arranque

El gestor de arranque es la primera pieza de software iniciada por [BIOS](https://en.wikipedia.org/wiki/BIOS deseados, y el [disco RAM inicial](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") en función de los archivos de configuración.

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

Véase también [Wikipedia:Comparación de gestores de arranque](https://en.wikipedia.org/wiki/Comparison_of_boot_loaders "wikipedia:Comparison of boot loaders")

## Kernel

El [kernel](/index.php/Kernel_(Espa%C3%B1ol) "Kernel (Español)") es el núcleo de un sistema operativo. Funciona en un nivel bajo (*kernelspace*) que interactúa entre el hardware de la máquina y los programas que utilizan los recursos del hardware para funcionar. Para hacer un uso eficiente de la CPU, el kernel utiliza un sistema de programación para arbitrar qué tareas tienen prioridad en un momento dado, creando la ilusión de varias tareas siendo ejecutadas simultáneamente.

## initramfs

Una vez cargado el kernel, este desempaqueta el [initramfs](/index.php/Initramfs_(Espa%C3%B1ol) "Initramfs (Español)") (sistema de archivos RAM inicial), que se convierte en el sistema de archivos raíz inicial. El kernel ejecuta entonces `/init` como el primer proceso. El *espacio de usuario inicial* comienza.

El propósito de initramfs es arrancar el sistema hasta el punto en que pueda acceder al sistema de archivos raíz (véase [FHS](/index.php/FHS_(Espa%C3%B1ol) "FHS (Español)") para obtener más información). Esto significa que cualquier módulo que se requiera para dispositivos como IDE, SCSI, SATA, USB/FW (si se arranca desde una unidad externa) debe poder cargarse desde initramfs si no está integrado en el kernel; Una vez que se cargan los módulos adecuados (ya sea explícitamente a través de un programa o script, o implícitamente a través de [udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)")), el proceso de arranque continúa. Por esta razón, el initramfs solo necesita contener los módulos necesarios para acceder al sistema de archivos raíz; no es necesario que contenga todos los módulos que uno quiera usar. La mayoría de los módulos se cargarán más tarde por udev, durante el proceso de inicio *(Init)*.

## Proceso de inicio (Init)

En la etapa final del espacio de usuario inicial, la verdadera raíz se monta y luego reemplaza el sistema de archivos raíz inicial. Se ejecuta `/sbin/init`, reemplazando el proceso `/init`. Arch utiliza [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") como [init](/index.php/Init "Init") predeterminado.

## Getty

[init](/index.php/Init "Init") llama a [getty](/index.php/Getty_(Espa%C3%B1ol) "Getty (Español)") una vez por cada [terminal virtual](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") (típicamente seis de ellos), lo que inicializa cada tty y solicita un nombre de usuario y una contraseña. Una vez que se proporcionan el nombre de usuario y la contraseña, getty los compara con `/etc/passwd` y `/etc/shadow`, luego llama al [inicio de sesión](#Inicio_de_sesi.C3.B3n). Alternativamente, getty puede iniciar un gestor de pantalla si hay uno presente en el sistema.

## Gestor de pantallas

Se puede configurar un [gestor de pantalla](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)") para reemplazar el indicador de inicio de sesión getty en un tty.

## Inicio de sesión

El programa *login* inicia una sesión para el usuario configurando variables de entorno e iniciando el intérprete de órdenes del usuario, basado en `/etc/passwd`.

El programa *login* muestra el contenido de [/etc/motd](https://en.wikipedia.org/wiki/motd_(Unix) (mensaje del día) después de un inicio de sesión exitoso, justo antes de que se ejecute el intérprete de órdenes de inicio de sesión. Es un buen lugar para mostrar sus términos de servicio para recordar a los usuarios sus políticas locales o cualquier cosa que desee decirles.

## Intérprete de órdenes

Una vez que el [intérprete de órdenes](/index.php/Shell "Shell") del usuario se inicia, normalmente ejecutará un archivo de configuración, como [bashrc](/index.php/Bashrc_(Espa%C3%B1ol) "Bashrc (Español)"), antes de presentar el indicador del intérprete de órdenes al usuario. Si la cuenta está configurada para [arrancar X al iniciar sesión](/index.php/Start_X_at_login_(Espa%C3%B1ol) "Start X at login (Español)"), el archivo de configuración llamará a [startx](/index.php/Startx_(Espa%C3%B1ol) "Startx (Español)") o [xinit](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)").

## GUI, xinit o wayland

[xinit](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)") ejecuta el archivo de configuración [xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)") del usuario, que normalmente inicia un [gestor de ventanas](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)"). Cuando el usuario finaliza y sale del gestor de ventanas, xinit, startx, el intérprete de órdenes y el inicio de sesión finalizarán en ese orden, volviendo a getty.

## Véase también

*   [Early Userspace en Arch Linux](https://web.archive.org/web/20150430223035/http://archlinux.me/brain0/2010/02/13/early-userspace-in-arch-linux/)
*   [El Proceso de Arranque de Linux desde Dentro](http://www.ibm.com/developerworks/linux/library/l-linuxboot/)
*   [Wikipedia: Proceso de inicio de Linux](https://en.wikipedia.org/wiki/es:Proceso_de_arranque_en_Linux "wikipedia:es:Proceso de arranque en Linux")
*   [Wikipedia: initrd](https://en.wikipedia.org/wiki/es:initrd "wikipedia:es:initrd")
*   [Del Arranque de Linux con GRUB en Modo Single User](http://www.cyberciti.biz/faq/grub-boot-into-single-user-mode/)
*   [NeoSmart: El proceso de arranque BIOS/MBR](https://neosmart.net/wiki/mbr-boot-process/)
*   [Kernel Newbie Corner: initrd e initramfs](https://www.linux.com/learn/kernel-newbie-corner-initrd-and-initramfs-whats)
*   [Rod Smith - Manejando los gestores de arranque EFI para Linux](http://www.rodsbooks.com/efi-bootloaders/)