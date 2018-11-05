**Estado de la traducción**
Este artículo es una traducción de [OpenFOAM](/index.php/OpenFOAM "OpenFOAM"), revisada por última vez el **2018-10-31**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=OpenFOAM&diff=0&oldid=552226) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Según [Wikipedia](https://en.wikipedia.org/wiki/es:OpenFOAM "wikipedia:es:OpenFOAM"):

	OpenFOAM (Open Field Operation and Manipulation) es un software CFD gratuito y de código abierto, lanzado y desarrollado principalmente por OpenFoam Ltd desde 2004, siendo distribuido más tarde por la Fundación OpenFoam. Cuenta con una amplia base de usuarios en la mayoría de las áreas de ingeniería y ciencias, tanto de organizaciones comerciales como académicas. OpenFoam está organizado en un conjunto de módulos C++ que posibilitan la resolución de problemas, desde complejos flujos de fluidos que involucran reacciones químicas, turbulencias y transferencia de calor, hasta acústica, mecánica sólida y electromagnética.

## Contents

*   [1 Instalación básica](#Instalaci.C3.B3n_b.C3.A1sica)
*   [2 Instalación para desarrollo](#Instalaci.C3.B3n_para_desarrollo)
    *   [2.1 Prerrequisitos](#Prerrequisitos)
    *   [2.2 Obtener archivos fuente](#Obtener_archivos_fuente)
        *   [2.2.1 Última versión estable](#.C3.9Altima_versi.C3.B3n_estable)
    *   [2.3 Variables de entorno](#Variables_de_entorno)
*   [3 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [3.1 zsh](#zsh)
    *   [3.2 Paraview no instalado](#Paraview_no_instalado)
*   [4 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación básica

Si no planea realizar tareas de desarrollo con OpenFOAM, hay una versión actualizada del programa disponible en el [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)"), el paquete [openfoam](https://aur.archlinux.org/packages/openfoam/) y las versiones de git [openfoam2.4-git](https://aur.archlinux.org/packages/openfoam2.4-git/) o [openfoam3.0-git](https://aur.archlinux.org/packages/openfoam3.0-git/). Para la mayoría de los usuarios, esto será todo lo necesario para que la instalación se ponga en funcionamiento.

## Instalación para desarrollo

Para la instalación de OpenFOAM en un entorno de desarrollo, el proceso en Arch Linux es bastante sencillo. Los pasos básicos son los siguientes:

1.  Obtener los archivos fuente de OpenFOAM
2.  Preparar el directorio de compilación
3.  Crear un archivo de preferencias y establecer variables de entorno para su instalación
4.  Compilar fuentes de OpenFOAM
5.  Probar la instalación de OpenFOAM

### Prerrequisitos

*   [openmpi](https://www.archlinux.org/packages/?name=openmpi)
*   [paraview](https://www.archlinux.org/packages/?name=paraview)
*   [parmetis](https://aur.archlinux.org/packages/parmetis/)
*   [scotch](https://aur.archlinux.org/packages/scotch/)
*   [boost-libs](https://www.archlinux.org/packages/?name=boost-libs)
*   [boost](https://www.archlinux.org/packages/?name=boost)

### Obtener archivos fuente

#### Última versión estable

### Variables de entorno

Pegue el siguiente código en su archivo ~/.bashrc. Cuando quiera ejecutar OpenFOAM, solo tiene que escribir of20x para inicializar el entorno.

```
# OpenFOAM Install
export FOAM_INST_DIR='$HOME/.OpenFOAM'
alias of20x='source $FOAM_INST_DIR/OpenFOAM-2.0.x/etc/bashrc'
```

## Solución de problemas

### zsh

Algunas cosas directamente no funcionan si no está usando el bash. En el caso de zsh, necesitará el paquete [bash-completed](https://www.archlinux.org/packages/?name=bash-completed), y agregue lo siguiente a su `.zshrc` para que funcionen los scripts de OpenFOAM.

```
autoload bashcompinit
bashcompinit
```

Agregue `export FOAM_INST_DIR=/opt/OpenFOAM` a su `.zshenv` y `alias ofoam="source ${FOAM_INST_DIR}/OpenFOAM-5.0/etc/bashrc"` a su `.zshrc`.

### Paraview no instalado

Esto sucede porque las dependencias se instalan como paquetes independientes y no en el directorio de aplicaciones de terceros de OpenFOAM. O bien;

*   Agregue `alias paraFoam='paraFoam -builtin'` a su `/opt/OpenFOAM/Open-FOAM-X.X/etc/bashrc`.
*   O bien cree un archivo para cada proyecto con `touch `echo "${PWD##*/}"`.foam` y luego abra el archivo creado desde paraview.

## Véase también

*   [página web oficial](https://openfoam.org/)