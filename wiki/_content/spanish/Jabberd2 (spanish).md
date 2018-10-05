**Estado de la traducción**
Este artículo es una traducción de [Jabberd2](/index.php/Jabberd2 "Jabberd2"), revisada por última vez el **2018-10-05**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Jabberd2&diff=0&oldid=484065) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[jabberd2](http://jabberd2.org/) es un servidor [XMPP](https://en.wikipedia.org/wiki/XMPP "wikipedia:XMPP"), escrito en lenguaje C y con licencia de software libre bajo la Licencia Pública General de GNU. Fue inspirado por jabberd14.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 Demonio](#Demonio)
*   [3 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

[Instale](/index.php/Install "Install") el paquete [jabberd2](https://aur.archlinux.org/packages/jabberd2/).

## Configuración

Edite `/etc/jabberd/c2s.xml` y cambie el contenido de la etiqueta `<id register-enable='mu'>` a su dominio.

Esa es la línea que se agregará a la identificación de sus usuarios. (Si coloca `example.com` allí, su ID de usuario será algo así como `user@example.com`). Si se va a tener acceso al servicio jabber a través de Internet abierto (en lugar de una VPN o LAN), entonces ese nombre **DEBERÍA** ser resuelto por el DNS a su servidor.

La parte `register-enable='mu'`, permite el registro de cuentas, utilizando un cliente jabber estándar.

También configure su servidor en `sm.xml`:

 `/etc/jabberd/sm.xml` 
```
<id>mymachine.com</id>

```

### Demonio

Configure el servicio `jabberd.service` para iniciar al arranque.

Lea [Daemons (Español)](/index.php/Daemons_(Espa%C3%B1ol) "Daemons (Español)") para más información.

## Véase también

*   [página de inicio de Jabberd2](http://jabberd2.org/)