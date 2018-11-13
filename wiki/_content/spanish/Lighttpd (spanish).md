[Lighttpd](https://www.lighttpd.net/) es un servidor web "seguro, rápido, compatible y muy flexible" que ha sido optimizado para ambientes de alto rendimiento. Consume muy pocos recursos comparado con otros servidores web y se ocupa de balancear el CPU. Sus características avanzadas ([FastCGI](https://en.wikipedia.org/wiki/FastCGI "wikipedia:FastCGI"), [CGI](https://en.wikipedia.org/wiki/Common_Gateway_Interface "wikipedia:Common Gateway Interface"), Auth, entre otras) hacen que lighttpd sea el servidor web perfecto para todos aquellos que sufren problemas de balanceo."

## Contents

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 Sistema básico](#Sistema_básico)
        *   [2.1.1 Historial básico](#Historial_básico)
        *   [2.1.2 Habilitar https con SSL](#Habilitar_https_con_SSL)
            *   [2.1.2.1 Auto firmado](#Auto_firmado)
            *   [2.1.2.2 Let's Encrypt](#Let's_Encrypt)
    *   [2.2 CGI](#CGI)
    *   [2.3 FastCGI](#FastCGI)
        *   [2.3.1 PHP](#PHP)
            *   [2.3.1.1 Uso php-cgi](#Uso_php-cgi)
            *   [2.3.1.2 Uso php-fpm](#Uso_php-fpm)
        *   [2.3.2 Python FastCGI](#Python_FastCGI)
            *   [2.3.2.1 Indicador del nombre del servidor](#Indicador_del_nombre_del_servidor)
        *   [2.3.3 Ruby on Rails](#Ruby_on_Rails)
        *   [2.3.4 Re-direccionamiento de http a https](#Re-direccionamiento_de_http_a_https)
    *   [2.4 Compresión](#Compresión)
*   [3 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [lighttpd](https://www.archlinux.org/packages/?name=lighttpd).

## Configuración

### Sistema básico

EL archivo de configuración de lighttpd es: `/etc/lighttpd/lighttpd.conf`. Por defecto debe producir una pagina de prueba.

Para comprobar su `lighttpd.conf` por bugs se puede usar el siguiente comando, que ayuda a encontrar errores en la configuración rápidamente:

```
$ lighttpd -t -f /etc/lighttpd/lighttpd.conf

```

Otra prueba mucho mas estricta puede ser ejecutada con:

```
$ lighttpd -tt -f /etc/lighttpd/lighttpd.conf

```

El archivo de la configuración por defecto especifica que el directorio `/srv/http/` es la base de los documentos servidos. Para comprobar la instalación, cree un archivo de prueba:

 `/srv/http/index.html`  `Hola Mundo!` 

Después [active](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)") la unidad `lighttpd.service` y en su navegador diríjase a `localhost`, donde debería ver la pagina de prueba.

Archivos de configuración con ejemplos están disponibles en `/usr/share/doc/lighttpd/`.

#### Historial básico

Lighttpd puede escribir archivos con historiales de acceso y de errores. Para habilitar ambas opciones edite el archivo `/etc/lighttpd/lighttpd.conf`:

```
server.modules += (
   "mod_access",
   "mod_accesslog",
)

server.errorlog   = "/var/log/lighttpd/errores.log"
accesslog.filename = "/var/log/lighttpd/accesos.log"

```

#### Habilitar https con SSL

**Advertencia:** Usuarios que planean implementar SSL/TLS, deben saber que algunas variaciones e implementaciones son vulnerables a ataques. Vease el articulo de [OpenSSL](/index.php/OpenSSL "OpenSSL") para mas detalles.

**Sugerencia:**

*   Mozilla tiene un [generador de configuracion](https://mozilla.github.io/server-side-tls/ssl-config-generator/) que puede ser usado con lighttpd.
*   Despues de configurar SSL, puede [verificar su configuracion](https://www.ssllabs.com/ssltest/index.html) con el servicio de Qualys SSL Labs.

##### Auto firmado

Certificados de SSL que son auto firmados pueden ser generados, asumiendo el paquete [openssl](https://www.archlinux.org/packages/?name=openssl) esta instalado, de la siguiente manera:

```
# mkdir /etc/lighttpd/certs
# openssl req -x509 -nodes -days 7300 -newkey rsa:2048 -sha256 -keyout /etc/lighttpd/certs/server.pem -out /etc/lighttpd/certs/server.pem
# chmod 600 /etc/lighttpd/certs/server.pem

```

Modifique el archivo `/etc/lighttpd/lighttpd.conf` para habilitar https:

```
$SERVER["socket"] == ":443" {
    ssl.engine                  = "enable" 
    ssl.pemfile                 = "/etc/lighttpd/certs/server.pem" 
 }

```

##### Let's Encrypt

Alternativamente, pero muy recomendado, puede generar un certificado firmado por [Let's Encrypt](/index.php/Let%27s_Encrypt "Let's Encrypt"). Despues de seguir las instrucciones de la generacion manual de un certificado, combine los archivos `privkey.pem` y `fullchain.pem` en uno:

```
# cat /etc/letsencrypt/live/*su-dominio*/{privkey.pem,fullchain.pem} > /etc/letsencrypt/live/*su-dominio*/combined.pem

```

Edite su archivo de configuracion principal `/etc/lighttpd/lighttpd.conf` agregando:

```
$SERVER["socket"] == ":443" {
    ssl.engine                  = "enable" 
    ssl.pemfile                 = "/etc/letsencrypt/live/*su-dominio*/combined.pem"
    ssl.ca-file                 = "/etc/letsencrypt/live/*su-dominio*/fullchain.pem"
}

```

Si recibe un error *empty reply from server* al intentar `curl [https://su-dominio](https://su-dominio)`, intente agregar:

```
ssl.openssl.ssl-conf-cmd = ("Protocol" => "-ALL, TLSv1.2") 

```

a la configuracion anterios. Esto tambien puede arreglar el caso qeu Firefox no pueda abrir la version HTTPs de su sitio.

### CGI

[Interfaz de entrada común](https://en.wikipedia.org/wiki/es:Interfaz_de_entrada_com%C3%BAn "wikipedia:es:Interfaz de entrada común") (Common Gateway Interface, **CGI** en ingles) funciona automáticamente con lighttpd, solo es necesario habilitar el modulo, incluir el archivo de configuración y asegurarse que su lenguaje interprete esta instalado. Por ejemplo [python](https://www.archlinux.org/packages/?name=python) o [ruby](https://www.archlinux.org/packages/?name=ruby).

Cree el archivo `/etc/lighttpd/conf.d/cgi.conf` y agregue lo siguiente:

```
server.modules += ( "mod_cgi" )

cgi.assign                 = ( ".pl"  => "/usr/bin/perl",
                               ".cgi" => "/usr/bin/perl",
                               ".rb"  => "/usr/bin/ruby",
                               ".erb" => "/usr/bin/eruby",
                               ".py"  => "/usr/bin/python",
                               ".php" => "/usr/bin/php-cgi" )

index-file.names           += ( "index.pl",   "default.pl",
                               "index.rb",   "default.rb",
                               "index.erb",  "default.erb",
                               "index.py",   "default.py",
                               "index.php",  "default.php" )

```

Para scripts de PHP debe asegurarse que la siguiente opción se encuentra en `/etc/php/php.ini`:

```
cgi.fix_pathinfo = 1

```

En su archivo de configuración principal `/etc/lighttpd/lighttpd.conf` agregue:

```
include "conf.d/cgi.conf"

```

### FastCGI

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [fcgi](https://www.archlinux.org/packages/?name=fcgi). Ahora ya tiene lighttpd con soporte para fcgi. Si esto era todo lo que se deseaba.

Si se desea expandir con Ruby on Rails, PHP o Python deben leer las secciones siguientes.

**Nota:** El usuario/grupo por defecto de lighttpd es `http`.

En primer lugar copie la configuración que provee lighttpd de `/usr/share/doc/lighttpd/config/conf.d/fastcgi.conf` a `/etc/lighttpd/conf.d`.

Agregue lo siguiente al archivo de configuración `/etc/lighttpd/conf.d/fastcgi.conf`:

```
server.modules += ( "mod_fastcgi" )

#server.indexfiles += ( "dispatch.fcgi" )      # Opcion obsoleta
index-file.names += ( "dispatch.fcgi" )        # dispatch.fcgi si Rails se especifica

server.error-handler-404   = "/dispatch.fcgi"  # tambien
fastcgi.server = (
    ".fcgi" => (
      "localhost" => ( 
        "socket" => "/run/lighttpd/rails-fastcgi.sock",
        "bin-path" => "/path/to/rails/application/public/dispatch.fcgi"
      )
    )
)

```

Incluya esta linea en su archivo de configuracion principal `/etc/lighttpd/lighttpd.conf`:

```
include "conf.d/fastcgi.conf"

```

#### PHP

##### Uso php-cgi

Instale [php](https://www.archlinux.org/packages/?name=php) y [php-cgi](https://www.archlinux.org/packages/?name=php-cgi), véase también [PHP](/index.php/PHP_(Espa%C3%B1ol) "PHP (Español)") y [LAMP](/index.php/LAMP_(Espa%C3%B1ol) "LAMP (Español)").

Asegúrese que php-cgi funciona ejecutando el comando `php-cgi --version`

```
PHP 5.4.3 (cgi-fcgi) (built: May  8 2012 17:10:17)
Copyright (c) 1997-2012 The PHP Group
Zend Engine v2.4.0, Copyright (c) 1998-2012 Zend Technologies

```

Si tiene un resultado similar, quiere decir que PHP fue instalado correctamente.

Cree un archivo de configuración:

 `/etc/lighttpd/conf.d/fastcgi.conf` 
```

# Asegurese de instalar php and php-cgi. Véase:                                                             
# https://wiki.archlinux.org/index.php/Lighttpd_(Español)#PHP

server.modules += ("mod_fastcgi")

# Servidor FCGI
# =============
#
# Configuración de un servidor FastCGI con resolución de PHP.
#
index-file.names += ("index.php")
fastcgi.server = ( 
    # Balancear peticiones para esta ruta..
    ".php" => (
        # ... dentro de los siguientes servidores FastCGI. El nombre de cada
        # servidor es una etiqueta para identificarlo en el historial.
        "localhost" => ( 
            "bin-path" => "/usr/bin/php-cgi",
            "socket" => "/tmp/php-fastcgi.sock",
            "broken-scriptfilename" => "enable",
            "max-procs" => 4,                     # Valor por defecto
            "bin-environment" => (
                "PHP_FCGI_CHILDREN" => "1"        # Valor por defecto
            )
        )
    )   
)

```

Asegúrese que lighttpd use el archivo anterior agregando la siguiente linea a su archivo de configuración principal:

 `/etc/lighttpd/lighttpd.conf` 
```
include "conf.d/fastcgi.conf"

```

**Nota:** recuerde que el orden en que los módulos se cargan es importante, una lista con el orden correcto esta en `/usr/share/doc/lighttpd/config/modules.conf`.

[Recargue](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)") lighttpd.

**Nota:**

*   Si tiene errores de forma *Archivo de entrada no encontrado (No input file found)*, puede tener varias explicaciones. Véase estas [preguntas frecuentes](https://redmine.lighttpd.net/projects/1/wiki/frequentlyaskedquestions#I-get-the-error-No-input-file-specified-when-trying-to-use-PHP) por mas información.
*   Asegúrese que ningún otro modulo, por ejemplo `mod_cgi`, intentara manejar la extensión *.php*.

##### Uso php-fpm

En versiones recientes de lighttps no hay inicio adaptivo. Para manejo dinámico de procesos PHP es posible instalar [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) y luego [activar](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") e iniciar automáticamente la unidad `php-fpm.service`.

**Nota:** Es posible configurar el numero de servidores y otras opciones modificando el archivo `/etc/php/php-fpm.conf`. Mas detalles en la [pagina web de php-fpm](http://php-fpm.org/). Recuerde que al realizar cambios en `/etc/php/php.ini` es necesario reiniciar la unidad `php-fpm.service`.

En el archivo `/etc/lighttpd/conf.d/fastcgi.conf` agregue:

```
server.modules += ( "mod_fastcgi" )

index-file.names += ( "index.php" ) 

fastcgi.server = (
    ".php" => (
      "localhost" => ( 
        "socket" => "/run/php-fpm/php-fpm.sock",
        "broken-scriptfilename" => "enable"
      ))
)

```

#### Python FastCGI

**Nota:**

*   lighttpd soporta el protocolo WSGI de Python: [HowToPythonWSGI](https://redmine.lighttpd.net/projects/lighttpd/wiki/HowToPythonWSGI).
*   El siguiente método no funcionara con Python 3, ya que la librería *Flup* solo esta disponible para Python 2\. Si desea usar Python 3, refiérase a la sección [#CGI](#CGI).

Instale y configure FastCGI, véase la sección [#FastCGI](#FastCGI).

Instale [python2-flup](https://www.archlinux.org/packages/?name=python2-flup).

Configure:

```
fastcgi.server = (
    ".py" =>
    (
        "python-fcgi" =>
        (
        "socket" => "/run/lighttpd/fastcgi.python.socket",
         "bin-path" => "test.py",
         "check-local" => "disable",
         "max-procs" => 1,
        )
    )
)

```

Ponga el archivo *test.py* en el directorio raíz de su servidor y no olvide permitir su ejecución: `chmod +x *test.py*`.

```
#!/usr/bin/env python2

def myapp(environ, start_response):
    print 'got request: %s' % environ
    start_response('200 OK', [('Content-Type', 'text/plain')])
    return ['Hello World!']

if __name__ == '__main__':
    from flup.server.fcgi import WSGIServer
    WSGIServer(myapp).run()
```

[Gracias a firecat53 por su explicación](https://bbs.archlinux.org/viewtopic.php?pid=734173#p734173)

##### Indicador del nombre del servidor

Para usar [SNI](https://en.wikipedia.org/wiki/es:Server_Name_Indication "wikipedia:es:Server Name Indication") (por sus siglas en ingles) simplemente ponga las directivas del archivo ssl.pemfile en los condicionales del servidor. Un ssl.pemfile es [requerido](https://redmine.lighttpd.net/projects/1/wiki/Docs_SSL#Server-Name-Indication-SNI) por defecto.

```
$HTTP["host"] == "www.example.org" {
    ssl.pemfile = "/etc/lighttpd/certs/www.example.org.pem" 
}

$HTTP["host"] == "mail.example.org" {
    ssl.pemfile = "/etc/lighttpd/certs/mail.example.org.pem" 
}

```

#### Ruby on Rails

Si se desea usar Ruby on Rails, [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") los paquetes [ruby](https://www.archlinux.org/packages/?name=ruby) y [rubygems](https://www.archlinux.org/packages/?name=rubygems).

Para documentación de como usar Ruby on Rails por favor consulta [http://rubyonrails.org](http://rubyonrails.org).

#### Re-direccionamiento de http a https

Agregue la linea `"mod_redirect"` en su archivo de configuración principal `/etc/lighttpd/lighttpd.conf`:

```
server.modules += ( "mod_redirect" )

$SERVER["socket"] == ":80" {
  $HTTP["host"] =~ "example.org" {
    url.redirect = ( "^/(.*)" => "https://example.org/$1" )
    server.name                 = "example.org" 
  }
}

$SERVER["socket"] == ":443" {
  ssl.engine = "enable" 
  ssl.pemfile = "/etc/lighttpd/certs/server.pem" 
  server.document-root = "..." 
}

```

Para el re-direccionamiento de todos los sitios a su equivalente seguro, use la siguiente configuración en lugar de la conexión al socket 80:

```
$SERVER["socket"] == ":80" {
  $HTTP["host"] =~ ".*" {
    url.redirect = (".*" => "https://%0$0")
  }
}

```

Para el re-direccionamiento de parte de los sitios, por ejemplo *phpmyadmin*:

```
$SERVER["socket"] == ":80" {
  $HTTP["url"] =~ "^/secure" {
    url.redirect = ( "^/(.*)" => "https://example.com/$1" )
  }
}

```

### Compresión

La compresión de los archivos que el servidor provee a los visitantes puede ser una gran ventaja al reducir el ancho de banda requerido para la carga de la pagina web:

En el archivo principal `/etc/lighttpd/lighttpd.conf` agregue:

```
var.cache_dir           = "/var/cache/lighttpd"

```

Cree un directorio para los archivos comprimidos:

```
# mkdir /var/cache/lighttpd/compress
# chown http:http /var/cache/lighttpd/compress

```

Copie el ejemplo del archivo de compresión:

```
# mkdir /etc/lighttpd/conf.d
# cp /usr/share/doc/lighttpd/config/conf.d/compress.conf /etc/lighttpd/conf.d/

```

Agregue la siguiente linea al archivo principal de configuración `/etc/lighttpd/lighttpd.conf`:

```
include "conf.d/compress.conf"

```

También es posible seleccionar el tipo de contenido que se puede comprimir, modifique `/etc/lighttpd/conf.d/compress.conf` en la opción `compress.filetype`:

```
compress.filetype     = ("text/plain", "text/html", "text/javascript", "text/css", "text/xml")

```

## Véase también

*   [lighttpd wiki](https://redmine.lighttpd.net/projects/lighttpd/wiki)