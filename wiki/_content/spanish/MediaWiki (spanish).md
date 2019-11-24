**Estado de la traducción**
Este artículo es una traducción de [MediaWiki](/index.php/MediaWiki "MediaWiki"), revisada por última vez el **2019-11-23**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=MediaWiki&diff=0&oldid=589866) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

**Nota:** MediaWiki no es totalmente compatible con PHP 7.3 todavía.[[1]](https://www.mediawiki.org/wiki/Compatibility#PHP)[[2]](https://phabricator.wikimedia.org/project/view/3494/).

[MediaWiki](https://www.mediawiki.org/wiki/MediaWiki) es un software wiki gratuito y de código abierto escrito en [PHP](/index.php/PHP "PHP"), desarrollado originalmente para Wikipedia. También alimenta esta wiki (vea [Special:Version](/index.php/Special:Version "Special:Version") y el [repositorio de GitHub](https://github.com/archlinux/archwiki)).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 PHP](#PHP)
    *   [2.2 Servidor web](#Servidor_web)
        *   [2.2.1 Apache](#Apache)
        *   [2.2.2 Nginx](#Nginx)
        *   [2.2.3 Lighttpd](#Lighttpd)
    *   [2.3 Base de datos](#Base_de_datos)
    *   [2.4 LocalSettings.php](#LocalSettings.php)
*   [3 Consejos y trucos](#Consejos_y_trucos)
    *   [3.1 Matemáticas (texvc)](#Matemáticas_(texvc))
    *   [3.2 Unicode](#Unicode)
    *   [3.3 VisualEditor](#VisualEditor)

## Instalación

Para ejecutar MediaWiki necesitará tres cosas:

*   el paquete [mediawiki](https://www.archlinux.org/packages/?name=mediawiki), que llama a [PHP](/index.php/PHP "PHP");
*   un servidor web: [Apache](/index.php/Apache "Apache"), [Nginx](/index.php/Nginx "Nginx") o [Lighttpd](/index.php/Lighttpd "Lighttpd");
*   un sistema de base de datos: [MySQL](/index.php/MySQL "MySQL"), [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") o [SQLite](/index.php/SQLite "SQLite").

Para instalar MediaWiki en [XAMPP](/index.php/XAMPP "XAMPP"), vea [mw:Manual:Installing MediaWiki on XAMPP](https://www.mediawiki.org/wiki/Manual:Installing_MediaWiki_on_XAMPP "mw:Manual:Installing MediaWiki on XAMPP")

## Configuración

Los pasos para lograr una configuración de MediaWiki que funcione, implican editar la configuración de PHP y agregar los fragmentos de configuración de MediaWiki.

### PHP

MediaWiki requiere la extensión `iconv`, por lo que debe descomentar `extension=iconv` en `/etc/php/php.ini`.

Dependencias opcionales:

*   Para renderizar imágenes en miniatura, instale [ImageMagick](/index.php/ImageMagick "ImageMagick") o [php-gd](https://www.archlinux.org/packages/?name=php-gd). Si elige este último, también debe descomentar `extension=gd`.
*   Para obtener una más eficiente [normalización Unicode](https://www.mediawiki.org/wiki/Unicode_normalization_considerations "mw:Unicode normalization considerations"), instale [php-intl](https://www.archlinux.org/packages/?name=php-intl) y descomente `extension=intl`.

Active la API para su [DBMS](https://en.wikipedia.org/wiki/es:sistemas_gestores_de_bases_de_datos "wikipedia:es:sistemas gestores de bases de datos") (del inglés Database Management System),:

*   Si utiliza [MariaDB](/index.php/MariaDB "MariaDB"), descomente `extension=mysqli`.
*   Si utiliza [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), instale [php-pgsql](https://www.archlinux.org/packages/?name=php-pgsql) y descomente `extension=pgsql`.
*   Si utiliza [SQLite](/index.php/SQLite "SQLite"), instale [php-sqlite](https://www.archlinux.org/packages/?name=php-sqlite) y descomente `extension=pdo_sqlite`.

En segundo lugar, modifique el manejo de la sesión o puede que obtenga un error grave (`PHP Fatal error: session_start(): Failed to initialize storage module[...]`) al encontrar la ruta `session.save_path`. Una buena opción puede ser `/var/lib/php/sessions` o `/tmp/`.

 `/etc/php/php.ini`  `session.save_path = "/var/lib/php/sessions"` 

Deberá crear el directorio si no existe y luego restringir sus permisos:

```
# mkdir -p /var/lib/php/sessions/
# chown http:http /var/lib/php/sessions
# chmod go-rwx /var/lib/php/sessions

```

Si utiliza [open_basedir PHP](/index.php/PHP#Configuration "PHP") y desea [permitir subir archivos](https://www.mediawiki.org/wiki/Manual:Configuring_file_uploads "mw:Manual:Configuring file uploads"), debe incluir `/var/lib/mediawiki/` (enlaces simbólicos de `images/` de [mediawiki](https://www.archlinux.org/packages/?name=mediawiki) a `/var/lib/mediawiki/`).

### Servidor web

#### Apache

Siga [Apache HTTP Server#PHP](/index.php/Apache_HTTP_Server#PHP "Apache HTTP Server").

Copie `/etc/webapps/mediawiki/apache.example.conf` a `/etc/httpd/conf/extra/mediawiki.conf` y edítelo conforme a sus necesidades.

Añada la siguiente línea a `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/mediawiki.conf

```

[Reinicie](/index.php/Restart_(Espa%C3%B1ol) "Restart (Español)") el demonio `httpd.service`.

**Nota:** el archivo predeterminado de `/etc/webapps/mediawiki/apache.example.conf` sobrescribirá la configuración open_basedir de PHP, posiblemente en conflicto con otras páginas. Este comportamiento se puede cambiar moviendo la línea que comienza con `php_admin_value` entre las etiquetas `<Directory>`. Además, si está ejecutando múltiples aplicaciones que dependen del mismo servidor, este valor también podría agregarse al valor de open_basedir en `/etc/php/php.ini` en lugar de `/etc/httpd/conf/extra/mediawiki.conf`

#### Nginx

Para que MediaWiki funcione con [Nginx](/index.php/Nginx "Nginx"), cree el siguiente archivo:

 `/etc/nginx/mediawiki.conf` 
```
location / {
   index index.php;
   try_files $uri $uri/ @mediawiki;
}
location @mediawiki {
   rewrite ^/(.*)$ /index.php;
}
location ~ \.php5?$ {
   include /etc/nginx/fastcgi_params;
   fastcgi_pass unix:/var/run/php-fpm/php-fpm.sock;
   fastcgi_index index.php5;
   fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
   try_files $uri @mediawiki;
}
location ~* \.(js|css|png|jpg|jpeg|gif|ico)$ {
   try_files $uri /index.php;
   expires max;
   log_not_found off;
}
# Restrictions based on the .htaccess files
location ^~ ^/(cache|includes|maintenance|languages|serialized|tests|images/deleted)/ {
   deny all;
}
location ^~ ^/(bin|docs|extensions|includes|maintenance|mw-config|resources|serialized|tests)/ {
   internal;
}
location ^~ /images/ {
   try_files $uri /index.php;
}
location ~ /\. {
   access_log off;
   log_not_found off; 
   deny all;
}

```

Asegúrese de que [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) esté instalado e [iniciado](/index.php/Start_(Espa%C3%B1ol) "Start (Español)").

Incluya una directiva de servidor, similar a esta:

 `/etc/nginx/nginx.conf` 
```
server {
  listen 80;
  server_name mediawiki;
  root /usr/share/webapps/mediawiki;
  index index.php;
  charset utf-8;
# For correct file uploads
  client_max_body_size    100m; # Equal or more than upload_max_filesize in /etc/php/php.ini
  client_body_timeout     60;
  include mediawiki.conf;

}

```

Por último, [reinicie](/index.php/Restart_(Espa%C3%B1ol) "Restart (Español)") los demonios `nginx.service` y `php-fpm.service`.

#### Lighttpd

Debería tener [Lighttpd](/index.php/Lighttpd "Lighttpd") instalado y configurado. Se requiere «mod_alias» y «mod_rewrite» en la matriz server.modules de lighttpd. Agregue al archivo de configuración lighttpd las siguientes líneas:

 `/etc/lighttpd/lighttpd.conf` 
```
alias.url += ("/mediawiki" => "/usr/share/webapps/mediawiki/")
url.rewrite-once += (
                "^/mediawiki/wiki/upload/(.+)" => "/mediawiki/wiki/upload/$1",
                "^/mediawiki/wiki/$" => "/mediawiki/index.php",
                "^/mediawiki/wiki/([^?]*)(?:\?(.*))?" => "/mediawiki/index.php?title=$1&$2"
)

```

[Reinicie](/index.php/Restart_(Espa%C3%B1ol) "Restart (Español)") el demonio `lighttpd.service`.

### Base de datos

Configure un servidor de base de datos como se explica en el artículo de su DBMS: [MySQL](/index.php/MySQL "MySQL"), [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") o [SQLite](/index.php/SQLite "SQLite").

MediaWiki puede crear automáticamente la base de datos, si proporciona la contraseña root de la base de datos, durante el [siguiente paso](#LocalSettings.php). De lo contrario, la base de datos debe crearse manualmente, consulte las [instrucciones de upstream](https://www.mediawiki.org/wiki/Manual:Installing_MediaWiki#Create_a_database "mw:Manual:Installing MediaWiki").

### LocalSettings.php

Abra la URL de la wiki (generalmente `http://*your_server*/mediawiki/`) en un navegador y realice la configuración inicial. Siga las [instrucciones de upstream](https://www.mediawiki.org/wiki/Manual:Config_script "mw:Manual:Config script").

El archivo generado `LocalSettings.php`, ofrecido para su descargar, guárdelo en `/usr/share/webapps/mediawiki/LocalSettings.php`. Este archivo define la configuración específica de su wiki. Cada vez que actualiza el paquete [mediawiki](https://www.archlinux.org/packages/?name=mediawiki), no se reemplaza.

## Consejos y trucos

### Matemáticas (texvc)

Por lo general, instalar [texvc](https://www.archlinux.org/packages/?name=texvc) y activarlo en la configuración es suficiente:

```
$wgUseTeX = true;

```

Si tiene problemas, intente aumentar los límites para las órdenes del intérprete de órdenes:

```
$wgMaxShellMemory = 8000000;
$wgMaxShellFileSize = 1000000;
$wgMaxShellTime = 300;
```

### Unicode

Verifique que php, apache y mysql usan UTF-8\. De lo contrario, puede enfrentarse a errores extraños debido a la falta de coincidencia de codificación.

### VisualEditor

La extensión [VisualEditor](https://en.wikipedia.org/wiki/es:Wikipedia:Editor_Visual "wikipedia:es:Wikipedia:Editor Visual") de MediaWiki proporciona un editor de texto enriquecido para MediaWiki. Siga [mw:Extension:VisualEditor](https://www.mediawiki.org/wiki/Extension:VisualEditor "mw:Extension:VisualEditor") para instalarlo.

También necesitará el backend Node.js de [Parsoid](https://www.mediawiki.org/wiki/Parsoid "mw:Parsoid"), que está disponible en [parsoid-git](https://aur.archlinux.org/packages/parsoid-git/).

Ajuste la ruta a MediaWiki en `/usr/share/webapps/parsoid/api/localsettings.js`:

```
parsoidConfig.setInterwiki( 'localhost', 'http://localhost/mediawiki/api.php' );

```

Después [active](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") e inicie `parsoid.service`.

Alternativamente, también se puede usar el paquete [parsoid](https://aur.archlinux.org/packages/parsoid/) y configurar el servicio a través del archivo yaml, donde las siguientes líneas deben estar presentes:

 `/usr/share/webapps/parsoid/config.yaml` 
```
uri: `'http://localhost/mediawiki/api.php'`
domain: 'localhost'

```

La parte correspondiente en la configuración de mediawiki:

 `/usr/share/webapps/mediawiki/LocalSettings.php` 
```
$wgVirtualRestConfig['modules']['parsoid'] = array(
  // URL to the Parsoid instance - use port 8142 if you use the Debian package - the parameter 'URL' was first used but is now deprecated (string)
  'url' => 'http://localhost:8000/',
  // Parsoid "domain" (string, optional) - MediaWiki >= 1.26
  'domain' => 'localhost',
  // Parsoid "prefix" (string, optional) - deprecated since MediaWiki 1.26, use 'domain'
  'prefix' => 'localhost',
  // Forward cookies in the case of private wikis (string or false, optional)
  'forwardCookies' => false,
  // request timeout in seconds (integer or null, optional)
  'timeout' => null,
  // Parsoid HTTP proxy (string or null, optional)
  'HTTPProxy' => null,
  // whether to parse URL as if they were meant for RESTBase (boolean or null, optional)
  'restbaseCompat' => null,
);

```

Después de la configuración, el servicio `parsoid` puede iniciarse (reiniciarse) y (si aún no lo ha hecho) activarse.