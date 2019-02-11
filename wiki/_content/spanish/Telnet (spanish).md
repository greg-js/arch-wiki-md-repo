**Estado de la traducción**
Este artículo es una traducción de [Telnet](/index.php/Telnet "Telnet"), revisada por última vez el **2019-02-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Telnet&diff=0&oldid=562857) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Telnet](https://en.wikipedia.org/wiki/es:Telnet o tunelizada a través de una VPN. Para una alternativa segura véase [SSH](/index.php/SSH_(Espa%C3%B1ol) "SSH (Español)").

## Instalación

El paquete [inetutils](https://www.archlinux.org/packages/?name=inetutils), parte del [grupo base](/index.php/Base_group_(Espa%C3%B1ol) "Base group (Español)"), incluye un cliente telnet.

Un servidor telnet puede configurarse con sockets de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") o xinetd. Telnetd via systemd requiere solo el paquete inetutils. Para configurar un servidor telnet con xinetd, instale también [xinetd](https://www.archlinux.org/packages/?name=xinetd).

## Configuración

Para habilitar las conexiones del servidor telnet en systemd, [habilite](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") `telnet.socket` (si desea que el servidor telnet arranque en cada inicio), e [inicie](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") `telnet.socket` para probar la conectividad.

Para habilitar las conexiones del servidor telnet en xinetd, edite `/etc/xinetd.d/telnet`, cambie `disable = yes` a `disable = no` y reinicie el servicio xinetd.

[Habilite](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") systemd xinetd service si desea iniciarlo en el momento del arranque.

### Probando la configuración

Intente abrir una conexión telnet a su servidor:

```
$ telnet localhost

```

Intente un inicio de sesión root para ver si su configuración lo permite y las implicaciones de seguridad que eso conlleva.

Si la sesión se desconecta antes de recibir un mensaje de inicio de sesión, intente instalar [inetutils-git](https://aur.archlinux.org/packages/inetutils-git/) en lugar del inetutils actual y reinicie telnet.socket.

**Sugerencia:** Si recibe código no deseado de un servidor telnet remoto que envía caracteres que no son ascii con una codificación que no es unicode, es posible que desee instalar [xorg-luit](https://www.archlinux.org/packages/?name=xorg-luit) para resolver este problema.