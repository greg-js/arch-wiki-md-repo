Para arrancar Arch Linux, un [gestor de arranque](/index.php/Boot_loaders "Boot loaders") capaz de iniciar Linux, como [GRUB](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") o [Syslinux](/index.php/Syslinux_(Espa%C3%B1ol) "Syslinux (Español)"), debe estar instalado en el [Master Boot Record](/index.php/Master_Boot_Record_(Espa%C3%B1ol) "Master Boot Record (Español)") o la [GUID Partition Table](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)"). El gestor de arranque es el responsable de cargar el kernel y el [ramdisk inicial](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") antes de iniciarse el proceso de arranque. El proceso es bastante diferente según se trate de un sistema [BIOS](https://en.wikipedia.org/wiki/es:BIOS "wikipedia:es:BIOS") o de [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)"), cuyos detalles se describen en esta página o en las enlazadas.

## Contents

*   [1 Tipos de firmware](#Tipos_de_firmware)
    *   [1.1 BIOS](#BIOS)
    *   [1.2 UEFI](#UEFI)
*   [2 Procesos de arranque](#Procesos_de_arranque)
    *   [2.1 Bajo BIOS](#Bajo_BIOS)
    *   [2.2 Bajo UEFI](#Bajo_UEFI)
*   [3 Kernel](#Kernel)
*   [4 initramfs](#initramfs)
*   [5 Fase init](#Fase_init)
*   [6 Getty](#Getty)
*   [7 Gestor de pantallas](#Gestor_de_pantallas)
*   [8 Login](#Login)
*   [9 Shell](#Shell)
*   [10 xinit](#xinit)
*   [11 Véase también](#V.C3.A9ase_tambi.C3.A9n)

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

## Kernel

El kernel es el núcleo de un sistema operativo. Funciona en un nivel bajo (*kernelspace*) que interactúa entre el hardware de la máquina y los programas que utilizan los recursos del hardware para funcionar. Para hacer un uso eficiente de la CPU, el kernel utiliza un sistema de programación para arbitrar qué tareas tienen prioridad en un momento dado, creando la ilusión (para la precepción humana) que varias tareas se están ejecutando simultáneamente.

## initramfs

Después de estar cargado, el Kernel descomprime la imagen [initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") (sistema de archivos RAM inicial), que se convierte en el sistema de ficheros root inicial. El kernel seguidamente ejecuta `/init` como el primer proceso. El primer espacio de usuario (*«early userspace»*) comienza.

El propósito de initramfs es arrancar el sistema hasta el punto donde se puede acceder al sistema de archivos raíz (consulte [FHS](/index.php/FHS "FHS") para más detalles). Esto significa que los módulos que se requieren para dispositivos como IDE, SCSI, SATA, USB/FW (si el arranque se realiza desde una unidad externa) deben ser cargados desde initramfs si no están compilados en el kernel; una vez que los módulos necesarios se cargan (ya sea de forma explícita a través de un programa o script, o implícitamente a través de [udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)")), el proceso de arranque continúa. Por esta razón, el initramfs sólo debe contener los módulos necesarios para acceder al sistema de archivos raíz, no tiene por qué contener todos los módulos que sirven al completo funcionamiento de la máquina. La mayoría de los módulos se cargarán más tarde por udev, durante la fase init.

## Fase init

En la etapa final del *«early userspace»*, el verdadero sistema de archivos root es montado, y pasa a sustituir al sistema de archivos root inicial. `/sbin/init` se ejecuta, sustituyendo al proceso `/init`. Arch Linux utiliza [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") como proceso init.

## Getty

[init](/index.php/Init "Init") lanza las [getty](/index.php/Getty "Getty"), una para cada [terminal virtual](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") (normalmente seis de ellas), las cuales inicializan cada tty pidiendo el nombre de usuario y contraseña. Una vez que se proporcionan el nombre de usuario y la contraseña, getty los compara con las que se encuentran en `/etc/passwd`, llamando a continuación al programa [login](#Login), para que, una vez inicida la sesión de usuario, lance la shell de usuario de acuerdo con lo definido en `/etc/passwd`. Alternativamente, getty puede iniciar directamente un gestor de pantallas si existe uno presente en el sistema.

## Gestor de pantallas

Si hay un [gestor de pantallas (o gestor de inicio de sesión)](/index.php/Display_Manager_(Espa%C3%B1ol) "Display Manager (Español)") instalado, este se ejecutará en la tty configurada, reemplazando el prompt de inicio de la getty. En su defecto, si no hay un gestor de pantallas, se mostrará el prompt de getty que pedirá en modo texto al usuario las credenciales, para poder realizar [inicio de sesión](#Login).

## Login

El programa *login* inicia una sesión para el usuario mediante el establecimiento de las variables de entorno y arranca la shell del usuario, basada en `/etc/passwd`.

## Shell

Una vez que la [shell](/index.php/Shell "Shell") del usuario se inicia, normalmente ejecuta un archivo de configuración runtime, como por ejemplo [.bashrc](/index.php/.bashrc ".bashrc"), antes de presentar un prompt para el usuario. Si la cuenta está configurada para [iniciar X al iniciar sesión](/index.php/Start_X_at_Login_(Espa%C3%B1ol) "Start X at Login (Español)"), el archivo de configuración mencionado llamará a [startx](/index.php/Startx "Startx") o [xinit](/index.php/Xinit "Xinit").

## xinit

[xinit](/index.php/Xinit "Xinit") ejecuta el archivo de configuración del usuario [.xinitrc](/index.php/.xinitrc ".xinitrc"), que normalmente arrancará un [gestor de ventanas](/index.php/Window_Manager_(Espa%C3%B1ol) "Window Manager (Español)"). Cuando el usuario ha terminado y sale del gestor de ventanas, xinit, startx, la shell, y el programa login terminarán en ese orden, devolviéndonos a getty.

## Véase también

*   [Early Userspace en Arch Linux](http://archlinux.me/brain0/2010/02/13/early-userspace-in-arch-linux/)
*   [El Proceso de Arranque de Linux desde Dentro](http://www.ibm.com/developerworks/linux/library/l-linuxboot/)
*   [Boot con GRUB](http://www.linuxjournal.com/article/4622)
*   [Wikipedia: Proceso de inicio de Linux](https://en.wikipedia.org/wiki/es:Proceso_de_arranque_en_Linux "wikipedia:es:Proceso de arranque en Linux")
*   [Wikipedia: initrd](https://en.wikipedia.org/wiki/es:initrd "wikipedia:es:initrd")
*   [Del Arranque de Linux con GRUB en Modo Single User](http://www.cyberciti.biz/faq/grub-boot-into-single-user-mode/)