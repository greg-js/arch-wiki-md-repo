**Estado de la traducción:** este artículo es una versión traducida de [Installation guide](/index.php/Installation_guide "Installation guide"). Fecha de la última traducción/revisión: **2017-01-11**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Installation_guide&diff=0&oldid=463062).

Este documento es una guía para la instalación de [Arch Linux (Español)](/index.php/Arch_Linux_(Espa%C3%B1ol) "Arch Linux (Español)") desde un sistema live arrancado con la imagen de instalación oficial. Antes de proceder a la instalación, es recomendable que le eche un vistazo a [FAQ (Español)](/index.php/FAQ_(Espa%C3%B1ol) "FAQ (Español)"). Para conocer las convenciones utilizadas en este documento, consulte [Help:Reading (Español)](/index.php/Help:Reading_(Espa%C3%B1ol) "Help:Reading (Español)").

Para obtener instrucciones más detalladas, consulte los artículos relacionados de [ArchWiki](/index.php/ArchWiki:About "ArchWiki:About"), o las [páginas de los manuales](/index.php/Man_page "Man page") de los distintos programas; vea [archlinux(7)](https://projects.archlinux.org/svntogit/packages.git/tree/filesystem/trunk/archlinux.7.txt) para una descripción general de la configuración. Para obtener ayuda interactiva, el [canal IRC](/index.php/IRC_channel_(Espa%C3%B1ol) "IRC channel (Español)") y los [foros](https://bbs.archlinux.org/) están disponibles.

## Contents

*   [1 Preinstalación](#Preinstalaci.C3.B3n)
    *   [1.1 Definir la distribución del teclado en el entorno live](#Definir_la_distribuci.C3.B3n_del_teclado_en_el_entorno_live)
    *   [1.2 Verificar el modo de arranque](#Verificar_el_modo_de_arranque)
    *   [1.3 Conectarse a Internet](#Conectarse_a_Internet)
    *   [1.4 Actualizar el reloj del sistema](#Actualizar_el_reloj_del_sistema)
    *   [1.5 Particionar el disco](#Particionar_el_disco)
    *   [1.6 Formatear las particiones](#Formatear_las_particiones)
    *   [1.7 Montar los sistemas de archivos](#Montar_los_sistemas_de_archivos)
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

*   Arch Linux puede ser ejecutado en cualquier máquina compatible con [x86_64](https://en.wikipedia.org/wiki/X86-64 "w:X86-64"), con un mínimo de 512 MB RAM. Una instalación básica con todos los paquetes del grupo [base](https://www.archlinux.org/groups/x86_64/base/) puede tomar alrededor de 800 MB de espacio en disco. Dado que el proceso de instalación necesita obtener los paquetes desde un repositorio remoto, necesitará una conexión a Internet funcional.

*   Descargue e inicie el soporte de instalación como se explica en [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch"). Iniciará sesión como usuario root en la primera [consola virtual](https://en.wikipedia.org/wiki/Virtual_console "w:Virtual console"), y se le presentará con el intérprete de órdenes [Zsh](/index.php/Zsh "Zsh"); órdenes comunes como [systemctl(1)](http://man7.org/linux/man-pages/man1/systemctl.1.html) pueden ser [completadas con el tabulador](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion").

*   Para cambiar a una consola diferente —por ejemplo, para ver esta guía con [ELinks](/index.php/ELinks "ELinks") junto con la instalación— utilice el [atajo](/index.php/Keyboard_shortcuts "Keyboard shortcuts") `Alt+*flecha*`. Para [editar/modificar](/index.php/Edit "Edit") los archivos de configuración, dispone de los editores [nano](/index.php/Nano#Usage "Nano"), [vi](https://en.wikipedia.org/wiki/vi "w:vi") y [vim](/index.php/Vim#Usage "Vim") .

### Definir la distribución del teclado en el entorno live

*   Por defecto, [la distribución del teclado de la consola](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") es la de [EE.UU.](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg"). Las opciones disponibles de los archivos de mapas de teclas se pueden enumerar con `ls /usr/share/kbd/keymaps/**/*.map.gz`.

*   La distribución del teclado se puede cambiar con la orden [loadkeys(1)](http://man7.org/linux/man-pages/man1/loadkeys.1.html), añadiendo el nombre de un archivo (no es necesario especificar la ruta ni la extensión del archivo cuando se usa «loadkeys»). Por ejemplo, ejecute `loadkeys es` para establecer una distribución de teclado [español](https://en.wikipedia.org/wiki/File:KB_Spanish.svg "wikipedia:File:KB Spanish.svg").

*   [Los tipos de letras para la consola](/index.php/Console_fonts "Console fonts") los puede encontrar en `/usr/share/kbd/consolefonts/`, y, como antes, se pueden ajustar con la orden [setfont(8)](http://man7.org/linux/man-pages/man8/setfont.8.html).

### Verificar el modo de arranque

*   Si el modo UEFI está activado en una placa base [UEFI](/index.php/UEFI "UEFI"), [Archiso](/index.php/Archiso "Archiso") [arrancará](/index.php/Boot "Boot") en consecuencia a través de [systemd-boot](/index.php/Systemd-boot "Systemd-boot"). Para comprobar esto, enumere el contenido del directorio [efivars](/index.php/UEFI#UEFI_Variables "UEFI"): `# ls /sys/firmware/efi/efivars` 

*   Si no existe el directorio, el sistema se iniciará en modo [BIOS](https://en.wikipedia.org/wiki/es:BIOS "w:es:BIOS") (o CSM). Referirse al manual de su tarjeta madre para detalles.

### Conectarse a Internet

*   El servicio de Internet a través del demonio [dhcpcd](/index.php/Dhcpcd "Dhcpcd") está [activado](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) en el arranque para los dispositivos **cableados**. Compruebe que su conexión se ha establecido, usando, por ejemplo, la herramienta [ping](/index.php/Ping "Ping"): `# ping archlinux.org` 

*   Si no dispone de ninguna conexión, [detenga](/index.php/Systemd#Using_units "Systemd") el servicio *dhcpcd* con la orden `systemctl stop dhcpcd@<TAB>` y eche un vistazo al artículo [Network configuration](/index.php/Network_configuration#Device_driver "Network configuration").

*   Para realizar conexiones **inalámbricas**, dispone de iw(8), wpa_supplicant(8) y [netctl](/index.php/Netctl#Wireless_.28WPA-PSK.29 "Netctl"). Vea [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

### Actualizar el reloj del sistema

*   Utilice [timedatectl(1)](http://man7.org/linux/man-pages/man1/timedatectl.1.html) para asegurarse de que la hora del sistema es correcta: `# timedatectl set-ntp true` 

*   Para comprobar el estado del servicio, utilice `timedatectl status`.

### Particionar el disco

*   [Identifique los dispositivos](/index.php/Core_utilities#lsblk "Core utilities") donde se instalará el nuevo sistema (los resultados que terminen en `rom`, `loop` o `airoot` pueden ser ignorados): `# fdisk -l` 

*   Se requieren las siguientes *particiones* (se muestran con un sufijo numérico) para el dispositivo elegido:

*   Una partición para el directorio raíz`/`.
*   Si [UEFI](/index.php/UEFI "UEFI") está activado, una [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition").

*   El [espacio de intercambio (swap)](/index.php/Swap_space "Swap space") puede establecerse en una partición separada o en un [archivo swap](/index.php/Swap#Swap_file "Swap").

*   Para modificar la *tabla de particiones* utilice [fdisk](/index.php/Fdisk "Fdisk") o [parted](/index.php/Parted "Parted"). Vea [Partitioning](/index.php/Partitioning "Partitioning") para obtener más información.

*   En esta fase de la instalación, también hay que crear los dispositivos de bloques apilados —stacked block devices— para [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)"), [Disk encryption (Español)](/index.php/Disk_encryption_(Espa%C3%B1ol) "Disk encryption (Español)") o [RAID (Español)](/index.php/RAID_(Espa%C3%B1ol) "RAID (Español)"), si se diera el caso.

### Formatear las particiones

*   Una vez que se han creado las particiones, cada una de ellas debe ser formateada con un [sistema de archivos](/index.php/File_system "File system") adecuado. Por ejemplo, para formatear la partición raíz situada en `/dev/*sda1*` con `*ext4*`, ejecute: `# mkfs.*ext4* /dev/*sda1*` 

*   Vea [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems") para obtener más detalles.

### Montar los sistemas de archivos

*   El siguiente paso es [montar](/index.php/File_systems#Mount_a_filesystem "File systems") la partición del sistema —root— en `/mnt`, por ejemplo: `# mount /dev/*sda1* /mnt` 

*   Después de esto, hay que crear tantos directorios como particiones haya realizado y montarlas, por ejemplo: `# mkdir /mnt/boot`  `# mount /dev/sda2 /mnt/boot` 

*   Los sistemas de archivos montados serán posteriormente detectados por [genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in).

## Instalación

### Seleccionar los servidores de réplica

*   Los paquetes que se instalen deben ser descargados desde [servidores de réplicas](/index.php/Mirrors "Mirrors"), los cuales se definen en `/etc/pacman.d/mirrorlist`. En el entorno live de instalación, todos los servidores de réplicas están activados y ordenados de acuerdo al estado de sincronización y velocidad en el momento de creación de la imagen de instalación.

*   Cuanto más alto se coloca un servidor de réplica en la lista, más prioridad tendrá al descargar un paquete. Es posible que desee modificar el archivo en consecuencia y mover los servidores de réplicas geográficamente más cercanos, a la parte superior de la lista, aunque se deben tener en consideración otros criterios.

*   Una copia del archivo mirrorlist se realizará más tarde en el nuevo sistema por *pacstrap*, por lo tanto vale la pena hacerlo bien en esta fase.

### Instalar los paquetes del sistema base

*   Utilice el script [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) para instalar el grupo de paquetes [base](https://www.archlinux.org/groups/x86_64/base/): `# pacstrap /mnt base` 

*   Este grupo de paquetes no incluye todas las herramientas disponibles en el entorno live de instalación, como son los casos de [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) o firmware de wireless específicas ; consulte [packages.both](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both) para ver la comparación.

*   Para [instalar](/index.php/Install "Install") otros paquetes o grupos de paquetes, como [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), en el nuevo sistema, añada sus nombres a la orden *pacstrap* (separados por espacios) o, posteriormente a la etapa de [#Chroot](#Chroot), con órdenes individuales con [pacman](/index.php/Pacman "Pacman").

## Configuración del sistema

### Fstab

*   Generar un archivo [fstab (Español)](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)") (utilizar el parámetro `-U` o `-L` para especificar en dicho archivo las UUID o las etiquetas, respectivamente, de las particiones): `# genfstab -U /mnt >> /mnt/etc/fstab` 

*   Compruebe el archivo resultante en `/mnt/etc/fstab` después, y modifíquelo en caso de errores.

### Chroot

*   Entrar en el nuevo sistema como [Change root (Español)](/index.php/Change_root_(Espa%C3%B1ol) "Change root (Español)"): `# arch-chroot /mnt` 

### Zona horaria

*   Configure la [zona horaria](/index.php/Time_zone "Time zone"): `# ln -s /usr/share/zoneinfo/*Región*/*Ciudad* /etc/localtime` 

*   Ejecute [hwclock(8)](http://man7.org/linux/man-pages/man8/hwclock.8.html) para generar el archivo `/etc/adjtime`: `# hwclock --systohc` 

*   Esta orden presume que le reloj del hardware esta configurada con [UTC](https://en.wikipedia.org/wiki/UTC "w:UTC"). Vea [Time#Time standard](/index.php/Time#Time_standard "Time") para obtener más detalles.

### Idioma del sistema

*   Descomente el [locale](/index.php/Locale "Locale") necesario en `/etc/locale.gen`, además de `en_US.UTF-8 UTF-8` y, después, genérelo con la orden: `# locale-gen` 

*   Defina la [variable](/index.php/Variable "Variable") `LANG` en [locale.conf(5)](http://man7.org/linux/man-pages/man5/locale.conf.5.html) según su caso, por ejemplo:

 `/etc/locale.conf`  `LANG=*es_ES.UTF-8*` 

*   Si fuese necesario, defina la [distribución del teclado de la consola](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") y las preferencias del [tipo de letras](/index.php/Fonts#Console_fonts "Fonts") en [vconsole.conf(5)](http://man7.org/linux/man-pages/man5/vconsole.conf.5.html).:

 `/etc/vconsole.conf`  `KEYMAP=*es*` 

### Nombre del equipo

*   Cree el archivo [hostname(5)](http://man7.org/linux/man-pages/man5/hostname.5.html):

 `/etc/hostname` 
```
*elnombredemiequipo*

```

*   Considere añadir una entrada similar en [hosts(5)](http://man7.org/linux/man-pages/man5/hosts.5.html):

 `/etc/hosts` 
```
127.0.0.1	localhost.localdomain	localhost
::1		localhost.localdomain	localhost
**127.0.1.1	*elnombredemiequipo*.localdomain	*elnombredemiequipo***

```

*   Ver también [Establecer el nombre del equipo](/index.php/Network_configuration_(Espa%C3%B1ol)#Establecer_el_nombre_del_equipo "Network configuration (Español)").

### Configuración de la conexión de red

*   Configure la red de nuevo para el entorno recién instalado: consulte [Network configuration (Español)](/index.php/Network_configuration_(Espa%C3%B1ol) "Network configuration (Español)").

*   Para la [configuración de la red inalámbrica](/index.php/Wireless_configuration "Wireless configuration"), [instale](/index.php/Install "Install") los paquetes [iw](https://www.archlinux.org/packages/?name=iw) y [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) y, si se diera el caso, los [paquetes de firmware](/index.php/Wireless#Installing_driver.2Ffirmware "Wireless"). Opcionalmente instalar [dialog](https://www.archlinux.org/packages/?name=dialog) para uso del *menú-wifi*.

### Initramfs

*   Normalmente no es necesario crear una imagen *initramfs* nueva, dado que [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") se ejecuta durante la instalación del paquete [linux](https://www.archlinux.org/packages/?name=linux) con *pacstrap*.

*   Cuando haga cambios especiales en la configuración de [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"), cree un nuevo disco RAM inicial con: `# mkinitcpio -p linux` 

### Contraseña de root

*   Establezca la [contraseña](/index.php/Password "Password") de root: `# passwd` 

### Instalar un gestor de arranque

*   Consulte [Category:Boot loaders](/index.php/Category:Boot_loaders "Category:Boot loaders") para conocer las opciones y configuraciones disponibles. Por ejemplo, configure el gestor de arranque con [systemd-boot](/index.php/Systemd-boot "Systemd-boot") si el sistema es compatible con UEFI, y [GRUB](/index.php/GRUB "GRUB") cuando no.

*   Si tiene una CPU Intel, además de instalar un gestor de arranque, instale el paquete [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) y [active las actualizaciones del microcódigo](/index.php/Microcode#Enabling_Intel_microcode_updates "Microcode").

## Reiniciar

*   Salga del entorno chroot escribiendo `exit` o presionando `Ctrl+D`.

*   Opcionalmente, desmonte manualmente todas las particiones con `umount -R /mnt`: esto permite advertir cualquier partición «ocupada», y buscar su causa con [fuser(1)](http://man7.org/linux/man-pages/man1/fuser.1.html).

*   Por último, reinicie el equipo escribiendo `reboot`: cualquier partición que todavía siga montada será desmontada automáticamente por *systemd*. Recuerde que debe retirar el soporte de instalación e iniciar sesión en el nuevo sistema con la cuenta de root.

## Posinstalación

*   Véase el artículo [General recommendations (Español)](/index.php/General_recommendations_(Espa%C3%B1ol) "General recommendations (Español)") para obtener indicaciones de cómo gestionar el sistema y tutoriales sobre qué hacer después de la instalación del sistema base (o temas relativos a la instalación, configuración de la interfaz gráfica de usuario, sonido o panel táctil).

*   Para obtener una lista de las aplicaciones que pueden ser de su interés, consulte [List of applications (Español)](/index.php/List_of_applications_(Espa%C3%B1ol) "List of applications (Español)").