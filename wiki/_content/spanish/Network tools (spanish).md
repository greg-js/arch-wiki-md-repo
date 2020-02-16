**Estado de la traducción**
Este artículo es una traducción de [Network tools](/index.php/Network_tools "Network tools"), revisada por última vez el **2020-02-12**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Network_tools&diff=0&oldid=593921) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Telnet](/index.php/Telnet_(Espa%C3%B1ol) "Telnet (Español)")
*   [Nmap](/index.php/Nmap "Nmap")
*   [Wireshark](/index.php/Wireshark "Wireshark")

Esta página lista varias herramientas de red. *ping* e *ip* son cubiertos en [Configuración de red](/index.php/Network_configuration_(Espa%C3%B1ol) "Network configuration (Español)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Traceroute](#Traceroute)
*   [2 Netcat](#Netcat)
*   [3 Whois](#Whois)
*   [4 inetd](#inetd)
*   [5 Véase también](#Véase_también)

## Traceroute

[Traceroute](https://en.wikipedia.org/wiki/es:Traceroute "wikipedia:es:Traceroute") es una herramienta para mostrar la ruta de los paquetes a través de una red IP.

Hay varias implementaciones disponibles:

*   [tracepath(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tracepath.8) de [iputils](https://www.archlinux.org/packages/?name=iputils) (requerido por [base](https://www.archlinux.org/packages/?name=base))
*   [traceroute(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/traceroute.8) de [traceroute](https://www.archlinux.org/packages/?name=traceroute)
*   **MTR** — Combina las funcionalidades de traceroute y ping en una sola herramienta.

	[http://www.bitwizard.nl/mtr/](http://www.bitwizard.nl/mtr/) || [mtr](https://www.archlinux.org/packages/?name=mtr), [mtr-gtk](https://www.archlinux.org/packages/?name=mtr-gtk)

## Netcat

Véase también [Wikipedia:es:Netcat](https://en.wikipedia.org/wiki/es:Netcat "wikipedia:es:Netcat").

*   **GNU Netcat** — Reescritura de netcat por GNU, la aplicación de canalización *(piping)* de red. No soporta IPv6.

	[http://netcat.sourceforge.net/](http://netcat.sourceforge.net/) || [gnu-netcat](https://www.archlinux.org/packages/?name=gnu-netcat)

*   **LibreSSL netcat** — Herramienta de conexión UDP/TCP de bajo nivel con soporte para el protocolo TLS.

	[https://www.libressl.org](https://www.libressl.org) || [libressl-netcat](https://aur.archlinux.org/packages/libressl-netcat/)

*   **Ncat** — Implementación Netcat del proyecto Nmap.

	[https://nmap.org/ncat/](https://nmap.org/ncat/) || [nmap](https://www.archlinux.org/packages/?name=nmap)

*   **openbsd-netcat** — Navaja suiza TCP/IP. Variante de OpenBSD.

	[https://packages.debian.org/sid/netcat-openbsd](https://packages.debian.org/sid/netcat-openbsd) || [openbsd-netcat](https://www.archlinux.org/packages/?name=openbsd-netcat)

Una alternativa mas compleja es [socat](https://www.archlinux.org/packages/?name=socat).

## Whois

Véase también [Wikipedia:es:WHOIS](https://en.wikipedia.org/wiki/es:WHOIS "wikipedia:es:WHOIS").

*   **whois** — Cliente WHOIS inteligente.

	[https://github.com/rfc1036/whois](https://github.com/rfc1036/whois) || [whois](https://www.archlinux.org/packages/?name=whois)

*   **jwhois** — Un cliente de Internet Whois.

	[https://www.gnu.org/software/jwhois/](https://www.gnu.org/software/jwhois/) || [jwhois](https://aur.archlinux.org/packages/jwhois/)

## inetd

Arch Linux no tiene [inetd](https://en.wikipedia.org/wiki/es:inetd "wikipedia:es:inetd") pero en su lugar puedes utilizar [systemd](http://0pointer.de/blog/projects/inetd.html) o [xinetd](https://en.wikipedia.org/wiki/es:xinetd "wikipedia:es:xinetd") ([xinetd](https://www.archlinux.org/packages/?name=xinetd)).

## Véase también

*   [List of applications/Security (Español)#Seguridad de la red](/index.php/List_of_applications/Security_(Espa%C3%B1ol)#Seguridad_de_la_red "List of applications/Security (Español)")