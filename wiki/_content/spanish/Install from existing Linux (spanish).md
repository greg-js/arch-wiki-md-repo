Este documento describe el proceso de [bootstrapping](https://en.wikipedia.org/wiki/es:Bootstrapping_(inform%C3%A1tica) necesario para instalar Arch Linux desde un sistema anfitrión de Linux en ejecución. Después del bootstrapping, la instalación continúa como se describe en la [guía de instalación](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)").

La instalación de Arch Linux desde un sistema Linux en ejecución es útil para:

*   instalar remótamente Arch Linux, por ejemplo, un servidor root (virtual)
*   sustituir un Linux existente sin un LiveCD (véase [#Sustituir el sistema existente sin un LiveCD](#Sustituir_el_sistema_existente_sin_un_LiveCD))
*   crear un distribución Linux nueva o LiveCD basada en Arch Linux
*   crear un entorno chroot de Arch Linux, por ejemplo para un contenedor de base Docker
*   [rootfs-sobre-NFS para máquinas sin disco](/index.php/Diskless_network_boot_NFS_root "Diskless network boot NFS root")

El objetivo del procedimiento de bootstrapping es configurar un entorno desde el que ejecutar los [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) (tales como `pacstrap` y `arch-root`). Este objetivo se logra mediante la instalación de los [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) nativos en un sistema anfitrión, o configurando un entorno chroot basado en Arch Linux.

Si el sistema anfitrión ejecuta Arch Linux, la instalación de los [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) es sencilla.

Desde otras distribuciones, el proceso es más complicado (el cual se describe en [#Alternativa: Instalación de los arch-install-scripts nativos en una distribución que no sea Arch](#Alternativa:_Instalaci.C3.B3n_de_los_arch-install-scripts_nativos_en_una_distribuci.C3.B3n_que_no_sea_Arch)). Para estas distribuciones, se recomienda la creación de un entorno chroot en su lugar.

**Nota:** Esta guía requiere que el sistema anfitrión existente sea capaz de ejecutar los nuevos programas de Arch Linux para la arquitectura de destino. En el caso de un anfitrión x86_64, es posible utilizar i686-Pacman para construir un entorno chroot de 32 bits. Véase [Arch64 Install bundled 32bit system](/index.php/Arch64_Install_bundled_32bit_system "Arch64 Install bundled 32bit system"). Sin embargo, no es tan fácil construir un entorno de 64 bits cuando el anfitrión solo permite ejecutar programas de 32 bits.

## Contents

*   [1 Efectuar chroot basado en Arch Linux](#Efectuar_chroot_basado_en_Arch_Linux)
    *   [1.1 Método 1: Utilizar la imagen Bootstrap](#M.C3.A9todo_1:_Utilizar_la_imagen_Bootstrap)
    *   [1.2 Método 2: Utilizar la imagen del LiveCD](#M.C3.A9todo_2:_Utilizar_la_imagen_del_LiveCD)
    *   [1.3 Método 3: Montar manulamente el entorno chroot (con un script)](#M.C3.A9todo_3:_Montar_manulamente_el_entorno_chroot_.28con_un_script.29)
    *   [1.4 Utilizar el entorno chroot](#Utilizar_el_entorno_chroot)
        *   [1.4.1 Inicializar pacman keyring](#Inicializar_pacman_keyring)
        *   [1.4.2 Instalación](#Instalaci.C3.B3n)
            *   [1.4.2.1 Anfitrión basado en Debian](#Anfitri.C3.B3n_basado_en_Debian)
        *   [1.4.3 Configurar el sistema](#Configurar_el_sistema)
*   [2 Sustituir el sistema existente sin un LiveCD](#Sustituir_el_sistema_existente_sin_un_LiveCD)

## Efectuar chroot basado en Arch Linux

La idea es ejecutar un sistema Arch en el sistema anfitrión. La instalación en curso se ejecuta desde este sistema Arch. Este sistema anidado está contenido dentro de un entorno chroot. Existen tres métodos para configurar e introducirnos en un entorno chroot, que se presentan a continuación, desde el más sencillo hasta el más complejo.

**Nota:** Su sistema anfitrión debe ejecutar Linux 2.6.32 o superior

### Método 1: Utilizar la imagen Bootstrap

Descargue la imagen Bootstrap desde un [servidor de réplica](https://www.archlinux.org/download):

```
 curl -O [http://www.gtlib.gatech.edu/pub/archlinux/iso/2013.10.01/archlinux-bootstrap-2013.10.01-x86_64.tar.gz](http://www.gtlib.gatech.edu/pub/archlinux/iso/2013.10.01/archlinux-bootstrap-2013.10.01-x86_64.tar.gz)

```

Extraiga el archivo tar:

```
 # cd /tmp
 # tar xzf <path-to-bootstrap-image>/archlinux-bootstrap-2013.10.01-x86_64.tar.gz

```

Seleccione un servidor de repositorio:

```
 # nano /tmp/root.x86_64/etc/pacman.d/mirrorlist

```

Entre en el entorno chroot:

*   Si tiene bash 4 o superior instalado:

```
  # /tmp/root.x86_64/bin/arch-chroot /tmp/root.x86_64/

```

*   Si es que no, ejecute las órdenes suiguientes:

```
  # cp /etc/resolv.conf /tmp/root.x86_64/etc
  # mount --rbind /proc /tmp/root.x86_64/proc
  # mount --rbind /sys /tmp/root.x86_64/sys
  # mount --rbind /dev /tmp/root.x86_64/dev
  # mount --rbind /run /tmp/root.x86_64/run
    (presumiento que /run exista en su sistema)
  # chroot /tmp/root.x86_64/

```

### Método 2: Utilizar la imagen del LiveCD

Es posible montar la imagen root con el soporte de instalación de Arch Linux más reciente y luego efectuar chroot en él. Este método tiene la ventaja de que proporciona una instalación de Arch Linux funcionando bien dentro de su sistema anfitrión, sin necesidad de prepararlo mediante la instalación de paquetes específicos.

**Nota:** Antes de continuar, asegúrese de que la última versión de [squashfs](http://squashfs.sourceforge.net/) está instalada en el sistema anfitrión. De lo contrario, se producirán errores como: `FATAL ERROR aborting: uncompress_inode_table: failed to read block`.

*   La imagen root se puede encontrar en uno de los [servidores de réplica](https://www.archlinux.org/download), disponible tanto para arquitecturas x86_64 como i686, dependiendo de sus necesidades.El formato squashfs no es editable, así que efectuaremos *unsquash* de la imagen root y luego la monteremos.

*   Para efectuar unsquash de la imagen root, ejecute:

 `# unsquashfs -d /squashfs-root root-image.fs.sfs` 

*   Ahora se puede montar la imagen root con la opción loop:

```
# mkdir /arch
# mount -o loop /squashfs-root/root-image.fs /arch

```

*   Antes de [enjaularlo](/index.php/Change_root "Change root"), tenemos que establecer algunos puntos de montaje y copiar el archivo resolv.conf para las conexiones de red:

```
# mount -t proc none /arch/proc
# mount -t sysfs none /arch/sys
# mount -o bind /dev /arch/dev
# mount -o bind /dev/pts /arch/dev/pts # important for pacman (for signature check)
# cp -L /etc/resolv.conf /arch/etc #this is needed to use networking within the chroot

```

*   Ahora está todo preparado para enjaular (efectuar chroot) el entorno donde Arch se va a instalar:

 `# chroot /arch bash` 

### Método 3: Montar manulamente el entorno chroot (con un script)

El script crea un directorio llamado `archinstall-pkg` y descarga los paquetes necesarios en él. A continuación, los extrae al directorio `archinstall-chroot`. Por último, prepara los puntos de montaje, configura pacman y enjaula el entorno.

 `archinstall-bootstrap.sh` 
```
#!/bin/bash
# last edited 04\. January 2014
# This script is inspired on the archbootstrap script.

# old PACKAGES=(acl attr bzip2 curl expat glibc gpgme gnupg libarchive libassuan libgcrypt libgpg-error libssh2 lzo2 openssl pacman xz zlib pacman-mirrorlist coreutils bash grep gawk file filesystem tar ncurses readline libcap util-linux pcre arch-install-scripts)
FIRST_PACKAGE=(filesystem)
BASH_PACKAGES=(glibc ncurses readline bash)
PACMAN_PACKAGES=(acl archlinux-keyring attr bzip2 curl expat gnupg gpgme libarchive libassuan libgpg-error libgcrypt libssh2 lzo2 openssl pacman pacman-mirrorlist xz zlib)
EXTRA_PACKAGES=(coreutils tar libcap arch-install-scripts util-linux systemd)
PACKAGES=(${FIRST_PACKAGE[*]} ${BASH_PACKAGES[*]} ${PACMAN_PACKAGES[*]} ${EXTRA_PACKAGES[*]})

# Enable the mirror which best fits for you
# USA
# MIRROR='http://mirrors.kernel.org/archlinux' 
# Germany
# MIRROR='http://archlinux.limun.org'

# You can set the ARCH variable to i686 or x86_64
ARCH=`uname -m`
LIST=`mktemp`
CHROOT_DIR=archinstall-chroot
DIR=archinstall-pkg
mkdir -p "$DIR"
mkdir -p "$CHROOT_DIR"
# Create a list with urls for the arch packages
for REPO in core community extra; do  
        wget -q -O- "$MIRROR/$REPO/os/$ARCH/" |sed  -n "s|.*href=\"\\([^\"]*\\).*|$MIRROR\\/$REPO\\/os\\/$ARCH\\/\\1|p"|grep -v 'sig$'|uniq >> $LIST  
done
# Download and extract each package.
for PACKAGE in ${PACKAGES[*]}; do
        URL=`grep "$PACKAGE-[0-9]" $LIST|head -n1`
        FILE=`echo $URL|sed 's/.*\/\([^\/][^\/]*\)$/\1/'`
        wget "$URL" -c -O "$DIR/$FILE" 
        xz -dc "$DIR/$FILE" | tar x -k -C "$CHROOT_DIR"

        # No error if they exist already
        if [ -f "$CHROOT_DIR/.PKGINFO" ]
        then 
    	    rm "$CHROOT_DIR/.PKGINFO" 
    	fi    
    	if [ -f "$CHROOT_DIR/.MTREE" ]
        then 
    	    rm "$CHROOT_DIR/.MTREE" 
    	fi    
    	if [ -f "$CHROOT_DIR/.INSTALL" ]
        then 
    	    rm "$CHROOT_DIR/.INSTALL" 
    	fi    
done
# Create mount points
mkdir -p "$CHROOT_DIR/dev" "$CHROOT_DIR/proc" "$CHROOT_DIR/sys" "$CHROOT_DIR/mnt"
mount -t proc proc "$CHROOT_DIR/proc/"
mount -t sysfs sys "$CHROOT_DIR/sys/"
mount -o bind /dev "$CHROOT_DIR/dev/"
mkdir -p "$CHROOT_DIR/dev/pts"
mount -t devpts pts "$CHROOT_DIR/dev/pts/"

# Hash for empty password  Created by doing: openssl passwd -1 -salt ihlrowCo and entering an empty password (just press enter)
echo 'root:$1$ihlrowCo$sF0HjA9E8up9DYs258uDQ0:10063:0:99999:7:::' > "$CHROOT_DIR/etc/shadow"
echo "root:x:0:0:root:/root:/bin/bash" > "$CHROOT_DIR/etc/passwd" 
touch "$CHROOT_DIR/etc/group"
echo "myhost" > "$CHROOT_DIR/etc/hostname"
test -e "$CHROOT_DIR/etc/mtab" || echo "rootfs / rootfs rw 0 0" > "$CHROOT_DIR/etc/mtab"
[ -f "/etc/resolv.conf" ] && cp "/etc/resolv.conf" "$CHROOT_DIR/etc/"

# Do you really want to switch the tests off?
#sed -ni '/^[ \t]*CheckSpace/ !p' "$CHROOT_DIR/etc/pacman.conf"
#sed -i "s/^[ \t]*SigLevel[ \t].*/SigLevel = Never/" "$CHROOT_DIR/etc/pacman.conf"

echo "Server = $MIRROR/\$repo/os/$ARCH" >> "$CHROOT_DIR/etc/pacman.d/mirrorlist"

chroot $CHROOT_DIR /usr/bin/pacman -Sy 
chroot $CHROOT_DIR /bin/bash

```

### Utilizar el entorno chroot

#### Inicializar pacman keyring

Antes de iniciar la instalación, las claves de pacman deben ser configuradas. Antes de ejecutar las siguientes órdenes lea [pacman-key#Initializing the keyring](/index.php/Pacman-key#Initializing_the_keyring "Pacman-key") para entender el proceso:

```
# pacman-key --init
# pacman-key --populate archlinux

```

#### Instalación

Siga la [guía para principiantes](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)") sobre [Montar las particiones](/index.php/Installation_guide_(Espa%C3%B1ol)#Montar_las_particiones "Installation guide (Español)") e [Instalar el sistema base](/index.php/Installation_guide_(Espa%C3%B1ol)#Instalaci.C3.B3n_del_sistema_base "Installation guide (Español)").

##### Anfitrión basado en Debian

En los sistemas basados en Debian, `pacstrap` arroja el siguiente error:

```
# pacstrap /mnt base
# ==> Creating install root at /mnt
# mount: mount point /mnt/dev/shm is a symbolic link to nowhere
# ==> ERROR: failed to setup API filesystems in new root

```

En Debian, los puntos de /dev/shm a /run/shm. Sin embargo, en el chroot basado en Arch, /run/shm no existe y el enlace está roto. Para corregir este error, cree un directorio /run/shm:

```
# mkdir /run/shm

```

#### Configurar el sistema

A partír de aquí, basta con seguir la [guía para principiantes](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)") desde [Montar las particiones](/index.php/Installation_guide_(Espa%C3%B1ol)#Montar_las_particiones "Installation guide (Español)").

## Sustituir el sistema existente sin un LiveCD

Encuentre ~500MB de espacio libre en el disco, por ejemplo, redimensionando una partición swap. Instale el nuevo sistema Arch Linux, reinicie desde el sistema recién creado, y realice un [rsync del sistema completo](/index.php/Full_system_backup_with_rsync#With_a_single_command "Full system backup with rsync") para la partición primaria. Fije la configuración del gestor de arranque antes de reiniciar.