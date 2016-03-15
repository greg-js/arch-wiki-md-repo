[DNSCrypt](http://dnscrypt.org/) encrypta y autentifica el tráfico DNS entre el usuario y la resolución DNS, previene la suplantación local de las consultas DNS, asegurando que las respuestas DNS son enviadas por el servidor de eleccion. [[1]](https://www.reddit.com/r/sysadmin/comments/2hn435/dnssec_vs_dnscrypt/ckuhcbu)

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
*   [3 Iniciar dnscrypt](#Iniciar_dnscrypt)
*   [4 Consejos y trucos](#Consejos_y_trucos)
    *   [4.1 DNSCrypt como un reenviador para un caché DNS local](#DNSCrypt_como_un_reenviador_para_un_cach.C3.A9_DNS_local)
        *   [4.1.1 Ejemplo: configuración para Unbound](#Ejemplo:_configuraci.C3.B3n_para_Unbound)
        *   [4.1.2 Ejemplo: configuración para dnsmasq](#Ejemplo:_configuraci.C3.B3n_para_dnsmasq)
    *   [4.2 Activar EDNS0](#Activar_EDNS0)
        *   [4.2.1 Test de EDNS0](#Test_de_EDNS0)

## Instalación

Instale el paquete [dnscrypt-proxy](https://www.archlinux.org/packages/?name=dnscrypt-proxy) disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

## Configuración

Cuando `dnscrypt-proxy.socket` esta activado. Acepta las peticiones entrantes en `127.0.0.1:53` a una resolucion DNS. La resolucion DNS por defecto para `dnscrypt-proxy.service` es *dnscrypt.eu-nl*. Los nombres del *resolver* compatibles son visibles en la primera columna de `/usr/share/dnscrypt-proxy/dnscrypt-resolvers.csv`.

Para cambiar el valor por defecto editar `dnscrypt-proxy.service`. Se recomienda elegis un proveedor creca de su ubicacion.

Modificar el archivo [Resolv.conf_(Español)](/index.php/Resolv.conf_(Espa%C3%B1ol) "Resolv.conf (Español)") y reemplazar el conjunto actual de direcciones del *resolver* con *localhost*:

```
nameserver 127.0.0.1

```

Otros programas pueden sobreescribir este ajuste; consulte [Resolv.conf_(Español)#Conservar_las_configuraciones_de_DNS](/index.php/Resolv.conf_(Espa%C3%B1ol)#Conservar_las_configuraciones_de_DNS "Resolv.conf (Español)") para mas detalles.

## Iniciar dnscrypt

Está disponible como un servicio de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"): `dnscrypt-proxy.service`

## Consejos y trucos

### DNSCrypt como un reenviador para un caché DNS local

Se recomienda ejecutar DNSCrypt como un reenviador para un caché DNS local, de lo contrario cada consulta única hará una ida y vuelta a la resolucion del upstream. Cualquier programa de almacenamiento de cache DNS local deberia trabajar. Los siguientes ejemplos muestran la configuracion para [Unbound](/index.php/Unbound "Unbound") y [dnsmasq](/index.php/Dnsmasq_(Espa%C3%B1ol) "Dnsmasq (Español)").

#### Ejemplo: configuración para Unbound

Configure [Unbound](/index.php/Unbound "Unbound") a su gusto (recuerde [ajustar /etc/resolv.conf para utilizar el servidor DNS local](/index.php/Unbound#Set_.2Fetc.2Fresolv.conf_to_use_the_local_DNS_server "Unbound")) y añada las siguientes líneas al final de la sección`server` en `/etc/unbound/unbound.conf`:

```
do-not-query-localhost: no
forward-zone:
  name: "."
  forward-addr: 127.0.0.1@40

```

**Nota:** El puerto 40 es dado como un ejemplo de cómo Unbound escucha por defecto el puerto 53, estos deben ser diferentes.

Inicie el servicio `unbound.service` de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"). Después configure DNScrypt para que coincidan la IP y el PORT presentes en `forward-zone` de Unbound en `/etc/conf.d/dnscrypt-proxy`:

```
DNSCRYPT_LOCALIP=127.0.0.1
DNSCRYPT_LOCALPORT=40

```

**Nota:** DNSCrypt debe ser iniciado antes que Unbound, así que incluya `unbound.service` en una línea `Before=` en la sección `[Unit]` de `dnscrypt-proxy.service`.

Reinicie `dnscrypt-proxy.service` y `unbound.service` para aplicar los cambios.

#### Ejemplo: configuración para dnsmasq

Configure dnsmasq como una [caché DNS local](/index.php/Dnsmasq_(Espa%C3%B1ol)#Configuraci.C3.B3n_de_la_cach.C3.A9_DNS "Dnsmasq (Español)"). He aquí la configuración básica para trabajar con DNSCrypt:

 `/etc/dnsmasq.conf` 
```
no-resolv
server=127.0.0.2#2053
listen-address=127.0.0.1
```

Si ha configurado DNSCrypt para usar un «resolver» con la validación DNSSEC activada, asegúrese de activarla también en dnsmasq:

 `/etc/dnsmasq.conf`  `proxy-dnssec` 

Configure DNSCrypt para escuchar en `127.0.0.2`, donde dnsmasq realizará la consulta:

 `/etc/conf.d/dnscrypt-proxy` 
```
DNSCRYPT_LOCALIP=127.0.0.2
DNSCRYPT_LOCALPORT=2053
```

Reinicie `dnscrypt-proxy.service` y `dnsmasq.service` para aplicar los cambios.

### Activar EDNS0

Los [mecanismos de extensión de DNS](https://en.wikipedia.org/wiki/es:Mecanismos_de_extension_de_DNS "wikipedia:es:Mecanismos de extension de DNS") permiten, entre otras cosas, que a un cliente especifique cuán grande puede ser una respuesta a través de UDP.

Agregue la siguiente línea a `/etc/resolv.conf`:

```
options edns0

```

También es posible que desee agregar el siguiente argumento a *dnscrypt-proxy*:

```
--edns-payload-size=<bytes>

```

El tamaño por defecto es **1252** bytes, con valores de hasta **4096** siguen siendo, supuestamente, seguros. Un valor por debajo o igual a **512** bytes desactivará este mecanismo, a menos que un cliente envíe un paquete con una sección OPT, proporcionando un tamaño de carga útil.

#### Test de EDNS0

Haga uso del [DNS Reply Size Test Server](https://www.dns-oarc.net/oarc/services/replysizetest), utilizando la herramienta de línea de órdenes *dig*, que forma parte del paquete [dnsutils](https://www.archlinux.org/packages/?name=dnsutils) disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"), para emitir una consulta TXT para el nombre *rs.dns-oarc.net*:

```
$ dig +short rs.dns-oarc.net txt

```

Con **EDNS0** funcionando, la salida debe ser similar a esta:

```
rst.x3827.rs.dns-oarc.net.
rst.x4049.x3827.rs.dns-oarc.net.
rst.x4055.x4049.x3827.rs.dns-oarc.net.
"2a00:d880:3:1::a6c1:2e89 DNS reply size limit is at least 4055 bytes"
"2a00:d880:3:1::a6c1:2e89 sent EDNS buffer size 4096"

```