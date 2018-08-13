## Contents

*   [1 Introducción](#Introducci.C3.B3n)
*   [2 Desabilitar el modo CD en el modem](#Desabilitar_el_modo_CD_en_el_modem)
*   [3 Configurar reglas de UDEV](#Configurar_reglas_de_UDEV)
*   [4 Configurar reglas de HAL](#Configurar_reglas_de_HAL)
*   [5 Cree una configuración de wvdial](#Cree_una_configuraci.C3.B3n_de_wvdial)
*   [6 Conectese a internet](#Conectese_a_internet)
*   [7 Resolución de problemas](#Resoluci.C3.B3n_de_problemas)
*   [8 Agradecimientos](#Agradecimientos)

## Introducción

vea tambien [USB 3G Modem](/index.php/USB_3G_Modem "USB 3G Modem").

El modem ZTE MF626 / MF636 es un modem USB que combina 3G+/3G con EDGE/GPRS en un dispositivo conpacto. Este tambien integra un lector de tarjetas Micro SD. Puede subir datos a una velocidad de 4.5 Mbps en redes 3G+ y recibir datos a una velocidad de 7.2 Mbps.  Es tambien conocido como "Rogers (Operador celular canadiense) red stick USB dongle".

## Desabilitar el modo CD en el modem

Usando una maquina con Windows, inserte el dispositivo USB y espere a que inicie el instalador. Cuando este termine, cierre la ventana del programa de conexión, vaya al administrador de dispositivos (Panel de Control -> Sistema -> Hardware -> Administrador de dispositivos). En la sección de puertos, busque el puerto COM al que esta conectado el módem (no el de modo diagnostico); en mi caso es COM4\. Conéctese a ese puerto mediante Hyperterminal, puede encontrarlo en el submenu accesorios del menú inicio. Los parámetros de conexión son:

```
Bits por segundo: 115200
Bits de datos: 8
Paridad: Ninguno
Bits de parada: 1
Control de flujo: Ninguno

```

Cuando este conectado, escriba los siguientes comandos (ignore los mensajes que van apareciendo):

```
AT+ZOPRT=5 [ENTER]
AT+ZCDRUN=8 [ENTER]

```

Luego de cada comando presione ENTER, deberia aparecer un "ok", esto desabilitara la autoejecucion del modo CD en el modem, ahora puede salir de Hypterterminal y retirar el dispositivo, esto es todo lo que debe hacer en windows.

## Configurar reglas de UDEV

Cree un archivo en /etc/udev/rules.d/90-zte.conf que contenga lo siguiente:

```
ACTION!="add", GOTO="ZTE_End"
SUBSYSTEM=="usb", SYSFS{idProduct}=="0031", SYSFS{idVendor}=="19d2", GOTO="ZTE_Modem"
GOTO="ZTE_End"

LABEL="ZTE_Modem"
RUN+="/sbin/modprobe usbserial vendor=0x19d2 product=0x0031", MODE="660", GROUP="network"
LABEL="ZTE_End"

```

## Configurar reglas de HAL

La versión actual de HAL no conoce el modem ZTE MF626 / MF636, pero si conoce modelos similares. Para informar esto, cree el archivo /etc/hal/fdi/information/10-modem.fdi con lo siguiente:

```
<?xml version="1.0" encoding="UTF-8"?> <!-- -*- xml -*- -->

<deviceinfo version="0.2">
  <device>
    <match key="info.category" string="serial">
        <!-- ZTE MF636 HSDPA USB dongle -->
        <match key="@info.parent:usb.product_id" int="0x0031">
          <match key="@info.parent:usb.interface.number" int="3">
            <append key="modem.command_sets" type="strlist">GSM-07.07</append>
            <append key="modem.command_sets" type="strlist">GSM-07.05</append>
          </match>
        </match>
    </match>
  </device>
</deviceinfo>

```

## Cree una configuración de wvdial

Primero asegurese de tener instalado [wvdial](/index.php/Wvdial "Wvdial"), si no es así ejecute:

```
# Pacman -S wvdial

```

Wvdial es un front-end para PPPd muy facil de usar. La configuración es facil de comprender con pequeños conocimientos de ingles. Esta es probablemente mas larga de lo que requiera, aqui se deja un archivo de ejemplo con la configuración que ha funcionado con el autor de esta guia, recuerde cambiar los parametros de acuerdo al tipo de modem y su ISP. Reemplace /dev/ttyUSB0 con el cual el modem esta conectado, en algunos casos el modem abre mas de un puerto, usted debera probar con cada uno, en mi caso, ha funcionado con /dev/ttyUSB2, puede verificar cuales son los puertos abiertos con dmesg. Guarde el archivo como /etc/wvdial.conf

```
[Dialer Defaults]
Init1 = ATZ
Init2 = ATQ0 V1 E1 S0=0 &C1 &D2 +FCLASS=0
Init3 = AT+CGDCONT=1,"IP","APN DE SU RED" # ejemplo: "bam.clarochile.cl" (comillas incluidas)
Modem Type = Analog Modem
Baud = 7200000
New PPPD = yes
Modem = /dev/ttyUSB0
ISDN = off
Phone = *99#
Username = SU NOMBRE DE USUARIO DE LA RED # ejemplo: clarochile
Password = CONTRASEÑA DE LA RED # ejemplo: clarochile
Stupid Mode = on

```

## Conectese a internet

Ejecute wvdial como root o con [sudo](/index.php/Sudo_(Espa%C3%B1ol) "Sudo (Español)"):

```
# wvdial &

```

Si la salida reporta la IP local y las DNS, la conexión ha funcionado.

## Resolución de problemas

*   Si queda en la orden de marcado, y luego aparece un mensaje de desconexion, pruebe otro puerto como /dev/ttyUSB2
*   Si, a pesar de que esta conectado, no puede navegar en internet, pero si puede hacer ping a direcciones IP u ocupar otros programas que dependan de internet, revise las direcciones DNS, en algunas ocaciones el modem no informa correctamente entregando DNS erroneas, usted puede añadir la opción `Auto DNS = off` al final de su archivo wvdial.conf, y a continuación configurar sus DNS manualmente, pudiendo usar por ejemplo Open DNS ([http://www.opendns.org](http://www.opendns.org))
*   En pruebas en mi red, he sufrido problemas entre tener el modem conectado desde el inicio y pulseaudio, con el resultado de que pulseaudio arranca desactivado, la unica solucion que he encontrado hasta el momento es arrancar sin el modem conectado y al terminar la carga del sistema colocar este.

## Agradecimientos

Gracias a las siguientes paginas por brindar la información necesaria:

```
   * [http://www.zeroflux.org/blog/post/255](http://www.zeroflux.org/blog/post/255)
   * [http://www.matt-barrett.com/?p=5](http://www.matt-barrett.com/?p=5)
   * [http://ubuntuforums.org/showthread.php?t=1005910](http://ubuntuforums.org/showthread.php?t=1005910)
   * [http://ubuntuforums.org/showthread.php?t=1065934](http://ubuntuforums.org/showthread.php?t=1065934)

```