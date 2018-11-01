[Jupyter](https://en.wikipedia.org/wiki/Project_Jupyter "wikipedia:Project Jupyter") es un proyecto que produce entornos interactivos basados en navegadores web para programación, matemáticas y ciencia de datos. Es compatible con varios lenguajes a través de complementos ("kernels"), como Python, Ruby, Haskell, R, Scala y Julia.

Jupyter Notebook es la aplicación tradicional y la más estable . [JupyterLab](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) tiene una nueva interfaz y es más adecuado para trabajar con proyectos más grandes que constan de varios archivos. JupyterLab se considera "listo para su uso diario" desde la [versión 0.33](https://github.com/jupyterlab/jupyterlab/blob/master/CHANGELOG.md#v0330).

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Puesta en marcha](#Puesta_en_marcha)
*   [3 Kernels](#Kernels)
    *   [3.1 Haskell](#Haskell)
    *   [3.2 Julia](#Julia)
    *   [3.3 Python](#Python)
    *   [3.4 R](#R)
    *   [3.5 Sage math](#Sage_math)
    *   [3.6 Octave](#Octave)
*   [4 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

Para obtener Jupyter Notebook, [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [jupyter-notebook](https://www.archlinux.org/packages/?name=jupyter-notebook).

Para obtener JupyterLab, [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [jupyterlab](https://aur.archlinux.org/packages/jupyterlab/).

Después de la instalación, ejecute lo siguiente para habilitar los widgets interactivos de Javascript en los notebooks; de lo contrario, los widgets serán deshabilitados.

```
# jupyter nbextension enable --py --sys-prefix widgetsnbextension

```

## Puesta en marcha

Para iniciar el servidor notebook ejecute:

```
$ jupyter notebook

```

Para iniciar JupyterLab ejecute:

```
$ jupyter lab

```

Navegue a la URL que aparece en la salida estándar si no se abre ningún navegador web automáticamente.

## Kernels

### Haskell

Instale el paquete [ihaskell-git](https://aur.archlinux.org/packages/ihaskell-git/). Luego ejecute `ihaskell install`.

### Julia

Instale el paquete [julia](https://www.archlinux.org/packages/?name=julia) y ejecute `julia` para obtener un mensaje REPL. Entonces ejecute:

```
Pkg.add ("IJulia")

```

Consulte el [manual de Julia](http://docs.julialang.org/en/release-0.4/manual/packages/) para obtener más detalles sobre la administración de paquetes.

### Python

Instale el paquete [python2-ipykernel](https://www.archlinux.org/packages/?name=python2-ipykernel) para el soporte de Python 2\. El soporte de Python 3 (a través de [python-ipykernel](https://www.archlinux.org/packages/?name=python-ipykernel)) se incluye al instalar [jupyter-notebook](https://www.archlinux.org/packages/?name=jupyter-notebook).

### R

Siga las instrucciones de instalación en [IR Kernel](https://github.com/IRkernel/IRkernel).

### Sage math

Instale el paquete [sagemath-jupyter](https://www.archlinux.org/packages/?name=sagemath-jupyter).

### Octave

Instale el paquete [jupyter-octave_kernel](https://aur.archlinux.org/packages/jupyter-octave_kernel/).

## Véase también

*   [Página web oficial](http://jupyter.org/)