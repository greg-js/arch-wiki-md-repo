**Status de tradução:** Esse artigo é uma tradução de [Go package guidelines](/index.php/Go_package_guidelines "Go package guidelines"). Data da última tradução: 2019-01-27\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Go_package_guidelines&diff=0&oldid=564399) na versão em inglês.

**[Diretrizes de criação de pacotes](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Electron](/index.php/Diretrizes_de_pacotes_Electron "Diretrizes de pacotes Electron") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") – [OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [Rust](/index.php/Diretrizes_de_pacotes_Rust "Diretrizes de pacotes Rust") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Esse documento cobra padrões e diretrizes sobre a escrita de [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") para [Go](/index.php/Go "Go").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Diretrizes gerais](#Diretrizes_gerais)
    *   [1.1 Nomenclatura de pacote](#Nomenclatura_de_pacote)
    *   [1.2 Instruções para gerenciadores de dependência alternativos](#Instruções_para_gerenciadores_de_dependência_alternativos)
*   [2 Compilação](#Compilação)
    *   [2.1 Sinalizadores e opções de compilação](#Sinalizadores_e_opções_de_compilação)
    *   [2.2 Projetos Go modernos (para Go >=1.11)](#Projetos_Go_modernos_(para_Go_>=1.11))
    *   [2.3 Projetos Go antigos (para Go <1.11)](#Projetos_Go_antigos_(para_Go_<1.11))
    *   [2.4 Notas sobre dependências e gerenciadores de dependências](#Notas_sobre_dependências_e_gerenciadores_de_dependências)
*   [3 Exemplos de PKGBUILDs](#Exemplos_de_PKGBUILDs)
    *   [3.1 PKGBUILD básico](#PKGBUILD_básico)
    *   [3.2 PKGBUILD com GOPATH e dep](#PKGBUILD_com_GOPATH_e_dep)
*   [4 Exemplos de pacotes](#Exemplos_de_pacotes)

## Diretrizes gerais

### Nomenclatura de pacote

Para módulos de biblioteca [Go](/index.php/Go "Go"), use `go-*nomemódulo*`. Use também o prefixo se o pacote fornecer um programa fortemente acoplado ao ecossistema Go. Para outras aplicações, use apenas o nome do programa.

**Nota:** O nome do pacote deve estar totalmente em minúsculo.

### Instruções para gerenciadores de dependência alternativos

Isso não é necessário para o Go 1.11 e posterior, a menos que um gerenciador de dependências alternativo seja exigido pelo projeto Go que você está empacotando.

Ao preparar as fontes antes de construir, pode ser necessário o seguinte:

*   Crie um diretório `$srcdir/gopath` para [$GOPATH](/index.php/Go#$GOPATH "Go") e copie o código-fonte para esse diretório.
*   Deve-se notar que esta etapa pode não ser necessária se o projeto fornecer um `Makefile` para o projeto que o configura.

```
prepare(){
  mkdir -p gopath/src/github.com/pkgbuild-example
  ln -rTsf $pkgname-$pkgver gopath/src/github.com/pkgbuild-example/$pkgname
  export GOPATH="$srcdir"/gopath

  # as dependências podem ser obtidas aqui, se necessário
  cd gopath/src/github.com/pkgbuild-example/$pkgname
  dep ensure
}

```

## Compilação

Existem nos repositórios dois pacotes go com os quais que você pode compilar; [go](https://www.archlinux.org/packages/?name=go) e [go-pie](https://www.archlinux.org/packages/?name=go-pie). Todos os pacotes devem ser compilados preferencialmente com o [go-pie](https://www.archlinux.org/packages/?name=go-pie), pois isso nos permite entregar binários seguros. No entanto, como upstream pode ter bugs, compilar com o [go](https://www.archlinux.org/packages/?name=go) deve ser o último recurso.

### Sinalizadores e opções de compilação

A maioria dos Makefiles escritos para aplicativos go não respeitam o `LDFLAGS` fornecido pelos sistemas de compilação, isso faz com que os binários do Go não sejam compilados com o RELRO. Isso precisa ser corrigido no Makefile, ou o Makefile deve ser omitido. Se houver um Makefile envolvido, você tem 3 opções para suportar o RELRO:

*   Aplicar um patch no Makefile
*   Ignorar o Makefile completamente e usar `go build`
*   Exportar `GOFLAGS` - Isso é menos desejável, pois estaremos descartando sinalizadores do `LDFLAGS`.

Para [reproducible builds](https://reproducible-builds.org/), é importante que os binários sejam removidos do caminho de compilação usando os sinalizadores `-trimpath`.

```
# LDFLAGS na variável de ambiente GOFLAGS.
export GOFLAGS="-gcflags=all=-trimpath=${PWD} -asmflags=all=-trimpath=${PWD} -ldflags=-extldflags=-zrelro -ldflags=-extldflags=-znow"

# ou, alternativamente, use LDFLAGS definido no go build.
go build \
    -gcflags "all=-trimpath=${PWD}" \
    -asmflags "all=-trimpath=${PWD}" \
    -ldflags "-extldflags ${LDFLAGS}" \
    .

```

**Nota:** Por uma questão de brevidade, esses sinalizadores são omitidos nos exemplos abaixo.

### Projetos Go modernos (para Go >=1.11)

Go 1.11 introduz [go modules](https://github.com/golang/go/wiki/Modules). Isso omite a necessidade de configuração `GOPATH` e nós podemos compilar diretamente no diretório.

Projetos como esses têm um arquivo `go.mod` e um `go.sum`.

**Nota:** Essas compilações precisam de `$PWD` retirado do binário.

```
build(){
  cd $pkgname-$pkgver
  go build .
}

```

### Projetos Go antigos (para Go <1.11)

Ao compilarmos pacotes com [$GOPATH](/index.php/Go#$GOPATH "Go"), existem alguns problemas que você pode encontrar. Normalmente o projeto entrega um `Makefile` que pode ser usado e deve ser usado. Existem casos em que você ainda precisa configurar um `$GOPATH` no [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)"). O trecho a seguir configura um `GOPATH` dentro de `$srcdir/gopath` que pode ser usado para compilar pacotes. Um novo diretório é usado, já que alguns gerenciador de dependências fazem coisas estranhas se descobrirem o projeto na raiz do `$GOPATH`.

**Nota:** Essas compilações devem ter `$GOPATH` removidos do binário.

```
prepare(){
  mkdir -p gopath/src/github.com/pkgbuild-example
  ln -rTsf $pkgname-$pkgver gopath/src/github.com/pkgbuild-example/$pkgname

  # as dependências podem ser obtidas aqui se necessário
  cd gopath/src/github.com/pkgbuild-example/$pkgname
  dep ensure
}

build(){
  export GOPATH="$srcdir"/gopath
  cd gopath/src/github.com/pkgbuild-example/$pkgname
  go install -v .
}

```

Note `install` e `build`, e que podem ser feitas compilações recursivas se você tiver um subdiretório `cmd/` com múltiplos binários: `go install -v github.com/pkgbuild-example/cmd/...`

### Notas sobre dependências e gerenciadores de dependências

Os pacotes Go atualmente usam a pasta `vendor/` para lidar com dependências em projetos. Geralmente, eles são gerenciados por um dos vários projetos do gerenciador de dependências. Se um for usado para o pacote, este passo deve ser executado na função [prepare()](/index.php/Criando_pacotes#prepare() "Criando pacotes") do [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)").

Dependências são normalmente gerenciadas pelo comando `go mod`, que vem com o Go 1.11 ou posterior.

Existem também gerenciadores de dependência alternativos:

*   [dep](https://www.archlinux.org/packages/?name=dep)
*   [godep](https://www.archlinux.org/packages/?name=godep)
*   [glide](https://www.archlinux.org/packages/?name=glide)

## Exemplos de PKGBUILDs

### PKGBUILD básico

```
pkgname=foo
pkgver=0.0.1
pkgrel=1
pkgdesc='Go PKGBUILD Example'
arch=('x86_64')
url='https://example.org/$pkgname'
license=('GPL')
makedepends=('go-pie')
source=("$url/$pkgname-$pkgver.tar.gz")
sha256sums=('1337deadbeef')

build() {
  cd $pkgname-$pkgver
  go build \
    -gcflags "all=-trimpath=$PWD" \
    -asmflags "all=-trimpath=$PWD" \
    -ldflags "-extldflags $LDFLAGS" \
    -o $pkgname .
}

package() {
  cd $pkgname-$pkgver
  install -Dm755 $pkgname "$pkgdir"/usr/bin/$pkgname
}

```

### PKGBUILD com GOPATH e dep

```
pkgname=foo
pkgver=0.0.1
pkgrel=1
pkgdesc='Go PKGBUILD Example'
arch=('x86_64')
url='https://example.org/$pkgname'
license=('GPL')
makedepends=('go-pie' 'dep')
source=("$url/$pkgname-$pkgver.tar.gz")
sha256sums=('1337deadbeef')

prepare(){
  mkdir -p gopath/src/example.org/foo
  ln -rTsf $pkgname-$pkgver gopath/src/example.org/foo
  cd gopath/src/example.org/foo
  dep ensure
}

build() {
  export GOPATH="$srcdir"/gopath
  cd gopath/src/example.org/foo
  go install \
    -gcflags "all=-trimpath=$GOPATH" \
    -asmflags "all=-trimpath=$GOPATH" \
    -ldflags "-extldflags $LDFLAGS" \
    -v ./...
}

check() {
  export GOPATH="$srcdir"/gopath
  cd gopath/src/example.org/foo
  go test ./...
}

package() {
  install -Dm755 gopath/bin/$pkgname "$pkgdir"/usr/bin/$pkgname
}

```

## Exemplos de pacotes

*   [dep](https://www.archlinux.org/packages/?name=dep)
*   [gopass](https://www.archlinux.org/packages/?name=gopass)
*   [delve](https://www.archlinux.org/packages/?name=delve)
*   [gitea](https://www.archlinux.org/packages/?name=gitea)
*   [git-lfs](https://www.archlinux.org/packages/?name=git-lfs)