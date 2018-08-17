**Estado de la traducción:** este artículo es una versión traducida de [Installation guide](/index.php/Installation_guide "Installation guide"). Fecha de la última traducción/revisión: **2018-08-16**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Installation_guide&diff=0&oldid=529413).

Este documento es una guía para la instalación de [Arch Linux](/index.php/Arch_Linux_(Espa%C3%B1ol) "Arch Linux (Español)") desde un sistema live arrancado con la imagen de instalación oficial. Antes de proceder a la instalación, es recomendable que eche un vistazo a las [preguntas frecuentes](/index.php/Frequently_asked_questions_(Espa%C3%B1ol) "Frequently asked questions (Español)"). Para conocer las convenciones utilizadas en este documento, consulte [Ayuda:Lectura](/index.php/Help:Reading_(Espa%C3%B1ol) "Help:Reading (Español)"). En particular, los ejemplos de código pueden contener marcadores de posición (resaltados en cursiva) que deberán reemplazarse manualmente.

Para obtener instrucciones más detalladas, consulte los artículos relacionados de [ArchWiki](/index.php/ArchWiki:About_(Espa%C3%B1ol) "ArchWiki:About (Español)"), o las [páginas del manual](/index.php/Man_page_(Espa%C3%B1ol) "Man page (Español)") de los distintos programas, con enlaces para ambos a lo largo de esta guía. Para obtener ayuda interactiva, el [canal IRC](/index.php/IRC_channel_(Espa%C3%B1ol) "IRC channel (Español)") y los [foros](https://bbs.archlinux.org/) están disponibles.

Arch Linux puede ejecutarse en cualquier máquina compatible [x86_64](https://en.wikipedia.org/wiki/es:X86-64 "wikipedia:es:X86-64") con al menos 512 MB de RAM. Una instalación básica con todos los paquetes del grupo [base](https://www.archlinux.org/groups/x86_64/base/) debería ocupar menos de 800 MB de espacio en disco. Como el proceso de instalación necesita recuperar paquetes de un repositorio remoto, esta guía asume que hay disponible una conexión a Internet.

## Contents

*   [1 Preinstalación](#Preinstalaci.C3.B3n)
    *   [1.1 Definición de la distribución de teclado](#Definici.C3.B3n_de_la_distribuci.C3.B3n_de_teclado)
    *   [1.2 Comprobación del modo de arranque](#Comprobaci.C3.B3n_del_modo_de_arranque)
    *   [1.3 Conexión a Internet](#Conexi.C3.B3n_a_Internet)
    *   [1.4 Actualización del reloj del sistema](#Actualizaci.C3.B3n_del_reloj_del_sistema)
    *   [1.5 Particionado del disco](#Particionado_del_disco)
    *   [1.6 Formateo de las particiones](#Formateo_de_las_particiones)
    *   [1.7 Montaje de los sistemas de archivos](#Montaje_de_los_sistemas_de_archivos)
*   [2 Instalación](#Instalaci.C3.B3n)
    *   [2.1 Selección de los servidores de réplica](#Selecci.C3.B3n_de_los_servidores_de_r.C3.A9plica)
    *   [2.2 Instalación de los paquetes del sistema base](#Instalaci.C3.B3n_de_los_paquetes_del_sistema_base)
*   [3 Configuración del sistema](#Configuraci.C3.B3n_del_sistema)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Zona horaria](#Zona_horaria)
    *   [3.4 Idioma del sistema](#Idioma_del_sistema)
    *   [3.5 Configuración de red](#Configuraci.C3.B3n_de_red)
    *   [3.6 Initramfs](#Initramfs)
    *   [3.7 Contraseña de superusuario *(root)*](#Contrase.C3.B1a_de_superusuario_.28root.29)
    *   [3.8 Gestor de arranque](#Gestor_de_arranque)
*   [4 Reinicio](#Reinicio)
*   [5 Posinstalación](#Posinstalaci.C3.B3n)

## Preinstalación

Descargue e inicie el soporte de instalación como se explica en la categoría [obtener e instalar Arch](/index.php/Category:Getting_and_installing_Arch_(Espa%C3%B1ol) "Category:Getting and installing Arch (Español)"). Se iniciará sesión en la primera [consola virtual](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") como superusuario *(root)*, y se le presentará un intérprete de comandos [Zsh](/index.php/Zsh "Zsh").

Para cambiar a una consola diferente —por ejemplo, para ver esta guía con [ELinks](/index.php/ELinks "ELinks") junto con la instalación— utilice el [atajo](/index.php/Keyboard_shortcuts "Keyboard shortcuts") `Alt+*flecha*`. Para [editar](/index.php/Textedit "Textedit") archivos de configuración, dispone de [nano](/index.php/Nano_(Espa%C3%B1ol)#Uso "Nano (Español)"), [vi](https://en.wikipedia.org/wiki/es:vi "wikipedia:es:vi") y [vim](/index.php/Vim_(Espa%C3%B1ol)#Gu.C3.ADa_r.C3.A1pida_de_VIM "Vim (Español)").

### Definición de la distribución de teclado

La [distribución de teclado de la consola](/index.php/Console_keymap "Console keymap") predeterminada es la [US](https://en.wikipedia.org/wiki/es:File:KB_United_States-NoAltGr.svg "wikipedia:es:File:KB United States-NoAltGr.svg"). Las distribuciones de teclado disponibles se pueden listar con:

```
# ls /usr/share/kbd/keymaps/**/*.map.gz

```

Para modificar la distribución de teclado, añada un nombre de archivo correspondiente a [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1), omitiendo la ruta y la extensión del archivo. Por ejemplo, para establecer un diseño de teclado en [español](https://en.wikipedia.org/wiki/es:File:KB_Spanish.svg "wikipedia:es:File:KB Spanish.svg"):

```
# loadkeys es

```

Los [tipos de letras para consola](/index.php/Fonts#Console_fonts "Fonts") se encuentran en `/usr/share/kbd/consolefonts/` y se pueden configurar igualmente con [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8).

### Comprobación del modo de arranque

Si el modo UEFI está activado en una placa base [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)"), [Archiso](/index.php/Archiso_(Espa%C3%B1ol) "Archiso (Español)") [arrancará](/index.php/Arch_boot_process_(Espa%C3%B1ol) "Arch boot process (Español)") a través de [systemd-boot](/index.php/Systemd-boot_(Espa%C3%B1ol) "Systemd-boot (Español)"). Para comprobarlo, liste el contenido del directorio [efivars](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#Variables_de_UEFI "Unified Extensible Firmware Interface (Español)"):

```
# ls /sys/firmware/efi/efivars

```

Si el directorio no existe, el sistema puede iniciarse en modo [BIOS](https://en.wikipedia.org/wiki/es:BIOS "wikipedia:es:BIOS") o CSM. Consulte el manual de su placa base para más detalles.

### Conexión a Internet

La imagen de instalación habilita el demonio [dhcpcd](/index.php/Dhcpcd "Dhcpcd") para el uso de una tarjeta de [red cableada](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) en el arranque. La conexión se puede comprobar con [ping](https://en.wikipedia.org/wiki/es:Ping "wikipedia:es:Ping"):

```
# ping archlinux.org

```

Si no hay disponible una conexión, [detenga](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)") el servicio *dhcpcd* con `systemctl stop dhcpcd@*interfaz*` donde `*interfaz*` puede ser [autocompletado con tabulador](https://en.wikipedia.org/wiki/Command-line_completion "wikipedia:Command-line completion"). Proceda a configurar la red como se describe en la [configuración de red](/index.php/Network_configuration_(Espa%C3%B1ol) "Network configuration (Español)").

### Actualización del reloj del sistema

Utilice [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) para asegurarse de que el reloj del sistema sea preciso:

```
# timedatectl set-ntp true

```

Para comprobar el estado del servicio, utilice `timedatectl status`.

### Particionado del disco

Cuando el sistema lo reconoce, los discos se asignan como [dispositivos de bloques](https://en.wikipedia.org/wiki/Device_file#Naming_conventions o *fdisk*.

```
# fdisk -l

```

Los resultados que terminan en `rom`, `loop` o `airoot` pueden ignorarse.

Las siguientes *particiones* son **necesarias** para el dispositivo elegido:

*   Una partición para el directorio raíz `/`.
*   Si [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)") está habilitado, una [partición del sistema EFI](/index.php/EFI_system_partition "EFI system partition").

**Nota:** El [espacio de intercambio *(swap)*](/index.php/Swap "Swap") se puede establecer en una partición separada o en un [archivo](/index.php/Swap_(Espa%C3%B1ol)#Archivo_swap "Swap (Español)").

Para modificar la *tablas de particiones*, utilice [fdisk](/index.php/Fdisk "Fdisk") o [parted](/index.php/GNU_Parted "GNU Parted").

```
# fdisk /dev/*sda*

```

Consulte [particionado](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)") para más información.

**Nota:** Si desea crear dispositivos de bloques apilados *(stacked block devices)* para [LVM](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)"), [cifrado de disco](/index.php/Disk_encryption_(Espa%C3%B1ol) "Disk encryption (Español)") o [RAID](/index.php/RAID_(Espa%C3%B1ol) "RAID (Español)"), hágalo ahora.

### Formateo de las particiones

Una vez creadas las particiones, cada una de ellas debe formatearse con un [sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)") apropiado. Por ejemplo, para formatear la partición raíz en `/dev/*sda1*` con `*ext4*`, ejecute:

```
# mkfs.*ext4* /dev/*sda1*

```

Si creó una partición para el espacio de intercambio *(swap)* (por ejemplo `/dev/*sda3*`), inicialícela con *mkswap*:

```
# mkswap /dev/*sda3*
# swapon /dev/*sda3*

```

Consulte [Crear un sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol)#Crear_un_sistema_de_archivos "File systems (Español)") para más detalles.

### Montaje de los sistemas de archivos

[Monte](/index.php/Mount "Mount") el sistema de archivos de la partición raíz en `/mnt`, por ejemplo:

```
# mount /dev/*sda1* /mnt

```

Cree puntos de montaje para cualquier partición restante y móntelos en consecuencia:

```
# mkdir /mnt/*boot*
# mount /dev/*sda2* /mnt/*boot*

```

[genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in) detectará posteriormente los sistemas de archivos montados y el espacio de intercambio.

## Instalación

### Selección de los servidores de réplica

Los paquetes que se instalarán se deben descargar desde los [servidores de réplicas](/index.php/Mirrors_(Espa%C3%B1ol) "Mirrors (Español)"), que se definen en `/etc/pacman.d/mirrorlist`. En el sistema para la instalación *(live)*, todas las réplicas están habilitadas y ordenadas por su estado de sincronización y velocidad en el momento en que se creó la imagen de instalación.

Cuanto más alto se coloque una réplica en la lista, más prioridad tendrá cuando descargue un paquete. Es posible que quiera editar el archivo y mover las réplicas geográficamente más cercanas hacia la parte superior de la lista, aunque deben tenerse en cuenta otros criterios.

Este archivo será luego copiado al nuevo sistema por *pacstrap*, por lo que vale la pena hacerlo bien.

### Instalación de los paquetes del sistema base

Utilice el script [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) para instalar el grupo de paquetes [base](https://www.archlinux.org/groups/x86_64/base/):

```
# pacstrap /mnt base

```

Este grupo no incluye todas las herramientas del sistema que está empleando para la instalación, como [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) o firmware inalámbrico específico; consulte [paquetes.x86_64](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) para una comparación.

Para [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") paquetes y otros grupos como [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), añada los nombres a *pacstrap* (separados por un espacio) o comandos individuales [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") después del paso [chroot](#Chroot).

## Configuración del sistema

### Fstab

Genere un archivo [fstab](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)") (utilice `-U` o `-L` para definir por [UUID](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol)#by-uuid "Persistent block device naming (Español)") o etiquetas, respectivamente):

```
# genfstab -U /mnt >> /mnt/etc/fstab

```

Luego, compruebe el archivo resultante en `/mnt/etc/fstab` y modifíquelo en caso de errores.

### Chroot

[Cambie la raíz](/index.php/Change_root_(Espa%C3%B1ol) "Change root (Español)") al nuevo sistema:

```
# arch-chroot /mnt

```

### Zona horaria

Establezca la [zona horaria](/index.php/Time_(Espa%C3%B1ol)#Huso_horario "Time (Español)"):

```
# ln -sf /usr/share/zoneinfo/*Región*/*Ciudad* /etc/localtime

```

**Nota:** *(del traductor)* para España —excepto en las islas Canarias— sería:
```
# ln -sf /usr/share/zoneinfo/Europe/Madrid /etc/localtime

```

Ejecute [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8) para generar `/etc/adjtime`:

```
# hwclock --systohc

```

Este comando asume que el reloj del hardware está configurado en [UTC](https://en.wikipedia.org/wiki/es:Tiempo_universal_coordinado para más detalles.

### Idioma del sistema

Descomente `en_US.UTF-8 UTF-8` y otros [locale](/index.php/Locale_(Espa%C3%B1ol) "Locale (Español)") necesarios en `/etc/locale.gen` (por ejemplo en España sería `es_ES.UTF-8 UTF-8`), y genérelos con:

```
# locale-gen

```

Establezca la [variable](/index.php/Environment_variables_(Espa%C3%B1ol) "Environment variables (Español)") `LANG` en [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5), por ejemplo:

 `/etc/locale.conf`  `LANG=*es_ES.UTF-8*` 

Si ha establecido la [distribución de teclado](#Definir_la_distribuci.C3.B3n_del_teclado) anteriormente, haga que los cambios sean persistentes en [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5):

 `/etc/vconsole.conf`  `KEYMAP=*es*` 

### Configuración de red

Cree el archivo [hostname](/index.php/Network_configuration_(Espa%C3%B1ol)#Establecer_el_nombre_del_equipo "Network configuration (Español)"):

 `/etc/hostname` 
```
*elnombredemiequipo*

```

Añada las entradas coincidentes a [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5):

 `/etc/hosts` 
```
127.0.0.1	localhost
::1		localhost
127.0.1.1	*elnombredemiequipo*.localdomain	*elnombredemiequipo*

```

Si el sistema tiene una dirección IP permanente, se debe usar en lugar de `127.0.1.1`.

Complete la [configuración de red](/index.php/Network_configuration_(Espa%C3%B1ol) "Network configuration (Español)") para el entorno recién instalado.

### Initramfs

Por lo general, no es necesario crear un nuevo *initramfs* porque se ejeca [mkinitcpio](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") durante la instalación del paquete [linux](https://www.archlinux.org/packages/?name=linux) con *pacstrap*.

Para configuraciones especiales, modifique el archivo [mkinitcpio.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.conf.5) y vuelva a crear la imagen de initramfs:

```
# mkinitcpio -p linux

```

### Contraseña de superusuario *(root)*

Establezca la [contraseña](/index.php/Users_and_groups_(Espa%C3%B1ol)#Base_de_datos_del_usuario "Users and groups (Español)") del superusuario

```
# passwd

```

### Gestor de arranque

Se debe instalar un gestor de arranque compatible con Linux para iniciar Arch Linux. Consulte la categoría sobre [gestores de arranque](/index.php/Category:Boot_loaders_(Espa%C3%B1ol) "Category:Boot loaders (Español)") para conocer las opciones disponibles.

Si tiene una CPU Intel, instale además el paquete [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode), y [habilite las actualizaciones de microcódigo](/index.php/Microcode_(Espa%C3%B1ol)#Activaci.C3.B3n_de_las_actualizaciones_del_microc.C3.B3digo_de_Intel "Microcode (Español)").

## Reinicio

Salga del entorno chroot escribiendo `exit` o presionando `Ctrl+D`.

Opcionalmente, puede desmontar manualmente todas las particiones con `umount -R /mnt`: esto permite detectar las particiones «ocupadas» y encontrar la causa con [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1).

Finalmente, reinicie la máquina escribiendo `reboot`: cualquier partición que todavía esté montada será desmontada automáticamente por *systemd*. Recuerde retirar los medios de instalación y luego inicie sesión en el nuevo sistema con la cuenta de superusuario.

## Posinstalación

Consulte las [recomendaciones generales](/index.php/General_recommendations_(Espa%C3%B1ol) "General recommendations (Español)") para obtener instrucciones para la administración del sistema y tutoriales posteriores a la instalación (como configurar una interfaz gráfica de usuario, sonido o un panel táctil).

Para obtener una lista de aplicaciones que pueden ser de interés, consulte esta [lista de aplicaciones](/index.php/List_of_applications_(Espa%C3%B1ol) "List of applications (Español)").