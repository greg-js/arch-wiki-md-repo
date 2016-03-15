[LAMP](https://en.wikipedia.org/wiki/LAMP "wikipedia:LAMP"), es el acrónimo para referirse a un conjunto de software, utilizado para ejecutar sitios web dinámicos o servicios.

*   **L**inux refiriendose al sistema operativo, en este caso Arch Linux claro;
*   **A**pache, el servidor Web;
*   **M**ySQL/**M**ariaDB, el sistema administrador de base de datos;
*   **P**HP u otros, p.e. Perl, Python.

## Contents

*   [1 Apache, PHP, y MySQL](#Apache.2C_PHP.2C_y_MySQL)
    *   [1.1 Instalar Paquetes](#Instalar_Paquetes)
    *   [1.2 Configurar Apache](#Configurar_Apache)
        *   [1.2.1 Opciones adicionales](#Opciones_adicionales)
    *   [1.3 Configurar PHP](#Configurar_PHP)
    *   [1.4 Configurar el soporte para MySQL](#Configurar_el_soporte_para_MySQL)
    *   [1.5 Configurar PHPMyAdmin](#Configurar_PHPMyAdmin)

### Apache, PHP, y MySQL

Este documento describe como configurar el servidor web Apache en un sistema Arch Linux. Además explica como, opcionalmente, instalar PHP y [MariaDB](/index.php/MariaDB "MariaDB") e integrarlos con Apache.

#### Instalar Paquetes

Si lo desea, puede instalar Apache/PHP/MySQL por separado. Este documento asume que instalará los tres, pero si lo desea, puede realizar cualquiera de las secciones que apliquen al software instalado.

```
# pacman -S apache php php-apache mariadb

```

#### Configurar Apache

*   Añada la siguiente línea a `/etc/hosts` (Si el archivo no existe deberá crearlo)

```
127.0.0.1  localhost.localdomain   localhost

```

**Note:** Si desea un hostname diferente, añádalo al final de la línea:

```
127.0.0.1  localhost.localdomain   localhost myhostname

```

*   Edite `/etc/rc.conf`. Si define un hostname en el paso anterior,

la variable HOSTNAME debe ser igual. Si no, deje solamente "localhost":

```
#
# Networking
#
HOSTNAME="localhost"

```

*   Comentar un modulo en el archivo de configuración de Apache

```
# nano /etc/httpd/conf/httpd.conf

```

```
LoadModule unique_id_module        modules/mod_unique_id.so

```

en

```
#LoadModule unique_id_module        modules/mod_unique_id.so

```

*   Ejecute en una terminal (como root):

```
# /etc/rc.d/httpd start

```

*   Apache debería ahora estar corriendo. Verifíquelo visitando [http://localhost/](http://localhost/) en un navegador web. Debería ver una página simple página de prueba de Apache.

*   Edite `/etc/rc.conf` (para iniciar Apache en el arranque):

```
DAEMONS=(... varios daemons ... httpd

```

**O** añada esta línea a `rc.local`:

```
/etc/rc.d/httpd start

```

*   Si quiere activar los directorios de usuario (p.e. `~/public_html` en la máquina es accesible como [http://localhost/~usuario/](http://localhost/~usuario/)) para estar disponibles en la web, descomente las siguientes líneas en `/etc/httpd/conf/extra/httpd-userdir.conf`:

```
UserDir public_html

```

y

```
<Directory /home/*/public_html>
  AllowOverride FileInfo AuthConfig Limit Indexes
  Options MultiViews Indexes SymLinksIfOwnerMatch ExecCGI
  <Limit GET POST OPTIONS PROPFIND>
    Order allow,deny
    Allow from all
  </Limit>
  <LimitExcept GET POST OPTIONS PROPFIND>      Order deny,allow
    Deny from all
  </LimitExcept>
</Directory>

```

Asegúrese de que Apache pueda ingresar al directorio home del usuario colocando los permisos correspondientes. El directorio del usuario y el directorio `~/public_html/` debe ser ejecutable para los otros ("el resto del mundo"). Esto sería suficiente:

```
$ chmod o+x ~
$ chmod o+x ~/public_html

```

Existen algunas otras formas, más seguras de colocar los permisos mediante la creación de un grupo especial y permitiendo sólo al usuario Apache y otros requeridos entrar ahí... Dependiendo del nivel paranoico que se tenga.

##### Opciones adicionales

Estas opciones en `/etc/httpd/conf/httpd.conf` pueden ser de interés:

El puerto que Apache utiliza para escuchar peticiones. Para el acceso a internet con router, se debe redireccinar a ese puerto.

```
# Listen 80

```

Este es el correo electrónico del administrador que puede ser encontrado en las páginas de error por ejemplo.

```
# ServerAdmin sample@sample.com

```

Este es el directorio donde se podrían colocar las páginas web.

```
# DocumentRoot "/home/httpd/html"

```

Si se cambia el directorio raíz (DocumentRoot) no se debe olvidar cambiar el siguiente elemento.

```
# <Directory "/home/httpd/html">

```

#### Configurar PHP

PHP ahora esta disponible prácticamente después de instalarlo.

*   Descomente esta línea en `/etc/httpd/conf/httpd.conf`

```
#LoadModule php5_module modules/libphp5.so

```

*   Para PHP5 los archivos manejadores ya están configurados

```
#
# DirectoryIndex: sets the file that Apache will serve if a directory
# is requested.
#
<IfModule dir_module>
    <IfModule mod_php5.c>
        DirectoryIndex index.php index.html
        AddType application/x-httpd-php .php
        AddType application/x-httpd-php-source .phps
    </IfModule>
    DirectoryIndex index.html
</IfModule>

```

*   Recordad agregar un archivo manejador para .phtml si es necesario:

```
DirectoryIndex index.php index.phtml index.html

```

*   Si se desea el módulo libGD, edite `/etc/php/php.ini` y descomente la siguiente línea (*quitando el ;*):

```
;extension=gd.so

```

*   Si el DocumentRoot está fuera de `/home/`, agergarlo

en la variable `open_basedir</open> en el archivo <code>/etc/php/php.ini` como:

```
open_basedir = /home/:/tmp/:/usr/share/pear/:/ruta/al/documentroot

```

*   Reinicie el servidor Apache para que los cambios tengan efecto (como root):

```
# /etc/rc.d/httpd restart

```

*   Pruebe PHP con un simple, pero muy informativo script:

```
<html>
<head>
  <title>Este es Arch Linux, ejecutando PHP.</title>
</head>
<body>

```

<?php phpinfo(); ?>

```
</body>
</html>

```

Guarde este archivo como `test.php` y copielo en `/srv/http/html/` o en `~/public_html` si lo permitió en la configuración.

*   Pruebe PHP en [http://localhost/test.php](http://localhost/test.php) o en [http://localhost/~usuario/test.php](http://localhost/~usuario/test.php)

**Si continua teniendo problemas**, edite su archivo /etc/httpd/conf/httpd.conf con la siguiente información

*   Edite su archivo httpd.conf

```
nano /etc/httpd/conf/httpd.conf

```

*   Bajo <IfModule mime_module>

```
AddType application/x-httpd-php .php
AddType application/x-httpd-php-source .phps

```

*   Reinicie Apache

```
# /etc/rc.d/httpd restart

```

Si después de esto el servidor no le ejecuta los scripts php añada la línea

```
LoadModule php5_module modules/libphp5.so

```

Justo antes de empezar el bloque de LoadModule ......

*   Reinicie Apache

```
# /etc/rc.d/httpd restart

```

Asegúrese de probar de nuevo la página para verificar que funciona correctamnente (como se vio anteriormente)

#### Configurar el soporte para MySQL

Haga ésto sólo si quiere activar el soporte para MySQL. Configure previamente MySQL en los pasos descritos de [MySQL](/index.php/MySQL "MySQL")

*   Edite `/etc/php/php.ini` y descomente la siguiente línea (*quitando el ;*):

```
;extension=mysql.so
;extension=mysqli.so

```

*   Si no ha configurado una contraseña de root para MySQL (en una terminal, como root):

```
# mysqladmin -u root password 'roots_password'

```

*   Se pueden agregar usuarios con menos privilegios, para los scripts que desee ejecutar, editando las tablas que se encuentran en la base de datos `mysql`. Deberá reiniciar el servicio para que los cambios tomen efecto.

No olvide revisar la tabla `mysql/users`. Si existe una segunda entrada para el usuario root y el hostname se deja sin ninguna clave establecida, cualquier persona de su máquina probablemente podría ganar el acceso total. Tal vez deba revisar la siguiente sección para estas labores.

*   Si se obtienen el mensaje "`error no. 2013: Lost Connection to mysql server during query`" instantaneamente después de intentar conectarse al daemon de MySQL mediante TCP/IP. Esto es por el sistema TCP wrappers (tcpd), el cual utiliza el sistema `hosts_access(5)` para permitir (allow) o denegar (disallow) las conexiones.

Si se esta en este problema, asegurarse de agregar lo siguiente en el archivo `/etc/hosts.allow`:

```
# mysqld : ALL : ALLOW
# mysqld-max : ALL : ALLOW
# y similar para otros daemons de MySQL.

```

**Note:** Los ejemplos anteriores son un caso simplista, diciendole a tcpd que permita todas las conexiones desde cualquier lugar. Se debe utilizar una selección más apropiada de fuentes permitidas en lugar de **ALL**. Sólo asegurese que localhost y la dirección IP (númerica o de DNS) de la interáz por la cuál se realice la conexión este especificada.

*   Podría también ser necesario editar el archivo `/etc/my.cnf` y comentar la siguiente línea como sigue:

```
# skip-networking

```

#### Configurar PHPMyAdmin

Si se quiere utilizar [PHPMyAdmin](http://www.phpmyadmin.net), podría proceder de la siguiente manera:

*   Instale el paquete

```
# pacman -S phpmyadmin

```

*   Edite el archivo de configuración para adaptarlo a sus necesidades: `/home/httpd/html/phpMyAdmin/config.inc.php`

Inserte la cadena correspondiente a la variable PmaAbsoluteUri para que sea parecida a:

```
$cfg[['PmaAbsoluteUri']] = 'http://>hostname</phpMyAdmin/';

```

Rellene la información de su servidor MySQL. En PHPMyAdmin, se pueden definir multiples servidores en el arreglo 'Servers'. Para acceder a su base de datos MySQL, tiene que editar la primera entrada; puede ignorar las demás.

En un sistema normal sólo tendría que asignar el auth_type a http. Esto hace que PHPMyAdmin use el usuario y contraseñas ingresados por el navegador web para acceder al servidor de bases de datos, de esa manera, no se pueden realizar acciones que no estén permitidas para dicho usuario del servidor MySql.

```
$cfg[['Servers']][[$i]][['auth_type']]     = 'http';

```

**Advertencia:** otros métodos de autorización o el escribir contraseñas directamente en este archivo puede comprometer la seguridad de la base de datos. Por defecto, este archivo es legible para todo el mundo, por lo que es conveniente restringirlo.

*   Para usar PHPMyAdmin dirigir el navegador web a:

```
http://>hostname</phpMyAdmin/

```