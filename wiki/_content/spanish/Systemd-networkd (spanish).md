Related articles

*   [systemd](/index.php/Systemd "Systemd")
*   [systemd-nspawn (Español)](/index.php/Systemd-nspawn_(Espa%C3%B1ol) "Systemd-nspawn (Español)")
*   [Network bridge](/index.php/Network_bridge "Network bridge")
*   [Network configuration](/index.php/Network_configuration "Network configuration")
*   [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")
*   [Category:Network configuration](/index.php/Category:Network_configuration "Category:Network configuration")

*systemd-networkd* es un demonio del sistema que maneja las configuraciones de red. Detecta y configura los dispositivos de red que aparecen; también puede crear dispositivos de red virtuales. Este servicio puede ser especialmente útil para establecer configuraciones complejas de red para un contenedor manejado por [systemd-nspawn (Español)](/index.php/Systemd-nspawn_(Espa%C3%B1ol) "Systemd-nspawn (Español)") o por maquinas virtuales. Además trabaja bien en conecciones simples.

## Contents

*   [1 Uso Básico](#Uso_B.C3.A1sico)
    *   [1.1 Servicios Requeridos e Instalación](#Servicios_Requeridos_e_Instalaci.C3.B3n)
*   [2 Ejemplos de Configuración](#Ejemplos_de_Configuraci.C3.B3n)
    *   [2.1 Adaptador alámbrico usando DHCP](#Adaptador_al.C3.A1mbrico_usando_DHCP)
    *   [2.2 Adaptador alámbrico Usando una IP Estática](#Adaptador_al.C3.A1mbrico_Usando_una_IP_Est.C3.A1tica)
    *   [2.3 Adaptador Inalámbrico](#Adaptador_Inal.C3.A1mbrico)
    *   [2.4 Adaptador Alámbrico e Inalámbrico en la misma máquina](#Adaptador_Al.C3.A1mbrico_e_Inal.C3.A1mbrico_en_la_misma_m.C3.A1quina)
    *   [2.5 IPv6 privacy extensions](#IPv6_privacy_extensions)
*   [3 Archivos de Configuración](#Archivos_de_Configuraci.C3.B3n)
    *   [3.1 Archivos de Red](#Archivos_de_Red)
        *   [3.1.1 Sección [Match]](#Secci.C3.B3n_.5BMatch.5D)
        *   [3.1.2 Sección [Network]](#Secci.C3.B3n_.5BNetwork.5D)
        *   [3.1.3 Sección [Address]](#Secci.C3.B3n_.5BAddress.5D)
        *   [3.1.4 Sección [Route]](#Secci.C3.B3n_.5BRoute.5D)
    *   [3.2 Archivos netdev](#Archivos_netdev)
        *   [3.2.1 Sección [Match]](#Secci.C3.B3n_.5BMatch.5D_2)
        *   [3.2.2 [Netdev] section](#.5BNetdev.5D_section)
    *   [3.3 Archivos Link](#Archivos_Link)
        *   [3.3.1 Sección [Match]](#Secci.C3.B3n_.5BMatch.5D_3)
        *   [3.3.2 Sección [Link]](#Secci.C3.B3n_.5BLink.5D)
*   [4 Uso De Contenedores](#Uso_De_Contenedores)
    *   [4.1 Basic DHCP network](#Basic_DHCP_network)
    *   [4.2 DHCP with two distinct IP](#DHCP_with_two_distinct_IP)
        *   [4.2.1 Bridge interface](#Bridge_interface)
        *   [4.2.2 Bind ethernet to bridge](#Bind_ethernet_to_bridge)
        *   [4.2.3 Bridge network](#Bridge_network)
        *   [4.2.4 Add option to boot the container](#Add_option_to_boot_the_container)
        *   [4.2.5 Result](#Result)
        *   [4.2.6 Notice](#Notice)
    *   [4.3 Static IP network](#Static_IP_network)
*   [5 See also](#See_also)

## Uso Básico

El paquete [systemd](https://www.archlinux.org/packages/?name=systemd) es parte de la instalación de Arch por defecto y contiene todo los archivos necesarios para operar redes cableadas. Adaptadores inalámbricos pueden instalarse por otros servicios, como [wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant"), los cuales serán vistos más adelante en ester articulo.

### Servicios Requeridos e Instalación

Para usar *systemd-networkd*, [iniciar[start]] los siguientes dos servicios y [habilitar[enable]] su ejecución al inicio del sistema:

*   `systemd-networkd.service`
*   `systemd-resolved.service`

**Note:** *systemd-resolved* es realmente requerido sólo su se esoecifica las entradas DNS en los archivos *.network* o si se quiere obtener direcciones DNS desde redes cliente DHCP.

Por compatibilidad con [resolv.conf](/index.php/Resolv.conf "Resolv.conf"), elimina o renombra el archivo existente y crear el siguiente vinculo simbolico:

```
# ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf

```

Opcionalmente, si se desea usar el talón resultor local DNS de *systemd-resolver* (y así usar LLMNR y fundir DNS por interface), reemplazar `dns` con `resolve` en `/etc/nsswitch.conf`:

```
hosts: files **resolve** myhostname

```

Mira [systemd-resolved(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-resolved.8) y [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5) y [Systemd README](https://github.com/systemd/systemd/blob/master/README#L205).

**Note:** Systemd's `resolve` no puede buscar el dominio local cuando sólo se da el hotname, aún cuando `UseDomains=yes` o `Domains=[domain-list]` está presente en el archivo `.network` apropiado, y ese archivo produce el esperado `search [domain-list]` en `resolv.conf`. Si se da ese problema:

*   Cambia a usar nombres de dominios completamente calificados
*   Usa `/etc/hosts` para resolver hostnames
*   Recurrir a usar `dns` de glibc en vez de usar `resolve` de systemd

## Ejemplos de Configuración

Todas las configuraciones estan almasenada como {ic|foo.network}} en `/etc/systemd/network`. Para una lista completa de opciones y orden de procesamiento, consulte [archivos de configuración](#Archivos_de_Configuraci.C3.B3n) y la página man de `systemd.network`.

Systemd/udev automaticamente asigna previsibles, nombres de intefaces de res estables para todo el Ethernet local, interfaces de WLAN y WWAN. Usa `networkctl list` para enlistar los dispositivos en el sistema.

Después de realizar cambios a los archivos de configuración, recarge el demonio de red.

```
# systemctl restart systemd-networkd 

```

**Note:** En el ejemplo de abajo, **enp1s0** es el adaptador de cable y **wlp2s0** es el adaptador inalámbrico. Estos nombres pueden ser diferentes en sistemas distintos.

#### Adaptador alámbrico usando DHCP

 `/etc/systemd/network/*wired*.network` 
```
[Match]
Name=enp1s0

[Network]
DHCP=ipv4

```

#### Adaptador alámbrico Usando una IP Estática

 `/etc/systemd/network/*wired*.network` 
```
[Match]
Name=enp1s0

[Network]
Address=10.1.10.9/24
Gateway=10.1.10.1

```

Vease la página man `systemd.network(5)` para más opciones de red como especificar servidores DNS y direcciones de difución.

#### Adaptador Inalámbrico

A fin de conectarse a una red inalámbrica con *systemd-networkd*, a un adaptador inalámbrico configurado con otro servicio como [wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant") es requerido. En este ejemplo, el archivo de servicio systemd correspondiente que se necesita habilitar es `wpa_supplicant@wlp2s0.service`.

 `/etc/systemd/network/*wireless*.network` 
```
[Match]
Name=wlp2s0

[Network]
DHCP=ipv4

```

Si el adaptador inalámbrico tiene una dirección IP estática, la configuracipon es la misma (excepto por el nombre de la interface) como en un [adaptador alámbrico](#Adaptador_al.C3.A1mbrico_Usando_una_IP_Est.C3.A1tica) .

#### Adaptador Alámbrico e Inalámbrico en la misma máquina

Esta instalación habilitará una IP DHCP para ambas conecciones haciendo uso de la directiva métrica que permite al kernel la desición al vuelo del cual usar. De esta forma, no se observará ningun tiempo de conección cuando la conección alámbrica se desconecte.

La ruta métrica del kernel (misma como configurada con *ip*) decide cual ruta usar para los paquetes salientes, en casos de mcuhas coincidencias. Esto será em el caso de que ambos dispositivos en el sistema tengan conecciones activas. Para romper la cola, el kernel usa la métrica. Si una de las conecciones es terminada, la otro automaticamente gana sin que sea un filtro con nada configurado (transferencias salientes pueden aún no lidiar con esto apropiadamente pero eso es otra capa diferente del OSI).

**Note:** La opción **Metric** es para rutas estáticas mientras la opción **RouteMetric** es para instalaciones que no usan rutas estáticas
 `/etc/systemd/network/*wired*.network` 
```
[Match]
Name=enp1s0

[Network]
DHCP=ipv4

[DHCP]
RouteMetric=10

```
 `/etc/systemd/network/*wireless*.network` 
```
[Match]
Name=wlp2s0

[Network]
DHCP=ipv4

[DHCP]
RouteMetric=20

```

#### IPv6 privacy extensions

Si se usa IPv6 tal vez se querrá además establecer la opción `IPv6PrivacyExtensions` como configuraciones localizadas en `/etc/sysctl.d/40-ipv6.conf` no son reconocidas.

 `/etc/systemd/network/*wireless*.network` 
```
[Match]
Name=wlp2s0

[Network]
DHCP=yes
IPv6PrivacyExtensions=true

[DHCP]
RouteMetric=20

```

## Archivos de Configuración

Los archivos de configuración están localizados en `/usr/lib/systemd/network`, el directorio volatil de ejecución de red `/run/systemd/network` y la carpeta local de administración de red `/etc/systemd/network`. Los archivos en `/etc/systemd/network` tienen la mayor prioridad.

Hay tres tipos de archivos de configuración.

*   Archivos **.network**. Se aplicarán a la configuración de la red por un dispositivo *acoplado*.
*   Archivos **.netdev**. Estos crean un *dispositivo de red virtual* para un entorno *acoplado*.
*   Archivos **.link'*. Cuando un dispositivo de red aparece, [[udev] buscará el primer archivo* .link** *acoplado*.

Todos ellos singuen las siguientes reglas:

*   Si **todas** las condiciones en la sección de `acoplamiento` coincidan, el perfil será activado.
*   Una sección de `acoplamiento` vacia hace que el perfil se aplique de cualquier manera (puede compararse con el comodin `*`).
*   Cada entrada es una clave con la sintaxis `NAME=VALUE`.
*   Todos los archivos de configuración son colectivamente almacenados y procesados en orden léxico, independientemente del directorio donde esté almacenado.
*   Los archivos con nombres identicos se reemplazan con el otro

**Tip:**

*   Para sobreescribir un archivo proporcionado por el sistema en `/usr/lib/systemd/network` de forma permanente (ejemplo incluso despues de actualizar), coloca el archivo con el mismo nombre en `/etc/systemd/network` y un enlace simbolico a `/dev/null`.
*   El comodin `*` se puede usar en `VALOR` (ejemplo `en*`) hará coincidir en cualquier dispositivo Ethernet.
*   Según este [hilo Arch-general](https://mailman.archlinux.org/pipermail/arch-general/2014-March/035381.html), la mejor forma es establecer un contenedor de ajustes de red especificos *dentro del contenedor* con los archivos de configuración de **networkd**.

### Archivos de Red

Estos archivos son dorogodos a establecer variables de configuración de red, en especial a servidores y contenedores.

A continuación se muestra una estructura básica de un archivo `*MiPerfil*.network`:

 `/etc/systemd/network/*MiPerfil*.network` 
```
[Match]
*una lista vertical de claves*

[Network]
*una lista vertical de claves*

[Address]
*una lista vertical de claves*

[Route]
*una lista vertical de claves*

```

#### Sección [Match]

Las claves más comunes son:

*   `Name=` el nombre del dispositivo (ejemplo Br0, enp4s0).
*   `Host=` el nombre de red del ordenador.
*   `Virtualization=` revisa lo que el sistema ejecuta en un entorno virtualizado o no. Una clave `Virtualization=no` sólo se aplicará en el ordenador anfitrion, mientras `Virtualization=yes` se aplica a cualquier contenedor o máquina virtual.

#### Sección [Network]

Las claves más comunes son:

*   `IPForward` por defecto es 0,

lo cual significa que si no se especifica una configuración para {ic|1=IPForward}} en el archivo .network, la interface tendrá el seguimiento IP deshabilitado aún si se habilitó con `sysctl` o escribiendo en `/proc/sys`.

#### Sección [Address]

Las claves más comunes en la sección `[Address]` son:

*   `Address=` es una dirección **IPv4** o **IPv6** estática y su longitud prefija, separada por un `/` (ejemplo

`192.168.1.92/24`). Ésta opción es **obligatoria** a menos que el DHCP sea usado.

#### Sección [Route]

Las claves más comunes en la sección `[Route]` son:

*   {{ic|1=Gateway=} es la dirección o la puerta de acceso del ordenador. ésta opción es **obligatoria** a menos que se use DHCP.

Para una exhaustiva lista de claves, por favor refiérase a`systemd.network(5)`

**Tip:** Se puede poner las claves `Address=` y `Gateway=` en la sección `[Network]` como un atajo si `Address=` contiene sólo una regla de dirección y la sección `Gateway=` contiene sólo una clave Gateway

### Archivos netdev

Estos archivos crean dispositivos virtuales de red.

A continuación se muestra la estructyura básica de un archivo *MiDispositivo*.netdev:

 `/etc/systemd/network/*MiDispositivo*.netdev` 
```
[Match]
*Una lista vertical de claves*

[Netdev]
*Una lista vertical de claves*

```

#### Sección [Match]

Las claves más comunes son `Host=` y`Virtualization=`

#### [Netdev] section

Las claves más comunes son:

*   `Name=` es el nombre de la interface cuando se crea el netdev. Esta opción es **Obligatoria**
*   `Kind=` es el tipo de netdev. Por ejemplo *bridge*, *bond*, *vlan*, *sit*, etc. son soportados. Esta opción es **Obligatoria**

Para una lista exhaustiva lista de claves, por favor refiérase a `systemd.netdev(5)`

### Archivos Link

Estos archivos son una alternativa para personalizar las reglas udev y son aplicados por [udev](/index.php/Udev "Udev") a medida que el dispositivo aparece.

A continuación se muestra la estructura básica de un archivo *MiDispositivo*.link:

 `/etc/systemd/network/*MiDispositivo*.link` 
```
[Match]
*Una lista vertical de claves*

[Link]
*Una lista vertical de claves*

```

La sección `[Match]` determinará si un archivo link dado puede aplicarse a un dispositivo dado, mientras la sección `[Link]` especifica la configuración del dispositivo.

#### Sección [Match]

Las claves más comunes son `MACAddress=`, `Host=` y `Virtualization=`.

`Type=` es el tipo de dispositivo (e.g. vlan)

#### Sección [Link]

Las claves más usadas son:

`MACAddressPolicy=` ya sea *persistente* cuando el hardware tiene una dirección MAC persistente (cómo la mayoría del hardware suele ser) o *random*, lo cual permite darle una dirección MAC aleatoria cuando aparece el dispositivo.

`MACAddress=` suele usarse cuando no se especifica `MACAddressPolicy=`.

**Note:** el sistema `/usr/lib/systemd/network/99-default.link` es generalmente suficiente para la mayoría de los casos básicos

## Uso De Contenedores

El servicio está disponible con [systemd](https://www.archlinux.org/packages/?name=systemd) >= 210\. Se requiere [habilitar e iniciar](/index.php/Systemd_(Espa%C3%B1ol)#Uso_b.C3.A1sico_de_systemctl "Systemd (Español)") el servicio `systemd-networkd.service` en el host y el contenedor

Para propositos de debugging, se recomienda [instalar](/index.php/Install "Install") los paquetes [bridge-utils](https://www.archlinux.org/packages/?name=bridge-utils), [net-tools](https://www.archlinux.org/packages/?name=net-tools) y [iproute2](https://www.archlinux.org/packages/?name=iproute2).

Si se está usando *systemd-nspawn*, se debe modificar el servicio `systemd-nspawn@.service` y añadir la opción boot a la linea `ExecStart`. Para una lista exhaustiva lista de claves, por favor refiérase a [systemd-nspawn(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-nspawn.1)

Note que si se desea tomar ventaja de la configuración automatica DNS desde DHCP, se necesita habilitar `systemd-resolved` y hacer un enlace simbólico `/run/systemd/resolve/resolv.conf` a `/etc/resolv.conf`. Ver `systemd-resolved.service(8)` para más detalles.

**Tip:** Antes de empezar a configurar el contenedor de red, es util:

*   Deshabilitar todos los servicios [netctl](/index.php/Netctl_(Espa%C3%B1ol) "Netctl (Español)"). Esto evitará cualquier conflicto potencial con **systemd-networkd** y hace las configuraciones faciles de probar. Además, hay muchas posibilidades de terminar con pocos o incluso ningun perfil [netctl](/index.php/Netctl_(Espa%C3%B1ol) "Netctl (Español)") activado. el comando `netctl list` imprime una lista de todos los perfiles, con los activados siendo vigilados.
*   Deshabilita el servicio `systemd-nspawn@.service` y use el comando `systemd-nspawn -bnD /path_to/your_container/` como super usuario para iniciar el contenedor. Para desconectar y apagar dentro del contenedor se usa `systemctl poweroff` como super usuario. Una vez que los ajustes de red encajan con los requerimientos, [habilita e inicia](/index.php/Systemd_(Espa%C3%B1ol)#Uso_b.C3.A1sico_de_systemctl "Systemd (Español)") `systemd-nspawn@.service`.
*   Deshabilita el servicio `dhcpcd.service` si está habilitado en el sistema, ya que habilita *dhcpcd* en **todas** las interfaces.
*   Asegurese de no tener perfiles [netctl](/index.php/Netctl_(Espa%C3%B1ol) "Netctl (Español)") activados en el contenedor, y asegurar que `systemd-networkd.service` tanpoco esté habilitado ni iniciado.
*   Asegurese que no tenga ninguna regla [iptables](/index.php/Iptables_(Espa%C3%B1ol) "Iptables (Español)") que pueda bloquear el tráfico.
*   Asegurese que *Reenvio de paquete* esté [habilitado](/index.php/Internet_sharing#Enable_packet_forwarding "Internet sharing") si se desea que los contenedores tengan acceso a internet. Asegurese que el archivo .network no haga accidentalmente apagar el reenvio porque si no se tiene un IPForward=1 en él, systemd-networkd apagará el reenvio en esa interface, incluso si está habilitado globalmente.
*   Cuando en demonio esté iniciado el comandp systemd `networkctl` muestra el estado de las interfaces de red.

**Note:** Para la intalacion descrita a continuación,

*   Se limitará la salida del comando `ip a` para las interfaces interesadas
*   Se asume que el *anfitrion* es el sistema opertivo principal en el que se está y el *contenedor* es una maquina virtual huésped
*   Todos los nombres de interfaces y las direcciones IP son sólo ejemplos.

### Basic DHCP network

This setup will enable a DHCP IP for host and container. In this case, both systems will share the same IP as they share the same interfaces.

 `/etc/systemd/network/*MyDhcp*.network` 
```
[Match]
Name=en*

[Network]
DHCP=ipv4

```

Then, [enable](/index.php/Enable "Enable") and start `systemd-networkd.service` on your container.

You can of course replace `en*` by the full name of your ethernet device given by the output of the `ip link` command.

*   on host and container:

 `$ ip a` 
```
2: enp7s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 14:da:e9:b5:7a:88 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.72/24 brd 192.168.1.255 scope global enp7s0
       valid_lft forever preferred_lft forever
    inet6 fe80::16da:e9ff:feb5:7a88/64 scope link 
       valid_lft forever preferred_lft forever

```

By default hostname received from the DHCP server will be used as the transient hostname.

To change it add `UseHostname=false` in section `[DHCPv4]`

 `/etc/systemd/network/*MyDhcp*.network` 
```
[DHCPv4]
UseHostname=false

```

If you did not want configure a DNS in `/etc/resolv.conf` and want to rely on DHCP for setting it up, you need to [enable](/index.php/Enable "Enable") `systemd-resolved.service` and symlink `/run/systemd/resolve/resolv.conf` to `/etc/resolv.conf`

```
# ln -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf

```

See `systemd-resolved.service(8)` for more details.

### DHCP with two distinct IP

#### Bridge interface

Create a virtual bridge interface

 `/etc/systemd/network/*MyBridge*.netdev` 
```
[NetDev]
Name=br0
Kind=bridge

```

On host and container:

 `$ ip a` 
```
3: br0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default 
    link/ether ae:bd:35:ea:0c:c9 brd ff:ff:ff:ff:ff:ff

```

Note that the interface br0 is listed but is DOWN.

#### Bind ethernet to bridge

Modify the `/etc/systemd/network/*MyDhcp*.network` to remove the DHCP, as the bridge requires an interface to bind to with no IP, and add a key to bind this device to br0\. Let us change its name to a more relevant one.

 `/etc/systemd/network/*MyEth*.network` 
```
[Match]
Name=en*

[Network]
Bridge=br0

```

#### Bridge network

Create a network profile for the Bridge

 `/etc/systemd/network/*MyBridge*.network` 
```
[Match]
Name=br0

[Network]
DHCP=ipv4

```

#### Add option to boot the container

As we want to give a separate IP for host and container, we need to *Disconnect* networking of the container from the host. To do this, add this option `--network-bridge=br0` to your container boot command.

```
# systemd-nspawn --network-bridge=br0 -bD /path_to/my_container

```

#### Result

*   on host

 `$ ip a` 
```
3: br0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 14:da:e9:b5:7a:88 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.87/24 brd 192.168.1.255 scope global br0
       valid_lft forever preferred_lft forever
    inet6 fe80::16da:e9ff:feb5:7a88/64 scope link 
       valid_lft forever preferred_lft forever
6: vb-*MyContainer*: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master br0 state UP group default qlen 1000
    link/ether d2:7c:97:97:37:25 brd ff:ff:ff:ff:ff:ff
    inet6 fe80::d07c:97ff:fe97:3725/64 scope link 
       valid_lft forever preferred_lft forever

```

*   on container

 `$ ip a` 
```
2: host0: <BROADCAST,MULTICAST,ALLMULTI,AUTOMEDIA,NOTRAILERS,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 5e:96:85:83:a8:5d brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.73/24 brd 192.168.1.255 scope global host0
       valid_lft forever preferred_lft forever
    inet6 fe80::5c96:85ff:fe83:a85d/64 scope link 
       valid_lft forever preferred_lft forever

```

#### Notice

*   we have now one IP address for Br0 on the host, and one for host0 in the container
*   two new interfaces have appeared: `vb-*MyContainer*` in the host and `host0` in the container. This comes as a result of the `--network-bridge=br0` option. This option *implies* another option, `--network-veth`. This means a *virtual Ethernet link* has been created between host and container.
*   the DHCP address on `host0` comes from the system `/usr/lib/systemd/network/80-container-host0.network` file.
*   on host

 `$ brctl show` 
```
bridge name	bridge id		STP enabled	interfaces
br0		8000.14dae9b57a88	no		enp7s0
							vb-*MyContainer*

```

the above command output confirms we have a bridge with two interfaces binded to.

*   on host

 `$ ip route` 
```
default via 192.168.1.254 dev br0 
192.168.1.0/24 dev br0  proto kernel  scope link  src 192.168.1.87

```

*   on container

 `$ ip route` 
```
default via 192.168.1.254 dev host0 
192.168.1.0/24 dev host0  proto kernel  scope link  src 192.168.1.73

```

the above command outputs confirm we have activated `br0` and `host0` interfaces with an IP address and Gateway 192.168.1.254\. The gateway address has been automatically grabbed by *systemd-networkd*

 `$ cat /run/systemd/resolve/resolv.conf` 
```
nameserver 192.168.1.254

```

### Static IP network

Setting a static IP for each device can be helpful in case of deployed web services (e.g FTP, http, SSH). Each device will keep the same MAC address across reboots if your system `/usr/lib/systemd/network/99-default.link` file has the `MACAddressPolicy=persistent` option (it has by default). Thus, you will easily route any service on your Gateway to the desired device. First, we shall get rid of the system `/usr/lib/systemd/network/80-container-host0.network` file. To do it in a permanent way (e.g even after upgrades), do the following on container. This will mask the file `/usr/lib/systemd/network/80-container-host0.network` since files of the same name in `/etc/systemd/network` take priority over `/usr/lib/systemd/network`.

```
# ln -sf /dev/null /etc/systemd/network/80-container-host0.network

```

Then, [enable and start](/index.php/Systemd#Basic_systemctl_usage "Systemd") `systemd-networkd` on your container.

The needed configuration files:

*   on host

```
/etc/systemd/network/*MyBridge*.netdev
/etc/systemd/network/*MyEth*.network

```

A modified *MyBridge*.network

 `/etc/systemd/network/*MyBridge*.network` 
```
[Match]
Name=br0

[Network]
DNS=192.168.1.254
Address=192.168.1.87/24
Gateway=192.168.1.254

```

*   on container

 `/etc/systemd/network/*MyVeth*.network` 
```
[Match]
Name=host0

[Network]
DNS=192.168.1.254
Address=192.168.1.94/24
Gateway=192.168.1.254

```

## See also

*   [systemd.networkd man page](http://www.freedesktop.org/software/systemd/man/systemd-networkd.service.html)
*   [Tom Gundersen, main systemd-networkd developer, G+ home page](https://plus.google.com/u/0/+TomGundersen/posts)
*   [Tom Gundersen posts on Core OS blog](https://coreos.com/blog/intro-to-systemd-networkd/)
*   [How to set up systemd-networkd with wpa_supplicant](https://bbs.archlinux.org/viewtopic.php?pid=1393759#p1393759) (WonderWoofy's walkthrough on Arch forums)