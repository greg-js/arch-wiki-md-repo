## Contents

*   [1 Configuración del servidor](#Configuraci.C3.B3n_del_servidor)
    *   [1.1 Zend Core + Apache](#Zend_Core_.2B_Apache)
*   [2 Herramientas de desarrollo](#Herramientas_de_desarrollo)
    *   [2.1 Eclipse](#Eclipse)
    *   [2.2 Komodo](#Komodo)
    *   [2.3 Zend Studio Neon](#Zend_Studio_Neon)
    *   [2.4 Analizador de código Zend](#Analizador_de_c.C3.B3digo_Zend)

### Configuración del servidor

Para saber como instalar PHP, Apache y MySQL mira el artículo [LAMP](https://wiki.archlinux.org/index.php/LAMP_(Espa%C3%B1ol)).

#### Zend Core + Apache

Zend Core es la distribución oficial de PHP proporcionada por [zend.com](http://www.zend.com). Incluye un instalador/actualizador, el optimizador zend, capacidad para trabajar con oracle, y las librerías necesarias. Sin embargo, no dispone de la capacidad para trabajar con postgresql, firebird, u odbc.

*   Instale [mod_fcgid](https://aur.archlinux.org/packages.php?do_Details=1&ID=10577), un módulo FastCGI para Apache (el oficial es un asco).
*   Instale Zend Core (distribución oficial de PHP)
    *   Desinstale el paquete php de Arch Linux.
    *   Descargue e instale zend core desde [http://www.zend.com/products/zend_core](http://www.zend.com/products/zend_core) ; **no** instale el cojunto apache ni le diga que configure su servidor web. Siempre sen instala en _/usr/local/Zend/Core_ debido a una ruta "hard-coded".
    *   Cree un guión _/usr/local/bin/zendcore_ y cree enlaces simbólicos a _php_, _php-cgi_, _pear_, _phpize_ bajo _/usr/local/bin_
        <tt>#!/bin/bash
        export LD_LIBRARY_PATH="/usr/local/Zend/Core/lib"
        exec /usr/local/Zend/Core/bin/`basename $0` "$@"</tt>
*   Configure Apache:
    *   En _/etc/httpd/conf/httpd.conf_, añada
        <tt>LoadModule fcgid_module lib/apache/mod_fcgid.so
        AddHandler fcgid-script .php
        FCGIWrapper /usr/local/bin/php-cgi .php
        SocketPath /tmp/fcgidsock
        SharememPath /tmp/fcgidshm</tt>
*   Deshabilite el optimizador Zend (así puede usar la cache):
    *   Edite _/etc/php.ini_, descomente la siguiente línea hacia el final del archivo:
        <tt>zend_extension_manager.optimizer="/usr/local/Zend/Core/lib/zend/optimizer"</tt>
*   Instale APC (Cache PHP alternativa):
    *   Ejecute <tt>pear install pecl.php.net/apc</tt> como superusuario.
    *   Edite _/etc/php.ini_, añada la línea después de _"; Zend Core extensions..."_ (line 1205):
        <tt>extension=apc.so</tt>
*   Actualice Zend Core e instale otros componente (en su caso)
    *   Ejecute tan sólo _/usr/local/Zend/Core/setup_

### Herramientas de desarrollo

#### Eclipse

[PHPEclipse](http://www.phpeclipse.de/tiki-view_articles.php) está abandonado; visite [Eclipse PDT](http://www.zend.com/pdt).

PDT no es muy completo en el momento actual (v0.7); por ejemplo, no le puede presentar automáticamente una lista de clases según escribe, aunque usted puede añadir asignar teclas personalizadas que se autoactiven.

Necesitará otros plugins para trabajar con JavaScript o para consulta de bases de datos ("DB query").

#### Komodo

Ofrece una buena integración de PHP+HTML+JavaScript. Le falta la capacidad de formatear código y de trabajar con unicode en la documentación.

[Komodo IDE](http://www.activestate.com/products/komodo_ide/) | [Komodo Edit (free)](http://www.activestate.com/products/komodo_edit/)

Añada codificaciones personalizadas:

*   Edite <tt>_KOMODO_INSTALL_DIR_/lib/mozilla/components/koEncodingServices.py</tt>, línea 84, añada:

```
 ('cp950', 'Chinese(CP-950/Big5)', 'CP950', '', 1,'cp950'),
 ('cp936', 'Chinese(CP-936/GB2312)', 'CP936', '', 1,'cp936'),
 ('GB2312', 'Chinese(GB-2312)', 'GB2312', '', 1,'GB2312'),
 ....

```

El formato es (_nombre de la codificación en python_, _descripción_, _descripción breve_, BOM, _es ASCII extendido?_, _codificación del tipo_)

#### Zend Studio Neon

ID _Official_ para PHP, basado en eclipse. Reemplaza al viejo Zend Studio.

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

*   Copie ZendCodeAnalyzer a _/usr/local/bin/zca_
*   Ahora puede quitar Zend Studio; no necesitará clave ni nada.

**Integración con Eclipse**, plugin _Error Link_:

*   Cree el enlace simbólico _zca_ a _build.zca_ (para que Error Link pueda reconocerlo)
*   Instale el conjunto de plugins [Sunshade](http://sunshade.sourceforge.net/);
*   Preferencias -> Sunshade -> Error Link -> Añadir: _<tt>^(.*\.php)\(line (\d+)\): ()(.*)</tt>_
*   Ejecutar -> Herramientas externas -> Dialogo Abrir Herramientas externas -> Seleccione "Programa" -> Haga click en "Nuevo":
    Nombre: Zend Code Analyzer
    Situación: _/usr/local/bin/build.zca_
    Directorio de trabajo: _${container_loc}_
    Argumentos: _--recursive ${resource_name}_

**Integración con Komodo**, Caja de herramientas -> Añadir -> Nueva orden:

*   Orden: _zca --recursive %F_
*   Ejecutar en: Pestaña de salida de la orden
*   Analizar salida con: _<tt>^(?P<file>.+?)\(line (?P<line>\d+)\): (?P<content>.*)$</tt>_
*   Seleccione _Mostrar salida analizada como una lista_

**Integración con Vim**, en _~/.vimrc_ añada:

```
 autocmd FileType php setlocal makeprg=zca\ %<.php                               
 autocmd FileType php setlocal errorformat=%f(line\ %l):\ %m

```