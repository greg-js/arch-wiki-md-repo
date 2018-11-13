Artículos relacionados

*   [Jumbo frames](/index.php/Jumbo_frames "Jumbo frames")
*   [Firewalls (Español)](/index.php/Firewalls_(Espa%C3%B1ol) "Firewalls (Español)")
*   [Wireless Setup (Español)](/index.php/Wireless_Setup_(Espa%C3%B1ol) "Wireless Setup (Español)")
*   [List of applications#Network managers](/index.php/List_of_applications#Network_managers "List of applications")

Esta página explica cómo configurar una conexión cableada (**wired**) a una red. Si necesita configurar una conexión inalámbrica (**wireless**) consulte la página de [Wireless Setup](/index.php/Wireless_Setup_(Espa%C3%B1ol) "Wireless Setup (Español)").

## Contents

*   [1 Comprobar la conexión](#Comprobar_la_conexión)
*   [2 Establecer el nombre del equipo](#Establecer_el_nombre_del_equipo)
*   [3 Controlador del dispositivo](#Controlador_del_dispositivo)
    *   [3.1 Comprobar el estado del controlador](#Comprobar_el_estado_del_controlador)
    *   [3.2 Cargar el módulo del dispositivo](#Cargar_el_módulo_del_dispositivo)
*   [4 Interfaces de red](#Interfaces_de_red)
    *   [4.1 Nombres de los dispositivos](#Nombres_de_los_dispositivos)
        *   [4.1.1 Cambiar el nombre de dispositivo](#Cambiar_el_nombre_de_dispositivo)
    *   [4.2 Establecer el MTU del dispositivo y la longitud de la cola](#Establecer_el_MTU_del_dispositivo_y_la_longitud_de_la_cola)
    *   [4.3 Conocer el nombre actual de los dispositivos](#Conocer_el_nombre_actual_de_los_dispositivos)
    *   [4.4 Activación y desactivación de las interfaces de red](#Activación_y_desactivación_de_las_interfaces_de_red)
*   [5 Configurar la dirección IP](#Configurar_la_dirección_IP)
    *   [5.1 Dirección IP dinámica](#Dirección_IP_dinámica)
        *   [5.1.1 Ejecutar manualmente el demonio DHCP Client](#Ejecutar_manualmente_el_demonio_DHCP_Client)
        *   [5.1.2 Ejecutar DHCP durante el arranque](#Ejecutar_DHCP_durante_el_arranque)
        *   [5.1.3 Enrutamiento estático DHCP](#Enrutamiento_estático_DHCP)
    *   [5.2 Dirección IP estática](#Dirección_IP_estática)
        *   [5.2.1 Asignación manual](#Asignación_manual)
        *   [5.2.2 Conexión manual al arranque usando systemd](#Conexión_manual_al_arranque_usando_systemd)
        *   [5.2.3 Calcular direcciones](#Calcular_direcciones)
*   [6 Cargar la configuración](#Cargar_la_configuración)
*   [7 Ajustes adicionales](#Ajustes_adicionales)
    *   [7.1 ifplugd para portátiles](#ifplugd_para_portátiles)
    *   [7.2 Bonding o LAG](#Bonding_o_LAG)
    *   [7.3 Aliasing de direcciones IP](#Aliasing_de_direcciones_IP)
        *   [7.3.1 Ejemplo](#Ejemplo)
    *   [7.4 Cambio de direcciones MAC/hardware](#Cambio_de_direcciones_MAC/hardware)
    *   [7.5 Compartir Internet](#Compartir_Internet)
    *   [7.6 Configuración del router](#Configuración_del_router)
*   [8 Solución de problemas](#Solución_de_problemas)
    *   [8.1 Intercambiando ordenadores con cable modem](#Intercambiando_ordenadores_con_cable_modem)
    *   [8.2 El problema con el TCP Window Scaling](#El_problema_con_el_TCP_Window_Scaling)
        *   [8.2.1 ¿Cómo diagnosticar este problema?](#¿Cómo_diagnosticar_este_problema?)
        *   [8.2.2 ¿Cómo arreglarlo? (El método equivocado)](#¿Cómo_arreglarlo?_(El_método_equivocado))
        *   [8.2.3 ¿Cómo arreglarlo? (El método correcto)](#¿Cómo_arreglarlo?_(El_método_correcto))
        *   [8.2.4 ¿Cómo arreglarlo? (El método óptimo)](#¿Cómo_arreglarlo?_(El_método_óptimo))
        *   [8.2.5 Información adicional sobre este problema](#Información_adicional_sobre_este_problema)
    *   [8.3 Problema con Realtek: sin Link / WOL](#Problema_con_Realtek:_sin_Link_/_WOL)
        *   [8.3.1 Método 1 - Restaurar el controlador de Windows](#Método_1_-_Restaurar_el_controlador_de_Windows)
        *   [8.3.2 Método 2 - Habilitar WOL en el controlador de Windows](#Método_2_-_Habilitar_WOL_en_el_controlador_de_Windows)
        *   [8.3.3 Método 3 - Nuevo driver de Realtek para Linux](#Método_3_-_Nuevo_driver_de_Realtek_para_Linux)
        *   [8.3.4 Method 4 - Activar *LAN Boot ROM* en la BIOS/CMOS](#Method_4_-_Activar_LAN_Boot_ROM_en_la_BIOS/CMOS)
    *   [8.4 Problemas de DNS con DLink G604T/DLink G502T](#Problemas_de_DNS_con_DLink_G604T/DLink_G502T)
        *   [8.4.1 Cómo diagnosticar el problema](#Cómo_diagnosticar_el_problema)
        *   [8.4.2 Cómo arreglarlo](#Cómo_arreglarlo)
        *   [8.4.3 Más información](#Más_información)
    *   [8.5 Comprobar problema de DHCP mediante la liberación de la primera IP](#Comprobar_problema_de_DHCP_mediante_la_liberación_de_la_primera_IP)
    *   [8.6 Sin eth0 con Atheros AR8161](#Sin_eth0_con_Atheros_AR8161)
    *   [8.7 Sin eth0 con Atheros AR9485](#Sin_eth0_con_Atheros_AR9485)
    *   [8.8 Sin transporte/sin conexión después de la suspensión](#Sin_transporte/sin_conexión_después_de_la_suspensión)
    *   [8.9 Broadcom BCM57780](#Broadcom_BCM57780)

## Comprobar la conexión

**Nota:** Si recibe un error como `ping: icmp open socket: Operation not permitted` al ejecutar ping, pruebe a reinstalar el paquete `iputils`.

Muchas veces, la instalación de base habrá creado una configuración de red correctamente. Para comprobar si esto es así, utilice la siguiente orden:

**Nota:** La opción `-c 3` establece que se ejecute ping tres veces. Vea [ping(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ping.8) para obtener más información
. `$ ping -c 3 www.google.com` 
```
PING www.l.google.com (74.125.224.146) 56(84) bytes of data.
64 bytes from 74.125.224.146: icmp_req=1 ttl=50 time=437 ms
64 bytes from 74.125.224.146: icmp_req=2 ttl=50 time=385 ms
64 bytes from 74.125.224.146: icmp_req=3 ttl=50 time=298 ms

--- www.l.google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 1999ms
rtt min/avg/max/mdev = 298.107/373.642/437.202/57.415 ms
```

Si funciona, se puede personalizar la configuración mediante las opciones siguientes.

Si la orden anterior informa de errores de hosts desconocidos, significa que el equipo no pudo resolver este nombre de dominio. Esto podría estar relacionado con su proveedor de servicios o el router/gateway. Se puede intentar hacer ping a una dirección IP estática para comprobar que el equipo tiene acceso a Internet.

 `$ ping -c 3 8.8.8.8` 
```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_req=1 ttl=53 time=52.9 ms
64 bytes from 8.8.8.8: icmp_req=2 ttl=53 time=72.5 ms
64 bytes from 8.8.8.8: icmp_req=3 ttl=53 time=70.6 ms

--- 8.8.8.8 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 52.975/65.375/72.543/8.803 ms
```

**Nota:** `8.8.8.8` es una dirección estática que es fácil de recordar. Es la dirección del servidor DNS primario de Google, por lo que se puede considerar fiable, y no es bloqueado generalmente por los sistemas de filtrado de contenidos y servidores proxy.

Si es capaz de hacer ping a esta dirección, es posible que desee añadir este servidor de nombres a su archivo `/etc/resolv.conf`.

## Establecer el nombre del equipo

El [hostname](https://en.wikipedia.org/wiki/es:Nombre_de_equipo "wikipedia:es:Nombre de equipo") es un nombre único creado para identificar una máquina en una red: está configurado en `/etc/hostname`. El archivo puede contener el nombre de dominio del sistema, si los hubiere.

Para establecer el nombre del equipo, escriba:

```
# hostnamectl set-hostname **elnombredemiequipo**

```

Esto pondrá **elnombredemiequipo** en `/etc/hostname`.

Consulte [hostname(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.5) y [hostnamectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostnamectl.1) para más detalles.

**Nota:**

*   `hostnamectl` da soporte técnico a FQDNs
*   Ya no es necesario editar `/etc/hosts`, [systemd](https://www.archlinux.org/packages/?name=systemd) proporcionará la resolución del nombre del equipo, y viene instalado en todos los sistemas por defecto.

Para establecer el nombre del equipo temporalmente (hasta que reinicie), use la orden `hostname` del paquete [inetutils](https://www.archlinux.org/packages/?name=inetutils):

```
# hostname *elnombredemiequipo*

```

## Controlador del dispositivo

### Comprobar el estado del controlador

[udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)") debería detectar el módulo del adaptador de red ([NIC](https://en.wikipedia.org/wiki/es:Tarjeta_de_red "wikipedia:es:Tarjeta de red")) y cargarlo automáticamente al arranque. Compruebe la entrada «Ethernet controller» (o similar) que proporciona la salida `lspci -v`. Cabe decir que los módulos del kernel contienen el controlador del propio dispositivo de red. Por ejemplo:

 `$ lspci -v` 
```
 02:00.0 Ethernet controller: Attansic Technology Corp. L1 Gigabit Ethernet Adapter (rev b0)
 	...
 	Kernel driver in use: atl1
 	Kernel modules: atl1
```

A continuación, compruebe que se ha cargado el controlador a través de `dmesg | grep *nombre_del_módulo*`. Por ejemplo:

```
$ dmesg | grep atl1
   ...
   atl1 0000:02:00.0: eth0 link is up 100 Mbps full duplex

```

Sáltese la siguiente sección, si el controlador se ha cargado con éxito. De lo contrario, tendrá que saber qué módulo es necesario para su modelo en particular.

### Cargar el módulo del dispositivo

Busque en Google para localizar el correcto módulo/controlador de su chipset. Algunos módulos comunes son `8139too` para las tarjetas con chipset Realtek, o `sis900` para las tarjetas con chipset SiS. Una vez que sepa qué módulo utilizar, puede [cargarlos manualmente](/index.php/Kernel_modules_(Espa%C3%B1ol)#Manejar_m.C3.B3dulos_manualmente "Kernel modules (Español)"). Si obtiene un error diciendole que no se encontró el módulo, es posible que el controlador no esté incluido en el kernel de Arch. Puede buscarlo en el [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)") por el nombre del módulo.

Si udev no detecta y carga el módulo adecuado de forma automática durante el arranque, consulte [este artículo](/index.php/Kernel_modules_(Espa%C3%B1ol)#Cargar_m.C3.B3dulos "Kernel modules (Español)").

## Interfaces de red

### Nombres de los dispositivos

Para las placas base que tengan tarjetas de red integradas, es importante contar con el nombre fijo del dispositivo. Muchos problemas de configuración son causados ​​por los nombres cambiantes de las interfaces.

[Udev](/index.php/Udev "Udev") es responsable de qué nombre se dé a cada dispositivo. Systemd v197 introdujo los [Nombres Predecibles de las Interfaces de Red](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames), que asigna automáticamente nombres estables a los dispositivos de red. Los nombres de las interfaces estarán precedidos por en (ethernet), wl (WLAN), o ww (WWAN) seguidos de un identificador generado automáticamente, creando una entrada como `enp0s25`.

Este comportamiento puede ser desactivado mediante la adición de un enlace simbólico:

```
# ln -s /dev/null /etc/udev/rules.d/80-net-name-slot.rules

```

Los usuarios que actualicen desde una versión anterior de systemd tendrán un archivo de reglas en blanco creado automáticamente. Así que, si desea utilizar los nombres permanentes de los dispositivos, basta con borrar dicho archivo.

**Sugerencia:** Puede ejecutar las órdenes `ip link` o `ls /sys/class/net` para conocer la lista de todas las interfaces disponibles.

**Nota:** Al cambiar el esquema de nomenclatura de la interfaz, no se olvide de actualizar todos los archivos de configuración relacionados con la red y los archivos de unidad de systemd personalizados para reflejar el cambio. Específicamente, si tiene [perfiles estáticos de netctl](/index.php/Netctl_(Espa%C3%B1ol)#Método_básico "Netctl (Español)") activados, ejecute `netctl reenable *perfil*` para actualizar el archivo de servicios generado.

#### Cambiar el nombre de dispositivo

Puede cambiar el nombre del dispositivo al definir manualmente el nombre con una regla udev. Por ejemplo:

 `/etc/udev/rules.d/10-network.rules` 
```
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="aa:bb:cc:dd:ee:ff", NAME="net1"
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="ff:ee:dd:cc:bb:aa", NAME="net0"
```

Algunas consideraciones:

*   Para obtener la dirección MAC de cada tarjeta, utilice esta orden: `cat /sys/class/net/**device-name**/address`
*   Asegúrese de utilizar los valores hexadecimales en minúsculas en las reglas de udev. No use mayúsculas.

Si tiene una tarjeta con dirección MAC dinámica, puede utilizar DEVPATH por ejemplo

 `/etc/udev/rules.d/10-network.rules` 
```
SUBSYSTEM=="net", DEVPATH=="/devices/platform/wemac.*", NAME="int"

```

**Nota:** Al elegir los nombres permanentes **se debe evitar el uso de nombres con el formato "eth*X*" y "wlan*X*"**, ya que esto puede conducir a conflictos entre el kernel y udev durante el arranque. En cambio, es mejor utilizar nombres de interfaces que no sean utilizados por el kernel por defecto, por ejemplo: `net0`, `net1`, `wifi0`, `wifi1`. Para más detalles, consulte la documentación de [systemd](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames).

### Establecer el MTU del dispositivo y la longitud de la cola

Puede cambiar el MTU del dispositivo y longitud de la cola, definiéndolos manualmente con una regla de udev. Por ejemplo:

 `/etc/udev/rules.d/10-network.rules`  `ACTION=="add", SUBSYSTEM=="net", KERNEL=="wl*", ATTR{mtu}="1480", ATTR{tx_queue_len}="2000"` 

### Conocer el nombre actual de los dispositivos

Los nombres actuales de NIC se pueden encontrar a través de sysfs:

 `$ ls /sys/class/net`  `lo eth0 eth1 firewire0` 

### Activación y desactivación de las interfaces de red

Puede activar o desactivar interfaces de red usando:

```
# ip link set eth0 up
# ip link set eth0 down

```

Para comprobar el resultado:

 `$ ip addr show dev eth0` 
```
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP qlen 1000
[...]
```

## Configurar la dirección IP

Tenemos dos opciones: la asignación dinámica de la dirección usando [DHCP](https://en.wikipedia.org/wiki/es:Dynamic_Host_Configuration_Protocol "wikipedia:es:Dynamic Host Configuration Protocol") o una dirección «estática» que no cambia.

### Dirección IP dinámica

#### Ejecutar manualmente el demonio DHCP Client

Tenga en cuenta que `dhcpcd` no es `dhcpd`.

 `$ dhcpcd eth0` 
```
 dhcpcd: version 5.1.1 starting
 dhcpcd: eth0: broadcasting for a lease
 ...
 dhcpcd: eth0: leased 192.168.1.70 for 86400 seconds
```

Y ahora, `ip addr show dev eth0` debe mostrar su dirección inet.

Para algunos usuarios, `dhclient` (con el paquete [dhclient](https://www.archlinux.org/packages/?name=dhclient)) ha funcionado cuando `dhcpcd` ha fallado.

#### Ejecutar DHCP durante el arranque

Si solo desea utilizar DHCP para la conexión Ethernet, puede utilizar `dhcpcd@.service` (proporcionado por el paquete [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd)).

Para activar DHCP para `eth0`, solo tiene que utilizar:

```
# systemctl start dhcpcd@eth0

```

Puede activar el servicio para que se inicie automáticamente en el arranque con:

```
# systemctl enable dhcpcd@eth0

```

Si el servicio dhcpd se inicia antes que el módulo de la tarjeta de red ([FS#30235](https://bugs.archlinux.org/task/30235)), agregue manualmente la tarjeta de red a `/etc/modules-load.d/*.conf`. Por ejemplo, si necesita cargar tarjetas Realtek `r8169`, cree:

 `/etc/modules-load.d/realtek.conf`  `r8169` 
**Sugerencia:** Para saber qué módulos son utilizados por la tarjeta de red, utilice `lspci -k`.

Si utiliza DHCP y **no** quiere que se asignen automáticamente servidores DNS cada vez que se inicie su red, agregue la siguiente línea a la última sección de `dhcpcd.conf`:

 `/etc/dhcpcd.conf`  `nohook resolv.conf` 

Además, si tiene una conexión de red con DHCPv4 que filtra los ID Clientes basado en direcciones MAC, es posible que tenga que cambiar la siguiente línea:

 `/etc/dhcpcd.conf` 
```
# Use the same DUID + IAID as set in DHCPv6 for DHCPv4 Client ID as per RFC4361\. 
duid

```

a:

 `/etc/dhcpcd.conf` 
```
# Use the hardware address of the interface for the Client ID (DHCPv4).
clientid

```

De lo contrario, no podrá obtener una dirección IP desde el servidor DHCP dado que no podrá leer correctamente el ID Cliente [estilo DHCPv6](https://en.wikipedia.org/wiki/DHCPv6 "wikipedia:DHCPv6"). Véase [RFC 4361](http://tools.ietf.org/html/rfc4361) para más información.

Para evitar que `dhcpcd` añada servidores de nombres de dominio a `/etc/resolve.conf`, use el parámetro `nooption`:

 `/etc/dhcpcd.conf`  `nooption domain_name_servers` 

A continuación, añada su propio servidor de nombre DNS a `/etc/resolv.conf`.

Se puede utilizar el paquete [openresolv](https://www.archlinux.org/packages/?name=openresolv) si desea controlar varios procesos diferentes mediante `/etc/resolv.conf` (por ejemplo, [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) y un cliente VPN). No es necesaria ninguna configuración adicional de [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) para usar [openresolv](https://www.archlinux.org/packages/?name=openresolv).

#### Enrutamiento estático DHCP

Si necesita añadir un cliente adjunto de enrutamiento estático, entonces cree un hook-script nuevo para dhcpcd en `/lib/dhcpcd/dhcpcd-hooks`. El ejemplo muestra un nuevo hook-script que añade un enrutamiento estático a una subred vpn sobre 10.11.12.0/24 a través de una máquina de puerta de enlace en 192.168.192.5:

 `/lib/dhcpcd/dhcpcd-hooks/40-vpnroute` 
```
ip route add 10.11.12.0/24 via 192.168.192.5

```

El prefacio 40 significa que es el final de hook-script para ejecutar cuando se inicia dhcpcd.

### Dirección IP estática

Hay varias razones por las que se puede desear asignar direcciones IP estáticas a su red. Por ejemplo, se puede obtener un cierto grado de previsibilidad en las direcciones permanentes, o puede querer no tener disponible un servidor DHCP.

**Nota:** Si comparte su conexión a Internet desde una máquina Windows sin un router, asegúrese de utilizar direcciones IP estáticas en ambos equipos para evitar problemas de LAN.

Necesitará:

*   La dirección IP estática
*   La [máscara de subred](https://en.wikipedia.org/wiki/es:Subred "wikipedia:es:Subred")
*   La [dirección Broadcast](https://en.wikipedia.org/wiki/Broadcast_address "wikipedia:Broadcast address")
*   Direcciones IP del [Gateway](https://en.wikipedia.org/wiki/es:Puerta_de_enlace_predeterminada "wikipedia:es:Puerta de enlace predeterminada")

Si está ejecutando una red privada, es seguro usar las direcciones IP del tipo 192.168.*.*, una máscara de subred 255.255.255.0 y una dirección de broadcast 192.168.*.255\. La puerta de entrada suele ser 192.168.*.1 o 192.168.*.254\.

#### Asignación manual

Se puede asignar una dirección IP estática desde la consola:

```
# ip addr add <IP address>/<subnet mask> dev <interface>

```

Por ejemplo:

```
# ip addr add 192.168.1.2/24 dev eth0

```

**Nota:** La máscara de subred se especifica tambien con [notación CIDR](https://en.wikipedia.org/wiki/CIDR_notation "wikipedia:CIDR notation").

Para conocer más opciones, vea [ip(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip.7).

Añada su puerta de entrada (*gateway*) de esta manera:

```
# ip route add default via <dirección IP gateway predeterminada>

```

Por ejemplo:

```
# ip route add default via 192.168.1.1

```

Si le sale el mensaje de error *«No such process»*, significa que tiene que ejecutar `ip link set dev eth0 up` como root.

#### Conexión manual al arranque usando systemd

En primer lugar crear el archivo de configuración de servicio de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"), sustituyendo `<interface>` con el nombre de la interfaz adecuada:

 `/etc/conf.d/network@<interface>` 
```
address=192.168.0.15
netmask=24
broadcast=192.168.0.255
gateway=192.168.0.1

```

Cree un archivo de unidad de systemd:

 `/etc/systemd/system/network@.service` 
```
[Unit]
Description=Network connectivity (%i)
Wants=network.target
Before=network.target
BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

[Service]
Type=oneshot
RemainAfterExit=yes
EnvironmentFile=/etc/conf.d/network@%i

ExecStart=/usr/bin/ip link set dev %i up
ExecStart=/usr/bin/ip addr add ${address}/${netmask} broadcast ${broadcast} dev %i
ExecStart=/usr/bin/ip route add default via ${gateway}

ExecStop=/usr/bin/ip addr flush dev %i
ExecStop=/usr/bin/ip link set dev %i down

[Install]
WantedBy=multi-user.target

```

Active la unidad e iníciela, proporcionando el nombre de la interfaz:

```
# systemctl enable network@eth0.service
# systemctl start network@eth0.service

```

#### Calcular direcciones

Se puede utilizar la orden `ipcalc`, proporcionado por el paquete [ipcalc](https://www.archlinux.org/packages/?name=ipcalc), para el calcular la IP broadcast, red, máscara de red y rangos de host para las configuraciones más avanzadas. Por ejemplo, es posible utilizar ethernet a través de firewire para conectar un PC con Windows para Arch. Para la seguridad y organización de la red, puede colocarlos en su propia red, configurar la máscara de red y broadcast de manera que sean las dos únicas máquinas en ella. Para mostrar las direcciones de máscara de red y broadcast, puede utilizar ipcalc, proporcionando la IP arch del firewire nic 10.66.66.1, y especificando ipcalc, debe crear una red de solo dos hosts.

 `$ ipcalc -nb 10.66.66.1 -s 1` 
```
Address:   10.66.66.1

Netmask:   255.255.255.252 = 30
Network:   10.66.66.0/30
HostMin:   10.66.66.1
HostMax:   10.66.66.2
Broadcast: 10.66.66.3
Hosts/Net: 2                     Class A, Private Internet
```

## Cargar la configuración

Para probar cualquier configuración reinicie el ordenador, o como root, ejecute:

```
# systemctl restart dhcpcd@eth0

```

Pruebe a hacer ping a su gateway, servidor DNS, proveedor de ISP y otros sitios de Internet, en ese orden, para detectar cualquier problema de conexión en el camino, como en este ejemplo:

```
$ ping -c 3 www.google.com

```

## Ajustes adicionales

### ifplugd para portátiles

**Sugerencia:** [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) proporciona la misma función tras instalarse sin necesidad de configuración adicional.

[ifplugd](https://www.archlinux.org/packages/?name=ifplugd) disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)") es un demonio que configura automáticamente el dispositivo Ethernet, cuando un cable de red está enchufado y automáticamente se desconfigura si el cable se retira. Esto es útil en portátiles con los adaptadores de red integrados, ya que solo se va a configurar la interfaz cuando un cable está realmente conectado. Otro utilidad es cuando solo tiene que reiniciar la red, pero no desea reiniciar el equipo o utilizar la shell.

Por defecto, está configurado para trabajar para el dispositivo `eth0`. Esta y otras configuraciones, como demoras, se pueden establecer en `/etc/ifplugd/ifplugd.conf`.

**Nota:** El paquete [Netctl](/index.php/Netctl_(Espa%C3%B1ol) "Netctl (Español)") incluye `netctl-ifplugd@.service`, en su defecto, puede utilizar `ifplugd@.service` del paquete [ifplugd](https://www.archlinux.org/packages/?name=ifplugd). Utilice por ejemplo `systemctl enable ifplugd@eth0.service`.

### Bonding o LAG

Véase [Netctl (Español)#Bonding](/index.php/Netctl_(Espa%C3%B1ol)#Bonding "Netctl (Español)")

### Aliasing de direcciones IP

El *aliasing* IP es el proceso de agregar más de una dirección IP a una interfaz de red. Con esto, un nodo en una red puede tener varias conexiones a una red, cada uno sirviendo a un propósito diferente. Los usos típicos son el alojamiento virtual de servidores Web y FTP o servidores de reorganización sin tener que actualizar cualquier otra máquina (esto es especialmente útil para los servidores de nombres).

#### Ejemplo

Necesitará [netcfg](https://aur.archlinux.org/packages/netcfg/) disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

Prepare la configuración:

 `/etc/netctl/mynetwork` 
```
Connection='ethernet'
Description='Five different addresses on the same NIC.'
Interface='eth0'
IP='static'
Address=('192.168.1.10' '192.168.178.11' '192.168.1.12' '192.168.1.13' '192.168.1.14' '192.168.1.15')
Gateway='192.168.1.1'
DNS=('192.168.1.1')
Donain=
```

Ejecute simplemente:

```
$ netctl start mynetwork

```

### Cambio de direcciones MAC/hardware

Véase [MAC address spoofing](/index.php/MAC_address_spoofing "MAC address spoofing").

### Compartir Internet

Véase [Internet sharing](/index.php/Internet_sharing "Internet sharing").

### Configuración del router

Véase [Router](/index.php/Router "Router").

## Solución de problemas

### Intercambiando ordenadores con cable modem

La mayoría de los ISPs domésticos estan configurados para reconocer solo una PC cliente por la dirección MAC de su interfaz de red. Una vez que el cable modem aprendió la dirección MAC de la primera PC que se comunica con el, no responderá a otra dirección MAC de ninguna manera. Entonces si cambias la PC por otra (o por un router), la nueva PC (o router) no funcionará con el cable modem, porque la nueva PC (o router) tiene una dirección MAC distinta a la anterior. Para resetear el cable modem y que este pueda reconocer la nueva PC (o router), debes apagarlo y volverlo a encender. Una vez que el modem se ha reiniciado y se ha conectado completamente (las luces de indicación encendidas), reinicia el nuevo PC (o router) para que haga una petición DHCP, o haz que lo haga manualmente.

Si este método no funciona, tendrá que clonar la dirección MAC de la máquina original. Véase también [Cambiar direcciones MAC/hardware](#Cambio_de_direcciones_MAC/hardware).

### El problema con el TCP Window Scaling

Los paquetes TCP contienen un valor «window» en sus cabeceras para indicar cuantos datos envió el otro host. Este valor es representado con solamente 16 bits, dado que el tamaño del «window» es de, como mucho, 64Kb. Los paquetes TCP son guardados en el cache por un tiempo (deben ser reordenados), y como la memoria era limitada, un host podía llenarla fácilmente.

En 1992, cuando se empezó a disponer de cada vez más memoria, se escribió [RFC 1323](http://www.faqs.org/rfcs/rfc1323.html) para mejorar la situación: Window Scaling. El valor «window», enviado en todos los paquetes, serán modificados por un factor Scale definido una vez, al inicio de la conexión.

Ese valor Scale de 8-bits permite al valor window ser 32 veces más grande que sus iniciales 64Kb.

Parece que algunos routers y firewalls dañados cambian el valor Scale a 0, lo que causa problemas entre los hosts.

El Kernel Linux 2.6.17 introdujo un nuevo esquema de calculación, generando valores Scale más altos, haciendo mas notable los problemas de los router y los firewalls dañados.

La conexión resultante, en el mejor de los casos, es muy lenta o núla.

#### ¿Cómo diagnosticar este problema?

En algúnos casos no podrás usar conexiones TCP (HTTP, FTP, ...) para nada, y en otros no podrás comunicarte con algunos hosts (muy pocos).

**Alerta**: La salida de `dmesg` esta bien, los logs estan limpios y la salida de `ifconfig` es normal — entonces, en realidad todo esta bien.

Si no puedes acceder a ningún sitio, pero puedes hacer ping a algúnos hosts, hay posibilidades de que estes pasando por este problema: el ping usa el protocolo ICMP y no es afectado por los problemas TCP.

Podrías probar usando WireShark. Puede que veas comunicaciones ICMP y UDP bien realizadas, pero problemas con las conexiones TCP (solo con hosts extranjeros).

#### ¿Cómo arreglarlo? (El método equivocado)

Para arreglarlo por el mal camino, puedes cambiar el valor tcp_rmem, donde se realiza la calculación del Scale Factor. Si bien debería funcionar para la mayoría de los hosts, no es seguro, especialmente para los que son muy distantes.

```
echo "4096 87380 174760" > /proc/sys/net/ipv4/tcp_rmem

```

O podrías remover alguno de tus módulos RAM.

#### ¿Cómo arreglarlo? (El método correcto)

Simple: Deshabilita Window Scaling. Si bien el Window Scaling es una buena característica TCP, puede resultar mala, especialmente si no puedes reparar tu router dañado. Hay varias formas de deshabilitar Window Scaling, y parece que la mejor (la que funcionará en la mayoría de los kernels) es añadir las siguientes líneas a `/etc/sysctl.d/99-disable_window_scaling.conf` (véase también [sysctl](/index.php/Sysctl "Sysctl"))

```
net.ipv4.tcp_window_scaling = 0

```

#### ¿Cómo arreglarlo? (El método óptimo)

Este problema es causado por un router/firewall dañado. Cámbielos.

#### Información adicional sobre este problema

Esta sección se basa en un artículo de LWN [TCP window scaling and broken router](http://lwn.net/Articles/92727/) (ingles) y un artículo de Kernel Trap: [Window Scaling on the Internet](http://kerneltrap.org/node/6723) (en ingles).

También hay varios temas similares en LKML.

### Problema con Realtek: sin Link / WOL

Usuarios de una NIC (tarjetas / y onboard) basada en Realtek 8168 8169 8101 8111 pueden pasar por un problema donde NIC parece estar deshabilitado desde el boot y la luz Link no se enciende. Esto ocurre generalmente en un sistema dual boot donde esta instalado un Windows. Parece que la causa es usar los drivers oficiales de Realtek (de después de Mayo del 2007) en Windows. Estos nuevos drivers deshabilitan la característica Wake-On-Lan, deshabilitando el NIC al momento de apagar Windows, y dejándolo deshabilitado hasta el próximo arranque. Sabrás si tienes este problema si ves que la luz del Link permanece apagada hasta que carga Windows. Lo normal sería que la luz de Link este siempre encendida mientras el sistema este funcionando. Este problema también afectará a otros sistemas operativos con drivers no actualizados. Aquí, algunas maneras de arreglar este problema:

#### Método 1 - Restaurar el controlador de Windows

Puedes volver a la versión brindada por Microsoft del driver NIC (si esta disponible), o volver a la versión anterior/instalar un driver oficial Realtek anterior a Mayo del 2007 (tal vez lo encuentre en el CD que le dieron con su hardware).

#### Método 2 - Habilitar WOL en el controlador de Windows

Probablemente la mejor solución (y la más rápida) es cambiar esta configuración en el driver de Windows. De esta forma se solucionaría para todos los SOs. En Windows, en el administrador de dispositivos, encuentra tu adaptador Realtek y dale doble click. En la pestaña «Advanced» cambie «Wake-on-LAN after shutdown» por «Enable» (habilitar).

```
En Windows XP (ejemplo)
 Haga clic en Mi PC
--> Pestaña Hardware
  --> Administrador de dispositivos
    --> Adaptadores de red
      --> «Doble clic» en Realtek ...
        --> Pestaña Avanzado
          --> Wake-On-Lan después de apagado
            --> Habilitar

```

**Nota:** Los controladores Realtek más recientes para Windows (probado con *Realtek 8111/8169 LAN Driver v5.708.1030.2008*, de fecha 2009/01/22, disponible en GIGABYTE) pueden referirse a esta opción de forma diferente, como *Shutdown Wake-On-LAN --> Enable*. Parece que cambiar a `Disable` no tiene efecto (lo notará al observar que la luz de enlace todavía se apaga, al apagar Windows). Una solución bastante burda consiste en arrancar Windows e, inmediatamente, resetear el sistema (realizar un reinicio/apagado sin miramientos), lo que no da al controlador de Windows la posibilidad de desactivar la LAN. La luz de enlace permanecerá encendida y el adaptador LAN se mantendrán accesible después del POST (*Power On Self Test*) -es decir, hasta que arranque de nuevo con Windows y lo apague correctamente-.

#### Método 3 - Nuevo driver de Realtek para Linux

Los drivers nuevos de estas tarjetas para Linux pueden encontrarse en el sitio de Realtek (no probado aunque se cree que también resuelve el problema).

#### Method 4 - Activar *LAN Boot ROM* en la BIOS/CMOS

Parece que el ajuste *Integrated Peripherals → Onboard LAN Boot ROM → Enabled* en BIOS/CMOS del chip Realtek reactiva LAN en el sistema al reiniciar, a pesar de que el controlador de Windows lo desactive en el apagado del sistema operativo.

**Nota:** Esto fue probado con éxito varias veces con la placa base GIGABYTE GA-G31M-ES2L con la liberación de la versión F8 de la BIOS el 05/02/. YMMV.

### Problemas de DNS con DLink G604T/DLink G502T

Los usuarios con un router DLink G604T/DLink G502T, usando DHCP con un firmware v2.00+ (normalmente los usuarios con firmware AUS) pueden tener problemas con algunos programas que no resuelven el DNS. Uno de estos programas es, desafortunadamente, pacman. El problema es, básicamente, que el router, en ciertas situaciones, no envía correctamente el DNS a DHCP, que provoca que los programas traten de conectarse a los servidores con una dirección IP de 1.0.0.0 y fallan al dar un error conexión caducada.

#### Cómo diagnosticar el problema

La mejor manera de diagnosticar el problema es usar Firefox/Konqueror/links/seamonkey y habilitar wget para pacman. Si se trata de una nueva instalación de Arch Linux, entonces es posible que desee considerar la posibilidad de instalar `links` a través del live CD.

En primer lugar, habilite wget para pacman (ya que nos da información sobre pacman cuando se descargan paquetes) Abra `/etc/pacman.conf` con su editor favorito y descomente la siguiente línea (quite el signo # si está presente)

```
XferCommand=/usr/bin/wget --passive-ftp -c -O %o %u

```

Al tiempo que edita `/etc/pacman.conf`, compruebe el mirror por defecto que utiliza pacman para descargar los paquetes.

Ahora abra el mirror predeterminado en el navegador de Internet para ver si el mirror realmente funciona. Si funciona, entonces ejecute `pacman -Syy` (también puede elegir otro mirror que funcione y ajustarlo como predeterminado en pacman). Si obtiene algo similar a lo siguiente (preste atención a 1.0.0.0),

```
ftp://mirror.pacific.net.au/linux/archlinux/extra/os/i686/extra.db.tar.gz
           => '/var/lib/pacman/community.db.tar.gz.part'
Resolving mirror.pacific.net.au... 1.0.0.0

```

entonces lo más probable es que tenga este problema. El resultado 1.0.0.0 significa que es incapaz de resolver el DNS, por lo que es preciso añadirlo a `/etc/resolv.conf`.

#### Cómo arreglarlo

Básicamente lo que hay que hacer es agregar manualmente los servidores DNS al archivo `/etc/resolv.conf`. El problema es que DHCP elimina automáticamente y sustituye dicho archivo en el arranque, por lo que tenemos que editar `/etc/conf.d/dhcpcd` y cambiar los flags para que DHCP deje de hacer esto.

Cuando abra `/etc/conf.d/dhcpcd`, debería ver algo parecido a lo siguiente:

```
DHCPCD_ARGS="-t 30 -h $HOSTNAME"

```

Añada el flag -R a los argumentos, por ejemplo,

```
DHCPCD_ARGS="-R -t 30 -h $HOSTNAME"

```

**Nota:** Si está usando [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) >= 4.0.2, el flag `-R` ha quedado en desuso. Por favor, consulte el apartado [Configurar la dirección IP](#Configurar_la_dirección_IP) para obtener información sobre cómo utilizar un archivo `/etc/resolv.conf` personalizado.

Guarde y cierre el archivo; ahora abra `/etc/resolv.conf`. Debería ver un nombre de servidor único (*nameserver*) (lo más probable 10.1.1.1). Esta es la puerta de entrada (*gateway*) al router, a la cual es necesario conectarse con el fin de obtener los servidores DNS del ISP. Pegue la dirección IP en el navegador y acceda al propio router. Vaya a la sección DNS, donde debería ver una dirección IP en el campo *Primary DNS Server* («Servidor DNS primario»); cópielo y péguelo como un nombre de servidor (*nameserver*) **ARRIBA** de la puerta de entrada (*gateway*) actual.

Por ejemplo, si `/etc/resolv.conf` muestra una línea similar a esta:

```
nameserver 10.1.1.1

```

Y el servidor DNS principal es 211.29.132.12, a continuación, cambie `/etc/resolv.conf`, de modo que quede así:

```
nameserver 211.29.132.12
nameserver 10.1.1.1

```

Ahora reinicie el demonio network haciendo `rc.d restart network` y, seguidamente, ejecutando `pacman -Syy`. Si se sincroniza correctamente con el servidor, entonces el problema está resuelto.

#### Más información

Este es el foro de whirlpool (Australian ISP community) que trata y le da la misma solución al problema:

[http://forums.whirlpool.net.au/forum-replies-archive.cfm/461625.html](http://forums.whirlpool.net.au/forum-replies-archive.cfm/461625.html)

### Comprobar problema de DHCP mediante la liberación de la primera IP

Este problema se puede producir cuando el DHCP obtiene una asignación de IP equivocada. Por ejemplo, cuando dos routers están unidos entre sí a través de VPN. El router que está conectado al propio ordenador por VPN puede asignar una dirección IP. Para solucionarlo, en una consola, como root, libere la dirección IP:

```
# dhcpcd -k

```

A continuación, solicite una nueva:

```
# dhcpcd

```

Tal vez tenga que ejecutar las dos órdenes varias veces.

### Sin eth0 con Atheros AR8161

Con la tarjeta Atheros AR8161 Gigabit Ethernet, la conexión ethernet no funciona después de la instalación (con el soporte de instalación de enero de 2013). El módulo «alx» necesita ser cargado, pero no está presente.

El controloador de [compat-wireless](http://linuxwireless.org/en/users/Download/stable/#compat-wireless_stable_releases) (que debería ser [compat-drives](https://backports.wiki.kernel.org/index.php/Releases) desde linux 3.7) necesita ser instalado. Necesita la versión del firmware con **pc** en el nombre del archivo para que funcionen los controladores de red ethernet.

```
 $ wget [http://www.orbit-lab.org/kernel/compat-wireless-3-stable/v3.6/compat-wireless-3.6.8-1-snpc.tar.bz2](http://www.orbit-lab.org/kernel/compat-wireless-3-stable/v3.6/compat-wireless-3.6.8-1-snpc.tar.bz2)
 $ tar xjf compat-wireless-3.6.8-1-snpc.tar.bz2
 $ cd compat-wireless-3.6.8-1-snpc
 $ ./scripts/driver-select alx
 $ make
 $ sudo make install
 $ sudo modprobe alx

```

Los controladores alx no han sido agregados al kernel Linux debido a diversas cuestiones y la compatibilidad entre las diferentes versiones del núcleo ha sido irregula, por lo que para conseguir un mejor soporte siga la [lista de correo](http://lists.infradead.org/mailman/listinfo/unified-drivers) y la [página de alx](http://www.linuxfoundation.org/collaborate/workgroups/networking/alx) a fin de encontrar una solución final para alx.

Alternativamente, puede utilizar el paquete de AUR para los [controladores compat](https://aur.archlinux.org/packages/compat-drivers-patched/).

### Sin eth0 con Atheros AR9485

La conexión ethernet (eth0) para Atheros AR9485 no está funcionando una vez instalada (con el soporte de instalación de marzo de 2013). La solución para que funcione es instalar el paquete [compat-drivers-patched](https://aur.archlinux.org/packages/compat-drivers-patched/) desde AUR.

### Sin transporte/sin conexión después de la suspensión

Después de suspender la RAM nos encontramos sin ​​conexión aunque el cable de red esté enchufado. Esto puede ser causado por la administración de energía PCI. Cuál es la salida de:

```
# ip link show eth0

```

si la línea contiene "NO-CARRIER" a pesar de que hay un cable conectado a su puerto eth0, es posible que el dispositivo se haya autosuspendido y la característica de detección de medios no funciona. Para solucionar esto, primero es necesario encontrar la direccione PCI del controlador ethernet con:

```
# lspci

```

debe ser similar a esto:

```
...
00:19.0 Ethernet controller: Intel Corporation 82577LM Gigabit Network Connection (rev 06)
...

```

En este caso la dirección es 00:19.0. Ahora comprobaremos el estado de PM del dispositivo mediante la emisión de:

```
# cat "/sys/bus/pci/devices/0000:00:19.0/power/control"

```

sustituyendo 00:19.0 con la dirección obtenida de lspci. Si en la salida se lee "auto", puede tratar de abrir el dispositivo después de la suspensión con:

```
# echo on > "/sys/bus/pci/devices/0000:00:19.0/power/control"

```

No olvide sustituir la dirección otra vez.

**Nota:** Esto parece ser un error en el kernel 3.8.4.1: [discusión del foro.](https://bbs.archlinux.org/viewtopic.php?id=159837&p=2) Otra solución podría ser [este camino.](https://lkml.org/lkml/2013/1/18/147) Mientras tanto, lo anterior es una solución adecuada.

### Broadcom BCM57780

Este chipset de Broadcom, a veces, no se comporta bien, a menos que se especifique el orden en que los módulos se deben cargar. Los módulos son `broadcom` y `tg3`, el antiguo necesita ser cargado primero.

Los siguientes pasos deben ayudar si el equipo tiene este chipset:

```
$ lspci | grep Ethernet
02:00.0 Ethernet controller: Broadcom Corporation NetLink BCM57780 Gigabit Ethernet PCIe (rev 01)

```

Si su red cableada no está funcionando bien, trate de desconectar el cable y luego hacer lo siguiente (como root):

```
# modprobe -r tg3
# modprobe broadcom
# modprobe tg3

```

Ahora conecte el cable de red. Si esto resuelve el problema puede hacerlo permanente, añadiendo `broadcom` y `tg3` (en este orden) en la matriz `MODULES` del archivo `/etc/mkinitcpio.conf`:

```
MODULES=".. broadcom tg3 .."

```

A continuación, reconstruya initramfs:

```
# mkinitcpio -p linux

```

**Nota:** Estos métodos pueden funcionar para otros chipsets, como BCM57760.