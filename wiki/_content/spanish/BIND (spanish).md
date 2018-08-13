Artículos relacionados

*   [DNSCrypt](/index.php/DNSCrypt "DNSCrypt")
*   [dnsmasq](/index.php/Dnsmasq "Dnsmasq")
*   [Pdnsd](/index.php/Pdnsd "Pdnsd")
*   [Unbound](/index.php/Unbound "Unbound")
*   [PowerDNS](/index.php/PowerDNS "PowerDNS")

**Estado de la traducción:** este artículo es una versión traducida de [Domain Name System (Español)](/index.php?title=Domain_Name_System_(Espa%C3%B1ol)&action=edit&redlink=1 "Domain Name System (Español) (page does not exist)"). Fecha de la última traducción/revisión: **2017-01-24**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Domain_Name_System_(Espa%C3%B1ol)&diff=0&oldid={{{3}}}).

BIND (*Berkeley Internet Name Daemon*) es la implementación de referencia del protocolo DNS (*Domain Name System*).

**Note:** The organization developing BIND is serving security notices to paying customers up to four days before Linux distributions or the general public.[[1]](https://kb.isc.org/article/AA-00861/0/ISC-Software-Defect-and-Security-Vulnerability-Disclosure-Policy.html)

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Redireccionamiento](#Redireccionamiento)
*   [3 Plantilla de configuración para ejecutar un dominio](#Plantilla_de_configuraci.C3.B3n_para_ejecutar_un_dominio)
    *   [3.1 1\. Crear un archivo de zona](#1._Crear_un_archivo_de_zona)
    *   [3.2 2\. Configurar un servidor maestro](#2._Configurar_un_servidor_maestro)
    *   [3.3 3\. Configurarlo como el servidor DNS por defecto](#3._Configurarlo_como_el_servidor_DNS_por_defecto)
*   [4 Configurar BIND para servir zonas firmadas con DNSSEC](#Configurar_BIND_para_servir_zonas_firmadas_con_DNSSEC)
*   [5 Escuchar automáticamente nuevas interfaces](#Escuchar_autom.C3.A1ticamente_nuevas_interfaces)
*   [6 Ejecutar BIND en un entorno chroot](#Ejecutar_BIND_en_un_entorno_chroot)
    *   [6.1 Crear un sistema de archivos para la jaula chroot](#Crear_un_sistema_de_archivos_para_la_jaula_chroot)
    *   [6.2 Archivo de servicio](#Archivo_de_servicio)
*   [7 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

Los siguientes pasos indican cómo instalar una configuración básica de BIND como servidor local DNS de solo caché.

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [bind](https://www.archlinux.org/packages/?name=bind) desde los repositorios oficiales.

Opcionalmente, edite `/etc/named.conf`, y añada la siguiente línea en la sección de opciones (options), para permitir únicamente conexiones de localhost:

```
listen-on { 127.0.0.1; };

```

Edite [resolv.conf](/index.php/Resolv.conf "Resolv.conf") para usar el servidor local DNS, 127.0.0.1.

Inicie `named.service` con [systemd](/index.php/Systemd_(Espa%C3%B1ol)#Uso_b.C3.A1sico_de_systemctl "Systemd (Español)").

## Redireccionamiento

Cuando BIND actúa como un servidor de redireccionamiento DNS, almacena por una parte memoria caché de las búsquedas DNS ya realizadas, y por otra redirigirá las peticiones DNS no guardadas en caché a otros servidores DNS que se hayan definido, como podría ser el servidor DNS de nuestro ISP u otros servicios DNS globales como OpenNIC.

Para configurar el redireccionamiento DNS, basta con añadir las siguientes líneas a `/etc/named.conf` en la secciones de opciones globales (*options*) o en una sección de zona específica, y cambiar la dirección IP de acuerdo con la del servidor DNS que deseamos emplear.

```
options {
 listen-on { 192.168.66.1; };
 forwarders { 8.8.8.8; 8.8.4.4; };
};

```

Tras realizar este cambio, es necesario [reiniciar](/index.php/Systemd_(Espa%C3%B1ol)#Uso_b.C3.A1sico_de_systemctl "Systemd (Español)") `named.service`.

## Plantilla de configuración para ejecutar un dominio

Este es un sencillo tutorial para configurar una servidor DNS en una red doméstica con bind. Usaremos "domain.tld" como nuestro dominio.

Para ver ejemplo más elaborados, consúltese [Two-in-one DNS server with BIND9](http://www.howtoforge.com/two_in_one_dns_bind9_views).

### 1\. Crear un archivo de zona

```
# nano /var/named/domain.tld.zone

```

```
$TTL 7200
; domain.tld
@       IN      SOA     ns01.domain.tld. postmaster.domain.tld. (
                                        2007011601 ; Serial
                                        28800      ; Refresh
                                        1800       ; Retry
                                        604800     ; Expire - 1 week
                                        86400 )    ; Minimum
                IN      NS      ns01
                IN      NS      ns02
ns01            IN      A       0.0.0.0
ns02            IN      A       0.0.0.0
localhost       IN      A       127.0.0.1
@               IN      MX 10   mail
imap            IN      CNAME   mail
smtp            IN      CNAME   mail
@               IN      A       0.0.0.0
www             IN      A       0.0.0.0
mail            IN      A       0.0.0.0
@               IN      TXT     "v=spf1 mx"

```

$TTL define el tiempo de vida en segundos por defecto para todos los registros de todos los tipos. En este ejemplo es de 2 horas.

**El número de serie (*Serial*) debe incrementarse manualmente antes de reiniciar named cada vez que se cambie un registro en la zona.** De lo contrario los servidores esclavos no retransmitirán la zona, ya que para ello requieren un número serie mayor que el de la última versión de la zona que transfirieron.

### 2\. Configurar un servidor maestro

Añade tu zona a `/etc/named.conf`:

```
zone "domain.tld" IN {
        type master;
        file "domain.tld.zone";
        allow-update { none; };
        notify no;
};

```

[Inicie](/index.php/Systemd_(Espa%C3%B1ol)#Uso_b.C3.A1sico_de_systemctl "Systemd (Español)") `named.service`.

Alternativamente, [recargue](/index.php/Systemd_(Espa%C3%B1ol)#Uso_b.C3.A1sico_de_systemctl "Systemd (Español)") los archivos de configuración. Esta última opción mantendrá el servidor disponible mientras se ejecuta el cambio.

### 3\. Configurarlo como el servidor DNS por defecto

Si estamos ejecutando nuestro propio servidor DNS, podríamos querer usarlo no solo para redirigir peticiones DNS, sino para realizar todas las búsquedas DNS. Esto requiere la capacidad de hacer búsquedas *recursivas*. Para prevenir ataques de amplificación de DNS ([DNS Amplification Attacks](https://www.us-cert.gov/ncas/alerts/TA13-088A)), la búsqueda recursiva está desactivada por defecto en la mayor parte de las configuraciones. El fichero Arch `/etc/named.conf` por defecto solo permite habilitar la recursión en la interfaz de circuito cerrado (*loopback*) del sistema.

```
allow-recursion { 127.0.0.1; };

```

Por lo tanto, para permitir búsquedas DNS para nuestro equipo, el fichero [resolv.conf](/index.php/Resolv.conf "Resolv.conf") debe incluir 127.0.0.1 como servidor de nombres. Consulte [Conservar las configuraciones de DNS](/index.php/Resolv.conf_(Espa%C3%B1ol)#Conservar_las_configuraciones_de_DNS "Resolv.conf (Español)") para prevenir que este fichero sea reescrito.

Para proveer un servicio de nombres a nuestra red local, por ejemplo 192.168.0, debemos añadir el rango apropiado de direcciones IP a `/etc/named.conf`:

```
allow-recursion { 192.168.0.0/24; 127.0.0.1; };

```

## Configurar BIND para servir zonas firmadas con DNSSEC

*   [http://www.dnssec.net/practical-documents](http://www.dnssec.net/practical-documents)
    *   [http://www.cymru.com/Documents/secure-bind-template.html](http://www.cymru.com/Documents/secure-bind-template.html) **(plantilla de configuración)**
    *   [http://www.bind9.net/manuals](http://www.bind9.net/manuals)
    *   [http://www.bind9.net/BIND-FAQ](http://www.bind9.net/BIND-FAQ)
*   [http://blog.techscrawl.com/2009/01/13/enabling-dnssec-on-bind/](http://blog.techscrawl.com/2009/01/13/enabling-dnssec-on-bind/)
*   O use un mecanismo externo tal como OpenDNSSEC (cambio de clave completamente automático)

## Escuchar automáticamente nuevas interfaces

Por defecto, bind hace un escaneo en búsqueda de nuevas interfaces cada hora, y deja de escuchar aquellas que dejan de existir. Este comportamiento se puede modificar añadiendo el parámetro:

```
interface-interval <rescan-timeout-in-minutes>;

```

en la sección de opciones de `named.conf`, con un valor máximo de 28 días (40320 min). También se puede desactivar esta caraterística con el valor 0.

A continuación, reniciamos el servicio.

## Ejecutar BIND en un entorno chroot

Ejecutar en un entorno [chroot](/index.php/Chroot "Chroot") mejora la seguridad del servidor DNS.

### Crear un sistema de archivos para la jaula chroot

En primer lugar, debemos crear un lugar donde contener la jaula chroot, como el directorio `/srv/named` por ejemplo, y disponer todos los archivos necesarios para el funcionamiento de BIND en el mismo.

```
 mkdir -p /srv/named/{dev,etc,usr/lib/engines,var/{run,log,named}}
 # Copy over required system files
 cp -av /etc/{localtime,named.conf} /srv/named/etc/
 cp -av /usr/lib/engines/* /srv/named/usr/lib/engines/
 cp -av /var/named/* /srv/named/var/named/.
 # Set up required dev nodes
 mknod /srv/named/dev/null c 1 3
 mknod /srv/named/dev/random c 1 8
 # Set Ownership of the files
 chown -R named:named /srv/named

```

Estas operaciones deberían crear el sistema de archivos necesario para la jaula chroot.

### Archivo de servicio

A continuación, debemos crear un nuevo archivo de servicio que fuerce bind a ejecutarse dentro de chroot.

```
 cp -av /usr/lib/systemd/system/named.service /etc/systemd/system/named-chroot.service

```

editando cómo el servicio llama a bind.

 `/etc/systemd/system/named-chroot.service` 
```
  ExecStart=/usr/bin/named -4 -f -u named -t "/srv/named"

```

Ahora, reload systemd `systemctl daemon-reload`. Entonces [inicie](/index.php/Systemd_(Espa%C3%B1ol)#Uso_b.C3.A1sico_de_systemctl "Systemd (Español)") `named-chroot.service`

## Véase también

*   [BIND 9 DNS Administration Reference Book](http://www.reedmedia.net/books/bind-dns/)
*   [DNS and BIND by Cricket Liu and Paul Albitz](http://shop.oreilly.com/product/9780596100575.do)
*   [Pro DNS and BIND](http://www.netwidget.net/books/apress/dns/intro.html)
*   [Internet Systems Consortium, Inc. (ISC)](http://www.isc.org/)
*   [DNS Glossary](http://www.menandmice.com/knowledgehub/dnsglossary)
*   [Archived mailing list discussion on BIND's future](https://lists.archlinux.org/pipermail/arch-dev-public/2013-March/024588.html)