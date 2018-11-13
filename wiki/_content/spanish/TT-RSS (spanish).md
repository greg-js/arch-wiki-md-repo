**Estado de la traducción**
Este artículo es una traducción de [TT-RSS](/index.php/TT-RSS "TT-RSS"), revisada por última vez el **2018-10-05**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=TT-RSS&diff=0&oldid=543832) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Tiny Tiny RSS](https://tt-rss.org/) es un agregador de fuentes de noticias (RSS/Atom) de código abierto basado en web, diseñado para permitirle leer noticias desde cualquier ubicación, de tal modo que le parecerá estar utilizando lo más parecido a la aplicación de un escritorio real.

## Contents

*   [1 Instalación](#Instalación)
    *   [1.1 Configurar PHP y base de datos](#Configurar_PHP_y_base_de_datos)
    *   [1.2 Hook de pacman](#Hook_de_pacman)
    *   [1.3 Configurar un demonio de actualización](#Configurar_un_demonio_de_actualización)

## Instalación

Instale [tt-rss](https://www.archlinux.org/packages/?name=tt-rss) desde los [repositorios oficiales](/index.php/Official_repositories "Official repositories").

Si planea usar PostgreSQL, instale [php-pgsql](https://www.archlinux.org/packages/?name=php-pgsql)

tt-rss se instala en `/usr/share/webapps/tt-rss/`. Tendrá que hacer que este directorio esté disponible desde su servidor web. La forma más sencilla de hacer es:

*   Con [Servidor HTTP Apache](/index.php/Apache_HTTP_Server "Apache HTTP Server"):

	 `# ln -s /usr/share/webapps/tt-rss /srv/http/tt-rss` 

*   Con [Nginx](/index.php/Nginx "Nginx"):

	 `# ln -s /usr/share/webapps/tt-rss /usr/share/nginx/html/tt-rss` 

### Configurar PHP y base de datos

Deberá configurar una base de datos, ya sea [MySQL](/index.php/MySQL "MySQL") o [PostgreSQL](/index.php/PostgreSQL "PostgreSQL").

Cree un usuario y una base de datos, por ejemplo. con mysql:

```
$ mysql -p -u root
mysql> CREATE USER 'ttrss'@'localhost' IDENTIFIED BY 'somepassword';
mysql> CREATE DATABASE ttrss;
mysql> GRANT ALL PRIVILEGES ON ttrss.* TO "ttrss"@"localhost" IDENTIFIED BY 'somepassword';

```

O cree un usuario y una base de datos en PostgreSQL, por ejemplo:

```
[postgres]$ createuser -P --interactive
[postgres]$ createdb -U ttrss ttrss

```

En `/etc/php/php.ini`, active los siguientes módulos:

```
extension=curl
extension=iconv
extension=mysqli # for MySQL
extension=pdo_mysql # for MySQL
extension=pdo_pgsql # for PostgreSQL
extension=pgsql # for legacy PostgreSQL plugins
extension=soap

```

*Si* `open_basedir` está configurado en `/etc/php/php.ini` (no está predeterminado), añada `/var/lib/tt-rss` para él.

La inicialización de la aplicación se puede hacer de forma automática o manual.

De forma automática:

*   elimine el archivo de configuración predeterminado `/etc/php/php.ini`, sin este archivo la aplicación web tt-rss ingresa al asistente de instalación;
*   navegue a (sus-servidores-raíz)/tt-rss/ y continúe con el instalador;
*   guarde el archivo de configuración generado en `/etc/webapps/tt-rss/config.php`.

De forma manual:

*   edite el archivo de configuración tt-rss `/etc/webapps/tt-rss/config.php` y actualice la configuración de la base de datos.
*   vuelva a crear la base de datos desde `/usr/share/webapps/tt-rss/schema/ttrss_schema_TYPE.sql`. Con MySQL funcionando:

```
$ mysql --user ttrss --password=<PASSWORD> ttrss < /usr/share/webapps/tt-rss/schema/ttrss_schema_mysql.sql

```

Con PostgreSQL ejecutea:

```
$ psql ttrss -U ttrss -f /usr/share/webapps/tt-rss/schema/ttrss_schema_pgsql.sql

```

### Hook de pacman

Para realizar las actualizaciones de la base de datos tt-rss automáticamente, puede configurar el hook de actualización de pacman basándose en el siguiente ejemplo:

```
[Trigger]
Operation = Install
Operation = Upgrade
Type = Package
Target = tt-rss

[Action]
Description = Updating TT-RSS Database
When = PostTransaction
Exec = /usr/bin/runuser -u http -- /usr/bin/php /usr/share/webapps/tt-rss/update.php --update-schema

```

Debe colocarlo en /etc/pacman.d/hooks/tt-rss.hook si no personalizó HookDir en pacman.conf.

Véase también [Pacman#Hooks](/index.php/Pacman#Hooks "Pacman")

### Configurar un demonio de actualización

Consulte [https://tt-rss.org/gitlab/fox/tt-rss/wikis/UpdatingFeeds](https://tt-rss.org/gitlab/fox/tt-rss/wikis/UpdatingFeeds), pero debería poder hacerse simplemente con:

```
# systemctl enable tt-rss

```

Lance

```
$ systemctl status tt-rss

```

para comprobar que está funcionando bien.