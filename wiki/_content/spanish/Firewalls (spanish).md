Un [cortafuegos](https://en.wikipedia.org/wiki/es:Cortafuegos_(inform%C3%A1tica) es un sistema diseñado para prevenir el acceso no autorizado a una red privada (que podría ser, incluso, a una sola máquina) o proveniente de ella. Los cortafuegos pueden ser implementados en hardware o software separadamente, o en una combinación de ambos. Los cortafuegos se utilizan, con frecuencia, para evitar que los usuarios de Internet no autorizados tengan acceso a redes privadas conectadas a Internet, especialmente [intranets](https://en.wikipedia.org/wiki/es:Intranet "wikipedia:es:Intranet"). Todos los paquetes que entren o salgan de la intranet pasan a través del cortafuegos, que examina cada paquete y permite o deniega (esto es, realiza la función de un servidor [proxy](https://en.wikipedia.org/wiki/es:Proxy "wikipedia:es:Proxy")),el tráfico en función de los criterios de seguridad especificados.

Los cortafuegos que figuran en este artículo se basan en los programas [iptables](/index.php/Iptables_(Espa%C3%B1ol) "Iptables (Español)"). Considere la posibilidad de configurar los procesos [iptables](https://en.wikipedia.org/wiki/es:Netfilter/iptables "wikipedia:es:Netfilter/iptables") siguiendo el mismo procedimiento descrito en las páginas de la wiki (indicadas a continuación) para mantener la filosofía [The Arch Way](/index.php/The_Arch_Way "The Arch Way").

Hay muchos posts en los foros sobre las diferentes aplicaciones y scripts de cortafuegos, de forma que aquí están todos condensados en una sola página —por favor, añada sus comentarios acerca de cada cortafuegos, sobre todo la facilidad de uso y el control de la seguridad en [Shields Up](https://www.grc.com/x/ne.dll?bh0bkyd2)—.

**Nota:** Los controles en Shields Up son solo una medida válida del propio router en caso de tener uno conectado a la LAN. Para evaluar con precisión un cortafuegos de software, hay que conectar la caja directamente al módem de cable.

## Contents

*   [1 Tutoriales y guías de cortafuegos](#Tutoriales_y_gu.C3.ADas_de_cortafuegos)
    *   [1.1 Tutoriales de cortafuegos externos](#Tutoriales_de_cortafuegos_externos)
*   [2 iptables](#iptables)
    *   [2.1 Frontends de consola](#Frontends_de_consola)
    *   [2.2 Frontends gráficos](#Frontends_gr.C3.A1ficos)
*   [3 Otros](#Otros)
*   [4 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Tutoriales y guías de cortafuegos

*   [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall") — Trata sobre la configuración de un cortafuegos integral con [iptables](/index.php/Iptables_(Espa%C3%B1ol) "Iptables (Español)").

*   [Uncomplicated Firewall](/index.php/Uncomplicated_Firewall "Uncomplicated Firewall") — Página de ArchWiki sobre la interfaz simple de [iptables](/index.php/Iptables_(Espa%C3%B1ol) "Iptables (Español)"), [**ufw**](https://en.wikipedia.org/wiki/es:Uncomplicated_Firewall "wikipedia:es:Uncomplicated Firewall") — Proporciona un buen tutorial para una configuración básica.

*   Guía de configuración del [Router](/index.php/Router "Router") — Un tutorial para convertir un ordenador en una [puesta de enlace](https://en.wikipedia.org/wiki/es:Puerta_de_enlace "wikipedia:es:Puerta de enlace")/[router](https://en.wikipedia.org/wiki/es:Router "wikipedia:es:Router") de Internet. Se centra en la [seguridad](/index.php/Security "Security") y la configuración de la puerta de enlace (*gateway*) para tener el menor número de agujeros de seguridad posibles en Internet.

#### Tutoriales de cortafuegos externos

*   [http://www.frozentux.net/documents/iptables-tutorial/](http://www.frozentux.net/documents/iptables-tutorial/) Un tutorial de iptables fácil y completo.

*   [http://tldp.org/HOWTO/Masquerading-Simple-HOWTO/IP](http://tldp.org/HOWTO/Masquerading-Simple-HOWTO/IP) Masq es una forma de *traducción de direcciones de red* (o [NAT](https://en.wikipedia.org/wiki/es:Network_Address_Translation "wikipedia:es:Network Address Translation")) que permite a los ordenadores conectados en una red privada, que no cuentan con más de una IP registrada, tener la posibilidad de comunicarse todos ellos con Internet, usando una máquina Linux con solo una IP.

*   [http://tldp.org/HOWTO/Masquerading-Simple-HOWTO/](http://tldp.org/HOWTO/Masquerading-Simple-HOWTO/) Enmascaramiento de IP, [proxy transparente](https://en.wikipedia.org/wiki/es:Proxy#Proxies_transparentes "wikipedia:es:Proxy"), [redirección de puerto](https://en.wikipedia.org/wiki/es:Redirecci%C3%B3n_de_puertos "wikipedia:es:Redirección de puertos") y otras formas de traducción de direcciones de red con los kernels 2.4 de Linux.

## iptables

El kernel de Linux incluye [iptables](/index.php/Iptables_(Espa%C3%B1ol) "Iptables (Español)") como una solución de cortafuegos integrada. La configuración puede ser gestionada directamente a través de las utilidades del espacio de usuario o mediante la instalación de una de las distintas herramientas gráficas de configuración existentes.

### [Frontends](https://en.wikipedia.org/wiki/es:Front-end_y_back-end "wikipedia:es:Front-end y back-end") de consola

*   **Arno's firewall** — Es un cortafuegos de seguridad para ordenadores tanto individuales como [multihomed](https://en.wikipedia.org/wiki/Multihoming "wikipedia:Multihoming"). Fácil de configurar y altamente personalizable. Proporciona soporte para: NAT y SNAT, redirección de puertos, módems ADSL Ethernet con direcciones IP estáticas y asignadas dinámicamente, filtrado de direcciones MAC, detección de escaneo sigiloso de puertos, transmisión de DMZ y DMZ-2-LAN, protección contra saturación de SYN/ICMP, registros definibles por el usuario con cadencia y límites para evitar la saturación del registro en el disco, todos los protocolos IP y VPN como IPsec, soporte para plugins para añadir características adicionales.

	[http://rocky.eld.leidenuniv.nl/](http://rocky.eld.leidenuniv.nl/) || [arno-iptables-firewall](https://aur.archlinux.org/packages/arno-iptables-firewall/)

*   **ferm** — (del acrónimo *«For Easy Rule Making»*) Es una herramienta para mantener cortafuegos complejos, sin tener la molestia de reescribir reglas complejas una y otra vez. ferm permite guardar el completo conjunto de reglas en un archivo separado, y cargarlas con una sola orden. La configuración del cortafuegos se parece a un lenguaje de programación estructurado, que puede contener niveles y listas.

	[http://ferm.foo-projects.org/](http://ferm.foo-projects.org/) || [ferm](https://www.archlinux.org/packages/?name=ferm)

*   **Firehol** — Es un lenguaje para expresar reglas del cortafuegos, y no solo un script que da origen a cualquier tipo de cortafuegos. Esto hace que la construcción sea fácil hasta para cortafuegos sofisticados —allí hasta donde uno esté dispuesto a diseñarlo—. El resultado es, en realidad, las reglas de iptables.

	[http://firehol.sourceforge.net/](http://firehol.sourceforge.net/) || [firehol](https://aur.archlinux.org/packages/firehol/)

*   **Firetable** — Es un cortafuegos basado en iptables, con una sintaxis «legible».

	[http://projects.leisink.net/Firetable](http://projects.leisink.net/Firetable) || [firetable](https://aur.archlinux.org/packages/firetable/)

*   **[Shorewall](/index.php/Shorewall "Shorewall")** — Es una herramienta de alto nivel para la configuración de Netfilter. Se describen los requisitos del cortafuegos/puerta de acceso usando entradas en un conjunto de archivos de configuración.

	[http://www.shorewall.net/](http://www.shorewall.net/) || [shorewall](https://www.archlinux.org/packages/?name=shorewall)

*   **[ufw](/index.php/Ufw "Ufw")** — (del acrónimo *«uncomplicated firewall»*) Es una sencilla interfaz para iptables.

	[https://launchpad.net/ufw](https://launchpad.net/ufw) || [ufw](https://www.archlinux.org/packages/?name=ufw)

*   **[PeerGuardian Linux](/index.php/PeerGuardian_Linux "PeerGuardian Linux")** — Aplicación de cortafuegos orientada a la privacidad. Bloquea las conexiones hacia y desde los hosts especificados en grandes listas de bloqueo (que pueden ir desde miles a millones de rangos IP).

	[http://sourceforge.net/projects/peerguardian/](http://sourceforge.net/projects/peerguardian/) || [pgl-cli](https://aur.archlinux.org/packages/pgl-cli/)

*   **Vuurmuur** — Es un potente gestor de cortafuegos construido sobre iptables. Tiene una configuración simple y fácil de aprender, que permite configuraciones tanto sencillas como complejas. La configuración puede ser totalmente modelable a través de una interfaz gráfica [ncurses](https://www.archlinux.org/packages/?name=ncurses), que permite la administración remota segura a través de SSH o desde la consola. Vuurmuur soporta [catalogación de tráfico](https://en.wikipedia.org/wiki/es:Traffic_shaping "wikipedia:es:Traffic shaping"), y cuenta con potentes funciones de vigilancia, que permiten al administrador ver los registros, las conexiones y el uso del ancho de banda en tiempo real.

	[http://www.vuurmuur.org/](http://www.vuurmuur.org/) || [vuurmuur](https://aur.archlinux.org/packages/vuurmuur/)

### Frontends gráficos

*   **Firestarter** — Es una buena interfaz gráfica de usuario para iptables, escrito en GTK2, que tiene la capacidad de utilizar tanto las listas blancas como negras para regular el tráfico; es muy simple y fácil de usar, y posee una buena documentación disponible en su página web.

	[http://www.fs-security.com/](http://www.fs-security.com/) || [Firestarter](https://aur.archlinux.org/packages/Firestarter/)

*   **Firewall Builder** — Herramienta gráfica de gestión y configuración de cortafuegos que soporta iptables (netfilter), ipfilter, pf, ipfw, Cisco PIX (FWSM, ASA) y las listas de acceso extendida de los routers Cisco. El programa se ejecuta en Linux, FreeBSD, OpenBSD, Windows y Mac OS X, y puede gestionar tanto servidores de seguridad locales como remotos.

	[http://www.fwbuilder.org/](http://www.fwbuilder.org/) || [fwbuilder](https://www.archlinux.org/packages/?name=fwbuilder)

*   **firewalld** — Demonio e interfaz gráfica para configurar zonas de conexiones de red y cortafuegos, así como para instalar y configurar reglas de cortafuegos.

	[https://fedoraproject.org/wiki/FirewallD](https://fedoraproject.org/wiki/FirewallD) || [firewalld](https://www.archlinux.org/packages/?name=firewalld)

*   **[Gufw](/index.php/Uncomplicated_Firewall#Gufw "Uncomplicated Firewall")** — Un frontend basado en GTK para [ufw](https://www.archlinux.org/packages/?name=ufw), que pasa a ser un frontend del intérprete de la línea de órdenes ([CLI](https://en.wikipedia.org/wiki/es:L%C3%ADnea_de_comandos "wikipedia:es:Línea de comandos")) para iptables (gufw → ufw → iptables); es muy fácil y sencillo de usar.

	[http://gufw.org/](http://gufw.org/) || [gufw](https://www.archlinux.org/packages/?name=gufw)

*   **KMyFirewall** — Es una interfaz gráfica de KDE3 para iptables. Las capacidades de edición del cortafuegos son bastante simples de usar, lo que lo hace adecuado para principiantes, pero también permiten ajustes sofisticados en la configuración del cortafuegos.

	[http://kmyfirewall.sourceforge.net/](http://kmyfirewall.sourceforge.net/) || [kmyfirewall](https://aur.archlinux.org/packages/kmyfirewall/)

*   **[PeerGuardian Linux](/index.php/PeerGuardian_Linux "PeerGuardian Linux")** — Aplicación de cortafuegos orientada a la privacidad. Bloquea las conexiones hacia y desde los hosts especificados en grandes listas de bloqueo (que pueden ir desde miles a millones de rangos IP).

	[http://sourceforge.net/projects/peerguardian/](http://sourceforge.net/projects/peerguardian/) || [pgl](https://aur.archlinux.org/packages/pgl/)

*   **[kcm-ufw](/index.php/Uncomplicated_Firewall#kcm-ufw "Uncomplicated Firewall")** — Es una alternativa de KDE para Gufw.

	[http://kde-apps.org/content/show.php?content=137789](http://kde-apps.org/content/show.php?content=137789) || [kcm-ufw](https://aur.archlinux.org/packages/kcm-ufw/)

## Otros

*   **[EtherApe](https://en.wikipedia.org/wiki/EtherApe "wikipedia:EtherApe")** — Proporciona una monitorización gráfica de la red para diversos protocolos y capas [OSI](https://en.wikipedia.org/wiki/es:Modelo_OSI "wikipedia:es:Modelo OSI").

	[http://etherape.sourceforge.net/](http://etherape.sourceforge.net/) || [etherape](https://www.archlinux.org/packages/?name=etherape)

*   **[Fail2ban](/index.php/Fail2ban "Fail2ban")** — Efectúa el [*baneo*](https://en.wikipedia.org/wiki/es:Ban "wikipedia:es:Ban") (restricción) de las IP después de varios intentos de autenticación fallidos al entrar en confrontación con los demonios más comunes.

	[http://www.fail2ban.org/](http://www.fail2ban.org/) || [fail2ban](https://www.archlinux.org/packages/?name=fail2ban)

## Véase también

*   [http://wiki.debian.org/Firewalls](http://wiki.debian.org/Firewalls) — Lista de cortafuegos de la wiki de Debian.