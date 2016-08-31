**Estado de la traducción:** este artículo es una versión traducida de [Installation guide](/index.php/Installation_guide "Installation guide"). Fecha de la última traducción/revisión: **2016-08-23**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Installation_guide&diff=0&oldid=447580).

Este documento es una guía para la instalación de [Arch Linux (Español)](/index.php/Arch_Linux_(Espa%C3%B1ol) "Arch Linux (Español)") desde un sistema live arrancado con la imagen de instalación oficial. Antes de proceder a la instalación, es recomendable que le eche un vistazo a [FAQ (Español)](/index.php/FAQ_(Espa%C3%B1ol) "FAQ (Español)"). Para conocer las convenciones utilizadas en este documento, consulte [Help:Reading (Español)](/index.php/Help:Reading_(Espa%C3%B1ol) "Help:Reading (Español)").

Para obtener instrucciones más detalladas, consulte los artículos relacionados de [ArchWiki](/index.php/ArchWiki:About "ArchWiki:About") (accesibles desde el entorno live de instalación con [ELinks](/index.php/ELinks "ELinks")), o las [páginas de los manuales](/index.php/Man_page "Man page") de los distintos programas; vea [archlinux(7)](https://projects.archlinux.org/svntogit/packages.git/tree/filesystem/trunk/archlinux.7.txt) para una descripción general de la configuración. Para obtener ayuda interactiva, el [canal IRC](/index.php/IRC_channel_(Espa%C3%B1ol) "IRC channel (Español)") y los [foros](https://bbs.archlinux.org/) también los tiene disponibles.

## Contents

*   [1 Preinstalación](#Preinstalaci.C3.B3n)
    *   [1.1 Verificar el modo de arranque](#Verificar_el_modo_de_arranque)
    *   [1.2 Distribución del teclado en el entorno live](#Distribuci.C3.B3n_del_teclado_en_el_entorno_live)
    *   [1.3 Conectarse a Internet](#Conectarse_a_Internet)
    *   [1.4 Actualizar el reloj del sistema](#Actualizar_el_reloj_del_sistema)
    *   [1.5 Particionar el disco](#Particionar_el_disco)
    *   [1.6 Formatear las particiones](#Formatear_las_particiones)
    *   [1.7 Montar las particiones](#Montar_las_particiones)
*   [2 Instalación](#Instalaci.C3.B3n)
    *   [2.1 Seleccionar los servidores de réplica](#Seleccionar_los_servidores_de_r.C3.A9plica)
    *   [2.2 Instalar los paquetes del sistema base](#Instalar_los_paquetes_del_sistema_base)
*   [3 Configuración del sistema](#Configuraci.C3.B3n_del_sistema)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Zona horaria](#Zona_horaria)
    *   [3.4 Idioma del sistema](#Idioma_del_sistema)
    *   [3.5 Nombre del equipo](#Nombre_del_equipo)
    *   [3.6 Configuración de la conexión de red](#Configuraci.C3.B3n_de_la_conexi.C3.B3n_de_red)
    *   [3.7 Initramfs](#Initramfs)
    *   [3.8 Contraseña de root](#Contrase.C3.B1a_de_root)
    *   [3.9 Instalar un gestor de arranque](#Instalar_un_gestor_de_arranque)
*   [4 Reiniciar](#Reiniciar)
*   [5 Posinstalación](#Posinstalaci.C3.B3n)

## Preinstalación

*   Arch Linux puede ser ejecutado en cualquier máquina [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) compatible, con un mínimo de 256 MB de RAM. Una instalación básica con todos los paquetes del grupo [base](https://www.archlinux.org/groups/x86_64/base/) puede tomar alrededor de 800 MB de espacio en disco.

*   Descargue e inicie el soporte de instalación como se explica en [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch"). Iniciará sesión como usuario root, y se le presentará con el intérprete de órdenes [Zsh](/index.php/Zsh "Zsh"); órdenes comunes como [systemctl(1)](http://man7.org/linux/man-pages/man1/systemctl.1.html) pueden ser [completadas con el tabulador](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion").

*   Para [editar/modificar](/index.php/Edit "Edit") los archivos de configuración, dispone de los editores [nano](/index.php/Nano#Usage "Nano"), [vi](https://en.wikipedia.org/wiki/vi "w:vi") y [vim](/index.php/Vim#Usage "Vim") .

*   El proceso de instalación necesita obtener los paquetes desde un repositorio remoto, por lo tanto, necesitará una conexión a Internet funcional.

### Verificar el modo de arranque

*   Dado que las instrucciones difieren respecto de los sistemas de [UEFI](/index.php/UEFI "UEFI"), verifique el modo de arranque mediante la comprobación [efivars](/index.php/Efivars "Efivars"): `# ls /sys/firmware/efi/efivars` 

### Distribución del teclado en el entorno live

*   Por defecto, [la distribución del teclado de la consola](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") es la de [EE.UU.](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg"). Las opciones disponibles de los archivos de mapas de teclas se pueden enumerar con `ls /usr/share/kbd/keymaps/**/*.map.gz`.

*   La distribución del teclado se puede cambiar con la orden [loadkeys(1)](http://man7.org/linux/man-pages/man1/loadkeys.1.html), añadiendo el nombre de un archivo (no es necesario especificar la ruta ni la extensión del archivo cuando se usa «loadkeys»). Por ejemplo: `# loadkeys *es* (para especificar el teclado en español)` 

*   [Los tipos de letras para la consola](/index.php/Console_fonts "Console fonts") los puede encontrar en `/usr/share/kbd/consolefonts/`, y, como antes, se pueden ajustar con la orden [setfont(8)](http://man7.org/linux/man-pages/man8/setfont.8.html).

### Conectarse a Internet

*   El servicio de Internet a través de [dhcpcd](/index.php/Dhcpcd "Dhcpcd") está activado en el arranque para los dispositivos cableados compatibles; compruebe su conexión usando herramientas como [ping(8)](http://man7.org/linux/man-pages/man8/ping.8.html).

*   Para realizar otras [configuraciones de conexión red](/index.php/Wireless_configuration "Wireless configuration"), dispone de [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") y [netctl](/index.php/Netctl "Netctl") . Vea [systemd.network(5)](http://man7.org/linux/man-pages/man5/systemd.network.5.html) y [netctl.profile(5)](https://git.archlinux.org/netctl.git/tree/docs/netctl.profile.5.txt) para obtener ejemplos.

*   Cuando utilice cualquiera de estos últimos servicios, [detenga](/index.php/Stop "Stop") el servicio `dhcpcd@*nombre_de_la_interfaz*.service`: `# systemctl stop dhcpcd@*nombre_de_la_interfaz*.service` 

### Actualizar el reloj del sistema

*   Utilice [timedatectl(1)](http://man7.org/linux/man-pages/man1/timedatectl.1.html) para asegurarse de que la hora del sistema es correcta: `# timedatectl set-ntp true` 

*   Para comprobar el estado del servicio, utilice `timedatectl status`.

### Particionar el disco

*   Para modificar y ver las [tablas de particionado](/index.php/Partition_table "Partition table"), utilice [fdisk](/index.php/Fdisk "Fdisk") o [parted](/index.php/Parted "Parted") tanto para [MBR](/index.php/MBR "MBR") como para [GPT](/index.php/GPT "GPT"), o [gdisk](/index.php/Gdisk "Gdisk") para GPT únicamente.

*   Es necesario, al menos, una partición disponible en el directorio `/`. Los sistemas [UEFI](/index.php/UEFI "UEFI") requieren una partición adicional llamada [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition"). También, puede que sea necesario crear otras particiones, como por ejemplo la [partición de arranque de la BIOS para GRUB (BIOS boot partition)](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB").

*   En esta fase de la instalación, también hay que crear los dispositivos de bloques apilados —stacked block devices— para [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)"), [Disk encryption (Español)](/index.php/Disk_encryption_(Espa%C3%B1ol) "Disk encryption (Español)") o [RAID (Español)](/index.php/RAID_(Espa%C3%B1ol) "RAID (Español)"), si se diera el caso.

### Formatear las particiones

*   Las particiones se formatean aplicándoles un sistema de archivos.

*   Los [sistemas de archivos](/index.php/File_systems "File systems") se crean utilizando las herramientas [mkfs(8)](http://man7.org/linux/man-pages/man8/mkfs.8.html), o [mkswap(8)](http://man7.org/linux/man-pages/man8/mkswap.8.html) en el caso de los espacios [swap](/index.php/Swap "Swap"). Consulte [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems") para obtener más detalles.

### Montar las particiones

*   El siguiente paso es montar la partición del sistema —root— en `/mnt`.

*   Después de esto, hay que crear tantos directorios como particiones haya realizado y montarlas (`/mnt/boot`, `/mnt/home`, ...).

*   También hay que activar la partición *swap*, si se dispone de una, para que pueda ser detectada más tarde cuando ejecute *genfstab*.

## Instalación

### Seleccionar los servidores de réplica

*   Edite `/etc/pacman.d/mirrorlist` y seleccione uno o varios servidores de réplicas para la descarga.

*   Los servidores de réplica regionales, por lo general, funcionan mejor; sin embargo, la cercanía no es el único criterio para discernir sobre la calidad de los mirrors, lea más sobre ello en [Mirrors (Español)](/index.php/Mirrors_(Espa%C3%B1ol) "Mirrors (Español)").

*   Una copia del archivo `mirrorlist` se realizará, más tarde, en el nuevo sistema por *pacstrap*, por lo que vale la pena hacerlo bien en esta fase.

### Instalar los paquetes del sistema base

*   Utilice el script [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) para instalar el grupo de paquetes [base](https://www.archlinux.org/groups/x86_64/base/): `# pacstrap /mnt base` 

*   Este grupo de paquetes no incluye todas las herramientas desponibles en el entorno live de instalación, como son los casos de [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) o firmware de wireless específicas ; consulte [packages.both](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both) para ver la comparación.

*   Para [instalar](/index.php/Install "Install") otros paquetes o grupos de paquetes en el nuevo sistema, añada sus nombres a la orden *pacstrap* (separados por espacios) o posteriormente a la etapa de [#Chroot](#Chroot) con órdenes individuales [pacman(8)](https://www.archlinux.org/pacman/pacman.8.html).

## Configuración del sistema

### Fstab

*   Generar un archivo [fstab (Español)](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)") (utilizar el parámetro `-U` o `-L` para especificar en dicho archivo las UUID o las etiquetas, respectivamente, de las particiones): `# genfstab -p /mnt >> /mnt/etc/fstab` 

*   Compruebe el archivo resultante en `/mnt/etc/fstab` después, y modifíquelo en caso de errores.

### Chroot

*   Entrar en el nuevo sistema como [Change root (Español)](/index.php/Change_root_(Espa%C3%B1ol) "Change root (Español)"): `# arch-chroot /mnt` 

### Zona horaria

*   Configure la [zona horaria](/index.php/Time_zone "Time zone"): `# ln -s /usr/share/zoneinfo/*zona*/*subzona* /etc/localtime` 

*   Ejecute [hwclock(8)](http://man7.org/linux/man-pages/man8/hwclock.8.html) para generar el archivo `/etc/adjtime`. Si el [horario estándar](/index.php/Time_standard "Time standard") está ajustado a [UTC](https://en.wikipedia.org/wiki/UTC "w:UTC"), otros sistemas operativos deben estar configurados en concordancia: `# hwclock --systohc --*utc*` 

### Idioma del sistema

*   Descomente el [locale](/index.php/Locale "Locale") necesario en `/etc/locale.gen`, y después generarlo con la orden: `# locale-gen` 

*   Añada `LANG=*su_locale*` a [locale.conf(5)](http://man7.org/linux/man-pages/man5/locale.conf.5.html), y, si fuese necesario, la [distribución de teclado de consola](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") y las preferencias del [tipo de letras](/index.php/Fonts#Console_fonts "Fonts") en [vconsole.conf(5)](http://man7.org/linux/man-pages/man5/vconsole.conf.5.html).

### Nombre del equipo

*   Cree una entrada para el [nombre de su equipo](/index.php/Hostname "Hostname") en `/etc/hostname` y `/etc/hosts`. Vea [hostname(5)](http://man7.org/linux/man-pages/man5/hostname.5.html) y [hosts(5)](http://man7.org/linux/man-pages/man5/hosts.5.html) para obtener más detalles.

### Configuración de la conexión de red

*   Configurar la red de nuevo para el entorno recién instalado: consultar [Network configuration (Español)](/index.php/Network_configuration_(Espa%C3%B1ol) "Network configuration (Español)").

*   Para la [configuración de la red inalámbrica](/index.php/Wireless_configuration "Wireless configuration"), [instale](/index.php/Install "Install") los paquetes [iw](https://www.archlinux.org/packages/?name=iw), [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant), y [dialog](https://www.archlinux.org/packages/?name=dialog), y, si se diese el caso, [paquetes de firmware](/index.php/Wireless#Installing_driver.2Ffirmware "Wireless").

### Initramfs

*   Cuando haga cambios en la configuración de [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"), cree un nuevo disco RAM inicial con: `# mkinitcpio -p linux` 

### Contraseña de root

*   Establezca la [contraseña](/index.php/Password "Password") de root: `# passwd` 

### Instalar un gestor de arranque

*   Consultar [Boot loaders (Español)](/index.php/Boot_loaders_(Espa%C3%B1ol) "Boot loaders (Español)") para conocer las opciones y configuraciones disponibles. Las elecciones incluyen [GRUB](/index.php/GRUB "GRUB") (BIOS/UEFI), [systemd-boot](/index.php/Systemd-boot "Systemd-boot") (UEFI) y [syslinux](/index.php/Syslinux "Syslinux") (BIOS).

*   Si tiene una CPU Intel, además de instalar un gestor de arranque, instale el paquete [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) y [active las actualizaciones del microcódigo](/index.php/Microcode#Enabling_Intel_microcode_updates "Microcode").

## Reiniciar

*   Salga del entorno chroot escribiendo `exit` o presionando `Ctrl+D`.

*   Opcionalmente, desmonte manualmente todas las particiones con `umount -R /mnt`: esto permite advertir cualquier partición «ocupada», y buscar su causa con [fuser(1)](http://man7.org/linux/man-pages/man1/fuser.1.html).

*   Por último, reinicie el equipo escribiendo `reboot`: cualquier partición que todavía siga montada será desmontada automáticamente por *systemd*. Recuerde que debe retirar el soporte de instalación y, luego, iniciar sesión en el nuevo sistema con la cuenta de root.

## Posinstalación

*   Véase el artículo [General recommendations (Español)](/index.php/General_recommendations_(Espa%C3%B1ol) "General recommendations (Español)") para obtener indicaciones sobre cómo gestionar el sistema, así como tutoriales sobre qué hacer después de la instalación del sistema base (como pueden ser temas relativos a la instalación y configuración de una interfaz gráfica de usuario, la del sonido o la del panel táctil).

*   Para obtener una lista de las aplicaciones que pueden ser de su interés, consulte [List of applications (Español)](/index.php/List_of_applications_(Espa%C3%B1ol) "List of applications (Español)").