# Dokuwiki (Español)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

"DokuWiki es un sistema de [Wiki](http://en.wikipedia.org/wiki/Wiki) de uso sencillo y compatible con los estándares. Orientado a crear documentación de cualquier tipo dentro de grupos de desarrollo, grupos de trabajo y pequeñas empresas. Su sintaxis es simple y potente, facilita la creación de textos estructurados, y permite que los archivos generados sean legibles incluso fuera del Wiki. Todos los datos se guardan en archivos de texto plano, de tal forma que no se necesita base de datos para su funcionamiento."

"Las revisiones ilimitadas de páginas permiten, no obstante, la restauración a cualquier versión de la página anterior; y con los datos almacenados en archivos de texto plano, las bases de datos son innecesarias. Una arquitectura basada en plugins de gran variedad permite la ampliación y mejora del sistema central. Vea la sección de características para obtener una descripción completa de lo que DokuWiki puede ofrecerle". [[1]](http://wiki.splitbrain.org/wiki:dokuwiki)

En otras palabras, DokuWiki es un Wiki escrito en PHP y no requiere base de datos.

[¿Le gustaría ver un ejemplo en funcionamiento?](http://www.dokuwiki.org/)

## Contents

*   [1 Notas iniciales](#Notas_iniciales)
*   [2 Instalación](#Instalaci.C3.B3n)
*   [3 Configuración](#Configuraci.C3.B3n)
    *   [3.1 Apache](#Apache)
    *   [3.2 Configuración específica para lighttpd](#Configuraci.C3.B3n_espec.C3.ADfica_para_lighttpd)
*   [4 Post-instalación](#Post-instalaci.C3.B3n)
    *   [4.1 Limpiando](#Limpiando)
    *   [4.2 Instalación de Plugins](#Instalaci.C3.B3n_de_Plugins)
    *   [4.3 Realizar copias de seguridad](#Realizar_copias_de_seguridad)
*   [5 Lecturas recomendadas](#Lecturas_recomendadas)
*   [6 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Notas iniciales

DokuWiki debería funcionar en cualquier servidor web que soporte PHP 5.1.2 o posterior. Dado que los requisitos pueden cambiar con el tiempo, debe consultar los [requerimientos](http://www.dokuwiki.org/requirements) para DokuWiki a fin de obtener detalles adicionales.

Es muy recomendable que lea las secciones correspondientes a la [seguridad de las páginas de Dokuwiki](http://www.dokuwiki.org/security) para el servidor web. Los servidores web más populares están cubiertos, pero hay instrucciones genéricas también.

El paquete de [community] descomprime DokuWiki en `/srv/http/dokuwiki`, luego, proceda a cambiar la propiedad del mismo al usuario "http". Ésto debería hacer que funcionara bien el empaquetado de Arch en los servidores web más populares.

## Instalación

1.  Instalar el servidor web de su elección (por ejemplo, [Apache](/index.php/Apache "Apache") o [lighttpd](/index.php/Lighttpd "Lighttpd")) y configurarlo para [PHP](/index.php/PHP "PHP"). Como se mencionó anteriormente, DokuWiki no tiene necesidad de un servidor database, por lo que puede omitir los pasos para configurar este último en su servidor web.
2.  Instalar [dokuwiki](https://www.archlinux.org/packages/?name=dokuwiki) desde [community] con [pacman](/index.php/Pacman "Pacman").
3.  Con el navegador web de su elección, abra **http://<su-servidor>/dokuwiki/install.php** y continue con la instalación desde ahí.

Alternativamente, si desea puede realizar la instalación con el archivo .tgz, se puede instruir en [http://www.dokuwiki.org/Install](http://www.dokuwiki.org/Install). Generalmente, el procedimiento es el mismo que el anterior. En lugar de usar pacman, tendrá que descargar el [archivo .tgz](http://www.splitbrain.org/projects/dokuwiki), descomprimirlo a la raíz del servidor para los documentos (por ejemplo, `/srv/http/dokuwiki`) y ejecutar el comando chown para dar permisos al usuario adecuado (por ejemplo, "http").

## Configuración

### Apache

En primer lugar, cree el archivo `/etc/httpd/conf/extra/dokuwiki.conf` con el siguiente contenido:

```
Alias /dokuwiki /usr/share/webapps/dokuwiki
<Directory /usr/share/webapps/dokuwiki/>
    Options +FollowSymLinks
    AllowOverride All
    order allow,deny
    allow from all
    php_admin_value open_basedir "/srv/http/:/home/:/tmp/:/usr/share/pear/:/usr/share/webapps/:/etc/webapps/dokuwiki/:/var/lib/dokuwiki/"
</Directory>

```

Incluya el archivo recién creado en la configuración de Apache poniendo la siguiente línea al final de `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/dokuwiki.conf

```

Asegúrese de que las carpetas `/etc/webapps/dokuwiki` y `/var/lib/dokuwiki` son propiedad del usuario y del grupo «http». Puede reubicar estos directorios si lo desea, siempre y cuando actualizar las referencias en `/etc/httpd/conf/extra/dokuwiki.conf` respectivamente.

Después reinicie Apache:

```
 # systemctl restart httpd.service

```

Por último, finalice la instalación ejecutando el script _dokuwiki/install.php_ en su navegador.

### Configuración específica para lighttpd

Edite el archivo `/etc/lighttpd/lighttpd.conf` como se indica en [dokuwiki en lighttpd](https://www.dokuwiki.org/install:lighttpd) (puede contener información actualizada).

Bajo la línea:

```

$HTTP["url"] =~ "\.pdf$" {
  server.range-requests = "disable"
}

```

añada lo siguiente:

```
# subdirectorio de dokuwidi
# comprende el subdirectorio y el directorio raiz donde está instalado dokuwiki
# en este caso el directorio raiz es el directorio base más /htdocs/
# Nota: tener cuidado con barra final al unir cadenas.
# todo el contenido de este servidor de ejemplo se sirve de htdocs/ up.
# var.dokudir = var.basedir + "/dokuwiki"
var.dokudir = server.document-root + "/dokuwiki"

# asegurarse de que se sirve siempre a través de fastcgi y nunca de archivos estáticos
# negar el acceso completamente a éstos
$HTTP["url"] =~ "/\.ht" { url.access-deny = ( "" ) }
$HTTP["url"] =~ "/_ht" { url.access-deny = ( "" ) }
$HTTP["url"] =~ "^" + var.dokudir + "/bin/"  { url.access-deny = ( "" ) }
$HTTP["url"] =~ "^" + var.dokudir + "/data/" { url.access-deny = ( "" ) }
$HTTP["url"] =~ "^" + var.dokudir + "/inc/"  { url.access-deny = ( "" ) }
$HTTP["url"] =~ "^" + var.dokudir + "/conf/" { url.access-deny = ( "" ) }

```

_Estas entradas dan algo de seguridad básica para DokuWiki_. Lighttpd no usa archivos .htaccess como Apache. Se PUEDEN instalar con este, pero NO es recomendable.

 `alias.url += ("/dokuwiki" => "/usr/share/webapps/dokuwiki/")` 

Añada un alias en algún lugar de lighttpd o un archivo conf de fastcgi

Reinicie lighttp:

```
  # systemctl restart lighttpd

```

## Post-instalación

### Limpiando

**¡Después de configurar el servidor elimine el archivo install.php!**

```
 # rm /srv/http/dokuwiki/install.php

```

### Instalación de Plugins

Muchos plugins creados por la comunidad se pueden encontrar [aquí](http://www.dokuwiki.org/plugins)

Se pueden añadir a través de la interfaz web (así como actualizarlos) a través del menú Admin. Algunos plugins no se pueden descargar, si se quieren obtener a través de ssl (por ejemplo git).

### Realizar copias de seguridad

Es muy trivial hacer copia de seguridad de DokuWiki, ya que no hay ninguna base de datos. Todas las páginas están en texto plano, y sólo requieren un simple tar, o rsync.

Un rápido resumen de los directorios de interés en la actual versión (2012-01-25b):

```
 /dokuwiki/data/         => Todos los Datos creados por el usuario
 /dokuwiki/lib/plugins/  => Todos los Plugins añadidos por el usuario

```

## Lecturas recomendadas

La web de [DokuWiki](http://www.dokuwiki.org/) tiene toda la información y ayuda que usted pueda necesitar.

## Véase también

[DokuWiki HowTo Install and Upgrade](http://wiki.gotux.net/config:dokuwiki)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dokuwiki_(Español)&oldid=414215](https://wiki.archlinux.org/index.php?title=Dokuwiki_(Español)&oldid=414215)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Office (Español)](/index.php/Category:Office_(Espa%C3%B1ol) "Category:Office (Español)")