Artículos relacionados

*   [systemd-networkd (Español)](/index.php/Systemd-networkd_(Espa%C3%B1ol) "Systemd-networkd (Español)")
*   [Domain name resolution (Español)](/index.php/Domain_name_resolution_(Espa%C3%B1ol) "Domain name resolution (Español)")
*   [Avahi](/index.php/Avahi "Avahi")

**Estado de la traducción**
Este artículo es una traducción de [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved"), revisada por última vez el **2019-10-29**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Systemd-resolved&diff=0&oldid=587429) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[systemd-resolved](https://www.freedesktop.org/wiki/Software/systemd/resolved/) es un servicio de [systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") que proporciona resolución de nombres de red a aplicaciones locales a través de una interfaz [D-Bus (Español)](/index.php/D-Bus_(Espa%C3%B1ol) "D-Bus (Español)"), el servicio [NSS](/index.php/Name_Service_Switch "Name Service Switch") de `resolve` ([nss-resolve(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nss-resolve.8)), y un receptor de escucha de DNS local en `127.0.0.53`. Consulte [systemd-resolved(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-resolved.8) para conocer su utilización.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 DNS](#DNS)
        *   [2.1.1 Configurar servidores DNS](#Configurar_servidores_DNS)
            *   [2.1.1.1 Automáticamente](#Automáticamente)
            *   [2.1.1.2 Manualmente](#Manualmente)
            *   [2.1.1.3 Reserva](#Reserva)
        *   [2.1.2 DNSSEC](#DNSSEC)
        *   [2.1.3 DNS mediante TLS](#DNS_mediante_TLS)
    *   [2.2 mDNS](#mDNS)
    *   [2.3 LLMNR](#LLMNR)
*   [3 Buscar](#Buscar)

## Instalación

*systemd-resolved* es una parte del paquete [systemd](https://www.archlinux.org/packages/?name=systemd) que se [instala](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") por defecto.

## Configuración

*systemd-resolved* proporciona servicios de resolución para [sistema de nombres de dominio (DNS)](https://en.wikipedia.org/wiki/es:Sistema_de_nombres_de_dominio "wikipedia:es:Sistema de nombres de dominio") (incluyendo [DNSSEC](https://en.wikipedia.org/wiki/es:Domain_Name_System_Security_Extensions "wikipedia:es:Domain Name System Security Extensions") y [DNS mediante TLS](https://en.wikipedia.org/wiki/es:DNS_mediante_TLS "wikipedia:es:DNS mediante TLS")), [DNS de multidifusión (mDNS)](https://en.wikipedia.org/wiki/Multicast_DNS "wikipedia:Multicast DNS") y [resolución de nombres de multidifusión de enlace local (LLMNR)](https://en.wikipedia.org/wiki/Link-Local_Multicast_Name_Resolution "wikipedia:Link-Local Multicast Name Resolution").

La resolución se puede configurar editando `/etc/systemd/resolved.conf` y/o colocando archivos con extensión *.conf* en `/etc/systemd/resolved.conf.d/`. Véase [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5).

Para utilizar *systemd-resolved* [inicie](/index.php/Start "Start") y [active](/index.php/Enable "Enable") `systemd-resolved.service`.

**Sugerencia:** para comprender el contexto en torno a las opciones y los cambios, se puede activar la información detallada de depuración de errores para *systemd-resolved* como se describe en [systemd (Español)#Diagnosticar un servicio](/index.php/Systemd_(Espa%C3%B1ol)#Diagnosticar_un_servicio "Systemd (Español)").

### DNS

*systemd-resolved* tiene cuatro modos diferentes para manejar la [resolución de nombres de dominio](/index.php/Domain_name_resolution "Domain name resolution") (los cuatro modos se describen en [systemd-resolved(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-resolved.8#%2FETC%2FRESOLV.CONF)). Nos centraremos aquí en los dos modos más relevantes:

1.  Utilizar el archivo «stub» de DNS de systemd: el archivo «stub» de DNS de systemd `/run/systemd/resolve/stub-resolv.conf` contiene el código local `127.0.0.53` como el único servidor DNS y una lista de dominios de búsqueda. Este es el modo de operación **recomendado**. Se aconseja a los usuarios del servicio que redirijan el archivo `/etc/resolv.conf` al archivo local de resolución de DNS `/run/systemd/resolve/stub-resolv.conf` administrado por *systemd-resolved*. Esto extiende la configuración administrada por systemd a todos los clientes. Se puede consiguir reemplazando `/etc/resolv.conf` con un enlace simbólico al archivo «stub» de systemd: `# ln -sf /run/systemd/resolve/stub-resolv.conf /etc/resolv.conf` 
2.  Preservar *resolv.conf*: este modo conserva `/etc/resolv.conf` y *systemd-resolved* es simplemente un cliente de aquel archivo. Este modo es menos disruptivo ya que `/etc/resolv.conf` puede continuar siendo administrado por otros paquetes.

**Nota:** el modo en que opera *systemd-resolved* se detecta automáticamente, dependiendo de si `/etc/resolv.conf` es un enlace simbólico al archivo de resolución de DNS del archivo «stub» local o contiene nombres de servidores.

#### Configurar servidores DNS

**Sugerencia:** para verificar el DNS realmente utilizado por *systemd-resolved*, utilice la orden:
```
$ resolvectl status

```

##### Automáticamente

*systemd-resolved* funcionará de forma inmediata con un [gestor de red](/index.php/Network_manager "Network manager") utilizando `/etc/resolv.conf`. No se requiere ninguna configuración particular ya que *systemd-resolved* se detectará siguiendo el enlace simbólico `/etc/resolv.conf`. Este será el caso con [systemd-networkd (Español)](/index.php/Systemd-networkd_(Espa%C3%B1ol) "Systemd-networkd (Español)") o [NetworkManager (Español)](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)").

Sin embargo, si los clientes [DHCP](/index.php/DHCP "DHCP") y [VPN](/index.php/VPN "VPN") utilizan el programa [resolvconf](https://en.wikipedia.org/wiki/resolvconf "wikipedia:resolvconf") para configurar servidores de nombres y dominios de búsqueda (consulte [openresolv#Users](/index.php/Openresolv#Users "Openresolv") para obtener una lista de software que use *resolvconf*), se necesita el paquete adicional [systemd-resolvconf](https://www.archlinux.org/packages/?name=systemd-resolvconf) para proporcionar el enlace simbólico `/usr/bin/resolvconf`.

**Nota:** *systemd-resolved* tiene una interfaz *resolvconf* limitada y es posible que no funcione con todos los clientes; consulte [resolvectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolvectl.1#COMPATIBILITY_WITH_RESOLVCONF%288%29) para obtener más información.

##### Manualmente

Con el modo de archivo «stub» de DNS local, se proporcionan servidores DNS alternativos en el archivo [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5):

 `/etc/systemd/resolved.conf.d/dns_servers.conf` 
```
[Resolve]
DNS=91.239.100.100 89.233.43.71
```

**Nota:** los [gestores de red](/index.php/Network_manager "Network manager") tienen su propia configuración de DNS que anula el valor predeterminado de *systemd-resolved'*.

##### Reserva

Si *systemd-resolved* no recibe las direcciones del servidor DNS del [gestor de red](/index.php/Network_manager "Network manager") y no hay servidores DNS configurados [[#Manualmente|manualmente], entonces *systemd-resolved* vuelve a las direcciones DNS de reserva, garantizando así que la resolución de DNS funcione siempre.

**Nota:** los DNS de reserva están en este orden: [Cloudflare](/index.php/Alternative_DNS_services#Cloudflare "Alternative DNS services"), [Quad9](/index.php/Alternative_DNS_services#Quad9 "Alternative DNS services") (sin filtrar y sin DNSSEC) y [Google](/index.php/Alternative_DNS_services#Google "Alternative DNS services"); vea el [PKGBUILD de systemd](https://git.archlinux.org/svntogit/packages.git/tree/trunk/PKGBUILD?h=packages/systemd#n103) donde se definen los servidores.

Las direcciones se pueden cambiar configurando `FallbackDNS=` en [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5). Por ejemplo:

 `/etc/systemd/resolved.conf.d/fallback_dns.conf` 
```
[Resolve]
FallbackDNS=127.0.0.1 ::1
```

Para desactivar la funcionalidad de reserva de DNS, configure la opción `FallbackDNS` sin especificar ninguna dirección:

 `/etc/systemd/resolved.conf.d/fallback_dns.conf` 
```
[Resolve]
FallbackDNS=
```

#### DNSSEC

Por defecto, la validación [DNSSEC (Español)](/index.php/DNSSEC_(Espa%C3%B1ol) "DNSSEC (Español)") solo se activará si el servidor DNS ascendente lo admite. Si desea validar siempre DNSSEC, rompiendo así la resolución de DNS con servidores de nombres que no lo admiten, establezca `DNSSEC=true`:

 `/etc/systemd/resolved.conf.d/dnssec.conf` 
```
[Resolve]
DNSSEC=true
```

**Sugerencia:** si su servidor DNS no es compatible con DNSSEC y experimenta problemas con el modo predeterminado de degradación permitida (por ejemplo, [systemd issue 10579](https://github.com/systemd/systemd/issues/10579)), puede desactivar explícitamente el soporte DNSSEC de systemd-resolve estableciendo `DNSSEC=false`.

Pruebe la validación de DNSSEC consultando un dominio con una firma no válida:

 `$ resolvectl query sigfail.verteiltesysteme.net` 
```
sigfail.verteiltesysteme.net: resolve call failed: DNSSEC validation failed: invalid

```

Ahora pruebe un dominio con firma válida:

 `$ resolvectl query sigok.verteiltesysteme.net` 
```
sigok.verteiltesysteme.net: 134.91.78.139

-- Information acquired via protocol DNS in 266.3ms.
-- Data is authenticated: yes

```

#### DNS mediante TLS

**Advertencia:** systemd-resolve solo valida el certificado del servidor DNS si el mismo se emite para la dirección IP del servidor (una solución rara). Los certificados de servidores DNS sin una dirección IP, no se comprueban, lo que hace que el sistema de resolución sea vulnerable a los ataques de intermediarios. Consulte [systemd issue 9397](https://github.com/systemd/systemd/issues/9397).

DNS mediante TLS está desactivado por defecto. Para activarlo, cambie la configuración `DNSOverTLS=` en la sección `[Resolve]` en [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5).

 `/etc/systemd/resolved.conf.d/dns_over_tls.conf` 
```
[Resolve]
DNSOverTLS=yes
```

**Nota:** el servidor DNS utilizado debe admitir DNS mediante TLS; de lo contrario, todas las solicitudes DNS fallarán.

### mDNS

*systemd-resolved* es capaz de funcionar solucionando y respondiendo a [DNS de multidifusión](https://en.wikipedia.org/wiki/Multicast_DNS "wikipedia:Multicast DNS").

Para actuar como «solucionador» se proporciona la resolución del [nombre del equipo](/index.php/Hostname "Hostname") utilizando un esquema de nombres tal como «*hostname*.local».

mDNS solo se activará para la conexión si tanto la configuración global de systemd-resolved (`MulticastDNS=` en [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5)) como la configuración del [gestor de red](/index.php/Network_manager "Network manager") por conexión están activadas. Por defecto, *systemd-resolved* activa el «respondedor» mDNS, pero tanto [systemd-networkd (Español)](/index.php/Systemd-networkd_(Espa%C3%B1ol) "Systemd-networkd (Español)") como [NetworkManager (Español)](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)") no lo activan para las conexiones:

*   Para [systemd-networkd (Español)](/index.php/Systemd-networkd_(Espa%C3%B1ol) "Systemd-networkd (Español)") la configuración es `MulticastDNS=` en la sección `[Network]`. Consulte [systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5).
*   Para [NetworkManager (Español)](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)") la configuración es `mdns=` en la sección `[connection]`; consulte [nm-settings(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nm-settings.5). Los valores son `0` - desactivado, `1` - solo resuelve, `2` - resuelve y responde. [[1]](https://cgit.freedesktop.org/NetworkManager/NetworkManager/tree/libnm-core/nm-setting-connection.h#n102)

**Nota:** si [Avahi](/index.php/Avahi "Avahi") está instalado, considere [desactivar](/index.php/Disabling "Disabling") `avahi-daemon.service` y `avahi-daemon.socket` para evitar conflictos con *systemd-resolved*.

{{Sugerencia|el valor predeterminado para todas las conexiones de [NetworkManager (Español)](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)") se puede establecer creando un archivo de configuración en `/etc/NetworkManager/conf.d/` y configurando `connection.mdns=` en la sección `[connection]`. Por ejemplo, lo siguiente activará el solucionador mDNS para todas las conexiones:

 `/etc/NetworkManager/conf.d/mdns.conf` 
```
[connection]
connection.mdns=1
```

Vea [NetworkManager.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/NetworkManager.conf.5).

Si planea usar mDNS y un [firewall](/index.php/Firewall "Firewall"), asegúrese de abrir el puerto UDP `5353`.

### LLMNR

La [resolución de nombres de multidifusión de enlace local](https://en.wikipedia.org/wiki/Link-Local_Multicast_Name_Resolution "wikipedia:Link-Local Multicast Name Resolution") es un protocolo de resolución de [nombres de equipo](/index.php/Hostname "Hostname") creado por Microsoft.

LLMNR solo se activará para la conexión si tanto la configuración global de systemd-resolved (`LLMNR=` en [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5)) como la configuración del [gestor de red](/index.php/Network_manager "Network manager") por conexión están activadas. Por defecto, *systemd-resolved* activa el «respondedor» LLMNR para [systemd-networkd (Español)](/index.php/Systemd-networkd_(Espa%C3%B1ol) "Systemd-networkd (Español)") y [NetworkManager (Español)](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)") lo activa para las conexiones:

*   Para [systemd-networkd (Español)](/index.php/Systemd-networkd_(Espa%C3%B1ol) "Systemd-networkd (Español)") la configuración es `LLMNR=` en la sección `[Network]`. Consulte [systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5).
*   Para [NetworkManager (Español)](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)") la configuración es `llmnr=` en la sección `[connection]`; consulte [nm-settings(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nm-settings.5). Los valores son `0` - desactivado, `1` - solo resolver, `2` - resolver y responder.

{{Sugerencia|el valor predeterminado para todas las conexiones de [NetworkManager (Español)](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)") se puede establecer creando un archivo de configuración en `/etc/NetworkManager/conf.d/` y configurando `connection.llmnr=` en la sección `[connection]`. Por ejemplo, lo siguiente desactivará LLMNR para todas las conexiones:

 `/etc/NetworkManager/conf.d/llmnr.conf` 
```
[connection]
connection.llmnr=0
```

Consulte [NetworkManager.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/NetworkManager.conf.5).

Si planea usar LLMNR y un [firewall](/index.php/Firewall "Firewall"), asegúrese de abrir los puertos UDP y TCP `5355`.

## Buscar

Para consultar registros DNS, servidores mDNS o LLMNR puede usar la utilidad *resolvectl*.

Por ejemplo, para consultar un registro DNS:

 `$ resolvectl query archlinux.org` 
```
archlinux.org: 2a01:4f8:172:1d86::1
               138.201.81.199

-- Information acquired via protocol DNS in 48.4ms.
-- Data is authenticated: no

```

Consulte [resolvectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolvectl.1#EXAMPLES) para conocer más ejemplos.