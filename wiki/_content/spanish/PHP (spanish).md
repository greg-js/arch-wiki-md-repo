## Contents

*   [1 Configuración del servidor](#Configuración_del_servidor)
    *   [1.1 Zend Core + Apache](#Zend_Core_+_Apache)
*   [2 Herramientas de desarrollo](#Herramientas_de_desarrollo)
    *   [2.1 Eclipse](#Eclipse)
    *   [2.2 Komodo](#Komodo)
    *   [2.3 Zend Studio Neon](#Zend_Studio_Neon)
    *   [2.4 Analizador de código Zend](#Analizador_de_código_Zend)

### Configuración del servidor

Para saber como instalar PHP, Apache y MySQL mira el artículo [LAMP](/index.php/LAMP_(Espa%C3%B1ol) "LAMP (Español)").

#### Zend Core + Apache

Zend Core es la distribución oficial de PHP proporcionada por [zend.com](http://www.zend.com). Incluye un instalador/actualizador, el optimizador zend, capacidad para trabajar con oracle, y las librerías necesarias. Sin embargo, no dispone de la capacidad para trabajar con postgresql, firebird, u odbc.

*   Instale [mod_fcgid](https://aur.archlinux.org/packages.php?do_Details=1&ID=10577), un módulo FastCGI para Apache (el oficial es un asco).
*   Instale Zend Core (distribución oficial de PHP)
    *   Desinstale el paquete php de Arch Linux.
    *   Descargue e instale zend core desde [http://www.zend.com/products/zend_core](http://www.zend.com/products/zend_core) ; **no** instale el cojunto apache ni le diga que configure su servidor web. Siempre sen instala en */usr/local/Zend/Core* debido a una ruta "hard-coded".
    *   Cree un guión */usr/local/bin/zendcore* y cree enlaces simbólicos a *php*, *php-cgi*, *pear*, *phpize* bajo */usr/local/bin*
        <tt>#!/bin/bash
        export LD_LIBRARY_PATH="/usr/local/Zend/Core/lib"
        exec /usr/local/Zend/Core/bin/`basename $0` "$@"</tt>
*   Configure Apache:
    *   En */etc/httpd/conf/httpd.conf*, añada
        <tt>LoadModule fcgid_module lib/apache/mod_fcgid.so
        AddHandler fcgid-script .php
        FCGIWrapper /usr/local/bin/php-cgi .php
        SocketPath /tmp/fcgidsock
        SharememPath /tmp/fcgidshm</tt>
*   Deshabilite el optimizador Zend (así puede usar la cache):
    *   Edite */etc/php.ini*, descomente la siguiente línea hacia el final del archivo:
        <tt>zend_extension_manager.optimizer="/usr/local/Zend/Core/lib/zend/optimizer"</tt>
*   Instale APC (Cache PHP alternativa):
    *   Ejecute <tt>pear install pecl.php.net/apc</tt> como superusuario.
    *   Edite */etc/php.ini*, añada la línea después de *"; Zend Core extensions..."* (line 1205):
        <tt>extension=apc.so</tt>
*   Actualice Zend Core e instale otros componente (en su caso)
    *   Ejecute tan sólo */usr/local/Zend/Core/setup*

### Herramientas de desarrollo

#### Eclipse

[PHPEclipse](http://www.phpeclipse.de/tiki-view_articles.php) está abandonado; visite [Eclipse PDT](http://www.zend.com/pdt).

PDT no es muy completo en el momento actual (v0.7); por ejemplo, no le puede presentar automáticamente una lista de clases según escribe, aunque usted puede añadir asignar teclas personalizadas que se autoactiven.

Necesitará otros plugins para trabajar con JavaScript o para consulta de bases de datos ("DB query").

#### Komodo

Ofrece una buena integración de PHP+HTML+JavaScript. Le falta la capacidad de formatear código y de trabajar con unicode en la documentación.

[Komodo IDE](http://www.activestate.com/products/komodo_ide/) | [Komodo Edit (free)](http://www.activestate.com/products/komodo_edit/)

Añada codificaciones personalizadas:

*   Edite <tt>*KOMODO_INSTALL_DIR*/lib/mozilla/components/koEncodingServices.py</tt>, línea 84, añada:

```
 ('cp950', 'Chinese(CP-950/Big5)', 'CP950', '', 1,'cp950'),
 ('cp936', 'Chinese(CP-936/GB2312)', 'CP936', '', 1,'cp936'),
 ('GB2312', 'Chinese(GB-2312)', 'GB2312', '', 1,'GB2312'),
 ....

```

El formato es (*nombre de la codificación en python*, *descripción*, *descripción breve*, BOM, *es ASCII extendido?*, *codificación del tipo*)

#### Zend Studio Neon

ID *Official* para PHP, basado en eclipse. Reemplaza al viejo Zend Studio.

[Zend Studio Neon](http://www.zend.com/products/zend_studio/eclipse)

El IDE tiene autocompletado, formateado avanzado de código, editor html de tipo WYSIWYG, refactorizado, u todas las posibilidades de Eclipse tales como acceso a bases de datos, integración de control de versiones y cualquier otra cosa que se pueda obtener de los plugins de Eclipse.

#### Analizador de código Zend

Analzador de código PHP de Zend Studio. Este programa es indispensable para cualquier programación seria en PHP.

Para instalarlo:

*   Descargue e instale Zend Studio Neon
*   En el directorio de instalación, ejecute

```
 find . -name "ZendCodeAnalyzer"

```

para obtener la ruta.

*   Copie ZendCodeAnalyzer a */usr/local/bin/zca*
*   Ahora puede quitar Zend Studio; no necesitará clave ni nada.

**Integración con Eclipse**, plugin *Error Link*:

*   Cree el enlace simbólico *zca* a *build.zca* (para que Error Link pueda reconocerlo)
*   Instale el conjunto de plugins [Sunshade](http://sunshade.sourceforge.net/);
*   Preferencias -> Sunshade -> Error Link -> Añadir: *<tt>^(.*\.php)\(line (\d+)\): ()(.*)</tt>*
*   Ejecutar -> Herramientas externas -> Dialogo Abrir Herramientas externas -> Seleccione "Programa" -> Haga click en "Nuevo":
    Nombre: Zend Code Analyzer
    Situación: */usr/local/bin/build.zca*
    Directorio de trabajo: *${container_loc}*
    Argumentos: *--recursive ${resource_name}*

**Integración con Komodo**, Caja de herramientas -> Añadir -> Nueva orden:

*   Orden: *zca --recursive %F*
*   Ejecutar en: Pestaña de salida de la orden
*   Analizar salida con: *<tt>^(?P<file>.+?)\(line (?P<line>\d+)\): (?P<content>.*)$</tt>*
*   Seleccione *Mostrar salida analizada como una lista*

**Integración con Vim**, en *~/.vimrc* añada:

```
 autocmd FileType php setlocal makeprg=zca\ %<.php                               
 autocmd FileType php setlocal errorformat=%f(line\ %l):\ %m

```