[Telnet](https://en.wikipedia.org/wiki/es:Telnet "wikipedia:es:Telnet") es el protocolo tradicional para hacer conexiones de consola remotas con TCP. Telnet **no es seguro** y se usa mas que todo para conectar equipos antiguos. Para una alternativa segura vea [SSH](/index.php/Secure_Shell_(Espa%C3%B1ol) "Secure Shell (Español)").

## Instalación

Para usar el cliente de telnet para conectar a otras maquinas [instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [inetutils](https://www.archlinux.org/packages/?name=inetutils), disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

Un servidor de telnet puede ser configurado con sockets de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") o xinetd.

telnetd con systemd solo requiere el paquete [inetutils](https://www.archlinux.org/packages/?name=inetutils), mientras que la configuracion de un servidor de telnet con xinetd requiere la instalacion de [xinetd](https://www.archlinux.org/packages/?name=xinetd).

## Configuración

Para habilitar un servidor de telnet con systemd, [active inicio automático](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)") en la unidad `telnet.socket`. Si el servidor de telnet se debe activar en cada inicio del sistema, o [active](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)") la unidad `telnet.socket` para comprobar conectividad.

Para habilitar unn servidor de telnet con xinetd, edite `/etc/xinetd.d/telnet`, cambie`disable = yes` por `disable = no` y [reinicie](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)") el servicio de `xinetd.service`.

[Active inicio automático](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)") del servicio `xinetd.service` si desea iniciarlo con el sistema.

### Comprobando el sistema

Intente abrir una conexión con su servidor:

```
$ telnet localhost

```

Intente iniciar sesión como root para comprobar si la configuración lo permite y las implicaciones de seguridad que esto conlleva.

Si la sesión se desconecta antes de abrir una consola, intente instalar [inetutils-git](https://aur.archlinux.org/packages/inetutils-git/) en lugar de [inetutils](https://www.archlinux.org/packages/?name=inetutils) y reinicie `telnet.socket`.

**Sugerencia:** Si se reciben caracteres no legibles en la consola en la conexión con un servidor remoto que envía no-ascii y no-unicode, intente instalar [xorg-luit](https://www.archlinux.org/packages/?name=xorg-luit) para solucionar este problema.