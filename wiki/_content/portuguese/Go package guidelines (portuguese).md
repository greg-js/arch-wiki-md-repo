**Status de tradução:** Esse artigo é uma tradução de [Go package guidelines](/index.php/Go_package_guidelines "Go package guidelines"). Data da última tradução: 2018-11-03\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Go_package_guidelines&diff=0&oldid=552778) na versão em inglês.

**[Diretrizes de criação de pacotes](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") –[OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

[Go](https://en.wikipedia.org/wiki/pt:Go_(linguagem_de_programa%C3%A7%C3%A3o) também encontra suporte no Arch Linux.

O pacote [go](https://www.archlinux.org/packages/?name=go) contém a ferramenta **go** (para executar `go fix`, `go build` etc). Também há [gcc-go](https://www.archlinux.org/packages/?name=gcc-go) que fornece `gccgo`.

## Contents

*   [1 Diretrizes gerais](#Diretrizes_gerais)
    *   [1.1 Nomenclatura](#Nomenclatura)
    *   [1.2 Empacotamento](#Empacotamento)
*   [2 Exemplos de PKGBUILDs](#Exemplos_de_PKGBUILDs)
    *   [2.1 Exemplo de PKGBUILD para um aplicativo escrito em Go](#Exemplo_de_PKGBUILD_para_um_aplicativo_escrito_em_Go)
        *   [2.1.1 Exemplos de pacotes](#Exemplos_de_pacotes)
    *   [2.2 Exemplo de PKGBUILD para quando apenas um único arquivo fonte está disponível](#Exemplo_de_PKGBUILD_para_quando_apenas_um_.C3.BAnico_arquivo_fonte_est.C3.A1_dispon.C3.ADvel)
        *   [2.2.1 Exemplos de pacotes](#Exemplos_de_pacotes_2)
    *   [2.3 Exemplos de PKGBUILDs para bibliotecas Go que também incluem executáveis](#Exemplos_de_PKGBUILDs_para_bibliotecas_Go_que_tamb.C3.A9m_incluem_execut.C3.A1veis)
        *   [2.3.1 Usando *go get*](#Usando_go_get)
        *   [2.3.2 Usando *go get*](#Usando_go_get_2)

## Diretrizes gerais

### Nomenclatura

*   Para aplicativos escritos em Go, use o nome do aplicativo como o nome do pacote, em letras minúsculas.
    *   Seja criativo se o nome já estiver sendo usado.
*   Para o PKGBUILDS que usa a ferramenta "go" para baixar o pacote, adicione apenas "-git" ao nome do pacote, se ele não for construído a partir de um tarball ou de um lançamento marcado (mas do trunk/HEAD).
    *   Da mesma forma, para pacotes mercurial, adicione apenas "-hg" ao nome do pacote, se não for uma revisão de versão.
    *   Estenda esse padrão para outros sistemas de controle de versão.
    *   A ferramenta go tem sua própria lógica para qual branch ou tag deve ser usada. Veja `go get --help`.
*   Considere adicionar o nome do autor ao nome do pacote se houver vários aplicativos com o mesmo nome, como [dcpu16-kballard](https://aur.archlinux.org/packages/dcpu16-kballard/).
    *   Em geral, os pacotes mais populares devem poder usar o nome mais curto ou "melhor".
*   Correções posteriores para os nomes dos pacotes (como `-hg`, `-git` ou `-svn`) são opcionais se não houver versões oficiais do projeto em questão. Por um lado, é comum usá-los quando o pacote é baixado de um VCS. Por outro lado, a maioria dos projetos Go não possui tarballs de lançamento, apenas o repositório que é usado para branching/tagging o release oficial, se não for *trunk*. Além disso, o `go get`, que é a maneira "oficial" de instalar os módulos do Go, usa os repositórios diretamente. Use seu melhor julgamento.

### Empacotamento

*   Os projetos Go são apenas arquivos de biblioteca, apenas executáveis ou ambos. Escolha a maneira apropriada de empacotá-los. Existem vários exemplos abaixo.
*   Alguns aplicativos ou bibliotecas do Go ainda não foram atualizados para a versão mais recente do Go.
    *   A execução de `go build -fix`  muitas vezes pode funcionar, mas pode ter de ser corrigida pelo desenvolvedor. Relate um problema upstream, se este for o caso.
*   Vários projetos do Go não possuem um número de versão ou um arquivo de licença.
    *   Use license=('unknown') e relate um problema ao desenvolvedor se um arquivo de licença estiver faltando.
    *   Use a versão "0.1", "1" ou a git-revision (ou equivalente para outros sistemas de controle de versão) se o número da versão estiver faltando.
    *   Como alternativa, use a data atual como o número da versão, desta forma `AAAAMMDD`.

## Exemplos de PKGBUILDs

### Exemplo de PKGBUILD para um aplicativo escrito em Go

```
# Maintainer: NOME <EMAIL>

pkgname=NOME PACOTE
pkgver=1.2.3
pkgrel=1
pkgdesc="DESCRIÇÃO PACOTE"
arch=('x86_64')
url="http://SERVIDOR/$pkgname/"
license=('MIT')
makedepends=('go')
options=('!strip' '!emptydirs')
source=("http://SERVIDOR/$pkgname/$pkgname-$pkgver.tar.gz")
sha256sums=('00112233445566778899aabbccddeeff')

build() {
  cd "$pkgname-$pkgver"

  go build
}

package() {
  cd "$pkgname-$pkgver"

  install -Dm755 "$pkgname-$pkgver" "$pkgdir/usr/bin/$pkgname"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim:set ts=2 sw=2 et:
```

#### Exemplos de pacotes

*   [gendesk](https://www.archlinux.org/packages/?name=gendesk)
*   [dcpu16](https://aur.archlinux.org/packages/dcpu16/)

### Exemplo de PKGBUILD para quando apenas um único arquivo fonte está disponível

```
# Maintainer: NOME <EMAIL>

pkgname=NOME PACOTE
pkgver=1.2.3
pkgrel=1
pkgdesc="DESCRIÇÃO PACOTE"
arch=('x86_64')
url="http://SERVIDOR/$pkgname/"
license=('GPL3')
makedepends=('go')
options=('!strip' '!emptydirs')
source=("http://SERVIDOR/$pkgname/$pkgname.go")
sha256sums=('00112233445566778899aabbccddeeff')

build() {
  go build -o "$pkgname"
}

package() {
  install -Dm755 "$pkgname" "$pkgdir/usr/bin/$pkgname"
}

# vim:set ts=2 sw=2 et:
```

#### Exemplos de pacotes

*   [gorun](https://aur.archlinux.org/packages/gorun/)

### Exemplos de PKGBUILDs para bibliotecas Go que também incluem executáveis

#### Usando *go get*

Esta é a forma recomendada, em vez do método acima.

Aqui está uma forma que depende do go get.

Você provavelmente não precisará modificar as funções build() ou package(), apenas as variáveis no topo (pkgname etc).

Se isso não funcionar, teste com got get primeiro.

**Nota:** Remova `/...` se o PKGBUILD falhar!

```
# Maintainer: NOME <EMAIL>

pkgname=codesearch
pkgver=20120515
pkgrel=1
pkgdesc="Code indexing and search written in Go"
arch=('x86_64')
url="https://github.com/google/codesearch"
license=('BSD')
depends=('go')
makedepends=('mercurial')
options=('!strip' '!emptydirs')
_gourl=github.com/google/codesearch

build() {
  GOPATH="$srcdir" go get -fix -v -x ${_gourl}/...
}

check() {
  GOPATH="$GOPATH:$srcdir" go test -v -x ${_gourl}/...
}

package() {
  mkdir -p "$pkgdir/usr/bin"
  install -p -m755 "$srcdir/bin/"* "$pkgdir/usr/bin"

  mkdir -p "$pkgdir/$GOPATH"
  cp -Rv --preserve=timestamps "$srcdir/"{src,pkg} "$pkgdir/$GOPATH"

  # Package license (if available)
  for f in LICENSE COPYING LICENSE.* COPYING.*; do
    if [ -e "$srcdir/src/$_gourl/$f" ]; then
      install -Dm644 "$srcdir/src/$_gourl/$f" \
        "$pkgdir/usr/share/licenses/$pkgname/$f"
    fi
  done
}

# vim:set ts=2 sw=2 et:
```

Obrigado a Rémy Oudompheng‎ por este aqui.

#### Usando *go get*

Aqui está uma outra forma que depende de `go get`.

Você provavelmente não precisará modificar as funções build() ou package(), apenas as variáveis no topo (pkgname etc). If this does not work, test with `go get` first.

```
# Maintainer: NOME <EMAIL>

pkgname=NOME PACOTE
pkgver=1.2.3
pkgrel=1
pkgdesc="DESCRIÇÃO PACOTE"
arch=('x86_64')
url="http://SERVIDOR/$pkgname/"
license=('MIT')
makedepends=('go' 'git')
options=('!strip' '!emptydirs')
_gourl=SERVIDOR.NET/CAMINHO/NOMEMÓDULO

build() {
  export GOROOT=/usr/lib/go

  rm -rf build
  mkdir -p build/go
  cd build/go

  for f in "$GOROOT/"*; do
    ln -s "$f"
  done

  rm pkg
  mkdir pkg
  cd pkg

  for f in "$GOROOT/pkg/"*; do
    ln -s "$f"
  done

  platform=`for f in "$GOROOT/pkg/"*; do echo \`basename $f\`; done|grep linux`

  rm -f "$platform"
  mkdir "$platform"
  cd "$platform"

  for f in "$GOROOT/pkg/$platform/"*.h; do
    ln -s "$f"
  done

  export GOROOT="$srcdir/build/go"
  export GOPATH="$srcdir/build"

  go get -fix "$_gourl"

  # Prepare executable
  if [ -d "$srcdir/build/src" ]; then
    cd "$srcdir/build/src/$_gourl"
    go build -o "$srcdir/build/$pkgname"
  else
    echo 'Old sources for a previous version of this package are already present!'
    echo 'Build in a chroot or uninstall the previous version.'
    return 1
  fi
}

package() {
  export GOROOT="$GOPATH"

  # Package go package files
  for f in "$srcdir/build/go/pkg/"* "$srcdir/build/pkg/"*; do
    # If it's a directory
    if [ -d "$f" ]; then
      cd "$f"
      mkdir -p "$pkgdir/$GOROOT/pkg/`basename $f`"
      for z in *; do
        # Check if the directory name matches
        if [ "$z" == `echo $_gourl | cut -d/ -f1` ]; then
          cp -r $z "$pkgdir/$GOROOT/pkg/`basename $f`"
        fi
      done
      cd ..
    fi
  done

  # Package source files
  if [ -d "$srcdir/build/src" ]; then
    mkdir -p "$pkgdir/$GOROOT/src/pkg"
    cp -r "$srcdir/build/src/"* "$pkgdir/$GOROOT/src/pkg/"
    find "$pkgdir" -depth -type d -name .git -exec rm -r {} \;
  fi

  # Package license (if available)
  for f in LICENSE COPYING; do
    if [ -e "$srcdir/build/src/$_gourl/$f" ]; then
      install -Dm644 "$srcdir/build/src/$_gourl/$f" \
        "$pkgdir/usr/share/licenses/$pkgname/$f"
    fi
  done

  # Package executables
  if [ -e "$srcdir/build/$pkgname" ]; then
    install -Dm755 "$srcdir/build/$pkgname" \
      "$pkgdir/usr/bin/$pkgname"
  fi
}

# vim:set ts=2 sw=2 et:
```