**Status de tradução:** Esse artigo é uma tradução de [OCaml package guidelines](/index.php/OCaml_package_guidelines "OCaml package guidelines"). Data da última tradução: 2018-11-04\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=OCaml_package_guidelines&diff=0&oldid=553087) na versão em inglês.

**[Diretrizes de criação de pacotes](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") –[OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Escrita de [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") para softwares escritos em [OCaml](https://en.wikipedia.org/wiki/pt:OCaml "wikipedia:pt:OCaml").

## Contents

*   [1 Nomenclatura de pacote](#Nomenclatura_de_pacote)
*   [2 Colocação de arquivos](#Coloca.C3.A7.C3.A3o_de_arquivos)
    *   [2.1 Bibliotecas](#Bibliotecas)
    *   [2.2 OASIS](#OASIS)
*   [3 Níveis e bytecode OCaml](#N.C3.ADveis_e_bytecode_OCaml)
*   [4 Exemplo de PKGBUILD](#Exemplo_de_PKGBUILD)

## Nomenclatura de pacote

Para bibliotecas, use `ocaml-*nomemodulo*`. Para aplicativos, use o nome do programa. Em ambos casos, o nome deve ser totalmente minúsculo.

## Colocação de arquivos

### Bibliotecas

As bibliotecas OCaml devem ser instaladas sob `/usr/lib/ocaml`. A instalação em `/usr/lib/ocaml/site-lib` está obsoleto.

As bibliotecas OCaml devem ser instaladas usando [ocaml-findlib](https://www.archlinux.org/packages/?name=ocaml-findlib). `ocaml-findlib` inclui metadados de biblioteca no pacote que facilita a gerência fr bibliotecas. Esse é um padrão *de fato* e muitos softwares OCaml agora precisam dele.

`ocaml-findlib` extrai dados necessários de um arquivo chamado `META` que deve ser incluído no arquivo de origem. Se este arquivo não estiver incluído, um deve ser obtido do pacote Debian, Ubuntu ou Fedora correspondente, ou criado para o pacote pelo mantenedor. Uma solicitação para incluir o arquivo também deve ser feita para os desenvolvedores upstream do pacote.

A variável `OCAMLFIND_DESTDIR` deve ser usada ao instalar pacotes com `ocaml-findlib`. Veja o exemplo de PKGBUILD abaixo para detalhes.

### OASIS

Os pacotes OCaml que instalam executáveis usando OASIS ignoram `DESTDIR`. Essa é uma limitação conhecida do OASIS ([issue #852](https://forge.ocamlcore.org/tracker/?func=detail&atid=294&aid=852&group_id=54)). Uma forma de habilitar funcionalidade do `DESTDIR` é executar o script `configure` com o argumento `--destdir`, dessa forma:

```
build() {
    cd "${srcdir}/${srcname}-${pkgver}"
    ./configure --prefix /usr --destdir "$pkgdir"

    # build commands
}
```

## Níveis e bytecode OCaml

O OCaml pode executar código em múltiplos "níveis", o nível superior interpreta o Código OCaml sem compilar, o nível de bytecode cria bytecode independente de máquina e o nível nativo cria binários de código de máquina (assim como C/C++).

Ao compilar Pacotes OCaml, você precisa estar ciente de que o processo de compilação está compilando código de máquina nativo, bytecode ou, como em muitos casos, ambos. Isso cria várias situações que podem causar problemas com as opções de pacote e as dependências corretas.

Se o bytecode for produzido, o PKGBUILD deverá conter o seguinte para proteger o bytecode:

```
options=('!strip')

```

Se o pacote não contiver bytecode e apenas distribuir um binário, então `ocaml` não é necessário como uma dependência, mas é claro que é necessário como um makedepends desde que o pacote `ocaml` fornece o OCaml compilador. Se o pacote contiver código nativo e bytecode, `ocaml` deve ser uma dependência e um makedepends.

O código OCaml é raramente (ou nunca) distribuído apenas como bytecode e quase sempre incluirá código nativo: o único caso em que usar *any* como o *arch* é aconselhável é quando apenas código-fonte não compilado é distribuído, geralmente com uma biblioteca, embora muitas bibliotecas ainda distribuam código nativo.

A moral da história aqui é estar ciente do que você está distribuindo, as chances são de que o seu pacote contenha código nativo de máquina e bytecode.

## Exemplo de PKGBUILD

```
# Contributor: Seu Nome <seuemail@dominio.com.br>

pkgname=ocaml-<nome_pacote>
pkgver=4.2
pkgrel=1
license=(*)*
arch=('i686' 'x86_64')
pkgdesc="An OCaml Package"
url=""
depends=('ocaml')
makedepends=('ocaml-findlib')
source=()
options=('!strip')
md5sums=()

OCAMLFIND_DESTDIR="${pkgdir}$(ocamlfind printconf destdir)"

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  mkdir -p "$OCAMLFIND_DESTDIR"
  ./configure --prefix=/usr
  make
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  env DESTDIR="${pkgdir}" \
    OCAMLFIND_DESTDIR="$OCAMLFIND_DESTDIR" \
    make install
}
```

Tenha em mente que muitos pacotes OCaml frequentemente precisarão de parâmetros extras para o `make` e `make install`. Lembre-se também de remover a opção `!strip` e alterar a arquitetura se o pacote não produzir bytecode.