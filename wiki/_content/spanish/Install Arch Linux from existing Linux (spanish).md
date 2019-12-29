**Estado de la traducción**
Este artículo es una traducción de [Install from existing Linux](/index.php/Install_from_existing_Linux "Install from existing Linux"), revisada por última vez el **2019-11-13**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Install_from_existing_Linux&diff=0&oldid=586812) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Install from SSH (Español)](/index.php/Install_from_SSH_(Espa%C3%B1ol) "Install from SSH (Español)")

Este documento describe el proceso de [bootstrapping](https://en.wikipedia.org/wiki/es:Bootstrapping_(inform%C3%A1tica) necesario para instalar Arch Linux desde un sistema anfitrión de Linux en ejecución. Después del bootstrapping, la instalación continúa como se describe en la [guía de instalación](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)").

La instalación de Arch Linux desde un sistema Linux en ejecución es útil para:

*   instalar remotamente Arch Linux, por ejemplo, un servidor root (virtual);
*   sustituir un Linux existente sin un LiveCD (véase [#Reemplazar el sistema existente sin un LiveCD](#Reemplazar_el_sistema_existente_sin_un_LiveCD));
*   crear un distribución Linux nueva o LiveCD basada en Arch Linux;
*   crear un entorno chroot de Arch Linux, por ejemplo para un contenedor de base Docker;
*   [rootfs-sobre-NFS para máquinas sin disco](/index.php/Diskless_network_boot_NFS_root "Diskless network boot NFS root").

El objetivo del procedimiento de bootstrapping es configurar un entorno desde el que ejecutar los [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) (tales como `pacstrap` y `arch-root`).

Si el sistema anfitrión ejecuta Arch Linux, esto se puede lograr simplemente instalando [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts). Si el sistema anfitrión ejecuta otra distribución de Linux, primero deberá configurar un entorno chroot basado en Arch Linux.

**Nota:** esta guía requiere que el sistema anfitrión existente sea capaz de ejecutar los nuevos programas de Arch Linux para la arquitectura de destino. Esto significa que tiene que ser un sistema anfitrión x86_64.

**Advertencia:** asegúrese de comprender cada paso antes de continuar. Es fácil destruir su sistema o perder datos críticos, y su proveedor de servicios, probablemente, le cobrará mucho para ayudarle a recuperarlo.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Realizar copia de seguridad y preparación](#Realizar_copia_de_seguridad_y_preparación)
*   [2 Desde un sistema anfitrión que ejecuta Arch Linux](#Desde_un_sistema_anfitrión_que_ejecuta_Arch_Linux)
    *   [2.1 Crear una nueva instalación de Arch](#Crear_una_nueva_instalación_de_Arch)
    *   [2.2 Crear una copia de una instalación de Arch existente](#Crear_una_copia_de_una_instalación_de_Arch_existente)
*   [3 Desde un sistema anfitrión que ejecuta otra distribución de Linux](#Desde_un_sistema_anfitrión_que_ejecuta_otra_distribución_de_Linux)
    *   [3.1 Utilizar pacman desde el sistema anfitrión](#Utilizar_pacman_desde_el_sistema_anfitrión)
    *   [3.2 Crear un entorno chroot](#Crear_un_entorno_chroot)
        *   [3.2.1 Método A: utilizar una imagen de bootstrap (recomendado)](#Método_A:_utilizar_una_imagen_de_bootstrap_(recomendado))
        *   [3.2.2 Método B: utilizar una imagen LiveCD](#Método_B:_utilizar_una_imagen_LiveCD)
    *   [3.3 Utilizar un entorno chroot](#Utilizar_un_entorno_chroot)
        *   [3.3.1 Inicializar el depósito de claves de pacman](#Inicializar_el_depósito_de_claves_de_pacman)
        *   [3.3.2 Seleccionar un servidor de réplica y descargar herramientas básicas](#Seleccionar_un_servidor_de_réplica_y_descargar_herramientas_básicas)
    *   [3.4 Sugerencias de instalación](#Sugerencias_de_instalación)
        *   [3.4.1 Anfitrión basado en Debian](#Anfitrión_basado_en_Debian)
            *   [3.4.1.1 /dev/shm](#/dev/shm)
            *   [3.4.1.2 /dev/pts](#/dev/pts)
            *   [3.4.1.3 lvmetad](#lvmetad)
        *   [3.4.2 Anfitrión basado en Fedora](#Anfitrión_basado_en_Fedora)
*   [4 Cosas que verificar antes de reiniciar](#Cosas_que_verificar_antes_de_reiniciar)
*   [5 Reemplazar el sistema existente sin un LiveCD](#Reemplazar_el_sistema_existente_sin_un_LiveCD)
    *   [5.1 Establecer la antigua partición de intercambio como nueva partición raíz](#Establecer_la_antigua_partición_de_intercambio_como_nueva_partición_raíz)
    *   [5.2 Instalación](#Instalación)

## Realizar copia de seguridad y preparación

Haga una copia de seguridad de todos sus datos, incluidos correos electrónicos, servidores web, etc. Tenga toda la información a su alcance. Preserve todas las configuraciones de su servidor, nombres de equipos, etc.

Aquí hay una lista de datos que probablemente necesitará:

*   Direcciones IP.
*   Nombre(s) de equipo, (nota: los servidores raíces también son en su mayoría parte del dominio de proveedores, verifique o guarde su `/etc/hosts` antes de eliminar).
*   Servidores DNS (compruebe `/etc/resolv.conf`).
*   Claves SSH (si otras personas trabajan en su servidor, de lo contrario tendrán que aceptar nuevas claves. Esto incluye claves de su Apache, sus servidores de correo, su servidor SSH y otros).
*   Información de hardware (tarjeta de red, etc. Consulte su preinstalado `/etc/modules.conf`).
*   Archivos de configuración de Grub.

En general, es una buena idea tener una copia local de su directorio original `/etc` en su disco duro local.

## Desde un sistema anfitrión que ejecuta Arch Linux

Instale el paquete [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts).

Siga [Installation guide (Español)#Montar los sistemas de archivos](/index.php/Installation_guide_(Espa%C3%B1ol)#Montar_los_sistemas_de_archivos "Installation guide (Español)") para montar el sistema de archivos y todos los puntos de montaje necesarios. Si ya utiliza el directorio `/mnt` para otra cosa, simplemente cree otro directorio como `/mnt/install`, y úselo en su lugar como la base del punto de montaje.

### Crear una nueva instalación de Arch

Siga la [Installation guide (Español)#Instalación](/index.php/Installation_guide_(Espa%C3%B1ol)#Instalación "Installation guide (Español)").

Respecto a la [Installation guide (Español)#Seleccionar los servidores de réplica](/index.php/Installation_guide_(Espa%C3%B1ol)#Seleccionar_los_servidores_de_réplica "Installation guide (Español)") se puede omitir ya que el equipo debería tener una lista de servidores de réplica correcta.

**Sugerencia:** para evitar volver a descargar todos los paquetes, considere seguir [Pacman (Español)/Tips and tricks (Español)#Caché de pacman compartida en red](/index.php/Pacman_(Espa%C3%B1ol)/Tips_and_tricks_(Espa%C3%B1ol)#Caché_de_pacman_compartida_en_red "Pacman (Español)/Tips and tricks (Español)") o utilizar la opción `-c` de *pacstrap*'.

**Sugerencia:** cuando se utiliza el cargador de arranque grub, el script `grub-mkconfig` puede detectar dispositivos incorrectamente. Esto resultará en `Error:no such device` al intentar arrancar desde el dispositivo. Para resolver este problema, desde el sistema anfitrión que ejecuta Arch Linux, monte las particiones recién instaladas, ejecute *arch-chroot* en la nueva partición, luego instale y configure grub. El último paso puede requerir desactivar *lvmetad* en `/etc/lvm/lvm.conf` configurando `use_lvmetad=0`.

### Crear una copia de una instalación de Arch existente

Es posible replicar una instalación existente de Arch Linux copiando el sistema de archivos del sistema anfitrión a la nueva partición y hacer algunos ajustes para que sea arrancable y única.

El primer paso es copiar los archivos del anfitrión en la nueva partición montada, para esto, considere usar el enfoque presentado en [rsync#Full system backup](/index.php/Rsync#Full_system_backup "Rsync").

Luego, siga el procedimiento descrito en [Installation guide (Español)#Configuración del sistema](/index.php/Installation_guide_(Espa%C3%B1ol)#Configuración_del_sistema "Installation guide (Español)") con algunas salvedades y pasos adicionales:

*   [Installation guide (Español)#Zona horaria](/index.php/Installation_guide_(Espa%C3%B1ol)#Zona_horaria "Installation guide (Español)"), [Installation guide (Español)#Idioma del sistema](/index.php/Installation_guide_(Espa%C3%B1ol)#Idioma_del_sistema "Installation guide (Español)") y [Installation guide (Español)#Contraseña de root](/index.php/Installation_guide_(Espa%C3%B1ol)#Contraseña_de_root "Installation guide (Español)") se pueden omitir.
*   [Installation guide (Español)#Initramfs](/index.php/Installation_guide_(Espa%C3%B1ol)#Initramfs "Installation guide (Español)") puede ser necesario en particular si se cambia el sistema de archivos, por ejemplo de [ext4 (Español)](/index.php/Ext4_(Espa%C3%B1ol) "Ext4 (Español)") a [Btrfs](/index.php/Btrfs "Btrfs").
*   Con respecto a [Installation guide (Español)#Instalar gestor de arranque](/index.php/Installation_guide_(Espa%C3%B1ol)#Instalar_gestor_de_arranque "Installation guide (Español)"), es necesario reinstalar el cargador de arranque.
*   Elimine `/etc/machine-id` para que se genere un id nuevo y único en el próximo arranque.

Si la instalación replicada de Arch se quiere usar dentro de una configuración diferente o con otro hardware, considere las siguientes operaciones adicionales:

*   Utilice [microcode](/index.php/Microcode_(Espa%C3%B1ol) "Microcode (Español)") para la actualización de la CPU adaptada al sistema de destino durante el paso [Installation guide (Español)#Instalar gestor de arranque](/index.php/Installation_guide_(Espa%C3%B1ol)#Instalar_gestor_de_arranque "Installation guide (Español)").
*   Si alguna [Xorg (Español)#Configuración](/index.php/Xorg_(Espa%C3%B1ol)#Configuración "Xorg (Español)") específica estuvo presente en el anfitrión y puede ser incompatible con el sistema de destino, siga [Moving an existing install into (or out of) a virtual machine#Disable any Xorg-related files](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine#Disable_any_Xorg-related_files "Moving an existing install into (or out of) a virtual machine").
*   Realice cualquier otro ajuste apropiado para el sistema de destino, como reconfigurar la red o el audio.

## Desde un sistema anfitrión que ejecuta otra distribución de Linux

Existen múltiples herramientas que automatizan una gran parte de los pasos descritos en las siguientes subsecciones. Consulte sus respectivas páginas de inicio para obtener instrucciones detalladas.

*   [arch-bootstrap](https://github.com/tokland/arch-bootstrap) (Bash)
*   [digitalocean-debian-to-arch](https://github.com/gh2o/digitalocean-debian-to-arch) (disco de reparticionado, específico de DigitalOCean)
*   [image-bootstrap](https://github.com/hartwork/image-bootstrap) (Python)
*   [vps2arch](https://gitlab.com/drizzt/vps2arch) (Bash)

En las siguientes subsecciones se presenta la forma de hacerlo manualmente. La idea es hacer que [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") trabaje directamente en el sistema anfitrión, o ejecutar un sistema Arch dentro del sistema anfitrión, con la instalación real ejecutada desde el sistema Arch. El sistema anidado estará contenido dentro de un entorno chroot.

### Utilizar pacman desde el sistema anfitrión

[Pacman](https://git.archlinux.org/pacman.git/) puede compilarse en la mayoría de las distribuciones de Linux y usarse directamente en el sistema anfitrión para arrancar Arch Linux. El script [arch-install-scripts](https://git.archlinux.org/arch-install-scripts.git/about/) debería ejecutarse sin problemas directamente de las fuentes descargadas en cualquier distribución reciente.

Algunas distribuciones proporcionan un paquete para *pacman* y/o *arch-install-scripts* en sus repositorios oficiales que pueden usarse para este propósito. Desde febrero de 2019, se sabe que «Gentoo» proporciona el paquete *pacman*, y «Alpine Linux» y «Fedora» se sabe que proporcionan tanto *pacman* como *arch-install-scripts*.

### Crear un entorno chroot

A continuación se presentan dos métodos para configurar e ingresar en chroot, desde el más fácil hasta el más complicado. Seleccione solo uno de los dos métodos. Luego, continúe en [#Utilizar un entorno chroot](#Utilizar_un_entorno_chroot).

#### Método A: utilizar una imagen de bootstrap (recomendado)

Descargue la imagen de bootstrap desde un [servidor de réplica](https://www.archlinux.org/download) en `/tmp`.

También puede descargar la firma (misma URL con `.sig` añadido) y [verifíquela con GnuPG](/index.php/GnuPG#Verify_a_signature "GnuPG").

Extraiga el tarball:

```
# tar xzf <path-to-bootstrap-image>/archlinux-bootstrap-*-x86_64.tar.gz

```

Seleccione un servidor de repositorio editando `/tmp/root.x86_64/etc/pacman.d/mirrorlist`.

Entre en entorno chroot:

*   Si tiene instalado bash 4 o posterior, y la orden unshare admite las opciones --fork y--pid, ejecute:

```
# /tmp/root.x86_64/bin/arch-chroot /tmp/root.x86_64/

```

*   De lo contrario, ejecute las siguientes órdenes:

```
# mount --bind /tmp/root.x86_64 /tmp/root.x86_64
# cd /tmp/root.x86_64
# cp /etc/resolv.conf etc
# mount -t proc /proc proc
# mount --make-rslave --rbind /sys sys
# mount --make-rslave --rbind /dev dev
# mount --make-rslave --rbind /run run    ## (suponiendo que /run existe en el sistema)
# chroot /tmp/root.x86_64 /bin/bash

```

#### Método B: utilizar una imagen LiveCD

Es posible montar la imagen raíz desde el soporte de instalación de Arch Linux más reciente y luego hacer un chroot en ella. Este método tiene la ventaja de proporcionar una instalación de Arch Linux en funcionamiento dentro del sistema anfitrión sin la necesidad de prepararlo instalando paquetes específicos.

**Nota:** antes de continuar, asegúrese de que la última versión de [squashfs](http://squashfs.sourceforge.net/) esté instalada en el sistema anfitrión. De lo contrario, obtendrá errores como los siguientes: `FATAL ERROR aborting: uncompress_inode_table: failed to read block`.

*   La imagen raíz se puede encontrar en uno de los [servidores de réplicas](https://www.archlinux.org/download) en `arch/x86_64/`. El formato squashfs no es editable, por lo que realizamos la descompresión de la imagen raíz con unsquash y la montamos.

*   Para realizar unsquash de la imagen raíz, ejecute:

```
# unsquashfs airootfs.sfs

```

*   Antes de [efectuar chroot](/index.php/Chroot_(Espa%C3%B1ol) "Chroot (Español)"), necesitamos configurar algunos puntos de montaje y copiar el archivo resolv.conf a fin tener conexión de red:

```
# mount --bind squashfs-root squashfs-root
# mount -t proc none squashfs-root/proc
# mount -t sysfs none squashfs-root/sys
# mount -o bind /dev squashfs-root/dev
# mount -o bind /dev/pts squashfs-root/dev/pts   ## importante para pacman (para comprobar la firma)
# cp -L /etc/resolv.conf squashfs-root/etc   ## esto es necesario para usar la red dentro del chroot

```

*   Ahora, todo está preparado para pasar al entorno chroot en el recién instalado entorno de Arch:

```
# chroot squashfs-root bash

```

### Utilizar un entorno chroot

El entorno de arranque es realmente básico (sin [nano](https://www.archlinux.org/packages/?name=nano) o [lvm2](https://www.archlinux.org/packages/?name=lvm2)). Por lo tanto, necesitamos configurar pacman para descargar otros paquetes necesarios.

#### Inicializar el depósito de claves de pacman

Las claves de pacman deben configurarse antes de comenzar la instalación. Antes de ejecutar las siguientes dos órdenes, lea [pacman-key (Español)#Inicializar el depósito de claves](/index.php/Pacman-key_(Espa%C3%B1ol)#Inicializar_el_depósito_de_claves "Pacman-key (Español)") para comprender los requisitos de la entropía:

```
# pacman-key --init
# pacman-key --populate archlinux

```

**Sugerencia:** la instalación y ejecución de [haveged](https://www.archlinux.org/packages/?name=haveged) debe realizarse en el sistema anfitrión, ya que no es posible instalar paquetes antes de inicializar pacman keyring y porque *systemd* detectará que se está ejecutando en un entorno chroot e [ignorará la solicitud de activación](https://superuser.com/questions/688733/start-a-systemd-service-inside-chroot). Si continúa haciendo `ls -Ra /` en otra consola (TTY, terminal, SSH session...), no tenga miedo de ejecutarlo en un bucle varias veces: cinco o seis veces de repetición desde el sistema anfitrión será suficiente para generar suficiente entropía en un servidor remoto sin encabezado.

#### Seleccionar un servidor de réplica y descargar herramientas básicas

Después de [seleccionar un servidor de réplica](/index.php/Mirrors_(Espa%C3%B1ol)#Activar_un_servidor_de_réplica_específico "Mirrors (Español)"), [actualice la lista de paquetes](/index.php/Mirrors_(Espa%C3%B1ol)#Forzar_a_pacman_a_actualizar_las_listas_de_paquetes "Mirrors (Español)") e [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") lo que necesite: [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), [parted](https://www.archlinux.org/packages/?name=parted), etc.

**Nota:**

*   Como todavía no hay ningún editor de texto, debe salir de arch-chroot y editar la lista de servidores de réplicas utilizando el editor de texto del anfitrión.
*   Puede que cuando intente instalar paquetes con pacman, obtenga `*error: could not determine cachedir mount point /var/cache/pacman/pkg*`. Para solucionarlo, puede ejecutar: `mount --bind *directory-to-livecd-or-bootstrap* *directory-to-livecd-or-bootstrap*` antes de realizar chroot. Vea [FS#46169](https://bugs.archlinux.org/task/46169).

### Sugerencias de instalación

Ahora puede continuar con [Installation guide (Español)#Particionar el disco](/index.php/Installation_guide_(Espa%C3%B1ol)#Particionar_el_disco "Installation guide (Español)") y seguir el resto de la [Installation guide (Español)](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)").

Algunos sistemas anfitriones o configuraciones pueden requerir ciertos pasos adicionales. Consulte las secciones siguientes para obtener consejos.

##### Anfitrión basado en Debian

###### /dev/shm

En algunos sistemas anfitriones basados en Debian, *pacstrap* puede producir el siguiente error:

 `# pacstrap /mnt base` 
```
==> Creating install root at /mnt
mount: mount point /mnt/dev/shm is a symbolic link to nowhere
==> ERROR: failed to setup API filesystems in new root

```

Esto se debe a que en algunas versiones de Debian, `/dev/shm` apunta a `/run/shm`, mientras que en el entorno chroot basado en Arch, `/run/shm` no existe y el enlace está roto. Para corregir este error, cree un directorio `/run/shm`:

```
# mkdir /run/shm

```

###### /dev/pts

Al instalar `archlinux-2015.07.01-x86_64` desde un sistema anfitrión Debian 7, el siguiente error impidió que tanto [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) como [arch-chroot](/index.php/Chroot_(Espa%C3%B1ol)#Usando_arch-chroot "Chroot (Español)") funcionasen:

 `# pacstrap -i /mnt` 
```
mount: mount point /mnt/dev/pts does not exist
==> ERROR: failed to setup chroot /mnt

```

Aparentemente, esto se debe a que estos dos scripts usan una característica común. `chroot_setup()`[[1]](https://projects.archlinux.org/arch-install-scripts.git/tree/common#n76) se basa en las nuevas características de [util-linux](https://www.archlinux.org/packages/?name=util-linux), que son incompatibles con Debian 7 (vea [FS#45737](https://bugs.archlinux.org/task/45737)).

La solución para *pacstrap* consiste en ejecutar manualmente sus [diversas tareas](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in#n77), pero utilizando el [procedimiento normal](/index.php/Chroot_(Espa%C3%B1ol)#Usando_arch-chroot "Chroot (Español)") para montar los sistemas de archivos del kernel en el directorio de destino (`"$newroot"`):

```
# newroot=/mnt
# mkdir -m 0755 -p "$newroot"/var/{cache/pacman/pkg,lib/pacman,log} "$newroot"/{dev,run,etc}
# mkdir -m 1777 -p "$newroot"/tmp
# mkdir -m 0555 -p "$newroot"/{sys,proc}
# mount --bind "$newroot" "$newroot"
# mount -t proc /proc "$newroot/proc"
# mount --rbind /sys "$newroot/sys"
# mount --rbind /run "$newroot/run"
# mount --rbind /dev "$newroot/dev"
# pacman -r "$newroot" --cachedir="$newroot/var/cache/pacman/pkg" -Sy base base-devel ... ## add the packages you want
# cp -a /etc/pacman.d/gnupg "$newroot/etc/pacman.d/"       ## copy keyring
# cp -a /etc/pacman.d/mirrorlist "$newroot/etc/pacman.d/"  ## copy mirrorlist

```

En lugar de usar *arch-chroot* para realizar [chroot](/index.php/Installation_guide_(Espa%C3%B1ol)#Chroot "Installation guide (Español)"), simplemente utilice:

```
# chroot "$newroot"

```

###### lvmetad

Intentar crear [volúmenes lógicos](/index.php/LVM_(Espa%C3%B1ol)#Volúmenes_lógicos "LVM (Español)") desde un entorno `archlinux-bootstrap-2015.07.01-x86_64` en un sistema anfitrión Debian 7 dará como resultado el siguiente error:

 `# lvcreate -L 20G lvm -n root` 
```
  /run/lvm/lvmetad.socket: connect failed: No such file or directory
  WARNING: Failed to connect to lvmetad. Falling back to internal scanning.
  /dev/lvm/root: not found: device not cleared
  Aborting. Failed to wipe start of new LV.
```

(El volumen físico y la creación del grupo de volúmenes funcionaron a pesar del fallo `/run/lvm/lvmetad.socket: connect failed: No such file or directory` mostrado.)

Esto podría solucionarse fácilmente creando los volúmenes lógicos fuera de chroot (desde el anfitrión Debian). Luego estarán disponibles una vez que se vuelva a entrar en chroot.

Además, si el sistema que está utilizando tiene lvm, es posible que obtenga la siguiente salida:

 `# grub-install --target=i386-pc --recheck /dev/main/archroot` 
```
Installing for i386-pc platform.
  /run/lvm/lvmetad.socket: connect failed: No such file or directory
  WARNING: Failed to connect to lvmetad. Falling back to internal scanning.
  /run/lvm/lvmetad.socket: connect failed: No such file or directory
  WARNING: Failed to connect to lvmetad. Falling back to internal scanning.
  /run/lvm/lvmetad.socket: connect failed: No such file or directory
  WARNING: Failed to connect to lvmetad. Falling back to internal scanning.
  /run/lvm/lvmetad.socket: connect failed: No such file or directory
  WARNING: Failed to connect to lvmetad. Falling back to internal scanning.
  /run/lvm/lvmetad.socket: connect failed: No such file or directory
  WARNING: Failed to connect to lvmetad. Falling back to internal scanning.
```

Esto se debe a que debian no usa lvmetad por defecto. Debe editar `/etc/lvm/lvm.conf` y establecer `use_lvmetad` en `0`:

```
use_lvmetad = 0

```

Esto dará más tarde un error en el arranque en la etapa initrd. Por lo tanto, debe volver a cambiarlo después de la generación de grub. En un RAID por software + LVM, los pasos serían los siguientes:

*   Después de instalar el sistema, verifique [mkinitcpio](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") y la configuración de su gestor de arranque. Consulte [Arch boot process (Español)#Gestor de arranque](/index.php/Arch_boot_process_(Espa%C3%B1ol)#Gestor_de_arranque "Arch boot process (Español)") para obtener una lista de cargadores de arranque.
*   Es posible que deba cambiar `/etc/mdadm.conf` para que refleje su configuración [RAID](/index.php/RAID_(Espa%C3%B1ol) "RAID (Español)") (si corresponde).
*   Es posible que deba cambiar sus `HOOKS` y `MODULES` de acuerdo con sus requisitos [LVM](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)") y [RAID](/index.php/RAID_(Espa%C3%B1ol) "RAID (Español)"): `MODULES="dm_mod" HOOKS="base udev **mdadm_udev** ... block **lvm2** filesystems ..."`
*   Lo más probable es que necesite generar nuevas imágenes initrd con mkinitcpio. Vea [mkinitcpio (Español)#Creación de la imagen y activación](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Creación_de_la_imagen_y_activación "Mkinitcpio (Español)").
*   Establezca `use_lvmetad = 0` en `/etc/lvm/lvm.conf`.
*   Actualice la configuración de tu gestor de arranque. Consulte la página wiki de su gestor de arranque para más detalles.
*   Establezca `use_lvmetad = 1` en `/etc/lvm/lvm.conf`.

##### Anfitrión basado en Fedora

En sistemas anfitriones basados en Fedora y USB live, puede encontrar problemas al usar *genfstab* para generar su [fstab](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)"). Elimine las entradas duplicadas y la opción «seclabel» donde aparezca, ya que esto es específico de Fedora y evitará que su sistema arranque normalmente.

## Cosas que verificar antes de reiniciar

Antes de reiniciar, vuelva a verificar algunos detalles en su instalación para lograr una instalación exitosa. Para hacerlo, primero entre en chroot en el sistema recién instalado y luego:

*   [Cree un usuario con contraseña](/index.php/Users_and_groups_(Espa%C3%B1ol)#Administración_de_grupos "Users and groups (Español)"), para que pueda iniciar sesión a través de *sh*. Esto es crítico ya que el inicio de sesión raíz está desactivado por defecto desde OpenSSH-7.1p2.
*   [Establezca una contraseña de root](/index.php/Users_and_groups_(Espa%C3%B1ol)#Administración_de_grupos "Users and groups (Español)") para que pueda cambiar a root a través de *su* más tarde.
*   [Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") una solución [ssh](/index.php/Ssh "Ssh") y [active](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") su instancia de servidor para iniciarse automáticamente en el arranque.
*   Configure su [conexión de red](/index.php/Network_configuration "Network configuration") para que la conexión se inicie automáticamente en el arranque.
*   Configure un [gesgtor de arranque](/index.php/Boot_loader_(Espa%C3%B1ol) "Boot loader (Español)") y configúrelo para usar la partición de intercambio que se apropió anteriormente como la partición raíz. Es posible que desee configurar su gestor de arranque para poder arrancar en su sistema anterior; es útil reutilizar la partición `/boot` existente del servidor en el nuevo sistema para este propósito.

## Reemplazar el sistema existente sin un LiveCD

Encuentre ~700 MB de espacio libre en algún lugar del disco, por ejemplo, formateando una partición de intercambio. Puede desactivar la partición de intercambio y configurar su sistema allí.

### Establecer la antigua partición de intercambio como nueva partición raíz

Compruebe `cfdisk`, `/proc/swaps` o `/etc/fstab` para encontrar su partición de intercambio. Suponiendo que su disco duro esté ubicado en `sda*X*` (`*X*` será un número).

Haga lo siguiente:

Desactive el espacio de intercambio:

```
# swapoff /dev/sda*X*

```

Crea un sistema de archivos en él:

```
# fdisk /dev/sda
(establezca el campo de identificación de /dev/sda*X* para "Linux" - Hex 83)
# mke2fs -j /dev/sda*X*

```

Crea un directorio para montarlo:La instalación de Arch Linux

```
# mkdir /mnt/newsys

```

Finalmente, monte el nuevo directorio para instalar el sistema:

```
# mount -t ext4 /dev/sda*X* /mnt/newsys

```

### Instalación

[Instale los paquetes esenciales](/index.php/Installation_guide_(Espa%C3%B1ol)#Instalar_paquetes_esenciales "Installation guide (Español)") y cualquier otro paquete requerido para obtener un sistema con conexión a Internet en funcionamiento en la partición temporal, teniendo cuidado con el límite de los ~700 MB de espacio. Cuando especifique paquetes para instalar con *pacstrap*, considere agregar el indicador `-c` para evitar llenar un espacio valioso descargando paquetes al sistema anfitrión.

Una vez que el nuevo sistema Arch Linux esté instalado, arregle la configuración del cargador de arranque, luego reinicie en el sistema recién creado y realice [rsync de todo el sistema](/index.php/Rsync#Full_system_backup "Rsync") en la partición primaria.