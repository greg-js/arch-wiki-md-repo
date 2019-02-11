**Status de tradução:** Esse artigo é uma tradução de [Network tools](/index.php/Network_tools "Network tools"). Data da última tradução: 2019-01-10\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Network_tools&diff=0&oldid=559049) na versão em inglês.

Artigos relacionados

*   [Telnet](/index.php/Telnet_(Portugu%C3%AAs) "Telnet (Português)")
*   [Nmap](/index.php/Nmap "Nmap")
*   [Wireshark](/index.php/Wireshark_(Portugu%C3%AAs) "Wireshark (Português)")

Essa página lista várias ferramentas de rede. *ping* e *ip* são cobertos por [Configuração de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede "Configuração de rede").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Traceroute](#Traceroute)
*   [2 Netcat](#Netcat)
*   [3 Whois](#Whois)
*   [4 inetd](#inetd)
*   [5 Veja também](#Veja_também)

## Traceroute

[Traceroute](https://en.wikipedia.org/wiki/pt:Traceroute "wikipedia:pt:Traceroute") é uma ferramenta para exibir o caminho dos pacotes através de uma rede IP.

Há várias implementações disponíveis:

*   [tracepath(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tracepath.8) do [iputils](https://www.archlinux.org/packages/?name=iputils) (parte do [base](https://www.archlinux.org/groups/x86_64/base/))
*   [traceroute(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/traceroute.8) do [traceroute](https://www.archlinux.org/packages/?name=traceroute)
*   **MTR** — Combina a funcionalidade do traceroute e do ping em uma ferramenta.

	[http://www.bitwizard.nl/mtr/](http://www.bitwizard.nl/mtr/) || [mtr](https://www.archlinux.org/packages/?name=mtr), [mtr-gtk](https://www.archlinux.org/packages/?name=mtr-gtk)

## Netcat

Veja também [Wikipedia:pt:Netcat](https://en.wikipedia.org/wiki/pt:Netcat "wikipedia:pt:Netcat").

*   **GNU Netcat** — Reescrita do netcat pelo GNU, o aplicativo de encadeamento de rede.

	[http://netcat.sourceforge.net/](http://netcat.sourceforge.net/) || [gnu-netcat](https://www.archlinux.org/packages/?name=gnu-netcat)

*   **openbsd-netcat** — Canivete suíço de TCP/IP. Variante OpenBSD.

	[https://packages.debian.org/sid/netcat-openbsd](https://packages.debian.org/sid/netcat-openbsd) || [openbsd-netcat](https://www.archlinux.org/packages/?name=openbsd-netcat)

*   **libressl-netcat** — Ferramenta de conexão UDP/TCP de baixo nível com suporte a protocolo TLS.

	[https://www.libressl.org](https://www.libressl.org) || [libressl-netcat](https://aur.archlinux.org/packages/libressl-netcat/)

Uma alternativa mais complexa é o [socat](https://www.archlinux.org/packages/?name=socat).

## Whois

Veja também [Wikipedia:pt:WHOIS](https://en.wikipedia.org/wiki/pt:WHOIS "wikipedia:pt:WHOIS").

*   **whois** — Cliente inteligente de WHOIS.

	[https://github.com/rfc1036/whois](https://github.com/rfc1036/whois) || [whois](https://www.archlinux.org/packages/?name=whois)

*   **jwhois** — Um cliente de Internet para Whois

	[https://www.gnu.org/software/jwhois/](https://www.gnu.org/software/jwhois/) || [jwhois](https://aur.archlinux.org/packages/jwhois/)

## inetd

Arch Linux não tem o [inetd](https://en.wikipedia.org/wiki/inetd "wikipedia:inetd"), mas você pode user [systemd](http://0pointer.de/blog/projects/inetd.html) ou [xinetd](https://en.wikipedia.org/wiki/pt:xinetd "wikipedia:pt:xinetd") ([xinetd](https://www.archlinux.org/packages/?name=xinetd)).

## Veja também

*   [List of applications/Security#Network security](/index.php/List_of_applications/Security#Network_security "List of applications/Security")