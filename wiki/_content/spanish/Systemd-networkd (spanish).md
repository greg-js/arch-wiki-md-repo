**Estado de la traducción**
Este artículo es una traducción de [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd"), revisada por última vez el **2019-10-27**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Systemd-networkd&diff=0&oldid=584270) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)")
*   [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved")
*   [systemd-nspawn (Español)](/index.php/Systemd-nspawn_(Espa%C3%B1ol) "Systemd-nspawn (Español)")
*   [Network bridge](/index.php/Network_bridge "Network bridge")
*   [Network configuration (Español)](/index.php/Network_configuration_(Espa%C3%B1ol) "Network configuration (Español)")
*   [Wireless network configuration (Español)](/index.php/Wireless_network_configuration_(Espa%C3%B1ol) "Wireless network configuration (Español)")
*   [Category:Network configuration (Español)](/index.php/Category:Network_configuration_(Espa%C3%B1ol) "Category:Network configuration (Español)")

*systemd-networkd* es un demonio del sistema que gestiona las configuraciones de red. Detecta y configura los dispositivos de red a medida que aparecen; también puede crear dispositivos de red virtuales. Este servicio puede ser especialmente útil para establecer configuraciones complejas de red para un contenedor gestionado por [systemd-nspawn (Español)](/index.php/Systemd-nspawn_(Espa%C3%B1ol) "Systemd-nspawn (Español)") o por maquinas virtuales. Además trabaja bien en conexiones simples.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Utilización básica](#Utilización_básica)
    *   [1.1 Servicios requeridos y configuración](#Servicios_requeridos_y_configuración)
    *   [1.2 Ejemplos de configuración](#Ejemplos_de_configuración)
        *   [1.2.1 Adaptador cableado utilizando DHCP](#Adaptador_cableado_utilizando_DHCP)
        *   [1.2.2 Adaptador cableado utilizando una IP estática](#Adaptador_cableado_utilizando_una_IP_estática)
        *   [1.2.3 Adaptador inalámbrico](#Adaptador_inalámbrico)
        *   [1.2.4 Adaptadores cableados e inalámbricos en la misma máquina](#Adaptadores_cableados_e_inalámbricos_en_la_misma_máquina)
        *   [1.2.5 Renombrar una interfaz](#Renombrar_una_interfaz)
*   [2 Archivos de configuración](#Archivos_de_configuración)
    *   [2.1 Archivos network](#Archivos_network)
        *   [2.1.1 [Match]](#[Match])
        *   [2.1.2 [Link]](#[Link])
        *   [2.1.3 [Network]](#[Network])
        *   [2.1.4 [Address]](#[Address])
        *   [2.1.5 [Route]](#[Route])
        *   [2.1.6 [DHCP]](#[DHCP])
    *   [2.2 Archivos netdev](#Archivos_netdev)
        *   [2.2.1 Sección [Match]](#Sección_[Match])
        *   [2.2.2 Sección [NetDev]](#Sección_[NetDev])
    *   [2.3 Archivos link](#Archivos_link)
        *   [2.3.1 Sección [Match]](#Sección_[Match]_2)
        *   [2.3.2 Sección [Link]](#Sección_[Link])
*   [3 Utilización de contenedores](#Utilización_de_contenedores)
    *   [3.1 Red básica con DHCP](#Red_básica_con_DHCP)
    *   [3.2 DHCP con dos IP distintas](#DHCP_con_dos_IP_distintas)
        *   [3.2.1 Interfaz del puente de red](#Interfaz_del_puente_de_red)
        *   [3.2.2 Vincular ethernet al puente de red](#Vincular_ethernet_al_puente_de_red)
        *   [3.2.3 Conectar el puente de red](#Conectar_el_puente_de_red)
        *   [3.2.4 Añadir opción para arrancar el contenedor](#Añadir_opción_para_arrancar_el_contenedor)
        *   [3.2.5 Resultado](#Resultado)
        *   [3.2.6 Aviso](#Aviso)
    *   [3.3 Red IP estática](#Red_IP_estática)
*   [4 Integración de interfaz y escritorio](#Integración_de_interfaz_y_escritorio)
*   [5 Solución de problemas](#Solución_de_problemas)
    *   [5.1 Los servicios de montaje fallan al arranque](#Los_servicios_de_montaje_fallan_al_arranque)
    *   [5.2 systemd-resolve no busca en el dominio local](#systemd-resolve_no_busca_en_el_dominio_local)
    *   [5.3 El segundo ordenador conectado no puede usar la LAN puenteada](#El_segundo_ordenador_conectado_no_puede_usar_la_LAN_puenteada)
*   [6 Véase también](#Véase_también)

## Utilización básica

El paquete [systemd](https://www.archlinux.org/packages/?name=systemd) es parte de la instalación de Arch por defecto y contiene todos los archivos necesarios para operar con redes cableadas. Los adaptadores inalámbricos pueden configurarse por otros servicios, como [wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant") o [iwd](/index.php/Iwd "Iwd"), los cuales serán vistos más adelante en este articulo.

### Servicios requeridos y configuración

Para usar *systemd-networkd*, [inicie/active](/index.php/Start/enable "Start/enable") `systemd-networkd.service`.

Es opcional también [iniciar/activar](/index.php/Start/enable "Start/enable") `systemd-resolved.service`, que es un servicio de resolución de nombres de red para aplicaciones locales, considerando los siguientes puntos:

*   el servicio [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") es necesario si las entradas DNS se especifican en archivos *.network*;
*   se puede usar para obtener automáticamente direcciones DNS del cliente de red DHCP;
*   es importante entender cómo [resolv.conf](/index.php/Resolv.conf "Resolv.conf") y *systemd-resolved* interactúan para configurar correctamente el DNS que se utilizará, algunas explicaciones se proporcionan en el artículo [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved");
*   advierta que *systemd-resolved* también se puede usar sin *systemd-networkd*.

### Ejemplos de configuración

Todas las configuraciones estan almacenadas como `foo.network` en `/etc/systemd/network`. Para una lista completa de opciones y orden de procesamiento, consulte los [#Archivos de Configuración](#Archivos_de_Configuración) y [systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5).

Systemd/udev asigna automaticamente nombres previsibles, nombres de intefaces de red estables para todo las interfaces de Ethernet local, WLAN y WWAN. Utilice `networkctl list` para listar los dispositivos presentes en el sistema.

Después de realizar cambios en los archivos de configuración, [reinicie](/index.php/Restart "Restart") `systemd-networkd.service`.

**Nota:**

*   Las opciones especificadas en los archivos de configuración distinguen entre mayúsculas y minúsculas.
*   En los ejemplos de abajo, `enp1s0` es el adaptador de cable y `wlp2s0` es el adaptador inalámbrico. Estos nombres pueden ser diferentes en sistemas distintos. También es posible usar un comodín, por ejemplo, `Name=en*`.
*   Si desea desactivar IPv6, consulte [IPv6#systemd-networkd](/index.php/IPv6#systemd-networkd_2 "IPv6").
*   Establezca `DHCP=yes` en la sección `[Network]` para aceptar una solicitud IPv4 **y** IPv6 de DHCP.

#### Adaptador cableado utilizando DHCP

 `/etc/systemd/network/*wired*.network` 
```
[Match]
Name=enp1s0

[Network]
DHCP=ipv4

```

#### Adaptador cableado utilizando una IP estática

 `/etc/systemd/network/20-wired.network` 
```
[Match]
Name=enp1s0

[Network]
Address=10.1.10.9/24
Gateway=10.1.10.1
DNS=10.1.10.1
#DNS=8.8.8.8
```

`Address=` se puede usar más de una vez para configurar múltiples direcciones IPv4 o IPv6\. Consulte [#Archivos network](#Archivos_network) o [systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5) para obtener más opciones.

#### Adaptador inalámbrico

A fin de conectarse a una red inalámbrica con *systemd-networkd*, es necesario un adaptador inalámbrico configurado con otro servicio como [wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant") o [Iwd](/index.php/Iwd "Iwd")

 `/etc/systemd/network/25-wireless.network` 
```
[Match]
Name=wlp2s0

[Network]
DHCP=ipv4

```

Si el adaptador inalámbrico tiene una dirección IP estática, la configuración es la misma (excepto por el nombre de la interfaz) como con la de un [adaptador cableado](#Adaptador_cableado_utilizando_una_IP_estática).

#### Adaptadores cableados e inalámbricos en la misma máquina

Esta instalación activará una IP con el cliente DHCP para ambas conexiones haciendo uso de la directiva métrica que permite al kernel la desición sobre cúal conexión utilizar sobre la marcha. De esta forma, no se observará ningún salto de desconexión cuando la conexión cableada se desconecte.

La métrica de ruta del kernel (misma que la configurada con *ip*) decide qué ruta utilizar para los paquetes salientes, en casos de muchas coincidencias. Esto se dará en el caso de que ambos adaptadores del sistema, cableados e inalámbricos, tengan conexiones activas. Para romper la cola, el kernel usa la métrica. Si una de las conexiones se apaga, la otra automaticamente se conecta sin que sea necesario un filtro con algo configurado (las transferencias en curso pueden aún no lidiar con esto apropiadamente, pero para eso hay otra capa diferente del [OSI](https://en.wikipedia.org/wiki/es:Modelo_OSI "wikipedia:es:Modelo OSI")).

**Nota:** la opción `Metric` es para rutas estáticas, mientras la opción `RouteMetric` es para instalaciones que no usan rutas estáticas. Consulte [systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5) para obtener más detalles.
 `/etc/systemd/network/20-wired.network` 
```
[Match]
Name=enp1s0

[Network]
DHCP=ipv4

[DHCP]
RouteMetric=10
```
 `/etc/systemd/network/25-wireless.network` 
```
[Match]
Name=wlp2s0

[Network]
DHCP=ipv4

[DHCP]
RouteMetric=20
```

#### Renombrar una interfaz

En lugar de [editar reglas udev](/index.php/Network_configuration#Change_interface_name "Network configuration"), se puede usar un archivo *.link* para cambiar el nombre de una interfaz. Un ejemplo útil es establecer un nombre de interfaz predecible para un adaptador USB de Ethernet en función de su dirección MAC, ya que a esos adaptadores, generalmente, obtienen diferentes nombres según el puerto USB en el que estén conectados.

 `/etc/systemd/network/10-ethusb0.link` 
```
[Match]
MACAddress=12:34:56:78:90:ab

[Link]
Description=Adaptador USB a Ethernet
Name=ethusb0
```

**Nota:** cualquier archivo *.link* proporcionado por el usuario **debe** tener un nombre de archivo léxicamente anterior al de la configuración predeterminada `99-default.link` para ser considerado antes del predeterminado. Por ejemplo, nombre el archivo `10-ethusb0.link` y no `ethusb0.link`.

## Archivos de configuración

Los archivos de configuración se encuentran en `/usr/lib/systemd/network`, el volátil directorio de red `/run/systemd/network` y el directorio de red de administración local `/etc/systemd/network`. Los archivos en `/etc/systemd/network` tienen la máxima prioridad.

Hay tres tipos de archivos de configuración. Todos usan un formato similar a los [archivos de unidad de systemd](/index.php/Systemd#Writing_unit_files "Systemd").

*   Archivos ***.network***. Aplicarán una configuración de red para un dispositivo *coincidente*
*   Archivos ***.netdev***. Crearán un «dispositivo de red virtual» para un entorno *coincidente*
*   Archivos ***.link***. Cuando aparece un dispositivo de red, [udev](/index.php/Udev "Udev") buscará el primer archivo *.link* *coincidente*

Todos siguen las mismas reglas:

*   si **todas** las condiciones en la sección `[Match]` coinciden, el perfil se activará;
*   una sección vacía `[Match]` significa que el perfil se aplicará en cualquier caso (se puede comparar al comodín `*`);
*   todos los archivos de configuración se ordenan y procesan colectivamente en orden léxico, independientemente del directorio en el que se alojen;
*   los archivos con el mismo nombre se reemplazan entre sí.

**Sugerencia:**

*   Para anular un archivo proporcionado por el sistema en `/usr/lib/systemd/network` de forma permanente (es decir, incluso después de la actualización), coloque un archivo con el mismo nombre en `/etc/systemd/network` y cree un enlace simbólico a `/dev/null`
*   El comodín `*` se puede usar en `VALUE` (por ejemplo, `en*` coincidirá con cualquier dispositivo Ethernet), una función [booleana](https://en.wikipedia.org/wiki/es:Funci%C3%B3n_booleana "wikipedia:es:Función booleana") puede escribirse simplemente como `yes` o `no`.
*   Siguiendo este [hilo de Arch-general](https://mailman.archlinux.org/pipermail/arch-general/2014-March/035381.html), la mejor práctica es establecer configuraciones de red de contenedor específicas *dentro del contenedor* con archivos de configuración **networkd**.
*   Systemd acepta los valores `1, true, yes, on` para indicar una función booleana verdadera, y los valores `0, false, no, off` para un booleano falso.

### Archivos network

Estos archivos están destinados a establecer variables de configuración de red, especialmente para servidores y contenedores.

Los archivos *.network* tienen las siguientes secciones: `[Match]`, `[Link]`, `[Network]`, `[Address]`, `[Route]`, y `[DHCP]`. A continuación se muestran las claves configuradas comúnmente para cada sección. Consulte [systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5) para obtener más información y ejemplos.

#### [Match]

| Parámetros | Descripción | Valores aceptados | Valores predeterminados |
| `Name=` | Hacer coincidir los nombres de los dispositivos, por ejemplo `en*`. Al anteponer el prefijo `!`, la lista se invierte. | nombres de dispositivos separados por espacios en blanco con patrones [globs](https://en.wikipedia.org/wiki/es:glob_(programming) "wikipedia:es:glob (programming)"), negación lógica (`!`) |
| `MACAddress=` | Hacer coincidir las direcciones MAC, por ejemplo `MACAddress=01:23:45:67:89:ab 00-11-22-33-44-55 AABB.CCDD.EEFF` | direcciones MAC separadas por espacios en blanco en formato hexadecimal delimitado por dos puntos, guiones o puntos |
| `Host=` | Hacer coincidir el nombre del equipo o la ID de máquina del sistema. | cadena de nombre del equipo con globs del [ID de la máquina](https://jlk.fjfi.cvut.cz/arch/manpages/man/machine-id.5.en) |
| `Virtualization=` | Comprobar si el sistema se ejecuta en un entorno virtualizado. `Virtualization=false` solo coincidirá con su máquina del equipo, mientras que `Virtualization=true` coincide con cualquier contenedor o máquina virtual. Es posible verificar un tipo o implementación de virtualización específica. | booleano, negación lógica (`!`), tipo (`vm`, `container`), implementación (`qemu`, `kvm`, `zvm`, `vmware`, `microsoft`, `oracle`, `xen`, `bochs`, `uml`, `bhyve`, `qnx`, `openvz`, `lxc`, `lxc-libvirt`, `systemd-nspawn`, `docker`, `podman`, `rkt`, `wsl`, `acrn`) |

#### [Link]

*   `MACAddress=` útil para [suplantación de direcciones MAC](/index.php/MAC_address_spoofing#systemd-networkd "MAC address spoofing").
*   `MTUBytes=` establecer un valor de MTU mayor (por ejemplo, cuando se usa [jumbo frames](/index.php/Jumbo_frames "Jumbo frames")) puede acelerar significativamente sus transferencias de red.
*   `Multicast` permite el uso de [multidifusión](https://en.wikipedia.org/wiki/es:Multidifusi%C3%B3n "wikipedia:es:Multidifusión") en interfaz(ces).

#### [Network]

| Parámetros | Descripción | Valores aceptados | Valores predeterminados |
| `DHCP=` | Controla el soporte de cliente DHCPv4 y/o DHCPv6. | booleano, `ipv4`, `ipv6` | `false` |
| `DHCPServer=` | Si está activado, se iniciará un servidor DHCPv4. | booleano | `false` |
| `MulticastDNS=` | Activa el soporte [DNS multidifusión](https://tools.ietf.org/html/rfc6762). Cuando se establece en `resolve`, solo se activa la resolución, pero no el registro y anuncio del equipo o servicio. | booleano, `resolve` | `false` |
| `DNSSEC=` | Controla el soporte de validación DNSSEC DNS en el enlace. Cuando se establece en `allow-downgrade`, la compatibilidad con redes que no son compatibles con DNSSEC aumenta, al desactivar automáticamente DNSSEC en este caso. | booleano, `allow-downgrade` | `false` |
| `DNS=` | Configura las direcciones [DNS](/index.php/DNS "DNS") estáticas. Se puede especificar más de una vez. | [`inet_pton`](http://man7.org/linux/man-pages/man3/inet_pton.3.html) |
| `Domains=` | Una lista de dominios que deben resolverse utilizando los servidores DNS sobre este enlace. [más información](https://www.freedesktop.org/software/systemd/man/systemd.network.html#Domains=) | nombre de dominio, opcionalmente prefijado con un signo (`~`) |
| `IPForward=` | Si está activado, los paquetes entrantes en cualquier interfaz de red se enviarán a cualquier otra interfaz de acuerdo con la tabla de enrutamiento. | booleano, `ipv4`, `ipv6` | `false` |
| `IPv6PrivacyExtensions=` | Configura el uso de direcciones temporales sin estado que cambian con el tiempo (consulte [RFC 4941](https://tools.ietf.org/html/rfc4941)). Cuando se fija `prefer-public`, activa las extensiones de privacidad, pero prefiere las direcciones públicas sobre las direcciones temporales. Cuando se fija `kernel`, la configuración predeterminada del kernel se mantendrá en su lugar. | booleano, `prefer-public`, `kernel` | `false` |

#### [Address]

*   `Address=` esta opción es **obligatoria** a menos que se use DHCP.

#### [Route]

*   `Gateway=` esta opción es **obligatoria** a menos que se utilice DHCP.
*   `Destination=` el prefijo de destino de la ruta, posiblemente seguido de una barra diagonal y la longitud del prefijo.

Si `Destination` no está presente en la sección `[Route]`, esta sección se trata como una ruta predeterminada.

**Sugerencia:** puede poner las claves `Address=` y `Gateway=` en la sección `[Network]` como una abreviatura si `[Address]` contiene solo una clave de «Dirección» y la sección `[Route]` contiene solo una clave de «Puerta de enlace».

#### [DHCP]

| Parámetros | Descripción | Valores aceptados | Valores predeterminados |
| `UseDNS=` | controla si se utilizan los servidores DNS anunciados por el servidor DHCP | booleano | `true` |
| `Anonymize=` | cuando es verdadero, las opciones enviadas al servidor DHCP seguirán el [RFC7844](https://tools.ietf.org/html/rfc7844) (perfiles de anonimato para clientes DHCP) para minimizar la divulgación de información de identificación | booleano | `false` |
| `UseDomains=` | controla si el nombre de dominio recibido del servidor DHCP se usará como dominio de búsqueda DNS. Si se establece en `route`, el nombre de dominio recibido del servidor DHCP se usará solo para enrutar consultas DNS, pero no para buscar. Esta opción a veces puede arreglar la resolución de nombres locales cuando se utiliza [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") | booleano, `route` | `false` |

### Archivos netdev

Estos archivos crearán dispositivos de red virtuales. Tienen dos secciones: `[Match]` y `[NetDev]`. A continuación se muestran las claves configuradas comúnmente para cada sección. Consulte [systemd.netdev(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.netdev.5) para obtener más información y ejemplos.

#### Sección [Match]

*   `Host=` el nombre del equipo.
*   `Virtualization=` comprueba si se ejecuta en una máquina virtual.

#### Sección [NetDev]

Las claves más comunes son:

*   `Name=` el nombre de la interfaz. **Obligatorio**.
*   `Kind=` por ejemplo, *bridge*, *bond*, *vlan*, *veth*, *sit*, etc. **Obligatorio**.

### Archivos link

Estos archivos son una alternativa a las reglas de udev personalizadas y serán aplicados por [udev](/index.php/Udev "Udev") a medida que aparezca el dispositivo. Tienen dos secciones: `[Match]` y `[Link]`. A continuación se encuentran las claves configuradas comúnmente para cada sección. Consulte [systemd.link(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.link.5) para obtener más información y ejemplos.

**Sugerencia:** utilice `# udevadm test-builtin net_setup_link /sys/path/to/network/device` para diagnosticar problemas con archivos *.link*.

#### Sección [Match]

*   `MACAddress=` la dirección MAC.
*   `Host=` el nombre del equipo.
*   `Virtualization=`
*   `Type=` el tipo de dispositivo, por ejemplo, vlan.

#### Sección [Link]

*   `MACAddressPolicy=` direcciones persistentes o aleatorias, o,
*   `MACAddress=` una dirección específica.

**Nota:** el sistema de `/usr/lib/systemd/network/99-default.link` es generalmente suficiente para la mayoría de los casos básicos.

## Utilización de contenedores

El servicio está disponible con [systemd](https://www.archlinux.org/packages/?name=systemd). Querrá [activar](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") e [iniciar](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") la unidad `systemd-networkd.service` tanto en el equipo como en el contenedor.

Para fines de depuración, se recomienda encarecidamente [instalar](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") los paquetes [bridge-utils](https://www.archlinux.org/packages/?name=bridge-utils), [net-tools](https://www.archlinux.org/packages/?name=net-tools) y [iproute2](https://www.archlinux.org/packages/?name=iproute2).

Si está utilizando [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn"), es posible que deba modificar `systemd-nspawn@.service` y añadir opciones de arranque a la línea `ExecStart`. Remítase a [systemd-nspawn(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-nspawn.1) para obtener una lista exhaustiva de opciones.

Tenga en cuenta que si desea aprovechar la configuración automática de DNS desde DHCP, debe activar `systemd-resolved` y crear el enlace simbólico `/run/systemd/resolve/resolv.conf` a `/etc/resolv.conf`. Consulte [systemd-resolved.service(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-resolved.service.8) para obtener más detalles.

Antes de comenzar a configurar su red de contenedores, es útil:

*   desactivar todos sus servicios [netctl](/index.php/Netctl "Netctl") (en equipo y contenedor), [dhcpcd](/index.php/Dhcpcd "Dhcpcd") (en equipo y contenedor), [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") (solo en contenedor) y `systemd-nspawn@.service` (solo en equipo) para evitar posibles conflictos y facilitar la depuración;
*   asegurarse de que el [reenvío de paquetes](/index.php/Internet_sharing#Enable_packet_forwarding "Internet sharing") esté activado si desea permitir que los contenedores accedan a Internet. Asegúrese de que su archivo *.network* no desactive accidentalmente el reenvío, porque si no tiene una configuración `IPForward=1` en él, `systemd-networkd` desactivará el reenvío en esa interfaz, incluso si la tiene activada globalmente;
*   asegurarse de no tener ninguna regla [iptables](/index.php/Iptables_(Espa%C3%B1ol) "Iptables (Español)") que pueda bloquear el tráfico;
*   cuando el demonio está iniciado, la orden `networkctl` de systemd mostrará el estado de las interfaces de red.

Para completar la configuración que se describe a continuación:

*   limitaremos la salida de la orden `ip a` a las interfaces correspondientes;
*   asumiremos que el «equipo» es su sistema operativo principal en el que está arrancando y el «contenedor» es su máquina virtual invitada;
*   todos los nombres de interfaces y direcciones IP son solo ejemplos.

### Red básica con DHCP

Esta configuración activará una IP obtenida con DHCP para el equipo y el contenedor. En este caso, ambos sistemas compartirán tanto la misma IP como las mismas interfaces.

 `/etc/systemd/network/*MyDhcp*.network` 
```
[Match]
Name=en*

[Network]
DHCP=ipv4

```

Luego, [active](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") e inicie `systemd-networkd.service` en su contenedor.

Por supuesto, puede reemplazar `en*` por el nombre completo de su dispositivo Ethernet dado por la salida de la orden `ip link`.

*   en el equipo y en el contenedor:

 `$ ip a` 
```
2: enp7s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 14:da:e9:b5:7a:88 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.72/24 brd 192.168.1.255 scope global enp7s0
       valid_lft forever preferred_lft forever
    inet6 fe80::16da:e9ff:feb5:7a88/64 scope link 
       valid_lft forever preferred_lft forever

```

Por defecto, el nombre del equipo recibido del servidor DHCP se utilizará como nombre de equipo transitorio.

Para cambiarlo, añada `UseHostname=false` en la sección `[DHCPv4]`

 `/etc/systemd/network/*MyDhcp*.network` 
```
[DHCPv4]
UseHostname=false

```

Si no desea configurar un DNS en `/etc/resolv.conf` y desea confiar en DHCP para definirlo, debe [activar](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") `systemd-resolved.service` y crear el enlace simbólico `/run/systemd/resolve/resolv.conf` a `/etc/resolv.conf`

```
# ln -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf

```

Consulte `systemd-resolved.service(8)` para obtener más detalles.

**Nota:** los usuarios que accedan a una partición del sistema a través de `/usr/bin/arch-chroot` desde [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts), deberán crear el enlace simbólico fuera de chroot, en la partición montada. Esto se debe a que arch-chroot vincula el archivo al entorno live.

### DHCP con dos IP distintas

#### Interfaz del puente de red

Primero, cree una interfaz del puente de red virtual. Le decimos a systemd que cree un dispositivo llamado *br0* que funcione como un puente de ethernet.

 `/etc/systemd/network/*MyBridge*.netdev` 
```
[NetDev]
Name=br0
Kind=bridge
```

[Reinicie](/index.php/Restart "Restart") `systemd-networkd.service` para que systemd puede tener conocimiento del puente de red creado.

En el equipo y en el contenedor:

 `$ ip a` 
```
3: br0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default 
    link/ether ae:bd:35:ea:0c:c9 brd ff:ff:ff:ff:ff:ff

```

Advierta que la interfaz br0 esté en la lista, pero está «DOWN» en esta etapa.

#### Vincular ethernet al puente de red

El siguiente paso es añadir al puente de red recién creado una interfaz de red. En el siguiente ejemplo, añadimos cualquier interfaz que coincida con el nombre *en** en el puente de red *br0*.

 `/etc/systemd/network/*bind*.network` 
```
[Match]
Name=en*

[Network]
Bridge=br0
```

La interfaz de ethernet no debe tener servicio DHCP o una dirección IP asociada, ya que el puente de red requiere una interfaz a la que se pueda vincular sin IP: modifique el archivo `/etc/systemd/network/*MyEth*.network` correspondiente para eliminar el direccionamiento.

#### Conectar el puente de red

Ahora que se ha creado el puente de red y se ha vinculado a una interfaz de red existente, se debe especificar la configuración IP de la interfaz del puente. Esto se define en un tercer archivo *.network*, el siguiente ejemplo utiliza DHCP.

 `/etc/systemd/network/*mybridge*.network` 
```
[Match]
Name=br0

[Network]
DHCP=ipv4
```

#### Añadir opción para arrancar el contenedor

Como queremos dar una IP separada para el equipo y otra para el contenedor, necesitamos «*Desconectar*» la red del contenedor de la del equipo. Para hacer esto, añada esta opción `--network-bridge=br0` a la orden de arranque del contenedor.

```
# systemd-nspawn --network-bridge=br0 -bD /path_to/my_container

```

#### Resultado

*   en el equipo:

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

*   en el contenedor:

 `$ ip a` 
```
2: host0: <BROADCAST,MULTICAST,ALLMULTI,AUTOMEDIA,NOTRAILERS,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 5e:96:85:83:a8:5d brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.73/24 brd 192.168.1.255 scope global host0
       valid_lft forever preferred_lft forever
    inet6 fe80::5c96:85ff:fe83:a85d/64 scope link 
       valid_lft forever preferred_lft forever

```

#### Aviso

*   ahora tenemos una dirección IP para `br0` en el equipo, y otra para `host0` en el contenedor;
*   han aparecido dos nuevas interfaces: `vb-*MyContainer*` en el equipo y `host0` en el contenedor. Esto viene como resultado de la opción `--network-bridge=br0`. Esta opción *implica* otra opción, `--network-veth`. Esto significa que se ha creado un *enlace virtual de Ethernet* entre el equipo y el contenedor;
*   la dirección DHCP en `host0` proviene del archivo del sistema `/usr/lib/systemd/network/80-container-host0.network`.

*   en el equipo:

 `$ brctl show` 
```
bridge name	bridge id		STP enabled	interfaces
br0		8000.14dae9b57a88	no		enp7s0
							vb-*MyContainer*

```

La salida de la orden anterior confirma que tenemos un puente de red con dos interfaces vinculadas.

*   en el equipo:

 `$ ip route` 
```
default via 192.168.1.254 dev br0 
192.168.1.0/24 dev br0  proto kernel  scope link  src 192.168.1.87

```

*   en el contenedor:

 `$ ip route` 
```
default via 192.168.1.254 dev host0 
192.168.1.0/24 dev host0  proto kernel  scope link  src 192.168.1.73

```

Las salidas de las órdenes anteriores confirman que hemos activado las interfaces `br0` y `host0` con una dirección IP y puerta de enlace 192.168.1.254\. La dirección de la puerta de enlace ha sido tomada automáticamente por *systemd-networkd*.

 `$ cat /run/systemd/resolve/resolv.conf` 
```
nameserver 192.168.1.254

```

### Red IP estática

Establecer una IP estática para cada dispositivo puede ser útil en caso de servicios web implementados (por ejemplo, FTP, http, SSH). Cada dispositivo mantendrá la misma dirección MAC en todos los reinicios si su archivo del sistema `/usr/lib/systemd/network/99-default.link` tiene la opción `MACAddressPolicy=persistent` (que viene por defecto). Por lo tanto, enrutará fácilmente cualquier servicio en su puerta de enlace al dispositivo deseado.

La siguiente configuración debe hacerse para esta:

*   en el equipo:

La configuración es muy similar a la de [#DHCP con dos IP distintas](#DHCP_con_dos_IP_distintas). Primero, se debe crear una interfaz del puente de red virtual y la interfaz física principal debe estar vinculada a ella. Esta tarea se puede lograr con los siguientes dos archivos, con contenidos iguales a los disponibles en la sección DHCP.

```
/etc/systemd/network/*MyBridge*.netdev
/etc/systemd/network/*MyEth*.network

```

A continuación, debe configurar la IP y el DNS de la interfaz del puente de red virtual recién creada. El siguiente archivo *MyBridge*.network proporciona un ejemplo de configuración:

 `/etc/systemd/network/*MyBridge*.network` 
```
[Match]
Name=br0

[Network]
DNS=192.168.1.254
Address=192.168.1.87/24
Gateway=192.168.1.254

```

*   en el contenedor:

Primero, eliminaremos el archivo del sistema `/usr/lib/systemd/network/80-container-host0.network` que proporciona una configuración DHCP para la interfaz de red predeterminada del contenedor. Para hacerlo de forma permanente (por ejemplo, incluso después de las actualizaciones de [systemd](https://www.archlinux.org/packages/?name=systemd)), haga lo siguiente en el contenedor. Esto enmascarará el archivo `/usr/lib/systemd/network/80-container-host0.network` ya que los archivos con el mismo nombre en `/etc/systemd/network` tienen prioridad sobre `/usr/lib/systemd/network`. Tenga en cuenta que este archivo puede mantenerse solo si desea una IP estática en el equipo y desea que la dirección IP de sus contenedores se asigne a través de DHCP.

```
# ln -sf /dev/null /etc/systemd/network/80-container-host0.network

```

Luego, configure una IP estática para la interfaz de red predeterminada `host0` y [active e inicie](/index.php/Systemd#Basic_systemctl_usage "Systemd") `systemd-networkd.service` en su contenedor. Seguidamente se proporciona una configuración de ejemplo:

 `/etc/systemd/network/*MyVeth*.network` 
```
[Match]
Name=host0

[Network]
DNS=192.168.1.254
Address=192.168.1.94/24
Gateway=192.168.1.254

```

## Integración de interfaz y escritorio

*systemd-networkd* no tiene una interfaz de gestión interactiva adecuada ni a través de línea de órdenes ni gráfica. Aún así, algunas herramientas están disponibles para mostrar el estado actual de la red, recibir notificaciones o interactuar con la configuración inalámbrica:

*   *networkctl* (a través de CLI) ofrece un simple volcado de los estados de la interfaz de red.

*   Cuando *networkd* está configurado con [wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant"), tanto *wpa_cli* como *wpa_gui* ofrecen la posibilidad de asociar y configurar interfaces WLAN dinámicamente.

*   [networkd-notify-git](https://aur.archlinux.org/packages/networkd-notify-git/) puede generar notificaciones simples en respuesta a los cambios de estado de la interfaz de red (como conexión/desconexión y nueva asociación).

*   El demonio [networkd-dispatcher](https://aur.archlinux.org/packages/networkd-dispatcher/) permite ejecutar scripts en respuesta a cambios en el estado de la interfaz de red, similar a *NetworkManager-dispatcher*.

*   En cuanto a la resolución de DNS de *systemd-resolved*, la información sobre los servidores DNS actuales se puede visualizar con `resolvectl status`.

## Solución de problemas

### Los servicios de montaje fallan al arranque

Si ejecuta servicios como [Samba](/index.php/Samba "Samba")/[NFS](/index.php/NFS "NFS") que fallan si se inician antes de que la red esté activa, puede [activar](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") el servicio `systemd-networkd-wait-online.service`. Sin embargo, esto rara vez es necesario porque la mayoría de los demonios de red comienzan bien, incluso si la red aún no se ha configurado.

### systemd-resolve no busca en el dominio local

[systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") puede no buscar el dominio local cuando se le da solo el nombre del equipo, incluso cuando `UseDomains=yes` o `Domains=[domain-list]` está presente en el archivo *.network* apropiadamente, y ese archivo produce la esperada `search [domain-list]` en `resolv.conf`. Puede ejecutar `networkctl status` o `resolvectl status` para verificar si la búsqueda de dominios se está recogiendo bien.

Posibles soluciones:

*   Desactive [LLMNR](/index.php/Systemd-resolved#LLMNR "Systemd-resolved") para permitir que *systemd-resolved* continúe inmediatamente agregando los sufijos DNS.
*   Recorte la base de datos de `hosts` para `/etc/nsswitch.conf` (por ejemplo, eliminando la opción `[!UNAVAIL=return]` después del servicio `resolve`).
*   Alterne con el uso de nombres de dominio totalmente calificados.
*   Utilice `/etc/hosts` para resolver nombres de equipo.
*   Recurra al uso de `dns` de glibc en lugar de utilizar `resolve` de systemd.

### El segundo ordenador conectado no puede usar la LAN puenteada

El primer ordenador tiene dos LAN. El segundo tiene una LAN y está conectado al primero. Vayamos al segundo ordenador para dar acceso completo a la LAN después de superar la interfaz puenteada:

```
# sysctl net.bridge.bridge-nf-filter-pppoe-tagged=0
# sysctl net.bridge.bridge-nf-filter-vlan-tagged=0
# sysctl net.bridge.bridge-nf-call-ip6tables=0
# sysctl net.bridge.bridge-nf-call-iptables=0
# sysctl net.bridge.bridge-nf-call-arptables=0

```

## Véase también

*   [systemd.networkd man page](http://www.freedesktop.org/software/systemd/man/systemd-networkd.service.html)
*   [Tom Gundersen, main systemd-networkd developer, G+ home page](https://plus.google.com/u/0/+TomGundersen/posts)
*   [Tom Gundersen posts on Core OS blog](https://coreos.com/blog/intro-to-systemd-networkd/)
*   [How to set up systemd-networkd with wpa_supplicant](https://bbs.archlinux.org/viewtopic.php?pid=1393759#p1393759) (WonderWoofy's walkthrough on Arch forums)