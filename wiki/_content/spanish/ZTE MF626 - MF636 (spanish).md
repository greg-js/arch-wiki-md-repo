**Estado de la traducción**
Este artículo es una traducción de [ZTE MF626 / MF636](/index.php/ZTE_MF626_/_MF636 "ZTE MF626 / MF636"), revisada por última vez el **2018-12-26**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=ZTE_MF626_/_MF636&diff=0&oldid=557086) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [USB 3G Modem](/index.php/USB_3G_Modem "USB 3G Modem")

El ZTE MF626 / MF636 es un módem USB que combina 3G+/3G con EDGE/GPRS en un dispositivo compacto. Cuenta con un lector de tarjetas micro-SD integrado. Puede enviar información a velocidades de hasta 4.5 Mbps en redes 3G+ y recibir información a velocidades de hasta 7.2 Mbps. También se conoce como el adaptador USB rojo de Rogers (compañía telefónica canadiense).

## Contents

*   [1 Configuración](#Configuración)
    *   [1.1 Deshabilitar el modo CD en el dispositivo](#Deshabilitar_el_modo_CD_en_el_dispositivo)
    *   [1.2 Deshabilitar el modo CD en el dispositivo con wvdial](#Deshabilitar_el_modo_CD_en_el_dispositivo_con_wvdial)
    *   [1.3 Configurar las reglas de udev](#Configurar_las_reglas_de_udev)
    *   [1.4 Crear una configuración wvdial](#Crear_una_configuración_wvdial)
*   [2 Conectarse a internet](#Conectarse_a_internet)
*   [3 Consejos y trucos](#Consejos_y_trucos)
*   [4 Véase también](#Véase_también)

## Configuración

### Deshabilitar el modo CD en el dispositivo

Con una máquina Windows, conecte el dispositivo USB y complete el breve asistente de instalación. Una vez hecho esto, cierre la aplicación Rogers que se inicia, luego diríjase al Administrador de dispositivos (*Panel de control > Sistema > Hardware > Administrador de dispositivos*). En la sección Puertos, busque el puerto COM que está conectado al módem USB (ignore el modo de diagnóstico). Conéctese a ese puerto COM a través del Hyperterminal, que se encuentra en el área de Accesorios del Menú de Inicio. Los parámetros de conexión son:

```
Bits per Second: 115200
Data bits: 8
Parity: None
Stop bits: 1
Flow Control: None

```

Una vez conectado, escriba las siguientes órdenes:

```
AT+ZOPRT=5
AT+ZCDRUN=8

```

Esto le indica al módem que no use el modo CD cuando se conecta por primera vez a un ordenador. Ahora salga del Hyperterminal y retire el módem USB. Ya ha terminado con Windows.

### Deshabilitar el modo CD en el dispositivo con wvdial

Primero, elimine el módulo `usb-storage`. Luego, cargue el módulo `usbserial`:

```
# rmmod usb_storage
# modprobe usbserial

```

Edite `/etc/wvdial.conf`:

```
[Dialer Defaults]
Modem = /dev/ttyUSB0
Modem Type = Analog Modem
ISDN = 0
Init1 = AT+ZOPRT=5
Init2 = AT+ZCDRUN=8

```

Ejecute *wvdial*, debería usar estas órdenes y fallar al intentar conectarse. Una vez que salga, desconecte el USB y vuelva a conectarlo, y debería ser reconocido como un módem.

### Configurar las reglas de udev

Cree la siguiente regla [udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)"):

 `/etc/udev/rules.d/90-zte.conf.rules`  `ACTION=="add", SUBSYSTEM=="usb", ATTRS{idVendor}=="19d2", ATTRS{idProduct}=="0031", RUN+="/sbin/modprobe usbserial vendor=0x19d2 product=0x0031", MODE="660", GROUP="network"` 

### Crear una configuración wvdial

[Wvdial](/index.php/Wvdial "Wvdial") es una interfaz fácil de usar para PPPd. Asegúrese de reemplazar la línea `/dev/ttyUSB0` con el nodo al que está conectado su módem USB, puede verlo con dmesg. Guárdelo como `/etc/wvdial.conf`.

```
[Dialer Defaults]
Modem = /dev/ttyUSB0
ISDN = off
Modem Type = USB Modem
Baud = 7200000
Init = ATZ
Init2 =
Init3 =
Init4 =
Init5 =
Init6 =
Init7 =
Init8 =
Init9 =
Phone = *99#
Phone1 =
Phone2 =
Phone3 =
Phone4 =
Dial Prefix =
Dial Attempts = 1
Dial Command = ATM1L3DT
Ask Password = off
Password = off
Username = na
Auto Reconnect = off
Abort on Busy = off
Carrier Check = off
Check Def Route = off
Abort on No Dialtone = off
Stupid Mode = on
Idle Seconds = 0
Auto DNS = on

```

Si lo anterior no funciona, intente lo siguiente (extraído de sakis3g):

Esto es para Etisalat Misr, pero debería funcionar para todas las demás redes que usan el mismo dispositivo.

```
[Dialer Defaults]
Modem = /dev/ttyUSB2
Modem Type = Analog Modem
ISDN = 0
Baud = 7200000
Dial Attempts = 3
Username = apn
Password = apn
Phone = *99#
Auto Reconnect = off
Stupid Mode = 1
Init1 = ATZ
Init6 = AT+CGEQMIN=1,4,64,640,64,640
Init7 = AT+CGEQREQ=1,4,64,640,64,640

```

## Conectarse a internet

Ahora simplemente ejecute *wvdial* para conectarse

```
# wvdial

```

Si ve que la salida muestra sus direcciones IP locales y endpoints PPP, entonces, ha funcionado.

## Consejos y trucos

Todos los pasos anteriores pueden quedar obsoletos si el módem USB se vuelve compatible con [sakis3g](http://www.sakis3g.org/), que es un script de línea de comandos todo en uno que automatiza todos los pasos anteriores. Los pasos de instalación son los siguientes:

```
wget "[http://www.sakis3g.org/versions/latest/$ARCH/sakis3g.gz](http://www.sakis3g.org/versions/latest/$ARCH/sakis3g.gz)" # where $ARCH is either i386 or amd64
gunzip sakis3g.gz
chmod +x sakis3g
./sakis3g --interactive

```

## Véase también

*   [Publicación 1 del foro de Ubuntu](http://ubuntuforums.org/showthread.php?t=1005910) - más detalles
*   [Publicación 2 del foro de Ubuntu](http://ubuntuforums.org/showthread.php?t=1065934) - más detalles