**Estado de la traducción**
Este artículo es una traducción de [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall"), revisada por última vez el **2018-09-05**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Simple_stateful_firewall&diff=0&oldid=538197) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Firewalls](/index.php/Firewalls "Firewalls")
*   [Internet sharing](/index.php/Internet_sharing "Internet sharing")
*   [Nftables#Simple stateful firewall](/index.php/Nftables#Simple_stateful_firewall "Nftables")
*   [Router](/index.php/Router "Router")
*   [Uncomplicated Firewall](/index.php/Uncomplicated_Firewall "Uncomplicated Firewall")

	Según [Wikipedia (en inglés)](https://en.wikipedia.org/wiki/Stateful_firewall "wikipedia:Stateful firewall")

	*Firewall Stateful es «en informática, un cortafuegos de estado (cualquier cortafuegos que realiza la inspección del estado de los paquetes (SPI) o la inspección de estado) es un cortafuegos que realiza un seguimiento del estado de las conexiones de red (por ejemplo, flujos TCP, comunicación UDP) que viajan a través de ella. El cortafuegos está programado para distinguir paquetes legítimos para diferentes tipos de conexiones. Solo los paquetes que coincidan con una conexión activa conocida serán permitidos por el cortafuegos; el resto serán rechazados».*

Esta página explica cómo configurar un cortafuegos [stateful](https://en.wikipedia.org/wiki/Stateful_firewall "wikipedia:Stateful firewall") usando [iptables](/index.php/Iptables_(Espa%C3%B1ol) "Iptables (Español)"). También explica lo que significan las reglas y por qué son necesarias. Para simplificar, se divide en dos secciones principales. La primera sección trata sobre la configuración de un cortafuegos para una sola máquina, la segunda establece la configuración de una puerta de enlace NAT además de la del cortafuegos de la primera sección.

**Advertencia:** Las reglas se dan en el orden en que se ejecutan. Si está conectado a una máquina remota, es posible que se cierre el acceso a la máquina, mientras crea las reglas. Solo debe seguir los siguientes pasos mientras se está conectado en el sistema local. El [ejemplo de archivo de configuración](#Archivo_resultante_de_iptables.rules) se puede utilizar para solucionar este problema.

## Contents

*   [1 Requisitos previos](#Requisitos_previos)
*   [2 Cortafuegos para una sola máquina](#Cortafuegos_para_una_sola_m.C3.A1quina)
    *   [2.1 Crear las cadenas necesarias](#Crear_las_cadenas_necesarias)
    *   [2.2 La cadena FORWARD](#La_cadena_FORWARD)
    *   [2.3 La cadena OUTPUT](#La_cadena_OUTPUT)
    *   [2.4 La cadena INPUT](#La_cadena_INPUT)
    *   [2.5 Archivo resultante de iptables.rules](#Archivo_resultante_de_iptables.rules)
    *   [2.6 Las cadenas TCP y UDP](#Las_cadenas_TCP_y_UDP)
        *   [2.6.1 Apertura de puertos para conexiones entrantes](#Apertura_de_puertos_para_conexiones_entrantes)
        *   [2.6.2 Golpear puertos](#Golpear_puertos)
    *   [2.7 Protección contra ataques de suplantación](#Protecci.C3.B3n_contra_ataques_de_suplantaci.C3.B3n)
    *   [2.8 «Ocultar» el ordenador](#.C2.ABOcultar.C2.BB_el_ordenador)
        *   [2.8.1 Bloquear solicitudes de ping](#Bloquear_solicitudes_de_ping)
        *   [2.8.2 Engañar a los analizadores de puertos](#Enga.C3.B1ar_a_los_analizadores_de_puertos)
            *   [2.8.2.1 Escaneos de SYN](#Escaneos_de_SYN)
            *   [2.8.2.2 Escaneos de UDP](#Escaneos_de_UDP)
            *   [2.8.2.3 Restaurar la regla final](#Restaurar_la_regla_final)
    *   [2.9 Protección contra otros ataques](#Protecci.C3.B3n_contra_otros_ataques)
        *   [2.9.1 Ataques de fuerza bruta](#Ataques_de_fuerza_bruta)
    *   [2.10 IPv6](#IPv6)
    *   [2.11 Guardar las reglas](#Guardar_las_reglas)
*   [3 Configurar una puerta de enlace NAT](#Configurar_una_puerta_de_enlace_NAT)
    *   [3.1 Configurar la tabla filter](#Configurar_la_tabla_filter)
        *   [3.1.1 Crear las cadenas necesarias](#Crear_las_cadenas_necesarias_2)
        *   [3.1.2 Configurar la cadena FORWARD](#Configurar_la_cadena_FORWARD)
        *   [3.1.3 Configurar las cadenas fw-interfaces y fw-open](#Configurar_las_cadenas_fw-interfaces_y_fw-open)
    *   [3.2 Configurar la tabla nat](#Configurar_la_tabla_nat)
        *   [3.2.1 Configurar la cadena POSTROUTING](#Configurar_la_cadena_POSTROUTING)
        *   [3.2.2 Configurar la cadena PREROUTING](#Configurar_la_cadena_PREROUTING)
    *   [3.3 Guardar las reglas](#Guardar_las_reglas_2)
*   [4 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Requisitos previos

**Nota:** El kernel debe ser compilado con soporte para iptables. Todos los kernels de stock de Arch Linux tienen soporte para iptables.

En primer lugar, instale las herramientas [iptables](https://www.archlinux.org/packages/?name=iptables) en el espacio de usuario o verifique que ya están instaladas.

Este artículo supone que no hay reglas iptables establecidas en su sistema. Para comprobar el conjunto de reglas vigentes y cerciorarse que no existen actualmente reglas, ejecute lo siguiente:

 `# iptables-save` 
```
# Generated by iptables-save v1.4.19.1 on Thu Aug  1 19:28:53 2013
*filter
:INPUT ACCEPT [50:3763]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [30:3472]
COMMIT
# Completed on Thu Aug  1 19:28:53 2013

```

o

 `# iptables -nvL --line-numbers` 
```
Chain INPUT (policy ACCEPT 156 packets, 12541 bytes)
num   pkts bytes target     prot opt in     out     source               destination

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 82 packets, 8672 bytes)
num   pkts bytes target     prot opt in     out     source               destination

```

Si hay reglas, podrá ser capaz de restablecerlas, cargando el conjunto de reglas por defecto:

```
# iptables-restore < /etc/iptables/empty.rules

```

De lo contrario, vea [Iptables (Español)#Restablecer las reglas](/index.php/Iptables_(Espa%C3%B1ol)#Restablecer_las_reglas "Iptables (Español)").

## Cortafuegos para una sola máquina

**Nota:** Puesto que las reglas de iptables siguen procesos en orden lineal, de arriba a abajo dentro de una cadena, se aconseja poner las reglas más frecuentemente afectadas al principio de la cadena. Por supuesto que hay un límite, en función de la lógica que se está implementando. Además, las reglas tienen un costo de tiempo de ejecución asociado, por lo que las reglas no deben ser reordenadas basandose únicamente en observaciones empíricas de los recuentos de bytes/paquetes de red.

### Crear las cadenas necesarias

Para esta configuración básica, vamos a crear dos cadenas, definidas por el usuario, que utilizaremos para abrir puertos en el cortafuegos.

```
# iptables -N TCP
# iptables -N UDP

```

Las cadenas pueden tener, por supuesto, nombres arbitrarios. Elegimos estos nombres solo para que coincidan con los protocolos que queremos manejar con ellos en las reglas posteriores, que se especifican con las opciones del protocolo, por ejemplo, `-p tcp`, siempre.

### La cadena FORWARD

Si desea configurar el equipo como una puerta de enlace NAT, vaya a [#Configurar una puerta de enlace NAT](#Configurar_una_puerta_de_enlace_NAT). Para una sola máquina, sin embargo, simplemente establecemos la política de la cadena **FORWARD** en **DROP** y continuamos con la configuración:

```
# iptables -P FORWARD DROP

```

### La cadena OUTPUT

No tenemos ninguna intención de filtrar todo el tráfico saliente, ya que esto haría la configuración mucho más complicada y requeriría alguna reflexión adicional. Para el caso simple que nos ocupa, ponemos la política **OUTPUT** en **ACCEPT**.

```
# iptables -P OUTPUT ACCEPT

```

### La cadena INPUT

De manera similar a las cadenas anteriores, fijamos la política predeterminada para la cadena **INPUT** en **DROP** como medida preventiva para evitar que se nos deslice algún error en nuestras reglas. Cerrar todo el tráfico y especificar luego qué tráfico entrante está permitido es la mejor manera de hacer un cortafuegos seguro.

**Advertencia:** Si está conectado a través de SSH, lo siguiente hará que se desconecte inmediatamente la sesión SSH. Para evitarlo: (1) añada la primera regla de la cadena INPUT de abajo (que mantendrá la sesión abierta), (2) añada una regla normal para permitir la entrada de SSH (para poder volver a reconectar en caso de una caída de la conexión) y (3) establezca la política de la cadena.

```
# iptables -P INPUT DROP

```

Cada paquete que se recibe por cualquier interfaz de red pasará primero por la cadena **INPUT**, si está destinado a nuestra máquina. Con esta cadena, nos aseguraremos de que solo los paquetes que queremos sean aceptados.

La primera regla añadida a la cadena INPUT permitirá el tráfico perteneciente a las conexiones ya establecidas, o para el nuevo tráfico válido relacionado con estas conexiones, como los errores ICMP, o las respuestas de Echo (los paquetes que retornan al equipo cuando se hace ping —«*(...) es un servicio de red que repite aquel comando que se le envía (como el eco). Es útil para hacer comprobaciones sobre el estado de la conectividad de una red»* ([fuente](https://en.wikipedia.org/wiki/esEcho_(inform%C3%A1tica) "wikipedia:esEcho (informática)"))—). **ICMP** (siglas en inglés de *Internet Control Message Protocol*) significa **Protocolo de Mensajes de Control de Internet**. Algunos mensajes [ICMP](https://en.wikipedia.org/wiki/es:Internet_Control_Message_Protocol "wikipedia:es:Internet Control Message Protocol") son muy importantes y ayudan a gestionar la congestión y [MTU](https://en.wikipedia.org/wiki/es:Unidad_m%C3%A1xima_de_transferencia "wikipedia:es:Unidad máxima de transferencia"), y son aceptados por esta regla.

El estado de conexión `ESTABLISHED` implica que, o bien otra regla anteriormente permitió la conexión inicial intentada (`--ctstate NEW`), o bien la conexión ya estaba activa (por ejemplo, una conexión SSH remota activa) al tiempo de establecer esta regla:

```
# iptables -A INPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT

```

La segunda regla aceptará todo el tráfico de la interfaz (lo) [«loopback»](https://en.wikipedia.org/wiki/es:Loopback "wikipedia:es:Loopback"), que es necesario para muchas aplicaciones y servicios.

**Nota:** Se pueden agregar las interfaces más fiables aquí como «eth1» si no quiere/necesita que el cortafuegos filtre el tráfico, pero tenga presente que si tiene una configuración NAT que redirige cualquier tipo de tráfico a esta interfaz desde otro lugar de la red (digamos un router), va a conseguir lo mismo a través de ello, independientemente de cualquier otra configuración que pueda tener.

```
# iptables -A INPUT -i lo -j ACCEPT

```

La tercera regla descartará todo el tráfico que coincida con el estado «INVALID». El tráfico puede agruparse en una de las cuatro categorías de «estado»: NEW, ESTABLISHED, RELATED o INVALID, y esto es lo que hace de este sea un cortafuegos «stateful» (podríamos definirlo como un cortafuegos de filtrado dinámico de paquetes), en lugar de un cortafuegos «stateless» (filtrado de paquetes sin estado) que es menos seguro. Los estados hacen un seguimiento usando los módulos del kernel «nf_conntrack_*» que se cargan automáticamente por el kernel a medida que se añaden las reglas.

**Nota:**

*   Esta regla descartará todos los paquetes con cabeceras o sumas de comprobación no válidas, indicadores TCP no válidos, mensajes ICMP no válidos (como un puerto inaccesible cuando no enviamos nada para el equipo), y descarta los paquetes secuenciados que pueden ser causados por la predicción de secuencia u otros ataques similares. El objetivo de «DROP» es descartar un paquete sin dar ninguna respuesta, contrariamente a REJECT que rechaza el paquete. Utilizamos DROP porque no hay una respuesta adecuada a los paquetes que no son válidos, y no queremos reconocer que hemos recibido esos paquetes.
*   Los paquetes [Neighbor Discovery](https://en.wikipedia.org/wiki/es:Neighbor_Discovery "wikipedia:es:Neighbor Discovery") de ICMPv6 permanecen sin seguimiento, y siempre se clasifican «INVALID» aunque no estén dañados o similares. Tenga esto presente, y acepte dicha situación antes de esta regla: iptables -A INPUT -p 41 -j ACCEPT

```
# iptables -A INPUT -m conntrack --ctstate INVALID -j DROP

```

La siguiente regla aceptará todos las nuevas peticiones de **ICMP echo requests**, también conocidas como pings. Solo el primer paquete contará como NUEVO, el resto estará a cargo de la regla RELATED,ESTABLISHED. Dado que el equipo no es un router, ningún otro tráfico ICMP con el estado NEW necesita ser permitido.

```
# iptables -A INPUT -p icmp --icmp-type 8 -m conntrack --ctstate NEW -j ACCEPT

```

Ahora asociamos las cadenas TCP y UDP a la cadena INPUT para manejar todas las nuevas conexiones entrantes. Una vez que una conexión es aceptada por la cadena TCP o UDP, la misma es manejada por la regla de tráfico RELATED/ESTABLISHED. Las cadenas TCP y UDP bien aceptan las nuevas conexiones entrantes, o bien las rechazan. Las nuevas conexiones TCP deben comenzar con paquetes SYN.

**Nota:** NEW pero no SYN es la única etiqueta TCP no válida no cubierta por el estado INVALID. La razón es porque raramente son paquetes maliciosos, y esto no basta para descartarlos. En su lugar, simplemente no los aceptamos, por lo que se rechazan con un [RST](https://en.wikipedia.org/wiki/es:RST_(flag) de TCP por la siguiente regla.

```
# iptables -A INPUT -p udp -m conntrack --ctstate NEW -j UDP
# iptables -A INPUT -p tcp --syn -m conntrack --ctstate NEW -j TCP

```

Rechazamos las conexiones TCP con paquetes RESET de TCP y flujos de UDP con mensaje de puerto ICMP inalcanzable, si no se abren los puertos. Esto imita el comportamiento predeterminado de Linux (RFC), y que permite al remitente cerrar rápidamente la conexión y limpiarla.

```
# iptables -A INPUT -p udp -j REJECT --reject-with icmp-port-unreachable
# iptables -A INPUT -p tcp -j REJECT --reject-with tcp-reset

```

Para otros protocolos, añadimos una regla final para la cadena INPUT para rechazar todo el tráfico entrante restante con protocolo ICMP de mensajes inaccesibles. Esto imita el comportamiento por defecto de Linux.

```
# iptables -A INPUT -j REJECT --reject-with icmp-proto-unreachable

```

### Archivo resultante de iptables.rules

He aquí un ejemplo de archivo `iptables.rules` que se obtendría después de ejecutar todas las órdenes anteriores:

 `/etc/iptables/iptables.rules` 
```
# Generated by iptables-save v1.4.18 on Sun Mar 17 14:21:12 2013
*filter
:INPUT DROP [0:0]
:FORWARD DROP [0:0]
:OUTPUT ACCEPT [0:0]
:TCP - [0:0]
:UDP - [0:0]
-A INPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A INPUT -i lo -j ACCEPT
-A INPUT -m conntrack --ctstate INVALID -j DROP
-A INPUT -p icmp -m icmp --icmp-type 8 -m conntrack --ctstate NEW -j ACCEPT
-A INPUT -p udp -m conntrack --ctstate NEW -j UDP
-A INPUT -p tcp --tcp-flags FIN,SYN,RST,ACK SYN -m conntrack --ctstate NEW -j TCP
-A INPUT -p udp -j REJECT --reject-with icmp-port-unreachable
-A INPUT -p tcp -j REJECT --reject-with tcp-reset
-A INPUT -j REJECT --reject-with icmp-proto-unreachable
COMMIT
# Completed on Sun Mar 17 14:21:12 2013

```

Este archivo se puede generar con:

```
# iptables-save > /etc/iptables/iptables.rules

```

y se puede utilizar como base para continuar con las siguientes secciones. Si va a configurar un cortafuegos de forma remota a través de SSH, añada la siguiente regla para permitir nuevas conexiones SSH antes de continuar (ajustar el puerto si es necesario):

```
-A TCP -p tcp --dport 22 -j ACCEPT

```

### Las cadenas TCP y UDP

Las cadenas TCP y UDP contienen reglas para la aceptación de nuevas conexiones [TCP](https://en.wikipedia.org/wiki/es: "wikipedia:es:") y flujos [UDP](https://en.wikipedia.org/wiki/es:User_Datagram_Protocol "wikipedia:es:User Datagram Protocol") entrantes para puertos específicos.

**Nota:** Aquí es donde necesita añadir reglas para aceptar conexiones entrantes, como SSH, HTTP u otros servicios a los que desee acceder de forma remota.

#### Apertura de puertos para conexiones entrantes

Para aceptar conexiones TCP entrantes en el puerto 80 para un servidor web:

```
# iptables -A TCP -p tcp --dport 80 -j ACCEPT

```

Para aceptar conexiones TCP entrantes en el puerto 443 para un servidor web (HTTPS):

```
# iptables -A TCP -p tcp --dport 443 -j ACCEPT

```

Para permitir conexiones remotas a través de SSH (en el puerto 22):

```
# iptables -A TCP -p tcp --dport 22 -j ACCEPT

```

Para aceptar transmisiones TCP/UDP entrantes en el puerto 53 para un servidor [DNS](/index.php/DNS "DNS"):

```
# iptables -A TCP -p tcp --dport 53 -j ACCEPT
# iptables -A UDP -p udp --dport 53 -j ACCEPT

```

Vea [iptables(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/iptables.8) para conocer reglas más avanzadas, como equipar múltiples puertos.

#### Golpear puertos

El [golpeo de puertos](https://en.wikipedia.org/wiki/es:Golpeo_de_puertos "wikipedia:es:Golpeo de puertos") es un método para abrir puertos externamente que, por defecto, el cortafuegos mantiene cerrado. Funciona al demandar intentos de conexión a una serie de puertos cerrados de forma predefinida. Cuando la secuencia correcta del puerto al que se «golpea» (intentos de conexión) es recibida, el cortafuegos abre determinado puerto(s) para permitir una conexión. Vea [Port knocking](/index.php/Port_knocking "Port knocking") para más información.

### Protección contra ataques de suplantación

**Nota:** `rp_filter` está ajustado actualmente en `1` por defecto en `/usr/lib/sysctl.d/50-default.conf`, por lo que el siguiente paso no es necesario.

El bloqueo de las direcciones locales reservadas entrantes desde Internet o red local se realiza normalmente a través de la configuración de `rp_filter` (Reverse Path Filter) en sysctl ajustándola a 1\. Para ello, añada la siguiente línea al archivo `/etc/sysctl.d/90-firewall.conf` (ver [sysctl](/index.php/Sysctl "Sysctl") para más detalles) para permitir la verificación de la dirección IP de origen que está integrado en el mismo kernel de Linux. La verificación por parte del kernel se encargará de la [suplantación de identidad o *spoofing*](https://en.wikipedia.org/wiki/es:Spoofing "wikipedia:es:Spoofing") mejor que las reglas de iptables individuales para cada caso.

```
net.ipv4.conf.all.rp_filter=1

```

Esto se puede hacer con netfilter en su lugar, si se desean estadíaticas (y mejorar el registro):

```
# iptables -t raw -I PREROUTING -m rpfilter --invert -j DROP

```

**Nota:** No hay ninguna razón para activar esto en ambos lugares. El método netfilter es la opción más moderna y también funciona con IPv6.

Solo cuando el enrutamiento es asíncrono, se debe utilizar la opción de sysctl `rp_filter=0`. Pasando el modificador `--loose` al módulo `rpfilter` se logrará lo mismo con netfilter.

### «Ocultar» el ordenador

Si está ejecutando una máquina de escritorio, esto podría ser una buena idea para bloquear algunas peticiones entrantes.

#### Bloquear solicitudes de ping

Una petición 'Ping' es un paquete ICMP enviado a la dirección IP de destino para garantizar la conectividad entre los dispositivos. Si la red funciona bien, puede bloquear de forma segura todas las solicitudes de ping. Es importante señalar que esto en realidad «no» oculta su ordenador —cualquier paquete que se le envíe será rechazado, por lo que aún se mostrará en un [nmap](https://en.wikipedia.org/wiki/es:Nmap "wikipedia:es:Nmap") simple de «escaneo de ping» de un conjunto de IP—.

Esta es una «protección» rudimentaria y hace más difícil la depuración de problemas en el futuro. Solo debe hacer esto para propósitos educativos.

Para bloquear las peticiones de Echo, añada la siguiente línea a su archivo `/etc/sysctl.d/90-firewall.conf` (ver [sysctl](/index.php/Sysctl "Sysctl") para más detalles):

```
net.ipv4.icmp_echo_ignore_all = 1

```

Puede encontrar más información en la página del manual de iptables, o leyendo la documentación y ejemplos en la página web [http://snowman.net/projects/ipt_recent/](http://snowman.net/projects/ipt_recent/)

#### Engañar a los analizadores de puertos

**Nota:**

*   Esto le abre a una forma de [DoS](https://en.wikipedia.org/wiki/es:Ataque_de_denegaci%C3%B3n_de_servicio "wikipedia:es:Ataque de denegación de servicio") (siglas en inglés de *Denial of Service* —ataque de denegación de servicios—). Un ataque puede enviar paquetes con direcciones IP falsas, y hacer que los recursos o servicios sean bloqueados para conectarse a los mismos por los usuarios legítimos.
*   Este truco puede bloquear una dirección IP legítima si algunos paquetes de red provenientes de esta dirección al puerto de destino se consideran NO VÁLIDOS por el módulo «*conntrack*». Para evitar su inclusión en listas negras, un cambio de tendencia es permitir que todos los paquetes se dirijan a ese puerto de destino particular.

Los escaneadores de puertos son utilizados por los atacantes para identificar los puertos abiertos en su equipo. Esto les permite identificar y analizar las huellas de sus servicios en ejecución y, posiblemente, lanzar [exploits](https://en.wikipedia.org/wiki/es:Exploit "wikipedia:es:Exploit") contra ellos.

La regla de estado INVALID se hará cargo de todos los tipos de escaneo de puertos, excepto para los escaneo de UDP, ACK y SYN (-sU, -sA y -sS en nmap, respectivamente).

Los *escaneos ACK* no se utilizan para identificar los puertos abiertos, pero si para identificar los puertos filtrados por un cortafuegos. Debido a la comprobación de SYN para todas las conexiones TCP con el estado NEW, cada paquete individual enviado por una exploración ACK será rechazado correctamente por un paquete TCP RST. Algunos cortafuegos bloquean estos paquetes en su lugar, y esto permite que un atacante pueda trazar las reglas del cortafuegos.

El módulo *recent* puede ser utilizado para engañar a los otros dos tipos de escaneos de puertos restantes. El módulo *recent* puede agregar equipos a una lista «recent» que se puede utilizar para los analizadores de huellas y detener ciertos tipos de ataques. Las listas *recent* actuales se pueden ver en `/proc/net/xt_recent/`.

##### Escaneos de SYN

En un escaneo SYN, el analizador de puertos envía paquetes SYN a cada puerto. Los puertos cerrados devuelven un paquete TCP RST, o son bloqueados por un cortafuegos estricto. Los puertos abiertos devuelven un paquete SYN ACK independientemente de la presencia o no de un cortafuegos.

El módulo recent se puede utilizar para realizar un seguimiento de los equipos con intentos rechazados y devolverles un TCP RST para cualquier paquete SYN que envían a puertos abiertos como si el puerto estuviera cerrado. Si un puerto abierto es el primero en ser escaneado, será devuelto un paquete SYN ACK pese a ello, por lo que las aplicaciones en ejecución, requieren que funcionen en puertos no esperados para que esto sea coherente, como ssh que debe ejecutarse en puertos no estándar.

En primer lugar, insertar una regla en la parte superior de la cadena TCP. Esta regla responde con un RST TCP a cualquier equipo añadido a la lista TCP PortScan en los últimos sesenta segundos. El parámetro `--update` hace que la lista recent se actualice, lo que hace que el contador de 60 segundo se restablezca.

```
# iptables -I TCP -p tcp -m recent --update --rsource --seconds 60 --name TCP-PORTSCAN -j REJECT --reject-with tcp-reset

```

A continuación, la regla para rechazar los paquetes TCP necesita ser modificada para incluir los equipos con paquetes rechazados en la lista TCP-PORTSCAN.

```
# iptables -D INPUT -p tcp -j REJECT --reject-with tcp-reset
# iptables -A INPUT -p tcp -m recent --set --rsource --name TCP-PORTSCAN -j REJECT --reject-with tcp-reset

```

##### Escaneos de UDP

Los escaneos de puertos UDP son similares a las exploraciones TCP SYN, excepto que UDP es un protocolo «sin conexión (previamente establecida)». No hay contacto ni reconocimiento. En cambio, el escáner envía paquetes UDP a cada puerto UDP. Los puertos cerrados devuelven mensajes ICMP de puertos inaccesibles, y los puertos abiertos no devuelven respuesta. Dado que UDP no es un protocolo «confiable», el escáner no tiene manera de saber si los paquetes se perdieron, y tiene que hacer varias comprobaciones para cada puerto que no devuelve una respuesta.

El kernel de Linux envía mensajes ICMP de puerto inaccesible muy lentamente, por lo que un escaneo UDP completo contra una máquina Linux podría durar más de 10 horas. Sin embargo, los puertos comunes todavía pudieron ser identificados, por lo que la aplicación de las mismas medidas contra escaneos de SYN para UDP es una buena idea.

En primer lugar, añada una regla para rechazar los paquetes de los equipos incluidos en la lista UDP-PortScan al inicio de la cadena de UDP.

```
# iptables -I UDP -p udp -m recent --update --rsource --seconds 60 --name UDP-PORTSCAN -j REJECT --reject-with icmp-port-unreachable

```

A continuación, modifique la regla de rechazo de paquetes para UDP:

```
# iptables -D INPUT -p udp -j REJECT --reject-with icmp-port-unreachable
# iptables -A INPUT -p udp -m recent --set --rsource --name UDP-PORTSCAN -j REJECT --reject-with icmp-port-unreachable

```

##### Restaurar la regla final

Si se utilizaron uno o ambas de los reglas de escaneo de puertos descritos, estas se colocarán por encima de la última regla por defecto, con lo cual esta última ya no será la regla final en la cadena INPUT. La regla por defecto tiene que ser la última regla, de lo contrario interferirá en las reglas del escaneo de puertos que acaba de agregar y nunca se utilizarán. Solo tiene que eliminar la regla (D) y, a continuación, añadirla (-A) de nuevo, lo que hará que la regla por defecto se coloque al final de la cadena.

```
# iptables -D INPUT -j REJECT --reject-with icmp-proto-unreachable
# iptables -A INPUT -j REJECT --reject-with icmp-proto-unreachable

```

### Protección contra otros ataques

Consulte [sysctl#TCP/IP stack hardening](/index.php/Sysctl#TCP.2FIP_stack_hardening "Sysctl") para conocer los parámetros del kernel más relevantes.

#### Ataques de fuerza bruta

Desafortunadamente, los ataques de fuerza bruta sobre los servicios accesibles a través de una dirección IP expuesta públicamente son comunes. Una razón para esto es que los ataques son fáciles de hacer con las muchas herramientas disponibles. Afortunadamente, hay varias formas de proteger los servicios contra ellos. Una de ellas es el uso de reglas apropiadas `iptables` que activen e incluyan en una lista negra las direcciones IP después de que estas hayan intentado iniciar una conexión de forma infructuosa con un número determinado de paquetes. Otro es el uso de demonios especializados que controlen los archivos del registro de intentos fallidos y la lista negra en consecuencia.

**Advertencia:** El uso de una lista negra de IP detendrá ataques triviales pero la misma se apoya en un demonio adicional y un registro de éxito (la partición que contiene /var puede llegar a saturarse, especialmente si un atacante golpea con fuerza en el servidor). Además, si el atacante conoce su dirección IP, puede enviar paquetes con un encabezado de origen falso y conseguir bloquearle el servidor. [SSH keys](/index.php/SSH_keys "SSH keys") proporciona una solución elegante al problema de la fuerza bruta sin estos problemas.

Dos aplicaciones que prohíben direcciones IP después de demasiados fracasos con la contraseña son [Fail2ban](/index.php/Fail2ban "Fail2ban") o, para `sshd` en particular, [Sshguard (Español)](/index.php/Sshguard_(Espa%C3%B1ol) "Sshguard (Español)"). Estas dos aplicaciones actualizan las reglas de iptables para rechazar futuras conexiones desde direcciones IP incluidas en la lista negra.

Las siguientes reglas se dan como un ejemplo de configuración para mitigar los ataques de fuerza bruta contra SSH utilizando `iptables`.

```
# iptables -N IN_SSH
# iptables -A INPUT -p tcp --dport ssh -m conntrack --ctstate NEW -j IN_SSH
# iptables -A IN_SSH -m recent --name sshbf --rttl --rcheck --hitcount 3 --seconds 10 -j DROP
# iptables -A IN_SSH -m recent --name sshbf --rttl --rcheck --hitcount 4 --seconds 1800 -j DROP 
# iptables -A IN_SSH -m recent --name sshbf --set -j ACCEPT

```

La mayoría de las opciones pueden explicarse por sí mismas, así las reglas precedentes permiten tres paquetes de conexión cada diez segundos. El resto de intentos en ese lapso de tiempo incluyen la IP en la lista negra. La siguiente regla añade una peculiaridad, al permitir un total de cuatro intentos en 30 minutos. Esto se hace porque algunos ataques de fuerza bruta que se realizan son realmente lentos y no en un estallido de intentos. Las reglas emplean una serie de opciones adicionales. Para leer más acerca de ellas, revise la referencia original para este ejemplo: [compilefailure.blogspot.com](http://compilefailure.blogspot.com/2011/04/better-ssh-brute-force-prevention-with.html)

Las reglas anteriores se pueden usar para proteger cualquier servicio, aunque el demonio SSH es probablemente uno de los más solicitado.

En términos de orden, uno debe asegurarse de que `-A INPUT -p tcp --dport ssh -m conntrack --ctstate NEW -j IN_SSH` esté en la posición correcta en la secuencia de iptables: debe aparecer antes que el de La cadena TCP que está conectada a INPUT para detectar nuevas conexiones SSH primero. Si se han completado todos los pasos anteriores de esta wiki, funcionaría con el siguiente posicionamiento:

```
...
-A INPUT -m conntrack --ctstate INVALID -j DROP
-A INPUT -p icmp -m icmp --icmp-type 8 -m conntrack --ctstate NEW -j ACCEPT
**-A INPUT -p tcp --dport 22 -m conntrack --ctstate NEW -j IN_SSH**
-A INPUT -p udp -m conntrack --ctstate NEW -j UDP
-A INPUT -p tcp --tcp-flags FIN,SYN,RST,ACK SYN -m conntrack --ctstate NEW -j TCP
...

```

**Sugerencia:** Para autodiagnosticar las reglas después de su configuración, la gestión de la lista negra vigente puede ralentizar la prueba, lo que dificultará afinar los parámetros. Se pueden ver los intentos de entrada a través de `cat /proc/net/xt_recent/sshbf`. Para desbloquear la propia IP durante las pruebas, se necesitan privilegios de root `# echo / > /proc/net/xt_recent/sshbf`

### IPv6

Si no utiliza IPv6, considere [desactivarlo](/index.php/Disabling_IPv6 "Disabling IPv6"), de lo contrario, siga estos pasos para activar las reglas de IPv6 para el cortafuegos.

Copie las reglas IPv4 utilizadas en este ejemplo como base, y cambie cualquier IP del formato IPv4 al formato IPv6:

```
# cp /etc/iptables/iptables.rules /etc/iptables/ip6tables.rules

```

A few of the rules in this example have to be adapted for use with IPv6\. The ICMP protocol has been updated in IPv6, replacing the ICMP protocol for use with IPv4\. Hence, the reject error return codes `--reject-with icmp-port-unreachable` and `--reject-with icmp-proto-unreachable` have to be converted to ICMPv6 codes.

Algunas de las reglas de este ejemplo deben adaptarse para su uso con IPv6\. El protocolo ICMP se ha actualizado en IPv6, reemplazando el protocolo ICMP para su uso con IPv4\. Por lo tanto, los códigos de retorno de error de rechazo `--reject-with icmp-port-unreachable` y {{ic | --reject-with icmp-proto-unreachable}. Por lo tanto, los códigos de retorno de error de rechazo `--reject-with icmp-port-unreachable` y `--reject-with icmp-proto-unreachable` tienen que ser convertidos en códigos ICMPv6.

Los códigos de error de ICMPv6 disponibles se enumeran en [RFC 4443](https://tools.ietf.org/html/rfc4443#section-3.1), que especifica que una regla de cortafuegos para bloquear los intentos de conexión debe utilizar `--reject-with icmp6-adm-prohibited`. Si lo bloquea, básicamente informa al sistema remoto que la conexión fue rechazada por el cortafuegos, en lugar de informar que un servicio fue escuchado.

Si se prefiere no informar explícitamente acerca de la existencia de un filtro en el cortafuegos, el paquete también puede ser rechazado sin el mensaje:

```
 -A INPUT -j REJECT

```

Lo anterior va a rechazar con la devolución de error por defecto `--reject-with-icmp6-port-unreachable`. Debe tener en cuenta, sin embargo, que la identificación de un cortafuegos es una característica básica de las aplicaciones de escaneo de puertos y la mayoría va a identificarlo a pesar de todo.

El siguiente paso es asegurarse de que el protocolo y la extensión se cambian al apropiado para IPv6 en la regla de todas las nuevas peticiones de echo ICMP entrantes (pings):

```
# ip6tables -A INPUT -p ipv6-icmp --icmpv6-type 128 -m conntrack --ctstate NEW -j ACCEPT

```

conntrack de netfilter no parece hacer el seguimiento del Protocolo Neighbor Discovery de ICMPv6 (el IPv6 equivalente de ARP), así que tenemos que permitir el tráfico ICMPv6 sin importar el estado para todas las subredes conectadas directamente. Lo siguiente debe insertarse después de descartar `--ctstate INVALID`, pero antes de cualquier otro objetivo DROP o REJECT, junto con la línea correspondiente de cada subred conectada directamente:

```
# ip6tables -A INPUT -s fe80::/10 -p ipv6-icmp -j ACCEPT

```

Como no existe un filtro de ruta inversa del kernel para IPv6, es posible que desee habilitar uno en *ip6tables* con lo siguiente:

```
# ip6tables -t raw -A PREROUTING -m rpfilter -j ACCEPT
# ip6tables -t raw -A PREROUTING -j DROP

```

### Guardar las reglas

El conjunto de reglas ya está terminado y se debe guardar en el disco duro para que pueda ser cargado en cada arranque.

Guarde las reglas de IPv4 y IPv6 con estas órdenes

```
# iptables-save > /etc/iptables/iptables.rules
# ip6tables-save > /etc/iptables/ip6tables.rules

```

Después [active](/index.php/Enable "Enable") e [inicie](/index.php/Start "Start") `iptables.service` y `ip6tables.service`. Compruebe el estado de los servicios para asegurarse de que las reglas estén cargadas correctamente.

## Configurar una puerta de enlace NAT

Esta sección de la guía trata sobre la configuración de una puerta de enlace [NAT](https://en.wikipedia.org/wiki/es:Network_Address_Translation "wikipedia:es:Network Address Translation") (siglas en inglés de Network Address Translation —conversión de direcciones de red—). Se supone que ya ha leído la [primera parte de la guía](#Cortafuegos_para_una_sola_m.C3.A1quina) y configurado las cadenas **INPUT**, **OUTPUT**, **TCP** y **UDP** como se ha descrito anteriormente. Todas las reglas hasta ahora se han creado en la tabla **filter**. En esta sección, también vamos a tener que utilizar la tabla **nat**.

### Configurar la tabla filter

#### Crear las cadenas necesarias

En nuestra configuración, utilizaremos otras dos cadenas en la tabla de filtros, las cadenas **fw-interfaces** y **fw-open** que crearemos con las siguientes órdenes:

```
# iptables -N fw-interfaces
# iptables -N fw-open

```

#### Configurar la cadena FORWARD

La creación de la cadena **FORWARD** es similar a la cadena **INPUT** de la primera parte de esta guía.

Ahora establecemos una regla con **conntrack**, idéntica a la de la cadena **INPUT**:

```
# iptables -A FORWARD -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT

```

El siguiente paso es activar el reenvío para las interfaces de confianza y hacer que todos los paquetes pasen por la cadena **fw-open**.

```
# iptables -A FORWARD -j fw-interfaces 
# iptables -A FORWARD -j fw-open 

```

A los paquetes restantes se les niega con un mensaje **ICMP**:

```
# iptables -A FORWARD -j REJECT --reject-with icmp-host-unreach
# iptables -P FORWARD DROP

```

#### Configurar las cadenas fw-interfaces y fw-open

El significado de las cadenas **fw-interfaces** y **fw-open** se explica más adelante, cuando nos ocupemos de las cadenas **POSTROUTING** y **PREROUTING** en la tabla **nat**, respectivamente.

### Configurar la tabla nat

En toda esta sección, se supone que la interfaz de salida (la que tiene la IP expuesta públicamente a internet) es **ppp0**. Tenga en cuenta que tiene que cambiar el nombre en todas las reglas siguientes si su interfaz de salida tiene otro nombre.

#### Configurar la cadena POSTROUTING

Ahora, tenemos que definir quién tiene permisos para conectarse a Internet. Supongamos que tenemos la subred **192.168.0.0/24** (que significa que todas las direcciones tienen el formato 192.168.0.*) en **eth0**. Primero tenemos que aceptar las máquinas en esta interfaz en la tabla FORWARD, es por eso que hemos creado la cadena **fw-interfaces** anterior:

```
# iptables -A fw-interfaces -i eth0 -j ACCEPT

```

Ahora, tenemos que modificar todos los paquetes salientes de manera que tengan nuestra dirección IP pública como la dirección IP de origen, en lugar de la dirección LAN local. Para ello, utilizamos el objetivo **MASQUERADE**:

```
# iptables -t nat -A POSTROUTING -s 192.168.0.0/24 -o ppp0 -j MASQUERADE

```

No se olvide el parámetro **-o ppp0** anterior. Si lo omite, su red no funcionará.

Supongamos que tenemos otra subred, **10.3.0.0/16** (que comprende todas las direcciones 10.3.*.*), en la interfaz **eth1**. Añadimos las mismas reglas que antes, además de:

```
# iptables -A fw-interfaces -i eth1 -j ACCEPT
# iptables -t nat -A POSTROUTING -s 10.3.0.0/16 -o ppp0 -j MASQUERADE

```

El último paso es activar [activar el reenvío de paquetes de red](/index.php/Internet_sharing#Enable_packet_forwarding "Internet sharing") (si no está ya activado):

Las máquinas de estas subredes pueden ahora utilizar su nueva máquina NAT como su puerta de enlace. Tenga en cuenta que es posible que desee configurar un servidor DNS y [DHCP](/index.php/DHCP "DHCP") como [dnsmasq](/index.php/Dnsmasq "Dnsmasq") o una combinación de [BIND](/index.php/BIND "BIND") and [dhcpd](/index.php/Dhcpd "Dhcpd") para simplificar la configuración de red en la resolución de DNS en los equipos clientes. Este no es el tema de esta guía.

#### Configurar la cadena PREROUTING

A veces, queremos cambiar la dirección de un paquete entrante de la puerta de entrada a una máquina de la LAN. Para ello, utilizamos la cadena **fw-open** definida antes, así como la cadena **PREROUTING** de la tabla **nat**.

Daremos dos ejemplos sencillos: en primer lugar, queremos cambiar todos los paquetes entrantes SSH (puerto 22) al servidor ssh en la máquina **192.168.0.5**:

```
# iptables -t nat -A PREROUTING -i ppp0 -p tcp --dport 22 -j DNAT --to 192.168.0.5
# iptables -A fw-open -d 192.168.0.5 -p tcp --dport 22 -j ACCEPT

```

El segundo ejemplo le mostrará cómo cambiar los paquetes a un puerto diferente del puerto de entrada. Queremos cambiar cualquier conexión entrante en el puerto **8000** en nuestro servidor web **192.168.0.6**, al puerto **80**:

```
# iptables -t nat -A PREROUTING -i ppp0 -p tcp --dport 8000 -j DNAT --to 192.168.0.6:80
# iptables -A fw-open -d 192.168.0.6 -p tcp --dport 80 -j ACCEPT

```

La misma configuración también funciona con los paquetes UDP.

### Guardar las reglas

Guarde las reglas con:

```
# iptables-save > /etc/iptables/iptables.rules

```

Esto supone que ha seguido los pasos [anteriores](#Guardar_las_reglas) para activar el servicio de systemd **iptables**.

## Véase también

*   [Methods to block SSH attacks](http://www.webhostingtalk.com/showthread.php?t=456571)
*   [Using iptables to block brute force attacks](http://www.ducea.com/2006/06/28/using-iptables-to-block-brute-force-attacks/)
*   [20 Iptables Examples For New SysAdmins](http://linuxconfig.org/collection-of-basic-linux-firewall-iptables-rules)
*   [25 Most Frequently Used Linux IPTables Rules Examples](http://www.thegeekstuff.com/2011/06/iptables-rules-examples/)