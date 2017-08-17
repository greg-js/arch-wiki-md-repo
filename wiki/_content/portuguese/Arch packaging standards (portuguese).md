Ao compilar pacotes para o Arch Linux, **siga as diretrizes de empacotamento** abaixo, especialmente se a intenção é **contribuir** com um novo pacote para o Arch Linux. Você também deve ler as páginas de manual do [PKGBUILD](https://archlinux.org/pacman/PKGBUILD.5.html) e do [makepkg](https://archlinux.org/pacman/makepkg.8.html).

## Contents

*   [1 Protótipo de PKGBUILD](#Prot.C3.B3tipo_de_PKGBUILD)
*   [2 Etiqueta de pacotes](#Etiqueta_de_pacotes)
*   [3 Nomenclatura de pacotes](#Nomenclatura_de_pacotes)
*   [4 Diretórios](#Diret.C3.B3rios)
*   [5 Tarefas do Makepkg](#Tarefas_do_Makepkg)
*   [6 Arquiteturas](#Arquiteturas)
*   [7 Licenças](#Licen.C3.A7as)
*   [8 Diretrizes adicionais](#Diretrizes_adicionais)

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
md5sums=() #gerado com updpkgsums

build() {
  cd "$pkgname-$pkgver"

  ./configure --prefix=/usr
  make
}

package() {
  cd "$pkgname-$pkgver"

  make DESTDIR="$pkgdir/" install
}
```

Outros protótipos podem ser encontrados em `/usr/share/pacman` dos pacotes pacman e abs.

## Etiqueta de pacotes

*   Os pacotes **jamais** devem ser instalados em `/usr/local`
*   **Não introduza novas variáveis ou funções** em scripts de compilação `PKGBUILD`, a menos que o pacote não possa ser compilado sem elas, pois elas podem **conflitar** com variáveis ou funções usadas pelo próprio makepkg.
*   Se uma nova variável ou uma nova função for absolutamente necessária, **prefixe seu nome com um caractere de sublinhado** (`_`), ex: `_variavelpersonalizada=` 
*   O campo `packager` do meta-arquivo do pacote pode ser **personalizado** pelo compilador do pacote, modificando a opção apropriada no arquivo `/etc/makepkg.conf` ou, alternativamente, sobrescrevendo-o com a criação de um ~/.makepkg.conf
*   Todas as mensagens importantes devem ser exibidas durante a instalação usando um **arquivo .install**. Por exemplo, se um pacote precisa de configurações extras para funcionar, as direções devem ser incluídas neste arquivo.
*   **Dependências** são os erros mais comuns de empacotamento. Por favor, invista um tempo em verificá-las cuidadosamente, por exemplo executando `ldd` em executáveis dinâmicos, verificando ferramentas necessárias por scripts ou olhando documentação do software. O utilitário [namcap](/index.php/Namcap "Namcap") pode lhe ajudar neste assunto. Essa ferramenta pode analisar ambos PKGBUILD e o tarball de pacote resultante e vai avisar você sobre permissões erradas, dependências em falta, dependências redundantes e outros erros comuns.
*   Quaisquer **dependências opcionais** que não são necessárias para executar o pacote ou que faça-o funcionar, não devem ser incluídas no vetor **depends**; em vez disso, a informação deve ser adicionada ao vetor **optdepends**:

```
optdepends=('cups: printing support'
            'sane: scanners support'
            'libgphoto2: digital cameras support'
            'alsa-lib: sound support'
            'giflib: GIF images support'
            'libjpeg: JPEG images support'
            'libpng: PNG images support')

```

	O exemplo acima foi tirado do pacote **wine** do `extra`. A informação do optdepends é automaticamente exibida na instalação/atualização, de forma que tal informação **não** deve-se manter esse tipo de informação em arquivos `.install`.

*   Ao criar a **descrição de pacote** para um pacote, não inclua o nome do pacote, em uma forma autorreferenciativa. Por exemplo, "Nedit is a text editor for X11" poderia ser simplificado em "A text editor for X11". Também tente manter as descrições abaixo de 80 caracteres.
*   Tente manter o **tamanho da linha** do PKGBUILD abaixo de 100 caracteres.
*   Onde for possível, **remova linhas vazias** do `PKGBUILD` (`provides`, `replaces`, etc.)
*   É uma prática comum **preservar a ordem** dos campos do `PKGBUILD` informada acima. Porém, isso não é obrigatório, sendo o único requisito neste contexto a **correção da sintaxe bash**.
*   **Envolva com aspas** as variáveis que podem conter espaços, tal como `"$pkgdir"` e `"$srcdir"`.
*   Para garantir a **integridade** de pacotes, certifique-se que as [variáveis de integridade](/index.php/PKGBUILD_(Portugu%C3%AAs)#Integridade "PKGBUILD (Português)") contêm os valores corretos. Essas podem ser atualizadas usando a ferramenta `updpkgsums`.

## Nomenclatura de pacotes

*   Nomes de pacotes pode conter apenas caracteres alfanuméricos e algum entre `@`, `.`, `_`, `+`, `-`. Nomes não podem iniciar com hífenes ou pontos. Todas as letras devem ser **minúsculas**.
*   Nomes de pacotes NÃO devem ser sufixados com o número de versão principal de lançamento do upstream (ex.: não queremos libfoo2 se upstream chama-o de libfoo v2.3.4) no caso da biblioteca e suas dependências esperadas para serem capazes de manter o uso da maioria das versões recentes de biblioteca com cada lançamento do upstream. Porém, para alguns softwares ou dependências, isso não pode ser presumido. No passado, isso foi especialmente verdadeiro para kits de ferramentas de widget, tal como GTK ou Qt. Softwares que depende em tais kits de ferramentas geralmente podem não ser trivialmente portadas para uma nova versão maior. Como tal, em casos em que softwares podem, trivialmente, se manter funcionando junto com suas dependências, nomes de pacotes devem carregar o sufixo da versão maior (ex.: gtk2, gtk3, qt4, qt5). Para casos em que a maioria das dependências podem se manter funcionando junto com lançamentos mais novos, mas alguns não podem (por exemplo, código fechado que precisa de libpng12 ou similar), uma versão obsoleta daquele pacote pode ser chamado de libfoo1 enquanto a versão atual é apenas libfoo.

*   Versões de pacotes **devem ser as mesmas que a versão lançada pelo autor**. Versões podem incluir letras, se for necessário (ex: a versão do nmap é 2.54BETA32). **Tags de versão não podem incluir hífens!** Letras, números e pontos, somente.
*   Lançamentos de pacotes são **específicos de pacotes do Arch Linux**. Eles permitem a usuários diferenciar entre compilações de pacotes mais novas das mais antigas. Quando uma nova versão de software do pacote é lançada, o **contador de lançamento recomeça em 1**. Então, na medida em que correções e otimizações forem feitas, o pacote será **relançado** para o público do Arch Linux e o **número de lançamento será incrementado**. Quando uma nova versão for lançada, o contador de lançamento será reiniciado para 1\. As tags de lançamento do pacote seguem as **mesmas restrições de nomenclatura que tags de versão**.

## Diretórios

*   **Arquivos de configuração** devem ser mantidos dentro do diretório `/etc`. Se há mais de um arquivo de configuração, é costumeiro **usar um subdiretório** para manter a área do `/etc` o mais limpo possível. Use `/etc/{pkgname}/`, sendo `{pkgname}` o nome do pacote (ou uma alternativa adequada, p.ex., o apache usa `/etc/httpd/`).

*   Arquivos de pacotes devem seguir essas **diretrizes gerais de diretórios**:

| `/etc` | Arquivos de configuração **essenciais para o sistema** |
| `/usr/bin` | Binários |
| `/usr/lib` | Bibliotecas |
| `/usr/include` | Arquivos cabeçalhos (*headers*) |
| `/usr/lib/{pkg}` | Módulos, plug-ins, etc. |
| `/usr/share/doc/{pkg}` | Documentação de aplicativo |
| `/usr/share/info` | Arquivos de sistema do GNU Info |
| `/usr/share/man` | Páginas de manual (*man*) |
| `/usr/share/{pkg}` | Dados de aplicativo |
| `/var/lib/{pkg}` | Armazenamento persistente de aplicativo |
| `/etc/{pkg}` | Arquivos de configuração de `{pkg}` |
| `/opt/{pkg}` | Pacotes grandes contendo todos os seus arquivos |

*   Pacotes não devem conter os diretórios abaixo:
    *   `/bin`
    *   `/sbin`
    *   `/dev`
    *   `/home`
    *   `/srv`
    *   `/media`
    *   `/mnt`
    *   `/proc`
    *   `/root`
    *   `/selinux`
    *   `/sys`
    *   `/tmp`
    *   `/var/tmp`
    *   `/run`

## Tarefas do Makepkg

Quando [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") é usado para compilar um pacote, ele automaticamente faz o seguinte:

1.  Verifica se as dependências (**depends**) e dependências em tempo de compilação (**makedepends**) do pacote estão instaladas
2.  **Baixa os arquivos fontes** dos servidores
3.  **Verifica a integridade** de arquivos fonte
4.  **Descompacta** os arquivos fonte
5.  Realiza qualquer **patching** necessário
6.  **Compila** o software e instala-o em um *fakeroot*
7.  Remove (**strips**) símbolos de binários
8.  Remove (**strips**) símbolos de depuração de bibliotecas
9.  **Compacta** páginas de manual e/ou info
10.  Gera o **meta-arquivo de pacote**, o qual é incluído em cada pacote
11.  **Compacta** o *fakeroot* no arquivo de pacote
12.  **Armazena** o arquivo de pacote no diretório de destino configurado (por padrão, cwd)

## Arquiteturas

O vetor `arch` deve conter `'i686'` e/ou `'x86_64'`, dependendo de em quais arquiteturas o pacote pode ser compilado. Você também pode usar `'any'` para pacotes que independem de arquitetura.

## Licenças

Veja [PKGBUILD#license](/index.php/PKGBUILD_(Portugu%C3%AAs)#license "PKGBUILD (Português)").

## Diretrizes adicionais

Ceritique-se de ler primeiro as diretrizes acima - pontos importantes são listados nesta página e que não serão repetidos nas páginas de diretrizes a seguir. As diretrizes específicas abaixo têm a intenção de ser um adicionar aos padrões listados nesta.

**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

Pacotes enviados ao AUR também devem estar em conformidade com as [regras de envio](/index.php/Arch_User_Repository_(Portugu%C3%AAs)#Regras_de_envio "Arch User Repository (Português)").