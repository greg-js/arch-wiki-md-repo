**Estado de la traducción**
Este artículo es una traducción de [Iptables](/index.php/Iptables "Iptables"), revisada por última vez el **2018-09-04**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Iptables&diff=0&oldid=536649) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Fail2ban](/index.php/Fail2ban "Fail2ban")
*   [Nftables (Español)](/index.php/Nftables_(Espa%C3%B1ol) "Nftables (Español)")
*   [Sshguard (Español)](/index.php/Sshguard_(Espa%C3%B1ol) "Sshguard (Español)")
*   [Simple stateful firewall (Español)](/index.php/Simple_stateful_firewall_(Espa%C3%B1ol) "Simple stateful firewall (Español)")
*   [Sysctl#TCP/IP stack hardening](/index.php/Sysctl#TCP.2FIP_stack_hardening "Sysctl")

*iptables* es una utilidad de línea de órdenes para configurar el [cortafuegos](/index.php/Firewalls_(Espa%C3%B1ol) "Firewalls (Español)") del kernel de Linux implementado como parte del proyecto [Netfilter](https://en.wikipedia.org/wiki/es:Netfilter "wikipedia:es:Netfilter"). El término *iptables* también se usa comúnmente para referirse a dicho cortafuegos del kernel. Puede configurarse directamente con iptables, o usando uno de los muchos frontend existentes de [consola](#De_consola) y [gráficos](#Gr.C3.A1ficos). El término *iptables* se usa para [IPv4](https://en.wikipedia.org/wiki/IPv4 "wikipedia:IPv4"), y el término *ip6tables* para [IPv6](/index.php/IPv6 "IPv6"). Tanto *iptables* como *ip6tables* tienen la misma sintaxis, pero algunas opciones son específicas de IPv4 o de IPv6.

[nftables](/index.php/Nftables "Nftables") está programada para [ser liberada con el kernel de Linux 3.13](http://www.phoronix.com/scan.php?page=news_item&px=MTQ5MDU), y vendrá a sustituir definitivamente iptables como la principal utilidad del cortafuegos de Linux.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 Frontend](#Frontend)
        *   [1.1.1 De consola](#De_consola)
        *   [1.1.2 Gráficos](#Gr.C3.A1ficos)
*   [2 Conceptos básicos](#Conceptos_b.C3.A1sicos)
    *   [2.1 Tablas](#Tablas)
    *   [2.2 Cadenas](#Cadenas)
    *   [2.3 Reglas](#Reglas)
    *   [2.4 Cadenas transversales](#Cadenas_transversales)
    *   [2.5 Módulos](#M.C3.B3dulos)
*   [3 Configuración y utilización](#Configuraci.C3.B3n_y_utilizaci.C3.B3n)
    *   [3.1 Desde la línea de órdenes](#Desde_la_l.C3.ADnea_de_.C3.B3rdenes)
        *   [3.1.1 Mostrar las reglas vigentes](#Mostrar_las_reglas_vigentes)
        *   [3.1.2 Restablecer las reglas](#Restablecer_las_reglas)
        *   [3.1.3 Modificar las reglas](#Modificar_las_reglas)
    *   [3.2 Guías](#Gu.C3.ADas)
*   [4 Registro](#Registro)
    *   [4.1 Limitar el tamaño del registro](#Limitar_el_tama.C3.B1o_del_registro)
    *   [4.2 Visualizar los paquetes registrados](#Visualizar_los_paquetes_registrados)
    *   [4.3 syslog-ng](#syslog-ng)
    *   [4.4 ulogd](#ulogd)
*   [5 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

Todos los kernels de serie de Arch Linux son compatibles con iptables. Solo necesita [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") las herramientas en el [espacio de usuario](https://en.wikipedia.org/wiki/es:Espacio_de_usuario "wikipedia:es:Espacio de usuario"), que son proporcionadas por el paquete [iptables](https://www.archlinux.org/packages/?name=iptables). El paquete [iproute2](https://www.archlinux.org/packages/?name=iproute2) presente en el grupo [base](https://www.archlinux.org/groups/x86_64/base/) depende de iptables, por lo que el paquete iptables debe estar instalado en su sistema por defecto.

### Frontend

#### De consola

*   **Arno's firewall** — Es un cortafuegos seguro, útil tanto para uno como para varios equipos. Muy fácil de configurar, de administrar y altamente personalizable. Admite: NAT y SNAT, reenvío de puertos, gestión de asignación de IP tanto estáticas como dinámicamente para módems ADSL ethernet, filtrado de direcciones MAC, detección de escaneo sigiloso de puertos, desvío DMZ y DMZ-2-LAN, protección contra saturación SYN/ICMP, amplio registro definible por el usuario con limitación de velocidad para evitar desbordamiento de registros, todos los protocolos IP y VPN tales como IPsec, compatibilidad con complementos para agregar funciones adicionales.

	[http://rocky.eld.leidenuniv.nl/](http://rocky.eld.leidenuniv.nl/) || [arno-iptables-firewall](https://aur.archlinux.org/packages/arno-iptables-firewall/)

*   **ferm** — Herramienta para mantener cortaguegos complejos, sin problemas para reescribir reglas complejas una y otra vez. Permite que todo el conjunto de reglas del cortaguegos se almacene en un archivo separado y se cargue con una orden. La configuración del cortaguegos se asemeja a un lenguaje estructurado similar al de programación, que puede contener niveles y listas.

	[http://ferm.foo-projects.org/](http://ferm.foo-projects.org/) || [ferm](https://www.archlinux.org/packages/?name=ferm)

*   **[FireHOL](https://en.wikipedia.org/wiki/FireHOL "wikipedia:FireHOL")** — Lenguaje para diseñar reglas de cortaguegos, no un simple script que lance un cortaguegos. Hace que construir cortaguegos, incluso sofisticados, sea fácil, de la manera que lo desee.

	[http://firehol.sourceforge.net/](http://firehol.sourceforge.net/) || [firehol](https://aur.archlinux.org/packages/firehol/)

*   **Firetable** — Herramienta para mantener un cortaguegos de IPtables. Cada interfaz se puede configurar por separado a través de su propio archivo de configuración, que tiene una sintaxis fácil de leer.

	[https://gitlab.com/hsleisink/firetable](https://gitlab.com/hsleisink/firetable) || [firetable](https://aur.archlinux.org/packages/firetable/)

*   **[firewalld](https://en.wikipedia.org/wiki/firewalld "wikipedia:firewalld") (firewall-cmd)** — Demonio e interfaz de consola para configurar zonas de red y cortafuegos, así como establecer y configurar las reglas del cortafuegos.

	[https://firewalld.org/](https://firewalld.org/) || [firewalld](https://www.archlinux.org/packages/?name=firewalld)

*   **[Shorewall](/index.php/Shorewall "Shorewall")** — Herramienta de alto nivel para configurar Netfilter. Se describen los requisitos del cortafuegos/puerta de enlace usando las entradas presentes en un conjunto de archivos de configuración.

	[http://www.shorewall.net/](http://www.shorewall.net/) || [shorewall](https://www.archlinux.org/packages/?name=shorewall)

*   **[Uncomplicated Firewall](/index.php/Uncomplicated_Firewall "Uncomplicated Firewall")** — Frontend simple para iptables.

	[https://launchpad.net/ufw](https://launchpad.net/ufw) || [ufw](https://www.archlinux.org/packages/?name=ufw)

*   **[PeerGuardian](/index.php/PeerGuardian_Linux "PeerGuardian Linux") (pglcmd)** — Aplicación de cortafuegos orientada a la privacidad. Bloquea las conexiones hacia y desde los hosts especificados en listas de bloques de gran tamaño (miles o millones de rangos de IP).

	[http://sourceforge.net/projects/peerguardian/](http://sourceforge.net/projects/peerguardian/) || [pgl](https://aur.archlinux.org/packages/pgl/)

*   **Vuurmuur** — Potente administrador de cortafuegos. Tiene un diseño simple y fácil de aprender que permite configuraciones simples y complejas. La configuración se puede definir completamente a través de una interfaz [ncurses](https://www.archlinux.org/packages/?name=ncurses), que permite una administración remota segura a través de SSH o a través de la consola. Vuurmuur es compatible con el tráfico de red compartido, y cuenta con poderosas funciones de monitorización que permiten al administrador fiscalizar los registros, las conexiones y el uso del ancho de banda en tiempo real.

	[https://www.vuurmuur.org/](https://www.vuurmuur.org/) || [vuurmuur](https://aur.archlinux.org/packages/vuurmuur/)

#### Gráficos

*   **Firewall Builder** — Interfaz para la administración y configuración de cortafuegos compatible con iptables (netfilter), ipfilter, pf, ipfw, Cisco PIX (FWSM, ASA) y listas de acceso ampliado de enrutadores Cisco. El programa se puede ejecurtar en Linux, FreeBSD, OpenBSD, Windows y macOS, y puede administrar cortafuegos tanto locales como remotos.

	[http://fwbuilder.sourceforge.net/](http://fwbuilder.sourceforge.net/) || [fwbuilder](https://www.archlinux.org/packages/?name=fwbuilder)

*   **[firewalld](https://en.wikipedia.org/wiki/firewalld "wikipedia:firewalld") (firewall-config)** — Demonio e interfaz gráfica que permite configurar zonas de red y cortafuegos, así como establecer y configurar reglas del cortafuegos.

	[https://firewalld.org/](https://firewalld.org/) || [firewalld](https://www.archlinux.org/packages/?name=firewalld)

*   **[Gufw](/index.php/Uncomplicated_Firewall#Gufw "Uncomplicated Firewall")** — Interfaz basada en GTK para [ufw](https://www.archlinux.org/packages/?name=ufw) que pasa a ser un frontend CLI para iptables (gufw->ufw->iptables), es muy fácil y simple de usar.

	[http://gufw.org/](http://gufw.org/) || [gufw](https://www.archlinux.org/packages/?name=gufw)

*   **[PeerGuardian](/index.php/PeerGuardian_Linux "PeerGuardian Linux") GUI (pglgui)** — Aplicación de cortafuegos orientada a la privacidad. Bloquea las conexiones hacia y desde los servidores definidos en listas de bloques de gran tamaño (miles o millones de rangos de IP).

	[http://sourceforge.net/projects/peerguardian/](http://sourceforge.net/projects/peerguardian/) || [pgl](https://aur.archlinux.org/packages/pgl/)

## Conceptos básicos

iptables se usa para inspeccionar, modificar, reenviar, redirigir y/o eliminar paquetes de red de IP. El código para filtrar paquetes de IP ya está integrado en el kernel y está organizado en una colección de *tablas*, cada una con un propósito específico. Las tablas están formadas por un conjunto de *cadenas* predefinidas, y las cadenas contienen reglas que se recorren en orden consecutivo. Cada regla consiste en una condición asociada a una eventual acción (llamada *target*) que si se cumple, se ejecuta la regla; esto es, se aplican las reglas si las condiciones coinciden. iptables es la utilidad de usuario que le permite trabajar con estas cadenas/reglas. La mayoría de los usuarios nuevos consideran que las complejidades del enrutamiento IP de linux son bastante desalentadoras, pero, en la práctica, los casos de uso más comunes (NAT y/o cortafuegos básico de Internet) son considerablemente menos complejos.

La clave para entender cómo funciona iptables es [este gráfico](http://www.frozentux.net/iptables-tutorial/images/tables_traverse.jpg). La palabra minúscula en la parte superior es la *tabla* y la palabra en mayúscula siguiente es la *cadena*. Cada paquete de IP que viene en «cualquier interfaz de red» pasa a través de este diagrama de flujo de arriba hacia abajo. Una confusión muy común es creer que los paquetes que ingresan desde, (digamos, para entendernos), una interfaz interna para consumo interno, se manejan de forma diferente a los paquetes desde una interfaz orientada a Internet. Todas las interfaces se manejan de la misma manera. Depende de uno definir las reglas que las traten de manera diferente. Por supuesto, algunos paquetes están destinados a procesos locales, por lo tanto, vienen desde la parte superior del gráfico y se detienen en <Proceso local>; mientras que otros paquetes son generados por procesos locales; por lo tanto, comienzan en <Proceso local> y continúan hacia abajo a través del diagrama de flujo. Puede encontrar una explicación detallada de cómo funciona este diagrama de flujo [aquí](http://www.frozentux.net/iptables-tutorial/iptables-tutorial.html#TRAVERSINGOFTABLES).

En la gran mayoría de los casos, no será necesario utilizar las tablas **raw**, **mangle**, o **security** a la vez. En consecuencia, el siguiente cuadro muestra un flujo simplificado de paquetes de red a través de *iptables*:

```
                               XXXXXXXXXXXXXXXXXX
                               XXX     Red    XXX
                               XXXXXXXXXXXXXXXXXX
                                        +
                                        |
                                        v
 +--------------+             +-------------------+
 |tabla:  filter| <---+       | tabla:  nat       |
 |cadena: INPUT |     |       | cadena: PREROUTING|
 +-----+--------+     |       +--------+----------+
       |              |                 |
       v              |                 v
 [proceso local]      |     ************************       +---------------+
       |              +---+ Decisión de enrutamiento +---> |tabla: filter  |
       v                    ************************       |cadena: FORWARD|
************************                                   +------+--------+
Decisión de enrutamiento                                          |
************************                                          |
       |                                                          |
       v                    ************************              |
+--------------+      +---+ Decisión de enrutamiento <------------+
|tabla:  nat   |      |     ************************
|cadena: OUTPUT|      |                +
+-----+--------+      |                |
      |               |                v
      v               |      +--------------------+
+---------------+     |      | tabla: nat         |
|tabla:  filter | +---+      | cadena: POSTROUTING|
|cadena: OUTPUT |            +--------+-----------+
+---------------+                      |
                                       v
                               XXXXXXXXXXXXXXXXXX
                               XXX    Red     XXX
                               XXXXXXXXXXXXXXXXXX

```

### Tablas

iptables cuenta con cinco tablas:

1.  `raw` filtra los paquetes antes que cualquier otra tabla. Se utiliza principalmente para configurar exenciones de seguimiento de conexiones en combinación con el objetivo `NOTRACK`.
2.  `filter` es la tabla por defecto (si no se pasa la opción `-t`).
3.  `nat` se utiliza para la [traducción de direcciones de red](https://en.wikipedia.org/wiki/es:Network_address_translation "wikipedia:es:Network address translation") (por ejemplo, el redirección de puertos). Debido a las limitaciones en iptables, el filtrado no se debe hacer aquí.
4.  `mangle` se utiliza para la alteración de los paquetes de red especializados (véase [Mangles packet](https://en.wikipedia.org/wiki/Mangled_packet "wikipedia:Mangled packet")).
5.  `security` se utiliza para reglas de conexión de red [Mandatory Access Control](/index.php/Security#Mandatory_access_control "Security") (por ejemplo, SELinux —consulte [este artículo](http://lwn.net/Articles/267140/) para obtener más detalles—).

En la mayoría de los casos al uso, solo utilizará dos de estas tablas: **filter** y **nat**. Las otras tablas están destinadas a configuraciones complejas que afectan a múltiples enrutadores y decisiones de enrutamiento que, en cualquier caso, quedan fuera de las explicaciones de este artículo.

### Cadenas

Las tablas contienen *cadenas*, que son listas de reglas que se siguen consecutivamente. Por defecto, la tabla `filter` contiene tres cadenas integradas: `INPUT`, `OUTPUT` y `FORWARD` que se activan en diferentes puntos del proceso de filtrado de paquetes de red, como se ilustra en el [diagrama de flujo](http://www.frozentux.net/iptables-tutorial/chunkyhtml/images/tables_traverse.jpg). La tabla nat incluye las cadenas `PREROUTING`, `POSTROUTING`, y `OUTPUT`.

Véase [iptables(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/iptables.8) para obtener una descripción de las cadenas integradas en otras tablas.

Por defecto, ninguna de las cadenas contiene ninguna regla. Depende de uno agregar reglas a las cadenas que quiera usar. Las cadenas *hacen* lo definido en su política predeterminada, que generalmente se establece en `ACCEPT`, pero se puede restablecer a `DROP`, si quiere asegurarse de que nada se desliza a través de su conjunto de reglas. La política predeterminada siempre se aplica al final de una cadena solamente. Por lo tanto, el paquete de red debe pasar por todas las reglas existentes en la cadena antes de aplicar la política predeterminada.

El usuario puede definir las reglas de las cadenas para hacerlas más eficientes o más fácilmente modificable. Consulte [Simple stateful firewall (Español)](/index.php/Simple_stateful_firewall_(Espa%C3%B1ol) "Simple stateful firewall (Español)") para ver un ejemplo de cómo se usan las cadenas definidas por el usuario.

### Reglas

El filtrado de los paquetes de red se basa en *rules* —*«reglas»*—, que se especifican por diversos *matches* —*«coincidencias»*— (condiciones que el paquete de red debe satisfacer para que la regla se puede aplicar), y un *target*—*«objetivo»*— (acción a tomar cuando el paquete coincide con la condición plenamente). The typical things a rule might match on are what interface the packet came in on (e.g eth0 or eth1), what type of packet it is (ICMP, TCP, or UDP), or the destination port of the packet.

Los targets se especifican mediante la opción `-j` o `--jump` —*«salto»*—. Los targets pueden ser bien cadenas definidas por el usuario, bien uno de los targets integrados especiales, o bien una extensión de target. Los targets integrados son `ACCEPT`, `DROP`, `QUEUE` y `RETURN`; las extensiones de target son, por ejemplo, `REJECT` y `LOG`. Si el objetivo es un target integrado, el destino del paquete es decidido inmediatamente y el procesamiento del paquete de red en la tabla actual se detiene. Si el objetivo («*target*») es una cadena definida por el usuario y el paquete supera con éxito esta segunda cadena, se moverá a la siguiente regla de la cadena original. Las extensiones de target pueden ser tanto *terminating* (como los targets integrados) como *non-terminating* (como las cadenas especificadas por el usuario), Véase [iptables-extensions(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/iptables-extensions.8) para obtener más detalles

### Cadenas transversales

Un paquete de red recibido en cualquier interfaz atraviesa las cadenas de control de tráfico de las tablas en el orden que se muestra en el [diagrama de flujo](http://www.frozentux.net/iptables-tutorial/chunkyhtml/images/tables_traverse.jpg). La primera decisión de enrutamiento implica decidir si el destino final del paquete es el equipo local (en cuyo caso el paquete atraviesa las cadenas `INPUT`) o va a otro lugar (en cuyo caso el paquete atraviesa las cademas `FORWARD` cadenas). Las decisiones de enrutamiento posteriores implican decidir qué interfaz asignar a un paquete saliente. En cada cadena subsiguiente, cada regla de esa cadena se atraviesa en el orden fijado, y siempre que una regla coincida, se ejecuta la acción, target/jump, correspondiente. Los 3 objetivos (*targets*) más comúnmente utilizados son `ACCEPT`, `DROP` y jump para una cadena definida por el usuario. Mientras que las cadenas integradas pueden tener políticas predeterminadas, las cadenas definidas por el usuario no pueden. Si todas las reglas de una cadena no proporcionan una coincidencia completa que permita ejecutarla, el paquete se devuelve a la cadena de llamadas como se ilustra [aquí](http://www.frozentux.net/iptables-tutorial/images/table_subtraverse.jpg). Si en algún momento se logra una coincidencia completa para una regla con un objetivo `DROP`, el paquete se descarta y no se realiza ningún otro procesamiento. Si un paquete está `ACCEPT` dentro de una cadena, también estará `ACCEPT` en todas las cadenas del superconjunto y no atravesará ninguna cadena más de ese superconjunto. Sin embargo, tenga en cuenta que el paquete continuará atravesando todas las demás cadenas en otras tablas de la manera descrita.

### Módulos

Hay muchos módulos que pueden ser utilizados para reforzar iptables, como connlimit, conntrack, limit y recent. Estos módulos añaden funcionalidad extra al permitir reglas de filtrado avanzadas.

## Configuración y utilización

iptables es un servicio de [systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") y estará predispuesto a [iniciarse](/index.php/Start "Start") adecuadamente. Sin embargo, el servicio no se iniciará a menos que encuentre un archivo `/etc/iptables/iptables.rules`, que no es proporcionado por el paquete [iptables](https://www.archlinux.org/packages/?name=iptables) de Arch. Por tanto, para iniciar el servicio por primera vez, ejecute:

```
# touch /etc/iptables/iptables.rules

```

o

```
# cp /etc/iptables/empty.rules /etc/iptables/iptables.rules

```

Luego, [inicie](/index.php/Start "Start") la unidad `iptables.service`. Al igual que con otros servicios, si desea que iptables se cargue automáticamente en el arranque, debe [activarlo](/index.php/Enable "Enable").

Las reglas de iptables para IPv6 se almacenan de manera predeterminada en el archivo `/etc/iptables/ip6tables.rules`, que es leído por `ip6tables.service`. Puede iniciarlo de la misma manera que hemos visto arriba.

Después de añadir reglas a través de la línea de órdenes como se muestra en las siguientes secciones, el archivo de configuración no guarda los cambios automáticamente —tiene que guardarlos manualmente—, así:

```
# iptables-save > /etc/iptables/iptables.rules

```

Si modifica el archivo de configuración manualmente, debe [recargar](/index.php/Reload "Reload") iptables.

O puede cargarlo directamente a través de iptables:

```
# iptables-restore < /etc/iptables/iptables.rules

```

### Desde la línea de órdenes

#### Mostrar las reglas vigentes

La órden básica para listar las reglas en vigor es `--list-rules` (`-S`), que es similar en formato de salida a la utilidad *iptables-save*. La diferencia principal entre las dos es que este último genera las reglas de todas las tablas por defecto, mientras que todos las órdenes de *iptables* están predeterminadas solo para la tabla `filter`.

Al trabajar con iptables en la línea de órdenes, la orden `--list` (`-L`) acepta más modificadores y muestra más información. Por ejemplo, puede verificar el conjunto de reglas en vigor y el número de visitas por regla usando la orden:

 `# iptables -nvL` 
```
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination
```

Si el resultado es similar a lo de arriba, entonces no hay reglas (es decir, nada está bloqueado) en la tabla predeterminada `filter`. Se puede especificar otra tabla con la opción `-t`.

Para mostrar los números de línea cuando se enumeran las reglas, anexe `--line-numbers` a dicha entrada. Los números de línea son una abreviatura útil cuando [modifica reglas](#Modificar_las_reglas) en la línea de órdenes.

#### Restablecer las reglas

Puede vaciar y restablecer la configuración, por defecto, de iptables utilizando las siguientes órdenes:

```
# iptables -F
# iptables -X
# iptables -t nat -F
# iptables -t nat -X
# iptables -t mangle -F
# iptables -t mangle -X
# iptables -t raw -F
# iptables -t raw -X
# iptables -t security -F
# iptables -t security -X
# iptables -P INPUT ACCEPT
# iptables -P FORWARD ACCEPT
# iptables -P OUTPUT ACCEPT

```

La orden `-F` sin argumentos vuelca todas las cadenas en su tabla actual. Del mismo modo, `-X` elimina todos las cadenas vacías no predeterminadas en una tabla.

Las cadenas individuales pueden ser eliminadas o borradas con `-F` y `-X` seguidas de un argumento `[chain]`.

#### Modificar las reglas

Las reglas pueden ser añadidas o bien como un apéndice a las reglas o a las cadenas, o bien insertarlas en una específica posición en la cadena. Exploraremos ambos métodos.

Antes de nada, nuestro equipo no es un router (salvo que, por supuesto, lo [sea](/index.php/Router "Router")). Cambiaremos la política, por defecto, en la cadena `FORWARD`, de `ACCEPT` a `DROP`.

```
# iptables -P FORWARD DROP

```

**Advertencia:** El resto de esta sección está destinada a enseñar la sintaxis y los conceptos que se esconden detrás de las reglas de iptables. No tiene la pretensión de enseñar cómo proteger los servidores. Para mejorar la seguridad de su sistema, consulte [Simple stateful firewall (Español)](/index.php/Simple_stateful_firewall_(Espa%C3%B1ol) "Simple stateful firewall (Español)") para una configuración de iptables mínimamente segura y [Security](/index.php/Security "Security") para proteger Arch Linux en general.

El servicio LAN de sincronización de [Dropbox](https://en.wikipedia.org/wiki/es:Dropbox "wikipedia:es:Dropbox") tiene la característica de [transmitir paquetes de red cada 30 segundos](https://isc.sans.edu/port.html?port=17500) a todos los equipos que estén en su área inalámbrica. Si estamos en una zona LAN con clientes de Dropbox y no usamos esta característica, entonces podríamos quererla para rechazar los paquetes.

```
# iptables -A INPUT -p tcp --dport 17500 -j REJECT --reject-with icmp-port-unreachable

```
 `# iptables -nvL --line-numbers` 
```
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination
1        0     0 REJECT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0            tcp dpt:17500 reject-with icmp-port-unreachable

Chain FORWARD (policy DROP 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

```

**Nota:** Utilizamos `REJECT` en lugar de `DROP` aquí, porque [RFC 1122 3.3.8](https://tools.ietf.org/html/rfc1122#page-69) requiere que los hosts devuelvan los errores ICMP siempre que sea posible, en vez de dejar caer los paquetes de red. [Esta página](http://www.chiark.greenend.org.uk/~peterb/network/drop-vs-reject) explica por qué casi siempre es mejor RECHAZAR («*REJECT* ») en lugar de SOLTAR («*DROP* ») los paquetes de red.

Ahora, supongamos que decidimos utilizar Dropbox e instalarlo en nuestro ordenador. También queremos la sincronización LAN, pero solo con una IP en particular en nuestra red. Así que debemos utilizar `-R` para sustituir nuestra antigua regla. Donde `10.0.0.85` es nuestra otra IP:

```
# iptables -R INPUT 1 -p tcp --dport 17500 ! -s 10.0.0.85 -j REJECT --reject-with icmp-port-unreachable

```
 `# iptables -nvL --line-numbers` 
```
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination
1        0     0 REJECT     tcp  --  *      *      !10.0.0.85            0.0.0.0/0            tcp dpt:17500 reject-with icmp-port-unreachable

Chain FORWARD (policy DROP 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

```

Hemos reemplazado nuestra regla original con otra que nos permite usar `10.0.0.85` para acceder al puerto `17500` de nuestro equipo. Pero ahora nos damos cuenta de que este no es escalable. Si un usuario amigable de Dropbox está intentando acceder al puerto `17500` de nuestro dispositivo, se debe permitir acceder de inmediato, sin comprobación frente a cualquier regla de firewall que esté detrás.

Así que escribimos una nueva regla para permitir que nuestro usuario de confianza acceda inmediatamente. Utilizaremos `-I` para insertar la nueva regla antes de la antigua:

```
# iptables -I INPUT 1 -p tcp --dport 17500 -s 10.0.0.85 -j ACCEPT -m comment --comment "Friendly Dropbox"

```

```
# iptables -nvL --line-numbers

```

```
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination         
1        0     0 ACCEPT     tcp  --  *      *       10.0.0.85            0.0.0.0/0            tcp dpt:17500 /* Friendly Dropbox */
2        0     0 REJECT     tcp  --  *      *      !10.0.0.85            0.0.0.0/0            tcp dpt:17500 reject-with icmp-port-unreachable

Chain FORWARD (policy DROP 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination         

Chain OUTPUT (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination    

```

Y reemplazar nuestra segunda regla con otra que rechace todo lo demás que entre al puerto `17500`:

```
# iptables -R INPUT 2 -p tcp --dport 17500 -j REJECT --reject-with icmp-port-unreachable

```

La lista de nuestra regla final ahora se vería así:

 `# iptables -nvL --line-numbers` 
```
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination
1        0     0 ACCEPT     tcp  --  *      *       10.0.0.85            0.0.0.0/0            tcp dpt:17500 /* Friendly Dropbox */
2        0     0 REJECT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0            tcp dpt:17500 reject-with icmp-port-unreachable

Chain FORWARD (policy DROP 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

```

### Guías

*   [Simple stateful firewall (Español)](/index.php/Simple_stateful_firewall_(Espa%C3%B1ol) "Simple stateful firewall (Español)")
*   [Router](/index.php/Router "Router")

## Registro

El objetivo `LOG` se puede utilizar para registrar los paquetes de red que satisfacen una regla. A diferencia de otros targets, como `ACCEPT` o `DROP`, el paquete de red continuará moviéndose a través de la cadena después de alcanzar un target `LOG`. Esto significa que, para activar el registro de todos los paquetes de red perdidos, se tendría que agregar una regla `LOG` duplicada antes de cada regla DROP. Como esto reduce la eficiencia y hace que las cosas sean menos simples, se puede crear, en su lugar, una cadena `logdrop`.

Cree la cadena con:

```
# iptables -N logdrop

```

Y añada las siguientes reglas a la cadena recién creada:

```
# iptables -A logdrop -m limit --limit 5/m --limit-burst 10 -j LOG
# iptables -A logdrop -j DROP

```

La explicación de las opciones `limit` y `limit-burst` son dadas [a continuación](#Limitar_el_tama.C3.B1o_del_registro).

Ahora, cada vez que queremos soltar un paquete de red y registrar este evento, simplemente saltamos a la cadena `logdrop`, por ejemplo:

```
# iptables -A INPUT -m conntrack --ctstate INVALID -j logdrop

```

### Limitar el tamaño del registro

La cadena de arriba (`logdrop`) utiliza el módulo *limit* para prevenir que el registro de *iptables* se haga demasiado grande o haga que el disco duro se escriba innecesariamente. Sin limitación, un atacante podría llenar el disco (o al menos la partición `/var`) causando la saturación del registro de iptables.

`-m limit` se utiliza para llamar al módulo limit. Puede usar `--limit` para utilizar una tasa promedio y `--limit-burst` para establecer una tasa de ráfaga (*«limit burst»*) inicial. En el ejemplo de `logdrop` de arriba:

```
iptables -A logdrop -m limit --limit 5/m --limit-burst 10 -j LOG

```

Esto agrega una regla a la cadena `logdrop` que registra todos los paquetes de red que pasan a través de ella. Los primeros 10 paquetes serán registrados, y de ahí en adelante quedarán registrados únicamente 5 paquetes por minuto. El «limit burst» es restaurado a uno cada vez que la «tasa límite» no se supera.

### Visualizar los paquetes registrados

Los paquetes registrados son visibles como mensajes del kernel con el [journal de systemd](/index.php/Systemd_journal "Systemd journal").

Para ver todos los paquetes que se registraron desde la última vez que se reinició el equipo:

```
# journalctl -k | grep "IN=.*OUT=.*" | less

```

### syslog-ng

Asumiendo que usa [syslog-ng](/index.php/Syslog-ng "Syslog-ng"), puede controlar donde será guardada la salida del registro de iptables, de este modo:

```
filter f_everything { level(debug..emerg) and not facility(auth, authpriv); };

```

a

```
filter f_everything { level(debug..emerg) and not facility(auth, authpriv) and not filter(f_iptables); };

```

Esto evitará la salida del registro de iptables en el archivo `/var/log/everything.log`.

Si quiere que el registro de iptables se vuelque en un archivo distinto de `/var/log/iptables.log`, basta con cambiar el valor de destino de `d_iptables` (siempre en el archivo `syslog-ng.conf`).

```
destination d_iptables { file("/var/log/iptables.log"); };

```

### ulogd

[ulogd](http://www.netfilter.org/projects/ulogd/index.html) es un demonio especializado en el registro de los paquetes de red ejecutado en el espacio de usuario para netfilter que puede sustituir el objetivo `LOG` predeterminado. El paquete [ulogd](https://www.archlinux.org/packages/?name=ulogd) está disponible en el repositorio `[community]`.

## Véase también

*   [Wikipedia article](https://en.wikipedia.org/wiki/iptables "wikipedia:iptables")
*   [Port knocking](/index.php/Port_knocking "Port knocking")
*   [Official iptables web site](http://www.netfilter.org/projects/iptables/index.html)
*   [iptables Tutorial 1.2.2](http://www.frozentux.net/iptables-tutorial/iptables-tutorial.html) por Oskar Andreasson
*   [Debian Wiki - iptables](https://wiki.debian.org/iptables "debian:iptables")
*   [Secure use of connection tracking helpers](https://home.regit.org/netfilter-en/secure-use-of-helpers/)