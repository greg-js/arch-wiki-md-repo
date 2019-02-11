**Estado de la traducción**
Este artículo es una traducción de [ThinkFinger](/index.php/ThinkFinger "ThinkFinger"), revisada por última vez el **2008-05-06**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=ThinkFinger&diff=0&oldid=40836) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

ThinkFinger es un controlador para el lector de huellas digitales SGS de la empresa Thomson Microelectronics que se monta en la mayoría de portátiles IBM/Lenovo ThinkPad.

**Advertencia:** Las revisiones de ThinkFinger-svn por encima de la 72 requieren que cargue el nódulo *uinput*!

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 TF-Tool](#TF-Tool)
*   [3 Pam](#Pam)
    *   [3.1 /etc/pam.d/login](#/etc/pam.d/login)
    *   [3.2 /etc/pam.d/su](#/etc/pam.d/su)
    *   [3.3 /etc/pam.d/sudo](#/etc/pam.d/sudo)
    *   [3.4 /etc/pam.d/xscreensaver](#/etc/pam.d/xscreensaver)
    *   [3.5 /etc/pam.d/gdm](#/etc/pam.d/gdm)
    *   [3.6 /etc/pam.d/xdm](#/etc/pam.d/xdm)
*   [4 SLiM](#SLiM)
*   [5 Más información](#Más_información)

## Instalación

Consiga el paquete desde [aquí](https://aur.archlinux.org/packages.php?do_Details=1&ID=8250).

## Configuración

### TF-Tool

Utilice *tf-tool* para probar ThinkFinger. Tendrá que ejecutar esto como root debido a que se necesita acceso directo a los dispositivos usb. Ejecute *tf-tool --acquire* para generar un archivo bir y *tf-tool --verify* para ver si le identifica correctamente. *tf-tool --add-user <nombreusuario>* adquiere y alamacena su huella digital en */etc/pam_thinkfinger/nombreusuario.bir*, archivo necesario para una identificación con pam.

## Pam

PAM ("Pluggable Authentication Module") es el módulo insertable de autentificación, inventado por Sun.

### /etc/pam.d/login

Cambie el archivo */etc/pam.d/other* para que se parezca a lo siguiente si quiere utilizar su huella digital para autentificarse a si mismo al ingresar al sistema:

```
#%PAM-1.0
auth           sufficient      pam_thinkfinger.so
auth           required        pam_unix.so use_first_pass nullok_secure
account        required        pam_unix.so
password       required        pam_unix.so
session        required        pam_unix.so

```

### /etc/pam.d/su

Cambie este archivo para confirmar la orden *su* con un suave movimiento circular con el dedo.

```
#%PAM-1.0
auth           sufficient      pam_rootok.so
auth           sufficient      pam_thinkfinger.so
auth           required        pam_unix.so nullok_secure try_first_pass
account        required        pam_unix.so
session        required        pam_unix.so

```

**Sugerencia:** No se olvide de hacer *tf-tool --add-user root* para usar esta característica!

### /etc/pam.d/sudo

Cambie este archivo para confirmar la orden *sudo* con un suave movimiento circular de su dedo.

```
#%PAM-1.0
auth           sufficient      pam_thinkfinger.so
auth           required        pam_unix.so nullok_secure try_first_pass
auth           required        pam_nologin.so

```

### /etc/pam.d/xscreensaver

XScreensaver tiene truco. Primero, configure PAM con un archivo "/etc/pam.d/xscreensaver" que contenga:

```
auth           sufficient      pam_thinkfinger.so
auth           required        pam_unix_auth.so try_first_pass

```

Pero aún así no funcionará porque xscreensaver no puede leer/escribir desde /dev/misc/uinput o /dev/bus/usb*. Se tiene que escribir una regla udev para autorizarle a un grupo el acceso de lectura/escritura.

Primero, cree un grupo nuevo. Le sugiero "fingerprint":

```
> sudo groupadd fingerprint

```

Añada el usuario que quiera que sea capaz de desbloquear xscreensaver con el lector de huellas digitales al grupo:

```
> sudo gpasswd -a <user> fingerprint

```

No olvide salir e ingresar de nuevo.

Haga una búsqueda de los términos "uinput" y "bus/usb" en directorio de reglas udev:

```
> grep -in uinput /etc/udev/rules.d/*
/etc/udev/rules.d/udev.rules:222:KERNEL=="uinput",  NAME="misc/%k", SYMLINK+="%k"
/etc/udev/rules.d/udev.rules:263:KERNEL=="uinput", NAME="input/%k"
> grep -in "bus/usb" /etc/udev/rules.d/*
/etc/udev/rules.d/udev.rules:318:SUBSYSTEM=="usb_device", ACTION=="add", PROGRAM="/bin/sh -c 'K=%k; K=$${K#usbdev};printf bus/usb/%%03i/%%03i $${K%%%%.*} $${K#*.}'", NAME="%c", MODE="0664"
/etc/udev/rules.d/udev.rules:320:SUBSYSTEM=="usb", ACTION=="add", ENV{DEVTYPE}=="usb_device", NAME="bus/usb/$env{BUSNUM}/$env{DEVNUM}", MODE="0664"

```

Ahora copie las ĺineas anteriores (222, 318 y 320 del archivo /etc/udev/rules.d/udev.rules) a un nuevo archivo de reglas udev. Le sugiero /etc/udev/rules.d/99my.rules

```
KERNEL=="uinput",  NAME="misc/%k", SYMLINK+="%k", MODE="0660", GROUP="fingerprint"
SUBSYSTEM=="usb_device", ACTION=="add", PROGRAM="/bin/sh -c 'K=%k; K=$${K#usbdev};printf bus/usb/%%03i/%%03i $${K%%%%.*} $${K#*.}'", NAME="%c", MODE="0664", GROUP="fingerprint"
SUBSYSTEM=="usb", ACTION=="add", ENV{DEVTYPE}=="usb_device", NAME="bus/usb/$env{BUSNUM}/$env{DEVNUM}", MODE="0664", GROUP="fingerprint"

```

La diferencia entre las reglas de /etc/udev/rules.d/99my.rules y aquellas de /etc/udev/rules.d/udev.rules sólo deberían ser el añadido de MODE="0664", GROUP="fingerprint" o MODE="0660", GROUP="fingerprint" al final de las líneas.

Después de esto tendrá realmente que dar a su usuario permisos de acceso a su propio archivo de huella digital, esto se puede hacer de la manera siguiente:

```
> chown $USERNAME:root /etc/pam_thinkfinger/$USERNAME.bir
> chmod 400 /etc/pam_thinkfinger/$USERNAME.bir
> chmod o+x /etc/pam_thinkfinger

```

Sí, la última establece permisos de ejecución para todo el mundo en un directotio, así que si es usted un super paranoico, podría considerar esto como un fallo de seguridad, queda avisado.

Lo último tiene que ver con xscreensaver. Si inspecciona el archivo xscreensaver verá que tiene el permiso setuid para root:

```
> ls -l /usr/bin/xscreensaver
-rwsr-sr-x 1 root root 217K aoû  2 20:47 /usr/bin/xscreensaver

```

Debido a esto, xscreensaver no será capaz de desbloquearse con el lector de huella digital. Tiene que quitar ese permiso con:

```
> sudo chmod -s /usr/bin/xscreensaver
> ls -l /usr/bin/xscreensaver
-rwxr-xr-x 1 root root 217K aoû  2 20:47 /usr/bin/xscreensaver

```

¡Ya está!

### /etc/pam.d/gdm

[No soy un experto en PAM pero esto funciona, puede que esta sección necesite correcciones]

Edite */etc/pam.d/gdm* como se hace en las secciones 3.1 y 3.2

Añada como primera fila del archivo:

```
auth           sufficient      pam_thinkfinger.so

```

Modifique:

```
auth           required        pam_unix.so ==> auth   		required	pam_unix.so use_first_pass nullok_secure

```

### /etc/pam.d/xdm

Cambie /etc/pam.d/xdm para que se parezca a esto:

```
#%PAM-1.0
auth            sufficient      pam_thinkfinger.so
auth            required        pam_unix.so use_first_pass nullok_secure
auth            required        pam_nologin.so
auth            required        pam_env.so
account         required        pam_unix.so
password        required        pam_unix.so
session         required        pam_unix.so
session         required        pam_limits.so

```

## SLiM

Para que thinkfinger pueda trabajar con el gestor de ingreso SLiM tendrá que activar la capacidad PAM. Consiga el código fuente del paquete slim desde el ABS y cambie la línea de "make" en el PKGBUILD:

```
make USE_PAM=1 || return 1

```

Reconstruya el paquete e instálelo.

Cree entonces un archivo /etc/pam.d/slim

```
#%PAM-1.0
auth            sufficient      pam_thinkfinger.so
auth            requisite       pam_nologin.so
auth            required        pam_env.so
auth            required        pam_unix.so
account         required        pam_unix.so
session         required        pam_limits.so
session         required        pam_unix.so
password        required        pam_unix.so

```

Ahora reinicie slim y haga un suave movimiento circular con su dedo.

## Más información

Vea por favor estas urls para más información.

[http://www.thinkwiki.org/wiki/Talk:How_to_enable_the_fingerprint_reader](http://www.thinkwiki.org/wiki/Talk:How_to_enable_the_fingerprint_reader)

[http://thinkfinger.sourceforge.net/](http://thinkfinger.sourceforge.net/)

[https://bbs.archlinux.org/viewtopic.php?id=36134](https://bbs.archlinux.org/viewtopic.php?id=36134)

[http://www.thinkwiki.org/wiki/How_to_enable_the_fingerprint_reader_with_ThinkFinger](http://www.thinkwiki.org/wiki/How_to_enable_the_fingerprint_reader_with_ThinkFinger)

[http://www.thinkwiki.org/index.php?title=Installing_Ubuntu_6.06_on_a_ThinkPad_T43#Fingerprint_Reader](http://www.thinkwiki.org/index.php?title=Installing_Ubuntu_6.06_on_a_ThinkPad_T43#Fingerprint_Reader)