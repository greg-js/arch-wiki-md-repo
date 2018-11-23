**Estado de la traducción**
Este artículo es una traducción de [Installation guide](/index.php/Installation_guide "Installation guide"), revisada por última vez el **2018-11-22**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Installation_guide&diff=0&oldid=549392) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Este documento es una guía para la instalación de [Arch Linux (Español)](/index.php/Arch_Linux_(Espa%C3%B1ol) "Arch Linux (Español)") desde un sistema live arrancado con la imagen de instalación oficial. Antes de proceder a la instalación, es recomendable que eche un vistazo a las [Frequently asked questions (Español)](/index.php/Frequently_asked_questions_(Espa%C3%B1ol) "Frequently asked questions (Español)"). Para conocer las convenciones utilizadas en este documento, consulte [Help:Reading (Español)](/index.php/Help:Reading_(Espa%C3%B1ol) "Help:Reading (Español)"). En particular, los ejemplos de código pueden contener marcadores de posición (resaltados en `*cursiva*`) que deberán reemplazarse manualmente.

Para obtener instrucciones más detalladas, consulte los artículos relacionados de [ArchWiki (Español)](/index.php/ArchWiki_(Espa%C3%B1ol) "ArchWiki (Español)"), o las [páginas de los manuales](/index.php/Man_page "Man page") de los distintos programas, con enlaces para ambos a lo largo de esta guía. Para obtener ayuda interactiva, el [IRC channel (Español)](/index.php/IRC_channel_(Espa%C3%B1ol) "IRC channel (Español)") y los [foros](https://bbs.archlinux.org/) están disponibles.

Arch Linux puede ejecutarse en cualquier máquina compatible [x86_64](https://en.wikipedia.org/wiki/es:X86-64 "wikipedia:es:X86-64") con al menos 512 MB de RAM. Una instalación básica con todos los paquetes del grupo [base](https://www.archlinux.org/groups/x86_64/base/) debería ocupar menos de 800 MB de espacio en disco. Dado que el proceso de instalación necesita obtener los paquetes desde un repositorio remoto, necesitará una conexión a Internet funcional.

## Contents

*   [1 Preinstalación](#Preinstalación)
    *   [1.1 Definir la distribución del teclado en el entorno live](#Definir_la_distribución_del_teclado_en_el_entorno_live)
    *   [1.2 Verificar la modalidad de arranque](#Verificar_la_modalidad_de_arranque)
    *   [1.3 Conectarse a Internet](#Conectarse_a_Internet)
    *   [1.4 Actualizar el reloj del sistema](#Actualizar_el_reloj_del_sistema)
    *   [1.5 Particionar el disco](#Particionar_el_disco)
    *   [1.6 Formatear las particiones](#Formatear_las_particiones)
    *   [1.7 Montar los sistemas de archivos](#Montar_los_sistemas_de_archivos)
*   [2 Instalación](#Instalación)
    *   [2.1 Seleccionar los servidores de réplica](#Seleccionar_los_servidores_de_réplica)
    *   [2.2 Instalar los paquetes del sistema base](#Instalar_los_paquetes_del_sistema_base)
*   [3 Configuración del sistema](#Configuración_del_sistema)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Zona horaria](#Zona_horaria)
    *   [3.4 Idioma del sistema](#Idioma_del_sistema)
    *   [3.5 Configurar la red](#Configurar_la_red)
    *   [3.6 Initramfs](#Initramfs)
    *   [3.7 Contraseña de root](#Contraseña_de_root)
    *   [3.8 Instalar gestor de arranque](#Instalar_gestor_de_arranque)
*   [4 Reiniciar](#Reiniciar)
*   [5 Posinstalación](#Posinstalación)

## Preinstalación

Descargue e inicie el soporte de instalación como se explica en [obtener e instalar Arch](/index.php/Getting_and_installing_Arch_(Espa%C3%B1ol) "Getting and installing Arch (Español)"). Se iniciará sesión en la primera [consola virtual](https://en.wikipedia.org/wiki/es:Consola_Virtual "wikipedia:es:Consola Virtual") como superusuario *(root)*, y se le presentará un intérprete de órdenes [Zsh](/index.php/Zsh "Zsh").

Para cambiar a una consola diferente —por ejemplo, para ver esta guía con [ELinks](/index.php/ELinks "ELinks") junto con la instalación— utilice el [atajo](/index.php/Keyboard_shortcuts "Keyboard shortcuts") `Alt+*flecha*`. Para [editar](/index.php/Textedit "Textedit") archivos de configuración, dispone de [nano](/index.php/Nano_(Espa%C3%B1ol)#Uso "Nano (Español)"), [vi](https://en.wikipedia.org/wiki/es:vi "wikipedia:es:vi") y [vim](/index.php/Vim_(Espa%C3%B1ol)#Guía_rápida_de_VIM "Vim (Español)").

### Definir la distribución del teclado en el entorno live

Por defecto, [la distribución del teclado de la consola](/index.php/Fonts_(Espa%C3%B1ol) "Fonts (Español)") es la de [EE.UU.](https://en.wikipedia.org/wiki/es:File:KB_United_States-NoAltGr.svg "wikipedia:es:File:KB United States-NoAltGr.svg"). Las distribuciones de teclado disponibles se pueden enumerar con: `# ls /usr/share/kbd/keymaps/**/*.map.gz` 

La distribución del teclado se puede cambiar con la orden [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1), añadiendo el nombre de un archivo (no es necesario especificar la ruta ni la extensión del archivo cuando se usa «loadkeys»). Por ejemplo, para establecer ua distribución de teclado en [español](https://en.wikipedia.org/wiki/es:File:KB_Spanish.svg "wikipedia:es:File:KB Spanish.svg"), ejecute:

```
# loadkeys es

```

Los [tipos de letras para consola](/index.php/Console_fonts "Console fonts") se encuentran en `/usr/share/kbd/consolefonts/` y se pueden configurar igualmente con [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8).

### Verificar la modalidad de arranque

Si el modo UEFI está activado en una placa base [UEFI (Español)](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)"), [Archiso (Español)](/index.php/Archiso_(Espa%C3%B1ol) "Archiso (Español)") [arrancará](/index.php/Arch_boot_process_(Espa%C3%B1ol) "Arch boot process (Español)") en consecuencia a través de [systemd-boot (Español)](/index.php/Systemd-boot_(Espa%C3%B1ol) "Systemd-boot (Español)"). Para comprobar esto, liste el contenido del directorio [efivars](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#Variables_de_UEFI "Unified Extensible Firmware Interface (Español)"):

```
# ls /sys/firmware/efi/efivars

```

Si no existe el directorio, el sistema se iniciará en modo [BIOS](https://en.wikipedia.org/wiki/es:BIOS "wikipedia:es:BIOS") o CSM (*Compatibility Support Module*). Remítase al manual de su placa base para obtener detalles.

### Conectarse a Internet

El servicio de Internet a través del demonio [dhcpcd](/index.php/Dhcpcd "Dhcpcd") está [activado](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) en el arranque para los dispositivos **cableados**. Compruebe que su conexión se ha establecido, utilizando la herramienta [ping](https://en.wikipedia.org/wiki/es:Ping "wikipedia:es:Ping"):

```
# ping archlinux.org

```

Si no hay disponible una conexión, [detenga](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)") el servicio *dhcpcd* con la orden `systemctl stop dhcpcd@*interfaz*` donde `*interfaz*` puede ser [autocompletado con el tabulador](https://en.wikipedia.org/wiki/Command-line_completion "wikipedia:Command-line completion"). Proceda a configurar la red como se describe en [Network configuration (Español)](/index.php/Network_configuration_(Espa%C3%B1ol) "Network configuration (Español)").

### Actualizar el reloj del sistema

Utilice [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) para asegurarse de que el reloj del sistema sea preciso:

```
# timedatectl set-ntp true

```

Para comprobar el estado del servicio, utilice `timedatectl status`.

### Particionar el disco

Cuando el sistema lo reconoce, los discos se asignan como [dispositivos de bloques](https://en.wikipedia.org/wiki/Device_file#Naming_conventions "wikipedia:Device file") como `/dev/sda` o `/dev/nvme0n1`. Para identificar estos dispositivos, utilice [lsblk](/index.php/Lsblk "Lsblk") o *fdisk*:

```
# fdisk -l

```

Los resultados que terminan en `rom`, `loop` o `airoot` pueden ignorarse.

Las siguientes *particiones* son **necesarias** para el dispositivo elegido:

*   Una partición para el directorio raíz `/`.
*   Si [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)") está activado, una [partición del sistema EFI](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)").
    **Nota:** El [espacio de intercambio *(swap)*](/index.php/Swap_(Espa%C3%B1ol) "Swap (Español)") se puede establecer en una partición separada o en un [archivo](/index.php/Swap_(Espa%C3%B1ol)#Archivo_swap "Swap (Español)").

Para modificar la *tablas de particiones*, utilice [fdisk](/index.php/Fdisk "Fdisk") o [parted](/index.php/GNU_Parted "GNU Parted").

```
# fdisk /dev/*sda*

```

Consulte [Partitioning (Español)](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)") para más información.

**Nota:** Si desea crear dispositivos de bloques apilados —*stacked block devices*— para [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)"), [cifrado de disco](/index.php/Disk_encryption_(Espa%C3%B1ol) "Disk encryption (Español)") o [RAID (Español)](/index.php/RAID_(Espa%C3%B1ol) "RAID (Español)"), hágalo ahora.

### Formatear las particiones

Una vez se han creado las particiones, cada una de ellas debe formatearse con un [sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)") adecuado. Por ejemplo, para formatear la partición raíz situada en `/dev/*sda1*` con `*ext4*`, ejecute:

```
# mkfs.*ext4* /dev/*sda1*

```

Si creó una partición para el espacio de intercambio *(swap)* (por ejemplo `/dev/*sda3*`), formatéela con *mkswap* e iníciela con *swapon*:

```
# mkswap /dev/*sda3*
 # swapon /dev/*sda3*

```

Consulte [Crear un sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol)#Crear_un_sistema_de_archivos "File systems (Español)") para más detalles.

### Montar los sistemas de archivos

El siguiente paso es [montar](/index.php/Mount "Mount") el sistema de archivos de la partición raíz —root— en `/mnt`, por ejemplo:

```
# mount /dev/*sda1* /mnt

```

Después de esto, hay que crear tantos directorios como particiones haya realizado y montarlas, por ejemplo:

```
# mkdir /mnt/*boot*
# mount /dev/*sda2* /mnt/*boot*

```

Los sistemas de archivos montados, así como el espacio de intercambio, serán posteriormente detectados por [genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in).

## Instalación

### Seleccionar los servidores de réplica

Los paquetes que se instalarán se deben descargar desde los [servidores de réplicas](/index.php/Mirrors_(Espa%C3%B1ol) "Mirrors (Español)"), que se definen en `/etc/pacman.d/mirrorlist`. En el entorno live de instalación, todos los servidores de réplicas están activados y ordenados de acuerdo al estado de sincronización y velocidad en el momento de creación de la imagen de instalación.

Cuanto más alto se coloca un servidor de réplica en la lista, más prioridad tendrá al descargar un paquete. Es posible que desee modificar el archivo en consecuencia y mover los servidores de réplicas geográficamente más cercanos, a la parte superior de la lista, aunque se deben tener en consideración otros criterios.

Una copia del archivo «mirrorlist» se realizará más tarde en el nuevo sistema por *pacstrap*, por lo tanto vale la pena hacerlo bien en esta fase.

### Instalar los paquetes del sistema base

Utilice el script [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) para instalar el grupo de paquetes [base](https://www.archlinux.org/groups/x86_64/base/):*Ejecute [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8) para generar el archivo `/etc/adjtime`:

```
# pacstrap /mnt base

```

Este grupo de paquetes no incluye todas las herramientas disponibles en el entorno live de instalación, como son los casos de [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) o firmware inalámbrico específico; consulte [paquetes.x86_64](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) para ver la comparación.

Para [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalación_de_paquetes "Help:Reading (Español)") otros paquetes o grupos de paquetes, como [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), en el nuevo sistema, añada sus nombres a la orden *pacstrap* (separados por un espacio)o, posteriormente a la etapa de [#Chroot](#Chroot) , con órdenes individuales con [pacman (Español)](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)").

## Configuración del sistema

### Fstab

Genere un archivo [fstab (Español)](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)") (utilice `-U` o `-L` para especificar en dicho archivo las [UUID](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol)#by-uuid "Persistent block device naming (Español)") o las etiquetas, respectivamente):

```
# genfstab -U /mnt >> /mnt/etc/fstab

```

Compruebe el archivo resultante e `/mnt/etc/fstab` después, y modifíquelo en caso de errores.

### Chroot

[Cambie la raíz](/index.php/Change_root_(Espa%C3%B1ol) "Change root (Español)") al nuevo sistema:

```
# arch-chroot /mnt

```

### Zona horaria

Defina su [zona horaria](/index.php/System_time_(Espa%C3%B1ol)#Huso_horario "System time (Español)"):

```
# ln -sf /usr/share/zoneinfo/*Región*/*Ciudad* /etc/localtime

```

Ejecute [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8) para generar el archivo `/etc/adjtime`:

```
# hwclock --systohc

```

Esta orden presume que le reloj del hardware esta configurado en [UTC](https://en.wikipedia.org/wiki/es:Tiempo_universal_coordinado para obtener más detalles.

### Idioma del sistema

Descomente el [locale (Español)](/index.php/Locale_(Espa%C3%B1ol) "Locale (Español)") necesario (por ejemplo en España sería `es_ES.UTF-8 UTF-8`) en `/etc/locale.gen`, además de `en_US.UTF-8 UTF-8` y, después, genérelo con la orden:

```
# locale-gen

```

Defina la [variable](/index.php/Environment_variables_(Espa%C3%B1ol) "Environment variables (Español)") `LANG` en [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5) según su caso, por ejemplo:

 `/etc/locale.conf`  `LANG=*es_ES.UTF-8*` 

Si fuese necesario, defina la [distribución de teclado](#Definir_la_distribución_del_teclado_en_el_entorno_live) en [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5) para que permanezca en cada reinicio:

 `/etc/vconsole.conf`  `KEYMAP=*es*` 

### Configurar la red

Cree el archivo [hostname](/index.php/Network_configuration_(Espa%C3%B1ol)#Establecer_el_nombre_del_equipo "Network configuration (Español)"):

 `/etc/hostname` 
```
*elnombredemiequipo*

```

Considere añadir una entrada similar en [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5):

 `/etc/hosts` 
```
127.0.0.1	localhost
::1		localhost
127.0.1.1	*elnombredemiequipo*.localdomain	*elnombredemiequipo*

```

Si el sistema tiene una dirección IP permanente, se debe usar dicha dirección, en lugar de `127.0.1.1`.

[Configure la conexión de red](/index.php/Network_configuration_(Espa%C3%B1ol) "Network configuration (Español)") de nuevo para el entorno recién instalado.

### Initramfs

Normalmente no es necesario crear una imagen *initramfs* nueva, dado que [mkinitcpio (Español)](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") se ejecuta durante la instalación del paquete [linux](https://www.archlinux.org/packages/?name=linux) con *pacstrap*.

Cuando haga cambios especiales en la configuración de [mkinitcpio (Español)](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)"), cree una nueva imagen RAM inicial con:

```
# mkinitcpio -p linux

```

### Contraseña de root

Establezca la [contraseña](/index.php/Users_and_groups_(Espa%C3%B1ol)#Base_de_datos_del_usuario "Users and groups (Español)") de [root](https://en.wikipedia.org/wiki/es:Root "wikipedia:es:Root"):

```
# passwd

```

### Instalar gestor de arranque

Se debe instalar un gestor de arranque compatible con Linux para iniciar Arch Linux. Consulte [Category:Boot loaders (Español)](/index.php/Category:Boot_loaders_(Espa%C3%B1ol) "Category:Boot loaders (Español)") para conocer las opciones y configuraciones disponibles.

Si tiene una CPU Intel, además de instalar un gestor de arranque, instale el paquete [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) y active las actualizaciones de [Microcode (Español)](/index.php/Microcode_(Espa%C3%B1ol) "Microcode (Español)").

## Reiniciar

Salga del entorno chroot escribiendo `exit` o presionando `Ctrl+D`.

Opcionalmente, puede desmontar manualmente todas las particiones con `umount -R /mnt`: esto permite advertir cualquier partición «ocupada», y buscar su causa con [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1).

Por último, reinicie el equipo escribiendo `reboot`: cualquier partición que todavía esté montada será desmontada automáticamente por *systemd*. Recuerde retirar los medios de instalación y luego inicie sesión en el nuevo sistema con la cuenta de root.

## Posinstalación

Vea el artículo [General recommendations (Español)](/index.php/General_recommendations_(Espa%C3%B1ol) "General recommendations (Español)") para obtener instrucciones sobre cómo gestionar el sistema, así como tutoriales sobre qué hacer después de la instalación (tales como configurar una interfaz gráfica de usuario, el sonido o un panel táctil).

Para obtener una lista de aplicaciones que pueden ser de su interés, consulte [List of applications (Español)](/index.php/List_of_applications_(Espa%C3%B1ol) "List of applications (Español)").