**Estado de la traducción:** este artículo es una versión traducida de [Installation guide](/index.php/Installation_guide "Installation guide"). Fecha de la última traducción/revisión: **2015-10-13**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Installation_guide&diff=0&oldid=404204).

Este documento es una guía para la instalación de [Arch Linux (Español)](/index.php/Arch_Linux_(Espa%C3%B1ol) "Arch Linux (Español)") desde un sistema live arrancado con la imagen de instalación oficial. Antes de proceder a la instalación, es recomendable que le eche un vistazo a [FAQ (Español)](/index.php/FAQ_(Espa%C3%B1ol) "FAQ (Español)"). Si lo que busca es una guía de instalación detallada y altamente explicativa remítase a la [Guía para principiantes](/index.php/Beginners%27_guide_(Espa%C3%B1ol) "Beginners' guide (Español)"), o a la categoría [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch") para conocer casos específicos de instalación.

La mayoría de la ayuda se puede encontrar en la wiki o a través de las [páginas del manual](/index.php/Man_page "Man page") de los distintos programas; consulte [archlinux(7)](https://projects.archlinux.org/svntogit/packages.git/tree/filesystem/trunk/archlinux.7.txt) para una descripción general de la configuración. Para obtener ayuda interactiva, el [canal IRC](/index.php/IRC_Channel_(Espa%C3%B1ol) "IRC Channel (Español)") y los [foros](https://bbs.archlinux.org/) también los tiene disponibles.

## Contents

*   [1 Preinstalación](#Preinstalaci.C3.B3n)
    *   [1.1 Distribución del teclado en el entorno live](#Distribuci.C3.B3n_del_teclado_en_el_entorno_live)
    *   [1.2 Conectarse a Internet](#Conectarse_a_Internet)
    *   [1.3 Actualizar el reloj del sistema](#Actualizar_el_reloj_del_sistema)
    *   [1.4 Particionar el disco](#Particionar_el_disco)
    *   [1.5 Formatear las particiones](#Formatear_las_particiones)
    *   [1.6 Montar las particiones](#Montar_las_particiones)
*   [2 Instalación](#Instalaci.C3.B3n)
    *   [2.1 Seleccionar servidores de réplica](#Seleccionar_servidores_de_r.C3.A9plica)
    *   [2.2 Instalar los paquetes del sistema base](#Instalar_los_paquetes_del_sistema_base)
    *   [2.3 Configurar el sistema](#Configurar_el_sistema)
    *   [2.4 Instalar un gestor de arranque](#Instalar_un_gestor_de_arranque)
    *   [2.5 Reiniciar](#Reiniciar)
*   [3 Posinstalación](#Posinstalaci.C3.B3n)

## Preinstalación

*   Descargue e inicie el soporte de instalación como se explica en [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch"), y, a continuación, siga con el resto de esta guía.

*   El proceso de instalación necesita obtener los paquetes de un repositorio remoto, por lo tanto, se requiere una conexión a Internet funcional.

### Distribución del teclado en el entorno live

*   La distribución del teclado por defecto es la de EE.UU.
*   Hay disponibles distribuciones de teclado alternativas que se pueden cargar con la orden `loadkeys *archivo_keymap*`: los archivos de mapas de teclas se pueden encontrar en la carpeta `/usr/share/kbd/keymaps/` (no es necesario especificar la ruta ni la extensión del archivo cuando se usa «loadkeys»).

### Conectarse a Internet

*   El servicio de Internet a través de DHCP está activado en el arranque para los dispositivos cableados compatibles; leer más en [Network configuration (Español)](/index.php/Network_configuration_(Espa%C3%B1ol) "Network configuration (Español)").
*   Para los dispositivos inalámbricos compatibles ejecute `wifi-menu`, para configurar la conexión de red; leer más en [Wireless network configuration (Español)](/index.php/Wireless_network_configuration_(Espa%C3%B1ol) "Wireless network configuration (Español)").
*   Si se necesita configurar una dirección IP estática o utilizar herramientas de gestión de redes, hay que detener el servicio DHCP con la orden `systemctl stop dhcpcd@*eth0*.service`, y consultar [Netctl (Español)](/index.php/Netctl_(Espa%C3%B1ol) "Netctl (Español)").

### Actualizar el reloj del sistema

*   Consultar [systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd").

### Particionar el disco

*   Consultar [Partitioning (Español)](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)") para obtener más detalles sobre cómo realizar el particionado.
*   Puede que sea necesario crear algunas particiones especiales, por ejemplo, si se está utilizando (U)EFI —Interfaz Extensible del Firmware (Unificada)—, lo más probable es que se necesite otra partición para albergar la partición del sistema EFI, ver [EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#EFI_System_Partition "Unified Extensible Firmware Interface (Español)"); y, si se planea instalar GRUB en un sistema con tabla de particionado GPT, necesitará una [BIOS boot partition para GRUB](/index.php/GRUB_(Espa%C3%B1ol)#Instrucciones_espec.C3.ADficas_para_GUID_Partition_Table_.28GPT.29 "GRUB (Español)").
*   Hay que crear, en esta fase de la instalación, los dispositivos de bloques apilados —stacked block devices— para [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)"), [Disk encryption (Español)](/index.php/Disk_encryption_(Espa%C3%B1ol) "Disk encryption (Español)") o [RAID (Español)](/index.php/RAID_(Espa%C3%B1ol) "RAID (Español)"), si se diera el caso.

### Formatear las particiones

*   Consultar [File systems (Español)](/index.php/File_systems_(Espa%C3%B1ol)#Crear_un_sistema_de_archivos "File systems (Español)") y, opcionalmente, [Swap (Español)](/index.php/Swap_(Espa%C3%B1ol) "Swap (Español)"), para obtener más información sobre cómo formatear un dispositivo.

### Montar las particiones

*   El siguiente paso es montar la partición del sistema —root— en `/mnt`.
*   Después de esto, hay que crear tantos directorios como particiones haya realizado y montarlas (`/mnt/boot`, `/mnt/home`, ...).
*   También hay que activar la partición *swap*, si se dispone de una, para que pueda ser detectada más tarde cuando ejecute *genfstab*.

## Instalación

### Seleccionar servidores de réplica

*   Editar `/etc/pacman.d/mirrorlist` y seleccionar uno o varios servidores de descarga.
*   Los servidores de réplica regionales, por lo general, funcionan mejor; sin embargo, la cercanía no es el único criterio para discernir sobre la calidad de los mirrors, leer más sobre ello en [Mirrors (Español)](/index.php/Mirrors_(Espa%C3%B1ol) "Mirrors (Español)").
*   Una copia del archivo `mirrorlist` se realizará, más tarde, en el nuevo sistema por *pacstrap*, por lo que vale la pena hacerlo bien en esta fase.

### Instalar los paquetes del sistema base

*   Utilizar el script [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) para instalar el grupo de paquetes [base](https://www.archlinux.org/groups/x86_64/base/): `# pacstrap /mnt base` 

*   Otros paquetes o grupos de paquetes pueden ser instalados añadiendo sus nombres a la orden anterior (separados por espacios), pudiendo incluir, por ejemplo, el gestor de arranque.

### Configurar el sistema

*   Generar un archivo [fstab (Español)](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)") (utilizar el parámetro `-U` o `-L` para especificar en dicho archivo las UUID o las etiquetas, respectivamente, de las particiones): `# genfstab -p /mnt >> /mnt/etc/fstab` 

*   Entrar en el nuevo sistema como [Change root (Español)](/index.php/Change_root_(Espa%C3%B1ol) "Change root (Español)"): `# arch-chroot /mnt` 

*   Configurar el [nombre del equipo](/index.php/Configuring_Network_(Espa%C3%B1ol)#Establecer_el_nombre_del_equipo "Configuring Network (Español)"): `# echo *nombre_equipo* > /etc/hostname` 

*   Configurar el [uso horario](/index.php/Time_(Espa%C3%B1ol)#Uso_horario "Time (Español)"): `# ln -sf /usr/share/zoneinfo/*zone*/*subzone* /etc/localtime` 

*   Configurar el [idioma del sistema](/index.php/Locale_(Espa%C3%B1ol) "Locale (Español)") descomentando el locale necesario en el archivo `/etc/locale.gen`, y después generarlo con la orden: `# locale-gen` 

*   Configurar las preferencias del idioma en `/etc/locale.conf` y, quizás también, en `$HOME/.config/locale.conf`: `# echo LANG=*nuestro_locale* > /etc/locale.conf` 

*   Configurar la [distribución del teclado](/index.php/Keyboard_configuration_in_console_(Espa%C3%B1ol) "Keyboard configuration in console (Español)") para la consola y las preferencias del [tipo de letra](/index.php/Fonts#Console_fonts "Fonts") de la misma en `/etc/vconsole.conf`.

*   Configurar la red de nuevo para el entorno recién instalado: consultar [Network configuration (Español)](/index.php/Network_configuration_(Espa%C3%B1ol) "Network configuration (Español)") y [Wireless network configuration (Español)](/index.php/Wireless_network_configuration_(Espa%C3%B1ol) "Wireless network configuration (Español)").

*   Configurar [/etc/mkinitcpio.conf](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") si es necesario añadirle funcionalidades adicionales. Crear una imagen RAM inicial nueva con la orden: `# mkinitcpio -p linux` 

*   Establecer la contraseña de root: `# passwd` 

### Instalar un gestor de arranque

*   Consultar [Boot loaders (Español)](/index.php/Boot_loaders_(Espa%C3%B1ol) "Boot loaders (Español)") para conocer las opciones y configuraciones disponibles.

### Reiniciar

*   Salir del entorno chroot escribiendo `exit` o presionando `Ctrl+D`.

*   Opcionalmente, desmontar manualmente todas las particiones con `umount -R /mnt`: esto permite advertir cualquier partición «ocupada», y buscar su causa con [fuser](https://en.wikipedia.org/wiki/fuser_(Unix) "wikipedia:fuser (Unix)").

*   Por último, reiniciar el equipo escribiendo `reboot`: cualquier partición que todavía siga montada será desmontada automáticamente por *systemd*. Recuerde que debe retirar el soporte de instalación y, luego, iniciar sesión en el nuevo sistema con la cuenta de root.

## Posinstalación

*   Véase el artículo [General recommendations (Español)](/index.php/General_recommendations_(Espa%C3%B1ol) "General recommendations (Español)") para obtener indicaciones sobre cómo gestionar el sistema, así como tutoriales sobre qué hacer después de la instalación del sistema base (como pueden ser temas relativos a la instalación y configuración de una interfaz gráfica de usuario, la del sonido o la del panel táctil).

*   Para obtener una lista de las aplicaciones que pueden ser de su interés, consulte [List of Applications (Español)](/index.php/List_of_Applications_(Espa%C3%B1ol) "List of Applications (Español)").