**Estado de la traducción**
Este artículo es una traducción de [MAC address spoofing](/index.php/MAC_address_spoofing "MAC address spoofing"), revisada por última vez el **2020-02-12**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=MAC_address_spoofing&diff=0&oldid=588944) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Este artículo proporciona varios métodos para falsificar una dirección de control de acceso al medio (MAC).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Manualmente](#Manualmente)
    *   [1.1 iproute2](#iproute2)
    *   [1.2 macchanger](#macchanger)
*   [2 Automáticamente](#Automáticamente)
    *   [2.1 systemd-networkd](#systemd-networkd)
    *   [2.2 systemd-udevd](#systemd-udevd)
    *   [2.3 Unidades systemd](#Unidades_systemd)
        *   [2.3.1 Crear la unidad](#Crear_la_unidad)
            *   [2.3.1.1 iproute2](#iproute2_2)
            *   [2.3.1.2 macchanger](#macchanger_2)
        *   [2.3.2 Activar el servicio](#Activar_el_servicio)
    *   [2.4 Interfaces netctl](#Interfaces_netctl)
    *   [2.5 NetworkManager](#NetworkManager)
    *   [2.6 wpa_supplicant](#wpa_supplicant)
    *   [2.7 iwd](#iwd)
*   [3 Solución de problemas](#Solución_de_problemas)
    *   [3.1 La conexión a la red DHCPv4 falla](#La_conexión_a_la_red_DHCPv4_falla)
*   [4 Véase también](#Véase_también)

## Manualmente

Hay dos métodos para falsificar una dirección MAC: [instalando](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") y configurando ya sea [iproute2](https://www.archlinux.org/packages/?name=iproute2) o [macchanger](https://www.archlinux.org/packages/?name=macchanger). Ambos se describen a continuación.

### iproute2

Primero, puede verificar su dirección MAC actual con el comando:

```
# ip link show *interfaz*

```

donde `*interfaz*` es el nombre de su [interfaz de red](/index.php/Network_interface_(Espa%C3%B1ol) "Network interface (Español)").

La sección que nos interesa en este momento es la que tiene "link/ether" seguido de un número de 6 bytes. Probablemente se verá algo como esto:

```
link/ether 00:1d:98:5a:d1:3a

```

El primer paso para falsificar la dirección MAC es desactivar la interfaz de red. Se puede lograr con el comando:

```
# ip link set dev *interfaz* down

```

A continuación, falsificaremos nuestra MAC. Cualquier valor hexadecimal servirá, pero algunas redes pueden configurarse para negarse a asignar direcciones IP a un cliente cuya MAC no coincida con ninguno de los proveedores conocidos. Por lo tanto, a menos que controle las redes a las que se está conectando, utilice el prefijo MAC de cualquier proveedor real (básicamente, los primeros tres bytes) y utilice valores aleatorios para los siguientes tres bytes. Para obtener más información, véase [Wikipedia:es:Identificador único de organización](https://en.wikipedia.org/wiki/es:Identificador_%C3%BAnico_de_organizaci%C3%B3n "wikipedia:es:Identificador único de organización").

Para cambiar la MAC, necesitamos ejecutar el comando:

```
# ip link set dev *interfaz* address *XX:XX:XX:XX:XX:XX*

```

Donde cualquier valor de 6 bytes será suficiente para `*XX:XX:XX:XX:XX:XX*`.

El último paso es volver a activar la interfaz de red. Esto se puede lograr ejecutando el comando:

```
# ip link set dev *interfaz* up

```

Si desea verificar que su MAC ha sido falsificada, simplemente ejecute nuevamente `ip link show *interfaz*` y verifique el valor para 'link/ether'. Si funcionó, 'link/ether' debería ser la dirección a la que decidió cambiarla.

### macchanger

Otro método utiliza [macchanger](https://www.archlinux.org/packages/?name=macchanger) (también conocido como el Cambiador de MAC de GNU). Proporciona una variedad de funciones, como cambiar la dirección para que coincida con un determinado proveedor o al azar.

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [macchanger](https://www.archlinux.org/packages/?name=macchanger).

La falsificación se realiza por interfaz, especifique el nombre del [interfaz de red](/index.php/Network_interface_(Espa%C3%B1ol) "Network interface (Español)") como `*interfaz*` en cada uno de los siguientes comandos.

La dirección MAC se puede falsificar con una dirección completamente aleatoria:

```
# macchanger -r *interfaz*

```

Para hacer aleatorio solo los bytes específicos de dispositivo de la dirección MAC actual (es decir, de modo que si la dirección MAC se verificara se registraría como si fuera del mismo proveedor), ejecutaría el comando:

```
# macchanger -e *interfaz*

```

Para cambiar la dirección MAC a un valor específico, debe ejecutar:

```
# macchanger --mac=*XX:XX:XX:XX:XX:XX* *interfaz*

```

Donde `*XX:XX:XX:XX:XX:XX*` es la MAC a la que desea cambiar.

Finalmente, para devolver la dirección MAC a su valor de hardware original y permanente:

```
# macchanger -p *interfaz*

```

**Nota:** Un dispositivo no puede estar en uso (conectado de ninguna manera o con su interfaz levantada) mientras se cambia la dirección MAC.

## Automáticamente

### systemd-networkd

[systemd-networkd](/index.php/Systemd-networkd_(Espa%C3%B1ol) "Systemd-networkd (Español)") soporta la falsificación de direcciones MAC a través de [archivos link](/index.php/Systemd-networkd_(Espa%C3%B1ol)#Archivos_link "Systemd-networkd (Español)") (véase [systemd.link(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.link.5) para los detalles).

Para establecer una dirección MAC estática falsificada:

 `/etc/systemd/network/00-default.link` 
```
[Match]
MACAddress=*MAC original*

[Link]
MACAddress=*MAC falsificada*
NamePolicy=kernel database onboard slot path
```

Para hacer aleatoria la dirección MAC en cada arranque, establezca `MACAddressPolicy=random` en lugar de `MACAddress=*MAC falsificada*`.

### systemd-udevd

[Udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)") le permite realizar la falsificación de la dirección MAC mediante la creación de reglas udev. Utilice el atributo `address` para que coincida con el dispositivo correcto por su dirección MAC original y cámbielo utilizando la orden *ip*:

 `/etc/udev/rules.d/75-mac-spoof.rules`  `ACTION=="add", SUBSYSTEM=="net", ATTR{address}=="XX:XX:XX:XX:XX:XX", RUN+="/usr/bin/ip link set dev $name address YY:YY:YY:YY:YY:YY"` 

Donde `XX:XX:XX:XX:XX:XX` es la dirección MAC original e `YY:YY:YY:YY:YY:YY` es la nueva.

### Unidades systemd

#### Crear la unidad

A continuación, encontrará dos ejemplos de unidades [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") para cambiar una dirección MAC durante el arranque, uno configura una MAC estática utilizando *ip* y el otro utiliza *macchanger* para asignar una dirección MAC aleatoria. El `network-pre.target` de systemd se utiliza para asegurar que la MAC se cambie antes que un gestor de red como [Netctl](/index.php/Netctl_(Espa%C3%B1ol) "Netctl (Español)") o [NetworkManager](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)"), comience el servicio [systemd-networkd](/index.php/Systemd-networkd_(Espa%C3%B1ol) "Systemd-networkd (Español)") o [dhcpcd](/index.php/Dhcpcd_(Espa%C3%B1ol) "Dhcpcd (Español)").

##### iproute2

La unidad [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") configura una dirección MAC predefinida:

 `/etc/systemd/system/macspoof@.service` 
```
[Unit]
Description=Cambio de dirección MAC %I
Wants=network-pre.target
Before=network-pre.target
BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

[Service]
Type=oneshot
ExecStart=/usr/bin/ip link set dev %i address 36:aa:88:c8:75:3a
ExecStart=/usr/bin/ip link set dev %i up

[Install]
WantedBy=multi-user.target

```

##### macchanger

La unidad [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") establece una dirección aleatoria mientras se conservan los bytes originales del proveedor NIC. Asegúrese de que [macchanger](https://www.archlinux.org/packages/?name=macchanger) está [instalado](/index.php/Pacman_(Espa%C3%B1ol)#Instalar_paquetes_específicos "Pacman (Español)"):

 `/etc/systemd/system/macspoof@.service` 
```
[Unit]
Description=macchanger en %I
Wants=network-pre.target
Before=network-pre.target
BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

[Service]
ExecStart=/usr/bin/macchanger -e %I
Type=oneshot

[Install]
WantedBy=multi-user.target

```

Se puede establecer una dirección completamente aleatoria utilizando la opción `-r`, véase [#macchanger](#macchanger).

#### Activar el servicio

Añada la interfaz de red deseada al nombre del servicio (por ejemplo `eth0`) y [active](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") el servicio (por ejemplo `macspoof@eth0.service`).

Reinicie, o detenga e inicie los servicios requeridos en el orden correcto. Si tiene el control de su red, verifique que el enrutador haya recogido la MAC falsificada mediante el examen de las tablas de direcciones DHCP o estáticas dentro del enrutador.

### Interfaces netctl

Puede utilizar un [hook de netctl](/index.php/Netctl#Using_hooks "Netctl") para ejecutar una orden cada vez que un perfil netctl es re-/iniciado para una interfaz de red específica. Reemplace `*interfaz*` en consecuencia:

 `/etc/netctl/interfaces/*interfaz*` 
```
#!/usr/bin/env sh
/usr/bin/macchanger -r *interfaz*
```

Haga el script ejecutable:

```
chmod +x /etc/netctl/interfaces/*interfaz*

```

Fuente: [akendo.eu](https://blog.akendo.eu/archlinuxrandom-mac-address-for-new-wireless-connections/)

### NetworkManager

Véase [NetworkManager#Configuring MAC address randomization](/index.php/NetworkManager#Configuring_MAC_address_randomization "NetworkManager").

### wpa_supplicant

wpa_supplicant puede utilizar una dirección MAC aleatoria para cada conexión ESS (AP) (véase [[1]](https://w1.fi/cgit/hostap/plain/wpa_supplicant/wpa_supplicant.conf) for details).

Añada esto a su configuración:

 `/etc/wpa_supplicant/wpa_supplicant-wlan0.conf` 
```
mac_addr=1
preassoc_mac_addr=1
gas_rand_mac_addr=1
```

### iwd

Para aleatorizar la dirección MAC cuando se inicia iwd (véase [iwd.config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/iwd.config.5) para más detalles):

 `/etc/iwd/main.conf` 
```
[General]
AddressRandomization=once
```

## Solución de problemas

### La conexión a la red DHCPv4 falla

Si no puede conectarse a una red DHCPv4 y está utilizando dhcpcd, que es el predeterminado para NetworkManager, es posible que deba [modificar la configuración dhcpcd](/index.php/Dhcpcd_(Espa%C3%B1ol)#ID_del_cliente "Dhcpcd (Español)") para obtener un arrendamiento *(lease)*.

## Véase también

*   [Wikipedia:es:MAC spoofing](https://en.wikipedia.org/wiki/es:MAC_spoofing "wikipedia:es:MAC spoofing")
*   [Página en GitHub de Macchanger](https://github.com/alobbs/macchanger)
*   [Artículo en DebianAdmin](http://www.debianadmin.com/change-your-network-card-mac-media-access-control-address.html) con más opciones de *macchanger*