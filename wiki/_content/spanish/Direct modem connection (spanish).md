Artículos relacionados

*   [Configuring Network (Español)](/index.php/Configuring_Network_(Espa%C3%B1ol) "Configuring Network (Español)")

En este artículo se describe cómo se puede conectar directamente a Internet desde un marco de Arch Linux usando un [módem](https://en.wikipedia.org/wiki/es:M%C3%B3dem "wikipedia:es:Módem") interno o un módem externo en modo puente.

Debido a la falta de desarrolladores para cuestiones de acceso telefónico, conectar Arch a Internet con una línea telefónica requiere mucha configuración manual. Si ello fuera posible, configure un router dedicado para que pueda ser utilizado como una puerta de enlace predeterminada en el marco de Arch.

## Contents

*   [1 Módem analógico](#M.C3.B3dem_anal.C3.B3gico)
*   [2 ISDN](#ISDN)
    *   [2.1 Instalar y configurar el hardware](#Instalar_y_configurar_el_hardware)
    *   [2.2 Instalar y configurar las utilidades ISDN](#Instalar_y_configurar_las_utilidades_ISDN)
*   [3 DSL (PPPoE)](#DSL_.28PPPoE.29)
*   [4 Acceso telefónico a redes sin un marcador](#Acceso_telef.C3.B3nico_a_redes_sin_un_marcador)

## Módem analógico

Para poder usar un modem analógico, externo, compatible con Hayes, necesitas tener como mínimo el paquete [ppp](https://www.archlinux.org/packages/?name=ppp) instalado. Modifica el archivo `/etc/ppp/options` para que se ajuste a tus necesidades y según [pppd(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/pppd.8). Necesitarás definir un script de chat para proporcionar tu nombre de usuario y contraseña al ISP después de que la conexión inicial haya sido establecida. Las manpages para pppd y chat tienen ejemplos que deben ser suficientes para obtener una conexión funcionando si eres o bien lo suficientemente experimentado, o bien lo suficientemente terco. Con udev, tus puertos seriales son usualmente `/dev/tts/0` y `/dev/tts/1`.

**Sugerencia:** Lee [Dialup without a dialer HOWTO](/index.php/Dialup_without_a_dialer_HOWTO "Dialup without a dialer HOWTO") (sólo en inglés).

En lugar de luchar una gloriosa batalla con pppd, puedes optar por instalar [wvdial](https://www.archlinux.org/packages/?name=wvdial) o una herramienta similar para facilitar considerablemente el proceso de configuración. En caso que estés usando un así llamado WinModem, que es básicamente una tarjeta PCI funcionando como un modem analógico interno, puedes aprovechar la gran cantidad de información encontrada en la página de [LinModem](http://www.linmodems.org/).

## ISDN

Configurar una conexión ISDN requiere tres pasos:

1.  Instalar y configurar el hardware
2.  Instalar y configurar las utilidades [ISDN](https://en.wikipedia.org/wiki/es:Red_Digital_de_Servicios_Integrados "wikipedia:es:Red Digital de Servicios Integrados")
3.  Agregar los datos de configuración para tu [ISP](https://en.wikipedia.org/wiki/es:Proveedor_de_servicios_de_Internet "wikipedia:es:Proveedor de servicios de Internet")

### Instalar y configurar el hardware

Los kernels de Arch actuales en stock incluyen los módulos ISDN necesarios, por lo que no necesitarás recompilar tu kernel, a menos que vayas a usar un hardware ISDN bastante viejo. Después de instalar físicamente tu tarjeta ISDN en tu máquina o enchufar tu caja ISDN USB, puedes intentar cargar los [módulos del kernel](/index.php/Kernel_modules_(Espa%C3%B1ol) "Kernel modules (Español)"). Casi todas las tarjetas ISDN PCI pasivas son manejadas por el módulo hisax, que requiere dos parámetros: tipo y protocolo. El protocolo debe ser:

*   '1' si tu país usa el estándar 1TR6.
*   '2' si usa EuroISDN (EDSS1).
*   '3' si estás conectado a un así llamado "leased-line" sin canal D.
*   '4' para US NI1.

Detalles sobre estas configuraciones y cómo establecerlas está incluido en la documentación del kernel, específicamente en el subdirectorio isdn, y también están disponibles online. El parámetro "tipo" depende de tu tarjeta; una lista con todos los tipos posibles se encuentra en la documentación del kernel `README.HiSax`. Selecciona tu tarjeta y carga el [módulo](/index.php/Kernel_modules "Kernel modules") con `modprobe`, con las opciones apropiadas, de esta forma:

```
# modprobe hisax type=18 protocol=2

```

Esto cargará el módulo `hisax` para mi ELSA Quickstep 1000PCI, que es usada en Alemania con el protocolo EDSS1\. Deberías encontrar información útil de debug en tu archivo `/var/log/everything.log`, en el que deberías ver tu tarjeta siendo preparada para la acción. Ten en cuenta que probablemente necesites cargar algunos módulos USB antes de poder usar un adaptador ISDN USB externo.

Una vez que hayas confirmado que tu tarjeta funciona con cierta configuración, puedes añadir las opciones del [módulo](/index.php/Kernel_modules "Kernel modules") a tu `/etc/modprobe.d/`:

 `/etc/modprobe.d/isdn.conf` 
```
alias ippp0 hisax
options hisax type=18 protocol=2
```

Una vez que esto esté hecho, deberías tener un hardware soportado funcionando. ¡Ahora necesitas las utilidades básicas para efectivamente usarlo!

### Instalar y configurar las utilidades ISDN

Instala el paquete [isdn4k-utils](https://www.archlinux.org/packages/?name=isdn4k-utils), y como primer paso, lee la manpage hasta `isdnctrl`. Más abajo en la manpage encontrarás explicaciones sobre cómo crear un archivo de configuración que será parseado por `isdnctrl`, así como algunos ejemplos útiles de configuración. Notar que tendrás que añadir tu SPID a tu configuración de MSN separada por dos puntos (:) si usas US NI1.

Después de haber configurado tu tarjeta ISDN con la utilidad `isdnctrl`, deberías ser capaz de discar a la máquina que especificaste con el parámetro PHONE_OUT, pero debería fallar la autenticación de usuario y contraseña. Para que esto funcione, agrega tu usuario y contraseña a `/etc/ppp/pap-secrets` or `/etc/ppp/chap-secrets` como si estuvieras configurando un enlace PPP análogo normal, dependiendo del protocolo que use tu ISP para autenticación. En caso de duda, coloca tus datos en ambos archivos.

Si configuraste todo correctamente, deberías ser capaz de establecer una conexión dial-up con:

```
# isdnctrl dial ippp0

```

¡Si tienes problemas, recuerda revisar los archivos de log!

## DSL (PPPoE)

Estas instrucciones son relevantes sólo si es tu PC misma la que debe manejar la conexión con tu ISP. No necesitas hacer nada más que definir correctamente un gateway por defecto si usas un router aparte para hacer el trabajo pesado.

Antes de poder usar tu conexión DSL online, deberás instalar físicamente en tu computadora la tarjeta de red que vaya a estar conectada con tu [DSL](https://en.wikipedia.org/wiki/es:modemL%C3%ADnea_de_abonado_digital "wikipedia:es:modemLínea de abonado digital"). Después de añadir tu nueva tarjeta de red al [módulo del kernel](/index.php/Kernel_modules "Kernel modules") apropiado, tienes que instalar el paquete [rp-pppoe](https://www.archlinux.org/packages/?name=rp-pppoe) y ejecutar el script `pppoe-setup` para configurar tu conexión. Después de ingresar toda la información, puedes establecer y cortar la conexión con

```
# systemctl start adsl

```

y

```
# systemctl stop adsl

```

respectivamente. La configuración suele ser bastante fácil y directa, pero siéntete libre de leer las manpages por sugerencias.

Si quieres que la conexión se establezca automáticamente al iniciar, lanza la orden:

```
# systemctl enable adsl

```

o

```
# systemctl disable adsl

```

para cortar la 'conexión' automática al arranque.

## Acceso telefónico a redes sin un marcador

Esta sección explica cómo se puede ejecutar `pppd` directamente sin utilizar software de marcación ([dialer](https://en.wikipedia.org/wiki/es:Dialer "wikipedia:es:Dialer")) como `pon`/`poff`, `wvdial`, `kppp`, etc. Esto permite seguir conectado durante las paradas del servidor X y es extremadamente simple, en coherencia con la filosofía de Arch.

*   Realizar copia de respaldo de `/etc/ppp/options`

```
# mv /etc/ppp/options /etc/ppp/options.old

```

*   Crear un nuevo archivo `/etc/ppp/options` usando la plantilla:

```
lock
modem
debug
</dev/DISPOSITIVO>
115200
defaultroute
noipdefault
user <NOMBREDEUSUARIO>
connect 'chat -t60 \"\" ATZ OK ATX3 OK ATDT<NÚMERO> CONNECT'

```

Sustituir </dev/DISPOSITIVO> con el dispositivo de su módem. Para compararlo con el nombre del dispositivo en otro sistema operativo, eche un vistazo a la siguiente tabla:

```
Windows        GNU/Linux
 COM1   -->   /dev/ttyS0
 COM2   -->   /dev/ttyS1
 COM3   -->   /dev/ttyS2
 ...

```

Modifique el archivo para que el dispositivo apunte a su dispositivo de módem, para utilizar el nombre de usuario de su cuenta de [dial-up](https://en.wikipedia.org/wiki/es:Conexi%C3%B3n_por_l%C3%ADnea_conmutada "wikipedia:es:Conexión por línea conmutada"), y para marcar el número de su ISP a continuación de [ATDT](https://en.wikipedia.org/wiki/es:Conjunto_de_comandos_Hayes "wikipedia:es:Conjunto de comandos Hayes"). Puede desactivar la llamada en espera utilizando ATDT 70,15555555 (en América del Norte, de todos modos). También es posible que desee editar las órdenes del marcador; [busque](http://www.google.com) para obtener información sobre cómo hacer esto. Si su ISP utiliza [CHAP](https://en.wikipedia.org/wiki/es:CHAP "wikipedia:es:CHAP"), entonces el archivo siguiente es `chap-secrets`.

*   Editar `/etc/ppp/chap-secrets`. Ver [The PAP/CHAP secrets file](http://www.tldp.org/HOWTO/PPP-HOWTO/x1005.html) para más información:

```
"USERNAME" * "PASSWORD"

```

*   Ahora ya está listo para conectarse. Conéctese (como root) mediante `pppd /dev/modem` (o cualquier otro dispositivo que esté conectado como módem).

Para desconectarse, use `killall pppd`.

Si desea conectarse como usuario, puede usar [sudo](https://www.archlinux.org/packages/?name=sudo). Configure sudo para llamar a las órdenes anteriores desde su usuario, y puede utilizar los siguientes alias en su archivo `~/.bashrc` (o `/etc/bash.bashrc` para tenerlo disponible en todo el sistema):

```
alias dial='sudo /usr/sbin/pppd /dev/modem'
alias hang='sudo /usr/bin/killall pppd'

```

Ahora, desde un terminal, puede conectarse mediante la ejecución de `dial` y desconectarse con `hang`.