**Estado de la traducción**
Este artículo es una traducción de [dnscrypt-proxy](/index.php/Dnscrypt-proxy "Dnscrypt-proxy"), revisada por última vez el **2019-11-06**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Dnscrypt-proxy&diff=0&oldid=570918) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[dnscrypt-proxy](https://github.com/jedisct1/dnscrypt-proxy) es un proxy DNS con soporte para los protocolos DNS cifrados, [DNS sobre HTTPS](https://en.wikipedia.org/wiki/es:DNS_mediante_HTTPS "wikipedia:es:DNS mediante HTTPS") y [DNSCrypt](https://dnscrypt.info/), que se puede utilizar para evitar [ataques de intermediario](https://en.wikipedia.org/wiki/es:Ataque_de_intermediario "wikipedia:es:Ataque de intermediario") y escuchas ilegales. *dnscrypt-proxy* es compatible también con [DNSSEC](/index.php/DNSSEC "DNSSEC").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 Poner en marcha](#Poner_en_marcha)
    *   [2.2 Seleccionar clientes DNS](#Seleccionar_clientes_DNS)
    *   [2.3 Desactivar cualquier servicio ligado al puerto 53](#Desactivar_cualquier_servicio_ligado_al_puerto_53)
    *   [2.4 Modificar resolv.conf](#Modificar_resolv.conf)
    *   [2.5 Iniciar el servicio de systemd](#Iniciar_el_servicio_de_systemd)
*   [3 Consejos y trucos](#Consejos_y_trucos)
    *   [3.1 Configuración de la caché DNS local](#Configuración_de_la_caché_DNS_local)
        *   [3.1.1 Cambiar el puerto](#Cambiar_el_puerto)
        *   [3.1.2 Ejemplo de configuraciones para una caché DNS local](#Ejemplo_de_configuraciones_para_una_caché_DNS_local)
            *   [3.1.2.1 Unbound](#Unbound)
            *   [3.1.2.2 dnsmasq](#dnsmasq)
            *   [3.1.2.3 pdnsd](#pdnsd)
    *   [3.2 Sandboxing](#Sandboxing)
    *   [3.3 Activar EDNS0](#Activar_EDNS0)
        *   [3.3.1 Test de EDNS0](#Test_de_EDNS0)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [dnscrypt-proxy](https://www.archlinux.org/packages/?name=dnscrypt-proxy).

## Configuración

### Poner en marcha

El servicio se puede iniciar de dos maneras mutuamente excluyentes (es decir, solo se puede activar uno de los dos):

*   Con el archivo `.service`.

**Nota:** la opción `listen_addresses` debe configurarse (por ejemplo, `listen_addresses = ['127.0.0.1:53', '[::1]:53']`) en el archivo de configuración cuando se utiliza el archivo `.service`.

*   Mediante la activación del `.socket`.

**Nota:** al utilizar la activación del socket, la opción `listen_addresses` se debe dejar vacía (es decir, `listen_addresses = [ ]`) en el archivo de configuración, ya que systemd se ocupa de la configuración del socket.

### Seleccionar clientes DNS

Al dejar `server_names` comentado en el archivo de configuración `/etc/dnscrypt-proxy/dnscrypt-proxy.toml`, *dnscrypt-proxy* elegirá el servidor más rápido de entre los ya configurados en `[sources]` [[1]](https://github.com/jedisct1/dnscrypt-proxy/wiki/Configuration#an-example-static-server-entry). Las listas de dichos servidores se descargarán, verificarán y actualizarán automáticamente. [[2]](https://github.com/jedisct1/dnscrypt-proxy/wiki/Configuration-Sources#what-is-the-point-of-these-lists). Por lo tanto, la configuración de un conjunto específico de servidores es opcional.

Para establecer manualmente qué servidor utilizar, edite `/etc/dnscrypt-proxy/dnscrypt-proxy.toml` y elimine el comentario de la variable `server_names`, seleccionando uno o más de los servidores. Por ejemplo, para usar los servidores de Cloudflare:

```
server_names = ['cloudflare', 'cloudflare-ipv6']

```

Una lista completa de clientes DNS («*resolver*») se encuentra en la [página upstream](https://download.dnscrypt.info/resolvers-list/v2/public-resolvers.md) o [Github](https://raw.githubusercontent.com/DNSCrypt/dnscrypt-resolvers/master/v2/public-resolvers.md). Si *dnscrypt-proxy* se ejecutó con éxito en el sistema anteriormente, `/var/cache/dnscrypt-proxy/public-resolvers.md` también contendrá una lista. Mire la descripción de los servidores que validan [DNSSEC](/index.php/DNSSEC_(Espa%C3%B1ol) "DNSSEC (Español)"), sin registro y sin cesura. Estos requisitos se pueden configurar de forma global con las opciones `require_dnssec`, `require_nolog`, `require_nofilter`.

### Desactivar cualquier servicio ligado al puerto 53

**Sugerencia:** si utiliza [#Unbound](#Unbound) como su caché DNS local, esta sección se puede ignorar, ya que *unbound* se ejecuta en el puerto 53 de forma predeterminada.

Para ver si algún programa está usando el puerto 53, ejecute:

```
 $ ss -lp 'sport = :domain'

```

Si el resultado contiene más de una línea a parte de los nombres de las columnas, debe desactivar cualquier servicio que esté utilizando el puerto 53\. Un servicio común que lo utiliza es `systemd-resolved.service`, ([NetworkManager#Unit dbus-org.freedesktop.resolve1.service not found](/index.php/NetworkManager#Unit_dbus-org.freedesktop.resolve1.service_not_found "NetworkManager")), pero otros administradores de red pueden tener componentes análogos. Puede continuar una vez que la orden anterior imprima solo la siguiente línea:

```
 Netid               State                 Recv-Q                Send-Q                                 Local Address:Port                                   Peer Address:Port

```

### Modificar resolv.conf

Modifique el archivo [resolv.conf](/index.php/Domain_name_resolution_(Espa%C3%B1ol) "Domain name resolution (Español)") y reemplace el conjunto vigente de direcciones de resolución con la dirección para *localhost* y las opciones [[3]](https://github.com/jedisct1/dnscrypt-proxy/wiki/Installation-linux#step-4-change-the-system-dns-settings):

```
nameserver ::1
nameserver 127.0.0.1
options edns0 single-request-reopen

```

Otros programas pueden sobrescribir esta configuración; consulte [resolv.conf#Overwriting of /etc/resolv.conf](/index.php/Resolv.conf#Overwriting_of_/etc/resolv.conf "Resolv.conf") para obtener más detalles.

### Iniciar el servicio de systemd

Finalmente, [inicie/active](/index.php/Start/enable "Start/enable") la unidad `dnscrypt-proxy.service` o `dnscrypt-proxy.socket`, dependiendo del método que elija.

## Consejos y trucos

### Configuración de la caché DNS local

**Sugerencia:** *dnscrypt-proxy* puede almacenar en caché las entradas sin depender de otro programa. Esta función está activada de manera predeterminada con la línea `cache = true` en el archivo de configuración *dnscrypt-proxy*

Se recomienda ejecutar *dnscrypt-proxy* como un reenviador a una caché de DNS local, si no se utiliza la función caché de *dnscrypt-proxy*; de lo contrario, cada consulta hará un viaje de ida y vuelta al servidor de resolución ascendente. Cualquier programa de almacenamiento DNS local debería funcionar. Además de configurar *dnscrypt-proxy*, debe configurar su programa de caché de DNS local.

#### Cambiar el puerto

Para reenviar consultas desde una caché del DNS local, *dnscrypt-proxy* debe escuchar en un puerto diferente del predeterminado `53`, ya que la caché DNS necesita escuchar en el puerto `53` y la consulta de *dnscrypt-proxy* debe hacerse sobre un puerto diferente. El número de puerto `53000` se usa como ejemplo en esta sección. En este ejemplo, el número de puerto es mayor que 1024 por lo que no es necesario que *dnscrypt-proxy* sea ejecutado por root.

Hay dos métodos para cambiar el puerto predeterminado:

**Método socket**

[Modifique](/index.php/Edit_(Espa%C3%B1ol) "Edit (Español)") `dnscrypt-proxy.socket` con los siguientes contenidos:

```
[Socket]
ListenStream=
ListenDatagram=
ListenStream=127.0.0.1:53000
ListenStream=[::1]:53000
ListenDatagram=127.0.0.1:53000
ListenDatagram=[::1]:53000

```

Cuando las consultas se reenvían desde la caché del DNS local al puerto `53000`, `dnscrypt-proxy.socket` iniciará `dnscrypt-proxy.service`.

**Método service**

Modifique la opción `listen_addresses` en `/etc/dnscrypt-proxy/dnscrypt-proxy.toml` con lo siguiente:

```
listen_addresses = ['127.0.0.1:53000', '[::1]:53000']

```

#### Ejemplo de configuraciones para una caché DNS local

Las siguientes configuraciones deberían funcionar con *dnscrypt-proxy* y asumir que está escuchando en el puerto `53000`.

##### Unbound

Configure [Unbound](/index.php/Unbound "Unbound") a su gusto (en particular, consulte [Unbound#Local DNS server](/index.php/Unbound#Local_DNS_server "Unbound")) y añada las siguientes líneas al final de la sección `server` en `/etc/unbound/unbound.conf`:

```
  do-not-query-localhost: no
forward-zone:
  name: "."
  forward-addr: ::1@53000
  forward-addr: 127.0.0.1@53000

```

**Sugerencia:** si está configurando un servidor, añada `interface: 0.0.0.0@53` y `access-control: *red*/*máscara-de-subred* allow` en la sección `server:` para que los otros equipos puedan conectarse al servidor. Un cliente debe configurarse con `nameserver *dirección-de-su-servidor*` en `/etc/resolv.conf`.

[Reinicie](/index.php/Restart_(Espa%C3%B1ol) "Restart (Español)") `unbound.service` para aplicar los cambios.

##### dnsmasq

Configure dnsmasq como un [caché DNS local](/index.php/Dnsmasq_(Espa%C3%B1ol)#Servidor_DNS "Dnsmasq (Español)"). La configuración básica para trabajar con *dnscrypt-proxy* es:

 `/etc/dnsmasq.conf` 
```
no-resolv
server=::1#53000
server=127.0.0.1#53000
listen-address=::1,127.0.0.1
```

Si configuró *dnscrypt-proxy* para usarlo como un «resolver» con la validación [DNSSEC](/index.php/DNSSEC_(Espa%C3%B1ol) "DNSSEC (Español)"), asegúrese de activarla también en dnsmasq:

 `/etc/dnsmasq.conf` 
```
conf-file=/usr/share/dnsmasq/trust-anchors.conf
dnssec
dnssec-check-unsigned
```

Reinicie `dnsmasq.service` para aplicar los cambios.

##### pdnsd

Instale [pdnsd](/index.php/Pdnsd "Pdnsd"). Una configuración básica para trabajar con *dnscrypt-proxy* es:

 `/etc/pdnsd.conf` 
```
global {
    perm_cache = 1024;
    cache_dir = "/var/cache/pdnsd";
    run_as = "pdnsd";
    server_ip = 127.0.0.1;
    status_ctl = on;
    query_method = udp_tcp;
    min_ttl = 15m;       # Retain cached entries at least 15 minutes.
    max_ttl = 1w;        # One week.
    timeout = 10;        # Global timeout option (10 seconds).
    neg_domain_pol = on;
    udpbufsize = 1024;   # Upper limit on the size of UDP messages.
}

server {
    label = "dnscrypt-proxy";
    ip = 127.0.0.1;
    port = 53000;
    timeout = 4;
    proxy_only = on;
}

source {
    owner = localhost;
    file = "/etc/hosts";
}
```

Reinicie `pdnsd.service` para aplicar los cambios.

### Sandboxing

**Nota:** **(del traductor):** el «*sandboxing*» o [aislamiento de procesos](https://en.wikipedia.org/wiki/es:Aislamiento_de_procesos "wikipedia:es:Aislamiento de procesos") es un mecanismo para ejecutar programas con seguridad y de manera separada, en este caso el servicio «dnscrypt-proxy.service».

[Edite](/index.php/Edit_(Espa%C3%B1ol) "Edit (Español)") `dnscrypt-proxy.service` para incluir las siguientes líneas:

```
[Service]
CapabilityBoundingSet=CAP_IPC_LOCK CAP_SETGID CAP_SETUID CAP_NET_BIND_SERVICE
ProtectSystem=strict
ProtectHome=true
ProtectKernelTunables=true
ProtectKernelModules=true
ProtectControlGroups=true
PrivateTmp=true
PrivateDevices=true
MemoryDenyWriteExecute=true
NoNewPrivileges=true
RestrictRealtime=true
RestrictAddressFamilies=AF_INET AF_INET6
SystemCallArchitectures=native
SystemCallFilter=~@clock @cpu-emulation @debug @keyring @ipc @module @mount @obsolete @raw-io

```

Consulte [systemd.exec(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.exec.5) y [Systemd (Español)#Entornos seguros para probar aplicaciones](/index.php/Systemd_(Espa%C3%B1ol)#Entornos_seguros_para_probar_aplicaciones "Systemd (Español)") para obtener más información.

### Activar EDNS0

Los [mecanismos de extensión de DNS](https://en.wikipedia.org/wiki/es:Mecanismos_de_extension_de_DNS "wikipedia:es:Mecanismos de extension de DNS") permiten, entre otras cosas, que un cliente especifique cuán grande puede ser una respuesta a través de UDP.

Añada la siguiente línea a `/etc/resolv.conf`:

```
options edns0

```

También es posible que desee agregar el siguiente argumento a `/etc/dnscrypt-proxy.conf`:

```
EDNSPayloadSize *<bytes>*

```

Donde *<bytes>* es un número, El tamaño por defecto comienza en **1252**, con valores de hasta **4096** bytes siguen siendo, supuestamente, seguros. Un valor por debajo o igual a **512** bytes desactivará este mecanismo, a menos que un cliente envíe un paquete con una sección OPT, proporcionando un tamaño de carga útil.

#### Test de EDNS0

Haga uso del [DNS Reply Size Test Server](https://www.dns-oarc.net/oarc/services/replysizetest), utilizando la herramienta de línea de órdenes *drill* para emitir una consulta TXT para el nombre *rs.dns-oarc.net*:

```
$ drill rs.dns-oarc.net TXT

```

Con **EDNS0** funcionando, la salida de la «answer section» debe ser similar a esta:

```
rst.x3827.rs.dns-oarc.net.
rst.x4049.x3827.rs.dns-oarc.net.
rst.x4055.x4049.x3827.rs.dns-oarc.net.
"2a00:d880:3:1::a6c1:2e89 DNS reply size limit is at least 4055 bytes"
"2a00:d880:3:1::a6c1:2e89 sent EDNS buffer size 4096"

```