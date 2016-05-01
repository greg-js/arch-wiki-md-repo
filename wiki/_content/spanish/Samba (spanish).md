(Traducción del artículo en inglés en curso)

## Contents

*   [1 Introducción](#Introducci.C3.B3n)
*   [2 Instalación](#Instalaci.C3.B3n)
*   [3 Configuración](#Configuraci.C3.B3n)
    *   [3.1 Iniciando el demonio](#Iniciando_el_demonio)
    *   [3.2 SWAT: Herramienta de administración web de Samba](#SWAT:_Herramienta_de_administraci.C3.B3n_web_de_Samba)
    *   [3.3 Añadiendo usuarios](#A.C3.B1adiendo_usuarios)
*   [4 Accediendo a los intercambios Samba](#Accediendo_a_los_intercambios_Samba)
    *   [4.1 Desde Gnome](#Desde_Gnome)
    *   [4.2 Desde otros entornos gráficos](#Desde_otros_entornos_gr.C3.A1ficos)
    *   [4.3 Desde una consola](#Desde_una_consola)
    *   [4.4 Montando una compartición de Samba](#Montando_una_compartici.C3.B3n_de_Samba)
    *   [4.5 Agregando una comparticion a fstab](#Agregando_una_comparticion_a_fstab)
*   [5 Compartiendo archivos en tu LAN sin usuario y contraseña](#Compartiendo_archivos_en_tu_LAN_sin_usuario_y_contrase.C3.B1a)
    *   [5.1 Ejemplo de archivo de configuración](#Ejemplo_de_archivo_de_configuraci.C3.B3n)
*   [6 Solución de problemas](#Soluci.C3.B3n_de_problemas)
*   [7 Ver también](#Ver_tambi.C3.A9n)
*   [8 Mas Recursos](#Mas_Recursos)

## Introducción

Samba es una reimplementación del protocolo de red SMB/CIFS. Facilita el intercambio de ficheros y de impresoras entre sistemas Linux y Windows, o entre sistemas Linux -como una alternativa a [NFS](/index.php/NFS "NFS"). Se configura fácilmente.

## Instalación

Para instalar el servidor Samba, instala el paquete *samba*

```
# pacman -S samba

```

## Configuración

Identificado como superusuario (root), copia el fichero por defecto de Samba a */etc/samba/smb.conf*

```
# cp /etc/samba/smb.conf.default /etc/samba/smb.conf

```

Abre */etc/samba/smb.conf* y edítalo según tus necesidades. El fichero está comentado y proporciona varios ejemplos. No debería ser difícil de entender.

El fichero, por defecto, crea una carpeta de intercambio para cada usuario. También crea un intercambio de impresoras.

### Iniciando el demonio

Samba puede ser iniciado con

```
# /etc/rc.d/samba start

```

Samba normalmente usa [FAM](/index.php/FAM "FAM") para vigilar los cambios en el sistema de ficheros. Necesitarás tener el demonio *fam* iniciado antes que *samba*. Una alternativa es usar [Gamin](/index.php/Gamin "Gamin")

Añade samba a la línea DAEMONS en *[rc.conf](/index.php/Rc.conf "Rc.conf")* para iniciar el demonio en cada arranque.

### SWAT: Herramienta de administración web de Samba

SWAT es una herramienta que es parte de Samba. El ejecutable principal se llama swat y se invoca el daemon extendido de [xinetd](https://en.wikipedia.org/wiki/xinetd "wikipedia:xinetd").

Hay muchas y variadas opiniones acerca de la utilidad de SWAT. No importa cómo uno intenta producir la herramienta de configuración perfecta, sigue siendo objeto de gustos personales. SWAT es una herramienta que permite la configuración basada en Web de Samba. Tiene un asistente que puede ayudar a obtener una configurado de Samba rápidamente, tiene ayuda contextual en cada parámetro de smb.conf, proporciona un seguimiento del estado actual de la información de la conexión, y permite la administración de contraseñas de red de MS Windows de toda la red.[[1]](http://samba.xsec.it/samba/docs/man/Samba-HOWTO-Collection/SWAT.html)

**Nota:** Si tiene problemas con estas instrucciones, puede utilizar la herramienta de Webmin en su lugar y fácilmente cargar el módulo SWAT allí.

**Advertencia:** Antes de utilizar SWAT, por favor tenga en cuenta que SWAT reemplazará completamente su smb.conf con un archivo totalmente optimizado que ha sido despojado de todos los comentarios que puede haber situado allí, y ninguna configuración no predeterminada se escribirán en el archivo.

Para utilizar SWAT, primero instale xinetd:

```
# pacman -S xinetd

```

Edita `/etc/xinetd.d/swat` usando tu editor de texto favorito. Para abilitar SWAT, cambie la linea `disable = yes` a `disable = no`.

```
service swat
{
        type                    = UNLISTED
        protocol                = tcp
        port                    = 901
        socket_type             = stream
        wait                    = no
        user                    = root
        server                  = /usr/sbin/swat
        log_on_success          += HOST DURATION
        log_on_failure          += HOST
        disable                 = no
}

```

Añade las entradas swat y swat_tunnel a `/etc/services` con los siguientes comandos usados como usuario root:[[2]](http://www.escomposlinux.org/lfs-es/blfs-es-6.0/server/samba3.html)

```
# echo "swat            901/tcp" >> /etc/services && echo "swat_tunnel     902/tcp" >> /etc/services

```

Si xinetd fue compilado con apoyo a tcp_wrappers (como es el predeterminado en arch), editar `/etc/hosts.allow` añadiendo después de línea:

```
swat:127.0.0.1

```

Para iniciar el daemon xinetd:

```
# /etc/rc.d/xinetd start

```

Puedes acceder a la interfaz web en el puerto 901 por defecto,

```
[http://localhost:901/](http://localhost:901/)

```

### Añadiendo usuarios

Para usar Samba necesitarás añadir un usuario:

```
# smbpasswd -a <user>

```

El usuario debe tener una cuenta en el servidor. Si el usuario no existe recibirás el error:

```
Failed to modify password entry for user "<user>"

```

Puedes añadir un nuevo usuario con [adduser](/index.php/User_Management#adduser "User Management")

## Accediendo a los intercambios Samba

KDE y Gnome pueden navegar por los directorios de intercambio Samba. De este modo, no necesitas ningún paquete adicional necesario si usas estos entornos de escritorio. (Sin embargo, para una GUI en la configuración del sistema de KDE usted tiene que instalar el paquete kdenetwork-filesharing package de [extra]. Otra opción es el programa es SMB4K). Si, por el contrario, tienes pensado el intercambio desde una consola de comandos, necesitarás un paquete más.

### Desde Gnome

Instala primero el paquete gvfs-smb

```
pacman -S gvfs-smb

```

En una ventana de Nautilus, presiona `ctrl`+`L` o ve al menú "Go-Ir" y selecciona "Lugar..." (N.T. no tengo Gnome, si esto es otra palabra que alguien lo edite si le place claro :) ). Cualquiera de las dos acciones te permitirá introducir **smb://servername/share** en la barra que aparece `Enter`.

**Note:** Si no tienes el nombre del servidor en el `/etc/hosts`, debes usar la direción IP del mismo en lugar del nombre.

```
smb://servername/sharename

```

or

```
smb://192.168.1.5/sharename

```

En KDE, es prácticamente igual (N.T. ídem). Para una interfaz gráfica necesitas instalar el paquete "kdenetwork-filesharing" desde el repositorio Extra.

### Desde otros entornos gráficos

Hay una serie de programas útiles, pero necesitan tener paquetes creados para ellos. Esto puede hacerse con el sistema de compilación de paquete de arch. Lo bueno de estos otros es que no necesitan un entorno particular a instalarse para apoyarlos, y así ser mas livianos.

LinNeighborhood es simple y genérico esplorador LAN y montador de comparticion. No muy bonito, pero efectivo.

Otros programas posibles son pyneighborhood, el plugin xffm-samba para Xffm y Gigolo.

### Desde una consola

Puedes también usar smbclient para navegar por la red desde la consola.

```
$ smbclient -L <hostname> -U%

```

Listará los directorios públicos del servidor

### Montando una compartición de Samba

Para montar manualmente una compartición a traves del shell:

```
# mount.cifs //<hostname>/<share> <punto_de_montaje> -o user=<username>,password=<password>

```

Para permitir a montar y desmontar una comparticion samba a un usuario normal puedes agregar setuid root a */sbin/mount.cifs*. Una alternativa es usar el paquete [smbnetfs](/index.php?title=Smbnetfs&action=edit&redlink=1 "Smbnetfs (page does not exist)").

### Agregando una comparticion a fstab

Puedes agregar una linea a *[fstab](/index.php/Fstab "Fstab")* de este modo:

```
//<hostname>/<share> <mount_point> cifs credentials=<credentials_file>,rw,user,noauto 0 0

```

Al ser fstab legible por todos los usuarios, no queremos poner nuestra contraseña Samba en este archivo. En este caso podemos usar un archivo de credenciales solo legible por ti. Es un simple archivo de texto que contiene:

```
username=<username>
password=<password>

```

La opción *user* de la línea de fstab permite al propietario del <punto_de_montaje>, montar y desmontar la compartición. La opción *noauto* desabilita el montaje en el arranque.

Si estas agreagando una compartición Samba a *[fstab](/index.php/Fstab "Fstab")*, debes agrear también el demonio *[netfs](/index.php?title=Netfs&action=edit&redlink=1 "Netfs (page does not exist)")* a *[rc.conf](/index.php/Rc.conf "Rc.conf")*, en algun lugar después del demonio *[network](/index.php/Network "Network")*. El demonio *netfs* montará particiones de red en el arranque y, mas importante, desmontar particiones de red en el apagado. Incluso si estás usando la opción *noauto* en fstab debes agregar el demonio *netfs* . Sin él cualquier comparticion de red que es desmontada cuando apagues la máquina, causará que el demonio *network* espere al time out de la conexión, extendiendo considerablemente el tiempo de apagado.

## Compartiendo archivos en tu LAN sin usuario y contraseña

Editar el /etc/samba/smb.conf por defecto en las siguientes líneas:

```
security = user

```

a

```
security = share

```

Si quieres restringir los datos compartidos a una interfaz específica, reemplaza

```
;   interfaces = 192.168.12.2/24 192.168.13.2/24

```

a (reemplaza eth0 a la red local en que quieras compartir)

```
interfaces = lo eth0
bind interfaces only = true

```

si quieres editar la cuenta que accede a los elementos compartidos, edita la siguiente línea:

```
;   guest account = nobody

```

El último paso es crear un directorio compartido (para permitir la escritura colocar: writable = yes):

```
[Public Share]
path = /ruta/hacia/la/comparticion/publica
available = yes
browsable = yes
public = yes
writable = no

```

### Ejemplo de archivo de configuración

La configuración que me funcionó:

```
[global]
workgroup = WORKGROUP
server string = Samba Server
netbios name = PC_NAME
security = share
; la línea de abajo es importante! Si tienes problemas de permisos asegúrate de que el usuario es el mismo que el usuario de la carpeta que desea compartir
guest account = mark
username map = /etc/samba/smbusers
name resolve order = hosts wins bcast
wins support = no

[public]
comment = Public Share
path = /path/to/public/share
available = yes
browsable = yes
public = yes
writable = no

```

## Solución de problemas

Si estás teniendo problemas accediendo a una compartición protegida desde Windows, prueba agregando esta línea al archivo /etc/samba/smb.conf [Sugerencia encontrada aquí](http://blogs.computerworld.com/networking_nightmare_ii_adding_linux)

```
[global]
# THE LANMAN FIX
client lanman auth = yes
client ntlmv2 auth = no

```

## Ver también

*   [Samba domain controller](/index.php/Samba_domain_controller "Samba domain controller")

## Mas Recursos

*   [Samba](http://wiki.archlinux.de/?title=Samba) Samba (German) (archlinux.de)
*   [Sitio de Samba Oficial](http://www.samba.org)
*   [Samba: An Introduction](http://www.samba.org/samba/docs/SambaIntro.html)