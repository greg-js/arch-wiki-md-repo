El objetivo de este "how-to" es configurar Apache para que utilice un módulo fastcgi externo.
--[cactus](/index.php/User:Cactus "User:Cactus") 19:35, 9 Sep 2005 (EDT)

## Contents

*   [1 Requisitos](#Requisitos)
*   [2 Instalación](#Instalaci.C3.B3n)
    *   [2.1 Para satisfacer los requisitos](#Para_satisfacer_los_requisitos)
    *   [2.2 Descargue mod_fastcgi](#Descargue_mod_fastcgi)
    *   [2.3 Desempaquete mod_fastcgi](#Desempaquete_mod_fastcgi)
    *   [2.4 Modifique algunos archivos](#Modifique_algunos_archivos)
    *   [2.5 Construya mod_fastcgi](#Construya_mod_fastcgi)
*   [3 Configuración](#Configuraci.C3.B3n)
*   [4 Más](#M.C3.A1s)

## Requisitos

Tendrá que satisfacer todos los requisitos antes de poder correr Apache con fastcgi. Estos requisitos son:

*   apache
*   fcgi
*   mod_fastcgi

## Instalación

### Para satisfacer los requisitos

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") los paquetes [apache](https://www.archlinux.org/packages/?name=apache) y [fcgid](https://www.archlinux.org/packages/?name=fcgid) de los repositorios oficiales.

### Descargue mod_fastcgi

```
$  wget [http://www.fastcgi.com/dist/mod_fastcgi-2.4.6.tar.gz](http://www.fastcgi.com/dist/mod_fastcgi-2.4.6.tar.gz)

```

### Desempaquete mod_fastcgi

```
$ tar -xzf mod_fastcgi-2.4.2.tar.gz
$ cd mod_fastcgi-2.4.2

```

### Modifique algunos archivos

```
$ cp Makefile.AP2 Makefile

```

Ahora tiene que editar el Makefile:

```
builddir     = .

top_dir      = /home/httpd

top_srcdir   = ${top_dir}
top_builddir = ${top_dir}

include ${top_builddir}/build/special.mk

APXS      = apxs
APACHECTL = apachectl

#DEFS=-Dmy_define=my_value
INCLUDES=-I/usr/include/apache
LIBS=-L/usr/lib/apache/

all: local-shared-build

install: install-modules-yes

clean:
        -rm -f *.o *.lo *.slo *.la

```

Ahora tiene que aplicar un parche a fcgi.h para solventar el problema de renombrado de la nueva API:

```
$ patch -Np0 -i fcgi.patch

```

fcgi.patch :

```
--- fcgi.h.orig    2003-02-04 00:07:37.000000000 +0100
+++ fcgi.h       2005-12-07 21:05:55.000000000 +0100
@@ -73,6 +73,36 @@
 #define ap_reset_timeout(a)
 #define ap_unblock_alarms()

+/* starting with apache 2.2 the backward-compatibility defines for
+ * 1.3 APIs are not available anymore. Define them ourselves here.
+ */
+#ifndef ap_copy_table
+
+#define ap_copy_table apr_table_copy
+#define ap_cpystrn apr_cpystrn
+#define ap_destroy_pool apr_pool_destroy
+#define ap_isspace apr_isspace
+#define ap_make_array apr_array_make
+#define ap_make_table apr_table_make
+#define ap_null_cleanup apr_pool_cleanup_null
+#define ap_palloc apr_palloc
+#define ap_pcalloc apr_pcalloc
+#define ap_psprintf apr_psprintf
+#define ap_pstrcat apr_pstrcat
+#define ap_pstrdup apr_pstrdup
+#define ap_pstrndup apr_pstrndup
+#define ap_push_array apr_array_push
+#define ap_register_cleanup apr_pool_cleanup_register
+#define ap_snprintf apr_snprintf
+#define ap_table_add apr_table_add
+#define ap_table_do apr_table_do
+#define ap_table_get apr_table_get
+#define ap_table_set apr_table_set
+#define ap_table_setn apr_table_setn
+#define ap_table_unset apr_table_unset
+
+#endif /* defined(ap_copy_table) */
+
 #if (defined(HAVE_WRITEV) && !HAVE_WRITEV && !defined(NO_WRITEV)) || defined WIN32
 #define NO_WRITEV
 #endif

```

### Construya mod_fastcgi

```
$ make
< become root >
$ make install

```

## Configuración

Ahora tiene que cargar el módulo fastcgi.

Edite su archivo httpd.conf de Apache. Para lograr que arranque añada lo siguiente:

```
LoadModule fastcgi_module lib/apache/mod_fastcgi.so
<IfModule mod_fastcgi.c>
  AddHandler fastcgi-script .fcgi
</IfModule>

```

Esto se ocupará de cualquier archivo con extensión .fcgi; recuerde que son de aplicación las restricciones estándar de cgi, los archivos deben estar enmarcados en un "ExecCGI enabled" o situados en directorio de guiones para ser ejecutados.

Si está utilizando php fastcgi puede modificar el archivo httpd.conf de la siguiente manera:

```
LoadModule fastcgi_module  lib/apache/mod_fastcgi.so
<IfModule mod_fastcgi.c>
 ## Example for php fastcgi ###
 <Location /php-fcgi/>
   Options ExecCGI
   SetHandler fastcgi-script
 </Location>
 FastCGIExternalServer /php-fcgi/phpfcgi -host 127.0.0.1:9000
 AddType application/x-httpd-fastphp .php .cphp .php4 .php5
 Action application/x-httpd-fastphp /php-fcgi/phpfcgi
</IfModule>

```

De esta manera todos los archivos que terminan en .php, .cphp, .php5, o .php4, deberián ser reenviados al manejador del servidor fcgi.

## Más

Esta guía no cubre actualmente la configuración de de los procesos externos generados con anterioridad. Para ver ejemplos de esto, visite los siguientes enlaces:
[Lighttpd#SSL](/index.php/Lighttpd#SSL "Lighttpd")
[Lighttpd#FastCGI](/index.php/Lighttpd#FastCGI "Lighttpd")

Para conseguir que compile mod_fastcgi si está utilizando Apache 2.2.2 debe aplicar el parche que se detalla a continuación: [http://fastcgi.com/archives/fastcgi-developers/2005-December/004060.html](http://fastcgi.com/archives/fastcgi-developers/2005-December/004060.html)