## Contents

*   [1 Pre-Instalación](#Pre-Instalaci.C3.B3n)
*   [2 Instalación](#Instalaci.C3.B3n)
*   [3 Configuración](#Configuraci.C3.B3n)
    *   [3.1 Añadir contraseña de blowfish_secret](#A.C3.B1adir_contrase.C3.B1a_de_blowfish_secret)
*   [4 Accediendo a tu instalación de phpMyAdmin](#Accediendo_a_tu_instalaci.C3.B3n_de_phpMyAdmin)
*   [5 Configuración de Lighttpd](#Configuraci.C3.B3n_de_Lighttpd)
*   [6 Configuración de NGINX](#Configuraci.C3.B3n_de_NGINX)
*   [7 Otra información (Antigua)](#Otra_informaci.C3.B3n_.28Antigua.29)

## Pre-Instalación

Revisa [LAMP](/index.php/LAMP "LAMP") Para instalar y configurar Apache, MySQL, and PHP.

## Instalación

Para instalar [phpMyAdmin](http://www.phpmyadmin.net/), instala los paquetes _phpmyadmin_ y _php-mcrypt_ con

```
pacman -S phpmyadmin php-mcrypt

```

## Configuración

Asegurate que que no tienes una copia antigua de phpMyAdmin.

```
rm -r /srv/http/phpMyAdmin

```

Copia el archivo de configuracion de ejemplo a tu diretorio de configuración de httpd

```
cp /etc/webapps/phpmyadmin/apache.example.conf /etc/httpd/conf/extra/httpd-phpmyadmin.conf

```

Añade las siguientes líneas a `/etc/httpd/conf/httpd.conf`:

```
# Configuracion de phpMyAdmin
Include conf/extra/httpd-phpmyadmin.conf

```

Puedes ingresar esto en la terminal y obtendrás el mismo efecto:

```
echo -e "\nInclude conf/extra/httpd-phpmyadmin.conf" >> /etc/httpd/conf/httpd.conf

```

En el archivo `/usr/share/webapps/phpMyAdmin/.htaccess`, comenta _deny from all_. La línea se debería ver como esto:

```
#deny from all

```

De lo contrario obtendrás un error similar a "Error 403 - Access forbidden!" cuando intentes acceder a tu instalación de phpMyAdmin.

Tu `/etc/httpd/conf/extra/httpd-phpmyadmin.conf` debería tener la siguiente información:

```
        Alias /phpmyadmin "/usr/share/webapps/phpMyAdmin"
        <Directory "/usr/share/webapps/phpMyAdmin">
                AllowOverride All
                Options FollowSymlinks
                Order allow,deny
                Allow from all
        </Directory>

```

Abre tu `/etc/php/php.ini` y ve a la línea que contiene _open_basedir_ y añade la ruta(s) a tu instalación de phpMyAdmin algo como lo siguiente:

```
:/usr/share/webapps/:/etc/webapps

```

Por ejemplo el mio contiene lo siguiente:

```
open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/:/srv/:/usr/share/webapps/:/etc/webapps/

```

También necesitas los módulos mcrypt y mysql, entonces descomenta en `/etc/php/php.ini`:

```
 ;extension=mcrypt.so
 ;extension=mysql.so

```

	a

```
 extension=mcrypt.so
 extension=mysql.so

```

### Añadir contraseña de blowfish_secret

Sí Tú ves el siguiente mensaje de error en la parte superior de la página cuando intentas loguearte por primera vez en /phpmyadmin (Usando un usuario y contraseña previamente configurado en MySql):

```
ERROR: The configuration file now needs a secret passphrase (blowfish_secret)

```

Tú necesitas añadir una contraseña de blowfish a el archivo de configuración de phpMyAdmin. Edita `/etc/webapps/phpmyadmin/config.inc.php` e inserta una contraseña aleatoria para blowfissh en la línea

```
$cfg['blowfish_secret'] = _; /* YOU MUST FILL IN THIS FOR COOKIE AUTH! */_

```

e [aquí](http://www.question-defense.com/tools/phpmyadmin-blowfish-secret-generator) para obetener un blowfish_secret muy bien generado y pégalo entre las comillas _. Ahora se debería ver algo como esto:_

```
$cfg['blowfish_secret'] = 'qtdRoGmbc9{8IZr323xYcSN]0s)r$9b_JUnb{~Xz'; /* YOU MUST FILL IN THIS FOR COOKIE AUTH! */

```

El errpr debería desaparecer cuando recargues la página de phpMyAdmin.

## Accediendo a tu instalación de phpMyAdmin

Finalmente tu instalación de phpMyAdmin está terminada. Antes de empezar a usarla necesitas reiniciar tu servidor apache con el siguiente comando:

```
# /etc/rc.d/httpd restart

```

Ya puedes acceder a tu instalación de phpMyAdmin usando la siguiente url:

```
http://localhost/phpmyadmin/
or
http://localhost/phpmyadmin/index.php

```

Not: 'localhost' en el nombre de host configurado en tu archivo /etc/rc.conf .

Sí tu quieres acceder usando:

```
http://localhost/phpmyadmin

```

cambia en '/etc/httpd/conf/extra/httpd-phpmyadmin.conf':

```
Alias /phpmyadmin/ "/usr/share/webapps/phpMyAdmin/"

```

a

```
Alias /phpmyadmin "/usr/share/webapps/phpMyAdmin"

```

Deberías también leer [este hilo](https://bbs.archlinux.org/viewtopic.php?pid=632500).

Si obtienes el siguiente error "#2002 - The server is not responding (or the local MySQL server's socket is not correctly configured)" entonces puede que desees cambiar "localhost" en /etc/webapps/phpmyadmin/config.inc.php en la siguiente línea:

```
$cfg['Servers'][$i]['host'] = 'localhost';

```

A tu hostname especificado en /etc/hosts y /etc/rc.conf bajo HOSTNAME.

Sí quisieras usar el script de configuración de phpMyAdmin ejecutando [http://localhost/phpmyadmin/setup](http://localhost/phpmyadmin/setup) necesitarás crear un directorio de configuración que sea escribible por httpd en /usr/share/webapps/phpmyadmin como lo siguiente:

```
cd /usr/share/webapps/phpMyAdmin
sudo mkdir config
sudo chgrp http config
sudo chmod g+w config

```

## Configuración de Lighttpd

La configuracíon de php para lighttpd es exactamente la misma que para apache. Has un alias para phpmyadmin en tu configuración de lighttpd.

```
 alias.url = ( "/phpmyadmin/" => "/usr/share/webapps/phpMyAdmin/")

```

Luego habilita mod_alias, mod_fastcgi and mod_cgi en tu configuración( sección server.modules )

Actualiza open_basedir en /etc/php/php.ini y añade "/usr/share/webapps/".

```
 open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/:/usr/share/webapps/

```

Asegúrate que lighttpd está configurada para servir archivos php.

[Lighttpd y FastCGI](/index.php?title=Lighttpd_y_FastCGI&action=edit&redlink=1 "Lighttpd y FastCGI (page does not exist)")

Reinicia lighttpd y navega a [http://localhost/phpmyadmin/index.php](http://localhost/phpmyadmin/index.php)

## Configuración de NGINX

También similar a la configuración de Apache.

Crea un enlace simbólico a el directorio /usr/share/webapps/phpmyadmin desde cualquier directorio desque que tu host virtual este sirviendo archivos, p.e. /srv/http/<domain>/public_html/

```
 sudo ln -s /usr/share/webapps/phpmyadmin /srv/http/<domain>/public_html/phpmyadmin

```

También puedes configurar un subdominio con un servidor con unas líneas como estas(Si estás usando php-fpm):

```
 server {
         server_name     phpmyadmin.<domain.tld>;
         access_log      /srv/http/<domain>/logs/phpmyadmin.access.log;
         error_log       /srv/http/<domain.tld>/logs/phpmyadmin.error.log;

         location / {
                 root    /srv/http/<domain.tld>/public_html/phpmyadmin;
                 index   index.html index.htm index.php;
         }

         location ~ \.php$ {
                 root            /srv/http/<domain.tld>/public_html/phpmyadmin;
                 fastcgi_pass    unix:/var/run/php-fpm/php-fpm.sock;
                 fastcgi_index   index.php;
                 fastcgi_param   SCRIPT_FILENAME  /srv/http/<domain.tld>/public_html/phpmyadmin/$fastcgi_script_name;
                 include         fastcgi_params;
         }
 }

```

Posiblemente encuentres algunos problemas con phpMyadmin que dicen "The Configuration File Now Needs A Secret Passphrase" y no muestra lo que escribes, el error es aún mostrado. Intenta cambiando el propietario de los archivos por el usuario o grupo especificado por NGINX, p.r. nginx...

```
 cd /usr/share/webapps/phpmyadmin
 sudo chown -R nginx:nginx *

```

Mientras ingresas cualquier cosa para la contraseña de blowfish, tal vez desees una clave generada aleatoriamente (Pos razones de seguridad). Aqui esta una herramienta muy útil que hará esto por ti.[[1]](http://www.question-defense.com/tools/phpmyadmin-blowfish-secret-generator).

## Otra información (Antigua)

Esta página tiene un ejemplo del archivo 'config.inc.php' que tu necesitas poner en el directorio de phpMyAdmin que inmediatamente emìeza a funcionar

**Cosas que deberías hacer primero**

Crea un 'controuser', de tal manera que phpMyAdmin pueda leer de la base de datos principal de mysql.

```
mysql -u root -pYOURROOTPASSWORD
mysql> grant usage on mysql.* to controluser@localhost identified by 'CONTROLPASS';

```

**Donde está phpmyadmin**

En phpMyAdmin 3.2.2-3 el archivo falta el archivo /srv/http/ crea este link simbólico

```
ln -s /usr/share/webapps/phpMyAdmin/ /srv/http/phpmyadmin

```

**Cosas que deberías configurar**

controluser se establece en controluser
controlpass está configurada como password
verbose ise establece name_of_server

**Sample 'config.inc.php' file**

```
<?php
/*
 * Generated configuration file
 * Generated by: phpMyAdmin 2.11.8.1 setup script by Michal Čihař <michal@cihar.com>
 * Version: $Id: setup.php 11423 2008-07-24 17:26:05Z lem9 $
 * Date: Mon, 01 Sep 2008 20:34:02 GMT
 */

/* Servers configuration */
$i = 0;

/* Server ravi-test-mysql (http) [1] */
$i++;
$cfg['Servers'][$i]['host'] = 'localhost';
$cfg['Servers'][$i]['extension'] = 'mysql';
$cfg['Servers'][$i]['port'] = '3306';
$cfg['Servers'][$i]['connect_type'] = 'tcp';
$cfg['Servers'][$i]['compress'] = false;
$cfg['Servers'][$i]['controluser'] = 'controluser';
$cfg['Servers'][$i]['controlpass'] = 'password';
$cfg['Servers'][$i]['auth_type'] = 'http';
$cfg['Servers'][$i]['verbose'] = 'name_of_server';

/* End of servers configuration */

$cfg['LeftFrameLight'] = true;
$cfg['LeftFrameDBTree'] = true;
$cfg['LeftFrameDBSeparator'] = '_';
$cfg['LeftFrameTableSeparator'] = '__';
$cfg['LeftFrameTableLevel'] = 1;
$cfg['LeftDisplayLogo'] = true;
$cfg['LeftDisplayServers'] = false;
$cfg['DisplayServersList'] = false;
$cfg['DisplayDatabasesList'] = 'auto';
$cfg['LeftPointerEnable'] = true;
$cfg['DefaultTabServer'] = 'main.php';
$cfg['DefaultTabDatabase'] = 'db_structure.php';
$cfg['DefaultTabTable'] = 'tbl_structure.php';
$cfg['LightTabs'] = false;
$cfg['ErrorIconic'] = true;
$cfg['MainPageIconic'] = true;
$cfg['ReplaceHelpImg'] = true;
$cfg['NavigationBarIconic'] = 'both';
$cfg['PropertiesIconic'] = 'both';
$cfg['BrowsePointerEnable'] = true;
$cfg['BrowseMarkerEnable'] = true;
$cfg['ModifyDeleteAtRight'] = false;
$cfg['ModifyDeleteAtLeft'] = true;
$cfg['RepeatCells'] = 100;
$cfg['DefaultDisplay'] = 'horizontal';
$cfg['TextareaCols'] = 40;
$cfg['TextareaRows'] = 7;
$cfg['LongtextDoubleTextarea'] = true;
$cfg['TextareaAutoSelect'] = false;
$cfg['CharEditing'] = 'input';
$cfg['CharTextareaCols'] = 40;
$cfg['CharTextareaRows'] = 2;
$cfg['CtrlArrowsMoving'] = true;
$cfg['DefaultPropDisplay'] = 'horizontal';
$cfg['InsertRows'] = 2;
$cfg['EditInWindow'] = true;
$cfg['QueryWindowHeight'] = 310;
$cfg['QueryWindowWidth'] = 550;
$cfg['QueryWindowDefTab'] = 'sql';
$cfg['ForceSSL'] = false;
$cfg['ShowPhpInfo'] = false;
$cfg['ShowChgPassword'] = false;
$cfg['AllowArbitraryServer'] = false;
$cfg['LoginCookieRecall'] = 'something';
$cfg['LoginCookieValidity'] = 1800;
?>

```