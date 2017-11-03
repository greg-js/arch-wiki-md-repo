Artículos relacionados

*   [Network Configuration (Español)](/index.php/Network_Configuration_(Espa%C3%B1ol) "Network Configuration (Español)")
*   [Software access point](/index.php/Software_access_point "Software access point")
*   [Ad-hoc networking](/index.php/Ad-hoc_networking "Ad-hoc networking")
*   [Internet sharing](/index.php/Internet_sharing "Internet sharing")

La configuración inalámbrica es un proceso que consta de dos partes: la primera parte consiste en identificar el controlador correcto para el dispositivo inalámbrico, asegurarse que está instalado (los cuales están disponibles en el disco de instalación, así que asegúrese de instalarlos), y configurar la interfaz. La segunda parte consiste en la elección de un método de gestión de las conexiones inalámbricas. Este artículo trata sobre las dos partes, y proporciona enlaces adicionales a las herramientas de gestión inalámbrica.

## Contents

*   [1 Controlador del dispositivo](#Controlador_del_dispositivo)
    *   [1.1 Comprobar el estado del controlador](#Comprobar_el_estado_del_controlador)
    *   [1.2 Instalar el controlador/firmware](#Instalar_el_controlador.2Ffirmware)
*   [2 Gestión de las redes inalámbricas](#Gesti.C3.B3n_de_las_redes_inal.C3.A1mbricas)
    *   [2.1 Configuración manual](#Configuraci.C3.B3n_manual)
        *   [2.1.1 Obtener información útil](#Obtener_informaci.C3.B3n_.C3.BAtil)
        *   [2.1.2 Activación de la interfaz](#Activaci.C3.B3n_de_la_interfaz)
        *   [2.1.3 Descubrir el punto de acceso](#Descubrir_el_punto_de_acceso)
        *   [2.1.4 Modalidades de funcionamiento](#Modalidades_de_funcionamiento)
        *   [2.1.5 Asociación](#Asociaci.C3.B3n)
        *   [2.1.6 Obtener una dirección IP](#Obtener_una_direcci.C3.B3n_IP)
        *   [2.1.7 Iniciar scripts/servicios personalizados](#Iniciar_scripts.2Fservicios_personalizados)
            *   [2.1.7.1 Conectarse manualmente a una red inalámbrica en el arranque con systemd y dhcpcd](#Conectarse_manualmente_a_una_red_inal.C3.A1mbrica_en_el_arranque_con_systemd_y_dhcpcd)
            *   [2.1.7.2 Systemd con wpa_supplicant e IP estática](#Systemd_con_wpa_supplicant_e_IP_est.C3.A1tica)
    *   [2.2 Configuración automática](#Configuraci.C3.B3n_autom.C3.A1tica)
        *   [2.2.1 Netctl](#Netctl)
        *   [2.2.2 Wicd](#Wicd)
        *   [2.2.3 NetworkManager](#NetworkManager)
        *   [2.2.4 WiFi Radar](#WiFi_Radar)
*   [3 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [3.1 Rfkill](#Rfkill)
    *   [3.2 Dominio regulador](#Dominio_regulador)
    *   [3.3 Observar los registros](#Observar_los_registros)
    *   [3.4 Ahorro de energía](#Ahorro_de_energ.C3.ADa)
    *   [3.5 Imposible obtener una dirección IP](#Imposible_obtener_una_direcci.C3.B3n_IP)
    *   [3.6 Conexión siempre fuera de tiempo](#Conexi.C3.B3n_siempre_fuera_de_tiempo)
        *   [3.6.1 Reducir la velocidad de la transmisión](#Reducir_la_velocidad_de_la_transmisi.C3.B3n)
        *   [3.6.2 Reducir la potencia de la transmisión](#Reducir_la_potencia_de_la_transmisi.C3.B3n)
        *   [3.6.3 Configurar rts y los umbrales de fragmentación](#Configurar_rts_y_los_umbrales_de_fragmentaci.C3.B3n)
    *   [3.7 Desconexiones al azar](#Desconexiones_al_azar)
        *   [3.7.1 Causa #1](#Causa_.231)
        *   [3.7.2 Causa #2](#Causa_.232)
*   [4 Solución de problemas sobre controladores y firmware](#Soluci.C3.B3n_de_problemas_sobre_controladores_y_firmware)
    *   [4.1 Ralink](#Ralink)
        *   [4.1.1 rt2x00](#rt2x00)
        *   [4.1.2 rt3090](#rt3090)
        *   [4.1.3 rt3290](#rt3290)
        *   [4.1.4 rt3573](#rt3573)
        *   [4.1.5 rt5572](#rt5572)
    *   [4.2 Realtek](#Realtek)
        *   [4.2.1 rtl8192cu](#rtl8192cu)
        *   [4.2.2 rtl8192e](#rtl8192e)
        *   [4.2.3 rtl8188eu](#rtl8188eu)
    *   [4.3 Atheros](#Atheros)
        *   [4.3.1 ath5k](#ath5k)
        *   [4.3.2 ath9k](#ath9k)
            *   [4.3.2.1 ASUS](#ASUS)
    *   [4.4 Intel](#Intel)
        *   [4.4.1 ipw2100 and ipw2200](#ipw2100_and_ipw2200)
        *   [4.4.2 iwlegacy](#iwlegacy)
        *   [4.4.3 iwlwifi](#iwlwifi)
        *   [4.4.4 Desactivar el parpadeo del LED](#Desactivar_el_parpadeo_del_LED)
    *   [4.5 Broadcom](#Broadcom)
    *   [4.6 Otros controladores/dispositivos](#Otros_controladores.2Fdispositivos)
        *   [4.6.1 Tenda w322u](#Tenda_w322u)
        *   [4.6.2 orinoco](#orinoco)
        *   [4.6.3 prism54](#prism54)
        *   [4.6.4 ACX100/111](#ACX100.2F111)
        *   [4.6.5 zd1211rw](#zd1211rw)
        *   [4.6.6 hostap_cs](#hostap_cs)
    *   [4.7 ndiswrapper](#ndiswrapper)
    *   [4.8 compat-drivers-patched](#compat-drivers-patched)
*   [5 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Controlador del dispositivo

De forma predeterminada el kernel de Arch Linux es *modular*, lo que significa que muchos de los controladores del hardware del equipo residen en el disco duro y están disponibles como *[modulos](/index.php/Kernel_modules_(Espa%C3%B1ol) "Kernel modules (Español)")*. En el arranque, [udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)") hace un inventario de su hardware, el cual cargará los módulos (controladores) apropiados para el hardware correspondiente, y el controlador, a su vez, permitirá la creación de una *interfaz* para el kernel.

Algunos chipsets inalámbricos también requieren un firmware, amén del controlador correspondiente. Muchas imágenes de firmware son proporcionados por el paquete [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) que se instala por defecto, sin embargo, las imágenes de firmware propietarias no están incluidas y deben instalarse por separado. Esto se describe en [#Instalar el controlador/firmware](#Instalar_el_controlador.2Ffirmware).

**Nota:**

*   Udev no es perfecto. Si el módulo apropiado no es cargado por udev en el arranque, simplemente [cárguelo manualmente](/index.php/Kernel_modules#Loading "Kernel modules"). Tenga en cuenta también que udev en ocasiones puede cargar más de un controlador para un dispositivo, y el conflicto resultante impide una configuración exitosa. Asegúrese de incluir en [blacklist](/index.php/Kernel_modules_(Espa%C3%B1ol)#Blacklisting "Kernel modules (Español)") el módulo no deseado.
*   El nombre de la interfaz para los diferentes controladores y chipsets pueden variar. Algunos ejemplos son `wlan0`, `eth1` y `ath0`. Véase también [esta sección](/index.php/Configuring_Network_(Espa%C3%B1ol)#Nombres_de_los_dispositivos "Configuring Network (Español)").

**Sugerencia:** Aunque no es estrictamente necesario, es una buena idea instalar primero las herramientas en el espacio de usuario mencionadas en [#Configuración manual](#Configuraci.C3.B3n_manual), especialmente ante la aparición de eventuales problemas.

### Comprobar el estado del controlador

Para comprobar si se ha cargado el controlador de la tarjeta, compruebe la salida de la orden `lspci -k`, con la cual se puede observar si hay algún controlador del kernel en uso, por ejemplo:

 `$ lspci -k` 
```
06:00.0 Network controller: Intel Corporation WiFi Link 5100
	Subsystem: Intel Corporation WiFi Link 5100 AGN
	Kernel driver in use: iwlwifi
	Kernel modules: iwlwifi

```

**Nota:** La tarjeta Wi-Fi interna de algunos portátiles puede ser, en realidad, un dispositivo USB, por lo que debe comprobar las salidas de estas órdenes también:

*   `lsusb -v`
*   `dmesg | grep usbcore`, debería ver algo como `usbcore: registered new interface driver rtl8187` en la salida

También puede ver la salida de la orden `ip link` para conocer si una interfaz inalámbrica (por ejemplo, `wlan0`, `wlp2s1`, `ath0`) ha sido creada. A continuación, active la interfaz con la orden `ip link set *interfaz* up`. Por ejemplo, suponiendo que la interfaz es `wlan0`:

```
# ip link set wlan0 up

```

Si recibe este mensaje de error: `SIOCSIFFLAGS: No such file or directory`, significa, sin duda, que su chipset inalámbrico requiere un firmware para funcionar.

Compruebe los eventuales mensajes del kernel relativos al cargamento del firmware:

 `$ dmesg | grep firmware` 
```
[   7.148259] iwlwifi 0000:02:00.0: loaded firmware version 39.30.4.1 build 35138 op_mode iwldvm

```

Si no hay salida relevante, compruebe los mensajes de la salida completa para el módulo que ha identificado anteriormente (`iwlwifi` en este ejemplo) para idenfificar el mensaje pertinente u otras cuestiones:

 `$ dmesg | grep iwlwifi` 
```
[   12.342694] iwlwifi 0000:02:00.0: irq 44 for MSI/MSI-X
[   12.353466] iwlwifi 0000:02:00.0: loaded firmware version 39.31.5.1 build 35138 op_mode iwldvm
[   12.430317] iwlwifi 0000:02:00.0: CONFIG_IWLWIFI_DEBUG disabled
...
[   12.430341] iwlwifi 0000:02:00.0: Detected Intel(R) Corporation WiFi Link 5100 AGN, REV=0x6B

```

Si el módulo del kernel se carga correctamente y la interfaz está funcionando, puede saltarse la siguiente sección.

### Instalar el controlador/firmware

Compruebe las siguientes listas para descubrir si su tarjeta está soportada:

*   La [Wiki de Ubuntu](https://help.ubuntu.com/community/WifiDocs/WirelessCardsSupported) tiene una buena lista de tarjetas inalámbricas y muestra si están o no soportadas, ya sea por el kernel de Linux, ya sea por un controlador en el espacio de usuario (incluye el nombre del controlador).
*   [Soporte inalámbrico para Linux](http://linux-wless.passys.nl/) y las preguntas para Linux de la [Lista de compatibilidad de hardware](http://www.linuxquestions.org/hcl/index.php?cat=10) (HCL) también proporcinan una buena base de datos sobre hardware compatible con el kernel.
*   La [página del kernel](http://wireless.kernel.org/en/users/Devices), contiene una matriz adicional de hardware compatible.

Si su tarjeta inalámbrica aparece en la lista anterior, continúe en [esta sección](#Soluci.C3.B3n_de_problemas_sobre_controladores_y_firmware) del presente artículo, que contiene información sobre la instalación de controladores y firmware de algunas tarjetas de red específicas. A continuación [compruebe el estado del controlador](#Comprobar_el_estado_del_controlador) de nuevo.

Si su tarjeta inalámbrica no aparece en la lista anterior, es posible que sea compatible solo en Windows (algunas como Broadcom, 3com, etc.). En estos casos, pruebe a usar [ndiswrapper](#ndiswrapper).

## Gestión de las redes inalámbricas

Suponiendo que los controladores están instalados y funcionando correctamente, tendrá que elegir un método para administrar las conexiones inalámbricas. Los apartados siguientes le ayudarán a decidir la mejor manera de hacer precisamente eso.

El procedimiento y herramientas necesarias dependerá de varios factores:

*   La naturaleza deseada de la gestión de configuración; desde un procedimiento de configuración totalmente manual desde la línea de órdenes hasta un software de gestión, con soluciones automáticas.
*   El tipo de cifrado (o su ausencia) que protege la red inalámbrica.
*   La necesidad de perfiles de red, si el equipo va a cambiar con frecuencia de redes (como un portátil).

**Sugerencia:**

*   Sea cual sea su elección, **realmente debe probar primero conectarse usando el método manual**. Esto le ayudará a entender los diferentes pasos que se necesitan y depurarlos, en su caso, si surge un problema.
*   Si puede (por ejemplo, si maneja su red Wi-Fi con punto de acceso), intente conectarlo sin cifrar, para comprobar que todo funciona. A continuación, intente utilizar el cifrado WEP (más fácil de configurar —pero manipulable en cuestión de segundos, por lo que no es más segura que una conexión sin cifrar—), WPA o WPA2.

La siguiente tabla muestra los diferentes métodos que pueden utilizarse para activar y gestionar una conexión de red inalámbrica, en función de la codificación y tipos de gestión, y las diversas herramientas que se requieren. Aunque puede haber otras posibilidades, estos son las más frecuentemente utilizados:

| Método de gestión | Activación de la interfaz | Gestión de la conexión Wi-Fi
(/=alternativas) | Asignar direcciones IP
(/=alternativas) |
| [Gestión manual](#Manual_setup),
sin cifrar o con encriptación WEP | [ip](/index.php/Core_utilities#ip "Core utilities") | [iw](https://www.archlinux.org/packages/?name=iw) / [iwconfig](https://www.archlinux.org/packages/?name=wireless_tools) | [ip](/index.php/Core_utilities#ip "Core utilities") / [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) / [dhclient](https://www.archlinux.org/packages/?name=dhclient) |
| [Gestión manual](#Manual_setup),
con encriptación WPA o WPA2 PSK | [ip](/index.php/Core_utilities#ip "Core utilities") | [iw](https://www.archlinux.org/packages/?name=iw) / [iwconfig](https://www.archlinux.org/packages/?name=wireless_tools) + [wpa_supplicant](/index.php/WPA_supplicant "WPA supplicant") | [ip](/index.php/Core_utilities#ip "Core utilities") / [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) / [dhclient](https://www.archlinux.org/packages/?name=dhclient) |
| [Gestión automática](#Automatic_setup),
compatibles con perfiles de red | [netctl](/index.php/Netctl "Netctl"), [Wicd](/index.php/Wicd "Wicd"), [NetworkManager](/index.php/NetworkManager "NetworkManager"), etc.

Estas herramientas arrastan las dependencias necesarias de la lista de paquetes al igual que con el método manual.

 |

### Configuración manual

Al igual que otras interfaces de red, las redes inalámbricas se controlan con `ip` del paquete [iproute2](https://www.archlinux.org/packages/?name=iproute2). Los programas proporcionados por el paquete [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools) son un conjunto básico de herramientas para configurar una red inalámbrica, Sin embargo, estas herramientas están en desuso en favor de la herramienta [iw](https://www.archlinux.org/packages/?name=iw). Si *iw* no funciona con su tarjeta, puede utilizar *wireless_tools*, la siguiente tabla presenta un resumen de las órdenes comparables entre ambos (véase [[1]](http://wireless.kernel.org/en/users/Documentation/iw/replace-iwconfig) para más ejemplos). Por otra parte, si se utiliza el cifrado WPA/WPA2, necesitará el paquete [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant). Estas poderosas herramientas en el espacio de usuario funcionan muy bien y permiten un total control manual de las conexiones de red inalámbricas.

**Nota:**

*   Los ejemplos de esta sección parten del supuesto de que el dispositivo inalámbrico es `wlan0` y que está conectado al punto de acceso inalámbrico `*your_essid*`. Sustituya dichos valores según su caso.
*   Tenga en cuenta que la mayoría de las órdenes tienen que ser ejecutadas con [permisos de root](/index.php/Users_and_groups "Users and groups"). Si se ejecutan como usuario normal, algunas de dichas órdenes (por ejemplo *iwlist*) salen sin error, pero no producen la salida correcta o bien pueden ser confusas.

| orden *iw* | orden *wireless_tools* | Descripción |
| iw dev wlan0 link | iwconfig wlan0 | Obtener el estado del enlace. |
| iw dev wlan0 scan | iwlist wlan0 scan | Escanear en busca de puntos de acceso disponibles. |
| iw dev wlan0 set type ibss | iwconfig wlan0 mode ad-hoc | Configurar el modo de operación para *ad-hoc*. |
| iw dev wlan0 connect *your_essid* | iwconfig wlan0 essid *your_essid* | Conectar para establecer conexión de red. |
| iw dev wlan0 connect *your_essid* 2432 | iwconfig wlan0 essid *your_essid* freq 2432M | Conectar para establecer conexión de red a través de un canal específico. |
| iw dev wlan0 connect *your_essid* key 0:*your_key* | iwconfig wlan0 essid *your_essid* key *your_key* | Conectar a una red encriptada WEP usando clave hexadecimal. |
| iw dev wlan0 connect *your_essid* key 0:*your_key* | iwconfig wlan0 essid *your_essid* key s:*your_key* | Conectar a una red encriptada WEP usando clave ASCII. |
| iw dev wlan0 set power_save on | iwconfig wlan0 power on | Activar ahorro de energía. |

**Nota:** Según el hardware y el tipo de cifrado, algunos de estos pasos pueden no ser necesario. Algunas tarjetas se sabe que requieren la activación de la interfaz y/o el escaneo del punto de acceso antes de ser asociado a un punto de acceso y asignarle una dirección IP. Puede que sea necesario experimentar previamente. Por ejemplo, los usuarios pueden intentar WPA/WPA2 directamente para activar su red inalámbrica desde el paso [#Asociación](#Asociaci.C3.B3n).

#### Obtener información útil

**Sugerencia:** Véase [official documentation](http://wireless.kernel.org/en/users/Documentation/iw) de la utilidad *iw* para obtener más ejemplos.

*   En primer lugar, necesita encontrar el nombre de la interfaz inalámbrica. Se puede hacer con la siguiente orden:

 `$ iw dev` 
```
phy#0
	Interface **wlan0**
		ifindex 3
		wdev 0x1
		addr 12:34:56:78:9a:bc
		type managed
		channel 1 (2412 MHz), width: 40 MHz, center1: 2422 MHz

```

*   Para comprobar el estado del enlace, utilice la orden de abajo. He aquí un ejemplo de salida cuando no está conectado a un punto de acceso:

 `$ iw dev wlan0 link` 
```
Not connected.

```

En cambio, cuando se conecta a un punto de acceso, se verá algo como:

 `$ iw dev wlan0 link` 
```
Connected to 12:34:56:78:9a:bc (on wlan0)
	SSID: MyESSID
	freq: 2412
	RX: 33016518 bytes (152703 packets)
	TX: 2024638 bytes (11477 packets)
	signal: -53 dBm
	tx bitrate: 150.0 MBit/s MCS 7 40MHz short GI

	bss flags:	short-preamble short-slot-time
	dtim period:	1
	beacon int:	100

```

*   Se puede obtener información estadística, como por ejemplo, la cantidad de bytes tx/rx, intensidad de la señal, etc., con la siguiente orden:

 `$ iw dev wlan0 station dump` 
```
Station 12:34:56:78:9a:bc (on wlan0)
	inactive time:	1450 ms
	rx bytes:	24668671
	rx packets:	114373
	tx bytes:	1606991
	tx packets:	8557
	tx retries:	623
	tx failed:	1425
	signal:  	-52 dBm
	signal avg:	-53 dBm
	tx bitrate:	150.0 MBit/s MCS 7 40MHz short GI
	authorized:	yes
	authenticated:	yes
	preamble:	long
	WMM/WME:	yes
	MFP:		no
	TDLS peer:	no

```

#### Activación de la interfaz

*(Opcional, aunque puede ser necesaria)*

Algunas tarjetas requieren que la interfaz del kernel esté activada antes de poder usar la utilidad *iw* o *wireless_tools*:

```
# ip link set wlan0 up

```

**Nota:** Si se obtienen errores como `RTNETLINK answers: Operation not possible due to RF-kill`, asegúrese de que el interruptor de hardware está en *on* (encendido). Además, la tarjeta de red inalámbrica puede estar bloqueda por algún sofware.Véase [#Rfkill](#Rfkill) para más detalles.

Para verificar que la interfaz está funcionando, inspeccione la salida de la siguiente orden:

 `# ip link show wlan0` 
```
3: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state DOWN mode DORMANT group default qlen 1000
    link/ether 12:34:56:78:9a:bc brd ff:ff:ff:ff:ff:ff

```

La `UP` en `<BROADCAST,MULTICAST,UP,LOWER_UP>` es lo que indica que la interfaz está activa, no el posterior `state DOWN`.

#### Descubrir el punto de acceso

Para ver los puntos de acceso disponibles:

```
# iw dev wlan0 scan | less

```

**Nota:** Si aparece le mensaje «*Interface doesn't support scanning*» (interfaz no compatible con el escaneo), entonces probablemente se olvidó de instalar el firmware. En algunos casos, este mensaje también se muestra cuando no se está ejecutando *iwlist* como root.

**Sugerencia:** Dependiendo de su ubicación, es posible que tenga que establecer el [dominio regulador](#Dominio_regulador) correcto, con el fin de ver todas las redes disponibles.

Puntos importantes a comprobar:

*   **SSID:** el nombre de la red.
*   **Signal:** informa en una proporción de potencia inalámbrica en dbm (por ejemplo -100 a 0). Cuanto más cerca el valor negativo esté de cero, mejor será la señal. Observando el consumo de energía registrado entre un vínculo de buena calidad y otro de mala, debería dar una idea acerca del rango apropiado para uno.
*   **Security:** no informa directamente, sino que hay que comprobar la línea que comienza con `capability`. Si esta es `Privacy`, por ejemplo `capability: ESS Privacy ShortSlotTime (0x0411)`, entonces la conexión de red está protegida de alguna manera.
    *   Si se observa un bloque de información `RSN`, entonces la red está protegida con el protocolo [Robust Security Network](https://en.wikipedia.org/wiki/Robust_Security_Network "wikipedia:Robust Security Network"), también conocido como WPA2.
    *   Si se observa un bloque de información `WPA`, entonces la red está protegida con el protocolo [Wi-Fi Protected Access](https://en.wikipedia.org/wiki/Wi-Fi_Protected_Access "wikipedia:Wi-Fi Protected Access").
    *   En los bloques `RSN` y `WPA` se puede encontrar la siguiente información:
        *   **Group cipher:** valores TKIP, CCMP, ambos, otros.
        *   **Pairwise ciphers:** valores TKIP, CCMP, ambos, otros. No necesariamente el mismo valor de Group cipher.
        *   **Authentication Suites:** valores PSK, 802.1x, otros. A través del router, por lo general encontrará PSK (*por ejemplo* la passphrase). En las universidades, es más probable que encuentre la suite 802.1x que requiere nombre de usuario y contraseña. Entonces tendrá que saber qué administración de claves está en uso (por ejemplo, EAP), y la encapsulación que utiliza (por ejemplo, PEAP). Encuentre más detalles en [Wikipedia:List_of_authentication_protocols](https://en.wikipedia.org/wiki/List_of_authentication_protocols "wikipedia:List of authentication protocols") y artículos relacionados.
    *   Si no se observa ni `RSN` ni `WPA` pero informa que es `Privacy`, entonces se utiliza WEP.

#### Modalidades de funcionamiento

*(Opcional, aunque puede ser necesario)*

En este paso, puede que tenga que ajustar el modo de funcionamiento adecuado de la tarjeta inalámbrica. Más específicamente, si se va a conectar una [red ad-hoc](/index.php/Ad-hoc_networking "Ad-hoc networking"), es necesario establecer el modo de funcionamiento a `ibss`:

```
# iw dev wlan0 set type ibss

```

**Nota:** Para cambiar el modo de funcionamiento en algunas tarjetas puede que sea necesario que desactivar la interfaz inalámbrica (*down*) (`ip link set wlan0 down`).

#### Asociación

Dependiendo del cifrado, es necesario asociar el dispositivo inalámbrico con el punto de acceso que desea utilizar y transmitirle la clave de cifrado.

*   **Sin cifrado** `# iw dev wlan0 connect your_essid` 
*   **WEP**
    *   Usar una clave hexadecimal o ASCII: `# iw dev wlan0 connect your_essid key 0:your_key` 
    *   Utilizar una clave hexadecimal o ASCII, especificando la tercera clave establecida como predeterminada (claves contadas desde cero): `# iw dev wlan0 connect your_essid key d:2:your_key` 
*   **WPA/WPA2**

Hay que modificar el archivo `/etc/wpa_supplicant.conf` como se describe en [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") y acomodarlo a lo que obtuvo en [#Descubrir el punto de acceso](#Descubrir_el_punto_de_acceso). A continuación, ejecute la siguiente orden:

```
# wpa_supplicant -i wlan0 -c /etc/wpa_supplicant.conf

```

Esto es suponiendo que el dispositivo utiliza el controlador `wext`. Si esto no funciona, puede que tenga que reajustar estas opciones. Si está conectado correctamente, continúe en una nueva terminal (o abandone `wpa_supplicant` con `Ctrl+c` y añada el parámetro `-B` a la orden anterior para que se ejecute en segundo plano). [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") contiene más información y solución de problemas.

Independientemente del método utilizado, se puede comprobar si se ha asociado con éxito de la siguiente manera:

```
# iw dev wlan0 link

```

#### Obtener una dirección IP

**Nota:** Véase [configurar la dirección IP](/index.php/Configuring_Network_(Espa%C3%B1ol)#Configurar_la_direcci.C3.B3n_IP "Configuring Network (Español)") para obtener más ejemplos. Esta parte es idéntica.

Por último, hay que proporcionar una dirección IP a la interfaz de red. Ejemplos sencillos son:

```
# dhcpcd wlan0

```

o

```
# dhclient wlan0

```

para DHCP, o

```
# ip addr add 192.168.0.2/24 dev wlan0
# ip route add default via 192.168.0.1

```

para direcciones IP estáticas.

**Sugerencia:** [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) contiene un hook (activado por defecto) para poner en marcha de forma automática [WPA supplicant](/index.php/WPA_supplicant_(Espa%C3%B1ol) "WPA supplicant (Español)") en busca de interfaces inalámbricas. Se inicia solo si existe un archivo de configuración en `/etc/wpa_supplicant.conf` y sin un proceso *wpa_supplicant* sondeando la interfaz en cuestión. En la mayoría de los casos, no es necesario crear ningún [servicio personalizado](#Conectarse_manualmente_a_una_red_inal.C3.A1mbrica_en_el_arranque_con_systemd_y_dhcpcd), basta con activar `dhcpcd@*interfaz*`.

#### Iniciar scripts/servicios personalizados

Aunque el método de configuración manual le ayudará a solucionar problemas inalámbricos, tendrá que volver a escribir cada órden cada vez que reinicie el sistema. Sin embargo, también puede escribir un script para automatizar todo el proceso, lo que supone una forma muy eficaz de administrar las conexiones de red, manteniendo un control total sobre la configuración. Puede encontrar algunos ejemplos en esta sección.

##### Conectarse manualmente a una red inalámbrica en el arranque con systemd y dhcpcd

Este ejemplo utiliza [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") para conectarse en el arranque a una red inalámbrica a través de [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") y obteniendo la dirección IP mediante [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd).

**Nota:** Asegúrese de que [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) está instalado, y cree el archivo `/etc/wpa_supplicant.conf`. Véase [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") para obtener más detalles.

Cree una unidad de systemd, por ejemplo `/etc/systemd/system/network-wireless@.service`:

 `/etc/systemd/system/network-wireless@.service` 
```
[Unit]
Description=Wireless network connectivity (%i)
Wants=network.target
Before=network.target
BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

[Service]
Type=oneshot
RemainAfterExit=yes

ExecStart=/usr/bin/ip link set dev %i up
ExecStart=/usr/bin/wpa_supplicant -B -i %i -c /etc/wpa_supplicant.conf
ExecStart=/usr/bin/dhcpcd %i

ExecStop=/usr/bin/ip link set dev %i down

[Install]
WantedBy=multi-user.target

```

Active la unidad e iníciela, pasándole el nombre de la interfaz:

```
# systemctl enable network-wireless@wlan0.service
# systemctl start network-wireless@wlan0.service

```

##### Systemd con wpa_supplicant e IP estática

**Nota:** Asegúrese de que [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) está instalado y crear el archivo `/etc/wpa_supplicant.conf`. Véase [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") para obtener más detalles.

En primer lugar, cree el archivo de configuración del servicio de [systemd](/index.php/Systemd "Systemd"), sustituyendo `*interface*` con el nombre de la interfaz propia:

 `/etc/conf.d/network-wireless@*interface*` 
```
address=192.168.0.10
netmask=24
broadcast=192.168.0.255
gateway=192.168.0.1

```

Cree un archivo de unidad de systemd:

 `/etc/systemd/system/network-wireless@.service` 
```
[Unit]
Description=Wireless network connectivity (%i)
Wants=network.target
Before=network.target
BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

[Service]
Type=oneshot
RemainAfterExit=yes
EnvironmentFile=/etc/conf.d/network-wireless@%i

ExecStart=/usr/bin/ip link set dev %i up
ExecStart=/usr/bin/wpa_supplicant -B -i %i -c /etc/wpa_supplicant.conf
ExecStart=/usr/bin/ip addr add ${address}/${netmask} broadcast ${broadcast} dev %i
ExecStart=/usr/bin/ip route add default via ${gateway}

ExecStop=/usr/bin/ip addr flush dev %i
ExecStop=/usr/bin/ip link set dev %i down

[Install]
WantedBy=multi-user.target

```

Active la unidad e iníciela, pasándole el nombre de la interfaz:

```
# systemctl enable network-wireless@wlan0.service
# systemctl start network-wireless@wlan0.service

```

### Configuración automática

Hay muchas soluciones donde elegir, pero recuerde que todas ellas se excluyen mútuamente, no se deben ejecutar dos demonios al mismo tiempo. La siguiente tabla compara los diferentes gestores de conexiones, con notas adicionales en las secciones siguientes.

| Gestor de conexión | Soporte
para perfiles
de red | Itinerancia
(autoconexión si se cae
o cambia de lugar) | Soporte para [PPP](https://en.wikipedia.org/wiki/es:Point-to-Point_Protocol "wikipedia:es:Point-to-Point Protocol")
(por ejemplo, modem 3G) | GUI
Oficial | Herramientas de consola |
| [ConnMan](/index.php/ConnMan "ConnMan") | Sí | Sí | Sí | No | `connmanctl` |
| [Netctl](/index.php/Netctl "Netctl") | Sí | Sí | Sí | No | `netctl`,`wifi-menu` |
| [NetworkManager](/index.php/NetworkManager "NetworkManager") | Sí | Sí | Sí | Sí | `nmcli` |
| [Wicd](/index.php/Wicd "Wicd") | Sí | Sí | No | Sí | `wicd-curses` |

#### Netctl

*netctl* sustituye a *netcfg*, diseñado para trabajar con systemd. Utiliza una configuración basada en perfiles y es capaz de la detección y conexión a una amplia gama de tipos de red. No es difícil de manejar usando herramientas gráficas.

Consulte: [Netctl (Español)](/index.php/Netctl_(Espa%C3%B1ol) "Netctl (Español)")

#### Wicd

Wicd es un gestor de red que puede manejar tanto conexiones inalámbricas como por cable. Está escrito en Python y GTK, con un menor número de dependencias que NetworkManager, por lo que es una solución ideal para los usuarios de escritorios ligeros. Wicd está disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

Consulte: [Wicd (Español)](/index.php/Wicd_(Espa%C3%B1ol) "Wicd (Español)")

**Nota:** [wicd](/index.php/Wicd_(Espa%C3%B1ol) "Wicd (Español)") puede provocar caídas excesivas de las conexiones con algunos controladores, mientras que [NetworkManager](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)") podría funcionar mejor.

#### NetworkManager

NetworkManager es una herramienta de gestión de red avanzada que está activada, por defecto, en la mayoría de las distribuciones GNU/Linux. Además de gestionar las conexiones por cable, NetworkManager proporciona, sin problemas, la gestión de las conexiones inalámbricas y de roaming, con un programa GUI fácil de usar para seleccionar la red deseada.

Consulte: [NetworkManager (Español)](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)")

**Note:** La extensión [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) de GNOME también trabaja en [Xfce](/index.php/Xfce "Xfce"), si instala primero [xfce4-xfapplet-plugin](https://aur.archlinux.org/packages/xfce4-xfapplet-plugin/) (disponible en [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)")). Además, hay applets disponibles para [KDE](/index.php/KDE "KDE").

#### WiFi Radar

WiFi Radar es una utilidad Python/PyGTK2 para la gestión de perfiles inalámbricos (y *solo* inalámbricos). Le permite escanear las redes disponibles y crear perfiles para sus redes preferidas.

Consulte: [Wifi Radar](/index.php/Wifi_Radar "Wifi Radar")

## Solución de problemas

Esta sección contiene sugerencias para resolver problemas generales, no estrictamente vinculados con problemas con los controladores o firmware. Para estos últimos temas, vea la sección siguiente.

### Rfkill

Muchos portátiles tienen un botón de hardware (o switch -*«alternador»*-) para desactivar la tarjeta inalámbrica, sin embargo, la tarjeta puede también ser bloqueada por el kernel. Esto puede ser manejado por rfkill. Utilice *rfkill* para mostrar el estado actual:

 `# rfkill list` 
```
0: phy0: Wireless LAN
	Soft blocked: yes
	Hard blocked: yes

```

Si la tarjeta está *hard-blocked* («bloqueada por el hardware»), utilice el botón del hardware (switch) para desbloquearla. Si la tarjeta no está *hard-blocked* pero está *soft-blocked* («bloqueada por el sotfware»), utilice la siguiente orden:

```
# rfkill unblock wifi

```

**Nota:** Es posible que la tarjeta pase del estado *hard-blocked* y *soft-unblocked*, al estado *hard-unblocked* y *soft-blocked*, presionando el botón del hardware (es decir, *soft-blocked* se cambia de estado sin motivo). Esto se puede ajustar mediante la regulación de algunas de las opciones del [módulo del kernel](/index.php/Kernel_modules_(Espa%C3%B1ol) "Kernel modules (Español)") `rfkill` .

Para más información: [http://askubuntu.com/questions/62166/siocsifflags-operation-not-possible-due-to-rf-kill](http://askubuntu.com/questions/62166/siocsifflags-operation-not-possible-due-to-rf-kill)

### Dominio regulador

Por ejemplo, el controlador `iwl3945` está configurado, por defecto, para trabajar solo con redes en los canales 1 a 11\. Bandas de frecuencias más altas no están permitidas en algunas partes del mundo (por ejemplo, en los EE.UU.). En la UE, sin embargo, los canales 12 y 13 se utilizan muy comúnmente (y en Japón permite el canal 14). Si el dominio regulador se ajusta a, por ejemplo EE.UU., consecuentemente, las redes que usan los canales más altos no se mostrará en la exploración.

Es posible configurar el módulo del kernel [cfg80211](http://wireless.kernel.org/en/developers/Documentation/cfg80211) para utilizar el dominio regulador específico, añadiendo, por ejemplo, `options cfg80211 ieee80211_regdom=EU` a `/etc/modprobe.d/modprobe.conf` (véase [módulos del kernel](/index.php/Kernel_modules_(Espa%C3%B1ol) "Kernel modules (Español)") para más detalles).

**Sugerencia:** Compruebe el bloque `Frequencies:` en la salida de `iw list` para ver qué frecuencias admite su tarjeta.

Una configuración alternativa podría ser la instalación del paquete [crda](https://www.archlinux.org/packages/?name=crda) y editar `/etc/conf.d/wireless-regdom` (el archivo es en realidad proporcionado por [wireless-regdb](https://www.archlinux.org/packages/?name=wireless-regdb) que es una dependencia de [crda](https://www.archlinux.org/packages/?name=crda)).

### Observar los registros

Una buena medida inicial para solucionar problemas, es analizar primero los archivos de registro del sistema. A fin de no analizar de forma manual dichos archivos directamente, puede ayudar abrir una segunda ventana de terminal/consola y ver los mensajes del kernel con la orden:

```
$ dmesg -w

```

mientras se realización la acción correspondiente, por ejemplo, intentar asociarse a una red inalámbrica.

Cuando se utiliza una herramienta de gestión de red, se puede hacer lo mismo para systemd con la orden:

```
# journalctl -f 

```

Las herramientas individuales que se utilizan en este artículo proporcionan más opciones para una salida de depuración de errores más detallada, que se pueden utilizar en un segundo paso del análisis, si es necesario.

### Ahorro de energía

Véase [Power saving#Network interfaces](/index.php/Power_saving#Network_interfaces "Power saving").

### Imposible obtener una dirección IP

*   Si falla repetidamente la obtención de una dirección IP por el cliente [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) predeterminado, pruebe instalando y usando [dhclient](https://www.archlinux.org/packages/?name=dhclient) en su lugar. No olvide seleccionar *dhclient* como el principal cliente DHCP en la [gestión de la conexión](#Configuraci.C3.B3n_autom.C3.A1tica).

*   Si puede obtener una dirección IP para la interfaz de cable y no para la interfaz inalámbrica, pruebe a desactivar las funciones de ahorro de energía de la tarjeta inalámbrica: ` # iwconfig wlan0 power off` 

*   Si se obtiene un error de timeout (*«tiempo excedido»*), debido a problemas *waiting for carrier*, entonces es posible que tenga que configurar la modalidad del canal a `auto` para ese dispositivo específico: ` # iwconfig wlan0 channel auto` Antes de cambiar el canal a auto, asegúrese de que su interfaz inalámbrica está desactivada. Después de que se ha cambiado con éxito, puede activar la interfaz de nuevo y continuar desde ahí.

### Conexión siempre fuera de tiempo

El controlador puede sufrir una gran cantidad de reintentos excesivos de transmisión y errores de «invalid misc», por alguna razón desconocida, lo que provoca la pérdida de gran cantidad de paquetes y continuas desconexiones, a veces instantáneamente. Los siguientes consejos pueden ser útiles.

#### Reducir la velocidad de la transmisión

Pruebe estableciendo la velocidad más baja, por ejemplo a 5.5M:

```
# iwconfig wlan0 rate 5.5M auto

```

Fije la opción para asegurarse de que el controlador no cambia la velocidad por su cuenta, lo que hará la conexión un poco más estable:

```
# iwconfig wlan0 rate 5.5M fixed

```

#### Reducir la potencia de la transmisión

Puede tratar de reducir la potencia de la transmisión también. Esto puede ahorrar energía:

```
# iwconfig wlan0 txpower 5

```

Los valores aceptados son de `0` a `20`, `auto` y `off`.

#### Configurar rts y los umbrales de fragmentación

Las opciones de iwconfig por defecto desactivan rts y los umbrales de fragmentación. Estas opciones son particularmente útiles en presencia de muchos puntos de acceso adyacentes o en un entorno con interferencias.

El valor mínimo para el valor de la fragmentación es 256 y el máximo es 2346\. En muchos controladores de Windows al máximo es el valor por defecto:

```
# iwconfig wlan0 frag 2346

```

Para rts el mínimo es 0 y el máximo de 2347\. Una vez más controladores de Windows, a menudo, utilizan el máximo por defecto:

```
# iwconfig wlan0 rts 2347

```

### Desconexiones al azar

#### Causa #1

Si dmesg informa `wlan0: deauthenticating from MAC by local choice (reason=3)` y se pierde la conexión Wi-Fi, es probable que tenga un modo demasiado agresivo de ahorro de energía para su tarjeta Wi-Fi [[2]](http://us.generation-nt.com/answer/gentoo-user-wireless-deauthenticating-by-local-choice-help-204640041.html). Pruebe a desactivar las funciones de ahorro de energía de la tarjeta inalámbrica:

```
# iwconfig wlan0 power off

```

Véase [Power saving](/index.php/Power_saving "Power saving") para obtener consejos sobre cómo hacerlo permanente (basta especificar `off` en lugar de `on`).

Si su tarjeta no soporta la función `iwconfig wlan0 power off`, compruebe en la **BIOS** las opciones relativas a la administración de energía. La desactivación de la administración de energía para el slot PCI-Express en la BIOS de un Lenovo W520 resolvió este problema.

#### Causa #2

Si experimenta desconexiones frecuentes y dmesg muestra mensajes tales como:

`ieee80211 phy0: wlan0: No probe response from AP xx:xx:xx:xx:xx:xx after 500ms, disconnecting`

intente cambiar el ancho de banda del canal a `20MHz` a través de la página de configuración del router.

## Solución de problemas sobre controladores y firmware

Esta sección trata sobre los métodos y procedimientos para la instalación de módulos del kernel y *firmware* para chipsets específicos, que difieren del método general.

Véase el artículo sobre los [módulos del Kernel](/index.php/Kernel_modules_(Espa%C3%B1ol) "Kernel modules (Español)") para obtener instrucciones generales sobre las operaciones con los módulos.

### Ralink

#### rt2x00

Este es el controlador unificado para los chipsets Ralink (que reemplaza a `rt2500`, `rt61`, `rt73`, etc.). Este controlador está incorporado en el kernel de Linux desde la versión 2.6.24, con lo cual basta con cargar el módulo correcto para el chip: `rt2400pci`, `rt2500pci`, `rt2500usb`, `rt61pci` o `rt73usb`, los cuales, a su vez, cargarán automáticamente los módulos `rt2x00` apropiados.

Una lista de los dispositivos soportados por los módulos está disponible en la [página principal](http://rt2x00.serialmonkey.com/wiki/index.php/Hardware) del proyecto.

	Notas adicionales.-

*   Desde el Kernel 3.0, rt2x00 incluye también estos controladores: `rt2800pci`, `rt2800usb`.
*   Desde el kernel 3.0, los controladores `rt2860sta` y `rt2870sta` se sustituyen por los controladores `rt2800pci` y `rt2800usb`.
*   Algunos dispositivos tienen una amplia gama de opciones que se pueden configurar con `iwpriv`. Estas están documentadas en [los archivos fuentes](http://web.ralinktech.com/ralink/Home/Support/Linux.html) disponibles en Ralink.

#### rt3090

Para los productos que utilizan el chipset rt3090, debería ser posible utilizar el controlador `rt2800pci`, sin embargo, no funciona con este chipset muy bien (por ejemplo, a veces no es posible utilizar una mayor tasa de 2Mb/s).

La mejor manera es usar el controlador [rt3090](https://aur.archlinux.org/packages/rt3090/) disponible en [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)"). Asegúrese de poner en [blacklist](/index.php/Kernel_modules#Blacklisting "Kernel modules") el módulo `rt2800pci`, y configurar el módulo `rt3090sta` para que se [cargue](/index.php/Kernel_modules#Loading "Kernel modules") en el arranque.

**Nota:** Este controlador también funciona con el chipset rt3062.

#### rt3290

El chipsep rt3290 es reconocido por el módulo `rt2800pci` del Kernel. Sin embargo , algunos usuarios experimentan problemas y prefieren un parche para el controlador Ralink que parece dar buenos resultados en estos [casos](https://bbs.archlinux.org/viewtopic.php?id=161952).

#### rt3573

Nuevo chipset a partir de 2012\. Puede requerir controladores propietarios de Ralink . Algunos fabricantes los utilizan, consulte el hilo del foro [Belkin N750 DB wireless usb adapter](https://bbs.archlinux.org/viewtopic.php?pid=1164228#p1164228).

#### rt5572

Nuevo chipset a partir de 2012 con soporte para bandas de hasta 5 Ghz. Puede requerir controladores propietarios de Ralink, lo que requiere cierto trabajo para compilarlo. En el momento de escribir esta guía está disponible la compilación para un DLINK DWA-160 rev. B2 [aquí](http://bernaerts.dyndns.org/linux/229-ubuntu-precise-dlink-dwa160-revb2).

### Realtek

#### rtl8192cu

El controlador se encuentra ahora en el kernel, pero muchos usuarios han informado que no son capaces de conectarse, aunque funciona buscando las redes.

El paquete [dkms-8192cu](https://aur.archlinux.org/packages/dkms-8192cu/) disponible en AUR puede ser una mejor opción.

#### rtl8192e

El controlador es parte del paquete actual del kernel. La inicialización del módulo puede fallar al arrancar dando este mensaje de error:

```
rtl819xE:ERR in CPUcheck_firmware_ready()
rtl819xE:ERR in init_firmware() step 2
rtl819xE:ERR!!! _rtl8192_up(): initialization is failed!
r8169 0000:03:00.0: eth0: link down

```

Una solución simple puede consistir en descargar el módulo:

```
# modprobe -r r8192e_pci

```

y volver a cargar el módulo (después de una pausa):

```
# modprobe r8192e_pci

```

#### rtl8188eu

Algunos dispositivos de seguridad, como el TP-Link TL-WN725N v2 (aunque parece que utiliza el chipset rtl8179), utilizan chipsets compatibles con este controlador. Para usarlo hay que instalar el paquete [dkms-8188eu](https://aur.archlinux.org/packages/dkms-8188eu/) disponible en AUR.

### Atheros

El [equipo de MadWifi](http://madwifi-project.org/) mantiene actualmente tres controladores diferentes para los dispositivos con chipset Atheros:

*   `madwifi` es un controlador viejo y obsoleto. No está presente en el kernel de Arch desde 2.6.39.1.
*   `ath5k` es el controlador más reciente, que reemplaza al controlador `madwifi`. Actualmente la mejor opción para algunos chipsets, aunque no compatible con todos (ver más abajo).
*   `ath9k` es el más reciente de estos tres controladores, y está pensado para los nuevos chipsets de Atheros. Todos los chips con capacidad 802.11n son compatibles.

Hay algunos otros controladores para algunos dispositivos de Atheros. Véase [Linux Wireless documentation](http://wireless.kernel.org/en/users/Drivers/Atheros#PCI_.2F_PCI-E_.2F_AHB_Drivers) para obtener más detalles.

#### ath5k

Recursos externos:

*   [http://wireless.kernel.org/en/users/Drivers/ath5k](http://wireless.kernel.org/en/users/Drivers/ath5k)
*   [http://wiki.debian.org/ath5k](http://wiki.debian.org/ath5k)

Si encuentra que algunas páginas web se cargan muy lentas, o si el dispositivo no mantiene una dirección IP, pruebe cambiando la encriptación por hardware a software para cargar el módulo `ath5k` con la opción `nohwcrypt=1`. Véase [Kernel modules#Options](/index.php/Kernel_modules#Options "Kernel modules") para obtener más detalles.

Algunos portátiles pueden tener problemas con el LED del wireless que parpadea entre el color rojo y azul. Para resolver este problema, haga:

```
# echo none > /sys/class/leds/ath5k-phy0::tx/trigger
# echo none > /sys/class/leds/ath5k-phy0::rx/trigger

```

Para otras alternativas, consulte [este informe de error](https://bugzilla.redhat.com/show_bug.cgi?id=618232).

#### ath9k

Recursos externos:

*   [http://wireless.kernel.org/en/users/Drivers/ath9k](http://wireless.kernel.org/en/users/Drivers/ath9k)
*   [http://wiki.debian.org/ath9k](http://wiki.debian.org/ath9k)

En el hipotético caso de que tenga problemas de estabilidad, intente probar con el paquete [compat-wireless](http://wireless.kernel.org/en/users/Download). Existe una [ath9k mailing list](https://lists.ath9k.org/mailman/listinfo/ath9k-devel) para dar soporte y debate relacionados con su desarrollo.

##### ASUS

Con algunos portátiles ASUS (probado con ASUS series U32U), podría ayudar añadir `options asus_nb_wmi wapf=1` a `/etc/modprobe.d/asus_nb_wmi.conf` para arreglar problemas relacionados con rfkill.

### Intel

#### ipw2100 and ipw2200

Estos módulos son totalmente compatibles con el kernel, pero requieren firmware adicional. Dependiendo de cuál de los chipsets tenga, [instale](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") o bien [ipw2100-fw](https://www.archlinux.org/packages/?name=ipw2100-fw) o bien [ipw2200-fw](https://www.archlinux.org/packages/?name=ipw2200-fw). Después [recargue](/index.php/Kernel_modules#Manual_module_handling "Kernel modules") el módulo apropiado.

**Sugerencia:** Puede utilizar las siguientes [opciones del módulo](/index.php/Kernel_modules#Setting_module_options "Kernel modules"):

*   La opción `rtap_iface=1` para activar la interfaz radiotap
*   La opción `led=1` para activar un LED frontal que indique cuando la red inalámbrica está o no conectada

#### iwlegacy

[iwlegacy](http://wireless.kernel.org/en/users/Drivers/iwlegacy) es el controlador inalámbrico para los chips wireless 3945 y 4965 de Intel. El firmware se incluye en el paquete [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware).

[udev](/index.php/Udev "Udev") debe cargar el controlador de forma automática, de lo contrario cargue manualmente `iwl3945` o `iwl4965`. Véase [Kernel modules#Loading](/index.php/Kernel_modules#Loading "Kernel modules") para obtener más detalles.

#### iwlwifi

[iwlwifi](http://wireless.kernel.org/en/users/Drivers/iwlwifi) es el controlador inalámbrico para los actuales chips inalámbricos de Intel, como 5100AGN, 5300AGN, y 5350AGN. Véase [full list of supported devices](http://wireless.kernel.org/en/users/Drivers/iwlwifi#Supported_Devices). El firmware está incluido en el paquete [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware).

Si tiene problemas para conectarse a las redes en general, o su calidad de enlace es muy pobre, trate de desactivar 802.11n y activar el cifrado de software:

 `/etc/modprobe.d/iwlwifi.conf` 
```
options iwlwifi 11n_disable=1
options iwlwifi swcrypto=1
```

#### Desactivar el parpadeo del LED

**Nota:** Esto funciona con los controladores `iwlegacy` y `iwlwifi`.

La configuración predeterminada del módulo establece el parpadeo del LED cuando esté en actividad. Algunos usuarios encuentran esto extremadamente molesto. Para que el LED no parpadee cuando el Wi-Fi está activo, puede usar [systemd-tmpfiles](/index.php/Systemd_(Espa%C3%B1ol)#Archivos_temporales "Systemd (Español)"):

 `/etc/tmpfiles.d/phy0-led.conf` 
```
w /sys/class/leds/phy0-led/trigger - - - - phy0radio

```

Ejecute `systemd-tmpfiles --create phy0-led.conf` para que los cambios surtan efecto, o reinicie el sistema.

Para ver todos los posibles valores de referencia para este LED:

```
# cat /sys/class/leds/phy0-led/trigger

```

**Sugerencia:** Si no tiene `/sys/class/leds/phy0-led`, puede tratar de utilizar la [opción del módulo](/index.php/Kernel_modules_(Espa%C3%B1ol)#Configurar_opciones_de_los_m.C3.B3dulos "Kernel modules (Español)") `led_mode="1"`. Debe ser válido tanto para el controlador `iwlwifi` como para `iwlegacy`.

### Broadcom

Véase [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless").

### Otros controladores/dispositivos

#### Tenda w322u

Tratar esta tarjeta Tenda como un dispositivo `rt2870sta`. Véase [#rt2x00](#rt2x00).

#### orinoco

Esto debería ser una parte del paquete del kernel y encontrarse instalado .

Algunos chipsets Orinoco son Hermes II. Puede utilizar el controlador `wlags49_h2_cs` en lugar de `orinoco_cs` y así ganar soporte para WPA. Para usarlo, primero introduzca `orinoco_cs` en [blacklist](/index.php/Kernel_modules#Blacklisting "Kernel modules").

#### prism54

El controlador `p54` está incluido en el kernel, pero tiene que descargar el firmware apropiado para su tarjeta de [este sitio](http://linuxwireless.org/en/users/Drivers/p54#firmware) e instalarlo en el directorio `/usr/lib/firmware`.

**Nota:** También está el obsoleto y antiguo controlador `prism54`, que podría entrar en conflicto con el controlador más reciente (`p54pci` o `p54usb`). Asegúrese de introducir en [blacklist](/index.php/Kernel_modules#Blacklisting "Kernel modules") el controlador `prism54`.

#### ACX100/111

**Advertencia:** Los controladores de estos dispositivos [están rotos](https://mailman.archlinux.org/pipermail/arch-dev-public/2011-June/020669.html) y no funcionan con las versiones más recientes del kernel.

Paquetes: `tiacx` `tiacx-firmware` (suprimidos de los repositorios oficiales y de AUR)

Véase [official wiki](http://sourceforge.net/apps/mediawiki/acx100/index.php?title=Main_Page) para obtener más detalles.

#### zd1211rw

[`zd1211rw`](http://zd1211.wiki.sourceforge.net/) es un controlador para el chipset USB WLAN ZyDAS ZD1211 802.11b/g, y se ha incluido en las últimas versiones del kernel de Linux. Véase [[5]](http://www.linuxwireless.org/en/users/Drivers/zd1211rw/devices) para obtener una lista de los dispositivos compatibles. Basta con [instalar](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") del firmware para el dispositivo , suministrado por el paquete [zd1211-firmware](https://www.archlinux.org/packages/?name=zd1211-firmware).

#### hostap_cs

[Host AP](http://hostap.epitest.fi/) es un controlador de Linux para las tarjetas wireless LAN basadas en el chipset Prism2/2.5/3 de Intersil. El controlador se incluye en el kernel de Linux.

**Nota:** Asegúrese de introducir en [blacklist](/index.php/Kernel_modules#Blacklisting "Kernel modules") el controlador `orinico_cs`, para evitar problemas.

### ndiswrapper

Ndiswrapper es un script que permite el uso de algunos controladores de Windows en Linux. Consulte la lista de compatibilidad [aquí](http://ndiswrapper.sourceforge.net/mediawiki/index.php/List). Necesitará los archivos `.inf` y `.sys` del controlador de Windows. Asegúrese de usar los controladores adecuados para su arquitectura (`x86` vs. `x86_64`).

**Sugerencia:** Si necesita extraer estos archivos de un archivo `*.exe`, puede utilizar [cabextract](https://www.archlinux.org/packages/?name=cabextract).

Siga estos pasos para configurar ndiswrapper.

1\. Instale el controlador en `/etc/ndiswrapper/*`

```
ndiswrapper -i filename.inf

```

2\. Conozca el listado de todos los controladores instalados para ndiswrapper

```
ndiswrapper -l

```

3\. Escriba el siguiente archivo de configuración:

 `/etc/modprobe.d/ndiswrapper.conf` 
```
ndiswrapper -m
depmod -a

```

Ahora la instalación de ndiswrapper está casi terminada, siga las instrucciones de [este artículo](/index.php/Kernel_modules_(Espa%C3%B1ol)#Cargar_m.C3.B3dulos "Kernel modules (Español)") para cargar automáticamente el módulo en el arranque.

Lo importante es asegurarse de que existe ndiswrapper en esta línea, por lo que solo tiene que añadirlo junto a los otros módulos. Para comprobar que ndiswrapper se cargará, escriba:

```
modprobe ndiswrapper
iwconfig

```

y *wlan0* debería mostrarse. Consulte esta página si está teniendo problemas: [Ndiswrapper installation wiki](http://ndiswrapper.sourceforge.net/joomla/index.php?/component/option,com_openwiki/Itemid,33/id,installation/).

### compat-drivers-patched

Los controladores inalámbricos de compat parcheado corrigen el problema «fixed-channel -1», proporcionando, al mismo tiempo, una mejor inyección. Instale el paquete [compat-drivers-patched](https://aur.archlinux.org/packages/compat-drivers-patched/) disponible en [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)").

[compat-drivers-patched](https://aur.archlinux.org/packages/compat-drivers-patched/) no entra en conflicto con ningún otro paquete y los módulos compilados residen en `/usr/lib/modules/*your_kernel_version*/updates`.

Estos drivers parcheados provienen de [Linux Wireless project](http://wireless.kernel.org/) y apoyan muchos de los chips anteriormente mencionados, tales como:

```
ath5k ath9k_htc carl9170 b43 zd1211rw rt2x00 wl1251 wl12xx ath6kl brcm80211

```

Grupos compatibles:

```
atheros ath iwlagn rtl818x rtlwifi wl12xx atlxx bt

```

También es posible compilar un módulo/controlador específico o un grupo de controladores editando el [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), particularmente descomentando la **línea #46**. He aquí un ejemplo de compilación del grupo atheros:

```
scripts/driver-select atheros

```

Por favor, lea el [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") del paquete para cualquier otra posible modificación antes de compilar e instalar.

## Véase también

*   [The Linux Wireless project](http://wireless.kernel.org/)
*   [Aircrack-ng guide on installing drivers](http://aircrack-ng.org/doku.php?id=install_drivers)