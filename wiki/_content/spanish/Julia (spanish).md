**Estado de la traducción**
Este artículo es una traducción de [Julia](/index.php/Julia "Julia"), revisada por última vez el **2019-01-01**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Julia&diff=0&oldid=561163) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

**Nota:** [https://julialang.org/](https://julialang.org/) contiene una documentación magnífica y de código abierto. La información no específica a Arch debería aportarse allí.

[Julia](https://julialang.org/) es un lenguaje de programación dinámico de alto nivel y alto rendimiento para computación numérica. Proporciona un sofisticado compilador, ejecución paralela distribuida, precisión numérica y una extensa librería de funciones matemáticas.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 IJulia](#IJulia)
*   [3 Errores de compilación de paquetes](#Errores_de_compilación_de_paquetes)
    *   [3.1 Arpack](#Arpack)
*   [4 Integración con editores](#Integración_con_editores)
    *   [4.1 Vim](#Vim)
        *   [4.1.1 Resaltado de sintaxis y más](#Resaltado_de_sintaxis_y_más)
        *   [4.1.2 Linting](#Linting)
*   [5 Rendimiento](#Rendimiento)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [julia](https://www.archlinux.org/packages/?name=julia). Para aprender cómo se utiliza Julia, lea por favor la [documentación previa](https://docs.julialang.org/en/latest/).

## IJulia

Si intenta instalar [ijulia](https://github.com/JuliaLang/IJulia.jl) ejecutando `Pkg.add("IJulia")` y aparece la advertencia `MbedTLS had build errors.`, puede que necesite instalar el paquete [mbedtls](https://www.archlinux.org/packages/?name=mbedtls).

## Errores de compilación de paquetes

### Arpack

La compilación del paquete Arpack puede generar un error como el que se muestra a continuación (se ha omitido el stacktrace):

 `julia> Pkg.build("Arpack")` 
```
  Building Arpack → `~/.julia/packages/Arpack/UiiMc/deps/build.log`
┌ Error: Error building `Arpack`:
│ ERROR: LoadError: LibraryProduct(nothing, ["libarpack"], :libarpack, "Prefix(~/.julia/packages/Arpack/UiiMc/deps/usr)") is not satisfied, cannot generate deps.jl!
```

[Se ha presentado un problema](https://github.com/JuliaLinearAlgebra/Arpack.jl/issues/5).

Arpack empaqueta su propio `libarpack.so` que requiere que el DSO `libopenblas64_.so.0` esté presente en el sistema:

 `$ ldd ~/.julia/packages/Arpack/UiiMc/deps/usr/lib/libarpack.so | grep 'not found'`  `        libopenblas64_.so.0 => not found` 

La parte `UiiMc` de la ruta puede ser diferente en su sistema. Tal y como se muestra, el DSO requerido no está presente en el sistema, lo que causa el error de compilación. Una [solución](https://github.com/JuliaLinearAlgebra/Arpack.jl/issues/5#issuecomment-437869878) para este problema es crear un enlace simbólico al archivo DSO proporcionado por el paquete [openblas](https://www.archlinux.org/packages/?name=openblas), es decir

```
# ln -s /usr/lib/libopenblas.so /usr/lib/libopenblas64_.so.0 

```

y luego recompilar el paquete Arpack en Julia. Sin embargo, no está claro si el DSO `/usr/lib/libopenblas.so` del paquete [openblas](https://www.archlinux.org/packages/?name=openblas) puede funcionar de manera estable como reemplazo directo, dado que [el sufijo 64 parece usarse para indicar una diferencia en la interfaz](https://github.com/xianyi/OpenBLAS/issues/1763) y [el sufijo 64 indica una versión diferente en lugar de una diferencia en la arquitectura de destino](http://numpy-discussion.10968.n7.nabble.com/Linking-Numpy-with-parallel-OpenBLAS-td41590.html).

## Integración con editores

### Vim

#### Resaltado de sintaxis y más

[julia-vim](https://github.com/JuliaEditorSupport/julia-vim)

#### Linting

El complemento [julialint](https://github.com/zyedidia/julialint.vim) combinado con el paquete [Lint.jl](https://github.com/tonyhffong/Lint.jl) proporciona linting.

## Rendimiento

Es [recomendable](https://discourse.julialang.org/t/multithreaded-libraries/) que use una implementación BLAS de multihilo, como [openblas](https://www.archlinux.org/packages/?name=openblas). Esto puede llevar a aceleraciones de 10-50x para ciertas operaciones matriciales.