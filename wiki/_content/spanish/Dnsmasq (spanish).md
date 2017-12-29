**dnsmasq** proporciona servicios como caché DNS y como servidor DHCP. Como un servidor de nombres de dominio (DNS), puede almacenar en caché las consultas DNS para mejorar las velocidades de conexión a los sitios visitados anteriormente, y, como un servidor DHCP, [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) puede ser utilizado para proporcionar direcciones IP internas y rutas a los equipos de una LAN. Uno, o ambos de estos servicios, se pueden implementar. dnsmasq es considerado ligero y fácil de configurar; está diseñado para su uso en un ordenador personal o para su uso en una red con menos de 50 ordenadores. También viene con un servidor [PXE](/index.php/PXE "PXE").

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración de la caché DNS](#Configuraci.C3.B3n_de_la_cach.C3.A9_DNS)
    *   [2.1 Archivo de direcciones DNS](#Archivo_de_direcciones_DNS)
        *   [2.1.1 resolv.conf](#resolv.conf)
            *   [2.1.1.1 Más de tres servidores de nombres](#M.C3.A1s_de_tres_servidores_de_nombres)
        *   [2.1.2 dhcpcd](#dhcpcd)
        *   [2.1.3 dhclient](#dhclient)
    *   [2.2 NetworkManager](#NetworkManager)
        *   [2.2.1 Otros métodos](#Otros_m.C3.A9todos)
*   [3 Configuración del servidor DHCP](#Configuraci.C3.B3n_del_servidor_DHCP)
*   [4 Iniciar el demonio](#Iniciar_el_demonio)
*   [5 Test](#Test)
    *   [5.1 Caching DNS](#Caching_DNS)
    *   [5.2 Servidor DHCP](#Servidor_DHCP)
*   [6 Consejos y trucos](#Consejos_y_trucos)
    *   [6.1 Prevenir que OpenDNS redirija consultas a Google](#Prevenir_que_OpenDNS_redirija_consultas_a_Google)
    *   [6.2 Visualizar leases](#Visualizar_leases)
    *   [6.3 Agregar un dominio personalizado](#Agregar_un_dominio_personalizado)

## Instalación

[Instale](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

## Configuración de la caché DNS

Para configurar dnsmasq como un demonio de almacenamiento de DNS en la caché de un único equipo, edite `/etc/dnsmasq.conf` y descomente la directiva `listen-address`, añadiendo la dirección IP localhost:

```
listen-address=127.0.0.1

```

Para utilizar este equipo a fin de que otros equipos conectados a la misma red puedan consultar con su dirección IP LAN:

```
listen-address=192.168.1.1    # IP de ejemplo

```

Se recomienda que utilice una IP LAN estática en este último caso.

### Archivo de direcciones DNS

Después de configurar dnsmasq necesitará configurar el cliente DHCP para anteponer la dirección de localhost a las direcciones DNS presentes en `/etc/resolv.conf`. Esto hará que todas las consultas se envíen a dnsmasq antes de tratar de resolverlas a través de un DNS externo. Después de configurar el cliente DHCP necesitará reiniciar la red para que los cambios surtan efecto.

#### resolv.conf

La opción principal consiste en una configuración pura de `resolv.conf`. Para ello, basta con poner el primer servidor de nombres en `/etc/resolv.conf` apuntando a localhost:

 `/etc/resolv.conf` 
```
nameserver 127.0.0.1
# Servidores de nombres externos
...

```

Ahora las consultas DNS serán resueltas, en primer lugar, con dnsmasq, acudiendo únicamente a los servidores externos si dnsmasq no puede resolver la consulta. [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd), por desgracia, tiende a sobrescribir, por defecto, el archivo `/etc/resolv.conf`, así que, si usa DHCP, es una buena idea proteger `/etc/resolv.conf` . Para ello, agregue `nohook resolv.conf` en el archivo de configuración de dhcpcd:

 `/etc/dhcpcd.conf` 
```
...
nohook resolv.conf
```

También es posible proteger contra escritura su resolv.conf con:

```
# chattr +i /etc/resolv.conf

```

##### Más de tres servidores de nombres

Una limitación de Linux a la hora de manejar las consultas DNS es que solo pueden utilizarse un máximo de tres servidores de nombres presentes en `resolv.conf`. Como solución alternativa, puede hacer de localhost el único servidor de nombres en `resolv.conf` y, luego, crear un archivo separado, `resolv-file`, para sus servidores de nombres externos. Para ello, en primer lugar, cree un nuevo archivo resolv para dnsmasq:

 `/etc/resolv.dnsmasq.conf` 
```
# Servidores de nombres de Google, por ejemplo
nameserver 8.8.8.8
nameserver 8.8.4.4

```

Y, luego, edite `/etc/dnsmasq.conf`, para utilizar el nuevo archivo resolv:

 `/etc/dnsmasq.conf` 
```
...
resolv-file=/etc/resolv.dnsmasq.conf
...

```

#### dhcpcd

[dhcpcd](/index.php/Dhcpcd "Dhcpcd") tiene la capacidad de anteponer o posponer servidores de nombres a los presentes en `/etc/resolv.conf` mediante la creación (o edición) del archivo `/etc/resolv.conf.head` y `/etc/resolv.conf.tail`, respectivamente:

```
echo "nameserver 127.0.0.1" > /etc/resolv.conf.head

```

#### dhclient

Para [dhclient](https://www.archlinux.org/packages/?name=dhclient), descomente en `/etc/dhclient.conf`:

```
prepend domain-name-servers 127.0.0.1;

```

### NetworkManager

[NetworkManager](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)") tiene la capacidad de iniciar *dnsmasq* desde su archivo de configuración. Añada la opción `dns=dnsmasq` a `NetworkManager.conf` en la sección `[main]`, después de desactivar `dnsmasq.service` para que puede ser cargado al comienzo por [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"):

 `/etc/NetworkManager/NetworkManager.conf` 
```
[main]
plugins=keyfile
dns=dnsmasq

```

Se pueden crear configuraciones personalizadas para *dnsmasq*, mediante la creación de archivos de configuración en `/etc/NetworkManager/dnsmasq.d/`. Por ejemplo, para cambiar el tamaño de la memoria caché DNS (que se almacena en RAM):

 `/etc/NetworkManager/dnsmasq.d/cache`  `cache-size=1000` 

Cuando *dnsmasq* sea iniciado por `NetworkManager`, el archivo de configuración de este directorio será usado en lugar del archivo de configuración predeterminado.

**Sugerencia:** Este método puede permitir que active los ajustes de DNS personalizados en dominios particulares. Por ejemplo: `server=/example1.com/exemple2.com/xx.xxx.xxx.x` cambia la primera dirección DNS a `xx.xxx.xxx.xx` mientras se navega únicamente por los sitios webs siguientes: `example1.com, example2.com`. Este método es preferible a una configuración global de DNS cuando se utilizan servidores de nombres DNS particulares que carecen de rapidez, estabilidad, privacidad y seguridad.

#### Otros métodos

Otra opción es ajustando la configuración de NetworkManager (normalmente haciendo clic con el botón secundario del ratón en el applet) e introduciendo los valores manualmente. La configuración variará en función del tipo de front-end utilizado; el proceso consistirá, generalmente, en hacer clic con el botón secundario sobre el applet, editar (o crear) un perfil, y, por último, elegir el tipo DHCP como «Automatico (especificar direcciones)». Necesitará conocer las direcciónes DNS a introducir y, normalmente, tendrá este formato: `127.0.0.1, DNS-server-one, ...`.

## Configuración del servidor DHCP

Por defecto, dnsmasq viene con la funcionalidad DHCP desactivada, si quiere usarla, hay que activarla en (`/etc/dnsmasq.conf`). He aquí los ajustes importantes:

```
# Only listen to routers' LAN NIC.  Doing so opens up tcp/udp port 53 to
# localhost and udp port 67 to world:
interface=<LAN-NIC>

# dnsmasq will open tcp/udp port 53 and udp port 67 to world to help with
# dynamic interfaces (assigning dynamic ips). Dnsmasq will discard world
# requests to them, but the paranoid might like to close them and let the 
# kernel handle them:
bind-interfaces

# Dynamic range of IPs to make available to LAN pc
dhcp-range=192.168.111.50,192.168.111.100,12h

# If you’d like to have dnsmasq assign static IPs, bind the LAN computer's
# NIC MAC address:
dhcp-host=aa:bb:cc:dd:ee:ff,192.168.111.50

```

## Iniciar el demonio

Para cargar dnsmasq en el arranque:

 `# systemctl enable dnsmasq` 

Para iniciar dnsmasq inmediatamente:

 `# systemctl start dnsmasq` 

Para ver si dnsmasq se ha iniciado correctamente, compruebe el «journal» del sistema:

 `$ journalctl -u dnsmasq` 

También será necesario reiniciar la red si se ha creado un archivo `/etc/resolv.conf` nuevo para el cliente DHCP.

## Test

### Caching DNS

Para hacer una prueba de velocidad de búsqueda, elija un sitio web que no haya visitado desde que dnsmasq se inició (*dig* es parte del paquete [bind-tools](https://www.archlinux.org/packages/?name=bind-tools)):

```
$ dig archlinux.org | grep "Query time"

```

Al ejecutar la orden de nuevo, se utilizará la IP DNS almacenada en caché y el resultado será un tiempo de búsqueda más rápido, si dnsmasq está configurado correctamente:

 `$ dig archlinux.org | grep "Query time"` 
```
;; Query time: 18 msec

```
 `$ dig archlinux.org | grep "Query time"` 
```
;; Query time: 2 msec

```

### Servidor DHCP

Desde un ordenador que esté conectado a otro donde se esté ejecutando dnsmasq, puede configurar aquel para que obtenga la asignación automática de direcciones IP mediante DHCP. A continuación, intente acceder a la red con normalidad.

## Consejos y trucos

### Prevenir que OpenDNS redirija consultas a Google

Para evitar que OpenDNS redirija todas las consultas a Google a su propio servidor de búsqueda, añada a `/etc/dnsmasq.conf`:

 `server=/www.google.com/<ISP DNS IP>` 

### Visualizar leases

 `$ cat /var/lib/misc/dnsmasq.leases` 

### Agregar un dominio personalizado

Es posible añadir un dominio personalizado a los hosts en su red (local):

```
local=/home.lan/
domain=home.lan

```

En este ejemplo, es posible hacer ping a un host/device (por ejemplo, definido en su archivo hots) como `hostname.home.lan`.

Descomente `expand-hosts` para agregar el dominio personalizado a las entradas de hosts:

```
expand-hosts

```

Sin este ajuste, tendrá que agregar el dominio a las entradas de /etc/hosts.