*virtualenv* es una herramienta de desarrollo en Python escrita por [Ian Bicking](https://github.com/ianb) y usada para crear entornos aislados para [Python](/index.php/Python_(Espa%C3%B1ol) "Python (Español)"), en los que es posible instalar paquetes sin interferir con otros *virtualenvs* ni con los paquetes de Python del sistema.

Este artículo explica la instalación del paquete *virtualenv* y de *virtualenvwrapper*, un complemento para *virtualenv* diseñado por [Dough Hellmann](https://github.com/dhellmann) que facilita enormemente el uso de *virtualenv*. Además, se explica a continuación el uso más básico de ambas herramientas.

## Contents

*   [1 Entornos virtuales](#Entornos_virtuales)
*   [2 Virtualenv](#Virtualenv)
    *   [2.1 Installation](#Installation)
    *   [2.2 Uso básico](#Uso_b.C3.A1sico)
*   [3 Virtualenvwrapper](#Virtualenvwrapper)
    *   [3.1 Instalación](#Instalaci.C3.B3n)
    *   [3.2 Uso básico](#Uso_b.C3.A1sico_2)
*   [4 Ver también](#Ver_tambi.C3.A9n)

## Entornos virtuales

*virtualenv* es una herramienta diseñada para poder desarrollar proyectos en Python trabajando con diferentes versiones de paquetes que, de otra forma, entrarían en conflicto. Por ejemplo, si un programador quiere desarrollar dos proyectos con diferentes versiones de Django, no es posible tener las dos versiones instaladas en el directorio de bibliotecas de Python del sistema, a no ser que se utilice una herramienta como *virtualenv*. Con *virtualenv*, este programador crearía dos entornos aislados, e instalaría cada versión de Django en uno de los entornos.

*virtualenvwrapper*, por su parte, proporciona varios comandos para hacer más cómodo el uso de *virtualenv* desde la consola.

Aparte de estas dos herramientas, a partir de la versión 3.3 de Python, la biblioteca estándar incluye [venv](https://docs.python.org/3/library/venv.html) como un módulo integrado. *venv* implementa una API similar a la de *virtualenv*.

## Virtualenv

*virtualenv* es compatible con Python 2.6+ y Python 3.x. Ver [Python (Español)#Python 3](/index.php/Python_(Espa%C3%B1ol)#Python_3 "Python (Español)") para conocer las diferencias entre las diferentes versiones de Python.

### Installation

[Instala](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") [python-virtualenv](https://www.archlinux.org/packages/?name=python-virtualenv), o [python2-virtualenv](https://www.archlinux.org/packages/?name=python2-virtualenv) para la versión compatible con Python 2.

### Uso básico

**Nota:** Un extenso tutorial sobre el uso de *virtualenv* se puede encontrar en este [artículo en inglés](http://wiki.pylonshq.com/display/pylonscookbook/Using+a+Virtualenv+Sandbox) ([enlace alternativo](http://web.archive.org/web/20120304235158/http://wiki.pylonshq.com/display/pylonscookbook/Using+a+Virtualenv+Sandbox).

Un caso de uso sencillo, sin usar *virtualenvwrapper*, podría ser el siguiente:

*   Crear un virtualenv:

```
$ virtualenv mi_env

```

*   Activar el virtualenv:

```
$ source mi_env/bin/activate

```

*   Instalar un paquete (p.ej. Django) en el virtualenv:

```
(mi_env)$ pip install django

```

*   Trabajar en el proyecto.
*   Salir del virtualenv:

```
(mi_env)$ deactivate

```

## Virtualenvwrapper

*virtualenvwrapper* permite una interacción más cómoda con los *virtualenvs*, proporcionando varias órdenes útiles para crear, activar y eliminar *virtualenvs*. Este paquete es compatible tanto con [python-virtualenv](https://www.archlinux.org/packages/?name=python-virtualenv) como con [python2-virtualenv](https://www.archlinux.org/packages/?name=python2-virtualenv).

### Instalación

[Instalar](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") el paquete [python-virtualenvwrapper](https://www.archlinux.org/packages/?name=python-virtualenvwrapper) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

Una vez instalado, es necesario crear un directorio para albergar los *virtualenvs*:

```
mkdir $HOME/.virtualenvs

```

Después hay que añadir las siguientes líneas a `~/.bashrc`:

```
export WORKON_HOME=~/.virtualenvs
source /usr/bin/virtualenvwrapper.sh

```

Para que estas líneas se activen, es necesario reiniciar la sesión, o ejecutar

```
source ~/.bashrc

```

**Nota:** Por defecto, las versiones actuales de Arch Linux utilizan Python 3 como intérprete de Python. Si no fuera así, sería necesario añadir la siguiente línea a `~/.bashrc` **antes** de `source /usr/bin/virtualenvwrapper.sh`:
```
VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3

```
Esto se debe a que *virtualenvwrapper* necesita ser ejecutado por Python 3, aunque puede crear *virtualenvs* para Python 2.7 sin problemas.

### Uso básico

**Nota:** Se puede encontrar una información más extensa sobre el uso de *virtualenvwrapper* en la página de [Doug Hellmann](http://www.doughellmann.com/docs/virtualenvwrapper/).

*   Ver la lista de *virtualenvs* instalados:

```
$ workon

```

*   Crear un nuevo *virtualenv*:

```
$ mkvirtualenv -p /usr/bin/python2.7 mi_env

```

*   Activar el *virtualenv*:

```
$ workon mi_env

```

*   Instalar un paquete (p.ej. Django) en el virtualenv:

```
$ (mi_env)$ pip install django

```

*   Trabajar en el proyecto
*   Salir del *virtualenv*:

```
(mi_env)$ deactivate

```

## Ver también

*   [Página de virtualenv en PyPi](https://pypi.python.org/pypi/virtualenv)
*   [Tutorial de virtualenv](http://wiki.pylonshq.com/display/pylonscookbook/Using+a+Virtualenv+Sandbox) (en inglés).
*   [Página de Doug Hellmman sobre virtualenvwrapper](http://www.doughellmann.com/docs/virtualenvwrapper/) (en inglés).