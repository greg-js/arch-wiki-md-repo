**Estado de la traducción**
Este artículo es una traducción de [Nftables](/index.php/Nftables "Nftables"), revisada por última vez el **2018-09-03**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Nftables&diff=0&oldid=528452) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [iptables (Español)](/index.php/Iptables_(Espa%C3%B1ol) "Iptables (Español)")

[nftables](http://netfilter.org/projects/nftables/) es un proyecto de netfilter que tiene como objetivo reemplazar el marco existente de tablas{ip,ip6,arp,eb}. Proporciona un nuevo marco de filtrado de paquetes, una nueva utilidad en el espacio de usuario (nft) y una capa de compatibilidad para las tablas{ip,ip6}. Utiliza los hooks existentes, el sistema de seguimiento de la conexiones, los componentes de la línea de espera de los paquetes de red («*packet queues*») del espacio de usuario y el subsistema de registro de netfilter.

Consta de tres componentes principales: una implementación del kernel, la comunicación de la biblioteca libnl con netlink y un frontend de nftables en el espacio de usuario («*nft*») . El kernel proporciona una interfaz para la configuración del enlace de red («*netlink*»), así como una evaluación del conjunto de reglas en tiempo de ejecución; libnl contiene las funciones de bajo nivel para comunicarse con el kernel, y, por último, el frontend nft proporciona interacción al usuario con nftables.

Para obtener más información también puede visitar la [página oficial de la wiki de nftables](https://wiki.nftables.org/wiki-nftables/index.php/Main_Page) .

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Utilización](#Utilización)
*   [3 Configuración](#Configuración)
    *   [3.1 Tablas](#Tablas)
        *   [3.1.1 Crear una tabla](#Crear_una_tabla)
        *   [3.1.2 Listar las tablas](#Listar_las_tablas)
        *   [3.1.3 Listar las cadenas y las reglas de una tabla](#Listar_las_cadenas_y_las_reglas_de_una_tabla)
        *   [3.1.4 Borrar una tabla](#Borrar_una_tabla)
        *   [3.1.5 Vaciar una tabla](#Vaciar_una_tabla)
    *   [3.2 Cadenas](#Cadenas)
        *   [3.2.1 Crear una cadena](#Crear_una_cadena)
            *   [3.2.1.1 Cadena normal](#Cadena_normal)
            *   [3.2.1.2 Cadena base](#Cadena_base)
        *   [3.2.2 Listar las reglas](#Listar_las_reglas)
        *   [3.2.3 Modificar una cadena](#Modificar_una_cadena)
        *   [3.2.4 Borrar una cadena](#Borrar_una_cadena)
        *   [3.2.5 Eliminar las reglas de una cadena](#Eliminar_las_reglas_de_una_cadena)
    *   [3.3 Reglas](#Reglas)
        *   [3.3.1 Añadir una regla](#Añadir_una_regla)
            *   [3.3.1.1 Expresiones](#Expresiones)
        *   [3.3.2 Eliminación](#Eliminación)
    *   [3.4 Recargar todo](#Recargar_todo)
*   [4 Ejemplos](#Ejemplos)
    *   [4.1 Estación de trabajo](#Estación_de_trabajo)
    *   [4.2 Cortafuegos simple con IPv4/IPv6](#Cortafuegos_simple_con_IPv4/IPv6)
    *   [4.3 Tipo de límite del cortafuegos IPv4/IPv6](#Tipo_de_límite_del_cortafuegos_IPv4/IPv6)
    *   [4.4 Jump](#Jump)
    *   [4.5 Diferentes reglas para diferentes interfaces](#Diferentes_reglas_para_diferentes_interfaces)
    *   [4.6 Enmascaramiento](#Enmascaramiento)
*   [5 Consejos y trucos](#Consejos_y_trucos)
    *   [5.1 Cortafuegos stateful simple](#Cortafuegos_stateful_simple)
        *   [5.1.1 Proteger un único equipo](#Proteger_un_único_equipo)
    *   [5.2 Evitar ataques de fuerza bruta](#Evitar_ataques_de_fuerza_bruta)
*   [6 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install "Install") las utilidades para el espacio de usuario proporcionadas por el paquete [nftables](https://www.archlinux.org/packages/?name=nftables) o su versión git [nftables-git](https://aur.archlinux.org/packages/nftables-git/).

## Utilización

*nftables* hace una distinción entre las reglas temporales realizadas en la línea de órdenes y aquellas otras permanentes cargadas o guardadas en un archivo. El archivo predeterminado es `/etc/nftables.conf`, que ya contiene una tabla simple de cortafuegos para ipv4/ipv6 llamada «inet filter».

Para utilizarlo, [inicie/active](/index.php/Start/enable "Start/enable") el servicio `nftables.service`.

Puede consultar el conjunto de reglas con:

```
# nft list ruleset

```

**Nota:** Puede que tenga que crear el archivo `/etc/modules-load.d/nftables.conf` introduciendo por líneas los nombres de todos los módulos relacionados con nftables, para que el servicio de systemd funcione correctamente. Puede obtener una lista de los módulos utilizando esta orden: `$ lsmod | grep '^nf'` De lo contrario, podría obtener el error: `Error: Could not process rule: No such file or directory`.

## Configuración

La utilidad de nftable en el espacio de usuario, *nft*, realiza la mayor parte de la evaluación del conjunto de reglas antes de pasarlas al kernel. Las reglas se almacenan en cadenas, que a su vez se almacenan en tablas. Las siguientes secciones indican cómo crear y modificar estos elementos.

Todos los cambios explicados a continuación son temporales. Para que los cambios permanezcan, guarde el conjunto de reglas en el archivo `/etc/nftables.conf`, que será cargado por el servicio `nftables.service`:

```
# nft list ruleset > /etc/nftables.conf

```

**Nota:** `nft list` no muestra las definiciones de variables; si tiene alguna en `/etc/nftables.conf` se perderán. Cualquier variable utilizada en las reglas será reemplazada por el valor de esa variable.

Para leer la entrada de un archivo, use el indicador `-f`:

```
# nft -f *nombre_del_archivo*

```

Tenga en cuenta que las reglas ya cargadas no se ejecutan automáticamente.

Consulte [nft(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nft.8) para obtener una lista completa de todas las órdenes.

### Tablas

Las tablas alojan [#Cadenas](#Cadenas). A diferencia de las tablas en iptables, no hay tablas integradas en nftables. La cantidad de tablas y sus nombres depende del usuario. Sin embargo, cada tabla solo tiene una familia de direcciones y solo se aplica a los paquetes de red de esa familia. Las tablas pueden tener una de las cinco familias que se especifican:

| Familia de nftables | Utilidad iptables |
| ip | iptables |
| ip6 | ip6tables |
| inet | iptables and ip6tables |
| arp | arptables |
| bridge | ebtables |

`ip` (es decir, IPv4) es la familia predeterminada y se usará si no se especifica la familia.

Para crear una regla que se aplique tanto a IPv4 como a IPv6, utilice `inet`. `inet` permite la unificación de las familias `ip` y `ip6` para que las reglas que las defines sean más sencillas para ambas.

**Nota:** `inet` no funciona para las cadenas `nat`, solo para las cadenas `filter`. ([fuente](http://www.spinics.net/lists/netfilter/msg56411.html))

Consulte la sección `ADDRESS FAMILIES` en [nft(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nft.8) para obtener una descripción completa de las familias de direcciones.

En todos los casos, `<*familia*>` es opcional y, si no se especifica, se decanta por `ip`.

#### Crear una tabla

La siguiente orden añade una nueva tabla:

```
# nft add table <*familia*> <*tabla*>

```

#### Listar las tablas

Para enumerar todas las tablas:

```
# nft list tables

```

#### Listar las cadenas y las reglas de una tabla

Para enumerar todas las cadenas y reglas de una tabla especificada, escriba lo siguiente:

```
# nft list table <*familia*> <*tabla*>

```

Por ejemplo, para enumerar todas las reglas de la tabla `filter` de la familia `inet`:

```
# nft list table inet filter

```

#### Borrar una tabla

Para eliminar una tabla, escriba lo siguiente:

```
# nft delete table <*familia*> <*tabla*>

```

Las tablas solo se pueden eliminar si no contienen cadenas.

#### Vaciar una tabla

Para eliminar todas las reglas de una tabla, escriba lo siguiente:

```
# nft flush table <*familia*> <*tabla*>

```

### Cadenas

El propósito de las cadenas es alojar [#Reglas](#Reglas). A diferencia de las cadenas en iptables, no hay cadenas integradas en nftables. Esto significa que si ninguna cadena utiliza ningún tipo o hook en el marco de netfilter, los paquetes de red que fluyan a través de esas cadenas no serán tocados por nftables, a diferencia de iptables.

Las cadenas son de dos tipos. Una cadena base que es un punto de entrada para los paquetes de la pila de red, donde se especifica un valor de enlace. Y una cadena normal que puede usarse como un objetivo de salto («**jump**») para una mejor organización.

En todo lo que sigue, la familia es opcional y, si no se especifica, esta se define como ip.

#### Crear una cadena

##### Cadena normal

A continuación, agregaremos una cadena normal, llamada `<*cadena*>`, a la tabla denominada `<*tabla*>`:

```
# nft add chain <*familia*> <*tabla*> <*cadena*>

```

Por ejemplo, para añadir una cadena normal llamada `tcpchain`, a la tabla `filter`, de la familia de direcciones `inet`, escribiremos lo siguiente:

```
# nft add chain inet filter tcpchain

```

##### Cadena base

Para añadir una cadena base, especificaremos los valores de hook y de priority:

```
# nft add chain <*familia*> <*tabla*> <*cadena*> { type *tipo* hook *hook* priority *prioridad* \; }

```

`*type*` puede ser `filter`, `route`, o `nat`.

Para familias de direcciones IPv4/IPv6/Inet el `*hook*` puede ser `prerouting`, `input`, `forward`, `output`, o `postrouting`. Consulte [nft(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nft.8)para obtener una lista de los hooks para otras familias.

`*priority*` toma un valor entero. Las cadenas con números más bajos se procesan primero y pueden ser negativos. [[1]](https://wiki.nftables.org/wiki-nftables/index.php/Configuring_chains#Base_chain_types)

Por ejemplo, para añadir una cadena base que filtre los paquetes de entrada:

```
# nft add chain inet filter input { type filter hook input priority 0\; }

```

Reemplace `add` con `create` en cualquiera de las órdenes anteriores para añadir una nueva cadena, pero tenga en cuenta que devolvera un error si la cadena ya existe.

#### Listar las reglas

A continuación enumeraremos todas las reglas de una cadena:

```
# nft list chain <*familia*> <*tabla*> <*cadena*>

```

Por ejemplo, la siguiente orden listará las reglas de la cadena llamada `output`, presentes en la tabla `inet` llamada `filter`:

```
# nft list chain inet filter output

```

#### Modificar una cadena

Para modificar una cadena, bastará con llamarla por su nombre y definiremos las reglas que deseamos cambiar.

```
# nft chain <tabla> <familia> <cadena> { [ type <tipo> hook <hook> device <dispositivo> priority <prioridad> \; policy <política> \; ] }

```

Si, por ejemplo, solo deseamos cambiar la política de la cadena de entrada («*input*») de la tabla predeterminada, de «accept» a «drop», escribiremos:

```
# nft chain inet filter input { policy drop \; }

```

#### Borrar una cadena

Para eliminar una cadena escribiremos:

```
# nft delete chain <*familia*> <*tabla*> <*cadena*>

```

La cadena no debe contener ninguna regla, ni tener un objetivo «jump».

#### Eliminar las reglas de una cadena

Para eliminar las reglas de una cadena, haremos lo siguiente:

```
# nft flush chain <*familia*> <*tabla*> <*cadena*>

```

### Reglas

Las reglas se construyen, bien a partir de expresiones («*expressions*») o bien a partir de declaraciones («*statements*»), y están contenidas dentro de cadenas.

#### Añadir una regla

**Sugerencia:** La utilidad *iptables-translate* traduce las reglas [iptables](/index.php/Iptables_(Espa%C3%B1ol) "Iptables (Español)") al formato nftables.

Para añadir una regla a una cadena, escribiremos:

```
# nft add rule <*familia*> <*tabla*> <*cadena*> handle <*identificador*> <*statement*>

```

La regla se agrega con `*handle*`, que es opcional. Si no se especifica, la regla se agrega al final de la cadena.

Para anteponer la regla de posición, escriba:

```
# nft insert rule <*familia*> <*tabla*> <*cadena*> handle <*identificador*> <*statement*>

```

Si el <*identificador*> (`*handle*`) no se especifica, la regla se antepone a la cadena.

##### Expresiones

Por lo general, un `*statement*` incluye alguna expresión de coincidencia (como «*condición*») y, luego, una «*declaración*» que resuelva (si coinciden). Las declaraciones resolutivas incluyen `accept`, `drop`, `queue`, `continue`, `return`, `<*cadena*> jump`, y `<*cadena*> goto`. Son posibles otros «*statement*» que contengan otras declaraciones resolutivas. Consulte [nft(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nft.8) para obtener más información.

Hay varias expresiones disponibles en nftables y, en su mayor parte, coinciden con sus contrapartes de iptables. La diferencia más notable es que no hay coincidencias genéricas o implícitas. Una coincidencia genérica siempre estuvo disponible, como era el caso de `--protocol` o `--source`. Las coincidencias implícitas eran específicas del protocolo, tales como `--sport` cuando se verificaba que un paquete era TCP.

He aquí es una lista no exhaustiva de las coincidencias disponibles:

*   meta (meta propiedades, por ejemplo, interfaces)
*   icmp (protocolo ICMP)
*   icmpv6 (protocolo ICMPv6)
*   ip (protocolo IP)
*   ip6 (protocolo IPv6)
*   tcp (protocolo TCP)
*   udp (protocolo UDP)
*   sctp (protocolo SCTP)
*   ct (seguimiento de la conexión)

He aquí una lista no exhaustiva de los argumentos de coincidencia (para una lista más completa, vea [nft(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nft.8)):

```
meta:
  oif <INDICE de la interfaz de salida>
  iif <INDICE de la interfaz de entrada>
  oifname <NOMBRE de la interfaz de salida>
  iifname <NOMBRE de la interfaz de entrada>

  (oif y iif aceptan argumentos de cadena y se convierten en índices de interfaz)
  (oifname y iifname son más dinámicos, pero más lentos debido a la coincidencia de cadenas)

icmp:
  type <tipo icmp>

icmpv6:
  type <tipo icmpv6>

ip:
  protocol <protocolo>
  daddr <dirección de destino>
  saddr <dirección de origen>

ip6:
  daddr <dirección de destino>
  saddr <dirección de origen>

tcp:
  dport <puerto de destino>
  sport <puerto de origen>

udp:
  dport <puerto de destino>
  sport <puerto de origen>

sctp:
  dport <puerto de destino>
  sport <puerto de origen>

ct:
  state <new | established | related | invalid>

```

**Nota:** *nft* no utiliza `/etc/services` para hacer coincidir los números de los puertos con los nombres, en su lugar utiliza una [lista interna](https://git.netfilter.org/nftables/plain/src/services.c). Para mostrar las asignaciones de puertos desde la línea de órdenes, utilice, por ejemplo `nft describe tcp dport`.

#### Eliminación

Las reglas individuales solo se pueden eliminar mediante sus identificadores («*handle*»). La orden `nft --handle list` se puede usar para determinar los identificadores de las reglas. Advierta que el modificador `--handle` le dice a `nft` que liste los identificadores en la salida.

Las siguientes órdenes determinan, primero, el identificador de una regla y, luego, borra dicha regla. El argumento `--number` es útil para que vuelque algún resultado numérico, como las direcciones IP no resueltas.

 `# nft --handle --numeric list chain filter input` 
```
table ip fltrTable {
     chain input {
          type filter hook input priority 0;
          ip saddr 127.0.0.1 accept # handle 10
     }
}

```

```
# nft delete rule fltrTable input handle 10

```

Todas las cadenas en una tabla se pueden limpiar con la orden `nft flush table`. Las cadenas individuales pueden eliminarse utilizando las órdenes `nft flush chain` o `nft delete rule`.

```
# nft flush table foo
# nft flush chain foo bar
# nft delete rule ip6 foo bar

```

La primera orden, limpia todas las cadenas en la tabla ip `foo`. La segunda, limpia la cadena `bar` en la tabla ip `foo`. La tercera, borra todas las reglas en la cadena `bar` en la tabla ip6 `foo`.

### Recargar todo

Vacíe el conjunto de reglas actuales:

```
# echo "flush ruleset" > /tmp/nftables 

```

Vuelque el conjunto de reglas actuales:

```
# nft list ruleset >> /tmp/nftables

```

Ahora puede editar /tmp/nftables y aplicar los cambios con:

```
# nft -f /tmp/nftables

```

## Ejemplos

### Estación de trabajo

 `/etc/nftables.conf` 
```
flush ruleset

table inet filter {
        chain input {
                type filter hook input priority 0;

                # aceptar cualquier tráfico de localhost
                iif lo accept

                # aceptar tráfico originado por nosotros
                ct state established,related accept

		# aceptar ICMP y IGMP
		ip6 nexthdr icmpv6 icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter-problem, mld-listener-query, mld-listener-report, mld-listener-reduction, nd-router-solicit, nd-router-advert, nd-neighbor-solicit, nd-neighbor-advert, ind-neighbor-solicit, ind-neighbor-advert, mld2-listener-report } accept
		ip protocol icmp icmp type { destination-unreachable, router-solicitation, router-advertisement, time-exceeded, parameter-problem } accept
		ip protocol igmp accept

                # descomentar la siguiente línea para aceptar servicios locales comunes
                #tcp dport { 22, 80, 443 } ct state new accept

                # cuenta y descarta cualquier otro tráfico
                counter drop
        }
}

```

### Cortafuegos simple con IPv4/IPv6

 `cortafuegos.rules` 
```
# A simple cortafuegos

flush ruleset

table inet filter {
	chain input {
		type filter hook input priority 0; policy drop;

		# conexiones establecidas/relacionadas
		ct state established,related accept

		# conexiones no válidas
		ct state invalid drop

		# interfaz loopback
		iif lo accept

		# ICMP y IGMP
		ip6 nexthdr icmpv6 icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter-problem, mld-listener-query, mld-listener-report, mld-listener-reduction, nd-router-solicit, nd-router-advert, nd-neighbor-solicit, nd-neighbor-advert, ind-neighbor-solicit, ind-neighbor-advert, mld2-listener-report } accept
		ip protocol icmp icmp type { destination-unreachable, router-solicitation, router-advertisement, time-exceeded, parameter-problem } accept
		ip protocol igmp accept

		# SSH (puerto 22)
		tcp dport ssh accept

		# HTTP (puertos 80 y 443)
		tcp dport { http, https } accept
	}

	chain forward {
		type filter hook forward priority 0; policy drop;
	}

	chain output {
		type filter hook output priority 0; policy accept;
	}

}

```

### Tipo de límite del cortafuegos IPv4/IPv6

 `cortafuegos.2.rules` 
```
table inet filter {
	chain input {
		type filter hook input priority 0; policy drop;

		ct state invalid drop

		iif lo accept

		# sin saturación de ping:
		ip protocol icmp icmp type echo-request limit rate over 10/second burst 4 packets  drop
		ip6 nexthdr icmpv6 icmpv6 type echo-request limit rate over 10/second burst 4 packets drop

		ct state established,related accept

		# ICMP y IGMP
		ip6 nexthdr icmpv6 icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter-problem, mld-listener-query, mld-listener-report, mld-listener-reduction, nd-router-solicit, nd-router-advert, nd-neighbor-solicit, nd-neighbor-advert, ind-neighbor-solicit, ind-neighbor-advert, mld2-listener-report } accept
		ip protocol icmp icmp type { destination-unreachable, router-solicitation, router-advertisement, time-exceeded, parameter-problem } accept
		ip protocol igmp accept

		# evitar la fuerza bruta en ssh:
		tcp dport ssh ct state new limit rate 15/minute accept

	}

	chain forward {
		type filter hook forward priority 0; policy drop;
	}

	chain output {
		type filter hook output priority 0; policy accept;
	}

}

```

### Jump

Al usar saltos (jump) en el archivo de configuración, primero es necesario definir la cadena *target*. De lo contrario, nos podríamos encontrar con el error `Error: Could not process rule: No such file or directory`.

 `jump.rules` 
```
table inet filter {
    chain web {
        tcp dport http accept
        tcp dport 8080 accept
    }
    chain input {
        type filter hook input priority 0;
        ip saddr 10.0.2.0/24 jump web
        drop
    }
}

```

### Diferentes reglas para diferentes interfaces

Si su equipo tiene más de una interfaz de red y le gustaría usar diferentes reglas para las diferentes interfaces, puede usar una cadena de filtros «*dispatching*», y luego cadenas de filtros específicas para cada interfaz. Por ejemplo, supongamos que tiene un equipo que actúa como un enrutador doméstico, y desea ejecutar un servidor web accesible a través de la LAN (interfaz nsp3s0), pero no desde Internet público (interfaz enp2s0), es posible que desee considerar una estructura como esta:

```
table inet filter {
  chain input { # esta cadena sirve como despachador
    type filter hook input priority 0;

    iif lo accept # always accept loopback
    iifname enp2s0 jump input_enp2s0
    iifname enp3s0 jump input_enp3s0

    reject with icmp type port-unreachable # refuse traffic from all other interfaces
  }
  chain input_enp2s0 { # reglas aplicables a la interfaz de acceso pública
    ct state {established,related} accept
    ct state invalid drop
    udp dport bootpc accept
    tcp dport bootpc accept
    reject with icmp type port-unreachable # todo el tráfico restante
  }
  chain input_enp3s0 {
    ct state {established,related} accept
    ct state invalid drop
    udp dport bootpc accept
    tcp dport bootpc accept
    tcp port http accept
    tcp port https accept
    reject with icmp type port-unreachable # todo el tráfico restante
  }
  chain ouput { # dejamos que todo salga
    type filter hook output priority 0;
    accept
  }
 }

```

De forma alternativa, podría elegir solo una declaración `iifname`, a modo de interfaz única ascendente, y colocar las reglas predeterminadas para todas las demás interfaces en un solo lugar, en vez de enviarlas para cada interfaz.

### Enmascaramiento

nftables tiene una palabra clave especial `masquerade` «donde la dirección de origen se configura automáticamente hacia la dirección de la interfaz de salida» ([source](http://wiki.nftables.org/wiki-nftables/index.php/Performing_Network_Address_Translation_%28NAT%29#Masquerading)). Esto es particularmente útil para situaciones en las que la dirección IP de la interfaz es impredecible o inestable, como la interfaz de los enrutadores que se conectan a muchos ISP. Sin esta opción, las reglas de traducción de las direcciones de red tendrían que actualizarse cada vez que cambiara la dirección IP de la interfaz.

Para usarlo:

*   asegúrese de que el enmascaramiento esté activado en el kernel (*true* (verdadero) si se utiliza el kernel predeterminado); de lo contrario, durante la configuración del kernel, defínalo:

```
CONFIG_NFT_MASQ=m

```

*   la palabra clave `masquerade` solo se puede usar en cadenas de tipo `nat`, las cuales no se pueden combinar en una tabla con la familia `inet`. Utilice una tabla con la familia `ip` y/o `ip6` en su lugar.

*   el enmascaramiento es un tipo de fuente NAT, por lo que solo funciona en la ruta de salida.

Ejemplo para un equipo con dos interfaces: LAN conectada a `nsp3s0`, e Internet pública conectada a `enp2s0`:

```
table ip nat {
  chain prerouting {
    type nat hook prerouting priority 0;
  }
  chain postrouting {
    type nat hook postrouting priority 0;
    oifname "enp0s2" masquerade
  }
}

```

## Consejos y trucos

### Cortafuegos stateful simple

Consulte [Simple stateful firewall (Español)](/index.php/Simple_stateful_firewall_(Espa%C3%B1ol) "Simple stateful firewall (Español)") para obtener más información.

#### Proteger un único equipo

Vacíe el conjunto de reglas actuales:

```
# nft flush ruleset

```

Añada una tabla:

```
# nft add table inet filter

```

Añada las cadenas base: input, forward y output. La política de *input* y *forward* será *drop*. La política de *output* será *accept*.

```
# nft add chain inet filter input { type filter hook input priority 0 \; policy drop \; }
# nft add chain inet filter forward { type filter hook forward priority 0 \; policy drop \; }
# nft add chain inet filter output { type filter hook output priority 0 \; policy accept \; }

```

Añada dos cadenas normales que se asociarán con tcp y udp:

```
# nft add chain inet filter TCP
# nft add chain inet filter UDP

```

El tráfico relacionado («*related*») y el ya establecido («*established*») será aceptado («*accept*»):

```
# nft add rule inet filter input ct state related,established accept

```

Se aceptará todo el tráfico procedente de la interfaz loopback:

```
# nft add rule inet filter input iif lo accept

```

Se establecerá la política de descartar («*drop*») para cualquier tráfico no válido:

```
# nft add rule inet filter input ct state invalid drop

```

Se aceptarán nuevas solicitudes de echo (pings):

```
# nft add rule inet filter input ip protocol icmp icmp type echo-request ct state new accept

```

El nuevo tráfico upd saltará («*jump*») a la cadena UDP:

```
# nft add rule inet filter input ip protocol udp ct state new jump UDP

```

El nuevo tráfico tcp saltará («*jump*») a la cadena TCP:

```
# nft add rule inet filter input ip protocol tcp tcp flags \& \(fin\|syn\|rst\|ack\) == syn ct state new jump TCP

```

Se rechazará («*reject*») todo el tráfico no procesado por la restantes reglas:

```
# nft add rule inet filter input ip protocol udp reject
# nft add rule inet filter input ip protocol tcp reject with tcp reset
# nft add rule inet filter input counter reject with icmp type prot-unreachable

```

En este punto, debe decidir qué puertos desea abrir para las conexiones entrantes, que son manejadas por las cadenas TCP y UDP. Por ejemplo, para abrir conexiones para un servidor web, añada:

```
# nft add rule inet filter TCP tcp dport 80 accept

```

Para aceptar conexiones HTTPS de un servidor web en el puerto 443:

```
# nft add rule inet filter TCP tcp dport 443 accept

```

Para aceptar el tráfico SSH en el puerto 22:

```
# nft add rule inet filter TCP tcp dport 22 accept

```

Para aceptar solicitudes de DNS entrantes:

```
# nft add rule inet filter TCP tcp dport 53 accept
# nft add rule inet filter UDP udp dport 53 accept

```

Asegúrese de hacer que sus cambios permanezcan cuando esté satisfecho.

### Evitar ataques de fuerza bruta

[Sshguard](/index.php/Sshguard "Sshguard") es un programa que puede detectar ataques de fuerza bruta y modificar el cortafuegos en función de las direcciones IP temporalmente bloqueadas. Consulte [Sshguard#nftables](/index.php/Sshguard#nftables "Sshguard") sobre cómo configurar nftables para usarlo con Sshguard.

## Véase también

*   [netfilter nftables wiki](https://wiki.nftables.org/)
*   [debian:nftables](https://wiki.debian.org/nftables "debian:nftables")
*   [gentoo:nftables](https://wiki.gentoo.org/wiki/nftables "gentoo:nftables")
*   [First release of nftables](https://lwn.net/Articles/324251/)
*   [nftables quick howto](https://home.regit.org/netfilter-en/nftables-quick-howto/)
*   [The return of nftables](https://lwn.net/Articles/564095/)
*   [What comes after ‘iptables’? Its successor, of course: `nftables`](http://developers.redhat.com/blog/2016/10/28/what-comes-after-iptables-its-successor-of-course-nftables/)