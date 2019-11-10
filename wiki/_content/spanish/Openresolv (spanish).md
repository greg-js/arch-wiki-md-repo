Artículos relacionados

*   [systemd-resolvconf](/index.php/Systemd-resolvconf "Systemd-resolvconf")

**Estado de la traducción**
Este artículo es una traducción de [openresolv](/index.php/Openresolv "Openresolv"), revisada por última vez el **2019-11-06**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Openresolv&diff=0&oldid=588023) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Openresolv](https://roy.marples.name/projects/openresolv) es una implementación de [resolvconf](https://en.wikipedia.org/wiki/resolvconf "wikipedia:resolvconf"), es decir, un marco de trabajo de gestión de [resolv.conf](/index.php/Resolv.conf "Resolv.conf").

Aunque openresolv es más conocido por permitir que múltiples aplicaciones modifiquen `/etc/resolv.conf`, actualmente es la única forma estándar de implementar:

*   control dinámico de una resolución de DNS (que no sea glibc);
*   [reenvío condicional](/index.php/Resolv.conf#Conditional_forwarding "Resolv.conf") dinámico.

**Sugerencia:** una implementación alternativa es [systemd-resolvconf](/index.php/Systemd-resolvconf "Systemd-resolvconf"), pero solo se puede usar con [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Utilización](#Utilización)
*   [3 Usuarios](#Usuarios)
*   [4 Suscriptores](#Suscriptores)
*   [5 Consejos y trucos](#Consejos_y_trucos)
    *   [5.1 Definir múltiples valores para las opciones](#Definir_múltiples_valores_para_las_opciones)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [openresolv](https://www.archlinux.org/packages/?name=openresolv).

## Utilización

Openresolv proporciona [resolvconf(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolvconf.8) y está configurado en `/etc/resolvconf.conf`. Consulte [resolvconf.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolvconf.conf.5) para ver las opciones admitidas.

La ejecución de `resolvconf -u` generará `/etc/resolv.conf`.

## Usuarios

Clientes [DHCP](/index.php/DHCP "DHCP"):

*   [dhcpcd](/index.php/Dhcpcd "Dhcpcd") tiene un hook que utiliza *resolvconf* si está instalado.
*   [iwd#Enable built-in network configuration](/index.php/Iwd#Enable_built-in_network_configuration "Iwd")

[Gestores de red](/index.php/Network_manager "Network manager"):

*   [netctl](/index.php/Netctl "Netctl") (utilizado por defecto).
*   [NetworkManager#Use openresolv](/index.php/NetworkManager#Use_openresolv "NetworkManager") (limitado a una única interfaz).

Clientes [VPN](/index.php/VPN "VPN"):

*   [OpenConnect](/index.php/OpenConnect "OpenConnect")
*   [OpenVPN#DNS](/index.php/OpenVPN#DNS "OpenVPN")
*   [strongSwan](/index.php/StrongSwan "StrongSwan")
*   [WireGuard](/index.php/WireGuard "WireGuard")

## Suscriptores

Openresolv se puede configurar para pasar servidores de nombres y buscar dominios a resolvedores de DNS. Los resolvedores compatibles son:

*   [BIND](/index.php/BIND "BIND")
*   [dnsmasq#openresolv](/index.php/Dnsmasq#openresolv "Dnsmasq")
*   [pdnsd](/index.php/Pdnsd "Pdnsd")
*   [powerdns-recursor](https://www.archlinux.org/packages/?name=powerdns-recursor)
*   [Unbound](/index.php/Unbound "Unbound")

Consulte la [documentación oficial](https://roy.marples.name/projects/openresolv/config) para obtener instrucciones.

## Consejos y trucos

### Definir múltiples valores para las opciones

La página de manual no lo menciona, pero para definir varios valores, para las opciones que lo admiten (por ejemplo, `name_servers`, `resolv_conf_options` etc.) en `/etc/resolvconf.conf`, debe escribirlos separados por espacios entre comillas. Por ejemplo:

 `/etc/resolvconf.conf` 
```
resolv_conf_options="edns0 single-request"
name_servers="192.168.35.1 fd7b:d0bd:7a6e::1"
```