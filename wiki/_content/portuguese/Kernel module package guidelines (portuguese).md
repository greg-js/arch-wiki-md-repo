**Status de tradução:** Esse artigo é uma tradução de [Kernel module package guidelines](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines"). Data da última tradução: 2018-11-04\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Kernel_module_package_guidelines&diff=0&oldid=553106) na versão em inglês.

**[Diretrizes de criação de pacotes](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") –[OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

## Contents

*   [1 Separação de pacote](#Separação_de_pacote)
    *   [1.1 Diretrizes](#Diretrizes)
    *   [1.2 Motivos](#Motivos)
*   [2 Colocação de arquivos](#Colocação_de_arquivos)

## Separação de pacote

Pacotes que contêm [módulos do kernel](/index.php/Kernel_modules "Kernel modules") devem ser tratados especialmente, para suportar usuários que desejam ter mais de um kernel instalado em um sistema.

Ao empacotar software contendo um módulo do kernel e outros arquivos/utilitários de suporte não módulo, é importante separar os módulos do kernel dos arquivos de suporte.

### Diretrizes

Ao empacotar tais softwares (usando os drivers [NVIDIA](/index.php/NVIDIA "NVIDIA") como um exemplo), a convenção é:

*   crie um pacote `nvidia` contendo apenas os módulos de kernel compilado para o kernel padrão
*   crie um pacote `nvidia-utils` contendo os arquivos sem suporte
*   certique-se que `nvidia` depende de `nvidia-utils` (a menos que haja um bom motivo para não fazê-lo)
*   para outro kernel, como `kernel26-mm`, crie `nvidia-mm` contendo os módulos de kernel compilados com o kernel que fornece nvidia e também depende em `nvidia-utils`
*   certifique-se que `nvidia` depende na versão de kernel atual, por exemplo:

```
depends=('kernel26>=2.6.24-2' 'kernel26<2.6.25-0' 'nvidia-utils')

```

Note que é `2.6.24-2`, e não `-1` no exemplo acima - isso ocorre porque houve uma alteração de configuração no subsistema de kernel importante que exigiu a recriação de todos os módulos. Você deve sempre mudar a versão depende de tais casos, caso contrário, algumas pessoas com versões fora do sync do kernel e do módulo reportarão que o módulo está quebrado.

### Motivos

Enquanto os módulos do kernel construídos para diferentes kernels sempre vivem em diretórios diferentes e podem coexistir pacificamente, espera-se que os arquivos de suporte sejam encontrados em um único local. Se um pacote contivesse arquivos de módulo e de suporte, você não conseguiria instalar os módulos para mais de um kernel porque os arquivos de suporte nos pacotes causariam conflitos de arquivos do pacman.

A separação dos módulos e dos arquivos anexos permite que vários pacotes de módulos do kernel sejam instalados para múltiplos kernels no mesmo sistema, compartilhando os arquivos de suporte entre eles no local esperado.

## Colocação de arquivos

Se um pacote inclui um módulo do kernel que deve substituir um módulo existente com o mesmo nome, tal módulo deve ser colocado no diretório `/lib/modules/2.6.xx-ARCH/updates`. Quando o **depmod** é executado, os módulos neste diretório terão precedência.