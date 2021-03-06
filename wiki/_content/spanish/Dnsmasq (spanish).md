**Estado de la traducción**
Este artículo es una traducción de [dnsmasq](/index.php/Dnsmasq "Dnsmasq"), revisada por última vez el **2019-11-06**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Dnsmasq&diff=0&oldid=587307) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Domain name resolution](/index.php/Domain_name_resolution "Domain name resolution")

[dnsmasq](http://www.thekelleys.org.uk/dnsmasq/doc.html) proporciona un [servidor DNS](https://en.wikipedia.org/wiki/Name_server "wikipedia:Name server"), un [servidor DHCP](https://en.wikipedia.org/wiki/es:Dynamic_Host_Configuration_Protocol "wikipedia:es:Dynamic Host Configuration Protocol") con soporte para [DHCPv6](https://en.wikipedia.org/wiki/es:DHCPv6 "wikipedia:es:DHCPv6") y [PXE](https://en.wikipedia.org/wiki/es:Preboot_Execution_Environment "wikipedia:es:Preboot Execution Environment"), y un [servidor TFTP](https://en.wikipedia.org/wiki/es:Trivial_File_Transfer_Protocol "wikipedia:es:Trivial File Transfer Protocol"). Está diseñado para ser liviano y consumir poco, adecuado para enrutadores y cortafuegos con recursos limitados. dnsmasq también se puede configurar para almacenar en caché las consultas a DNS con el fin mejorar las velocidades de búsqueda de DNS de los sitios visitados con anterioridad.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Iniciar el demonio](#Iniciar_el_demonio)
*   [3 Configuración](#Configuración)
    *   [3.1 Servidor DNS](#Servidor_DNS)
        *   [3.1.1 Archivo de direcciones DNS y de reenvío](#Archivo_de_direcciones_DNS_y_de_reenvío)
            *   [3.1.1.1 openresolv](#openresolv)
            *   [3.1.1.2 Reenvío manual](#Reenvío_manual)
        *   [3.1.2 Añadir un dominio personalizado](#Añadir_un_dominio_personalizado)
        *   [3.1.3 Prueba](#Prueba)
    *   [3.2 Servidor DHCP](#Servidor_DHCP)
        *   [3.2.1 Prueba](#Prueba_2)
    *   [3.3 Servidor TFTP](#Servidor_TFTP)
    *   [3.4 Servidor PXE](#Servidor_PXE)
*   [4 Consejos y trucos](#Consejos_y_trucos)
    *   [4.1 Impedir que OpenDNS redirija las consultas de Google](#Impedir_que_OpenDNS_redirija_las_consultas_de_Google)
    *   [4.2 Anular direcciones](#Anular_direcciones)
    *   [4.3 Tener más de una instancia](#Tener_más_de_una_instancia)
        *   [4.3.1 Estático](#Estático)
        *   [4.3.2 Dinámico](#Dinámico)
    *   [4.4 Lista negra de dominios](#Lista_negra_de_dominios)
*   [5 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq).

## Iniciar el demonio

[Inicie/active](/index.php/Start/enable "Start/enable") el servicio `dnsmasq.service`.

Para ver si dnsmasq se inició correctamente, consulte el «*journal*» de systemd:

```
$ journalctl -u dnsmasq.service

```

La red también deberá reiniciarse para que el cliente DHCP pueda crear un nuevo archivo `/etc/resolv.conf`.

## Configuración

Para configurar dnsmasq, necesita editar `/etc/dnsmasq.conf`. El archivo contiene extensos comentarios que explican sus opciones. Para todas las opciones disponibles, consulte [dnsmasq(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dnsmasq.8).

**Advertencia:** dnsmasq activa de forma predeterminada su servidor DNS. Si no lo necesita, debe desactivarlo explícitamente definiendo el puerto DNS en `0`: `port=0` 

**Sugerencia:** para verificar la sintaxis de los archivos de configuración, ejecute:
```
$ dnsmasq --test

```

### Servidor DNS

Para configurar dnsmasq como un demonio para el almacenamiento de DNS en un solo equipo, especifique una directiva `listen-address`, añadiendo la [dirección IP](https://en.wikipedia.org/wiki/es:Direcci%C3%B3n_IP "wikipedia:es:Dirección IP") del [equipo local](https://en.wikipedia.org/wiki/es:Localhost "wikipedia:es:Localhost"):

```
listen-address=::1,127.0.0.1

```

Para utilizar este equipo con el fin de que su dirección IP de [LAN](https://en.wikipedia.org/wiki/es:Red_de_%C3%A1rea_local "wikipedia:es:Red de área local") escuche otros equipos en la red. Se recomienda utilizar una IP LAN estática en este caso. Por ejemplo:

```
listen-address=::1,127.0.0.1,192.168.1.1

```

Establezca el número de nombres de dominio almacenables en caché con la opción `cache-size=*size*` (el valor predeterminado es `150`):

```
cache-size=1000

```

Para validar con [DNSSEC](/index.php/DNSSEC "DNSSEC") cargue [los anclajes de confianza](https://en.wikipedia.org/wiki/es:Ancla_de_confianza "wikipedia:es:Ancla de confianza") de DNSSEC proporcionados por el paquete [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) y configure la opción `dnssec`:

```
conf-file=/usr/share/dnsmasq/trust-anchors.conf
dnssec

```

Consulte [dnsmasq(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dnsmasq.8) para ver más opciones que quizás pueda querer usar.

#### Archivo de direcciones DNS y de reenvío

Después de configurar dnsmasq, necesita añadir las direcciones del equipo local como los únicos servidores de nombres en `/etc/resolv.conf`. Esto hace que todas las consultas se envíen a dnsmasq.

Como dnsmasq no es un servidor DNS recursivo, debe configurar el reenvío a un servidor DNS externo. Esto se puede hacer automáticamente usando [openresolv](/index.php/Openresolv "Openresolv") o especificando manualmente la dirección del servidor DNS en la configuración de dnsmasq.

##### openresolv

Si su administrador de red admite *resolvconf*, en lugar de modificar directamente `/etc/resolv.conf`, puede utilizar [openresolv](/index.php/Openresolv "Openresolv") para generar archivos de configuración para dnsmasq. [[1]](https://roy.marples.name/projects/openresolv/config)

Edite `/etc/resolvconf.conf` y añada las direcciones de [loopback](https://en.wikipedia.org/wiki/es:Loopback "wikipedia:es:Loopback") como servidores de nombres, y configure openresolv para escribir la configuración de dnsmasq:

 `/etc/resolvconf.conf` 
```
# Utilizar el servidor de nombre local
name_servers="::1 127.0.0.1"

# Escribir los archivos de configuración extendida y de resolución de dnsmasq
dnsmasq_conf=/etc/dnsmasq-openresolv.conf
dnsmasq_resolv=/etc/dnsmasq-resolv.conf
```

Ejecute `resolvconf -u` para que se creen los archivos de configuración. Si los archivos no existen `dnsmasq.service` no podrá iniciarse.

Edite el archivo de configuración de dnsmasq para usar la configuración generada de openresolv:

```
# Leer la configuración generada por openresolv
conf-file=/etc/dnsmasq-openresolv.conf
resolv-file=/etc/dnsmasq-resolv.conf

```

##### Reenvío manual

Primero debe establecer las direcciones del servidor local como los únicos servidores de nombres en `/etc/resolv.conf`:

 `/etc/resolv.conf` 
```
nameserver ::1
nameserver 127.0.0.1

```

Consulte [Domain name resolution#Overwriting of /etc/resolv.conf](/index.php/Domain_name_resolution#Overwriting_of_/etc/resolv.conf "Domain name resolution") sobre cómo proteger el archivo `/etc/resolv.conf` de ser modificado.

Las direcciones del servidor DNS ascendente deben especificarse en el archivo de configuración de dnsmasq como `server=*server_address*`. También añada `no-resolv` para que dnsmasq no lea innecesariamente `/etc/resolv.conf`, que solo contiene las direcciones del equipo local.

```
no-resolv

# Servidores de nombres de Google, por ejemplo
server=8.8.8.8
server=8.8.4.4
```

Ahora las consultas DNS se resolverán con dnsmasq, solo se verificará si los servidores externos no pueden responder a la consulta desde su caché.

#### Añadir un dominio personalizado

Es posible agregar un dominio personalizado a los equipos de nuestra red (local):

```
local=/lan/
domain=lan

```

En este ejemplo, es posible enviar un ping a un servidor/dispositivo (por ejemplo, definido en el archivo `/etc/hosts` como `*hostname*.Lan`.

Descomente `expand-hosts` para añadir el dominio personalizado a las entradas del equipo:

```
expand-hosts

```

Sin esta configuración, deberá añadir el dominio a las entradas de `/etc/hosts`.

#### Prueba

Para realizar una prueba de velocidad de búsqueda, elija un sitio web que no se haya visitado desde que se inició dnsmasq (*drill* es parte del paquete [ldns](https://www.archlinux.org/packages/?name=ldns)):

```
$ drill archlinux.org | grep "Query time"

```

Al ejecutar nuevamente la orden, se usará la IP del DNS almacenada en la caché y se obtendrá un tiempo de búsqueda más rápido si dnsmasq está configurado correctamente:

 `$ drill archlinux.org | grep "Query time"` 
```
;; Query time: 18 msec

```
 `$ drill archlinux.org | grep "Query time"` 
```
;; Query time: 2 msec

```

Para comprobar si la validación de DNSSEC funciona, consulte [DNSSEC#Testing](/index.php/DNSSEC#Testing "DNSSEC").

### Servidor DHCP

De manera predeterminada, dnsmasq tiene la funcionalidad DHCP desactivada; si desea usarla, debe activarla. Aquí están las configuraciones importantes:

```
# Solo escucha la interfaz LAN de los enrutadores.
# Al hacerlo, se abre el puerto 53 para tcp/udp (para localhost)
# y el 67 para udp (para el resto):
interface=<LAN-NIC>

# dnsmasq abrirá el puerto 53 tcp/udp y el puerto 67 udp (para el resto)
# para ayudar con las interfaces dinámicas (asignación de ip dinámicas).
# Dnsmasq descartará el resto de solicitudes,
# aunque al sistema «paranoid» le gustaría cerrarlos
# y dejar al kernel manejarlas:
bind-interfaces

# Opcionalmente, establecer un nombre de dominio.
domain=example.com

# Establecer la puerta de enlace predeterminada.
dhcp-option=3,0.0.0.0

# Establecer servidores DNS para anunciar
dhcp-option=6,0.0.0.0

# Si su servidor dnsmasq también está haciendo el enrutamiento para su red,
# puede usar la opción 121 para forzar una ruta estática.
# x.x.x.x es la LAN de destino, yy es la notación CIDR (generalmente /24),
# y z.z.z.z es el host que hará el enrutamiento.
dhcp-option=121,x.x.x.x/yy,z.z.z.z

# Rango dinámico de direcciones IP para poner a disposición
# de la interfaz LAN del equipo y el tiempo de «lease».
# Lo ideal es establecer el tiempo de «lease» en 5 m solo al principio
# para probar que todo funciona bien antes de establecer registros más largos.
dhcp-range=192.168.111.50,192.168.111.100,12h

# Proporcionar contratos de «lease» de DHCP para IPv6 a través de Router Advertisements (RAs) para la máscara de subred aaaa:bbbb:cccc:dddd::/64
dhcp-range=aaaa:bbbb:cccc:dddd::,ra-only,infinite

# Si desea que dnsmasq asigne direcciones IP estáticas a algunos clientes,
# vincule las interfaces LAN de los equipos.
# Direcciones MAC:
dhcp-host=aa:bb:cc:dd:ee:ff,192.168.111.50
dhcp-host=aa:bb:cc:ff:dd:ee,192.168.111.51

```

Consulte [dnsmasq(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dnsmasq.8) para conocer más detalles.

#### Prueba

Desde un equipo que está conectado al que tiene dnsmasq, configúrelo para utilizar DHCP para la asignación automática de direcciones IP, luego intente iniciar sesión normalmente en la red.

Si inspecciona el archivo `/var/lib/misc/dnsmasq.leases` en el servidor, debería poder ver su asignación.

### Servidor TFTP

dnsmasq tiene un servidor [TFTP](/index.php/TFTP_(Espa%C3%B1ol) "TFTP (Español)") incorporado.

Para utilizarlo, cree un directorio para la raíz de TFTP (por ejemplo `/srv/tftp`) para colocar los archivos transferibles.

Para mayor seguridad, se recomienda utilizar el modo seguro TFTP de dnsmasq. En modo seguro, solo los archivos propiedad del usuario `dnsmasq` pasarán a través de TFTP. Necesitará hacer [chown](/index.php/Chown "Chown") a la raís de TFTP y a todos los archivos para que pertenezcan al usuario `dnsmasq` a fin de que pueda usar esta característica.

Active TFTP:

```
enable-tftp
tftp-root=/srv/tftp
tftp-secure

```

Consulte [dnsmasq(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dnsmasq.8) para más opciones.

### Servidor PXE

PXE requiere servidores DHCP y TFTP, ambas funciones pueden ser provistas por dnsmasq.

**Sugerencia:** dnsmasq puede ejecutarse en modo «proxy-DHCP» y agregar opciones de arranque PXE a una red con un servidor DHCP en ejecución:
```
interface=*enp0s0*
bind-dynamic
dhcp-range=*192.168.0.1*,proxy
```

1.  configurar [#Servidor TFTP](#Servidor_TFTP) y [#Servidor DHCP](#Servidor_DHCP);
2.  copiar y configurar un gestor de arranque compatible con PXE (por ejemplo, [PXELINUX](/index.php/PXELINUX "PXELINUX")) sobre la raíz TFTP;
3.  active PXE en `/etc/dnsmasq.conf`:

**Nota:**

*   las rutas de archivos son relativas a la raíz TFTP
*   si el archivo tiene un sufijo de `.0`, debe excluir el sufijo en las opciones de `pxe-service`

Para enviar simplemente un archivo:

```
dhcp-boot=lpxelinux.0

```

Para enviar un archivo dependiendo de la arquitectura del cliente:

```
pxe-service=x86PC, "PXELINUX (BIOS)", "bios/lpxelinux"
pxe-service=X86-64_EFI, "PXELINUX (EFI)", "efi64/syslinux.efi"

```

**Nota:** en caso de que `pxe-service` no funcione (especialmente para clientes basados ​​en UEFI), la combinación de `dhcp-match` y `dhcp-boot` puede hacer que funcione. Consulte [RFC4578](https://tools.ietf.org/html/rfc4578#section-2.1) para obtener más números `client-arch` para utilizarlos con el protocolo de arranque dhcp.

```
dhcp-match=set:efi-x86_64,option:client-arch,7
dhcp-match=set:efi-x86_64,option:client-arch,9
dhcp-match=set:efi-x86,option:client-arch,6
dhcp-match=set:bios,option:client-arch,0
dhcp-boot=tag:efi-x86_64,"efi64/syslinux.efi"
dhcp-boot=tag:efi-x86,"efi32/syslinux.efi"
dhcp-boot=tag:bios,"bios/lpxelinux.0"

```

Consulte [dnsmasq(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dnsmasq.8) para conocer más opciones.

El resto depende del [gestor de arranque](/index.php/Bootloader "Bootloader").

## Consejos y trucos

### Impedir que OpenDNS redirija las consultas de Google

Para evitar que OpenDNS redirija todas las consultas de Google a su propio servidor de búsqueda, añada a `/etc/dnsmasq.conf`:

 `server=/www.google.com/<ISP DNS IP>` 

### Anular direcciones

En algunos casos, como cuando esté operando un portal cautivo, puede ser útil resolver nombres de dominios específicos en un conjunto de direcciones codificadas. Esto se hace con la configuración `address`:

```
address=/example.com/1.2.3.4

```

Además, es posible devolver una dirección específica para todos los nombres de dominio que no son contestados desde `/etc/hosts` o DHCP utilizando un comodín especial:

```
address=/#/1.2.3.4

```

### Tener más de una instancia

Si queremos que dos o más servidores dnsmasq funcionen por interfaz(ces).

#### Estático

Para hacer esto de forma estática, servidor por interfaz, utilice las opciones `interface` y `bind-interface`. Esto obliga a dnsmasq a iniciarse en segundo lugar.

#### Dinámico

En este caso, podemos excluir por interfaz y enlazar cualquier otra:

```
except-interface=lo
bind-dynamic

```

**Nota:** esto está predeterminado en [libvirt](/index.php/Libvirt "Libvirt").

### Lista negra de dominios

Para poner en la lista negra dominios, es decir, responder consultas para ellos con NXDOMAIN, utilice la opción `address` sin especificar la dirección IP:

```
address=/blacklisted.example/
address=/another.blacklisted.example/

```

Para facilitar su uso, coloque la lista negra en un archivo separado, por ejemplo `/etc/dnsmasq.d/blacklist.conf` y cárguelo desde `/etc/dnsmasq.conf` con `conf-file=/etc/dnsmasq.d/blacklist.conf` o `conf-dir=conf-dir=/etc/dnsmasq.d/,*.conf`.

**Sugerencia:** se puede encontrar una lista de posibles fuentes para la lista negra en [OpenWrt's adblock package's README](https://github.com/openwrt/packages/blob/master/net/adblock/files/README.md).

## Véase también

*   [Caching Nameserver using dnsmasq, and a few other tips and tricks.](http://www.g-loaded.eu/2010/09/18/caching-nameserver-using-dnsmasq/)