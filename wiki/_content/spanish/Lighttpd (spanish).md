Este documento te describirá como configurar Ruby on Rails y PHP en un servidor lighttpd (a través de fastcgi).

## Contents

*   [1 Instalando lighttpd and fcgi](#Instalando_lighttpd_and_fcgi)
*   [2 Instalando php-cgi](#Instalando_php-cgi)
*   [3 Ruby on Rails](#Ruby_on_Rails)
*   [4 Configuración de /etc/lighttpd/lighttpd.conf](#Configuraci.C3.B3n_de_.2Fetc.2Flighttpd.2Flighttpd.conf)
*   [5 Links de Referencia](#Links_de_Referencia)

#### Instalando lighttpd and fcgi

```
pacman -S lighttpd fcgi

```

Ahora ya tienes lighttpd con soporte para fcgi. Si esto era todo lo que querias, listo, pero los que quieran tener Ruby on Rails y/o PHP deberian continuar.

#### Instalando php-cgi

```
pacman -S php php-cgi

```

Ahora revisa la versión de php-cgi escribiendo *php-cgi --version*

```
PHP 5.2.5 with Suhosin-Patch 0.9.6.2 (cgi-fcgi) (built: Nov 13 2007 20:03:00)
Copyright (c) 1997-2007 The PHP Group
Zend Engine v2.2.0, Copyright (c) 1998-2007 Zend Technologies

```

Si tienes una salida similar a esa quiere decir que PHP fue instalado correctamente

**Note** : Por favor mantén en cuenta que si recibes errores del tipo *No input file found* luego de intentar accesar a tus arhivos php entonces asegurate de que /etc/php/php.ini tenga las directivas habilitadas

```
cgi.fix_pathinfo=1
open_basedir = /home/:/tmp/:/usr/share/pear/:/another/path:/second/path

```

#### Ruby on Rails

Considerando que también quieras usar Ruby on Rails, asumo que tu tienes ruby instalado, sino hazlo de la siguiente forma:

```
pacman -S ruby

```

Ahora necesitamos rubygems y ruby-fcgi. Revisa en AUR!.

Rubygems:

```
pacman -S rubygems

```

ruby-fcgi:

Si usas [yaourt](http://archlinux.fr/yaourt-en/) puedes hacer:

```
yaourt -S ruby-fcgi

```

En caso de que no uses yaourt ni ninguna herramienta para AUR:

```
wget [https://aur.archlinux.org/packages/ruby-fcgi/ruby-fcgi/PKGBUILD](https://aur.archlinux.org/packages/ruby-fcgi/ruby-fcgi/PKGBUILD)
makepkg
pacman -U ruby-fcgi-*.pkg.tar.gz

```

Si todo salió bien deberiamos tener rubygems. Ahora vamos con rails!

```
gem install rails --include-dependencies
gem install fcgi --include-dependencies

```

Si esto falla, descarga [fcgi](http://fastcgi.com/dist/fcgi.tar.gz) y compílalo por ti mismo, de la siguiente forma.

```
$ wget http://fastcgi.com/dist/fcgi.tar.gz
$ tar zxvf fcgi.tar.gz
$ cd fcgi-2.4.0
$./configure
$ make
# make install

```

Y repite la instalación de gem.

Recuerda verificar si tienes mas de un fcgi.so de la siguiente forma:

```
find /usr -name fcgi.so

```

Si tienes dos o mas, borra el que no tiene "/site_ruby/" en el path.

Para documentación de como usar Ruby on Rails por favor consulta [http://rubyonrails.org](http://rubyonrails.org).

#### Configuración de /etc/lighttpd/lighttpd.conf

Solo voy a mostrar todo lo que debes cambiar. La configuración está bien comentada y la documentación oficial está en [http://lighttpd.net](http://lighttpd.net)

```
server.modules = (
"mod_access",
"mod_fastcgi",
"mod_accesslog" )

server.indexfiles = ( "dispatch.fcgi", "index.php" ) #dispatch.fcgi is rails specified

server.error-handler-404   = "/dispatch.fcgi" #too

fastcgi.server = (
".fcgi" =>
  ( "localhost" =>
    (
      "socket" => "/tmp/rails-fastcgi.socket",
      "bin-path" => "/path/to/rails/application/public/dispatch.fcgi"
    )
  ),
".php" =>
  ( "localhost" =>
    (
      "socket" => "/tmp/php-fastcgi.socket",
      "bin-path" => "/usr/bin/php-cgi"
    )
  )
)

```

Antes de encender el servicio, para asegurarnos que todo este completamente funcional, asegurate de crear el directorio /var/run/lighttpd y configurar el acceso de forma acorde. La instalación de Lighttpd no lo crea automaticamente.

#### Links de Referencia

[Lighttpd FAQ](http://trac.lighttpd.net/trac/wiki/FrequentlyAskedQuestions)