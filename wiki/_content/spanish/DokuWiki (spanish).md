**Estado de la traducción**
Este artículo es una traducción de [DokuWiki](/index.php/DokuWiki "DokuWiki"), revisada por última vez el **2019-11-24**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=DokuWiki&diff=0&oldid=582473) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

«[DokuWiki](https://www.dokuwiki.org/dokuwiki#) es un wiki que cumple con los estándares, simple de usar y que permite a los usuarios crear ricos repositorios de documentación. Proporciona un entorno para que personas, equipos y empresas creen y colaboren utilizando una sintaxis sencilla pero potente que garantiza que los archivos de datos permanezcan estructurados y legibles fuera de la wiki».

«Las revisiones ilimitadas de cada página permiten la restauración de cualquier versión anterior de dichas páginas, y con los datos almacenados en archivos de texto plano, no se requiere ninguna base de datos. Una poderosa arquitectura de complementos permite la extensión y la mejora del sistema central. Vea la sección de características para obtener una descripción completa de lo que DokuWiki puede ofrecer.» [[1]](http://wiki.splitbrain.org/wiki:dokuwiki)

En otras palabras, DokuWiki es una Wiki escrita en PHP y que no requiere base de datos.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Notas iniciales](#Notas_iniciales)
*   [2 Instalación](#Instalación)
*   [3 Configuración](#Configuración)
    *   [3.1 Apache](#Apache)
    *   [3.2 lighttpd](#lighttpd)
    *   [3.3 nginx](#nginx)
    *   [3.4 Activar la carga y visualización de archivos SVG](#Activar_la_carga_y_visualización_de_archivos_SVG)
*   [4 Posinstalación](#Posinstalación)
    *   [4.1 Limpiar](#Limpiar)
    *   [4.2 Instalar complementos](#Instalar_complementos)
    *   [4.3 Realizar copias de seguridad](#Realizar_copias_de_seguridad)
*   [5 Lecturas recomendadas](#Lecturas_recomendadas)

## Notas iniciales

DokuWiki debería funcionar en cualquier servidor web que soporte PHP 5.6 o posterior. Como los requisitos pueden cambiar con el tiempo, debe consultar la [página de requisitos](http://www.dokuwiki.org/requirements) de DokuWiki para obtener más detalles.

Se recomienda encarecidamente leer las secciones apropiadas de la [página de seguridad](http://www.dokuwiki.org/security) de DokuWiki para su servidor web. La mayoría de los servidores web más populares están cubiertos, pero también hay instrucciones genéricas.

El paquete en [community] descomprime DokuWiki en `/usr/share/webapps/dokuwiki` con los archivos de configuración en `/etc/webapps/dokuwiki` y los archivos de datos en `/var/lib/dokuwiki/data`. También cambia la propiedad de los archivos relevantes al usuario «http». Esto debería funcionar bien para la mayoría de los servidores web más populares, tal como están empaquetados por Arch.

## Instalación

1.  Instale un servidor web de su elección (por ejemplo, [Apache](/index.php/Apache "Apache"), [nginx](/index.php/Nginx "Nginx") o [lighttpd](/index.php/Lighttpd "Lighttpd")) y configúrelo para [PHP](/index.php/PHP "PHP"). Como se mencionó anteriormente, DokuWiki no tiene necesidad de un servidor de base de datos por lo que puede saltarse ese paso al configurar su servidor web.
2.  Instale [dokuwiki](https://www.archlinux.org/packages/?name=dokuwiki) desde [community] con [pacman](/index.php/Pacman "Pacman").
3.  Configure el servidor web para DokuWiki (consulte la sección siguiente).
4.  Con el navegador web de su elección, abra http://<your-server>/dokuwiki/install.php y continúe la instalación desde allí. Para nginx la URL es http://<your-server>/install.php.

Alternativamente, si desea instalar desde un archivo tarball, puede informarse en [http://www.dokuwiki.org/Install](http://www.dokuwiki.org/Install). Generalmente el procedimiento es el mismo que el anterior. En lugar de usar pacman, necesitará [descargar el tarball](http://www.splitbrain.org/projects/dokuwiki), descomprimirlo en la raíz del documento del servidor (por ejemplo, `/srv/http/dokuwiki`), y cambiar los permisos al usuario apropiado (por ejemplo, «http»).

## Configuración

Si está utilizando [lighttpd](/index.php/Lighttpd "Lighttpd") o [nginx](/index.php/Nginx "Nginx") y la versión de PHP es inferior a 7, debe ajustar `open_basedir` en `/etc/php/php.ini` para incluir los directorios dokuwiki (php prohíbe seguir enlaces simbólicos fuera del ámbito permitido):

 `/etc/php/php.ini` 
```
open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/:/usr/share/webapps/:/etc/webapps/dokuwiki/:/var/lib/dokuwiki/

```

También descomente la siguiente línea:

 `/etc/php/php.ini` 
```
extension=gd

```

Dokuwiki necesita esta biblioteca para cambiar el tamaño de las imágenes.

### Apache

El paquete debe tener el archivo `/etc/httpd/conf/extra/dokuwiki.conf` con el siguiente contenido:

```
Alias /dokuwiki /usr/share/webapps/dokuwiki
<Directory /usr/share/webapps/dokuwiki/>
    Options +FollowSymLinks
    AllowOverride All
    order allow,deny
    allow from all
    php_admin_value open_basedir "/tmp/:/usr/share/pear/:/usr/share/webapps/:/etc/webapps/dokuwiki/:/var/lib/dokuwiki/"
</Directory>

```

Si está ejecutando [Apache 2.4 o posterior](https://httpd.apache.org/docs/2.4/upgrading.html), tendrá que cambiar las siguientes líneas:

```
    order allow,deny
    allow from all

```

para que lea:

```
    Require all granted

```

Incluya el archivo recién creado en la configuración de Apache colocando la siguiente línea al final de `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/dokuwiki.conf

```

Asegúrese de que las carpetas `/etc/webapps/dokuwiki` y `/var/lib/dokuwiki` sean propiedad del usuario y del grupo «http». Puede reubicar estos directorios si lo desea, siempre que actualice las referencias en `/etc/httpd/conf/extra/dokuwiki.conf` respectivamente, para que DokuWiki encuentre los complementos y la carpeta tpl.

Después reinicie Apache:

```
 # systemctl restart httpd.service

```

Para terminar la instalación, ejecute el script *dokuwiki/install.php* en su navegador.

### lighttpd

Edite el archivo `/etc/lighttpd/lighttpd.conf` de acuerdo con las [instrucciones dokuwiki](http://www.dokuwiki.org/install:lighttpd) (puede contener información actualizada).

Asegúrese de que los módulos `mod_access` y `mod_alias` están cargados. Si no, carguelos, añadiendo lo siguiente a:

`/etc/lighttpd/lighttpd.conf`:

```
server.modules += ("mod_access")
server.modules += ("mod_alias")
```

`mod_access` proporciona la orden `url.access-deny` que estamos utilizando desde este punto.

Bajo la línea:

```
$HTTP["url"] =~ "\.pdf$" {
  server.range-requests = "disable"
}
```

añada esto:

```
# subdirectorio de dokuwiki
# compuesto por el subdirectorio del directorio raíz donde está instalado dokuwiki
# en este caso el directorio raíz es el directorio base /htdocs/
# Nota: tenga cuidado con las barras inclinadas al unir cadenas.
# Todo el contenido de este servidor de ejemplo se sirve desde htdocs/ hacia arriba.
#var.dokudir = var.basedir + "/dokuwiki"
var.dokudir = server.document-root + "/dokuwiki"

# asegúrese de que siempre se sirvan a través de fastcgi fastcgi y nunca como archivos estáticos
# denegar completamente el acceso a estos
$HTTP["url"] =~ "/(\.|_)ht" { url.access-deny = ( "" ) }
$HTTP["url"] =~ "^" + var.dokudir + "/(bin|data|inc|conf)/"  { url.access-deny = ( "" ) }
```

*Estas entradas dan alguna seguridad básica a DokuWiki*. Lighttpd no utiliza archivos .htaccess como Apache. PUEDE hacer la instalación sin esto, pero NUNCA es recomendable.

Añada alias en algún lugar del archivo de configuración de lighttpd o fastcgi:

 `alias.url += ("/dokuwiki" => "/usr/share/webapps/dokuwiki/")` 

Reinicie lighttpd:

```
 # systemctl restart lighttpd

```

### nginx

Asegúrese de que [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) esté instalado e [iniciado](/index.php/Start_(Espa%C3%B1ol) "Start (Español)").

Añada el siguiente bloque de «server», pero cambie el nombre del servidor por el suyo y comente el bloque install.php hasta que haya terminado de instalar DokuWiki. Este bloque se supone que utiliza TLS. [[2]](https://www.dokuwiki.org/install:nginx)

 `/etc/nginx/nginx.conf` 
```
    server {
        listen 443 ssl http2;
        listen [::]:443 ssl http2;
        server_name wiki.example.com;

        root /usr/share/webapps/dokuwiki;
        index doku.php;

        #Recuerde comentar lo siguiente cuando esté instalando DokuWiki, y descomentarlo cuando haya terminado.
        location ~ /(data/|conf/|bin/|inc/|install.php) { deny all; } # secure Dokuwiki

        location ~^/\.ht { deny all; } # also secure the Apache .htaccess files
        location @dokuwiki {
            #rewrites "doku.php/" out of the URLs if you set the userewrite setting to .htaccess in dokuwiki config page
            rewrite ^/_media/(.*) /lib/exe/fetch.php?media=$1 last;
            rewrite ^/_detail/(.*) /lib/exe/detail.php?media=$1 last;
            rewrite ^/_export/([^/]+)/(.*) /doku.php?do=export_$1&id=$2 last;
            rewrite ^/(.*) /doku.php?id=$1&$args last;
        }

        location / { try_files $uri $uri/ @dokuwiki; }
        location ~ \.php$ {
            try_files $uri =404;
            fastcgi_pass unix:/run/php-fpm/php-fpm.sock;
            fastcgi_index index.php;
            include fastcgi.conf;
        }

    }

```

Reinicie nginx:

```
 # systemctl restart nginx

```

### Activar la carga y visualización de archivos SVG

DokuWiki admite archivos SVG pero los tiene desactivados de forma predeterminada.

Si desea activarlos, cree el siguiente archivo:

 `/etc/webapps/dokuwiki/mime.local.conf` 
```
svg image/svg+xml

```

Esto tiene implicaciones de seguridad: [mire aquí](https://github.com/splitbrain/dokuwiki/issues/1045#issuecomment-90226230)

## Posinstalación

### Limpiar

**Después de configurar el servidor, quite el archivo install.php o asegúrese de que esté inaccesible en la configuración de su servidor web**

```
 # rm /usr/share/webapps/dokuwiki/install.php

```

### Instalar complementos

Muchos complementos creados por la comunidad se pueden encontrar [aquí](http://www.dokuwiki.org/plugins)

Se pueden agregar a través de la interfaz web (así como actualizarla) a través del menú Admin. Algunos plugins no se pueden descargar, si se hace mediante ssl (por ejemplo, git).

### Realizar copias de seguridad

Es muy trivial hacer una copia de seguridad de DokuWiki, ya que no hay base de datos. Todas las páginas están en texto plano, y requieren solo un tar simple, o [rsync](/index.php/Rsync "Rsync")

Un desglose rápido de los directorios de interés en la versión actual (2015-08-10a):

```
  /usr/share/webapps/dokuwiki/data/  =>  Todos los datos creados por el usuario
  /usr/share/webapps/dokuwiki/conf/  =>  Ajustes de configuración

```

Esto puede cambiar en versiones futuras, por favor consulte las [FAQ de DokuWiki](https://www.dokuwiki.org/faq:backup) para comprobarlo.

## Lecturas recomendadas

La [página principal de DokuWiki](http://www.dokuwiki.org/) tiene toda la información y ayuda que pueda necesitar.