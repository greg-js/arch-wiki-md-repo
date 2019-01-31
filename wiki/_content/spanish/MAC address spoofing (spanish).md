**Estado de la traducción**
Este artículo es una traducción de [MAC address spoofing](/index.php/MAC_address_spoofing "MAC address spoofing"), revisada por última vez el **2019-01-30**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=MAC_address_spoofing&diff=0&oldid=563556) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Este artículo proporciona varios métodos para falsificar una dirección de control de acceso al medio (MAC).

## Contents

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
        *   [2.3.2 Enabling service](#Enabling_service)
    *   [2.4 netctl interfaces](#netctl_interfaces)
    *   [2.5 NetworkManager](#NetworkManager)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Connection to DHCPv4 network fails](#Connection_to_DHCPv4_network_fails)
*   [4 See also](#See_also)

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

[systemd-networkd](/index.php/Systemd-networkd_(Espa%C3%B1ol) "Systemd-networkd (Español)") soporta la falsificación de direcciones MAC a través de [archivos link](/index.php/Systemd-networkd_(Espa%C3%B1ol)#Archivos_Link "Systemd-networkd (Español)") (véase [systemd.link(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.link.5) para los detalles).

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

Below you find two examples of [systemd](/index.php/Systemd "Systemd") units to change a MAC address at boot, one sets a static MAC using *ip* and one uses *macchanger* to assign a random MAC address. The systemd `network-pre.target` is used to ensure the MAC is changed before a network manager like [Netctl](/index.php/Netctl "Netctl") or [NetworkManager](/index.php/NetworkManager "NetworkManager"), [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") or [dhcpcd](/index.php/Dhcpcd "Dhcpcd") service starts.

##### iproute2

[systemd](/index.php/Systemd "Systemd") unit setting a predefined MAC address:

 `/etc/systemd/system/macspoof@.service` 
```
[Unit]
Description=MAC Address Change %I
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

[systemd](/index.php/Systemd "Systemd") unit setting a random address while preserving the original NIC vendor bytes. Ensure that [macchanger](https://www.archlinux.org/packages/?name=macchanger) is [installed](/index.php/Pacman#Installing_specific_packages "Pacman"):

 `/etc/systemd/system/macspoof@.service` 
```
[Unit]
Description=macchanger on %I
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

A full random address can be set using the `-r` option, see [#macchanger](#macchanger).

#### Enabling service

Append the desired network interface to the service name (e.g. `eth0`) and [enable](/index.php/Enable "Enable") the service (e.g. `macspoof@eth0.service`).

Reboot, or stop and start the prerequisite and requisite services in the proper order. If you are in control of your network, verify that the spoofed MAC has been picked up by your router by examining the static, or DHCP address tables within the router.

### netctl interfaces

You can use a [netctl hook](/index.php/Netctl#Using_hooks "Netctl") to run a command each time a netctl profile is re-/started for a specific network interface. Replace `*interface*` accordingly:

 `/etc/netctl/interfaces/*interface*` 
```
#!/usr/bin/env sh
/usr/bin/macchanger -r *interface*
```

Make the script executable:

```
chmod +x /etc/netctl/interfaces/*interface*

```

Source: [akendo.eu](https://blog.akendo.eu/archlinuxrandom-mac-address-for-new-wireless-connections/)

### NetworkManager

See [NetworkManager#Configuring MAC address randomization](/index.php/NetworkManager#Configuring_MAC_address_randomization "NetworkManager").

## Troubleshooting

### Connection to DHCPv4 network fails

If you cannot connect to a DHCPv4 network and you are using dhcpcd, which is the default for NetworkManager, you might need to [modify the dhcpcd configuration](/index.php/Dhcpcd#Client_ID "Dhcpcd") to obtain a lease.

## See also

*   [Wikipedia:MAC spoofing](https://en.wikipedia.org/wiki/MAC_spoofing "wikipedia:MAC spoofing")
*   [Macchanger GitHub page](https://github.com/alobbs/macchanger)
*   [Article on DebianAdmin](http://www.debianadmin.com/change-your-network-card-mac-media-access-control-address.html) with more *macchanger* options