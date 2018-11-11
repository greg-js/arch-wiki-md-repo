**Estado de la traducción**
Este artículo es una traducción de [AgenDAV](/index.php/AgenDAV "AgenDAV"), revisada por última vez el **2018-11-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=AgenDAV&diff=0&oldid=548452) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [DAViCal](/index.php/DAViCal_(Espa%C3%B1ol) "DAViCal (Español)")
*   [Kcaldav](/index.php/Kcaldav_(Espa%C3%B1ol) "Kcaldav (Español)")
*   [Radicale](/index.php/Radicale "Radicale")

[AgenDAV](http://agendav.org/) es una aplicación web CalDAV multilenguaje de código abierto, escrita en PHP, que cuenta con una completa interfaz AJAX con soporte para calendarios compartidos.

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [agendav](https://aur.archlinux.org/packages/agendav/).

### Base de datos

Debe proporcionar una base de datos SQL a AgenDAV. Aquí hay un ejemplo con PostgreSQL.

Instale [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") según el artículo. Cree un usuario y una base de datos de `agendav`:

```
# createuser agendav
# createdb -O agendav agendav

```

### Configuración

Cuando la base de datos esté configurada, debe rellenarla manualmente:

```
# psql -U agendav agendav < /usr/share/webapps/agendav/sql/pgsql.schema.sql
# bash /usr/share/webapps/agendav/bin/agendavcli dbupdate

```

Asegúrese de habilitar las extensiones `extension=pgsql` (o la base de datos que haya utilizado) y `extension=iconv` en `php.ini`.

Modifique los archivos de configuración `/etc/webapps/agendav/{config,caldav,database}.php` a su gusto.

Sirva la aplicación a través de apache `/etc/webapps/agendav/apache.example.conf`, nginx/php-fpm `/etc/webapps/agendav/nginx.example.conf` u otro servidor web.