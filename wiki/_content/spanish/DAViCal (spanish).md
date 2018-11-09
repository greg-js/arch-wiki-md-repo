Artículos relacionados

*   [AgenDAV](/index.php/AgenDAV "AgenDAV")
*   [Radicale](/index.php/Radicale "Radicale")

[DAViCal](https://www.davical.org/) es un servidor que implementa los protocolos CalDAV y CardDAV. Es solamente un servidor, con una mínima interacción directa del usuario, basándose en su lugar en el uso de clientes CalDav, como iCal.app de Apple, iOS (iPhone, iPad, iPod), Thunderbird con Sunbird o Evolution.

## Instalación

### Requisitos previos a la instalación

DAViCal está escrito en [PHP](/index.php/PHP_(Espa%C3%B1ol) "PHP (Español)") y utiliza la base de datos [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") como soporte para almacenar la información del calendario. Actualmente solo es compatible con PostgreSQL, pero se está trabajando para que también admita otras bases de datos.

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [davical](https://aur.archlinux.org/packages/davical/), [postgresql](https://www.archlinux.org/packages/?name=postgresql), [php](https://www.archlinux.org/packages/?name=php), y [php-pgsql](https://www.archlinux.org/packages/?name=php-pgsql).

Los directorios de instalación están definidos por las [Pautas de empaquetado de aplicaciones web](/index.php/Web_application_package_guidelines "Web application package guidelines") y son ligeramente diferentes a la documentación anterior (`/usr/share/webapps/davical` y `/etc/webapps/davical`) .

DAViCal es una aplicación web y, por lo tanto, también necesita una configuración de servidor web. Aquí se dará por sentado [Nginx](/index.php/Nginx "Nginx"), pero DAViCal puede ejecutarse en casi cualquier servidor web (algunos pueden dejar de procesar solicitudes cuando ven los encabezados HTTP de CalDAV, y por lo tanto, DAViCal no podrá verlos).

### Preparando PostgreSQL

En primer lugar, debe configurar PostgreSQL para que pueda iniciarse siguiendo las pautas descritas en [PostgreSQL#Instalación](/index.php/PostgreSQL#Installation "PostgreSQL").

DAViCal requiere que se configuren dos cuentas independientes, una para acceder a la base de datos desde la aplicación web, que tendrá un poder limitado, y otra que se usará para administrar las tablas relacionadas con DAViCal.

Para hacerlo, deberá editar `/var/lib/postgres/data/pg_hba.conf`:

Añada las siguientes líneas:

```
   local   davical         davical_app                             trust
   local   davical         davical_dba                             trust

```

Asegúrese de tener un rol 'root' en su base de datos. Si no lo tiene, créelo convirtiéndose en el usuario postgres como se describe en la página de [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") y ejecute lo siguiente:

```
$ createuser -s -U postgres --interactive
$ Enter name of role to add: root

```

Prepare la base de datos ejecutando el script create-database.sh como root:

```
# /usr/share/webapps/davical/dba/create-database.sh

```

Luego ejecute createdb como root:

```
# createdb

```

Si su servidor PostgreSQL está en un host remoto, use [DAViCal PostgreSQL_Config](https://wiki.davical.org/index.php/PostgreSQL_Config) en lugar de las instrucciones anteriores.