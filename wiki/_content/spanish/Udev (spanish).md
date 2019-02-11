`udev` reemplaza la funcionalidad de `hotplug` y `hwdetect`.

Del [artículo de Wikipedia](https://en.wikipedia.org/wiki/Udev "wikipedia:Udev"):

	*«Udev es el gestor de dispositivos que usa el kernel de Linux. Principalmente, su función es controlar los archivos de dispositivo en `/dev`. Es el sucesor de devfs y de hotplug, lo que significa que maneja el directorio `/dev` y todas las acciones del espacio de usuario al agregar o quitar dispositivos, incluyendo la carga de firmware»*.

Udev carga los módulos del kernel en paralelo (simultáneamente) para proveer una potencial ventaja de rendimiento, en vez de cargar los módulos secuencialmente (uno después de otro). Los módulos son, por lo tanto, cargados asíncronamente. La desventaja inherente de este método es que udev no siempre carga los módulos en el mismo orden en cada arranque del sistema. Si la máquina posee múltiples dispositivos de bloque, esto se puede manifestar en que los nodos de los dispositivos cambian su designación aleatoriamente. Por ejemplo, si la máquina tiene dos discos duros, `/dev/sda` puede convertirse aleatoriamente en `/dev/sdb`. Continue leyendo más abajo para mayor información.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Acerca de las reglas udev](#Acerca_de_las_reglas_udev)
    *   [2.1 Escribir reglas udev](#Escribir_reglas_udev)
    *   [2.2 Listar los atributos de un dispositivo](#Listar_los_atributos_de_un_dispositivo)
    *   [2.3 Comprobar las reglas antes de cargarlas](#Comprobar_las_reglas_antes_de_cargarlas)
    *   [2.4 Cargar reglas nuevas](#Cargar_reglas_nuevas)
*   [3 Udisks](#Udisks)
    *   [3.1 Montaje automático de wrappers de udisks](#Montaje_automático_de_wrappers_de_udisks)
    *   [3.2 Funciones de la shell de udisks](#Funciones_de_la_shell_de_udisks)
    *   [3.3 udisks2 - montar en /media](#udisks2_-_montar_en_/media)
*   [4 Consejos y Trucos](#Consejos_y_Trucos)
    *   [4.1 Acceder a programadores de firmware y a dispositivos USB de comunicación virtual](#Acceder_a_programadores_de_firmware_y_a_dispositivos_USB_de_comunicación_virtual)
    *   [4.2 Ejecutar USB al insertar](#Ejecutar_USB_al_insertar)
    *   [4.3 Detectar nuevas unidades eSATA](#Detectar_nuevas_unidades_eSATA)
    *   [4.4 Marca como interna tanto SATA-Ports como eSATA-Ports](#Marca_como_interna_tanto_SATA-Ports_como_eSATA-Ports)
    *   [4.5 Configurar nombres estáticos para los dispositivos](#Configurar_nombres_estáticos_para_los_dispositivos)
        *   [4.5.1 Dispositivo iscsi](#Dispositivo_iscsi)
        *   [4.5.2 Dispositivos de vídeo](#Dispositivos_de_vídeo)
        *   [4.5.3 Impresoras](#Impresoras)
    *   [4.6 Despertar desde la suspención con un dispositivo USB](#Despertar_desde_la_suspención_con_un_dispositivo_USB)
*   [5 Solución de problemas](#Solución_de_problemas)
    *   [5.1 Blacklisting de Módulos](#Blacklisting_de_Módulos)
    *   [5.2 udevd falla al inicio](#udevd_falla_al_inicio)
    *   [5.3 Problemas conocidos con el Hardware](#Problemas_conocidos_con_el_Hardware)
        *   [5.3.1 Dispositivos BusLogic dejan de funcionar y causan bloqueos durante el arranque](#Dispositivos_BusLogic_dejan_de_funcionar_y_causan_bloqueos_durante_el_arranque)
        *   [5.3.2 Dispositivos extraibles no son reconocidos como tales](#Dispositivos_extraibles_no_son_reconocidos_como_tales)
    *   [5.4 Problemas conocidos con la carga automática](#Problemas_conocidos_con_la_carga_automática)
        *   [5.4.1 Problemas de sonido con algunos módulos no cargados automáticamente](#Problemas_de_sonido_con_algunos_módulos_no_cargados_automáticamente)
    *   [5.5 Problemas conocidos para usuarios con Kernel personalizado](#Problemas_conocidos_para_usuarios_con_Kernel_personalizado)
        *   [5.5.1 Udev no se ejecuta](#Udev_no_se_ejecuta)
    *   [5.6 Dispositivos IDE CD/DVD](#Dispositivos_IDE_CD/DVD)
    *   [5.7 Dispositivos ópticos con ID de grupo ajustado a «disk»](#Dispositivos_ópticos_con_ID_de_grupo_ajustado_a_«disk»)
*   [6 Véase también](#Véase_también)

## Instalación

Udev es ahora parte de [systemd](https://www.archlinux.org/packages/?name=systemd) y es instalado de forma predeterminada en los sistemas Arch Linux.

## Acerca de las reglas udev

Las reglas de udev escritas por el administrador del sistema se encuentran en el directorio `/etc/udev/rules.d/`, y el nombre del archivo terminado con la extensión `.rules`. Las reglas proporcionadas por la instalación de diversos paquetes se encuentran en `/usr/lib/udev/rules.d/`. En el caso de que existan dos reglas con el mismo nombre en `/usr/lib` y en `/etc`, la norma que se encuentra en la carpeta `/etc` tendrá prioridad.

### Escribir reglas udev

*   Para aprender a escribir las reglas de udev, consulte: [Escribir reglas udev](http://www.reactivated.net/writing_udev_rules.html)
*   Para ver un ejemplo de regla udev, consulte: [Regla udev mejorada para Arch Linux](https://soosck.wordpress.com/2011/01/19/improved-udev-rule-arch-linux/).

Este es un ejemplo de una regla que coloca un enlace simbólico /dev/video-cam1 cuando una cámara web está conectada. En primer lugar, hemos averiguado que dicha cámara se conecta y se carga como el dispositivo /dev/video2\. La razón para escribir esta regla es que en el siguiente arranque el dispositivo bien podría aparecer bajo otro nombre, como por ejemplo /dev/video0.

 `# udevadm info -a -p $(udevadm info -q path -n /dev/video2)` 
```
Udevadm info starts with the device specified by the devpath and then
walks up the chain of parent devices. It prints for every device
found, all possible attributes in the udev rules key format.
A rule to match, can be composed by the attributes of the device
and the attributes from one single parent device.

  looking at device '/devices/pci0000:00/0000:00:04.1/usb3/3-2/3-2:1.0/video4linux/video2':
    KERNEL=="video2"
    SUBSYSTEM=="video4linux"
    ...
  looking at parent device '/devices/pci0000:00/0000:00:04.1/usb3/3-2/3-2:1.0':
    KERNELS=="3-2:1.0"
    SUBSYSTEMS=="usb"
    ...
  looking at parent device '/devices/pci0000:00/0000:00:04.1/usb3/3-2':
    KERNELS=="3-2"
    SUBSYSTEMS=="usb"
    ...
    ATTRS{idVendor}=="05a9"
    ...
    ATTRS{manufacturer}=="OmniVision Technologies, Inc."
    ATTRS{removable}=="unknown"
    ATTRS{idProduct}=="4519"
    ATTRS{bDeviceClass}=="00"
    ATTRS{product}=="USB Camera"
    ...

```

Desde el dipositivo video4linux usamos `KERNEL=="video2"` y `SUBSYSTEM=="video4linux"`, entoces hacemos que coincida con la webcam del usb principal usando los ID del proveedor y del producto `SUBSYSTEMS=="usb"`, `ATTRS{idVendor}=="05a9"` y `ATTRS{idProduct}=="4519"`.

 `/etc/udev/rules.d/83-webcam.rules` 
```
KERNEL=="video[0-9]*", SUBSYSTEM=="video4linux", SUBSYSTEMS=="usb", \
        ATTRS{idVendor}=="05a9", ATTRS{idProduct}=="4519", SYMLINK+="video-cam1"

```

En el ejemplo anterior hemos creado un enlace simbólico con `SYMLINK+="video-cam1"`, pero podemos configurar fácilmente el usuario `OWNER="john"` o el grupo usando `GROUP="video"`, o ajustando los permisos mediante `MODE="0660"`

Sin embargo, si tiene la intención de escribir una regla para que actúe cuando se remueve dispositivo, tenga en cuenta que los atributos del dispositivos pueden no estar accesibles. En este caso, tendrá que trabajar con las variables del entorno predeterminadas del dispositivo. Para controlar las variables del entorno, ejecute la orden siguiente al desenchufar el dispositivo:

```
# udevadm monitor --environment --udev

```

En la salida de esta orden, verá pares de valores tales como ID_VENDOR_ID and ID_MODEL_ID, que se corresponden a los atributos utilizados anteriormente "idVendor" y "idProduct". Una regla que utilice variables de entorno del dispositivo puede tener este aspecto:

 `/etc/udev/rules.d/83-webcam-removed.rules` 
```
ACTION=="remove", SUBSYSTEM=="usb", \
        ENV{ID_VENDOR_ID}=="05a9", ENV{ID_MODEL_ID}=="4519", RUN+="/path/to/your/script"
```

### Listar los atributos de un dispositivo

Para obtener una lista de todos los atributos de un dispositivo que podemos utilizar para escribir reglas, ejecutaremos esta orden:

```
# udevadm info -a -n [device name]

```

Sustituya `[device name]` con el dispositivo presente en el sistema, como `/dev/sda` o `/dev/ttyUSB0`.

Si no sabemos el nombre del dispositivo, también podemos listar todos los atributos de una ruta específica del sistema:

```
# udevadm info -a -p /sys/class/backlight/acpi_video0

```

### Comprobar las reglas antes de cargarlas

```
# udevadm test $(udevadm info -q path -n [device name]) 2>&1

```

This will not perform all actions in your new rules but it will however process symlink rules on existing devices which might come in handy if you are unable to load them otherwise. You can also directly provide the path to the device you want to test the udev rule for:

```
# udevadm test /sys/class/backlight/acpi_video0/

```

### Cargar reglas nuevas

Udev detecta automáticamente cambios en los archivos de reglas, por lo que los cambios surtan efecto inmediatamente sin necesidad de reiniciar udev. Sin embargo, las reglas no se recargan automáticamente en aquellos dispositivos que están en funcionamiento. Los dispositivos que se ponen en funcionamiento al conectarse, como los dispositivos USB, si ya estaban conectados, probablemente tendrán que volver a conectarse para que la nueva regla entre en vigor, o, al menos, recargar los módulos del kernel ohci-hcd y ehci-hcd y, por lo tanto, volver a cargar todos los controladores USB.

Si las reglas no pueden cargarse de manera automática:

```
# udevadm control --reload-rules

```

Podemos forzar manualmente a udev a activar sus reglas con:

```
# udevadm trigger

```

## Udisks

Si desea montar unidades extraíbles no haga una llamada a 'mount' en la regla udev. En el caso de sistemas de archivos fuse (por ejemplo, ntfs-3g) obtendrá el error "Transport endpoint not connected". En su lugar utilice udisks que maneja el montaje automático correctamente.

Hay dos versiones incompatibles, udisks y udisks2, una reescritura de udisks que rompe la compatibilidad. Dependiendo de nuestro DE, uno u otra versión será necesaria (la cual ya vendrá instalada como una dependencia):

*   Para [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)") o [KDE](/index.php/KDE "KDE") 4.10+, instale [udisks2](https://www.archlinux.org/packages/?name=udisks2)
*   Para [Xfce](/index.php/Xfce "Xfce"), instale [udisks](https://aur.archlinux.org/packages/udisks/)

No hay necesidad de cualquier regla adicional. Como elemento adicional, se puede eliminar HAL si se está utilizando solo para fines de montaje automático.

### Montaje automático de wrappers de udisks

Los soportes de udisks (*«udisks wrapper»*) tienen la ventaja de ser muy fácil de instalar y sin necesidad de configuración (o mínima). Con wrapper se montarán automáticamente elementos como CDs y memorias flash.

*   [udevil](http://ignorantguru.github.com/udevil/) - [udevil](https://www.archlinux.org/packages/?name=udevil) *«Monta y desmonta dispositivos extraíbles sin necesidad de una contraseña, muestra información del dispositivo, y monitorea los cambios de los dispositivos»*. Está escrito en C y puede sustituir a udisks e incluye [devmon](http://igurublog.wordpress.com/downloads/script-devmon/), que se puede instalar por separado desde AUR ([devmon](https://aur.archlinux.org/packages/devmon/)). También puede iniciar aplicaciones automáticamente de forma selectiva o ejecutar órdenes después del montaje, hacer caso omiso de dispositivos especificados y volúmenes etiquetados, y desmontar las unidades extraíbles.
*   [ldm](https://aur.archlinux.org/packages/ldm/) - Un demonio ligero que monta automáticamente unidades usb, cd, dvd o floppys. [[1]](https://bbs.archlinux.org/viewtopic.php?id=125918)
*   [udiskie](/index.php/Udiskie "Udiskie") - Escrito en Python. Permite el montaje y desmontaje automático por otros usuarios.
*   [udisksevt](https://aur.archlinux.org/packages/udisksevt/) - Escrito en Haskell. Permite el montaje automático por cualquier usuario. Diseñado para ser integrado con [traydevice](https://aur.archlinux.org/packages/traydevice/).
*   [udisksvm](https://aur.archlinux.org/packages/udisksvm/) - Una GUI de UDisks wrapper que utiliza la interfaz dbus udisks2\. Llama al script 'traydvm' , incluido en el paquete. El utilidad GUI 'traydvm' es un script que muestra un icono de la bandeja del sistema para un dispositivo conectado, proporcionando un menú con el botón derecho del ratón para realizar acciones simples sobre el dispositivo. Así, se puede desactivar la función de montaje automático; esta herramienta debe trabajar con otras herramientas de montaje automático, para mostrar los iconos de la bandeja del sistema. Es independiente de cualquier administrador de archivos.

*   Se pueden montar automáticamente y expulsar dispositivos extraíbles con la combinación de [pmount](https://aur.archlinux.org/packages/pmount/), [udisks2](https://www.archlinux.org/packages/?name=udisks2) y [spacefm](https://aur.archlinux.org/packages/spacefm/). Tenga en cuenta que ha de ejecutar spacefm en modo demonio con `spacefm -d &` en los scripts de inicio, `~/.xinitrc` o `~/.xsession`, para obtener el montaje automático . También puede montar los discos internos agregándolos a `/etc/pmount.allow`.

### Funciones de la shell de udisks

Mientras udisks incluye un método simple de montaje (y desmontaje) de los dispositivos a través de la línea de órdenes, puede ser, sin embargo, tedioso tener que escribir las órdenes una y otra vez. Estas funciones de la shell que se enumeran a continuación, generalmente, sirven para acortar y facilitar el uso de la línea de órdenes.

*   [udisks_functions](https://bbs.archlinux.org/viewtopic.php?id=109307) - Escrito para Bash.
*   [bashmount](https://bbs.archlinux.org/viewtopic.php?id=117674) - [bashmount](https://aur.archlinux.org/packages/bashmount/) es un script bash estructurado a modo de menú, articulado como un simple archivo de configuración que hace que sea fácil de redactar e implementar.

### udisks2 - montar en /media

Por defecto, udisks2 monta unidades extraibles en `/run/media/$USER/`, en lugar de `/media/`. Si no le gusta este comportamiento, utilice esta regla:

 `/etc/udev/rules.d/99-udisks2.rules` 
```
ENV{ID_FS_USAGE}=="filesystem|other|crypto", ENV{UDISKS_FILESYSTEM_SHARED}="1"

```

## Consejos y Trucos

### Acceder a programadores de firmware y a dispositivos USB de comunicación virtual

El siguiente conjunto de reglas permite a los usuarios normales (en el grupo «users») acceder al programador USB [USBtinyISP](http://www.ladyada.net/make/usbtinyisp/) para microcontroladores AVR y al USB genérico (SiLabs [CP2102](http://www.silabs.com/products/interface/usbtouart)) para el adaptador UART y para el programador [Atmel AVR Dragon](http://www.atmel.com/tools/AVRDRAGON.aspx?tab=overview) y [Atmel AVR ISP mkII](http://www.atmel.com/tools/AVRISPMKII.aspx) . Ajuste los permiso de acuerdo al caso. Verificado al 31-10-2012.

 `/etc/udev/rules.d/50-embedded_devices.rules` 
```
# USBtinyISP Programmer rules
SUBSYSTEMS=="usb", ATTRS{idVendor}=="1781", ATTRS{idProduct}=="0c9f", GROUP="users", MODE="0666"
SUBSYSTEMS=="usb", ATTRS{idVendor}=="16c0", ATTRS{idProduct}=="0479", GROUP="users", MODE="0666"
# USBasp Programmer rules http://www.fischl.de/usbasp/
SUBSYSTEMS=="usb", ATTRS{idVendor}=="16c0", ATTRS{idProduct}=="05dc", GROUP="users", MODE="0666"

# Mdfly.com Generic (SiLabs CP2102) 3.3v/5v USB VComm adapter
SUBSYSTEMS=="usb", ATTRS{idVendor}=="10c4", ATTRS{idProduct}=="ea60", GROUP="users", MODE="0666"

#Atmel AVR Dragon (dragon_isp) rules
SUBSYSTEM=="usb", ATTRS{idVendor}=="03eb", ATTRS{idProduct}=="2107", GROUP="users", MODE="0666"

#Atmel AVR JTAGICEMKII rules
SUBSYSTEM=="usb", ATTRS{idVendor}=="03eb", ATTRS{idProduct}=="2103", GROUP="users", MODE="0666"

#Atmel Corp. AVR ISP mkII
SUBSYSTEM=="usb", ATTRS{idVendor}=="03eb", ATTRS{idProduct}=="2104", GROUP="users", MODE="0666"

```

### Ejecutar USB al insertar

Consulte el artículo [Execute on USB insert](/index.php/Execute_on_USB_insert "Execute on USB insert") o [devmon wrapper script](http://igurublog.wordpress.com/downloads/script-devmon/).

### Detectar nuevas unidades eSATA

Si la unidad eSATA no se detecta cuando se conecte, podemos intertar algunas cosas. Por ejemplo reiniciar con la unidad eSATA enchufada, o bien podría intentar lo siguente:

```
# echo 0 0 0 | tee /sys/class/scsi_host/host*/scan

```

O puede instalar scsiadd (disponible en AUR) y probar esto:

```
# scsiadd -s

```

Esperaremos para comprobar que la unidad se encuentra ahora en /dev. Si esto no funciona, podríamos probar con las órdenes anteriores mientras se ejecuta:

```
# udevadm monitor

```

para ver qué está sucediendo realmente.

### Marca como interna tanto SATA-Ports como eSATA-Ports

Si ha conectado un puerto eSATA u otro adaptador eSATA, el sistema todavía reconocerá este puerto como un disco duro SATA interno. GNOME y KDE le preguntará por su contraseña de root todo el tiempo. La siguiente regla marcará el SATA-Port especificado como un eSATA-Port externo. Con esto, un usuario normal de GNOME pueden conectar sus unidades de disco eSATA al puerto como una unidad USB, sin ningún tipo de contraseña de root y así sucesivamente.

 `/etc/udev/rules.d/10-esata.rules` 
```
DEVPATH=="/devices/pci0000:00/0000:00:1f.2/host4/*", ENV{UDISKS_SYSTEM}="0"

```

**Nota:** el DEVPATH (ruta del dispositivo) se puede encontrar después de la conexión de la unidad de disco eSATA con la siguiente orden (sustituya sdb según su caso):
```
# udevadm info -q path -n /dev/sdb
/devices/pci0000:00/0000:00:1f.2/host4/target4:0:0/4:0:0:0/block/sdb

```

```
# find /sys/devices/ -name sdb
/sys/devices/pci0000:00/0000:00:1f.2/host4/target4:0:0/4:0:0:0/block/sdb

```

### Configurar nombres estáticos para los dispositivos

Debido a que udev carga todos los módulos de forma asíncrona, se pueden inicializar en un orden diferente en cada arranque. Esto puede dar como resultado dispositivos con nombres cambiados aleatoriamente. Udev permite crear reglas donde se utilicen nombres estáticos para los dispositivo:

*   Véase [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") para dispositivos de bloque.
*   Véase [Network configuration#Device names](/index.php/Network_configuration#Device_names "Network configuration") para dispositivos de red.

#### Dispositivo iscsi

Compruebe la salida de scsi_id:

```
/usr/lib/udev/scsi_id --whitelisted --replace-whitespace --device=/dev/sdb
3600601607db11e0013ab5a8e371ce111

```
 `/etc/udev/rules.d/75-iscsi.rules` 
```
#The iscsi device rules.
#This will create an iscsi device for each of the targets.
KERNEL=="sd*", SUBSYSTEM=="block", \
     PROGRAM="/usr/lib/udev/scsi_id --whitelisted --replace-whitespace /dev/$name", \ RESULT=="3600601607db11e0013ab5a8e371ce111", \
     NAME="isda"
```

#### Dispositivos de vídeo

Para configurar la cámara web, en primer lugar, consulte [Webcam configuration](/index.php/Webcam_setup#Webcam_configuration "Webcam setup").

Si utilizamos múltiples cámaras web, útil por ejemplo con [motion](https://aur.archlinux.org/packages/motion/) (software detector de movimiento que toma imágenes de los dispositivos video4linux y/o de webcams), asignará los dispositivos de vídeo como /dev/video0..n al azar en el arranque. La solución recomendada es crear enlaces simbólicos que utilicen una regla udev (como en el ejemplo de la [sección anterior](#Escribir_reglas_udev)).

 `/etc/udev/rules.d/83-webcam.rules` 
```
KERNEL=="video[0-9]*", SUBSYSTEM=="video4linux", SUBSYSTEMS=="usb", ATTRS{idVendor}=="05a9", ATTRS{idProduct}=="4519", SYMLINK+="video-cam1"
KERNEL=="video[0-9]*", SUBSYSTEM=="video4linux", SUBSYSTEMS=="usb", ATTRS{idVendor}=="046d", ATTRS{idProduct}=="08f6", SYMLINK+="video-cam2"
KERNEL=="video[0-9]*", SUBSYSTEM=="video4linux", SUBSYSTEMS=="usb", ATTRS{idVendor}=="046d", ATTRS{idProduct}=="0840", SYMLINK+="video-cam3"

```

**Nota:** El uso de otros nombres distintos de "/dev/video*" se romperá con la precarga de v4l1compat.so y, quizás, v4l2convert.so.

#### Impresoras

Si utiliza varias impresoras, los dispositivos `/dev/lp[0-9]` serán asignados al azar en el arranque, que rompera, por ejemplo, la configuración de [CUPS](/index.php/CUPS_(Espa%C3%B1ol) "CUPS (Español)").

Puede crear la siguiente regla, que creará enlaces simbólicos en `/dev/lp/by-id` y `/dev/lp/by-path`, similar al esquema [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming"):

 `/etc/udev/rules.d/60-persistent-printer.rules` 
```
ACTION=="remove", GOTO="persistent_printer_end"

# This should not be necessary
#KERNEL!="lp*", GOTO="persistent_printer_end"

SUBSYSTEMS=="usb", IMPORT{builtin}="usb_id"
ENV{ID_TYPE}!="printer", GOTO="persistent_printer_end"

ENV{ID_SERIAL}=="?*", SYMLINK+="lp/by-id/$env{ID_BUS}-$env{ID_SERIAL}"

IMPORT{builtin}="path_id"
ENV{ID_PATH}=="?*", SYMLINK+="lp/by-path/$env{ID_PATH}"

LABEL="persistent_printer_end"

```

### Despertar desde la suspención con un dispositivo USB

En primer lugar, encuentre el ID del proveedor y del producto del dispositivo, por ejemplo:

 `# lsusb | grep Logitech`  `Bus 007 Device 002: ID 046d:c52b Logitech, Inc. Unifying Receiver` 

Ahora cambie el atributo `power/wakeup` del dispositivo y del controlador USB al que está conectado, que en este caso es `driver/usb7/power/wakeup`. Utilice la siguiente regla:

 `/etc/udev/rules.d/50-wake-on-device.rules` 
```
ACTION=="add", SUBSYSTEM=="usb", ATTRS{idVendor}=="046d", ATTRS{idProduct}=="c52b", ATTR{power/wakeup}="enabled", ATTR{driver/usb7/power/wakeup}="enabled"

```

**Nota:** Asegúrese también que el controlador del USB esté activado en `/proc/acpi/wakeup`.

## Solución de problemas

### Blacklisting de Módulos

En casos extraños, udev puede cometer un error y cargar los módulos incorrectos. Para prevenir este comportamiento, se pueden introducir los módulos afectados en lista negra (*«blacklist»*). Udev nunca cargará los módulos que estén listados (*«blacklisted»*). Consulte [Blacklisting](/index.php/Kernel_modules_(Espa%C3%B1ol)#Blacklisting "Kernel modules (Español)"). Ni al momento del arranque del sistema ni después cuando se produce un evento de conexión sobre la marcha es recibido (por ejemplo, conectando una unidad flash USB).

### udevd falla al inicio

Después de migrar a LDAP o actulizar el sistema con LDAP-backed, udevd puede colgarse en el arranque apareciendo el mensaje «Starting UDev Daemon». Esto es causado, normalmente, porque udevd trata de buscar un nombre de LDAP, pero falla, porque la red no está todavía. La solución es asegurarse de que todos los nombres de grupo del sistema están presentes localmente.

Extraiga los nombres de los grupos mencionados en las reglas de udev y los nombres de grupos realmente presentes en el sistema:

```
# fgrep -r GROUP /etc/udev/rules.d/ /usr/lib/udev/rules.d | perl -nle '/GROUP\s*=\s*"(.*?)"/ && print $1;' | sort | uniq > udev_groups
# cut -f1 -d: /etc/gshadow /etc/group | sort | uniq > present_groups

```

Para ver las diferencias, hacer una comparación de lado a lado:

```
# diff -y present_groups udev_groups
...
network							      <
nobody							      <
ntp							      <
optical								optical
power							      |	pcscd
rfkill							      <
root								root
scanner								scanner
smmsp							      <
storage								storage
...

```

En este caso, el grupo pcscd, por alguna razón, no está presente en el sistema. Agregue, en consecuencia, los grupos que faltan, en este caso:

```
# groupadd pcscd

```

Además, asegúrese de que los recursos locales se desbloquearon antes de recurrir a LDAP. El archivo de configuración `/etc/nsswitch.conf` debe contener la siguiente línea:

```
group: files ldap

```

### Problemas conocidos con el Hardware

#### Dispositivos BusLogic dejan de funcionar y causan bloqueos durante el arranque

Esto es un error en el kernel y todavía no se a provisto ningún arreglo.

#### Dispositivos extraibles no son reconocidos como tales

Cree una regla udev personalizada, configurando `UDISKS_SYSTEM_INTERNAL=0`. Para más detalles, consulte la manpage de udisks.

### Problemas conocidos con la carga automática

#### Problemas de sonido con algunos módulos no cargados automáticamente

Algunos usuarios han reportado este problema de entradas antiguas en `/etc/modprobe.d/sound.conf`. Intente limpiar ese archivo y probar de nuevo.

**Nota:** A partir de `udev>=171`, los módulos de emulación de OSS, (`snd_seq_oss, snd_pcm_oss, snd_mixer_oss`), no vienen cargados automáticamente por defecto.

### Problemas conocidos para usuarios con Kernel personalizado

#### Udev no se ejecuta

Asegúrese que tiene una versión del kernel 2.6.15 o superior. Los kernels anteriores no tienen las capacidades uevent necesarias para que udev realice la auto-carga.

### Dispositivos IDE CD/DVD

A partir de la versión 170, udev no es compatible con las unidades de CD-ROM/DVD-ROM, que vendrán cargadas como unidades tradicionales IDE con el módulo `ide_cd_mod` y vendrán identificadas como `/dev/hd*`. La unidad sigue siendo usable para las herramientas que acceden directamente al hardware, como cdparanoia, pero es invisible para los programas userspace más avanzados, como KDE.

Un motivo por el cual el módulo ide_cd_mod se carga antes que otros, como sr_mod, podría ser debido, quizás, a que, por cualquier razón, el módulo piix viene cargado por initramfs. En ese caso, es posible reemplazarlo con ata_piix en el archivo `/etc/mkinitcpio.conf`.

### Dispositivos ópticos con ID de grupo ajustado a «disk»

Si el ID de grupo de la unidad de disco óptico está ajustado a *disk* y desea que esté configurado para *optical* tiene que crear una regla udev personalizada:

 `/etc/udev/rules.d` 
```
# permissions for IDE CD devices
SUBSYSTEMS=="ide", KERNEL=="hd[a-z]", ATTR{removable}=="1", ATTRS{media}=="cdrom*", GROUP="optical"

# permissions for SCSI CD devices
SUBSYSTEMS=="scsi", KERNEL=="s[rg][0-9]*", ATTRS{type}=="5", GROUP="optical"
```

## Véase también

*   [Udev Homepage](https://www.kernel.org/pub/linux/utils/kernel/hotplug/udev/udev.html)
*   [An Introduction to Udev](http://www.linux.com/news/hardware/peripherals/180950-udev)
*   [Udev mailing list information](http://vger.kernel.org/vger-lists.html#linux-hotplug)