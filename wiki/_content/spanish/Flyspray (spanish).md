**Estado de la traducción**
Este artículo es una traducción de [Flyspray](/index.php/Flyspray "Flyspray"), revisada por última vez el **2019-02-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Flyspray&diff=0&oldid=557661) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [LAMP](/index.php/LAMP "LAMP")

[Flyspray](http://www.flyspray.org/) es un sistema de seguimiento de errores escrito en [PHP](/index.php/PHP_(Espa%C3%B1ol) "PHP (Español)").

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [flyspray](https://www.archlinux.org/packages/?name=flyspray). Flyspray requiere un servidor web como [Apache HTTP Server](/index.php/Apache_HTTP_Server_(Espa%C3%B1ol) "Apache HTTP Server (Español)") con [PHP](/index.php/PHP_(Espa%C3%B1ol) "PHP (Español)"), y un servidor SQL como [MySQL](/index.php/MySQL_(Espa%C3%B1ol) "MySQL (Español)") o [PostgreSQL](/index.php/PostgreSQL "PostgreSQL").

### Configuración de Apache

**Nota:** Deberá tener [Apache](/index.php/Apache_HTTP_Server_(Espa%C3%B1ol) "Apache HTTP Server (Español)") configurado para ejecutarse con [PHP](/index.php/PHP_(Espa%C3%B1ol) "PHP (Español)"). Véase [Apache#PHP](/index.php/Apache#PHP "Apache") para obtener instrucciones. Asegúrese de descomentar `extension=mysqli` en `/etc/php/php.ini`.

Necesitará crear un archivo de configuración para que Apache encuentre su instalación de Flyspray. Cree el siguiente archivo:

 `/etc/httpd/conf/extra/flyspray.conf` 
```
Alias /flyspray "/usr/share/webapps/flyspray"
<Directory "/usr/share/webapps/flyspray">
	AllowOverride All
	Options FollowSymlinks
	Require all granted
	php_admin_value open_basedir "/srv/http/:/tmp/:/usr/share/webapps/flyspray"
</Directory>
```

Luego deberá editar `/etc/webapps/flyspray/.htaccess` y cambiar `deny from all` a `allow from all`. Ahora debería poder navegar a la interfaz de flyspray (por ejemplo, `[http://localhost/flyspray](http://localhost/flyspray)`) y mostrará una página de comprobaciones previas a la instalación. Cualquier problema aquí debe ser resuelto antes de continuar.