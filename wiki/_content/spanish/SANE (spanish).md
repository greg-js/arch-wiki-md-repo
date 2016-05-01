Sane proporciona una biblioteca y una herramienta en línea de órdenes para utilizar los escáneres bajo GNU/Linux. [Aquí](http://www.sane-project.org/sane-supported-devices.html) se puede comprobar si sane es compatible con su escáner.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 Para hardware Acer/BenQ](#Para_hardware_Acer.2FBenQ)
    *   [2.2 Para hardware HP](#Para_hardware_HP)
    *   [2.3 Para hardware Brother](#Para_hardware_Brother)
    *   [2.4 Para hardware Epson](#Para_hardware_Epson)
    *   [2.5 Para hardware Samsung](#Para_hardware_Samsung)
    *   [2.6 Para escáneres Plustek](#Para_esc.C3.A1neres_Plustek)
*   [3 Firmware](#Firmware)
*   [4 Instalar un frontend](#Instalar_un_frontend)
*   [5 Escanear en red](#Escanear_en_red)
    *   [5.1 Compartir el escáner en una red](#Compartir_el_esc.C3.A1ner_en_una_red)
    *   [5.2 Configurar xinetd para sane](#Configurar_xinetd_para_sane)
    *   [5.3 Acceder al escáner desde una Workstation remota](#Acceder_al_esc.C3.A1ner_desde_una_Workstation_remota)
*   [6 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [6.1 Invalid argument](#Invalid_argument)
        *   [6.1.1 Falta el archivo firmware](#Falta_el_archivo_firmware)
        *   [6.1.2 Permisos de archivos erróneos para el firmware](#Permisos_de_archivos_err.C3.B3neos_para_el_firmware)
        *   [6.1.3 Múltiples backends reclamando el escáner](#M.C3.BAltiples_backends_reclamando_el_esc.C3.A1ner)
    *   [6.2 Inicio lento](#Inicio_lento)
    *   [6.3 Problemas de permisos](#Problemas_de_permisos)
    *   [6.4 Epson Perfection 1270](#Epson_Perfection_1270)

## Instalación

[Instale](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") [sane](https://www.archlinux.org/packages/?name=sane) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

## Configuración

Ahora puede comprobar si sane reconoce el escáner:

```
$ scanimage -L

```

Si esto no funciona, compruebe que el escáner está conectado al ordenador. También podría ser necesario tener que desconectar/conectar el escáner para que la regla `/etc/udev/rules.d/sane.rules` reconozca su escáner.

Ahora puede ver si funciona realmente:

```
$ scanimage --format=tiff > test.tiff

```

Si el escaneo falla con el mensaje `scanimage: sane_start: Invalid argument`, puede que tenga que especificar el dispositivo:

 `$ scanimage -L` 
```
device `v4l:/dev/video0' is a Noname Video WebCam virtual device
device `pixma:04A91749_247936' is a CANON Canon PIXMA MG5200 multi-function peripheral
```

A continuación, tendrá que ejecutar:

```
$ scanimage --device pixma:04A91749_247936 --format=tiff > test.tiff

```

### Para hardware Acer/BenQ

Si es poseedor de un escáner USB de Acer (ahora BenQ), es necesario descargar un archivo binario de firmware adecuado y configurar `/etc/sane.d/snapscan.conf`.

*   Averigüe cuál es el modelo que posee y tome nota de la ID del USB:

 `$ lsusb`  `Bus 002 Device 010: ID 04a5:20b0 Acer Peripherals Inc. (now BenQ Corp.) S2W 3300U/4300U` 

*   Vaya a la página principal de [snapscan](http://snapscan.sourceforge.net/) y vea si el escáner es compatible y el firmware que necesita (por ejemplo `u176v046.bin`).
*   Busque la imagen del firmware en Internet y descárguelo en `/usr/share/sane/snapscan/`.
*   Edite la cabecera de `/etc/sane.d/snapscan.conf` y configure las dos líneas siguientes:

```
firmware /usr/share/sane/snapscan/u176v046.bin
/dev/usb/scanner0 bus=usb

```

### Para hardware HP

Para el hardware de HP es posible que tenga que instalar [hplip](https://www.archlinux.org/packages/?name=hplip) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)") y/o [hpoj](https://aur.archlinux.org/packages/hpoj/) desde [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)").

*   No se olvide descomentar `hpaio` en el archivo `/etc/sane.d/dll.conf`.
*   Ejecutar `hp-setup`, como root, puede ayudarle a agregar el dispositivo.
*   `hp-plugin` es el 'Plugin HPLIP para Descargar e Instalar Utility'.
*   `hp-scan` es el 'Utilidad HPLIP de Escaneado'.

Para impresoras Hewlett-Packard OfficeJet, PSC, LaserJet, y PhotoSmart y periféricos multifunción, ejecute `ptal-init setup` como usuario root y siga las instrucciones. A continuación ejecute el [demonio](/index.php/Daemons_(Espa%C3%B1ol) "Daemons (Español)") **ptal-init**.

### Para hardware Brother

Con el fin de instalar un Escáner Brother o una Impresora/Escáner Combo se necesita el controlador adecuado (que se puede encontrar en AUR). Solo hay cuatro controladores a elegir (brscan1-4). Con el fin de encontrar el más adecuado debe buscar su modelo en la página [brother linux scanner](http://welcome.solutions.brother.com/bsc/public_s/id/linux/en/download_scn.html).

Después de instalar el controlador necesita ejecutar:

```
# /usr/local/Brother/sane/setupSaneScan1 -i

```

para que los controladores/escáner sean reconocidos por sane.

Para escáneres de red, Brother ofrece una herramienta de configuración:

```
# brsaneconfig2 -a name=<ScannerName> model=<ScannerModel> ip=<ScannerIP>

```

Ejemplo:

```
# brsaneconfig2 -a name=SCANNER_DCP770CW model=DCP-770CW ip=192.168.0.110

```

### Para hardware Epson

Para instalar escáneres epson via Wi-Fi y/o red, puede usar «*Image Scan* para Linux».

Instale [iscan](https://www.archlinux.org/packages/?name=iscan) y [iscan-plugin-network](https://aur.archlinux.org/packages/iscan-plugin-network/) desde [AUR](/index.php/AUR "AUR"), actualizando `/etc/sane.d/epkowa.conf` con la adición de la línea:

```
net {IP_OF_SCANNER}

```

### Para hardware Samsung

En algunas impresoras Samsung MFP puede que tenga que modificar el archivo `/etc/sane.d/xerox_mfp.conf`.

Ejemplo de entrada:

```
#Samsung SCX-3200
usb 0x04e8 0x3441

```

Cambie el modelo de impresora según su caso. Puede obtener el código ipVendor y idProduct con `lsusb`. Consulte [este hilo](https://bbs.archlinux.org/viewtopic.php?id=123934).

### Para escáneres Plustek

Algunos escáneres plustek (especialmente los Canoscan), requieren un directorio de bloqueo. Asegúrese de que el directorio /var/lock/sane existe, que los permisos son 660, y que es propiedad de <user>:scanner. Si los permisos del directorio son distintos, solo será capaz de utilizar el escáner como usuario root. Parece que (al menos en x86-64) algunos programas que utilizan libusb (sobretodo xsane y kooka) el grupo scanner también necesita permisos rw para acceder a /proc/bus/usb y poder funcionar con un usuario normal.

## Firmware

**Nota:** Esta sección solo es necesaria seguirla si requiere cargar el firmware de su escáner.

Los firmware suelen tener el extensión **`.bin`**.

En primer lugar, se necesita poner el firmware en algún lugar seguro, se recomienda ponerlo en el subdirectorio `/usr/share/sane`.

Luego hay que decirle a sane cuál es el firmware:

*   Busque el nombre del backend para el escáner en la [lista de dispositivos compatibles con sane](http://www.sane-project.org/sane-supported-devices.html).
*   Abra el archivo `/etc/sane.d/<nombre-del-backend>.conf`.
*   Asegúrese de que la entrada del firmware está descomentada y ponga en la fila de puntos la ruta donde se encuentra el archivo de firmware para su escáner. Asegúrese de que los miembros del grupo `scanner` pueden tener acceso al archivo `/etc/sane.d/<nombre-del-backend>.conf`.

Si el backend de su escáner no es parte del paquete sane (como, por ejemplo, hpaio.conf que forma parte de hplip), es necesario comentar la entrada correspondiente en /etc/sane.d/dll.d/hplip.

## Instalar un frontend

XSane proporciona una interfaz basada en GTK para Sane. Puede [instalarlo](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") con el paquete [xsane](https://www.archlinux.org/packages/?name=xsane), disponible en los [repositorios oficiales](/index.php/Official_repositories "Official repositories").

**Nota:** Xsane puede guardar lo escaneado directamente en formato .pdf. ¡Esto solo funciona en el modo de 8 bits de profundidad de color! (el modo de 16 bits produce [archivos dañados](https://bugs.launchpad.net/ubuntu/+source/xsane/+bug/539162)).

Existen otras interfaces, que puede encontrarlas como sigue:

*   Use `pacman -Ss` para buscar palabras clave como «sane» o «scanner».
*   Consulte la [lista de frontends](http://www.sane-project.org/sane-frontends.html) en la página web del proyecto sane.

## Escanear en red

#### Compartir el escáner en una red

Puede compartir el escáner con otros hosts de la red que usan sane , xsane o Gimp con xsane habilitado. Para configurar el servidor, en primer lugar indique que los hosts de la red tienen permitido el acceso al escáner.

Modifique el archivo `/etc/sane.d/saned.conf` según su caso, por ejemplo:

```
# requerido
localhost
# permitir subred local
192.168.0.0/24

```

Inserte el módulo `nf_conntrack_sane` de iptables para permitir el seguimiento del firewall de las conexiones de saned.

Las solicitudes de escaneo son manejadas por saned. Esto se puede ejecutar como un demonio con `saned -a` o ejecutar cuando sea necesario por xinetd.

#### Configurar xinetd para sane

[Instale](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") [xinetd](https://www.archlinux.org/packages/?name=xinetd) desde los [repositorios oficiales](/index.php/Official_repositories "Official repositories").

A continuación, asegúrese que el archivo llamado `/etc/xinetd.d/sane` existe y ajuste la opción desactivar (*«disable»*) a no:

```
service sane-port
{
   port        = 6566
   socket_type = stream
   wait        = no
   user        = root
   group       = scanner
   server      = /usr/sbin/saned
   disable     = no
}

```

El usuario llamado ('nobody' en el archivo incluido en el paquete sane) debe normalmente ser miembro del grupo scanner para tener permisos de acceso al escáner::

```
# usermod -a -G scanner nobody

```

Para algunas HP combinadas escáner-impresoras el usuario, en cambio, debe ser miembro del grupo lp, para que también pueda usar el escáner en el archivo de servicio.

Agregue la línea siguiente a `/etc/services`, si no está ya presente:

```
sane-port 6566/tcp

```

Inicie el [demonio](/index.php/Daemon_(Espa%C3%B1ol)#Iniciar_manualmente "Daemon (Español)") **xinetd**.

Ahora el escáner puede ser utilizado por otras estaciones de trabajo, a través de su red de área local.

#### Acceder al escáner desde una Workstation remota

Puede acceder al escáner de red habilitada desde una estación de trabajo remota de Arch Linux.

Para configurar la estación de trabajo, comience [instalando](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") [xsane](https://www.archlinux.org/packages/?name=xsane) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

A continuación, especifique el nombre del servidor host o la dirección IP en el archivo `/etc/sane.d/net.conf`:

```
# dirección IP estática
192.168.0.1
# o nombre de host
stratus

```

Ahora pruebe la conexión de su estación de trabajo, a partir de un inicio de sesión de usuario no root:

```
$ xsane

```

o

```
$ scanimage -L

```

Después de un breve tiempo, xsane ha debido encontrar el escáner remoto y le presentará las ventanas habituales, listos para el escaneado en red.

Para una impresora HP todo-en-uno (impresora/escáner/fax) la red necesitará configurarla a través de:

```
$ hp-setup <ip de la impresora>

```

## Solución de problemas

### Invalid argument

Si se recibe el mensaje de error *«Invalid argument»* con xsane u otro front-end de sane, podría ser causado por una de las siguientes razones:

#### Falta el archivo firmware

No existe el archivo de firmware proveido para el escáner utilizado (vea más arriba).

#### Permisos de archivos erróneos para el firmware

Los permisos para el archivo de firmware utilizado son erróneos. Corríjalo utilizando:

```
# chown root:scanner /usr/share/sane/SCANNER_MODEL/FIRMWARE_FILE
# chmod ug+r /usr/share/sane/SCANNER_MODEL/FIRMWARE_FILE

```

#### Múltiples backends reclamando el escáner

Puede suceder que múltiples backends apoyen (o pretendan apoyar) al escáner, y sane elija uno que, a la postre, no le proporciona soporte (en ese caso, el escáner no se mostrará al escribir scanimage -L). Esto ha sido reportado sobre todo con escáneres Epson y los backends `epson2` resp. `epson`. En este supuesto, la solución es comentar el backend no deseado en el archivo `/etc/sane.d/dll.conf`. En el caso de Epson, sería cambiar:

```
epson2
#epson

```

a

```
#epson2
epson

```

### Inicio lento

Si se encuentra con problemas de inicio lento (por ejemplo, `xsane` o `scanimage -L` tarda mucho en encontrar el escáner) es posible que exista más de un controlador disponible.

Eche un vistazo al archivo `/etc/sane.d/dll.conf` y pruebe comentando una de las entradas (por ejemplo, si tiene epson, epson2 y epkowa activados al mismo tiempo, trate de dejar solo epson o epkowa sin comentarios).

### Problemas de permisos

Si se muestra el escáner solo cuando se hace `sudo lsusb`, podría hacerlo funcionar como usuario normal añadiendo su usuario al grupo `scanne` y/o `lp`.

```
# gpasswd -a username scanner
# gpasswd -a username lp

```

Esta solución se reportó para hacer funcionar una HP modelos todo-en-uno (por ejemplo, PSC 1315 y PSC 2355).

También se puede probar a cambiar el permiso del dispositivo usb, pero esto no es recomendable; una mejor solución es corregir las reglas udev para que el escáner sea reconocido.

Ejemplo:

En primer lugar, acceda como root y compruebe los dispositivos USB conectados con la orden `lsusb`:

```
#Bus 006 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
#Bus 005 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
#Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
#Bus 003 Device 003: ID 04d9:1603 Holtek Semiconductor, Inc. 
#Bus 003 Device 002: ID 04fc:0538 Sunplus Technology Co., Ltd 
#Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
#Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
#Bus 001 Device 006: ID 03f0:2504 Hewlett-Packard 
#Bus 001 Device 002: ID 046d:0802 Logitech, Inc. Webcam C200
#Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

En nuestro ejemplo, vemos el escáner - '**Bus 001 Device 006: ID 03f0:2504 Hewlett-Packard'**

Ahora, edite el archivo `/lib/udev/rules.d/53-sane.rules` y busque la primera parte del ID encontrado anteriormente y compruebe también si hay una línea que informe de la segunda parte del número (número del modelo), en este ejemplo 2504\. Si no se encuentra, cambie y copie la línea de abajo y escriba el idVendor y el idProduct de su escáner, en este ejemplo sería:

```
# Hewlett-Packard ScanJet 4100C
ATTRS{idVendor}=="03f0", ATTRS{idProduct}=="2504", MODE="0664", GROUP="scanner",
 ENV{libsane_matched}="yes"

```

Guarde el archivo, desconecte y conecte de nuevo el scanner, y los permisos del archivo deberían estar en orden.

Otro consejo sería agregar su dispositivo (escáner) en el archivo backend:

En el ejemplo seguido, añadimos la cadena '**usb 0x03f0 0x2504'** en el archivo `/etc/sane.d/hp4200.conf`, que se vería así:

```
#
# Configuration file for the hp4200 backend
#
#
# HP4200
#usb 0x03f0 0x0105
usb 0x03f0 0x2504

```

### Epson Perfection 1270

Para Epson Perfection 1270, también necesita un firmware llamado esfw3e.bin. Se puede obtener instalando el controlador de Windows.

Modifique el archivo de configuración de backend snapscan, `/etc/sane.d/snapscan.conf`. Cambie la ruta del firmware por la suya:

```
# Change to the fully qualified filename of your firmware file, if
# firmware upload is needed by the scanner
firmware /mnt/mydata/Backups/firmware/esfw3e.bin

```

Y añada la siguiente línea al final o cualquier otro lugar:

```
# Epson Perfection 1270
usb 0x04b8 0x0120

```

Puede obtener información de dicho código (*usb 0x04b8 0x0120*) con la orden «sane-find-scanner».

También agregue estas líneas en el archivo `/etc/hotplug/usb/libsane.usermap` para configurar sus privilegios, de este modo:

```
#Epson Perfection 1270
libusbscanner 0x0003 0x04b8 0x0120 0x0000 0x0000 0x00 0x00 0x00 0x00 0x00 0x00 0x00000000

```

Vuelva a reconectar el escáner y ahora debería funcionar su Epson Perfection 1270.

NOTA: Se puede escanear la imagen si se definen los valores de X e Y, pero se obtiene el error: *"scanimage: sane_start: Error during device I/O"*, si alguien tiene una solución, por favor, complete la sección.

*   Para evitar «scanimage: sane_start: Error during device I/O» y que se cuelgue el propio escáner, cuando se intanta escanear con ADF (alimentador automático de documentos) activado, tuve que quitar o comentar todos los Backends de `/etc/sane.d/dll.conf` y añadir, en su lugar, lo siguiente al archivo:

```
snapscan

```

Por último. Si sigue apareciendo el mensaje «Error I/O» pruebe comprobando el bloqueo de transporte del escáner. Está en la parte inferior del escáner. Tiene que ser abierta.