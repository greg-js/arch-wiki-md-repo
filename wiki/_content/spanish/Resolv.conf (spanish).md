El archivo de configuración para los resolvers de DNS es `/etc/resolv.conf`. Desde su [man page](http://www.kernel.org/doc/man-pages/online/pages/man5/resolv.conf.5.html):

	*«El resolver es un conjunto de rutinas de la biblioteca C, que proporciona acceso al Sistema de Nombres de Dominio de Internet (DNS). El archivo de configuración del resolver contiene información que es leída por las subrutinas cada vez que un proceso le reclama. El archivo está diseñado para ser fácilmente comprensible y contiene una lista de palabras claves con valores que proporcionan diferentes tipos de información del resolver.»*

	*«En un sistema correctamente configurado este archivo puede no ser necesario. El único servidor de nombres a consultar será la máquina local; el nombre de dominio se determina a partir del nombre del host y la ruta de búsqueda de dominio se construye a partir del nombre de dominio.»*

## Contents

*   [1 DNS en Linux](#DNS_en_Linux)
*   [2 Servidores DNS alternativos](#Servidores_DNS_alternativos)
    *   [2.1 OpenNIC](#OpenNIC)
    *   [2.2 OpenDNS](#OpenDNS)
    *   [2.3 Google](#Google)
    *   [2.4 Comodo](#Comodo)
    *   [2.5 Yandex](#Yandex)
*   [3 Conservar las configuraciones de DNS](#Conservar_las_configuraciones_de_DNS)
    *   [3.1 Utilizar openresolv](#Utilizar_openresolv)
    *   [3.2 Modificar la configuración dhcpcd](#Modificar_la_configuraci.C3.B3n_dhcpcd)
    *   [3.3 Protección contra escritura de /etc/resolv.conf](#Protecci.C3.B3n_contra_escritura_de_.2Fetc.2Fresolv.conf)
    *   [3.4 Utilizar la opción timeout para reducir el tiempo de búsqueda del nombre del equipo](#Utilizar_la_opci.C3.B3n_timeout_para_reducir_el_tiempo_de_b.C3.BAsqueda_del_nombre_del_equipo)

## DNS en Linux

Su proveedor de internet (por lo general) le ofrecerá servidores [DNS](https://en.wikipedia.org/wiki/es:Domain_Name_System "wikipedia:es:Domain Name System") funcionales, y un router, que también puede agregar un servidor DNS adicional, en caso de que tenga su propio servidor caché. El cambio entre los servidores DNS no representa un problema para los usuarios de Windows, ya que si un servidor DNS es lento o no funciona, pasará de inmediato a otro mejor. Sin embargo, Linux, por lo general, toma más tiempo para realizar este proceso, lo que podría ser la razón por la que puede estar apreciando cierto retraso.

Utilice *dig* (proporcionado por el paquete [dnsutils](https://www.archlinux.org/packages/?name=dnsutils)) antes de realizar cualquier cambio, repítalo después de hacer los ajustes en la sección de abajo, y compare el tiempo(s) de consulta:

```
$ dig www5.yahoo.com

```

También puede especificar un servidor de nombres:

```
$ dig @ip.of.name.server www5.yahoo.com

```

## Servidores DNS alternativos

Para utilizar servidores DNS alternativos, edite `/etc/resolv.conf` y añádalos a la parte superior del archivo para que se utilicen los primeros, y, opcionalmente, elimine o comente los servidores consecutivos.

**Nota:** Los cambios realizados en `/etc/resolv.conf` surten efecto inmediatamente.

### OpenNIC

[OpenNIC](http://www.opennicproject.org/) proporciona servidores de nombres sin censura, gratis y con características adicionales.

**Sugerencia:** OpenNIC ofrece muchos [servidores de nombres diferentes](http://wiki.opennicproject.org/Tier2) situados en múltiples países. Escoja algunos de los [servidores de nombres más cercanos](http://www.opennicproject.org/nearest-servers/) para optimizar el rendimiento.

```
# OpenNIC IPv4 nameservers (US)
nameserver 107.170.95.180
nameserver 75.127.14.107

```

```
# OpenNIC IPv4 nameservers (ES)
nameserver 109.69.8.34    #(BCN, ES)
nameserver 185.16.40.143  #(MD, ES)
nameserver 87.216.170.85  #(MD, ES) 

```

### OpenDNS

[OpenDNS](https://opendns.com) proporciona servidores de nombres alternativos gratuitos:

```
# OpenDNS IPv4 nameservers
nameserver 208.67.222.222
nameserver 208.67.220.220

```

```
# OpenDNS IPv6 nameservers
nameserver 2620:0:ccc::2
nameserver 2620:0:ccd::2

```

### Google

Los [nombres de servidores de Google](https://developers.google.com/speed/public-dns/) pueden ser utilizados como una alternativa:

```
# Google IPv4 nameservers
nameserver 8.8.8.8
nameserver 8.8.4.4

```

```
# Google IPv6 nameservers
nameserver 2001:4860:4860::8888
nameserver 2001:4860:4860::8844

```

### Comodo

[Comodo](http://securedns.dnsbycomodo.com/) proporciona otro conjunto de IPv4, con una opción de filtrado web (no gratis). Implícito en esta característica es que el servicio secuestra las consultas.

```
# Comodo nameservers 
nameserver 8.26.56.26 
nameserver 8.20.247.20

```

### Yandex

[Yandex.DNS](http://dns.yandex.ru/) tiene 3 modelos:

```
# Basic Yandex.DNS - DNS rápidos y fiables
nameserver 77.88.8.8
nameserver 77.88.8.1

```

```
# Safe Yandex.DNS - Protección contra virus y contenido fraudulento
nameserver 77.88.8.88
nameserver 77.88.8.2

```

```
# Family Yandex.DNS - Sin contenido para adultos
nameserver 77.88.8.7
nameserver 77.88.8.3

```

## Conservar las configuraciones de DNS

[dhcpcd](/index.php/Dhcpcd "Dhcpcd"), [netctl](/index.php/Netctl_(Espa%C3%B1ol) "Netctl (Español)"), [NetworkManager](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)") y otros muchos procesos, pueden sobrescribir `/etc/resolv.conf`. Esto suele ser un comportamiento deseable, pero a veces la configuración de DNS exige ajustarla manualmente (por ejemplo, cuando se utiliza una dirección IP estática). Hay varias maneras de hacer esto.

*   Si se está usando dhcpcd, vea [#Modificar la configuración dhcpcd](#Modificar_la_configuraci.C3.B3n_dhcpcd) a continuación.
*   Si se está usando [netctl](/index.php/Netctl_(Espa%C3%B1ol) "Netctl (Español)"), con asignación de dirección IP estática, no utilize las opciones `DNS*` en su perfil, de lo contrario *resolvconf* será llamado y sobrescribirá `/etc/resolv.conf`.

### Utilizar openresolv

[openresolv](https://www.archlinux.org/packages/?name=openresolv) proporciona una utilidad *resolvconf* , que es una infraestructura para la gestión de múltiples configuraciones DNS. Vea `man 8 resolvconf` y `man 5 resolvconf.conf` para obtener más información.

La configuración se realiza en `/etc/resolvconf.conf`, que al ejecutar `resolvconf -u` generará `/etc/resolv.conf`.

### Modificar la configuración dhcpcd

El archivo de configuración de dhcpcd puede ser editado para evitar que el demonio dhcpcd sobrescriba `/etc/resolv.conf`. Para ello, agregue lo siguiente a la última sección de `/etc/dhcpcd.conf`:

```
nohook resolv.conf

```

Como alternativa, puede crear un archivo llamado `/etc/resolv.conf.head` que contenga los servidores DNS. dhcpcd antepondrá este archivo a `/etc/resolv.conf`.

### Protección contra escritura de /etc/resolv.conf

Otra manera de proteger su `/etc/resolv.conf` de ser modificado por cualquier proceso es establecer el atributo (protección contra escritura) inmutable:

```
# chattr +i /etc/resolv.conf

```

### Utilizar la opción timeout para reducir el tiempo de búsqueda del nombre del equipo

Si se enfrenta a una búsqueda de nombre de host muy largo (como puede ser en [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") o durante la navegación), a menudo puede ayudar definir un tiempo de espera pequeño después del cual se utilizará un servidor de nombres alternativos. Para ello, escriba lo siguiente en `/etc/resolv.conf`.

```
options timeout:1

```