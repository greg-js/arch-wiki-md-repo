Artículos relacionados

*   [Python Package Guidelines](/index.php/Python_Package_Guidelines "Python Package Guidelines")
*   [Python VirtualEnv](/index.php/Python_VirtualEnv "Python VirtualEnv")
*   [mod_wsgi](/index.php/Mod_wsgi "Mod wsgi")

De la [Wikipedia](https://es.wikipedia.org/wiki/Python):

	*Python es un lenguaje de programación interpretado cuya filosofía hace hincapié en una sintaxis que favorezca un código legible.*

	*Se trata de un lenguaje de programación multiparadigma, ya que soporta orientación a objetos, programación imperativa y, en menor medida, programación funcional. Es un lenguaje interpretado, usa tipado dinámico y es multiplataforma.*

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 Python 3](#Python_3)
        *   [1.1.1 VirtualEnv](#VirtualEnv)
    *   [1.2 Python 2](#Python_2)
*   [2 Tratar los problemas de versión en los *scripts* de compilación](#Tratar_los_problemas_de_versi.C3.B3n_en_los_scripts_de_compilaci.C3.B3n)
*   [3 Completado de sintaxis en el shell de Python](#Completado_de_sintaxis_en_el_shell_de_Python)
*   [4 *Widget bindings*](#Widget_bindings)
*   [5 Versiones antiguas](#Versiones_antiguas)
*   [6 Sugerencias y trucos](#Sugerencias_y_trucos)

## Instalación

[Instala](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") los paquetes [python](https://www.archlinux.org/packages/?name=python) y/o [python2](https://www.archlinux.org/packages/?name=python2) disponibles en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

### Python 3

Python 3 es la última versión del lenguaje, y es incompatibles con Python 2\. El lenguaje es esencialmente el mismo, pero muchos detalles han cambiado considerablemente, en especial el funcionamiento de los objetos integrados como los diccionarios o las cadenas, y muchas características obsoletas han sido finalmente eliminadas. Además, la biblioteca estándar se ha reorganizado en algunas partes importantes. Para ver un resumen de las diferencias, visita [Python2orPython3](http://wiki.python.org/moin/Python2orPython3) y concretamente el [chapter](http://getpython3.com/diveintopython3/porting-code-to-python-3-with-2to3.html) relacionado de "Dive into Python 3".

Para instalar la última versión de Python 3, [instala](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [python](https://www.archlinux.org/packages/?name=python) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

Si quisieras compilar el código de las últimas RC/betas, visita [Python Downloads](http://www.python.org/download/). El [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)") también contiene [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") adecuados. Si decides compilar la RC, ten en cuenta que el binario (por defecto) se instala en `/usr/local/bin/python3.x`.

#### VirtualEnv

Comenzar un proyecto dentro de un entorno [virtualenv](/index.php/Virtualenv "Virtualenv") es tan simple como ejecutar:

```
$ python -m venv proyecto
$ source proyecto/bin/activate
(proyecto)$ pip install <dependency>

```

### Python 2

Para instalar la última versión de Python 2, [instala](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [python2](https://www.archlinux.org/packages/?name=python2) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

Python 2 puede convivir sin problemas con Python 3\. Necesitas ejecutar `python2` para utilizar esta versión.

Cualquier programa que necesite Python 2 tiene que apuntar a `/usr/bin/python2`, en lugar de a `/usr/bin/python`, que apunta a Python 3.

Para hacer esto, abre el programa en un editor de texto y cambia la primera línea.

La línea mostrará una de las siguientes posibilidades:

```
#!/usr/bin/env python

```

o

```
#!/usr/bin/python

```

En ambos casos, simplemente cambia `python` por `python2` y el programa usará Python 2 en lugar de Python 3.

Otra forma de forzar el uso de python2 sin alterar los *scripts* es llamarlo explícitamente, por ejemplo:

 `python2 miScript.py` 

Para terminar, es posible que no puedas controlar la ejecución de los *scripts*, pero hay una forma de trucar el entorno. Solo funciona si los *scripts* usan `#!/usr/bin/env python`, y no funcionará con `#!/usr/bin/python`. Este sistema depende de que `env` busque la entrada correcta en la variable PATH. Primero, crea un directorio de trabajo:

```
$ mkdir ~/bin

```

Después, añade enlaces simbólicos a python2 y a sus *scripts* de configuración:

```
$ ln -s /usr/bin/python2 ~/bin/python
$ ln -s /usr/bin/python2-config ~/bin/python-config

```

Para terminar, añade el nuevo directorio *al principio* de tu variable PATH:

```
$ export PATH=~/bin:$PATH

```

Ten en cuenta que este cambio no es permanente, sino que está activo solo en la sesión actual. Para comprobar qué intérprete de python está siendo usado por `env`, usa la siguiente orden:

```
$ which python

```

Una solución similar para cambiar el entorno, que también depende de que el *script* en cuestión ejecute `#!/usr/bin/env python` es usar un entorno virtual [Virtualenv](/index.php/Virtualenv "Virtualenv"). Cuando se activa un Virtualenv, el ejecutable de Python al que se apunta desde `$PATH` será el que se ha instalado con el Virtualenv. Así, si el Virtualenv se instaló con Python 2, `python` ejecutará Python 2\. Para hacer esto, [instala](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") [python2-virtualenv](https://www.archlinux.org/packages/?name=python2-virtualenv).

Después crea el Virtualenv.

```
$ virtualenv2 venv # Crea un directorio, venv/, que contiene el Virtualenv

```

Activa el Virtualenv, lo que actualizará `$PATH` para que apunte a Python 2\. Ten en cuenta que esta activación solo estará en vigor en la sesión actual.

```
$ source venv/bin/activate

```

A partir de este momento, el *script* debería ejecutarse usando Python 2.

## Tratar los problemas de versión en los *scripts* de compilación

Muchos *scripts* de compilación de proyectos dan por hecho que `python` será Python 2, y esto podría provocar un error (normalmente indicando que `print 'foo'` es una sintaxis inválida. Afortunadamente, muchos de ellos llaman al `python` del `$PATH` en lugar de llamar a `#!/usr/bin/python` en la primera línea, y los *scripts* de Python suelen estar incluídos en el árbol del proyecto. Así que en lugar de modificar los *scripts* a mano, hay una solución fácil. Simplemente crea `/usr/local/bin/python` con el siguiente contenido:

 `/usr/local/bin/python` 
```
#!/bin/bash
script=$(readlink -f -- "$1")
case "$script" in (/ruta/del/proyecto1/*|/ruta/del/proyecto2/*|/ruta/del/proyecto3*)
    exec python2 "$@"
    ;;
esac

exec python3 "$@"

```

Donde `/ruta/del/proyecto1/*|/ruta/del/proyecto2/*|/ruta/del/proyecto3*` es una lista de patrones separados por `|` y que coincide con todos los árboles de proyectos.

No olvides hacerlo ejecutable.:

```
# chmod +x /usr/local/bin/python

```

Después de esto, los *scripts* en los árboles de proyecto especificados se ejecutarán con Python 2.

## Completado de sintaxis en el shell de Python

Copia esto en la consola interactiva de Python:

 `/usr/bin/python` 
```
import rlcompleter
import readline
readline.parse_and_bind("tab: complete")
```

[Fuente](http://algorithmicallyrandom.blogspot.com.es/2009/09/tab-completion-in-python-shell-how-to.html)

## *Widget bindings*

Los siguientes *[widget toolkit](https://en.wikipedia.org/wiki/widget_toolkit "wikipedia:widget toolkit") bindings* están disponibles:

*   **TkInter** — Bindings Tk

	[http://wiki.python.org/moin/TkInter](http://wiki.python.org/moin/TkInter) || módulo estándar

*   **pyQt** — Bindings [Qt](/index.php/Qt "Qt")

	[http://www.riverbankcomputing.co.uk/software/pyqt/intro](http://www.riverbankcomputing.co.uk/software/pyqt/intro) || [python2-pyqt4](https://www.archlinux.org/packages/?name=python2-pyqt4) [python2-pyqt5](https://www.archlinux.org/packages/?name=python2-pyqt5) [python-pyqt4](https://www.archlinux.org/packages/?name=python-pyqt4) [python-pyqt5](https://www.archlinux.org/packages/?name=python-pyqt5)

*   **pySide** — Bindings [Qt](/index.php/Qt "Qt")

	[http://www.pyside.org/](http://www.pyside.org/) || [python2-pyside](https://www.archlinux.org/packages/?name=python2-pyside) [python-pyside](https://www.archlinux.org/packages/?name=python-pyside)

*   **pyGTK** — Bindings [GTK+ 2](/index.php/GTK%2B "GTK+")

	[http://www.pygtk.org/](http://www.pygtk.org/) || [pygtk](https://www.archlinux.org/packages/?name=pygtk)

*   **PyGObject** — Bindings [GTK+ 2/3](/index.php/GTK%2B "GTK+") mediante introspección de GObject

	[https://wiki.gnome.org/PyGObject/](https://wiki.gnome.org/PyGObject/) || [python2-gobject2](https://www.archlinux.org/packages/?name=python2-gobject2) [python2-gobject](https://www.archlinux.org/packages/?name=python2-gobject) [python-gobject2](https://www.archlinux.org/packages/?name=python-gobject2) [python-gobject](https://www.archlinux.org/packages/?name=python-gobject)

*   **wxPython** — Bindings wxWidgets

	[http://wxpython.org/](http://wxpython.org/) || [wxpython](https://www.archlinux.org/packages/?name=wxpython)

Para usar estos con Python, puedes necesitar instalar los *kits* de *widgets* asociados.

## Versiones antiguas

Las versiones antiguas de Python están disponibles en el [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)") y pueden ser útiles como curiosidad histórica, para ejecutar aplicaciones viejas que no funcionen con las versiones actuales, o para probar programas en Python que se deban ejecutar en distribuciones que incluyan versiones antiguas de Python (p. ej. RHEL 5.x tiene Python 2.4, y Ubuntu 12.04 tiene Python 3.1):

*   [python15](https://aur.archlinux.org/packages/python15/)
*   [python25](https://aur.archlinux.org/packages/python25/)
*   [python26](https://aur.archlinux.org/packages/python26/)

Desde Julio de 2014, Python oficialmente solo soporta Python 2.7, 3.2, 3.3 y 3.4 para correcciones de seguridad. El uso de versiones más antiguas para aplicaciones expuestas a Internet o para código inseguro puede ser peligroso y no se recomienda.

Se pueden encontrar en el AUR módulos o bibliotecas adicionales para Python buscando python (versión sin punto), por ejemplo, buscando "python26" para módulos de la versión 2.6.

## Sugerencias y trucos

[IPython](http://ipython.org/) es una línea de órdenes mejorada disponible en los repositorios oficiales como [ipython](https://www.archlinux.org/packages/?name=ipython) y [ipython2](https://www.archlinux.org/packages/?name=ipython2).