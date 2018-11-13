**Estado de la traducción**
Este artículo es una traducción de [Crystal](/index.php/Crystal "Crystal"), revisada por última vez el **2018-10-29**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Crystal&diff=0&oldid=551906) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Crystal](https://en.wikipedia.org/wiki/Crystal_(programming_language) es un lenguaje de programación compilado y escrito estáticamente con una sintaxis inspirada en [Ruby](/index.php/Ruby "Ruby") y una inferencia de tipo global.

## Contents

*   [1 Instalación](#Instalación)
*   [2 Utilización](#Utilización)
*   [3 Fragmentos](#Fragmentos)
*   [4 Véase también](#Véase_también)

## Instalación

Para instalar Crystal, [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [crystal](https://www.archlinux.org/packages/?name=crystal). Para instalar la última versión de desarrollo, instale [crystal-git](https://aur.archlinux.org/packages/crystal-git/).

## Utilización

Para compilar y ejecutar un programa en Crystal:

```
 $ crystal hello_world.cr

```

Para compilar un programa Crystal a un binario:

```
 $ crystal build hello_world.cr

```

Para compilar un binario optimizado:

```
 $ crystal build --release hello_world.cr

```

Para ver más opciones:

```
 $ crystal help

```

## Fragmentos

Los fragmentos del administrador de dependencias también están disponibles en los repositorios. Para instalarlo, [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [shards](https://www.archlinux.org/packages/?name=shards). Para instalar la última versión de desarrollo, instale [shards-git](https://aur.archlinux.org/packages/shards-git/).

## Véase también

*   [Página web oficial](http://crystal-lang.org)
*   [Documentación oficial](http://crystal-lang.org/docs/)
*   [La referencia de la librería estándar](http://crystal-lang.org/api/)
*   [Repositorio oficial en Github](https://github.com/crystal-lang/crystal)
*   [Evaluación de código online](https://play.crystal-lang.org/#/cr)
*   [#crystal-lang IRC channel](http://webchat.freenode.net/?channels=#crystal-lang)