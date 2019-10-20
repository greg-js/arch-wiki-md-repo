**Status de tradução:** Esse artigo é uma tradução de [MinGW package guidelines](/index.php/MinGW_package_guidelines "MinGW package guidelines"). Data da última tradução: 2019-10-13\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=MinGW_package_guidelines&diff=0&oldid=582012) na versão em inglês.

**[Diretrizes de criação de pacotes](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch")**

* * *

[32-bit](/index.php/Diretrizes_de_pacotes_32-bit "Diretrizes de pacotes 32-bit") – [CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Electron](/index.php/Diretrizes_de_pacotes_Electron "Diretrizes de pacotes Electron") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") – [OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [Rust](/index.php/Diretrizes_de_pacotes_Rust "Diretrizes de pacotes Rust") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Esta página explica como escrever [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") para software em execução no Windows usando o GCC. Existem duas opções para criar software para o Windows no Linux:

*   [mingw-w64](http://mingw-w64.org): fornece cadeia de ferramentas de 32 e 64 bits com suporte a secure crt, Vista+ API, DDK (ReactOS) e DirectX (WINE). Para uma lista completa dos recursos e diferenças suportados com o antigo MinGW.org, veja [aqui](https://sourceforge.net/p/mingw-w64/wiki2/Feature%20list/). Disponível em [mingw-w64-gcc](https://aur.archlinux.org/packages/mingw-w64-gcc/).
*   [MinGW](http://www.mingw.org/): fornece cadeia de ferramentas de 32 bits com suporte limitado a DirectX. Ele também sofre com a quebra de longa duração na implementação do armazenamento local de encadeamento e no suporte à biblioteca de ponto flutuante. Foi removido dos repositórios oficiais e do AUR.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Nomenclatura de pacote](#Nomenclatura_de_pacote)
*   [2 Empacotamento](#Empacotamento)
*   [3 Exemplos](#Exemplos)
    *   [3.1 Autotools](#Autotools)
    *   [3.2 CMake](#CMake)

## Nomenclatura de pacote

Um pacote para mingw-w64 deve ser nomeado `mingw-w64-*pkgname*`. Se uma variante estática do pacote está sendo compilado, acrescente o sufixo de nome de pacote com `-static` (veja abaixo para os casos nos quais isso é necessário).

## Empacotamento

O empacotamento para pacotes de plataforma cruzada pode ser bastante complicada, pois há muitos sistemas de construção diferentes e peculiaridades de baixo nível. Tome nota das seguintes coisas:

*   sempre adicione [mingw-w64-crt](https://aur.archlinux.org/packages/mingw-w64-crt/) ao `depends`, a menos que ele dependa de outro pacote que implicitamente depende dele
*   sempre adicione [mingw-w64-gcc](https://aur.archlinux.org/packages/mingw-w64-gcc/) ao `makedepends`, a menos que esteja usando [mingw-w64-configure](https://aur.archlinux.org/packages/mingw-w64-configure/) ou [mingw-w64-cmake](https://aur.archlinux.org/packages/mingw-w64-cmake/)
*   sempre adicione `!strip`, `staticlibs` e `!buildflags` ao `options`
*   sempre use o `pkgdesc` original e adicione `(mingw-w64)` ao fim do `pkgdesc`
*   sempre use e siga o `pkgver` original do pacote oficial
*   sempre compile as versões 32 bit e 64 bit das bibliotecas
*   sempre coloque todas as coisas sob o prefixo `/usr/i686-w64-mingw32` e `/usr/x86_64-w64-mingw32`
*   sempre use `any` como a arquitetura (exceto que o pacote contém executáveis que devem ser executados no sistema de compilação)
*   sempre compile os binários compartilhados e estáticos, a menos que eles conflitem
*   considere a remoção de documentação desnecessária (`rm -r $pkgdir/usr/i686-w64-mingw32/share/{doc,info,man}`, `rm -r $pkgdir/usr/x86_64-w64-mingw32/share/{doc,info,man}`)
*   considere usar [mingw-w64-configure](https://aur.archlinux.org/packages/mingw-w64-configure/) para compilação com scripts de configuração
*   considere usar [mingw-w64-cmake](https://aur.archlinux.org/packages/mingw-w64-cmake/) para compilação com CMake
*   considere usar [mingw-w64-qt5-base](https://aur.archlinux.org/packages/mingw-w64-qt5-base/) ou [mingw-w64-qt4](https://aur.archlinux.org/packages/mingw-w64-qt4/) para compilação com QMake
*   considere usar opções de compilação `-D_FORTIFY_SOURCE=2 -O2 -pipe -fno-plt -fexceptions --param=ssp-buffer-size=4` (geralmente nomeadas com CFLAGS, CXXFLAGS) quando nenhum sistema de compilação adequado foi fornecido
*   considere remover símbolos explicitamente com `${_arch}-strip` em loop for `package()` como demonstrado nos exemplos de PKGBUILD abaixo.
    *   considere usar o comando [find](/index.php/Find_(Portugu%C3%AAs) "Find (Português)") para interagir com `$pkgdir` já que todas DLLs, bibliotecas estáticas ou executáveis podem residir em localizações apropriadas.
        *   se o binário é uma DLL, use `${_arch}-strip --strip-unneeded *.dll`
        *   se o binário é uma biblioteca estática, use `${_arch}-strip -g *.a`
*   se um pacote é modular (requer certas dependências de compilação, mas tais dependências são opcionais para o usuário final) adicione essas ao `makedepends` e `optdepends`. Certifique-se de subtrai-los do `depends` se estiver atualizando um pacote existente. Exemplo disto em uso: [mingw-w64-ruby](https://aur.archlinux.org/packages/mingw-w64-ruby/), [mingw-w64-allegro](https://aur.archlinux.org/packages/mingw-w64-allegro/)
*   se um pacote instala um script `$pkgdir/usr/${_arch}/bin/*-config`, crie um link simbólico para `$pkgdir/usr/bin/${_arch}-*-config`
*   se um pacote usa autoconf, defina explicitamente `--build="$CHOST"` no `configure` para contornar o [bug #108405 do autoconf](//savannah.gnu.org/support/?108405) ou usar [mingw-w64-configure](https://aur.archlinux.org/packages/mingw-w64-configure/)

Como mencionado acima, os arquivos devem ser todos instalados em `/usr/i686-w64-mingw32` e `/usr/x86_64-w64-mingw32`. Especificamente, todas as DLLs devem ser colocadas em `/usr/*-w64-mingw32/bin`, pois são bibliotecas dinâmicas necessárias no tempo de execução. Seus arquivos `.dll.a` correspondentes devem ir para `/usr/*-w64-mingw32/lib`. Por favor, exclua qualquer documentação desnecessária e talvez outros arquivos de `/usr/share`. Os pacotes de compilações cruzadas não são destinados ao usuário, mas apenas ao compilador e à distribuição binária, e, como tal, você deve tentar torná-los o menor possível.

Sempre tente combinar o `pkgver` em seus pacotes mingw-w64 com o `pkgver` dos pacotes comuns correspondentes nas repositórios oficiais do Arch Linux (e não nos repos de teste). Isso garante que o software de compilação cruzada funcione exatamente da mesma maneira no Windows, sem nenhum erro inesperado. Se os pacotes no Arch estão desatualizados, geralmente há uma boa razão e você ainda deve seguir a versão do Arch em vez de usar o release upstream mais recente. Se o pacote nativo correspondente estiver no AUR, não será necessário seguir esta política de versão, pois muitos pacotes do AUR são muitas vezes órfãos ou não são mantidos.

## Exemplos

Os exemplos a seguir tentarão cobrir algumas das convenções e sistemas de compilação mais comuns.

### Autotools

```
pkgname=mingw-w64-foo
pkgver=1.0
pkgrel=1
pkgdesc="Foo bar (mingw-w64)"
arch=('any')
url="http://www.foo.bar"
license=('GPL')
makedepends=('mingw-w64-configure')
depends=('mingw-w64-crt')
options=('!strip' '!buildflags' 'staticlibs')
source=("http://www.foo.bar/foobar.tar.gz")
sha256sums=('8f32d4617390d1c2d16f26a27ab60d97807b35440d45891fa340fc2648b04406')

_architectures="i686-w64-mingw32 x86_64-w64-mingw32"

build() {
  cd "${srcdir}/foo-$pkgver/"
  for _arch in ${_architectures}; do
    mkdir -p build-${_arch} && pushd build-${_arch}
    ${_arch}-configure ..
    make
    popd
  done
}

package() {
  for _arch in ${_architectures}; do
    cd "${srcdir}/foo-$pkgver/build-${_arch}"
    make DESTDIR="${pkgdir}" install
    ${_arch}-strip --strip-unneeded "$pkgdir"/usr/${_arch}/bin/*.dll
    ${_arch}-strip -g "$pkgdir"/usr/${_arch}/lib/*.a
  done
}

```

### CMake

```
pkgname=mingw-w64-foo
pkgver=1.0
pkgrel=1
pkgdesc="Foo bar (mingw-w64)"
arch=('any')
url="http://www.foo.bar"
license=('GPL')
makedepends=('mingw-w64-cmake')
depends=('mingw-w64-crt')
options=('!strip' '!buildflags' 'staticlibs')
source=("http://www.foo.bar/foobar.tar.gz")
sha256sums=('8f32d4617390d1c2d16f26a27ab60d97807b35440d45891fa340fc2648b04406')
_architectures="i686-w64-mingw32 x86_64-w64-mingw32"

build() { 
  cd "$srcdir/foo-$pkgver/"
  for _arch in ${_architectures}; do
    mkdir -p build-${_arch} && pushd build-${_arch}
    ${_arch}-cmake ..
    make
    popd
  done
}

package() {
  for _arch in ${_architectures}; do
    cd "${srcdir}/foo-$pkgver/build-${_arch}"
    make DESTDIR="${pkgdir}" install
    ${_arch}-strip --strip-unneeded "$pkgdir"/usr/${_arch}/bin/*.dll
    ${_arch}-strip -g "$pkgdir"/usr/${_arch}/lib/*.a
  done
}

```