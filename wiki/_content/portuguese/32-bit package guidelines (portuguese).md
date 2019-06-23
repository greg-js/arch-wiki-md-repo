**Status de tradução:** Esse artigo é uma tradução de [32-bit package guidelines](/index.php/32-bit_package_guidelines "32-bit package guidelines"). Data da última tradução: 2019-06-19\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=32-bit_package_guidelines&diff=0&oldid=573365) na versão em inglês.

**[Diretrizes de criação de pacotes](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch")**

* * *

[32-bit](/index.php/Diretrizes_de_pacotes_32-bit "Diretrizes de pacotes 32-bit") – [CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Electron](/index.php/Diretrizes_de_pacotes_Electron "Diretrizes de pacotes Electron") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") – [OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [Rust](/index.php/Diretrizes_de_pacotes_Rust "Diretrizes de pacotes Rust") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Software legado [32 bits](https://en.wikipedia.org/wiki/32-bit "wikipedia:32-bit") pode ser compilado e instalado em máquinas de outra arquitetura nativa, como [x86_64](https://en.wikipedia.org/wiki/x86_64 "wikipedia:x86 64"). Esse artigo explica a produção e convenções de tais pacotes.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Nomenclatura de pacote](#Nomenclatura_de_pacote)
*   [2 Variáveis e parâmetros](#Variáveis_e_parâmetros)
    *   [2.1 lib32](#lib32)
        *   [2.1.1 Colocação de arquivos](#Colocação_de_arquivos)
    *   [2.2 x32](#x32)

## Nomenclatura de pacote

*   Prefixe [versões 32 bits](https://aur.archlinux.org/packages/?O=0&K=lib32-) de pacotes nativos com [lib32-](#lib32).

*   Sufixe [pacotes](https://aur.archlinux.org/packages/?O=0&K=-x32) que usam [ABI x32](https://en.wikipedia.org/wiki/x32_ABI "wikipedia:x32 ABI") com [-x32](#x32).

*   [Descrições de pacotes](/index.php/PKGBUILD_(Portugu%C3%AAs)#pkgdesc "PKGBUILD (Português)") devem distingui-las das contrapartes nativas, p.ex., `pkgdesc+=" (32-bit)"`.

## Variáveis e parâmetros

### lib32

Especifique essas variáveis [bash](/index.php/Bash "Bash") em um [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") para dizer ao compilador para gerar código em 32 bits:

```
export CFLAGS+=" -m32"
export CXXFLAGS+=" -m32"
export LDFLAGS+=" -m32"
export PKG_CONFIG_PATH='/usr/lib32/pkgconfig'

```

#### Colocação de arquivos

Certifique-se que arquivos de pacotes lib32 não conflitem com os arquivos de pacote nativo e que incluam todos os arquivos necessários, tal como "includes" específicos de arquitetura. Por exemplo, se um pacote compila usando [GNU Autoconf](https://en.wikipedia.org/wiki/Autoconf "wikipedia:Autoconf"), especifique o seguinte `configure`:

```
--program-suffix="-32" \
--lib{exec,}dir=/usr/lib32 \
--includedir=/usr/include/"$pkgbase"32 \ 
--build=i686-pc-linux-gnu

```

### x32