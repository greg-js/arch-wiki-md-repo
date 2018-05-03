**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

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

Tenha em mente que muitos pacotes OCaml frequentemente precisarão de parâmetros extras para o `make` e `make install`. Lembre-se também de remover a opção **!strip** e alterar a arquitetura se o pacote não produzir bytecode.