**Estado de la traducción**
Este artículo es una traducción de [Sendmail](/index.php/Sendmail "Sendmail"), revisada por última vez el **2019-11-21**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Sendmail&diff=0&oldid=589655) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Sendmail](https://en.wikipedia.org/wiki/Sendmail "wikipedia:Sendmail") es el clásico [agente de transferencia de correo](/index.php/Mail_transfer_agent "Mail transfer agent") del mundo Unix. Este artículo se basa en [Mail server](/index.php/Mail_server "Mail server").

El objetivo de este artículo es configurar Sendmail para cuentas de usuarios locales, sin usar MySQL u otra base de datos, y también permitir la creación de *cuentas solo de correo* .

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Añadir usuarios](#Añadir_usuarios)
*   [3 Configuración](#Configuración)
    *   [3.1 Obtener certificado TLS](#Obtener_certificado_TLS)
    *   [3.2 sendmail.cf](#sendmail.cf)
    *   [3.3 local-host-names](#local-host-names)
    *   [3.4 access.db](#access.db)
    *   [3.5 aliases.db](#aliases.db)
    *   [3.6 virtusertable.db](#virtusertable.db)
    *   [3.7 Comenzar en el arranque](#Comenzar_en_el_arranque)
    *   [3.8 Autenticación SASL](#Autenticación_SASL)
*   [4 Consejos y trucos](#Consejos_y_trucos)
    *   [4.1 Reenviar todo el correo de un dominio a cierto usuario](#Reenviar_todo_el_correo_de_un_dominio_a_cierto_usuario)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") los paquetes [sendmail](https://aur.archlinux.org/packages/sendmail/), [procmail](https://www.archlinux.org/packages/?name=procmail) y [m4](https://www.archlinux.org/packages/?name=m4).

## Añadir usuarios

Cree un [usuario de Linux](/index.php/Users_and_groups_(Espa%C3%B1ol) "Users and groups (Español)") para cada usuario que desee recibir correo electrónico en *username@your-domain.com*. Para añadir *cuentas solo de correo*, es decir, usuarios que pueden recibir correos electrónicos, pero no pueden tener acceso de shell o iniciar sesión en X, puede agregarlos así:

```
# useradd -m -s /usr/bin/nologin *nombre-de-usuario*

```

## Configuración

### Obtener certificado TLS

**Advertencia:** si implementa [TLS](https://en.wikipedia.org/wiki/TLS "wikipedia:TLS"), asegúrese de seguir [guía de weakdh.org](https://weakdh.org/sysadmin.html) y [desactivar SSLv3](http://disablessl3.com/) para evitar vulnerabilidades. Para obtener más información, consulte [Server-side TLS](/index.php/Server-side_TLS "Server-side TLS").

Para obtener un certificado, consulte [OpenSSL#Usage](/index.php/OpenSSL#Usage "OpenSSL").

### sendmail.cf

Cree el archivo `/etc/mail/sendmail.mc`. Puede leer todas las opciones para configurar sendmail en el archivo `/usr/share/sendmail-cf/README`.

**Advertencia:** si crea su propio archivo sendmail.mc, recuerde que la autenticación de texto plano mediante **non-TLS** es muy arriesgada. Utilizar el siguiente ejemplo obliga a utilizar TLS y, por lo tanto, es más seguro, a menos que sepa lo que está haciendo.

He aquí hay un ejemplo usando «auth» mediante [TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security "wikipedia:Transport Layer Security"). El ejemplo tiene comentarios que explican cómo funciona. Los comentarios comienzan con `dnl` .

 `/etc/mail/sendmail.mc` 
```
include(`/usr/share/sendmail-cf/m4/cf.m4')
define(`confDOMAIN_NAME', `your-domain.com')dnl
FEATURE(use_cw_file)
dnl  Lo siguiente permite enviar si el usuario se autentica,
dnl  y no permite la autenticación de texto plano (PLAIN/LOGIN) mediante
dnl  enlaces non-TLS:
define(`confAUTH_OPTIONS', `A p y')dnl
dnl
dnl  Aceptar autenticaciones PLAIN y LOGIN:
TRUST_AUTH_MECH(`LOGIN PLAIN')dnl
define(`confAUTH_MECHANISMS', `LOGIN PLAIN')dnl
dnl
dnl Asegúrese de que estas rutas apuntan correctamente a sus archivos cert SSL:
define(`confCACERT_PATH',`/etc/ssl/certs')
define(`confCACERT',`/etc/ssl/cacert.pem')
define(`confSERVER_CERT',`/etc/ssl/certs/server.crt')
define(`confSERVER_KEY',`/etc/ssl/private/server.key')
dnl
FEATURE(`virtusertable', `hash /etc/mail/virtusertable.db')dnl
OSTYPE(linux)dnl
MAILER(local)dnl
MAILER(smtp)dnl

```

Luego procéselo con:

```
# m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf

```

### local-host-names

Coloque sus dominios en el archivo `local-host-names`:

 `/etc/mail/local-host-names` 
```
localhost
your-domain.com
mail.your-domain.com
localhost.localdomain

```

Asegúrese de que los dominios también sean resueltos por su archivo `/etc/hosts`.

### access.db

Cree el archivo `/etc/mail/access`y coloque allí las direcciones base donde desea poder enviar el correo. Supongamos que tiene una vpn en `10.5.0.0/24`, y desea enviar correos desde cualquier ip en ese rango:

 `/etc/mail/access` 
```
10.5.0 RELAY
127.0.0 RELAY

```

Luego procéselo con:

```
# makemap hash /etc/mail/access.db < /etc/mail/access

```

### aliases.db

Cree el archivo `/etc/mail/aliases`, descomente la línea `#root: human being here` y cámbielo para que sea así:

 `root:         your-username` 

Puede añadir alias para sus nombres de usuario allí, de esta forma:

```
coolguy:      your-username
somedude:     your-username
```

Luego procéselo con:

```
# newaliases

```

### virtusertable.db

Cree el archivo `virtusertable` y coloque alias que incluyan dominios (útil si su servidor aloja varios dominios):

 `/etc/mail/virtusertable` 
```
your-username@your-domain.com         your-username
joe@my-other.tk                       joenobody

```

Luego procéselo con:

```
# makemap hash /etc/mail/virtusertable.db < /etc/mail/virtusertable

```

### Comenzar en el arranque

Active e inicie los siguientes servicios. Lea [Daemons](/index.php/Daemons "Daemons") para obtener más detalles.

*   `saslauthd.service`
*   `sendmail.service`
*   `sm-client.service`

### Autenticación SASL

Añada un usuario a la base de datos SASL para la autenticación SMTP:

```
# saslpasswd2 -c your-username

```

## Consejos y trucos

### Reenviar todo el correo de un dominio a cierto usuario

Para reenviar todo el correo dirigido a cualquier usuario en el dominio **my-other.tk** a **your-username@your-domain.com**, añádalo al archivo `/etc/mail/virtusertable`:

 `@my-other.tk        your-username@your-domain.com` 

No olvide procesarlo nuevamente con:

```
# makemap hash /etc/mail/virtusertable.db < /etc/mail/virtusertable

```