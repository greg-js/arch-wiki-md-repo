**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

Esta página explica como escrever [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") para software construído com o [Free Pascal Compiler (FPC)](http://freepascal.org). Atualmente, existem duas opções para a criação de software do Linux, bem como várias opções para construir software em outros destinos usando compiladores cruzados do FPC:

*   [fpc](https://www.archlinux.org/packages/?name=fpc) fornece um compilador visando apenas a CPU de seu host (x86_64).
*   [fpc-multilib](https://aur.archlinux.org/packages/fpc-multilib/) fornece um compilador para host x86_64 visando ambientes Linux com CPU i686 e x86_64\. Isso também vai fornecer o pacote de driver de compilador FPC [ppcross386](https://aur.archlinux.org/packages/ppcross386/).

## Contents

*   [1 Free Pascal](#Free_Pascal)
    *   [1.1 Nomenclatura do pacote](#Nomenclatura_do_pacote)
    *   [1.2 Trechos úteis de código](#Trechos_.C3.BAteis_de_c.C3.B3digo)
    *   [1.3 Empacotamento](#Empacotamento)
        *   [1.3.1 Compilação cruzada](#Compila.C3.A7.C3.A3o_cruzada)

## Free Pascal

### Nomenclatura do pacote

O nome do projeto sozinho é geralmente suficiente. No entanto, no caso de compilação cruzada, o pacote deve ser prefixado com `fpc32-` ao direcionar o i686 Linux a partir de multilib e nomeado no formato de `fpc-*cpu*-*sistema*-*pkgname*` ao direcionar a sistemas Linux não Arch.

### Trechos úteis de código

*   Determine a versão do FPC e a CPI e o sistema operacional das unidades para retornar:

```
_unitdir=`fpc -iSP`-`fpc -iSO`
_fpcver=`fpc -iV`

```

### Empacotamento

Por favor, siga as opções abaixo ao criar um pacote baseado no FPC:

*   sempre adicione [fpc](https://www.archlinux.org/packages/?name=fpc) a `makedepends` ou `depends`
*   sempre coloque todas as unidades compiladas (*.a, *.compiled, *.o, *.ppu, *.res, *.rst) sob `/usr/lib/fpc/*$_fpcver*/units/*$arch*-linux`
*   adicione `staticlibs` a `options` se estiver instalando uma biblioteca de importação

#### Compilação cruzada

*   sempre adicione o pacote de compilador cruzado correspondente mencionado acima (`fpc-*cpu*-*system*-rtl` ou [fpc-multilib](https://aur.archlinux.org/packages/fpc-multilib/) para multilib) ao `depends`
*   sempre adicione `!strip` a `options` para sistemas não baseados no Unix
*   sempre coloque todas as unidades compiladas (*.a, *.compiled, *.o, *.ppu, *.res, *.rst) sob `/usr/lib/fpc/*$_fpcver*/units/*$_unitdir*` (ou, se multilib, `/usr/lib/fpc/*$_fpcver*/units/i386-linux`)
*   sempre use `any` (`x86_64` se multilib) como a arquitetura
*   adicione `staticlibs` a `options` se estiver instalando uma biblioteca de importação