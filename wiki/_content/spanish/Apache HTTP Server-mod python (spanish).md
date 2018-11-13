**Advertencia:** mod_python está [desatendido](http://blog.dscpl.com.au/2010/06/modpython-project-is-now-officially.html) y tiene múltiples problemas de seguridad, rendimiento y estabilidad. Se recomienda encarecidamente utilizar [mod_wsgi](/index.php/Mod_wsgi "Mod wsgi") en su lugar.

## Contents

*   [1 Introducción](#Introducción)
*   [2 Instalación](#Instalación)
    *   [2.1 Módulo de Apache : Mod_Python](#Módulo_de_Apache_:_Mod_Python)
        *   [2.1.1 Instalar paquete](#Instalar_paquete)
        *   [2.1.2 Configurar Apache](#Configurar_Apache)
        *   [2.1.3 Probando Mod_python](#Probando_Mod_python)
*   [3 Enlaces externos](#Enlaces_externos)

## Introducción

Mod_python es un módulo de [Apache](/index.php/Apache "Apache") que integra el interprete de [Python](http://www.python.org) dentro del servidor. Con mod_python tú puedes escribir aplicaciones web basadas en Python que se ejecutarán mucho mas rápido que el tradicional CGI y tendrá acceso a avanzadas características tales como la capacidad de mantener conexiones con la base de datos y otros datos entre los acccesos y los acessos de Apache internos. Una descripción más detallada acerca de que es mod_python puede ser encontrada en este [artículo O'Reilly](http://www.onlamp.com/pub/a/python/2003/10/02/mod_python.html).

## Instalación

### Módulo de Apache : Mod_Python

Este documento describe como configurar y probar el modulo de Apache mod_python en un sistema Archlinux.

#### Instalar paquete

```
$ yaourt -Sy mod_python

```

#### Configurar Apache

*   Añade esta linea a `/etc/httpd/conf/httpd.conf`:

```
LoadModule python_module modules/mod_python.so

```

*   Reinicia Apache

```
# httpd -k restart

```

*   Asegúrate de que Apache haya cargado correctamente

#### Probando Mod_python

*   Añade estas líneas a `/etc/httpd/conf/httpd.conf`:

```
<Directory /srv/httpd/> 
   AddHandler mod_python .py
   PythonHandler mod_python.publisher 
   PythonDebug On 
</Directory>

```

*   Crea un archivo en `/srv/httpd/` llamado `mptest.py` y añade este contenido:

```
from mod_python import apache
def handler(req):
    req.content_type = 'text/plain'
    req.send_http_header()
    req.write("Hola mundo!")
    return apache.OK

```

*   Reinicia Apache

```
# sudo apachectl restart

```

*   Revisa que el Apache haya cargado correctamente

*   Ingresa a `[http://tusitio.com/mptest.py/handler](http://tusitio.com/mptest.py/handler)` y debería verse un sitio que diga solo:

```
Hola mundo!

```

## Enlaces externos

*   [Gentoo Wiki Mod_Python](http://gentoo-wiki.com/Apache_Modules_mod_python)
*   [mod_python Tutorial](http://webpython.codepoint.net/mod_python)
*   [http://www.modpython.org/](http://www.modpython.org/)
*   [mod_python manual](http://www.modpython.org/live/current/doc-html/)