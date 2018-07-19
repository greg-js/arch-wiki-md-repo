**[Diretrizes de criação de pacotes](/index.php/Criando_pacotes "Criando pacotes")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") –[OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

[Sistema de controle de versões](https://en.wikipedia.org/wiki/pt:Sistema_de_controle_de_vers%C3%B5es "wikipedia:pt:Sistema de controle de versões") pode ser usado para obter o códifo fonte para tanto pacotes versionados estaticamente quanto a última versão (*trunk*) de um ramo de desenvolvimento. Esse artigo cobre ambos casos.

## Contents

*   [1 Protótipos](#Prot.C3.B3tipos)
*   [2 Diretrizes](#Diretrizes)
    *   [2.1 Fontes VCS](#Fontes_VCS)
    *   [2.2 A função pkgver()](#A_fun.C3.A7.C3.A3o_pkgver.28.29)
        *   [2.2.1 Git](#Git)
        *   [2.2.2 Subversion](#Subversion)
        *   [2.2.3 Mercurial](#Mercurial)
        *   [2.2.4 Bazaar](#Bazaar)
        *   [2.2.5 Reserva](#Reserva)
*   [3 Dicas](#Dicas)
    *   [3.1 Submódulos git](#Subm.C3.B3dulos_git)

## Protótipos

Use apenas os protótipos de PKGBUILD fornecidos pelo pacote [pacman](https://www.archlinux.org/packages/?name=pacman) (`PKGBUILD-split.proto`, `PKGBUILD-vcs.proto` e `PKGBUILD.proto` em `/usr/share/pacman`).

## Diretrizes

*   Adicione um sufixo a `pkgname` com `-cvs`, `-svn`, `-hg`, `-darcs`, `-bzr`, `-git` etc. a menos que o pacote obtenha uma versão especifíca.

*   Se o pacote resultante for diferente depois de alterar as dependências, URL, fontes, etc., aumentar o `pkgrel` é obrigatório. Tocar no `pkgver` não é.

*   `--holdver` pode ser usado para evitar que [makepkg (Português)](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") atualize o `pkgver` (veja: [makepkg(8)](https://www.archlinux.org/pacman/makepkg.8.html))

*   Inclua o que o pacote conflita com e fornece (p.ex. para [fluxbox-git](https://aur.archlinux.org/packages/fluxbox-git/): `conflicts=('fluxbox')` e `provides=('fluxbox')`).

*   `replaces=()` geralmente causa problemas desnecessários e deve ser evitado.

*   Ao usar o cvsroot, use `anonymous:@` em vez de `anonymous@` para evitar ter que digitar uma senha em branco ou `anonymous:senha@`, se uma for exigida.

*   Inclua a ferramenta de VCS apropriada em `makedepends=()` ([cvs](https://www.archlinux.org/packages/?name=cvs), [subversion](https://www.archlinux.org/packages/?name=subversion), [git](https://www.archlinux.org/packages/?name=git), ...).

*   Porque os fontes não são estáticos, ignore a verificação de soma em `md5sums=()` adicionando `'SKIP'`.

### Fontes VCS

**Nota:** O pacman 4.1 possui suporte aos seguintes fontes VCS: `bzr`, `git`, `hg` and `svn`. Veja a seção `fragment` do [PKGBUILD(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/PKGBUILD.5) ou [PKGBUILD(5)](https://www.archlinux.org/pacman/PKGBUILD.5.html) para uma lista de VCS suportados.

A partir do [pacman](https://www.archlinux.org/packages/?name=pacman) 4.1, os fontes VCS devem ser especificados no vetor `source=()` e será tratado como qualquer outro fonte. `makepkg` vai realizar *clone*/*checkout*/*branch* do repositório para `$SRCDEST` (mesmo que `$startdir` se não definido no [makepkg.conf(5)](https://www.archlinux.org/pacman/makepkg.conf.5.html)) e vai copiá-lo para `$srcdir` (em uma forma específica para cada VCS). O repositório local é deixado intocado, portanto passando a ser desnecessário ter um diretório `-build`.

O formato geral de um vetor `source=()` de VCS é:

```
source=('[pasta::][vcs+]url[#fragmento]')

```

*   `pasta` (opcional) é usada para alterar o nome do repositório padrão para algo mais relevante (p. ex., do que `trunk`) ou para preservar os fontes anteriores.
*   `vcs+` é necessário para URLs que não refletem o tipo VCS, p. ex., `git+http://algum_repo`.
*   `url` é o URL para o repositório distante ou local.
*   `#fragmento` (opcional) é necessário para fazer *pull* um *branch* ou *commit* específico. Veja [PKGBUILD(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/PKGBUILD.5) para mais informações nos fragmentos disponíveis para cada VCS.

Um exemplo de vetor fonte de Git:

```
source=('nome_projeto::git+http://url_projeto#branch=ramo_projeto')

```

### A função pkgver()

O autoincremento de `pkgver` agora é alcançado através de uma função `pkgver()` dedicada. Isso permite um melhor controle sobre o `pkgver`, e os mantenedores devem favorecer um `pkgver` que faça sentido. Para usar `pkgver()`, você ainda precisa declarar a variável `pkgver` com o valor mais recente. O makepkg irá invocar a função `pkgver()` e atualizar a variável `pkgver` de acordo.

Recomenda-se ter o seguinte formato de versão: *LANÇAMENTO.rREVISÃO* onde *REVISÃO* é um número monotonicamente crescente que identifica exclusivamente a árvore de fonte (revisões VCS fazem isso). Se não houver lançamentos públicos e nenhuma tag de repositório, o zero pode ser usado como um número de release ou você pode descartar *LANÇAMENTO* e usar o número da versão que se parece com *rREVISÃO*. Se houver lançamentos públicos, mas o repo não tiver tags, o desenvolvedor deve obter a versão de lançamento de alguma forma, por exemplo, analisando os arquivos do projeto.

O delimitador do número de revisão ("r" logo antes da REVISÃO) é importante. Esse delimitador permite evitar problemas caso o upstream decida fazer seu primeiro lançamento ou use versões com diferentes números de componentes. Por exemplo, se na revisão "455" o upstream decidir lançar a versão 0.1, o delimitador de revisão preservará a monotonicidade da versão - `0.1.r456 > r454`. Sem o delimitador, a monotonicidade falha - `0.1.456 < 454`.

Veja [PKGBUILD-vcs.proto](https://projects.archlinux.org/pacman.git/tree/proto/PKGBUILD-vcs.proto#n33) para exemplos genéricos mostrando a saúde visada.

#### Git

Usando a tag anotada mais recente alcançável do último commit:

```
pkgver() {
  cd "$pkgname"
  git describe --long | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}
```

```
2.0.r6.ga17a017

```

Usando a tag não anotada mais recente alcançável do último commit:

```
pkgver() {
  cd "$pkgname"
  git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}
```

```
0.71.r115.gd95ee07

```

No caso, se a tag git não contém traços, então pode-se usar uma expressão sed mais simples, como `sed 's/-/.r/;s/-/./'`.

Se a tag contiver um prefixo, como `v` ou o nome do projeto, ele deverá ser cortado:

```
pkgver() {
  cd "$pkgname"
  # cutting off 'foo-' prefix that presents in the git tag
  git describe --long | sed 's/^foo-//;s/\([^-]*-g\)/r\1/;s/-/./g'
}
```

```
6.1.r3.gd77e105

```

Se não houver tags, use o número de revisões desde o início do histórico:

```
pkgver() {
  cd "$pkgname"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}
```

```
r1142.a17a017

```

Versão e somente o commit/número da revisão (SHA1 omitido; no entanto, sem uma referência rápida SHA1 de uma revisão exata, ela é perdida se não estiver atento ao controle de versão):

```
git describe --long | sed -r 's/-([0-9,a-g,A-G]{7}.*)//' | sed 's/-/./'

```

Ambos os métodos também podem ser combinados, para suportar repositórios que iniciam sem uma tag, mas são marcados mais tarde (use um bashismo):

```
pkgver() {
  cd "$pkgname"
  ( set -o pipefail
    git describe --long 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  )
}
```

```
0.9.9.r27.g2b039da  # if tags exist
r1581.2b039da       # else fallback

```

#### Subversion

```
pkgver() {
  cd "$pkgname"
  local ver="$(svnversion)"
  printf "r%s" "${ver//[[:alpha:]]}"
}
```

```
r8546

```

**Nota:** Se o projeto tiver lançamentos, você deve usá-los em vez do `0.`.

#### Mercurial

```
pkgver() {
  cd "$pkgname"
  printf "r%s.%s" "$(hg identify -n)" "$(hg identify -i)"
}
```

```
r2813.75881cc5391e

```

#### Bazaar

```
pkgver() {
  cd "$pkgname"
  printf "r%s" "$(bzr revno)"
}
```

```
r830

```

#### Reserva

Caso nenhum `pkgver` satisfatório possa ser extraído do repositório, a data atual pode ser usada:

```
pkgver() {
  date +%Y%m%d
}
```

```
20130408

```

Embora não identifique o estado da árvore de fonte de forma exclusiva, então evite-o, se possível.

## Dicas

### Submódulos git

Submódulos de Git são um pouco complicados de se fazer. A ideia é adicionar as URLs dos submódulos diretamente ao vetor de fontes e, em seguida, referenciá-las durante o prepare(). Isso poderia ser assim:

```
source=("git://algumlugar.org/algumacoisa/algumacoisa.git"
        "git://algumlugar.org/meusubmódulo/meusubmódulo.git")

prepare() {
  cd something
  git submodule init
  git config submodule.meusubmódulo.url $srcdir/meusubmódulo
  git submodule update
}

```