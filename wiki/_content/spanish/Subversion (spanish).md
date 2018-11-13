**Estado de la traducción**
Este artículo es una traducción de [Subversion](/index.php/Subversion "Subversion"), revisada por última vez el **2018-10-22**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Subversion&diff=0&oldid=550193) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Apache Subversion](http://subversion.apache.org/features.html) es «un completo sistema de control de versiones originalmente diseñado para ser un mejor [CVS](/index.php/CVS "CVS"). Desde entonces, Subversion se ha expandido más allá de su objetivo original de reemplazar CVS, pero su modelo básico, diseño e interfaz siguen siendo fuertemente influenciados por ese objetivo».

Este artículo trata sobre la configuración de un servidor svn en su máquina. Hay dos servidores svn populares, el *vnserve* incorporado y la opción más avanzada, [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server") con complementos svn.

## Contents

*   [1 Configuración de Apache Subversion](#Configuración_de_Apache_Subversion)
    *   [1.1 Objetivos](#Objetivos)
    *   [1.2 Instalación](#Instalación)
    *   [1.3 Configuración de Subversion](#Configuración_de_Subversion)
        *   [1.3.1 Editar /etc/httpd/conf/httpd.conf](#Editar_/etc/httpd/conf/httpd.conf)
        *   [1.3.2 ¿SSL o no SSL?](#¿SSL_o_no_SSL?)
        *   [1.3.3 Crear /home/svn/.svn-policy-file](#Crear_/home/svn/.svn-policy-file)
        *   [1.3.4 Crear /home/svn/.svn-auth-file](#Crear_/home/svn/.svn-auth-file)
        *   [1.3.5 Crear un repositorio](#Crear_un_repositorio)
        *   [1.3.6 Establecer permisos](#Establecer_permisos)
    *   [1.4 Crear un proyecto](#Crear_un_proyecto)
        *   [1.4.1 Estructura de directorio para proyecto](#Estructura_de_directorio_para_proyecto)
        *   [1.4.2 Poblar el directorio](#Poblar_el_directorio)
        *   [1.4.3 Importar el proyecto](#Importar_el_proyecto)
        *   [1.4.4 Revisar prueba SVN](#Revisar_prueba_SVN)
*   [2 Configurar Svnserve](#Configurar_Svnserve)
    *   [2.1 Instalar el paquete](#Instalar_el_paquete)
    *   [2.2 Crear un repositorio](#Crear_un_repositorio_2)
    *   [2.3 Establecer políticas de acceso](#Establecer_políticas_de_acceso)
    *   [2.4 Iniciar el demonio del servidor](#Iniciar_el_demonio_del_servidor)
    *   [2.5 svn+ssh](#svn+ssh)
*   [3 Copia de seguridad y restauración de Subversion](#Copia_de_seguridad_y_restauración_de_Subversion)
*   [4 Clientes Subversion](#Clientes_Subversion)
*   [5 Véase también](#Véase_también)

## Configuración de Apache Subversion

### Objetivos

El objetivo de este ejemplo es configurar Subversion, con Apache. ¿Por qué usar Apache para Subversion? Bueno, sencillamente, proporciona características que el `svnserve` independiente no tiene...

*   Soporte HTTPS. Esto es más seguro que la autenticación MD5 utilizada por svnserve.
*   Controles de acceso de grano fino. Puede utilizar la autenticación de Apache para limitar los permisos por directorio. Esto significa que puede otorgar acceso de lectura a todo, pero solo puede confirmar el acceso al troncal, mientras que otro grupo tiene acceso de confirmación a etiquetas o sucursales.
*   Un visor de repositorio gratuito.
*   El equipo de Subversion está trabajando en la integración perfecta de WebDAV. En algún momento, debería poder utilizar cualquier interfaz WebDAV para actualizar los archivos en el repositorio.

### Instalación

Instale [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server") como se describe en su artículo.

Además de Apache, solo necesitará [instalar](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [subversion](https://www.archlinux.org/packages/?name=subversion).

### Configuración de Subversion

Cree un directorio para sus repositorios:

```
# mkdir -p /home/svn/repositories

```

#### Editar /etc/httpd/conf/httpd.conf

Asegúrese que lo siguiente esté listado... Si no, agréguelos (normalmente tendrá que agregar solo los dos últimos), deben estar en este orden:

```
LoadModule dav_module           modules/mod_dav.so
LoadModule dav_fs_module        modules/mod_dav_fs.so
LoadModule dav_svn_module       modules/mod_dav_svn.so
LoadModule authz_svn_module     modules/mod_authz_svn.so

```

#### ¿SSL o no SSL?

SSL para el acceso SVN tiene algunos beneficios, por ejemplo, le permite usar el Autotipo Básico de Apache, con poco temor a que alguien esté buscando contraseñas.

Genere el certificado:

```
# cd /etc/httpd/conf/
# openssl req -new -x509 -keyout server.key -out server.crt -days 365 -nodes

```

Agregue lo siguiente a `/etc/httpd/conf/extra/httpd-ssl.conf` (o a `/etc/httpd/conf/extra/httpd-vhosts.conf` Si no está utilizando ssl). Incluya lo siguiente dentro de una directiva de host virtual:

```
<Location /svn>
   DAV svn
   SVNParentPath /home/svn/repositories
   AuthzSVNAccessFile /home/svn/.svn-policy-file
   AuthName "SVN Repositories"
   AuthType Basic
   AuthUserFile /home/svn/.svn-auth-file
   Require valid-user
</Location>

```

Para asegurarse de que la configuración de SSL se cargue, elimine el comentario de la línea de configuración de SSL en `/etc/httpd/conf/httpd.conf` para que se vea así:

```
LoadModule ssl_module modules/mod_ssl.so
LoadModule socache_shmcb_module modules/mod_socache_shmcb.so
Include /etc/httpd/conf/extra/httpd-ssl.conf

```

#### Crear /home/svn/.svn-policy-file

```
[/]
* = r

[REPO_NAME:/]
USER_NAME = rw

```

El * en la sección / coincide con los usuarios anónimos. Cualquier acceso por encima y más allá de solo lectura se le pedirá un usuario/contraseña por apache AuthType Basic. La sección REPO_NAME:/ hereda los permisos de los anteriores, por lo que los usuarios no tienen permiso de solo lectura. El último bit otorga permiso de lectura/escritura del repositorio REPO_NAME al usuario USER_NAME.

#### Crear /home/svn/.svn-auth-file

Esto es un archivo htpasswd o htdigest. Utilice htpasswd. Nuevamente, debido a SSL, no debe preocuparse tanto por el rastreo de contraseñas. htdigest proporcionaría aún más seguridad en comparación con la inhalación, pero en este momento no lo necesita. Ejecute la siguiente orden.

```
# htpasswd -cs /home/svn/.svn-auth-file USER_NAME

```

Lo anterior crea el archivo (`-c`) y usa SHA-1 para almacenar la contraseña (`-s`). Se crea el usuario `USER_NAME`.

Para agregar usuarios adicionales, omita la marca (`-c`).

```
# htpasswd -s /home/svn/.svn-auth-file OTHER_USER_NAME

```

#### Crear un repositorio

```
# svnadmin create /home/svn/repositories/REPO_NAME

```

#### Establecer permisos

El usuario de Apache necesita permisos sobre el nuevo repositorio.

```
# chown -R http:http /home/svn/repositories/REPO_NAME

```

### Crear un proyecto

#### Estructura de directorio para proyecto

Cree un directorio temporal con la estructura de directorio `branches` `tags` `trunk` en su máquina de desarrollo.

```
$ mkdir -p ~/svn-import/{ramas, etiquetas, principal}

```

#### Poblar el directorio

Copie o mueva los archivos de origen de su proyecto al directorio principal creado.

```
$ cp -R /my/existing/project/* ~/svn-import/trunk

```

#### Importar el proyecto

```
$ svn import -m "Initial import" ~/svn-import [https://yourdomain.net/svn/REPO_NAME/](https://yourdomain.net/svn/REPO_NAME/)

```

#### Revisar prueba SVN

```
$ svn checkout [https://yourdomain.net/svn/REPO_NAME/](https://yourdomain.net/svn/REPO_NAME/) /my/svn/working/copy

```

Si todo funcionó, ahora debería tener una copia revisada y en funcionamiento de su repositorio SVN recién creado.

## Configurar Svnserve

### Instalar el paquete

Instale el paquete [subversion](https://www.archlinux.org/packages/?name=subversion).

### Crear un repositorio

Cree su repositorio

```
mkdir /path/to/repos/
svnadmin create /path/to/repos/repo1

```

Su repositorio inicial está vacío, si desea importar archivos en él, use la siguiente orden:

```
svn import ~/code/project1 file:///path/to/repos/repo1 --message 'Initial repository layout'

```

### Establecer políticas de acceso

Edite el archivo /path/to/repos/repo1/conf/svnserve.conf y elimine el comentario o agregue la línea debajo de [general]

```
password-db = passwd

```

Es posible que también desee cambiar la opción predeterminada para usuarios anónimos.

```
anon-access = read

```

Reemplace «read» con «write» para un repositorio en el que cualquiera pueda comprometerse, o configúrelo en «none» para deshabilitar todo el acceso anónimo.

Ahora edite el archivo /path/to/repos/repo1/conf/passwd

```
[users]
harry = foopassword
sally = barpassword

```

Lo anterior define a los usuarios harry y sally, con contraseñas foopassword y barpassword, cámbielas como desee.

### Iniciar el demonio del servidor

Antes de iniciar el servidor, edite el archivo de configuración:

 `/etc/conf.d/svnserve`  `SVNSERVE_ARGS="--root=/path/to/repos"` 

La opción `--root=/path/to/repos` establece la raíz del árbol del repositorio. Si tiene varios repositorios, use `--root=/path-to/reposparent`. Luego acceda a los repositorios independientes pasando el nombre del repositorio en la URL: `[svn://host/repo1](svn://host/repo1)`. asegúrese de que el usuario tenga acceso de lectura / escritura a los archivos del repositorio.

Opcionalmente, agregue un `--listen-port` si desea un puerto diferente u otras opciones.

Por defecto, el servicio se ejecuta como root. Si desea cambiar eso, agregue un drop-in:

 `/etc/systemd/system/svnserve.service.d/50-custom.conf` 
```
[Service]
User=svn
```

Ahora inicie *svnserve.service* [daemon](/index.php/Daemon "Daemon").

### svn+ssh

Para usar svn+ssh: //, tenemos que tener un contenedor escrito para svnserve.

Compruebe dónde se encuentran los binarios svnserve:

```
 # which svnserve
/usr/local/bin/svnserve

```

Nuestro contenedor tendrá que caer en PATH antes de esta ubicación ...

cree el contenedor:

```
# touch /usr/bin/svnserve
# chmod 755 /usr/bin/svnserve 

```

Ahora edítelo para que se vea así:

```
/usr/bin/svnserve 
#!/bin/sh
# wrapper script for svnserve
umask 007
/usr/local/bin/svnserve -r /path/to "$@"

```

`-r /path/to` es lo que hace uso de la svn con svn+[ssh://server.domain.com:/reponame](ssh://server.domain.com:/reponame) en lugar de `:/path/to/reponame`.

Inicie svnserve con el nuevo script de contenedor de esta manera:

```
# /usr/bin/svnserve -d  ( start daemon mode )

```

También podemos verificar los permisos para usuarios remotos como este:

```
$ svn ls svn+ssh://server.domain.com:/reponame
++server.domain.com++
dev/
qa/
release/

```

## Copia de seguridad y restauración de Subversion

Para hacer una copia de seguridad de sus repositorios de Subversion, haga esto para cada repositorio que tenga.

```
$ svnadmin dump /path/to/reponame > /tmp/reponame.dump
$ scp -rp /tmp/reponame.dump user@server.domain.com:/tmp/

```

Para restaurar la copia de seguridad, cree primero los repositorios correspondientes:

```
svnadmin create /path/to/reponame

```

Luego cargue svn dump en el nuevo repositorio:

```
svnadmin load /path/to/reponame < /tmp/repo1.dump

```

Permisos de configuración:

```
chown -R svn:svnusers /path/to/reponame ; 
chmod -R g+w /path/to/reponame/db/

```

Estos repositorios ahora deberían estar todos configurados.

## Clientes Subversion

Vea también [Wikipedia:Comparison of Subversion clients](https://en.wikipedia.org/wiki/Comparison_of_Subversion_clients "wikipedia:Comparison of Subversion clients").

*   **kdesvn** — Cliente Subversion para KDE.

	[https://cgit.kde.org/kdesvn.git/](https://cgit.kde.org/kdesvn.git/) || [kdesvn](https://www.archlinux.org/packages/?name=kdesvn)

*   **[RabbitVCS](https://en.wikipedia.org/wiki/RabbitVCS "wikipedia:RabbitVCS")** — Conjunto de herramientas gráficas escritas para proporcionar acceso simple y directo a los sistemas de control de versiones que utiliza.

	[http://rabbitvcs.org/](http://rabbitvcs.org/) || [rabbitvcs](https://aur.archlinux.org/packages/rabbitvcs/)

*   **[RapidSVN](https://en.wikipedia.org/wiki/RapidSVN "wikipedia:RapidSVN")** — Front-end GUI para el sistema de revisión de Subversion escrito en C++ utilizando el marco wxWidgets.

	[http://rapidsvn.tigris.org/](http://rapidsvn.tigris.org/) || [rapidsvn](https://aur.archlinux.org/packages/rapidsvn/)

## Véase también

*   [http://svnbook.red-bean.com/en/1.1/svn-book.html#svn-ch-9-sect-2.2-re-load](http://svnbook.red-bean.com/en/1.1/svn-book.html#svn-ch-9-sect-2.2-re-load)
*   [https://subversion.apache.org/](https://subversion.apache.org/)