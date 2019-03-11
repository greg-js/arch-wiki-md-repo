**Estado de la traducción**
Este artículo es una traducción de [Drupal](/index.php/Drupal "Drupal"), revisada por última vez el **2019-01-02**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Drupal&diff=0&oldid=548112) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [LAMP](/index.php/LAMP_(Espa%C3%B1ol) "LAMP (Español)")
*   [LAPP](/index.php/LAPP "LAPP")
*   [LASP](/index.php/LASP "LASP")
*   [MySQL](/index.php/MySQL_(Espa%C3%B1ol) "MySQL (Español)")
*   [PostgreSQL](/index.php/PostgreSQL "PostgreSQL")
*   [SQLite](/index.php/SQLite "SQLite")
*   [Sendmail](/index.php/Sendmail "Sendmail")
*   [Postfix](/index.php/Postfix_(Espa%C3%B1ol) "Postfix (Español)")
*   [Exim](/index.php/Exim "Exim")

De [Wikipedia](https://en.wikipedia.org/wiki/es:Drupal "wikipedia:es:Drupal"):

	*Drupal (pronunciación IPA en inglés: [druː pʰʊɫ]) es un sistema de gestión de contenidos1 o CMS (por sus siglas en inglés, Content Management System) libre, modular, multipropósito y muy configurable que permite publicar artículos, imágenes, archivos y que también ofrece la posibilidad de otros servicios añadidos como foros, encuestas, votaciones, blogs, administración de usuarios y permisos.*

	*[...]*

	*Es un programa libre, con licencia GNU/GPL, escrito en PHP, combinable con MySQL, desarrollado y mantenido por una activa comunidad de usuarios. Destaca por la calidad de su código y de las páginas generadas, el respeto de los estándares de la web, y un énfasis especial en la usabilidad y consistencia de todo el sistema.*

Este artículo describe cómo configurar Drupal y [Apache](/index.php/Apache_HTTP_Server_(Espa%C3%B1ol) "Apache HTTP Server (Español)"), [MySQL](/index.php/MySQL_(Espa%C3%B1ol) "MySQL (Español)") o [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), [PHP](/index.php/PHP_(Espa%C3%B1ol) "PHP (Español)") y [Postfix](/index.php/Postfix_(Espa%C3%B1ol) "Postfix (Español)") para trabajar con él. Se da por hecho que tiene algún tipo de servidor [LAMP](/index.php/LAMP_(Espa%C3%B1ol) "LAMP (Español)") (Linux, Apache, MySQL, PHP), LAPP (Linux, Apache, PostgreSQL, PHP) o LASP (Linux, Apache, SQLite, PHP) ya configurado.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 PHP](#PHP)
    *   [2.2 Apache](#Apache)
    *   [2.3 Drupal](#Drupal)
*   [3 Herramientas de la línea de comandos](#Herramientas_de_la_línea_de_comandos)
    *   [3.1 Drush](#Drush)
    *   [3.2 Drupalconsole](#Drupalconsole)
    *   [3.3 PHP-Codesniffer-Drupal](#PHP-Codesniffer-Drupal)
*   [4 Consejos y trucos](#Consejos_y_trucos)
    *   [4.1 Enviar correos](#Enviar_correos)
    *   [4.2 Programación con Cron](#Programación_con_Cron)
    *   [4.3 El progreso de la subida no está habilitado](#El_progreso_de_la_subida_no_está_habilitado)
*   [5 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [drupal](https://www.archlinux.org/packages/?name=drupal).

## Configuración

### PHP

Edite `/etc/php/php.ini`:

*   Para habilitar el soporte para la manipulación de imágenes, descomente la línea `extension=gd`

Para el soporte de bases de datos, habilite una extensión PDO para su base de datos

*   Para habilitar el soporte para [SQLite](/index.php/SQLite "SQLite"), descomente la línea `extension=pdo_sqlite`
*   Para habilitar el soporte para [MySQL](/index.php/MySQL_(Espa%C3%B1ol) "MySQL (Español)"), descomente la línea `extension=pdo_mysql`
*   Para habilitar el soporte para [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), descomente la línea `extension=pdo_pgsql`

Apache fallará al intentar iniciarse y mostrará un error al encontrar *php_admin_value*. A continuación se detalla la solución a este problema:

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [php-apache](https://www.archlinux.org/packages/?name=php-apache).

En `/etc/httpd/conf/httpd.conf`, comente la línea:

```
#LoadModule mpm_event_module modules/mod_mpm_event.so

```

y descomente la línea:

```
LoadModule mpm_prefork_module modules/mod_mpm_prefork.so

```

Coloque esto al final de la lista `LoadModule`:

```
LoadModule php7_module modules/libphp7.so
AddHandler php7-script .php

```

Coloque esto al final de la lista `Include`:

```
Include conf/extra/php7_module.conf

```

Reinicie `httpd.service` usando [systemd](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)").

Apache fallará al intentar iniciarse y mostrará un error al encontrar *open_basedir*. A continuación se detalla la solución a este problema:

En `/etc/php/php.ini`, descomente y añada el sufijo `open_basedir` para que tenga este aspecto:

```
open_basedir = /etc/webapps

```

### Apache

Copie el ejemplo del archivo de configuración de Apache:

```
# cp /etc/webapps/drupal/apache.example.conf /etc/httpd/conf/extra/drupal.conf

```

E inclúyalo en la parte inferior de `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/drupal.conf

```

En `/etc/httpd/conf/httpd.conf`, descomente también la línea `LoadModule rewrite_module modules/mod_rewrite.so`.

### Drupal

Edite `/usr/share/webapps/drupal/.htaccess` y reemplace `Require all denied` por `Require all granted`.

Finalmente, [reinicie](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") Apache (`httpd.service`). Ahora puede acceder a la instalación de Drupal en [http://localhost/drupal](http://localhost/drupal) .

## Herramientas de la línea de comandos

### Drush

[Drush](http://www.drush.org/) es un shell de línea de comandos y una interfaz de scripting Unix para Drupal. El núcleo Drush se suministra con una gran cantidad de comandos útiles para interactuar con el código, como módulos/temas/perfiles. Del mismo modo, ejecuta update.php, ejecuta consultas de sql y migraciones de base de datos, y otras utilidades como ejecutar Cron o borrar la caché. Drush se puede ampliar por archivos de comandos de terceros. Se puede instalar con el paquete [drush](https://aur.archlinux.org/packages/drush/).

### Drupalconsole

[Drupalconsole](https://drupalconsole.com/) es una herramienta CLI para generar código cliché, interactuar y depurar Drupal 8. Se puede instalar con el paquete [drupalconsole](https://aur.archlinux.org/packages/drupalconsole/).

### PHP-Codesniffer-Drupal

[PHP-Codesniffer-Drupal](https://www.drupal.org/project/coder) revisa su código Drupal contra los estándares de codificación y otras mejores prácticas. Se puede instalar con el paquete [php-codesniffer-drupal](https://aur.archlinux.org/packages/php-codesniffer-drupal/).

## Consejos y trucos

### Enviar correos

Drupal necesita un MTA compatible con Sendmail como por ejemplo [Sendmail](/index.php/Sendmail "Sendmail"), [Postfix](/index.php/Postfix_(Espa%C3%B1ol) "Postfix (Español)") o [Exim](/index.php/Exim "Exim") si planea enviar correos desde su configuración local. Alternativamente, existen múltiples soluciones para enviar correos mediante servidores de correo externos a través de SMTP u otros medios como [SMTP](https://drupal.org/project/smtp) o [PHPMailer](https://drupal.org/project/phpmailer). Utilice la [página de búsqueda](https://www.drupal.org/search/site/mail) para encontrar más posibilidades.

### Programación con Cron

Drupal recomienda ejecutar los trabajos Cron a cada hora. Cron puede ejecutarse desde el navegador web visitando [http://localhost/drupal/cron](http://localhost/drupal/cron). También es posible ejecutar Cron a través de un script copiando el archivo apropiado de la carpeta "scripts" a `/etc/cron.hourly` y haciéndolo ejecutable.

### El progreso de la subida no está habilitado

Tras una correcta instalación, podría ver el siguiente mensaje en el informe de estado:

 `Your server is capable of displaying file upload progress, but does not have the required libraries. It is recommended to install the PECL uploadprogress library (preferred) or to install APC.` 

Primero, instale el paquete [php-pear](https://aur.archlinux.org/packages/php-pear/). A continuación, utilize la orden **pecl** para descargar, compilar e instalar automáticamente la librería:

```
# pecl install uploadprogress

```

Finalmente, agregue lo siguiente a `/etc/php/php.ini`

```
extension=uploadprogress

```

Reinicie Apache.

## Véase también

*   [Documentación oficial de Drupal](http://drupal.org/handbook)
*   [Guía simple para instalar Drupal en Xampp](http://drupal.org/node/307956)