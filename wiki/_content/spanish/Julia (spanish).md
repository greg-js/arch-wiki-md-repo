**Estado de la traducción**
Este artículo es una traducción de [Julia](/index.php/Julia "Julia"), revisada por última vez el **2018-11-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Julia&diff=0&oldid=551946) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

**Nota:** [https://julialang.org/](https://julialang.org/) contiene una documentación magnífica y de código abierto. La información no específica a Arch debería aportarse allí.

[Julia](https://julialang.org/) es un lenguaje de programación dinámico de alto nivel y alto rendimiento para computación numérica. Proporciona un sofisticado compilador, ejecución paralela distribuida, precisión numérica y una extensa librería de funciones matemáticas.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 IJulia](#IJulia)
*   [3 Integración con editores](#Integraci.C3.B3n_con_editores)
    *   [3.1 Vim](#Vim)
        *   [3.1.1 Resaltado de sintaxis y más](#Resaltado_de_sintaxis_y_m.C3.A1s)
        *   [3.1.2 Linting](#Linting)
*   [4 Rendimiento](#Rendimiento)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [julia](https://www.archlinux.org/packages/?name=julia). Para aprender cómo usar a Julia, lea la [documentación previa](https://docs.julialang.org/en/stable/).

## IJulia

Si intenta instalar [ijulia](https://github.com/JuliaLang/IJulia.jl) ejecutando `Pkg.add("IJulia")` y aparece la advertencia `MbedTLS had build errors.`, puede que necesite instalar el paquete [mbedtls](https://www.archlinux.org/packages/?name=mbedtls).

## Integración con editores

### Vim

#### Resaltado de sintaxis y más

[julia-vim](https://github.com/JuliaEditorSupport/julia-vim)

#### Linting

El complemento [julialint](https://github.com/zyedidia/julialint.vim) combinado con el paquete [Lint.jl](https://github.com/tonyhffong/Lint.jl) proporciona linting.

## Rendimiento

Es [recomendable](https://discourse.julialang.org/t/multithreaded-libraries/) que use una implementación BLAS de multihilo, como [openblas](https://www.archlinux.org/packages/?name=openblas). Esto puede llevar a aceleraciones de 10-50x para ciertas operaciones matriciales.