**Estado de la traducción**
Este artículo es una traducción de [Installation guide](/index.php/Installation_guide "Installation guide"), revisada por última vez el **2019-09-14**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Installation_guide&diff=0&oldid=582205) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Este documento es una guía para la instalación de [Arch Linux (Español)](/index.php/Arch_Linux_(Espa%C3%B1ol) "Arch Linux (Español)") desde un sistema «*live*» arrancado con la imagen de instalación oficial. Antes de proceder a la instalación, es recomendable que eche un vistazo a las [Frequently asked questions (Español)](/index.php/Frequently_asked_questions_(Espa%C3%B1ol) "Frequently asked questions (Español)"). Para conocer las convenciones utilizadas en este documento, consulte [Help:Reading (Español)](/index.php/Help:Reading_(Espa%C3%B1ol) "Help:Reading (Español)"). En particular, los ejemplos de código pueden contener marcadores de posición (resaltados en `*cursiva*`) que deberán reemplazarse manualmente.

Para obtener instrucciones más detalladas, consulte los artículos relacionados de [ArchWiki (Español)](/index.php/ArchWiki_(Espa%C3%B1ol) "ArchWiki (Español)"), o las [páginas de los manuales](/index.php/Man_page "Man page") de los distintos programas, con enlaces para ambos a lo largo de esta guía. Para obtener ayuda interactiva, dispone de los [Arch IRC channels (Español)](/index.php/Arch_IRC_channels_(Espa%C3%B1ol) "Arch IRC channels (Español)") y los [foros](https://bbs.archlinux.org/).

Arch Linux puede ejecutarse en cualquier máquina compatible [x86_64](https://en.wikipedia.org/wiki/es:X86-64 "wikipedia:es:X86-64") con al menos 512 MiB de RAM. Una instalación básica con todos los paquetes del grupo [base](https://www.archlinux.org/packages/?name=base) debería ocupar menos de 800 MiB de espacio en disco. Dado que el proceso de instalación necesita obtener los paquetes desde un repositorio remoto, esta guía asume que dispone de una conexión a internet funcional.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Preinstalación](#Preinstalación)
    *   [1.1 Verificar las firmas](#Verificar_las_firmas)
    *   [1.2 Arrancar el entorno live](#Arrancar_el_entorno_live)
    *   [1.3 Definir la distribución del teclado en el entorno live](#Definir_la_distribución_del_teclado_en_el_entorno_live)
    *   [1.4 Verificar la modalidad de arranque](#Verificar_la_modalidad_de_arranque)
    *   [1.5 Conectarse a Internet](#Conectarse_a_Internet)
    *   [1.6 Actualizar el reloj del sistema](#Actualizar_el_reloj_del_sistema)
    *   [1.7 Particionar el disco](#Particionar_el_disco)
        *   [1.7.1 Esquemas de ejemplo](#Esquemas_de_ejemplo)
    *   [1.8 Formatear las particiones](#Formatear_las_particiones)
    *   [1.9 Montar los sistemas de archivos](#Montar_los_sistemas_de_archivos)
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

Las imágenes de instalación y sus firmas [GnuPG (Español)](/index.php/GnuPG_(Espa%C3%B1ol) "GnuPG (Español)") se pueden obtener desde la página de [descargas](https://archlinux.org/download/).

### Verificar las firmas

Se recomienda verificar la firma de la imagen antes de usarla, especialmente cuando se descarga desde un *servidor de réplica HTTP*, donde las descargas generalmente son susceptibles de ser interceptadas por [imágenes de servidores maliciosos](https://www2.cs.arizona.edu/stork/packagemanagersecurity/attacks-on-package-managers.html).

En un sistema con [GnuPG (Español)](/index.php/GnuPG_(Espa%C3%B1ol) "GnuPG (Español)") instalado, realice esta operación descargando la *firma PGP* (bajo *Checksums*) en el directorio de la imagen ISO, y [verifíquela](/index.php/GnuPG#Verify_a_signature "GnuPG") con la siguiente orden:

```
$ gpg --keyserver-options auto-key-retrieve --verify archlinux-*version*-x86_64.iso.sig

```

También, desde una instalación existente de Arch Linux, puede escribir:

```
$ pacman-key -v archlinux-*version*-x86_64.iso.sig

```

**Nota:**

*   La firma en sí podría manipularse si se descarga desde un sitio de réplica, en lugar de hacerlo desde [archlinux.org](https://archlinux.org/download/) como se recomendó antes. En este caso, asegúrese de que la clave pública, que se utiliza para decodificar la firma, esté firmada por otra clave de confianza. La orden `gpg` emitirá la huella digital de la clave pública.
*   Otro método para verificar la autenticidad de la firma es asegurarse de que la huella digital de la clave pública sea idéntica a la huella digital de la del [desarrollador de Arch Linux](https://www.archlinux.org/people/developers/) que firmó el archivo ISO. Consulte [Wikipedia:Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography "wikipedia:Public-key cryptography") y [Wikipedia:es:Criptografía asimétrica](https://en.wikipedia.org/wiki/es:Criptograf%C3%ADa_asim%C3%A9trica "wikipedia:es:Criptografía asimétrica") para obtener más información sobre el proceso de clave pública para autenticar claves.

### Arrancar el entorno live

El entorno live se puede iniciar desde una [unidad flash USB](/index.php/USB_flash_installation_media_(Espa%C3%B1ol) "USB flash installation media (Español)"), un [disco óptico](/index.php/Optical_disc_drive_(Espa%C3%B1ol)#Grabación "Optical disc drive (Español)") o una red con [PXE (Español)](/index.php/PXE_(Espa%C3%B1ol) "PXE (Español)"). Para medios de instalación alternativos, vea [Category:Installation process (Español)](/index.php/Category:Installation_process_(Espa%C3%B1ol) "Category:Installation process (Español)").

*   La indicación del dispositivo de arranque actual en una unidad que contenga el soporte de instalación de Arch se logra, normalmente, presionando una tecla durante la fase [POST](https://en.wikipedia.org/wiki/es:POST "wikipedia:es:POST") (siglas en inglés de «*power-on self-test*» o autoprueba de arranque), tecla que se suele indicar en la pantalla de inicio del ordenador. Consulte el manual de su placa base para más detalles.
*   Cuando aparezca el menú de Arch, seleccione *Boot Arch Linux* y presione `Intro` para ingresar al entorno de instalación.
*   Consulte [README.bootparams](https://projects.archlinux.org/archiso.git/tree/docs/README.bootparams) para obtener una lista de los [parámetros de arranque](/index.php/Kernel_parameters_(Espa%C3%B1ol)#Configuración "Kernel parameters (Español)"), y [packages.x86_64](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) para obtener una lista de los paquetes incluidos (en la imagen).
*   Iniciará sesión en la primera [consola virtual](https://en.wikipedia.org/wiki/es:Consola_Virtual "wikipedia:es:Consola Virtual") como usuario root, y se le presentará un intérprete de línea de órdens [Zsh (Español)](/index.php/Zsh_(Espa%C3%B1ol) "Zsh (Español)").

Para cambiar a una consola diferente —por ejemplo, para ver esta guía con el navegador web [ELinks](/index.php/ELinks "ELinks") junto a la instalación—, utilice el [atajo del teclado](/index.php/Keyboard_shortcuts "Keyboard shortcuts") `Alt+*flecha*` . Para [editar](/index.php/Help:Reading_(Espa%C3%B1ol)#Adjuntar,_añadir,_crear,_editar "Help:Reading (Español)") los archivos de configuración, dispone de los editores [nano](/index.php/Nano_(Espa%C3%B1ol)#Uso "Nano (Español)"), [vi](https://en.wikipedia.org/wiki/es:Vi "wikipedia:es:Vi") y [vim](/index.php/Vim#Usage "Vim").

### Definir la distribución del teclado en el entorno live

Por defecto, [la distribución del teclado de la consola](/index.php/Fonts_(Espa%C3%B1ol) "Fonts (Español)") es la de [EE.UU.](https://en.wikipedia.org/wiki/es:File:KB_United_States-NoAltGr.svg "wikipedia:es:File:KB United States-NoAltGr.svg"). Las distribuciones de teclado disponibles se pueden enumerar con:

```
# ls /usr/share/kbd/keymaps/**/*.map.gz

```

La distribución del teclado se puede cambiar con la orden [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1), añadiendo el nombre de un archivo (no es necesario especificar la ruta ni la extensión del archivo cuando se usa «loadkeys»). Por ejemplo, para establecer una distribución de teclado en [español](https://en.wikipedia.org/wiki/es:File:KB_Spanish.svg "wikipedia:es:File:KB Spanish.svg"), ejecute:

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

Para configurar una conexión de red, siga los siguientes pasos:

*   Asegúrese de que su [interfaz de red](/index.php/Network_interface "Network interface") está en la lista y activada, por ejemplo con la orden [ip-link(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-link.8): `# ip link` 
*   Conéctese a la red. Enchufe el cable Ethernet o [conéctese a una LAN inalámbrica](/index.php/Wireless_network_configuration_(Espa%C3%B1ol) "Wireless network configuration (Español)").
*   Configure su conexión de red:
    *   [Dirección IP estática](/index.php/Network_configuration#Static_IP_address "Network configuration").
    *   Dirección IP dinámica: utilice [DHCP](/index.php/DHCP "DHCP").

    **Nota:** la imagen de la instalación activa en el arranque [dhcpcd](/index.php/Dhcpcd "Dhcpcd") (`dhcpcd@*nombredelainterfaz*.service`) para [los dispositivos de red cableados](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules).

*   La conexión se puede verificar con la utilidad [ping](https://en.wikipedia.org/wiki/ping "wikipedia:ping"): `# ping archlinux.org` 

### Actualizar el reloj del sistema

Utilice [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) para asegurarse de que el reloj del sistema sea preciso:

```
# timedatectl set-ntp true

```

Para comprobar el estado del servicio, utilice `timedatectl status`.

### Particionar el disco

Cuando el sistema lo reconoce, los discos se asignan a un [dispositivo de bloque](/index.php/Block_device_(Espa%C3%B1ol) "Block device (Español)") como `/dev/sda` o `/dev/nvme0n1`. Para identificar estos dispositivos, utilice [lsblk](/index.php/Lsblk_(Espa%C3%B1ol) "Lsblk (Español)") o *fdisk*:

```
# fdisk -l

```

Los resultados que terminan en `rom`, `loop` o `airoot` pueden ignorarse.

Las siguientes [particiones](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)") son **necesarias** para el dispositivo elegido:

*   Una partición para el directorio raíz `/`.
*   Si [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)") está activado, una [partición del sistema EFI](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)").

Si desea crear dispositivos de bloques apilados —*stacked block devices*— para [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)"), [cifrado de disco](/index.php/Disk_encryption_(Espa%C3%B1ol) "Disk encryption (Español)") o [RAID (Español)](/index.php/RAID_(Espa%C3%B1ol) "RAID (Español)"), hágalo ahora.

#### Esquemas de ejemplo

| BIOS con [MBR](/index.php/MBR "MBR") |
| Punto de montaje | Partición | [Tipo de partición](https://en.wikipedia.org/wiki/Partition_type "wikipedia:Partition type") | Tamaño sugerido |
| `/mnt` | `/dev/sd*X*1` | Linux | Resto del dispositivo |
| [SWAP] | `/dev/sd*X*2` | Linux swap | Más de 512 MiB |
| UEFI con [GPT](/index.php/GPT "GPT") |
| Punto de montaje | Partición | [Tipo de partición](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table") | Tamaño sugerido |
| `/mnt/boot` o `/mnt/efi` | `/dev/sd*X*1` | [EFI system partition](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)") | 260–512 MiB |
| `/mnt` | `/dev/sd*X*2` | Linux x86-64 root (/) | Resto del dispositivo |
| [SWAP] | `/dev/sd*X*3` | Linux swap | Más de 512 MiB |

Véase también [Partitioning (Español)#Esquemas de particionado](/index.php/Partitioning_(Espa%C3%B1ol)#Esquemas_de_particionado "Partitioning (Español)").

**Nota:**

*   Utilice [fdisk (Español)](/index.php/Fdisk_(Espa%C3%B1ol) "Fdisk (Español)") o [parted](/index.php/Parted "Parted") para modificar la tabla de particionado, por ejemplo, `fdisk /dev/sd*X*`.
*   El espacio [de intercambio](/index.php/Swap_(Espa%C3%B1ol) "Swap (Español)") se puede configurar en un [archivo de intercambio](/index.php/Swap_(Espa%C3%B1ol)#Archivo_swap "Swap (Español)") para los sistemas de archivos que lo admitan.

### Formatear las particiones

Una vez se han creado las particiones, cada una de ellas debe formatearse con un [sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)") adecuado. Por ejemplo, si la partición raíz está en `/dev/sd*X*1` y se ha pensado en `*ext4*` como su sistema de archivos, ejecute:

```
# mkfs.*ext4* /dev/sd*X1*

```

Si creó una partición para el espacio de intercambio *(swap)*, formatéela con *mkswap*:

```
# mkswap /dev/sd*X2*
# swapon /dev/sd*X2*

```

Consulte cómo [crear un sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol)#Crear_un_sistema_de_archivos "File systems (Español)") para más detalles.

### Montar los sistemas de archivos

El siguiente paso es [montar](/index.php/Mount "Mount") el sistema de archivos de la partición raíz —root— en `/mnt`, por ejemplo:

```
# mount /dev/sd*X1* /mnt

```

Cree los puntos de montaje restantes (como `/mnt/efi`) y monte las particiones correspondientes en ellos.

Los sistemas de archivos montados, así como el espacio de intercambio, serán posteriormente detectados por [genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in).

## Instalación

### Seleccionar los servidores de réplica

Los paquetes que se instalarán se deben descargar desde los [servidores de réplicas](/index.php/Mirrors_(Espa%C3%B1ol) "Mirrors (Español)"), que se definen en `/etc/pacman.d/mirrorlist`. En el entorno live de instalación, todos los servidores de réplicas están activados y ordenados de acuerdo al estado de sincronización y velocidad en el momento de creación de la imagen de instalación.

Cuanto más alto se coloca un servidor de réplica en la lista, más prioridad tendrá al descargar un paquete. Es posible que desee modificar el archivo en consecuencia y mover los servidores de réplicas geográficamente más cercanos, a la parte superior de la lista, aunque se deben tener en consideración otros criterios.

Una copia del archivo «mirrorlist» se realizará más tarde en el nuevo sistema por *pacstrap*, por lo tanto vale la pena hacerlo bien en esta fase.

### Instalar los paquetes del sistema base

Utilice el script [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) para instalar el grupo de paquetes [base](https://www.archlinux.org/packages/?name=base) y un [Kernel](/index.php/Kernel_(Espa%C3%B1ol) "Kernel (Español)") ([linux](https://www.archlinux.org/packages/?name=linux)):

```
# pacstrap /mnt base linux

```

**Note:** Este grupo de paquetes no incluye todas las herramientas disponibles en el entorno live de instalación, como son los casos de [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) o firmware inalámbrico específico; consulte [paquetes.x86_64](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) para ver la comparación.

Es posible sustituir [linux](https://www.archlinux.org/packages/?name=linux) con el [Kernel](/index.php/Kernel_(Espa%C3%B1ol) "Kernel (Español)") de su elección, o en caso de saber lo que se hace se puede no instalar ninguno.

Para [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalación_de_paquetes "Help:Reading (Español)") otros paquetes o grupos de paquetes, como [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), en el nuevo sistema, añada sus nombres a la orden *pacstrap* (separados por un espacio) o, posteriormente a la etapa de [#Chroot](#Chroot), con órdenes individuales con [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)").

## Configuración del sistema

### Fstab

Genere un archivo [fstab (Español)](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)") (utilice `-U` o `-L` para especificar en dicho archivo las [UUID](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol)#by-uuid "Persistent block device naming (Español)") o las etiquetas, respectivamente):

```
# genfstab -U /mnt >> /mnt/etc/fstab

```

Compruebe el archivo resultante en `/mnt/etc/fstab` después, y modifíquelo en caso de errores.

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

Cree el archivo [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5), y defina la [variable](/index.php/Environment_variables_(Espa%C3%B1ol) "Environment variables (Español)") `LANG` en [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5) según su caso, por ejemplo:

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

Para [LVM](/index.php/LVM_(Espa%C3%B1ol)#Configurar_mkinitcpio "LVM (Español)"), [cifrado del sistema](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)") o [RAID](/index.php/RAID#Configure_mkinitcpio "RAID"), modifique [mkinitcpio.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.conf.5) y regenere la imagen initramfs:

```
# mkinitcpio -p linux

```

### Contraseña de root

Establezca la [contraseña](/index.php/Users_and_groups_(Espa%C3%B1ol)#Base_de_datos_del_usuario "Users and groups (Español)") de [root](https://en.wikipedia.org/wiki/es:Root "wikipedia:es:Root"):

```
# passwd

```

### Instalar gestor de arranque

Elija e instale un [gestor de arranque](/index.php/Boot_loader_(Espa%C3%B1ol) "Boot loader (Español)") compatible con Linux. Si tiene una CPU Intel o AMD, active las actualizaciones de [microcode (Español)](/index.php/Microcode_(Espa%C3%B1ol) "Microcode (Español)").

## Reiniciar

Salga del entorno chroot escribiendo `exit` o presionando `Ctrl+d`.

Opcionalmente, puede desmontar manualmente todas las particiones con `umount -R /mnt`: esto permite advertir cualquier partición «ocupada», y buscar su causa con [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1).

Por último, reinicie el equipo escribiendo `reboot`: cualquier partición que todavía esté montada será desmontada automáticamente por *systemd*. Recuerde retirar los medios de instalación y luego inicie sesión en el nuevo sistema con la cuenta de root.

## Posinstalación

Vea el artículo [General recommendations (Español)](/index.php/General_recommendations_(Espa%C3%B1ol) "General recommendations (Español)") para obtener instrucciones sobre cómo gestionar el sistema, así como tutoriales sobre qué hacer después de la instalación (tales como configurar una interfaz gráfica de usuario, el sonido o un panel táctil).

Para obtener una lista de aplicaciones que pueden ser de su interés, consulte [List of applications (Español)](/index.php/List_of_applications_(Espa%C3%B1ol) "List of applications (Español)").