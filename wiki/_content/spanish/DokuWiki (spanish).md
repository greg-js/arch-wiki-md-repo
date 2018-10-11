**Estado de la traducción**
Este artículo es una traducción de [DokuWiki](/index.php/DokuWiki "DokuWiki"), revisada por última vez el **2017-9-16**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=DokuWiki&diff=0&oldid=) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

"[DokuWiki](https://www.dokuwiki.org/dokuwiki#) es un wiki que cumple con los estándares, simple de usar y que permite a los usuarios crear ricos repositorios de documentación. Además permite a los individuos, equipos y empresas crear y colaborar utilizando una sintaxis sencilla pero potente que garantiza que los archivos de datos permanezcan estructurados y legible fuera del wiki".

"Las revisiones de página ilimitadas permiten la restauración de cualquier versión anterior de la página, y con los datos almacenados en archivos de texto sin formato, además no se requiere ninguna base de datos. Una poderosa arquitectura de complementos permite la extensión y la mejora del sistema central. Vea la sección de características para una descripción completa de lo que DokuWiki tiene para ofrecer." [[1]](http://wiki.splitbrain.org/wiki:dokuwiki)

En otras palabras, DokuWiki es un Wiki escrito en PHP y no requiere base de datos.

## Contents

*   [1 Notas iniciales](#Notas_iniciales)
*   [2 Instalación](#Instalaci.C3.B3n)
*   [3 Configuración](#Configuraci.C3.B3n)
    *   [3.1 Apache](#Apache)
    *   [3.2 lighttpd](#lighttpd)
    *   [3.3 nginx](#nginx)
*   [4 Post-instalación](#Post-instalaci.C3.B3n)
    *   [4.1 Limpiando](#Limpiando)
    *   [4.2 Instalación de Plugins](#Instalaci.C3.B3n_de_Plugins)
    *   [4.3 Realizar copias de seguridad](#Realizar_copias_de_seguridad)
*   [5 Crear enlace en Kde Plasma](#Crear_enlace_en_Kde_Plasma)
*   [6 Lecturas recomendadas](#Lecturas_recomendadas)
*   [7 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Notas iniciales

DokuWiki debería funcionar en cualquier servidor web que soporte PHP 5.6 o posterior. Como los requisitos pueden cambiar con el tiempo, debe consultar la [página de requisitos](http://www.dokuwiki.org/requirements) de DokuWiki para obtener más detalles.

Se recomienda encarecidamente leer las secciones apropiadas de la [página de seguridad](http://www.dokuwiki.org/security) de DokuWiki para su servidor web. La mayoría de los servidores web más populares están cubiertos, pero también hay instrucciones genéricas.

El paquete en [community] descomprime DokuWiki en `/usr/share/webapps/dokuwiki` con los archivos de configuración en `/etc/webapps/dokuwiki` y los archivos de datos en `/var/lib/dokuwiki/data`. También cambia la propiedad de los archivos relevantes al usuario "http". Esto debería funcionar bien para la mayoría de los servidores web más populares, tal como están empaquetados para Arch.

## Instalación

1.  Instale un servidor web de su elección (por ejemplo, [Apache](/index.php/Apache "Apache"), [nginx](/index.php/Nginx "Nginx") o [lighttpd](/index.php/Lighttpd "Lighttpd")) y configúrelo para [PHP](/index.php/PHP "PHP"). Como se mencionó anteriormente, DokuWiki no tiene necesidad de un servidor de base de datos por lo que puede ser capaz de saltar esos pasos al configurar su servidor
2.  Instalar [dokuwiki](https://www.archlinux.org/packages/?name=dokuwiki) desde [community] con [pacman](/index.php/Pacman "Pacman").
3.  Configure el servidor web para DokuWiki (consulte la sección siguiente)
4.  Con su navegador web de su elección, abra http://<your-server>/dokuwiki/install.php y continúe la instalación desde allí. Para nginx la URL es http://<your-server>/install.php.

Alternativamente, si desea instalar desde un tarball, puede leerlo en [http://www.dokuwiki.org/Install](http://www.dokuwiki.org/Install) . Generalmente el procedimiento es el mismo que el anterior. En lugar de usar pacman, necesitará [descargar el tarball](http://www.splitbrain.org/projects/dokuwiki), descomprimirlo en la raíz del documento del servidor (por ejemplo, `/srv/http/dokuwiki`), y cambie los permisos al usuario apropiado (por ejemplo, "http").

## Configuración

Si está usando [lighttpd](/index.php/Lighttpd "Lighttpd") o [nginx](/index.php/Nginx "Nginx") y su versión de PHP es inferior a 7, debe ajustar `open_basedir` en `/etc/php/php.ini` para incluir los directorios dokuwiki (php prohíbe seguir enlaces simbólicos fuera del ámbito permitido):

 `/etc/php/php.ini` 
```
open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/:/usr/share/webapps/:/etc/webapps/dokuwiki/:/var/lib/dokuwiki/

```

También descomente la siguiente línea.

 `/etc/php/php.ini` 
```
extension=gd.so

```

Dokuwiki necesita esta biblioteca para cambiar el tamaño de las imágenes.

### Apache

El paquete debe ser agregado a el archivo `/etc/httpd/conf/extra/dokuwiki.conf` con el siguiente contenido:

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

Si está ejecutando [Apache 2.4 o más reciente](https://httpd.apache.org/docs/2.4/upgrading.html), tendrá que cambiar las siguientes líneas:

```
    order allow,deny
    allow from all

```

a leer:

```
    Require all granted

```

Incluya el archivo recién creado en la configuración de Apache colocando la siguiente línea al final de `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/dokuwiki.conf

```

Asegúrese de que las carpetas `/etc/webapps/dokuwiki` y `/var/lib/dokuwiki` sean propiedad del usuario y del grupo "http". Puede reubicar estos directorios si lo desea, siempre que actualice las referencias en `/etc/httpd/conf/extra/dokuwiki.conf` respectivamente.

Después reinicie Apache:

```
 # Systemctl restart httpd.service

```

Luego termine la instalación ejecutando el script *dokuwiki/install.php* en su navegador.

### lighttpd

Edite el archivo `/etc/lighttpd/lighttpd.conf` de acuerdo con las instrucciones dokuwiki (puede contener información actualizada).

Asegúrese de que los módulos `mod_access` y `mod_alias` están cargados. Si no, carguelos añadiendo lo siguiente a `/etc/lighttpd/lighttpd.conf`:

```
server.modules += ("mod_access")
server.modules += ("mod_alias")
```

`mod_access` proporciona el comando `url.access-deny` que estamos utilizando desde este punto.

Bajo la línea:

```
$HTTP["url"] =~ "\.pdf$" {
  server.range-requests = "disable"
}
```

Agregue esto:

```
# subdir of dokuwiki
# comprised of the subdir of the root dir where dokuwiki is installed
# in this case the root dir is the basedir plus /htdocs/
# Note: be careful with trailing slashes when uniting strings.
# all content on this example server is served from htdocs/ up.
#var.dokudir = var.basedir + "/dokuwiki"
var.dokudir = server.document-root + "/dokuwiki"

# make sure those are always served through fastcgi and never as static files
# deny access completly to these
$HTTP["url"] =~ "/(\.|_)ht" { url.access-deny = ( "" ) }
$HTTP["url"] =~ "^" + var.dokudir + "/(bin|data|inc|conf)/"  { url.access-deny = ( "" ) }
```

*Estas entradas dan alguna seguridad básica a DokuWiki*. Lighttpd no utiliza archivos .htaccess como Apache. Puedes hacer la instalar sin esto, pero nunca es recomendable.

Añadir alias en algún lugar en lighttpd o fastcgi archivo conf:

 `alias.url += ("/dokuwiki" => "/usr/share/webapps/dokuwiki/")` 

Reinicie lighttpd:

```
 # Systemctl restart lighttpd

```

### nginx

Asegúrese de que [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) esté instalado e iniciado [start](/index.php/Start "Start").

Agregue el siguiente bloque del servidor, pero cambie el nombre del servidor al suyo y comente el bloque install.php hasta que haya terminado de instalar DokuWiki. Este bloque se supone que utiliza TLS. [[2]](https://www.dokuwiki.org/install:nginx)

 `/etc/nginx/nginx.conf` 
```
    server {
        listen 443 ssl http2;
        listen [::]:443 ssl http2;
        server_name wiki.example.com;

        root /usr/share/webapps/dokuwiki;
        index doku.php;

        #Remember to comment the below out when you're installing DokuWiki, and uncomment it when you're done.
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

Reinicie nginx

```
 # Systemctl restart nginx

```

## Post-instalación

### Limpiando

**Después de configurar el servidor, quite el archivo install.php o asegúrese de que esté inaccesible en su configuración de servidor web!**

```
 # rm /srv/http/dokuwiki/install.php

```

### Instalación de Plugins

Muchos complementos creados por la comunidad se pueden encontrar [aquí](http://www.dokuwiki.org/plugins)

Se pueden agregar a través de la interfaz web (así como actualizada) a través del menú Admin. Algunos plugins no se pueden descargar, si están por encima de ssl (por ejemplo, git).

### Realizar copias de seguridad

Es muy trivial hacer una copia de seguridad de DokuWiki, ya que no hay base de datos. Todas las páginas están en texto sin formato, y requieren sólo un tar simple, o [rsync](/index.php/Rsync "Rsync").

Un desglose rápido de los directorios de interés en la versión actual (2015-08-10a):

```
 / Dokuwiki / data / => Todos los datos creados por el usuario
 / Dokuwiki / conf / => Configuraciones

```

Esto puede cambiar en versiones futuras, por favor consulte las [Preguntas Frecuentes de DokuWiki](https://www.dokuwiki.org/faq:backup) para verificación.

## Crear enlace en Kde Plasma

Para crear un enlace y ejecutar automaticamente el servidor instalado y la wiki, crearemos un script bash y un archivo .desktop.

Cree un archivo de texto y guárdelo con el nombre Dokuwiki:

Agregue las siguientes lineas:

```
#!/bin/bash
#
# Dokuwiki -- script: ejecuta el servidor web y luego abre
#                     la url de la wiki con el navegador firefox 
#

# Servidor instalado, puede ser httpd.service, lighttpd o nginx
service=httpd.service   

# Navegador por defecto, sustituya por el de su preferencia opera, chrome, etc.
nav=firefox   

# Reinicia el servicio del servidor web
systemctl restart $service     

# Inicia el navegador web con la url de la wiki
$nav "http://localhost/dokuwiki/doku.php\?id\=start"
```

Para crear el acceso directo al menu de aplicaciones, cree un archivo acceso directo en la ruta `/home/usuario/.local/share/applications/` haciendo clic derecho *Crear nuevo > Enlace a aplicación*, con el nombre Dokuwiki. Abra el archivo Dokuwiki.desktop y agregue lo siquiente:

**Nota:** Tenga en cuenta que la opción **Exec** es la ruta donde se encuentra el script, además del nombre del mismo *./Dokuwiki*.

```
[Desktop Entry]
Categories=Office;
Comment[es_CO]=
Comment=
Exec=bash -c 'cd /home/"usuario"/.local/share/applications/; ./Dokuwiki;$SHELL exit'
GenericName[es_CO]
GenericName=
Icon=/usr/share/webapps/dokuwiki/data/media/wiki/dokuwiki-128.png
MimeType=
Name[es_CO]=Dokuwiki
Name=Dokuwiki
Path=
StartupNotify=true
Terminal=true
TerminalOptions=
Type=Application
X-DBUS-ServiceName=
X-DBUS-StartupType=
X-KDE-SubstituteUID=false
X-KDE-Username=
```

## Lecturas recomendadas

La web de [DokuWiki](http://www.dokuwiki.org/) tiene toda la información y ayuda que usted pueda necesitar.

## Véase también

[DokuWiki HowTo Install and Upgrade](http://wiki.gotux.net/config:dokuwiki)