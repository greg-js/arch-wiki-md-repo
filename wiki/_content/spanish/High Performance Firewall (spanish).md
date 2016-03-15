Imaginemos esta situación: tenemos más de dos redes separadas por un protocolo Lan Virtual (IEEE 802.1q) o VLAN, las cuales nos llegan a través de un conmutador inteligente/manejable en una línea troncal 10/100/1000 MB HD/FD (naturalmente lo mejor sería 1000 MB FD).

Esta página nos introduce la forma de crear un Firewall/Nat de alto rendimiento con iptables, VLAN e iproute2\. Entonces se podrá compartir Internet con un gran número de equipos y seguir manteniendo un buen rendimiento.

## Contents

*   [1 Soporte de VLAN](#Soporte_de_VLAN)
    *   [1.1 El NAT round robin](#El_NAT_round_robin)
    *   [1.2 Sugerencias](#Sugerencias)
*   [2 Alto Rendimiento](#Alto_Rendimiento)
*   [3 Iproute2](#Iproute2)

## Soporte de VLAN

En primer lugar, crearemos una subred, como se indica en la página [VLAN](/index.php/VLAN "VLAN").

### El NAT round robin

Supongamos que tenemos una IP 200.AAA.BBB.6 y nuestro gateway es 200.AAA.BBB.1\. Sin ningun problema podemos poner estos parámetros por defecto en nuestra configuracion. No va a afectar para nada a nuestro firewall.

Partimos del supuesto de que tenemos 3 grupos de 10 IP publicas cada uno... Con esto, vamos a definir lo siguiente en el comienzo de nuestro script de firewall:

```
Gr1='200.AAA.CCC.10-200.AAA.CCC.20'
Gr2='200.AAA.DDD.10-200.AAA.DDD.20'
Gr3='200.AAA.EEE.10-200.AAA.EEE.20'

```

**Y las siguientes líneas importantes son:**

```
iptables -t nat -A POSTROUTING -s 192.168.0.0/21  -j SNAT --to $Gr1 #ACCESS VLAN 10
iptables -t nat -A POSTROUTING -s 192.168.8.0/21  -j SNAT --to $Gr2 #ACCESS VLAN 20
iptables -t nat -A POSTROUTING -s 192.168.15.0/21  -j SNAT --to $Gr1 #ACCESS VLAN 30
.... etc

```

Podemos repetir los grupos de acceso, subdividir las redes, etc. Iptables hace de forma automática *round robin* sobre Gr1, Gr2 y Gr3 por defecto, sin que sea necesaria modificación ulterior.

No es necesario crear tarjetas virtuales (alias) para cada IP en cada grupo.

Es importante que cada router real (router BGP) conozca a cada grupo y lo difunda a través de BGP (o similar) a los router «vecinos».

### Sugerencias

Para acelerar algunos puertos podemos poner lo siguiente en la cabeza de nuestra cadena `FORWARD`:

```
iptables -A FORWARD -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A FORWARD -p icmp -o eth0 -j ACCEPT
iptables -A FORWARD -p tcp -m multiport --dports 80,443,110,53 -j ACCEPT  # FAST FAST FAST 
iptables -A FORWARD -p udp  --dport 53 -j ACCEPT

```

Esto significa:

*   Los paquetes de tráfico solo pasaran 1 regla si estos son de una conexion establecida.
*   Los paquetes de tráfico solo pasaran 2 reglas si son un PING o similar.
*   Los paquetes solo pasaran 3 reglas si son http, correo o similar.
*   Y por ultimo los paquetes de DNS van a pasar 3 o 4 reglas máximo antes de salir.

Los virus de los clientes pueden matar el trafico de nuestro firewall, y no vamos a necesitar compartir conversaciones con windows, asi que las bloqueamos...

```
 #VIRUS
iptables -A FORWARD -p tcp --dport 135:139 -j DROP
iptables -A FORWARD -p tcp --dport 445 -j DROP
iptables -A FORWARD -p udp --dport 135:139 -j DROP
iptables -A FORWARD -p udp --dport 445 -j DROP

```

...si se puede, antes de que lleguen a nuestra máquina.

## Alto Rendimiento

Llegamos a la parte que realmente importa de este documento.

En nuestra carrera por obtener un gran número de host pasando a través de nuestra máquina, olvidamos algunas cosas:

1.  Que tenemos solo una tarjeta para, potencialmente, más de 8000 direcciones físicas (MAC). ¡La memoria compartida de la tarjeta no está preparada para esto!
2.  Por defecto, iptables tampoco está preparado para trabajar con este gran número de conexiones simultáneas.

Asi que...

Para el primer problema... la solución es esta: aumentar el umbral de memoria para los vecinos.

Escriba esto y lea:

```
# cat /proc/sys/net/ipv4/neigh/default/gc_thresh1 
128
# cat /proc/sys/net/ipv4/neigh/default/gc_thresh2 
512
# cat /proc/sys/net/ipv4/neigh/default/gc_thresh3 
1024

```

Lo siguiente es poner este resultado en `/etc/sysctl.d/99-sysctl.conf`::

```
net.ipv4.neigh.default.gc_thresh1 = 512
net.ipv4.neigh.default.gc_thresh2 = 1024
net.ipv4.neigh.default.gc_thresh3 = 2048

```

Y ejecutar `syscrtl -p` para aumentar la memoria al doble (no es necesario reiniciar). ¡Con esto eliminaremos los errores relativos a la tarjeta!

Para la siguiente parte necesitaremos algún conocimiento sobre buckets, conntracks y hashsize (la manera de cómo iptables maneja las conecciones NAT). Existe un buen documento acerca de esto [aquí](http://www.wallfire.org/misc/netfilter_conntrack_perf.txt). ¡Léalo! Algunas cosas han cambiado desde que IPtables se conoce ahora como Netfiler.

En resumen:

Escriba esto en la sección `MODULES`:

```
MODULES=(8021q 'nf_conntrack hashsize=1048576' nf_conntrack_ftp 
                               ...y otros nf_stuff ...)

```

Lo último es solo para evitar algunos de los problemas que podríamos tener con conexiones ftp (esto ya no es necesario, pero lo mantenemos por si acaso). La seccion '**nf_conntrack hashsize=1048576'** incrementa el numero hashsize (incrementa la memoria del kernel destinada a las conecciones de NAT) (necesita reiniciar o **recargar el módulo** :-) escriba `dmesg | grep conntrack` antes y después, para ver los cambios).

Lo siguiente es poner algo similar en el archivo `/etc/sysctl.d/99-sysctl.conf`:

```
...
net.netfilter.nf_conntrack_max = 1048576
...

```

Y nuevamente ejecutamos la orden `sysctl --system`.

En mi caso, es el mismo número, esto significa que tengo una conexion por bucket. No necesito más. Por defecto NetFilter maneja una relación de 1:8, es decir, 8 conexiones por bucket (creo, no recuerdo bien).

En nuestro caso hemos llegado a tener mas de 600.000 conexiones simultáneas con 2 targetas de 1 GB. Se puede ver este numero con la siguiente orden:

```
# cat /proc/sys/net/netfilter/nf_conntrack_count

```

Y se puede poner en un agente snmp para poder graficarlo en algún servidor MRTG/cacti.

## Iproute2

¡Tenemos 3 grandes accesos a Internet! Esto se debe a que se trata de tres grupos de IP de clase C (relativo a algunas restricciones de BGP). Asi es que tenemos 3 traficos entrantes que podemos manejar, ¡pero solo uno de salida!, nuestro gateway principal. Esto podría fácilmente ocupar nuestro ancho de banda de salida. Asi que hay que separarlo.

Primero, añadimos algunas tablas en el archivo `/etc/iproute2/rt_tables`:

```
# echo 200 PRO_1 >> /etc/iproute2/rt_tables
# echo 205 PRO_2 >> /etc/iproute2/rt_tables
# echo 210 PRO_3 >> /etc/iproute2/rt_tables

```

Puede ser menos, o más, depende del tráfico.

Segundo, debemos dar un gateway por defecto a cada tabla:

```
# ip route add default via 200.aaa.bbb.2 table PRO_1
# ip route add default via 200.aaa.bbb.3 table PRO_2
# ip route add default via 200.aaa.bbb.4 table PRO_3

```

Es recomendable, pero no necesario (solo para obtener respuestas de pings o cosas similares), poner las redes locales y sus interfaces a cada tabla. Si no ponemos las siguientes líneas no obtendremos respuesta de ping en la red local, pero seguiremos teniendo conexión:

```
# ip route add 192.168.0.0/21 via 192.168.0.1 table PRO_1
# ip route add 192.168.8.0/21 via 192.168.8.1 table PRO_1
# ip route add 192.168.15.0/21 via 192.168.15.1 table PRO_1
...
same PRO_2, same PRO_3

```

Y, la última operación, es darle la orden a los paquetes entrantes:

```
# ip rule add from 192.168.0.0/21 table PRO_1
...
...

```

Una vez más, podemos jugar con PRO_X, e, incluso, podemos jugar con la máscara y submáscara. Por ejemplo, si solo le queremos dar a una clase C acceso por la tabla PRO_3:

```
# ip rule add from 192.168.1.0/24 table PRO_3

```

Hay que colocar esto antes de `<NET>/21`.