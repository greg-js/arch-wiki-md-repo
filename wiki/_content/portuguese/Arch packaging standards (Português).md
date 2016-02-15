**Os PKGBUILDs enviados não devem compilar aplicativos que já estejam em quaisquer dos repositórios de binários oficiais em qualquer circunstância. Exceção a esta regra estrita pode ser pacotes que tenha recursos extras habilitados e/ou patches em comparação aos oficiais. Nesta ocasião, o vetor pkgname deve ser diferente.**

Ao compilar pacotes para o Arch Linux, **siga as diretrizes de empacotamento** abaixo, especialmente a intenção é **contribuir** com um novo pacote para o Arch Linux. Você também deveria ler as páginas man do [PKGBUILD](https://archlinux.org/pacman/PKGBUILD.5.html) e do [makepkg](https://archlinux.org/pacman/makepkg.8.html).

## Contents

*   [1 Protótipo de PKGBUILD](#Prot.C3.B3tipo_de_PKGBUILD)
*   [2 Etiqueta de pacotes](#Etiqueta_de_pacotes)
*   [3 Nomenclatura de pacotes](#Nomenclatura_de_pacotes)
*   [4 Diretórios](#Diret.C3.B3rios)
*   [5 Tarefas do Makepkg](#Tarefas_do_Makepkg)
*   [6 Arquiteturas](#Arquiteturas)
*   [7 Licenças](#Licen.C3.A7as)
*   [8 Enviando pacotes para o AUR](#Enviando_pacotes_para_o_AUR)
*   [9 Diretrizes adicionais](#Diretrizes_adicionais)
    *   [9.1 Pacotes de CVS (SVN, GIT, HG etc.)](#Pacotes_de_CVS_.28SVN.2C_GIT.2C_HG_etc..29)
    *   [9.2 Pacotes de plug-ins do Eclipse](#Pacotes_de_plug-ins_do_Eclipse)
    *   [9.3 Pacotes de GNOME](#Pacotes_de_GNOME)
    *   [9.4 Pacotes de Go](#Pacotes_de_Go)
    *   [9.5 Pacotes de Haskell](#Pacotes_de_Haskell)
    *   [9.6 Pacotes de Java](#Pacotes_de_Java)
    *   [9.7 Pacotes do KDE](#Pacotes_do_KDE)
    *   [9.8 Pacotes de módulos de kernel](#Pacotes_de_m.C3.B3dulos_de_kernel)
    *   [9.9 Pacotes de Lisp](#Pacotes_de_Lisp)
    *   [9.10 Pacotes de OCaml](#Pacotes_de_OCaml)
    *   [9.11 Pacotes de Perl](#Pacotes_de_Perl)
    *   [9.12 Pacotes de Python](#Pacotes_de_Python)
    *   [9.13 Pacotes de Ruby Gem](#Pacotes_de_Ruby_Gem)
    *   [9.14 Pacotes de Wine](#Pacotes_de_Wine)
    *   [9.15 Pacotes de MinGW](#Pacotes_de_MinGW)

## Protótipo de PKGBUILD

```
# Maintainer: Seu nome <seu-email@domínio.com>
pkgname=NOME
pkgver=VERSÃO
pkgrel=1
pkgdesc=""
arch=()
url=""
license=('GPL')
groups=()
depends=()
makedepends=()
optdepends=()
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=
changelog=
source=($pkgname-$pkgver.tar.gz)
noextract=()
md5sums=() #gerado com 'makepkg -g'

build() {
  cd "$srcdir/$pkgname-$pkgver"

  ./configure --prefix=/usr
  make
}

package() {
  cd "$srcdir/$pkgname-$pkgver"

  make DESTDIR="$pkgdir/" install
}
```

Outros protótipos podem ser encontrados em `/usr/share/pacman` dos pacotes `pacman` e `abs`.

## Etiqueta de pacotes

*   Os pacotes **nunca** devem ser instalados em `/usr/local`
*   **Não introduza novas variáveis** em scripts de compilação `PKGBUILD`, a menos que o pacote não possa ser compilado sem elas, pois elas podem **conflitar** com variáveis usadas pelo próprio makepkg. Se uma nova variável for absolutamente necessária, **acrescente, antes da variável, um underscore** (`_`), ex: `_variavelpersonalizada=` 

    O AUR não consegue detectar o uso de variáveis personalizadas e, portanto, não consegue usar em substituições. Isso normalmente pode ser visto em vertores de fontes. Ex:

     `http://downloads.sourceforge.net/directxwine/$patchname.$patchver.diff.bz2` 

    Tal situação acaba com a funcionalidade efetiva do AUR.

*   **Evite** usar `/usr/libexec/` para qualquer coisa. Ao invés disso, use `/usr/lib/${pkgname}/`.
*   O campo `packager` do meta arquivo do pacote pode ser **personalizado** para compilador do pacote, modificando a opção apropriada no arquivo `/etc/makepkg.conf` ou, alternativamente, sobrescrevendo-o com a criação de um ~/.makepkg.conf
*   Todas as mensagenjs importantes deveriam ser exibidas durante a isntalação usando um arquivo **.install**. Por exemplo, se um pacote precisa de configurações extras para funcionar, as direções devem ser incluídas neste arquivo.
*   Qualquer **dependência opcional** que não é necessária para executar o pacote ou que faça-o funcionar, não deveria ser incluída; Ao invés disso, a informação deveria ser adicionada ao vetor **optdepends**:

    ```
    optdepends=('cups: printing support'
                'sane: scanners support'
                'libgphoto2: digital cameras support'
                'alsa-lib: sound support'
                'giflib: GIF images support'
                'libjpeg: JPEG images support'
                'libpng: PNG images support')
    ```

    O exemplo acima foi tirado do pacote **wine** do `extra`. A informação do optdepends é automaticamente exibida na instalação/atualização, de forma que tal informação **não** deve ser acrescentada em arquivos .install.

*   Ao criar a **description** para um pacote, não inclua o nome do pacote, em uma forma auto-referenciativa. Por exemplo, "Nedit is a text editor for X11" poderia ser simplificado em "A text editor for X11". Também tente manter as descrições abaixo de 80 caracteres.
*   Tente manter o **tamanho da linha** do PKGBUILD abaixo de 100 caracteres.
*   Onde for possível, **remova linhas vazias** do `PKGBUILD` (`provides`, `replaces`, etc.)
*   É uma prática comum **preservar a ordem** dos campos do `PKGBUILD` informada acima. Apesar disso, isso não é obrigatório, sendo o único requisito neste contexto a **corretude da sintaxe bash**.

## Nomenclatura de pacotes

*   Nomes de pacotes devem conter **caracteres alfanuméricos, somente**; todas as letras devem ser **minúsculas**.
*   Versões de pacotes **devem ser a mesma que a versão lança para autor**. Versões podem incluir letras, se for necessário (ex: a versão do nmap é 2.54BETA32). **A versão não pode incluir hífens!** Letras, números e pontos, somente.
*   Lançamento ("releases") de pacotes são **específicos de pacotes do Arch Linux**. Eles permitem a usuários diferenciar entre compilações de pacotes mais novas das mais antigas. Quando uma nova versão de software do pacote foi lançada, o **contador de lançamento recomeça em 1**. Então, na medida em que correções e otimizações forem feitas, o pacote será **re-relançado** para o público do Arch Linux e o **número de lançamento será incrementado**. Quando uma nova versão for lançada, o contador de lançamento será reiniciado para 1\. O número do lançamento do pacote segue a **mesma restrição de nomenclatura da versão do pacote**.

## Diretórios

*   **Arquivos de configuração** devem ser mantidos dentro do diretório `/etc`. Se há mais de um arquivo de configuração, é costumeiro **usar um subdiretório** para manter a área do `/etc` o mais limpo possível. Use `/etc/{pkgname}/`, sendo `{pkgname}` o nome do pacote (ou uma alternativa adequada, p.ex., o apache usa `/etc/httpd/`).
*   Os arquivos de pacotes devem seguir essas **diretrizes gerais de diretórios**:

| `/etc` | 

Arquivos de configuração **essenciais para o sistema**

 |
| `/usr/bin` | Binários de aplicativos |
| `/usr/sbin` | Binários do sistema |
| `/usr/lib` | Bibliotecas |
| `/usr/include` | Arquivos headers |
| `/usr/lib/{pkg}` | Módulos, plug-ins etc. |
| `/usr/share/doc/{pkg}` | Documentação de aplicativos |
| `/usr/share/info` | Arquivos de sistema do GNU Info |
| `/usr/share/man` | Páginas Man |
| `/usr/share/{pkg}` | Dados de aplicativos |
| `/var/lib/{pkg}` | Armazenamento persistente de aplicativos |
| `/etc/{pkg}` | Arquivos de configuração do `{pkg}` |
| `/opt/{pkg}` | 

Pacotes grandes contendo todos os seus arquivos, como o Java, etc.

 |

*   Pacotes não devem conter os diretórios abaixo:
    *   /dev
    *   /home
    *   /srv
    *   /media
    *   /mnt
    *   /proc
    *   /root
    *   /selinux
    *   /sys
    *   /tmp
    *   /var/tmp

## Tarefas do Makepkg

Quando [makepkg](/index.php/Makepkg "Makepkg") é usado para criar um pacote, ele automaticamente faz o seguinte:

1.  Verifica se as dependências (**dependencies**) e dependências em tempo de compilação (**makedepends**) do pacote estão instaladas
2.  **Baixar os arquivos fontes** dos servidores
3.  **Verifica a integridade** de arquivos fonte
4.  **Descompacta** os arquivos fonte
5.  Realiza qualquer **patch** necessário
6.  **Compila** o software e instala-o em um fakeroot (ambiente falso)
7.  Remove (**strips**) símbolos de binários
8.  Remove (**strips**) símbolos de depuração de biblotecas
9.  **Compacta** páginas de manual e/ou info
10.  Gera o **meta-arquivo de pacote**, o qual é incluído em cada pacote
11.  **Compresses** the fake root into the package file
12.  **Armazena** o arquivo de pacote no diretório configurado (por padrão, no cwd)

## Arquiteturas

O vetor `arch` deve conter `'i686'` e/ou `'x86_64'`, dependendo de quais arquiteturas o pacote pode ser compilado. Você também pode usar `'any'` para pacotes que independem de arquitetura.

## Licenças

A variável de vetor [license](/index.php/Licenses "Licenses") está sendo implementada nos repositórios oficiais, e ela **deve** ser usada em seus pacotes da mesma forma. Use-a da seguinte forma:

*   Um pacote de licenças foi criado no [core] armazenando as licenças comuns em /usr/share/licenses/common (ex: /usr/share/licenses/common/GPL). Se um pacote está licenciado sbo uma dessas licenças, a variável de licenças deve ser definido com o nome do diretório, p. ex: license=('GPL')
*   Se a licença apropriada não estiver incluída no pacote oficial de licenças, várias coisas devem ser feitas:
    1.  Os arquivos de licença devem ser incluídos em /usr/share/licenses/$pkgname/. Por exemplo: /usr/share/licenses/dibfoo/LICENSE. Uma ótima forma de fazer isso é usando: `install -D -m644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"` 
    2.  Se o tarball fonte NÃO contém os detalhes da licenças e a licença é exibida somente no site, por exemplo, então copie a licença para um arquivo e inclua-o no pacote. Lembre-se de chamar este arquivo de forma apropriada também.
    3.  Adicione 'custom' no vetor de licenças. Opcionalmente, você pode substituir 'custom' com 'custom:"nome da licença"'.
*   Quando uma licença é usada em um ou mais pacotes no repositório oficial, incluindo [community], ela vira uma licença comum
*   As licenças MIT, BSD, zlib/libpng e Python são casos especiais e não podem ser incluidos no pacote de licenças "comuns". Do ponto de vista da variável de licenças, deve ser tratado com uma licença comum (license=('BSD'), license=('MIT'), license=('ZLIB') ou license=('Python')), mas do ponto de vista do sistema de arquivos, é uma variável personalizada, porque cada licença terá sua própria linha de copyright. Cada pacote licenciado com MIT, BSD, zlib/libpng ou Python devem ter seus locais únicos de armazenamento em /usr/share/licenses/$pkgname/.
*   Alguns pacotes podem não estar cobertos por uma única licença. Nesses casos, várias entradas pode ser feitas no vetor license, p. ex.: license=("GPL" "custom:alguma-licença-comercial"). Para a maioria dos pacotes, essas licenças funcionam de em situações diferentes, ao contrário de se aplicarem ao mesmo tempo. Quando pacman tiver a habilidade de filtrar licenças (para que você possa dizer, "Eu quero somente softwares licenciados com GPL e BSD") duas (ou mais) licenças serão tratadas pelo pacman usando o operador lógico OU, ao invés de E, de forma que o pacman vai considerar o exemplo anterior como um software licenciado via GPL, independentemente das outras licenças listadas.
*   A (L)GPL tem várias versões e permutações dessas versões. Para softwares (L)GPL, a conveção é:
    *   (L)GPL - (L)GPLv2 ou qualquer versão posterior
    *   (L)GPL2 - (L)GPL2 somente
    *   (L)GPL3 - (L)GPL3 ou qualquer versão posterior

## Enviando pacotes para o AUR

Note o seguinte antes de enviar qualquer pacote para o AUR:

1.  Os PKGBUILDs enviados **NÃO DEVEM** compilar aplicativos já disponíveis em qualquer dos repositórios oficiais de binários em circunstância nenhuma. Excepção a esta estrita regra pode ser somente para pacotes que tenham recursos extras e/ou pacthes em comparação com as versões oficiais. Nesta ocasição, a variável de vetor pkgname deve ser diferente para expressar esta diferença. Por exemplo, Um PKGBUILD do GNU screen enviado contendo patch para a barra lateral (sidebar), poderia ser chamado de screen-sidebar etc. Além disso, a variável de vetor **provides=('screen')** deve estar definida no PKGBUILD de forma a evitar conflito com o pacote oficial.
2.  Para conferir segurança aos pacotes enviados para o AUR please **certifique-se** de que você preencheu corretamente o campo de `md5sum`. Os `md5sum`s podem ser gerados usando o comando `makepkg -g`.
3.  Por favor **adicione uma linha de comentário** ao topo do arquivo `PKGBUILD` que siga este formato. Lembre-se de disfarçar seu e-mail para se proteger de spams: `# Maintainer: Seu Nome <endereço at domínio ponto com>` 

    Se você está assumindo o papel de mantenedor de um PKGBUILD existente, adicione sdeu nome no topo como descrito abaixo e altere o título do mantenedor (Maintainer) para contribuidor (Contributor):

    ```
    # Maintainer: Seu Nome <endereço at domínio ponto com>
    # Contributor: Nome Anterior <endereço at domínio ponto com>
    ```

4.  Verifique as **dependências** do pacote (p.ex.: execute `ldd` nos executáveis dinâmicos, verifique as ferramentas necessárias por scripts, etc). A equipe de TUs recomenda **fortemente** o uso do utilitário `namcap`, escrito por [Jason Chu](https://www.archlinux.org/fellows/#jason), para analisar a sanidade dos pacotes. O `namcap` vai avisar você sobre permissões incorretas, dependências faltando, dependências desnecessárias, e outros erros comuns. Você pode instalar o pacote `namcap` com o `pacman`. Lembre-se de que o `namcap` pode ser usado para verificar tanto os arquivos pkg.tar.gz quanto os PKGBUILDs
5.  As **dependências** são a maioria dos erros de empacotamento. Namcap pode ajudar a detectar tais erros, mas nem sempre está correto. Verifique as dependências consultando na documentação do código fonte e no site do programa.
6.  **Não use o `replaces`** em um PKGBUILD a não ser que o pacote tenha sido renomeado, como, por exemplo, quando _Ethereal_ se tornou _Wireshark_. Se o pacote é uma versão alternativa de um pacote já existente, use `conflicts` (e `provides`, se aquele pacote é necessário por outros). A diferença principal é: depois de sincronizar (-Sy), o pacman vai imediatamente querer substituir um pacote instalado, sobrescrevendo-o pelo pacote encontrado com o correspondente `replaces` onde quer que esteja nos repositórios; O `conflicts`, por outro lado, será somente avaliado quando se estiver instalado o pacote, que é o comportamento desejado porque é menos invasivo.
7.  Todos os arquivos enviados para o AUR devem conter um **arquivo tar compactado** contendo um diretório com o **`PKGBUILD`** e **arquivos de compilação adicionais** (patches, install etc.).

    ```
    foo/PKGBUILD
    foo/foo.install
    foo/foo_bar.diff
    foo/foo.rc.conf
    ```

    O nome do arquivo deve conter o nome do pacote, como, por exemplo, foo.tar.gz.

    Pode-se facilmente criar um tarball contendo todos os arquivos necessários usando `makepkg --source`. Isso vai criar um tarball chamado `$pkgname-$pkgver-$pkgrel.src.tar.gz`, o qual pode então ser enviado para o AUR.

    O tarball **não pode** conter o tarball de binário criado pelo makepkg, nem deveria conter a lista de arquivos

## Diretrizes adicionais

Ceritique-se de ler primeiro as diretrizes acima - pontos importantes são listados nesta página e que não serão repetidos nas páginas de diretrizes a seguir. As diretrizes específicas abaixo têm a intenção de ser um adicionar aos padrões listados nesta.

### Pacotes de CVS (SVN, GIT, HG etc.)

Por favor, ver as [diretrizes de PKGBUILD de CVS do Arch](/index.php/Arch_CVS_%26_SVN_PKGBUILD_guidelines "Arch CVS & SVN PKGBUILD guidelines")

### Pacotes de plug-ins do Eclipse

Por favor, ver as [diretrizes de pacotes de plug-ins do Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines")

### Pacotes de GNOME

Por favor, ver as [diretrizes de pacotes do GNOME](/index.php/GNOME_Package_Guidelines "GNOME Package Guidelines")

### Pacotes de Go

Por favor, ver as [diretrizes de pacotes de Go](/index.php/Go_Package_Guidelines "Go Package Guidelines")

### Pacotes de Haskell

Por favor, ver as [diretrizes de pacotes de Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines")

### Pacotes de Java

Por favor, ver as [diretrizes de pacotes de Java](/index.php/Java_Package_Guidelines "Java Package Guidelines")

### Pacotes do KDE

Por favor, ver as [diretrizes de pacotes do KDE](/index.php/KDE_Package_Guidelines "KDE Package Guidelines")

### Pacotes de módulos de kernel

Por favor, ver as [diretrizes de pacotes de módulos do kernel](/index.php/Kernel_Module_Package_Guidelines "Kernel Module Package Guidelines")

### Pacotes de Lisp

Por favor, ver as [diretrizes de pacotes de Lisp](/index.php/Lisp_Package_Guidelines "Lisp Package Guidelines")

### Pacotes de OCaml

Por favor, ver as [diretrizes de pacotes de Ocaml](/index.php/OCaml_Package_Guidelines "OCaml Package Guidelines")

### Pacotes de Perl

Por favor, ver as [diretrizes de pacotes de Perl](/index.php/Perl_Package_Guidelines "Perl Package Guidelines")

### Pacotes de Python

Por favor, ver as [diretrizes de pacotes de Python](/index.php/Python_Package_Guidelines "Python Package Guidelines")

### Pacotes de Ruby Gem

Por favor, ver as [diretrizes de pacotes de Ruby Gem](/index.php/Ruby_Gem_Package_Guidelines "Ruby Gem Package Guidelines")

### Pacotes de Wine

Por favor, ver as [diretrizes de pacotes de Wine](/index.php/Arch_wine_PKGBUILD_guidelines "Arch wine PKGBUILD guidelines")

### Pacotes de MinGW

Por favor, ver as [diretrizes de pacotes de MingW](/index.php/MinGW_PKGBUILD_guidelines "MinGW PKGBUILD guidelines")