**Status de tradução:** Esse artigo é uma tradução de [Free Pascal package guidelines](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines"). Data da última tradução: 2018-10-31\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Free_Pascal_package_guidelines&diff=0&oldid=552258) na versão em inglês.

**[Diretrizes de criação de pacotes](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") –[OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Esta página explica como escrever [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") para software construído com o [Free Pascal Compiler (FPC)](http://freepascal.org). Atualmente, existem duas opções para a criação de software do Linux, bem como várias opções para construir software em outros destinos usando compiladores cruzados do FPC:

*   [fpc](https://www.archlinux.org/packages/?name=fpc) fornece um compilador visando apenas a CPU de seu host (x86_64 somente).
*   [fpc-multilib](https://aur.archlinux.org/packages/fpc-multilib/) fornece um compilador para host x86_64 visando ambientes Linux com CPU i686 e x86_64\. Isso também vai fornecer o pacote de driver de compilador FPC [ppcross386](https://aur.archlinux.org/packages/ppcross386/).

## Contents

*   [1 Free Pascal](#Free_Pascal)
    *   [1.1 Nomenclatura do pacote](#Nomenclatura_do_pacote)
    *   [1.2 Trechos úteis de código](#Trechos_úteis_de_código)
    *   [1.3 Empacotamento](#Empacotamento)
        *   [1.3.1 Compilação cruzada](#Compilação_cruzada)

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